## Seq2Seq-DSL Training for 500 Epochs (my-rk, rk-my)

```
time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
--lang myrk \
--gpu_id 0 --batch_size 64 --n_epochs 500 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
--dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
--lm_fn  ./model/lm/lm-200epoch.pth \
--model_fn ./model/dsl/seq2seq/myrk-500epoch/seq2seq-dsl-500epoch-model-myrk.pth | tee ./model/dsl/seq2seq/myrk-500epoch/training.log;  
```

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
> --lang myrk \
> --gpu_id 0 --batch_size 64 --n_epochs 500 --max_length 100 --dropout .2 \
> --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
> --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
> --lm_fn ./model/lm/lm-200epoch.pth \
> --model_fn ./model/dsl/seq2seq/myrk-500epoch/seq2seq-dsl-500epoch-model-myrk.pth | tee ./model/dsl/seq2seq/myrk-500epoch/training.log;
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.01,
    'dsl_n_warmup_epochs': 20,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lm_fn': './model/lm/lm-200epoch.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/seq2seq/myrk-500epoch/seq2seq-dsl-500epoch-model-myrk.pth',
    'n_epochs': 500,
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
Epoch 1 - |param|=9.07e+02 |g_param|=2.91e+05 loss_x2y=4.4127e+00 ppl_x2y=82.49 loss_y2x=4.4392e+00 ppl_y2x=84.71 dual_loss=0.0000e+00
Validation X2Y - loss=4.0409e+00 ppl=56.88 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0692e+00 ppl=58.51 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.08e+02 |g_param|=2.40e+05 loss_x2y=4.1359e+00 ppl_x2y=62.54 loss_y2x=4.1576e+00 ppl_y2x=63.92 dual_loss=0.0000e+00
Validation X2Y - loss=3.8946e+00 ppl=49.13 best_loss=4.0409e+00 best_ppl=56.88                                          
Validation Y2X - loss=3.9193e+00 ppl=50.36 best_loss=4.0692e+00 best_ppl=58.51
Epoch 3 - |param|=9.08e+02 |g_param|=2.49e+05 loss_x2y=4.0338e+00 ppl_x2y=56.47 loss_y2x=4.0639e+00 ppl_y2x=58.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.7986e+00 ppl=44.64 best_loss=3.8946e+00 best_ppl=49.13                                          
Validation Y2X - loss=3.8247e+00 ppl=45.82 best_loss=3.9193e+00 best_ppl=50.36
Epoch 4 - |param|=9.08e+02 |g_param|=2.64e+05 loss_x2y=3.9324e+00 ppl_x2y=51.03 loss_y2x=3.9563e+00 ppl_y2x=52.26 dual_loss=0.0000e+00
Validation X2Y - loss=3.6850e+00 ppl=39.84 best_loss=3.7986e+00 best_ppl=44.64                                          
Validation Y2X - loss=3.7298e+00 ppl=41.67 best_loss=3.8247e+00 best_ppl=45.82
Epoch 5 - |param|=9.09e+02 |g_param|=2.51e+05 loss_x2y=3.8096e+00 ppl_x2y=45.13 loss_y2x=3.8387e+00 ppl_y2x=46.47 dual_loss=0.0000e+00
Validation X2Y - loss=3.5754e+00 ppl=35.71 best_loss=3.6850e+00 best_ppl=39.84                                          
Validation Y2X - loss=3.6052e+00 ppl=36.79 best_loss=3.7298e+00 best_ppl=41.67
Epoch 6 - |param|=9.09e+02 |g_param|=2.78e+05 loss_x2y=3.7060e+00 ppl_x2y=40.69 loss_y2x=3.7115e+00 ppl_y2x=40.92 dual_loss=0.0000e+00
Validation X2Y - loss=3.5131e+00 ppl=33.55 best_loss=3.5754e+00 best_ppl=35.71                                          
Validation Y2X - loss=3.5059e+00 ppl=33.31 best_loss=3.6052e+00 best_ppl=36.79
Epoch 7 - |param|=9.10e+02 |g_param|=2.25e+05 loss_x2y=3.6225e+00 ppl_x2y=37.43 loss_y2x=3.5488e+00 ppl_y2x=34.77 dual_loss=0.0000e+00
Validation X2Y - loss=3.4038e+00 ppl=30.08 best_loss=3.5131e+00 best_ppl=33.55                                          
Validation Y2X - loss=3.2970e+00 ppl=27.03 best_loss=3.5059e+00 best_ppl=33.31
Epoch 8 - |param|=9.11e+02 |g_param|=2.52e+05 loss_x2y=3.5244e+00 ppl_x2y=33.93 loss_y2x=3.3698e+00 ppl_y2x=29.07 dual_loss=0.0000e+00
Validation X2Y - loss=3.2955e+00 ppl=26.99 best_loss=3.4038e+00 best_ppl=30.08                                          
Validation Y2X - loss=3.0890e+00 ppl=21.95 best_loss=3.2970e+00 best_ppl=27.03
Epoch 9 - |param|=9.12e+02 |g_param|=1.92e+05 loss_x2y=3.3333e+00 ppl_x2y=28.03 loss_y2x=3.0184e+00 ppl_y2x=20.46 dual_loss=0.0000e+00
Validation X2Y - loss=3.0904e+00 ppl=21.99 best_loss=3.2955e+00 best_ppl=26.99                                          
Validation Y2X - loss=2.7550e+00 ppl=15.72 best_loss=3.0890e+00 best_ppl=21.95
Epoch 10 - |param|=9.13e+02 |g_param|=2.53e+05 loss_x2y=3.1544e+00 ppl_x2y=23.44 loss_y2x=2.7798e+00 ppl_y2x=16.12 dual_loss=0.0000e+00
Validation X2Y - loss=2.9707e+00 ppl=19.51 best_loss=3.0904e+00 best_ppl=21.99                                          
Validation Y2X - loss=2.5616e+00 ppl=12.96 best_loss=2.7550e+00 best_ppl=15.72
Epoch 11 - |param|=9.14e+02 |g_param|=2.06e+05 loss_x2y=2.9106e+00 ppl_x2y=18.37 loss_y2x=2.4890e+00 ppl_y2x=12.05 dual_loss=0.0000e+00
Validation X2Y - loss=2.7546e+00 ppl=15.71 best_loss=2.9707e+00 best_ppl=19.51                                          
Validation Y2X - loss=2.3430e+00 ppl=10.41 best_loss=2.5616e+00 best_ppl=12.96
Epoch 12 - |param|=9.15e+02 |g_param|=2.61e+05 loss_x2y=2.7784e+00 ppl_x2y=16.09 loss_y2x=2.4140e+00 ppl_y2x=11.18 dual_loss=0.0000e+00
Validation X2Y - loss=2.7659e+00 ppl=15.89 best_loss=2.7546e+00 best_ppl=15.71                                          
Validation Y2X - loss=2.1896e+00 ppl=8.93 best_loss=2.3430e+00 best_ppl=10.41
Epoch 13 - |param|=9.16e+02 |g_param|=1.48e+05 loss_x2y=2.6078e+00 ppl_x2y=13.57 loss_y2x=2.2120e+00 ppl_y2x=9.13 dual_loss=0.0000e+00
Validation X2Y - loss=2.4021e+00 ppl=11.05 best_loss=2.7546e+00 best_ppl=15.71                                          
Validation Y2X - loss=2.0252e+00 ppl=7.58 best_loss=2.1896e+00 best_ppl=8.93
Epoch 14 - |param|=9.17e+02 |g_param|=2.09e+05 loss_x2y=2.3973e+00 ppl_x2y=10.99 loss_y2x=2.1567e+00 ppl_y2x=8.64 dual_loss=0.0000e+00
Validation X2Y - loss=2.2530e+00 ppl=9.52 best_loss=2.4021e+00 best_ppl=11.05                                           
Validation Y2X - loss=2.0655e+00 ppl=7.89 best_loss=2.0252e+00 best_ppl=7.58
Epoch 15 - |param|=9.18e+02 |g_param|=1.40e+05 loss_x2y=2.1196e+00 ppl_x2y=8.33 loss_y2x=1.8404e+00 ppl_y2x=6.30 dual_loss=0.0000e+00
Validation X2Y - loss=2.0638e+00 ppl=7.88 best_loss=2.2530e+00 best_ppl=9.52                                            
Validation Y2X - loss=1.8093e+00 ppl=6.11 best_loss=2.0252e+00 best_ppl=7.58
Epoch 16 - |param|=9.19e+02 |g_param|=2.09e+05 loss_x2y=2.1475e+00 ppl_x2y=8.56 loss_y2x=1.7977e+00 ppl_y2x=6.04 dual_loss=0.0000e+00
Validation X2Y - loss=2.0037e+00 ppl=7.42 best_loss=2.0638e+00 best_ppl=7.88                                            
Validation Y2X - loss=1.7294e+00 ppl=5.64 best_loss=1.8093e+00 best_ppl=6.11
Epoch 17 - |param|=9.19e+02 |g_param|=1.83e+05 loss_x2y=1.8551e+00 ppl_x2y=6.39 loss_y2x=1.6341e+00 ppl_y2x=5.12 dual_loss=0.0000e+00
Validation X2Y - loss=1.8200e+00 ppl=6.17 best_loss=2.0037e+00 best_ppl=7.42                                            
Validation Y2X - loss=1.5823e+00 ppl=4.87 best_loss=1.7294e+00 best_ppl=5.64
Epoch 18 - |param|=9.20e+02 |g_param|=1.82e+05 loss_x2y=1.6825e+00 ppl_x2y=5.38 loss_y2x=1.6190e+00 ppl_y2x=5.05 dual_loss=0.0000e+00
Validation X2Y - loss=1.7162e+00 ppl=5.56 best_loss=1.8200e+00 best_ppl=6.17                                            
Validation Y2X - loss=1.5172e+00 ppl=4.56 best_loss=1.5823e+00 best_ppl=4.87
Epoch 19 - |param|=9.21e+02 |g_param|=1.71e+05 loss_x2y=1.6207e+00 ppl_x2y=5.06 loss_y2x=1.4359e+00 ppl_y2x=4.20 dual_loss=0.0000e+00
Validation X2Y - loss=1.6079e+00 ppl=4.99 best_loss=1.7162e+00 best_ppl=5.56                                            
Validation Y2X - loss=1.4188e+00 ppl=4.13 best_loss=1.5172e+00 best_ppl=4.56
Epoch 20 - |param|=9.22e+02 |g_param|=1.59e+05 loss_x2y=1.4829e+00 ppl_x2y=4.41 loss_y2x=1.3972e+00 ppl_y2x=4.04 dual_loss=0.0000e+00
Validation X2Y - loss=1.5394e+00 ppl=4.66 best_loss=1.6079e+00 best_ppl=4.99                                            
Validation Y2X - loss=1.4305e+00 ppl=4.18 best_loss=1.4188e+00 best_ppl=4.13
Epoch 21 - |param|=9.23e+02 |g_param|=1.30e+05 loss_x2y=1.3630e+00 ppl_x2y=3.91 loss_y2x=1.3624e+00 ppl_y2x=3.91 dual_loss=1.4951e+00
Validation X2Y - loss=1.4305e+00 ppl=4.18 best_loss=1.5394e+00 best_ppl=4.66                                            
Validation Y2X - loss=1.6100e+00 ppl=5.00 best_loss=1.4188e+00 best_ppl=4.13
Epoch 22 - |param|=9.23e+02 |g_param|=1.78e+05 loss_x2y=1.4794e+00 ppl_x2y=4.39 loss_y2x=1.4280e+00 ppl_y2x=4.17 dual_loss=1.4279e+00
Validation X2Y - loss=1.5029e+00 ppl=4.49 best_loss=1.4305e+00 best_ppl=4.18                                            
Validation Y2X - loss=1.2886e+00 ppl=3.63 best_loss=1.4188e+00 best_ppl=4.13
Epoch 23 - |param|=9.24e+02 |g_param|=9.97e+04 loss_x2y=1.2486e+00 ppl_x2y=3.49 loss_y2x=1.1750e+00 ppl_y2x=3.24 dual_loss=6.9528e-01
Validation X2Y - loss=1.3033e+00 ppl=3.68 best_loss=1.4305e+00 best_ppl=4.18                                            
Validation Y2X - loss=1.2036e+00 ppl=3.33 best_loss=1.2886e+00 best_ppl=3.63
Epoch 24 - |param|=9.25e+02 |g_param|=1.13e+05 loss_x2y=1.1905e+00 ppl_x2y=3.29 loss_y2x=1.3239e+00 ppl_y2x=3.76 dual_loss=1.9074e+00
Validation X2Y - loss=1.2458e+00 ppl=3.48 best_loss=1.3033e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2162e+00 ppl=3.37 best_loss=1.2036e+00 best_ppl=3.33
Epoch 25 - |param|=9.25e+02 |g_param|=8.29e+04 loss_x2y=1.0506e+00 ppl_x2y=2.86 loss_y2x=1.0435e+00 ppl_y2x=2.84 dual_loss=7.7661e-01
Validation X2Y - loss=1.1738e+00 ppl=3.23 best_loss=1.2458e+00 best_ppl=3.48                                            
Validation Y2X - loss=1.0993e+00 ppl=3.00 best_loss=1.2036e+00 best_ppl=3.33
Epoch 26 - |param|=9.26e+02 |g_param|=9.65e+04 loss_x2y=1.0183e+00 ppl_x2y=2.77 loss_y2x=1.0334e+00 ppl_y2x=2.81 dual_loss=7.5042e-01
Validation X2Y - loss=1.1554e+00 ppl=3.18 best_loss=1.1738e+00 best_ppl=3.23                                            
Validation Y2X - loss=1.0741e+00 ppl=2.93 best_loss=1.0993e+00 best_ppl=3.00
Epoch 27 - |param|=9.27e+02 |g_param|=7.85e+04 loss_x2y=9.5453e-01 ppl_x2y=2.60 loss_y2x=9.3667e-01 ppl_y2x=2.55 dual_loss=6.5762e-01
Validation X2Y - loss=1.1106e+00 ppl=3.04 best_loss=1.1554e+00 best_ppl=3.18                                            
Validation Y2X - loss=1.0280e+00 ppl=2.80 best_loss=1.0741e+00 best_ppl=2.93
Epoch 28 - |param|=9.27e+02 |g_param|=6.68e+04 loss_x2y=8.8896e-01 ppl_x2y=2.43 loss_y2x=8.9501e-01 ppl_y2x=2.45 dual_loss=5.5788e-01
Validation X2Y - loss=1.0830e+00 ppl=2.95 best_loss=1.1106e+00 best_ppl=3.04                                            
Validation Y2X - loss=1.0361e+00 ppl=2.82 best_loss=1.0280e+00 best_ppl=2.80
Epoch 29 - |param|=9.28e+02 |g_param|=5.90e+04 loss_x2y=8.8730e-01 ppl_x2y=2.43 loss_y2x=8.6920e-01 ppl_y2x=2.39 dual_loss=5.6062e-01
Validation X2Y - loss=1.0411e+00 ppl=2.83 best_loss=1.0830e+00 best_ppl=2.95                                            
Validation Y2X - loss=9.5112e-01 ppl=2.59 best_loss=1.0280e+00 best_ppl=2.80
Epoch 30 - |param|=9.28e+02 |g_param|=7.26e+04 loss_x2y=8.5153e-01 ppl_x2y=2.34 loss_y2x=8.4443e-01 ppl_y2x=2.33 dual_loss=6.1334e-01
Validation X2Y - loss=1.0461e+00 ppl=2.85 best_loss=1.0411e+00 best_ppl=2.83                                            
Validation Y2X - loss=9.5124e-01 ppl=2.59 best_loss=9.5112e-01 best_ppl=2.59
Epoch 31 - |param|=9.29e+02 |g_param|=8.85e+04 loss_x2y=8.1370e-01 ppl_x2y=2.26 loss_y2x=8.3896e-01 ppl_y2x=2.31 dual_loss=8.1948e-01
Validation X2Y - loss=9.8546e-01 ppl=2.68 best_loss=1.0411e+00 best_ppl=2.83                                            
Validation Y2X - loss=9.4000e-01 ppl=2.56 best_loss=9.5112e-01 best_ppl=2.59
Epoch 32 - |param|=9.29e+02 |g_param|=1.03e+05 loss_x2y=7.9766e-01 ppl_x2y=2.22 loss_y2x=7.8015e-01 ppl_y2x=2.18 dual_loss=9.8746e-01
Validation X2Y - loss=1.0634e+00 ppl=2.90 best_loss=9.8546e-01 best_ppl=2.68                                            
Validation Y2X - loss=9.3090e-01 ppl=2.54 best_loss=9.4000e-01 best_ppl=2.56
Epoch 33 - |param|=9.30e+02 |g_param|=9.89e+04 loss_x2y=9.2073e-01 ppl_x2y=2.51 loss_y2x=8.0536e-01 ppl_y2x=2.24 dual_loss=8.6322e-01
Validation X2Y - loss=9.6193e-01 ppl=2.62 best_loss=9.8546e-01 best_ppl=2.68                                            
Validation Y2X - loss=9.1073e-01 ppl=2.49 best_loss=9.3090e-01 best_ppl=2.54
Epoch 34 - |param|=9.31e+02 |g_param|=5.16e+04 loss_x2y=7.2989e-01 ppl_x2y=2.07 loss_y2x=7.3290e-01 ppl_y2x=2.08 dual_loss=5.3451e-01
Validation X2Y - loss=9.1685e-01 ppl=2.50 best_loss=9.6193e-01 best_ppl=2.62                                            
Validation Y2X - loss=8.6892e-01 ppl=2.38 best_loss=9.1073e-01 best_ppl=2.49
Epoch 35 - |param|=9.31e+02 |g_param|=6.18e+04 loss_x2y=7.1792e-01 ppl_x2y=2.05 loss_y2x=7.7032e-01 ppl_y2x=2.16 dual_loss=7.6655e-01
Validation X2Y - loss=8.8364e-01 ppl=2.42 best_loss=9.1685e-01 best_ppl=2.50                                            
Validation Y2X - loss=8.7388e-01 ppl=2.40 best_loss=8.6892e-01 best_ppl=2.38
Epoch 36 - |param|=9.32e+02 |g_param|=4.33e+04 loss_x2y=6.6422e-01 ppl_x2y=1.94 loss_y2x=6.9514e-01 ppl_y2x=2.00 dual_loss=9.7882e-01
Validation X2Y - loss=8.6988e-01 ppl=2.39 best_loss=8.8364e-01 best_ppl=2.42                                            
Validation Y2X - loss=8.4132e-01 ppl=2.32 best_loss=8.6892e-01 best_ppl=2.38
Epoch 37 - |param|=9.32e+02 |g_param|=4.80e+04 loss_x2y=6.6999e-01 ppl_x2y=1.95 loss_y2x=7.0279e-01 ppl_y2x=2.02 dual_loss=7.1074e-01
Validation X2Y - loss=8.5445e-01 ppl=2.35 best_loss=8.6988e-01 best_ppl=2.39                                            
Validation Y2X - loss=8.8407e-01 ppl=2.42 best_loss=8.4132e-01 best_ppl=2.32
Epoch 38 - |param|=9.33e+02 |g_param|=3.98e+04 loss_x2y=6.0224e-01 ppl_x2y=1.83 loss_y2x=6.1278e-01 ppl_y2x=1.85 dual_loss=4.5231e-01
Validation X2Y - loss=8.5621e-01 ppl=2.35 best_loss=8.5445e-01 best_ppl=2.35                                            
Validation Y2X - loss=8.5149e-01 ppl=2.34 best_loss=8.4132e-01 best_ppl=2.32
Epoch 39 - |param|=9.33e+02 |g_param|=3.30e+04 loss_x2y=6.2799e-01 ppl_x2y=1.87 loss_y2x=6.4005e-01 ppl_y2x=1.90 dual_loss=5.7267e-01
Validation X2Y - loss=8.4583e-01 ppl=2.33 best_loss=8.5445e-01 best_ppl=2.35                                            
Validation Y2X - loss=8.2184e-01 ppl=2.27 best_loss=8.4132e-01 best_ppl=2.32
Epoch 40 - |param|=9.34e+02 |g_param|=2.98e+04 loss_x2y=5.8761e-01 ppl_x2y=1.80 loss_y2x=6.8221e-01 ppl_y2x=1.98 dual_loss=8.8790e-01
Validation X2Y - loss=8.1093e-01 ppl=2.25 best_loss=8.4583e-01 best_ppl=2.33                                            
Validation Y2X - loss=8.5782e-01 ppl=2.36 best_loss=8.2184e-01 best_ppl=2.27
Epoch 41 - |param|=9.34e+02 |g_param|=3.11e+04 loss_x2y=5.6443e-01 ppl_x2y=1.76 loss_y2x=6.4307e-01 ppl_y2x=1.90 dual_loss=6.7237e-01
Validation X2Y - loss=8.2503e-01 ppl=2.28 best_loss=8.1093e-01 best_ppl=2.25                                            
Validation Y2X - loss=8.5530e-01 ppl=2.35 best_loss=8.2184e-01 best_ppl=2.27
Epoch 42 - |param|=9.35e+02 |g_param|=2.36e+04 loss_x2y=5.4853e-01 ppl_x2y=1.73 loss_y2x=5.9640e-01 ppl_y2x=1.82 dual_loss=6.5985e-01
Validation X2Y - loss=7.8551e-01 ppl=2.19 best_loss=8.1093e-01 best_ppl=2.25                                            
Validation Y2X - loss=7.9886e-01 ppl=2.22 best_loss=8.2184e-01 best_ppl=2.27
Epoch 43 - |param|=9.35e+02 |g_param|=2.58e+04 loss_x2y=5.4739e-01 ppl_x2y=1.73 loss_y2x=6.0333e-01 ppl_y2x=1.83 dual_loss=6.1731e-01
Validation X2Y - loss=7.8390e-01 ppl=2.19 best_loss=7.8551e-01 best_ppl=2.19                                            
Validation Y2X - loss=7.7626e-01 ppl=2.17 best_loss=7.9886e-01 best_ppl=2.22
Epoch 44 - |param|=9.36e+02 |g_param|=4.43e+04 loss_x2y=5.6991e-01 ppl_x2y=1.77 loss_y2x=7.9481e-01 ppl_y2x=2.21 dual_loss=1.6906e+00
Validation X2Y - loss=7.7104e-01 ppl=2.16 best_loss=7.8390e-01 best_ppl=2.19                                            
Validation Y2X - loss=8.2236e-01 ppl=2.28 best_loss=7.7626e-01 best_ppl=2.17
Epoch 45 - |param|=9.36e+02 |g_param|=3.15e+04 loss_x2y=5.5018e-01 ppl_x2y=1.73 loss_y2x=6.3948e-01 ppl_y2x=1.90 dual_loss=8.2051e-01
Validation X2Y - loss=7.6096e-01 ppl=2.14 best_loss=7.7104e-01 best_ppl=2.16                                            
Validation Y2X - loss=7.7428e-01 ppl=2.17 best_loss=7.7626e-01 best_ppl=2.17
Epoch 46 - |param|=9.37e+02 |g_param|=4.27e+04 loss_x2y=5.7139e-01 ppl_x2y=1.77 loss_y2x=5.6785e-01 ppl_y2x=1.76 dual_loss=7.3894e-01
Validation X2Y - loss=9.4263e-01 ppl=2.57 best_loss=7.6096e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.5410e-01 ppl=2.13 best_loss=7.7428e-01 best_ppl=2.17
Epoch 47 - |param|=9.37e+02 |g_param|=3.07e+04 loss_x2y=5.5808e-01 ppl_x2y=1.75 loss_y2x=5.3537e-01 ppl_y2x=1.71 dual_loss=4.8498e-01
Validation X2Y - loss=7.8607e-01 ppl=2.19 best_loss=7.6096e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.3939e-01 ppl=2.09 best_loss=7.5410e-01 best_ppl=2.13
Epoch 48 - |param|=9.38e+02 |g_param|=2.45e+04 loss_x2y=5.3959e-01 ppl_x2y=1.72 loss_y2x=5.2228e-01 ppl_y2x=1.69 dual_loss=4.7554e-01
Validation X2Y - loss=7.7613e-01 ppl=2.17 best_loss=7.6096e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.3906e-01 ppl=2.09 best_loss=7.3939e-01 best_ppl=2.09
Epoch 49 - |param|=9.38e+02 |g_param|=1.84e+04 loss_x2y=4.8035e-01 ppl_x2y=1.62 loss_y2x=5.0274e-01 ppl_y2x=1.65 dual_loss=4.0797e-01
Validation X2Y - loss=7.3240e-01 ppl=2.08 best_loss=7.6096e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.4168e-01 ppl=2.10 best_loss=7.3906e-01 best_ppl=2.09
Epoch 50 - |param|=9.38e+02 |g_param|=1.91e+04 loss_x2y=4.4977e-01 ppl_x2y=1.57 loss_y2x=4.8321e-01 ppl_y2x=1.62 dual_loss=5.5967e-01
Validation X2Y - loss=7.4231e-01 ppl=2.10 best_loss=7.3240e-01 best_ppl=2.08                                            
Validation Y2X - loss=7.2542e-01 ppl=2.07 best_loss=7.3906e-01 best_ppl=2.09
Epoch 51 - |param|=9.39e+02 |g_param|=1.57e+04 loss_x2y=4.5407e-01 ppl_x2y=1.57 loss_y2x=4.8157e-01 ppl_y2x=1.62 dual_loss=6.0771e-01
Validation X2Y - loss=7.2771e-01 ppl=2.07 best_loss=7.3240e-01 best_ppl=2.08                                            
Validation Y2X - loss=7.3498e-01 ppl=2.09 best_loss=7.2542e-01 best_ppl=2.07
Epoch 52 - |param|=9.39e+02 |g_param|=1.62e+04 loss_x2y=4.6019e-01 ppl_x2y=1.58 loss_y2x=4.7544e-01 ppl_y2x=1.61 dual_loss=4.1337e-01
Validation X2Y - loss=7.2336e-01 ppl=2.06 best_loss=7.2771e-01 best_ppl=2.07                                            
Validation Y2X - loss=7.2444e-01 ppl=2.06 best_loss=7.2542e-01 best_ppl=2.07
Epoch 53 - |param|=9.40e+02 |g_param|=1.37e+04 loss_x2y=4.1700e-01 ppl_x2y=1.52 loss_y2x=4.4571e-01 ppl_y2x=1.56 dual_loss=4.2202e-01
Validation X2Y - loss=7.3130e-01 ppl=2.08 best_loss=7.2336e-01 best_ppl=2.06                                            
Validation Y2X - loss=7.2791e-01 ppl=2.07 best_loss=7.2444e-01 best_ppl=2.06
Epoch 54 - |param|=9.40e+02 |g_param|=1.40e+04 loss_x2y=4.3378e-01 ppl_x2y=1.54 loss_y2x=4.3677e-01 ppl_y2x=1.55 dual_loss=4.2363e-01
Validation X2Y - loss=7.3206e-01 ppl=2.08 best_loss=7.2336e-01 best_ppl=2.06                                            
Validation Y2X - loss=7.1840e-01 ppl=2.05 best_loss=7.2444e-01 best_ppl=2.06
Epoch 55 - |param|=9.41e+02 |g_param|=1.34e+04 loss_x2y=3.9022e-01 ppl_x2y=1.48 loss_y2x=4.2457e-01 ppl_y2x=1.53 dual_loss=4.6110e-01
Validation X2Y - loss=7.1553e-01 ppl=2.05 best_loss=7.2336e-01 best_ppl=2.06                                            
Validation Y2X - loss=7.2708e-01 ppl=2.07 best_loss=7.1840e-01 best_ppl=2.05
Epoch 56 - |param|=9.41e+02 |g_param|=2.27e+04 loss_x2y=4.2063e-01 ppl_x2y=1.52 loss_y2x=5.3280e-01 ppl_y2x=1.70 dual_loss=9.0216e-01
Validation X2Y - loss=7.0281e-01 ppl=2.02 best_loss=7.1553e-01 best_ppl=2.05                                            
Validation Y2X - loss=8.2343e-01 ppl=2.28 best_loss=7.1840e-01 best_ppl=2.05
Epoch 57 - |param|=9.42e+02 |g_param|=2.68e+04 loss_x2y=4.9143e-01 ppl_x2y=1.63 loss_y2x=7.9031e-01 ppl_y2x=2.20 dual_loss=2.4130e+00
Validation X2Y - loss=7.1758e-01 ppl=2.05 best_loss=7.0281e-01 best_ppl=2.02                                            
Validation Y2X - loss=8.3225e-01 ppl=2.30 best_loss=7.1840e-01 best_ppl=2.05
Epoch 58 - |param|=9.42e+02 |g_param|=2.34e+04 loss_x2y=4.7833e-01 ppl_x2y=1.61 loss_y2x=5.7404e-01 ppl_y2x=1.78 dual_loss=1.0043e+00
Validation X2Y - loss=7.3830e-01 ppl=2.09 best_loss=7.0281e-01 best_ppl=2.02                                            
Validation Y2X - loss=7.4612e-01 ppl=2.11 best_loss=7.1840e-01 best_ppl=2.05
Epoch 59 - |param|=9.43e+02 |g_param|=2.22e+04 loss_x2y=4.2364e-01 ppl_x2y=1.53 loss_y2x=4.8215e-01 ppl_y2x=1.62 dual_loss=5.2511e-01
Validation X2Y - loss=6.9864e-01 ppl=2.01 best_loss=7.0281e-01 best_ppl=2.02                                            
Validation Y2X - loss=7.0736e-01 ppl=2.03 best_loss=7.1840e-01 best_ppl=2.05
Epoch 60 - |param|=9.43e+02 |g_param|=2.31e+04 loss_x2y=3.9145e-01 ppl_x2y=1.48 loss_y2x=4.4214e-01 ppl_y2x=1.56 dual_loss=5.1158e-01
Validation X2Y - loss=7.0206e-01 ppl=2.02 best_loss=6.9864e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.8454e-01 ppl=1.98 best_loss=7.0736e-01 best_ppl=2.03
Epoch 61 - |param|=9.43e+02 |g_param|=2.06e+04 loss_x2y=3.7123e-01 ppl_x2y=1.45 loss_y2x=4.2443e-01 ppl_y2x=1.53 dual_loss=4.3650e-01
Validation X2Y - loss=6.8971e-01 ppl=1.99 best_loss=6.9864e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.8009e-01 ppl=1.97 best_loss=6.8454e-01 best_ppl=1.98
Epoch 62 - |param|=9.44e+02 |g_param|=2.18e+04 loss_x2y=3.8471e-01 ppl_x2y=1.47 loss_y2x=4.3379e-01 ppl_y2x=1.54 dual_loss=5.1399e-01
Validation X2Y - loss=6.9089e-01 ppl=2.00 best_loss=6.8971e-01 best_ppl=1.99                                            
Validation Y2X - loss=6.7444e-01 ppl=1.96 best_loss=6.8009e-01 best_ppl=1.97
Epoch 63 - |param|=9.44e+02 |g_param|=2.35e+04 loss_x2y=3.5418e-01 ppl_x2y=1.43 loss_y2x=3.8623e-01 ppl_y2x=1.47 dual_loss=4.4728e-01
Validation X2Y - loss=7.0190e-01 ppl=2.02 best_loss=6.8971e-01 best_ppl=1.99                                            
Validation Y2X - loss=6.6950e-01 ppl=1.95 best_loss=6.7444e-01 best_ppl=1.96
Epoch 64 - |param|=9.44e+02 |g_param|=2.02e+04 loss_x2y=3.6620e-01 ppl_x2y=1.44 loss_y2x=4.1449e-01 ppl_y2x=1.51 dual_loss=4.5928e-01
Validation X2Y - loss=6.8912e-01 ppl=1.99 best_loss=6.8971e-01 best_ppl=1.99                                            
Validation Y2X - loss=6.8849e-01 ppl=1.99 best_loss=6.6950e-01 best_ppl=1.95
Epoch 65 - |param|=9.45e+02 |g_param|=2.13e+04 loss_x2y=3.4889e-01 ppl_x2y=1.42 loss_y2x=3.9037e-01 ppl_y2x=1.48 dual_loss=4.9733e-01
Validation X2Y - loss=6.8515e-01 ppl=1.98 best_loss=6.8912e-01 best_ppl=1.99                                            
Validation Y2X - loss=6.9309e-01 ppl=2.00 best_loss=6.6950e-01 best_ppl=1.95
Epoch 66 - |param|=9.45e+02 |g_param|=2.10e+04 loss_x2y=3.5293e-01 ppl_x2y=1.42 loss_y2x=3.9317e-01 ppl_y2x=1.48 dual_loss=4.3281e-01
Validation X2Y - loss=6.9252e-01 ppl=2.00 best_loss=6.8515e-01 best_ppl=1.98                                            
Validation Y2X - loss=6.7026e-01 ppl=1.95 best_loss=6.6950e-01 best_ppl=1.95
Epoch 67 - |param|=9.46e+02 |g_param|=2.23e+04 loss_x2y=3.3198e-01 ppl_x2y=1.39 loss_y2x=3.7797e-01 ppl_y2x=1.46 dual_loss=4.0911e-01
Validation X2Y - loss=6.7551e-01 ppl=1.97 best_loss=6.8515e-01 best_ppl=1.98                                            
Validation Y2X - loss=6.7757e-01 ppl=1.97 best_loss=6.6950e-01 best_ppl=1.95
Epoch 68 - |param|=9.46e+02 |g_param|=2.47e+04 loss_x2y=3.2973e-01 ppl_x2y=1.39 loss_y2x=3.6597e-01 ppl_y2x=1.44 dual_loss=4.6041e-01
Validation X2Y - loss=6.7009e-01 ppl=1.95 best_loss=6.7551e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.8404e-01 ppl=1.98 best_loss=6.6950e-01 best_ppl=1.95
Epoch 69 - |param|=9.46e+02 |g_param|=2.06e+04 loss_x2y=3.4088e-01 ppl_x2y=1.41 loss_y2x=3.7088e-01 ppl_y2x=1.45 dual_loss=4.0155e-01
Validation X2Y - loss=6.9351e-01 ppl=2.00 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7583e-01 ppl=1.97 best_loss=6.6950e-01 best_ppl=1.95
Epoch 70 - |param|=9.47e+02 |g_param|=1.90e+04 loss_x2y=3.2452e-01 ppl_x2y=1.38 loss_y2x=3.6246e-01 ppl_y2x=1.44 dual_loss=3.8845e-01
Validation X2Y - loss=6.8735e-01 ppl=1.99 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.8882e-01 ppl=1.99 best_loss=6.6950e-01 best_ppl=1.95
Epoch 71 - |param|=9.47e+02 |g_param|=2.30e+04 loss_x2y=3.3025e-01 ppl_x2y=1.39 loss_y2x=3.8876e-01 ppl_y2x=1.48 dual_loss=5.2523e-01
Validation X2Y - loss=6.7167e-01 ppl=1.96 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.8169e-01 ppl=1.98 best_loss=6.6950e-01 best_ppl=1.95
Epoch 72 - |param|=9.47e+02 |g_param|=2.39e+04 loss_x2y=3.2043e-01 ppl_x2y=1.38 loss_y2x=3.6611e-01 ppl_y2x=1.44 dual_loss=4.8278e-01
Validation X2Y - loss=6.7582e-01 ppl=1.97 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.8480e-01 ppl=1.98 best_loss=6.6950e-01 best_ppl=1.95
Epoch 73 - |param|=9.48e+02 |g_param|=2.33e+04 loss_x2y=3.2052e-01 ppl_x2y=1.38 loss_y2x=3.5923e-01 ppl_y2x=1.43 dual_loss=4.4615e-01
Validation X2Y - loss=6.8619e-01 ppl=1.99 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7812e-01 ppl=1.97 best_loss=6.6950e-01 best_ppl=1.95
Epoch 74 - |param|=9.48e+02 |g_param|=2.57e+04 loss_x2y=3.2272e-01 ppl_x2y=1.38 loss_y2x=3.5306e-01 ppl_y2x=1.42 dual_loss=4.0281e-01
Validation X2Y - loss=6.9404e-01 ppl=2.00 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7030e-01 ppl=1.95 best_loss=6.6950e-01 best_ppl=1.95
Epoch 75 - |param|=9.49e+02 |g_param|=2.78e+04 loss_x2y=3.1891e-01 ppl_x2y=1.38 loss_y2x=3.3549e-01 ppl_y2x=1.40 dual_loss=3.9628e-01
Validation X2Y - loss=6.9482e-01 ppl=2.00 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7908e-01 ppl=1.97 best_loss=6.6950e-01 best_ppl=1.95
Epoch 76 - |param|=9.49e+02 |g_param|=3.24e+04 loss_x2y=3.2444e-01 ppl_x2y=1.38 loss_y2x=3.2067e-01 ppl_y2x=1.38 dual_loss=3.4375e-01
Validation X2Y - loss=6.9947e-01 ppl=2.01 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7090e-01 ppl=1.96 best_loss=6.6950e-01 best_ppl=1.95
Epoch 77 - |param|=9.50e+02 |g_param|=3.29e+04 loss_x2y=4.6258e-01 ppl_x2y=1.59 loss_y2x=3.4139e-01 ppl_y2x=1.41 dual_loss=7.7636e-01
Validation X2Y - loss=7.3652e-01 ppl=2.09 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7191e-01 ppl=1.96 best_loss=6.6950e-01 best_ppl=1.95
Epoch 78 - |param|=9.50e+02 |g_param|=2.13e+04 loss_x2y=3.8018e-01 ppl_x2y=1.46 loss_y2x=3.2617e-01 ppl_y2x=1.39 dual_loss=3.5152e-01
Validation X2Y - loss=6.8636e-01 ppl=1.99 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.6413e-01 ppl=1.94 best_loss=6.6950e-01 best_ppl=1.95
Epoch 79 - |param|=9.51e+02 |g_param|=2.07e+04 loss_x2y=3.1933e-01 ppl_x2y=1.38 loss_y2x=3.2634e-01 ppl_y2x=1.39 dual_loss=3.7716e-01
Validation X2Y - loss=6.7498e-01 ppl=1.96 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.7184e-01 ppl=1.96 best_loss=6.6413e-01 best_ppl=1.94
Epoch 80 - |param|=9.51e+02 |g_param|=2.54e+04 loss_x2y=3.1385e-01 ppl_x2y=1.37 loss_y2x=3.6800e-01 ppl_y2x=1.44 dual_loss=5.3995e-01
Validation X2Y - loss=6.5603e-01 ppl=1.93 best_loss=6.7009e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.9751e-01 ppl=2.01 best_loss=6.6413e-01 best_ppl=1.94
Epoch 81 - |param|=9.51e+02 |g_param|=3.65e+04 loss_x2y=3.2144e-01 ppl_x2y=1.38 loss_y2x=3.8916e-01 ppl_y2x=1.48 dual_loss=8.0384e-01
Validation X2Y - loss=6.6380e-01 ppl=1.94 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=7.1563e-01 ppl=2.05 best_loss=6.6413e-01 best_ppl=1.94
Epoch 82 - |param|=9.52e+02 |g_param|=5.15e+04 loss_x2y=3.5062e-01 ppl_x2y=1.42 loss_y2x=5.3366e-01 ppl_y2x=1.71 dual_loss=3.7393e+00
Validation X2Y - loss=6.8668e-01 ppl=1.99 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=8.5372e-01 ppl=2.35 best_loss=6.6413e-01 best_ppl=1.94
Epoch 83 - |param|=9.53e+02 |g_param|=2.47e+04 loss_x2y=3.7371e-01 ppl_x2y=1.45 loss_y2x=5.5582e-01 ppl_y2x=1.74 dual_loss=1.9191e+00
Validation X2Y - loss=7.0008e-01 ppl=2.01 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=8.2200e-01 ppl=2.28 best_loss=6.6413e-01 best_ppl=1.94
Epoch 84 - |param|=9.53e+02 |g_param|=1.88e+04 loss_x2y=3.4118e-01 ppl_x2y=1.41 loss_y2x=4.2355e-01 ppl_y2x=1.53 dual_loss=7.1244e-01
Validation X2Y - loss=6.8087e-01 ppl=1.98 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.7458e-01 ppl=1.96 best_loss=6.6413e-01 best_ppl=1.94
Epoch 85 - |param|=9.53e+02 |g_param|=1.12e+04 loss_x2y=2.8996e-01 ppl_x2y=1.34 loss_y2x=3.5304e-01 ppl_y2x=1.42 dual_loss=4.7686e-01
Validation X2Y - loss=6.6112e-01 ppl=1.94 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.4400e-01 ppl=1.90 best_loss=6.6413e-01 best_ppl=1.94
Epoch 86 - |param|=9.54e+02 |g_param|=1.06e+04 loss_x2y=2.8092e-01 ppl_x2y=1.32 loss_y2x=3.3574e-01 ppl_y2x=1.40 dual_loss=4.5490e-01
Validation X2Y - loss=6.7219e-01 ppl=1.96 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.4204e-01 ppl=1.90 best_loss=6.4400e-01 best_ppl=1.90
Epoch 87 - |param|=9.54e+02 |g_param|=1.06e+04 loss_x2y=2.8000e-01 ppl_x2y=1.32 loss_y2x=3.2906e-01 ppl_y2x=1.39 dual_loss=4.5045e-01
Validation X2Y - loss=6.6373e-01 ppl=1.94 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.5001e-01 ppl=1.92 best_loss=6.4204e-01 best_ppl=1.90
Epoch 88 - |param|=9.54e+02 |g_param|=1.24e+04 loss_x2y=2.8186e-01 ppl_x2y=1.33 loss_y2x=3.2840e-01 ppl_y2x=1.39 dual_loss=5.1299e-01
Validation X2Y - loss=6.6468e-01 ppl=1.94 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.6673e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 89 - |param|=9.55e+02 |g_param|=9.60e+03 loss_x2y=2.6778e-01 ppl_x2y=1.31 loss_y2x=3.1355e-01 ppl_y2x=1.37 dual_loss=4.6985e-01
Validation X2Y - loss=6.5415e-01 ppl=1.92 best_loss=6.5603e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.6736e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 90 - |param|=9.55e+02 |g_param|=1.14e+04 loss_x2y=2.6378e-01 ppl_x2y=1.30 loss_y2x=3.1093e-01 ppl_y2x=1.36 dual_loss=5.3548e-01
Validation X2Y - loss=6.6241e-01 ppl=1.94 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5713e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 91 - |param|=9.55e+02 |g_param|=9.81e+03 loss_x2y=2.6622e-01 ppl_x2y=1.31 loss_y2x=3.1219e-01 ppl_y2x=1.37 dual_loss=4.6549e-01
Validation X2Y - loss=6.6027e-01 ppl=1.94 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5473e-01 ppl=1.92 best_loss=6.4204e-01 best_ppl=1.90
Epoch 92 - |param|=9.56e+02 |g_param|=1.04e+04 loss_x2y=2.5933e-01 ppl_x2y=1.30 loss_y2x=2.9340e-01 ppl_y2x=1.34 dual_loss=3.3901e-01
Validation X2Y - loss=6.8758e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5947e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 93 - |param|=9.56e+02 |g_param|=1.18e+04 loss_x2y=2.5987e-01 ppl_x2y=1.30 loss_y2x=2.9416e-01 ppl_y2x=1.34 dual_loss=3.7838e-01
Validation X2Y - loss=6.8138e-01 ppl=1.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5926e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 94 - |param|=9.56e+02 |g_param|=1.01e+04 loss_x2y=2.4931e-01 ppl_x2y=1.28 loss_y2x=2.7997e-01 ppl_y2x=1.32 dual_loss=3.5720e-01
Validation X2Y - loss=6.8981e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5805e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 95 - |param|=9.57e+02 |g_param|=1.12e+04 loss_x2y=2.5807e-01 ppl_x2y=1.29 loss_y2x=2.9407e-01 ppl_y2x=1.34 dual_loss=3.7593e-01
Validation X2Y - loss=6.8838e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.4624e-01 ppl=1.91 best_loss=6.4204e-01 best_ppl=1.90
Epoch 96 - |param|=9.57e+02 |g_param|=1.09e+04 loss_x2y=2.5269e-01 ppl_x2y=1.29 loss_y2x=2.8150e-01 ppl_y2x=1.33 dual_loss=3.4293e-01
Validation X2Y - loss=6.9797e-01 ppl=2.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.4915e-01 ppl=1.91 best_loss=6.4204e-01 best_ppl=1.90
Epoch 97 - |param|=9.57e+02 |g_param|=1.38e+04 loss_x2y=2.4831e-01 ppl_x2y=1.28 loss_y2x=2.7580e-01 ppl_y2x=1.32 dual_loss=3.3850e-01
Validation X2Y - loss=6.8534e-01 ppl=1.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7389e-01 ppl=1.96 best_loss=6.4204e-01 best_ppl=1.90
Epoch 98 - |param|=9.58e+02 |g_param|=2.34e+04 loss_x2y=2.5838e-01 ppl_x2y=1.29 loss_y2x=2.8862e-01 ppl_y2x=1.33 dual_loss=4.8148e-01
Validation X2Y - loss=6.9459e-01 ppl=2.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6770e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 99 - |param|=9.58e+02 |g_param|=2.11e+04 loss_x2y=2.5526e-01 ppl_x2y=1.29 loss_y2x=2.8353e-01 ppl_y2x=1.33 dual_loss=3.8372e-01
Validation X2Y - loss=6.8138e-01 ppl=1.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6055e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 100 - |param|=9.59e+02 |g_param|=1.79e+04 loss_x2y=2.3855e-01 ppl_x2y=1.27 loss_y2x=2.7493e-01 ppl_y2x=1.32 dual_loss=4.4078e-01
Validation X2Y - loss=6.9354e-01 ppl=2.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6014e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 101 - |param|=9.59e+02 |g_param|=1.69e+04 loss_x2y=2.2784e-01 ppl_x2y=1.26 loss_y2x=2.8176e-01 ppl_y2x=1.33 dual_loss=4.2054e-01
Validation X2Y - loss=6.8663e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8625e-01 ppl=1.99 best_loss=6.4204e-01 best_ppl=1.90
Epoch 102 - |param|=9.59e+02 |g_param|=1.80e+04 loss_x2y=2.2499e-01 ppl_x2y=1.25 loss_y2x=2.6688e-01 ppl_y2x=1.31 dual_loss=3.8395e-01
Validation X2Y - loss=6.8857e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7334e-01 ppl=1.96 best_loss=6.4204e-01 best_ppl=1.90
Epoch 103 - |param|=9.60e+02 |g_param|=2.00e+04 loss_x2y=2.2928e-01 ppl_x2y=1.26 loss_y2x=2.6041e-01 ppl_y2x=1.30 dual_loss=3.5860e-01
Validation X2Y - loss=6.8963e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6969e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 104 - |param|=9.60e+02 |g_param|=2.03e+04 loss_x2y=2.2233e-01 ppl_x2y=1.25 loss_y2x=2.6061e-01 ppl_y2x=1.30 dual_loss=3.8913e-01
Validation X2Y - loss=6.8978e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8042e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 105 - |param|=9.60e+02 |g_param|=1.97e+04 loss_x2y=2.2853e-01 ppl_x2y=1.26 loss_y2x=2.6163e-01 ppl_y2x=1.30 dual_loss=3.6675e-01
Validation X2Y - loss=6.8496e-01 ppl=1.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8079e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 106 - |param|=9.61e+02 |g_param|=1.99e+04 loss_x2y=2.2433e-01 ppl_x2y=1.25 loss_y2x=2.5605e-01 ppl_y2x=1.29 dual_loss=3.7171e-01
Validation X2Y - loss=7.0805e-01 ppl=2.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7610e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 107 - |param|=9.61e+02 |g_param|=2.03e+04 loss_x2y=2.1731e-01 ppl_x2y=1.24 loss_y2x=2.4692e-01 ppl_y2x=1.28 dual_loss=3.9804e-01
Validation X2Y - loss=6.8983e-01 ppl=1.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7732e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 108 - |param|=9.62e+02 |g_param|=2.15e+04 loss_x2y=2.1701e-01 ppl_x2y=1.24 loss_y2x=2.5512e-01 ppl_y2x=1.29 dual_loss=3.7353e-01
Validation X2Y - loss=6.9996e-01 ppl=2.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6027e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 109 - |param|=9.62e+02 |g_param|=2.88e+04 loss_x2y=2.2480e-01 ppl_x2y=1.25 loss_y2x=2.9047e-01 ppl_y2x=1.34 dual_loss=5.7500e-01
Validation X2Y - loss=7.0535e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9837e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 110 - |param|=9.63e+02 |g_param|=2.14e+04 loss_x2y=2.1447e-01 ppl_x2y=1.24 loss_y2x=2.6887e-01 ppl_y2x=1.31 dual_loss=4.4961e-01
Validation X2Y - loss=7.0573e-01 ppl=2.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6144e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 111 - |param|=9.63e+02 |g_param|=2.05e+04 loss_x2y=2.1315e-01 ppl_x2y=1.24 loss_y2x=2.6654e-01 ppl_y2x=1.31 dual_loss=4.1126e-01
Validation X2Y - loss=7.0697e-01 ppl=2.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6552e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 112 - |param|=9.63e+02 |g_param|=2.26e+04 loss_x2y=2.1067e-01 ppl_x2y=1.23 loss_y2x=2.6120e-01 ppl_y2x=1.30 dual_loss=4.5681e-01
Validation X2Y - loss=6.9452e-01 ppl=2.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5019e-01 ppl=1.92 best_loss=6.4204e-01 best_ppl=1.90
Epoch 113 - |param|=9.64e+02 |g_param|=2.10e+04 loss_x2y=2.1199e-01 ppl_x2y=1.24 loss_y2x=2.4712e-01 ppl_y2x=1.28 dual_loss=4.3990e-01
Validation X2Y - loss=7.0369e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6062e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 114 - |param|=9.64e+02 |g_param|=3.22e+04 loss_x2y=2.3836e-01 ppl_x2y=1.27 loss_y2x=2.5324e-01 ppl_y2x=1.29 dual_loss=3.9552e-01
Validation X2Y - loss=7.0411e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6939e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 115 - |param|=9.65e+02 |g_param|=3.03e+04 loss_x2y=2.4368e-01 ppl_x2y=1.28 loss_y2x=2.4468e-01 ppl_y2x=1.28 dual_loss=3.4365e-01
Validation X2Y - loss=7.2007e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6590e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 116 - |param|=9.65e+02 |g_param|=1.87e+04 loss_x2y=2.3495e-01 ppl_x2y=1.26 loss_y2x=2.3589e-01 ppl_y2x=1.27 dual_loss=5.0180e-01
Validation X2Y - loss=7.1082e-01 ppl=2.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5374e-01 ppl=1.92 best_loss=6.4204e-01 best_ppl=1.90
Epoch 117 - |param|=9.66e+02 |g_param|=1.66e+04 loss_x2y=2.2168e-01 ppl_x2y=1.25 loss_y2x=2.2775e-01 ppl_y2x=1.26 dual_loss=3.3300e-01
Validation X2Y - loss=7.3050e-01 ppl=2.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5812e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 118 - |param|=9.66e+02 |g_param|=1.48e+04 loss_x2y=2.2010e-01 ppl_x2y=1.25 loss_y2x=2.3672e-01 ppl_y2x=1.27 dual_loss=3.7241e-01
Validation X2Y - loss=7.0248e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6276e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 119 - |param|=9.66e+02 |g_param|=1.66e+04 loss_x2y=2.0351e-01 ppl_x2y=1.23 loss_y2x=2.4289e-01 ppl_y2x=1.27 dual_loss=4.0178e-01
Validation X2Y - loss=7.0217e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7274e-01 ppl=1.96 best_loss=6.4204e-01 best_ppl=1.90
Epoch 120 - |param|=9.67e+02 |g_param|=1.24e+04 loss_x2y=1.9172e-01 ppl_x2y=1.21 loss_y2x=2.2579e-01 ppl_y2x=1.25 dual_loss=3.8815e-01
Validation X2Y - loss=7.0823e-01 ppl=2.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7614e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 121 - |param|=9.67e+02 |g_param|=1.36e+04 loss_x2y=1.9047e-01 ppl_x2y=1.21 loss_y2x=2.2726e-01 ppl_y2x=1.26 dual_loss=3.7430e-01
Validation X2Y - loss=7.1598e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6830e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 122 - |param|=9.68e+02 |g_param|=3.48e+04 loss_x2y=1.9572e-01 ppl_x2y=1.22 loss_y2x=3.0210e-01 ppl_y2x=1.35 dual_loss=7.4069e-01
Validation X2Y - loss=7.1223e-01 ppl=2.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2043e-01 ppl=2.06 best_loss=6.4204e-01 best_ppl=1.90
Epoch 123 - |param|=9.68e+02 |g_param|=2.52e+04 loss_x2y=2.0129e-01 ppl_x2y=1.22 loss_y2x=2.8371e-01 ppl_y2x=1.33 dual_loss=1.2817e+00
Validation X2Y - loss=7.2989e-01 ppl=2.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1618e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 124 - |param|=9.68e+02 |g_param|=3.97e+04 loss_x2y=3.9322e-01 ppl_x2y=1.48 loss_y2x=2.7041e-01 ppl_y2x=1.31 dual_loss=1.2205e+00
Validation X2Y - loss=9.1384e-01 ppl=2.49 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8041e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 125 - |param|=9.69e+02 |g_param|=2.90e+04 loss_x2y=3.3242e-01 ppl_x2y=1.39 loss_y2x=2.3743e-01 ppl_y2x=1.27 dual_loss=4.5805e-01
Validation X2Y - loss=7.6233e-01 ppl=2.14 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7699e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 126 - |param|=9.70e+02 |g_param|=1.71e+04 loss_x2y=3.0037e-01 ppl_x2y=1.35 loss_y2x=2.4743e-01 ppl_y2x=1.28 dual_loss=8.7196e-01
Validation X2Y - loss=7.0450e-01 ppl=2.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6478e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 127 - |param|=9.70e+02 |g_param|=1.25e+04 loss_x2y=2.4408e-01 ppl_x2y=1.28 loss_y2x=2.7250e-01 ppl_y2x=1.31 dual_loss=5.9488e-01
Validation X2Y - loss=7.0970e-01 ppl=2.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6795e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 128 - |param|=9.71e+02 |g_param|=1.10e+04 loss_x2y=2.4183e-01 ppl_x2y=1.27 loss_y2x=2.8321e-01 ppl_y2x=1.33 dual_loss=5.1895e-01
Validation X2Y - loss=7.1706e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6780e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 129 - |param|=9.71e+02 |g_param|=5.11e+03 loss_x2y=2.0472e-01 ppl_x2y=1.23 loss_y2x=2.3380e-01 ppl_y2x=1.26 dual_loss=3.8756e-01
Validation X2Y - loss=7.1618e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6239e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 130 - |param|=9.71e+02 |g_param|=5.47e+03 loss_x2y=1.9671e-01 ppl_x2y=1.22 loss_y2x=2.1842e-01 ppl_y2x=1.24 dual_loss=3.9497e-01
Validation X2Y - loss=7.1850e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5839e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 131 - |param|=9.72e+02 |g_param|=4.85e+03 loss_x2y=1.9187e-01 ppl_x2y=1.21 loss_y2x=2.3037e-01 ppl_y2x=1.26 dual_loss=4.1197e-01
Validation X2Y - loss=7.1738e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6725e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 132 - |param|=9.72e+02 |g_param|=4.68e+03 loss_x2y=1.8790e-01 ppl_x2y=1.21 loss_y2x=2.2357e-01 ppl_y2x=1.25 dual_loss=3.7932e-01
Validation X2Y - loss=7.2020e-01 ppl=2.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7676e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 133 - |param|=9.72e+02 |g_param|=1.13e+04 loss_x2y=2.3009e-01 ppl_x2y=1.26 loss_y2x=4.3016e-01 ppl_y2x=1.54 dual_loss=1.4315e+00
Validation X2Y - loss=7.2715e-01 ppl=2.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8331e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 134 - |param|=9.73e+02 |g_param|=4.69e+03 loss_x2y=1.7170e-01 ppl_x2y=1.19 loss_y2x=2.3116e-01 ppl_y2x=1.26 dual_loss=4.4362e-01
Validation X2Y - loss=7.3409e-01 ppl=2.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6261e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 135 - |param|=9.73e+02 |g_param|=4.12e+03 loss_x2y=1.7419e-01 ppl_x2y=1.19 loss_y2x=2.2371e-01 ppl_y2x=1.25 dual_loss=4.2492e-01
Validation X2Y - loss=7.3532e-01 ppl=2.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6340e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 136 - |param|=9.73e+02 |g_param|=3.80e+03 loss_x2y=1.6956e-01 ppl_x2y=1.18 loss_y2x=2.0777e-01 ppl_y2x=1.23 dual_loss=3.6875e-01
Validation X2Y - loss=7.2605e-01 ppl=2.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.4668e-01 ppl=1.91 best_loss=6.4204e-01 best_ppl=1.90
Epoch 137 - |param|=9.74e+02 |g_param|=4.51e+03 loss_x2y=1.6792e-01 ppl_x2y=1.18 loss_y2x=2.0571e-01 ppl_y2x=1.23 dual_loss=3.5640e-01
Validation X2Y - loss=7.3017e-01 ppl=2.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5564e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 138 - |param|=9.74e+02 |g_param|=4.14e+03 loss_x2y=1.6538e-01 ppl_x2y=1.18 loss_y2x=1.9224e-01 ppl_y2x=1.21 dual_loss=3.4265e-01
Validation X2Y - loss=7.2560e-01 ppl=2.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5055e-01 ppl=1.92 best_loss=6.4204e-01 best_ppl=1.90
Epoch 139 - |param|=9.74e+02 |g_param|=3.91e+03 loss_x2y=1.6546e-01 ppl_x2y=1.18 loss_y2x=1.9231e-01 ppl_y2x=1.21 dual_loss=3.1341e-01
Validation X2Y - loss=7.3911e-01 ppl=2.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6769e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 140 - |param|=9.74e+02 |g_param|=3.69e+03 loss_x2y=1.6272e-01 ppl_x2y=1.18 loss_y2x=1.8607e-01 ppl_y2x=1.20 dual_loss=3.2218e-01
Validation X2Y - loss=7.4142e-01 ppl=2.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.5750e-01 ppl=1.93 best_loss=6.4204e-01 best_ppl=1.90
Epoch 141 - |param|=9.75e+02 |g_param|=4.79e+03 loss_x2y=1.6445e-01 ppl_x2y=1.18 loss_y2x=1.9079e-01 ppl_y2x=1.21 dual_loss=3.6544e-01
Validation X2Y - loss=7.4151e-01 ppl=2.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6878e-01 ppl=1.95 best_loss=6.4204e-01 best_ppl=1.90
Epoch 142 - |param|=9.75e+02 |g_param|=4.14e+03 loss_x2y=1.5476e-01 ppl_x2y=1.17 loss_y2x=1.8317e-01 ppl_y2x=1.20 dual_loss=3.4716e-01
Validation X2Y - loss=7.4455e-01 ppl=2.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.6324e-01 ppl=1.94 best_loss=6.4204e-01 best_ppl=1.90
Epoch 143 - |param|=9.75e+02 |g_param|=4.69e+03 loss_x2y=1.5995e-01 ppl_x2y=1.17 loss_y2x=1.8114e-01 ppl_y2x=1.20 dual_loss=3.5316e-01
Validation X2Y - loss=7.5152e-01 ppl=2.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8070e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 144 - |param|=9.76e+02 |g_param|=5.02e+03 loss_x2y=1.6855e-01 ppl_x2y=1.18 loss_y2x=1.9081e-01 ppl_y2x=1.21 dual_loss=3.3341e-01
Validation X2Y - loss=7.6019e-01 ppl=2.14 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7101e-01 ppl=1.96 best_loss=6.4204e-01 best_ppl=1.90
Epoch 145 - |param|=9.76e+02 |g_param|=4.38e+03 loss_x2y=1.5639e-01 ppl_x2y=1.17 loss_y2x=1.7806e-01 ppl_y2x=1.19 dual_loss=3.5346e-01
Validation X2Y - loss=7.5385e-01 ppl=2.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8308e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 146 - |param|=9.76e+02 |g_param|=4.44e+03 loss_x2y=1.5762e-01 ppl_x2y=1.17 loss_y2x=1.8241e-01 ppl_y2x=1.20 dual_loss=3.4592e-01
Validation X2Y - loss=7.5829e-01 ppl=2.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7952e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 147 - |param|=9.77e+02 |g_param|=7.83e+03 loss_x2y=1.5990e-01 ppl_x2y=1.17 loss_y2x=1.8101e-01 ppl_y2x=1.20 dual_loss=4.3644e-01
Validation X2Y - loss=7.5564e-01 ppl=2.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9761e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 148 - |param|=9.77e+02 |g_param|=6.92e+03 loss_x2y=1.5354e-01 ppl_x2y=1.17 loss_y2x=1.7685e-01 ppl_y2x=1.19 dual_loss=4.3178e-01
Validation X2Y - loss=7.6713e-01 ppl=2.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0698e-01 ppl=2.03 best_loss=6.4204e-01 best_ppl=1.90
Epoch 149 - |param|=9.77e+02 |g_param|=7.36e+03 loss_x2y=1.4915e-01 ppl_x2y=1.16 loss_y2x=1.8670e-01 ppl_y2x=1.21 dual_loss=3.8648e-01
Validation X2Y - loss=7.5614e-01 ppl=2.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8945e-01 ppl=1.99 best_loss=6.4204e-01 best_ppl=1.90
Epoch 150 - |param|=9.78e+02 |g_param|=1.06e+04 loss_x2y=1.6290e-01 ppl_x2y=1.18 loss_y2x=1.7782e-01 ppl_y2x=1.19 dual_loss=4.1337e-01
Validation X2Y - loss=7.4355e-01 ppl=2.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9870e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 151 - |param|=9.78e+02 |g_param|=9.45e+03 loss_x2y=1.6182e-01 ppl_x2y=1.18 loss_y2x=1.8309e-01 ppl_y2x=1.20 dual_loss=3.3072e-01
Validation X2Y - loss=7.5435e-01 ppl=2.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9154e-01 ppl=2.00 best_loss=6.4204e-01 best_ppl=1.90
Epoch 152 - |param|=9.79e+02 |g_param|=9.84e+03 loss_x2y=1.5323e-01 ppl_x2y=1.17 loss_y2x=1.7164e-01 ppl_y2x=1.19 dual_loss=3.9258e-01
Validation X2Y - loss=7.7340e-01 ppl=2.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0207e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 153 - |param|=9.79e+02 |g_param|=9.78e+03 loss_x2y=1.6107e-01 ppl_x2y=1.17 loss_y2x=1.9071e-01 ppl_y2x=1.21 dual_loss=5.0412e-01
Validation X2Y - loss=7.6620e-01 ppl=2.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9319e-01 ppl=2.00 best_loss=6.4204e-01 best_ppl=1.90
Epoch 154 - |param|=9.79e+02 |g_param|=1.01e+04 loss_x2y=1.5786e-01 ppl_x2y=1.17 loss_y2x=1.9005e-01 ppl_y2x=1.21 dual_loss=4.6242e-01
Validation X2Y - loss=7.6615e-01 ppl=2.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9250e-01 ppl=2.00 best_loss=6.4204e-01 best_ppl=1.90
Epoch 155 - |param|=9.80e+02 |g_param|=1.01e+04 loss_x2y=1.4751e-01 ppl_x2y=1.16 loss_y2x=1.7700e-01 ppl_y2x=1.19 dual_loss=5.0715e-01
Validation X2Y - loss=7.7217e-01 ppl=2.16 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8372e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 156 - |param|=9.80e+02 |g_param|=1.38e+04 loss_x2y=1.6965e-01 ppl_x2y=1.18 loss_y2x=1.8246e-01 ppl_y2x=1.20 dual_loss=3.6141e-01
Validation X2Y - loss=7.7701e-01 ppl=2.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.7619e-01 ppl=1.97 best_loss=6.4204e-01 best_ppl=1.90
Epoch 157 - |param|=9.81e+02 |g_param|=1.18e+04 loss_x2y=1.6302e-01 ppl_x2y=1.18 loss_y2x=1.7706e-01 ppl_y2x=1.19 dual_loss=3.6158e-01
Validation X2Y - loss=7.8484e-01 ppl=2.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.8546e-01 ppl=1.98 best_loss=6.4204e-01 best_ppl=1.90
Epoch 158 - |param|=9.81e+02 |g_param|=1.10e+04 loss_x2y=1.6153e-01 ppl_x2y=1.18 loss_y2x=1.7595e-01 ppl_y2x=1.19 dual_loss=3.8643e-01
Validation X2Y - loss=7.6890e-01 ppl=2.16 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0356e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 159 - |param|=9.81e+02 |g_param|=1.15e+04 loss_x2y=1.6068e-01 ppl_x2y=1.17 loss_y2x=1.6711e-01 ppl_y2x=1.18 dual_loss=3.4779e-01
Validation X2Y - loss=7.7771e-01 ppl=2.18 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0981e-01 ppl=2.03 best_loss=6.4204e-01 best_ppl=1.90
Epoch 160 - |param|=9.82e+02 |g_param|=1.06e+04 loss_x2y=1.6308e-01 ppl_x2y=1.18 loss_y2x=1.6520e-01 ppl_y2x=1.18 dual_loss=3.1348e-01
Validation X2Y - loss=7.8470e-01 ppl=2.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9567e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 161 - |param|=9.82e+02 |g_param|=1.18e+04 loss_x2y=1.6101e-01 ppl_x2y=1.17 loss_y2x=1.8344e-01 ppl_y2x=1.20 dual_loss=3.6997e-01
Validation X2Y - loss=7.7596e-01 ppl=2.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0342e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 162 - |param|=9.83e+02 |g_param|=9.49e+03 loss_x2y=1.4331e-01 ppl_x2y=1.15 loss_y2x=1.6655e-01 ppl_y2x=1.18 dual_loss=3.5761e-01
Validation X2Y - loss=7.6495e-01 ppl=2.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1780e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 163 - |param|=9.83e+02 |g_param|=1.00e+04 loss_x2y=1.3830e-01 ppl_x2y=1.15 loss_y2x=1.6264e-01 ppl_y2x=1.18 dual_loss=3.7293e-01
Validation X2Y - loss=7.6764e-01 ppl=2.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0371e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 164 - |param|=9.83e+02 |g_param|=1.07e+04 loss_x2y=1.3741e-01 ppl_x2y=1.15 loss_y2x=1.7152e-01 ppl_y2x=1.19 dual_loss=4.3329e-01
Validation X2Y - loss=7.7323e-01 ppl=2.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2544e-01 ppl=2.07 best_loss=6.4204e-01 best_ppl=1.90
Epoch 165 - |param|=9.84e+02 |g_param|=9.74e+03 loss_x2y=1.4477e-01 ppl_x2y=1.16 loss_y2x=1.7349e-01 ppl_y2x=1.19 dual_loss=5.1493e-01
Validation X2Y - loss=8.0773e-01 ppl=2.24 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1923e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 166 - |param|=9.84e+02 |g_param|=1.13e+04 loss_x2y=1.4187e-01 ppl_x2y=1.15 loss_y2x=1.9312e-01 ppl_y2x=1.21 dual_loss=4.8571e-01
Validation X2Y - loss=7.7231e-01 ppl=2.16 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0338e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 167 - |param|=9.85e+02 |g_param|=1.52e+04 loss_x2y=1.3321e-01 ppl_x2y=1.14 loss_y2x=1.7034e-01 ppl_y2x=1.19 dual_loss=5.1628e-01
Validation X2Y - loss=7.8556e-01 ppl=2.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9693e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 168 - |param|=9.85e+02 |g_param|=1.47e+04 loss_x2y=1.2858e-01 ppl_x2y=1.14 loss_y2x=1.7593e-01 ppl_y2x=1.19 dual_loss=3.9287e-01
Validation X2Y - loss=7.8976e-01 ppl=2.20 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.9832e-01 ppl=2.01 best_loss=6.4204e-01 best_ppl=1.90
Epoch 169 - |param|=9.85e+02 |g_param|=1.58e+04 loss_x2y=1.3439e-01 ppl_x2y=1.14 loss_y2x=1.7462e-01 ppl_y2x=1.19 dual_loss=4.0377e-01
Validation X2Y - loss=7.9014e-01 ppl=2.20 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2907e-01 ppl=2.07 best_loss=6.4204e-01 best_ppl=1.90
Epoch 170 - |param|=9.86e+02 |g_param|=1.98e+04 loss_x2y=1.3643e-01 ppl_x2y=1.15 loss_y2x=1.5501e-01 ppl_y2x=1.17 dual_loss=3.2550e-01
Validation X2Y - loss=7.9838e-01 ppl=2.22 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1070e-01 ppl=2.04 best_loss=6.4204e-01 best_ppl=1.90
Epoch 171 - |param|=9.86e+02 |g_param|=2.51e+04 loss_x2y=1.4937e-01 ppl_x2y=1.16 loss_y2x=1.5975e-01 ppl_y2x=1.17 dual_loss=4.0384e-01
Validation X2Y - loss=8.0399e-01 ppl=2.23 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0444e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 172 - |param|=9.87e+02 |g_param|=2.14e+04 loss_x2y=1.5006e-01 ppl_x2y=1.16 loss_y2x=1.5883e-01 ppl_y2x=1.17 dual_loss=3.7441e-01
Validation X2Y - loss=7.9804e-01 ppl=2.22 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1457e-01 ppl=2.04 best_loss=6.4204e-01 best_ppl=1.90
Epoch 173 - |param|=9.87e+02 |g_param|=1.93e+04 loss_x2y=1.3704e-01 ppl_x2y=1.15 loss_y2x=1.4869e-01 ppl_y2x=1.16 dual_loss=3.7747e-01
Validation X2Y - loss=8.2147e-01 ppl=2.27 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1355e-01 ppl=2.04 best_loss=6.4204e-01 best_ppl=1.90
Epoch 174 - |param|=9.87e+02 |g_param|=1.66e+04 loss_x2y=1.3058e-01 ppl_x2y=1.14 loss_y2x=1.4166e-01 ppl_y2x=1.15 dual_loss=3.1473e-01
Validation X2Y - loss=8.0362e-01 ppl=2.23 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0156e-01 ppl=2.02 best_loss=6.4204e-01 best_ppl=1.90
Epoch 175 - |param|=9.88e+02 |g_param|=1.79e+04 loss_x2y=1.3255e-01 ppl_x2y=1.14 loss_y2x=1.4600e-01 ppl_y2x=1.16 dual_loss=3.5385e-01
Validation X2Y - loss=8.1207e-01 ppl=2.25 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1821e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 176 - |param|=9.88e+02 |g_param|=1.78e+04 loss_x2y=1.2734e-01 ppl_x2y=1.14 loss_y2x=1.4964e-01 ppl_y2x=1.16 dual_loss=3.5650e-01
Validation X2Y - loss=8.3291e-01 ppl=2.30 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1602e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 177 - |param|=9.88e+02 |g_param|=1.66e+04 loss_x2y=1.2481e-01 ppl_x2y=1.13 loss_y2x=1.3964e-01 ppl_y2x=1.15 dual_loss=3.2202e-01
Validation X2Y - loss=8.3261e-01 ppl=2.30 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2283e-01 ppl=2.06 best_loss=6.4204e-01 best_ppl=1.90
Epoch 178 - |param|=9.89e+02 |g_param|=1.68e+04 loss_x2y=1.2487e-01 ppl_x2y=1.13 loss_y2x=1.4440e-01 ppl_y2x=1.16 dual_loss=3.8345e-01
Validation X2Y - loss=8.2521e-01 ppl=2.28 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2002e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 179 - |param|=9.89e+02 |g_param|=1.53e+04 loss_x2y=1.1519e-01 ppl_x2y=1.12 loss_y2x=1.3602e-01 ppl_y2x=1.15 dual_loss=3.3032e-01
Validation X2Y - loss=8.2192e-01 ppl=2.27 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.3648e-01 ppl=2.09 best_loss=6.4204e-01 best_ppl=1.90
Epoch 180 - |param|=9.89e+02 |g_param|=1.92e+04 loss_x2y=1.2523e-01 ppl_x2y=1.13 loss_y2x=1.4626e-01 ppl_y2x=1.16 dual_loss=4.0618e-01
Validation X2Y - loss=8.1926e-01 ppl=2.27 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2483e-01 ppl=2.06 best_loss=6.4204e-01 best_ppl=1.90
Epoch 181 - |param|=9.90e+02 |g_param|=1.82e+04 loss_x2y=1.1929e-01 ppl_x2y=1.13 loss_y2x=1.3779e-01 ppl_y2x=1.15 dual_loss=3.2470e-01
Validation X2Y - loss=8.1897e-01 ppl=2.27 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1878e-01 ppl=2.05 best_loss=6.4204e-01 best_ppl=1.90
Epoch 182 - |param|=9.90e+02 |g_param|=3.81e+04 loss_x2y=1.5249e-01 ppl_x2y=1.16 loss_y2x=3.0314e-01 ppl_y2x=1.35 dual_loss=1.1499e+00
Validation X2Y - loss=8.1997e-01 ppl=2.27 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8864e-01 ppl=2.20 best_loss=6.4204e-01 best_ppl=1.90
Epoch 183 - |param|=9.91e+02 |g_param|=2.18e+04 loss_x2y=1.2090e-01 ppl_x2y=1.13 loss_y2x=1.8210e-01 ppl_y2x=1.20 dual_loss=4.8323e-01
Validation X2Y - loss=8.4113e-01 ppl=2.32 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2193e-01 ppl=2.06 best_loss=6.4204e-01 best_ppl=1.90
Epoch 184 - |param|=9.91e+02 |g_param|=1.88e+04 loss_x2y=1.2187e-01 ppl_x2y=1.13 loss_y2x=1.5888e-01 ppl_y2x=1.17 dual_loss=5.3179e-01
Validation X2Y - loss=8.4085e-01 ppl=2.32 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.0575e-01 ppl=2.03 best_loss=6.4204e-01 best_ppl=1.90
Epoch 185 - |param|=9.91e+02 |g_param|=1.58e+04 loss_x2y=1.1465e-01 ppl_x2y=1.12 loss_y2x=1.4475e-01 ppl_y2x=1.16 dual_loss=3.5146e-01
Validation X2Y - loss=8.3498e-01 ppl=2.30 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1235e-01 ppl=2.04 best_loss=6.4204e-01 best_ppl=1.90
Epoch 186 - |param|=9.92e+02 |g_param|=1.73e+04 loss_x2y=1.2280e-01 ppl_x2y=1.13 loss_y2x=1.4506e-01 ppl_y2x=1.16 dual_loss=3.4131e-01
Validation X2Y - loss=8.4356e-01 ppl=2.32 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.1357e-01 ppl=2.04 best_loss=6.4204e-01 best_ppl=1.90
Epoch 187 - |param|=9.92e+02 |g_param|=3.45e+04 loss_x2y=1.1716e-01 ppl_x2y=1.12 loss_y2x=1.3104e-01 ppl_y2x=1.14 dual_loss=3.9127e-01
Validation X2Y - loss=8.4914e-01 ppl=2.34 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2926e-01 ppl=2.07 best_loss=6.4204e-01 best_ppl=1.90
Epoch 188 - |param|=9.92e+02 |g_param|=4.08e+04 loss_x2y=1.2466e-01 ppl_x2y=1.13 loss_y2x=1.3821e-01 ppl_y2x=1.15 dual_loss=3.5365e-01
Validation X2Y - loss=8.5534e-01 ppl=2.35 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.5164e-01 ppl=2.12 best_loss=6.4204e-01 best_ppl=1.90
Epoch 189 - |param|=9.93e+02 |g_param|=3.68e+04 loss_x2y=1.1974e-01 ppl_x2y=1.13 loss_y2x=1.2834e-01 ppl_y2x=1.14 dual_loss=3.9120e-01
Validation X2Y - loss=8.5849e-01 ppl=2.36 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.3911e-01 ppl=2.09 best_loss=6.4204e-01 best_ppl=1.90
Epoch 190 - |param|=9.93e+02 |g_param|=3.79e+04 loss_x2y=1.2340e-01 ppl_x2y=1.13 loss_y2x=1.4002e-01 ppl_y2x=1.15 dual_loss=3.6791e-01
Validation X2Y - loss=8.4698e-01 ppl=2.33 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.2273e-01 ppl=2.06 best_loss=6.4204e-01 best_ppl=1.90
Epoch 191 - |param|=9.94e+02 |g_param|=3.38e+04 loss_x2y=1.1360e-01 ppl_x2y=1.12 loss_y2x=1.3834e-01 ppl_y2x=1.15 dual_loss=3.3252e-01
Validation X2Y - loss=8.3259e-01 ppl=2.30 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.4841e-01 ppl=2.11 best_loss=6.4204e-01 best_ppl=1.90
Epoch 192 - |param|=9.94e+02 |g_param|=3.96e+04 loss_x2y=1.1430e-01 ppl_x2y=1.12 loss_y2x=1.5246e-01 ppl_y2x=1.16 dual_loss=3.6806e-01
Validation X2Y - loss=8.5332e-01 ppl=2.35 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.3700e-01 ppl=2.09 best_loss=6.4204e-01 best_ppl=1.90
Epoch 193 - |param|=9.94e+02 |g_param|=3.17e+04 loss_x2y=1.0325e-01 ppl_x2y=1.11 loss_y2x=1.2820e-01 ppl_y2x=1.14 dual_loss=3.5096e-01
Validation X2Y - loss=8.4774e-01 ppl=2.33 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.3622e-01 ppl=2.09 best_loss=6.4204e-01 best_ppl=1.90
Epoch 194 - |param|=9.95e+02 |g_param|=3.41e+04 loss_x2y=1.0368e-01 ppl_x2y=1.11 loss_y2x=1.2210e-01 ppl_y2x=1.13 dual_loss=4.1633e-01
Validation X2Y - loss=8.7135e-01 ppl=2.39 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.5385e-01 ppl=2.13 best_loss=6.4204e-01 best_ppl=1.90
Epoch 195 - |param|=9.95e+02 |g_param|=3.87e+04 loss_x2y=1.1568e-01 ppl_x2y=1.12 loss_y2x=1.2779e-01 ppl_y2x=1.14 dual_loss=3.5400e-01
Validation X2Y - loss=8.6569e-01 ppl=2.38 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.5515e-01 ppl=2.13 best_loss=6.4204e-01 best_ppl=1.90
Epoch 196 - |param|=9.95e+02 |g_param|=4.30e+04 loss_x2y=1.2195e-01 ppl_x2y=1.13 loss_y2x=1.2890e-01 ppl_y2x=1.14 dual_loss=3.3201e-01
Validation X2Y - loss=8.4863e-01 ppl=2.34 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.3582e-01 ppl=2.09 best_loss=6.4204e-01 best_ppl=1.90
Epoch 197 - |param|=9.96e+02 |g_param|=3.56e+04 loss_x2y=1.1467e-01 ppl_x2y=1.12 loss_y2x=1.2258e-01 ppl_y2x=1.13 dual_loss=3.5825e-01
Validation X2Y - loss=8.7617e-01 ppl=2.40 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6370e-01 ppl=2.15 best_loss=6.4204e-01 best_ppl=1.90
Epoch 198 - |param|=9.96e+02 |g_param|=3.37e+04 loss_x2y=1.0836e-01 ppl_x2y=1.11 loss_y2x=1.2206e-01 ppl_y2x=1.13 dual_loss=3.2534e-01
Validation X2Y - loss=8.8407e-01 ppl=2.42 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.5376e-01 ppl=2.12 best_loss=6.4204e-01 best_ppl=1.90
Epoch 199 - |param|=9.96e+02 |g_param|=3.82e+04 loss_x2y=1.0992e-01 ppl_x2y=1.12 loss_y2x=1.2090e-01 ppl_y2x=1.13 dual_loss=3.3166e-01
Validation X2Y - loss=8.6678e-01 ppl=2.38 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.4349e-01 ppl=2.10 best_loss=6.4204e-01 best_ppl=1.90
Epoch 200 - |param|=9.97e+02 |g_param|=3.77e+04 loss_x2y=1.1433e-01 ppl_x2y=1.12 loss_y2x=1.1998e-01 ppl_y2x=1.13 dual_loss=3.5093e-01
Validation X2Y - loss=8.6257e-01 ppl=2.37 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6098e-01 ppl=2.14 best_loss=6.4204e-01 best_ppl=1.90
Epoch 201 - |param|=9.97e+02 |g_param|=3.99e+04 loss_x2y=1.1339e-01 ppl_x2y=1.12 loss_y2x=1.2459e-01 ppl_y2x=1.13 dual_loss=3.7230e-01
Validation X2Y - loss=8.5590e-01 ppl=2.35 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6632e-01 ppl=2.15 best_loss=6.4204e-01 best_ppl=1.90
Epoch 202 - |param|=9.97e+02 |g_param|=3.94e+04 loss_x2y=1.1105e-01 ppl_x2y=1.12 loss_y2x=1.3690e-01 ppl_y2x=1.15 dual_loss=3.9948e-01
Validation X2Y - loss=8.7246e-01 ppl=2.39 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6260e-01 ppl=2.14 best_loss=6.4204e-01 best_ppl=1.90
Epoch 203 - |param|=9.98e+02 |g_param|=4.74e+04 loss_x2y=1.1677e-01 ppl_x2y=1.12 loss_y2x=1.2420e-01 ppl_y2x=1.13 dual_loss=3.6038e-01
Validation X2Y - loss=8.6432e-01 ppl=2.37 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6052e-01 ppl=2.14 best_loss=6.4204e-01 best_ppl=1.90
Epoch 204 - |param|=9.98e+02 |g_param|=4.39e+04 loss_x2y=1.1571e-01 ppl_x2y=1.12 loss_y2x=1.1693e-01 ppl_y2x=1.12 dual_loss=4.3951e-01
Validation X2Y - loss=8.5139e-01 ppl=2.34 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9274e-01 ppl=2.21 best_loss=6.4204e-01 best_ppl=1.90
Epoch 205 - |param|=9.98e+02 |g_param|=3.62e+04 loss_x2y=1.0459e-01 ppl_x2y=1.11 loss_y2x=1.1811e-01 ppl_y2x=1.13 dual_loss=3.1360e-01
Validation X2Y - loss=8.5865e-01 ppl=2.36 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6852e-01 ppl=2.16 best_loss=6.4204e-01 best_ppl=1.90
Epoch 206 - |param|=9.99e+02 |g_param|=3.44e+04 loss_x2y=9.8926e-02 ppl_x2y=1.10 loss_y2x=1.2090e-01 ppl_y2x=1.13 dual_loss=3.6276e-01
Validation X2Y - loss=8.6661e-01 ppl=2.38 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6677e-01 ppl=2.15 best_loss=6.4204e-01 best_ppl=1.90
Epoch 207 - |param|=9.99e+02 |g_param|=4.49e+04 loss_x2y=1.0206e-01 ppl_x2y=1.11 loss_y2x=1.2264e-01 ppl_y2x=1.13 dual_loss=4.5502e-01
Validation X2Y - loss=8.6129e-01 ppl=2.37 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1421e-01 ppl=2.26 best_loss=6.4204e-01 best_ppl=1.90
Epoch 208 - |param|=1.00e+03 |g_param|=5.82e+04 loss_x2y=9.8053e-02 ppl_x2y=1.10 loss_y2x=1.2669e-01 ppl_y2x=1.14 dual_loss=4.1643e-01
Validation X2Y - loss=8.8891e-01 ppl=2.43 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8485e-01 ppl=2.19 best_loss=6.4204e-01 best_ppl=1.90
Epoch 209 - |param|=1.00e+03 |g_param|=5.95e+04 loss_x2y=1.0295e-01 ppl_x2y=1.11 loss_y2x=1.5282e-01 ppl_y2x=1.17 dual_loss=4.8050e-01
Validation X2Y - loss=8.7088e-01 ppl=2.39 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6369e-01 ppl=2.15 best_loss=6.4204e-01 best_ppl=1.90
Epoch 210 - |param|=1.00e+03 |g_param|=5.71e+04 loss_x2y=9.4755e-02 ppl_x2y=1.10 loss_y2x=1.3005e-01 ppl_y2x=1.14 dual_loss=4.0612e-01
Validation X2Y - loss=8.9023e-01 ppl=2.44 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.4730e-01 ppl=2.11 best_loss=6.4204e-01 best_ppl=1.90
Epoch 211 - |param|=1.00e+03 |g_param|=5.60e+04 loss_x2y=9.6172e-02 ppl_x2y=1.10 loss_y2x=1.2562e-01 ppl_y2x=1.13 dual_loss=3.8291e-01
Validation X2Y - loss=8.8094e-01 ppl=2.41 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6240e-01 ppl=2.14 best_loss=6.4204e-01 best_ppl=1.90
Epoch 212 - |param|=1.00e+03 |g_param|=5.26e+04 loss_x2y=9.7524e-02 ppl_x2y=1.10 loss_y2x=1.2441e-01 ppl_y2x=1.13 dual_loss=3.9427e-01
Validation X2Y - loss=9.0390e-01 ppl=2.47 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9301e-01 ppl=2.21 best_loss=6.4204e-01 best_ppl=1.90
Epoch 213 - |param|=1.00e+03 |g_param|=5.95e+04 loss_x2y=9.7275e-02 ppl_x2y=1.10 loss_y2x=1.2633e-01 ppl_y2x=1.13 dual_loss=5.5597e-01
Validation X2Y - loss=9.0172e-01 ppl=2.46 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8800e-01 ppl=2.20 best_loss=6.4204e-01 best_ppl=1.90
Epoch 214 - |param|=1.00e+03 |g_param|=6.33e+04 loss_x2y=1.2007e-01 ppl_x2y=1.13 loss_y2x=2.4644e-01 ppl_y2x=1.28 dual_loss=1.1844e+00
Validation X2Y - loss=9.0673e-01 ppl=2.48 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3131e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 215 - |param|=1.00e+03 |g_param|=4.93e+04 loss_x2y=1.1098e-01 ppl_x2y=1.12 loss_y2x=1.7579e-01 ppl_y2x=1.19 dual_loss=6.8725e-01
Validation X2Y - loss=9.1582e-01 ppl=2.50 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6765e-01 ppl=2.15 best_loss=6.4204e-01 best_ppl=1.90
Epoch 216 - |param|=1.00e+03 |g_param|=3.82e+04 loss_x2y=1.0177e-01 ppl_x2y=1.11 loss_y2x=1.4990e-01 ppl_y2x=1.16 dual_loss=4.7933e-01
Validation X2Y - loss=9.1371e-01 ppl=2.49 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0258e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 217 - |param|=1.00e+03 |g_param|=2.40e+04 loss_x2y=1.0268e-01 ppl_x2y=1.11 loss_y2x=1.3300e-01 ppl_y2x=1.14 dual_loss=4.3018e-01
Validation X2Y - loss=9.0399e-01 ppl=2.47 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.7178e-01 ppl=2.16 best_loss=6.4204e-01 best_ppl=1.90
Epoch 218 - |param|=1.00e+03 |g_param|=1.84e+04 loss_x2y=9.8579e-02 ppl_x2y=1.10 loss_y2x=1.2056e-01 ppl_y2x=1.13 dual_loss=3.7945e-01
Validation X2Y - loss=9.1285e-01 ppl=2.49 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.7199e-01 ppl=2.16 best_loss=6.4204e-01 best_ppl=1.90
Epoch 219 - |param|=1.00e+03 |g_param|=1.73e+04 loss_x2y=1.0342e-01 ppl_x2y=1.11 loss_y2x=1.1494e-01 ppl_y2x=1.12 dual_loss=3.2873e-01
Validation X2Y - loss=9.3320e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8030e-01 ppl=2.18 best_loss=6.4204e-01 best_ppl=1.90
Epoch 220 - |param|=1.00e+03 |g_param|=2.84e+04 loss_x2y=1.2020e-01 ppl_x2y=1.13 loss_y2x=1.1761e-01 ppl_y2x=1.12 dual_loss=3.4226e-01
Validation X2Y - loss=9.2669e-01 ppl=2.53 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0994e-01 ppl=2.25 best_loss=6.4204e-01 best_ppl=1.90
Epoch 221 - |param|=1.00e+03 |g_param|=2.81e+04 loss_x2y=1.2632e-01 ppl_x2y=1.13 loss_y2x=1.1058e-01 ppl_y2x=1.12 dual_loss=3.2645e-01
Validation X2Y - loss=9.1861e-01 ppl=2.51 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9023e-01 ppl=2.20 best_loss=6.4204e-01 best_ppl=1.90
Epoch 222 - |param|=1.00e+03 |g_param|=2.12e+04 loss_x2y=1.1665e-01 ppl_x2y=1.12 loss_y2x=1.0613e-01 ppl_y2x=1.11 dual_loss=3.0612e-01
Validation X2Y - loss=9.2460e-01 ppl=2.52 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0312e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 223 - |param|=1.01e+03 |g_param|=1.51e+04 loss_x2y=9.8152e-02 ppl_x2y=1.10 loss_y2x=1.0204e-01 ppl_y2x=1.11 dual_loss=3.4008e-01
Validation X2Y - loss=9.1735e-01 ppl=2.50 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8108e-01 ppl=2.18 best_loss=6.4204e-01 best_ppl=1.90
Epoch 224 - |param|=1.01e+03 |g_param|=1.57e+04 loss_x2y=9.6158e-02 ppl_x2y=1.10 loss_y2x=1.0433e-01 ppl_y2x=1.11 dual_loss=3.7738e-01
Validation X2Y - loss=9.2310e-01 ppl=2.52 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.5806e-01 ppl=2.13 best_loss=6.4204e-01 best_ppl=1.90
Epoch 225 - |param|=1.01e+03 |g_param|=1.49e+04 loss_x2y=9.6925e-02 ppl_x2y=1.10 loss_y2x=1.0415e-01 ppl_y2x=1.11 dual_loss=3.5114e-01
Validation X2Y - loss=9.2340e-01 ppl=2.52 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.6088e-01 ppl=2.14 best_loss=6.4204e-01 best_ppl=1.90
Epoch 226 - |param|=1.01e+03 |g_param|=2.73e+04 loss_x2y=1.0888e-01 ppl_x2y=1.12 loss_y2x=1.0587e-01 ppl_y2x=1.11 dual_loss=3.9610e-01
Validation X2Y - loss=9.1921e-01 ppl=2.51 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.7998e-01 ppl=2.18 best_loss=6.4204e-01 best_ppl=1.90
Epoch 227 - |param|=1.01e+03 |g_param|=1.94e+04 loss_x2y=1.0561e-01 ppl_x2y=1.11 loss_y2x=1.0557e-01 ppl_y2x=1.11 dual_loss=3.7494e-01
Validation X2Y - loss=9.1771e-01 ppl=2.50 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8339e-01 ppl=2.19 best_loss=6.4204e-01 best_ppl=1.90
Epoch 228 - |param|=1.01e+03 |g_param|=1.84e+04 loss_x2y=9.5863e-02 ppl_x2y=1.10 loss_y2x=9.9760e-02 ppl_y2x=1.10 dual_loss=3.4658e-01
Validation X2Y - loss=9.3382e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.7864e-01 ppl=2.18 best_loss=6.4204e-01 best_ppl=1.90
Epoch 229 - |param|=1.01e+03 |g_param|=1.53e+04 loss_x2y=8.6224e-02 ppl_x2y=1.09 loss_y2x=9.1861e-02 ppl_y2x=1.10 dual_loss=3.3914e-01
Validation X2Y - loss=9.2236e-01 ppl=2.52 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9655e-01 ppl=2.22 best_loss=6.4204e-01 best_ppl=1.90
Epoch 230 - |param|=1.01e+03 |g_param|=1.42e+04 loss_x2y=8.7667e-02 ppl_x2y=1.09 loss_y2x=9.8619e-02 ppl_y2x=1.10 dual_loss=3.5352e-01
Validation X2Y - loss=9.3157e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8573e-01 ppl=2.19 best_loss=6.4204e-01 best_ppl=1.90
Epoch 231 - |param|=1.01e+03 |g_param|=1.53e+04 loss_x2y=8.4072e-02 ppl_x2y=1.09 loss_y2x=1.0163e-01 ppl_y2x=1.11 dual_loss=3.7097e-01
Validation X2Y - loss=9.2824e-01 ppl=2.53 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.7717e-01 ppl=2.18 best_loss=6.4204e-01 best_ppl=1.90
Epoch 232 - |param|=1.01e+03 |g_param|=1.80e+04 loss_x2y=8.7503e-02 ppl_x2y=1.09 loss_y2x=1.0083e-01 ppl_y2x=1.11 dual_loss=3.9489e-01
Validation X2Y - loss=9.0841e-01 ppl=2.48 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0110e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 233 - |param|=1.01e+03 |g_param|=1.56e+04 loss_x2y=8.0284e-02 ppl_x2y=1.08 loss_y2x=9.7182e-02 ppl_y2x=1.10 dual_loss=4.3186e-01
Validation X2Y - loss=9.2115e-01 ppl=2.51 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8898e-01 ppl=2.20 best_loss=6.4204e-01 best_ppl=1.90
Epoch 234 - |param|=1.01e+03 |g_param|=1.55e+04 loss_x2y=8.2083e-02 ppl_x2y=1.09 loss_y2x=9.8907e-02 ppl_y2x=1.10 dual_loss=4.3678e-01
Validation X2Y - loss=9.3947e-01 ppl=2.56 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0047e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 235 - |param|=1.01e+03 |g_param|=1.29e+04 loss_x2y=8.4696e-02 ppl_x2y=1.09 loss_y2x=9.9413e-02 ppl_y2x=1.10 dual_loss=4.0191e-01
Validation X2Y - loss=9.2423e-01 ppl=2.52 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0587e-01 ppl=2.24 best_loss=6.4204e-01 best_ppl=1.90
Epoch 236 - |param|=1.01e+03 |g_param|=1.26e+04 loss_x2y=7.7751e-02 ppl_x2y=1.08 loss_y2x=1.0142e-01 ppl_y2x=1.11 dual_loss=3.6196e-01
Validation X2Y - loss=9.1847e-01 ppl=2.51 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0730e-01 ppl=2.24 best_loss=6.4204e-01 best_ppl=1.90
Epoch 237 - |param|=1.01e+03 |g_param|=1.20e+04 loss_x2y=7.5644e-02 ppl_x2y=1.08 loss_y2x=9.4003e-02 ppl_y2x=1.10 dual_loss=3.3942e-01
Validation X2Y - loss=9.3912e-01 ppl=2.56 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3171e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 238 - |param|=1.01e+03 |g_param|=2.80e+04 loss_x2y=7.9338e-02 ppl_x2y=1.08 loss_y2x=9.9989e-02 ppl_y2x=1.11 dual_loss=4.1443e-01
Validation X2Y - loss=9.3414e-01 ppl=2.55 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0339e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 239 - |param|=1.01e+03 |g_param|=3.12e+04 loss_x2y=7.8320e-02 ppl_x2y=1.08 loss_y2x=1.0253e-01 ppl_y2x=1.11 dual_loss=4.4533e-01
Validation X2Y - loss=9.6374e-01 ppl=2.62 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0070e-01 ppl=2.23 best_loss=6.4204e-01 best_ppl=1.90
Epoch 240 - |param|=1.01e+03 |g_param|=2.74e+04 loss_x2y=7.8460e-02 ppl_x2y=1.08 loss_y2x=1.0827e-01 ppl_y2x=1.11 dual_loss=3.6417e-01
Validation X2Y - loss=9.4636e-01 ppl=2.58 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2368e-01 ppl=2.28 best_loss=6.4204e-01 best_ppl=1.90
Epoch 241 - |param|=1.01e+03 |g_param|=3.22e+04 loss_x2y=8.3864e-02 ppl_x2y=1.09 loss_y2x=1.0296e-01 ppl_y2x=1.11 dual_loss=4.2191e-01
Validation X2Y - loss=9.3103e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.8921e-01 ppl=2.20 best_loss=6.4204e-01 best_ppl=1.90
Epoch 242 - |param|=1.01e+03 |g_param|=2.85e+04 loss_x2y=8.1945e-02 ppl_x2y=1.09 loss_y2x=1.0014e-01 ppl_y2x=1.11 dual_loss=4.5132e-01
Validation X2Y - loss=9.4284e-01 ppl=2.57 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1739e-01 ppl=2.26 best_loss=6.4204e-01 best_ppl=1.90
Epoch 243 - |param|=1.01e+03 |g_param|=3.14e+04 loss_x2y=8.3694e-02 ppl_x2y=1.09 loss_y2x=1.0049e-01 ppl_y2x=1.11 dual_loss=4.7591e-01
Validation X2Y - loss=9.2942e-01 ppl=2.53 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9930e-01 ppl=2.22 best_loss=6.4204e-01 best_ppl=1.90
Epoch 244 - |param|=1.01e+03 |g_param|=2.91e+04 loss_x2y=7.9216e-02 ppl_x2y=1.08 loss_y2x=9.6097e-02 ppl_y2x=1.10 dual_loss=4.0334e-01
Validation X2Y - loss=9.3063e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1133e-01 ppl=2.25 best_loss=6.4204e-01 best_ppl=1.90
Epoch 245 - |param|=1.01e+03 |g_param|=3.96e+04 loss_x2y=8.7691e-02 ppl_x2y=1.09 loss_y2x=9.7872e-02 ppl_y2x=1.10 dual_loss=3.7066e-01
Validation X2Y - loss=9.3963e-01 ppl=2.56 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1557e-01 ppl=2.26 best_loss=6.4204e-01 best_ppl=1.90
Epoch 246 - |param|=1.01e+03 |g_param|=5.72e+04 loss_x2y=1.0226e-01 ppl_x2y=1.11 loss_y2x=9.8918e-02 ppl_y2x=1.10 dual_loss=4.8265e-01
Validation X2Y - loss=9.3045e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5808e-01 ppl=2.36 best_loss=6.4204e-01 best_ppl=1.90
Epoch 247 - |param|=1.01e+03 |g_param|=2.94e+04 loss_x2y=1.3141e-01 ppl_x2y=1.14 loss_y2x=8.6094e-02 ppl_y2x=1.09 dual_loss=3.5056e-01
Validation X2Y - loss=9.5793e-01 ppl=2.61 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4797e-01 ppl=2.33 best_loss=6.4204e-01 best_ppl=1.90
Epoch 248 - |param|=1.01e+03 |g_param|=2.14e+04 loss_x2y=1.0392e-01 ppl_x2y=1.11 loss_y2x=8.6733e-02 ppl_y2x=1.09 dual_loss=3.1080e-01
Validation X2Y - loss=9.6587e-01 ppl=2.63 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1713e-01 ppl=2.26 best_loss=6.4204e-01 best_ppl=1.90
Epoch 249 - |param|=1.01e+03 |g_param|=1.59e+04 loss_x2y=9.0296e-02 ppl_x2y=1.09 loss_y2x=9.2377e-02 ppl_y2x=1.10 dual_loss=3.6756e-01
Validation X2Y - loss=9.4419e-01 ppl=2.57 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=7.9687e-01 ppl=2.22 best_loss=6.4204e-01 best_ppl=1.90
Epoch 250 - |param|=1.01e+03 |g_param|=1.58e+04 loss_x2y=8.5527e-02 ppl_x2y=1.09 loss_y2x=9.4306e-02 ppl_y2x=1.10 dual_loss=4.0062e-01
Validation X2Y - loss=9.5714e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.0925e-01 ppl=2.25 best_loss=6.4204e-01 best_ppl=1.90
Epoch 251 - |param|=1.01e+03 |g_param|=1.29e+04 loss_x2y=7.6702e-02 ppl_x2y=1.08 loss_y2x=8.6038e-02 ppl_y2x=1.09 dual_loss=4.0813e-01
Validation X2Y - loss=9.6084e-01 ppl=2.61 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4275e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 252 - |param|=1.01e+03 |g_param|=1.48e+04 loss_x2y=7.8977e-02 ppl_x2y=1.08 loss_y2x=9.8607e-02 ppl_y2x=1.10 dual_loss=3.8770e-01
Validation X2Y - loss=9.5963e-01 ppl=2.61 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3507e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 253 - |param|=1.01e+03 |g_param|=1.27e+04 loss_x2y=7.6975e-02 ppl_x2y=1.08 loss_y2x=9.1362e-02 ppl_y2x=1.10 dual_loss=3.6528e-01
Validation X2Y - loss=9.5963e-01 ppl=2.61 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1924e-01 ppl=2.27 best_loss=6.4204e-01 best_ppl=1.90
Epoch 254 - |param|=1.01e+03 |g_param|=1.60e+04 loss_x2y=7.6040e-02 ppl_x2y=1.08 loss_y2x=9.1123e-02 ppl_y2x=1.10 dual_loss=3.7991e-01
Validation X2Y - loss=9.5441e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6122e-01 ppl=2.37 best_loss=6.4204e-01 best_ppl=1.90
Epoch 255 - |param|=1.02e+03 |g_param|=1.54e+04 loss_x2y=7.7026e-02 ppl_x2y=1.08 loss_y2x=8.9938e-02 ppl_y2x=1.09 dual_loss=4.3804e-01
Validation X2Y - loss=9.7082e-01 ppl=2.64 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6216e-01 ppl=2.37 best_loss=6.4204e-01 best_ppl=1.90
Epoch 256 - |param|=1.02e+03 |g_param|=1.35e+04 loss_x2y=7.5337e-02 ppl_x2y=1.08 loss_y2x=9.0393e-02 ppl_y2x=1.09 dual_loss=4.4973e-01
Validation X2Y - loss=9.6942e-01 ppl=2.64 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2993e-01 ppl=2.29 best_loss=6.4204e-01 best_ppl=1.90
Epoch 257 - |param|=1.02e+03 |g_param|=1.33e+04 loss_x2y=7.5545e-02 ppl_x2y=1.08 loss_y2x=1.0169e-01 ppl_y2x=1.11 dual_loss=4.6607e-01
Validation X2Y - loss=9.5281e-01 ppl=2.59 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3984e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 258 - |param|=1.02e+03 |g_param|=1.23e+04 loss_x2y=7.0494e-02 ppl_x2y=1.07 loss_y2x=1.0270e-01 ppl_y2x=1.11 dual_loss=4.3716e-01
Validation X2Y - loss=9.6466e-01 ppl=2.62 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2085e-01 ppl=2.27 best_loss=6.4204e-01 best_ppl=1.90
Epoch 259 - |param|=1.02e+03 |g_param|=1.59e+04 loss_x2y=7.7835e-02 ppl_x2y=1.08 loss_y2x=9.4541e-02 ppl_y2x=1.10 dual_loss=3.5631e-01
Validation X2Y - loss=9.7619e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3593e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 260 - |param|=1.02e+03 |g_param|=1.46e+04 loss_x2y=7.7737e-02 ppl_x2y=1.08 loss_y2x=9.9102e-02 ppl_y2x=1.10 dual_loss=4.0448e-01
Validation X2Y - loss=9.8895e-01 ppl=2.69 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3286e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 261 - |param|=1.02e+03 |g_param|=1.53e+04 loss_x2y=7.3574e-02 ppl_x2y=1.08 loss_y2x=8.9791e-02 ppl_y2x=1.09 dual_loss=3.9465e-01
Validation X2Y - loss=9.6017e-01 ppl=2.61 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3481e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 262 - |param|=1.02e+03 |g_param|=1.62e+04 loss_x2y=7.5031e-02 ppl_x2y=1.08 loss_y2x=8.7784e-02 ppl_y2x=1.09 dual_loss=3.7640e-01
Validation X2Y - loss=9.9742e-01 ppl=2.71 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2491e-01 ppl=2.28 best_loss=6.4204e-01 best_ppl=1.90
Epoch 263 - |param|=1.02e+03 |g_param|=1.47e+04 loss_x2y=7.4832e-02 ppl_x2y=1.08 loss_y2x=8.6302e-02 ppl_y2x=1.09 dual_loss=3.7225e-01
Validation X2Y - loss=9.6626e-01 ppl=2.63 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3017e-01 ppl=2.29 best_loss=6.4204e-01 best_ppl=1.90
Epoch 264 - |param|=1.02e+03 |g_param|=1.39e+04 loss_x2y=7.4619e-02 ppl_x2y=1.08 loss_y2x=8.5671e-02 ppl_y2x=1.09 dual_loss=3.8492e-01
Validation X2Y - loss=9.5659e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3618e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 265 - |param|=1.02e+03 |g_param|=1.38e+04 loss_x2y=7.1147e-02 ppl_x2y=1.07 loss_y2x=8.1788e-02 ppl_y2x=1.09 dual_loss=3.1928e-01
Validation X2Y - loss=9.5590e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4633e-01 ppl=2.33 best_loss=6.4204e-01 best_ppl=1.90
Epoch 266 - |param|=1.02e+03 |g_param|=1.60e+04 loss_x2y=7.7106e-02 ppl_x2y=1.08 loss_y2x=8.2865e-02 ppl_y2x=1.09 dual_loss=3.5818e-01
Validation X2Y - loss=9.7466e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3038e-01 ppl=2.29 best_loss=6.4204e-01 best_ppl=1.90
Epoch 267 - |param|=1.02e+03 |g_param|=2.28e+04 loss_x2y=6.9874e-02 ppl_x2y=1.07 loss_y2x=7.6782e-02 ppl_y2x=1.08 dual_loss=3.3672e-01
Validation X2Y - loss=9.6476e-01 ppl=2.62 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3264e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 268 - |param|=1.02e+03 |g_param|=2.43e+04 loss_x2y=6.5757e-02 ppl_x2y=1.07 loss_y2x=7.5675e-02 ppl_y2x=1.08 dual_loss=3.1972e-01
Validation X2Y - loss=9.6482e-01 ppl=2.62 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4294e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 269 - |param|=1.02e+03 |g_param|=2.66e+04 loss_x2y=6.8016e-02 ppl_x2y=1.07 loss_y2x=7.7245e-02 ppl_y2x=1.08 dual_loss=3.8204e-01
Validation X2Y - loss=9.8726e-01 ppl=2.68 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5543e-01 ppl=2.35 best_loss=6.4204e-01 best_ppl=1.90
Epoch 270 - |param|=1.02e+03 |g_param|=2.77e+04 loss_x2y=7.0891e-02 ppl_x2y=1.07 loss_y2x=8.0046e-02 ppl_y2x=1.08 dual_loss=3.6756e-01
Validation X2Y - loss=9.8716e-01 ppl=2.68 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4098e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 271 - |param|=1.02e+03 |g_param|=2.67e+04 loss_x2y=6.7355e-02 ppl_x2y=1.07 loss_y2x=7.2826e-02 ppl_y2x=1.08 dual_loss=3.5351e-01
Validation X2Y - loss=9.7448e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5130e-01 ppl=2.34 best_loss=6.4204e-01 best_ppl=1.90
Epoch 272 - |param|=1.02e+03 |g_param|=2.84e+04 loss_x2y=6.9558e-02 ppl_x2y=1.07 loss_y2x=8.5694e-02 ppl_y2x=1.09 dual_loss=4.3092e-01
Validation X2Y - loss=9.8643e-01 ppl=2.68 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3920e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 273 - |param|=1.02e+03 |g_param|=3.41e+04 loss_x2y=7.6015e-02 ppl_x2y=1.08 loss_y2x=9.0400e-02 ppl_y2x=1.09 dual_loss=3.6902e-01
Validation X2Y - loss=9.7897e-01 ppl=2.66 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.7172e-01 ppl=2.39 best_loss=6.4204e-01 best_ppl=1.90
Epoch 274 - |param|=1.02e+03 |g_param|=2.74e+04 loss_x2y=8.7555e-02 ppl_x2y=1.09 loss_y2x=1.1776e-01 ppl_y2x=1.12 dual_loss=5.3048e-01
Validation X2Y - loss=9.7649e-01 ppl=2.66 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4251e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 275 - |param|=1.02e+03 |g_param|=1.85e+04 loss_x2y=7.7550e-02 ppl_x2y=1.08 loss_y2x=1.0799e-01 ppl_y2x=1.11 dual_loss=4.4285e-01
Validation X2Y - loss=9.7578e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5438e-01 ppl=2.35 best_loss=6.4204e-01 best_ppl=1.90
Epoch 276 - |param|=1.02e+03 |g_param|=1.78e+04 loss_x2y=7.4868e-02 ppl_x2y=1.08 loss_y2x=1.0418e-01 ppl_y2x=1.11 dual_loss=4.4625e-01
Validation X2Y - loss=9.8980e-01 ppl=2.69 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4795e-01 ppl=2.33 best_loss=6.4204e-01 best_ppl=1.90
Epoch 277 - |param|=1.02e+03 |g_param|=1.94e+04 loss_x2y=7.1209e-02 ppl_x2y=1.07 loss_y2x=9.2605e-02 ppl_y2x=1.10 dual_loss=5.1029e-01
Validation X2Y - loss=9.7104e-01 ppl=2.64 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4623e-01 ppl=2.33 best_loss=6.4204e-01 best_ppl=1.90
Epoch 278 - |param|=1.02e+03 |g_param|=1.59e+04 loss_x2y=6.8438e-02 ppl_x2y=1.07 loss_y2x=8.5835e-02 ppl_y2x=1.09 dual_loss=4.2324e-01
Validation X2Y - loss=9.9140e-01 ppl=2.70 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4076e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 279 - |param|=1.02e+03 |g_param|=1.62e+04 loss_x2y=6.8964e-02 ppl_x2y=1.07 loss_y2x=7.8462e-02 ppl_y2x=1.08 dual_loss=3.6514e-01
Validation X2Y - loss=1.0075e+00 ppl=2.74 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3453e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 280 - |param|=1.02e+03 |g_param|=1.78e+04 loss_x2y=6.9445e-02 ppl_x2y=1.07 loss_y2x=7.5633e-02 ppl_y2x=1.08 dual_loss=4.3638e-01
Validation X2Y - loss=1.0200e+00 ppl=2.77 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2738e-01 ppl=2.29 best_loss=6.4204e-01 best_ppl=1.90
Epoch 281 - |param|=1.02e+03 |g_param|=1.38e+04 loss_x2y=6.4637e-02 ppl_x2y=1.07 loss_y2x=7.6341e-02 ppl_y2x=1.08 dual_loss=3.3779e-01
Validation X2Y - loss=1.0045e+00 ppl=2.73 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3799e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 282 - |param|=1.02e+03 |g_param|=1.51e+04 loss_x2y=6.7962e-02 ppl_x2y=1.07 loss_y2x=7.2822e-02 ppl_y2x=1.08 dual_loss=3.4212e-01
Validation X2Y - loss=1.0098e+00 ppl=2.75 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3607e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 283 - |param|=1.02e+03 |g_param|=1.59e+04 loss_x2y=6.5870e-02 ppl_x2y=1.07 loss_y2x=7.3838e-02 ppl_y2x=1.08 dual_loss=3.5407e-01
Validation X2Y - loss=1.0129e+00 ppl=2.75 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4547e-01 ppl=2.33 best_loss=6.4204e-01 best_ppl=1.90
Epoch 284 - |param|=1.02e+03 |g_param|=1.47e+04 loss_x2y=6.3516e-02 ppl_x2y=1.07 loss_y2x=6.9707e-02 ppl_y2x=1.07 dual_loss=3.8721e-01
Validation X2Y - loss=9.9746e-01 ppl=2.71 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5553e-01 ppl=2.35 best_loss=6.4204e-01 best_ppl=1.90
Epoch 285 - |param|=1.02e+03 |g_param|=1.68e+04 loss_x2y=6.7448e-02 ppl_x2y=1.07 loss_y2x=7.6635e-02 ppl_y2x=1.08 dual_loss=4.1261e-01
Validation X2Y - loss=1.0174e+00 ppl=2.77 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6016e-01 ppl=2.36 best_loss=6.4204e-01 best_ppl=1.90
Epoch 286 - |param|=1.02e+03 |g_param|=2.17e+04 loss_x2y=7.1850e-02 ppl_x2y=1.07 loss_y2x=8.6488e-02 ppl_y2x=1.09 dual_loss=4.6652e-01
Validation X2Y - loss=1.0269e+00 ppl=2.79 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9654e-01 ppl=2.45 best_loss=6.4204e-01 best_ppl=1.90
Epoch 287 - |param|=1.03e+03 |g_param|=3.28e+04 loss_x2y=9.8459e-02 ppl_x2y=1.10 loss_y2x=1.8588e-01 ppl_y2x=1.20 dual_loss=1.0546e+00
Validation X2Y - loss=1.0223e+00 ppl=2.78 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0204e+00 ppl=2.77 best_loss=6.4204e-01 best_ppl=1.90
Epoch 288 - |param|=1.03e+03 |g_param|=3.52e+04 loss_x2y=1.4700e-01 ppl_x2y=1.16 loss_y2x=1.6826e-01 ppl_y2x=1.18 dual_loss=1.6777e+00
Validation X2Y - loss=1.0576e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.1676e-01 ppl=2.26 best_loss=6.4204e-01 best_ppl=1.90
Epoch 289 - |param|=1.03e+03 |g_param|=2.70e+04 loss_x2y=1.1590e-01 ppl_x2y=1.12 loss_y2x=1.1458e-01 ppl_y2x=1.12 dual_loss=4.7167e-01
Validation X2Y - loss=1.0081e+00 ppl=2.74 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3930e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 290 - |param|=1.03e+03 |g_param|=3.28e+04 loss_x2y=1.2384e-01 ppl_x2y=1.13 loss_y2x=9.1274e-02 ppl_y2x=1.10 dual_loss=6.1497e-01
Validation X2Y - loss=9.9531e-01 ppl=2.71 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3484e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 291 - |param|=1.03e+03 |g_param|=2.76e+04 loss_x2y=1.5109e-01 ppl_x2y=1.16 loss_y2x=8.3503e-02 ppl_y2x=1.09 dual_loss=5.1450e-01
Validation X2Y - loss=9.6128e-01 ppl=2.62 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3777e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 292 - |param|=1.03e+03 |g_param|=2.32e+04 loss_x2y=1.1847e-01 ppl_x2y=1.13 loss_y2x=7.8274e-02 ppl_y2x=1.08 dual_loss=6.3404e-01
Validation X2Y - loss=9.6733e-01 ppl=2.63 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.2794e-01 ppl=2.29 best_loss=6.4204e-01 best_ppl=1.90
Epoch 293 - |param|=1.03e+03 |g_param|=2.03e+04 loss_x2y=1.8484e-01 ppl_x2y=1.20 loss_y2x=8.0225e-02 ppl_y2x=1.08 dual_loss=4.4507e-01
Validation X2Y - loss=9.7626e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3933e-01 ppl=2.31 best_loss=6.4204e-01 best_ppl=1.90
Epoch 294 - |param|=1.03e+03 |g_param|=1.18e+04 loss_x2y=1.1499e-01 ppl_x2y=1.12 loss_y2x=7.0131e-02 ppl_y2x=1.07 dual_loss=3.3253e-01
Validation X2Y - loss=9.3182e-01 ppl=2.54 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.3430e-01 ppl=2.30 best_loss=6.4204e-01 best_ppl=1.90
Epoch 295 - |param|=1.03e+03 |g_param|=1.01e+04 loss_x2y=9.0791e-02 ppl_x2y=1.10 loss_y2x=6.7423e-02 ppl_y2x=1.07 dual_loss=3.5962e-01
Validation X2Y - loss=9.4237e-01 ppl=2.57 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.4212e-01 ppl=2.32 best_loss=6.4204e-01 best_ppl=1.90
Epoch 296 - |param|=1.03e+03 |g_param|=6.61e+03 loss_x2y=7.4735e-02 ppl_x2y=1.08 loss_y2x=6.4250e-02 ppl_y2x=1.07 dual_loss=3.1259e-01
Validation X2Y - loss=9.5069e-01 ppl=2.59 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.7186e-01 ppl=2.39 best_loss=6.4204e-01 best_ppl=1.90
Epoch 297 - |param|=1.03e+03 |g_param|=7.73e+03 loss_x2y=7.8760e-02 ppl_x2y=1.08 loss_y2x=7.0819e-02 ppl_y2x=1.07 dual_loss=4.1623e-01
Validation X2Y - loss=9.5612e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5781e-01 ppl=2.36 best_loss=6.4204e-01 best_ppl=1.90
Epoch 298 - |param|=1.03e+03 |g_param|=7.16e+03 loss_x2y=7.1806e-02 ppl_x2y=1.07 loss_y2x=6.4317e-02 ppl_y2x=1.07 dual_loss=3.7882e-01
Validation X2Y - loss=9.5528e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.5668e-01 ppl=2.36 best_loss=6.4204e-01 best_ppl=1.90
Epoch 299 - |param|=1.03e+03 |g_param|=6.49e+03 loss_x2y=7.0136e-02 ppl_x2y=1.07 loss_y2x=6.4439e-02 ppl_y2x=1.07 dual_loss=3.6629e-01
Validation X2Y - loss=9.4248e-01 ppl=2.57 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6301e-01 ppl=2.37 best_loss=6.4204e-01 best_ppl=1.90
Epoch 300 - |param|=1.03e+03 |g_param|=6.21e+03 loss_x2y=6.6301e-02 ppl_x2y=1.07 loss_y2x=6.4887e-02 ppl_y2x=1.07 dual_loss=3.5482e-01
Validation X2Y - loss=9.8166e-01 ppl=2.67 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6318e-01 ppl=2.37 best_loss=6.4204e-01 best_ppl=1.90
Epoch 301 - |param|=1.03e+03 |g_param|=5.51e+03 loss_x2y=6.2919e-02 ppl_x2y=1.06 loss_y2x=6.1964e-02 ppl_y2x=1.06 dual_loss=3.1586e-01
Validation X2Y - loss=9.5597e-01 ppl=2.60 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6169e-01 ppl=2.37 best_loss=6.4204e-01 best_ppl=1.90
Epoch 302 - |param|=1.03e+03 |g_param|=6.04e+03 loss_x2y=6.3590e-02 ppl_x2y=1.07 loss_y2x=5.9587e-02 ppl_y2x=1.06 dual_loss=3.8257e-01
Validation X2Y - loss=9.6853e-01 ppl=2.63 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6779e-01 ppl=2.38 best_loss=6.4204e-01 best_ppl=1.90
Epoch 303 - |param|=1.03e+03 |g_param|=5.74e+03 loss_x2y=6.3170e-02 ppl_x2y=1.07 loss_y2x=6.4227e-02 ppl_y2x=1.07 dual_loss=3.8219e-01
Validation X2Y - loss=9.7262e-01 ppl=2.64 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.6749e-01 ppl=2.38 best_loss=6.4204e-01 best_ppl=1.90
Epoch 304 - |param|=1.03e+03 |g_param|=5.69e+03 loss_x2y=6.0171e-02 ppl_x2y=1.06 loss_y2x=6.3566e-02 ppl_y2x=1.07 dual_loss=3.9387e-01
Validation X2Y - loss=9.7555e-01 ppl=2.65 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.7568e-01 ppl=2.40 best_loss=6.4204e-01 best_ppl=1.90
Epoch 305 - |param|=1.03e+03 |g_param|=5.02e+03 loss_x2y=6.1148e-02 ppl_x2y=1.06 loss_y2x=6.4817e-02 ppl_y2x=1.07 dual_loss=4.1464e-01
Validation X2Y - loss=9.8409e-01 ppl=2.68 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9656e-01 ppl=2.45 best_loss=6.4204e-01 best_ppl=1.90
Epoch 306 - |param|=1.03e+03 |g_param|=5.92e+03 loss_x2y=5.9019e-02 ppl_x2y=1.06 loss_y2x=6.2305e-02 ppl_y2x=1.06 dual_loss=3.8732e-01
Validation X2Y - loss=9.8444e-01 ppl=2.68 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0447e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 307 - |param|=1.03e+03 |g_param|=6.18e+03 loss_x2y=6.0419e-02 ppl_x2y=1.06 loss_y2x=6.1139e-02 ppl_y2x=1.06 dual_loss=3.9028e-01
Validation X2Y - loss=9.9877e-01 ppl=2.71 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9192e-01 ppl=2.44 best_loss=6.4204e-01 best_ppl=1.90
Epoch 308 - |param|=1.03e+03 |g_param|=5.84e+03 loss_x2y=5.7711e-02 ppl_x2y=1.06 loss_y2x=6.1890e-02 ppl_y2x=1.06 dual_loss=4.1087e-01
Validation X2Y - loss=9.9944e-01 ppl=2.72 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9329e-01 ppl=2.44 best_loss=6.4204e-01 best_ppl=1.90
Epoch 309 - |param|=1.03e+03 |g_param|=8.39e+03 loss_x2y=5.9946e-02 ppl_x2y=1.06 loss_y2x=6.5692e-02 ppl_y2x=1.07 dual_loss=4.0738e-01
Validation X2Y - loss=1.0011e+00 ppl=2.72 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1866e-01 ppl=2.51 best_loss=6.4204e-01 best_ppl=1.90
Epoch 310 - |param|=1.03e+03 |g_param|=1.07e+04 loss_x2y=6.5194e-02 ppl_x2y=1.07 loss_y2x=1.2050e-01 ppl_y2x=1.13 dual_loss=5.4784e-01
Validation X2Y - loss=9.9702e-01 ppl=2.71 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0759e-01 ppl=2.48 best_loss=6.4204e-01 best_ppl=1.90
Epoch 311 - |param|=1.03e+03 |g_param|=1.06e+04 loss_x2y=6.5191e-02 ppl_x2y=1.07 loss_y2x=1.2766e-01 ppl_y2x=1.14 dual_loss=5.7348e-01
Validation X2Y - loss=1.0170e+00 ppl=2.76 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.8195e-01 ppl=2.42 best_loss=6.4204e-01 best_ppl=1.90
Epoch 312 - |param|=1.03e+03 |g_param|=1.20e+04 loss_x2y=6.2666e-02 ppl_x2y=1.06 loss_y2x=1.1382e-01 ppl_y2x=1.12 dual_loss=5.7931e-01
Validation X2Y - loss=9.9920e-01 ppl=2.72 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.8439e-01 ppl=2.42 best_loss=6.4204e-01 best_ppl=1.90
Epoch 313 - |param|=1.03e+03 |g_param|=1.35e+04 loss_x2y=5.9357e-02 ppl_x2y=1.06 loss_y2x=9.0360e-02 ppl_y2x=1.09 dual_loss=4.9412e-01
Validation X2Y - loss=1.0123e+00 ppl=2.75 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.8010e-01 ppl=2.41 best_loss=6.4204e-01 best_ppl=1.90
Epoch 314 - |param|=1.03e+03 |g_param|=1.40e+04 loss_x2y=6.0479e-02 ppl_x2y=1.06 loss_y2x=8.2412e-02 ppl_y2x=1.09 dual_loss=4.6081e-01
Validation X2Y - loss=1.0003e+00 ppl=2.72 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.7092e-01 ppl=2.39 best_loss=6.4204e-01 best_ppl=1.90
Epoch 315 - |param|=1.03e+03 |g_param|=1.10e+04 loss_x2y=5.6347e-02 ppl_x2y=1.06 loss_y2x=7.5084e-02 ppl_y2x=1.08 dual_loss=3.5859e-01
Validation X2Y - loss=1.0047e+00 ppl=2.73 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.7262e-01 ppl=2.39 best_loss=6.4204e-01 best_ppl=1.90
Epoch 316 - |param|=1.03e+03 |g_param|=1.17e+04 loss_x2y=5.6258e-02 ppl_x2y=1.06 loss_y2x=7.2429e-02 ppl_y2x=1.08 dual_loss=3.8432e-01
Validation X2Y - loss=1.0041e+00 ppl=2.73 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0070e-01 ppl=2.46 best_loss=6.4204e-01 best_ppl=1.90
Epoch 317 - |param|=1.03e+03 |g_param|=1.00e+04 loss_x2y=5.5257e-02 ppl_x2y=1.06 loss_y2x=6.6019e-02 ppl_y2x=1.07 dual_loss=4.0923e-01
Validation X2Y - loss=1.0212e+00 ppl=2.78 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.8974e-01 ppl=2.43 best_loss=6.4204e-01 best_ppl=1.90
Epoch 318 - |param|=1.03e+03 |g_param|=1.08e+04 loss_x2y=5.5244e-02 ppl_x2y=1.06 loss_y2x=6.4945e-02 ppl_y2x=1.07 dual_loss=4.4040e-01
Validation X2Y - loss=1.0229e+00 ppl=2.78 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0549e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 319 - |param|=1.03e+03 |g_param|=1.25e+04 loss_x2y=5.7669e-02 ppl_x2y=1.06 loss_y2x=6.4063e-02 ppl_y2x=1.07 dual_loss=3.9560e-01
Validation X2Y - loss=1.0236e+00 ppl=2.78 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9638e-01 ppl=2.45 best_loss=6.4204e-01 best_ppl=1.90
Epoch 320 - |param|=1.03e+03 |g_param|=1.13e+04 loss_x2y=5.4279e-02 ppl_x2y=1.06 loss_y2x=5.9805e-02 ppl_y2x=1.06 dual_loss=3.3506e-01
Validation X2Y - loss=1.0341e+00 ppl=2.81 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.8162e-01 ppl=2.41 best_loss=6.4204e-01 best_ppl=1.90
Epoch 321 - |param|=1.03e+03 |g_param|=1.21e+04 loss_x2y=6.0584e-02 ppl_x2y=1.06 loss_y2x=6.2073e-02 ppl_y2x=1.06 dual_loss=3.7436e-01
Validation X2Y - loss=1.0134e+00 ppl=2.75 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=8.9143e-01 ppl=2.44 best_loss=6.4204e-01 best_ppl=1.90
Epoch 322 - |param|=1.03e+03 |g_param|=1.27e+04 loss_x2y=6.1016e-02 ppl_x2y=1.06 loss_y2x=6.4213e-02 ppl_y2x=1.07 dual_loss=3.9550e-01
Validation X2Y - loss=1.0444e+00 ppl=2.84 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1126e-01 ppl=2.49 best_loss=6.4204e-01 best_ppl=1.90
Epoch 323 - |param|=1.03e+03 |g_param|=1.48e+04 loss_x2y=6.4360e-02 ppl_x2y=1.07 loss_y2x=6.5457e-02 ppl_y2x=1.07 dual_loss=3.8359e-01
Validation X2Y - loss=1.0391e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0424e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 324 - |param|=1.03e+03 |g_param|=1.07e+04 loss_x2y=5.5863e-02 ppl_x2y=1.06 loss_y2x=6.2209e-02 ppl_y2x=1.06 dual_loss=3.6924e-01
Validation X2Y - loss=1.0476e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0395e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 325 - |param|=1.03e+03 |g_param|=1.46e+04 loss_x2y=6.2398e-02 ppl_x2y=1.06 loss_y2x=6.2147e-02 ppl_y2x=1.06 dual_loss=3.8062e-01
Validation X2Y - loss=1.0501e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0037e-01 ppl=2.46 best_loss=6.4204e-01 best_ppl=1.90
Epoch 326 - |param|=1.03e+03 |g_param|=1.21e+04 loss_x2y=6.0446e-02 ppl_x2y=1.06 loss_y2x=6.0525e-02 ppl_y2x=1.06 dual_loss=3.7236e-01
Validation X2Y - loss=1.0386e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2564e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 327 - |param|=1.04e+03 |g_param|=1.53e+04 loss_x2y=6.2944e-02 ppl_x2y=1.06 loss_y2x=6.0298e-02 ppl_y2x=1.06 dual_loss=3.7965e-01
Validation X2Y - loss=1.0504e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0504e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 328 - |param|=1.04e+03 |g_param|=1.65e+04 loss_x2y=6.7843e-02 ppl_x2y=1.07 loss_y2x=6.3247e-02 ppl_y2x=1.07 dual_loss=3.8379e-01
Validation X2Y - loss=1.0489e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1737e-01 ppl=2.50 best_loss=6.4204e-01 best_ppl=1.90
Epoch 329 - |param|=1.04e+03 |g_param|=1.59e+04 loss_x2y=6.5341e-02 ppl_x2y=1.07 loss_y2x=6.4541e-02 ppl_y2x=1.07 dual_loss=3.9741e-01
Validation X2Y - loss=1.0640e+00 ppl=2.90 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2100e-01 ppl=2.51 best_loss=6.4204e-01 best_ppl=1.90
Epoch 330 - |param|=1.04e+03 |g_param|=1.70e+04 loss_x2y=6.6586e-02 ppl_x2y=1.07 loss_y2x=6.2670e-02 ppl_y2x=1.06 dual_loss=3.9858e-01
Validation X2Y - loss=1.0373e+00 ppl=2.82 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2708e-01 ppl=2.53 best_loss=6.4204e-01 best_ppl=1.90
Epoch 331 - |param|=1.04e+03 |g_param|=1.54e+04 loss_x2y=6.2752e-02 ppl_x2y=1.06 loss_y2x=6.2346e-02 ppl_y2x=1.06 dual_loss=4.0083e-01
Validation X2Y - loss=1.0725e+00 ppl=2.92 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0577e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 332 - |param|=1.04e+03 |g_param|=2.62e+04 loss_x2y=6.0404e-02 ppl_x2y=1.06 loss_y2x=5.9613e-02 ppl_y2x=1.06 dual_loss=3.5147e-01
Validation X2Y - loss=1.0794e+00 ppl=2.94 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3311e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 333 - |param|=1.04e+03 |g_param|=3.12e+04 loss_x2y=6.3440e-02 ppl_x2y=1.07 loss_y2x=5.9989e-02 ppl_y2x=1.06 dual_loss=4.2544e-01
Validation X2Y - loss=1.0587e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0713e-01 ppl=2.48 best_loss=6.4204e-01 best_ppl=1.90
Epoch 334 - |param|=1.04e+03 |g_param|=4.08e+04 loss_x2y=7.2719e-02 ppl_x2y=1.08 loss_y2x=5.7601e-02 ppl_y2x=1.06 dual_loss=3.3515e-01
Validation X2Y - loss=1.0895e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2400e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 335 - |param|=1.04e+03 |g_param|=4.10e+04 loss_x2y=8.1492e-02 ppl_x2y=1.08 loss_y2x=5.8276e-02 ppl_y2x=1.06 dual_loss=3.2373e-01
Validation X2Y - loss=1.0533e+00 ppl=2.87 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4184e-01 ppl=2.56 best_loss=6.4204e-01 best_ppl=1.90
Epoch 336 - |param|=1.04e+03 |g_param|=3.92e+04 loss_x2y=7.8811e-02 ppl_x2y=1.08 loss_y2x=6.2573e-02 ppl_y2x=1.06 dual_loss=3.5681e-01
Validation X2Y - loss=1.0671e+00 ppl=2.91 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5509e-01 ppl=2.60 best_loss=6.4204e-01 best_ppl=1.90
Epoch 337 - |param|=1.04e+03 |g_param|=3.12e+04 loss_x2y=6.5737e-02 ppl_x2y=1.07 loss_y2x=6.1356e-02 ppl_y2x=1.06 dual_loss=3.2096e-01
Validation X2Y - loss=1.0473e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4845e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 338 - |param|=1.04e+03 |g_param|=3.82e+04 loss_x2y=7.1761e-02 ppl_x2y=1.07 loss_y2x=6.5160e-02 ppl_y2x=1.07 dual_loss=3.5375e-01
Validation X2Y - loss=1.0740e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4901e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 339 - |param|=1.04e+03 |g_param|=3.21e+04 loss_x2y=6.2141e-02 ppl_x2y=1.06 loss_y2x=5.9453e-02 ppl_y2x=1.06 dual_loss=4.0705e-01
Validation X2Y - loss=1.0583e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4016e-01 ppl=2.56 best_loss=6.4204e-01 best_ppl=1.90
Epoch 340 - |param|=1.04e+03 |g_param|=2.90e+04 loss_x2y=6.1516e-02 ppl_x2y=1.06 loss_y2x=6.1639e-02 ppl_y2x=1.06 dual_loss=3.8380e-01
Validation X2Y - loss=1.0811e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2872e-01 ppl=2.53 best_loss=6.4204e-01 best_ppl=1.90
Epoch 341 - |param|=1.04e+03 |g_param|=2.76e+04 loss_x2y=5.7505e-02 ppl_x2y=1.06 loss_y2x=5.6396e-02 ppl_y2x=1.06 dual_loss=4.2060e-01
Validation X2Y - loss=1.0458e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3204e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 342 - |param|=1.04e+03 |g_param|=2.77e+04 loss_x2y=6.2476e-02 ppl_x2y=1.06 loss_y2x=9.7177e-02 ppl_y2x=1.10 dual_loss=5.9166e-01
Validation X2Y - loss=1.0526e+00 ppl=2.87 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3391e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 343 - |param|=1.04e+03 |g_param|=2.91e+04 loss_x2y=6.1334e-02 ppl_x2y=1.06 loss_y2x=8.8603e-02 ppl_y2x=1.09 dual_loss=5.9654e-01
Validation X2Y - loss=1.0684e+00 ppl=2.91 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3185e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 344 - |param|=1.04e+03 |g_param|=4.78e+04 loss_x2y=9.6128e-02 ppl_x2y=1.10 loss_y2x=1.5757e-01 ppl_y2x=1.17 dual_loss=9.3248e-01
Validation X2Y - loss=1.1045e+00 ppl=3.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8817e-01 ppl=2.69 best_loss=6.4204e-01 best_ppl=1.90
Epoch 345 - |param|=1.04e+03 |g_param|=2.91e+04 loss_x2y=9.1840e-02 ppl_x2y=1.10 loss_y2x=1.3220e-01 ppl_y2x=1.14 dual_loss=5.8932e-01
Validation X2Y - loss=1.1052e+00 ppl=3.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2555e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 346 - |param|=1.04e+03 |g_param|=2.23e+04 loss_x2y=8.9851e-02 ppl_x2y=1.09 loss_y2x=8.8114e-02 ppl_y2x=1.09 dual_loss=5.1132e-01
Validation X2Y - loss=1.0874e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0584e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 347 - |param|=1.04e+03 |g_param|=2.67e+04 loss_x2y=1.2038e-01 ppl_x2y=1.13 loss_y2x=9.0986e-02 ppl_y2x=1.10 dual_loss=8.5608e-01
Validation X2Y - loss=1.0979e+00 ppl=3.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1457e-01 ppl=2.50 best_loss=6.4204e-01 best_ppl=1.90
Epoch 348 - |param|=1.04e+03 |g_param|=1.52e+04 loss_x2y=1.1012e-01 ppl_x2y=1.12 loss_y2x=1.0106e-01 ppl_y2x=1.11 dual_loss=6.3472e-01
Validation X2Y - loss=1.0392e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7208e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 349 - |param|=1.04e+03 |g_param|=1.53e+04 loss_x2y=1.0106e-01 ppl_x2y=1.11 loss_y2x=1.2844e-01 ppl_y2x=1.14 dual_loss=7.4600e-01
Validation X2Y - loss=1.0306e+00 ppl=2.80 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4433e-01 ppl=2.57 best_loss=6.4204e-01 best_ppl=1.90
Epoch 350 - |param|=1.04e+03 |g_param|=2.15e+04 loss_x2y=1.1216e-01 ppl_x2y=1.12 loss_y2x=1.0175e-01 ppl_y2x=1.11 dual_loss=8.0257e-01
Validation X2Y - loss=1.0373e+00 ppl=2.82 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1221e-01 ppl=2.49 best_loss=6.4204e-01 best_ppl=1.90
Epoch 351 - |param|=1.04e+03 |g_param|=1.59e+04 loss_x2y=1.1353e-01 ppl_x2y=1.12 loss_y2x=9.8939e-02 ppl_y2x=1.10 dual_loss=6.1269e-01
Validation X2Y - loss=1.0394e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2984e-01 ppl=2.53 best_loss=6.4204e-01 best_ppl=1.90
Epoch 352 - |param|=1.04e+03 |g_param|=1.50e+04 loss_x2y=9.8216e-02 ppl_x2y=1.10 loss_y2x=8.4450e-02 ppl_y2x=1.09 dual_loss=5.1088e-01
Validation X2Y - loss=1.0493e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.0335e-01 ppl=2.47 best_loss=6.4204e-01 best_ppl=1.90
Epoch 353 - |param|=1.04e+03 |g_param|=1.47e+04 loss_x2y=7.9518e-02 ppl_x2y=1.08 loss_y2x=8.2939e-02 ppl_y2x=1.09 dual_loss=5.9835e-01
Validation X2Y - loss=1.0310e+00 ppl=2.80 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4738e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 354 - |param|=1.04e+03 |g_param|=1.21e+04 loss_x2y=8.8994e-02 ppl_x2y=1.09 loss_y2x=1.0131e-01 ppl_y2x=1.11 dual_loss=4.9951e-01
Validation X2Y - loss=1.0327e+00 ppl=2.81 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2286e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 355 - |param|=1.04e+03 |g_param|=8.30e+03 loss_x2y=7.1302e-02 ppl_x2y=1.07 loss_y2x=8.0478e-02 ppl_y2x=1.08 dual_loss=3.8745e-01
Validation X2Y - loss=1.0316e+00 ppl=2.81 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2165e-01 ppl=2.51 best_loss=6.4204e-01 best_ppl=1.90
Epoch 356 - |param|=1.04e+03 |g_param|=7.48e+03 loss_x2y=6.4411e-02 ppl_x2y=1.07 loss_y2x=6.8393e-02 ppl_y2x=1.07 dual_loss=3.6136e-01
Validation X2Y - loss=1.0401e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1739e-01 ppl=2.50 best_loss=6.4204e-01 best_ppl=1.90
Epoch 357 - |param|=1.04e+03 |g_param|=7.19e+03 loss_x2y=5.8061e-02 ppl_x2y=1.06 loss_y2x=6.0076e-02 ppl_y2x=1.06 dual_loss=3.3458e-01
Validation X2Y - loss=1.0302e+00 ppl=2.80 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1088e-01 ppl=2.49 best_loss=6.4204e-01 best_ppl=1.90
Epoch 358 - |param|=1.04e+03 |g_param|=7.37e+03 loss_x2y=6.0872e-02 ppl_x2y=1.06 loss_y2x=6.1026e-02 ppl_y2x=1.06 dual_loss=3.6407e-01
Validation X2Y - loss=1.0307e+00 ppl=2.80 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2174e-01 ppl=2.51 best_loss=6.4204e-01 best_ppl=1.90
Epoch 359 - |param|=1.04e+03 |g_param|=6.62e+03 loss_x2y=5.4052e-02 ppl_x2y=1.06 loss_y2x=5.8389e-02 ppl_y2x=1.06 dual_loss=3.5124e-01
Validation X2Y - loss=1.0525e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1222e-01 ppl=2.49 best_loss=6.4204e-01 best_ppl=1.90
Epoch 360 - |param|=1.04e+03 |g_param|=6.17e+03 loss_x2y=5.4955e-02 ppl_x2y=1.06 loss_y2x=5.6861e-02 ppl_y2x=1.06 dual_loss=4.1096e-01
Validation X2Y - loss=1.0414e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2270e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 361 - |param|=1.04e+03 |g_param|=8.77e+03 loss_x2y=5.8206e-02 ppl_x2y=1.06 loss_y2x=6.0180e-02 ppl_y2x=1.06 dual_loss=4.7885e-01
Validation X2Y - loss=1.0263e+00 ppl=2.79 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3110e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 362 - |param|=1.04e+03 |g_param|=8.48e+03 loss_x2y=5.9726e-02 ppl_x2y=1.06 loss_y2x=6.0491e-02 ppl_y2x=1.06 dual_loss=4.3898e-01
Validation X2Y - loss=1.0243e+00 ppl=2.79 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3622e-01 ppl=2.55 best_loss=6.4204e-01 best_ppl=1.90
Epoch 363 - |param|=1.04e+03 |g_param|=7.89e+03 loss_x2y=5.5466e-02 ppl_x2y=1.06 loss_y2x=5.8333e-02 ppl_y2x=1.06 dual_loss=3.9710e-01
Validation X2Y - loss=1.0387e+00 ppl=2.83 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.1704e-01 ppl=2.50 best_loss=6.4204e-01 best_ppl=1.90
Epoch 364 - |param|=1.04e+03 |g_param|=5.49e+03 loss_x2y=5.0574e-02 ppl_x2y=1.05 loss_y2x=5.5818e-02 ppl_y2x=1.06 dual_loss=3.7039e-01
Validation X2Y - loss=1.0585e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2552e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 365 - |param|=1.05e+03 |g_param|=5.82e+03 loss_x2y=5.3868e-02 ppl_x2y=1.06 loss_y2x=5.5501e-02 ppl_y2x=1.06 dual_loss=4.5214e-01
Validation X2Y - loss=1.0483e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2830e-01 ppl=2.53 best_loss=6.4204e-01 best_ppl=1.90
Epoch 366 - |param|=1.05e+03 |g_param|=6.48e+03 loss_x2y=5.2482e-02 ppl_x2y=1.05 loss_y2x=5.5502e-02 ppl_y2x=1.06 dual_loss=4.6666e-01
Validation X2Y - loss=1.0376e+00 ppl=2.82 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3029e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 367 - |param|=1.05e+03 |g_param|=1.08e+04 loss_x2y=4.9021e-02 ppl_x2y=1.05 loss_y2x=5.2845e-02 ppl_y2x=1.05 dual_loss=3.5319e-01
Validation X2Y - loss=1.0351e+00 ppl=2.82 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4255e-01 ppl=2.57 best_loss=6.4204e-01 best_ppl=1.90
Epoch 368 - |param|=1.05e+03 |g_param|=1.24e+04 loss_x2y=5.2731e-02 ppl_x2y=1.05 loss_y2x=5.9418e-02 ppl_y2x=1.06 dual_loss=4.7376e-01
Validation X2Y - loss=1.0438e+00 ppl=2.84 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4844e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 369 - |param|=1.05e+03 |g_param|=1.39e+04 loss_x2y=5.1812e-02 ppl_x2y=1.05 loss_y2x=6.4277e-02 ppl_y2x=1.07 dual_loss=4.1162e-01
Validation X2Y - loss=1.0357e+00 ppl=2.82 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2240e-01 ppl=2.52 best_loss=6.4204e-01 best_ppl=1.90
Epoch 370 - |param|=1.05e+03 |g_param|=1.65e+04 loss_x2y=5.2364e-02 ppl_x2y=1.05 loss_y2x=5.6549e-02 ppl_y2x=1.06 dual_loss=4.6980e-01
Validation X2Y - loss=1.0534e+00 ppl=2.87 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3852e-01 ppl=2.56 best_loss=6.4204e-01 best_ppl=1.90
Epoch 371 - |param|=1.05e+03 |g_param|=1.44e+04 loss_x2y=5.3176e-02 ppl_x2y=1.05 loss_y2x=5.2557e-02 ppl_y2x=1.05 dual_loss=3.8026e-01
Validation X2Y - loss=1.0498e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4594e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 372 - |param|=1.05e+03 |g_param|=1.20e+04 loss_x2y=5.1079e-02 ppl_x2y=1.05 loss_y2x=5.2889e-02 ppl_y2x=1.05 dual_loss=3.5787e-01
Validation X2Y - loss=1.0661e+00 ppl=2.90 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4814e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 373 - |param|=1.05e+03 |g_param|=1.31e+04 loss_x2y=5.1888e-02 ppl_x2y=1.05 loss_y2x=5.1893e-02 ppl_y2x=1.05 dual_loss=3.4581e-01
Validation X2Y - loss=1.0468e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4553e-01 ppl=2.57 best_loss=6.4204e-01 best_ppl=1.90
Epoch 374 - |param|=1.05e+03 |g_param|=1.17e+04 loss_x2y=5.1916e-02 ppl_x2y=1.05 loss_y2x=5.5057e-02 ppl_y2x=1.06 dual_loss=4.1396e-01
Validation X2Y - loss=1.0602e+00 ppl=2.89 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4621e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 375 - |param|=1.05e+03 |g_param|=1.24e+04 loss_x2y=4.8463e-02 ppl_x2y=1.05 loss_y2x=5.4622e-02 ppl_y2x=1.06 dual_loss=3.9119e-01
Validation X2Y - loss=1.0733e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6649e-01 ppl=2.63 best_loss=6.4204e-01 best_ppl=1.90
Epoch 376 - |param|=1.05e+03 |g_param|=1.32e+04 loss_x2y=5.0705e-02 ppl_x2y=1.05 loss_y2x=5.0462e-02 ppl_y2x=1.05 dual_loss=4.2095e-01
Validation X2Y - loss=1.0810e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5181e-01 ppl=2.59 best_loss=6.4204e-01 best_ppl=1.90
Epoch 377 - |param|=1.05e+03 |g_param|=1.19e+04 loss_x2y=4.8073e-02 ppl_x2y=1.05 loss_y2x=5.1688e-02 ppl_y2x=1.05 dual_loss=3.6867e-01
Validation X2Y - loss=1.0753e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6669e-01 ppl=2.63 best_loss=6.4204e-01 best_ppl=1.90
Epoch 378 - |param|=1.05e+03 |g_param|=1.52e+04 loss_x2y=5.5095e-02 ppl_x2y=1.06 loss_y2x=6.0626e-02 ppl_y2x=1.06 dual_loss=4.6002e-01
Validation X2Y - loss=1.0564e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6591e-01 ppl=2.63 best_loss=6.4204e-01 best_ppl=1.90
Epoch 379 - |param|=1.05e+03 |g_param|=2.54e+04 loss_x2y=6.3958e-02 ppl_x2y=1.07 loss_y2x=1.0933e-01 ppl_y2x=1.12 dual_loss=6.1207e-01
Validation X2Y - loss=1.0629e+00 ppl=2.89 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8064e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 380 - |param|=1.05e+03 |g_param|=3.18e+04 loss_x2y=7.3367e-02 ppl_x2y=1.08 loss_y2x=1.3028e-01 ppl_y2x=1.14 dual_loss=8.1297e-01
Validation X2Y - loss=1.0487e+00 ppl=2.85 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8168e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 381 - |param|=1.05e+03 |g_param|=2.66e+04 loss_x2y=7.2260e-02 ppl_x2y=1.07 loss_y2x=1.5104e-01 ppl_y2x=1.16 dual_loss=8.4383e-01
Validation X2Y - loss=1.0931e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7224e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 382 - |param|=1.05e+03 |g_param|=1.99e+04 loss_x2y=6.3294e-02 ppl_x2y=1.07 loss_y2x=9.0272e-02 ppl_y2x=1.09 dual_loss=4.5009e-01
Validation X2Y - loss=1.0805e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8184e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 383 - |param|=1.05e+03 |g_param|=1.71e+04 loss_x2y=6.0691e-02 ppl_x2y=1.06 loss_y2x=7.5868e-02 ppl_y2x=1.08 dual_loss=4.3240e-01
Validation X2Y - loss=1.0605e+00 ppl=2.89 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3150e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 384 - |param|=1.05e+03 |g_param|=2.08e+04 loss_x2y=6.3181e-02 ppl_x2y=1.07 loss_y2x=6.7752e-02 ppl_y2x=1.07 dual_loss=3.7870e-01
Validation X2Y - loss=1.0741e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4763e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 385 - |param|=1.05e+03 |g_param|=2.33e+04 loss_x2y=7.5169e-02 ppl_x2y=1.08 loss_y2x=6.1214e-02 ppl_y2x=1.06 dual_loss=3.7284e-01
Validation X2Y - loss=1.0519e+00 ppl=2.86 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3249e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 386 - |param|=1.05e+03 |g_param|=1.86e+04 loss_x2y=6.7799e-02 ppl_x2y=1.07 loss_y2x=5.7630e-02 ppl_y2x=1.06 dual_loss=4.1709e-01
Validation X2Y - loss=1.0891e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3449e-01 ppl=2.55 best_loss=6.4204e-01 best_ppl=1.90
Epoch 387 - |param|=1.05e+03 |g_param|=2.70e+04 loss_x2y=6.4030e-02 ppl_x2y=1.07 loss_y2x=5.4003e-02 ppl_y2x=1.06 dual_loss=3.7378e-01
Validation X2Y - loss=1.0990e+00 ppl=3.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3570e-01 ppl=2.55 best_loss=6.4204e-01 best_ppl=1.90
Epoch 388 - |param|=1.05e+03 |g_param|=2.85e+04 loss_x2y=5.7004e-02 ppl_x2y=1.06 loss_y2x=4.9060e-02 ppl_y2x=1.05 dual_loss=3.3893e-01
Validation X2Y - loss=1.0657e+00 ppl=2.90 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.2821e-01 ppl=2.53 best_loss=6.4204e-01 best_ppl=1.90
Epoch 389 - |param|=1.05e+03 |g_param|=2.99e+04 loss_x2y=5.8985e-02 ppl_x2y=1.06 loss_y2x=5.2032e-02 ppl_y2x=1.05 dual_loss=3.6520e-01
Validation X2Y - loss=1.0912e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3225e-01 ppl=2.54 best_loss=6.4204e-01 best_ppl=1.90
Epoch 390 - |param|=1.05e+03 |g_param|=2.62e+04 loss_x2y=5.4572e-02 ppl_x2y=1.06 loss_y2x=4.9567e-02 ppl_y2x=1.05 dual_loss=3.4019e-01
Validation X2Y - loss=1.0816e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3745e-01 ppl=2.55 best_loss=6.4204e-01 best_ppl=1.90
Epoch 391 - |param|=1.05e+03 |g_param|=3.36e+04 loss_x2y=5.6457e-02 ppl_x2y=1.06 loss_y2x=4.8437e-02 ppl_y2x=1.05 dual_loss=3.4910e-01
Validation X2Y - loss=1.0565e+00 ppl=2.88 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3698e-01 ppl=2.55 best_loss=6.4204e-01 best_ppl=1.90
Epoch 392 - |param|=1.05e+03 |g_param|=3.71e+04 loss_x2y=5.7955e-02 ppl_x2y=1.06 loss_y2x=4.9417e-02 ppl_y2x=1.05 dual_loss=3.8569e-01
Validation X2Y - loss=1.0953e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4767e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 393 - |param|=1.05e+03 |g_param|=1.67e+04 loss_x2y=5.5608e-02 ppl_x2y=1.06 loss_y2x=4.9053e-02 ppl_y2x=1.05 dual_loss=3.7490e-01
Validation X2Y - loss=1.0828e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4647e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 394 - |param|=1.05e+03 |g_param|=1.74e+04 loss_x2y=5.2293e-02 ppl_x2y=1.05 loss_y2x=4.7776e-02 ppl_y2x=1.05 dual_loss=3.7292e-01
Validation X2Y - loss=1.0960e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5819e-01 ppl=2.61 best_loss=6.4204e-01 best_ppl=1.90
Epoch 395 - |param|=1.05e+03 |g_param|=1.74e+04 loss_x2y=5.5222e-02 ppl_x2y=1.06 loss_y2x=4.7999e-02 ppl_y2x=1.05 dual_loss=3.8403e-01
Validation X2Y - loss=1.0885e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5323e-01 ppl=2.59 best_loss=6.4204e-01 best_ppl=1.90
Epoch 396 - |param|=1.05e+03 |g_param|=1.83e+04 loss_x2y=5.6878e-02 ppl_x2y=1.06 loss_y2x=4.8222e-02 ppl_y2x=1.05 dual_loss=3.8121e-01
Validation X2Y - loss=1.1382e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.3954e-01 ppl=2.56 best_loss=6.4204e-01 best_ppl=1.90
Epoch 397 - |param|=1.05e+03 |g_param|=1.63e+04 loss_x2y=5.2771e-02 ppl_x2y=1.05 loss_y2x=5.2020e-02 ppl_y2x=1.05 dual_loss=3.5235e-01
Validation X2Y - loss=1.1088e+00 ppl=3.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4335e-01 ppl=2.57 best_loss=6.4204e-01 best_ppl=1.90
Epoch 398 - |param|=1.05e+03 |g_param|=1.73e+04 loss_x2y=5.1685e-02 ppl_x2y=1.05 loss_y2x=4.7839e-02 ppl_y2x=1.05 dual_loss=3.5940e-01
Validation X2Y - loss=1.1013e+00 ppl=3.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6986e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 399 - |param|=1.05e+03 |g_param|=1.64e+04 loss_x2y=4.9223e-02 ppl_x2y=1.05 loss_y2x=5.0065e-02 ppl_y2x=1.05 dual_loss=4.3757e-01
Validation X2Y - loss=1.0914e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5214e-01 ppl=2.59 best_loss=6.4204e-01 best_ppl=1.90
Epoch 400 - |param|=1.05e+03 |g_param|=1.68e+04 loss_x2y=4.9508e-02 ppl_x2y=1.05 loss_y2x=5.3431e-02 ppl_y2x=1.05 dual_loss=3.7675e-01
Validation X2Y - loss=1.1014e+00 ppl=3.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.4876e-01 ppl=2.58 best_loss=6.4204e-01 best_ppl=1.90
Epoch 401 - |param|=1.05e+03 |g_param|=1.85e+04 loss_x2y=4.9612e-02 ppl_x2y=1.05 loss_y2x=5.7917e-02 ppl_y2x=1.06 dual_loss=3.9446e-01
Validation X2Y - loss=1.0956e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5666e-01 ppl=2.60 best_loss=6.4204e-01 best_ppl=1.90
Epoch 402 - |param|=1.05e+03 |g_param|=2.15e+04 loss_x2y=4.8710e-02 ppl_x2y=1.05 loss_y2x=5.3632e-02 ppl_y2x=1.06 dual_loss=4.1475e-01
Validation X2Y - loss=1.1177e+00 ppl=3.06 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6616e-01 ppl=2.63 best_loss=6.4204e-01 best_ppl=1.90
Epoch 403 - |param|=1.05e+03 |g_param|=2.23e+04 loss_x2y=5.3321e-02 ppl_x2y=1.05 loss_y2x=6.6141e-02 ppl_y2x=1.07 dual_loss=5.0399e-01
Validation X2Y - loss=1.1236e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5454e-01 ppl=2.60 best_loss=6.4204e-01 best_ppl=1.90
Epoch 404 - |param|=1.05e+03 |g_param|=3.50e+04 loss_x2y=6.9580e-02 ppl_x2y=1.07 loss_y2x=5.7835e-02 ppl_y2x=1.06 dual_loss=4.4573e-01
Validation X2Y - loss=1.1590e+00 ppl=3.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5640e-01 ppl=2.60 best_loss=6.4204e-01 best_ppl=1.90
Epoch 405 - |param|=1.05e+03 |g_param|=4.04e+04 loss_x2y=1.0864e-01 ppl_x2y=1.11 loss_y2x=5.2344e-02 ppl_y2x=1.05 dual_loss=3.8503e-01
Validation X2Y - loss=1.0890e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6111e-01 ppl=2.61 best_loss=6.4204e-01 best_ppl=1.90
Epoch 406 - |param|=1.05e+03 |g_param|=3.22e+04 loss_x2y=8.8588e-02 ppl_x2y=1.09 loss_y2x=5.2307e-02 ppl_y2x=1.05 dual_loss=4.6175e-01
Validation X2Y - loss=1.1069e+00 ppl=3.02 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7345e-01 ppl=2.65 best_loss=6.4204e-01 best_ppl=1.90
Epoch 407 - |param|=1.05e+03 |g_param|=3.74e+04 loss_x2y=1.0810e-01 ppl_x2y=1.11 loss_y2x=5.1885e-02 ppl_y2x=1.05 dual_loss=4.0056e-01
Validation X2Y - loss=1.0762e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6326e-01 ppl=2.62 best_loss=6.4204e-01 best_ppl=1.90
Epoch 408 - |param|=1.06e+03 |g_param|=3.36e+04 loss_x2y=1.2995e-01 ppl_x2y=1.14 loss_y2x=5.8223e-02 ppl_y2x=1.06 dual_loss=7.4315e-01
Validation X2Y - loss=1.0778e+00 ppl=2.94 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7209e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 409 - |param|=1.06e+03 |g_param|=2.92e+04 loss_x2y=9.4479e-02 ppl_x2y=1.10 loss_y2x=5.1163e-02 ppl_y2x=1.05 dual_loss=3.8431e-01
Validation X2Y - loss=1.0809e+00 ppl=2.95 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6835e-01 ppl=2.63 best_loss=6.4204e-01 best_ppl=1.90
Epoch 410 - |param|=1.06e+03 |g_param|=2.19e+04 loss_x2y=6.7088e-02 ppl_x2y=1.07 loss_y2x=4.8570e-02 ppl_y2x=1.05 dual_loss=3.3315e-01
Validation X2Y - loss=1.0745e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8558e-01 ppl=2.68 best_loss=6.4204e-01 best_ppl=1.90
Epoch 411 - |param|=1.06e+03 |g_param|=2.58e+04 loss_x2y=6.1637e-02 ppl_x2y=1.06 loss_y2x=4.9495e-02 ppl_y2x=1.05 dual_loss=3.8138e-01
Validation X2Y - loss=1.0745e+00 ppl=2.93 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7221e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 412 - |param|=1.06e+03 |g_param|=2.06e+04 loss_x2y=5.6200e-02 ppl_x2y=1.06 loss_y2x=5.2623e-02 ppl_y2x=1.05 dual_loss=3.5852e-01
Validation X2Y - loss=1.0693e+00 ppl=2.91 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7997e-01 ppl=2.66 best_loss=6.4204e-01 best_ppl=1.90
Epoch 413 - |param|=1.06e+03 |g_param|=1.75e+04 loss_x2y=5.2246e-02 ppl_x2y=1.05 loss_y2x=5.3102e-02 ppl_y2x=1.05 dual_loss=4.1543e-01
Validation X2Y - loss=1.0857e+00 ppl=2.96 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.6054e-01 ppl=2.61 best_loss=6.4204e-01 best_ppl=1.90
Epoch 414 - |param|=1.06e+03 |g_param|=1.75e+04 loss_x2y=5.4430e-02 ppl_x2y=1.06 loss_y2x=5.7235e-02 ppl_y2x=1.06 dual_loss=4.1974e-01
Validation X2Y - loss=1.0958e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7767e-01 ppl=2.66 best_loss=6.4204e-01 best_ppl=1.90
Epoch 415 - |param|=1.06e+03 |g_param|=3.02e+04 loss_x2y=5.6868e-02 ppl_x2y=1.06 loss_y2x=9.2507e-02 ppl_y2x=1.10 dual_loss=5.3241e-01
Validation X2Y - loss=1.0849e+00 ppl=2.96 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7430e-01 ppl=2.65 best_loss=6.4204e-01 best_ppl=1.90
Epoch 416 - |param|=1.06e+03 |g_param|=2.66e+04 loss_x2y=5.7685e-02 ppl_x2y=1.06 loss_y2x=9.1793e-02 ppl_y2x=1.10 dual_loss=5.5813e-01
Validation X2Y - loss=1.1349e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5522e-01 ppl=2.60 best_loss=6.4204e-01 best_ppl=1.90
Epoch 417 - |param|=1.06e+03 |g_param|=1.97e+04 loss_x2y=5.1260e-02 ppl_x2y=1.05 loss_y2x=6.9291e-02 ppl_y2x=1.07 dual_loss=4.6820e-01
Validation X2Y - loss=1.0923e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7158e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 418 - |param|=1.06e+03 |g_param|=2.35e+04 loss_x2y=5.1296e-02 ppl_x2y=1.05 loss_y2x=6.8725e-02 ppl_y2x=1.07 dual_loss=5.7139e-01
Validation X2Y - loss=1.0913e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7077e-01 ppl=2.64 best_loss=6.4204e-01 best_ppl=1.90
Epoch 419 - |param|=1.06e+03 |g_param|=1.73e+04 loss_x2y=4.7640e-02 ppl_x2y=1.05 loss_y2x=6.2563e-02 ppl_y2x=1.06 dual_loss=4.0583e-01
Validation X2Y - loss=1.1035e+00 ppl=3.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7953e-01 ppl=2.66 best_loss=6.4204e-01 best_ppl=1.90
Epoch 420 - |param|=1.06e+03 |g_param|=1.71e+04 loss_x2y=4.7632e-02 ppl_x2y=1.05 loss_y2x=5.7962e-02 ppl_y2x=1.06 dual_loss=3.8753e-01
Validation X2Y - loss=1.0931e+00 ppl=2.98 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8865e-01 ppl=2.69 best_loss=6.4204e-01 best_ppl=1.90
Epoch 421 - |param|=1.06e+03 |g_param|=1.44e+04 loss_x2y=4.6377e-02 ppl_x2y=1.05 loss_y2x=5.6411e-02 ppl_y2x=1.06 dual_loss=4.3156e-01
Validation X2Y - loss=1.0964e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7842e-01 ppl=2.66 best_loss=6.4204e-01 best_ppl=1.90
Epoch 422 - |param|=1.06e+03 |g_param|=1.70e+04 loss_x2y=4.8914e-02 ppl_x2y=1.05 loss_y2x=5.7026e-02 ppl_y2x=1.06 dual_loss=4.0393e-01
Validation X2Y - loss=1.1107e+00 ppl=3.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9441e-01 ppl=2.70 best_loss=6.4204e-01 best_ppl=1.90
Epoch 423 - |param|=1.06e+03 |g_param|=1.53e+04 loss_x2y=4.9005e-02 ppl_x2y=1.05 loss_y2x=5.4269e-02 ppl_y2x=1.06 dual_loss=3.9744e-01
Validation X2Y - loss=1.0940e+00 ppl=2.99 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8918e-01 ppl=2.69 best_loss=6.4204e-01 best_ppl=1.90
Epoch 424 - |param|=1.06e+03 |g_param|=1.41e+04 loss_x2y=4.5946e-02 ppl_x2y=1.05 loss_y2x=5.0571e-02 ppl_y2x=1.05 dual_loss=4.0712e-01
Validation X2Y - loss=1.0892e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7641e-01 ppl=2.65 best_loss=6.4204e-01 best_ppl=1.90
Epoch 425 - |param|=1.06e+03 |g_param|=1.91e+04 loss_x2y=5.0148e-02 ppl_x2y=1.05 loss_y2x=6.1942e-02 ppl_y2x=1.06 dual_loss=4.4097e-01
Validation X2Y - loss=1.1107e+00 ppl=3.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8739e-01 ppl=2.68 best_loss=6.4204e-01 best_ppl=1.90
Epoch 426 - |param|=1.06e+03 |g_param|=2.04e+04 loss_x2y=4.6068e-02 ppl_x2y=1.05 loss_y2x=5.8140e-02 ppl_y2x=1.06 dual_loss=4.2884e-01
Validation X2Y - loss=1.1142e+00 ppl=3.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8602e-01 ppl=2.68 best_loss=6.4204e-01 best_ppl=1.90
Epoch 427 - |param|=1.06e+03 |g_param|=1.68e+04 loss_x2y=5.0719e-02 ppl_x2y=1.05 loss_y2x=5.5114e-02 ppl_y2x=1.06 dual_loss=4.2833e-01
Validation X2Y - loss=1.1089e+00 ppl=3.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0004e+00 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 428 - |param|=1.06e+03 |g_param|=1.46e+04 loss_x2y=4.4772e-02 ppl_x2y=1.05 loss_y2x=4.9691e-02 ppl_y2x=1.05 dual_loss=3.4110e-01
Validation X2Y - loss=1.1230e+00 ppl=3.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9411e-01 ppl=2.70 best_loss=6.4204e-01 best_ppl=1.90
Epoch 429 - |param|=1.06e+03 |g_param|=1.77e+04 loss_x2y=4.8509e-02 ppl_x2y=1.05 loss_y2x=5.0907e-02 ppl_y2x=1.05 dual_loss=4.1020e-01
Validation X2Y - loss=1.1408e+00 ppl=3.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.5790e-01 ppl=2.61 best_loss=6.4204e-01 best_ppl=1.90
Epoch 430 - |param|=1.06e+03 |g_param|=1.87e+04 loss_x2y=4.7335e-02 ppl_x2y=1.05 loss_y2x=5.3944e-02 ppl_y2x=1.06 dual_loss=3.9768e-01
Validation X2Y - loss=1.1307e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.7270e-01 ppl=2.65 best_loss=6.4204e-01 best_ppl=1.90
Epoch 431 - |param|=1.06e+03 |g_param|=1.87e+04 loss_x2y=4.9391e-02 ppl_x2y=1.05 loss_y2x=5.5839e-02 ppl_y2x=1.06 dual_loss=3.9783e-01
Validation X2Y - loss=1.1278e+00 ppl=3.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8029e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 432 - |param|=1.06e+03 |g_param|=2.23e+04 loss_x2y=5.2580e-02 ppl_x2y=1.05 loss_y2x=5.3792e-02 ppl_y2x=1.06 dual_loss=5.1060e-01
Validation X2Y - loss=1.1109e+00 ppl=3.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9155e-01 ppl=2.70 best_loss=6.4204e-01 best_ppl=1.90
Epoch 433 - |param|=1.06e+03 |g_param|=3.48e+04 loss_x2y=5.4077e-02 ppl_x2y=1.06 loss_y2x=5.4618e-02 ppl_y2x=1.06 dual_loss=4.0546e-01
Validation X2Y - loss=1.1191e+00 ppl=3.06 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0014e+00 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 434 - |param|=1.06e+03 |g_param|=3.43e+04 loss_x2y=5.8820e-02 ppl_x2y=1.06 loss_y2x=5.4223e-02 ppl_y2x=1.06 dual_loss=3.7776e-01
Validation X2Y - loss=1.1211e+00 ppl=3.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8251e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 435 - |param|=1.06e+03 |g_param|=2.51e+04 loss_x2y=5.4964e-02 ppl_x2y=1.06 loss_y2x=5.2179e-02 ppl_y2x=1.05 dual_loss=4.9143e-01
Validation X2Y - loss=1.0877e+00 ppl=2.97 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0095e+00 ppl=2.74 best_loss=6.4204e-01 best_ppl=1.90
Epoch 436 - |param|=1.06e+03 |g_param|=2.17e+04 loss_x2y=5.5599e-02 ppl_x2y=1.06 loss_y2x=5.4959e-02 ppl_y2x=1.06 dual_loss=4.1506e-01
Validation X2Y - loss=1.0979e+00 ppl=3.00 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0152e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90
Epoch 437 - |param|=1.06e+03 |g_param|=2.12e+04 loss_x2y=5.2399e-02 ppl_x2y=1.05 loss_y2x=5.5619e-02 ppl_y2x=1.06 dual_loss=4.0640e-01
Validation X2Y - loss=1.1106e+00 ppl=3.04 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0228e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 438 - |param|=1.06e+03 |g_param|=1.92e+04 loss_x2y=4.9208e-02 ppl_x2y=1.05 loss_y2x=5.0245e-02 ppl_y2x=1.05 dual_loss=3.8644e-01
Validation X2Y - loss=1.1427e+00 ppl=3.14 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9763e-01 ppl=2.71 best_loss=6.4204e-01 best_ppl=1.90
Epoch 439 - |param|=1.06e+03 |g_param|=1.94e+04 loss_x2y=5.0337e-02 ppl_x2y=1.05 loss_y2x=5.5574e-02 ppl_y2x=1.06 dual_loss=3.9768e-01
Validation X2Y - loss=1.1233e+00 ppl=3.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9830e-01 ppl=2.71 best_loss=6.4204e-01 best_ppl=1.90
Epoch 440 - |param|=1.06e+03 |g_param|=1.93e+04 loss_x2y=4.8639e-02 ppl_x2y=1.05 loss_y2x=6.2279e-02 ppl_y2x=1.06 dual_loss=3.9754e-01
Validation X2Y - loss=1.1030e+00 ppl=3.01 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0240e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 441 - |param|=1.06e+03 |g_param|=2.27e+04 loss_x2y=4.8046e-02 ppl_x2y=1.05 loss_y2x=7.2008e-02 ppl_y2x=1.07 dual_loss=4.3331e-01
Validation X2Y - loss=1.1168e+00 ppl=3.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0201e+00 ppl=2.77 best_loss=6.4204e-01 best_ppl=1.90
Epoch 442 - |param|=1.06e+03 |g_param|=3.21e+04 loss_x2y=7.9553e-02 ppl_x2y=1.08 loss_y2x=7.3372e-02 ppl_y2x=1.08 dual_loss=6.2061e-01
Validation X2Y - loss=1.0713e+00 ppl=2.92 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0079e+00 ppl=2.74 best_loss=6.4204e-01 best_ppl=1.90
Epoch 443 - |param|=1.06e+03 |g_param|=2.74e+04 loss_x2y=6.4415e-02 ppl_x2y=1.07 loss_y2x=6.8915e-02 ppl_y2x=1.07 dual_loss=4.2930e-01
Validation X2Y - loss=1.1268e+00 ppl=3.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0057e+00 ppl=2.73 best_loss=6.4204e-01 best_ppl=1.90
Epoch 444 - |param|=1.06e+03 |g_param|=2.07e+04 loss_x2y=5.7676e-02 ppl_x2y=1.06 loss_y2x=5.6637e-02 ppl_y2x=1.06 dual_loss=3.8718e-01
Validation X2Y - loss=1.1181e+00 ppl=3.06 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9310e-01 ppl=2.70 best_loss=6.4204e-01 best_ppl=1.90
Epoch 445 - |param|=1.06e+03 |g_param|=2.08e+04 loss_x2y=5.5435e-02 ppl_x2y=1.06 loss_y2x=5.2324e-02 ppl_y2x=1.05 dual_loss=4.5702e-01
Validation X2Y - loss=1.1353e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0013e+00 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 446 - |param|=1.06e+03 |g_param|=1.86e+04 loss_x2y=5.4603e-02 ppl_x2y=1.06 loss_y2x=5.1888e-02 ppl_y2x=1.05 dual_loss=4.1563e-01
Validation X2Y - loss=1.1394e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.8198e-01 ppl=2.67 best_loss=6.4204e-01 best_ppl=1.90
Epoch 447 - |param|=1.06e+03 |g_param|=1.82e+04 loss_x2y=5.1470e-02 ppl_x2y=1.05 loss_y2x=4.7560e-02 ppl_y2x=1.05 dual_loss=4.1176e-01
Validation X2Y - loss=1.1322e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0020e+00 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 448 - |param|=1.06e+03 |g_param|=1.52e+04 loss_x2y=4.6474e-02 ppl_x2y=1.05 loss_y2x=4.3243e-02 ppl_y2x=1.04 dual_loss=3.5638e-01
Validation X2Y - loss=1.1425e+00 ppl=3.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0322e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 449 - |param|=1.06e+03 |g_param|=2.15e+04 loss_x2y=4.6743e-02 ppl_x2y=1.05 loss_y2x=4.3336e-02 ppl_y2x=1.04 dual_loss=3.6546e-01
Validation X2Y - loss=1.1098e+00 ppl=3.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0128e+00 ppl=2.75 best_loss=6.4204e-01 best_ppl=1.90
Epoch 450 - |param|=1.06e+03 |g_param|=2.26e+04 loss_x2y=4.4056e-02 ppl_x2y=1.05 loss_y2x=4.4510e-02 ppl_y2x=1.05 dual_loss=3.5463e-01
Validation X2Y - loss=1.1314e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0081e+00 ppl=2.74 best_loss=6.4204e-01 best_ppl=1.90
Epoch 451 - |param|=1.06e+03 |g_param|=2.17e+04 loss_x2y=4.3272e-02 ppl_x2y=1.04 loss_y2x=4.6284e-02 ppl_y2x=1.05 dual_loss=3.6501e-01
Validation X2Y - loss=1.1497e+00 ppl=3.16 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0244e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 452 - |param|=1.06e+03 |g_param|=2.48e+04 loss_x2y=4.3892e-02 ppl_x2y=1.04 loss_y2x=4.4719e-02 ppl_y2x=1.05 dual_loss=4.2798e-01
Validation X2Y - loss=1.1315e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0167e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90
Epoch 453 - |param|=1.06e+03 |g_param|=2.70e+04 loss_x2y=4.7314e-02 ppl_x2y=1.05 loss_y2x=4.9534e-02 ppl_y2x=1.05 dual_loss=4.1880e-01
Validation X2Y - loss=1.1203e+00 ppl=3.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0080e+00 ppl=2.74 best_loss=6.4204e-01 best_ppl=1.90
Epoch 454 - |param|=1.07e+03 |g_param|=2.81e+04 loss_x2y=4.8250e-02 ppl_x2y=1.05 loss_y2x=5.0920e-02 ppl_y2x=1.05 dual_loss=3.8999e-01
Validation X2Y - loss=1.1303e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0047e+00 ppl=2.73 best_loss=6.4204e-01 best_ppl=1.90
Epoch 455 - |param|=1.07e+03 |g_param|=2.88e+04 loss_x2y=5.1303e-02 ppl_x2y=1.05 loss_y2x=5.2635e-02 ppl_y2x=1.05 dual_loss=3.8201e-01
Validation X2Y - loss=1.1091e+00 ppl=3.03 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0223e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 456 - |param|=1.07e+03 |g_param|=3.34e+04 loss_x2y=4.7365e-02 ppl_x2y=1.05 loss_y2x=5.0340e-02 ppl_y2x=1.05 dual_loss=4.2803e-01
Validation X2Y - loss=1.1390e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0012e+00 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 457 - |param|=1.07e+03 |g_param|=3.79e+04 loss_x2y=5.1436e-02 ppl_x2y=1.05 loss_y2x=5.0125e-02 ppl_y2x=1.05 dual_loss=3.9384e-01
Validation X2Y - loss=1.1289e+00 ppl=3.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9726e-01 ppl=2.71 best_loss=6.4204e-01 best_ppl=1.90
Epoch 458 - |param|=1.07e+03 |g_param|=3.54e+04 loss_x2y=4.8683e-02 ppl_x2y=1.05 loss_y2x=4.8164e-02 ppl_y2x=1.05 dual_loss=3.8583e-01
Validation X2Y - loss=1.1234e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0318e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 459 - |param|=1.07e+03 |g_param|=5.02e+04 loss_x2y=5.1638e-02 ppl_x2y=1.05 loss_y2x=5.0769e-02 ppl_y2x=1.05 dual_loss=4.1384e-01
Validation X2Y - loss=1.1392e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0270e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 460 - |param|=1.07e+03 |g_param|=3.55e+04 loss_x2y=5.2851e-02 ppl_x2y=1.05 loss_y2x=5.1725e-02 ppl_y2x=1.05 dual_loss=4.4545e-01
Validation X2Y - loss=1.1304e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0248e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 461 - |param|=1.07e+03 |g_param|=3.82e+04 loss_x2y=5.4873e-02 ppl_x2y=1.06 loss_y2x=4.9019e-02 ppl_y2x=1.05 dual_loss=3.9521e-01
Validation X2Y - loss=1.1529e+00 ppl=3.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0038e+00 ppl=2.73 best_loss=6.4204e-01 best_ppl=1.90
Epoch 462 - |param|=1.07e+03 |g_param|=4.28e+04 loss_x2y=5.0157e-02 ppl_x2y=1.05 loss_y2x=4.9411e-02 ppl_y2x=1.05 dual_loss=4.1051e-01
Validation X2Y - loss=1.1313e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=9.9970e-01 ppl=2.72 best_loss=6.4204e-01 best_ppl=1.90
Epoch 463 - |param|=1.07e+03 |g_param|=4.71e+04 loss_x2y=5.2003e-02 ppl_x2y=1.05 loss_y2x=5.0566e-02 ppl_y2x=1.05 dual_loss=4.6627e-01
Validation X2Y - loss=1.1240e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0146e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90
Epoch 464 - |param|=1.07e+03 |g_param|=4.39e+04 loss_x2y=5.4245e-02 ppl_x2y=1.06 loss_y2x=4.8817e-02 ppl_y2x=1.05 dual_loss=4.0923e-01
Validation X2Y - loss=1.1441e+00 ppl=3.14 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0072e+00 ppl=2.74 best_loss=6.4204e-01 best_ppl=1.90
Epoch 465 - |param|=1.07e+03 |g_param|=4.99e+04 loss_x2y=5.5943e-02 ppl_x2y=1.06 loss_y2x=4.5342e-02 ppl_y2x=1.05 dual_loss=3.9715e-01
Validation X2Y - loss=1.1552e+00 ppl=3.17 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0129e+00 ppl=2.75 best_loss=6.4204e-01 best_ppl=1.90
Epoch 466 - |param|=1.07e+03 |g_param|=3.79e+04 loss_x2y=8.3401e-02 ppl_x2y=1.09 loss_y2x=4.8344e-02 ppl_y2x=1.05 dual_loss=4.1393e-01
Validation X2Y - loss=1.1795e+00 ppl=3.25 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0224e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 467 - |param|=1.07e+03 |g_param|=3.32e+04 loss_x2y=7.4868e-02 ppl_x2y=1.08 loss_y2x=4.8329e-02 ppl_y2x=1.05 dual_loss=3.6210e-01
Validation X2Y - loss=1.1605e+00 ppl=3.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0258e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 468 - |param|=1.07e+03 |g_param|=3.49e+04 loss_x2y=6.2142e-02 ppl_x2y=1.06 loss_y2x=5.1747e-02 ppl_y2x=1.05 dual_loss=4.4639e-01
Validation X2Y - loss=1.1426e+00 ppl=3.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0281e+00 ppl=2.80 best_loss=6.4204e-01 best_ppl=1.90
Epoch 469 - |param|=1.07e+03 |g_param|=4.10e+04 loss_x2y=5.6794e-02 ppl_x2y=1.06 loss_y2x=5.4052e-02 ppl_y2x=1.06 dual_loss=4.7109e-01
Validation X2Y - loss=1.1305e+00 ppl=3.10 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0124e+00 ppl=2.75 best_loss=6.4204e-01 best_ppl=1.90
Epoch 470 - |param|=1.07e+03 |g_param|=2.53e+04 loss_x2y=5.3182e-02 ppl_x2y=1.05 loss_y2x=5.5754e-02 ppl_y2x=1.06 dual_loss=4.4226e-01
Validation X2Y - loss=1.1393e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0265e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 471 - |param|=1.07e+03 |g_param|=2.29e+04 loss_x2y=5.2134e-02 ppl_x2y=1.05 loss_y2x=5.8487e-02 ppl_y2x=1.06 dual_loss=4.4166e-01
Validation X2Y - loss=1.1176e+00 ppl=3.06 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0494e+00 ppl=2.86 best_loss=6.4204e-01 best_ppl=1.90
Epoch 472 - |param|=1.07e+03 |g_param|=2.35e+04 loss_x2y=5.3266e-02 ppl_x2y=1.05 loss_y2x=5.3891e-02 ppl_y2x=1.06 dual_loss=4.7878e-01
Validation X2Y - loss=1.1390e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0191e+00 ppl=2.77 best_loss=6.4204e-01 best_ppl=1.90
Epoch 473 - |param|=1.07e+03 |g_param|=2.52e+04 loss_x2y=4.9955e-02 ppl_x2y=1.05 loss_y2x=6.4478e-02 ppl_y2x=1.07 dual_loss=3.9899e-01
Validation X2Y - loss=1.1351e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0432e+00 ppl=2.84 best_loss=6.4204e-01 best_ppl=1.90
Epoch 474 - |param|=1.07e+03 |g_param|=2.28e+04 loss_x2y=4.9505e-02 ppl_x2y=1.05 loss_y2x=6.3945e-02 ppl_y2x=1.07 dual_loss=4.5476e-01
Validation X2Y - loss=1.1181e+00 ppl=3.06 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0427e+00 ppl=2.84 best_loss=6.4204e-01 best_ppl=1.90
Epoch 475 - |param|=1.07e+03 |g_param|=1.86e+04 loss_x2y=4.6572e-02 ppl_x2y=1.05 loss_y2x=5.4853e-02 ppl_y2x=1.06 dual_loss=4.0020e-01
Validation X2Y - loss=1.1159e+00 ppl=3.05 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0332e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 476 - |param|=1.07e+03 |g_param|=1.75e+04 loss_x2y=4.4876e-02 ppl_x2y=1.05 loss_y2x=5.0379e-02 ppl_y2x=1.05 dual_loss=3.6742e-01
Validation X2Y - loss=1.1252e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0612e+00 ppl=2.89 best_loss=6.4204e-01 best_ppl=1.90
Epoch 477 - |param|=1.07e+03 |g_param|=1.86e+04 loss_x2y=5.0826e-02 ppl_x2y=1.05 loss_y2x=5.2955e-02 ppl_y2x=1.05 dual_loss=4.1878e-01
Validation X2Y - loss=1.1253e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0344e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 478 - |param|=1.07e+03 |g_param|=1.63e+04 loss_x2y=4.7786e-02 ppl_x2y=1.05 loss_y2x=4.5864e-02 ppl_y2x=1.05 dual_loss=3.7090e-01
Validation X2Y - loss=1.1237e+00 ppl=3.08 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0392e+00 ppl=2.83 best_loss=6.4204e-01 best_ppl=1.90
Epoch 479 - |param|=1.07e+03 |g_param|=2.22e+04 loss_x2y=4.5550e-02 ppl_x2y=1.05 loss_y2x=5.7086e-02 ppl_y2x=1.06 dual_loss=3.8204e-01
Validation X2Y - loss=1.1357e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0287e+00 ppl=2.80 best_loss=6.4204e-01 best_ppl=1.90
Epoch 480 - |param|=1.07e+03 |g_param|=2.41e+04 loss_x2y=5.0381e-02 ppl_x2y=1.05 loss_y2x=6.4409e-02 ppl_y2x=1.07 dual_loss=4.5592e-01
Validation X2Y - loss=1.1402e+00 ppl=3.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0375e+00 ppl=2.82 best_loss=6.4204e-01 best_ppl=1.90
Epoch 481 - |param|=1.07e+03 |g_param|=2.08e+04 loss_x2y=4.8356e-02 ppl_x2y=1.05 loss_y2x=5.5173e-02 ppl_y2x=1.06 dual_loss=4.2656e-01
Validation X2Y - loss=1.1335e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0431e+00 ppl=2.84 best_loss=6.4204e-01 best_ppl=1.90
Epoch 482 - |param|=1.07e+03 |g_param|=1.71e+04 loss_x2y=4.6637e-02 ppl_x2y=1.05 loss_y2x=4.9848e-02 ppl_y2x=1.05 dual_loss=4.4268e-01
Validation X2Y - loss=1.1414e+00 ppl=3.13 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0343e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 483 - |param|=1.07e+03 |g_param|=2.97e+04 loss_x2y=5.0456e-02 ppl_x2y=1.05 loss_y2x=7.8268e-02 ppl_y2x=1.08 dual_loss=5.2910e-01
Validation X2Y - loss=1.1206e+00 ppl=3.07 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0356e+00 ppl=2.82 best_loss=6.4204e-01 best_ppl=1.90
Epoch 484 - |param|=1.07e+03 |g_param|=3.35e+04 loss_x2y=5.3716e-02 ppl_x2y=1.06 loss_y2x=8.1372e-02 ppl_y2x=1.08 dual_loss=5.9908e-01
Validation X2Y - loss=1.1392e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0376e+00 ppl=2.82 best_loss=6.4204e-01 best_ppl=1.90
Epoch 485 - |param|=1.07e+03 |g_param|=2.60e+04 loss_x2y=5.4592e-02 ppl_x2y=1.06 loss_y2x=6.4247e-02 ppl_y2x=1.07 dual_loss=4.9208e-01
Validation X2Y - loss=1.1269e+00 ppl=3.09 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0145e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90
Epoch 486 - |param|=1.07e+03 |g_param|=4.02e+04 loss_x2y=5.7370e-02 ppl_x2y=1.06 loss_y2x=5.2362e-02 ppl_y2x=1.05 dual_loss=4.0226e-01
Validation X2Y - loss=1.1337e+00 ppl=3.11 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0511e+00 ppl=2.86 best_loss=6.4204e-01 best_ppl=1.90
Epoch 487 - |param|=1.07e+03 |g_param|=3.75e+04 loss_x2y=6.1006e-02 ppl_x2y=1.06 loss_y2x=4.7380e-02 ppl_y2x=1.05 dual_loss=3.9794e-01
Validation X2Y - loss=1.1507e+00 ppl=3.16 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0215e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 488 - |param|=1.07e+03 |g_param|=3.42e+04 loss_x2y=5.7421e-02 ppl_x2y=1.06 loss_y2x=4.8873e-02 ppl_y2x=1.05 dual_loss=3.7988e-01
Validation X2Y - loss=1.1609e+00 ppl=3.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0169e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90
Epoch 489 - |param|=1.07e+03 |g_param|=3.14e+04 loss_x2y=5.6974e-02 ppl_x2y=1.06 loss_y2x=4.5220e-02 ppl_y2x=1.05 dual_loss=3.7100e-01
Validation X2Y - loss=1.1661e+00 ppl=3.21 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0214e+00 ppl=2.78 best_loss=6.4204e-01 best_ppl=1.90
Epoch 490 - |param|=1.07e+03 |g_param|=2.66e+04 loss_x2y=4.9819e-02 ppl_x2y=1.05 loss_y2x=4.3146e-02 ppl_y2x=1.04 dual_loss=3.6086e-01
Validation X2Y - loss=1.1709e+00 ppl=3.22 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0289e+00 ppl=2.80 best_loss=6.4204e-01 best_ppl=1.90
Epoch 491 - |param|=1.07e+03 |g_param|=3.27e+04 loss_x2y=4.6492e-02 ppl_x2y=1.05 loss_y2x=4.3230e-02 ppl_y2x=1.04 dual_loss=3.6846e-01
Validation X2Y - loss=1.1686e+00 ppl=3.22 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0303e+00 ppl=2.80 best_loss=6.4204e-01 best_ppl=1.90
Epoch 492 - |param|=1.07e+03 |g_param|=3.56e+04 loss_x2y=5.0052e-02 ppl_x2y=1.05 loss_y2x=4.4286e-02 ppl_y2x=1.05 dual_loss=4.5162e-01
Validation X2Y - loss=1.1585e+00 ppl=3.19 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0324e+00 ppl=2.81 best_loss=6.4204e-01 best_ppl=1.90
Epoch 493 - |param|=1.07e+03 |g_param|=3.00e+04 loss_x2y=4.8145e-02 ppl_x2y=1.05 loss_y2x=4.3047e-02 ppl_y2x=1.04 dual_loss=3.8466e-01
Validation X2Y - loss=1.1560e+00 ppl=3.18 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0276e+00 ppl=2.79 best_loss=6.4204e-01 best_ppl=1.90
Epoch 494 - |param|=1.07e+03 |g_param|=3.24e+04 loss_x2y=4.5425e-02 ppl_x2y=1.05 loss_y2x=4.0368e-02 ppl_y2x=1.04 dual_loss=4.0873e-01
Validation X2Y - loss=1.1573e+00 ppl=3.18 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0393e+00 ppl=2.83 best_loss=6.4204e-01 best_ppl=1.90
Epoch 495 - |param|=1.07e+03 |g_param|=3.06e+04 loss_x2y=4.6066e-02 ppl_x2y=1.05 loss_y2x=4.1240e-02 ppl_y2x=1.04 dual_loss=3.9052e-01
Validation X2Y - loss=1.1451e+00 ppl=3.14 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0370e+00 ppl=2.82 best_loss=6.4204e-01 best_ppl=1.90
Epoch 496 - |param|=1.07e+03 |g_param|=3.56e+04 loss_x2y=4.6903e-02 ppl_x2y=1.05 loss_y2x=4.1050e-02 ppl_y2x=1.04 dual_loss=3.8134e-01
Validation X2Y - loss=1.1389e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0313e+00 ppl=2.80 best_loss=6.4204e-01 best_ppl=1.90
Epoch 497 - |param|=1.07e+03 |g_param|=3.04e+04 loss_x2y=4.8298e-02 ppl_x2y=1.05 loss_y2x=4.4295e-02 ppl_y2x=1.05 dual_loss=4.9067e-01
Validation X2Y - loss=1.1469e+00 ppl=3.15 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0427e+00 ppl=2.84 best_loss=6.4204e-01 best_ppl=1.90
Epoch 498 - |param|=1.08e+03 |g_param|=3.24e+04 loss_x2y=4.3085e-02 ppl_x2y=1.04 loss_y2x=4.0810e-02 ppl_y2x=1.04 dual_loss=3.6598e-01
Validation X2Y - loss=1.1373e+00 ppl=3.12 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0438e+00 ppl=2.84 best_loss=6.4204e-01 best_ppl=1.90
Epoch 499 - |param|=1.08e+03 |g_param|=3.57e+04 loss_x2y=4.8041e-02 ppl_x2y=1.05 loss_y2x=4.5540e-02 ppl_y2x=1.05 dual_loss=4.0041e-01
Validation X2Y - loss=1.1558e+00 ppl=3.18 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0381e+00 ppl=2.82 best_loss=6.4204e-01 best_ppl=1.90
Epoch 500 - |param|=1.08e+03 |g_param|=3.61e+04 loss_x2y=4.2573e-02 ppl_x2y=1.04 loss_y2x=4.5759e-02 ppl_y2x=1.05 dual_loss=3.5481e-01
Validation X2Y - loss=1.1760e+00 ppl=3.24 best_loss=6.5415e-01 best_ppl=1.92                                            
Validation Y2X - loss=1.0166e+00 ppl=2.76 best_loss=6.4204e-01 best_ppl=1.90

real	212m19.351s
user	209m52.727s
sys	2m15.535s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-xy-seq2seq-500epoch-myrk.sh
/home/ye/exp/simple-nmt/model/dsl/seq2seq/myrk-500epoch
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.01.4.41-82.49.4.44-84.71.4.04-56.88.4.07-58.51.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.2/0.6/0.0/0.0 (BP=0.978, ratio=0.978, hyp_len=22662, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.01.4.41-82.49.4.44-84.71.4.04-56.88.4.07-58.51.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.7/0.7/0.0/0.0 (BP=0.982, ratio=0.982, hyp_len=23084, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.02.4.14-62.54.4.16-63.92.3.89-49.13.3.92-50.36.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.1/1.6/0.0/0.0 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.02.4.14-62.54.4.16-63.92.3.89-49.13.3.92-50.36.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.6/0.1/0.0/0.0 (BP=0.962, ratio=0.963, hyp_len=22643, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.03.4.03-56.47.4.06-58.20.3.80-44.64.3.82-45.82.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.5/1.8/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.03.4.03-56.47.4.06-58.20.3.80-44.64.3.82-45.82.pth, rkmy
BLEU = 0.25, 19.0/1.2/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=23112, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.04.3.93-51.03.3.96-52.26.3.68-39.84.3.73-41.67.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.0/1.9/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23219, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.04.3.93-51.03.3.96-52.26.3.68-39.84.3.73-41.67.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.8/3.6/0.1/0.0 (BP=0.982, ratio=0.982, hyp_len=23085, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.05.3.81-45.13.3.84-46.47.3.58-35.71.3.61-36.79.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.7/2.2/0.0/0.0 (BP=0.995, ratio=0.995, hyp_len=23041, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.05.3.81-45.13.3.84-46.47.3.58-35.71.3.61-36.79.pth, rkmy
BLEU = 0.96, 24.6/3.9/0.4/0.0 (BP=0.998, ratio=0.998, hyp_len=23454, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.06.3.71-40.69.3.71-40.92.3.51-33.55.3.51-33.31.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.6/3.4/0.1/0.0 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.06.3.71-40.69.3.71-40.92.3.51-33.55.3.51-33.31.pth, rkmy
BLEU = 0.66, 24.4/4.2/0.3/0.0 (BP=1.000, ratio=1.010, hyp_len=23749, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.07.3.62-37.43.3.55-34.77.3.40-30.08.3.30-27.03.pth, myrk
BLEU = 1.85, 28.0/5.7/0.9/0.1 (BP=0.996, ratio=0.996, hyp_len=23076, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.07.3.62-37.43.3.55-34.77.3.40-30.08.3.30-27.03.pth, rkmy
BLEU = 1.82, 29.2/7.4/0.9/0.1 (BP=1.000, ratio=1.011, hyp_len=23761, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.08.3.52-33.93.3.37-29.07.3.30-26.99.3.09-21.95.pth, myrk
BLEU = 1.89, 28.4/6.5/0.9/0.1 (BP=1.000, ratio=1.006, hyp_len=23305, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.08.3.52-33.93.3.37-29.07.3.30-26.99.3.09-21.95.pth, rkmy
BLEU = 3.06, 33.3/9.5/1.5/0.2 (BP=0.991, ratio=0.991, hyp_len=23302, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.09.3.33-28.03.3.02-20.46.3.09-21.99.2.75-15.72.pth, myrk
BLEU = 4.36, 31.6/9.1/2.3/0.5 (BP=1.000, ratio=1.006, hyp_len=23310, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.09.3.33-28.03.3.02-20.46.3.09-21.99.2.75-15.72.pth, rkmy
BLEU = 6.63, 38.5/14.2/3.8/0.9 (BP=1.000, ratio=1.006, hyp_len=23649, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.100.0.24-1.27.0.27-1.32.0.69-2.00.0.66-1.94.pth, myrk
BLEU = 74.46, 87.5/78.2/70.4/63.8 (BP=1.000, ratio=1.027, hyp_len=23792, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.100.0.24-1.27.0.27-1.32.0.69-2.00.0.66-1.94.pth, rkmy
BLEU = 74.65, 87.6/78.6/70.4/64.0 (BP=1.000, ratio=1.031, hyp_len=24249, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.101.0.23-1.26.0.28-1.33.0.69-1.99.0.69-1.99.pth, myrk
BLEU = 74.75, 87.6/78.4/70.8/64.2 (BP=1.000, ratio=1.030, hyp_len=23849, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.101.0.23-1.26.0.28-1.33.0.69-1.99.0.69-1.99.pth, rkmy
BLEU = 74.00, 87.3/78.0/69.7/63.2 (BP=1.000, ratio=1.039, hyp_len=24418, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.102.0.22-1.25.0.27-1.31.0.69-1.99.0.67-1.96.pth, myrk
BLEU = 74.15, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.102.0.22-1.25.0.27-1.31.0.69-1.99.0.67-1.96.pth, rkmy
BLEU = 73.02, 86.6/77.2/68.6/62.0 (BP=1.000, ratio=1.045, hyp_len=24558, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.103.0.23-1.26.0.26-1.30.0.69-1.99.0.67-1.95.pth, myrk
BLEU = 73.53, 86.9/77.5/69.4/62.6 (BP=1.000, ratio=1.036, hyp_len=23998, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.103.0.23-1.26.0.26-1.30.0.69-1.99.0.67-1.95.pth, rkmy
BLEU = 74.02, 87.2/78.0/69.7/63.3 (BP=1.000, ratio=1.041, hyp_len=24463, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.10.3.15-23.44.2.78-16.12.2.97-19.51.2.56-12.96.pth, myrk
BLEU = 6.15, 35.1/11.3/3.5/1.1 (BP=0.983, ratio=0.983, hyp_len=22760, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.10.3.15-23.44.2.78-16.12.2.97-19.51.2.56-12.96.pth, rkmy
BLEU = 10.26, 42.2/18.1/6.2/2.3 (BP=1.000, ratio=1.016, hyp_len=23882, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.104.0.22-1.25.0.26-1.30.0.69-1.99.0.68-1.97.pth, myrk
BLEU = 74.62, 87.7/78.4/70.6/63.9 (BP=1.000, ratio=1.030, hyp_len=23858, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.104.0.22-1.25.0.26-1.30.0.69-1.99.0.68-1.97.pth, rkmy
BLEU = 74.25, 87.3/78.2/70.0/63.6 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.105.0.23-1.26.0.26-1.30.0.68-1.98.0.68-1.98.pth, myrk
BLEU = 74.42, 87.4/78.2/70.4/63.8 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.105.0.23-1.26.0.26-1.30.0.68-1.98.0.68-1.98.pth, rkmy
BLEU = 74.51, 87.5/78.4/70.2/64.0 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.106.0.22-1.25.0.26-1.29.0.71-2.03.0.68-1.97.pth, myrk
BLEU = 74.24, 87.3/78.0/70.2/63.6 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.106.0.22-1.25.0.26-1.29.0.71-2.03.0.68-1.97.pth, rkmy
BLEU = 73.64, 87.0/77.7/69.3/62.8 (BP=1.000, ratio=1.042, hyp_len=24491, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.107.0.22-1.24.0.25-1.28.0.69-1.99.0.68-1.97.pth, myrk
BLEU = 75.59, 88.1/79.1/71.7/65.3 (BP=1.000, ratio=1.027, hyp_len=23784, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.107.0.22-1.24.0.25-1.28.0.69-1.99.0.68-1.97.pth, rkmy
BLEU = 74.96, 87.9/78.8/70.8/64.5 (BP=1.000, ratio=1.034, hyp_len=24314, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.108.0.22-1.24.0.26-1.29.0.70-2.01.0.66-1.94.pth, myrk
BLEU = 73.10, 86.4/76.9/69.0/62.3 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.108.0.22-1.24.0.26-1.29.0.70-2.01.0.66-1.94.pth, rkmy
BLEU = 73.52, 87.0/77.6/69.1/62.6 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.109.0.22-1.25.0.29-1.34.0.71-2.02.0.70-2.01.pth, myrk
BLEU = 73.92, 87.3/77.8/69.8/63.0 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.109.0.22-1.25.0.29-1.34.0.71-2.02.0.70-2.01.pth, rkmy
BLEU = 72.86, 86.6/77.2/68.5/61.5 (BP=1.000, ratio=1.042, hyp_len=24494, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.110.0.21-1.24.0.27-1.31.0.71-2.03.0.66-1.94.pth, myrk
BLEU = 74.53, 87.4/78.2/70.5/64.0 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.110.0.21-1.24.0.27-1.31.0.71-2.03.0.66-1.94.pth, rkmy
BLEU = 73.72, 87.1/77.8/69.4/62.8 (BP=1.000, ratio=1.037, hyp_len=24376, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.111.0.21-1.24.0.27-1.31.0.71-2.03.0.67-1.95.pth, myrk
BLEU = 73.91, 87.1/77.6/69.8/63.2 (BP=1.000, ratio=1.029, hyp_len=23823, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.111.0.21-1.24.0.27-1.31.0.71-2.03.0.67-1.95.pth, rkmy
BLEU = 74.07, 87.3/78.1/69.8/63.3 (BP=1.000, ratio=1.036, hyp_len=24365, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.112.0.21-1.23.0.26-1.30.0.69-2.00.0.65-1.92.pth, myrk
BLEU = 74.58, 87.7/78.3/70.5/63.9 (BP=1.000, ratio=1.028, hyp_len=23804, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.112.0.21-1.23.0.26-1.30.0.69-2.00.0.65-1.92.pth, rkmy
BLEU = 73.39, 86.8/77.3/69.0/62.6 (BP=1.000, ratio=1.043, hyp_len=24513, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.11.2.91-18.37.2.49-12.05.2.75-15.71.2.34-10.41.pth, myrk
BLEU = 8.17, 38.7/14.0/4.9/1.7 (BP=1.000, ratio=1.013, hyp_len=23462, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.11.2.91-18.37.2.49-12.05.2.75-15.71.2.34-10.41.pth, rkmy
BLEU = 12.58, 45.6/20.8/8.3/3.2 (BP=1.000, ratio=1.012, hyp_len=23781, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.113.0.21-1.24.0.25-1.28.0.70-2.02.0.66-1.94.pth, myrk
BLEU = 74.72, 87.6/78.4/70.7/64.2 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.113.0.21-1.24.0.25-1.28.0.70-2.02.0.66-1.94.pth, rkmy
BLEU = 74.08, 87.3/78.0/69.8/63.4 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.114.0.24-1.27.0.25-1.29.0.70-2.02.0.67-1.95.pth, myrk
BLEU = 73.56, 86.9/77.4/69.5/62.7 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.114.0.24-1.27.0.25-1.29.0.70-2.02.0.67-1.95.pth, rkmy
BLEU = 72.86, 86.4/76.9/68.5/62.0 (BP=1.000, ratio=1.045, hyp_len=24578, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.115.0.24-1.28.0.24-1.28.0.72-2.05.0.67-1.95.pth, myrk
BLEU = 73.72, 87.0/77.5/69.6/62.9 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.115.0.24-1.28.0.24-1.28.0.72-2.05.0.67-1.95.pth, rkmy
BLEU = 73.77, 87.1/77.7/69.5/63.0 (BP=1.000, ratio=1.040, hyp_len=24443, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.116.0.23-1.26.0.24-1.27.0.71-2.04.0.65-1.92.pth, myrk
BLEU = 74.67, 87.6/78.3/70.7/64.1 (BP=1.000, ratio=1.029, hyp_len=23827, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.116.0.23-1.26.0.24-1.27.0.71-2.04.0.65-1.92.pth, rkmy
BLEU = 74.18, 87.4/78.2/69.8/63.5 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.117.0.22-1.25.0.23-1.26.0.73-2.08.0.66-1.93.pth, myrk
BLEU = 73.50, 87.1/77.3/69.4/62.5 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.117.0.22-1.25.0.23-1.26.0.73-2.08.0.66-1.93.pth, rkmy
BLEU = 74.13, 87.2/78.1/69.9/63.4 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.118.0.22-1.25.0.24-1.27.0.70-2.02.0.66-1.94.pth, myrk
BLEU = 73.72, 87.0/77.5/69.6/62.9 (BP=1.000, ratio=1.035, hyp_len=23968, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.118.0.22-1.25.0.24-1.27.0.70-2.02.0.66-1.94.pth, rkmy
BLEU = 73.16, 86.7/77.3/68.8/62.2 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.119.0.20-1.23.0.24-1.27.0.70-2.02.0.67-1.96.pth, myrk
BLEU = 74.60, 87.5/78.3/70.6/64.0 (BP=1.000, ratio=1.029, hyp_len=23827, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.119.0.20-1.23.0.24-1.27.0.70-2.02.0.67-1.96.pth, rkmy
BLEU = 73.50, 86.9/77.6/69.1/62.6 (BP=1.000, ratio=1.043, hyp_len=24513, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.120.0.19-1.21.0.23-1.25.0.71-2.03.0.68-1.97.pth, myrk
BLEU = 74.89, 87.9/78.6/70.8/64.3 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.120.0.19-1.21.0.23-1.25.0.71-2.03.0.68-1.97.pth, rkmy
BLEU = 73.95, 87.3/78.0/69.7/63.1 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.121.0.19-1.21.0.23-1.26.0.72-2.05.0.67-1.95.pth, myrk
BLEU = 74.32, 87.4/78.0/70.3/63.7 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.121.0.19-1.21.0.23-1.26.0.72-2.05.0.67-1.95.pth, rkmy
BLEU = 74.26, 87.4/78.2/70.0/63.6 (BP=1.000, ratio=1.038, hyp_len=24395, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.122.0.20-1.22.0.30-1.35.0.71-2.04.0.72-2.06.pth, myrk
BLEU = 74.21, 87.4/78.0/70.1/63.4 (BP=1.000, ratio=1.035, hyp_len=23979, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.122.0.20-1.22.0.30-1.35.0.71-2.04.0.72-2.06.pth, rkmy
BLEU = 72.25, 86.2/76.4/67.8/61.0 (BP=1.000, ratio=1.043, hyp_len=24510, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.12.2.78-16.09.2.41-11.18.2.77-15.89.2.19-8.93.pth, myrk
BLEU = 7.60, 35.9/14.1/4.6/1.5 (BP=0.993, ratio=0.993, hyp_len=23005, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.12.2.78-16.09.2.41-11.18.2.77-15.89.2.19-8.93.pth, rkmy
BLEU = 15.56, 49.6/24.2/10.7/4.8 (BP=0.989, ratio=0.989, hyp_len=23243, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.123.0.20-1.22.0.28-1.33.0.73-2.07.0.72-2.05.pth, myrk
BLEU = 74.29, 87.7/78.1/70.2/63.4 (BP=1.000, ratio=1.025, hyp_len=23740, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.123.0.20-1.22.0.28-1.33.0.73-2.07.0.72-2.05.pth, rkmy
BLEU = 73.25, 86.9/77.3/68.9/62.2 (BP=1.000, ratio=1.043, hyp_len=24511, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.124.0.39-1.48.0.27-1.31.0.91-2.49.0.68-1.97.pth, myrk
BLEU = 67.70, 84.6/72.6/62.7/54.5 (BP=1.000, ratio=1.011, hyp_len=23413, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.124.0.39-1.48.0.27-1.31.0.91-2.49.0.68-1.97.pth, rkmy
BLEU = 73.96, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.040, hyp_len=24438, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.125.0.33-1.39.0.24-1.27.0.76-2.14.0.68-1.97.pth, myrk
BLEU = 71.25, 86.1/75.6/66.8/59.3 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.125.0.33-1.39.0.24-1.27.0.76-2.14.0.68-1.97.pth, rkmy
BLEU = 73.92, 87.2/77.9/69.6/63.1 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.126.0.30-1.35.0.25-1.28.0.70-2.02.0.66-1.94.pth, myrk
BLEU = 73.45, 87.0/77.4/69.3/62.4 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.126.0.30-1.35.0.25-1.28.0.70-2.02.0.66-1.94.pth, rkmy
BLEU = 72.70, 86.5/76.8/68.2/61.7 (BP=1.000, ratio=1.043, hyp_len=24528, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.127.0.24-1.28.0.27-1.31.0.71-2.03.0.67-1.95.pth, myrk
BLEU = 73.57, 87.0/77.5/69.5/62.5 (BP=1.000, ratio=1.034, hyp_len=23938, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.127.0.24-1.28.0.27-1.31.0.71-2.03.0.67-1.95.pth, rkmy
BLEU = 74.00, 87.2/78.0/69.7/63.3 (BP=1.000, ratio=1.039, hyp_len=24425, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.128.0.24-1.27.0.28-1.33.0.72-2.05.0.67-1.95.pth, myrk
BLEU = 73.48, 86.9/77.3/69.4/62.5 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.128.0.24-1.27.0.28-1.33.0.72-2.05.0.67-1.95.pth, rkmy
BLEU = 73.97, 87.1/77.9/69.6/63.3 (BP=1.000, ratio=1.037, hyp_len=24374, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.129.0.20-1.23.0.23-1.26.0.72-2.05.0.66-1.94.pth, myrk
BLEU = 73.93, 87.2/77.8/69.9/63.1 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.129.0.20-1.23.0.23-1.26.0.72-2.05.0.66-1.94.pth, rkmy
BLEU = 73.77, 87.0/77.7/69.5/63.0 (BP=1.000, ratio=1.041, hyp_len=24472, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.130.0.20-1.22.0.22-1.24.0.72-2.05.0.66-1.93.pth, myrk
BLEU = 74.13, 87.5/78.0/70.0/63.2 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.130.0.20-1.22.0.22-1.24.0.72-2.05.0.66-1.93.pth, rkmy
BLEU = 73.26, 86.8/77.3/68.9/62.4 (BP=1.000, ratio=1.042, hyp_len=24506, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.131.0.19-1.21.0.23-1.26.0.72-2.05.0.67-1.95.pth, myrk
BLEU = 74.17, 87.4/77.9/70.0/63.4 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.131.0.19-1.21.0.23-1.26.0.72-2.05.0.67-1.95.pth, rkmy
BLEU = 73.80, 87.3/78.0/69.4/62.8 (BP=1.000, ratio=1.041, hyp_len=24471, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.132.0.19-1.21.0.22-1.25.0.72-2.05.0.68-1.97.pth, myrk
BLEU = 73.89, 87.1/77.7/69.8/63.1 (BP=1.000, ratio=1.035, hyp_len=23978, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.132.0.19-1.21.0.22-1.25.0.72-2.05.0.68-1.97.pth, rkmy
BLEU = 73.37, 86.9/77.4/69.0/62.4 (BP=1.000, ratio=1.041, hyp_len=24473, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.13.2.61-13.57.2.21-9.13.2.40-11.05.2.03-7.58.pth, myrk
BLEU = 13.95, 45.7/21.2/9.4/4.1 (BP=1.000, ratio=1.012, hyp_len=23446, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.13.2.61-13.57.2.21-9.13.2.40-11.05.2.03-7.58.pth, rkmy
BLEU = 21.42, 54.7/30.3/15.9/8.1 (BP=0.998, ratio=0.998, hyp_len=23453, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.133.0.23-1.26.0.43-1.54.0.73-2.07.0.68-1.98.pth, myrk
BLEU = 74.38, 87.4/78.1/70.4/63.8 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.133.0.23-1.26.0.43-1.54.0.73-2.07.0.68-1.98.pth, rkmy
BLEU = 71.67, 85.8/76.0/67.2/60.2 (BP=1.000, ratio=1.047, hyp_len=24604, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.134.0.17-1.19.0.23-1.26.0.73-2.08.0.66-1.94.pth, myrk
BLEU = 74.84, 87.7/78.5/70.8/64.3 (BP=1.000, ratio=1.032, hyp_len=23903, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.134.0.17-1.19.0.23-1.26.0.73-2.08.0.66-1.94.pth, rkmy
BLEU = 73.67, 87.1/77.7/69.3/62.8 (BP=1.000, ratio=1.042, hyp_len=24496, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.135.0.17-1.19.0.22-1.25.0.74-2.09.0.66-1.94.pth, myrk
BLEU = 74.65, 87.6/78.3/70.6/64.1 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.135.0.17-1.19.0.22-1.25.0.74-2.09.0.66-1.94.pth, rkmy
BLEU = 73.67, 87.0/77.6/69.3/62.9 (BP=1.000, ratio=1.044, hyp_len=24537, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.136.0.17-1.18.0.21-1.23.0.73-2.07.0.65-1.91.pth, myrk
BLEU = 74.60, 87.5/78.3/70.6/64.0 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.136.0.17-1.18.0.21-1.23.0.73-2.07.0.65-1.91.pth, rkmy
BLEU = 73.24, 86.8/77.3/68.8/62.3 (BP=1.000, ratio=1.045, hyp_len=24578, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.137.0.17-1.18.0.21-1.23.0.73-2.08.0.66-1.93.pth, myrk
BLEU = 75.01, 87.8/78.6/71.0/64.6 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.137.0.17-1.18.0.21-1.23.0.73-2.08.0.66-1.93.pth, rkmy
BLEU = 73.61, 87.0/77.6/69.2/62.8 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.138.0.17-1.18.0.19-1.21.0.73-2.07.0.65-1.92.pth, myrk
BLEU = 74.34, 87.4/78.1/70.3/63.6 (BP=1.000, ratio=1.030, hyp_len=23862, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.138.0.17-1.18.0.19-1.21.0.73-2.07.0.65-1.92.pth, rkmy
BLEU = 73.37, 86.8/77.4/69.0/62.5 (BP=1.000, ratio=1.046, hyp_len=24588, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.139.0.17-1.18.0.19-1.21.0.74-2.09.0.67-1.95.pth, myrk
BLEU = 74.52, 87.5/78.3/70.5/63.8 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.139.0.17-1.18.0.19-1.21.0.74-2.09.0.67-1.95.pth, rkmy
BLEU = 73.57, 87.0/77.6/69.3/62.7 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.140.0.16-1.18.0.19-1.20.0.74-2.10.0.66-1.93.pth, myrk
BLEU = 74.18, 87.3/78.0/70.1/63.4 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.140.0.16-1.18.0.19-1.20.0.74-2.10.0.66-1.93.pth, rkmy
BLEU = 74.19, 87.3/78.2/69.9/63.5 (BP=1.000, ratio=1.041, hyp_len=24465, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.141.0.16-1.18.0.19-1.21.0.74-2.10.0.67-1.95.pth, myrk
BLEU = 74.76, 87.9/78.5/70.7/64.1 (BP=1.000, ratio=1.028, hyp_len=23805, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.141.0.16-1.18.0.19-1.21.0.74-2.10.0.67-1.95.pth, rkmy
BLEU = 73.70, 87.1/77.8/69.4/62.7 (BP=1.000, ratio=1.041, hyp_len=24479, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.142.0.15-1.17.0.18-1.20.0.74-2.11.0.66-1.94.pth, myrk
BLEU = 74.30, 87.5/78.0/70.2/63.6 (BP=1.000, ratio=1.035, hyp_len=23966, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.142.0.15-1.17.0.18-1.20.0.74-2.11.0.66-1.94.pth, rkmy
BLEU = 74.07, 87.2/78.0/69.7/63.4 (BP=1.000, ratio=1.042, hyp_len=24507, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.14.2.40-10.99.2.16-8.64.2.25-9.52.2.07-7.89.pth, myrk
BLEU = 17.58, 50.3/25.6/12.5/5.9 (BP=1.000, ratio=1.005, hyp_len=23269, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.14.2.40-10.99.2.16-8.64.2.25-9.52.2.07-7.89.pth, rkmy
BLEU = 19.12, 53.2/28.1/13.6/6.6 (BP=1.000, ratio=1.001, hyp_len=23538, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.143.0.16-1.17.0.18-1.20.0.75-2.12.0.68-1.98.pth, myrk
BLEU = 73.83, 87.0/77.6/69.8/63.1 (BP=1.000, ratio=1.036, hyp_len=23998, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.143.0.16-1.17.0.18-1.20.0.75-2.12.0.68-1.98.pth, rkmy
BLEU = 74.38, 87.5/78.3/70.1/63.7 (BP=1.000, ratio=1.038, hyp_len=24399, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.144.0.17-1.18.0.19-1.21.0.76-2.14.0.67-1.96.pth, myrk
BLEU = 73.68, 87.2/77.6/69.5/62.7 (BP=1.000, ratio=1.037, hyp_len=24006, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.144.0.17-1.18.0.19-1.21.0.76-2.14.0.67-1.96.pth, rkmy
BLEU = 73.51, 87.0/77.5/69.1/62.7 (BP=1.000, ratio=1.046, hyp_len=24591, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.145.0.16-1.17.0.18-1.19.0.75-2.13.0.68-1.98.pth, myrk
BLEU = 74.69, 87.7/78.3/70.7/64.1 (BP=1.000, ratio=1.030, hyp_len=23858, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.145.0.16-1.17.0.18-1.19.0.75-2.13.0.68-1.98.pth, rkmy
BLEU = 73.38, 86.8/77.4/69.0/62.5 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.146.0.16-1.17.0.18-1.20.0.76-2.13.0.68-1.97.pth, myrk
BLEU = 74.23, 87.2/78.0/70.2/63.6 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.146.0.16-1.17.0.18-1.20.0.76-2.13.0.68-1.97.pth, rkmy
BLEU = 73.75, 87.2/77.8/69.4/62.9 (BP=1.000, ratio=1.042, hyp_len=24493, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.147.0.16-1.17.0.18-1.20.0.76-2.13.0.70-2.01.pth, myrk
BLEU = 74.80, 87.6/78.5/70.8/64.2 (BP=1.000, ratio=1.029, hyp_len=23832, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.147.0.16-1.17.0.18-1.20.0.76-2.13.0.70-2.01.pth, rkmy
BLEU = 73.84, 87.3/77.8/69.5/63.0 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.148.0.15-1.17.0.18-1.19.0.77-2.15.0.71-2.03.pth, myrk
BLEU = 74.86, 87.7/78.5/70.8/64.4 (BP=1.000, ratio=1.032, hyp_len=23890, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.148.0.15-1.17.0.18-1.19.0.77-2.15.0.71-2.03.pth, rkmy
BLEU = 73.00, 86.7/77.1/68.6/61.9 (BP=1.000, ratio=1.046, hyp_len=24597, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.149.0.15-1.16.0.19-1.21.0.76-2.13.0.69-1.99.pth, myrk
BLEU = 73.68, 87.0/77.5/69.5/62.8 (BP=1.000, ratio=1.036, hyp_len=23993, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.149.0.15-1.16.0.19-1.21.0.76-2.13.0.69-1.99.pth, rkmy
BLEU = 73.91, 87.2/77.9/69.6/63.2 (BP=1.000, ratio=1.041, hyp_len=24471, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.150.0.16-1.18.0.18-1.19.0.74-2.10.0.70-2.01.pth, myrk
BLEU = 73.71, 87.1/77.6/69.6/62.8 (BP=1.000, ratio=1.036, hyp_len=23989, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.150.0.16-1.18.0.18-1.19.0.74-2.10.0.70-2.01.pth, rkmy
BLEU = 74.01, 87.2/78.0/69.7/63.3 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.151.0.16-1.18.0.18-1.20.0.75-2.13.0.69-2.00.pth, myrk
BLEU = 74.16, 87.6/78.0/70.0/63.2 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.151.0.16-1.18.0.18-1.20.0.75-2.13.0.69-2.00.pth, rkmy
BLEU = 73.66, 86.9/77.6/69.4/62.9 (BP=1.000, ratio=1.042, hyp_len=24508, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.152.0.15-1.17.0.17-1.19.0.77-2.17.0.70-2.02.pth, myrk
BLEU = 74.08, 87.5/78.0/69.9/63.2 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.152.0.15-1.17.0.17-1.19.0.77-2.17.0.70-2.02.pth, rkmy
BLEU = 73.94, 87.2/77.9/69.6/63.1 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.15.2.12-8.33.1.84-6.30.2.06-7.88.1.81-6.11.pth, myrk
BLEU = 21.88, 54.2/29.9/16.2/8.7 (BP=1.000, ratio=1.019, hyp_len=23592, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.15.2.12-8.33.1.84-6.30.2.06-7.88.1.81-6.11.pth, rkmy
BLEU = 28.92, 61.2/37.7/22.7/13.6 (BP=0.996, ratio=0.996, hyp_len=23416, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.153.0.16-1.17.0.19-1.21.0.77-2.15.0.69-2.00.pth, myrk
BLEU = 73.42, 86.7/77.2/69.3/62.6 (BP=1.000, ratio=1.037, hyp_len=24027, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.153.0.16-1.17.0.19-1.21.0.77-2.15.0.69-2.00.pth, rkmy
BLEU = 73.48, 87.0/77.5/69.1/62.6 (BP=1.000, ratio=1.044, hyp_len=24541, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.154.0.16-1.17.0.19-1.21.0.77-2.15.0.69-2.00.pth, myrk
BLEU = 74.51, 87.7/78.3/70.4/63.8 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.154.0.16-1.17.0.19-1.21.0.77-2.15.0.69-2.00.pth, rkmy
BLEU = 72.57, 86.5/76.8/68.1/61.3 (BP=1.000, ratio=1.050, hyp_len=24678, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.155.0.15-1.16.0.18-1.19.0.77-2.16.0.68-1.98.pth, myrk
BLEU = 74.29, 87.5/78.1/70.2/63.5 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.155.0.15-1.16.0.18-1.19.0.77-2.16.0.68-1.98.pth, rkmy
BLEU = 74.18, 87.5/78.2/69.9/63.4 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.156.0.17-1.18.0.18-1.20.0.78-2.17.0.68-1.97.pth, myrk
BLEU = 72.91, 86.7/76.9/68.7/61.7 (BP=1.000, ratio=1.040, hyp_len=24075, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.156.0.17-1.18.0.18-1.20.0.78-2.17.0.68-1.97.pth, rkmy
BLEU = 73.66, 87.1/77.7/69.3/62.8 (BP=1.000, ratio=1.042, hyp_len=24501, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.157.0.16-1.18.0.18-1.19.0.78-2.19.0.69-1.98.pth, myrk
BLEU = 73.89, 87.4/77.7/69.7/63.0 (BP=1.000, ratio=1.033, hyp_len=23923, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.157.0.16-1.18.0.18-1.19.0.78-2.19.0.69-1.98.pth, rkmy
BLEU = 73.11, 86.7/77.2/68.7/62.1 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.158.0.16-1.18.0.18-1.19.0.77-2.16.0.70-2.02.pth, myrk
BLEU = 73.49, 87.0/77.4/69.4/62.5 (BP=1.000, ratio=1.037, hyp_len=24008, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.158.0.16-1.18.0.18-1.19.0.77-2.16.0.70-2.02.pth, rkmy
BLEU = 73.75, 87.0/77.7/69.5/63.0 (BP=1.000, ratio=1.042, hyp_len=24491, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.159.0.16-1.17.0.17-1.18.0.78-2.18.0.71-2.03.pth, myrk
BLEU = 73.67, 87.1/77.5/69.5/62.7 (BP=1.000, ratio=1.035, hyp_len=23965, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.159.0.16-1.17.0.17-1.18.0.78-2.18.0.71-2.03.pth, rkmy
BLEU = 74.23, 87.4/78.2/69.9/63.6 (BP=1.000, ratio=1.039, hyp_len=24434, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.160.0.16-1.18.0.17-1.18.0.78-2.19.0.70-2.01.pth, myrk
BLEU = 74.05, 87.3/77.9/70.0/63.2 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.160.0.16-1.18.0.17-1.18.0.78-2.19.0.70-2.01.pth, rkmy
BLEU = 73.24, 86.9/77.3/68.8/62.3 (BP=1.000, ratio=1.044, hyp_len=24546, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.161.0.16-1.17.0.18-1.20.0.78-2.17.0.70-2.02.pth, myrk
BLEU = 73.48, 87.0/77.4/69.3/62.5 (BP=1.000, ratio=1.036, hyp_len=23990, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.161.0.16-1.17.0.18-1.20.0.78-2.17.0.70-2.02.pth, rkmy
BLEU = 73.85, 87.2/77.7/69.5/63.2 (BP=1.000, ratio=1.040, hyp_len=24450, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.162.0.14-1.15.0.17-1.18.0.76-2.15.0.72-2.05.pth, myrk
BLEU = 74.48, 87.6/78.3/70.4/63.7 (BP=1.000, ratio=1.030, hyp_len=23861, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.162.0.14-1.15.0.17-1.18.0.76-2.15.0.72-2.05.pth, rkmy
BLEU = 73.60, 87.0/77.6/69.3/62.7 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.16.2.15-8.56.1.80-6.04.2.00-7.42.1.73-5.64.pth, myrk
BLEU = 22.95, 55.5/31.2/17.2/9.3 (BP=1.000, ratio=1.004, hyp_len=23252, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.16.2.15-8.56.1.80-6.04.2.00-7.42.1.73-5.64.pth, rkmy
BLEU = 32.63, 63.4/41.2/26.1/16.7 (BP=1.000, ratio=1.002, hyp_len=23550, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.163.0.14-1.15.0.16-1.18.0.77-2.15.0.70-2.02.pth, myrk
BLEU = 74.38, 87.8/78.2/70.2/63.5 (BP=1.000, ratio=1.030, hyp_len=23848, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.163.0.14-1.15.0.16-1.18.0.77-2.15.0.70-2.02.pth, rkmy
BLEU = 73.57, 87.0/77.5/69.2/62.7 (BP=1.000, ratio=1.044, hyp_len=24535, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.164.0.14-1.15.0.17-1.19.0.77-2.17.0.73-2.07.pth, myrk
BLEU = 74.04, 87.3/77.9/69.9/63.2 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.164.0.14-1.15.0.17-1.19.0.77-2.17.0.73-2.07.pth, rkmy
BLEU = 74.49, 87.5/78.4/70.3/63.8 (BP=1.000, ratio=1.034, hyp_len=24307, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.165.0.14-1.16.0.17-1.19.0.81-2.24.0.72-2.05.pth, myrk
BLEU = 73.55, 87.1/77.5/69.4/62.5 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.165.0.14-1.16.0.17-1.19.0.81-2.24.0.72-2.05.pth, rkmy
BLEU = 73.96, 87.1/77.9/69.7/63.2 (BP=1.000, ratio=1.039, hyp_len=24434, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.166.0.14-1.15.0.19-1.21.0.77-2.16.0.70-2.02.pth, myrk
BLEU = 74.49, 87.4/78.2/70.4/64.0 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.166.0.14-1.15.0.19-1.21.0.77-2.16.0.70-2.02.pth, rkmy
BLEU = 73.51, 86.9/77.5/69.2/62.6 (BP=1.000, ratio=1.036, hyp_len=24349, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.167.0.13-1.14.0.17-1.19.0.79-2.19.0.70-2.01.pth, myrk
BLEU = 74.34, 87.4/78.0/70.3/63.8 (BP=1.000, ratio=1.032, hyp_len=23890, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.167.0.13-1.14.0.17-1.19.0.79-2.19.0.70-2.01.pth, rkmy
BLEU = 73.42, 86.9/77.6/69.1/62.4 (BP=1.000, ratio=1.043, hyp_len=24511, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.168.0.13-1.14.0.18-1.19.0.79-2.20.0.70-2.01.pth, myrk
BLEU = 73.77, 87.1/77.6/69.6/62.9 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.168.0.13-1.14.0.18-1.19.0.79-2.20.0.70-2.01.pth, rkmy
BLEU = 73.57, 86.9/77.6/69.3/62.7 (BP=1.000, ratio=1.042, hyp_len=24494, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.169.0.13-1.14.0.17-1.19.0.79-2.20.0.73-2.07.pth, myrk
BLEU = 74.55, 87.7/78.3/70.4/63.8 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.169.0.13-1.14.0.17-1.19.0.79-2.20.0.73-2.07.pth, rkmy
BLEU = 73.54, 86.8/77.5/69.2/62.8 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.170.0.14-1.15.0.16-1.17.0.80-2.22.0.71-2.04.pth, myrk
BLEU = 73.20, 86.9/77.1/69.0/62.0 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.170.0.14-1.15.0.16-1.17.0.80-2.22.0.71-2.04.pth, rkmy
BLEU = 73.65, 87.0/77.7/69.3/62.8 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.171.0.15-1.16.0.16-1.17.0.80-2.23.0.70-2.02.pth, myrk
BLEU = 73.61, 87.2/77.5/69.4/62.5 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.171.0.15-1.16.0.16-1.17.0.80-2.23.0.70-2.02.pth, rkmy
BLEU = 73.62, 87.0/77.5/69.3/62.9 (BP=1.000, ratio=1.042, hyp_len=24495, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.17.1.86-6.39.1.63-5.12.1.82-6.17.1.58-4.87.pth, myrk
BLEU = 29.71, 60.4/38.0/23.5/14.4 (BP=1.000, ratio=1.015, hyp_len=23504, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.17.1.86-6.39.1.63-5.12.1.82-6.17.1.58-4.87.pth, rkmy
BLEU = 35.68, 66.2/44.3/28.9/19.1 (BP=1.000, ratio=1.007, hyp_len=23669, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.172.0.15-1.16.0.16-1.17.0.80-2.22.0.71-2.04.pth, myrk
BLEU = 73.95, 87.4/77.8/69.8/63.0 (BP=1.000, ratio=1.035, hyp_len=23960, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.172.0.15-1.16.0.16-1.17.0.80-2.22.0.71-2.04.pth, rkmy
BLEU = 73.00, 86.7/77.1/68.6/61.9 (BP=1.000, ratio=1.045, hyp_len=24576, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.173.0.14-1.15.0.15-1.16.0.82-2.27.0.71-2.04.pth, myrk
BLEU = 73.41, 87.1/77.4/69.3/62.2 (BP=1.000, ratio=1.038, hyp_len=24033, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.173.0.14-1.15.0.15-1.16.0.82-2.27.0.71-2.04.pth, rkmy
BLEU = 73.70, 87.0/77.6/69.4/62.9 (BP=1.000, ratio=1.041, hyp_len=24472, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.174.0.13-1.14.0.14-1.15.0.80-2.23.0.70-2.02.pth, myrk
BLEU = 74.43, 87.8/78.3/70.4/63.5 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.174.0.13-1.14.0.14-1.15.0.80-2.23.0.70-2.02.pth, rkmy
BLEU = 73.68, 87.1/77.6/69.4/62.9 (BP=1.000, ratio=1.043, hyp_len=24510, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.175.0.13-1.14.0.15-1.16.0.81-2.25.0.72-2.05.pth, myrk
BLEU = 74.21, 87.4/78.0/70.2/63.4 (BP=1.000, ratio=1.036, hyp_len=23994, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.175.0.13-1.14.0.15-1.16.0.81-2.25.0.72-2.05.pth, rkmy
BLEU = 73.44, 86.9/77.5/69.1/62.5 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.176.0.13-1.14.0.15-1.16.0.83-2.30.0.72-2.05.pth, myrk
BLEU = 74.01, 87.3/77.8/69.9/63.2 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.176.0.13-1.14.0.15-1.16.0.83-2.30.0.72-2.05.pth, rkmy
BLEU = 73.13, 86.8/77.2/68.7/62.1 (BP=1.000, ratio=1.045, hyp_len=24556, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.177.0.12-1.13.0.14-1.15.0.83-2.30.0.72-2.06.pth, myrk
BLEU = 73.96, 87.4/77.8/69.9/63.0 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.177.0.12-1.13.0.14-1.15.0.83-2.30.0.72-2.06.pth, rkmy
BLEU = 73.36, 86.9/77.3/69.0/62.4 (BP=1.000, ratio=1.043, hyp_len=24528, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.178.0.12-1.13.0.14-1.16.0.83-2.28.0.72-2.05.pth, myrk
BLEU = 74.13, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.178.0.12-1.13.0.14-1.16.0.83-2.28.0.72-2.05.pth, rkmy
BLEU = 74.28, 87.5/78.2/70.0/63.5 (BP=1.000, ratio=1.037, hyp_len=24383, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.179.0.12-1.12.0.14-1.15.0.82-2.27.0.74-2.09.pth, myrk
BLEU = 74.73, 87.6/78.3/70.7/64.2 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.179.0.12-1.12.0.14-1.15.0.82-2.27.0.74-2.09.pth, rkmy
BLEU = 73.36, 86.9/77.3/69.0/62.5 (BP=1.000, ratio=1.043, hyp_len=24528, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.180.0.13-1.13.0.15-1.16.0.82-2.27.0.72-2.06.pth, myrk
BLEU = 73.99, 87.4/77.9/69.9/63.0 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.180.0.13-1.13.0.15-1.16.0.82-2.27.0.72-2.06.pth, rkmy
BLEU = 73.38, 87.0/77.3/69.0/62.5 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.181.0.12-1.13.0.14-1.15.0.82-2.27.0.72-2.05.pth, myrk
BLEU = 74.56, 87.7/78.3/70.5/63.8 (BP=1.000, ratio=1.029, hyp_len=23821, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.181.0.12-1.13.0.14-1.15.0.82-2.27.0.72-2.05.pth, rkmy
BLEU = 74.18, 87.3/78.0/69.9/63.6 (BP=1.000, ratio=1.040, hyp_len=24456, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.18.1.68-5.38.1.62-5.05.1.72-5.56.1.52-4.56.pth, myrk
BLEU = 33.49, 63.6/41.7/27.1/17.5 (BP=1.000, ratio=1.019, hyp_len=23600, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.18.1.68-5.38.1.62-5.05.1.72-5.56.1.52-4.56.pth, rkmy
BLEU = 36.90, 66.7/45.5/30.2/20.2 (BP=1.000, ratio=1.014, hyp_len=23840, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.182.0.15-1.16.0.30-1.35.0.82-2.27.0.79-2.20.pth, myrk
BLEU = 74.15, 87.4/78.0/70.1/63.3 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.182.0.15-1.16.0.30-1.35.0.82-2.27.0.79-2.20.pth, rkmy
BLEU = 71.04, 85.6/75.4/66.4/59.4 (BP=1.000, ratio=1.052, hyp_len=24742, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.183.0.12-1.13.0.18-1.20.0.84-2.32.0.72-2.06.pth, myrk
BLEU = 73.46, 87.0/77.3/69.3/62.4 (BP=1.000, ratio=1.037, hyp_len=24006, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.183.0.12-1.13.0.18-1.20.0.84-2.32.0.72-2.06.pth, rkmy
BLEU = 72.73, 86.6/76.9/68.3/61.6 (BP=1.000, ratio=1.047, hyp_len=24607, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.184.0.12-1.13.0.16-1.17.0.84-2.32.0.71-2.03.pth, myrk
BLEU = 73.97, 87.4/77.8/69.8/63.1 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.184.0.12-1.13.0.16-1.17.0.84-2.32.0.71-2.03.pth, rkmy
BLEU = 74.06, 87.5/78.1/69.8/63.1 (BP=1.000, ratio=1.037, hyp_len=24386, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.185.0.11-1.12.0.14-1.16.0.83-2.30.0.71-2.04.pth, myrk
BLEU = 73.67, 87.3/77.6/69.5/62.6 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.185.0.11-1.12.0.14-1.16.0.83-2.30.0.71-2.04.pth, rkmy
BLEU = 74.48, 87.6/78.4/70.2/63.8 (BP=1.000, ratio=1.037, hyp_len=24369, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.186.0.12-1.13.0.15-1.16.0.84-2.32.0.71-2.04.pth, myrk
BLEU = 73.63, 87.1/77.5/69.4/62.7 (BP=1.000, ratio=1.036, hyp_len=24005, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.186.0.12-1.13.0.15-1.16.0.84-2.32.0.71-2.04.pth, rkmy
BLEU = 73.71, 87.1/77.7/69.4/62.9 (BP=1.000, ratio=1.044, hyp_len=24533, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.187.0.12-1.12.0.13-1.14.0.85-2.34.0.73-2.07.pth, myrk
BLEU = 74.00, 87.4/77.8/69.9/63.1 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.187.0.12-1.12.0.13-1.14.0.85-2.34.0.73-2.07.pth, rkmy
BLEU = 74.04, 87.3/77.9/69.7/63.4 (BP=1.000, ratio=1.041, hyp_len=24470, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.188.0.12-1.13.0.14-1.15.0.86-2.35.0.75-2.12.pth, myrk
BLEU = 72.74, 86.7/76.8/68.5/61.4 (BP=1.000, ratio=1.036, hyp_len=23996, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.188.0.12-1.13.0.14-1.15.0.86-2.35.0.75-2.12.pth, rkmy
BLEU = 73.48, 87.1/77.6/69.1/62.4 (BP=1.000, ratio=1.041, hyp_len=24466, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.189.0.12-1.13.0.13-1.14.0.86-2.36.0.74-2.09.pth, myrk
BLEU = 73.35, 86.8/77.2/69.2/62.3 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.189.0.12-1.13.0.13-1.14.0.86-2.36.0.74-2.09.pth, rkmy
BLEU = 74.07, 87.4/78.1/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.190.0.12-1.13.0.14-1.15.0.85-2.33.0.72-2.06.pth, myrk
BLEU = 73.80, 87.2/77.7/69.7/62.8 (BP=1.000, ratio=1.035, hyp_len=23961, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.190.0.12-1.13.0.14-1.15.0.85-2.33.0.72-2.06.pth, rkmy
BLEU = 73.63, 87.1/77.7/69.3/62.7 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.191.0.11-1.12.0.14-1.15.0.83-2.30.0.75-2.11.pth, myrk
BLEU = 73.86, 87.1/77.7/69.8/63.0 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.191.0.11-1.12.0.14-1.15.0.83-2.30.0.75-2.11.pth, rkmy
BLEU = 73.45, 87.0/77.5/69.1/62.5 (BP=1.000, ratio=1.044, hyp_len=24555, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.19.1.62-5.06.1.44-4.20.1.61-4.99.1.42-4.13.pth, myrk
BLEU = 36.64, 66.7/45.1/30.1/19.9 (BP=1.000, ratio=1.004, hyp_len=23262, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.19.1.62-5.06.1.44-4.20.1.61-4.99.1.42-4.13.pth, rkmy
BLEU = 43.19, 71.0/51.4/36.5/26.2 (BP=1.000, ratio=1.005, hyp_len=23626, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.192.0.11-1.12.0.15-1.16.0.85-2.35.0.74-2.09.pth, myrk
BLEU = 73.67, 87.2/77.5/69.5/62.7 (BP=1.000, ratio=1.035, hyp_len=23965, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.192.0.11-1.12.0.15-1.16.0.85-2.35.0.74-2.09.pth, rkmy
BLEU = 73.68, 87.1/77.6/69.4/62.9 (BP=1.000, ratio=1.041, hyp_len=24471, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.193.0.10-1.11.0.13-1.14.0.85-2.33.0.74-2.09.pth, myrk
BLEU = 74.51, 87.7/78.2/70.4/63.8 (BP=1.000, ratio=1.031, hyp_len=23871, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.193.0.10-1.11.0.13-1.14.0.85-2.33.0.74-2.09.pth, rkmy
BLEU = 73.62, 87.0/77.6/69.4/62.7 (BP=1.000, ratio=1.042, hyp_len=24508, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.194.0.10-1.11.0.12-1.13.0.87-2.39.0.75-2.13.pth, myrk
BLEU = 73.87, 87.3/77.7/69.8/62.9 (BP=1.000, ratio=1.033, hyp_len=23923, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.194.0.10-1.11.0.12-1.13.0.87-2.39.0.75-2.13.pth, rkmy
BLEU = 74.25, 87.5/78.3/70.0/63.5 (BP=1.000, ratio=1.038, hyp_len=24410, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.195.0.12-1.12.0.13-1.14.0.87-2.38.0.76-2.13.pth, myrk
BLEU = 73.43, 86.9/77.3/69.3/62.4 (BP=1.000, ratio=1.035, hyp_len=23968, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.195.0.12-1.12.0.13-1.14.0.87-2.38.0.76-2.13.pth, rkmy
BLEU = 73.70, 87.1/77.7/69.4/62.9 (BP=1.000, ratio=1.043, hyp_len=24516, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.196.0.12-1.13.0.13-1.14.0.85-2.34.0.74-2.09.pth, myrk
BLEU = 73.84, 87.2/77.6/69.8/63.0 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.196.0.12-1.13.0.13-1.14.0.85-2.34.0.74-2.09.pth, rkmy
BLEU = 73.60, 87.0/77.5/69.3/62.8 (BP=1.000, ratio=1.042, hyp_len=24502, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.197.0.11-1.12.0.12-1.13.0.88-2.40.0.76-2.15.pth, myrk
BLEU = 73.57, 87.1/77.4/69.4/62.6 (BP=1.000, ratio=1.038, hyp_len=24032, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.197.0.11-1.12.0.12-1.13.0.88-2.40.0.76-2.15.pth, rkmy
BLEU = 73.02, 86.7/77.1/68.6/62.0 (BP=1.000, ratio=1.046, hyp_len=24596, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.198.0.11-1.11.0.12-1.13.0.88-2.42.0.75-2.12.pth, myrk
BLEU = 74.14, 87.6/77.9/70.0/63.2 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.198.0.11-1.11.0.12-1.13.0.88-2.42.0.75-2.12.pth, rkmy
BLEU = 73.29, 86.8/77.2/69.0/62.4 (BP=1.000, ratio=1.044, hyp_len=24542, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.199.0.11-1.12.0.12-1.13.0.87-2.38.0.74-2.10.pth, myrk
BLEU = 74.33, 87.6/78.2/70.3/63.4 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.199.0.11-1.12.0.12-1.13.0.87-2.38.0.74-2.10.pth, rkmy
BLEU = 73.46, 87.0/77.4/69.1/62.6 (BP=1.000, ratio=1.044, hyp_len=24533, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.200.0.11-1.12.0.12-1.13.0.86-2.37.0.76-2.14.pth, myrk
BLEU = 74.53, 87.8/78.4/70.5/63.6 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.200.0.11-1.12.0.12-1.13.0.86-2.37.0.76-2.14.pth, rkmy
BLEU = 72.51, 86.6/76.7/68.0/61.3 (BP=1.000, ratio=1.049, hyp_len=24664, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.201.0.11-1.12.0.12-1.13.0.86-2.35.0.77-2.15.pth, myrk
BLEU = 74.23, 87.5/78.0/70.2/63.4 (BP=1.000, ratio=1.029, hyp_len=23829, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.201.0.11-1.12.0.12-1.13.0.86-2.35.0.77-2.15.pth, rkmy
BLEU = 73.50, 87.0/77.6/69.2/62.5 (BP=1.000, ratio=1.044, hyp_len=24533, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.20.1.48-4.41.1.40-4.04.1.54-4.66.1.43-4.18.pth, myrk
BLEU = 39.84, 68.0/47.6/33.4/23.3 (BP=1.000, ratio=1.015, hyp_len=23518, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.20.1.48-4.41.1.40-4.04.1.54-4.66.1.43-4.18.pth, rkmy
BLEU = 43.16, 71.1/51.5/36.4/26.0 (BP=1.000, ratio=1.006, hyp_len=23647, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.202.0.11-1.12.0.14-1.15.0.87-2.39.0.76-2.14.pth, myrk
BLEU = 74.42, 87.8/78.2/70.3/63.5 (BP=1.000, ratio=1.031, hyp_len=23879, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.202.0.11-1.12.0.14-1.15.0.87-2.39.0.76-2.14.pth, rkmy
BLEU = 72.99, 86.7/77.1/68.6/61.8 (BP=1.000, ratio=1.045, hyp_len=24557, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.203.0.12-1.12.0.12-1.13.0.86-2.37.0.76-2.14.pth, myrk
BLEU = 74.23, 87.6/78.0/70.2/63.3 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.203.0.12-1.12.0.12-1.13.0.86-2.37.0.76-2.14.pth, rkmy
BLEU = 73.82, 87.2/77.6/69.5/63.1 (BP=1.000, ratio=1.041, hyp_len=24463, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.204.0.12-1.12.0.12-1.12.0.85-2.34.0.79-2.21.pth, myrk
BLEU = 73.33, 86.9/77.2/69.2/62.3 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.204.0.12-1.12.0.12-1.12.0.85-2.34.0.79-2.21.pth, rkmy
BLEU = 74.31, 87.5/78.2/70.1/63.6 (BP=1.000, ratio=1.039, hyp_len=24430, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.205.0.10-1.11.0.12-1.13.0.86-2.36.0.77-2.16.pth, myrk
BLEU = 74.03, 87.5/77.9/69.9/63.0 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.205.0.10-1.11.0.12-1.13.0.86-2.36.0.77-2.16.pth, rkmy
BLEU = 74.37, 87.7/78.3/70.0/63.6 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.206.0.10-1.10.0.12-1.13.0.87-2.38.0.77-2.15.pth, myrk
BLEU = 73.85, 87.1/77.6/69.7/63.0 (BP=1.000, ratio=1.035, hyp_len=23975, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.206.0.10-1.10.0.12-1.13.0.87-2.38.0.77-2.15.pth, rkmy
BLEU = 73.98, 87.3/77.9/69.7/63.2 (BP=1.000, ratio=1.038, hyp_len=24394, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.207.0.10-1.11.0.12-1.13.0.86-2.37.0.81-2.26.pth, myrk
BLEU = 74.14, 87.4/77.9/70.1/63.3 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.207.0.10-1.11.0.12-1.13.0.86-2.37.0.81-2.26.pth, rkmy
BLEU = 73.75, 87.3/77.8/69.4/62.8 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.208.0.10-1.10.0.13-1.14.0.89-2.43.0.78-2.19.pth, myrk
BLEU = 73.97, 87.3/77.8/69.9/63.1 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.208.0.10-1.10.0.13-1.14.0.89-2.43.0.78-2.19.pth, rkmy
BLEU = 73.22, 86.9/77.3/68.9/62.1 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.209.0.10-1.11.0.15-1.17.0.87-2.39.0.76-2.15.pth, myrk
BLEU = 74.15, 87.4/77.9/70.0/63.4 (BP=1.000, ratio=1.035, hyp_len=23964, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.209.0.10-1.11.0.15-1.17.0.87-2.39.0.76-2.15.pth, rkmy
BLEU = 73.65, 86.9/77.6/69.4/62.8 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.210.0.09-1.10.0.13-1.14.0.89-2.44.0.75-2.11.pth, myrk
BLEU = 73.91, 87.3/77.8/69.8/62.9 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.210.0.09-1.10.0.13-1.14.0.89-2.44.0.75-2.11.pth, rkmy
BLEU = 73.17, 86.8/77.1/68.8/62.3 (BP=1.000, ratio=1.045, hyp_len=24569, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.211.0.10-1.10.0.13-1.13.0.88-2.41.0.76-2.14.pth, myrk
BLEU = 74.22, 87.5/78.1/70.1/63.4 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.211.0.10-1.10.0.13-1.13.0.88-2.41.0.76-2.14.pth, rkmy
BLEU = 73.22, 86.8/77.1/68.8/62.4 (BP=1.000, ratio=1.047, hyp_len=24613, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.21.1.36-3.91.1.36-3.91.1.43-4.18.1.61-5.00.pth, myrk
BLEU = 44.63, 71.4/52.0/38.2/27.9 (BP=1.000, ratio=1.010, hyp_len=23382, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.21.1.36-3.91.1.36-3.91.1.43-4.18.1.61-5.00.pth, rkmy
BLEU = 37.70, 67.8/46.6/31.0/20.9 (BP=0.997, ratio=0.997, hyp_len=23429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.212.0.10-1.10.0.12-1.13.0.90-2.47.0.79-2.21.pth, myrk
BLEU = 73.91, 87.3/77.8/69.8/63.0 (BP=1.000, ratio=1.036, hyp_len=24001, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.212.0.10-1.10.0.12-1.13.0.90-2.47.0.79-2.21.pth, rkmy
BLEU = 72.51, 86.5/76.6/68.0/61.3 (BP=1.000, ratio=1.047, hyp_len=24622, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.213.0.10-1.10.0.13-1.13.0.90-2.46.0.79-2.20.pth, myrk
BLEU = 74.06, 87.5/77.9/69.9/63.1 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.213.0.10-1.10.0.13-1.13.0.90-2.46.0.79-2.20.pth, rkmy
BLEU = 72.81, 86.6/77.0/68.5/61.5 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.214.0.12-1.13.0.25-1.28.0.91-2.48.0.83-2.30.pth, myrk
BLEU = 73.08, 87.0/77.2/68.8/61.7 (BP=1.000, ratio=1.035, hyp_len=23981, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.214.0.12-1.13.0.25-1.28.0.91-2.48.0.83-2.30.pth, rkmy
BLEU = 71.03, 85.8/75.3/66.5/59.2 (BP=1.000, ratio=1.050, hyp_len=24673, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.215.0.11-1.12.0.18-1.19.0.92-2.50.0.77-2.15.pth, myrk
BLEU = 73.89, 87.2/77.7/69.8/63.0 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.215.0.11-1.12.0.18-1.19.0.92-2.50.0.77-2.15.pth, rkmy
BLEU = 72.48, 86.4/76.6/68.0/61.3 (BP=1.000, ratio=1.048, hyp_len=24642, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.216.0.10-1.11.0.15-1.16.0.91-2.49.0.80-2.23.pth, myrk
BLEU = 73.36, 87.0/77.3/69.2/62.3 (BP=1.000, ratio=1.034, hyp_len=23940, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.216.0.10-1.11.0.15-1.16.0.91-2.49.0.80-2.23.pth, rkmy
BLEU = 74.27, 87.5/78.1/70.0/63.5 (BP=1.000, ratio=1.036, hyp_len=24348, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.217.0.10-1.11.0.13-1.14.0.90-2.47.0.77-2.16.pth, myrk
BLEU = 73.84, 87.3/77.8/69.8/62.8 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.217.0.10-1.11.0.13-1.14.0.90-2.47.0.77-2.16.pth, rkmy
BLEU = 73.85, 87.3/77.8/69.5/63.0 (BP=1.000, ratio=1.041, hyp_len=24482, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.218.0.10-1.10.0.12-1.13.0.91-2.49.0.77-2.16.pth, myrk
BLEU = 73.55, 87.2/77.6/69.4/62.3 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.218.0.10-1.10.0.12-1.13.0.91-2.49.0.77-2.16.pth, rkmy
BLEU = 73.74, 87.2/77.6/69.4/62.9 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.219.0.10-1.11.0.11-1.12.0.93-2.54.0.78-2.18.pth, myrk
BLEU = 73.23, 87.0/77.2/69.0/62.0 (BP=1.000, ratio=1.035, hyp_len=23975, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.219.0.10-1.11.0.11-1.12.0.93-2.54.0.78-2.18.pth, rkmy
BLEU = 73.96, 87.4/78.0/69.7/63.1 (BP=1.000, ratio=1.039, hyp_len=24420, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.220.0.12-1.13.0.12-1.12.0.93-2.53.0.81-2.25.pth, myrk
BLEU = 72.77, 87.0/76.9/68.5/61.2 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.220.0.12-1.13.0.12-1.12.0.93-2.53.0.81-2.25.pth, rkmy
BLEU = 73.33, 87.0/77.4/68.9/62.3 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.221.0.13-1.13.0.11-1.12.0.92-2.51.0.79-2.20.pth, myrk
BLEU = 71.48, 86.3/75.9/67.1/59.4 (BP=1.000, ratio=1.037, hyp_len=24015, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.221.0.13-1.13.0.11-1.12.0.92-2.51.0.79-2.20.pth, rkmy
BLEU = 74.08, 87.3/78.0/69.8/63.4 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.22.1.48-4.39.1.43-4.17.1.50-4.49.1.29-3.63.pth, myrk
BLEU = 40.80, 68.6/48.6/34.3/24.2 (BP=1.000, ratio=1.043, hyp_len=24154, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.22.1.48-4.39.1.43-4.17.1.50-4.49.1.29-3.63.pth, rkmy
BLEU = 47.52, 73.8/55.4/40.9/30.5 (BP=1.000, ratio=1.005, hyp_len=23637, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.222.0.12-1.12.0.11-1.11.0.92-2.52.0.80-2.23.pth, myrk
BLEU = 72.84, 86.8/76.9/68.6/61.4 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.222.0.12-1.12.0.11-1.11.0.92-2.52.0.80-2.23.pth, rkmy
BLEU = 73.69, 87.0/77.6/69.4/62.9 (BP=1.000, ratio=1.043, hyp_len=24526, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.223.0.10-1.10.0.10-1.11.0.92-2.50.0.78-2.18.pth, myrk
BLEU = 73.80, 87.3/77.7/69.6/62.8 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.223.0.10-1.10.0.10-1.11.0.92-2.50.0.78-2.18.pth, rkmy
BLEU = 73.80, 87.3/77.7/69.5/62.9 (BP=1.000, ratio=1.042, hyp_len=24487, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.224.0.10-1.10.0.10-1.11.0.92-2.52.0.76-2.13.pth, myrk
BLEU = 72.91, 86.7/76.9/68.7/61.7 (BP=1.000, ratio=1.039, hyp_len=24066, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.224.0.10-1.10.0.10-1.11.0.92-2.52.0.76-2.13.pth, rkmy
BLEU = 73.44, 87.0/77.4/69.1/62.5 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.225.0.10-1.10.0.10-1.11.0.92-2.52.0.76-2.14.pth, myrk
BLEU = 73.10, 86.9/77.1/68.9/61.8 (BP=1.000, ratio=1.037, hyp_len=24021, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.225.0.10-1.10.0.10-1.11.0.92-2.52.0.76-2.14.pth, rkmy
BLEU = 73.90, 87.4/78.0/69.6/62.9 (BP=1.000, ratio=1.041, hyp_len=24480, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.226.0.11-1.12.0.11-1.11.0.92-2.51.0.78-2.18.pth, myrk
BLEU = 71.92, 86.3/76.1/67.6/60.3 (BP=1.000, ratio=1.044, hyp_len=24182, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.226.0.11-1.12.0.11-1.11.0.92-2.51.0.78-2.18.pth, rkmy
BLEU = 73.36, 87.0/77.5/69.0/62.3 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.227.0.11-1.11.0.11-1.11.0.92-2.50.0.78-2.19.pth, myrk
BLEU = 72.24, 86.3/76.3/68.0/60.9 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.227.0.11-1.11.0.11-1.11.0.92-2.50.0.78-2.19.pth, rkmy
BLEU = 74.11, 87.4/78.1/69.8/63.3 (BP=1.000, ratio=1.039, hyp_len=24435, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.228.0.10-1.10.0.10-1.10.0.93-2.54.0.78-2.18.pth, myrk
BLEU = 74.30, 87.8/78.2/70.2/63.3 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.228.0.10-1.10.0.10-1.10.0.93-2.54.0.78-2.18.pth, rkmy
BLEU = 73.52, 87.1/77.5/69.2/62.6 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.229.0.09-1.09.0.09-1.10.0.92-2.52.0.80-2.22.pth, myrk
BLEU = 73.91, 87.4/77.8/69.8/62.8 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.229.0.09-1.09.0.09-1.10.0.92-2.52.0.80-2.22.pth, rkmy
BLEU = 74.01, 87.3/78.0/69.7/63.2 (BP=1.000, ratio=1.041, hyp_len=24464, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.230.0.09-1.09.0.10-1.10.0.93-2.54.0.79-2.19.pth, myrk
BLEU = 74.21, 87.5/78.0/70.1/63.4 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.230.0.09-1.09.0.10-1.10.0.93-2.54.0.79-2.19.pth, rkmy
BLEU = 73.87, 87.3/77.9/69.5/63.0 (BP=1.000, ratio=1.039, hyp_len=24427, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.231.0.08-1.09.0.10-1.11.0.93-2.53.0.78-2.18.pth, myrk
BLEU = 74.03, 87.5/77.9/69.9/63.1 (BP=1.000, ratio=1.033, hyp_len=23915, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.231.0.08-1.09.0.10-1.11.0.93-2.53.0.78-2.18.pth, rkmy
BLEU = 73.95, 87.5/78.0/69.6/63.0 (BP=1.000, ratio=1.039, hyp_len=24426, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.23.1.25-3.49.1.17-3.24.1.30-3.68.1.20-3.33.pth, myrk
BLEU = 50.62, 75.1/57.5/44.3/34.3 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.23.1.25-3.49.1.17-3.24.1.30-3.68.1.20-3.33.pth, rkmy
BLEU = 52.55, 76.5/59.7/46.2/36.1 (BP=1.000, ratio=1.011, hyp_len=23757, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.232.0.09-1.09.0.10-1.11.0.91-2.48.0.80-2.23.pth, myrk
BLEU = 73.79, 87.3/77.6/69.6/62.8 (BP=1.000, ratio=1.033, hyp_len=23924, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.232.0.09-1.09.0.10-1.11.0.91-2.48.0.80-2.23.pth, rkmy
BLEU = 74.02, 87.4/78.1/69.7/63.1 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.233.0.08-1.08.0.10-1.10.0.92-2.51.0.79-2.20.pth, myrk
BLEU = 74.00, 87.5/77.9/69.9/63.0 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.233.0.08-1.08.0.10-1.10.0.92-2.51.0.79-2.20.pth, rkmy
BLEU = 73.85, 87.3/77.8/69.6/63.0 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.234.0.08-1.09.0.10-1.10.0.94-2.56.0.80-2.23.pth, myrk
BLEU = 74.19, 87.5/78.0/70.1/63.3 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.234.0.08-1.09.0.10-1.10.0.94-2.56.0.80-2.23.pth, rkmy
BLEU = 73.15, 86.7/77.2/68.8/62.1 (BP=1.000, ratio=1.045, hyp_len=24564, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.235.0.08-1.09.0.10-1.10.0.92-2.52.0.81-2.24.pth, myrk
BLEU = 73.73, 87.4/77.7/69.5/62.6 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.235.0.08-1.09.0.10-1.10.0.92-2.52.0.81-2.24.pth, rkmy
BLEU = 74.36, 87.5/78.3/70.1/63.6 (BP=1.000, ratio=1.037, hyp_len=24372, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.236.0.08-1.08.0.10-1.11.0.92-2.51.0.81-2.24.pth, myrk
BLEU = 73.98, 87.6/78.0/69.8/62.8 (BP=1.000, ratio=1.033, hyp_len=23922, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.236.0.08-1.08.0.10-1.11.0.92-2.51.0.81-2.24.pth, rkmy
BLEU = 73.59, 87.1/77.6/69.3/62.7 (BP=1.000, ratio=1.042, hyp_len=24490, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.237.0.08-1.08.0.09-1.10.0.94-2.56.0.83-2.30.pth, myrk
BLEU = 73.67, 87.3/77.6/69.5/62.5 (BP=1.000, ratio=1.036, hyp_len=23989, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.237.0.08-1.08.0.09-1.10.0.94-2.56.0.83-2.30.pth, rkmy
BLEU = 74.27, 87.6/78.3/70.0/63.4 (BP=1.000, ratio=1.037, hyp_len=24372, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.238.0.08-1.08.0.10-1.11.0.93-2.55.0.80-2.23.pth, myrk
BLEU = 74.03, 87.5/77.9/69.9/63.1 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.238.0.08-1.08.0.10-1.11.0.93-2.55.0.80-2.23.pth, rkmy
BLEU = 73.50, 87.0/77.5/69.2/62.5 (BP=1.000, ratio=1.043, hyp_len=24529, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.239.0.08-1.08.0.10-1.11.0.96-2.62.0.80-2.23.pth, myrk
BLEU = 73.62, 87.3/77.5/69.4/62.5 (BP=1.000, ratio=1.037, hyp_len=24011, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.239.0.08-1.08.0.10-1.11.0.96-2.62.0.80-2.23.pth, rkmy
BLEU = 73.72, 87.2/77.7/69.4/62.8 (BP=1.000, ratio=1.038, hyp_len=24399, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.240.0.08-1.08.0.11-1.11.0.95-2.58.0.82-2.28.pth, myrk
BLEU = 74.43, 87.6/78.2/70.4/63.7 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.240.0.08-1.08.0.11-1.11.0.95-2.58.0.82-2.28.pth, rkmy
BLEU = 73.92, 87.2/78.0/69.7/63.0 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.241.0.08-1.09.0.10-1.11.0.93-2.54.0.79-2.20.pth, myrk
BLEU = 73.82, 87.3/77.7/69.7/62.9 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.241.0.08-1.09.0.10-1.11.0.93-2.54.0.79-2.20.pth, rkmy
BLEU = 73.73, 87.1/77.7/69.4/62.9 (BP=1.000, ratio=1.041, hyp_len=24484, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.24.1.19-3.29.1.32-3.76.1.25-3.48.1.22-3.37.pth, myrk
BLEU = 53.20, 76.5/59.8/47.1/37.1 (BP=1.000, ratio=1.008, hyp_len=23336, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.24.1.19-3.29.1.32-3.76.1.25-3.48.1.22-3.37.pth, rkmy
BLEU = 50.26, 75.1/57.7/43.8/33.6 (BP=1.000, ratio=1.013, hyp_len=23805, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.242.0.08-1.09.0.10-1.11.0.94-2.57.0.82-2.26.pth, myrk
BLEU = 73.83, 87.4/77.7/69.6/62.8 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.242.0.08-1.09.0.10-1.11.0.94-2.57.0.82-2.26.pth, rkmy
BLEU = 74.00, 87.4/77.9/69.8/63.1 (BP=1.000, ratio=1.038, hyp_len=24396, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.243.0.08-1.09.0.10-1.11.0.93-2.53.0.80-2.22.pth, myrk
BLEU = 73.81, 87.4/77.8/69.7/62.7 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.243.0.08-1.09.0.10-1.11.0.93-2.53.0.80-2.22.pth, rkmy
BLEU = 74.56, 87.6/78.4/70.4/63.9 (BP=1.000, ratio=1.034, hyp_len=24309, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.244.0.08-1.08.0.10-1.10.0.93-2.54.0.81-2.25.pth, myrk
BLEU = 73.58, 87.4/77.6/69.4/62.3 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.244.0.08-1.08.0.10-1.10.0.93-2.54.0.81-2.25.pth, rkmy
BLEU = 73.54, 87.1/77.6/69.2/62.5 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.245.0.09-1.09.0.10-1.10.0.94-2.56.0.82-2.26.pth, myrk
BLEU = 73.91, 87.3/77.8/69.8/62.9 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.245.0.09-1.09.0.10-1.10.0.94-2.56.0.82-2.26.pth, rkmy
BLEU = 73.68, 87.2/77.7/69.3/62.7 (BP=1.000, ratio=1.038, hyp_len=24396, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.246.0.10-1.11.0.10-1.10.0.93-2.54.0.86-2.36.pth, myrk
BLEU = 73.42, 87.1/77.3/69.3/62.3 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.246.0.10-1.11.0.10-1.10.0.93-2.54.0.86-2.36.pth, rkmy
BLEU = 73.24, 86.9/77.3/68.8/62.2 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.247.0.13-1.14.0.09-1.09.0.96-2.61.0.85-2.33.pth, myrk
BLEU = 73.66, 87.2/77.5/69.5/62.6 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.247.0.13-1.14.0.09-1.09.0.96-2.61.0.85-2.33.pth, rkmy
BLEU = 73.55, 87.0/77.6/69.2/62.6 (BP=1.000, ratio=1.044, hyp_len=24555, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.248.0.10-1.11.0.09-1.09.0.97-2.63.0.82-2.26.pth, myrk
BLEU = 73.03, 87.0/77.0/68.8/61.7 (BP=1.000, ratio=1.036, hyp_len=24005, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.248.0.10-1.11.0.09-1.09.0.97-2.63.0.82-2.26.pth, rkmy
BLEU = 73.81, 87.3/77.7/69.5/62.9 (BP=1.000, ratio=1.040, hyp_len=24446, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.249.0.09-1.09.0.09-1.10.0.94-2.57.0.80-2.22.pth, myrk
BLEU = 73.15, 87.0/77.2/68.9/61.8 (BP=1.000, ratio=1.037, hyp_len=24014, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.249.0.09-1.09.0.09-1.10.0.94-2.57.0.80-2.22.pth, rkmy
BLEU = 73.71, 87.2/77.7/69.4/62.8 (BP=1.000, ratio=1.040, hyp_len=24459, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.250.0.09-1.09.0.09-1.10.0.96-2.60.0.81-2.25.pth, myrk
BLEU = 73.36, 87.2/77.3/69.1/62.2 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.250.0.09-1.09.0.09-1.10.0.96-2.60.0.81-2.25.pth, rkmy
BLEU = 73.31, 87.0/77.3/69.0/62.3 (BP=1.000, ratio=1.043, hyp_len=24521, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.251.0.08-1.08.0.09-1.09.0.96-2.61.0.84-2.32.pth, myrk
BLEU = 74.18, 87.6/78.1/70.1/63.2 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.251.0.08-1.08.0.09-1.09.0.96-2.61.0.84-2.32.pth, rkmy
BLEU = 73.98, 87.2/77.9/69.7/63.2 (BP=1.000, ratio=1.042, hyp_len=24507, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.25.1.05-2.86.1.04-2.84.1.17-3.23.1.10-3.00.pth, myrk
BLEU = 56.80, 78.7/63.0/50.9/41.2 (BP=1.000, ratio=1.005, hyp_len=23281, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.25.1.05-2.86.1.04-2.84.1.17-3.23.1.10-3.00.pth, rkmy
BLEU = 56.40, 78.7/63.2/50.2/40.5 (BP=1.000, ratio=1.019, hyp_len=23967, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.252.0.08-1.08.0.10-1.10.0.96-2.61.0.84-2.30.pth, myrk
BLEU = 73.36, 87.2/77.3/69.1/62.1 (BP=1.000, ratio=1.036, hyp_len=23993, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.252.0.08-1.08.0.10-1.10.0.96-2.61.0.84-2.30.pth, rkmy
BLEU = 74.37, 87.8/78.3/70.1/63.6 (BP=1.000, ratio=1.033, hyp_len=24287, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.253.0.08-1.08.0.09-1.10.0.96-2.61.0.82-2.27.pth, myrk
BLEU = 73.70, 87.4/77.5/69.5/62.7 (BP=1.000, ratio=1.034, hyp_len=23939, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.253.0.08-1.08.0.09-1.10.0.96-2.61.0.82-2.27.pth, rkmy
BLEU = 74.86, 87.9/78.7/70.6/64.2 (BP=1.000, ratio=1.033, hyp_len=24293, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.254.0.08-1.08.0.09-1.10.0.95-2.60.0.86-2.37.pth, myrk
BLEU = 73.81, 87.5/77.8/69.7/62.6 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.254.0.08-1.08.0.09-1.10.0.95-2.60.0.86-2.37.pth, rkmy
BLEU = 73.99, 87.4/77.9/69.7/63.2 (BP=1.000, ratio=1.038, hyp_len=24408, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.255.0.08-1.08.0.09-1.09.0.97-2.64.0.86-2.37.pth, myrk
BLEU = 73.66, 87.3/77.6/69.5/62.5 (BP=1.000, ratio=1.034, hyp_len=23939, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.255.0.08-1.08.0.09-1.09.0.97-2.64.0.86-2.37.pth, rkmy
BLEU = 73.71, 87.3/77.7/69.4/62.8 (BP=1.000, ratio=1.040, hyp_len=24445, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.256.0.08-1.08.0.09-1.09.0.97-2.64.0.83-2.29.pth, myrk
BLEU = 74.04, 87.4/78.0/70.0/63.0 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.256.0.08-1.08.0.09-1.09.0.97-2.64.0.83-2.29.pth, rkmy
BLEU = 73.65, 87.3/77.7/69.3/62.6 (BP=1.000, ratio=1.038, hyp_len=24411, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.257.0.08-1.08.0.10-1.11.0.95-2.59.0.84-2.32.pth, myrk
BLEU = 73.99, 87.5/77.9/69.8/63.0 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.257.0.08-1.08.0.10-1.11.0.95-2.59.0.84-2.32.pth, rkmy
BLEU = 73.71, 87.2/77.7/69.4/62.7 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.258.0.07-1.07.0.10-1.11.0.96-2.62.0.82-2.27.pth, myrk
BLEU = 73.91, 87.5/77.9/69.8/62.8 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.258.0.07-1.07.0.10-1.11.0.96-2.62.0.82-2.27.pth, rkmy
BLEU = 73.31, 87.0/77.3/68.9/62.3 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.259.0.08-1.08.0.09-1.10.0.98-2.65.0.84-2.31.pth, myrk
BLEU = 72.81, 86.8/76.9/68.6/61.4 (BP=1.000, ratio=1.037, hyp_len=24006, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.259.0.08-1.08.0.09-1.10.0.98-2.65.0.84-2.31.pth, rkmy
BLEU = 74.53, 87.6/78.4/70.3/63.9 (BP=1.000, ratio=1.035, hyp_len=24343, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.260.0.08-1.08.0.10-1.10.0.99-2.69.0.83-2.30.pth, myrk
BLEU = 73.35, 87.0/77.3/69.2/62.2 (BP=1.000, ratio=1.036, hyp_len=24003, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.260.0.08-1.08.0.10-1.10.0.99-2.69.0.83-2.30.pth, rkmy
BLEU = 74.11, 87.5/78.1/69.8/63.3 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.261.0.07-1.08.0.09-1.09.0.96-2.61.0.83-2.30.pth, myrk
BLEU = 74.30, 87.7/78.2/70.2/63.3 (BP=1.000, ratio=1.029, hyp_len=23826, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.261.0.07-1.08.0.09-1.09.0.96-2.61.0.83-2.30.pth, rkmy
BLEU = 73.72, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.26.1.02-2.77.1.03-2.81.1.16-3.18.1.07-2.93.pth, myrk
BLEU = 57.62, 79.3/63.9/51.7/42.1 (BP=1.000, ratio=1.017, hyp_len=23547, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.26.1.02-2.77.1.03-2.81.1.16-3.18.1.07-2.93.pth, rkmy
BLEU = 57.26, 79.2/64.0/51.2/41.4 (BP=1.000, ratio=1.015, hyp_len=23854, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.262.0.08-1.08.0.09-1.09.1.00-2.71.0.82-2.28.pth, myrk
BLEU = 72.78, 86.9/77.0/68.5/61.3 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.262.0.08-1.08.0.09-1.09.1.00-2.71.0.82-2.28.pth, rkmy
BLEU = 73.51, 87.2/77.6/69.1/62.5 (BP=1.000, ratio=1.041, hyp_len=24471, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.263.0.07-1.08.0.09-1.09.0.97-2.63.0.83-2.29.pth, myrk
BLEU = 73.59, 87.4/77.6/69.4/62.4 (BP=1.000, ratio=1.035, hyp_len=23961, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.263.0.07-1.08.0.09-1.09.0.97-2.63.0.83-2.29.pth, rkmy
BLEU = 74.37, 87.5/78.3/70.1/63.7 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.264.0.07-1.08.0.09-1.09.0.96-2.60.0.84-2.31.pth, myrk
BLEU = 73.80, 87.5/77.8/69.6/62.6 (BP=1.000, ratio=1.031, hyp_len=23869, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.264.0.07-1.08.0.09-1.09.0.96-2.60.0.84-2.31.pth, rkmy
BLEU = 73.47, 87.1/77.5/69.1/62.4 (BP=1.000, ratio=1.043, hyp_len=24520, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.265.0.07-1.07.0.08-1.09.0.96-2.60.0.85-2.33.pth, myrk
BLEU = 73.77, 87.3/77.6/69.7/62.7 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.265.0.07-1.07.0.08-1.09.0.96-2.60.0.85-2.33.pth, rkmy
BLEU = 74.07, 87.4/78.0/69.8/63.3 (BP=1.000, ratio=1.043, hyp_len=24509, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.266.0.08-1.08.0.08-1.09.0.97-2.65.0.83-2.29.pth, myrk
BLEU = 73.99, 87.5/77.8/69.9/63.0 (BP=1.000, ratio=1.034, hyp_len=23938, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.266.0.08-1.08.0.08-1.09.0.97-2.65.0.83-2.29.pth, rkmy
BLEU = 73.94, 87.4/77.9/69.6/63.0 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.267.0.07-1.07.0.08-1.08.0.96-2.62.0.83-2.30.pth, myrk
BLEU = 73.73, 87.3/77.6/69.5/62.8 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.267.0.07-1.07.0.08-1.08.0.96-2.62.0.83-2.30.pth, rkmy
BLEU = 74.01, 87.4/78.0/69.7/63.1 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.268.0.07-1.07.0.08-1.08.0.96-2.62.0.84-2.32.pth, myrk
BLEU = 74.00, 87.4/77.8/69.9/63.1 (BP=1.000, ratio=1.033, hyp_len=23922, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.268.0.07-1.07.0.08-1.08.0.96-2.62.0.84-2.32.pth, rkmy
BLEU = 73.58, 87.2/77.6/69.2/62.6 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.269.0.07-1.07.0.08-1.08.0.99-2.68.0.86-2.35.pth, myrk
BLEU = 73.67, 87.0/77.5/69.6/62.8 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.269.0.07-1.07.0.08-1.08.0.99-2.68.0.86-2.35.pth, rkmy
BLEU = 74.51, 87.7/78.4/70.3/63.8 (BP=1.000, ratio=1.036, hyp_len=24367, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.270.0.07-1.07.0.08-1.08.0.99-2.68.0.84-2.32.pth, myrk
BLEU = 73.75, 87.5/77.7/69.5/62.6 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.270.0.07-1.07.0.08-1.08.0.99-2.68.0.84-2.32.pth, rkmy
BLEU = 72.91, 86.7/77.0/68.5/61.8 (BP=1.000, ratio=1.048, hyp_len=24632, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.27.0.95-2.60.0.94-2.55.1.11-3.04.1.03-2.80.pth, myrk
BLEU = 58.97, 79.9/65.0/53.3/43.8 (BP=1.000, ratio=1.020, hyp_len=23633, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.27.0.95-2.60.0.94-2.55.1.11-3.04.1.03-2.80.pth, rkmy
BLEU = 58.59, 79.9/65.2/52.6/43.0 (BP=1.000, ratio=1.024, hyp_len=24081, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.271.0.07-1.07.0.07-1.08.0.97-2.65.0.85-2.34.pth, myrk
BLEU = 73.38, 87.2/77.4/69.2/62.2 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.271.0.07-1.07.0.07-1.08.0.97-2.65.0.85-2.34.pth, rkmy
BLEU = 74.24, 87.6/78.2/69.9/63.4 (BP=1.000, ratio=1.036, hyp_len=24364, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.272.0.07-1.07.0.09-1.09.0.99-2.68.0.84-2.31.pth, myrk
BLEU = 73.28, 87.1/77.3/69.0/62.1 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.272.0.07-1.07.0.09-1.09.0.99-2.68.0.84-2.31.pth, rkmy
BLEU = 73.68, 87.3/77.7/69.3/62.6 (BP=1.000, ratio=1.039, hyp_len=24420, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.273.0.08-1.08.0.09-1.09.0.98-2.66.0.87-2.39.pth, myrk
BLEU = 73.92, 87.4/77.8/69.8/62.9 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.273.0.08-1.08.0.09-1.09.0.98-2.66.0.87-2.39.pth, rkmy
BLEU = 73.68, 87.4/77.7/69.3/62.6 (BP=1.000, ratio=1.036, hyp_len=24350, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.274.0.09-1.09.0.12-1.12.0.98-2.66.0.84-2.32.pth, myrk
BLEU = 73.36, 87.3/77.5/69.1/62.0 (BP=1.000, ratio=1.033, hyp_len=23922, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.274.0.09-1.09.0.12-1.12.0.98-2.66.0.84-2.32.pth, rkmy
BLEU = 73.45, 87.2/77.6/69.0/62.3 (BP=1.000, ratio=1.037, hyp_len=24371, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.275.0.08-1.08.0.11-1.11.0.98-2.65.0.85-2.35.pth, myrk
BLEU = 72.70, 86.9/76.9/68.4/61.1 (BP=1.000, ratio=1.037, hyp_len=24006, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.275.0.08-1.08.0.11-1.11.0.98-2.65.0.85-2.35.pth, rkmy
BLEU = 73.50, 87.2/77.6/69.1/62.4 (BP=1.000, ratio=1.037, hyp_len=24374, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.276.0.07-1.08.0.10-1.11.0.99-2.69.0.85-2.33.pth, myrk
BLEU = 73.49, 87.2/77.5/69.3/62.3 (BP=1.000, ratio=1.035, hyp_len=23978, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.276.0.07-1.08.0.10-1.11.0.99-2.69.0.85-2.33.pth, rkmy
BLEU = 74.65, 87.7/78.5/70.4/64.0 (BP=1.000, ratio=1.034, hyp_len=24317, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.277.0.07-1.07.0.09-1.10.0.97-2.64.0.85-2.33.pth, myrk
BLEU = 73.88, 87.6/77.9/69.7/62.6 (BP=1.000, ratio=1.031, hyp_len=23869, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.277.0.07-1.07.0.09-1.10.0.97-2.64.0.85-2.33.pth, rkmy
BLEU = 73.28, 86.9/77.3/68.9/62.3 (BP=1.000, ratio=1.044, hyp_len=24552, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.278.0.07-1.07.0.09-1.09.0.99-2.70.0.84-2.32.pth, myrk
BLEU = 73.79, 87.5/77.8/69.6/62.6 (BP=1.000, ratio=1.031, hyp_len=23885, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.278.0.07-1.07.0.09-1.09.0.99-2.70.0.84-2.32.pth, rkmy
BLEU = 73.95, 87.4/77.9/69.6/63.1 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.279.0.07-1.07.0.08-1.08.1.01-2.74.0.83-2.30.pth, myrk
BLEU = 73.42, 87.1/77.3/69.3/62.3 (BP=1.000, ratio=1.031, hyp_len=23879, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.279.0.07-1.07.0.08-1.08.1.01-2.74.0.83-2.30.pth, rkmy
BLEU = 74.14, 87.5/78.1/69.8/63.3 (BP=1.000, ratio=1.040, hyp_len=24444, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.280.0.07-1.07.0.08-1.08.1.02-2.77.0.83-2.29.pth, myrk
BLEU = 73.37, 87.2/77.3/69.2/62.2 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.280.0.07-1.07.0.08-1.08.1.02-2.77.0.83-2.29.pth, rkmy
BLEU = 73.17, 86.9/77.2/68.8/62.1 (BP=1.000, ratio=1.044, hyp_len=24542, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.28.0.89-2.43.0.90-2.45.1.08-2.95.1.04-2.82.pth, myrk
BLEU = 61.49, 81.5/67.2/55.9/46.7 (BP=1.000, ratio=1.006, hyp_len=23306, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.28.0.89-2.43.0.90-2.45.1.08-2.95.1.04-2.82.pth, rkmy
BLEU = 58.65, 79.7/65.3/52.7/43.1 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.281.0.06-1.07.0.08-1.08.1.00-2.73.0.84-2.31.pth, myrk
BLEU = 73.46, 87.2/77.5/69.2/62.2 (BP=1.000, ratio=1.037, hyp_len=24016, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.281.0.06-1.07.0.08-1.08.1.00-2.73.0.84-2.31.pth, rkmy
BLEU = 74.48, 87.7/78.4/70.2/63.7 (BP=1.000, ratio=1.036, hyp_len=24359, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.282.0.07-1.07.0.07-1.08.1.01-2.75.0.84-2.31.pth, myrk
BLEU = 73.42, 87.2/77.3/69.2/62.2 (BP=1.000, ratio=1.031, hyp_len=23882, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.282.0.07-1.07.0.07-1.08.1.01-2.75.0.84-2.31.pth, rkmy
BLEU = 73.78, 87.4/77.8/69.5/62.7 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.283.0.07-1.07.0.07-1.08.1.01-2.75.0.85-2.33.pth, myrk
BLEU = 73.80, 87.5/77.8/69.6/62.6 (BP=1.000, ratio=1.031, hyp_len=23886, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.283.0.07-1.07.0.07-1.08.1.01-2.75.0.85-2.33.pth, rkmy
BLEU = 72.96, 86.9/77.0/68.5/61.8 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.284.0.06-1.07.0.07-1.07.1.00-2.71.0.86-2.35.pth, myrk
BLEU = 73.63, 87.3/77.6/69.5/62.4 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.284.0.06-1.07.0.07-1.07.1.00-2.71.0.86-2.35.pth, rkmy
BLEU = 73.89, 87.4/77.8/69.5/63.1 (BP=1.000, ratio=1.041, hyp_len=24466, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.285.0.07-1.07.0.08-1.08.1.02-2.77.0.86-2.36.pth, myrk
BLEU = 73.49, 87.2/77.4/69.3/62.4 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.285.0.07-1.07.0.08-1.08.1.02-2.77.0.86-2.36.pth, rkmy
BLEU = 73.76, 87.4/77.8/69.4/62.7 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.286.0.07-1.07.0.09-1.09.1.03-2.79.0.90-2.45.pth, myrk
BLEU = 73.08, 87.0/77.1/68.8/61.8 (BP=1.000, ratio=1.036, hyp_len=24005, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.286.0.07-1.07.0.09-1.09.1.03-2.79.0.90-2.45.pth, rkmy
BLEU = 72.46, 86.7/76.9/68.0/60.8 (BP=1.000, ratio=1.045, hyp_len=24567, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.287.0.10-1.10.0.19-1.20.1.02-2.78.1.02-2.77.pth, myrk
BLEU = 72.99, 86.9/77.0/68.8/61.7 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.287.0.10-1.10.0.19-1.20.1.02-2.78.1.02-2.77.pth, rkmy
BLEU = 71.39, 86.4/75.9/66.8/59.3 (BP=1.000, ratio=1.022, hyp_len=24037, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.288.0.15-1.16.0.17-1.18.1.06-2.88.0.82-2.26.pth, myrk
BLEU = 72.53, 87.0/76.7/68.2/60.8 (BP=1.000, ratio=1.021, hyp_len=23657, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.288.0.15-1.16.0.17-1.18.1.06-2.88.0.82-2.26.pth, rkmy
BLEU = 73.56, 87.2/77.6/69.2/62.5 (BP=1.000, ratio=1.038, hyp_len=24400, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.289.0.12-1.12.0.11-1.12.1.01-2.74.0.84-2.31.pth, myrk
BLEU = 72.40, 86.9/76.6/68.0/60.7 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.289.0.12-1.12.0.11-1.12.1.01-2.74.0.84-2.31.pth, rkmy
BLEU = 72.26, 86.5/76.4/67.7/60.9 (BP=1.000, ratio=1.044, hyp_len=24542, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.290.0.12-1.13.0.09-1.10.1.00-2.71.0.83-2.30.pth, myrk
BLEU = 71.56, 86.1/75.9/67.2/59.7 (BP=1.000, ratio=1.042, hyp_len=24136, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.290.0.12-1.13.0.09-1.10.1.00-2.71.0.83-2.30.pth, rkmy
BLEU = 74.40, 87.8/78.2/70.1/63.6 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.29.0.89-2.43.0.87-2.39.1.04-2.83.0.95-2.59.pth, myrk
BLEU = 61.55, 81.4/67.4/56.0/46.8 (BP=1.000, ratio=1.020, hyp_len=23616, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.29.0.89-2.43.0.87-2.39.1.04-2.83.0.95-2.59.pth, rkmy
BLEU = 62.09, 81.7/68.3/56.4/47.2 (BP=1.000, ratio=1.019, hyp_len=23960, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.291.0.15-1.16.0.08-1.09.0.96-2.62.0.84-2.31.pth, myrk
BLEU = 73.21, 87.1/77.2/69.0/61.9 (BP=1.000, ratio=1.031, hyp_len=23870, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.291.0.15-1.16.0.08-1.09.0.96-2.62.0.84-2.31.pth, rkmy
BLEU = 73.47, 87.1/77.4/69.1/62.6 (BP=1.000, ratio=1.042, hyp_len=24493, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.292.0.12-1.13.0.08-1.08.0.97-2.63.0.83-2.29.pth, myrk
BLEU = 72.78, 87.2/76.9/68.4/61.2 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.292.0.12-1.13.0.08-1.08.0.97-2.63.0.83-2.29.pth, rkmy
BLEU = 73.60, 87.2/77.4/69.2/62.8 (BP=1.000, ratio=1.040, hyp_len=24444, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.293.0.18-1.20.0.08-1.08.0.98-2.65.0.84-2.31.pth, myrk
BLEU = 70.81, 85.7/75.1/66.4/58.9 (BP=1.000, ratio=1.040, hyp_len=24091, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.293.0.18-1.20.0.08-1.08.0.98-2.65.0.84-2.31.pth, rkmy
BLEU = 73.73, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24440, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.294.0.11-1.12.0.07-1.07.0.93-2.54.0.83-2.30.pth, myrk
BLEU = 73.11, 87.0/77.1/68.9/61.9 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.294.0.11-1.12.0.07-1.07.0.93-2.54.0.83-2.30.pth, rkmy
BLEU = 73.93, 87.4/77.8/69.7/63.1 (BP=1.000, ratio=1.040, hyp_len=24439, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.295.0.09-1.10.0.07-1.07.0.94-2.57.0.84-2.32.pth, myrk
BLEU = 73.61, 87.4/77.6/69.4/62.4 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.295.0.09-1.10.0.07-1.07.0.94-2.57.0.84-2.32.pth, rkmy
BLEU = 73.23, 87.0/77.2/68.8/62.2 (BP=1.000, ratio=1.044, hyp_len=24537, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.296.0.07-1.08.0.06-1.07.0.95-2.59.0.87-2.39.pth, myrk
BLEU = 73.00, 87.0/77.1/68.8/61.6 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.296.0.07-1.08.0.06-1.07.0.95-2.59.0.87-2.39.pth, rkmy
BLEU = 74.19, 87.6/78.2/69.9/63.2 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.297.0.08-1.08.0.07-1.07.0.96-2.60.0.86-2.36.pth, myrk
BLEU = 73.24, 87.1/77.2/69.0/61.9 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.297.0.08-1.08.0.07-1.07.0.96-2.60.0.86-2.36.pth, rkmy
BLEU = 74.33, 87.6/78.3/70.1/63.5 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.298.0.07-1.07.0.06-1.07.0.96-2.60.0.86-2.36.pth, myrk
BLEU = 73.99, 87.5/77.9/69.9/62.9 (BP=1.000, ratio=1.031, hyp_len=23879, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.298.0.07-1.07.0.06-1.07.0.96-2.60.0.86-2.36.pth, rkmy
BLEU = 74.10, 87.5/77.9/69.8/63.3 (BP=1.000, ratio=1.040, hyp_len=24445, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.299.0.07-1.07.0.06-1.07.0.94-2.57.0.86-2.37.pth, myrk
BLEU = 73.57, 87.2/77.5/69.4/62.4 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.299.0.07-1.07.0.06-1.07.0.94-2.57.0.86-2.37.pth, rkmy
BLEU = 73.77, 87.2/77.7/69.4/62.9 (BP=1.000, ratio=1.041, hyp_len=24462, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.300.0.07-1.07.0.06-1.07.0.98-2.67.0.86-2.37.pth, myrk
BLEU = 73.58, 87.4/77.5/69.4/62.4 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.300.0.07-1.07.0.06-1.07.0.98-2.67.0.86-2.37.pth, rkmy
BLEU = 74.29, 87.7/78.3/70.0/63.4 (BP=1.000, ratio=1.036, hyp_len=24366, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.30.0.85-2.34.0.84-2.33.1.05-2.85.0.95-2.59.pth, myrk
BLEU = 62.28, 81.6/67.8/56.8/47.9 (BP=1.000, ratio=1.019, hyp_len=23589, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.30.0.85-2.34.0.84-2.33.1.05-2.85.0.95-2.59.pth, rkmy
BLEU = 62.15, 81.8/68.3/56.5/47.3 (BP=1.000, ratio=1.024, hyp_len=24084, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.301.0.06-1.06.0.06-1.06.0.96-2.60.0.86-2.37.pth, myrk
BLEU = 73.66, 87.5/77.7/69.5/62.3 (BP=1.000, ratio=1.032, hyp_len=23894, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.301.0.06-1.06.0.06-1.06.0.96-2.60.0.86-2.37.pth, rkmy
BLEU = 74.21, 87.7/78.2/69.9/63.3 (BP=1.000, ratio=1.037, hyp_len=24370, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.302.0.06-1.07.0.06-1.06.0.97-2.63.0.87-2.38.pth, myrk
BLEU = 73.38, 87.2/77.3/69.2/62.1 (BP=1.000, ratio=1.035, hyp_len=23968, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.302.0.06-1.07.0.06-1.06.0.97-2.63.0.87-2.38.pth, rkmy
BLEU = 73.99, 87.4/77.9/69.7/63.2 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.303.0.06-1.07.0.06-1.07.0.97-2.64.0.87-2.38.pth, myrk
BLEU = 73.87, 87.5/77.8/69.7/62.7 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.303.0.06-1.07.0.06-1.07.0.97-2.64.0.87-2.38.pth, rkmy
BLEU = 74.34, 87.6/78.2/70.1/63.6 (BP=1.000, ratio=1.037, hyp_len=24380, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.304.0.06-1.06.0.06-1.07.0.98-2.65.0.88-2.40.pth, myrk
BLEU = 73.64, 87.3/77.5/69.5/62.5 (BP=1.000, ratio=1.034, hyp_len=23946, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.304.0.06-1.06.0.06-1.07.0.98-2.65.0.88-2.40.pth, rkmy
BLEU = 73.74, 87.4/77.9/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24460, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.305.0.06-1.06.0.06-1.07.0.98-2.68.0.90-2.45.pth, myrk
BLEU = 73.47, 87.3/77.5/69.3/62.2 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.305.0.06-1.06.0.06-1.07.0.98-2.68.0.90-2.45.pth, rkmy
BLEU = 74.04, 87.5/78.1/69.7/63.1 (BP=1.000, ratio=1.039, hyp_len=24424, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.306.0.06-1.06.0.06-1.06.0.98-2.68.0.90-2.47.pth, myrk
BLEU = 73.51, 87.3/77.5/69.3/62.3 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.306.0.06-1.06.0.06-1.06.0.98-2.68.0.90-2.47.pth, rkmy
BLEU = 74.01, 87.5/78.0/69.7/63.1 (BP=1.000, ratio=1.040, hyp_len=24456, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.307.0.06-1.06.0.06-1.06.1.00-2.71.0.89-2.44.pth, myrk
BLEU = 73.75, 87.4/77.7/69.6/62.6 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.307.0.06-1.06.0.06-1.06.1.00-2.71.0.89-2.44.pth, rkmy
BLEU = 73.86, 87.4/77.9/69.5/62.8 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.308.0.06-1.06.0.06-1.06.1.00-2.72.0.89-2.44.pth, myrk
BLEU = 73.92, 87.5/77.8/69.8/62.9 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.308.0.06-1.06.0.06-1.06.1.00-2.72.0.89-2.44.pth, rkmy
BLEU = 73.96, 87.4/77.9/69.7/63.1 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.309.0.06-1.06.0.07-1.07.1.00-2.72.0.92-2.51.pth, myrk
BLEU = 73.11, 87.0/77.1/68.9/61.8 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.309.0.06-1.06.0.07-1.07.1.00-2.72.0.92-2.51.pth, rkmy
BLEU = 73.93, 87.3/77.9/69.6/63.1 (BP=1.000, ratio=1.035, hyp_len=24343, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.310.0.07-1.07.0.12-1.13.1.00-2.71.0.91-2.48.pth, myrk
BLEU = 73.01, 87.0/77.0/68.8/61.7 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.310.0.07-1.07.0.12-1.13.1.00-2.71.0.91-2.48.pth, rkmy
BLEU = 73.44, 87.1/77.5/69.1/62.4 (BP=1.000, ratio=1.039, hyp_len=24427, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.31.0.81-2.26.0.84-2.31.0.99-2.68.0.94-2.56.pth, myrk
BLEU = 64.68, 83.3/70.0/59.4/50.6 (BP=1.000, ratio=1.012, hyp_len=23438, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.31.0.81-2.26.0.84-2.31.0.99-2.68.0.94-2.56.pth, rkmy
BLEU = 63.64, 82.7/69.6/58.0/49.1 (BP=1.000, ratio=1.018, hyp_len=23938, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.311.0.07-1.07.0.13-1.14.1.02-2.76.0.88-2.42.pth, myrk
BLEU = 73.52, 87.1/77.4/69.4/62.4 (BP=1.000, ratio=1.032, hyp_len=23900, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.311.0.07-1.07.0.13-1.14.1.02-2.76.0.88-2.42.pth, rkmy
BLEU = 73.42, 87.2/77.5/69.1/62.3 (BP=1.000, ratio=1.037, hyp_len=24386, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.312.0.06-1.06.0.11-1.12.1.00-2.72.0.88-2.42.pth, myrk
BLEU = 73.55, 87.4/77.5/69.3/62.3 (BP=1.000, ratio=1.035, hyp_len=23961, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.312.0.06-1.06.0.11-1.12.1.00-2.72.0.88-2.42.pth, rkmy
BLEU = 73.37, 87.1/77.4/69.0/62.3 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.313.0.06-1.06.0.09-1.09.1.01-2.75.0.88-2.41.pth, myrk
BLEU = 73.57, 87.5/77.6/69.3/62.2 (BP=1.000, ratio=1.030, hyp_len=23855, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.313.0.06-1.06.0.09-1.09.1.01-2.75.0.88-2.41.pth, rkmy
BLEU = 73.34, 87.1/77.4/68.9/62.2 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.314.0.06-1.06.0.08-1.09.1.00-2.72.0.87-2.39.pth, myrk
BLEU = 73.31, 87.2/77.3/69.1/62.1 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.314.0.06-1.06.0.08-1.09.1.00-2.72.0.87-2.39.pth, rkmy
BLEU = 73.96, 87.4/78.0/69.6/63.0 (BP=1.000, ratio=1.036, hyp_len=24352, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.315.0.06-1.06.0.08-1.08.1.00-2.73.0.87-2.39.pth, myrk
BLEU = 73.06, 87.0/77.1/68.8/61.7 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.315.0.06-1.06.0.08-1.08.1.00-2.73.0.87-2.39.pth, rkmy
BLEU = 73.28, 87.1/77.4/68.9/62.2 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.316.0.06-1.06.0.07-1.08.1.00-2.73.0.90-2.46.pth, myrk
BLEU = 73.40, 87.4/77.4/69.1/62.1 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.316.0.06-1.06.0.07-1.08.1.00-2.73.0.90-2.46.pth, rkmy
BLEU = 74.20, 87.6/78.2/69.9/63.3 (BP=1.000, ratio=1.037, hyp_len=24381, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.317.0.06-1.06.0.07-1.07.1.02-2.78.0.89-2.43.pth, myrk
BLEU = 73.13, 87.0/77.1/68.9/61.8 (BP=1.000, ratio=1.035, hyp_len=23964, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.317.0.06-1.06.0.07-1.07.1.02-2.78.0.89-2.43.pth, rkmy
BLEU = 73.80, 87.4/77.9/69.5/62.7 (BP=1.000, ratio=1.040, hyp_len=24454, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.318.0.06-1.06.0.06-1.07.1.02-2.78.0.91-2.47.pth, myrk
BLEU = 74.11, 87.6/77.9/70.0/63.1 (BP=1.000, ratio=1.031, hyp_len=23871, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.318.0.06-1.06.0.06-1.07.1.02-2.78.0.91-2.47.pth, rkmy
BLEU = 74.43, 87.6/78.4/70.2/63.7 (BP=1.000, ratio=1.037, hyp_len=24375, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.319.0.06-1.06.0.06-1.07.1.02-2.78.0.90-2.45.pth, myrk
BLEU = 73.59, 87.2/77.5/69.4/62.5 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.319.0.06-1.06.0.06-1.07.1.02-2.78.0.90-2.45.pth, rkmy
BLEU = 74.15, 87.7/78.1/69.8/63.3 (BP=1.000, ratio=1.037, hyp_len=24383, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.320.0.05-1.06.0.06-1.06.1.03-2.81.0.88-2.41.pth, myrk
BLEU = 73.12, 87.2/77.2/68.9/61.6 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.320.0.05-1.06.0.06-1.06.1.03-2.81.0.88-2.41.pth, rkmy
BLEU = 74.82, 88.1/78.7/70.5/64.1 (BP=1.000, ratio=1.032, hyp_len=24269, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.32.0.80-2.22.0.78-2.18.1.06-2.90.0.93-2.54.pth, myrk
BLEU = 62.43, 81.9/67.9/56.9/48.0 (BP=1.000, ratio=1.006, hyp_len=23303, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.32.0.80-2.22.0.78-2.18.1.06-2.90.0.93-2.54.pth, rkmy
BLEU = 65.49, 83.7/71.1/60.1/51.4 (BP=1.000, ratio=1.009, hyp_len=23723, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.321.0.06-1.06.0.06-1.06.1.01-2.75.0.89-2.44.pth, myrk
BLEU = 73.25, 87.2/77.3/69.0/61.9 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.321.0.06-1.06.0.06-1.06.1.01-2.75.0.89-2.44.pth, rkmy
BLEU = 74.06, 87.4/78.0/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.322.0.06-1.06.0.06-1.07.1.04-2.84.0.91-2.49.pth, myrk
BLEU = 73.51, 87.3/77.5/69.3/62.2 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.322.0.06-1.06.0.06-1.07.1.04-2.84.0.91-2.49.pth, rkmy
BLEU = 73.86, 87.3/77.8/69.5/62.9 (BP=1.000, ratio=1.038, hyp_len=24409, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.323.0.06-1.07.0.07-1.07.1.04-2.83.0.90-2.47.pth, myrk
BLEU = 73.06, 87.1/77.1/68.8/61.7 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.323.0.06-1.07.0.07-1.07.1.04-2.83.0.90-2.47.pth, rkmy
BLEU = 74.10, 87.6/78.1/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24412, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.324.0.06-1.06.0.06-1.06.1.05-2.85.0.90-2.47.pth, myrk
BLEU = 73.30, 87.3/77.4/69.1/61.9 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.324.0.06-1.06.0.06-1.06.1.05-2.85.0.90-2.47.pth, rkmy
BLEU = 73.87, 87.5/78.0/69.5/62.8 (BP=1.000, ratio=1.038, hyp_len=24407, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.325.0.06-1.06.0.06-1.06.1.05-2.86.0.90-2.46.pth, myrk
BLEU = 73.18, 87.3/77.3/68.9/61.7 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.325.0.06-1.06.0.06-1.06.1.05-2.86.0.90-2.46.pth, rkmy
BLEU = 73.79, 87.4/77.8/69.5/62.8 (BP=1.000, ratio=1.040, hyp_len=24456, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.326.0.06-1.06.0.06-1.06.1.04-2.83.0.93-2.52.pth, myrk
BLEU = 73.07, 87.1/77.1/68.8/61.6 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.326.0.06-1.06.0.06-1.06.1.04-2.83.0.93-2.52.pth, rkmy
BLEU = 73.25, 87.0/77.4/68.9/62.0 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.327.0.06-1.06.0.06-1.06.1.05-2.86.0.91-2.47.pth, myrk
BLEU = 73.37, 87.4/77.4/69.1/61.9 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.327.0.06-1.06.0.06-1.06.1.05-2.86.0.91-2.47.pth, rkmy
BLEU = 73.81, 87.3/77.8/69.5/62.9 (BP=1.000, ratio=1.039, hyp_len=24434, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.328.0.07-1.07.0.06-1.07.1.05-2.85.0.92-2.50.pth, myrk
BLEU = 72.93, 87.0/77.0/68.7/61.5 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.328.0.07-1.07.0.06-1.07.1.05-2.85.0.92-2.50.pth, rkmy
BLEU = 73.86, 87.4/77.8/69.5/62.9 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.329.0.07-1.07.0.06-1.07.1.06-2.90.0.92-2.51.pth, myrk
BLEU = 72.93, 87.0/77.1/68.7/61.5 (BP=1.000, ratio=1.037, hyp_len=24009, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.329.0.07-1.07.0.06-1.07.1.06-2.90.0.92-2.51.pth, rkmy
BLEU = 74.53, 87.8/78.4/70.2/63.8 (BP=1.000, ratio=1.034, hyp_len=24299, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.330.0.07-1.07.0.06-1.06.1.04-2.82.0.93-2.53.pth, myrk
BLEU = 73.24, 87.3/77.2/69.0/61.9 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.330.0.07-1.07.0.06-1.06.1.04-2.82.0.93-2.53.pth, rkmy
BLEU = 73.82, 87.4/77.8/69.5/62.9 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.33.0.92-2.51.0.81-2.24.0.96-2.62.0.91-2.49.pth, myrk
BLEU = 64.36, 82.9/69.8/59.1/50.1 (BP=1.000, ratio=1.019, hyp_len=23591, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.33.0.92-2.51.0.81-2.24.0.96-2.62.0.91-2.49.pth, rkmy
BLEU = 65.34, 83.4/71.0/60.0/51.4 (BP=1.000, ratio=1.022, hyp_len=24017, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.331.0.06-1.06.0.06-1.06.1.07-2.92.0.91-2.47.pth, myrk
BLEU = 73.52, 87.2/77.4/69.3/62.4 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.331.0.06-1.06.0.06-1.06.1.07-2.92.0.91-2.47.pth, rkmy
BLEU = 73.56, 87.1/77.4/69.2/62.7 (BP=1.000, ratio=1.041, hyp_len=24465, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.332.0.06-1.06.0.06-1.06.1.08-2.94.0.93-2.54.pth, myrk
BLEU = 73.21, 87.2/77.2/69.0/61.8 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.332.0.06-1.06.0.06-1.06.1.08-2.94.0.93-2.54.pth, rkmy
BLEU = 73.21, 87.1/77.4/68.8/62.0 (BP=1.000, ratio=1.042, hyp_len=24488, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.333.0.06-1.07.0.06-1.06.1.06-2.88.0.91-2.48.pth, myrk
BLEU = 73.11, 87.2/77.1/68.8/61.7 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.333.0.06-1.07.0.06-1.06.1.06-2.88.0.91-2.48.pth, rkmy
BLEU = 74.34, 87.6/78.3/70.1/63.5 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.334.0.07-1.08.0.06-1.06.1.09-2.97.0.92-2.52.pth, myrk
BLEU = 72.56, 86.8/76.8/68.3/61.0 (BP=1.000, ratio=1.038, hyp_len=24032, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.334.0.07-1.08.0.06-1.06.1.09-2.97.0.92-2.52.pth, rkmy
BLEU = 73.91, 87.4/77.9/69.6/63.0 (BP=1.000, ratio=1.037, hyp_len=24388, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.335.0.08-1.08.0.06-1.06.1.05-2.87.0.94-2.56.pth, myrk
BLEU = 72.41, 86.8/76.6/68.1/60.7 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.335.0.08-1.08.0.06-1.06.1.05-2.87.0.94-2.56.pth, rkmy
BLEU = 74.49, 87.7/78.4/70.2/63.7 (BP=1.000, ratio=1.036, hyp_len=24349, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.336.0.08-1.08.0.06-1.06.1.07-2.91.0.96-2.60.pth, myrk
BLEU = 73.46, 87.3/77.5/69.2/62.2 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.336.0.08-1.08.0.06-1.06.1.07-2.91.0.96-2.60.pth, rkmy
BLEU = 74.49, 87.8/78.4/70.2/63.7 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.337.0.07-1.07.0.06-1.06.1.05-2.85.0.95-2.58.pth, myrk
BLEU = 73.20, 87.2/77.3/68.9/61.8 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.337.0.07-1.07.0.06-1.06.1.05-2.85.0.95-2.58.pth, rkmy
BLEU = 74.42, 87.8/78.4/70.1/63.6 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.338.0.07-1.07.0.07-1.07.1.07-2.93.0.95-2.58.pth, myrk
BLEU = 73.27, 87.3/77.4/69.0/61.8 (BP=1.000, ratio=1.034, hyp_len=23945, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.338.0.07-1.07.0.07-1.07.1.07-2.93.0.95-2.58.pth, rkmy
BLEU = 73.54, 87.2/77.6/69.2/62.5 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.339.0.06-1.06.0.06-1.06.1.06-2.88.0.94-2.56.pth, myrk
BLEU = 73.90, 87.6/77.9/69.7/62.7 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.339.0.06-1.06.0.06-1.06.1.06-2.88.0.94-2.56.pth, rkmy
BLEU = 74.39, 87.8/78.4/70.1/63.4 (BP=1.000, ratio=1.035, hyp_len=24334, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.340.0.06-1.06.0.06-1.06.1.08-2.95.0.93-2.53.pth, myrk
BLEU = 73.39, 87.3/77.4/69.2/62.1 (BP=1.000, ratio=1.035, hyp_len=23969, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.340.0.06-1.06.0.06-1.06.1.08-2.95.0.93-2.53.pth, rkmy
BLEU = 74.13, 87.7/78.1/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24353, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.34.0.73-2.07.0.73-2.08.0.92-2.50.0.87-2.38.pth, myrk
BLEU = 66.29, 83.8/71.3/61.2/52.8 (BP=1.000, ratio=1.014, hyp_len=23482, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.34.0.73-2.07.0.73-2.08.0.92-2.50.0.87-2.38.pth, rkmy
BLEU = 65.42, 83.4/71.1/60.0/51.5 (BP=1.000, ratio=1.024, hyp_len=24072, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.341.0.06-1.06.0.06-1.06.1.05-2.85.0.93-2.54.pth, myrk
BLEU = 73.59, 87.4/77.6/69.4/62.3 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.341.0.06-1.06.0.06-1.06.1.05-2.85.0.93-2.54.pth, rkmy
BLEU = 72.70, 86.8/77.0/68.2/61.3 (BP=1.000, ratio=1.043, hyp_len=24527, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.342.0.06-1.06.0.10-1.10.1.05-2.87.0.93-2.54.pth, myrk
BLEU = 73.35, 87.4/77.4/69.1/61.9 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.342.0.06-1.06.0.10-1.10.1.05-2.87.0.93-2.54.pth, rkmy
BLEU = 73.12, 87.0/77.3/68.8/61.8 (BP=1.000, ratio=1.039, hyp_len=24416, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.343.0.06-1.06.0.09-1.09.1.07-2.91.0.93-2.54.pth, myrk
BLEU = 73.58, 87.5/77.6/69.4/62.3 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.343.0.06-1.06.0.09-1.09.1.07-2.91.0.93-2.54.pth, rkmy
BLEU = 74.04, 87.5/78.0/69.8/63.1 (BP=1.000, ratio=1.034, hyp_len=24305, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.344.0.10-1.10.0.16-1.17.1.10-3.02.0.99-2.69.pth, myrk
BLEU = 72.39, 86.7/76.5/68.0/60.9 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.344.0.10-1.10.0.16-1.17.1.10-3.02.0.99-2.69.pth, rkmy
BLEU = 74.20, 87.9/78.3/69.8/63.1 (BP=1.000, ratio=1.019, hyp_len=23948, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.345.0.09-1.10.0.13-1.14.1.11-3.02.0.93-2.52.pth, myrk
BLEU = 72.53, 86.8/76.6/68.3/61.0 (BP=1.000, ratio=1.038, hyp_len=24034, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.345.0.09-1.10.0.13-1.14.1.11-3.02.0.93-2.52.pth, rkmy
BLEU = 73.21, 87.0/77.2/68.8/62.1 (BP=1.000, ratio=1.039, hyp_len=24420, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.346.0.09-1.09.0.09-1.09.1.09-2.97.0.91-2.47.pth, myrk
BLEU = 72.58, 86.9/76.7/68.3/61.0 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.346.0.09-1.09.0.09-1.09.1.09-2.97.0.91-2.47.pth, rkmy
BLEU = 73.62, 87.3/77.6/69.3/62.6 (BP=1.000, ratio=1.039, hyp_len=24430, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.347.0.12-1.13.0.09-1.10.1.10-3.00.0.91-2.50.pth, myrk
BLEU = 70.71, 85.9/75.2/66.2/58.5 (BP=1.000, ratio=1.038, hyp_len=24041, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.347.0.12-1.13.0.09-1.10.1.10-3.00.0.91-2.50.pth, rkmy
BLEU = 72.57, 86.8/76.8/68.1/61.2 (BP=1.000, ratio=1.039, hyp_len=24422, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.348.0.11-1.12.0.10-1.11.1.04-2.83.0.97-2.64.pth, myrk
BLEU = 72.36, 86.7/76.5/68.0/60.8 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.348.0.11-1.12.0.10-1.11.1.04-2.83.0.97-2.64.pth, rkmy
BLEU = 73.06, 87.1/77.1/68.6/61.8 (BP=1.000, ratio=1.035, hyp_len=24340, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.349.0.10-1.11.0.13-1.14.1.03-2.80.0.94-2.57.pth, myrk
BLEU = 71.95, 86.6/76.2/67.5/60.1 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.349.0.10-1.11.0.13-1.14.1.03-2.80.0.94-2.57.pth, rkmy
BLEU = 73.03, 87.1/77.3/68.6/61.6 (BP=1.000, ratio=1.035, hyp_len=24323, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.350.0.11-1.12.0.10-1.11.1.04-2.82.0.91-2.49.pth, myrk
BLEU = 71.20, 86.2/75.6/66.7/59.1 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.350.0.11-1.12.0.10-1.11.1.04-2.82.0.91-2.49.pth, rkmy
BLEU = 73.50, 87.3/77.6/69.1/62.4 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.35.0.72-2.05.0.77-2.16.0.88-2.42.0.87-2.40.pth, myrk
BLEU = 68.11, 84.8/73.0/63.2/54.9 (BP=1.000, ratio=1.015, hyp_len=23502, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.35.0.72-2.05.0.77-2.16.0.88-2.42.0.87-2.40.pth, rkmy
BLEU = 65.58, 83.4/71.1/60.2/51.8 (BP=1.000, ratio=1.028, hyp_len=24166, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.351.0.11-1.12.0.10-1.10.1.04-2.83.0.93-2.53.pth, myrk
BLEU = 72.60, 87.0/76.7/68.2/61.0 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.351.0.11-1.12.0.10-1.10.1.04-2.83.0.93-2.53.pth, rkmy
BLEU = 72.72, 86.7/76.9/68.3/61.4 (BP=1.000, ratio=1.040, hyp_len=24441, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.352.0.10-1.10.0.08-1.09.1.05-2.86.0.90-2.47.pth, myrk
BLEU = 72.34, 86.8/76.5/67.9/60.7 (BP=1.000, ratio=1.033, hyp_len=23922, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.352.0.10-1.10.0.08-1.09.1.05-2.86.0.90-2.47.pth, rkmy
BLEU = 73.57, 87.2/77.6/69.2/62.6 (BP=1.000, ratio=1.038, hyp_len=24395, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.353.0.08-1.08.0.08-1.09.1.03-2.80.0.95-2.58.pth, myrk
BLEU = 73.05, 87.1/77.1/68.8/61.6 (BP=1.000, ratio=1.031, hyp_len=23870, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.353.0.08-1.08.0.08-1.09.1.03-2.80.0.95-2.58.pth, rkmy
BLEU = 71.36, 86.0/75.8/66.8/59.6 (BP=1.000, ratio=1.048, hyp_len=24635, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.354.0.09-1.09.0.10-1.11.1.03-2.81.0.92-2.52.pth, myrk
BLEU = 73.94, 87.6/77.9/69.8/62.8 (BP=1.000, ratio=1.030, hyp_len=23846, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.354.0.09-1.09.0.10-1.11.1.03-2.81.0.92-2.52.pth, rkmy
BLEU = 73.60, 87.2/77.6/69.2/62.6 (BP=1.000, ratio=1.038, hyp_len=24414, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.355.0.07-1.07.0.08-1.08.1.03-2.81.0.92-2.51.pth, myrk
BLEU = 73.30, 87.3/77.3/69.0/62.0 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.355.0.07-1.07.0.08-1.08.1.03-2.81.0.92-2.51.pth, rkmy
BLEU = 73.73, 87.3/77.8/69.4/62.6 (BP=1.000, ratio=1.038, hyp_len=24404, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.356.0.06-1.07.0.07-1.07.1.04-2.83.0.92-2.50.pth, myrk
BLEU = 73.18, 87.1/77.2/68.9/61.9 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.356.0.06-1.07.0.07-1.07.1.04-2.83.0.92-2.50.pth, rkmy
BLEU = 74.29, 87.8/78.3/70.0/63.3 (BP=1.000, ratio=1.036, hyp_len=24346, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.357.0.06-1.06.0.06-1.06.1.03-2.80.0.91-2.49.pth, myrk
BLEU = 73.24, 87.2/77.3/69.0/61.9 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.357.0.06-1.06.0.06-1.06.1.03-2.80.0.91-2.49.pth, rkmy
BLEU = 74.48, 87.7/78.4/70.2/63.7 (BP=1.000, ratio=1.035, hyp_len=24328, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.358.0.06-1.06.0.06-1.06.1.03-2.80.0.92-2.51.pth, myrk
BLEU = 73.88, 87.6/77.9/69.7/62.6 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.358.0.06-1.06.0.06-1.06.1.03-2.80.0.92-2.51.pth, rkmy
BLEU = 73.69, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.359.0.05-1.06.0.06-1.06.1.05-2.86.0.91-2.49.pth, myrk
BLEU = 73.53, 87.4/77.6/69.3/62.2 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.359.0.05-1.06.0.06-1.06.1.05-2.86.0.91-2.49.pth, rkmy
BLEU = 73.64, 87.3/77.6/69.3/62.7 (BP=1.000, ratio=1.040, hyp_len=24442, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.360.0.05-1.06.0.06-1.06.1.04-2.83.0.92-2.52.pth, myrk
BLEU = 73.22, 87.2/77.3/69.0/61.8 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.360.0.05-1.06.0.06-1.06.1.04-2.83.0.92-2.52.pth, rkmy
BLEU = 74.08, 87.6/78.1/69.8/63.1 (BP=1.000, ratio=1.038, hyp_len=24402, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.36.0.66-1.94.0.70-2.00.0.87-2.39.0.84-2.32.pth, myrk
BLEU = 68.49, 84.9/73.3/63.7/55.6 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.36.0.66-1.94.0.70-2.00.0.87-2.39.0.84-2.32.pth, rkmy
BLEU = 68.32, 84.9/73.5/63.2/55.2 (BP=1.000, ratio=1.020, hyp_len=23972, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.361.0.06-1.06.0.06-1.06.1.03-2.79.0.93-2.54.pth, myrk
BLEU = 73.45, 87.2/77.4/69.2/62.2 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.361.0.06-1.06.0.06-1.06.1.03-2.79.0.93-2.54.pth, rkmy
BLEU = 74.46, 87.7/78.4/70.2/63.6 (BP=1.000, ratio=1.035, hyp_len=24321, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.362.0.06-1.06.0.06-1.06.1.02-2.79.0.94-2.55.pth, myrk
BLEU = 73.56, 87.3/77.6/69.4/62.4 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.362.0.06-1.06.0.06-1.06.1.02-2.79.0.94-2.55.pth, rkmy
BLEU = 73.05, 87.1/77.2/68.6/61.8 (BP=1.000, ratio=1.042, hyp_len=24491, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.363.0.06-1.06.0.06-1.06.1.04-2.83.0.92-2.50.pth, myrk
BLEU = 73.73, 87.5/77.7/69.5/62.6 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.363.0.06-1.06.0.06-1.06.1.04-2.83.0.92-2.50.pth, rkmy
BLEU = 74.06, 87.4/78.1/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24392, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.364.0.05-1.05.0.06-1.06.1.06-2.88.0.93-2.52.pth, myrk
BLEU = 73.78, 87.4/77.7/69.6/62.7 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.364.0.05-1.05.0.06-1.06.1.06-2.88.0.93-2.52.pth, rkmy
BLEU = 73.91, 87.4/77.9/69.6/62.9 (BP=1.000, ratio=1.040, hyp_len=24441, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.365.0.05-1.06.0.06-1.06.1.05-2.85.0.93-2.53.pth, myrk
BLEU = 73.86, 87.5/77.8/69.7/62.8 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.365.0.05-1.06.0.06-1.06.1.05-2.85.0.93-2.53.pth, rkmy
BLEU = 74.05, 87.5/78.0/69.8/63.1 (BP=1.000, ratio=1.039, hyp_len=24425, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.366.0.05-1.05.0.06-1.06.1.04-2.82.0.93-2.54.pth, myrk
BLEU = 73.30, 87.3/77.3/69.0/62.0 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.366.0.05-1.05.0.06-1.06.1.04-2.82.0.93-2.54.pth, rkmy
BLEU = 74.68, 87.9/78.6/70.5/63.9 (BP=1.000, ratio=1.035, hyp_len=24323, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.367.0.05-1.05.0.05-1.05.1.04-2.82.0.94-2.57.pth, myrk
BLEU = 73.88, 87.5/77.8/69.7/62.8 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.367.0.05-1.05.0.05-1.05.1.04-2.82.0.94-2.57.pth, rkmy
BLEU = 74.30, 87.6/78.2/70.1/63.5 (BP=1.000, ratio=1.035, hyp_len=24336, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.368.0.05-1.05.0.06-1.06.1.04-2.84.0.95-2.58.pth, myrk
BLEU = 73.72, 87.5/77.7/69.5/62.5 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.368.0.05-1.05.0.06-1.06.1.04-2.84.0.95-2.58.pth, rkmy
BLEU = 73.13, 86.9/77.2/68.8/62.0 (BP=1.000, ratio=1.042, hyp_len=24490, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.369.0.05-1.05.0.06-1.07.1.04-2.82.0.92-2.52.pth, myrk
BLEU = 73.89, 87.6/77.9/69.7/62.7 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.369.0.05-1.05.0.06-1.07.1.04-2.82.0.92-2.52.pth, rkmy
BLEU = 74.56, 87.8/78.6/70.3/63.7 (BP=1.000, ratio=1.033, hyp_len=24286, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.370.0.05-1.05.0.06-1.06.1.05-2.87.0.94-2.56.pth, myrk
BLEU = 73.73, 87.6/77.7/69.5/62.5 (BP=1.000, ratio=1.030, hyp_len=23848, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.370.0.05-1.05.0.06-1.06.1.05-2.87.0.94-2.56.pth, rkmy
BLEU = 73.74, 87.3/77.8/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24460, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.37.0.67-1.95.0.70-2.02.0.85-2.35.0.88-2.42.pth, myrk
BLEU = 69.47, 85.8/74.2/64.7/56.6 (BP=1.000, ratio=1.010, hyp_len=23382, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.37.0.67-1.95.0.70-2.02.0.85-2.35.0.88-2.42.pth, rkmy
BLEU = 65.98, 83.5/71.4/60.7/52.3 (BP=1.000, ratio=1.034, hyp_len=24317, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.371.0.05-1.05.0.05-1.05.1.05-2.86.0.95-2.58.pth, myrk
BLEU = 73.69, 87.5/77.6/69.5/62.5 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.371.0.05-1.05.0.05-1.05.1.05-2.86.0.95-2.58.pth, rkmy
BLEU = 74.09, 87.5/78.1/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24394, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.372.0.05-1.05.0.05-1.05.1.07-2.90.0.95-2.58.pth, myrk
BLEU = 73.52, 87.3/77.5/69.3/62.2 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.372.0.05-1.05.0.05-1.05.1.07-2.90.0.95-2.58.pth, rkmy
BLEU = 74.39, 87.7/78.3/70.1/63.6 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.373.0.05-1.05.0.05-1.05.1.05-2.85.0.95-2.57.pth, myrk
BLEU = 73.44, 87.3/77.5/69.2/62.1 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.373.0.05-1.05.0.05-1.05.1.05-2.85.0.95-2.57.pth, rkmy
BLEU = 73.81, 87.5/77.9/69.5/62.7 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.374.0.05-1.05.0.06-1.06.1.06-2.89.0.95-2.58.pth, myrk
BLEU = 73.59, 87.4/77.6/69.4/62.4 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.374.0.05-1.05.0.06-1.06.1.06-2.89.0.95-2.58.pth, rkmy
BLEU = 74.29, 87.6/78.2/70.0/63.5 (BP=1.000, ratio=1.038, hyp_len=24402, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.375.0.05-1.05.0.05-1.06.1.07-2.93.0.97-2.63.pth, myrk
BLEU = 73.47, 87.3/77.5/69.3/62.1 (BP=1.000, ratio=1.035, hyp_len=23968, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.375.0.05-1.05.0.05-1.06.1.07-2.93.0.97-2.63.pth, rkmy
BLEU = 73.64, 87.2/77.7/69.3/62.6 (BP=1.000, ratio=1.040, hyp_len=24459, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.376.0.05-1.05.0.05-1.05.1.08-2.95.0.95-2.59.pth, myrk
BLEU = 73.39, 87.2/77.3/69.2/62.2 (BP=1.000, ratio=1.034, hyp_len=23946, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.376.0.05-1.05.0.05-1.05.1.08-2.95.0.95-2.59.pth, rkmy
BLEU = 73.94, 87.4/77.9/69.6/63.0 (BP=1.000, ratio=1.037, hyp_len=24374, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.377.0.05-1.05.0.05-1.05.1.08-2.93.0.97-2.63.pth, myrk
BLEU = 73.83, 87.6/77.8/69.6/62.6 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.377.0.05-1.05.0.05-1.05.1.08-2.93.0.97-2.63.pth, rkmy
BLEU = 74.10, 87.5/78.1/69.8/63.2 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.378.0.06-1.06.0.06-1.06.1.06-2.88.0.97-2.63.pth, myrk
BLEU = 73.61, 87.5/77.6/69.4/62.3 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.378.0.06-1.06.0.06-1.06.1.06-2.88.0.97-2.63.pth, rkmy
BLEU = 73.98, 87.5/78.0/69.7/63.0 (BP=1.000, ratio=1.037, hyp_len=24370, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.379.0.06-1.07.0.11-1.12.1.06-2.89.0.98-2.67.pth, myrk
BLEU = 73.53, 87.3/77.5/69.3/62.4 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.379.0.06-1.07.0.11-1.12.1.06-2.89.0.98-2.67.pth, rkmy
BLEU = 74.30, 87.8/78.3/69.9/63.4 (BP=1.000, ratio=1.027, hyp_len=24148, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.380.0.07-1.08.0.13-1.14.1.05-2.85.0.98-2.67.pth, myrk
BLEU = 73.71, 87.5/77.6/69.5/62.6 (BP=1.000, ratio=1.030, hyp_len=23855, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.380.0.07-1.08.0.13-1.14.1.05-2.85.0.98-2.67.pth, rkmy
BLEU = 72.44, 86.9/76.8/67.9/60.7 (BP=1.000, ratio=1.024, hyp_len=24069, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.38.0.60-1.83.0.61-1.85.0.86-2.35.0.85-2.34.pth, myrk
BLEU = 68.63, 85.1/73.5/63.8/55.6 (BP=1.000, ratio=1.020, hyp_len=23614, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.38.0.60-1.83.0.61-1.85.0.86-2.35.0.85-2.34.pth, rkmy
BLEU = 67.94, 84.9/73.2/62.8/54.6 (BP=1.000, ratio=1.018, hyp_len=23937, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.381.0.07-1.07.0.15-1.16.1.09-2.98.0.97-2.64.pth, myrk
BLEU = 73.27, 87.2/77.3/69.0/62.0 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.381.0.07-1.07.0.15-1.16.1.09-2.98.0.97-2.64.pth, rkmy
BLEU = 73.48, 87.3/77.5/69.1/62.4 (BP=1.000, ratio=1.029, hyp_len=24193, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.382.0.06-1.07.0.09-1.09.1.08-2.95.0.98-2.67.pth, myrk
BLEU = 73.39, 87.2/77.4/69.2/62.1 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.382.0.06-1.07.0.09-1.09.1.08-2.95.0.98-2.67.pth, rkmy
BLEU = 73.26, 87.0/77.2/68.9/62.2 (BP=1.000, ratio=1.041, hyp_len=24474, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.383.0.06-1.06.0.08-1.08.1.06-2.89.0.93-2.54.pth, myrk
BLEU = 73.68, 87.5/77.6/69.4/62.6 (BP=1.000, ratio=1.028, hyp_len=23809, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.383.0.06-1.06.0.08-1.08.1.06-2.89.0.93-2.54.pth, rkmy
BLEU = 73.09, 86.9/77.1/68.7/62.0 (BP=1.000, ratio=1.042, hyp_len=24492, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.384.0.06-1.07.0.07-1.07.1.07-2.93.0.95-2.58.pth, myrk
BLEU = 73.77, 87.5/77.7/69.5/62.7 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.384.0.06-1.07.0.07-1.07.1.07-2.93.0.95-2.58.pth, rkmy
BLEU = 73.68, 87.3/77.7/69.4/62.6 (BP=1.000, ratio=1.040, hyp_len=24444, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.385.0.08-1.08.0.06-1.06.1.05-2.86.0.93-2.54.pth, myrk
BLEU = 72.67, 86.9/76.7/68.3/61.2 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.385.0.08-1.08.0.06-1.06.1.05-2.86.0.93-2.54.pth, rkmy
BLEU = 73.92, 87.4/77.9/69.6/63.0 (BP=1.000, ratio=1.038, hyp_len=24405, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.386.0.07-1.07.0.06-1.06.1.09-2.97.0.93-2.55.pth, myrk
BLEU = 72.42, 86.8/76.6/68.0/60.8 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.386.0.07-1.07.0.06-1.06.1.09-2.97.0.93-2.55.pth, rkmy
BLEU = 74.06, 87.5/78.0/69.8/63.1 (BP=1.000, ratio=1.037, hyp_len=24385, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.387.0.06-1.07.0.05-1.06.1.10-3.00.0.94-2.55.pth, myrk
BLEU = 73.16, 87.1/77.1/68.9/61.9 (BP=1.000, ratio=1.032, hyp_len=23893, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.387.0.06-1.07.0.05-1.06.1.10-3.00.0.94-2.55.pth, rkmy
BLEU = 74.03, 87.6/78.0/69.7/63.0 (BP=1.000, ratio=1.037, hyp_len=24383, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.388.0.06-1.06.0.05-1.05.1.07-2.90.0.93-2.53.pth, myrk
BLEU = 73.80, 87.5/77.7/69.6/62.6 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.388.0.06-1.06.0.05-1.05.1.07-2.90.0.93-2.53.pth, rkmy
BLEU = 73.95, 87.5/78.0/69.6/63.0 (BP=1.000, ratio=1.037, hyp_len=24389, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.389.0.06-1.06.0.05-1.05.1.09-2.98.0.93-2.54.pth, myrk
BLEU = 73.77, 87.5/77.6/69.6/62.7 (BP=1.000, ratio=1.029, hyp_len=23829, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.389.0.06-1.06.0.05-1.05.1.09-2.98.0.93-2.54.pth, rkmy
BLEU = 74.12, 87.6/78.2/69.8/63.1 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.390.0.05-1.06.0.05-1.05.1.08-2.95.0.94-2.55.pth, myrk
BLEU = 73.13, 87.2/77.2/68.9/61.7 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.390.0.05-1.06.0.05-1.05.1.08-2.95.0.94-2.55.pth, rkmy
BLEU = 73.71, 87.3/77.8/69.4/62.6 (BP=1.000, ratio=1.040, hyp_len=24438, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.39.0.63-1.87.0.64-1.90.0.85-2.33.0.82-2.27.pth, myrk
BLEU = 67.73, 84.4/72.6/62.9/54.6 (BP=1.000, ratio=1.018, hyp_len=23578, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.39.0.63-1.87.0.64-1.90.0.85-2.33.0.82-2.27.pth, rkmy
BLEU = 67.97, 84.6/73.3/62.9/54.7 (BP=1.000, ratio=1.031, hyp_len=24230, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.391.0.06-1.06.0.05-1.05.1.06-2.88.0.94-2.55.pth, myrk
BLEU = 73.53, 87.2/77.4/69.3/62.4 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.391.0.06-1.06.0.05-1.05.1.06-2.88.0.94-2.55.pth, rkmy
BLEU = 73.73, 87.3/77.7/69.4/62.8 (BP=1.000, ratio=1.038, hyp_len=24407, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.392.0.06-1.06.0.05-1.05.1.10-2.99.0.95-2.58.pth, myrk
BLEU = 73.57, 87.4/77.6/69.3/62.3 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.392.0.06-1.06.0.05-1.05.1.10-2.99.0.95-2.58.pth, rkmy
BLEU = 74.10, 87.6/78.0/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.393.0.06-1.06.0.05-1.05.1.08-2.95.0.95-2.58.pth, myrk
BLEU = 73.83, 87.5/77.7/69.6/62.8 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.393.0.06-1.06.0.05-1.05.1.08-2.95.0.95-2.58.pth, rkmy
BLEU = 73.74, 87.3/77.7/69.4/62.8 (BP=1.000, ratio=1.040, hyp_len=24445, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.394.0.05-1.05.0.05-1.05.1.10-2.99.0.96-2.61.pth, myrk
BLEU = 73.04, 87.1/77.1/68.8/61.6 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.394.0.05-1.05.0.05-1.05.1.10-2.99.0.96-2.61.pth, rkmy
BLEU = 74.00, 87.4/77.9/69.7/63.2 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.395.0.06-1.06.0.05-1.05.1.09-2.97.0.95-2.59.pth, myrk
BLEU = 74.15, 87.6/78.1/70.0/63.1 (BP=1.000, ratio=1.031, hyp_len=23870, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.395.0.06-1.06.0.05-1.05.1.09-2.97.0.95-2.59.pth, rkmy
BLEU = 73.88, 87.4/77.8/69.6/62.9 (BP=1.000, ratio=1.037, hyp_len=24369, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.396.0.06-1.06.0.05-1.05.1.14-3.12.0.94-2.56.pth, myrk
BLEU = 73.09, 87.0/77.2/68.8/61.7 (BP=1.000, ratio=1.036, hyp_len=23986, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.396.0.06-1.06.0.05-1.05.1.14-3.12.0.94-2.56.pth, rkmy
BLEU = 74.28, 87.6/78.1/70.0/63.6 (BP=1.000, ratio=1.037, hyp_len=24370, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.397.0.05-1.05.0.05-1.05.1.11-3.03.0.94-2.57.pth, myrk
BLEU = 74.17, 87.7/78.0/70.0/63.2 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.397.0.05-1.05.0.05-1.05.1.11-3.03.0.94-2.57.pth, rkmy
BLEU = 73.81, 87.3/77.8/69.5/62.9 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.398.0.05-1.05.0.05-1.05.1.10-3.01.0.97-2.64.pth, myrk
BLEU = 73.56, 87.4/77.5/69.4/62.3 (BP=1.000, ratio=1.033, hyp_len=23919, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.398.0.05-1.05.0.05-1.05.1.10-3.01.0.97-2.64.pth, rkmy
BLEU = 74.31, 87.7/78.3/70.1/63.4 (BP=1.000, ratio=1.036, hyp_len=24345, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.399.0.05-1.05.0.05-1.05.1.09-2.98.0.95-2.59.pth, myrk
BLEU = 73.96, 87.7/77.9/69.7/62.8 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.399.0.05-1.05.0.05-1.05.1.09-2.98.0.95-2.59.pth, rkmy
BLEU = 73.74, 87.4/77.7/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24450, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.400.0.05-1.05.0.05-1.05.1.10-3.01.0.95-2.58.pth, myrk
BLEU = 73.64, 87.3/77.6/69.4/62.5 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.400.0.05-1.05.0.05-1.05.1.10-3.01.0.95-2.58.pth, rkmy
BLEU = 73.67, 87.2/77.7/69.4/62.6 (BP=1.000, ratio=1.039, hyp_len=24435, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.40.0.59-1.80.0.68-1.98.0.81-2.25.0.86-2.36.pth, myrk
BLEU = 69.87, 85.6/74.5/65.2/57.3 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.40.0.59-1.80.0.68-1.98.0.81-2.25.0.86-2.36.pth, rkmy
BLEU = 66.14, 83.5/71.6/60.8/52.6 (BP=1.000, ratio=1.032, hyp_len=24250, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.401.0.05-1.05.0.06-1.06.1.10-2.99.0.96-2.60.pth, myrk
BLEU = 73.27, 87.2/77.2/69.0/62.1 (BP=1.000, ratio=1.035, hyp_len=23967, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.401.0.05-1.05.0.06-1.06.1.10-2.99.0.96-2.60.pth, rkmy
BLEU = 73.28, 87.2/77.4/68.9/62.0 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.402.0.05-1.05.0.05-1.06.1.12-3.06.0.97-2.63.pth, myrk
BLEU = 74.14, 87.7/78.0/69.9/63.2 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.402.0.05-1.05.0.05-1.06.1.12-3.06.0.97-2.63.pth, rkmy
BLEU = 73.20, 87.1/77.4/68.8/61.9 (BP=1.000, ratio=1.040, hyp_len=24450, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.403.0.05-1.05.0.07-1.07.1.12-3.08.0.95-2.60.pth, myrk
BLEU = 73.86, 87.6/77.9/69.6/62.6 (BP=1.000, ratio=1.032, hyp_len=23904, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.403.0.05-1.05.0.07-1.07.1.12-3.08.0.95-2.60.pth, rkmy
BLEU = 73.84, 87.4/77.8/69.5/62.9 (BP=1.000, ratio=1.038, hyp_len=24392, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.404.0.07-1.07.0.06-1.06.1.16-3.19.0.96-2.60.pth, myrk
BLEU = 70.58, 85.8/75.0/66.0/58.4 (BP=1.000, ratio=1.040, hyp_len=24078, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.404.0.07-1.07.0.06-1.06.1.16-3.19.0.96-2.60.pth, rkmy
BLEU = 74.04, 87.6/78.0/69.7/63.1 (BP=1.000, ratio=1.036, hyp_len=24346, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.405.0.11-1.11.0.05-1.05.1.09-2.97.0.96-2.61.pth, myrk
BLEU = 72.05, 86.7/76.3/67.6/60.3 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.405.0.11-1.11.0.05-1.05.1.09-2.97.0.96-2.61.pth, rkmy
BLEU = 73.99, 87.5/78.0/69.7/63.0 (BP=1.000, ratio=1.036, hyp_len=24351, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.406.0.09-1.09.0.05-1.05.1.11-3.02.0.97-2.65.pth, myrk
BLEU = 72.35, 86.7/76.5/68.0/60.8 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.406.0.09-1.09.0.05-1.05.1.11-3.02.0.97-2.65.pth, rkmy
BLEU = 74.48, 87.8/78.5/70.3/63.6 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.407.0.11-1.11.0.05-1.05.1.08-2.93.0.96-2.62.pth, myrk
BLEU = 72.21, 86.6/76.3/67.9/60.6 (BP=1.000, ratio=1.035, hyp_len=23960, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.407.0.11-1.11.0.05-1.05.1.08-2.93.0.96-2.62.pth, rkmy
BLEU = 73.87, 87.4/77.9/69.6/62.9 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.408.0.13-1.14.0.06-1.06.1.08-2.94.0.97-2.64.pth, myrk
BLEU = 72.57, 86.7/76.7/68.2/61.2 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.408.0.13-1.14.0.06-1.06.1.08-2.94.0.97-2.64.pth, rkmy
BLEU = 74.32, 87.6/78.2/70.1/63.5 (BP=1.000, ratio=1.036, hyp_len=24362, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.409.0.09-1.10.0.05-1.05.1.08-2.95.0.97-2.63.pth, myrk
BLEU = 72.57, 86.7/76.7/68.3/61.1 (BP=1.000, ratio=1.035, hyp_len=23962, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.409.0.09-1.10.0.05-1.05.1.08-2.95.0.97-2.63.pth, rkmy
BLEU = 74.16, 87.5/78.1/69.9/63.3 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.410.0.07-1.07.0.05-1.05.1.07-2.93.0.99-2.68.pth, myrk
BLEU = 73.19, 87.1/77.2/69.0/61.9 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.410.0.07-1.07.0.05-1.05.1.07-2.93.0.99-2.68.pth, rkmy
BLEU = 73.90, 87.4/78.0/69.6/62.9 (BP=1.000, ratio=1.037, hyp_len=24387, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.41.0.56-1.76.0.64-1.90.0.83-2.28.0.86-2.35.pth, myrk
BLEU = 68.90, 85.0/73.7/64.1/56.0 (BP=1.000, ratio=1.030, hyp_len=23845, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.41.0.56-1.76.0.64-1.90.0.83-2.28.0.86-2.35.pth, rkmy
BLEU = 67.64, 84.7/73.0/62.5/54.2 (BP=1.000, ratio=1.023, hyp_len=24045, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.411.0.06-1.06.0.05-1.05.1.07-2.93.0.97-2.64.pth, myrk
BLEU = 73.93, 87.5/77.8/69.7/62.9 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.411.0.06-1.06.0.05-1.05.1.07-2.93.0.97-2.64.pth, rkmy
BLEU = 73.78, 87.3/77.8/69.5/62.8 (BP=1.000, ratio=1.039, hyp_len=24419, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.412.0.06-1.06.0.05-1.05.1.07-2.91.0.98-2.66.pth, myrk
BLEU = 74.07, 87.6/77.9/69.9/63.0 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.412.0.06-1.06.0.05-1.05.1.07-2.91.0.98-2.66.pth, rkmy
BLEU = 74.67, 87.8/78.5/70.5/64.0 (BP=1.000, ratio=1.034, hyp_len=24298, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.413.0.05-1.05.0.05-1.05.1.09-2.96.0.96-2.61.pth, myrk
BLEU = 73.73, 87.4/77.7/69.6/62.6 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.413.0.05-1.05.0.05-1.05.1.09-2.96.0.96-2.61.pth, rkmy
BLEU = 74.44, 87.7/78.4/70.2/63.6 (BP=1.000, ratio=1.033, hyp_len=24289, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.414.0.05-1.06.0.06-1.06.1.10-2.99.0.98-2.66.pth, myrk
BLEU = 73.32, 87.3/77.4/69.1/61.9 (BP=1.000, ratio=1.034, hyp_len=23959, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.414.0.05-1.06.0.06-1.06.1.10-2.99.0.98-2.66.pth, rkmy
BLEU = 75.10, 88.0/78.9/71.0/64.6 (BP=1.000, ratio=1.030, hyp_len=24205, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.415.0.06-1.06.0.09-1.10.1.08-2.96.0.97-2.65.pth, myrk
BLEU = 73.28, 87.3/77.3/69.0/61.9 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.415.0.06-1.06.0.09-1.10.1.08-2.96.0.97-2.65.pth, rkmy
BLEU = 72.94, 86.9/77.1/68.5/61.7 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.416.0.06-1.06.0.09-1.10.1.13-3.11.0.96-2.60.pth, myrk
BLEU = 73.50, 87.3/77.5/69.3/62.2 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.416.0.06-1.06.0.09-1.10.1.13-3.11.0.96-2.60.pth, rkmy
BLEU = 72.78, 86.6/76.9/68.4/61.6 (BP=1.000, ratio=1.043, hyp_len=24528, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.417.0.05-1.05.0.07-1.07.1.09-2.98.0.97-2.64.pth, myrk
BLEU = 73.67, 87.4/77.6/69.5/62.5 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.417.0.05-1.05.0.07-1.07.1.09-2.98.0.97-2.64.pth, rkmy
BLEU = 73.85, 87.4/77.9/69.5/62.9 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.418.0.05-1.05.0.07-1.07.1.09-2.98.0.97-2.64.pth, myrk
BLEU = 73.96, 87.6/77.9/69.8/62.8 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.418.0.05-1.05.0.07-1.07.1.09-2.98.0.97-2.64.pth, rkmy
BLEU = 74.50, 87.9/78.4/70.2/63.7 (BP=1.000, ratio=1.034, hyp_len=24302, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.419.0.05-1.05.0.06-1.06.1.10-3.01.0.98-2.66.pth, myrk
BLEU = 73.65, 87.4/77.6/69.5/62.4 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.419.0.05-1.05.0.06-1.06.1.10-3.01.0.98-2.66.pth, rkmy
BLEU = 74.11, 87.6/78.0/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.420.0.05-1.05.0.06-1.06.1.09-2.98.0.99-2.69.pth, myrk
BLEU = 73.74, 87.4/77.7/69.6/62.6 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.420.0.05-1.05.0.06-1.06.1.09-2.98.0.99-2.69.pth, rkmy
BLEU = 73.51, 87.2/77.6/69.1/62.5 (BP=1.000, ratio=1.040, hyp_len=24456, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.42.0.55-1.73.0.60-1.82.0.79-2.19.0.80-2.22.pth, myrk
BLEU = 71.17, 86.3/75.6/66.7/59.0 (BP=1.000, ratio=1.016, hyp_len=23535, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.42.0.55-1.73.0.60-1.82.0.79-2.19.0.80-2.22.pth, rkmy
BLEU = 69.49, 85.5/74.4/64.5/56.8 (BP=1.000, ratio=1.020, hyp_len=23974, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.421.0.05-1.05.0.06-1.06.1.10-2.99.0.98-2.66.pth, myrk
BLEU = 73.71, 87.4/77.7/69.5/62.5 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.421.0.05-1.05.0.06-1.06.1.10-2.99.0.98-2.66.pth, rkmy
BLEU = 74.29, 87.7/78.2/70.0/63.5 (BP=1.000, ratio=1.036, hyp_len=24358, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.422.0.05-1.05.0.06-1.06.1.11-3.04.0.99-2.70.pth, myrk
BLEU = 73.45, 87.3/77.5/69.2/62.2 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.422.0.05-1.05.0.06-1.06.1.11-3.04.0.99-2.70.pth, rkmy
BLEU = 74.74, 87.9/78.6/70.5/64.1 (BP=1.000, ratio=1.033, hyp_len=24280, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.423.0.05-1.05.0.05-1.06.1.09-2.99.0.99-2.69.pth, myrk
BLEU = 73.45, 87.2/77.4/69.2/62.3 (BP=1.000, ratio=1.035, hyp_len=23962, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.423.0.05-1.05.0.05-1.06.1.09-2.99.0.99-2.69.pth, rkmy
BLEU = 74.16, 87.6/78.2/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24364, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.424.0.05-1.05.0.05-1.05.1.09-2.97.0.98-2.65.pth, myrk
BLEU = 73.61, 87.4/77.5/69.4/62.5 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.424.0.05-1.05.0.05-1.05.1.09-2.97.0.98-2.65.pth, rkmy
BLEU = 73.08, 87.0/77.2/68.7/61.9 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.425.0.05-1.05.0.06-1.06.1.11-3.04.0.99-2.68.pth, myrk
BLEU = 73.19, 87.1/77.2/69.0/61.9 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.425.0.05-1.05.0.06-1.06.1.11-3.04.0.99-2.68.pth, rkmy
BLEU = 73.41, 87.3/77.5/68.9/62.2 (BP=1.000, ratio=1.039, hyp_len=24417, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.426.0.05-1.05.0.06-1.06.1.11-3.05.0.99-2.68.pth, myrk
BLEU = 73.23, 87.1/77.2/69.0/61.9 (BP=1.000, ratio=1.035, hyp_len=23969, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.426.0.05-1.05.0.06-1.06.1.11-3.05.0.99-2.68.pth, rkmy
BLEU = 73.98, 87.4/78.0/69.7/63.0 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.427.0.05-1.05.0.06-1.06.1.11-3.03.1.00-2.72.pth, myrk
BLEU = 73.41, 87.2/77.4/69.2/62.1 (BP=1.000, ratio=1.036, hyp_len=23983, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.427.0.05-1.05.0.06-1.06.1.11-3.03.1.00-2.72.pth, rkmy
BLEU = 73.86, 87.4/77.8/69.5/62.9 (BP=1.000, ratio=1.038, hyp_len=24410, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.428.0.04-1.05.0.05-1.05.1.12-3.07.0.99-2.70.pth, myrk
BLEU = 73.43, 87.3/77.4/69.2/62.2 (BP=1.000, ratio=1.035, hyp_len=23967, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.428.0.04-1.05.0.05-1.05.1.12-3.07.0.99-2.70.pth, rkmy
BLEU = 74.41, 87.7/78.3/70.1/63.6 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.429.0.05-1.05.0.05-1.05.1.14-3.13.0.96-2.61.pth, myrk
BLEU = 73.45, 87.4/77.5/69.2/62.1 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.429.0.05-1.05.0.05-1.05.1.14-3.13.0.96-2.61.pth, rkmy
BLEU = 74.91, 88.1/78.9/70.7/64.1 (BP=1.000, ratio=1.032, hyp_len=24267, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.430.0.05-1.05.0.05-1.06.1.13-3.10.0.97-2.65.pth, myrk
BLEU = 73.43, 87.3/77.5/69.2/62.1 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.430.0.05-1.05.0.05-1.06.1.13-3.10.0.97-2.65.pth, rkmy
BLEU = 73.63, 87.4/77.8/69.3/62.4 (BP=1.000, ratio=1.039, hyp_len=24426, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.43.0.55-1.73.0.60-1.83.0.78-2.19.0.78-2.17.pth, myrk
BLEU = 71.13, 86.3/75.6/66.6/58.9 (BP=1.000, ratio=1.020, hyp_len=23632, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.43.0.55-1.73.0.60-1.83.0.78-2.19.0.78-2.17.pth, rkmy
BLEU = 70.66, 86.0/75.4/65.9/58.3 (BP=1.000, ratio=1.023, hyp_len=24039, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.431.0.05-1.05.0.06-1.06.1.13-3.09.0.98-2.67.pth, myrk
BLEU = 73.18, 87.1/77.2/68.9/61.9 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.431.0.05-1.05.0.06-1.06.1.13-3.09.0.98-2.67.pth, rkmy
BLEU = 74.09, 87.6/78.0/69.8/63.2 (BP=1.000, ratio=1.038, hyp_len=24414, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.432.0.05-1.05.0.05-1.06.1.11-3.04.0.99-2.70.pth, myrk
BLEU = 73.15, 87.2/77.2/68.8/61.7 (BP=1.000, ratio=1.034, hyp_len=23957, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.432.0.05-1.05.0.05-1.06.1.11-3.04.0.99-2.70.pth, rkmy
BLEU = 74.51, 87.9/78.5/70.2/63.7 (BP=1.000, ratio=1.033, hyp_len=24295, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.433.0.05-1.06.0.05-1.06.1.12-3.06.1.00-2.72.pth, myrk
BLEU = 73.90, 87.6/77.8/69.7/62.8 (BP=1.000, ratio=1.030, hyp_len=23846, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.433.0.05-1.06.0.05-1.06.1.12-3.06.1.00-2.72.pth, rkmy
BLEU = 74.05, 87.5/78.0/69.8/63.1 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.434.0.06-1.06.0.05-1.06.1.12-3.07.0.98-2.67.pth, myrk
BLEU = 73.81, 87.5/77.8/69.6/62.7 (BP=1.000, ratio=1.032, hyp_len=23903, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.434.0.06-1.06.0.05-1.06.1.12-3.07.0.98-2.67.pth, rkmy
BLEU = 73.28, 87.0/77.4/68.9/62.2 (BP=1.000, ratio=1.041, hyp_len=24479, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.435.0.05-1.06.0.05-1.05.1.09-2.97.1.01-2.74.pth, myrk
BLEU = 73.80, 87.4/77.7/69.6/62.7 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.435.0.05-1.06.0.05-1.05.1.09-2.97.1.01-2.74.pth, rkmy
BLEU = 75.00, 88.0/78.8/70.8/64.4 (BP=1.000, ratio=1.033, hyp_len=24295, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.436.0.06-1.06.0.05-1.06.1.10-3.00.1.02-2.76.pth, myrk
BLEU = 73.62, 87.3/77.6/69.4/62.5 (BP=1.000, ratio=1.035, hyp_len=23979, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.436.0.06-1.06.0.05-1.06.1.10-3.00.1.02-2.76.pth, rkmy
BLEU = 74.09, 87.6/78.1/69.7/63.1 (BP=1.000, ratio=1.035, hyp_len=24325, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.437.0.05-1.05.0.06-1.06.1.11-3.04.1.02-2.78.pth, myrk
BLEU = 73.24, 87.2/77.3/68.9/61.9 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.437.0.05-1.05.0.06-1.06.1.11-3.04.1.02-2.78.pth, rkmy
BLEU = 73.49, 87.3/77.6/69.1/62.3 (BP=1.000, ratio=1.040, hyp_len=24459, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.438.0.05-1.05.0.05-1.05.1.14-3.14.1.00-2.71.pth, myrk
BLEU = 73.54, 87.3/77.5/69.3/62.4 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.438.0.05-1.05.0.05-1.05.1.14-3.14.1.00-2.71.pth, rkmy
BLEU = 75.14, 88.1/79.0/71.0/64.5 (BP=1.000, ratio=1.030, hyp_len=24212, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.439.0.05-1.05.0.06-1.06.1.12-3.07.1.00-2.71.pth, myrk
BLEU = 73.66, 87.4/77.6/69.4/62.5 (BP=1.000, ratio=1.031, hyp_len=23879, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.439.0.05-1.05.0.06-1.06.1.12-3.07.1.00-2.71.pth, rkmy
BLEU = 74.20, 87.6/78.3/69.9/63.3 (BP=1.000, ratio=1.038, hyp_len=24409, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.440.0.05-1.05.0.06-1.06.1.10-3.01.1.02-2.78.pth, myrk
BLEU = 73.61, 87.3/77.6/69.4/62.4 (BP=1.000, ratio=1.034, hyp_len=23945, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.440.0.05-1.05.0.06-1.06.1.10-3.01.1.02-2.78.pth, rkmy
BLEU = 75.23, 88.1/79.0/71.1/64.8 (BP=1.000, ratio=1.033, hyp_len=24284, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.44.0.57-1.77.0.79-2.21.0.77-2.16.0.82-2.28.pth, myrk
BLEU = 71.43, 86.5/75.8/66.9/59.3 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.44.0.57-1.77.0.79-2.21.0.77-2.16.0.82-2.28.pth, rkmy
BLEU = 67.44, 84.3/72.6/62.3/54.2 (BP=1.000, ratio=1.029, hyp_len=24198, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.441.0.05-1.05.0.07-1.07.1.12-3.05.1.02-2.77.pth, myrk
BLEU = 74.06, 87.6/78.0/69.9/63.0 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.441.0.05-1.05.0.07-1.07.1.12-3.05.1.02-2.77.pth, rkmy
BLEU = 74.81, 87.9/78.7/70.6/64.1 (BP=1.000, ratio=1.030, hyp_len=24219, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.442.0.08-1.08.0.07-1.08.1.07-2.92.1.01-2.74.pth, myrk
BLEU = 73.61, 87.4/77.6/69.4/62.4 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.442.0.08-1.08.0.07-1.08.1.07-2.92.1.01-2.74.pth, rkmy
BLEU = 74.25, 87.6/78.1/70.0/63.4 (BP=1.000, ratio=1.035, hyp_len=24321, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.443.0.06-1.07.0.07-1.07.1.13-3.09.1.01-2.73.pth, myrk
BLEU = 74.01, 87.6/77.9/69.8/63.0 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.443.0.06-1.07.0.07-1.07.1.13-3.09.1.01-2.73.pth, rkmy
BLEU = 73.82, 87.4/77.9/69.4/62.8 (BP=1.000, ratio=1.038, hyp_len=24396, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.444.0.06-1.06.0.06-1.06.1.12-3.06.0.99-2.70.pth, myrk
BLEU = 73.38, 87.3/77.4/69.1/62.1 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.444.0.06-1.06.0.06-1.06.1.12-3.06.0.99-2.70.pth, rkmy
BLEU = 73.90, 87.4/77.9/69.6/63.0 (BP=1.000, ratio=1.039, hyp_len=24422, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.445.0.06-1.06.0.05-1.05.1.14-3.11.1.00-2.72.pth, myrk
BLEU = 73.60, 87.4/77.6/69.4/62.4 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.445.0.06-1.06.0.05-1.05.1.14-3.11.1.00-2.72.pth, rkmy
BLEU = 74.06, 87.4/78.0/69.8/63.2 (BP=1.000, ratio=1.040, hyp_len=24450, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.446.0.05-1.06.0.05-1.05.1.14-3.12.0.98-2.67.pth, myrk
BLEU = 74.37, 87.9/78.2/70.2/63.4 (BP=1.000, ratio=1.029, hyp_len=23823, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.446.0.05-1.06.0.05-1.05.1.14-3.12.0.98-2.67.pth, rkmy
BLEU = 74.83, 88.0/78.8/70.6/64.1 (BP=1.000, ratio=1.033, hyp_len=24293, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.447.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.72.pth, myrk
BLEU = 73.57, 87.4/77.6/69.3/62.3 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.447.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.72.pth, rkmy
BLEU = 73.99, 87.4/78.0/69.7/63.1 (BP=1.000, ratio=1.040, hyp_len=24441, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.448.0.05-1.05.0.04-1.04.1.14-3.13.1.03-2.81.pth, myrk
BLEU = 73.74, 87.5/77.7/69.6/62.5 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.448.0.05-1.05.0.04-1.04.1.14-3.13.1.03-2.81.pth, rkmy
BLEU = 74.17, 87.6/78.2/69.9/63.2 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.449.0.05-1.05.0.04-1.04.1.11-3.03.1.01-2.75.pth, myrk
BLEU = 73.57, 87.4/77.5/69.4/62.3 (BP=1.000, ratio=1.035, hyp_len=23981, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.449.0.05-1.05.0.04-1.04.1.11-3.03.1.01-2.75.pth, rkmy
BLEU = 74.84, 87.9/78.7/70.7/64.2 (BP=1.000, ratio=1.035, hyp_len=24324, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.450.0.04-1.05.0.04-1.05.1.13-3.10.1.01-2.74.pth, myrk
BLEU = 73.35, 87.2/77.3/69.1/62.1 (BP=1.000, ratio=1.034, hyp_len=23939, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.450.0.04-1.05.0.04-1.05.1.13-3.10.1.01-2.74.pth, rkmy
BLEU = 74.47, 87.7/78.5/70.3/63.6 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.45.0.55-1.73.0.64-1.90.0.76-2.14.0.77-2.17.pth, myrk
BLEU = 71.63, 86.5/76.0/67.2/59.6 (BP=1.000, ratio=1.018, hyp_len=23574, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.45.0.55-1.73.0.64-1.90.0.76-2.14.0.77-2.17.pth, rkmy
BLEU = 69.44, 85.3/74.4/64.5/56.8 (BP=1.000, ratio=1.028, hyp_len=24160, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.451.0.04-1.04.0.05-1.05.1.15-3.16.1.02-2.79.pth, myrk
BLEU = 73.88, 87.4/77.8/69.7/62.8 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.451.0.04-1.04.0.05-1.05.1.15-3.16.1.02-2.79.pth, rkmy
BLEU = 74.51, 87.7/78.3/70.3/63.8 (BP=1.000, ratio=1.035, hyp_len=24338, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.452.0.04-1.04.0.04-1.05.1.13-3.10.1.02-2.76.pth, myrk
BLEU = 73.82, 87.5/77.8/69.6/62.7 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.452.0.04-1.04.0.04-1.05.1.13-3.10.1.02-2.76.pth, rkmy
BLEU = 74.72, 87.8/78.5/70.5/64.1 (BP=1.000, ratio=1.035, hyp_len=24332, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.453.0.05-1.05.0.05-1.05.1.12-3.07.1.01-2.74.pth, myrk
BLEU = 73.96, 87.6/77.8/69.8/62.9 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.453.0.05-1.05.0.05-1.05.1.12-3.07.1.01-2.74.pth, rkmy
BLEU = 74.24, 87.5/78.1/70.0/63.5 (BP=1.000, ratio=1.037, hyp_len=24383, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.454.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.73.pth, myrk
BLEU = 74.06, 87.7/78.0/69.9/62.9 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.454.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.73.pth, rkmy
BLEU = 74.24, 87.7/78.2/69.9/63.3 (BP=1.000, ratio=1.034, hyp_len=24316, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.455.0.05-1.05.0.05-1.05.1.11-3.03.1.02-2.78.pth, myrk
BLEU = 73.80, 87.6/77.8/69.6/62.6 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.455.0.05-1.05.0.05-1.05.1.11-3.03.1.02-2.78.pth, rkmy
BLEU = 74.90, 88.1/78.8/70.6/64.2 (BP=1.000, ratio=1.032, hyp_len=24254, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.456.0.05-1.05.0.05-1.05.1.14-3.12.1.00-2.72.pth, myrk
BLEU = 73.11, 87.1/77.2/68.8/61.8 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.456.0.05-1.05.0.05-1.05.1.14-3.12.1.00-2.72.pth, rkmy
BLEU = 74.19, 87.5/78.1/69.9/63.3 (BP=1.000, ratio=1.039, hyp_len=24419, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.457.0.05-1.05.0.05-1.05.1.13-3.09.1.00-2.71.pth, myrk
BLEU = 72.95, 86.9/76.9/68.6/61.7 (BP=1.000, ratio=1.037, hyp_len=24017, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.457.0.05-1.05.0.05-1.05.1.13-3.09.1.00-2.71.pth, rkmy
BLEU = 75.14, 88.3/79.0/70.9/64.5 (BP=1.000, ratio=1.030, hyp_len=24216, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.458.0.05-1.05.0.05-1.05.1.12-3.08.1.03-2.81.pth, myrk
BLEU = 73.36, 87.3/77.4/69.1/62.0 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.458.0.05-1.05.0.05-1.05.1.12-3.08.1.03-2.81.pth, rkmy
BLEU = 73.71, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.042, hyp_len=24496, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.459.0.05-1.05.0.05-1.05.1.14-3.12.1.03-2.79.pth, myrk
BLEU = 72.96, 87.0/77.1/68.7/61.5 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.459.0.05-1.05.0.05-1.05.1.14-3.12.1.03-2.79.pth, rkmy
BLEU = 75.30, 88.4/79.1/71.1/64.7 (BP=1.000, ratio=1.025, hyp_len=24090, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.460.0.05-1.05.0.05-1.05.1.13-3.10.1.02-2.79.pth, myrk
BLEU = 73.41, 87.2/77.3/69.2/62.3 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.460.0.05-1.05.0.05-1.05.1.13-3.10.1.02-2.79.pth, rkmy
BLEU = 73.54, 87.3/77.5/69.1/62.5 (BP=1.000, ratio=1.040, hyp_len=24450, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.46.0.57-1.77.0.57-1.76.0.94-2.57.0.75-2.13.pth, myrk
BLEU = 63.43, 81.7/69.2/58.2/49.2 (BP=1.000, ratio=1.054, hyp_len=24411, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.46.0.57-1.77.0.57-1.76.0.94-2.57.0.75-2.13.pth, rkmy
BLEU = 69.70, 85.4/74.5/64.8/57.2 (BP=1.000, ratio=1.031, hyp_len=24247, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.461.0.05-1.06.0.05-1.05.1.15-3.17.1.00-2.73.pth, myrk
BLEU = 72.88, 87.0/77.0/68.5/61.4 (BP=1.000, ratio=1.037, hyp_len=24013, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.461.0.05-1.06.0.05-1.05.1.15-3.17.1.00-2.73.pth, rkmy
BLEU = 74.04, 87.5/78.0/69.8/63.1 (BP=1.000, ratio=1.039, hyp_len=24419, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.462.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.72.pth, myrk
BLEU = 73.58, 87.3/77.5/69.4/62.4 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.462.0.05-1.05.0.05-1.05.1.13-3.10.1.00-2.72.pth, rkmy
BLEU = 74.17, 87.5/78.0/69.9/63.4 (BP=1.000, ratio=1.039, hyp_len=24431, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.463.0.05-1.05.0.05-1.05.1.12-3.08.1.01-2.76.pth, myrk
BLEU = 73.80, 87.4/77.8/69.7/62.6 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.463.0.05-1.05.0.05-1.05.1.12-3.08.1.01-2.76.pth, rkmy
BLEU = 74.22, 87.5/78.3/70.0/63.3 (BP=1.000, ratio=1.039, hyp_len=24421, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.464.0.05-1.06.0.05-1.05.1.14-3.14.1.01-2.74.pth, myrk
BLEU = 73.13, 87.1/77.2/68.8/61.8 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.464.0.05-1.06.0.05-1.05.1.14-3.14.1.01-2.74.pth, rkmy
BLEU = 74.63, 87.9/78.6/70.4/63.8 (BP=1.000, ratio=1.035, hyp_len=24324, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.465.0.06-1.06.0.05-1.05.1.16-3.17.1.01-2.75.pth, myrk
BLEU = 72.84, 87.0/77.0/68.5/61.3 (BP=1.000, ratio=1.035, hyp_len=23967, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.465.0.06-1.06.0.05-1.05.1.16-3.17.1.01-2.75.pth, rkmy
BLEU = 73.68, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.466.0.08-1.09.0.05-1.05.1.18-3.25.1.02-2.78.pth, myrk
BLEU = 73.40, 87.3/77.5/69.2/62.0 (BP=1.000, ratio=1.024, hyp_len=23725, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.466.0.08-1.09.0.05-1.05.1.18-3.25.1.02-2.78.pth, rkmy
BLEU = 74.07, 87.6/78.0/69.7/63.1 (BP=1.000, ratio=1.037, hyp_len=24382, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.467.0.07-1.08.0.05-1.05.1.16-3.19.1.03-2.79.pth, myrk
BLEU = 72.71, 87.0/77.0/68.4/61.0 (BP=1.000, ratio=1.036, hyp_len=23990, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.467.0.07-1.08.0.05-1.05.1.16-3.19.1.03-2.79.pth, rkmy
BLEU = 74.65, 87.9/78.6/70.4/63.9 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.468.0.06-1.06.0.05-1.05.1.14-3.13.1.03-2.80.pth, myrk
BLEU = 73.37, 87.3/77.4/69.1/62.0 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.468.0.06-1.06.0.05-1.05.1.14-3.13.1.03-2.80.pth, rkmy
BLEU = 74.47, 88.0/78.4/70.1/63.6 (BP=1.000, ratio=1.033, hyp_len=24283, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.469.0.06-1.06.0.05-1.06.1.13-3.10.1.01-2.75.pth, myrk
BLEU = 74.36, 88.0/78.3/70.2/63.2 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.469.0.06-1.06.0.05-1.06.1.13-3.10.1.01-2.75.pth, rkmy
BLEU = 74.54, 87.8/78.4/70.3/63.8 (BP=1.000, ratio=1.032, hyp_len=24254, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.470.0.05-1.05.0.06-1.06.1.14-3.12.1.03-2.79.pth, myrk
BLEU = 73.08, 87.2/77.3/68.7/61.5 (BP=1.000, ratio=1.035, hyp_len=23976, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.470.0.05-1.05.0.06-1.06.1.14-3.12.1.03-2.79.pth, rkmy
BLEU = 74.27, 87.6/78.1/70.0/63.5 (BP=1.000, ratio=1.037, hyp_len=24370, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.47.0.56-1.75.0.54-1.71.0.79-2.19.0.74-2.09.pth, myrk
BLEU = 69.97, 85.4/74.7/65.5/57.4 (BP=1.000, ratio=1.037, hyp_len=24008, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.47.0.56-1.75.0.54-1.71.0.79-2.19.0.74-2.09.pth, rkmy
BLEU = 70.88, 85.9/75.5/66.1/58.9 (BP=1.000, ratio=1.031, hyp_len=24238, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.471.0.05-1.05.0.06-1.06.1.12-3.06.1.05-2.86.pth, myrk
BLEU = 74.09, 87.7/78.1/69.9/63.0 (BP=1.000, ratio=1.028, hyp_len=23812, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.471.0.05-1.05.0.06-1.06.1.12-3.06.1.05-2.86.pth, rkmy
BLEU = 73.89, 87.5/77.8/69.5/62.9 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.472.0.05-1.05.0.05-1.06.1.14-3.12.1.02-2.77.pth, myrk
BLEU = 73.34, 87.3/77.5/69.1/61.9 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.472.0.05-1.05.0.05-1.06.1.14-3.12.1.02-2.77.pth, rkmy
BLEU = 74.17, 87.7/78.2/69.8/63.2 (BP=1.000, ratio=1.035, hyp_len=24324, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.473.0.05-1.05.0.06-1.07.1.14-3.11.1.04-2.84.pth, myrk
BLEU = 74.12, 87.8/78.1/69.9/63.0 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.473.0.05-1.05.0.06-1.07.1.14-3.11.1.04-2.84.pth, rkmy
BLEU = 73.80, 87.3/77.8/69.5/62.8 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.474.0.05-1.05.0.06-1.07.1.12-3.06.1.04-2.84.pth, myrk
BLEU = 73.74, 87.5/77.7/69.5/62.6 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.474.0.05-1.05.0.06-1.07.1.12-3.06.1.04-2.84.pth, rkmy
BLEU = 74.05, 87.6/78.1/69.8/63.1 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.475.0.05-1.05.0.05-1.06.1.12-3.05.1.03-2.81.pth, myrk
BLEU = 73.39, 87.3/77.4/69.1/62.1 (BP=1.000, ratio=1.033, hyp_len=23915, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.475.0.05-1.05.0.05-1.06.1.12-3.05.1.03-2.81.pth, rkmy
BLEU = 74.71, 88.0/78.5/70.4/64.0 (BP=1.000, ratio=1.035, hyp_len=24331, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.476.0.04-1.05.0.05-1.05.1.13-3.08.1.06-2.89.pth, myrk
BLEU = 72.90, 87.0/77.0/68.6/61.4 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.476.0.04-1.05.0.05-1.05.1.13-3.08.1.06-2.89.pth, rkmy
BLEU = 74.28, 87.7/78.2/70.0/63.4 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.477.0.05-1.05.0.05-1.05.1.13-3.08.1.03-2.81.pth, myrk
BLEU = 73.54, 87.3/77.6/69.3/62.3 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.477.0.05-1.05.0.05-1.05.1.13-3.08.1.03-2.81.pth, rkmy
BLEU = 73.53, 87.2/77.4/69.2/62.6 (BP=1.000, ratio=1.042, hyp_len=24503, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.478.0.05-1.05.0.05-1.05.1.12-3.08.1.04-2.83.pth, myrk
BLEU = 73.76, 87.4/77.7/69.6/62.6 (BP=1.000, ratio=1.033, hyp_len=23923, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.478.0.05-1.05.0.05-1.05.1.12-3.08.1.04-2.83.pth, rkmy
BLEU = 74.29, 87.6/78.3/70.0/63.4 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.479.0.05-1.05.0.06-1.06.1.14-3.11.1.03-2.80.pth, myrk
BLEU = 73.46, 87.4/77.5/69.2/62.0 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.479.0.05-1.05.0.06-1.06.1.14-3.11.1.03-2.80.pth, rkmy
BLEU = 73.44, 87.2/77.5/69.0/62.3 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.480.0.05-1.05.0.06-1.07.1.14-3.13.1.04-2.82.pth, myrk
BLEU = 73.92, 87.7/78.0/69.7/62.6 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.480.0.05-1.05.0.06-1.07.1.14-3.13.1.04-2.82.pth, rkmy
BLEU = 74.61, 87.9/78.6/70.3/63.8 (BP=1.000, ratio=1.033, hyp_len=24281, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.48.0.54-1.72.0.52-1.69.0.78-2.17.0.74-2.09.pth, myrk
BLEU = 69.54, 85.1/74.2/64.9/57.1 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.48.0.54-1.72.0.52-1.69.0.78-2.17.0.74-2.09.pth, rkmy
BLEU = 71.71, 86.4/76.3/67.0/59.9 (BP=1.000, ratio=1.027, hyp_len=24153, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.481.0.05-1.05.0.06-1.06.1.13-3.11.1.04-2.84.pth, myrk
BLEU = 73.42, 87.4/77.5/69.1/62.0 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.481.0.05-1.05.0.06-1.06.1.13-3.11.1.04-2.84.pth, rkmy
BLEU = 72.30, 86.7/76.6/67.8/60.7 (BP=1.000, ratio=1.044, hyp_len=24551, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.482.0.05-1.05.0.05-1.05.1.14-3.13.1.03-2.81.pth, myrk
BLEU = 73.53, 87.4/77.5/69.3/62.2 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.482.0.05-1.05.0.05-1.05.1.14-3.13.1.03-2.81.pth, rkmy
BLEU = 73.87, 87.6/77.9/69.6/62.8 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.483.0.05-1.05.0.08-1.08.1.12-3.07.1.04-2.82.pth, myrk
BLEU = 73.71, 87.4/77.7/69.5/62.5 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.483.0.05-1.05.0.08-1.08.1.12-3.07.1.04-2.82.pth, rkmy
BLEU = 74.03, 87.5/78.1/69.8/63.0 (BP=1.000, ratio=1.033, hyp_len=24295, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.484.0.05-1.06.0.08-1.08.1.14-3.12.1.04-2.82.pth, myrk
BLEU = 73.70, 87.5/77.7/69.5/62.5 (BP=1.000, ratio=1.032, hyp_len=23900, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.484.0.05-1.06.0.08-1.08.1.14-3.12.1.04-2.82.pth, rkmy
BLEU = 73.70, 87.3/77.7/69.4/62.7 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.485.0.05-1.06.0.06-1.07.1.13-3.09.1.01-2.76.pth, myrk
BLEU = 72.79, 87.0/77.0/68.5/61.2 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.485.0.05-1.06.0.06-1.07.1.13-3.09.1.01-2.76.pth, rkmy
BLEU = 73.50, 87.2/77.6/69.1/62.4 (BP=1.000, ratio=1.038, hyp_len=24404, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.486.0.06-1.06.0.05-1.05.1.13-3.11.1.05-2.86.pth, myrk
BLEU = 72.79, 87.1/76.9/68.5/61.2 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.486.0.06-1.06.0.05-1.05.1.13-3.11.1.05-2.86.pth, rkmy
BLEU = 74.22, 87.5/78.1/70.0/63.4 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.487.0.06-1.06.0.05-1.05.1.15-3.16.1.02-2.78.pth, myrk
BLEU = 74.18, 87.7/78.0/70.0/63.1 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.487.0.06-1.06.0.05-1.05.1.15-3.16.1.02-2.78.pth, rkmy
BLEU = 73.76, 87.2/77.7/69.5/62.8 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.488.0.06-1.06.0.05-1.05.1.16-3.19.1.02-2.76.pth, myrk
BLEU = 73.82, 87.6/77.9/69.6/62.5 (BP=1.000, ratio=1.031, hyp_len=23878, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.488.0.06-1.06.0.05-1.05.1.16-3.19.1.02-2.76.pth, rkmy
BLEU = 74.31, 87.7/78.3/70.1/63.3 (BP=1.000, ratio=1.035, hyp_len=24332, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.489.0.06-1.06.0.05-1.05.1.17-3.21.1.02-2.78.pth, myrk
BLEU = 72.74, 86.9/76.8/68.4/61.3 (BP=1.000, ratio=1.038, hyp_len=24051, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.489.0.06-1.06.0.05-1.05.1.17-3.21.1.02-2.78.pth, rkmy
BLEU = 74.87, 87.9/78.7/70.7/64.2 (BP=1.000, ratio=1.034, hyp_len=24317, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.490.0.05-1.05.0.04-1.04.1.17-3.22.1.03-2.80.pth, myrk
BLEU = 73.02, 87.2/77.2/68.7/61.5 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.490.0.05-1.05.0.04-1.04.1.17-3.22.1.03-2.80.pth, rkmy
BLEU = 74.44, 87.7/78.3/70.2/63.7 (BP=1.000, ratio=1.039, hyp_len=24424, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.49.0.48-1.62.0.50-1.65.0.73-2.08.0.74-2.10.pth, myrk
BLEU = 73.15, 87.1/77.2/69.0/61.8 (BP=1.000, ratio=1.021, hyp_len=23649, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.49.0.48-1.62.0.50-1.65.0.73-2.08.0.74-2.10.pth, rkmy
BLEU = 71.40, 86.2/75.9/66.7/59.6 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.491.0.05-1.05.0.04-1.04.1.17-3.22.1.03-2.80.pth, myrk
BLEU = 73.41, 87.2/77.5/69.2/62.1 (BP=1.000, ratio=1.035, hyp_len=23965, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.491.0.05-1.05.0.04-1.04.1.17-3.22.1.03-2.80.pth, rkmy
BLEU = 74.58, 87.8/78.5/70.3/63.8 (BP=1.000, ratio=1.036, hyp_len=24349, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.492.0.05-1.05.0.04-1.05.1.16-3.19.1.03-2.81.pth, myrk
BLEU = 73.30, 87.4/77.5/69.0/61.7 (BP=1.000, ratio=1.034, hyp_len=23939, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.492.0.05-1.05.0.04-1.05.1.16-3.19.1.03-2.81.pth, rkmy
BLEU = 74.64, 87.8/78.4/70.4/64.0 (BP=1.000, ratio=1.036, hyp_len=24366, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.493.0.05-1.05.0.04-1.04.1.16-3.18.1.03-2.79.pth, myrk
BLEU = 73.73, 87.5/77.7/69.5/62.4 (BP=1.000, ratio=1.032, hyp_len=23903, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.493.0.05-1.05.0.04-1.04.1.16-3.18.1.03-2.79.pth, rkmy
BLEU = 74.17, 87.5/78.1/69.9/63.3 (BP=1.000, ratio=1.039, hyp_len=24432, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.494.0.05-1.05.0.04-1.04.1.16-3.18.1.04-2.83.pth, myrk
BLEU = 73.57, 87.3/77.6/69.4/62.3 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.494.0.05-1.05.0.04-1.04.1.16-3.18.1.04-2.83.pth, rkmy
BLEU = 74.40, 87.6/78.3/70.2/63.6 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.495.0.05-1.05.0.04-1.04.1.15-3.14.1.04-2.82.pth, myrk
BLEU = 72.86, 87.1/77.1/68.5/61.2 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.495.0.05-1.05.0.04-1.04.1.15-3.14.1.04-2.82.pth, rkmy
BLEU = 74.54, 87.6/78.4/70.4/63.9 (BP=1.000, ratio=1.038, hyp_len=24394, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.496.0.05-1.05.0.04-1.04.1.14-3.12.1.03-2.80.pth, myrk
BLEU = 73.27, 87.2/77.4/69.0/61.9 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.496.0.05-1.05.0.04-1.04.1.14-3.12.1.03-2.80.pth, rkmy
BLEU = 74.19, 87.6/78.2/70.0/63.2 (BP=1.000, ratio=1.037, hyp_len=24385, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.497.0.05-1.05.0.04-1.05.1.15-3.15.1.04-2.84.pth, myrk
BLEU = 74.11, 87.6/78.0/69.9/63.1 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.497.0.05-1.05.0.04-1.05.1.15-3.15.1.04-2.84.pth, rkmy
BLEU = 74.37, 87.6/78.2/70.2/63.7 (BP=1.000, ratio=1.039, hyp_len=24417, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.498.0.04-1.04.0.04-1.04.1.14-3.12.1.04-2.84.pth, myrk
BLEU = 73.28, 87.3/77.4/69.0/61.9 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.498.0.04-1.04.0.04-1.04.1.14-3.12.1.04-2.84.pth, rkmy
BLEU = 74.03, 87.5/78.0/69.7/63.1 (BP=1.000, ratio=1.040, hyp_len=24453, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.499.0.05-1.05.0.05-1.05.1.16-3.18.1.04-2.82.pth, myrk
BLEU = 73.64, 87.4/77.7/69.4/62.4 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.499.0.05-1.05.0.05-1.05.1.16-3.18.1.04-2.82.pth, rkmy
BLEU = 74.94, 88.0/78.8/70.8/64.3 (BP=1.000, ratio=1.033, hyp_len=24283, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.500.0.04-1.04.0.05-1.05.1.18-3.24.1.02-2.76.pth, myrk
BLEU = 73.20, 87.2/77.3/68.9/61.7 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.500.0.04-1.04.0.05-1.05.1.18-3.24.1.02-2.76.pth, rkmy
BLEU = 74.39, 87.7/78.3/70.1/63.6 (BP=1.000, ratio=1.035, hyp_len=24342, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.50.0.45-1.57.0.48-1.62.0.74-2.10.0.73-2.07.pth, myrk
BLEU = 72.72, 86.7/76.8/68.5/61.3 (BP=1.000, ratio=1.021, hyp_len=23650, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.50.0.45-1.57.0.48-1.62.0.74-2.10.0.73-2.07.pth, rkmy
BLEU = 72.20, 86.6/76.6/67.6/60.6 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.51.0.45-1.57.0.48-1.62.0.73-2.07.0.73-2.09.pth, myrk
BLEU = 72.91, 86.8/77.0/68.7/61.5 (BP=1.000, ratio=1.024, hyp_len=23717, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.51.0.45-1.57.0.48-1.62.0.73-2.07.0.73-2.09.pth, rkmy
BLEU = 72.30, 86.7/76.7/67.7/60.7 (BP=1.000, ratio=1.025, hyp_len=24092, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.52.0.46-1.58.0.48-1.61.0.72-2.06.0.72-2.06.pth, myrk
BLEU = 72.28, 86.6/76.5/67.9/60.7 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.52.0.46-1.58.0.48-1.61.0.72-2.06.0.72-2.06.pth, rkmy
BLEU = 72.45, 86.8/76.8/67.8/60.9 (BP=1.000, ratio=1.029, hyp_len=24196, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.53.0.42-1.52.0.45-1.56.0.73-2.08.0.73-2.07.pth, myrk
BLEU = 72.91, 86.9/76.9/68.7/61.6 (BP=1.000, ratio=1.021, hyp_len=23635, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.53.0.42-1.52.0.45-1.56.0.73-2.08.0.73-2.07.pth, rkmy
BLEU = 71.65, 86.4/76.1/66.9/59.9 (BP=1.000, ratio=1.031, hyp_len=24249, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.54.0.43-1.54.0.44-1.55.0.73-2.08.0.72-2.05.pth, myrk
BLEU = 73.02, 87.0/77.0/68.8/61.7 (BP=1.000, ratio=1.022, hyp_len=23676, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.54.0.43-1.54.0.44-1.55.0.73-2.08.0.72-2.05.pth, rkmy
BLEU = 73.05, 87.1/77.3/68.5/61.7 (BP=1.000, ratio=1.023, hyp_len=24048, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.55.0.39-1.48.0.42-1.53.0.72-2.05.0.73-2.07.pth, myrk
BLEU = 73.73, 87.3/77.7/69.6/62.6 (BP=1.000, ratio=1.023, hyp_len=23683, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.55.0.39-1.48.0.42-1.53.0.72-2.05.0.73-2.07.pth, rkmy
BLEU = 72.50, 86.7/76.8/68.0/61.0 (BP=1.000, ratio=1.025, hyp_len=24105, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.56.0.42-1.52.0.53-1.70.0.70-2.02.0.82-2.28.pth, myrk
BLEU = 73.35, 86.9/77.2/69.2/62.3 (BP=1.000, ratio=1.024, hyp_len=23706, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.56.0.42-1.52.0.53-1.70.0.70-2.02.0.82-2.28.pth, rkmy
BLEU = 67.33, 84.2/72.5/62.2/54.2 (BP=1.000, ratio=1.034, hyp_len=24316, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.57.0.49-1.63.0.79-2.20.0.72-2.05.0.83-2.30.pth, myrk
BLEU = 72.31, 86.5/76.4/68.0/60.8 (BP=1.000, ratio=1.026, hyp_len=23769, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.57.0.49-1.63.0.79-2.20.0.72-2.05.0.83-2.30.pth, rkmy
BLEU = 65.77, 83.0/71.3/60.6/52.2 (BP=1.000, ratio=1.043, hyp_len=24529, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.58.0.48-1.61.0.57-1.78.0.74-2.09.0.75-2.11.pth, myrk
BLEU = 71.19, 85.9/75.6/66.7/59.3 (BP=1.000, ratio=1.024, hyp_len=23727, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.58.0.48-1.61.0.57-1.78.0.74-2.09.0.75-2.11.pth, rkmy
BLEU = 69.28, 85.1/74.4/64.4/56.5 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.59.0.42-1.53.0.48-1.62.0.70-2.01.0.71-2.03.pth, myrk
BLEU = 72.82, 86.7/76.8/68.6/61.6 (BP=1.000, ratio=1.024, hyp_len=23718, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.59.0.42-1.53.0.48-1.62.0.70-2.01.0.71-2.03.pth, rkmy
BLEU = 71.56, 86.1/76.1/66.9/59.8 (BP=1.000, ratio=1.034, hyp_len=24315, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.60.0.39-1.48.0.44-1.56.0.70-2.02.0.68-1.98.pth, myrk
BLEU = 73.32, 86.9/77.2/69.1/62.4 (BP=1.000, ratio=1.026, hyp_len=23770, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.60.0.39-1.48.0.44-1.56.0.70-2.02.0.68-1.98.pth, rkmy
BLEU = 73.17, 87.0/77.4/68.7/61.9 (BP=1.000, ratio=1.030, hyp_len=24215, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.61.0.37-1.45.0.42-1.53.0.69-1.99.0.68-1.97.pth, myrk
BLEU = 73.86, 87.2/77.7/69.8/63.0 (BP=1.000, ratio=1.024, hyp_len=23705, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.61.0.37-1.45.0.42-1.53.0.69-1.99.0.68-1.97.pth, rkmy
BLEU = 72.62, 86.8/77.0/68.1/61.1 (BP=1.000, ratio=1.032, hyp_len=24256, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.62.0.38-1.47.0.43-1.54.0.69-2.00.0.67-1.96.pth, myrk
BLEU = 73.92, 87.2/77.6/69.9/63.1 (BP=1.000, ratio=1.025, hyp_len=23743, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.62.0.38-1.47.0.43-1.54.0.69-2.00.0.67-1.96.pth, rkmy
BLEU = 72.66, 86.9/77.0/68.1/61.2 (BP=1.000, ratio=1.033, hyp_len=24295, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.63.0.35-1.43.0.39-1.47.0.70-2.02.0.67-1.95.pth, myrk
BLEU = 74.01, 87.4/77.8/69.9/63.2 (BP=1.000, ratio=1.024, hyp_len=23711, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.63.0.35-1.43.0.39-1.47.0.70-2.02.0.67-1.95.pth, rkmy
BLEU = 73.34, 87.1/77.5/68.9/62.2 (BP=1.000, ratio=1.031, hyp_len=24229, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.64.0.37-1.44.0.41-1.51.0.69-1.99.0.69-1.99.pth, myrk
BLEU = 73.77, 87.0/77.5/69.7/63.0 (BP=1.000, ratio=1.028, hyp_len=23798, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.64.0.37-1.44.0.41-1.51.0.69-1.99.0.69-1.99.pth, rkmy
BLEU = 72.34, 86.4/76.6/67.8/61.0 (BP=1.000, ratio=1.038, hyp_len=24412, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.65.0.35-1.42.0.39-1.48.0.69-1.98.0.69-2.00.pth, myrk
BLEU = 73.36, 86.8/77.2/69.2/62.5 (BP=1.000, ratio=1.031, hyp_len=23882, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.65.0.35-1.42.0.39-1.48.0.69-1.98.0.69-2.00.pth, rkmy
BLEU = 73.58, 87.2/77.7/69.1/62.5 (BP=1.000, ratio=1.032, hyp_len=24260, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.66.0.35-1.42.0.39-1.48.0.69-2.00.0.67-1.95.pth, myrk
BLEU = 73.85, 87.2/77.7/69.7/62.9 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.66.0.35-1.42.0.39-1.48.0.69-2.00.0.67-1.95.pth, rkmy
BLEU = 72.59, 86.6/76.8/68.1/61.3 (BP=1.000, ratio=1.039, hyp_len=24432, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.67.0.33-1.39.0.38-1.46.0.68-1.97.0.68-1.97.pth, myrk
BLEU = 73.71, 87.1/77.5/69.6/62.9 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.67.0.33-1.39.0.38-1.46.0.68-1.97.0.68-1.97.pth, rkmy
BLEU = 73.15, 86.9/77.4/68.7/61.9 (BP=1.000, ratio=1.037, hyp_len=24375, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.68.0.33-1.39.0.37-1.44.0.67-1.95.0.68-1.98.pth, myrk
BLEU = 74.45, 87.7/78.2/70.4/63.7 (BP=1.000, ratio=1.026, hyp_len=23759, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.68.0.33-1.39.0.37-1.44.0.67-1.95.0.68-1.98.pth, rkmy
BLEU = 73.17, 87.0/77.4/68.7/61.9 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.69.0.34-1.41.0.37-1.45.0.69-2.00.0.68-1.97.pth, myrk
BLEU = 74.28, 87.4/78.1/70.2/63.5 (BP=1.000, ratio=1.027, hyp_len=23779, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.69.0.34-1.41.0.37-1.45.0.69-2.00.0.68-1.97.pth, rkmy
BLEU = 73.55, 87.2/77.7/69.2/62.4 (BP=1.000, ratio=1.033, hyp_len=24295, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.70.0.32-1.38.0.36-1.44.0.69-1.99.0.69-1.99.pth, myrk
BLEU = 73.70, 87.0/77.4/69.6/62.9 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.70.0.32-1.38.0.36-1.44.0.69-1.99.0.69-1.99.pth, rkmy
BLEU = 74.52, 87.6/78.5/70.3/63.8 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.71.0.33-1.39.0.39-1.48.0.67-1.96.0.68-1.98.pth, myrk
BLEU = 74.05, 87.1/77.7/70.0/63.4 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.71.0.33-1.39.0.39-1.48.0.67-1.96.0.68-1.98.pth, rkmy
BLEU = 73.21, 86.9/77.4/68.8/62.0 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.72.0.32-1.38.0.37-1.44.0.68-1.97.0.68-1.98.pth, myrk
BLEU = 73.42, 86.7/77.2/69.3/62.7 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.72.0.32-1.38.0.37-1.44.0.68-1.97.0.68-1.98.pth, rkmy
BLEU = 73.40, 87.0/77.5/69.0/62.3 (BP=1.000, ratio=1.033, hyp_len=24291, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.73.0.32-1.38.0.36-1.43.0.69-1.99.0.68-1.97.pth, myrk
BLEU = 74.24, 87.4/78.0/70.2/63.5 (BP=1.000, ratio=1.025, hyp_len=23735, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.73.0.32-1.38.0.36-1.43.0.69-1.99.0.68-1.97.pth, rkmy
BLEU = 74.77, 87.7/78.6/70.6/64.2 (BP=1.000, ratio=1.026, hyp_len=24129, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.74.0.32-1.38.0.35-1.42.0.69-2.00.0.67-1.95.pth, myrk
BLEU = 73.65, 86.9/77.5/69.6/62.8 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.74.0.32-1.38.0.35-1.42.0.69-2.00.0.67-1.95.pth, rkmy
BLEU = 73.04, 86.8/77.2/68.6/61.9 (BP=1.000, ratio=1.041, hyp_len=24463, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.75.0.32-1.38.0.34-1.40.0.69-2.00.0.68-1.97.pth, myrk
BLEU = 73.60, 86.9/77.4/69.5/62.7 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.75.0.32-1.38.0.34-1.40.0.69-2.00.0.68-1.97.pth, rkmy
BLEU = 74.36, 87.4/78.3/70.1/63.7 (BP=1.000, ratio=1.035, hyp_len=24322, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.76.0.32-1.38.0.32-1.38.0.70-2.01.0.67-1.96.pth, myrk
BLEU = 73.79, 87.2/77.6/69.7/62.8 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.76.0.32-1.38.0.32-1.38.0.70-2.01.0.67-1.96.pth, rkmy
BLEU = 74.24, 87.5/78.3/69.9/63.4 (BP=1.000, ratio=1.033, hyp_len=24296, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.77.0.46-1.59.0.34-1.41.0.74-2.09.0.67-1.96.pth, myrk
BLEU = 72.10, 86.5/76.3/67.7/60.5 (BP=1.000, ratio=1.028, hyp_len=23816, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.77.0.46-1.59.0.34-1.41.0.74-2.09.0.67-1.96.pth, rkmy
BLEU = 73.59, 87.2/77.7/69.2/62.6 (BP=1.000, ratio=1.036, hyp_len=24346, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.78.0.38-1.46.0.33-1.39.0.69-1.99.0.66-1.94.pth, myrk
BLEU = 73.58, 87.2/77.5/69.4/62.5 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.78.0.38-1.46.0.33-1.39.0.69-1.99.0.66-1.94.pth, rkmy
BLEU = 74.73, 87.7/78.7/70.5/64.1 (BP=1.000, ratio=1.031, hyp_len=24249, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.79.0.32-1.38.0.33-1.39.0.67-1.96.0.67-1.96.pth, myrk
BLEU = 74.06, 87.2/77.9/70.0/63.3 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.79.0.32-1.38.0.33-1.39.0.67-1.96.0.67-1.96.pth, rkmy
BLEU = 74.18, 87.5/78.3/69.9/63.3 (BP=1.000, ratio=1.031, hyp_len=24240, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.80.0.31-1.37.0.37-1.44.0.66-1.93.0.70-2.01.pth, myrk
BLEU = 74.28, 87.3/78.0/70.3/63.6 (BP=1.000, ratio=1.027, hyp_len=23783, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.80.0.31-1.37.0.37-1.44.0.66-1.93.0.70-2.01.pth, rkmy
BLEU = 71.78, 86.2/76.3/67.2/60.1 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.81.0.32-1.38.0.39-1.48.0.66-1.94.0.72-2.05.pth, myrk
BLEU = 73.65, 86.9/77.4/69.6/62.8 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.81.0.32-1.38.0.39-1.48.0.66-1.94.0.72-2.05.pth, rkmy
BLEU = 70.17, 85.3/75.0/65.4/58.0 (BP=1.000, ratio=1.047, hyp_len=24606, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.82.0.35-1.42.0.53-1.71.0.69-1.99.0.85-2.35.pth, myrk
BLEU = 72.75, 86.7/76.8/68.5/61.3 (BP=1.000, ratio=1.029, hyp_len=23831, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.82.0.35-1.42.0.53-1.71.0.69-1.99.0.85-2.35.pth, rkmy
BLEU = 64.27, 82.4/69.9/59.0/50.2 (BP=1.000, ratio=1.024, hyp_len=24072, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.83.0.37-1.45.0.56-1.74.0.70-2.01.0.82-2.28.pth, myrk
BLEU = 72.37, 86.4/76.5/68.1/60.9 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.83.0.37-1.45.0.56-1.74.0.70-2.01.0.82-2.28.pth, rkmy
BLEU = 67.39, 83.3/72.3/62.6/54.7 (BP=1.000, ratio=1.040, hyp_len=24443, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.84.0.34-1.41.0.42-1.53.0.68-1.98.0.67-1.96.pth, myrk
BLEU = 73.88, 87.1/77.7/69.8/63.0 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.84.0.34-1.41.0.42-1.53.0.68-1.98.0.67-1.96.pth, rkmy
BLEU = 72.95, 86.8/77.4/68.6/61.5 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.85.0.29-1.34.0.35-1.42.0.66-1.94.0.64-1.90.pth, myrk
BLEU = 73.58, 86.8/77.4/69.5/62.8 (BP=1.000, ratio=1.032, hyp_len=23898, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.85.0.29-1.34.0.35-1.42.0.66-1.94.0.64-1.90.pth, rkmy
BLEU = 73.99, 87.3/78.0/69.7/63.1 (BP=1.000, ratio=1.033, hyp_len=24284, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.86.0.28-1.32.0.34-1.40.0.67-1.96.0.64-1.90.pth, myrk
BLEU = 73.49, 86.8/77.3/69.4/62.6 (BP=1.000, ratio=1.035, hyp_len=23976, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.86.0.28-1.32.0.34-1.40.0.67-1.96.0.64-1.90.pth, rkmy
BLEU = 73.08, 86.8/77.2/68.6/62.0 (BP=1.000, ratio=1.040, hyp_len=24446, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.87.0.28-1.32.0.33-1.39.0.66-1.94.0.65-1.92.pth, myrk
BLEU = 74.45, 87.3/78.1/70.5/63.9 (BP=1.000, ratio=1.029, hyp_len=23831, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.87.0.28-1.32.0.33-1.39.0.66-1.94.0.65-1.92.pth, rkmy
BLEU = 73.87, 87.3/78.0/69.5/63.0 (BP=1.000, ratio=1.037, hyp_len=24377, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.88.0.28-1.33.0.33-1.39.0.66-1.94.0.67-1.95.pth, myrk
BLEU = 73.82, 87.0/77.7/69.7/63.0 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.88.0.28-1.33.0.33-1.39.0.66-1.94.0.67-1.95.pth, rkmy
BLEU = 73.90, 87.3/78.0/69.6/62.9 (BP=1.000, ratio=1.037, hyp_len=24388, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.89.0.27-1.31.0.31-1.37.0.65-1.92.0.67-1.95.pth, myrk
BLEU = 74.84, 87.7/78.5/70.9/64.2 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.89.0.27-1.31.0.31-1.37.0.65-1.92.0.67-1.95.pth, rkmy
BLEU = 74.61, 87.6/78.5/70.4/64.0 (BP=1.000, ratio=1.034, hyp_len=24317, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.90.0.26-1.30.0.31-1.36.0.66-1.94.0.66-1.93.pth, myrk
BLEU = 74.77, 87.6/78.5/70.8/64.2 (BP=1.000, ratio=1.024, hyp_len=23722, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.90.0.26-1.30.0.31-1.36.0.66-1.94.0.66-1.93.pth, rkmy
BLEU = 73.59, 87.1/77.7/69.2/62.6 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.91.0.27-1.31.0.31-1.37.0.66-1.94.0.65-1.92.pth, myrk
BLEU = 74.07, 87.2/77.8/70.0/63.4 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.91.0.27-1.31.0.31-1.37.0.66-1.94.0.65-1.92.pth, rkmy
BLEU = 74.62, 87.7/78.6/70.3/63.9 (BP=1.000, ratio=1.034, hyp_len=24313, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.92.0.26-1.30.0.29-1.34.0.69-1.99.0.66-1.93.pth, myrk
BLEU = 74.26, 87.3/78.0/70.2/63.6 (BP=1.000, ratio=1.028, hyp_len=23818, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.92.0.26-1.30.0.29-1.34.0.69-1.99.0.66-1.93.pth, rkmy
BLEU = 73.83, 87.1/77.8/69.5/63.0 (BP=1.000, ratio=1.040, hyp_len=24454, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.93.0.26-1.30.0.29-1.34.0.68-1.98.0.66-1.93.pth, myrk
BLEU = 74.69, 87.7/78.4/70.7/64.0 (BP=1.000, ratio=1.024, hyp_len=23727, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.93.0.26-1.30.0.29-1.34.0.68-1.98.0.66-1.93.pth, rkmy
BLEU = 73.86, 87.1/77.9/69.6/63.0 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.94.0.25-1.28.0.28-1.32.0.69-1.99.0.66-1.93.pth, myrk
BLEU = 73.66, 86.9/77.5/69.6/62.8 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.94.0.25-1.28.0.28-1.32.0.69-1.99.0.66-1.93.pth, rkmy
BLEU = 73.97, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.040, hyp_len=24442, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.95.0.26-1.29.0.29-1.34.0.69-1.99.0.65-1.91.pth, myrk
BLEU = 74.96, 88.1/78.7/71.0/64.2 (BP=1.000, ratio=1.024, hyp_len=23716, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.95.0.26-1.29.0.29-1.34.0.69-1.99.0.65-1.91.pth, rkmy
BLEU = 73.48, 86.9/77.6/69.1/62.5 (BP=1.000, ratio=1.040, hyp_len=24453, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.96.0.25-1.29.0.28-1.33.0.70-2.01.0.65-1.91.pth, myrk
BLEU = 73.64, 87.1/77.5/69.5/62.7 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.96.0.25-1.29.0.28-1.33.0.70-2.01.0.65-1.91.pth, rkmy
BLEU = 74.70, 87.6/78.6/70.5/64.2 (BP=1.000, ratio=1.035, hyp_len=24333, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.97.0.25-1.28.0.28-1.32.0.69-1.98.0.67-1.96.pth, myrk
BLEU = 74.11, 87.2/77.9/70.1/63.4 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.97.0.25-1.28.0.28-1.32.0.69-1.98.0.67-1.96.pth, rkmy
BLEU = 73.73, 87.0/77.7/69.4/62.9 (BP=1.000, ratio=1.041, hyp_len=24474, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.98.0.26-1.29.0.29-1.33.0.69-2.00.0.67-1.95.pth, myrk
BLEU = 74.37, 87.4/78.2/70.3/63.6 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.98.0.26-1.29.0.29-1.33.0.69-2.00.0.67-1.95.pth, rkmy
BLEU = 74.02, 87.3/78.1/69.7/63.2 (BP=1.000, ratio=1.037, hyp_len=24383, ref_len=23509)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.99.0.26-1.29.0.28-1.33.0.68-1.98.0.66-1.94.pth, myrk
BLEU = 73.50, 87.0/77.4/69.3/62.5 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
Evaluation result for the model: seq2seq-dsl-500epoch-model-myrk.99.0.26-1.29.0.28-1.33.0.68-1.98.0.66-1.94.pth, rkmy
BLEU = 73.95, 87.1/77.9/69.7/63.2 (BP=1.000, ratio=1.040, hyp_len=24448, ref_len=23509)
==========

real	306m25.761s
user	299m52.735s
sys	17m43.384s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-rk အတွက် Seq2Seq-DSL Best model က 107 epoch model ဖြစ်ပြီးတော့ Best Score က 75.59 BLEU ပါ။  
rk-my အတွက် Seq2Seq-DSL Best model က 459 epoch model ဖြစ်ပြီးတော့ Best Score က 75.30 BLEU ပါ။   

## Transformer-DSL Training for 500 Epochs (my-rk, rk-my)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 1 --batch_size 64 --n_epochs 500 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 --lm_fn ./model/lm/lm-200epoch.pth --use_transformer --init_epoch 1 --model_fn ./model/dsl/transformer/myrk-500epoch/dsl-model-myrk.pth | tee ./model/dsl/transformer/myrk-500epoch/training.log;
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.01,
    'dsl_n_warmup_epochs': 20,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lm_fn': './model/lm/lm-200epoch.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/transformer/myrk-500epoch/dsl-model-myrk.pth',
    'n_epochs': 500,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_transformer': True,
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
[Transformer(
  (emb_enc): Embedding(1541, 128)
  (emb_dec): Embedding(1642, 128)
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
    (1): Linear(in_features=128, out_features=1642, bias=True)
    (2): LogSoftmax(dim=-1)
  )
), Transformer(
  (emb_enc): Embedding(1642, 128)
  (emb_dec): Embedding(1541, 128)
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
    (1): Linear(in_features=128, out_features=1541, bias=True)
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
Epoch 1 - |param|=9.11e+02 |g_param|=2.96e+05 loss_x2y=3.5206e+00 ppl_x2y=33.81 loss_y2x=3.5347e+00 ppl_y2x=34.28 dual_loss=0.0000e+00
Validation X2Y - loss=2.9098e+00 ppl=18.35 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.8521e+00 ppl=17.32 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.11e+02 |g_param|=3.41e+05 loss_x2y=2.3582e+00 ppl_x2y=10.57 loss_y2x=2.3048e+00 ppl_y2x=10.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.9995e+00 ppl=7.39 best_loss=2.9098e+00 best_ppl=18.35                                           
Validation Y2X - loss=1.9189e+00 ppl=6.81 best_loss=2.8521e+00 best_ppl=17.32
Epoch 3 - |param|=9.12e+02 |g_param|=3.37e+05 loss_x2y=1.7075e+00 ppl_x2y=5.51 loss_y2x=1.6926e+00 ppl_y2x=5.43 dual_loss=0.0000e+00
Validation X2Y - loss=1.4575e+00 ppl=4.30 best_loss=1.9995e+00 best_ppl=7.39                                            
Validation Y2X - loss=1.4381e+00 ppl=4.21 best_loss=1.9189e+00 best_ppl=6.81
Epoch 4 - |param|=9.12e+02 |g_param|=3.64e+05 loss_x2y=1.2855e+00 ppl_x2y=3.62 loss_y2x=1.2782e+00 ppl_y2x=3.59 dual_loss=0.0000e+00
Validation X2Y - loss=1.1636e+00 ppl=3.20 best_loss=1.4575e+00 best_ppl=4.30                                            
Validation Y2X - loss=1.1115e+00 ppl=3.04 best_loss=1.4381e+00 best_ppl=4.21
Epoch 5 - |param|=9.13e+02 |g_param|=3.29e+05 loss_x2y=1.1191e+00 ppl_x2y=3.06 loss_y2x=1.1510e+00 ppl_y2x=3.16 dual_loss=0.0000e+00
Validation X2Y - loss=9.6195e-01 ppl=2.62 best_loss=1.1636e+00 best_ppl=3.20                                            
Validation Y2X - loss=9.5308e-01 ppl=2.59 best_loss=1.1115e+00 best_ppl=3.04
Epoch 6 - |param|=9.13e+02 |g_param|=2.44e+05 loss_x2y=9.1947e-01 ppl_x2y=2.51 loss_y2x=9.2067e-01 ppl_y2x=2.51 dual_loss=0.0000e+00
Validation X2Y - loss=9.0773e-01 ppl=2.48 best_loss=9.6195e-01 best_ppl=2.62                                            
Validation Y2X - loss=8.2771e-01 ppl=2.29 best_loss=9.5308e-01 best_ppl=2.59
Epoch 7 - |param|=9.13e+02 |g_param|=2.45e+05 loss_x2y=8.0534e-01 ppl_x2y=2.24 loss_y2x=8.1658e-01 ppl_y2x=2.26 dual_loss=0.0000e+00
Validation X2Y - loss=8.3159e-01 ppl=2.30 best_loss=9.0773e-01 best_ppl=2.48                                            
Validation Y2X - loss=7.5411e-01 ppl=2.13 best_loss=8.2771e-01 best_ppl=2.29
Epoch 8 - |param|=9.13e+02 |g_param|=2.33e+05 loss_x2y=7.2094e-01 ppl_x2y=2.06 loss_y2x=7.0268e-01 ppl_y2x=2.02 dual_loss=0.0000e+00
Validation X2Y - loss=8.0822e-01 ppl=2.24 best_loss=8.3159e-01 best_ppl=2.30                                            
Validation Y2X - loss=7.3439e-01 ppl=2.08 best_loss=7.5411e-01 best_ppl=2.13
Epoch 9 - |param|=9.14e+02 |g_param|=2.36e+05 loss_x2y=6.8422e-01 ppl_x2y=1.98 loss_y2x=6.8764e-01 ppl_y2x=1.99 dual_loss=0.0000e+00
Validation X2Y - loss=7.5683e-01 ppl=2.13 best_loss=8.0822e-01 best_ppl=2.24                                            
Validation Y2X - loss=7.1188e-01 ppl=2.04 best_loss=7.3439e-01 best_ppl=2.08
Epoch 10 - |param|=9.14e+02 |g_param|=2.34e+05 loss_x2y=6.3633e-01 ppl_x2y=1.89 loss_y2x=6.3762e-01 ppl_y2x=1.89 dual_loss=0.0000e+00
Validation X2Y - loss=7.2227e-01 ppl=2.06 best_loss=7.5683e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.4815e-01 ppl=1.91 best_loss=7.1188e-01 best_ppl=2.04
Epoch 11 - |param|=9.14e+02 |g_param|=2.10e+05 loss_x2y=5.7656e-01 ppl_x2y=1.78 loss_y2x=5.6612e-01 ppl_y2x=1.76 dual_loss=0.0000e+00
Validation X2Y - loss=7.1072e-01 ppl=2.04 best_loss=7.2227e-01 best_ppl=2.06                                            
Validation Y2X - loss=6.4611e-01 ppl=1.91 best_loss=6.4815e-01 best_ppl=1.91
Epoch 12 - |param|=9.15e+02 |g_param|=1.97e+05 loss_x2y=4.8762e-01 ppl_x2y=1.63 loss_y2x=4.9202e-01 ppl_y2x=1.64 dual_loss=0.0000e+00
Validation X2Y - loss=6.7929e-01 ppl=1.97 best_loss=7.1072e-01 best_ppl=2.04                                            
Validation Y2X - loss=6.5097e-01 ppl=1.92 best_loss=6.4611e-01 best_ppl=1.91
Epoch 13 - |param|=9.15e+02 |g_param|=2.03e+05 loss_x2y=4.9467e-01 ppl_x2y=1.64 loss_y2x=4.8349e-01 ppl_y2x=1.62 dual_loss=0.0000e+00
Validation X2Y - loss=7.0092e-01 ppl=2.02 best_loss=6.7929e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1444e-01 ppl=1.85 best_loss=6.4611e-01 best_ppl=1.91
Epoch 14 - |param|=9.15e+02 |g_param|=2.43e+05 loss_x2y=4.8831e-01 ppl_x2y=1.63 loss_y2x=4.7835e-01 ppl_y2x=1.61 dual_loss=0.0000e+00
Validation X2Y - loss=6.8989e-01 ppl=1.99 best_loss=6.7929e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.3715e-01 ppl=1.89 best_loss=6.1444e-01 best_ppl=1.85
Epoch 15 - |param|=9.16e+02 |g_param|=1.93e+05 loss_x2y=4.2890e-01 ppl_x2y=1.54 loss_y2x=4.2091e-01 ppl_y2x=1.52 dual_loss=0.0000e+00
Validation X2Y - loss=6.9402e-01 ppl=2.00 best_loss=6.7929e-01 best_ppl=1.97                                            
Validation Y2X - loss=5.9226e-01 ppl=1.81 best_loss=6.1444e-01 best_ppl=1.85
Epoch 16 - |param|=9.16e+02 |g_param|=2.16e+05 loss_x2y=4.4575e-01 ppl_x2y=1.56 loss_y2x=4.3092e-01 ppl_y2x=1.54 dual_loss=0.0000e+00
Validation X2Y - loss=6.8224e-01 ppl=1.98 best_loss=6.7929e-01 best_ppl=1.97                                            
Validation Y2X - loss=5.8312e-01 ppl=1.79 best_loss=5.9226e-01 best_ppl=1.81
Epoch 17 - |param|=9.16e+02 |g_param|=1.93e+05 loss_x2y=3.9561e-01 ppl_x2y=1.49 loss_y2x=3.9700e-01 ppl_y2x=1.49 dual_loss=0.0000e+00
Validation X2Y - loss=6.5831e-01 ppl=1.93 best_loss=6.7929e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1607e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 18 - |param|=9.17e+02 |g_param|=2.06e+05 loss_x2y=3.7213e-01 ppl_x2y=1.45 loss_y2x=3.7247e-01 ppl_y2x=1.45 dual_loss=0.0000e+00
Validation X2Y - loss=6.7264e-01 ppl=1.96 best_loss=6.5831e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.3445e-01 ppl=1.89 best_loss=5.8312e-01 best_ppl=1.79
Epoch 19 - |param|=9.17e+02 |g_param|=1.96e+05 loss_x2y=3.8067e-01 ppl_x2y=1.46 loss_y2x=3.5993e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.6333e-01 ppl=1.94 best_loss=6.5831e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.0246e-01 ppl=1.83 best_loss=5.8312e-01 best_ppl=1.79
Epoch 20 - |param|=9.18e+02 |g_param|=1.80e+05 loss_x2y=3.2699e-01 ppl_x2y=1.39 loss_y2x=3.2116e-01 ppl_y2x=1.38 dual_loss=0.0000e+00
Validation X2Y - loss=6.8898e-01 ppl=1.99 best_loss=6.5831e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.1353e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 21 - |param|=9.18e+02 |g_param|=2.00e+05 loss_x2y=3.5576e-01 ppl_x2y=1.43 loss_y2x=3.8387e-01 ppl_y2x=1.47 dual_loss=5.6384e-01
Validation X2Y - loss=6.5901e-01 ppl=1.93 best_loss=6.5831e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.0216e-01 ppl=1.83 best_loss=5.8312e-01 best_ppl=1.79
Epoch 22 - |param|=9.18e+02 |g_param|=3.12e+05 loss_x2y=3.4592e-01 ppl_x2y=1.41 loss_y2x=3.4680e-01 ppl_y2x=1.41 dual_loss=4.8116e-01
Validation X2Y - loss=6.4610e-01 ppl=1.91 best_loss=6.5831e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.8468e-01 ppl=1.79 best_loss=5.8312e-01 best_ppl=1.79
Epoch 23 - |param|=9.19e+02 |g_param|=3.17e+05 loss_x2y=3.2864e-01 ppl_x2y=1.39 loss_y2x=3.2407e-01 ppl_y2x=1.38 dual_loss=3.8075e-01
Validation X2Y - loss=6.5099e-01 ppl=1.92 best_loss=6.4610e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.1771e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 24 - |param|=9.19e+02 |g_param|=2.97e+05 loss_x2y=3.0545e-01 ppl_x2y=1.36 loss_y2x=3.1063e-01 ppl_y2x=1.36 dual_loss=3.6292e-01
Validation X2Y - loss=6.3822e-01 ppl=1.89 best_loss=6.4610e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.0162e-01 ppl=1.83 best_loss=5.8312e-01 best_ppl=1.79
Epoch 25 - |param|=9.20e+02 |g_param|=3.30e+05 loss_x2y=3.0583e-01 ppl_x2y=1.36 loss_y2x=3.0747e-01 ppl_y2x=1.36 dual_loss=4.4909e-01
Validation X2Y - loss=6.4786e-01 ppl=1.91 best_loss=6.3822e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9805e-01 ppl=1.82 best_loss=5.8312e-01 best_ppl=1.79
Epoch 26 - |param|=9.20e+02 |g_param|=3.54e+05 loss_x2y=2.9390e-01 ppl_x2y=1.34 loss_y2x=2.9982e-01 ppl_y2x=1.35 dual_loss=3.7566e-01
Validation X2Y - loss=6.5749e-01 ppl=1.93 best_loss=6.3822e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9261e-01 ppl=1.81 best_loss=5.8312e-01 best_ppl=1.79
Epoch 27 - |param|=9.20e+02 |g_param|=4.05e+05 loss_x2y=2.8598e-01 ppl_x2y=1.33 loss_y2x=2.8244e-01 ppl_y2x=1.33 dual_loss=4.0886e-01
Validation X2Y - loss=6.6172e-01 ppl=1.94 best_loss=6.3822e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1401e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 28 - |param|=9.21e+02 |g_param|=3.79e+05 loss_x2y=2.6971e-01 ppl_x2y=1.31 loss_y2x=2.6851e-01 ppl_y2x=1.31 dual_loss=3.6511e-01
Validation X2Y - loss=6.3516e-01 ppl=1.89 best_loss=6.3822e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1985e-01 ppl=1.86 best_loss=5.8312e-01 best_ppl=1.79
Epoch 29 - |param|=9.21e+02 |g_param|=3.65e+05 loss_x2y=2.7227e-01 ppl_x2y=1.31 loss_y2x=2.6327e-01 ppl_y2x=1.30 dual_loss=3.4471e-01
Validation X2Y - loss=6.6539e-01 ppl=1.95 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8964e-01 ppl=1.80 best_loss=5.8312e-01 best_ppl=1.79
Epoch 30 - |param|=9.22e+02 |g_param|=3.87e+05 loss_x2y=2.5811e-01 ppl_x2y=1.29 loss_y2x=2.6389e-01 ppl_y2x=1.30 dual_loss=3.5969e-01
Validation X2Y - loss=6.7464e-01 ppl=1.96 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9840e-01 ppl=1.82 best_loss=5.8312e-01 best_ppl=1.79
Epoch 31 - |param|=9.22e+02 |g_param|=3.62e+05 loss_x2y=2.5734e-01 ppl_x2y=1.29 loss_y2x=2.5770e-01 ppl_y2x=1.29 dual_loss=3.6429e-01
Validation X2Y - loss=6.6037e-01 ppl=1.94 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0988e-01 ppl=1.84 best_loss=5.8312e-01 best_ppl=1.79
Epoch 32 - |param|=9.22e+02 |g_param|=3.58e+05 loss_x2y=2.4163e-01 ppl_x2y=1.27 loss_y2x=2.3951e-01 ppl_y2x=1.27 dual_loss=3.6315e-01
Validation X2Y - loss=6.6157e-01 ppl=1.94 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1705e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 33 - |param|=9.23e+02 |g_param|=3.54e+05 loss_x2y=2.5315e-01 ppl_x2y=1.29 loss_y2x=2.5331e-01 ppl_y2x=1.29 dual_loss=4.8625e-01
Validation X2Y - loss=6.6398e-01 ppl=1.94 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1993e-01 ppl=1.86 best_loss=5.8312e-01 best_ppl=1.79
Epoch 34 - |param|=9.23e+02 |g_param|=3.38e+05 loss_x2y=2.2416e-01 ppl_x2y=1.25 loss_y2x=2.1973e-01 ppl_y2x=1.25 dual_loss=3.2246e-01
Validation X2Y - loss=6.5859e-01 ppl=1.93 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1939e-01 ppl=1.86 best_loss=5.8312e-01 best_ppl=1.79
Epoch 35 - |param|=9.24e+02 |g_param|=3.29e+05 loss_x2y=2.3131e-01 ppl_x2y=1.26 loss_y2x=2.3361e-01 ppl_y2x=1.26 dual_loss=3.5907e-01
Validation X2Y - loss=6.6109e-01 ppl=1.94 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1532e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 36 - |param|=9.24e+02 |g_param|=3.13e+05 loss_x2y=2.1324e-01 ppl_x2y=1.24 loss_y2x=2.1037e-01 ppl_y2x=1.23 dual_loss=3.3443e-01
Validation X2Y - loss=6.8256e-01 ppl=1.98 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2620e-01 ppl=1.87 best_loss=5.8312e-01 best_ppl=1.79
Epoch 37 - |param|=9.24e+02 |g_param|=3.30e+05 loss_x2y=2.1429e-01 ppl_x2y=1.24 loss_y2x=2.2050e-01 ppl_y2x=1.25 dual_loss=3.4204e-01
Validation X2Y - loss=6.6654e-01 ppl=1.95 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0746e-01 ppl=1.84 best_loss=5.8312e-01 best_ppl=1.79
Epoch 38 - |param|=9.25e+02 |g_param|=3.48e+05 loss_x2y=2.2836e-01 ppl_x2y=1.26 loss_y2x=2.1675e-01 ppl_y2x=1.24 dual_loss=4.2892e-01
Validation X2Y - loss=6.6857e-01 ppl=1.95 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0168e-01 ppl=1.83 best_loss=5.8312e-01 best_ppl=1.79
Epoch 39 - |param|=9.25e+02 |g_param|=2.54e+05 loss_x2y=2.1443e-01 ppl_x2y=1.24 loss_y2x=2.0553e-01 ppl_y2x=1.23 dual_loss=3.3932e-01
Validation X2Y - loss=6.5797e-01 ppl=1.93 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9709e-01 ppl=1.82 best_loss=5.8312e-01 best_ppl=1.79
Epoch 40 - |param|=9.26e+02 |g_param|=2.39e+05 loss_x2y=1.9999e-01 ppl_x2y=1.22 loss_y2x=2.0609e-01 ppl_y2x=1.23 dual_loss=3.3609e-01
Validation X2Y - loss=6.6331e-01 ppl=1.94 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0917e-01 ppl=1.84 best_loss=5.8312e-01 best_ppl=1.79
Epoch 41 - |param|=9.26e+02 |g_param|=2.47e+05 loss_x2y=2.0498e-01 ppl_x2y=1.23 loss_y2x=2.0354e-01 ppl_y2x=1.23 dual_loss=3.4111e-01
Validation X2Y - loss=6.7690e-01 ppl=1.97 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1700e-01 ppl=1.85 best_loss=5.8312e-01 best_ppl=1.79
Epoch 42 - |param|=9.26e+02 |g_param|=2.44e+05 loss_x2y=1.9463e-01 ppl_x2y=1.21 loss_y2x=1.9776e-01 ppl_y2x=1.22 dual_loss=3.6505e-01
Validation X2Y - loss=6.8397e-01 ppl=1.98 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5325e-01 ppl=1.92 best_loss=5.8312e-01 best_ppl=1.79
Epoch 43 - |param|=9.27e+02 |g_param|=2.38e+05 loss_x2y=1.8687e-01 ppl_x2y=1.21 loss_y2x=1.8512e-01 ppl_y2x=1.20 dual_loss=3.2270e-01
Validation X2Y - loss=6.9643e-01 ppl=2.01 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4868e-01 ppl=1.91 best_loss=5.8312e-01 best_ppl=1.79
Epoch 44 - |param|=9.27e+02 |g_param|=2.41e+05 loss_x2y=1.8354e-01 ppl_x2y=1.20 loss_y2x=1.8156e-01 ppl_y2x=1.20 dual_loss=3.6274e-01
Validation X2Y - loss=6.9061e-01 ppl=1.99 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2827e-01 ppl=1.87 best_loss=5.8312e-01 best_ppl=1.79
Epoch 45 - |param|=9.28e+02 |g_param|=2.62e+05 loss_x2y=1.9360e-01 ppl_x2y=1.21 loss_y2x=1.8617e-01 ppl_y2x=1.20 dual_loss=3.7778e-01
Validation X2Y - loss=7.3441e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2055e-01 ppl=1.86 best_loss=5.8312e-01 best_ppl=1.79
Epoch 46 - |param|=9.28e+02 |g_param|=4.14e+05 loss_x2y=1.7766e-01 ppl_x2y=1.19 loss_y2x=1.7416e-01 ppl_y2x=1.19 dual_loss=4.1107e-01
Validation X2Y - loss=6.9528e-01 ppl=2.00 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4604e-01 ppl=1.91 best_loss=5.8312e-01 best_ppl=1.79
Epoch 47 - |param|=9.28e+02 |g_param|=4.06e+05 loss_x2y=1.7540e-01 ppl_x2y=1.19 loss_y2x=1.7400e-01 ppl_y2x=1.19 dual_loss=3.9059e-01
Validation X2Y - loss=6.9787e-01 ppl=2.01 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3249e-01 ppl=1.88 best_loss=5.8312e-01 best_ppl=1.79
Epoch 48 - |param|=9.29e+02 |g_param|=4.20e+05 loss_x2y=1.7600e-01 ppl_x2y=1.19 loss_y2x=1.7277e-01 ppl_y2x=1.19 dual_loss=3.1946e-01
Validation X2Y - loss=7.0424e-01 ppl=2.02 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1961e-01 ppl=1.86 best_loss=5.8312e-01 best_ppl=1.79
Epoch 49 - |param|=9.29e+02 |g_param|=4.06e+05 loss_x2y=1.7167e-01 ppl_x2y=1.19 loss_y2x=1.6930e-01 ppl_y2x=1.18 dual_loss=3.3739e-01
Validation X2Y - loss=6.9600e-01 ppl=2.01 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3116e-01 ppl=1.88 best_loss=5.8312e-01 best_ppl=1.79
Epoch 50 - |param|=9.30e+02 |g_param|=4.10e+05 loss_x2y=1.6257e-01 ppl_x2y=1.18 loss_y2x=1.6215e-01 ppl_y2x=1.18 dual_loss=3.5314e-01
Validation X2Y - loss=7.1332e-01 ppl=2.04 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3329e-01 ppl=1.88 best_loss=5.8312e-01 best_ppl=1.79
Epoch 51 - |param|=9.30e+02 |g_param|=3.89e+05 loss_x2y=1.6384e-01 ppl_x2y=1.18 loss_y2x=1.6485e-01 ppl_y2x=1.18 dual_loss=3.3140e-01
Validation X2Y - loss=7.1653e-01 ppl=2.05 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3755e-01 ppl=1.89 best_loss=5.8312e-01 best_ppl=1.79
Epoch 52 - |param|=9.30e+02 |g_param|=4.17e+05 loss_x2y=1.6677e-01 ppl_x2y=1.18 loss_y2x=1.6072e-01 ppl_y2x=1.17 dual_loss=3.8855e-01
Validation X2Y - loss=7.3276e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4373e-01 ppl=1.90 best_loss=5.8312e-01 best_ppl=1.79
Epoch 53 - |param|=9.31e+02 |g_param|=3.95e+05 loss_x2y=1.5878e-01 ppl_x2y=1.17 loss_y2x=1.5987e-01 ppl_y2x=1.17 dual_loss=3.6849e-01
Validation X2Y - loss=7.1834e-01 ppl=2.05 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4141e-01 ppl=1.90 best_loss=5.8312e-01 best_ppl=1.79
Epoch 54 - |param|=9.31e+02 |g_param|=4.01e+05 loss_x2y=1.5553e-01 ppl_x2y=1.17 loss_y2x=1.5639e-01 ppl_y2x=1.17 dual_loss=3.4122e-01
Validation X2Y - loss=7.2260e-01 ppl=2.06 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2358e-01 ppl=1.87 best_loss=5.8312e-01 best_ppl=1.79
Epoch 55 - |param|=9.32e+02 |g_param|=4.20e+05 loss_x2y=1.6302e-01 ppl_x2y=1.18 loss_y2x=1.5949e-01 ppl_y2x=1.17 dual_loss=3.7262e-01
Validation X2Y - loss=7.4756e-01 ppl=2.11 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5513e-01 ppl=1.93 best_loss=5.8312e-01 best_ppl=1.79
Epoch 56 - |param|=9.32e+02 |g_param|=4.28e+05 loss_x2y=1.5497e-01 ppl_x2y=1.17 loss_y2x=1.5067e-01 ppl_y2x=1.16 dual_loss=3.8778e-01
Validation X2Y - loss=7.2612e-01 ppl=2.07 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5677e-01 ppl=1.93 best_loss=5.8312e-01 best_ppl=1.79
Epoch 57 - |param|=9.32e+02 |g_param|=3.80e+05 loss_x2y=1.4696e-01 ppl_x2y=1.16 loss_y2x=1.4625e-01 ppl_y2x=1.16 dual_loss=3.2665e-01
Validation X2Y - loss=7.3000e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3674e-01 ppl=1.89 best_loss=5.8312e-01 best_ppl=1.79
Epoch 58 - |param|=9.33e+02 |g_param|=4.08e+05 loss_x2y=1.5158e-01 ppl_x2y=1.16 loss_y2x=1.4874e-01 ppl_y2x=1.16 dual_loss=3.7223e-01
Validation X2Y - loss=7.3137e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5879e-01 ppl=1.93 best_loss=5.8312e-01 best_ppl=1.79
Epoch 59 - |param|=9.33e+02 |g_param|=4.16e+05 loss_x2y=1.4521e-01 ppl_x2y=1.16 loss_y2x=1.4665e-01 ppl_y2x=1.16 dual_loss=3.1929e-01
Validation X2Y - loss=7.3108e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4588e-01 ppl=1.91 best_loss=5.8312e-01 best_ppl=1.79
Epoch 60 - |param|=9.34e+02 |g_param|=4.31e+05 loss_x2y=1.4361e-01 ppl_x2y=1.15 loss_y2x=1.4251e-01 ppl_y2x=1.15 dual_loss=4.0316e-01
Validation X2Y - loss=7.2372e-01 ppl=2.06 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3837e-01 ppl=1.89 best_loss=5.8312e-01 best_ppl=1.79
Epoch 61 - |param|=9.34e+02 |g_param|=4.39e+05 loss_x2y=1.4553e-01 ppl_x2y=1.16 loss_y2x=1.4234e-01 ppl_y2x=1.15 dual_loss=3.7480e-01
Validation X2Y - loss=7.5459e-01 ppl=2.13 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6514e-01 ppl=1.94 best_loss=5.8312e-01 best_ppl=1.79
Epoch 62 - |param|=9.34e+02 |g_param|=4.15e+05 loss_x2y=1.3910e-01 ppl_x2y=1.15 loss_y2x=1.4327e-01 ppl_y2x=1.15 dual_loss=3.6940e-01
Validation X2Y - loss=7.3485e-01 ppl=2.09 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6243e-01 ppl=1.94 best_loss=5.8312e-01 best_ppl=1.79
Epoch 63 - |param|=9.35e+02 |g_param|=4.26e+05 loss_x2y=1.4157e-01 ppl_x2y=1.15 loss_y2x=1.4623e-01 ppl_y2x=1.16 dual_loss=3.8955e-01
Validation X2Y - loss=7.4768e-01 ppl=2.11 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6579e-01 ppl=1.95 best_loss=5.8312e-01 best_ppl=1.79
Epoch 64 - |param|=9.35e+02 |g_param|=4.72e+05 loss_x2y=1.4097e-01 ppl_x2y=1.15 loss_y2x=1.4415e-01 ppl_y2x=1.16 dual_loss=4.8369e-01
Validation X2Y - loss=7.2869e-01 ppl=2.07 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7259e-01 ppl=1.96 best_loss=5.8312e-01 best_ppl=1.79
Epoch 65 - |param|=9.36e+02 |g_param|=4.55e+05 loss_x2y=1.3870e-01 ppl_x2y=1.15 loss_y2x=1.3810e-01 ppl_y2x=1.15 dual_loss=3.7932e-01
Validation X2Y - loss=7.4276e-01 ppl=2.10 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7070e-01 ppl=1.96 best_loss=5.8312e-01 best_ppl=1.79
Epoch 66 - |param|=9.36e+02 |g_param|=6.31e+05 loss_x2y=1.3730e-01 ppl_x2y=1.15 loss_y2x=1.3401e-01 ppl_y2x=1.14 dual_loss=3.4972e-01
Validation X2Y - loss=7.3290e-01 ppl=2.08 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7111e-01 ppl=1.96 best_loss=5.8312e-01 best_ppl=1.79
Epoch 67 - |param|=9.36e+02 |g_param|=7.13e+05 loss_x2y=1.2684e-01 ppl_x2y=1.14 loss_y2x=1.2829e-01 ppl_y2x=1.14 dual_loss=3.6474e-01
Validation X2Y - loss=7.3863e-01 ppl=2.09 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8938e-01 ppl=1.99 best_loss=5.8312e-01 best_ppl=1.79
Epoch 68 - |param|=9.37e+02 |g_param|=8.49e+05 loss_x2y=1.3737e-01 ppl_x2y=1.15 loss_y2x=1.3239e-01 ppl_y2x=1.14 dual_loss=4.1775e-01
Validation X2Y - loss=7.6711e-01 ppl=2.15 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6157e-01 ppl=1.94 best_loss=5.8312e-01 best_ppl=1.79
Epoch 69 - |param|=9.37e+02 |g_param|=4.40e+05 loss_x2y=1.2711e-01 ppl_x2y=1.14 loss_y2x=1.2550e-01 ppl_y2x=1.13 dual_loss=3.5322e-01
Validation X2Y - loss=7.4674e-01 ppl=2.11 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9760e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 70 - |param|=9.37e+02 |g_param|=4.13e+05 loss_x2y=1.2976e-01 ppl_x2y=1.14 loss_y2x=1.2559e-01 ppl_y2x=1.13 dual_loss=3.5517e-01
Validation X2Y - loss=7.5432e-01 ppl=2.13 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8471e-01 ppl=1.98 best_loss=5.8312e-01 best_ppl=1.79
Epoch 71 - |param|=9.38e+02 |g_param|=3.54e+05 loss_x2y=1.2543e-01 ppl_x2y=1.13 loss_y2x=1.3065e-01 ppl_y2x=1.14 dual_loss=4.1865e-01
Validation X2Y - loss=7.3590e-01 ppl=2.09 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8382e-01 ppl=1.98 best_loss=5.8312e-01 best_ppl=1.79
Epoch 72 - |param|=9.38e+02 |g_param|=2.71e+05 loss_x2y=1.2116e-01 ppl_x2y=1.13 loss_y2x=1.1860e-01 ppl_y2x=1.13 dual_loss=3.3272e-01
Validation X2Y - loss=7.6417e-01 ppl=2.15 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7076e-01 ppl=1.96 best_loss=5.8312e-01 best_ppl=1.79
Epoch 73 - |param|=9.39e+02 |g_param|=2.54e+05 loss_x2y=1.1808e-01 ppl_x2y=1.13 loss_y2x=1.1839e-01 ppl_y2x=1.13 dual_loss=3.4640e-01
Validation X2Y - loss=7.6841e-01 ppl=2.16 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0488e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 74 - |param|=9.39e+02 |g_param|=2.83e+05 loss_x2y=1.2463e-01 ppl_x2y=1.13 loss_y2x=1.2554e-01 ppl_y2x=1.13 dual_loss=3.8014e-01
Validation X2Y - loss=7.6903e-01 ppl=2.16 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8118e-01 ppl=1.98 best_loss=5.8312e-01 best_ppl=1.79
Epoch 75 - |param|=9.39e+02 |g_param|=2.74e+05 loss_x2y=1.1605e-01 ppl_x2y=1.12 loss_y2x=1.1749e-01 ppl_y2x=1.12 dual_loss=3.5130e-01
Validation X2Y - loss=7.9031e-01 ppl=2.20 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0339e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 76 - |param|=9.40e+02 |g_param|=2.58e+05 loss_x2y=1.1511e-01 ppl_x2y=1.12 loss_y2x=1.1878e-01 ppl_y2x=1.13 dual_loss=3.4332e-01
Validation X2Y - loss=8.0009e-01 ppl=2.23 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8297e-01 ppl=1.98 best_loss=5.8312e-01 best_ppl=1.79
Epoch 77 - |param|=9.40e+02 |g_param|=2.72e+05 loss_x2y=1.1744e-01 ppl_x2y=1.12 loss_y2x=1.1915e-01 ppl_y2x=1.13 dual_loss=3.3778e-01
Validation X2Y - loss=8.0747e-01 ppl=2.24 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9855e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 78 - |param|=9.40e+02 |g_param|=2.84e+05 loss_x2y=1.1719e-01 ppl_x2y=1.12 loss_y2x=1.2255e-01 ppl_y2x=1.13 dual_loss=3.9410e-01
Validation X2Y - loss=7.6779e-01 ppl=2.15 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8507e-01 ppl=1.98 best_loss=5.8312e-01 best_ppl=1.79
Epoch 79 - |param|=9.41e+02 |g_param|=2.50e+05 loss_x2y=1.0964e-01 ppl_x2y=1.12 loss_y2x=1.0972e-01 ppl_y2x=1.12 dual_loss=3.4609e-01
Validation X2Y - loss=7.7521e-01 ppl=2.17 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9304e-01 ppl=2.00 best_loss=5.8312e-01 best_ppl=1.79
Epoch 80 - |param|=9.41e+02 |g_param|=4.76e+05 loss_x2y=1.1303e-01 ppl_x2y=1.12 loss_y2x=1.1198e-01 ppl_y2x=1.12 dual_loss=4.2354e-01
Validation X2Y - loss=7.7063e-01 ppl=2.16 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9591e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 81 - |param|=9.42e+02 |g_param|=4.13e+05 loss_x2y=1.0792e-01 ppl_x2y=1.11 loss_y2x=1.1262e-01 ppl_y2x=1.12 dual_loss=3.5098e-01
Validation X2Y - loss=7.9013e-01 ppl=2.20 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.1535e-01 ppl=2.04 best_loss=5.8312e-01 best_ppl=1.79
Epoch 82 - |param|=9.42e+02 |g_param|=3.03e+05 loss_x2y=1.1590e-01 ppl_x2y=1.12 loss_y2x=1.1438e-01 ppl_y2x=1.12 dual_loss=3.8133e-01
Validation X2Y - loss=8.0057e-01 ppl=2.23 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8838e-01 ppl=1.99 best_loss=5.8312e-01 best_ppl=1.79
Epoch 83 - |param|=9.42e+02 |g_param|=2.61e+05 loss_x2y=1.0982e-01 ppl_x2y=1.12 loss_y2x=1.1037e-01 ppl_y2x=1.12 dual_loss=3.6656e-01
Validation X2Y - loss=7.9224e-01 ppl=2.21 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0259e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 84 - |param|=9.43e+02 |g_param|=2.52e+05 loss_x2y=1.0561e-01 ppl_x2y=1.11 loss_y2x=1.0715e-01 ppl_y2x=1.11 dual_loss=3.2498e-01
Validation X2Y - loss=7.8666e-01 ppl=2.20 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9785e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 85 - |param|=9.43e+02 |g_param|=2.56e+05 loss_x2y=1.0734e-01 ppl_x2y=1.11 loss_y2x=1.0708e-01 ppl_y2x=1.11 dual_loss=3.7756e-01
Validation X2Y - loss=7.9892e-01 ppl=2.22 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9877e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 86 - |param|=9.44e+02 |g_param|=2.61e+05 loss_x2y=1.0590e-01 ppl_x2y=1.11 loss_y2x=1.0617e-01 ppl_y2x=1.11 dual_loss=3.4213e-01
Validation X2Y - loss=8.0004e-01 ppl=2.23 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9963e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 87 - |param|=9.44e+02 |g_param|=2.67e+05 loss_x2y=1.1010e-01 ppl_x2y=1.12 loss_y2x=1.0974e-01 ppl_y2x=1.12 dual_loss=4.3683e-01
Validation X2Y - loss=7.9955e-01 ppl=2.22 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0328e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 88 - |param|=9.44e+02 |g_param|=2.58e+05 loss_x2y=1.0654e-01 ppl_x2y=1.11 loss_y2x=1.0630e-01 ppl_y2x=1.11 dual_loss=3.8609e-01
Validation X2Y - loss=7.9576e-01 ppl=2.22 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0582e-01 ppl=2.03 best_loss=5.8312e-01 best_ppl=1.79
Epoch 89 - |param|=9.45e+02 |g_param|=2.52e+05 loss_x2y=1.0206e-01 ppl_x2y=1.11 loss_y2x=1.0235e-01 ppl_y2x=1.11 dual_loss=3.5149e-01
Validation X2Y - loss=8.1425e-01 ppl=2.26 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9776e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 90 - |param|=9.45e+02 |g_param|=2.68e+05 loss_x2y=1.0444e-01 ppl_x2y=1.11 loss_y2x=1.0295e-01 ppl_y2x=1.11 dual_loss=3.8046e-01
Validation X2Y - loss=8.2164e-01 ppl=2.27 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0524e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 91 - |param|=9.45e+02 |g_param|=2.48e+05 loss_x2y=1.0513e-01 ppl_x2y=1.11 loss_y2x=1.0422e-01 ppl_y2x=1.11 dual_loss=3.4118e-01
Validation X2Y - loss=7.9525e-01 ppl=2.21 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0729e-01 ppl=2.03 best_loss=5.8312e-01 best_ppl=1.79
Epoch 92 - |param|=9.46e+02 |g_param|=3.82e+05 loss_x2y=1.0358e-01 ppl_x2y=1.11 loss_y2x=1.0017e-01 ppl_y2x=1.11 dual_loss=4.1587e-01
Validation X2Y - loss=8.1745e-01 ppl=2.26 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.1164e-01 ppl=2.04 best_loss=5.8312e-01 best_ppl=1.79
Epoch 93 - |param|=9.46e+02 |g_param|=4.03e+05 loss_x2y=1.0208e-01 ppl_x2y=1.11 loss_y2x=9.9019e-02 ppl_y2x=1.10 dual_loss=3.6586e-01
Validation X2Y - loss=8.2741e-01 ppl=2.29 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9831e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 94 - |param|=9.47e+02 |g_param|=3.91e+05 loss_x2y=1.0075e-01 ppl_x2y=1.11 loss_y2x=1.0424e-01 ppl_y2x=1.11 dual_loss=3.8623e-01
Validation X2Y - loss=8.2040e-01 ppl=2.27 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0389e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 95 - |param|=9.47e+02 |g_param|=3.52e+05 loss_x2y=9.2865e-02 ppl_x2y=1.10 loss_y2x=9.4720e-02 ppl_y2x=1.10 dual_loss=3.4656e-01
Validation X2Y - loss=8.2611e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0911e-01 ppl=2.03 best_loss=5.8312e-01 best_ppl=1.79
Epoch 96 - |param|=9.47e+02 |g_param|=3.88e+05 loss_x2y=1.0200e-01 ppl_x2y=1.11 loss_y2x=1.0276e-01 ppl_y2x=1.11 dual_loss=4.0421e-01
Validation X2Y - loss=8.2273e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9571e-01 ppl=2.01 best_loss=5.8312e-01 best_ppl=1.79
Epoch 97 - |param|=9.48e+02 |g_param|=3.97e+05 loss_x2y=1.0263e-01 ppl_x2y=1.11 loss_y2x=9.8080e-02 ppl_y2x=1.10 dual_loss=4.0780e-01
Validation X2Y - loss=8.1194e-01 ppl=2.25 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2558e-01 ppl=2.07 best_loss=5.8312e-01 best_ppl=1.79
Epoch 98 - |param|=9.48e+02 |g_param|=3.58e+05 loss_x2y=9.5158e-02 ppl_x2y=1.10 loss_y2x=9.8779e-02 ppl_y2x=1.10 dual_loss=3.8473e-01
Validation X2Y - loss=8.3655e-01 ppl=2.31 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5231e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 99 - |param|=9.48e+02 |g_param|=3.41e+05 loss_x2y=9.5488e-02 ppl_x2y=1.10 loss_y2x=9.5536e-02 ppl_y2x=1.10 dual_loss=3.9554e-01
Validation X2Y - loss=8.1070e-01 ppl=2.25 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3334e-01 ppl=2.08 best_loss=5.8312e-01 best_ppl=1.79
Epoch 100 - |param|=9.49e+02 |g_param|=3.87e+05 loss_x2y=9.9062e-02 ppl_x2y=1.10 loss_y2x=9.6026e-02 ppl_y2x=1.10 dual_loss=3.6942e-01
Validation X2Y - loss=7.8888e-01 ppl=2.20 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2722e-01 ppl=2.07 best_loss=5.8312e-01 best_ppl=1.79
Epoch 101 - |param|=9.49e+02 |g_param|=3.65e+05 loss_x2y=9.4360e-02 ppl_x2y=1.10 loss_y2x=9.2611e-02 ppl_y2x=1.10 dual_loss=3.7674e-01
Validation X2Y - loss=8.1595e-01 ppl=2.26 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0178e-01 ppl=2.02 best_loss=5.8312e-01 best_ppl=1.79
Epoch 102 - |param|=9.50e+02 |g_param|=4.51e+05 loss_x2y=9.1689e-02 ppl_x2y=1.10 loss_y2x=9.4806e-02 ppl_y2x=1.10 dual_loss=4.1391e-01
Validation X2Y - loss=8.1890e-01 ppl=2.27 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2368e-01 ppl=2.06 best_loss=5.8312e-01 best_ppl=1.79
Epoch 103 - |param|=9.50e+02 |g_param|=3.93e+05 loss_x2y=9.6153e-02 ppl_x2y=1.10 loss_y2x=9.7769e-02 ppl_y2x=1.10 dual_loss=4.1245e-01
Validation X2Y - loss=8.0026e-01 ppl=2.23 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2438e-01 ppl=2.06 best_loss=5.8312e-01 best_ppl=1.79
Epoch 104 - |param|=9.50e+02 |g_param|=3.96e+05 loss_x2y=9.4505e-02 ppl_x2y=1.10 loss_y2x=9.7546e-02 ppl_y2x=1.10 dual_loss=4.8263e-01
Validation X2Y - loss=8.2398e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2061e-01 ppl=2.06 best_loss=5.8312e-01 best_ppl=1.79
Epoch 105 - |param|=9.51e+02 |g_param|=3.82e+05 loss_x2y=9.1408e-02 ppl_x2y=1.10 loss_y2x=9.1278e-02 ppl_y2x=1.10 dual_loss=4.0124e-01
Validation X2Y - loss=8.2211e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0963e-01 ppl=2.03 best_loss=5.8312e-01 best_ppl=1.79
Epoch 106 - |param|=9.51e+02 |g_param|=3.47e+05 loss_x2y=8.4700e-02 ppl_x2y=1.09 loss_y2x=8.5859e-02 ppl_y2x=1.09 dual_loss=3.6997e-01
Validation X2Y - loss=8.1825e-01 ppl=2.27 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4269e-01 ppl=2.10 best_loss=5.8312e-01 best_ppl=1.79
Epoch 107 - |param|=9.51e+02 |g_param|=3.58e+05 loss_x2y=9.0407e-02 ppl_x2y=1.09 loss_y2x=8.9227e-02 ppl_y2x=1.09 dual_loss=3.5831e-01
Validation X2Y - loss=8.2349e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5069e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 108 - |param|=9.52e+02 |g_param|=3.43e+05 loss_x2y=8.8428e-02 ppl_x2y=1.09 loss_y2x=8.7526e-02 ppl_y2x=1.09 dual_loss=4.3182e-01
Validation X2Y - loss=8.4838e-01 ppl=2.34 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3482e-01 ppl=2.09 best_loss=5.8312e-01 best_ppl=1.79
Epoch 109 - |param|=9.52e+02 |g_param|=3.60e+05 loss_x2y=8.9896e-02 ppl_x2y=1.09 loss_y2x=9.2265e-02 ppl_y2x=1.10 dual_loss=3.9406e-01
Validation X2Y - loss=8.2566e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3214e-01 ppl=2.08 best_loss=5.8312e-01 best_ppl=1.79
Epoch 110 - |param|=9.52e+02 |g_param|=3.44e+05 loss_x2y=8.6098e-02 ppl_x2y=1.09 loss_y2x=8.9862e-02 ppl_y2x=1.09 dual_loss=3.9346e-01
Validation X2Y - loss=8.5268e-01 ppl=2.35 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3516e-01 ppl=2.09 best_loss=5.8312e-01 best_ppl=1.79
Epoch 111 - |param|=9.53e+02 |g_param|=3.57e+05 loss_x2y=8.7685e-02 ppl_x2y=1.09 loss_y2x=8.4573e-02 ppl_y2x=1.09 dual_loss=3.6727e-01
Validation X2Y - loss=8.2579e-01 ppl=2.28 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5094e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 112 - |param|=9.53e+02 |g_param|=5.67e+05 loss_x2y=8.3395e-02 ppl_x2y=1.09 loss_y2x=8.6358e-02 ppl_y2x=1.09 dual_loss=3.8981e-01
Validation X2Y - loss=8.4954e-01 ppl=2.34 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4998e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 113 - |param|=9.54e+02 |g_param|=4.77e+05 loss_x2y=8.3034e-02 ppl_x2y=1.09 loss_y2x=8.1943e-02 ppl_y2x=1.09 dual_loss=3.8992e-01
Validation X2Y - loss=8.3468e-01 ppl=2.30 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5600e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 114 - |param|=9.54e+02 |g_param|=3.52e+05 loss_x2y=8.5738e-02 ppl_x2y=1.09 loss_y2x=8.3954e-02 ppl_y2x=1.09 dual_loss=3.8525e-01
Validation X2Y - loss=8.6552e-01 ppl=2.38 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5834e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 115 - |param|=9.54e+02 |g_param|=3.30e+05 loss_x2y=8.3216e-02 ppl_x2y=1.09 loss_y2x=8.6502e-02 ppl_y2x=1.09 dual_loss=3.8042e-01
Validation X2Y - loss=8.3449e-01 ppl=2.30 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3694e-01 ppl=2.09 best_loss=5.8312e-01 best_ppl=1.79
Epoch 116 - |param|=9.55e+02 |g_param|=3.41e+05 loss_x2y=8.1872e-02 ppl_x2y=1.09 loss_y2x=8.5466e-02 ppl_y2x=1.09 dual_loss=3.7274e-01
Validation X2Y - loss=8.4184e-01 ppl=2.32 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5161e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 117 - |param|=9.55e+02 |g_param|=3.40e+05 loss_x2y=8.4414e-02 ppl_x2y=1.09 loss_y2x=8.2176e-02 ppl_y2x=1.09 dual_loss=4.0505e-01
Validation X2Y - loss=8.6440e-01 ppl=2.37 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6125e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 118 - |param|=9.55e+02 |g_param|=3.51e+05 loss_x2y=8.3470e-02 ppl_x2y=1.09 loss_y2x=8.5602e-02 ppl_y2x=1.09 dual_loss=4.0578e-01
Validation X2Y - loss=8.5799e-01 ppl=2.36 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5511e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 119 - |param|=9.56e+02 |g_param|=3.15e+05 loss_x2y=7.8699e-02 ppl_x2y=1.08 loss_y2x=8.3691e-02 ppl_y2x=1.09 dual_loss=3.7320e-01
Validation X2Y - loss=8.6441e-01 ppl=2.37 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2514e-01 ppl=2.07 best_loss=5.8312e-01 best_ppl=1.79
Epoch 120 - |param|=9.56e+02 |g_param|=3.35e+05 loss_x2y=8.4116e-02 ppl_x2y=1.09 loss_y2x=8.3670e-02 ppl_y2x=1.09 dual_loss=3.7868e-01
Validation X2Y - loss=8.5620e-01 ppl=2.35 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3336e-01 ppl=2.08 best_loss=5.8312e-01 best_ppl=1.79
Epoch 121 - |param|=9.56e+02 |g_param|=3.34e+05 loss_x2y=8.1429e-02 ppl_x2y=1.08 loss_y2x=8.0519e-02 ppl_y2x=1.08 dual_loss=3.6908e-01
Validation X2Y - loss=8.4241e-01 ppl=2.32 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.2091e-01 ppl=2.06 best_loss=5.8312e-01 best_ppl=1.79
Epoch 122 - |param|=9.57e+02 |g_param|=3.48e+05 loss_x2y=8.2395e-02 ppl_x2y=1.09 loss_y2x=8.2162e-02 ppl_y2x=1.09 dual_loss=3.6596e-01
Validation X2Y - loss=8.5871e-01 ppl=2.36 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4531e-01 ppl=2.11 best_loss=5.8312e-01 best_ppl=1.79
Epoch 123 - |param|=9.57e+02 |g_param|=4.11e+05 loss_x2y=8.4484e-02 ppl_x2y=1.09 loss_y2x=8.3873e-02 ppl_y2x=1.09 dual_loss=4.7150e-01
Validation X2Y - loss=8.2958e-01 ppl=2.29 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5948e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 124 - |param|=9.58e+02 |g_param|=4.64e+05 loss_x2y=8.0994e-02 ppl_x2y=1.08 loss_y2x=7.7874e-02 ppl_y2x=1.08 dual_loss=4.7437e-01
Validation X2Y - loss=8.4269e-01 ppl=2.32 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4572e-01 ppl=2.11 best_loss=5.8312e-01 best_ppl=1.79
Epoch 125 - |param|=9.58e+02 |g_param|=4.31e+05 loss_x2y=8.0425e-02 ppl_x2y=1.08 loss_y2x=8.1076e-02 ppl_y2x=1.08 dual_loss=3.8108e-01
Validation X2Y - loss=8.4866e-01 ppl=2.34 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4029e-01 ppl=2.10 best_loss=5.8312e-01 best_ppl=1.79
Epoch 126 - |param|=9.58e+02 |g_param|=4.42e+05 loss_x2y=7.8196e-02 ppl_x2y=1.08 loss_y2x=7.6061e-02 ppl_y2x=1.08 dual_loss=3.7258e-01
Validation X2Y - loss=8.6225e-01 ppl=2.37 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5951e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 127 - |param|=9.59e+02 |g_param|=4.40e+05 loss_x2y=7.7866e-02 ppl_x2y=1.08 loss_y2x=7.6748e-02 ppl_y2x=1.08 dual_loss=3.8562e-01
Validation X2Y - loss=8.6366e-01 ppl=2.37 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7794e-01 ppl=2.18 best_loss=5.8312e-01 best_ppl=1.79
Epoch 128 - |param|=9.59e+02 |g_param|=4.31e+05 loss_x2y=7.9196e-02 ppl_x2y=1.08 loss_y2x=7.7156e-02 ppl_y2x=1.08 dual_loss=3.7775e-01
Validation X2Y - loss=9.0060e-01 ppl=2.46 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5919e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 129 - |param|=9.59e+02 |g_param|=4.07e+05 loss_x2y=7.4716e-02 ppl_x2y=1.08 loss_y2x=7.7006e-02 ppl_y2x=1.08 dual_loss=3.5708e-01
Validation X2Y - loss=8.7436e-01 ppl=2.40 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5913e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 130 - |param|=9.60e+02 |g_param|=4.16e+05 loss_x2y=7.7316e-02 ppl_x2y=1.08 loss_y2x=7.6984e-02 ppl_y2x=1.08 dual_loss=3.8996e-01
Validation X2Y - loss=8.4463e-01 ppl=2.33 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5854e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 131 - |param|=9.60e+02 |g_param|=4.22e+05 loss_x2y=7.4386e-02 ppl_x2y=1.08 loss_y2x=7.5058e-02 ppl_y2x=1.08 dual_loss=3.8380e-01
Validation X2Y - loss=8.5956e-01 ppl=2.36 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5785e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 132 - |param|=9.61e+02 |g_param|=4.49e+05 loss_x2y=7.6517e-02 ppl_x2y=1.08 loss_y2x=7.7749e-02 ppl_y2x=1.08 dual_loss=4.3601e-01
Validation X2Y - loss=8.5312e-01 ppl=2.35 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6182e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 133 - |param|=9.61e+02 |g_param|=4.21e+05 loss_x2y=7.4330e-02 ppl_x2y=1.08 loss_y2x=7.5546e-02 ppl_y2x=1.08 dual_loss=3.7213e-01
Validation X2Y - loss=8.8122e-01 ppl=2.41 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7277e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 134 - |param|=9.61e+02 |g_param|=6.58e+05 loss_x2y=7.6608e-02 ppl_x2y=1.08 loss_y2x=7.6865e-02 ppl_y2x=1.08 dual_loss=4.4743e-01
Validation X2Y - loss=8.6703e-01 ppl=2.38 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7026e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 135 - |param|=9.62e+02 |g_param|=6.28e+05 loss_x2y=7.3628e-02 ppl_x2y=1.08 loss_y2x=7.3225e-02 ppl_y2x=1.08 dual_loss=3.8801e-01
Validation X2Y - loss=8.8272e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7216e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 136 - |param|=9.62e+02 |g_param|=6.44e+05 loss_x2y=7.6610e-02 ppl_x2y=1.08 loss_y2x=7.3315e-02 ppl_y2x=1.08 dual_loss=4.1421e-01
Validation X2Y - loss=8.7285e-01 ppl=2.39 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4978e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 137 - |param|=9.62e+02 |g_param|=5.97e+05 loss_x2y=7.4871e-02 ppl_x2y=1.08 loss_y2x=7.7356e-02 ppl_y2x=1.08 dual_loss=3.7217e-01
Validation X2Y - loss=8.8492e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.3479e-01 ppl=2.09 best_loss=5.8312e-01 best_ppl=1.79
Epoch 138 - |param|=9.63e+02 |g_param|=4.35e+05 loss_x2y=7.2760e-02 ppl_x2y=1.08 loss_y2x=7.4392e-02 ppl_y2x=1.08 dual_loss=3.8311e-01
Validation X2Y - loss=8.8533e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4828e-01 ppl=2.11 best_loss=5.8312e-01 best_ppl=1.79
Epoch 139 - |param|=9.63e+02 |g_param|=3.96e+05 loss_x2y=7.2575e-02 ppl_x2y=1.08 loss_y2x=7.3672e-02 ppl_y2x=1.08 dual_loss=3.8377e-01
Validation X2Y - loss=8.7130e-01 ppl=2.39 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5828e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 140 - |param|=9.63e+02 |g_param|=4.09e+05 loss_x2y=7.3810e-02 ppl_x2y=1.08 loss_y2x=7.4194e-02 ppl_y2x=1.08 dual_loss=3.8554e-01
Validation X2Y - loss=8.5484e-01 ppl=2.35 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6497e-01 ppl=2.15 best_loss=5.8312e-01 best_ppl=1.79
Epoch 141 - |param|=9.64e+02 |g_param|=4.18e+05 loss_x2y=7.3683e-02 ppl_x2y=1.08 loss_y2x=7.3841e-02 ppl_y2x=1.08 dual_loss=3.8259e-01
Validation X2Y - loss=8.8404e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6299e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 142 - |param|=9.64e+02 |g_param|=4.09e+05 loss_x2y=7.4077e-02 ppl_x2y=1.08 loss_y2x=7.5497e-02 ppl_y2x=1.08 dual_loss=4.2810e-01
Validation X2Y - loss=8.7076e-01 ppl=2.39 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5199e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 143 - |param|=9.64e+02 |g_param|=4.33e+05 loss_x2y=7.1286e-02 ppl_x2y=1.07 loss_y2x=7.2001e-02 ppl_y2x=1.07 dual_loss=3.8784e-01
Validation X2Y - loss=8.8832e-01 ppl=2.43 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6530e-01 ppl=2.15 best_loss=5.8312e-01 best_ppl=1.79
Epoch 144 - |param|=9.65e+02 |g_param|=4.34e+05 loss_x2y=7.1739e-02 ppl_x2y=1.07 loss_y2x=6.9324e-02 ppl_y2x=1.07 dual_loss=3.7867e-01
Validation X2Y - loss=9.0764e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4289e-01 ppl=2.10 best_loss=5.8312e-01 best_ppl=1.79
Epoch 145 - |param|=9.65e+02 |g_param|=3.89e+05 loss_x2y=6.9617e-02 ppl_x2y=1.07 loss_y2x=7.2106e-02 ppl_y2x=1.07 dual_loss=3.6463e-01
Validation X2Y - loss=8.7652e-01 ppl=2.40 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6660e-01 ppl=2.15 best_loss=5.8312e-01 best_ppl=1.79
Epoch 146 - |param|=9.66e+02 |g_param|=4.18e+05 loss_x2y=7.2759e-02 ppl_x2y=1.08 loss_y2x=7.3116e-02 ppl_y2x=1.08 dual_loss=4.2290e-01
Validation X2Y - loss=8.8099e-01 ppl=2.41 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9410e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 147 - |param|=9.66e+02 |g_param|=3.95e+05 loss_x2y=7.0893e-02 ppl_x2y=1.07 loss_y2x=6.9712e-02 ppl_y2x=1.07 dual_loss=3.8232e-01
Validation X2Y - loss=8.9931e-01 ppl=2.46 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7545e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 148 - |param|=9.66e+02 |g_param|=4.07e+05 loss_x2y=6.9962e-02 ppl_x2y=1.07 loss_y2x=7.2048e-02 ppl_y2x=1.07 dual_loss=3.9500e-01
Validation X2Y - loss=8.9435e-01 ppl=2.45 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7845e-01 ppl=2.18 best_loss=5.8312e-01 best_ppl=1.79
Epoch 149 - |param|=9.67e+02 |g_param|=4.01e+05 loss_x2y=7.1788e-02 ppl_x2y=1.07 loss_y2x=6.8862e-02 ppl_y2x=1.07 dual_loss=4.3258e-01
Validation X2Y - loss=8.8859e-01 ppl=2.43 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7182e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 150 - |param|=9.67e+02 |g_param|=4.25e+05 loss_x2y=7.2515e-02 ppl_x2y=1.08 loss_y2x=7.2390e-02 ppl_y2x=1.08 dual_loss=4.8922e-01
Validation X2Y - loss=9.1067e-01 ppl=2.49 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5615e-01 ppl=2.13 best_loss=5.8312e-01 best_ppl=1.79
Epoch 151 - |param|=9.67e+02 |g_param|=3.82e+05 loss_x2y=6.8855e-02 ppl_x2y=1.07 loss_y2x=6.8987e-02 ppl_y2x=1.07 dual_loss=4.0844e-01
Validation X2Y - loss=8.8338e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6084e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 152 - |param|=9.68e+02 |g_param|=4.35e+05 loss_x2y=7.1268e-02 ppl_x2y=1.07 loss_y2x=7.0271e-02 ppl_y2x=1.07 dual_loss=4.8650e-01
Validation X2Y - loss=8.9443e-01 ppl=2.45 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.5061e-01 ppl=2.12 best_loss=5.8312e-01 best_ppl=1.79
Epoch 153 - |param|=9.68e+02 |g_param|=3.22e+05 loss_x2y=6.8087e-02 ppl_x2y=1.07 loss_y2x=6.6512e-02 ppl_y2x=1.07 dual_loss=3.6493e-01
Validation X2Y - loss=8.9373e-01 ppl=2.44 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6283e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 154 - |param|=9.68e+02 |g_param|=3.26e+05 loss_x2y=7.4256e-02 ppl_x2y=1.08 loss_y2x=6.9735e-02 ppl_y2x=1.07 dual_loss=4.2314e-01
Validation X2Y - loss=9.0302e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7423e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 155 - |param|=9.69e+02 |g_param|=2.84e+05 loss_x2y=6.7202e-02 ppl_x2y=1.07 loss_y2x=7.0899e-02 ppl_y2x=1.07 dual_loss=4.0112e-01
Validation X2Y - loss=8.8261e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7220e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 156 - |param|=9.69e+02 |g_param|=3.04e+05 loss_x2y=6.9529e-02 ppl_x2y=1.07 loss_y2x=6.8173e-02 ppl_y2x=1.07 dual_loss=4.2105e-01
Validation X2Y - loss=9.1119e-01 ppl=2.49 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6616e-01 ppl=2.15 best_loss=5.8312e-01 best_ppl=1.79
Epoch 157 - |param|=9.69e+02 |g_param|=2.75e+05 loss_x2y=6.6124e-02 ppl_x2y=1.07 loss_y2x=6.5448e-02 ppl_y2x=1.07 dual_loss=3.8487e-01
Validation X2Y - loss=9.1091e-01 ppl=2.49 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6050e-01 ppl=2.14 best_loss=5.8312e-01 best_ppl=1.79
Epoch 158 - |param|=9.70e+02 |g_param|=5.14e+05 loss_x2y=6.7816e-02 ppl_x2y=1.07 loss_y2x=6.8847e-02 ppl_y2x=1.07 dual_loss=3.9828e-01
Validation X2Y - loss=8.9349e-01 ppl=2.44 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.4812e-01 ppl=2.11 best_loss=5.8312e-01 best_ppl=1.79
Epoch 159 - |param|=9.70e+02 |g_param|=5.09e+05 loss_x2y=6.8653e-02 ppl_x2y=1.07 loss_y2x=7.0022e-02 ppl_y2x=1.07 dual_loss=4.0103e-01
Validation X2Y - loss=8.9784e-01 ppl=2.45 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7305e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 160 - |param|=9.71e+02 |g_param|=3.92e+05 loss_x2y=6.6238e-02 ppl_x2y=1.07 loss_y2x=6.6436e-02 ppl_y2x=1.07 dual_loss=3.7064e-01
Validation X2Y - loss=8.9043e-01 ppl=2.44 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.6968e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 161 - |param|=9.71e+02 |g_param|=2.85e+05 loss_x2y=6.2993e-02 ppl_x2y=1.07 loss_y2x=6.3491e-02 ppl_y2x=1.07 dual_loss=3.5294e-01
Validation X2Y - loss=9.0461e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8143e-01 ppl=2.18 best_loss=5.8312e-01 best_ppl=1.79
Epoch 162 - |param|=9.71e+02 |g_param|=2.90e+05 loss_x2y=6.7377e-02 ppl_x2y=1.07 loss_y2x=6.5515e-02 ppl_y2x=1.07 dual_loss=4.4041e-01
Validation X2Y - loss=9.2192e-01 ppl=2.51 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9263e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 163 - |param|=9.72e+02 |g_param|=2.98e+05 loss_x2y=7.0701e-02 ppl_x2y=1.07 loss_y2x=6.6916e-02 ppl_y2x=1.07 dual_loss=4.0015e-01
Validation X2Y - loss=9.1470e-01 ppl=2.50 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8215e-01 ppl=2.19 best_loss=5.8312e-01 best_ppl=1.79
Epoch 164 - |param|=9.72e+02 |g_param|=2.96e+05 loss_x2y=6.3696e-02 ppl_x2y=1.07 loss_y2x=6.5901e-02 ppl_y2x=1.07 dual_loss=3.9502e-01
Validation X2Y - loss=8.9787e-01 ppl=2.45 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9454e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 165 - |param|=9.72e+02 |g_param|=2.79e+05 loss_x2y=6.6068e-02 ppl_x2y=1.07 loss_y2x=6.5671e-02 ppl_y2x=1.07 dual_loss=3.8939e-01
Validation X2Y - loss=9.2261e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0600e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 166 - |param|=9.73e+02 |g_param|=2.80e+05 loss_x2y=6.3030e-02 ppl_x2y=1.07 loss_y2x=6.2265e-02 ppl_y2x=1.06 dual_loss=3.7217e-01
Validation X2Y - loss=9.0689e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8673e-01 ppl=2.20 best_loss=5.8312e-01 best_ppl=1.79
Epoch 167 - |param|=9.73e+02 |g_param|=2.88e+05 loss_x2y=6.3813e-02 ppl_x2y=1.07 loss_y2x=6.4577e-02 ppl_y2x=1.07 dual_loss=3.9128e-01
Validation X2Y - loss=8.9853e-01 ppl=2.46 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9381e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 168 - |param|=9.73e+02 |g_param|=2.76e+05 loss_x2y=6.2962e-02 ppl_x2y=1.06 loss_y2x=6.2786e-02 ppl_y2x=1.06 dual_loss=3.9158e-01
Validation X2Y - loss=9.0839e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9583e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 169 - |param|=9.74e+02 |g_param|=2.67e+05 loss_x2y=6.2693e-02 ppl_x2y=1.06 loss_y2x=6.3428e-02 ppl_y2x=1.07 dual_loss=3.6334e-01
Validation X2Y - loss=9.1453e-01 ppl=2.50 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0466e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 170 - |param|=9.74e+02 |g_param|=2.80e+05 loss_x2y=6.3689e-02 ppl_x2y=1.07 loss_y2x=6.3112e-02 ppl_y2x=1.07 dual_loss=4.1882e-01
Validation X2Y - loss=9.0081e-01 ppl=2.46 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2160e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 171 - |param|=9.74e+02 |g_param|=2.84e+05 loss_x2y=6.1184e-02 ppl_x2y=1.06 loss_y2x=5.9598e-02 ppl_y2x=1.06 dual_loss=4.0166e-01
Validation X2Y - loss=8.9330e-01 ppl=2.44 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9915e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 172 - |param|=9.75e+02 |g_param|=2.92e+05 loss_x2y=6.3714e-02 ppl_x2y=1.07 loss_y2x=6.3780e-02 ppl_y2x=1.07 dual_loss=4.2288e-01
Validation X2Y - loss=9.0959e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7637e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 173 - |param|=9.75e+02 |g_param|=2.85e+05 loss_x2y=6.4555e-02 ppl_x2y=1.07 loss_y2x=6.6593e-02 ppl_y2x=1.07 dual_loss=4.3650e-01
Validation X2Y - loss=8.8547e-01 ppl=2.42 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7913e-01 ppl=2.18 best_loss=5.8312e-01 best_ppl=1.79
Epoch 174 - |param|=9.76e+02 |g_param|=3.74e+05 loss_x2y=6.2330e-02 ppl_x2y=1.06 loss_y2x=6.3178e-02 ppl_y2x=1.07 dual_loss=3.7875e-01
Validation X2Y - loss=9.0143e-01 ppl=2.46 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1384e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 175 - |param|=9.76e+02 |g_param|=3.55e+05 loss_x2y=6.0747e-02 ppl_x2y=1.06 loss_y2x=5.8799e-02 ppl_y2x=1.06 dual_loss=3.8255e-01
Validation X2Y - loss=9.1951e-01 ppl=2.51 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9321e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 176 - |param|=9.76e+02 |g_param|=3.78e+05 loss_x2y=6.3227e-02 ppl_x2y=1.07 loss_y2x=6.4325e-02 ppl_y2x=1.07 dual_loss=4.1684e-01
Validation X2Y - loss=9.3062e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2657e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 177 - |param|=9.77e+02 |g_param|=3.65e+05 loss_x2y=6.2546e-02 ppl_x2y=1.06 loss_y2x=6.4428e-02 ppl_y2x=1.07 dual_loss=4.9175e-01
Validation X2Y - loss=9.0355e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2104e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 178 - |param|=9.77e+02 |g_param|=3.88e+05 loss_x2y=6.2614e-02 ppl_x2y=1.06 loss_y2x=6.0323e-02 ppl_y2x=1.06 dual_loss=4.0595e-01
Validation X2Y - loss=9.0597e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2044e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 179 - |param|=9.77e+02 |g_param|=3.54e+05 loss_x2y=5.8289e-02 ppl_x2y=1.06 loss_y2x=5.9074e-02 ppl_y2x=1.06 dual_loss=3.8691e-01
Validation X2Y - loss=9.3454e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1230e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 180 - |param|=9.78e+02 |g_param|=3.72e+05 loss_x2y=6.3099e-02 ppl_x2y=1.07 loss_y2x=6.3063e-02 ppl_y2x=1.07 dual_loss=3.7908e-01
Validation X2Y - loss=9.2539e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1843e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 181 - |param|=9.78e+02 |g_param|=5.12e+05 loss_x2y=6.0778e-02 ppl_x2y=1.06 loss_y2x=6.2082e-02 ppl_y2x=1.06 dual_loss=4.4996e-01
Validation X2Y - loss=9.2353e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2124e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 182 - |param|=9.78e+02 |g_param|=5.05e+05 loss_x2y=6.5081e-02 ppl_x2y=1.07 loss_y2x=5.9640e-02 ppl_y2x=1.06 dual_loss=5.0934e-01
Validation X2Y - loss=9.0347e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2837e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 183 - |param|=9.79e+02 |g_param|=3.31e+05 loss_x2y=6.0414e-02 ppl_x2y=1.06 loss_y2x=5.7627e-02 ppl_y2x=1.06 dual_loss=3.7597e-01
Validation X2Y - loss=9.2288e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1343e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 184 - |param|=9.79e+02 |g_param|=2.77e+05 loss_x2y=6.0585e-02 ppl_x2y=1.06 loss_y2x=5.9658e-02 ppl_y2x=1.06 dual_loss=3.7906e-01
Validation X2Y - loss=9.2400e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8179e-01 ppl=2.19 best_loss=5.8312e-01 best_ppl=1.79
Epoch 185 - |param|=9.79e+02 |g_param|=2.61e+05 loss_x2y=6.1802e-02 ppl_x2y=1.06 loss_y2x=6.2322e-02 ppl_y2x=1.06 dual_loss=4.0625e-01
Validation X2Y - loss=9.0899e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2727e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 186 - |param|=9.80e+02 |g_param|=2.59e+05 loss_x2y=6.1992e-02 ppl_x2y=1.06 loss_y2x=5.9365e-02 ppl_y2x=1.06 dual_loss=4.1155e-01
Validation X2Y - loss=8.9664e-01 ppl=2.45 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1108e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 187 - |param|=9.80e+02 |g_param|=2.78e+05 loss_x2y=6.1597e-02 ppl_x2y=1.06 loss_y2x=6.2313e-02 ppl_y2x=1.06 dual_loss=3.8995e-01
Validation X2Y - loss=9.2553e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3459e-01 ppl=2.30 best_loss=5.8312e-01 best_ppl=1.79
Epoch 188 - |param|=9.80e+02 |g_param|=2.72e+05 loss_x2y=6.1728e-02 ppl_x2y=1.06 loss_y2x=5.9489e-02 ppl_y2x=1.06 dual_loss=4.5168e-01
Validation X2Y - loss=9.2485e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9769e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 189 - |param|=9.81e+02 |g_param|=2.58e+05 loss_x2y=5.8751e-02 ppl_x2y=1.06 loss_y2x=5.9898e-02 ppl_y2x=1.06 dual_loss=3.9067e-01
Validation X2Y - loss=9.4343e-01 ppl=2.57 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9711e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 190 - |param|=9.81e+02 |g_param|=2.67e+05 loss_x2y=5.9019e-02 ppl_x2y=1.06 loss_y2x=5.8064e-02 ppl_y2x=1.06 dual_loss=3.8860e-01
Validation X2Y - loss=9.1379e-01 ppl=2.49 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8868e-01 ppl=2.20 best_loss=5.8312e-01 best_ppl=1.79
Epoch 191 - |param|=9.82e+02 |g_param|=2.55e+05 loss_x2y=5.8566e-02 ppl_x2y=1.06 loss_y2x=5.7587e-02 ppl_y2x=1.06 dual_loss=3.8664e-01
Validation X2Y - loss=9.2824e-01 ppl=2.53 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0463e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 192 - |param|=9.82e+02 |g_param|=2.70e+05 loss_x2y=6.1035e-02 ppl_x2y=1.06 loss_y2x=6.1063e-02 ppl_y2x=1.06 dual_loss=3.9080e-01
Validation X2Y - loss=9.0921e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1042e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 193 - |param|=9.82e+02 |g_param|=2.50e+05 loss_x2y=5.9130e-02 ppl_x2y=1.06 loss_y2x=6.0490e-02 ppl_y2x=1.06 dual_loss=4.9371e-01
Validation X2Y - loss=9.3151e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0747e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 194 - |param|=9.83e+02 |g_param|=2.92e+05 loss_x2y=5.9410e-02 ppl_x2y=1.06 loss_y2x=5.7656e-02 ppl_y2x=1.06 dual_loss=4.8847e-01
Validation X2Y - loss=9.3426e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1330e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 195 - |param|=9.83e+02 |g_param|=2.56e+05 loss_x2y=5.7964e-02 ppl_x2y=1.06 loss_y2x=5.6324e-02 ppl_y2x=1.06 dual_loss=3.7806e-01
Validation X2Y - loss=9.3401e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0895e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 196 - |param|=9.83e+02 |g_param|=2.55e+05 loss_x2y=5.9010e-02 ppl_x2y=1.06 loss_y2x=5.9765e-02 ppl_y2x=1.06 dual_loss=3.9041e-01
Validation X2Y - loss=9.0242e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2509e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 197 - |param|=9.84e+02 |g_param|=2.73e+05 loss_x2y=6.1504e-02 ppl_x2y=1.06 loss_y2x=5.9766e-02 ppl_y2x=1.06 dual_loss=5.1620e-01
Validation X2Y - loss=9.0829e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1923e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 198 - |param|=9.84e+02 |g_param|=2.54e+05 loss_x2y=5.8011e-02 ppl_x2y=1.06 loss_y2x=5.6990e-02 ppl_y2x=1.06 dual_loss=4.0341e-01
Validation X2Y - loss=9.1464e-01 ppl=2.50 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2907e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 199 - |param|=9.84e+02 |g_param|=2.58e+05 loss_x2y=5.8461e-02 ppl_x2y=1.06 loss_y2x=5.8724e-02 ppl_y2x=1.06 dual_loss=4.2343e-01
Validation X2Y - loss=9.0638e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2304e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 200 - |param|=9.85e+02 |g_param|=2.59e+05 loss_x2y=5.8300e-02 ppl_x2y=1.06 loss_y2x=5.9838e-02 ppl_y2x=1.06 dual_loss=4.0038e-01
Validation X2Y - loss=9.3147e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1245e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 201 - |param|=9.85e+02 |g_param|=1.92e+05 loss_x2y=6.1692e-02 ppl_x2y=1.06 loss_y2x=5.8723e-02 ppl_y2x=1.06 dual_loss=4.6328e-01
Validation X2Y - loss=9.1448e-01 ppl=2.50 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0348e-01 ppl=2.23 best_loss=5.8312e-01 best_ppl=1.79
Epoch 202 - |param|=9.85e+02 |g_param|=1.69e+05 loss_x2y=5.6516e-02 ppl_x2y=1.06 loss_y2x=5.6849e-02 ppl_y2x=1.06 dual_loss=4.4707e-01
Validation X2Y - loss=9.0493e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4616e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 203 - |param|=9.86e+02 |g_param|=1.73e+05 loss_x2y=5.6272e-02 ppl_x2y=1.06 loss_y2x=5.6725e-02 ppl_y2x=1.06 dual_loss=3.8756e-01
Validation X2Y - loss=9.1656e-01 ppl=2.50 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2052e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 204 - |param|=9.86e+02 |g_param|=2.19e+05 loss_x2y=5.6826e-02 ppl_x2y=1.06 loss_y2x=5.5397e-02 ppl_y2x=1.06 dual_loss=4.3149e-01
Validation X2Y - loss=9.3096e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0116e-01 ppl=2.23 best_loss=5.8312e-01 best_ppl=1.79
Epoch 205 - |param|=9.86e+02 |g_param|=2.80e+05 loss_x2y=5.8522e-02 ppl_x2y=1.06 loss_y2x=5.5692e-02 ppl_y2x=1.06 dual_loss=3.9559e-01
Validation X2Y - loss=9.3494e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1442e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 206 - |param|=9.87e+02 |g_param|=2.77e+05 loss_x2y=5.6245e-02 ppl_x2y=1.06 loss_y2x=5.6160e-02 ppl_y2x=1.06 dual_loss=3.8925e-01
Validation X2Y - loss=9.4490e-01 ppl=2.57 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1766e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 207 - |param|=9.87e+02 |g_param|=2.64e+05 loss_x2y=5.6471e-02 ppl_x2y=1.06 loss_y2x=5.5140e-02 ppl_y2x=1.06 dual_loss=3.7826e-01
Validation X2Y - loss=9.3000e-01 ppl=2.53 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0878e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 208 - |param|=9.87e+02 |g_param|=2.62e+05 loss_x2y=5.6857e-02 ppl_x2y=1.06 loss_y2x=5.4713e-02 ppl_y2x=1.06 dual_loss=3.8298e-01
Validation X2Y - loss=9.2169e-01 ppl=2.51 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9688e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 209 - |param|=9.88e+02 |g_param|=2.69e+05 loss_x2y=5.7744e-02 ppl_x2y=1.06 loss_y2x=5.7481e-02 ppl_y2x=1.06 dual_loss=3.9850e-01
Validation X2Y - loss=9.0222e-01 ppl=2.47 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1523e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 210 - |param|=9.88e+02 |g_param|=2.75e+05 loss_x2y=5.6663e-02 ppl_x2y=1.06 loss_y2x=5.5410e-02 ppl_y2x=1.06 dual_loss=4.0117e-01
Validation X2Y - loss=9.2963e-01 ppl=2.53 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3759e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 211 - |param|=9.89e+02 |g_param|=2.67e+05 loss_x2y=5.3438e-02 ppl_x2y=1.05 loss_y2x=5.5319e-02 ppl_y2x=1.06 dual_loss=4.2614e-01
Validation X2Y - loss=9.1832e-01 ppl=2.51 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0906e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 212 - |param|=9.89e+02 |g_param|=3.12e+05 loss_x2y=5.8420e-02 ppl_x2y=1.06 loss_y2x=5.6934e-02 ppl_y2x=1.06 dual_loss=4.9585e-01
Validation X2Y - loss=9.2250e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2418e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 213 - |param|=9.89e+02 |g_param|=2.82e+05 loss_x2y=5.8408e-02 ppl_x2y=1.06 loss_y2x=5.6364e-02 ppl_y2x=1.06 dual_loss=4.2228e-01
Validation X2Y - loss=9.3043e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3407e-01 ppl=2.30 best_loss=5.8312e-01 best_ppl=1.79
Epoch 214 - |param|=9.90e+02 |g_param|=2.70e+05 loss_x2y=5.4144e-02 ppl_x2y=1.06 loss_y2x=5.2489e-02 ppl_y2x=1.05 dual_loss=3.6932e-01
Validation X2Y - loss=9.2359e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0868e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 215 - |param|=9.90e+02 |g_param|=2.60e+05 loss_x2y=5.4247e-02 ppl_x2y=1.06 loss_y2x=5.3681e-02 ppl_y2x=1.06 dual_loss=3.8903e-01
Validation X2Y - loss=9.0738e-01 ppl=2.48 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1238e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 216 - |param|=9.90e+02 |g_param|=2.75e+05 loss_x2y=5.6456e-02 ppl_x2y=1.06 loss_y2x=5.6499e-02 ppl_y2x=1.06 dual_loss=3.9816e-01
Validation X2Y - loss=9.6468e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0172e-01 ppl=2.23 best_loss=5.8312e-01 best_ppl=1.79
Epoch 217 - |param|=9.91e+02 |g_param|=1.74e+05 loss_x2y=5.7041e-02 ppl_x2y=1.06 loss_y2x=5.4534e-02 ppl_y2x=1.06 dual_loss=3.8937e-01
Validation X2Y - loss=9.8424e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2322e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 218 - |param|=9.91e+02 |g_param|=1.64e+05 loss_x2y=5.4904e-02 ppl_x2y=1.06 loss_y2x=5.6011e-02 ppl_y2x=1.06 dual_loss=4.2150e-01
Validation X2Y - loss=9.4076e-01 ppl=2.56 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7629e-01 ppl=2.17 best_loss=5.8312e-01 best_ppl=1.79
Epoch 219 - |param|=9.91e+02 |g_param|=1.54e+05 loss_x2y=5.3310e-02 ppl_x2y=1.05 loss_y2x=5.3988e-02 ppl_y2x=1.06 dual_loss=3.8344e-01
Validation X2Y - loss=9.2516e-01 ppl=2.52 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8945e-01 ppl=2.20 best_loss=5.8312e-01 best_ppl=1.79
Epoch 220 - |param|=9.92e+02 |g_param|=1.71e+05 loss_x2y=5.5318e-02 ppl_x2y=1.06 loss_y2x=5.3972e-02 ppl_y2x=1.06 dual_loss=4.6084e-01
Validation X2Y - loss=9.3784e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9617e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 221 - |param|=9.92e+02 |g_param|=1.80e+05 loss_x2y=5.4505e-02 ppl_x2y=1.06 loss_y2x=5.5409e-02 ppl_y2x=1.06 dual_loss=3.9208e-01
Validation X2Y - loss=9.2735e-01 ppl=2.53 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8793e-01 ppl=2.20 best_loss=5.8312e-01 best_ppl=1.79
Epoch 222 - |param|=9.92e+02 |g_param|=2.35e+05 loss_x2y=5.1931e-02 ppl_x2y=1.05 loss_y2x=5.4359e-02 ppl_y2x=1.06 dual_loss=3.7863e-01
Validation X2Y - loss=9.5509e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.8370e-01 ppl=2.19 best_loss=5.8312e-01 best_ppl=1.79
Epoch 223 - |param|=9.93e+02 |g_param|=2.38e+05 loss_x2y=5.2174e-02 ppl_x2y=1.05 loss_y2x=5.2912e-02 ppl_y2x=1.05 dual_loss=3.8461e-01
Validation X2Y - loss=9.6457e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.7063e-01 ppl=2.16 best_loss=5.8312e-01 best_ppl=1.79
Epoch 224 - |param|=9.93e+02 |g_param|=2.35e+05 loss_x2y=5.3961e-02 ppl_x2y=1.06 loss_y2x=5.2804e-02 ppl_y2x=1.05 dual_loss=3.9075e-01
Validation X2Y - loss=9.5528e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9026e-01 ppl=2.20 best_loss=5.8312e-01 best_ppl=1.79
Epoch 225 - |param|=9.93e+02 |g_param|=2.47e+05 loss_x2y=5.4761e-02 ppl_x2y=1.06 loss_y2x=5.5095e-02 ppl_y2x=1.06 dual_loss=4.3537e-01
Validation X2Y - loss=9.8219e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0169e-01 ppl=2.23 best_loss=5.8312e-01 best_ppl=1.79
Epoch 226 - |param|=9.94e+02 |g_param|=2.41e+05 loss_x2y=5.4911e-02 ppl_x2y=1.06 loss_y2x=5.4121e-02 ppl_y2x=1.06 dual_loss=4.2789e-01
Validation X2Y - loss=9.6185e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3702e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 227 - |param|=9.94e+02 |g_param|=2.45e+05 loss_x2y=5.6068e-02 ppl_x2y=1.06 loss_y2x=5.4654e-02 ppl_y2x=1.06 dual_loss=4.1214e-01
Validation X2Y - loss=9.5032e-01 ppl=2.59 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1053e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 228 - |param|=9.94e+02 |g_param|=2.42e+05 loss_x2y=5.2792e-02 ppl_x2y=1.05 loss_y2x=5.2498e-02 ppl_y2x=1.05 dual_loss=4.7260e-01
Validation X2Y - loss=9.7513e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4286e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 229 - |param|=9.95e+02 |g_param|=2.42e+05 loss_x2y=5.4476e-02 ppl_x2y=1.06 loss_y2x=5.2911e-02 ppl_y2x=1.05 dual_loss=4.3428e-01
Validation X2Y - loss=9.6911e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3119e-01 ppl=2.30 best_loss=5.8312e-01 best_ppl=1.79
Epoch 230 - |param|=9.95e+02 |g_param|=2.35e+05 loss_x2y=5.3971e-02 ppl_x2y=1.06 loss_y2x=5.1478e-02 ppl_y2x=1.05 dual_loss=3.9004e-01
Validation X2Y - loss=9.6853e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3610e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 231 - |param|=9.95e+02 |g_param|=2.35e+05 loss_x2y=5.1803e-02 ppl_x2y=1.05 loss_y2x=5.3000e-02 ppl_y2x=1.05 dual_loss=3.7629e-01
Validation X2Y - loss=9.4680e-01 ppl=2.58 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2358e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 232 - |param|=9.96e+02 |g_param|=2.51e+05 loss_x2y=5.2147e-02 ppl_x2y=1.05 loss_y2x=5.2558e-02 ppl_y2x=1.05 dual_loss=4.1375e-01
Validation X2Y - loss=9.3293e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1098e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 233 - |param|=9.96e+02 |g_param|=2.40e+05 loss_x2y=5.3071e-02 ppl_x2y=1.05 loss_y2x=5.3400e-02 ppl_y2x=1.05 dual_loss=3.9602e-01
Validation X2Y - loss=9.3298e-01 ppl=2.54 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9250e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 234 - |param|=9.96e+02 |g_param|=2.30e+05 loss_x2y=5.1831e-02 ppl_x2y=1.05 loss_y2x=5.2568e-02 ppl_y2x=1.05 dual_loss=3.7799e-01
Validation X2Y - loss=9.3706e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4073e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 235 - |param|=9.97e+02 |g_param|=2.33e+05 loss_x2y=5.2298e-02 ppl_x2y=1.05 loss_y2x=5.1737e-02 ppl_y2x=1.05 dual_loss=4.2290e-01
Validation X2Y - loss=9.2660e-01 ppl=2.53 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1233e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 236 - |param|=9.97e+02 |g_param|=2.42e+05 loss_x2y=5.3363e-02 ppl_x2y=1.05 loss_y2x=5.1992e-02 ppl_y2x=1.05 dual_loss=4.5156e-01
Validation X2Y - loss=9.6060e-01 ppl=2.61 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0790e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 237 - |param|=9.97e+02 |g_param|=2.55e+05 loss_x2y=5.3615e-02 ppl_x2y=1.06 loss_y2x=5.4032e-02 ppl_y2x=1.06 dual_loss=4.1431e-01
Validation X2Y - loss=9.5040e-01 ppl=2.59 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2021e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 238 - |param|=9.98e+02 |g_param|=3.05e+05 loss_x2y=5.2032e-02 ppl_x2y=1.05 loss_y2x=5.1499e-02 ppl_y2x=1.05 dual_loss=3.7615e-01
Validation X2Y - loss=9.5421e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9836e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 239 - |param|=9.98e+02 |g_param|=2.55e+05 loss_x2y=4.9949e-02 ppl_x2y=1.05 loss_y2x=4.9906e-02 ppl_y2x=1.05 dual_loss=3.7290e-01
Validation X2Y - loss=9.5858e-01 ppl=2.61 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9500e-01 ppl=2.21 best_loss=5.8312e-01 best_ppl=1.79
Epoch 240 - |param|=9.98e+02 |g_param|=1.95e+05 loss_x2y=5.2002e-02 ppl_x2y=1.05 loss_y2x=5.0350e-02 ppl_y2x=1.05 dual_loss=4.3971e-01
Validation X2Y - loss=9.5402e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2828e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 241 - |param|=9.99e+02 |g_param|=1.59e+05 loss_x2y=5.0559e-02 ppl_x2y=1.05 loss_y2x=5.2696e-02 ppl_y2x=1.05 dual_loss=4.0140e-01
Validation X2Y - loss=9.3468e-01 ppl=2.55 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0768e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 242 - |param|=9.99e+02 |g_param|=1.55e+05 loss_x2y=5.1364e-02 ppl_x2y=1.05 loss_y2x=5.2707e-02 ppl_y2x=1.05 dual_loss=4.3677e-01
Validation X2Y - loss=9.5471e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3856e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 243 - |param|=1.00e+03 |g_param|=1.53e+05 loss_x2y=5.0778e-02 ppl_x2y=1.05 loss_y2x=5.0661e-02 ppl_y2x=1.05 dual_loss=4.1942e-01
Validation X2Y - loss=9.6193e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2534e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 244 - |param|=1.00e+03 |g_param|=1.63e+05 loss_x2y=5.0758e-02 ppl_x2y=1.05 loss_y2x=5.3305e-02 ppl_y2x=1.05 dual_loss=4.8808e-01
Validation X2Y - loss=9.6556e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2185e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 245 - |param|=1.00e+03 |g_param|=1.47e+05 loss_x2y=4.8218e-02 ppl_x2y=1.05 loss_y2x=5.0221e-02 ppl_y2x=1.05 dual_loss=3.8545e-01
Validation X2Y - loss=9.4005e-01 ppl=2.56 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4131e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 246 - |param|=1.00e+03 |g_param|=1.50e+05 loss_x2y=5.1888e-02 ppl_x2y=1.05 loss_y2x=5.0339e-02 ppl_y2x=1.05 dual_loss=3.8559e-01
Validation X2Y - loss=9.5580e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3754e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 247 - |param|=1.00e+03 |g_param|=1.55e+05 loss_x2y=5.2251e-02 ppl_x2y=1.05 loss_y2x=5.0459e-02 ppl_y2x=1.05 dual_loss=4.4452e-01
Validation X2Y - loss=9.5992e-01 ppl=2.61 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4622e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 248 - |param|=1.00e+03 |g_param|=1.59e+05 loss_x2y=5.2657e-02 ppl_x2y=1.05 loss_y2x=5.1021e-02 ppl_y2x=1.05 dual_loss=4.7690e-01
Validation X2Y - loss=9.5592e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2000e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 249 - |param|=1.00e+03 |g_param|=1.56e+05 loss_x2y=5.2470e-02 ppl_x2y=1.05 loss_y2x=5.1905e-02 ppl_y2x=1.05 dual_loss=4.6524e-01
Validation X2Y - loss=9.5038e-01 ppl=2.59 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3691e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 250 - |param|=1.00e+03 |g_param|=1.55e+05 loss_x2y=5.2944e-02 ppl_x2y=1.05 loss_y2x=5.1153e-02 ppl_y2x=1.05 dual_loss=4.6834e-01
Validation X2Y - loss=9.7443e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4096e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 251 - |param|=1.00e+03 |g_param|=1.49e+05 loss_x2y=4.8841e-02 ppl_x2y=1.05 loss_y2x=4.8814e-02 ppl_y2x=1.05 dual_loss=3.6904e-01
Validation X2Y - loss=9.6120e-01 ppl=2.61 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2442e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 252 - |param|=1.00e+03 |g_param|=1.45e+05 loss_x2y=5.0502e-02 ppl_x2y=1.05 loss_y2x=4.7058e-02 ppl_y2x=1.05 dual_loss=3.8257e-01
Validation X2Y - loss=9.6598e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1523e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 253 - |param|=1.00e+03 |g_param|=1.48e+05 loss_x2y=5.2933e-02 ppl_x2y=1.05 loss_y2x=5.0924e-02 ppl_y2x=1.05 dual_loss=4.0915e-01
Validation X2Y - loss=9.7624e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2005e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 254 - |param|=1.00e+03 |g_param|=1.45e+05 loss_x2y=4.8234e-02 ppl_x2y=1.05 loss_y2x=4.7304e-02 ppl_y2x=1.05 dual_loss=3.6579e-01
Validation X2Y - loss=1.0116e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2225e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 255 - |param|=1.00e+03 |g_param|=1.60e+05 loss_x2y=5.2482e-02 ppl_x2y=1.05 loss_y2x=5.2805e-02 ppl_y2x=1.05 dual_loss=5.0719e-01
Validation X2Y - loss=1.0001e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1942e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 256 - |param|=1.00e+03 |g_param|=1.45e+05 loss_x2y=4.9708e-02 ppl_x2y=1.05 loss_y2x=4.9240e-02 ppl_y2x=1.05 dual_loss=4.0944e-01
Validation X2Y - loss=9.7822e-01 ppl=2.66 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3565e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 257 - |param|=1.00e+03 |g_param|=1.49e+05 loss_x2y=5.1020e-02 ppl_x2y=1.05 loss_y2x=5.0590e-02 ppl_y2x=1.05 dual_loss=4.1543e-01
Validation X2Y - loss=9.7556e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3083e-01 ppl=2.30 best_loss=5.8312e-01 best_ppl=1.79
Epoch 258 - |param|=1.00e+03 |g_param|=1.48e+05 loss_x2y=4.6522e-02 ppl_x2y=1.05 loss_y2x=4.7272e-02 ppl_y2x=1.05 dual_loss=4.4197e-01
Validation X2Y - loss=9.5518e-01 ppl=2.60 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4148e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 259 - |param|=1.01e+03 |g_param|=1.65e+05 loss_x2y=5.0309e-02 ppl_x2y=1.05 loss_y2x=5.0101e-02 ppl_y2x=1.05 dual_loss=4.8452e-01
Validation X2Y - loss=9.6787e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0435e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 260 - |param|=1.01e+03 |g_param|=2.32e+05 loss_x2y=4.9043e-02 ppl_x2y=1.05 loss_y2x=4.6595e-02 ppl_y2x=1.05 dual_loss=3.9253e-01
Validation X2Y - loss=9.4608e-01 ppl=2.58 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1974e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 261 - |param|=1.01e+03 |g_param|=2.81e+05 loss_x2y=4.8691e-02 ppl_x2y=1.05 loss_y2x=4.7241e-02 ppl_y2x=1.05 dual_loss=3.9899e-01
Validation X2Y - loss=9.6789e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4806e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 262 - |param|=1.01e+03 |g_param|=2.84e+05 loss_x2y=4.8357e-02 ppl_x2y=1.05 loss_y2x=4.7699e-02 ppl_y2x=1.05 dual_loss=3.8279e-01
Validation X2Y - loss=9.4647e-01 ppl=2.58 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2702e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 263 - |param|=1.01e+03 |g_param|=2.28e+05 loss_x2y=4.8510e-02 ppl_x2y=1.05 loss_y2x=4.7826e-02 ppl_y2x=1.05 dual_loss=3.8486e-01
Validation X2Y - loss=9.7362e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2292e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 264 - |param|=1.01e+03 |g_param|=2.11e+05 loss_x2y=4.6944e-02 ppl_x2y=1.05 loss_y2x=5.0819e-02 ppl_y2x=1.05 dual_loss=3.7641e-01
Validation X2Y - loss=9.7456e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1054e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Iteration:   2%|█▋                                                                               | 1/47 [00:00<?, ?it/s]Epoch 265 - |param|=1.01e+03 |g_param|=2.10e+05 loss_x2y=4.7358e-02 ppl_x2y=1.05 loss_y2x=4.8095e-02 ppl_y2x=1.05 dual_loss=3.8905e-01
Validation X2Y - loss=9.8516e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.9667e-01 ppl=2.22 best_loss=5.8312e-01 best_ppl=1.79
Epoch 266 - |param|=1.01e+03 |g_param|=2.16e+05 loss_x2y=4.7760e-02 ppl_x2y=1.05 loss_y2x=4.6397e-02 ppl_y2x=1.05 dual_loss=3.9553e-01
Validation X2Y - loss=9.8652e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1203e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 267 - |param|=1.01e+03 |g_param|=2.09e+05 loss_x2y=4.7329e-02 ppl_x2y=1.05 loss_y2x=4.6894e-02 ppl_y2x=1.05 dual_loss=3.6300e-01
Validation X2Y - loss=9.7092e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1767e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 268 - |param|=1.01e+03 |g_param|=2.21e+05 loss_x2y=5.1559e-02 ppl_x2y=1.05 loss_y2x=4.8490e-02 ppl_y2x=1.05 dual_loss=4.8012e-01
Validation X2Y - loss=9.7049e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3217e-01 ppl=2.30 best_loss=5.8312e-01 best_ppl=1.79
Epoch 269 - |param|=1.01e+03 |g_param|=2.08e+05 loss_x2y=4.5481e-02 ppl_x2y=1.05 loss_y2x=4.5423e-02 ppl_y2x=1.05 dual_loss=3.6726e-01
Validation X2Y - loss=1.0052e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1060e-01 ppl=2.25 best_loss=5.8312e-01 best_ppl=1.79
Epoch 270 - |param|=1.01e+03 |g_param|=2.18e+05 loss_x2y=4.8272e-02 ppl_x2y=1.05 loss_y2x=4.5705e-02 ppl_y2x=1.05 dual_loss=3.8462e-01
Validation X2Y - loss=9.7209e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1928e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 271 - |param|=1.01e+03 |g_param|=2.20e+05 loss_x2y=4.7400e-02 ppl_x2y=1.05 loss_y2x=4.7767e-02 ppl_y2x=1.05 dual_loss=4.3389e-01
Validation X2Y - loss=1.0047e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1897e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 272 - |param|=1.01e+03 |g_param|=2.09e+05 loss_x2y=4.8458e-02 ppl_x2y=1.05 loss_y2x=4.7408e-02 ppl_y2x=1.05 dual_loss=4.1186e-01
Validation X2Y - loss=9.8762e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2331e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 273 - |param|=1.01e+03 |g_param|=2.04e+05 loss_x2y=4.8717e-02 ppl_x2y=1.05 loss_y2x=4.7920e-02 ppl_y2x=1.05 dual_loss=4.2342e-01
Validation X2Y - loss=1.0015e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4019e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 274 - |param|=1.01e+03 |g_param|=2.07e+05 loss_x2y=4.7810e-02 ppl_x2y=1.05 loss_y2x=4.6739e-02 ppl_y2x=1.05 dual_loss=4.0507e-01
Validation X2Y - loss=9.9399e-01 ppl=2.70 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2781e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 275 - |param|=1.01e+03 |g_param|=2.18e+05 loss_x2y=4.8713e-02 ppl_x2y=1.05 loss_y2x=4.7863e-02 ppl_y2x=1.05 dual_loss=4.1727e-01
Validation X2Y - loss=9.6890e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.0837e-01 ppl=2.24 best_loss=5.8312e-01 best_ppl=1.79
Epoch 276 - |param|=1.01e+03 |g_param|=2.25e+05 loss_x2y=4.7339e-02 ppl_x2y=1.05 loss_y2x=4.5303e-02 ppl_y2x=1.05 dual_loss=3.9584e-01
Validation X2Y - loss=9.8081e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5395e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 277 - |param|=1.01e+03 |g_param|=2.04e+05 loss_x2y=4.6209e-02 ppl_x2y=1.05 loss_y2x=4.5259e-02 ppl_y2x=1.05 dual_loss=3.5183e-01
Validation X2Y - loss=9.5086e-01 ppl=2.59 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3603e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 278 - |param|=1.01e+03 |g_param|=2.18e+05 loss_x2y=4.8003e-02 ppl_x2y=1.05 loss_y2x=4.7594e-02 ppl_y2x=1.05 dual_loss=4.4096e-01
Validation X2Y - loss=9.5899e-01 ppl=2.61 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3790e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 279 - |param|=1.01e+03 |g_param|=2.18e+05 loss_x2y=4.8211e-02 ppl_x2y=1.05 loss_y2x=4.4720e-02 ppl_y2x=1.05 dual_loss=4.1754e-01
Validation X2Y - loss=9.4733e-01 ppl=2.58 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3657e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 280 - |param|=1.01e+03 |g_param|=3.69e+05 loss_x2y=4.8140e-02 ppl_x2y=1.05 loss_y2x=4.8791e-02 ppl_y2x=1.05 dual_loss=4.2049e-01
Validation X2Y - loss=9.6588e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7397e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 281 - |param|=1.01e+03 |g_param|=2.59e+05 loss_x2y=4.7523e-02 ppl_x2y=1.05 loss_y2x=4.5155e-02 ppl_y2x=1.05 dual_loss=4.3865e-01
Validation X2Y - loss=9.7136e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3605e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 282 - |param|=1.01e+03 |g_param|=2.34e+05 loss_x2y=5.0730e-02 ppl_x2y=1.05 loss_y2x=4.9168e-02 ppl_y2x=1.05 dual_loss=5.4212e-01
Validation X2Y - loss=9.7516e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2358e-01 ppl=2.28 best_loss=5.8312e-01 best_ppl=1.79
Epoch 283 - |param|=1.01e+03 |g_param|=2.15e+05 loss_x2y=4.8646e-02 ppl_x2y=1.05 loss_y2x=4.7758e-02 ppl_y2x=1.05 dual_loss=4.1118e-01
Validation X2Y - loss=9.6134e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.1645e-01 ppl=2.26 best_loss=5.8312e-01 best_ppl=1.79
Epoch 284 - |param|=1.01e+03 |g_param|=2.79e+05 loss_x2y=4.3076e-02 ppl_x2y=1.04 loss_y2x=4.5044e-02 ppl_y2x=1.05 dual_loss=3.6582e-01
Validation X2Y - loss=9.6564e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5992e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 285 - |param|=1.01e+03 |g_param|=2.77e+05 loss_x2y=4.6316e-02 ppl_x2y=1.05 loss_y2x=4.5089e-02 ppl_y2x=1.05 dual_loss=4.1794e-01
Validation X2Y - loss=9.8037e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9361e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 286 - |param|=1.01e+03 |g_param|=2.98e+05 loss_x2y=4.6102e-02 ppl_x2y=1.05 loss_y2x=4.6662e-02 ppl_y2x=1.05 dual_loss=4.2593e-01
Validation X2Y - loss=1.0189e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4637e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 287 - |param|=1.01e+03 |g_param|=2.69e+05 loss_x2y=4.4492e-02 ppl_x2y=1.05 loss_y2x=4.3462e-02 ppl_y2x=1.04 dual_loss=3.5938e-01
Validation X2Y - loss=1.0008e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2777e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 288 - |param|=1.01e+03 |g_param|=3.03e+05 loss_x2y=4.8963e-02 ppl_x2y=1.05 loss_y2x=4.8090e-02 ppl_y2x=1.05 dual_loss=4.8843e-01
Validation X2Y - loss=1.0183e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2695e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 289 - |param|=1.02e+03 |g_param|=2.78e+05 loss_x2y=4.7076e-02 ppl_x2y=1.05 loss_y2x=4.5851e-02 ppl_y2x=1.05 dual_loss=4.0387e-01
Validation X2Y - loss=1.0166e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2668e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 290 - |param|=1.02e+03 |g_param|=2.88e+05 loss_x2y=4.7887e-02 ppl_x2y=1.05 loss_y2x=4.3809e-02 ppl_y2x=1.04 dual_loss=4.2536e-01
Validation X2Y - loss=9.7108e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4408e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 291 - |param|=1.02e+03 |g_param|=2.82e+05 loss_x2y=4.7028e-02 ppl_x2y=1.05 loss_y2x=4.5732e-02 ppl_y2x=1.05 dual_loss=4.0523e-01
Validation X2Y - loss=9.8574e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2835e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 292 - |param|=1.02e+03 |g_param|=2.93e+05 loss_x2y=4.7142e-02 ppl_x2y=1.05 loss_y2x=4.3808e-02 ppl_y2x=1.04 dual_loss=4.4138e-01
Validation X2Y - loss=1.0149e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4592e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 293 - |param|=1.02e+03 |g_param|=2.55e+05 loss_x2y=4.2521e-02 ppl_x2y=1.04 loss_y2x=4.4107e-02 ppl_y2x=1.05 dual_loss=3.6208e-01
Validation X2Y - loss=9.9694e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4725e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 294 - |param|=1.02e+03 |g_param|=2.78e+05 loss_x2y=4.4504e-02 ppl_x2y=1.05 loss_y2x=4.3564e-02 ppl_y2x=1.04 dual_loss=4.2358e-01
Validation X2Y - loss=9.8522e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4664e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 295 - |param|=1.02e+03 |g_param|=2.78e+05 loss_x2y=4.6305e-02 ppl_x2y=1.05 loss_y2x=4.8559e-02 ppl_y2x=1.05 dual_loss=4.1892e-01
Validation X2Y - loss=9.8971e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4282e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 296 - |param|=1.02e+03 |g_param|=2.85e+05 loss_x2y=4.6123e-02 ppl_x2y=1.05 loss_y2x=4.5285e-02 ppl_y2x=1.05 dual_loss=4.2603e-01
Validation X2Y - loss=9.7065e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5037e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 297 - |param|=1.02e+03 |g_param|=2.70e+05 loss_x2y=4.6652e-02 ppl_x2y=1.05 loss_y2x=4.4837e-02 ppl_y2x=1.05 dual_loss=4.2784e-01
Validation X2Y - loss=9.9613e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4428e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 298 - |param|=1.02e+03 |g_param|=2.09e+05 loss_x2y=4.6308e-02 ppl_x2y=1.05 loss_y2x=4.4284e-02 ppl_y2x=1.05 dual_loss=3.8718e-01
Validation X2Y - loss=9.7165e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3050e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 299 - |param|=1.02e+03 |g_param|=1.91e+05 loss_x2y=4.4138e-02 ppl_x2y=1.05 loss_y2x=4.4759e-02 ppl_y2x=1.05 dual_loss=3.7965e-01
Validation X2Y - loss=9.6841e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5217e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 300 - |param|=1.02e+03 |g_param|=2.08e+05 loss_x2y=4.6320e-02 ppl_x2y=1.05 loss_y2x=4.6299e-02 ppl_y2x=1.05 dual_loss=4.1996e-01
Validation X2Y - loss=9.8412e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3832e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 301 - |param|=1.02e+03 |g_param|=2.03e+05 loss_x2y=4.6921e-02 ppl_x2y=1.05 loss_y2x=4.5021e-02 ppl_y2x=1.05 dual_loss=4.2350e-01
Validation X2Y - loss=9.8331e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5377e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 302 - |param|=1.02e+03 |g_param|=2.37e+05 loss_x2y=4.7174e-02 ppl_x2y=1.05 loss_y2x=4.8510e-02 ppl_y2x=1.05 dual_loss=4.2340e-01
Validation X2Y - loss=9.6881e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5076e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 303 - |param|=1.02e+03 |g_param|=2.01e+05 loss_x2y=4.6670e-02 ppl_x2y=1.05 loss_y2x=4.5970e-02 ppl_y2x=1.05 dual_loss=4.3494e-01
Validation X2Y - loss=9.8740e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7185e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 304 - |param|=1.02e+03 |g_param|=2.06e+05 loss_x2y=4.5213e-02 ppl_x2y=1.05 loss_y2x=4.3977e-02 ppl_y2x=1.04 dual_loss=3.5887e-01
Validation X2Y - loss=9.8724e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6339e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 305 - |param|=1.02e+03 |g_param|=2.01e+05 loss_x2y=4.6986e-02 ppl_x2y=1.05 loss_y2x=4.6391e-02 ppl_y2x=1.05 dual_loss=4.4682e-01
Validation X2Y - loss=9.8050e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4843e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 306 - |param|=1.02e+03 |g_param|=1.94e+05 loss_x2y=4.3417e-02 ppl_x2y=1.04 loss_y2x=4.3681e-02 ppl_y2x=1.04 dual_loss=3.7572e-01
Validation X2Y - loss=9.9052e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3608e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 307 - |param|=1.02e+03 |g_param|=2.02e+05 loss_x2y=4.5649e-02 ppl_x2y=1.05 loss_y2x=4.5523e-02 ppl_y2x=1.05 dual_loss=3.9045e-01
Validation X2Y - loss=9.7995e-01 ppl=2.66 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4785e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 308 - |param|=1.02e+03 |g_param|=1.84e+05 loss_x2y=4.1901e-02 ppl_x2y=1.04 loss_y2x=4.0873e-02 ppl_y2x=1.04 dual_loss=3.5020e-01
Validation X2Y - loss=9.9911e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7974e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 309 - |param|=1.02e+03 |g_param|=1.95e+05 loss_x2y=4.4106e-02 ppl_x2y=1.05 loss_y2x=4.3806e-02 ppl_y2x=1.04 dual_loss=4.1822e-01
Validation X2Y - loss=1.0018e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5212e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 310 - |param|=1.02e+03 |g_param|=1.86e+05 loss_x2y=4.3653e-02 ppl_x2y=1.04 loss_y2x=4.5252e-02 ppl_y2x=1.05 dual_loss=3.9432e-01
Validation X2Y - loss=9.9929e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4562e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 311 - |param|=1.02e+03 |g_param|=1.90e+05 loss_x2y=4.5353e-02 ppl_x2y=1.05 loss_y2x=4.5410e-02 ppl_y2x=1.05 dual_loss=4.8742e-01
Validation X2Y - loss=9.7974e-01 ppl=2.66 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5704e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 312 - |param|=1.02e+03 |g_param|=1.95e+05 loss_x2y=4.7446e-02 ppl_x2y=1.05 loss_y2x=4.7168e-02 ppl_y2x=1.05 dual_loss=5.1727e-01
Validation X2Y - loss=1.0023e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4787e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 313 - |param|=1.02e+03 |g_param|=1.96e+05 loss_x2y=4.6558e-02 ppl_x2y=1.05 loss_y2x=4.5756e-02 ppl_y2x=1.05 dual_loss=4.2998e-01
Validation X2Y - loss=9.8277e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4825e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 314 - |param|=1.02e+03 |g_param|=1.85e+05 loss_x2y=4.1581e-02 ppl_x2y=1.04 loss_y2x=4.2132e-02 ppl_y2x=1.04 dual_loss=3.6065e-01
Validation X2Y - loss=9.8812e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4335e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 315 - |param|=1.02e+03 |g_param|=1.86e+05 loss_x2y=4.5258e-02 ppl_x2y=1.05 loss_y2x=4.4738e-02 ppl_y2x=1.05 dual_loss=5.2277e-01
Validation X2Y - loss=1.0125e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4041e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 316 - |param|=1.02e+03 |g_param|=2.07e+05 loss_x2y=4.5273e-02 ppl_x2y=1.05 loss_y2x=4.4445e-02 ppl_y2x=1.05 dual_loss=4.2021e-01
Validation X2Y - loss=9.8596e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4461e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 317 - |param|=1.02e+03 |g_param|=1.90e+05 loss_x2y=4.4672e-02 ppl_x2y=1.05 loss_y2x=4.3312e-02 ppl_y2x=1.04 dual_loss=4.2515e-01
Validation X2Y - loss=9.7810e-01 ppl=2.66 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6786e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 318 - |param|=1.02e+03 |g_param|=2.13e+05 loss_x2y=4.2876e-02 ppl_x2y=1.04 loss_y2x=4.1431e-02 ppl_y2x=1.04 dual_loss=3.8091e-01
Validation X2Y - loss=9.8997e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7549e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 319 - |param|=1.03e+03 |g_param|=2.46e+05 loss_x2y=4.1075e-02 ppl_x2y=1.04 loss_y2x=4.3596e-02 ppl_y2x=1.04 dual_loss=3.8217e-01
Validation X2Y - loss=9.8856e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7488e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 320 - |param|=1.03e+03 |g_param|=2.16e+05 loss_x2y=4.4012e-02 ppl_x2y=1.04 loss_y2x=4.4322e-02 ppl_y2x=1.05 dual_loss=4.3700e-01
Validation X2Y - loss=1.0226e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6878e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 321 - |param|=1.03e+03 |g_param|=2.03e+05 loss_x2y=4.6308e-02 ppl_x2y=1.05 loss_y2x=4.5264e-02 ppl_y2x=1.05 dual_loss=4.5432e-01
Validation X2Y - loss=9.9399e-01 ppl=2.70 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5331e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 322 - |param|=1.03e+03 |g_param|=2.26e+05 loss_x2y=4.4839e-02 ppl_x2y=1.05 loss_y2x=4.4239e-02 ppl_y2x=1.05 dual_loss=4.3003e-01
Validation X2Y - loss=9.9764e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4255e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 323 - |param|=1.03e+03 |g_param|=3.76e+05 loss_x2y=4.6168e-02 ppl_x2y=1.05 loss_y2x=4.6968e-02 ppl_y2x=1.05 dual_loss=4.4284e-01
Validation X2Y - loss=1.0145e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.2185e-01 ppl=2.27 best_loss=5.8312e-01 best_ppl=1.79
Epoch 324 - |param|=1.03e+03 |g_param|=3.41e+05 loss_x2y=4.2600e-02 ppl_x2y=1.04 loss_y2x=4.1696e-02 ppl_y2x=1.04 dual_loss=4.3589e-01
Validation X2Y - loss=1.0171e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3778e-01 ppl=2.31 best_loss=5.8312e-01 best_ppl=1.79
Epoch 325 - |param|=1.03e+03 |g_param|=2.28e+05 loss_x2y=4.6315e-02 ppl_x2y=1.05 loss_y2x=4.6457e-02 ppl_y2x=1.05 dual_loss=5.0127e-01
Validation X2Y - loss=1.0077e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5356e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 326 - |param|=1.03e+03 |g_param|=1.98e+05 loss_x2y=4.3751e-02 ppl_x2y=1.04 loss_y2x=4.4561e-02 ppl_y2x=1.05 dual_loss=4.2309e-01
Validation X2Y - loss=1.0389e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7087e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 327 - |param|=1.03e+03 |g_param|=1.91e+05 loss_x2y=4.5229e-02 ppl_x2y=1.05 loss_y2x=4.4057e-02 ppl_y2x=1.05 dual_loss=3.9257e-01
Validation X2Y - loss=1.0188e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5959e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 328 - |param|=1.03e+03 |g_param|=1.99e+05 loss_x2y=4.2513e-02 ppl_x2y=1.04 loss_y2x=4.2119e-02 ppl_y2x=1.04 dual_loss=3.9959e-01
Validation X2Y - loss=1.0095e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6046e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 329 - |param|=1.03e+03 |g_param|=1.88e+05 loss_x2y=4.3973e-02 ppl_x2y=1.04 loss_y2x=4.2969e-02 ppl_y2x=1.04 dual_loss=3.8484e-01
Validation X2Y - loss=1.0073e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7152e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 330 - |param|=1.03e+03 |g_param|=2.04e+05 loss_x2y=4.3347e-02 ppl_x2y=1.04 loss_y2x=4.4099e-02 ppl_y2x=1.05 dual_loss=3.9761e-01
Validation X2Y - loss=1.0145e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4743e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 331 - |param|=1.03e+03 |g_param|=1.93e+05 loss_x2y=4.5207e-02 ppl_x2y=1.05 loss_y2x=4.3966e-02 ppl_y2x=1.04 dual_loss=4.8774e-01
Validation X2Y - loss=9.9999e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7482e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 332 - |param|=1.03e+03 |g_param|=2.03e+05 loss_x2y=4.5250e-02 ppl_x2y=1.05 loss_y2x=4.4327e-02 ppl_y2x=1.05 dual_loss=4.0311e-01
Validation X2Y - loss=9.9788e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6062e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 333 - |param|=1.03e+03 |g_param|=1.85e+05 loss_x2y=4.1360e-02 ppl_x2y=1.04 loss_y2x=4.2832e-02 ppl_y2x=1.04 dual_loss=3.7873e-01
Validation X2Y - loss=9.8652e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5333e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 334 - |param|=1.03e+03 |g_param|=1.82e+05 loss_x2y=4.0894e-02 ppl_x2y=1.04 loss_y2x=4.1960e-02 ppl_y2x=1.04 dual_loss=3.5749e-01
Validation X2Y - loss=9.7632e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4456e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 335 - |param|=1.03e+03 |g_param|=1.88e+05 loss_x2y=4.5421e-02 ppl_x2y=1.05 loss_y2x=4.3923e-02 ppl_y2x=1.04 dual_loss=4.2234e-01
Validation X2Y - loss=9.8470e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6912e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 336 - |param|=1.03e+03 |g_param|=2.07e+05 loss_x2y=4.5412e-02 ppl_x2y=1.05 loss_y2x=4.3360e-02 ppl_y2x=1.04 dual_loss=4.4908e-01
Validation X2Y - loss=9.9724e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6875e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 337 - |param|=1.03e+03 |g_param|=1.97e+05 loss_x2y=4.1345e-02 ppl_x2y=1.04 loss_y2x=4.2035e-02 ppl_y2x=1.04 dual_loss=4.0450e-01
Validation X2Y - loss=1.0006e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7280e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 338 - |param|=1.03e+03 |g_param|=1.87e+05 loss_x2y=4.0736e-02 ppl_x2y=1.04 loss_y2x=4.2340e-02 ppl_y2x=1.04 dual_loss=4.1224e-01
Validation X2Y - loss=1.0051e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7282e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 339 - |param|=1.03e+03 |g_param|=1.76e+05 loss_x2y=4.2193e-02 ppl_x2y=1.04 loss_y2x=4.0062e-02 ppl_y2x=1.04 dual_loss=3.8020e-01
Validation X2Y - loss=1.0012e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7279e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 340 - |param|=1.03e+03 |g_param|=1.95e+05 loss_x2y=4.2765e-02 ppl_x2y=1.04 loss_y2x=4.2048e-02 ppl_y2x=1.04 dual_loss=4.5224e-01
Validation X2Y - loss=1.0047e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7082e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 341 - |param|=1.03e+03 |g_param|=2.57e+05 loss_x2y=4.4005e-02 ppl_x2y=1.04 loss_y2x=4.3782e-02 ppl_y2x=1.04 dual_loss=4.1467e-01
Validation X2Y - loss=9.6529e-01 ppl=2.63 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6868e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 342 - |param|=1.03e+03 |g_param|=2.35e+05 loss_x2y=4.5251e-02 ppl_x2y=1.05 loss_y2x=4.4969e-02 ppl_y2x=1.05 dual_loss=5.2800e-01
Validation X2Y - loss=9.7622e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6319e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 343 - |param|=1.03e+03 |g_param|=1.90e+05 loss_x2y=4.2636e-02 ppl_x2y=1.04 loss_y2x=4.1422e-02 ppl_y2x=1.04 dual_loss=4.2875e-01
Validation X2Y - loss=9.6380e-01 ppl=2.62 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6368e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 344 - |param|=1.03e+03 |g_param|=1.87e+05 loss_x2y=4.3169e-02 ppl_x2y=1.04 loss_y2x=4.3390e-02 ppl_y2x=1.04 dual_loss=4.4630e-01
Validation X2Y - loss=9.9037e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5398e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 345 - |param|=1.03e+03 |g_param|=2.53e+05 loss_x2y=4.2925e-02 ppl_x2y=1.04 loss_y2x=4.2185e-02 ppl_y2x=1.04 dual_loss=4.1660e-01
Validation X2Y - loss=9.8642e-01 ppl=2.68 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5882e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 346 - |param|=1.03e+03 |g_param|=3.17e+05 loss_x2y=4.1080e-02 ppl_x2y=1.04 loss_y2x=4.1090e-02 ppl_y2x=1.04 dual_loss=3.9353e-01
Validation X2Y - loss=9.7136e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5585e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 347 - |param|=1.03e+03 |g_param|=3.14e+05 loss_x2y=4.1186e-02 ppl_x2y=1.04 loss_y2x=4.2054e-02 ppl_y2x=1.04 dual_loss=3.9721e-01
Validation X2Y - loss=9.8117e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5682e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 348 - |param|=1.03e+03 |g_param|=3.46e+05 loss_x2y=4.2926e-02 ppl_x2y=1.04 loss_y2x=4.2453e-02 ppl_y2x=1.04 dual_loss=4.5296e-01
Validation X2Y - loss=9.7269e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4631e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 349 - |param|=1.04e+03 |g_param|=3.29e+05 loss_x2y=4.2484e-02 ppl_x2y=1.04 loss_y2x=4.1887e-02 ppl_y2x=1.04 dual_loss=3.9815e-01
Validation X2Y - loss=9.7464e-01 ppl=2.65 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2103e-01 ppl=2.51 best_loss=5.8312e-01 best_ppl=1.79
Epoch 350 - |param|=1.04e+03 |g_param|=3.31e+05 loss_x2y=4.1828e-02 ppl_x2y=1.04 loss_y2x=4.0594e-02 ppl_y2x=1.04 dual_loss=3.9213e-01
Validation X2Y - loss=1.0031e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9713e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 351 - |param|=1.04e+03 |g_param|=2.03e+05 loss_x2y=4.1742e-02 ppl_x2y=1.04 loss_y2x=3.9095e-02 ppl_y2x=1.04 dual_loss=4.3397e-01
Validation X2Y - loss=9.9614e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0322e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 352 - |param|=1.04e+03 |g_param|=1.80e+05 loss_x2y=4.2337e-02 ppl_x2y=1.04 loss_y2x=4.2637e-02 ppl_y2x=1.04 dual_loss=4.5347e-01
Validation X2Y - loss=1.0225e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8159e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 353 - |param|=1.04e+03 |g_param|=1.70e+05 loss_x2y=4.1327e-02 ppl_x2y=1.04 loss_y2x=3.9897e-02 ppl_y2x=1.04 dual_loss=3.7307e-01
Validation X2Y - loss=1.0092e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9334e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 354 - |param|=1.04e+03 |g_param|=1.80e+05 loss_x2y=4.2187e-02 ppl_x2y=1.04 loss_y2x=4.0955e-02 ppl_y2x=1.04 dual_loss=3.9940e-01
Validation X2Y - loss=1.0017e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8025e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 355 - |param|=1.04e+03 |g_param|=1.88e+05 loss_x2y=4.4990e-02 ppl_x2y=1.05 loss_y2x=4.2368e-02 ppl_y2x=1.04 dual_loss=4.6601e-01
Validation X2Y - loss=1.0258e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7654e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 356 - |param|=1.04e+03 |g_param|=1.78e+05 loss_x2y=4.2559e-02 ppl_x2y=1.04 loss_y2x=4.1206e-02 ppl_y2x=1.04 dual_loss=4.8058e-01
Validation X2Y - loss=1.0176e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8066e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 357 - |param|=1.04e+03 |g_param|=1.86e+05 loss_x2y=4.3878e-02 ppl_x2y=1.04 loss_y2x=4.0697e-02 ppl_y2x=1.04 dual_loss=4.7478e-01
Validation X2Y - loss=9.9944e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6836e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 358 - |param|=1.04e+03 |g_param|=1.97e+05 loss_x2y=4.4885e-02 ppl_x2y=1.05 loss_y2x=4.2860e-02 ppl_y2x=1.04 dual_loss=4.4553e-01
Validation X2Y - loss=1.0077e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8211e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 359 - |param|=1.04e+03 |g_param|=1.96e+05 loss_x2y=4.5126e-02 ppl_x2y=1.05 loss_y2x=4.3859e-02 ppl_y2x=1.04 dual_loss=4.9923e-01
Validation X2Y - loss=1.0149e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6588e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 360 - |param|=1.04e+03 |g_param|=1.84e+05 loss_x2y=4.4044e-02 ppl_x2y=1.05 loss_y2x=4.0748e-02 ppl_y2x=1.04 dual_loss=4.5420e-01
Validation X2Y - loss=1.0206e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0614e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 361 - |param|=1.04e+03 |g_param|=1.83e+05 loss_x2y=4.1813e-02 ppl_x2y=1.04 loss_y2x=4.1252e-02 ppl_y2x=1.04 dual_loss=4.6096e-01
Validation X2Y - loss=1.0139e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9837e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 362 - |param|=1.04e+03 |g_param|=1.95e+05 loss_x2y=4.4070e-02 ppl_x2y=1.05 loss_y2x=4.2392e-02 ppl_y2x=1.04 dual_loss=4.8994e-01
Validation X2Y - loss=1.0110e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9293e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 363 - |param|=1.04e+03 |g_param|=2.36e+05 loss_x2y=4.2470e-02 ppl_x2y=1.04 loss_y2x=4.0111e-02 ppl_y2x=1.04 dual_loss=4.1029e-01
Validation X2Y - loss=9.7066e-01 ppl=2.64 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4769e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 364 - |param|=1.04e+03 |g_param|=2.43e+05 loss_x2y=4.2936e-02 ppl_x2y=1.04 loss_y2x=4.1542e-02 ppl_y2x=1.04 dual_loss=4.0458e-01
Validation X2Y - loss=1.0166e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4894e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 365 - |param|=1.04e+03 |g_param|=2.43e+05 loss_x2y=4.1398e-02 ppl_x2y=1.04 loss_y2x=3.9771e-02 ppl_y2x=1.04 dual_loss=3.8046e-01
Validation X2Y - loss=1.0237e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8261e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 366 - |param|=1.04e+03 |g_param|=2.47e+05 loss_x2y=4.1935e-02 ppl_x2y=1.04 loss_y2x=4.1122e-02 ppl_y2x=1.04 dual_loss=3.9671e-01
Validation X2Y - loss=1.0283e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5501e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 367 - |param|=1.04e+03 |g_param|=2.63e+05 loss_x2y=4.1967e-02 ppl_x2y=1.04 loss_y2x=4.3456e-02 ppl_y2x=1.04 dual_loss=4.4295e-01
Validation X2Y - loss=1.0091e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5338e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 368 - |param|=1.04e+03 |g_param|=2.39e+05 loss_x2y=4.1036e-02 ppl_x2y=1.04 loss_y2x=3.9788e-02 ppl_y2x=1.04 dual_loss=4.2675e-01
Validation X2Y - loss=1.0102e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9194e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 369 - |param|=1.04e+03 |g_param|=2.35e+05 loss_x2y=4.1569e-02 ppl_x2y=1.04 loss_y2x=3.9975e-02 ppl_y2x=1.04 dual_loss=4.4495e-01
Validation X2Y - loss=1.0089e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9121e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 370 - |param|=1.04e+03 |g_param|=2.40e+05 loss_x2y=4.1107e-02 ppl_x2y=1.04 loss_y2x=4.0298e-02 ppl_y2x=1.04 dual_loss=3.8571e-01
Validation X2Y - loss=1.0208e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6382e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 371 - |param|=1.04e+03 |g_param|=3.64e+05 loss_x2y=4.1950e-02 ppl_x2y=1.04 loss_y2x=4.0720e-02 ppl_y2x=1.04 dual_loss=4.4495e-01
Validation X2Y - loss=9.8867e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6077e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 372 - |param|=1.04e+03 |g_param|=3.86e+05 loss_x2y=4.1515e-02 ppl_x2y=1.04 loss_y2x=4.3642e-02 ppl_y2x=1.04 dual_loss=4.3580e-01
Validation X2Y - loss=9.9880e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4533e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 373 - |param|=1.04e+03 |g_param|=3.64e+05 loss_x2y=4.1274e-02 ppl_x2y=1.04 loss_y2x=4.0409e-02 ppl_y2x=1.04 dual_loss=4.0662e-01
Validation X2Y - loss=1.0230e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5141e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 374 - |param|=1.04e+03 |g_param|=2.95e+05 loss_x2y=3.9490e-02 ppl_x2y=1.04 loss_y2x=4.0142e-02 ppl_y2x=1.04 dual_loss=3.9712e-01
Validation X2Y - loss=1.0250e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6962e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 375 - |param|=1.04e+03 |g_param|=3.23e+05 loss_x2y=4.1157e-02 ppl_x2y=1.04 loss_y2x=4.0559e-02 ppl_y2x=1.04 dual_loss=4.3394e-01
Validation X2Y - loss=1.0056e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6068e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 376 - |param|=1.04e+03 |g_param|=3.10e+05 loss_x2y=4.0754e-02 ppl_x2y=1.04 loss_y2x=3.9149e-02 ppl_y2x=1.04 dual_loss=3.9313e-01
Validation X2Y - loss=1.0369e+00 ppl=2.82 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6819e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 377 - |param|=1.04e+03 |g_param|=2.90e+05 loss_x2y=3.9051e-02 ppl_x2y=1.04 loss_y2x=4.1378e-02 ppl_y2x=1.04 dual_loss=4.0468e-01
Validation X2Y - loss=1.0104e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5296e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 378 - |param|=1.04e+03 |g_param|=2.89e+05 loss_x2y=3.8190e-02 ppl_x2y=1.04 loss_y2x=3.9600e-02 ppl_y2x=1.04 dual_loss=3.7009e-01
Validation X2Y - loss=1.0023e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5462e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 379 - |param|=1.05e+03 |g_param|=2.09e+05 loss_x2y=4.0066e-02 ppl_x2y=1.04 loss_y2x=4.0182e-02 ppl_y2x=1.04 dual_loss=3.7399e-01
Validation X2Y - loss=1.0315e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8367e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 380 - |param|=1.05e+03 |g_param|=1.91e+05 loss_x2y=4.5529e-02 ppl_x2y=1.05 loss_y2x=4.2466e-02 ppl_y2x=1.04 dual_loss=4.1606e-01
Validation X2Y - loss=1.0073e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0624e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 381 - |param|=1.05e+03 |g_param|=1.55e+05 loss_x2y=3.8098e-02 ppl_x2y=1.04 loss_y2x=4.0132e-02 ppl_y2x=1.04 dual_loss=3.6825e-01
Validation X2Y - loss=1.0051e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6374e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 382 - |param|=1.05e+03 |g_param|=1.78e+05 loss_x2y=4.1192e-02 ppl_x2y=1.04 loss_y2x=4.1079e-02 ppl_y2x=1.04 dual_loss=4.1157e-01
Validation X2Y - loss=1.0385e+00 ppl=2.82 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6406e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 383 - |param|=1.05e+03 |g_param|=1.85e+05 loss_x2y=4.0903e-02 ppl_x2y=1.04 loss_y2x=4.0883e-02 ppl_y2x=1.04 dual_loss=4.2225e-01
Validation X2Y - loss=1.0292e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8107e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 384 - |param|=1.05e+03 |g_param|=1.79e+05 loss_x2y=4.1424e-02 ppl_x2y=1.04 loss_y2x=3.8382e-02 ppl_y2x=1.04 dual_loss=3.8358e-01
Validation X2Y - loss=1.0274e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8043e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 385 - |param|=1.05e+03 |g_param|=1.75e+05 loss_x2y=4.0474e-02 ppl_x2y=1.04 loss_y2x=3.8836e-02 ppl_y2x=1.04 dual_loss=3.6628e-01
Validation X2Y - loss=1.0292e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8617e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 386 - |param|=1.05e+03 |g_param|=1.80e+05 loss_x2y=4.2285e-02 ppl_x2y=1.04 loss_y2x=3.9701e-02 ppl_y2x=1.04 dual_loss=4.4903e-01
Validation X2Y - loss=9.9589e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4668e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 387 - |param|=1.05e+03 |g_param|=1.23e+05 loss_x2y=3.9529e-02 ppl_x2y=1.04 loss_y2x=3.8963e-02 ppl_y2x=1.04 dual_loss=3.9415e-01
Validation X2Y - loss=1.0025e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9710e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 388 - |param|=1.05e+03 |g_param|=1.17e+05 loss_x2y=4.4380e-02 ppl_x2y=1.05 loss_y2x=4.0827e-02 ppl_y2x=1.04 dual_loss=4.3865e-01
Validation X2Y - loss=9.9003e-01 ppl=2.69 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8304e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 389 - |param|=1.05e+03 |g_param|=1.24e+05 loss_x2y=4.1785e-02 ppl_x2y=1.04 loss_y2x=4.2438e-02 ppl_y2x=1.04 dual_loss=4.5970e-01
Validation X2Y - loss=1.0051e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6736e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 390 - |param|=1.05e+03 |g_param|=1.21e+05 loss_x2y=3.9710e-02 ppl_x2y=1.04 loss_y2x=3.9992e-02 ppl_y2x=1.04 dual_loss=4.6944e-01
Validation X2Y - loss=1.0182e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7600e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 391 - |param|=1.05e+03 |g_param|=1.24e+05 loss_x2y=4.1402e-02 ppl_x2y=1.04 loss_y2x=4.0794e-02 ppl_y2x=1.04 dual_loss=4.0127e-01
Validation X2Y - loss=1.0543e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7067e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 392 - |param|=1.05e+03 |g_param|=1.18e+05 loss_x2y=4.1046e-02 ppl_x2y=1.04 loss_y2x=3.8954e-02 ppl_y2x=1.04 dual_loss=4.7247e-01
Validation X2Y - loss=9.9966e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7026e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 393 - |param|=1.05e+03 |g_param|=1.17e+05 loss_x2y=4.2439e-02 ppl_x2y=1.04 loss_y2x=3.9302e-02 ppl_y2x=1.04 dual_loss=3.8745e-01
Validation X2Y - loss=9.7959e-01 ppl=2.66 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0740e-01 ppl=2.48 best_loss=5.8312e-01 best_ppl=1.79
Epoch 394 - |param|=1.05e+03 |g_param|=1.51e+05 loss_x2y=4.0937e-02 ppl_x2y=1.04 loss_y2x=4.0038e-02 ppl_y2x=1.04 dual_loss=3.9680e-01
Validation X2Y - loss=1.0157e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8560e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 395 - |param|=1.05e+03 |g_param|=1.90e+05 loss_x2y=3.9313e-02 ppl_x2y=1.04 loss_y2x=3.8253e-02 ppl_y2x=1.04 dual_loss=3.7369e-01
Validation X2Y - loss=1.0106e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8709e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 396 - |param|=1.05e+03 |g_param|=1.92e+05 loss_x2y=4.1714e-02 ppl_x2y=1.04 loss_y2x=4.0686e-02 ppl_y2x=1.04 dual_loss=4.2059e-01
Validation X2Y - loss=1.0109e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8384e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 397 - |param|=1.05e+03 |g_param|=1.83e+05 loss_x2y=3.9541e-02 ppl_x2y=1.04 loss_y2x=3.7273e-02 ppl_y2x=1.04 dual_loss=3.9743e-01
Validation X2Y - loss=1.0326e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7856e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 398 - |param|=1.05e+03 |g_param|=1.66e+05 loss_x2y=3.7740e-02 ppl_x2y=1.04 loss_y2x=3.6041e-02 ppl_y2x=1.04 dual_loss=3.4374e-01
Validation X2Y - loss=1.0080e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7181e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 399 - |param|=1.05e+03 |g_param|=1.81e+05 loss_x2y=3.9815e-02 ppl_x2y=1.04 loss_y2x=3.9813e-02 ppl_y2x=1.04 dual_loss=3.8790e-01
Validation X2Y - loss=1.0163e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8323e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 400 - |param|=1.05e+03 |g_param|=1.77e+05 loss_x2y=4.0630e-02 ppl_x2y=1.04 loss_y2x=3.6844e-02 ppl_y2x=1.04 dual_loss=3.6652e-01
Validation X2Y - loss=1.0119e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8241e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 401 - |param|=1.05e+03 |g_param|=1.94e+05 loss_x2y=3.9938e-02 ppl_x2y=1.04 loss_y2x=4.1012e-02 ppl_y2x=1.04 dual_loss=4.0443e-01
Validation X2Y - loss=1.0133e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9180e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 402 - |param|=1.05e+03 |g_param|=2.06e+05 loss_x2y=4.0064e-02 ppl_x2y=1.04 loss_y2x=4.0153e-02 ppl_y2x=1.04 dual_loss=4.5445e-01
Validation X2Y - loss=1.0043e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1368e-01 ppl=2.49 best_loss=5.8312e-01 best_ppl=1.79
Epoch 403 - |param|=1.05e+03 |g_param|=1.96e+05 loss_x2y=4.1793e-02 ppl_x2y=1.04 loss_y2x=4.0714e-02 ppl_y2x=1.04 dual_loss=4.2856e-01
Validation X2Y - loss=1.0263e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6255e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 404 - |param|=1.05e+03 |g_param|=1.89e+05 loss_x2y=3.9478e-02 ppl_x2y=1.04 loss_y2x=3.9254e-02 ppl_y2x=1.04 dual_loss=4.2798e-01
Validation X2Y - loss=1.0336e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8070e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 405 - |param|=1.05e+03 |g_param|=1.93e+05 loss_x2y=3.9714e-02 ppl_x2y=1.04 loss_y2x=3.9935e-02 ppl_y2x=1.04 dual_loss=4.1994e-01
Validation X2Y - loss=1.0286e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5914e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 406 - |param|=1.05e+03 |g_param|=1.83e+05 loss_x2y=4.0924e-02 ppl_x2y=1.04 loss_y2x=3.9592e-02 ppl_y2x=1.04 dual_loss=4.4978e-01
Validation X2Y - loss=1.0288e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4802e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 407 - |param|=1.05e+03 |g_param|=1.90e+05 loss_x2y=3.9278e-02 ppl_x2y=1.04 loss_y2x=3.9969e-02 ppl_y2x=1.04 dual_loss=4.0224e-01
Validation X2Y - loss=1.0084e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5377e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 408 - |param|=1.05e+03 |g_param|=2.37e+05 loss_x2y=4.0100e-02 ppl_x2y=1.04 loss_y2x=4.0310e-02 ppl_y2x=1.04 dual_loss=4.9135e-01
Validation X2Y - loss=1.0388e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7120e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 409 - |param|=1.05e+03 |g_param|=2.20e+05 loss_x2y=3.9280e-02 ppl_x2y=1.04 loss_y2x=3.9204e-02 ppl_y2x=1.04 dual_loss=3.8267e-01
Validation X2Y - loss=1.0154e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6966e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 410 - |param|=1.06e+03 |g_param|=2.31e+05 loss_x2y=3.9399e-02 ppl_x2y=1.04 loss_y2x=3.9682e-02 ppl_y2x=1.04 dual_loss=4.3187e-01
Validation X2Y - loss=1.0245e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.3002e-01 ppl=2.29 best_loss=5.8312e-01 best_ppl=1.79
Epoch 411 - |param|=1.06e+03 |g_param|=2.14e+05 loss_x2y=3.8288e-02 ppl_x2y=1.04 loss_y2x=3.8313e-02 ppl_y2x=1.04 dual_loss=3.7437e-01
Validation X2Y - loss=1.0387e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4752e-01 ppl=2.33 best_loss=5.8312e-01 best_ppl=1.79
Epoch 412 - |param|=1.06e+03 |g_param|=2.22e+05 loss_x2y=4.0436e-02 ppl_x2y=1.04 loss_y2x=4.0401e-02 ppl_y2x=1.04 dual_loss=4.9406e-01
Validation X2Y - loss=1.0145e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7396e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 413 - |param|=1.06e+03 |g_param|=2.29e+05 loss_x2y=3.9702e-02 ppl_x2y=1.04 loss_y2x=3.9463e-02 ppl_y2x=1.04 dual_loss=4.1355e-01
Validation X2Y - loss=1.0393e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6828e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 414 - |param|=1.06e+03 |g_param|=1.73e+05 loss_x2y=3.8025e-02 ppl_x2y=1.04 loss_y2x=3.6619e-02 ppl_y2x=1.04 dual_loss=3.4917e-01
Validation X2Y - loss=1.0488e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5232e-01 ppl=2.35 best_loss=5.8312e-01 best_ppl=1.79
Epoch 415 - |param|=1.06e+03 |g_param|=1.69e+05 loss_x2y=3.7414e-02 ppl_x2y=1.04 loss_y2x=3.9621e-02 ppl_y2x=1.04 dual_loss=4.0661e-01
Validation X2Y - loss=1.0441e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8938e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 416 - |param|=1.06e+03 |g_param|=1.76e+05 loss_x2y=4.0634e-02 ppl_x2y=1.04 loss_y2x=3.8670e-02 ppl_y2x=1.04 dual_loss=4.6691e-01
Validation X2Y - loss=1.0337e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6916e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 417 - |param|=1.06e+03 |g_param|=1.67e+05 loss_x2y=4.0054e-02 ppl_x2y=1.04 loss_y2x=3.8837e-02 ppl_y2x=1.04 dual_loss=4.7244e-01
Validation X2Y - loss=1.0247e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6726e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 418 - |param|=1.06e+03 |g_param|=1.72e+05 loss_x2y=3.8503e-02 ppl_x2y=1.04 loss_y2x=3.9932e-02 ppl_y2x=1.04 dual_loss=4.2442e-01
Validation X2Y - loss=1.0418e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6756e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 419 - |param|=1.06e+03 |g_param|=1.76e+05 loss_x2y=4.0218e-02 ppl_x2y=1.04 loss_y2x=3.9442e-02 ppl_y2x=1.04 dual_loss=4.4759e-01
Validation X2Y - loss=1.0456e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4923e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 420 - |param|=1.06e+03 |g_param|=1.72e+05 loss_x2y=3.9328e-02 ppl_x2y=1.04 loss_y2x=3.9731e-02 ppl_y2x=1.04 dual_loss=4.5289e-01
Validation X2Y - loss=1.0330e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6770e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 421 - |param|=1.06e+03 |g_param|=1.67e+05 loss_x2y=4.1248e-02 ppl_x2y=1.04 loss_y2x=4.0754e-02 ppl_y2x=1.04 dual_loss=4.2446e-01
Validation X2Y - loss=1.0558e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7568e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 422 - |param|=1.06e+03 |g_param|=1.83e+05 loss_x2y=4.1378e-02 ppl_x2y=1.04 loss_y2x=3.9572e-02 ppl_y2x=1.04 dual_loss=4.9285e-01
Validation X2Y - loss=1.0301e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8080e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 423 - |param|=1.06e+03 |g_param|=1.74e+05 loss_x2y=3.8787e-02 ppl_x2y=1.04 loss_y2x=3.9432e-02 ppl_y2x=1.04 dual_loss=4.2276e-01
Validation X2Y - loss=1.0292e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9544e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 424 - |param|=1.06e+03 |g_param|=1.71e+05 loss_x2y=3.8122e-02 ppl_x2y=1.04 loss_y2x=3.8077e-02 ppl_y2x=1.04 dual_loss=3.8442e-01
Validation X2Y - loss=1.0168e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9327e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 425 - |param|=1.06e+03 |g_param|=1.71e+05 loss_x2y=3.8608e-02 ppl_x2y=1.04 loss_y2x=3.8930e-02 ppl_y2x=1.04 dual_loss=4.0844e-01
Validation X2Y - loss=1.0340e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5931e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 426 - |param|=1.06e+03 |g_param|=1.75e+05 loss_x2y=3.9348e-02 ppl_x2y=1.04 loss_y2x=3.7593e-02 ppl_y2x=1.04 dual_loss=4.4016e-01
Validation X2Y - loss=1.0517e+00 ppl=2.86 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7528e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 427 - |param|=1.06e+03 |g_param|=1.68e+05 loss_x2y=3.9407e-02 ppl_x2y=1.04 loss_y2x=3.8123e-02 ppl_y2x=1.04 dual_loss=4.0289e-01
Validation X2Y - loss=1.0583e+00 ppl=2.88 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9110e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 428 - |param|=1.06e+03 |g_param|=2.91e+05 loss_x2y=3.7554e-02 ppl_x2y=1.04 loss_y2x=3.8051e-02 ppl_y2x=1.04 dual_loss=3.8984e-01
Validation X2Y - loss=1.0272e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8787e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 429 - |param|=1.06e+03 |g_param|=1.71e+05 loss_x2y=3.8093e-02 ppl_x2y=1.04 loss_y2x=3.6676e-02 ppl_y2x=1.04 dual_loss=4.3323e-01
Validation X2Y - loss=1.0391e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7821e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 430 - |param|=1.06e+03 |g_param|=1.69e+05 loss_x2y=3.7723e-02 ppl_x2y=1.04 loss_y2x=3.7289e-02 ppl_y2x=1.04 dual_loss=4.2875e-01
Validation X2Y - loss=1.0111e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9898e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 431 - |param|=1.06e+03 |g_param|=1.60e+05 loss_x2y=3.7529e-02 ppl_x2y=1.04 loss_y2x=3.7812e-02 ppl_y2x=1.04 dual_loss=3.9305e-01
Validation X2Y - loss=1.0340e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6377e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 432 - |param|=1.06e+03 |g_param|=1.68e+05 loss_x2y=3.9374e-02 ppl_x2y=1.04 loss_y2x=3.8873e-02 ppl_y2x=1.04 dual_loss=4.6133e-01
Validation X2Y - loss=1.0228e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.5773e-01 ppl=2.36 best_loss=5.8312e-01 best_ppl=1.79
Epoch 433 - |param|=1.06e+03 |g_param|=1.61e+05 loss_x2y=3.8696e-02 ppl_x2y=1.04 loss_y2x=3.7044e-02 ppl_y2x=1.04 dual_loss=3.9242e-01
Validation X2Y - loss=1.0428e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6750e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 434 - |param|=1.06e+03 |g_param|=1.85e+05 loss_x2y=3.9079e-02 ppl_x2y=1.04 loss_y2x=3.7799e-02 ppl_y2x=1.04 dual_loss=4.0062e-01
Validation X2Y - loss=1.0550e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4299e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 435 - |param|=1.06e+03 |g_param|=2.05e+05 loss_x2y=3.6289e-02 ppl_x2y=1.04 loss_y2x=3.6937e-02 ppl_y2x=1.04 dual_loss=3.7737e-01
Validation X2Y - loss=1.0539e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6417e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 436 - |param|=1.06e+03 |g_param|=2.18e+05 loss_x2y=4.0103e-02 ppl_x2y=1.04 loss_y2x=3.6225e-02 ppl_y2x=1.04 dual_loss=4.0515e-01
Validation X2Y - loss=1.0444e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4091e-01 ppl=2.32 best_loss=5.8312e-01 best_ppl=1.79
Epoch 437 - |param|=1.06e+03 |g_param|=2.24e+05 loss_x2y=3.8299e-02 ppl_x2y=1.04 loss_y2x=3.9126e-02 ppl_y2x=1.04 dual_loss=4.0539e-01
Validation X2Y - loss=1.0582e+00 ppl=2.88 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.4845e-01 ppl=2.34 best_loss=5.8312e-01 best_ppl=1.79
Epoch 438 - |param|=1.06e+03 |g_param|=1.81e+05 loss_x2y=3.8173e-02 ppl_x2y=1.04 loss_y2x=3.7494e-02 ppl_y2x=1.04 dual_loss=4.0014e-01
Validation X2Y - loss=1.0761e+00 ppl=2.93 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6999e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 439 - |param|=1.06e+03 |g_param|=1.65e+05 loss_x2y=3.7312e-02 ppl_x2y=1.04 loss_y2x=3.7474e-02 ppl_y2x=1.04 dual_loss=3.9663e-01
Validation X2Y - loss=1.0670e+00 ppl=2.91 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6154e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 440 - |param|=1.06e+03 |g_param|=1.46e+05 loss_x2y=3.6210e-02 ppl_x2y=1.04 loss_y2x=3.8073e-02 ppl_y2x=1.04 dual_loss=3.9210e-01
Validation X2Y - loss=1.0169e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7193e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 441 - |param|=1.07e+03 |g_param|=1.60e+05 loss_x2y=3.7713e-02 ppl_x2y=1.04 loss_y2x=3.6015e-02 ppl_y2x=1.04 dual_loss=3.7884e-01
Validation X2Y - loss=1.0902e+00 ppl=2.97 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6151e-01 ppl=2.37 best_loss=5.8312e-01 best_ppl=1.79
Epoch 442 - |param|=1.07e+03 |g_param|=1.57e+05 loss_x2y=3.7859e-02 ppl_x2y=1.04 loss_y2x=3.7768e-02 ppl_y2x=1.04 dual_loss=3.9598e-01
Validation X2Y - loss=1.0412e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8301e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 443 - |param|=1.07e+03 |g_param|=1.67e+05 loss_x2y=3.8401e-02 ppl_x2y=1.04 loss_y2x=3.8012e-02 ppl_y2x=1.04 dual_loss=4.2188e-01
Validation X2Y - loss=1.0263e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8956e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 444 - |param|=1.07e+03 |g_param|=1.60e+05 loss_x2y=3.8451e-02 ppl_x2y=1.04 loss_y2x=3.8041e-02 ppl_y2x=1.04 dual_loss=3.9085e-01
Validation X2Y - loss=1.0053e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1554e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 445 - |param|=1.07e+03 |g_param|=1.73e+05 loss_x2y=3.7929e-02 ppl_x2y=1.04 loss_y2x=3.6508e-02 ppl_y2x=1.04 dual_loss=4.2131e-01
Validation X2Y - loss=1.0146e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8249e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 446 - |param|=1.07e+03 |g_param|=1.74e+05 loss_x2y=3.7207e-02 ppl_x2y=1.04 loss_y2x=3.6206e-02 ppl_y2x=1.04 dual_loss=4.2579e-01
Validation X2Y - loss=1.0069e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0184e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 447 - |param|=1.07e+03 |g_param|=1.66e+05 loss_x2y=4.0356e-02 ppl_x2y=1.04 loss_y2x=3.8485e-02 ppl_y2x=1.04 dual_loss=4.7398e-01
Validation X2Y - loss=1.0237e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7846e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 448 - |param|=1.07e+03 |g_param|=1.54e+05 loss_x2y=3.7209e-02 ppl_x2y=1.04 loss_y2x=3.6005e-02 ppl_y2x=1.04 dual_loss=3.7386e-01
Validation X2Y - loss=1.0429e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9534e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 449 - |param|=1.07e+03 |g_param|=2.54e+05 loss_x2y=3.6204e-02 ppl_x2y=1.04 loss_y2x=3.5171e-02 ppl_y2x=1.04 dual_loss=3.8222e-01
Validation X2Y - loss=1.0198e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7797e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 450 - |param|=1.07e+03 |g_param|=3.04e+05 loss_x2y=3.7659e-02 ppl_x2y=1.04 loss_y2x=3.5586e-02 ppl_y2x=1.04 dual_loss=4.2122e-01
Validation X2Y - loss=1.0389e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8413e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 451 - |param|=1.07e+03 |g_param|=2.12e+05 loss_x2y=3.7932e-02 ppl_x2y=1.04 loss_y2x=3.6579e-02 ppl_y2x=1.04 dual_loss=3.7152e-01
Validation X2Y - loss=1.0620e+00 ppl=2.89 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1134e-01 ppl=2.49 best_loss=5.8312e-01 best_ppl=1.79
Epoch 452 - |param|=1.07e+03 |g_param|=1.70e+05 loss_x2y=3.8683e-02 ppl_x2y=1.04 loss_y2x=3.8517e-02 ppl_y2x=1.04 dual_loss=3.9585e-01
Validation X2Y - loss=1.0223e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1703e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 453 - |param|=1.07e+03 |g_param|=1.67e+05 loss_x2y=3.9362e-02 ppl_x2y=1.04 loss_y2x=3.6152e-02 ppl_y2x=1.04 dual_loss=4.3575e-01
Validation X2Y - loss=1.0097e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0416e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 454 - |param|=1.07e+03 |g_param|=1.60e+05 loss_x2y=3.7753e-02 ppl_x2y=1.04 loss_y2x=3.5936e-02 ppl_y2x=1.04 dual_loss=3.7972e-01
Validation X2Y - loss=1.0097e+00 ppl=2.74 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0108e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 455 - |param|=1.07e+03 |g_param|=1.57e+05 loss_x2y=3.5213e-02 ppl_x2y=1.04 loss_y2x=3.4878e-02 ppl_y2x=1.04 dual_loss=3.6258e-01
Validation X2Y - loss=1.0560e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0526e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 456 - |param|=1.07e+03 |g_param|=1.63e+05 loss_x2y=3.6523e-02 ppl_x2y=1.04 loss_y2x=3.6282e-02 ppl_y2x=1.04 dual_loss=3.6328e-01
Validation X2Y - loss=1.0521e+00 ppl=2.86 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2729e-01 ppl=2.53 best_loss=5.8312e-01 best_ppl=1.79
Epoch 457 - |param|=1.07e+03 |g_param|=1.71e+05 loss_x2y=4.0358e-02 ppl_x2y=1.04 loss_y2x=3.8316e-02 ppl_y2x=1.04 dual_loss=4.8863e-01
Validation X2Y - loss=1.0106e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1820e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 458 - |param|=1.07e+03 |g_param|=1.61e+05 loss_x2y=3.6067e-02 ppl_x2y=1.04 loss_y2x=3.4644e-02 ppl_y2x=1.04 dual_loss=3.6668e-01
Validation X2Y - loss=1.0287e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8816e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 459 - |param|=1.07e+03 |g_param|=2.45e+05 loss_x2y=3.7916e-02 ppl_x2y=1.04 loss_y2x=3.7746e-02 ppl_y2x=1.04 dual_loss=4.1802e-01
Validation X2Y - loss=1.0055e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8024e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 460 - |param|=1.07e+03 |g_param|=2.08e+05 loss_x2y=3.8099e-02 ppl_x2y=1.04 loss_y2x=3.7982e-02 ppl_y2x=1.04 dual_loss=4.0418e-01
Validation X2Y - loss=1.0262e+00 ppl=2.79 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7832e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 461 - |param|=1.07e+03 |g_param|=2.17e+05 loss_x2y=3.9450e-02 ppl_x2y=1.04 loss_y2x=3.7417e-02 ppl_y2x=1.04 dual_loss=4.7535e-01
Validation X2Y - loss=1.0301e+00 ppl=2.80 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9155e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 462 - |param|=1.07e+03 |g_param|=2.42e+05 loss_x2y=3.8797e-02 ppl_x2y=1.04 loss_y2x=3.7148e-02 ppl_y2x=1.04 dual_loss=4.6437e-01
Validation X2Y - loss=1.0228e+00 ppl=2.78 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8614e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 463 - |param|=1.07e+03 |g_param|=1.80e+05 loss_x2y=3.5836e-02 ppl_x2y=1.04 loss_y2x=3.6176e-02 ppl_y2x=1.04 dual_loss=3.7463e-01
Validation X2Y - loss=1.0185e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2946e-01 ppl=2.53 best_loss=5.8312e-01 best_ppl=1.79
Epoch 464 - |param|=1.07e+03 |g_param|=1.75e+05 loss_x2y=3.6264e-02 ppl_x2y=1.04 loss_y2x=3.5996e-02 ppl_y2x=1.04 dual_loss=3.6433e-01
Validation X2Y - loss=1.0321e+00 ppl=2.81 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9710e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 465 - |param|=1.07e+03 |g_param|=1.97e+05 loss_x2y=3.7421e-02 ppl_x2y=1.04 loss_y2x=3.7615e-02 ppl_y2x=1.04 dual_loss=4.5149e-01
Validation X2Y - loss=9.9956e-01 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8949e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 466 - |param|=1.07e+03 |g_param|=1.43e+05 loss_x2y=4.0024e-02 ppl_x2y=1.04 loss_y2x=3.8963e-02 ppl_y2x=1.04 dual_loss=4.8722e-01
Validation X2Y - loss=1.0100e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.6880e-01 ppl=2.38 best_loss=5.8312e-01 best_ppl=1.79
Epoch 467 - |param|=1.07e+03 |g_param|=1.00e+05 loss_x2y=3.5084e-02 ppl_x2y=1.04 loss_y2x=3.5891e-02 ppl_y2x=1.04 dual_loss=3.9924e-01
Validation X2Y - loss=9.9864e-01 ppl=2.71 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8973e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 468 - |param|=1.07e+03 |g_param|=1.03e+05 loss_x2y=3.6289e-02 ppl_x2y=1.04 loss_y2x=3.4527e-02 ppl_y2x=1.04 dual_loss=3.8488e-01
Validation X2Y - loss=1.0099e+00 ppl=2.75 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7921e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 469 - |param|=1.07e+03 |g_param|=1.08e+05 loss_x2y=3.7954e-02 ppl_x2y=1.04 loss_y2x=3.5644e-02 ppl_y2x=1.04 dual_loss=4.2238e-01
Validation X2Y - loss=1.0453e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7829e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 470 - |param|=1.07e+03 |g_param|=1.01e+05 loss_x2y=3.4972e-02 ppl_x2y=1.04 loss_y2x=3.6569e-02 ppl_y2x=1.04 dual_loss=4.1113e-01
Validation X2Y - loss=1.0360e+00 ppl=2.82 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7637e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79
Epoch 471 - |param|=1.07e+03 |g_param|=1.08e+05 loss_x2y=3.6754e-02 ppl_x2y=1.04 loss_y2x=3.7082e-02 ppl_y2x=1.04 dual_loss=4.4924e-01
Validation X2Y - loss=1.0204e+00 ppl=2.77 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8396e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 472 - |param|=1.08e+03 |g_param|=1.03e+05 loss_x2y=3.6245e-02 ppl_x2y=1.04 loss_y2x=3.6878e-02 ppl_y2x=1.04 dual_loss=3.6319e-01
Validation X2Y - loss=1.0557e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7202e-01 ppl=2.39 best_loss=5.8312e-01 best_ppl=1.79
Epoch 473 - |param|=1.08e+03 |g_param|=1.11e+05 loss_x2y=3.7467e-02 ppl_x2y=1.04 loss_y2x=3.7286e-02 ppl_y2x=1.04 dual_loss=4.2540e-01
Validation X2Y - loss=1.0022e+00 ppl=2.72 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0220e-01 ppl=2.47 best_loss=5.8312e-01 best_ppl=1.79
Epoch 474 - |param|=1.08e+03 |g_param|=1.09e+05 loss_x2y=3.6375e-02 ppl_x2y=1.04 loss_y2x=3.6282e-02 ppl_y2x=1.04 dual_loss=4.0280e-01
Validation X2Y - loss=1.0397e+00 ppl=2.83 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2135e-01 ppl=2.51 best_loss=5.8312e-01 best_ppl=1.79
Epoch 475 - |param|=1.08e+03 |g_param|=1.02e+05 loss_x2y=3.4833e-02 ppl_x2y=1.04 loss_y2x=3.5138e-02 ppl_y2x=1.04 dual_loss=3.6846e-01
Validation X2Y - loss=1.0152e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2228e-01 ppl=2.52 best_loss=5.8312e-01 best_ppl=1.79
Epoch 476 - |param|=1.08e+03 |g_param|=1.09e+05 loss_x2y=3.9036e-02 ppl_x2y=1.04 loss_y2x=3.7875e-02 ppl_y2x=1.04 dual_loss=4.0473e-01
Validation X2Y - loss=9.8252e-01 ppl=2.67 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8547e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 477 - |param|=1.08e+03 |g_param|=9.85e+04 loss_x2y=3.7059e-02 ppl_x2y=1.04 loss_y2x=3.5321e-02 ppl_y2x=1.04 dual_loss=3.9688e-01
Validation X2Y - loss=1.0438e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8778e-01 ppl=2.43 best_loss=5.8312e-01 best_ppl=1.79
Epoch 478 - |param|=1.08e+03 |g_param|=1.06e+05 loss_x2y=3.8943e-02 ppl_x2y=1.04 loss_y2x=3.7306e-02 ppl_y2x=1.04 dual_loss=4.8534e-01
Validation X2Y - loss=1.0150e+00 ppl=2.76 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.2129e-01 ppl=2.51 best_loss=5.8312e-01 best_ppl=1.79
Epoch 479 - |param|=1.08e+03 |g_param|=1.06e+05 loss_x2y=3.5975e-02 ppl_x2y=1.04 loss_y2x=3.6593e-02 ppl_y2x=1.04 dual_loss=3.8290e-01
Validation X2Y - loss=1.0058e+00 ppl=2.73 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1601e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 480 - |param|=1.08e+03 |g_param|=1.05e+05 loss_x2y=3.6561e-02 ppl_x2y=1.04 loss_y2x=3.5123e-02 ppl_y2x=1.04 dual_loss=3.9981e-01
Validation X2Y - loss=1.0353e+00 ppl=2.82 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1763e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 481 - |param|=1.08e+03 |g_param|=9.95e+04 loss_x2y=3.5806e-02 ppl_x2y=1.04 loss_y2x=3.6175e-02 ppl_y2x=1.04 dual_loss=3.6313e-01
Validation X2Y - loss=1.0682e+00 ppl=2.91 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9817e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 482 - |param|=1.08e+03 |g_param|=9.85e+04 loss_x2y=3.5736e-02 ppl_x2y=1.04 loss_y2x=3.4045e-02 ppl_y2x=1.03 dual_loss=3.9999e-01
Validation X2Y - loss=1.0507e+00 ppl=2.86 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0153e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 483 - |param|=1.08e+03 |g_param|=1.52e+05 loss_x2y=3.8709e-02 ppl_x2y=1.04 loss_y2x=3.7619e-02 ppl_y2x=1.04 dual_loss=4.6239e-01
Validation X2Y - loss=1.0548e+00 ppl=2.87 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8996e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 484 - |param|=1.08e+03 |g_param|=1.74e+05 loss_x2y=3.8403e-02 ppl_x2y=1.04 loss_y2x=3.8394e-02 ppl_y2x=1.04 dual_loss=4.5209e-01
Validation X2Y - loss=1.0469e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0961e-01 ppl=2.48 best_loss=5.8312e-01 best_ppl=1.79
Epoch 485 - |param|=1.08e+03 |g_param|=1.64e+05 loss_x2y=3.8475e-02 ppl_x2y=1.04 loss_y2x=3.5405e-02 ppl_y2x=1.04 dual_loss=4.1977e-01
Validation X2Y - loss=1.0450e+00 ppl=2.84 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.3295e-01 ppl=2.54 best_loss=5.8312e-01 best_ppl=1.79
Epoch 486 - |param|=1.08e+03 |g_param|=1.54e+05 loss_x2y=3.7693e-02 ppl_x2y=1.04 loss_y2x=3.6000e-02 ppl_y2x=1.04 dual_loss=4.1709e-01
Validation X2Y - loss=1.0620e+00 ppl=2.89 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9608e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 487 - |param|=1.08e+03 |g_param|=2.03e+05 loss_x2y=3.7177e-02 ppl_x2y=1.04 loss_y2x=3.7100e-02 ppl_y2x=1.04 dual_loss=4.0977e-01
Validation X2Y - loss=1.0473e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.3646e-01 ppl=2.55 best_loss=5.8312e-01 best_ppl=1.79
Epoch 488 - |param|=1.08e+03 |g_param|=2.12e+05 loss_x2y=3.5794e-02 ppl_x2y=1.04 loss_y2x=3.4734e-02 ppl_y2x=1.04 dual_loss=3.8000e-01
Validation X2Y - loss=1.0682e+00 ppl=2.91 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9624e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 489 - |param|=1.08e+03 |g_param|=1.71e+05 loss_x2y=3.7309e-02 ppl_x2y=1.04 loss_y2x=3.5962e-02 ppl_y2x=1.04 dual_loss=4.3604e-01
Validation X2Y - loss=1.0458e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9236e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 490 - |param|=1.08e+03 |g_param|=1.53e+05 loss_x2y=3.6591e-02 ppl_x2y=1.04 loss_y2x=3.5476e-02 ppl_y2x=1.04 dual_loss=3.9562e-01
Validation X2Y - loss=1.0605e+00 ppl=2.89 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7853e-01 ppl=2.41 best_loss=5.8312e-01 best_ppl=1.79
Epoch 491 - |param|=1.08e+03 |g_param|=1.55e+05 loss_x2y=3.7818e-02 ppl_x2y=1.04 loss_y2x=3.7595e-02 ppl_y2x=1.04 dual_loss=4.3375e-01
Validation X2Y - loss=1.0745e+00 ppl=2.93 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9538e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 492 - |param|=1.08e+03 |g_param|=1.66e+05 loss_x2y=3.5606e-02 ppl_x2y=1.04 loss_y2x=3.3225e-02 ppl_y2x=1.03 dual_loss=4.0488e-01
Validation X2Y - loss=1.0505e+00 ppl=2.86 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9484e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 493 - |param|=1.08e+03 |g_param|=1.60e+05 loss_x2y=3.5770e-02 ppl_x2y=1.04 loss_y2x=3.6078e-02 ppl_y2x=1.04 dual_loss=3.7882e-01
Validation X2Y - loss=1.0495e+00 ppl=2.86 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8506e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 494 - |param|=1.08e+03 |g_param|=1.67e+05 loss_x2y=3.7327e-02 ppl_x2y=1.04 loss_y2x=3.6718e-02 ppl_y2x=1.04 dual_loss=4.3747e-01
Validation X2Y - loss=1.0923e+00 ppl=2.98 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9783e-01 ppl=2.45 best_loss=5.8312e-01 best_ppl=1.79
Epoch 495 - |param|=1.08e+03 |g_param|=1.62e+05 loss_x2y=3.8439e-02 ppl_x2y=1.04 loss_y2x=3.7225e-02 ppl_y2x=1.04 dual_loss=4.4639e-01
Validation X2Y - loss=1.0372e+00 ppl=2.82 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.1442e-01 ppl=2.50 best_loss=5.8312e-01 best_ppl=1.79
Epoch 496 - |param|=1.08e+03 |g_param|=1.53e+05 loss_x2y=3.5988e-02 ppl_x2y=1.04 loss_y2x=3.5883e-02 ppl_y2x=1.04 dual_loss=4.4022e-01
Validation X2Y - loss=1.0464e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0662e-01 ppl=2.48 best_loss=5.8312e-01 best_ppl=1.79
Epoch 497 - |param|=1.08e+03 |g_param|=1.63e+05 loss_x2y=3.8340e-02 ppl_x2y=1.04 loss_y2x=3.7446e-02 ppl_y2x=1.04 dual_loss=4.6531e-01
Validation X2Y - loss=1.0658e+00 ppl=2.90 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.9219e-01 ppl=2.44 best_loss=5.8312e-01 best_ppl=1.79
Epoch 498 - |param|=1.08e+03 |g_param|=1.64e+05 loss_x2y=3.6544e-02 ppl_x2y=1.04 loss_y2x=3.7623e-02 ppl_y2x=1.04 dual_loss=4.4722e-01
Validation X2Y - loss=1.0485e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.8250e-01 ppl=2.42 best_loss=5.8312e-01 best_ppl=1.79
Epoch 499 - |param|=1.08e+03 |g_param|=1.51e+05 loss_x2y=3.6566e-02 ppl_x2y=1.04 loss_y2x=3.5280e-02 ppl_y2x=1.04 dual_loss=4.0077e-01
Validation X2Y - loss=1.0732e+00 ppl=2.92 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=9.0182e-01 ppl=2.46 best_loss=5.8312e-01 best_ppl=1.79
Epoch 500 - |param|=1.08e+03 |g_param|=1.53e+05 loss_x2y=3.7268e-02 ppl_x2y=1.04 loss_y2x=3.7567e-02 ppl_y2x=1.04 dual_loss=4.7212e-01
Validation X2Y - loss=1.0487e+00 ppl=2.85 best_loss=6.3516e-01 best_ppl=1.89                                            
Validation Y2X - loss=8.7458e-01 ppl=2.40 best_loss=5.8312e-01 best_ppl=1.79

real	257m45.724s
user	253m53.343s
sys	3m52.191s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-transformerDSL-500epoch-xy.sh 
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-500epoch
Evaluation result for the model: dsl-model-myrk.01.3.52-33.81.3.53-34.28.2.91-18.35.2.85-17.32.pth, myrk
BLEU = 9.40, 38.5/16.2/6.0/2.1 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.52-33.81.3.53-34.28.2.91-18.35.2.85-17.32.pth, rkmy
BLEU = 7.76, 35.8/14.6/4.8/1.4 (BP=1.000, ratio=1.062, hyp_len=24967, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.36-10.57.2.30-10.02.2.00-7.39.1.92-6.81.pth, myrk
BLEU = 26.29, 57.3/34.5/20.4/11.8 (BP=1.000, ratio=1.015, hyp_len=23507, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.36-10.57.2.30-10.02.2.00-7.39.1.92-6.81.pth, rkmy
BLEU = 23.43, 53.0/31.3/17.9/10.2 (BP=1.000, ratio=1.073, hyp_len=25228, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.71-5.51.1.69-5.43.1.46-4.30.1.44-4.21.pth, myrk
BLEU = 42.03, 70.1/50.3/35.5/24.9 (BP=1.000, ratio=1.030, hyp_len=23862, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.71-5.51.1.69-5.43.1.46-4.30.1.44-4.21.pth, rkmy
BLEU = 40.55, 69.0/49.1/34.0/23.5 (BP=1.000, ratio=1.020, hyp_len=23973, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.29-3.62.1.28-3.59.1.16-3.20.1.11-3.04.pth, myrk
BLEU = 49.58, 74.3/57.1/43.5/32.7 (BP=1.000, ratio=1.061, hyp_len=24580, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.29-3.62.1.28-3.59.1.16-3.20.1.11-3.04.pth, rkmy
BLEU = 48.18, 72.2/55.5/41.9/32.1 (BP=1.000, ratio=1.066, hyp_len=25065, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.06.1.15-3.16.0.96-2.62.0.95-2.59.pth, myrk
BLEU = 57.29, 80.2/64.6/51.4/40.4 (BP=1.000, ratio=1.023, hyp_len=23691, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.06.1.15-3.16.0.96-2.62.0.95-2.59.pth, rkmy
BLEU = 50.23, 71.7/56.8/44.6/35.1 (BP=1.000, ratio=1.128, hyp_len=26517, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.92-2.51.0.92-2.51.0.91-2.48.0.83-2.29.pth, myrk
BLEU = 61.94, 83.0/68.3/56.2/46.2 (BP=1.000, ratio=1.010, hyp_len=23399, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.92-2.51.0.92-2.51.0.91-2.48.0.83-2.29.pth, rkmy
BLEU = 59.26, 79.8/66.0/53.7/43.6 (BP=1.000, ratio=1.046, hyp_len=24596, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.81-2.24.0.82-2.26.0.83-2.30.0.75-2.13.pth, myrk
BLEU = 62.86, 82.9/69.1/57.4/47.6 (BP=1.000, ratio=1.028, hyp_len=23807, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.81-2.24.0.82-2.26.0.83-2.30.0.75-2.13.pth, rkmy
BLEU = 61.63, 81.5/68.1/56.1/46.3 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.06.0.70-2.02.0.81-2.24.0.73-2.08.pth, myrk
BLEU = 65.57, 84.7/71.6/60.2/50.6 (BP=1.000, ratio=1.003, hyp_len=23218, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.06.0.70-2.02.0.81-2.24.0.73-2.08.pth, rkmy
BLEU = 63.71, 82.4/70.0/58.4/48.9 (BP=1.000, ratio=1.040, hyp_len=24453, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.68-1.98.0.69-1.99.0.76-2.13.0.71-2.04.pth, myrk
BLEU = 64.76, 83.6/70.7/59.6/50.0 (BP=1.000, ratio=1.038, hyp_len=24045, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.68-1.98.0.69-1.99.0.76-2.13.0.71-2.04.pth, rkmy
BLEU = 62.06, 81.0/68.7/56.8/47.0 (BP=1.000, ratio=1.069, hyp_len=25134, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.100.0.10-1.10.0.10-1.10.0.79-2.20.0.73-2.07.pth, myrk
BLEU = 69.94, 85.6/74.7/65.4/57.2 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.100.0.10-1.10.0.10-1.10.0.79-2.20.0.73-2.07.pth, rkmy
BLEU = 69.31, 84.9/74.2/64.6/56.7 (BP=1.000, ratio=1.062, hyp_len=24958, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.64-1.89.0.64-1.89.0.72-2.06.0.65-1.91.pth, myrk
BLEU = 67.12, 85.4/73.0/61.9/52.6 (BP=1.000, ratio=1.025, hyp_len=23734, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.64-1.89.0.64-1.89.0.72-2.06.0.65-1.91.pth, rkmy
BLEU = 66.26, 84.1/72.2/61.1/51.9 (BP=1.000, ratio=1.037, hyp_len=24376, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.101.0.09-1.10.0.09-1.10.0.82-2.26.0.70-2.02.pth, myrk
BLEU = 68.94, 85.0/73.8/64.3/56.0 (BP=1.000, ratio=1.053, hyp_len=24389, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.101.0.09-1.10.0.09-1.10.0.82-2.26.0.70-2.02.pth, rkmy
BLEU = 70.28, 85.6/75.2/65.6/57.8 (BP=1.000, ratio=1.054, hyp_len=24774, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.102.0.09-1.10.0.09-1.10.0.82-2.27.0.72-2.06.pth, myrk
BLEU = 69.10, 85.2/73.9/64.4/56.2 (BP=1.000, ratio=1.048, hyp_len=24279, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.102.0.09-1.10.0.09-1.10.0.82-2.27.0.72-2.06.pth, rkmy
BLEU = 69.85, 85.3/74.7/65.1/57.3 (BP=1.000, ratio=1.052, hyp_len=24735, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.103.0.10-1.10.0.10-1.10.0.80-2.23.0.72-2.06.pth, myrk
BLEU = 69.86, 85.5/74.6/65.2/57.3 (BP=1.000, ratio=1.047, hyp_len=24252, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.103.0.10-1.10.0.10-1.10.0.80-2.23.0.72-2.06.pth, rkmy
BLEU = 69.87, 85.3/74.8/65.2/57.3 (BP=1.000, ratio=1.059, hyp_len=24886, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.104.0.09-1.10.0.10-1.10.0.82-2.28.0.72-2.06.pth, myrk
BLEU = 69.68, 85.4/74.3/65.1/57.1 (BP=1.000, ratio=1.046, hyp_len=24236, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.104.0.09-1.10.0.10-1.10.0.82-2.28.0.72-2.06.pth, rkmy
BLEU = 71.21, 85.9/75.8/66.7/59.2 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.105.0.09-1.10.0.09-1.10.0.82-2.28.0.71-2.03.pth, myrk
BLEU = 69.59, 85.1/74.3/65.0/57.0 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.105.0.09-1.10.0.09-1.10.0.82-2.28.0.71-2.03.pth, rkmy
BLEU = 69.59, 85.0/74.5/64.9/57.1 (BP=1.000, ratio=1.063, hyp_len=24988, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.106.0.08-1.09.0.09-1.09.0.82-2.27.0.74-2.10.pth, myrk
BLEU = 69.93, 85.4/74.6/65.4/57.4 (BP=1.000, ratio=1.050, hyp_len=24314, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.106.0.08-1.09.0.09-1.09.0.82-2.27.0.74-2.10.pth, rkmy
BLEU = 70.68, 85.9/75.5/66.0/58.3 (BP=1.000, ratio=1.053, hyp_len=24757, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.107.0.09-1.09.0.09-1.09.0.82-2.28.0.75-2.12.pth, myrk
BLEU = 69.55, 85.4/74.5/65.0/56.7 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.107.0.09-1.09.0.09-1.09.0.82-2.28.0.75-2.12.pth, rkmy
BLEU = 71.93, 86.6/76.6/67.4/59.9 (BP=1.000, ratio=1.044, hyp_len=24554, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.108.0.09-1.09.0.09-1.09.0.85-2.34.0.73-2.09.pth, myrk
BLEU = 70.35, 85.8/75.0/65.8/57.8 (BP=1.000, ratio=1.046, hyp_len=24219, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.108.0.09-1.09.0.09-1.09.0.85-2.34.0.73-2.09.pth, rkmy
BLEU = 70.70, 85.8/75.5/66.1/58.4 (BP=1.000, ratio=1.053, hyp_len=24744, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.109.0.09-1.09.0.09-1.10.0.83-2.28.0.73-2.08.pth, myrk
BLEU = 70.86, 86.1/75.4/66.4/58.5 (BP=1.000, ratio=1.040, hyp_len=24076, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.109.0.09-1.09.0.09-1.10.0.83-2.28.0.73-2.08.pth, rkmy
BLEU = 69.83, 85.2/74.6/65.1/57.4 (BP=1.000, ratio=1.061, hyp_len=24945, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.110.0.09-1.09.0.09-1.09.0.85-2.35.0.74-2.09.pth, myrk
BLEU = 69.93, 85.6/74.7/65.3/57.2 (BP=1.000, ratio=1.048, hyp_len=24282, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.110.0.09-1.09.0.09-1.09.0.85-2.35.0.74-2.09.pth, rkmy
BLEU = 69.35, 84.7/74.1/64.7/56.9 (BP=1.000, ratio=1.064, hyp_len=25018, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.57-1.76.0.71-2.04.0.65-1.91.pth, myrk
BLEU = 66.11, 84.1/72.0/61.1/51.6 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.57-1.76.0.71-2.04.0.65-1.91.pth, rkmy
BLEU = 65.52, 83.1/71.2/60.4/51.6 (BP=1.000, ratio=1.047, hyp_len=24616, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.111.0.09-1.09.0.08-1.09.0.83-2.28.0.75-2.12.pth, myrk
BLEU = 70.96, 86.3/75.5/66.4/58.6 (BP=1.000, ratio=1.041, hyp_len=24110, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.111.0.09-1.09.0.08-1.09.0.83-2.28.0.75-2.12.pth, rkmy
BLEU = 70.17, 85.4/74.9/65.5/57.9 (BP=1.000, ratio=1.056, hyp_len=24816, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.112.0.08-1.09.0.09-1.09.0.85-2.34.0.75-2.12.pth, myrk
BLEU = 70.08, 86.0/75.0/65.5/57.2 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.112.0.08-1.09.0.09-1.09.0.85-2.34.0.75-2.12.pth, rkmy
BLEU = 71.07, 86.0/75.9/66.5/58.8 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.113.0.08-1.09.0.08-1.09.0.83-2.30.0.76-2.13.pth, myrk
BLEU = 69.71, 85.5/74.5/65.1/56.9 (BP=1.000, ratio=1.046, hyp_len=24231, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.113.0.08-1.09.0.08-1.09.0.83-2.30.0.76-2.13.pth, rkmy
BLEU = 69.91, 85.3/74.8/65.3/57.4 (BP=1.000, ratio=1.058, hyp_len=24875, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.114.0.09-1.09.0.08-1.09.0.87-2.38.0.76-2.13.pth, myrk
BLEU = 70.02, 85.8/74.8/65.3/57.4 (BP=1.000, ratio=1.044, hyp_len=24173, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.114.0.09-1.09.0.08-1.09.0.87-2.38.0.76-2.13.pth, rkmy
BLEU = 70.86, 85.9/75.7/66.2/58.6 (BP=1.000, ratio=1.053, hyp_len=24749, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.115.0.08-1.09.0.09-1.09.0.83-2.30.0.74-2.09.pth, myrk
BLEU = 69.87, 85.5/74.5/65.3/57.3 (BP=1.000, ratio=1.046, hyp_len=24228, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.115.0.08-1.09.0.09-1.09.0.83-2.30.0.74-2.09.pth, rkmy
BLEU = 68.87, 84.5/73.8/64.1/56.3 (BP=1.000, ratio=1.066, hyp_len=25064, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.116.0.08-1.09.0.09-1.09.0.84-2.32.0.75-2.12.pth, myrk
BLEU = 70.22, 85.5/74.8/65.7/57.9 (BP=1.000, ratio=1.044, hyp_len=24170, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.116.0.08-1.09.0.09-1.09.0.84-2.32.0.75-2.12.pth, rkmy
BLEU = 69.73, 85.1/74.6/65.1/57.2 (BP=1.000, ratio=1.061, hyp_len=24949, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.117.0.08-1.09.0.08-1.09.0.86-2.37.0.76-2.14.pth, myrk
BLEU = 70.19, 85.9/75.0/65.6/57.4 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.117.0.08-1.09.0.08-1.09.0.86-2.37.0.76-2.14.pth, rkmy
BLEU = 69.84, 85.4/74.7/65.1/57.2 (BP=1.000, ratio=1.059, hyp_len=24890, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.118.0.08-1.09.0.09-1.09.0.86-2.36.0.76-2.13.pth, myrk
BLEU = 70.96, 86.5/75.7/66.4/58.4 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.118.0.08-1.09.0.09-1.09.0.86-2.36.0.76-2.13.pth, rkmy
BLEU = 71.17, 86.0/75.9/66.6/59.0 (BP=1.000, ratio=1.051, hyp_len=24712, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.119.0.08-1.08.0.08-1.09.0.86-2.37.0.73-2.07.pth, myrk
BLEU = 70.01, 86.0/74.9/65.4/57.1 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.119.0.08-1.08.0.08-1.09.0.86-2.37.0.73-2.07.pth, rkmy
BLEU = 69.90, 85.2/74.8/65.2/57.5 (BP=1.000, ratio=1.059, hyp_len=24890, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.120.0.08-1.09.0.08-1.09.0.86-2.35.0.73-2.08.pth, myrk
BLEU = 68.92, 85.1/73.8/64.2/56.0 (BP=1.000, ratio=1.052, hyp_len=24375, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.120.0.08-1.09.0.08-1.09.0.86-2.35.0.73-2.08.pth, rkmy
BLEU = 70.59, 85.6/75.4/66.0/58.3 (BP=1.000, ratio=1.053, hyp_len=24762, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.49-1.63.0.49-1.64.0.68-1.97.0.65-1.92.pth, myrk
BLEU = 67.79, 85.1/73.3/62.9/53.9 (BP=1.000, ratio=1.035, hyp_len=23960, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.49-1.63.0.49-1.64.0.68-1.97.0.65-1.92.pth, rkmy
BLEU = 64.00, 81.9/69.8/58.9/49.9 (BP=1.000, ratio=1.070, hyp_len=25163, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.121.0.08-1.08.0.08-1.08.0.84-2.32.0.72-2.06.pth, myrk
BLEU = 70.15, 85.8/74.8/65.5/57.6 (BP=1.000, ratio=1.042, hyp_len=24124, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.121.0.08-1.08.0.08-1.08.0.84-2.32.0.72-2.06.pth, rkmy
BLEU = 69.63, 85.1/74.6/64.9/57.1 (BP=1.000, ratio=1.061, hyp_len=24938, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.122.0.08-1.09.0.08-1.09.0.86-2.36.0.75-2.11.pth, myrk
BLEU = 68.89, 84.9/73.7/64.3/56.1 (BP=1.000, ratio=1.056, hyp_len=24457, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.122.0.08-1.09.0.08-1.09.0.86-2.36.0.75-2.11.pth, rkmy
BLEU = 70.15, 85.5/74.9/65.4/57.8 (BP=1.000, ratio=1.055, hyp_len=24805, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.123.0.08-1.09.0.08-1.09.0.83-2.29.0.76-2.14.pth, myrk
BLEU = 69.34, 85.5/74.3/64.7/56.3 (BP=1.000, ratio=1.051, hyp_len=24347, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.123.0.08-1.09.0.08-1.09.0.83-2.29.0.76-2.14.pth, rkmy
BLEU = 70.54, 85.9/75.3/65.9/58.1 (BP=1.000, ratio=1.052, hyp_len=24735, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.124.0.08-1.08.0.08-1.08.0.84-2.32.0.75-2.11.pth, myrk
BLEU = 69.31, 85.3/74.3/64.7/56.3 (BP=1.000, ratio=1.052, hyp_len=24373, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.124.0.08-1.08.0.08-1.08.0.84-2.32.0.75-2.11.pth, rkmy
BLEU = 71.08, 86.1/75.8/66.4/58.9 (BP=1.000, ratio=1.051, hyp_len=24711, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.125.0.08-1.08.0.08-1.08.0.85-2.34.0.74-2.10.pth, myrk
BLEU = 70.13, 85.6/74.7/65.6/57.6 (BP=1.000, ratio=1.048, hyp_len=24269, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.125.0.08-1.08.0.08-1.08.0.85-2.34.0.74-2.10.pth, rkmy
BLEU = 70.47, 85.6/75.2/65.8/58.2 (BP=1.000, ratio=1.056, hyp_len=24825, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.126.0.08-1.08.0.08-1.08.0.86-2.37.0.76-2.14.pth, myrk
BLEU = 70.37, 85.7/75.0/65.8/57.9 (BP=1.000, ratio=1.046, hyp_len=24234, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.126.0.08-1.08.0.08-1.08.0.86-2.37.0.76-2.14.pth, rkmy
BLEU = 69.74, 85.1/74.6/65.0/57.3 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.127.0.08-1.08.0.08-1.08.0.86-2.37.0.78-2.18.pth, myrk
BLEU = 69.98, 85.7/74.7/65.3/57.3 (BP=1.000, ratio=1.048, hyp_len=24273, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.127.0.08-1.08.0.08-1.08.0.86-2.37.0.78-2.18.pth, rkmy
BLEU = 71.48, 86.2/76.1/66.9/59.4 (BP=1.000, ratio=1.051, hyp_len=24703, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.128.0.08-1.08.0.08-1.08.0.90-2.46.0.76-2.14.pth, myrk
BLEU = 70.12, 85.8/74.9/65.5/57.4 (BP=1.000, ratio=1.044, hyp_len=24179, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.128.0.08-1.08.0.08-1.08.0.90-2.46.0.76-2.14.pth, rkmy
BLEU = 70.15, 85.5/75.1/65.5/57.6 (BP=1.000, ratio=1.055, hyp_len=24807, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.129.0.07-1.08.0.08-1.08.0.87-2.40.0.76-2.14.pth, myrk
BLEU = 69.63, 85.5/74.4/65.0/56.9 (BP=1.000, ratio=1.050, hyp_len=24310, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.129.0.07-1.08.0.08-1.08.0.87-2.40.0.76-2.14.pth, rkmy
BLEU = 71.30, 86.1/75.9/66.7/59.3 (BP=1.000, ratio=1.049, hyp_len=24656, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.130.0.08-1.08.0.08-1.08.0.84-2.33.0.76-2.14.pth, myrk
BLEU = 71.13, 86.5/75.7/66.6/58.7 (BP=1.000, ratio=1.041, hyp_len=24110, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.130.0.08-1.08.0.08-1.08.0.84-2.33.0.76-2.14.pth, rkmy
BLEU = 71.16, 86.0/75.8/66.6/59.1 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.64.0.48-1.62.0.70-2.02.0.61-1.85.pth, myrk
BLEU = 68.08, 85.9/73.4/62.9/54.1 (BP=1.000, ratio=1.018, hyp_len=23576, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.64.0.48-1.62.0.70-2.02.0.61-1.85.pth, rkmy
BLEU = 66.36, 83.9/72.3/61.3/52.2 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.131.0.07-1.08.0.08-1.08.0.86-2.36.0.76-2.13.pth, myrk
BLEU = 70.04, 85.9/74.9/65.4/57.2 (BP=1.000, ratio=1.047, hyp_len=24239, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.131.0.07-1.08.0.08-1.08.0.86-2.36.0.76-2.13.pth, rkmy
BLEU = 70.80, 85.7/75.5/66.2/58.7 (BP=1.000, ratio=1.056, hyp_len=24824, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.132.0.08-1.08.0.08-1.08.0.85-2.35.0.76-2.14.pth, myrk
BLEU = 70.25, 86.0/75.0/65.6/57.5 (BP=1.000, ratio=1.046, hyp_len=24215, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.132.0.08-1.08.0.08-1.08.0.85-2.35.0.76-2.14.pth, rkmy
BLEU = 70.82, 85.6/75.4/66.2/58.9 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.133.0.07-1.08.0.08-1.08.0.88-2.41.0.77-2.17.pth, myrk
BLEU = 70.59, 86.0/75.2/66.1/58.1 (BP=1.000, ratio=1.045, hyp_len=24206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.133.0.07-1.08.0.08-1.08.0.88-2.41.0.77-2.17.pth, rkmy
BLEU = 70.70, 85.9/75.5/66.0/58.3 (BP=1.000, ratio=1.053, hyp_len=24763, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.134.0.08-1.08.0.08-1.08.0.87-2.38.0.77-2.16.pth, myrk
BLEU = 70.74, 86.2/75.5/66.2/58.2 (BP=1.000, ratio=1.045, hyp_len=24191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.134.0.08-1.08.0.08-1.08.0.87-2.38.0.77-2.16.pth, rkmy
BLEU = 70.61, 85.8/75.4/65.9/58.3 (BP=1.000, ratio=1.054, hyp_len=24780, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.135.0.07-1.08.0.07-1.08.0.88-2.42.0.77-2.16.pth, myrk
BLEU = 69.72, 85.6/74.5/65.1/56.9 (BP=1.000, ratio=1.050, hyp_len=24309, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.135.0.07-1.08.0.07-1.08.0.88-2.42.0.77-2.16.pth, rkmy
BLEU = 71.09, 86.0/75.6/66.4/59.1 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.136.0.08-1.08.0.07-1.08.0.87-2.39.0.75-2.12.pth, myrk
BLEU = 69.79, 85.4/74.5/65.2/57.1 (BP=1.000, ratio=1.051, hyp_len=24339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.136.0.08-1.08.0.07-1.08.0.87-2.39.0.75-2.12.pth, rkmy
BLEU = 70.62, 85.6/75.3/66.0/58.4 (BP=1.000, ratio=1.054, hyp_len=24768, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.137.0.07-1.08.0.08-1.08.0.88-2.42.0.73-2.09.pth, myrk
BLEU = 69.34, 84.9/74.0/64.8/56.8 (BP=1.000, ratio=1.056, hyp_len=24462, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.137.0.07-1.08.0.08-1.08.0.88-2.42.0.73-2.09.pth, rkmy
BLEU = 70.79, 86.0/75.6/66.1/58.4 (BP=1.000, ratio=1.054, hyp_len=24773, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.138.0.07-1.08.0.07-1.08.0.89-2.42.0.75-2.11.pth, myrk
BLEU = 70.46, 85.9/75.1/65.9/57.9 (BP=1.000, ratio=1.048, hyp_len=24274, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.138.0.07-1.08.0.07-1.08.0.89-2.42.0.75-2.11.pth, rkmy
BLEU = 69.86, 85.3/74.7/65.2/57.3 (BP=1.000, ratio=1.060, hyp_len=24915, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.139.0.07-1.08.0.07-1.08.0.87-2.39.0.76-2.13.pth, myrk
BLEU = 69.87, 85.6/74.6/65.2/57.2 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.139.0.07-1.08.0.07-1.08.0.87-2.39.0.76-2.13.pth, rkmy
BLEU = 71.11, 86.1/75.7/66.5/58.9 (BP=1.000, ratio=1.052, hyp_len=24726, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.140.0.07-1.08.0.07-1.08.0.85-2.35.0.76-2.15.pth, myrk
BLEU = 70.67, 86.0/75.3/66.1/58.3 (BP=1.000, ratio=1.044, hyp_len=24176, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.140.0.07-1.08.0.07-1.08.0.85-2.35.0.76-2.15.pth, rkmy
BLEU = 71.12, 86.1/75.8/66.5/59.0 (BP=1.000, ratio=1.050, hyp_len=24679, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.49-1.63.0.48-1.61.0.69-1.99.0.64-1.89.pth, myrk
BLEU = 65.35, 82.8/70.9/60.5/51.4 (BP=1.000, ratio=1.067, hyp_len=24709, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.49-1.63.0.48-1.61.0.69-1.99.0.64-1.89.pth, rkmy
BLEU = 62.98, 80.3/68.9/58.1/49.0 (BP=1.000, ratio=1.103, hyp_len=25934, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.141.0.07-1.08.0.07-1.08.0.88-2.42.0.76-2.14.pth, myrk
BLEU = 70.13, 85.8/74.9/65.5/57.5 (BP=1.000, ratio=1.048, hyp_len=24268, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.141.0.07-1.08.0.07-1.08.0.88-2.42.0.76-2.14.pth, rkmy
BLEU = 71.11, 86.2/75.8/66.5/58.9 (BP=1.000, ratio=1.052, hyp_len=24731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.142.0.07-1.08.0.08-1.08.0.87-2.39.0.75-2.12.pth, myrk
BLEU = 70.91, 86.2/75.4/66.3/58.7 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.142.0.07-1.08.0.08-1.08.0.87-2.39.0.75-2.12.pth, rkmy
BLEU = 70.49, 85.6/75.3/65.9/58.1 (BP=1.000, ratio=1.056, hyp_len=24821, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.143.0.07-1.07.0.07-1.07.0.89-2.43.0.77-2.15.pth, myrk
BLEU = 69.71, 85.2/74.4/65.2/57.2 (BP=1.000, ratio=1.053, hyp_len=24376, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.143.0.07-1.07.0.07-1.07.0.89-2.43.0.77-2.15.pth, rkmy
BLEU = 70.99, 85.9/75.7/66.4/58.8 (BP=1.000, ratio=1.053, hyp_len=24761, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.144.0.07-1.07.0.07-1.07.0.91-2.48.0.74-2.10.pth, myrk
BLEU = 70.95, 86.1/75.4/66.5/58.7 (BP=1.000, ratio=1.043, hyp_len=24156, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.144.0.07-1.07.0.07-1.07.0.91-2.48.0.74-2.10.pth, rkmy
BLEU = 70.89, 85.8/75.5/66.3/58.8 (BP=1.000, ratio=1.055, hyp_len=24795, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.145.0.07-1.07.0.07-1.07.0.88-2.40.0.77-2.15.pth, myrk
BLEU = 69.23, 85.2/74.0/64.6/56.4 (BP=1.000, ratio=1.051, hyp_len=24342, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.145.0.07-1.07.0.07-1.07.0.88-2.40.0.77-2.15.pth, rkmy
BLEU = 71.55, 86.3/76.1/67.0/59.6 (BP=1.000, ratio=1.051, hyp_len=24714, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.146.0.07-1.08.0.07-1.08.0.88-2.41.0.79-2.21.pth, myrk
BLEU = 70.20, 85.9/74.9/65.6/57.5 (BP=1.000, ratio=1.044, hyp_len=24186, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.146.0.07-1.08.0.07-1.08.0.88-2.41.0.79-2.21.pth, rkmy
BLEU = 70.09, 85.4/74.9/65.4/57.7 (BP=1.000, ratio=1.060, hyp_len=24909, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.147.0.07-1.07.0.07-1.07.0.90-2.46.0.78-2.17.pth, myrk
BLEU = 70.51, 86.3/75.3/65.9/57.8 (BP=1.000, ratio=1.042, hyp_len=24127, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.147.0.07-1.07.0.07-1.07.0.90-2.46.0.78-2.17.pth, rkmy
BLEU = 71.83, 86.4/76.2/67.3/60.0 (BP=1.000, ratio=1.049, hyp_len=24656, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.148.0.07-1.07.0.07-1.07.0.89-2.45.0.78-2.18.pth, myrk
BLEU = 69.31, 85.2/74.0/64.7/56.6 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.148.0.07-1.07.0.07-1.07.0.89-2.45.0.78-2.18.pth, rkmy
BLEU = 70.45, 85.4/75.2/65.8/58.2 (BP=1.000, ratio=1.060, hyp_len=24929, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.149.0.07-1.07.0.07-1.07.0.89-2.43.0.77-2.16.pth, myrk
BLEU = 70.09, 85.8/74.8/65.5/57.4 (BP=1.000, ratio=1.045, hyp_len=24198, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.149.0.07-1.07.0.07-1.07.0.89-2.43.0.77-2.16.pth, rkmy
BLEU = 70.79, 85.9/75.5/66.2/58.5 (BP=1.000, ratio=1.056, hyp_len=24831, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.150.0.07-1.08.0.07-1.08.0.91-2.49.0.76-2.13.pth, myrk
BLEU = 70.12, 85.8/74.7/65.5/57.5 (BP=1.000, ratio=1.048, hyp_len=24273, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.150.0.07-1.08.0.07-1.08.0.91-2.49.0.76-2.13.pth, rkmy
BLEU = 71.60, 86.3/76.3/67.1/59.4 (BP=1.000, ratio=1.049, hyp_len=24660, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.43-1.54.0.42-1.52.0.69-2.00.0.59-1.81.pth, myrk
BLEU = 67.21, 84.7/72.5/62.2/53.4 (BP=1.000, ratio=1.041, hyp_len=24111, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.43-1.54.0.42-1.52.0.69-2.00.0.59-1.81.pth, rkmy
BLEU = 68.05, 84.9/73.4/63.1/54.5 (BP=1.000, ratio=1.037, hyp_len=24375, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.151.0.07-1.07.0.07-1.07.0.88-2.42.0.76-2.14.pth, myrk
BLEU = 69.68, 85.5/74.4/65.1/57.0 (BP=1.000, ratio=1.047, hyp_len=24247, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.151.0.07-1.07.0.07-1.07.0.88-2.42.0.76-2.14.pth, rkmy
BLEU = 70.92, 85.9/75.6/66.3/58.7 (BP=1.000, ratio=1.054, hyp_len=24784, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.152.0.07-1.07.0.07-1.07.0.89-2.45.0.75-2.12.pth, myrk
BLEU = 69.11, 85.2/73.9/64.4/56.3 (BP=1.000, ratio=1.053, hyp_len=24386, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.152.0.07-1.07.0.07-1.07.0.89-2.45.0.75-2.12.pth, rkmy
BLEU = 71.35, 86.1/76.0/66.8/59.3 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.153.0.07-1.07.0.07-1.07.0.89-2.44.0.76-2.14.pth, myrk
BLEU = 69.09, 85.6/74.1/64.3/55.8 (BP=1.000, ratio=1.051, hyp_len=24338, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.153.0.07-1.07.0.07-1.07.0.89-2.44.0.76-2.14.pth, rkmy
BLEU = 70.71, 86.0/75.6/66.0/58.2 (BP=1.000, ratio=1.053, hyp_len=24757, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.154.0.07-1.08.0.07-1.07.0.90-2.47.0.77-2.17.pth, myrk
BLEU = 69.37, 85.3/74.1/64.7/56.6 (BP=1.000, ratio=1.054, hyp_len=24401, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.154.0.07-1.08.0.07-1.07.0.90-2.47.0.77-2.17.pth, rkmy
BLEU = 71.22, 86.0/75.9/66.6/59.2 (BP=1.000, ratio=1.054, hyp_len=24773, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.155.0.07-1.07.0.07-1.07.0.88-2.42.0.77-2.16.pth, myrk
BLEU = 69.82, 85.7/74.6/65.2/57.0 (BP=1.000, ratio=1.048, hyp_len=24278, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.155.0.07-1.07.0.07-1.07.0.88-2.42.0.77-2.16.pth, rkmy
BLEU = 71.39, 86.3/76.0/66.8/59.3 (BP=1.000, ratio=1.050, hyp_len=24679, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.156.0.07-1.07.0.07-1.07.0.91-2.49.0.77-2.15.pth, myrk
BLEU = 69.91, 85.6/74.6/65.3/57.3 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.156.0.07-1.07.0.07-1.07.0.91-2.49.0.77-2.15.pth, rkmy
BLEU = 70.01, 85.3/74.9/65.3/57.5 (BP=1.000, ratio=1.059, hyp_len=24889, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.157.0.07-1.07.0.07-1.07.0.91-2.49.0.76-2.14.pth, myrk
BLEU = 69.28, 85.2/74.1/64.7/56.4 (BP=1.000, ratio=1.053, hyp_len=24390, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.157.0.07-1.07.0.07-1.07.0.91-2.49.0.76-2.14.pth, rkmy
BLEU = 71.25, 86.0/75.9/66.7/59.2 (BP=1.000, ratio=1.050, hyp_len=24689, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.158.0.07-1.07.0.07-1.07.0.89-2.44.0.75-2.11.pth, myrk
BLEU = 69.68, 85.3/74.4/65.1/57.1 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.158.0.07-1.07.0.07-1.07.0.89-2.44.0.75-2.11.pth, rkmy
BLEU = 70.92, 85.9/75.5/66.3/58.8 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.159.0.07-1.07.0.07-1.07.0.90-2.45.0.77-2.17.pth, myrk
BLEU = 69.75, 85.6/74.5/65.1/57.0 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.159.0.07-1.07.0.07-1.07.0.90-2.45.0.77-2.17.pth, rkmy
BLEU = 71.05, 86.1/75.8/66.5/58.8 (BP=1.000, ratio=1.051, hyp_len=24715, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.160.0.07-1.07.0.07-1.07.0.89-2.44.0.77-2.16.pth, myrk
BLEU = 70.18, 85.7/74.8/65.6/57.6 (BP=1.000, ratio=1.046, hyp_len=24235, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.160.0.07-1.07.0.07-1.07.0.89-2.44.0.77-2.16.pth, rkmy
BLEU = 70.21, 85.5/75.0/65.5/57.8 (BP=1.000, ratio=1.056, hyp_len=24830, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.45-1.56.0.43-1.54.0.68-1.98.0.58-1.79.pth, myrk
BLEU = 67.13, 84.1/72.5/62.3/53.5 (BP=1.000, ratio=1.056, hyp_len=24465, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.45-1.56.0.43-1.54.0.68-1.98.0.58-1.79.pth, rkmy
BLEU = 67.23, 84.1/72.7/62.2/53.7 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.161.0.06-1.07.0.06-1.07.0.90-2.47.0.78-2.18.pth, myrk
BLEU = 71.03, 86.5/75.7/66.5/58.5 (BP=1.000, ratio=1.041, hyp_len=24105, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.161.0.06-1.07.0.06-1.07.0.90-2.47.0.78-2.18.pth, rkmy
BLEU = 70.61, 85.9/75.4/65.9/58.2 (BP=1.000, ratio=1.055, hyp_len=24796, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.162.0.07-1.07.0.07-1.07.0.92-2.51.0.79-2.21.pth, myrk
BLEU = 69.94, 85.4/74.6/65.4/57.4 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.162.0.07-1.07.0.07-1.07.0.92-2.51.0.79-2.21.pth, rkmy
BLEU = 70.60, 85.5/75.3/66.0/58.5 (BP=1.000, ratio=1.057, hyp_len=24842, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.163.0.07-1.07.0.07-1.07.0.91-2.50.0.78-2.19.pth, myrk
BLEU = 68.65, 84.9/73.6/63.9/55.6 (BP=1.000, ratio=1.055, hyp_len=24442, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.163.0.07-1.07.0.07-1.07.0.91-2.50.0.78-2.19.pth, rkmy
BLEU = 70.94, 85.9/75.6/66.3/58.8 (BP=1.000, ratio=1.050, hyp_len=24693, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.164.0.06-1.07.0.07-1.07.0.90-2.45.0.79-2.21.pth, myrk
BLEU = 70.05, 85.7/74.8/65.5/57.3 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.164.0.06-1.07.0.07-1.07.0.90-2.45.0.79-2.21.pth, rkmy
BLEU = 71.19, 86.2/76.0/66.6/58.9 (BP=1.000, ratio=1.052, hyp_len=24734, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.165.0.07-1.07.0.07-1.07.0.92-2.52.0.81-2.24.pth, myrk
BLEU = 70.24, 85.8/74.9/65.7/57.7 (BP=1.000, ratio=1.050, hyp_len=24328, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.165.0.07-1.07.0.07-1.07.0.92-2.52.0.81-2.24.pth, rkmy
BLEU = 71.17, 86.1/75.8/66.6/59.0 (BP=1.000, ratio=1.056, hyp_len=24817, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.166.0.06-1.07.0.06-1.06.0.91-2.48.0.79-2.20.pth, myrk
BLEU = 70.62, 86.3/75.3/66.0/57.9 (BP=1.000, ratio=1.043, hyp_len=24164, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.166.0.06-1.07.0.06-1.06.0.91-2.48.0.79-2.20.pth, rkmy
BLEU = 70.06, 85.5/74.9/65.4/57.5 (BP=1.000, ratio=1.060, hyp_len=24921, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.167.0.06-1.07.0.06-1.07.0.90-2.46.0.79-2.21.pth, myrk
BLEU = 69.18, 85.4/74.2/64.5/56.1 (BP=1.000, ratio=1.052, hyp_len=24363, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.167.0.06-1.07.0.06-1.07.0.90-2.46.0.79-2.21.pth, rkmy
BLEU = 71.91, 86.4/76.4/67.3/60.2 (BP=1.000, ratio=1.050, hyp_len=24694, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.168.0.06-1.06.0.06-1.06.0.91-2.48.0.80-2.22.pth, myrk
BLEU = 69.48, 85.4/74.4/64.9/56.6 (BP=1.000, ratio=1.051, hyp_len=24346, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.168.0.06-1.06.0.06-1.06.0.91-2.48.0.80-2.22.pth, rkmy
BLEU = 70.34, 85.4/75.1/65.7/58.0 (BP=1.000, ratio=1.060, hyp_len=24923, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.169.0.06-1.06.0.06-1.07.0.91-2.50.0.80-2.24.pth, myrk
BLEU = 69.65, 85.7/74.5/64.9/56.8 (BP=1.000, ratio=1.051, hyp_len=24331, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.169.0.06-1.06.0.06-1.07.0.91-2.50.0.80-2.24.pth, rkmy
BLEU = 72.15, 86.7/76.7/67.7/60.2 (BP=1.000, ratio=1.046, hyp_len=24581, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.170.0.06-1.07.0.06-1.07.0.90-2.46.0.82-2.27.pth, myrk
BLEU = 69.88, 85.6/74.6/65.3/57.2 (BP=1.000, ratio=1.047, hyp_len=24246, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.170.0.06-1.07.0.06-1.07.0.90-2.46.0.82-2.27.pth, rkmy
BLEU = 71.08, 85.9/75.7/66.6/59.0 (BP=1.000, ratio=1.057, hyp_len=24856, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.40-1.49.0.66-1.93.0.62-1.85.pth, myrk
BLEU = 68.20, 84.9/73.4/63.4/54.7 (BP=1.000, ratio=1.048, hyp_len=24268, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.40-1.49.0.66-1.93.0.62-1.85.pth, rkmy
BLEU = 64.95, 81.3/70.3/60.2/51.7 (BP=1.000, ratio=1.094, hyp_len=25718, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.171.0.06-1.06.0.06-1.06.0.89-2.44.0.80-2.22.pth, myrk
BLEU = 70.07, 85.9/74.9/65.4/57.3 (BP=1.000, ratio=1.046, hyp_len=24217, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.171.0.06-1.06.0.06-1.06.0.89-2.44.0.80-2.22.pth, rkmy
BLEU = 71.96, 86.4/76.5/67.5/60.0 (BP=1.000, ratio=1.048, hyp_len=24626, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.172.0.06-1.07.0.06-1.07.0.91-2.48.0.78-2.17.pth, myrk
BLEU = 70.56, 85.8/75.0/66.0/58.4 (BP=1.000, ratio=1.049, hyp_len=24288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.172.0.06-1.07.0.06-1.07.0.91-2.48.0.78-2.17.pth, rkmy
BLEU = 70.97, 85.8/75.6/66.4/58.8 (BP=1.000, ratio=1.056, hyp_len=24814, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.173.0.06-1.07.0.07-1.07.0.89-2.42.0.78-2.18.pth, myrk
BLEU = 70.30, 86.0/75.0/65.7/57.6 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.173.0.06-1.07.0.07-1.07.0.89-2.42.0.78-2.18.pth, rkmy
BLEU = 70.65, 85.8/75.5/66.0/58.3 (BP=1.000, ratio=1.057, hyp_len=24859, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.174.0.06-1.06.0.06-1.07.0.90-2.46.0.81-2.26.pth, myrk
BLEU = 69.18, 85.1/74.0/64.5/56.4 (BP=1.000, ratio=1.056, hyp_len=24455, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.174.0.06-1.06.0.06-1.07.0.90-2.46.0.81-2.26.pth, rkmy
BLEU = 71.01, 85.9/75.7/66.5/58.8 (BP=1.000, ratio=1.054, hyp_len=24768, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.175.0.06-1.06.0.06-1.06.0.92-2.51.0.79-2.21.pth, myrk
BLEU = 70.11, 85.5/74.7/65.5/57.8 (BP=1.000, ratio=1.050, hyp_len=24323, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.175.0.06-1.06.0.06-1.06.0.92-2.51.0.79-2.21.pth, rkmy
BLEU = 71.80, 86.3/76.2/67.3/60.0 (BP=1.000, ratio=1.050, hyp_len=24681, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.176.0.06-1.07.0.06-1.07.0.93-2.54.0.83-2.29.pth, myrk
BLEU = 69.34, 85.3/74.2/64.7/56.4 (BP=1.000, ratio=1.050, hyp_len=24327, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.176.0.06-1.07.0.06-1.07.0.93-2.54.0.83-2.29.pth, rkmy
BLEU = 70.88, 86.1/75.8/66.3/58.4 (BP=1.000, ratio=1.055, hyp_len=24807, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.177.0.06-1.06.0.06-1.07.0.90-2.47.0.82-2.27.pth, myrk
BLEU = 70.06, 85.9/74.8/65.4/57.3 (BP=1.000, ratio=1.043, hyp_len=24148, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.177.0.06-1.06.0.06-1.07.0.90-2.47.0.82-2.27.pth, rkmy
BLEU = 70.00, 85.1/74.9/65.5/57.5 (BP=1.000, ratio=1.063, hyp_len=25001, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.178.0.06-1.06.0.06-1.06.0.91-2.47.0.82-2.27.pth, myrk
BLEU = 69.84, 85.4/74.6/65.3/57.1 (BP=1.000, ratio=1.049, hyp_len=24288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.178.0.06-1.06.0.06-1.06.0.91-2.47.0.82-2.27.pth, rkmy
BLEU = 70.86, 85.9/75.7/66.3/58.4 (BP=1.000, ratio=1.056, hyp_len=24815, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.179.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.25.pth, myrk
BLEU = 69.18, 85.2/74.0/64.5/56.3 (BP=1.000, ratio=1.056, hyp_len=24465, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.179.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.25.pth, rkmy
BLEU = 72.17, 86.6/76.7/67.7/60.3 (BP=1.000, ratio=1.049, hyp_len=24670, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.180.0.06-1.07.0.06-1.07.0.93-2.52.0.82-2.27.pth, myrk
BLEU = 69.34, 85.4/74.2/64.7/56.3 (BP=1.000, ratio=1.051, hyp_len=24342, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.180.0.06-1.07.0.06-1.07.0.93-2.52.0.82-2.27.pth, rkmy
BLEU = 71.63, 86.1/76.2/67.2/59.7 (BP=1.000, ratio=1.049, hyp_len=24650, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.37-1.45.0.67-1.96.0.63-1.89.pth, myrk
BLEU = 69.33, 86.0/74.4/64.4/56.1 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.37-1.45.0.67-1.96.0.63-1.89.pth, rkmy
BLEU = 70.12, 86.1/75.2/65.3/57.2 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.181.0.06-1.06.0.06-1.06.0.92-2.52.0.82-2.27.pth, myrk
BLEU = 69.43, 85.6/74.4/64.8/56.4 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.181.0.06-1.06.0.06-1.06.0.92-2.52.0.82-2.27.pth, rkmy
BLEU = 71.85, 86.4/76.4/67.3/60.0 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.182.0.07-1.07.0.06-1.06.0.90-2.47.0.83-2.29.pth, myrk
BLEU = 70.12, 85.6/74.8/65.6/57.6 (BP=1.000, ratio=1.050, hyp_len=24309, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.182.0.07-1.07.0.06-1.06.0.90-2.47.0.83-2.29.pth, rkmy
BLEU = 71.84, 86.5/76.5/67.4/59.8 (BP=1.000, ratio=1.048, hyp_len=24637, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.183.0.06-1.06.0.06-1.06.0.92-2.52.0.81-2.26.pth, myrk
BLEU = 69.81, 85.8/74.5/65.1/57.1 (BP=1.000, ratio=1.048, hyp_len=24283, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.183.0.06-1.06.0.06-1.06.0.92-2.52.0.81-2.26.pth, rkmy
BLEU = 70.59, 85.8/75.3/65.9/58.3 (BP=1.000, ratio=1.056, hyp_len=24837, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.184.0.06-1.06.0.06-1.06.0.92-2.52.0.78-2.19.pth, myrk
BLEU = 68.83, 84.9/73.6/64.2/56.0 (BP=1.000, ratio=1.054, hyp_len=24412, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.184.0.06-1.06.0.06-1.06.0.92-2.52.0.78-2.19.pth, rkmy
BLEU = 71.25, 85.9/75.9/66.8/59.2 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.185.0.06-1.06.0.06-1.06.0.91-2.48.0.83-2.29.pth, myrk
BLEU = 69.17, 85.6/74.2/64.4/55.9 (BP=1.000, ratio=1.049, hyp_len=24301, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.185.0.06-1.06.0.06-1.06.0.91-2.48.0.83-2.29.pth, rkmy
BLEU = 70.35, 85.5/75.2/65.8/57.9 (BP=1.000, ratio=1.061, hyp_len=24946, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.186.0.06-1.06.0.06-1.06.0.90-2.45.0.81-2.25.pth, myrk
BLEU = 69.42, 85.5/74.2/64.7/56.6 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.186.0.06-1.06.0.06-1.06.0.90-2.45.0.81-2.25.pth, rkmy
BLEU = 71.30, 86.1/75.9/66.8/59.2 (BP=1.000, ratio=1.052, hyp_len=24721, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.187.0.06-1.06.0.06-1.06.0.93-2.52.0.83-2.30.pth, myrk
BLEU = 69.89, 85.6/74.6/65.3/57.2 (BP=1.000, ratio=1.050, hyp_len=24321, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.187.0.06-1.06.0.06-1.06.0.93-2.52.0.83-2.30.pth, rkmy
BLEU = 70.16, 85.4/75.1/65.7/57.6 (BP=1.000, ratio=1.061, hyp_len=24944, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.188.0.06-1.06.0.06-1.06.0.92-2.52.0.80-2.22.pth, myrk
BLEU = 70.85, 86.3/75.5/66.3/58.3 (BP=1.000, ratio=1.044, hyp_len=24175, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.188.0.06-1.06.0.06-1.06.0.92-2.52.0.80-2.22.pth, rkmy
BLEU = 71.40, 86.0/76.0/67.0/59.4 (BP=1.000, ratio=1.055, hyp_len=24801, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.189.0.06-1.06.0.06-1.06.0.94-2.57.0.80-2.22.pth, myrk
BLEU = 69.79, 85.2/74.5/65.2/57.3 (BP=1.000, ratio=1.053, hyp_len=24387, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.189.0.06-1.06.0.06-1.06.0.94-2.57.0.80-2.22.pth, rkmy
BLEU = 71.44, 86.0/76.1/67.0/59.4 (BP=1.000, ratio=1.056, hyp_len=24815, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.190.0.06-1.06.0.06-1.06.0.91-2.49.0.79-2.20.pth, myrk
BLEU = 70.15, 85.7/74.9/65.6/57.5 (BP=1.000, ratio=1.048, hyp_len=24282, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.190.0.06-1.06.0.06-1.06.0.91-2.49.0.79-2.20.pth, rkmy
BLEU = 71.41, 86.1/76.0/66.9/59.3 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.38-1.46.0.36-1.43.0.66-1.94.0.60-1.83.pth, myrk
BLEU = 66.59, 83.6/71.8/61.8/53.0 (BP=1.000, ratio=1.063, hyp_len=24615, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.38-1.46.0.36-1.43.0.66-1.94.0.60-1.83.pth, rkmy
BLEU = 60.16, 76.0/65.2/55.6/47.5 (BP=1.000, ratio=1.174, hyp_len=27590, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.191.0.06-1.06.0.06-1.06.0.93-2.53.0.80-2.24.pth, myrk
BLEU = 70.07, 85.9/74.8/65.4/57.3 (BP=1.000, ratio=1.044, hyp_len=24168, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.191.0.06-1.06.0.06-1.06.0.93-2.53.0.80-2.24.pth, rkmy
BLEU = 71.05, 86.0/75.7/66.5/58.9 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.192.0.06-1.06.0.06-1.06.0.91-2.48.0.81-2.25.pth, myrk
BLEU = 69.86, 85.7/74.6/65.3/57.1 (BP=1.000, ratio=1.051, hyp_len=24338, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.192.0.06-1.06.0.06-1.06.0.91-2.48.0.81-2.25.pth, rkmy
BLEU = 71.72, 86.2/76.3/67.3/59.8 (BP=1.000, ratio=1.050, hyp_len=24692, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.193.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.24.pth, myrk
BLEU = 69.80, 85.8/74.7/65.2/56.8 (BP=1.000, ratio=1.049, hyp_len=24291, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.193.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.24.pth, rkmy
BLEU = 71.31, 86.1/76.0/66.8/59.2 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.194.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.26.pth, myrk
BLEU = 70.03, 85.9/74.9/65.4/57.2 (BP=1.000, ratio=1.048, hyp_len=24272, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.194.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.26.pth, rkmy
BLEU = 71.48, 86.5/76.2/66.9/59.2 (BP=1.000, ratio=1.051, hyp_len=24708, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.195.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.25.pth, myrk
BLEU = 69.89, 85.8/74.7/65.3/57.1 (BP=1.000, ratio=1.049, hyp_len=24285, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.195.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.25.pth, rkmy
BLEU = 72.09, 86.6/76.6/67.6/60.2 (BP=1.000, ratio=1.049, hyp_len=24662, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.196.0.06-1.06.0.06-1.06.0.90-2.47.0.83-2.28.pth, myrk
BLEU = 70.72, 86.2/75.4/66.2/58.2 (BP=1.000, ratio=1.045, hyp_len=24211, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.196.0.06-1.06.0.06-1.06.0.90-2.47.0.83-2.28.pth, rkmy
BLEU = 70.78, 85.7/75.6/66.3/58.5 (BP=1.000, ratio=1.059, hyp_len=24903, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.197.0.06-1.06.0.06-1.06.0.91-2.48.0.82-2.27.pth, myrk
BLEU = 70.71, 86.1/75.4/66.2/58.2 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.197.0.06-1.06.0.06-1.06.0.91-2.48.0.82-2.27.pth, rkmy
BLEU = 71.24, 85.9/75.8/66.7/59.3 (BP=1.000, ratio=1.057, hyp_len=24850, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.198.0.06-1.06.0.06-1.06.0.91-2.50.0.83-2.29.pth, myrk
BLEU = 70.59, 86.0/75.2/66.1/58.1 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.198.0.06-1.06.0.06-1.06.0.91-2.50.0.83-2.29.pth, rkmy
BLEU = 71.00, 86.0/75.8/66.4/58.7 (BP=1.000, ratio=1.054, hyp_len=24771, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.199.0.06-1.06.0.06-1.06.0.91-2.48.0.82-2.28.pth, myrk
BLEU = 70.36, 85.6/75.0/65.9/57.9 (BP=1.000, ratio=1.050, hyp_len=24316, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.199.0.06-1.06.0.06-1.06.0.91-2.48.0.82-2.28.pth, rkmy
BLEU = 71.38, 86.0/76.0/67.0/59.3 (BP=1.000, ratio=1.055, hyp_len=24809, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.200.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.25.pth, myrk
BLEU = 70.49, 85.9/75.2/66.0/57.9 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.200.0.06-1.06.0.06-1.06.0.93-2.54.0.81-2.25.pth, rkmy
BLEU = 71.47, 86.2/76.1/67.0/59.4 (BP=1.000, ratio=1.053, hyp_len=24766, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.33-1.39.0.32-1.38.0.69-1.99.0.61-1.85.pth, myrk
BLEU = 70.79, 86.8/75.7/66.1/57.8 (BP=1.000, ratio=1.020, hyp_len=23618, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.33-1.39.0.32-1.38.0.69-1.99.0.61-1.85.pth, rkmy
BLEU = 67.35, 83.8/72.9/62.5/53.9 (BP=1.000, ratio=1.063, hyp_len=25000, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.201.0.06-1.06.0.06-1.06.0.91-2.50.0.80-2.23.pth, myrk
BLEU = 70.04, 85.8/74.9/65.5/57.2 (BP=1.000, ratio=1.046, hyp_len=24217, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.201.0.06-1.06.0.06-1.06.0.91-2.50.0.80-2.23.pth, rkmy
BLEU = 71.19, 86.2/76.0/66.6/58.8 (BP=1.000, ratio=1.053, hyp_len=24744, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.202.0.06-1.06.0.06-1.06.0.90-2.47.0.85-2.33.pth, myrk
BLEU = 69.37, 85.5/74.3/64.7/56.4 (BP=1.000, ratio=1.051, hyp_len=24339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.202.0.06-1.06.0.06-1.06.0.90-2.47.0.85-2.33.pth, rkmy
BLEU = 70.96, 86.1/75.8/66.4/58.5 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.203.0.06-1.06.0.06-1.06.0.92-2.50.0.82-2.27.pth, myrk
BLEU = 70.41, 86.0/75.1/65.8/57.7 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.203.0.06-1.06.0.06-1.06.0.92-2.50.0.82-2.27.pth, rkmy
BLEU = 70.95, 85.8/75.8/66.4/58.7 (BP=1.000, ratio=1.058, hyp_len=24869, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.204.0.06-1.06.0.06-1.06.0.93-2.54.0.80-2.23.pth, myrk
BLEU = 70.18, 85.8/74.9/65.6/57.5 (BP=1.000, ratio=1.049, hyp_len=24292, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.204.0.06-1.06.0.06-1.06.0.93-2.54.0.80-2.23.pth, rkmy
BLEU = 71.55, 86.1/76.1/67.1/59.6 (BP=1.000, ratio=1.056, hyp_len=24816, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.205.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.26.pth, myrk
BLEU = 70.13, 85.7/74.7/65.6/57.6 (BP=1.000, ratio=1.044, hyp_len=24190, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.205.0.06-1.06.0.06-1.06.0.93-2.55.0.81-2.26.pth, rkmy
BLEU = 71.73, 86.1/76.2/67.3/59.9 (BP=1.000, ratio=1.055, hyp_len=24794, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.206.0.06-1.06.0.06-1.06.0.94-2.57.0.82-2.27.pth, myrk
BLEU = 69.60, 85.7/74.5/64.9/56.6 (BP=1.000, ratio=1.049, hyp_len=24306, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.206.0.06-1.06.0.06-1.06.0.94-2.57.0.82-2.27.pth, rkmy
BLEU = 71.07, 85.8/75.6/66.6/59.0 (BP=1.000, ratio=1.056, hyp_len=24831, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.207.0.06-1.06.0.06-1.06.0.93-2.53.0.81-2.25.pth, myrk
BLEU = 70.11, 86.0/74.9/65.4/57.3 (BP=1.000, ratio=1.046, hyp_len=24228, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.207.0.06-1.06.0.06-1.06.0.93-2.53.0.81-2.25.pth, rkmy
BLEU = 71.59, 86.1/76.2/67.2/59.6 (BP=1.000, ratio=1.053, hyp_len=24766, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.208.0.06-1.06.0.05-1.06.0.92-2.51.0.80-2.22.pth, myrk
BLEU = 69.82, 85.7/74.6/65.1/57.1 (BP=1.000, ratio=1.049, hyp_len=24287, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.208.0.06-1.06.0.05-1.06.0.92-2.51.0.80-2.22.pth, rkmy
BLEU = 71.25, 85.9/75.8/66.7/59.3 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.209.0.06-1.06.0.06-1.06.0.90-2.47.0.82-2.26.pth, myrk
BLEU = 69.46, 85.5/74.3/64.8/56.5 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.209.0.06-1.06.0.06-1.06.0.90-2.47.0.82-2.26.pth, rkmy
BLEU = 70.47, 85.5/75.2/65.9/58.2 (BP=1.000, ratio=1.059, hyp_len=24889, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.210.0.06-1.06.0.06-1.06.0.93-2.53.0.84-2.31.pth, myrk
BLEU = 70.89, 86.5/75.6/66.3/58.3 (BP=1.000, ratio=1.039, hyp_len=24062, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.210.0.06-1.06.0.06-1.06.0.93-2.53.0.84-2.31.pth, rkmy
BLEU = 71.92, 86.6/76.6/67.4/59.8 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.36-1.43.0.38-1.47.0.66-1.93.0.60-1.83.pth, myrk
BLEU = 69.24, 85.6/74.4/64.5/56.0 (BP=1.000, ratio=1.043, hyp_len=24157, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.36-1.43.0.38-1.47.0.66-1.93.0.60-1.83.pth, rkmy
BLEU = 67.03, 84.0/72.5/62.0/53.4 (BP=1.000, ratio=1.053, hyp_len=24762, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.211.0.05-1.05.0.06-1.06.0.92-2.51.0.81-2.25.pth, myrk
BLEU = 70.16, 85.8/74.8/65.5/57.6 (BP=1.000, ratio=1.048, hyp_len=24262, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.211.0.05-1.05.0.06-1.06.0.92-2.51.0.81-2.25.pth, rkmy
BLEU = 71.24, 85.8/75.9/66.7/59.3 (BP=1.000, ratio=1.057, hyp_len=24849, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.212.0.06-1.06.0.06-1.06.0.92-2.52.0.82-2.28.pth, myrk
BLEU = 70.89, 86.3/75.6/66.3/58.4 (BP=1.000, ratio=1.044, hyp_len=24178, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.212.0.06-1.06.0.06-1.06.0.92-2.52.0.82-2.28.pth, rkmy
BLEU = 71.35, 86.1/76.0/66.9/59.2 (BP=1.000, ratio=1.051, hyp_len=24717, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.213.0.06-1.06.0.06-1.06.0.93-2.54.0.83-2.30.pth, myrk
BLEU = 70.04, 85.8/74.8/65.4/57.3 (BP=1.000, ratio=1.047, hyp_len=24242, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.213.0.06-1.06.0.06-1.06.0.93-2.54.0.83-2.30.pth, rkmy
BLEU = 71.46, 86.3/76.1/66.9/59.3 (BP=1.000, ratio=1.053, hyp_len=24763, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.214.0.05-1.06.0.05-1.05.0.92-2.52.0.81-2.24.pth, myrk
BLEU = 70.47, 86.0/75.1/65.9/57.9 (BP=1.000, ratio=1.045, hyp_len=24194, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.214.0.05-1.06.0.05-1.05.0.92-2.52.0.81-2.24.pth, rkmy
BLEU = 71.05, 85.9/75.6/66.5/59.0 (BP=1.000, ratio=1.057, hyp_len=24845, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.215.0.05-1.06.0.05-1.06.0.91-2.48.0.81-2.25.pth, myrk
BLEU = 70.27, 86.1/75.2/65.7/57.4 (BP=1.000, ratio=1.048, hyp_len=24261, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.215.0.05-1.06.0.05-1.06.0.91-2.48.0.81-2.25.pth, rkmy
BLEU = 71.74, 86.3/76.4/67.3/59.7 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.216.0.06-1.06.0.06-1.06.0.96-2.62.0.80-2.23.pth, myrk
BLEU = 70.15, 86.0/75.0/65.6/57.3 (BP=1.000, ratio=1.047, hyp_len=24256, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.216.0.06-1.06.0.06-1.06.0.96-2.62.0.80-2.23.pth, rkmy
BLEU = 71.64, 86.4/76.4/67.2/59.4 (BP=1.000, ratio=1.052, hyp_len=24720, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.217.0.06-1.06.0.05-1.06.0.98-2.68.0.82-2.28.pth, myrk
BLEU = 69.70, 85.4/74.5/65.2/56.9 (BP=1.000, ratio=1.054, hyp_len=24419, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.217.0.06-1.06.0.05-1.06.0.98-2.68.0.82-2.28.pth, rkmy
BLEU = 70.66, 85.7/75.6/66.1/58.3 (BP=1.000, ratio=1.058, hyp_len=24863, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.218.0.05-1.06.0.06-1.06.0.94-2.56.0.78-2.17.pth, myrk
BLEU = 69.68, 85.5/74.5/65.2/56.8 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.218.0.05-1.06.0.06-1.06.0.94-2.56.0.78-2.17.pth, rkmy
BLEU = 70.98, 85.9/75.6/66.4/58.9 (BP=1.000, ratio=1.058, hyp_len=24875, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.219.0.05-1.05.0.05-1.06.0.93-2.52.0.79-2.20.pth, myrk
BLEU = 69.70, 85.6/74.6/65.1/56.8 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.219.0.05-1.05.0.05-1.06.0.93-2.52.0.79-2.20.pth, rkmy
BLEU = 70.29, 85.6/75.2/65.7/57.7 (BP=1.000, ratio=1.059, hyp_len=24899, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.220.0.06-1.06.0.05-1.06.0.94-2.55.0.80-2.22.pth, myrk
BLEU = 70.05, 85.9/74.8/65.4/57.3 (BP=1.000, ratio=1.048, hyp_len=24278, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.220.0.06-1.06.0.05-1.06.0.94-2.55.0.80-2.22.pth, rkmy
BLEU = 69.95, 85.4/74.8/65.3/57.4 (BP=1.000, ratio=1.060, hyp_len=24929, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.41.0.35-1.41.0.65-1.91.0.58-1.79.pth, myrk
BLEU = 69.12, 85.4/74.3/64.4/55.8 (BP=1.000, ratio=1.043, hyp_len=24163, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.41.0.35-1.41.0.65-1.91.0.58-1.79.pth, rkmy
BLEU = 68.47, 84.7/73.8/63.6/55.2 (BP=1.000, ratio=1.054, hyp_len=24774, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.221.0.05-1.06.0.06-1.06.0.93-2.53.0.79-2.20.pth, myrk
BLEU = 71.23, 86.2/75.7/66.8/59.1 (BP=1.000, ratio=1.045, hyp_len=24193, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.221.0.05-1.06.0.06-1.06.0.93-2.53.0.79-2.20.pth, rkmy
BLEU = 71.58, 86.2/76.0/67.1/59.7 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.222.0.05-1.05.0.05-1.06.0.96-2.60.0.78-2.19.pth, myrk
BLEU = 70.18, 85.8/74.9/65.6/57.6 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.222.0.05-1.05.0.05-1.06.0.96-2.60.0.78-2.19.pth, rkmy
BLEU = 70.15, 85.5/75.0/65.5/57.7 (BP=1.000, ratio=1.060, hyp_len=24919, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.223.0.05-1.05.0.05-1.05.0.96-2.62.0.77-2.16.pth, myrk
BLEU = 70.47, 86.0/75.0/65.9/58.0 (BP=1.000, ratio=1.046, hyp_len=24218, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.223.0.05-1.05.0.05-1.05.0.96-2.62.0.77-2.16.pth, rkmy
BLEU = 70.90, 85.8/75.6/66.4/58.7 (BP=1.000, ratio=1.057, hyp_len=24851, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.224.0.05-1.06.0.05-1.05.0.96-2.60.0.79-2.20.pth, myrk
BLEU = 70.45, 85.9/75.0/65.9/58.0 (BP=1.000, ratio=1.047, hyp_len=24247, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.224.0.05-1.06.0.05-1.05.0.96-2.60.0.79-2.20.pth, rkmy
BLEU = 71.32, 86.2/76.0/66.8/59.1 (BP=1.000, ratio=1.053, hyp_len=24746, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.225.0.05-1.06.0.06-1.06.0.98-2.67.0.80-2.23.pth, myrk
BLEU = 70.99, 86.4/75.6/66.5/58.5 (BP=1.000, ratio=1.044, hyp_len=24173, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.225.0.05-1.06.0.06-1.06.0.98-2.67.0.80-2.23.pth, rkmy
BLEU = 70.74, 85.9/75.6/66.2/58.3 (BP=1.000, ratio=1.055, hyp_len=24795, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.226.0.05-1.06.0.05-1.06.0.96-2.62.0.84-2.31.pth, myrk
BLEU = 70.69, 86.0/75.3/66.2/58.3 (BP=1.000, ratio=1.046, hyp_len=24228, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.226.0.05-1.06.0.05-1.06.0.96-2.62.0.84-2.31.pth, rkmy
BLEU = 69.84, 85.3/74.8/65.2/57.2 (BP=1.000, ratio=1.061, hyp_len=24946, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.227.0.06-1.06.0.05-1.06.0.95-2.59.0.81-2.25.pth, myrk
BLEU = 69.95, 85.7/74.6/65.3/57.3 (BP=1.000, ratio=1.054, hyp_len=24401, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.227.0.06-1.06.0.05-1.06.0.95-2.59.0.81-2.25.pth, rkmy
BLEU = 72.35, 86.7/76.8/67.9/60.5 (BP=1.000, ratio=1.046, hyp_len=24600, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.228.0.05-1.05.0.05-1.05.0.98-2.65.0.84-2.32.pth, myrk
BLEU = 70.37, 86.0/75.1/65.8/57.8 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.228.0.05-1.05.0.05-1.05.0.98-2.65.0.84-2.32.pth, rkmy
BLEU = 70.80, 85.8/75.6/66.3/58.4 (BP=1.000, ratio=1.057, hyp_len=24840, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.229.0.05-1.06.0.05-1.05.0.97-2.64.0.83-2.30.pth, myrk
BLEU = 70.39, 86.1/75.2/65.7/57.7 (BP=1.000, ratio=1.047, hyp_len=24242, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.229.0.05-1.06.0.05-1.05.0.97-2.64.0.83-2.30.pth, rkmy
BLEU = 72.43, 86.8/77.0/68.0/60.5 (BP=1.000, ratio=1.047, hyp_len=24610, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.230.0.05-1.06.0.05-1.05.0.97-2.63.0.84-2.31.pth, myrk
BLEU = 71.40, 86.5/75.9/66.9/59.1 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.230.0.05-1.06.0.05-1.05.0.97-2.63.0.84-2.31.pth, rkmy
BLEU = 70.82, 85.9/75.7/66.3/58.3 (BP=1.000, ratio=1.055, hyp_len=24792, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.32-1.38.0.65-1.92.0.62-1.85.pth, myrk
BLEU = 70.20, 86.0/75.2/65.6/57.2 (BP=1.000, ratio=1.038, hyp_len=24048, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.32-1.38.0.65-1.92.0.62-1.85.pth, rkmy
BLEU = 68.15, 84.6/73.3/63.3/55.0 (BP=1.000, ratio=1.058, hyp_len=24879, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.231.0.05-1.05.0.05-1.05.0.95-2.58.0.82-2.28.pth, myrk
BLEU = 71.01, 86.2/75.6/66.6/58.6 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.231.0.05-1.05.0.05-1.05.0.95-2.58.0.82-2.28.pth, rkmy
BLEU = 71.70, 86.3/76.3/67.2/59.7 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.232.0.05-1.05.0.05-1.05.0.93-2.54.0.81-2.25.pth, myrk
BLEU = 70.89, 86.3/75.5/66.4/58.4 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.232.0.05-1.05.0.05-1.05.0.93-2.54.0.81-2.25.pth, rkmy
BLEU = 71.46, 86.0/76.0/67.0/59.5 (BP=1.000, ratio=1.052, hyp_len=24734, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.233.0.05-1.05.0.05-1.05.0.93-2.54.0.79-2.21.pth, myrk
BLEU = 70.87, 86.2/75.5/66.3/58.5 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.233.0.05-1.05.0.05-1.05.0.93-2.54.0.79-2.21.pth, rkmy
BLEU = 71.47, 86.2/76.2/67.0/59.3 (BP=1.000, ratio=1.054, hyp_len=24771, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.234.0.05-1.05.0.05-1.05.0.94-2.55.0.84-2.32.pth, myrk
BLEU = 70.32, 85.9/75.0/65.7/57.8 (BP=1.000, ratio=1.048, hyp_len=24269, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.234.0.05-1.05.0.05-1.05.0.94-2.55.0.84-2.32.pth, rkmy
BLEU = 70.69, 85.7/75.4/66.1/58.4 (BP=1.000, ratio=1.056, hyp_len=24835, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.235.0.05-1.05.0.05-1.05.0.93-2.53.0.81-2.25.pth, myrk
BLEU = 71.12, 86.5/75.8/66.6/58.7 (BP=1.000, ratio=1.042, hyp_len=24127, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.235.0.05-1.05.0.05-1.05.0.93-2.53.0.81-2.25.pth, rkmy
BLEU = 71.73, 86.4/76.4/67.2/59.7 (BP=1.000, ratio=1.050, hyp_len=24685, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.236.0.05-1.05.0.05-1.05.0.96-2.61.0.81-2.24.pth, myrk
BLEU = 69.33, 85.3/74.2/64.7/56.4 (BP=1.000, ratio=1.055, hyp_len=24436, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.236.0.05-1.05.0.05-1.05.0.96-2.61.0.81-2.24.pth, rkmy
BLEU = 72.60, 86.8/77.0/68.2/60.9 (BP=1.000, ratio=1.048, hyp_len=24634, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.237.0.05-1.06.0.05-1.06.0.95-2.59.0.82-2.27.pth, myrk
BLEU = 69.56, 85.1/74.2/65.0/57.0 (BP=1.000, ratio=1.058, hyp_len=24504, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.237.0.05-1.06.0.05-1.06.0.95-2.59.0.82-2.27.pth, rkmy
BLEU = 71.66, 86.3/76.3/67.2/59.6 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.238.0.05-1.05.0.05-1.05.0.95-2.60.0.80-2.22.pth, myrk
BLEU = 70.80, 86.0/75.4/66.3/58.5 (BP=1.000, ratio=1.046, hyp_len=24230, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.238.0.05-1.05.0.05-1.05.0.95-2.60.0.80-2.22.pth, rkmy
BLEU = 71.47, 86.2/76.1/67.0/59.4 (BP=1.000, ratio=1.056, hyp_len=24832, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.239.0.05-1.05.0.05-1.05.0.96-2.61.0.80-2.21.pth, myrk
BLEU = 70.28, 85.8/75.0/65.7/57.7 (BP=1.000, ratio=1.047, hyp_len=24253, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.239.0.05-1.05.0.05-1.05.0.96-2.61.0.80-2.21.pth, rkmy
BLEU = 71.10, 86.0/75.9/66.6/58.8 (BP=1.000, ratio=1.054, hyp_len=24775, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.240.0.05-1.05.0.05-1.05.0.95-2.60.0.83-2.29.pth, myrk
BLEU = 69.77, 85.6/74.5/65.1/57.1 (BP=1.000, ratio=1.052, hyp_len=24360, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.240.0.05-1.05.0.05-1.05.0.95-2.60.0.83-2.29.pth, rkmy
BLEU = 71.98, 86.5/76.5/67.5/60.1 (BP=1.000, ratio=1.050, hyp_len=24677, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.31-1.36.0.64-1.89.0.60-1.83.pth, myrk
BLEU = 69.11, 85.4/74.2/64.3/56.0 (BP=1.000, ratio=1.043, hyp_len=24146, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.31-1.36.0.64-1.89.0.60-1.83.pth, rkmy
BLEU = 70.03, 85.7/74.9/65.3/57.4 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.241.0.05-1.05.0.05-1.05.0.93-2.55.0.81-2.24.pth, myrk
BLEU = 69.99, 85.7/74.8/65.4/57.2 (BP=1.000, ratio=1.050, hyp_len=24313, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.241.0.05-1.05.0.05-1.05.0.93-2.55.0.81-2.24.pth, rkmy
BLEU = 71.56, 86.2/76.3/67.1/59.4 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.242.0.05-1.05.0.05-1.05.0.95-2.60.0.84-2.31.pth, myrk
BLEU = 68.81, 84.9/73.7/64.2/55.8 (BP=1.000, ratio=1.062, hyp_len=24601, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.242.0.05-1.05.0.05-1.05.0.95-2.60.0.84-2.31.pth, rkmy
BLEU = 70.96, 85.9/75.8/66.4/58.7 (BP=1.000, ratio=1.060, hyp_len=24916, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.243.0.05-1.05.0.05-1.05.0.96-2.62.0.83-2.28.pth, myrk
BLEU = 70.59, 85.9/75.3/66.1/58.1 (BP=1.000, ratio=1.050, hyp_len=24326, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.243.0.05-1.05.0.05-1.05.0.96-2.62.0.83-2.28.pth, rkmy
BLEU = 71.95, 86.5/76.5/67.4/60.0 (BP=1.000, ratio=1.049, hyp_len=24670, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.244.0.05-1.05.0.05-1.05.0.97-2.63.0.82-2.27.pth, myrk
BLEU = 70.39, 85.9/75.1/65.9/57.7 (BP=1.000, ratio=1.047, hyp_len=24246, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.244.0.05-1.05.0.05-1.05.0.97-2.63.0.82-2.27.pth, rkmy
BLEU = 71.28, 86.1/75.9/66.8/59.1 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.245.0.05-1.05.0.05-1.05.0.94-2.56.0.84-2.32.pth, myrk
BLEU = 70.07, 85.9/74.9/65.4/57.3 (BP=1.000, ratio=1.049, hyp_len=24299, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.245.0.05-1.05.0.05-1.05.0.94-2.56.0.84-2.32.pth, rkmy
BLEU = 72.64, 86.9/77.2/68.3/60.7 (BP=1.000, ratio=1.048, hyp_len=24637, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.246.0.05-1.05.0.05-1.05.0.96-2.60.0.84-2.31.pth, myrk
BLEU = 69.78, 85.6/74.5/65.2/57.0 (BP=1.000, ratio=1.049, hyp_len=24302, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.246.0.05-1.05.0.05-1.05.0.96-2.60.0.84-2.31.pth, rkmy
BLEU = 71.36, 86.2/76.0/66.8/59.3 (BP=1.000, ratio=1.055, hyp_len=24798, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.247.0.05-1.05.0.05-1.05.0.96-2.61.0.85-2.33.pth, myrk
BLEU = 69.97, 85.7/74.8/65.4/57.2 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.247.0.05-1.05.0.05-1.05.0.96-2.61.0.85-2.33.pth, rkmy
BLEU = 71.79, 86.2/76.2/67.3/60.1 (BP=1.000, ratio=1.052, hyp_len=24739, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.248.0.05-1.05.0.05-1.05.0.96-2.60.0.82-2.27.pth, myrk
BLEU = 70.81, 86.3/75.5/66.3/58.2 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.248.0.05-1.05.0.05-1.05.0.96-2.60.0.82-2.27.pth, rkmy
BLEU = 71.42, 86.1/76.0/66.9/59.3 (BP=1.000, ratio=1.056, hyp_len=24829, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.249.0.05-1.05.0.05-1.05.0.95-2.59.0.84-2.31.pth, myrk
BLEU = 70.89, 86.3/75.5/66.3/58.4 (BP=1.000, ratio=1.045, hyp_len=24211, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.249.0.05-1.05.0.05-1.05.0.95-2.59.0.84-2.31.pth, rkmy
BLEU = 70.94, 86.1/75.8/66.4/58.5 (BP=1.000, ratio=1.054, hyp_len=24785, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.250.0.05-1.05.0.05-1.05.0.97-2.65.0.84-2.32.pth, myrk
BLEU = 70.85, 86.2/75.6/66.3/58.3 (BP=1.000, ratio=1.047, hyp_len=24251, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.250.0.05-1.05.0.05-1.05.0.97-2.65.0.84-2.32.pth, rkmy
BLEU = 71.93, 86.5/76.6/67.5/59.9 (BP=1.000, ratio=1.051, hyp_len=24705, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.31-1.36.0.31-1.36.0.65-1.91.0.60-1.82.pth, myrk
BLEU = 68.51, 85.1/73.6/63.7/55.3 (BP=1.000, ratio=1.048, hyp_len=24277, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.31-1.36.0.31-1.36.0.65-1.91.0.60-1.82.pth, rkmy
BLEU = 70.96, 86.3/75.9/66.3/58.4 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.251.0.05-1.05.0.05-1.05.0.96-2.61.0.82-2.28.pth, myrk
BLEU = 70.01, 85.8/74.7/65.4/57.3 (BP=1.000, ratio=1.051, hyp_len=24339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.251.0.05-1.05.0.05-1.05.0.96-2.61.0.82-2.28.pth, rkmy
BLEU = 71.82, 86.4/76.4/67.3/59.9 (BP=1.000, ratio=1.051, hyp_len=24705, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.252.0.05-1.05.0.05-1.05.0.97-2.63.0.82-2.26.pth, myrk
BLEU = 70.25, 86.1/75.1/65.6/57.5 (BP=1.000, ratio=1.047, hyp_len=24247, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.252.0.05-1.05.0.05-1.05.0.97-2.63.0.82-2.26.pth, rkmy
BLEU = 72.84, 87.1/77.3/68.4/61.2 (BP=1.000, ratio=1.042, hyp_len=24497, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.253.0.05-1.05.0.05-1.05.0.98-2.65.0.82-2.27.pth, myrk
BLEU = 70.59, 86.2/75.2/66.0/58.0 (BP=1.000, ratio=1.045, hyp_len=24191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.253.0.05-1.05.0.05-1.05.0.98-2.65.0.82-2.27.pth, rkmy
BLEU = 71.41, 86.1/76.1/66.9/59.3 (BP=1.000, ratio=1.056, hyp_len=24824, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.254.0.05-1.05.0.05-1.05.1.01-2.75.0.82-2.28.pth, myrk
BLEU = 69.77, 85.7/74.7/65.1/56.8 (BP=1.000, ratio=1.051, hyp_len=24345, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.254.0.05-1.05.0.05-1.05.1.01-2.75.0.82-2.28.pth, rkmy
BLEU = 70.97, 86.0/75.8/66.4/58.6 (BP=1.000, ratio=1.056, hyp_len=24831, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.255.0.05-1.05.0.05-1.05.1.00-2.72.0.82-2.27.pth, myrk
BLEU = 70.80, 86.3/75.5/66.3/58.2 (BP=1.000, ratio=1.045, hyp_len=24212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.255.0.05-1.05.0.05-1.05.1.00-2.72.0.82-2.27.pth, rkmy
BLEU = 71.21, 86.0/75.9/66.7/59.0 (BP=1.000, ratio=1.055, hyp_len=24796, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.256.0.05-1.05.0.05-1.05.0.98-2.66.0.84-2.31.pth, myrk
BLEU = 70.45, 86.1/75.2/65.9/57.8 (BP=1.000, ratio=1.049, hyp_len=24287, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.256.0.05-1.05.0.05-1.05.0.98-2.66.0.84-2.31.pth, rkmy
BLEU = 71.12, 86.1/75.9/66.6/58.8 (BP=1.000, ratio=1.054, hyp_len=24768, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.257.0.05-1.05.0.05-1.05.0.98-2.65.0.83-2.30.pth, myrk
BLEU = 70.45, 86.0/75.2/65.9/57.8 (BP=1.000, ratio=1.047, hyp_len=24257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.257.0.05-1.05.0.05-1.05.0.98-2.65.0.83-2.30.pth, rkmy
BLEU = 71.81, 86.5/76.4/67.3/59.7 (BP=1.000, ratio=1.051, hyp_len=24700, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.258.0.05-1.05.0.05-1.05.0.96-2.60.0.84-2.32.pth, myrk
BLEU = 69.55, 85.7/74.6/64.9/56.4 (BP=1.000, ratio=1.051, hyp_len=24339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.258.0.05-1.05.0.05-1.05.0.96-2.60.0.84-2.32.pth, rkmy
BLEU = 72.36, 86.7/76.9/68.0/60.5 (BP=1.000, ratio=1.047, hyp_len=24623, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.259.0.05-1.05.0.05-1.05.0.97-2.63.0.80-2.24.pth, myrk
BLEU = 69.89, 85.9/74.9/65.3/56.9 (BP=1.000, ratio=1.051, hyp_len=24350, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.259.0.05-1.05.0.05-1.05.0.97-2.63.0.80-2.24.pth, rkmy
BLEU = 71.51, 86.3/76.1/67.0/59.5 (BP=1.000, ratio=1.058, hyp_len=24861, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.260.0.05-1.05.0.05-1.05.0.95-2.58.0.82-2.27.pth, myrk
BLEU = 70.30, 86.0/75.1/65.6/57.6 (BP=1.000, ratio=1.049, hyp_len=24304, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.260.0.05-1.05.0.05-1.05.0.95-2.58.0.82-2.27.pth, rkmy
BLEU = 71.95, 86.5/76.6/67.5/59.9 (BP=1.000, ratio=1.050, hyp_len=24683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.30-1.35.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 67.51, 84.0/72.6/62.7/54.4 (BP=1.000, ratio=1.059, hyp_len=24533, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.30-1.35.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 69.15, 84.5/74.1/64.5/56.6 (BP=1.000, ratio=1.058, hyp_len=24882, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.261.0.05-1.05.0.05-1.05.0.97-2.63.0.85-2.34.pth, myrk
BLEU = 70.07, 86.0/75.0/65.4/57.1 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.261.0.05-1.05.0.05-1.05.0.97-2.63.0.85-2.34.pth, rkmy
BLEU = 71.57, 86.4/76.3/67.1/59.3 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.262.0.05-1.05.0.05-1.05.0.95-2.58.0.83-2.29.pth, myrk
BLEU = 70.65, 86.2/75.3/66.1/58.1 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.262.0.05-1.05.0.05-1.05.0.95-2.58.0.83-2.29.pth, rkmy
BLEU = 71.25, 86.1/76.0/66.7/59.0 (BP=1.000, ratio=1.056, hyp_len=24832, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.263.0.05-1.05.0.05-1.05.0.97-2.65.0.82-2.28.pth, myrk
BLEU = 70.33, 86.1/75.2/65.7/57.6 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.263.0.05-1.05.0.05-1.05.0.97-2.65.0.82-2.28.pth, rkmy
BLEU = 71.39, 86.3/76.1/66.8/59.2 (BP=1.000, ratio=1.054, hyp_len=24789, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.264.0.05-1.05.0.05-1.05.0.97-2.65.0.81-2.25.pth, myrk
BLEU = 70.83, 86.2/75.5/66.3/58.3 (BP=1.000, ratio=1.045, hyp_len=24196, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.264.0.05-1.05.0.05-1.05.0.97-2.65.0.81-2.25.pth, rkmy
BLEU = 70.41, 85.3/75.1/65.9/58.2 (BP=1.000, ratio=1.066, hyp_len=25070, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.265.0.05-1.05.0.05-1.05.0.99-2.68.0.80-2.22.pth, myrk
BLEU = 70.15, 85.8/75.0/65.6/57.4 (BP=1.000, ratio=1.052, hyp_len=24354, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.265.0.05-1.05.0.05-1.05.0.99-2.68.0.80-2.22.pth, rkmy
BLEU = 71.72, 86.5/76.4/67.2/59.6 (BP=1.000, ratio=1.050, hyp_len=24684, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.266.0.05-1.05.0.05-1.05.0.99-2.68.0.81-2.25.pth, myrk
BLEU = 70.42, 86.2/75.2/65.8/57.7 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.266.0.05-1.05.0.05-1.05.0.99-2.68.0.81-2.25.pth, rkmy
BLEU = 71.63, 86.3/76.3/67.2/59.5 (BP=1.000, ratio=1.053, hyp_len=24766, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.267.0.05-1.05.0.05-1.05.0.97-2.64.0.82-2.27.pth, myrk
BLEU = 69.97, 85.6/74.6/65.3/57.4 (BP=1.000, ratio=1.051, hyp_len=24348, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.267.0.05-1.05.0.05-1.05.0.97-2.64.0.82-2.27.pth, rkmy
BLEU = 71.27, 86.3/76.1/66.7/59.0 (BP=1.000, ratio=1.054, hyp_len=24767, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.268.0.05-1.05.0.05-1.05.0.97-2.64.0.83-2.30.pth, myrk
BLEU = 69.91, 85.8/74.7/65.3/57.1 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.268.0.05-1.05.0.05-1.05.0.97-2.64.0.83-2.30.pth, rkmy
BLEU = 71.22, 86.0/76.0/66.8/59.0 (BP=1.000, ratio=1.055, hyp_len=24796, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.269.0.05-1.05.0.05-1.05.1.01-2.73.0.81-2.25.pth, myrk
BLEU = 70.21, 85.8/74.9/65.7/57.6 (BP=1.000, ratio=1.052, hyp_len=24364, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.269.0.05-1.05.0.05-1.05.1.01-2.73.0.81-2.25.pth, rkmy
BLEU = 70.49, 85.5/75.3/66.0/58.1 (BP=1.000, ratio=1.060, hyp_len=24909, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.270.0.05-1.05.0.05-1.05.0.97-2.64.0.82-2.27.pth, myrk
BLEU = 70.49, 85.8/75.1/66.0/58.1 (BP=1.000, ratio=1.049, hyp_len=24304, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.270.0.05-1.05.0.05-1.05.0.97-2.64.0.82-2.27.pth, rkmy
BLEU = 71.45, 86.1/76.2/67.0/59.2 (BP=1.000, ratio=1.056, hyp_len=24825, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.33.0.28-1.33.0.66-1.94.0.61-1.85.pth, myrk
BLEU = 68.93, 84.5/73.6/64.3/56.5 (BP=1.000, ratio=1.059, hyp_len=24537, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.33.0.28-1.33.0.66-1.94.0.61-1.85.pth, rkmy
BLEU = 67.05, 83.0/72.3/62.3/54.0 (BP=1.000, ratio=1.080, hyp_len=25390, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.271.0.05-1.05.0.05-1.05.1.00-2.73.0.82-2.27.pth, myrk
BLEU = 69.48, 85.2/74.2/64.9/56.8 (BP=1.000, ratio=1.055, hyp_len=24437, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.271.0.05-1.05.0.05-1.05.1.00-2.73.0.82-2.27.pth, rkmy
BLEU = 71.43, 86.0/76.0/67.0/59.5 (BP=1.000, ratio=1.057, hyp_len=24858, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.272.0.05-1.05.0.05-1.05.0.99-2.68.0.82-2.28.pth, myrk
BLEU = 68.77, 84.6/73.6/64.1/56.0 (BP=1.000, ratio=1.061, hyp_len=24578, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.272.0.05-1.05.0.05-1.05.0.99-2.68.0.82-2.28.pth, rkmy
BLEU = 71.76, 86.3/76.5/67.3/59.8 (BP=1.000, ratio=1.052, hyp_len=24741, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.273.0.05-1.05.0.05-1.05.1.00-2.72.0.84-2.32.pth, myrk
BLEU = 70.39, 85.9/75.1/65.9/57.8 (BP=1.000, ratio=1.046, hyp_len=24230, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.273.0.05-1.05.0.05-1.05.1.00-2.72.0.84-2.32.pth, rkmy
BLEU = 72.07, 86.5/76.7/67.6/60.1 (BP=1.000, ratio=1.051, hyp_len=24707, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.274.0.05-1.05.0.05-1.05.0.99-2.70.0.83-2.29.pth, myrk
BLEU = 70.33, 85.8/75.0/65.8/57.8 (BP=1.000, ratio=1.053, hyp_len=24385, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.274.0.05-1.05.0.05-1.05.0.99-2.70.0.83-2.29.pth, rkmy
BLEU = 71.96, 86.4/76.6/67.6/60.0 (BP=1.000, ratio=1.053, hyp_len=24760, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.275.0.05-1.05.0.05-1.05.0.97-2.64.0.81-2.24.pth, myrk
BLEU = 70.38, 86.0/75.1/65.8/57.7 (BP=1.000, ratio=1.048, hyp_len=24265, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.275.0.05-1.05.0.05-1.05.0.97-2.64.0.81-2.24.pth, rkmy
BLEU = 71.58, 86.3/76.4/67.1/59.4 (BP=1.000, ratio=1.054, hyp_len=24778, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.276.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.35.pth, myrk
BLEU = 70.77, 86.1/75.3/66.3/58.3 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.276.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.35.pth, rkmy
BLEU = 71.30, 86.0/76.0/66.8/59.2 (BP=1.000, ratio=1.056, hyp_len=24834, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.277.0.05-1.05.0.05-1.05.0.95-2.59.0.84-2.31.pth, myrk
BLEU = 70.10, 85.6/74.7/65.5/57.6 (BP=1.000, ratio=1.052, hyp_len=24355, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.277.0.05-1.05.0.05-1.05.0.95-2.59.0.84-2.31.pth, rkmy
BLEU = 71.30, 86.1/76.0/66.8/59.2 (BP=1.000, ratio=1.052, hyp_len=24732, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.278.0.05-1.05.0.05-1.05.0.96-2.61.0.84-2.31.pth, myrk
BLEU = 69.61, 85.6/74.5/65.0/56.6 (BP=1.000, ratio=1.053, hyp_len=24387, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.278.0.05-1.05.0.05-1.05.0.96-2.61.0.84-2.31.pth, rkmy
BLEU = 71.63, 86.2/76.4/67.1/59.5 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.279.0.05-1.05.0.04-1.05.0.95-2.58.0.84-2.31.pth, myrk
BLEU = 69.70, 85.8/74.6/65.0/56.8 (BP=1.000, ratio=1.049, hyp_len=24291, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.279.0.05-1.05.0.04-1.05.0.95-2.58.0.84-2.31.pth, rkmy
BLEU = 71.16, 86.0/75.9/66.7/59.0 (BP=1.000, ratio=1.056, hyp_len=24827, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.280.0.05-1.05.0.05-1.05.0.97-2.63.0.87-2.40.pth, myrk
BLEU = 69.83, 85.6/74.6/65.2/57.1 (BP=1.000, ratio=1.052, hyp_len=24353, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.280.0.05-1.05.0.05-1.05.0.97-2.63.0.87-2.40.pth, rkmy
BLEU = 72.04, 86.5/76.8/67.6/60.0 (BP=1.000, ratio=1.050, hyp_len=24689, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.27-1.31.0.64-1.89.0.62-1.86.pth, myrk
BLEU = 68.68, 84.0/73.3/64.2/56.3 (BP=1.000, ratio=1.068, hyp_len=24746, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.27-1.31.0.64-1.89.0.62-1.86.pth, rkmy
BLEU = 66.54, 82.4/71.8/61.8/53.7 (BP=1.000, ratio=1.095, hyp_len=25734, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.281.0.05-1.05.0.05-1.05.0.97-2.64.0.84-2.31.pth, myrk
BLEU = 70.46, 86.1/75.1/65.8/57.9 (BP=1.000, ratio=1.044, hyp_len=24169, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.281.0.05-1.05.0.05-1.05.0.97-2.64.0.84-2.31.pth, rkmy
BLEU = 71.77, 86.4/76.4/67.3/59.7 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.282.0.05-1.05.0.05-1.05.0.98-2.65.0.82-2.28.pth, myrk
BLEU = 70.22, 86.0/75.0/65.6/57.4 (BP=1.000, ratio=1.049, hyp_len=24296, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.282.0.05-1.05.0.05-1.05.0.98-2.65.0.82-2.28.pth, rkmy
BLEU = 72.52, 86.9/77.1/68.1/60.6 (BP=1.000, ratio=1.046, hyp_len=24599, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.283.0.05-1.05.0.05-1.05.0.96-2.62.0.82-2.26.pth, myrk
BLEU = 70.25, 85.7/74.9/65.7/57.8 (BP=1.000, ratio=1.049, hyp_len=24295, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.283.0.05-1.05.0.05-1.05.0.96-2.62.0.82-2.26.pth, rkmy
BLEU = 71.07, 85.9/75.8/66.5/58.9 (BP=1.000, ratio=1.059, hyp_len=24888, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.284.0.04-1.04.0.05-1.05.0.97-2.63.0.86-2.36.pth, myrk
BLEU = 70.52, 85.9/75.2/66.0/58.1 (BP=1.000, ratio=1.047, hyp_len=24239, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.284.0.04-1.04.0.05-1.05.0.97-2.63.0.86-2.36.pth, rkmy
BLEU = 71.82, 86.5/76.5/67.4/59.7 (BP=1.000, ratio=1.052, hyp_len=24728, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.285.0.05-1.05.0.05-1.05.0.98-2.67.0.89-2.44.pth, myrk
BLEU = 70.35, 85.8/75.0/65.9/57.8 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.285.0.05-1.05.0.05-1.05.0.98-2.67.0.89-2.44.pth, rkmy
BLEU = 71.95, 86.6/76.6/67.5/59.9 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.286.0.05-1.05.0.05-1.05.1.02-2.77.0.85-2.33.pth, myrk
BLEU = 70.29, 85.9/75.1/65.8/57.6 (BP=1.000, ratio=1.051, hyp_len=24348, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.286.0.05-1.05.0.05-1.05.1.02-2.77.0.85-2.33.pth, rkmy
BLEU = 71.46, 86.0/76.0/67.0/59.5 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.287.0.04-1.05.0.04-1.04.1.00-2.72.0.83-2.29.pth, myrk
BLEU = 70.09, 85.7/74.9/65.6/57.4 (BP=1.000, ratio=1.050, hyp_len=24310, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.287.0.04-1.05.0.04-1.04.1.00-2.72.0.83-2.29.pth, rkmy
BLEU = 71.89, 86.4/76.6/67.5/59.8 (BP=1.000, ratio=1.053, hyp_len=24746, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.288.0.05-1.05.0.05-1.05.1.02-2.77.0.83-2.29.pth, myrk
BLEU = 70.28, 85.6/74.9/65.7/57.9 (BP=1.000, ratio=1.051, hyp_len=24348, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.288.0.05-1.05.0.05-1.05.1.02-2.77.0.83-2.29.pth, rkmy
BLEU = 72.47, 86.5/76.9/68.2/60.8 (BP=1.000, ratio=1.052, hyp_len=24721, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.289.0.05-1.05.0.05-1.05.1.02-2.76.0.83-2.29.pth, myrk
BLEU = 69.96, 85.6/74.8/65.4/57.2 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.289.0.05-1.05.0.05-1.05.1.02-2.76.0.83-2.29.pth, rkmy
BLEU = 72.46, 86.7/77.1/68.1/60.6 (BP=1.000, ratio=1.048, hyp_len=24647, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.290.0.05-1.05.0.04-1.04.0.97-2.64.0.84-2.33.pth, myrk
BLEU = 71.04, 86.2/75.6/66.6/58.7 (BP=1.000, ratio=1.042, hyp_len=24133, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.290.0.05-1.05.0.04-1.04.0.97-2.64.0.84-2.33.pth, rkmy
BLEU = 72.16, 86.7/76.9/67.7/60.1 (BP=1.000, ratio=1.050, hyp_len=24691, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.26-1.30.0.67-1.95.0.59-1.80.pth, myrk
BLEU = 71.65, 87.3/76.4/67.0/59.0 (BP=1.000, ratio=1.023, hyp_len=23700, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.26-1.30.0.67-1.95.0.59-1.80.pth, rkmy
BLEU = 68.39, 84.5/73.5/63.5/55.4 (BP=1.000, ratio=1.056, hyp_len=24823, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.291.0.05-1.05.0.05-1.05.0.99-2.68.0.83-2.29.pth, myrk
BLEU = 70.04, 85.7/74.8/65.4/57.4 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.291.0.05-1.05.0.05-1.05.0.99-2.68.0.83-2.29.pth, rkmy
BLEU = 71.87, 86.1/76.3/67.5/60.1 (BP=1.000, ratio=1.056, hyp_len=24819, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.292.0.05-1.05.0.04-1.04.1.01-2.76.0.85-2.33.pth, myrk
BLEU = 70.54, 86.2/75.2/66.0/57.9 (BP=1.000, ratio=1.047, hyp_len=24252, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.292.0.05-1.05.0.04-1.04.1.01-2.76.0.85-2.33.pth, rkmy
BLEU = 71.56, 86.3/76.3/67.0/59.4 (BP=1.000, ratio=1.054, hyp_len=24772, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.293.0.04-1.04.0.04-1.05.1.00-2.71.0.85-2.33.pth, myrk
BLEU = 70.09, 85.8/74.9/65.6/57.3 (BP=1.000, ratio=1.052, hyp_len=24363, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.293.0.04-1.04.0.04-1.05.1.00-2.71.0.85-2.33.pth, rkmy
BLEU = 71.82, 86.3/76.3/67.4/60.0 (BP=1.000, ratio=1.055, hyp_len=24802, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.294.0.04-1.05.0.04-1.04.0.99-2.68.0.85-2.33.pth, myrk
BLEU = 70.18, 85.8/74.9/65.7/57.5 (BP=1.000, ratio=1.048, hyp_len=24282, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.294.0.04-1.05.0.04-1.04.0.99-2.68.0.85-2.33.pth, rkmy
BLEU = 72.69, 87.0/77.3/68.3/60.8 (BP=1.000, ratio=1.046, hyp_len=24601, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.295.0.05-1.05.0.05-1.05.0.99-2.69.0.84-2.32.pth, myrk
BLEU = 70.70, 86.2/75.4/66.2/58.1 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.295.0.05-1.05.0.05-1.05.0.99-2.69.0.84-2.32.pth, rkmy
BLEU = 72.79, 86.9/77.2/68.4/61.1 (BP=1.000, ratio=1.048, hyp_len=24630, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.296.0.05-1.05.0.05-1.05.0.97-2.64.0.85-2.34.pth, myrk
BLEU = 70.53, 86.1/75.3/66.0/57.9 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.296.0.05-1.05.0.05-1.05.0.97-2.64.0.85-2.34.pth, rkmy
BLEU = 71.60, 86.2/76.2/67.2/59.5 (BP=1.000, ratio=1.055, hyp_len=24813, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.297.0.05-1.05.0.04-1.05.1.00-2.71.0.84-2.33.pth, myrk
BLEU = 70.55, 86.1/75.3/66.0/57.9 (BP=1.000, ratio=1.046, hyp_len=24214, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.297.0.05-1.05.0.04-1.05.1.00-2.71.0.84-2.33.pth, rkmy
BLEU = 71.50, 86.0/76.1/67.1/59.5 (BP=1.000, ratio=1.058, hyp_len=24870, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.298.0.05-1.05.0.04-1.05.0.97-2.64.0.83-2.29.pth, myrk
BLEU = 70.27, 86.0/75.0/65.7/57.5 (BP=1.000, ratio=1.047, hyp_len=24260, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.298.0.05-1.05.0.04-1.05.0.97-2.64.0.83-2.29.pth, rkmy
BLEU = 72.69, 86.7/77.1/68.4/61.1 (BP=1.000, ratio=1.049, hyp_len=24658, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.299.0.04-1.05.0.04-1.05.0.97-2.63.0.85-2.34.pth, myrk
BLEU = 69.19, 84.9/73.9/64.6/56.5 (BP=1.000, ratio=1.059, hyp_len=24535, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.299.0.04-1.05.0.04-1.05.0.97-2.63.0.85-2.34.pth, rkmy
BLEU = 72.19, 86.7/76.9/67.7/60.2 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.300.0.05-1.05.0.05-1.05.0.98-2.68.0.84-2.31.pth, myrk
BLEU = 70.08, 85.6/74.8/65.6/57.4 (BP=1.000, ratio=1.052, hyp_len=24353, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.300.0.05-1.05.0.05-1.05.0.98-2.68.0.84-2.31.pth, rkmy
BLEU = 71.14, 86.0/75.9/66.6/58.9 (BP=1.000, ratio=1.057, hyp_len=24848, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.26-1.30.0.67-1.96.0.60-1.82.pth, myrk
BLEU = 70.69, 86.6/75.4/66.0/57.9 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.26-1.30.0.67-1.96.0.60-1.82.pth, rkmy
BLEU = 68.08, 84.4/73.4/63.3/54.9 (BP=1.000, ratio=1.061, hyp_len=24954, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.301.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.35.pth, myrk
BLEU = 70.24, 85.8/74.8/65.6/57.7 (BP=1.000, ratio=1.048, hyp_len=24277, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.301.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.35.pth, rkmy
BLEU = 72.31, 86.5/76.8/67.9/60.6 (BP=1.000, ratio=1.050, hyp_len=24690, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.302.0.05-1.05.0.05-1.05.0.97-2.63.0.85-2.34.pth, myrk
BLEU = 70.28, 86.1/75.2/65.7/57.4 (BP=1.000, ratio=1.048, hyp_len=24265, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.302.0.05-1.05.0.05-1.05.0.97-2.63.0.85-2.34.pth, rkmy
BLEU = 72.21, 86.5/76.7/67.8/60.5 (BP=1.000, ratio=1.052, hyp_len=24727, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.303.0.05-1.05.0.05-1.05.0.99-2.68.0.87-2.39.pth, myrk
BLEU = 70.33, 86.1/75.1/65.7/57.5 (BP=1.000, ratio=1.047, hyp_len=24240, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.303.0.05-1.05.0.05-1.05.0.99-2.68.0.87-2.39.pth, rkmy
BLEU = 72.71, 86.9/77.2/68.3/61.0 (BP=1.000, ratio=1.048, hyp_len=24634, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.304.0.05-1.05.0.04-1.04.0.99-2.68.0.86-2.37.pth, myrk
BLEU = 69.80, 85.6/74.6/65.2/57.0 (BP=1.000, ratio=1.053, hyp_len=24394, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.304.0.05-1.05.0.04-1.04.0.99-2.68.0.86-2.37.pth, rkmy
BLEU = 72.48, 86.8/77.0/68.0/60.7 (BP=1.000, ratio=1.047, hyp_len=24611, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.305.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.34.pth, myrk
BLEU = 70.72, 86.3/75.4/66.1/58.1 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.305.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.34.pth, rkmy
BLEU = 71.23, 85.7/75.8/66.8/59.4 (BP=1.000, ratio=1.059, hyp_len=24886, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.306.0.04-1.04.0.04-1.04.0.99-2.69.0.84-2.31.pth, myrk
BLEU = 70.19, 85.9/75.0/65.6/57.4 (BP=1.000, ratio=1.049, hyp_len=24299, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.306.0.04-1.04.0.04-1.04.0.99-2.69.0.84-2.31.pth, rkmy
BLEU = 71.21, 85.9/75.9/66.8/59.0 (BP=1.000, ratio=1.057, hyp_len=24859, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.307.0.05-1.05.0.05-1.05.0.98-2.66.0.85-2.33.pth, myrk
BLEU = 70.47, 85.9/75.0/65.9/58.0 (BP=1.000, ratio=1.046, hyp_len=24214, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.307.0.05-1.05.0.05-1.05.0.98-2.66.0.85-2.33.pth, rkmy
BLEU = 71.32, 86.0/75.9/66.8/59.3 (BP=1.000, ratio=1.057, hyp_len=24849, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.308.0.04-1.04.0.04-1.04.1.00-2.72.0.88-2.41.pth, myrk
BLEU = 70.73, 86.1/75.3/66.2/58.3 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.308.0.04-1.04.0.04-1.04.1.00-2.72.0.88-2.41.pth, rkmy
BLEU = 73.03, 87.1/77.5/68.7/61.4 (BP=1.000, ratio=1.046, hyp_len=24600, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.309.0.04-1.05.0.04-1.04.1.00-2.72.0.85-2.34.pth, myrk
BLEU = 70.70, 86.0/75.4/66.3/58.2 (BP=1.000, ratio=1.051, hyp_len=24344, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.309.0.04-1.05.0.04-1.04.1.00-2.72.0.85-2.34.pth, rkmy
BLEU = 71.98, 86.7/76.5/67.4/60.0 (BP=1.000, ratio=1.050, hyp_len=24696, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.310.0.04-1.04.0.05-1.05.1.00-2.72.0.85-2.33.pth, myrk
BLEU = 70.12, 85.8/74.9/65.5/57.4 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.310.0.04-1.04.0.05-1.05.1.00-2.72.0.85-2.33.pth, rkmy
BLEU = 72.63, 86.7/77.1/68.3/60.9 (BP=1.000, ratio=1.049, hyp_len=24659, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.26-1.29.0.26-1.29.0.66-1.94.0.61-1.84.pth, myrk
BLEU = 70.36, 85.8/75.0/65.8/57.9 (BP=1.000, ratio=1.039, hyp_len=24066, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.26-1.29.0.26-1.29.0.66-1.94.0.61-1.84.pth, rkmy
BLEU = 68.33, 84.2/73.7/63.7/55.1 (BP=1.000, ratio=1.066, hyp_len=25057, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.311.0.05-1.05.0.05-1.05.0.98-2.66.0.86-2.36.pth, myrk
BLEU = 70.74, 86.1/75.4/66.2/58.2 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.311.0.05-1.05.0.05-1.05.0.98-2.66.0.86-2.36.pth, rkmy
BLEU = 71.44, 86.1/76.2/67.0/59.3 (BP=1.000, ratio=1.056, hyp_len=24832, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.312.0.05-1.05.0.05-1.05.1.00-2.72.0.85-2.33.pth, myrk
BLEU = 70.39, 86.0/75.1/65.8/57.8 (BP=1.000, ratio=1.048, hyp_len=24274, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.312.0.05-1.05.0.05-1.05.1.00-2.72.0.85-2.33.pth, rkmy
BLEU = 72.83, 86.9/77.3/68.5/61.2 (BP=1.000, ratio=1.050, hyp_len=24681, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.313.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.34.pth, myrk
BLEU = 70.08, 85.7/74.9/65.5/57.4 (BP=1.000, ratio=1.051, hyp_len=24348, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.313.0.05-1.05.0.05-1.05.0.98-2.67.0.85-2.34.pth, rkmy
BLEU = 71.87, 86.4/76.5/67.5/59.9 (BP=1.000, ratio=1.056, hyp_len=24819, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.314.0.04-1.04.0.04-1.04.0.99-2.69.0.84-2.32.pth, myrk
BLEU = 70.23, 85.8/75.1/65.7/57.5 (BP=1.000, ratio=1.049, hyp_len=24304, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.314.0.04-1.04.0.04-1.04.0.99-2.69.0.84-2.32.pth, rkmy
BLEU = 72.46, 86.8/77.0/68.0/60.7 (BP=1.000, ratio=1.051, hyp_len=24698, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.315.0.05-1.05.0.04-1.05.1.01-2.75.0.84-2.32.pth, myrk
BLEU = 69.61, 85.1/74.3/65.1/57.0 (BP=1.000, ratio=1.055, hyp_len=24440, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.315.0.05-1.05.0.04-1.05.1.01-2.75.0.84-2.32.pth, rkmy
BLEU = 71.53, 86.3/76.3/67.0/59.3 (BP=1.000, ratio=1.053, hyp_len=24765, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.316.0.05-1.05.0.04-1.05.0.99-2.68.0.84-2.33.pth, myrk
BLEU = 68.89, 85.1/73.8/64.2/55.8 (BP=1.000, ratio=1.054, hyp_len=24421, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.316.0.05-1.05.0.04-1.05.0.99-2.68.0.84-2.33.pth, rkmy
BLEU = 71.03, 86.0/75.9/66.5/58.6 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.317.0.04-1.05.0.04-1.04.0.98-2.66.0.87-2.38.pth, myrk
BLEU = 69.86, 85.4/74.5/65.3/57.3 (BP=1.000, ratio=1.053, hyp_len=24377, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.317.0.04-1.05.0.04-1.04.0.98-2.66.0.87-2.38.pth, rkmy
BLEU = 71.37, 86.1/76.2/66.9/59.1 (BP=1.000, ratio=1.056, hyp_len=24817, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.318.0.04-1.04.0.04-1.04.0.99-2.69.0.88-2.40.pth, myrk
BLEU = 70.56, 86.2/75.3/65.9/58.0 (BP=1.000, ratio=1.043, hyp_len=24157, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.318.0.04-1.04.0.04-1.04.0.99-2.69.0.88-2.40.pth, rkmy
BLEU = 72.21, 86.6/76.8/67.8/60.3 (BP=1.000, ratio=1.049, hyp_len=24659, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.319.0.04-1.04.0.04-1.04.0.99-2.69.0.87-2.40.pth, myrk
BLEU = 70.14, 85.8/74.9/65.6/57.4 (BP=1.000, ratio=1.051, hyp_len=24343, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.319.0.04-1.04.0.04-1.04.0.99-2.69.0.87-2.40.pth, rkmy
BLEU = 71.66, 86.3/76.3/67.2/59.6 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.320.0.04-1.04.0.04-1.05.1.02-2.78.0.87-2.38.pth, myrk
BLEU = 70.32, 86.0/75.1/65.7/57.6 (BP=1.000, ratio=1.047, hyp_len=24253, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.320.0.04-1.04.0.04-1.05.1.02-2.78.0.87-2.38.pth, rkmy
BLEU = 72.88, 87.0/77.4/68.5/61.2 (BP=1.000, ratio=1.047, hyp_len=24615, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.24-1.27.0.66-1.94.0.62-1.85.pth, myrk
BLEU = 68.64, 84.8/73.6/63.9/55.6 (BP=1.000, ratio=1.052, hyp_len=24366, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.24-1.27.0.66-1.94.0.62-1.85.pth, rkmy
BLEU = 67.67, 84.0/72.9/62.8/54.5 (BP=1.000, ratio=1.062, hyp_len=24966, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.321.0.05-1.05.0.05-1.05.0.99-2.70.0.85-2.35.pth, myrk
BLEU = 70.25, 86.0/75.0/65.6/57.5 (BP=1.000, ratio=1.047, hyp_len=24250, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.321.0.05-1.05.0.05-1.05.0.99-2.70.0.85-2.35.pth, rkmy
BLEU = 71.74, 86.6/76.6/67.2/59.5 (BP=1.000, ratio=1.051, hyp_len=24717, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.322.0.04-1.05.0.04-1.05.1.00-2.71.0.84-2.32.pth, myrk
BLEU = 70.43, 86.0/75.2/65.9/57.7 (BP=1.000, ratio=1.048, hyp_len=24278, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.322.0.04-1.05.0.04-1.05.1.00-2.71.0.84-2.32.pth, rkmy
BLEU = 73.81, 87.5/78.2/69.5/62.4 (BP=1.000, ratio=1.043, hyp_len=24517, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.323.0.05-1.05.0.05-1.05.1.01-2.76.0.82-2.27.pth, myrk
BLEU = 69.45, 85.3/74.4/64.8/56.6 (BP=1.000, ratio=1.055, hyp_len=24434, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.323.0.05-1.05.0.05-1.05.1.01-2.76.0.82-2.27.pth, rkmy
BLEU = 72.18, 86.5/76.8/67.8/60.3 (BP=1.000, ratio=1.053, hyp_len=24745, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.324.0.04-1.04.0.04-1.04.1.02-2.77.0.84-2.31.pth, myrk
BLEU = 69.96, 85.4/74.7/65.4/57.4 (BP=1.000, ratio=1.056, hyp_len=24451, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.324.0.04-1.04.0.04-1.04.1.02-2.77.0.84-2.31.pth, rkmy
BLEU = 72.18, 86.7/76.7/67.8/60.3 (BP=1.000, ratio=1.050, hyp_len=24673, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.325.0.05-1.05.0.05-1.05.1.01-2.74.0.85-2.35.pth, myrk
BLEU = 71.13, 86.3/75.7/66.7/58.8 (BP=1.000, ratio=1.046, hyp_len=24222, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.325.0.05-1.05.0.05-1.05.1.01-2.74.0.85-2.35.pth, rkmy
BLEU = 71.77, 86.4/76.4/67.3/59.8 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.326.0.04-1.04.0.04-1.05.1.04-2.83.0.87-2.39.pth, myrk
BLEU = 69.85, 85.8/74.8/65.2/56.9 (BP=1.000, ratio=1.054, hyp_len=24409, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.326.0.04-1.04.0.04-1.05.1.04-2.83.0.87-2.39.pth, rkmy
BLEU = 72.72, 86.7/77.1/68.4/61.1 (BP=1.000, ratio=1.050, hyp_len=24685, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.327.0.05-1.05.0.04-1.05.1.02-2.77.0.86-2.36.pth, myrk
BLEU = 70.64, 86.2/75.4/66.0/58.0 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.327.0.05-1.05.0.04-1.05.1.02-2.77.0.86-2.36.pth, rkmy
BLEU = 72.11, 86.5/76.7/67.7/60.2 (BP=1.000, ratio=1.053, hyp_len=24748, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.328.0.04-1.04.0.04-1.04.1.01-2.74.0.86-2.36.pth, myrk
BLEU = 70.34, 85.8/75.1/65.8/57.7 (BP=1.000, ratio=1.050, hyp_len=24326, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.328.0.04-1.04.0.04-1.04.1.01-2.74.0.86-2.36.pth, rkmy
BLEU = 71.65, 86.2/76.2/67.2/59.7 (BP=1.000, ratio=1.055, hyp_len=24792, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.329.0.04-1.04.0.04-1.04.1.01-2.74.0.87-2.39.pth, myrk
BLEU = 70.79, 86.2/75.4/66.2/58.3 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.329.0.04-1.04.0.04-1.04.1.01-2.74.0.87-2.39.pth, rkmy
BLEU = 72.23, 86.6/76.9/67.8/60.3 (BP=1.000, ratio=1.053, hyp_len=24760, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.330.0.04-1.04.0.04-1.05.1.01-2.76.0.85-2.33.pth, myrk
BLEU = 70.08, 85.8/74.8/65.4/57.4 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.330.0.04-1.04.0.04-1.05.1.01-2.76.0.85-2.33.pth, rkmy
BLEU = 71.11, 86.1/76.0/66.6/58.7 (BP=1.000, ratio=1.056, hyp_len=24816, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.29.0.25-1.29.0.66-1.94.0.62-1.86.pth, myrk
BLEU = 70.28, 86.1/75.1/65.6/57.5 (BP=1.000, ratio=1.040, hyp_len=24087, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.29.0.25-1.29.0.66-1.94.0.62-1.86.pth, rkmy
BLEU = 68.49, 84.5/73.6/63.7/55.6 (BP=1.000, ratio=1.058, hyp_len=24870, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.331.0.05-1.05.0.04-1.04.1.00-2.72.0.87-2.40.pth, myrk
BLEU = 69.40, 85.5/74.4/64.7/56.4 (BP=1.000, ratio=1.054, hyp_len=24402, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.331.0.05-1.05.0.04-1.04.1.00-2.72.0.87-2.40.pth, rkmy
BLEU = 73.52, 87.3/77.8/69.2/62.1 (BP=1.000, ratio=1.043, hyp_len=24527, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.332.0.05-1.05.0.04-1.05.1.00-2.71.0.86-2.36.pth, myrk
BLEU = 70.97, 86.2/75.4/66.4/58.7 (BP=1.000, ratio=1.046, hyp_len=24221, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.332.0.05-1.05.0.04-1.05.1.00-2.71.0.86-2.36.pth, rkmy
BLEU = 72.25, 86.5/76.7/67.8/60.6 (BP=1.000, ratio=1.051, hyp_len=24716, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.333.0.04-1.04.0.04-1.04.0.99-2.68.0.85-2.35.pth, myrk
BLEU = 69.63, 85.6/74.5/65.0/56.7 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.333.0.04-1.04.0.04-1.04.0.99-2.68.0.85-2.35.pth, rkmy
BLEU = 72.13, 86.5/76.7/67.7/60.2 (BP=1.000, ratio=1.052, hyp_len=24728, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.334.0.04-1.04.0.04-1.04.0.98-2.65.0.84-2.33.pth, myrk
BLEU = 68.91, 84.8/73.6/64.2/56.3 (BP=1.000, ratio=1.056, hyp_len=24454, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.334.0.04-1.04.0.04-1.04.0.98-2.65.0.84-2.33.pth, rkmy
BLEU = 72.84, 86.9/77.3/68.5/61.2 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.335.0.05-1.05.0.04-1.04.0.98-2.68.0.87-2.38.pth, myrk
BLEU = 70.36, 85.8/75.0/65.8/57.8 (BP=1.000, ratio=1.048, hyp_len=24274, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.335.0.05-1.05.0.04-1.04.0.98-2.68.0.87-2.38.pth, rkmy
BLEU = 72.19, 86.6/76.8/67.7/60.3 (BP=1.000, ratio=1.051, hyp_len=24715, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.336.0.05-1.05.0.04-1.04.1.00-2.71.0.87-2.38.pth, myrk
BLEU = 70.26, 85.8/75.1/65.7/57.5 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.336.0.05-1.05.0.04-1.04.1.00-2.71.0.87-2.38.pth, rkmy
BLEU = 72.31, 86.6/76.9/67.9/60.4 (BP=1.000, ratio=1.051, hyp_len=24710, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.337.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, myrk
BLEU = 70.70, 86.2/75.4/66.1/58.1 (BP=1.000, ratio=1.046, hyp_len=24229, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.337.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, rkmy
BLEU = 72.34, 86.7/76.8/67.9/60.6 (BP=1.000, ratio=1.051, hyp_len=24713, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.338.0.04-1.04.0.04-1.04.1.01-2.73.0.87-2.39.pth, myrk
BLEU = 70.58, 86.1/75.3/66.0/57.9 (BP=1.000, ratio=1.048, hyp_len=24280, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.338.0.04-1.04.0.04-1.04.1.01-2.73.0.87-2.39.pth, rkmy
BLEU = 71.54, 86.2/76.3/67.1/59.3 (BP=1.000, ratio=1.055, hyp_len=24794, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.339.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, myrk
BLEU = 71.01, 86.3/75.6/66.5/58.6 (BP=1.000, ratio=1.046, hyp_len=24214, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.339.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, rkmy
BLEU = 72.42, 86.8/77.0/68.0/60.6 (BP=1.000, ratio=1.049, hyp_len=24667, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.340.0.04-1.04.0.04-1.04.1.00-2.73.0.87-2.39.pth, myrk
BLEU = 71.45, 86.6/76.0/67.0/59.2 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.340.0.04-1.04.0.04-1.04.1.00-2.73.0.87-2.39.pth, rkmy
BLEU = 72.36, 86.6/76.8/68.0/60.6 (BP=1.000, ratio=1.052, hyp_len=24725, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.22-1.25.0.22-1.25.0.66-1.93.0.62-1.86.pth, myrk
BLEU = 70.13, 85.8/74.8/65.4/57.6 (BP=1.000, ratio=1.039, hyp_len=24057, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.22-1.25.0.22-1.25.0.66-1.93.0.62-1.86.pth, rkmy
BLEU = 70.53, 85.8/75.4/65.9/58.1 (BP=1.000, ratio=1.046, hyp_len=24598, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.341.0.04-1.04.0.04-1.04.0.97-2.63.0.87-2.38.pth, myrk
BLEU = 71.34, 86.3/75.8/66.8/59.2 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.341.0.04-1.04.0.04-1.04.0.97-2.63.0.87-2.38.pth, rkmy
BLEU = 71.16, 86.0/76.0/66.7/58.9 (BP=1.000, ratio=1.057, hyp_len=24840, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.342.0.05-1.05.0.04-1.05.0.98-2.65.0.86-2.37.pth, myrk
BLEU = 70.27, 85.8/75.0/65.7/57.7 (BP=1.000, ratio=1.051, hyp_len=24337, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.342.0.05-1.05.0.04-1.05.0.98-2.65.0.86-2.37.pth, rkmy
BLEU = 72.89, 87.0/77.3/68.5/61.3 (BP=1.000, ratio=1.047, hyp_len=24625, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.343.0.04-1.04.0.04-1.04.0.96-2.62.0.86-2.37.pth, myrk
BLEU = 70.74, 86.0/75.3/66.2/58.3 (BP=1.000, ratio=1.047, hyp_len=24257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.343.0.04-1.04.0.04-1.04.0.96-2.62.0.86-2.37.pth, rkmy
BLEU = 71.90, 86.4/76.5/67.4/60.0 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.344.0.04-1.04.0.04-1.04.0.99-2.69.0.85-2.35.pth, myrk
BLEU = 70.17, 85.7/74.9/65.6/57.6 (BP=1.000, ratio=1.052, hyp_len=24363, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.344.0.04-1.04.0.04-1.04.0.99-2.69.0.85-2.35.pth, rkmy
BLEU = 72.36, 86.6/76.7/67.9/60.7 (BP=1.000, ratio=1.049, hyp_len=24656, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.345.0.04-1.04.0.04-1.04.0.99-2.68.0.86-2.36.pth, myrk
BLEU = 70.47, 85.9/75.1/65.9/57.9 (BP=1.000, ratio=1.048, hyp_len=24269, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.345.0.04-1.04.0.04-1.04.0.99-2.68.0.86-2.36.pth, rkmy
BLEU = 71.61, 86.1/76.3/67.2/59.6 (BP=1.000, ratio=1.054, hyp_len=24788, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.346.0.04-1.04.0.04-1.04.0.97-2.64.0.86-2.35.pth, myrk
BLEU = 70.32, 85.9/74.9/65.7/57.8 (BP=1.000, ratio=1.049, hyp_len=24296, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.346.0.04-1.04.0.04-1.04.0.97-2.64.0.86-2.35.pth, rkmy
BLEU = 71.32, 86.1/76.1/66.9/59.1 (BP=1.000, ratio=1.056, hyp_len=24819, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.347.0.04-1.04.0.04-1.04.0.98-2.67.0.86-2.36.pth, myrk
BLEU = 69.98, 85.6/74.7/65.4/57.3 (BP=1.000, ratio=1.052, hyp_len=24370, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.347.0.04-1.04.0.04-1.04.0.98-2.67.0.86-2.36.pth, rkmy
BLEU = 72.12, 86.5/76.7/67.7/60.2 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.348.0.04-1.04.0.04-1.04.0.97-2.65.0.85-2.33.pth, myrk
BLEU = 70.61, 85.8/75.1/66.1/58.3 (BP=1.000, ratio=1.050, hyp_len=24309, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.348.0.04-1.04.0.04-1.04.0.97-2.65.0.85-2.33.pth, rkmy
BLEU = 71.45, 86.2/76.1/67.0/59.3 (BP=1.000, ratio=1.054, hyp_len=24783, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.349.0.04-1.04.0.04-1.04.0.97-2.65.0.92-2.51.pth, myrk
BLEU = 70.18, 85.7/74.8/65.6/57.6 (BP=1.000, ratio=1.049, hyp_len=24305, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.349.0.04-1.04.0.04-1.04.0.97-2.65.0.92-2.51.pth, rkmy
BLEU = 72.43, 86.6/77.0/68.1/60.6 (BP=1.000, ratio=1.050, hyp_len=24678, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.350.0.04-1.04.0.04-1.04.1.00-2.73.0.90-2.45.pth, myrk
BLEU = 70.38, 86.1/75.0/65.7/57.9 (BP=1.000, ratio=1.049, hyp_len=24287, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.350.0.04-1.04.0.04-1.04.1.00-2.73.0.90-2.45.pth, rkmy
BLEU = 72.19, 86.4/76.6/67.8/60.5 (BP=1.000, ratio=1.051, hyp_len=24710, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.26.0.66-1.94.0.62-1.85.pth, myrk
BLEU = 70.23, 86.0/75.0/65.6/57.5 (BP=1.000, ratio=1.042, hyp_len=24135, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.26.0.66-1.94.0.62-1.85.pth, rkmy
BLEU = 68.52, 84.3/73.5/63.7/55.9 (BP=1.000, ratio=1.066, hyp_len=25055, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.351.0.04-1.04.0.04-1.04.1.00-2.71.0.90-2.47.pth, myrk
BLEU = 70.64, 86.0/75.3/66.1/58.2 (BP=1.000, ratio=1.050, hyp_len=24318, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.351.0.04-1.04.0.04-1.04.1.00-2.71.0.90-2.47.pth, rkmy
BLEU = 72.30, 86.6/76.9/67.9/60.4 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.352.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.41.pth, myrk
BLEU = 69.51, 85.1/74.1/65.0/56.9 (BP=1.000, ratio=1.058, hyp_len=24501, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.352.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.41.pth, rkmy
BLEU = 72.19, 86.7/76.8/67.8/60.2 (BP=1.000, ratio=1.049, hyp_len=24661, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.353.0.04-1.04.0.04-1.04.1.01-2.74.0.89-2.44.pth, myrk
BLEU = 70.53, 86.1/75.2/65.9/58.0 (BP=1.000, ratio=1.048, hyp_len=24266, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.353.0.04-1.04.0.04-1.04.1.01-2.74.0.89-2.44.pth, rkmy
BLEU = 70.33, 85.3/75.1/65.8/58.1 (BP=1.000, ratio=1.062, hyp_len=24976, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.354.0.04-1.04.0.04-1.04.1.00-2.72.0.88-2.41.pth, myrk
BLEU = 70.60, 85.9/75.1/66.1/58.3 (BP=1.000, ratio=1.051, hyp_len=24335, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.354.0.04-1.04.0.04-1.04.1.00-2.72.0.88-2.41.pth, rkmy
BLEU = 72.28, 86.7/77.0/67.9/60.3 (BP=1.000, ratio=1.051, hyp_len=24703, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.355.0.04-1.05.0.04-1.04.1.03-2.79.0.88-2.40.pth, myrk
BLEU = 70.72, 86.1/75.3/66.2/58.3 (BP=1.000, ratio=1.045, hyp_len=24195, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.355.0.04-1.05.0.04-1.04.1.03-2.79.0.88-2.40.pth, rkmy
BLEU = 71.70, 86.0/76.2/67.2/60.0 (BP=1.000, ratio=1.056, hyp_len=24830, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.356.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.41.pth, myrk
BLEU = 71.33, 86.4/75.8/66.9/59.1 (BP=1.000, ratio=1.046, hyp_len=24220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.356.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.41.pth, rkmy
BLEU = 72.49, 86.5/76.9/68.2/60.9 (BP=1.000, ratio=1.052, hyp_len=24737, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.357.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.38.pth, myrk
BLEU = 69.87, 85.7/74.7/65.2/57.1 (BP=1.000, ratio=1.051, hyp_len=24338, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.357.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.38.pth, rkmy
BLEU = 72.96, 87.2/77.4/68.5/61.3 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.358.0.04-1.05.0.04-1.04.1.01-2.74.0.88-2.42.pth, myrk
BLEU = 70.47, 86.1/75.2/65.9/57.9 (BP=1.000, ratio=1.046, hyp_len=24231, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.358.0.04-1.05.0.04-1.04.1.01-2.74.0.88-2.42.pth, rkmy
BLEU = 71.49, 86.1/76.2/67.0/59.4 (BP=1.000, ratio=1.055, hyp_len=24810, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.359.0.05-1.05.0.04-1.04.1.01-2.76.0.87-2.38.pth, myrk
BLEU = 70.46, 86.1/75.2/65.8/57.8 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.359.0.05-1.05.0.04-1.04.1.01-2.76.0.87-2.38.pth, rkmy
BLEU = 71.13, 86.0/75.9/66.6/58.9 (BP=1.000, ratio=1.059, hyp_len=24887, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.360.0.04-1.05.0.04-1.04.1.02-2.77.0.91-2.47.pth, myrk
BLEU = 69.18, 85.4/74.2/64.5/56.0 (BP=1.000, ratio=1.056, hyp_len=24462, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.360.0.04-1.05.0.04-1.04.1.02-2.77.0.91-2.47.pth, rkmy
BLEU = 71.36, 85.9/76.0/66.9/59.3 (BP=1.000, ratio=1.057, hyp_len=24858, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.21-1.24.0.21-1.23.0.68-1.98.0.63-1.87.pth, myrk
BLEU = 68.95, 84.9/73.9/64.3/56.0 (BP=1.000, ratio=1.053, hyp_len=24398, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.21-1.24.0.21-1.23.0.68-1.98.0.63-1.87.pth, rkmy
BLEU = 71.01, 86.2/75.7/66.3/58.7 (BP=1.000, ratio=1.038, hyp_len=24409, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.361.0.04-1.04.0.04-1.04.1.01-2.76.0.90-2.46.pth, myrk
BLEU = 70.78, 86.3/75.5/66.2/58.1 (BP=1.000, ratio=1.047, hyp_len=24257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.361.0.04-1.04.0.04-1.04.1.01-2.76.0.90-2.46.pth, rkmy
BLEU = 72.14, 86.5/76.7/67.6/60.4 (BP=1.000, ratio=1.054, hyp_len=24768, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.362.0.04-1.05.0.04-1.04.1.01-2.75.0.89-2.44.pth, myrk
BLEU = 70.55, 86.2/75.3/65.9/57.9 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.362.0.04-1.05.0.04-1.04.1.01-2.75.0.89-2.44.pth, rkmy
BLEU = 71.78, 86.5/76.5/67.3/59.7 (BP=1.000, ratio=1.053, hyp_len=24756, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.363.0.04-1.04.0.04-1.04.0.97-2.64.0.85-2.33.pth, myrk
BLEU = 69.99, 85.7/74.7/65.4/57.3 (BP=1.000, ratio=1.052, hyp_len=24369, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.363.0.04-1.04.0.04-1.04.0.97-2.64.0.85-2.33.pth, rkmy
BLEU = 71.29, 86.1/76.0/66.7/59.1 (BP=1.000, ratio=1.058, hyp_len=24863, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.364.0.04-1.04.0.04-1.04.1.02-2.76.0.85-2.34.pth, myrk
BLEU = 69.86, 85.9/74.8/65.1/56.9 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.364.0.04-1.04.0.04-1.04.1.02-2.76.0.85-2.34.pth, rkmy
BLEU = 71.36, 85.6/75.9/66.9/59.6 (BP=1.000, ratio=1.062, hyp_len=24975, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.365.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.42.pth, myrk
BLEU = 69.81, 85.8/74.6/65.1/57.0 (BP=1.000, ratio=1.053, hyp_len=24398, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.365.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.42.pth, rkmy
BLEU = 71.94, 86.5/76.5/67.5/59.9 (BP=1.000, ratio=1.051, hyp_len=24716, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.366.0.04-1.04.0.04-1.04.1.03-2.80.0.86-2.35.pth, myrk
BLEU = 70.66, 86.0/75.2/66.1/58.3 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.366.0.04-1.04.0.04-1.04.1.03-2.80.0.86-2.35.pth, rkmy
BLEU = 72.10, 86.5/76.7/67.7/60.2 (BP=1.000, ratio=1.053, hyp_len=24765, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.367.0.04-1.04.0.04-1.04.1.01-2.74.0.85-2.35.pth, myrk
BLEU = 70.49, 85.9/75.0/66.0/58.1 (BP=1.000, ratio=1.048, hyp_len=24270, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.367.0.04-1.04.0.04-1.04.1.01-2.74.0.85-2.35.pth, rkmy
BLEU = 71.74, 86.3/76.3/67.3/59.8 (BP=1.000, ratio=1.054, hyp_len=24781, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.368.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.44.pth, myrk
BLEU = 70.73, 86.2/75.4/66.2/58.2 (BP=1.000, ratio=1.048, hyp_len=24277, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.368.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.44.pth, rkmy
BLEU = 71.91, 86.3/76.4/67.5/60.1 (BP=1.000, ratio=1.055, hyp_len=24805, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.369.0.04-1.04.0.04-1.04.1.01-2.74.0.89-2.44.pth, myrk
BLEU = 69.98, 85.9/74.8/65.3/57.1 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.369.0.04-1.04.0.04-1.04.1.01-2.74.0.89-2.44.pth, rkmy
BLEU = 71.93, 86.3/76.5/67.5/60.0 (BP=1.000, ratio=1.055, hyp_len=24807, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.370.0.04-1.04.0.04-1.04.1.02-2.78.0.86-2.37.pth, myrk
BLEU = 70.92, 86.2/75.5/66.4/58.5 (BP=1.000, ratio=1.044, hyp_len=24181, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.370.0.04-1.04.0.04-1.04.1.02-2.78.0.86-2.37.pth, rkmy
BLEU = 70.97, 86.1/75.9/66.4/58.6 (BP=1.000, ratio=1.058, hyp_len=24875, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.21-1.24.0.22-1.25.0.67-1.95.0.61-1.84.pth, myrk
BLEU = 69.14, 85.2/74.0/64.4/56.3 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.21-1.24.0.22-1.25.0.67-1.95.0.61-1.84.pth, rkmy
BLEU = 68.81, 84.9/73.8/63.9/55.9 (BP=1.000, ratio=1.056, hyp_len=24814, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.371.0.04-1.04.0.04-1.04.0.99-2.69.0.86-2.36.pth, myrk
BLEU = 70.32, 86.1/75.1/65.7/57.6 (BP=1.000, ratio=1.048, hyp_len=24261, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.371.0.04-1.04.0.04-1.04.0.99-2.69.0.86-2.36.pth, rkmy
BLEU = 72.23, 86.6/76.7/67.8/60.4 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.372.0.04-1.04.0.04-1.04.1.00-2.72.0.85-2.33.pth, myrk
BLEU = 70.70, 86.2/75.3/66.1/58.3 (BP=1.000, ratio=1.045, hyp_len=24192, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.372.0.04-1.04.0.04-1.04.1.00-2.72.0.85-2.33.pth, rkmy
BLEU = 72.67, 86.7/77.0/68.3/61.1 (BP=1.000, ratio=1.052, hyp_len=24727, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.373.0.04-1.04.0.04-1.04.1.02-2.78.0.85-2.34.pth, myrk
BLEU = 70.52, 85.9/75.0/66.0/58.2 (BP=1.000, ratio=1.049, hyp_len=24290, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.373.0.04-1.04.0.04-1.04.1.02-2.78.0.85-2.34.pth, rkmy
BLEU = 71.33, 86.2/76.0/66.8/59.1 (BP=1.000, ratio=1.054, hyp_len=24783, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.374.0.04-1.04.0.04-1.04.1.03-2.79.0.87-2.39.pth, myrk
BLEU = 70.42, 85.9/75.0/65.9/57.9 (BP=1.000, ratio=1.049, hyp_len=24305, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.374.0.04-1.04.0.04-1.04.1.03-2.79.0.87-2.39.pth, rkmy
BLEU = 72.55, 86.9/77.1/68.2/60.6 (BP=1.000, ratio=1.048, hyp_len=24646, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.375.0.04-1.04.0.04-1.04.1.01-2.73.0.86-2.36.pth, myrk
BLEU = 71.49, 86.6/76.0/67.0/59.2 (BP=1.000, ratio=1.045, hyp_len=24191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.375.0.04-1.04.0.04-1.04.1.01-2.73.0.86-2.36.pth, rkmy
BLEU = 72.02, 86.5/76.6/67.6/60.0 (BP=1.000, ratio=1.053, hyp_len=24746, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.376.0.04-1.04.0.04-1.04.1.04-2.82.0.87-2.38.pth, myrk
BLEU = 69.77, 85.4/74.5/65.2/57.1 (BP=1.000, ratio=1.053, hyp_len=24378, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.376.0.04-1.04.0.04-1.04.1.04-2.82.0.87-2.38.pth, rkmy
BLEU = 71.23, 86.0/75.9/66.7/59.1 (BP=1.000, ratio=1.058, hyp_len=24874, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.377.0.04-1.04.0.04-1.04.1.01-2.75.0.85-2.35.pth, myrk
BLEU = 70.17, 85.8/74.8/65.6/57.6 (BP=1.000, ratio=1.051, hyp_len=24336, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.377.0.04-1.04.0.04-1.04.1.01-2.75.0.85-2.35.pth, rkmy
BLEU = 72.61, 86.7/77.1/68.3/60.9 (BP=1.000, ratio=1.049, hyp_len=24664, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.378.0.04-1.04.0.04-1.04.1.00-2.72.0.85-2.35.pth, myrk
BLEU = 70.57, 86.0/75.2/66.0/58.1 (BP=1.000, ratio=1.046, hyp_len=24231, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.378.0.04-1.04.0.04-1.04.1.00-2.72.0.85-2.35.pth, rkmy
BLEU = 72.09, 86.5/76.7/67.7/60.1 (BP=1.000, ratio=1.054, hyp_len=24767, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.379.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.42.pth, myrk
BLEU = 70.55, 86.1/75.2/65.9/58.0 (BP=1.000, ratio=1.049, hyp_len=24284, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.379.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.42.pth, rkmy
BLEU = 72.77, 86.9/77.2/68.4/61.1 (BP=1.000, ratio=1.050, hyp_len=24683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.380.0.05-1.05.0.04-1.04.1.01-2.74.0.91-2.47.pth, myrk
BLEU = 70.97, 86.3/75.5/66.4/58.6 (BP=1.000, ratio=1.045, hyp_len=24200, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.380.0.05-1.05.0.04-1.04.1.01-2.74.0.91-2.47.pth, rkmy
BLEU = 71.87, 86.4/76.6/67.5/59.7 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.23-1.26.0.22-1.24.0.67-1.95.0.60-1.83.pth, myrk
BLEU = 70.39, 86.0/75.2/65.8/57.7 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.23-1.26.0.22-1.24.0.67-1.95.0.60-1.83.pth, rkmy
BLEU = 68.80, 84.4/74.0/64.1/56.0 (BP=1.000, ratio=1.069, hyp_len=25121, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.381.0.04-1.04.0.04-1.04.1.01-2.73.0.86-2.37.pth, myrk
BLEU = 70.77, 86.1/75.4/66.2/58.3 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.381.0.04-1.04.0.04-1.04.1.01-2.73.0.86-2.37.pth, rkmy
BLEU = 72.50, 86.7/77.1/68.1/60.7 (BP=1.000, ratio=1.049, hyp_len=24671, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.382.0.04-1.04.0.04-1.04.1.04-2.82.0.86-2.37.pth, myrk
BLEU = 70.92, 86.2/75.5/66.4/58.5 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.382.0.04-1.04.0.04-1.04.1.04-2.82.0.86-2.37.pth, rkmy
BLEU = 71.66, 86.2/76.2/67.2/59.7 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.383.0.04-1.04.0.04-1.04.1.03-2.80.0.88-2.41.pth, myrk
BLEU = 69.86, 85.7/74.6/65.2/57.2 (BP=1.000, ratio=1.049, hyp_len=24305, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.383.0.04-1.04.0.04-1.04.1.03-2.80.0.88-2.41.pth, rkmy
BLEU = 72.56, 86.6/77.0/68.3/60.9 (BP=1.000, ratio=1.053, hyp_len=24756, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.384.0.04-1.04.0.04-1.04.1.03-2.79.0.88-2.41.pth, myrk
BLEU = 69.86, 85.8/74.7/65.2/57.0 (BP=1.000, ratio=1.051, hyp_len=24351, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.384.0.04-1.04.0.04-1.04.1.03-2.79.0.88-2.41.pth, rkmy
BLEU = 72.48, 86.6/76.9/68.1/60.8 (BP=1.000, ratio=1.051, hyp_len=24707, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.385.0.04-1.04.0.04-1.04.1.03-2.80.0.89-2.43.pth, myrk
BLEU = 70.27, 85.9/75.0/65.7/57.6 (BP=1.000, ratio=1.050, hyp_len=24309, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.385.0.04-1.04.0.04-1.04.1.03-2.80.0.89-2.43.pth, rkmy
BLEU = 72.54, 86.5/76.8/68.2/61.1 (BP=1.000, ratio=1.052, hyp_len=24722, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.386.0.04-1.04.0.04-1.04.1.00-2.71.0.85-2.33.pth, myrk
BLEU = 70.69, 86.0/75.4/66.2/58.2 (BP=1.000, ratio=1.050, hyp_len=24313, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.386.0.04-1.04.0.04-1.04.1.00-2.71.0.85-2.33.pth, rkmy
BLEU = 71.89, 86.3/76.5/67.5/60.0 (BP=1.000, ratio=1.055, hyp_len=24802, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.387.0.04-1.04.0.04-1.04.1.00-2.73.0.90-2.45.pth, myrk
BLEU = 70.85, 86.3/75.6/66.3/58.2 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.387.0.04-1.04.0.04-1.04.1.00-2.73.0.90-2.45.pth, rkmy
BLEU = 71.89, 86.4/76.5/67.4/60.0 (BP=1.000, ratio=1.053, hyp_len=24761, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.388.0.04-1.05.0.04-1.04.0.99-2.69.0.88-2.42.pth, myrk
BLEU = 69.90, 85.7/74.7/65.2/57.2 (BP=1.000, ratio=1.052, hyp_len=24354, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.388.0.04-1.05.0.04-1.04.0.99-2.69.0.88-2.42.pth, rkmy
BLEU = 71.74, 86.2/76.3/67.3/59.9 (BP=1.000, ratio=1.059, hyp_len=24885, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.389.0.04-1.04.0.04-1.04.1.01-2.73.0.87-2.38.pth, myrk
BLEU = 70.74, 86.0/75.4/66.2/58.4 (BP=1.000, ratio=1.049, hyp_len=24286, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.389.0.04-1.04.0.04-1.04.1.01-2.73.0.87-2.38.pth, rkmy
BLEU = 71.90, 86.2/76.5/67.5/60.1 (BP=1.000, ratio=1.054, hyp_len=24781, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.390.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.40.pth, myrk
BLEU = 70.55, 86.0/75.2/66.0/58.1 (BP=1.000, ratio=1.048, hyp_len=24264, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.390.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.40.pth, rkmy
BLEU = 71.69, 86.3/76.4/67.3/59.6 (BP=1.000, ratio=1.054, hyp_len=24788, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.23.0.66-1.93.0.60-1.82.pth, myrk
BLEU = 69.81, 85.8/74.7/65.1/56.9 (BP=1.000, ratio=1.043, hyp_len=24155, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.23.0.66-1.93.0.60-1.82.pth, rkmy
BLEU = 68.65, 84.8/73.7/63.8/55.7 (BP=1.000, ratio=1.061, hyp_len=24938, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.391.0.04-1.04.0.04-1.04.1.05-2.87.0.87-2.39.pth, myrk
BLEU = 70.42, 86.0/75.2/65.9/57.7 (BP=1.000, ratio=1.051, hyp_len=24330, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.391.0.04-1.04.0.04-1.04.1.05-2.87.0.87-2.39.pth, rkmy
BLEU = 72.58, 86.7/77.1/68.3/60.8 (BP=1.000, ratio=1.048, hyp_len=24649, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.392.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, myrk
BLEU = 70.41, 86.0/75.1/65.8/57.9 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.392.0.04-1.04.0.04-1.04.1.00-2.72.0.87-2.39.pth, rkmy
BLEU = 71.65, 86.3/76.3/67.2/59.6 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.393.0.04-1.04.0.04-1.04.0.98-2.66.0.91-2.48.pth, myrk
BLEU = 71.20, 86.3/75.7/66.7/58.9 (BP=1.000, ratio=1.048, hyp_len=24261, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.393.0.04-1.04.0.04-1.04.0.98-2.66.0.91-2.48.pth, rkmy
BLEU = 71.75, 86.2/76.3/67.3/59.9 (BP=1.000, ratio=1.055, hyp_len=24793, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.394.0.04-1.04.0.04-1.04.1.02-2.76.0.89-2.42.pth, myrk
BLEU = 70.40, 85.8/75.1/65.8/57.9 (BP=1.000, ratio=1.050, hyp_len=24308, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.394.0.04-1.04.0.04-1.04.1.02-2.76.0.89-2.42.pth, rkmy
BLEU = 71.05, 85.8/75.8/66.5/58.9 (BP=1.000, ratio=1.060, hyp_len=24926, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.395.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.43.pth, myrk
BLEU = 70.44, 86.1/75.2/65.8/57.8 (BP=1.000, ratio=1.048, hyp_len=24270, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.395.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.43.pth, rkmy
BLEU = 70.93, 85.8/75.7/66.4/58.7 (BP=1.000, ratio=1.060, hyp_len=24908, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.396.0.04-1.04.0.04-1.04.1.01-2.75.0.88-2.42.pth, myrk
BLEU = 70.12, 85.8/74.8/65.5/57.5 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.396.0.04-1.04.0.04-1.04.1.01-2.75.0.88-2.42.pth, rkmy
BLEU = 72.58, 86.8/77.1/68.2/60.8 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.397.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.41.pth, myrk
BLEU = 70.88, 86.2/75.5/66.3/58.5 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.397.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.41.pth, rkmy
BLEU = 72.58, 86.9/77.1/68.1/60.7 (BP=1.000, ratio=1.048, hyp_len=24648, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.398.0.04-1.04.0.04-1.04.1.01-2.74.0.87-2.39.pth, myrk
BLEU = 70.75, 86.1/75.4/66.2/58.3 (BP=1.000, ratio=1.048, hyp_len=24280, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.398.0.04-1.04.0.04-1.04.1.01-2.74.0.87-2.39.pth, rkmy
BLEU = 71.95, 86.4/76.6/67.5/60.0 (BP=1.000, ratio=1.054, hyp_len=24788, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.399.0.04-1.04.0.04-1.04.1.02-2.76.0.88-2.42.pth, myrk
BLEU = 70.85, 86.4/75.5/66.2/58.3 (BP=1.000, ratio=1.046, hyp_len=24223, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.399.0.04-1.04.0.04-1.04.1.02-2.76.0.88-2.42.pth, rkmy
BLEU = 72.15, 86.6/76.6/67.7/60.4 (BP=1.000, ratio=1.053, hyp_len=24754, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.400.0.04-1.04.0.04-1.04.1.01-2.75.0.88-2.42.pth, myrk
BLEU = 70.83, 86.2/75.5/66.3/58.4 (BP=1.000, ratio=1.050, hyp_len=24314, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.400.0.04-1.04.0.04-1.04.1.01-2.75.0.88-2.42.pth, rkmy
BLEU = 71.42, 86.0/76.0/67.0/59.4 (BP=1.000, ratio=1.058, hyp_len=24868, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.21-1.23.0.66-1.94.0.61-1.84.pth, myrk
BLEU = 69.64, 85.6/74.5/64.9/56.8 (BP=1.000, ratio=1.041, hyp_len=24105, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.21-1.23.0.66-1.94.0.61-1.84.pth, rkmy
BLEU = 68.64, 84.7/73.7/63.8/55.8 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.401.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.44.pth, myrk
BLEU = 70.80, 86.3/75.6/66.2/58.2 (BP=1.000, ratio=1.046, hyp_len=24217, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.401.0.04-1.04.0.04-1.04.1.01-2.75.0.89-2.44.pth, rkmy
BLEU = 72.46, 86.6/76.7/68.1/60.9 (BP=1.000, ratio=1.049, hyp_len=24657, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.402.0.04-1.04.0.04-1.04.1.00-2.73.0.91-2.49.pth, myrk
BLEU = 70.77, 86.2/75.4/66.2/58.3 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.402.0.04-1.04.0.04-1.04.1.00-2.73.0.91-2.49.pth, rkmy
BLEU = 72.52, 86.8/77.1/68.1/60.7 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.403.0.04-1.04.0.04-1.04.1.03-2.79.0.86-2.37.pth, myrk
BLEU = 69.77, 85.6/74.6/65.1/56.9 (BP=1.000, ratio=1.052, hyp_len=24356, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.403.0.04-1.04.0.04-1.04.1.03-2.79.0.86-2.37.pth, rkmy
BLEU = 72.26, 86.6/76.8/67.9/60.4 (BP=1.000, ratio=1.051, hyp_len=24709, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.404.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.41.pth, myrk
BLEU = 70.41, 86.1/75.2/65.9/57.6 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.404.0.04-1.04.0.04-1.04.1.03-2.81.0.88-2.41.pth, rkmy
BLEU = 71.96, 86.5/76.5/67.5/60.0 (BP=1.000, ratio=1.055, hyp_len=24811, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.405.0.04-1.04.0.04-1.04.1.03-2.80.0.86-2.36.pth, myrk
BLEU = 70.49, 85.9/75.2/66.0/57.9 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.405.0.04-1.04.0.04-1.04.1.03-2.80.0.86-2.36.pth, rkmy
BLEU = 72.34, 86.5/76.8/68.0/60.7 (BP=1.000, ratio=1.052, hyp_len=24736, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.406.0.04-1.04.0.04-1.04.1.03-2.80.0.85-2.34.pth, myrk
BLEU = 72.09, 86.9/76.6/67.7/59.9 (BP=1.000, ratio=1.039, hyp_len=24069, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.406.0.04-1.04.0.04-1.04.1.03-2.80.0.85-2.34.pth, rkmy
BLEU = 72.48, 86.6/76.9/68.2/60.8 (BP=1.000, ratio=1.050, hyp_len=24689, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.407.0.04-1.04.0.04-1.04.1.01-2.74.0.85-2.35.pth, myrk
BLEU = 70.58, 86.0/75.3/66.0/58.0 (BP=1.000, ratio=1.050, hyp_len=24313, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.407.0.04-1.04.0.04-1.04.1.01-2.74.0.85-2.35.pth, rkmy
BLEU = 71.43, 86.1/76.2/67.1/59.2 (BP=1.000, ratio=1.058, hyp_len=24864, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.408.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.39.pth, myrk
BLEU = 70.82, 86.1/75.5/66.3/58.4 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.408.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.39.pth, rkmy
BLEU = 72.34, 86.6/76.8/67.9/60.6 (BP=1.000, ratio=1.053, hyp_len=24757, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.409.0.04-1.04.0.04-1.04.1.02-2.76.0.87-2.39.pth, myrk
BLEU = 70.33, 85.9/75.1/65.8/57.6 (BP=1.000, ratio=1.051, hyp_len=24342, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.409.0.04-1.04.0.04-1.04.1.02-2.76.0.87-2.39.pth, rkmy
BLEU = 71.91, 86.5/76.4/67.5/60.0 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.410.0.04-1.04.0.04-1.04.1.02-2.79.0.83-2.29.pth, myrk
BLEU = 70.46, 85.9/75.2/65.9/57.9 (BP=1.000, ratio=1.050, hyp_len=24311, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.410.0.04-1.04.0.04-1.04.1.02-2.79.0.83-2.29.pth, rkmy
BLEU = 72.68, 86.9/77.2/68.3/60.9 (BP=1.000, ratio=1.051, hyp_len=24700, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.23.0.20-1.23.0.68-1.97.0.62-1.85.pth, myrk
BLEU = 69.63, 85.3/74.4/65.0/57.0 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.23.0.20-1.23.0.68-1.97.0.62-1.85.pth, rkmy
BLEU = 69.63, 85.2/74.5/64.9/57.1 (BP=1.000, ratio=1.055, hyp_len=24791, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.411.0.04-1.04.0.04-1.04.1.04-2.83.0.85-2.33.pth, myrk
BLEU = 70.92, 86.2/75.6/66.4/58.4 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.411.0.04-1.04.0.04-1.04.1.04-2.83.0.85-2.33.pth, rkmy
BLEU = 72.70, 86.8/77.1/68.4/61.0 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.412.0.04-1.04.0.04-1.04.1.01-2.76.0.87-2.40.pth, myrk
BLEU = 71.08, 86.4/75.7/66.6/58.6 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.412.0.04-1.04.0.04-1.04.1.01-2.76.0.87-2.40.pth, rkmy
BLEU = 73.05, 87.0/77.4/68.8/61.5 (BP=1.000, ratio=1.046, hyp_len=24599, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.413.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.38.pth, myrk
BLEU = 70.12, 85.7/74.9/65.6/57.5 (BP=1.000, ratio=1.053, hyp_len=24390, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.413.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.38.pth, rkmy
BLEU = 70.94, 85.8/75.7/66.5/58.6 (BP=1.000, ratio=1.060, hyp_len=24931, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.414.0.04-1.04.0.04-1.04.1.05-2.85.0.85-2.35.pth, myrk
BLEU = 70.65, 85.8/75.2/66.2/58.4 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.414.0.04-1.04.0.04-1.04.1.05-2.85.0.85-2.35.pth, rkmy
BLEU = 71.20, 85.8/75.8/66.8/59.2 (BP=1.000, ratio=1.061, hyp_len=24943, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.415.0.04-1.04.0.04-1.04.1.04-2.84.0.89-2.43.pth, myrk
BLEU = 70.71, 85.8/75.3/66.2/58.4 (BP=1.000, ratio=1.049, hyp_len=24306, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.415.0.04-1.04.0.04-1.04.1.04-2.84.0.89-2.43.pth, rkmy
BLEU = 72.15, 86.5/76.6/67.7/60.4 (BP=1.000, ratio=1.053, hyp_len=24750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.416.0.04-1.04.0.04-1.04.1.03-2.81.0.87-2.38.pth, myrk
BLEU = 70.11, 85.8/74.9/65.6/57.4 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.416.0.04-1.04.0.04-1.04.1.03-2.81.0.87-2.38.pth, rkmy
BLEU = 72.49, 86.7/77.0/68.1/60.7 (BP=1.000, ratio=1.050, hyp_len=24685, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.417.0.04-1.04.0.04-1.04.1.02-2.79.0.87-2.38.pth, myrk
BLEU = 70.52, 86.0/75.2/66.0/57.9 (BP=1.000, ratio=1.051, hyp_len=24330, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.417.0.04-1.04.0.04-1.04.1.02-2.79.0.87-2.38.pth, rkmy
BLEU = 72.77, 86.6/77.2/68.5/61.2 (BP=1.000, ratio=1.051, hyp_len=24697, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.418.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.38.pth, myrk
BLEU = 70.88, 86.1/75.5/66.4/58.5 (BP=1.000, ratio=1.050, hyp_len=24319, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.418.0.04-1.04.0.04-1.04.1.04-2.83.0.87-2.38.pth, rkmy
BLEU = 71.15, 85.8/75.8/66.7/59.1 (BP=1.000, ratio=1.061, hyp_len=24944, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.419.0.04-1.04.0.04-1.04.1.05-2.85.0.85-2.34.pth, myrk
BLEU = 70.83, 85.9/75.4/66.4/58.5 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.419.0.04-1.04.0.04-1.04.1.05-2.85.0.85-2.34.pth, rkmy
BLEU = 72.25, 86.7/76.9/67.9/60.3 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.420.0.04-1.04.0.04-1.04.1.03-2.81.0.87-2.38.pth, myrk
BLEU = 70.97, 86.2/75.5/66.5/58.6 (BP=1.000, ratio=1.047, hyp_len=24248, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.420.0.04-1.04.0.04-1.04.1.03-2.81.0.87-2.38.pth, rkmy
BLEU = 72.40, 86.7/77.1/68.0/60.4 (BP=1.000, ratio=1.053, hyp_len=24748, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.20-1.22.0.68-1.98.0.65-1.92.pth, myrk
BLEU = 69.27, 85.1/74.1/64.6/56.5 (BP=1.000, ratio=1.049, hyp_len=24305, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.20-1.22.0.68-1.98.0.65-1.92.pth, rkmy
BLEU = 69.48, 85.1/74.4/64.7/56.9 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.421.0.04-1.04.0.04-1.04.1.06-2.87.0.88-2.40.pth, myrk
BLEU = 70.75, 86.3/75.4/66.1/58.2 (BP=1.000, ratio=1.048, hyp_len=24265, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.421.0.04-1.04.0.04-1.04.1.06-2.87.0.88-2.40.pth, rkmy
BLEU = 71.67, 86.5/76.5/67.2/59.4 (BP=1.000, ratio=1.053, hyp_len=24753, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.422.0.04-1.04.0.04-1.04.1.03-2.80.0.88-2.41.pth, myrk
BLEU = 70.98, 86.3/75.5/66.4/58.6 (BP=1.000, ratio=1.045, hyp_len=24193, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.422.0.04-1.04.0.04-1.04.1.03-2.80.0.88-2.41.pth, rkmy
BLEU = 71.82, 86.3/76.5/67.4/59.7 (BP=1.000, ratio=1.054, hyp_len=24781, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.423.0.04-1.04.0.04-1.04.1.03-2.80.0.90-2.45.pth, myrk
BLEU = 70.86, 86.1/75.4/66.4/58.6 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.423.0.04-1.04.0.04-1.04.1.03-2.80.0.90-2.45.pth, rkmy
BLEU = 71.67, 86.4/76.4/67.2/59.4 (BP=1.000, ratio=1.055, hyp_len=24813, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.424.0.04-1.04.0.04-1.04.1.02-2.76.0.89-2.44.pth, myrk
BLEU = 70.06, 85.5/74.7/65.5/57.5 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.424.0.04-1.04.0.04-1.04.1.02-2.76.0.89-2.44.pth, rkmy
BLEU = 73.09, 87.0/77.5/68.8/61.5 (BP=1.000, ratio=1.048, hyp_len=24642, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.425.0.04-1.04.0.04-1.04.1.03-2.81.0.86-2.36.pth, myrk
BLEU = 70.45, 86.2/75.2/65.8/57.7 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.425.0.04-1.04.0.04-1.04.1.03-2.81.0.86-2.36.pth, rkmy
BLEU = 71.65, 86.3/76.3/67.2/59.6 (BP=1.000, ratio=1.056, hyp_len=24833, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.426.0.04-1.04.0.04-1.04.1.05-2.86.0.88-2.40.pth, myrk
BLEU = 70.99, 86.3/75.6/66.5/58.5 (BP=1.000, ratio=1.047, hyp_len=24245, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.426.0.04-1.04.0.04-1.04.1.05-2.86.0.88-2.40.pth, rkmy
BLEU = 73.53, 87.3/78.0/69.3/62.0 (BP=1.000, ratio=1.046, hyp_len=24590, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.427.0.04-1.04.0.04-1.04.1.06-2.88.0.89-2.44.pth, myrk
BLEU = 70.09, 85.9/74.8/65.4/57.4 (BP=1.000, ratio=1.048, hyp_len=24268, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.427.0.04-1.04.0.04-1.04.1.06-2.88.0.89-2.44.pth, rkmy
BLEU = 73.10, 86.9/77.5/68.8/61.6 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.428.0.04-1.04.0.04-1.04.1.03-2.79.0.89-2.43.pth, myrk
BLEU = 70.86, 86.2/75.5/66.3/58.4 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.428.0.04-1.04.0.04-1.04.1.03-2.79.0.89-2.43.pth, rkmy
BLEU = 73.10, 87.0/77.4/68.7/61.7 (BP=1.000, ratio=1.048, hyp_len=24626, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.429.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.41.pth, myrk
BLEU = 70.96, 86.4/75.6/66.4/58.4 (BP=1.000, ratio=1.047, hyp_len=24248, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.429.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.41.pth, rkmy
BLEU = 72.59, 86.9/77.2/68.2/60.7 (BP=1.000, ratio=1.048, hyp_len=24648, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.430.0.04-1.04.0.04-1.04.1.01-2.75.0.90-2.46.pth, myrk
BLEU = 70.95, 86.4/75.6/66.4/58.4 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.430.0.04-1.04.0.04-1.04.1.01-2.75.0.90-2.46.pth, rkmy
BLEU = 71.71, 86.1/76.4/67.3/59.7 (BP=1.000, ratio=1.057, hyp_len=24853, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.19-1.21.0.19-1.20.0.70-2.01.0.65-1.91.pth, myrk
BLEU = 70.13, 86.0/75.0/65.5/57.3 (BP=1.000, ratio=1.040, hyp_len=24096, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.19-1.21.0.19-1.20.0.70-2.01.0.65-1.91.pth, rkmy
BLEU = 69.10, 84.9/74.1/64.4/56.3 (BP=1.000, ratio=1.055, hyp_len=24812, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.431.0.04-1.04.0.04-1.04.1.03-2.81.0.86-2.37.pth, myrk
BLEU = 71.06, 86.3/75.7/66.6/58.7 (BP=1.000, ratio=1.048, hyp_len=24282, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.431.0.04-1.04.0.04-1.04.1.03-2.81.0.86-2.37.pth, rkmy
BLEU = 72.30, 86.7/76.9/67.9/60.4 (BP=1.000, ratio=1.053, hyp_len=24747, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.432.0.04-1.04.0.04-1.04.1.02-2.78.0.86-2.36.pth, myrk
BLEU = 70.90, 86.2/75.5/66.4/58.5 (BP=1.000, ratio=1.049, hyp_len=24284, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.432.0.04-1.04.0.04-1.04.1.02-2.78.0.86-2.36.pth, rkmy
BLEU = 71.60, 86.4/76.3/67.1/59.4 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.433.0.04-1.04.0.04-1.04.1.04-2.84.0.87-2.38.pth, myrk
BLEU = 70.91, 86.3/75.4/66.4/58.5 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.433.0.04-1.04.0.04-1.04.1.04-2.84.0.87-2.38.pth, rkmy
BLEU = 73.04, 87.0/77.5/68.8/61.4 (BP=1.000, ratio=1.049, hyp_len=24658, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.434.0.04-1.04.0.04-1.04.1.05-2.87.0.84-2.32.pth, myrk
BLEU = 70.31, 86.0/75.1/65.8/57.6 (BP=1.000, ratio=1.052, hyp_len=24373, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.434.0.04-1.04.0.04-1.04.1.05-2.87.0.84-2.32.pth, rkmy
BLEU = 71.66, 86.3/76.4/67.2/59.5 (BP=1.000, ratio=1.054, hyp_len=24785, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.435.0.04-1.04.0.04-1.04.1.05-2.87.0.86-2.37.pth, myrk
BLEU = 70.32, 85.8/75.1/65.9/57.6 (BP=1.000, ratio=1.053, hyp_len=24388, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.435.0.04-1.04.0.04-1.04.1.05-2.87.0.86-2.37.pth, rkmy
BLEU = 72.56, 86.9/77.1/68.2/60.7 (BP=1.000, ratio=1.049, hyp_len=24650, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.436.0.04-1.04.0.04-1.04.1.04-2.84.0.84-2.32.pth, myrk
BLEU = 70.44, 86.1/75.2/65.9/57.7 (BP=1.000, ratio=1.048, hyp_len=24262, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.436.0.04-1.04.0.04-1.04.1.04-2.84.0.84-2.32.pth, rkmy
BLEU = 72.29, 86.8/77.0/67.8/60.3 (BP=1.000, ratio=1.049, hyp_len=24650, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.437.0.04-1.04.0.04-1.04.1.06-2.88.0.85-2.34.pth, myrk
BLEU = 71.38, 86.4/75.9/67.0/59.1 (BP=1.000, ratio=1.045, hyp_len=24206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.437.0.04-1.04.0.04-1.04.1.06-2.88.0.85-2.34.pth, rkmy
BLEU = 72.51, 86.8/77.0/68.1/60.7 (BP=1.000, ratio=1.050, hyp_len=24676, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.438.0.04-1.04.0.04-1.04.1.08-2.93.0.87-2.39.pth, myrk
BLEU = 70.48, 86.2/75.3/65.9/57.7 (BP=1.000, ratio=1.049, hyp_len=24299, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.438.0.04-1.04.0.04-1.04.1.08-2.93.0.87-2.39.pth, rkmy
BLEU = 73.01, 87.1/77.5/68.6/61.4 (BP=1.000, ratio=1.046, hyp_len=24596, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.439.0.04-1.04.0.04-1.04.1.07-2.91.0.86-2.37.pth, myrk
BLEU = 71.11, 86.1/75.5/66.7/59.0 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.439.0.04-1.04.0.04-1.04.1.07-2.91.0.86-2.37.pth, rkmy
BLEU = 72.84, 86.7/77.2/68.5/61.3 (BP=1.000, ratio=1.049, hyp_len=24672, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.440.0.04-1.04.0.04-1.04.1.02-2.76.0.87-2.39.pth, myrk
BLEU = 70.52, 86.0/75.2/66.0/58.0 (BP=1.000, ratio=1.050, hyp_len=24318, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.440.0.04-1.04.0.04-1.04.1.02-2.76.0.87-2.39.pth, rkmy
BLEU = 72.91, 86.9/77.4/68.6/61.3 (BP=1.000, ratio=1.049, hyp_len=24664, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.18-1.20.0.18-1.20.0.69-1.99.0.63-1.87.pth, myrk
BLEU = 70.01, 85.5/74.6/65.4/57.6 (BP=1.000, ratio=1.042, hyp_len=24142, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.18-1.20.0.18-1.20.0.69-1.99.0.63-1.87.pth, rkmy
BLEU = 68.80, 84.1/73.6/64.1/56.5 (BP=1.000, ratio=1.069, hyp_len=25142, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.441.0.04-1.04.0.04-1.04.1.09-2.97.0.86-2.37.pth, myrk
BLEU = 70.25, 85.9/75.0/65.7/57.5 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.441.0.04-1.04.0.04-1.04.1.09-2.97.0.86-2.37.pth, rkmy
BLEU = 72.21, 86.5/76.7/67.8/60.4 (BP=1.000, ratio=1.051, hyp_len=24714, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.442.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.42.pth, myrk
BLEU = 71.34, 86.5/75.9/66.9/59.0 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.442.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.42.pth, rkmy
BLEU = 72.44, 86.6/76.9/68.1/60.7 (BP=1.000, ratio=1.052, hyp_len=24726, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.443.0.04-1.04.0.04-1.04.1.03-2.79.0.89-2.43.pth, myrk
BLEU = 70.73, 85.9/75.3/66.2/58.4 (BP=1.000, ratio=1.048, hyp_len=24279, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.443.0.04-1.04.0.04-1.04.1.03-2.79.0.89-2.43.pth, rkmy
BLEU = 71.62, 86.0/76.3/67.2/59.7 (BP=1.000, ratio=1.059, hyp_len=24885, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.444.0.04-1.04.0.04-1.04.1.01-2.73.0.92-2.50.pth, myrk
BLEU = 70.58, 86.1/75.3/66.0/58.0 (BP=1.000, ratio=1.047, hyp_len=24258, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.444.0.04-1.04.0.04-1.04.1.01-2.73.0.92-2.50.pth, rkmy
BLEU = 73.36, 87.2/77.8/69.1/61.8 (BP=1.000, ratio=1.046, hyp_len=24588, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.445.0.04-1.04.0.04-1.04.1.01-2.76.0.88-2.42.pth, myrk
BLEU = 71.09, 86.3/75.7/66.6/58.8 (BP=1.000, ratio=1.048, hyp_len=24270, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.445.0.04-1.04.0.04-1.04.1.01-2.76.0.88-2.42.pth, rkmy
BLEU = 72.25, 86.9/76.9/67.7/60.2 (BP=1.000, ratio=1.049, hyp_len=24662, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.446.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.46.pth, myrk
BLEU = 70.38, 85.9/75.0/65.9/57.8 (BP=1.000, ratio=1.049, hyp_len=24286, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.446.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.46.pth, rkmy
BLEU = 72.34, 86.8/77.0/67.9/60.3 (BP=1.000, ratio=1.052, hyp_len=24731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.447.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.41.pth, myrk
BLEU = 70.63, 86.0/75.2/66.1/58.2 (BP=1.000, ratio=1.051, hyp_len=24339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.447.0.04-1.04.0.04-1.04.1.02-2.78.0.88-2.41.pth, rkmy
BLEU = 72.12, 86.5/76.8/67.7/60.2 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.448.0.04-1.04.0.04-1.04.1.04-2.84.0.90-2.45.pth, myrk
BLEU = 70.92, 86.2/75.6/66.4/58.4 (BP=1.000, ratio=1.049, hyp_len=24288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.448.0.04-1.04.0.04-1.04.1.04-2.84.0.90-2.45.pth, rkmy
BLEU = 72.42, 86.9/77.1/68.0/60.4 (BP=1.000, ratio=1.049, hyp_len=24668, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.449.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.41.pth, myrk
BLEU = 70.62, 86.0/75.3/66.1/58.0 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.449.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.41.pth, rkmy
BLEU = 73.05, 87.1/77.5/68.7/61.4 (BP=1.000, ratio=1.047, hyp_len=24612, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.450.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.42.pth, myrk
BLEU = 70.02, 85.8/74.9/65.4/57.2 (BP=1.000, ratio=1.052, hyp_len=24354, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.450.0.04-1.04.0.04-1.04.1.04-2.83.0.88-2.42.pth, rkmy
BLEU = 72.02, 86.7/76.8/67.5/59.9 (BP=1.000, ratio=1.052, hyp_len=24739, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.20.0.73-2.08.0.62-1.86.pth, myrk
BLEU = 69.03, 84.8/73.8/64.5/56.2 (BP=1.000, ratio=1.059, hyp_len=24526, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.20.0.73-2.08.0.62-1.86.pth, rkmy
BLEU = 70.84, 85.9/75.7/66.2/58.4 (BP=1.000, ratio=1.048, hyp_len=24641, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.451.0.04-1.04.0.04-1.04.1.06-2.89.0.91-2.49.pth, myrk
BLEU = 71.04, 86.3/75.7/66.6/58.6 (BP=1.000, ratio=1.044, hyp_len=24182, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.451.0.04-1.04.0.04-1.04.1.06-2.89.0.91-2.49.pth, rkmy
BLEU = 72.23, 86.6/76.8/67.8/60.4 (BP=1.000, ratio=1.050, hyp_len=24685, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.452.0.04-1.04.0.04-1.04.1.02-2.78.0.92-2.50.pth, myrk
BLEU = 70.98, 86.4/75.7/66.5/58.4 (BP=1.000, ratio=1.047, hyp_len=24247, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.452.0.04-1.04.0.04-1.04.1.02-2.78.0.92-2.50.pth, rkmy
BLEU = 72.38, 86.7/76.9/68.0/60.5 (BP=1.000, ratio=1.051, hyp_len=24707, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.453.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.47.pth, myrk
BLEU = 70.82, 86.0/75.4/66.3/58.5 (BP=1.000, ratio=1.050, hyp_len=24316, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.453.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.47.pth, rkmy
BLEU = 73.04, 87.0/77.5/68.8/61.4 (BP=1.000, ratio=1.050, hyp_len=24680, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.454.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.46.pth, myrk
BLEU = 70.72, 85.8/75.2/66.2/58.5 (BP=1.000, ratio=1.049, hyp_len=24288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.454.0.04-1.04.0.04-1.04.1.01-2.74.0.90-2.46.pth, rkmy
BLEU = 72.38, 86.6/76.9/68.0/60.7 (BP=1.000, ratio=1.052, hyp_len=24740, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.455.0.04-1.04.0.03-1.04.1.06-2.87.0.91-2.47.pth, myrk
BLEU = 69.98, 85.7/74.6/65.3/57.4 (BP=1.000, ratio=1.053, hyp_len=24395, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.455.0.04-1.04.0.03-1.04.1.06-2.87.0.91-2.47.pth, rkmy
BLEU = 72.73, 86.8/77.2/68.4/61.0 (BP=1.000, ratio=1.051, hyp_len=24703, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.456.0.04-1.04.0.04-1.04.1.05-2.86.0.93-2.53.pth, myrk
BLEU = 71.79, 86.7/76.3/67.3/59.6 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.456.0.04-1.04.0.04-1.04.1.05-2.86.0.93-2.53.pth, rkmy
BLEU = 72.49, 86.8/77.0/68.1/60.7 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.457.0.04-1.04.0.04-1.04.1.01-2.75.0.92-2.50.pth, myrk
BLEU = 70.50, 86.0/75.1/65.9/58.0 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.457.0.04-1.04.0.04-1.04.1.01-2.75.0.92-2.50.pth, rkmy
BLEU = 71.29, 86.0/76.1/66.9/59.0 (BP=1.000, ratio=1.058, hyp_len=24865, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.458.0.04-1.04.0.03-1.04.1.03-2.80.0.89-2.43.pth, myrk
BLEU = 70.95, 86.3/75.4/66.4/58.6 (BP=1.000, ratio=1.045, hyp_len=24193, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.458.0.04-1.04.0.03-1.04.1.03-2.80.0.89-2.43.pth, rkmy
BLEU = 72.98, 87.0/77.4/68.7/61.4 (BP=1.000, ratio=1.048, hyp_len=24643, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.459.0.04-1.04.0.04-1.04.1.01-2.73.0.88-2.41.pth, myrk
BLEU = 70.93, 86.2/75.5/66.5/58.5 (BP=1.000, ratio=1.048, hyp_len=24283, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.459.0.04-1.04.0.04-1.04.1.01-2.73.0.88-2.41.pth, rkmy
BLEU = 72.08, 86.5/76.6/67.7/60.2 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.460.0.04-1.04.0.04-1.04.1.03-2.79.0.88-2.41.pth, myrk
BLEU = 70.91, 86.2/75.5/66.4/58.5 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.460.0.04-1.04.0.04-1.04.1.03-2.79.0.88-2.41.pth, rkmy
BLEU = 72.53, 86.6/77.0/68.1/60.9 (BP=1.000, ratio=1.052, hyp_len=24732, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.17-1.19.0.70-2.00.0.65-1.91.pth, myrk
BLEU = 70.97, 86.5/75.5/66.4/58.5 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.17-1.19.0.70-2.00.0.65-1.91.pth, rkmy
BLEU = 69.73, 85.2/74.6/65.0/57.2 (BP=1.000, ratio=1.056, hyp_len=24832, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.461.0.04-1.04.0.04-1.04.1.03-2.80.0.89-2.44.pth, myrk
BLEU = 70.14, 85.7/74.9/65.6/57.5 (BP=1.000, ratio=1.053, hyp_len=24388, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.461.0.04-1.04.0.04-1.04.1.03-2.80.0.89-2.44.pth, rkmy
BLEU = 72.36, 86.6/77.0/68.0/60.4 (BP=1.000, ratio=1.055, hyp_len=24808, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.462.0.04-1.04.0.04-1.04.1.02-2.78.0.89-2.43.pth, myrk
BLEU = 70.61, 86.0/75.3/66.1/58.0 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.462.0.04-1.04.0.04-1.04.1.02-2.78.0.89-2.43.pth, rkmy
BLEU = 72.66, 86.8/77.1/68.3/60.9 (BP=1.000, ratio=1.049, hyp_len=24669, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.463.0.04-1.04.0.04-1.04.1.02-2.77.0.93-2.53.pth, myrk
BLEU = 70.66, 86.2/75.4/66.1/58.0 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.463.0.04-1.04.0.04-1.04.1.02-2.77.0.93-2.53.pth, rkmy
BLEU = 72.28, 86.4/76.7/67.9/60.6 (BP=1.000, ratio=1.055, hyp_len=24806, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.464.0.04-1.04.0.04-1.04.1.03-2.81.0.90-2.45.pth, myrk
BLEU = 69.82, 85.7/74.7/65.2/56.9 (BP=1.000, ratio=1.053, hyp_len=24385, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.464.0.04-1.04.0.04-1.04.1.03-2.81.0.90-2.45.pth, rkmy
BLEU = 71.07, 85.8/75.8/66.6/58.9 (BP=1.000, ratio=1.061, hyp_len=24942, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.465.0.04-1.04.0.04-1.04.1.00-2.72.0.89-2.43.pth, myrk
BLEU = 71.36, 86.5/76.0/66.9/59.0 (BP=1.000, ratio=1.041, hyp_len=24117, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.465.0.04-1.04.0.04-1.04.1.00-2.72.0.89-2.43.pth, rkmy
BLEU = 71.40, 86.2/76.1/66.9/59.2 (BP=1.000, ratio=1.058, hyp_len=24869, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.466.0.04-1.04.0.04-1.04.1.01-2.75.0.87-2.38.pth, myrk
BLEU = 71.06, 86.3/75.6/66.6/58.7 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.466.0.04-1.04.0.04-1.04.1.01-2.75.0.87-2.38.pth, rkmy
BLEU = 72.01, 86.4/76.6/67.6/60.1 (BP=1.000, ratio=1.054, hyp_len=24772, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.467.0.04-1.04.0.04-1.04.1.00-2.71.0.89-2.43.pth, myrk
BLEU = 70.75, 86.2/75.4/66.2/58.2 (BP=1.000, ratio=1.047, hyp_len=24246, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.467.0.04-1.04.0.04-1.04.1.00-2.71.0.89-2.43.pth, rkmy
BLEU = 72.45, 86.6/76.9/68.1/60.7 (BP=1.000, ratio=1.053, hyp_len=24755, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.468.0.04-1.04.0.03-1.04.1.01-2.75.0.88-2.41.pth, myrk
BLEU = 70.50, 85.9/75.2/66.0/57.9 (BP=1.000, ratio=1.051, hyp_len=24349, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.468.0.04-1.04.0.03-1.04.1.01-2.75.0.88-2.41.pth, rkmy
BLEU = 72.88, 87.0/77.4/68.6/61.1 (BP=1.000, ratio=1.049, hyp_len=24672, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.469.0.04-1.04.0.04-1.04.1.05-2.84.0.88-2.41.pth, myrk
BLEU = 69.89, 85.6/74.8/65.3/57.1 (BP=1.000, ratio=1.055, hyp_len=24424, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.469.0.04-1.04.0.04-1.04.1.05-2.84.0.88-2.41.pth, rkmy
BLEU = 72.22, 86.6/76.8/67.8/60.3 (BP=1.000, ratio=1.051, hyp_len=24711, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.470.0.03-1.04.0.04-1.04.1.04-2.82.0.88-2.40.pth, myrk
BLEU = 70.94, 86.3/75.6/66.5/58.5 (BP=1.000, ratio=1.047, hyp_len=24257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.470.0.03-1.04.0.04-1.04.1.04-2.82.0.88-2.40.pth, rkmy
BLEU = 72.71, 86.8/77.2/68.4/60.9 (BP=1.000, ratio=1.049, hyp_len=24657, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.70-2.01.0.63-1.88.pth, myrk
BLEU = 69.72, 85.8/74.5/64.9/57.0 (BP=1.000, ratio=1.042, hyp_len=24142, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.70-2.01.0.63-1.88.pth, rkmy
BLEU = 71.25, 86.2/76.1/66.7/58.9 (BP=1.000, ratio=1.043, hyp_len=24529, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.471.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.42.pth, myrk
BLEU = 70.94, 86.3/75.6/66.4/58.5 (BP=1.000, ratio=1.045, hyp_len=24213, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.471.0.04-1.04.0.04-1.04.1.02-2.77.0.88-2.42.pth, rkmy
BLEU = 72.21, 86.4/76.8/67.9/60.4 (BP=1.000, ratio=1.055, hyp_len=24797, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.472.0.04-1.04.0.04-1.04.1.06-2.87.0.87-2.39.pth, myrk
BLEU = 70.60, 86.0/75.3/66.1/58.0 (BP=1.000, ratio=1.048, hyp_len=24266, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.472.0.04-1.04.0.04-1.04.1.06-2.87.0.87-2.39.pth, rkmy
BLEU = 72.30, 86.6/76.8/67.8/60.6 (BP=1.000, ratio=1.052, hyp_len=24739, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.473.0.04-1.04.0.04-1.04.1.00-2.72.0.90-2.47.pth, myrk
BLEU = 70.67, 86.0/75.4/66.2/58.1 (BP=1.000, ratio=1.046, hyp_len=24230, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.473.0.04-1.04.0.04-1.04.1.00-2.72.0.90-2.47.pth, rkmy
BLEU = 72.88, 86.9/77.3/68.6/61.2 (BP=1.000, ratio=1.048, hyp_len=24647, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.474.0.04-1.04.0.04-1.04.1.04-2.83.0.92-2.51.pth, myrk
BLEU = 70.49, 86.0/75.2/66.0/57.8 (BP=1.000, ratio=1.045, hyp_len=24206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.474.0.04-1.04.0.04-1.04.1.04-2.83.0.92-2.51.pth, rkmy
BLEU = 72.41, 86.6/76.9/68.1/60.7 (BP=1.000, ratio=1.053, hyp_len=24763, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.475.0.03-1.04.0.04-1.04.1.02-2.76.0.92-2.52.pth, myrk
BLEU = 70.09, 85.6/74.8/65.5/57.5 (BP=1.000, ratio=1.048, hyp_len=24278, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.475.0.03-1.04.0.04-1.04.1.02-2.76.0.92-2.52.pth, rkmy
BLEU = 73.83, 87.4/78.1/69.6/62.6 (BP=1.000, ratio=1.045, hyp_len=24570, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.476.0.04-1.04.0.04-1.04.0.98-2.67.0.89-2.42.pth, myrk
BLEU = 70.57, 86.2/75.3/65.9/58.0 (BP=1.000, ratio=1.045, hyp_len=24212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.476.0.04-1.04.0.04-1.04.0.98-2.67.0.89-2.42.pth, rkmy
BLEU = 72.57, 86.7/77.0/68.2/60.9 (BP=1.000, ratio=1.052, hyp_len=24721, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.477.0.04-1.04.0.04-1.04.1.04-2.84.0.89-2.43.pth, myrk
BLEU = 70.50, 86.0/75.2/65.9/57.9 (BP=1.000, ratio=1.048, hyp_len=24275, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.477.0.04-1.04.0.04-1.04.1.04-2.84.0.89-2.43.pth, rkmy
BLEU = 72.71, 86.8/77.2/68.4/61.0 (BP=1.000, ratio=1.050, hyp_len=24683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.478.0.04-1.04.0.04-1.04.1.01-2.76.0.92-2.51.pth, myrk
BLEU = 70.74, 86.2/75.3/66.2/58.3 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.478.0.04-1.04.0.04-1.04.1.01-2.76.0.92-2.51.pth, rkmy
BLEU = 72.66, 86.7/77.2/68.4/60.9 (BP=1.000, ratio=1.053, hyp_len=24761, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.479.0.04-1.04.0.04-1.04.1.01-2.73.0.92-2.50.pth, myrk
BLEU = 70.67, 85.9/75.3/66.2/58.3 (BP=1.000, ratio=1.050, hyp_len=24321, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.479.0.04-1.04.0.04-1.04.1.01-2.73.0.92-2.50.pth, rkmy
BLEU = 73.03, 86.9/77.4/68.8/61.5 (BP=1.000, ratio=1.050, hyp_len=24687, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.480.0.04-1.04.0.04-1.04.1.04-2.82.0.92-2.50.pth, myrk
BLEU = 71.01, 86.2/75.6/66.5/58.6 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.480.0.04-1.04.0.04-1.04.1.04-2.82.0.92-2.50.pth, rkmy
BLEU = 72.43, 86.7/77.0/68.1/60.5 (BP=1.000, ratio=1.051, hyp_len=24714, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.19.0.17-1.19.0.70-2.02.0.62-1.86.pth, myrk
BLEU = 68.44, 85.0/73.6/63.6/55.2 (BP=1.000, ratio=1.049, hyp_len=24288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.19.0.17-1.19.0.70-2.02.0.62-1.86.pth, rkmy
BLEU = 68.95, 84.8/74.0/64.1/56.1 (BP=1.000, ratio=1.058, hyp_len=24880, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.481.0.04-1.04.0.04-1.04.1.07-2.91.0.90-2.46.pth, myrk
BLEU = 70.61, 86.1/75.3/66.1/58.1 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.481.0.04-1.04.0.04-1.04.1.07-2.91.0.90-2.46.pth, rkmy
BLEU = 72.94, 86.9/77.4/68.7/61.3 (BP=1.000, ratio=1.049, hyp_len=24671, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.482.0.04-1.04.0.03-1.03.1.05-2.86.0.90-2.46.pth, myrk
BLEU = 70.80, 86.2/75.5/66.3/58.2 (BP=1.000, ratio=1.048, hyp_len=24283, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.482.0.04-1.04.0.03-1.03.1.05-2.86.0.90-2.46.pth, rkmy
BLEU = 73.05, 86.9/77.5/68.8/61.5 (BP=1.000, ratio=1.049, hyp_len=24655, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.483.0.04-1.04.0.04-1.04.1.05-2.87.0.89-2.44.pth, myrk
BLEU = 70.95, 86.1/75.5/66.5/58.6 (BP=1.000, ratio=1.048, hyp_len=24270, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.483.0.04-1.04.0.04-1.04.1.05-2.87.0.89-2.44.pth, rkmy
BLEU = 71.88, 86.3/76.6/67.5/59.8 (BP=1.000, ratio=1.058, hyp_len=24871, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.484.0.04-1.04.0.04-1.04.1.05-2.85.0.91-2.48.pth, myrk
BLEU = 70.61, 85.9/75.2/66.1/58.2 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.484.0.04-1.04.0.04-1.04.1.05-2.85.0.91-2.48.pth, rkmy
BLEU = 72.76, 86.9/77.3/68.5/61.0 (BP=1.000, ratio=1.048, hyp_len=24630, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.485.0.04-1.04.0.04-1.04.1.04-2.84.0.93-2.54.pth, myrk
BLEU = 70.98, 86.1/75.6/66.5/58.7 (BP=1.000, ratio=1.047, hyp_len=24245, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.485.0.04-1.04.0.04-1.04.1.04-2.84.0.93-2.54.pth, rkmy
BLEU = 71.85, 86.3/76.5/67.5/59.8 (BP=1.000, ratio=1.055, hyp_len=24812, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.486.0.04-1.04.0.04-1.04.1.06-2.89.0.90-2.45.pth, myrk
BLEU = 70.54, 85.9/75.2/66.0/58.1 (BP=1.000, ratio=1.049, hyp_len=24298, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.486.0.04-1.04.0.04-1.04.1.06-2.89.0.90-2.45.pth, rkmy
BLEU = 73.47, 87.2/77.8/69.3/62.0 (BP=1.000, ratio=1.047, hyp_len=24611, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.487.0.04-1.04.0.04-1.04.1.05-2.85.0.94-2.55.pth, myrk
BLEU = 70.53, 85.9/75.1/66.0/58.1 (BP=1.000, ratio=1.047, hyp_len=24253, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.487.0.04-1.04.0.04-1.04.1.05-2.85.0.94-2.55.pth, rkmy
BLEU = 72.89, 86.9/77.4/68.6/61.2 (BP=1.000, ratio=1.050, hyp_len=24688, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.488.0.04-1.04.0.03-1.04.1.07-2.91.0.90-2.45.pth, myrk
BLEU = 71.09, 86.2/75.6/66.6/58.9 (BP=1.000, ratio=1.047, hyp_len=24253, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.488.0.04-1.04.0.03-1.04.1.07-2.91.0.90-2.45.pth, rkmy
BLEU = 73.46, 87.1/77.8/69.3/62.0 (BP=1.000, ratio=1.045, hyp_len=24565, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.489.0.04-1.04.0.04-1.04.1.05-2.85.0.89-2.44.pth, myrk
BLEU = 70.53, 86.1/75.3/66.0/57.9 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.489.0.04-1.04.0.04-1.04.1.05-2.85.0.89-2.44.pth, rkmy
BLEU = 72.97, 86.9/77.4/68.7/61.3 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.490.0.04-1.04.0.04-1.04.1.06-2.89.0.88-2.41.pth, myrk
BLEU = 70.38, 86.0/75.2/65.9/57.6 (BP=1.000, ratio=1.050, hyp_len=24317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.490.0.04-1.04.0.04-1.04.1.06-2.89.0.88-2.41.pth, rkmy
BLEU = 72.86, 86.8/77.2/68.6/61.3 (BP=1.000, ratio=1.049, hyp_len=24653, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.18.0.70-2.01.0.63-1.88.pth, myrk
BLEU = 70.03, 85.7/74.9/65.4/57.3 (BP=1.000, ratio=1.047, hyp_len=24243, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.18.0.70-2.01.0.63-1.88.pth, rkmy
BLEU = 70.62, 85.6/75.3/66.0/58.4 (BP=1.000, ratio=1.047, hyp_len=24618, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.491.0.04-1.04.0.04-1.04.1.07-2.93.0.90-2.45.pth, myrk
BLEU = 70.57, 86.0/75.3/66.1/57.9 (BP=1.000, ratio=1.048, hyp_len=24269, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.491.0.04-1.04.0.04-1.04.1.07-2.93.0.90-2.45.pth, rkmy
BLEU = 72.83, 86.8/77.2/68.5/61.3 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.492.0.04-1.04.0.03-1.03.1.05-2.86.0.89-2.45.pth, myrk
BLEU = 71.36, 86.5/75.9/66.8/59.1 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.492.0.04-1.04.0.03-1.03.1.05-2.86.0.89-2.45.pth, rkmy
BLEU = 73.23, 87.2/77.6/68.9/61.7 (BP=1.000, ratio=1.048, hyp_len=24649, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.493.0.04-1.04.0.04-1.04.1.05-2.86.0.89-2.42.pth, myrk
BLEU = 71.35, 86.5/75.9/66.9/59.0 (BP=1.000, ratio=1.043, hyp_len=24152, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.493.0.04-1.04.0.04-1.04.1.05-2.86.0.89-2.42.pth, rkmy
BLEU = 72.61, 86.8/77.2/68.3/60.7 (BP=1.000, ratio=1.051, hyp_len=24700, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.494.0.04-1.04.0.04-1.04.1.09-2.98.0.90-2.45.pth, myrk
BLEU = 69.97, 85.6/74.7/65.4/57.3 (BP=1.000, ratio=1.054, hyp_len=24413, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.494.0.04-1.04.0.04-1.04.1.09-2.98.0.90-2.45.pth, rkmy
BLEU = 72.90, 86.7/77.3/68.7/61.3 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.495.0.04-1.04.0.04-1.04.1.04-2.82.0.91-2.50.pth, myrk
BLEU = 71.02, 86.3/75.7/66.5/58.6 (BP=1.000, ratio=1.045, hyp_len=24192, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.495.0.04-1.04.0.04-1.04.1.04-2.82.0.91-2.50.pth, rkmy
BLEU = 71.93, 86.4/76.6/67.5/59.9 (BP=1.000, ratio=1.055, hyp_len=24800, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.496.0.04-1.04.0.04-1.04.1.05-2.85.0.91-2.48.pth, myrk
BLEU = 70.95, 86.3/75.6/66.4/58.4 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.496.0.04-1.04.0.04-1.04.1.05-2.85.0.91-2.48.pth, rkmy
BLEU = 72.73, 86.8/77.2/68.4/61.0 (BP=1.000, ratio=1.050, hyp_len=24683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.497.0.04-1.04.0.04-1.04.1.07-2.90.0.89-2.44.pth, myrk
BLEU = 71.63, 86.7/76.1/67.1/59.4 (BP=1.000, ratio=1.041, hyp_len=24108, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.497.0.04-1.04.0.04-1.04.1.07-2.90.0.89-2.44.pth, rkmy
BLEU = 71.53, 86.2/76.3/67.2/59.3 (BP=1.000, ratio=1.056, hyp_len=24821, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.498.0.04-1.04.0.04-1.04.1.05-2.85.0.88-2.42.pth, myrk
BLEU = 71.17, 86.5/75.7/66.7/58.8 (BP=1.000, ratio=1.043, hyp_len=24153, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.498.0.04-1.04.0.04-1.04.1.05-2.85.0.88-2.42.pth, rkmy
BLEU = 73.00, 87.0/77.5/68.7/61.3 (BP=1.000, ratio=1.049, hyp_len=24654, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.499.0.04-1.04.0.04-1.04.1.07-2.92.0.90-2.46.pth, myrk
BLEU = 71.31, 86.5/75.9/66.8/58.9 (BP=1.000, ratio=1.047, hyp_len=24239, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.499.0.04-1.04.0.04-1.04.1.07-2.92.0.90-2.46.pth, rkmy
BLEU = 72.71, 86.9/77.1/68.3/61.0 (BP=1.000, ratio=1.047, hyp_len=24608, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.500.0.04-1.04.0.04-1.04.1.05-2.85.0.87-2.40.pth, myrk
BLEU = 70.60, 85.9/75.2/66.1/58.1 (BP=1.000, ratio=1.051, hyp_len=24338, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.500.0.04-1.04.0.04-1.04.1.05-2.85.0.87-2.40.pth, rkmy
BLEU = 72.35, 86.6/76.9/68.0/60.5 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.16-1.18.0.16-1.18.0.71-2.04.0.63-1.88.pth, myrk
BLEU = 69.62, 85.4/74.4/65.0/56.9 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.16-1.18.0.16-1.18.0.71-2.04.0.63-1.88.pth, rkmy
BLEU = 70.13, 85.4/75.0/65.5/57.6 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.18.0.16-1.18.0.72-2.05.0.64-1.89.pth, myrk
BLEU = 70.65, 86.1/75.2/66.1/58.2 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.18.0.16-1.18.0.72-2.05.0.64-1.89.pth, rkmy
BLEU = 68.89, 84.8/73.9/64.0/56.2 (BP=1.000, ratio=1.061, hyp_len=24941, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.16-1.17.0.73-2.08.0.64-1.90.pth, myrk
BLEU = 69.66, 85.5/74.4/64.9/57.0 (BP=1.000, ratio=1.045, hyp_len=24196, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.16-1.17.0.73-2.08.0.64-1.90.pth, rkmy
BLEU = 70.21, 85.4/74.9/65.6/57.9 (BP=1.000, ratio=1.051, hyp_len=24706, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.16-1.17.0.72-2.05.0.64-1.90.pth, myrk
BLEU = 69.55, 85.4/74.4/64.9/56.8 (BP=1.000, ratio=1.050, hyp_len=24307, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.16-1.17.0.72-2.05.0.64-1.90.pth, rkmy
BLEU = 70.35, 85.6/75.2/65.6/57.9 (BP=1.000, ratio=1.054, hyp_len=24772, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.72-2.06.0.62-1.87.pth, myrk
BLEU = 69.18, 84.9/73.9/64.6/56.5 (BP=1.000, ratio=1.053, hyp_len=24378, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.72-2.06.0.62-1.87.pth, rkmy
BLEU = 69.15, 84.6/73.9/64.4/56.8 (BP=1.000, ratio=1.061, hyp_len=24938, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.18.0.16-1.17.0.75-2.11.0.66-1.93.pth, myrk
BLEU = 69.97, 85.8/74.8/65.3/57.2 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.18.0.16-1.17.0.75-2.11.0.66-1.93.pth, rkmy
BLEU = 70.03, 85.5/74.9/65.3/57.5 (BP=1.000, ratio=1.050, hyp_len=24688, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.15-1.17.0.15-1.16.0.73-2.07.0.66-1.93.pth, myrk
BLEU = 69.23, 85.1/74.1/64.6/56.4 (BP=1.000, ratio=1.050, hyp_len=24323, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.15-1.17.0.15-1.16.0.73-2.07.0.66-1.93.pth, rkmy
BLEU = 69.53, 84.7/74.3/64.9/57.2 (BP=1.000, ratio=1.063, hyp_len=24983, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.73-2.08.0.64-1.89.pth, myrk
BLEU = 68.68, 84.9/73.5/63.9/55.8 (BP=1.000, ratio=1.051, hyp_len=24331, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.73-2.08.0.64-1.89.pth, rkmy
BLEU = 67.89, 83.8/72.9/63.1/55.1 (BP=1.000, ratio=1.069, hyp_len=25137, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.73-2.08.0.66-1.93.pth, myrk
BLEU = 69.89, 85.7/74.5/65.2/57.3 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.73-2.08.0.66-1.93.pth, rkmy
BLEU = 69.76, 85.1/74.7/65.1/57.2 (BP=1.000, ratio=1.056, hyp_len=24821, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.73-2.08.0.65-1.91.pth, myrk
BLEU = 69.56, 85.5/74.4/64.9/56.8 (BP=1.000, ratio=1.044, hyp_len=24169, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.73-2.08.0.65-1.91.pth, rkmy
BLEU = 70.36, 85.6/75.1/65.6/58.1 (BP=1.000, ratio=1.052, hyp_len=24726, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.72-2.06.0.64-1.89.pth, myrk
BLEU = 69.65, 85.6/74.5/65.0/56.8 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.72-2.06.0.64-1.89.pth, rkmy
BLEU = 70.15, 85.5/75.0/65.5/57.7 (BP=1.000, ratio=1.052, hyp_len=24740, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.15-1.16.0.14-1.15.0.75-2.13.0.67-1.94.pth, myrk
BLEU = 69.20, 84.7/73.8/64.6/56.8 (BP=1.000, ratio=1.052, hyp_len=24356, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.15-1.16.0.14-1.15.0.75-2.13.0.67-1.94.pth, rkmy
BLEU = 69.76, 85.1/74.6/65.1/57.4 (BP=1.000, ratio=1.058, hyp_len=24870, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.73-2.09.0.66-1.94.pth, myrk
BLEU = 69.08, 85.0/73.9/64.4/56.3 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.73-2.09.0.66-1.94.pth, rkmy
BLEU = 70.66, 85.9/75.4/66.0/58.3 (BP=1.000, ratio=1.048, hyp_len=24643, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.15-1.16.0.75-2.11.0.67-1.95.pth, myrk
BLEU = 69.94, 85.5/74.7/65.3/57.3 (BP=1.000, ratio=1.046, hyp_len=24215, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.15-1.16.0.75-2.11.0.67-1.95.pth, rkmy
BLEU = 70.19, 85.4/74.9/65.5/57.9 (BP=1.000, ratio=1.053, hyp_len=24751, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.16.0.73-2.07.0.67-1.96.pth, myrk
BLEU = 69.37, 85.0/74.0/64.7/56.9 (BP=1.000, ratio=1.053, hyp_len=24378, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.16.0.73-2.07.0.67-1.96.pth, rkmy
BLEU = 69.25, 84.8/74.2/64.5/56.6 (BP=1.000, ratio=1.060, hyp_len=24915, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.14-1.15.0.14-1.15.0.74-2.10.0.67-1.96.pth, myrk
BLEU = 69.99, 85.4/74.6/65.5/57.6 (BP=1.000, ratio=1.044, hyp_len=24170, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.14-1.15.0.14-1.15.0.74-2.10.0.67-1.96.pth, rkmy
BLEU = 69.57, 85.0/74.4/64.8/57.1 (BP=1.000, ratio=1.055, hyp_len=24802, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.14-1.15.0.13-1.14.0.73-2.08.0.67-1.96.pth, myrk
BLEU = 69.33, 85.2/74.1/64.7/56.6 (BP=1.000, ratio=1.047, hyp_len=24252, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.14-1.15.0.13-1.14.0.73-2.08.0.67-1.96.pth, rkmy
BLEU = 68.78, 84.6/73.8/63.9/56.1 (BP=1.000, ratio=1.063, hyp_len=24988, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.13-1.14.0.13-1.14.0.74-2.09.0.69-1.99.pth, myrk
BLEU = 70.22, 85.8/74.8/65.6/57.7 (BP=1.000, ratio=1.044, hyp_len=24179, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.13-1.14.0.13-1.14.0.74-2.09.0.69-1.99.pth, rkmy
BLEU = 69.87, 85.2/74.6/65.1/57.6 (BP=1.000, ratio=1.057, hyp_len=24844, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.14-1.15.0.13-1.14.0.77-2.15.0.66-1.94.pth, myrk
BLEU = 69.79, 85.4/74.6/65.2/57.1 (BP=1.000, ratio=1.048, hyp_len=24263, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.14-1.15.0.13-1.14.0.77-2.15.0.66-1.94.pth, rkmy
BLEU = 70.43, 85.7/75.3/65.7/58.0 (BP=1.000, ratio=1.053, hyp_len=24749, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.13-1.13.0.75-2.11.0.70-2.01.pth, myrk
BLEU = 70.44, 85.9/75.1/65.8/58.0 (BP=1.000, ratio=1.045, hyp_len=24194, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.13-1.13.0.75-2.11.0.70-2.01.pth, rkmy
BLEU = 71.13, 86.0/75.8/66.5/59.0 (BP=1.000, ratio=1.047, hyp_len=24603, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.13.0.75-2.13.0.68-1.98.pth, myrk
BLEU = 69.56, 85.6/74.4/64.8/56.7 (BP=1.000, ratio=1.047, hyp_len=24240, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.13.0.75-2.13.0.68-1.98.pth, rkmy
BLEU = 71.00, 86.1/75.7/66.3/58.8 (BP=1.000, ratio=1.047, hyp_len=24607, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.13.0.13-1.14.0.74-2.09.0.68-1.98.pth, myrk
BLEU = 70.41, 86.1/75.1/65.8/57.8 (BP=1.000, ratio=1.042, hyp_len=24136, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.13.0.13-1.14.0.74-2.09.0.68-1.98.pth, rkmy
BLEU = 71.23, 86.2/75.9/66.6/59.1 (BP=1.000, ratio=1.044, hyp_len=24533, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.12-1.13.0.12-1.13.0.76-2.15.0.67-1.96.pth, myrk
BLEU = 69.50, 85.5/74.3/64.8/56.7 (BP=1.000, ratio=1.043, hyp_len=24165, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.12-1.13.0.12-1.13.0.76-2.15.0.67-1.96.pth, rkmy
BLEU = 70.72, 86.0/75.6/66.1/58.3 (BP=1.000, ratio=1.050, hyp_len=24674, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.12-1.13.0.77-2.16.0.70-2.02.pth, myrk
BLEU = 68.98, 85.2/73.8/64.2/56.0 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.12-1.13.0.77-2.16.0.70-2.02.pth, rkmy
BLEU = 70.42, 85.8/75.2/65.6/58.1 (BP=1.000, ratio=1.050, hyp_len=24692, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.13-1.13.0.77-2.16.0.68-1.98.pth, myrk
BLEU = 70.67, 86.1/75.2/66.1/58.3 (BP=1.000, ratio=1.040, hyp_len=24096, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.13-1.13.0.77-2.16.0.68-1.98.pth, rkmy
BLEU = 70.12, 85.5/75.1/65.4/57.5 (BP=1.000, ratio=1.055, hyp_len=24796, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.12.0.12-1.12.0.79-2.20.0.70-2.02.pth, myrk
BLEU = 70.48, 86.1/75.2/65.8/57.9 (BP=1.000, ratio=1.041, hyp_len=24105, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.12.0.12-1.12.0.79-2.20.0.70-2.02.pth, rkmy
BLEU = 69.37, 84.9/74.2/64.6/57.0 (BP=1.000, ratio=1.060, hyp_len=24919, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.12.0.12-1.13.0.80-2.23.0.68-1.98.pth, myrk
BLEU = 69.80, 85.5/74.5/65.2/57.2 (BP=1.000, ratio=1.046, hyp_len=24223, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.12.0.12-1.13.0.80-2.23.0.68-1.98.pth, rkmy
BLEU = 70.80, 86.0/75.7/66.2/58.4 (BP=1.000, ratio=1.047, hyp_len=24611, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.12.0.12-1.13.0.81-2.24.0.70-2.01.pth, myrk
BLEU = 70.16, 85.9/74.7/65.5/57.7 (BP=1.000, ratio=1.041, hyp_len=24118, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.12.0.12-1.13.0.81-2.24.0.70-2.01.pth, rkmy
BLEU = 70.20, 85.6/75.1/65.5/57.8 (BP=1.000, ratio=1.051, hyp_len=24701, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.12-1.13.0.77-2.15.0.69-1.98.pth, myrk
BLEU = 69.97, 85.8/74.7/65.3/57.2 (BP=1.000, ratio=1.041, hyp_len=24108, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.12-1.13.0.77-2.15.0.69-1.98.pth, rkmy
BLEU = 70.68, 85.7/75.4/66.0/58.4 (BP=1.000, ratio=1.053, hyp_len=24745, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.11-1.12.0.78-2.17.0.69-2.00.pth, myrk
BLEU = 70.03, 85.8/74.8/65.4/57.3 (BP=1.000, ratio=1.038, hyp_len=24051, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.11-1.12.0.78-2.17.0.69-2.00.pth, rkmy
BLEU = 70.95, 86.0/75.7/66.3/58.7 (BP=1.000, ratio=1.050, hyp_len=24687, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.11-1.12.0.77-2.16.0.70-2.01.pth, myrk
BLEU = 69.08, 85.1/74.1/64.4/56.0 (BP=1.000, ratio=1.053, hyp_len=24379, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.11-1.12.0.77-2.16.0.70-2.01.pth, rkmy
BLEU = 69.68, 85.2/74.6/64.9/57.2 (BP=1.000, ratio=1.060, hyp_len=24925, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.11.0.11-1.12.0.79-2.20.0.72-2.04.pth, myrk
BLEU = 69.62, 85.2/74.3/65.0/57.1 (BP=1.000, ratio=1.053, hyp_len=24394, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.11.0.11-1.12.0.79-2.20.0.72-2.04.pth, rkmy
BLEU = 70.74, 85.6/75.3/66.2/58.7 (BP=1.000, ratio=1.052, hyp_len=24736, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.82.0.12-1.12.0.11-1.12.0.80-2.23.0.69-1.99.pth, myrk
BLEU = 69.76, 85.7/74.5/65.1/57.0 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.82.0.12-1.12.0.11-1.12.0.80-2.23.0.69-1.99.pth, rkmy
BLEU = 69.55, 85.1/74.5/64.8/57.0 (BP=1.000, ratio=1.060, hyp_len=24921, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.11-1.12.0.79-2.21.0.70-2.02.pth, myrk
BLEU = 69.67, 85.5/74.4/65.1/56.9 (BP=1.000, ratio=1.044, hyp_len=24190, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.11-1.12.0.79-2.21.0.70-2.02.pth, rkmy
BLEU = 71.11, 86.1/75.8/66.4/59.0 (BP=1.000, ratio=1.046, hyp_len=24584, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.11.0.11-1.11.0.79-2.20.0.70-2.01.pth, myrk
BLEU = 69.61, 85.0/74.3/65.1/57.2 (BP=1.000, ratio=1.051, hyp_len=24352, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.11.0.11-1.11.0.79-2.20.0.70-2.01.pth, rkmy
BLEU = 71.30, 86.1/76.0/66.7/59.2 (BP=1.000, ratio=1.049, hyp_len=24659, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.11.0.11-1.11.0.80-2.22.0.70-2.01.pth, myrk
BLEU = 69.75, 85.4/74.4/65.1/57.3 (BP=1.000, ratio=1.047, hyp_len=24257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.11.0.11-1.11.0.80-2.22.0.70-2.01.pth, rkmy
BLEU = 70.16, 85.3/74.9/65.5/57.9 (BP=1.000, ratio=1.059, hyp_len=24896, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.86.0.11-1.11.0.11-1.11.0.80-2.23.0.70-2.01.pth, myrk
BLEU = 69.74, 85.5/74.4/65.1/57.0 (BP=1.000, ratio=1.044, hyp_len=24177, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.86.0.11-1.11.0.11-1.11.0.80-2.23.0.70-2.01.pth, rkmy
BLEU = 71.28, 86.0/75.8/66.7/59.4 (BP=1.000, ratio=1.052, hyp_len=24722, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.87.0.11-1.12.0.11-1.12.0.80-2.22.0.70-2.02.pth, myrk
BLEU = 70.33, 85.6/74.9/65.8/58.0 (BP=1.000, ratio=1.046, hyp_len=24223, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.87.0.11-1.12.0.11-1.12.0.80-2.22.0.70-2.02.pth, rkmy
BLEU = 71.10, 85.8/75.8/66.5/59.1 (BP=1.000, ratio=1.054, hyp_len=24787, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.11.0.11-1.11.0.80-2.22.0.71-2.03.pth, myrk
BLEU = 70.34, 85.6/74.9/65.9/58.0 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.11.0.11-1.11.0.80-2.22.0.71-2.03.pth, rkmy
BLEU = 69.98, 85.1/74.6/65.3/57.9 (BP=1.000, ratio=1.060, hyp_len=24927, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.89.0.10-1.11.0.10-1.11.0.81-2.26.0.70-2.01.pth, myrk
BLEU = 69.16, 85.3/74.0/64.4/56.2 (BP=1.000, ratio=1.050, hyp_len=24329, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.89.0.10-1.11.0.10-1.11.0.81-2.26.0.70-2.01.pth, rkmy
BLEU = 70.94, 85.8/75.5/66.4/58.9 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.10-1.11.0.82-2.27.0.71-2.02.pth, myrk
BLEU = 69.15, 85.1/74.0/64.5/56.4 (BP=1.000, ratio=1.051, hyp_len=24332, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.10-1.11.0.82-2.27.0.71-2.02.pth, rkmy
BLEU = 71.19, 85.9/75.8/66.7/59.2 (BP=1.000, ratio=1.051, hyp_len=24708, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.91.0.11-1.11.0.10-1.11.0.80-2.21.0.71-2.03.pth, myrk
BLEU = 69.68, 85.2/74.3/65.1/57.1 (BP=1.000, ratio=1.048, hyp_len=24278, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.91.0.11-1.11.0.10-1.11.0.80-2.21.0.71-2.03.pth, rkmy
BLEU = 69.81, 85.4/74.8/65.1/57.1 (BP=1.000, ratio=1.058, hyp_len=24870, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.92.0.10-1.11.0.10-1.11.0.82-2.26.0.71-2.04.pth, myrk
BLEU = 70.92, 86.1/75.5/66.5/58.5 (BP=1.000, ratio=1.040, hyp_len=24089, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.92.0.10-1.11.0.10-1.11.0.82-2.26.0.71-2.04.pth, rkmy
BLEU = 69.87, 85.1/74.7/65.2/57.4 (BP=1.000, ratio=1.060, hyp_len=24909, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.93.0.10-1.11.0.10-1.10.0.83-2.29.0.70-2.01.pth, myrk
BLEU = 69.71, 85.5/74.4/65.1/57.0 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.93.0.10-1.11.0.10-1.10.0.83-2.29.0.70-2.01.pth, rkmy
BLEU = 69.62, 85.3/74.6/64.9/56.9 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.94.0.10-1.11.0.10-1.11.0.82-2.27.0.70-2.02.pth, myrk
BLEU = 69.89, 85.5/74.5/65.3/57.3 (BP=1.000, ratio=1.049, hyp_len=24293, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.94.0.10-1.11.0.10-1.11.0.82-2.27.0.70-2.02.pth, rkmy
BLEU = 69.67, 85.4/74.5/64.9/57.0 (BP=1.000, ratio=1.057, hyp_len=24856, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.95.0.09-1.10.0.09-1.10.0.83-2.28.0.71-2.03.pth, myrk
BLEU = 69.39, 85.3/74.2/64.7/56.6 (BP=1.000, ratio=1.050, hyp_len=24317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.95.0.09-1.10.0.09-1.10.0.83-2.28.0.71-2.03.pth, rkmy
BLEU = 70.21, 85.4/75.0/65.6/57.9 (BP=1.000, ratio=1.055, hyp_len=24802, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.96.0.10-1.11.0.10-1.11.0.82-2.28.0.70-2.01.pth, myrk
BLEU = 69.64, 85.3/74.4/65.1/56.9 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.96.0.10-1.11.0.10-1.11.0.82-2.28.0.70-2.01.pth, rkmy
BLEU = 69.62, 84.8/74.5/65.0/57.2 (BP=1.000, ratio=1.066, hyp_len=25070, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.97.0.10-1.11.0.10-1.10.0.81-2.25.0.73-2.07.pth, myrk
BLEU = 68.65, 84.8/73.5/64.0/55.7 (BP=1.000, ratio=1.056, hyp_len=24459, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.97.0.10-1.11.0.10-1.10.0.81-2.25.0.73-2.07.pth, rkmy
BLEU = 70.98, 85.9/75.6/66.4/58.8 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.98.0.10-1.10.0.10-1.10.0.84-2.31.0.75-2.12.pth, myrk
BLEU = 69.84, 85.6/74.6/65.2/57.1 (BP=1.000, ratio=1.047, hyp_len=24256, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.98.0.10-1.10.0.10-1.10.0.84-2.31.0.75-2.12.pth, rkmy
BLEU = 71.27, 85.8/75.8/66.8/59.5 (BP=1.000, ratio=1.051, hyp_len=24699, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.99.0.10-1.10.0.10-1.10.0.81-2.25.0.73-2.08.pth, myrk
BLEU = 70.14, 85.5/74.7/65.6/57.7 (BP=1.000, ratio=1.045, hyp_len=24205, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.99.0.10-1.10.0.10-1.10.0.81-2.25.0.73-2.08.pth, rkmy
BLEU = 71.03, 85.9/75.8/66.5/58.8 (BP=1.000, ratio=1.048, hyp_len=24644, ref_len=23509)
==========

real	506m5.408s
user	497m33.156s
sys	20m56.803s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-rk အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
rk-my အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   


