## Running Log of Extending 40-60, 50-50, 60-40, 70-30

### seq2seq, 40 epoch model, my-rk

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.pth;
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.pth',
    'n_epochs': 40,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 1 - |param|=6.40e+02 |g_param|=1.72e+05 loss=4.4532e+00 ppl=85.90                                                 
Validation - loss=4.0836e+00 ppl=59.36 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.40e+02 |g_param|=8.44e+04 loss=4.1146e+00 ppl=61.23                                                 
Validation - loss=3.8910e+00 ppl=48.96 best_loss=4.0836e+00 best_ppl=59.36                                              
Epoch 3 - |param|=6.40e+02 |g_param|=8.80e+04 loss=4.0598e+00 ppl=57.96                                                 
Validation - loss=3.8064e+00 ppl=44.99 best_loss=3.8910e+00 best_ppl=48.96                                              
Epoch 4 - |param|=6.40e+02 |g_param|=8.70e+04 loss=3.9125e+00 ppl=50.02                                                 
Validation - loss=3.6946e+00 ppl=40.23 best_loss=3.8064e+00 best_ppl=44.99                                              
Epoch 5 - |param|=6.41e+02 |g_param|=8.94e+04 loss=3.8477e+00 ppl=46.89                                                 
Validation - loss=3.6385e+00 ppl=38.03 best_loss=3.6946e+00 best_ppl=40.23                                              
Epoch 6 - |param|=6.41e+02 |g_param|=8.74e+04 loss=3.7911e+00 ppl=44.31                                                 
Validation - loss=3.5473e+00 ppl=34.72 best_loss=3.6385e+00 best_ppl=38.03                                              
Epoch 7 - |param|=6.41e+02 |g_param|=8.52e+04 loss=3.6580e+00 ppl=38.78                                                 
Validation - loss=3.4608e+00 ppl=31.84 best_loss=3.5473e+00 best_ppl=34.72                                              
Epoch 8 - |param|=6.42e+02 |g_param|=1.00e+05 loss=3.6363e+00 ppl=37.95                                                 
Validation - loss=3.3883e+00 ppl=29.61 best_loss=3.4608e+00 best_ppl=31.84                                              
Epoch 9 - |param|=6.43e+02 |g_param|=8.44e+04 loss=3.4309e+00 ppl=30.90                                                 
Validation - loss=3.2107e+00 ppl=24.80 best_loss=3.3883e+00 best_ppl=29.61                                              
Epoch 10 - |param|=6.43e+02 |g_param|=6.72e+04 loss=3.2340e+00 ppl=25.38                                                
Validation - loss=3.1215e+00 ppl=22.68 best_loss=3.2107e+00 best_ppl=24.80                                              
Epoch 11 - |param|=6.44e+02 |g_param|=5.00e+04 loss=3.0985e+00 ppl=22.16                                                
Validation - loss=2.9504e+00 ppl=19.11 best_loss=3.1215e+00 best_ppl=22.68                                              
Epoch 12 - |param|=6.45e+02 |g_param|=4.89e+04 loss=3.0615e+00 ppl=21.36                                                
Validation - loss=2.8535e+00 ppl=17.35 best_loss=2.9504e+00 best_ppl=19.11                                              
Epoch 13 - |param|=6.45e+02 |g_param|=3.21e+04 loss=3.0184e+00 ppl=20.46                                                
Validation - loss=2.6991e+00 ppl=14.87 best_loss=2.8535e+00 best_ppl=17.35                                              
Epoch 14 - |param|=6.46e+02 |g_param|=3.58e+04 loss=2.7643e+00 ppl=15.87                                                
Validation - loss=2.5682e+00 ppl=13.04 best_loss=2.6991e+00 best_ppl=14.87                                              
Epoch 15 - |param|=6.47e+02 |g_param|=5.14e+04 loss=2.6485e+00 ppl=14.13                                                
Validation - loss=2.6105e+00 ppl=13.61 best_loss=2.5682e+00 best_ppl=13.04                                              
Epoch 16 - |param|=6.47e+02 |g_param|=3.66e+04 loss=2.3853e+00 ppl=10.86                                                
Validation - loss=2.2633e+00 ppl=9.62 best_loss=2.5682e+00 best_ppl=13.04                                               
Epoch 17 - |param|=6.48e+02 |g_param|=4.84e+04 loss=2.2476e+00 ppl=9.47                                                 
Validation - loss=2.1700e+00 ppl=8.76 best_loss=2.2633e+00 best_ppl=9.62                                                
Epoch 18 - |param|=6.49e+02 |g_param|=4.44e+04 loss=1.9929e+00 ppl=7.34                                                 
Validation - loss=1.9834e+00 ppl=7.27 best_loss=2.1700e+00 best_ppl=8.76                                                
Epoch 19 - |param|=6.49e+02 |g_param|=5.00e+04 loss=1.9402e+00 ppl=6.96                                                 
Validation - loss=1.8609e+00 ppl=6.43 best_loss=1.9834e+00 best_ppl=7.27                                                
Epoch 20 - |param|=6.50e+02 |g_param|=5.06e+04 loss=1.7272e+00 ppl=5.62                                                 
Validation - loss=1.7555e+00 ppl=5.79 best_loss=1.8609e+00 best_ppl=6.43                                                
Epoch 21 - |param|=6.50e+02 |g_param|=4.56e+04 loss=1.6109e+00 ppl=5.01                                                 
Validation - loss=1.6125e+00 ppl=5.02 best_loss=1.7555e+00 best_ppl=5.79                                                
Epoch 22 - |param|=6.51e+02 |g_param|=4.98e+04 loss=1.5026e+00 ppl=4.49                                                 
Validation - loss=1.5533e+00 ppl=4.73 best_loss=1.6125e+00 best_ppl=5.02                                                
Epoch 23 - |param|=6.51e+02 |g_param|=4.56e+04 loss=1.3814e+00 ppl=3.98                                                 
Validation - loss=1.4637e+00 ppl=4.32 best_loss=1.5533e+00 best_ppl=4.73                                                
Epoch 24 - |param|=6.52e+02 |g_param|=3.80e+04 loss=1.2428e+00 ppl=3.47                                                 
Validation - loss=1.3769e+00 ppl=3.96 best_loss=1.4637e+00 best_ppl=4.32                                                
Epoch 25 - |param|=6.52e+02 |g_param|=4.20e+04 loss=1.1837e+00 ppl=3.27                                                 
Validation - loss=1.2878e+00 ppl=3.62 best_loss=1.3769e+00 best_ppl=3.96                                                
Epoch 26 - |param|=6.53e+02 |g_param|=4.09e+04 loss=1.1043e+00 ppl=3.02                                                 
Validation - loss=1.2402e+00 ppl=3.46 best_loss=1.2878e+00 best_ppl=3.62                                                
Epoch 27 - |param|=6.53e+02 |g_param|=4.07e+04 loss=1.0010e+00 ppl=2.72                                                 
Validation - loss=1.1743e+00 ppl=3.24 best_loss=1.2402e+00 best_ppl=3.46                                                
Epoch 28 - |param|=6.54e+02 |g_param|=4.04e+04 loss=9.4713e-01 ppl=2.58                                                 
Validation - loss=1.1258e+00 ppl=3.08 best_loss=1.1743e+00 best_ppl=3.24                                                
Epoch 29 - |param|=6.54e+02 |g_param|=3.93e+04 loss=9.2144e-01 ppl=2.51                                                 
Validation - loss=1.0744e+00 ppl=2.93 best_loss=1.1258e+00 best_ppl=3.08                                                
Epoch 30 - |param|=6.55e+02 |g_param|=5.34e+04 loss=8.8319e-01 ppl=2.42                                                 
Validation - loss=1.0877e+00 ppl=2.97 best_loss=1.0744e+00 best_ppl=2.93                                                
Epoch 31 - |param|=6.55e+02 |g_param|=2.05e+04 loss=7.9263e-01 ppl=2.21                                                 
Validation - loss=9.9310e-01 ppl=2.70 best_loss=1.0744e+00 best_ppl=2.93                                                
Epoch 32 - |param|=6.55e+02 |g_param|=2.16e+04 loss=7.8285e-01 ppl=2.19                                                 
Validation - loss=9.9663e-01 ppl=2.71 best_loss=9.9310e-01 best_ppl=2.70                                                
Epoch 33 - |param|=6.56e+02 |g_param|=3.12e+04 loss=8.1551e-01 ppl=2.26                                                 
Validation - loss=9.9027e-01 ppl=2.69 best_loss=9.9310e-01 best_ppl=2.70                                                
Epoch 34 - |param|=6.56e+02 |g_param|=1.71e+04 loss=6.9317e-01 ppl=2.00                                                 
Validation - loss=9.4654e-01 ppl=2.58 best_loss=9.9027e-01 best_ppl=2.69                                                
Epoch 35 - |param|=6.57e+02 |g_param|=1.72e+04 loss=6.8254e-01 ppl=1.98                                                 
Validation - loss=9.2620e-01 ppl=2.52 best_loss=9.4654e-01 best_ppl=2.58                                                
Epoch 36 - |param|=6.57e+02 |g_param|=2.66e+04 loss=7.0237e-01 ppl=2.02                                                 
Validation - loss=9.2837e-01 ppl=2.53 best_loss=9.2620e-01 best_ppl=2.52                                                
Epoch 37 - |param|=6.58e+02 |g_param|=1.99e+04 loss=6.4044e-01 ppl=1.90                                                 
Validation - loss=8.9718e-01 ppl=2.45 best_loss=9.2620e-01 best_ppl=2.52                                                
Epoch 38 - |param|=6.58e+02 |g_param|=1.37e+04 loss=6.0018e-01 ppl=1.82                                                 
Validation - loss=8.8302e-01 ppl=2.42 best_loss=8.9718e-01 best_ppl=2.45                                                
Epoch 39 - |param|=6.58e+02 |g_param|=1.66e+04 loss=5.8510e-01 ppl=1.80                                                 
Validation - loss=8.8131e-01 ppl=2.41 best_loss=8.8302e-01 best_ppl=2.42                                                
Epoch 40 - |param|=6.59e+02 |g_param|=2.04e+04 loss=5.5123e-01 ppl=1.74                                                 
Validation - loss=8.9340e-01 ppl=2.44 best_loss=8.8131e-01 best_ppl=2.41                                                

real	7m33.373s
user	7m27.063s
sys	0m6.836s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-myrk.01.4.45-85.90.4.08-59.36.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 3.9/0.0/0.0/0.0 (BP=1.000, ratio=3.621, hyp_len=83864, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.4.11-61.23.3.89-48.96.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.6/2.1/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.4.06-57.96.3.81-44.99.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.6/2.8/0.1/0.0 (BP=0.999, ratio=0.999, hyp_len=23148, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.91-50.02.3.69-40.23.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.8/1.9/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=23331, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.85-46.89.3.64-38.03.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.4/3.1/0.0/0.0 (BP=1.000, ratio=1.017, hyp_len=23546, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.79-44.31.3.55-34.72.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/3.5/0.1/0.0 (BP=1.000, ratio=1.002, hyp_len=23200, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.66-38.78.3.46-31.84.pth
BLEU = 1.08, 25.4/4.7/0.5/0.0 (BP=1.000, ratio=1.007, hyp_len=23314, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.3.64-37.95.3.39-29.61.pth
BLEU = 1.55, 27.8/6.0/1.0/0.0 (BP=1.000, ratio=1.015, hyp_len=23512, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.3.43-30.90.3.21-24.80.pth
BLEU = 2.47, 29.8/7.7/1.3/0.1 (BP=0.999, ratio=0.999, hyp_len=23145, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.3.23-25.38.3.12-22.68.pth
BLEU = 3.93, 32.6/9.0/2.0/0.5 (BP=0.962, ratio=0.962, hyp_len=22291, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.3.10-22.16.2.95-19.11.pth
BLEU = 5.10, 34.7/11.3/2.9/0.6 (BP=1.000, ratio=1.012, hyp_len=23441, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.3.06-21.36.2.85-17.35.pth
BLEU = 6.88, 35.9/13.4/4.1/1.1 (BP=1.000, ratio=1.005, hyp_len=23280, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.3.02-20.46.2.70-14.87.pth
BLEU = 8.58, 39.4/15.8/5.5/1.6 (BP=1.000, ratio=1.007, hyp_len=23317, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.2.76-15.87.2.57-13.04.pth
BLEU = 10.73, 42.7/18.6/7.2/2.3 (BP=1.000, ratio=1.011, hyp_len=23424, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.2.65-14.13.2.61-13.61.pth
BLEU = 9.54, 41.3/17.4/6.3/1.8 (BP=1.000, ratio=1.021, hyp_len=23640, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.2.39-10.86.2.26-9.62.pth
BLEU = 15.77, 48.0/23.7/11.1/4.9 (BP=1.000, ratio=1.014, hyp_len=23489, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.2.25-9.47.2.17-8.76.pth
BLEU = 19.05, 52.1/27.3/14.1/7.0 (BP=0.983, ratio=0.983, hyp_len=22770, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.99-7.34.1.98-7.27.pth
BLEU = 22.65, 55.1/30.8/17.0/9.1 (BP=1.000, ratio=1.007, hyp_len=23322, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.94-6.96.1.86-6.43.pth
BLEU = 26.81, 58.7/35.1/20.8/12.0 (BP=1.000, ratio=1.020, hyp_len=23624, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.73-5.62.1.76-5.79.pth
BLEU = 32.35, 63.2/40.6/25.9/16.5 (BP=1.000, ratio=1.001, hyp_len=23180, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.61-5.01.1.61-5.02.pth
BLEU = 36.46, 65.8/44.4/30.0/20.2 (BP=1.000, ratio=1.010, hyp_len=23403, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.1.50-4.49.1.55-4.73.pth
BLEU = 38.03, 66.8/45.9/31.6/21.5 (BP=1.000, ratio=1.014, hyp_len=23490, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.1.38-3.98.1.46-4.32.pth
BLEU = 42.50, 70.3/50.2/35.9/25.7 (BP=1.000, ratio=1.010, hyp_len=23391, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.1.24-3.47.1.38-3.96.pth
BLEU = 48.59, 74.0/55.7/42.2/32.0 (BP=1.000, ratio=1.003, hyp_len=23236, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.1.18-3.27.1.29-3.62.pth
BLEU = 50.76, 75.6/57.8/44.4/34.2 (BP=1.000, ratio=1.004, hyp_len=23248, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.1.10-3.02.1.24-3.46.pth
BLEU = 53.76, 76.9/60.3/47.6/37.8 (BP=1.000, ratio=1.015, hyp_len=23514, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.1.00-2.72.1.17-3.24.pth
BLEU = 56.66, 79.0/63.0/50.6/40.9 (BP=1.000, ratio=1.006, hyp_len=23296, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.95-2.58.1.13-3.08.pth
BLEU = 58.74, 79.8/64.8/53.0/43.5 (BP=1.000, ratio=1.015, hyp_len=23507, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.92-2.51.1.07-2.93.pth
BLEU = 61.20, 81.2/67.0/55.6/46.4 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.88-2.42.1.09-2.97.pth
BLEU = 59.61, 80.4/65.8/53.9/44.3 (BP=1.000, ratio=1.025, hyp_len=23740, ref_len=23160)
Evaluation result for the model: seq-model-myrk.31.0.79-2.21.0.99-2.70.pth
BLEU = 64.37, 83.1/69.8/59.0/50.2 (BP=1.000, ratio=1.009, hyp_len=23374, ref_len=23160)
Evaluation result for the model: seq-model-myrk.32.0.78-2.19.1.00-2.71.pth
BLEU = 65.27, 83.5/70.6/60.0/51.3 (BP=1.000, ratio=1.012, hyp_len=23438, ref_len=23160)
Evaluation result for the model: seq-model-myrk.33.0.82-2.26.0.99-2.69.pth
BLEU = 65.01, 83.2/70.2/59.8/51.1 (BP=1.000, ratio=1.018, hyp_len=23573, ref_len=23160)
Evaluation result for the model: seq-model-myrk.34.0.69-2.00.0.95-2.58.pth
BLEU = 67.14, 84.5/72.1/62.1/53.7 (BP=1.000, ratio=1.009, hyp_len=23373, ref_len=23160)
Evaluation result for the model: seq-model-myrk.35.0.68-1.98.0.93-2.52.pth
BLEU = 67.55, 84.6/72.5/62.6/54.3 (BP=1.000, ratio=1.017, hyp_len=23563, ref_len=23160)
Evaluation result for the model: seq-model-myrk.36.0.70-2.02.0.93-2.53.pth
BLEU = 67.51, 84.6/72.4/62.6/54.3 (BP=1.000, ratio=1.011, hyp_len=23425, ref_len=23160)
Evaluation result for the model: seq-model-myrk.37.0.64-1.90.0.90-2.45.pth
BLEU = 67.00, 84.1/72.0/62.1/53.6 (BP=1.000, ratio=1.029, hyp_len=23826, ref_len=23160)
Evaluation result for the model: seq-model-myrk.38.0.60-1.82.0.88-2.42.pth
BLEU = 69.88, 85.8/74.5/65.1/57.2 (BP=1.000, ratio=1.016, hyp_len=23541, ref_len=23160)
Evaluation result for the model: seq-model-myrk.39.0.59-1.80.0.88-2.41.pth
BLEU = 68.64, 84.9/73.4/63.9/55.8 (BP=1.000, ratio=1.027, hyp_len=23781, ref_len=23160)
Evaluation result for the model: seq-model-myrk.40.0.55-1.74.0.89-2.44.pth
BLEU = 70.40, 86.1/74.9/65.7/58.0 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)

real	13m47.806s
user	13m28.160s
sys	0m44.862s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-40epoch$
```

Baseline model best BLEU:   

```
Evaluation result for the model: seq-model-myrk.40.0.55-1.74.0.89-2.44.pth
BLEU = 70.40, 86.1/74.9/65.7/58.0 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)
```

## for seq2seq, 50 epoch model, my-rk

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 50 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.pth',
    'n_epochs': 50,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 1 - |param|=6.41e+02 |g_param|=2.87e+05 loss=4.4210e+00 ppl=83.18                                                 
Validation - loss=4.0621e+00 ppl=58.09 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.41e+02 |g_param|=1.76e+05 loss=4.1546e+00 ppl=63.73                                                 
Validation - loss=3.8540e+00 ppl=47.18 best_loss=4.0621e+00 best_ppl=58.09                                              
Epoch 3 - |param|=6.41e+02 |g_param|=1.89e+05 loss=3.9826e+00 ppl=53.66                                                 
Validation - loss=3.7815e+00 ppl=43.88 best_loss=3.8540e+00 best_ppl=47.18                                              
Epoch 4 - |param|=6.42e+02 |g_param|=1.82e+05 loss=3.9169e+00 ppl=50.24                                                 
Validation - loss=3.6597e+00 ppl=38.85 best_loss=3.7815e+00 best_ppl=43.88                                              
Epoch 5 - |param|=6.42e+02 |g_param|=1.91e+05 loss=3.8325e+00 ppl=46.18                                                 
Validation - loss=3.5812e+00 ppl=35.92 best_loss=3.6597e+00 best_ppl=38.85                                              
Epoch 6 - |param|=6.42e+02 |g_param|=1.91e+05 loss=3.6918e+00 ppl=40.12                                                 
Validation - loss=3.5095e+00 ppl=33.43 best_loss=3.5812e+00 best_ppl=35.92                                              
Epoch 7 - |param|=6.43e+02 |g_param|=2.03e+05 loss=3.6422e+00 ppl=38.17                                                 
Validation - loss=3.3669e+00 ppl=28.99 best_loss=3.5095e+00 best_ppl=33.43                                              
Epoch 8 - |param|=6.44e+02 |g_param|=1.74e+05 loss=3.3911e+00 ppl=29.70                                                 
Validation - loss=3.2184e+00 ppl=24.99 best_loss=3.3669e+00 best_ppl=28.99                                              
Epoch 9 - |param|=6.44e+02 |g_param|=2.28e+05 loss=3.3291e+00 ppl=27.91                                                 
Validation - loss=3.0775e+00 ppl=21.70 best_loss=3.2184e+00 best_ppl=24.99                                              
Epoch 10 - |param|=6.45e+02 |g_param|=2.42e+05 loss=3.1170e+00 ppl=22.58                                                
Validation - loss=2.9644e+00 ppl=19.38 best_loss=3.0775e+00 best_ppl=21.70                                              
Epoch 11 - |param|=6.46e+02 |g_param|=2.30e+05 loss=2.9362e+00 ppl=18.84                                                
Validation - loss=2.8286e+00 ppl=16.92 best_loss=2.9644e+00 best_ppl=19.38                                              
Epoch 12 - |param|=6.46e+02 |g_param|=1.52e+05 loss=2.7664e+00 ppl=15.90                                                
Validation - loss=2.6784e+00 ppl=14.56 best_loss=2.8286e+00 best_ppl=16.92                                              
Epoch 13 - |param|=6.47e+02 |g_param|=1.68e+05 loss=2.6787e+00 ppl=14.57                                                
Validation - loss=2.5742e+00 ppl=13.12 best_loss=2.6784e+00 best_ppl=14.56                                              
Epoch 14 - |param|=6.48e+02 |g_param|=1.54e+05 loss=2.5378e+00 ppl=12.65                                                
Validation - loss=2.4193e+00 ppl=11.24 best_loss=2.5742e+00 best_ppl=13.12                                              
Epoch 15 - |param|=6.48e+02 |g_param|=1.70e+05 loss=2.3035e+00 ppl=10.01                                                
Validation - loss=2.3464e+00 ppl=10.45 best_loss=2.4193e+00 best_ppl=11.24                                              
Epoch 16 - |param|=6.49e+02 |g_param|=2.09e+05 loss=2.2127e+00 ppl=9.14                                                 
Validation - loss=2.1648e+00 ppl=8.71 best_loss=2.3464e+00 best_ppl=10.45                                               
Epoch 17 - |param|=6.50e+02 |g_param|=1.81e+05 loss=1.9964e+00 ppl=7.36                                                 
Validation - loss=1.9706e+00 ppl=7.18 best_loss=2.1648e+00 best_ppl=8.71                                                
Epoch 18 - |param|=6.50e+02 |g_param|=1.83e+05 loss=1.8136e+00 ppl=6.13                                                 
Validation - loss=1.8497e+00 ppl=6.36 best_loss=1.9706e+00 best_ppl=7.18                                                
Epoch 19 - |param|=6.51e+02 |g_param|=8.42e+04 loss=1.6558e+00 ppl=5.24                                                 
Validation - loss=1.6859e+00 ppl=5.40 best_loss=1.8497e+00 best_ppl=6.36                                                
Epoch 20 - |param|=6.51e+02 |g_param|=1.04e+05 loss=1.6230e+00 ppl=5.07                                                 
Validation - loss=1.6527e+00 ppl=5.22 best_loss=1.6859e+00 best_ppl=5.40                                                
Epoch 21 - |param|=6.52e+02 |g_param|=1.13e+05 loss=1.5367e+00 ppl=4.65                                                 
Validation - loss=1.5741e+00 ppl=4.83 best_loss=1.6527e+00 best_ppl=5.22                                                
Epoch 22 - |param|=6.53e+02 |g_param|=8.80e+04 loss=1.3717e+00 ppl=3.94                                                 
Validation - loss=1.4746e+00 ppl=4.37 best_loss=1.5741e+00 best_ppl=4.83                                                
Epoch 23 - |param|=6.53e+02 |g_param|=7.54e+04 loss=1.2863e+00 ppl=3.62                                                 
Validation - loss=1.3520e+00 ppl=3.87 best_loss=1.4746e+00 best_ppl=4.37                                                
Epoch 24 - |param|=6.53e+02 |g_param|=7.98e+04 loss=1.2075e+00 ppl=3.34                                                 
Validation - loss=1.2749e+00 ppl=3.58 best_loss=1.3520e+00 best_ppl=3.87                                                
Epoch 25 - |param|=6.54e+02 |g_param|=7.45e+04 loss=1.1095e+00 ppl=3.03                                                 
Validation - loss=1.2286e+00 ppl=3.42 best_loss=1.2749e+00 best_ppl=3.58                                                
Epoch 26 - |param|=6.54e+02 |g_param|=8.54e+04 loss=1.0454e+00 ppl=2.84                                                 
Validation - loss=1.1810e+00 ppl=3.26 best_loss=1.2286e+00 best_ppl=3.42                                                
Epoch 27 - |param|=6.55e+02 |g_param|=7.83e+04 loss=1.0759e+00 ppl=2.93                                                 
Validation - loss=1.1289e+00 ppl=3.09 best_loss=1.1810e+00 best_ppl=3.26                                                
Epoch 28 - |param|=6.55e+02 |g_param|=3.88e+04 loss=9.5486e-01 ppl=2.60                                                 
Validation - loss=1.0764e+00 ppl=2.93 best_loss=1.1289e+00 best_ppl=3.09                                                
Epoch 29 - |param|=6.56e+02 |g_param|=2.96e+04 loss=8.5266e-01 ppl=2.35                                                 
Validation - loss=1.0192e+00 ppl=2.77 best_loss=1.0764e+00 best_ppl=2.93                                                
Epoch 30 - |param|=6.56e+02 |g_param|=3.59e+04 loss=8.3785e-01 ppl=2.31                                                 
Validation - loss=9.8209e-01 ppl=2.67 best_loss=1.0192e+00 best_ppl=2.77                                                
Epoch 31 - |param|=6.57e+02 |g_param|=3.42e+04 loss=7.6790e-01 ppl=2.16                                                 
Validation - loss=9.7333e-01 ppl=2.65 best_loss=9.8209e-01 best_ppl=2.67                                                
Epoch 32 - |param|=6.57e+02 |g_param|=4.58e+04 loss=7.9243e-01 ppl=2.21                                                 
Validation - loss=9.3551e-01 ppl=2.55 best_loss=9.7333e-01 best_ppl=2.65                                                
Epoch 33 - |param|=6.58e+02 |g_param|=3.37e+04 loss=7.1275e-01 ppl=2.04                                                 
Validation - loss=9.0988e-01 ppl=2.48 best_loss=9.3551e-01 best_ppl=2.55                                                
Epoch 34 - |param|=6.58e+02 |g_param|=4.12e+04 loss=7.2468e-01 ppl=2.06                                                 
Validation - loss=8.9411e-01 ppl=2.45 best_loss=9.0988e-01 best_ppl=2.48                                                
Epoch 35 - |param|=6.58e+02 |g_param|=2.82e+04 loss=6.5153e-01 ppl=1.92                                                 
Validation - loss=8.8257e-01 ppl=2.42 best_loss=8.9411e-01 best_ppl=2.45                                                
Epoch 36 - |param|=6.59e+02 |g_param|=2.93e+04 loss=6.1952e-01 ppl=1.86                                                 
Validation - loss=8.6901e-01 ppl=2.38 best_loss=8.8257e-01 best_ppl=2.42                                                
Epoch 37 - |param|=6.59e+02 |g_param|=4.28e+04 loss=6.4161e-01 ppl=1.90                                                 
Validation - loss=8.7153e-01 ppl=2.39 best_loss=8.6901e-01 best_ppl=2.38                                                
Epoch 38 - |param|=6.60e+02 |g_param|=3.17e+04 loss=5.8744e-01 ppl=1.80                                                 
Validation - loss=8.4460e-01 ppl=2.33 best_loss=8.6901e-01 best_ppl=2.38                                                
Epoch 39 - |param|=6.60e+02 |g_param|=3.26e+04 loss=5.5324e-01 ppl=1.74                                                 
Validation - loss=8.2655e-01 ppl=2.29 best_loss=8.4460e-01 best_ppl=2.33                                                
Epoch 40 - |param|=6.60e+02 |g_param|=3.04e+04 loss=5.4920e-01 ppl=1.73                                                 
Validation - loss=7.9836e-01 ppl=2.22 best_loss=8.2655e-01 best_ppl=2.29                                                
Epoch 41 - |param|=6.61e+02 |g_param|=3.38e+04 loss=5.2123e-01 ppl=1.68                                                 
Validation - loss=8.0907e-01 ppl=2.25 best_loss=7.9836e-01 best_ppl=2.22                                                
Epoch 42 - |param|=6.61e+02 |g_param|=2.99e+04 loss=4.9703e-01 ppl=1.64                                                 
Validation - loss=7.8320e-01 ppl=2.19 best_loss=7.9836e-01 best_ppl=2.22                                                
Epoch 43 - |param|=6.62e+02 |g_param|=2.75e+04 loss=4.6499e-01 ppl=1.59                                                 
Validation - loss=7.8210e-01 ppl=2.19 best_loss=7.8320e-01 best_ppl=2.19                                                
Epoch 44 - |param|=6.62e+02 |g_param|=2.70e+04 loss=4.7450e-01 ppl=1.61                                                 
Validation - loss=7.6349e-01 ppl=2.15 best_loss=7.8210e-01 best_ppl=2.19                                                
Epoch 45 - |param|=6.62e+02 |g_param|=2.60e+04 loss=4.5696e-01 ppl=1.58                                                 
Validation - loss=7.5306e-01 ppl=2.12 best_loss=7.6349e-01 best_ppl=2.15                                                
Epoch 46 - |param|=6.63e+02 |g_param|=3.26e+04 loss=4.5417e-01 ppl=1.57                                                 
Validation - loss=7.7512e-01 ppl=2.17 best_loss=7.5306e-01 best_ppl=2.12                                                
Epoch 47 - |param|=6.63e+02 |g_param|=3.41e+04 loss=4.6509e-01 ppl=1.59                                                 
Validation - loss=7.6742e-01 ppl=2.15 best_loss=7.5306e-01 best_ppl=2.12                                                
Epoch 48 - |param|=6.63e+02 |g_param|=5.28e+04 loss=4.3002e-01 ppl=1.54                                                 
Validation - loss=7.6204e-01 ppl=2.14 best_loss=7.5306e-01 best_ppl=2.12                                                
Epoch 49 - |param|=6.64e+02 |g_param|=4.77e+04 loss=4.0954e-01 ppl=1.51                                                 
Validation - loss=7.5805e-01 ppl=2.13 best_loss=7.5306e-01 best_ppl=2.12                                                
Epoch 50 - |param|=6.64e+02 |g_param|=4.98e+04 loss=4.1940e-01 ppl=1.52                                                 
Validation - loss=7.4077e-01 ppl=2.10 best_loss=7.5306e-01 best_ppl=2.12                                                

real	9m33.740s
user	9m24.878s
sys	0m8.303s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-50epoch$ ./test-eval-loop.sh 
Evaluation result for the model: seq-model-myrk.01.4.42-83.18.4.06-58.09.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.6/1.8/0.0/0.0 (BP=0.970, ratio=0.971, hyp_len=22485, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.4.15-63.73.3.85-47.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.3/2.2/0.0/0.0 (BP=1.000, ratio=1.024, hyp_len=23714, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.3.98-53.66.3.78-43.88.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.1/1.9/0.0/0.0 (BP=0.996, ratio=0.997, hyp_len=23079, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.92-50.24.3.66-38.85.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.8/2.3/0.0/0.0 (BP=1.000, ratio=1.008, hyp_len=23339, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.83-46.18.3.58-35.92.pth
BLEU = 0.63, 22.8/2.9/0.2/0.0 (BP=1.000, ratio=1.001, hyp_len=23189, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.69-40.12.3.51-33.43.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.2/2.9/0.1/0.0 (BP=1.000, ratio=1.017, hyp_len=23564, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.64-38.17.3.37-28.99.pth
BLEU = 1.02, 27.4/4.3/0.6/0.0 (BP=0.987, ratio=0.987, hyp_len=22868, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.3.39-29.70.3.22-24.99.pth
BLEU = 1.68, 29.1/5.6/0.9/0.1 (BP=1.000, ratio=1.006, hyp_len=23292, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.3.33-27.91.3.08-21.70.pth
BLEU = 2.71, 32.3/8.1/1.5/0.1 (BP=1.000, ratio=1.000, hyp_len=23157, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.3.12-22.58.2.96-19.38.pth
BLEU = 5.98, 36.2/11.4/3.4/0.9 (BP=0.996, ratio=0.996, hyp_len=23074, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.2.94-18.84.2.83-16.92.pth
BLEU = 7.91, 38.2/13.7/4.8/1.6 (BP=0.989, ratio=0.989, hyp_len=22903, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.2.77-15.90.2.68-14.56.pth
BLEU = 10.87, 40.0/17.0/7.1/2.9 (BP=1.000, ratio=1.000, hyp_len=23171, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.2.68-14.57.2.57-13.12.pth
BLEU = 11.66, 42.8/18.2/7.7/3.1 (BP=1.000, ratio=1.002, hyp_len=23213, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.2.54-12.65.2.42-11.24.pth
BLEU = 14.49, 46.9/22.1/9.9/4.4 (BP=0.991, ratio=0.991, hyp_len=22955, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.2.30-10.01.2.35-10.45.pth
BLEU = 15.98, 48.0/23.4/11.2/5.2 (BP=1.000, ratio=1.010, hyp_len=23398, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.2.21-9.14.2.16-8.71.pth
BLEU = 20.28, 53.1/28.6/15.0/7.6 (BP=0.994, ratio=0.994, hyp_len=23031, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.2.00-7.36.1.97-7.18.pth
BLEU = 23.18, 55.4/31.3/17.4/9.6 (BP=1.000, ratio=1.009, hyp_len=23370, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.81-6.13.1.85-6.36.pth
BLEU = 26.56, 58.5/34.9/20.6/11.9 (BP=1.000, ratio=1.008, hyp_len=23340, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.66-5.24.1.69-5.40.pth
BLEU = 32.51, 62.9/40.7/26.3/16.6 (BP=1.000, ratio=1.006, hyp_len=23290, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.62-5.07.1.65-5.22.pth
BLEU = 33.75, 63.5/41.9/27.5/17.7 (BP=1.000, ratio=1.027, hyp_len=23787, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.54-4.65.1.57-4.83.pth
BLEU = 36.88, 65.8/44.9/30.5/20.5 (BP=1.000, ratio=1.010, hyp_len=23402, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.1.37-3.94.1.47-4.37.pth
BLEU = 40.70, 68.5/48.3/34.3/24.2 (BP=1.000, ratio=1.009, hyp_len=23368, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.1.29-3.62.1.35-3.87.pth
BLEU = 46.79, 72.8/54.0/40.4/30.3 (BP=0.999, ratio=0.999, hyp_len=23143, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.1.21-3.34.1.27-3.58.pth
BLEU = 49.06, 74.1/56.0/42.8/32.6 (BP=1.000, ratio=1.009, hyp_len=23358, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.1.11-3.03.1.23-3.42.pth
BLEU = 51.76, 75.8/58.5/45.6/35.5 (BP=1.000, ratio=1.006, hyp_len=23299, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.1.05-2.84.1.18-3.26.pth
BLEU = 53.71, 76.7/60.2/47.7/37.8 (BP=1.000, ratio=1.017, hyp_len=23558, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.1.08-2.93.1.13-3.09.pth
BLEU = 54.98, 77.7/61.3/49.0/39.2 (BP=1.000, ratio=1.011, hyp_len=23411, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.95-2.60.1.08-2.93.pth
BLEU = 58.83, 79.9/64.8/53.1/43.6 (BP=1.000, ratio=1.012, hyp_len=23446, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.85-2.35.1.02-2.77.pth
BLEU = 60.71, 80.9/66.5/55.1/45.8 (BP=1.000, ratio=1.016, hyp_len=23526, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.84-2.31.0.98-2.67.pth
BLEU = 62.27, 81.8/67.8/56.8/47.8 (BP=1.000, ratio=1.012, hyp_len=23434, ref_len=23160)
Evaluation result for the model: seq-model-myrk.31.0.77-2.16.0.97-2.65.pth
BLEU = 64.15, 82.9/69.5/58.8/49.9 (BP=1.000, ratio=1.009, hyp_len=23373, ref_len=23160)
Evaluation result for the model: seq-model-myrk.32.0.79-2.21.0.94-2.55.pth
BLEU = 64.17, 82.8/69.6/58.8/50.0 (BP=1.000, ratio=1.015, hyp_len=23501, ref_len=23160)
Evaluation result for the model: seq-model-myrk.33.0.71-2.04.0.91-2.48.pth
BLEU = 65.79, 83.7/70.9/60.6/52.1 (BP=1.000, ratio=1.011, hyp_len=23419, ref_len=23160)
Evaluation result for the model: seq-model-myrk.34.0.72-2.06.0.89-2.45.pth
BLEU = 65.83, 83.7/71.1/60.7/52.0 (BP=1.000, ratio=1.018, hyp_len=23581, ref_len=23160)
Evaluation result for the model: seq-model-myrk.35.0.65-1.92.0.88-2.42.pth
BLEU = 66.38, 83.7/71.4/61.4/52.9 (BP=1.000, ratio=1.017, hyp_len=23561, ref_len=23160)
Evaluation result for the model: seq-model-myrk.36.0.62-1.86.0.87-2.38.pth
BLEU = 68.47, 85.2/73.2/63.5/55.5 (BP=1.000, ratio=1.011, hyp_len=23425, ref_len=23160)
Evaluation result for the model: seq-model-myrk.37.0.64-1.90.0.87-2.39.pth
BLEU = 67.60, 84.6/72.7/62.6/54.3 (BP=1.000, ratio=1.022, hyp_len=23665, ref_len=23160)
Evaluation result for the model: seq-model-myrk.38.0.59-1.80.0.84-2.33.pth
BLEU = 68.35, 84.9/73.2/63.5/55.3 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: seq-model-myrk.39.0.55-1.74.0.83-2.29.pth
BLEU = 69.57, 85.5/74.1/64.9/57.0 (BP=1.000, ratio=1.015, hyp_len=23518, ref_len=23160)
Evaluation result for the model: seq-model-myrk.40.0.55-1.73.0.80-2.22.pth
BLEU = 70.21, 85.9/74.7/65.6/57.7 (BP=1.000, ratio=1.020, hyp_len=23622, ref_len=23160)
Evaluation result for the model: seq-model-myrk.41.0.52-1.68.0.81-2.25.pth
BLEU = 71.37, 86.5/75.7/66.8/59.3 (BP=1.000, ratio=1.013, hyp_len=23469, ref_len=23160)
Evaluation result for the model: seq-model-myrk.42.0.50-1.64.0.78-2.19.pth
BLEU = 71.59, 86.5/75.9/67.1/59.6 (BP=1.000, ratio=1.017, hyp_len=23560, ref_len=23160)
Evaluation result for the model: seq-model-myrk.43.0.46-1.59.0.78-2.19.pth
BLEU = 71.81, 86.5/76.0/67.4/60.0 (BP=1.000, ratio=1.019, hyp_len=23606, ref_len=23160)
Evaluation result for the model: seq-model-myrk.44.0.47-1.61.0.76-2.15.pth
BLEU = 71.95, 86.6/76.1/67.5/60.3 (BP=1.000, ratio=1.021, hyp_len=23640, ref_len=23160)
Evaluation result for the model: seq-model-myrk.45.0.46-1.58.0.75-2.12.pth
BLEU = 72.68, 87.1/76.8/68.3/61.1 (BP=1.000, ratio=1.016, hyp_len=23538, ref_len=23160)
Evaluation result for the model: seq-model-myrk.46.0.45-1.57.0.78-2.17.pth
BLEU = 72.13, 86.6/76.3/67.7/60.5 (BP=1.000, ratio=1.025, hyp_len=23742, ref_len=23160)
Evaluation result for the model: seq-model-myrk.47.0.47-1.59.0.77-2.15.pth
BLEU = 72.84, 87.1/76.9/68.5/61.3 (BP=1.000, ratio=1.016, hyp_len=23534, ref_len=23160)
Evaluation result for the model: seq-model-myrk.48.0.43-1.54.0.76-2.14.pth
BLEU = 73.15, 87.2/77.1/68.9/61.8 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
Evaluation result for the model: seq-model-myrk.49.0.41-1.51.0.76-2.13.pth
BLEU = 72.69, 87.0/76.9/68.3/61.1 (BP=1.000, ratio=1.024, hyp_len=23724, ref_len=23160)
Evaluation result for the model: seq-model-myrk.50.0.42-1.52.0.74-2.10.pth
BLEU = 72.69, 86.8/76.8/68.4/61.2 (BP=1.000, ratio=1.027, hyp_len=23785, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-50epoch$
```

Best core of seq2seq 50 model က ...  

```
Evaluation result for the model: seq-model-myrk.48.0.43-1.54.0.76-2.14.pth
BLEU = 73.15, 87.2/77.1/68.9/61.8 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
```

## seq2seq 60 epoch model, my-rk

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 60 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.pth',
    'n_epochs': 60,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 1 - |param|=6.43e+02 |g_param|=2.25e+05 loss=4.4902e+00 ppl=89.14                                                 
Validation - loss=4.0528e+00 ppl=57.56 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.43e+02 |g_param|=1.67e+05 loss=4.1113e+00 ppl=61.02                                                 
Validation - loss=3.8801e+00 ppl=48.43 best_loss=4.0528e+00 best_ppl=57.56                                              
Epoch 3 - |param|=6.43e+02 |g_param|=1.59e+05 loss=4.0564e+00 ppl=57.77                                                 
Validation - loss=3.7609e+00 ppl=42.99 best_loss=3.8801e+00 best_ppl=48.43                                              
Epoch 4 - |param|=6.43e+02 |g_param|=1.83e+05 loss=3.9085e+00 ppl=49.82                                                 
Validation - loss=3.6466e+00 ppl=38.34 best_loss=3.7609e+00 best_ppl=42.99                                              
Epoch 5 - |param|=6.43e+02 |g_param|=1.88e+05 loss=3.7751e+00 ppl=43.60                                                 
Validation - loss=3.5334e+00 ppl=34.24 best_loss=3.6466e+00 best_ppl=38.34                                              
Epoch 6 - |param|=6.44e+02 |g_param|=1.95e+05 loss=3.6745e+00 ppl=39.43                                                 
Validation - loss=3.4203e+00 ppl=30.58 best_loss=3.5334e+00 best_ppl=34.24                                              
Epoch 7 - |param|=6.44e+02 |g_param|=1.81e+05 loss=3.5812e+00 ppl=35.92                                                 
Validation - loss=3.3062e+00 ppl=27.28 best_loss=3.4203e+00 best_ppl=30.58                                              
Epoch 8 - |param|=6.45e+02 |g_param|=1.27e+05 loss=3.4357e+00 ppl=31.05                                                 
Validation - loss=3.2097e+00 ppl=24.77 best_loss=3.3062e+00 best_ppl=27.28                                              
Epoch 9 - |param|=6.46e+02 |g_param|=1.20e+05 loss=3.3011e+00 ppl=27.14                                                 
Validation - loss=3.1518e+00 ppl=23.38 best_loss=3.2097e+00 best_ppl=24.77                                              
Epoch 10 - |param|=6.47e+02 |g_param|=9.85e+04 loss=3.1338e+00 ppl=22.96                                                
Validation - loss=2.8919e+00 ppl=18.03 best_loss=3.1518e+00 best_ppl=23.38                                              
Epoch 11 - |param|=6.47e+02 |g_param|=9.85e+04 loss=2.9007e+00 ppl=18.19                                                
Validation - loss=2.7478e+00 ppl=15.61 best_loss=2.8919e+00 best_ppl=18.03                                              
Epoch 12 - |param|=6.48e+02 |g_param|=9.92e+04 loss=2.7968e+00 ppl=16.39                                                
Validation - loss=2.6030e+00 ppl=13.50 best_loss=2.7478e+00 best_ppl=15.61                                              
Epoch 13 - |param|=6.49e+02 |g_param|=1.10e+05 loss=2.6534e+00 ppl=14.20                                                
Validation - loss=2.4910e+00 ppl=12.07 best_loss=2.6030e+00 best_ppl=13.50                                              
Epoch 14 - |param|=6.50e+02 |g_param|=9.42e+04 loss=2.4747e+00 ppl=11.88                                                
Validation - loss=2.3465e+00 ppl=10.45 best_loss=2.4910e+00 best_ppl=12.07                                              
Epoch 15 - |param|=6.50e+02 |g_param|=1.14e+05 loss=2.3445e+00 ppl=10.43                                                
Validation - loss=2.1782e+00 ppl=8.83 best_loss=2.3465e+00 best_ppl=10.45                                               
Epoch 16 - |param|=6.51e+02 |g_param|=1.31e+05 loss=2.0804e+00 ppl=8.01                                                 
Validation - loss=1.9634e+00 ppl=7.12 best_loss=2.1782e+00 best_ppl=8.83                                                
Epoch 17 - |param|=6.52e+02 |g_param|=1.39e+05 loss=1.8380e+00 ppl=6.28                                                 
Validation - loss=1.7654e+00 ppl=5.84 best_loss=1.9634e+00 best_ppl=7.12                                                
Epoch 18 - |param|=6.53e+02 |g_param|=1.47e+05 loss=1.6272e+00 ppl=5.09                                                 
Validation - loss=1.5829e+00 ppl=4.87 best_loss=1.7654e+00 best_ppl=5.84                                                
Epoch 19 - |param|=6.53e+02 |g_param|=1.16e+05 loss=1.4116e+00 ppl=4.10                                                 
Validation - loss=1.4401e+00 ppl=4.22 best_loss=1.5829e+00 best_ppl=4.87                                                
Epoch 20 - |param|=6.54e+02 |g_param|=1.00e+05 loss=1.3341e+00 ppl=3.80                                                 
Validation - loss=1.3696e+00 ppl=3.93 best_loss=1.4401e+00 best_ppl=4.22                                                
Epoch 21 - |param|=6.55e+02 |g_param|=9.54e+04 loss=1.2008e+00 ppl=3.32                                                 
Validation - loss=1.2757e+00 ppl=3.58 best_loss=1.3696e+00 best_ppl=3.93                                                
Epoch 22 - |param|=6.55e+02 |g_param|=9.02e+04 loss=1.0985e+00 ppl=3.00                                                 
Validation - loss=1.1523e+00 ppl=3.17 best_loss=1.2757e+00 best_ppl=3.58                                                
Epoch 23 - |param|=6.56e+02 |g_param|=1.14e+05 loss=1.1158e+00 ppl=3.05                                                 
Validation - loss=1.1616e+00 ppl=3.20 best_loss=1.1523e+00 best_ppl=3.17                                                
Epoch 24 - |param|=6.56e+02 |g_param|=7.89e+04 loss=9.1402e-01 ppl=2.49                                                 
Validation - loss=1.0222e+00 ppl=2.78 best_loss=1.1523e+00 best_ppl=3.17                                                
Epoch 25 - |param|=6.57e+02 |g_param|=7.64e+04 loss=8.3609e-01 ppl=2.31                                                 
Validation - loss=9.8008e-01 ppl=2.66 best_loss=1.0222e+00 best_ppl=2.78                                                
Epoch 26 - |param|=6.57e+02 |g_param|=8.22e+04 loss=8.1952e-01 ppl=2.27                                                 
Validation - loss=9.4775e-01 ppl=2.58 best_loss=9.8008e-01 best_ppl=2.66                                                
Epoch 27 - |param|=6.58e+02 |g_param|=7.56e+04 loss=7.2717e-01 ppl=2.07                                                 
Validation - loss=8.9235e-01 ppl=2.44 best_loss=9.4775e-01 best_ppl=2.58                                                
Epoch 28 - |param|=6.58e+02 |g_param|=6.82e+04 loss=6.8145e-01 ppl=1.98                                                 
Validation - loss=8.6692e-01 ppl=2.38 best_loss=8.9235e-01 best_ppl=2.44                                                
Epoch 29 - |param|=6.59e+02 |g_param|=5.59e+04 loss=6.2931e-01 ppl=1.88                                                 
Validation - loss=8.3079e-01 ppl=2.30 best_loss=8.6692e-01 best_ppl=2.38                                                
Epoch 30 - |param|=6.59e+02 |g_param|=6.45e+04 loss=6.0363e-01 ppl=1.83                                                 
Validation - loss=8.2691e-01 ppl=2.29 best_loss=8.3079e-01 best_ppl=2.30                                                
Epoch 31 - |param|=6.60e+02 |g_param|=7.53e+04 loss=5.9305e-01 ppl=1.81                                                 
Validation - loss=8.2407e-01 ppl=2.28 best_loss=8.2691e-01 best_ppl=2.29                                                
Epoch 32 - |param|=6.60e+02 |g_param|=5.04e+04 loss=5.4923e-01 ppl=1.73                                                 
Validation - loss=7.8805e-01 ppl=2.20 best_loss=8.2407e-01 best_ppl=2.28                                                
Epoch 33 - |param|=6.60e+02 |g_param|=5.88e+04 loss=5.0410e-01 ppl=1.66                                                 
Validation - loss=7.6580e-01 ppl=2.15 best_loss=7.8805e-01 best_ppl=2.20                                                
Epoch 34 - |param|=6.61e+02 |g_param|=5.78e+04 loss=4.9573e-01 ppl=1.64                                                 
Validation - loss=7.4589e-01 ppl=2.11 best_loss=7.6580e-01 best_ppl=2.15                                                
Epoch 35 - |param|=6.61e+02 |g_param|=5.25e+04 loss=4.6908e-01 ppl=1.60                                                 
Validation - loss=7.3262e-01 ppl=2.08 best_loss=7.4589e-01 best_ppl=2.11                                                
Epoch 36 - |param|=6.62e+02 |g_param|=1.18e+05 loss=5.5160e-01 ppl=1.74                                                 
Validation - loss=7.8958e-01 ppl=2.20 best_loss=7.3262e-01 best_ppl=2.08                                                
Epoch 37 - |param|=6.62e+02 |g_param|=7.74e+04 loss=4.8855e-01 ppl=1.63                                                 
Validation - loss=7.4816e-01 ppl=2.11 best_loss=7.3262e-01 best_ppl=2.08                                                
Epoch 38 - |param|=6.63e+02 |g_param|=5.33e+04 loss=4.4200e-01 ppl=1.56                                                 
Validation - loss=7.2250e-01 ppl=2.06 best_loss=7.3262e-01 best_ppl=2.08                                                
Epoch 39 - |param|=6.63e+02 |g_param|=4.55e+04 loss=4.1148e-01 ppl=1.51                                                 
Validation - loss=7.2490e-01 ppl=2.06 best_loss=7.2250e-01 best_ppl=2.06                                                
Epoch 40 - |param|=6.63e+02 |g_param|=1.05e+05 loss=4.1009e-01 ppl=1.51                                                 
Validation - loss=7.0126e-01 ppl=2.02 best_loss=7.2250e-01 best_ppl=2.06                                                
Epoch 41 - |param|=6.64e+02 |g_param|=9.35e+04 loss=3.9570e-01 ppl=1.49                                                 
Validation - loss=6.8714e-01 ppl=1.99 best_loss=7.0126e-01 best_ppl=2.02                                                
Epoch 42 - |param|=6.64e+02 |g_param|=9.17e+04 loss=3.6078e-01 ppl=1.43                                                 
Validation - loss=6.8349e-01 ppl=1.98 best_loss=6.8714e-01 best_ppl=1.99                                                
Epoch 43 - |param|=6.64e+02 |g_param|=9.36e+04 loss=3.7720e-01 ppl=1.46                                                 
Validation - loss=6.7232e-01 ppl=1.96 best_loss=6.8349e-01 best_ppl=1.98                                                
Epoch 44 - |param|=6.64e+02 |g_param|=1.03e+05 loss=3.7234e-01 ppl=1.45                                                 
Validation - loss=6.9372e-01 ppl=2.00 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 45 - |param|=6.65e+02 |g_param|=1.20e+05 loss=3.5059e-01 ppl=1.42                                                 
Validation - loss=6.7533e-01 ppl=1.96 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 46 - |param|=6.65e+02 |g_param|=1.07e+05 loss=3.5109e-01 ppl=1.42                                                 
Validation - loss=7.0086e-01 ppl=2.02 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 47 - |param|=6.65e+02 |g_param|=9.80e+04 loss=3.3986e-01 ppl=1.40                                                 
Validation - loss=7.0070e-01 ppl=2.02 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 48 - |param|=6.66e+02 |g_param|=8.42e+04 loss=3.4504e-01 ppl=1.41                                                 
Validation - loss=6.7653e-01 ppl=1.97 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 49 - |param|=6.66e+02 |g_param|=6.70e+04 loss=3.6284e-01 ppl=1.44                                                 
Validation - loss=6.8220e-01 ppl=1.98 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 50 - |param|=6.66e+02 |g_param|=4.41e+04 loss=3.1134e-01 ppl=1.37                                                 
Validation - loss=6.6136e-01 ppl=1.94 best_loss=6.7232e-01 best_ppl=1.96                                                
Epoch 51 - |param|=6.67e+02 |g_param|=4.00e+04 loss=2.9443e-01 ppl=1.34                                                 
Validation - loss=6.6205e-01 ppl=1.94 best_loss=6.6136e-01 best_ppl=1.94                                                
Epoch 52 - |param|=6.67e+02 |g_param|=4.26e+04 loss=3.0282e-01 ppl=1.35                                                 
Validation - loss=6.6731e-01 ppl=1.95 best_loss=6.6136e-01 best_ppl=1.94                                                
Epoch 53 - |param|=6.67e+02 |g_param|=4.11e+04 loss=3.1418e-01 ppl=1.37                                                 
Validation - loss=6.7482e-01 ppl=1.96 best_loss=6.6136e-01 best_ppl=1.94                                                
Epoch 54 - |param|=6.68e+02 |g_param|=3.92e+04 loss=2.9289e-01 ppl=1.34                                                 
Validation - loss=6.6099e-01 ppl=1.94 best_loss=6.6136e-01 best_ppl=1.94                                                
Epoch 55 - |param|=6.68e+02 |g_param|=4.57e+04 loss=2.8611e-01 ppl=1.33                                                 
Validation - loss=6.4661e-01 ppl=1.91 best_loss=6.6099e-01 best_ppl=1.94                                                
Epoch 56 - |param|=6.68e+02 |g_param|=4.21e+04 loss=2.8883e-01 ppl=1.33                                                 
Validation - loss=6.5539e-01 ppl=1.93 best_loss=6.4661e-01 best_ppl=1.91                                                
Epoch 57 - |param|=6.69e+02 |g_param|=4.84e+04 loss=2.7527e-01 ppl=1.32                                                 
Validation - loss=6.5655e-01 ppl=1.93 best_loss=6.4661e-01 best_ppl=1.91                                                
Epoch 58 - |param|=6.69e+02 |g_param|=3.95e+04 loss=2.8506e-01 ppl=1.33                                                 
Validation - loss=6.5376e-01 ppl=1.92 best_loss=6.4661e-01 best_ppl=1.91                                                
Epoch 59 - |param|=6.69e+02 |g_param|=4.06e+04 loss=2.7647e-01 ppl=1.32                                                 
Validation - loss=6.5160e-01 ppl=1.92 best_loss=6.4661e-01 best_ppl=1.91                                                
Epoch 60 - |param|=6.70e+02 |g_param|=4.34e+04 loss=2.7444e-01 ppl=1.32                                                 
Validation - loss=6.6622e-01 ppl=1.95 best_loss=6.4661e-01 best_ppl=1.91                                                

real	11m28.447s
user	11m16.946s
sys	0m9.566s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation...  

```
Evaluation result for the model: seq-model-myrk.01.4.49-89.14.4.05-57.56.pth
BLEU = 0.00, 15.7/2.0/0.0/0.0 (BP=1.000, ratio=1.010, hyp_len=23402, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.4.11-61.02.3.88-48.43.pth
BLEU = 0.00, 21.7/2.0/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=23513, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.4.06-57.77.3.76-42.99.pth
BLEU = 0.00, 21.8/2.2/0.0/0.0 (BP=1.000, ratio=1.004, hyp_len=23246, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.91-49.82.3.65-38.34.pth
BLEU = 0.63, 24.3/3.9/0.2/0.0 (BP=1.000, ratio=1.004, hyp_len=23262, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.78-43.60.3.53-34.24.pth
BLEU = 0.68, 24.9/4.0/0.2/0.0 (BP=1.000, ratio=1.003, hyp_len=23229, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.67-39.43.3.42-30.58.pth
BLEU = 0.83, 26.8/5.5/0.6/0.0 (BP=1.000, ratio=1.021, hyp_len=23638, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.58-35.92.3.31-27.28.pth
BLEU = 2.10, 30.0/7.5/1.3/0.1 (BP=1.000, ratio=1.004, hyp_len=23261, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.3.44-31.05.3.21-24.77.pth
BLEU = 3.53, 32.1/9.8/2.2/0.2 (BP=1.000, ratio=1.006, hyp_len=23304, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.3.30-27.14.3.15-23.38.pth
BLEU = 4.81, 35.7/11.4/2.4/0.5 (BP=0.999, ratio=0.999, hyp_len=23146, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.3.13-22.96.2.89-18.03.pth
BLEU = 7.61, 39.6/14.8/4.6/1.3 (BP=0.997, ratio=0.997, hyp_len=23081, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.2.90-18.19.2.75-15.61.pth
BLEU = 9.56, 41.6/16.9/5.9/2.0 (BP=1.000, ratio=1.011, hyp_len=23406, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.2.80-16.39.2.60-13.50.pth
BLEU = 11.85, 43.7/19.5/7.7/3.0 (BP=1.000, ratio=1.007, hyp_len=23326, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.2.65-14.20.2.49-12.07.pth
BLEU = 13.09, 45.4/21.1/8.9/3.5 (BP=0.999, ratio=0.999, hyp_len=23134, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.2.47-11.88.2.35-10.45.pth
BLEU = 15.17, 48.0/23.2/10.5/4.5 (BP=1.000, ratio=1.005, hyp_len=23267, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.2.34-10.43.2.18-8.83.pth
BLEU = 18.23, 51.2/26.3/13.0/6.3 (BP=1.000, ratio=1.010, hyp_len=23396, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.2.08-8.01.1.96-7.12.pth
BLEU = 23.85, 56.5/32.1/18.0/9.9 (BP=1.000, ratio=1.000, hyp_len=23153, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.1.84-6.28.1.77-5.84.pth
BLEU = 30.06, 61.4/38.2/23.9/14.6 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.63-5.09.1.58-4.87.pth
BLEU = 36.92, 66.3/44.8/30.4/20.6 (BP=1.000, ratio=1.007, hyp_len=23324, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.41-4.10.1.44-4.22.pth
BLEU = 41.96, 69.9/49.7/35.3/25.3 (BP=1.000, ratio=1.008, hyp_len=23339, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.33-3.80.1.37-3.93.pth
BLEU = 44.90, 71.7/52.7/38.4/28.0 (BP=1.000, ratio=1.014, hyp_len=23491, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.20-3.32.1.28-3.58.pth
BLEU = 50.82, 75.4/57.8/44.5/34.4 (BP=1.000, ratio=1.007, hyp_len=23316, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.1.10-3.00.1.15-3.17.pth
BLEU = 53.83, 76.9/60.5/47.7/37.8 (BP=1.000, ratio=1.019, hyp_len=23598, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.1.12-3.05.1.16-3.20.pth
BLEU = 53.16, 76.5/60.0/47.0/37.0 (BP=1.000, ratio=1.026, hyp_len=23758, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.0.91-2.49.1.02-2.78.pth
BLEU = 60.83, 81.3/66.7/55.1/45.8 (BP=1.000, ratio=1.007, hyp_len=23324, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.0.84-2.31.0.98-2.66.pth
BLEU = 62.90, 82.3/68.4/57.5/48.4 (BP=1.000, ratio=1.013, hyp_len=23455, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.0.82-2.27.0.95-2.58.pth
BLEU = 64.07, 82.7/69.5/58.8/49.8 (BP=1.000, ratio=1.015, hyp_len=23512, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.0.73-2.07.0.89-2.44.pth
BLEU = 66.25, 84.0/71.3/61.1/52.6 (BP=1.000, ratio=1.016, hyp_len=23532, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.68-1.98.0.87-2.38.pth
BLEU = 66.67, 84.1/71.9/61.7/53.0 (BP=1.000, ratio=1.025, hyp_len=23736, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.63-1.88.0.83-2.30.pth
BLEU = 68.63, 85.2/73.5/63.8/55.6 (BP=1.000, ratio=1.019, hyp_len=23609, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.60-1.83.0.83-2.29.pth
BLEU = 68.86, 85.2/73.7/64.1/55.9 (BP=1.000, ratio=1.020, hyp_len=23634, ref_len=23160)
Evaluation result for the model: seq-model-myrk.31.0.59-1.81.0.82-2.28.pth
BLEU = 68.46, 84.9/73.3/63.7/55.4 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq-model-myrk.32.0.55-1.73.0.79-2.20.pth
BLEU = 70.47, 86.0/75.0/65.8/58.1 (BP=1.000, ratio=1.024, hyp_len=23720, ref_len=23160)
Evaluation result for the model: seq-model-myrk.33.0.50-1.66.0.77-2.15.pth
BLEU = 71.68, 86.5/76.0/67.3/59.7 (BP=1.000, ratio=1.021, hyp_len=23647, ref_len=23160)
Evaluation result for the model: seq-model-myrk.34.0.50-1.64.0.75-2.11.pth
BLEU = 71.84, 86.5/76.1/67.5/59.9 (BP=1.000, ratio=1.023, hyp_len=23689, ref_len=23160)
Evaluation result for the model: seq-model-myrk.35.0.47-1.60.0.73-2.08.pth
BLEU = 72.91, 87.2/77.0/68.6/61.3 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
Evaluation result for the model: seq-model-myrk.36.0.55-1.74.0.79-2.20.pth
BLEU = 70.67, 85.9/75.2/66.2/58.3 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: seq-model-myrk.37.0.49-1.63.0.75-2.11.pth
BLEU = 71.59, 86.5/75.9/67.1/59.5 (BP=1.000, ratio=1.025, hyp_len=23733, ref_len=23160)
Evaluation result for the model: seq-model-myrk.38.0.44-1.56.0.72-2.06.pth
BLEU = 72.98, 87.2/77.1/68.7/61.4 (BP=1.000, ratio=1.026, hyp_len=23760, ref_len=23160)
Evaluation result for the model: seq-model-myrk.39.0.41-1.51.0.72-2.06.pth
BLEU = 73.32, 87.1/77.3/69.1/62.0 (BP=1.000, ratio=1.025, hyp_len=23750, ref_len=23160)
Evaluation result for the model: seq-model-myrk.40.0.41-1.51.0.70-2.02.pth
BLEU = 73.53, 87.4/77.5/69.3/62.2 (BP=1.000, ratio=1.024, hyp_len=23718, ref_len=23160)
Evaluation result for the model: seq-model-myrk.41.0.40-1.49.0.69-1.99.pth
BLEU = 74.14, 87.8/78.1/70.0/63.0 (BP=1.000, ratio=1.021, hyp_len=23656, ref_len=23160)
Evaluation result for the model: seq-model-myrk.42.0.36-1.43.0.68-1.98.pth
BLEU = 73.57, 87.4/77.5/69.3/62.4 (BP=1.000, ratio=1.027, hyp_len=23782, ref_len=23160)
Evaluation result for the model: seq-model-myrk.43.0.38-1.46.0.67-1.96.pth
BLEU = 73.72, 87.4/77.7/69.6/62.6 (BP=1.000, ratio=1.028, hyp_len=23812, ref_len=23160)
Evaluation result for the model: seq-model-myrk.44.0.37-1.45.0.69-2.00.pth
BLEU = 74.21, 87.8/78.0/70.0/63.2 (BP=1.000, ratio=1.022, hyp_len=23668, ref_len=23160)
Evaluation result for the model: seq-model-myrk.45.0.35-1.42.0.68-1.96.pth
BLEU = 74.36, 87.6/78.1/70.3/63.5 (BP=1.000, ratio=1.024, hyp_len=23721, ref_len=23160)
Evaluation result for the model: seq-model-myrk.46.0.35-1.42.0.70-2.02.pth
BLEU = 73.42, 87.0/77.3/69.2/62.4 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-model-myrk.47.0.34-1.40.0.70-2.02.pth
BLEU = 73.97, 87.7/77.9/69.8/62.8 (BP=1.000, ratio=1.023, hyp_len=23696, ref_len=23160)
Evaluation result for the model: seq-model-myrk.48.0.35-1.41.0.68-1.97.pth
BLEU = 74.76, 88.0/78.5/70.7/64.0 (BP=1.000, ratio=1.024, hyp_len=23707, ref_len=23160)
Evaluation result for the model: seq-model-myrk.49.0.36-1.44.0.68-1.98.pth
BLEU = 73.28, 86.8/77.2/69.2/62.3 (BP=1.000, ratio=1.034, hyp_len=23945, ref_len=23160)
Evaluation result for the model: seq-model-myrk.50.0.31-1.37.0.66-1.94.pth
BLEU = 74.65, 87.8/78.4/70.6/63.9 (BP=1.000, ratio=1.024, hyp_len=23722, ref_len=23160)
Evaluation result for the model: seq-model-myrk.51.0.29-1.34.0.66-1.94.pth
BLEU = 74.04, 87.3/77.8/69.9/63.2 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)
Evaluation result for the model: seq-model-myrk.52.0.30-1.35.0.67-1.95.pth
BLEU = 74.10, 87.4/77.8/70.0/63.3 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq-model-myrk.53.0.31-1.37.0.67-1.96.pth
BLEU = 73.43, 87.2/77.3/69.2/62.4 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq-model-myrk.54.0.29-1.34.0.66-1.94.pth
BLEU = 74.59, 87.8/78.3/70.6/63.8 (BP=1.000, ratio=1.027, hyp_len=23779, ref_len=23160)
Evaluation result for the model: seq-model-myrk.55.0.29-1.33.0.65-1.91.pth
BLEU = 75.30, 88.3/79.0/71.3/64.7 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
Evaluation result for the model: seq-model-myrk.56.0.29-1.33.0.66-1.93.pth
BLEU = 73.62, 87.1/77.4/69.5/62.7 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq-model-myrk.57.0.28-1.32.0.66-1.93.pth
BLEU = 74.18, 87.6/78.0/70.0/63.3 (BP=1.000, ratio=1.027, hyp_len=23790, ref_len=23160)
Evaluation result for the model: seq-model-myrk.58.0.29-1.33.0.65-1.92.pth
BLEU = 74.37, 87.6/78.1/70.4/63.6 (BP=1.000, ratio=1.026, hyp_len=23759, ref_len=23160)
Evaluation result for the model: seq-model-myrk.59.0.28-1.32.0.65-1.92.pth
BLEU = 74.11, 87.4/77.8/70.0/63.4 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq-model-myrk.60.0.27-1.32.0.67-1.95.pth
BLEU = 73.82, 87.1/77.6/69.7/63.0 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
```

best score:  

```
Evaluation result for the model: seq-model-myrk.55.0.29-1.33.0.65-1.91.pth
BLEU = 75.30, 88.3/79.0/71.3/64.7 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
```

### seq2seq, 70 epoch model, my-rk

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 70 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.pth',
    'n_epochs': 70,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 1 - |param|=6.42e+02 |g_param|=1.75e+05 loss=4.4078e+00 ppl=82.09                                                 
Validation - loss=4.0440e+00 ppl=57.06 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.42e+02 |g_param|=8.66e+04 loss=4.1423e+00 ppl=62.95                                                 
Validation - loss=3.8898e+00 ppl=48.90 best_loss=4.0440e+00 best_ppl=57.06                                              
Epoch 3 - |param|=6.42e+02 |g_param|=8.31e+04 loss=3.9820e+00 ppl=53.62                                                 
Validation - loss=3.8488e+00 ppl=46.94 best_loss=3.8898e+00 best_ppl=48.90                                              
Epoch 4 - |param|=6.42e+02 |g_param|=8.77e+04 loss=3.9913e+00 ppl=54.12                                                 
Validation - loss=3.7880e+00 ppl=44.17 best_loss=3.8488e+00 best_ppl=46.94                                              
Epoch 5 - |param|=6.43e+02 |g_param|=9.37e+04 loss=3.9795e+00 ppl=53.49                                                 
Validation - loss=3.6494e+00 ppl=38.45 best_loss=3.7880e+00 best_ppl=44.17                                              
Epoch 6 - |param|=6.43e+02 |g_param|=8.69e+04 loss=3.8018e+00 ppl=44.78                                                 
Validation - loss=3.5561e+00 ppl=35.03 best_loss=3.6494e+00 best_ppl=38.45                                              
Epoch 7 - |param|=6.44e+02 |g_param|=8.22e+04 loss=3.6845e+00 ppl=39.83                                                 
Validation - loss=3.4275e+00 ppl=30.80 best_loss=3.5561e+00 best_ppl=35.03                                              
Epoch 8 - |param|=6.44e+02 |g_param|=8.77e+04 loss=3.4081e+00 ppl=30.21                                                 
Validation - loss=3.1745e+00 ppl=23.91 best_loss=3.4275e+00 best_ppl=30.80                                              
Epoch 9 - |param|=6.45e+02 |g_param|=1.04e+05 loss=3.1448e+00 ppl=23.22                                                 
Validation - loss=2.9767e+00 ppl=19.62 best_loss=3.1745e+00 best_ppl=23.91                                              
Epoch 10 - |param|=6.46e+02 |g_param|=1.73e+05 loss=2.9526e+00 ppl=19.16                                                
Validation - loss=2.8185e+00 ppl=16.75 best_loss=2.9767e+00 best_ppl=19.62                                              
Epoch 11 - |param|=6.46e+02 |g_param|=1.56e+05 loss=2.6810e+00 ppl=14.60                                                
Validation - loss=2.5356e+00 ppl=12.62 best_loss=2.8185e+00 best_ppl=16.75                                              
Epoch 12 - |param|=6.47e+02 |g_param|=1.62e+05 loss=2.4421e+00 ppl=11.50                                                
Validation - loss=2.3619e+00 ppl=10.61 best_loss=2.5356e+00 best_ppl=12.62                                              
Epoch 13 - |param|=6.48e+02 |g_param|=2.03e+05 loss=2.2878e+00 ppl=9.85                                                 
Validation - loss=2.1871e+00 ppl=8.91 best_loss=2.3619e+00 best_ppl=10.61                                               
Epoch 14 - |param|=6.48e+02 |g_param|=2.45e+05 loss=2.1576e+00 ppl=8.65                                                 
Validation - loss=2.1096e+00 ppl=8.24 best_loss=2.1871e+00 best_ppl=8.91                                                
Epoch 15 - |param|=6.49e+02 |g_param|=1.57e+05 loss=2.1530e+00 ppl=8.61                                                 
Validation - loss=2.0532e+00 ppl=7.79 best_loss=2.1096e+00 best_ppl=8.24                                                
Epoch 16 - |param|=6.50e+02 |g_param|=1.17e+05 loss=1.9089e+00 ppl=6.75                                                 
Validation - loss=1.8692e+00 ppl=6.48 best_loss=2.0532e+00 best_ppl=7.79                                                
Epoch 17 - |param|=6.50e+02 |g_param|=1.13e+05 loss=1.8088e+00 ppl=6.10                                                 
Validation - loss=1.7888e+00 ppl=5.98 best_loss=1.8692e+00 best_ppl=6.48                                                
Epoch 18 - |param|=6.51e+02 |g_param|=9.96e+04 loss=1.6285e+00 ppl=5.10                                                 
Validation - loss=1.6539e+00 ppl=5.23 best_loss=1.7888e+00 best_ppl=5.98                                                
Epoch 19 - |param|=6.52e+02 |g_param|=1.16e+05 loss=1.5010e+00 ppl=4.49                                                 
Validation - loss=1.5868e+00 ppl=4.89 best_loss=1.6539e+00 best_ppl=5.23                                                
Epoch 20 - |param|=6.52e+02 |g_param|=1.30e+05 loss=1.4385e+00 ppl=4.21                                                 
Validation - loss=1.4859e+00 ppl=4.42 best_loss=1.5868e+00 best_ppl=4.89                                                
Epoch 21 - |param|=6.53e+02 |g_param|=1.15e+05 loss=1.3061e+00 ppl=3.69                                                 
Validation - loss=1.4270e+00 ppl=4.17 best_loss=1.4859e+00 best_ppl=4.42                                                
Epoch 22 - |param|=6.53e+02 |g_param|=6.67e+04 loss=1.2406e+00 ppl=3.46                                                 
Validation - loss=1.3680e+00 ppl=3.93 best_loss=1.4270e+00 best_ppl=4.17                                                
Epoch 23 - |param|=6.54e+02 |g_param|=4.93e+04 loss=1.1818e+00 ppl=3.26                                                 
Validation - loss=1.2711e+00 ppl=3.56 best_loss=1.3680e+00 best_ppl=3.93                                                
Epoch 24 - |param|=6.54e+02 |g_param|=5.63e+04 loss=1.0654e+00 ppl=2.90                                                 
Validation - loss=1.2229e+00 ppl=3.40 best_loss=1.2711e+00 best_ppl=3.56                                                
Epoch 25 - |param|=6.55e+02 |g_param|=7.22e+04 loss=1.0454e+00 ppl=2.84                                                 
Validation - loss=1.1996e+00 ppl=3.32 best_loss=1.2229e+00 best_ppl=3.40                                                
Epoch 26 - |param|=6.55e+02 |g_param|=6.27e+04 loss=1.0283e+00 ppl=2.80                                                 
Validation - loss=1.1514e+00 ppl=3.16 best_loss=1.1996e+00 best_ppl=3.32                                                
Epoch 27 - |param|=6.56e+02 |g_param|=6.65e+04 loss=9.3246e-01 ppl=2.54                                                 
Validation - loss=1.1047e+00 ppl=3.02 best_loss=1.1514e+00 best_ppl=3.16                                                
Epoch 28 - |param|=6.56e+02 |g_param|=4.18e+04 loss=8.5275e-01 ppl=2.35                                                 
Validation - loss=1.0648e+00 ppl=2.90 best_loss=1.1047e+00 best_ppl=3.02                                                
Epoch 29 - |param|=6.57e+02 |g_param|=6.13e+04 loss=8.6296e-01 ppl=2.37                                                 
Validation - loss=1.0136e+00 ppl=2.76 best_loss=1.0648e+00 best_ppl=2.90                                                
Epoch 30 - |param|=6.57e+02 |g_param|=5.18e+04 loss=8.3761e-01 ppl=2.31                                                 
Validation - loss=1.0017e+00 ppl=2.72 best_loss=1.0136e+00 best_ppl=2.76                                                
Epoch 31 - |param|=6.58e+02 |g_param|=4.24e+04 loss=7.3188e-01 ppl=2.08                                                 
Validation - loss=9.7036e-01 ppl=2.64 best_loss=1.0017e+00 best_ppl=2.72                                                
Epoch 32 - |param|=6.58e+02 |g_param|=4.86e+04 loss=7.2814e-01 ppl=2.07                                                 
Validation - loss=9.5446e-01 ppl=2.60 best_loss=9.7036e-01 best_ppl=2.64                                                
Epoch 33 - |param|=6.58e+02 |g_param|=4.40e+04 loss=6.9362e-01 ppl=2.00                                                 
Validation - loss=9.3911e-01 ppl=2.56 best_loss=9.5446e-01 best_ppl=2.60                                                
Epoch 34 - |param|=6.59e+02 |g_param|=3.12e+04 loss=6.4987e-01 ppl=1.92                                                 
Validation - loss=9.1627e-01 ppl=2.50 best_loss=9.3911e-01 best_ppl=2.56                                                
Epoch 35 - |param|=6.59e+02 |g_param|=2.73e+04 loss=6.1090e-01 ppl=1.84                                                 
Validation - loss=9.0386e-01 ppl=2.47 best_loss=9.1627e-01 best_ppl=2.50                                                
Epoch 36 - |param|=6.60e+02 |g_param|=4.46e+04 loss=6.2717e-01 ppl=1.87                                                 
Validation - loss=8.9829e-01 ppl=2.46 best_loss=9.0386e-01 best_ppl=2.47                                                
Epoch 37 - |param|=6.60e+02 |g_param|=4.00e+04 loss=5.7143e-01 ppl=1.77                                                 
Validation - loss=9.0539e-01 ppl=2.47 best_loss=8.9829e-01 best_ppl=2.46                                                
Epoch 38 - |param|=6.60e+02 |g_param|=3.63e+04 loss=5.6585e-01 ppl=1.76                                                 
Validation - loss=8.6911e-01 ppl=2.38 best_loss=8.9829e-01 best_ppl=2.46                                                
Epoch 39 - |param|=6.61e+02 |g_param|=3.63e+04 loss=5.5134e-01 ppl=1.74                                                 
Validation - loss=8.6188e-01 ppl=2.37 best_loss=8.6911e-01 best_ppl=2.38                                                
Epoch 40 - |param|=6.61e+02 |g_param|=4.26e+04 loss=5.3834e-01 ppl=1.71                                                 
Validation - loss=8.5978e-01 ppl=2.36 best_loss=8.6188e-01 best_ppl=2.37                                                
Epoch 41 - |param|=6.61e+02 |g_param|=2.88e+04 loss=5.0212e-01 ppl=1.65                                                 
Validation - loss=8.2708e-01 ppl=2.29 best_loss=8.5978e-01 best_ppl=2.36                                                
Epoch 42 - |param|=6.62e+02 |g_param|=6.65e+04 loss=5.0112e-01 ppl=1.65                                                 
Validation - loss=8.5470e-01 ppl=2.35 best_loss=8.2708e-01 best_ppl=2.29                                                
Epoch 43 - |param|=6.62e+02 |g_param|=3.56e+04 loss=4.8598e-01 ppl=1.63                                                 
Validation - loss=8.2141e-01 ppl=2.27 best_loss=8.2708e-01 best_ppl=2.29                                                
Epoch 44 - |param|=6.62e+02 |g_param|=2.51e+04 loss=4.4666e-01 ppl=1.56                                                 
Validation - loss=8.1746e-01 ppl=2.26 best_loss=8.2141e-01 best_ppl=2.27                                                
Epoch 45 - |param|=6.63e+02 |g_param|=3.61e+04 loss=4.8115e-01 ppl=1.62                                                 
Validation - loss=8.1646e-01 ppl=2.26 best_loss=8.1746e-01 best_ppl=2.26                                                
Epoch 46 - |param|=6.63e+02 |g_param|=6.34e+04 loss=6.5702e-01 ppl=1.93                                                 
Validation - loss=8.9507e-01 ppl=2.45 best_loss=8.1646e-01 best_ppl=2.26                                                
Epoch 47 - |param|=6.64e+02 |g_param|=2.07e+04 loss=5.0557e-01 ppl=1.66                                                 
Validation - loss=8.3874e-01 ppl=2.31 best_loss=8.1646e-01 best_ppl=2.26                                                
Epoch 48 - |param|=6.64e+02 |g_param|=1.92e+04 loss=4.5699e-01 ppl=1.58                                                 
Validation - loss=8.1545e-01 ppl=2.26 best_loss=8.1646e-01 best_ppl=2.26                                                
Epoch 49 - |param|=6.64e+02 |g_param|=1.51e+04 loss=4.3976e-01 ppl=1.55                                                 
Validation - loss=8.1577e-01 ppl=2.26 best_loss=8.1545e-01 best_ppl=2.26                                                
Epoch 50 - |param|=6.65e+02 |g_param|=1.35e+04 loss=4.2987e-01 ppl=1.54                                                 
Validation - loss=7.8001e-01 ppl=2.18 best_loss=8.1545e-01 best_ppl=2.26                                                
Epoch 51 - |param|=6.65e+02 |g_param|=1.27e+04 loss=4.0882e-01 ppl=1.51                                                 
Validation - loss=7.7018e-01 ppl=2.16 best_loss=7.8001e-01 best_ppl=2.18                                                
Epoch 52 - |param|=6.65e+02 |g_param|=1.18e+04 loss=4.1265e-01 ppl=1.51                                                 
Validation - loss=7.8173e-01 ppl=2.19 best_loss=7.7018e-01 best_ppl=2.16                                                
Epoch 53 - |param|=6.66e+02 |g_param|=1.65e+04 loss=4.0372e-01 ppl=1.50                                                 
Validation - loss=7.8722e-01 ppl=2.20 best_loss=7.7018e-01 best_ppl=2.16                                                
Epoch 54 - |param|=6.66e+02 |g_param|=1.77e+04 loss=4.0541e-01 ppl=1.50                                                 
Validation - loss=7.8456e-01 ppl=2.19 best_loss=7.7018e-01 best_ppl=2.16                                                
Epoch 55 - |param|=6.66e+02 |g_param|=1.26e+04 loss=3.7720e-01 ppl=1.46                                                 
Validation - loss=7.6827e-01 ppl=2.16 best_loss=7.7018e-01 best_ppl=2.16                                                
Epoch 56 - |param|=6.67e+02 |g_param|=1.48e+04 loss=3.8595e-01 ppl=1.47                                                 
Validation - loss=7.7448e-01 ppl=2.17 best_loss=7.6827e-01 best_ppl=2.16                                                
Epoch 57 - |param|=6.67e+02 |g_param|=1.45e+04 loss=3.6520e-01 ppl=1.44                                                 
Validation - loss=7.7779e-01 ppl=2.18 best_loss=7.6827e-01 best_ppl=2.16                                                
Epoch 58 - |param|=6.67e+02 |g_param|=1.53e+04 loss=3.6419e-01 ppl=1.44                                                 
Validation - loss=7.8122e-01 ppl=2.18 best_loss=7.6827e-01 best_ppl=2.16                                                
Epoch 59 - |param|=6.67e+02 |g_param|=1.23e+04 loss=3.5235e-01 ppl=1.42                                                 
Validation - loss=7.5708e-01 ppl=2.13 best_loss=7.6827e-01 best_ppl=2.16                                                
Epoch 60 - |param|=6.68e+02 |g_param|=1.53e+04 loss=3.5140e-01 ppl=1.42                                                 
Validation - loss=7.5470e-01 ppl=2.13 best_loss=7.5708e-01 best_ppl=2.13                                                
Epoch 61 - |param|=6.68e+02 |g_param|=1.42e+04 loss=3.3421e-01 ppl=1.40                                                 
Validation - loss=7.7374e-01 ppl=2.17 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 62 - |param|=6.68e+02 |g_param|=1.12e+04 loss=3.1844e-01 ppl=1.37                                                 
Validation - loss=7.7832e-01 ppl=2.18 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 63 - |param|=6.69e+02 |g_param|=1.22e+04 loss=3.4662e-01 ppl=1.41                                                 
Validation - loss=7.5836e-01 ppl=2.13 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 64 - |param|=6.69e+02 |g_param|=1.46e+04 loss=3.2991e-01 ppl=1.39                                                 
Validation - loss=7.7666e-01 ppl=2.17 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 65 - |param|=6.69e+02 |g_param|=1.48e+04 loss=3.3896e-01 ppl=1.40                                                 
Validation - loss=7.6977e-01 ppl=2.16 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 66 - |param|=6.70e+02 |g_param|=2.52e+04 loss=3.7975e-01 ppl=1.46                                                 
Validation - loss=7.9584e-01 ppl=2.22 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 67 - |param|=6.70e+02 |g_param|=7.46e+04 loss=4.1237e-01 ppl=1.51                                                 
Validation - loss=7.8485e-01 ppl=2.19 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 68 - |param|=6.71e+02 |g_param|=2.29e+04 loss=3.6023e-01 ppl=1.43                                                 
Validation - loss=7.3703e-01 ppl=2.09 best_loss=7.5470e-01 best_ppl=2.13                                                
Epoch 69 - |param|=6.71e+02 |g_param|=2.16e+04 loss=3.4479e-01 ppl=1.41                                                 
Validation - loss=7.6357e-01 ppl=2.15 best_loss=7.3703e-01 best_ppl=2.09                                                
Epoch 70 - |param|=6.71e+02 |g_param|=7.13e+03 loss=3.2805e-01 ppl=1.39                                                 
Validation - loss=7.3365e-01 ppl=2.08 best_loss=7.3703e-01 best_ppl=2.09                                                

real	13m13.895s
user	13m3.064s
sys	0m10.725s
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-myrk.01.4.41-82.09.4.04-57.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 12.8/0.1/0.0/0.0 (BP=1.000, ratio=1.070, hyp_len=24788, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.4.14-62.95.3.89-48.90.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.2/2.0/0.0/0.0 (BP=0.985, ratio=0.986, hyp_len=22825, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.3.98-53.62.3.85-46.94.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.4/1.8/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=23332, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.99-54.12.3.79-44.17.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.1/1.7/0.0/0.0 (BP=1.000, ratio=1.018, hyp_len=23566, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.98-53.49.3.65-38.45.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.2/2.5/0.1/0.0 (BP=1.000, ratio=1.007, hyp_len=23313, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.80-44.78.3.56-35.03.pth
BLEU = 1.98, 26.9/5.7/1.0/0.1 (BP=1.000, ratio=1.014, hyp_len=23494, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.68-39.83.3.43-30.80.pth
BLEU = 2.22, 28.6/6.7/1.1/0.1 (BP=1.000, ratio=1.006, hyp_len=23298, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.3.41-30.21.3.17-23.91.pth
BLEU = 3.63, 33.2/10.2/2.1/0.2 (BP=0.999, ratio=0.999, hyp_len=23129, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.3.14-23.22.2.98-19.62.pth
BLEU = 6.42, 38.5/13.7/3.6/0.9 (BP=1.000, ratio=1.002, hyp_len=23204, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.2.95-19.16.2.82-16.75.pth
BLEU = 9.22, 41.0/16.8/5.7/1.9 (BP=1.000, ratio=1.014, hyp_len=23473, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.2.68-14.60.2.54-12.62.pth
BLEU = 13.27, 45.2/20.6/8.8/3.8 (BP=1.000, ratio=1.000, hyp_len=23162, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.2.44-11.50.2.36-10.61.pth
BLEU = 16.30, 49.2/24.3/11.3/5.2 (BP=1.000, ratio=1.010, hyp_len=23381, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.2.29-9.85.2.19-8.91.pth
BLEU = 20.61, 53.3/28.7/15.1/7.8 (BP=1.000, ratio=1.010, hyp_len=23392, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.2.16-8.65.2.11-8.24.pth
BLEU = 22.83, 56.0/31.4/17.0/9.1 (BP=1.000, ratio=1.014, hyp_len=23473, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.2.15-8.61.2.05-7.79.pth
BLEU = 23.30, 56.4/31.7/17.4/9.4 (BP=1.000, ratio=1.021, hyp_len=23656, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.1.91-6.75.1.87-6.48.pth
BLEU = 29.19, 61.0/37.6/22.9/13.8 (BP=1.000, ratio=1.011, hyp_len=23422, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.1.81-6.10.1.79-5.98.pth
BLEU = 32.36, 63.9/40.7/26.0/16.4 (BP=0.997, ratio=0.997, hyp_len=23093, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.63-5.10.1.65-5.23.pth
BLEU = 37.05, 66.5/45.0/30.4/20.7 (BP=1.000, ratio=1.013, hyp_len=23451, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.50-4.49.1.59-4.89.pth
BLEU = 40.32, 68.9/48.0/33.8/23.7 (BP=1.000, ratio=1.007, hyp_len=23318, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.44-4.21.1.49-4.42.pth
BLEU = 43.17, 70.8/50.9/36.6/26.4 (BP=1.000, ratio=1.012, hyp_len=23439, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.31-3.69.1.43-4.17.pth
BLEU = 45.63, 72.4/53.2/39.1/28.8 (BP=1.000, ratio=1.006, hyp_len=23295, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.1.24-3.46.1.37-3.93.pth
BLEU = 47.68, 73.5/55.0/41.3/31.0 (BP=1.000, ratio=1.006, hyp_len=23310, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.1.18-3.26.1.27-3.56.pth
BLEU = 52.37, 76.3/59.1/46.2/36.1 (BP=1.000, ratio=1.011, hyp_len=23419, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.1.07-2.90.1.22-3.40.pth
BLEU = 54.38, 77.4/61.0/48.3/38.3 (BP=1.000, ratio=1.017, hyp_len=23544, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.1.05-2.84.1.20-3.32.pth
BLEU = 54.53, 77.5/61.2/48.5/38.4 (BP=1.000, ratio=1.026, hyp_len=23771, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.1.03-2.80.1.15-3.16.pth
BLEU = 56.06, 78.4/62.5/50.1/40.2 (BP=1.000, ratio=1.017, hyp_len=23555, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.0.93-2.54.1.10-3.02.pth
BLEU = 60.06, 80.8/66.2/54.3/44.8 (BP=1.000, ratio=1.010, hyp_len=23397, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.85-2.35.1.06-2.90.pth
BLEU = 60.67, 80.4/66.5/55.2/46.0 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.86-2.37.1.01-2.76.pth
BLEU = 62.52, 81.9/68.3/57.1/47.8 (BP=1.000, ratio=1.019, hyp_len=23594, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.84-2.31.1.00-2.72.pth
BLEU = 64.45, 83.1/70.0/59.1/50.2 (BP=1.000, ratio=1.017, hyp_len=23552, ref_len=23160)
Evaluation result for the model: seq-model-myrk.31.0.73-2.08.0.97-2.64.pth
BLEU = 66.57, 84.4/71.7/61.5/52.8 (BP=1.000, ratio=1.008, hyp_len=23340, ref_len=23160)
Evaluation result for the model: seq-model-myrk.32.0.73-2.07.0.95-2.60.pth
BLEU = 67.35, 84.6/72.3/62.3/54.0 (BP=1.000, ratio=1.013, hyp_len=23456, ref_len=23160)
Evaluation result for the model: seq-model-myrk.33.0.69-2.00.0.94-2.56.pth
BLEU = 67.82, 84.9/72.8/62.8/54.5 (BP=1.000, ratio=1.015, hyp_len=23498, ref_len=23160)
Evaluation result for the model: seq-model-myrk.34.0.65-1.92.0.92-2.50.pth
BLEU = 67.85, 84.6/72.8/62.9/54.7 (BP=1.000, ratio=1.024, hyp_len=23707, ref_len=23160)
Evaluation result for the model: seq-model-myrk.35.0.61-1.84.0.90-2.47.pth
BLEU = 69.75, 85.8/74.4/65.0/57.0 (BP=1.000, ratio=1.010, hyp_len=23397, ref_len=23160)
Evaluation result for the model: seq-model-myrk.36.0.63-1.87.0.90-2.46.pth
BLEU = 70.54, 86.2/75.1/65.9/58.1 (BP=1.000, ratio=1.010, hyp_len=23399, ref_len=23160)
Evaluation result for the model: seq-model-myrk.37.0.57-1.77.0.91-2.47.pth
BLEU = 67.63, 84.4/72.6/62.8/54.4 (BP=1.000, ratio=1.029, hyp_len=23831, ref_len=23160)
Evaluation result for the model: seq-model-myrk.38.0.57-1.76.0.87-2.38.pth
BLEU = 70.45, 85.9/75.0/65.8/58.1 (BP=1.000, ratio=1.018, hyp_len=23588, ref_len=23160)
Evaluation result for the model: seq-model-myrk.39.0.55-1.74.0.86-2.37.pth
BLEU = 69.17, 85.3/74.0/64.4/56.3 (BP=1.000, ratio=1.020, hyp_len=23614, ref_len=23160)
Evaluation result for the model: seq-model-myrk.40.0.54-1.71.0.86-2.36.pth
BLEU = 70.48, 85.7/74.9/65.9/58.2 (BP=1.000, ratio=1.022, hyp_len=23681, ref_len=23160)
Evaluation result for the model: seq-model-myrk.41.0.50-1.65.0.83-2.29.pth
BLEU = 71.09, 86.1/75.5/66.6/59.0 (BP=1.000, ratio=1.021, hyp_len=23651, ref_len=23160)
Evaluation result for the model: seq-model-myrk.42.0.50-1.65.0.85-2.35.pth
BLEU = 71.03, 86.2/75.5/66.5/58.9 (BP=1.000, ratio=1.022, hyp_len=23665, ref_len=23160)
Evaluation result for the model: seq-model-myrk.43.0.49-1.63.0.82-2.27.pth
BLEU = 71.89, 86.5/76.1/67.5/60.1 (BP=1.000, ratio=1.022, hyp_len=23673, ref_len=23160)
Evaluation result for the model: seq-model-myrk.44.0.45-1.56.0.82-2.26.pth
BLEU = 71.85, 86.6/76.1/67.4/60.0 (BP=1.000, ratio=1.020, hyp_len=23617, ref_len=23160)
Evaluation result for the model: seq-model-myrk.45.0.48-1.62.0.82-2.26.pth
BLEU = 71.65, 86.3/75.8/67.3/59.9 (BP=1.000, ratio=1.020, hyp_len=23616, ref_len=23160)
Evaluation result for the model: seq-model-myrk.46.0.66-1.93.0.90-2.45.pth
BLEU = 70.32, 86.0/75.0/65.7/57.7 (BP=1.000, ratio=1.008, hyp_len=23355, ref_len=23160)
Evaluation result for the model: seq-model-myrk.47.0.51-1.66.0.84-2.31.pth
BLEU = 70.49, 85.7/74.9/65.9/58.4 (BP=1.000, ratio=1.019, hyp_len=23607, ref_len=23160)
Evaluation result for the model: seq-model-myrk.48.0.46-1.58.0.82-2.26.pth
BLEU = 70.85, 85.7/75.2/66.4/58.8 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: seq-model-myrk.49.0.44-1.55.0.82-2.26.pth
BLEU = 72.21, 86.8/76.5/67.8/60.4 (BP=1.000, ratio=1.018, hyp_len=23582, ref_len=23160)
Evaluation result for the model: seq-model-myrk.50.0.43-1.54.0.78-2.18.pth
BLEU = 73.04, 87.0/77.1/68.8/61.7 (BP=1.000, ratio=1.022, hyp_len=23660, ref_len=23160)
Evaluation result for the model: seq-model-myrk.51.0.41-1.51.0.77-2.16.pth
BLEU = 73.17, 87.0/77.2/68.9/61.9 (BP=1.000, ratio=1.022, hyp_len=23673, ref_len=23160)
Evaluation result for the model: seq-model-myrk.52.0.41-1.51.0.78-2.19.pth
BLEU = 73.04, 86.9/77.0/68.8/61.8 (BP=1.000, ratio=1.024, hyp_len=23706, ref_len=23160)
Evaluation result for the model: seq-model-myrk.53.0.40-1.50.0.79-2.20.pth
BLEU = 72.81, 87.0/77.0/68.5/61.2 (BP=1.000, ratio=1.022, hyp_len=23679, ref_len=23160)
Evaluation result for the model: seq-model-myrk.54.0.41-1.50.0.78-2.19.pth
BLEU = 71.64, 86.2/75.9/67.2/59.9 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq-model-myrk.55.0.38-1.46.0.77-2.16.pth
BLEU = 73.30, 87.1/77.2/69.1/62.2 (BP=1.000, ratio=1.023, hyp_len=23693, ref_len=23160)
Evaluation result for the model: seq-model-myrk.56.0.39-1.47.0.77-2.17.pth
BLEU = 72.55, 86.6/76.6/68.2/61.2 (BP=1.000, ratio=1.027, hyp_len=23782, ref_len=23160)
Evaluation result for the model: seq-model-myrk.57.0.37-1.44.0.78-2.18.pth
BLEU = 73.66, 87.5/77.6/69.4/62.5 (BP=1.000, ratio=1.023, hyp_len=23686, ref_len=23160)
Evaluation result for the model: seq-model-myrk.58.0.36-1.44.0.78-2.18.pth
BLEU = 73.42, 87.2/77.4/69.2/62.2 (BP=1.000, ratio=1.021, hyp_len=23649, ref_len=23160)
Evaluation result for the model: seq-model-myrk.59.0.35-1.42.0.76-2.13.pth
BLEU = 72.89, 86.9/76.9/68.6/61.5 (BP=1.000, ratio=1.028, hyp_len=23800, ref_len=23160)
Evaluation result for the model: seq-model-myrk.60.0.35-1.42.0.75-2.13.pth
BLEU = 73.34, 87.1/77.3/69.1/62.2 (BP=1.000, ratio=1.024, hyp_len=23718, ref_len=23160)
Evaluation result for the model: seq-model-myrk.61.0.33-1.40.0.77-2.17.pth
BLEU = 74.36, 87.9/78.2/70.2/63.3 (BP=1.000, ratio=1.019, hyp_len=23602, ref_len=23160)
Evaluation result for the model: seq-model-myrk.62.0.32-1.37.0.78-2.18.pth
BLEU = 73.64, 87.2/77.6/69.5/62.6 (BP=1.000, ratio=1.026, hyp_len=23754, ref_len=23160)
Evaluation result for the model: seq-model-myrk.63.0.35-1.41.0.76-2.13.pth
BLEU = 73.70, 87.2/77.6/69.6/62.7 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: seq-model-myrk.64.0.33-1.39.0.78-2.17.pth
BLEU = 74.09, 87.6/78.0/69.9/63.1 (BP=1.000, ratio=1.023, hyp_len=23696, ref_len=23160)
Evaluation result for the model: seq-model-myrk.65.0.34-1.40.0.77-2.16.pth
BLEU = 74.31, 87.8/78.1/70.2/63.4 (BP=1.000, ratio=1.020, hyp_len=23633, ref_len=23160)
Evaluation result for the model: seq-model-myrk.66.0.38-1.46.0.80-2.22.pth
BLEU = 72.66, 87.1/76.8/68.3/61.0 (BP=1.000, ratio=1.017, hyp_len=23548, ref_len=23160)
Evaluation result for the model: seq-model-myrk.67.0.41-1.51.0.78-2.19.pth
BLEU = 71.29, 85.9/75.6/66.9/59.4 (BP=1.000, ratio=1.026, hyp_len=23763, ref_len=23160)
Evaluation result for the model: seq-model-myrk.68.0.36-1.43.0.74-2.09.pth
BLEU = 72.75, 86.5/76.7/68.5/61.6 (BP=1.000, ratio=1.031, hyp_len=23878, ref_len=23160)
Evaluation result for the model: seq-model-myrk.69.0.34-1.41.0.76-2.15.pth
BLEU = 71.77, 85.9/75.9/67.5/60.3 (BP=1.000, ratio=1.032, hyp_len=23907, ref_len=23160)
Evaluation result for the model: seq-model-myrk.70.0.33-1.39.0.73-2.08.pth
BLEU = 73.91, 87.4/77.7/69.8/63.0 (BP=1.000, ratio=1.025, hyp_len=23737, ref_len=23160)

real	22m56.709s
user	22m23.688s
sys	1m18.010s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-70epoch$
```

my-rk seq2seq 70 epoch model ရဲ့ Best score က  

```
Evaluation result for the model: seq-model-myrk.61.0.33-1.40.0.77-2.17.pth
BLEU = 74.36, 87.9/78.2/70.2/63.3 (BP=1.000, ratio=1.019, hyp_len=23602, ref_len=23160)
```

### seq2seq 40 eopch model, rk-my

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.pth',
    'n_epochs': 40,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 1 - |param|=6.42e+02 |g_param|=2.20e+05 loss=4.4547e+00 ppl=86.03                                                 
Validation - loss=4.0806e+00 ppl=59.18 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.43e+02 |g_param|=1.81e+05 loss=4.1957e+00 ppl=66.40                                                 
Validation - loss=3.9093e+00 ppl=49.86 best_loss=4.0806e+00 best_ppl=59.18                                              
Epoch 3 - |param|=6.43e+02 |g_param|=1.75e+05 loss=4.0478e+00 ppl=57.27                                                 
Validation - loss=3.8197e+00 ppl=45.59 best_loss=3.9093e+00 best_ppl=49.86                                              
Epoch 4 - |param|=6.43e+02 |g_param|=1.82e+05 loss=3.9870e+00 ppl=53.89                                                 
Validation - loss=3.7513e+00 ppl=42.58 best_loss=3.8197e+00 best_ppl=45.59                                              
Epoch 5 - |param|=6.43e+02 |g_param|=1.93e+05 loss=3.8967e+00 ppl=49.24                                                 
Validation - loss=3.6512e+00 ppl=38.52 best_loss=3.7513e+00 best_ppl=42.58                                              
Epoch 6 - |param|=6.44e+02 |g_param|=1.76e+05 loss=3.7624e+00 ppl=43.05                                                 
Validation - loss=3.5431e+00 ppl=34.57 best_loss=3.6512e+00 best_ppl=38.52                                              
Epoch 7 - |param|=6.44e+02 |g_param|=1.82e+05 loss=3.6921e+00 ppl=40.13                                                 
Validation - loss=3.4418e+00 ppl=31.24 best_loss=3.5431e+00 best_ppl=34.57                                              
Epoch 8 - |param|=6.45e+02 |g_param|=1.78e+05 loss=3.4989e+00 ppl=33.08                                                 
Validation - loss=3.2414e+00 ppl=25.57 best_loss=3.4418e+00 best_ppl=31.24                                              
Epoch 9 - |param|=6.45e+02 |g_param|=2.16e+05 loss=3.3380e+00 ppl=28.16                                                 
Validation - loss=3.0963e+00 ppl=22.12 best_loss=3.2414e+00 best_ppl=25.57                                              
Epoch 10 - |param|=6.46e+02 |g_param|=2.28e+05 loss=3.1382e+00 ppl=23.06                                                
Validation - loss=2.9351e+00 ppl=18.82 best_loss=3.0963e+00 best_ppl=22.12                                              
Epoch 11 - |param|=6.47e+02 |g_param|=2.34e+05 loss=2.8332e+00 ppl=17.00                                                
Validation - loss=2.6743e+00 ppl=14.50 best_loss=2.9351e+00 best_ppl=18.82                                              
Epoch 12 - |param|=6.47e+02 |g_param|=3.33e+05 loss=2.7275e+00 ppl=15.29                                                
Validation - loss=2.5183e+00 ppl=12.41 best_loss=2.6743e+00 best_ppl=14.50                                              
Epoch 13 - |param|=6.48e+02 |g_param|=3.26e+05 loss=2.4515e+00 ppl=11.61                                                
Validation - loss=2.3003e+00 ppl=9.98 best_loss=2.5183e+00 best_ppl=12.41                                               
Epoch 14 - |param|=6.49e+02 |g_param|=1.55e+05 loss=2.2679e+00 ppl=9.66                                                 
Validation - loss=2.1328e+00 ppl=8.44 best_loss=2.3003e+00 best_ppl=9.98                                                
Epoch 15 - |param|=6.49e+02 |g_param|=1.98e+05 loss=2.1686e+00 ppl=8.75                                                 
Validation - loss=1.9916e+00 ppl=7.33 best_loss=2.1328e+00 best_ppl=8.44                                                
Epoch 16 - |param|=6.50e+02 |g_param|=2.14e+05 loss=1.9186e+00 ppl=6.81                                                 
Validation - loss=1.8160e+00 ppl=6.15 best_loss=1.9916e+00 best_ppl=7.33                                                
Epoch 17 - |param|=6.50e+02 |g_param|=2.79e+05 loss=1.8388e+00 ppl=6.29                                                 
Validation - loss=1.8385e+00 ppl=6.29 best_loss=1.8160e+00 best_ppl=6.15                                                
Epoch 18 - |param|=6.51e+02 |g_param|=2.33e+05 loss=1.6975e+00 ppl=5.46                                                 
Validation - loss=1.6051e+00 ppl=4.98 best_loss=1.8160e+00 best_ppl=6.15                                                
Epoch 19 - |param|=6.52e+02 |g_param|=1.44e+05 loss=1.5169e+00 ppl=4.56                                                 
Validation - loss=1.4794e+00 ppl=4.39 best_loss=1.6051e+00 best_ppl=4.98                                                
Epoch 20 - |param|=6.52e+02 |g_param|=1.08e+05 loss=1.4278e+00 ppl=4.17                                                 
Validation - loss=1.4201e+00 ppl=4.14 best_loss=1.4794e+00 best_ppl=4.39                                                
Epoch 21 - |param|=6.52e+02 |g_param|=9.51e+04 loss=1.3302e+00 ppl=3.78                                                 
Validation - loss=1.3707e+00 ppl=3.94 best_loss=1.4201e+00 best_ppl=4.14                                                
Epoch 22 - |param|=6.53e+02 |g_param|=1.20e+05 loss=1.2804e+00 ppl=3.60                                                 
Validation - loss=1.5124e+00 ppl=4.54 best_loss=1.3707e+00 best_ppl=3.94                                                
Epoch 23 - |param|=6.53e+02 |g_param|=1.17e+05 loss=1.2086e+00 ppl=3.35                                                 
Validation - loss=1.2508e+00 ppl=3.49 best_loss=1.3707e+00 best_ppl=3.94                                                
Epoch 24 - |param|=6.54e+02 |g_param|=3.84e+04 loss=1.0873e+00 ppl=2.97                                                 
Validation - loss=1.1854e+00 ppl=3.27 best_loss=1.2508e+00 best_ppl=3.49                                                
Epoch 25 - |param|=6.54e+02 |g_param|=3.85e+04 loss=1.0234e+00 ppl=2.78                                                 
Validation - loss=1.1533e+00 ppl=3.17 best_loss=1.1854e+00 best_ppl=3.27                                                
Epoch 26 - |param|=6.55e+02 |g_param|=6.86e+04 loss=1.0536e+00 ppl=2.87                                                 
Validation - loss=1.1258e+00 ppl=3.08 best_loss=1.1533e+00 best_ppl=3.17                                                
Epoch 27 - |param|=6.55e+02 |g_param|=3.96e+04 loss=9.4234e-01 ppl=2.57                                                 
Validation - loss=1.0810e+00 ppl=2.95 best_loss=1.1258e+00 best_ppl=3.08                                                
Epoch 28 - |param|=6.56e+02 |g_param|=4.51e+04 loss=8.8305e-01 ppl=2.42                                                 
Validation - loss=1.0388e+00 ppl=2.83 best_loss=1.0810e+00 best_ppl=2.95                                                
Epoch 29 - |param|=6.56e+02 |g_param|=4.51e+04 loss=8.1082e-01 ppl=2.25                                                 
Validation - loss=1.2342e+00 ppl=3.44 best_loss=1.0388e+00 best_ppl=2.83                                                
Epoch 30 - |param|=6.57e+02 |g_param|=5.77e+04 loss=9.1081e-01 ppl=2.49                                                 
Validation - loss=9.9645e-01 ppl=2.71 best_loss=1.0388e+00 best_ppl=2.83                                                
Epoch 31 - |param|=6.57e+02 |g_param|=4.55e+04 loss=7.4795e-01 ppl=2.11                                                 
Validation - loss=9.9853e-01 ppl=2.71 best_loss=9.9645e-01 best_ppl=2.71                                                
Epoch 32 - |param|=6.57e+02 |g_param|=4.63e+04 loss=7.6166e-01 ppl=2.14                                                 
Validation - loss=9.4748e-01 ppl=2.58 best_loss=9.9645e-01 best_ppl=2.71                                                
Epoch 33 - |param|=6.58e+02 |g_param|=4.49e+04 loss=7.5419e-01 ppl=2.13                                                 
Validation - loss=9.7273e-01 ppl=2.65 best_loss=9.4748e-01 best_ppl=2.58                                                
Epoch 34 - |param|=6.58e+02 |g_param|=4.30e+04 loss=7.0892e-01 ppl=2.03                                                 
Validation - loss=9.0931e-01 ppl=2.48 best_loss=9.4748e-01 best_ppl=2.58                                                
Epoch 35 - |param|=6.59e+02 |g_param|=3.17e+04 loss=6.5968e-01 ppl=1.93                                                 
Validation - loss=8.9127e-01 ppl=2.44 best_loss=9.0931e-01 best_ppl=2.48                                                
Epoch 36 - |param|=6.59e+02 |g_param|=3.27e+04 loss=6.3408e-01 ppl=1.89                                                 
Validation - loss=8.8012e-01 ppl=2.41 best_loss=8.9127e-01 best_ppl=2.44                                                
Epoch 37 - |param|=6.59e+02 |g_param|=3.55e+04 loss=6.0395e-01 ppl=1.83                                                 
Validation - loss=8.5790e-01 ppl=2.36 best_loss=8.8012e-01 best_ppl=2.41                                                
Epoch 38 - |param|=6.60e+02 |g_param|=3.13e+04 loss=6.0561e-01 ppl=1.83                                                 
Validation - loss=8.6345e-01 ppl=2.37 best_loss=8.5790e-01 best_ppl=2.36                                                
Epoch 39 - |param|=6.60e+02 |g_param|=3.41e+04 loss=5.9250e-01 ppl=1.81                                                 
Validation - loss=8.3310e-01 ppl=2.30 best_loss=8.5790e-01 best_ppl=2.36                                                
Epoch 40 - |param|=6.60e+02 |g_param|=4.05e+04 loss=5.6539e-01 ppl=1.76                                                 
Validation - loss=8.5853e-01 ppl=2.36 best_loss=8.3310e-01 best_ppl=2.30                                                

real	7m50.668s
user	7m43.432s
sys	0m6.953s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-rkmy.01.4.45-86.03.4.08-59.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.9/0.4/0.0/0.0 (BP=1.000, ratio=1.041, hyp_len=24480, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.20-66.40.3.91-49.86.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 16.1/2.3/0.0/0.0 (BP=0.993, ratio=0.993, hyp_len=23342, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.4.05-57.27.3.82-45.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.1/1.7/0.1/0.0 (BP=0.980, ratio=0.980, hyp_len=23048, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.3.99-53.89.3.75-42.58.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.6/2.9/0.1/0.0 (BP=0.985, ratio=0.986, hyp_len=23169, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.90-49.24.3.65-38.52.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.6/3.8/0.2/0.0 (BP=0.976, ratio=0.977, hyp_len=22961, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.76-43.05.3.54-34.57.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.9/4.7/0.4/0.0 (BP=0.994, ratio=0.994, hyp_len=23378, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.69-40.13.3.44-31.24.pth
BLEU = 1.20, 25.6/5.9/0.8/0.0 (BP=0.998, ratio=0.998, hyp_len=23467, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.50-33.08.3.24-25.57.pth
BLEU = 2.17, 28.7/8.1/1.4/0.1 (BP=0.998, ratio=0.998, hyp_len=23472, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.34-28.16.3.10-22.12.pth
BLEU = 3.22, 31.7/9.9/1.6/0.2 (BP=1.000, ratio=1.000, hyp_len=23505, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.3.14-23.06.2.94-18.82.pth
BLEU = 4.79, 34.5/11.9/2.4/0.5 (BP=1.000, ratio=1.036, hyp_len=24354, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.2.83-17.00.2.67-14.50.pth
BLEU = 8.29, 38.9/15.7/5.0/1.5 (BP=1.000, ratio=1.029, hyp_len=24185, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.73-15.29.2.52-12.41.pth
BLEU = 9.92, 40.6/17.6/6.3/2.2 (BP=1.000, ratio=1.033, hyp_len=24274, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.45-11.61.2.30-9.98.pth
BLEU = 13.37, 44.7/21.3/8.9/3.8 (BP=1.000, ratio=1.025, hyp_len=24090, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.27-9.66.2.13-8.44.pth
BLEU = 16.84, 49.1/25.3/11.9/5.4 (BP=1.000, ratio=1.008, hyp_len=23687, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.2.17-8.75.1.99-7.33.pth
BLEU = 20.49, 52.3/28.8/14.9/7.8 (BP=1.000, ratio=1.030, hyp_len=24209, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.1.92-6.81.1.82-6.15.pth
BLEU = 24.18, 56.0/32.7/18.3/10.2 (BP=1.000, ratio=1.011, hyp_len=23756, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.1.84-6.29.1.84-6.29.pth
BLEU = 27.23, 59.6/36.5/21.1/12.3 (BP=0.994, ratio=0.994, hyp_len=23374, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.70-5.46.1.61-4.98.pth
BLEU = 32.31, 62.8/41.1/25.8/16.3 (BP=1.000, ratio=1.014, hyp_len=23843, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.52-4.56.1.48-4.39.pth
BLEU = 39.21, 67.4/47.3/32.6/22.7 (BP=1.000, ratio=1.019, hyp_len=23952, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.43-4.17.1.42-4.14.pth
BLEU = 41.47, 69.5/49.6/34.8/24.7 (BP=1.000, ratio=1.004, hyp_len=23598, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.33-3.78.1.37-3.94.pth
BLEU = 43.85, 70.8/51.8/37.2/27.1 (BP=1.000, ratio=1.017, hyp_len=23917, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.28-3.60.1.51-4.54.pth
BLEU = 38.13, 67.5/46.7/31.4/21.4 (BP=1.000, ratio=1.000, hyp_len=23520, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.1.21-3.35.1.25-3.49.pth
BLEU = 48.71, 73.8/56.1/42.2/32.2 (BP=1.000, ratio=1.022, hyp_len=24018, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.1.09-2.97.1.19-3.27.pth
BLEU = 52.36, 76.3/59.5/46.0/36.0 (BP=1.000, ratio=1.013, hyp_len=23805, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.1.02-2.78.1.15-3.17.pth
BLEU = 55.21, 78.0/62.2/49.0/39.1 (BP=1.000, ratio=1.012, hyp_len=23800, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.1.05-2.87.1.13-3.08.pth
BLEU = 53.86, 77.0/61.1/47.5/37.6 (BP=1.000, ratio=1.029, hyp_len=24186, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.0.94-2.57.1.08-2.95.pth
BLEU = 58.77, 80.0/65.3/52.8/43.3 (BP=1.000, ratio=1.013, hyp_len=23823, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.0.88-2.42.1.04-2.83.pth
BLEU = 60.71, 81.0/67.0/54.9/45.6 (BP=1.000, ratio=1.009, hyp_len=23711, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.81-2.25.1.23-3.44.pth
BLEU = 55.76, 77.4/62.9/49.8/39.9 (BP=1.000, ratio=1.055, hyp_len=24799, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.91-2.49.1.00-2.71.pth
BLEU = 61.44, 81.4/67.6/55.6/46.6 (BP=1.000, ratio=1.017, hyp_len=23909, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.31.0.75-2.11.1.00-2.71.pth
BLEU = 62.35, 81.9/68.4/56.6/47.6 (BP=1.000, ratio=1.019, hyp_len=23949, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.32.0.76-2.14.0.95-2.58.pth
BLEU = 63.62, 82.4/69.5/58.0/49.3 (BP=1.000, ratio=1.026, hyp_len=24110, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.33.0.75-2.13.0.97-2.65.pth
BLEU = 63.11, 81.7/69.1/57.6/48.7 (BP=1.000, ratio=1.035, hyp_len=24341, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.34.0.71-2.03.0.91-2.48.pth
BLEU = 67.29, 84.5/72.6/62.0/53.8 (BP=1.000, ratio=1.014, hyp_len=23830, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.35.0.66-1.93.0.89-2.44.pth
BLEU = 66.42, 83.7/71.8/61.1/53.0 (BP=1.000, ratio=1.027, hyp_len=24138, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.36.0.63-1.89.0.88-2.41.pth
BLEU = 67.73, 84.6/73.0/62.5/54.6 (BP=1.000, ratio=1.021, hyp_len=23991, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.37.0.60-1.83.0.86-2.36.pth
BLEU = 68.43, 85.0/73.6/63.3/55.4 (BP=1.000, ratio=1.020, hyp_len=23969, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.38.0.61-1.83.0.86-2.37.pth
BLEU = 68.60, 85.0/73.7/63.5/55.6 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth
BLEU = 69.39, 85.4/74.4/64.4/56.6 (BP=1.000, ratio=1.022, hyp_len=24037, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.40.0.57-1.76.0.86-2.36.pth
BLEU = 67.85, 84.4/73.2/62.7/54.7 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)

real	13m40.771s
user	13m19.973s
sys	0m45.599s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-40epoch$
```

rk-my, seq2seq, 40 Best Score:  

```
Evaluation result for the model: seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth
BLEU = 69.39, 85.4/74.4/64.4/56.6 (BP=1.000, ratio=1.022, hyp_len=24037, ref_len=23509)
```

###  seq2seq 50 eopch model, rk-my

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 50 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.pth
...
...
Validation - loss=2.7430e+00 ppl=15.53 best_loss=2.8574e+00 best_ppl=17.42                                              
Epoch 11 - |param|=6.47e+02 |g_param|=9.25e+04 loss=2.7802e+00 ppl=16.12                                                
Validation - loss=2.6486e+00 ppl=14.13 best_loss=2.7430e+00 best_ppl=15.53                                              
Epoch 12 - |param|=6.47e+02 |g_param|=1.08e+05 loss=2.6968e+00 ppl=14.83                                                
Validation - loss=2.5537e+00 ppl=12.85 best_loss=2.6486e+00 best_ppl=14.13                                              
Epoch 13 - |param|=6.48e+02 |g_param|=9.76e+04 loss=2.5638e+00 ppl=12.98                                                
Validation - loss=2.4562e+00 ppl=11.66 best_loss=2.5537e+00 best_ppl=12.85                                              
Epoch 14 - |param|=6.49e+02 |g_param|=1.02e+05 loss=2.5260e+00 ppl=12.50                                                
Validation - loss=2.3781e+00 ppl=10.78 best_loss=2.4562e+00 best_ppl=11.66                                              
Epoch 15 - |param|=6.49e+02 |g_param|=9.91e+04 loss=2.3717e+00 ppl=10.72                                                
Validation - loss=2.2852e+00 ppl=9.83 best_loss=2.3781e+00 best_ppl=10.78                                               
Epoch 16 - |param|=6.50e+02 |g_param|=1.20e+05 loss=2.2699e+00 ppl=9.68                                                 
Validation - loss=2.1552e+00 ppl=8.63 best_loss=2.2852e+00 best_ppl=9.83                                                
Epoch 17 - |param|=6.50e+02 |g_param|=1.57e+05 loss=2.1207e+00 ppl=8.34                                                 
Validation - loss=1.9942e+00 ppl=7.35 best_loss=2.1552e+00 best_ppl=8.63                                                
Epoch 18 - |param|=6.51e+02 |g_param|=2.44e+05 loss=1.8924e+00 ppl=6.64                                                 
Validation - loss=1.9986e+00 ppl=7.38 best_loss=1.9942e+00 best_ppl=7.35                                                
Epoch 19 - |param|=6.52e+02 |g_param|=1.70e+05 loss=1.6475e+00 ppl=5.19                                                 
Validation - loss=1.6097e+00 ppl=5.00 best_loss=1.9942e+00 best_ppl=7.35                                                
Epoch 20 - |param|=6.52e+02 |g_param|=1.51e+05 loss=1.4466e+00 ppl=4.25                                                 
Validation - loss=1.3960e+00 ppl=4.04 best_loss=1.6097e+00 best_ppl=5.00                                                
Epoch 21 - |param|=6.53e+02 |g_param|=2.03e+05 loss=1.2439e+00 ppl=3.47                                                 
Validation - loss=1.2813e+00 ppl=3.60 best_loss=1.3960e+00 best_ppl=4.04                                                
Epoch 22 - |param|=6.54e+02 |g_param|=2.06e+05 loss=1.1777e+00 ppl=3.25                                                 
Validation - loss=1.2345e+00 ppl=3.44 best_loss=1.2813e+00 best_ppl=3.60                                                
Epoch 23 - |param|=6.54e+02 |g_param|=1.66e+05 loss=1.0285e+00 ppl=2.80                                                 
Validation - loss=1.0754e+00 ppl=2.93 best_loss=1.2345e+00 best_ppl=3.44                                                
Epoch 24 - |param|=6.55e+02 |g_param|=1.55e+05 loss=9.6020e-01 ppl=2.61                                                 
Validation - loss=1.0195e+00 ppl=2.77 best_loss=1.0754e+00 best_ppl=2.93                                                
Epoch 25 - |param|=6.55e+02 |g_param|=1.89e+05 loss=8.4940e-01 ppl=2.34                                                 
Validation - loss=9.8498e-01 ppl=2.68 best_loss=1.0195e+00 best_ppl=2.77                                                
Epoch 26 - |param|=6.56e+02 |g_param|=5.33e+04 loss=8.0544e-01 ppl=2.24                                                 
Validation - loss=8.9332e-01 ppl=2.44 best_loss=9.8498e-01 best_ppl=2.68                                                
Epoch 27 - |param|=6.56e+02 |g_param|=4.08e+04 loss=7.2538e-01 ppl=2.07                                                 
Validation - loss=8.5888e-01 ppl=2.36 best_loss=8.9332e-01 best_ppl=2.44                                                
Epoch 28 - |param|=6.57e+02 |g_param|=3.77e+04 loss=7.0998e-01 ppl=2.03                                                 
Validation - loss=8.3422e-01 ppl=2.30 best_loss=8.5888e-01 best_ppl=2.36                                                
Epoch 29 - |param|=6.57e+02 |g_param|=3.55e+04 loss=6.5715e-01 ppl=1.93                                                 
Validation - loss=8.0980e-01 ppl=2.25 best_loss=8.3422e-01 best_ppl=2.30                                                
Epoch 30 - |param|=6.58e+02 |g_param|=3.73e+04 loss=6.0584e-01 ppl=1.83                                                 
Validation - loss=7.8599e-01 ppl=2.19 best_loss=8.0980e-01 best_ppl=2.25                                                
Epoch 31 - |param|=6.58e+02 |g_param|=2.75e+04 loss=5.6780e-01 ppl=1.76                                                 
Validation - loss=7.7769e-01 ppl=2.18 best_loss=7.8599e-01 best_ppl=2.19                                                
Epoch 32 - |param|=6.59e+02 |g_param|=4.03e+04 loss=5.8122e-01 ppl=1.79                                                 
Validation - loss=7.8656e-01 ppl=2.20 best_loss=7.7769e-01 best_ppl=2.18                                                
Epoch 33 - |param|=6.59e+02 |g_param|=3.25e+04 loss=5.3616e-01 ppl=1.71                                                 
Validation - loss=7.4483e-01 ppl=2.11 best_loss=7.7769e-01 best_ppl=2.18                                                
Epoch 34 - |param|=6.59e+02 |g_param|=6.81e+04 loss=6.4196e-01 ppl=1.90                                                 
Validation - loss=7.9670e-01 ppl=2.22 best_loss=7.4483e-01 best_ppl=2.11                                                
Epoch 35 - |param|=6.60e+02 |g_param|=3.45e+04 loss=5.2804e-01 ppl=1.70                                                 
Validation - loss=7.1236e-01 ppl=2.04 best_loss=7.4483e-01 best_ppl=2.11                                                
Epoch 36 - |param|=6.60e+02 |g_param|=2.91e+04 loss=4.8616e-01 ppl=1.63                                                 
Validation - loss=6.9474e-01 ppl=2.00 best_loss=7.1236e-01 best_ppl=2.04                                                
Epoch 37 - |param|=6.61e+02 |g_param|=1.34e+04 loss=4.6472e-01 ppl=1.59                                                 
Validation - loss=7.0132e-01 ppl=2.02 best_loss=6.9474e-01 best_ppl=2.00                                                
Epoch 38 - |param|=6.61e+02 |g_param|=1.31e+04 loss=4.4644e-01 ppl=1.56                                                 
Validation - loss=6.8853e-01 ppl=1.99 best_loss=6.9474e-01 best_ppl=2.00                                                
Epoch 39 - |param|=6.61e+02 |g_param|=1.18e+04 loss=4.3788e-01 ppl=1.55                                                 
Validation - loss=6.7978e-01 ppl=1.97 best_loss=6.8853e-01 best_ppl=1.99                                                
Epoch 40 - |param|=6.62e+02 |g_param|=1.17e+04 loss=4.1857e-01 ppl=1.52                                                 
Validation - loss=6.6587e-01 ppl=1.95 best_loss=6.7978e-01 best_ppl=1.97                                                
Epoch 41 - |param|=6.62e+02 |g_param|=1.31e+04 loss=4.3065e-01 ppl=1.54                                                 
Validation - loss=6.7292e-01 ppl=1.96 best_loss=6.6587e-01 best_ppl=1.95                                                
Epoch 42 - |param|=6.62e+02 |g_param|=1.31e+04 loss=3.9757e-01 ppl=1.49                                                 
Validation - loss=6.6779e-01 ppl=1.95 best_loss=6.6587e-01 best_ppl=1.95                                                
Epoch 43 - |param|=6.63e+02 |g_param|=1.34e+04 loss=3.9630e-01 ppl=1.49                                                 
Validation - loss=6.5876e-01 ppl=1.93 best_loss=6.6587e-01 best_ppl=1.95                                                
Epoch 44 - |param|=6.63e+02 |g_param|=1.15e+04 loss=3.8665e-01 ppl=1.47                                                 
Validation - loss=6.6138e-01 ppl=1.94 best_loss=6.5876e-01 best_ppl=1.93                                                
Epoch 45 - |param|=6.63e+02 |g_param|=1.09e+04 loss=3.6604e-01 ppl=1.44                                                 
Validation - loss=6.5385e-01 ppl=1.92 best_loss=6.5876e-01 best_ppl=1.93                                                
Epoch 46 - |param|=6.64e+02 |g_param|=1.99e+04 loss=3.5420e-01 ppl=1.43                                                 
Validation - loss=6.6492e-01 ppl=1.94 best_loss=6.5385e-01 best_ppl=1.92                                                
Epoch 47 - |param|=6.64e+02 |g_param|=2.50e+04 loss=3.9062e-01 ppl=1.48                                                 
Validation - loss=6.5968e-01 ppl=1.93 best_loss=6.5385e-01 best_ppl=1.92                                                
Epoch 48 - |param|=6.64e+02 |g_param|=1.45e+04 loss=3.4604e-01 ppl=1.41                                                 
Validation - loss=6.7228e-01 ppl=1.96 best_loss=6.5385e-01 best_ppl=1.92                                                
Epoch 49 - |param|=6.65e+02 |g_param|=1.16e+04 loss=3.3219e-01 ppl=1.39                                                 
Validation - loss=6.4218e-01 ppl=1.90 best_loss=6.5385e-01 best_ppl=1.92                                                
Epoch 50 - |param|=6.65e+02 |g_param|=1.08e+04 loss=3.3504e-01 ppl=1.40                                                 
Validation - loss=6.3097e-01 ppl=1.88 best_loss=6.4218e-01 best_ppl=1.90                                                

real	9m50.818s
user	9m41.772s
sys	0m8.139s
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-rkmy.01.4.44-84.62.4.06-58.26.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 12.6/0.6/0.0/0.0 (BP=1.000, ratio=1.056, hyp_len=24815, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.12-61.81.3.90-49.65.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/2.8/0.0/0.0 (BP=0.981, ratio=0.982, hyp_len=23075, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.4.02-55.74.3.82-45.45.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.0/2.8/0.0/0.0 (BP=0.979, ratio=0.979, hyp_len=23016, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.3.93-51.02.3.70-40.45.pth
BLEU = 0.55, 23.8/4.3/0.2/0.0 (BP=0.983, ratio=0.983, hyp_len=23117, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.71-40.75.3.44-31.24.pth
BLEU = 0.78, 25.9/4.4/0.3/0.0 (BP=0.985, ratio=0.985, hyp_len=23155, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.59-36.27.3.27-26.18.pth
BLEU = 1.17, 26.7/5.8/0.7/0.0 (BP=0.999, ratio=0.999, hyp_len=23487, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.32-27.54.3.10-22.16.pth
BLEU = 3.39, 30.7/8.5/1.7/0.3 (BP=1.000, ratio=1.007, hyp_len=23669, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.15-23.24.2.94-18.87.pth
BLEU = 4.67, 32.9/10.6/2.5/0.5 (BP=1.000, ratio=1.004, hyp_len=23608, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.11-22.43.2.86-17.42.pth
BLEU = 4.07, 33.1/10.5/2.2/0.4 (BP=0.986, ratio=0.986, hyp_len=23183, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.2.93-18.82.2.74-15.53.pth
BLEU = 6.12, 34.6/12.4/3.5/0.9 (BP=1.000, ratio=1.029, hyp_len=24195, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.2.78-16.12.2.65-14.13.pth
BLEU = 7.29, 37.0/13.7/4.3/1.3 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.70-14.83.2.55-12.85.pth
BLEU = 8.88, 39.1/15.7/5.5/1.9 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.56-12.98.2.46-11.66.pth
BLEU = 9.84, 40.1/16.7/6.2/2.2 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.53-12.50.2.38-10.78.pth
BLEU = 11.52, 42.3/18.4/7.5/3.0 (BP=1.000, ratio=1.020, hyp_len=23988, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.2.37-10.72.2.29-9.83.pth
BLEU = 12.69, 43.7/19.9/8.4/3.6 (BP=1.000, ratio=1.031, hyp_len=24239, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.2.27-9.68.2.16-8.63.pth
BLEU = 14.58, 46.0/22.0/10.0/4.5 (BP=1.000, ratio=1.034, hyp_len=24314, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.2.12-8.34.1.99-7.35.pth
BLEU = 18.96, 51.3/26.8/13.6/6.9 (BP=1.000, ratio=1.013, hyp_len=23815, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.89-6.64.2.00-7.38.pth
BLEU = 20.37, 51.8/28.6/14.9/7.8 (BP=0.999, ratio=0.999, hyp_len=23488, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.65-5.19.1.61-5.00.pth
BLEU = 31.40, 62.2/39.9/24.9/15.7 (BP=1.000, ratio=1.026, hyp_len=24113, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.45-4.25.1.40-4.04.pth
BLEU = 40.85, 68.7/48.8/34.2/24.3 (BP=1.000, ratio=1.016, hyp_len=23888, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.24-3.47.1.28-3.60.pth
BLEU = 46.36, 72.2/53.8/39.8/29.9 (BP=1.000, ratio=1.016, hyp_len=23895, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.18-3.25.1.23-3.44.pth
BLEU = 49.24, 74.4/56.5/42.7/32.8 (BP=1.000, ratio=1.003, hyp_len=23587, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.1.03-2.80.1.08-2.93.pth
BLEU = 54.50, 77.0/61.2/48.4/38.7 (BP=1.000, ratio=1.026, hyp_len=24111, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.0.96-2.61.1.02-2.77.pth
BLEU = 56.41, 78.0/62.9/50.4/41.0 (BP=1.000, ratio=1.029, hyp_len=24199, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.0.85-2.34.0.98-2.68.pth
BLEU = 58.53, 79.3/64.9/52.6/43.3 (BP=1.000, ratio=1.027, hyp_len=24144, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.0.81-2.24.0.89-2.44.pth
BLEU = 64.15, 82.5/69.7/58.7/50.2 (BP=1.000, ratio=1.020, hyp_len=23971, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.0.73-2.07.0.86-2.36.pth
BLEU = 63.82, 82.2/69.5/58.3/49.8 (BP=1.000, ratio=1.030, hyp_len=24226, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.0.71-2.03.0.83-2.30.pth
BLEU = 64.55, 82.5/70.2/59.2/50.7 (BP=1.000, ratio=1.033, hyp_len=24279, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.66-1.93.0.81-2.25.pth
BLEU = 66.84, 83.8/72.0/61.6/53.6 (BP=1.000, ratio=1.029, hyp_len=24185, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.61-1.83.0.79-2.19.pth
BLEU = 68.05, 84.5/73.2/63.0/55.1 (BP=1.000, ratio=1.030, hyp_len=24211, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.31.0.57-1.76.0.78-2.18.pth
BLEU = 67.37, 83.9/72.7/62.3/54.2 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.32.0.58-1.79.0.79-2.20.pth
BLEU = 68.27, 84.7/73.5/63.2/55.2 (BP=1.000, ratio=1.028, hyp_len=24174, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.33.0.54-1.71.0.74-2.11.pth
BLEU = 68.98, 84.9/74.2/64.0/56.1 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.34.0.64-1.90.0.80-2.22.pth
BLEU = 68.16, 84.3/73.3/63.2/55.3 (BP=1.000, ratio=1.032, hyp_len=24254, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.35.0.53-1.70.0.71-2.04.pth
BLEU = 70.78, 85.6/75.4/66.1/58.8 (BP=1.000, ratio=1.031, hyp_len=24246, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.36.0.49-1.63.0.69-2.00.pth
BLEU = 70.96, 85.8/75.6/66.3/59.0 (BP=1.000, ratio=1.034, hyp_len=24310, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.37.0.46-1.59.0.70-2.02.pth
BLEU = 72.25, 86.6/76.7/67.6/60.7 (BP=1.000, ratio=1.028, hyp_len=24171, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.38.0.45-1.56.0.69-1.99.pth
BLEU = 71.89, 86.2/76.3/67.4/60.3 (BP=1.000, ratio=1.034, hyp_len=24318, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.39.0.44-1.55.0.68-1.97.pth
BLEU = 72.21, 86.4/76.6/67.7/60.7 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.40.0.42-1.52.0.67-1.95.pth
BLEU = 71.56, 86.0/76.0/66.9/60.0 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.41.0.43-1.54.0.67-1.96.pth
BLEU = 72.00, 86.2/76.4/67.5/60.5 (BP=1.000, ratio=1.039, hyp_len=24417, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.42.0.40-1.49.0.67-1.95.pth
BLEU = 72.42, 86.5/76.9/67.9/60.9 (BP=1.000, ratio=1.039, hyp_len=24437, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.43.0.40-1.49.0.66-1.93.pth
BLEU = 73.40, 87.1/77.6/69.0/62.3 (BP=1.000, ratio=1.030, hyp_len=24212, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.44.0.39-1.47.0.66-1.94.pth
BLEU = 72.04, 86.2/76.4/67.5/60.5 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.45.0.37-1.44.0.65-1.92.pth
BLEU = 73.65, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.034, hyp_len=24307, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.46.0.35-1.43.0.66-1.94.pth
BLEU = 73.22, 87.1/77.4/68.8/62.0 (BP=1.000, ratio=1.024, hyp_len=24077, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.47.0.39-1.48.0.66-1.93.pth
BLEU = 71.28, 85.7/75.7/66.7/59.6 (BP=1.000, ratio=1.046, hyp_len=24598, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.48.0.35-1.41.0.67-1.96.pth
BLEU = 73.76, 87.3/77.9/69.4/62.7 (BP=1.000, ratio=1.026, hyp_len=24123, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth
BLEU = 74.04, 87.3/78.1/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24361, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.50.0.34-1.40.0.63-1.88.pth
BLEU = 73.66, 87.0/77.8/69.3/62.8 (BP=1.000, ratio=1.038, hyp_len=24406, ref_len=23509)

real	16m55.152s
user	16m28.673s
sys	0m56.382s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-50epoch$
```

seq2seq 50 epoch model (rk-my) ရဲ့ best score က   

```
Evaluation result for the model: seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth
BLEU = 74.04, 87.3/78.1/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24361, ref_len=23509)
```

###  seq2seq 60 eopch model, rk-my

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 60 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.pth',
    'n_epochs': 60,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 1 - |param|=6.41e+02 |g_param|=2.26e+05 loss=4.4537e+00 ppl=85.94                                                 
Validation - loss=4.0784e+00 ppl=59.05 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.41e+02 |g_param|=1.88e+05 loss=4.1859e+00 ppl=65.75                                                 
Validation - loss=3.9141e+00 ppl=50.10 best_loss=4.0784e+00 best_ppl=59.05                                              
Epoch 3 - |param|=6.41e+02 |g_param|=1.92e+05 loss=4.0835e+00 ppl=59.35                                                 
Validation - loss=3.7972e+00 ppl=44.58 best_loss=3.9141e+00 best_ppl=50.10                                              
Epoch 4 - |param|=6.42e+02 |g_param|=1.83e+05 loss=3.9240e+00 ppl=50.60                                                 
Validation - loss=3.6850e+00 ppl=39.84 best_loss=3.7972e+00 best_ppl=44.58                                              
Epoch 5 - |param|=6.42e+02 |g_param|=1.87e+05 loss=3.8323e+00 ppl=46.17                                                 
Validation - loss=3.5931e+00 ppl=36.35 best_loss=3.6850e+00 best_ppl=39.84                                              
Epoch 6 - |param|=6.42e+02 |g_param|=1.75e+05 loss=3.7033e+00 ppl=40.58                                                 
Validation - loss=3.4548e+00 ppl=31.65 best_loss=3.5931e+00 best_ppl=36.35                                              
Epoch 7 - |param|=6.43e+02 |g_param|=2.33e+05 loss=3.5430e+00 ppl=34.57                                                 
Validation - loss=3.3402e+00 ppl=28.23 best_loss=3.4548e+00 best_ppl=31.65                                              
Epoch 8 - |param|=6.43e+02 |g_param|=2.35e+05 loss=3.3899e+00 ppl=29.66                                                 
Validation - loss=3.0694e+00 ppl=21.53 best_loss=3.3402e+00 best_ppl=28.23                                              
Epoch 9 - |param|=6.44e+02 |g_param|=1.66e+05 loss=3.1387e+00 ppl=23.07                                                 
Validation - loss=2.8611e+00 ppl=17.48 best_loss=3.0694e+00 best_ppl=21.53                                              
Epoch 10 - |param|=6.45e+02 |g_param|=2.00e+05 loss=2.8159e+00 ppl=16.71                                                
Validation - loss=2.6666e+00 ppl=14.39 best_loss=2.8611e+00 best_ppl=17.48                                              
Epoch 11 - |param|=6.46e+02 |g_param|=1.77e+05 loss=2.6255e+00 ppl=13.81                                                
Validation - loss=2.4725e+00 ppl=11.85 best_loss=2.6666e+00 best_ppl=14.39                                              
Epoch 12 - |param|=6.46e+02 |g_param|=2.80e+05 loss=2.5062e+00 ppl=12.26                                                
Validation - loss=2.3248e+00 ppl=10.23 best_loss=2.4725e+00 best_ppl=11.85                                              
Epoch 13 - |param|=6.47e+02 |g_param|=1.97e+05 loss=2.2786e+00 ppl=9.76                                                 
Validation - loss=2.2312e+00 ppl=9.31 best_loss=2.3248e+00 best_ppl=10.23                                               
Epoch 14 - |param|=6.47e+02 |g_param|=1.63e+05 loss=2.1748e+00 ppl=8.80                                                 
Validation - loss=2.1069e+00 ppl=8.22 best_loss=2.2312e+00 best_ppl=9.31                                                
Epoch 15 - |param|=6.48e+02 |g_param|=1.09e+05 loss=2.0453e+00 ppl=7.73                                                 
Validation - loss=2.0739e+00 ppl=7.96 best_loss=2.1069e+00 best_ppl=8.22                                                
Epoch 16 - |param|=6.49e+02 |g_param|=1.73e+05 loss=1.9948e+00 ppl=7.35                                                 
Validation - loss=1.9396e+00 ppl=6.96 best_loss=2.0739e+00 best_ppl=7.96                                                
Epoch 17 - |param|=6.49e+02 |g_param|=1.23e+05 loss=1.8376e+00 ppl=6.28                                                 
Validation - loss=1.8130e+00 ppl=6.13 best_loss=1.9396e+00 best_ppl=6.96                                                
Epoch 18 - |param|=6.50e+02 |g_param|=1.44e+05 loss=1.6930e+00 ppl=5.44                                                 
Validation - loss=1.6813e+00 ppl=5.37 best_loss=1.8130e+00 best_ppl=6.13                                                
Epoch 19 - |param|=6.51e+02 |g_param|=1.48e+05 loss=1.6104e+00 ppl=5.00                                                 
Validation - loss=1.6294e+00 ppl=5.10 best_loss=1.6813e+00 best_ppl=5.37                                                
Epoch 20 - |param|=6.51e+02 |g_param|=1.01e+05 loss=1.4648e+00 ppl=4.33                                                 
Validation - loss=1.5238e+00 ppl=4.59 best_loss=1.6294e+00 best_ppl=5.10                                                
Epoch 21 - |param|=6.52e+02 |g_param|=1.22e+05 loss=1.4088e+00 ppl=4.09                                                 
Validation - loss=1.4855e+00 ppl=4.42 best_loss=1.5238e+00 best_ppl=4.59                                                
Epoch 22 - |param|=6.52e+02 |g_param|=1.47e+05 loss=1.4234e+00 ppl=4.15                                                 
Validation - loss=1.4416e+00 ppl=4.23 best_loss=1.4855e+00 best_ppl=4.42                                                
Epoch 23 - |param|=6.53e+02 |g_param|=1.20e+05 loss=1.3157e+00 ppl=3.73                                                 
Validation - loss=1.4502e+00 ppl=4.26 best_loss=1.4416e+00 best_ppl=4.23                                                
Epoch 24 - |param|=6.53e+02 |g_param|=1.19e+05 loss=1.2366e+00 ppl=3.44                                                 
Validation - loss=1.3219e+00 ppl=3.75 best_loss=1.4416e+00 best_ppl=4.23                                                
Epoch 25 - |param|=6.53e+02 |g_param|=6.79e+04 loss=1.1707e+00 ppl=3.22                                                 
Validation - loss=1.2960e+00 ppl=3.65 best_loss=1.3219e+00 best_ppl=3.75                                                
Epoch 26 - |param|=6.54e+02 |g_param|=5.20e+04 loss=1.1028e+00 ppl=3.01                                                 
Validation - loss=1.2347e+00 ppl=3.44 best_loss=1.2960e+00 best_ppl=3.65                                                
Epoch 27 - |param|=6.54e+02 |g_param|=6.93e+04 loss=1.0975e+00 ppl=3.00                                                 
Validation - loss=1.2385e+00 ppl=3.45 best_loss=1.2347e+00 best_ppl=3.44                                                
Epoch 28 - |param|=6.55e+02 |g_param|=8.22e+04 loss=1.1032e+00 ppl=3.01                                                 
Validation - loss=1.2505e+00 ppl=3.49 best_loss=1.2347e+00 best_ppl=3.44                                                
Epoch 29 - |param|=6.55e+02 |g_param|=4.37e+04 loss=9.5414e-01 ppl=2.60                                                 
Validation - loss=1.1717e+00 ppl=3.23 best_loss=1.2347e+00 best_ppl=3.44                                                
Epoch 30 - |param|=6.56e+02 |g_param|=7.72e+04 loss=9.8396e-01 ppl=2.68                                                 
Validation - loss=1.2193e+00 ppl=3.38 best_loss=1.1717e+00 best_ppl=3.23                                                
Epoch 31 - |param|=6.56e+02 |g_param|=5.11e+04 loss=9.2533e-01 ppl=2.52                                                 
Validation - loss=1.0824e+00 ppl=2.95 best_loss=1.1717e+00 best_ppl=3.23                                                
Epoch 32 - |param|=6.57e+02 |g_param|=9.03e+04 loss=9.4548e-01 ppl=2.57                                                 
Validation - loss=1.1261e+00 ppl=3.08 best_loss=1.0824e+00 best_ppl=2.95                                                
Epoch 33 - |param|=6.57e+02 |g_param|=4.63e+04 loss=8.3270e-01 ppl=2.30                                                 
Validation - loss=1.0917e+00 ppl=2.98 best_loss=1.0824e+00 best_ppl=2.95                                                
Epoch 34 - |param|=6.57e+02 |g_param|=3.71e+04 loss=7.6988e-01 ppl=2.16                                                 
Validation - loss=1.0709e+00 ppl=2.92 best_loss=1.0824e+00 best_ppl=2.95                                                
Epoch 35 - |param|=6.58e+02 |g_param|=3.38e+04 loss=7.4953e-01 ppl=2.12                                                 
Validation - loss=9.8542e-01 ppl=2.68 best_loss=1.0709e+00 best_ppl=2.92                                                
Epoch 36 - |param|=6.58e+02 |g_param|=4.57e+04 loss=7.2992e-01 ppl=2.07                                                 
Validation - loss=9.9081e-01 ppl=2.69 best_loss=9.8542e-01 best_ppl=2.68                                                
Epoch 37 - |param|=6.59e+02 |g_param|=4.72e+04 loss=7.4192e-01 ppl=2.10                                                 
Validation - loss=9.6699e-01 ppl=2.63 best_loss=9.8542e-01 best_ppl=2.68                                                
Epoch 38 - |param|=6.59e+02 |g_param|=3.27e+04 loss=6.7244e-01 ppl=1.96                                                 
Validation - loss=9.4168e-01 ppl=2.56 best_loss=9.6699e-01 best_ppl=2.63                                                
Epoch 39 - |param|=6.59e+02 |g_param|=5.33e+04 loss=6.9982e-01 ppl=2.01                                                 
Validation - loss=9.3004e-01 ppl=2.53 best_loss=9.4168e-01 best_ppl=2.56                                                
Epoch 40 - |param|=6.60e+02 |g_param|=5.85e+04 loss=7.1494e-01 ppl=2.04                                                 
Validation - loss=9.3550e-01 ppl=2.55 best_loss=9.3004e-01 best_ppl=2.53                                                
Epoch 41 - |param|=6.60e+02 |g_param|=3.97e+04 loss=6.5033e-01 ppl=1.92                                                 
Validation - loss=8.9893e-01 ppl=2.46 best_loss=9.3004e-01 best_ppl=2.53                                                
Epoch 42 - |param|=6.60e+02 |g_param|=5.62e+04 loss=6.4542e-01 ppl=1.91                                                 
Validation - loss=8.8331e-01 ppl=2.42 best_loss=8.9893e-01 best_ppl=2.46                                                
Epoch 43 - |param|=6.61e+02 |g_param|=4.14e+04 loss=6.1664e-01 ppl=1.85                                                 
Validation - loss=8.9890e-01 ppl=2.46 best_loss=8.8331e-01 best_ppl=2.42                                                
Epoch 44 - |param|=6.61e+02 |g_param|=3.24e+04 loss=5.6179e-01 ppl=1.75                                                 
Validation - loss=8.7355e-01 ppl=2.40 best_loss=8.8331e-01 best_ppl=2.42                                                
Epoch 45 - |param|=6.61e+02 |g_param|=7.24e+04 loss=5.7014e-01 ppl=1.77                                                 
Validation - loss=8.7198e-01 ppl=2.39 best_loss=8.7355e-01 best_ppl=2.40                                                
Epoch 46 - |param|=6.62e+02 |g_param|=8.51e+04 loss=5.6463e-01 ppl=1.76                                                 
Validation - loss=8.4936e-01 ppl=2.34 best_loss=8.7198e-01 best_ppl=2.39                                                
Epoch 47 - |param|=6.62e+02 |g_param|=9.66e+04 loss=5.5627e-01 ppl=1.74                                                 
Validation - loss=8.6411e-01 ppl=2.37 best_loss=8.4936e-01 best_ppl=2.34                                                
Epoch 48 - |param|=6.63e+02 |g_param|=8.28e+04 loss=5.3106e-01 ppl=1.70                                                 
Validation - loss=8.3397e-01 ppl=2.30 best_loss=8.4936e-01 best_ppl=2.34                                                
Epoch 49 - |param|=6.63e+02 |g_param|=1.00e+05 loss=5.5451e-01 ppl=1.74                                                 
Validation - loss=8.4328e-01 ppl=2.32 best_loss=8.3397e-01 best_ppl=2.30                                                
Epoch 50 - |param|=6.63e+02 |g_param|=7.64e+04 loss=4.9150e-01 ppl=1.63                                                 
Validation - loss=8.6636e-01 ppl=2.38 best_loss=8.3397e-01 best_ppl=2.30                                                
Epoch 51 - |param|=6.64e+02 |g_param|=6.92e+04 loss=4.7193e-01 ppl=1.60                                                 
Validation - loss=8.2983e-01 ppl=2.29 best_loss=8.3397e-01 best_ppl=2.30                                                
Epoch 52 - |param|=6.64e+02 |g_param|=4.55e+04 loss=4.6642e-01 ppl=1.59                                                 
Validation - loss=8.1546e-01 ppl=2.26 best_loss=8.2983e-01 best_ppl=2.29                                                
Epoch 53 - |param|=6.64e+02 |g_param|=2.61e+04 loss=4.4739e-01 ppl=1.56                                                 
Validation - loss=8.1556e-01 ppl=2.26 best_loss=8.1546e-01 best_ppl=2.26                                                
Epoch 54 - |param|=6.65e+02 |g_param|=2.76e+04 loss=4.3825e-01 ppl=1.55                                                 
Validation - loss=8.0179e-01 ppl=2.23 best_loss=8.1546e-01 best_ppl=2.26                                                
Epoch 55 - |param|=6.65e+02 |g_param|=2.93e+04 loss=4.4075e-01 ppl=1.55                                                 
Validation - loss=8.0075e-01 ppl=2.23 best_loss=8.0179e-01 best_ppl=2.23                                                
Epoch 56 - |param|=6.65e+02 |g_param|=4.04e+04 loss=4.5852e-01 ppl=1.58                                                 
Validation - loss=8.0533e-01 ppl=2.24 best_loss=8.0075e-01 best_ppl=2.23                                                
Epoch 57 - |param|=6.66e+02 |g_param|=2.74e+04 loss=4.1616e-01 ppl=1.52                                                 
Validation - loss=8.0421e-01 ppl=2.23 best_loss=8.0075e-01 best_ppl=2.23                                                
Epoch 58 - |param|=6.66e+02 |g_param|=2.55e+04 loss=3.9191e-01 ppl=1.48                                                 
Validation - loss=8.0763e-01 ppl=2.24 best_loss=8.0075e-01 best_ppl=2.23                                                
Epoch 59 - |param|=6.66e+02 |g_param|=4.31e+04 loss=4.3676e-01 ppl=1.55                                                 
Validation - loss=7.9721e-01 ppl=2.22 best_loss=8.0075e-01 best_ppl=2.23                                                
Epoch 60 - |param|=6.66e+02 |g_param|=3.40e+04 loss=3.9283e-01 ppl=1.48                                                 
Validation - loss=8.0779e-01 ppl=2.24 best_loss=7.9721e-01 best_ppl=2.22                                                

real	11m36.683s
user	11m26.999s
sys	0m9.621s
(simple-nmt) ye@:~/exp/simple-nmt$
```
testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-rkmy.01.4.45-85.94.4.08-59.05.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.3/0.4/0.0/0.0 (BP=0.934, ratio=0.936, hyp_len=22011, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.19-65.75.3.91-50.10.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.2/1.9/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=23162, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.4.08-59.35.3.80-44.58.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.2/2.7/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=23103, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.3.92-50.60.3.68-39.84.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.3/2.5/0.0/0.0 (BP=0.977, ratio=0.978, hyp_len=22985, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.83-46.17.3.59-36.35.pth
BLEU = 0.72, 24.0/4.4/0.5/0.0 (BP=0.998, ratio=0.998, hyp_len=23457, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.70-40.58.3.45-31.65.pth
BLEU = 1.97, 26.4/6.3/1.1/0.1 (BP=0.998, ratio=0.998, hyp_len=23471, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.54-34.57.3.34-28.23.pth
BLEU = 2.77, 29.1/8.2/1.7/0.1 (BP=0.998, ratio=0.998, hyp_len=23464, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.39-29.66.3.07-21.53.pth
BLEU = 4.99, 34.5/10.7/2.7/0.7 (BP=0.985, ratio=0.985, hyp_len=23167, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.14-23.07.2.86-17.48.pth
BLEU = 6.31, 37.0/12.7/3.4/1.0 (BP=0.986, ratio=0.986, hyp_len=23184, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.2.82-16.71.2.67-14.39.pth
BLEU = 8.61, 40.0/16.2/5.3/1.7 (BP=0.986, ratio=0.986, hyp_len=23185, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.2.63-13.81.2.47-11.85.pth
BLEU = 12.77, 44.7/20.3/8.3/3.5 (BP=1.000, ratio=1.002, hyp_len=23551, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.51-12.26.2.32-10.23.pth
BLEU = 13.82, 46.2/21.7/9.1/4.0 (BP=1.000, ratio=1.008, hyp_len=23690, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.28-9.76.2.23-9.31.pth
BLEU = 15.87, 48.6/24.3/10.8/5.0 (BP=1.000, ratio=1.027, hyp_len=24149, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.17-8.80.2.11-8.22.pth
BLEU = 18.71, 52.0/27.9/13.4/6.3 (BP=1.000, ratio=1.026, hyp_len=24125, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.2.05-7.73.2.07-7.96.pth
BLEU = 20.57, 53.2/29.3/15.0/7.7 (BP=1.000, ratio=1.050, hyp_len=24680, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.1.99-7.35.1.94-6.96.pth
BLEU = 23.90, 57.0/32.7/17.9/10.0 (BP=0.995, ratio=0.995, hyp_len=23400, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.1.84-6.28.1.81-6.13.pth
BLEU = 28.43, 60.2/37.3/22.2/13.1 (BP=1.000, ratio=1.019, hyp_len=23948, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.69-5.44.1.68-5.37.pth
BLEU = 31.92, 63.0/40.8/25.4/15.9 (BP=1.000, ratio=1.010, hyp_len=23738, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.61-5.00.1.63-5.10.pth
BLEU = 34.87, 64.8/43.4/28.2/18.6 (BP=1.000, ratio=1.005, hyp_len=23627, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.46-4.33.1.52-4.59.pth
BLEU = 39.59, 68.0/47.8/32.9/23.0 (BP=1.000, ratio=1.010, hyp_len=23737, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.41-4.09.1.49-4.42.pth
BLEU = 41.69, 69.8/50.0/35.0/24.8 (BP=1.000, ratio=1.003, hyp_len=23583, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.42-4.15.1.44-4.23.pth
BLEU = 43.42, 70.7/51.4/36.7/26.6 (BP=1.000, ratio=1.006, hyp_len=23659, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.1.32-3.73.1.45-4.26.pth
BLEU = 43.70, 70.9/51.7/37.0/26.9 (BP=1.000, ratio=1.011, hyp_len=23772, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.1.24-3.44.1.32-3.75.pth
BLEU = 48.12, 73.4/55.8/41.7/31.4 (BP=1.000, ratio=1.017, hyp_len=23916, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.1.17-3.22.1.30-3.65.pth
BLEU = 49.57, 74.7/57.2/43.1/32.8 (BP=1.000, ratio=1.012, hyp_len=23798, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.1.10-3.01.1.23-3.44.pth
BLEU = 52.02, 76.2/59.4/45.6/35.5 (BP=1.000, ratio=1.015, hyp_len=23861, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.1.10-3.00.1.24-3.45.pth
BLEU = 51.89, 76.2/59.4/45.5/35.3 (BP=1.000, ratio=1.014, hyp_len=23827, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.1.10-3.01.1.25-3.49.pth
BLEU = 51.62, 75.7/59.0/45.2/35.2 (BP=1.000, ratio=1.028, hyp_len=24161, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.95-2.60.1.17-3.23.pth
BLEU = 56.91, 79.1/63.7/50.8/41.0 (BP=1.000, ratio=1.007, hyp_len=23681, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.98-2.68.1.22-3.38.pth
BLEU = 54.45, 77.1/61.6/48.2/38.4 (BP=1.000, ratio=1.031, hyp_len=24228, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.31.0.93-2.52.1.08-2.95.pth
BLEU = 59.20, 80.2/65.7/53.2/43.8 (BP=1.000, ratio=1.020, hyp_len=23979, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.32.0.95-2.57.1.13-3.08.pth
BLEU = 56.90, 78.5/64.0/50.8/41.1 (BP=1.000, ratio=1.042, hyp_len=24494, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.33.0.83-2.30.1.09-2.98.pth
BLEU = 58.87, 79.9/65.3/52.9/43.5 (BP=1.000, ratio=1.019, hyp_len=23952, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.34.0.77-2.16.1.07-2.92.pth
BLEU = 63.04, 82.6/69.1/57.3/48.3 (BP=1.000, ratio=1.005, hyp_len=23628, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.35.0.75-2.12.0.99-2.68.pth
BLEU = 64.01, 82.8/69.8/58.4/49.6 (BP=1.000, ratio=1.014, hyp_len=23836, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.36.0.73-2.07.0.99-2.69.pth
BLEU = 63.67, 82.6/69.6/58.1/49.2 (BP=1.000, ratio=1.018, hyp_len=23936, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.37.0.74-2.10.0.97-2.63.pth
BLEU = 66.08, 83.9/71.6/60.7/52.2 (BP=1.000, ratio=1.010, hyp_len=23739, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.38.0.67-1.96.0.94-2.56.pth
BLEU = 65.31, 83.2/71.0/59.9/51.4 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.39.0.70-2.01.0.93-2.53.pth
BLEU = 65.37, 83.1/71.0/60.0/51.6 (BP=1.000, ratio=1.027, hyp_len=24139, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.40.0.71-2.04.0.94-2.55.pth
BLEU = 65.33, 83.3/70.9/59.9/51.5 (BP=1.000, ratio=1.021, hyp_len=24008, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.41.0.65-1.92.0.90-2.46.pth
BLEU = 66.86, 84.0/72.2/61.6/53.5 (BP=1.000, ratio=1.026, hyp_len=24128, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.42.0.65-1.91.0.88-2.42.pth
BLEU = 67.77, 84.4/73.0/62.7/54.6 (BP=1.000, ratio=1.022, hyp_len=24034, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.43.0.62-1.85.0.90-2.46.pth
BLEU = 68.24, 84.9/73.4/63.1/55.1 (BP=1.000, ratio=1.016, hyp_len=23890, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.44.0.56-1.75.0.87-2.40.pth
BLEU = 69.28, 85.3/74.3/64.2/56.6 (BP=1.000, ratio=1.025, hyp_len=24094, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.45.0.57-1.77.0.87-2.39.pth
BLEU = 69.44, 85.6/74.4/64.4/56.7 (BP=1.000, ratio=1.018, hyp_len=23925, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.46.0.56-1.76.0.85-2.34.pth
BLEU = 69.05, 85.1/74.1/64.1/56.3 (BP=1.000, ratio=1.026, hyp_len=24118, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.47.0.56-1.74.0.86-2.37.pth
BLEU = 68.40, 85.2/73.7/63.3/55.1 (BP=1.000, ratio=1.013, hyp_len=23823, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.48.0.53-1.70.0.83-2.30.pth
BLEU = 69.01, 85.1/74.1/64.0/56.3 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.49.0.55-1.74.0.84-2.32.pth
BLEU = 68.97, 85.0/74.0/64.0/56.2 (BP=1.000, ratio=1.030, hyp_len=24210, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.50.0.49-1.63.0.87-2.38.pth
BLEU = 70.51, 85.9/75.3/65.7/58.1 (BP=1.000, ratio=1.023, hyp_len=24042, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.51.0.47-1.60.0.83-2.29.pth
BLEU = 71.83, 86.6/76.4/67.1/60.0 (BP=1.000, ratio=1.020, hyp_len=23977, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.52.0.47-1.59.0.82-2.26.pth
BLEU = 71.44, 86.1/76.1/66.7/59.6 (BP=1.000, ratio=1.029, hyp_len=24190, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.53.0.45-1.56.0.82-2.26.pth
BLEU = 71.89, 86.6/76.4/67.2/60.1 (BP=1.000, ratio=1.021, hyp_len=24010, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.54.0.44-1.55.0.80-2.23.pth
BLEU = 72.05, 86.4/76.5/67.4/60.4 (BP=1.000, ratio=1.028, hyp_len=24166, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.55.0.44-1.55.0.80-2.23.pth
BLEU = 71.66, 86.2/76.2/67.0/59.9 (BP=1.000, ratio=1.029, hyp_len=24191, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.56.0.46-1.58.0.81-2.24.pth
BLEU = 71.26, 86.1/75.9/66.5/59.3 (BP=1.000, ratio=1.027, hyp_len=24143, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.57.0.42-1.52.0.80-2.23.pth
BLEU = 72.00, 86.4/76.5/67.4/60.4 (BP=1.000, ratio=1.029, hyp_len=24191, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth
BLEU = 72.06, 86.3/76.5/67.5/60.5 (BP=1.000, ratio=1.032, hyp_len=24261, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.59.0.44-1.55.0.80-2.22.pth
BLEU = 70.41, 85.4/75.2/65.6/58.3 (BP=1.000, ratio=1.042, hyp_len=24491, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.60.0.39-1.48.0.81-2.24.pth
BLEU = 71.05, 85.8/75.7/66.3/59.1 (BP=1.000, ratio=1.036, hyp_len=24358, ref_len=23509)

real	19m25.593s
user	18m57.084s
sys	1m7.034s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-60epoch$
```

best BLEU score of seq, 60 epoch, rk-my:  

```
Evaluation result for the model: seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth
BLEU = 72.06, 86.3/76.5/67.5/60.5 (BP=1.000, ratio=1.032, hyp_len=24261, ref_len=23509)
```

###  seq2seq 70 eopch model, rk-my

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 70 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.pth',
    'n_epochs': 70,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 1 - |param|=6.42e+02 |g_param|=2.00e+05 loss=4.4840e+00 ppl=88.59                                                 
Validation - loss=4.1055e+00 ppl=60.67 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.42e+02 |g_param|=1.89e+05 loss=4.1489e+00 ppl=63.36                                                 
Validation - loss=3.9057e+00 ppl=49.68 best_loss=4.1055e+00 best_ppl=60.67                                              
Epoch 3 - |param|=6.42e+02 |g_param|=1.82e+05 loss=4.0657e+00 ppl=58.31                                                 
Validation - loss=3.8146e+00 ppl=45.36 best_loss=3.9057e+00 best_ppl=49.68                                              
Epoch 4 - |param|=6.42e+02 |g_param|=1.97e+05 loss=3.9984e+00 ppl=54.51                                                 
Validation - loss=3.7428e+00 ppl=42.22 best_loss=3.8146e+00 best_ppl=45.36                                              
Epoch 5 - |param|=6.43e+02 |g_param|=1.94e+05 loss=3.9004e+00 ppl=49.42                                                 
Validation - loss=3.6777e+00 ppl=39.56 best_loss=3.7428e+00 best_ppl=42.22                                              
Epoch 6 - |param|=6.43e+02 |g_param|=2.16e+05 loss=3.9033e+00 ppl=49.57                                                 
Validation - loss=3.5853e+00 ppl=36.06 best_loss=3.6777e+00 best_ppl=39.56                                              
Epoch 7 - |param|=6.44e+02 |g_param|=2.06e+05 loss=3.7389e+00 ppl=42.05                                                 
Validation - loss=3.4675e+00 ppl=32.06 best_loss=3.5853e+00 best_ppl=36.06                                              
Epoch 8 - |param|=6.44e+02 |g_param|=2.11e+05 loss=3.5419e+00 ppl=34.53                                                 
Validation - loss=3.2737e+00 ppl=26.41 best_loss=3.4675e+00 best_ppl=32.06                                              
Epoch 9 - |param|=6.45e+02 |g_param|=2.12e+05 loss=3.3710e+00 ppl=29.11                                                 
Validation - loss=3.2155e+00 ppl=24.92 best_loss=3.2737e+00 best_ppl=26.41                                              
Epoch 10 - |param|=6.46e+02 |g_param|=2.26e+05 loss=3.2754e+00 ppl=26.45                                                
Validation - loss=3.0287e+00 ppl=20.67 best_loss=3.2155e+00 best_ppl=24.92                                              
Epoch 11 - |param|=6.46e+02 |g_param|=2.01e+05 loss=3.0581e+00 ppl=21.29                                                
Validation - loss=2.8705e+00 ppl=17.65 best_loss=3.0287e+00 best_ppl=20.67                                              
Epoch 12 - |param|=6.47e+02 |g_param|=2.21e+05 loss=2.9488e+00 ppl=19.08                                                
Validation - loss=2.7662e+00 ppl=15.90 best_loss=2.8705e+00 best_ppl=17.65                                              
Epoch 13 - |param|=6.47e+02 |g_param|=2.05e+05 loss=2.7942e+00 ppl=16.35                                                
Validation - loss=2.6226e+00 ppl=13.77 best_loss=2.7662e+00 best_ppl=15.90                                              
Epoch 14 - |param|=6.48e+02 |g_param|=2.17e+05 loss=2.6469e+00 ppl=14.11                                                
Validation - loss=2.4491e+00 ppl=11.58 best_loss=2.6226e+00 best_ppl=13.77                                              
Epoch 15 - |param|=6.49e+02 |g_param|=1.67e+05 loss=2.3413e+00 ppl=10.39                                                
Validation - loss=2.2370e+00 ppl=9.37 best_loss=2.4491e+00 best_ppl=11.58                                               
Epoch 16 - |param|=6.50e+02 |g_param|=1.63e+05 loss=2.1834e+00 ppl=8.88                                                 
Validation - loss=2.0599e+00 ppl=7.84 best_loss=2.2370e+00 best_ppl=9.37                                                
Epoch 17 - |param|=6.50e+02 |g_param|=1.66e+05 loss=1.8751e+00 ppl=6.52                                                 
Validation - loss=1.9022e+00 ppl=6.70 best_loss=2.0599e+00 best_ppl=7.84                                                
Epoch 18 - |param|=6.51e+02 |g_param|=1.59e+05 loss=1.7461e+00 ppl=5.73                                                 
Validation - loss=1.7030e+00 ppl=5.49 best_loss=1.9022e+00 best_ppl=6.70                                                
Epoch 19 - |param|=6.52e+02 |g_param|=2.04e+05 loss=1.5618e+00 ppl=4.77                                                 
Validation - loss=1.5763e+00 ppl=4.84 best_loss=1.7030e+00 best_ppl=5.49                                                
Epoch 20 - |param|=6.52e+02 |g_param|=1.17e+05 loss=1.4061e+00 ppl=4.08                                                 
Validation - loss=1.4422e+00 ppl=4.23 best_loss=1.5763e+00 best_ppl=4.84                                                
Epoch 21 - |param|=6.53e+02 |g_param|=1.45e+05 loss=1.4201e+00 ppl=4.14                                                 
Validation - loss=1.4804e+00 ppl=4.39 best_loss=1.4422e+00 best_ppl=4.23                                                
Epoch 22 - |param|=6.53e+02 |g_param|=9.49e+04 loss=1.2451e+00 ppl=3.47                                                 
Validation - loss=1.2579e+00 ppl=3.52 best_loss=1.4422e+00 best_ppl=4.23                                                
Epoch 23 - |param|=6.54e+02 |g_param|=8.51e+04 loss=1.1094e+00 ppl=3.03                                                 
Validation - loss=1.2027e+00 ppl=3.33 best_loss=1.2579e+00 best_ppl=3.52                                                
Epoch 24 - |param|=6.54e+02 |g_param|=9.24e+04 loss=1.0664e+00 ppl=2.90                                                 
Validation - loss=1.1587e+00 ppl=3.19 best_loss=1.2027e+00 best_ppl=3.33                                                
Epoch 25 - |param|=6.55e+02 |g_param|=6.75e+04 loss=9.6101e-01 ppl=2.61                                                 
Validation - loss=1.0724e+00 ppl=2.92 best_loss=1.1587e+00 best_ppl=3.19                                                
Epoch 26 - |param|=6.55e+02 |g_param|=8.47e+04 loss=9.2313e-01 ppl=2.52                                                 
Validation - loss=1.0332e+00 ppl=2.81 best_loss=1.0724e+00 best_ppl=2.92                                                
Epoch 27 - |param|=6.56e+02 |g_param|=6.39e+04 loss=8.3044e-01 ppl=2.29                                                 
Validation - loss=1.0084e+00 ppl=2.74 best_loss=1.0332e+00 best_ppl=2.81                                                
Epoch 28 - |param|=6.56e+02 |g_param|=7.28e+04 loss=8.1396e-01 ppl=2.26                                                 
Validation - loss=9.8583e-01 ppl=2.68 best_loss=1.0084e+00 best_ppl=2.74                                                
Epoch 29 - |param|=6.57e+02 |g_param|=7.50e+04 loss=7.7961e-01 ppl=2.18                                                 
Validation - loss=9.5282e-01 ppl=2.59 best_loss=9.8583e-01 best_ppl=2.68                                                
Epoch 30 - |param|=6.57e+02 |g_param|=7.44e+04 loss=7.3944e-01 ppl=2.09                                                 
Validation - loss=9.2275e-01 ppl=2.52 best_loss=9.5282e-01 best_ppl=2.59                                                
Epoch 31 - |param|=6.57e+02 |g_param|=7.91e+04 loss=6.9912e-01 ppl=2.01                                                 
Validation - loss=8.8678e-01 ppl=2.43 best_loss=9.2275e-01 best_ppl=2.52                                                
Epoch 32 - |param|=6.58e+02 |g_param|=7.21e+04 loss=6.8023e-01 ppl=1.97                                                 
Validation - loss=8.5229e-01 ppl=2.35 best_loss=8.8678e-01 best_ppl=2.43                                                
Epoch 33 - |param|=6.58e+02 |g_param|=9.27e+04 loss=6.6335e-01 ppl=1.94                                                 
Validation - loss=8.7251e-01 ppl=2.39 best_loss=8.5229e-01 best_ppl=2.35                                                
Epoch 34 - |param|=6.59e+02 |g_param|=8.37e+04 loss=6.7237e-01 ppl=1.96                                                 
Validation - loss=8.5760e-01 ppl=2.36 best_loss=8.5229e-01 best_ppl=2.35                                                
Epoch 35 - |param|=6.59e+02 |g_param|=6.46e+04 loss=5.9028e-01 ppl=1.80                                                 
Validation - loss=8.1710e-01 ppl=2.26 best_loss=8.5229e-01 best_ppl=2.35                                                
Epoch 36 - |param|=6.60e+02 |g_param|=6.65e+04 loss=5.6772e-01 ppl=1.76                                                 
Validation - loss=8.0807e-01 ppl=2.24 best_loss=8.1710e-01 best_ppl=2.26                                                
Epoch 37 - |param|=6.60e+02 |g_param|=6.72e+04 loss=5.6678e-01 ppl=1.76                                                 
Validation - loss=8.0070e-01 ppl=2.23 best_loss=8.0807e-01 best_ppl=2.24                                                
Epoch 38 - |param|=6.60e+02 |g_param|=5.50e+04 loss=5.2344e-01 ppl=1.69                                                 
Validation - loss=7.7108e-01 ppl=2.16 best_loss=8.0070e-01 best_ppl=2.23                                                
Epoch 39 - |param|=6.61e+02 |g_param|=4.96e+04 loss=5.0919e-01 ppl=1.66                                                 
Validation - loss=7.6191e-01 ppl=2.14 best_loss=7.7108e-01 best_ppl=2.16                                                
Epoch 40 - |param|=6.61e+02 |g_param|=5.60e+04 loss=5.1910e-01 ppl=1.68                                                 
Validation - loss=7.6362e-01 ppl=2.15 best_loss=7.6191e-01 best_ppl=2.14                                                
Epoch 41 - |param|=6.61e+02 |g_param|=1.18e+05 loss=4.7796e-01 ppl=1.61                                                 
Validation - loss=7.6776e-01 ppl=2.15 best_loss=7.6191e-01 best_ppl=2.14                                                
Epoch 42 - |param|=6.62e+02 |g_param|=1.18e+05 loss=4.6916e-01 ppl=1.60                                                 
Validation - loss=7.6663e-01 ppl=2.15 best_loss=7.6191e-01 best_ppl=2.14                                                
Epoch 43 - |param|=6.62e+02 |g_param|=1.15e+05 loss=4.5571e-01 ppl=1.58                                                 
Validation - loss=7.3056e-01 ppl=2.08 best_loss=7.6191e-01 best_ppl=2.14                                                
Epoch 44 - |param|=6.62e+02 |g_param|=9.52e+04 loss=4.1942e-01 ppl=1.52                                                 
Validation - loss=7.3427e-01 ppl=2.08 best_loss=7.3056e-01 best_ppl=2.08                                                
Epoch 45 - |param|=6.63e+02 |g_param|=9.06e+04 loss=4.2516e-01 ppl=1.53                                                 
Validation - loss=7.3423e-01 ppl=2.08 best_loss=7.3056e-01 best_ppl=2.08                                                
Epoch 46 - |param|=6.63e+02 |g_param|=1.18e+05 loss=4.1865e-01 ppl=1.52                                                 
Validation - loss=7.2417e-01 ppl=2.06 best_loss=7.3056e-01 best_ppl=2.08                                                
Epoch 47 - |param|=6.63e+02 |g_param|=1.13e+05 loss=4.2364e-01 ppl=1.53                                                 
Validation - loss=7.0119e-01 ppl=2.02 best_loss=7.2417e-01 best_ppl=2.06                                                
Epoch 48 - |param|=6.64e+02 |g_param|=1.20e+05 loss=4.0518e-01 ppl=1.50                                                 
Validation - loss=7.1042e-01 ppl=2.03 best_loss=7.0119e-01 best_ppl=2.02                                                
Epoch 49 - |param|=6.64e+02 |g_param|=1.09e+05 loss=4.0807e-01 ppl=1.50                                                 
Validation - loss=6.8721e-01 ppl=1.99 best_loss=7.0119e-01 best_ppl=2.02                                                
Epoch 50 - |param|=6.64e+02 |g_param|=1.13e+05 loss=3.9893e-01 ppl=1.49                                                 
Validation - loss=7.0628e-01 ppl=2.03 best_loss=6.8721e-01 best_ppl=1.99                                                
Epoch 51 - |param|=6.65e+02 |g_param|=9.89e+04 loss=3.6020e-01 ppl=1.43                                                 
Validation - loss=6.8957e-01 ppl=1.99 best_loss=6.8721e-01 best_ppl=1.99                                                
Epoch 52 - |param|=6.65e+02 |g_param|=9.59e+04 loss=3.7144e-01 ppl=1.45                                                 
Validation - loss=6.8995e-01 ppl=1.99 best_loss=6.8721e-01 best_ppl=1.99                                                
Epoch 53 - |param|=6.65e+02 |g_param|=1.05e+05 loss=3.5966e-01 ppl=1.43                                                 
Validation - loss=7.1169e-01 ppl=2.04 best_loss=6.8721e-01 best_ppl=1.99                                                
Epoch 54 - |param|=6.66e+02 |g_param|=4.84e+04 loss=3.5174e-01 ppl=1.42                                                 
Validation - loss=6.7136e-01 ppl=1.96 best_loss=6.8721e-01 best_ppl=1.99                                                
Epoch 55 - |param|=6.66e+02 |g_param|=4.88e+04 loss=3.4511e-01 ppl=1.41                                                 
Validation - loss=6.9179e-01 ppl=2.00 best_loss=6.7136e-01 best_ppl=1.96                                                
Epoch 56 - |param|=6.66e+02 |g_param|=5.12e+04 loss=3.3863e-01 ppl=1.40                                                 
Validation - loss=6.8109e-01 ppl=1.98 best_loss=6.7136e-01 best_ppl=1.96                                                
Epoch 57 - |param|=6.67e+02 |g_param|=5.54e+04 loss=3.2907e-01 ppl=1.39                                                 
Validation - loss=6.8277e-01 ppl=1.98 best_loss=6.7136e-01 best_ppl=1.96                                                
Epoch 58 - |param|=6.67e+02 |g_param|=5.28e+04 loss=3.4111e-01 ppl=1.41                                                 
Validation - loss=6.8193e-01 ppl=1.98 best_loss=6.7136e-01 best_ppl=1.96                                                
Epoch 59 - |param|=6.67e+02 |g_param|=4.37e+04 loss=3.2456e-01 ppl=1.38                                                 
Validation - loss=6.6696e-01 ppl=1.95 best_loss=6.7136e-01 best_ppl=1.96                                                
Epoch 60 - |param|=6.68e+02 |g_param|=4.99e+04 loss=3.3031e-01 ppl=1.39                                                 
Validation - loss=6.8429e-01 ppl=1.98 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 61 - |param|=6.68e+02 |g_param|=6.42e+04 loss=3.4601e-01 ppl=1.41                                                 
Validation - loss=7.0068e-01 ppl=2.02 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 62 - |param|=6.68e+02 |g_param|=6.29e+04 loss=3.3995e-01 ppl=1.40                                                 
Validation - loss=6.7724e-01 ppl=1.97 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 63 - |param|=6.69e+02 |g_param|=5.02e+04 loss=3.0390e-01 ppl=1.36                                                 
Validation - loss=6.9498e-01 ppl=2.00 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 64 - |param|=6.69e+02 |g_param|=8.99e+04 loss=3.2256e-01 ppl=1.38                                                 
Validation - loss=7.2417e-01 ppl=2.06 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 65 - |param|=6.69e+02 |g_param|=4.44e+04 loss=2.9973e-01 ppl=1.35                                                 
Validation - loss=6.5541e-01 ppl=1.93 best_loss=6.6696e-01 best_ppl=1.95                                                
Epoch 66 - |param|=6.70e+02 |g_param|=4.62e+04 loss=2.8996e-01 ppl=1.34                                                 
Validation - loss=6.4889e-01 ppl=1.91 best_loss=6.5541e-01 best_ppl=1.93                                                
Epoch 67 - |param|=6.70e+02 |g_param|=3.90e+04 loss=2.7005e-01 ppl=1.31                                                 
Validation - loss=6.5807e-01 ppl=1.93 best_loss=6.4889e-01 best_ppl=1.91                                                
Epoch 68 - |param|=6.70e+02 |g_param|=4.02e+04 loss=2.7849e-01 ppl=1.32                                                 
Validation - loss=6.7825e-01 ppl=1.97 best_loss=6.4889e-01 best_ppl=1.91                                                
Epoch 69 - |param|=6.70e+02 |g_param|=4.55e+04 loss=2.8645e-01 ppl=1.33                                                 
Validation - loss=6.4954e-01 ppl=1.91 best_loss=6.4889e-01 best_ppl=1.91                                                
Epoch 70 - |param|=6.71e+02 |g_param|=3.58e+04 loss=2.7859e-01 ppl=1.32                                                 
Validation - loss=6.4205e-01 ppl=1.90 best_loss=6.4889e-01 best_ppl=1.91                                                

real	13m23.765s
user	13m11.266s
sys	0m11.289s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-rkmy.01.4.48-88.59.4.11-60.67.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.4/0.1/0.0/0.0 (BP=1.000, ratio=1.152, hyp_len=27091, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.15-63.36.3.91-49.68.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.9/0.4/0.0/0.0 (BP=1.000, ratio=1.004, hyp_len=23609, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.4.07-58.31.3.81-45.36.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.0/2.6/0.1/0.0 (BP=0.978, ratio=0.978, hyp_len=22998, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.4.00-54.51.3.74-42.22.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.3/2.4/0.1/0.0 (BP=0.979, ratio=0.979, hyp_len=23022, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.90-49.42.3.68-39.56.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.8/3.2/0.3/0.0 (BP=0.987, ratio=0.987, hyp_len=23197, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.90-49.57.3.59-36.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.9/4.5/0.5/0.0 (BP=0.987, ratio=0.987, hyp_len=23208, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.74-42.05.3.47-32.06.pth
BLEU = 0.85, 24.4/5.6/0.7/0.0 (BP=0.992, ratio=0.992, hyp_len=23316, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.54-34.53.3.27-26.41.pth
BLEU = 2.17, 28.8/7.4/1.3/0.1 (BP=0.989, ratio=0.989, hyp_len=23241, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.37-29.11.3.22-24.92.pth
BLEU = 3.19, 30.2/8.3/1.7/0.3 (BP=0.960, ratio=0.961, hyp_len=22589, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.3.28-26.45.3.03-20.67.pth
BLEU = 4.28, 31.5/9.6/2.2/0.5 (BP=1.000, ratio=1.027, hyp_len=24133, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.3.06-21.29.2.87-17.65.pth
BLEU = 5.75, 34.8/11.7/3.2/0.8 (BP=1.000, ratio=1.003, hyp_len=23590, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.95-19.08.2.77-15.90.pth
BLEU = 6.98, 36.0/13.0/4.1/1.2 (BP=1.000, ratio=1.008, hyp_len=23686, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.79-16.35.2.62-13.77.pth
BLEU = 7.79, 37.9/14.2/4.4/1.5 (BP=1.000, ratio=1.025, hyp_len=24106, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.65-14.11.2.45-11.58.pth
BLEU = 11.03, 42.4/17.7/6.9/2.8 (BP=1.000, ratio=1.008, hyp_len=23688, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.2.34-10.39.2.24-9.37.pth
BLEU = 15.29, 48.0/23.3/10.3/4.7 (BP=1.000, ratio=1.004, hyp_len=23608, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.2.18-8.88.2.06-7.84.pth
BLEU = 18.66, 51.0/27.0/13.3/6.6 (BP=1.000, ratio=1.053, hyp_len=24755, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.1.88-6.52.1.90-6.70.pth
BLEU = 23.15, 55.5/31.7/17.3/9.4 (BP=1.000, ratio=1.012, hyp_len=23793, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.75-5.73.1.70-5.49.pth
BLEU = 30.70, 61.5/39.4/24.3/15.1 (BP=1.000, ratio=1.024, hyp_len=24072, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.56-4.77.1.58-4.84.pth
BLEU = 34.88, 65.1/43.7/28.3/18.4 (BP=1.000, ratio=1.016, hyp_len=23889, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.41-4.08.1.44-4.23.pth
BLEU = 40.64, 68.7/48.7/34.0/24.0 (BP=1.000, ratio=1.020, hyp_len=23973, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.42-4.14.1.48-4.39.pth
BLEU = 39.64, 67.4/47.7/33.2/23.1 (BP=1.000, ratio=1.045, hyp_len=24576, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.25-3.47.1.26-3.52.pth
BLEU = 48.83, 73.9/56.2/42.3/32.3 (BP=1.000, ratio=1.010, hyp_len=23750, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.1.11-3.03.1.20-3.33.pth
BLEU = 51.15, 75.1/58.4/44.8/34.8 (BP=1.000, ratio=1.015, hyp_len=23851, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.1.07-2.90.1.16-3.19.pth
BLEU = 53.77, 76.6/60.7/47.6/37.8 (BP=1.000, ratio=1.014, hyp_len=23832, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.0.96-2.61.1.07-2.92.pth
BLEU = 56.66, 78.4/63.3/50.6/41.1 (BP=1.000, ratio=1.021, hyp_len=24004, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.0.92-2.52.1.03-2.81.pth
BLEU = 58.56, 79.4/64.9/52.7/43.4 (BP=1.000, ratio=1.022, hyp_len=24024, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.0.83-2.29.1.01-2.74.pth
BLEU = 60.47, 80.7/66.6/54.6/45.6 (BP=1.000, ratio=1.014, hyp_len=23828, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.0.81-2.26.0.99-2.68.pth
BLEU = 60.59, 80.3/66.7/54.9/45.8 (BP=1.000, ratio=1.031, hyp_len=24239, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.78-2.18.0.95-2.59.pth
BLEU = 61.76, 80.9/67.6/56.2/47.3 (BP=1.000, ratio=1.031, hyp_len=24234, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.74-2.09.0.92-2.52.pth
BLEU = 64.08, 82.3/69.7/58.7/50.0 (BP=1.000, ratio=1.019, hyp_len=23949, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.31.0.70-2.01.0.89-2.43.pth
BLEU = 64.68, 82.9/70.3/59.3/50.7 (BP=1.000, ratio=1.022, hyp_len=24031, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.32.0.68-1.97.0.85-2.35.pth
BLEU = 66.10, 83.5/71.5/60.8/52.6 (BP=1.000, ratio=1.026, hyp_len=24113, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.33.0.66-1.94.0.87-2.39.pth
BLEU = 66.20, 83.6/71.6/61.0/52.6 (BP=1.000, ratio=1.025, hyp_len=24098, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.34.0.67-1.96.0.86-2.36.pth
BLEU = 64.84, 82.7/70.4/59.5/51.0 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.35.0.59-1.80.0.82-2.26.pth
BLEU = 68.51, 84.7/73.6/63.5/55.6 (BP=1.000, ratio=1.023, hyp_len=24042, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.36.0.57-1.76.0.81-2.24.pth
BLEU = 69.24, 85.2/74.3/64.3/56.5 (BP=1.000, ratio=1.025, hyp_len=24092, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.37.0.57-1.76.0.80-2.23.pth
BLEU = 69.45, 85.3/74.4/64.5/56.8 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.38.0.52-1.69.0.77-2.16.pth
BLEU = 70.34, 85.6/75.1/65.6/58.1 (BP=1.000, ratio=1.029, hyp_len=24192, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.39.0.51-1.66.0.76-2.14.pth
BLEU = 71.02, 86.0/75.7/66.4/59.0 (BP=1.000, ratio=1.026, hyp_len=24122, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.40.0.52-1.68.0.76-2.15.pth
BLEU = 69.89, 85.3/74.7/65.0/57.6 (BP=1.000, ratio=1.038, hyp_len=24400, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.41.0.48-1.61.0.77-2.15.pth
BLEU = 71.21, 85.8/75.7/66.5/59.5 (BP=1.000, ratio=1.033, hyp_len=24282, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.42.0.47-1.60.0.77-2.15.pth
BLEU = 72.03, 86.5/76.5/67.4/60.3 (BP=1.000, ratio=1.028, hyp_len=24160, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.43.0.46-1.58.0.73-2.08.pth
BLEU = 71.85, 86.2/76.3/67.3/60.2 (BP=1.000, ratio=1.033, hyp_len=24286, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.44.0.42-1.52.0.73-2.08.pth
BLEU = 72.64, 86.7/77.0/68.1/61.2 (BP=1.000, ratio=1.029, hyp_len=24187, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.45.0.43-1.53.0.73-2.08.pth
BLEU = 72.12, 86.3/76.5/67.6/60.6 (BP=1.000, ratio=1.035, hyp_len=24327, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.46.0.42-1.52.0.72-2.06.pth
BLEU = 72.93, 86.9/77.2/68.4/61.6 (BP=1.000, ratio=1.031, hyp_len=24227, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.47.0.42-1.53.0.70-2.02.pth
BLEU = 72.41, 86.4/76.7/67.9/61.0 (BP=1.000, ratio=1.036, hyp_len=24365, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.48.0.41-1.50.0.71-2.03.pth
BLEU = 73.10, 86.9/77.4/68.6/61.8 (BP=1.000, ratio=1.034, hyp_len=24300, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.49.0.41-1.50.0.69-1.99.pth
BLEU = 73.47, 87.1/77.7/69.0/62.4 (BP=1.000, ratio=1.031, hyp_len=24230, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.50.0.40-1.49.0.71-2.03.pth
BLEU = 71.74, 86.2/76.2/67.1/60.1 (BP=1.000, ratio=1.039, hyp_len=24429, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.51.0.36-1.43.0.69-1.99.pth
BLEU = 72.94, 86.7/77.2/68.5/61.7 (BP=1.000, ratio=1.036, hyp_len=24355, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.52.0.37-1.45.0.69-1.99.pth
BLEU = 73.73, 87.2/77.8/69.3/62.8 (BP=1.000, ratio=1.033, hyp_len=24280, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.53.0.36-1.43.0.71-2.04.pth
BLEU = 73.38, 86.9/77.6/69.0/62.4 (BP=1.000, ratio=1.032, hyp_len=24255, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.54.0.35-1.42.0.67-1.96.pth
BLEU = 72.96, 86.7/77.2/68.5/61.8 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.55.0.35-1.41.0.69-2.00.pth
BLEU = 73.62, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.034, hyp_len=24297, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.56.0.34-1.40.0.68-1.98.pth
BLEU = 73.59, 87.1/77.7/69.2/62.6 (BP=1.000, ratio=1.032, hyp_len=24271, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.57.0.33-1.39.0.68-1.98.pth
BLEU = 72.08, 86.0/76.4/67.6/60.7 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.58.0.34-1.41.0.68-1.98.pth
BLEU = 72.31, 86.2/76.6/67.8/61.1 (BP=1.000, ratio=1.046, hyp_len=24584, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.59.0.32-1.38.0.67-1.95.pth
BLEU = 73.95, 87.2/78.0/69.6/63.1 (BP=1.000, ratio=1.034, hyp_len=24302, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.60.0.33-1.39.0.68-1.98.pth
BLEU = 72.27, 86.3/76.6/67.8/60.9 (BP=1.000, ratio=1.043, hyp_len=24512, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.61.0.35-1.41.0.70-2.02.pth
BLEU = 71.91, 86.2/76.3/67.3/60.4 (BP=1.000, ratio=1.043, hyp_len=24517, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.62.0.34-1.40.0.68-1.97.pth
BLEU = 73.80, 87.2/77.8/69.5/62.9 (BP=1.000, ratio=1.031, hyp_len=24241, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.63.0.30-1.36.0.69-2.00.pth
BLEU = 72.27, 86.2/76.6/67.8/61.0 (BP=1.000, ratio=1.046, hyp_len=24582, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.64.0.32-1.38.0.72-2.06.pth
BLEU = 70.37, 85.3/75.1/65.7/58.3 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.65.0.30-1.35.0.66-1.93.pth
BLEU = 74.38, 87.5/78.4/70.1/63.6 (BP=1.000, ratio=1.032, hyp_len=24273, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.66.0.29-1.34.0.65-1.91.pth
BLEU = 74.33, 87.4/78.3/70.1/63.6 (BP=1.000, ratio=1.033, hyp_len=24275, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth
BLEU = 74.84, 87.8/78.8/70.6/64.3 (BP=1.000, ratio=1.031, hyp_len=24242, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.68.0.28-1.32.0.68-1.97.pth
BLEU = 73.41, 86.9/77.5/69.0/62.4 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.69.0.29-1.33.0.65-1.91.pth
BLEU = 73.40, 86.9/77.6/69.0/62.3 (BP=1.000, ratio=1.041, hyp_len=24471, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.70.0.28-1.32.0.64-1.90.pth
BLEU = 73.11, 86.8/77.3/68.7/62.0 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)

real	23m22.224s
user	22m50.012s
sys	1m18.340s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-70epoch$
```

seq2seq, 70 epoch, rk-my မော်ဒယ်ရဲ့ အကောင်းဆုံး BLEU score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth
BLEU = 74.84, 87.8/78.8/70.6/64.3 (BP=1.000, ratio=1.031, hyp_len=24242, ref_len=23509)
```

### Transformer, my-rk, 40 epoch

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/myrk-40epoch/myrk-transformer-model.pth',
    'n_epochs': 40,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.63e+05 loss=5.7969e+00 ppl=329.28                                                
Validation - loss=5.8017e+00 ppl=330.87 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.23e+02 |g_param|=3.52e+05 loss=5.0093e+00 ppl=149.80                                                
Validation - loss=5.0331e+00 ppl=153.40 best_loss=5.8017e+00 best_ppl=330.87                                            
Epoch 3 - |param|=3.23e+02 |g_param|=2.38e+05 loss=4.5116e+00 ppl=91.07                                                 
Validation - loss=4.6116e+00 ppl=100.64 best_loss=5.0331e+00 best_ppl=153.40                                            
Epoch 4 - |param|=3.24e+02 |g_param|=1.92e+05 loss=4.2239e+00 ppl=68.30                                                 
Validation - loss=4.3389e+00 ppl=76.62 best_loss=4.6116e+00 best_ppl=100.64                                             
Epoch 5 - |param|=3.24e+02 |g_param|=1.60e+05 loss=4.0462e+00 ppl=57.18                                                 
Validation - loss=4.1266e+00 ppl=61.97 best_loss=4.3389e+00 best_ppl=76.62                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.48e+05 loss=3.8680e+00 ppl=47.84                                                 
Validation - loss=3.9383e+00 ppl=51.33 best_loss=4.1266e+00 best_ppl=61.97                                              
Epoch 7 - |param|=3.24e+02 |g_param|=2.07e+05 loss=3.6714e+00 ppl=39.31                                                 
Validation - loss=3.7755e+00 ppl=43.62 best_loss=3.9383e+00 best_ppl=51.33                                              
Epoch 8 - |param|=3.24e+02 |g_param|=1.40e+05 loss=3.5036e+00 ppl=33.23                                                 
Validation - loss=3.6194e+00 ppl=37.32 best_loss=3.7755e+00 best_ppl=43.62                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.91e+05 loss=3.3650e+00 ppl=28.93                                                 
Validation - loss=3.4839e+00 ppl=32.59 best_loss=3.6194e+00 best_ppl=37.32                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.57e+05 loss=3.2286e+00 ppl=25.24                                                
Validation - loss=3.3658e+00 ppl=28.96 best_loss=3.4839e+00 best_ppl=32.59                                              
Epoch 11 - |param|=3.24e+02 |g_param|=2.09e+05 loss=3.1941e+00 ppl=24.39                                                
Validation - loss=3.2547e+00 ppl=25.91 best_loss=3.3658e+00 best_ppl=28.96                                              
Epoch 12 - |param|=3.24e+02 |g_param|=2.64e+05 loss=3.0675e+00 ppl=21.49                                                
Validation - loss=3.1578e+00 ppl=23.52 best_loss=3.2547e+00 best_ppl=25.91                                              
Epoch 13 - |param|=3.24e+02 |g_param|=2.79e+05 loss=2.9714e+00 ppl=19.52                                                
Validation - loss=3.0733e+00 ppl=21.61 best_loss=3.1578e+00 best_ppl=23.52                                              
Epoch 14 - |param|=3.24e+02 |g_param|=2.81e+05 loss=2.8857e+00 ppl=17.92                                                
Validation - loss=2.9884e+00 ppl=19.85 best_loss=3.0733e+00 best_ppl=21.61                                              
Epoch 15 - |param|=3.24e+02 |g_param|=1.93e+05 loss=2.8747e+00 ppl=17.72                                                
Validation - loss=2.9056e+00 ppl=18.28 best_loss=2.9884e+00 best_ppl=19.85                                              
Epoch 16 - |param|=3.25e+02 |g_param|=2.30e+05 loss=2.7891e+00 ppl=16.27                                                
Validation - loss=2.8303e+00 ppl=16.95 best_loss=2.9056e+00 best_ppl=18.28                                              
Epoch 17 - |param|=3.25e+02 |g_param|=3.07e+05 loss=2.7752e+00 ppl=16.04                                                
Validation - loss=2.7655e+00 ppl=15.89 best_loss=2.8303e+00 best_ppl=16.95                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.14e+05 loss=2.6481e+00 ppl=14.13                                                
Validation - loss=2.7067e+00 ppl=14.98 best_loss=2.7655e+00 best_ppl=15.89                                              
Epoch 19 - |param|=3.25e+02 |g_param|=2.88e+05 loss=2.5858e+00 ppl=13.27                                                
Validation - loss=2.6368e+00 ppl=13.97 best_loss=2.7067e+00 best_ppl=14.98                                              
Epoch 20 - |param|=3.25e+02 |g_param|=3.37e+05 loss=2.5673e+00 ppl=13.03                                                
Validation - loss=2.5792e+00 ppl=13.19 best_loss=2.6368e+00 best_ppl=13.97                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.42e+05 loss=2.4618e+00 ppl=11.73                                                
Validation - loss=2.5218e+00 ppl=12.45 best_loss=2.5792e+00 best_ppl=13.19                                              
Epoch 22 - |param|=3.25e+02 |g_param|=3.40e+05 loss=2.4729e+00 ppl=11.86                                                
Validation - loss=2.4623e+00 ppl=11.73 best_loss=2.5218e+00 best_ppl=12.45                                              
Epoch 23 - |param|=3.25e+02 |g_param|=4.49e+05 loss=2.3744e+00 ppl=10.74                                                
Validation - loss=2.4154e+00 ppl=11.19 best_loss=2.4623e+00 best_ppl=11.73                                              
Epoch 24 - |param|=3.25e+02 |g_param|=3.91e+05 loss=2.3097e+00 ppl=10.07                                                
Validation - loss=2.3654e+00 ppl=10.65 best_loss=2.4154e+00 best_ppl=11.19                                              
Epoch 25 - |param|=3.25e+02 |g_param|=3.92e+05 loss=2.3192e+00 ppl=10.17                                                
Validation - loss=2.3166e+00 ppl=10.14 best_loss=2.3654e+00 best_ppl=10.65                                              
Epoch 26 - |param|=3.25e+02 |g_param|=3.40e+05 loss=2.3110e+00 ppl=10.08                                                
Validation - loss=2.2738e+00 ppl=9.72 best_loss=2.3166e+00 best_ppl=10.14                                               
Epoch 27 - |param|=3.25e+02 |g_param|=3.67e+05 loss=2.2193e+00 ppl=9.20                                                 
Validation - loss=2.2210e+00 ppl=9.22 best_loss=2.2738e+00 best_ppl=9.72                                                
Epoch 28 - |param|=3.25e+02 |g_param|=3.58e+05 loss=2.1926e+00 ppl=8.96                                                 
Validation - loss=2.1753e+00 ppl=8.80 best_loss=2.2210e+00 best_ppl=9.22                                                
Epoch 29 - |param|=3.25e+02 |g_param|=5.38e+05 loss=2.1158e+00 ppl=8.30                                                 
Validation - loss=2.1502e+00 ppl=8.59 best_loss=2.1753e+00 best_ppl=8.80                                                
Epoch 30 - |param|=3.25e+02 |g_param|=4.29e+05 loss=2.1298e+00 ppl=8.41                                                 
Validation - loss=2.0943e+00 ppl=8.12 best_loss=2.1502e+00 best_ppl=8.59                                                
Epoch 31 - |param|=3.25e+02 |g_param|=4.32e+05 loss=2.1364e+00 ppl=8.47                                                 
Validation - loss=2.0582e+00 ppl=7.83 best_loss=2.0943e+00 best_ppl=8.12                                                
Epoch 32 - |param|=3.25e+02 |g_param|=4.09e+05 loss=2.0501e+00 ppl=7.77                                                 
Validation - loss=2.0138e+00 ppl=7.49 best_loss=2.0582e+00 best_ppl=7.83                                                
Epoch 33 - |param|=3.25e+02 |g_param|=4.66e+05 loss=2.1310e+00 ppl=8.42                                                 
Validation - loss=1.9940e+00 ppl=7.34 best_loss=2.0138e+00 best_ppl=7.49                                                
Epoch 34 - |param|=3.25e+02 |g_param|=3.70e+05 loss=2.0470e+00 ppl=7.74                                                 
Validation - loss=1.9368e+00 ppl=6.94 best_loss=1.9940e+00 best_ppl=7.34                                                
Epoch 35 - |param|=3.25e+02 |g_param|=4.78e+05 loss=1.9732e+00 ppl=7.19                                                 
Validation - loss=1.9030e+00 ppl=6.71 best_loss=1.9368e+00 best_ppl=6.94                                                
Epoch 36 - |param|=3.26e+02 |g_param|=3.92e+05 loss=1.9387e+00 ppl=6.95                                                 
Validation - loss=1.8661e+00 ppl=6.46 best_loss=1.9030e+00 best_ppl=6.71                                                
Epoch 37 - |param|=3.26e+02 |g_param|=4.23e+05 loss=1.9759e+00 ppl=7.21                                                 
Validation - loss=1.8290e+00 ppl=6.23 best_loss=1.8661e+00 best_ppl=6.46                                                
Epoch 38 - |param|=3.26e+02 |g_param|=4.49e+05 loss=1.9096e+00 ppl=6.75                                                 
Validation - loss=1.7944e+00 ppl=6.02 best_loss=1.8290e+00 best_ppl=6.23                                                
Epoch 39 - |param|=3.26e+02 |g_param|=4.77e+05 loss=1.8571e+00 ppl=6.41                                                 
Validation - loss=1.7704e+00 ppl=5.87 best_loss=1.7944e+00 best_ppl=6.02                                                
Epoch 40 - |param|=3.26e+02 |g_param|=4.61e+05 loss=1.8372e+00 ppl=6.28                                                 
Validation - loss=1.7375e+00 ppl=5.68 best_loss=1.7704e+00 best_ppl=5.87                                                

real	20m35.329s
user	20m30.709s
sys	0m4.528s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.80-329.28.5.80-330.87.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 41.0/0.1/0.0/0.0 (BP=0.117, ratio=0.318, hyp_len=7357, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.5.01-149.80.5.03-153.40.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 53.1/0.4/0.0/0.0 (BP=0.068, ratio=0.271, hyp_len=6287, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.51-91.07.4.61-100.64.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 39.7/1.3/0.0/0.0 (BP=0.249, ratio=0.418, hyp_len=9684, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.22-68.30.4.34-76.62.pth
BLEU = 0.88, 25.3/4.1/0.3/0.0 (BP=0.886, ratio=0.892, hyp_len=20667, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.4.05-57.18.4.13-61.97.pth
BLEU = 2.44, 27.6/7.2/1.1/0.2 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.87-47.84.3.94-51.33.pth
BLEU = 3.17, 25.6/8.1/1.5/0.3 (BP=1.000, ratio=1.261, hyp_len=29211, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.67-39.31.3.78-43.62.pth
BLEU = 3.73, 26.8/8.9/1.9/0.4 (BP=1.000, ratio=1.264, hyp_len=29267, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.50-33.23.3.62-37.32.pth
BLEU = 4.91, 29.9/10.9/2.7/0.7 (BP=1.000, ratio=1.198, hyp_len=27752, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.36-28.93.3.48-32.59.pth
BLEU = 5.95, 32.1/12.4/3.5/0.9 (BP=1.000, ratio=1.170, hyp_len=27098, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.23-25.24.3.37-28.96.pth
BLEU = 7.52, 36.6/14.6/4.6/1.3 (BP=1.000, ratio=1.063, hyp_len=24611, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.19-24.39.3.25-25.91.pth
BLEU = 7.76, 35.0/14.4/4.8/1.5 (BP=1.000, ratio=1.178, hyp_len=27279, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.07-21.49.3.16-23.52.pth
BLEU = 9.84, 40.7/17.5/6.3/2.1 (BP=1.000, ratio=1.039, hyp_len=24069, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.2.97-19.52.3.07-21.61.pth
BLEU = 9.42, 37.8/16.4/6.1/2.1 (BP=1.000, ratio=1.179, hyp_len=27295, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.89-17.92.2.99-19.85.pth
BLEU = 11.41, 41.8/18.9/7.6/2.8 (BP=1.000, ratio=1.089, hyp_len=25227, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.87-17.72.2.91-18.28.pth
BLEU = 12.02, 42.3/19.4/8.1/3.1 (BP=1.000, ratio=1.115, hyp_len=25824, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.79-16.27.2.83-16.95.pth
BLEU = 12.55, 41.6/19.7/8.6/3.5 (BP=1.000, ratio=1.163, hyp_len=26936, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.78-16.04.2.77-15.89.pth
BLEU = 12.79, 42.2/20.0/8.8/3.6 (BP=1.000, ratio=1.180, hyp_len=27336, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.65-14.13.2.71-14.98.pth
BLEU = 13.32, 42.3/20.6/9.3/3.9 (BP=1.000, ratio=1.200, hyp_len=27784, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.59-13.27.2.64-13.97.pth
BLEU = 15.45, 45.8/22.9/11.0/5.0 (BP=1.000, ratio=1.138, hyp_len=26354, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.57-13.03.2.58-13.19.pth
BLEU = 16.64, 48.4/24.5/11.9/5.4 (BP=1.000, ratio=1.088, hyp_len=25207, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.46-11.73.2.52-12.45.pth
BLEU = 18.43, 50.6/26.4/13.3/6.5 (BP=1.000, ratio=1.057, hyp_len=24488, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.47-11.86.2.46-11.73.pth
BLEU = 17.95, 49.0/25.7/13.1/6.3 (BP=1.000, ratio=1.115, hyp_len=25814, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.37-10.74.2.42-11.19.pth
BLEU = 19.73, 52.3/28.0/14.4/7.2 (BP=1.000, ratio=1.059, hyp_len=24537, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.31-10.07.2.37-10.65.pth
BLEU = 19.10, 49.9/26.8/14.1/7.1 (BP=1.000, ratio=1.139, hyp_len=26384, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.32-10.17.2.32-10.14.pth
BLEU = 22.09, 54.8/30.5/16.6/8.6 (BP=1.000, ratio=1.047, hyp_len=24250, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.31-10.08.2.27-9.72.pth
BLEU = 19.97, 49.4/27.4/15.0/7.8 (BP=1.000, ratio=1.190, hyp_len=27570, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.22-9.20.2.22-9.22.pth
BLEU = 23.01, 54.8/31.3/17.4/9.4 (BP=1.000, ratio=1.085, hyp_len=25129, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.19-8.96.2.18-8.80.pth
BLEU = 25.44, 57.7/33.7/19.5/11.1 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.12-8.30.2.15-8.59.pth
BLEU = 24.85, 56.3/33.1/19.1/10.7 (BP=1.000, ratio=1.079, hyp_len=24989, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.13-8.41.2.09-8.12.pth
BLEU = 26.57, 58.3/34.9/20.6/11.9 (BP=1.000, ratio=1.060, hyp_len=24561, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.14-8.47.2.06-7.83.pth
BLEU = 28.20, 60.1/36.7/22.1/13.0 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.05-7.77.2.01-7.49.pth
BLEU = 28.14, 59.3/36.5/22.1/13.1 (BP=1.000, ratio=1.072, hyp_len=24830, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.13-8.42.1.99-7.34.pth
BLEU = 28.41, 59.3/36.9/22.4/13.3 (BP=1.000, ratio=1.083, hyp_len=25071, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.2.05-7.74.1.94-6.94.pth
BLEU = 30.73, 61.8/38.8/24.4/15.3 (BP=1.000, ratio=1.044, hyp_len=24170, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.1.97-7.19.1.90-6.71.pth
BLEU = 32.34, 63.5/40.7/25.8/16.4 (BP=1.000, ratio=1.026, hyp_len=23759, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.94-6.95.1.87-6.46.pth
BLEU = 33.20, 64.3/41.4/26.6/17.1 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.1.98-7.21.1.83-6.23.pth
BLEU = 33.52, 63.8/41.7/27.0/17.5 (BP=1.000, ratio=1.044, hyp_len=24183, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.91-6.75.1.79-6.02.pth
BLEU = 34.71, 65.0/42.7/28.2/18.6 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth
BLEU = 35.33, 65.7/43.6/28.8/18.9 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.84-6.28.1.74-5.68.pth
BLEU = 34.20, 63.7/42.3/27.9/18.2 (BP=1.000, ratio=1.078, hyp_len=24955, ref_len=23160)

real	25m12.792s
user	24m48.889s
sys	0m51.134s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-40epoch$
```

transformer, 40 epoch, my-rk မော်ဒယ်ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth
BLEU = 35.33, 65.7/43.6/28.8/18.9 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
```

### Transformer, my-rk, 50 epoch

50 epoch training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 50 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-50epoch/myrk-transformer-model.pth
...
...
...
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.66e+05 loss=5.7481e+00 ppl=313.58                                                
Validation - loss=5.7878e+00 ppl=326.29 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.39e+05 loss=4.9508e+00 ppl=141.28                                                
Validation - loss=5.0110e+00 ppl=150.06 best_loss=5.7878e+00 best_ppl=326.29                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.20e+05 loss=4.5394e+00 ppl=93.63                                                 
Validation - loss=4.6186e+00 ppl=101.35 best_loss=5.0110e+00 best_ppl=150.06                                            
Epoch 4 - |param|=3.24e+02 |g_param|=1.88e+05 loss=4.2541e+00 ppl=70.39                                                 
Validation - loss=4.3566e+00 ppl=77.99 best_loss=4.6186e+00 best_ppl=101.35                                             
Epoch 5 - |param|=3.24e+02 |g_param|=1.86e+05 loss=4.0322e+00 ppl=56.38                                                 
Validation - loss=4.1519e+00 ppl=63.55 best_loss=4.3566e+00 best_ppl=77.99                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.65e+05 loss=3.8793e+00 ppl=48.39                                                 
Validation - loss=3.9522e+00 ppl=52.05 best_loss=4.1519e+00 best_ppl=63.55                                              
Epoch 7 - |param|=3.24e+02 |g_param|=1.47e+05 loss=3.7065e+00 ppl=40.71                                                 
Validation - loss=3.7747e+00 ppl=43.59 best_loss=3.9522e+00 best_ppl=52.05                                              
Epoch 8 - |param|=3.24e+02 |g_param|=1.53e+05 loss=3.5419e+00 ppl=34.53                                                 
Validation - loss=3.6131e+00 ppl=37.08 best_loss=3.7747e+00 best_ppl=43.59                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.98e+05 loss=3.3246e+00 ppl=27.79                                                 
Validation - loss=3.4778e+00 ppl=32.39 best_loss=3.6131e+00 best_ppl=37.08                                              
Epoch 10 - |param|=3.24e+02 |g_param|=2.36e+05 loss=3.2039e+00 ppl=24.63                                                
Validation - loss=3.3581e+00 ppl=28.73 best_loss=3.4778e+00 best_ppl=32.39                                              
Epoch 11 - |param|=3.24e+02 |g_param|=2.55e+05 loss=3.1589e+00 ppl=23.55                                                
Validation - loss=3.2500e+00 ppl=25.79 best_loss=3.3581e+00 best_ppl=28.73                                              
Epoch 12 - |param|=3.24e+02 |g_param|=2.92e+05 loss=3.0991e+00 ppl=22.18                                                
Validation - loss=3.1488e+00 ppl=23.31 best_loss=3.2500e+00 best_ppl=25.79                                              
Epoch 13 - |param|=3.25e+02 |g_param|=1.74e+05 loss=3.0126e+00 ppl=20.34                                                
Validation - loss=3.0580e+00 ppl=21.28 best_loss=3.1488e+00 best_ppl=23.31                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.36e+05 loss=2.8811e+00 ppl=17.83                                                
Validation - loss=2.9789e+00 ppl=19.67 best_loss=3.0580e+00 best_ppl=21.28                                              
Epoch 15 - |param|=3.25e+02 |g_param|=2.00e+05 loss=2.8524e+00 ppl=17.33                                                
Validation - loss=2.8947e+00 ppl=18.08 best_loss=2.9789e+00 best_ppl=19.67                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.21e+05 loss=2.8612e+00 ppl=17.48                                                
Validation - loss=2.8214e+00 ppl=16.80 best_loss=2.8947e+00 best_ppl=18.08                                              
Epoch 17 - |param|=3.25e+02 |g_param|=3.38e+05 loss=2.7665e+00 ppl=15.90                                                
Validation - loss=2.7534e+00 ppl=15.70 best_loss=2.8214e+00 best_ppl=16.80                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.50e+05 loss=2.6743e+00 ppl=14.50                                                
Validation - loss=2.6869e+00 ppl=14.69 best_loss=2.7534e+00 best_ppl=15.70                                              
Epoch 19 - |param|=3.25e+02 |g_param|=2.47e+05 loss=2.5837e+00 ppl=13.25                                                
Validation - loss=2.6319e+00 ppl=13.90 best_loss=2.6869e+00 best_ppl=14.69                                              
Epoch 20 - |param|=3.25e+02 |g_param|=3.27e+05 loss=2.5194e+00 ppl=12.42                                                
Validation - loss=2.5805e+00 ppl=13.20 best_loss=2.6319e+00 best_ppl=13.90                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.56e+05 loss=2.5200e+00 ppl=12.43                                                
Validation - loss=2.5164e+00 ppl=12.38 best_loss=2.5805e+00 best_ppl=13.20                                              
Epoch 22 - |param|=3.25e+02 |g_param|=2.69e+05 loss=2.4796e+00 ppl=11.94                                                
Validation - loss=2.4657e+00 ppl=11.77 best_loss=2.5164e+00 best_ppl=12.38                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.68e+05 loss=2.4444e+00 ppl=11.52                                                
Validation - loss=2.4192e+00 ppl=11.24 best_loss=2.4657e+00 best_ppl=11.77                                              
Epoch 24 - |param|=3.25e+02 |g_param|=4.04e+05 loss=2.3757e+00 ppl=10.76                                                
Validation - loss=2.3702e+00 ppl=10.70 best_loss=2.4192e+00 best_ppl=11.24                                              
Epoch 25 - |param|=3.25e+02 |g_param|=3.12e+05 loss=2.3304e+00 ppl=10.28                                                
Validation - loss=2.3180e+00 ppl=10.15 best_loss=2.3702e+00 best_ppl=10.70                                              
Epoch 26 - |param|=3.25e+02 |g_param|=3.15e+05 loss=2.3111e+00 ppl=10.09                                                
Validation - loss=2.2735e+00 ppl=9.71 best_loss=2.3180e+00 best_ppl=10.15                                               
Epoch 27 - |param|=3.25e+02 |g_param|=3.27e+05 loss=2.2318e+00 ppl=9.32                                                 
Validation - loss=2.2187e+00 ppl=9.20 best_loss=2.2735e+00 best_ppl=9.71                                                
Epoch 28 - |param|=3.25e+02 |g_param|=4.75e+05 loss=2.2285e+00 ppl=9.29                                                 
Validation - loss=2.1776e+00 ppl=8.82 best_loss=2.2187e+00 best_ppl=9.20                                                
Epoch 29 - |param|=3.25e+02 |g_param|=4.08e+05 loss=2.2109e+00 ppl=9.12                                                 
Validation - loss=2.1426e+00 ppl=8.52 best_loss=2.1776e+00 best_ppl=8.82                                                
Epoch 30 - |param|=3.25e+02 |g_param|=5.01e+05 loss=2.0931e+00 ppl=8.11                                                 
Validation - loss=2.1051e+00 ppl=8.21 best_loss=2.1426e+00 best_ppl=8.52                                                
Epoch 31 - |param|=3.25e+02 |g_param|=4.56e+05 loss=2.1551e+00 ppl=8.63                                                 
Validation - loss=2.0613e+00 ppl=7.86 best_loss=2.1051e+00 best_ppl=8.21                                                
Epoch 32 - |param|=3.26e+02 |g_param|=3.95e+05 loss=2.0608e+00 ppl=7.85                                                 
Validation - loss=2.0174e+00 ppl=7.52 best_loss=2.0613e+00 best_ppl=7.86                                                
Epoch 33 - |param|=3.26e+02 |g_param|=4.12e+05 loss=2.0995e+00 ppl=8.16                                                 
Validation - loss=1.9876e+00 ppl=7.30 best_loss=2.0174e+00 best_ppl=7.52                                                
Epoch 34 - |param|=3.26e+02 |g_param|=3.82e+05 loss=2.0178e+00 ppl=7.52                                                 
Validation - loss=1.9549e+00 ppl=7.06 best_loss=1.9876e+00 best_ppl=7.30                                                
Epoch 35 - |param|=3.26e+02 |g_param|=4.83e+05 loss=1.9682e+00 ppl=7.16                                                 
Validation - loss=1.9091e+00 ppl=6.75 best_loss=1.9549e+00 best_ppl=7.06                                                
Epoch 36 - |param|=3.26e+02 |g_param|=4.60e+05 loss=1.9662e+00 ppl=7.14                                                 
Validation - loss=1.8677e+00 ppl=6.47 best_loss=1.9091e+00 best_ppl=6.75                                                
Epoch 37 - |param|=3.26e+02 |g_param|=4.97e+05 loss=1.8997e+00 ppl=6.68                                                 
Validation - loss=1.8494e+00 ppl=6.36 best_loss=1.8677e+00 best_ppl=6.47                                                
Epoch 38 - |param|=3.26e+02 |g_param|=4.17e+05 loss=1.8617e+00 ppl=6.43                                                 
Validation - loss=1.8121e+00 ppl=6.12 best_loss=1.8494e+00 best_ppl=6.36                                                
Epoch 39 - |param|=3.26e+02 |g_param|=5.19e+05 loss=1.8814e+00 ppl=6.56                                                 
Validation - loss=1.7688e+00 ppl=5.86 best_loss=1.8121e+00 best_ppl=6.12                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.93e+05 loss=1.7923e+00 ppl=6.00                                                 
Validation - loss=1.7610e+00 ppl=5.82 best_loss=1.7688e+00 best_ppl=5.86                                                
Epoch 41 - |param|=3.26e+02 |g_param|=5.35e+05 loss=1.8366e+00 ppl=6.28                                                 
Validation - loss=1.7282e+00 ppl=5.63 best_loss=1.7610e+00 best_ppl=5.82                                                
Epoch 42 - |param|=3.26e+02 |g_param|=5.35e+05 loss=1.8129e+00 ppl=6.13                                                 
Validation - loss=1.6877e+00 ppl=5.41 best_loss=1.7282e+00 best_ppl=5.63                                                
Epoch 43 - |param|=3.26e+02 |g_param|=4.42e+05 loss=1.7662e+00 ppl=5.85                                                 
Validation - loss=1.6820e+00 ppl=5.38 best_loss=1.6877e+00 best_ppl=5.41                                                
Epoch 44 - |param|=3.26e+02 |g_param|=5.47e+05 loss=1.7116e+00 ppl=5.54                                                 
Validation - loss=1.6344e+00 ppl=5.13 best_loss=1.6820e+00 best_ppl=5.38                                                
Epoch 45 - |param|=3.26e+02 |g_param|=3.71e+05 loss=1.7632e+00 ppl=5.83                                                 
Validation - loss=1.6403e+00 ppl=5.16 best_loss=1.6344e+00 best_ppl=5.13                                                
Epoch 46 - |param|=3.26e+02 |g_param|=7.08e+05 loss=1.7003e+00 ppl=5.48                                                 
Validation - loss=1.5870e+00 ppl=4.89 best_loss=1.6344e+00 best_ppl=5.13                                                
Epoch 47 - |param|=3.26e+02 |g_param|=3.05e+05 loss=1.6987e+00 ppl=5.47                                                 
Validation - loss=1.5638e+00 ppl=4.78 best_loss=1.5870e+00 best_ppl=4.89                                                
Epoch 48 - |param|=3.26e+02 |g_param|=2.11e+05 loss=1.6584e+00 ppl=5.25                                                 
Validation - loss=1.5422e+00 ppl=4.67 best_loss=1.5638e+00 best_ppl=4.78                                                
Epoch 49 - |param|=3.26e+02 |g_param|=2.55e+05 loss=1.6570e+00 ppl=5.24                                                 
Validation - loss=1.5227e+00 ppl=4.58 best_loss=1.5422e+00 best_ppl=4.67                                                
Epoch 50 - |param|=3.26e+02 |g_param|=2.60e+05 loss=1.6442e+00 ppl=5.18                                                 
Validation - loss=1.5341e+00 ppl=4.64 best_loss=1.5227e+00 best_ppl=4.58                                                

real	25m34.628s
user	25m29.562s
sys	0m5.005s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.75-313.58.5.79-326.29.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 35.9/0.0/0.0/0.0 (BP=0.038, ratio=0.234, hyp_len=5429, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.4.95-141.28.5.01-150.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 68.9/8.6/0.0/0.0 (BP=0.005, ratio=0.158, hyp_len=3656, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.54-93.63.4.62-101.35.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 44.7/4.5/0.9/0.0 (BP=0.086, ratio=0.290, hyp_len=6717, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.25-70.39.4.36-77.99.pth
BLEU = 0.68, 40.8/10.4/1.2/0.0 (BP=0.419, ratio=0.535, hyp_len=12381, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.4.03-56.38.4.15-63.55.pth
BLEU = 1.54, 33.0/9.9/1.4/0.0 (BP=0.812, ratio=0.828, hyp_len=19177, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.88-48.39.3.95-52.05.pth
BLEU = 3.13, 28.5/9.0/1.5/0.2 (BP=1.000, ratio=1.073, hyp_len=24852, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.71-40.71.3.77-43.59.pth
BLEU = 3.49, 24.7/8.3/1.9/0.4 (BP=1.000, ratio=1.344, hyp_len=31133, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.54-34.53.3.61-37.08.pth
BLEU = 3.15, 20.1/7.0/1.8/0.4 (BP=1.000, ratio=1.749, hyp_len=40510, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.32-27.79.3.48-32.39.pth
BLEU = 3.30, 18.3/6.7/1.9/0.5 (BP=1.000, ratio=2.060, hyp_len=47709, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.20-24.63.3.36-28.73.pth
BLEU = 4.96, 24.9/9.6/3.0/0.9 (BP=1.000, ratio=1.581, hyp_len=36623, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.16-23.55.3.25-25.79.pth
BLEU = 6.25, 28.9/11.6/3.9/1.2 (BP=1.000, ratio=1.427, hyp_len=33056, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.10-22.18.3.15-23.31.pth
BLEU = 7.92, 33.3/13.9/5.1/1.7 (BP=1.000, ratio=1.285, hyp_len=29765, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.3.01-20.34.3.06-21.28.pth
BLEU = 8.23, 33.0/14.1/5.3/1.9 (BP=1.000, ratio=1.330, hyp_len=30794, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.88-17.83.2.98-19.67.pth
BLEU = 8.98, 34.9/15.3/5.9/2.1 (BP=1.000, ratio=1.291, hyp_len=29888, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.85-17.33.2.89-18.08.pth
BLEU = 10.41, 37.3/16.9/7.0/2.7 (BP=1.000, ratio=1.256, hyp_len=29088, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.86-17.48.2.82-16.80.pth
BLEU = 11.03, 37.9/17.6/7.4/3.0 (BP=1.000, ratio=1.267, hyp_len=29353, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.77-15.90.2.75-15.70.pth
BLEU = 13.49, 43.9/21.1/9.3/3.8 (BP=1.000, ratio=1.109, hyp_len=25696, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.67-14.50.2.69-14.69.pth
BLEU = 13.69, 43.1/21.1/9.5/4.0 (BP=1.000, ratio=1.160, hyp_len=26864, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.58-13.25.2.63-13.90.pth
BLEU = 15.96, 47.4/23.8/11.3/5.1 (BP=1.000, ratio=1.076, hyp_len=24925, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.52-12.42.2.58-13.20.pth
BLEU = 13.60, 40.3/20.1/9.6/4.4 (BP=1.000, ratio=1.295, hyp_len=29999, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.52-12.43.2.52-12.38.pth
BLEU = 17.03, 48.3/24.9/12.2/5.7 (BP=1.000, ratio=1.093, hyp_len=25311, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.48-11.94.2.47-11.77.pth
BLEU = 18.01, 49.1/25.9/13.0/6.4 (BP=1.000, ratio=1.096, hyp_len=25394, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.44-11.52.2.42-11.24.pth
BLEU = 18.48, 49.0/26.1/13.5/6.8 (BP=1.000, ratio=1.117, hyp_len=25879, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.38-10.76.2.37-10.70.pth
BLEU = 19.31, 49.9/27.0/14.2/7.2 (BP=1.000, ratio=1.116, hyp_len=25856, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.33-10.28.2.32-10.15.pth
BLEU = 21.17, 53.2/29.4/15.7/8.2 (BP=1.000, ratio=1.057, hyp_len=24483, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.31-10.09.2.27-9.71.pth
BLEU = 22.61, 54.9/30.9/17.0/9.1 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.23-9.32.2.22-9.20.pth
BLEU = 23.01, 55.1/31.4/17.4/9.4 (BP=1.000, ratio=1.057, hyp_len=24474, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.23-9.29.2.18-8.82.pth
BLEU = 22.64, 53.2/30.5/17.2/9.4 (BP=1.000, ratio=1.107, hyp_len=25640, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.21-9.12.2.14-8.52.pth
BLEU = 23.54, 54.2/31.6/18.0/10.0 (BP=1.000, ratio=1.102, hyp_len=25524, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.09-8.11.2.11-8.21.pth
BLEU = 25.24, 56.1/33.4/19.5/11.2 (BP=1.000, ratio=1.085, hyp_len=25118, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.16-8.63.2.06-7.86.pth
BLEU = 26.36, 57.2/34.5/20.5/12.0 (BP=1.000, ratio=1.081, hyp_len=25039, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.06-7.85.2.02-7.52.pth
BLEU = 27.00, 57.7/35.0/21.0/12.5 (BP=1.000, ratio=1.081, hyp_len=25044, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.10-8.16.1.99-7.30.pth
BLEU = 27.67, 58.4/35.9/21.7/12.9 (BP=1.000, ratio=1.091, hyp_len=25274, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.2.02-7.52.1.95-7.06.pth
BLEU = 28.28, 58.8/36.5/22.3/13.4 (BP=1.000, ratio=1.092, hyp_len=25298, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.1.97-7.16.1.91-6.75.pth
BLEU = 32.07, 63.4/40.3/25.5/16.2 (BP=1.000, ratio=1.015, hyp_len=23517, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.97-7.14.1.87-6.47.pth
BLEU = 31.79, 61.9/39.7/25.5/16.3 (BP=1.000, ratio=1.064, hyp_len=24644, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.1.90-6.68.1.85-6.36.pth
BLEU = 31.63, 61.2/39.5/25.4/16.3 (BP=1.000, ratio=1.092, hyp_len=25282, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.86-6.43.1.81-6.12.pth
BLEU = 33.42, 63.7/41.6/27.0/17.4 (BP=1.000, ratio=1.051, hyp_len=24345, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.88-6.56.1.77-5.86.pth
BLEU = 35.56, 66.0/43.7/29.0/19.1 (BP=1.000, ratio=1.022, hyp_len=23677, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.79-6.00.1.76-5.82.pth
BLEU = 34.15, 63.7/42.1/27.8/18.2 (BP=1.000, ratio=1.069, hyp_len=24758, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.41.1.84-6.28.1.73-5.63.pth
BLEU = 33.85, 62.9/41.7/27.6/18.1 (BP=1.000, ratio=1.093, hyp_len=25303, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.42.1.81-6.13.1.69-5.41.pth
BLEU = 38.05, 68.1/46.2/31.4/21.2 (BP=1.000, ratio=1.011, hyp_len=23411, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.43.1.77-5.85.1.68-5.38.pth
BLEU = 35.77, 64.7/43.8/29.5/19.6 (BP=1.000, ratio=1.079, hyp_len=24990, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.44.1.71-5.54.1.63-5.13.pth
BLEU = 37.91, 67.1/46.0/31.4/21.3 (BP=1.000, ratio=1.045, hyp_len=24211, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.45.1.76-5.83.1.64-5.16.pth
BLEU = 36.48, 64.8/44.5/30.3/20.3 (BP=1.000, ratio=1.096, hyp_len=25373, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.46.1.70-5.48.1.59-4.89.pth
BLEU = 39.19, 68.0/47.2/32.7/22.5 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth
BLEU = 40.85, 69.4/48.7/34.3/24.0 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.48.1.66-5.25.1.54-4.67.pth
BLEU = 39.33, 67.1/47.1/33.0/22.9 (BP=1.000, ratio=1.075, hyp_len=24889, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.49.1.66-5.24.1.52-4.58.pth
BLEU = 40.76, 68.7/48.7/34.4/24.0 (BP=1.000, ratio=1.050, hyp_len=24326, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.50.1.64-5.18.1.53-4.64.pth
BLEU = 40.22, 68.2/48.2/34.0/23.4 (BP=1.000, ratio=1.066, hyp_len=24694, ref_len=23160)

real	33m20.305s
user	32m49.311s
sys	1m3.886s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-50epoch$
```

transformer, 50 epoch, my-rk မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်...  

```
Evaluation result for the model: myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth
BLEU = 40.85, 69.4/48.7/34.3/24.0 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
```

### Transformer, my-rk, 60 epoch

tranining ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 60 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-60epoch/myrk-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/myrk-60epoch/myrk-transformer-model.pth',
    'n_epochs': 60,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.70e+05 loss=5.7851e+00 ppl=325.41                                                
Validation - loss=5.7877e+00 ppl=326.26 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.59e+05 loss=4.9802e+00 ppl=145.51                                                
Validation - loss=4.9999e+00 ppl=148.39 best_loss=5.7877e+00 best_ppl=326.26                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.74e+05 loss=4.4828e+00 ppl=88.48                                                 
Validation - loss=4.5946e+00 ppl=98.95 best_loss=4.9999e+00 best_ppl=148.39                                             
Epoch 4 - |param|=3.25e+02 |g_param|=2.20e+05 loss=4.2260e+00 ppl=68.45                                                 
Validation - loss=4.3225e+00 ppl=75.37 best_loss=4.5946e+00 best_ppl=98.95                                              
Epoch 5 - |param|=3.25e+02 |g_param|=2.04e+05 loss=4.0239e+00 ppl=55.92                                                 
Validation - loss=4.1080e+00 ppl=60.82 best_loss=4.3225e+00 best_ppl=75.37                                              
Epoch 6 - |param|=3.25e+02 |g_param|=1.56e+05 loss=3.7863e+00 ppl=44.09                                                 
Validation - loss=3.9192e+00 ppl=50.36 best_loss=4.1080e+00 best_ppl=60.82                                              
Epoch 7 - |param|=3.25e+02 |g_param|=1.45e+05 loss=3.6585e+00 ppl=38.80                                                 
Validation - loss=3.7523e+00 ppl=42.62 best_loss=3.9192e+00 best_ppl=50.36                                              
Epoch 8 - |param|=3.25e+02 |g_param|=1.52e+05 loss=3.5189e+00 ppl=33.75                                                 
Validation - loss=3.6010e+00 ppl=36.64 best_loss=3.7523e+00 best_ppl=42.62                                              
Epoch 9 - |param|=3.25e+02 |g_param|=2.06e+05 loss=3.2690e+00 ppl=26.28                                                 
Validation - loss=3.4736e+00 ppl=32.25 best_loss=3.6010e+00 best_ppl=36.64                                              
Epoch 10 - |param|=3.25e+02 |g_param|=2.40e+05 loss=3.2975e+00 ppl=27.04                                                
Validation - loss=3.3549e+00 ppl=28.64 best_loss=3.4736e+00 best_ppl=32.25                                              
Epoch 11 - |param|=3.25e+02 |g_param|=2.22e+05 loss=3.1937e+00 ppl=24.38                                                
Validation - loss=3.2417e+00 ppl=25.58 best_loss=3.3549e+00 best_ppl=28.64                                              
Epoch 12 - |param|=3.25e+02 |g_param|=2.18e+05 loss=3.0398e+00 ppl=20.90                                                
Validation - loss=3.1473e+00 ppl=23.27 best_loss=3.2417e+00 best_ppl=25.58                                              
Epoch 13 - |param|=3.25e+02 |g_param|=3.15e+05 loss=2.9703e+00 ppl=19.50                                                
Validation - loss=3.0576e+00 ppl=21.28 best_loss=3.1473e+00 best_ppl=23.27                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.54e+05 loss=2.8980e+00 ppl=18.14                                                
Validation - loss=2.9807e+00 ppl=19.70 best_loss=3.0576e+00 best_ppl=21.28                                              
Epoch 15 - |param|=3.25e+02 |g_param|=1.99e+05 loss=2.8538e+00 ppl=17.35                                                
Validation - loss=2.8931e+00 ppl=18.05 best_loss=2.9807e+00 best_ppl=19.70                                              
Epoch 16 - |param|=3.25e+02 |g_param|=2.81e+05 loss=2.7740e+00 ppl=16.02                                                
Validation - loss=2.8223e+00 ppl=16.82 best_loss=2.8931e+00 best_ppl=18.05                                              
Epoch 17 - |param|=3.25e+02 |g_param|=3.19e+05 loss=2.7422e+00 ppl=15.52                                                
Validation - loss=2.7550e+00 ppl=15.72 best_loss=2.8223e+00 best_ppl=16.82                                              
Epoch 18 - |param|=3.25e+02 |g_param|=2.68e+05 loss=2.6841e+00 ppl=14.65                                                
Validation - loss=2.6892e+00 ppl=14.72 best_loss=2.7550e+00 best_ppl=15.72                                              
Epoch 19 - |param|=3.25e+02 |g_param|=3.26e+05 loss=2.6523e+00 ppl=14.19                                                
Validation - loss=2.6292e+00 ppl=13.86 best_loss=2.6892e+00 best_ppl=14.72                                              
Epoch 20 - |param|=3.26e+02 |g_param|=3.79e+05 loss=2.5928e+00 ppl=13.37                                                
Validation - loss=2.5649e+00 ppl=13.00 best_loss=2.6292e+00 best_ppl=13.86                                              
Epoch 21 - |param|=3.26e+02 |g_param|=3.77e+05 loss=2.5717e+00 ppl=13.09                                                
Validation - loss=2.5217e+00 ppl=12.45 best_loss=2.5649e+00 best_ppl=13.00                                              
Epoch 22 - |param|=3.26e+02 |g_param|=4.41e+05 loss=2.5121e+00 ppl=12.33                                                
Validation - loss=2.4686e+00 ppl=11.81 best_loss=2.5217e+00 best_ppl=12.45                                              
Epoch 23 - |param|=3.26e+02 |g_param|=3.48e+05 loss=2.4633e+00 ppl=11.74                                                
Validation - loss=2.4092e+00 ppl=11.12 best_loss=2.4686e+00 best_ppl=11.81                                              
Epoch 24 - |param|=3.26e+02 |g_param|=3.71e+05 loss=2.3526e+00 ppl=10.51                                                
Validation - loss=2.3577e+00 ppl=10.57 best_loss=2.4092e+00 best_ppl=11.12                                              
Epoch 25 - |param|=3.26e+02 |g_param|=4.50e+05 loss=2.2474e+00 ppl=9.46                                                 
Validation - loss=2.3154e+00 ppl=10.13 best_loss=2.3577e+00 best_ppl=10.57                                              
Epoch 26 - |param|=3.26e+02 |g_param|=2.78e+05 loss=2.2690e+00 ppl=9.67                                                 
Validation - loss=2.2643e+00 ppl=9.62 best_loss=2.3154e+00 best_ppl=10.13                                               
Epoch 27 - |param|=3.26e+02 |g_param|=3.91e+05 loss=2.2219e+00 ppl=9.22                                                 
Validation - loss=2.2137e+00 ppl=9.15 best_loss=2.2643e+00 best_ppl=9.62                                                
Epoch 28 - |param|=3.26e+02 |g_param|=3.91e+05 loss=2.2834e+00 ppl=9.81                                                 
Validation - loss=2.1664e+00 ppl=8.73 best_loss=2.2137e+00 best_ppl=9.15                                                
Epoch 29 - |param|=3.26e+02 |g_param|=4.95e+05 loss=2.2179e+00 ppl=9.19                                                 
Validation - loss=2.1413e+00 ppl=8.51 best_loss=2.1664e+00 best_ppl=8.73                                                
Epoch 30 - |param|=3.26e+02 |g_param|=4.21e+05 loss=2.1721e+00 ppl=8.78                                                 
Validation - loss=2.0965e+00 ppl=8.14 best_loss=2.1413e+00 best_ppl=8.51                                                
Epoch 31 - |param|=3.26e+02 |g_param|=3.26e+05 loss=2.0366e+00 ppl=7.66                                                 
Validation - loss=2.0563e+00 ppl=7.82 best_loss=2.0965e+00 best_ppl=8.14                                                
Epoch 32 - |param|=3.26e+02 |g_param|=4.60e+05 loss=2.1276e+00 ppl=8.39                                                 
Validation - loss=2.0157e+00 ppl=7.51 best_loss=2.0563e+00 best_ppl=7.82                                                
Epoch 33 - |param|=3.26e+02 |g_param|=4.39e+05 loss=2.0700e+00 ppl=7.92                                                 
Validation - loss=1.9659e+00 ppl=7.14 best_loss=2.0157e+00 best_ppl=7.51                                                
Epoch 34 - |param|=3.26e+02 |g_param|=4.31e+05 loss=2.0479e+00 ppl=7.75                                                 
Validation - loss=1.9245e+00 ppl=6.85 best_loss=1.9659e+00 best_ppl=7.14                                                
Epoch 35 - |param|=3.26e+02 |g_param|=5.88e+05 loss=2.0383e+00 ppl=7.68                                                 
Validation - loss=1.8859e+00 ppl=6.59 best_loss=1.9245e+00 best_ppl=6.85                                                
Epoch 36 - |param|=3.26e+02 |g_param|=3.57e+05 loss=1.9411e+00 ppl=6.97                                                 
Validation - loss=1.8516e+00 ppl=6.37 best_loss=1.8859e+00 best_ppl=6.59                                                
Epoch 37 - |param|=3.26e+02 |g_param|=3.67e+05 loss=1.9674e+00 ppl=7.15                                                 
Validation - loss=1.8182e+00 ppl=6.16 best_loss=1.8516e+00 best_ppl=6.37                                                
Epoch 38 - |param|=3.26e+02 |g_param|=4.51e+05 loss=1.9105e+00 ppl=6.76                                                 
Validation - loss=1.8079e+00 ppl=6.10 best_loss=1.8182e+00 best_ppl=6.16                                                
Epoch 39 - |param|=3.26e+02 |g_param|=6.56e+05 loss=1.8886e+00 ppl=6.61                                                 
Validation - loss=1.7762e+00 ppl=5.91 best_loss=1.8079e+00 best_ppl=6.10                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.05e+05 loss=1.8911e+00 ppl=6.63                                                 
Validation - loss=1.7397e+00 ppl=5.70 best_loss=1.7762e+00 best_ppl=5.91                                                
Epoch 41 - |param|=3.26e+02 |g_param|=7.59e+05 loss=1.8044e+00 ppl=6.08                                                 
Validation - loss=1.7338e+00 ppl=5.66 best_loss=1.7397e+00 best_ppl=5.70                                                
Epoch 42 - |param|=3.26e+02 |g_param|=5.42e+05 loss=1.7471e+00 ppl=5.74                                                 
Validation - loss=1.6784e+00 ppl=5.36 best_loss=1.7338e+00 best_ppl=5.66                                                
Epoch 43 - |param|=3.26e+02 |g_param|=4.31e+05 loss=1.7712e+00 ppl=5.88                                                 
Validation - loss=1.6432e+00 ppl=5.17 best_loss=1.6784e+00 best_ppl=5.36                                                
Epoch 44 - |param|=3.26e+02 |g_param|=6.08e+05 loss=1.8091e+00 ppl=6.10                                                 
Validation - loss=1.6611e+00 ppl=5.27 best_loss=1.6432e+00 best_ppl=5.17                                                
Epoch 45 - |param|=3.26e+02 |g_param|=5.79e+05 loss=1.7418e+00 ppl=5.71                                                 
Validation - loss=1.6234e+00 ppl=5.07 best_loss=1.6432e+00 best_ppl=5.17                                                
Epoch 46 - |param|=3.26e+02 |g_param|=5.38e+05 loss=1.6922e+00 ppl=5.43                                                 
Validation - loss=1.5678e+00 ppl=4.80 best_loss=1.6234e+00 best_ppl=5.07                                                
Epoch 47 - |param|=3.26e+02 |g_param|=5.30e+05 loss=1.6728e+00 ppl=5.33                                                 
Validation - loss=1.5454e+00 ppl=4.69 best_loss=1.5678e+00 best_ppl=4.80                                                
Epoch 48 - |param|=3.26e+02 |g_param|=4.66e+05 loss=1.6018e+00 ppl=4.96                                                 
Validation - loss=1.5317e+00 ppl=4.63 best_loss=1.5454e+00 best_ppl=4.69                                                
Epoch 49 - |param|=3.26e+02 |g_param|=4.13e+05 loss=1.6592e+00 ppl=5.26                                                 
Validation - loss=1.5000e+00 ppl=4.48 best_loss=1.5317e+00 best_ppl=4.63                                                
Epoch 50 - |param|=3.26e+02 |g_param|=8.56e+05 loss=1.6666e+00 ppl=5.29                                                 
Validation - loss=1.4814e+00 ppl=4.40 best_loss=1.5000e+00 best_ppl=4.48                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.71e+05 loss=1.6529e+00 ppl=5.22                                                 
Validation - loss=1.4562e+00 ppl=4.29 best_loss=1.4814e+00 best_ppl=4.40                                                
Epoch 52 - |param|=3.26e+02 |g_param|=6.80e+05 loss=1.5865e+00 ppl=4.89                                                 
Validation - loss=1.4726e+00 ppl=4.36 best_loss=1.4562e+00 best_ppl=4.29                                                
Epoch 53 - |param|=3.26e+02 |g_param|=4.58e+05 loss=1.5420e+00 ppl=4.67                                                 
Validation - loss=1.4241e+00 ppl=4.15 best_loss=1.4562e+00 best_ppl=4.29                                                
Epoch 54 - |param|=3.26e+02 |g_param|=5.48e+05 loss=1.5668e+00 ppl=4.79                                                 
Validation - loss=1.4058e+00 ppl=4.08 best_loss=1.4241e+00 best_ppl=4.15                                                
Epoch 55 - |param|=3.26e+02 |g_param|=4.88e+05 loss=1.4834e+00 ppl=4.41                                                 
Validation - loss=1.4109e+00 ppl=4.10 best_loss=1.4058e+00 best_ppl=4.08                                                
Epoch 56 - |param|=3.26e+02 |g_param|=6.03e+05 loss=1.5316e+00 ppl=4.63                                                 
Validation - loss=1.3858e+00 ppl=4.00 best_loss=1.4058e+00 best_ppl=4.08                                                
Epoch 57 - |param|=3.26e+02 |g_param|=8.95e+05 loss=1.4186e+00 ppl=4.13                                                 
Validation - loss=1.3713e+00 ppl=3.94 best_loss=1.3858e+00 best_ppl=4.00                                                
Epoch 58 - |param|=3.26e+02 |g_param|=7.54e+05 loss=1.4715e+00 ppl=4.36                                                 
Validation - loss=1.3860e+00 ppl=4.00 best_loss=1.3713e+00 best_ppl=3.94                                                
Epoch 59 - |param|=3.26e+02 |g_param|=4.94e+05 loss=1.4888e+00 ppl=4.43                                                 
Validation - loss=1.3295e+00 ppl=3.78 best_loss=1.3713e+00 best_ppl=3.94                                                
Epoch 60 - |param|=3.26e+02 |g_param|=6.26e+05 loss=1.4212e+00 ppl=4.14                                                 
Validation - loss=1.3369e+00 ppl=3.81 best_loss=1.3295e+00 best_ppl=3.78                                                

real	31m41.198s
user	31m31.876s
sys	0m6.171s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.79-325.41.5.79-326.26.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.1/1.5/0.0/0.0 (BP=1.000, ratio=1.268, hyp_len=29362, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.4.98-145.51.5.00-148.39.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.6/0.2/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=23464, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.48-88.48.4.59-98.95.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.7/1.1/0.0/0.0 (BP=0.996, ratio=0.996, hyp_len=23076, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.23-68.45.4.32-75.37.pth
BLEU = 1.43, 25.6/6.4/1.3/0.0 (BP=0.830, ratio=0.843, hyp_len=19522, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.4.02-55.92.4.11-60.82.pth
BLEU = 1.83, 31.4/8.7/1.5/0.1 (BP=0.802, ratio=0.819, hyp_len=18977, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.79-44.09.3.92-50.36.pth
BLEU = 2.68, 28.6/8.2/1.5/0.1 (BP=1.000, ratio=1.021, hyp_len=23652, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.66-38.80.3.75-42.62.pth
BLEU = 3.66, 29.7/9.5/2.2/0.3 (BP=1.000, ratio=1.093, hyp_len=25307, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.52-33.75.3.60-36.64.pth
BLEU = 4.71, 30.0/10.7/2.8/0.6 (BP=1.000, ratio=1.162, hyp_len=26906, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.27-26.28.3.47-32.25.pth
BLEU = 4.85, 28.4/10.5/2.9/0.7 (BP=1.000, ratio=1.277, hyp_len=29567, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.30-27.04.3.35-28.64.pth
BLEU = 6.78, 34.4/13.2/4.1/1.1 (BP=1.000, ratio=1.125, hyp_len=26065, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.19-24.38.3.24-25.58.pth
BLEU = 7.42, 33.6/13.4/4.7/1.4 (BP=1.000, ratio=1.224, hyp_len=28344, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.04-20.90.3.15-23.27.pth
BLEU = 8.60, 36.2/15.0/5.4/1.9 (BP=1.000, ratio=1.174, hyp_len=27186, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.2.97-19.50.3.06-21.28.pth
BLEU = 9.00, 36.0/15.4/5.9/2.0 (BP=1.000, ratio=1.248, hyp_len=28914, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.90-18.14.2.98-19.70.pth
BLEU = 11.46, 43.0/19.1/7.6/2.7 (BP=1.000, ratio=1.057, hyp_len=24491, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.85-17.35.2.89-18.05.pth
BLEU = 12.28, 43.3/19.6/8.2/3.3 (BP=1.000, ratio=1.097, hyp_len=25404, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.77-16.02.2.82-16.82.pth
BLEU = 13.16, 44.3/20.6/8.9/3.7 (BP=1.000, ratio=1.087, hyp_len=25174, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.74-15.52.2.75-15.72.pth
BLEU = 15.11, 47.9/23.1/10.5/4.5 (BP=1.000, ratio=1.038, hyp_len=24038, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.68-14.65.2.69-14.72.pth
BLEU = 14.41, 45.0/21.8/10.0/4.4 (BP=1.000, ratio=1.125, hyp_len=26054, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.65-14.19.2.63-13.86.pth
BLEU = 16.12, 48.4/24.1/11.3/5.1 (BP=1.000, ratio=1.064, hyp_len=24640, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.59-13.37.2.56-13.00.pth
BLEU = 16.43, 47.9/24.1/11.7/5.4 (BP=1.000, ratio=1.100, hyp_len=25468, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.57-13.09.2.52-12.45.pth
BLEU = 15.85, 45.4/23.2/11.4/5.3 (BP=1.000, ratio=1.195, hyp_len=27666, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.51-12.33.2.47-11.81.pth
BLEU = 18.26, 49.8/26.2/13.3/6.4 (BP=1.000, ratio=1.097, hyp_len=25397, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.46-11.74.2.41-11.12.pth
BLEU = 19.51, 51.6/27.5/14.3/7.1 (BP=1.000, ratio=1.081, hyp_len=25034, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.35-10.51.2.36-10.57.pth
BLEU = 20.24, 51.9/28.2/14.9/7.7 (BP=1.000, ratio=1.091, hyp_len=25273, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.25-9.46.2.32-10.13.pth
BLEU = 22.45, 55.7/31.0/16.8/8.8 (BP=1.000, ratio=1.025, hyp_len=23731, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.27-9.67.2.26-9.62.pth
BLEU = 21.98, 53.4/30.0/16.5/8.8 (BP=1.000, ratio=1.092, hyp_len=25289, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.22-9.22.2.21-9.15.pth
BLEU = 22.28, 53.0/30.1/16.9/9.2 (BP=1.000, ratio=1.116, hyp_len=25850, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.28-9.81.2.17-8.73.pth
BLEU = 24.56, 56.4/32.9/18.7/10.5 (BP=1.000, ratio=1.066, hyp_len=24699, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.22-9.19.2.14-8.51.pth
BLEU = 23.10, 52.8/30.8/17.7/9.9 (BP=1.000, ratio=1.168, hyp_len=27044, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.17-8.78.2.10-8.14.pth
BLEU = 25.68, 56.7/33.7/19.8/11.5 (BP=1.000, ratio=1.091, hyp_len=25267, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.04-7.66.2.06-7.82.pth
BLEU = 26.56, 57.4/34.6/20.6/12.2 (BP=1.000, ratio=1.086, hyp_len=25163, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.13-8.39.2.02-7.51.pth
BLEU = 26.49, 56.4/34.3/20.7/12.3 (BP=1.000, ratio=1.129, hyp_len=26144, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.07-7.92.1.97-7.14.pth
BLEU = 29.14, 60.2/37.2/22.9/14.1 (BP=1.000, ratio=1.065, hyp_len=24666, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.2.05-7.75.1.92-6.85.pth
BLEU = 29.64, 60.2/37.8/23.5/14.4 (BP=1.000, ratio=1.082, hyp_len=25066, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.2.04-7.68.1.89-6.59.pth
BLEU = 31.23, 61.9/39.3/24.9/15.7 (BP=1.000, ratio=1.052, hyp_len=24373, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.94-6.97.1.85-6.37.pth
BLEU = 33.55, 64.6/41.8/26.9/17.4 (BP=1.000, ratio=1.023, hyp_len=23684, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.1.97-7.15.1.82-6.16.pth
BLEU = 33.87, 64.5/42.1/27.3/17.8 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.91-6.76.1.81-6.10.pth
BLEU = 32.46, 62.3/40.7/26.2/16.7 (BP=1.000, ratio=1.084, hyp_len=25111, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.89-6.61.1.78-5.91.pth
BLEU = 33.46, 63.1/41.5/27.1/17.6 (BP=1.000, ratio=1.077, hyp_len=24938, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.89-6.63.1.74-5.70.pth
BLEU = 35.17, 65.1/43.5/28.7/18.8 (BP=1.000, ratio=1.054, hyp_len=24421, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.41.1.80-6.08.1.73-5.66.pth
BLEU = 34.44, 63.7/42.7/28.2/18.4 (BP=1.000, ratio=1.092, hyp_len=25284, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.42.1.75-5.74.1.68-5.36.pth
BLEU = 36.09, 65.3/44.3/29.7/19.8 (BP=1.000, ratio=1.066, hyp_len=24696, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.43.1.77-5.88.1.64-5.17.pth
BLEU = 37.21, 66.2/45.1/30.8/20.9 (BP=1.000, ratio=1.063, hyp_len=24615, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.44.1.81-6.10.1.66-5.27.pth
BLEU = 36.44, 65.5/44.7/30.1/20.0 (BP=1.000, ratio=1.079, hyp_len=25001, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.45.1.74-5.71.1.62-5.07.pth
BLEU = 37.11, 65.8/45.2/30.8/20.7 (BP=1.000, ratio=1.085, hyp_len=25127, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.46.1.69-5.43.1.57-4.80.pth
BLEU = 40.43, 68.8/48.1/33.8/23.9 (BP=1.000, ratio=1.039, hyp_len=24065, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.47.1.67-5.33.1.55-4.69.pth
BLEU = 41.03, 69.5/48.9/34.5/24.2 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.48.1.60-4.96.1.53-4.63.pth
BLEU = 40.39, 68.8/48.4/33.9/23.6 (BP=1.000, ratio=1.053, hyp_len=24376, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.49.1.66-5.26.1.50-4.48.pth
BLEU = 42.09, 69.8/49.9/35.6/25.3 (BP=1.000, ratio=1.043, hyp_len=24157, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.50.1.67-5.29.1.48-4.40.pth
BLEU = 43.63, 71.8/51.5/36.9/26.6 (BP=1.000, ratio=1.017, hyp_len=23546, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.51.1.65-5.22.1.46-4.29.pth
BLEU = 43.24, 71.3/51.2/36.6/26.2 (BP=1.000, ratio=1.030, hyp_len=23852, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.52.1.59-4.89.1.47-4.36.pth
BLEU = 40.73, 68.0/48.8/34.5/24.0 (BP=1.000, ratio=1.098, hyp_len=25434, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.53.1.54-4.67.1.42-4.15.pth
BLEU = 43.79, 71.3/51.7/37.4/26.7 (BP=1.000, ratio=1.041, hyp_len=24119, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.54.1.57-4.79.1.41-4.08.pth
BLEU = 44.49, 71.9/52.4/37.9/27.4 (BP=1.000, ratio=1.038, hyp_len=24032, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.55.1.48-4.41.1.41-4.10.pth
BLEU = 44.27, 71.6/52.3/37.8/27.1 (BP=1.000, ratio=1.047, hyp_len=24250, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.56.1.53-4.63.1.39-4.00.pth
BLEU = 44.17, 70.9/51.9/37.9/27.3 (BP=1.000, ratio=1.068, hyp_len=24738, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.57.1.42-4.13.1.37-3.94.pth
BLEU = 46.98, 73.3/54.4/40.4/30.3 (BP=1.000, ratio=1.029, hyp_len=23838, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.58.1.47-4.36.1.39-4.00.pth
BLEU = 44.23, 71.4/52.4/37.9/27.0 (BP=1.000, ratio=1.072, hyp_len=24822, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth
BLEU = 47.13, 73.5/54.8/40.7/30.1 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.60.1.42-4.14.1.34-3.81.pth
BLEU = 45.49, 71.9/53.4/39.2/28.4 (BP=1.000, ratio=1.072, hyp_len=24828, ref_len=23160)

real	36m8.975s
user	35m29.697s
sys	1m18.359s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-60epoch$
```

Transformer, my-rk, 60 epoch ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth
BLEU = 47.13, 73.5/54.8/40.7/30.1 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
```

### Transformer, my-rk, 70 epoch

training...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 70 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-70epoch/myrk-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/myrk-70epoch/myrk-transformer-model.pth',
    'n_epochs': 70,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.49e+05 loss=5.8703e+00 ppl=354.35                                                
Validation - loss=5.8439e+00 ppl=345.13 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.23e+02 |g_param|=3.46e+05 loss=5.0278e+00 ppl=152.60                                                
Validation - loss=5.0608e+00 ppl=157.72 best_loss=5.8439e+00 best_ppl=345.13                                            
Epoch 3 - |param|=3.23e+02 |g_param|=2.54e+05 loss=4.5418e+00 ppl=93.86                                                 
Validation - loss=4.6260e+00 ppl=102.11 best_loss=5.0608e+00 best_ppl=157.72                                            
Epoch 4 - |param|=3.23e+02 |g_param|=1.96e+05 loss=4.1908e+00 ppl=66.08                                                 
Validation - loss=4.3340e+00 ppl=76.25 best_loss=4.6260e+00 best_ppl=102.11                                             
Epoch 5 - |param|=3.23e+02 |g_param|=1.60e+05 loss=4.0099e+00 ppl=55.14                                                 
Validation - loss=4.1267e+00 ppl=61.97 best_loss=4.3340e+00 best_ppl=76.25                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.39e+05 loss=3.8117e+00 ppl=45.23                                                 
Validation - loss=3.9384e+00 ppl=51.34 best_loss=4.1267e+00 best_ppl=61.97                                              
Epoch 7 - |param|=3.24e+02 |g_param|=1.79e+05 loss=3.6139e+00 ppl=37.11                                                 
Validation - loss=3.7822e+00 ppl=43.91 best_loss=3.9384e+00 best_ppl=51.34                                              
Epoch 8 - |param|=3.24e+02 |g_param|=2.10e+05 loss=3.5490e+00 ppl=34.78                                                 
Validation - loss=3.6302e+00 ppl=37.72 best_loss=3.7822e+00 best_ppl=43.91                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.98e+05 loss=3.4139e+00 ppl=30.38                                                 
Validation - loss=3.4882e+00 ppl=32.73 best_loss=3.6302e+00 best_ppl=37.72                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.83e+05 loss=3.3353e+00 ppl=28.09                                                
Validation - loss=3.3606e+00 ppl=28.81 best_loss=3.4882e+00 best_ppl=32.73                                              
Epoch 11 - |param|=3.24e+02 |g_param|=1.60e+05 loss=3.0985e+00 ppl=22.16                                                
Validation - loss=3.2444e+00 ppl=25.65 best_loss=3.3606e+00 best_ppl=28.81                                              
Epoch 12 - |param|=3.24e+02 |g_param|=2.08e+05 loss=3.0540e+00 ppl=21.20                                                
Validation - loss=3.1546e+00 ppl=23.44 best_loss=3.2444e+00 best_ppl=25.65                                              
Epoch 13 - |param|=3.24e+02 |g_param|=2.45e+05 loss=2.9509e+00 ppl=19.12                                                
Validation - loss=3.0447e+00 ppl=21.00 best_loss=3.1546e+00 best_ppl=23.44                                              
Epoch 14 - |param|=3.24e+02 |g_param|=1.89e+05 loss=2.9050e+00 ppl=18.27                                                
Validation - loss=2.9598e+00 ppl=19.29 best_loss=3.0447e+00 best_ppl=21.00                                              
Epoch 15 - |param|=3.24e+02 |g_param|=3.19e+05 loss=2.8585e+00 ppl=17.44                                                
Validation - loss=2.8799e+00 ppl=17.81 best_loss=2.9598e+00 best_ppl=19.29                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.96e+05 loss=2.7504e+00 ppl=15.65                                                
Validation - loss=2.8021e+00 ppl=16.48 best_loss=2.8799e+00 best_ppl=17.81                                              
Epoch 17 - |param|=3.25e+02 |g_param|=3.15e+05 loss=2.6963e+00 ppl=14.83                                                
Validation - loss=2.7391e+00 ppl=15.47 best_loss=2.8021e+00 best_ppl=16.48                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.05e+05 loss=2.6857e+00 ppl=14.67                                                
Validation - loss=2.6768e+00 ppl=14.54 best_loss=2.7391e+00 best_ppl=15.47                                              
Epoch 19 - |param|=3.25e+02 |g_param|=2.77e+05 loss=2.5978e+00 ppl=13.43                                                
Validation - loss=2.6143e+00 ppl=13.66 best_loss=2.6768e+00 best_ppl=14.54                                              
Epoch 20 - |param|=3.25e+02 |g_param|=2.64e+05 loss=2.4654e+00 ppl=11.77                                                
Validation - loss=2.5511e+00 ppl=12.82 best_loss=2.6143e+00 best_ppl=13.66                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.09e+05 loss=2.4891e+00 ppl=12.05                                                
Validation - loss=2.4962e+00 ppl=12.14 best_loss=2.5511e+00 best_ppl=12.82                                              
Epoch 22 - |param|=3.25e+02 |g_param|=3.07e+05 loss=2.4304e+00 ppl=11.36                                                
Validation - loss=2.4396e+00 ppl=11.47 best_loss=2.4962e+00 best_ppl=12.14                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.91e+05 loss=2.3321e+00 ppl=10.30                                                
Validation - loss=2.3859e+00 ppl=10.87 best_loss=2.4396e+00 best_ppl=11.47                                              
Epoch 24 - |param|=3.25e+02 |g_param|=2.88e+05 loss=2.3529e+00 ppl=10.52                                                
Validation - loss=2.3332e+00 ppl=10.31 best_loss=2.3859e+00 best_ppl=10.87                                              
Epoch 25 - |param|=3.25e+02 |g_param|=3.96e+05 loss=2.3338e+00 ppl=10.32                                                
Validation - loss=2.2847e+00 ppl=9.82 best_loss=2.3332e+00 best_ppl=10.31                                               
Epoch 26 - |param|=3.25e+02 |g_param|=3.25e+05 loss=2.3108e+00 ppl=10.08                                                
Validation - loss=2.2270e+00 ppl=9.27 best_loss=2.2847e+00 best_ppl=9.82                                                
Epoch 27 - |param|=3.25e+02 |g_param|=2.88e+05 loss=2.2454e+00 ppl=9.44                                                 
Validation - loss=2.1840e+00 ppl=8.88 best_loss=2.2270e+00 best_ppl=9.27                                                
Epoch 28 - |param|=3.25e+02 |g_param|=3.35e+05 loss=2.1875e+00 ppl=8.91                                                 
Validation - loss=2.1355e+00 ppl=8.46 best_loss=2.1840e+00 best_ppl=8.88                                                
Epoch 29 - |param|=3.25e+02 |g_param|=3.72e+05 loss=2.1652e+00 ppl=8.72                                                 
Validation - loss=2.0950e+00 ppl=8.13 best_loss=2.1355e+00 best_ppl=8.46                                                
Epoch 30 - |param|=3.25e+02 |g_param|=3.57e+05 loss=2.1401e+00 ppl=8.50                                                 
Validation - loss=2.0457e+00 ppl=7.73 best_loss=2.0950e+00 best_ppl=8.13                                                
Epoch 31 - |param|=3.25e+02 |g_param|=4.42e+05 loss=2.0874e+00 ppl=8.06                                                 
Validation - loss=2.0098e+00 ppl=7.46 best_loss=2.0457e+00 best_ppl=7.73                                                
Epoch 32 - |param|=3.25e+02 |g_param|=3.51e+05 loss=2.0226e+00 ppl=7.56                                                 
Validation - loss=1.9678e+00 ppl=7.15 best_loss=2.0098e+00 best_ppl=7.46                                                
Epoch 33 - |param|=3.25e+02 |g_param|=3.75e+05 loss=1.9959e+00 ppl=7.36                                                 
Validation - loss=1.9233e+00 ppl=6.84 best_loss=1.9678e+00 best_ppl=7.15                                                
Epoch 34 - |param|=3.25e+02 |g_param|=4.72e+05 loss=2.0148e+00 ppl=7.50                                                 
Validation - loss=1.8840e+00 ppl=6.58 best_loss=1.9233e+00 best_ppl=6.84                                                
Epoch 35 - |param|=3.25e+02 |g_param|=3.81e+05 loss=1.9519e+00 ppl=7.04                                                 
Validation - loss=1.8505e+00 ppl=6.36 best_loss=1.8840e+00 best_ppl=6.58                                                
Epoch 36 - |param|=3.25e+02 |g_param|=4.07e+05 loss=1.9156e+00 ppl=6.79                                                 
Validation - loss=1.8103e+00 ppl=6.11 best_loss=1.8505e+00 best_ppl=6.36                                                
Epoch 37 - |param|=3.25e+02 |g_param|=5.94e+05 loss=1.8998e+00 ppl=6.68                                                 
Validation - loss=1.7797e+00 ppl=5.93 best_loss=1.8103e+00 best_ppl=6.11                                                
Epoch 38 - |param|=3.25e+02 |g_param|=3.54e+05 loss=1.8026e+00 ppl=6.07                                                 
Validation - loss=1.7564e+00 ppl=5.79 best_loss=1.7797e+00 best_ppl=5.93                                                
Epoch 39 - |param|=3.25e+02 |g_param|=4.08e+05 loss=1.8397e+00 ppl=6.29                                                 
Validation - loss=1.7166e+00 ppl=5.57 best_loss=1.7564e+00 best_ppl=5.79                                                
Epoch 40 - |param|=3.25e+02 |g_param|=5.63e+05 loss=1.8544e+00 ppl=6.39                                                 
Validation - loss=1.6856e+00 ppl=5.40 best_loss=1.7166e+00 best_ppl=5.57                                                
Epoch 41 - |param|=3.25e+02 |g_param|=5.78e+05 loss=1.7504e+00 ppl=5.76                                                 
Validation - loss=1.6631e+00 ppl=5.28 best_loss=1.6856e+00 best_ppl=5.40                                                
Epoch 42 - |param|=3.25e+02 |g_param|=3.43e+05 loss=1.7587e+00 ppl=5.80                                                 
Validation - loss=1.6242e+00 ppl=5.07 best_loss=1.6631e+00 best_ppl=5.28                                                
Epoch 43 - |param|=3.25e+02 |g_param|=5.71e+05 loss=1.7294e+00 ppl=5.64                                                 
Validation - loss=1.5961e+00 ppl=4.93 best_loss=1.6242e+00 best_ppl=5.07                                                
Epoch 44 - |param|=3.26e+02 |g_param|=6.38e+05 loss=1.6671e+00 ppl=5.30                                                 
Validation - loss=1.5859e+00 ppl=4.88 best_loss=1.5961e+00 best_ppl=4.93                                                
Epoch 45 - |param|=3.26e+02 |g_param|=9.34e+05 loss=1.6408e+00 ppl=5.16                                                 
Validation - loss=1.5573e+00 ppl=4.75 best_loss=1.5859e+00 best_ppl=4.88                                                
Epoch 46 - |param|=3.26e+02 |g_param|=7.02e+05 loss=1.6644e+00 ppl=5.28                                                 
Validation - loss=1.5299e+00 ppl=4.62 best_loss=1.5573e+00 best_ppl=4.75                                                
Epoch 47 - |param|=3.26e+02 |g_param|=4.21e+05 loss=1.6267e+00 ppl=5.09                                                 
Validation - loss=1.5082e+00 ppl=4.52 best_loss=1.5299e+00 best_ppl=4.62                                                
Epoch 48 - |param|=3.26e+02 |g_param|=5.58e+05 loss=1.5869e+00 ppl=4.89                                                 
Validation - loss=1.4808e+00 ppl=4.40 best_loss=1.5082e+00 best_ppl=4.52                                                
Epoch 49 - |param|=3.26e+02 |g_param|=5.21e+05 loss=1.5907e+00 ppl=4.91                                                 
Validation - loss=1.4698e+00 ppl=4.35 best_loss=1.4808e+00 best_ppl=4.40                                                
Epoch 50 - |param|=3.26e+02 |g_param|=7.19e+05 loss=1.5426e+00 ppl=4.68                                                 
Validation - loss=1.4547e+00 ppl=4.28 best_loss=1.4698e+00 best_ppl=4.35                                                
Epoch 51 - |param|=3.26e+02 |g_param|=7.14e+05 loss=1.6005e+00 ppl=4.96                                                 
Validation - loss=1.4517e+00 ppl=4.27 best_loss=1.4547e+00 best_ppl=4.28                                                
Epoch 52 - |param|=3.26e+02 |g_param|=8.56e+05 loss=1.5120e+00 ppl=4.54                                                 
Validation - loss=1.4020e+00 ppl=4.06 best_loss=1.4517e+00 best_ppl=4.27                                                
Epoch 53 - |param|=3.26e+02 |g_param|=6.17e+05 loss=1.5219e+00 ppl=4.58                                                 
Validation - loss=1.3894e+00 ppl=4.01 best_loss=1.4020e+00 best_ppl=4.06                                                
Epoch 54 - |param|=3.26e+02 |g_param|=9.27e+05 loss=1.4672e+00 ppl=4.34                                                 
Validation - loss=1.3864e+00 ppl=4.00 best_loss=1.3894e+00 best_ppl=4.01                                                
Epoch 55 - |param|=3.26e+02 |g_param|=6.26e+05 loss=1.4972e+00 ppl=4.47                                                 
Validation - loss=1.3567e+00 ppl=3.88 best_loss=1.3864e+00 best_ppl=4.00                                                
Epoch 56 - |param|=3.26e+02 |g_param|=4.57e+05 loss=1.4466e+00 ppl=4.25                                                 
Validation - loss=1.3416e+00 ppl=3.83 best_loss=1.3567e+00 best_ppl=3.88                                                
Epoch 57 - |param|=3.26e+02 |g_param|=5.87e+05 loss=1.4607e+00 ppl=4.31                                                 
Validation - loss=1.3317e+00 ppl=3.79 best_loss=1.3416e+00 best_ppl=3.83                                                
Epoch 58 - |param|=3.26e+02 |g_param|=6.68e+05 loss=1.4463e+00 ppl=4.25                                                 
Validation - loss=1.3092e+00 ppl=3.70 best_loss=1.3317e+00 best_ppl=3.79                                                
Epoch 59 - |param|=3.26e+02 |g_param|=6.87e+05 loss=1.4131e+00 ppl=4.11                                                 
Validation - loss=1.3051e+00 ppl=3.69 best_loss=1.3092e+00 best_ppl=3.70                                                
Epoch 60 - |param|=3.26e+02 |g_param|=7.56e+05 loss=1.4523e+00 ppl=4.27                                                 
Validation - loss=1.2773e+00 ppl=3.59 best_loss=1.3051e+00 best_ppl=3.69                                                
Epoch 61 - |param|=3.26e+02 |g_param|=4.57e+05 loss=1.3757e+00 ppl=3.96                                                 
Validation - loss=1.2817e+00 ppl=3.60 best_loss=1.2773e+00 best_ppl=3.59                                                
Epoch 62 - |param|=3.26e+02 |g_param|=7.91e+05 loss=1.3595e+00 ppl=3.89                                                 
Validation - loss=1.2640e+00 ppl=3.54 best_loss=1.2773e+00 best_ppl=3.59                                                
Epoch 63 - |param|=3.26e+02 |g_param|=8.75e+05 loss=1.3942e+00 ppl=4.03                                                 
Validation - loss=1.2534e+00 ppl=3.50 best_loss=1.2640e+00 best_ppl=3.54                                                
Epoch 64 - |param|=3.26e+02 |g_param|=7.41e+05 loss=1.3196e+00 ppl=3.74                                                 
Validation - loss=1.2400e+00 ppl=3.46 best_loss=1.2534e+00 best_ppl=3.50                                                
Epoch 65 - |param|=3.26e+02 |g_param|=8.08e+05 loss=1.3376e+00 ppl=3.81                                                 
Validation - loss=1.2305e+00 ppl=3.42 best_loss=1.2400e+00 best_ppl=3.46                                                
Epoch 66 - |param|=3.26e+02 |g_param|=5.86e+05 loss=1.3617e+00 ppl=3.90                                                 
Validation - loss=1.2236e+00 ppl=3.40 best_loss=1.2305e+00 best_ppl=3.42                                                
Epoch 67 - |param|=3.26e+02 |g_param|=9.44e+05 loss=1.3166e+00 ppl=3.73                                                 
Validation - loss=1.2283e+00 ppl=3.42 best_loss=1.2236e+00 best_ppl=3.40                                                
Epoch 68 - |param|=3.26e+02 |g_param|=7.08e+05 loss=1.3044e+00 ppl=3.69                                                 
Validation - loss=1.1971e+00 ppl=3.31 best_loss=1.2236e+00 best_ppl=3.40                                                
Epoch 69 - |param|=3.26e+02 |g_param|=5.96e+05 loss=1.2417e+00 ppl=3.46                                                 
Validation - loss=1.1937e+00 ppl=3.30 best_loss=1.1971e+00 best_ppl=3.31                                                
Epoch 70 - |param|=3.26e+02 |g_param|=7.07e+05 loss=1.2694e+00 ppl=3.56                                                 
Validation - loss=1.1683e+00 ppl=3.22 best_loss=1.1937e+00 best_ppl=3.30                                                

real	37m57.771s
user	37m43.886s
sys	0m7.496s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.87-354.35.5.84-345.13.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 30.0/0.0/0.0/0.0 (BP=0.089, ratio=0.293, hyp_len=6778, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.5.03-152.60.5.06-157.72.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 45.9/1.2/0.0/0.0 (BP=0.101, ratio=0.303, hyp_len=7024, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.54-93.86.4.63-102.11.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 33.5/1.3/0.1/0.0 (BP=0.218, ratio=0.396, hyp_len=9176, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.19-66.08.4.33-76.25.pth
BLEU = 1.25, 35.1/7.7/1.0/0.1 (BP=0.621, ratio=0.677, hyp_len=15687, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.4.01-55.14.4.13-61.97.pth
BLEU = 1.58, 31.4/8.5/1.1/0.1 (BP=0.812, ratio=0.828, hyp_len=19167, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.81-45.23.3.94-51.34.pth
BLEU = 2.57, 26.4/8.4/1.4/0.1 (BP=1.000, ratio=1.077, hyp_len=24938, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.61-37.11.3.78-43.91.pth
BLEU = 3.92, 25.4/9.0/2.1/0.5 (BP=1.000, ratio=1.269, hyp_len=29388, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.55-34.78.3.63-37.72.pth
BLEU = 6.19, 32.0/12.3/3.5/1.1 (BP=1.000, ratio=1.102, hyp_len=25518, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.41-30.38.3.49-32.73.pth
BLEU = 6.16, 30.9/12.1/3.7/1.1 (BP=1.000, ratio=1.214, hyp_len=28109, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.34-28.09.3.36-28.81.pth
BLEU = 7.41, 35.0/14.1/4.6/1.3 (BP=1.000, ratio=1.115, hyp_len=25815, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.10-22.16.3.24-25.65.pth
BLEU = 8.05, 35.8/14.7/5.1/1.6 (BP=1.000, ratio=1.131, hyp_len=26202, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.05-21.20.3.15-23.44.pth
BLEU = 9.60, 40.6/17.2/6.3/1.9 (BP=1.000, ratio=1.032, hyp_len=23893, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.2.95-19.12.3.04-21.00.pth
BLEU = 9.87, 39.7/17.2/6.4/2.2 (BP=1.000, ratio=1.116, hyp_len=25846, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.91-18.27.2.96-19.29.pth
BLEU = 11.41, 42.3/19.0/7.7/2.7 (BP=1.000, ratio=1.074, hyp_len=24870, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.86-17.44.2.88-17.81.pth
BLEU = 12.66, 44.5/20.4/8.7/3.3 (BP=1.000, ratio=1.062, hyp_len=24599, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.75-15.65.2.80-16.48.pth
BLEU = 12.33, 42.2/19.6/8.5/3.3 (BP=1.000, ratio=1.160, hyp_len=26873, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.70-14.83.2.74-15.47.pth
BLEU = 14.50, 46.8/22.5/10.2/4.1 (BP=1.000, ratio=1.063, hyp_len=24617, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.69-14.67.2.68-14.54.pth
BLEU = 15.95, 48.3/23.8/11.3/5.0 (BP=1.000, ratio=1.051, hyp_len=24346, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.60-13.43.2.61-13.66.pth
BLEU = 16.86, 49.3/24.8/12.0/5.5 (BP=1.000, ratio=1.057, hyp_len=24480, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.47-11.77.2.55-12.82.pth
BLEU = 17.69, 50.3/25.5/12.7/6.0 (BP=1.000, ratio=1.049, hyp_len=24300, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.49-12.05.2.50-12.14.pth
BLEU = 18.22, 49.9/26.0/13.2/6.4 (BP=1.000, ratio=1.091, hyp_len=25273, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.43-11.36.2.44-11.47.pth
BLEU = 18.73, 50.4/26.7/13.8/6.7 (BP=1.000, ratio=1.096, hyp_len=25375, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.33-10.30.2.39-10.87.pth
BLEU = 19.10, 50.0/26.8/14.1/7.1 (BP=1.000, ratio=1.118, hyp_len=25883, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.35-10.52.2.33-10.31.pth
BLEU = 21.57, 54.0/29.7/16.1/8.4 (BP=1.000, ratio=1.052, hyp_len=24360, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.33-10.32.2.28-9.82.pth
BLEU = 21.93, 53.6/30.0/16.5/8.7 (BP=1.000, ratio=1.076, hyp_len=24911, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.31-10.08.2.23-9.27.pth
BLEU = 24.11, 56.6/32.4/18.3/10.1 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.25-9.44.2.18-8.88.pth
BLEU = 25.37, 58.1/33.7/19.4/10.9 (BP=1.000, ratio=1.017, hyp_len=23559, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.19-8.91.2.14-8.46.pth
BLEU = 24.60, 55.8/32.7/18.9/10.6 (BP=1.000, ratio=1.081, hyp_len=25038, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.17-8.72.2.10-8.13.pth
BLEU = 26.72, 58.9/35.0/20.7/12.0 (BP=1.000, ratio=1.033, hyp_len=23923, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.14-8.50.2.05-7.73.pth
BLEU = 26.81, 58.0/35.0/20.8/12.2 (BP=1.000, ratio=1.075, hyp_len=24889, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.09-8.06.2.01-7.46.pth
BLEU = 28.53, 60.2/36.9/22.4/13.3 (BP=1.000, ratio=1.038, hyp_len=24046, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.02-7.56.1.97-7.15.pth
BLEU = 28.31, 59.5/36.6/22.2/13.3 (BP=1.000, ratio=1.069, hyp_len=24755, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.00-7.36.1.92-6.84.pth
BLEU = 29.38, 59.5/37.2/23.3/14.5 (BP=1.000, ratio=1.082, hyp_len=25058, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.2.01-7.50.1.88-6.58.pth
BLEU = 30.97, 61.6/39.0/24.7/15.5 (BP=1.000, ratio=1.056, hyp_len=24448, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.1.95-7.04.1.85-6.36.pth
BLEU = 32.19, 62.2/40.1/25.9/16.7 (BP=1.000, ratio=1.061, hyp_len=24572, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.92-6.79.1.81-6.11.pth
BLEU = 33.47, 63.7/41.6/27.1/17.5 (BP=1.000, ratio=1.045, hyp_len=24200, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.1.90-6.68.1.78-5.93.pth
BLEU = 33.27, 63.2/41.3/26.9/17.4 (BP=1.000, ratio=1.064, hyp_len=24650, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.80-6.07.1.76-5.79.pth
BLEU = 36.32, 66.9/44.6/29.7/19.6 (BP=1.000, ratio=1.007, hyp_len=23314, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.84-6.29.1.72-5.57.pth
BLEU = 35.26, 64.8/43.3/28.8/19.1 (BP=1.000, ratio=1.055, hyp_len=24435, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.85-6.39.1.69-5.40.pth
BLEU = 37.42, 66.9/45.4/30.8/20.9 (BP=1.000, ratio=1.024, hyp_len=23726, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.41.1.75-5.76.1.66-5.28.pth
BLEU = 36.61, 65.0/44.2/30.2/20.7 (BP=1.000, ratio=1.069, hyp_len=24752, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.42.1.76-5.80.1.62-5.07.pth
BLEU = 37.60, 66.8/45.7/31.1/21.1 (BP=1.000, ratio=1.050, hyp_len=24313, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.43.1.73-5.64.1.60-4.93.pth
BLEU = 38.99, 67.8/46.8/32.4/22.5 (BP=1.000, ratio=1.041, hyp_len=24104, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.44.1.67-5.30.1.59-4.88.pth
BLEU = 40.11, 68.7/47.9/33.5/23.4 (BP=1.000, ratio=1.028, hyp_len=23815, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.45.1.64-5.16.1.56-4.75.pth
BLEU = 39.59, 68.0/47.5/33.1/23.0 (BP=1.000, ratio=1.048, hyp_len=24277, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.46.1.66-5.28.1.53-4.62.pth
BLEU = 41.28, 69.8/49.2/34.7/24.4 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.47.1.63-5.09.1.51-4.52.pth
BLEU = 41.14, 69.3/49.2/34.6/24.3 (BP=1.000, ratio=1.051, hyp_len=24331, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.48.1.59-4.89.1.48-4.40.pth
BLEU = 41.89, 70.1/49.8/35.3/25.0 (BP=1.000, ratio=1.043, hyp_len=24153, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.49.1.59-4.91.1.47-4.35.pth
BLEU = 43.12, 70.7/50.8/36.5/26.4 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.50.1.54-4.68.1.45-4.28.pth
BLEU = 42.12, 70.1/50.2/35.6/25.1 (BP=1.000, ratio=1.049, hyp_len=24305, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.51.1.60-4.96.1.45-4.27.pth
BLEU = 41.15, 68.6/49.2/34.9/24.3 (BP=1.000, ratio=1.086, hyp_len=25141, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.52.1.51-4.54.1.40-4.06.pth
BLEU = 44.94, 72.5/52.9/38.3/27.8 (BP=1.000, ratio=1.026, hyp_len=23758, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.53.1.52-4.58.1.39-4.01.pth
BLEU = 45.14, 72.1/52.9/38.6/28.2 (BP=1.000, ratio=1.038, hyp_len=24042, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.54.1.47-4.34.1.39-4.00.pth
BLEU = 47.13, 74.1/54.6/40.4/30.2 (BP=1.000, ratio=1.006, hyp_len=23302, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.55.1.50-4.47.1.36-3.88.pth
BLEU = 45.86, 72.2/53.4/39.4/29.1 (BP=1.000, ratio=1.044, hyp_len=24174, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.56.1.45-4.25.1.34-3.83.pth
BLEU = 45.78, 72.2/53.5/39.4/28.9 (BP=1.000, ratio=1.049, hyp_len=24285, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.57.1.46-4.31.1.33-3.79.pth
BLEU = 45.80, 72.0/53.4/39.4/29.0 (BP=1.000, ratio=1.054, hyp_len=24420, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.58.1.45-4.25.1.31-3.70.pth
BLEU = 47.68, 73.7/55.1/41.2/30.9 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.59.1.41-4.11.1.31-3.69.pth
BLEU = 47.85, 74.1/55.3/41.4/30.9 (BP=1.000, ratio=1.028, hyp_len=23804, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.60.1.45-4.27.1.28-3.59.pth
BLEU = 48.56, 74.5/56.0/42.1/31.7 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.61.1.38-3.96.1.28-3.60.pth
BLEU = 47.20, 73.1/54.9/40.9/30.3 (BP=1.000, ratio=1.056, hyp_len=24459, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.62.1.36-3.89.1.26-3.54.pth
BLEU = 47.47, 73.4/55.3/41.2/30.4 (BP=1.000, ratio=1.054, hyp_len=24418, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.63.1.39-4.03.1.25-3.50.pth
BLEU = 46.62, 72.1/54.2/40.4/29.9 (BP=1.000, ratio=1.079, hyp_len=24993, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.64.1.32-3.74.1.24-3.46.pth
BLEU = 47.79, 72.9/55.2/41.6/31.1 (BP=1.000, ratio=1.070, hyp_len=24772, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.65.1.34-3.81.1.23-3.42.pth
BLEU = 48.44, 73.9/56.2/42.2/31.4 (BP=1.000, ratio=1.056, hyp_len=24448, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.66.1.36-3.90.1.22-3.40.pth
BLEU = 48.61, 73.7/56.1/42.4/31.9 (BP=1.000, ratio=1.065, hyp_len=24659, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.67.1.32-3.73.1.23-3.42.pth
BLEU = 48.74, 74.2/56.6/42.5/31.6 (BP=1.000, ratio=1.057, hyp_len=24474, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.68.1.30-3.69.1.20-3.31.pth
BLEU = 50.18, 75.3/57.7/43.9/33.2 (BP=1.000, ratio=1.042, hyp_len=24137, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.69.1.24-3.46.1.19-3.30.pth
BLEU = 48.88, 73.3/56.2/42.8/32.4 (BP=1.000, ratio=1.079, hyp_len=24981, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth
BLEU = 50.51, 75.0/57.8/44.3/33.9 (BP=1.000, ratio=1.057, hyp_len=24476, ref_len=23160)

real	39m4.007s
user	38m18.923s
sys	1m31.064s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-70epoch$
```

Transformer, my-rk, 70 epochs ရဲ့ အကောင်းဆုံး BLEU score က အောက်ပါအတိုင်း  

```
Evaluation result for the model: myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth
BLEU = 50.51, 75.0/57.8/44.3/33.9 (BP=1.000, ratio=1.057, hyp_len=24476, ref_len=23160)
```

### Transformer, rk-my, 40 epoch

training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.pth',
    'n_epochs': 40,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.49e+05 loss=5.6892e+00 ppl=295.64                                                
Validation - loss=5.7029e+00 ppl=299.74 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.23e+02 |g_param|=3.17e+05 loss=4.8930e+00 ppl=133.36                                                
Validation - loss=4.9650e+00 ppl=143.31 best_loss=5.7029e+00 best_ppl=299.74                                            
Epoch 3 - |param|=3.23e+02 |g_param|=2.20e+05 loss=4.4449e+00 ppl=85.19                                                 
Validation - loss=4.6091e+00 ppl=100.39 best_loss=4.9650e+00 best_ppl=143.31                                            
Epoch 4 - |param|=3.23e+02 |g_param|=1.71e+05 loss=4.2503e+00 ppl=70.12                                                 
Validation - loss=4.3634e+00 ppl=78.52 best_loss=4.6091e+00 best_ppl=100.39                                             
Epoch 5 - |param|=3.24e+02 |g_param|=1.73e+05 loss=4.0840e+00 ppl=59.38                                                 
Validation - loss=4.1533e+00 ppl=63.65 best_loss=4.3634e+00 best_ppl=78.52                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.52e+05 loss=3.8114e+00 ppl=45.22                                                 
Validation - loss=3.9528e+00 ppl=52.08 best_loss=4.1533e+00 best_ppl=63.65                                              
Epoch 7 - |param|=3.24e+02 |g_param|=2.14e+05 loss=3.6307e+00 ppl=37.74                                                 
Validation - loss=3.7778e+00 ppl=43.72 best_loss=3.9528e+00 best_ppl=52.08                                              
Epoch 8 - |param|=3.24e+02 |g_param|=1.34e+05 loss=3.5027e+00 ppl=33.21                                                 
Validation - loss=3.6105e+00 ppl=36.99 best_loss=3.7778e+00 best_ppl=43.72                                              
Epoch 9 - |param|=3.24e+02 |g_param|=2.63e+05 loss=3.4082e+00 ppl=30.21                                                 
Validation - loss=3.4868e+00 ppl=32.68 best_loss=3.6105e+00 best_ppl=36.99                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.83e+05 loss=3.3271e+00 ppl=27.86                                                
Validation - loss=3.3298e+00 ppl=27.93 best_loss=3.4868e+00 best_ppl=32.68                                              
Epoch 11 - |param|=3.24e+02 |g_param|=1.63e+05 loss=3.1384e+00 ppl=23.07                                                
Validation - loss=3.2100e+00 ppl=24.78 best_loss=3.3298e+00 best_ppl=27.93                                              
Epoch 12 - |param|=3.24e+02 |g_param|=1.99e+05 loss=3.0859e+00 ppl=21.89                                                
Validation - loss=3.1001e+00 ppl=22.20 best_loss=3.2100e+00 best_ppl=24.78                                              
Epoch 13 - |param|=3.24e+02 |g_param|=1.93e+05 loss=2.8998e+00 ppl=18.17                                                
Validation - loss=3.0081e+00 ppl=20.25 best_loss=3.1001e+00 best_ppl=22.20                                              
Epoch 14 - |param|=3.24e+02 |g_param|=3.78e+05 loss=2.8953e+00 ppl=18.09                                                
Validation - loss=2.9174e+00 ppl=18.49 best_loss=3.0081e+00 best_ppl=20.25                                              
Epoch 15 - |param|=3.24e+02 |g_param|=2.61e+05 loss=2.7982e+00 ppl=16.42                                                
Validation - loss=2.8346e+00 ppl=17.02 best_loss=2.9174e+00 best_ppl=18.49                                              
Epoch 16 - |param|=3.24e+02 |g_param|=3.57e+05 loss=2.7646e+00 ppl=15.87                                                
Validation - loss=2.7551e+00 ppl=15.72 best_loss=2.8346e+00 best_ppl=17.02                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.03e+05 loss=2.6589e+00 ppl=14.28                                                
Validation - loss=2.6879e+00 ppl=14.70 best_loss=2.7551e+00 best_ppl=15.72                                              
Epoch 18 - |param|=3.25e+02 |g_param|=2.68e+05 loss=2.5695e+00 ppl=13.06                                                
Validation - loss=2.6226e+00 ppl=13.77 best_loss=2.6879e+00 best_ppl=14.70                                              
Epoch 19 - |param|=3.25e+02 |g_param|=2.46e+05 loss=2.5554e+00 ppl=12.88                                                
Validation - loss=2.5635e+00 ppl=12.98 best_loss=2.6226e+00 best_ppl=13.77                                              
Epoch 20 - |param|=3.25e+02 |g_param|=3.07e+05 loss=2.4592e+00 ppl=11.70                                                
Validation - loss=2.5040e+00 ppl=12.23 best_loss=2.5635e+00 best_ppl=12.98                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.47e+05 loss=2.3875e+00 ppl=10.89                                                
Validation - loss=2.4406e+00 ppl=11.48 best_loss=2.5040e+00 best_ppl=12.23                                              
Epoch 22 - |param|=3.25e+02 |g_param|=3.09e+05 loss=2.4411e+00 ppl=11.49                                                
Validation - loss=2.3911e+00 ppl=10.93 best_loss=2.4406e+00 best_ppl=11.48                                              
Epoch 23 - |param|=3.25e+02 |g_param|=4.66e+05 loss=2.4492e+00 ppl=11.58                                                
Validation - loss=2.3505e+00 ppl=10.49 best_loss=2.3911e+00 best_ppl=10.93                                              
Epoch 24 - |param|=3.25e+02 |g_param|=2.87e+05 loss=2.3098e+00 ppl=10.07                                                
Validation - loss=2.2805e+00 ppl=9.78 best_loss=2.3505e+00 best_ppl=10.49                                               
Epoch 25 - |param|=3.25e+02 |g_param|=3.31e+05 loss=2.2572e+00 ppl=9.56                                                 
Validation - loss=2.2365e+00 ppl=9.36 best_loss=2.2805e+00 best_ppl=9.78                                                
Epoch 26 - |param|=3.25e+02 |g_param|=3.81e+05 loss=2.2435e+00 ppl=9.43                                                 
Validation - loss=2.1826e+00 ppl=8.87 best_loss=2.2365e+00 best_ppl=9.36                                                
Epoch 27 - |param|=3.25e+02 |g_param|=3.64e+05 loss=2.2301e+00 ppl=9.30                                                 
Validation - loss=2.1408e+00 ppl=8.51 best_loss=2.1826e+00 best_ppl=8.87                                                
Epoch 28 - |param|=3.25e+02 |g_param|=3.54e+05 loss=2.1050e+00 ppl=8.21                                                 
Validation - loss=2.1034e+00 ppl=8.19 best_loss=2.1408e+00 best_ppl=8.51                                                
Epoch 29 - |param|=3.25e+02 |g_param|=3.98e+05 loss=2.0936e+00 ppl=8.11                                                 
Validation - loss=2.0548e+00 ppl=7.81 best_loss=2.1034e+00 best_ppl=8.19                                                
Epoch 30 - |param|=3.25e+02 |g_param|=3.65e+05 loss=2.0118e+00 ppl=7.48                                                 
Validation - loss=2.0105e+00 ppl=7.47 best_loss=2.0548e+00 best_ppl=7.81                                                
Epoch 31 - |param|=3.25e+02 |g_param|=3.23e+05 loss=2.0790e+00 ppl=8.00                                                 
Validation - loss=1.9677e+00 ppl=7.15 best_loss=2.0105e+00 best_ppl=7.47                                                
Epoch 32 - |param|=3.25e+02 |g_param|=4.62e+05 loss=2.0467e+00 ppl=7.74                                                 
Validation - loss=1.9305e+00 ppl=6.89 best_loss=1.9677e+00 best_ppl=7.15                                                
Epoch 33 - |param|=3.25e+02 |g_param|=5.15e+05 loss=1.9866e+00 ppl=7.29                                                 
Validation - loss=1.9247e+00 ppl=6.85 best_loss=1.9305e+00 best_ppl=6.89                                                
Epoch 34 - |param|=3.25e+02 |g_param|=5.93e+05 loss=2.0172e+00 ppl=7.52                                                 
Validation - loss=1.8615e+00 ppl=6.43 best_loss=1.9247e+00 best_ppl=6.85                                                
Epoch 35 - |param|=3.25e+02 |g_param|=4.55e+05 loss=1.9018e+00 ppl=6.70                                                 
Validation - loss=1.8256e+00 ppl=6.21 best_loss=1.8615e+00 best_ppl=6.43                                                
Epoch 36 - |param|=3.25e+02 |g_param|=5.51e+05 loss=1.9220e+00 ppl=6.83                                                 
Validation - loss=1.7858e+00 ppl=5.96 best_loss=1.8256e+00 best_ppl=6.21                                                
Epoch 37 - |param|=3.26e+02 |g_param|=3.69e+05 loss=1.9417e+00 ppl=6.97                                                 
Validation - loss=1.7599e+00 ppl=5.81 best_loss=1.7858e+00 best_ppl=5.96                                                
Epoch 38 - |param|=3.26e+02 |g_param|=3.42e+05 loss=1.7838e+00 ppl=5.95                                                 
Validation - loss=1.7195e+00 ppl=5.58 best_loss=1.7599e+00 best_ppl=5.81                                                
Epoch 39 - |param|=3.26e+02 |g_param|=4.00e+05 loss=1.8900e+00 ppl=6.62                                                 
Validation - loss=1.6871e+00 ppl=5.40 best_loss=1.7195e+00 best_ppl=5.58                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.05e+05 loss=1.8301e+00 ppl=6.23                                                 
Validation - loss=1.6672e+00 ppl=5.30 best_loss=1.6871e+00 best_ppl=5.40                                                

real	20m44.438s
user	20m39.416s
sys	0m4.416s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.69-295.64.5.70-299.74.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 32.9/9.4/0.0/0.0 (BP=0.106, ratio=0.308, hyp_len=7244, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.4.89-133.36.4.96-143.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 63.2/24.7/0.0/0.0 (BP=0.006, ratio=0.165, hyp_len=3869, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.44-85.19.4.61-100.39.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.9/3.4/0.0/0.0 (BP=0.377, ratio=0.506, hyp_len=11903, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.25-70.12.4.36-78.52.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.2/4.5/0.2/0.0 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.08-59.38.4.15-63.65.pth
BLEU = 1.69, 27.3/7.3/0.7/0.1 (BP=1.000, ratio=1.000, hyp_len=23501, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.81-45.22.3.95-52.08.pth
BLEU = 2.47, 23.2/6.8/1.2/0.2 (BP=1.000, ratio=1.323, hyp_len=31112, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.63-37.74.3.78-43.72.pth
BLEU = 3.69, 27.7/9.2/2.0/0.4 (BP=1.000, ratio=1.170, hyp_len=27508, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.50-33.21.3.61-36.99.pth
BLEU = 4.86, 30.0/10.9/2.9/0.6 (BP=1.000, ratio=1.136, hyp_len=26698, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.41-30.21.3.49-32.68.pth
BLEU = 6.56, 35.7/13.9/4.2/0.9 (BP=0.993, ratio=0.993, hyp_len=23334, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.33-27.86.3.33-27.93.pth
BLEU = 5.94, 29.2/11.8/3.7/1.0 (BP=1.000, ratio=1.324, hyp_len=31137, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.14-23.07.3.21-24.78.pth
BLEU = 8.05, 35.1/14.8/5.1/1.6 (BP=1.000, ratio=1.142, hyp_len=26857, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.09-21.89.3.10-22.20.pth
BLEU = 9.04, 37.2/16.1/5.9/1.9 (BP=1.000, ratio=1.124, hyp_len=26421, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.2.90-18.17.3.01-20.25.pth
BLEU = 9.92, 37.5/16.8/6.5/2.3 (BP=1.000, ratio=1.149, hyp_len=27017, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.90-18.09.2.92-18.49.pth
BLEU = 11.37, 40.1/18.6/7.6/2.9 (BP=1.000, ratio=1.117, hyp_len=26269, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.80-16.42.2.83-17.02.pth
BLEU = 13.06, 43.2/20.7/8.9/3.7 (BP=1.000, ratio=1.071, hyp_len=25171, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.76-15.87.2.76-15.72.pth
BLEU = 12.80, 41.3/20.0/8.7/3.7 (BP=1.000, ratio=1.161, hyp_len=27296, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.66-14.28.2.69-14.70.pth
BLEU = 14.33, 43.8/21.7/9.9/4.5 (BP=1.000, ratio=1.112, hyp_len=26136, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.57-13.06.2.62-13.77.pth
BLEU = 15.82, 46.6/23.6/11.1/5.1 (BP=1.000, ratio=1.067, hyp_len=25079, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.56-12.88.2.56-12.98.pth
BLEU = 15.81, 45.3/23.4/11.3/5.2 (BP=1.000, ratio=1.129, hyp_len=26539, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.46-11.70.2.50-12.23.pth
BLEU = 16.25, 45.5/23.7/11.7/5.5 (BP=1.000, ratio=1.151, hyp_len=27056, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.39-10.89.2.44-11.48.pth
BLEU = 18.71, 50.2/26.8/13.6/6.7 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.44-11.49.2.39-10.93.pth
BLEU = 18.93, 49.3/26.8/13.9/7.0 (BP=1.000, ratio=1.100, hyp_len=25871, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.45-11.58.2.35-10.49.pth
BLEU = 19.92, 50.6/28.1/14.8/7.5 (BP=1.000, ratio=1.092, hyp_len=25667, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.31-10.07.2.28-9.78.pth
BLEU = 21.64, 53.3/29.9/16.1/8.6 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.26-9.56.2.24-9.36.pth
BLEU = 20.84, 50.7/28.6/15.5/8.4 (BP=1.000, ratio=1.121, hyp_len=26361, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.24-9.43.2.18-8.87.pth
BLEU = 22.74, 53.1/30.6/17.2/9.6 (BP=1.000, ratio=1.083, hyp_len=25464, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.23-9.30.2.14-8.51.pth
BLEU = 23.85, 54.5/31.9/18.2/10.2 (BP=1.000, ratio=1.065, hyp_len=25041, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.11-8.21.2.10-8.19.pth
BLEU = 24.61, 55.7/32.8/18.8/10.7 (BP=1.000, ratio=1.060, hyp_len=24921, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.09-8.11.2.05-7.81.pth
BLEU = 26.24, 57.1/34.4/20.2/12.0 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.01-7.48.2.01-7.47.pth
BLEU = 26.90, 58.0/35.2/20.8/12.3 (BP=1.000, ratio=1.043, hyp_len=24523, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.31.2.08-8.00.1.97-7.15.pth
BLEU = 27.34, 57.8/35.5/21.3/12.8 (BP=1.000, ratio=1.063, hyp_len=24998, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.32.2.05-7.74.1.93-6.89.pth
BLEU = 28.07, 58.7/36.4/21.9/13.3 (BP=1.000, ratio=1.058, hyp_len=24876, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.33.1.99-7.29.1.92-6.85.pth
BLEU = 26.83, 56.1/34.8/21.1/12.6 (BP=1.000, ratio=1.125, hyp_len=26453, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.34.2.02-7.52.1.86-6.43.pth
BLEU = 29.83, 60.2/38.2/23.6/14.6 (BP=1.000, ratio=1.049, hyp_len=24660, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.35.1.90-6.70.1.83-6.21.pth
BLEU = 31.37, 61.7/39.7/25.1/15.8 (BP=1.000, ratio=1.037, hyp_len=24375, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.36.1.92-6.83.1.79-5.96.pth
BLEU = 32.55, 62.8/40.8/26.1/16.8 (BP=1.000, ratio=1.027, hyp_len=24132, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.37.1.94-6.97.1.76-5.81.pth
BLEU = 31.20, 60.3/39.1/25.0/16.1 (BP=1.000, ratio=1.086, hyp_len=25540, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.38.1.78-5.95.1.72-5.58.pth
BLEU = 32.65, 61.8/40.7/26.3/17.1 (BP=1.000, ratio=1.072, hyp_len=25208, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth
BLEU = 34.17, 63.5/42.3/27.8/18.3 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.40.1.83-6.23.1.67-5.30.pth
BLEU = 32.17, 60.3/40.0/26.1/17.0 (BP=1.000, ratio=1.116, hyp_len=26239, ref_len=23509)

real	27m27.535s
user	27m1.923s
sys	0m51.476s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-40epoch$
```

transformer, 40 epoch, rk-my မော်ဒယ်ရဲ့ အကောင်းဆုံး BLEU က  

```
Evaluation result for the model: rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth
BLEU = 34.17, 63.5/42.3/27.8/18.3 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
```

### Transformer, rk-my, 50 epoch

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 50 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.pth',
    'n_epochs': 50,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.54e+05 loss=5.7499e+00 ppl=314.17                                                
Validation - loss=5.7633e+00 ppl=318.40 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.23e+02 |g_param|=3.22e+05 loss=4.9872e+00 ppl=146.52                                                
Validation - loss=5.0249e+00 ppl=152.16 best_loss=5.7633e+00 best_ppl=318.40                                            
Epoch 3 - |param|=3.23e+02 |g_param|=2.60e+05 loss=4.5560e+00 ppl=95.21                                                 
Validation - loss=4.6290e+00 ppl=102.41 best_loss=5.0249e+00 best_ppl=152.16                                            
Epoch 4 - |param|=3.23e+02 |g_param|=2.08e+05 loss=4.2310e+00 ppl=68.79                                                 
Validation - loss=4.3469e+00 ppl=77.24 best_loss=4.6290e+00 best_ppl=102.41                                             
Epoch 5 - |param|=3.23e+02 |g_param|=1.81e+05 loss=4.0044e+00 ppl=54.84                                                 
Validation - loss=4.1098e+00 ppl=60.93 best_loss=4.3469e+00 best_ppl=77.24                                              
Epoch 6 - |param|=3.23e+02 |g_param|=2.03e+05 loss=3.7988e+00 ppl=44.65                                                 
Validation - loss=3.8936e+00 ppl=49.09 best_loss=4.1098e+00 best_ppl=60.93                                              
Epoch 7 - |param|=3.24e+02 |g_param|=2.33e+05 loss=3.6454e+00 ppl=38.30                                                 
Validation - loss=3.7232e+00 ppl=41.40 best_loss=3.8936e+00 best_ppl=49.09                                              
Epoch 8 - |param|=3.24e+02 |g_param|=1.81e+05 loss=3.5177e+00 ppl=33.71                                                 
Validation - loss=3.5598e+00 ppl=35.16 best_loss=3.7232e+00 best_ppl=41.40                                              
Epoch 9 - |param|=3.24e+02 |g_param|=2.05e+05 loss=3.3163e+00 ppl=27.56                                                 
Validation - loss=3.4129e+00 ppl=30.35 best_loss=3.5598e+00 best_ppl=35.16                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.85e+05 loss=3.2522e+00 ppl=25.85                                                
Validation - loss=3.2781e+00 ppl=26.53 best_loss=3.4129e+00 best_ppl=30.35                                              
Epoch 11 - |param|=3.24e+02 |g_param|=1.86e+05 loss=3.0936e+00 ppl=22.06                                                
Validation - loss=3.1599e+00 ppl=23.57 best_loss=3.2781e+00 best_ppl=26.53                                              
Epoch 12 - |param|=3.24e+02 |g_param|=1.93e+05 loss=3.0411e+00 ppl=20.93                                                
Validation - loss=3.0545e+00 ppl=21.21 best_loss=3.1599e+00 best_ppl=23.57                                              
Epoch 13 - |param|=3.24e+02 |g_param|=2.08e+05 loss=2.9000e+00 ppl=18.17                                                
Validation - loss=2.9571e+00 ppl=19.24 best_loss=3.0545e+00 best_ppl=21.21                                              
Epoch 14 - |param|=3.24e+02 |g_param|=2.49e+05 loss=2.8660e+00 ppl=17.57                                                
Validation - loss=2.8743e+00 ppl=17.71 best_loss=2.9571e+00 best_ppl=19.24                                              
Epoch 15 - |param|=3.24e+02 |g_param|=3.45e+05 loss=2.7838e+00 ppl=16.18                                                
Validation - loss=2.7857e+00 ppl=16.21 best_loss=2.8743e+00 best_ppl=17.71                                              
Epoch 16 - |param|=3.24e+02 |g_param|=3.28e+05 loss=2.6955e+00 ppl=14.81                                                
Validation - loss=2.7290e+00 ppl=15.32 best_loss=2.7857e+00 best_ppl=16.21                                              
Epoch 17 - |param|=3.24e+02 |g_param|=2.81e+05 loss=2.6384e+00 ppl=13.99                                                
Validation - loss=2.6505e+00 ppl=14.16 best_loss=2.7290e+00 best_ppl=15.32                                              
Epoch 18 - |param|=3.24e+02 |g_param|=3.09e+05 loss=2.6320e+00 ppl=13.90                                                
Validation - loss=2.5860e+00 ppl=13.28 best_loss=2.6505e+00 best_ppl=14.16                                              
Epoch 19 - |param|=3.24e+02 |g_param|=3.99e+05 loss=2.5436e+00 ppl=12.73                                                
Validation - loss=2.5264e+00 ppl=12.51 best_loss=2.5860e+00 best_ppl=13.28                                              
Epoch 20 - |param|=3.24e+02 |g_param|=4.69e+05 loss=2.5114e+00 ppl=12.32                                                
Validation - loss=2.4647e+00 ppl=11.76 best_loss=2.5264e+00 best_ppl=12.51                                              
Epoch 21 - |param|=3.24e+02 |g_param|=4.17e+05 loss=2.4073e+00 ppl=11.10                                                
Validation - loss=2.4102e+00 ppl=11.14 best_loss=2.4647e+00 best_ppl=11.76                                              
Epoch 22 - |param|=3.25e+02 |g_param|=4.01e+05 loss=2.3813e+00 ppl=10.82                                                
Validation - loss=2.3552e+00 ppl=10.54 best_loss=2.4102e+00 best_ppl=11.14                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.43e+05 loss=2.3575e+00 ppl=10.56                                                
Validation - loss=2.3003e+00 ppl=9.98 best_loss=2.3552e+00 best_ppl=10.54                                               
Epoch 24 - |param|=3.25e+02 |g_param|=4.62e+05 loss=2.2802e+00 ppl=9.78                                                 
Validation - loss=2.2554e+00 ppl=9.54 best_loss=2.3003e+00 best_ppl=9.98                                                
Epoch 25 - |param|=3.25e+02 |g_param|=4.43e+05 loss=2.3225e+00 ppl=10.20                                                
Validation - loss=2.1942e+00 ppl=8.97 best_loss=2.2554e+00 best_ppl=9.54                                                
Epoch 26 - |param|=3.25e+02 |g_param|=4.69e+05 loss=2.2266e+00 ppl=9.27                                                 
Validation - loss=2.1494e+00 ppl=8.58 best_loss=2.1942e+00 best_ppl=8.97                                                
Epoch 27 - |param|=3.25e+02 |g_param|=3.43e+05 loss=2.1684e+00 ppl=8.74                                                 
Validation - loss=2.1088e+00 ppl=8.24 best_loss=2.1494e+00 best_ppl=8.58                                                
Epoch 28 - |param|=3.25e+02 |g_param|=4.19e+05 loss=2.1809e+00 ppl=8.85                                                 
Validation - loss=2.0732e+00 ppl=7.95 best_loss=2.1088e+00 best_ppl=8.24                                                
Epoch 29 - |param|=3.25e+02 |g_param|=4.98e+05 loss=2.0924e+00 ppl=8.10                                                 
Validation - loss=2.0400e+00 ppl=7.69 best_loss=2.0732e+00 best_ppl=7.95                                                
Epoch 30 - |param|=3.25e+02 |g_param|=5.38e+05 loss=2.1119e+00 ppl=8.26                                                 
Validation - loss=2.0223e+00 ppl=7.56 best_loss=2.0400e+00 best_ppl=7.69                                                
Epoch 31 - |param|=3.25e+02 |g_param|=3.81e+05 loss=2.0161e+00 ppl=7.51                                                 
Validation - loss=1.9464e+00 ppl=7.00 best_loss=2.0223e+00 best_ppl=7.56                                                
Epoch 32 - |param|=3.25e+02 |g_param|=4.45e+05 loss=2.0132e+00 ppl=7.49                                                 
Validation - loss=1.9053e+00 ppl=6.72 best_loss=1.9464e+00 best_ppl=7.00                                                
Epoch 33 - |param|=3.25e+02 |g_param|=5.81e+05 loss=2.0094e+00 ppl=7.46                                                 
Validation - loss=1.8739e+00 ppl=6.51 best_loss=1.9053e+00 best_ppl=6.72                                                
Epoch 34 - |param|=3.25e+02 |g_param|=6.92e+05 loss=1.9444e+00 ppl=6.99                                                 
Validation - loss=1.8479e+00 ppl=6.35 best_loss=1.8739e+00 best_ppl=6.51                                                
Epoch 35 - |param|=3.25e+02 |g_param|=4.64e+05 loss=1.8694e+00 ppl=6.48                                                 
Validation - loss=1.7959e+00 ppl=6.02 best_loss=1.8479e+00 best_ppl=6.35                                                
Epoch 36 - |param|=3.25e+02 |g_param|=4.13e+05 loss=1.9358e+00 ppl=6.93                                                 
Validation - loss=1.7812e+00 ppl=5.94 best_loss=1.7959e+00 best_ppl=6.02                                                
Epoch 37 - |param|=3.25e+02 |g_param|=6.74e+05 loss=1.8470e+00 ppl=6.34                                                 
Validation - loss=1.7268e+00 ppl=5.62 best_loss=1.7812e+00 best_ppl=5.94                                                
Epoch 38 - |param|=3.25e+02 |g_param|=4.22e+05 loss=1.8512e+00 ppl=6.37                                                 
Validation - loss=1.7211e+00 ppl=5.59 best_loss=1.7268e+00 best_ppl=5.62                                                
Epoch 39 - |param|=3.25e+02 |g_param|=7.57e+05 loss=1.7396e+00 ppl=5.70                                                 
Validation - loss=1.6810e+00 ppl=5.37 best_loss=1.7211e+00 best_ppl=5.59                                                
Epoch 40 - |param|=3.25e+02 |g_param|=4.89e+05 loss=1.8391e+00 ppl=6.29                                                 
Validation - loss=1.6510e+00 ppl=5.21 best_loss=1.6810e+00 best_ppl=5.37                                                
Epoch 41 - |param|=3.25e+02 |g_param|=6.07e+05 loss=1.6976e+00 ppl=5.46                                                 
Validation - loss=1.6297e+00 ppl=5.10 best_loss=1.6510e+00 best_ppl=5.21                                                
Epoch 42 - |param|=3.25e+02 |g_param|=5.31e+05 loss=1.7753e+00 ppl=5.90                                                 
Validation - loss=1.6340e+00 ppl=5.12 best_loss=1.6297e+00 best_ppl=5.10                                                
Epoch 43 - |param|=3.25e+02 |g_param|=5.64e+05 loss=1.7304e+00 ppl=5.64                                                 
Validation - loss=1.5898e+00 ppl=4.90 best_loss=1.6297e+00 best_ppl=5.10                                                
Epoch 44 - |param|=3.25e+02 |g_param|=6.95e+05 loss=1.6924e+00 ppl=5.43                                                 
Validation - loss=1.5523e+00 ppl=4.72 best_loss=1.5898e+00 best_ppl=4.90                                                
Epoch 45 - |param|=3.25e+02 |g_param|=6.11e+05 loss=1.6438e+00 ppl=5.17                                                 
Validation - loss=1.5464e+00 ppl=4.69 best_loss=1.5523e+00 best_ppl=4.72                                                
Epoch 46 - |param|=3.25e+02 |g_param|=6.92e+05 loss=1.6232e+00 ppl=5.07                                                 
Validation - loss=1.5104e+00 ppl=4.53 best_loss=1.5464e+00 best_ppl=4.69                                                
Epoch 47 - |param|=3.25e+02 |g_param|=5.64e+05 loss=1.6050e+00 ppl=4.98                                                 
Validation - loss=1.5044e+00 ppl=4.50 best_loss=1.5104e+00 best_ppl=4.53                                                
Epoch 48 - |param|=3.25e+02 |g_param|=9.19e+05 loss=1.6133e+00 ppl=5.02                                                 
Validation - loss=1.4894e+00 ppl=4.43 best_loss=1.5044e+00 best_ppl=4.50                                                
Epoch 49 - |param|=3.25e+02 |g_param|=5.07e+05 loss=1.5518e+00 ppl=4.72                                                 
Validation - loss=1.4553e+00 ppl=4.29 best_loss=1.4894e+00 best_ppl=4.43                                                
Epoch 50 - |param|=3.25e+02 |g_param|=7.04e+05 loss=1.5784e+00 ppl=4.85                                                 
Validation - loss=1.4782e+00 ppl=4.38 best_loss=1.4553e+00 best_ppl=4.29                                                

real	26m36.189s
user	26m25.576s
sys	0m5.196s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.75-314.17.5.76-318.40.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 31.8/5.8/0.0/0.0 (BP=0.132, ratio=0.330, hyp_len=7763, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.4.99-146.52.5.02-152.16.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 33.0/9.3/0.0/0.0 (BP=0.209, ratio=0.390, hyp_len=9162, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.56-95.21.4.63-102.41.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 25.0/4.6/0.3/0.0 (BP=0.530, ratio=0.611, hyp_len=14373, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.23-68.79.4.35-77.24.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 26.6/5.7/0.4/0.0 (BP=0.811, ratio=0.827, hyp_len=19442, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.00-54.84.4.11-60.93.pth
BLEU = 1.85, 24.5/7.3/0.8/0.1 (BP=1.000, ratio=1.113, hyp_len=26154, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.80-44.65.3.89-49.09.pth
BLEU = 3.37, 29.3/9.6/1.7/0.3 (BP=1.000, ratio=1.030, hyp_len=24212, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.65-38.30.3.72-41.40.pth
BLEU = 3.88, 26.9/9.4/2.1/0.4 (BP=1.000, ratio=1.210, hyp_len=28454, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.52-33.71.3.56-35.16.pth
BLEU = 4.77, 27.9/10.5/2.7/0.6 (BP=1.000, ratio=1.276, hyp_len=29986, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.32-27.56.3.41-30.35.pth
BLEU = 6.86, 34.8/13.6/4.1/1.2 (BP=1.000, ratio=1.075, hyp_len=25265, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.25-25.85.3.28-26.53.pth
BLEU = 6.70, 32.0/12.9/4.1/1.2 (BP=1.000, ratio=1.225, hyp_len=28804, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.09-22.06.3.16-23.57.pth
BLEU = 7.85, 34.4/14.4/4.9/1.5 (BP=1.000, ratio=1.206, hyp_len=28356, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.04-20.93.3.05-21.21.pth
BLEU = 9.32, 37.9/16.5/6.0/2.0 (BP=1.000, ratio=1.129, hyp_len=26537, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.2.90-18.17.2.96-19.24.pth
BLEU = 10.99, 41.5/18.8/7.2/2.6 (BP=1.000, ratio=1.074, hyp_len=25254, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.87-17.57.2.87-17.71.pth
BLEU = 10.57, 38.2/17.6/7.0/2.6 (BP=1.000, ratio=1.216, hyp_len=28583, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.78-16.18.2.79-16.21.pth
BLEU = 13.66, 45.6/21.7/9.3/3.8 (BP=1.000, ratio=1.032, hyp_len=24258, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.70-14.81.2.73-15.32.pth
BLEU = 12.29, 40.7/19.5/8.4/3.4 (BP=1.000, ratio=1.200, hyp_len=28207, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.64-13.99.2.65-14.16.pth
BLEU = 14.40, 44.3/22.0/10.0/4.4 (BP=1.000, ratio=1.117, hyp_len=26262, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.63-13.90.2.59-13.28.pth
BLEU = 15.52, 46.1/23.4/10.8/5.0 (BP=1.000, ratio=1.100, hyp_len=25858, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.54-12.73.2.53-12.51.pth
BLEU = 16.66, 47.9/24.8/11.8/5.5 (BP=1.000, ratio=1.077, hyp_len=25315, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.51-12.32.2.46-11.76.pth
BLEU = 17.89, 49.1/26.1/12.8/6.3 (BP=1.000, ratio=1.070, hyp_len=25143, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.41-11.10.2.41-11.14.pth
BLEU = 17.88, 48.2/25.7/12.9/6.4 (BP=1.000, ratio=1.113, hyp_len=26155, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.38-10.82.2.36-10.54.pth
BLEU = 19.17, 50.5/27.2/13.9/7.1 (BP=1.000, ratio=1.074, hyp_len=25250, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.36-10.56.2.30-9.98.pth
BLEU = 20.76, 52.2/29.0/15.2/8.1 (BP=1.000, ratio=1.057, hyp_len=24846, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.28-9.78.2.26-9.54.pth
BLEU = 21.06, 52.1/29.2/15.5/8.3 (BP=1.000, ratio=1.082, hyp_len=25434, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.32-10.20.2.19-8.97.pth
BLEU = 22.41, 53.9/30.7/16.7/9.2 (BP=1.000, ratio=1.066, hyp_len=25049, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.23-9.27.2.15-8.58.pth
BLEU = 23.74, 55.2/32.1/17.9/10.0 (BP=1.000, ratio=1.057, hyp_len=24858, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.17-8.74.2.11-8.24.pth
BLEU = 24.52, 55.5/32.8/18.6/10.7 (BP=1.000, ratio=1.071, hyp_len=25179, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.18-8.85.2.07-7.95.pth
BLEU = 24.15, 54.1/32.2/18.3/10.6 (BP=1.000, ratio=1.115, hyp_len=26209, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.09-8.10.2.04-7.69.pth
BLEU = 24.40, 53.6/32.3/18.8/10.9 (BP=1.000, ratio=1.138, hyp_len=26753, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.11-8.26.2.02-7.56.pth
BLEU = 25.74, 55.9/34.0/19.9/11.6 (BP=1.000, ratio=1.104, hyp_len=25950, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.31.2.02-7.51.1.95-7.00.pth
BLEU = 27.92, 58.5/36.2/21.8/13.2 (BP=1.000, ratio=1.061, hyp_len=24949, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.32.2.01-7.49.1.91-6.72.pth
BLEU = 29.01, 59.1/37.1/22.8/14.1 (BP=1.000, ratio=1.062, hyp_len=24972, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.33.2.01-7.46.1.87-6.51.pth
BLEU = 28.32, 57.3/36.1/22.3/13.9 (BP=1.000, ratio=1.117, hyp_len=26262, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.34.1.94-6.99.1.85-6.35.pth
BLEU = 30.27, 60.9/38.7/23.9/14.9 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.35.1.87-6.48.1.80-6.02.pth
BLEU = 32.30, 62.3/40.3/25.8/16.8 (BP=1.000, ratio=1.036, hyp_len=24357, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.36.1.94-6.93.1.78-5.94.pth
BLEU = 31.36, 61.1/39.7/25.1/15.9 (BP=1.000, ratio=1.077, hyp_len=25318, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.37.1.85-6.34.1.73-5.62.pth
BLEU = 33.93, 63.5/41.9/27.4/18.2 (BP=1.000, ratio=1.040, hyp_len=24448, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.38.1.85-6.37.1.72-5.59.pth
BLEU = 33.33, 63.1/41.7/26.8/17.5 (BP=1.000, ratio=1.060, hyp_len=24911, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.39.1.74-5.70.1.68-5.37.pth
BLEU = 32.20, 59.9/39.8/26.1/17.3 (BP=1.000, ratio=1.128, hyp_len=26517, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.40.1.84-6.29.1.65-5.21.pth
BLEU = 34.86, 63.7/42.9/28.5/19.0 (BP=1.000, ratio=1.065, hyp_len=25045, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.41.1.70-5.46.1.63-5.10.pth
BLEU = 36.16, 65.2/44.3/29.6/19.9 (BP=1.000, ratio=1.044, hyp_len=24534, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.42.1.78-5.90.1.63-5.12.pth
BLEU = 35.34, 64.3/43.6/29.0/19.2 (BP=1.000, ratio=1.071, hyp_len=25180, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.43.1.73-5.64.1.59-4.90.pth
BLEU = 37.12, 65.9/45.3/30.6/20.8 (BP=1.000, ratio=1.053, hyp_len=24757, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.44.1.69-5.43.1.55-4.72.pth
BLEU = 37.94, 66.7/46.0/31.4/21.5 (BP=1.000, ratio=1.048, hyp_len=24649, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.45.1.64-5.17.1.55-4.69.pth
BLEU = 37.39, 65.8/45.7/31.0/21.0 (BP=1.000, ratio=1.069, hyp_len=25140, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth
BLEU = 40.40, 68.8/48.5/33.7/23.7 (BP=1.000, ratio=1.025, hyp_len=24088, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.47.1.61-4.98.1.50-4.50.pth
BLEU = 39.08, 67.6/47.4/32.5/22.4 (BP=1.000, ratio=1.046, hyp_len=24589, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.48.1.61-5.02.1.49-4.43.pth
BLEU = 37.94, 65.4/46.0/31.6/21.8 (BP=1.000, ratio=1.094, hyp_len=25728, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.49.1.55-4.72.1.46-4.29.pth
BLEU = 39.60, 67.5/47.9/33.2/22.9 (BP=1.000, ratio=1.064, hyp_len=25018, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.50.1.58-4.85.1.48-4.38.pth
BLEU = 38.51, 66.3/46.8/32.1/22.1 (BP=1.000, ratio=1.086, hyp_len=25526, ref_len=23509)

real	31m52.746s
user	31m21.749s
sys	1m4.008s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-50epoch$
```

Transformer, rk-my, 50 epoch model ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth
BLEU = 40.40, 68.8/48.5/33.7/23.7 (BP=1.000, ratio=1.025, hyp_len=24088, ref_len=23509)
```

### Transformer model, rk-my, 60 epoch

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 60 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.pth',
    'n_epochs': 60,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.39e+05 loss=5.8393e+00 ppl=343.54                                                
Validation - loss=5.8306e+00 ppl=340.57 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.35e+05 loss=4.9837e+00 ppl=146.01                                                
Validation - loss=5.0185e+00 ppl=151.18 best_loss=5.8306e+00 best_ppl=340.57                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.51e+05 loss=4.5133e+00 ppl=91.23                                                 
Validation - loss=4.6229e+00 ppl=101.79 best_loss=5.0185e+00 best_ppl=151.18                                            
Epoch 4 - |param|=3.24e+02 |g_param|=2.18e+05 loss=4.2208e+00 ppl=68.09                                                 
Validation - loss=4.3508e+00 ppl=77.54 best_loss=4.6229e+00 best_ppl=101.79                                             
Epoch 5 - |param|=3.24e+02 |g_param|=2.03e+05 loss=4.0368e+00 ppl=56.64                                                 
Validation - loss=4.1181e+00 ppl=61.44 best_loss=4.3508e+00 best_ppl=77.54                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.78e+05 loss=3.7808e+00 ppl=43.85                                                 
Validation - loss=3.9090e+00 ppl=49.85 best_loss=4.1181e+00 best_ppl=61.44                                              
Epoch 7 - |param|=3.24e+02 |g_param|=2.03e+05 loss=3.6291e+00 ppl=37.68                                                 
Validation - loss=3.7280e+00 ppl=41.59 best_loss=3.9090e+00 best_ppl=49.85                                              
Epoch 8 - |param|=3.24e+02 |g_param|=2.11e+05 loss=3.5262e+00 ppl=33.99                                                 
Validation - loss=3.5716e+00 ppl=35.57 best_loss=3.7280e+00 best_ppl=41.59                                              
Epoch 9 - |param|=3.24e+02 |g_param|=2.34e+05 loss=3.3607e+00 ppl=28.81                                                 
Validation - loss=3.4226e+00 ppl=30.65 best_loss=3.5716e+00 best_ppl=35.57                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.81e+05 loss=3.1962e+00 ppl=24.44                                                
Validation - loss=3.2965e+00 ppl=27.02 best_loss=3.4226e+00 best_ppl=30.65                                              
Epoch 11 - |param|=3.24e+02 |g_param|=2.02e+05 loss=3.1435e+00 ppl=23.19                                                
Validation - loss=3.1815e+00 ppl=24.08 best_loss=3.2965e+00 best_ppl=27.02                                              
Epoch 12 - |param|=3.25e+02 |g_param|=2.01e+05 loss=3.0025e+00 ppl=20.13                                                
Validation - loss=3.0789e+00 ppl=21.74 best_loss=3.1815e+00 best_ppl=24.08                                              
Epoch 13 - |param|=3.25e+02 |g_param|=2.86e+05 loss=2.9709e+00 ppl=19.51                                                
Validation - loss=2.9879e+00 ppl=19.84 best_loss=3.0789e+00 best_ppl=21.74                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.34e+05 loss=2.8068e+00 ppl=16.56                                                
Validation - loss=2.9052e+00 ppl=18.27 best_loss=2.9879e+00 best_ppl=19.84                                              
Epoch 15 - |param|=3.25e+02 |g_param|=2.11e+05 loss=2.8380e+00 ppl=17.08                                                
Validation - loss=2.8329e+00 ppl=16.99 best_loss=2.9052e+00 best_ppl=18.27                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.31e+05 loss=2.7984e+00 ppl=16.42                                                
Validation - loss=2.7580e+00 ppl=15.77 best_loss=2.8329e+00 best_ppl=16.99                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.39e+05 loss=2.7078e+00 ppl=15.00                                                
Validation - loss=2.6964e+00 ppl=14.83 best_loss=2.7580e+00 best_ppl=15.77                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.39e+05 loss=2.6284e+00 ppl=13.85                                                
Validation - loss=2.6345e+00 ppl=13.94 best_loss=2.6964e+00 best_ppl=14.83                                              
Epoch 19 - |param|=3.25e+02 |g_param|=3.77e+05 loss=2.5938e+00 ppl=13.38                                                
Validation - loss=2.5815e+00 ppl=13.22 best_loss=2.6345e+00 best_ppl=13.94                                              
Epoch 20 - |param|=3.25e+02 |g_param|=2.63e+05 loss=2.4477e+00 ppl=11.56                                                
Validation - loss=2.5160e+00 ppl=12.38 best_loss=2.5815e+00 best_ppl=13.22                                              
Epoch 21 - |param|=3.25e+02 |g_param|=2.96e+05 loss=2.4971e+00 ppl=12.15                                                
Validation - loss=2.4544e+00 ppl=11.64 best_loss=2.5160e+00 best_ppl=12.38                                              
Epoch 22 - |param|=3.25e+02 |g_param|=3.33e+05 loss=2.4598e+00 ppl=11.70                                                
Validation - loss=2.4028e+00 ppl=11.05 best_loss=2.4544e+00 best_ppl=11.64                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.23e+05 loss=2.3665e+00 ppl=10.66                                                
Validation - loss=2.3489e+00 ppl=10.47 best_loss=2.4028e+00 best_ppl=11.05                                              
Epoch 24 - |param|=3.25e+02 |g_param|=2.99e+05 loss=2.2451e+00 ppl=9.44                                                 
Validation - loss=2.3011e+00 ppl=9.99 best_loss=2.3489e+00 best_ppl=10.47                                               
Epoch 25 - |param|=3.25e+02 |g_param|=3.69e+05 loss=2.2032e+00 ppl=9.05                                                 
Validation - loss=2.2519e+00 ppl=9.51 best_loss=2.3011e+00 best_ppl=9.99                                                
Epoch 26 - |param|=3.25e+02 |g_param|=4.65e+05 loss=2.2256e+00 ppl=9.26                                                 
Validation - loss=2.2012e+00 ppl=9.04 best_loss=2.2519e+00 best_ppl=9.51                                                
Epoch 27 - |param|=3.25e+02 |g_param|=5.14e+05 loss=2.2382e+00 ppl=9.38                                                 
Validation - loss=2.1542e+00 ppl=8.62 best_loss=2.2012e+00 best_ppl=9.04                                                
Epoch 28 - |param|=3.25e+02 |g_param|=4.47e+05 loss=2.1582e+00 ppl=8.66                                                 
Validation - loss=2.1126e+00 ppl=8.27 best_loss=2.1542e+00 best_ppl=8.62                                                
Epoch 29 - |param|=3.25e+02 |g_param|=4.20e+05 loss=2.1571e+00 ppl=8.65                                                 
Validation - loss=2.0699e+00 ppl=7.92 best_loss=2.1126e+00 best_ppl=8.27                                                
Epoch 30 - |param|=3.25e+02 |g_param|=3.64e+05 loss=2.0831e+00 ppl=8.03                                                 
Validation - loss=2.0341e+00 ppl=7.65 best_loss=2.0699e+00 best_ppl=7.92                                                
Epoch 31 - |param|=3.25e+02 |g_param|=4.60e+05 loss=2.0955e+00 ppl=8.13                                                 
Validation - loss=1.9780e+00 ppl=7.23 best_loss=2.0341e+00 best_ppl=7.65                                                
Epoch 32 - |param|=3.25e+02 |g_param|=4.18e+05 loss=2.0991e+00 ppl=8.16                                                 
Validation - loss=1.9565e+00 ppl=7.07 best_loss=1.9780e+00 best_ppl=7.23                                                
Epoch 33 - |param|=3.25e+02 |g_param|=4.10e+05 loss=1.9552e+00 ppl=7.06                                                 
Validation - loss=1.9262e+00 ppl=6.86 best_loss=1.9565e+00 best_ppl=7.07                                                
Epoch 34 - |param|=3.25e+02 |g_param|=3.77e+05 loss=1.9840e+00 ppl=7.27                                                 
Validation - loss=1.8821e+00 ppl=6.57 best_loss=1.9262e+00 best_ppl=6.86                                                
Epoch 35 - |param|=3.25e+02 |g_param|=3.66e+05 loss=1.9557e+00 ppl=7.07                                                 
Validation - loss=1.8284e+00 ppl=6.22 best_loss=1.8821e+00 best_ppl=6.57                                                
Epoch 36 - |param|=3.25e+02 |g_param|=3.68e+05 loss=1.9151e+00 ppl=6.79                                                 
Validation - loss=1.8072e+00 ppl=6.09 best_loss=1.8284e+00 best_ppl=6.22                                                
Epoch 37 - |param|=3.25e+02 |g_param|=4.95e+05 loss=1.8935e+00 ppl=6.64                                                 
Validation - loss=1.7796e+00 ppl=5.93 best_loss=1.8072e+00 best_ppl=6.09                                                
Epoch 38 - |param|=3.25e+02 |g_param|=5.35e+05 loss=1.8650e+00 ppl=6.46                                                 
Validation - loss=1.7462e+00 ppl=5.73 best_loss=1.7796e+00 best_ppl=5.93                                                
Epoch 39 - |param|=3.25e+02 |g_param|=4.93e+05 loss=1.8961e+00 ppl=6.66                                                 
Validation - loss=1.6973e+00 ppl=5.46 best_loss=1.7462e+00 best_ppl=5.73                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.00e+05 loss=1.7736e+00 ppl=5.89                                                 
Validation - loss=1.6773e+00 ppl=5.35 best_loss=1.6973e+00 best_ppl=5.46                                                
Epoch 41 - |param|=3.26e+02 |g_param|=6.18e+05 loss=1.8287e+00 ppl=6.23                                                 
Validation - loss=1.6453e+00 ppl=5.18 best_loss=1.6773e+00 best_ppl=5.35                                                
Epoch 42 - |param|=3.26e+02 |g_param|=5.52e+05 loss=1.7868e+00 ppl=5.97                                                 
Validation - loss=1.6186e+00 ppl=5.05 best_loss=1.6453e+00 best_ppl=5.18                                                
Epoch 43 - |param|=3.26e+02 |g_param|=5.85e+05 loss=1.7477e+00 ppl=5.74                                                 
Validation - loss=1.5994e+00 ppl=4.95 best_loss=1.6186e+00 best_ppl=5.05                                                
Epoch 44 - |param|=3.26e+02 |g_param|=4.35e+05 loss=1.6815e+00 ppl=5.37                                                 
Validation - loss=1.5652e+00 ppl=4.78 best_loss=1.5994e+00 best_ppl=4.95                                                
Epoch 45 - |param|=3.26e+02 |g_param|=4.27e+05 loss=1.6136e+00 ppl=5.02                                                 
Validation - loss=1.5502e+00 ppl=4.71 best_loss=1.5652e+00 best_ppl=4.78                                                
Epoch 46 - |param|=3.26e+02 |g_param|=7.60e+05 loss=1.6526e+00 ppl=5.22                                                 
Validation - loss=1.5318e+00 ppl=4.63 best_loss=1.5502e+00 best_ppl=4.71                                                
Epoch 47 - |param|=3.26e+02 |g_param|=3.73e+05 loss=1.5845e+00 ppl=4.88                                                 
Validation - loss=1.4942e+00 ppl=4.46 best_loss=1.5318e+00 best_ppl=4.63                                                
Epoch 48 - |param|=3.26e+02 |g_param|=5.27e+05 loss=1.6337e+00 ppl=5.12                                                 
Validation - loss=1.4754e+00 ppl=4.37 best_loss=1.4942e+00 best_ppl=4.46                                                
Epoch 49 - |param|=3.26e+02 |g_param|=4.75e+05 loss=1.6354e+00 ppl=5.13                                                 
Validation - loss=1.4603e+00 ppl=4.31 best_loss=1.4754e+00 best_ppl=4.37                                                
Epoch 50 - |param|=3.26e+02 |g_param|=7.13e+05 loss=1.6678e+00 ppl=5.30                                                 
Validation - loss=1.4361e+00 ppl=4.20 best_loss=1.4603e+00 best_ppl=4.31                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.01e+05 loss=1.5651e+00 ppl=4.78                                                 
Validation - loss=1.4205e+00 ppl=4.14 best_loss=1.4361e+00 best_ppl=4.20                                                
Epoch 52 - |param|=3.26e+02 |g_param|=6.92e+05 loss=1.5164e+00 ppl=4.56                                                 
Validation - loss=1.4224e+00 ppl=4.15 best_loss=1.4205e+00 best_ppl=4.14                                                
Epoch 53 - |param|=3.26e+02 |g_param|=5.72e+05 loss=1.5156e+00 ppl=4.55                                                 
Validation - loss=1.3838e+00 ppl=3.99 best_loss=1.4205e+00 best_ppl=4.14                                                
Epoch 54 - |param|=3.26e+02 |g_param|=9.13e+05 loss=1.5245e+00 ppl=4.59                                                 
Validation - loss=1.3646e+00 ppl=3.91 best_loss=1.3838e+00 best_ppl=3.99                                                
Epoch 55 - |param|=3.26e+02 |g_param|=8.19e+05 loss=1.4387e+00 ppl=4.22                                                 
Validation - loss=1.3488e+00 ppl=3.85 best_loss=1.3646e+00 best_ppl=3.91                                                
Epoch 56 - |param|=3.26e+02 |g_param|=5.43e+05 loss=1.4404e+00 ppl=4.22                                                 
Validation - loss=1.3462e+00 ppl=3.84 best_loss=1.3488e+00 best_ppl=3.85                                                
Epoch 57 - |param|=3.26e+02 |g_param|=6.48e+05 loss=1.4429e+00 ppl=4.23                                                 
Validation - loss=1.3214e+00 ppl=3.75 best_loss=1.3462e+00 best_ppl=3.84                                                
Epoch 58 - |param|=3.26e+02 |g_param|=5.01e+05 loss=1.5061e+00 ppl=4.51                                                 
Validation - loss=1.3136e+00 ppl=3.72 best_loss=1.3214e+00 best_ppl=3.75                                                
Epoch 59 - |param|=3.26e+02 |g_param|=7.52e+05 loss=1.4612e+00 ppl=4.31                                                 
Validation - loss=1.3200e+00 ppl=3.74 best_loss=1.3136e+00 best_ppl=3.72                                                
Epoch 60 - |param|=3.26e+02 |g_param|=7.32e+05 loss=1.4078e+00 ppl=4.09                                                 
Validation - loss=1.2961e+00 ppl=3.66 best_loss=1.3136e+00 best_ppl=3.72                                                

real	31m6.354s
user	30m59.308s
sys	0m5.774s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.84-343.54.5.83-340.57.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 11.9/0.0/0.0/0.0 (BP=0.683, ratio=0.724, hyp_len=17016, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.4.98-146.01.5.02-151.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.5/1.5/0.0/0.0 (BP=0.525, ratio=0.608, hyp_len=14295, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.51-91.23.4.62-101.79.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 7.4/0.5/0.0/0.0 (BP=1.000, ratio=2.446, hyp_len=57506, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.22-68.09.4.35-77.54.pth
BLEU = 1.08, 29.1/6.9/0.4/0.0 (BP=0.849, ratio=0.859, hyp_len=20205, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.04-56.64.4.12-61.44.pth
BLEU = 2.68, 31.0/9.8/1.3/0.2 (BP=0.860, ratio=0.869, hyp_len=20428, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.78-43.85.3.91-49.85.pth
BLEU = 3.75, 27.7/9.5/1.8/0.4 (BP=1.000, ratio=1.055, hyp_len=24799, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.63-37.68.3.73-41.59.pth
BLEU = 3.86, 26.2/9.3/2.0/0.5 (BP=1.000, ratio=1.225, hyp_len=28810, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.53-33.99.3.57-35.57.pth
BLEU = 4.00, 23.8/9.0/2.2/0.5 (BP=1.000, ratio=1.469, hyp_len=34540, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.36-28.81.3.42-30.65.pth
BLEU = 4.58, 24.4/9.6/2.7/0.7 (BP=1.000, ratio=1.493, hyp_len=35103, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.20-24.44.3.30-27.02.pth
BLEU = 5.83, 29.2/12.0/3.6/0.9 (BP=1.000, ratio=1.300, hyp_len=30558, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.14-23.19.3.18-24.08.pth
BLEU = 7.97, 35.9/15.3/5.0/1.5 (BP=1.000, ratio=1.115, hyp_len=26220, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.00-20.13.3.08-21.74.pth
BLEU = 7.88, 34.0/14.6/5.1/1.5 (BP=1.000, ratio=1.224, hyp_len=28776, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.2.97-19.51.2.99-19.84.pth
BLEU = 7.85, 32.4/14.2/5.2/1.6 (BP=1.000, ratio=1.346, hyp_len=31639, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.81-16.56.2.91-18.27.pth
BLEU = 10.11, 38.9/17.6/6.8/2.2 (BP=1.000, ratio=1.147, hyp_len=26969, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.84-17.08.2.83-16.99.pth
BLEU = 10.74, 39.1/18.1/7.3/2.6 (BP=1.000, ratio=1.181, hyp_len=27771, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.80-16.42.2.76-15.77.pth
BLEU = 12.57, 42.3/20.2/8.6/3.4 (BP=1.000, ratio=1.130, hyp_len=26569, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.71-15.00.2.70-14.83.pth
BLEU = 13.78, 43.6/21.5/9.6/4.0 (BP=1.000, ratio=1.123, hyp_len=26404, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.63-13.85.2.63-13.94.pth
BLEU = 15.61, 47.0/23.7/11.0/4.9 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.59-13.38.2.58-13.22.pth
BLEU = 16.16, 47.4/24.1/11.5/5.2 (BP=1.000, ratio=1.071, hyp_len=25184, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.45-11.56.2.52-12.38.pth
BLEU = 16.04, 45.8/23.6/11.4/5.4 (BP=1.000, ratio=1.138, hyp_len=26747, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.50-12.15.2.45-11.64.pth
BLEU = 16.92, 46.9/24.6/12.1/5.9 (BP=1.000, ratio=1.127, hyp_len=26504, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.46-11.70.2.40-11.05.pth
BLEU = 19.26, 51.0/27.5/14.0/7.0 (BP=1.000, ratio=1.054, hyp_len=24786, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.37-10.66.2.35-10.47.pth
BLEU = 19.11, 50.2/27.3/13.9/7.0 (BP=1.000, ratio=1.092, hyp_len=25682, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.25-9.44.2.30-9.99.pth
BLEU = 21.18, 53.2/29.6/15.6/8.2 (BP=1.000, ratio=1.041, hyp_len=24477, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.20-9.05.2.25-9.51.pth
BLEU = 20.98, 51.9/29.2/15.5/8.2 (BP=1.000, ratio=1.086, hyp_len=25528, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.23-9.26.2.20-9.04.pth
BLEU = 22.89, 54.7/31.3/17.1/9.4 (BP=1.000, ratio=1.041, hyp_len=24474, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.24-9.38.2.15-8.62.pth
BLEU = 21.92, 51.7/29.7/16.5/9.1 (BP=1.000, ratio=1.125, hyp_len=26450, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.16-8.66.2.11-8.27.pth
BLEU = 22.42, 52.1/30.4/16.9/9.4 (BP=1.000, ratio=1.127, hyp_len=26498, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.16-8.65.2.07-7.92.pth
BLEU = 25.36, 56.9/33.8/19.3/11.1 (BP=1.000, ratio=1.035, hyp_len=24339, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.08-8.03.2.03-7.65.pth
BLEU = 25.47, 55.9/33.7/19.6/11.4 (BP=1.000, ratio=1.078, hyp_len=25352, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.31.2.10-8.13.1.98-7.23.pth
BLEU = 26.47, 57.1/34.8/20.5/12.0 (BP=1.000, ratio=1.070, hyp_len=25156, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.32.2.10-8.16.1.96-7.07.pth
BLEU = 26.25, 55.5/34.2/20.4/12.2 (BP=1.000, ratio=1.124, hyp_len=26435, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.33.1.96-7.06.1.93-6.86.pth
BLEU = 26.34, 54.9/34.1/20.6/12.4 (BP=1.000, ratio=1.152, hyp_len=27077, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.34.1.98-7.27.1.88-6.57.pth
BLEU = 29.34, 59.9/37.6/23.1/14.3 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.35.1.96-7.07.1.83-6.22.pth
BLEU = 30.37, 60.3/38.5/24.2/15.1 (BP=1.000, ratio=1.069, hyp_len=25120, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.36.1.92-6.79.1.81-6.09.pth
BLEU = 30.47, 59.7/38.4/24.3/15.5 (BP=1.000, ratio=1.093, hyp_len=25687, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.37.1.89-6.64.1.78-5.93.pth
BLEU = 31.96, 61.6/40.2/25.7/16.4 (BP=1.000, ratio=1.067, hyp_len=25095, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.38.1.86-6.46.1.75-5.73.pth
BLEU = 32.18, 61.6/40.4/25.9/16.6 (BP=1.000, ratio=1.079, hyp_len=25375, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.39.1.90-6.66.1.70-5.46.pth
BLEU = 34.80, 64.2/42.8/28.2/18.9 (BP=1.000, ratio=1.038, hyp_len=24400, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.40.1.77-5.89.1.68-5.35.pth
BLEU = 36.40, 66.4/44.6/29.7/20.0 (BP=1.000, ratio=1.007, hyp_len=23680, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.41.1.83-6.23.1.65-5.18.pth
BLEU = 35.92, 65.1/44.0/29.4/19.8 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.42.1.79-5.97.1.62-5.05.pth
BLEU = 35.23, 63.3/43.0/28.8/19.6 (BP=1.000, ratio=1.075, hyp_len=25268, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.43.1.75-5.74.1.60-4.95.pth
BLEU = 36.85, 65.5/44.9/30.3/20.7 (BP=1.000, ratio=1.043, hyp_len=24521, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.44.1.68-5.37.1.57-4.78.pth
BLEU = 36.83, 64.9/44.7/30.4/20.9 (BP=1.000, ratio=1.066, hyp_len=25049, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.45.1.61-5.02.1.55-4.71.pth
BLEU = 38.65, 67.0/46.8/32.0/22.3 (BP=1.000, ratio=1.036, hyp_len=24350, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.46.1.65-5.22.1.53-4.63.pth
BLEU = 40.23, 68.5/48.2/33.5/23.7 (BP=1.000, ratio=1.019, hyp_len=23960, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.47.1.58-4.88.1.49-4.46.pth
BLEU = 38.77, 66.3/46.6/32.3/22.6 (BP=1.000, ratio=1.064, hyp_len=25021, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.48.1.63-5.12.1.48-4.37.pth
BLEU = 40.37, 68.0/48.3/33.8/23.9 (BP=1.000, ratio=1.041, hyp_len=24462, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.49.1.64-5.13.1.46-4.31.pth
BLEU = 41.47, 68.8/49.2/34.9/25.0 (BP=1.000, ratio=1.035, hyp_len=24327, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.50.1.67-5.30.1.44-4.20.pth
BLEU = 41.64, 69.1/49.7/35.2/24.9 (BP=1.000, ratio=1.042, hyp_len=24502, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.51.1.57-4.78.1.42-4.14.pth
BLEU = 41.53, 68.3/49.2/35.1/25.3 (BP=1.000, ratio=1.059, hyp_len=24888, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.52.1.52-4.56.1.42-4.15.pth
BLEU = 41.74, 69.1/49.9/35.2/25.0 (BP=1.000, ratio=1.044, hyp_len=24554, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.53.1.52-4.55.1.38-3.99.pth
BLEU = 42.21, 68.6/49.9/35.8/25.9 (BP=1.000, ratio=1.067, hyp_len=25089, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.54.1.52-4.59.1.36-3.91.pth
BLEU = 43.99, 70.6/51.8/37.4/27.3 (BP=1.000, ratio=1.036, hyp_len=24365, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.55.1.44-4.22.1.35-3.85.pth
BLEU = 43.42, 69.7/51.0/37.0/27.0 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth
BLEU = 45.70, 71.8/53.2/39.1/29.2 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.57.1.44-4.23.1.32-3.75.pth
BLEU = 42.15, 67.5/49.6/36.0/26.2 (BP=1.000, ratio=1.104, hyp_len=25960, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.58.1.51-4.51.1.31-3.72.pth
BLEU = 45.36, 71.6/53.2/38.8/28.6 (BP=1.000, ratio=1.038, hyp_len=24402, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.59.1.46-4.31.1.32-3.74.pth
BLEU = 43.07, 69.1/51.0/36.8/26.5 (BP=1.000, ratio=1.083, hyp_len=25449, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.60.1.41-4.09.1.30-3.66.pth
BLEU = 44.65, 70.5/52.5/38.3/28.0 (BP=1.000, ratio=1.068, hyp_len=25104, ref_len=23509)

real	41m47.601s
user	41m6.632s
sys	1m18.819s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-60epoch$
```

Transformer, rk-my, 60 epoch ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth
BLEU = 45.70, 71.8/53.2/39.1/29.2 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
```

### Transformer, rk-my, 70 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 70 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.pth',
    'n_epochs': 70,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.62e+05 loss=5.8151e+00 ppl=335.32                                                
Validation - loss=5.7981e+00 ppl=329.67 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.45e+05 loss=5.0106e+00 ppl=149.99                                                
Validation - loss=5.0313e+00 ppl=153.13 best_loss=5.7981e+00 best_ppl=329.67                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.57e+05 loss=4.5198e+00 ppl=91.81                                                 
Validation - loss=4.6166e+00 ppl=101.15 best_loss=5.0313e+00 best_ppl=153.13                                            
Epoch 4 - |param|=3.24e+02 |g_param|=2.06e+05 loss=4.2411e+00 ppl=69.48                                                 
Validation - loss=4.3533e+00 ppl=77.73 best_loss=4.6166e+00 best_ppl=101.15                                             
Epoch 5 - |param|=3.24e+02 |g_param|=1.70e+05 loss=4.0669e+00 ppl=58.37                                                 
Validation - loss=4.1328e+00 ppl=62.35 best_loss=4.3533e+00 best_ppl=77.73                                              
Epoch 6 - |param|=3.25e+02 |g_param|=1.66e+05 loss=3.8621e+00 ppl=47.57                                                 
Validation - loss=3.9320e+00 ppl=51.01 best_loss=4.1328e+00 best_ppl=62.35                                              
Epoch 7 - |param|=3.25e+02 |g_param|=1.44e+05 loss=3.6604e+00 ppl=38.88                                                 
Validation - loss=3.7596e+00 ppl=42.93 best_loss=3.9320e+00 best_ppl=51.01                                              
Epoch 8 - |param|=3.25e+02 |g_param|=1.63e+05 loss=3.4702e+00 ppl=32.14                                                 
Validation - loss=3.6051e+00 ppl=36.79 best_loss=3.7596e+00 best_ppl=42.93                                              
Epoch 9 - |param|=3.25e+02 |g_param|=1.71e+05 loss=3.4219e+00 ppl=30.63                                                 
Validation - loss=3.4522e+00 ppl=31.57 best_loss=3.6051e+00 best_ppl=36.79                                              
Epoch 10 - |param|=3.25e+02 |g_param|=2.14e+05 loss=3.2314e+00 ppl=25.32                                                
Validation - loss=3.3252e+00 ppl=27.81 best_loss=3.4522e+00 best_ppl=31.57                                              
Epoch 11 - |param|=3.25e+02 |g_param|=1.90e+05 loss=3.1801e+00 ppl=24.05                                                
Validation - loss=3.2123e+00 ppl=24.83 best_loss=3.3252e+00 best_ppl=27.81                                              
Epoch 12 - |param|=3.25e+02 |g_param|=1.76e+05 loss=3.0401e+00 ppl=20.91                                                
Validation - loss=3.1082e+00 ppl=22.38 best_loss=3.2123e+00 best_ppl=24.83                                              
Epoch 13 - |param|=3.25e+02 |g_param|=1.91e+05 loss=2.9353e+00 ppl=18.83                                                
Validation - loss=3.0096e+00 ppl=20.28 best_loss=3.1082e+00 best_ppl=22.38                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.63e+05 loss=2.8695e+00 ppl=17.63                                                
Validation - loss=2.9321e+00 ppl=18.77 best_loss=3.0096e+00 best_ppl=20.28                                              
Epoch 15 - |param|=3.25e+02 |g_param|=2.16e+05 loss=2.8168e+00 ppl=16.72                                                
Validation - loss=2.8473e+00 ppl=17.24 best_loss=2.9321e+00 best_ppl=18.77                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.37e+05 loss=2.7180e+00 ppl=15.15                                                
Validation - loss=2.7745e+00 ppl=16.03 best_loss=2.8473e+00 best_ppl=17.24                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.68e+05 loss=2.6517e+00 ppl=14.18                                                
Validation - loss=2.7162e+00 ppl=15.12 best_loss=2.7745e+00 best_ppl=16.03                                              
Epoch 18 - |param|=3.25e+02 |g_param|=2.31e+05 loss=2.7071e+00 ppl=14.99                                                
Validation - loss=2.6417e+00 ppl=14.04 best_loss=2.7162e+00 best_ppl=15.12                                              
Epoch 19 - |param|=3.25e+02 |g_param|=4.27e+05 loss=2.5811e+00 ppl=13.21                                                
Validation - loss=2.5864e+00 ppl=13.28 best_loss=2.6417e+00 best_ppl=14.04                                              
Epoch 20 - |param|=3.25e+02 |g_param|=2.91e+05 loss=2.4955e+00 ppl=12.13                                                
Validation - loss=2.5241e+00 ppl=12.48 best_loss=2.5864e+00 best_ppl=13.28                                              
Epoch 21 - |param|=3.25e+02 |g_param|=2.73e+05 loss=2.4663e+00 ppl=11.78                                                
Validation - loss=2.4673e+00 ppl=11.79 best_loss=2.5241e+00 best_ppl=12.48                                              
Epoch 22 - |param|=3.25e+02 |g_param|=2.92e+05 loss=2.4329e+00 ppl=11.39                                                
Validation - loss=2.4086e+00 ppl=11.12 best_loss=2.4673e+00 best_ppl=11.79                                              
Epoch 23 - |param|=3.26e+02 |g_param|=3.41e+05 loss=2.3780e+00 ppl=10.78                                                
Validation - loss=2.3588e+00 ppl=10.58 best_loss=2.4086e+00 best_ppl=11.12                                              
Epoch 24 - |param|=3.26e+02 |g_param|=3.66e+05 loss=2.3351e+00 ppl=10.33                                                
Validation - loss=2.3217e+00 ppl=10.19 best_loss=2.3588e+00 best_ppl=10.58                                              
Epoch 25 - |param|=3.26e+02 |g_param|=3.70e+05 loss=2.2478e+00 ppl=9.47                                                 
Validation - loss=2.2659e+00 ppl=9.64 best_loss=2.3217e+00 best_ppl=10.19                                               
Epoch 26 - |param|=3.26e+02 |g_param|=3.26e+05 loss=2.2792e+00 ppl=9.77                                                 
Validation - loss=2.2137e+00 ppl=9.15 best_loss=2.2659e+00 best_ppl=9.64                                                
Epoch 27 - |param|=3.26e+02 |g_param|=3.17e+05 loss=2.2305e+00 ppl=9.30                                                 
Validation - loss=2.1690e+00 ppl=8.75 best_loss=2.2137e+00 best_ppl=9.15                                                
Epoch 28 - |param|=3.26e+02 |g_param|=4.01e+05 loss=2.1782e+00 ppl=8.83                                                 
Validation - loss=2.1306e+00 ppl=8.42 best_loss=2.1690e+00 best_ppl=8.75                                                
Epoch 29 - |param|=3.26e+02 |g_param|=4.75e+05 loss=2.1227e+00 ppl=8.35                                                 
Validation - loss=2.0970e+00 ppl=8.14 best_loss=2.1306e+00 best_ppl=8.42                                                
Epoch 30 - |param|=3.26e+02 |g_param|=4.43e+05 loss=2.0649e+00 ppl=7.88                                                 
Validation - loss=2.0416e+00 ppl=7.70 best_loss=2.0970e+00 best_ppl=8.14                                                
Epoch 31 - |param|=3.26e+02 |g_param|=6.07e+05 loss=2.0512e+00 ppl=7.78                                                 
Validation - loss=2.0111e+00 ppl=7.47 best_loss=2.0416e+00 best_ppl=7.70                                                
Epoch 32 - |param|=3.26e+02 |g_param|=3.66e+05 loss=2.0630e+00 ppl=7.87                                                 
Validation - loss=1.9720e+00 ppl=7.19 best_loss=2.0111e+00 best_ppl=7.47                                                
Epoch 33 - |param|=3.26e+02 |g_param|=3.68e+05 loss=1.9662e+00 ppl=7.14                                                 
Validation - loss=1.9262e+00 ppl=6.86 best_loss=1.9720e+00 best_ppl=7.19                                                
Epoch 34 - |param|=3.26e+02 |g_param|=4.02e+05 loss=2.0366e+00 ppl=7.66                                                 
Validation - loss=1.8881e+00 ppl=6.61 best_loss=1.9262e+00 best_ppl=6.86                                                
Epoch 35 - |param|=3.26e+02 |g_param|=5.34e+05 loss=1.9327e+00 ppl=6.91                                                 
Validation - loss=1.8602e+00 ppl=6.43 best_loss=1.8881e+00 best_ppl=6.61                                                
Epoch 36 - |param|=3.26e+02 |g_param|=5.24e+05 loss=1.8907e+00 ppl=6.62                                                 
Validation - loss=1.8245e+00 ppl=6.20 best_loss=1.8602e+00 best_ppl=6.43                                                
Epoch 37 - |param|=3.26e+02 |g_param|=4.35e+05 loss=1.8558e+00 ppl=6.40                                                 
Validation - loss=1.7827e+00 ppl=5.95 best_loss=1.8245e+00 best_ppl=6.20                                                
Epoch 38 - |param|=3.26e+02 |g_param|=3.95e+05 loss=1.8307e+00 ppl=6.24                                                 
Validation - loss=1.7526e+00 ppl=5.77 best_loss=1.7827e+00 best_ppl=5.95                                                
Epoch 39 - |param|=3.26e+02 |g_param|=5.74e+05 loss=1.8827e+00 ppl=6.57                                                 
Validation - loss=1.7184e+00 ppl=5.58 best_loss=1.7526e+00 best_ppl=5.77                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.64e+05 loss=1.8310e+00 ppl=6.24                                                 
Validation - loss=1.7034e+00 ppl=5.49 best_loss=1.7184e+00 best_ppl=5.58                                                
Epoch 41 - |param|=3.26e+02 |g_param|=4.68e+05 loss=1.8377e+00 ppl=6.28                                                 
Validation - loss=1.6594e+00 ppl=5.26 best_loss=1.7034e+00 best_ppl=5.49                                                
Epoch 42 - |param|=3.26e+02 |g_param|=4.27e+05 loss=1.7176e+00 ppl=5.57                                                 
Validation - loss=1.6277e+00 ppl=5.09 best_loss=1.6594e+00 best_ppl=5.26                                                
Epoch 43 - |param|=3.26e+02 |g_param|=7.12e+05 loss=1.7253e+00 ppl=5.61                                                 
Validation - loss=1.6052e+00 ppl=4.98 best_loss=1.6277e+00 best_ppl=5.09                                                
Epoch 44 - |param|=3.26e+02 |g_param|=4.36e+05 loss=1.7062e+00 ppl=5.51                                                 
Validation - loss=1.5778e+00 ppl=4.84 best_loss=1.6052e+00 best_ppl=4.98                                                
Epoch 45 - |param|=3.26e+02 |g_param|=5.08e+05 loss=1.7072e+00 ppl=5.51                                                 
Validation - loss=1.5556e+00 ppl=4.74 best_loss=1.5778e+00 best_ppl=4.84                                                
Epoch 46 - |param|=3.26e+02 |g_param|=6.09e+05 loss=1.6834e+00 ppl=5.38                                                 
Validation - loss=1.5432e+00 ppl=4.68 best_loss=1.5556e+00 best_ppl=4.74                                                
Epoch 47 - |param|=3.26e+02 |g_param|=4.15e+05 loss=1.6771e+00 ppl=5.35                                                 
Validation - loss=1.5042e+00 ppl=4.50 best_loss=1.5432e+00 best_ppl=4.68                                                
Epoch 48 - |param|=3.27e+02 |g_param|=7.40e+05 loss=1.6066e+00 ppl=4.99                                                 
Validation - loss=1.4910e+00 ppl=4.44 best_loss=1.5042e+00 best_ppl=4.50                                                
Epoch 49 - |param|=3.27e+02 |g_param|=3.95e+05 loss=1.5720e+00 ppl=4.82                                                 
Validation - loss=1.4734e+00 ppl=4.36 best_loss=1.4910e+00 best_ppl=4.44                                                
Epoch 50 - |param|=3.27e+02 |g_param|=5.04e+05 loss=1.6078e+00 ppl=4.99                                                 
Validation - loss=1.4450e+00 ppl=4.24 best_loss=1.4734e+00 best_ppl=4.36                                                
Epoch 51 - |param|=3.27e+02 |g_param|=4.37e+05 loss=1.4715e+00 ppl=4.36                                                 
Validation - loss=1.4234e+00 ppl=4.15 best_loss=1.4450e+00 best_ppl=4.24                                                
Epoch 52 - |param|=3.27e+02 |g_param|=6.27e+05 loss=1.5263e+00 ppl=4.60                                                 
Validation - loss=1.4145e+00 ppl=4.11 best_loss=1.4234e+00 best_ppl=4.15                                                
Epoch 53 - |param|=3.27e+02 |g_param|=1.05e+06 loss=1.5696e+00 ppl=4.80                                                 
Validation - loss=1.3995e+00 ppl=4.05 best_loss=1.4145e+00 best_ppl=4.11                                                
Epoch 54 - |param|=3.27e+02 |g_param|=5.53e+05 loss=1.5225e+00 ppl=4.58                                                 
Validation - loss=1.3757e+00 ppl=3.96 best_loss=1.3995e+00 best_ppl=4.05                                                
Epoch 55 - |param|=3.27e+02 |g_param|=7.16e+05 loss=1.5843e+00 ppl=4.88                                                 
Validation - loss=1.3641e+00 ppl=3.91 best_loss=1.3757e+00 best_ppl=3.96                                                
Epoch 56 - |param|=3.27e+02 |g_param|=5.04e+05 loss=1.4269e+00 ppl=4.17                                                 
Validation - loss=1.3423e+00 ppl=3.83 best_loss=1.3641e+00 best_ppl=3.91                                                
Epoch 57 - |param|=3.27e+02 |g_param|=6.16e+05 loss=1.4593e+00 ppl=4.30                                                 
Validation - loss=1.3193e+00 ppl=3.74 best_loss=1.3423e+00 best_ppl=3.83                                                
Epoch 58 - |param|=3.27e+02 |g_param|=6.13e+05 loss=1.4400e+00 ppl=4.22                                                 
Validation - loss=1.3145e+00 ppl=3.72 best_loss=1.3193e+00 best_ppl=3.74                                                
Epoch 59 - |param|=3.27e+02 |g_param|=4.12e+05 loss=1.4489e+00 ppl=4.26                                                 
Validation - loss=1.2874e+00 ppl=3.62 best_loss=1.3145e+00 best_ppl=3.72                                                
Epoch 60 - |param|=3.27e+02 |g_param|=2.65e+05 loss=1.4541e+00 ppl=4.28                                                 
Validation - loss=1.2796e+00 ppl=3.60 best_loss=1.2874e+00 best_ppl=3.62                                                
Epoch 61 - |param|=3.27e+02 |g_param|=3.00e+05 loss=1.4392e+00 ppl=4.22                                                 
Validation - loss=1.2714e+00 ppl=3.57 best_loss=1.2796e+00 best_ppl=3.60                                                
Epoch 62 - |param|=3.27e+02 |g_param|=3.79e+05 loss=1.3485e+00 ppl=3.85                                                 
Validation - loss=1.2543e+00 ppl=3.51 best_loss=1.2714e+00 best_ppl=3.57                                                
Epoch 63 - |param|=3.27e+02 |g_param|=3.22e+05 loss=1.3316e+00 ppl=3.79                                                 
Validation - loss=1.2580e+00 ppl=3.52 best_loss=1.2543e+00 best_ppl=3.51                                                
Epoch 64 - |param|=3.27e+02 |g_param|=3.70e+05 loss=1.3836e+00 ppl=3.99                                                 
Validation - loss=1.2323e+00 ppl=3.43 best_loss=1.2543e+00 best_ppl=3.51                                                
Epoch 65 - |param|=3.27e+02 |g_param|=2.62e+05 loss=1.3636e+00 ppl=3.91                                                 
Validation - loss=1.2137e+00 ppl=3.37 best_loss=1.2323e+00 best_ppl=3.43                                                
Epoch 66 - |param|=3.27e+02 |g_param|=5.11e+05 loss=1.3911e+00 ppl=4.02                                                 
Validation - loss=1.2025e+00 ppl=3.33 best_loss=1.2137e+00 best_ppl=3.37                                                
Epoch 67 - |param|=3.27e+02 |g_param|=3.76e+05 loss=1.3218e+00 ppl=3.75                                                 
Validation - loss=1.2043e+00 ppl=3.33 best_loss=1.2025e+00 best_ppl=3.33                                                
Epoch 68 - |param|=3.27e+02 |g_param|=3.61e+05 loss=1.3087e+00 ppl=3.70                                                 
Validation - loss=1.1809e+00 ppl=3.26 best_loss=1.2025e+00 best_ppl=3.33                                                
Epoch 69 - |param|=3.27e+02 |g_param|=5.32e+05 loss=1.3062e+00 ppl=3.69                                                 
Validation - loss=1.2116e+00 ppl=3.36 best_loss=1.1809e+00 best_ppl=3.26                                                
Epoch 70 - |param|=3.27e+02 |g_param|=3.67e+05 loss=1.2454e+00 ppl=3.47                                                 
Validation - loss=1.1675e+00 ppl=3.21 best_loss=1.1809e+00 best_ppl=3.26                                                

real	36m39.400s
user	36m29.314s
sys	0m6.726s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.82-335.32.5.80-329.67.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 0.7/0.0/0.0/0.0 (BP=1.000, ratio=2.562, hyp_len=60239, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.5.01-149.99.5.03-153.13.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.5/0.6/0.0/0.0 (BP=0.758, ratio=0.783, hyp_len=18410, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.52-91.81.4.62-101.15.pth
BLEU = 0.69, 37.9/6.1/0.5/0.1 (BP=0.435, ratio=0.546, hyp_len=12828, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.24-69.48.4.35-77.73.pth
BLEU = 0.88, 42.5/10.5/0.8/0.1 (BP=0.409, ratio=0.528, hyp_len=12410, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.07-58.37.4.13-62.35.pth
BLEU = 1.74, 39.7/11.9/1.2/0.1 (BP=0.605, ratio=0.665, hyp_len=15643, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.86-47.57.3.93-51.01.pth
BLEU = 3.15, 35.5/12.0/1.7/0.3 (BP=0.806, ratio=0.822, hyp_len=19330, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.66-38.88.3.76-42.93.pth
BLEU = 4.56, 32.9/11.8/2.3/0.6 (BP=0.953, ratio=0.954, hyp_len=22438, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.47-32.14.3.61-36.79.pth
BLEU = 5.09, 36.9/13.6/2.9/0.7 (BP=0.892, ratio=0.898, hyp_len=21106, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.42-30.63.3.45-31.57.pth
BLEU = 6.38, 34.8/13.4/3.5/1.0 (BP=1.000, ratio=1.029, hyp_len=24194, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.23-25.32.3.33-27.81.pth
BLEU = 7.09, 35.8/14.2/4.1/1.2 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.18-24.05.3.21-24.83.pth
BLEU = 8.15, 37.8/15.5/4.9/1.5 (BP=1.000, ratio=1.035, hyp_len=24337, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.04-20.91.3.11-22.38.pth
BLEU = 9.35, 40.5/17.1/5.7/1.9 (BP=1.000, ratio=1.008, hyp_len=23695, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.2.94-18.83.3.01-20.28.pth
BLEU = 9.69, 38.3/16.7/6.1/2.2 (BP=1.000, ratio=1.116, hyp_len=26233, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.87-17.63.2.93-18.77.pth
BLEU = 11.15, 41.1/18.5/7.3/2.8 (BP=1.000, ratio=1.073, hyp_len=25226, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.82-16.72.2.85-17.24.pth
BLEU = 13.01, 44.8/20.9/8.7/3.5 (BP=0.999, ratio=0.999, hyp_len=23493, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.72-15.15.2.77-16.03.pth
BLEU = 13.57, 44.8/21.4/9.2/3.8 (BP=1.000, ratio=1.043, hyp_len=24513, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.65-14.18.2.72-15.12.pth
BLEU = 14.23, 45.1/21.9/9.7/4.3 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.71-14.99.2.64-14.04.pth
BLEU = 15.47, 47.1/23.5/10.8/4.8 (BP=1.000, ratio=1.035, hyp_len=24329, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.58-13.21.2.59-13.28.pth
BLEU = 15.25, 45.3/22.8/10.7/4.9 (BP=1.000, ratio=1.103, hyp_len=25930, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.50-12.13.2.52-12.48.pth
BLEU = 17.43, 48.9/25.5/12.4/6.0 (BP=1.000, ratio=1.039, hyp_len=24421, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.47-11.78.2.47-11.79.pth
BLEU = 18.01, 49.7/26.2/13.0/6.2 (BP=1.000, ratio=1.047, hyp_len=24619, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.43-11.39.2.41-11.12.pth
BLEU = 18.17, 49.3/26.3/13.1/6.4 (BP=1.000, ratio=1.083, hyp_len=25471, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.38-10.78.2.36-10.58.pth
BLEU = 19.11, 50.4/27.2/14.0/7.0 (BP=1.000, ratio=1.071, hyp_len=25187, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.34-10.33.2.32-10.19.pth
BLEU = 19.00, 49.0/26.8/14.0/7.1 (BP=1.000, ratio=1.131, hyp_len=26587, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.25-9.47.2.27-9.64.pth
BLEU = 19.65, 49.0/27.3/14.6/7.6 (BP=1.000, ratio=1.146, hyp_len=26933, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.28-9.77.2.21-9.15.pth
BLEU = 21.45, 52.4/29.7/16.0/8.5 (BP=1.000, ratio=1.080, hyp_len=25397, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.23-9.30.2.17-8.75.pth
BLEU = 22.41, 53.9/30.7/16.9/9.0 (BP=1.000, ratio=1.073, hyp_len=25223, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.18-8.83.2.13-8.42.pth
BLEU = 24.96, 57.3/33.4/19.0/10.7 (BP=1.000, ratio=1.017, hyp_len=23909, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.12-8.35.2.10-8.14.pth
BLEU = 23.18, 54.0/31.4/17.6/9.7 (BP=1.000, ratio=1.096, hyp_len=25777, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.06-7.88.2.04-7.70.pth
BLEU = 24.59, 55.8/33.0/18.8/10.6 (BP=1.000, ratio=1.077, hyp_len=25324, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.31.2.05-7.78.2.01-7.47.pth
BLEU = 26.62, 58.0/35.0/20.6/12.0 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.32.2.06-7.87.1.97-7.19.pth
BLEU = 25.97, 56.2/34.1/20.1/11.8 (BP=1.000, ratio=1.100, hyp_len=25853, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.33.1.97-7.14.1.93-6.86.pth
BLEU = 28.59, 59.9/37.0/22.3/13.5 (BP=1.000, ratio=1.041, hyp_len=24474, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.34.2.04-7.66.1.89-6.61.pth
BLEU = 29.59, 60.4/37.9/23.3/14.4 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.35.1.93-6.91.1.86-6.43.pth
BLEU = 28.30, 58.1/36.4/22.3/13.6 (BP=1.000, ratio=1.103, hyp_len=25939, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.36.1.89-6.62.1.82-6.20.pth
BLEU = 28.89, 58.2/36.9/22.9/14.2 (BP=1.000, ratio=1.117, hyp_len=26252, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.37.1.86-6.40.1.78-5.95.pth
BLEU = 30.96, 60.3/39.0/24.7/15.8 (BP=1.000, ratio=1.091, hyp_len=25656, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.38.1.83-6.24.1.75-5.77.pth
BLEU = 31.40, 60.5/39.4/25.2/16.2 (BP=1.000, ratio=1.097, hyp_len=25796, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.39.1.88-6.57.1.72-5.58.pth
BLEU = 33.04, 62.8/41.4/26.6/17.3 (BP=1.000, ratio=1.060, hyp_len=24923, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.40.1.83-6.24.1.70-5.49.pth
BLEU = 32.84, 61.8/41.1/26.6/17.2 (BP=1.000, ratio=1.096, hyp_len=25777, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.41.1.84-6.28.1.66-5.26.pth
BLEU = 34.95, 64.4/43.2/28.4/18.9 (BP=1.000, ratio=1.056, hyp_len=24829, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.42.1.72-5.57.1.63-5.09.pth
BLEU = 35.68, 64.7/43.8/29.2/19.6 (BP=1.000, ratio=1.057, hyp_len=24852, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.43.1.73-5.61.1.61-4.98.pth
BLEU = 37.07, 65.8/45.1/30.5/20.9 (BP=1.000, ratio=1.049, hyp_len=24650, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.44.1.71-5.51.1.58-4.84.pth
BLEU = 37.20, 65.8/45.3/30.7/20.9 (BP=1.000, ratio=1.058, hyp_len=24881, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.45.1.71-5.51.1.56-4.74.pth
BLEU = 38.27, 66.7/46.3/31.7/21.9 (BP=1.000, ratio=1.048, hyp_len=24633, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.46.1.68-5.38.1.54-4.68.pth
BLEU = 36.22, 63.5/44.1/30.0/20.5 (BP=1.000, ratio=1.113, hyp_len=26175, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.47.1.68-5.35.1.50-4.50.pth
BLEU = 39.06, 66.6/47.0/32.6/22.8 (BP=1.000, ratio=1.067, hyp_len=25090, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.48.1.61-4.99.1.49-4.44.pth
BLEU = 38.78, 66.4/46.8/32.4/22.5 (BP=1.000, ratio=1.079, hyp_len=25376, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.49.1.57-4.82.1.47-4.36.pth
BLEU = 39.69, 67.1/47.7/33.3/23.2 (BP=1.000, ratio=1.072, hyp_len=25206, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.50.1.61-4.99.1.45-4.24.pth
BLEU = 41.21, 68.5/49.0/34.7/24.8 (BP=1.000, ratio=1.055, hyp_len=24805, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.51.1.47-4.36.1.42-4.15.pth
BLEU = 41.71, 69.0/49.7/35.3/25.0 (BP=1.000, ratio=1.054, hyp_len=24781, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.52.1.53-4.60.1.41-4.11.pth
BLEU = 41.47, 68.6/49.4/35.1/24.9 (BP=1.000, ratio=1.070, hyp_len=25161, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.53.1.57-4.80.1.40-4.05.pth
BLEU = 44.96, 71.9/52.6/38.3/28.2 (BP=1.000, ratio=1.012, hyp_len=23790, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.54.1.52-4.58.1.38-3.96.pth
BLEU = 42.22, 68.9/50.0/35.8/25.8 (BP=1.000, ratio=1.073, hyp_len=25230, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.55.1.58-4.88.1.36-3.91.pth
BLEU = 41.33, 67.6/49.1/35.1/25.1 (BP=1.000, ratio=1.101, hyp_len=25872, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.56.1.43-4.17.1.34-3.83.pth
BLEU = 43.39, 70.1/51.2/37.0/26.7 (BP=1.000, ratio=1.062, hyp_len=24966, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.57.1.46-4.30.1.32-3.74.pth
BLEU = 44.72, 70.9/52.2/38.3/28.2 (BP=1.000, ratio=1.058, hyp_len=24879, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.58.1.44-4.22.1.31-3.72.pth
BLEU = 44.33, 70.3/51.9/38.0/27.9 (BP=1.000, ratio=1.067, hyp_len=25092, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.59.1.45-4.26.1.29-3.62.pth
BLEU = 45.92, 71.7/53.4/39.5/29.4 (BP=1.000, ratio=1.052, hyp_len=24743, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.60.1.45-4.28.1.28-3.60.pth
BLEU = 45.13, 70.5/52.4/38.8/28.9 (BP=1.000, ratio=1.077, hyp_len=25322, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.61.1.44-4.22.1.27-3.57.pth
BLEU = 46.90, 72.5/54.4/40.5/30.3 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.62.1.35-3.85.1.25-3.51.pth
BLEU = 46.65, 72.1/54.1/40.3/30.2 (BP=1.000, ratio=1.055, hyp_len=24809, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.63.1.33-3.79.1.26-3.52.pth
BLEU = 45.90, 71.5/53.8/39.7/29.1 (BP=1.000, ratio=1.071, hyp_len=25185, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.64.1.38-3.99.1.23-3.43.pth
BLEU = 46.01, 70.8/53.3/39.8/29.8 (BP=1.000, ratio=1.085, hyp_len=25502, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.65.1.36-3.91.1.21-3.37.pth
BLEU = 48.06, 73.2/55.4/41.7/31.5 (BP=1.000, ratio=1.050, hyp_len=24682, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.66.1.39-4.02.1.20-3.33.pth
BLEU = 47.36, 71.6/54.5/41.2/31.3 (BP=1.000, ratio=1.081, hyp_len=25415, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.67.1.32-3.75.1.20-3.33.pth
BLEU = 48.26, 73.1/55.8/42.0/31.6 (BP=1.000, ratio=1.057, hyp_len=24841, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.68.1.31-3.70.1.18-3.26.pth
BLEU = 48.94, 73.5/56.2/42.6/32.6 (BP=1.000, ratio=1.056, hyp_len=24814, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.69.1.31-3.69.1.21-3.36.pth
BLEU = 46.00, 70.7/53.6/39.9/29.6 (BP=1.000, ratio=1.100, hyp_len=25855, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth
BLEU = 51.15, 75.4/58.2/44.7/34.9 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)

real	43m33.362s
user	42m25.463s
sys	1m35.009s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-70epoch$
```

Transformer, rk-my, 70 epoch မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth
BLEU = 51.15, 75.4/58.2/44.7/34.9 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
```


## seq2seq RL Models

### for 60 epoch

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth --model_fn ./model/rl/seq2seq/myrk-40epoch/seq-rl-model-myrk.pth --init_epoch 40 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/myrk-40epoch/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 40
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 40,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/myrk-40epoch/seq-rl-model-myrk.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 40 - |param|=6.59e+02 |g_param|=7.10e+04 loss=5.4270e-01 ppl=1.72                                                 
Validation - loss=8.5581e-01 ppl=2.35 best_loss=inf best_ppl=inf                                                        
Epoch 41 - |param|=6.59e+02 |g_param|=6.16e+04 loss=5.2621e-01 ppl=1.69                                                 
Validation - loss=8.3004e-01 ppl=2.29 best_loss=8.5581e-01 best_ppl=2.35                                                
Epoch 42 - |param|=6.60e+02 |g_param|=5.47e+04 loss=5.0194e-01 ppl=1.65                                                 
Validation - loss=8.3196e-01 ppl=2.30 best_loss=8.3004e-01 best_ppl=2.29                                                
Epoch 43 - |param|=6.60e+02 |g_param|=5.87e+04 loss=4.9970e-01 ppl=1.65                                                 
Validation - loss=8.2329e-01 ppl=2.28 best_loss=8.3004e-01 best_ppl=2.29                                                
Epoch 44 - |param|=6.60e+02 |g_param|=5.80e+04 loss=4.8400e-01 ppl=1.62                                                 
Validation - loss=8.1375e-01 ppl=2.26 best_loss=8.2329e-01 best_ppl=2.28                                                
Epoch 45 - |param|=6.61e+02 |g_param|=5.17e+04 loss=4.6427e-01 ppl=1.59                                                 
Validation - loss=8.0949e-01 ppl=2.25 best_loss=8.1375e-01 best_ppl=2.26                                                
Epoch 46 - |param|=6.61e+02 |g_param|=5.78e+04 loss=4.6303e-01 ppl=1.59                                                 
Validation - loss=8.0942e-01 ppl=2.25 best_loss=8.0949e-01 best_ppl=2.25                                                
Epoch 47 - |param|=6.62e+02 |g_param|=5.37e+04 loss=4.3658e-01 ppl=1.55                                                 
Validation - loss=7.8958e-01 ppl=2.20 best_loss=8.0942e-01 best_ppl=2.25                                                
Epoch 48 - |param|=6.62e+02 |g_param|=2.76e+04 loss=4.1476e-01 ppl=1.51                                                 
Validation - loss=8.0515e-01 ppl=2.24 best_loss=7.8958e-01 best_ppl=2.20                                                
Epoch 49 - |param|=6.62e+02 |g_param|=3.60e+04 loss=4.3250e-01 ppl=1.54                                                 
Validation - loss=8.8794e-01 ppl=2.43 best_loss=7.8958e-01 best_ppl=2.20                                                
Epoch 50 - |param|=6.63e+02 |g_param|=3.24e+04 loss=4.3090e-01 ppl=1.54                                                 
Validation - loss=8.1315e-01 ppl=2.25 best_loss=7.8958e-01 best_ppl=2.20                                                
Epoch 51 - |param|=6.63e+02 |g_param|=3.59e+04 loss=4.5764e-01 ppl=1.58                                                 
Validation - loss=7.8275e-01 ppl=2.19 best_loss=7.8958e-01 best_ppl=2.20                                                
Epoch 52 - |param|=6.63e+02 |g_param|=3.80e+04 loss=4.2003e-01 ppl=1.52                                                 
Validation - loss=8.3052e-01 ppl=2.29 best_loss=7.8275e-01 best_ppl=2.19                                                
Epoch 53 - |param|=6.64e+02 |g_param|=3.46e+04 loss=3.9830e-01 ppl=1.49                                                 
Validation - loss=7.9564e-01 ppl=2.22 best_loss=7.8275e-01 best_ppl=2.19                                                
Epoch 54 - |param|=6.64e+02 |g_param|=2.99e+04 loss=3.7911e-01 ppl=1.46                                                 
Validation - loss=7.5882e-01 ppl=2.14 best_loss=7.8275e-01 best_ppl=2.19                                                
Epoch 55 - |param|=6.64e+02 |g_param|=2.28e+04 loss=3.7982e-01 ppl=1.46                                                 
Validation - loss=7.7435e-01 ppl=2.17 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 56 - |param|=6.65e+02 |g_param|=2.66e+04 loss=3.4646e-01 ppl=1.41                                                 
Validation - loss=7.6180e-01 ppl=2.14 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 57 - |param|=6.65e+02 |g_param|=2.04e+04 loss=3.4441e-01 ppl=1.41                                                 
Validation - loss=7.6044e-01 ppl=2.14 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 58 - |param|=6.65e+02 |g_param|=2.68e+04 loss=3.5699e-01 ppl=1.43                                                 
Validation - loss=7.8055e-01 ppl=2.18 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 59 - |param|=6.66e+02 |g_param|=3.95e+04 loss=3.8496e-01 ppl=1.47                                                 
Validation - loss=7.8174e-01 ppl=2.19 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 60 - |param|=6.66e+02 |g_param|=2.39e+04 loss=3.5636e-01 ppl=1.43                                                 
Validation - loss=7.5480e-01 ppl=2.13 best_loss=7.5882e-01 best_ppl=2.14                                                
Epoch 61 - |param|=6.66e+02 |g_param|=2.59e+04 loss=3.3531e-01 ppl=1.40                                                 
Validation - loss=7.6149e-01 ppl=2.14 best_loss=7.5480e-01 best_ppl=2.13                                                
Epoch 62 - |param|=6.67e+02 |g_param|=2.69e+04 loss=3.1409e-01 ppl=1.37                                                 
Validation - loss=7.6679e-01 ppl=2.15 best_loss=7.5480e-01 best_ppl=2.13                                                
Epoch 63 - |param|=6.67e+02 |g_param|=2.44e+04 loss=3.2691e-01 ppl=1.39                                                 
Validation - loss=7.4361e-01 ppl=2.10 best_loss=7.5480e-01 best_ppl=2.13                                                
Epoch 64 - |param|=6.67e+02 |g_param|=2.59e+04 loss=3.2177e-01 ppl=1.38                                                 
Validation - loss=7.4559e-01 ppl=2.11 best_loss=7.4361e-01 best_ppl=2.10                                                
Epoch 65 - |param|=6.68e+02 |g_param|=2.13e+04 loss=3.1702e-01 ppl=1.37                                                 
Validation - loss=7.5147e-01 ppl=2.12 best_loss=7.4361e-01 best_ppl=2.10                                                
Epoch 66 - |param|=6.68e+02 |g_param|=2.73e+04 loss=3.2325e-01 ppl=1.38                                                 
Validation - loss=7.4911e-01 ppl=2.12 best_loss=7.4361e-01 best_ppl=2.10                                                
Epoch 67 - |param|=6.68e+02 |g_param|=2.13e+04 loss=3.1183e-01 ppl=1.37                                                 
Validation - loss=7.4355e-01 ppl=2.10 best_loss=7.4361e-01 best_ppl=2.10                                                
Epoch 68 - |param|=6.68e+02 |g_param|=2.28e+04 loss=2.9390e-01 ppl=1.34                                                 
Validation - loss=7.3672e-01 ppl=2.09 best_loss=7.4355e-01 best_ppl=2.10                                                
Epoch 69 - |param|=6.69e+02 |g_param|=3.66e+04 loss=2.7461e-01 ppl=1.32                                                 
Validation - loss=7.5107e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 70 - |param|=6.69e+02 |g_param|=4.16e+04 loss=2.9816e-01 ppl=1.35                                                 
Validation - loss=7.5378e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 71 - |param|=6.69e+02 |g_param|=4.26e+04 loss=2.8149e-01 ppl=1.33                                                 
Validation - loss=7.4007e-01 ppl=2.10 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 72 - |param|=6.70e+02 |g_param|=4.69e+04 loss=2.7019e-01 ppl=1.31                                                 
Validation - loss=7.5093e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 73 - |param|=6.70e+02 |g_param|=4.94e+04 loss=2.9791e-01 ppl=1.35                                                 
Validation - loss=7.4754e-01 ppl=2.11 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 74 - |param|=6.70e+02 |g_param|=4.72e+04 loss=2.7606e-01 ppl=1.32                                                 
Validation - loss=7.5791e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 75 - |param|=6.71e+02 |g_param|=3.06e+04 loss=2.7580e-01 ppl=1.32                                                 
Validation - loss=7.4989e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 76 - |param|=6.71e+02 |g_param|=2.10e+04 loss=2.4994e-01 ppl=1.28                                                 
Validation - loss=7.4113e-01 ppl=2.10 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 77 - |param|=6.71e+02 |g_param|=2.28e+04 loss=2.6659e-01 ppl=1.31                                                 
Validation - loss=7.5315e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 78 - |param|=6.71e+02 |g_param|=2.49e+04 loss=2.7431e-01 ppl=1.32                                                 
Validation - loss=7.5805e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 79 - |param|=6.72e+02 |g_param|=2.16e+04 loss=2.6081e-01 ppl=1.30                                                 
Validation - loss=7.5576e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 80 - |param|=6.72e+02 |g_param|=2.60e+04 loss=2.5443e-01 ppl=1.29                                                 
Validation - loss=7.6363e-01 ppl=2.15 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 81 - |param|=6.72e+02 |g_param|=2.42e+04 loss=2.6353e-01 ppl=1.30                                                 
Validation - loss=7.6289e-01 ppl=2.14 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 82 - |param|=6.73e+02 |g_param|=2.54e+04 loss=2.6137e-01 ppl=1.30                                                 
Validation - loss=7.4735e-01 ppl=2.11 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 83 - |param|=6.73e+02 |g_param|=2.45e+04 loss=2.5287e-01 ppl=1.29                                                 
Validation - loss=7.3763e-01 ppl=2.09 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 84 - |param|=6.73e+02 |g_param|=2.09e+04 loss=2.3354e-01 ppl=1.26                                                 
Validation - loss=7.5351e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 85 - |param|=6.74e+02 |g_param|=1.90e+04 loss=2.3675e-01 ppl=1.27                                                 
Validation - loss=7.4127e-01 ppl=2.10 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 86 - |param|=6.74e+02 |g_param|=2.23e+04 loss=2.3362e-01 ppl=1.26                                                 
Validation - loss=7.4993e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 87 - |param|=6.74e+02 |g_param|=2.09e+04 loss=2.3047e-01 ppl=1.26                                                 
Validation - loss=7.4689e-01 ppl=2.11 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 88 - |param|=6.75e+02 |g_param|=2.99e+04 loss=2.3697e-01 ppl=1.27                                                 
Validation - loss=8.2432e-01 ppl=2.28 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 89 - |param|=6.75e+02 |g_param|=2.53e+04 loss=2.4200e-01 ppl=1.27                                                 
Validation - loss=8.3282e-01 ppl=2.30 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 90 - |param|=6.75e+02 |g_param|=3.37e+04 loss=2.5446e-01 ppl=1.29                                                 
Validation - loss=7.4484e-01 ppl=2.11 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 91 - |param|=6.76e+02 |g_param|=2.32e+04 loss=2.4037e-01 ppl=1.27                                                 
Validation - loss=7.5104e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 92 - |param|=6.76e+02 |g_param|=1.96e+04 loss=2.2815e-01 ppl=1.26                                                 
Validation - loss=7.3893e-01 ppl=2.09 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 93 - |param|=6.76e+02 |g_param|=1.72e+04 loss=2.0839e-01 ppl=1.23                                                 
Validation - loss=7.5196e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 94 - |param|=6.77e+02 |g_param|=2.07e+04 loss=2.1318e-01 ppl=1.24                                                 
Validation - loss=7.5309e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 95 - |param|=6.77e+02 |g_param|=1.98e+04 loss=1.9559e-01 ppl=1.22                                                 
Validation - loss=7.5528e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 96 - |param|=6.77e+02 |g_param|=4.72e+04 loss=2.1740e-01 ppl=1.24                                                 
Validation - loss=7.5891e-01 ppl=2.14 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 97 - |param|=6.77e+02 |g_param|=3.91e+04 loss=2.0370e-01 ppl=1.23                                                 
Validation - loss=7.5811e-01 ppl=2.13 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 98 - |param|=6.78e+02 |g_param|=3.30e+04 loss=1.9590e-01 ppl=1.22                                                 
Validation - loss=7.5180e-01 ppl=2.12 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 99 - |param|=6.78e+02 |g_param|=3.61e+04 loss=2.0418e-01 ppl=1.23                                                 
Validation - loss=7.4291e-01 ppl=2.10 best_loss=7.3672e-01 best_ppl=2.09                                                
Epoch 100 - |param|=6.78e+02 |g_param|=4.75e+04 loss=2.0674e-01 ppl=1.23                                                
Validation - loss=7.7280e-01 ppl=2.17 best_loss=7.3672e-01 best_ppl=2.09                                                

real	12m29.015s
user	11m43.276s
sys	0m21.894s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.40.0.54-1.72.0.86-2.35.pth
BLEU = 70.58, 85.9/75.0/66.0/58.3 (BP=1.000, ratio=1.016, hyp_len=23532, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.41.0.53-1.69.0.83-2.29.pth
BLEU = 70.28, 85.8/74.8/65.7/58.0 (BP=1.000, ratio=1.022, hyp_len=23678, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.42.0.50-1.65.0.83-2.30.pth
BLEU = 71.16, 86.0/75.4/66.7/59.3 (BP=1.000, ratio=1.023, hyp_len=23688, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.43.0.50-1.65.0.82-2.28.pth
BLEU = 70.87, 85.9/75.2/66.4/58.8 (BP=1.000, ratio=1.025, hyp_len=23729, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.44.0.48-1.62.0.81-2.26.pth
BLEU = 71.36, 86.2/75.7/66.9/59.4 (BP=1.000, ratio=1.024, hyp_len=23707, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.45.0.46-1.59.0.81-2.25.pth
BLEU = 71.61, 86.3/75.8/67.2/59.8 (BP=1.000, ratio=1.022, hyp_len=23665, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.46.0.46-1.59.0.81-2.25.pth
BLEU = 72.01, 86.5/76.1/67.6/60.4 (BP=1.000, ratio=1.024, hyp_len=23714, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.47.0.44-1.55.0.79-2.20.pth
BLEU = 71.68, 86.2/75.8/67.3/60.0 (BP=1.000, ratio=1.029, hyp_len=23841, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.48.0.41-1.51.0.81-2.24.pth
BLEU = 72.71, 87.0/76.8/68.4/61.2 (BP=1.000, ratio=1.023, hyp_len=23696, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.49.0.43-1.54.0.89-2.43.pth
BLEU = 71.85, 86.7/76.1/67.4/59.9 (BP=1.000, ratio=1.011, hyp_len=23423, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.50.0.43-1.54.0.81-2.25.pth
BLEU = 71.87, 86.5/76.1/67.4/60.1 (BP=1.000, ratio=1.021, hyp_len=23648, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.51.0.46-1.58.0.78-2.19.pth
BLEU = 73.20, 87.0/77.1/69.0/62.0 (BP=1.000, ratio=1.019, hyp_len=23598, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.52.0.42-1.52.0.83-2.29.pth
BLEU = 70.84, 85.5/75.2/66.4/58.9 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.53.0.40-1.49.0.80-2.22.pth
BLEU = 70.90, 85.9/75.4/66.4/58.8 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.54.0.38-1.46.0.76-2.14.pth
BLEU = 72.40, 86.3/76.3/68.1/61.2 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.55.0.38-1.46.0.77-2.17.pth
BLEU = 73.64, 87.2/77.5/69.5/62.7 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.56.0.35-1.41.0.76-2.14.pth
BLEU = 73.10, 87.0/77.1/68.9/61.8 (BP=1.000, ratio=1.024, hyp_len=23722, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.57.0.34-1.41.0.76-2.14.pth
BLEU = 73.06, 86.8/76.9/68.8/62.0 (BP=1.000, ratio=1.030, hyp_len=23852, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.58.0.36-1.43.0.78-2.18.pth
BLEU = 73.77, 87.3/77.6/69.7/62.8 (BP=1.000, ratio=1.020, hyp_len=23629, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.59.0.38-1.47.0.78-2.19.pth
BLEU = 73.52, 87.3/77.4/69.2/62.5 (BP=1.000, ratio=1.022, hyp_len=23673, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.60.0.36-1.43.0.75-2.13.pth
BLEU = 73.22, 86.9/77.1/69.0/62.2 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.61.0.34-1.40.0.76-2.14.pth
BLEU = 73.26, 86.9/77.1/69.1/62.2 (BP=1.000, ratio=1.027, hyp_len=23787, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.62.0.31-1.37.0.77-2.15.pth
BLEU = 73.42, 86.9/77.3/69.3/62.5 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.63.0.33-1.39.0.74-2.10.pth
BLEU = 72.95, 86.8/77.0/68.7/61.7 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.64.0.32-1.38.0.75-2.11.pth
BLEU = 72.97, 86.8/77.0/68.8/61.7 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.65.0.32-1.37.0.75-2.12.pth
BLEU = 72.28, 86.3/76.3/68.0/61.0 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.66.0.32-1.38.0.75-2.12.pth
BLEU = 72.71, 86.5/76.7/68.5/61.5 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.67.0.31-1.37.0.74-2.10.pth
BLEU = 73.48, 86.8/77.3/69.4/62.6 (BP=1.000, ratio=1.030, hyp_len=23846, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.68.0.29-1.34.0.74-2.09.pth
BLEU = 74.18, 87.4/78.0/70.1/63.3 (BP=1.000, ratio=1.026, hyp_len=23753, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.69.0.27-1.32.0.75-2.12.pth
BLEU = 73.11, 86.8/77.1/68.9/62.0 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.70.0.30-1.35.0.75-2.13.pth
BLEU = 73.34, 86.8/77.2/69.2/62.4 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.71.0.28-1.33.0.74-2.10.pth
BLEU = 73.32, 86.8/77.2/69.2/62.3 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.72.0.27-1.31.0.75-2.12.pth
BLEU = 72.12, 86.2/76.1/67.8/60.8 (BP=1.000, ratio=1.039, hyp_len=24068, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.73.0.30-1.35.0.75-2.11.pth
BLEU = 73.41, 86.8/77.2/69.3/62.5 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.74.0.28-1.32.0.76-2.13.pth
BLEU = 72.94, 86.6/76.9/68.7/61.8 (BP=1.000, ratio=1.036, hyp_len=24001, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.75.0.28-1.32.0.75-2.12.pth
BLEU = 74.19, 87.5/78.0/70.1/63.4 (BP=1.000, ratio=1.028, hyp_len=23806, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.76.0.25-1.28.0.74-2.10.pth
BLEU = 74.06, 87.3/77.8/70.0/63.3 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.77.0.27-1.31.0.75-2.12.pth
BLEU = 73.22, 86.9/77.2/69.1/62.0 (BP=1.000, ratio=1.037, hyp_len=24014, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.78.0.27-1.32.0.76-2.13.pth
BLEU = 73.67, 87.0/77.5/69.6/62.8 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.79.0.26-1.30.0.76-2.13.pth
BLEU = 74.07, 87.1/77.8/70.0/63.4 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.80.0.25-1.29.0.76-2.15.pth
BLEU = 73.21, 86.8/77.1/69.1/62.2 (BP=1.000, ratio=1.035, hyp_len=23964, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.81.0.26-1.30.0.76-2.14.pth
BLEU = 73.47, 87.0/77.3/69.3/62.5 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.82.0.26-1.30.0.75-2.11.pth
BLEU = 72.77, 86.6/76.8/68.5/61.5 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.83.0.25-1.29.0.74-2.09.pth
BLEU = 74.18, 87.4/77.9/70.1/63.4 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.84.0.23-1.26.0.75-2.12.pth
BLEU = 73.73, 87.1/77.5/69.6/62.9 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.85.0.24-1.27.0.74-2.10.pth
BLEU = 73.76, 87.0/77.5/69.7/62.9 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.86.0.23-1.26.0.75-2.12.pth
BLEU = 73.54, 87.1/77.4/69.4/62.5 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.87.0.23-1.26.0.75-2.11.pth
BLEU = 73.45, 86.9/77.3/69.3/62.5 (BP=1.000, ratio=1.036, hyp_len=23990, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.24-1.27.0.82-2.28.pth
BLEU = 73.58, 87.3/77.5/69.4/62.4 (BP=1.000, ratio=1.020, hyp_len=23618, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.24-1.27.0.83-2.30.pth
BLEU = 73.08, 87.0/77.1/68.8/61.8 (BP=1.000, ratio=1.020, hyp_len=23624, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.25-1.29.0.74-2.11.pth
BLEU = 73.25, 86.6/77.1/69.2/62.3 (BP=1.000, ratio=1.037, hyp_len=24018, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.24-1.27.0.75-2.12.pth
BLEU = 74.13, 87.3/77.9/70.0/63.4 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.23-1.26.0.74-2.09.pth
BLEU = 73.77, 87.0/77.5/69.7/63.0 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.21-1.23.0.75-2.12.pth
BLEU = 74.18, 87.3/77.9/70.1/63.5 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.21-1.24.0.75-2.12.pth
BLEU = 73.24, 86.9/77.2/69.1/62.1 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.20-1.22.0.76-2.13.pth
BLEU = 73.60, 87.0/77.4/69.5/62.7 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.22-1.24.0.76-2.14.pth
BLEU = 73.91, 87.2/77.7/69.8/63.1 (BP=1.000, ratio=1.029, hyp_len=23832, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.20-1.23.0.76-2.13.pth
BLEU = 73.64, 87.1/77.5/69.5/62.7 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.20-1.22.0.75-2.12.pth
BLEU = 74.53, 87.5/78.3/70.5/63.8 (BP=1.000, ratio=1.030, hyp_len=23845, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.20-1.23.0.74-2.10.pth
BLEU = 73.58, 86.9/77.4/69.5/62.7 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.100.0.21-1.23.0.77-2.17.pth
BLEU = 73.22, 87.0/77.2/69.0/62.0 (BP=1.000, ratio=1.030, hyp_len=23845, ref_len=23160)
real	22m33.296s
user	19m43.364s
sys	1m43.926s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-40epoch$
```

seq2seq 40 model (Baseline) က 
RL, my-rk, 40-60 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: seq-rl-model-myrk.98.0.20-1.22.0.75-2.12.pth
BLEU = 74.53, 87.5/78.3/70.5/63.8 (BP=1.000, ratio=1.030, hyp_len=23845, ref_len=23160)
```

### RL, my-rk, 50-50 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.48.0.43-1.54.0.76-2.14.pth --model_fn ./model/rl/seq2seq/myrk-50epoch/seq-rl-model-myrk.pth --init_epoch 48 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.48.0.43-1.54.0.76-2.14.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/myrk-50epoch/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 48
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 48,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.48.0.43-1.54.0.76-2.14.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/myrk-50epoch/seq-rl-model-myrk.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 48 - |param|=6.64e+02 |g_param|=1.61e+05 loss=4.0566e-01 ppl=1.50                                                 
Validation - loss=7.4487e-01 ppl=2.11 best_loss=inf best_ppl=inf                                                        
Epoch 49 - |param|=6.64e+02 |g_param|=1.18e+05 loss=4.0880e-01 ppl=1.51                                                 
Validation - loss=7.6120e-01 ppl=2.14 best_loss=7.4487e-01 best_ppl=2.11                                                
Epoch 50 - |param|=6.64e+02 |g_param|=1.11e+05 loss=4.2382e-01 ppl=1.53                                                 
Validation - loss=7.4192e-01 ppl=2.10 best_loss=7.4487e-01 best_ppl=2.11                                                
Epoch 51 - |param|=6.65e+02 |g_param|=9.50e+04 loss=3.8502e-01 ppl=1.47                                                 
Validation - loss=7.4011e-01 ppl=2.10 best_loss=7.4192e-01 best_ppl=2.10                                                
Epoch 52 - |param|=6.65e+02 |g_param|=1.01e+05 loss=3.7131e-01 ppl=1.45                                                 
Validation - loss=7.5337e-01 ppl=2.12 best_loss=7.4011e-01 best_ppl=2.10                                                
Epoch 53 - |param|=6.65e+02 |g_param|=1.07e+05 loss=3.8713e-01 ppl=1.47                                                 
Validation - loss=7.4790e-01 ppl=2.11 best_loss=7.4011e-01 best_ppl=2.10                                                
Epoch 54 - |param|=6.66e+02 |g_param|=1.09e+05 loss=3.7206e-01 ppl=1.45                                                 
Validation - loss=7.4440e-01 ppl=2.11 best_loss=7.4011e-01 best_ppl=2.10                                                
Epoch 55 - |param|=6.66e+02 |g_param|=1.01e+05 loss=3.5875e-01 ppl=1.43                                                 
Validation - loss=7.4736e-01 ppl=2.11 best_loss=7.4011e-01 best_ppl=2.10                                                
Epoch 56 - |param|=6.66e+02 |g_param|=8.54e+04 loss=3.3499e-01 ppl=1.40                                                 
Validation - loss=7.2055e-01 ppl=2.06 best_loss=7.4011e-01 best_ppl=2.10                                                
Epoch 57 - |param|=6.67e+02 |g_param|=9.60e+04 loss=3.3695e-01 ppl=1.40                                                 
Validation - loss=7.3836e-01 ppl=2.09 best_loss=7.2055e-01 best_ppl=2.06                                                
Epoch 58 - |param|=6.67e+02 |g_param|=1.02e+05 loss=3.5595e-01 ppl=1.43                                                 
Validation - loss=7.1129e-01 ppl=2.04 best_loss=7.2055e-01 best_ppl=2.06                                                
Epoch 59 - |param|=6.67e+02 |g_param|=9.81e+04 loss=3.4636e-01 ppl=1.41                                                 
Validation - loss=7.2223e-01 ppl=2.06 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 60 - |param|=6.68e+02 |g_param|=9.45e+04 loss=3.2522e-01 ppl=1.38                                                 
Validation - loss=7.2461e-01 ppl=2.06 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 61 - |param|=6.68e+02 |g_param|=8.58e+04 loss=3.2640e-01 ppl=1.39                                                 
Validation - loss=7.4522e-01 ppl=2.11 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 62 - |param|=6.68e+02 |g_param|=8.07e+04 loss=3.1219e-01 ppl=1.37                                                 
Validation - loss=7.2933e-01 ppl=2.07 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 63 - |param|=6.69e+02 |g_param|=9.48e+04 loss=3.0860e-01 ppl=1.36                                                 
Validation - loss=7.3569e-01 ppl=2.09 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 64 - |param|=6.69e+02 |g_param|=8.76e+04 loss=3.2604e-01 ppl=1.39                                                 
Validation - loss=7.4785e-01 ppl=2.11 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 65 - |param|=6.69e+02 |g_param|=4.79e+04 loss=3.1231e-01 ppl=1.37                                                 
Validation - loss=7.2642e-01 ppl=2.07 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 66 - |param|=6.70e+02 |g_param|=5.04e+04 loss=3.1048e-01 ppl=1.36                                                 
Validation - loss=7.2682e-01 ppl=2.07 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 67 - |param|=6.70e+02 |g_param|=4.64e+04 loss=3.0757e-01 ppl=1.36                                                 
Validation - loss=7.1680e-01 ppl=2.05 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 68 - |param|=6.70e+02 |g_param|=4.32e+04 loss=2.8376e-01 ppl=1.33                                                 
Validation - loss=7.3025e-01 ppl=2.08 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 69 - |param|=6.71e+02 |g_param|=5.19e+04 loss=2.9865e-01 ppl=1.35                                                 
Validation - loss=7.3102e-01 ppl=2.08 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 70 - |param|=6.71e+02 |g_param|=4.62e+04 loss=2.8562e-01 ppl=1.33                                                 
Validation - loss=7.0313e-01 ppl=2.02 best_loss=7.1129e-01 best_ppl=2.04                                                
Epoch 71 - |param|=6.71e+02 |g_param|=4.22e+04 loss=2.8278e-01 ppl=1.33                                                 
Validation - loss=7.4323e-01 ppl=2.10 best_loss=7.0313e-01 best_ppl=2.02                                                
Epoch 72 - |param|=6.72e+02 |g_param|=2.37e+04 loss=2.7823e-01 ppl=1.32                                                 
Validation - loss=7.1944e-01 ppl=2.05 best_loss=7.0313e-01 best_ppl=2.02                                                
Epoch 73 - |param|=6.72e+02 |g_param|=2.63e+04 loss=2.7922e-01 ppl=1.32                                                 
Validation - loss=7.0301e-01 ppl=2.02 best_loss=7.0313e-01 best_ppl=2.02                                                
Epoch 74 - |param|=6.72e+02 |g_param|=3.09e+04 loss=3.0616e-01 ppl=1.36                                                 
Validation - loss=7.5033e-01 ppl=2.12 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 75 - |param|=6.73e+02 |g_param|=2.65e+04 loss=2.8673e-01 ppl=1.33                                                 
Validation - loss=7.1512e-01 ppl=2.04 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 76 - |param|=6.73e+02 |g_param|=2.13e+04 loss=2.5779e-01 ppl=1.29                                                 
Validation - loss=7.5144e-01 ppl=2.12 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 77 - |param|=6.73e+02 |g_param|=2.47e+04 loss=2.8322e-01 ppl=1.33                                                 
Validation - loss=7.1144e-01 ppl=2.04 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 78 - |param|=6.74e+02 |g_param|=2.06e+04 loss=2.6851e-01 ppl=1.31                                                 
Validation - loss=7.1632e-01 ppl=2.05 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 79 - |param|=6.74e+02 |g_param|=1.90e+04 loss=2.5022e-01 ppl=1.28                                                 
Validation - loss=7.2227e-01 ppl=2.06 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 80 - |param|=6.74e+02 |g_param|=1.98e+04 loss=2.4755e-01 ppl=1.28                                                 
Validation - loss=7.1418e-01 ppl=2.04 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 81 - |param|=6.75e+02 |g_param|=1.86e+04 loss=2.4033e-01 ppl=1.27                                                 
Validation - loss=7.1816e-01 ppl=2.05 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 82 - |param|=6.75e+02 |g_param|=1.84e+04 loss=2.3553e-01 ppl=1.27                                                 
Validation - loss=7.4550e-01 ppl=2.11 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 83 - |param|=6.75e+02 |g_param|=2.02e+04 loss=2.3801e-01 ppl=1.27                                                 
Validation - loss=7.3326e-01 ppl=2.08 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 84 - |param|=6.75e+02 |g_param|=1.98e+04 loss=2.4038e-01 ppl=1.27                                                 
Validation - loss=7.3666e-01 ppl=2.09 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 85 - |param|=6.76e+02 |g_param|=1.91e+04 loss=2.2640e-01 ppl=1.25                                                 
Validation - loss=7.2653e-01 ppl=2.07 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 86 - |param|=6.76e+02 |g_param|=2.06e+04 loss=2.4334e-01 ppl=1.28                                                 
Validation - loss=7.4491e-01 ppl=2.11 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 87 - |param|=6.76e+02 |g_param|=2.07e+04 loss=2.2803e-01 ppl=1.26                                                 
Validation - loss=7.2948e-01 ppl=2.07 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 88 - |param|=6.77e+02 |g_param|=2.24e+04 loss=2.1898e-01 ppl=1.24                                                 
Validation - loss=7.4654e-01 ppl=2.11 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 89 - |param|=6.77e+02 |g_param|=2.00e+04 loss=2.3348e-01 ppl=1.26                                                 
Validation - loss=7.4254e-01 ppl=2.10 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 90 - |param|=6.77e+02 |g_param|=1.73e+04 loss=2.1303e-01 ppl=1.24                                                 
Validation - loss=7.4442e-01 ppl=2.11 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 91 - |param|=6.78e+02 |g_param|=2.40e+04 loss=2.2435e-01 ppl=1.25                                                 
Validation - loss=7.5250e-01 ppl=2.12 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 92 - |param|=6.78e+02 |g_param|=2.61e+04 loss=2.1400e-01 ppl=1.24                                                 
Validation - loss=7.4273e-01 ppl=2.10 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 93 - |param|=6.78e+02 |g_param|=4.20e+04 loss=2.1710e-01 ppl=1.24                                                 
Validation - loss=7.5757e-01 ppl=2.13 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 94 - |param|=6.79e+02 |g_param|=5.23e+04 loss=2.2473e-01 ppl=1.25                                                 
Validation - loss=7.3587e-01 ppl=2.09 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 95 - |param|=6.79e+02 |g_param|=4.80e+04 loss=2.2621e-01 ppl=1.25                                                 
Validation - loss=7.4267e-01 ppl=2.10 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 96 - |param|=6.79e+02 |g_param|=3.70e+04 loss=2.0627e-01 ppl=1.23                                                 
Validation - loss=7.6078e-01 ppl=2.14 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 97 - |param|=6.79e+02 |g_param|=3.66e+04 loss=1.9707e-01 ppl=1.22                                                 
Validation - loss=7.3853e-01 ppl=2.09 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 98 - |param|=6.80e+02 |g_param|=3.82e+04 loss=2.0362e-01 ppl=1.23                                                 
Validation - loss=7.4907e-01 ppl=2.12 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 99 - |param|=6.80e+02 |g_param|=4.71e+04 loss=2.0310e-01 ppl=1.23                                                 
Validation - loss=7.6065e-01 ppl=2.14 best_loss=7.0301e-01 best_ppl=2.02                                                
Epoch 100 - |param|=6.80e+02 |g_param|=3.42e+04 loss=1.9288e-01 ppl=1.21                                                
Validation - loss=7.4523e-01 ppl=2.11 best_loss=7.0301e-01 best_ppl=2.02                                                

real	10m5.754s
user	9m54.488s
sys	0m9.052s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.100.0.19-1.21.0.75-2.11.pth
BLEU = 74.40, 87.5/78.2/70.4/63.6 (BP=1.000, ratio=1.032, hyp_len=23904, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.48.0.41-1.50.0.74-2.11.pth
BLEU = 73.26, 87.1/77.2/69.0/62.0 (BP=1.000, ratio=1.022, hyp_len=23659, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.49.0.41-1.51.0.76-2.14.pth
BLEU = 73.55, 87.5/77.5/69.3/62.3 (BP=1.000, ratio=1.014, hyp_len=23484, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.50.0.42-1.53.0.74-2.10.pth
BLEU = 72.22, 86.5/76.3/67.9/60.7 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.51.0.39-1.47.0.74-2.10.pth
BLEU = 72.45, 86.6/76.5/68.1/61.1 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.52.0.37-1.45.0.75-2.12.pth
BLEU = 72.52, 86.7/76.6/68.2/61.1 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.53.0.39-1.47.0.75-2.11.pth
BLEU = 72.01, 86.2/76.1/67.7/60.5 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.54.0.37-1.45.0.74-2.11.pth
BLEU = 73.04, 87.0/77.1/68.8/61.7 (BP=1.000, ratio=1.026, hyp_len=23759, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.55.0.36-1.43.0.75-2.11.pth
BLEU = 73.03, 87.0/77.1/68.8/61.6 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.56.0.33-1.40.0.72-2.06.pth
BLEU = 74.12, 87.7/78.0/69.9/63.1 (BP=1.000, ratio=1.021, hyp_len=23656, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.57.0.34-1.40.0.74-2.09.pth
BLEU = 72.54, 86.6/76.7/68.3/61.1 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.58.0.36-1.43.0.71-2.04.pth
BLEU = 73.79, 87.5/77.7/69.5/62.7 (BP=1.000, ratio=1.024, hyp_len=23712, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.59.0.35-1.41.0.72-2.06.pth
BLEU = 72.80, 86.7/76.9/68.6/61.5 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.60.0.33-1.38.0.72-2.06.pth
BLEU = 73.79, 87.5/77.7/69.6/62.6 (BP=1.000, ratio=1.025, hyp_len=23739, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.61.0.33-1.39.0.75-2.11.pth
BLEU = 72.91, 86.8/76.9/68.6/61.7 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.62.0.31-1.37.0.73-2.07.pth
BLEU = 73.81, 87.3/77.6/69.6/62.9 (BP=1.000, ratio=1.026, hyp_len=23771, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.63.0.31-1.36.0.74-2.09.pth
BLEU = 74.58, 87.7/78.3/70.5/63.9 (BP=1.000, ratio=1.024, hyp_len=23716, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.64.0.33-1.39.0.75-2.11.pth
BLEU = 73.87, 87.3/77.7/69.7/63.0 (BP=1.000, ratio=1.027, hyp_len=23779, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.65.0.31-1.37.0.73-2.07.pth
BLEU = 73.64, 87.2/77.6/69.5/62.6 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.66.0.31-1.36.0.73-2.07.pth
BLEU = 73.62, 87.2/77.6/69.5/62.6 (BP=1.000, ratio=1.028, hyp_len=23808, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.67.0.31-1.36.0.72-2.05.pth
BLEU = 73.48, 87.1/77.4/69.3/62.4 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.68.0.28-1.33.0.73-2.08.pth
BLEU = 74.58, 88.2/78.4/70.4/63.6 (BP=1.000, ratio=1.017, hyp_len=23565, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.69.0.30-1.35.0.73-2.08.pth
BLEU = 73.07, 86.7/76.9/68.9/62.0 (BP=1.000, ratio=1.033, hyp_len=23919, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.70.0.29-1.33.0.70-2.02.pth
BLEU = 73.70, 87.1/77.5/69.5/62.8 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.71.0.28-1.33.0.74-2.10.pth
BLEU = 73.13, 86.8/77.0/68.8/62.1 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.72.0.28-1.32.0.72-2.05.pth
BLEU = 73.33, 87.0/77.3/69.2/62.1 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.73.0.28-1.32.0.70-2.02.pth
BLEU = 72.99, 86.8/77.0/68.8/61.7 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.74.0.31-1.36.0.75-2.12.pth
BLEU = 73.47, 87.1/77.4/69.3/62.4 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.75.0.29-1.33.0.72-2.04.pth
BLEU = 73.85, 87.3/77.8/69.7/62.8 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.76.0.26-1.29.0.75-2.12.pth
BLEU = 73.58, 87.3/77.5/69.4/62.5 (BP=1.000, ratio=1.025, hyp_len=23744, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.77.0.28-1.33.0.71-2.04.pth
BLEU = 74.29, 87.5/78.1/70.2/63.4 (BP=1.000, ratio=1.025, hyp_len=23750, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.78.0.27-1.31.0.72-2.05.pth
BLEU = 74.03, 87.4/77.8/69.9/63.2 (BP=1.000, ratio=1.026, hyp_len=23756, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.79.0.25-1.28.0.72-2.06.pth
BLEU = 73.10, 86.7/77.0/68.9/62.1 (BP=1.000, ratio=1.035, hyp_len=23964, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.80.0.25-1.28.0.71-2.04.pth
BLEU = 73.37, 86.9/77.2/69.2/62.4 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.81.0.24-1.27.0.72-2.05.pth
BLEU = 73.90, 87.2/77.8/69.8/63.0 (BP=1.000, ratio=1.029, hyp_len=23837, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.82.0.24-1.27.0.75-2.11.pth
BLEU = 73.58, 87.4/77.6/69.3/62.4 (BP=1.000, ratio=1.029, hyp_len=23828, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.83.0.24-1.27.0.73-2.08.pth
BLEU = 74.72, 87.7/78.5/70.7/64.0 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.84.0.24-1.27.0.74-2.09.pth
BLEU = 73.90, 87.2/77.7/69.8/63.1 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.85.0.23-1.25.0.73-2.07.pth
BLEU = 74.06, 87.3/77.8/70.0/63.3 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.86.0.24-1.28.0.74-2.11.pth
BLEU = 72.52, 86.3/76.5/68.3/61.3 (BP=1.000, ratio=1.039, hyp_len=24074, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.87.0.23-1.26.0.73-2.07.pth
BLEU = 73.50, 86.9/77.4/69.4/62.5 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.22-1.24.0.75-2.11.pth
BLEU = 73.19, 87.0/77.2/68.9/62.0 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.23-1.26.0.74-2.10.pth
BLEU = 73.09, 86.7/77.1/68.9/62.0 (BP=1.000, ratio=1.037, hyp_len=24019, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.21-1.24.0.74-2.11.pth
BLEU = 73.92, 87.3/77.8/69.8/63.0 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.22-1.25.0.75-2.12.pth
BLEU = 73.57, 86.9/77.3/69.4/62.8 (BP=1.000, ratio=1.034, hyp_len=23946, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.21-1.24.0.74-2.10.pth
BLEU = 73.21, 86.9/77.2/69.0/62.0 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.22-1.24.0.76-2.13.pth
BLEU = 73.16, 86.6/77.1/69.0/62.2 (BP=1.000, ratio=1.035, hyp_len=23969, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.22-1.25.0.74-2.09.pth
BLEU = 73.35, 86.7/77.2/69.2/62.4 (BP=1.000, ratio=1.035, hyp_len=23976, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.23-1.25.0.74-2.10.pth
BLEU = 74.13, 87.4/77.9/70.1/63.3 (BP=1.000, ratio=1.025, hyp_len=23739, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.21-1.23.0.76-2.14.pth
BLEU = 74.03, 87.2/77.8/70.0/63.2 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.20-1.22.0.74-2.09.pth
BLEU = 73.39, 86.9/77.3/69.2/62.4 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.20-1.23.0.75-2.12.pth
BLEU = 73.63, 86.9/77.5/69.6/62.7 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.20-1.23.0.76-2.14.pth
BLEU = 72.90, 86.5/76.8/68.7/61.9 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)

real	17m30.449s
user	16m57.446s
sys	1m2.031s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-50epoch$ 
```

Baseline က seq-model-myrk.48.0.43-1.54.0.76-2.14.pth: BLEU = 73.15  
RL, my-rk, 50-50 model ရဲ့ best score က  

```
Evaluation result for the model: seq-rl-model-myrk.83.0.24-1.27.0.73-2.08.pth
BLEU = 74.72, 87.7/78.5/70.7/64.0 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
```

### RL, my-rk, 60-40 model

training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.55.0.29-1.33.0.65-1.91.pth --model_fn ./model/rl/seq2seq/myrk-60epoch/seq-rl-model-myrk.pth --init_epoch 55 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.55.0.29-1.33.0.65-1.91.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/myrk-60epoch/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 55
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 55,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.55.0.29-1.33.0.65-1.91.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/myrk-60epoch/seq-rl-model-myrk.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 55 - |param|=6.68e+02 |g_param|=1.85e+05 loss=2.9336e-01 ppl=1.34                                                 
Validation - loss=6.5249e-01 ppl=1.92 best_loss=inf best_ppl=inf                                                        
Epoch 56 - |param|=6.69e+02 |g_param|=1.56e+05 loss=2.7864e-01 ppl=1.32                                                 
Validation - loss=6.5805e-01 ppl=1.93 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 57 - |param|=6.69e+02 |g_param|=1.45e+05 loss=2.6434e-01 ppl=1.30                                                 
Validation - loss=6.7821e-01 ppl=1.97 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 58 - |param|=6.69e+02 |g_param|=1.70e+05 loss=2.7655e-01 ppl=1.32                                                 
Validation - loss=6.6804e-01 ppl=1.95 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 59 - |param|=6.70e+02 |g_param|=9.31e+04 loss=2.7443e-01 ppl=1.32                                                 
Validation - loss=6.7126e-01 ppl=1.96 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 60 - |param|=6.70e+02 |g_param|=8.46e+04 loss=2.6246e-01 ppl=1.30                                                 
Validation - loss=6.6637e-01 ppl=1.95 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 61 - |param|=6.70e+02 |g_param|=6.95e+04 loss=2.4734e-01 ppl=1.28                                                 
Validation - loss=6.4762e-01 ppl=1.91 best_loss=6.5249e-01 best_ppl=1.92                                                
Epoch 62 - |param|=6.70e+02 |g_param|=7.93e+04 loss=2.5302e-01 ppl=1.29                                                 
Validation - loss=6.6894e-01 ppl=1.95 best_loss=6.4762e-01 best_ppl=1.91                                                
Epoch 63 - |param|=6.71e+02 |g_param|=9.84e+04 loss=2.5193e-01 ppl=1.29                                                 
Validation - loss=6.6451e-01 ppl=1.94 best_loss=6.4762e-01 best_ppl=1.91                                                
Epoch 64 - |param|=6.71e+02 |g_param|=1.02e+05 loss=2.5684e-01 ppl=1.29                                                 
Validation - loss=6.5390e-01 ppl=1.92 best_loss=6.4762e-01 best_ppl=1.91                                                
Epoch 65 - |param|=6.71e+02 |g_param|=1.04e+05 loss=2.6612e-01 ppl=1.30                                                 
Validation - loss=6.5775e-01 ppl=1.93 best_loss=6.4762e-01 best_ppl=1.91                                                
Epoch 66 - |param|=6.72e+02 |g_param|=4.35e+04 loss=2.5075e-01 ppl=1.28                                                 
Validation - loss=6.4484e-01 ppl=1.91 best_loss=6.4762e-01 best_ppl=1.91                                                
Epoch 67 - |param|=6.72e+02 |g_param|=4.12e+04 loss=2.4886e-01 ppl=1.28                                                 
Validation - loss=6.5103e-01 ppl=1.92 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 68 - |param|=6.72e+02 |g_param|=4.22e+04 loss=2.3423e-01 ppl=1.26                                                 
Validation - loss=6.5966e-01 ppl=1.93 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 69 - |param|=6.73e+02 |g_param|=4.66e+04 loss=2.3437e-01 ppl=1.26                                                 
Validation - loss=6.7108e-01 ppl=1.96 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 70 - |param|=6.73e+02 |g_param|=5.41e+04 loss=2.7162e-01 ppl=1.31                                                 
Validation - loss=6.5720e-01 ppl=1.93 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 71 - |param|=6.74e+02 |g_param|=3.76e+04 loss=2.2812e-01 ppl=1.26                                                 
Validation - loss=6.5241e-01 ppl=1.92 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 72 - |param|=6.74e+02 |g_param|=3.96e+04 loss=2.3092e-01 ppl=1.26                                                 
Validation - loss=6.5305e-01 ppl=1.92 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 73 - |param|=6.74e+02 |g_param|=3.39e+04 loss=2.1818e-01 ppl=1.24                                                 
Validation - loss=6.4663e-01 ppl=1.91 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 74 - |param|=6.74e+02 |g_param|=3.76e+04 loss=2.1659e-01 ppl=1.24                                                 
Validation - loss=6.5608e-01 ppl=1.93 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 75 - |param|=6.75e+02 |g_param|=3.30e+04 loss=2.0955e-01 ppl=1.23                                                 
Validation - loss=6.5205e-01 ppl=1.92 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 76 - |param|=6.75e+02 |g_param|=3.73e+04 loss=2.0952e-01 ppl=1.23                                                 
Validation - loss=6.8979e-01 ppl=1.99 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 77 - |param|=6.75e+02 |g_param|=3.60e+04 loss=2.0587e-01 ppl=1.23                                                 
Validation - loss=6.6452e-01 ppl=1.94 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 78 - |param|=6.76e+02 |g_param|=4.28e+04 loss=1.9664e-01 ppl=1.22                                                 
Validation - loss=6.8202e-01 ppl=1.98 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 79 - |param|=6.76e+02 |g_param|=3.67e+04 loss=2.0174e-01 ppl=1.22                                                 
Validation - loss=6.7959e-01 ppl=1.97 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 80 - |param|=6.76e+02 |g_param|=4.24e+04 loss=2.0217e-01 ppl=1.22                                                 
Validation - loss=6.9621e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 81 - |param|=6.76e+02 |g_param|=4.23e+04 loss=2.0136e-01 ppl=1.22                                                 
Validation - loss=6.8694e-01 ppl=1.99 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 82 - |param|=6.77e+02 |g_param|=3.83e+04 loss=2.0199e-01 ppl=1.22                                                 
Validation - loss=6.5591e-01 ppl=1.93 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 83 - |param|=6.77e+02 |g_param|=3.76e+04 loss=1.9510e-01 ppl=1.22                                                 
Validation - loss=6.7592e-01 ppl=1.97 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 84 - |param|=6.77e+02 |g_param|=4.04e+04 loss=1.9040e-01 ppl=1.21                                                 
Validation - loss=6.9830e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 85 - |param|=6.78e+02 |g_param|=4.01e+04 loss=1.9050e-01 ppl=1.21                                                 
Validation - loss=7.1515e-01 ppl=2.04 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 86 - |param|=6.78e+02 |g_param|=6.84e+04 loss=1.8421e-01 ppl=1.20                                                 
Validation - loss=6.9741e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 87 - |param|=6.78e+02 |g_param|=6.81e+04 loss=1.7189e-01 ppl=1.19                                                 
Validation - loss=6.6319e-01 ppl=1.94 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 88 - |param|=6.79e+02 |g_param|=7.41e+04 loss=1.7687e-01 ppl=1.19                                                 
Validation - loss=6.9929e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 89 - |param|=6.79e+02 |g_param|=8.25e+04 loss=1.7065e-01 ppl=1.19                                                 
Validation - loss=7.0499e-01 ppl=2.02 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 90 - |param|=6.79e+02 |g_param|=4.63e+04 loss=1.7797e-01 ppl=1.19                                                 
Validation - loss=7.0459e-01 ppl=2.02 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 91 - |param|=6.80e+02 |g_param|=4.64e+04 loss=1.7785e-01 ppl=1.19                                                 
Validation - loss=6.9606e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 92 - |param|=6.80e+02 |g_param|=5.15e+04 loss=1.7770e-01 ppl=1.19                                                 
Validation - loss=7.2194e-01 ppl=2.06 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 93 - |param|=6.80e+02 |g_param|=2.21e+04 loss=1.9573e-01 ppl=1.22                                                 
Validation - loss=7.0436e-01 ppl=2.02 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 94 - |param|=6.81e+02 |g_param|=2.33e+04 loss=1.8572e-01 ppl=1.20                                                 
Validation - loss=7.0205e-01 ppl=2.02 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 95 - |param|=6.81e+02 |g_param|=2.22e+04 loss=1.8752e-01 ppl=1.21                                                 
Validation - loss=6.9773e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 96 - |param|=6.81e+02 |g_param|=1.86e+04 loss=1.6675e-01 ppl=1.18                                                 
Validation - loss=6.9962e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 97 - |param|=6.82e+02 |g_param|=1.68e+04 loss=1.6117e-01 ppl=1.17                                                 
Validation - loss=6.9092e-01 ppl=2.00 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 98 - |param|=6.82e+02 |g_param|=1.67e+04 loss=1.6017e-01 ppl=1.17                                                 
Validation - loss=6.8738e-01 ppl=1.99 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 99 - |param|=6.82e+02 |g_param|=1.84e+04 loss=1.5679e-01 ppl=1.17                                                 
Validation - loss=7.0023e-01 ppl=2.01 best_loss=6.4484e-01 best_ppl=1.91                                                
Epoch 100 - |param|=6.82e+02 |g_param|=2.17e+04 loss=1.5890e-01 ppl=1.17                                                
Validation - loss=7.0377e-01 ppl=2.02 best_loss=6.4484e-01 best_ppl=1.91                                                

real	9m2.986s
user	8m53.723s
sys	0m7.988s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.100.0.16-1.17.0.70-2.02.pth
BLEU = 74.85, 87.5/78.5/70.9/64.4 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.55.0.29-1.34.0.65-1.92.pth
BLEU = 74.12, 87.5/77.9/70.0/63.2 (BP=1.000, ratio=1.031, hyp_len=23870, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.56.0.28-1.32.0.66-1.93.pth
BLEU = 75.10, 88.1/78.8/71.1/64.5 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.57.0.26-1.30.0.68-1.97.pth
BLEU = 74.50, 87.8/78.2/70.4/63.7 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.58.0.28-1.32.0.67-1.95.pth
BLEU = 74.10, 87.3/77.8/70.0/63.4 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.59.0.27-1.32.0.67-1.96.pth
BLEU = 74.75, 87.8/78.4/70.7/64.2 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.60.0.26-1.30.0.67-1.95.pth
BLEU = 73.52, 87.0/77.4/69.4/62.5 (BP=1.000, ratio=1.037, hyp_len=24012, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.61.0.25-1.28.0.65-1.91.pth
BLEU = 74.58, 87.6/78.3/70.6/63.9 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.62.0.25-1.29.0.67-1.95.pth
BLEU = 72.95, 86.6/76.8/68.7/61.9 (BP=1.000, ratio=1.039, hyp_len=24066, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.63.0.25-1.29.0.66-1.94.pth
BLEU = 73.86, 87.4/77.8/69.7/62.8 (BP=1.000, ratio=1.031, hyp_len=23871, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.64.0.26-1.29.0.65-1.92.pth
BLEU = 74.09, 87.5/77.9/69.9/63.2 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.65.0.27-1.30.0.66-1.93.pth
BLEU = 74.75, 87.8/78.4/70.7/64.1 (BP=1.000, ratio=1.026, hyp_len=23764, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.66.0.25-1.28.0.64-1.91.pth
BLEU = 75.11, 88.0/78.7/71.1/64.6 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.67.0.25-1.28.0.65-1.92.pth
BLEU = 74.74, 87.6/78.3/70.8/64.3 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.68.0.23-1.26.0.66-1.93.pth
BLEU = 74.02, 87.3/77.8/70.0/63.2 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.69.0.23-1.26.0.67-1.96.pth
BLEU = 74.76, 87.8/78.4/70.7/64.2 (BP=1.000, ratio=1.026, hyp_len=23764, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.70.0.27-1.31.0.66-1.93.pth
BLEU = 75.03, 88.0/78.7/71.0/64.4 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.71.0.23-1.26.0.65-1.92.pth
BLEU = 74.83, 87.7/78.4/70.8/64.3 (BP=1.000, ratio=1.029, hyp_len=23843, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.72.0.23-1.26.0.65-1.92.pth
BLEU = 74.54, 87.7/78.3/70.5/63.9 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.73.0.22-1.24.0.65-1.91.pth
BLEU = 74.51, 87.6/78.2/70.4/63.8 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.74.0.22-1.24.0.66-1.93.pth
BLEU = 74.66, 87.7/78.3/70.7/64.1 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.75.0.21-1.23.0.65-1.92.pth
BLEU = 74.40, 87.5/78.1/70.3/63.8 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.76.0.21-1.23.0.69-1.99.pth
BLEU = 73.52, 86.9/77.3/69.4/62.7 (BP=1.000, ratio=1.040, hyp_len=24082, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.77.0.21-1.23.0.66-1.94.pth
BLEU = 74.33, 87.5/78.0/70.3/63.6 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.78.0.20-1.22.0.68-1.98.pth
BLEU = 73.98, 87.1/77.7/70.0/63.3 (BP=1.000, ratio=1.038, hyp_len=24048, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.79.0.20-1.22.0.68-1.97.pth
BLEU = 74.13, 87.3/77.9/70.0/63.5 (BP=1.000, ratio=1.036, hyp_len=23989, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.80.0.20-1.22.0.70-2.01.pth
BLEU = 74.37, 87.3/78.0/70.4/63.8 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.81.0.20-1.22.0.69-1.99.pth
BLEU = 74.04, 87.1/77.7/70.0/63.4 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.82.0.20-1.22.0.66-1.93.pth
BLEU = 74.94, 87.7/78.5/71.0/64.5 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.83.0.20-1.22.0.68-1.97.pth
BLEU = 74.56, 87.7/78.3/70.5/63.8 (BP=1.000, ratio=1.032, hyp_len=23909, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.84.0.19-1.21.0.70-2.01.pth
BLEU = 74.61, 87.6/78.3/70.6/64.1 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.85.0.19-1.21.0.72-2.04.pth
BLEU = 73.86, 87.0/77.7/69.8/63.1 (BP=1.000, ratio=1.039, hyp_len=24074, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.86.0.18-1.20.0.70-2.01.pth
BLEU = 73.77, 86.9/77.5/69.7/63.1 (BP=1.000, ratio=1.040, hyp_len=24089, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.87.0.17-1.19.0.66-1.94.pth
BLEU = 74.22, 87.3/78.0/70.2/63.5 (BP=1.000, ratio=1.036, hyp_len=24004, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.18-1.19.0.70-2.01.pth
BLEU = 74.16, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.037, hyp_len=24020, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.17-1.19.0.70-2.02.pth
BLEU = 74.06, 87.1/77.8/70.1/63.4 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.18-1.19.0.70-2.02.pth
BLEU = 74.80, 87.8/78.5/70.8/64.2 (BP=1.000, ratio=1.030, hyp_len=23863, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.18-1.19.0.70-2.01.pth
BLEU = 74.29, 87.5/78.0/70.2/63.6 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.18-1.19.0.72-2.06.pth
BLEU = 73.55, 87.0/77.4/69.4/62.6 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.20-1.22.0.70-2.02.pth
BLEU = 74.36, 87.5/78.1/70.3/63.6 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.19-1.20.0.70-2.02.pth
BLEU = 73.68, 87.1/77.5/69.5/62.8 (BP=1.000, ratio=1.035, hyp_len=23981, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.19-1.21.0.70-2.01.pth
BLEU = 74.66, 87.6/78.3/70.6/64.2 (BP=1.000, ratio=1.033, hyp_len=23924, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.17-1.18.0.70-2.01.pth
BLEU = 75.03, 87.9/78.6/71.0/64.6 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.16-1.17.0.69-2.00.pth
BLEU = 74.72, 87.7/78.3/70.7/64.2 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.16-1.17.0.69-1.99.pth
BLEU = 74.90, 87.6/78.5/71.0/64.5 (BP=1.000, ratio=1.032, hyp_len=23893, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.16-1.17.0.70-2.01.pth
BLEU = 74.60, 87.6/78.3/70.6/64.0 (BP=1.000, ratio=1.030, hyp_len=23863, ref_len=23160)

real	16m41.922s
user	15m21.765s
sys	1m3.434s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-60epoch$
```

Baseline ရဲ့ အကောင်းဆုံး မော်ဒယ် ရဲ့ score က seq-model-myrk.55.0.29-1.33.0.65-1.91.pth: BLEU = 75.30  
RL ရဲ့ Best Score ပေးတဲ့ မော်ဒယ်က seq-rl-model-myrk.66.0.25-1.28.0.64-1.91.pth:  

```
Evaluation result for the model: seq-rl-model-myrk.66.0.25-1.28.0.64-1.91.pth
BLEU = 75.11, 88.0/78.7/71.1/64.6 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
```

### RL, my-rk, 70-30 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.61.0.33-1.40.0.77-2.17.pth --model_fn ./model/rl/seq2seq/myrk-70epoch/seq-rl-model-myrk.pth --init_epoch 61 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.61.0.33-1.40.0.77-2.17.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/myrk-70epoch/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 61
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 61,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.61.0.33-1.40.0.77-2.17.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/myrk-70epoch/seq-rl-model-myrk.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1539, 128)
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
Epoch 61 - |param|=6.68e+02 |g_param|=1.54e+05 loss=3.4458e-01 ppl=1.41                                                 
Validation - loss=7.6032e-01 ppl=2.14 best_loss=inf best_ppl=inf                                                        
Epoch 62 - |param|=6.69e+02 |g_param|=4.87e+04 loss=3.2112e-01 ppl=1.38                                                 
Validation - loss=7.6307e-01 ppl=2.14 best_loss=7.6032e-01 best_ppl=2.14                                                
Epoch 63 - |param|=6.69e+02 |g_param|=6.01e+04 loss=3.3373e-01 ppl=1.40                                                 
Validation - loss=7.5255e-01 ppl=2.12 best_loss=7.6032e-01 best_ppl=2.14                                                
Epoch 64 - |param|=6.69e+02 |g_param|=7.36e+04 loss=3.3110e-01 ppl=1.39                                                 
Validation - loss=7.5522e-01 ppl=2.13 best_loss=7.5255e-01 best_ppl=2.12                                                
Epoch 65 - |param|=6.70e+02 |g_param|=5.63e+04 loss=3.2924e-01 ppl=1.39                                                 
Validation - loss=7.5957e-01 ppl=2.14 best_loss=7.5255e-01 best_ppl=2.12                                                
Epoch 66 - |param|=6.70e+02 |g_param|=3.97e+04 loss=3.4583e-01 ppl=1.41                                                 
Validation - loss=7.6064e-01 ppl=2.14 best_loss=7.5255e-01 best_ppl=2.12                                                
Epoch 67 - |param|=6.70e+02 |g_param|=2.13e+04 loss=3.1646e-01 ppl=1.37                                                 
Validation - loss=7.4632e-01 ppl=2.11 best_loss=7.5255e-01 best_ppl=2.12                                                
Epoch 68 - |param|=6.71e+02 |g_param|=1.34e+04 loss=3.1268e-01 ppl=1.37                                                 
Validation - loss=7.6102e-01 ppl=2.14 best_loss=7.4632e-01 best_ppl=2.11                                                
Epoch 69 - |param|=6.71e+02 |g_param|=1.32e+04 loss=3.0183e-01 ppl=1.35                                                 
Validation - loss=7.4759e-01 ppl=2.11 best_loss=7.4632e-01 best_ppl=2.11                                                
Epoch 70 - |param|=6.71e+02 |g_param|=2.31e+04 loss=3.7552e-01 ppl=1.46                                                 
Validation - loss=7.6969e-01 ppl=2.16 best_loss=7.4632e-01 best_ppl=2.11                                                
Epoch 71 - |param|=6.72e+02 |g_param|=1.51e+04 loss=3.2989e-01 ppl=1.39                                                 
Validation - loss=7.3444e-01 ppl=2.08 best_loss=7.4632e-01 best_ppl=2.11                                                
Epoch 72 - |param|=6.72e+02 |g_param|=1.11e+04 loss=3.0956e-01 ppl=1.36                                                 
Validation - loss=7.4328e-01 ppl=2.10 best_loss=7.3444e-01 best_ppl=2.08                                                
Epoch 73 - |param|=6.72e+02 |g_param|=1.03e+04 loss=2.8975e-01 ppl=1.34                                                 
Validation - loss=7.2948e-01 ppl=2.07 best_loss=7.3444e-01 best_ppl=2.08                                                
Epoch 74 - |param|=6.73e+02 |g_param|=1.01e+04 loss=2.6656e-01 ppl=1.31                                                 
Validation - loss=7.4282e-01 ppl=2.10 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 75 - |param|=6.73e+02 |g_param|=1.02e+04 loss=2.6889e-01 ppl=1.31                                                 
Validation - loss=7.4265e-01 ppl=2.10 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 76 - |param|=6.73e+02 |g_param|=9.98e+03 loss=2.7195e-01 ppl=1.31                                                 
Validation - loss=7.5183e-01 ppl=2.12 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 77 - |param|=6.73e+02 |g_param|=1.00e+04 loss=2.6397e-01 ppl=1.30                                                 
Validation - loss=7.4771e-01 ppl=2.11 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 78 - |param|=6.74e+02 |g_param|=1.36e+04 loss=2.8122e-01 ppl=1.32                                                 
Validation - loss=7.4249e-01 ppl=2.10 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 79 - |param|=6.74e+02 |g_param|=2.36e+04 loss=2.9780e-01 ppl=1.35                                                 
Validation - loss=9.4039e-01 ppl=2.56 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 80 - |param|=6.74e+02 |g_param|=2.83e+04 loss=3.4257e-01 ppl=1.41                                                 
Validation - loss=7.3683e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 81 - |param|=6.75e+02 |g_param|=1.37e+04 loss=2.8869e-01 ppl=1.33                                                 
Validation - loss=7.3565e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 82 - |param|=6.75e+02 |g_param|=1.01e+04 loss=2.5640e-01 ppl=1.29                                                 
Validation - loss=7.3871e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 83 - |param|=6.75e+02 |g_param|=1.02e+04 loss=2.5400e-01 ppl=1.29                                                 
Validation - loss=7.3397e-01 ppl=2.08 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 84 - |param|=6.76e+02 |g_param|=1.23e+04 loss=2.5191e-01 ppl=1.29                                                 
Validation - loss=7.3280e-01 ppl=2.08 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 85 - |param|=6.76e+02 |g_param|=1.02e+04 loss=2.4520e-01 ppl=1.28                                                 
Validation - loss=7.3619e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 86 - |param|=6.76e+02 |g_param|=9.26e+03 loss=2.3964e-01 ppl=1.27                                                 
Validation - loss=7.3786e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 87 - |param|=6.76e+02 |g_param|=9.95e+03 loss=2.4032e-01 ppl=1.27                                                 
Validation - loss=7.4677e-01 ppl=2.11 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 88 - |param|=6.77e+02 |g_param|=2.07e+04 loss=2.3734e-01 ppl=1.27                                                 
Validation - loss=7.3810e-01 ppl=2.09 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 89 - |param|=6.77e+02 |g_param|=2.64e+04 loss=2.3743e-01 ppl=1.27                                                 
Validation - loss=7.4307e-01 ppl=2.10 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 90 - |param|=6.77e+02 |g_param|=1.94e+04 loss=2.2853e-01 ppl=1.26                                                 
Validation - loss=7.4607e-01 ppl=2.11 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 91 - |param|=6.78e+02 |g_param|=2.03e+04 loss=2.4787e-01 ppl=1.28                                                 
Validation - loss=7.5511e-01 ppl=2.13 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 92 - |param|=6.78e+02 |g_param|=2.77e+04 loss=2.3459e-01 ppl=1.26                                                 
Validation - loss=7.8842e-01 ppl=2.20 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 93 - |param|=6.78e+02 |g_param|=2.53e+04 loss=2.4025e-01 ppl=1.27                                                 
Validation - loss=7.7561e-01 ppl=2.17 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 94 - |param|=6.79e+02 |g_param|=2.30e+04 loss=2.2998e-01 ppl=1.26                                                 
Validation - loss=7.6131e-01 ppl=2.14 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 95 - |param|=6.79e+02 |g_param|=1.96e+04 loss=2.2383e-01 ppl=1.25                                                 
Validation - loss=7.5316e-01 ppl=2.12 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 96 - |param|=6.79e+02 |g_param|=2.10e+04 loss=2.2714e-01 ppl=1.26                                                 
Validation - loss=7.5037e-01 ppl=2.12 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 97 - |param|=6.79e+02 |g_param|=1.86e+04 loss=2.1878e-01 ppl=1.24                                                 
Validation - loss=7.5531e-01 ppl=2.13 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 98 - |param|=6.80e+02 |g_param|=2.02e+04 loss=2.1400e-01 ppl=1.24                                                 
Validation - loss=7.5831e-01 ppl=2.13 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 99 - |param|=6.80e+02 |g_param|=1.93e+04 loss=2.1804e-01 ppl=1.24                                                 
Validation - loss=7.5748e-01 ppl=2.13 best_loss=7.2948e-01 best_ppl=2.07                                                
Epoch 100 - |param|=6.80e+02 |g_param|=2.00e+04 loss=2.1054e-01 ppl=1.23                                                
Validation - loss=7.5331e-01 ppl=2.12 best_loss=7.2948e-01 best_ppl=2.07                                                

real	7m51.590s
user	7m41.981s
sys	0m7.505s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.61.0.34-1.41.0.76-2.14.pth
BLEU = 73.86, 87.3/77.7/69.7/63.0 (BP=1.000, ratio=1.022, hyp_len=23677, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.62.0.32-1.38.0.76-2.14.pth
BLEU = 74.17, 87.6/78.0/70.0/63.2 (BP=1.000, ratio=1.024, hyp_len=23724, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.63.0.33-1.40.0.75-2.12.pth
BLEU = 73.79, 87.3/77.7/69.6/62.8 (BP=1.000, ratio=1.025, hyp_len=23738, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.64.0.33-1.39.0.76-2.13.pth
BLEU = 74.16, 87.5/78.0/70.0/63.3 (BP=1.000, ratio=1.024, hyp_len=23723, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.65.0.33-1.39.0.76-2.14.pth
BLEU = 73.48, 87.1/77.4/69.3/62.4 (BP=1.000, ratio=1.026, hyp_len=23773, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.66.0.35-1.41.0.76-2.14.pth
BLEU = 72.78, 86.7/76.8/68.5/61.5 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.67.0.32-1.37.0.75-2.11.pth
BLEU = 74.03, 87.4/77.9/69.9/63.2 (BP=1.000, ratio=1.024, hyp_len=23708, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.68.0.31-1.37.0.76-2.14.pth
BLEU = 73.04, 86.9/77.1/68.8/61.8 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.69.0.30-1.35.0.75-2.11.pth
BLEU = 73.85, 87.5/77.7/69.7/62.8 (BP=1.000, ratio=1.022, hyp_len=23679, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.70.0.38-1.46.0.77-2.16.pth
BLEU = 72.93, 86.8/76.9/68.7/61.7 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.71.0.33-1.39.0.73-2.08.pth
BLEU = 74.63, 87.9/78.4/70.6/63.8 (BP=1.000, ratio=1.024, hyp_len=23719, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.72.0.31-1.36.0.74-2.10.pth
BLEU = 74.30, 87.4/78.0/70.3/63.6 (BP=1.000, ratio=1.027, hyp_len=23787, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.73.0.29-1.34.0.73-2.07.pth
BLEU = 74.10, 87.3/77.9/70.0/63.3 (BP=1.000, ratio=1.027, hyp_len=23783, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.74.0.27-1.31.0.74-2.10.pth
BLEU = 74.66, 87.7/78.3/70.6/64.0 (BP=1.000, ratio=1.025, hyp_len=23750, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.75.0.27-1.31.0.74-2.10.pth
BLEU = 73.68, 87.1/77.5/69.5/62.8 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.76.0.27-1.31.0.75-2.12.pth
BLEU = 75.14, 88.1/78.8/71.1/64.6 (BP=1.000, ratio=1.020, hyp_len=23634, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.77.0.26-1.30.0.75-2.11.pth
BLEU = 74.54, 87.5/78.2/70.6/63.9 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.78.0.28-1.32.0.74-2.10.pth
BLEU = 73.46, 86.8/77.2/69.4/62.7 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.79.0.30-1.35.0.94-2.56.pth
BLEU = 67.39, 83.5/72.6/62.7/54.2 (BP=1.000, ratio=1.062, hyp_len=24607, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.80.0.34-1.41.0.74-2.09.pth
BLEU = 73.39, 87.0/77.3/69.2/62.4 (BP=1.000, ratio=1.025, hyp_len=23745, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.81.0.29-1.33.0.74-2.09.pth
BLEU = 73.76, 87.0/77.5/69.7/63.0 (BP=1.000, ratio=1.030, hyp_len=23852, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.82.0.26-1.29.0.74-2.09.pth
BLEU = 74.40, 87.6/78.1/70.3/63.8 (BP=1.000, ratio=1.028, hyp_len=23798, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.83.0.25-1.29.0.73-2.08.pth
BLEU = 74.90, 87.9/78.6/70.9/64.3 (BP=1.000, ratio=1.026, hyp_len=23764, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.84.0.25-1.29.0.73-2.08.pth
BLEU = 74.75, 87.7/78.4/70.7/64.3 (BP=1.000, ratio=1.024, hyp_len=23711, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.85.0.25-1.28.0.74-2.09.pth
BLEU = 75.01, 87.7/78.6/71.0/64.6 (BP=1.000, ratio=1.029, hyp_len=23828, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.86.0.24-1.27.0.74-2.09.pth
BLEU = 74.30, 87.5/78.0/70.2/63.7 (BP=1.000, ratio=1.028, hyp_len=23815, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.87.0.24-1.27.0.75-2.11.pth
BLEU = 73.88, 87.1/77.6/69.8/63.2 (BP=1.000, ratio=1.032, hyp_len=23890, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.24-1.27.0.74-2.09.pth
BLEU = 74.20, 87.4/77.9/70.1/63.5 (BP=1.000, ratio=1.026, hyp_len=23763, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.24-1.27.0.74-2.10.pth
BLEU = 75.06, 87.9/78.7/71.1/64.6 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.23-1.26.0.75-2.11.pth
BLEU = 74.44, 87.5/78.1/70.4/63.8 (BP=1.000, ratio=1.025, hyp_len=23749, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.25-1.28.0.76-2.13.pth
BLEU = 73.69, 87.0/77.4/69.6/62.9 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.23-1.26.0.79-2.20.pth
BLEU = 70.60, 85.2/74.8/66.2/58.8 (BP=1.000, ratio=1.036, hyp_len=24000, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.24-1.27.0.78-2.17.pth
BLEU = 73.75, 87.2/77.7/69.6/62.7 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.23-1.26.0.76-2.14.pth
BLEU = 74.07, 87.3/77.8/70.0/63.3 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.22-1.25.0.75-2.12.pth
BLEU = 74.90, 87.7/78.5/71.0/64.4 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.23-1.26.0.75-2.12.pth
BLEU = 74.60, 87.6/78.2/70.5/64.1 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.22-1.24.0.76-2.13.pth
BLEU = 74.75, 87.5/78.4/70.8/64.3 (BP=1.000, ratio=1.028, hyp_len=23811, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.21-1.24.0.76-2.13.pth
BLEU = 75.50, 88.2/79.1/71.6/65.1 (BP=1.000, ratio=1.023, hyp_len=23701, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.22-1.24.0.76-2.13.pth
BLEU = 74.14, 87.3/77.8/70.0/63.5 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.100.0.21-1.23.0.75-2.12.pth
BLEU = 74.78, 87.6/78.4/70.8/64.3 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)

real	14m35.868s
user	13m3.608s
sys	0m59.015s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/myrk-70epoch$
```

Baseline: seq-model-myrk.61.0.33-1.40.0.77-2.17.pth, BLEU = 74.36  
RL, my-rk, 70-30 ရဲ့ best score က  

```
Evaluation result for the model: seq-rl-model-myrk.98.0.21-1.24.0.76-2.13.pth
BLEU = 75.50, 88.2/79.1/71.6/65.1 (BP=1.000, ratio=1.023, hyp_len=23701, ref_len=23160)
```

*** for RK-My language pair ***  

### RL, rk-my, 40-60 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth --model_fn ./model/rl/seq2seq/rkmy-40epoch/seq-rl-model-rkmy.pth --init_epoch 39 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/rkmy-40epoch/seq-rl-model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 39
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 39,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'load_fn': './model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/rkmy-40epoch/seq-rl-model-rkmy.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 39 - |param|=6.60e+02 |g_param|=1.15e+05 loss=5.7597e-01 ppl=1.78                                                 
Validation - loss=8.2342e-01 ppl=2.28 best_loss=inf best_ppl=inf                                                        
Epoch 40 - |param|=6.61e+02 |g_param|=6.25e+04 loss=5.3424e-01 ppl=1.71                                                 
Validation - loss=8.2698e-01 ppl=2.29 best_loss=8.2342e-01 best_ppl=2.28                                                
Epoch 41 - |param|=6.61e+02 |g_param|=8.68e+04 loss=5.5408e-01 ppl=1.74                                                 
Validation - loss=8.8143e-01 ppl=2.41 best_loss=8.2342e-01 best_ppl=2.28                                                
Epoch 42 - |param|=6.61e+02 |g_param|=6.24e+04 loss=5.2621e-01 ppl=1.69                                                 
Validation - loss=8.0805e-01 ppl=2.24 best_loss=8.2342e-01 best_ppl=2.28                                                
Epoch 43 - |param|=6.62e+02 |g_param|=8.01e+04 loss=5.6256e-01 ppl=1.76                                                 
Validation - loss=8.3104e-01 ppl=2.30 best_loss=8.0805e-01 best_ppl=2.24                                                
Epoch 44 - |param|=6.62e+02 |g_param|=3.28e+04 loss=4.9466e-01 ppl=1.64                                                 
Validation - loss=7.9453e-01 ppl=2.21 best_loss=8.0805e-01 best_ppl=2.24                                                
Epoch 45 - |param|=6.62e+02 |g_param|=3.53e+04 loss=5.1040e-01 ppl=1.67                                                 
Validation - loss=8.0163e-01 ppl=2.23 best_loss=7.9453e-01 best_ppl=2.21                                                
Epoch 46 - |param|=6.63e+02 |g_param|=3.36e+04 loss=4.6948e-01 ppl=1.60                                                 
Validation - loss=7.9119e-01 ppl=2.21 best_loss=7.9453e-01 best_ppl=2.21                                                
Epoch 47 - |param|=6.63e+02 |g_param|=3.42e+04 loss=4.7542e-01 ppl=1.61                                                 
Validation - loss=8.0691e-01 ppl=2.24 best_loss=7.9119e-01 best_ppl=2.21                                                
Epoch 48 - |param|=6.63e+02 |g_param|=4.02e+04 loss=4.6602e-01 ppl=1.59                                                 
Validation - loss=7.7205e-01 ppl=2.16 best_loss=7.9119e-01 best_ppl=2.21                                                
Epoch 49 - |param|=6.64e+02 |g_param|=5.63e+04 loss=5.5446e-01 ppl=1.74                                                 
Validation - loss=8.1251e-01 ppl=2.25 best_loss=7.7205e-01 best_ppl=2.16                                                
Epoch 50 - |param|=6.64e+02 |g_param|=3.60e+04 loss=4.7746e-01 ppl=1.61                                                 
Validation - loss=7.7311e-01 ppl=2.17 best_loss=7.7205e-01 best_ppl=2.16                                                
Epoch 51 - |param|=6.65e+02 |g_param|=2.82e+04 loss=4.5143e-01 ppl=1.57                                                 
Validation - loss=7.9438e-01 ppl=2.21 best_loss=7.7205e-01 best_ppl=2.16                                                
Epoch 52 - |param|=6.65e+02 |g_param|=2.88e+04 loss=4.1207e-01 ppl=1.51                                                 
Validation - loss=7.6790e-01 ppl=2.16 best_loss=7.7205e-01 best_ppl=2.16                                                
Epoch 53 - |param|=6.65e+02 |g_param|=3.01e+04 loss=4.1897e-01 ppl=1.52                                                 
Validation - loss=7.5873e-01 ppl=2.14 best_loss=7.6790e-01 best_ppl=2.16                                                
Epoch 54 - |param|=6.65e+02 |g_param|=2.86e+04 loss=4.0088e-01 ppl=1.49                                                 
Validation - loss=7.5939e-01 ppl=2.14 best_loss=7.5873e-01 best_ppl=2.14                                                
Epoch 55 - |param|=6.66e+02 |g_param|=2.66e+04 loss=4.0457e-01 ppl=1.50                                                 
Validation - loss=7.6401e-01 ppl=2.15 best_loss=7.5873e-01 best_ppl=2.14                                                
Epoch 56 - |param|=6.66e+02 |g_param|=3.43e+04 loss=4.1825e-01 ppl=1.52                                                 
Validation - loss=7.5501e-01 ppl=2.13 best_loss=7.5873e-01 best_ppl=2.14                                                
Epoch 57 - |param|=6.66e+02 |g_param|=3.09e+04 loss=3.9626e-01 ppl=1.49                                                 
Validation - loss=7.5058e-01 ppl=2.12 best_loss=7.5501e-01 best_ppl=2.13                                                
Epoch 58 - |param|=6.67e+02 |g_param|=2.51e+04 loss=3.7168e-01 ppl=1.45                                                 
Validation - loss=7.6833e-01 ppl=2.16 best_loss=7.5058e-01 best_ppl=2.12                                                
Epoch 59 - |param|=6.67e+02 |g_param|=2.66e+04 loss=3.6880e-01 ppl=1.45                                                 
Validation - loss=7.7852e-01 ppl=2.18 best_loss=7.5058e-01 best_ppl=2.12                                                
Epoch 60 - |param|=6.67e+02 |g_param|=2.50e+04 loss=3.6898e-01 ppl=1.45                                                 
Validation - loss=7.5930e-01 ppl=2.14 best_loss=7.5058e-01 best_ppl=2.12                                                
Epoch 61 - |param|=6.68e+02 |g_param|=2.06e+04 loss=3.4397e-01 ppl=1.41                                                 
Validation - loss=7.5308e-01 ppl=2.12 best_loss=7.5058e-01 best_ppl=2.12                                                
Epoch 62 - |param|=6.68e+02 |g_param|=2.43e+04 loss=3.2901e-01 ppl=1.39                                                 
Validation - loss=7.4422e-01 ppl=2.10 best_loss=7.5058e-01 best_ppl=2.12                                                
Epoch 63 - |param|=6.68e+02 |g_param|=2.99e+04 loss=3.5045e-01 ppl=1.42                                                 
Validation - loss=7.6563e-01 ppl=2.15 best_loss=7.4422e-01 best_ppl=2.10                                                
Epoch 64 - |param|=6.68e+02 |g_param|=4.15e+04 loss=3.5544e-01 ppl=1.43                                                 
Validation - loss=7.5829e-01 ppl=2.13 best_loss=7.4422e-01 best_ppl=2.10                                                
Epoch 65 - |param|=6.69e+02 |g_param|=4.53e+04 loss=3.4371e-01 ppl=1.41                                                 
Validation - loss=7.4636e-01 ppl=2.11 best_loss=7.4422e-01 best_ppl=2.10                                                
Epoch 66 - |param|=6.69e+02 |g_param|=6.55e+04 loss=3.4400e-01 ppl=1.41                                                 
Validation - loss=7.4019e-01 ppl=2.10 best_loss=7.4422e-01 best_ppl=2.10                                                
Epoch 67 - |param|=6.69e+02 |g_param|=2.94e+04 loss=3.4390e-01 ppl=1.41                                                 
Validation - loss=7.3895e-01 ppl=2.09 best_loss=7.4019e-01 best_ppl=2.10                                                
Epoch 68 - |param|=6.70e+02 |g_param|=3.40e+04 loss=3.1527e-01 ppl=1.37                                                 
Validation - loss=7.4300e-01 ppl=2.10 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 69 - |param|=6.70e+02 |g_param|=3.86e+04 loss=3.6830e-01 ppl=1.45                                                 
Validation - loss=7.6304e-01 ppl=2.14 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 70 - |param|=6.70e+02 |g_param|=2.38e+04 loss=3.2472e-01 ppl=1.38                                                 
Validation - loss=7.5009e-01 ppl=2.12 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 71 - |param|=6.71e+02 |g_param|=2.28e+04 loss=3.1963e-01 ppl=1.38                                                 
Validation - loss=7.6681e-01 ppl=2.15 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 72 - |param|=6.71e+02 |g_param|=2.15e+04 loss=3.0333e-01 ppl=1.35                                                 
Validation - loss=7.7746e-01 ppl=2.18 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 73 - |param|=6.71e+02 |g_param|=2.04e+04 loss=2.8427e-01 ppl=1.33                                                 
Validation - loss=7.5346e-01 ppl=2.12 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 74 - |param|=6.72e+02 |g_param|=2.22e+04 loss=2.8530e-01 ppl=1.33                                                 
Validation - loss=7.4874e-01 ppl=2.11 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 75 - |param|=6.72e+02 |g_param|=2.35e+04 loss=2.9779e-01 ppl=1.35                                                 
Validation - loss=7.5978e-01 ppl=2.14 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 76 - |param|=6.72e+02 |g_param|=2.12e+04 loss=2.9432e-01 ppl=1.34                                                 
Validation - loss=7.4741e-01 ppl=2.11 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 77 - |param|=6.72e+02 |g_param|=2.41e+04 loss=2.9138e-01 ppl=1.34                                                 
Validation - loss=7.8071e-01 ppl=2.18 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 78 - |param|=6.73e+02 |g_param|=2.56e+04 loss=2.9666e-01 ppl=1.35                                                 
Validation - loss=7.4378e-01 ppl=2.10 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 79 - |param|=6.73e+02 |g_param|=2.09e+04 loss=2.7470e-01 ppl=1.32                                                 
Validation - loss=7.5043e-01 ppl=2.12 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 80 - |param|=6.73e+02 |g_param|=1.94e+04 loss=2.6910e-01 ppl=1.31                                                 
Validation - loss=7.4586e-01 ppl=2.11 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 81 - |param|=6.74e+02 |g_param|=2.19e+04 loss=2.7062e-01 ppl=1.31                                                 
Validation - loss=7.4637e-01 ppl=2.11 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 82 - |param|=6.74e+02 |g_param|=2.47e+04 loss=2.7937e-01 ppl=1.32                                                 
Validation - loss=7.5883e-01 ppl=2.14 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 83 - |param|=6.74e+02 |g_param|=2.46e+04 loss=2.7706e-01 ppl=1.32                                                 
Validation - loss=7.5562e-01 ppl=2.13 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 84 - |param|=6.75e+02 |g_param|=6.86e+04 loss=4.6719e-01 ppl=1.60                                                 
Validation - loss=7.8611e-01 ppl=2.19 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 85 - |param|=6.75e+02 |g_param|=2.83e+04 loss=3.0380e-01 ppl=1.36                                                 
Validation - loss=7.5765e-01 ppl=2.13 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 86 - |param|=6.75e+02 |g_param|=2.47e+04 loss=2.8172e-01 ppl=1.33                                                 
Validation - loss=7.5192e-01 ppl=2.12 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 87 - |param|=6.76e+02 |g_param|=2.07e+04 loss=2.6461e-01 ppl=1.30                                                 
Validation - loss=7.3069e-01 ppl=2.08 best_loss=7.3895e-01 best_ppl=2.09                                                
Epoch 88 - |param|=6.76e+02 |g_param|=4.12e+04 loss=2.4745e-01 ppl=1.28                                                 
Validation - loss=7.3853e-01 ppl=2.09 best_loss=7.3069e-01 best_ppl=2.08                                                
Epoch 89 - |param|=6.76e+02 |g_param|=3.81e+04 loss=2.5480e-01 ppl=1.29                                                 
Validation - loss=7.4580e-01 ppl=2.11 best_loss=7.3069e-01 best_ppl=2.08                                                
Epoch 90 - |param|=6.76e+02 |g_param|=3.93e+04 loss=2.5204e-01 ppl=1.29                                                 
Validation - loss=7.2915e-01 ppl=2.07 best_loss=7.3069e-01 best_ppl=2.08                                                
Epoch 91 - |param|=6.77e+02 |g_param|=3.89e+04 loss=2.2922e-01 ppl=1.26                                                 
Validation - loss=7.3881e-01 ppl=2.09 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 92 - |param|=6.77e+02 |g_param|=3.62e+04 loss=2.4061e-01 ppl=1.27                                                 
Validation - loss=7.3272e-01 ppl=2.08 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 93 - |param|=6.77e+02 |g_param|=3.70e+04 loss=2.4613e-01 ppl=1.28                                                 
Validation - loss=7.4131e-01 ppl=2.10 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 94 - |param|=6.78e+02 |g_param|=3.94e+04 loss=2.2344e-01 ppl=1.25                                                 
Validation - loss=7.5950e-01 ppl=2.14 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 95 - |param|=6.78e+02 |g_param|=3.66e+04 loss=2.4073e-01 ppl=1.27                                                 
Validation - loss=7.4657e-01 ppl=2.11 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 96 - |param|=6.78e+02 |g_param|=4.32e+04 loss=2.2323e-01 ppl=1.25                                                 
Validation - loss=7.6601e-01 ppl=2.15 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 97 - |param|=6.78e+02 |g_param|=4.29e+04 loss=2.2187e-01 ppl=1.25                                                 
Validation - loss=7.5489e-01 ppl=2.13 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 98 - |param|=6.79e+02 |g_param|=4.10e+04 loss=2.2128e-01 ppl=1.25                                                 
Validation - loss=7.4523e-01 ppl=2.11 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 99 - |param|=6.79e+02 |g_param|=4.57e+04 loss=2.2720e-01 ppl=1.26                                                 
Validation - loss=7.4526e-01 ppl=2.11 best_loss=7.2915e-01 best_ppl=2.07                                                
Epoch 100 - |param|=6.79e+02 |g_param|=3.82e+04 loss=2.2059e-01 ppl=1.25                                                
Validation - loss=7.4791e-01 ppl=2.11 best_loss=7.2915e-01 best_ppl=2.07                                                

real	15m52.429s
user	11m36.980s
sys	1m19.262s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-rkmy.39.0.58-1.78.0.82-2.28.pth
BLEU = 69.00, 85.1/74.0/63.9/56.3 (BP=1.000, ratio=1.030, hyp_len=24212, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.40.0.53-1.71.0.83-2.29.pth
BLEU = 71.04, 86.3/75.8/66.2/58.8 (BP=1.000, ratio=1.019, hyp_len=23964, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.41.0.55-1.74.0.88-2.41.pth
BLEU = 68.19, 84.5/73.5/63.2/55.1 (BP=1.000, ratio=1.042, hyp_len=24504, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.42.0.53-1.69.0.81-2.24.pth
BLEU = 69.68, 85.3/74.6/64.7/57.2 (BP=1.000, ratio=1.036, hyp_len=24355, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.43.0.56-1.76.0.83-2.30.pth
BLEU = 68.77, 84.9/74.0/63.7/55.9 (BP=1.000, ratio=1.039, hyp_len=24436, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.44.0.49-1.64.0.79-2.21.pth
BLEU = 71.26, 86.2/75.9/66.5/59.3 (BP=1.000, ratio=1.028, hyp_len=24162, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.45.0.51-1.67.0.80-2.23.pth
BLEU = 70.27, 85.5/75.1/65.4/58.0 (BP=1.000, ratio=1.036, hyp_len=24357, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.46.0.47-1.60.0.79-2.21.pth
BLEU = 72.04, 86.6/76.6/67.3/60.4 (BP=1.000, ratio=1.029, hyp_len=24195, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.47.0.48-1.61.0.81-2.24.pth
BLEU = 71.01, 86.0/75.7/66.3/58.9 (BP=1.000, ratio=1.030, hyp_len=24220, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.48.0.47-1.59.0.77-2.16.pth
BLEU = 72.60, 87.0/77.0/68.0/61.0 (BP=1.000, ratio=1.024, hyp_len=24080, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.49.0.55-1.74.0.81-2.25.pth
BLEU = 70.82, 85.8/75.5/66.1/58.7 (BP=1.000, ratio=1.028, hyp_len=24162, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.50.0.48-1.61.0.77-2.17.pth
BLEU = 71.91, 86.5/76.4/67.2/60.2 (BP=1.000, ratio=1.033, hyp_len=24291, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.51.0.45-1.57.0.79-2.21.pth
BLEU = 71.61, 86.1/76.1/66.9/60.0 (BP=1.000, ratio=1.040, hyp_len=24443, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.52.0.41-1.51.0.77-2.16.pth
BLEU = 72.71, 86.7/77.1/68.2/61.3 (BP=1.000, ratio=1.029, hyp_len=24201, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.53.0.42-1.52.0.76-2.14.pth
BLEU = 72.29, 86.5/76.7/67.7/60.9 (BP=1.000, ratio=1.033, hyp_len=24296, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.54.0.40-1.49.0.76-2.14.pth
BLEU = 72.80, 86.8/77.1/68.3/61.5 (BP=1.000, ratio=1.032, hyp_len=24263, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.55.0.40-1.50.0.76-2.15.pth
BLEU = 73.83, 87.4/78.0/69.4/62.8 (BP=1.000, ratio=1.029, hyp_len=24185, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.56.0.42-1.52.0.76-2.13.pth
BLEU = 72.00, 86.4/76.4/67.3/60.5 (BP=1.000, ratio=1.037, hyp_len=24387, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.57.0.40-1.49.0.75-2.12.pth
BLEU = 73.55, 87.2/77.7/69.1/62.5 (BP=1.000, ratio=1.027, hyp_len=24145, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.58.0.37-1.45.0.77-2.16.pth
BLEU = 72.40, 86.6/76.9/67.8/60.9 (BP=1.000, ratio=1.040, hyp_len=24458, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.59.0.37-1.45.0.78-2.18.pth
BLEU = 72.25, 86.5/76.6/67.6/60.8 (BP=1.000, ratio=1.036, hyp_len=24351, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.60.0.37-1.45.0.76-2.14.pth
BLEU = 74.07, 87.5/78.2/69.6/63.2 (BP=1.000, ratio=1.031, hyp_len=24246, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.61.0.34-1.41.0.75-2.12.pth
BLEU = 74.08, 87.4/78.2/69.7/63.2 (BP=1.000, ratio=1.034, hyp_len=24319, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.62.0.33-1.39.0.74-2.10.pth
BLEU = 73.88, 87.4/78.0/69.5/62.9 (BP=1.000, ratio=1.028, hyp_len=24175, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.63.0.35-1.42.0.77-2.15.pth
BLEU = 72.90, 87.0/77.3/68.3/61.5 (BP=1.000, ratio=1.035, hyp_len=24324, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.64.0.36-1.43.0.76-2.13.pth
BLEU = 73.76, 87.2/77.9/69.4/62.8 (BP=1.000, ratio=1.034, hyp_len=24309, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.65.0.34-1.41.0.75-2.11.pth
BLEU = 73.62, 87.1/77.8/69.2/62.6 (BP=1.000, ratio=1.035, hyp_len=24339, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.66.0.34-1.41.0.74-2.10.pth
BLEU = 73.77, 87.2/77.9/69.4/62.9 (BP=1.000, ratio=1.035, hyp_len=24321, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.67.0.34-1.41.0.74-2.09.pth
BLEU = 73.08, 86.8/77.2/68.6/62.1 (BP=1.000, ratio=1.041, hyp_len=24482, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.68.0.32-1.37.0.74-2.10.pth
BLEU = 73.88, 87.4/77.9/69.5/62.9 (BP=1.000, ratio=1.032, hyp_len=24258, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.69.0.37-1.45.0.76-2.14.pth
BLEU = 71.99, 86.1/76.4/67.5/60.5 (BP=1.000, ratio=1.039, hyp_len=24435, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.70.0.32-1.38.0.75-2.12.pth
BLEU = 73.88, 87.2/78.0/69.5/63.0 (BP=1.000, ratio=1.035, hyp_len=24342, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.71.0.32-1.38.0.77-2.15.pth
BLEU = 73.73, 87.2/77.9/69.3/62.8 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.72.0.30-1.35.0.78-2.18.pth
BLEU = 74.22, 87.5/78.3/69.9/63.4 (BP=1.000, ratio=1.033, hyp_len=24288, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.73.0.28-1.33.0.75-2.12.pth
BLEU = 74.48, 87.6/78.5/70.2/63.7 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.74.0.29-1.33.0.75-2.11.pth
BLEU = 74.98, 88.0/79.0/70.7/64.3 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.75.0.30-1.35.0.76-2.14.pth
BLEU = 74.05, 87.4/78.1/69.7/63.2 (BP=1.000, ratio=1.037, hyp_len=24385, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.76.0.29-1.34.0.75-2.11.pth
BLEU = 73.60, 87.2/77.8/69.1/62.6 (BP=1.000, ratio=1.039, hyp_len=24434, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.77.0.29-1.34.0.78-2.18.pth
BLEU = 73.00, 86.8/77.3/68.5/61.7 (BP=1.000, ratio=1.043, hyp_len=24509, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.78.0.30-1.35.0.74-2.10.pth
BLEU = 73.10, 86.7/77.2/68.6/62.1 (BP=1.000, ratio=1.044, hyp_len=24547, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.79.0.27-1.32.0.75-2.12.pth
BLEU = 73.82, 87.2/77.9/69.4/63.0 (BP=1.000, ratio=1.040, hyp_len=24444, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.80.0.27-1.31.0.75-2.11.pth
BLEU = 74.23, 87.4/78.3/69.9/63.4 (BP=1.000, ratio=1.040, hyp_len=24446, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.81.0.27-1.31.0.75-2.11.pth
BLEU = 73.92, 87.3/78.0/69.6/63.0 (BP=1.000, ratio=1.038, hyp_len=24400, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.82.0.28-1.32.0.76-2.14.pth
BLEU = 72.67, 86.6/76.9/68.1/61.4 (BP=1.000, ratio=1.045, hyp_len=24578, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.83.0.28-1.32.0.76-2.13.pth
BLEU = 73.49, 87.1/77.7/69.0/62.4 (BP=1.000, ratio=1.040, hyp_len=24445, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.84.0.47-1.60.0.79-2.19.pth
BLEU = 72.34, 86.4/76.6/67.8/61.0 (BP=1.000, ratio=1.039, hyp_len=24425, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.85.0.30-1.36.0.76-2.13.pth
BLEU = 73.63, 87.2/77.8/69.2/62.6 (BP=1.000, ratio=1.039, hyp_len=24419, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.86.0.28-1.33.0.75-2.12.pth
BLEU = 73.02, 86.8/77.2/68.5/61.9 (BP=1.000, ratio=1.044, hyp_len=24535, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.87.0.26-1.30.0.73-2.08.pth
BLEU = 72.56, 86.4/76.8/68.0/61.4 (BP=1.000, ratio=1.048, hyp_len=24639, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.88.0.25-1.28.0.74-2.09.pth
BLEU = 74.67, 87.7/78.6/70.4/64.0 (BP=1.000, ratio=1.036, hyp_len=24345, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.89.0.25-1.29.0.75-2.11.pth
BLEU = 72.94, 86.8/77.1/68.4/61.8 (BP=1.000, ratio=1.045, hyp_len=24575, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.90.0.25-1.29.0.73-2.07.pth
BLEU = 73.82, 87.3/77.9/69.4/62.9 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.91.0.23-1.26.0.74-2.09.pth
BLEU = 74.73, 87.8/78.7/70.4/64.0 (BP=1.000, ratio=1.034, hyp_len=24305, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.92.0.24-1.27.0.73-2.08.pth
BLEU = 73.45, 87.0/77.6/69.0/62.5 (BP=1.000, ratio=1.040, hyp_len=24444, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.93.0.25-1.28.0.74-2.10.pth
BLEU = 73.21, 86.9/77.4/68.7/62.1 (BP=1.000, ratio=1.042, hyp_len=24487, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.94.0.22-1.25.0.76-2.14.pth
BLEU = 73.81, 87.2/77.8/69.4/63.0 (BP=1.000, ratio=1.043, hyp_len=24512, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.95.0.24-1.27.0.75-2.11.pth
BLEU = 71.88, 85.7/76.0/67.3/60.9 (BP=1.000, ratio=1.059, hyp_len=24891, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.96.0.22-1.25.0.77-2.15.pth
BLEU = 74.58, 87.6/78.6/70.3/63.9 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.97.0.22-1.25.0.75-2.13.pth
BLEU = 73.29, 86.9/77.4/68.8/62.3 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.98.0.22-1.25.0.75-2.11.pth
BLEU = 74.28, 87.3/78.2/70.0/63.6 (BP=1.000, ratio=1.040, hyp_len=24459, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.99.0.23-1.26.0.75-2.11.pth
BLEU = 74.21, 87.5/78.2/69.9/63.4 (BP=1.000, ratio=1.036, hyp_len=24345, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.100.0.22-1.25.0.75-2.11.pth
BLEU = 73.44, 87.0/77.5/69.0/62.6 (BP=1.000, ratio=1.044, hyp_len=24555, ref_len=23509)

real	21m15.502s
user	20m1.967s
sys	1m18.073s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-40epoch$
```

Baseline: seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth, BLEU = 69.39  
RL, rk-my, 40-60 model Best Score:  

```
Evaluation result for the model: seq-rl-model-rkmy.74.0.29-1.33.0.75-2.11.pth
BLEU = 74.98, 88.0/79.0/70.7/64.3 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
```

### RL, rk-my, 50-50 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth --model_fn ./model/rl/seq2seq/rkmy-50epoch/seq-rl-model-rkmy.pth --init_epoch 49 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/rkmy-50epoch/seq-rl-model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 49
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 49,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'load_fn': './model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/rkmy-50epoch/seq-rl-model-rkmy.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 49 - |param|=6.65e+02 |g_param|=2.75e+05 loss=3.3212e-01 ppl=1.39                                                 
Validation - loss=6.3525e-01 ppl=1.89 best_loss=inf best_ppl=inf                                                        
Epoch 50 - |param|=6.65e+02 |g_param|=1.89e+05 loss=3.2162e-01 ppl=1.38                                                 
Validation - loss=6.3031e-01 ppl=1.88 best_loss=6.3525e-01 best_ppl=1.89                                                
Epoch 51 - |param|=6.66e+02 |g_param|=8.71e+04 loss=2.9801e-01 ppl=1.35                                                 
Validation - loss=6.2755e-01 ppl=1.87 best_loss=6.3031e-01 best_ppl=1.88                                                
Epoch 52 - |param|=6.66e+02 |g_param|=8.46e+04 loss=3.2240e-01 ppl=1.38                                                 
Validation - loss=6.2880e-01 ppl=1.88 best_loss=6.2755e-01 best_ppl=1.87                                                
Epoch 53 - |param|=6.66e+02 |g_param|=6.91e+04 loss=2.9150e-01 ppl=1.34                                                 
Validation - loss=6.2194e-01 ppl=1.86 best_loss=6.2755e-01 best_ppl=1.87                                                
Epoch 54 - |param|=6.66e+02 |g_param|=4.07e+04 loss=2.9989e-01 ppl=1.35                                                 
Validation - loss=6.3927e-01 ppl=1.90 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 55 - |param|=6.67e+02 |g_param|=4.87e+04 loss=3.0294e-01 ppl=1.35                                                 
Validation - loss=6.3879e-01 ppl=1.89 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 56 - |param|=6.67e+02 |g_param|=4.38e+04 loss=2.9690e-01 ppl=1.35                                                 
Validation - loss=6.3204e-01 ppl=1.88 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 57 - |param|=6.67e+02 |g_param|=8.10e+04 loss=3.3338e-01 ppl=1.40                                                 
Validation - loss=7.3547e-01 ppl=2.09 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 58 - |param|=6.68e+02 |g_param|=4.78e+04 loss=3.1006e-01 ppl=1.36                                                 
Validation - loss=6.3427e-01 ppl=1.89 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 59 - |param|=6.68e+02 |g_param|=3.93e+04 loss=2.8318e-01 ppl=1.33                                                 
Validation - loss=6.2527e-01 ppl=1.87 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 60 - |param|=6.68e+02 |g_param|=4.83e+04 loss=2.8229e-01 ppl=1.33                                                 
Validation - loss=6.1779e-01 ppl=1.85 best_loss=6.2194e-01 best_ppl=1.86                                                
Epoch 61 - |param|=6.69e+02 |g_param|=4.33e+04 loss=2.8229e-01 ppl=1.33                                                 
Validation - loss=6.1810e-01 ppl=1.86 best_loss=6.1779e-01 best_ppl=1.85                                                
Epoch 62 - |param|=6.69e+02 |g_param|=4.76e+04 loss=2.7936e-01 ppl=1.32                                                 
Validation - loss=6.1915e-01 ppl=1.86 best_loss=6.1779e-01 best_ppl=1.85                                                
Epoch 63 - |param|=6.69e+02 |g_param|=4.52e+04 loss=2.6843e-01 ppl=1.31                                                 
Validation - loss=6.1808e-01 ppl=1.86 best_loss=6.1779e-01 best_ppl=1.85                                                
Epoch 64 - |param|=6.70e+02 |g_param|=3.85e+04 loss=2.6224e-01 ppl=1.30                                                 
Validation - loss=6.1128e-01 ppl=1.84 best_loss=6.1779e-01 best_ppl=1.85                                                
Epoch 65 - |param|=6.70e+02 |g_param|=3.54e+04 loss=2.4600e-01 ppl=1.28                                                 
Validation - loss=6.1315e-01 ppl=1.85 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 66 - |param|=6.70e+02 |g_param|=3.56e+04 loss=2.3911e-01 ppl=1.27                                                 
Validation - loss=6.2086e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 67 - |param|=6.71e+02 |g_param|=3.63e+04 loss=2.4440e-01 ppl=1.28                                                 
Validation - loss=6.2914e-01 ppl=1.88 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 68 - |param|=6.71e+02 |g_param|=4.87e+04 loss=2.4382e-01 ppl=1.28                                                 
Validation - loss=6.2464e-01 ppl=1.87 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 69 - |param|=6.71e+02 |g_param|=3.75e+04 loss=2.2980e-01 ppl=1.26                                                 
Validation - loss=6.2028e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 70 - |param|=6.72e+02 |g_param|=3.98e+04 loss=2.3392e-01 ppl=1.26                                                 
Validation - loss=6.2248e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 71 - |param|=6.72e+02 |g_param|=4.63e+04 loss=2.3239e-01 ppl=1.26                                                 
Validation - loss=6.2980e-01 ppl=1.88 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 72 - |param|=6.72e+02 |g_param|=4.00e+04 loss=2.2743e-01 ppl=1.26                                                 
Validation - loss=6.2302e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 73 - |param|=6.72e+02 |g_param|=3.96e+04 loss=2.1725e-01 ppl=1.24                                                 
Validation - loss=6.3055e-01 ppl=1.88 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 74 - |param|=6.73e+02 |g_param|=8.98e+04 loss=2.2778e-01 ppl=1.26                                                 
Validation - loss=6.2234e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 75 - |param|=6.73e+02 |g_param|=8.43e+04 loss=2.1721e-01 ppl=1.24                                                 
Validation - loss=6.1731e-01 ppl=1.85 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 76 - |param|=6.73e+02 |g_param|=7.53e+04 loss=2.1525e-01 ppl=1.24                                                 
Validation - loss=6.1637e-01 ppl=1.85 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 77 - |param|=6.74e+02 |g_param|=2.51e+04 loss=2.0153e-01 ppl=1.22                                                 
Validation - loss=6.2297e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 78 - |param|=6.74e+02 |g_param|=2.06e+04 loss=2.0531e-01 ppl=1.23                                                 
Validation - loss=6.2075e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 79 - |param|=6.74e+02 |g_param|=2.64e+04 loss=2.2278e-01 ppl=1.25                                                 
Validation - loss=6.3802e-01 ppl=1.89 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 80 - |param|=6.75e+02 |g_param|=2.26e+04 loss=2.1155e-01 ppl=1.24                                                 
Validation - loss=6.2844e-01 ppl=1.87 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 81 - |param|=6.75e+02 |g_param|=3.12e+04 loss=2.3417e-01 ppl=1.26                                                 
Validation - loss=6.8455e-01 ppl=1.98 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 82 - |param|=6.75e+02 |g_param|=3.14e+04 loss=2.3801e-01 ppl=1.27                                                 
Validation - loss=6.8597e-01 ppl=1.99 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 83 - |param|=6.76e+02 |g_param|=3.02e+04 loss=2.3086e-01 ppl=1.26                                                 
Validation - loss=6.3515e-01 ppl=1.89 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 84 - |param|=6.76e+02 |g_param|=1.56e+04 loss=2.2983e-01 ppl=1.26                                                 
Validation - loss=6.2378e-01 ppl=1.87 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 85 - |param|=6.76e+02 |g_param|=1.19e+04 loss=2.1069e-01 ppl=1.23                                                 
Validation - loss=6.2957e-01 ppl=1.88 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 86 - |param|=6.77e+02 |g_param|=9.43e+03 loss=1.9204e-01 ppl=1.21                                                 
Validation - loss=6.2245e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 87 - |param|=6.77e+02 |g_param|=9.57e+03 loss=1.8199e-01 ppl=1.20                                                 
Validation - loss=6.2121e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 88 - |param|=6.77e+02 |g_param|=8.46e+03 loss=1.8306e-01 ppl=1.20                                                 
Validation - loss=6.2075e-01 ppl=1.86 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 89 - |param|=6.77e+02 |g_param|=8.37e+03 loss=1.7864e-01 ppl=1.20                                                 
Validation - loss=6.4382e-01 ppl=1.90 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 90 - |param|=6.78e+02 |g_param|=9.26e+03 loss=1.7247e-01 ppl=1.19                                                 
Validation - loss=6.3754e-01 ppl=1.89 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 91 - |param|=6.78e+02 |g_param|=9.92e+03 loss=1.7571e-01 ppl=1.19                                                 
Validation - loss=6.3543e-01 ppl=1.89 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 92 - |param|=6.78e+02 |g_param|=1.28e+04 loss=1.8509e-01 ppl=1.20                                                 
Validation - loss=6.5017e-01 ppl=1.92 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 93 - |param|=6.79e+02 |g_param|=1.13e+04 loss=1.7968e-01 ppl=1.20                                                 
Validation - loss=6.4223e-01 ppl=1.90 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 94 - |param|=6.79e+02 |g_param|=9.71e+03 loss=1.7761e-01 ppl=1.19                                                 
Validation - loss=6.4703e-01 ppl=1.91 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 95 - |param|=6.79e+02 |g_param|=8.92e+03 loss=1.6626e-01 ppl=1.18                                                 
Validation - loss=6.4424e-01 ppl=1.90 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 96 - |param|=6.80e+02 |g_param|=8.31e+03 loss=1.6091e-01 ppl=1.17                                                 
Validation - loss=6.4650e-01 ppl=1.91 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 97 - |param|=6.80e+02 |g_param|=7.75e+03 loss=1.5726e-01 ppl=1.17                                                 
Validation - loss=6.4684e-01 ppl=1.91 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 98 - |param|=6.80e+02 |g_param|=9.55e+03 loss=1.4843e-01 ppl=1.16                                                 
Validation - loss=6.5279e-01 ppl=1.92 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 99 - |param|=6.80e+02 |g_param|=8.19e+03 loss=1.5623e-01 ppl=1.17                                                 
Validation - loss=6.6518e-01 ppl=1.94 best_loss=6.1128e-01 best_ppl=1.84                                                
Epoch 100 - |param|=6.81e+02 |g_param|=9.60e+03 loss=1.5517e-01 ppl=1.17                                                
Validation - loss=6.6024e-01 ppl=1.94 best_loss=6.1128e-01 best_ppl=1.84                                                

real	9m52.672s
user	9m42.823s
sys	0m8.687s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-rkmy.100.0.16-1.17.0.66-1.94.pth
BLEU = 73.39, 86.7/77.5/69.1/62.5 (BP=1.000, ratio=1.049, hyp_len=24663, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.49.0.33-1.39.0.64-1.89.pth
BLEU = 74.46, 87.4/78.4/70.3/63.9 (BP=1.000, ratio=1.036, hyp_len=24357, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.50.0.32-1.38.0.63-1.88.pth
BLEU = 74.39, 87.4/78.4/70.2/63.7 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.51.0.30-1.35.0.63-1.87.pth
BLEU = 74.76, 87.8/78.7/70.5/64.1 (BP=1.000, ratio=1.032, hyp_len=24261, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.52.0.32-1.38.0.63-1.88.pth
BLEU = 74.02, 87.2/78.1/69.7/63.2 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.53.0.29-1.34.0.62-1.86.pth
BLEU = 74.46, 87.6/78.5/70.2/63.7 (BP=1.000, ratio=1.036, hyp_len=24353, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.54.0.30-1.35.0.64-1.90.pth
BLEU = 72.50, 86.4/76.8/68.0/61.2 (BP=1.000, ratio=1.047, hyp_len=24603, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.55.0.30-1.35.0.64-1.89.pth
BLEU = 72.89, 86.5/77.2/68.5/61.8 (BP=1.000, ratio=1.045, hyp_len=24564, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.56.0.30-1.35.0.63-1.88.pth
BLEU = 73.69, 87.0/77.7/69.3/62.9 (BP=1.000, ratio=1.042, hyp_len=24502, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.57.0.33-1.40.0.74-2.09.pth
BLEU = 71.54, 85.9/76.2/66.9/59.8 (BP=1.000, ratio=1.055, hyp_len=24805, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.58.0.31-1.36.0.63-1.89.pth
BLEU = 73.47, 86.8/77.5/69.1/62.6 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.59.0.28-1.33.0.63-1.87.pth
BLEU = 73.61, 86.9/77.6/69.3/62.9 (BP=1.000, ratio=1.042, hyp_len=24493, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.60.0.28-1.33.0.62-1.85.pth
BLEU = 73.63, 86.9/77.7/69.3/62.8 (BP=1.000, ratio=1.041, hyp_len=24483, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.61.0.28-1.33.0.62-1.86.pth
BLEU = 72.34, 86.2/76.6/67.9/61.1 (BP=1.000, ratio=1.051, hyp_len=24698, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.62.0.28-1.32.0.62-1.86.pth
BLEU = 73.27, 86.8/77.5/68.9/62.2 (BP=1.000, ratio=1.043, hyp_len=24517, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.63.0.27-1.31.0.62-1.86.pth
BLEU = 73.01, 86.6/77.2/68.6/61.9 (BP=1.000, ratio=1.045, hyp_len=24557, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.64.0.26-1.30.0.61-1.84.pth
BLEU = 74.20, 87.3/78.2/69.9/63.5 (BP=1.000, ratio=1.040, hyp_len=24453, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.65.0.25-1.28.0.61-1.85.pth
BLEU = 74.42, 87.5/78.4/70.1/63.7 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.66.0.24-1.27.0.62-1.86.pth
BLEU = 74.45, 87.4/78.5/70.3/63.7 (BP=1.000, ratio=1.039, hyp_len=24420, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.67.0.24-1.28.0.63-1.88.pth
BLEU = 73.88, 87.1/77.9/69.6/63.1 (BP=1.000, ratio=1.045, hyp_len=24566, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.68.0.24-1.28.0.62-1.87.pth
BLEU = 73.48, 87.1/77.7/69.0/62.3 (BP=1.000, ratio=1.043, hyp_len=24515, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.69.0.23-1.26.0.62-1.86.pth
BLEU = 74.04, 87.4/78.1/69.7/63.1 (BP=1.000, ratio=1.038, hyp_len=24396, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.70.0.23-1.26.0.62-1.86.pth
BLEU = 73.20, 86.7/77.3/68.9/62.2 (BP=1.000, ratio=1.046, hyp_len=24596, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.71.0.23-1.26.0.63-1.88.pth
BLEU = 73.84, 87.2/77.9/69.5/62.9 (BP=1.000, ratio=1.041, hyp_len=24464, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.72.0.23-1.26.0.62-1.86.pth
BLEU = 73.92, 87.2/77.9/69.6/63.2 (BP=1.000, ratio=1.044, hyp_len=24555, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.73.0.22-1.24.0.63-1.88.pth
BLEU = 74.08, 87.2/78.1/69.8/63.3 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.74.0.23-1.26.0.62-1.86.pth
BLEU = 73.57, 86.9/77.7/69.2/62.7 (BP=1.000, ratio=1.044, hyp_len=24543, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.75.0.22-1.24.0.62-1.85.pth
BLEU = 73.80, 87.0/77.9/69.5/63.0 (BP=1.000, ratio=1.045, hyp_len=24561, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.76.0.22-1.24.0.62-1.85.pth
BLEU = 74.03, 87.2/78.1/69.8/63.3 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.77.0.20-1.22.0.62-1.86.pth
BLEU = 74.36, 87.5/78.4/70.1/63.6 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.78.0.21-1.23.0.62-1.86.pth
BLEU = 73.76, 87.0/77.9/69.5/62.9 (BP=1.000, ratio=1.047, hyp_len=24614, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.79.0.22-1.25.0.64-1.89.pth
BLEU = 73.64, 87.0/77.8/69.3/62.7 (BP=1.000, ratio=1.041, hyp_len=24462, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.80.0.21-1.24.0.63-1.87.pth
BLEU = 73.97, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.81.0.23-1.26.0.68-1.98.pth
BLEU = 73.68, 87.1/77.8/69.4/62.7 (BP=1.000, ratio=1.031, hyp_len=24245, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.82.0.24-1.27.0.69-1.99.pth
BLEU = 70.74, 85.0/75.1/66.2/59.3 (BP=1.000, ratio=1.048, hyp_len=24632, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.83.0.23-1.26.0.64-1.89.pth
BLEU = 73.22, 86.8/77.5/68.9/62.0 (BP=1.000, ratio=1.039, hyp_len=24418, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.84.0.23-1.26.0.62-1.87.pth
BLEU = 73.64, 87.0/77.7/69.3/62.8 (BP=1.000, ratio=1.044, hyp_len=24544, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.85.0.21-1.23.0.63-1.88.pth
BLEU = 73.98, 87.3/78.2/69.7/63.0 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.86.0.19-1.21.0.62-1.86.pth
BLEU = 73.94, 87.2/78.0/69.6/63.1 (BP=1.000, ratio=1.042, hyp_len=24491, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.87.0.18-1.20.0.62-1.86.pth
BLEU = 74.02, 87.3/78.1/69.7/63.2 (BP=1.000, ratio=1.044, hyp_len=24535, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.88.0.18-1.20.0.62-1.86.pth
BLEU = 74.02, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.89.0.18-1.20.0.64-1.90.pth
BLEU = 73.82, 87.0/77.8/69.5/63.0 (BP=1.000, ratio=1.043, hyp_len=24516, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.90.0.17-1.19.0.64-1.89.pth
BLEU = 72.78, 86.4/77.0/68.4/61.6 (BP=1.000, ratio=1.051, hyp_len=24699, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.91.0.18-1.19.0.64-1.89.pth
BLEU = 72.78, 86.6/77.1/68.3/61.6 (BP=1.000, ratio=1.050, hyp_len=24680, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.92.0.19-1.20.0.65-1.92.pth
BLEU = 74.23, 87.2/78.3/70.0/63.6 (BP=1.000, ratio=1.043, hyp_len=24514, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.93.0.18-1.20.0.64-1.90.pth
BLEU = 73.09, 86.6/77.3/68.7/62.0 (BP=1.000, ratio=1.047, hyp_len=24611, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.94.0.18-1.19.0.65-1.91.pth
BLEU = 73.51, 86.9/77.5/69.1/62.6 (BP=1.000, ratio=1.046, hyp_len=24584, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.95.0.17-1.18.0.64-1.90.pth
BLEU = 74.16, 87.3/78.2/69.9/63.4 (BP=1.000, ratio=1.044, hyp_len=24539, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.96.0.16-1.17.0.65-1.91.pth
BLEU = 74.10, 87.1/78.1/69.8/63.5 (BP=1.000, ratio=1.046, hyp_len=24589, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.97.0.16-1.17.0.65-1.91.pth
BLEU = 73.71, 87.0/77.8/69.4/62.8 (BP=1.000, ratio=1.048, hyp_len=24631, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.98.0.15-1.16.0.65-1.92.pth
BLEU = 74.91, 87.7/78.8/70.8/64.4 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.99.0.16-1.17.0.67-1.94.pth
BLEU = 73.79, 86.9/77.8/69.5/63.1 (BP=1.000, ratio=1.049, hyp_len=24650, ref_len=23509)

real	19m2.785s
user	17m7.820s
sys	1m14.183s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-50epoch$
```

Baseline, seq2seq, rk-my, 50 epoch:  seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth, BLEU = 74.04
RL, rk-my, 50-50 model Best score:  

```
Evaluation result for the model: seq-rl-model-rkmy.98.0.15-1.16.0.65-1.92.pth
BLEU = 74.91, 87.7/78.8/70.8/64.4 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
```

### RL, rk-my, 60-40 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth --model_fn ./model/rl/seq2seq/rkmy-60epoch/seq-rl-model-rkmy.pth --init_epoch 58 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/rkmy-60epoch/seq-rl-model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 58
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 58,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'load_fn': './model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/rkmy-60epoch/seq-rl-model-rkmy.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 58 - |param|=6.66e+02 |g_param|=8.37e+04 loss=4.0373e-01 ppl=1.50                                                 
Validation - loss=8.1957e-01 ppl=2.27 best_loss=inf best_ppl=inf                                                        
Epoch 59 - |param|=6.66e+02 |g_param|=5.85e+04 loss=3.8686e-01 ppl=1.47                                                 
Validation - loss=8.0894e-01 ppl=2.25 best_loss=8.1957e-01 best_ppl=2.27                                                
Epoch 60 - |param|=6.67e+02 |g_param|=5.56e+04 loss=4.5205e-01 ppl=1.57                                                 
Validation - loss=7.7353e-01 ppl=2.17 best_loss=8.0894e-01 best_ppl=2.25                                                
Epoch 61 - |param|=6.67e+02 |g_param|=3.20e+04 loss=4.0651e-01 ppl=1.50                                                 
Validation - loss=7.9537e-01 ppl=2.22 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 62 - |param|=6.68e+02 |g_param|=2.82e+04 loss=3.8224e-01 ppl=1.47                                                 
Validation - loss=8.0755e-01 ppl=2.24 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 63 - |param|=6.68e+02 |g_param|=4.50e+04 loss=4.0792e-01 ppl=1.50                                                 
Validation - loss=7.9285e-01 ppl=2.21 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 64 - |param|=6.68e+02 |g_param|=2.79e+04 loss=3.8890e-01 ppl=1.48                                                 
Validation - loss=7.7452e-01 ppl=2.17 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 65 - |param|=6.69e+02 |g_param|=2.89e+04 loss=3.6196e-01 ppl=1.44                                                 
Validation - loss=7.8334e-01 ppl=2.19 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 66 - |param|=6.69e+02 |g_param|=2.37e+04 loss=3.4403e-01 ppl=1.41                                                 
Validation - loss=7.8089e-01 ppl=2.18 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 67 - |param|=6.69e+02 |g_param|=2.44e+04 loss=3.3490e-01 ppl=1.40                                                 
Validation - loss=7.7918e-01 ppl=2.18 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 68 - |param|=6.69e+02 |g_param|=2.58e+04 loss=3.3485e-01 ppl=1.40                                                 
Validation - loss=7.8163e-01 ppl=2.19 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 69 - |param|=6.70e+02 |g_param|=2.60e+04 loss=3.3022e-01 ppl=1.39                                                 
Validation - loss=7.8056e-01 ppl=2.18 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 70 - |param|=6.70e+02 |g_param|=3.65e+04 loss=3.5898e-01 ppl=1.43                                                 
Validation - loss=7.9552e-01 ppl=2.22 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 71 - |param|=6.70e+02 |g_param|=2.88e+04 loss=3.4395e-01 ppl=1.41                                                 
Validation - loss=7.7155e-01 ppl=2.16 best_loss=7.7353e-01 best_ppl=2.17                                                
Epoch 72 - |param|=6.71e+02 |g_param|=4.75e+04 loss=3.4950e-01 ppl=1.42                                                 
Validation - loss=8.6624e-01 ppl=2.38 best_loss=7.7155e-01 best_ppl=2.16                                                
Epoch 73 - |param|=6.71e+02 |g_param|=3.21e+04 loss=3.3327e-01 ppl=1.40                                                 
Validation - loss=7.9953e-01 ppl=2.22 best_loss=7.7155e-01 best_ppl=2.16                                                
Epoch 74 - |param|=6.71e+02 |g_param|=2.46e+04 loss=3.1990e-01 ppl=1.38                                                 
Validation - loss=7.6203e-01 ppl=2.14 best_loss=7.7155e-01 best_ppl=2.16                                                
Epoch 75 - |param|=6.72e+02 |g_param|=2.77e+04 loss=3.1859e-01 ppl=1.38                                                 
Validation - loss=7.4763e-01 ppl=2.11 best_loss=7.6203e-01 best_ppl=2.14                                                
Epoch 76 - |param|=6.72e+02 |g_param|=2.36e+04 loss=2.9951e-01 ppl=1.35                                                 
Validation - loss=7.6705e-01 ppl=2.15 best_loss=7.4763e-01 best_ppl=2.11                                                
Epoch 77 - |param|=6.72e+02 |g_param|=3.59e+04 loss=3.3124e-01 ppl=1.39                                                 
Validation - loss=7.7220e-01 ppl=2.16 best_loss=7.4763e-01 best_ppl=2.11                                                
Epoch 78 - |param|=6.73e+02 |g_param|=5.68e+04 loss=3.9272e-01 ppl=1.48                                                 
Validation - loss=7.8372e-01 ppl=2.19 best_loss=7.4763e-01 best_ppl=2.11                                                
Epoch 79 - |param|=6.73e+02 |g_param|=3.65e+04 loss=3.4151e-01 ppl=1.41                                                 
Validation - loss=7.4207e-01 ppl=2.10 best_loss=7.4763e-01 best_ppl=2.11                                                
Epoch 80 - |param|=6.73e+02 |g_param|=3.20e+04 loss=3.0518e-01 ppl=1.36                                                 
Validation - loss=7.6741e-01 ppl=2.15 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 81 - |param|=6.74e+02 |g_param|=3.44e+04 loss=2.9357e-01 ppl=1.34                                                 
Validation - loss=7.5316e-01 ppl=2.12 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 82 - |param|=6.74e+02 |g_param|=2.75e+04 loss=2.7795e-01 ppl=1.32                                                 
Validation - loss=7.5465e-01 ppl=2.13 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 83 - |param|=6.74e+02 |g_param|=2.54e+04 loss=2.8549e-01 ppl=1.33                                                 
Validation - loss=7.6120e-01 ppl=2.14 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 84 - |param|=6.74e+02 |g_param|=2.43e+04 loss=2.8397e-01 ppl=1.33                                                 
Validation - loss=7.6052e-01 ppl=2.14 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 85 - |param|=6.75e+02 |g_param|=2.56e+04 loss=2.8182e-01 ppl=1.33                                                 
Validation - loss=7.4087e-01 ppl=2.10 best_loss=7.4207e-01 best_ppl=2.10                                                
Epoch 86 - |param|=6.75e+02 |g_param|=2.32e+04 loss=2.6865e-01 ppl=1.31                                                 
Validation - loss=7.3522e-01 ppl=2.09 best_loss=7.4087e-01 best_ppl=2.10                                                
Epoch 87 - |param|=6.75e+02 |g_param|=3.16e+04 loss=2.8197e-01 ppl=1.33                                                 
Validation - loss=7.5536e-01 ppl=2.13 best_loss=7.3522e-01 best_ppl=2.09                                                
Epoch 88 - |param|=6.76e+02 |g_param|=2.21e+04 loss=2.6133e-01 ppl=1.30                                                 
Validation - loss=7.4421e-01 ppl=2.10 best_loss=7.3522e-01 best_ppl=2.09                                                
Epoch 89 - |param|=6.76e+02 |g_param|=3.43e+04 loss=2.8284e-01 ppl=1.33                                                 
Validation - loss=7.3421e-01 ppl=2.08 best_loss=7.3522e-01 best_ppl=2.09                                                
Epoch 90 - |param|=6.76e+02 |g_param|=2.10e+04 loss=2.4492e-01 ppl=1.28                                                 
Validation - loss=7.6583e-01 ppl=2.15 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 91 - |param|=6.77e+02 |g_param|=2.36e+04 loss=2.4711e-01 ppl=1.28                                                 
Validation - loss=7.6279e-01 ppl=2.14 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 92 - |param|=6.77e+02 |g_param|=2.25e+04 loss=2.5904e-01 ppl=1.30                                                 
Validation - loss=7.6147e-01 ppl=2.14 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 93 - |param|=6.77e+02 |g_param|=2.16e+04 loss=2.4339e-01 ppl=1.28                                                 
Validation - loss=7.4773e-01 ppl=2.11 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 94 - |param|=6.77e+02 |g_param|=2.21e+04 loss=2.4949e-01 ppl=1.28                                                 
Validation - loss=7.7196e-01 ppl=2.16 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 95 - |param|=6.78e+02 |g_param|=2.24e+04 loss=2.3702e-01 ppl=1.27                                                 
Validation - loss=7.7811e-01 ppl=2.18 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 96 - |param|=6.78e+02 |g_param|=2.17e+04 loss=2.3728e-01 ppl=1.27                                                 
Validation - loss=7.7851e-01 ppl=2.18 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 97 - |param|=6.78e+02 |g_param|=2.18e+04 loss=2.3507e-01 ppl=1.26                                                 
Validation - loss=7.4561e-01 ppl=2.11 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 98 - |param|=6.79e+02 |g_param|=2.29e+04 loss=2.3724e-01 ppl=1.27                                                 
Validation - loss=7.6005e-01 ppl=2.14 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 99 - |param|=6.79e+02 |g_param|=2.30e+04 loss=2.3649e-01 ppl=1.27                                                 
Validation - loss=7.8436e-01 ppl=2.19 best_loss=7.3421e-01 best_ppl=2.08                                                
Epoch 100 - |param|=6.79e+02 |g_param|=2.22e+04 loss=2.1623e-01 ppl=1.24                                                
Validation - loss=7.7264e-01 ppl=2.17 best_loss=7.3421e-01 best_ppl=2.08                                                

real	8m14.317s
user	8m5.211s
sys	0m7.895s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-rkmy.100.0.22-1.24.0.77-2.17.pth
BLEU = 73.61, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.58.0.40-1.50.0.82-2.27.pth
BLEU = 70.70, 85.5/75.3/65.9/58.9 (BP=1.000, ratio=1.046, hyp_len=24592, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.59.0.39-1.47.0.81-2.25.pth
BLEU = 72.99, 87.2/77.4/68.4/61.4 (BP=1.000, ratio=1.022, hyp_len=24032, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.60.0.45-1.57.0.77-2.17.pth
BLEU = 71.53, 86.1/75.9/66.8/60.0 (BP=1.000, ratio=1.038, hyp_len=24407, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.61.0.41-1.50.0.80-2.22.pth
BLEU = 72.71, 86.8/77.1/68.2/61.3 (BP=1.000, ratio=1.028, hyp_len=24160, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.62.0.38-1.47.0.81-2.24.pth
BLEU = 71.54, 86.2/76.1/66.8/59.7 (BP=1.000, ratio=1.028, hyp_len=24170, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.63.0.41-1.50.0.79-2.21.pth
BLEU = 72.90, 86.8/77.2/68.4/61.6 (BP=1.000, ratio=1.028, hyp_len=24173, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.64.0.39-1.48.0.77-2.17.pth
BLEU = 72.31, 86.5/76.6/67.7/60.9 (BP=1.000, ratio=1.036, hyp_len=24361, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.65.0.36-1.44.0.78-2.19.pth
BLEU = 73.98, 87.4/78.1/69.6/63.0 (BP=1.000, ratio=1.028, hyp_len=24171, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.66.0.34-1.41.0.78-2.18.pth
BLEU = 73.25, 86.8/77.4/68.9/62.2 (BP=1.000, ratio=1.035, hyp_len=24338, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.67.0.33-1.40.0.78-2.18.pth
BLEU = 73.88, 87.1/77.9/69.6/63.1 (BP=1.000, ratio=1.033, hyp_len=24293, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.68.0.33-1.40.0.78-2.19.pth
BLEU = 71.74, 86.0/76.1/67.1/60.3 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.69.0.33-1.39.0.78-2.18.pth
BLEU = 73.00, 86.7/77.1/68.5/62.0 (BP=1.000, ratio=1.036, hyp_len=24367, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.70.0.36-1.43.0.80-2.22.pth
BLEU = 71.69, 85.9/76.0/67.1/60.3 (BP=1.000, ratio=1.045, hyp_len=24572, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.71.0.34-1.41.0.77-2.16.pth
BLEU = 73.85, 87.3/78.0/69.5/62.9 (BP=1.000, ratio=1.029, hyp_len=24196, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.72.0.35-1.42.0.87-2.38.pth
BLEU = 70.74, 85.8/75.8/66.0/58.3 (BP=1.000, ratio=1.045, hyp_len=24573, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.73.0.33-1.40.0.80-2.22.pth
BLEU = 71.72, 85.9/76.1/67.2/60.3 (BP=1.000, ratio=1.049, hyp_len=24669, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.74.0.32-1.38.0.76-2.14.pth
BLEU = 73.46, 86.9/77.6/69.1/62.5 (BP=1.000, ratio=1.036, hyp_len=24353, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.75.0.32-1.38.0.75-2.11.pth
BLEU = 73.96, 87.3/78.1/69.6/63.0 (BP=1.000, ratio=1.032, hyp_len=24250, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.76.0.30-1.35.0.77-2.15.pth
BLEU = 73.67, 87.1/77.8/69.3/62.8 (BP=1.000, ratio=1.037, hyp_len=24384, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.77.0.33-1.39.0.77-2.16.pth
BLEU = 71.94, 86.1/76.2/67.3/60.6 (BP=1.000, ratio=1.038, hyp_len=24406, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.78.0.39-1.48.0.78-2.19.pth
BLEU = 70.66, 85.3/75.2/66.0/58.8 (BP=1.000, ratio=1.035, hyp_len=24338, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.79.0.34-1.41.0.74-2.10.pth
BLEU = 74.16, 87.4/78.2/69.9/63.4 (BP=1.000, ratio=1.030, hyp_len=24213, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.80.0.31-1.36.0.77-2.15.pth
BLEU = 73.04, 86.6/77.2/68.6/62.0 (BP=1.000, ratio=1.040, hyp_len=24446, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.81.0.29-1.34.0.75-2.12.pth
BLEU = 73.00, 86.6/77.1/68.5/62.1 (BP=1.000, ratio=1.040, hyp_len=24446, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.82.0.28-1.32.0.75-2.13.pth
BLEU = 74.27, 87.4/78.3/70.0/63.5 (BP=1.000, ratio=1.029, hyp_len=24195, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.83.0.29-1.33.0.76-2.14.pth
BLEU = 73.20, 86.8/77.4/68.7/62.1 (BP=1.000, ratio=1.040, hyp_len=24448, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.84.0.28-1.33.0.76-2.14.pth
BLEU = 74.52, 87.6/78.5/70.2/63.9 (BP=1.000, ratio=1.029, hyp_len=24198, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.85.0.28-1.33.0.74-2.10.pth
BLEU = 74.32, 87.3/78.2/70.1/63.7 (BP=1.000, ratio=1.036, hyp_len=24354, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.86.0.27-1.31.0.74-2.09.pth
BLEU = 74.19, 87.3/78.1/69.9/63.5 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.87.0.28-1.33.0.76-2.13.pth
BLEU = 73.69, 87.1/77.8/69.3/62.7 (BP=1.000, ratio=1.039, hyp_len=24430, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.88.0.26-1.30.0.74-2.10.pth
BLEU = 71.84, 86.0/76.2/67.3/60.5 (BP=1.000, ratio=1.046, hyp_len=24582, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.89.0.28-1.33.0.73-2.08.pth
BLEU = 72.50, 86.4/76.8/68.0/61.2 (BP=1.000, ratio=1.044, hyp_len=24533, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.90.0.24-1.28.0.77-2.15.pth
BLEU = 74.45, 87.4/78.3/70.2/63.9 (BP=1.000, ratio=1.035, hyp_len=24327, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.91.0.25-1.28.0.76-2.14.pth
BLEU = 74.48, 87.5/78.4/70.2/63.8 (BP=1.000, ratio=1.031, hyp_len=24231, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.92.0.26-1.30.0.76-2.14.pth
BLEU = 73.34, 86.8/77.4/69.0/62.5 (BP=1.000, ratio=1.043, hyp_len=24530, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.93.0.24-1.28.0.75-2.11.pth
BLEU = 74.18, 87.3/78.2/69.9/63.5 (BP=1.000, ratio=1.036, hyp_len=24353, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.94.0.25-1.28.0.77-2.16.pth
BLEU = 74.15, 87.3/78.1/69.8/63.5 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.95.0.24-1.27.0.78-2.18.pth
BLEU = 73.82, 87.2/77.9/69.5/62.9 (BP=1.000, ratio=1.036, hyp_len=24347, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.96.0.24-1.27.0.78-2.18.pth
BLEU = 73.91, 87.2/78.0/69.6/63.0 (BP=1.000, ratio=1.035, hyp_len=24339, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.97.0.24-1.26.0.75-2.11.pth
BLEU = 74.19, 87.4/78.1/69.9/63.5 (BP=1.000, ratio=1.038, hyp_len=24397, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.98.0.24-1.27.0.76-2.14.pth
BLEU = 73.68, 87.0/77.6/69.3/63.0 (BP=1.000, ratio=1.041, hyp_len=24482, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.99.0.24-1.27.0.78-2.19.pth
BLEU = 73.84, 87.0/77.7/69.5/63.2 (BP=1.000, ratio=1.040, hyp_len=24440, ref_len=23509)

real	18m22.677s
user	13m55.909s
sys	2m4.986s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-60epoch$
```

Baseline: seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth, BLEU = 72.06  
RL rk-my, 60-40 model ရဲ့ အကောင်းဆုံး BLEU score က ...  

```
Evaluation result for the model: seq-rl-model-rkmy.84.0.28-1.33.0.76-2.14.pth
BLEU = 74.52, 87.6/78.5/70.2/63.9 (BP=1.000, ratio=1.029, hyp_len=24198, ref_len=23509)
```

### RL, rk-my, 70-30 model

training...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth --model_fn ./model/rl/seq2seq/rkmy-70epoch/seq-rl-model-rkmy.pth --init_epoch 67 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/rkmy-70epoch/seq-rl-model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 67
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 67,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'load_fn': './model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/rkmy-70epoch/seq-rl-model-rkmy.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1640, 128)
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
Epoch 67 - |param|=6.70e+02 |g_param|=1.84e+05 loss=2.8260e-01 ppl=1.33                                                 
Validation - loss=6.4225e-01 ppl=1.90 best_loss=inf best_ppl=inf                                                        
Epoch 68 - |param|=6.70e+02 |g_param|=1.46e+05 loss=2.6439e-01 ppl=1.30                                                 
Validation - loss=6.4491e-01 ppl=1.91 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 69 - |param|=6.71e+02 |g_param|=1.64e+05 loss=2.6934e-01 ppl=1.31                                                 
Validation - loss=6.4685e-01 ppl=1.91 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 70 - |param|=6.71e+02 |g_param|=8.84e+04 loss=2.6017e-01 ppl=1.30                                                 
Validation - loss=6.4966e-01 ppl=1.91 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 71 - |param|=6.71e+02 |g_param|=7.10e+04 loss=2.4822e-01 ppl=1.28                                                 
Validation - loss=6.5280e-01 ppl=1.92 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 72 - |param|=6.72e+02 |g_param|=9.60e+04 loss=2.5878e-01 ppl=1.30                                                 
Validation - loss=6.8635e-01 ppl=1.99 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 73 - |param|=6.72e+02 |g_param|=9.60e+04 loss=2.7719e-01 ppl=1.32                                                 
Validation - loss=6.6682e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 74 - |param|=6.72e+02 |g_param|=5.28e+04 loss=2.7756e-01 ppl=1.32                                                 
Validation - loss=6.8487e-01 ppl=1.98 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 75 - |param|=6.73e+02 |g_param|=5.39e+04 loss=2.6596e-01 ppl=1.30                                                 
Validation - loss=6.8875e-01 ppl=1.99 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 76 - |param|=6.73e+02 |g_param|=5.17e+04 loss=2.5890e-01 ppl=1.30                                                 
Validation - loss=6.6579e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 77 - |param|=6.73e+02 |g_param|=4.21e+04 loss=2.4675e-01 ppl=1.28                                                 
Validation - loss=6.5045e-01 ppl=1.92 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 78 - |param|=6.74e+02 |g_param|=3.48e+04 loss=2.3145e-01 ppl=1.26                                                 
Validation - loss=6.5818e-01 ppl=1.93 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 79 - |param|=6.74e+02 |g_param|=4.09e+04 loss=2.4875e-01 ppl=1.28                                                 
Validation - loss=6.6527e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 80 - |param|=6.74e+02 |g_param|=3.48e+04 loss=2.2990e-01 ppl=1.26                                                 
Validation - loss=6.5396e-01 ppl=1.92 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 81 - |param|=6.74e+02 |g_param|=3.79e+04 loss=2.1679e-01 ppl=1.24                                                 
Validation - loss=6.5734e-01 ppl=1.93 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 82 - |param|=6.75e+02 |g_param|=4.13e+04 loss=2.2339e-01 ppl=1.25                                                 
Validation - loss=6.6647e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 83 - |param|=6.75e+02 |g_param|=3.98e+04 loss=2.2571e-01 ppl=1.25                                                 
Validation - loss=6.6525e-01 ppl=1.94 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 84 - |param|=6.75e+02 |g_param|=5.64e+04 loss=2.3433e-01 ppl=1.26                                                 
Validation - loss=6.5802e-01 ppl=1.93 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 85 - |param|=6.76e+02 |g_param|=4.04e+04 loss=2.1302e-01 ppl=1.24                                                 
Validation - loss=6.6230e-01 ppl=1.94 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 86 - |param|=6.76e+02 |g_param|=3.64e+04 loss=2.1527e-01 ppl=1.24                                                 
Validation - loss=6.5570e-01 ppl=1.93 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 87 - |param|=6.76e+02 |g_param|=4.74e+04 loss=2.3378e-01 ppl=1.26                                                 
Validation - loss=6.4863e-01 ppl=1.91 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 88 - |param|=6.77e+02 |g_param|=4.36e+04 loss=2.2142e-01 ppl=1.25                                                 
Validation - loss=6.6604e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 89 - |param|=6.77e+02 |g_param|=4.06e+04 loss=2.0023e-01 ppl=1.22                                                 
Validation - loss=6.6515e-01 ppl=1.94 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 90 - |param|=6.77e+02 |g_param|=3.69e+04 loss=1.9977e-01 ppl=1.22                                                 
Validation - loss=6.6295e-01 ppl=1.94 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 91 - |param|=6.78e+02 |g_param|=3.37e+04 loss=1.8981e-01 ppl=1.21                                                 
Validation - loss=6.5056e-01 ppl=1.92 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 92 - |param|=6.78e+02 |g_param|=5.60e+04 loss=2.1686e-01 ppl=1.24                                                 
Validation - loss=6.8482e-01 ppl=1.98 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 93 - |param|=6.78e+02 |g_param|=3.93e+04 loss=1.9367e-01 ppl=1.21                                                 
Validation - loss=6.9213e-01 ppl=2.00 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 94 - |param|=6.79e+02 |g_param|=7.19e+04 loss=1.9223e-01 ppl=1.21                                                 
Validation - loss=6.7743e-01 ppl=1.97 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 95 - |param|=6.79e+02 |g_param|=7.84e+04 loss=1.9561e-01 ppl=1.22                                                 
Validation - loss=6.7005e-01 ppl=1.95 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 96 - |param|=6.79e+02 |g_param|=7.97e+04 loss=1.8232e-01 ppl=1.20                                                 
Validation - loss=6.8228e-01 ppl=1.98 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 97 - |param|=6.79e+02 |g_param|=8.09e+04 loss=1.8839e-01 ppl=1.21                                                 
Validation - loss=6.8091e-01 ppl=1.98 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 98 - |param|=6.80e+02 |g_param|=8.26e+04 loss=1.8778e-01 ppl=1.21                                                 
Validation - loss=6.8262e-01 ppl=1.98 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 99 - |param|=6.80e+02 |g_param|=1.13e+05 loss=2.0670e-01 ppl=1.23                                                 
Validation - loss=7.1175e-01 ppl=2.04 best_loss=6.4225e-01 best_ppl=1.90                                                
Epoch 100 - |param|=6.80e+02 |g_param|=7.39e+04 loss=1.8576e-01 ppl=1.20                                                
Validation - loss=6.5266e-01 ppl=1.92 best_loss=6.4225e-01 best_ppl=1.90                                                

real	6m30.101s
user	6m24.883s
sys	0m5.737s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-rkmy.100.0.19-1.20.0.65-1.92.pth
BLEU = 72.94, 86.5/77.1/68.5/62.0 (BP=1.000, ratio=1.046, hyp_len=24597, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.67.0.28-1.33.0.64-1.90.pth
BLEU = 73.84, 87.2/77.9/69.5/63.0 (BP=1.000, ratio=1.037, hyp_len=24380, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.68.0.26-1.30.0.64-1.91.pth
BLEU = 74.41, 87.5/78.4/70.1/63.7 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.69.0.27-1.31.0.65-1.91.pth
BLEU = 73.44, 87.0/77.6/69.1/62.4 (BP=1.000, ratio=1.039, hyp_len=24419, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.70.0.26-1.30.0.65-1.91.pth
BLEU = 72.79, 86.5/76.9/68.4/61.7 (BP=1.000, ratio=1.044, hyp_len=24546, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.71.0.25-1.28.0.65-1.92.pth
BLEU = 74.18, 87.3/78.2/69.9/63.4 (BP=1.000, ratio=1.035, hyp_len=24339, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.72.0.26-1.30.0.69-1.99.pth
BLEU = 71.59, 85.8/76.1/67.1/60.0 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.73.0.28-1.32.0.67-1.95.pth
BLEU = 72.67, 86.5/76.8/68.2/61.5 (BP=1.000, ratio=1.043, hyp_len=24519, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.74.0.28-1.32.0.68-1.98.pth
BLEU = 73.69, 87.1/77.8/69.3/62.8 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.75.0.27-1.30.0.69-1.99.pth
BLEU = 73.75, 87.4/78.0/69.3/62.7 (BP=1.000, ratio=1.030, hyp_len=24224, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.76.0.26-1.30.0.67-1.95.pth
BLEU = 72.49, 86.3/76.7/68.0/61.3 (BP=1.000, ratio=1.048, hyp_len=24639, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.77.0.25-1.28.0.65-1.92.pth
BLEU = 73.99, 87.3/78.0/69.6/63.2 (BP=1.000, ratio=1.037, hyp_len=24381, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.78.0.23-1.26.0.66-1.93.pth
BLEU = 73.71, 87.0/77.7/69.4/63.0 (BP=1.000, ratio=1.041, hyp_len=24469, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.79.0.25-1.28.0.67-1.95.pth
BLEU = 72.63, 86.3/76.7/68.2/61.6 (BP=1.000, ratio=1.047, hyp_len=24614, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.80.0.23-1.26.0.65-1.92.pth
BLEU = 72.64, 86.4/76.8/68.1/61.6 (BP=1.000, ratio=1.046, hyp_len=24595, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.81.0.22-1.24.0.66-1.93.pth
BLEU = 74.22, 87.4/78.2/69.9/63.5 (BP=1.000, ratio=1.037, hyp_len=24375, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.82.0.22-1.25.0.67-1.95.pth
BLEU = 72.85, 86.6/77.0/68.4/61.8 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.83.0.23-1.25.0.67-1.94.pth
BLEU = 73.16, 86.7/77.2/68.8/62.3 (BP=1.000, ratio=1.043, hyp_len=24522, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.84.0.23-1.26.0.66-1.93.pth
BLEU = 72.86, 86.5/77.1/68.5/61.7 (BP=1.000, ratio=1.046, hyp_len=24600, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.85.0.21-1.24.0.66-1.94.pth
BLEU = 72.72, 86.4/77.0/68.3/61.5 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.86.0.22-1.24.0.66-1.93.pth
BLEU = 72.37, 86.3/76.6/67.9/61.2 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.87.0.23-1.26.0.65-1.91.pth
BLEU = 73.86, 87.2/77.8/69.5/63.1 (BP=1.000, ratio=1.039, hyp_len=24417, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.88.0.22-1.25.0.67-1.95.pth
BLEU = 73.38, 86.9/77.5/69.0/62.4 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.89.0.20-1.22.0.67-1.94.pth
BLEU = 73.13, 86.6/77.2/68.8/62.2 (BP=1.000, ratio=1.046, hyp_len=24597, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.90.0.20-1.22.0.66-1.94.pth
BLEU = 73.44, 86.9/77.5/69.1/62.5 (BP=1.000, ratio=1.043, hyp_len=24518, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.91.0.19-1.21.0.65-1.92.pth
BLEU = 73.82, 87.0/77.8/69.5/63.1 (BP=1.000, ratio=1.043, hyp_len=24514, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.92.0.22-1.24.0.68-1.98.pth
BLEU = 73.30, 86.9/77.4/68.9/62.3 (BP=1.000, ratio=1.042, hyp_len=24489, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.93.0.19-1.21.0.69-2.00.pth
BLEU = 74.48, 87.5/78.5/70.2/63.8 (BP=1.000, ratio=1.036, hyp_len=24351, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.94.0.19-1.21.0.68-1.97.pth
BLEU = 74.34, 87.4/78.3/70.1/63.7 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.95.0.20-1.22.0.67-1.95.pth
BLEU = 73.71, 87.0/77.7/69.4/62.9 (BP=1.000, ratio=1.042, hyp_len=24499, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.96.0.18-1.20.0.68-1.98.pth
BLEU = 73.57, 87.0/77.7/69.2/62.7 (BP=1.000, ratio=1.042, hyp_len=24503, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.97.0.19-1.21.0.68-1.98.pth
BLEU = 73.13, 86.9/77.3/68.7/61.9 (BP=1.000, ratio=1.042, hyp_len=24494, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.98.0.19-1.21.0.68-1.98.pth
BLEU = 73.44, 86.9/77.6/69.1/62.4 (BP=1.000, ratio=1.042, hyp_len=24495, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.99.0.21-1.23.0.71-2.04.pth
BLEU = 72.00, 86.2/76.5/67.4/60.4 (BP=1.000, ratio=1.050, hyp_len=24675, ref_len=23509)

real	11m38.229s
user	11m21.839s
sys	0m38.634s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/rkmy-70epoch$
```

Baseline က : BLEU = 74.84  
RL 70-30, rk-my best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: seq-rl-model-rkmy.93.0.19-1.21.0.69-2.00.pth
BLEU = 74.48, 87.5/78.5/70.2/63.8 (BP=1.000, ratio=1.036, hyp_len=24351, ref_len=23509)
```

## RL Transformer

### RL, my-rk, 40-60 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth --model_fn ./model/rl/transformer/myrk-40epoch/transformer-rl-myrk.pth --init_epoch 39 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/myrk-40epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 39
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 39,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/baseline/myrk-40epoch/myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/myrk-40epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 39 - |param|=3.26e+02 |g_param|=5.44e+05 loss=1.8557e+00 ppl=6.40                                                 
Validation - loss=1.7443e+00 ppl=5.72 best_loss=inf best_ppl=inf                                                        
Epoch 40 - |param|=3.26e+02 |g_param|=4.23e+05 loss=1.7858e+00 ppl=5.96                                                 
Validation - loss=1.7066e+00 ppl=5.51 best_loss=1.7443e+00 best_ppl=5.72                                                
Epoch 41 - |param|=3.26e+02 |g_param|=6.27e+05 loss=1.7408e+00 ppl=5.70                                                 
Validation - loss=1.6807e+00 ppl=5.37 best_loss=1.7066e+00 best_ppl=5.51                                                
Epoch 42 - |param|=3.26e+02 |g_param|=6.77e+05 loss=1.7798e+00 ppl=5.93                                                 
Validation - loss=1.6799e+00 ppl=5.37 best_loss=1.6807e+00 best_ppl=5.37                                                
Epoch 43 - |param|=3.26e+02 |g_param|=4.03e+05 loss=1.7420e+00 ppl=5.71                                                 
Validation - loss=1.6268e+00 ppl=5.09 best_loss=1.6799e+00 best_ppl=5.37                                                
Epoch 44 - |param|=3.26e+02 |g_param|=5.63e+05 loss=1.7458e+00 ppl=5.73                                                 
Validation - loss=1.6022e+00 ppl=4.96 best_loss=1.6268e+00 best_ppl=5.09                                                
Epoch 45 - |param|=3.26e+02 |g_param|=7.44e+05 loss=1.7307e+00 ppl=5.64                                                 
Validation - loss=1.5786e+00 ppl=4.85 best_loss=1.6022e+00 best_ppl=4.96                                                
Epoch 46 - |param|=3.26e+02 |g_param|=4.15e+05 loss=1.6502e+00 ppl=5.21                                                 
Validation - loss=1.5633e+00 ppl=4.77 best_loss=1.5786e+00 best_ppl=4.85                                                
Epoch 47 - |param|=3.26e+02 |g_param|=4.88e+05 loss=1.6606e+00 ppl=5.26                                                 
Validation - loss=1.5313e+00 ppl=4.62 best_loss=1.5633e+00 best_ppl=4.77                                                
Epoch 48 - |param|=3.26e+02 |g_param|=5.01e+05 loss=1.6036e+00 ppl=4.97                                                 
Validation - loss=1.5116e+00 ppl=4.53 best_loss=1.5313e+00 best_ppl=4.62                                                
Epoch 49 - |param|=3.26e+02 |g_param|=5.32e+05 loss=1.6005e+00 ppl=4.96                                                 
Validation - loss=1.4855e+00 ppl=4.42 best_loss=1.5116e+00 best_ppl=4.53                                                
Epoch 50 - |param|=3.26e+02 |g_param|=7.22e+05 loss=1.5931e+00 ppl=4.92                                                 
Validation - loss=1.4730e+00 ppl=4.36 best_loss=1.4855e+00 best_ppl=4.42                                                
Epoch 51 - |param|=3.26e+02 |g_param|=4.53e+05 loss=1.6081e+00 ppl=4.99                                                 
Validation - loss=1.4418e+00 ppl=4.23 best_loss=1.4730e+00 best_ppl=4.36                                                
Epoch 52 - |param|=3.26e+02 |g_param|=6.56e+05 loss=1.5441e+00 ppl=4.68                                                 
Validation - loss=1.4252e+00 ppl=4.16 best_loss=1.4418e+00 best_ppl=4.23                                                
Epoch 53 - |param|=3.26e+02 |g_param|=5.55e+05 loss=1.5702e+00 ppl=4.81                                                 
Validation - loss=1.4038e+00 ppl=4.07 best_loss=1.4252e+00 best_ppl=4.16                                                
Epoch 54 - |param|=3.26e+02 |g_param|=5.29e+05 loss=1.5303e+00 ppl=4.62                                                 
Validation - loss=1.3905e+00 ppl=4.02 best_loss=1.4038e+00 best_ppl=4.07                                                
Epoch 55 - |param|=3.26e+02 |g_param|=7.46e+05 loss=1.4572e+00 ppl=4.29                                                 
Validation - loss=1.3740e+00 ppl=3.95 best_loss=1.3905e+00 best_ppl=4.02                                                
Epoch 56 - |param|=3.26e+02 |g_param|=5.10e+05 loss=1.4879e+00 ppl=4.43                                                 
Validation - loss=1.3622e+00 ppl=3.90 best_loss=1.3740e+00 best_ppl=3.95                                                
Epoch 57 - |param|=3.26e+02 |g_param|=6.26e+05 loss=1.5131e+00 ppl=4.54                                                 
Validation - loss=1.3433e+00 ppl=3.83 best_loss=1.3622e+00 best_ppl=3.90                                                
Epoch 58 - |param|=3.26e+02 |g_param|=6.95e+05 loss=1.4665e+00 ppl=4.33                                                 
Validation - loss=1.3417e+00 ppl=3.83 best_loss=1.3433e+00 best_ppl=3.83                                                
Epoch 59 - |param|=3.26e+02 |g_param|=1.09e+06 loss=1.4531e+00 ppl=4.28                                                 
Validation - loss=1.3533e+00 ppl=3.87 best_loss=1.3417e+00 best_ppl=3.83                                                
Epoch 60 - |param|=3.26e+02 |g_param|=5.18e+05 loss=1.4613e+00 ppl=4.31                                                 
Validation - loss=1.2993e+00 ppl=3.67 best_loss=1.3417e+00 best_ppl=3.83                                                
Epoch 61 - |param|=3.26e+02 |g_param|=6.19e+05 loss=1.4187e+00 ppl=4.13                                                 
Validation - loss=1.2835e+00 ppl=3.61 best_loss=1.2993e+00 best_ppl=3.67                                                
Epoch 62 - |param|=3.26e+02 |g_param|=7.90e+05 loss=1.4859e+00 ppl=4.42                                                 
Validation - loss=1.2862e+00 ppl=3.62 best_loss=1.2835e+00 best_ppl=3.61                                                
Epoch 63 - |param|=3.26e+02 |g_param|=5.25e+05 loss=1.3456e+00 ppl=3.84                                                 
Validation - loss=1.2649e+00 ppl=3.54 best_loss=1.2835e+00 best_ppl=3.61                                                
Epoch 64 - |param|=3.26e+02 |g_param|=7.43e+05 loss=1.3475e+00 ppl=3.85                                                 
Validation - loss=1.2698e+00 ppl=3.56 best_loss=1.2649e+00 best_ppl=3.54                                                
Epoch 65 - |param|=3.26e+02 |g_param|=7.39e+05 loss=1.3577e+00 ppl=3.89                                                 
Validation - loss=1.2351e+00 ppl=3.44 best_loss=1.2649e+00 best_ppl=3.54                                                
Epoch 66 - |param|=3.26e+02 |g_param|=6.28e+05 loss=1.3859e+00 ppl=4.00                                                 
Validation - loss=1.2270e+00 ppl=3.41 best_loss=1.2351e+00 best_ppl=3.44                                                
Epoch 67 - |param|=3.26e+02 |g_param|=6.17e+05 loss=1.3666e+00 ppl=3.92                                                 
Validation - loss=1.2240e+00 ppl=3.40 best_loss=1.2270e+00 best_ppl=3.41                                                
Epoch 68 - |param|=3.26e+02 |g_param|=5.18e+05 loss=1.3452e+00 ppl=3.84                                                 
Validation - loss=1.2237e+00 ppl=3.40 best_loss=1.2240e+00 best_ppl=3.40                                                
Epoch 69 - |param|=3.26e+02 |g_param|=5.87e+05 loss=1.2931e+00 ppl=3.64                                                 
Validation - loss=1.1938e+00 ppl=3.30 best_loss=1.2237e+00 best_ppl=3.40                                                
Epoch 70 - |param|=3.26e+02 |g_param|=5.77e+05 loss=1.3112e+00 ppl=3.71                                                 
Validation - loss=1.1843e+00 ppl=3.27 best_loss=1.1938e+00 best_ppl=3.30                                                
Epoch 71 - |param|=3.26e+02 |g_param|=5.73e+05 loss=1.2951e+00 ppl=3.65                                                 
Validation - loss=1.1816e+00 ppl=3.26 best_loss=1.1843e+00 best_ppl=3.27                                                
Epoch 72 - |param|=3.26e+02 |g_param|=7.80e+05 loss=1.3705e+00 ppl=3.94                                                 
Validation - loss=1.2121e+00 ppl=3.36 best_loss=1.1816e+00 best_ppl=3.26                                                
Epoch 73 - |param|=3.26e+02 |g_param|=5.56e+05 loss=1.2411e+00 ppl=3.46                                                 
Validation - loss=1.1623e+00 ppl=3.20 best_loss=1.1816e+00 best_ppl=3.26                                                
Epoch 74 - |param|=3.26e+02 |g_param|=8.72e+05 loss=1.2731e+00 ppl=3.57                                                 
Validation - loss=1.1993e+00 ppl=3.32 best_loss=1.1623e+00 best_ppl=3.20                                                
Epoch 75 - |param|=3.26e+02 |g_param|=8.08e+05 loss=1.2602e+00 ppl=3.53                                                 
Validation - loss=1.1572e+00 ppl=3.18 best_loss=1.1623e+00 best_ppl=3.20                                                
Epoch 76 - |param|=3.26e+02 |g_param|=5.12e+05 loss=1.2555e+00 ppl=3.51                                                 
Validation - loss=1.1306e+00 ppl=3.10 best_loss=1.1572e+00 best_ppl=3.18                                                
Epoch 77 - |param|=3.26e+02 |g_param|=4.90e+05 loss=1.2344e+00 ppl=3.44                                                 
Validation - loss=1.1206e+00 ppl=3.07 best_loss=1.1306e+00 best_ppl=3.10                                                
Epoch 78 - |param|=3.26e+02 |g_param|=9.92e+05 loss=1.1905e+00 ppl=3.29                                                 
Validation - loss=1.1689e+00 ppl=3.22 best_loss=1.1206e+00 best_ppl=3.07                                                
Epoch 79 - |param|=3.26e+02 |g_param|=9.33e+05 loss=1.2071e+00 ppl=3.34                                                 
Validation - loss=1.1196e+00 ppl=3.06 best_loss=1.1206e+00 best_ppl=3.07                                                
Epoch 80 - |param|=3.27e+02 |g_param|=5.97e+05 loss=1.2133e+00 ppl=3.36                                                 
Validation - loss=1.1070e+00 ppl=3.03 best_loss=1.1196e+00 best_ppl=3.06                                                
Epoch 81 - |param|=3.27e+02 |g_param|=8.39e+05 loss=1.1970e+00 ppl=3.31                                                 
Validation - loss=1.1024e+00 ppl=3.01 best_loss=1.1070e+00 best_ppl=3.03                                                
Epoch 82 - |param|=3.27e+02 |g_param|=1.01e+06 loss=1.1502e+00 ppl=3.16                                                 
Validation - loss=1.1089e+00 ppl=3.03 best_loss=1.1024e+00 best_ppl=3.01                                                
Epoch 83 - |param|=3.27e+02 |g_param|=8.51e+05 loss=1.3021e+00 ppl=3.68                                                 
Validation - loss=1.0838e+00 ppl=2.96 best_loss=1.1024e+00 best_ppl=3.01                                                
Epoch 84 - |param|=3.27e+02 |g_param|=6.32e+05 loss=1.1979e+00 ppl=3.31                                                 
Validation - loss=1.0786e+00 ppl=2.94 best_loss=1.0838e+00 best_ppl=2.96                                                
Epoch 85 - |param|=3.27e+02 |g_param|=1.27e+06 loss=1.1926e+00 ppl=3.30                                                 
Validation - loss=1.0967e+00 ppl=2.99 best_loss=1.0786e+00 best_ppl=2.94                                                
Epoch 86 - |param|=3.27e+02 |g_param|=5.72e+05 loss=1.1423e+00 ppl=3.13                                                 
Validation - loss=1.0706e+00 ppl=2.92 best_loss=1.0786e+00 best_ppl=2.94                                                
Epoch 87 - |param|=3.27e+02 |g_param|=7.76e+05 loss=1.1018e+00 ppl=3.01                                                 
Validation - loss=1.0643e+00 ppl=2.90 best_loss=1.0706e+00 best_ppl=2.92                                                
Epoch 88 - |param|=3.27e+02 |g_param|=1.36e+06 loss=1.1523e+00 ppl=3.17                                                 
Validation - loss=1.0668e+00 ppl=2.91 best_loss=1.0643e+00 best_ppl=2.90                                                
Epoch 89 - |param|=3.27e+02 |g_param|=1.10e+06 loss=1.2005e+00 ppl=3.32                                                 
Validation - loss=1.0510e+00 ppl=2.86 best_loss=1.0643e+00 best_ppl=2.90                                                
Epoch 90 - |param|=3.27e+02 |g_param|=8.38e+05 loss=1.1766e+00 ppl=3.24                                                 
Validation - loss=1.0753e+00 ppl=2.93 best_loss=1.0510e+00 best_ppl=2.86                                                
Epoch 91 - |param|=3.27e+02 |g_param|=1.25e+06 loss=1.1327e+00 ppl=3.10                                                 
Validation - loss=1.0397e+00 ppl=2.83 best_loss=1.0510e+00 best_ppl=2.86                                                
Epoch 92 - |param|=3.27e+02 |g_param|=1.04e+06 loss=1.1535e+00 ppl=3.17                                                 
Validation - loss=1.0578e+00 ppl=2.88 best_loss=1.0397e+00 best_ppl=2.83                                                
Epoch 93 - |param|=3.27e+02 |g_param|=7.16e+05 loss=1.1258e+00 ppl=3.08                                                 
Validation - loss=1.0270e+00 ppl=2.79 best_loss=1.0397e+00 best_ppl=2.83                                                
Epoch 94 - |param|=3.27e+02 |g_param|=7.33e+05 loss=1.0726e+00 ppl=2.92                                                 
Validation - loss=1.0237e+00 ppl=2.78 best_loss=1.0270e+00 best_ppl=2.79                                                
Epoch 95 - |param|=3.27e+02 |g_param|=8.53e+05 loss=1.0897e+00 ppl=2.97                                                 
Validation - loss=1.0168e+00 ppl=2.76 best_loss=1.0237e+00 best_ppl=2.78                                                
Epoch 96 - |param|=3.27e+02 |g_param|=1.53e+06 loss=1.1084e+00 ppl=3.03                                                 
Validation - loss=1.0201e+00 ppl=2.77 best_loss=1.0168e+00 best_ppl=2.76                                                
Epoch 97 - |param|=3.27e+02 |g_param|=1.14e+06 loss=1.0931e+00 ppl=2.98                                                 
Validation - loss=1.0027e+00 ppl=2.73 best_loss=1.0168e+00 best_ppl=2.76                                                
Epoch 98 - |param|=3.27e+02 |g_param|=1.12e+06 loss=1.0728e+00 ppl=2.92                                                 
Validation - loss=1.0315e+00 ppl=2.81 best_loss=1.0027e+00 best_ppl=2.73                                                
Epoch 99 - |param|=3.27e+02 |g_param|=1.08e+06 loss=1.0669e+00 ppl=2.91                                                 
Validation - loss=1.0488e+00 ppl=2.85 best_loss=1.0027e+00 best_ppl=2.73                                                
Epoch 100 - |param|=3.27e+02 |g_param|=6.00e+05 loss=1.0694e+00 ppl=2.91                                                
Validation - loss=1.0067e+00 ppl=2.74 best_loss=1.0027e+00 best_ppl=2.73                                                

real	32m8.945s
user	32m2.663s
sys	0m5.688s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.39.1.86-6.40.1.74-5.72.pth
BLEU = 35.66, 65.5/43.8/29.2/19.3 (BP=1.000, ratio=1.041, hyp_len=24118, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.40.1.79-5.96.1.71-5.51.pth
BLEU = 37.56, 67.4/45.6/30.9/20.9 (BP=1.000, ratio=1.017, hyp_len=23555, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.41.1.74-5.70.1.68-5.37.pth
BLEU = 36.79, 66.5/45.1/30.3/20.2 (BP=1.000, ratio=1.043, hyp_len=24167, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.42.1.78-5.93.1.68-5.37.pth
BLEU = 36.63, 65.5/44.7/30.3/20.3 (BP=1.000, ratio=1.070, hyp_len=24770, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.43.1.74-5.71.1.63-5.09.pth
BLEU = 38.76, 68.2/46.9/32.2/22.0 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.44.1.75-5.73.1.60-4.96.pth
BLEU = 38.77, 67.9/47.0/32.2/22.0 (BP=1.000, ratio=1.037, hyp_len=24021, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.45.1.73-5.64.1.58-4.85.pth
BLEU = 40.30, 68.9/48.1/33.7/23.6 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.46.1.65-5.21.1.56-4.77.pth
BLEU = 39.27, 67.8/47.3/32.8/22.6 (BP=1.000, ratio=1.052, hyp_len=24370, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.47.1.66-5.26.1.53-4.62.pth
BLEU = 40.15, 68.3/48.2/33.8/23.4 (BP=1.000, ratio=1.061, hyp_len=24567, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.48.1.60-4.97.1.51-4.53.pth
BLEU = 40.43, 68.3/48.4/34.0/23.8 (BP=1.000, ratio=1.063, hyp_len=24618, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.49.1.60-4.96.1.49-4.42.pth
BLEU = 42.96, 71.2/50.9/36.4/25.8 (BP=1.000, ratio=1.019, hyp_len=23594, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.50.1.59-4.92.1.47-4.36.pth
BLEU = 41.58, 69.3/49.6/35.2/24.7 (BP=1.000, ratio=1.056, hyp_len=24455, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.51.1.61-4.99.1.44-4.23.pth
BLEU = 43.79, 71.4/51.6/37.3/26.8 (BP=1.000, ratio=1.030, hyp_len=23856, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.52.1.54-4.68.1.43-4.16.pth
BLEU = 43.30, 70.9/51.2/36.8/26.3 (BP=1.000, ratio=1.046, hyp_len=24220, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.53.1.57-4.81.1.40-4.07.pth
BLEU = 44.64, 72.1/52.4/38.1/27.6 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.54.1.53-4.62.1.39-4.02.pth
BLEU = 44.64, 72.0/52.5/38.1/27.6 (BP=1.000, ratio=1.036, hyp_len=24004, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.55.1.46-4.29.1.37-3.95.pth
BLEU = 43.95, 71.0/51.8/37.6/27.0 (BP=1.000, ratio=1.058, hyp_len=24495, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.56.1.49-4.43.1.36-3.90.pth
BLEU = 44.10, 70.8/52.0/37.8/27.2 (BP=1.000, ratio=1.069, hyp_len=24766, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.57.1.51-4.54.1.34-3.83.pth
BLEU = 47.14, 74.1/54.8/40.5/30.0 (BP=1.000, ratio=1.014, hyp_len=23481, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.58.1.47-4.33.1.34-3.83.pth
BLEU = 44.42, 70.9/52.4/38.2/27.4 (BP=1.000, ratio=1.075, hyp_len=24906, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.59.1.45-4.28.1.35-3.87.pth
BLEU = 44.07, 70.3/52.0/38.0/27.2 (BP=1.000, ratio=1.083, hyp_len=25092, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.60.1.46-4.31.1.30-3.67.pth
BLEU = 46.82, 73.3/54.5/40.4/29.8 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.61.1.42-4.13.1.28-3.61.pth
BLEU = 48.08, 73.9/55.6/41.7/31.1 (BP=1.000, ratio=1.038, hyp_len=24035, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.62.1.49-4.42.1.29-3.62.pth
BLEU = 46.87, 73.2/55.0/40.7/29.5 (BP=1.000, ratio=1.054, hyp_len=24411, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.63.1.35-3.84.1.26-3.54.pth
BLEU = 48.59, 74.8/56.4/42.2/31.3 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.64.1.35-3.85.1.27-3.56.pth
BLEU = 47.10, 72.8/54.9/40.9/30.1 (BP=1.000, ratio=1.067, hyp_len=24716, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.65.1.36-3.89.1.24-3.44.pth
BLEU = 49.61, 75.2/57.3/43.3/32.5 (BP=1.000, ratio=1.029, hyp_len=23827, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.66.1.39-4.00.1.23-3.41.pth
BLEU = 49.09, 74.4/56.7/42.8/32.2 (BP=1.000, ratio=1.044, hyp_len=24181, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.67.1.37-3.92.1.22-3.40.pth
BLEU = 49.16, 74.3/56.8/43.0/32.2 (BP=1.000, ratio=1.054, hyp_len=24404, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.68.1.35-3.84.1.22-3.40.pth
BLEU = 48.80, 73.5/56.2/42.8/32.1 (BP=1.000, ratio=1.068, hyp_len=24735, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.69.1.29-3.64.1.19-3.30.pth
BLEU = 51.05, 75.9/58.3/44.7/34.3 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.70.1.31-3.71.1.18-3.27.pth
BLEU = 51.52, 76.2/58.7/45.2/34.8 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.71.1.30-3.65.1.18-3.26.pth
BLEU = 50.64, 75.4/58.0/44.4/33.8 (BP=1.000, ratio=1.044, hyp_len=24190, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.72.1.37-3.94.1.21-3.36.pth
BLEU = 49.16, 74.1/56.9/43.2/32.1 (BP=1.000, ratio=1.069, hyp_len=24765, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.73.1.24-3.46.1.16-3.20.pth
BLEU = 51.99, 76.5/59.3/45.8/35.2 (BP=1.000, ratio=1.034, hyp_len=23951, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.74.1.27-3.57.1.20-3.32.pth
BLEU = 49.84, 74.5/57.6/43.9/32.8 (BP=1.000, ratio=1.069, hyp_len=24767, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.75.1.26-3.53.1.16-3.18.pth
BLEU = 50.45, 74.5/57.8/44.4/33.9 (BP=1.000, ratio=1.071, hyp_len=24794, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.76.1.26-3.51.1.13-3.10.pth
BLEU = 52.03, 75.8/59.2/46.0/35.5 (BP=1.000, ratio=1.053, hyp_len=24376, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.77.1.23-3.44.1.12-3.07.pth
BLEU = 52.92, 77.0/60.2/46.8/36.2 (BP=1.000, ratio=1.040, hyp_len=24087, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.78.1.19-3.29.1.17-3.22.pth
BLEU = 51.17, 75.6/59.0/45.2/34.0 (BP=1.000, ratio=1.060, hyp_len=24545, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.79.1.21-3.34.1.12-3.06.pth
BLEU = 52.83, 76.5/60.0/46.8/36.3 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.80.1.21-3.36.1.11-3.03.pth
BLEU = 52.68, 76.6/60.0/46.6/36.0 (BP=1.000, ratio=1.049, hyp_len=24284, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.81.1.20-3.31.1.10-3.01.pth
BLEU = 53.25, 76.9/60.5/47.3/36.6 (BP=1.000, ratio=1.048, hyp_len=24275, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.82.1.15-3.16.1.11-3.03.pth
BLEU = 52.34, 76.0/59.7/46.4/35.6 (BP=1.000, ratio=1.062, hyp_len=24589, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.83.1.30-3.68.1.08-2.96.pth
BLEU = 54.24, 77.7/61.4/48.2/37.6 (BP=1.000, ratio=1.036, hyp_len=23998, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.84.1.20-3.31.1.08-2.94.pth
BLEU = 55.03, 78.3/62.0/48.9/38.6 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.85.1.19-3.30.1.10-2.99.pth
BLEU = 53.26, 76.8/60.7/47.4/36.4 (BP=1.000, ratio=1.059, hyp_len=24534, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.86.1.14-3.13.1.07-2.92.pth
BLEU = 54.34, 77.4/61.3/48.4/37.9 (BP=1.000, ratio=1.047, hyp_len=24243, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.87.1.10-3.01.1.06-2.90.pth
BLEU = 55.24, 78.3/62.3/49.3/38.7 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.88.1.15-3.17.1.07-2.91.pth
BLEU = 55.41, 77.7/61.9/49.5/39.7 (BP=1.000, ratio=1.042, hyp_len=24127, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.89.1.20-3.32.1.05-2.86.pth
BLEU = 55.79, 78.6/62.7/49.8/39.5 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.90.1.18-3.24.1.08-2.93.pth
BLEU = 53.76, 77.0/61.2/48.0/37.0 (BP=1.000, ratio=1.064, hyp_len=24633, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.91.1.13-3.10.1.04-2.83.pth
BLEU = 55.94, 78.5/62.6/49.9/39.9 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.92.1.15-3.17.1.06-2.88.pth
BLEU = 54.10, 77.3/61.6/48.2/37.3 (BP=1.000, ratio=1.058, hyp_len=24492, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.93.1.13-3.08.1.03-2.79.pth
BLEU = 55.59, 78.2/62.4/49.6/39.4 (BP=1.000, ratio=1.047, hyp_len=24248, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.94.1.07-2.92.1.02-2.78.pth
BLEU = 56.72, 79.3/63.6/50.7/40.5 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.95.1.09-2.97.1.02-2.76.pth
BLEU = 56.92, 79.1/63.5/51.0/40.9 (BP=1.000, ratio=1.038, hyp_len=24031, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.96.1.11-3.03.1.02-2.77.pth
BLEU = 55.99, 78.6/63.1/50.1/39.5 (BP=1.000, ratio=1.047, hyp_len=24248, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.97.1.09-2.98.1.00-2.73.pth
BLEU = 57.59, 79.7/64.2/51.7/41.6 (BP=1.000, ratio=1.030, hyp_len=23849, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.98.1.07-2.92.1.03-2.81.pth
BLEU = 59.13, 81.2/65.4/53.1/43.4 (BP=1.000, ratio=1.006, hyp_len=23292, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.99.1.07-2.91.1.05-2.85.pth
BLEU = 54.56, 77.3/61.9/48.9/37.9 (BP=1.000, ratio=1.070, hyp_len=24789, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.100.1.07-2.91.1.01-2.74.pth
BLEU = 56.62, 79.0/63.6/50.8/40.3 (BP=1.000, ratio=1.046, hyp_len=24222, ref_len=23160)

real	33m30.993s
user	32m52.317s
sys	1m19.865s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-40epoch$
```

Baseline: my-rk, transformer, 40 epoch ရဲ့ Best BLEU score: 35.33  
RL, my-rk, 40-60 model ရဲ့ အများဆုံးက  

```
Evaluation result for the model: transformer-rl-myrk.98.1.07-2.92.1.03-2.81.pth
BLEU = 59.13, 81.2/65.4/53.1/43.4 (BP=1.000, ratio=1.006, hyp_len=23292, ref_len=23160)
```

### RL, my-rk, 50-50 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-50epoch/myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth --model_fn ./model/rl/transformer/myrk-50epoch/transformer-rl-myrk.pth --init_epoch 47 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/myrk-50epoch/myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/myrk-50epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 47
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 47,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/baseline/myrk-50epoch/myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/myrk-50epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 47 - |param|=3.26e+02 |g_param|=4.10e+05 loss=1.6883e+00 ppl=5.41                                                 
Validation - loss=1.5613e+00 ppl=4.76 best_loss=inf best_ppl=inf                                                        
Epoch 48 - |param|=3.26e+02 |g_param|=7.68e+05 loss=1.6035e+00 ppl=4.97                                                 
Validation - loss=1.5246e+00 ppl=4.59 best_loss=1.5613e+00 best_ppl=4.76                                                
Epoch 49 - |param|=3.26e+02 |g_param|=5.77e+05 loss=1.6847e+00 ppl=5.39                                                 
Validation - loss=1.5470e+00 ppl=4.70 best_loss=1.5246e+00 best_ppl=4.59                                                
Epoch 50 - |param|=3.26e+02 |g_param|=5.71e+05 loss=1.6507e+00 ppl=5.21                                                 
Validation - loss=1.4874e+00 ppl=4.43 best_loss=1.5246e+00 best_ppl=4.59                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.36e+05 loss=1.5857e+00 ppl=4.88                                                 
Validation - loss=1.4658e+00 ppl=4.33 best_loss=1.4874e+00 best_ppl=4.43                                                
Epoch 52 - |param|=3.26e+02 |g_param|=5.36e+05 loss=1.5763e+00 ppl=4.84                                                 
Validation - loss=1.4483e+00 ppl=4.26 best_loss=1.4658e+00 best_ppl=4.33                                                
Epoch 53 - |param|=3.26e+02 |g_param|=9.44e+05 loss=1.5533e+00 ppl=4.73                                                 
Validation - loss=1.4997e+00 ppl=4.48 best_loss=1.4483e+00 best_ppl=4.26                                                
Epoch 54 - |param|=3.26e+02 |g_param|=5.51e+05 loss=1.5573e+00 ppl=4.75                                                 
Validation - loss=1.4341e+00 ppl=4.20 best_loss=1.4483e+00 best_ppl=4.26                                                
Epoch 55 - |param|=3.26e+02 |g_param|=7.64e+05 loss=1.4803e+00 ppl=4.39                                                 
Validation - loss=1.3893e+00 ppl=4.01 best_loss=1.4341e+00 best_ppl=4.20                                                
Epoch 56 - |param|=3.26e+02 |g_param|=6.21e+05 loss=1.5070e+00 ppl=4.51                                                 
Validation - loss=1.3684e+00 ppl=3.93 best_loss=1.3893e+00 best_ppl=4.01                                                
Epoch 57 - |param|=3.26e+02 |g_param|=4.38e+05 loss=1.4651e+00 ppl=4.33                                                 
Validation - loss=1.3727e+00 ppl=3.95 best_loss=1.3684e+00 best_ppl=3.93                                                
Epoch 58 - |param|=3.26e+02 |g_param|=8.15e+05 loss=1.4224e+00 ppl=4.15                                                 
Validation - loss=1.3598e+00 ppl=3.90 best_loss=1.3684e+00 best_ppl=3.93                                                
Epoch 59 - |param|=3.26e+02 |g_param|=5.00e+05 loss=1.4158e+00 ppl=4.12                                                 
Validation - loss=1.3566e+00 ppl=3.88 best_loss=1.3598e+00 best_ppl=3.90                                                
Epoch 60 - |param|=3.26e+02 |g_param|=5.51e+05 loss=1.3778e+00 ppl=3.97                                                 
Validation - loss=1.3218e+00 ppl=3.75 best_loss=1.3566e+00 best_ppl=3.88                                                
Epoch 61 - |param|=3.26e+02 |g_param|=6.39e+05 loss=1.4075e+00 ppl=4.09                                                 
Validation - loss=1.3317e+00 ppl=3.79 best_loss=1.3218e+00 best_ppl=3.75                                                
Epoch 62 - |param|=3.26e+02 |g_param|=1.04e+06 loss=1.4657e+00 ppl=4.33                                                 
Validation - loss=1.2820e+00 ppl=3.60 best_loss=1.3218e+00 best_ppl=3.75                                                
Epoch 63 - |param|=3.26e+02 |g_param|=6.27e+05 loss=1.3913e+00 ppl=4.02                                                 
Validation - loss=1.2810e+00 ppl=3.60 best_loss=1.2820e+00 best_ppl=3.60                                                
Epoch 64 - |param|=3.26e+02 |g_param|=3.93e+05 loss=1.3434e+00 ppl=3.83                                                 
Validation - loss=1.2808e+00 ppl=3.60 best_loss=1.2810e+00 best_ppl=3.60                                                
Epoch 65 - |param|=3.26e+02 |g_param|=4.57e+05 loss=1.4056e+00 ppl=4.08                                                 
Validation - loss=1.3028e+00 ppl=3.68 best_loss=1.2808e+00 best_ppl=3.60                                                
Epoch 66 - |param|=3.26e+02 |g_param|=2.75e+05 loss=1.3750e+00 ppl=3.96                                                 
Validation - loss=1.2458e+00 ppl=3.48 best_loss=1.2808e+00 best_ppl=3.60                                                
Epoch 67 - |param|=3.26e+02 |g_param|=2.42e+05 loss=1.2942e+00 ppl=3.65                                                 
Validation - loss=1.2452e+00 ppl=3.47 best_loss=1.2458e+00 best_ppl=3.48                                                
Epoch 68 - |param|=3.26e+02 |g_param|=2.60e+05 loss=1.3091e+00 ppl=3.70                                                 
Validation - loss=1.2328e+00 ppl=3.43 best_loss=1.2452e+00 best_ppl=3.47                                                
Epoch 69 - |param|=3.26e+02 |g_param|=4.64e+05 loss=1.3446e+00 ppl=3.84                                                 
Validation - loss=1.2694e+00 ppl=3.56 best_loss=1.2328e+00 best_ppl=3.43                                                
Epoch 70 - |param|=3.26e+02 |g_param|=3.28e+05 loss=1.3417e+00 ppl=3.83                                                 
Validation - loss=1.2034e+00 ppl=3.33 best_loss=1.2328e+00 best_ppl=3.43                                                
Epoch 71 - |param|=3.26e+02 |g_param|=3.20e+05 loss=1.2820e+00 ppl=3.60                                                 
Validation - loss=1.1941e+00 ppl=3.30 best_loss=1.2034e+00 best_ppl=3.33                                                
Epoch 72 - |param|=3.26e+02 |g_param|=3.22e+05 loss=1.2767e+00 ppl=3.58                                                 
Validation - loss=1.1928e+00 ppl=3.30 best_loss=1.1941e+00 best_ppl=3.30                                                
Epoch 73 - |param|=3.26e+02 |g_param|=3.75e+05 loss=1.3009e+00 ppl=3.67                                                 
Validation - loss=1.2165e+00 ppl=3.38 best_loss=1.1928e+00 best_ppl=3.30                                                
Epoch 74 - |param|=3.26e+02 |g_param|=2.98e+05 loss=1.2683e+00 ppl=3.55                                                 
Validation - loss=1.1910e+00 ppl=3.29 best_loss=1.1928e+00 best_ppl=3.30                                                
Epoch 75 - |param|=3.26e+02 |g_param|=3.29e+05 loss=1.2744e+00 ppl=3.58                                                 
Validation - loss=1.1808e+00 ppl=3.26 best_loss=1.1910e+00 best_ppl=3.29                                                
Epoch 76 - |param|=3.26e+02 |g_param|=4.24e+05 loss=1.2302e+00 ppl=3.42                                                 
Validation - loss=1.1475e+00 ppl=3.15 best_loss=1.1808e+00 best_ppl=3.26                                                
Epoch 77 - |param|=3.26e+02 |g_param|=2.58e+05 loss=1.2477e+00 ppl=3.48                                                 
Validation - loss=1.1644e+00 ppl=3.20 best_loss=1.1475e+00 best_ppl=3.15                                                
Epoch 78 - |param|=3.26e+02 |g_param|=4.60e+05 loss=1.1876e+00 ppl=3.28                                                 
Validation - loss=1.1289e+00 ppl=3.09 best_loss=1.1475e+00 best_ppl=3.15                                                
Epoch 79 - |param|=3.26e+02 |g_param|=4.67e+05 loss=1.2618e+00 ppl=3.53                                                 
Validation - loss=1.1345e+00 ppl=3.11 best_loss=1.1289e+00 best_ppl=3.09                                                
Epoch 80 - |param|=3.27e+02 |g_param|=4.79e+05 loss=1.2017e+00 ppl=3.33                                                 
Validation - loss=1.1208e+00 ppl=3.07 best_loss=1.1289e+00 best_ppl=3.09                                                
Epoch 81 - |param|=3.27e+02 |g_param|=4.15e+05 loss=1.2190e+00 ppl=3.38                                                 
Validation - loss=1.1649e+00 ppl=3.21 best_loss=1.1208e+00 best_ppl=3.07                                                
Epoch 82 - |param|=3.27e+02 |g_param|=4.35e+05 loss=1.2056e+00 ppl=3.34                                                 
Validation - loss=1.1250e+00 ppl=3.08 best_loss=1.1208e+00 best_ppl=3.07                                                
Epoch 83 - |param|=3.27e+02 |g_param|=4.66e+05 loss=1.2010e+00 ppl=3.32                                                 
Validation - loss=1.0915e+00 ppl=2.98 best_loss=1.1208e+00 best_ppl=3.07                                                
Epoch 84 - |param|=3.27e+02 |g_param|=2.87e+05 loss=1.2561e+00 ppl=3.51                                                 
Validation - loss=1.0835e+00 ppl=2.95 best_loss=1.0915e+00 best_ppl=2.98                                                
Epoch 85 - |param|=3.27e+02 |g_param|=3.15e+05 loss=1.1824e+00 ppl=3.26                                                 
Validation - loss=1.0870e+00 ppl=2.97 best_loss=1.0835e+00 best_ppl=2.95                                                
Epoch 86 - |param|=3.27e+02 |g_param|=3.46e+05 loss=1.1675e+00 ppl=3.21                                                 
Validation - loss=1.0801e+00 ppl=2.95 best_loss=1.0835e+00 best_ppl=2.95                                                
Epoch 87 - |param|=3.27e+02 |g_param|=4.92e+05 loss=1.1467e+00 ppl=3.15                                                 
Validation - loss=1.1146e+00 ppl=3.05 best_loss=1.0801e+00 best_ppl=2.95                                                
Epoch 88 - |param|=3.27e+02 |g_param|=3.55e+05 loss=1.1584e+00 ppl=3.18                                                 
Validation - loss=1.0572e+00 ppl=2.88 best_loss=1.0801e+00 best_ppl=2.95                                                
Epoch 89 - |param|=3.27e+02 |g_param|=2.32e+05 loss=1.1680e+00 ppl=3.22                                                 
Validation - loss=1.0686e+00 ppl=2.91 best_loss=1.0572e+00 best_ppl=2.88                                                
Epoch 90 - |param|=3.27e+02 |g_param|=4.63e+05 loss=1.0882e+00 ppl=2.97                                                 
Validation - loss=1.0528e+00 ppl=2.87 best_loss=1.0572e+00 best_ppl=2.88                                                
Epoch 91 - |param|=3.27e+02 |g_param|=3.69e+05 loss=1.1174e+00 ppl=3.06                                                 
Validation - loss=1.0460e+00 ppl=2.85 best_loss=1.0528e+00 best_ppl=2.87                                                
Epoch 92 - |param|=3.27e+02 |g_param|=4.36e+05 loss=1.0869e+00 ppl=2.96                                                 
Validation - loss=1.0384e+00 ppl=2.82 best_loss=1.0460e+00 best_ppl=2.85                                                
Epoch 93 - |param|=3.27e+02 |g_param|=3.95e+05 loss=1.0841e+00 ppl=2.96                                                 
Validation - loss=1.0333e+00 ppl=2.81 best_loss=1.0384e+00 best_ppl=2.82                                                
Epoch 94 - |param|=3.27e+02 |g_param|=2.62e+05 loss=1.0990e+00 ppl=3.00                                                 
Validation - loss=1.0261e+00 ppl=2.79 best_loss=1.0333e+00 best_ppl=2.81                                                
Epoch 95 - |param|=3.27e+02 |g_param|=3.99e+05 loss=1.0876e+00 ppl=2.97                                                 
Validation - loss=1.0445e+00 ppl=2.84 best_loss=1.0261e+00 best_ppl=2.79                                                
Epoch 96 - |param|=3.27e+02 |g_param|=4.82e+05 loss=1.1642e+00 ppl=3.20                                                 
Validation - loss=1.0271e+00 ppl=2.79 best_loss=1.0261e+00 best_ppl=2.79                                                
Epoch 97 - |param|=3.27e+02 |g_param|=4.71e+05 loss=1.0991e+00 ppl=3.00                                                 
Validation - loss=1.0378e+00 ppl=2.82 best_loss=1.0261e+00 best_ppl=2.79                                                
Epoch 98 - |param|=3.27e+02 |g_param|=3.88e+05 loss=1.1212e+00 ppl=3.07                                                 
Validation - loss=1.0186e+00 ppl=2.77 best_loss=1.0261e+00 best_ppl=2.79                                                
Epoch 99 - |param|=3.27e+02 |g_param|=3.65e+05 loss=1.0678e+00 ppl=2.91                                                 
Validation - loss=9.9605e-01 ppl=2.71 best_loss=1.0186e+00 best_ppl=2.77                                                
Epoch 100 - |param|=3.27e+02 |g_param|=6.60e+05 loss=1.1027e+00 ppl=3.01                                                
Validation - loss=1.0276e+00 ppl=2.79 best_loss=9.9605e-01 best_ppl=2.71                                                

real	27m54.964s
user	27m49.018s
sys	0m5.292s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/validation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.100.1.10-3.01.1.03-2.79.pth
BLEU = 54.79, 77.0/61.8/49.1/38.6 (BP=1.000, ratio=1.076, hyp_len=24919, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.47.1.69-5.41.1.56-4.76.pth
BLEU = 39.60, 68.4/47.8/33.2/22.7 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.48.1.60-4.97.1.52-4.59.pth
BLEU = 42.49, 70.7/50.4/35.9/25.5 (BP=1.000, ratio=1.017, hyp_len=23543, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.49.1.68-5.39.1.55-4.70.pth
BLEU = 37.68, 64.1/45.2/31.8/21.9 (BP=1.000, ratio=1.141, hyp_len=26428, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.50.1.65-5.21.1.49-4.43.pth
BLEU = 41.89, 69.9/49.9/35.5/24.9 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.51.1.59-4.88.1.47-4.33.pth
BLEU = 41.52, 68.6/49.3/35.3/24.9 (BP=1.000, ratio=1.074, hyp_len=24866, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.52.1.58-4.84.1.45-4.26.pth
BLEU = 43.22, 70.4/50.9/36.9/26.4 (BP=1.000, ratio=1.046, hyp_len=24232, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.53.1.55-4.73.1.50-4.48.pth
BLEU = 39.77, 66.5/47.7/33.8/23.4 (BP=1.000, ratio=1.124, hyp_len=26039, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.54.1.56-4.75.1.43-4.20.pth
BLEU = 42.56, 69.5/50.5/36.4/25.7 (BP=1.000, ratio=1.072, hyp_len=24833, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.55.1.48-4.39.1.39-4.01.pth
BLEU = 46.30, 73.3/53.8/39.8/29.3 (BP=1.000, ratio=1.012, hyp_len=23429, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.56.1.51-4.51.1.37-3.93.pth
BLEU = 46.15, 72.2/53.4/39.7/29.6 (BP=1.000, ratio=1.038, hyp_len=24032, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.57.1.47-4.33.1.37-3.95.pth
BLEU = 45.99, 72.5/53.7/39.6/29.0 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.58.1.42-4.15.1.36-3.90.pth
BLEU = 45.65, 71.9/53.4/39.4/28.7 (BP=1.000, ratio=1.055, hyp_len=24438, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.59.1.42-4.12.1.36-3.88.pth
BLEU = 45.67, 72.1/53.5/39.5/28.6 (BP=1.000, ratio=1.050, hyp_len=24318, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.60.1.38-3.97.1.32-3.75.pth
BLEU = 47.17, 73.1/54.7/40.9/30.3 (BP=1.000, ratio=1.045, hyp_len=24194, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.61.1.41-4.09.1.33-3.79.pth
BLEU = 45.37, 71.2/53.2/39.3/28.4 (BP=1.000, ratio=1.080, hyp_len=25022, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.62.1.47-4.33.1.28-3.60.pth
BLEU = 49.56, 75.1/56.8/43.1/32.8 (BP=1.000, ratio=1.023, hyp_len=23686, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.63.1.39-4.02.1.28-3.60.pth
BLEU = 47.96, 72.9/55.1/41.7/31.5 (BP=1.000, ratio=1.063, hyp_len=24622, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.64.1.34-3.83.1.28-3.60.pth
BLEU = 48.62, 74.3/56.1/42.3/31.7 (BP=1.000, ratio=1.039, hyp_len=24052, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.65.1.41-4.08.1.30-3.68.pth
BLEU = 46.37, 71.8/54.2/40.4/29.5 (BP=1.000, ratio=1.083, hyp_len=25089, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.66.1.37-3.96.1.25-3.48.pth
BLEU = 49.23, 74.3/56.4/43.0/32.6 (BP=1.000, ratio=1.044, hyp_len=24176, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.67.1.29-3.65.1.25-3.47.pth
BLEU = 47.54, 72.2/54.9/41.5/31.0 (BP=1.000, ratio=1.084, hyp_len=25110, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.68.1.31-3.70.1.23-3.43.pth
BLEU = 50.30, 75.6/57.9/44.1/33.2 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.69.1.34-3.84.1.27-3.56.pth
BLEU = 44.72, 69.0/52.2/39.0/28.5 (BP=1.000, ratio=1.145, hyp_len=26516, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.70.1.34-3.83.1.20-3.33.pth
BLEU = 49.76, 74.0/56.8/43.7/33.3 (BP=1.000, ratio=1.062, hyp_len=24586, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.71.1.28-3.60.1.19-3.30.pth
BLEU = 50.69, 75.3/58.2/44.6/33.8 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.72.1.28-3.58.1.19-3.30.pth
BLEU = 50.42, 74.8/57.8/44.4/33.7 (BP=1.000, ratio=1.060, hyp_len=24552, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.73.1.30-3.67.1.22-3.38.pth
BLEU = 49.67, 74.7/57.5/43.7/32.4 (BP=1.000, ratio=1.064, hyp_len=24648, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.74.1.27-3.55.1.19-3.29.pth
BLEU = 50.36, 74.9/57.9/44.4/33.4 (BP=1.000, ratio=1.062, hyp_len=24603, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.75.1.27-3.58.1.18-3.26.pth
BLEU = 50.53, 75.0/58.2/44.6/33.5 (BP=1.000, ratio=1.065, hyp_len=24656, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.76.1.23-3.42.1.15-3.15.pth
BLEU = 53.24, 77.4/60.2/47.0/36.7 (BP=1.000, ratio=1.027, hyp_len=23785, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.77.1.25-3.48.1.16-3.20.pth
BLEU = 51.12, 75.5/58.6/45.1/34.2 (BP=1.000, ratio=1.057, hyp_len=24486, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.78.1.19-3.28.1.13-3.09.pth
BLEU = 52.91, 76.5/59.9/46.9/36.4 (BP=1.000, ratio=1.048, hyp_len=24270, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.79.1.26-3.53.1.13-3.11.pth
BLEU = 52.69, 76.6/60.1/46.7/35.8 (BP=1.000, ratio=1.048, hyp_len=24263, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.80.1.20-3.33.1.12-3.07.pth
BLEU = 54.52, 77.7/61.3/48.5/38.2 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.81.1.22-3.38.1.16-3.21.pth
BLEU = 50.10, 74.2/57.8/44.3/33.1 (BP=1.000, ratio=1.090, hyp_len=25238, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.82.1.21-3.34.1.13-3.08.pth
BLEU = 53.56, 77.4/60.9/47.6/36.6 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.83.1.20-3.32.1.09-2.98.pth
BLEU = 56.01, 79.1/62.8/50.0/39.7 (BP=1.000, ratio=1.014, hyp_len=23495, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.84.1.26-3.51.1.08-2.95.pth
BLEU = 54.58, 77.4/61.2/48.6/38.5 (BP=1.000, ratio=1.043, hyp_len=24164, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.85.1.18-3.26.1.09-2.97.pth
BLEU = 53.40, 76.8/60.6/47.5/36.7 (BP=1.000, ratio=1.059, hyp_len=24531, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.86.1.17-3.21.1.08-2.95.pth
BLEU = 56.09, 79.2/62.7/50.0/39.8 (BP=1.000, ratio=1.018, hyp_len=23573, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.87.1.15-3.15.1.11-3.05.pth
BLEU = 52.82, 76.6/60.4/47.0/35.8 (BP=1.000, ratio=1.062, hyp_len=24592, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.88.1.16-3.18.1.06-2.88.pth
BLEU = 56.79, 79.3/63.4/50.8/40.7 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.89.1.17-3.22.1.07-2.91.pth
BLEU = 53.82, 76.4/60.7/48.0/37.7 (BP=1.000, ratio=1.067, hyp_len=24710, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.90.1.09-2.97.1.05-2.87.pth
BLEU = 55.77, 78.8/62.7/49.8/39.3 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.91.1.12-3.06.1.05-2.85.pth
BLEU = 55.40, 78.3/62.3/49.5/39.0 (BP=1.000, ratio=1.045, hyp_len=24208, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.92.1.09-2.96.1.04-2.82.pth
BLEU = 56.62, 78.7/63.1/50.7/40.8 (BP=1.000, ratio=1.037, hyp_len=24011, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.93.1.08-2.96.1.03-2.81.pth
BLEU = 56.10, 78.7/63.0/50.3/39.7 (BP=1.000, ratio=1.041, hyp_len=24099, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.94.1.10-3.00.1.03-2.79.pth
BLEU = 55.84, 78.1/62.5/50.0/39.9 (BP=1.000, ratio=1.048, hyp_len=24280, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.95.1.09-2.97.1.04-2.84.pth
BLEU = 54.72, 77.3/61.8/49.0/38.3 (BP=1.000, ratio=1.066, hyp_len=24677, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.96.1.16-3.20.1.03-2.79.pth
BLEU = 55.59, 78.1/62.7/49.8/39.2 (BP=1.000, ratio=1.054, hyp_len=24413, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.97.1.10-3.00.1.04-2.82.pth
BLEU = 55.45, 78.1/62.5/49.7/39.0 (BP=1.000, ratio=1.051, hyp_len=24346, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.98.1.12-3.07.1.02-2.77.pth
BLEU = 54.99, 77.3/61.9/49.2/38.8 (BP=1.000, ratio=1.070, hyp_len=24774, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.99.1.07-2.91.1.00-2.71.pth
BLEU = 56.77, 78.8/63.5/51.0/40.7 (BP=1.000, ratio=1.043, hyp_len=24167, ref_len=23160)

real	30m32.871s
user	29m57.441s
sys	1m9.361s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-50epoch$
```

Baseline က BLEU = 40.85
RL my-rk, 50-50 model ရဲ့ best score က ...  

```
Evaluation result for the model: transformer-rl-myrk.88.1.16-3.18.1.06-2.88.pth
BLEU = 56.79, 79.3/63.4/50.8/40.7 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
```

### RL, my-rk, 60-40 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-60epoch/myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth --model_fn ./model/rl/transformer/myrk-60epoch/transformer-rl-myrk.pth --init_epoch 59 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/myrk-60epoch/myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/myrk-60epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 59
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 59,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/baseline/myrk-60epoch/myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/myrk-60epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 59 - |param|=3.26e+02 |g_param|=5.27e+05 loss=1.5095e+00 ppl=4.52                                                 
Validation - loss=1.3173e+00 ppl=3.73 best_loss=inf best_ppl=inf                                                        
Epoch 60 - |param|=3.26e+02 |g_param|=7.01e+05 loss=1.4564e+00 ppl=4.29                                                 
Validation - loss=1.2969e+00 ppl=3.66 best_loss=1.3173e+00 best_ppl=3.73                                                
Epoch 61 - |param|=3.26e+02 |g_param|=9.23e+05 loss=1.3993e+00 ppl=4.05                                                 
Validation - loss=1.3701e+00 ppl=3.94 best_loss=1.2969e+00 best_ppl=3.66                                                
Epoch 62 - |param|=3.26e+02 |g_param|=7.03e+05 loss=1.3909e+00 ppl=4.02                                                 
Validation - loss=1.2878e+00 ppl=3.62 best_loss=1.2969e+00 best_ppl=3.66                                                
Epoch 63 - |param|=3.26e+02 |g_param|=5.62e+05 loss=1.4537e+00 ppl=4.28                                                 
Validation - loss=1.2717e+00 ppl=3.57 best_loss=1.2878e+00 best_ppl=3.62                                                
Epoch 64 - |param|=3.26e+02 |g_param|=5.91e+05 loss=1.3813e+00 ppl=3.98                                                 
Validation - loss=1.2648e+00 ppl=3.54 best_loss=1.2717e+00 best_ppl=3.57                                                
Epoch 65 - |param|=3.26e+02 |g_param|=6.23e+05 loss=1.3427e+00 ppl=3.83                                                 
Validation - loss=1.2392e+00 ppl=3.45 best_loss=1.2648e+00 best_ppl=3.54                                                
Epoch 66 - |param|=3.26e+02 |g_param|=1.10e+06 loss=1.4320e+00 ppl=4.19                                                 
Validation - loss=1.2694e+00 ppl=3.56 best_loss=1.2392e+00 best_ppl=3.45                                                
Epoch 67 - |param|=3.26e+02 |g_param|=4.81e+05 loss=1.3085e+00 ppl=3.70                                                 
Validation - loss=1.2167e+00 ppl=3.38 best_loss=1.2392e+00 best_ppl=3.45                                                
Epoch 68 - |param|=3.26e+02 |g_param|=6.88e+05 loss=1.3746e+00 ppl=3.95                                                 
Validation - loss=1.2059e+00 ppl=3.34 best_loss=1.2167e+00 best_ppl=3.38                                                
Epoch 69 - |param|=3.26e+02 |g_param|=6.57e+05 loss=1.3128e+00 ppl=3.72                                                 
Validation - loss=1.1955e+00 ppl=3.31 best_loss=1.2059e+00 best_ppl=3.34                                                
Epoch 70 - |param|=3.26e+02 |g_param|=9.83e+05 loss=1.3456e+00 ppl=3.84                                                 
Validation - loss=1.1854e+00 ppl=3.27 best_loss=1.1955e+00 best_ppl=3.31                                                
Epoch 71 - |param|=3.26e+02 |g_param|=8.08e+05 loss=1.2667e+00 ppl=3.55                                                 
Validation - loss=1.1728e+00 ppl=3.23 best_loss=1.1854e+00 best_ppl=3.27                                                
Epoch 72 - |param|=3.26e+02 |g_param|=9.08e+05 loss=1.3257e+00 ppl=3.76                                                 
Validation - loss=1.1660e+00 ppl=3.21 best_loss=1.1728e+00 best_ppl=3.23                                                
Epoch 73 - |param|=3.26e+02 |g_param|=6.77e+05 loss=1.3339e+00 ppl=3.80                                                 
Validation - loss=1.1808e+00 ppl=3.26 best_loss=1.1660e+00 best_ppl=3.21                                                
Epoch 74 - |param|=3.26e+02 |g_param|=6.15e+05 loss=1.2496e+00 ppl=3.49                                                 
Validation - loss=1.1627e+00 ppl=3.20 best_loss=1.1660e+00 best_ppl=3.21                                                
Epoch 75 - |param|=3.26e+02 |g_param|=7.94e+05 loss=1.2530e+00 ppl=3.50                                                 
Validation - loss=1.1473e+00 ppl=3.15 best_loss=1.1627e+00 best_ppl=3.20                                                
Epoch 76 - |param|=3.26e+02 |g_param|=1.42e+06 loss=1.3345e+00 ppl=3.80                                                 
Validation - loss=1.1409e+00 ppl=3.13 best_loss=1.1473e+00 best_ppl=3.15                                                
Epoch 77 - |param|=3.26e+02 |g_param|=5.77e+05 loss=1.2609e+00 ppl=3.53                                                 
Validation - loss=1.1334e+00 ppl=3.11 best_loss=1.1409e+00 best_ppl=3.13                                                
Epoch 78 - |param|=3.26e+02 |g_param|=6.25e+05 loss=1.2326e+00 ppl=3.43                                                 
Validation - loss=1.1145e+00 ppl=3.05 best_loss=1.1334e+00 best_ppl=3.11                                                
Epoch 79 - |param|=3.26e+02 |g_param|=8.03e+05 loss=1.2315e+00 ppl=3.43                                                 
Validation - loss=1.1135e+00 ppl=3.05 best_loss=1.1145e+00 best_ppl=3.05                                                
Epoch 80 - |param|=3.26e+02 |g_param|=1.06e+06 loss=1.1850e+00 ppl=3.27                                                 
Validation - loss=1.1030e+00 ppl=3.01 best_loss=1.1135e+00 best_ppl=3.05                                                
Epoch 81 - |param|=3.26e+02 |g_param|=6.32e+05 loss=1.1867e+00 ppl=3.28                                                 
Validation - loss=1.0946e+00 ppl=2.99 best_loss=1.1030e+00 best_ppl=3.01                                                
Epoch 82 - |param|=3.26e+02 |g_param|=9.14e+05 loss=1.2731e+00 ppl=3.57                                                 
Validation - loss=1.1024e+00 ppl=3.01 best_loss=1.0946e+00 best_ppl=2.99                                                
Epoch 83 - |param|=3.26e+02 |g_param|=4.47e+05 loss=1.2246e+00 ppl=3.40                                                 
Validation - loss=1.0898e+00 ppl=2.97 best_loss=1.0946e+00 best_ppl=2.99                                                
Epoch 84 - |param|=3.26e+02 |g_param|=3.22e+05 loss=1.1394e+00 ppl=3.12                                                 
Validation - loss=1.0810e+00 ppl=2.95 best_loss=1.0898e+00 best_ppl=2.97                                                
Epoch 85 - |param|=3.26e+02 |g_param|=3.40e+05 loss=1.1918e+00 ppl=3.29                                                 
Validation - loss=1.0768e+00 ppl=2.94 best_loss=1.0810e+00 best_ppl=2.95                                                
Epoch 86 - |param|=3.26e+02 |g_param|=3.27e+05 loss=1.1351e+00 ppl=3.11                                                 
Validation - loss=1.0701e+00 ppl=2.92 best_loss=1.0768e+00 best_ppl=2.94                                                
Epoch 87 - |param|=3.27e+02 |g_param|=3.80e+05 loss=1.1733e+00 ppl=3.23                                                 
Validation - loss=1.0740e+00 ppl=2.93 best_loss=1.0701e+00 best_ppl=2.92                                                
Epoch 88 - |param|=3.27e+02 |g_param|=3.25e+05 loss=1.1512e+00 ppl=3.16                                                 
Validation - loss=1.0525e+00 ppl=2.86 best_loss=1.0701e+00 best_ppl=2.92                                                
Epoch 89 - |param|=3.27e+02 |g_param|=3.72e+05 loss=1.1058e+00 ppl=3.02                                                 
Validation - loss=1.0727e+00 ppl=2.92 best_loss=1.0525e+00 best_ppl=2.86                                                
Epoch 90 - |param|=3.27e+02 |g_param|=2.83e+05 loss=1.1137e+00 ppl=3.05                                                 
Validation - loss=1.0462e+00 ppl=2.85 best_loss=1.0525e+00 best_ppl=2.86                                                
Epoch 91 - |param|=3.27e+02 |g_param|=3.14e+05 loss=1.0981e+00 ppl=3.00                                                 
Validation - loss=1.0461e+00 ppl=2.85 best_loss=1.0462e+00 best_ppl=2.85                                                
Epoch 92 - |param|=3.27e+02 |g_param|=4.09e+05 loss=1.1180e+00 ppl=3.06                                                 
Validation - loss=1.0327e+00 ppl=2.81 best_loss=1.0461e+00 best_ppl=2.85                                                
Epoch 93 - |param|=3.27e+02 |g_param|=4.28e+05 loss=1.1605e+00 ppl=3.19                                                 
Validation - loss=1.0262e+00 ppl=2.79 best_loss=1.0327e+00 best_ppl=2.81                                                
Epoch 94 - |param|=3.27e+02 |g_param|=4.32e+05 loss=1.0669e+00 ppl=2.91                                                 
Validation - loss=1.0194e+00 ppl=2.77 best_loss=1.0262e+00 best_ppl=2.79                                                
Epoch 95 - |param|=3.27e+02 |g_param|=5.40e+05 loss=1.1672e+00 ppl=3.21                                                 
Validation - loss=1.0207e+00 ppl=2.78 best_loss=1.0194e+00 best_ppl=2.77                                                
Epoch 96 - |param|=3.27e+02 |g_param|=3.31e+05 loss=1.1032e+00 ppl=3.01                                                 
Validation - loss=1.0234e+00 ppl=2.78 best_loss=1.0194e+00 best_ppl=2.77                                                
Epoch 97 - |param|=3.27e+02 |g_param|=5.37e+05 loss=1.0864e+00 ppl=2.96                                                 
Validation - loss=1.0059e+00 ppl=2.73 best_loss=1.0194e+00 best_ppl=2.77                                                
Epoch 98 - |param|=3.27e+02 |g_param|=3.00e+05 loss=1.1241e+00 ppl=3.08                                                 
Validation - loss=9.9930e-01 ppl=2.72 best_loss=1.0059e+00 best_ppl=2.73                                                
Epoch 99 - |param|=3.27e+02 |g_param|=5.93e+05 loss=1.0475e+00 ppl=2.85                                                 
Validation - loss=1.0401e+00 ppl=2.83 best_loss=9.9930e-01 best_ppl=2.72                                                
Epoch 100 - |param|=3.27e+02 |g_param|=5.30e+05 loss=1.0657e+00 ppl=2.90                                                
Validation - loss=1.0618e+00 ppl=2.89 best_loss=9.9930e-01 best_ppl=2.72                                                

real	22m0.645s
user	21m55.181s
sys	0m4.731s
(simple-nmt) ye@:~/exp/simple-nmt
```

testing/validation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.59.1.51-4.52.1.32-3.73.pth
BLEU = 47.19, 73.3/54.9/40.9/30.2 (BP=1.000, ratio=1.047, hyp_len=24254, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.60.1.46-4.29.1.30-3.66.pth
BLEU = 49.14, 75.1/56.6/42.7/32.2 (BP=1.000, ratio=1.023, hyp_len=23688, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.61.1.40-4.05.1.37-3.94.pth
BLEU = 43.80, 70.0/52.0/37.8/26.8 (BP=1.000, ratio=1.113, hyp_len=25781, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.62.1.39-4.02.1.29-3.62.pth
BLEU = 47.53, 73.6/55.2/41.2/30.5 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.63.1.45-4.28.1.27-3.57.pth
BLEU = 47.78, 73.9/55.8/41.4/30.5 (BP=1.000, ratio=1.053, hyp_len=24378, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.64.1.38-3.98.1.26-3.54.pth
BLEU = 48.17, 73.8/55.8/41.9/31.2 (BP=1.000, ratio=1.055, hyp_len=24428, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.65.1.34-3.83.1.24-3.45.pth
BLEU = 48.92, 74.0/56.3/42.7/32.2 (BP=1.000, ratio=1.057, hyp_len=24471, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.66.1.43-4.19.1.27-3.56.pth
BLEU = 47.15, 73.0/55.2/41.0/29.9 (BP=1.000, ratio=1.076, hyp_len=24924, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.67.1.31-3.70.1.22-3.38.pth
BLEU = 50.36, 75.4/57.6/44.1/33.6 (BP=1.000, ratio=1.037, hyp_len=24012, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.68.1.37-3.95.1.21-3.34.pth
BLEU = 51.76, 76.6/58.9/45.4/35.0 (BP=1.000, ratio=1.026, hyp_len=23758, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.69.1.31-3.72.1.20-3.31.pth
BLEU = 51.19, 75.8/58.3/44.9/34.6 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.70.1.35-3.84.1.19-3.27.pth
BLEU = 50.91, 75.6/58.3/44.7/34.1 (BP=1.000, ratio=1.045, hyp_len=24197, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.71.1.27-3.55.1.17-3.23.pth
BLEU = 52.09, 76.5/59.2/45.8/35.4 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.72.1.33-3.76.1.17-3.21.pth
BLEU = 51.90, 76.2/58.8/45.7/35.4 (BP=1.000, ratio=1.039, hyp_len=24058, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.73.1.33-3.80.1.18-3.26.pth
BLEU = 50.69, 75.4/58.1/44.5/33.8 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.74.1.25-3.49.1.16-3.20.pth
BLEU = 50.96, 75.2/58.2/44.9/34.3 (BP=1.000, ratio=1.061, hyp_len=24574, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.75.1.25-3.50.1.15-3.15.pth
BLEU = 52.56, 76.8/59.7/46.4/35.8 (BP=1.000, ratio=1.038, hyp_len=24031, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.76.1.33-3.80.1.14-3.13.pth
BLEU = 53.61, 77.5/60.5/47.4/37.1 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.77.1.26-3.53.1.13-3.11.pth
BLEU = 52.39, 76.5/59.5/46.3/35.8 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.78.1.23-3.43.1.11-3.05.pth
BLEU = 54.01, 77.7/61.0/47.9/37.5 (BP=1.000, ratio=1.031, hyp_len=23871, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.79.1.23-3.43.1.11-3.05.pth
BLEU = 54.77, 78.1/61.4/48.7/38.5 (BP=1.000, ratio=1.028, hyp_len=23804, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.80.1.19-3.27.1.10-3.01.pth
BLEU = 54.71, 78.3/61.6/48.6/38.2 (BP=1.000, ratio=1.024, hyp_len=23717, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.81.1.19-3.28.1.09-2.99.pth
BLEU = 54.29, 77.6/61.1/48.3/37.9 (BP=1.000, ratio=1.039, hyp_len=24063, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.82.1.27-3.57.1.10-3.01.pth
BLEU = 52.73, 76.6/60.1/46.7/35.9 (BP=1.000, ratio=1.055, hyp_len=24438, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.83.1.22-3.40.1.09-2.97.pth
BLEU = 54.50, 78.0/61.6/48.4/37.9 (BP=1.000, ratio=1.032, hyp_len=23900, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.84.1.14-3.12.1.08-2.95.pth
BLEU = 54.30, 77.8/61.3/48.3/37.8 (BP=1.000, ratio=1.040, hyp_len=24082, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.85.1.19-3.29.1.08-2.94.pth
BLEU = 54.34, 77.7/61.5/48.4/37.8 (BP=1.000, ratio=1.046, hyp_len=24231, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.86.1.14-3.11.1.07-2.92.pth
BLEU = 54.76, 78.0/61.8/48.8/38.2 (BP=1.000, ratio=1.041, hyp_len=24118, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.87.1.17-3.23.1.07-2.93.pth
BLEU = 53.40, 76.7/60.7/47.6/36.7 (BP=1.000, ratio=1.059, hyp_len=24529, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.88.1.15-3.16.1.05-2.86.pth
BLEU = 55.19, 77.8/61.9/49.3/39.1 (BP=1.000, ratio=1.046, hyp_len=24229, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.89.1.11-3.02.1.07-2.92.pth
BLEU = 54.44, 77.9/61.8/48.6/37.6 (BP=1.000, ratio=1.049, hyp_len=24295, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.90.1.11-3.05.1.05-2.85.pth
BLEU = 55.75, 78.6/62.7/49.8/39.3 (BP=1.000, ratio=1.038, hyp_len=24040, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.91.1.10-3.00.1.05-2.85.pth
BLEU = 54.37, 76.8/61.1/48.6/38.3 (BP=1.000, ratio=1.066, hyp_len=24684, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.92.1.12-3.06.1.03-2.81.pth
BLEU = 57.72, 80.1/64.2/51.7/41.7 (BP=1.000, ratio=1.019, hyp_len=23599, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.93.1.16-3.19.1.03-2.79.pth
BLEU = 57.43, 79.5/63.9/51.5/41.6 (BP=1.000, ratio=1.025, hyp_len=23736, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.94.1.07-2.91.1.02-2.77.pth
BLEU = 56.53, 78.9/63.3/50.7/40.4 (BP=1.000, ratio=1.038, hyp_len=24048, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.95.1.17-3.21.1.02-2.78.pth
BLEU = 57.71, 79.9/64.2/51.8/41.8 (BP=1.000, ratio=1.024, hyp_len=23725, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.96.1.10-3.01.1.02-2.78.pth
BLEU = 55.57, 78.0/62.6/49.8/39.2 (BP=1.000, ratio=1.059, hyp_len=24515, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.97.1.09-2.96.1.01-2.73.pth
BLEU = 58.22, 80.2/64.7/52.3/42.4 (BP=1.000, ratio=1.022, hyp_len=23667, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.98.1.12-3.08.1.00-2.72.pth
BLEU = 56.81, 79.1/63.6/51.0/40.6 (BP=1.000, ratio=1.042, hyp_len=24135, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.99.1.05-2.85.1.04-2.83.pth
BLEU = 54.51, 77.1/61.7/48.7/38.0 (BP=1.000, ratio=1.073, hyp_len=24856, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.100.1.07-2.90.1.06-2.89.pth
BLEU = 53.82, 76.1/61.0/48.2/37.5 (BP=1.000, ratio=1.097, hyp_len=25397, ref_len=23160)

real	23m0.084s
user	22m31.242s
sys	0m53.873s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-60epoch$
```

Baseline က BLEU = 47.13  
RL, my-rk, 60-40 model ရဲ့ အကောင်းဆုံး best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-rl-myrk.97.1.09-2.96.1.01-2.73.pth
BLEU = 58.22, 80.2/64.7/52.3/42.4 (BP=1.000, ratio=1.022, hyp_len=23667, ref_len=23160)
```

### RL, my-rk, 70-30 model

training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-70epoch/myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth --model_fn ./model/rl/transformer/myrk-70epoch/transformer-rl-myrk.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/myrk-70epoch/myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/myrk-70epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 70
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 70,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/baseline/myrk-70epoch/myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/myrk-70epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1539, 32)
  (emb_dec): Embedding(1642, 32)
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
    (1): Linear(in_features=32, out_features=1642, bias=True)
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
Epoch 70 - |param|=3.26e+02 |g_param|=6.19e+05 loss=1.3222e+00 ppl=3.75                                                 
Validation - loss=1.1728e+00 ppl=3.23 best_loss=inf best_ppl=inf                                                        
Epoch 71 - |param|=3.26e+02 |g_param|=9.36e+05 loss=1.3049e+00 ppl=3.69                                                 
Validation - loss=1.1558e+00 ppl=3.18 best_loss=1.1728e+00 best_ppl=3.23                                                
Epoch 72 - |param|=3.26e+02 |g_param|=8.84e+05 loss=1.2616e+00 ppl=3.53                                                 
Validation - loss=1.1700e+00 ppl=3.22 best_loss=1.1558e+00 best_ppl=3.18                                                
Epoch 73 - |param|=3.26e+02 |g_param|=7.56e+05 loss=1.2691e+00 ppl=3.56                                                 
Validation - loss=1.1371e+00 ppl=3.12 best_loss=1.1558e+00 best_ppl=3.18                                                
Epoch 74 - |param|=3.26e+02 |g_param|=7.62e+05 loss=1.2507e+00 ppl=3.49                                                 
Validation - loss=1.1371e+00 ppl=3.12 best_loss=1.1371e+00 best_ppl=3.12                                                
Epoch 75 - |param|=3.26e+02 |g_param|=7.03e+05 loss=1.2319e+00 ppl=3.43                                                 
Validation - loss=1.1231e+00 ppl=3.07 best_loss=1.1371e+00 best_ppl=3.12                                                
Epoch 76 - |param|=3.26e+02 |g_param|=6.96e+05 loss=1.1867e+00 ppl=3.28                                                 
Validation - loss=1.1262e+00 ppl=3.08 best_loss=1.1231e+00 best_ppl=3.07                                                
Epoch 77 - |param|=3.26e+02 |g_param|=9.45e+05 loss=1.2617e+00 ppl=3.53                                                 
Validation - loss=1.1123e+00 ppl=3.04 best_loss=1.1231e+00 best_ppl=3.07                                                
Epoch 78 - |param|=3.26e+02 |g_param|=6.96e+05 loss=1.1987e+00 ppl=3.32                                                 
Validation - loss=1.1190e+00 ppl=3.06 best_loss=1.1123e+00 best_ppl=3.04                                                
Epoch 79 - |param|=3.26e+02 |g_param|=7.87e+05 loss=1.1888e+00 ppl=3.28                                                 
Validation - loss=1.0994e+00 ppl=3.00 best_loss=1.1123e+00 best_ppl=3.04                                                
Epoch 80 - |param|=3.26e+02 |g_param|=7.10e+05 loss=1.1950e+00 ppl=3.30                                                 
Validation - loss=1.0879e+00 ppl=2.97 best_loss=1.0994e+00 best_ppl=3.00                                                
Epoch 81 - |param|=3.26e+02 |g_param|=6.01e+05 loss=1.2600e+00 ppl=3.53                                                 
Validation - loss=1.1027e+00 ppl=3.01 best_loss=1.0879e+00 best_ppl=2.97                                                
Epoch 82 - |param|=3.26e+02 |g_param|=1.04e+06 loss=1.1697e+00 ppl=3.22                                                 
Validation - loss=1.0762e+00 ppl=2.93 best_loss=1.0879e+00 best_ppl=2.97                                                
Epoch 83 - |param|=3.26e+02 |g_param|=7.32e+05 loss=1.1098e+00 ppl=3.03                                                 
Validation - loss=1.0610e+00 ppl=2.89 best_loss=1.0762e+00 best_ppl=2.93                                                
Epoch 84 - |param|=3.26e+02 |g_param|=1.22e+06 loss=1.1571e+00 ppl=3.18                                                 
Validation - loss=1.1240e+00 ppl=3.08 best_loss=1.0610e+00 best_ppl=2.89                                                
Epoch 85 - |param|=3.26e+02 |g_param|=6.90e+05 loss=1.1725e+00 ppl=3.23                                                 
Validation - loss=1.0628e+00 ppl=2.89 best_loss=1.0610e+00 best_ppl=2.89                                                
Epoch 86 - |param|=3.26e+02 |g_param|=9.07e+05 loss=1.1213e+00 ppl=3.07                                                 
Validation - loss=1.0533e+00 ppl=2.87 best_loss=1.0610e+00 best_ppl=2.89                                                
Epoch 87 - |param|=3.26e+02 |g_param|=8.67e+05 loss=1.1646e+00 ppl=3.20                                                 
Validation - loss=1.0418e+00 ppl=2.83 best_loss=1.0533e+00 best_ppl=2.87                                                
Epoch 88 - |param|=3.26e+02 |g_param|=8.15e+05 loss=1.1351e+00 ppl=3.11                                                 
Validation - loss=1.0438e+00 ppl=2.84 best_loss=1.0418e+00 best_ppl=2.83                                                
Epoch 89 - |param|=3.26e+02 |g_param|=8.10e+05 loss=1.1322e+00 ppl=3.10                                                 
Validation - loss=1.0364e+00 ppl=2.82 best_loss=1.0418e+00 best_ppl=2.83                                                
Epoch 90 - |param|=3.26e+02 |g_param|=6.72e+05 loss=1.0728e+00 ppl=2.92                                                 
Validation - loss=1.0448e+00 ppl=2.84 best_loss=1.0364e+00 best_ppl=2.82                                                
Epoch 91 - |param|=3.26e+02 |g_param|=4.15e+05 loss=1.0861e+00 ppl=2.96                                                 
Validation - loss=1.0233e+00 ppl=2.78 best_loss=1.0364e+00 best_ppl=2.82                                                
Epoch 92 - |param|=3.26e+02 |g_param|=3.32e+05 loss=1.0596e+00 ppl=2.89                                                 
Validation - loss=1.0237e+00 ppl=2.78 best_loss=1.0233e+00 best_ppl=2.78                                                
Epoch 93 - |param|=3.26e+02 |g_param|=4.18e+05 loss=1.1142e+00 ppl=3.05                                                 
Validation - loss=1.0115e+00 ppl=2.75 best_loss=1.0233e+00 best_ppl=2.78                                                
Epoch 94 - |param|=3.26e+02 |g_param|=7.39e+05 loss=1.0682e+00 ppl=2.91                                                 
Validation - loss=1.0416e+00 ppl=2.83 best_loss=1.0115e+00 best_ppl=2.75                                                
Epoch 95 - |param|=3.26e+02 |g_param|=4.17e+05 loss=1.0804e+00 ppl=2.95                                                 
Validation - loss=1.0451e+00 ppl=2.84 best_loss=1.0115e+00 best_ppl=2.75                                                
Epoch 96 - |param|=3.27e+02 |g_param|=3.77e+05 loss=1.0215e+00 ppl=2.78                                                 
Validation - loss=1.0005e+00 ppl=2.72 best_loss=1.0115e+00 best_ppl=2.75                                                
Epoch 97 - |param|=3.27e+02 |g_param|=4.83e+05 loss=1.1191e+00 ppl=3.06                                                 
Validation - loss=9.9288e-01 ppl=2.70 best_loss=1.0005e+00 best_ppl=2.72                                                
Epoch 98 - |param|=3.27e+02 |g_param|=4.03e+05 loss=1.0026e+00 ppl=2.73                                                 
Validation - loss=9.9397e-01 ppl=2.70 best_loss=9.9288e-01 best_ppl=2.70                                                
Epoch 99 - |param|=3.27e+02 |g_param|=3.47e+05 loss=1.1003e+00 ppl=3.01                                                 
Validation - loss=9.8220e-01 ppl=2.67 best_loss=9.9288e-01 best_ppl=2.70                                                
Epoch 100 - |param|=3.27e+02 |g_param|=4.43e+05 loss=1.0901e+00 ppl=2.97                                                
Validation - loss=1.0035e+00 ppl=2.73 best_loss=9.8220e-01 best_ppl=2.67                                                

real	16m5.958s
user	16m1.834s
sys	0m3.717s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.70.1.32-3.75.1.17-3.23.pth
BLEU = 51.42, 76.0/58.8/45.2/34.6 (BP=1.000, ratio=1.043, hyp_len=24147, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.71.1.30-3.69.1.16-3.18.pth
BLEU = 51.84, 76.1/59.0/45.6/35.3 (BP=1.000, ratio=1.042, hyp_len=24123, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.72.1.26-3.53.1.17-3.22.pth
BLEU = 50.47, 75.1/58.0/44.4/33.6 (BP=1.000, ratio=1.060, hyp_len=24556, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.73.1.27-3.56.1.14-3.12.pth
BLEU = 53.45, 77.6/60.6/47.2/36.7 (BP=1.000, ratio=1.026, hyp_len=23765, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.74.1.25-3.49.1.14-3.12.pth
BLEU = 52.32, 76.7/59.9/46.2/35.3 (BP=1.000, ratio=1.041, hyp_len=24118, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.75.1.23-3.43.1.12-3.07.pth
BLEU = 52.81, 77.1/60.1/46.6/36.0 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.76.1.19-3.28.1.13-3.08.pth
BLEU = 51.52, 75.7/59.0/45.4/34.7 (BP=1.000, ratio=1.063, hyp_len=24624, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.77.1.26-3.53.1.11-3.04.pth
BLEU = 53.48, 77.3/60.5/47.3/37.0 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.78.1.20-3.32.1.12-3.06.pth
BLEU = 52.34, 76.1/59.6/46.4/35.7 (BP=1.000, ratio=1.057, hyp_len=24471, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.79.1.19-3.28.1.10-3.00.pth
BLEU = 51.53, 74.8/58.4/45.6/35.4 (BP=1.000, ratio=1.080, hyp_len=25007, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.80.1.20-3.30.1.09-2.97.pth
BLEU = 53.47, 76.8/60.4/47.5/37.1 (BP=1.000, ratio=1.048, hyp_len=24280, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.81.1.26-3.53.1.10-3.01.pth
BLEU = 52.39, 75.7/59.8/46.5/35.8 (BP=1.000, ratio=1.072, hyp_len=24833, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.82.1.17-3.22.1.08-2.93.pth
BLEU = 54.73, 78.0/61.5/48.7/38.4 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.83.1.11-3.03.1.06-2.89.pth
BLEU = 54.62, 77.9/61.7/48.6/38.1 (BP=1.000, ratio=1.040, hyp_len=24097, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.84.1.16-3.18.1.12-3.08.pth
BLEU = 51.15, 74.3/58.7/45.5/34.5 (BP=1.000, ratio=1.099, hyp_len=25446, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.85.1.17-3.23.1.06-2.89.pth
BLEU = 53.64, 76.9/60.8/47.7/37.1 (BP=1.000, ratio=1.062, hyp_len=24605, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.86.1.12-3.07.1.05-2.87.pth
BLEU = 54.55, 77.8/61.7/48.6/38.0 (BP=1.000, ratio=1.046, hyp_len=24222, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.87.1.16-3.20.1.04-2.83.pth
BLEU = 55.77, 78.5/62.5/49.8/39.6 (BP=1.000, ratio=1.035, hyp_len=23979, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.88.1.14-3.11.1.04-2.84.pth
BLEU = 54.96, 78.0/62.0/49.1/38.5 (BP=1.000, ratio=1.048, hyp_len=24280, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.89.1.13-3.10.1.04-2.82.pth
BLEU = 55.44, 78.2/62.3/49.5/39.2 (BP=1.000, ratio=1.046, hyp_len=24227, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.90.1.07-2.92.1.04-2.84.pth
BLEU = 54.63, 77.6/61.9/48.8/38.0 (BP=1.000, ratio=1.055, hyp_len=24434, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.91.1.09-2.96.1.02-2.78.pth
BLEU = 57.03, 79.7/63.8/51.0/40.8 (BP=1.000, ratio=1.022, hyp_len=23662, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.92.1.06-2.89.1.02-2.78.pth
BLEU = 54.20, 76.5/61.0/48.4/38.1 (BP=1.000, ratio=1.076, hyp_len=24918, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.93.1.11-3.05.1.01-2.75.pth
BLEU = 58.20, 80.4/64.7/52.2/42.2 (BP=1.000, ratio=1.020, hyp_len=23617, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.94.1.07-2.91.1.04-2.83.pth
BLEU = 53.84, 76.4/61.0/48.1/37.4 (BP=1.000, ratio=1.079, hyp_len=24997, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.95.1.08-2.95.1.05-2.84.pth
BLEU = 53.58, 76.7/61.1/47.8/36.8 (BP=1.000, ratio=1.077, hyp_len=24950, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.96.1.02-2.78.1.00-2.72.pth
BLEU = 56.75, 79.0/63.6/50.9/40.5 (BP=1.000, ratio=1.043, hyp_len=24145, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.97.1.12-3.06.0.99-2.70.pth
BLEU = 57.85, 79.8/64.3/51.9/42.0 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.98.1.00-2.73.0.99-2.70.pth
BLEU = 56.62, 78.9/63.5/50.8/40.4 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.99.1.10-3.01.0.98-2.67.pth
BLEU = 56.97, 79.1/63.8/51.1/40.8 (BP=1.000, ratio=1.043, hyp_len=24165, ref_len=23160)
Evaluation result for the model: transformer-rl-myrk.100.1.09-2.97.1.00-2.73.pth
BLEU = 55.69, 77.9/62.7/50.0/39.4 (BP=1.000, ratio=1.065, hyp_len=24671, ref_len=23160)

real	17m7.984s
user	16m49.102s
sys	0m39.671s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/myrk-70epoch$
```

Baseline က BLEU = 50.51  
RL, my-rk, 70-30 model ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: transformer-rl-myrk.93.1.11-3.05.1.01-2.75.pth
BLEU = 58.20, 80.4/64.7/52.2/42.2 (BP=1.000, ratio=1.020, hyp_len=23617, ref_len=23160)
```

### RL, rk-my, 40-70 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth --model_fn ./model/rl/transformer/rkmy-40epoch/transformer-rl-myrk.pth --init_epoch 39 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/rkmy-40epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 39
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 39,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'load_fn': './model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/rkmy-40epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 39 - |param|=3.26e+02 |g_param|=5.22e+05 loss=1.7810e+00 ppl=5.94                                                 
Validation - loss=1.6876e+00 ppl=5.41 best_loss=inf best_ppl=inf                                                        
Epoch 40 - |param|=3.26e+02 |g_param|=4.29e+05 loss=1.7723e+00 ppl=5.88                                                 
Validation - loss=1.6389e+00 ppl=5.15 best_loss=1.6876e+00 best_ppl=5.41                                                
Epoch 41 - |param|=3.26e+02 |g_param|=4.42e+05 loss=1.7244e+00 ppl=5.61                                                 
Validation - loss=1.6064e+00 ppl=4.98 best_loss=1.6389e+00 best_ppl=5.15                                                
Epoch 42 - |param|=3.26e+02 |g_param|=5.07e+05 loss=1.7250e+00 ppl=5.61                                                 
Validation - loss=1.5793e+00 ppl=4.85 best_loss=1.6064e+00 best_ppl=4.98                                                
Epoch 43 - |param|=3.26e+02 |g_param|=4.68e+05 loss=1.7194e+00 ppl=5.58                                                 
Validation - loss=1.5637e+00 ppl=4.78 best_loss=1.5793e+00 best_ppl=4.85                                                
Epoch 44 - |param|=3.26e+02 |g_param|=3.88e+05 loss=1.6607e+00 ppl=5.26                                                 
Validation - loss=1.5346e+00 ppl=4.64 best_loss=1.5637e+00 best_ppl=4.78                                                
Epoch 45 - |param|=3.26e+02 |g_param|=3.70e+05 loss=1.6330e+00 ppl=5.12                                                 
Validation - loss=1.5167e+00 ppl=4.56 best_loss=1.5346e+00 best_ppl=4.64                                                
Epoch 46 - |param|=3.26e+02 |g_param|=5.09e+05 loss=1.6109e+00 ppl=5.01                                                 
Validation - loss=1.5082e+00 ppl=4.52 best_loss=1.5167e+00 best_ppl=4.56                                                
Epoch 47 - |param|=3.26e+02 |g_param|=6.10e+05 loss=1.6378e+00 ppl=5.14                                                 
Validation - loss=1.4734e+00 ppl=4.36 best_loss=1.5082e+00 best_ppl=4.52                                                
Epoch 48 - |param|=3.26e+02 |g_param|=7.20e+05 loss=1.6065e+00 ppl=4.99                                                 
Validation - loss=1.4714e+00 ppl=4.36 best_loss=1.4734e+00 best_ppl=4.36                                                
Epoch 49 - |param|=3.26e+02 |g_param|=5.83e+05 loss=1.5249e+00 ppl=4.59                                                 
Validation - loss=1.4521e+00 ppl=4.27 best_loss=1.4714e+00 best_ppl=4.36                                                
Epoch 50 - |param|=3.26e+02 |g_param|=4.30e+05 loss=1.6197e+00 ppl=5.05                                                 
Validation - loss=1.4220e+00 ppl=4.15 best_loss=1.4521e+00 best_ppl=4.27                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.70e+05 loss=1.4869e+00 ppl=4.42                                                 
Validation - loss=1.4023e+00 ppl=4.06 best_loss=1.4220e+00 best_ppl=4.15                                                
Epoch 52 - |param|=3.26e+02 |g_param|=6.95e+05 loss=1.5580e+00 ppl=4.75                                                 
Validation - loss=1.4032e+00 ppl=4.07 best_loss=1.4023e+00 best_ppl=4.06                                                
Epoch 53 - |param|=3.26e+02 |g_param|=5.21e+05 loss=1.4921e+00 ppl=4.45                                                 
Validation - loss=1.3929e+00 ppl=4.03 best_loss=1.4023e+00 best_ppl=4.06                                                
Epoch 54 - |param|=3.26e+02 |g_param|=8.39e+05 loss=1.4924e+00 ppl=4.45                                                 
Validation - loss=1.3813e+00 ppl=3.98 best_loss=1.3929e+00 best_ppl=4.03                                                
Epoch 55 - |param|=3.26e+02 |g_param|=8.39e+05 loss=1.5427e+00 ppl=4.68                                                 
Validation - loss=1.3583e+00 ppl=3.89 best_loss=1.3813e+00 best_ppl=3.98                                                
Epoch 56 - |param|=3.26e+02 |g_param|=5.48e+05 loss=1.4390e+00 ppl=4.22                                                 
Validation - loss=1.3137e+00 ppl=3.72 best_loss=1.3583e+00 best_ppl=3.89                                                
Epoch 57 - |param|=3.26e+02 |g_param|=8.89e+05 loss=1.4951e+00 ppl=4.46                                                 
Validation - loss=1.3100e+00 ppl=3.71 best_loss=1.3137e+00 best_ppl=3.72                                                
Epoch 58 - |param|=3.26e+02 |g_param|=5.12e+05 loss=1.4290e+00 ppl=4.17                                                 
Validation - loss=1.3168e+00 ppl=3.73 best_loss=1.3100e+00 best_ppl=3.71                                                
Epoch 59 - |param|=3.26e+02 |g_param|=6.52e+05 loss=1.4388e+00 ppl=4.22                                                 
Validation - loss=1.2831e+00 ppl=3.61 best_loss=1.3100e+00 best_ppl=3.71                                                
Epoch 60 - |param|=3.26e+02 |g_param|=4.85e+05 loss=1.4943e+00 ppl=4.46                                                 
Validation - loss=1.2589e+00 ppl=3.52 best_loss=1.2831e+00 best_ppl=3.61                                                
Epoch 61 - |param|=3.26e+02 |g_param|=4.77e+05 loss=1.4245e+00 ppl=4.16                                                 
Validation - loss=1.2449e+00 ppl=3.47 best_loss=1.2589e+00 best_ppl=3.52                                                
Epoch 62 - |param|=3.26e+02 |g_param|=1.03e+06 loss=1.4111e+00 ppl=4.10                                                 
Validation - loss=1.2519e+00 ppl=3.50 best_loss=1.2449e+00 best_ppl=3.47                                                
Epoch 63 - |param|=3.26e+02 |g_param|=6.93e+05 loss=1.4447e+00 ppl=4.24                                                 
Validation - loss=1.2330e+00 ppl=3.43 best_loss=1.2449e+00 best_ppl=3.47                                                
Epoch 64 - |param|=3.26e+02 |g_param|=5.62e+05 loss=1.3886e+00 ppl=4.01                                                 
Validation - loss=1.2146e+00 ppl=3.37 best_loss=1.2330e+00 best_ppl=3.43                                                
Epoch 65 - |param|=3.26e+02 |g_param|=4.95e+05 loss=1.3248e+00 ppl=3.76                                                 
Validation - loss=1.2198e+00 ppl=3.39 best_loss=1.2146e+00 best_ppl=3.37                                                
Epoch 66 - |param|=3.26e+02 |g_param|=5.74e+05 loss=1.3021e+00 ppl=3.68                                                 
Validation - loss=1.1912e+00 ppl=3.29 best_loss=1.2146e+00 best_ppl=3.37                                                
Epoch 67 - |param|=3.26e+02 |g_param|=4.75e+05 loss=1.3007e+00 ppl=3.67                                                 
Validation - loss=1.1849e+00 ppl=3.27 best_loss=1.1912e+00 best_ppl=3.29                                                
Epoch 68 - |param|=3.26e+02 |g_param|=7.33e+05 loss=1.3028e+00 ppl=3.68                                                 
Validation - loss=1.1730e+00 ppl=3.23 best_loss=1.1849e+00 best_ppl=3.27                                                
Epoch 69 - |param|=3.26e+02 |g_param|=5.16e+05 loss=1.2677e+00 ppl=3.55                                                 
Validation - loss=1.1712e+00 ppl=3.23 best_loss=1.1730e+00 best_ppl=3.23                                                
Epoch 70 - |param|=3.26e+02 |g_param|=9.71e+05 loss=1.2743e+00 ppl=3.58                                                 
Validation - loss=1.2101e+00 ppl=3.35 best_loss=1.1712e+00 best_ppl=3.23                                                
Epoch 71 - |param|=3.26e+02 |g_param|=5.63e+05 loss=1.2403e+00 ppl=3.46                                                 
Validation - loss=1.1407e+00 ppl=3.13 best_loss=1.1712e+00 best_ppl=3.23                                                
Epoch 72 - |param|=3.27e+02 |g_param|=5.40e+05 loss=1.2681e+00 ppl=3.55                                                 
Validation - loss=1.1319e+00 ppl=3.10 best_loss=1.1407e+00 best_ppl=3.13                                                
Epoch 73 - |param|=3.27e+02 |g_param|=7.69e+05 loss=1.2829e+00 ppl=3.61                                                 
Validation - loss=1.1817e+00 ppl=3.26 best_loss=1.1319e+00 best_ppl=3.10                                                
Epoch 74 - |param|=3.27e+02 |g_param|=9.69e+05 loss=1.2659e+00 ppl=3.55                                                 
Validation - loss=1.1886e+00 ppl=3.28 best_loss=1.1319e+00 best_ppl=3.10                                                
Epoch 75 - |param|=3.27e+02 |g_param|=6.66e+05 loss=1.2721e+00 ppl=3.57                                                 
Validation - loss=1.1656e+00 ppl=3.21 best_loss=1.1319e+00 best_ppl=3.10                                                
Epoch 76 - |param|=3.27e+02 |g_param|=6.55e+05 loss=1.2671e+00 ppl=3.55                                                 
Validation - loss=1.0963e+00 ppl=2.99 best_loss=1.1319e+00 best_ppl=3.10                                                
Epoch 77 - |param|=3.27e+02 |g_param|=2.37e+05 loss=1.2340e+00 ppl=3.43                                                 
Validation - loss=1.0995e+00 ppl=3.00 best_loss=1.0963e+00 best_ppl=2.99                                                
Epoch 78 - |param|=3.27e+02 |g_param|=3.19e+05 loss=1.1911e+00 ppl=3.29                                                 
Validation - loss=1.1023e+00 ppl=3.01 best_loss=1.0963e+00 best_ppl=2.99                                                
Epoch 79 - |param|=3.27e+02 |g_param|=4.59e+05 loss=1.2097e+00 ppl=3.35                                                 
Validation - loss=1.0840e+00 ppl=2.96 best_loss=1.0963e+00 best_ppl=2.99                                                
Epoch 80 - |param|=3.27e+02 |g_param|=2.73e+05 loss=1.2374e+00 ppl=3.45                                                 
Validation - loss=1.0917e+00 ppl=2.98 best_loss=1.0840e+00 best_ppl=2.96                                                
Epoch 81 - |param|=3.27e+02 |g_param|=3.72e+05 loss=1.2381e+00 ppl=3.45                                                 
Validation - loss=1.0739e+00 ppl=2.93 best_loss=1.0840e+00 best_ppl=2.96                                                
Epoch 82 - |param|=3.27e+02 |g_param|=4.33e+05 loss=1.1499e+00 ppl=3.16                                                 
Validation - loss=1.0624e+00 ppl=2.89 best_loss=1.0739e+00 best_ppl=2.93                                                
Epoch 83 - |param|=3.27e+02 |g_param|=3.27e+05 loss=1.1674e+00 ppl=3.21                                                 
Validation - loss=1.0467e+00 ppl=2.85 best_loss=1.0624e+00 best_ppl=2.89                                                
Epoch 84 - |param|=3.27e+02 |g_param|=3.84e+05 loss=1.2105e+00 ppl=3.36                                                 
Validation - loss=1.0479e+00 ppl=2.85 best_loss=1.0467e+00 best_ppl=2.85                                                
Epoch 85 - |param|=3.27e+02 |g_param|=3.77e+05 loss=1.1031e+00 ppl=3.01                                                 
Validation - loss=1.0397e+00 ppl=2.83 best_loss=1.0467e+00 best_ppl=2.85                                                
Epoch 86 - |param|=3.27e+02 |g_param|=6.50e+05 loss=1.2038e+00 ppl=3.33                                                 
Validation - loss=1.0860e+00 ppl=2.96 best_loss=1.0397e+00 best_ppl=2.83                                                
Epoch 87 - |param|=3.27e+02 |g_param|=4.29e+05 loss=1.1945e+00 ppl=3.30                                                 
Validation - loss=1.0234e+00 ppl=2.78 best_loss=1.0397e+00 best_ppl=2.83                                                
Epoch 88 - |param|=3.27e+02 |g_param|=5.35e+05 loss=1.1454e+00 ppl=3.14                                                 
Validation - loss=1.0342e+00 ppl=2.81 best_loss=1.0234e+00 best_ppl=2.78                                                
Epoch 89 - |param|=3.27e+02 |g_param|=4.42e+05 loss=1.1549e+00 ppl=3.17                                                 
Validation - loss=1.0297e+00 ppl=2.80 best_loss=1.0234e+00 best_ppl=2.78                                                
Epoch 90 - |param|=3.27e+02 |g_param|=3.75e+05 loss=1.1058e+00 ppl=3.02                                                 
Validation - loss=1.0205e+00 ppl=2.77 best_loss=1.0234e+00 best_ppl=2.78                                                
Epoch 91 - |param|=3.27e+02 |g_param|=4.79e+05 loss=1.1208e+00 ppl=3.07                                                 
Validation - loss=1.0189e+00 ppl=2.77 best_loss=1.0205e+00 best_ppl=2.77                                                
Epoch 92 - |param|=3.27e+02 |g_param|=4.01e+05 loss=1.1196e+00 ppl=3.06                                                 
Validation - loss=1.0042e+00 ppl=2.73 best_loss=1.0189e+00 best_ppl=2.77                                                
Epoch 93 - |param|=3.27e+02 |g_param|=2.91e+05 loss=1.0529e+00 ppl=2.87                                                 
Validation - loss=9.9163e-01 ppl=2.70 best_loss=1.0042e+00 best_ppl=2.73                                                
Epoch 94 - |param|=3.27e+02 |g_param|=4.52e+05 loss=1.1030e+00 ppl=3.01                                                 
Validation - loss=9.8466e-01 ppl=2.68 best_loss=9.9163e-01 best_ppl=2.70                                                
Epoch 95 - |param|=3.27e+02 |g_param|=3.59e+05 loss=1.1198e+00 ppl=3.06                                                 
Validation - loss=9.8060e-01 ppl=2.67 best_loss=9.8466e-01 best_ppl=2.68                                                
Epoch 96 - |param|=3.27e+02 |g_param|=3.39e+05 loss=1.0819e+00 ppl=2.95                                                 
Validation - loss=9.9173e-01 ppl=2.70 best_loss=9.8060e-01 best_ppl=2.67                                                
Epoch 97 - |param|=3.27e+02 |g_param|=3.98e+05 loss=1.0697e+00 ppl=2.91                                                 
Validation - loss=9.7487e-01 ppl=2.65 best_loss=9.8060e-01 best_ppl=2.67                                                
Epoch 98 - |param|=3.27e+02 |g_param|=5.22e+05 loss=1.0799e+00 ppl=2.94                                                 
Validation - loss=9.7674e-01 ppl=2.66 best_loss=9.7487e-01 best_ppl=2.65                                                
Epoch 99 - |param|=3.27e+02 |g_param|=3.89e+05 loss=1.1108e+00 ppl=3.04                                                 
Validation - loss=9.6297e-01 ppl=2.62 best_loss=9.7487e-01 best_ppl=2.65                                                
Epoch 100 - |param|=3.27e+02 |g_param|=4.21e+05 loss=1.0997e+00 ppl=3.00                                                
Validation - loss=9.6193e-01 ppl=2.62 best_loss=9.6297e-01 best_ppl=2.62                                                

real	32m36.757s
user	32m28.267s
sys	0m6.346s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-40epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.39.1.78-5.94.1.69-5.41.pth
BLEU = 31.33, 58.8/39.0/25.4/16.5 (BP=1.000, ratio=1.150, hyp_len=27044, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.40.1.77-5.88.1.64-5.15.pth
BLEU = 34.25, 62.8/42.2/27.9/18.6 (BP=1.000, ratio=1.076, hyp_len=25302, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.41.1.72-5.61.1.61-4.98.pth
BLEU = 35.71, 63.8/43.4/29.3/20.0 (BP=1.000, ratio=1.070, hyp_len=25153, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.42.1.73-5.61.1.58-4.85.pth
BLEU = 36.41, 65.1/44.4/29.9/20.3 (BP=1.000, ratio=1.053, hyp_len=24762, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.43.1.72-5.58.1.56-4.78.pth
BLEU = 35.18, 62.5/42.8/29.0/19.8 (BP=1.000, ratio=1.106, hyp_len=26001, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.44.1.66-5.26.1.53-4.64.pth
BLEU = 36.79, 64.5/44.5/30.5/20.9 (BP=1.000, ratio=1.081, hyp_len=25424, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.45.1.63-5.12.1.52-4.56.pth
BLEU = 37.79, 65.2/45.5/31.4/21.8 (BP=1.000, ratio=1.076, hyp_len=25296, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.46.1.61-5.01.1.51-4.52.pth
BLEU = 37.97, 65.7/46.0/31.5/21.8 (BP=1.000, ratio=1.074, hyp_len=25258, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.47.1.64-5.14.1.47-4.36.pth
BLEU = 38.91, 66.3/46.7/32.6/22.7 (BP=1.000, ratio=1.067, hyp_len=25079, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.48.1.61-4.99.1.47-4.36.pth
BLEU = 39.09, 65.9/46.8/32.8/23.1 (BP=1.000, ratio=1.083, hyp_len=25464, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.49.1.52-4.59.1.45-4.27.pth
BLEU = 37.67, 63.7/45.2/31.6/22.1 (BP=1.000, ratio=1.134, hyp_len=26663, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.50.1.62-5.05.1.42-4.15.pth
BLEU = 38.47, 63.9/45.7/32.5/23.1 (BP=1.000, ratio=1.133, hyp_len=26635, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.51.1.49-4.42.1.40-4.06.pth
BLEU = 39.17, 64.9/46.6/33.1/23.6 (BP=1.000, ratio=1.121, hyp_len=26358, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.52.1.56-4.75.1.40-4.07.pth
BLEU = 40.88, 67.5/48.7/34.6/24.5 (BP=1.000, ratio=1.078, hyp_len=25350, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.53.1.49-4.45.1.39-4.03.pth
BLEU = 41.73, 68.4/49.6/35.5/25.2 (BP=1.000, ratio=1.069, hyp_len=25134, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.54.1.49-4.45.1.38-3.98.pth
BLEU = 40.99, 67.0/48.8/34.9/24.7 (BP=1.000, ratio=1.102, hyp_len=25903, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.55.1.54-4.68.1.36-3.89.pth
BLEU = 41.88, 67.8/49.6/35.7/25.6 (BP=1.000, ratio=1.095, hyp_len=25731, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.56.1.44-4.22.1.31-3.72.pth
BLEU = 44.73, 70.6/52.2/38.3/28.4 (BP=1.000, ratio=1.048, hyp_len=24627, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.57.1.50-4.46.1.31-3.71.pth
BLEU = 43.60, 69.1/50.9/37.3/27.5 (BP=1.000, ratio=1.073, hyp_len=25231, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.58.1.43-4.17.1.32-3.73.pth
BLEU = 43.16, 68.7/50.9/37.0/26.8 (BP=1.000, ratio=1.085, hyp_len=25507, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.59.1.44-4.22.1.28-3.61.pth
BLEU = 45.12, 70.8/52.8/38.8/28.6 (BP=1.000, ratio=1.058, hyp_len=24871, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.60.1.49-4.46.1.26-3.52.pth
BLEU = 45.03, 70.7/52.7/38.7/28.5 (BP=1.000, ratio=1.063, hyp_len=25000, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.61.1.42-4.16.1.24-3.47.pth
BLEU = 46.63, 71.7/54.1/40.3/30.2 (BP=1.000, ratio=1.054, hyp_len=24785, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.62.1.41-4.10.1.25-3.50.pth
BLEU = 47.56, 73.1/54.9/41.1/31.0 (BP=1.000, ratio=1.031, hyp_len=24243, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.63.1.44-4.24.1.23-3.43.pth
BLEU = 45.68, 70.4/53.2/39.5/29.4 (BP=1.000, ratio=1.082, hyp_len=25427, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.64.1.39-4.01.1.21-3.37.pth
BLEU = 47.03, 71.6/54.3/40.8/30.8 (BP=1.000, ratio=1.069, hyp_len=25124, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.65.1.32-3.76.1.22-3.39.pth
BLEU = 45.06, 69.1/52.3/39.0/29.2 (BP=1.000, ratio=1.114, hyp_len=26180, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.66.1.30-3.68.1.19-3.29.pth
BLEU = 48.37, 72.8/55.6/42.1/32.1 (BP=1.000, ratio=1.055, hyp_len=24804, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.67.1.30-3.67.1.18-3.27.pth
BLEU = 49.15, 73.4/56.4/42.9/32.8 (BP=1.000, ratio=1.052, hyp_len=24725, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.68.1.30-3.68.1.17-3.23.pth
BLEU = 46.52, 70.3/53.7/40.5/30.7 (BP=1.000, ratio=1.102, hyp_len=25912, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.69.1.27-3.55.1.17-3.23.pth
BLEU = 48.06, 72.4/55.5/41.9/31.7 (BP=1.000, ratio=1.074, hyp_len=25251, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.70.1.27-3.58.1.21-3.35.pth
BLEU = 46.77, 71.2/54.5/40.7/30.2 (BP=1.000, ratio=1.099, hyp_len=25833, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.71.1.24-3.46.1.14-3.13.pth
BLEU = 50.39, 74.5/57.7/44.1/34.0 (BP=1.000, ratio=1.043, hyp_len=24528, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.72.1.27-3.55.1.13-3.10.pth
BLEU = 50.04, 73.9/57.3/43.8/33.8 (BP=1.000, ratio=1.057, hyp_len=24841, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.73.1.28-3.61.1.18-3.26.pth
BLEU = 46.64, 70.5/54.3/40.8/30.3 (BP=1.000, ratio=1.120, hyp_len=26319, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.74.1.27-3.55.1.19-3.28.pth
BLEU = 47.98, 72.0/55.6/41.9/31.5 (BP=1.000, ratio=1.089, hyp_len=25599, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.75.1.27-3.57.1.17-3.21.pth
BLEU = 47.77, 71.9/55.5/41.8/31.2 (BP=1.000, ratio=1.095, hyp_len=25732, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.76.1.27-3.55.1.10-2.99.pth
BLEU = 51.04, 74.3/58.1/44.9/35.0 (BP=1.000, ratio=1.060, hyp_len=24927, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.77.1.23-3.43.1.10-3.00.pth
BLEU = 49.03, 72.3/56.2/43.0/33.1 (BP=1.000, ratio=1.092, hyp_len=25668, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.78.1.19-3.29.1.10-3.01.pth
BLEU = 50.59, 73.8/57.7/44.5/34.6 (BP=1.000, ratio=1.072, hyp_len=25197, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.79.1.21-3.35.1.08-2.96.pth
BLEU = 52.05, 75.0/58.8/45.9/36.2 (BP=1.000, ratio=1.054, hyp_len=24771, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.80.1.24-3.45.1.09-2.98.pth
BLEU = 50.72, 74.2/58.1/44.7/34.4 (BP=1.000, ratio=1.071, hyp_len=25180, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.81.1.24-3.45.1.07-2.93.pth
BLEU = 52.47, 75.5/59.5/46.4/36.4 (BP=1.000, ratio=1.050, hyp_len=24682, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.82.1.15-3.16.1.06-2.89.pth
BLEU = 52.03, 75.0/59.2/46.0/35.9 (BP=1.000, ratio=1.065, hyp_len=25043, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.83.1.17-3.21.1.05-2.85.pth
BLEU = 52.67, 75.5/59.7/46.7/36.6 (BP=1.000, ratio=1.058, hyp_len=24877, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.84.1.21-3.36.1.05-2.85.pth
BLEU = 52.89, 75.8/60.0/46.8/36.8 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.85.1.10-3.01.1.04-2.83.pth
BLEU = 52.23, 74.8/59.3/46.3/36.3 (BP=1.000, ratio=1.072, hyp_len=25205, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.86.1.20-3.33.1.09-2.96.pth
BLEU = 50.35, 73.4/57.7/44.5/34.1 (BP=1.000, ratio=1.096, hyp_len=25764, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.87.1.19-3.30.1.02-2.78.pth
BLEU = 53.36, 76.0/60.3/47.3/37.4 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.88.1.15-3.14.1.03-2.81.pth
BLEU = 53.00, 75.4/60.0/47.1/37.0 (BP=1.000, ratio=1.070, hyp_len=25145, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.89.1.15-3.17.1.03-2.80.pth
BLEU = 52.05, 74.6/59.2/46.1/36.0 (BP=1.000, ratio=1.084, hyp_len=25477, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.90.1.11-3.02.1.02-2.77.pth
BLEU = 53.97, 76.2/60.8/48.0/38.1 (BP=1.000, ratio=1.057, hyp_len=24850, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.91.1.12-3.07.1.02-2.77.pth
BLEU = 54.16, 76.4/60.9/48.2/38.4 (BP=1.000, ratio=1.051, hyp_len=24713, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.92.1.12-3.06.1.00-2.73.pth
BLEU = 54.39, 76.9/61.4/48.4/38.3 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.93.1.05-2.87.0.99-2.70.pth
BLEU = 54.70, 77.0/61.6/48.7/38.8 (BP=1.000, ratio=1.050, hyp_len=24682, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.94.1.10-3.01.0.98-2.68.pth
BLEU = 55.63, 77.5/62.4/49.7/39.8 (BP=1.000, ratio=1.045, hyp_len=24561, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.95.1.12-3.06.0.98-2.67.pth
BLEU = 55.42, 77.3/62.1/49.5/39.7 (BP=1.000, ratio=1.049, hyp_len=24662, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.96.1.08-2.95.0.99-2.70.pth
BLEU = 54.26, 76.5/61.3/48.4/38.2 (BP=1.000, ratio=1.062, hyp_len=24965, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.97.1.07-2.91.0.97-2.65.pth
BLEU = 56.16, 77.7/62.6/50.3/40.7 (BP=1.000, ratio=1.045, hyp_len=24577, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.98.1.08-2.94.0.98-2.66.pth
BLEU = 56.25, 78.0/62.8/50.3/40.7 (BP=1.000, ratio=1.040, hyp_len=24440, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.99.1.11-3.04.0.96-2.62.pth
BLEU = 56.09, 77.9/62.8/50.1/40.4 (BP=1.000, ratio=1.047, hyp_len=24615, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.100.1.10-3.00.0.96-2.62.pth
BLEU = 56.95, 78.4/63.4/51.0/41.5 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)

real	38m36.888s
user	37m56.377s
sys	1m19.144s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-40epoch$
```

Baseline က BLEU = 34.17
RL, rk-my, 40-60 model ရဲ့ အကောင်းဆုံး BLEU score က   

```
Evaluation result for the model: transformer-rl-myrk.100.1.10-3.00.0.96-2.62.pth
BLEU = 56.95, 78.4/63.4/51.0/41.5 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)
```

### RL, rk-my, 50-50 model

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth --model_fn ./model/rl/transformer/rkmy-50epoch/transformer-rl-myrk.pth --init_epoch 46 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/rkmy-50epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 46
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 46,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'load_fn': './model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/rkmy-50epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 46 - |param|=3.25e+02 |g_param|=5.54e+05 loss=1.6655e+00 ppl=5.29                                                 
Validation - loss=1.4897e+00 ppl=4.44 best_loss=inf best_ppl=inf                                                        
Epoch 47 - |param|=3.25e+02 |g_param|=1.15e+06 loss=1.6902e+00 ppl=5.42                                                 
Validation - loss=1.4866e+00 ppl=4.42 best_loss=1.4897e+00 best_ppl=4.44                                                
Epoch 48 - |param|=3.25e+02 |g_param|=5.62e+05 loss=1.6081e+00 ppl=4.99                                                 
Validation - loss=1.4552e+00 ppl=4.29 best_loss=1.4866e+00 best_ppl=4.42                                                
Epoch 49 - |param|=3.25e+02 |g_param|=4.75e+05 loss=1.6128e+00 ppl=5.02                                                 
Validation - loss=1.4388e+00 ppl=4.22 best_loss=1.4552e+00 best_ppl=4.29                                                
Epoch 50 - |param|=3.25e+02 |g_param|=5.81e+05 loss=1.6031e+00 ppl=4.97                                                 
Validation - loss=1.4274e+00 ppl=4.17 best_loss=1.4388e+00 best_ppl=4.22                                                
Epoch 51 - |param|=3.25e+02 |g_param|=7.85e+05 loss=1.5879e+00 ppl=4.89                                                 
Validation - loss=1.4036e+00 ppl=4.07 best_loss=1.4274e+00 best_ppl=4.17                                                
Epoch 52 - |param|=3.25e+02 |g_param|=1.04e+06 loss=1.4719e+00 ppl=4.36                                                 
Validation - loss=1.3927e+00 ppl=4.03 best_loss=1.4036e+00 best_ppl=4.07                                                
Epoch 53 - |param|=3.25e+02 |g_param|=5.88e+05 loss=1.5395e+00 ppl=4.66                                                 
Validation - loss=1.3750e+00 ppl=3.96 best_loss=1.3927e+00 best_ppl=4.03                                                
Epoch 54 - |param|=3.25e+02 |g_param|=5.48e+05 loss=1.4580e+00 ppl=4.30                                                 
Validation - loss=1.3627e+00 ppl=3.91 best_loss=1.3750e+00 best_ppl=3.96                                                
Epoch 55 - |param|=3.25e+02 |g_param|=6.96e+05 loss=1.4412e+00 ppl=4.23                                                 
Validation - loss=1.3757e+00 ppl=3.96 best_loss=1.3627e+00 best_ppl=3.91                                                
Epoch 56 - |param|=3.25e+02 |g_param|=7.49e+05 loss=1.4616e+00 ppl=4.31                                                 
Validation - loss=1.3496e+00 ppl=3.86 best_loss=1.3627e+00 best_ppl=3.91                                                
Epoch 57 - |param|=3.25e+02 |g_param|=5.39e+05 loss=1.4258e+00 ppl=4.16                                                 
Validation - loss=1.3350e+00 ppl=3.80 best_loss=1.3496e+00 best_ppl=3.86                                                
Epoch 58 - |param|=3.25e+02 |g_param|=6.38e+05 loss=1.4385e+00 ppl=4.21                                                 
Validation - loss=1.3278e+00 ppl=3.77 best_loss=1.3350e+00 best_ppl=3.80                                                
Epoch 59 - |param|=3.26e+02 |g_param|=9.23e+05 loss=1.4544e+00 ppl=4.28                                                 
Validation - loss=1.2840e+00 ppl=3.61 best_loss=1.3278e+00 best_ppl=3.77                                                
Epoch 60 - |param|=3.26e+02 |g_param|=7.29e+05 loss=1.3353e+00 ppl=3.80                                                 
Validation - loss=1.2766e+00 ppl=3.58 best_loss=1.2840e+00 best_ppl=3.61                                                
Epoch 61 - |param|=3.26e+02 |g_param|=5.11e+05 loss=1.4265e+00 ppl=4.16                                                 
Validation - loss=1.2747e+00 ppl=3.58 best_loss=1.2766e+00 best_ppl=3.58                                                
Epoch 62 - |param|=3.26e+02 |g_param|=6.75e+05 loss=1.3471e+00 ppl=3.85                                                 
Validation - loss=1.2805e+00 ppl=3.60 best_loss=1.2747e+00 best_ppl=3.58                                                
Epoch 63 - |param|=3.26e+02 |g_param|=7.25e+05 loss=1.3695e+00 ppl=3.93                                                 
Validation - loss=1.2731e+00 ppl=3.57 best_loss=1.2747e+00 best_ppl=3.58                                                
Epoch 64 - |param|=3.26e+02 |g_param|=8.13e+05 loss=1.3520e+00 ppl=3.87                                                 
Validation - loss=1.2377e+00 ppl=3.45 best_loss=1.2731e+00 best_ppl=3.57                                                
Epoch 65 - |param|=3.26e+02 |g_param|=9.10e+05 loss=1.3554e+00 ppl=3.88                                                 
Validation - loss=1.2167e+00 ppl=3.38 best_loss=1.2377e+00 best_ppl=3.45                                                
Epoch 66 - |param|=3.26e+02 |g_param|=5.69e+05 loss=1.3632e+00 ppl=3.91                                                 
Validation - loss=1.2263e+00 ppl=3.41 best_loss=1.2167e+00 best_ppl=3.38                                                
Epoch 67 - |param|=3.26e+02 |g_param|=5.32e+05 loss=1.3371e+00 ppl=3.81                                                 
Validation - loss=1.2013e+00 ppl=3.32 best_loss=1.2167e+00 best_ppl=3.38                                                
Epoch 68 - |param|=3.26e+02 |g_param|=6.83e+05 loss=1.2937e+00 ppl=3.65                                                 
Validation - loss=1.2392e+00 ppl=3.45 best_loss=1.2013e+00 best_ppl=3.32                                                
Epoch 69 - |param|=3.26e+02 |g_param|=8.83e+05 loss=1.3135e+00 ppl=3.72                                                 
Validation - loss=1.1823e+00 ppl=3.26 best_loss=1.2013e+00 best_ppl=3.32                                                
Epoch 70 - |param|=3.26e+02 |g_param|=5.52e+05 loss=1.3063e+00 ppl=3.69                                                 
Validation - loss=1.1728e+00 ppl=3.23 best_loss=1.1823e+00 best_ppl=3.26                                                
Epoch 71 - |param|=3.26e+02 |g_param|=8.14e+05 loss=1.3273e+00 ppl=3.77                                                 
Validation - loss=1.1575e+00 ppl=3.18 best_loss=1.1728e+00 best_ppl=3.23                                                
Epoch 72 - |param|=3.26e+02 |g_param|=8.32e+05 loss=1.3645e+00 ppl=3.91                                                 
Validation - loss=1.1534e+00 ppl=3.17 best_loss=1.1575e+00 best_ppl=3.18                                                
Epoch 73 - |param|=3.26e+02 |g_param|=8.74e+05 loss=1.2830e+00 ppl=3.61                                                 
Validation - loss=1.1551e+00 ppl=3.17 best_loss=1.1534e+00 best_ppl=3.17                                                
Epoch 74 - |param|=3.26e+02 |g_param|=8.51e+05 loss=1.2490e+00 ppl=3.49                                                 
Validation - loss=1.1401e+00 ppl=3.13 best_loss=1.1534e+00 best_ppl=3.17                                                
Epoch 75 - |param|=3.26e+02 |g_param|=6.27e+05 loss=1.2235e+00 ppl=3.40                                                 
Validation - loss=1.1442e+00 ppl=3.14 best_loss=1.1401e+00 best_ppl=3.13                                                
Epoch 76 - |param|=3.26e+02 |g_param|=7.10e+05 loss=1.2552e+00 ppl=3.51                                                 
Validation - loss=1.1284e+00 ppl=3.09 best_loss=1.1401e+00 best_ppl=3.13                                                
Epoch 77 - |param|=3.26e+02 |g_param|=8.56e+05 loss=1.2737e+00 ppl=3.57                                                 
Validation - loss=1.1132e+00 ppl=3.04 best_loss=1.1284e+00 best_ppl=3.09                                                
Epoch 78 - |param|=3.26e+02 |g_param|=9.29e+05 loss=1.3138e+00 ppl=3.72                                                 
Validation - loss=1.1257e+00 ppl=3.08 best_loss=1.1132e+00 best_ppl=3.04                                                
Epoch 79 - |param|=3.26e+02 |g_param|=6.14e+05 loss=1.2046e+00 ppl=3.34                                                 
Validation - loss=1.1233e+00 ppl=3.08 best_loss=1.1132e+00 best_ppl=3.04                                                
Epoch 80 - |param|=3.26e+02 |g_param|=6.17e+05 loss=1.1804e+00 ppl=3.26                                                 
Validation - loss=1.1063e+00 ppl=3.02 best_loss=1.1132e+00 best_ppl=3.04                                                
Epoch 81 - |param|=3.26e+02 |g_param|=5.28e+05 loss=1.2223e+00 ppl=3.40                                                 
Validation - loss=1.0813e+00 ppl=2.95 best_loss=1.1063e+00 best_ppl=3.02                                                
Epoch 82 - |param|=3.26e+02 |g_param|=4.18e+05 loss=1.1531e+00 ppl=3.17                                                 
Validation - loss=1.0769e+00 ppl=2.94 best_loss=1.0813e+00 best_ppl=2.95                                                
Epoch 83 - |param|=3.26e+02 |g_param|=3.67e+05 loss=1.1505e+00 ppl=3.16                                                 
Validation - loss=1.0785e+00 ppl=2.94 best_loss=1.0769e+00 best_ppl=2.94                                                
Epoch 84 - |param|=3.26e+02 |g_param|=5.44e+05 loss=1.1654e+00 ppl=3.21                                                 
Validation - loss=1.0735e+00 ppl=2.93 best_loss=1.0769e+00 best_ppl=2.94                                                
Epoch 85 - |param|=3.26e+02 |g_param|=5.16e+05 loss=1.1547e+00 ppl=3.17                                                 
Validation - loss=1.0960e+00 ppl=2.99 best_loss=1.0735e+00 best_ppl=2.93                                                
Epoch 86 - |param|=3.26e+02 |g_param|=4.16e+05 loss=1.1079e+00 ppl=3.03                                                 
Validation - loss=1.0541e+00 ppl=2.87 best_loss=1.0735e+00 best_ppl=2.93                                                
Epoch 87 - |param|=3.26e+02 |g_param|=4.49e+05 loss=1.1639e+00 ppl=3.20                                                 
Validation - loss=1.0722e+00 ppl=2.92 best_loss=1.0541e+00 best_ppl=2.87                                                
Epoch 88 - |param|=3.26e+02 |g_param|=4.36e+05 loss=1.1960e+00 ppl=3.31                                                 
Validation - loss=1.0488e+00 ppl=2.85 best_loss=1.0541e+00 best_ppl=2.87                                                
Epoch 89 - |param|=3.26e+02 |g_param|=3.74e+05 loss=1.1373e+00 ppl=3.12                                                 
Validation - loss=1.0531e+00 ppl=2.87 best_loss=1.0488e+00 best_ppl=2.85                                                
Epoch 90 - |param|=3.26e+02 |g_param|=4.93e+05 loss=1.1855e+00 ppl=3.27                                                 
Validation - loss=1.0436e+00 ppl=2.84 best_loss=1.0488e+00 best_ppl=2.85                                                
Epoch 91 - |param|=3.26e+02 |g_param|=4.70e+05 loss=1.1520e+00 ppl=3.16                                                 
Validation - loss=1.0852e+00 ppl=2.96 best_loss=1.0436e+00 best_ppl=2.84                                                
Epoch 92 - |param|=3.26e+02 |g_param|=5.57e+05 loss=1.1128e+00 ppl=3.04                                                 
Validation - loss=1.0665e+00 ppl=2.91 best_loss=1.0436e+00 best_ppl=2.84                                                
Epoch 93 - |param|=3.26e+02 |g_param|=3.52e+05 loss=1.1209e+00 ppl=3.07                                                 
Validation - loss=1.0263e+00 ppl=2.79 best_loss=1.0436e+00 best_ppl=2.84                                                
Epoch 94 - |param|=3.26e+02 |g_param|=3.04e+05 loss=1.1239e+00 ppl=3.08                                                 
Validation - loss=1.0162e+00 ppl=2.76 best_loss=1.0263e+00 best_ppl=2.79                                                
Epoch 95 - |param|=3.26e+02 |g_param|=7.96e+05 loss=1.0948e+00 ppl=2.99                                                 
Validation - loss=1.0277e+00 ppl=2.79 best_loss=1.0162e+00 best_ppl=2.76                                                
Epoch 96 - |param|=3.26e+02 |g_param|=4.50e+05 loss=1.0681e+00 ppl=2.91                                                 
Validation - loss=1.0028e+00 ppl=2.73 best_loss=1.0162e+00 best_ppl=2.76                                                
Epoch 97 - |param|=3.26e+02 |g_param|=3.56e+05 loss=1.1047e+00 ppl=3.02                                                 
Validation - loss=9.9750e-01 ppl=2.71 best_loss=1.0028e+00 best_ppl=2.73                                                
Epoch 98 - |param|=3.27e+02 |g_param|=2.70e+05 loss=1.0599e+00 ppl=2.89                                                 
Validation - loss=1.0100e+00 ppl=2.75 best_loss=9.9750e-01 best_ppl=2.71                                                
Epoch 99 - |param|=3.27e+02 |g_param|=4.44e+05 loss=1.0623e+00 ppl=2.89                                                 
Validation - loss=9.9321e-01 ppl=2.70 best_loss=9.9750e-01 best_ppl=2.71                                                
Epoch 100 - |param|=3.27e+02 |g_param|=4.99e+05 loss=1.0461e+00 ppl=2.85                                                
Validation - loss=9.8302e-01 ppl=2.67 best_loss=9.9321e-01 best_ppl=2.70                                                

real	29m27.705s
user	29m17.414s
sys	0m6.410s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-50epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.46.1.67-5.29.1.49-4.44.pth
BLEU = 39.37, 67.5/47.5/32.8/22.8 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.47.1.69-5.42.1.49-4.42.pth
BLEU = 38.06, 65.6/46.2/31.8/21.8 (BP=1.000, ratio=1.090, hyp_len=25636, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.48.1.61-4.99.1.46-4.29.pth
BLEU = 41.75, 69.9/49.8/35.0/24.9 (BP=1.000, ratio=1.021, hyp_len=24003, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.49.1.61-5.02.1.44-4.22.pth
BLEU = 40.73, 68.6/49.0/34.2/23.9 (BP=1.000, ratio=1.050, hyp_len=24691, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.50.1.60-4.97.1.43-4.17.pth
BLEU = 40.36, 67.9/48.5/33.8/23.8 (BP=1.000, ratio=1.067, hyp_len=25077, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.51.1.59-4.89.1.40-4.07.pth
BLEU = 42.21, 70.0/50.5/35.6/25.2 (BP=1.000, ratio=1.037, hyp_len=24387, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.52.1.47-4.36.1.39-4.03.pth
BLEU = 41.62, 68.7/49.6/35.1/25.1 (BP=1.000, ratio=1.063, hyp_len=24995, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.53.1.54-4.66.1.37-3.96.pth
BLEU = 42.34, 70.2/50.8/35.8/25.2 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.54.1.46-4.30.1.36-3.91.pth
BLEU = 41.82, 68.7/49.9/35.4/25.2 (BP=1.000, ratio=1.071, hyp_len=25183, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.55.1.44-4.23.1.38-3.96.pth
BLEU = 41.13, 67.7/49.4/34.9/24.5 (BP=1.000, ratio=1.096, hyp_len=25761, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.56.1.46-4.31.1.35-3.86.pth
BLEU = 41.55, 68.0/49.8/35.3/24.9 (BP=1.000, ratio=1.097, hyp_len=25778, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.57.1.43-4.16.1.34-3.80.pth
BLEU = 43.89, 70.6/52.1/37.5/26.9 (BP=1.000, ratio=1.059, hyp_len=24907, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.58.1.44-4.21.1.33-3.77.pth
BLEU = 43.10, 69.3/51.3/36.9/26.3 (BP=1.000, ratio=1.085, hyp_len=25511, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.59.1.45-4.28.1.28-3.61.pth
BLEU = 46.13, 72.4/54.1/39.6/29.2 (BP=1.000, ratio=1.036, hyp_len=24355, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.60.1.34-3.80.1.28-3.58.pth
BLEU = 45.77, 71.6/53.7/39.4/29.0 (BP=1.000, ratio=1.056, hyp_len=24815, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.61.1.43-4.16.1.27-3.58.pth
BLEU = 44.97, 71.3/53.1/38.6/28.0 (BP=1.000, ratio=1.060, hyp_len=24924, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.62.1.35-3.85.1.28-3.60.pth
BLEU = 44.54, 70.6/52.6/38.3/27.7 (BP=1.000, ratio=1.078, hyp_len=25345, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.63.1.37-3.93.1.27-3.57.pth
BLEU = 45.08, 70.8/53.3/38.9/28.1 (BP=1.000, ratio=1.079, hyp_len=25356, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.64.1.35-3.87.1.24-3.45.pth
BLEU = 46.48, 72.1/54.4/40.2/29.6 (BP=1.000, ratio=1.060, hyp_len=24918, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.65.1.36-3.88.1.22-3.38.pth
BLEU = 49.05, 74.4/56.6/42.6/32.3 (BP=1.000, ratio=1.027, hyp_len=24138, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.66.1.36-3.91.1.23-3.41.pth
BLEU = 47.73, 73.2/55.7/41.4/30.7 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.67.1.34-3.81.1.20-3.32.pth
BLEU = 48.63, 74.1/56.5/42.2/31.6 (BP=1.000, ratio=1.037, hyp_len=24388, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.68.1.29-3.65.1.24-3.45.pth
BLEU = 46.34, 71.9/54.4/40.1/29.4 (BP=1.000, ratio=1.075, hyp_len=25276, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.69.1.31-3.72.1.18-3.26.pth
BLEU = 47.80, 72.5/55.4/41.6/31.3 (BP=1.000, ratio=1.069, hyp_len=25140, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.70.1.31-3.69.1.17-3.23.pth
BLEU = 49.70, 74.4/57.4/43.4/32.9 (BP=1.000, ratio=1.044, hyp_len=24544, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.71.1.33-3.77.1.16-3.18.pth
BLEU = 50.31, 74.9/57.8/43.9/33.6 (BP=1.000, ratio=1.037, hyp_len=24369, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.72.1.36-3.91.1.15-3.17.pth
BLEU = 50.49, 74.9/58.0/44.2/33.8 (BP=1.000, ratio=1.038, hyp_len=24396, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.73.1.28-3.61.1.16-3.17.pth
BLEU = 48.89, 72.9/56.3/42.8/32.6 (BP=1.000, ratio=1.076, hyp_len=25292, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.74.1.25-3.49.1.14-3.13.pth
BLEU = 52.25, 76.5/59.6/45.9/35.6 (BP=1.000, ratio=1.019, hyp_len=23965, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.75.1.22-3.40.1.14-3.14.pth
BLEU = 48.87, 72.8/56.2/42.8/32.5 (BP=1.000, ratio=1.080, hyp_len=25382, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.76.1.26-3.51.1.13-3.09.pth
BLEU = 50.31, 74.4/57.8/44.2/33.7 (BP=1.000, ratio=1.057, hyp_len=24852, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.77.1.27-3.57.1.11-3.04.pth
BLEU = 51.17, 74.9/58.4/45.0/34.8 (BP=1.000, ratio=1.050, hyp_len=24695, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.78.1.31-3.72.1.13-3.08.pth
BLEU = 50.72, 75.0/58.3/44.5/34.0 (BP=1.000, ratio=1.048, hyp_len=24633, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.79.1.20-3.34.1.12-3.08.pth
BLEU = 50.91, 75.2/58.7/44.7/34.0 (BP=1.000, ratio=1.053, hyp_len=24763, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.80.1.18-3.26.1.11-3.02.pth
BLEU = 51.25, 75.1/58.8/45.1/34.6 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.81.1.22-3.40.1.08-2.95.pth
BLEU = 53.11, 76.3/60.1/46.9/37.0 (BP=1.000, ratio=1.041, hyp_len=24480, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.82.1.15-3.17.1.08-2.94.pth
BLEU = 53.05, 75.9/59.9/47.0/37.2 (BP=1.000, ratio=1.049, hyp_len=24655, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.83.1.15-3.16.1.08-2.94.pth
BLEU = 52.86, 76.2/60.1/46.7/36.5 (BP=1.000, ratio=1.045, hyp_len=24556, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.84.1.17-3.21.1.07-2.93.pth
BLEU = 52.33, 75.6/59.5/46.2/36.1 (BP=1.000, ratio=1.060, hyp_len=24914, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.85.1.15-3.17.1.10-2.99.pth
BLEU = 50.76, 73.9/58.2/44.8/34.4 (BP=1.000, ratio=1.084, hyp_len=25488, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.86.1.11-3.03.1.05-2.87.pth
BLEU = 53.61, 76.7/60.7/47.5/37.4 (BP=1.000, ratio=1.045, hyp_len=24573, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.87.1.16-3.20.1.07-2.92.pth
BLEU = 52.59, 75.9/59.9/46.5/36.2 (BP=1.000, ratio=1.057, hyp_len=24850, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.88.1.20-3.31.1.05-2.85.pth
BLEU = 53.55, 76.6/60.6/47.5/37.3 (BP=1.000, ratio=1.046, hyp_len=24601, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.89.1.14-3.12.1.05-2.87.pth
BLEU = 53.45, 76.6/60.8/47.4/37.0 (BP=1.000, ratio=1.046, hyp_len=24601, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.90.1.19-3.27.1.04-2.84.pth
BLEU = 53.38, 76.3/60.6/47.4/37.1 (BP=1.000, ratio=1.056, hyp_len=24832, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.91.1.15-3.16.1.09-2.96.pth
BLEU = 51.02, 74.2/58.7/45.1/34.5 (BP=1.000, ratio=1.087, hyp_len=25558, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.92.1.11-3.04.1.07-2.91.pth
BLEU = 52.74, 76.3/60.4/46.7/36.0 (BP=1.000, ratio=1.055, hyp_len=24812, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.93.1.12-3.07.1.03-2.79.pth
BLEU = 53.82, 76.7/61.0/47.8/37.5 (BP=1.000, ratio=1.052, hyp_len=24731, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.94.1.12-3.08.1.02-2.76.pth
BLEU = 54.58, 77.2/61.6/48.6/38.4 (BP=1.000, ratio=1.047, hyp_len=24617, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.95.1.09-2.99.1.03-2.79.pth
BLEU = 53.44, 76.3/60.8/47.4/37.1 (BP=1.000, ratio=1.064, hyp_len=25022, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.96.1.07-2.91.1.00-2.73.pth
BLEU = 55.73, 78.0/62.5/49.6/39.9 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.97.1.10-3.02.1.00-2.71.pth
BLEU = 55.46, 77.8/62.4/49.5/39.4 (BP=1.000, ratio=1.044, hyp_len=24542, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.98.1.06-2.89.1.01-2.75.pth
BLEU = 53.61, 76.4/60.9/47.7/37.2 (BP=1.000, ratio=1.063, hyp_len=24981, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.99.1.06-2.89.0.99-2.70.pth
BLEU = 56.43, 78.5/63.1/50.4/40.6 (BP=1.000, ratio=1.034, hyp_len=24311, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.100.1.05-2.85.0.98-2.67.pth
BLEU = 56.08, 78.0/62.8/50.2/40.3 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)

real	31m24.246s
user	30m44.754s
sys	1m10.681s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-50epoch$
```

Baseline က BLEU = 40.40  
RL, rk-my, 50-50 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: transformer-rl-myrk.99.1.06-2.89.0.99-2.70.pth
BLEU = 56.43, 78.5/63.1/50.4/40.6 (BP=1.000, ratio=1.034, hyp_len=24311, ref_len=23509)
```

### RL, rk-my, 60-40 model

training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth --model_fn ./model/rl/transformer/rkmy-60epoch/transformer-rl-myrk.pth --init_epoch 56 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/rkmy-60epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 56
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 56,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'load_fn': './model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/rkmy-60epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 56 - |param|=3.26e+02 |g_param|=8.42e+05 loss=1.4891e+00 ppl=4.43                                                 
Validation - loss=1.3326e+00 ppl=3.79 best_loss=inf best_ppl=inf                                                        
Epoch 57 - |param|=3.26e+02 |g_param|=5.87e+05 loss=1.5109e+00 ppl=4.53                                                 
Validation - loss=1.3143e+00 ppl=3.72 best_loss=1.3326e+00 best_ppl=3.79                                                
Epoch 58 - |param|=3.26e+02 |g_param|=6.41e+05 loss=1.4414e+00 ppl=4.23                                                 
Validation - loss=1.2968e+00 ppl=3.66 best_loss=1.3143e+00 best_ppl=3.72                                                
Epoch 59 - |param|=3.26e+02 |g_param|=9.33e+05 loss=1.4507e+00 ppl=4.27                                                 
Validation - loss=1.3326e+00 ppl=3.79 best_loss=1.2968e+00 best_ppl=3.66                                                
Epoch 60 - |param|=3.26e+02 |g_param|=6.72e+05 loss=1.3655e+00 ppl=3.92                                                 
Validation - loss=1.2669e+00 ppl=3.55 best_loss=1.2968e+00 best_ppl=3.66                                                
Epoch 61 - |param|=3.26e+02 |g_param|=7.35e+05 loss=1.4129e+00 ppl=4.11                                                 
Validation - loss=1.2556e+00 ppl=3.51 best_loss=1.2669e+00 best_ppl=3.55                                                
Epoch 62 - |param|=3.26e+02 |g_param|=7.04e+05 loss=1.3813e+00 ppl=3.98                                                 
Validation - loss=1.2458e+00 ppl=3.48 best_loss=1.2556e+00 best_ppl=3.51                                                
Epoch 63 - |param|=3.26e+02 |g_param|=5.80e+05 loss=1.3754e+00 ppl=3.96                                                 
Validation - loss=1.2338e+00 ppl=3.43 best_loss=1.2458e+00 best_ppl=3.48                                                
Epoch 64 - |param|=3.26e+02 |g_param|=7.43e+05 loss=1.4237e+00 ppl=4.15                                                 
Validation - loss=1.2286e+00 ppl=3.42 best_loss=1.2338e+00 best_ppl=3.43                                                
Epoch 65 - |param|=3.26e+02 |g_param|=7.35e+05 loss=1.3501e+00 ppl=3.86                                                 
Validation - loss=1.2445e+00 ppl=3.47 best_loss=1.2286e+00 best_ppl=3.42                                                
Epoch 66 - |param|=3.26e+02 |g_param|=2.49e+05 loss=1.3289e+00 ppl=3.78                                                 
Validation - loss=1.2035e+00 ppl=3.33 best_loss=1.2286e+00 best_ppl=3.42                                                
Epoch 67 - |param|=3.26e+02 |g_param|=3.02e+05 loss=1.3245e+00 ppl=3.76                                                 
Validation - loss=1.1950e+00 ppl=3.30 best_loss=1.2035e+00 best_ppl=3.33                                                
Epoch 68 - |param|=3.26e+02 |g_param|=4.90e+05 loss=1.3519e+00 ppl=3.86                                                 
Validation - loss=1.2449e+00 ppl=3.47 best_loss=1.1950e+00 best_ppl=3.30                                                
Epoch 69 - |param|=3.26e+02 |g_param|=4.10e+05 loss=1.3304e+00 ppl=3.78                                                 
Validation - loss=1.1949e+00 ppl=3.30 best_loss=1.1950e+00 best_ppl=3.30                                                
Epoch 70 - |param|=3.26e+02 |g_param|=3.35e+05 loss=1.2843e+00 ppl=3.61                                                 
Validation - loss=1.1882e+00 ppl=3.28 best_loss=1.1949e+00 best_ppl=3.30                                                
Epoch 71 - |param|=3.26e+02 |g_param|=3.71e+05 loss=1.3164e+00 ppl=3.73                                                 
Validation - loss=1.1548e+00 ppl=3.17 best_loss=1.1882e+00 best_ppl=3.28                                                
Epoch 72 - |param|=3.26e+02 |g_param|=3.43e+05 loss=1.2909e+00 ppl=3.64                                                 
Validation - loss=1.1430e+00 ppl=3.14 best_loss=1.1548e+00 best_ppl=3.17                                                
Epoch 73 - |param|=3.26e+02 |g_param|=4.88e+05 loss=1.2718e+00 ppl=3.57                                                 
Validation - loss=1.1451e+00 ppl=3.14 best_loss=1.1430e+00 best_ppl=3.14                                                
Epoch 74 - |param|=3.26e+02 |g_param|=4.40e+05 loss=1.2581e+00 ppl=3.52                                                 
Validation - loss=1.1390e+00 ppl=3.12 best_loss=1.1430e+00 best_ppl=3.14                                                
Epoch 75 - |param|=3.26e+02 |g_param|=3.03e+05 loss=1.2740e+00 ppl=3.58                                                 
Validation - loss=1.1462e+00 ppl=3.15 best_loss=1.1390e+00 best_ppl=3.12                                                
Epoch 76 - |param|=3.26e+02 |g_param|=3.67e+05 loss=1.2245e+00 ppl=3.40                                                 
Validation - loss=1.1130e+00 ppl=3.04 best_loss=1.1390e+00 best_ppl=3.12                                                
Epoch 77 - |param|=3.26e+02 |g_param|=3.14e+05 loss=1.2556e+00 ppl=3.51                                                 
Validation - loss=1.1135e+00 ppl=3.04 best_loss=1.1130e+00 best_ppl=3.04                                                
Epoch 78 - |param|=3.26e+02 |g_param|=4.22e+05 loss=1.2594e+00 ppl=3.52                                                 
Validation - loss=1.0981e+00 ppl=3.00 best_loss=1.1130e+00 best_ppl=3.04                                                
Epoch 79 - |param|=3.26e+02 |g_param|=4.10e+05 loss=1.2070e+00 ppl=3.34                                                 
Validation - loss=1.0889e+00 ppl=2.97 best_loss=1.0981e+00 best_ppl=3.00                                                
Epoch 80 - |param|=3.26e+02 |g_param|=6.25e+05 loss=1.2296e+00 ppl=3.42                                                 
Validation - loss=1.0929e+00 ppl=2.98 best_loss=1.0889e+00 best_ppl=2.97                                                
Epoch 81 - |param|=3.26e+02 |g_param|=2.44e+05 loss=1.1507e+00 ppl=3.16                                                 
Validation - loss=1.0780e+00 ppl=2.94 best_loss=1.0889e+00 best_ppl=2.97                                                
Epoch 82 - |param|=3.26e+02 |g_param|=8.50e+05 loss=1.2009e+00 ppl=3.32                                                 
Validation - loss=1.0794e+00 ppl=2.94 best_loss=1.0780e+00 best_ppl=2.94                                                
Epoch 83 - |param|=3.26e+02 |g_param|=4.15e+05 loss=1.1723e+00 ppl=3.23                                                 
Validation - loss=1.0716e+00 ppl=2.92 best_loss=1.0780e+00 best_ppl=2.94                                                
Epoch 84 - |param|=3.26e+02 |g_param|=4.77e+05 loss=1.1585e+00 ppl=3.19                                                 
Validation - loss=1.0646e+00 ppl=2.90 best_loss=1.0716e+00 best_ppl=2.92                                                
Epoch 85 - |param|=3.26e+02 |g_param|=3.82e+05 loss=1.1549e+00 ppl=3.17                                                 
Validation - loss=1.0466e+00 ppl=2.85 best_loss=1.0646e+00 best_ppl=2.90                                                
Epoch 86 - |param|=3.26e+02 |g_param|=4.51e+05 loss=1.1554e+00 ppl=3.18                                                 
Validation - loss=1.0464e+00 ppl=2.85 best_loss=1.0466e+00 best_ppl=2.85                                                
Epoch 87 - |param|=3.26e+02 |g_param|=4.51e+05 loss=1.1754e+00 ppl=3.24                                                 
Validation - loss=1.0426e+00 ppl=2.84 best_loss=1.0464e+00 best_ppl=2.85                                                
Epoch 88 - |param|=3.26e+02 |g_param|=3.23e+05 loss=1.1420e+00 ppl=3.13                                                 
Validation - loss=1.0346e+00 ppl=2.81 best_loss=1.0426e+00 best_ppl=2.84                                                
Epoch 89 - |param|=3.26e+02 |g_param|=3.47e+05 loss=1.1682e+00 ppl=3.22                                                 
Validation - loss=1.0280e+00 ppl=2.80 best_loss=1.0346e+00 best_ppl=2.81                                                
Epoch 90 - |param|=3.26e+02 |g_param|=7.07e+05 loss=1.1838e+00 ppl=3.27                                                 
Validation - loss=1.0392e+00 ppl=2.83 best_loss=1.0280e+00 best_ppl=2.80                                                
Epoch 91 - |param|=3.26e+02 |g_param|=3.78e+05 loss=1.1198e+00 ppl=3.06                                                 
Validation - loss=1.0207e+00 ppl=2.78 best_loss=1.0280e+00 best_ppl=2.80                                                
Epoch 92 - |param|=3.26e+02 |g_param|=3.32e+05 loss=1.1402e+00 ppl=3.13                                                 
Validation - loss=1.0193e+00 ppl=2.77 best_loss=1.0207e+00 best_ppl=2.78                                                
Epoch 93 - |param|=3.26e+02 |g_param|=3.11e+05 loss=1.1347e+00 ppl=3.11                                                 
Validation - loss=1.0446e+00 ppl=2.84 best_loss=1.0193e+00 best_ppl=2.77                                                
Epoch 94 - |param|=3.26e+02 |g_param|=4.14e+05 loss=1.0853e+00 ppl=2.96                                                 
Validation - loss=1.0079e+00 ppl=2.74 best_loss=1.0193e+00 best_ppl=2.77                                                
Epoch 95 - |param|=3.26e+02 |g_param|=4.78e+05 loss=1.0680e+00 ppl=2.91                                                 
Validation - loss=1.0065e+00 ppl=2.74 best_loss=1.0079e+00 best_ppl=2.74                                                
Epoch 96 - |param|=3.26e+02 |g_param|=3.29e+05 loss=1.0421e+00 ppl=2.84                                                 
Validation - loss=1.0023e+00 ppl=2.72 best_loss=1.0065e+00 best_ppl=2.74                                                
Epoch 97 - |param|=3.26e+02 |g_param|=4.48e+05 loss=1.0535e+00 ppl=2.87                                                 
Validation - loss=1.0007e+00 ppl=2.72 best_loss=1.0023e+00 best_ppl=2.72                                                
Epoch 98 - |param|=3.26e+02 |g_param|=4.61e+05 loss=1.0738e+00 ppl=2.93                                                 
Validation - loss=9.9663e-01 ppl=2.71 best_loss=1.0007e+00 best_ppl=2.72                                                
Epoch 99 - |param|=3.26e+02 |g_param|=6.21e+05 loss=1.0614e+00 ppl=2.89                                                 
Validation - loss=1.0256e+00 ppl=2.79 best_loss=9.9663e-01 best_ppl=2.71                                                
Epoch 100 - |param|=3.26e+02 |g_param|=5.20e+05 loss=1.0428e+00 ppl=2.84                                                
Validation - loss=9.7335e-01 ppl=2.65 best_loss=9.9663e-01 best_ppl=2.71                                                

real	23m30.342s
user	23m22.944s
sys	0m5.052s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-60epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.56.1.49-4.43.1.33-3.79.pth
BLEU = 42.77, 68.9/50.5/36.5/26.3 (BP=1.000, ratio=1.080, hyp_len=25394, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.57.1.51-4.53.1.31-3.72.pth
BLEU = 43.38, 69.3/51.2/37.1/26.9 (BP=1.000, ratio=1.078, hyp_len=25341, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.58.1.44-4.23.1.30-3.66.pth
BLEU = 46.94, 72.6/54.4/40.4/30.4 (BP=1.000, ratio=1.026, hyp_len=24114, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.59.1.45-4.27.1.33-3.79.pth
BLEU = 47.53, 73.5/54.9/40.8/31.0 (BP=1.000, ratio=1.011, hyp_len=23774, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.60.1.37-3.92.1.27-3.55.pth
BLEU = 46.87, 72.6/54.6/40.4/30.1 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.61.1.41-4.11.1.26-3.51.pth
BLEU = 47.74, 72.9/55.1/41.2/31.4 (BP=1.000, ratio=1.032, hyp_len=24269, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.62.1.38-3.98.1.25-3.48.pth
BLEU = 46.26, 71.4/53.8/39.9/29.9 (BP=1.000, ratio=1.064, hyp_len=25014, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.63.1.38-3.96.1.23-3.43.pth
BLEU = 47.32, 72.6/55.0/41.0/30.6 (BP=1.000, ratio=1.046, hyp_len=24595, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.64.1.42-4.15.1.23-3.42.pth
BLEU = 49.18, 74.2/56.5/42.6/32.7 (BP=1.000, ratio=1.026, hyp_len=24116, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.65.1.35-3.86.1.24-3.47.pth
BLEU = 45.10, 70.3/53.0/38.9/28.5 (BP=1.000, ratio=1.089, hyp_len=25607, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.66.1.33-3.78.1.20-3.33.pth
BLEU = 49.37, 74.0/56.7/43.0/32.9 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.67.1.32-3.76.1.19-3.30.pth
BLEU = 47.20, 71.9/54.8/41.0/30.7 (BP=1.000, ratio=1.077, hyp_len=25318, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.68.1.35-3.86.1.24-3.47.pth
BLEU = 44.31, 69.0/52.3/38.4/27.8 (BP=1.000, ratio=1.124, hyp_len=26428, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.69.1.33-3.78.1.19-3.30.pth
BLEU = 46.88, 71.8/54.8/40.7/30.1 (BP=1.000, ratio=1.077, hyp_len=25322, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.70.1.28-3.61.1.19-3.28.pth
BLEU = 51.37, 75.5/58.5/45.0/35.0 (BP=1.000, ratio=1.021, hyp_len=24001, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.71.1.32-3.73.1.15-3.17.pth
BLEU = 48.60, 72.7/55.9/42.4/32.3 (BP=1.000, ratio=1.072, hyp_len=25210, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.72.1.29-3.64.1.14-3.14.pth
BLEU = 50.14, 74.1/57.5/44.0/33.8 (BP=1.000, ratio=1.051, hyp_len=24716, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.73.1.27-3.57.1.15-3.14.pth
BLEU = 50.58, 74.9/58.0/44.2/34.1 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.74.1.26-3.52.1.14-3.12.pth
BLEU = 46.46, 69.9/53.8/40.6/30.5 (BP=1.000, ratio=1.128, hyp_len=26524, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.75.1.27-3.58.1.15-3.15.pth
BLEU = 45.75, 69.3/53.2/39.9/29.7 (BP=1.000, ratio=1.135, hyp_len=26675, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.76.1.22-3.40.1.11-3.04.pth
BLEU = 50.77, 74.4/58.1/44.7/34.4 (BP=1.000, ratio=1.056, hyp_len=24817, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.77.1.26-3.51.1.11-3.04.pth
BLEU = 50.67, 74.3/58.0/44.6/34.3 (BP=1.000, ratio=1.060, hyp_len=24915, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.78.1.26-3.52.1.10-3.00.pth
BLEU = 53.76, 76.8/60.6/47.5/37.8 (BP=1.000, ratio=1.026, hyp_len=24127, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.79.1.21-3.34.1.09-2.97.pth
BLEU = 52.53, 75.9/59.8/46.4/36.2 (BP=1.000, ratio=1.043, hyp_len=24512, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.80.1.23-3.42.1.09-2.98.pth
BLEU = 50.40, 73.5/57.5/44.4/34.4 (BP=1.000, ratio=1.081, hyp_len=25417, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.81.1.15-3.16.1.08-2.94.pth
BLEU = 54.00, 77.2/61.1/47.8/37.7 (BP=1.000, ratio=1.026, hyp_len=24122, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.82.1.20-3.32.1.08-2.94.pth
BLEU = 51.62, 74.8/58.9/45.6/35.3 (BP=1.000, ratio=1.066, hyp_len=25061, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.83.1.17-3.23.1.07-2.92.pth
BLEU = 51.47, 74.7/58.8/45.5/35.1 (BP=1.000, ratio=1.067, hyp_len=25081, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.84.1.16-3.19.1.06-2.90.pth
BLEU = 53.34, 76.4/60.4/47.2/37.2 (BP=1.000, ratio=1.042, hyp_len=24490, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.85.1.15-3.17.1.05-2.85.pth
BLEU = 53.99, 76.6/60.9/47.9/38.0 (BP=1.000, ratio=1.044, hyp_len=24544, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.86.1.16-3.18.1.05-2.85.pth
BLEU = 52.98, 75.7/60.1/47.0/36.8 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.87.1.18-3.24.1.04-2.84.pth
BLEU = 54.85, 77.1/61.6/48.8/39.1 (BP=1.000, ratio=1.039, hyp_len=24422, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.88.1.14-3.13.1.03-2.81.pth
BLEU = 52.77, 75.1/59.8/46.9/36.8 (BP=1.000, ratio=1.074, hyp_len=25240, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.89.1.17-3.22.1.03-2.80.pth
BLEU = 53.85, 76.3/60.9/47.9/37.8 (BP=1.000, ratio=1.054, hyp_len=24773, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.90.1.18-3.27.1.04-2.83.pth
BLEU = 56.17, 78.2/62.8/50.1/40.4 (BP=1.000, ratio=1.026, hyp_len=24129, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.91.1.12-3.06.1.02-2.78.pth
BLEU = 56.48, 78.7/63.3/50.4/40.6 (BP=1.000, ratio=1.021, hyp_len=24002, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.92.1.14-3.13.1.02-2.77.pth
BLEU = 53.68, 76.1/60.9/47.8/37.5 (BP=1.000, ratio=1.062, hyp_len=24971, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.93.1.13-3.11.1.04-2.84.pth
BLEU = 52.99, 76.1/60.5/47.0/36.4 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.94.1.09-2.96.1.01-2.74.pth
BLEU = 53.48, 75.8/60.6/47.6/37.4 (BP=1.000, ratio=1.069, hyp_len=25123, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.95.1.07-2.91.1.01-2.74.pth
BLEU = 53.55, 75.2/60.3/47.7/38.0 (BP=1.000, ratio=1.080, hyp_len=25382, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.96.1.04-2.84.1.00-2.72.pth
BLEU = 54.43, 76.8/61.6/48.5/38.3 (BP=1.000, ratio=1.057, hyp_len=24842, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.97.1.05-2.87.1.00-2.72.pth
BLEU = 58.26, 79.7/64.7/52.3/42.7 (BP=1.000, ratio=1.017, hyp_len=23909, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.98.1.07-2.93.1.00-2.71.pth
BLEU = 54.30, 76.3/61.4/48.5/38.2 (BP=1.000, ratio=1.069, hyp_len=25125, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.99.1.06-2.89.1.03-2.79.pth
BLEU = 53.34, 75.8/60.9/47.6/36.9 (BP=1.000, ratio=1.076, hyp_len=25303, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.100.1.04-2.84.0.97-2.65.pth
BLEU = 57.52, 78.8/63.9/51.6/42.1 (BP=1.000, ratio=1.037, hyp_len=24376, ref_len=23509)

real	27m56.672s
user	27m27.646s
sys	0m57.737s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-60epoch$
```

Baseline က BLEU = 45.70  
RL, rk-my, 60-40 မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-rl-myrk.97.1.05-2.87.1.00-2.72.pth
BLEU = 58.26, 79.7/64.7/52.3/42.7 (BP=1.000, ratio=1.017, hyp_len=23909, ref_len=23509)
```

### RL, rk-my, 70-30 model

training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth --model_fn ./model/rl/transformer/rkmy-70epoch/transformer-rl-myrk.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/rkmy-70epoch/transformer-rl-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 70
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 70,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'load_fn': './model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/rkmy-70epoch/transformer-rl-myrk.pth',
    'n_epochs': 100,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1640, 32)
  (emb_dec): Embedding(1541, 32)
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
    (1): Linear(in_features=32, out_features=1541, bias=True)
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
Epoch 70 - |param|=3.27e+02 |g_param|=9.36e+05 loss=1.2780e+00 ppl=3.59                                                 
Validation - loss=1.1709e+00 ppl=3.22 best_loss=inf best_ppl=inf                                                        
Epoch 71 - |param|=3.27e+02 |g_param|=6.63e+05 loss=1.2974e+00 ppl=3.66                                                 
Validation - loss=1.1524e+00 ppl=3.17 best_loss=1.1709e+00 best_ppl=3.22                                                
Epoch 72 - |param|=3.27e+02 |g_param|=6.35e+05 loss=1.3020e+00 ppl=3.68                                                 
Validation - loss=1.1453e+00 ppl=3.14 best_loss=1.1524e+00 best_ppl=3.17                                                
Epoch 73 - |param|=3.27e+02 |g_param|=6.71e+05 loss=1.2752e+00 ppl=3.58                                                 
Validation - loss=1.1416e+00 ppl=3.13 best_loss=1.1453e+00 best_ppl=3.14                                                
Epoch 74 - |param|=3.27e+02 |g_param|=6.74e+05 loss=1.2379e+00 ppl=3.45                                                 
Validation - loss=1.1211e+00 ppl=3.07 best_loss=1.1416e+00 best_ppl=3.13                                                
Epoch 75 - |param|=3.27e+02 |g_param|=5.57e+05 loss=1.2749e+00 ppl=3.58                                                 
Validation - loss=1.1120e+00 ppl=3.04 best_loss=1.1211e+00 best_ppl=3.07                                                
Epoch 76 - |param|=3.27e+02 |g_param|=7.40e+05 loss=1.2039e+00 ppl=3.33                                                 
Validation - loss=1.1048e+00 ppl=3.02 best_loss=1.1120e+00 best_ppl=3.04                                                
Epoch 77 - |param|=3.27e+02 |g_param|=6.22e+05 loss=1.2075e+00 ppl=3.35                                                 
Validation - loss=1.1062e+00 ppl=3.02 best_loss=1.1048e+00 best_ppl=3.02                                                
Epoch 78 - |param|=3.27e+02 |g_param|=1.38e+06 loss=1.2653e+00 ppl=3.54                                                 
Validation - loss=1.0985e+00 ppl=3.00 best_loss=1.1048e+00 best_ppl=3.02                                                
Epoch 79 - |param|=3.27e+02 |g_param|=8.96e+05 loss=1.1572e+00 ppl=3.18                                                 
Validation - loss=1.0901e+00 ppl=2.97 best_loss=1.0985e+00 best_ppl=3.00                                                
Epoch 80 - |param|=3.28e+02 |g_param|=9.85e+05 loss=1.1706e+00 ppl=3.22                                                 
Validation - loss=1.0820e+00 ppl=2.95 best_loss=1.0901e+00 best_ppl=2.97                                                
Epoch 81 - |param|=3.28e+02 |g_param|=5.46e+05 loss=1.2012e+00 ppl=3.32                                                 
Validation - loss=1.0723e+00 ppl=2.92 best_loss=1.0820e+00 best_ppl=2.95                                                
Epoch 82 - |param|=3.28e+02 |g_param|=6.76e+05 loss=1.1530e+00 ppl=3.17                                                 
Validation - loss=1.0639e+00 ppl=2.90 best_loss=1.0723e+00 best_ppl=2.92                                                
Epoch 83 - |param|=3.28e+02 |g_param|=7.39e+05 loss=1.1637e+00 ppl=3.20                                                 
Validation - loss=1.0622e+00 ppl=2.89 best_loss=1.0639e+00 best_ppl=2.90                                                
Epoch 84 - |param|=3.28e+02 |g_param|=2.27e+05 loss=1.1777e+00 ppl=3.25                                                 
Validation - loss=1.0514e+00 ppl=2.86 best_loss=1.0622e+00 best_ppl=2.89                                                
Epoch 85 - |param|=3.28e+02 |g_param|=6.26e+05 loss=1.1669e+00 ppl=3.21                                                 
Validation - loss=1.0830e+00 ppl=2.95 best_loss=1.0514e+00 best_ppl=2.86                                                
Epoch 86 - |param|=3.28e+02 |g_param|=4.43e+05 loss=1.0956e+00 ppl=2.99                                                 
Validation - loss=1.0455e+00 ppl=2.84 best_loss=1.0514e+00 best_ppl=2.86                                                
Epoch 87 - |param|=3.28e+02 |g_param|=6.89e+05 loss=1.1303e+00 ppl=3.10                                                 
Validation - loss=1.0531e+00 ppl=2.87 best_loss=1.0455e+00 best_ppl=2.84                                                
Epoch 88 - |param|=3.28e+02 |g_param|=3.56e+05 loss=1.0912e+00 ppl=2.98                                                 
Validation - loss=1.0256e+00 ppl=2.79 best_loss=1.0455e+00 best_ppl=2.84                                                
Epoch 89 - |param|=3.28e+02 |g_param|=3.12e+05 loss=1.0867e+00 ppl=2.96                                                 
Validation - loss=1.0304e+00 ppl=2.80 best_loss=1.0256e+00 best_ppl=2.79                                                
Epoch 90 - |param|=3.28e+02 |g_param|=3.37e+05 loss=1.0528e+00 ppl=2.87                                                 
Validation - loss=1.0301e+00 ppl=2.80 best_loss=1.0256e+00 best_ppl=2.79                                                
Epoch 91 - |param|=3.28e+02 |g_param|=3.28e+05 loss=1.1020e+00 ppl=3.01                                                 
Validation - loss=1.0217e+00 ppl=2.78 best_loss=1.0256e+00 best_ppl=2.79                                                
Epoch 92 - |param|=3.28e+02 |g_param|=3.84e+05 loss=1.1083e+00 ppl=3.03                                                 
Validation - loss=1.0044e+00 ppl=2.73 best_loss=1.0217e+00 best_ppl=2.78                                                
Epoch 93 - |param|=3.28e+02 |g_param|=6.26e+05 loss=1.1671e+00 ppl=3.21                                                 
Validation - loss=1.0073e+00 ppl=2.74 best_loss=1.0044e+00 best_ppl=2.73                                                
Epoch 94 - |param|=3.28e+02 |g_param|=5.15e+05 loss=1.0597e+00 ppl=2.89                                                 
Validation - loss=1.0154e+00 ppl=2.76 best_loss=1.0044e+00 best_ppl=2.73                                                
Epoch 95 - |param|=3.28e+02 |g_param|=3.21e+05 loss=1.0666e+00 ppl=2.91                                                 
Validation - loss=9.9531e-01 ppl=2.71 best_loss=1.0044e+00 best_ppl=2.73                                                
Epoch 96 - |param|=3.28e+02 |g_param|=3.65e+05 loss=1.0224e+00 ppl=2.78                                                 
Validation - loss=9.9072e-01 ppl=2.69 best_loss=9.9531e-01 best_ppl=2.71                                                
Epoch 97 - |param|=3.28e+02 |g_param|=6.41e+05 loss=1.0702e+00 ppl=2.92                                                 
Validation - loss=9.9578e-01 ppl=2.71 best_loss=9.9072e-01 best_ppl=2.69                                                
Epoch 98 - |param|=3.28e+02 |g_param|=5.52e+05 loss=1.0559e+00 ppl=2.87                                                 
Validation - loss=1.0418e+00 ppl=2.83 best_loss=9.9072e-01 best_ppl=2.69                                                
Epoch 99 - |param|=3.28e+02 |g_param|=4.95e+05 loss=1.0430e+00 ppl=2.84                                                 
Validation - loss=9.7975e-01 ppl=2.66 best_loss=9.9072e-01 best_ppl=2.69                                                
Epoch 100 - |param|=3.28e+02 |g_param|=3.42e+05 loss=1.0445e+00 ppl=2.84                                                
Validation - loss=9.6695e-01 ppl=2.63 best_loss=9.7975e-01 best_ppl=2.66                                                

real	16m17.247s
user	16m11.844s
sys	0m3.685s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-70epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-myrk.70.1.28-3.59.1.17-3.22.pth
BLEU = 48.71, 73.1/56.1/42.5/32.3 (BP=1.000, ratio=1.066, hyp_len=25066, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.71.1.30-3.66.1.15-3.17.pth
BLEU = 47.69, 71.5/54.9/41.6/31.7 (BP=1.000, ratio=1.097, hyp_len=25783, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.72.1.30-3.68.1.15-3.14.pth
BLEU = 49.08, 73.4/56.5/42.9/32.6 (BP=1.000, ratio=1.069, hyp_len=25134, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.73.1.28-3.58.1.14-3.13.pth
BLEU = 49.51, 73.6/57.0/43.4/33.0 (BP=1.000, ratio=1.067, hyp_len=25075, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.74.1.24-3.45.1.12-3.07.pth
BLEU = 52.61, 75.9/59.3/46.4/36.7 (BP=1.000, ratio=1.031, hyp_len=24245, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.75.1.27-3.58.1.11-3.04.pth
BLEU = 51.15, 74.8/58.3/45.0/34.9 (BP=1.000, ratio=1.050, hyp_len=24674, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.76.1.20-3.33.1.10-3.02.pth
BLEU = 51.76, 75.5/58.8/45.5/35.5 (BP=1.000, ratio=1.047, hyp_len=24618, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.77.1.21-3.35.1.11-3.02.pth
BLEU = 53.10, 76.3/59.9/46.9/37.1 (BP=1.000, ratio=1.035, hyp_len=24335, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.78.1.27-3.54.1.10-3.00.pth
BLEU = 53.20, 76.6/60.1/46.9/37.1 (BP=1.000, ratio=1.034, hyp_len=24313, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.79.1.16-3.18.1.09-2.97.pth
BLEU = 53.00, 76.4/60.0/46.8/36.8 (BP=1.000, ratio=1.039, hyp_len=24425, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.80.1.17-3.22.1.08-2.95.pth
BLEU = 52.32, 75.9/59.5/46.1/35.9 (BP=1.000, ratio=1.049, hyp_len=24672, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.81.1.20-3.32.1.07-2.92.pth
BLEU = 52.69, 75.7/59.6/46.6/36.6 (BP=1.000, ratio=1.053, hyp_len=24761, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.82.1.15-3.17.1.06-2.90.pth
BLEU = 53.85, 77.1/60.8/47.7/37.6 (BP=1.000, ratio=1.034, hyp_len=24302, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.83.1.16-3.20.1.06-2.89.pth
BLEU = 53.10, 76.1/60.0/47.0/37.1 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.84.1.18-3.25.1.05-2.86.pth
BLEU = 53.49, 76.2/60.2/47.4/37.7 (BP=1.000, ratio=1.050, hyp_len=24694, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.85.1.17-3.21.1.08-2.95.pth
BLEU = 50.90, 74.2/58.3/44.9/34.5 (BP=1.000, ratio=1.084, hyp_len=25486, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.86.1.10-2.99.1.05-2.84.pth
BLEU = 55.24, 77.7/61.8/49.2/39.4 (BP=1.000, ratio=1.030, hyp_len=24210, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.87.1.13-3.10.1.05-2.87.pth
BLEU = 55.60, 77.7/62.1/49.6/39.9 (BP=1.000, ratio=1.031, hyp_len=24246, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.88.1.09-2.98.1.03-2.79.pth
BLEU = 54.26, 76.6/60.9/48.3/38.5 (BP=1.000, ratio=1.055, hyp_len=24809, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.89.1.09-2.96.1.03-2.80.pth
BLEU = 56.07, 78.1/62.5/50.1/40.4 (BP=1.000, ratio=1.029, hyp_len=24197, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.90.1.05-2.87.1.03-2.80.pth
BLEU = 53.19, 75.9/60.3/47.2/37.1 (BP=1.000, ratio=1.066, hyp_len=25063, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.91.1.10-3.01.1.02-2.78.pth
BLEU = 53.98, 76.5/60.9/48.1/37.9 (BP=1.000, ratio=1.055, hyp_len=24813, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.92.1.11-3.03.1.00-2.73.pth
BLEU = 53.87, 76.2/60.8/48.0/37.9 (BP=1.000, ratio=1.065, hyp_len=25042, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.93.1.17-3.21.1.01-2.74.pth
BLEU = 54.60, 76.4/61.1/48.7/39.1 (BP=1.000, ratio=1.060, hyp_len=24930, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.94.1.06-2.89.1.02-2.76.pth
BLEU = 52.84, 75.4/59.9/47.0/36.7 (BP=1.000, ratio=1.077, hyp_len=25323, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.95.1.07-2.91.1.00-2.71.pth
BLEU = 53.77, 75.8/60.5/47.9/38.1 (BP=1.000, ratio=1.074, hyp_len=25256, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.96.1.02-2.78.0.99-2.69.pth
BLEU = 55.22, 76.9/61.6/49.3/39.8 (BP=1.000, ratio=1.062, hyp_len=24972, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.97.1.07-2.92.1.00-2.71.pth
BLEU = 54.85, 77.2/61.9/48.9/38.7 (BP=1.000, ratio=1.056, hyp_len=24836, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.98.1.06-2.87.1.04-2.83.pth
BLEU = 51.07, 73.9/58.7/45.3/34.6 (BP=1.000, ratio=1.109, hyp_len=26069, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.99.1.04-2.84.0.98-2.66.pth
BLEU = 57.20, 78.5/63.5/51.3/41.8 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
Evaluation result for the model: transformer-rl-myrk.100.1.04-2.84.0.97-2.63.pth
BLEU = 56.25, 77.7/62.7/50.4/40.8 (BP=1.000, ratio=1.054, hyp_len=24778, ref_len=23509)

real	18m12.490s
user	17m44.615s
sys	0m40.551s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/rkmy-70epoch$
```

Baseline: BLEU = 51.15  
RL, rk-my, 70-30 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: transformer-rl-myrk.99.1.04-2.84.0.98-2.66.pth
BLEU = 57.20, 78.5/63.5/51.3/41.8 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
```
