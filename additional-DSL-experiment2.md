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

```

testing/evaluation ...  

```

```

my-rk အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
rk-my အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   


