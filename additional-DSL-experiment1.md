# Additional DSL Experiment No. 1

ရှေ့မှာ လုပ်ခဲ့တဲ့ Epoch-100 experiment မှာ Seq2Seq-DSL ရဲ့ ရလဒ်က Transformer-DSL နဲ့ ရလဒ်နဲ့ အများကြီးကွာနေတာကို တွေ့ရတယ်။ အဲဒါကြောင့် epoch ကို ၅၀၀ ထိ တိုးကြည့်ရင်ကော Seq2Seq-DSL နဲ့ Transformer-DSL ရဲ့အကြားမှာ ဘယ်လိုနေမလဲ ဆိုတာကို သိရအောင်လို့ additional experiment အနေနဲ့ ထပ် run ခဲ့တယ်။ ဒီ markdown ဖိုင်က အဲဒီ run ခဲ့တဲ့ log ဖိုင်ဖြစ်တယ်။  

## Seq2Seq-DSL Training for 500 Epochs (my-bk, bk-my)  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python dual_train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
>    --lang mybk \
>    --gpu_id 0 --batch_size 64 --n_epochs 500 --max_length 100 --dropout .2 \
>    --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
>    --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
>    --lm_fn ./model/lm/mybk/lm-200epoch-mybk.pth \
>    --model_fn ./model/dsl/mybk-500epoch/dsl-model-mybk.pth | tee ./model/dsl/mybk-500epoch/training.log;
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
    'model_fn': './model/dsl/mybk-500epoch/dsl-model-mybk.pth',
    'n_epochs': 500,
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
Epoch 1 - |param|=8.50e+02 |g_param|=4.27e+05 loss_x2y=4.8800e+00 ppl_x2y=131.64 loss_y2x=4.6983e+00 ppl_y2x=109.76 dual_loss=0.0000e+00
Validation X2Y - loss=4.1257e+00 ppl=61.91 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0155e+00 ppl=55.45 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.50e+02 |g_param|=2.92e+05 loss_x2y=4.4484e+00 ppl_x2y=85.49 loss_y2x=4.2292e+00 ppl_y2x=68.66 dual_loss=0.0000e+00
Validation X2Y - loss=3.8852e+00 ppl=48.68 best_loss=4.1257e+00 best_ppl=61.91                                          
Validation Y2X - loss=3.8137e+00 ppl=45.32 best_loss=4.0155e+00 best_ppl=55.45
Epoch 3 - |param|=8.50e+02 |g_param|=2.28e+05 loss_x2y=4.3715e+00 ppl_x2y=79.16 loss_y2x=4.1270e+00 ppl_y2x=61.99 dual_loss=0.0000e+00
Validation X2Y - loss=3.8413e+00 ppl=46.58 best_loss=3.8852e+00 best_ppl=48.68                                          
Validation Y2X - loss=3.7507e+00 ppl=42.55 best_loss=3.8137e+00 best_ppl=45.32
Epoch 4 - |param|=8.50e+02 |g_param|=2.35e+05 loss_x2y=4.3597e+00 ppl_x2y=78.23 loss_y2x=4.1124e+00 ppl_y2x=61.09 dual_loss=0.0000e+00
Validation X2Y - loss=3.8095e+00 ppl=45.13 best_loss=3.8413e+00 best_ppl=46.58                                          
Validation Y2X - loss=3.7500e+00 ppl=42.52 best_loss=3.7507e+00 best_ppl=42.55
Epoch 5 - |param|=8.51e+02 |g_param|=2.34e+05 loss_x2y=4.3665e+00 ppl_x2y=78.77 loss_y2x=4.1983e+00 ppl_y2x=66.57 dual_loss=0.0000e+00
Validation X2Y - loss=3.8082e+00 ppl=45.07 best_loss=3.8095e+00 best_ppl=45.13                                          
Validation Y2X - loss=3.6976e+00 ppl=40.35 best_loss=3.7500e+00 best_ppl=42.52
Epoch 6 - |param|=8.51e+02 |g_param|=2.33e+05 loss_x2y=4.2994e+00 ppl_x2y=73.65 loss_y2x=4.0992e+00 ppl_y2x=60.29 dual_loss=0.0000e+00
Validation X2Y - loss=3.7974e+00 ppl=44.59 best_loss=3.8082e+00 best_ppl=45.07                                          
Validation Y2X - loss=3.7289e+00 ppl=41.63 best_loss=3.6976e+00 best_ppl=40.35
Epoch 7 - |param|=8.51e+02 |g_param|=2.22e+05 loss_x2y=4.2759e+00 ppl_x2y=71.94 loss_y2x=4.0402e+00 ppl_y2x=56.84 dual_loss=0.0000e+00
Validation X2Y - loss=3.7865e+00 ppl=44.10 best_loss=3.7974e+00 best_ppl=44.59                                          
Validation Y2X - loss=3.6419e+00 ppl=38.16 best_loss=3.6976e+00 best_ppl=40.35
Epoch 8 - |param|=8.52e+02 |g_param|=2.37e+05 loss_x2y=4.2625e+00 ppl_x2y=70.99 loss_y2x=4.0442e+00 ppl_y2x=57.07 dual_loss=0.0000e+00
Validation X2Y - loss=3.7902e+00 ppl=44.26 best_loss=3.7865e+00 best_ppl=44.10                                          
Validation Y2X - loss=3.6577e+00 ppl=38.77 best_loss=3.6419e+00 best_ppl=38.16
Epoch 9 - |param|=8.52e+02 |g_param|=2.15e+05 loss_x2y=4.2120e+00 ppl_x2y=67.49 loss_y2x=3.9955e+00 ppl_y2x=54.35 dual_loss=0.0000e+00
Validation X2Y - loss=3.7118e+00 ppl=40.93 best_loss=3.7865e+00 best_ppl=44.10                                          
Validation Y2X - loss=3.5566e+00 ppl=35.05 best_loss=3.6419e+00 best_ppl=38.16
Epoch 10 - |param|=8.53e+02 |g_param|=1.98e+05 loss_x2y=4.0549e+00 ppl_x2y=57.68 loss_y2x=3.8801e+00 ppl_y2x=48.43 dual_loss=0.0000e+00
Validation X2Y - loss=3.5253e+00 ppl=33.97 best_loss=3.7118e+00 best_ppl=40.93                                          
Validation Y2X - loss=3.4496e+00 ppl=31.49 best_loss=3.5566e+00 best_ppl=35.05
Epoch 11 - |param|=8.53e+02 |g_param|=1.67e+05 loss_x2y=3.9591e+00 ppl_x2y=52.41 loss_y2x=3.7268e+00 ppl_y2x=41.55 dual_loss=0.0000e+00
Validation X2Y - loss=3.4075e+00 ppl=30.19 best_loss=3.5253e+00 best_ppl=33.97                                          
Validation Y2X - loss=3.2899e+00 ppl=26.84 best_loss=3.4496e+00 best_ppl=31.49
Epoch 12 - |param|=8.54e+02 |g_param|=1.69e+05 loss_x2y=3.8748e+00 ppl_x2y=48.17 loss_y2x=3.5770e+00 ppl_y2x=35.77 dual_loss=0.0000e+00
Validation X2Y - loss=3.3575e+00 ppl=28.72 best_loss=3.4075e+00 best_ppl=30.19                                          
Validation Y2X - loss=3.1579e+00 ppl=23.52 best_loss=3.2899e+00 best_ppl=26.84
Epoch 13 - |param|=8.54e+02 |g_param|=1.43e+05 loss_x2y=3.7035e+00 ppl_x2y=40.59 loss_y2x=3.4134e+00 ppl_y2x=30.37 dual_loss=0.0000e+00
Validation X2Y - loss=3.2877e+00 ppl=26.78 best_loss=3.3575e+00 best_ppl=28.72                                          
Validation Y2X - loss=3.0846e+00 ppl=21.86 best_loss=3.1579e+00 best_ppl=23.52
Epoch 14 - |param|=8.55e+02 |g_param|=1.51e+05 loss_x2y=3.6320e+00 ppl_x2y=37.79 loss_y2x=3.3153e+00 ppl_y2x=27.53 dual_loss=0.0000e+00
Validation X2Y - loss=3.2598e+00 ppl=26.04 best_loss=3.2877e+00 best_ppl=26.78                                          
Validation Y2X - loss=3.0183e+00 ppl=20.46 best_loss=3.0846e+00 best_ppl=21.86
Epoch 15 - |param|=8.56e+02 |g_param|=1.52e+05 loss_x2y=3.5938e+00 ppl_x2y=36.37 loss_y2x=3.2778e+00 ppl_y2x=26.52 dual_loss=0.0000e+00
Validation X2Y - loss=3.1880e+00 ppl=24.24 best_loss=3.2598e+00 best_ppl=26.04                                          
Validation Y2X - loss=2.9755e+00 ppl=19.60 best_loss=3.0183e+00 best_ppl=20.46
Epoch 16 - |param|=8.56e+02 |g_param|=1.61e+05 loss_x2y=3.5673e+00 ppl_x2y=35.42 loss_y2x=3.3089e+00 ppl_y2x=27.35 dual_loss=0.0000e+00
Validation X2Y - loss=3.1481e+00 ppl=23.29 best_loss=3.1880e+00 best_ppl=24.24                                          
Validation Y2X - loss=2.9281e+00 ppl=18.69 best_loss=2.9755e+00 best_ppl=19.60
Epoch 17 - |param|=8.57e+02 |g_param|=1.57e+05 loss_x2y=3.4920e+00 ppl_x2y=32.85 loss_y2x=3.2269e+00 ppl_y2x=25.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.1077e+00 ppl=22.37 best_loss=3.1481e+00 best_ppl=23.29                                          
Validation Y2X - loss=2.8773e+00 ppl=17.77 best_loss=2.9281e+00 best_ppl=18.69
Epoch 18 - |param|=8.58e+02 |g_param|=1.52e+05 loss_x2y=3.3767e+00 ppl_x2y=29.27 loss_y2x=3.0831e+00 ppl_y2x=21.83 dual_loss=0.0000e+00
Validation X2Y - loss=3.0481e+00 ppl=21.08 best_loss=3.1077e+00 best_ppl=22.37                                          
Validation Y2X - loss=2.8175e+00 ppl=16.74 best_loss=2.8773e+00 best_ppl=17.77
Epoch 19 - |param|=8.58e+02 |g_param|=1.54e+05 loss_x2y=3.3996e+00 ppl_x2y=29.95 loss_y2x=3.0619e+00 ppl_y2x=21.37 dual_loss=0.0000e+00
Validation X2Y - loss=3.0304e+00 ppl=20.71 best_loss=3.0481e+00 best_ppl=21.08                                          
Validation Y2X - loss=2.8163e+00 ppl=16.71 best_loss=2.8175e+00 best_ppl=16.74
Epoch 20 - |param|=8.59e+02 |g_param|=1.74e+05 loss_x2y=3.3224e+00 ppl_x2y=27.73 loss_y2x=3.0530e+00 ppl_y2x=21.18 dual_loss=0.0000e+00
Validation X2Y - loss=2.9632e+00 ppl=19.36 best_loss=3.0304e+00 best_ppl=20.71                                          
Validation Y2X - loss=2.7588e+00 ppl=15.78 best_loss=2.8163e+00 best_ppl=16.71
Epoch 21 - |param|=8.60e+02 |g_param|=1.59e+05 loss_x2y=3.2730e+00 ppl_x2y=26.39 loss_y2x=3.0434e+00 ppl_y2x=20.98 dual_loss=6.5387e-01
Validation X2Y - loss=2.9746e+00 ppl=19.58 best_loss=2.9632e+00 best_ppl=19.36                                          
Validation Y2X - loss=2.7248e+00 ppl=15.25 best_loss=2.7588e+00 best_ppl=15.78
Epoch 22 - |param|=8.60e+02 |g_param|=1.72e+05 loss_x2y=3.2140e+00 ppl_x2y=24.88 loss_y2x=3.0007e+00 ppl_y2x=20.10 dual_loss=6.1087e-01
Validation X2Y - loss=2.9414e+00 ppl=18.94 best_loss=2.9632e+00 best_ppl=19.36                                          
Validation Y2X - loss=2.6856e+00 ppl=14.67 best_loss=2.7248e+00 best_ppl=15.25
Epoch 23 - |param|=8.61e+02 |g_param|=1.67e+05 loss_x2y=3.1563e+00 ppl_x2y=23.48 loss_y2x=2.9101e+00 ppl_y2x=18.36 dual_loss=5.2969e-01
Validation X2Y - loss=2.8875e+00 ppl=17.95 best_loss=2.9414e+00 best_ppl=18.94                                          
Validation Y2X - loss=2.6542e+00 ppl=14.21 best_loss=2.6856e+00 best_ppl=14.67
Epoch 24 - |param|=8.62e+02 |g_param|=1.73e+05 loss_x2y=3.1028e+00 ppl_x2y=22.26 loss_y2x=2.8778e+00 ppl_y2x=17.77 dual_loss=4.7051e-01
Validation X2Y - loss=2.8614e+00 ppl=17.49 best_loss=2.8875e+00 best_ppl=17.95                                          
Validation Y2X - loss=2.6474e+00 ppl=14.12 best_loss=2.6542e+00 best_ppl=14.21
Epoch 25 - |param|=8.63e+02 |g_param|=1.74e+05 loss_x2y=3.0825e+00 ppl_x2y=21.81 loss_y2x=2.8115e+00 ppl_y2x=16.63 dual_loss=4.5583e-01
Validation X2Y - loss=2.8092e+00 ppl=16.60 best_loss=2.8614e+00 best_ppl=17.49                                          
Validation Y2X - loss=2.6009e+00 ppl=13.48 best_loss=2.6474e+00 best_ppl=14.12
Epoch 26 - |param|=8.63e+02 |g_param|=1.75e+05 loss_x2y=3.0733e+00 ppl_x2y=21.61 loss_y2x=2.8857e+00 ppl_y2x=17.92 dual_loss=5.4068e-01
Validation X2Y - loss=2.8264e+00 ppl=16.88 best_loss=2.8092e+00 best_ppl=16.60                                          
Validation Y2X - loss=2.5895e+00 ppl=13.32 best_loss=2.6009e+00 best_ppl=13.48
Epoch 27 - |param|=8.64e+02 |g_param|=1.79e+05 loss_x2y=3.0499e+00 ppl_x2y=21.11 loss_y2x=2.8101e+00 ppl_y2x=16.61 dual_loss=4.5234e-01
Validation X2Y - loss=2.8110e+00 ppl=16.63 best_loss=2.8092e+00 best_ppl=16.60                                          
Validation Y2X - loss=2.5803e+00 ppl=13.20 best_loss=2.5895e+00 best_ppl=13.32
Epoch 28 - |param|=8.65e+02 |g_param|=1.84e+05 loss_x2y=2.9879e+00 ppl_x2y=19.84 loss_y2x=2.7173e+00 ppl_y2x=15.14 dual_loss=4.1341e-01
Validation X2Y - loss=2.7916e+00 ppl=16.31 best_loss=2.8092e+00 best_ppl=16.60                                          
Validation Y2X - loss=2.5556e+00 ppl=12.88 best_loss=2.5803e+00 best_ppl=13.20
Epoch 29 - |param|=8.65e+02 |g_param|=1.75e+05 loss_x2y=2.8766e+00 ppl_x2y=17.75 loss_y2x=2.6515e+00 ppl_y2x=14.18 dual_loss=3.6991e-01
Validation X2Y - loss=2.7839e+00 ppl=16.18 best_loss=2.7916e+00 best_ppl=16.31                                          
Validation Y2X - loss=2.5141e+00 ppl=12.36 best_loss=2.5556e+00 best_ppl=12.88
Epoch 30 - |param|=8.66e+02 |g_param|=1.86e+05 loss_x2y=2.8599e+00 ppl_x2y=17.46 loss_y2x=2.6368e+00 ppl_y2x=13.97 dual_loss=3.6206e-01
Validation X2Y - loss=2.7481e+00 ppl=15.61 best_loss=2.7839e+00 best_ppl=16.18                                          
Validation Y2X - loss=2.4875e+00 ppl=12.03 best_loss=2.5141e+00 best_ppl=12.36
Epoch 31 - |param|=8.67e+02 |g_param|=1.94e+05 loss_x2y=2.8482e+00 ppl_x2y=17.26 loss_y2x=2.6181e+00 ppl_y2x=13.71 dual_loss=3.6444e-01
Validation X2Y - loss=2.8258e+00 ppl=16.88 best_loss=2.7481e+00 best_ppl=15.61                                          
Validation Y2X - loss=2.4992e+00 ppl=12.17 best_loss=2.4875e+00 best_ppl=12.03
Epoch 32 - |param|=8.67e+02 |g_param|=2.01e+05 loss_x2y=2.8290e+00 ppl_x2y=16.93 loss_y2x=2.5905e+00 ppl_y2x=13.34 dual_loss=3.5516e-01
Validation X2Y - loss=2.7536e+00 ppl=15.70 best_loss=2.7481e+00 best_ppl=15.61                                          
Validation Y2X - loss=2.4625e+00 ppl=11.73 best_loss=2.4875e+00 best_ppl=12.03
Epoch 33 - |param|=8.68e+02 |g_param|=1.91e+05 loss_x2y=2.7760e+00 ppl_x2y=16.05 loss_y2x=2.5447e+00 ppl_y2x=12.74 dual_loss=3.3016e-01
Validation X2Y - loss=2.7393e+00 ppl=15.48 best_loss=2.7481e+00 best_ppl=15.61                                          
Validation Y2X - loss=2.4438e+00 ppl=11.52 best_loss=2.4625e+00 best_ppl=11.73
Epoch 34 - |param|=8.69e+02 |g_param|=2.13e+05 loss_x2y=2.7916e+00 ppl_x2y=16.31 loss_y2x=2.5738e+00 ppl_y2x=13.12 dual_loss=3.5664e-01
Validation X2Y - loss=2.7134e+00 ppl=15.08 best_loss=2.7393e+00 best_ppl=15.48                                          
Validation Y2X - loss=2.4400e+00 ppl=11.47 best_loss=2.4438e+00 best_ppl=11.52
Epoch 35 - |param|=8.69e+02 |g_param|=3.74e+05 loss_x2y=2.6709e+00 ppl_x2y=14.45 loss_y2x=2.4484e+00 ppl_y2x=11.57 dual_loss=3.0020e-01
Validation X2Y - loss=2.7219e+00 ppl=15.21 best_loss=2.7134e+00 best_ppl=15.08                                          
Validation Y2X - loss=2.4218e+00 ppl=11.27 best_loss=2.4400e+00 best_ppl=11.47
Epoch 36 - |param|=8.70e+02 |g_param|=4.12e+05 loss_x2y=2.6728e+00 ppl_x2y=14.48 loss_y2x=2.4517e+00 ppl_y2x=11.61 dual_loss=3.1251e-01
Validation X2Y - loss=2.7040e+00 ppl=14.94 best_loss=2.7134e+00 best_ppl=15.08                                          
Validation Y2X - loss=2.4043e+00 ppl=11.07 best_loss=2.4218e+00 best_ppl=11.27
Epoch 37 - |param|=8.71e+02 |g_param|=4.01e+05 loss_x2y=2.6301e+00 ppl_x2y=13.88 loss_y2x=2.4133e+00 ppl_y2x=11.17 dual_loss=3.0244e-01
Validation X2Y - loss=2.6914e+00 ppl=14.75 best_loss=2.7040e+00 best_ppl=14.94                                          
Validation Y2X - loss=2.4023e+00 ppl=11.05 best_loss=2.4043e+00 best_ppl=11.07
Epoch 38 - |param|=8.71e+02 |g_param|=3.94e+05 loss_x2y=2.6080e+00 ppl_x2y=13.57 loss_y2x=2.3772e+00 ppl_y2x=10.77 dual_loss=2.8564e-01
Validation X2Y - loss=2.7119e+00 ppl=15.06 best_loss=2.6914e+00 best_ppl=14.75                                          
Validation Y2X - loss=2.3646e+00 ppl=10.64 best_loss=2.4023e+00 best_ppl=11.05
Epoch 39 - |param|=8.72e+02 |g_param|=4.23e+05 loss_x2y=2.6179e+00 ppl_x2y=13.71 loss_y2x=2.3591e+00 ppl_y2x=10.58 dual_loss=2.9182e-01
Validation X2Y - loss=2.6878e+00 ppl=14.70 best_loss=2.6914e+00 best_ppl=14.75                                          
Validation Y2X - loss=2.3765e+00 ppl=10.77 best_loss=2.3646e+00 best_ppl=10.64
Epoch 40 - |param|=8.73e+02 |g_param|=4.22e+05 loss_x2y=2.5730e+00 ppl_x2y=13.10 loss_y2x=2.3540e+00 ppl_y2x=10.53 dual_loss=2.8372e-01
Validation X2Y - loss=2.6949e+00 ppl=14.80 best_loss=2.6878e+00 best_ppl=14.70                                          
Validation Y2X - loss=2.3713e+00 ppl=10.71 best_loss=2.3646e+00 best_ppl=10.64
Epoch 41 - |param|=8.73e+02 |g_param|=4.12e+05 loss_x2y=2.4897e+00 ppl_x2y=12.06 loss_y2x=2.2832e+00 ppl_y2x=9.81 dual_loss=2.8018e-01
Validation X2Y - loss=2.6825e+00 ppl=14.62 best_loss=2.6878e+00 best_ppl=14.70                                          
Validation Y2X - loss=2.3587e+00 ppl=10.58 best_loss=2.3646e+00 best_ppl=10.64
Epoch 42 - |param|=8.74e+02 |g_param|=4.39e+05 loss_x2y=2.5101e+00 ppl_x2y=12.31 loss_y2x=2.2758e+00 ppl_y2x=9.74 dual_loss=2.7048e-01
Validation X2Y - loss=2.6544e+00 ppl=14.22 best_loss=2.6825e+00 best_ppl=14.62                                          
Validation Y2X - loss=2.3628e+00 ppl=10.62 best_loss=2.3587e+00 best_ppl=10.58
Epoch 43 - |param|=8.74e+02 |g_param|=4.29e+05 loss_x2y=2.4946e+00 ppl_x2y=12.12 loss_y2x=2.3089e+00 ppl_y2x=10.06 dual_loss=2.8053e-01
Validation X2Y - loss=2.6800e+00 ppl=14.59 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3723e+00 ppl=10.72 best_loss=2.3587e+00 best_ppl=10.58
Epoch 44 - |param|=8.75e+02 |g_param|=4.65e+05 loss_x2y=2.4167e+00 ppl_x2y=11.21 loss_y2x=2.1861e+00 ppl_y2x=8.90 dual_loss=2.5724e-01
Validation X2Y - loss=2.6567e+00 ppl=14.25 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3539e+00 ppl=10.53 best_loss=2.3587e+00 best_ppl=10.58
Epoch 45 - |param|=8.76e+02 |g_param|=4.26e+05 loss_x2y=2.3718e+00 ppl_x2y=10.72 loss_y2x=2.1585e+00 ppl_y2x=8.66 dual_loss=2.5642e-01
Validation X2Y - loss=2.6708e+00 ppl=14.45 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3432e+00 ppl=10.41 best_loss=2.3539e+00 best_ppl=10.53
Epoch 46 - |param|=8.76e+02 |g_param|=4.55e+05 loss_x2y=2.3765e+00 ppl_x2y=10.77 loss_y2x=2.1768e+00 ppl_y2x=8.82 dual_loss=2.6658e-01
Validation X2Y - loss=2.6962e+00 ppl=14.82 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3473e+00 ppl=10.46 best_loss=2.3432e+00 best_ppl=10.41
Epoch 47 - |param|=8.77e+02 |g_param|=4.57e+05 loss_x2y=2.3533e+00 ppl_x2y=10.52 loss_y2x=2.1020e+00 ppl_y2x=8.18 dual_loss=2.5997e-01
Validation X2Y - loss=2.6591e+00 ppl=14.28 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3301e+00 ppl=10.28 best_loss=2.3432e+00 best_ppl=10.41
Epoch 48 - |param|=8.78e+02 |g_param|=4.87e+05 loss_x2y=2.4025e+00 ppl_x2y=11.05 loss_y2x=2.1098e+00 ppl_y2x=8.25 dual_loss=2.8031e-01
Validation X2Y - loss=2.6804e+00 ppl=14.59 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3477e+00 ppl=10.46 best_loss=2.3301e+00 best_ppl=10.28
Epoch 49 - |param|=8.78e+02 |g_param|=4.52e+05 loss_x2y=2.3060e+00 ppl_x2y=10.03 loss_y2x=2.0912e+00 ppl_y2x=8.09 dual_loss=2.6307e-01
Validation X2Y - loss=2.6643e+00 ppl=14.36 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3121e+00 ppl=10.10 best_loss=2.3301e+00 best_ppl=10.28
Epoch 50 - |param|=8.79e+02 |g_param|=5.04e+05 loss_x2y=2.2478e+00 ppl_x2y=9.47 loss_y2x=2.0368e+00 ppl_y2x=7.67 dual_loss=2.6600e-01
Validation X2Y - loss=2.6638e+00 ppl=14.35 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3557e+00 ppl=10.55 best_loss=2.3121e+00 best_ppl=10.10
Epoch 51 - |param|=8.79e+02 |g_param|=4.69e+05 loss_x2y=2.2257e+00 ppl_x2y=9.26 loss_y2x=2.0171e+00 ppl_y2x=7.52 dual_loss=2.5563e-01
Validation X2Y - loss=2.6532e+00 ppl=14.20 best_loss=2.6544e+00 best_ppl=14.22                                          
Validation Y2X - loss=2.3395e+00 ppl=10.38 best_loss=2.3121e+00 best_ppl=10.10
Epoch 52 - |param|=8.80e+02 |g_param|=5.06e+05 loss_x2y=2.2023e+00 ppl_x2y=9.05 loss_y2x=1.9862e+00 ppl_y2x=7.29 dual_loss=2.5420e-01
Validation X2Y - loss=2.6502e+00 ppl=14.16 best_loss=2.6532e+00 best_ppl=14.20                                          
Validation Y2X - loss=2.3174e+00 ppl=10.15 best_loss=2.3121e+00 best_ppl=10.10
Epoch 53 - |param|=8.81e+02 |g_param|=4.89e+05 loss_x2y=2.1986e+00 ppl_x2y=9.01 loss_y2x=1.9916e+00 ppl_y2x=7.33 dual_loss=2.6798e-01
Validation X2Y - loss=2.6616e+00 ppl=14.32 best_loss=2.6502e+00 best_ppl=14.16                                          
Validation Y2X - loss=2.3146e+00 ppl=10.12 best_loss=2.3121e+00 best_ppl=10.10
Epoch 54 - |param|=8.81e+02 |g_param|=5.01e+05 loss_x2y=2.1767e+00 ppl_x2y=8.82 loss_y2x=1.9501e+00 ppl_y2x=7.03 dual_loss=2.6475e-01
Validation X2Y - loss=2.6384e+00 ppl=13.99 best_loss=2.6502e+00 best_ppl=14.16                                          
Validation Y2X - loss=2.3201e+00 ppl=10.18 best_loss=2.3121e+00 best_ppl=10.10
Epoch 55 - |param|=8.82e+02 |g_param|=4.87e+05 loss_x2y=2.1692e+00 ppl_x2y=8.75 loss_y2x=1.9259e+00 ppl_y2x=6.86 dual_loss=2.5502e-01
Validation X2Y - loss=2.7039e+00 ppl=14.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3090e+00 ppl=10.06 best_loss=2.3121e+00 best_ppl=10.10
Epoch 56 - |param|=8.82e+02 |g_param|=5.25e+05 loss_x2y=2.2103e+00 ppl_x2y=9.12 loss_y2x=1.9871e+00 ppl_y2x=7.29 dual_loss=2.7343e-01
Validation X2Y - loss=2.6534e+00 ppl=14.20 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3217e+00 ppl=10.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 57 - |param|=8.83e+02 |g_param|=5.07e+05 loss_x2y=2.0965e+00 ppl_x2y=8.14 loss_y2x=1.8888e+00 ppl_y2x=6.61 dual_loss=2.5742e-01
Validation X2Y - loss=2.6771e+00 ppl=14.54 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3527e+00 ppl=10.51 best_loss=2.3090e+00 best_ppl=10.06
Epoch 58 - |param|=8.84e+02 |g_param|=5.18e+05 loss_x2y=2.0448e+00 ppl_x2y=7.73 loss_y2x=1.8632e+00 ppl_y2x=6.44 dual_loss=2.5142e-01
Validation X2Y - loss=2.6542e+00 ppl=14.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3239e+00 ppl=10.22 best_loss=2.3090e+00 best_ppl=10.06
Epoch 59 - |param|=8.84e+02 |g_param|=5.61e+05 loss_x2y=2.1983e+00 ppl_x2y=9.01 loss_y2x=2.0130e+00 ppl_y2x=7.49 dual_loss=2.9927e-01
Validation X2Y - loss=2.6755e+00 ppl=14.52 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3204e+00 ppl=10.18 best_loss=2.3090e+00 best_ppl=10.06
Epoch 60 - |param|=8.85e+02 |g_param|=5.60e+05 loss_x2y=2.0644e+00 ppl_x2y=7.88 loss_y2x=1.8449e+00 ppl_y2x=6.33 dual_loss=2.6130e-01
Validation X2Y - loss=2.6779e+00 ppl=14.55 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3305e+00 ppl=10.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 61 - |param|=8.85e+02 |g_param|=5.36e+05 loss_x2y=2.0283e+00 ppl_x2y=7.60 loss_y2x=1.8341e+00 ppl_y2x=6.26 dual_loss=2.7522e-01
Validation X2Y - loss=2.6878e+00 ppl=14.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3517e+00 ppl=10.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 62 - |param|=8.86e+02 |g_param|=5.55e+05 loss_x2y=2.0343e+00 ppl_x2y=7.65 loss_y2x=1.8078e+00 ppl_y2x=6.10 dual_loss=2.6417e-01
Validation X2Y - loss=2.7052e+00 ppl=14.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3209e+00 ppl=10.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 63 - |param|=8.86e+02 |g_param|=5.46e+05 loss_x2y=2.0168e+00 ppl_x2y=7.51 loss_y2x=1.7801e+00 ppl_y2x=5.93 dual_loss=2.6404e-01
Validation X2Y - loss=2.6854e+00 ppl=14.66 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3343e+00 ppl=10.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 64 - |param|=8.87e+02 |g_param|=5.58e+05 loss_x2y=1.9831e+00 ppl_x2y=7.27 loss_y2x=1.7582e+00 ppl_y2x=5.80 dual_loss=2.5625e-01
Validation X2Y - loss=2.7109e+00 ppl=15.04 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3409e+00 ppl=10.39 best_loss=2.3090e+00 best_ppl=10.06
Epoch 65 - |param|=8.87e+02 |g_param|=5.45e+05 loss_x2y=1.9920e+00 ppl_x2y=7.33 loss_y2x=1.7718e+00 ppl_y2x=5.88 dual_loss=2.6620e-01
Validation X2Y - loss=2.6492e+00 ppl=14.14 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3445e+00 ppl=10.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 66 - |param|=8.88e+02 |g_param|=5.60e+05 loss_x2y=1.9394e+00 ppl_x2y=6.95 loss_y2x=1.7056e+00 ppl_y2x=5.50 dual_loss=2.7207e-01
Validation X2Y - loss=2.6890e+00 ppl=14.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3523e+00 ppl=10.51 best_loss=2.3090e+00 best_ppl=10.06
Epoch 67 - |param|=8.89e+02 |g_param|=6.39e+05 loss_x2y=1.9280e+00 ppl_x2y=6.88 loss_y2x=1.7139e+00 ppl_y2x=5.55 dual_loss=2.6354e-01
Validation X2Y - loss=2.7031e+00 ppl=14.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3622e+00 ppl=10.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 68 - |param|=8.89e+02 |g_param|=7.32e+05 loss_x2y=1.8906e+00 ppl_x2y=6.62 loss_y2x=1.6833e+00 ppl_y2x=5.38 dual_loss=2.5890e-01
Validation X2Y - loss=2.6925e+00 ppl=14.77 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3640e+00 ppl=10.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 69 - |param|=8.90e+02 |g_param|=7.01e+05 loss_x2y=1.8539e+00 ppl_x2y=6.38 loss_y2x=1.6439e+00 ppl_y2x=5.18 dual_loss=2.5762e-01
Validation X2Y - loss=2.6685e+00 ppl=14.42 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3512e+00 ppl=10.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 70 - |param|=8.90e+02 |g_param|=7.68e+05 loss_x2y=1.9075e+00 ppl_x2y=6.74 loss_y2x=1.7022e+00 ppl_y2x=5.49 dual_loss=2.7350e-01
Validation X2Y - loss=2.6905e+00 ppl=14.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3847e+00 ppl=10.86 best_loss=2.3090e+00 best_ppl=10.06
Epoch 71 - |param|=8.91e+02 |g_param|=7.20e+05 loss_x2y=1.8681e+00 ppl_x2y=6.48 loss_y2x=1.6547e+00 ppl_y2x=5.23 dual_loss=2.7175e-01
Validation X2Y - loss=2.7075e+00 ppl=14.99 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3623e+00 ppl=10.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 72 - |param|=8.91e+02 |g_param|=8.02e+05 loss_x2y=1.8782e+00 ppl_x2y=6.54 loss_y2x=1.6746e+00 ppl_y2x=5.34 dual_loss=3.0551e-01
Validation X2Y - loss=2.7361e+00 ppl=15.43 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3916e+00 ppl=10.93 best_loss=2.3090e+00 best_ppl=10.06
Epoch 73 - |param|=8.92e+02 |g_param|=7.35e+05 loss_x2y=1.8327e+00 ppl_x2y=6.25 loss_y2x=1.6259e+00 ppl_y2x=5.08 dual_loss=2.8430e-01
Validation X2Y - loss=2.7460e+00 ppl=15.58 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3798e+00 ppl=10.80 best_loss=2.3090e+00 best_ppl=10.06
Epoch 74 - |param|=8.92e+02 |g_param|=8.30e+05 loss_x2y=1.8260e+00 ppl_x2y=6.21 loss_y2x=1.6441e+00 ppl_y2x=5.18 dual_loss=2.9179e-01
Validation X2Y - loss=2.7436e+00 ppl=15.54 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3887e+00 ppl=10.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 75 - |param|=8.93e+02 |g_param|=7.40e+05 loss_x2y=1.7932e+00 ppl_x2y=6.01 loss_y2x=1.5865e+00 ppl_y2x=4.89 dual_loss=2.9369e-01
Validation X2Y - loss=2.7312e+00 ppl=15.35 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3671e+00 ppl=10.67 best_loss=2.3090e+00 best_ppl=10.06
Epoch 76 - |param|=8.93e+02 |g_param|=8.01e+05 loss_x2y=1.7387e+00 ppl_x2y=5.69 loss_y2x=1.5278e+00 ppl_y2x=4.61 dual_loss=2.8074e-01
Validation X2Y - loss=2.7468e+00 ppl=15.59 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3930e+00 ppl=10.95 best_loss=2.3090e+00 best_ppl=10.06
Epoch 77 - |param|=8.94e+02 |g_param|=7.59e+05 loss_x2y=1.7311e+00 ppl_x2y=5.65 loss_y2x=1.5318e+00 ppl_y2x=4.63 dual_loss=2.7723e-01
Validation X2Y - loss=2.7699e+00 ppl=15.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3946e+00 ppl=10.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 78 - |param|=8.94e+02 |g_param|=8.22e+05 loss_x2y=1.8349e+00 ppl_x2y=6.26 loss_y2x=1.6613e+00 ppl_y2x=5.27 dual_loss=3.6559e-01
Validation X2Y - loss=2.7899e+00 ppl=16.28 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.3759e+00 ppl=10.76 best_loss=2.3090e+00 best_ppl=10.06
Epoch 79 - |param|=8.95e+02 |g_param|=7.61e+05 loss_x2y=1.7115e+00 ppl_x2y=5.54 loss_y2x=1.5105e+00 ppl_y2x=4.53 dual_loss=2.8175e-01
Validation X2Y - loss=2.8148e+00 ppl=16.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4016e+00 ppl=11.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 80 - |param|=8.96e+02 |g_param|=7.94e+05 loss_x2y=1.6753e+00 ppl_x2y=5.34 loss_y2x=1.4965e+00 ppl_y2x=4.47 dual_loss=2.9175e-01
Validation X2Y - loss=2.7623e+00 ppl=15.84 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4152e+00 ppl=11.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 81 - |param|=8.96e+02 |g_param|=7.53e+05 loss_x2y=1.6793e+00 ppl_x2y=5.36 loss_y2x=1.4831e+00 ppl_y2x=4.41 dual_loss=3.0490e-01
Validation X2Y - loss=2.7861e+00 ppl=16.22 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4092e+00 ppl=11.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 82 - |param|=8.97e+02 |g_param|=8.27e+05 loss_x2y=1.6714e+00 ppl_x2y=5.32 loss_y2x=1.4702e+00 ppl_y2x=4.35 dual_loss=2.9878e-01
Validation X2Y - loss=2.7735e+00 ppl=16.01 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4172e+00 ppl=11.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 83 - |param|=8.97e+02 |g_param|=7.71e+05 loss_x2y=1.6567e+00 ppl_x2y=5.24 loss_y2x=1.4418e+00 ppl_y2x=4.23 dual_loss=2.8288e-01
Validation X2Y - loss=2.8210e+00 ppl=16.79 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4135e+00 ppl=11.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 84 - |param|=8.98e+02 |g_param|=8.31e+05 loss_x2y=1.6521e+00 ppl_x2y=5.22 loss_y2x=1.4583e+00 ppl_y2x=4.30 dual_loss=3.0658e-01
Validation X2Y - loss=2.8152e+00 ppl=16.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4447e+00 ppl=11.53 best_loss=2.3090e+00 best_ppl=10.06
Epoch 85 - |param|=8.98e+02 |g_param|=8.13e+05 loss_x2y=1.6235e+00 ppl_x2y=5.07 loss_y2x=1.4531e+00 ppl_y2x=4.28 dual_loss=2.9633e-01
Validation X2Y - loss=2.8071e+00 ppl=16.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4184e+00 ppl=11.23 best_loss=2.3090e+00 best_ppl=10.06
Epoch 86 - |param|=8.99e+02 |g_param|=8.18e+05 loss_x2y=1.6263e+00 ppl_x2y=5.09 loss_y2x=1.4330e+00 ppl_y2x=4.19 dual_loss=3.1386e-01
Validation X2Y - loss=2.7887e+00 ppl=16.26 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4458e+00 ppl=11.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 87 - |param|=8.99e+02 |g_param|=7.13e+05 loss_x2y=1.6148e+00 ppl_x2y=5.03 loss_y2x=1.4061e+00 ppl_y2x=4.08 dual_loss=3.1447e-01
Validation X2Y - loss=2.7983e+00 ppl=16.42 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4276e+00 ppl=11.33 best_loss=2.3090e+00 best_ppl=10.06
Epoch 88 - |param|=9.00e+02 |g_param|=6.56e+05 loss_x2y=1.5964e+00 ppl_x2y=4.94 loss_y2x=1.3903e+00 ppl_y2x=4.02 dual_loss=3.1730e-01
Validation X2Y - loss=2.8303e+00 ppl=16.95 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4438e+00 ppl=11.52 best_loss=2.3090e+00 best_ppl=10.06
Epoch 89 - |param|=9.00e+02 |g_param|=6.29e+05 loss_x2y=1.5835e+00 ppl_x2y=4.87 loss_y2x=1.3939e+00 ppl_y2x=4.03 dual_loss=3.1870e-01
Validation X2Y - loss=2.8121e+00 ppl=16.64 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4723e+00 ppl=11.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 90 - |param|=9.01e+02 |g_param|=6.89e+05 loss_x2y=1.5880e+00 ppl_x2y=4.89 loss_y2x=1.3836e+00 ppl_y2x=3.99 dual_loss=3.3251e-01
Validation X2Y - loss=2.7984e+00 ppl=16.42 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4872e+00 ppl=12.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 91 - |param|=9.01e+02 |g_param|=6.24e+05 loss_x2y=1.5201e+00 ppl_x2y=4.57 loss_y2x=1.3462e+00 ppl_y2x=3.84 dual_loss=3.0577e-01
Validation X2Y - loss=2.8290e+00 ppl=16.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5007e+00 ppl=12.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 92 - |param|=9.02e+02 |g_param|=6.69e+05 loss_x2y=1.5316e+00 ppl_x2y=4.63 loss_y2x=1.3321e+00 ppl_y2x=3.79 dual_loss=3.3414e-01
Validation X2Y - loss=2.8216e+00 ppl=16.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4948e+00 ppl=12.12 best_loss=2.3090e+00 best_ppl=10.06
Epoch 93 - |param|=9.02e+02 |g_param|=6.31e+05 loss_x2y=1.5056e+00 ppl_x2y=4.51 loss_y2x=1.3140e+00 ppl_y2x=3.72 dual_loss=3.2122e-01
Validation X2Y - loss=2.8495e+00 ppl=17.28 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5003e+00 ppl=12.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 94 - |param|=9.03e+02 |g_param|=6.81e+05 loss_x2y=1.5705e+00 ppl_x2y=4.81 loss_y2x=1.3141e+00 ppl_y2x=3.72 dual_loss=3.5664e-01
Validation X2Y - loss=2.8518e+00 ppl=17.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4936e+00 ppl=12.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 95 - |param|=9.03e+02 |g_param|=6.35e+05 loss_x2y=1.4995e+00 ppl_x2y=4.48 loss_y2x=1.2872e+00 ppl_y2x=3.62 dual_loss=3.1995e-01
Validation X2Y - loss=2.8636e+00 ppl=17.52 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4732e+00 ppl=11.86 best_loss=2.3090e+00 best_ppl=10.06
Epoch 96 - |param|=9.04e+02 |g_param|=6.94e+05 loss_x2y=1.5496e+00 ppl_x2y=4.71 loss_y2x=1.3888e+00 ppl_y2x=4.01 dual_loss=3.9314e-01
Validation X2Y - loss=2.8597e+00 ppl=17.46 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4744e+00 ppl=11.87 best_loss=2.3090e+00 best_ppl=10.06
Epoch 97 - |param|=9.04e+02 |g_param|=6.67e+05 loss_x2y=1.4685e+00 ppl_x2y=4.34 loss_y2x=1.2787e+00 ppl_y2x=3.59 dual_loss=3.2275e-01
Validation X2Y - loss=2.8838e+00 ppl=17.88 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5241e+00 ppl=12.48 best_loss=2.3090e+00 best_ppl=10.06
Epoch 98 - |param|=9.05e+02 |g_param|=6.87e+05 loss_x2y=1.4826e+00 ppl_x2y=4.40 loss_y2x=1.3267e+00 ppl_y2x=3.77 dual_loss=3.4799e-01
Validation X2Y - loss=2.8836e+00 ppl=17.88 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.4972e+00 ppl=12.15 best_loss=2.3090e+00 best_ppl=10.06
Epoch 99 - |param|=9.05e+02 |g_param|=6.64e+05 loss_x2y=1.4508e+00 ppl_x2y=4.27 loss_y2x=1.2635e+00 ppl_y2x=3.54 dual_loss=3.4764e-01
Validation X2Y - loss=2.8852e+00 ppl=17.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5366e+00 ppl=12.64 best_loss=2.3090e+00 best_ppl=10.06
Epoch 100 - |param|=9.06e+02 |g_param|=1.22e+06 loss_x2y=1.4231e+00 ppl_x2y=4.15 loss_y2x=1.2545e+00 ppl_y2x=3.51 dual_loss=3.3718e-01
Validation X2Y - loss=2.9017e+00 ppl=18.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5676e+00 ppl=13.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 101 - |param|=9.06e+02 |g_param|=7.03e+05 loss_x2y=1.4081e+00 ppl_x2y=4.09 loss_y2x=1.2300e+00 ppl_y2x=3.42 dual_loss=3.3031e-01
Validation X2Y - loss=2.8920e+00 ppl=18.03 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5585e+00 ppl=12.92 best_loss=2.3090e+00 best_ppl=10.06
Epoch 102 - |param|=9.07e+02 |g_param|=4.96e+05 loss_x2y=1.4626e+00 ppl_x2y=4.32 loss_y2x=1.2495e+00 ppl_y2x=3.49 dual_loss=3.6570e-01
Validation X2Y - loss=2.9369e+00 ppl=18.86 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5594e+00 ppl=12.93 best_loss=2.3090e+00 best_ppl=10.06
Epoch 103 - |param|=9.07e+02 |g_param|=4.28e+05 loss_x2y=1.4156e+00 ppl_x2y=4.12 loss_y2x=1.2163e+00 ppl_y2x=3.37 dual_loss=3.5066e-01
Validation X2Y - loss=2.9320e+00 ppl=18.77 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5405e+00 ppl=12.69 best_loss=2.3090e+00 best_ppl=10.06
Epoch 104 - |param|=9.07e+02 |g_param|=4.52e+05 loss_x2y=1.3654e+00 ppl_x2y=3.92 loss_y2x=1.1901e+00 ppl_y2x=3.29 dual_loss=3.3289e-01
Validation X2Y - loss=2.9408e+00 ppl=18.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5743e+00 ppl=13.12 best_loss=2.3090e+00 best_ppl=10.06
Epoch 105 - |param|=9.08e+02 |g_param|=4.56e+05 loss_x2y=1.4210e+00 ppl_x2y=4.14 loss_y2x=1.2877e+00 ppl_y2x=3.62 dual_loss=3.8278e-01
Validation X2Y - loss=2.9098e+00 ppl=18.35 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5936e+00 ppl=13.38 best_loss=2.3090e+00 best_ppl=10.06
Epoch 106 - |param|=9.08e+02 |g_param|=4.64e+05 loss_x2y=1.3849e+00 ppl_x2y=3.99 loss_y2x=1.2184e+00 ppl_y2x=3.38 dual_loss=3.6964e-01
Validation X2Y - loss=2.9108e+00 ppl=18.37 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5783e+00 ppl=13.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 107 - |param|=9.09e+02 |g_param|=4.16e+05 loss_x2y=1.3435e+00 ppl_x2y=3.83 loss_y2x=1.1539e+00 ppl_y2x=3.17 dual_loss=3.4100e-01
Validation X2Y - loss=2.9305e+00 ppl=18.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5705e+00 ppl=13.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 108 - |param|=9.09e+02 |g_param|=4.70e+05 loss_x2y=1.3735e+00 ppl_x2y=3.95 loss_y2x=1.2293e+00 ppl_y2x=3.42 dual_loss=3.8875e-01
Validation X2Y - loss=2.9619e+00 ppl=19.34 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5639e+00 ppl=12.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 109 - |param|=9.10e+02 |g_param|=4.28e+05 loss_x2y=1.3223e+00 ppl_x2y=3.75 loss_y2x=1.1451e+00 ppl_y2x=3.14 dual_loss=3.5943e-01
Validation X2Y - loss=2.9760e+00 ppl=19.61 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5888e+00 ppl=13.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 110 - |param|=9.10e+02 |g_param|=4.54e+05 loss_x2y=1.3272e+00 ppl_x2y=3.77 loss_y2x=1.1437e+00 ppl_y2x=3.14 dual_loss=3.5928e-01
Validation X2Y - loss=2.9456e+00 ppl=19.02 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5824e+00 ppl=13.23 best_loss=2.3090e+00 best_ppl=10.06
Epoch 111 - |param|=9.11e+02 |g_param|=4.39e+05 loss_x2y=1.3138e+00 ppl_x2y=3.72 loss_y2x=1.1355e+00 ppl_y2x=3.11 dual_loss=3.7747e-01
Validation X2Y - loss=2.9367e+00 ppl=18.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6301e+00 ppl=13.88 best_loss=2.3090e+00 best_ppl=10.06
Epoch 112 - |param|=9.11e+02 |g_param|=4.74e+05 loss_x2y=1.3435e+00 ppl_x2y=3.83 loss_y2x=1.1649e+00 ppl_y2x=3.21 dual_loss=3.9618e-01
Validation X2Y - loss=2.9332e+00 ppl=18.79 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5982e+00 ppl=13.44 best_loss=2.3090e+00 best_ppl=10.06
Epoch 113 - |param|=9.12e+02 |g_param|=4.67e+05 loss_x2y=1.3319e+00 ppl_x2y=3.79 loss_y2x=1.1604e+00 ppl_y2x=3.19 dual_loss=3.9448e-01
Validation X2Y - loss=3.0153e+00 ppl=20.40 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6490e+00 ppl=14.14 best_loss=2.3090e+00 best_ppl=10.06
Epoch 114 - |param|=9.12e+02 |g_param|=4.69e+05 loss_x2y=1.2841e+00 ppl_x2y=3.61 loss_y2x=1.1144e+00 ppl_y2x=3.05 dual_loss=3.8784e-01
Validation X2Y - loss=2.9973e+00 ppl=20.03 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6054e+00 ppl=13.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 115 - |param|=9.13e+02 |g_param|=4.49e+05 loss_x2y=1.2909e+00 ppl_x2y=3.64 loss_y2x=1.0944e+00 ppl_y2x=2.99 dual_loss=3.8986e-01
Validation X2Y - loss=2.9870e+00 ppl=19.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.5993e+00 ppl=13.45 best_loss=2.3090e+00 best_ppl=10.06
Epoch 116 - |param|=9.13e+02 |g_param|=4.64e+05 loss_x2y=1.2549e+00 ppl_x2y=3.51 loss_y2x=1.0780e+00 ppl_y2x=2.94 dual_loss=3.8645e-01
Validation X2Y - loss=2.9620e+00 ppl=19.34 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6003e+00 ppl=13.47 best_loss=2.3090e+00 best_ppl=10.06
Epoch 117 - |param|=9.14e+02 |g_param|=4.64e+05 loss_x2y=1.2692e+00 ppl_x2y=3.56 loss_y2x=1.0987e+00 ppl_y2x=3.00 dual_loss=3.8983e-01
Validation X2Y - loss=2.9923e+00 ppl=19.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6301e+00 ppl=13.87 best_loss=2.3090e+00 best_ppl=10.06
Epoch 118 - |param|=9.14e+02 |g_param|=4.63e+05 loss_x2y=1.2394e+00 ppl_x2y=3.45 loss_y2x=1.0789e+00 ppl_y2x=2.94 dual_loss=3.9102e-01
Validation X2Y - loss=3.0087e+00 ppl=20.26 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6131e+00 ppl=13.64 best_loss=2.3090e+00 best_ppl=10.06
Epoch 119 - |param|=9.14e+02 |g_param|=4.50e+05 loss_x2y=1.2536e+00 ppl_x2y=3.50 loss_y2x=1.0633e+00 ppl_y2x=2.90 dual_loss=3.8645e-01
Validation X2Y - loss=3.0306e+00 ppl=20.71 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6376e+00 ppl=13.98 best_loss=2.3090e+00 best_ppl=10.06
Epoch 120 - |param|=9.15e+02 |g_param|=7.19e+05 loss_x2y=1.2213e+00 ppl_x2y=3.39 loss_y2x=1.0575e+00 ppl_y2x=2.88 dual_loss=4.0626e-01
Validation X2Y - loss=3.0115e+00 ppl=20.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6684e+00 ppl=14.42 best_loss=2.3090e+00 best_ppl=10.06
Epoch 121 - |param|=9.15e+02 |g_param|=7.05e+05 loss_x2y=1.2322e+00 ppl_x2y=3.43 loss_y2x=1.0369e+00 ppl_y2x=2.82 dual_loss=4.0212e-01
Validation X2Y - loss=2.9926e+00 ppl=19.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6539e+00 ppl=14.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 122 - |param|=9.16e+02 |g_param|=7.40e+05 loss_x2y=1.2198e+00 ppl_x2y=3.39 loss_y2x=1.0511e+00 ppl_y2x=2.86 dual_loss=4.2475e-01
Validation X2Y - loss=3.0534e+00 ppl=21.19 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6790e+00 ppl=14.57 best_loss=2.3090e+00 best_ppl=10.06
Epoch 123 - |param|=9.16e+02 |g_param|=7.06e+05 loss_x2y=1.2089e+00 ppl_x2y=3.35 loss_y2x=1.0361e+00 ppl_y2x=2.82 dual_loss=4.0682e-01
Validation X2Y - loss=3.0598e+00 ppl=21.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6796e+00 ppl=14.58 best_loss=2.3090e+00 best_ppl=10.06
Epoch 124 - |param|=9.17e+02 |g_param|=7.64e+05 loss_x2y=1.2695e+00 ppl_x2y=3.56 loss_y2x=1.0278e+00 ppl_y2x=2.79 dual_loss=4.8741e-01
Validation X2Y - loss=3.0203e+00 ppl=20.50 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6963e+00 ppl=14.83 best_loss=2.3090e+00 best_ppl=10.06
Epoch 125 - |param|=9.17e+02 |g_param|=6.82e+05 loss_x2y=1.1971e+00 ppl_x2y=3.31 loss_y2x=1.0216e+00 ppl_y2x=2.78 dual_loss=4.1048e-01
Validation X2Y - loss=3.0170e+00 ppl=20.43 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6736e+00 ppl=14.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 126 - |param|=9.18e+02 |g_param|=4.82e+05 loss_x2y=1.1900e+00 ppl_x2y=3.29 loss_y2x=1.0240e+00 ppl_y2x=2.78 dual_loss=4.1982e-01
Validation X2Y - loss=3.0450e+00 ppl=21.01 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6900e+00 ppl=14.73 best_loss=2.3090e+00 best_ppl=10.06
Epoch 127 - |param|=9.18e+02 |g_param|=4.69e+05 loss_x2y=1.2043e+00 ppl_x2y=3.33 loss_y2x=1.0108e+00 ppl_y2x=2.75 dual_loss=4.5252e-01
Validation X2Y - loss=3.0236e+00 ppl=20.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6885e+00 ppl=14.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 128 - |param|=9.19e+02 |g_param|=4.86e+05 loss_x2y=1.1786e+00 ppl_x2y=3.25 loss_y2x=9.8732e-01 ppl_y2x=2.68 dual_loss=4.3778e-01
Validation X2Y - loss=3.0340e+00 ppl=20.78 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7073e+00 ppl=14.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 129 - |param|=9.19e+02 |g_param|=4.56e+05 loss_x2y=1.1525e+00 ppl_x2y=3.17 loss_y2x=9.7895e-01 ppl_y2x=2.66 dual_loss=4.2960e-01
Validation X2Y - loss=3.0460e+00 ppl=21.03 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.6864e+00 ppl=14.68 best_loss=2.3090e+00 best_ppl=10.06
Epoch 130 - |param|=9.19e+02 |g_param|=4.76e+05 loss_x2y=1.1447e+00 ppl_x2y=3.14 loss_y2x=1.0131e+00 ppl_y2x=2.75 dual_loss=4.4885e-01
Validation X2Y - loss=3.0827e+00 ppl=21.82 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7024e+00 ppl=14.92 best_loss=2.3090e+00 best_ppl=10.06
Epoch 131 - |param|=9.20e+02 |g_param|=4.57e+05 loss_x2y=1.1344e+00 ppl_x2y=3.11 loss_y2x=9.9083e-01 ppl_y2x=2.69 dual_loss=4.4245e-01
Validation X2Y - loss=3.0837e+00 ppl=21.84 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7044e+00 ppl=14.94 best_loss=2.3090e+00 best_ppl=10.06
Epoch 132 - |param|=9.20e+02 |g_param|=4.81e+05 loss_x2y=1.1516e+00 ppl_x2y=3.16 loss_y2x=9.6691e-01 ppl_y2x=2.63 dual_loss=4.2939e-01
Validation X2Y - loss=3.1354e+00 ppl=23.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7460e+00 ppl=15.58 best_loss=2.3090e+00 best_ppl=10.06
Epoch 133 - |param|=9.21e+02 |g_param|=4.68e+05 loss_x2y=1.1150e+00 ppl_x2y=3.05 loss_y2x=9.6547e-01 ppl_y2x=2.63 dual_loss=4.4338e-01
Validation X2Y - loss=3.0742e+00 ppl=21.63 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7651e+00 ppl=15.88 best_loss=2.3090e+00 best_ppl=10.06
Epoch 134 - |param|=9.21e+02 |g_param|=6.53e+05 loss_x2y=1.1158e+00 ppl_x2y=3.05 loss_y2x=9.3541e-01 ppl_y2x=2.55 dual_loss=4.2683e-01
Validation X2Y - loss=3.0910e+00 ppl=22.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7338e+00 ppl=15.39 best_loss=2.3090e+00 best_ppl=10.06
Epoch 135 - |param|=9.22e+02 |g_param|=7.38e+05 loss_x2y=1.1008e+00 ppl_x2y=3.01 loss_y2x=9.9226e-01 ppl_y2x=2.70 dual_loss=4.8389e-01
Validation X2Y - loss=3.1399e+00 ppl=23.10 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7894e+00 ppl=16.27 best_loss=2.3090e+00 best_ppl=10.06
Epoch 136 - |param|=9.22e+02 |g_param|=7.45e+05 loss_x2y=1.0704e+00 ppl_x2y=2.92 loss_y2x=9.1249e-01 ppl_y2x=2.49 dual_loss=4.1741e-01
Validation X2Y - loss=3.1439e+00 ppl=23.19 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7497e+00 ppl=15.64 best_loss=2.3090e+00 best_ppl=10.06
Epoch 137 - |param|=9.23e+02 |g_param|=7.39e+05 loss_x2y=1.0934e+00 ppl_x2y=2.98 loss_y2x=9.2670e-01 ppl_y2x=2.53 dual_loss=4.4136e-01
Validation X2Y - loss=3.1271e+00 ppl=22.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7772e+00 ppl=16.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 138 - |param|=9.23e+02 |g_param|=7.31e+05 loss_x2y=1.0664e+00 ppl_x2y=2.90 loss_y2x=9.1977e-01 ppl_y2x=2.51 dual_loss=4.2789e-01
Validation X2Y - loss=3.1403e+00 ppl=23.11 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7881e+00 ppl=16.25 best_loss=2.3090e+00 best_ppl=10.06
Epoch 139 - |param|=9.23e+02 |g_param|=7.54e+05 loss_x2y=1.0985e+00 ppl_x2y=3.00 loss_y2x=9.3024e-01 ppl_y2x=2.54 dual_loss=4.7601e-01
Validation X2Y - loss=3.1254e+00 ppl=22.77 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7788e+00 ppl=16.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 140 - |param|=9.24e+02 |g_param|=7.73e+05 loss_x2y=1.0690e+00 ppl_x2y=2.91 loss_y2x=9.0689e-01 ppl_y2x=2.48 dual_loss=4.4937e-01
Validation X2Y - loss=3.1711e+00 ppl=23.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7945e+00 ppl=16.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 141 - |param|=9.24e+02 |g_param|=7.56e+05 loss_x2y=1.1022e+00 ppl_x2y=3.01 loss_y2x=9.3510e-01 ppl_y2x=2.55 dual_loss=5.1554e-01
Validation X2Y - loss=3.1646e+00 ppl=23.68 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7927e+00 ppl=16.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 142 - |param|=9.25e+02 |g_param|=7.56e+05 loss_x2y=1.0592e+00 ppl_x2y=2.88 loss_y2x=8.8328e-01 ppl_y2x=2.42 dual_loss=4.6389e-01
Validation X2Y - loss=3.1742e+00 ppl=23.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7780e+00 ppl=16.09 best_loss=2.3090e+00 best_ppl=10.06
Epoch 143 - |param|=9.25e+02 |g_param|=7.66e+05 loss_x2y=1.0844e+00 ppl_x2y=2.96 loss_y2x=9.1709e-01 ppl_y2x=2.50 dual_loss=4.7904e-01
Validation X2Y - loss=3.1867e+00 ppl=24.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7981e+00 ppl=16.41 best_loss=2.3090e+00 best_ppl=10.06
Epoch 144 - |param|=9.26e+02 |g_param|=8.12e+05 loss_x2y=1.1040e+00 ppl_x2y=3.02 loss_y2x=9.5711e-01 ppl_y2x=2.60 dual_loss=5.4346e-01
Validation X2Y - loss=3.2282e+00 ppl=25.23 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8032e+00 ppl=16.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 145 - |param|=9.26e+02 |g_param|=7.45e+05 loss_x2y=1.0278e+00 ppl_x2y=2.79 loss_y2x=8.6966e-01 ppl_y2x=2.39 dual_loss=4.5590e-01
Validation X2Y - loss=3.1992e+00 ppl=24.51 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7728e+00 ppl=16.00 best_loss=2.3090e+00 best_ppl=10.06
Epoch 146 - |param|=9.27e+02 |g_param|=7.83e+05 loss_x2y=1.0236e+00 ppl_x2y=2.78 loss_y2x=8.7252e-01 ppl_y2x=2.39 dual_loss=4.6429e-01
Validation X2Y - loss=3.2127e+00 ppl=24.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8003e+00 ppl=16.45 best_loss=2.3090e+00 best_ppl=10.06
Epoch 147 - |param|=9.27e+02 |g_param|=7.53e+05 loss_x2y=1.0191e+00 ppl_x2y=2.77 loss_y2x=8.4831e-01 ppl_y2x=2.34 dual_loss=4.7397e-01
Validation X2Y - loss=3.2186e+00 ppl=24.99 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7900e+00 ppl=16.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 148 - |param|=9.27e+02 |g_param|=7.70e+05 loss_x2y=1.0191e+00 ppl_x2y=2.77 loss_y2x=8.6470e-01 ppl_y2x=2.37 dual_loss=4.8712e-01
Validation X2Y - loss=3.2224e+00 ppl=25.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.7777e+00 ppl=16.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 149 - |param|=9.28e+02 |g_param|=7.44e+05 loss_x2y=9.8792e-01 ppl_x2y=2.69 loss_y2x=8.3460e-01 ppl_y2x=2.30 dual_loss=4.5951e-01
Validation X2Y - loss=3.1874e+00 ppl=24.22 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8195e+00 ppl=16.77 best_loss=2.3090e+00 best_ppl=10.06
Epoch 150 - |param|=9.28e+02 |g_param|=7.66e+05 loss_x2y=1.0272e+00 ppl_x2y=2.79 loss_y2x=8.2955e-01 ppl_y2x=2.29 dual_loss=4.9333e-01
Validation X2Y - loss=3.1712e+00 ppl=23.84 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8373e+00 ppl=17.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 151 - |param|=9.29e+02 |g_param|=7.50e+05 loss_x2y=9.8842e-01 ppl_x2y=2.69 loss_y2x=8.5416e-01 ppl_y2x=2.35 dual_loss=5.0136e-01
Validation X2Y - loss=3.2264e+00 ppl=25.19 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8678e+00 ppl=17.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 152 - |param|=9.29e+02 |g_param|=7.89e+05 loss_x2y=9.8538e-01 ppl_x2y=2.68 loss_y2x=8.1746e-01 ppl_y2x=2.26 dual_loss=4.9047e-01
Validation X2Y - loss=3.2544e+00 ppl=25.90 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8741e+00 ppl=17.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 153 - |param|=9.30e+02 |g_param|=7.66e+05 loss_x2y=1.0079e+00 ppl_x2y=2.74 loss_y2x=8.2937e-01 ppl_y2x=2.29 dual_loss=5.1835e-01
Validation X2Y - loss=3.2444e+00 ppl=25.65 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8602e+00 ppl=17.46 best_loss=2.3090e+00 best_ppl=10.06
Epoch 154 - |param|=9.30e+02 |g_param|=7.97e+05 loss_x2y=9.7205e-01 ppl_x2y=2.64 loss_y2x=8.3838e-01 ppl_y2x=2.31 dual_loss=5.0813e-01
Validation X2Y - loss=3.2659e+00 ppl=26.20 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8657e+00 ppl=17.56 best_loss=2.3090e+00 best_ppl=10.06
Epoch 155 - |param|=9.30e+02 |g_param|=7.47e+05 loss_x2y=9.6539e-01 ppl_x2y=2.63 loss_y2x=8.0711e-01 ppl_y2x=2.24 dual_loss=5.0481e-01
Validation X2Y - loss=3.2201e+00 ppl=25.03 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8644e+00 ppl=17.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 156 - |param|=9.31e+02 |g_param|=5.53e+05 loss_x2y=9.6968e-01 ppl_x2y=2.64 loss_y2x=8.1357e-01 ppl_y2x=2.26 dual_loss=5.1520e-01
Validation X2Y - loss=3.2473e+00 ppl=25.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8545e+00 ppl=17.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 157 - |param|=9.31e+02 |g_param|=4.89e+05 loss_x2y=9.5698e-01 ppl_x2y=2.60 loss_y2x=7.9899e-01 ppl_y2x=2.22 dual_loss=5.1785e-01
Validation X2Y - loss=3.2427e+00 ppl=25.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8765e+00 ppl=17.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 158 - |param|=9.32e+02 |g_param|=7.28e+05 loss_x2y=9.4550e-01 ppl_x2y=2.57 loss_y2x=8.1703e-01 ppl_y2x=2.26 dual_loss=5.1481e-01
Validation X2Y - loss=3.2937e+00 ppl=26.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8983e+00 ppl=18.14 best_loss=2.3090e+00 best_ppl=10.06
Epoch 159 - |param|=9.32e+02 |g_param|=7.77e+05 loss_x2y=9.6125e-01 ppl_x2y=2.61 loss_y2x=8.1208e-01 ppl_y2x=2.25 dual_loss=5.3012e-01
Validation X2Y - loss=3.3057e+00 ppl=27.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8901e+00 ppl=17.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 160 - |param|=9.33e+02 |g_param|=8.35e+05 loss_x2y=9.8162e-01 ppl_x2y=2.67 loss_y2x=7.9588e-01 ppl_y2x=2.22 dual_loss=5.3650e-01
Validation X2Y - loss=3.2883e+00 ppl=26.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8665e+00 ppl=17.58 best_loss=2.3090e+00 best_ppl=10.06
Epoch 161 - |param|=9.33e+02 |g_param|=7.87e+05 loss_x2y=9.2484e-01 ppl_x2y=2.52 loss_y2x=7.7735e-01 ppl_y2x=2.18 dual_loss=5.1854e-01
Validation X2Y - loss=3.2341e+00 ppl=25.38 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9335e+00 ppl=18.79 best_loss=2.3090e+00 best_ppl=10.06
Epoch 162 - |param|=9.33e+02 |g_param|=8.14e+05 loss_x2y=9.8901e-01 ppl_x2y=2.69 loss_y2x=8.0295e-01 ppl_y2x=2.23 dual_loss=5.8543e-01
Validation X2Y - loss=3.3011e+00 ppl=27.14 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.8878e+00 ppl=17.95 best_loss=2.3090e+00 best_ppl=10.06
Epoch 163 - |param|=9.34e+02 |g_param|=7.91e+05 loss_x2y=9.3311e-01 ppl_x2y=2.54 loss_y2x=7.7412e-01 ppl_y2x=2.17 dual_loss=5.4342e-01
Validation X2Y - loss=3.3309e+00 ppl=27.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9230e+00 ppl=18.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 164 - |param|=9.34e+02 |g_param|=8.08e+05 loss_x2y=9.1665e-01 ppl_x2y=2.50 loss_y2x=7.9048e-01 ppl_y2x=2.20 dual_loss=5.3754e-01
Validation X2Y - loss=3.3167e+00 ppl=27.57 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9645e+00 ppl=19.38 best_loss=2.3090e+00 best_ppl=10.06
Epoch 165 - |param|=9.35e+02 |g_param|=7.97e+05 loss_x2y=9.5160e-01 ppl_x2y=2.59 loss_y2x=7.8058e-01 ppl_y2x=2.18 dual_loss=5.7320e-01
Validation X2Y - loss=3.3257e+00 ppl=27.82 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9509e+00 ppl=19.12 best_loss=2.3090e+00 best_ppl=10.06
Epoch 166 - |param|=9.35e+02 |g_param|=8.34e+05 loss_x2y=9.7120e-01 ppl_x2y=2.64 loss_y2x=7.6277e-01 ppl_y2x=2.14 dual_loss=6.2134e-01
Validation X2Y - loss=3.3432e+00 ppl=28.31 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9323e+00 ppl=18.77 best_loss=2.3090e+00 best_ppl=10.06
Epoch 167 - |param|=9.35e+02 |g_param|=8.12e+05 loss_x2y=9.3351e-01 ppl_x2y=2.54 loss_y2x=7.9604e-01 ppl_y2x=2.22 dual_loss=5.7606e-01
Validation X2Y - loss=3.3253e+00 ppl=27.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9394e+00 ppl=18.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 168 - |param|=9.36e+02 |g_param|=8.06e+05 loss_x2y=9.1851e-01 ppl_x2y=2.51 loss_y2x=7.5925e-01 ppl_y2x=2.14 dual_loss=5.5625e-01
Validation X2Y - loss=3.3561e+00 ppl=28.68 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9843e+00 ppl=19.77 best_loss=2.3090e+00 best_ppl=10.06
Epoch 169 - |param|=9.36e+02 |g_param|=7.75e+05 loss_x2y=9.5911e-01 ppl_x2y=2.61 loss_y2x=7.8985e-01 ppl_y2x=2.20 dual_loss=6.1677e-01
Validation X2Y - loss=3.3256e+00 ppl=27.82 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0109e+00 ppl=20.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 170 - |param|=9.37e+02 |g_param|=8.01e+05 loss_x2y=9.2385e-01 ppl_x2y=2.52 loss_y2x=7.4050e-01 ppl_y2x=2.10 dual_loss=5.8272e-01
Validation X2Y - loss=3.3157e+00 ppl=27.54 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9808e+00 ppl=19.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 171 - |param|=9.37e+02 |g_param|=6.66e+05 loss_x2y=9.2805e-01 ppl_x2y=2.53 loss_y2x=7.7261e-01 ppl_y2x=2.17 dual_loss=6.3100e-01
Validation X2Y - loss=3.3300e+00 ppl=27.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0011e+00 ppl=20.11 best_loss=2.3090e+00 best_ppl=10.06
Epoch 172 - |param|=9.38e+02 |g_param|=5.07e+05 loss_x2y=8.7988e-01 ppl_x2y=2.41 loss_y2x=7.3284e-01 ppl_y2x=2.08 dual_loss=5.4592e-01
Validation X2Y - loss=3.3670e+00 ppl=28.99 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9808e+00 ppl=19.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 173 - |param|=9.38e+02 |g_param|=5.01e+05 loss_x2y=9.6415e-01 ppl_x2y=2.62 loss_y2x=7.4700e-01 ppl_y2x=2.11 dual_loss=7.5293e-01
Validation X2Y - loss=3.3552e+00 ppl=28.65 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0106e+00 ppl=20.30 best_loss=2.3090e+00 best_ppl=10.06
Epoch 174 - |param|=9.38e+02 |g_param|=5.12e+05 loss_x2y=8.5776e-01 ppl_x2y=2.36 loss_y2x=7.0862e-01 ppl_y2x=2.03 dual_loss=5.5239e-01
Validation X2Y - loss=3.3638e+00 ppl=28.90 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0207e+00 ppl=20.51 best_loss=2.3090e+00 best_ppl=10.06
Epoch 175 - |param|=9.39e+02 |g_param|=4.77e+05 loss_x2y=8.4993e-01 ppl_x2y=2.34 loss_y2x=7.0211e-01 ppl_y2x=2.02 dual_loss=5.1840e-01
Validation X2Y - loss=3.3271e+00 ppl=27.86 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9856e+00 ppl=19.80 best_loss=2.3090e+00 best_ppl=10.06
Epoch 176 - |param|=9.39e+02 |g_param|=5.13e+05 loss_x2y=8.3793e-01 ppl_x2y=2.31 loss_y2x=7.1240e-01 ppl_y2x=2.04 dual_loss=5.4989e-01
Validation X2Y - loss=3.3671e+00 ppl=28.99 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=2.9971e+00 ppl=20.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 177 - |param|=9.40e+02 |g_param|=4.82e+05 loss_x2y=8.5208e-01 ppl_x2y=2.34 loss_y2x=6.9180e-01 ppl_y2x=2.00 dual_loss=5.3861e-01
Validation X2Y - loss=3.3766e+00 ppl=29.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0316e+00 ppl=20.73 best_loss=2.3090e+00 best_ppl=10.06
Epoch 178 - |param|=9.40e+02 |g_param|=4.98e+05 loss_x2y=8.5246e-01 ppl_x2y=2.35 loss_y2x=7.0960e-01 ppl_y2x=2.03 dual_loss=5.8661e-01
Validation X2Y - loss=3.4210e+00 ppl=30.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0139e+00 ppl=20.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 179 - |param|=9.40e+02 |g_param|=4.85e+05 loss_x2y=8.7443e-01 ppl_x2y=2.40 loss_y2x=7.0963e-01 ppl_y2x=2.03 dual_loss=6.0472e-01
Validation X2Y - loss=3.4573e+00 ppl=31.73 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0590e+00 ppl=21.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 180 - |param|=9.41e+02 |g_param|=5.64e+05 loss_x2y=8.9921e-01 ppl_x2y=2.46 loss_y2x=7.6408e-01 ppl_y2x=2.15 dual_loss=6.5748e-01
Validation X2Y - loss=3.4297e+00 ppl=30.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0612e+00 ppl=21.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 181 - |param|=9.41e+02 |g_param|=5.12e+05 loss_x2y=8.4172e-01 ppl_x2y=2.32 loss_y2x=7.2010e-01 ppl_y2x=2.05 dual_loss=5.7626e-01
Validation X2Y - loss=3.4352e+00 ppl=31.04 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0980e+00 ppl=22.15 best_loss=2.3090e+00 best_ppl=10.06
Epoch 182 - |param|=9.42e+02 |g_param|=5.23e+05 loss_x2y=8.3546e-01 ppl_x2y=2.31 loss_y2x=6.8960e-01 ppl_y2x=1.99 dual_loss=6.0312e-01
Validation X2Y - loss=3.4428e+00 ppl=31.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0769e+00 ppl=21.69 best_loss=2.3090e+00 best_ppl=10.06
Epoch 183 - |param|=9.42e+02 |g_param|=5.15e+05 loss_x2y=8.5778e-01 ppl_x2y=2.36 loss_y2x=7.5474e-01 ppl_y2x=2.13 dual_loss=6.7529e-01
Validation X2Y - loss=3.4599e+00 ppl=31.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0983e+00 ppl=22.16 best_loss=2.3090e+00 best_ppl=10.06
Epoch 184 - |param|=9.42e+02 |g_param|=5.20e+05 loss_x2y=8.2306e-01 ppl_x2y=2.28 loss_y2x=6.9580e-01 ppl_y2x=2.01 dual_loss=5.9916e-01
Validation X2Y - loss=3.4240e+00 ppl=30.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0465e+00 ppl=21.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 185 - |param|=9.43e+02 |g_param|=5.08e+05 loss_x2y=8.2066e-01 ppl_x2y=2.27 loss_y2x=6.9326e-01 ppl_y2x=2.00 dual_loss=6.1160e-01
Validation X2Y - loss=3.4689e+00 ppl=32.10 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0562e+00 ppl=21.25 best_loss=2.3090e+00 best_ppl=10.06
Epoch 186 - |param|=9.43e+02 |g_param|=5.06e+05 loss_x2y=8.3135e-01 ppl_x2y=2.30 loss_y2x=6.9756e-01 ppl_y2x=2.01 dual_loss=6.3046e-01
Validation X2Y - loss=3.4414e+00 ppl=31.23 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0679e+00 ppl=21.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 187 - |param|=9.44e+02 |g_param|=4.91e+05 loss_x2y=9.1123e-01 ppl_x2y=2.49 loss_y2x=6.9598e-01 ppl_y2x=2.01 dual_loss=8.0297e-01
Validation X2Y - loss=3.4676e+00 ppl=32.06 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0728e+00 ppl=21.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 188 - |param|=9.44e+02 |g_param|=6.33e+05 loss_x2y=7.9712e-01 ppl_x2y=2.22 loss_y2x=6.6371e-01 ppl_y2x=1.94 dual_loss=6.2126e-01
Validation X2Y - loss=3.5294e+00 ppl=34.10 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0478e+00 ppl=21.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 189 - |param|=9.44e+02 |g_param|=7.81e+05 loss_x2y=7.9575e-01 ppl_x2y=2.22 loss_y2x=7.0785e-01 ppl_y2x=2.03 dual_loss=6.5695e-01
Validation X2Y - loss=3.4960e+00 ppl=32.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0805e+00 ppl=21.77 best_loss=2.3090e+00 best_ppl=10.06
Epoch 190 - |param|=9.45e+02 |g_param|=8.30e+05 loss_x2y=7.9502e-01 ppl_x2y=2.21 loss_y2x=6.7451e-01 ppl_y2x=1.96 dual_loss=6.1821e-01
Validation X2Y - loss=3.5193e+00 ppl=33.76 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0423e+00 ppl=20.95 best_loss=2.3090e+00 best_ppl=10.06
Epoch 191 - |param|=9.45e+02 |g_param|=6.08e+05 loss_x2y=7.9357e-01 ppl_x2y=2.21 loss_y2x=6.4127e-01 ppl_y2x=1.90 dual_loss=6.1815e-01
Validation X2Y - loss=3.5610e+00 ppl=35.20 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1028e+00 ppl=22.26 best_loss=2.3090e+00 best_ppl=10.06
Epoch 192 - |param|=9.46e+02 |g_param|=5.20e+05 loss_x2y=8.5056e-01 ppl_x2y=2.34 loss_y2x=6.6620e-01 ppl_y2x=1.95 dual_loss=7.0208e-01
Validation X2Y - loss=3.5523e+00 ppl=34.89 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.0955e+00 ppl=22.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 193 - |param|=9.46e+02 |g_param|=4.99e+05 loss_x2y=7.9975e-01 ppl_x2y=2.22 loss_y2x=6.4745e-01 ppl_y2x=1.91 dual_loss=6.6946e-01
Validation X2Y - loss=3.5282e+00 ppl=34.06 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1093e+00 ppl=22.41 best_loss=2.3090e+00 best_ppl=10.06
Epoch 194 - |param|=9.46e+02 |g_param|=5.37e+05 loss_x2y=7.8077e-01 ppl_x2y=2.18 loss_y2x=6.5232e-01 ppl_y2x=1.92 dual_loss=6.1748e-01
Validation X2Y - loss=3.4569e+00 ppl=31.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1203e+00 ppl=22.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 195 - |param|=9.47e+02 |g_param|=5.30e+05 loss_x2y=8.3270e-01 ppl_x2y=2.30 loss_y2x=7.1305e-01 ppl_y2x=2.04 dual_loss=8.0247e-01
Validation X2Y - loss=3.5245e+00 ppl=33.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1315e+00 ppl=22.91 best_loss=2.3090e+00 best_ppl=10.06
Epoch 196 - |param|=9.47e+02 |g_param|=5.22e+05 loss_x2y=7.7431e-01 ppl_x2y=2.17 loss_y2x=6.2771e-01 ppl_y2x=1.87 dual_loss=6.2541e-01
Validation X2Y - loss=3.5189e+00 ppl=33.75 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1243e+00 ppl=22.74 best_loss=2.3090e+00 best_ppl=10.06
Epoch 197 - |param|=9.48e+02 |g_param|=4.89e+05 loss_x2y=7.6655e-01 ppl_x2y=2.15 loss_y2x=6.3884e-01 ppl_y2x=1.89 dual_loss=6.2476e-01
Validation X2Y - loss=3.5498e+00 ppl=34.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1415e+00 ppl=23.14 best_loss=2.3090e+00 best_ppl=10.06
Epoch 198 - |param|=9.48e+02 |g_param|=5.17e+05 loss_x2y=7.6641e-01 ppl_x2y=2.15 loss_y2x=6.3935e-01 ppl_y2x=1.90 dual_loss=6.4342e-01
Validation X2Y - loss=3.5566e+00 ppl=35.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1034e+00 ppl=22.27 best_loss=2.3090e+00 best_ppl=10.06
Epoch 199 - |param|=9.48e+02 |g_param|=5.10e+05 loss_x2y=8.1565e-01 ppl_x2y=2.26 loss_y2x=6.5784e-01 ppl_y2x=1.93 dual_loss=6.7672e-01
Validation X2Y - loss=3.5537e+00 ppl=34.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1310e+00 ppl=22.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 200 - |param|=9.49e+02 |g_param|=5.14e+05 loss_x2y=7.7929e-01 ppl_x2y=2.18 loss_y2x=6.3475e-01 ppl_y2x=1.89 dual_loss=6.5813e-01
Validation X2Y - loss=3.5385e+00 ppl=34.41 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1106e+00 ppl=22.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 201 - |param|=9.49e+02 |g_param|=5.07e+05 loss_x2y=8.2250e-01 ppl_x2y=2.28 loss_y2x=6.4608e-01 ppl_y2x=1.91 dual_loss=8.0044e-01
Validation X2Y - loss=3.6286e+00 ppl=37.66 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1561e+00 ppl=23.48 best_loss=2.3090e+00 best_ppl=10.06
Epoch 202 - |param|=9.50e+02 |g_param|=5.20e+05 loss_x2y=7.6773e-01 ppl_x2y=2.15 loss_y2x=6.3543e-01 ppl_y2x=1.89 dual_loss=6.9440e-01
Validation X2Y - loss=3.5663e+00 ppl=35.39 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1655e+00 ppl=23.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 203 - |param|=9.50e+02 |g_param|=4.99e+05 loss_x2y=8.0628e-01 ppl_x2y=2.24 loss_y2x=6.1790e-01 ppl_y2x=1.86 dual_loss=7.9444e-01
Validation X2Y - loss=3.6025e+00 ppl=36.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1835e+00 ppl=24.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 204 - |param|=9.50e+02 |g_param|=7.41e+05 loss_x2y=7.4316e-01 ppl_x2y=2.10 loss_y2x=6.1148e-01 ppl_y2x=1.84 dual_loss=6.7605e-01
Validation X2Y - loss=3.5522e+00 ppl=34.89 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2056e+00 ppl=24.67 best_loss=2.3090e+00 best_ppl=10.06
Epoch 205 - |param|=9.51e+02 |g_param|=5.70e+05 loss_x2y=7.4685e-01 ppl_x2y=2.11 loss_y2x=6.4589e-01 ppl_y2x=1.91 dual_loss=7.4536e-01
Validation X2Y - loss=3.5334e+00 ppl=34.24 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1680e+00 ppl=23.76 best_loss=2.3090e+00 best_ppl=10.06
Epoch 206 - |param|=9.51e+02 |g_param|=5.09e+05 loss_x2y=7.5262e-01 ppl_x2y=2.12 loss_y2x=6.0908e-01 ppl_y2x=1.84 dual_loss=7.0208e-01
Validation X2Y - loss=3.5526e+00 ppl=34.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1825e+00 ppl=24.11 best_loss=2.3090e+00 best_ppl=10.06
Epoch 207 - |param|=9.52e+02 |g_param|=5.05e+05 loss_x2y=7.5081e-01 ppl_x2y=2.12 loss_y2x=6.0502e-01 ppl_y2x=1.83 dual_loss=6.9353e-01
Validation X2Y - loss=3.5494e+00 ppl=34.79 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2139e+00 ppl=24.88 best_loss=2.3090e+00 best_ppl=10.06
Epoch 208 - |param|=9.52e+02 |g_param|=5.38e+05 loss_x2y=7.3728e-01 ppl_x2y=2.09 loss_y2x=6.3802e-01 ppl_y2x=1.89 dual_loss=7.0045e-01
Validation X2Y - loss=3.5134e+00 ppl=33.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2129e+00 ppl=24.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 209 - |param|=9.52e+02 |g_param|=5.17e+05 loss_x2y=7.4391e-01 ppl_x2y=2.10 loss_y2x=6.1967e-01 ppl_y2x=1.86 dual_loss=7.1639e-01
Validation X2Y - loss=3.5535e+00 ppl=34.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1996e+00 ppl=24.52 best_loss=2.3090e+00 best_ppl=10.06
Epoch 210 - |param|=9.53e+02 |g_param|=5.30e+05 loss_x2y=7.9655e-01 ppl_x2y=2.22 loss_y2x=6.0192e-01 ppl_y2x=1.83 dual_loss=7.4572e-01
Validation X2Y - loss=3.6017e+00 ppl=36.66 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.1943e+00 ppl=24.39 best_loss=2.3090e+00 best_ppl=10.06
Epoch 211 - |param|=9.53e+02 |g_param|=5.07e+05 loss_x2y=8.0520e-01 ppl_x2y=2.24 loss_y2x=6.1161e-01 ppl_y2x=1.84 dual_loss=9.3226e-01
Validation X2Y - loss=3.5505e+00 ppl=34.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2116e+00 ppl=24.82 best_loss=2.3090e+00 best_ppl=10.06
Epoch 212 - |param|=9.54e+02 |g_param|=5.17e+05 loss_x2y=7.4065e-01 ppl_x2y=2.10 loss_y2x=6.4073e-01 ppl_y2x=1.90 dual_loss=7.9497e-01
Validation X2Y - loss=3.6292e+00 ppl=37.68 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2366e+00 ppl=25.45 best_loss=2.3090e+00 best_ppl=10.06
Epoch 213 - |param|=9.54e+02 |g_param|=4.90e+05 loss_x2y=7.2086e-01 ppl_x2y=2.06 loss_y2x=5.9183e-01 ppl_y2x=1.81 dual_loss=7.0305e-01
Validation X2Y - loss=3.6090e+00 ppl=36.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2258e+00 ppl=25.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 214 - |param|=9.54e+02 |g_param|=5.25e+05 loss_x2y=7.2026e-01 ppl_x2y=2.05 loss_y2x=5.7899e-01 ppl_y2x=1.78 dual_loss=7.1240e-01
Validation X2Y - loss=3.6025e+00 ppl=36.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2240e+00 ppl=25.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 215 - |param|=9.55e+02 |g_param|=4.87e+05 loss_x2y=7.3220e-01 ppl_x2y=2.08 loss_y2x=5.9013e-01 ppl_y2x=1.80 dual_loss=7.3437e-01
Validation X2Y - loss=3.5946e+00 ppl=36.40 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2057e+00 ppl=24.67 best_loss=2.3090e+00 best_ppl=10.06
Epoch 216 - |param|=9.55e+02 |g_param|=5.39e+05 loss_x2y=7.1166e-01 ppl_x2y=2.04 loss_y2x=5.8433e-01 ppl_y2x=1.79 dual_loss=7.4174e-01
Validation X2Y - loss=3.6703e+00 ppl=39.26 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2320e+00 ppl=25.33 best_loss=2.3090e+00 best_ppl=10.06
Epoch 217 - |param|=9.56e+02 |g_param|=5.19e+05 loss_x2y=7.2469e-01 ppl_x2y=2.06 loss_y2x=6.3675e-01 ppl_y2x=1.89 dual_loss=7.6353e-01
Validation X2Y - loss=3.5762e+00 ppl=35.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2433e+00 ppl=25.62 best_loss=2.3090e+00 best_ppl=10.06
Epoch 218 - |param|=9.56e+02 |g_param|=5.19e+05 loss_x2y=7.0512e-01 ppl_x2y=2.02 loss_y2x=5.9249e-01 ppl_y2x=1.81 dual_loss=7.4056e-01
Validation X2Y - loss=3.6635e+00 ppl=39.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2724e+00 ppl=26.38 best_loss=2.3090e+00 best_ppl=10.06
Epoch 219 - |param|=9.56e+02 |g_param|=4.96e+05 loss_x2y=6.9884e-01 ppl_x2y=2.01 loss_y2x=5.6685e-01 ppl_y2x=1.76 dual_loss=7.1511e-01
Validation X2Y - loss=3.6183e+00 ppl=37.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2720e+00 ppl=26.36 best_loss=2.3090e+00 best_ppl=10.06
Epoch 220 - |param|=9.57e+02 |g_param|=5.30e+05 loss_x2y=7.5600e-01 ppl_x2y=2.13 loss_y2x=5.8860e-01 ppl_y2x=1.80 dual_loss=8.4086e-01
Validation X2Y - loss=3.6352e+00 ppl=37.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2513e+00 ppl=25.82 best_loss=2.3090e+00 best_ppl=10.06
Epoch 221 - |param|=9.57e+02 |g_param|=5.10e+05 loss_x2y=7.1770e-01 ppl_x2y=2.05 loss_y2x=5.9861e-01 ppl_y2x=1.82 dual_loss=7.7810e-01
Validation X2Y - loss=3.6267e+00 ppl=37.59 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2713e+00 ppl=26.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 222 - |param|=9.57e+02 |g_param|=5.21e+05 loss_x2y=7.0019e-01 ppl_x2y=2.01 loss_y2x=5.6861e-01 ppl_y2x=1.77 dual_loss=7.3877e-01
Validation X2Y - loss=3.6604e+00 ppl=38.88 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2832e+00 ppl=26.66 best_loss=2.3090e+00 best_ppl=10.06
Epoch 223 - |param|=9.58e+02 |g_param|=5.13e+05 loss_x2y=7.0269e-01 ppl_x2y=2.02 loss_y2x=5.9227e-01 ppl_y2x=1.81 dual_loss=7.9646e-01
Validation X2Y - loss=3.6733e+00 ppl=39.38 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3181e+00 ppl=27.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 224 - |param|=9.58e+02 |g_param|=7.71e+05 loss_x2y=7.1806e-01 ppl_x2y=2.05 loss_y2x=5.4472e-01 ppl_y2x=1.72 dual_loss=8.0912e-01
Validation X2Y - loss=3.7027e+00 ppl=40.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2701e+00 ppl=26.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 225 - |param|=9.59e+02 |g_param|=7.87e+05 loss_x2y=7.0871e-01 ppl_x2y=2.03 loss_y2x=5.5895e-01 ppl_y2x=1.75 dual_loss=7.5882e-01
Validation X2Y - loss=3.6962e+00 ppl=40.29 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3119e+00 ppl=27.44 best_loss=2.3090e+00 best_ppl=10.06
Epoch 226 - |param|=9.59e+02 |g_param|=8.43e+05 loss_x2y=6.9745e-01 ppl_x2y=2.01 loss_y2x=5.5256e-01 ppl_y2x=1.74 dual_loss=7.4601e-01
Validation X2Y - loss=3.7031e+00 ppl=40.57 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2885e+00 ppl=26.80 best_loss=2.3090e+00 best_ppl=10.06
Epoch 227 - |param|=9.59e+02 |g_param|=7.79e+05 loss_x2y=6.6852e-01 ppl_x2y=1.95 loss_y2x=5.6228e-01 ppl_y2x=1.75 dual_loss=7.6009e-01
Validation X2Y - loss=3.7773e+00 ppl=43.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3695e+00 ppl=29.06 best_loss=2.3090e+00 best_ppl=10.06
Epoch 228 - |param|=9.60e+02 |g_param|=8.60e+05 loss_x2y=6.8011e-01 ppl_x2y=1.97 loss_y2x=5.4144e-01 ppl_y2x=1.72 dual_loss=7.0786e-01
Validation X2Y - loss=3.7164e+00 ppl=41.11 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.2766e+00 ppl=26.48 best_loss=2.3090e+00 best_ppl=10.06
Epoch 229 - |param|=9.60e+02 |g_param|=8.52e+05 loss_x2y=7.1862e-01 ppl_x2y=2.05 loss_y2x=6.2081e-01 ppl_y2x=1.86 dual_loss=9.0441e-01
Validation X2Y - loss=3.7305e+00 ppl=41.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3104e+00 ppl=27.40 best_loss=2.3090e+00 best_ppl=10.06
Epoch 230 - |param|=9.60e+02 |g_param|=8.37e+05 loss_x2y=6.9138e-01 ppl_x2y=2.00 loss_y2x=5.3984e-01 ppl_y2x=1.72 dual_loss=7.5714e-01
Validation X2Y - loss=3.7795e+00 ppl=43.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3055e+00 ppl=27.26 best_loss=2.3090e+00 best_ppl=10.06
Epoch 231 - |param|=9.61e+02 |g_param|=8.29e+05 loss_x2y=7.1144e-01 ppl_x2y=2.04 loss_y2x=5.8433e-01 ppl_y2x=1.79 dual_loss=8.3750e-01
Validation X2Y - loss=3.7392e+00 ppl=42.07 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3100e+00 ppl=27.39 best_loss=2.3090e+00 best_ppl=10.06
Epoch 232 - |param|=9.61e+02 |g_param|=8.15e+05 loss_x2y=6.5596e-01 ppl_x2y=1.93 loss_y2x=5.5207e-01 ppl_y2x=1.74 dual_loss=7.7875e-01
Validation X2Y - loss=3.7636e+00 ppl=43.10 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3433e+00 ppl=28.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 233 - |param|=9.62e+02 |g_param|=7.86e+05 loss_x2y=7.4672e-01 ppl_x2y=2.11 loss_y2x=5.7053e-01 ppl_y2x=1.77 dual_loss=1.0488e+00
Validation X2Y - loss=3.7451e+00 ppl=42.31 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3474e+00 ppl=28.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 234 - |param|=9.62e+02 |g_param|=7.64e+05 loss_x2y=6.7794e-01 ppl_x2y=1.97 loss_y2x=5.4370e-01 ppl_y2x=1.72 dual_loss=8.4242e-01
Validation X2Y - loss=3.7916e+00 ppl=44.33 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3201e+00 ppl=27.66 best_loss=2.3090e+00 best_ppl=10.06
Epoch 235 - |param|=9.62e+02 |g_param|=4.14e+05 loss_x2y=6.6550e-01 ppl_x2y=1.95 loss_y2x=5.3919e-01 ppl_y2x=1.71 dual_loss=7.6295e-01
Validation X2Y - loss=3.7850e+00 ppl=44.03 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3246e+00 ppl=27.79 best_loss=2.3090e+00 best_ppl=10.06
Epoch 236 - |param|=9.63e+02 |g_param|=4.42e+05 loss_x2y=6.7264e-01 ppl_x2y=1.96 loss_y2x=5.4288e-01 ppl_y2x=1.72 dual_loss=8.1594e-01
Validation X2Y - loss=3.7700e+00 ppl=43.38 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3325e+00 ppl=28.01 best_loss=2.3090e+00 best_ppl=10.06
Epoch 237 - |param|=9.63e+02 |g_param|=5.01e+05 loss_x2y=6.8376e-01 ppl_x2y=1.98 loss_y2x=6.2386e-01 ppl_y2x=1.87 dual_loss=1.0287e+00
Validation X2Y - loss=3.7454e+00 ppl=42.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3221e+00 ppl=27.72 best_loss=2.3090e+00 best_ppl=10.06
Epoch 238 - |param|=9.63e+02 |g_param|=5.17e+05 loss_x2y=6.5362e-01 ppl_x2y=1.92 loss_y2x=5.4409e-01 ppl_y2x=1.72 dual_loss=7.5941e-01
Validation X2Y - loss=3.8220e+00 ppl=45.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3902e+00 ppl=29.67 best_loss=2.3090e+00 best_ppl=10.06
Epoch 239 - |param|=9.64e+02 |g_param|=4.03e+05 loss_x2y=6.4455e-01 ppl_x2y=1.91 loss_y2x=5.3262e-01 ppl_y2x=1.70 dual_loss=7.9683e-01
Validation X2Y - loss=3.8168e+00 ppl=45.46 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3750e+00 ppl=29.22 best_loss=2.3090e+00 best_ppl=10.06
Epoch 240 - |param|=9.64e+02 |g_param|=4.40e+05 loss_x2y=6.3765e-01 ppl_x2y=1.89 loss_y2x=5.1994e-01 ppl_y2x=1.68 dual_loss=7.8065e-01
Validation X2Y - loss=3.8016e+00 ppl=44.77 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3968e+00 ppl=29.87 best_loss=2.3090e+00 best_ppl=10.06
Epoch 241 - |param|=9.65e+02 |g_param|=3.96e+05 loss_x2y=6.2773e-01 ppl_x2y=1.87 loss_y2x=5.1637e-01 ppl_y2x=1.68 dual_loss=7.8693e-01
Validation X2Y - loss=3.8086e+00 ppl=45.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4047e+00 ppl=30.11 best_loss=2.3090e+00 best_ppl=10.06
Epoch 242 - |param|=9.65e+02 |g_param|=4.07e+05 loss_x2y=6.2362e-01 ppl_x2y=1.87 loss_y2x=5.1323e-01 ppl_y2x=1.67 dual_loss=7.8508e-01
Validation X2Y - loss=3.7924e+00 ppl=44.36 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4020e+00 ppl=30.02 best_loss=2.3090e+00 best_ppl=10.06
Epoch 243 - |param|=9.65e+02 |g_param|=3.95e+05 loss_x2y=6.2897e-01 ppl_x2y=1.88 loss_y2x=5.2042e-01 ppl_y2x=1.68 dual_loss=7.9406e-01
Validation X2Y - loss=3.8037e+00 ppl=44.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3918e+00 ppl=29.72 best_loss=2.3090e+00 best_ppl=10.06
Epoch 244 - |param|=9.66e+02 |g_param|=4.01e+05 loss_x2y=6.4387e-01 ppl_x2y=1.90 loss_y2x=5.3010e-01 ppl_y2x=1.70 dual_loss=8.0516e-01
Validation X2Y - loss=3.8503e+00 ppl=47.01 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3540e+00 ppl=28.62 best_loss=2.3090e+00 best_ppl=10.06
Epoch 245 - |param|=9.66e+02 |g_param|=3.94e+05 loss_x2y=6.2882e-01 ppl_x2y=1.88 loss_y2x=5.2940e-01 ppl_y2x=1.70 dual_loss=8.2149e-01
Validation X2Y - loss=3.8135e+00 ppl=45.31 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4082e+00 ppl=30.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 246 - |param|=9.66e+02 |g_param|=4.13e+05 loss_x2y=6.4348e-01 ppl_x2y=1.90 loss_y2x=5.1691e-01 ppl_y2x=1.68 dual_loss=7.7389e-01
Validation X2Y - loss=3.8412e+00 ppl=46.58 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4409e+00 ppl=31.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 247 - |param|=9.67e+02 |g_param|=3.93e+05 loss_x2y=6.4845e-01 ppl_x2y=1.91 loss_y2x=5.1363e-01 ppl_y2x=1.67 dual_loss=8.5748e-01
Validation X2Y - loss=3.8296e+00 ppl=46.04 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4844e+00 ppl=32.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 248 - |param|=9.67e+02 |g_param|=3.98e+05 loss_x2y=6.2783e-01 ppl_x2y=1.87 loss_y2x=5.0357e-01 ppl_y2x=1.65 dual_loss=8.2634e-01
Validation X2Y - loss=3.7985e+00 ppl=44.64 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.3980e+00 ppl=29.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 249 - |param|=9.68e+02 |g_param|=4.05e+05 loss_x2y=6.4562e-01 ppl_x2y=1.91 loss_y2x=5.2106e-01 ppl_y2x=1.68 dual_loss=8.8105e-01
Validation X2Y - loss=3.7963e+00 ppl=44.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4396e+00 ppl=31.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 250 - |param|=9.68e+02 |g_param|=4.21e+05 loss_x2y=6.4356e-01 ppl_x2y=1.90 loss_y2x=5.4932e-01 ppl_y2x=1.73 dual_loss=9.0165e-01
Validation X2Y - loss=3.8384e+00 ppl=46.45 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4713e+00 ppl=32.18 best_loss=2.3090e+00 best_ppl=10.06
Epoch 251 - |param|=9.68e+02 |g_param|=4.20e+05 loss_x2y=6.6254e-01 ppl_x2y=1.94 loss_y2x=5.9043e-01 ppl_y2x=1.80 dual_loss=1.2111e+00
Validation X2Y - loss=3.7861e+00 ppl=44.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4596e+00 ppl=31.81 best_loss=2.3090e+00 best_ppl=10.06
Epoch 252 - |param|=9.69e+02 |g_param|=4.11e+05 loss_x2y=6.0569e-01 ppl_x2y=1.83 loss_y2x=5.0146e-01 ppl_y2x=1.65 dual_loss=8.1425e-01
Validation X2Y - loss=3.8320e+00 ppl=46.15 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4786e+00 ppl=32.41 best_loss=2.3090e+00 best_ppl=10.06
Epoch 253 - |param|=9.69e+02 |g_param|=3.91e+05 loss_x2y=6.1533e-01 ppl_x2y=1.85 loss_y2x=5.0311e-01 ppl_y2x=1.65 dual_loss=8.1591e-01
Validation X2Y - loss=3.8490e+00 ppl=46.95 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5228e+00 ppl=33.88 best_loss=2.3090e+00 best_ppl=10.06
Epoch 254 - |param|=9.69e+02 |g_param|=4.01e+05 loss_x2y=6.1595e-01 ppl_x2y=1.85 loss_y2x=4.9201e-01 ppl_y2x=1.64 dual_loss=8.2286e-01
Validation X2Y - loss=3.8024e+00 ppl=44.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5198e+00 ppl=33.78 best_loss=2.3090e+00 best_ppl=10.06
Epoch 255 - |param|=9.70e+02 |g_param|=3.97e+05 loss_x2y=5.9670e-01 ppl_x2y=1.82 loss_y2x=4.9380e-01 ppl_y2x=1.64 dual_loss=8.1708e-01
Validation X2Y - loss=3.8643e+00 ppl=47.67 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4682e+00 ppl=32.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 256 - |param|=9.70e+02 |g_param|=4.19e+05 loss_x2y=6.3216e-01 ppl_x2y=1.88 loss_y2x=4.9977e-01 ppl_y2x=1.65 dual_loss=9.0307e-01
Validation X2Y - loss=3.8542e+00 ppl=47.19 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4941e+00 ppl=32.92 best_loss=2.3090e+00 best_ppl=10.06
Epoch 257 - |param|=9.70e+02 |g_param|=2.94e+05 loss_x2y=5.8589e-01 ppl_x2y=1.80 loss_y2x=5.2225e-01 ppl_y2x=1.69 dual_loss=8.6537e-01
Validation X2Y - loss=3.8365e+00 ppl=46.36 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4828e+00 ppl=32.55 best_loss=2.3090e+00 best_ppl=10.06
Epoch 258 - |param|=9.71e+02 |g_param|=2.55e+05 loss_x2y=5.9917e-01 ppl_x2y=1.82 loss_y2x=4.8780e-01 ppl_y2x=1.63 dual_loss=8.2064e-01
Validation X2Y - loss=3.8695e+00 ppl=47.92 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5094e+00 ppl=33.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 259 - |param|=9.71e+02 |g_param|=2.46e+05 loss_x2y=6.1151e-01 ppl_x2y=1.84 loss_y2x=4.7405e-01 ppl_y2x=1.61 dual_loss=8.4926e-01
Validation X2Y - loss=3.8485e+00 ppl=46.92 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5333e+00 ppl=34.24 best_loss=2.3090e+00 best_ppl=10.06
Epoch 260 - |param|=9.72e+02 |g_param|=2.56e+05 loss_x2y=5.8179e-01 ppl_x2y=1.79 loss_y2x=4.7672e-01 ppl_y2x=1.61 dual_loss=7.7898e-01
Validation X2Y - loss=3.8652e+00 ppl=47.71 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4962e+00 ppl=32.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 261 - |param|=9.72e+02 |g_param|=2.55e+05 loss_x2y=6.0652e-01 ppl_x2y=1.83 loss_y2x=4.9594e-01 ppl_y2x=1.64 dual_loss=8.5186e-01
Validation X2Y - loss=3.8682e+00 ppl=47.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5189e+00 ppl=33.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 262 - |param|=9.72e+02 |g_param|=2.71e+05 loss_x2y=6.2698e-01 ppl_x2y=1.87 loss_y2x=5.1689e-01 ppl_y2x=1.68 dual_loss=9.8501e-01
Validation X2Y - loss=3.9065e+00 ppl=49.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5264e+00 ppl=34.00 best_loss=2.3090e+00 best_ppl=10.06
Epoch 263 - |param|=9.73e+02 |g_param|=2.51e+05 loss_x2y=5.9593e-01 ppl_x2y=1.81 loss_y2x=4.8181e-01 ppl_y2x=1.62 dual_loss=8.7763e-01
Validation X2Y - loss=3.8999e+00 ppl=49.40 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5155e+00 ppl=33.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 264 - |param|=9.73e+02 |g_param|=2.65e+05 loss_x2y=6.0861e-01 ppl_x2y=1.84 loss_y2x=4.8927e-01 ppl_y2x=1.63 dual_loss=8.8417e-01
Validation X2Y - loss=3.9382e+00 ppl=51.33 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5141e+00 ppl=33.59 best_loss=2.3090e+00 best_ppl=10.06
Epoch 265 - |param|=9.73e+02 |g_param|=2.54e+05 loss_x2y=6.7277e-01 ppl_x2y=1.96 loss_y2x=5.0974e-01 ppl_y2x=1.66 dual_loss=1.0742e+00
Validation X2Y - loss=3.9306e+00 ppl=50.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5022e+00 ppl=33.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 266 - |param|=9.74e+02 |g_param|=2.59e+05 loss_x2y=5.9817e-01 ppl_x2y=1.82 loss_y2x=4.9889e-01 ppl_y2x=1.65 dual_loss=9.3218e-01
Validation X2Y - loss=3.9561e+00 ppl=52.25 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5162e+00 ppl=33.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 267 - |param|=9.74e+02 |g_param|=2.52e+05 loss_x2y=6.2507e-01 ppl_x2y=1.87 loss_y2x=5.0280e-01 ppl_y2x=1.65 dual_loss=9.8941e-01
Validation X2Y - loss=3.9535e+00 ppl=52.12 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5631e+00 ppl=35.27 best_loss=2.3090e+00 best_ppl=10.06
Epoch 268 - |param|=9.74e+02 |g_param|=3.96e+05 loss_x2y=5.9785e-01 ppl_x2y=1.82 loss_y2x=4.7306e-01 ppl_y2x=1.60 dual_loss=8.8833e-01
Validation X2Y - loss=3.9303e+00 ppl=50.92 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5602e+00 ppl=35.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 269 - |param|=9.75e+02 |g_param|=3.82e+05 loss_x2y=6.7759e-01 ppl_x2y=1.97 loss_y2x=4.8833e-01 ppl_y2x=1.63 dual_loss=1.1916e+00
Validation X2Y - loss=3.9191e+00 ppl=50.35 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5442e+00 ppl=34.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 270 - |param|=9.75e+02 |g_param|=4.08e+05 loss_x2y=5.7067e-01 ppl_x2y=1.77 loss_y2x=4.7376e-01 ppl_y2x=1.61 dual_loss=8.8736e-01
Validation X2Y - loss=3.9643e+00 ppl=52.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5467e+00 ppl=34.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 271 - |param|=9.76e+02 |g_param|=4.20e+05 loss_x2y=6.1364e-01 ppl_x2y=1.85 loss_y2x=5.4475e-01 ppl_y2x=1.72 dual_loss=1.2496e+00
Validation X2Y - loss=3.9174e+00 ppl=50.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5369e+00 ppl=34.36 best_loss=2.3090e+00 best_ppl=10.06
Epoch 272 - |param|=9.76e+02 |g_param|=3.92e+05 loss_x2y=5.7484e-01 ppl_x2y=1.78 loss_y2x=4.6224e-01 ppl_y2x=1.59 dual_loss=8.9125e-01
Validation X2Y - loss=3.9686e+00 ppl=52.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5084e+00 ppl=33.39 best_loss=2.3090e+00 best_ppl=10.06
Epoch 273 - |param|=9.76e+02 |g_param|=4.09e+05 loss_x2y=6.4997e-01 ppl_x2y=1.92 loss_y2x=4.8363e-01 ppl_y2x=1.62 dual_loss=1.0594e+00
Validation X2Y - loss=3.9506e+00 ppl=51.97 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.4687e+00 ppl=32.09 best_loss=2.3090e+00 best_ppl=10.06
Epoch 274 - |param|=9.77e+02 |g_param|=4.13e+05 loss_x2y=5.9777e-01 ppl_x2y=1.82 loss_y2x=4.7371e-01 ppl_y2x=1.61 dual_loss=9.1185e-01
Validation X2Y - loss=3.9651e+00 ppl=52.73 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5287e+00 ppl=34.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 275 - |param|=9.77e+02 |g_param|=3.90e+05 loss_x2y=5.9570e-01 ppl_x2y=1.81 loss_y2x=4.6773e-01 ppl_y2x=1.60 dual_loss=9.3989e-01
Validation X2Y - loss=3.9506e+00 ppl=51.97 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5111e+00 ppl=33.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 276 - |param|=9.77e+02 |g_param|=4.11e+05 loss_x2y=5.7138e-01 ppl_x2y=1.77 loss_y2x=4.6347e-01 ppl_y2x=1.59 dual_loss=8.9226e-01
Validation X2Y - loss=4.0009e+00 ppl=54.65 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5270e+00 ppl=34.02 best_loss=2.3090e+00 best_ppl=10.06
Epoch 277 - |param|=9.78e+02 |g_param|=3.88e+05 loss_x2y=5.7480e-01 ppl_x2y=1.78 loss_y2x=4.4838e-01 ppl_y2x=1.57 dual_loss=8.9245e-01
Validation X2Y - loss=3.9652e+00 ppl=52.73 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5574e+00 ppl=35.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 278 - |param|=9.78e+02 |g_param|=4.03e+05 loss_x2y=5.6815e-01 ppl_x2y=1.76 loss_y2x=4.7177e-01 ppl_y2x=1.60 dual_loss=8.9752e-01
Validation X2Y - loss=3.9670e+00 ppl=52.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5542e+00 ppl=34.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 279 - |param|=9.78e+02 |g_param|=4.08e+05 loss_x2y=5.8468e-01 ppl_x2y=1.79 loss_y2x=4.9068e-01 ppl_y2x=1.63 dual_loss=9.8748e-01
Validation X2Y - loss=3.9959e+00 ppl=54.37 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5767e+00 ppl=35.76 best_loss=2.3090e+00 best_ppl=10.06
Epoch 280 - |param|=9.79e+02 |g_param|=3.89e+05 loss_x2y=5.6540e-01 ppl_x2y=1.76 loss_y2x=4.5268e-01 ppl_y2x=1.57 dual_loss=8.9478e-01
Validation X2Y - loss=3.9728e+00 ppl=53.13 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5685e+00 ppl=35.46 best_loss=2.3090e+00 best_ppl=10.06
Epoch 281 - |param|=9.79e+02 |g_param|=3.92e+05 loss_x2y=5.4455e-01 ppl_x2y=1.72 loss_y2x=4.5505e-01 ppl_y2x=1.58 dual_loss=9.1370e-01
Validation X2Y - loss=4.0552e+00 ppl=57.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5685e+00 ppl=35.46 best_loss=2.3090e+00 best_ppl=10.06
Epoch 282 - |param|=9.79e+02 |g_param|=3.89e+05 loss_x2y=5.4472e-01 ppl_x2y=1.72 loss_y2x=4.3250e-01 ppl_y2x=1.54 dual_loss=8.4351e-01
Validation X2Y - loss=4.0134e+00 ppl=55.34 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6116e+00 ppl=37.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 283 - |param|=9.80e+02 |g_param|=3.91e+05 loss_x2y=5.5075e-01 ppl_x2y=1.73 loss_y2x=4.4664e-01 ppl_y2x=1.56 dual_loss=9.1963e-01
Validation X2Y - loss=4.0218e+00 ppl=55.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5809e+00 ppl=35.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 284 - |param|=9.80e+02 |g_param|=4.21e+05 loss_x2y=5.9786e-01 ppl_x2y=1.82 loss_y2x=4.6211e-01 ppl_y2x=1.59 dual_loss=1.0426e+00
Validation X2Y - loss=3.9838e+00 ppl=53.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6099e+00 ppl=36.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 285 - |param|=9.80e+02 |g_param|=4.09e+05 loss_x2y=5.6992e-01 ppl_x2y=1.77 loss_y2x=5.0256e-01 ppl_y2x=1.65 dual_loss=9.8470e-01
Validation X2Y - loss=3.9839e+00 ppl=53.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5934e+00 ppl=36.36 best_loss=2.3090e+00 best_ppl=10.06
Epoch 286 - |param|=9.81e+02 |g_param|=4.13e+05 loss_x2y=5.3061e-01 ppl_x2y=1.70 loss_y2x=4.3569e-01 ppl_y2x=1.55 dual_loss=8.7743e-01
Validation X2Y - loss=3.9816e+00 ppl=53.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6087e+00 ppl=36.92 best_loss=2.3090e+00 best_ppl=10.06
Epoch 287 - |param|=9.81e+02 |g_param|=4.13e+05 loss_x2y=5.6630e-01 ppl_x2y=1.76 loss_y2x=4.5125e-01 ppl_y2x=1.57 dual_loss=9.6688e-01
Validation X2Y - loss=3.9733e+00 ppl=53.16 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6103e+00 ppl=36.98 best_loss=2.3090e+00 best_ppl=10.06
Epoch 288 - |param|=9.82e+02 |g_param|=3.97e+05 loss_x2y=5.3951e-01 ppl_x2y=1.72 loss_y2x=4.4129e-01 ppl_y2x=1.55 dual_loss=8.9110e-01
Validation X2Y - loss=4.0354e+00 ppl=56.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5945e+00 ppl=36.40 best_loss=2.3090e+00 best_ppl=10.06
Epoch 289 - |param|=9.82e+02 |g_param|=3.83e+05 loss_x2y=5.3861e-01 ppl_x2y=1.71 loss_y2x=4.4917e-01 ppl_y2x=1.57 dual_loss=9.1469e-01
Validation X2Y - loss=4.0002e+00 ppl=54.61 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5873e+00 ppl=36.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 290 - |param|=9.82e+02 |g_param|=4.95e+05 loss_x2y=5.5200e-01 ppl_x2y=1.74 loss_y2x=4.6913e-01 ppl_y2x=1.60 dual_loss=1.0224e+00
Validation X2Y - loss=4.0105e+00 ppl=55.17 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5971e+00 ppl=36.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 291 - |param|=9.83e+02 |g_param|=4.68e+05 loss_x2y=5.5793e-01 ppl_x2y=1.75 loss_y2x=4.8422e-01 ppl_y2x=1.62 dual_loss=1.0579e+00
Validation X2Y - loss=4.0231e+00 ppl=55.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5755e+00 ppl=35.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 292 - |param|=9.83e+02 |g_param|=4.24e+05 loss_x2y=5.3980e-01 ppl_x2y=1.72 loss_y2x=4.5167e-01 ppl_y2x=1.57 dual_loss=9.4726e-01
Validation X2Y - loss=3.9605e+00 ppl=52.48 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5696e+00 ppl=35.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 293 - |param|=9.83e+02 |g_param|=3.78e+05 loss_x2y=5.3854e-01 ppl_x2y=1.71 loss_y2x=4.3703e-01 ppl_y2x=1.55 dual_loss=9.2608e-01
Validation X2Y - loss=3.9840e+00 ppl=53.73 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.5831e+00 ppl=35.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 294 - |param|=9.84e+02 |g_param|=4.00e+05 loss_x2y=5.3490e-01 ppl_x2y=1.71 loss_y2x=4.2781e-01 ppl_y2x=1.53 dual_loss=8.8447e-01
Validation X2Y - loss=4.0174e+00 ppl=55.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6229e+00 ppl=37.45 best_loss=2.3090e+00 best_ppl=10.06
Epoch 295 - |param|=9.84e+02 |g_param|=4.05e+05 loss_x2y=6.3269e-01 ppl_x2y=1.88 loss_y2x=4.7612e-01 ppl_y2x=1.61 dual_loss=1.2844e+00
Validation X2Y - loss=4.0460e+00 ppl=57.17 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6333e+00 ppl=37.84 best_loss=2.3090e+00 best_ppl=10.06
Epoch 296 - |param|=9.84e+02 |g_param|=3.89e+05 loss_x2y=5.3512e-01 ppl_x2y=1.71 loss_y2x=4.4111e-01 ppl_y2x=1.55 dual_loss=9.5625e-01
Validation X2Y - loss=4.0612e+00 ppl=58.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6647e+00 ppl=39.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 297 - |param|=9.85e+02 |g_param|=4.01e+05 loss_x2y=5.3447e-01 ppl_x2y=1.71 loss_y2x=4.6024e-01 ppl_y2x=1.58 dual_loss=9.9297e-01
Validation X2Y - loss=4.0604e+00 ppl=58.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6547e+00 ppl=38.66 best_loss=2.3090e+00 best_ppl=10.06
Epoch 298 - |param|=9.85e+02 |g_param|=3.98e+05 loss_x2y=5.2683e-01 ppl_x2y=1.69 loss_y2x=4.3679e-01 ppl_y2x=1.55 dual_loss=9.5519e-01
Validation X2Y - loss=4.0530e+00 ppl=57.57 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6663e+00 ppl=39.11 best_loss=2.3090e+00 best_ppl=10.06
Epoch 299 - |param|=9.85e+02 |g_param|=3.78e+05 loss_x2y=5.2722e-01 ppl_x2y=1.69 loss_y2x=4.2262e-01 ppl_y2x=1.53 dual_loss=9.4947e-01
Validation X2Y - loss=4.0407e+00 ppl=56.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6562e+00 ppl=38.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 300 - |param|=9.86e+02 |g_param|=6.24e+05 loss_x2y=5.3510e-01 ppl_x2y=1.71 loss_y2x=4.3208e-01 ppl_y2x=1.54 dual_loss=9.6212e-01
Validation X2Y - loss=4.0502e+00 ppl=57.41 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6636e+00 ppl=39.00 best_loss=2.3090e+00 best_ppl=10.06
Epoch 301 - |param|=9.86e+02 |g_param|=7.04e+05 loss_x2y=5.2646e-01 ppl_x2y=1.69 loss_y2x=4.2853e-01 ppl_y2x=1.54 dual_loss=9.0210e-01
Validation X2Y - loss=4.0625e+00 ppl=58.12 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6373e+00 ppl=37.99 best_loss=2.3090e+00 best_ppl=10.06
Epoch 302 - |param|=9.86e+02 |g_param|=7.44e+05 loss_x2y=6.3249e-01 ppl_x2y=1.88 loss_y2x=4.5510e-01 ppl_y2x=1.58 dual_loss=1.2115e+00
Validation X2Y - loss=4.0148e+00 ppl=55.41 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6631e+00 ppl=38.98 best_loss=2.3090e+00 best_ppl=10.06
Epoch 303 - |param|=9.87e+02 |g_param|=4.35e+05 loss_x2y=5.1605e-01 ppl_x2y=1.68 loss_y2x=4.2358e-01 ppl_y2x=1.53 dual_loss=9.6866e-01
Validation X2Y - loss=4.0759e+00 ppl=58.90 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6871e+00 ppl=39.93 best_loss=2.3090e+00 best_ppl=10.06
Epoch 304 - |param|=9.87e+02 |g_param|=4.01e+05 loss_x2y=5.9485e-01 ppl_x2y=1.81 loss_y2x=4.4572e-01 ppl_y2x=1.56 dual_loss=1.2121e+00
Validation X2Y - loss=4.0623e+00 ppl=58.11 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6598e+00 ppl=38.86 best_loss=2.3090e+00 best_ppl=10.06
Epoch 305 - |param|=9.87e+02 |g_param|=3.78e+05 loss_x2y=5.4488e-01 ppl_x2y=1.72 loss_y2x=4.3017e-01 ppl_y2x=1.54 dual_loss=1.0323e+00
Validation X2Y - loss=4.0567e+00 ppl=57.79 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6249e+00 ppl=37.52 best_loss=2.3090e+00 best_ppl=10.06
Epoch 306 - |param|=9.88e+02 |g_param|=3.94e+05 loss_x2y=5.0012e-01 ppl_x2y=1.65 loss_y2x=4.2506e-01 ppl_y2x=1.53 dual_loss=9.4735e-01
Validation X2Y - loss=4.0647e+00 ppl=58.25 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6202e+00 ppl=37.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 307 - |param|=9.88e+02 |g_param|=3.75e+05 loss_x2y=5.3575e-01 ppl_x2y=1.71 loss_y2x=4.2485e-01 ppl_y2x=1.53 dual_loss=1.0611e+00
Validation X2Y - loss=4.0900e+00 ppl=59.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6915e+00 ppl=40.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 308 - |param|=9.88e+02 |g_param|=3.88e+05 loss_x2y=5.2720e-01 ppl_x2y=1.69 loss_y2x=4.2819e-01 ppl_y2x=1.53 dual_loss=1.0140e+00
Validation X2Y - loss=4.0814e+00 ppl=59.23 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6800e+00 ppl=39.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 309 - |param|=9.89e+02 |g_param|=3.80e+05 loss_x2y=5.4094e-01 ppl_x2y=1.72 loss_y2x=4.1310e-01 ppl_y2x=1.51 dual_loss=1.0085e+00
Validation X2Y - loss=4.0932e+00 ppl=59.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6505e+00 ppl=38.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 310 - |param|=9.89e+02 |g_param|=3.91e+05 loss_x2y=5.2117e-01 ppl_x2y=1.68 loss_y2x=4.2269e-01 ppl_y2x=1.53 dual_loss=9.8816e-01
Validation X2Y - loss=4.1164e+00 ppl=61.34 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6971e+00 ppl=40.33 best_loss=2.3090e+00 best_ppl=10.06
Epoch 311 - |param|=9.89e+02 |g_param|=3.76e+05 loss_x2y=5.5426e-01 ppl_x2y=1.74 loss_y2x=4.5524e-01 ppl_y2x=1.58 dual_loss=1.1485e+00
Validation X2Y - loss=4.1082e+00 ppl=60.84 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6999e+00 ppl=40.45 best_loss=2.3090e+00 best_ppl=10.06
Epoch 312 - |param|=9.90e+02 |g_param|=4.01e+05 loss_x2y=5.2302e-01 ppl_x2y=1.69 loss_y2x=4.0685e-01 ppl_y2x=1.50 dual_loss=9.8837e-01
Validation X2Y - loss=4.1032e+00 ppl=60.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6855e+00 ppl=39.86 best_loss=2.3090e+00 best_ppl=10.06
Epoch 313 - |param|=9.90e+02 |g_param|=4.13e+05 loss_x2y=5.3614e-01 ppl_x2y=1.71 loss_y2x=4.7312e-01 ppl_y2x=1.60 dual_loss=1.1319e+00
Validation X2Y - loss=4.0889e+00 ppl=59.67 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6910e+00 ppl=40.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 314 - |param|=9.91e+02 |g_param|=3.89e+05 loss_x2y=5.8013e-01 ppl_x2y=1.79 loss_y2x=4.2342e-01 ppl_y2x=1.53 dual_loss=1.2681e+00
Validation X2Y - loss=4.0952e+00 ppl=60.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6838e+00 ppl=39.80 best_loss=2.3090e+00 best_ppl=10.06
Epoch 315 - |param|=9.91e+02 |g_param|=3.83e+05 loss_x2y=4.9789e-01 ppl_x2y=1.65 loss_y2x=4.1541e-01 ppl_y2x=1.51 dual_loss=1.0065e+00
Validation X2Y - loss=4.1091e+00 ppl=60.89 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6911e+00 ppl=40.09 best_loss=2.3090e+00 best_ppl=10.06
Epoch 316 - |param|=9.91e+02 |g_param|=4.09e+05 loss_x2y=5.4207e-01 ppl_x2y=1.72 loss_y2x=4.6249e-01 ppl_y2x=1.59 dual_loss=1.1930e+00
Validation X2Y - loss=4.1490e+00 ppl=63.37 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.6471e+00 ppl=38.36 best_loss=2.3090e+00 best_ppl=10.06
Epoch 317 - |param|=9.92e+02 |g_param|=3.93e+05 loss_x2y=5.1368e-01 ppl_x2y=1.67 loss_y2x=3.9949e-01 ppl_y2x=1.49 dual_loss=1.0033e+00
Validation X2Y - loss=4.2005e+00 ppl=66.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7324e+00 ppl=41.78 best_loss=2.3090e+00 best_ppl=10.06
Epoch 318 - |param|=9.92e+02 |g_param|=4.22e+05 loss_x2y=5.2455e-01 ppl_x2y=1.69 loss_y2x=4.5411e-01 ppl_y2x=1.57 dual_loss=1.1419e+00
Validation X2Y - loss=4.1721e+00 ppl=64.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7098e+00 ppl=40.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 319 - |param|=9.92e+02 |g_param|=3.90e+05 loss_x2y=5.0804e-01 ppl_x2y=1.66 loss_y2x=4.0600e-01 ppl_y2x=1.50 dual_loss=9.6490e-01
Validation X2Y - loss=4.1724e+00 ppl=64.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7085e+00 ppl=40.79 best_loss=2.3090e+00 best_ppl=10.06
Epoch 320 - |param|=9.93e+02 |g_param|=3.69e+05 loss_x2y=4.8191e-01 ppl_x2y=1.62 loss_y2x=3.9315e-01 ppl_y2x=1.48 dual_loss=9.6903e-01
Validation X2Y - loss=4.1428e+00 ppl=62.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7305e+00 ppl=41.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 321 - |param|=9.93e+02 |g_param|=3.63e+05 loss_x2y=4.8522e-01 ppl_x2y=1.62 loss_y2x=3.9735e-01 ppl_y2x=1.49 dual_loss=9.6179e-01
Validation X2Y - loss=4.1873e+00 ppl=65.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7578e+00 ppl=42.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 322 - |param|=9.93e+02 |g_param|=3.99e+05 loss_x2y=5.0080e-01 ppl_x2y=1.65 loss_y2x=4.1791e-01 ppl_y2x=1.52 dual_loss=1.0637e+00
Validation X2Y - loss=4.1771e+00 ppl=65.18 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7794e+00 ppl=43.79 best_loss=2.3090e+00 best_ppl=10.06
Epoch 323 - |param|=9.94e+02 |g_param|=4.12e+05 loss_x2y=5.2899e-01 ppl_x2y=1.70 loss_y2x=4.6465e-01 ppl_y2x=1.59 dual_loss=1.2796e+00
Validation X2Y - loss=4.1548e+00 ppl=63.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7902e+00 ppl=44.27 best_loss=2.3090e+00 best_ppl=10.06
Epoch 324 - |param|=9.94e+02 |g_param|=4.64e+05 loss_x2y=5.0854e-01 ppl_x2y=1.66 loss_y2x=3.9888e-01 ppl_y2x=1.49 dual_loss=1.0209e+00
Validation X2Y - loss=4.1357e+00 ppl=62.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7630e+00 ppl=43.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 325 - |param|=9.94e+02 |g_param|=4.94e+05 loss_x2y=5.1682e-01 ppl_x2y=1.68 loss_y2x=4.0992e-01 ppl_y2x=1.51 dual_loss=1.0686e+00
Validation X2Y - loss=4.1712e+00 ppl=64.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7437e+00 ppl=42.25 best_loss=2.3090e+00 best_ppl=10.06
Epoch 326 - |param|=9.95e+02 |g_param|=5.18e+05 loss_x2y=5.1225e-01 ppl_x2y=1.67 loss_y2x=4.2127e-01 ppl_y2x=1.52 dual_loss=1.0967e+00
Validation X2Y - loss=4.1575e+00 ppl=63.91 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7351e+00 ppl=41.89 best_loss=2.3090e+00 best_ppl=10.06
Epoch 327 - |param|=9.95e+02 |g_param|=3.94e+05 loss_x2y=5.3933e-01 ppl_x2y=1.71 loss_y2x=4.3194e-01 ppl_y2x=1.54 dual_loss=1.2739e+00
Validation X2Y - loss=4.2461e+00 ppl=69.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7977e+00 ppl=44.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 328 - |param|=9.95e+02 |g_param|=3.93e+05 loss_x2y=4.9002e-01 ppl_x2y=1.63 loss_y2x=3.9468e-01 ppl_y2x=1.48 dual_loss=1.0236e+00
Validation X2Y - loss=4.2055e+00 ppl=67.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7830e+00 ppl=43.95 best_loss=2.3090e+00 best_ppl=10.06
Epoch 329 - |param|=9.96e+02 |g_param|=3.81e+05 loss_x2y=4.8346e-01 ppl_x2y=1.62 loss_y2x=3.9405e-01 ppl_y2x=1.48 dual_loss=9.8070e-01
Validation X2Y - loss=4.2028e+00 ppl=66.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7876e+00 ppl=44.15 best_loss=2.3090e+00 best_ppl=10.06
Epoch 330 - |param|=9.96e+02 |g_param|=4.10e+05 loss_x2y=4.8227e-01 ppl_x2y=1.62 loss_y2x=3.9062e-01 ppl_y2x=1.48 dual_loss=9.7494e-01
Validation X2Y - loss=4.2192e+00 ppl=67.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7489e+00 ppl=42.47 best_loss=2.3090e+00 best_ppl=10.06
Epoch 331 - |param|=9.96e+02 |g_param|=3.89e+05 loss_x2y=4.9760e-01 ppl_x2y=1.64 loss_y2x=3.9763e-01 ppl_y2x=1.49 dual_loss=1.0667e+00
Validation X2Y - loss=4.1478e+00 ppl=63.30 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7810e+00 ppl=43.86 best_loss=2.3090e+00 best_ppl=10.06
Epoch 332 - |param|=9.97e+02 |g_param|=3.99e+05 loss_x2y=4.9819e-01 ppl_x2y=1.65 loss_y2x=4.0298e-01 ppl_y2x=1.50 dual_loss=1.0598e+00
Validation X2Y - loss=4.1482e+00 ppl=63.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7612e+00 ppl=43.00 best_loss=2.3090e+00 best_ppl=10.06
Epoch 333 - |param|=9.97e+02 |g_param|=3.83e+05 loss_x2y=4.8694e-01 ppl_x2y=1.63 loss_y2x=3.9078e-01 ppl_y2x=1.48 dual_loss=1.0479e+00
Validation X2Y - loss=4.1662e+00 ppl=64.47 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7697e+00 ppl=43.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 334 - |param|=9.97e+02 |g_param|=4.01e+05 loss_x2y=4.8790e-01 ppl_x2y=1.63 loss_y2x=3.9388e-01 ppl_y2x=1.48 dual_loss=1.0459e+00
Validation X2Y - loss=4.2048e+00 ppl=67.01 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7742e+00 ppl=43.56 best_loss=2.3090e+00 best_ppl=10.06
Epoch 335 - |param|=9.98e+02 |g_param|=3.72e+05 loss_x2y=4.9320e-01 ppl_x2y=1.64 loss_y2x=3.9449e-01 ppl_y2x=1.48 dual_loss=1.0639e+00
Validation X2Y - loss=4.1699e+00 ppl=64.71 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8062e+00 ppl=44.98 best_loss=2.3090e+00 best_ppl=10.06
Epoch 336 - |param|=9.98e+02 |g_param|=3.85e+05 loss_x2y=4.7504e-01 ppl_x2y=1.61 loss_y2x=3.8905e-01 ppl_y2x=1.48 dual_loss=9.9112e-01
Validation X2Y - loss=4.1603e+00 ppl=64.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7828e+00 ppl=43.94 best_loss=2.3090e+00 best_ppl=10.06
Epoch 337 - |param|=9.98e+02 |g_param|=3.79e+05 loss_x2y=4.8769e-01 ppl_x2y=1.63 loss_y2x=4.0104e-01 ppl_y2x=1.49 dual_loss=1.1467e+00
Validation X2Y - loss=4.1579e+00 ppl=63.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8142e+00 ppl=45.34 best_loss=2.3090e+00 best_ppl=10.06
Epoch 338 - |param|=9.99e+02 |g_param|=4.05e+05 loss_x2y=4.9816e-01 ppl_x2y=1.65 loss_y2x=4.3151e-01 ppl_y2x=1.54 dual_loss=1.3001e+00
Validation X2Y - loss=4.2170e+00 ppl=67.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8204e+00 ppl=45.62 best_loss=2.3090e+00 best_ppl=10.06
Epoch 339 - |param|=9.99e+02 |g_param|=3.87e+05 loss_x2y=4.9469e-01 ppl_x2y=1.64 loss_y2x=4.1849e-01 ppl_y2x=1.52 dual_loss=1.2458e+00
Validation X2Y - loss=4.2466e+00 ppl=69.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8073e+00 ppl=45.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 340 - |param|=9.99e+02 |g_param|=4.29e+05 loss_x2y=4.6967e-01 ppl_x2y=1.60 loss_y2x=3.8409e-01 ppl_y2x=1.47 dual_loss=1.0151e+00
Validation X2Y - loss=4.1785e+00 ppl=65.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7921e+00 ppl=44.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 341 - |param|=1.00e+03 |g_param|=3.79e+05 loss_x2y=4.8162e-01 ppl_x2y=1.62 loss_y2x=3.8381e-01 ppl_y2x=1.47 dual_loss=1.0766e+00
Validation X2Y - loss=4.1875e+00 ppl=65.86 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8149e+00 ppl=45.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 342 - |param|=1.00e+03 |g_param|=3.82e+05 loss_x2y=4.9135e-01 ppl_x2y=1.63 loss_y2x=3.9360e-01 ppl_y2x=1.48 dual_loss=1.1559e+00
Validation X2Y - loss=4.2186e+00 ppl=67.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8138e+00 ppl=45.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 343 - |param|=1.00e+03 |g_param|=3.85e+05 loss_x2y=5.2154e-01 ppl_x2y=1.68 loss_y2x=4.0758e-01 ppl_y2x=1.50 dual_loss=1.1400e+00
Validation X2Y - loss=4.2114e+00 ppl=67.45 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7984e+00 ppl=44.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 344 - |param|=1.00e+03 |g_param|=4.06e+05 loss_x2y=5.8259e-01 ppl_x2y=1.79 loss_y2x=4.2781e-01 ppl_y2x=1.53 dual_loss=1.5706e+00
Validation X2Y - loss=4.1912e+00 ppl=66.10 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8128e+00 ppl=45.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 345 - |param|=1.00e+03 |g_param|=3.95e+05 loss_x2y=4.8005e-01 ppl_x2y=1.62 loss_y2x=3.9185e-01 ppl_y2x=1.48 dual_loss=1.0957e+00
Validation X2Y - loss=4.2014e+00 ppl=66.78 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8420e+00 ppl=46.62 best_loss=2.3090e+00 best_ppl=10.06
Epoch 346 - |param|=1.00e+03 |g_param|=3.73e+05 loss_x2y=4.8940e-01 ppl_x2y=1.63 loss_y2x=4.0034e-01 ppl_y2x=1.49 dual_loss=1.2012e+00
Validation X2Y - loss=4.2099e+00 ppl=67.35 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8224e+00 ppl=45.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 347 - |param|=1.00e+03 |g_param|=3.89e+05 loss_x2y=4.7989e-01 ppl_x2y=1.62 loss_y2x=3.9152e-01 ppl_y2x=1.48 dual_loss=1.1240e+00
Validation X2Y - loss=4.2871e+00 ppl=72.75 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8023e+00 ppl=44.81 best_loss=2.3090e+00 best_ppl=10.06
Epoch 348 - |param|=1.00e+03 |g_param|=3.82e+05 loss_x2y=4.6907e-01 ppl_x2y=1.60 loss_y2x=3.6389e-01 ppl_y2x=1.44 dual_loss=9.8594e-01
Validation X2Y - loss=4.2272e+00 ppl=68.52 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7990e+00 ppl=44.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 349 - |param|=1.00e+03 |g_param|=4.13e+05 loss_x2y=5.0443e-01 ppl_x2y=1.66 loss_y2x=4.6923e-01 ppl_y2x=1.60 dual_loss=1.5782e+00
Validation X2Y - loss=4.2407e+00 ppl=69.46 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8138e+00 ppl=45.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 350 - |param|=1.00e+03 |g_param|=3.85e+05 loss_x2y=4.7963e-01 ppl_x2y=1.62 loss_y2x=4.0184e-01 ppl_y2x=1.49 dual_loss=1.2026e+00
Validation X2Y - loss=4.2956e+00 ppl=73.37 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.7850e+00 ppl=44.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 351 - |param|=1.00e+03 |g_param|=3.63e+05 loss_x2y=4.7351e-01 ppl_x2y=1.61 loss_y2x=3.7117e-01 ppl_y2x=1.45 dual_loss=1.0591e+00
Validation X2Y - loss=4.2400e+00 ppl=69.41 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8054e+00 ppl=44.94 best_loss=2.3090e+00 best_ppl=10.06
Epoch 352 - |param|=1.00e+03 |g_param|=3.90e+05 loss_x2y=4.7678e-01 ppl_x2y=1.61 loss_y2x=3.8511e-01 ppl_y2x=1.47 dual_loss=1.1403e+00
Validation X2Y - loss=4.2764e+00 ppl=71.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8247e+00 ppl=45.82 best_loss=2.3090e+00 best_ppl=10.06
Epoch 353 - |param|=1.00e+03 |g_param|=3.66e+05 loss_x2y=4.6616e-01 ppl_x2y=1.59 loss_y2x=3.6213e-01 ppl_y2x=1.44 dual_loss=1.0788e+00
Validation X2Y - loss=4.2724e+00 ppl=71.69 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8028e+00 ppl=44.83 best_loss=2.3090e+00 best_ppl=10.06
Epoch 354 - |param|=1.00e+03 |g_param|=3.82e+05 loss_x2y=4.7626e-01 ppl_x2y=1.61 loss_y2x=3.7234e-01 ppl_y2x=1.45 dual_loss=1.1302e+00
Validation X2Y - loss=4.2477e+00 ppl=69.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8763e+00 ppl=48.24 best_loss=2.3090e+00 best_ppl=10.06
Epoch 355 - |param|=1.00e+03 |g_param|=3.62e+05 loss_x2y=4.8402e-01 ppl_x2y=1.62 loss_y2x=3.7987e-01 ppl_y2x=1.46 dual_loss=1.1952e+00
Validation X2Y - loss=4.2684e+00 ppl=71.41 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8409e+00 ppl=46.57 best_loss=2.3090e+00 best_ppl=10.06
Epoch 356 - |param|=1.00e+03 |g_param|=4.89e+05 loss_x2y=4.5513e-01 ppl_x2y=1.58 loss_y2x=3.7221e-01 ppl_y2x=1.45 dual_loss=1.0761e+00
Validation X2Y - loss=4.2549e+00 ppl=70.45 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8847e+00 ppl=48.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 357 - |param|=1.00e+03 |g_param|=4.11e+05 loss_x2y=4.5925e-01 ppl_x2y=1.58 loss_y2x=3.7456e-01 ppl_y2x=1.45 dual_loss=1.0808e+00
Validation X2Y - loss=4.2808e+00 ppl=72.30 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8896e+00 ppl=48.89 best_loss=2.3090e+00 best_ppl=10.06
Epoch 358 - |param|=1.01e+03 |g_param|=3.74e+05 loss_x2y=4.4092e-01 ppl_x2y=1.55 loss_y2x=3.6439e-01 ppl_y2x=1.44 dual_loss=1.0443e+00
Validation X2Y - loss=4.2584e+00 ppl=70.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9301e+00 ppl=50.91 best_loss=2.3090e+00 best_ppl=10.06
Epoch 359 - |param|=1.01e+03 |g_param|=3.75e+05 loss_x2y=4.5050e-01 ppl_x2y=1.57 loss_y2x=3.6645e-01 ppl_y2x=1.44 dual_loss=1.0521e+00
Validation X2Y - loss=4.2741e+00 ppl=71.81 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8704e+00 ppl=47.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 360 - |param|=1.01e+03 |g_param|=4.57e+05 loss_x2y=4.6486e-01 ppl_x2y=1.59 loss_y2x=3.6384e-01 ppl_y2x=1.44 dual_loss=1.0947e+00
Validation X2Y - loss=4.2636e+00 ppl=71.07 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9274e+00 ppl=50.77 best_loss=2.3090e+00 best_ppl=10.06
Epoch 361 - |param|=1.01e+03 |g_param|=4.79e+05 loss_x2y=4.5883e-01 ppl_x2y=1.58 loss_y2x=3.8610e-01 ppl_y2x=1.47 dual_loss=1.1263e+00
Validation X2Y - loss=4.2788e+00 ppl=72.15 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8607e+00 ppl=47.50 best_loss=2.3090e+00 best_ppl=10.06
Epoch 362 - |param|=1.01e+03 |g_param|=5.21e+05 loss_x2y=4.4625e-01 ppl_x2y=1.56 loss_y2x=3.8339e-01 ppl_y2x=1.47 dual_loss=1.0923e+00
Validation X2Y - loss=4.2887e+00 ppl=72.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8778e+00 ppl=48.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 363 - |param|=1.01e+03 |g_param|=4.74e+05 loss_x2y=4.5666e-01 ppl_x2y=1.58 loss_y2x=3.8020e-01 ppl_y2x=1.46 dual_loss=1.1691e+00
Validation X2Y - loss=4.3483e+00 ppl=77.34 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8615e+00 ppl=47.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 364 - |param|=1.01e+03 |g_param|=4.41e+05 loss_x2y=4.6796e-01 ppl_x2y=1.60 loss_y2x=4.0656e-01 ppl_y2x=1.50 dual_loss=1.3062e+00
Validation X2Y - loss=4.2628e+00 ppl=71.01 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8859e+00 ppl=48.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 365 - |param|=1.01e+03 |g_param|=3.79e+05 loss_x2y=4.6500e-01 ppl_x2y=1.59 loss_y2x=3.6618e-01 ppl_y2x=1.44 dual_loss=1.1482e+00
Validation X2Y - loss=4.2905e+00 ppl=73.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9137e+00 ppl=50.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 366 - |param|=1.01e+03 |g_param|=3.89e+05 loss_x2y=4.7496e-01 ppl_x2y=1.61 loss_y2x=4.0572e-01 ppl_y2x=1.50 dual_loss=1.3005e+00
Validation X2Y - loss=4.2881e+00 ppl=72.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9400e+00 ppl=51.42 best_loss=2.3090e+00 best_ppl=10.06
Epoch 367 - |param|=1.01e+03 |g_param|=3.62e+05 loss_x2y=4.4996e-01 ppl_x2y=1.57 loss_y2x=3.6601e-01 ppl_y2x=1.44 dual_loss=1.1062e+00
Validation X2Y - loss=4.3449e+00 ppl=77.08 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9245e+00 ppl=50.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 368 - |param|=1.01e+03 |g_param|=3.82e+05 loss_x2y=4.6212e-01 ppl_x2y=1.59 loss_y2x=3.8117e-01 ppl_y2x=1.46 dual_loss=1.2169e+00
Validation X2Y - loss=4.3328e+00 ppl=76.16 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9183e+00 ppl=50.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 369 - |param|=1.01e+03 |g_param|=3.75e+05 loss_x2y=5.2915e-01 ppl_x2y=1.70 loss_y2x=3.7352e-01 ppl_y2x=1.45 dual_loss=1.3088e+00
Validation X2Y - loss=4.3462e+00 ppl=77.18 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8596e+00 ppl=47.44 best_loss=2.3090e+00 best_ppl=10.06
Epoch 370 - |param|=1.01e+03 |g_param|=3.98e+05 loss_x2y=4.6470e-01 ppl_x2y=1.59 loss_y2x=4.0042e-01 ppl_y2x=1.49 dual_loss=1.3338e+00
Validation X2Y - loss=4.2292e+00 ppl=68.66 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8839e+00 ppl=48.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 371 - |param|=1.01e+03 |g_param|=3.81e+05 loss_x2y=4.8288e-01 ppl_x2y=1.62 loss_y2x=4.0265e-01 ppl_y2x=1.50 dual_loss=1.3280e+00
Validation X2Y - loss=4.3143e+00 ppl=74.76 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8720e+00 ppl=48.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 372 - |param|=1.01e+03 |g_param|=3.76e+05 loss_x2y=4.4679e-01 ppl_x2y=1.56 loss_y2x=3.6609e-01 ppl_y2x=1.44 dual_loss=1.1032e+00
Validation X2Y - loss=4.2912e+00 ppl=73.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8774e+00 ppl=48.30 best_loss=2.3090e+00 best_ppl=10.06
Epoch 373 - |param|=1.01e+03 |g_param|=3.79e+05 loss_x2y=5.2945e-01 ppl_x2y=1.70 loss_y2x=4.0503e-01 ppl_y2x=1.50 dual_loss=1.6294e+00
Validation X2Y - loss=4.2920e+00 ppl=73.11 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8947e+00 ppl=49.14 best_loss=2.3090e+00 best_ppl=10.06
Epoch 374 - |param|=1.01e+03 |g_param|=3.75e+05 loss_x2y=4.4955e-01 ppl_x2y=1.57 loss_y2x=3.5815e-01 ppl_y2x=1.43 dual_loss=1.1417e+00
Validation X2Y - loss=4.3265e+00 ppl=75.68 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9722e+00 ppl=53.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 375 - |param|=1.01e+03 |g_param|=3.76e+05 loss_x2y=5.0437e-01 ppl_x2y=1.66 loss_y2x=3.8030e-01 ppl_y2x=1.46 dual_loss=1.3122e+00
Validation X2Y - loss=4.3069e+00 ppl=74.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.8958e+00 ppl=49.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 376 - |param|=1.01e+03 |g_param|=3.86e+05 loss_x2y=5.4212e-01 ppl_x2y=1.72 loss_y2x=4.0970e-01 ppl_y2x=1.51 dual_loss=1.6342e+00
Validation X2Y - loss=4.3006e+00 ppl=73.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9298e+00 ppl=50.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 377 - |param|=1.01e+03 |g_param|=3.75e+05 loss_x2y=4.5470e-01 ppl_x2y=1.58 loss_y2x=3.9304e-01 ppl_y2x=1.48 dual_loss=1.3096e+00
Validation X2Y - loss=4.2742e+00 ppl=71.82 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9207e+00 ppl=50.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 378 - |param|=1.01e+03 |g_param|=3.64e+05 loss_x2y=4.3033e-01 ppl_x2y=1.54 loss_y2x=3.4664e-01 ppl_y2x=1.41 dual_loss=1.0517e+00
Validation X2Y - loss=4.3098e+00 ppl=74.43 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9167e+00 ppl=50.24 best_loss=2.3090e+00 best_ppl=10.06
Epoch 379 - |param|=1.01e+03 |g_param|=3.58e+05 loss_x2y=4.4256e-01 ppl_x2y=1.56 loss_y2x=3.6956e-01 ppl_y2x=1.45 dual_loss=1.1552e+00
Validation X2Y - loss=4.3877e+00 ppl=80.46 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9006e+00 ppl=49.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 380 - |param|=1.01e+03 |g_param|=3.81e+05 loss_x2y=4.4067e-01 ppl_x2y=1.55 loss_y2x=3.6742e-01 ppl_y2x=1.44 dual_loss=1.2416e+00
Validation X2Y - loss=4.3122e+00 ppl=74.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9430e+00 ppl=51.57 best_loss=2.3090e+00 best_ppl=10.06
Epoch 381 - |param|=1.01e+03 |g_param|=3.68e+05 loss_x2y=4.4039e-01 ppl_x2y=1.55 loss_y2x=3.5554e-01 ppl_y2x=1.43 dual_loss=1.1065e+00
Validation X2Y - loss=4.3884e+00 ppl=80.52 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9575e+00 ppl=52.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 382 - |param|=1.01e+03 |g_param|=3.83e+05 loss_x2y=4.5938e-01 ppl_x2y=1.58 loss_y2x=3.8030e-01 ppl_y2x=1.46 dual_loss=1.3444e+00
Validation X2Y - loss=4.2988e+00 ppl=73.61 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9918e+00 ppl=54.15 best_loss=2.3090e+00 best_ppl=10.06
Epoch 383 - |param|=1.01e+03 |g_param|=3.71e+05 loss_x2y=4.6115e-01 ppl_x2y=1.59 loss_y2x=3.6211e-01 ppl_y2x=1.44 dual_loss=1.1972e+00
Validation X2Y - loss=4.3413e+00 ppl=76.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9306e+00 ppl=50.94 best_loss=2.3090e+00 best_ppl=10.06
Epoch 384 - |param|=1.01e+03 |g_param|=3.90e+05 loss_x2y=4.4193e-01 ppl_x2y=1.56 loss_y2x=3.4835e-01 ppl_y2x=1.42 dual_loss=1.1174e+00
Validation X2Y - loss=4.3565e+00 ppl=77.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9533e+00 ppl=52.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 385 - |param|=1.01e+03 |g_param|=3.71e+05 loss_x2y=4.2628e-01 ppl_x2y=1.53 loss_y2x=3.4318e-01 ppl_y2x=1.41 dual_loss=1.0759e+00
Validation X2Y - loss=4.3811e+00 ppl=79.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9355e+00 ppl=51.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 386 - |param|=1.01e+03 |g_param|=3.81e+05 loss_x2y=4.4297e-01 ppl_x2y=1.56 loss_y2x=3.6480e-01 ppl_y2x=1.44 dual_loss=1.2121e+00
Validation X2Y - loss=4.3721e+00 ppl=79.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9793e+00 ppl=53.48 best_loss=2.3090e+00 best_ppl=10.06
Epoch 387 - |param|=1.01e+03 |g_param|=3.59e+05 loss_x2y=5.1892e-01 ppl_x2y=1.68 loss_y2x=4.0072e-01 ppl_y2x=1.49 dual_loss=1.6993e+00
Validation X2Y - loss=4.3787e+00 ppl=79.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9360e+00 ppl=51.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 388 - |param|=1.01e+03 |g_param|=3.95e+05 loss_x2y=4.3591e-01 ppl_x2y=1.55 loss_y2x=3.6663e-01 ppl_y2x=1.44 dual_loss=1.1637e+00
Validation X2Y - loss=4.3770e+00 ppl=79.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9126e+00 ppl=50.03 best_loss=2.3090e+00 best_ppl=10.06
Epoch 389 - |param|=1.02e+03 |g_param|=3.72e+05 loss_x2y=4.4939e-01 ppl_x2y=1.57 loss_y2x=3.6153e-01 ppl_y2x=1.44 dual_loss=1.1982e+00
Validation X2Y - loss=4.3562e+00 ppl=77.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9338e+00 ppl=51.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 390 - |param|=1.02e+03 |g_param|=3.76e+05 loss_x2y=4.7129e-01 ppl_x2y=1.60 loss_y2x=3.7877e-01 ppl_y2x=1.46 dual_loss=1.2305e+00
Validation X2Y - loss=4.3584e+00 ppl=78.13 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9519e+00 ppl=52.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 391 - |param|=1.02e+03 |g_param|=3.75e+05 loss_x2y=4.1191e-01 ppl_x2y=1.51 loss_y2x=3.5365e-01 ppl_y2x=1.42 dual_loss=1.1011e+00
Validation X2Y - loss=4.4194e+00 ppl=83.05 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9772e+00 ppl=53.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 392 - |param|=1.02e+03 |g_param|=5.84e+05 loss_x2y=4.5081e-01 ppl_x2y=1.57 loss_y2x=3.6169e-01 ppl_y2x=1.44 dual_loss=1.2517e+00
Validation X2Y - loss=4.3690e+00 ppl=78.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9815e+00 ppl=53.60 best_loss=2.3090e+00 best_ppl=10.06
Epoch 393 - |param|=1.02e+03 |g_param|=6.68e+05 loss_x2y=4.2463e-01 ppl_x2y=1.53 loss_y2x=3.5269e-01 ppl_y2x=1.42 dual_loss=1.1289e+00
Validation X2Y - loss=4.3886e+00 ppl=80.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9955e+00 ppl=54.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 394 - |param|=1.02e+03 |g_param|=6.86e+05 loss_x2y=5.3140e-01 ppl_x2y=1.70 loss_y2x=3.8185e-01 ppl_y2x=1.46 dual_loss=1.5047e+00
Validation X2Y - loss=4.4361e+00 ppl=84.45 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9370e+00 ppl=51.26 best_loss=2.3090e+00 best_ppl=10.06
Epoch 395 - |param|=1.02e+03 |g_param|=6.64e+05 loss_x2y=4.3288e-01 ppl_x2y=1.54 loss_y2x=3.4831e-01 ppl_y2x=1.42 dual_loss=1.1810e+00
Validation X2Y - loss=4.3929e+00 ppl=80.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9539e+00 ppl=52.14 best_loss=2.3090e+00 best_ppl=10.06
Epoch 396 - |param|=1.02e+03 |g_param|=3.97e+05 loss_x2y=4.2235e-01 ppl_x2y=1.53 loss_y2x=3.3656e-01 ppl_y2x=1.40 dual_loss=1.1642e+00
Validation X2Y - loss=4.4432e+00 ppl=85.04 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0207e+00 ppl=55.74 best_loss=2.3090e+00 best_ppl=10.06
Epoch 397 - |param|=1.02e+03 |g_param|=4.62e+05 loss_x2y=4.2764e-01 ppl_x2y=1.53 loss_y2x=3.3857e-01 ppl_y2x=1.40 dual_loss=1.1627e+00
Validation X2Y - loss=4.4186e+00 ppl=82.98 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0129e+00 ppl=55.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 398 - |param|=1.02e+03 |g_param|=4.91e+05 loss_x2y=4.3182e-01 ppl_x2y=1.54 loss_y2x=3.4364e-01 ppl_y2x=1.41 dual_loss=1.2392e+00
Validation X2Y - loss=4.4537e+00 ppl=85.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9857e+00 ppl=53.82 best_loss=2.3090e+00 best_ppl=10.06
Epoch 399 - |param|=1.02e+03 |g_param|=4.58e+05 loss_x2y=4.1408e-01 ppl_x2y=1.51 loss_y2x=3.3688e-01 ppl_y2x=1.40 dual_loss=1.1234e+00
Validation X2Y - loss=4.4345e+00 ppl=84.31 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9698e+00 ppl=52.97 best_loss=2.3090e+00 best_ppl=10.06
Epoch 400 - |param|=1.02e+03 |g_param|=4.64e+05 loss_x2y=4.1998e-01 ppl_x2y=1.52 loss_y2x=3.3573e-01 ppl_y2x=1.40 dual_loss=1.1556e+00
Validation X2Y - loss=4.4425e+00 ppl=84.99 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9989e+00 ppl=54.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 401 - |param|=1.02e+03 |g_param|=4.62e+05 loss_x2y=4.1528e-01 ppl_x2y=1.51 loss_y2x=3.4001e-01 ppl_y2x=1.40 dual_loss=1.1565e+00
Validation X2Y - loss=4.4283e+00 ppl=83.79 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9656e+00 ppl=52.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 402 - |param|=1.02e+03 |g_param|=5.04e+05 loss_x2y=4.4171e-01 ppl_x2y=1.56 loss_y2x=3.5544e-01 ppl_y2x=1.43 dual_loss=1.2474e+00
Validation X2Y - loss=4.4245e+00 ppl=83.47 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0233e+00 ppl=55.88 best_loss=2.3090e+00 best_ppl=10.06
Epoch 403 - |param|=1.02e+03 |g_param|=4.52e+05 loss_x2y=4.2432e-01 ppl_x2y=1.53 loss_y2x=3.4585e-01 ppl_y2x=1.41 dual_loss=1.1761e+00
Validation X2Y - loss=4.4502e+00 ppl=85.65 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9814e+00 ppl=53.59 best_loss=2.3090e+00 best_ppl=10.06
Epoch 404 - |param|=1.02e+03 |g_param|=4.69e+05 loss_x2y=4.1900e-01 ppl_x2y=1.52 loss_y2x=3.4378e-01 ppl_y2x=1.41 dual_loss=1.1669e+00
Validation X2Y - loss=4.4272e+00 ppl=83.70 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0571e+00 ppl=57.81 best_loss=2.3090e+00 best_ppl=10.06
Epoch 405 - |param|=1.02e+03 |g_param|=4.53e+05 loss_x2y=5.0311e-01 ppl_x2y=1.65 loss_y2x=3.7623e-01 ppl_y2x=1.46 dual_loss=1.6165e+00
Validation X2Y - loss=4.4946e+00 ppl=89.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0310e+00 ppl=56.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 406 - |param|=1.02e+03 |g_param|=4.65e+05 loss_x2y=4.1580e-01 ppl_x2y=1.52 loss_y2x=3.4068e-01 ppl_y2x=1.41 dual_loss=1.1853e+00
Validation X2Y - loss=4.4407e+00 ppl=84.84 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9991e+00 ppl=54.55 best_loss=2.3090e+00 best_ppl=10.06
Epoch 407 - |param|=1.02e+03 |g_param|=4.47e+05 loss_x2y=4.3240e-01 ppl_x2y=1.54 loss_y2x=3.3811e-01 ppl_y2x=1.40 dual_loss=1.1671e+00
Validation X2Y - loss=4.4407e+00 ppl=84.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9871e+00 ppl=53.90 best_loss=2.3090e+00 best_ppl=10.06
Epoch 408 - |param|=1.02e+03 |g_param|=4.83e+05 loss_x2y=4.3986e-01 ppl_x2y=1.55 loss_y2x=3.6741e-01 ppl_y2x=1.44 dual_loss=1.2796e+00
Validation X2Y - loss=4.4140e+00 ppl=82.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0137e+00 ppl=55.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 409 - |param|=1.02e+03 |g_param|=3.78e+05 loss_x2y=4.9803e-01 ppl_x2y=1.65 loss_y2x=3.7800e-01 ppl_y2x=1.46 dual_loss=1.5705e+00
Validation X2Y - loss=4.3941e+00 ppl=80.97 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0037e+00 ppl=54.80 best_loss=2.3090e+00 best_ppl=10.06
Epoch 410 - |param|=1.02e+03 |g_param|=3.76e+05 loss_x2y=4.1558e-01 ppl_x2y=1.52 loss_y2x=3.4734e-01 ppl_y2x=1.42 dual_loss=1.1832e+00
Validation X2Y - loss=4.4428e+00 ppl=85.02 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9744e+00 ppl=53.22 best_loss=2.3090e+00 best_ppl=10.06
Epoch 411 - |param|=1.02e+03 |g_param|=3.64e+05 loss_x2y=4.3800e-01 ppl_x2y=1.55 loss_y2x=3.5526e-01 ppl_y2x=1.43 dual_loss=1.3131e+00
Validation X2Y - loss=4.4599e+00 ppl=86.48 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0124e+00 ppl=55.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 412 - |param|=1.02e+03 |g_param|=3.76e+05 loss_x2y=4.1640e-01 ppl_x2y=1.52 loss_y2x=3.3292e-01 ppl_y2x=1.40 dual_loss=1.1607e+00
Validation X2Y - loss=4.4651e+00 ppl=86.93 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0128e+00 ppl=55.30 best_loss=2.3090e+00 best_ppl=10.06
Epoch 413 - |param|=1.02e+03 |g_param|=3.51e+05 loss_x2y=4.3673e-01 ppl_x2y=1.55 loss_y2x=3.3692e-01 ppl_y2x=1.40 dual_loss=1.2226e+00
Validation X2Y - loss=4.4359e+00 ppl=84.43 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0795e+00 ppl=59.12 best_loss=2.3090e+00 best_ppl=10.06
Epoch 414 - |param|=1.02e+03 |g_param|=3.76e+05 loss_x2y=4.6615e-01 ppl_x2y=1.59 loss_y2x=3.6637e-01 ppl_y2x=1.44 dual_loss=1.4512e+00
Validation X2Y - loss=4.4257e+00 ppl=83.57 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0340e+00 ppl=56.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 415 - |param|=1.02e+03 |g_param|=3.72e+05 loss_x2y=4.1968e-01 ppl_x2y=1.52 loss_y2x=3.4985e-01 ppl_y2x=1.42 dual_loss=1.2696e+00
Validation X2Y - loss=4.4233e+00 ppl=83.37 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9755e+00 ppl=53.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 416 - |param|=1.02e+03 |g_param|=3.79e+05 loss_x2y=4.1857e-01 ppl_x2y=1.52 loss_y2x=3.4373e-01 ppl_y2x=1.41 dual_loss=1.1836e+00
Validation X2Y - loss=4.4596e+00 ppl=86.46 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9900e+00 ppl=54.06 best_loss=2.3090e+00 best_ppl=10.06
Epoch 417 - |param|=1.02e+03 |g_param|=3.62e+05 loss_x2y=4.3069e-01 ppl_x2y=1.54 loss_y2x=3.4575e-01 ppl_y2x=1.41 dual_loss=1.2068e+00
Validation X2Y - loss=4.4606e+00 ppl=86.54 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0309e+00 ppl=56.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 418 - |param|=1.02e+03 |g_param|=3.74e+05 loss_x2y=4.1828e-01 ppl_x2y=1.52 loss_y2x=3.3520e-01 ppl_y2x=1.40 dual_loss=1.2113e+00
Validation X2Y - loss=4.4420e+00 ppl=84.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0397e+00 ppl=56.81 best_loss=2.3090e+00 best_ppl=10.06
Epoch 419 - |param|=1.02e+03 |g_param|=3.57e+05 loss_x2y=4.3724e-01 ppl_x2y=1.55 loss_y2x=3.3312e-01 ppl_y2x=1.40 dual_loss=1.2553e+00
Validation X2Y - loss=4.4371e+00 ppl=84.53 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=3.9997e+00 ppl=54.58 best_loss=2.3090e+00 best_ppl=10.06
Epoch 420 - |param|=1.03e+03 |g_param|=3.86e+05 loss_x2y=4.5696e-01 ppl_x2y=1.58 loss_y2x=3.6251e-01 ppl_y2x=1.44 dual_loss=1.5058e+00
Validation X2Y - loss=4.4011e+00 ppl=81.54 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0205e+00 ppl=55.73 best_loss=2.3090e+00 best_ppl=10.06
Epoch 421 - |param|=1.03e+03 |g_param|=3.58e+05 loss_x2y=4.1399e-01 ppl_x2y=1.51 loss_y2x=3.3064e-01 ppl_y2x=1.39 dual_loss=1.2545e+00
Validation X2Y - loss=4.5021e+00 ppl=90.21 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0172e+00 ppl=55.55 best_loss=2.3090e+00 best_ppl=10.06
Epoch 422 - |param|=1.03e+03 |g_param|=3.73e+05 loss_x2y=4.0104e-01 ppl_x2y=1.49 loss_y2x=3.3066e-01 ppl_y2x=1.39 dual_loss=1.2075e+00
Validation X2Y - loss=4.4554e+00 ppl=86.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0223e+00 ppl=55.83 best_loss=2.3090e+00 best_ppl=10.06
Epoch 423 - |param|=1.03e+03 |g_param|=3.49e+05 loss_x2y=4.1334e-01 ppl_x2y=1.51 loss_y2x=3.4353e-01 ppl_y2x=1.41 dual_loss=1.2371e+00
Validation X2Y - loss=4.4859e+00 ppl=88.75 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0023e+00 ppl=54.72 best_loss=2.3090e+00 best_ppl=10.06
Epoch 424 - |param|=1.03e+03 |g_param|=3.80e+05 loss_x2y=4.4342e-01 ppl_x2y=1.56 loss_y2x=3.5852e-01 ppl_y2x=1.43 dual_loss=1.4011e+00
Validation X2Y - loss=4.5617e+00 ppl=95.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0525e+00 ppl=57.54 best_loss=2.3090e+00 best_ppl=10.06
Epoch 425 - |param|=1.03e+03 |g_param|=3.53e+05 loss_x2y=4.1549e-01 ppl_x2y=1.52 loss_y2x=3.3431e-01 ppl_y2x=1.40 dual_loss=1.2452e+00
Validation X2Y - loss=4.5300e+00 ppl=92.76 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0892e+00 ppl=59.69 best_loss=2.3090e+00 best_ppl=10.06
Epoch 426 - |param|=1.03e+03 |g_param|=3.58e+05 loss_x2y=3.9784e-01 ppl_x2y=1.49 loss_y2x=3.4532e-01 ppl_y2x=1.41 dual_loss=1.2759e+00
Validation X2Y - loss=4.4751e+00 ppl=87.80 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0727e+00 ppl=58.72 best_loss=2.3090e+00 best_ppl=10.06
Epoch 427 - |param|=1.03e+03 |g_param|=3.57e+05 loss_x2y=4.2072e-01 ppl_x2y=1.52 loss_y2x=3.2850e-01 ppl_y2x=1.39 dual_loss=1.1991e+00
Validation X2Y - loss=4.5138e+00 ppl=91.27 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0978e+00 ppl=60.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 428 - |param|=1.03e+03 |g_param|=5.76e+05 loss_x2y=4.2596e-01 ppl_x2y=1.53 loss_y2x=3.4922e-01 ppl_y2x=1.42 dual_loss=1.3254e+00
Validation X2Y - loss=4.5501e+00 ppl=94.64 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0657e+00 ppl=58.31 best_loss=2.3090e+00 best_ppl=10.06
Epoch 429 - |param|=1.03e+03 |g_param|=6.75e+05 loss_x2y=3.9495e-01 ppl_x2y=1.48 loss_y2x=3.3181e-01 ppl_y2x=1.39 dual_loss=1.1650e+00
Validation X2Y - loss=4.5320e+00 ppl=92.94 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0972e+00 ppl=60.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 430 - |param|=1.03e+03 |g_param|=7.02e+05 loss_x2y=3.9667e-01 ppl_x2y=1.49 loss_y2x=3.2415e-01 ppl_y2x=1.38 dual_loss=1.1863e+00
Validation X2Y - loss=4.5217e+00 ppl=92.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0797e+00 ppl=59.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 431 - |param|=1.03e+03 |g_param|=6.53e+05 loss_x2y=4.1498e-01 ppl_x2y=1.51 loss_y2x=3.3577e-01 ppl_y2x=1.40 dual_loss=1.2469e+00
Validation X2Y - loss=4.5359e+00 ppl=93.31 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0951e+00 ppl=60.05 best_loss=2.3090e+00 best_ppl=10.06
Epoch 432 - |param|=1.03e+03 |g_param|=6.98e+05 loss_x2y=4.0447e-01 ppl_x2y=1.50 loss_y2x=3.2672e-01 ppl_y2x=1.39 dual_loss=1.2620e+00
Validation X2Y - loss=4.5283e+00 ppl=92.60 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0764e+00 ppl=58.93 best_loss=2.3090e+00 best_ppl=10.06
Epoch 433 - |param|=1.03e+03 |g_param|=6.46e+05 loss_x2y=4.0052e-01 ppl_x2y=1.49 loss_y2x=3.2828e-01 ppl_y2x=1.39 dual_loss=1.1811e+00
Validation X2Y - loss=4.4953e+00 ppl=89.59 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1067e+00 ppl=60.74 best_loss=2.3090e+00 best_ppl=10.06
Epoch 434 - |param|=1.03e+03 |g_param|=6.74e+05 loss_x2y=4.8257e-01 ppl_x2y=1.62 loss_y2x=3.6653e-01 ppl_y2x=1.44 dual_loss=1.6503e+00
Validation X2Y - loss=4.4813e+00 ppl=88.35 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1633e+00 ppl=64.28 best_loss=2.3090e+00 best_ppl=10.06
Epoch 435 - |param|=1.03e+03 |g_param|=6.59e+05 loss_x2y=4.2148e-01 ppl_x2y=1.52 loss_y2x=3.3156e-01 ppl_y2x=1.39 dual_loss=1.3459e+00
Validation X2Y - loss=4.5192e+00 ppl=91.76 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1134e+00 ppl=61.15 best_loss=2.3090e+00 best_ppl=10.06
Epoch 436 - |param|=1.03e+03 |g_param|=6.85e+05 loss_x2y=4.3044e-01 ppl_x2y=1.54 loss_y2x=3.7266e-01 ppl_y2x=1.45 dual_loss=1.4998e+00
Validation X2Y - loss=4.4837e+00 ppl=88.56 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1060e+00 ppl=60.71 best_loss=2.3090e+00 best_ppl=10.06
Epoch 437 - |param|=1.03e+03 |g_param|=6.59e+05 loss_x2y=4.7044e-01 ppl_x2y=1.60 loss_y2x=3.6106e-01 ppl_y2x=1.43 dual_loss=1.5456e+00
Validation X2Y - loss=4.5163e+00 ppl=91.50 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0543e+00 ppl=57.65 best_loss=2.3090e+00 best_ppl=10.06
Epoch 438 - |param|=1.03e+03 |g_param|=6.64e+05 loss_x2y=4.0497e-01 ppl_x2y=1.50 loss_y2x=3.2570e-01 ppl_y2x=1.39 dual_loss=1.2520e+00
Validation X2Y - loss=4.5496e+00 ppl=94.59 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0724e+00 ppl=58.70 best_loss=2.3090e+00 best_ppl=10.06
Epoch 439 - |param|=1.03e+03 |g_param|=6.51e+05 loss_x2y=3.9852e-01 ppl_x2y=1.49 loss_y2x=3.2776e-01 ppl_y2x=1.39 dual_loss=1.2746e+00
Validation X2Y - loss=4.5054e+00 ppl=90.51 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0791e+00 ppl=59.09 best_loss=2.3090e+00 best_ppl=10.06
Epoch 440 - |param|=1.03e+03 |g_param|=7.09e+05 loss_x2y=4.3586e-01 ppl_x2y=1.55 loss_y2x=3.6927e-01 ppl_y2x=1.45 dual_loss=1.5094e+00
Validation X2Y - loss=4.5317e+00 ppl=92.92 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0550e+00 ppl=57.68 best_loss=2.3090e+00 best_ppl=10.06
Epoch 441 - |param|=1.03e+03 |g_param|=5.44e+05 loss_x2y=4.0045e-01 ppl_x2y=1.49 loss_y2x=3.2911e-01 ppl_y2x=1.39 dual_loss=1.3090e+00
Validation X2Y - loss=4.5282e+00 ppl=92.59 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0495e+00 ppl=57.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 442 - |param|=1.03e+03 |g_param|=4.39e+05 loss_x2y=3.8444e-01 ppl_x2y=1.47 loss_y2x=2.9824e-01 ppl_y2x=1.35 dual_loss=1.1217e+00
Validation X2Y - loss=4.5108e+00 ppl=91.00 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0486e+00 ppl=57.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 443 - |param|=1.03e+03 |g_param|=4.17e+05 loss_x2y=3.9428e-01 ppl_x2y=1.48 loss_y2x=3.2528e-01 ppl_y2x=1.38 dual_loss=1.2884e+00
Validation X2Y - loss=4.5463e+00 ppl=94.29 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0881e+00 ppl=59.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 444 - |param|=1.03e+03 |g_param|=4.53e+05 loss_x2y=3.9921e-01 ppl_x2y=1.49 loss_y2x=3.2454e-01 ppl_y2x=1.38 dual_loss=1.2930e+00
Validation X2Y - loss=4.5021e+00 ppl=90.20 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0637e+00 ppl=58.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 445 - |param|=1.03e+03 |g_param|=4.34e+05 loss_x2y=4.1451e-01 ppl_x2y=1.51 loss_y2x=3.2542e-01 ppl_y2x=1.38 dual_loss=1.2869e+00
Validation X2Y - loss=4.5458e+00 ppl=94.24 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1021e+00 ppl=60.47 best_loss=2.3090e+00 best_ppl=10.06
Epoch 446 - |param|=1.03e+03 |g_param|=4.69e+05 loss_x2y=4.1067e-01 ppl_x2y=1.51 loss_y2x=3.3608e-01 ppl_y2x=1.40 dual_loss=1.3279e+00
Validation X2Y - loss=4.5720e+00 ppl=96.74 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0992e+00 ppl=60.29 best_loss=2.3090e+00 best_ppl=10.06
Epoch 447 - |param|=1.03e+03 |g_param|=4.49e+05 loss_x2y=4.0486e-01 ppl_x2y=1.50 loss_y2x=3.2474e-01 ppl_y2x=1.38 dual_loss=1.2316e+00
Validation X2Y - loss=4.5429e+00 ppl=93.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0578e+00 ppl=57.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 448 - |param|=1.03e+03 |g_param|=4.65e+05 loss_x2y=4.0528e-01 ppl_x2y=1.50 loss_y2x=3.5280e-01 ppl_y2x=1.42 dual_loss=1.4092e+00
Validation X2Y - loss=4.6121e+00 ppl=100.70 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0713e+00 ppl=58.63 best_loss=2.3090e+00 best_ppl=10.06
Epoch 449 - |param|=1.03e+03 |g_param|=4.58e+05 loss_x2y=4.0113e-01 ppl_x2y=1.49 loss_y2x=3.3265e-01 ppl_y2x=1.39 dual_loss=1.3222e+00
Validation X2Y - loss=4.5629e+00 ppl=95.86 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0262e+00 ppl=56.05 best_loss=2.3090e+00 best_ppl=10.06
Epoch 450 - |param|=1.03e+03 |g_param|=4.63e+05 loss_x2y=4.0187e-01 ppl_x2y=1.49 loss_y2x=3.3143e-01 ppl_y2x=1.39 dual_loss=1.3428e+00
Validation X2Y - loss=4.5923e+00 ppl=98.72 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0562e+00 ppl=57.76 best_loss=2.3090e+00 best_ppl=10.06
Epoch 451 - |param|=1.03e+03 |g_param|=4.59e+05 loss_x2y=4.0443e-01 ppl_x2y=1.50 loss_y2x=3.3811e-01 ppl_y2x=1.40 dual_loss=1.3471e+00
Validation X2Y - loss=4.6408e+00 ppl=103.62 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0782e+00 ppl=59.04 best_loss=2.3090e+00 best_ppl=10.06
Epoch 452 - |param|=1.03e+03 |g_param|=4.59e+05 loss_x2y=3.9070e-01 ppl_x2y=1.48 loss_y2x=3.1783e-01 ppl_y2x=1.37 dual_loss=1.2299e+00
Validation X2Y - loss=4.5846e+00 ppl=97.96 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1032e+00 ppl=60.53 best_loss=2.3090e+00 best_ppl=10.06
Epoch 453 - |param|=1.04e+03 |g_param|=4.72e+05 loss_x2y=4.2227e-01 ppl_x2y=1.53 loss_y2x=3.6894e-01 ppl_y2x=1.45 dual_loss=1.5026e+00
Validation X2Y - loss=4.5583e+00 ppl=95.42 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0386e+00 ppl=56.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 454 - |param|=1.04e+03 |g_param|=4.64e+05 loss_x2y=3.8971e-01 ppl_x2y=1.48 loss_y2x=3.1934e-01 ppl_y2x=1.38 dual_loss=1.2452e+00
Validation X2Y - loss=4.5610e+00 ppl=95.68 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1310e+00 ppl=62.24 best_loss=2.3090e+00 best_ppl=10.06
Epoch 455 - |param|=1.04e+03 |g_param|=4.36e+05 loss_x2y=3.9060e-01 ppl_x2y=1.48 loss_y2x=3.2019e-01 ppl_y2x=1.38 dual_loss=1.2646e+00
Validation X2Y - loss=4.5467e+00 ppl=94.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0423e+00 ppl=56.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 456 - |param|=1.04e+03 |g_param|=4.74e+05 loss_x2y=4.4532e-01 ppl_x2y=1.56 loss_y2x=3.6241e-01 ppl_y2x=1.44 dual_loss=1.6263e+00
Validation X2Y - loss=4.5720e+00 ppl=96.73 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0526e+00 ppl=57.55 best_loss=2.3090e+00 best_ppl=10.06
Epoch 457 - |param|=1.04e+03 |g_param|=4.41e+05 loss_x2y=3.7584e-01 ppl_x2y=1.46 loss_y2x=3.1381e-01 ppl_y2x=1.37 dual_loss=1.2250e+00
Validation X2Y - loss=4.6059e+00 ppl=100.07 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0733e+00 ppl=58.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 458 - |param|=1.04e+03 |g_param|=4.48e+05 loss_x2y=3.8437e-01 ppl_x2y=1.47 loss_y2x=3.2135e-01 ppl_y2x=1.38 dual_loss=1.3457e+00
Validation X2Y - loss=4.5892e+00 ppl=98.42 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0602e+00 ppl=57.98 best_loss=2.3090e+00 best_ppl=10.06
Epoch 459 - |param|=1.04e+03 |g_param|=4.47e+05 loss_x2y=3.9498e-01 ppl_x2y=1.48 loss_y2x=3.2296e-01 ppl_y2x=1.38 dual_loss=1.3772e+00
Validation X2Y - loss=4.5573e+00 ppl=95.32 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1407e+00 ppl=62.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 460 - |param|=1.04e+03 |g_param|=4.52e+05 loss_x2y=4.0129e-01 ppl_x2y=1.49 loss_y2x=3.1870e-01 ppl_y2x=1.38 dual_loss=1.2908e+00
Validation X2Y - loss=4.5628e+00 ppl=95.85 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1314e+00 ppl=62.26 best_loss=2.3090e+00 best_ppl=10.06
Epoch 461 - |param|=1.04e+03 |g_param|=4.42e+05 loss_x2y=3.9070e-01 ppl_x2y=1.48 loss_y2x=3.2154e-01 ppl_y2x=1.38 dual_loss=1.2807e+00
Validation X2Y - loss=4.5549e+00 ppl=95.09 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0958e+00 ppl=60.09 best_loss=2.3090e+00 best_ppl=10.06
Epoch 462 - |param|=1.04e+03 |g_param|=4.75e+05 loss_x2y=3.9519e-01 ppl_x2y=1.48 loss_y2x=3.2583e-01 ppl_y2x=1.39 dual_loss=1.3439e+00
Validation X2Y - loss=4.5934e+00 ppl=98.83 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1431e+00 ppl=63.00 best_loss=2.3090e+00 best_ppl=10.06
Epoch 463 - |param|=1.04e+03 |g_param|=4.49e+05 loss_x2y=4.0073e-01 ppl_x2y=1.49 loss_y2x=3.3785e-01 ppl_y2x=1.40 dual_loss=1.3848e+00
Validation X2Y - loss=4.6220e+00 ppl=101.70 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0844e+00 ppl=59.40 best_loss=2.3090e+00 best_ppl=10.06
Epoch 464 - |param|=1.04e+03 |g_param|=4.79e+05 loss_x2y=4.1423e-01 ppl_x2y=1.51 loss_y2x=3.6776e-01 ppl_y2x=1.44 dual_loss=1.6183e+00
Validation X2Y - loss=4.5711e+00 ppl=96.65 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.0763e+00 ppl=58.93 best_loss=2.3090e+00 best_ppl=10.06
Epoch 465 - |param|=1.04e+03 |g_param|=4.43e+05 loss_x2y=3.9704e-01 ppl_x2y=1.49 loss_y2x=3.1927e-01 ppl_y2x=1.38 dual_loss=1.2645e+00
Validation X2Y - loss=4.5792e+00 ppl=97.43 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1180e+00 ppl=61.44 best_loss=2.3090e+00 best_ppl=10.06
Epoch 466 - |param|=1.04e+03 |g_param|=4.76e+05 loss_x2y=4.0701e-01 ppl_x2y=1.50 loss_y2x=3.3180e-01 ppl_y2x=1.39 dual_loss=1.4216e+00
Validation X2Y - loss=4.6228e+00 ppl=101.78 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1004e+00 ppl=60.36 best_loss=2.3090e+00 best_ppl=10.06
Epoch 467 - |param|=1.04e+03 |g_param|=3.66e+05 loss_x2y=3.9097e-01 ppl_x2y=1.48 loss_y2x=3.1288e-01 ppl_y2x=1.37 dual_loss=1.3312e+00
Validation X2Y - loss=4.6206e+00 ppl=101.55 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1490e+00 ppl=63.37 best_loss=2.3090e+00 best_ppl=10.06
Epoch 468 - |param|=1.04e+03 |g_param|=3.66e+05 loss_x2y=4.0136e-01 ppl_x2y=1.49 loss_y2x=3.5358e-01 ppl_y2x=1.42 dual_loss=1.5034e+00
Validation X2Y - loss=4.6137e+00 ppl=100.85 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0959e+00 ppl=60.10 best_loss=2.3090e+00 best_ppl=10.06
Epoch 469 - |param|=1.04e+03 |g_param|=3.41e+05 loss_x2y=3.8311e-01 ppl_x2y=1.47 loss_y2x=3.1106e-01 ppl_y2x=1.36 dual_loss=1.2482e+00
Validation X2Y - loss=4.6508e+00 ppl=104.67 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0834e+00 ppl=59.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 470 - |param|=1.04e+03 |g_param|=3.63e+05 loss_x2y=3.9483e-01 ppl_x2y=1.48 loss_y2x=3.2641e-01 ppl_y2x=1.39 dual_loss=1.3110e+00
Validation X2Y - loss=4.6353e+00 ppl=103.06 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1341e+00 ppl=62.43 best_loss=2.3090e+00 best_ppl=10.06
Epoch 471 - |param|=1.04e+03 |g_param|=3.41e+05 loss_x2y=3.8694e-01 ppl_x2y=1.47 loss_y2x=3.2476e-01 ppl_y2x=1.38 dual_loss=1.3701e+00
Validation X2Y - loss=4.5630e+00 ppl=95.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1369e+00 ppl=62.61 best_loss=2.3090e+00 best_ppl=10.06
Epoch 472 - |param|=1.04e+03 |g_param|=3.56e+05 loss_x2y=3.9749e-01 ppl_x2y=1.49 loss_y2x=3.2190e-01 ppl_y2x=1.38 dual_loss=1.3297e+00
Validation X2Y - loss=4.6023e+00 ppl=99.71 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1501e+00 ppl=63.44 best_loss=2.3090e+00 best_ppl=10.06
Epoch 473 - |param|=1.04e+03 |g_param|=3.58e+05 loss_x2y=3.9446e-01 ppl_x2y=1.48 loss_y2x=3.0988e-01 ppl_y2x=1.36 dual_loss=1.3174e+00
Validation X2Y - loss=4.6464e+00 ppl=104.20 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.2122e+00 ppl=67.51 best_loss=2.3090e+00 best_ppl=10.06
Epoch 474 - |param|=1.04e+03 |g_param|=6.39e+05 loss_x2y=4.3611e-01 ppl_x2y=1.55 loss_y2x=3.5286e-01 ppl_y2x=1.42 dual_loss=1.6778e+00
Validation X2Y - loss=4.6362e+00 ppl=103.16 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1508e+00 ppl=63.49 best_loss=2.3090e+00 best_ppl=10.06
Epoch 475 - |param|=1.04e+03 |g_param|=3.60e+05 loss_x2y=3.9550e-01 ppl_x2y=1.49 loss_y2x=3.3258e-01 ppl_y2x=1.39 dual_loss=1.4112e+00
Validation X2Y - loss=4.6308e+00 ppl=102.59 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1327e+00 ppl=62.35 best_loss=2.3090e+00 best_ppl=10.06
Epoch 476 - |param|=1.04e+03 |g_param|=3.63e+05 loss_x2y=4.0611e-01 ppl_x2y=1.50 loss_y2x=3.6410e-01 ppl_y2x=1.44 dual_loss=1.6053e+00
Validation X2Y - loss=4.6134e+00 ppl=100.83 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1298e+00 ppl=62.17 best_loss=2.3090e+00 best_ppl=10.06
Epoch 477 - |param|=1.04e+03 |g_param|=3.38e+05 loss_x2y=3.8641e-01 ppl_x2y=1.47 loss_y2x=3.1006e-01 ppl_y2x=1.36 dual_loss=1.2714e+00
Validation X2Y - loss=4.6228e+00 ppl=101.77 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1937e+00 ppl=66.27 best_loss=2.3090e+00 best_ppl=10.06
Epoch 478 - |param|=1.04e+03 |g_param|=3.57e+05 loss_x2y=3.9297e-01 ppl_x2y=1.48 loss_y2x=3.1970e-01 ppl_y2x=1.38 dual_loss=1.3947e+00
Validation X2Y - loss=4.6481e+00 ppl=104.39 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1601e+00 ppl=64.08 best_loss=2.3090e+00 best_ppl=10.06
Epoch 479 - |param|=1.04e+03 |g_param|=3.37e+05 loss_x2y=3.7856e-01 ppl_x2y=1.46 loss_y2x=3.2079e-01 ppl_y2x=1.38 dual_loss=1.3151e+00
Validation X2Y - loss=4.6746e+00 ppl=107.19 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.0954e+00 ppl=60.07 best_loss=2.3090e+00 best_ppl=10.06
Epoch 480 - |param|=1.04e+03 |g_param|=3.53e+05 loss_x2y=3.8150e-01 ppl_x2y=1.46 loss_y2x=3.1986e-01 ppl_y2x=1.38 dual_loss=1.3133e+00
Validation X2Y - loss=4.6447e+00 ppl=104.03 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1292e+00 ppl=62.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 481 - |param|=1.04e+03 |g_param|=3.34e+05 loss_x2y=3.9806e-01 ppl_x2y=1.49 loss_y2x=3.4559e-01 ppl_y2x=1.41 dual_loss=1.5551e+00
Validation X2Y - loss=4.5938e+00 ppl=98.87 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1732e+00 ppl=64.92 best_loss=2.3090e+00 best_ppl=10.06
Epoch 482 - |param|=1.04e+03 |g_param|=3.47e+05 loss_x2y=3.9872e-01 ppl_x2y=1.49 loss_y2x=3.2086e-01 ppl_y2x=1.38 dual_loss=1.4358e+00
Validation X2Y - loss=4.6454e+00 ppl=104.11 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1074e+00 ppl=60.79 best_loss=2.3090e+00 best_ppl=10.06
Epoch 483 - |param|=1.04e+03 |g_param|=3.42e+05 loss_x2y=3.7925e-01 ppl_x2y=1.46 loss_y2x=3.2168e-01 ppl_y2x=1.38 dual_loss=1.3441e+00
Validation X2Y - loss=4.5913e+00 ppl=98.62 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1842e+00 ppl=65.64 best_loss=2.3090e+00 best_ppl=10.06
Epoch 484 - |param|=1.04e+03 |g_param|=3.53e+05 loss_x2y=3.8026e-01 ppl_x2y=1.46 loss_y2x=3.2750e-01 ppl_y2x=1.39 dual_loss=1.3889e+00
Validation X2Y - loss=4.6461e+00 ppl=104.18 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1347e+00 ppl=62.47 best_loss=2.3090e+00 best_ppl=10.06
Epoch 485 - |param|=1.05e+03 |g_param|=3.40e+05 loss_x2y=3.6370e-01 ppl_x2y=1.44 loss_y2x=3.1150e-01 ppl_y2x=1.37 dual_loss=1.2868e+00
Validation X2Y - loss=4.6244e+00 ppl=101.94 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1753e+00 ppl=65.06 best_loss=2.3090e+00 best_ppl=10.06
Epoch 486 - |param|=1.05e+03 |g_param|=3.58e+05 loss_x2y=4.1775e-01 ppl_x2y=1.52 loss_y2x=3.5055e-01 ppl_y2x=1.42 dual_loss=1.5722e+00
Validation X2Y - loss=4.6625e+00 ppl=105.90 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1304e+00 ppl=62.21 best_loss=2.3090e+00 best_ppl=10.06
Epoch 487 - |param|=1.05e+03 |g_param|=3.39e+05 loss_x2y=3.5858e-01 ppl_x2y=1.43 loss_y2x=3.1407e-01 ppl_y2x=1.37 dual_loss=1.2881e+00
Validation X2Y - loss=4.6411e+00 ppl=103.66 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1425e+00 ppl=62.96 best_loss=2.3090e+00 best_ppl=10.06
Epoch 488 - |param|=1.05e+03 |g_param|=3.58e+05 loss_x2y=3.8913e-01 ppl_x2y=1.48 loss_y2x=3.2520e-01 ppl_y2x=1.38 dual_loss=1.4352e+00
Validation X2Y - loss=4.6015e+00 ppl=99.64 best_loss=2.6384e+00 best_ppl=13.99                                          
Validation Y2X - loss=4.1706e+00 ppl=64.75 best_loss=2.3090e+00 best_ppl=10.06
Epoch 489 - |param|=1.05e+03 |g_param|=3.52e+05 loss_x2y=3.7270e-01 ppl_x2y=1.45 loss_y2x=3.0359e-01 ppl_y2x=1.35 dual_loss=1.2434e+00
Validation X2Y - loss=4.6793e+00 ppl=107.69 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.2174e+00 ppl=67.85 best_loss=2.3090e+00 best_ppl=10.06
Epoch 490 - |param|=1.05e+03 |g_param|=3.65e+05 loss_x2y=3.6741e-01 ppl_x2y=1.44 loss_y2x=2.9720e-01 ppl_y2x=1.35 dual_loss=1.2769e+00
Validation X2Y - loss=4.6284e+00 ppl=102.35 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.2075e+00 ppl=67.19 best_loss=2.3090e+00 best_ppl=10.06
Epoch 491 - |param|=1.05e+03 |g_param|=3.57e+05 loss_x2y=3.8394e-01 ppl_x2y=1.47 loss_y2x=3.1969e-01 ppl_y2x=1.38 dual_loss=1.3649e+00
Validation X2Y - loss=4.6571e+00 ppl=105.33 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1948e+00 ppl=66.34 best_loss=2.3090e+00 best_ppl=10.06
Epoch 492 - |param|=1.05e+03 |g_param|=3.89e+05 loss_x2y=3.9606e-01 ppl_x2y=1.49 loss_y2x=3.2923e-01 ppl_y2x=1.39 dual_loss=1.4727e+00
Validation X2Y - loss=4.6373e+00 ppl=103.26 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.2074e+00 ppl=67.18 best_loss=2.3090e+00 best_ppl=10.06
Epoch 493 - |param|=1.05e+03 |g_param|=3.48e+05 loss_x2y=3.7544e-01 ppl_x2y=1.46 loss_y2x=3.0067e-01 ppl_y2x=1.35 dual_loss=1.2928e+00
Validation X2Y - loss=4.6481e+00 ppl=104.39 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1630e+00 ppl=64.26 best_loss=2.3090e+00 best_ppl=10.06
Epoch 494 - |param|=1.05e+03 |g_param|=3.54e+05 loss_x2y=4.7223e-01 ppl_x2y=1.60 loss_y2x=3.3239e-01 ppl_y2x=1.39 dual_loss=1.6546e+00
Validation X2Y - loss=4.7253e+00 ppl=112.77 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1639e+00 ppl=64.32 best_loss=2.3090e+00 best_ppl=10.06
Epoch 495 - |param|=1.05e+03 |g_param|=3.43e+05 loss_x2y=3.9223e-01 ppl_x2y=1.48 loss_y2x=3.3263e-01 ppl_y2x=1.39 dual_loss=1.5309e+00
Validation X2Y - loss=4.6669e+00 ppl=106.37 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1374e+00 ppl=62.64 best_loss=2.3090e+00 best_ppl=10.06
Epoch 496 - |param|=1.05e+03 |g_param|=3.49e+05 loss_x2y=3.7931e-01 ppl_x2y=1.46 loss_y2x=3.0334e-01 ppl_y2x=1.35 dual_loss=1.3090e+00
Validation X2Y - loss=4.6692e+00 ppl=106.61 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1921e+00 ppl=66.16 best_loss=2.3090e+00 best_ppl=10.06
Epoch 497 - |param|=1.05e+03 |g_param|=3.45e+05 loss_x2y=3.7061e-01 ppl_x2y=1.45 loss_y2x=3.0039e-01 ppl_y2x=1.35 dual_loss=1.3274e+00
Validation X2Y - loss=4.6060e+00 ppl=100.09 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1524e+00 ppl=63.59 best_loss=2.3090e+00 best_ppl=10.06
Epoch 498 - |param|=1.05e+03 |g_param|=3.73e+05 loss_x2y=4.0182e-01 ppl_x2y=1.49 loss_y2x=3.4666e-01 ppl_y2x=1.41 dual_loss=1.5796e+00
Validation X2Y - loss=4.6943e+00 ppl=109.32 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1609e+00 ppl=64.13 best_loss=2.3090e+00 best_ppl=10.06
Epoch 499 - |param|=1.05e+03 |g_param|=4.00e+05 loss_x2y=3.9803e-01 ppl_x2y=1.49 loss_y2x=3.3002e-01 ppl_y2x=1.39 dual_loss=1.5907e+00
Validation X2Y - loss=4.6503e+00 ppl=104.61 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1620e+00 ppl=64.20 best_loss=2.3090e+00 best_ppl=10.06
Epoch 500 - |param|=1.05e+03 |g_param|=3.81e+05 loss_x2y=3.9012e-01 ppl_x2y=1.48 loss_y2x=3.4397e-01 ppl_y2x=1.41 dual_loss=1.6351e+00
Validation X2Y - loss=4.6522e+00 ppl=104.81 best_loss=2.6384e+00 best_ppl=13.99                                         
Validation Y2X - loss=4.1626e+00 ppl=64.24 best_loss=2.3090e+00 best_ppl=10.06

real	131m32.570s
user	129m2.928s
sys	1m39.214s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Testing/Evaluation for Seq2Seq-DSL 500 Models 

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-xy-seq2seq-500epoch-mybk.sh 
/home/ye/exp/simple-nmt/model/dsl/mybk-500epoch
Evaluation result for the model: dsl-model-mybk.01.4.88-131.64.4.70-109.76.4.13-61.91.4.02-55.45.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.7/0.0/0.0/0.0 (BP=0.972, ratio=0.972, hyp_len=11111, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.88-131.64.4.70-109.76.4.13-61.91.4.02-55.45.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.1/0.0/0.0 (BP=0.909, ratio=0.913, hyp_len=11166, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.45-85.49.4.23-68.66.3.89-48.68.3.81-45.32.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.6/0.0/0.0/0.0 (BP=0.977, ratio=0.977, hyp_len=11174, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.45-85.49.4.23-68.66.3.89-48.68.3.81-45.32.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.7/2.0/0.3/0.0 (BP=0.990, ratio=0.990, hyp_len=12107, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.16.4.13-61.99.3.84-46.58.3.75-42.55.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.5/0.2/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=11604, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.16.4.13-61.99.3.84-46.58.3.75-42.55.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/1.9/0.3/0.0 (BP=0.998, ratio=0.998, hyp_len=12212, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.23.4.11-61.09.3.81-45.13.3.75-42.52.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.3/0.0/0.0 (BP=0.966, ratio=0.967, hyp_len=11055, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.23.4.11-61.09.3.81-45.13.3.75-42.52.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.1/1.9/0.3/0.0 (BP=1.000, ratio=1.018, hyp_len=12449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.37-78.77.4.20-66.57.3.81-45.07.3.70-40.35.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.3/0.3/0.0/0.0 (BP=1.000, ratio=1.033, hyp_len=11809, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.37-78.77.4.20-66.57.3.81-45.07.3.70-40.35.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.6/0.0/0.0 (BP=0.976, ratio=0.976, hyp_len=11942, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.30-73.65.4.10-60.29.3.80-44.59.3.73-41.63.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.2/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=11720, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.30-73.65.4.10-60.29.3.80-44.59.3.73-41.63.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.018, hyp_len=12453, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.28-71.94.4.04-56.84.3.79-44.10.3.64-38.16.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.4/0.1/0.0/0.0 (BP=1.000, ratio=1.065, hyp_len=12179, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.28-71.94.4.04-56.84.3.79-44.10.3.64-38.16.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/0.5/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=12313, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.99.4.04-57.07.3.79-44.26.3.66-38.77.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.3/0.4/0.0/0.0 (BP=1.000, ratio=1.132, hyp_len=12946, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.99.4.04-57.07.3.79-44.26.3.66-38.77.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.0/1.1/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=12342, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.21-67.49.4.00-54.35.3.71-40.93.3.56-35.05.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.3/0.0/0.0 (BP=1.000, ratio=1.020, hyp_len=11659, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.21-67.49.4.00-54.35.3.71-40.93.3.56-35.05.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.5/0.8/0.1/0.0 (BP=1.000, ratio=1.083, hyp_len=13244, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.100.1.42-4.15.1.25-3.51.2.90-18.21.2.57-13.03.pth, mybk
BLEU = 10.03, 34.9/13.6/6.5/3.3 (BP=1.000, ratio=1.100, hyp_len=12573, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.100.1.42-4.15.1.25-3.51.2.90-18.21.2.57-13.03.pth, bkmy
BLEU = 11.82, 38.7/16.4/7.8/3.9 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.101.1.41-4.09.1.23-3.42.2.89-18.03.2.56-12.92.pth, mybk
BLEU = 9.56, 34.0/13.1/6.2/3.0 (BP=1.000, ratio=1.115, hyp_len=12742, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.101.1.41-4.09.1.23-3.42.2.89-18.03.2.56-12.92.pth, bkmy
BLEU = 11.54, 39.3/16.5/7.6/3.6 (BP=1.000, ratio=1.068, hyp_len=13058, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.102.1.46-4.32.1.25-3.49.2.94-18.86.2.56-12.93.pth, mybk
BLEU = 9.79, 35.0/13.4/6.2/3.2 (BP=1.000, ratio=1.101, hyp_len=12592, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.102.1.46-4.32.1.25-3.49.2.94-18.86.2.56-12.93.pth, bkmy
BLEU = 11.79, 39.5/16.7/7.8/3.8 (BP=1.000, ratio=1.064, hyp_len=13018, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.103.1.42-4.12.1.22-3.37.2.93-18.77.2.54-12.69.pth, mybk
BLEU = 9.69, 34.7/13.2/6.2/3.1 (BP=1.000, ratio=1.107, hyp_len=12659, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.103.1.42-4.12.1.22-3.37.2.93-18.77.2.54-12.69.pth, bkmy
BLEU = 11.85, 39.8/17.0/7.9/3.7 (BP=1.000, ratio=1.053, hyp_len=12880, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.05-57.68.3.88-48.43.3.53-33.97.3.45-31.49.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.6/0.6/0.0/0.0 (BP=0.798, ratio=0.816, hyp_len=9325, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.05-57.68.3.88-48.43.3.53-33.97.3.45-31.49.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.1/0.9/0.0/0.0 (BP=0.904, ratio=0.908, hyp_len=11105, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.104.1.37-3.92.1.19-3.29.2.94-18.93.2.57-13.12.pth, mybk
BLEU = 9.99, 34.4/13.3/6.4/3.4 (BP=1.000, ratio=1.118, hyp_len=12784, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.104.1.37-3.92.1.19-3.29.2.94-18.93.2.57-13.12.pth, bkmy
BLEU = 11.83, 38.9/16.5/7.8/3.9 (BP=1.000, ratio=1.092, hyp_len=13356, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.105.1.42-4.14.1.29-3.62.2.91-18.35.2.59-13.38.pth, mybk
BLEU = 9.52, 34.5/13.0/6.2/3.0 (BP=1.000, ratio=1.107, hyp_len=12655, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.105.1.42-4.14.1.29-3.62.2.91-18.35.2.59-13.38.pth, bkmy
BLEU = 11.55, 38.5/16.1/7.6/3.8 (BP=1.000, ratio=1.091, hyp_len=13339, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.106.1.38-3.99.1.22-3.38.2.91-18.37.2.58-13.17.pth, mybk
BLEU = 9.87, 33.9/13.2/6.4/3.3 (BP=1.000, ratio=1.121, hyp_len=12814, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.106.1.38-3.99.1.22-3.38.2.91-18.37.2.58-13.17.pth, bkmy
BLEU = 12.19, 39.4/16.7/8.0/4.2 (BP=1.000, ratio=1.075, hyp_len=13145, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.107.1.34-3.83.1.15-3.17.2.93-18.74.2.57-13.07.pth, mybk
BLEU = 10.33, 35.1/13.8/6.7/3.5 (BP=1.000, ratio=1.101, hyp_len=12585, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.107.1.34-3.83.1.15-3.17.2.93-18.74.2.57-13.07.pth, bkmy
BLEU = 11.95, 39.1/16.7/7.9/3.9 (BP=1.000, ratio=1.064, hyp_len=13014, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.108.1.37-3.95.1.23-3.42.2.96-19.34.2.56-12.99.pth, mybk
BLEU = 9.93, 34.7/13.3/6.3/3.3 (BP=1.000, ratio=1.095, hyp_len=12514, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.108.1.37-3.95.1.23-3.42.2.96-19.34.2.56-12.99.pth, bkmy
BLEU = 11.35, 38.6/16.1/7.5/3.6 (BP=1.000, ratio=1.069, hyp_len=13074, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.109.1.32-3.75.1.15-3.14.2.98-19.61.2.59-13.31.pth, mybk
BLEU = 9.70, 34.1/13.0/6.2/3.2 (BP=1.000, ratio=1.125, hyp_len=12858, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.109.1.32-3.75.1.15-3.14.2.98-19.61.2.59-13.31.pth, bkmy
BLEU = 12.02, 39.8/16.9/8.0/3.9 (BP=1.000, ratio=1.060, hyp_len=12960, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.110.1.33-3.77.1.14-3.14.2.95-19.02.2.58-13.23.pth, mybk
BLEU = 9.91, 34.7/13.4/6.3/3.3 (BP=1.000, ratio=1.099, hyp_len=12565, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.110.1.33-3.77.1.14-3.14.2.95-19.02.2.58-13.23.pth, bkmy
BLEU = 11.50, 39.3/16.3/7.5/3.6 (BP=1.000, ratio=1.060, hyp_len=12960, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.111.1.31-3.72.1.14-3.11.2.94-18.85.2.63-13.88.pth, mybk
BLEU = 9.78, 34.8/13.4/6.1/3.2 (BP=1.000, ratio=1.103, hyp_len=12604, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.111.1.31-3.72.1.14-3.11.2.94-18.85.2.63-13.88.pth, bkmy
BLEU = 12.08, 39.2/16.8/8.1/4.0 (BP=1.000, ratio=1.078, hyp_len=13186, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.112.1.34-3.83.1.16-3.21.2.93-18.79.2.60-13.44.pth, mybk
BLEU = 10.02, 34.4/13.4/6.4/3.4 (BP=1.000, ratio=1.100, hyp_len=12570, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.112.1.34-3.83.1.16-3.21.2.93-18.79.2.60-13.44.pth, bkmy
BLEU = 11.72, 39.0/16.5/7.8/3.8 (BP=1.000, ratio=1.068, hyp_len=13068, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.113.1.33-3.79.1.16-3.19.3.02-20.40.2.65-14.14.pth, mybk
BLEU = 10.29, 34.7/13.6/6.7/3.5 (BP=1.000, ratio=1.105, hyp_len=12627, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.113.1.33-3.79.1.16-3.19.3.02-20.40.2.65-14.14.pth, bkmy
BLEU = 11.52, 38.3/16.2/7.7/3.7 (BP=1.000, ratio=1.100, hyp_len=13460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.96-52.41.3.73-41.55.3.41-30.19.3.29-26.84.pth, mybk
BLEU = 0.55, 26.4/2.6/0.2/0.0 (BP=0.786, ratio=0.806, hyp_len=9217, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.96-52.41.3.73-41.55.3.41-30.19.3.29-26.84.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/1.9/0.0/0.0 (BP=1.000, ratio=1.331, hyp_len=16279, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.114.1.28-3.61.1.11-3.05.3.00-20.03.2.61-13.54.pth, mybk
BLEU = 9.96, 34.5/13.3/6.4/3.4 (BP=1.000, ratio=1.106, hyp_len=12644, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.114.1.28-3.61.1.11-3.05.3.00-20.03.2.61-13.54.pth, bkmy
BLEU = 11.34, 38.7/16.1/7.4/3.6 (BP=1.000, ratio=1.084, hyp_len=13253, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.115.1.29-3.64.1.09-2.99.2.99-19.83.2.60-13.45.pth, mybk
BLEU = 9.71, 34.3/13.1/6.2/3.2 (BP=1.000, ratio=1.103, hyp_len=12605, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.115.1.29-3.64.1.09-2.99.2.99-19.83.2.60-13.45.pth, bkmy
BLEU = 11.84, 39.3/16.5/7.8/3.9 (BP=1.000, ratio=1.065, hyp_len=13030, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.116.1.25-3.51.1.08-2.94.2.96-19.34.2.60-13.47.pth, mybk
BLEU = 9.78, 34.5/13.0/6.2/3.3 (BP=1.000, ratio=1.110, hyp_len=12687, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.116.1.25-3.51.1.08-2.94.2.96-19.34.2.60-13.47.pth, bkmy
BLEU = 11.40, 38.5/16.1/7.5/3.6 (BP=1.000, ratio=1.076, hyp_len=13160, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.117.1.27-3.56.1.10-3.00.2.99-19.93.2.63-13.87.pth, mybk
BLEU = 10.00, 34.7/13.4/6.4/3.3 (BP=1.000, ratio=1.083, hyp_len=12386, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.117.1.27-3.56.1.10-3.00.2.99-19.93.2.63-13.87.pth, bkmy
BLEU = 11.98, 39.4/16.8/7.9/3.9 (BP=1.000, ratio=1.078, hyp_len=13189, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.118.1.24-3.45.1.08-2.94.3.01-20.26.2.61-13.64.pth, mybk
BLEU = 9.87, 34.3/13.4/6.3/3.3 (BP=1.000, ratio=1.094, hyp_len=12508, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.118.1.24-3.45.1.08-2.94.3.01-20.26.2.61-13.64.pth, bkmy
BLEU = 12.40, 39.6/17.1/8.3/4.2 (BP=1.000, ratio=1.060, hyp_len=12967, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.119.1.25-3.50.1.06-2.90.3.03-20.71.2.64-13.98.pth, mybk
BLEU = 10.33, 35.0/13.7/6.7/3.5 (BP=1.000, ratio=1.096, hyp_len=12524, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.119.1.25-3.50.1.06-2.90.3.03-20.71.2.64-13.98.pth, bkmy
BLEU = 11.28, 38.6/16.0/7.4/3.5 (BP=1.000, ratio=1.077, hyp_len=13173, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.120.1.22-3.39.1.06-2.88.3.01-20.32.2.67-14.42.pth, mybk
BLEU = 9.47, 33.9/12.7/6.0/3.1 (BP=1.000, ratio=1.117, hyp_len=12769, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.120.1.22-3.39.1.06-2.88.3.01-20.32.2.67-14.42.pth, bkmy
BLEU = 11.83, 38.8/16.2/7.9/3.9 (BP=1.000, ratio=1.073, hyp_len=13118, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.121.1.23-3.43.1.04-2.82.2.99-19.94.2.65-14.21.pth, mybk
BLEU = 9.79, 34.8/13.3/6.3/3.2 (BP=1.000, ratio=1.097, hyp_len=12538, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.121.1.23-3.43.1.04-2.82.2.99-19.94.2.65-14.21.pth, bkmy
BLEU = 11.75, 38.9/16.4/7.7/3.9 (BP=1.000, ratio=1.080, hyp_len=13212, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.122.1.22-3.39.1.05-2.86.3.05-21.19.2.68-14.57.pth, mybk
BLEU = 9.94, 35.2/13.6/6.4/3.2 (BP=1.000, ratio=1.088, hyp_len=12439, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.122.1.22-3.39.1.05-2.86.3.05-21.19.2.68-14.57.pth, bkmy
BLEU = 11.90, 39.0/16.6/7.9/3.9 (BP=1.000, ratio=1.092, hyp_len=13360, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.123.1.21-3.35.1.04-2.82.3.06-21.32.2.68-14.58.pth, mybk
BLEU = 9.89, 34.7/13.5/6.3/3.2 (BP=1.000, ratio=1.102, hyp_len=12599, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.123.1.21-3.35.1.04-2.82.3.06-21.32.2.68-14.58.pth, bkmy
BLEU = 11.80, 38.9/16.5/7.8/3.9 (BP=1.000, ratio=1.078, hyp_len=13182, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.87-48.17.3.58-35.77.3.36-28.72.3.16-23.52.pth, mybk
BLEU = 1.58, 20.6/3.8/0.6/0.1 (BP=1.000, ratio=1.075, hyp_len=12294, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.87-48.17.3.58-35.77.3.36-28.72.3.16-23.52.pth, bkmy
BLEU = 1.20, 22.6/4.0/0.5/0.0 (BP=1.000, ratio=1.084, hyp_len=13256, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.124.1.27-3.56.1.03-2.79.3.02-20.50.2.70-14.83.pth, mybk
BLEU = 10.11, 35.4/13.5/6.4/3.4 (BP=1.000, ratio=1.072, hyp_len=12250, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.124.1.27-3.56.1.03-2.79.3.02-20.50.2.70-14.83.pth, bkmy
BLEU = 11.52, 39.0/16.2/7.5/3.7 (BP=1.000, ratio=1.075, hyp_len=13147, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.125.1.20-3.31.1.02-2.78.3.02-20.43.2.67-14.49.pth, mybk
BLEU = 10.01, 34.9/13.4/6.4/3.3 (BP=1.000, ratio=1.093, hyp_len=12491, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.125.1.20-3.31.1.02-2.78.3.02-20.43.2.67-14.49.pth, bkmy
BLEU = 12.49, 39.6/17.3/8.4/4.2 (BP=1.000, ratio=1.071, hyp_len=13103, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.126.1.19-3.29.1.02-2.78.3.05-21.01.2.69-14.73.pth, mybk
BLEU = 9.82, 34.4/13.3/6.3/3.2 (BP=1.000, ratio=1.115, hyp_len=12742, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.126.1.19-3.29.1.02-2.78.3.05-21.01.2.69-14.73.pth, bkmy
BLEU = 12.01, 38.7/16.8/8.0/4.0 (BP=1.000, ratio=1.094, hyp_len=13386, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.127.1.20-3.33.1.01-2.75.3.02-20.56.2.69-14.71.pth, mybk
BLEU = 9.51, 34.8/13.0/6.0/3.0 (BP=1.000, ratio=1.097, hyp_len=12537, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.127.1.20-3.33.1.01-2.75.3.02-20.56.2.69-14.71.pth, bkmy
BLEU = 11.85, 38.5/16.7/7.9/3.9 (BP=1.000, ratio=1.092, hyp_len=13360, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.128.1.18-3.25.0.99-2.68.3.03-20.78.2.71-14.99.pth, mybk
BLEU = 10.05, 34.9/13.4/6.4/3.4 (BP=1.000, ratio=1.103, hyp_len=12609, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.128.1.18-3.25.0.99-2.68.3.03-20.78.2.71-14.99.pth, bkmy
BLEU = 11.53, 38.6/16.4/7.6/3.6 (BP=1.000, ratio=1.091, hyp_len=13344, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.129.1.15-3.17.0.98-2.66.3.05-21.03.2.69-14.68.pth, mybk
BLEU = 9.89, 35.0/13.4/6.4/3.2 (BP=1.000, ratio=1.107, hyp_len=12655, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.129.1.15-3.17.0.98-2.66.3.05-21.03.2.69-14.68.pth, bkmy
BLEU = 11.84, 39.0/16.7/7.8/3.9 (BP=1.000, ratio=1.075, hyp_len=13153, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.130.1.14-3.14.1.01-2.75.3.08-21.82.2.70-14.92.pth, mybk
BLEU = 9.91, 34.4/13.2/6.3/3.4 (BP=1.000, ratio=1.102, hyp_len=12600, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.130.1.14-3.14.1.01-2.75.3.08-21.82.2.70-14.92.pth, bkmy
BLEU = 11.70, 38.6/16.3/7.7/3.8 (BP=1.000, ratio=1.070, hyp_len=13091, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.131.1.13-3.11.0.99-2.69.3.08-21.84.2.70-14.94.pth, mybk
BLEU = 10.01, 35.5/13.6/6.4/3.3 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.131.1.13-3.11.0.99-2.69.3.08-21.84.2.70-14.94.pth, bkmy
BLEU = 11.49, 38.4/16.3/7.5/3.7 (BP=1.000, ratio=1.075, hyp_len=13153, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.132.1.15-3.16.0.97-2.63.3.14-23.00.2.75-15.58.pth, mybk
BLEU = 9.65, 34.2/13.1/6.2/3.1 (BP=1.000, ratio=1.115, hyp_len=12747, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.132.1.15-3.16.0.97-2.63.3.14-23.00.2.75-15.58.pth, bkmy
BLEU = 11.88, 38.3/16.4/7.9/4.0 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.133.1.11-3.05.0.97-2.63.3.07-21.63.2.77-15.88.pth, mybk
BLEU = 9.84, 34.7/13.4/6.3/3.2 (BP=1.000, ratio=1.105, hyp_len=12631, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.133.1.11-3.05.0.97-2.63.3.07-21.63.2.77-15.88.pth, bkmy
BLEU = 11.83, 38.4/16.4/7.9/4.0 (BP=1.000, ratio=1.077, hyp_len=13172, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.70-40.59.3.41-30.37.3.29-26.78.3.08-21.86.pth, mybk
BLEU = 2.08, 25.9/4.2/0.8/0.3 (BP=0.904, ratio=0.908, hyp_len=10379, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.70-40.59.3.41-30.37.3.29-26.78.3.08-21.86.pth, bkmy
BLEU = 0.09, 1.5/0.3/0.0/0.0 (BP=1.000, ratio=12.443, hyp_len=152185, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.134.1.12-3.05.0.94-2.55.3.09-22.00.2.73-15.39.pth, mybk
BLEU = 10.55, 35.7/14.0/6.9/3.6 (BP=1.000, ratio=1.089, hyp_len=12451, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.134.1.12-3.05.0.94-2.55.3.09-22.00.2.73-15.39.pth, bkmy
BLEU = 11.79, 38.1/16.2/7.9/4.0 (BP=1.000, ratio=1.082, hyp_len=13236, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.135.1.10-3.01.0.99-2.70.3.14-23.10.2.79-16.27.pth, mybk
BLEU = 10.15, 35.2/13.7/6.6/3.4 (BP=1.000, ratio=1.101, hyp_len=12588, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.135.1.10-3.01.0.99-2.70.3.14-23.10.2.79-16.27.pth, bkmy
BLEU = 11.64, 38.4/16.4/7.7/3.8 (BP=1.000, ratio=1.084, hyp_len=13259, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.136.1.07-2.92.0.91-2.49.3.14-23.19.2.75-15.64.pth, mybk
BLEU = 10.37, 35.6/13.9/6.7/3.5 (BP=1.000, ratio=1.084, hyp_len=12388, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.136.1.07-2.92.0.91-2.49.3.14-23.19.2.75-15.64.pth, bkmy
BLEU = 11.73, 38.6/16.5/7.8/3.8 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.137.1.09-2.98.0.93-2.53.3.13-22.81.2.78-16.07.pth, mybk
BLEU = 10.15, 34.3/13.2/6.5/3.6 (BP=1.000, ratio=1.110, hyp_len=12686, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.137.1.09-2.98.0.93-2.53.3.13-22.81.2.78-16.07.pth, bkmy
BLEU = 12.01, 38.5/16.7/8.0/4.0 (BP=1.000, ratio=1.086, hyp_len=13286, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.138.1.07-2.90.0.92-2.51.3.14-23.11.2.79-16.25.pth, mybk
BLEU = 10.05, 34.8/13.6/6.4/3.4 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.138.1.07-2.90.0.92-2.51.3.14-23.11.2.79-16.25.pth, bkmy
BLEU = 11.30, 37.8/15.9/7.4/3.7 (BP=1.000, ratio=1.107, hyp_len=13539, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.139.1.10-3.00.0.93-2.54.3.13-22.77.2.78-16.10.pth, mybk
BLEU = 10.06, 34.9/13.7/6.4/3.4 (BP=1.000, ratio=1.099, hyp_len=12559, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.139.1.10-3.00.0.93-2.54.3.13-22.77.2.78-16.10.pth, bkmy
BLEU = 11.68, 38.4/16.2/7.8/3.8 (BP=1.000, ratio=1.087, hyp_len=13292, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.140.1.07-2.91.0.91-2.48.3.17-23.83.2.79-16.35.pth, mybk
BLEU = 10.36, 34.6/13.8/6.7/3.6 (BP=1.000, ratio=1.120, hyp_len=12801, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.140.1.07-2.91.0.91-2.48.3.17-23.83.2.79-16.35.pth, bkmy
BLEU = 11.65, 38.3/16.1/7.7/3.9 (BP=1.000, ratio=1.086, hyp_len=13288, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.141.1.10-3.01.0.94-2.55.3.16-23.68.2.79-16.32.pth, mybk
BLEU = 10.15, 34.8/13.6/6.6/3.4 (BP=1.000, ratio=1.096, hyp_len=12531, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.141.1.10-3.01.0.94-2.55.3.16-23.68.2.79-16.32.pth, bkmy
BLEU = 11.84, 38.3/16.6/7.8/4.0 (BP=1.000, ratio=1.097, hyp_len=13421, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.142.1.06-2.88.0.88-2.42.3.17-23.91.2.78-16.09.pth, mybk
BLEU = 9.85, 34.5/13.2/6.3/3.3 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.142.1.06-2.88.0.88-2.42.3.17-23.91.2.78-16.09.pth, bkmy
BLEU = 11.68, 39.4/16.6/7.7/3.7 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.143.1.08-2.96.0.92-2.50.3.19-24.21.2.80-16.41.pth, mybk
BLEU = 9.56, 34.2/12.8/6.0/3.2 (BP=1.000, ratio=1.109, hyp_len=12681, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.143.1.08-2.96.0.92-2.50.3.19-24.21.2.80-16.41.pth, bkmy
BLEU = 11.90, 39.1/16.9/7.8/3.9 (BP=1.000, ratio=1.069, hyp_len=13078, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.63-37.79.3.32-27.53.3.26-26.04.3.02-20.46.pth, mybk
BLEU = 3.92, 23.3/5.4/2.1/0.9 (BP=1.000, ratio=1.073, hyp_len=12272, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.63-37.79.3.32-27.53.3.26-26.04.3.02-20.46.pth, bkmy
BLEU = 0.85, 15.2/2.8/0.4/0.0 (BP=1.000, ratio=1.903, hyp_len=23279, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.144.1.10-3.02.0.96-2.60.3.23-25.23.2.80-16.50.pth, mybk
BLEU = 9.59, 34.0/12.8/6.0/3.2 (BP=1.000, ratio=1.120, hyp_len=12805, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.144.1.10-3.02.0.96-2.60.3.23-25.23.2.80-16.50.pth, bkmy
BLEU = 11.42, 38.3/16.2/7.5/3.7 (BP=1.000, ratio=1.082, hyp_len=13230, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.145.1.03-2.79.0.87-2.39.3.20-24.51.2.77-16.00.pth, mybk
BLEU = 9.77, 34.9/13.5/6.3/3.1 (BP=1.000, ratio=1.100, hyp_len=12570, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.145.1.03-2.79.0.87-2.39.3.20-24.51.2.77-16.00.pth, bkmy
BLEU = 11.73, 38.5/16.2/7.8/3.9 (BP=1.000, ratio=1.069, hyp_len=13074, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.146.1.02-2.78.0.87-2.39.3.21-24.85.2.80-16.45.pth, mybk
BLEU = 9.84, 34.2/13.2/6.3/3.3 (BP=1.000, ratio=1.104, hyp_len=12620, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.146.1.02-2.78.0.87-2.39.3.21-24.85.2.80-16.45.pth, bkmy
BLEU = 11.45, 38.9/16.3/7.6/3.6 (BP=1.000, ratio=1.064, hyp_len=13014, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.147.1.02-2.77.0.85-2.34.3.22-24.99.2.79-16.28.pth, mybk
BLEU = 10.29, 34.9/13.5/6.6/3.6 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.147.1.02-2.77.0.85-2.34.3.22-24.99.2.79-16.28.pth, bkmy
BLEU = 11.52, 38.7/16.2/7.5/3.7 (BP=1.000, ratio=1.080, hyp_len=13213, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.148.1.02-2.77.0.86-2.37.3.22-25.09.2.78-16.08.pth, mybk
BLEU = 9.77, 34.0/13.1/6.3/3.3 (BP=1.000, ratio=1.124, hyp_len=12848, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.148.1.02-2.77.0.86-2.37.3.22-25.09.2.78-16.08.pth, bkmy
BLEU = 12.09, 38.8/16.4/8.0/4.2 (BP=1.000, ratio=1.081, hyp_len=13222, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.149.0.99-2.69.0.83-2.30.3.19-24.22.2.82-16.77.pth, mybk
BLEU = 10.29, 35.3/13.8/6.6/3.5 (BP=1.000, ratio=1.086, hyp_len=12416, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.149.0.99-2.69.0.83-2.30.3.19-24.22.2.82-16.77.pth, bkmy
BLEU = 11.93, 38.6/16.5/7.9/4.0 (BP=1.000, ratio=1.081, hyp_len=13218, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.150.1.03-2.79.0.83-2.29.3.17-23.84.2.84-17.07.pth, mybk
BLEU = 10.06, 35.0/13.6/6.5/3.3 (BP=1.000, ratio=1.082, hyp_len=12375, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.150.1.03-2.79.0.83-2.29.3.17-23.84.2.84-17.07.pth, bkmy
BLEU = 11.79, 38.8/16.4/8.0/3.8 (BP=1.000, ratio=1.076, hyp_len=13156, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.151.0.99-2.69.0.85-2.35.3.23-25.19.2.87-17.60.pth, mybk
BLEU = 9.74, 34.0/13.0/6.2/3.3 (BP=1.000, ratio=1.113, hyp_len=12720, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.151.0.99-2.69.0.85-2.35.3.23-25.19.2.87-17.60.pth, bkmy
BLEU = 11.64, 38.5/16.2/7.8/3.8 (BP=1.000, ratio=1.089, hyp_len=13318, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.152.0.99-2.68.0.82-2.26.3.25-25.90.2.87-17.71.pth, mybk
BLEU = 9.67, 34.0/12.8/6.3/3.2 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.152.0.99-2.68.0.82-2.26.3.25-25.90.2.87-17.71.pth, bkmy
BLEU = 11.74, 38.4/16.4/7.8/3.9 (BP=1.000, ratio=1.091, hyp_len=13349, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.153.1.01-2.74.0.83-2.29.3.24-25.65.2.86-17.46.pth, mybk
BLEU = 9.76, 33.6/12.8/6.3/3.3 (BP=1.000, ratio=1.113, hyp_len=12728, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.153.1.01-2.74.0.83-2.29.3.24-25.65.2.86-17.46.pth, bkmy
BLEU = 12.27, 39.4/17.0/8.2/4.1 (BP=1.000, ratio=1.073, hyp_len=13126, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.59-36.37.3.28-26.52.3.19-24.24.2.98-19.60.pth, mybk
BLEU = 4.34, 25.5/6.7/2.3/0.9 (BP=0.988, ratio=0.988, hyp_len=11299, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.59-36.37.3.28-26.52.3.19-24.24.2.98-19.60.pth, bkmy
BLEU = 2.70, 23.0/5.8/1.5/0.3 (BP=1.000, ratio=1.204, hyp_len=14724, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.154.0.97-2.64.0.84-2.31.3.27-26.20.2.87-17.56.pth, mybk
BLEU = 9.76, 33.9/12.9/6.3/3.3 (BP=1.000, ratio=1.112, hyp_len=12718, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.154.0.97-2.64.0.84-2.31.3.27-26.20.2.87-17.56.pth, bkmy
BLEU = 11.94, 38.3/16.5/7.9/4.1 (BP=1.000, ratio=1.093, hyp_len=13370, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.155.0.97-2.63.0.81-2.24.3.22-25.03.2.86-17.54.pth, mybk
BLEU = 9.83, 34.4/13.4/6.3/3.2 (BP=1.000, ratio=1.099, hyp_len=12569, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.155.0.97-2.63.0.81-2.24.3.22-25.03.2.86-17.54.pth, bkmy
BLEU = 11.68, 38.7/16.4/7.8/3.8 (BP=1.000, ratio=1.072, hyp_len=13112, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.156.0.97-2.64.0.81-2.26.3.25-25.72.2.85-17.37.pth, mybk
BLEU = 9.36, 33.9/12.9/6.0/3.0 (BP=1.000, ratio=1.116, hyp_len=12753, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.156.0.97-2.64.0.81-2.26.3.25-25.72.2.85-17.37.pth, bkmy
BLEU = 11.43, 38.3/16.1/7.6/3.6 (BP=1.000, ratio=1.089, hyp_len=13318, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.157.0.96-2.60.0.80-2.22.3.24-25.60.2.88-17.75.pth, mybk
BLEU = 10.08, 34.6/13.6/6.5/3.4 (BP=1.000, ratio=1.099, hyp_len=12560, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.157.0.96-2.60.0.80-2.22.3.24-25.60.2.88-17.75.pth, bkmy
BLEU = 11.65, 38.6/16.3/7.7/3.8 (BP=1.000, ratio=1.100, hyp_len=13459, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.158.0.95-2.57.0.82-2.26.3.29-26.94.2.90-18.14.pth, mybk
BLEU = 9.72, 34.7/13.3/6.2/3.1 (BP=1.000, ratio=1.097, hyp_len=12536, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.158.0.95-2.57.0.82-2.26.3.29-26.94.2.90-18.14.pth, bkmy
BLEU = 11.81, 38.5/16.4/7.9/3.9 (BP=1.000, ratio=1.082, hyp_len=13232, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.159.0.96-2.61.0.81-2.25.3.31-27.27.2.89-17.99.pth, mybk
BLEU = 9.47, 34.3/12.9/6.0/3.0 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.159.0.96-2.61.0.81-2.25.3.31-27.27.2.89-17.99.pth, bkmy
BLEU = 11.19, 38.2/15.9/7.5/3.5 (BP=1.000, ratio=1.082, hyp_len=13237, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.160.0.98-2.67.0.80-2.22.3.29-26.80.2.87-17.58.pth, mybk
BLEU = 9.45, 34.3/13.0/6.1/2.9 (BP=1.000, ratio=1.100, hyp_len=12575, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.160.0.98-2.67.0.80-2.22.3.29-26.80.2.87-17.58.pth, bkmy
BLEU = 11.81, 38.4/16.1/7.8/4.0 (BP=1.000, ratio=1.080, hyp_len=13206, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.161.0.92-2.52.0.78-2.18.3.23-25.38.2.93-18.79.pth, mybk
BLEU = 9.40, 34.5/13.0/6.0/2.9 (BP=1.000, ratio=1.091, hyp_len=12475, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.161.0.92-2.52.0.78-2.18.3.23-25.38.2.93-18.79.pth, bkmy
BLEU = 11.80, 38.5/16.2/7.8/4.0 (BP=1.000, ratio=1.092, hyp_len=13354, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.162.0.99-2.69.0.80-2.23.3.30-27.14.2.89-17.95.pth, mybk
BLEU = 8.96, 33.6/12.2/5.7/2.8 (BP=1.000, ratio=1.108, hyp_len=12666, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.162.0.99-2.69.0.80-2.23.3.30-27.14.2.89-17.95.pth, bkmy
BLEU = 11.71, 38.8/16.6/7.8/3.8 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.163.0.93-2.54.0.77-2.17.3.33-27.96.2.92-18.60.pth, mybk
BLEU = 10.16, 34.3/13.6/6.7/3.4 (BP=1.000, ratio=1.108, hyp_len=12672, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.163.0.93-2.54.0.77-2.17.3.33-27.96.2.92-18.60.pth, bkmy
BLEU = 11.22, 37.9/15.9/7.4/3.6 (BP=1.000, ratio=1.087, hyp_len=13299, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.57-35.42.3.31-27.35.3.15-23.29.2.93-18.69.pth, mybk
BLEU = 4.21, 22.7/6.3/2.2/1.0 (BP=1.000, ratio=1.130, hyp_len=12919, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.57-35.42.3.31-27.35.3.15-23.29.2.93-18.69.pth, bkmy
BLEU = 1.62, 13.6/3.6/1.0/0.1 (BP=1.000, ratio=2.097, hyp_len=25649, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.164.0.92-2.50.0.79-2.20.3.32-27.57.2.96-19.38.pth, mybk
BLEU = 9.71, 34.1/13.1/6.2/3.2 (BP=1.000, ratio=1.110, hyp_len=12693, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.164.0.92-2.50.0.79-2.20.3.32-27.57.2.96-19.38.pth, bkmy
BLEU = 11.72, 38.5/16.1/7.7/3.9 (BP=1.000, ratio=1.082, hyp_len=13231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.165.0.95-2.59.0.78-2.18.3.33-27.82.2.95-19.12.pth, mybk
BLEU = 9.76, 33.9/12.9/6.3/3.3 (BP=1.000, ratio=1.124, hyp_len=12844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.165.0.95-2.59.0.78-2.18.3.33-27.82.2.95-19.12.pth, bkmy
BLEU = 11.13, 38.0/15.7/7.3/3.5 (BP=1.000, ratio=1.090, hyp_len=13335, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.166.0.97-2.64.0.76-2.14.3.34-28.31.2.93-18.77.pth, mybk
BLEU = 9.66, 34.1/13.0/6.2/3.2 (BP=1.000, ratio=1.114, hyp_len=12733, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.166.0.97-2.64.0.76-2.14.3.34-28.31.2.93-18.77.pth, bkmy
BLEU = 11.19, 37.7/15.8/7.3/3.6 (BP=1.000, ratio=1.078, hyp_len=13191, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.167.0.93-2.54.0.80-2.22.3.33-27.81.2.94-18.90.pth, mybk
BLEU = 9.53, 34.4/12.9/6.1/3.1 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.167.0.93-2.54.0.80-2.22.3.33-27.81.2.94-18.90.pth, bkmy
BLEU = 11.09, 37.2/15.5/7.3/3.6 (BP=1.000, ratio=1.109, hyp_len=13563, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.168.0.92-2.51.0.76-2.14.3.36-28.68.2.98-19.77.pth, mybk
BLEU = 9.23, 34.1/12.7/5.8/2.9 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.168.0.92-2.51.0.76-2.14.3.36-28.68.2.98-19.77.pth, bkmy
BLEU = 11.44, 37.6/16.0/7.5/3.8 (BP=1.000, ratio=1.096, hyp_len=13408, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.169.0.96-2.61.0.79-2.20.3.33-27.82.3.01-20.31.pth, mybk
BLEU = 9.73, 34.5/13.2/6.1/3.2 (BP=1.000, ratio=1.105, hyp_len=12630, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.169.0.96-2.61.0.79-2.20.3.33-27.82.3.01-20.31.pth, bkmy
BLEU = 11.78, 38.6/16.5/7.8/3.9 (BP=1.000, ratio=1.088, hyp_len=13303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.170.0.92-2.52.0.74-2.10.3.32-27.54.2.98-19.70.pth, mybk
BLEU = 9.68, 33.9/12.8/6.1/3.3 (BP=1.000, ratio=1.113, hyp_len=12728, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.170.0.92-2.52.0.74-2.10.3.32-27.54.2.98-19.70.pth, bkmy
BLEU = 11.96, 38.3/16.5/8.1/4.0 (BP=1.000, ratio=1.079, hyp_len=13202, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.171.0.93-2.53.0.77-2.17.3.33-27.94.3.00-20.11.pth, mybk
BLEU = 9.72, 34.3/13.0/6.2/3.2 (BP=1.000, ratio=1.107, hyp_len=12650, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.171.0.93-2.53.0.77-2.17.3.33-27.94.3.00-20.11.pth, bkmy
BLEU = 11.73, 37.9/16.3/7.8/3.9 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.172.0.88-2.41.0.73-2.08.3.37-28.99.2.98-19.70.pth, mybk
BLEU = 9.33, 33.7/12.4/5.9/3.1 (BP=1.000, ratio=1.115, hyp_len=12741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.172.0.88-2.41.0.73-2.08.3.37-28.99.2.98-19.70.pth, bkmy
BLEU = 11.34, 38.0/15.8/7.5/3.7 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.173.0.96-2.62.0.75-2.11.3.36-28.65.3.01-20.30.pth, mybk
BLEU = 9.62, 33.7/12.6/6.1/3.3 (BP=1.000, ratio=1.118, hyp_len=12781, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.173.0.96-2.62.0.75-2.11.3.36-28.65.3.01-20.30.pth, bkmy
BLEU = 12.01, 38.7/16.6/8.1/4.0 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.49-32.85.3.23-25.20.3.11-22.37.2.88-17.77.pth, mybk
BLEU = 3.84, 21.7/6.0/2.0/0.8 (BP=1.000, ratio=1.163, hyp_len=13292, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.49-32.85.3.23-25.20.3.11-22.37.2.88-17.77.pth, bkmy
BLEU = 3.69, 29.3/8.8/2.0/0.4 (BP=1.000, ratio=1.053, hyp_len=12876, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.174.0.86-2.36.0.71-2.03.3.36-28.90.3.02-20.51.pth, mybk
BLEU = 9.84, 34.8/13.3/6.3/3.2 (BP=1.000, ratio=1.102, hyp_len=12603, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.174.0.86-2.36.0.71-2.03.3.36-28.90.3.02-20.51.pth, bkmy
BLEU = 12.04, 38.8/16.5/8.0/4.1 (BP=1.000, ratio=1.080, hyp_len=13210, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.175.0.85-2.34.0.70-2.02.3.33-27.86.2.99-19.80.pth, mybk
BLEU = 10.06, 35.0/13.2/6.5/3.4 (BP=1.000, ratio=1.087, hyp_len=12424, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.175.0.85-2.34.0.70-2.02.3.33-27.86.2.99-19.80.pth, bkmy
BLEU = 11.47, 38.3/15.9/7.6/3.7 (BP=1.000, ratio=1.080, hyp_len=13214, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.176.0.84-2.31.0.71-2.04.3.37-28.99.3.00-20.03.pth, mybk
BLEU = 9.73, 34.5/13.0/6.2/3.2 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.176.0.84-2.31.0.71-2.04.3.37-28.99.3.00-20.03.pth, bkmy
BLEU = 11.52, 38.2/16.0/7.6/3.8 (BP=1.000, ratio=1.076, hyp_len=13165, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.177.0.85-2.34.0.69-2.00.3.38-29.27.3.03-20.73.pth, mybk
BLEU = 9.58, 34.2/12.8/6.1/3.2 (BP=1.000, ratio=1.115, hyp_len=12742, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.177.0.85-2.34.0.69-2.00.3.38-29.27.3.03-20.73.pth, bkmy
BLEU = 11.66, 38.4/16.2/7.7/3.8 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.178.0.85-2.35.0.71-2.03.3.42-30.60.3.01-20.37.pth, mybk
BLEU = 9.47, 33.7/12.6/6.0/3.1 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.178.0.85-2.35.0.71-2.03.3.42-30.60.3.01-20.37.pth, bkmy
BLEU = 11.60, 38.1/16.0/7.6/3.9 (BP=1.000, ratio=1.086, hyp_len=13281, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.179.0.87-2.40.0.71-2.03.3.46-31.73.3.06-21.31.pth, mybk
BLEU = 9.89, 34.1/13.2/6.4/3.3 (BP=1.000, ratio=1.102, hyp_len=12594, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.179.0.87-2.40.0.71-2.03.3.46-31.73.3.06-21.31.pth, bkmy
BLEU = 11.03, 37.7/15.8/7.2/3.5 (BP=1.000, ratio=1.094, hyp_len=13384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.180.0.90-2.46.0.76-2.15.3.43-30.87.3.06-21.35.pth, mybk
BLEU = 9.83, 34.3/13.2/6.3/3.2 (BP=1.000, ratio=1.098, hyp_len=12549, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.180.0.90-2.46.0.76-2.15.3.43-30.87.3.06-21.35.pth, bkmy
BLEU = 11.80, 38.9/16.5/7.8/3.9 (BP=1.000, ratio=1.068, hyp_len=13067, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.181.0.84-2.32.0.72-2.05.3.44-31.04.3.10-22.15.pth, mybk
BLEU = 9.77, 34.2/13.2/6.3/3.2 (BP=1.000, ratio=1.119, hyp_len=12791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.181.0.84-2.32.0.72-2.05.3.44-31.04.3.10-22.15.pth, bkmy
BLEU = 12.13, 39.0/16.9/8.1/4.1 (BP=1.000, ratio=1.063, hyp_len=13005, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.182.0.84-2.31.0.69-1.99.3.44-31.27.3.08-21.69.pth, mybk
BLEU = 9.51, 33.2/12.6/6.1/3.2 (BP=1.000, ratio=1.134, hyp_len=12961, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.182.0.84-2.31.0.69-1.99.3.44-31.27.3.08-21.69.pth, bkmy
BLEU = 11.81, 38.4/16.2/7.8/4.0 (BP=1.000, ratio=1.087, hyp_len=13295, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.183.0.86-2.36.0.75-2.13.3.46-31.81.3.10-22.16.pth, mybk
BLEU = 9.34, 33.7/12.6/5.9/3.0 (BP=1.000, ratio=1.113, hyp_len=12725, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.183.0.86-2.36.0.75-2.13.3.46-31.81.3.10-22.16.pth, bkmy
BLEU = 11.37, 38.3/15.8/7.5/3.7 (BP=1.000, ratio=1.080, hyp_len=13209, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.38-29.27.3.08-21.83.3.05-21.08.2.82-16.74.pth, mybk
BLEU = 3.93, 22.0/6.0/2.1/0.8 (BP=1.000, ratio=1.166, hyp_len=13330, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.38-29.27.3.08-21.83.3.05-21.08.2.82-16.74.pth, bkmy
BLEU = 4.54, 30.4/9.2/2.6/0.6 (BP=1.000, ratio=1.033, hyp_len=12637, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.184.0.82-2.28.0.70-2.01.3.42-30.69.3.05-21.04.pth, mybk
BLEU = 9.95, 34.4/13.2/6.4/3.3 (BP=1.000, ratio=1.106, hyp_len=12643, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.184.0.82-2.28.0.70-2.01.3.42-30.69.3.05-21.04.pth, bkmy
BLEU = 11.82, 38.7/16.5/7.9/3.9 (BP=1.000, ratio=1.081, hyp_len=13220, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.185.0.82-2.27.0.69-2.00.3.47-32.10.3.06-21.25.pth, mybk
BLEU = 9.56, 33.7/12.7/6.1/3.2 (BP=1.000, ratio=1.133, hyp_len=12949, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.185.0.82-2.27.0.69-2.00.3.47-32.10.3.06-21.25.pth, bkmy
BLEU = 11.76, 39.2/16.6/7.7/3.8 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.186.0.83-2.30.0.70-2.01.3.44-31.23.3.07-21.50.pth, mybk
BLEU = 9.39, 33.8/12.7/6.0/3.0 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.186.0.83-2.30.0.70-2.01.3.44-31.23.3.07-21.50.pth, bkmy
BLEU = 11.49, 38.2/15.9/7.5/3.8 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.187.0.91-2.49.0.70-2.01.3.47-32.06.3.07-21.60.pth, mybk
BLEU = 9.48, 33.4/12.7/6.0/3.2 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.187.0.91-2.49.0.70-2.01.3.47-32.06.3.07-21.60.pth, bkmy
BLEU = 11.88, 39.2/16.6/7.8/3.9 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.188.0.80-2.22.0.66-1.94.3.53-34.10.3.05-21.07.pth, mybk
BLEU = 9.56, 33.5/12.6/6.1/3.3 (BP=1.000, ratio=1.116, hyp_len=12754, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.188.0.80-2.22.0.66-1.94.3.53-34.10.3.05-21.07.pth, bkmy
BLEU = 11.72, 38.5/16.3/7.8/3.9 (BP=1.000, ratio=1.082, hyp_len=13229, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.189.0.80-2.22.0.71-2.03.3.50-32.98.3.08-21.77.pth, mybk
BLEU = 9.95, 34.0/13.0/6.4/3.5 (BP=1.000, ratio=1.106, hyp_len=12649, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.189.0.80-2.22.0.71-2.03.3.50-32.98.3.08-21.77.pth, bkmy
BLEU = 11.70, 38.2/16.2/7.7/3.9 (BP=1.000, ratio=1.092, hyp_len=13352, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.190.0.80-2.21.0.67-1.96.3.52-33.76.3.04-20.95.pth, mybk
BLEU = 9.44, 33.5/12.7/6.0/3.1 (BP=1.000, ratio=1.121, hyp_len=12813, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.190.0.80-2.21.0.67-1.96.3.52-33.76.3.04-20.95.pth, bkmy
BLEU = 11.35, 38.5/16.0/7.4/3.7 (BP=1.000, ratio=1.079, hyp_len=13198, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.191.0.79-2.21.0.64-1.90.3.56-35.20.3.10-22.26.pth, mybk
BLEU = 9.28, 33.0/12.4/5.9/3.1 (BP=1.000, ratio=1.115, hyp_len=12744, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.191.0.79-2.21.0.64-1.90.3.56-35.20.3.10-22.26.pth, bkmy
BLEU = 11.67, 38.0/16.1/7.7/3.9 (BP=1.000, ratio=1.100, hyp_len=13456, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.192.0.85-2.34.0.67-1.95.3.55-34.89.3.10-22.10.pth, mybk
BLEU = 9.38, 34.6/12.8/5.9/2.9 (BP=1.000, ratio=1.100, hyp_len=12573, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.192.0.85-2.34.0.67-1.95.3.55-34.89.3.10-22.10.pth, bkmy
BLEU = 11.22, 37.7/15.6/7.4/3.6 (BP=1.000, ratio=1.108, hyp_len=13551, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.193.0.80-2.22.0.65-1.91.3.53-34.06.3.11-22.41.pth, mybk
BLEU = 9.67, 34.1/12.9/6.2/3.2 (BP=1.000, ratio=1.112, hyp_len=12713, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.193.0.80-2.22.0.65-1.91.3.53-34.06.3.11-22.41.pth, bkmy
BLEU = 11.28, 37.7/15.8/7.3/3.7 (BP=1.000, ratio=1.079, hyp_len=13201, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.95.3.06-21.37.3.03-20.71.2.82-16.71.pth, mybk
BLEU = 4.47, 24.5/6.8/2.4/1.0 (BP=1.000, ratio=1.065, hyp_len=12175, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.95.3.06-21.37.3.03-20.71.2.82-16.71.pth, bkmy
BLEU = 5.58, 29.7/9.9/3.2/1.0 (BP=1.000, ratio=1.103, hyp_len=13490, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.194.0.78-2.18.0.65-1.92.3.46-31.72.3.12-22.65.pth, mybk
BLEU = 9.93, 34.0/13.2/6.4/3.4 (BP=1.000, ratio=1.101, hyp_len=12583, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.194.0.78-2.18.0.65-1.92.3.46-31.72.3.12-22.65.pth, bkmy
BLEU = 11.32, 38.2/15.8/7.4/3.7 (BP=1.000, ratio=1.088, hyp_len=13305, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.195.0.83-2.30.0.71-2.04.3.52-33.94.3.13-22.91.pth, mybk
BLEU = 9.40, 33.2/12.4/5.9/3.2 (BP=1.000, ratio=1.118, hyp_len=12780, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.195.0.83-2.30.0.71-2.04.3.52-33.94.3.13-22.91.pth, bkmy
BLEU = 11.47, 38.1/16.1/7.6/3.7 (BP=1.000, ratio=1.084, hyp_len=13255, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.196.0.77-2.17.0.63-1.87.3.52-33.75.3.12-22.74.pth, mybk
BLEU = 9.70, 33.6/12.8/6.1/3.4 (BP=1.000, ratio=1.104, hyp_len=12622, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.196.0.77-2.17.0.63-1.87.3.52-33.75.3.12-22.74.pth, bkmy
BLEU = 11.55, 38.1/15.9/7.6/3.9 (BP=1.000, ratio=1.089, hyp_len=13325, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.197.0.77-2.15.0.64-1.89.3.55-34.81.3.14-23.14.pth, mybk
BLEU = 9.43, 33.8/12.8/6.0/3.1 (BP=1.000, ratio=1.117, hyp_len=12767, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.197.0.77-2.15.0.64-1.89.3.55-34.81.3.14-23.14.pth, bkmy
BLEU = 11.43, 38.0/15.7/7.4/3.9 (BP=1.000, ratio=1.092, hyp_len=13351, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.198.0.77-2.15.0.64-1.90.3.56-35.05.3.10-22.27.pth, mybk
BLEU = 9.15, 32.9/12.3/5.8/3.0 (BP=1.000, ratio=1.124, hyp_len=12849, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.198.0.77-2.15.0.64-1.90.3.56-35.05.3.10-22.27.pth, bkmy
BLEU = 11.78, 38.5/16.3/7.7/4.0 (BP=1.000, ratio=1.082, hyp_len=13232, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.199.0.82-2.26.0.66-1.93.3.55-34.94.3.13-22.90.pth, mybk
BLEU = 9.61, 33.5/12.7/6.1/3.3 (BP=1.000, ratio=1.106, hyp_len=12645, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.199.0.82-2.26.0.66-1.93.3.55-34.94.3.13-22.90.pth, bkmy
BLEU = 11.74, 38.2/16.1/7.7/4.0 (BP=1.000, ratio=1.091, hyp_len=13348, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.200.0.78-2.18.0.63-1.89.3.54-34.41.3.11-22.43.pth, mybk
BLEU = 9.74, 34.1/13.1/6.2/3.2 (BP=1.000, ratio=1.102, hyp_len=12599, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.200.0.78-2.18.0.63-1.89.3.54-34.41.3.11-22.43.pth, bkmy
BLEU = 11.30, 37.6/15.7/7.4/3.7 (BP=1.000, ratio=1.079, hyp_len=13194, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.201.0.82-2.28.0.65-1.91.3.63-37.66.3.16-23.48.pth, mybk
BLEU = 9.69, 33.9/13.0/6.2/3.2 (BP=1.000, ratio=1.101, hyp_len=12584, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.201.0.82-2.28.0.65-1.91.3.63-37.66.3.16-23.48.pth, bkmy
BLEU = 11.75, 38.2/16.2/7.6/4.0 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.202.0.77-2.15.0.64-1.89.3.57-35.39.3.17-23.70.pth, mybk
BLEU = 9.15, 33.1/12.3/5.7/3.0 (BP=1.000, ratio=1.129, hyp_len=12911, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.202.0.77-2.15.0.64-1.89.3.57-35.39.3.17-23.70.pth, bkmy
BLEU = 11.31, 38.0/16.0/7.4/3.6 (BP=1.000, ratio=1.084, hyp_len=13260, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.203.0.81-2.24.0.62-1.86.3.60-36.69.3.18-24.13.pth, mybk
BLEU = 8.97, 33.0/12.0/5.6/2.9 (BP=1.000, ratio=1.113, hyp_len=12724, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.203.0.81-2.24.0.62-1.86.3.60-36.69.3.18-24.13.pth, bkmy
BLEU = 11.15, 37.7/15.5/7.3/3.6 (BP=1.000, ratio=1.106, hyp_len=13524, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.32-27.73.3.05-21.18.2.96-19.36.2.76-15.78.pth, mybk
BLEU = 4.77, 25.9/7.2/2.6/1.1 (BP=1.000, ratio=1.059, hyp_len=12104, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.32-27.73.3.05-21.18.2.96-19.36.2.76-15.78.pth, bkmy
BLEU = 5.08, 31.0/9.8/2.9/0.8 (BP=1.000, ratio=1.035, hyp_len=12663, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.204.0.74-2.10.0.61-1.84.3.55-34.89.3.21-24.67.pth, mybk
BLEU = 9.32, 33.7/12.2/5.7/3.2 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.204.0.74-2.10.0.61-1.84.3.55-34.89.3.21-24.67.pth, bkmy
BLEU = 11.41, 37.9/15.7/7.4/3.8 (BP=1.000, ratio=1.100, hyp_len=13450, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.205.0.75-2.11.0.65-1.91.3.53-34.24.3.17-23.76.pth, mybk
BLEU = 9.31, 33.4/12.5/5.8/3.1 (BP=1.000, ratio=1.109, hyp_len=12676, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.205.0.75-2.11.0.65-1.91.3.53-34.24.3.17-23.76.pth, bkmy
BLEU = 11.16, 37.8/15.7/7.3/3.6 (BP=1.000, ratio=1.083, hyp_len=13251, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.206.0.75-2.12.0.61-1.84.3.55-34.91.3.18-24.11.pth, mybk
BLEU = 9.46, 33.4/12.7/6.0/3.2 (BP=1.000, ratio=1.123, hyp_len=12842, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.206.0.75-2.12.0.61-1.84.3.55-34.91.3.18-24.11.pth, bkmy
BLEU = 11.35, 37.6/15.8/7.4/3.8 (BP=1.000, ratio=1.094, hyp_len=13386, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.207.0.75-2.12.0.61-1.83.3.55-34.79.3.21-24.88.pth, mybk
BLEU = 9.11, 33.1/12.2/5.8/3.0 (BP=1.000, ratio=1.126, hyp_len=12867, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.207.0.75-2.12.0.61-1.83.3.55-34.79.3.21-24.88.pth, bkmy
BLEU = 10.89, 37.7/15.2/6.9/3.5 (BP=1.000, ratio=1.091, hyp_len=13339, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.208.0.74-2.09.0.64-1.89.3.51-33.56.3.21-24.85.pth, mybk
BLEU = 8.81, 32.4/11.9/5.5/2.9 (BP=1.000, ratio=1.121, hyp_len=12819, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.208.0.74-2.09.0.64-1.89.3.51-33.56.3.21-24.85.pth, bkmy
BLEU = 11.73, 38.7/16.2/7.7/3.9 (BP=1.000, ratio=1.091, hyp_len=13350, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.209.0.74-2.10.0.62-1.86.3.55-34.93.3.20-24.52.pth, mybk
BLEU = 9.60, 33.4/12.4/6.2/3.3 (BP=1.000, ratio=1.113, hyp_len=12724, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.209.0.74-2.10.0.62-1.86.3.55-34.93.3.20-24.52.pth, bkmy
BLEU = 11.24, 38.1/15.7/7.4/3.6 (BP=1.000, ratio=1.096, hyp_len=13408, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.210.0.80-2.22.0.60-1.83.3.60-36.66.3.19-24.39.pth, mybk
BLEU = 9.24, 32.9/12.1/5.8/3.1 (BP=1.000, ratio=1.112, hyp_len=12709, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.210.0.80-2.22.0.60-1.83.3.60-36.66.3.19-24.39.pth, bkmy
BLEU = 11.57, 38.2/15.8/7.6/3.9 (BP=1.000, ratio=1.068, hyp_len=13064, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.211.0.81-2.24.0.61-1.84.3.55-34.83.3.21-24.82.pth, mybk
BLEU = 9.44, 33.7/12.5/6.0/3.2 (BP=1.000, ratio=1.120, hyp_len=12802, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.211.0.81-2.24.0.61-1.84.3.55-34.83.3.21-24.82.pth, bkmy
BLEU = 11.47, 38.1/15.8/7.4/3.9 (BP=1.000, ratio=1.077, hyp_len=13176, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.212.0.74-2.10.0.64-1.90.3.63-37.68.3.24-25.45.pth, mybk
BLEU = 9.48, 33.5/12.7/6.0/3.1 (BP=1.000, ratio=1.120, hyp_len=12805, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.212.0.74-2.10.0.64-1.90.3.63-37.68.3.24-25.45.pth, bkmy
BLEU = 10.36, 36.9/14.8/6.6/3.2 (BP=1.000, ratio=1.098, hyp_len=13430, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.213.0.72-2.06.0.59-1.81.3.61-36.93.3.23-25.17.pth, mybk
BLEU = 9.18, 33.3/12.5/5.8/2.9 (BP=1.000, ratio=1.119, hyp_len=12792, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.213.0.72-2.06.0.59-1.81.3.61-36.93.3.23-25.17.pth, bkmy
BLEU = 11.41, 38.2/16.1/7.5/3.7 (BP=1.000, ratio=1.093, hyp_len=13367, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.27-26.39.3.04-20.98.2.97-19.58.2.72-15.25.pth, mybk
BLEU = 4.64, 24.8/6.9/2.7/1.0 (BP=1.000, ratio=1.147, hyp_len=13110, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.27-26.39.3.04-20.98.2.97-19.58.2.72-15.25.pth, bkmy
BLEU = 6.09, 30.4/10.2/3.6/1.2 (BP=1.000, ratio=1.089, hyp_len=13319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.214.0.72-2.05.0.58-1.78.3.60-36.69.3.22-25.13.pth, mybk
BLEU = 9.26, 33.0/12.3/5.8/3.1 (BP=1.000, ratio=1.118, hyp_len=12786, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.214.0.72-2.05.0.58-1.78.3.60-36.69.3.22-25.13.pth, bkmy
BLEU = 11.21, 38.0/15.9/7.3/3.6 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.215.0.73-2.08.0.59-1.80.3.59-36.40.3.21-24.67.pth, mybk
BLEU = 9.43, 33.1/12.5/6.0/3.2 (BP=1.000, ratio=1.114, hyp_len=12735, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.215.0.73-2.08.0.59-1.80.3.59-36.40.3.21-24.67.pth, bkmy
BLEU = 11.57, 38.9/16.4/7.6/3.7 (BP=1.000, ratio=1.073, hyp_len=13124, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.216.0.71-2.04.0.58-1.79.3.67-39.26.3.23-25.33.pth, mybk
BLEU = 9.22, 33.2/12.7/5.9/2.9 (BP=1.000, ratio=1.117, hyp_len=12773, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.216.0.71-2.04.0.58-1.79.3.67-39.26.3.23-25.33.pth, bkmy
BLEU = 11.05, 37.4/15.5/7.3/3.5 (BP=1.000, ratio=1.086, hyp_len=13286, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.217.0.72-2.06.0.64-1.89.3.58-35.74.3.24-25.62.pth, mybk
BLEU = 9.26, 33.4/12.6/5.8/3.0 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.217.0.72-2.06.0.64-1.89.3.58-35.74.3.24-25.62.pth, bkmy
BLEU = 11.14, 37.7/15.7/7.4/3.5 (BP=1.000, ratio=1.107, hyp_len=13542, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.218.0.71-2.02.0.59-1.81.3.66-39.00.3.27-26.38.pth, mybk
BLEU = 9.58, 33.2/12.6/6.1/3.3 (BP=1.000, ratio=1.113, hyp_len=12724, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.218.0.71-2.02.0.59-1.81.3.66-39.00.3.27-26.38.pth, bkmy
BLEU = 11.42, 38.4/16.0/7.6/3.6 (BP=1.000, ratio=1.082, hyp_len=13232, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.219.0.70-2.01.0.57-1.76.3.62-37.27.3.27-26.36.pth, mybk
BLEU = 9.64, 33.8/12.8/6.1/3.3 (BP=1.000, ratio=1.097, hyp_len=12538, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.219.0.70-2.01.0.57-1.76.3.62-37.27.3.27-26.36.pth, bkmy
BLEU = 11.22, 38.3/16.1/7.4/3.5 (BP=1.000, ratio=1.084, hyp_len=13254, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.220.0.76-2.13.0.59-1.80.3.64-37.91.3.25-25.82.pth, mybk
BLEU = 9.71, 33.7/12.5/6.2/3.4 (BP=1.000, ratio=1.119, hyp_len=12791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.220.0.76-2.13.0.59-1.80.3.64-37.91.3.25-25.82.pth, bkmy
BLEU = 11.39, 37.6/15.8/7.6/3.7 (BP=1.000, ratio=1.100, hyp_len=13449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.221.0.72-2.05.0.60-1.82.3.63-37.59.3.27-26.35.pth, mybk
BLEU = 9.32, 33.6/12.5/5.8/3.1 (BP=1.000, ratio=1.104, hyp_len=12620, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.221.0.72-2.05.0.60-1.82.3.63-37.59.3.27-26.35.pth, bkmy
BLEU = 11.58, 38.1/16.1/7.6/3.8 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.222.0.70-2.01.0.57-1.77.3.66-38.88.3.28-26.66.pth, mybk
BLEU = 9.96, 34.0/13.0/6.4/3.5 (BP=1.000, ratio=1.091, hyp_len=12476, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.222.0.70-2.01.0.57-1.77.3.66-38.88.3.28-26.66.pth, bkmy
BLEU = 11.36, 37.5/15.5/7.5/3.8 (BP=1.000, ratio=1.098, hyp_len=13424, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.223.0.70-2.02.0.59-1.81.3.67-39.38.3.32-27.61.pth, mybk
BLEU = 9.76, 33.7/13.0/6.3/3.3 (BP=1.000, ratio=1.119, hyp_len=12791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.223.0.70-2.02.0.59-1.81.3.67-39.38.3.32-27.61.pth, bkmy
BLEU = 11.01, 37.2/15.4/7.2/3.6 (BP=1.000, ratio=1.085, hyp_len=13274, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.21-24.88.3.00-20.10.2.94-18.94.2.69-14.67.pth, mybk
BLEU = 4.49, 23.7/6.6/2.6/1.0 (BP=1.000, ratio=1.159, hyp_len=13249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.21-24.88.3.00-20.10.2.94-18.94.2.69-14.67.pth, bkmy
BLEU = 2.75, 15.6/5.1/1.6/0.4 (BP=1.000, ratio=2.104, hyp_len=25738, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.224.0.72-2.05.0.54-1.72.3.70-40.56.3.27-26.31.pth, mybk
BLEU = 10.04, 34.4/13.3/6.5/3.4 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.224.0.72-2.05.0.54-1.72.3.70-40.56.3.27-26.31.pth, bkmy
BLEU = 11.12, 37.7/15.5/7.2/3.6 (BP=1.000, ratio=1.100, hyp_len=13452, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.225.0.71-2.03.0.56-1.75.3.70-40.29.3.31-27.44.pth, mybk
BLEU = 9.09, 32.9/12.3/5.8/2.9 (BP=1.000, ratio=1.114, hyp_len=12740, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.225.0.71-2.03.0.56-1.75.3.70-40.29.3.31-27.44.pth, bkmy
BLEU = 11.38, 37.8/15.7/7.4/3.8 (BP=1.000, ratio=1.090, hyp_len=13329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.226.0.70-2.01.0.55-1.74.3.70-40.57.3.29-26.80.pth, mybk
BLEU = 9.91, 33.5/13.1/6.4/3.5 (BP=1.000, ratio=1.107, hyp_len=12654, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.226.0.70-2.01.0.55-1.74.3.70-40.57.3.29-26.80.pth, bkmy
BLEU = 11.51, 38.1/16.2/7.6/3.8 (BP=1.000, ratio=1.087, hyp_len=13293, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.227.0.67-1.95.0.56-1.75.3.78-43.70.3.37-29.06.pth, mybk
BLEU = 9.49, 33.3/12.7/6.1/3.1 (BP=1.000, ratio=1.122, hyp_len=12823, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.227.0.67-1.95.0.56-1.75.3.78-43.70.3.37-29.06.pth, bkmy
BLEU = 11.44, 38.0/16.0/7.5/3.8 (BP=1.000, ratio=1.107, hyp_len=13536, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.228.0.68-1.97.0.54-1.72.3.72-41.11.3.28-26.48.pth, mybk
BLEU = 9.57, 33.6/12.7/6.0/3.3 (BP=1.000, ratio=1.098, hyp_len=12554, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.228.0.68-1.97.0.54-1.72.3.72-41.11.3.28-26.48.pth, bkmy
BLEU = 11.51, 38.2/15.9/7.6/3.8 (BP=1.000, ratio=1.075, hyp_len=13147, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.229.0.72-2.05.0.62-1.86.3.73-41.70.3.31-27.40.pth, mybk
BLEU = 9.16, 33.2/12.1/5.7/3.1 (BP=1.000, ratio=1.128, hyp_len=12897, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.229.0.72-2.05.0.62-1.86.3.73-41.70.3.31-27.40.pth, bkmy
BLEU = 11.34, 38.4/16.0/7.4/3.6 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.230.0.69-2.00.0.54-1.72.3.78-43.80.3.31-27.26.pth, mybk
BLEU = 9.55, 33.1/12.6/6.2/3.2 (BP=1.000, ratio=1.110, hyp_len=12686, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.230.0.69-2.00.0.54-1.72.3.78-43.80.3.31-27.26.pth, bkmy
BLEU = 11.47, 38.3/16.1/7.5/3.7 (BP=1.000, ratio=1.097, hyp_len=13420, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.231.0.71-2.04.0.58-1.79.3.74-42.07.3.31-27.39.pth, mybk
BLEU = 9.35, 33.5/12.4/6.0/3.1 (BP=1.000, ratio=1.112, hyp_len=12711, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.231.0.71-2.04.0.58-1.79.3.74-42.07.3.31-27.39.pth, bkmy
BLEU = 11.12, 37.5/15.6/7.2/3.7 (BP=1.000, ratio=1.105, hyp_len=13514, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.232.0.66-1.93.0.55-1.74.3.76-43.10.3.34-28.31.pth, mybk
BLEU = 9.65, 33.4/12.5/6.1/3.4 (BP=1.000, ratio=1.115, hyp_len=12748, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.232.0.66-1.93.0.55-1.74.3.76-43.10.3.34-28.31.pth, bkmy
BLEU = 11.34, 37.5/15.7/7.5/3.8 (BP=1.000, ratio=1.102, hyp_len=13476, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.233.0.75-2.11.0.57-1.77.3.75-42.31.3.35-28.43.pth, mybk
BLEU = 9.19, 33.1/12.0/5.7/3.1 (BP=1.000, ratio=1.127, hyp_len=12888, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.233.0.75-2.11.0.57-1.77.3.75-42.31.3.35-28.43.pth, bkmy
BLEU = 11.11, 37.1/15.4/7.2/3.7 (BP=1.000, ratio=1.113, hyp_len=13609, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.16-23.48.2.91-18.36.2.89-17.95.2.65-14.21.pth, mybk
BLEU = 4.88, 26.1/7.4/2.8/1.1 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.16-23.48.2.91-18.36.2.89-17.95.2.65-14.21.pth, bkmy
BLEU = 6.68, 32.2/11.5/4.0/1.3 (BP=1.000, ratio=1.057, hyp_len=12932, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.234.0.68-1.97.0.54-1.72.3.79-44.33.3.32-27.66.pth, mybk
BLEU = 9.54, 33.3/12.6/6.0/3.3 (BP=1.000, ratio=1.110, hyp_len=12687, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.234.0.68-1.97.0.54-1.72.3.79-44.33.3.32-27.66.pth, bkmy
BLEU = 11.57, 38.2/16.2/7.6/3.8 (BP=1.000, ratio=1.088, hyp_len=13306, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.235.0.67-1.95.0.54-1.71.3.78-44.03.3.32-27.79.pth, mybk
BLEU = 9.63, 33.4/12.5/6.2/3.3 (BP=1.000, ratio=1.114, hyp_len=12731, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.235.0.67-1.95.0.54-1.71.3.78-44.03.3.32-27.79.pth, bkmy
BLEU = 11.36, 38.0/15.9/7.4/3.7 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.236.0.67-1.96.0.54-1.72.3.77-43.38.3.33-28.01.pth, mybk
BLEU = 9.73, 33.5/12.7/6.1/3.4 (BP=1.000, ratio=1.091, hyp_len=12468, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.236.0.67-1.96.0.54-1.72.3.77-43.38.3.33-28.01.pth, bkmy
BLEU = 11.50, 38.0/15.8/7.5/3.9 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.237.0.68-1.98.0.62-1.87.3.75-42.32.3.32-27.72.pth, mybk
BLEU = 9.98, 34.3/13.2/6.4/3.4 (BP=1.000, ratio=1.110, hyp_len=12690, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.237.0.68-1.98.0.62-1.87.3.75-42.32.3.32-27.72.pth, bkmy
BLEU = 11.81, 38.2/16.3/7.9/4.0 (BP=1.000, ratio=1.081, hyp_len=13220, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.238.0.65-1.92.0.54-1.72.3.82-45.69.3.39-29.67.pth, mybk
BLEU = 8.91, 32.8/12.0/5.6/2.9 (BP=1.000, ratio=1.132, hyp_len=12942, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.238.0.65-1.92.0.54-1.72.3.82-45.69.3.39-29.67.pth, bkmy
BLEU = 10.92, 36.7/15.2/7.2/3.5 (BP=1.000, ratio=1.112, hyp_len=13596, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.239.0.64-1.91.0.53-1.70.3.82-45.46.3.37-29.22.pth, mybk
BLEU = 9.61, 34.3/13.0/6.0/3.2 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.239.0.64-1.91.0.53-1.70.3.82-45.46.3.37-29.22.pth, bkmy
BLEU = 11.55, 38.0/16.0/7.6/3.8 (BP=1.000, ratio=1.089, hyp_len=13319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.240.0.64-1.89.0.52-1.68.3.80-44.77.3.40-29.87.pth, mybk
BLEU = 9.40, 33.8/12.6/6.0/3.1 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.240.0.64-1.89.0.52-1.68.3.80-44.77.3.40-29.87.pth, bkmy
BLEU = 10.83, 37.6/15.4/7.1/3.4 (BP=1.000, ratio=1.106, hyp_len=13531, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.241.0.63-1.87.0.52-1.68.3.81-45.09.3.40-30.11.pth, mybk
BLEU = 9.77, 33.8/12.8/6.2/3.4 (BP=1.000, ratio=1.101, hyp_len=12586, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.241.0.63-1.87.0.52-1.68.3.81-45.09.3.40-30.11.pth, bkmy
BLEU = 11.04, 37.8/15.5/7.2/3.5 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.242.0.62-1.87.0.51-1.67.3.79-44.36.3.40-30.02.pth, mybk
BLEU = 9.96, 34.0/13.1/6.3/3.5 (BP=1.000, ratio=1.094, hyp_len=12502, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.242.0.62-1.87.0.51-1.67.3.79-44.36.3.40-30.02.pth, bkmy
BLEU = 10.96, 37.4/15.3/7.1/3.5 (BP=1.000, ratio=1.102, hyp_len=13475, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.243.0.63-1.88.0.52-1.68.3.80-44.87.3.39-29.72.pth, mybk
BLEU = 9.52, 33.7/12.7/5.9/3.2 (BP=1.000, ratio=1.100, hyp_len=12576, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.243.0.63-1.88.0.52-1.68.3.80-44.87.3.39-29.72.pth, bkmy
BLEU = 11.80, 37.7/16.2/7.9/4.0 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.10-22.26.2.88-17.77.2.86-17.49.2.65-14.12.pth, mybk
BLEU = 4.81, 25.3/7.2/2.8/1.1 (BP=1.000, ratio=1.128, hyp_len=12898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.10-22.26.2.88-17.77.2.86-17.49.2.65-14.12.pth, bkmy
BLEU = 7.05, 31.7/11.5/4.2/1.6 (BP=1.000, ratio=1.067, hyp_len=13050, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.244.0.64-1.90.0.53-1.70.3.85-47.01.3.35-28.62.pth, mybk
BLEU = 9.47, 32.8/12.4/6.1/3.3 (BP=1.000, ratio=1.123, hyp_len=12842, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.244.0.64-1.90.0.53-1.70.3.85-47.01.3.35-28.62.pth, bkmy
BLEU = 11.25, 37.4/15.4/7.3/3.8 (BP=1.000, ratio=1.106, hyp_len=13526, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.245.0.63-1.88.0.53-1.70.3.81-45.31.3.41-30.21.pth, mybk
BLEU = 9.17, 32.9/12.2/5.7/3.1 (BP=1.000, ratio=1.114, hyp_len=12739, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.245.0.63-1.88.0.53-1.70.3.81-45.31.3.41-30.21.pth, bkmy
BLEU = 11.03, 37.3/15.2/7.2/3.6 (BP=1.000, ratio=1.091, hyp_len=13347, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.246.0.64-1.90.0.52-1.68.3.84-46.58.3.44-31.21.pth, mybk
BLEU = 9.37, 33.8/12.6/5.9/3.1 (BP=1.000, ratio=1.106, hyp_len=12648, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.246.0.64-1.90.0.52-1.68.3.84-46.58.3.44-31.21.pth, bkmy
BLEU = 10.84, 37.1/15.3/6.9/3.5 (BP=1.000, ratio=1.099, hyp_len=13438, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.247.0.65-1.91.0.51-1.67.3.83-46.04.3.48-32.60.pth, mybk
BLEU = 9.55, 33.6/12.6/6.1/3.2 (BP=1.000, ratio=1.115, hyp_len=12751, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.247.0.65-1.91.0.51-1.67.3.83-46.04.3.48-32.60.pth, bkmy
BLEU = 11.18, 37.1/15.6/7.3/3.7 (BP=1.000, ratio=1.115, hyp_len=13634, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.248.0.63-1.87.0.50-1.65.3.80-44.64.3.40-29.90.pth, mybk
BLEU = 9.35, 33.6/12.3/5.8/3.2 (BP=1.000, ratio=1.105, hyp_len=12630, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.248.0.63-1.87.0.50-1.65.3.80-44.64.3.40-29.90.pth, bkmy
BLEU = 11.38, 36.9/15.6/7.5/3.9 (BP=1.000, ratio=1.110, hyp_len=13577, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.249.0.65-1.91.0.52-1.68.3.80-44.53.3.44-31.17.pth, mybk
BLEU = 9.11, 33.5/12.2/5.7/3.0 (BP=1.000, ratio=1.120, hyp_len=12805, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.249.0.65-1.91.0.52-1.68.3.80-44.53.3.44-31.17.pth, bkmy
BLEU = 11.05, 37.3/15.4/7.2/3.6 (BP=1.000, ratio=1.090, hyp_len=13326, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.250.0.64-1.90.0.55-1.73.3.84-46.45.3.47-32.18.pth, mybk
BLEU = 8.94, 33.0/12.0/5.6/2.9 (BP=1.000, ratio=1.106, hyp_len=12649, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.250.0.64-1.90.0.55-1.73.3.84-46.45.3.47-32.18.pth, bkmy
BLEU = 11.19, 37.9/15.7/7.3/3.6 (BP=1.000, ratio=1.083, hyp_len=13245, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.251.0.66-1.94.0.59-1.80.3.79-44.09.3.46-31.81.pth, mybk
BLEU = 9.46, 33.7/12.6/5.9/3.2 (BP=1.000, ratio=1.111, hyp_len=12698, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.251.0.66-1.94.0.59-1.80.3.79-44.09.3.46-31.81.pth, bkmy
BLEU = 10.79, 36.6/14.9/7.0/3.5 (BP=1.000, ratio=1.116, hyp_len=13645, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.252.0.61-1.83.0.50-1.65.3.83-46.15.3.48-32.41.pth, mybk
BLEU = 9.62, 33.8/12.8/6.1/3.2 (BP=1.000, ratio=1.110, hyp_len=12694, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.252.0.61-1.83.0.50-1.65.3.83-46.15.3.48-32.41.pth, bkmy
BLEU = 10.83, 37.5/15.4/7.0/3.4 (BP=1.000, ratio=1.104, hyp_len=13506, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.253.0.62-1.85.0.50-1.65.3.85-46.95.3.52-33.88.pth, mybk
BLEU = 9.63, 33.0/12.5/6.2/3.4 (BP=1.000, ratio=1.117, hyp_len=12764, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.253.0.62-1.85.0.50-1.65.3.85-46.95.3.52-33.88.pth, bkmy
BLEU = 10.74, 37.0/14.9/6.9/3.5 (BP=1.000, ratio=1.092, hyp_len=13353, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.08-21.81.2.81-16.63.2.81-16.60.2.60-13.48.pth, mybk
BLEU = 5.14, 25.9/7.7/2.9/1.2 (BP=1.000, ratio=1.111, hyp_len=12705, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.08-21.81.2.81-16.63.2.81-16.60.2.60-13.48.pth, bkmy
BLEU = 6.58, 31.0/11.0/4.0/1.4 (BP=1.000, ratio=1.095, hyp_len=13387, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.254.0.62-1.85.0.49-1.64.3.80-44.81.3.52-33.78.pth, mybk
BLEU = 9.33, 33.0/12.4/5.8/3.2 (BP=1.000, ratio=1.125, hyp_len=12860, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.254.0.62-1.85.0.49-1.64.3.80-44.81.3.52-33.78.pth, bkmy
BLEU = 10.92, 37.0/15.1/7.1/3.6 (BP=1.000, ratio=1.117, hyp_len=13660, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.255.0.60-1.82.0.49-1.64.3.86-47.67.3.47-32.08.pth, mybk
BLEU = 8.91, 32.4/12.2/5.6/2.9 (BP=1.000, ratio=1.139, hyp_len=13019, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.255.0.60-1.82.0.49-1.64.3.86-47.67.3.47-32.08.pth, bkmy
BLEU = 11.07, 37.5/15.7/7.3/3.5 (BP=1.000, ratio=1.091, hyp_len=13349, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.256.0.63-1.88.0.50-1.65.3.85-47.19.3.49-32.92.pth, mybk
BLEU = 9.69, 33.4/12.7/6.2/3.4 (BP=1.000, ratio=1.124, hyp_len=12850, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.256.0.63-1.88.0.50-1.65.3.85-47.19.3.49-32.92.pth, bkmy
BLEU = 11.08, 38.2/15.5/7.2/3.6 (BP=1.000, ratio=1.088, hyp_len=13304, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.257.0.59-1.80.0.52-1.69.3.84-46.36.3.48-32.55.pth, mybk
BLEU = 9.04, 33.4/12.2/5.7/2.9 (BP=1.000, ratio=1.129, hyp_len=12912, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.257.0.59-1.80.0.52-1.69.3.84-46.36.3.48-32.55.pth, bkmy
BLEU = 11.44, 38.3/15.8/7.5/3.8 (BP=1.000, ratio=1.091, hyp_len=13342, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.258.0.60-1.82.0.49-1.63.3.87-47.92.3.51-33.43.pth, mybk
BLEU = 9.39, 33.4/12.6/6.0/3.1 (BP=1.000, ratio=1.127, hyp_len=12886, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.258.0.60-1.82.0.49-1.63.3.87-47.92.3.51-33.43.pth, bkmy
BLEU = 10.93, 37.7/15.5/7.1/3.4 (BP=1.000, ratio=1.095, hyp_len=13396, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.259.0.61-1.84.0.47-1.61.3.85-46.92.3.53-34.24.pth, mybk
BLEU = 9.40, 33.2/12.5/5.9/3.2 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.259.0.61-1.84.0.47-1.61.3.85-46.92.3.53-34.24.pth, bkmy
BLEU = 11.11, 37.8/15.7/7.3/3.5 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.260.0.58-1.79.0.48-1.61.3.87-47.71.3.50-32.99.pth, mybk
BLEU = 9.20, 33.0/12.1/5.7/3.1 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.260.0.58-1.79.0.48-1.61.3.87-47.71.3.50-32.99.pth, bkmy
BLEU = 11.10, 38.1/15.6/7.2/3.6 (BP=1.000, ratio=1.092, hyp_len=13358, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.261.0.61-1.83.0.50-1.64.3.87-47.85.3.52-33.75.pth, mybk
BLEU = 9.08, 32.9/12.0/5.7/3.0 (BP=1.000, ratio=1.122, hyp_len=12827, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.261.0.61-1.83.0.50-1.64.3.87-47.85.3.52-33.75.pth, bkmy
BLEU = 11.25, 37.6/15.6/7.3/3.8 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.262.0.63-1.87.0.52-1.68.3.91-49.72.3.53-34.00.pth, mybk
BLEU = 9.59, 33.4/12.8/6.1/3.2 (BP=1.000, ratio=1.106, hyp_len=12648, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.262.0.63-1.87.0.52-1.68.3.91-49.72.3.53-34.00.pth, bkmy
BLEU = 11.18, 37.4/15.6/7.3/3.7 (BP=1.000, ratio=1.094, hyp_len=13375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.263.0.60-1.81.0.48-1.62.3.90-49.40.3.52-33.63.pth, mybk
BLEU = 9.90, 33.2/12.8/6.4/3.5 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.263.0.60-1.81.0.48-1.62.3.90-49.40.3.52-33.63.pth, bkmy
BLEU = 11.65, 38.1/16.1/7.7/3.9 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.07-21.61.2.89-17.92.2.83-16.88.2.59-13.32.pth, mybk
BLEU = 5.57, 25.9/8.2/3.4/1.3 (BP=1.000, ratio=1.111, hyp_len=12698, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.07-21.61.2.89-17.92.2.83-16.88.2.59-13.32.pth, bkmy
BLEU = 5.94, 27.6/9.8/3.6/1.3 (BP=1.000, ratio=1.271, hyp_len=15548, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.264.0.61-1.84.0.49-1.63.3.94-51.33.3.51-33.59.pth, mybk
BLEU = 9.33, 33.0/12.2/5.9/3.2 (BP=1.000, ratio=1.121, hyp_len=12817, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.264.0.61-1.84.0.49-1.63.3.94-51.33.3.51-33.59.pth, bkmy
BLEU = 10.58, 37.2/15.0/6.8/3.3 (BP=1.000, ratio=1.106, hyp_len=13528, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.265.0.67-1.96.0.51-1.66.3.93-50.94.3.50-33.19.pth, mybk
BLEU = 9.07, 33.1/12.1/5.6/3.0 (BP=1.000, ratio=1.114, hyp_len=12734, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.265.0.67-1.96.0.51-1.66.3.93-50.94.3.50-33.19.pth, bkmy
BLEU = 11.00, 37.5/15.4/7.1/3.6 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.266.0.60-1.82.0.50-1.65.3.96-52.25.3.52-33.65.pth, mybk
BLEU = 9.30, 33.3/12.4/5.9/3.1 (BP=1.000, ratio=1.124, hyp_len=12848, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.266.0.60-1.82.0.50-1.65.3.96-52.25.3.52-33.65.pth, bkmy
BLEU = 11.72, 38.2/16.1/7.7/4.0 (BP=1.000, ratio=1.091, hyp_len=13350, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.267.0.63-1.87.0.50-1.65.3.95-52.12.3.56-35.27.pth, mybk
BLEU = 8.57, 32.6/11.7/5.2/2.7 (BP=1.000, ratio=1.124, hyp_len=12844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.267.0.63-1.87.0.50-1.65.3.95-52.12.3.56-35.27.pth, bkmy
BLEU = 10.82, 37.3/15.3/7.0/3.4 (BP=1.000, ratio=1.110, hyp_len=13581, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.268.0.60-1.82.0.47-1.60.3.93-50.92.3.56-35.17.pth, mybk
BLEU = 8.70, 32.3/11.6/5.4/2.8 (BP=1.000, ratio=1.134, hyp_len=12960, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.268.0.60-1.82.0.47-1.60.3.93-50.92.3.56-35.17.pth, bkmy
BLEU = 11.66, 37.9/16.0/7.7/4.0 (BP=1.000, ratio=1.104, hyp_len=13500, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.269.0.68-1.97.0.49-1.63.3.92-50.35.3.54-34.61.pth, mybk
BLEU = 9.43, 33.3/12.3/6.0/3.2 (BP=1.000, ratio=1.116, hyp_len=12761, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.269.0.68-1.97.0.49-1.63.3.92-50.35.3.54-34.61.pth, bkmy
BLEU = 11.25, 37.5/15.6/7.4/3.7 (BP=1.000, ratio=1.100, hyp_len=13455, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.270.0.57-1.77.0.47-1.61.3.96-52.69.3.55-34.70.pth, mybk
BLEU = 8.93, 33.0/12.0/5.6/2.9 (BP=1.000, ratio=1.117, hyp_len=12773, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.270.0.57-1.77.0.47-1.61.3.96-52.69.3.55-34.70.pth, bkmy
BLEU = 11.23, 37.6/15.7/7.2/3.7 (BP=1.000, ratio=1.099, hyp_len=13446, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.271.0.61-1.85.0.54-1.72.3.92-50.27.3.54-34.36.pth, mybk
BLEU = 9.39, 33.4/12.6/5.9/3.1 (BP=1.000, ratio=1.120, hyp_len=12809, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.271.0.61-1.85.0.54-1.72.3.92-50.27.3.54-34.36.pth, bkmy
BLEU = 11.01, 37.4/15.3/7.2/3.6 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.272.0.57-1.78.0.46-1.59.3.97-52.91.3.51-33.39.pth, mybk
BLEU = 9.17, 33.2/12.2/5.8/3.0 (BP=1.000, ratio=1.123, hyp_len=12838, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.272.0.57-1.78.0.46-1.59.3.97-52.91.3.51-33.39.pth, bkmy
BLEU = 10.73, 37.4/15.0/6.9/3.4 (BP=1.000, ratio=1.096, hyp_len=13410, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.3.05-21.11.2.81-16.61.2.81-16.63.2.58-13.20.pth, mybk
BLEU = 4.85, 24.4/7.3/2.9/1.1 (BP=1.000, ratio=1.193, hyp_len=13634, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.3.05-21.11.2.81-16.61.2.81-16.63.2.58-13.20.pth, bkmy
BLEU = 5.06, 23.5/8.5/3.1/1.1 (BP=1.000, ratio=1.500, hyp_len=18347, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.273.0.65-1.92.0.48-1.62.3.95-51.97.3.47-32.09.pth, mybk
BLEU = 9.71, 33.4/12.5/6.2/3.4 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.273.0.65-1.92.0.48-1.62.3.95-51.97.3.47-32.09.pth, bkmy
BLEU = 10.97, 37.5/15.4/7.1/3.5 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.274.0.60-1.82.0.47-1.61.3.97-52.73.3.53-34.08.pth, mybk
BLEU = 9.04, 32.9/12.4/5.6/2.9 (BP=1.000, ratio=1.129, hyp_len=12904, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.274.0.60-1.82.0.47-1.61.3.97-52.73.3.53-34.08.pth, bkmy
BLEU = 10.84, 37.5/15.3/6.9/3.5 (BP=1.000, ratio=1.088, hyp_len=13305, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.275.0.60-1.81.0.47-1.60.3.95-51.97.3.51-33.49.pth, mybk
BLEU = 9.11, 32.4/12.0/5.7/3.1 (BP=1.000, ratio=1.128, hyp_len=12892, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.275.0.60-1.81.0.47-1.60.3.95-51.97.3.51-33.49.pth, bkmy
BLEU = 10.35, 36.8/14.7/6.6/3.2 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.276.0.57-1.77.0.46-1.59.4.00-54.65.3.53-34.02.pth, mybk
BLEU = 8.90, 32.5/11.7/5.5/3.0 (BP=1.000, ratio=1.122, hyp_len=12830, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.276.0.57-1.77.0.46-1.59.4.00-54.65.3.53-34.02.pth, bkmy
BLEU = 11.38, 38.2/15.9/7.4/3.7 (BP=1.000, ratio=1.082, hyp_len=13240, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.277.0.57-1.78.0.45-1.57.3.97-52.73.3.56-35.07.pth, mybk
BLEU = 9.31, 32.9/12.4/5.9/3.1 (BP=1.000, ratio=1.133, hyp_len=12955, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.277.0.57-1.78.0.45-1.57.3.97-52.73.3.56-35.07.pth, bkmy
BLEU = 10.85, 37.0/15.4/7.1/3.4 (BP=1.000, ratio=1.109, hyp_len=13569, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.278.0.57-1.76.0.47-1.60.3.97-52.83.3.55-34.96.pth, mybk
BLEU = 8.91, 32.6/11.9/5.6/2.9 (BP=1.000, ratio=1.123, hyp_len=12834, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.278.0.57-1.76.0.47-1.60.3.97-52.83.3.55-34.96.pth, bkmy
BLEU = 10.96, 37.4/15.5/7.1/3.5 (BP=1.000, ratio=1.104, hyp_len=13501, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.279.0.58-1.79.0.49-1.63.4.00-54.37.3.58-35.76.pth, mybk
BLEU = 9.20, 33.1/12.3/5.8/3.0 (BP=1.000, ratio=1.115, hyp_len=12742, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.279.0.58-1.79.0.49-1.63.4.00-54.37.3.58-35.76.pth, bkmy
BLEU = 11.23, 37.5/15.6/7.4/3.7 (BP=1.000, ratio=1.096, hyp_len=13407, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.280.0.57-1.76.0.45-1.57.3.97-53.13.3.57-35.46.pth, mybk
BLEU = 9.21, 32.6/12.1/5.9/3.1 (BP=1.000, ratio=1.131, hyp_len=12934, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.280.0.57-1.76.0.45-1.57.3.97-53.13.3.57-35.46.pth, bkmy
BLEU = 11.29, 37.4/15.6/7.3/3.8 (BP=1.000, ratio=1.106, hyp_len=13523, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.281.0.54-1.72.0.46-1.58.4.06-57.69.3.57-35.46.pth, mybk
BLEU = 8.95, 32.5/11.8/5.6/3.0 (BP=1.000, ratio=1.114, hyp_len=12736, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.281.0.54-1.72.0.46-1.58.4.06-57.69.3.57-35.46.pth, bkmy
BLEU = 11.63, 37.8/15.9/7.6/4.0 (BP=1.000, ratio=1.096, hyp_len=13403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.282.0.54-1.72.0.43-1.54.4.01-55.34.3.61-37.03.pth, mybk
BLEU = 9.15, 32.9/12.1/5.7/3.1 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.282.0.54-1.72.0.43-1.54.4.01-55.34.3.61-37.03.pth, bkmy
BLEU = 11.58, 37.5/15.6/7.5/4.1 (BP=1.000, ratio=1.090, hyp_len=13327, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.99-19.84.2.72-15.14.2.79-16.31.2.56-12.88.pth, mybk
BLEU = 5.54, 25.6/8.3/3.4/1.3 (BP=1.000, ratio=1.182, hyp_len=13518, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.99-19.84.2.72-15.14.2.79-16.31.2.56-12.88.pth, bkmy
BLEU = 3.93, 18.9/6.6/2.3/0.8 (BP=1.000, ratio=1.825, hyp_len=22327, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.283.0.55-1.73.0.45-1.56.4.02-55.80.3.58-35.90.pth, mybk
BLEU = 9.03, 32.9/12.1/5.6/3.0 (BP=1.000, ratio=1.117, hyp_len=12770, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.283.0.55-1.73.0.45-1.56.4.02-55.80.3.58-35.90.pth, bkmy
BLEU = 11.46, 37.8/15.8/7.5/3.9 (BP=1.000, ratio=1.103, hyp_len=13487, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.284.0.60-1.82.0.46-1.59.3.98-53.72.3.61-36.96.pth, mybk
BLEU = 8.87, 32.7/11.9/5.5/2.9 (BP=1.000, ratio=1.106, hyp_len=12639, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.284.0.60-1.82.0.46-1.59.3.98-53.72.3.61-36.96.pth, bkmy
BLEU = 10.93, 36.9/15.2/7.2/3.5 (BP=1.000, ratio=1.112, hyp_len=13606, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.285.0.57-1.77.0.50-1.65.3.98-53.72.3.59-36.36.pth, mybk
BLEU = 9.21, 33.4/12.1/5.8/3.1 (BP=1.000, ratio=1.108, hyp_len=12663, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.285.0.57-1.77.0.50-1.65.3.98-53.72.3.59-36.36.pth, bkmy
BLEU = 10.89, 37.3/15.2/7.0/3.5 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.286.0.53-1.70.0.44-1.55.3.98-53.60.3.61-36.92.pth, mybk
BLEU = 9.23, 32.9/12.1/5.8/3.2 (BP=1.000, ratio=1.122, hyp_len=12823, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.286.0.53-1.70.0.44-1.55.3.98-53.60.3.61-36.92.pth, bkmy
BLEU = 11.20, 37.8/15.6/7.3/3.7 (BP=1.000, ratio=1.091, hyp_len=13345, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.287.0.57-1.76.0.45-1.57.3.97-53.16.3.61-36.98.pth, mybk
BLEU = 8.76, 32.9/11.9/5.4/2.8 (BP=1.000, ratio=1.119, hyp_len=12798, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.287.0.57-1.76.0.45-1.57.3.97-53.16.3.61-36.98.pth, bkmy
BLEU = 10.89, 37.5/15.4/7.0/3.5 (BP=1.000, ratio=1.101, hyp_len=13468, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.288.0.54-1.72.0.44-1.55.4.04-56.56.3.59-36.40.pth, mybk
BLEU = 9.24, 33.0/12.2/5.8/3.1 (BP=1.000, ratio=1.114, hyp_len=12732, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.288.0.54-1.72.0.44-1.55.4.04-56.56.3.59-36.40.pth, bkmy
BLEU = 11.17, 37.3/15.3/7.3/3.8 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.289.0.54-1.71.0.45-1.57.4.00-54.61.3.59-36.13.pth, mybk
BLEU = 9.41, 33.6/12.4/5.9/3.2 (BP=1.000, ratio=1.096, hyp_len=12535, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.289.0.54-1.71.0.45-1.57.4.00-54.61.3.59-36.13.pth, bkmy
BLEU = 11.03, 37.4/15.4/7.2/3.6 (BP=1.000, ratio=1.096, hyp_len=13411, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.290.0.55-1.74.0.47-1.60.4.01-55.17.3.60-36.49.pth, mybk
BLEU = 9.36, 33.4/12.4/5.9/3.1 (BP=1.000, ratio=1.114, hyp_len=12734, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.290.0.55-1.74.0.47-1.60.4.01-55.17.3.60-36.49.pth, bkmy
BLEU = 10.70, 36.6/14.9/6.9/3.5 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.291.0.56-1.75.0.48-1.62.4.02-55.87.3.58-35.71.pth, mybk
BLEU = 8.81, 32.8/11.9/5.4/2.9 (BP=1.000, ratio=1.118, hyp_len=12776, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.291.0.56-1.75.0.48-1.62.4.02-55.87.3.58-35.71.pth, bkmy
BLEU = 11.01, 37.0/15.2/7.1/3.7 (BP=1.000, ratio=1.106, hyp_len=13530, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.292.0.54-1.72.0.45-1.57.3.96-52.48.3.57-35.50.pth, mybk
BLEU = 9.13, 33.4/12.0/5.6/3.1 (BP=1.000, ratio=1.103, hyp_len=12606, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.292.0.54-1.72.0.45-1.57.3.96-52.48.3.57-35.50.pth, bkmy
BLEU = 10.34, 36.8/14.5/6.5/3.3 (BP=1.000, ratio=1.099, hyp_len=13444, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.88-17.75.2.65-14.18.2.78-16.18.2.51-12.36.pth, mybk
BLEU = 6.48, 28.8/9.8/3.9/1.6 (BP=1.000, ratio=1.078, hyp_len=12321, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.88-17.75.2.65-14.18.2.78-16.18.2.51-12.36.pth, bkmy
BLEU = 6.36, 28.4/10.2/3.8/1.5 (BP=1.000, ratio=1.260, hyp_len=15406, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.293.0.54-1.71.0.44-1.55.3.98-53.73.3.58-35.99.pth, mybk
BLEU = 9.03, 33.1/12.1/5.6/3.0 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.293.0.54-1.71.0.44-1.55.3.98-53.73.3.58-35.99.pth, bkmy
BLEU = 10.88, 36.9/15.0/7.0/3.6 (BP=1.000, ratio=1.100, hyp_len=13460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.294.0.53-1.71.0.43-1.53.4.02-55.56.3.62-37.45.pth, mybk
BLEU = 9.30, 33.5/12.5/5.8/3.1 (BP=1.000, ratio=1.119, hyp_len=12792, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.294.0.53-1.71.0.43-1.53.4.02-55.56.3.62-37.45.pth, bkmy
BLEU = 11.05, 37.6/15.5/7.0/3.6 (BP=1.000, ratio=1.098, hyp_len=13432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.295.0.63-1.88.0.48-1.61.4.05-57.17.3.63-37.84.pth, mybk
BLEU = 9.24, 32.9/12.2/5.8/3.1 (BP=1.000, ratio=1.125, hyp_len=12857, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.295.0.63-1.88.0.48-1.61.4.05-57.17.3.63-37.84.pth, bkmy
BLEU = 10.96, 37.4/15.3/7.1/3.5 (BP=1.000, ratio=1.088, hyp_len=13303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.296.0.54-1.71.0.44-1.55.4.06-58.05.3.66-39.04.pth, mybk
BLEU = 8.72, 32.8/11.7/5.4/2.8 (BP=1.000, ratio=1.129, hyp_len=12911, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.296.0.54-1.71.0.44-1.55.4.06-58.05.3.66-39.04.pth, bkmy
BLEU = 10.35, 36.5/14.4/6.6/3.3 (BP=1.000, ratio=1.099, hyp_len=13438, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.297.0.53-1.71.0.46-1.58.4.06-58.00.3.65-38.66.pth, mybk
BLEU = 9.19, 33.1/12.3/5.7/3.1 (BP=1.000, ratio=1.110, hyp_len=12685, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.297.0.53-1.71.0.46-1.58.4.06-58.00.3.65-38.66.pth, bkmy
BLEU = 11.26, 37.5/15.5/7.3/3.8 (BP=1.000, ratio=1.082, hyp_len=13239, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.298.0.53-1.69.0.44-1.55.4.05-57.57.3.67-39.11.pth, mybk
BLEU = 9.23, 33.3/12.4/5.8/3.0 (BP=1.000, ratio=1.115, hyp_len=12743, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.298.0.53-1.69.0.44-1.55.4.05-57.57.3.67-39.11.pth, bkmy
BLEU = 11.15, 37.6/15.5/7.3/3.6 (BP=1.000, ratio=1.097, hyp_len=13421, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.299.0.53-1.69.0.42-1.53.4.04-56.87.3.66-38.71.pth, mybk
BLEU = 9.01, 33.1/12.1/5.6/2.9 (BP=1.000, ratio=1.114, hyp_len=12737, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.299.0.53-1.69.0.42-1.53.4.04-56.87.3.66-38.71.pth, bkmy
BLEU = 11.43, 37.8/15.8/7.5/3.8 (BP=1.000, ratio=1.087, hyp_len=13289, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.300.0.54-1.71.0.43-1.54.4.05-57.41.3.66-39.00.pth, mybk
BLEU = 9.15, 33.0/12.3/5.8/3.0 (BP=1.000, ratio=1.125, hyp_len=12856, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.300.0.54-1.71.0.43-1.54.4.05-57.41.3.66-39.00.pth, bkmy
BLEU = 11.32, 38.1/16.0/7.4/3.6 (BP=1.000, ratio=1.090, hyp_len=13335, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.301.0.53-1.69.0.43-1.54.4.06-58.12.3.64-37.99.pth, mybk
BLEU = 9.55, 33.1/12.6/6.1/3.3 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.301.0.53-1.69.0.43-1.54.4.06-58.12.3.64-37.99.pth, bkmy
BLEU = 11.81, 38.2/16.1/7.7/4.1 (BP=1.000, ratio=1.092, hyp_len=13352, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.302.0.63-1.88.0.46-1.58.4.01-55.41.3.66-38.98.pth, mybk
BLEU = 8.44, 32.0/11.0/5.2/2.8 (BP=1.000, ratio=1.125, hyp_len=12862, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.302.0.63-1.88.0.46-1.58.4.01-55.41.3.66-38.98.pth, bkmy
BLEU = 11.00, 37.2/15.4/7.1/3.6 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.86-17.46.2.64-13.97.2.75-15.61.2.49-12.03.pth, mybk
BLEU = 6.76, 29.0/9.8/4.2/1.8 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.86-17.46.2.64-13.97.2.75-15.61.2.49-12.03.pth, bkmy
BLEU = 7.03, 31.5/11.6/4.2/1.6 (BP=1.000, ratio=1.125, hyp_len=13754, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.303.0.52-1.68.0.42-1.53.4.08-58.90.3.69-39.93.pth, mybk
BLEU = 8.57, 31.8/11.5/5.3/2.8 (BP=1.000, ratio=1.135, hyp_len=12975, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.303.0.52-1.68.0.42-1.53.4.08-58.90.3.69-39.93.pth, bkmy
BLEU = 10.63, 37.1/15.1/6.9/3.3 (BP=1.000, ratio=1.097, hyp_len=13413, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.304.0.59-1.81.0.45-1.56.4.06-58.11.3.66-38.86.pth, mybk
BLEU = 8.90, 32.3/12.1/5.6/2.9 (BP=1.000, ratio=1.140, hyp_len=13029, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.304.0.59-1.81.0.45-1.56.4.06-58.11.3.66-38.86.pth, bkmy
BLEU = 11.57, 38.2/15.9/7.4/4.0 (BP=1.000, ratio=1.091, hyp_len=13342, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.305.0.54-1.72.0.43-1.54.4.06-57.79.3.62-37.52.pth, mybk
BLEU = 8.41, 32.3/11.5/5.1/2.6 (BP=1.000, ratio=1.125, hyp_len=12866, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.305.0.54-1.72.0.43-1.54.4.06-57.79.3.62-37.52.pth, bkmy
BLEU = 10.42, 37.0/15.0/6.7/3.2 (BP=1.000, ratio=1.099, hyp_len=13446, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.306.0.50-1.65.0.43-1.53.4.06-58.25.3.62-37.35.pth, mybk
BLEU = 9.23, 33.1/12.2/5.9/3.1 (BP=1.000, ratio=1.126, hyp_len=12872, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.306.0.50-1.65.0.43-1.53.4.06-58.25.3.62-37.35.pth, bkmy
BLEU = 11.40, 38.0/15.7/7.3/3.8 (BP=1.000, ratio=1.081, hyp_len=13218, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.307.0.54-1.71.0.42-1.53.4.09-59.74.3.69-40.10.pth, mybk
BLEU = 9.54, 33.4/12.5/6.0/3.3 (BP=1.000, ratio=1.111, hyp_len=12700, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.307.0.54-1.71.0.42-1.53.4.09-59.74.3.69-40.10.pth, bkmy
BLEU = 10.90, 37.5/15.4/7.0/3.5 (BP=1.000, ratio=1.104, hyp_len=13504, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.308.0.53-1.69.0.43-1.53.4.08-59.23.3.68-39.65.pth, mybk
BLEU = 9.58, 33.2/12.6/6.1/3.3 (BP=1.000, ratio=1.119, hyp_len=12790, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.308.0.53-1.69.0.43-1.53.4.08-59.23.3.68-39.65.pth, bkmy
BLEU = 11.33, 37.2/15.3/7.3/4.0 (BP=1.000, ratio=1.099, hyp_len=13437, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.309.0.54-1.72.0.41-1.51.4.09-59.93.3.65-38.49.pth, mybk
BLEU = 9.05, 32.4/11.9/5.8/3.0 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.309.0.54-1.72.0.41-1.51.4.09-59.93.3.65-38.49.pth, bkmy
BLEU = 11.23, 37.2/15.5/7.3/3.8 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.310.0.52-1.68.0.42-1.53.4.12-61.34.3.70-40.33.pth, mybk
BLEU = 9.17, 33.0/12.1/5.7/3.1 (BP=1.000, ratio=1.125, hyp_len=12857, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.310.0.52-1.68.0.42-1.53.4.12-61.34.3.70-40.33.pth, bkmy
BLEU = 11.01, 37.1/15.3/7.1/3.7 (BP=1.000, ratio=1.100, hyp_len=13449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.311.0.55-1.74.0.46-1.58.4.11-60.84.3.70-40.45.pth, mybk
BLEU = 8.85, 32.7/11.9/5.5/2.9 (BP=1.000, ratio=1.120, hyp_len=12801, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.311.0.55-1.74.0.46-1.58.4.11-60.84.3.70-40.45.pth, bkmy
BLEU = 11.54, 37.8/15.8/7.5/4.0 (BP=1.000, ratio=1.101, hyp_len=13461, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.312.0.52-1.69.0.41-1.50.4.10-60.53.3.69-39.86.pth, mybk
BLEU = 9.20, 33.2/12.1/5.8/3.0 (BP=1.000, ratio=1.113, hyp_len=12723, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.312.0.52-1.69.0.41-1.50.4.10-60.53.3.69-39.86.pth, bkmy
BLEU = 11.28, 37.7/15.5/7.2/3.8 (BP=1.000, ratio=1.094, hyp_len=13380, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.85-17.26.2.62-13.71.2.83-16.88.2.50-12.17.pth, mybk
BLEU = 6.48, 27.5/9.5/4.1/1.7 (BP=1.000, ratio=1.159, hyp_len=13245, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.85-17.26.2.62-13.71.2.83-16.88.2.50-12.17.pth, bkmy
BLEU = 5.71, 24.7/9.0/3.5/1.4 (BP=1.000, ratio=1.467, hyp_len=17945, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.313.0.54-1.71.0.47-1.60.4.09-59.67.3.69-40.08.pth, mybk
BLEU = 8.92, 32.8/11.9/5.6/2.9 (BP=1.000, ratio=1.120, hyp_len=12809, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.313.0.54-1.71.0.47-1.60.4.09-59.67.3.69-40.08.pth, bkmy
BLEU = 10.96, 37.4/15.3/7.0/3.6 (BP=1.000, ratio=1.104, hyp_len=13499, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.314.0.58-1.79.0.42-1.53.4.10-60.05.3.68-39.80.pth, mybk
BLEU = 9.01, 32.6/12.1/5.6/3.0 (BP=1.000, ratio=1.118, hyp_len=12780, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.314.0.58-1.79.0.42-1.53.4.10-60.05.3.68-39.80.pth, bkmy
BLEU = 10.97, 37.2/15.4/7.1/3.6 (BP=1.000, ratio=1.096, hyp_len=13403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.315.0.50-1.65.0.42-1.51.4.11-60.89.3.69-40.09.pth, mybk
BLEU = 9.00, 32.7/11.8/5.6/3.0 (BP=1.000, ratio=1.125, hyp_len=12860, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.315.0.50-1.65.0.42-1.51.4.11-60.89.3.69-40.09.pth, bkmy
BLEU = 10.91, 36.6/14.8/7.0/3.7 (BP=1.000, ratio=1.104, hyp_len=13500, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.316.0.54-1.72.0.46-1.59.4.15-63.37.3.65-38.36.pth, mybk
BLEU = 9.12, 33.1/12.3/5.7/3.0 (BP=1.000, ratio=1.124, hyp_len=12850, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.316.0.54-1.72.0.46-1.59.4.15-63.37.3.65-38.36.pth, bkmy
BLEU = 10.90, 37.8/15.3/7.0/3.5 (BP=1.000, ratio=1.089, hyp_len=13321, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.317.0.51-1.67.0.40-1.49.4.20-66.72.3.73-41.78.pth, mybk
BLEU = 9.29, 32.9/12.3/5.9/3.1 (BP=1.000, ratio=1.110, hyp_len=12693, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.317.0.51-1.67.0.40-1.49.4.20-66.72.3.73-41.78.pth, bkmy
BLEU = 10.94, 37.1/15.4/7.1/3.5 (BP=1.000, ratio=1.103, hyp_len=13485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.318.0.52-1.69.0.45-1.57.4.17-64.85.3.71-40.85.pth, mybk
BLEU = 9.34, 33.6/12.5/5.9/3.1 (BP=1.000, ratio=1.111, hyp_len=12698, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.318.0.52-1.69.0.45-1.57.4.17-64.85.3.71-40.85.pth, bkmy
BLEU = 11.07, 37.8/15.4/7.1/3.6 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.319.0.51-1.66.0.41-1.50.4.17-64.87.3.71-40.79.pth, mybk
BLEU = 9.22, 32.8/12.2/5.8/3.1 (BP=1.000, ratio=1.125, hyp_len=12865, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.319.0.51-1.66.0.41-1.50.4.17-64.87.3.71-40.79.pth, bkmy
BLEU = 11.37, 37.3/15.3/7.5/3.9 (BP=1.000, ratio=1.102, hyp_len=13481, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.320.0.48-1.62.0.39-1.48.4.14-62.98.3.73-41.70.pth, mybk
BLEU = 9.09, 33.4/12.4/5.7/2.9 (BP=1.000, ratio=1.127, hyp_len=12888, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.320.0.48-1.62.0.39-1.48.4.14-62.98.3.73-41.70.pth, bkmy
BLEU = 11.31, 37.3/15.5/7.4/3.8 (BP=1.000, ratio=1.102, hyp_len=13474, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.321.0.49-1.62.0.40-1.49.4.19-65.85.3.76-42.85.pth, mybk
BLEU = 9.18, 32.3/12.1/5.9/3.1 (BP=1.000, ratio=1.127, hyp_len=12879, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.321.0.49-1.62.0.40-1.49.4.19-65.85.3.76-42.85.pth, bkmy
BLEU = 11.19, 38.1/15.5/7.3/3.7 (BP=1.000, ratio=1.075, hyp_len=13143, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.322.0.50-1.65.0.42-1.52.4.18-65.18.3.78-43.79.pth, mybk
BLEU = 8.80, 32.4/11.7/5.5/2.9 (BP=1.000, ratio=1.133, hyp_len=12949, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.322.0.50-1.65.0.42-1.52.4.18-65.18.3.78-43.79.pth, bkmy
BLEU = 10.30, 36.5/14.6/6.6/3.2 (BP=1.000, ratio=1.120, hyp_len=13694, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.83-16.93.2.59-13.34.2.75-15.70.2.46-11.73.pth, mybk
BLEU = 6.14, 27.6/9.2/3.8/1.5 (BP=1.000, ratio=1.119, hyp_len=12794, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.83-16.93.2.59-13.34.2.75-15.70.2.46-11.73.pth, bkmy
BLEU = 8.13, 34.4/13.0/5.0/1.9 (BP=1.000, ratio=1.057, hyp_len=12930, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.323.0.53-1.70.0.46-1.59.4.15-63.74.3.79-44.27.pth, mybk
BLEU = 9.32, 33.1/12.3/6.0/3.1 (BP=1.000, ratio=1.125, hyp_len=12857, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.323.0.53-1.70.0.46-1.59.4.15-63.74.3.79-44.27.pth, bkmy
BLEU = 10.72, 37.2/15.1/7.0/3.4 (BP=1.000, ratio=1.108, hyp_len=13546, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.324.0.51-1.66.0.40-1.49.4.14-62.53.3.76-43.08.pth, mybk
BLEU = 9.59, 33.1/12.4/6.2/3.3 (BP=1.000, ratio=1.132, hyp_len=12942, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.324.0.51-1.66.0.40-1.49.4.14-62.53.3.76-43.08.pth, bkmy
BLEU = 10.53, 36.8/14.7/6.8/3.3 (BP=1.000, ratio=1.100, hyp_len=13449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.325.0.52-1.68.0.41-1.51.4.17-64.80.3.74-42.25.pth, mybk
BLEU = 9.04, 32.8/12.0/5.7/3.0 (BP=1.000, ratio=1.121, hyp_len=12811, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.325.0.52-1.68.0.41-1.51.4.17-64.80.3.74-42.25.pth, bkmy
BLEU = 11.08, 37.1/15.3/7.2/3.7 (BP=1.000, ratio=1.112, hyp_len=13595, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.326.0.51-1.67.0.42-1.52.4.16-63.91.3.74-41.89.pth, mybk
BLEU = 9.10, 32.7/12.1/5.7/3.1 (BP=1.000, ratio=1.121, hyp_len=12810, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.326.0.51-1.67.0.42-1.52.4.16-63.91.3.74-41.89.pth, bkmy
BLEU = 10.99, 37.4/15.5/7.2/3.5 (BP=1.000, ratio=1.111, hyp_len=13587, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.327.0.54-1.71.0.43-1.54.4.25-69.83.3.80-44.60.pth, mybk
BLEU = 8.94, 32.1/11.7/5.6/3.0 (BP=1.000, ratio=1.133, hyp_len=12949, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.327.0.54-1.71.0.43-1.54.4.25-69.83.3.80-44.60.pth, bkmy
BLEU = 10.64, 36.8/14.8/6.9/3.4 (BP=1.000, ratio=1.117, hyp_len=13666, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.328.0.49-1.63.0.39-1.48.4.21-67.05.3.78-43.95.pth, mybk
BLEU = 8.96, 33.1/12.3/5.6/2.8 (BP=1.000, ratio=1.122, hyp_len=12831, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.328.0.49-1.63.0.39-1.48.4.21-67.05.3.78-43.95.pth, bkmy
BLEU = 11.13, 37.1/15.3/7.3/3.7 (BP=1.000, ratio=1.094, hyp_len=13380, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.329.0.48-1.62.0.39-1.48.4.20-66.87.3.79-44.15.pth, mybk
BLEU = 8.98, 32.7/11.9/5.5/3.0 (BP=1.000, ratio=1.133, hyp_len=12952, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.329.0.48-1.62.0.39-1.48.4.20-66.87.3.79-44.15.pth, bkmy
BLEU = 10.88, 36.9/15.1/7.0/3.6 (BP=1.000, ratio=1.100, hyp_len=13452, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.330.0.48-1.62.0.39-1.48.4.22-67.98.3.75-42.47.pth, mybk
BLEU = 9.47, 33.5/12.6/6.0/3.2 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.330.0.48-1.62.0.39-1.48.4.22-67.98.3.75-42.47.pth, bkmy
BLEU = 10.84, 37.0/15.2/7.0/3.5 (BP=1.000, ratio=1.108, hyp_len=13555, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.331.0.50-1.64.0.40-1.49.4.15-63.30.3.78-43.86.pth, mybk
BLEU = 9.61, 33.2/12.5/6.1/3.3 (BP=1.000, ratio=1.122, hyp_len=12821, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.331.0.50-1.64.0.40-1.49.4.15-63.30.3.78-43.86.pth, bkmy
BLEU = 10.95, 37.0/15.1/7.2/3.6 (BP=1.000, ratio=1.098, hyp_len=13426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.332.0.50-1.65.0.40-1.50.4.15-63.32.3.76-43.00.pth, mybk
BLEU = 9.19, 33.1/12.0/5.7/3.1 (BP=1.000, ratio=1.124, hyp_len=12848, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.332.0.50-1.65.0.40-1.50.4.15-63.32.3.76-43.00.pth, bkmy
BLEU = 11.08, 36.9/15.3/7.2/3.7 (BP=1.000, ratio=1.116, hyp_len=13647, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.78-16.05.2.54-12.74.2.74-15.48.2.44-11.52.pth, mybk
BLEU = 8.06, 31.1/11.4/5.2/2.3 (BP=1.000, ratio=1.059, hyp_len=12105, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.78-16.05.2.54-12.74.2.74-15.48.2.44-11.52.pth, bkmy
BLEU = 8.98, 36.6/14.4/5.6/2.2 (BP=0.999, ratio=0.999, hyp_len=12224, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.333.0.49-1.63.0.39-1.48.4.17-64.47.3.77-43.37.pth, mybk
BLEU = 8.88, 32.8/12.0/5.5/2.9 (BP=1.000, ratio=1.128, hyp_len=12891, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.333.0.49-1.63.0.39-1.48.4.17-64.47.3.77-43.37.pth, bkmy
BLEU = 11.56, 37.7/15.9/7.6/3.9 (BP=1.000, ratio=1.102, hyp_len=13483, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.334.0.49-1.63.0.39-1.48.4.20-67.01.3.77-43.56.pth, mybk
BLEU = 8.83, 32.5/11.9/5.5/2.8 (BP=1.000, ratio=1.132, hyp_len=12946, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.334.0.49-1.63.0.39-1.48.4.20-67.01.3.77-43.56.pth, bkmy
BLEU = 11.37, 38.2/15.8/7.4/3.8 (BP=1.000, ratio=1.086, hyp_len=13287, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.335.0.49-1.64.0.39-1.48.4.17-64.71.3.81-44.98.pth, mybk
BLEU = 8.73, 32.4/11.9/5.3/2.8 (BP=1.000, ratio=1.132, hyp_len=12946, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.335.0.49-1.64.0.39-1.48.4.17-64.71.3.81-44.98.pth, bkmy
BLEU = 10.88, 37.2/15.5/7.2/3.4 (BP=1.000, ratio=1.108, hyp_len=13547, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.336.0.48-1.61.0.39-1.48.4.16-64.09.3.78-43.94.pth, mybk
BLEU = 9.16, 32.9/12.1/5.8/3.0 (BP=1.000, ratio=1.128, hyp_len=12898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.336.0.48-1.61.0.39-1.48.4.16-64.09.3.78-43.94.pth, bkmy
BLEU = 11.75, 37.8/16.0/7.7/4.1 (BP=1.000, ratio=1.081, hyp_len=13223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.337.0.49-1.63.0.40-1.49.4.16-63.94.3.81-45.34.pth, mybk
BLEU = 9.14, 32.7/12.0/5.8/3.1 (BP=1.000, ratio=1.132, hyp_len=12942, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.337.0.49-1.63.0.40-1.49.4.16-63.94.3.81-45.34.pth, bkmy
BLEU = 11.42, 38.1/16.0/7.5/3.7 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.338.0.50-1.65.0.43-1.54.4.22-67.83.3.82-45.62.pth, mybk
BLEU = 9.11, 32.8/12.2/5.7/3.0 (BP=1.000, ratio=1.131, hyp_len=12933, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.338.0.50-1.65.0.43-1.54.4.22-67.83.3.82-45.62.pth, bkmy
BLEU = 11.10, 37.5/15.6/7.2/3.6 (BP=1.000, ratio=1.096, hyp_len=13405, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.339.0.49-1.64.0.42-1.52.4.25-69.87.3.81-45.03.pth, mybk
BLEU = 9.40, 33.0/12.5/6.0/3.2 (BP=1.000, ratio=1.110, hyp_len=12685, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.339.0.49-1.64.0.42-1.52.4.25-69.87.3.81-45.03.pth, bkmy
BLEU = 10.74, 36.9/15.1/7.0/3.4 (BP=1.000, ratio=1.103, hyp_len=13492, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.340.0.47-1.60.0.38-1.47.4.18-65.27.3.79-44.35.pth, mybk
BLEU = 9.07, 33.1/12.2/5.7/3.0 (BP=1.000, ratio=1.122, hyp_len=12821, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.340.0.47-1.60.0.38-1.47.4.18-65.27.3.79-44.35.pth, bkmy
BLEU = 10.77, 36.8/15.0/6.9/3.5 (BP=1.000, ratio=1.120, hyp_len=13701, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.341.0.48-1.62.0.38-1.47.4.19-65.86.3.81-45.37.pth, mybk
BLEU = 8.64, 32.1/11.5/5.4/2.8 (BP=1.000, ratio=1.134, hyp_len=12968, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.341.0.48-1.62.0.38-1.47.4.19-65.86.3.81-45.37.pth, bkmy
BLEU = 11.26, 38.0/15.8/7.4/3.6 (BP=1.000, ratio=1.094, hyp_len=13386, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.342.0.49-1.63.0.39-1.48.4.22-67.94.3.81-45.32.pth, mybk
BLEU = 8.51, 32.4/11.5/5.3/2.7 (BP=1.000, ratio=1.115, hyp_len=12750, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.342.0.49-1.63.0.39-1.48.4.22-67.94.3.81-45.32.pth, bkmy
BLEU = 11.44, 38.4/15.9/7.5/3.7 (BP=1.000, ratio=1.077, hyp_len=13177, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.79-16.31.2.57-13.12.2.71-15.08.2.44-11.47.pth, mybk
BLEU = 7.45, 30.2/10.6/4.7/2.1 (BP=1.000, ratio=1.087, hyp_len=12422, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.79-16.31.2.57-13.12.2.71-15.08.2.44-11.47.pth, bkmy
BLEU = 6.31, 26.5/10.0/3.9/1.5 (BP=1.000, ratio=1.393, hyp_len=17035, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.343.0.52-1.68.0.41-1.50.4.21-67.45.3.80-44.63.pth, mybk
BLEU = 8.64, 32.2/11.6/5.3/2.8 (BP=1.000, ratio=1.127, hyp_len=12888, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.343.0.52-1.68.0.41-1.50.4.21-67.45.3.80-44.63.pth, bkmy
BLEU = 11.30, 37.7/15.6/7.3/3.8 (BP=1.000, ratio=1.103, hyp_len=13493, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.344.0.58-1.79.0.43-1.53.4.19-66.10.3.81-45.28.pth, mybk
BLEU = 9.02, 32.3/11.9/5.7/3.0 (BP=1.000, ratio=1.123, hyp_len=12843, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.344.0.58-1.79.0.43-1.53.4.19-66.10.3.81-45.28.pth, bkmy
BLEU = 11.23, 37.8/15.7/7.3/3.7 (BP=1.000, ratio=1.092, hyp_len=13359, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.345.0.48-1.62.0.39-1.48.4.20-66.78.3.84-46.62.pth, mybk
BLEU = 9.44, 33.3/12.6/6.0/3.2 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.345.0.48-1.62.0.39-1.48.4.20-66.78.3.84-46.62.pth, bkmy
BLEU = 10.96, 37.5/15.5/7.1/3.5 (BP=1.000, ratio=1.095, hyp_len=13393, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.346.0.49-1.63.0.40-1.49.4.21-67.35.3.82-45.71.pth, mybk
BLEU = 8.88, 32.5/11.9/5.5/2.9 (BP=1.000, ratio=1.131, hyp_len=12925, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.346.0.49-1.63.0.40-1.49.4.21-67.35.3.82-45.71.pth, bkmy
BLEU = 11.21, 37.9/15.6/7.3/3.7 (BP=1.000, ratio=1.102, hyp_len=13483, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.347.0.48-1.62.0.39-1.48.4.29-72.75.3.80-44.81.pth, mybk
BLEU = 9.13, 32.6/12.2/5.7/3.0 (BP=1.000, ratio=1.120, hyp_len=12802, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.347.0.48-1.62.0.39-1.48.4.29-72.75.3.80-44.81.pth, bkmy
BLEU = 10.81, 37.0/15.0/7.0/3.5 (BP=1.000, ratio=1.101, hyp_len=13462, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.348.0.47-1.60.0.36-1.44.4.23-68.52.3.80-44.65.pth, mybk
BLEU = 8.76, 32.8/11.8/5.4/2.8 (BP=1.000, ratio=1.124, hyp_len=12851, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.348.0.47-1.60.0.36-1.44.4.23-68.52.3.80-44.65.pth, bkmy
BLEU = 10.81, 37.1/15.1/7.1/3.5 (BP=1.000, ratio=1.112, hyp_len=13600, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.349.0.50-1.66.0.47-1.60.4.24-69.46.3.81-45.32.pth, mybk
BLEU = 9.03, 32.3/11.8/5.6/3.1 (BP=1.000, ratio=1.138, hyp_len=13005, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.349.0.50-1.66.0.47-1.60.4.24-69.46.3.81-45.32.pth, bkmy
BLEU = 10.69, 37.0/15.0/6.9/3.4 (BP=1.000, ratio=1.112, hyp_len=13596, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.350.0.48-1.62.0.40-1.49.4.30-73.37.3.78-44.04.pth, mybk
BLEU = 9.15, 32.6/12.1/5.8/3.1 (BP=1.000, ratio=1.123, hyp_len=12840, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.350.0.48-1.62.0.40-1.49.4.30-73.37.3.78-44.04.pth, bkmy
BLEU = 11.38, 37.2/15.7/7.5/3.8 (BP=1.000, ratio=1.107, hyp_len=13543, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.351.0.47-1.61.0.37-1.45.4.24-69.41.3.81-44.94.pth, mybk
BLEU = 8.59, 31.8/11.4/5.3/2.8 (BP=1.000, ratio=1.141, hyp_len=13043, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.351.0.47-1.61.0.37-1.45.4.24-69.41.3.81-44.94.pth, bkmy
BLEU = 11.24, 37.7/15.7/7.3/3.7 (BP=1.000, ratio=1.094, hyp_len=13385, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.352.0.48-1.61.0.39-1.47.4.28-71.98.3.82-45.82.pth, mybk
BLEU = 9.10, 32.9/12.0/5.7/3.0 (BP=1.000, ratio=1.114, hyp_len=12733, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.352.0.48-1.61.0.39-1.47.4.28-71.98.3.82-45.82.pth, bkmy
BLEU = 10.94, 37.6/15.5/7.1/3.5 (BP=1.000, ratio=1.098, hyp_len=13430, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.67-14.45.2.45-11.57.2.72-15.21.2.42-11.27.pth, mybk
BLEU = 7.18, 29.9/10.6/4.5/1.9 (BP=1.000, ratio=1.106, hyp_len=12647, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.67-14.45.2.45-11.57.2.72-15.21.2.42-11.27.pth, bkmy
BLEU = 8.45, 35.1/13.5/5.3/2.0 (BP=1.000, ratio=1.058, hyp_len=12936, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.353.0.47-1.59.0.36-1.44.4.27-71.69.3.80-44.83.pth, mybk
BLEU = 8.96, 32.3/11.7/5.5/3.1 (BP=1.000, ratio=1.120, hyp_len=12806, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.353.0.47-1.59.0.36-1.44.4.27-71.69.3.80-44.83.pth, bkmy
BLEU = 11.20, 36.9/15.3/7.3/3.8 (BP=1.000, ratio=1.115, hyp_len=13640, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.354.0.48-1.61.0.37-1.45.4.25-69.94.3.88-48.24.pth, mybk
BLEU = 8.99, 32.8/12.0/5.6/3.0 (BP=1.000, ratio=1.113, hyp_len=12723, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.354.0.48-1.61.0.37-1.45.4.25-69.94.3.88-48.24.pth, bkmy
BLEU = 10.48, 35.9/14.4/6.7/3.5 (BP=1.000, ratio=1.128, hyp_len=13798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.355.0.48-1.62.0.38-1.46.4.27-71.41.3.84-46.57.pth, mybk
BLEU = 9.14, 32.5/12.2/5.8/3.1 (BP=1.000, ratio=1.128, hyp_len=12892, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.355.0.48-1.62.0.38-1.46.4.27-71.41.3.84-46.57.pth, bkmy
BLEU = 11.17, 37.1/15.2/7.3/3.8 (BP=1.000, ratio=1.097, hyp_len=13422, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.356.0.46-1.58.0.37-1.45.4.25-70.45.3.88-48.65.pth, mybk
BLEU = 8.72, 32.5/11.7/5.3/2.9 (BP=1.000, ratio=1.126, hyp_len=12878, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.356.0.46-1.58.0.37-1.45.4.25-70.45.3.88-48.65.pth, bkmy
BLEU = 10.78, 37.3/15.1/7.0/3.4 (BP=1.000, ratio=1.085, hyp_len=13269, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.357.0.46-1.58.0.37-1.45.4.28-72.30.3.89-48.89.pth, mybk
BLEU = 9.36, 32.6/12.0/5.9/3.4 (BP=1.000, ratio=1.129, hyp_len=12912, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.357.0.46-1.58.0.37-1.45.4.28-72.30.3.89-48.89.pth, bkmy
BLEU = 10.81, 37.2/15.1/6.9/3.5 (BP=1.000, ratio=1.095, hyp_len=13389, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.358.0.44-1.55.0.36-1.44.4.26-70.70.3.93-50.91.pth, mybk
BLEU = 9.37, 33.5/12.4/5.9/3.1 (BP=1.000, ratio=1.105, hyp_len=12630, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.358.0.44-1.55.0.36-1.44.4.26-70.70.3.93-50.91.pth, bkmy
BLEU = 10.63, 37.2/15.0/6.8/3.3 (BP=1.000, ratio=1.107, hyp_len=13545, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.359.0.45-1.57.0.37-1.44.4.27-71.81.3.87-47.96.pth, mybk
BLEU = 8.58, 32.4/11.7/5.2/2.7 (BP=1.000, ratio=1.130, hyp_len=12915, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.359.0.45-1.57.0.37-1.44.4.27-71.81.3.87-47.96.pth, bkmy
BLEU = 10.46, 37.0/14.8/6.7/3.3 (BP=1.000, ratio=1.103, hyp_len=13494, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.360.0.46-1.59.0.36-1.44.4.26-71.07.3.93-50.77.pth, mybk
BLEU = 8.58, 32.5/11.8/5.2/2.7 (BP=1.000, ratio=1.115, hyp_len=12748, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.360.0.46-1.59.0.36-1.44.4.26-71.07.3.93-50.77.pth, bkmy
BLEU = 11.24, 37.2/15.4/7.3/3.8 (BP=1.000, ratio=1.111, hyp_len=13589, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.361.0.46-1.58.0.39-1.47.4.28-72.15.3.86-47.50.pth, mybk
BLEU = 9.30, 33.1/12.2/5.8/3.2 (BP=1.000, ratio=1.116, hyp_len=12758, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.361.0.46-1.58.0.39-1.47.4.28-72.15.3.86-47.50.pth, bkmy
BLEU = 11.03, 37.6/15.5/7.1/3.6 (BP=1.000, ratio=1.105, hyp_len=13511, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.362.0.45-1.56.0.38-1.47.4.29-72.87.3.88-48.32.pth, mybk
BLEU = 9.12, 32.7/12.0/5.7/3.1 (BP=1.000, ratio=1.128, hyp_len=12896, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.362.0.45-1.56.0.38-1.47.4.29-72.87.3.88-48.32.pth, bkmy
BLEU = 11.26, 37.4/15.5/7.4/3.7 (BP=1.000, ratio=1.099, hyp_len=13445, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.67-14.48.2.45-11.61.2.70-14.94.2.40-11.07.pth, mybk
BLEU = 7.71, 30.4/11.1/4.8/2.2 (BP=1.000, ratio=1.111, hyp_len=12703, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.67-14.48.2.45-11.61.2.70-14.94.2.40-11.07.pth, bkmy
BLEU = 9.07, 36.1/14.0/5.8/2.3 (BP=1.000, ratio=1.044, hyp_len=12769, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.363.0.46-1.58.0.38-1.46.4.35-77.34.3.86-47.54.pth, mybk
BLEU = 9.31, 33.5/12.3/5.8/3.1 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.363.0.46-1.58.0.38-1.46.4.35-77.34.3.86-47.54.pth, bkmy
BLEU = 10.98, 37.3/15.2/7.1/3.6 (BP=1.000, ratio=1.100, hyp_len=13455, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.364.0.47-1.60.0.41-1.50.4.26-71.01.3.89-48.71.pth, mybk
BLEU = 9.22, 33.2/12.1/5.8/3.1 (BP=1.000, ratio=1.121, hyp_len=12812, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.364.0.47-1.60.0.41-1.50.4.26-71.01.3.89-48.71.pth, bkmy
BLEU = 11.53, 37.9/15.7/7.6/3.9 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.365.0.46-1.59.0.37-1.44.4.29-73.00.3.91-50.08.pth, mybk
BLEU = 8.68, 31.8/11.5/5.3/2.9 (BP=1.000, ratio=1.140, hyp_len=13032, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.365.0.46-1.59.0.37-1.44.4.29-73.00.3.91-50.08.pth, bkmy
BLEU = 10.34, 36.7/14.6/6.7/3.2 (BP=1.000, ratio=1.126, hyp_len=13777, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.366.0.47-1.61.0.41-1.50.4.29-72.83.3.94-51.42.pth, mybk
BLEU = 8.93, 32.7/12.0/5.5/2.9 (BP=1.000, ratio=1.131, hyp_len=12924, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.366.0.47-1.61.0.41-1.50.4.29-72.83.3.94-51.42.pth, bkmy
BLEU = 11.40, 37.7/15.8/7.5/3.8 (BP=1.000, ratio=1.112, hyp_len=13601, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.367.0.45-1.57.0.37-1.44.4.34-77.08.3.92-50.63.pth, mybk
BLEU = 9.40, 33.5/12.5/5.9/3.2 (BP=1.000, ratio=1.115, hyp_len=12752, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.367.0.45-1.57.0.37-1.44.4.34-77.08.3.92-50.63.pth, bkmy
BLEU = 10.96, 37.6/15.4/7.1/3.5 (BP=1.000, ratio=1.098, hyp_len=13432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.368.0.46-1.59.0.38-1.46.4.33-76.16.3.92-50.32.pth, mybk
BLEU = 8.54, 32.1/11.6/5.3/2.7 (BP=1.000, ratio=1.134, hyp_len=12967, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.368.0.46-1.59.0.38-1.46.4.33-76.16.3.92-50.32.pth, bkmy
BLEU = 11.18, 37.6/15.6/7.4/3.6 (BP=1.000, ratio=1.104, hyp_len=13500, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.369.0.53-1.70.0.37-1.45.4.35-77.18.3.86-47.44.pth, mybk
BLEU = 9.19, 33.2/12.1/5.7/3.1 (BP=1.000, ratio=1.118, hyp_len=12781, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.369.0.53-1.70.0.37-1.45.4.35-77.18.3.86-47.44.pth, bkmy
BLEU = 10.33, 36.5/14.7/6.6/3.2 (BP=1.000, ratio=1.110, hyp_len=13573, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.370.0.46-1.59.0.40-1.49.4.23-68.66.3.88-48.61.pth, mybk
BLEU = 8.91, 33.2/11.9/5.6/2.9 (BP=1.000, ratio=1.109, hyp_len=12677, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.370.0.46-1.59.0.40-1.49.4.23-68.66.3.88-48.61.pth, bkmy
BLEU = 11.01, 37.6/15.4/7.1/3.6 (BP=1.000, ratio=1.091, hyp_len=13343, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.371.0.48-1.62.0.40-1.50.4.31-74.76.3.87-48.04.pth, mybk
BLEU = 9.09, 33.1/12.0/5.6/3.1 (BP=1.000, ratio=1.120, hyp_len=12803, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.371.0.48-1.62.0.40-1.50.4.31-74.76.3.87-48.04.pth, bkmy
BLEU = 10.62, 37.3/15.0/6.8/3.3 (BP=1.000, ratio=1.085, hyp_len=13273, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.372.0.45-1.56.0.37-1.44.4.29-73.05.3.88-48.30.pth, mybk
BLEU = 8.75, 32.8/11.7/5.4/2.9 (BP=1.000, ratio=1.123, hyp_len=12836, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.372.0.45-1.56.0.37-1.44.4.29-73.05.3.88-48.30.pth, bkmy
BLEU = 10.84, 37.3/15.3/7.0/3.5 (BP=1.000, ratio=1.091, hyp_len=13344, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.63-13.88.2.41-11.17.2.69-14.75.2.40-11.05.pth, mybk
BLEU = 7.55, 30.1/10.9/4.8/2.1 (BP=1.000, ratio=1.134, hyp_len=12966, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.63-13.88.2.41-11.17.2.69-14.75.2.40-11.05.pth, bkmy
BLEU = 8.94, 35.3/14.0/5.7/2.3 (BP=1.000, ratio=1.059, hyp_len=12957, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.373.0.53-1.70.0.41-1.50.4.29-73.11.3.89-49.14.pth, mybk
BLEU = 8.97, 32.5/11.9/5.6/3.0 (BP=1.000, ratio=1.131, hyp_len=12927, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.373.0.53-1.70.0.41-1.50.4.29-73.11.3.89-49.14.pth, bkmy
BLEU = 10.53, 37.0/14.9/6.7/3.3 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.374.0.45-1.57.0.36-1.43.4.33-75.68.3.97-53.10.pth, mybk
BLEU = 8.49, 31.9/11.4/5.2/2.8 (BP=1.000, ratio=1.117, hyp_len=12775, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.374.0.45-1.57.0.36-1.43.4.33-75.68.3.97-53.10.pth, bkmy
BLEU = 11.03, 37.2/15.4/7.2/3.6 (BP=1.000, ratio=1.121, hyp_len=13713, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.375.0.50-1.66.0.38-1.46.4.31-74.21.3.90-49.19.pth, mybk
BLEU = 8.67, 32.8/11.5/5.3/2.8 (BP=1.000, ratio=1.115, hyp_len=12743, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.375.0.50-1.66.0.38-1.46.4.31-74.21.3.90-49.19.pth, bkmy
BLEU = 10.71, 36.7/15.1/6.9/3.4 (BP=1.000, ratio=1.117, hyp_len=13658, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.376.0.54-1.72.0.41-1.51.4.30-73.74.3.93-50.90.pth, mybk
BLEU = 8.48, 33.0/11.7/5.2/2.6 (BP=1.000, ratio=1.111, hyp_len=12697, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.376.0.54-1.72.0.41-1.51.4.30-73.74.3.93-50.90.pth, bkmy
BLEU = 10.78, 36.9/15.0/7.0/3.4 (BP=1.000, ratio=1.113, hyp_len=13612, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.377.0.45-1.58.0.39-1.48.4.27-71.82.3.92-50.43.pth, mybk
BLEU = 9.17, 33.2/12.0/5.7/3.1 (BP=1.000, ratio=1.114, hyp_len=12730, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.377.0.45-1.58.0.39-1.48.4.27-71.82.3.92-50.43.pth, bkmy
BLEU = 11.06, 37.9/15.6/7.1/3.6 (BP=1.000, ratio=1.103, hyp_len=13492, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.378.0.43-1.54.0.35-1.41.4.31-74.43.3.92-50.24.pth, mybk
BLEU = 8.58, 32.7/11.6/5.3/2.7 (BP=1.000, ratio=1.129, hyp_len=12903, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.378.0.43-1.54.0.35-1.41.4.31-74.43.3.92-50.24.pth, bkmy
BLEU = 11.62, 37.6/15.9/7.7/4.0 (BP=1.000, ratio=1.089, hyp_len=13320, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.379.0.44-1.56.0.37-1.45.4.39-80.46.3.90-49.43.pth, mybk
BLEU = 8.88, 32.8/11.7/5.4/3.0 (BP=1.000, ratio=1.126, hyp_len=12868, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.379.0.44-1.56.0.37-1.45.4.39-80.46.3.90-49.43.pth, bkmy
BLEU = 11.11, 37.6/15.4/7.2/3.6 (BP=1.000, ratio=1.102, hyp_len=13479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.380.0.44-1.55.0.37-1.44.4.31-74.60.3.94-51.57.pth, mybk
BLEU = 8.79, 33.0/11.9/5.4/2.8 (BP=1.000, ratio=1.127, hyp_len=12889, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.380.0.44-1.55.0.37-1.44.4.31-74.60.3.94-51.57.pth, bkmy
BLEU = 10.94, 37.4/15.5/7.1/3.5 (BP=1.000, ratio=1.106, hyp_len=13529, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.381.0.44-1.55.0.36-1.43.4.39-80.52.3.96-52.32.pth, mybk
BLEU = 8.65, 32.4/11.8/5.4/2.7 (BP=1.000, ratio=1.141, hyp_len=13045, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.381.0.44-1.55.0.36-1.43.4.39-80.52.3.96-52.32.pth, bkmy
BLEU = 11.04, 37.3/15.3/7.2/3.6 (BP=1.000, ratio=1.092, hyp_len=13361, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.382.0.46-1.58.0.38-1.46.4.30-73.61.3.99-54.15.pth, mybk
BLEU = 8.95, 32.8/12.0/5.6/2.9 (BP=1.000, ratio=1.113, hyp_len=12729, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.382.0.46-1.58.0.38-1.46.4.30-73.61.3.99-54.15.pth, bkmy
BLEU = 10.43, 36.7/14.7/6.7/3.2 (BP=1.000, ratio=1.122, hyp_len=13718, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.61-13.57.2.38-10.77.2.71-15.06.2.36-10.64.pth, mybk
BLEU = 7.48, 30.5/10.7/4.7/2.0 (BP=1.000, ratio=1.086, hyp_len=12412, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.61-13.57.2.38-10.77.2.71-15.06.2.36-10.64.pth, bkmy
BLEU = 9.41, 36.1/14.7/6.1/2.4 (BP=1.000, ratio=1.058, hyp_len=12944, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.383.0.46-1.59.0.36-1.44.4.34-76.80.3.93-50.94.pth, mybk
BLEU = 8.83, 32.7/11.8/5.4/2.9 (BP=1.000, ratio=1.121, hyp_len=12820, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.383.0.46-1.59.0.36-1.44.4.34-76.80.3.93-50.94.pth, bkmy
BLEU = 11.31, 38.1/15.5/7.3/3.8 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.384.0.44-1.56.0.35-1.42.4.36-77.98.3.95-52.10.pth, mybk
BLEU = 8.83, 33.1/12.0/5.5/2.8 (BP=1.000, ratio=1.127, hyp_len=12889, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.384.0.44-1.56.0.35-1.42.4.36-77.98.3.95-52.10.pth, bkmy
BLEU = 11.60, 37.2/15.8/7.7/4.0 (BP=1.000, ratio=1.109, hyp_len=13563, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.385.0.43-1.53.0.34-1.41.4.38-79.93.3.94-51.19.pth, mybk
BLEU = 9.08, 33.0/12.0/5.6/3.1 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.385.0.43-1.53.0.34-1.41.4.38-79.93.3.94-51.19.pth, bkmy
BLEU = 10.95, 37.4/15.1/7.0/3.6 (BP=1.000, ratio=1.103, hyp_len=13485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.386.0.44-1.56.0.36-1.44.4.37-79.21.3.98-53.48.pth, mybk
BLEU = 8.92, 32.7/11.8/5.5/3.0 (BP=1.000, ratio=1.128, hyp_len=12890, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.386.0.44-1.56.0.36-1.44.4.37-79.21.3.98-53.48.pth, bkmy
BLEU = 10.84, 37.5/15.3/6.9/3.5 (BP=1.000, ratio=1.091, hyp_len=13347, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.387.0.52-1.68.0.40-1.49.4.38-79.74.3.94-51.21.pth, mybk
BLEU = 8.70, 32.6/11.9/5.4/2.8 (BP=1.000, ratio=1.134, hyp_len=12960, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.387.0.52-1.68.0.40-1.49.4.38-79.74.3.94-51.21.pth, bkmy
BLEU = 11.23, 37.2/15.5/7.3/3.8 (BP=1.000, ratio=1.126, hyp_len=13768, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.388.0.44-1.55.0.37-1.44.4.38-79.60.3.91-50.03.pth, mybk
BLEU = 9.50, 32.9/12.4/6.0/3.3 (BP=1.000, ratio=1.114, hyp_len=12731, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.388.0.44-1.55.0.37-1.44.4.38-79.60.3.91-50.03.pth, bkmy
BLEU = 11.11, 37.6/15.5/7.3/3.6 (BP=1.000, ratio=1.095, hyp_len=13394, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.389.0.45-1.57.0.36-1.44.4.36-77.96.3.93-51.10.pth, mybk
BLEU = 9.01, 32.8/11.8/5.6/3.0 (BP=1.000, ratio=1.120, hyp_len=12803, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.389.0.45-1.57.0.36-1.44.4.36-77.96.3.93-51.10.pth, bkmy
BLEU = 10.92, 37.5/15.4/7.1/3.5 (BP=1.000, ratio=1.098, hyp_len=13433, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.390.0.47-1.60.0.38-1.46.4.36-78.13.3.95-52.04.pth, mybk
BLEU = 8.99, 33.1/12.2/5.6/2.9 (BP=1.000, ratio=1.117, hyp_len=12774, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.390.0.47-1.60.0.38-1.46.4.36-78.13.3.95-52.04.pth, bkmy
BLEU = 10.98, 37.4/15.2/7.0/3.6 (BP=1.000, ratio=1.104, hyp_len=13502, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.391.0.41-1.51.0.35-1.42.4.42-83.05.3.98-53.37.pth, mybk
BLEU = 9.13, 32.9/11.9/5.7/3.1 (BP=1.000, ratio=1.131, hyp_len=12924, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.391.0.41-1.51.0.35-1.42.4.42-83.05.3.98-53.37.pth, bkmy
BLEU = 11.03, 36.8/15.0/7.2/3.7 (BP=1.000, ratio=1.116, hyp_len=13648, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.392.0.45-1.57.0.36-1.44.4.37-78.96.3.98-53.60.pth, mybk
BLEU = 9.39, 33.6/12.2/5.9/3.2 (BP=1.000, ratio=1.106, hyp_len=12641, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.392.0.45-1.57.0.36-1.44.4.37-78.96.3.98-53.60.pth, bkmy
BLEU = 11.11, 37.2/15.4/7.3/3.7 (BP=1.000, ratio=1.089, hyp_len=13319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.62-13.71.2.36-10.58.2.69-14.70.2.38-10.77.pth, mybk
BLEU = 7.77, 29.8/10.9/5.0/2.2 (BP=1.000, ratio=1.154, hyp_len=13190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.62-13.71.2.36-10.58.2.69-14.70.2.38-10.77.pth, bkmy
BLEU = 7.95, 33.1/12.8/5.1/1.9 (BP=1.000, ratio=1.117, hyp_len=13664, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.393.0.42-1.53.0.35-1.42.4.39-80.53.4.00-54.35.pth, mybk
BLEU = 8.90, 33.2/12.1/5.5/2.8 (BP=1.000, ratio=1.117, hyp_len=12768, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.393.0.42-1.53.0.35-1.42.4.39-80.53.4.00-54.35.pth, bkmy
BLEU = 10.58, 37.6/15.0/6.8/3.3 (BP=1.000, ratio=1.103, hyp_len=13495, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.394.0.53-1.70.0.38-1.46.4.44-84.45.3.94-51.26.pth, mybk
BLEU = 8.25, 31.9/11.1/5.0/2.6 (BP=1.000, ratio=1.136, hyp_len=12983, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.394.0.53-1.70.0.38-1.46.4.44-84.45.3.94-51.26.pth, bkmy
BLEU = 10.95, 38.0/15.4/7.1/3.5 (BP=1.000, ratio=1.102, hyp_len=13483, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.395.0.43-1.54.0.35-1.42.4.39-80.87.3.95-52.14.pth, mybk
BLEU = 9.02, 33.0/12.0/5.6/3.0 (BP=1.000, ratio=1.114, hyp_len=12736, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.395.0.43-1.54.0.35-1.42.4.39-80.87.3.95-52.14.pth, bkmy
BLEU = 10.72, 37.7/15.3/7.0/3.3 (BP=1.000, ratio=1.093, hyp_len=13373, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.396.0.42-1.53.0.34-1.40.4.44-85.04.4.02-55.74.pth, mybk
BLEU = 8.59, 32.1/11.4/5.3/2.8 (BP=1.000, ratio=1.114, hyp_len=12730, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.396.0.42-1.53.0.34-1.40.4.44-85.04.4.02-55.74.pth, bkmy
BLEU = 11.34, 37.4/15.5/7.4/3.9 (BP=1.000, ratio=1.110, hyp_len=13573, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.397.0.43-1.53.0.34-1.40.4.42-82.98.4.01-55.31.pth, mybk
BLEU = 9.01, 32.9/11.9/5.6/3.0 (BP=1.000, ratio=1.125, hyp_len=12865, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.397.0.43-1.53.0.34-1.40.4.42-82.98.4.01-55.31.pth, bkmy
BLEU = 10.65, 36.9/15.0/6.9/3.4 (BP=1.000, ratio=1.117, hyp_len=13667, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.398.0.43-1.54.0.34-1.41.4.45-85.94.3.99-53.82.pth, mybk
BLEU = 8.89, 33.2/11.8/5.5/2.9 (BP=1.000, ratio=1.105, hyp_len=12631, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.398.0.43-1.54.0.34-1.41.4.45-85.94.3.99-53.82.pth, bkmy
BLEU = 11.18, 37.7/15.6/7.3/3.6 (BP=1.000, ratio=1.097, hyp_len=13419, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.399.0.41-1.51.0.34-1.40.4.43-84.31.3.97-52.97.pth, mybk
BLEU = 8.71, 32.4/11.7/5.3/2.8 (BP=1.000, ratio=1.130, hyp_len=12914, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.399.0.41-1.51.0.34-1.40.4.43-84.31.3.97-52.97.pth, bkmy
BLEU = 11.02, 37.4/15.4/7.1/3.6 (BP=1.000, ratio=1.101, hyp_len=13467, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.400.0.42-1.52.0.34-1.40.4.44-84.99.4.00-54.54.pth, mybk
BLEU = 8.99, 33.3/12.0/5.5/3.0 (BP=1.000, ratio=1.119, hyp_len=12797, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.400.0.42-1.52.0.34-1.40.4.44-84.99.4.00-54.54.pth, bkmy
BLEU = 10.95, 37.6/15.4/7.1/3.5 (BP=1.000, ratio=1.101, hyp_len=13466, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.401.0.42-1.51.0.34-1.40.4.43-83.79.3.97-52.75.pth, mybk
BLEU = 8.65, 32.6/11.5/5.3/2.8 (BP=1.000, ratio=1.117, hyp_len=12768, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.401.0.42-1.51.0.34-1.40.4.43-83.79.3.97-52.75.pth, bkmy
BLEU = 10.87, 38.0/15.5/7.0/3.4 (BP=1.000, ratio=1.093, hyp_len=13373, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.402.0.44-1.56.0.36-1.43.4.42-83.47.4.02-55.88.pth, mybk
BLEU = 9.08, 32.6/11.8/5.6/3.1 (BP=1.000, ratio=1.122, hyp_len=12826, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.402.0.44-1.56.0.36-1.43.4.42-83.47.4.02-55.88.pth, bkmy
BLEU = 10.77, 37.2/15.1/6.9/3.5 (BP=1.000, ratio=1.121, hyp_len=13708, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.57-13.10.2.35-10.53.2.69-14.80.2.37-10.71.pth, mybk
BLEU = 7.67, 29.8/11.0/4.8/2.2 (BP=1.000, ratio=1.146, hyp_len=13105, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.57-13.10.2.35-10.53.2.69-14.80.2.37-10.71.pth, bkmy
BLEU = 9.26, 35.8/14.4/5.9/2.4 (BP=1.000, ratio=1.072, hyp_len=13108, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.403.0.42-1.53.0.35-1.41.4.45-85.65.3.98-53.59.pth, mybk
BLEU = 8.62, 32.2/11.6/5.3/2.8 (BP=1.000, ratio=1.143, hyp_len=13071, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.403.0.42-1.53.0.35-1.41.4.45-85.65.3.98-53.59.pth, bkmy
BLEU = 10.98, 37.3/15.2/7.0/3.7 (BP=1.000, ratio=1.107, hyp_len=13534, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.404.0.42-1.52.0.34-1.41.4.43-83.70.4.06-57.81.pth, mybk
BLEU = 8.69, 32.3/11.5/5.4/2.9 (BP=1.000, ratio=1.114, hyp_len=12736, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.404.0.42-1.52.0.34-1.41.4.43-83.70.4.06-57.81.pth, bkmy
BLEU = 10.93, 36.8/15.0/7.0/3.7 (BP=1.000, ratio=1.115, hyp_len=13634, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.405.0.50-1.65.0.38-1.46.4.49-89.53.4.03-56.32.pth, mybk
BLEU = 8.92, 32.7/11.9/5.5/2.9 (BP=1.000, ratio=1.118, hyp_len=12776, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.405.0.50-1.65.0.38-1.46.4.49-89.53.4.03-56.32.pth, bkmy
BLEU = 11.01, 37.3/15.5/7.1/3.6 (BP=1.000, ratio=1.109, hyp_len=13567, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.406.0.42-1.52.0.34-1.41.4.44-84.84.4.00-54.55.pth, mybk
BLEU = 8.49, 32.2/11.4/5.3/2.7 (BP=1.000, ratio=1.134, hyp_len=12967, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.406.0.42-1.52.0.34-1.41.4.44-84.84.4.00-54.55.pth, bkmy
BLEU = 10.59, 36.9/14.8/6.8/3.4 (BP=1.000, ratio=1.116, hyp_len=13651, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.407.0.43-1.54.0.34-1.40.4.44-84.83.3.99-53.90.pth, mybk
BLEU = 8.82, 32.4/11.9/5.5/2.8 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.407.0.43-1.54.0.34-1.40.4.44-84.83.3.99-53.90.pth, bkmy
BLEU = 10.93, 37.3/15.2/7.1/3.5 (BP=1.000, ratio=1.094, hyp_len=13379, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.408.0.44-1.55.0.37-1.44.4.41-82.60.4.01-55.35.pth, mybk
BLEU = 8.78, 32.3/11.8/5.5/2.9 (BP=1.000, ratio=1.137, hyp_len=13002, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.408.0.44-1.55.0.37-1.44.4.41-82.60.4.01-55.35.pth, bkmy
BLEU = 11.17, 37.4/15.3/7.3/3.7 (BP=1.000, ratio=1.097, hyp_len=13412, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.409.0.50-1.65.0.38-1.46.4.39-80.97.4.00-54.80.pth, mybk
BLEU = 9.11, 33.0/12.1/5.6/3.1 (BP=1.000, ratio=1.120, hyp_len=12807, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.409.0.50-1.65.0.38-1.46.4.39-80.97.4.00-54.80.pth, bkmy
BLEU = 11.30, 37.2/15.5/7.5/3.8 (BP=1.000, ratio=1.095, hyp_len=13398, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.410.0.42-1.52.0.35-1.42.4.44-85.02.3.97-53.22.pth, mybk
BLEU = 8.96, 33.3/12.0/5.5/2.9 (BP=1.000, ratio=1.128, hyp_len=12891, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.410.0.42-1.52.0.35-1.42.4.44-85.02.3.97-53.22.pth, bkmy
BLEU = 11.39, 37.8/15.7/7.4/3.9 (BP=1.000, ratio=1.078, hyp_len=13181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.411.0.44-1.55.0.36-1.43.4.46-86.48.4.01-55.28.pth, mybk
BLEU = 9.47, 32.8/12.3/5.9/3.4 (BP=1.000, ratio=1.127, hyp_len=12886, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.411.0.44-1.55.0.36-1.43.4.46-86.48.4.01-55.28.pth, bkmy
BLEU = 11.01, 37.4/15.2/7.2/3.6 (BP=1.000, ratio=1.094, hyp_len=13378, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.412.0.42-1.52.0.33-1.40.4.47-86.93.4.01-55.30.pth, mybk
BLEU = 8.84, 32.9/11.7/5.4/2.9 (BP=1.000, ratio=1.111, hyp_len=12705, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.412.0.42-1.52.0.33-1.40.4.47-86.93.4.01-55.30.pth, bkmy
BLEU = 10.51, 36.8/14.5/6.8/3.4 (BP=1.000, ratio=1.093, hyp_len=13369, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.49-12.06.2.28-9.81.2.68-14.62.2.36-10.58.pth, mybk
BLEU = 7.88, 30.8/11.1/5.0/2.3 (BP=1.000, ratio=1.124, hyp_len=12847, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.49-12.06.2.28-9.81.2.68-14.62.2.36-10.58.pth, bkmy
BLEU = 8.62, 33.2/13.3/5.5/2.3 (BP=1.000, ratio=1.160, hyp_len=14183, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.413.0.44-1.55.0.34-1.40.4.44-84.43.4.08-59.12.pth, mybk
BLEU = 8.77, 32.5/11.8/5.4/2.9 (BP=1.000, ratio=1.144, hyp_len=13074, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.413.0.44-1.55.0.34-1.40.4.44-84.43.4.08-59.12.pth, bkmy
BLEU = 10.61, 36.6/14.7/6.7/3.5 (BP=1.000, ratio=1.126, hyp_len=13767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.414.0.47-1.59.0.37-1.44.4.43-83.57.4.03-56.49.pth, mybk
BLEU = 8.96, 33.0/12.0/5.6/2.9 (BP=1.000, ratio=1.115, hyp_len=12749, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.414.0.47-1.59.0.37-1.44.4.43-83.57.4.03-56.49.pth, bkmy
BLEU = 11.46, 38.1/15.9/7.5/3.8 (BP=1.000, ratio=1.085, hyp_len=13276, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.415.0.42-1.52.0.35-1.42.4.42-83.37.3.98-53.28.pth, mybk
BLEU = 8.89, 33.1/11.9/5.5/2.9 (BP=1.000, ratio=1.116, hyp_len=12761, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.415.0.42-1.52.0.35-1.42.4.42-83.37.3.98-53.28.pth, bkmy
BLEU = 10.65, 37.2/14.7/6.8/3.4 (BP=1.000, ratio=1.115, hyp_len=13632, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.416.0.42-1.52.0.34-1.41.4.46-86.46.3.99-54.06.pth, mybk
BLEU = 8.02, 31.9/11.0/4.9/2.4 (BP=1.000, ratio=1.139, hyp_len=13021, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.416.0.42-1.52.0.34-1.41.4.46-86.46.3.99-54.06.pth, bkmy
BLEU = 11.14, 36.9/15.4/7.2/3.8 (BP=1.000, ratio=1.110, hyp_len=13571, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.417.0.43-1.54.0.35-1.41.4.46-86.54.4.03-56.31.pth, mybk
BLEU = 8.19, 32.2/11.3/5.0/2.5 (BP=1.000, ratio=1.131, hyp_len=12932, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.417.0.43-1.54.0.35-1.41.4.46-86.54.4.03-56.31.pth, bkmy
BLEU = 10.96, 37.2/15.4/7.1/3.6 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.418.0.42-1.52.0.34-1.40.4.44-84.94.4.04-56.81.pth, mybk
BLEU = 8.68, 32.3/11.5/5.4/2.8 (BP=1.000, ratio=1.146, hyp_len=13097, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.418.0.42-1.52.0.34-1.40.4.44-84.94.4.04-56.81.pth, bkmy
BLEU = 10.87, 36.8/15.0/7.1/3.6 (BP=1.000, ratio=1.108, hyp_len=13549, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.419.0.44-1.55.0.33-1.40.4.44-84.53.4.00-54.58.pth, mybk
BLEU = 9.27, 33.1/12.1/5.8/3.2 (BP=1.000, ratio=1.116, hyp_len=12753, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.419.0.44-1.55.0.33-1.40.4.44-84.53.4.00-54.58.pth, bkmy
BLEU = 10.73, 37.1/15.2/6.9/3.4 (BP=1.000, ratio=1.099, hyp_len=13444, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.420.0.46-1.58.0.36-1.44.4.40-81.54.4.02-55.73.pth, mybk
BLEU = 8.86, 32.7/11.6/5.5/2.9 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.420.0.46-1.58.0.36-1.44.4.40-81.54.4.02-55.73.pth, bkmy
BLEU = 10.89, 36.8/15.0/7.0/3.6 (BP=1.000, ratio=1.105, hyp_len=13511, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.421.0.41-1.51.0.33-1.39.4.50-90.21.4.02-55.55.pth, mybk
BLEU = 8.71, 32.6/12.0/5.4/2.7 (BP=1.000, ratio=1.130, hyp_len=12917, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.421.0.41-1.51.0.33-1.39.4.50-90.21.4.02-55.55.pth, bkmy
BLEU = 11.12, 37.1/15.3/7.2/3.8 (BP=1.000, ratio=1.100, hyp_len=13448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.422.0.40-1.49.0.33-1.39.4.46-86.09.4.02-55.83.pth, mybk
BLEU = 8.78, 32.9/11.9/5.5/2.8 (BP=1.000, ratio=1.118, hyp_len=12776, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.422.0.40-1.49.0.33-1.39.4.46-86.09.4.02-55.83.pth, bkmy
BLEU = 11.01, 37.1/15.3/7.1/3.6 (BP=1.000, ratio=1.120, hyp_len=13703, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.51-12.31.2.28-9.74.2.65-14.22.2.36-10.62.pth, mybk
BLEU = 8.27, 31.5/11.6/5.3/2.4 (BP=1.000, ratio=1.103, hyp_len=12614, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.51-12.31.2.28-9.74.2.65-14.22.2.36-10.62.pth, bkmy
BLEU = 8.99, 35.9/14.0/5.7/2.3 (BP=1.000, ratio=1.095, hyp_len=13397, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.423.0.41-1.51.0.34-1.41.4.49-88.75.4.00-54.72.pth, mybk
BLEU = 9.05, 32.8/11.9/5.7/3.0 (BP=1.000, ratio=1.131, hyp_len=12928, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.423.0.41-1.51.0.34-1.41.4.49-88.75.4.00-54.72.pth, bkmy
BLEU = 11.00, 37.3/15.3/7.1/3.6 (BP=1.000, ratio=1.096, hyp_len=13403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.424.0.44-1.56.0.36-1.43.4.56-95.74.4.05-57.54.pth, mybk
BLEU = 8.96, 32.2/11.8/5.6/3.0 (BP=1.000, ratio=1.142, hyp_len=13054, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.424.0.44-1.56.0.36-1.43.4.56-95.74.4.05-57.54.pth, bkmy
BLEU = 11.09, 37.2/15.2/7.2/3.7 (BP=1.000, ratio=1.099, hyp_len=13447, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.425.0.42-1.52.0.33-1.40.4.53-92.76.4.09-59.69.pth, mybk
BLEU = 9.14, 33.2/12.0/5.7/3.1 (BP=1.000, ratio=1.110, hyp_len=12691, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.425.0.42-1.52.0.33-1.40.4.53-92.76.4.09-59.69.pth, bkmy
BLEU = 10.33, 35.8/14.4/6.6/3.4 (BP=1.000, ratio=1.126, hyp_len=13778, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.426.0.40-1.49.0.35-1.41.4.48-87.80.4.07-58.72.pth, mybk
BLEU = 8.92, 32.8/12.0/5.5/2.9 (BP=1.000, ratio=1.130, hyp_len=12913, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.426.0.40-1.49.0.35-1.41.4.48-87.80.4.07-58.72.pth, bkmy
BLEU = 11.08, 36.9/15.2/7.2/3.8 (BP=1.000, ratio=1.110, hyp_len=13574, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.427.0.42-1.52.0.33-1.39.4.51-91.27.4.10-60.21.pth, mybk
BLEU = 9.13, 33.1/12.1/5.7/3.0 (BP=1.000, ratio=1.109, hyp_len=12679, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.427.0.42-1.52.0.33-1.39.4.51-91.27.4.10-60.21.pth, bkmy
BLEU = 10.85, 36.6/14.8/7.0/3.6 (BP=1.000, ratio=1.114, hyp_len=13621, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.428.0.43-1.53.0.35-1.42.4.55-94.64.4.07-58.31.pth, mybk
BLEU = 8.92, 32.9/11.9/5.5/2.9 (BP=1.000, ratio=1.124, hyp_len=12849, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.428.0.43-1.53.0.35-1.42.4.55-94.64.4.07-58.31.pth, bkmy
BLEU = 10.67, 37.3/14.9/6.9/3.4 (BP=1.000, ratio=1.096, hyp_len=13401, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.429.0.39-1.48.0.33-1.39.4.53-92.94.4.10-60.17.pth, mybk
BLEU = 8.47, 32.5/11.6/5.2/2.7 (BP=1.000, ratio=1.125, hyp_len=12859, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.429.0.39-1.48.0.33-1.39.4.53-92.94.4.10-60.17.pth, bkmy
BLEU = 11.13, 37.4/15.4/7.2/3.7 (BP=1.000, ratio=1.091, hyp_len=13342, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.430.0.40-1.49.0.32-1.38.4.52-92.00.4.08-59.13.pth, mybk
BLEU = 9.07, 33.1/12.0/5.6/3.0 (BP=1.000, ratio=1.125, hyp_len=12863, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.430.0.40-1.49.0.32-1.38.4.52-92.00.4.08-59.13.pth, bkmy
BLEU = 11.20, 37.0/15.4/7.3/3.8 (BP=1.000, ratio=1.103, hyp_len=13485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.431.0.41-1.51.0.34-1.40.4.54-93.31.4.10-60.05.pth, mybk
BLEU = 8.34, 32.2/11.4/5.1/2.6 (BP=1.000, ratio=1.130, hyp_len=12923, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.431.0.41-1.51.0.34-1.40.4.54-93.31.4.10-60.05.pth, bkmy
BLEU = 10.71, 37.4/15.2/6.9/3.4 (BP=1.000, ratio=1.102, hyp_len=13479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.432.0.40-1.50.0.33-1.39.4.53-92.60.4.08-58.93.pth, mybk
BLEU = 8.40, 32.2/11.3/5.1/2.7 (BP=1.000, ratio=1.133, hyp_len=12951, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.432.0.40-1.50.0.33-1.39.4.53-92.60.4.08-58.93.pth, bkmy
BLEU = 11.39, 37.6/15.7/7.5/3.8 (BP=1.000, ratio=1.091, hyp_len=13344, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.49-12.12.2.31-10.06.2.68-14.59.2.37-10.72.pth, mybk
BLEU = 9.10, 32.4/12.5/5.9/2.9 (BP=1.000, ratio=1.083, hyp_len=12386, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.49-12.12.2.31-10.06.2.68-14.59.2.37-10.72.pth, bkmy
BLEU = 8.33, 33.0/13.0/5.3/2.1 (BP=1.000, ratio=1.161, hyp_len=14200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.433.0.40-1.49.0.33-1.39.4.50-89.59.4.11-60.74.pth, mybk
BLEU = 8.67, 32.4/11.5/5.3/2.9 (BP=1.000, ratio=1.128, hyp_len=12901, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.433.0.40-1.49.0.33-1.39.4.50-89.59.4.11-60.74.pth, bkmy
BLEU = 11.12, 37.5/15.3/7.3/3.7 (BP=1.000, ratio=1.109, hyp_len=13570, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.434.0.48-1.62.0.37-1.44.4.48-88.35.4.16-64.28.pth, mybk
BLEU = 8.73, 32.7/11.8/5.4/2.8 (BP=1.000, ratio=1.127, hyp_len=12879, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.434.0.48-1.62.0.37-1.44.4.48-88.35.4.16-64.28.pth, bkmy
BLEU = 11.08, 36.9/15.2/7.2/3.8 (BP=1.000, ratio=1.102, hyp_len=13474, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.435.0.42-1.52.0.33-1.39.4.52-91.76.4.11-61.15.pth, mybk
BLEU = 8.31, 32.0/11.1/5.1/2.7 (BP=1.000, ratio=1.145, hyp_len=13090, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.435.0.42-1.52.0.33-1.39.4.52-91.76.4.11-61.15.pth, bkmy
BLEU = 11.10, 36.8/15.1/7.2/3.8 (BP=1.000, ratio=1.127, hyp_len=13781, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.436.0.43-1.54.0.37-1.45.4.48-88.56.4.11-60.71.pth, mybk
BLEU = 8.83, 32.8/11.8/5.4/2.9 (BP=1.000, ratio=1.120, hyp_len=12800, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.436.0.43-1.54.0.37-1.45.4.48-88.56.4.11-60.71.pth, bkmy
BLEU = 10.88, 36.8/15.0/7.0/3.6 (BP=1.000, ratio=1.123, hyp_len=13737, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.437.0.47-1.60.0.36-1.43.4.52-91.50.4.05-57.65.pth, mybk
BLEU = 8.39, 31.9/11.3/5.1/2.7 (BP=1.000, ratio=1.141, hyp_len=13041, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.437.0.47-1.60.0.36-1.43.4.52-91.50.4.05-57.65.pth, bkmy
BLEU = 11.28, 37.4/15.5/7.4/3.8 (BP=1.000, ratio=1.103, hyp_len=13489, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.438.0.40-1.50.0.33-1.39.4.55-94.59.4.07-58.70.pth, mybk
BLEU = 8.65, 32.8/11.8/5.3/2.7 (BP=1.000, ratio=1.111, hyp_len=12706, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.438.0.40-1.50.0.33-1.39.4.55-94.59.4.07-58.70.pth, bkmy
BLEU = 11.04, 37.0/15.4/7.2/3.6 (BP=1.000, ratio=1.108, hyp_len=13558, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.439.0.40-1.49.0.33-1.39.4.51-90.51.4.08-59.09.pth, mybk
BLEU = 8.71, 32.3/11.6/5.4/2.9 (BP=1.000, ratio=1.134, hyp_len=12966, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.439.0.40-1.49.0.33-1.39.4.51-90.51.4.08-59.09.pth, bkmy
BLEU = 10.86, 37.5/15.2/7.0/3.5 (BP=1.000, ratio=1.091, hyp_len=13344, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.440.0.44-1.55.0.37-1.45.4.53-92.92.4.05-57.68.pth, mybk
BLEU = 8.85, 32.1/11.6/5.6/3.0 (BP=1.000, ratio=1.135, hyp_len=12972, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.440.0.44-1.55.0.37-1.45.4.53-92.92.4.05-57.68.pth, bkmy
BLEU = 11.30, 37.8/15.6/7.3/3.8 (BP=1.000, ratio=1.093, hyp_len=13365, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.441.0.40-1.49.0.33-1.39.4.53-92.59.4.05-57.37.pth, mybk
BLEU = 9.12, 32.9/12.1/5.8/3.0 (BP=1.000, ratio=1.120, hyp_len=12804, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.441.0.40-1.49.0.33-1.39.4.53-92.59.4.05-57.37.pth, bkmy
BLEU = 10.85, 37.3/15.1/6.9/3.6 (BP=1.000, ratio=1.096, hyp_len=13403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.442.0.38-1.47.0.30-1.35.4.51-91.00.4.05-57.32.pth, mybk
BLEU = 8.60, 32.4/11.5/5.3/2.8 (BP=1.000, ratio=1.134, hyp_len=12965, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.442.0.38-1.47.0.30-1.35.4.51-91.00.4.05-57.32.pth, bkmy
BLEU = 10.54, 36.7/14.8/6.8/3.3 (BP=1.000, ratio=1.111, hyp_len=13593, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.42-11.21.2.19-8.90.2.66-14.25.2.35-10.53.pth, mybk
BLEU = 8.39, 31.5/11.6/5.4/2.5 (BP=1.000, ratio=1.122, hyp_len=12824, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.42-11.21.2.19-8.90.2.66-14.25.2.35-10.53.pth, bkmy
BLEU = 9.69, 36.0/14.6/6.3/2.7 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.443.0.39-1.48.0.33-1.38.4.55-94.29.4.09-59.63.pth, mybk
BLEU = 8.54, 32.8/11.6/5.2/2.7 (BP=1.000, ratio=1.119, hyp_len=12789, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.443.0.39-1.48.0.33-1.38.4.55-94.29.4.09-59.63.pth, bkmy
BLEU = 10.59, 37.0/14.9/6.8/3.4 (BP=1.000, ratio=1.114, hyp_len=13620, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.444.0.40-1.49.0.32-1.38.4.50-90.20.4.06-58.19.pth, mybk
BLEU = 8.87, 32.6/11.8/5.5/2.9 (BP=1.000, ratio=1.114, hyp_len=12733, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.444.0.40-1.49.0.32-1.38.4.50-90.20.4.06-58.19.pth, bkmy
BLEU = 10.82, 36.6/14.7/7.1/3.6 (BP=1.000, ratio=1.112, hyp_len=13596, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.445.0.41-1.51.0.33-1.38.4.55-94.24.4.10-60.47.pth, mybk
BLEU = 9.02, 33.0/12.1/5.6/2.9 (BP=1.000, ratio=1.113, hyp_len=12729, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.445.0.41-1.51.0.33-1.38.4.55-94.24.4.10-60.47.pth, bkmy
BLEU = 10.89, 36.9/14.9/7.1/3.6 (BP=1.000, ratio=1.117, hyp_len=13661, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.446.0.41-1.51.0.34-1.40.4.57-96.74.4.10-60.29.pth, mybk
BLEU = 8.46, 32.1/11.4/5.3/2.7 (BP=1.000, ratio=1.121, hyp_len=12810, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.446.0.41-1.51.0.34-1.40.4.57-96.74.4.10-60.29.pth, bkmy
BLEU = 11.04, 37.2/15.4/7.2/3.6 (BP=1.000, ratio=1.105, hyp_len=13517, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.447.0.40-1.50.0.32-1.38.4.54-93.96.4.06-57.85.pth, mybk
BLEU = 8.70, 33.0/11.8/5.3/2.8 (BP=1.000, ratio=1.114, hyp_len=12733, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.447.0.40-1.50.0.32-1.38.4.54-93.96.4.06-57.85.pth, bkmy
BLEU = 10.91, 37.2/15.1/7.0/3.6 (BP=1.000, ratio=1.103, hyp_len=13493, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.448.0.41-1.50.0.35-1.42.4.61-100.70.4.07-58.63.pth, mybk
BLEU = 8.89, 32.9/12.2/5.5/2.8 (BP=1.000, ratio=1.119, hyp_len=12793, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.448.0.41-1.50.0.35-1.42.4.61-100.70.4.07-58.63.pth, bkmy
BLEU = 10.85, 37.0/15.2/7.0/3.5 (BP=1.000, ratio=1.118, hyp_len=13679, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.449.0.40-1.49.0.33-1.39.4.56-95.86.4.03-56.05.pth, mybk
BLEU = 9.10, 32.9/12.1/5.7/3.0 (BP=1.000, ratio=1.115, hyp_len=12744, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.449.0.40-1.49.0.33-1.39.4.56-95.86.4.03-56.05.pth, bkmy
BLEU = 10.97, 37.5/15.3/7.1/3.6 (BP=1.000, ratio=1.099, hyp_len=13441, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.450.0.40-1.49.0.33-1.39.4.59-98.72.4.06-57.76.pth, mybk
BLEU = 8.84, 32.1/11.6/5.5/3.0 (BP=1.000, ratio=1.135, hyp_len=12975, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.450.0.40-1.49.0.33-1.39.4.59-98.72.4.06-57.76.pth, bkmy
BLEU = 10.63, 37.1/15.0/6.8/3.4 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.451.0.40-1.50.0.34-1.40.4.64-103.62.4.08-59.04.pth, mybk
BLEU = 8.98, 32.6/11.9/5.6/3.0 (BP=1.000, ratio=1.122, hyp_len=12821, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.451.0.40-1.50.0.34-1.40.4.64-103.62.4.08-59.04.pth, bkmy
BLEU = 11.62, 38.5/16.2/7.7/3.8 (BP=1.000, ratio=1.077, hyp_len=13168, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.452.0.39-1.48.0.32-1.37.4.58-97.96.4.10-60.53.pth, mybk
BLEU = 9.02, 32.8/11.9/5.6/3.0 (BP=1.000, ratio=1.129, hyp_len=12912, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.452.0.39-1.48.0.32-1.37.4.58-97.96.4.10-60.53.pth, bkmy
BLEU = 10.43, 36.2/14.6/6.7/3.4 (BP=1.000, ratio=1.125, hyp_len=13763, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.37-10.72.2.16-8.66.2.67-14.45.2.34-10.41.pth, mybk
BLEU = 8.56, 31.8/11.9/5.5/2.6 (BP=1.000, ratio=1.104, hyp_len=12625, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.37-10.72.2.16-8.66.2.67-14.45.2.34-10.41.pth, bkmy
BLEU = 9.54, 36.4/14.6/6.1/2.6 (BP=1.000, ratio=1.087, hyp_len=13298, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.453.0.42-1.53.0.37-1.45.4.56-95.42.4.04-56.75.pth, mybk
BLEU = 8.51, 32.2/11.4/5.3/2.7 (BP=1.000, ratio=1.126, hyp_len=12868, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.453.0.42-1.53.0.37-1.45.4.56-95.42.4.04-56.75.pth, bkmy
BLEU = 10.55, 37.1/14.9/6.7/3.3 (BP=1.000, ratio=1.099, hyp_len=13440, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.454.0.39-1.48.0.32-1.38.4.56-95.68.4.13-62.24.pth, mybk
BLEU = 8.69, 32.1/11.5/5.3/2.9 (BP=1.000, ratio=1.124, hyp_len=12847, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.454.0.39-1.48.0.32-1.38.4.56-95.68.4.13-62.24.pth, bkmy
BLEU = 10.64, 36.5/14.8/6.8/3.5 (BP=1.000, ratio=1.118, hyp_len=13674, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.455.0.39-1.48.0.32-1.38.4.55-94.32.4.04-56.96.pth, mybk
BLEU = 9.25, 32.7/12.0/5.8/3.2 (BP=1.000, ratio=1.110, hyp_len=12687, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.455.0.39-1.48.0.32-1.38.4.55-94.32.4.04-56.96.pth, bkmy
BLEU = 11.04, 37.1/15.2/7.2/3.6 (BP=1.000, ratio=1.099, hyp_len=13446, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.456.0.45-1.56.0.36-1.44.4.57-96.73.4.05-57.55.pth, mybk
BLEU = 8.77, 32.4/11.7/5.5/2.9 (BP=1.000, ratio=1.122, hyp_len=12822, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.456.0.45-1.56.0.36-1.44.4.57-96.73.4.05-57.55.pth, bkmy
BLEU = 11.13, 37.8/15.7/7.2/3.6 (BP=1.000, ratio=1.093, hyp_len=13370, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.457.0.38-1.46.0.31-1.37.4.61-100.07.4.07-58.75.pth, mybk
BLEU = 8.42, 31.8/11.1/5.2/2.7 (BP=1.000, ratio=1.128, hyp_len=12893, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.457.0.38-1.46.0.31-1.37.4.61-100.07.4.07-58.75.pth, bkmy
BLEU = 10.97, 36.7/15.2/7.1/3.6 (BP=1.000, ratio=1.102, hyp_len=13481, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.458.0.38-1.47.0.32-1.38.4.59-98.42.4.06-57.98.pth, mybk
BLEU = 8.63, 32.3/11.6/5.3/2.8 (BP=1.000, ratio=1.133, hyp_len=12951, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.458.0.38-1.47.0.32-1.38.4.59-98.42.4.06-57.98.pth, bkmy
BLEU = 10.62, 36.7/14.8/6.8/3.4 (BP=1.000, ratio=1.100, hyp_len=13460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.459.0.39-1.48.0.32-1.38.4.56-95.32.4.14-62.85.pth, mybk
BLEU = 8.76, 32.8/12.0/5.5/2.7 (BP=1.000, ratio=1.120, hyp_len=12809, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.459.0.39-1.48.0.32-1.38.4.56-95.32.4.14-62.85.pth, bkmy
BLEU = 10.72, 36.3/14.8/6.9/3.6 (BP=1.000, ratio=1.119, hyp_len=13690, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.460.0.40-1.49.0.32-1.38.4.56-95.85.4.13-62.26.pth, mybk
BLEU = 8.14, 31.8/11.1/4.9/2.5 (BP=1.000, ratio=1.132, hyp_len=12943, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.460.0.40-1.49.0.32-1.38.4.56-95.85.4.13-62.26.pth, bkmy
BLEU = 11.05, 37.7/15.5/7.3/3.5 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.461.0.39-1.48.0.32-1.38.4.55-95.09.4.10-60.09.pth, mybk
BLEU = 8.47, 32.8/11.7/5.2/2.6 (BP=1.000, ratio=1.112, hyp_len=12710, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.461.0.39-1.48.0.32-1.38.4.55-95.09.4.10-60.09.pth, bkmy
BLEU = 10.66, 36.6/14.9/6.9/3.4 (BP=1.000, ratio=1.097, hyp_len=13422, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.462.0.40-1.48.0.33-1.39.4.59-98.83.4.14-63.00.pth, mybk
BLEU = 8.54, 31.8/11.3/5.3/2.8 (BP=1.000, ratio=1.128, hyp_len=12898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.462.0.40-1.48.0.33-1.39.4.59-98.83.4.14-63.00.pth, bkmy
BLEU = 10.74, 36.5/15.2/7.0/3.4 (BP=1.000, ratio=1.131, hyp_len=13834, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.38-10.77.2.18-8.82.2.70-14.82.2.35-10.46.pth, mybk
BLEU = 8.70, 32.5/12.2/5.6/2.6 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.38-10.77.2.18-8.82.2.70-14.82.2.35-10.46.pth, bkmy
BLEU = 9.45, 36.1/14.5/6.1/2.5 (BP=1.000, ratio=1.105, hyp_len=13514, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.463.0.40-1.49.0.34-1.40.4.62-101.70.4.08-59.40.pth, mybk
BLEU = 8.67, 32.5/11.7/5.4/2.8 (BP=1.000, ratio=1.140, hyp_len=13032, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.463.0.40-1.49.0.34-1.40.4.62-101.70.4.08-59.40.pth, bkmy
BLEU = 10.62, 37.0/15.1/6.9/3.3 (BP=1.000, ratio=1.105, hyp_len=13517, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.464.0.41-1.51.0.37-1.44.4.57-96.65.4.08-58.93.pth, mybk
BLEU = 8.71, 32.7/11.6/5.4/2.8 (BP=1.000, ratio=1.115, hyp_len=12741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.464.0.41-1.51.0.37-1.44.4.57-96.65.4.08-58.93.pth, bkmy
BLEU = 11.47, 37.0/15.6/7.6/4.0 (BP=1.000, ratio=1.099, hyp_len=13442, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.465.0.40-1.49.0.32-1.38.4.58-97.43.4.12-61.44.pth, mybk
BLEU = 8.70, 32.7/11.7/5.4/2.7 (BP=1.000, ratio=1.123, hyp_len=12836, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.465.0.40-1.49.0.32-1.38.4.58-97.43.4.12-61.44.pth, bkmy
BLEU = 11.09, 37.3/15.3/7.2/3.7 (BP=1.000, ratio=1.102, hyp_len=13479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.466.0.41-1.50.0.33-1.39.4.62-101.78.4.10-60.36.pth, mybk
BLEU = 8.35, 32.4/11.4/5.1/2.6 (BP=1.000, ratio=1.127, hyp_len=12889, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.466.0.41-1.50.0.33-1.39.4.62-101.78.4.10-60.36.pth, bkmy
BLEU = 10.77, 37.1/15.2/7.0/3.4 (BP=1.000, ratio=1.104, hyp_len=13501, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.467.0.39-1.48.0.31-1.37.4.62-101.55.4.15-63.37.pth, mybk
BLEU = 8.36, 32.0/11.4/5.2/2.6 (BP=1.000, ratio=1.118, hyp_len=12784, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.467.0.39-1.48.0.31-1.37.4.62-101.55.4.15-63.37.pth, bkmy
BLEU = 11.14, 37.2/15.6/7.4/3.6 (BP=1.000, ratio=1.106, hyp_len=13526, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.468.0.40-1.49.0.35-1.42.4.61-100.85.4.10-60.10.pth, mybk
BLEU = 8.50, 32.5/11.7/5.2/2.6 (BP=1.000, ratio=1.119, hyp_len=12793, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.468.0.40-1.49.0.35-1.42.4.61-100.85.4.10-60.10.pth, bkmy
BLEU = 11.29, 37.7/15.6/7.4/3.7 (BP=1.000, ratio=1.094, hyp_len=13375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.469.0.38-1.47.0.31-1.36.4.65-104.67.4.08-59.35.pth, mybk
BLEU = 8.57, 32.8/11.6/5.3/2.7 (BP=1.000, ratio=1.120, hyp_len=12807, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.469.0.38-1.47.0.31-1.36.4.65-104.67.4.08-59.35.pth, bkmy
BLEU = 10.92, 36.5/14.9/7.1/3.7 (BP=1.000, ratio=1.118, hyp_len=13677, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.470.0.39-1.48.0.33-1.39.4.64-103.06.4.13-62.43.pth, mybk
BLEU = 8.92, 33.1/11.8/5.5/2.9 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.470.0.39-1.48.0.33-1.39.4.64-103.06.4.13-62.43.pth, bkmy
BLEU = 10.95, 37.4/15.4/7.2/3.5 (BP=1.000, ratio=1.098, hyp_len=13429, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.471.0.39-1.47.0.32-1.38.4.56-95.87.4.14-62.61.pth, mybk
BLEU = 8.83, 31.9/11.6/5.5/3.0 (BP=1.000, ratio=1.139, hyp_len=13026, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.471.0.39-1.47.0.32-1.38.4.56-95.87.4.14-62.61.pth, bkmy
BLEU = 10.83, 36.8/15.2/7.0/3.5 (BP=1.000, ratio=1.098, hyp_len=13427, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.472.0.40-1.49.0.32-1.38.4.60-99.71.4.15-63.44.pth, mybk
BLEU = 8.25, 32.2/11.2/5.0/2.5 (BP=1.000, ratio=1.129, hyp_len=12906, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.472.0.40-1.49.0.32-1.38.4.60-99.71.4.15-63.44.pth, bkmy
BLEU = 10.93, 37.2/15.2/7.0/3.6 (BP=1.000, ratio=1.099, hyp_len=13439, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.35-10.52.2.10-8.18.2.66-14.28.2.33-10.28.pth, mybk
BLEU = 8.74, 32.0/12.1/5.7/2.6 (BP=1.000, ratio=1.112, hyp_len=12716, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.35-10.52.2.10-8.18.2.66-14.28.2.33-10.28.pth, bkmy
BLEU = 9.87, 37.1/15.1/6.4/2.6 (BP=1.000, ratio=1.074, hyp_len=13136, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.473.0.39-1.48.0.31-1.36.4.65-104.20.4.21-67.51.pth, mybk
BLEU = 8.69, 32.8/11.8/5.4/2.7 (BP=1.000, ratio=1.115, hyp_len=12741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.473.0.39-1.48.0.31-1.36.4.65-104.20.4.21-67.51.pth, bkmy
BLEU = 10.94, 36.6/15.4/7.1/3.6 (BP=1.000, ratio=1.109, hyp_len=13562, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.474.0.44-1.55.0.35-1.42.4.64-103.16.4.15-63.49.pth, mybk
BLEU = 8.36, 32.0/11.2/5.0/2.7 (BP=1.000, ratio=1.126, hyp_len=12871, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.474.0.44-1.55.0.35-1.42.4.64-103.16.4.15-63.49.pth, bkmy
BLEU = 10.73, 36.5/15.0/6.9/3.5 (BP=1.000, ratio=1.105, hyp_len=13510, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.475.0.40-1.49.0.33-1.39.4.63-102.59.4.13-62.35.pth, mybk
BLEU = 8.69, 32.9/11.8/5.3/2.8 (BP=1.000, ratio=1.120, hyp_len=12801, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.475.0.40-1.49.0.33-1.39.4.63-102.59.4.13-62.35.pth, bkmy
BLEU = 11.21, 37.3/15.4/7.3/3.8 (BP=1.000, ratio=1.113, hyp_len=13615, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.476.0.41-1.50.0.36-1.44.4.61-100.83.4.13-62.17.pth, mybk
BLEU = 8.59, 32.7/11.7/5.3/2.7 (BP=1.000, ratio=1.125, hyp_len=12860, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.476.0.41-1.50.0.36-1.44.4.61-100.83.4.13-62.17.pth, bkmy
BLEU = 10.68, 37.3/15.0/6.9/3.4 (BP=1.000, ratio=1.102, hyp_len=13483, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.477.0.39-1.47.0.31-1.36.4.62-101.77.4.19-66.27.pth, mybk
BLEU = 9.13, 32.9/12.2/5.7/3.0 (BP=1.000, ratio=1.119, hyp_len=12798, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.477.0.39-1.47.0.31-1.36.4.62-101.77.4.19-66.27.pth, bkmy
BLEU = 11.02, 37.4/15.4/7.2/3.6 (BP=1.000, ratio=1.102, hyp_len=13474, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.478.0.39-1.48.0.32-1.38.4.65-104.39.4.16-64.08.pth, mybk
BLEU = 8.92, 32.7/12.0/5.5/2.9 (BP=1.000, ratio=1.119, hyp_len=12788, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.478.0.39-1.48.0.32-1.38.4.65-104.39.4.16-64.08.pth, bkmy
BLEU = 10.60, 36.1/14.7/6.8/3.5 (BP=1.000, ratio=1.141, hyp_len=13956, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.479.0.38-1.46.0.32-1.38.4.67-107.19.4.10-60.07.pth, mybk
BLEU = 9.17, 33.0/12.1/5.7/3.1 (BP=1.000, ratio=1.111, hyp_len=12706, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.479.0.38-1.46.0.32-1.38.4.67-107.19.4.10-60.07.pth, bkmy
BLEU = 11.40, 37.6/15.8/7.4/3.8 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.480.0.38-1.46.0.32-1.38.4.64-104.03.4.13-62.13.pth, mybk
BLEU = 8.82, 32.7/11.8/5.5/2.9 (BP=1.000, ratio=1.134, hyp_len=12965, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.480.0.38-1.46.0.32-1.38.4.64-104.03.4.13-62.13.pth, bkmy
BLEU = 11.10, 37.1/15.2/7.2/3.8 (BP=1.000, ratio=1.093, hyp_len=13374, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.481.0.40-1.49.0.35-1.41.4.59-98.87.4.17-64.92.pth, mybk
BLEU = 8.64, 33.2/12.0/5.3/2.7 (BP=1.000, ratio=1.108, hyp_len=12671, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.481.0.40-1.49.0.35-1.41.4.59-98.87.4.17-64.92.pth, bkmy
BLEU = 10.84, 36.8/15.0/7.0/3.6 (BP=1.000, ratio=1.104, hyp_len=13502, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.482.0.40-1.49.0.32-1.38.4.65-104.11.4.11-60.79.pth, mybk
BLEU = 8.38, 32.4/11.3/5.1/2.6 (BP=1.000, ratio=1.127, hyp_len=12880, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.482.0.40-1.49.0.32-1.38.4.65-104.11.4.11-60.79.pth, bkmy
BLEU = 11.05, 37.0/15.3/7.2/3.7 (BP=1.000, ratio=1.105, hyp_len=13520, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.40-11.05.2.11-8.25.2.68-14.59.2.35-10.46.pth, mybk
BLEU = 8.58, 32.1/12.2/5.5/2.5 (BP=1.000, ratio=1.115, hyp_len=12751, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.40-11.05.2.11-8.25.2.68-14.59.2.35-10.46.pth, bkmy
BLEU = 10.17, 37.3/15.3/6.5/2.9 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.483.0.38-1.46.0.32-1.38.4.59-98.62.4.18-65.64.pth, mybk
BLEU = 8.73, 32.7/11.9/5.4/2.8 (BP=1.000, ratio=1.115, hyp_len=12741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.483.0.38-1.46.0.32-1.38.4.59-98.62.4.18-65.64.pth, bkmy
BLEU = 10.53, 36.3/14.6/6.9/3.4 (BP=1.000, ratio=1.117, hyp_len=13657, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.484.0.38-1.46.0.33-1.39.4.65-104.18.4.13-62.47.pth, mybk
BLEU = 8.69, 31.6/11.7/5.4/2.8 (BP=1.000, ratio=1.124, hyp_len=12846, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.484.0.38-1.46.0.33-1.39.4.65-104.18.4.13-62.47.pth, bkmy
BLEU = 10.83, 36.9/14.9/7.0/3.6 (BP=1.000, ratio=1.108, hyp_len=13557, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.485.0.36-1.44.0.31-1.37.4.62-101.94.4.18-65.06.pth, mybk
BLEU = 8.53, 32.7/11.5/5.2/2.7 (BP=1.000, ratio=1.128, hyp_len=12897, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.485.0.36-1.44.0.31-1.37.4.62-101.94.4.18-65.06.pth, bkmy
BLEU = 10.53, 36.6/14.9/6.8/3.3 (BP=1.000, ratio=1.118, hyp_len=13678, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.486.0.42-1.52.0.35-1.42.4.66-105.90.4.13-62.21.pth, mybk
BLEU = 8.76, 32.6/11.8/5.5/2.8 (BP=1.000, ratio=1.122, hyp_len=12824, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.486.0.42-1.52.0.35-1.42.4.66-105.90.4.13-62.21.pth, bkmy
BLEU = 11.10, 37.8/15.6/7.3/3.5 (BP=1.000, ratio=1.087, hyp_len=13293, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.487.0.36-1.43.0.31-1.37.4.64-103.66.4.14-62.96.pth, mybk
BLEU = 8.77, 32.8/11.8/5.5/2.8 (BP=1.000, ratio=1.121, hyp_len=12813, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.487.0.36-1.43.0.31-1.37.4.64-103.66.4.14-62.96.pth, bkmy
BLEU = 10.64, 36.3/14.9/7.0/3.4 (BP=1.000, ratio=1.121, hyp_len=13714, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.488.0.39-1.48.0.33-1.38.4.60-99.64.4.17-64.75.pth, mybk
BLEU = 8.57, 32.3/11.5/5.3/2.8 (BP=1.000, ratio=1.138, hyp_len=13014, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.488.0.39-1.48.0.33-1.38.4.60-99.64.4.17-64.75.pth, bkmy
BLEU = 10.97, 36.9/15.0/7.1/3.7 (BP=1.000, ratio=1.112, hyp_len=13601, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.489.0.37-1.45.0.30-1.35.4.68-107.69.4.22-67.85.pth, mybk
BLEU = 8.35, 32.5/11.3/5.1/2.6 (BP=1.000, ratio=1.130, hyp_len=12915, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.489.0.37-1.45.0.30-1.35.4.68-107.69.4.22-67.85.pth, bkmy
BLEU = 11.16, 37.4/15.5/7.3/3.7 (BP=1.000, ratio=1.091, hyp_len=13339, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.490.0.37-1.44.0.30-1.35.4.63-102.35.4.21-67.19.pth, mybk
BLEU = 8.21, 32.1/11.1/5.0/2.6 (BP=1.000, ratio=1.126, hyp_len=12869, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.490.0.37-1.44.0.30-1.35.4.63-102.35.4.21-67.19.pth, bkmy
BLEU = 10.92, 37.5/15.5/7.1/3.5 (BP=1.000, ratio=1.100, hyp_len=13457, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.491.0.38-1.47.0.32-1.38.4.66-105.33.4.19-66.34.pth, mybk
BLEU = 8.63, 32.2/11.6/5.3/2.8 (BP=1.000, ratio=1.133, hyp_len=12956, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.491.0.38-1.47.0.32-1.38.4.66-105.33.4.19-66.34.pth, bkmy
BLEU = 11.06, 37.5/15.6/7.1/3.6 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.492.0.40-1.49.0.33-1.39.4.64-103.26.4.21-67.18.pth, mybk
BLEU = 9.01, 32.9/12.1/5.7/2.9 (BP=1.000, ratio=1.102, hyp_len=12593, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.492.0.40-1.49.0.33-1.39.4.64-103.26.4.21-67.18.pth, bkmy
BLEU = 10.46, 36.8/14.6/6.7/3.3 (BP=1.000, ratio=1.093, hyp_len=13364, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.31-10.03.2.09-8.09.2.66-14.36.2.31-10.10.pth, mybk
BLEU = 9.27, 33.3/12.9/6.0/2.9 (BP=1.000, ratio=1.094, hyp_len=12510, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.31-10.03.2.09-8.09.2.66-14.36.2.31-10.10.pth, bkmy
BLEU = 9.96, 37.0/15.3/6.4/2.7 (BP=1.000, ratio=1.069, hyp_len=13077, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.493.0.38-1.46.0.30-1.35.4.65-104.39.4.16-64.26.pth, mybk
BLEU = 8.75, 32.5/11.8/5.4/2.8 (BP=1.000, ratio=1.115, hyp_len=12752, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.493.0.38-1.46.0.30-1.35.4.65-104.39.4.16-64.26.pth, bkmy
BLEU = 10.77, 37.1/14.9/6.9/3.5 (BP=1.000, ratio=1.107, hyp_len=13540, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.494.0.47-1.60.0.33-1.39.4.73-112.77.4.16-64.32.pth, mybk
BLEU = 8.32, 32.1/11.4/5.0/2.6 (BP=1.000, ratio=1.107, hyp_len=12656, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.494.0.47-1.60.0.33-1.39.4.73-112.77.4.16-64.32.pth, bkmy
BLEU = 10.48, 36.8/14.8/6.7/3.3 (BP=1.000, ratio=1.091, hyp_len=13340, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.495.0.39-1.48.0.33-1.39.4.67-106.37.4.14-62.64.pth, mybk
BLEU = 8.71, 32.4/11.6/5.3/2.9 (BP=1.000, ratio=1.111, hyp_len=12700, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.495.0.39-1.48.0.33-1.39.4.67-106.37.4.14-62.64.pth, bkmy
BLEU = 10.76, 37.0/15.2/6.9/3.4 (BP=1.000, ratio=1.117, hyp_len=13662, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.496.0.38-1.46.0.30-1.35.4.67-106.61.4.19-66.16.pth, mybk
BLEU = 8.72, 32.2/11.4/5.5/2.9 (BP=1.000, ratio=1.130, hyp_len=12922, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.496.0.38-1.46.0.30-1.35.4.67-106.61.4.19-66.16.pth, bkmy
BLEU = 11.20, 37.6/15.5/7.3/3.7 (BP=1.000, ratio=1.106, hyp_len=13524, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.497.0.37-1.45.0.30-1.35.4.61-100.09.4.15-63.59.pth, mybk
BLEU = 8.90, 32.7/11.7/5.5/3.0 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.497.0.37-1.45.0.30-1.35.4.61-100.09.4.15-63.59.pth, bkmy
BLEU = 11.06, 37.2/15.4/7.2/3.6 (BP=1.000, ratio=1.108, hyp_len=13558, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.498.0.40-1.49.0.35-1.41.4.69-109.32.4.16-64.13.pth, mybk
BLEU = 8.69, 32.3/11.6/5.3/2.8 (BP=1.000, ratio=1.119, hyp_len=12793, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.498.0.40-1.49.0.35-1.41.4.69-109.32.4.16-64.13.pth, bkmy
BLEU = 10.81, 37.4/15.1/6.9/3.5 (BP=1.000, ratio=1.095, hyp_len=13392, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.499.0.40-1.49.0.33-1.39.4.65-104.61.4.16-64.20.pth, mybk
BLEU = 8.79, 32.8/11.8/5.5/2.8 (BP=1.000, ratio=1.120, hyp_len=12802, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.499.0.40-1.49.0.33-1.39.4.65-104.61.4.16-64.20.pth, bkmy
BLEU = 10.68, 36.7/15.0/6.9/3.4 (BP=1.000, ratio=1.111, hyp_len=13589, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.500.0.39-1.48.0.34-1.41.4.65-104.81.4.16-64.24.pth, mybk
BLEU = 9.46, 33.2/12.3/6.0/3.3 (BP=1.000, ratio=1.112, hyp_len=12713, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.500.0.39-1.48.0.34-1.41.4.65-104.81.4.16-64.24.pth, bkmy
BLEU = 11.44, 37.8/15.8/7.5/3.8 (BP=1.000, ratio=1.097, hyp_len=13420, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.25-9.47.2.04-7.67.2.66-14.35.2.36-10.55.pth, mybk
BLEU = 8.98, 31.7/12.2/5.9/2.8 (BP=1.000, ratio=1.122, hyp_len=12832, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.25-9.47.2.04-7.67.2.66-14.35.2.36-10.55.pth, bkmy
BLEU = 9.77, 37.2/15.0/6.4/2.6 (BP=1.000, ratio=1.085, hyp_len=13270, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.23-9.26.2.02-7.52.2.65-14.20.2.34-10.38.pth, mybk
BLEU = 8.91, 32.2/12.2/5.7/2.8 (BP=1.000, ratio=1.127, hyp_len=12880, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.23-9.26.2.02-7.52.2.65-14.20.2.34-10.38.pth, bkmy
BLEU = 10.49, 37.3/15.7/6.8/3.0 (BP=1.000, ratio=1.066, hyp_len=13042, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.20-9.05.1.99-7.29.2.65-14.16.2.32-10.15.pth, mybk
BLEU = 9.24, 33.2/13.1/6.0/2.8 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.20-9.05.1.99-7.29.2.65-14.16.2.32-10.15.pth, bkmy
BLEU = 9.47, 36.4/14.4/6.0/2.6 (BP=1.000, ratio=1.093, hyp_len=13368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.20-9.01.1.99-7.33.2.66-14.32.2.31-10.12.pth, mybk
BLEU = 9.13, 32.9/12.6/5.9/2.8 (BP=1.000, ratio=1.115, hyp_len=12750, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.20-9.01.1.99-7.33.2.66-14.32.2.31-10.12.pth, bkmy
BLEU = 9.81, 37.6/15.4/6.4/2.5 (BP=1.000, ratio=1.063, hyp_len=12999, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.18-8.82.1.95-7.03.2.64-13.99.2.32-10.18.pth, mybk
BLEU = 9.19, 33.3/12.8/6.0/2.8 (BP=1.000, ratio=1.086, hyp_len=12415, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.18-8.82.1.95-7.03.2.64-13.99.2.32-10.18.pth, bkmy
BLEU = 10.05, 37.4/15.3/6.5/2.7 (BP=1.000, ratio=1.087, hyp_len=13291, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.17-8.75.1.93-6.86.2.70-14.94.2.31-10.06.pth, mybk
BLEU = 9.31, 32.3/12.8/6.1/3.0 (BP=1.000, ratio=1.132, hyp_len=12945, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.17-8.75.1.93-6.86.2.70-14.94.2.31-10.06.pth, bkmy
BLEU = 10.39, 37.5/15.5/6.7/3.0 (BP=1.000, ratio=1.089, hyp_len=13319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.21-9.12.1.99-7.29.2.65-14.20.2.32-10.19.pth, mybk
BLEU = 9.28, 33.0/12.8/6.0/2.9 (BP=1.000, ratio=1.110, hyp_len=12688, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.21-9.12.1.99-7.29.2.65-14.20.2.32-10.19.pth, bkmy
BLEU = 10.37, 37.7/15.4/6.8/3.0 (BP=1.000, ratio=1.081, hyp_len=13224, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.10-8.14.1.89-6.61.2.68-14.54.2.35-10.51.pth, mybk
BLEU = 9.75, 34.0/13.3/6.5/3.1 (BP=1.000, ratio=1.097, hyp_len=12536, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.10-8.14.1.89-6.61.2.68-14.54.2.35-10.51.pth, bkmy
BLEU = 9.58, 36.4/14.5/6.1/2.6 (BP=1.000, ratio=1.120, hyp_len=13700, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.04-7.73.1.86-6.44.2.65-14.21.2.32-10.22.pth, mybk
BLEU = 9.91, 34.5/13.5/6.4/3.2 (BP=1.000, ratio=1.081, hyp_len=12359, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.04-7.73.1.86-6.44.2.65-14.21.2.32-10.22.pth, bkmy
BLEU = 10.30, 37.9/15.6/6.7/2.8 (BP=1.000, ratio=1.086, hyp_len=13278, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.20-9.01.2.01-7.49.2.68-14.52.2.32-10.18.pth, mybk
BLEU = 9.50, 34.2/13.2/6.1/3.0 (BP=1.000, ratio=1.103, hyp_len=12613, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.20-9.01.2.01-7.49.2.68-14.52.2.32-10.18.pth, bkmy
BLEU = 10.90, 38.6/16.0/7.1/3.2 (BP=1.000, ratio=1.064, hyp_len=13013, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.2.06-7.88.1.84-6.33.2.68-14.55.2.33-10.28.pth, mybk
BLEU = 9.70, 34.0/13.1/6.3/3.2 (BP=1.000, ratio=1.106, hyp_len=12642, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.2.06-7.88.1.84-6.33.2.68-14.55.2.33-10.28.pth, bkmy
BLEU = 10.91, 38.1/15.9/7.1/3.3 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.2.03-7.60.1.83-6.26.2.69-14.70.2.35-10.50.pth, mybk
BLEU = 9.55, 33.7/13.0/6.2/3.1 (BP=1.000, ratio=1.125, hyp_len=12858, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.2.03-7.60.1.83-6.26.2.69-14.70.2.35-10.50.pth, bkmy
BLEU = 11.16, 38.6/16.3/7.4/3.3 (BP=1.000, ratio=1.062, hyp_len=12992, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.2.03-7.65.1.81-6.10.2.71-14.96.2.32-10.19.pth, mybk
BLEU = 9.57, 33.2/12.9/6.2/3.2 (BP=1.000, ratio=1.115, hyp_len=12749, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.2.03-7.65.1.81-6.10.2.71-14.96.2.32-10.19.pth, bkmy
BLEU = 11.30, 39.0/16.5/7.5/3.4 (BP=1.000, ratio=1.067, hyp_len=13045, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.2.02-7.51.1.78-5.93.2.69-14.66.2.33-10.32.pth, mybk
BLEU = 9.67, 33.9/13.3/6.2/3.1 (BP=1.000, ratio=1.111, hyp_len=12706, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.2.02-7.51.1.78-5.93.2.69-14.66.2.33-10.32.pth, bkmy
BLEU = 10.80, 38.7/16.3/7.1/3.0 (BP=1.000, ratio=1.051, hyp_len=12852, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.1.98-7.27.1.76-5.80.2.71-15.04.2.34-10.39.pth, mybk
BLEU = 9.43, 33.1/13.1/6.1/3.0 (BP=1.000, ratio=1.134, hyp_len=12963, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.1.98-7.27.1.76-5.80.2.71-15.04.2.34-10.39.pth, bkmy
BLEU = 10.97, 38.5/16.3/7.2/3.2 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.1.99-7.33.1.77-5.88.2.65-14.14.2.34-10.43.pth, mybk
BLEU = 9.75, 34.0/13.5/6.4/3.1 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.1.99-7.33.1.77-5.88.2.65-14.14.2.34-10.43.pth, bkmy
BLEU = 11.32, 38.8/16.4/7.5/3.4 (BP=1.000, ratio=1.062, hyp_len=12986, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.1.94-6.95.1.71-5.50.2.69-14.72.2.35-10.51.pth, mybk
BLEU = 9.36, 34.5/13.3/6.0/2.8 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.1.94-6.95.1.71-5.50.2.69-14.72.2.35-10.51.pth, bkmy
BLEU = 11.52, 39.0/16.8/7.6/3.5 (BP=1.000, ratio=1.067, hyp_len=13055, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.1.93-6.88.1.71-5.55.2.70-14.93.2.36-10.61.pth, mybk
BLEU = 9.82, 34.6/13.4/6.5/3.1 (BP=1.000, ratio=1.084, hyp_len=12392, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.1.93-6.88.1.71-5.55.2.70-14.93.2.36-10.61.pth, bkmy
BLEU = 11.19, 38.5/16.5/7.4/3.3 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.1.89-6.62.1.68-5.38.2.69-14.77.2.36-10.63.pth, mybk
BLEU = 9.81, 34.4/13.6/6.4/3.1 (BP=1.000, ratio=1.107, hyp_len=12657, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.1.89-6.62.1.68-5.38.2.69-14.77.2.36-10.63.pth, bkmy
BLEU = 11.50, 38.7/16.5/7.8/3.5 (BP=1.000, ratio=1.062, hyp_len=12990, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.1.85-6.38.1.64-5.18.2.67-14.42.2.35-10.50.pth, mybk
BLEU = 10.06, 35.5/13.8/6.6/3.2 (BP=1.000, ratio=1.070, hyp_len=12229, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.1.85-6.38.1.64-5.18.2.67-14.42.2.35-10.50.pth, bkmy
BLEU = 11.92, 39.1/16.9/7.9/3.9 (BP=1.000, ratio=1.075, hyp_len=13147, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.1.91-6.74.1.70-5.49.2.69-14.74.2.38-10.86.pth, mybk
BLEU = 9.48, 33.5/13.0/6.2/3.0 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.1.91-6.74.1.70-5.49.2.69-14.74.2.38-10.86.pth, bkmy
BLEU = 11.07, 38.1/16.0/7.3/3.4 (BP=1.000, ratio=1.089, hyp_len=13320, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.1.87-6.48.1.65-5.23.2.71-14.99.2.36-10.61.pth, mybk
BLEU = 9.73, 34.7/13.4/6.3/3.1 (BP=1.000, ratio=1.083, hyp_len=12382, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.1.87-6.48.1.65-5.23.2.71-14.99.2.36-10.61.pth, bkmy
BLEU = 11.17, 38.6/16.1/7.2/3.5 (BP=1.000, ratio=1.082, hyp_len=13240, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.1.88-6.54.1.67-5.34.2.74-15.43.2.39-10.93.pth, mybk
BLEU = 9.98, 34.4/13.4/6.5/3.3 (BP=1.000, ratio=1.100, hyp_len=12580, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.1.88-6.54.1.67-5.34.2.74-15.43.2.39-10.93.pth, bkmy
BLEU = 11.19, 38.3/16.1/7.4/3.5 (BP=1.000, ratio=1.098, hyp_len=13428, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.1.83-6.25.1.63-5.08.2.75-15.58.2.38-10.80.pth, mybk
BLEU = 9.19, 33.4/12.7/6.0/2.8 (BP=1.000, ratio=1.118, hyp_len=12784, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.1.83-6.25.1.63-5.08.2.75-15.58.2.38-10.80.pth, bkmy
BLEU = 11.47, 38.6/16.4/7.5/3.6 (BP=1.000, ratio=1.079, hyp_len=13201, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.1.83-6.21.1.64-5.18.2.74-15.54.2.39-10.90.pth, mybk
BLEU = 9.38, 34.2/13.1/6.0/2.9 (BP=1.000, ratio=1.098, hyp_len=12549, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.1.83-6.21.1.64-5.18.2.74-15.54.2.39-10.90.pth, bkmy
BLEU = 11.60, 38.9/16.4/7.6/3.7 (BP=1.000, ratio=1.090, hyp_len=13336, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.1.79-6.01.1.59-4.89.2.73-15.35.2.37-10.67.pth, mybk
BLEU = 9.58, 33.5/12.7/6.2/3.2 (BP=1.000, ratio=1.117, hyp_len=12769, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.1.79-6.01.1.59-4.89.2.73-15.35.2.37-10.67.pth, bkmy
BLEU = 11.17, 38.6/16.0/7.3/3.4 (BP=1.000, ratio=1.075, hyp_len=13152, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.1.74-5.69.1.53-4.61.2.75-15.59.2.39-10.95.pth, mybk
BLEU = 9.86, 34.2/13.3/6.4/3.3 (BP=1.000, ratio=1.104, hyp_len=12625, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.1.74-5.69.1.53-4.61.2.75-15.59.2.39-10.95.pth, bkmy
BLEU = 11.05, 37.9/15.9/7.3/3.4 (BP=1.000, ratio=1.085, hyp_len=13273, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.1.73-5.65.1.53-4.63.2.77-15.96.2.39-10.96.pth, mybk
BLEU = 10.35, 35.1/13.8/6.8/3.5 (BP=1.000, ratio=1.072, hyp_len=12257, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.1.73-5.65.1.53-4.63.2.77-15.96.2.39-10.96.pth, bkmy
BLEU = 11.72, 39.1/16.8/7.9/3.7 (BP=1.000, ratio=1.063, hyp_len=13004, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.1.83-6.26.1.66-5.27.2.79-16.28.2.38-10.76.pth, mybk
BLEU = 9.40, 33.8/13.2/6.1/2.9 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.1.83-6.26.1.66-5.27.2.79-16.28.2.38-10.76.pth, bkmy
BLEU = 11.82, 39.1/16.8/7.9/3.8 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.1.71-5.54.1.51-4.53.2.81-16.69.2.40-11.04.pth, mybk
BLEU = 10.06, 34.7/13.5/6.6/3.3 (BP=1.000, ratio=1.100, hyp_len=12570, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.1.71-5.54.1.51-4.53.2.81-16.69.2.40-11.04.pth, bkmy
BLEU = 12.01, 39.2/16.9/8.0/3.9 (BP=1.000, ratio=1.071, hyp_len=13099, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.1.68-5.34.1.50-4.47.2.76-15.84.2.42-11.19.pth, mybk
BLEU = 9.59, 34.1/13.2/6.2/3.0 (BP=1.000, ratio=1.096, hyp_len=12535, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.1.68-5.34.1.50-4.47.2.76-15.84.2.42-11.19.pth, bkmy
BLEU = 11.35, 38.8/16.4/7.4/3.5 (BP=1.000, ratio=1.095, hyp_len=13392, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.1.68-5.36.1.48-4.41.2.79-16.22.2.41-11.13.pth, mybk
BLEU = 9.72, 34.8/13.3/6.3/3.1 (BP=1.000, ratio=1.099, hyp_len=12567, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.1.68-5.36.1.48-4.41.2.79-16.22.2.41-11.13.pth, bkmy
BLEU = 11.74, 39.4/16.8/7.7/3.7 (BP=1.000, ratio=1.065, hyp_len=13026, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.1.67-5.32.1.47-4.35.2.77-16.01.2.42-11.21.pth, mybk
BLEU = 9.36, 34.2/13.2/6.0/2.8 (BP=1.000, ratio=1.099, hyp_len=12563, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.1.67-5.32.1.47-4.35.2.77-16.01.2.42-11.21.pth, bkmy
BLEU = 11.58, 38.7/16.7/7.7/3.6 (BP=1.000, ratio=1.087, hyp_len=13290, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.1.66-5.24.1.44-4.23.2.82-16.79.2.41-11.17.pth, mybk
BLEU = 9.94, 34.9/13.6/6.6/3.1 (BP=1.000, ratio=1.095, hyp_len=12523, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.1.66-5.24.1.44-4.23.2.82-16.79.2.41-11.17.pth, bkmy
BLEU = 11.31, 39.0/16.5/7.4/3.4 (BP=1.000, ratio=1.071, hyp_len=13100, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.1.65-5.22.1.46-4.30.2.82-16.70.2.44-11.53.pth, mybk
BLEU = 9.93, 34.5/13.6/6.5/3.2 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.1.65-5.22.1.46-4.30.2.82-16.70.2.44-11.53.pth, bkmy
BLEU = 11.54, 38.7/16.6/7.8/3.5 (BP=1.000, ratio=1.074, hyp_len=13134, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.1.62-5.07.1.45-4.28.2.81-16.56.2.42-11.23.pth, mybk
BLEU = 9.73, 34.8/13.4/6.4/3.0 (BP=1.000, ratio=1.107, hyp_len=12658, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.1.62-5.07.1.45-4.28.2.81-16.56.2.42-11.23.pth, bkmy
BLEU = 11.57, 39.3/16.5/7.7/3.6 (BP=1.000, ratio=1.059, hyp_len=12955, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.1.63-5.09.1.43-4.19.2.79-16.26.2.45-11.54.pth, mybk
BLEU = 10.35, 35.1/14.2/6.9/3.4 (BP=1.000, ratio=1.098, hyp_len=12554, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.1.63-5.09.1.43-4.19.2.79-16.26.2.45-11.54.pth, bkmy
BLEU = 11.93, 39.5/16.9/8.0/3.8 (BP=1.000, ratio=1.065, hyp_len=13020, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.1.61-5.03.1.41-4.08.2.80-16.42.2.43-11.33.pth, mybk
BLEU = 9.73, 33.8/13.2/6.4/3.1 (BP=1.000, ratio=1.114, hyp_len=12734, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.1.61-5.03.1.41-4.08.2.80-16.42.2.43-11.33.pth, bkmy
BLEU = 11.35, 39.1/16.5/7.5/3.4 (BP=1.000, ratio=1.069, hyp_len=13073, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.1.60-4.94.1.39-4.02.2.83-16.95.2.44-11.52.pth, mybk
BLEU = 10.18, 34.4/13.8/6.7/3.4 (BP=1.000, ratio=1.123, hyp_len=12839, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.1.60-4.94.1.39-4.02.2.83-16.95.2.44-11.52.pth, bkmy
BLEU = 11.47, 39.0/16.4/7.5/3.6 (BP=1.000, ratio=1.073, hyp_len=13122, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.1.58-4.87.1.39-4.03.2.81-16.64.2.47-11.85.pth, mybk
BLEU = 10.04, 34.9/13.6/6.5/3.3 (BP=1.000, ratio=1.091, hyp_len=12475, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.1.58-4.87.1.39-4.03.2.81-16.64.2.47-11.85.pth, bkmy
BLEU = 11.39, 39.4/16.5/7.4/3.5 (BP=1.000, ratio=1.070, hyp_len=13085, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.1.59-4.89.1.38-3.99.2.80-16.42.2.49-12.03.pth, mybk
BLEU = 10.29, 35.1/13.8/6.7/3.5 (BP=1.000, ratio=1.103, hyp_len=12613, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.1.59-4.89.1.38-3.99.2.80-16.42.2.49-12.03.pth, bkmy
BLEU = 11.86, 39.6/16.8/7.8/3.8 (BP=1.000, ratio=1.062, hyp_len=12992, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.91.1.52-4.57.1.35-3.84.2.83-16.93.2.50-12.19.pth, mybk
BLEU = 10.08, 34.6/13.6/6.6/3.3 (BP=1.000, ratio=1.098, hyp_len=12554, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.91.1.52-4.57.1.35-3.84.2.83-16.93.2.50-12.19.pth, bkmy
BLEU = 11.06, 38.3/15.6/7.1/3.6 (BP=1.000, ratio=1.085, hyp_len=13274, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.92.1.53-4.63.1.33-3.79.2.82-16.80.2.49-12.12.pth, mybk
BLEU = 10.02, 34.6/13.5/6.5/3.3 (BP=1.000, ratio=1.093, hyp_len=12491, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.92.1.53-4.63.1.33-3.79.2.82-16.80.2.49-12.12.pth, bkmy
BLEU = 11.48, 39.5/16.4/7.5/3.5 (BP=1.000, ratio=1.066, hyp_len=13044, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.93.1.51-4.51.1.31-3.72.2.85-17.28.2.50-12.19.pth, mybk
BLEU = 9.38, 33.5/13.0/6.0/3.0 (BP=1.000, ratio=1.128, hyp_len=12893, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.93.1.51-4.51.1.31-3.72.2.85-17.28.2.50-12.19.pth, bkmy
BLEU = 11.78, 39.1/16.7/7.8/3.8 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.94.1.57-4.81.1.31-3.72.2.85-17.32.2.49-12.10.pth, mybk
BLEU = 10.32, 34.9/14.0/6.8/3.4 (BP=1.000, ratio=1.104, hyp_len=12626, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.94.1.57-4.81.1.31-3.72.2.85-17.32.2.49-12.10.pth, bkmy
BLEU = 11.69, 38.9/16.6/7.7/3.7 (BP=1.000, ratio=1.078, hyp_len=13182, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.95.1.50-4.48.1.29-3.62.2.86-17.52.2.47-11.86.pth, mybk
BLEU = 10.08, 34.8/13.5/6.6/3.3 (BP=1.000, ratio=1.095, hyp_len=12522, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.95.1.50-4.48.1.29-3.62.2.86-17.52.2.47-11.86.pth, bkmy
BLEU = 11.31, 39.3/16.1/7.4/3.5 (BP=1.000, ratio=1.058, hyp_len=12946, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.96.1.55-4.71.1.39-4.01.2.86-17.46.2.47-11.87.pth, mybk
BLEU = 9.80, 34.5/13.2/6.3/3.2 (BP=1.000, ratio=1.106, hyp_len=12646, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.96.1.55-4.71.1.39-4.01.2.86-17.46.2.47-11.87.pth, bkmy
BLEU = 11.51, 39.2/16.6/7.5/3.6 (BP=1.000, ratio=1.072, hyp_len=13114, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.97.1.47-4.34.1.28-3.59.2.88-17.88.2.52-12.48.pth, mybk
BLEU = 10.47, 34.9/13.7/6.8/3.7 (BP=1.000, ratio=1.102, hyp_len=12599, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.97.1.47-4.34.1.28-3.59.2.88-17.88.2.52-12.48.pth, bkmy
BLEU = 11.79, 39.1/16.7/7.8/3.8 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.98.1.48-4.40.1.33-3.77.2.88-17.88.2.50-12.15.pth, mybk
BLEU = 9.97, 34.8/13.6/6.5/3.2 (BP=1.000, ratio=1.093, hyp_len=12493, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.98.1.48-4.40.1.33-3.77.2.88-17.88.2.50-12.15.pth, bkmy
BLEU = 11.41, 38.7/16.2/7.4/3.6 (BP=1.000, ratio=1.083, hyp_len=13243, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.99.1.45-4.27.1.26-3.54.2.89-17.91.2.54-12.64.pth, mybk
BLEU = 9.84, 34.5/13.2/6.3/3.3 (BP=1.000, ratio=1.106, hyp_len=12647, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.99.1.45-4.27.1.26-3.54.2.89-17.91.2.54-12.64.pth, bkmy
BLEU = 11.63, 39.3/16.7/7.6/3.7 (BP=1.000, ratio=1.073, hyp_len=13126, ref_len=12231)
==========

real	203m16.533s
user	186m23.691s
sys	21m3.800s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-bk အတွက် Best model က 134 epoch model ဖြစ်ပြီးတော့ Best Score က 10.55 BLEU ပါ။  
bk-my အတွက် Best model က 125 epoch model ဖြစ်ပြီးတော့ Best Score က 12.49 BLEU ပါ။   

## Transformer-DSL Training for 500 Epochs (my-bk, bk-my)  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python dual_train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
>    --lang mybk \
>    --gpu_id 0 --batch_size 64 --n_epochs 500 --max_length 100 --dropout .2 \
>    --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
>    --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
>    --lm_fn ./model/lm/mybk/lm-200epoch-mybk.pth \
>    --use_transformer --init_epoch 1\
>    --model_fn ./model/dsl/transformer/mybk-500epoch/dsl-model-mybk.pth | tee ./model/dsl/transformer/mybk-500epoch/training.log;
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
    'model_fn': './model/dsl/transformer/mybk-500epoch/dsl-model-mybk.pth',
    'n_epochs': 500,
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
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 1 - |param|=8.53e+02 |g_param|=2.39e+05 loss_x2y=4.4452e+00 ppl_x2y=85.22 loss_y2x=4.0983e+00 ppl_y2x=60.24 dual_loss=0.0000e+00
Epoch [2/500]:   1%|▌                                                                           | 1/123 [00:00<?, ?it/s]Validation X2Y - loss=3.5367e+00 ppl=34.35 best_loss=inf best_ppl=inf
Validation Y2X - loss=3.2095e+00 ppl=24.77 best_loss=inf best_ppl=inf
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=2.83, y2x=2.51]Epoch 2 - |param|=8.54e+02 |g_param|=2.10e+05 loss_x2y=3.6678e+00 ppl_x2y=39.16 loss_y2x=3.1738e+00 ppl_y2x=23.90 dual_loss=0.0000e+00
  1%|▋                                                                                          | 1/123 [00:00<?, ?it/s]Validation X2Y - loss=3.0049e+00 ppl=20.18 best_loss=3.5367e+00 best_ppl=34.35
Validation Y2X - loss=2.6763e+00 ppl=14.53 best_loss=3.2095e+00 best_ppl=24.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=2.44, y2x=2.21]Epoch 3 - |param|=8.54e+02 |g_param|=1.96e+05 loss_x2y=3.2347e+00 ppl_x2y=25.40 loss_y2x=2.8606e+00 ppl_y2x=17.47 dual_loss=0.0000e+00
Validation X2Y - loss=2.6038e+00 ppl=13.51 best_loss=3.0049e+00 best_ppl=20.18                                          
Validation Y2X - loss=2.3447e+00 ppl=10.43 best_loss=2.6763e+00 best_ppl=14.53
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 4 - |param|=8.55e+02 |g_param|=2.11e+05 loss_x2y=2.9636e+00 ppl_x2y=19.37 loss_y2x=2.5824e+00 ppl_y2x=13.23 dual_loss=0.0000e+00
Validation X2Y - loss=2.2866e+00 ppl=9.84 best_loss=2.6038e+00 best_ppl=13.51                                           
Validation Y2X - loss=2.0036e+00 ppl=7.42 best_loss=2.3447e+00 best_ppl=10.43
Iteration:   5%|██▊                                                           | 1/22 [00:00<?, ?it/s, x2y=1.91, y2x=1.7]Epoch 5 - |param|=8.56e+02 |g_param|=2.20e+05 loss_x2y=2.8164e+00 ppl_x2y=16.72 loss_y2x=2.4933e+00 ppl_y2x=12.10 dual_loss=0.0000e+00
Validation X2Y - loss=2.0760e+00 ppl=7.97 best_loss=2.2866e+00 best_ppl=9.84                                            
Validation Y2X - loss=1.8382e+00 ppl=6.28 best_loss=2.0036e+00 best_ppl=7.42
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 6 - |param|=8.56e+02 |g_param|=2.35e+05 loss_x2y=2.5384e+00 ppl_x2y=12.66 loss_y2x=2.2153e+00 ppl_y2x=9.16 dual_loss=0.0000e+00
Validation X2Y - loss=1.8352e+00 ppl=6.27 best_loss=2.0760e+00 best_ppl=7.97                                            
Validation Y2X - loss=1.6277e+00 ppl=5.09 best_loss=1.8382e+00 best_ppl=6.28
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.58, y2x=1.36]Epoch 7 - |param|=8.57e+02 |g_param|=2.33e+05 loss_x2y=2.4304e+00 ppl_x2y=11.36 loss_y2x=2.1178e+00 ppl_y2x=8.31 dual_loss=0.0000e+00
Validation X2Y - loss=1.7307e+00 ppl=5.64 best_loss=1.8352e+00 best_ppl=6.27                                            
Validation Y2X - loss=1.4973e+00 ppl=4.47 best_loss=1.6277e+00 best_ppl=5.09
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 8 - |param|=8.58e+02 |g_param|=2.52e+05 loss_x2y=2.2924e+00 ppl_x2y=9.90 loss_y2x=2.0082e+00 ppl_y2x=7.45 dual_loss=0.0000e+00
Validation X2Y - loss=1.6095e+00 ppl=5.00 best_loss=1.7307e+00 best_ppl=5.64                                            
Validation Y2X - loss=1.3769e+00 ppl=3.96 best_loss=1.4973e+00 best_ppl=4.47
Iteration:   5%|██▊                                                           | 1/22 [00:00<?, ?it/s, x2y=1.4, y2x=1.16]Epoch 9 - |param|=8.58e+02 |g_param|=2.55e+05 loss_x2y=2.1673e+00 ppl_x2y=8.73 loss_y2x=1.8876e+00 ppl_y2x=6.60 dual_loss=0.0000e+00
Validation X2Y - loss=1.5396e+00 ppl=4.66 best_loss=1.6095e+00 best_ppl=5.00                                            
Validation Y2X - loss=1.3003e+00 ppl=3.67 best_loss=1.3769e+00 best_ppl=3.96
Iteration:   5%|██▊                                                           | 1/22 [00:00<?, ?it/s, x2y=1.33, y2x=1.1]Epoch 10 - |param|=8.59e+02 |g_param|=2.72e+05 loss_x2y=2.1233e+00 ppl_x2y=8.36 loss_y2x=1.8288e+00 ppl_y2x=6.23 dual_loss=0.0000e+00
Validation X2Y - loss=1.4741e+00 ppl=4.37 best_loss=1.5396e+00 best_ppl=4.66                                            
Validation Y2X - loss=1.2400e+00 ppl=3.46 best_loss=1.3003e+00 best_ppl=3.67
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.32, y2x=1.07]Epoch 11 - |param|=8.59e+02 |g_param|=2.81e+05 loss_x2y=2.0983e+00 ppl_x2y=8.15 loss_y2x=1.7691e+00 ppl_y2x=5.87 dual_loss=0.0000e+00
Validation X2Y - loss=1.4486e+00 ppl=4.26 best_loss=1.4741e+00 best_ppl=4.37                                            
Validation Y2X - loss=1.2028e+00 ppl=3.33 best_loss=1.2400e+00 best_ppl=3.46
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.32, y2x=1.01]Epoch 12 - |param|=8.60e+02 |g_param|=2.96e+05 loss_x2y=2.0450e+00 ppl_x2y=7.73 loss_y2x=1.7725e+00 ppl_y2x=5.89 dual_loss=0.0000e+00
Validation X2Y - loss=1.4370e+00 ppl=4.21 best_loss=1.4486e+00 best_ppl=4.26                                            
Validation Y2X - loss=1.1542e+00 ppl=3.17 best_loss=1.2028e+00 best_ppl=3.33
Epoch 13 - |param|=8.60e+02 |g_param|=2.94e+05 loss_x2y=1.9339e+00 ppl_x2y=6.92 loss_y2x=1.7267e+00 ppl_y2x=5.62 dual_loss=0.0000e+00
Validation X2Y - loss=1.3511e+00 ppl=3.86 best_loss=1.4370e+00 best_ppl=4.21                                            
Validation Y2X - loss=1.0995e+00 ppl=3.00 best_loss=1.1542e+00 best_ppl=3.17
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.2, y2x=0.975]Epoch 14 - |param|=8.61e+02 |g_param|=3.02e+05 loss_x2y=1.7877e+00 ppl_x2y=5.98 loss_y2x=1.5168e+00 ppl_y2x=4.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.3452e+00 ppl=3.84 best_loss=1.3511e+00 best_ppl=3.86                                            
Validation Y2X - loss=1.1086e+00 ppl=3.03 best_loss=1.0995e+00 best_ppl=3.00
Iteration:   5%|██▋                                                         | 1/22 [00:00<?, ?it/s, x2y=1.17, y2x=0.949]Epoch 15 - |param|=8.61e+02 |g_param|=3.01e+05 loss_x2y=1.7872e+00 ppl_x2y=5.97 loss_y2x=1.5387e+00 ppl_y2x=4.66 dual_loss=0.0000e+00
Validation X2Y - loss=1.3035e+00 ppl=3.68 best_loss=1.3452e+00 best_ppl=3.84                                            
Validation Y2X - loss=1.0805e+00 ppl=2.95 best_loss=1.0995e+00 best_ppl=3.00
Iteration:   5%|██▋                                                         | 1/22 [00:00<?, ?it/s, x2y=1.25, y2x=0.968]Epoch 16 - |param|=8.62e+02 |g_param|=3.21e+05 loss_x2y=1.6954e+00 ppl_x2y=5.45 loss_y2x=1.4611e+00 ppl_y2x=4.31 dual_loss=0.0000e+00
Validation X2Y - loss=1.3558e+00 ppl=3.88 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0883e+00 ppl=2.97 best_loss=1.0805e+00 best_ppl=2.95
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 17 - |param|=8.62e+02 |g_param|=3.15e+05 loss_x2y=1.6684e+00 ppl_x2y=5.30 loss_y2x=1.4265e+00 ppl_y2x=4.16 dual_loss=0.0000e+00
Validation X2Y - loss=1.3396e+00 ppl=3.82 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0919e+00 ppl=2.98 best_loss=1.0805e+00 best_ppl=2.95
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 18 - |param|=8.63e+02 |g_param|=3.37e+05 loss_x2y=1.6076e+00 ppl_x2y=4.99 loss_y2x=1.3818e+00 ppl_y2x=3.98 dual_loss=0.0000e+00
Epoch [19/500]:   1%|▌                                                                          | 1/123 [00:00<?, ?it/s]Validation X2Y - loss=1.3132e+00 ppl=3.72 best_loss=1.3035e+00 best_ppl=3.68
Validation Y2X - loss=1.0187e+00 ppl=2.77 best_loss=1.0805e+00 best_ppl=2.95
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.2, y2x=0.873]Epoch 19 - |param|=8.64e+02 |g_param|=3.25e+05 loss_x2y=1.4826e+00 ppl_x2y=4.40 loss_y2x=1.2644e+00 ppl_y2x=3.54 dual_loss=0.0000e+00
Validation X2Y - loss=1.3141e+00 ppl=3.72 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0214e+00 ppl=2.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 20 - |param|=8.64e+02 |g_param|=3.53e+05 loss_x2y=1.4970e+00 ppl_x2y=4.47 loss_y2x=1.2774e+00 ppl_y2x=3.59 dual_loss=0.0000e+00
Validation X2Y - loss=1.3340e+00 ppl=3.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0705e+00 ppl=2.92 best_loss=1.0187e+00 best_ppl=2.77
Epoch 21 - |param|=8.65e+02 |g_param|=3.31e+05 loss_x2y=1.4460e+00 ppl_x2y=4.25 loss_y2x=1.2204e+00 ppl_y2x=3.39 dual_loss=5.2322e-01
Validation X2Y - loss=1.3255e+00 ppl=3.76 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0343e+00 ppl=2.81 best_loss=1.0187e+00 best_ppl=2.77
Epoch 22 - |param|=8.65e+02 |g_param|=3.51e+05 loss_x2y=1.4313e+00 ppl_x2y=4.18 loss_y2x=1.2411e+00 ppl_y2x=3.46 dual_loss=5.0702e-01
Validation X2Y - loss=1.3204e+00 ppl=3.74 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0668e+00 ppl=2.91 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 23 - |param|=8.66e+02 |g_param|=3.42e+05 loss_x2y=1.3956e+00 ppl_x2y=4.04 loss_y2x=1.1652e+00 ppl_y2x=3.21 dual_loss=4.8559e-01
Validation X2Y - loss=1.3602e+00 ppl=3.90 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0592e+00 ppl=2.88 best_loss=1.0187e+00 best_ppl=2.77
Epoch 24 - |param|=8.66e+02 |g_param|=3.62e+05 loss_x2y=1.4154e+00 ppl_x2y=4.12 loss_y2x=1.1948e+00 ppl_y2x=3.30 dual_loss=5.1838e-01
Validation X2Y - loss=1.3486e+00 ppl=3.85 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0680e+00 ppl=2.91 best_loss=1.0187e+00 best_ppl=2.77
Epoch 25 - |param|=8.67e+02 |g_param|=3.53e+05 loss_x2y=1.3403e+00 ppl_x2y=3.82 loss_y2x=1.1351e+00 ppl_y2x=3.11 dual_loss=4.8237e-01
Validation X2Y - loss=1.3549e+00 ppl=3.88 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0473e+00 ppl=2.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 26 - |param|=8.67e+02 |g_param|=3.76e+05 loss_x2y=1.3606e+00 ppl_x2y=3.90 loss_y2x=1.1920e+00 ppl_y2x=3.29 dual_loss=6.1540e-01
Validation X2Y - loss=1.3711e+00 ppl=3.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0212e+00 ppl=2.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 27 - |param|=8.68e+02 |g_param|=3.43e+05 loss_x2y=1.2408e+00 ppl_x2y=3.46 loss_y2x=1.0446e+00 ppl_y2x=2.84 dual_loss=4.4564e-01
Validation X2Y - loss=1.3358e+00 ppl=3.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0394e+00 ppl=2.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 28 - |param|=8.68e+02 |g_param|=3.68e+05 loss_x2y=1.2077e+00 ppl_x2y=3.35 loss_y2x=1.0327e+00 ppl_y2x=2.81 dual_loss=4.7372e-01
Validation X2Y - loss=1.3891e+00 ppl=4.01 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0814e+00 ppl=2.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 29 - |param|=8.69e+02 |g_param|=3.76e+05 loss_x2y=1.3214e+00 ppl_x2y=3.75 loss_y2x=1.0874e+00 ppl_y2x=2.97 dual_loss=6.6205e-01
Validation X2Y - loss=1.3657e+00 ppl=3.92 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0578e+00 ppl=2.88 best_loss=1.0187e+00 best_ppl=2.77
Epoch 30 - |param|=8.69e+02 |g_param|=4.03e+05 loss_x2y=1.2424e+00 ppl_x2y=3.46 loss_y2x=1.0922e+00 ppl_y2x=2.98 dual_loss=7.4434e-01
Validation X2Y - loss=1.4079e+00 ppl=4.09 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0653e+00 ppl=2.90 best_loss=1.0187e+00 best_ppl=2.77
Epoch 31 - |param|=8.70e+02 |g_param|=3.74e+05 loss_x2y=1.2321e+00 ppl_x2y=3.43 loss_y2x=1.0126e+00 ppl_y2x=2.75 dual_loss=5.4649e-01
Validation X2Y - loss=1.4318e+00 ppl=4.19 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1107e+00 ppl=3.04 best_loss=1.0187e+00 best_ppl=2.77
Epoch 32 - |param|=8.70e+02 |g_param|=3.81e+05 loss_x2y=1.1206e+00 ppl_x2y=3.07 loss_y2x=9.3153e-01 ppl_y2x=2.54 dual_loss=5.3969e-01
Validation X2Y - loss=1.3808e+00 ppl=3.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0926e+00 ppl=2.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 33 - |param|=8.71e+02 |g_param|=6.03e+05 loss_x2y=1.1136e+00 ppl_x2y=3.05 loss_y2x=9.3162e-01 ppl_y2x=2.54 dual_loss=5.3527e-01
Validation X2Y - loss=1.3953e+00 ppl=4.04 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.0995e+00 ppl=3.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 34 - |param|=8.71e+02 |g_param|=8.20e+05 loss_x2y=1.1950e+00 ppl_x2y=3.30 loss_y2x=9.8581e-01 ppl_y2x=2.68 dual_loss=6.5311e-01
Validation X2Y - loss=1.4216e+00 ppl=4.14 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1136e+00 ppl=3.05 best_loss=1.0187e+00 best_ppl=2.77
Epoch 35 - |param|=8.72e+02 |g_param|=7.62e+05 loss_x2y=1.1082e+00 ppl_x2y=3.03 loss_y2x=9.2150e-01 ppl_y2x=2.51 dual_loss=6.2690e-01
Validation X2Y - loss=1.4571e+00 ppl=4.29 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1439e+00 ppl=3.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 36 - |param|=8.72e+02 |g_param|=7.87e+05 loss_x2y=1.0355e+00 ppl_x2y=2.82 loss_y2x=8.4828e-01 ppl_y2x=2.34 dual_loss=5.4349e-01
Validation X2Y - loss=1.3943e+00 ppl=4.03 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1552e+00 ppl=3.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 37 - |param|=8.73e+02 |g_param|=7.81e+05 loss_x2y=1.0484e+00 ppl_x2y=2.85 loss_y2x=8.7424e-01 ppl_y2x=2.40 dual_loss=5.8551e-01
Validation X2Y - loss=1.4193e+00 ppl=4.13 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1541e+00 ppl=3.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 38 - |param|=8.73e+02 |g_param|=8.17e+05 loss_x2y=1.0439e+00 ppl_x2y=2.84 loss_y2x=8.5457e-01 ppl_y2x=2.35 dual_loss=6.2042e-01
Validation X2Y - loss=1.4618e+00 ppl=4.31 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1400e+00 ppl=3.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 39 - |param|=8.74e+02 |g_param|=7.61e+05 loss_x2y=1.0010e+00 ppl_x2y=2.72 loss_y2x=8.3498e-01 ppl_y2x=2.30 dual_loss=6.4298e-01
Validation X2Y - loss=1.4494e+00 ppl=4.26 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1554e+00 ppl=3.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 40 - |param|=8.74e+02 |g_param|=8.17e+05 loss_x2y=9.9306e-01 ppl_x2y=2.70 loss_y2x=8.3547e-01 ppl_y2x=2.31 dual_loss=6.6314e-01
Validation X2Y - loss=1.4473e+00 ppl=4.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1447e+00 ppl=3.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 41 - |param|=8.75e+02 |g_param|=7.92e+05 loss_x2y=9.2974e-01 ppl_x2y=2.53 loss_y2x=7.7684e-01 ppl_y2x=2.17 dual_loss=6.5972e-01
Validation X2Y - loss=1.4118e+00 ppl=4.10 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1662e+00 ppl=3.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 42 - |param|=8.75e+02 |g_param|=8.17e+05 loss_x2y=9.5348e-01 ppl_x2y=2.59 loss_y2x=7.9565e-01 ppl_y2x=2.22 dual_loss=6.7277e-01
Validation X2Y - loss=1.4924e+00 ppl=4.45 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2032e+00 ppl=3.33 best_loss=1.0187e+00 best_ppl=2.77
Epoch 43 - |param|=8.76e+02 |g_param|=7.94e+05 loss_x2y=9.2616e-01 ppl_x2y=2.52 loss_y2x=7.6836e-01 ppl_y2x=2.16 dual_loss=7.1769e-01
Validation X2Y - loss=1.4621e+00 ppl=4.31 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2053e+00 ppl=3.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 44 - |param|=8.76e+02 |g_param|=8.34e+05 loss_x2y=9.5223e-01 ppl_x2y=2.59 loss_y2x=8.0457e-01 ppl_y2x=2.24 dual_loss=7.3102e-01
Validation X2Y - loss=1.4635e+00 ppl=4.32 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1992e+00 ppl=3.32 best_loss=1.0187e+00 best_ppl=2.77
Epoch 45 - |param|=8.77e+02 |g_param|=7.77e+05 loss_x2y=8.9859e-01 ppl_x2y=2.46 loss_y2x=7.4023e-01 ppl_y2x=2.10 dual_loss=7.0210e-01
Validation X2Y - loss=1.4948e+00 ppl=4.46 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.1910e+00 ppl=3.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 46 - |param|=8.77e+02 |g_param|=8.17e+05 loss_x2y=8.6703e-01 ppl_x2y=2.38 loss_y2x=7.2143e-01 ppl_y2x=2.06 dual_loss=6.9341e-01
Validation X2Y - loss=1.4780e+00 ppl=4.38 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2180e+00 ppl=3.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 47 - |param|=8.78e+02 |g_param|=8.00e+05 loss_x2y=8.7266e-01 ppl_x2y=2.39 loss_y2x=7.1567e-01 ppl_y2x=2.05 dual_loss=7.3251e-01
Validation X2Y - loss=1.5144e+00 ppl=4.55 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2156e+00 ppl=3.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 48 - |param|=8.78e+02 |g_param|=8.43e+05 loss_x2y=8.3377e-01 ppl_x2y=2.30 loss_y2x=7.0006e-01 ppl_y2x=2.01 dual_loss=7.1774e-01
Validation X2Y - loss=1.4939e+00 ppl=4.45 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2049e+00 ppl=3.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 49 - |param|=8.79e+02 |g_param|=7.86e+05 loss_x2y=8.4075e-01 ppl_x2y=2.32 loss_y2x=6.9887e-01 ppl_y2x=2.01 dual_loss=7.1593e-01
Validation X2Y - loss=1.5033e+00 ppl=4.50 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2330e+00 ppl=3.43 best_loss=1.0187e+00 best_ppl=2.77
Epoch 50 - |param|=8.79e+02 |g_param|=6.38e+05 loss_x2y=8.4868e-01 ppl_x2y=2.34 loss_y2x=6.9907e-01 ppl_y2x=2.01 dual_loss=7.0627e-01
Validation X2Y - loss=1.4992e+00 ppl=4.48 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2242e+00 ppl=3.40 best_loss=1.0187e+00 best_ppl=2.77
Epoch 51 - |param|=8.80e+02 |g_param|=4.98e+05 loss_x2y=8.2006e-01 ppl_x2y=2.27 loss_y2x=6.7242e-01 ppl_y2x=1.96 dual_loss=7.4908e-01
Validation X2Y - loss=1.5347e+00 ppl=4.64 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2425e+00 ppl=3.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 52 - |param|=8.80e+02 |g_param|=5.52e+05 loss_x2y=8.3622e-01 ppl_x2y=2.31 loss_y2x=7.1701e-01 ppl_y2x=2.05 dual_loss=9.7292e-01
Validation X2Y - loss=1.5649e+00 ppl=4.78 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2360e+00 ppl=3.44 best_loss=1.0187e+00 best_ppl=2.77
Epoch 53 - |param|=8.81e+02 |g_param|=5.06e+05 loss_x2y=8.2151e-01 ppl_x2y=2.27 loss_y2x=6.6691e-01 ppl_y2x=1.95 dual_loss=9.1085e-01
Validation X2Y - loss=1.5688e+00 ppl=4.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2348e+00 ppl=3.44 best_loss=1.0187e+00 best_ppl=2.77
Epoch 54 - |param|=8.81e+02 |g_param|=5.32e+05 loss_x2y=8.1234e-01 ppl_x2y=2.25 loss_y2x=6.6481e-01 ppl_y2x=1.94 dual_loss=8.1656e-01
Validation X2Y - loss=1.5531e+00 ppl=4.73 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2380e+00 ppl=3.45 best_loss=1.0187e+00 best_ppl=2.77
Epoch 55 - |param|=8.82e+02 |g_param|=5.13e+05 loss_x2y=8.2320e-01 ppl_x2y=2.28 loss_y2x=6.8057e-01 ppl_y2x=1.98 dual_loss=8.3239e-01
Validation X2Y - loss=1.6069e+00 ppl=4.99 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2344e+00 ppl=3.44 best_loss=1.0187e+00 best_ppl=2.77
Epoch 56 - |param|=8.82e+02 |g_param|=5.21e+05 loss_x2y=7.8510e-01 ppl_x2y=2.19 loss_y2x=6.4573e-01 ppl_y2x=1.91 dual_loss=8.8009e-01
Validation X2Y - loss=1.5929e+00 ppl=4.92 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2578e+00 ppl=3.52 best_loss=1.0187e+00 best_ppl=2.77
Epoch 57 - |param|=8.83e+02 |g_param|=4.93e+05 loss_x2y=7.6406e-01 ppl_x2y=2.15 loss_y2x=6.1521e-01 ppl_y2x=1.85 dual_loss=8.2552e-01
Validation X2Y - loss=1.6049e+00 ppl=4.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2740e+00 ppl=3.58 best_loss=1.0187e+00 best_ppl=2.77
Epoch 58 - |param|=8.83e+02 |g_param|=5.46e+05 loss_x2y=7.8718e-01 ppl_x2y=2.20 loss_y2x=6.4709e-01 ppl_y2x=1.91 dual_loss=9.0531e-01
Validation X2Y - loss=1.5831e+00 ppl=4.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2933e+00 ppl=3.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 59 - |param|=8.84e+02 |g_param|=4.99e+05 loss_x2y=7.3328e-01 ppl_x2y=2.08 loss_y2x=6.0915e-01 ppl_y2x=1.84 dual_loss=9.0523e-01
Validation X2Y - loss=1.6559e+00 ppl=5.24 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3010e+00 ppl=3.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 60 - |param|=8.84e+02 |g_param|=5.18e+05 loss_x2y=7.9022e-01 ppl_x2y=2.20 loss_y2x=6.5051e-01 ppl_y2x=1.92 dual_loss=9.4057e-01
Validation X2Y - loss=1.6376e+00 ppl=5.14 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3457e+00 ppl=3.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 61 - |param|=8.84e+02 |g_param|=4.94e+05 loss_x2y=7.4734e-01 ppl_x2y=2.11 loss_y2x=6.2068e-01 ppl_y2x=1.86 dual_loss=8.9838e-01
Validation X2Y - loss=1.6759e+00 ppl=5.34 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2985e+00 ppl=3.66 best_loss=1.0187e+00 best_ppl=2.77
Epoch 62 - |param|=8.85e+02 |g_param|=5.16e+05 loss_x2y=7.6299e-01 ppl_x2y=2.14 loss_y2x=6.3118e-01 ppl_y2x=1.88 dual_loss=9.8958e-01
Validation X2Y - loss=1.6798e+00 ppl=5.36 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3448e+00 ppl=3.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 63 - |param|=8.85e+02 |g_param|=4.98e+05 loss_x2y=7.4145e-01 ppl_x2y=2.10 loss_y2x=5.9775e-01 ppl_y2x=1.82 dual_loss=8.8046e-01
Validation X2Y - loss=1.6942e+00 ppl=5.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3292e+00 ppl=3.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 64 - |param|=8.86e+02 |g_param|=5.08e+05 loss_x2y=6.8502e-01 ppl_x2y=1.98 loss_y2x=5.8048e-01 ppl_y2x=1.79 dual_loss=8.9862e-01
Validation X2Y - loss=1.6793e+00 ppl=5.36 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2741e+00 ppl=3.58 best_loss=1.0187e+00 best_ppl=2.77
Epoch 65 - |param|=8.86e+02 |g_param|=5.08e+05 loss_x2y=7.1392e-01 ppl_x2y=2.04 loss_y2x=5.9257e-01 ppl_y2x=1.81 dual_loss=9.6365e-01
Validation X2Y - loss=1.6867e+00 ppl=5.40 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.2811e+00 ppl=3.60 best_loss=1.0187e+00 best_ppl=2.77
Epoch 66 - |param|=8.87e+02 |g_param|=7.99e+05 loss_x2y=7.2720e-01 ppl_x2y=2.07 loss_y2x=6.3821e-01 ppl_y2x=1.89 dual_loss=1.4490e+00
Validation X2Y - loss=1.6680e+00 ppl=5.30 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3352e+00 ppl=3.80 best_loss=1.0187e+00 best_ppl=2.77
Epoch 67 - |param|=8.87e+02 |g_param|=5.72e+05 loss_x2y=7.3003e-01 ppl_x2y=2.08 loss_y2x=5.9357e-01 ppl_y2x=1.81 dual_loss=1.1749e+00
Validation X2Y - loss=1.7076e+00 ppl=5.52 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3154e+00 ppl=3.73 best_loss=1.0187e+00 best_ppl=2.77
Epoch 68 - |param|=8.88e+02 |g_param|=5.33e+05 loss_x2y=6.9403e-01 ppl_x2y=2.00 loss_y2x=5.6268e-01 ppl_y2x=1.76 dual_loss=9.2544e-01
Validation X2Y - loss=1.6624e+00 ppl=5.27 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3151e+00 ppl=3.73 best_loss=1.0187e+00 best_ppl=2.77
Epoch 69 - |param|=8.88e+02 |g_param|=5.09e+05 loss_x2y=6.8463e-01 ppl_x2y=1.98 loss_y2x=5.8932e-01 ppl_y2x=1.80 dual_loss=1.0910e+00
Validation X2Y - loss=1.6823e+00 ppl=5.38 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3271e+00 ppl=3.77 best_loss=1.0187e+00 best_ppl=2.77
Epoch 70 - |param|=8.88e+02 |g_param|=5.18e+05 loss_x2y=6.6327e-01 ppl_x2y=1.94 loss_y2x=5.3296e-01 ppl_y2x=1.70 dual_loss=8.9352e-01
Validation X2Y - loss=1.6888e+00 ppl=5.41 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3334e+00 ppl=3.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 71 - |param|=8.89e+02 |g_param|=5.14e+05 loss_x2y=6.9913e-01 ppl_x2y=2.01 loss_y2x=5.6385e-01 ppl_y2x=1.76 dual_loss=1.0916e+00
Validation X2Y - loss=1.7285e+00 ppl=5.63 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3660e+00 ppl=3.92 best_loss=1.0187e+00 best_ppl=2.77
Epoch 72 - |param|=8.89e+02 |g_param|=5.21e+05 loss_x2y=6.3176e-01 ppl_x2y=1.88 loss_y2x=5.2664e-01 ppl_y2x=1.69 dual_loss=9.6379e-01
Validation X2Y - loss=1.6907e+00 ppl=5.42 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3427e+00 ppl=3.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 73 - |param|=8.90e+02 |g_param|=5.08e+05 loss_x2y=6.9636e-01 ppl_x2y=2.01 loss_y2x=5.7571e-01 ppl_y2x=1.78 dual_loss=1.1380e+00
Validation X2Y - loss=1.7387e+00 ppl=5.69 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3436e+00 ppl=3.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 74 - |param|=8.90e+02 |g_param|=5.08e+05 loss_x2y=6.6036e-01 ppl_x2y=1.94 loss_y2x=5.3052e-01 ppl_y2x=1.70 dual_loss=1.0648e+00
Validation X2Y - loss=1.7491e+00 ppl=5.75 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3436e+00 ppl=3.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 75 - |param|=8.91e+02 |g_param|=4.77e+05 loss_x2y=6.1680e-01 ppl_x2y=1.85 loss_y2x=5.0832e-01 ppl_y2x=1.66 dual_loss=8.8677e-01
Validation X2Y - loss=1.7438e+00 ppl=5.72 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3426e+00 ppl=3.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 76 - |param|=8.91e+02 |g_param|=5.26e+05 loss_x2y=6.2584e-01 ppl_x2y=1.87 loss_y2x=5.1493e-01 ppl_y2x=1.67 dual_loss=1.0001e+00
Validation X2Y - loss=1.7071e+00 ppl=5.51 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3917e+00 ppl=4.02 best_loss=1.0187e+00 best_ppl=2.77
Epoch 77 - |param|=8.91e+02 |g_param|=4.96e+05 loss_x2y=6.3572e-01 ppl_x2y=1.89 loss_y2x=5.1126e-01 ppl_y2x=1.67 dual_loss=1.0668e+00
Validation X2Y - loss=1.6765e+00 ppl=5.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3571e+00 ppl=3.89 best_loss=1.0187e+00 best_ppl=2.77
Epoch 78 - |param|=8.92e+02 |g_param|=4.94e+05 loss_x2y=6.5993e-01 ppl_x2y=1.93 loss_y2x=5.1069e-01 ppl_y2x=1.67 dual_loss=1.0980e+00
Validation X2Y - loss=1.7398e+00 ppl=5.70 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3686e+00 ppl=3.93 best_loss=1.0187e+00 best_ppl=2.77
Epoch 79 - |param|=8.92e+02 |g_param|=4.92e+05 loss_x2y=6.1230e-01 ppl_x2y=1.84 loss_y2x=5.0245e-01 ppl_y2x=1.65 dual_loss=1.0198e+00
Validation X2Y - loss=1.7370e+00 ppl=5.68 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3892e+00 ppl=4.01 best_loss=1.0187e+00 best_ppl=2.77
Epoch 80 - |param|=8.93e+02 |g_param|=4.98e+05 loss_x2y=6.1497e-01 ppl_x2y=1.85 loss_y2x=4.9940e-01 ppl_y2x=1.65 dual_loss=9.8538e-01
Validation X2Y - loss=1.7709e+00 ppl=5.88 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3809e+00 ppl=3.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 81 - |param|=8.93e+02 |g_param|=4.86e+05 loss_x2y=5.9797e-01 ppl_x2y=1.82 loss_y2x=4.9677e-01 ppl_y2x=1.64 dual_loss=1.0364e+00
Validation X2Y - loss=1.8136e+00 ppl=6.13 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4087e+00 ppl=4.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 82 - |param|=8.94e+02 |g_param|=4.98e+05 loss_x2y=6.0144e-01 ppl_x2y=1.82 loss_y2x=4.8795e-01 ppl_y2x=1.63 dual_loss=1.0556e+00
Validation X2Y - loss=1.8048e+00 ppl=6.08 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.3963e+00 ppl=4.04 best_loss=1.0187e+00 best_ppl=2.77
Epoch 83 - |param|=8.94e+02 |g_param|=4.91e+05 loss_x2y=6.0952e-01 ppl_x2y=1.84 loss_y2x=5.0042e-01 ppl_y2x=1.65 dual_loss=1.1145e+00
Validation X2Y - loss=1.8184e+00 ppl=6.16 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4290e+00 ppl=4.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 84 - |param|=8.94e+02 |g_param|=5.05e+05 loss_x2y=6.0419e-01 ppl_x2y=1.83 loss_y2x=4.8417e-01 ppl_y2x=1.62 dual_loss=1.0479e+00
Validation X2Y - loss=1.7713e+00 ppl=5.88 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4010e+00 ppl=4.06 best_loss=1.0187e+00 best_ppl=2.77
Epoch 85 - |param|=8.95e+02 |g_param|=4.86e+05 loss_x2y=5.9004e-01 ppl_x2y=1.80 loss_y2x=4.8160e-01 ppl_y2x=1.62 dual_loss=1.0663e+00
Validation X2Y - loss=1.7737e+00 ppl=5.89 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4034e+00 ppl=4.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 86 - |param|=8.95e+02 |g_param|=4.95e+05 loss_x2y=5.8508e-01 ppl_x2y=1.80 loss_y2x=4.7565e-01 ppl_y2x=1.61 dual_loss=1.0943e+00
Validation X2Y - loss=1.8329e+00 ppl=6.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4268e+00 ppl=4.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 87 - |param|=8.96e+02 |g_param|=4.88e+05 loss_x2y=5.9610e-01 ppl_x2y=1.82 loss_y2x=5.0592e-01 ppl_y2x=1.66 dual_loss=1.1345e+00
Validation X2Y - loss=1.8558e+00 ppl=6.40 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4511e+00 ppl=4.27 best_loss=1.0187e+00 best_ppl=2.77
Epoch 88 - |param|=8.96e+02 |g_param|=5.08e+05 loss_x2y=6.2482e-01 ppl_x2y=1.87 loss_y2x=4.9001e-01 ppl_y2x=1.63 dual_loss=1.2536e+00
Validation X2Y - loss=1.8523e+00 ppl=6.37 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4250e+00 ppl=4.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 89 - |param|=8.96e+02 |g_param|=4.80e+05 loss_x2y=5.5892e-01 ppl_x2y=1.75 loss_y2x=4.5276e-01 ppl_y2x=1.57 dual_loss=1.0942e+00
Validation X2Y - loss=1.8558e+00 ppl=6.40 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4094e+00 ppl=4.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 90 - |param|=8.97e+02 |g_param|=4.97e+05 loss_x2y=5.6722e-01 ppl_x2y=1.76 loss_y2x=4.6037e-01 ppl_y2x=1.58 dual_loss=1.1429e+00
Validation X2Y - loss=1.8229e+00 ppl=6.19 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4310e+00 ppl=4.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 91 - |param|=8.97e+02 |g_param|=4.69e+05 loss_x2y=5.7003e-01 ppl_x2y=1.77 loss_y2x=4.6120e-01 ppl_y2x=1.59 dual_loss=1.1353e+00
Validation X2Y - loss=1.8390e+00 ppl=6.29 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4350e+00 ppl=4.20 best_loss=1.0187e+00 best_ppl=2.77
Epoch 92 - |param|=8.98e+02 |g_param|=5.06e+05 loss_x2y=5.5605e-01 ppl_x2y=1.74 loss_y2x=4.5204e-01 ppl_y2x=1.57 dual_loss=1.0993e+00
Validation X2Y - loss=1.8956e+00 ppl=6.66 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4545e+00 ppl=4.28 best_loss=1.0187e+00 best_ppl=2.77
Epoch 93 - |param|=8.98e+02 |g_param|=4.68e+05 loss_x2y=5.8644e-01 ppl_x2y=1.80 loss_y2x=4.4399e-01 ppl_y2x=1.56 dual_loss=1.1004e+00
Validation X2Y - loss=1.8357e+00 ppl=6.27 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4227e+00 ppl=4.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 94 - |param|=8.98e+02 |g_param|=4.90e+05 loss_x2y=5.6125e-01 ppl_x2y=1.75 loss_y2x=4.4488e-01 ppl_y2x=1.56 dual_loss=1.0945e+00
Validation X2Y - loss=1.8637e+00 ppl=6.45 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5053e+00 ppl=4.51 best_loss=1.0187e+00 best_ppl=2.77
Epoch 95 - |param|=8.99e+02 |g_param|=4.68e+05 loss_x2y=5.3975e-01 ppl_x2y=1.72 loss_y2x=4.4144e-01 ppl_y2x=1.55 dual_loss=1.1664e+00
Validation X2Y - loss=1.8733e+00 ppl=6.51 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4357e+00 ppl=4.20 best_loss=1.0187e+00 best_ppl=2.77
Epoch 96 - |param|=8.99e+02 |g_param|=4.99e+05 loss_x2y=5.5384e-01 ppl_x2y=1.74 loss_y2x=4.2826e-01 ppl_y2x=1.53 dual_loss=1.0929e+00
Validation X2Y - loss=1.8519e+00 ppl=6.37 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4557e+00 ppl=4.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 97 - |param|=9.00e+02 |g_param|=4.92e+05 loss_x2y=5.4501e-01 ppl_x2y=1.72 loss_y2x=4.7464e-01 ppl_y2x=1.61 dual_loss=1.3690e+00
Validation X2Y - loss=1.8896e+00 ppl=6.62 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4196e+00 ppl=4.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 98 - |param|=9.00e+02 |g_param|=4.85e+05 loss_x2y=5.2005e-01 ppl_x2y=1.68 loss_y2x=4.2223e-01 ppl_y2x=1.53 dual_loss=1.0779e+00
Validation X2Y - loss=1.9014e+00 ppl=6.70 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4398e+00 ppl=4.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 99 - |param|=9.00e+02 |g_param|=4.79e+05 loss_x2y=5.3835e-01 ppl_x2y=1.71 loss_y2x=4.6026e-01 ppl_y2x=1.58 dual_loss=1.3881e+00
Validation X2Y - loss=1.9472e+00 ppl=7.01 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4405e+00 ppl=4.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 100 - |param|=9.01e+02 |g_param|=7.59e+05 loss_x2y=5.3877e-01 ppl_x2y=1.71 loss_y2x=4.2602e-01 ppl_y2x=1.53 dual_loss=1.1542e+00
Validation X2Y - loss=1.9142e+00 ppl=6.78 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4325e+00 ppl=4.19 best_loss=1.0187e+00 best_ppl=2.77
Epoch 101 - |param|=9.01e+02 |g_param|=7.23e+05 loss_x2y=5.0191e-01 ppl_x2y=1.65 loss_y2x=4.1839e-01 ppl_y2x=1.52 dual_loss=1.0769e+00
Validation X2Y - loss=1.9270e+00 ppl=6.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4521e+00 ppl=4.27 best_loss=1.0187e+00 best_ppl=2.77
Epoch 102 - |param|=9.02e+02 |g_param|=7.66e+05 loss_x2y=5.3537e-01 ppl_x2y=1.71 loss_y2x=4.2848e-01 ppl_y2x=1.53 dual_loss=1.1658e+00
Validation X2Y - loss=1.8722e+00 ppl=6.50 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4888e+00 ppl=4.43 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                           | 1/22 [00:00<?, ?it/s, x2y=1.7, y2x=1.23]Epoch 103 - |param|=9.02e+02 |g_param|=7.25e+05 loss_x2y=5.0364e-01 ppl_x2y=1.65 loss_y2x=4.1032e-01 ppl_y2x=1.51 dual_loss=1.1131e+00
Validation X2Y - loss=1.8748e+00 ppl=6.52 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4438e+00 ppl=4.24 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 104 - |param|=9.02e+02 |g_param|=7.47e+05 loss_x2y=5.1490e-01 ppl_x2y=1.67 loss_y2x=4.3157e-01 ppl_y2x=1.54 dual_loss=1.2112e+00
Validation X2Y - loss=1.8631e+00 ppl=6.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4385e+00 ppl=4.21 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 105 - |param|=9.03e+02 |g_param|=4.95e+05 loss_x2y=5.1236e-01 ppl_x2y=1.67 loss_y2x=4.0910e-01 ppl_y2x=1.51 dual_loss=1.1584e+00
Validation X2Y - loss=1.8895e+00 ppl=6.62 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4485e+00 ppl=4.26 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 106 - |param|=9.03e+02 |g_param|=4.78e+05 loss_x2y=5.2029e-01 ppl_x2y=1.68 loss_y2x=4.1506e-01 ppl_y2x=1.51 dual_loss=1.1492e+00
  1%|▋                                                                                          | 1/123 [00:00<?, ?it/s]Validation X2Y - loss=1.8767e+00 ppl=6.53 best_loss=1.3035e+00 best_ppl=3.68
Validation Y2X - loss=1.4653e+00 ppl=4.33 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.77, y2x=1.22]Epoch 107 - |param|=9.04e+02 |g_param|=4.54e+05 loss_x2y=5.2190e-01 ppl_x2y=1.69 loss_y2x=4.0751e-01 ppl_y2x=1.50 dual_loss=1.1926e+00
Validation X2Y - loss=1.9296e+00 ppl=6.89 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4458e+00 ppl=4.25 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.69, y2x=1.26]Epoch 108 - |param|=9.04e+02 |g_param|=4.98e+05 loss_x2y=5.3164e-01 ppl_x2y=1.70 loss_y2x=4.3550e-01 ppl_y2x=1.55 dual_loss=1.4086e+00
Validation X2Y - loss=1.8755e+00 ppl=6.52 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4734e+00 ppl=4.36 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.74, y2x=1.21]Epoch 109 - |param|=9.04e+02 |g_param|=4.61e+05 loss_x2y=4.8350e-01 ppl_x2y=1.62 loss_y2x=3.9868e-01 ppl_y2x=1.49 dual_loss=1.0979e+00
Epoch [110/500]:   1%|▌                                                                         | 1/123 [00:00<?, ?it/s]Validation X2Y - loss=1.9097e+00 ppl=6.75 best_loss=1.3035e+00 best_ppl=3.68
Validation Y2X - loss=1.4384e+00 ppl=4.21 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.78, y2x=1.24]Epoch 110 - |param|=9.05e+02 |g_param|=4.72e+05 loss_x2y=5.0149e-01 ppl_x2y=1.65 loss_y2x=3.9432e-01 ppl_y2x=1.48 dual_loss=1.1895e+00
Validation X2Y - loss=1.9420e+00 ppl=6.97 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4548e+00 ppl=4.28 best_loss=1.0187e+00 best_ppl=2.77
  5%|████▏                                                                                       | 1/22 [00:00<?, ?it/s]Epoch 111 - |param|=9.05e+02 |g_param|=4.54e+05 loss_x2y=4.9506e-01 ppl_x2y=1.64 loss_y2x=4.0280e-01 ppl_y2x=1.50 dual_loss=1.2363e+00
Validation X2Y - loss=1.9429e+00 ppl=6.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4251e+00 ppl=4.16 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 112 - |param|=9.06e+02 |g_param|=4.66e+05 loss_x2y=5.7083e-01 ppl_x2y=1.77 loss_y2x=4.4918e-01 ppl_y2x=1.57 dual_loss=1.6090e+00
Validation X2Y - loss=1.9795e+00 ppl=7.24 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4866e+00 ppl=4.42 best_loss=1.0187e+00 best_ppl=2.77
Epoch 113 - |param|=9.06e+02 |g_param|=4.53e+05 loss_x2y=4.8212e-01 ppl_x2y=1.62 loss_y2x=4.0766e-01 ppl_y2x=1.50 dual_loss=1.2598e+00
Validation X2Y - loss=1.9372e+00 ppl=6.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4695e+00 ppl=4.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 114 - |param|=9.06e+02 |g_param|=4.64e+05 loss_x2y=4.7221e-01 ppl_x2y=1.60 loss_y2x=3.8983e-01 ppl_y2x=1.48 dual_loss=1.1685e+00
Validation X2Y - loss=2.0070e+00 ppl=7.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4521e+00 ppl=4.27 best_loss=1.0187e+00 best_ppl=2.77
Epoch 115 - |param|=9.07e+02 |g_param|=5.71e+05 loss_x2y=4.7961e-01 ppl_x2y=1.62 loss_y2x=3.8664e-01 ppl_y2x=1.47 dual_loss=1.1936e+00
Validation X2Y - loss=1.9430e+00 ppl=6.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5464e+00 ppl=4.69 best_loss=1.0187e+00 best_ppl=2.77
Epoch 116 - |param|=9.07e+02 |g_param|=7.49e+05 loss_x2y=5.0322e-01 ppl_x2y=1.65 loss_y2x=3.9263e-01 ppl_y2x=1.48 dual_loss=1.3188e+00
Validation X2Y - loss=1.9527e+00 ppl=7.05 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5408e+00 ppl=4.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 117 - |param|=9.07e+02 |g_param|=4.86e+05 loss_x2y=4.7919e-01 ppl_x2y=1.61 loss_y2x=3.7263e-01 ppl_y2x=1.45 dual_loss=1.2204e+00
Validation X2Y - loss=1.9848e+00 ppl=7.28 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5162e+00 ppl=4.56 best_loss=1.0187e+00 best_ppl=2.77
Epoch 118 - |param|=9.08e+02 |g_param|=4.61e+05 loss_x2y=4.8108e-01 ppl_x2y=1.62 loss_y2x=3.8594e-01 ppl_y2x=1.47 dual_loss=1.2479e+00
Validation X2Y - loss=1.9483e+00 ppl=7.02 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5297e+00 ppl=4.62 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 119 - |param|=9.08e+02 |g_param|=4.41e+05 loss_x2y=4.7137e-01 ppl_x2y=1.60 loss_y2x=3.8245e-01 ppl_y2x=1.47 dual_loss=1.2120e+00
Validation X2Y - loss=1.9656e+00 ppl=7.14 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5222e+00 ppl=4.58 best_loss=1.0187e+00 best_ppl=2.77
Epoch 120 - |param|=9.09e+02 |g_param|=4.69e+05 loss_x2y=4.7055e-01 ppl_x2y=1.60 loss_y2x=4.0727e-01 ppl_y2x=1.50 dual_loss=1.5283e+00
Validation X2Y - loss=1.9348e+00 ppl=6.92 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5334e+00 ppl=4.63 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 121 - |param|=9.09e+02 |g_param|=4.45e+05 loss_x2y=4.8063e-01 ppl_x2y=1.62 loss_y2x=3.8034e-01 ppl_y2x=1.46 dual_loss=1.2179e+00
Validation X2Y - loss=1.9809e+00 ppl=7.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4828e+00 ppl=4.41 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 122 - |param|=9.09e+02 |g_param|=4.54e+05 loss_x2y=4.5768e-01 ppl_x2y=1.58 loss_y2x=3.7308e-01 ppl_y2x=1.45 dual_loss=1.2583e+00
Validation X2Y - loss=2.0367e+00 ppl=7.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.4954e+00 ppl=4.46 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 123 - |param|=9.10e+02 |g_param|=4.39e+05 loss_x2y=4.5524e-01 ppl_x2y=1.58 loss_y2x=3.7291e-01 ppl_y2x=1.45 dual_loss=1.2198e+00
Validation X2Y - loss=2.0135e+00 ppl=7.49 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5377e+00 ppl=4.65 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 124 - |param|=9.10e+02 |g_param|=4.62e+05 loss_x2y=4.7785e-01 ppl_x2y=1.61 loss_y2x=3.9848e-01 ppl_y2x=1.49 dual_loss=1.4041e+00
Validation X2Y - loss=1.9884e+00 ppl=7.30 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5452e+00 ppl=4.69 best_loss=1.0187e+00 best_ppl=2.77
Epoch 125 - |param|=9.10e+02 |g_param|=4.49e+05 loss_x2y=4.9407e-01 ppl_x2y=1.64 loss_y2x=3.8601e-01 ppl_y2x=1.47 dual_loss=1.3650e+00
Validation X2Y - loss=2.0027e+00 ppl=7.41 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5564e+00 ppl=4.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 126 - |param|=9.11e+02 |g_param|=4.50e+05 loss_x2y=4.6176e-01 ppl_x2y=1.59 loss_y2x=3.6946e-01 ppl_y2x=1.45 dual_loss=1.2792e+00
Validation X2Y - loss=1.9884e+00 ppl=7.30 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5758e+00 ppl=4.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 127 - |param|=9.11e+02 |g_param|=4.29e+05 loss_x2y=4.5437e-01 ppl_x2y=1.58 loss_y2x=3.6583e-01 ppl_y2x=1.44 dual_loss=1.2706e+00
Validation X2Y - loss=2.0327e+00 ppl=7.64 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5940e+00 ppl=4.92 best_loss=1.0187e+00 best_ppl=2.77
Epoch 128 - |param|=9.12e+02 |g_param|=4.49e+05 loss_x2y=4.4772e-01 ppl_x2y=1.56 loss_y2x=3.6126e-01 ppl_y2x=1.44 dual_loss=1.2644e+00
Validation X2Y - loss=1.9808e+00 ppl=7.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5435e+00 ppl=4.68 best_loss=1.0187e+00 best_ppl=2.77
Epoch 129 - |param|=9.12e+02 |g_param|=4.30e+05 loss_x2y=4.5649e-01 ppl_x2y=1.58 loss_y2x=3.7309e-01 ppl_y2x=1.45 dual_loss=1.2958e+00
Validation X2Y - loss=1.9784e+00 ppl=7.23 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5414e+00 ppl=4.67 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 130 - |param|=9.12e+02 |g_param|=4.42e+05 loss_x2y=4.4934e-01 ppl_x2y=1.57 loss_y2x=3.5942e-01 ppl_y2x=1.43 dual_loss=1.2951e+00
Validation X2Y - loss=1.9444e+00 ppl=6.99 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5648e+00 ppl=4.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 131 - |param|=9.13e+02 |g_param|=4.28e+05 loss_x2y=5.1089e-01 ppl_x2y=1.67 loss_y2x=3.9520e-01 ppl_y2x=1.48 dual_loss=1.5928e+00
Validation X2Y - loss=1.9920e+00 ppl=7.33 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5639e+00 ppl=4.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 132 - |param|=9.13e+02 |g_param|=4.45e+05 loss_x2y=4.4430e-01 ppl_x2y=1.56 loss_y2x=3.6389e-01 ppl_y2x=1.44 dual_loss=1.3987e+00
Validation X2Y - loss=1.9544e+00 ppl=7.06 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5692e+00 ppl=4.80 best_loss=1.0187e+00 best_ppl=2.77
Epoch 133 - |param|=9.13e+02 |g_param|=4.29e+05 loss_x2y=4.3429e-01 ppl_x2y=1.54 loss_y2x=3.6209e-01 ppl_y2x=1.44 dual_loss=1.3452e+00
Validation X2Y - loss=1.9959e+00 ppl=7.36 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5808e+00 ppl=4.86 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.75, y2x=1.34]Epoch 134 - |param|=9.14e+02 |g_param|=4.51e+05 loss_x2y=4.5588e-01 ppl_x2y=1.58 loss_y2x=3.7245e-01 ppl_y2x=1.45 dual_loss=1.3550e+00
Validation X2Y - loss=1.9587e+00 ppl=7.09 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5507e+00 ppl=4.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 135 - |param|=9.14e+02 |g_param|=4.34e+05 loss_x2y=4.2785e-01 ppl_x2y=1.53 loss_y2x=3.6855e-01 ppl_y2x=1.45 dual_loss=1.4717e+00
Validation X2Y - loss=1.9577e+00 ppl=7.08 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5566e+00 ppl=4.74 best_loss=1.0187e+00 best_ppl=2.77
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 136 - |param|=9.15e+02 |g_param|=4.44e+05 loss_x2y=4.5708e-01 ppl_x2y=1.58 loss_y2x=3.8720e-01 ppl_y2x=1.47 dual_loss=1.6605e+00
Validation X2Y - loss=1.9890e+00 ppl=7.31 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5889e+00 ppl=4.90 best_loss=1.0187e+00 best_ppl=2.77
Epoch 137 - |param|=9.15e+02 |g_param|=5.16e+05 loss_x2y=4.4975e-01 ppl_x2y=1.57 loss_y2x=3.6087e-01 ppl_y2x=1.43 dual_loss=1.3524e+00
Validation X2Y - loss=2.0107e+00 ppl=7.47 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5404e+00 ppl=4.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 138 - |param|=9.15e+02 |g_param|=6.68e+05 loss_x2y=4.3024e-01 ppl_x2y=1.54 loss_y2x=3.4831e-01 ppl_y2x=1.42 dual_loss=1.3249e+00
Validation X2Y - loss=2.0534e+00 ppl=7.79 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5671e+00 ppl=4.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 139 - |param|=9.16e+02 |g_param|=6.61e+05 loss_x2y=4.2066e-01 ppl_x2y=1.52 loss_y2x=3.4208e-01 ppl_y2x=1.41 dual_loss=1.2628e+00
Validation X2Y - loss=2.0877e+00 ppl=8.07 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5562e+00 ppl=4.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 140 - |param|=9.16e+02 |g_param|=7.10e+05 loss_x2y=4.5154e-01 ppl_x2y=1.57 loss_y2x=3.8234e-01 ppl_y2x=1.47 dual_loss=1.6058e+00
Validation X2Y - loss=2.0626e+00 ppl=7.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5671e+00 ppl=4.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 141 - |param|=9.16e+02 |g_param|=6.78e+05 loss_x2y=4.7735e-01 ppl_x2y=1.61 loss_y2x=3.7006e-01 ppl_y2x=1.45 dual_loss=1.5304e+00
Validation X2Y - loss=2.0630e+00 ppl=7.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5838e+00 ppl=4.87 best_loss=1.0187e+00 best_ppl=2.77
Epoch 142 - |param|=9.17e+02 |g_param|=6.86e+05 loss_x2y=4.0515e-01 ppl_x2y=1.50 loss_y2x=3.2741e-01 ppl_y2x=1.39 dual_loss=1.2419e+00
Validation X2Y - loss=1.9819e+00 ppl=7.26 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5485e+00 ppl=4.70 best_loss=1.0187e+00 best_ppl=2.77
Epoch 143 - |param|=9.17e+02 |g_param|=6.55e+05 loss_x2y=4.2822e-01 ppl_x2y=1.53 loss_y2x=3.4359e-01 ppl_y2x=1.41 dual_loss=1.3935e+00
Validation X2Y - loss=2.0219e+00 ppl=7.55 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6046e+00 ppl=4.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 144 - |param|=9.17e+02 |g_param|=6.53e+05 loss_x2y=4.2115e-01 ppl_x2y=1.52 loss_y2x=3.3803e-01 ppl_y2x=1.40 dual_loss=1.2983e+00
Validation X2Y - loss=2.0699e+00 ppl=7.92 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6324e+00 ppl=5.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 145 - |param|=9.18e+02 |g_param|=4.60e+05 loss_x2y=4.7826e-01 ppl_x2y=1.61 loss_y2x=3.6964e-01 ppl_y2x=1.45 dual_loss=1.7794e+00
Validation X2Y - loss=2.0702e+00 ppl=7.93 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5601e+00 ppl=4.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 146 - |param|=9.18e+02 |g_param|=4.48e+05 loss_x2y=4.2965e-01 ppl_x2y=1.54 loss_y2x=3.4125e-01 ppl_y2x=1.41 dual_loss=1.3815e+00
Validation X2Y - loss=2.0637e+00 ppl=7.88 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6062e+00 ppl=4.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 147 - |param|=9.19e+02 |g_param|=4.22e+05 loss_x2y=4.3118e-01 ppl_x2y=1.54 loss_y2x=3.5605e-01 ppl_y2x=1.43 dual_loss=1.4922e+00
Validation X2Y - loss=2.0904e+00 ppl=8.09 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5930e+00 ppl=4.92 best_loss=1.0187e+00 best_ppl=2.77
Epoch 148 - |param|=9.19e+02 |g_param|=4.30e+05 loss_x2y=4.3677e-01 ppl_x2y=1.55 loss_y2x=3.4598e-01 ppl_y2x=1.41 dual_loss=1.4337e+00
Validation X2Y - loss=2.0740e+00 ppl=7.96 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5793e+00 ppl=4.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 149 - |param|=9.19e+02 |g_param|=4.98e+05 loss_x2y=3.9987e-01 ppl_x2y=1.49 loss_y2x=3.3302e-01 ppl_y2x=1.40 dual_loss=1.2696e+00
Validation X2Y - loss=2.0743e+00 ppl=7.96 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6406e+00 ppl=5.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 150 - |param|=9.20e+02 |g_param|=6.69e+05 loss_x2y=4.2785e-01 ppl_x2y=1.53 loss_y2x=3.4680e-01 ppl_y2x=1.41 dual_loss=1.5136e+00
Validation X2Y - loss=2.1162e+00 ppl=8.30 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6151e+00 ppl=5.03 best_loss=1.0187e+00 best_ppl=2.77
Epoch 151 - |param|=9.20e+02 |g_param|=6.56e+05 loss_x2y=4.0663e-01 ppl_x2y=1.50 loss_y2x=3.3041e-01 ppl_y2x=1.39 dual_loss=1.3515e+00
Validation X2Y - loss=2.0810e+00 ppl=8.01 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6152e+00 ppl=5.03 best_loss=1.0187e+00 best_ppl=2.77
Epoch 152 - |param|=9.20e+02 |g_param|=6.75e+05 loss_x2y=4.0543e-01 ppl_x2y=1.50 loss_y2x=3.2470e-01 ppl_y2x=1.38 dual_loss=1.3924e+00
Validation X2Y - loss=2.1277e+00 ppl=8.40 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5988e+00 ppl=4.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 153 - |param|=9.21e+02 |g_param|=4.27e+05 loss_x2y=4.2006e-01 ppl_x2y=1.52 loss_y2x=3.1727e-01 ppl_y2x=1.37 dual_loss=1.3974e+00
Validation X2Y - loss=2.0973e+00 ppl=8.14 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6347e+00 ppl=5.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 154 - |param|=9.21e+02 |g_param|=4.17e+05 loss_x2y=3.9558e-01 ppl_x2y=1.49 loss_y2x=3.2279e-01 ppl_y2x=1.38 dual_loss=1.3457e+00
Validation X2Y - loss=2.0596e+00 ppl=7.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6089e+00 ppl=5.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 155 - |param|=9.21e+02 |g_param|=4.03e+05 loss_x2y=4.1621e-01 ppl_x2y=1.52 loss_y2x=3.2261e-01 ppl_y2x=1.38 dual_loss=1.3891e+00
Validation X2Y - loss=2.0617e+00 ppl=7.86 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5309e+00 ppl=4.62 best_loss=1.0187e+00 best_ppl=2.77
Epoch 156 - |param|=9.22e+02 |g_param|=4.22e+05 loss_x2y=4.1703e-01 ppl_x2y=1.52 loss_y2x=3.2667e-01 ppl_y2x=1.39 dual_loss=1.4314e+00
Validation X2Y - loss=2.0061e+00 ppl=7.43 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5960e+00 ppl=4.93 best_loss=1.0187e+00 best_ppl=2.77
Epoch 157 - |param|=9.22e+02 |g_param|=4.02e+05 loss_x2y=3.8814e-01 ppl_x2y=1.47 loss_y2x=3.1635e-01 ppl_y2x=1.37 dual_loss=1.3055e+00
Validation X2Y - loss=2.0667e+00 ppl=7.90 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5914e+00 ppl=4.91 best_loss=1.0187e+00 best_ppl=2.77
Epoch 158 - |param|=9.22e+02 |g_param|=4.12e+05 loss_x2y=3.8194e-01 ppl_x2y=1.47 loss_y2x=3.0938e-01 ppl_y2x=1.36 dual_loss=1.3269e+00
Validation X2Y - loss=2.0718e+00 ppl=7.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6268e+00 ppl=5.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 159 - |param|=9.23e+02 |g_param|=3.97e+05 loss_x2y=3.8594e-01 ppl_x2y=1.47 loss_y2x=3.2528e-01 ppl_y2x=1.38 dual_loss=1.3454e+00
Validation X2Y - loss=2.0977e+00 ppl=8.15 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5671e+00 ppl=4.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 160 - |param|=9.23e+02 |g_param|=4.13e+05 loss_x2y=3.8641e-01 ppl_x2y=1.47 loss_y2x=3.1183e-01 ppl_y2x=1.37 dual_loss=1.3408e+00
Validation X2Y - loss=2.0989e+00 ppl=8.16 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5605e+00 ppl=4.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 161 - |param|=9.23e+02 |g_param|=4.06e+05 loss_x2y=3.9491e-01 ppl_x2y=1.48 loss_y2x=3.2231e-01 ppl_y2x=1.38 dual_loss=1.4480e+00
Validation X2Y - loss=2.0794e+00 ppl=8.00 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5827e+00 ppl=4.87 best_loss=1.0187e+00 best_ppl=2.77
Epoch 162 - |param|=9.24e+02 |g_param|=4.16e+05 loss_x2y=4.0840e-01 ppl_x2y=1.50 loss_y2x=3.2748e-01 ppl_y2x=1.39 dual_loss=1.4656e+00
Validation X2Y - loss=2.0110e+00 ppl=7.47 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5999e+00 ppl=4.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 163 - |param|=9.24e+02 |g_param|=3.90e+05 loss_x2y=3.8450e-01 ppl_x2y=1.47 loss_y2x=3.0658e-01 ppl_y2x=1.36 dual_loss=1.3304e+00
Validation X2Y - loss=2.1057e+00 ppl=8.21 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6109e+00 ppl=5.01 best_loss=1.0187e+00 best_ppl=2.77
Epoch 164 - |param|=9.24e+02 |g_param|=4.21e+05 loss_x2y=4.0961e-01 ppl_x2y=1.51 loss_y2x=3.6142e-01 ppl_y2x=1.44 dual_loss=1.9024e+00
Validation X2Y - loss=2.0714e+00 ppl=7.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6004e+00 ppl=4.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 165 - |param|=9.25e+02 |g_param|=3.96e+05 loss_x2y=3.8860e-01 ppl_x2y=1.47 loss_y2x=3.1807e-01 ppl_y2x=1.37 dual_loss=1.4554e+00
Validation X2Y - loss=2.0990e+00 ppl=8.16 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6234e+00 ppl=5.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 166 - |param|=9.25e+02 |g_param|=4.04e+05 loss_x2y=3.8405e-01 ppl_x2y=1.47 loss_y2x=3.1954e-01 ppl_y2x=1.38 dual_loss=1.3673e+00
Validation X2Y - loss=2.0382e+00 ppl=7.68 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5981e+00 ppl=4.94 best_loss=1.0187e+00 best_ppl=2.77
Epoch 167 - |param|=9.25e+02 |g_param|=4.02e+05 loss_x2y=3.9994e-01 ppl_x2y=1.49 loss_y2x=3.2874e-01 ppl_y2x=1.39 dual_loss=1.4419e+00
Validation X2Y - loss=2.0925e+00 ppl=8.11 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6540e+00 ppl=5.23 best_loss=1.0187e+00 best_ppl=2.77
Epoch 168 - |param|=9.26e+02 |g_param|=4.08e+05 loss_x2y=3.8524e-01 ppl_x2y=1.47 loss_y2x=3.1446e-01 ppl_y2x=1.37 dual_loss=1.3880e+00
Validation X2Y - loss=2.1156e+00 ppl=8.29 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6184e+00 ppl=5.04 best_loss=1.0187e+00 best_ppl=2.77
Epoch 169 - |param|=9.26e+02 |g_param|=4.03e+05 loss_x2y=3.9779e-01 ppl_x2y=1.49 loss_y2x=3.3003e-01 ppl_y2x=1.39 dual_loss=1.5513e+00
Validation X2Y - loss=2.0724e+00 ppl=7.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6393e+00 ppl=5.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 170 - |param|=9.26e+02 |g_param|=4.14e+05 loss_x2y=4.0271e-01 ppl_x2y=1.50 loss_y2x=3.2818e-01 ppl_y2x=1.39 dual_loss=1.6055e+00
Validation X2Y - loss=2.1220e+00 ppl=8.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6220e+00 ppl=5.06 best_loss=1.0187e+00 best_ppl=2.77
Epoch 171 - |param|=9.27e+02 |g_param|=3.84e+05 loss_x2y=3.6628e-01 ppl_x2y=1.44 loss_y2x=3.0459e-01 ppl_y2x=1.36 dual_loss=1.3030e+00
Validation X2Y - loss=2.0545e+00 ppl=7.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6097e+00 ppl=5.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 172 - |param|=9.27e+02 |g_param|=3.97e+05 loss_x2y=3.8383e-01 ppl_x2y=1.47 loss_y2x=3.1147e-01 ppl_y2x=1.37 dual_loss=1.4655e+00
Validation X2Y - loss=2.1035e+00 ppl=8.19 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6161e+00 ppl=5.03 best_loss=1.0187e+00 best_ppl=2.77
Epoch 173 - |param|=9.28e+02 |g_param|=3.83e+05 loss_x2y=3.7895e-01 ppl_x2y=1.46 loss_y2x=3.0707e-01 ppl_y2x=1.36 dual_loss=1.4338e+00
Validation X2Y - loss=2.1044e+00 ppl=8.20 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6488e+00 ppl=5.20 best_loss=1.0187e+00 best_ppl=2.77
Epoch 174 - |param|=9.28e+02 |g_param|=3.93e+05 loss_x2y=4.3938e-01 ppl_x2y=1.55 loss_y2x=3.4056e-01 ppl_y2x=1.41 dual_loss=1.7224e+00
Validation X2Y - loss=2.1008e+00 ppl=8.17 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5467e+00 ppl=4.70 best_loss=1.0187e+00 best_ppl=2.77
Epoch 175 - |param|=9.28e+02 |g_param|=3.95e+05 loss_x2y=3.8142e-01 ppl_x2y=1.46 loss_y2x=3.4255e-01 ppl_y2x=1.41 dual_loss=1.7498e+00
Validation X2Y - loss=2.1368e+00 ppl=8.47 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.5631e+00 ppl=4.77 best_loss=1.0187e+00 best_ppl=2.77
Epoch 176 - |param|=9.29e+02 |g_param|=4.02e+05 loss_x2y=3.8397e-01 ppl_x2y=1.47 loss_y2x=3.1158e-01 ppl_y2x=1.37 dual_loss=1.5297e+00
Validation X2Y - loss=2.1529e+00 ppl=8.61 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6382e+00 ppl=5.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 177 - |param|=9.29e+02 |g_param|=4.66e+05 loss_x2y=3.6005e-01 ppl_x2y=1.43 loss_y2x=3.0696e-01 ppl_y2x=1.36 dual_loss=1.4427e+00
Validation X2Y - loss=2.1045e+00 ppl=8.20 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6682e+00 ppl=5.30 best_loss=1.0187e+00 best_ppl=2.77
Epoch 178 - |param|=9.29e+02 |g_param|=6.24e+05 loss_x2y=4.4501e-01 ppl_x2y=1.56 loss_y2x=3.5106e-01 ppl_y2x=1.42 dual_loss=1.9061e+00
Validation X2Y - loss=2.0906e+00 ppl=8.09 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6811e+00 ppl=5.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 179 - |param|=9.30e+02 |g_param|=6.11e+05 loss_x2y=4.3928e-01 ppl_x2y=1.55 loss_y2x=3.5129e-01 ppl_y2x=1.42 dual_loss=1.9212e+00
Validation X2Y - loss=2.1396e+00 ppl=8.50 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6238e+00 ppl=5.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 180 - |param|=9.30e+02 |g_param|=6.19e+05 loss_x2y=3.7859e-01 ppl_x2y=1.46 loss_y2x=2.9939e-01 ppl_y2x=1.35 dual_loss=1.4069e+00
Validation X2Y - loss=2.1601e+00 ppl=8.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6281e+00 ppl=5.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 181 - |param|=9.30e+02 |g_param|=6.13e+05 loss_x2y=3.9472e-01 ppl_x2y=1.48 loss_y2x=3.3828e-01 ppl_y2x=1.40 dual_loss=1.8195e+00
Validation X2Y - loss=2.1656e+00 ppl=8.72 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6337e+00 ppl=5.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 182 - |param|=9.31e+02 |g_param|=6.00e+05 loss_x2y=3.6790e-01 ppl_x2y=1.44 loss_y2x=3.0311e-01 ppl_y2x=1.35 dual_loss=1.4271e+00
Validation X2Y - loss=2.1479e+00 ppl=8.57 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6557e+00 ppl=5.24 best_loss=1.0187e+00 best_ppl=2.77
Epoch 183 - |param|=9.31e+02 |g_param|=5.66e+05 loss_x2y=3.7423e-01 ppl_x2y=1.45 loss_y2x=2.9527e-01 ppl_y2x=1.34 dual_loss=1.4404e+00
Validation X2Y - loss=2.1765e+00 ppl=8.82 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6141e+00 ppl=5.02 best_loss=1.0187e+00 best_ppl=2.77
Epoch 184 - |param|=9.31e+02 |g_param|=6.05e+05 loss_x2y=3.5800e-01 ppl_x2y=1.43 loss_y2x=2.9478e-01 ppl_y2x=1.34 dual_loss=1.4281e+00
Validation X2Y - loss=2.1491e+00 ppl=8.58 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6406e+00 ppl=5.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 185 - |param|=9.32e+02 |g_param|=6.77e+05 loss_x2y=3.7157e-01 ppl_x2y=1.45 loss_y2x=2.9410e-01 ppl_y2x=1.34 dual_loss=1.4403e+00
Validation X2Y - loss=2.1294e+00 ppl=8.41 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6071e+00 ppl=4.99 best_loss=1.0187e+00 best_ppl=2.77
Epoch 186 - |param|=9.32e+02 |g_param|=7.75e+05 loss_x2y=4.0414e-01 ppl_x2y=1.50 loss_y2x=3.3525e-01 ppl_y2x=1.40 dual_loss=1.7867e+00
Validation X2Y - loss=2.1452e+00 ppl=8.54 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6441e+00 ppl=5.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 187 - |param|=9.32e+02 |g_param|=7.51e+05 loss_x2y=3.6878e-01 ppl_x2y=1.45 loss_y2x=3.0432e-01 ppl_y2x=1.36 dual_loss=1.4823e+00
Validation X2Y - loss=2.1678e+00 ppl=8.74 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6497e+00 ppl=5.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 188 - |param|=9.33e+02 |g_param|=7.66e+05 loss_x2y=3.7540e-01 ppl_x2y=1.46 loss_y2x=2.9599e-01 ppl_y2x=1.34 dual_loss=1.5180e+00
Validation X2Y - loss=2.1022e+00 ppl=8.18 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6650e+00 ppl=5.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 189 - |param|=9.33e+02 |g_param|=7.46e+05 loss_x2y=3.5741e-01 ppl_x2y=1.43 loss_y2x=2.8782e-01 ppl_y2x=1.33 dual_loss=1.4254e+00
Validation X2Y - loss=2.2132e+00 ppl=9.15 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6523e+00 ppl=5.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 190 - |param|=9.33e+02 |g_param|=7.68e+05 loss_x2y=3.8390e-01 ppl_x2y=1.47 loss_y2x=3.1544e-01 ppl_y2x=1.37 dual_loss=1.7404e+00
Validation X2Y - loss=2.1487e+00 ppl=8.57 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6613e+00 ppl=5.27 best_loss=1.0187e+00 best_ppl=2.77
Epoch 191 - |param|=9.34e+02 |g_param|=7.30e+05 loss_x2y=3.6319e-01 ppl_x2y=1.44 loss_y2x=2.9400e-01 ppl_y2x=1.34 dual_loss=1.5235e+00
Validation X2Y - loss=2.1390e+00 ppl=8.49 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6883e+00 ppl=5.41 best_loss=1.0187e+00 best_ppl=2.77
Epoch 192 - |param|=9.34e+02 |g_param|=7.46e+05 loss_x2y=3.5435e-01 ppl_x2y=1.43 loss_y2x=2.9888e-01 ppl_y2x=1.35 dual_loss=1.5515e+00
Validation X2Y - loss=2.1102e+00 ppl=8.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6603e+00 ppl=5.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 193 - |param|=9.34e+02 |g_param|=7.17e+05 loss_x2y=3.5676e-01 ppl_x2y=1.43 loss_y2x=2.9750e-01 ppl_y2x=1.35 dual_loss=1.5417e+00
Validation X2Y - loss=2.1308e+00 ppl=8.42 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6392e+00 ppl=5.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 194 - |param|=9.35e+02 |g_param|=7.89e+05 loss_x2y=3.7196e-01 ppl_x2y=1.45 loss_y2x=3.0102e-01 ppl_y2x=1.35 dual_loss=1.5765e+00
Validation X2Y - loss=2.1392e+00 ppl=8.49 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6543e+00 ppl=5.23 best_loss=1.0187e+00 best_ppl=2.77
Epoch 195 - |param|=9.35e+02 |g_param|=7.31e+05 loss_x2y=3.7575e-01 ppl_x2y=1.46 loss_y2x=3.1173e-01 ppl_y2x=1.37 dual_loss=1.7459e+00
Validation X2Y - loss=2.1965e+00 ppl=8.99 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6602e+00 ppl=5.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 196 - |param|=9.35e+02 |g_param|=7.65e+05 loss_x2y=3.8867e-01 ppl_x2y=1.48 loss_y2x=3.1258e-01 ppl_y2x=1.37 dual_loss=1.7296e+00
Validation X2Y - loss=2.2006e+00 ppl=9.03 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6578e+00 ppl=5.25 best_loss=1.0187e+00 best_ppl=2.77
Epoch 197 - |param|=9.35e+02 |g_param|=7.19e+05 loss_x2y=3.6446e-01 ppl_x2y=1.44 loss_y2x=2.8949e-01 ppl_y2x=1.34 dual_loss=1.4819e+00
Validation X2Y - loss=2.1600e+00 ppl=8.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6769e+00 ppl=5.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 198 - |param|=9.36e+02 |g_param|=7.94e+05 loss_x2y=3.6905e-01 ppl_x2y=1.45 loss_y2x=3.2883e-01 ppl_y2x=1.39 dual_loss=1.8350e+00
Validation X2Y - loss=2.1578e+00 ppl=8.65 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6605e+00 ppl=5.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 199 - |param|=9.36e+02 |g_param|=6.67e+05 loss_x2y=3.5491e-01 ppl_x2y=1.43 loss_y2x=2.9190e-01 ppl_y2x=1.34 dual_loss=1.4421e+00
Validation X2Y - loss=2.1609e+00 ppl=8.68 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6415e+00 ppl=5.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 200 - |param|=9.36e+02 |g_param|=5.99e+05 loss_x2y=3.4419e-01 ppl_x2y=1.41 loss_y2x=2.9330e-01 ppl_y2x=1.34 dual_loss=1.4875e+00
Validation X2Y - loss=2.1678e+00 ppl=8.74 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6445e+00 ppl=5.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 201 - |param|=9.37e+02 |g_param|=5.80e+05 loss_x2y=3.7073e-01 ppl_x2y=1.45 loss_y2x=2.9630e-01 ppl_y2x=1.34 dual_loss=1.6073e+00
Validation X2Y - loss=2.1434e+00 ppl=8.53 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6056e+00 ppl=4.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 202 - |param|=9.37e+02 |g_param|=5.89e+05 loss_x2y=3.4920e-01 ppl_x2y=1.42 loss_y2x=2.8947e-01 ppl_y2x=1.34 dual_loss=1.5473e+00
Validation X2Y - loss=2.1284e+00 ppl=8.40 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6068e+00 ppl=4.99 best_loss=1.0187e+00 best_ppl=2.77
Epoch 203 - |param|=9.37e+02 |g_param|=5.61e+05 loss_x2y=3.5605e-01 ppl_x2y=1.43 loss_y2x=2.9592e-01 ppl_y2x=1.34 dual_loss=1.4987e+00
Validation X2Y - loss=2.1680e+00 ppl=8.74 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6377e+00 ppl=5.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 204 - |param|=9.38e+02 |g_param|=6.05e+05 loss_x2y=3.6243e-01 ppl_x2y=1.44 loss_y2x=2.9671e-01 ppl_y2x=1.35 dual_loss=1.5976e+00
Validation X2Y - loss=2.1359e+00 ppl=8.46 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6274e+00 ppl=5.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 205 - |param|=9.38e+02 |g_param|=5.74e+05 loss_x2y=3.5571e-01 ppl_x2y=1.43 loss_y2x=2.8886e-01 ppl_y2x=1.33 dual_loss=1.5225e+00
Validation X2Y - loss=2.1219e+00 ppl=8.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6066e+00 ppl=4.99 best_loss=1.0187e+00 best_ppl=2.77
Epoch 206 - |param|=9.38e+02 |g_param|=5.90e+05 loss_x2y=3.5443e-01 ppl_x2y=1.43 loss_y2x=2.8372e-01 ppl_y2x=1.33 dual_loss=1.6439e+00
Validation X2Y - loss=2.1266e+00 ppl=8.39 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6101e+00 ppl=5.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 207 - |param|=9.39e+02 |g_param|=5.72e+05 loss_x2y=3.7543e-01 ppl_x2y=1.46 loss_y2x=2.9394e-01 ppl_y2x=1.34 dual_loss=1.5980e+00
Validation X2Y - loss=2.1234e+00 ppl=8.36 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6384e+00 ppl=5.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 208 - |param|=9.39e+02 |g_param|=5.86e+05 loss_x2y=3.3391e-01 ppl_x2y=1.40 loss_y2x=2.8686e-01 ppl_y2x=1.33 dual_loss=1.5443e+00
Validation X2Y - loss=2.1433e+00 ppl=8.53 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6379e+00 ppl=5.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 209 - |param|=9.39e+02 |g_param|=5.51e+05 loss_x2y=3.3752e-01 ppl_x2y=1.40 loss_y2x=2.6868e-01 ppl_y2x=1.31 dual_loss=1.4430e+00
Validation X2Y - loss=2.1178e+00 ppl=8.31 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7042e+00 ppl=5.50 best_loss=1.0187e+00 best_ppl=2.77
Epoch 210 - |param|=9.40e+02 |g_param|=5.69e+05 loss_x2y=3.5579e-01 ppl_x2y=1.43 loss_y2x=2.8561e-01 ppl_y2x=1.33 dual_loss=1.6015e+00
Validation X2Y - loss=2.1626e+00 ppl=8.69 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6809e+00 ppl=5.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 211 - |param|=9.40e+02 |g_param|=5.45e+05 loss_x2y=3.3638e-01 ppl_x2y=1.40 loss_y2x=2.7398e-01 ppl_y2x=1.32 dual_loss=1.4880e+00
Validation X2Y - loss=2.1568e+00 ppl=8.64 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6806e+00 ppl=5.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 212 - |param|=9.40e+02 |g_param|=5.83e+05 loss_x2y=3.3511e-01 ppl_x2y=1.40 loss_y2x=2.8510e-01 ppl_y2x=1.33 dual_loss=1.5275e+00
Validation X2Y - loss=2.1628e+00 ppl=8.70 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6661e+00 ppl=5.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 213 - |param|=9.41e+02 |g_param|=5.80e+05 loss_x2y=3.4923e-01 ppl_x2y=1.42 loss_y2x=2.8018e-01 ppl_y2x=1.32 dual_loss=1.5553e+00
Validation X2Y - loss=2.2162e+00 ppl=9.17 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6948e+00 ppl=5.45 best_loss=1.0187e+00 best_ppl=2.77
Epoch 214 - |param|=9.41e+02 |g_param|=5.87e+05 loss_x2y=3.4220e-01 ppl_x2y=1.41 loss_y2x=2.8388e-01 ppl_y2x=1.33 dual_loss=1.5699e+00
Validation X2Y - loss=2.2964e+00 ppl=9.94 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6602e+00 ppl=5.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 215 - |param|=9.41e+02 |g_param|=5.41e+05 loss_x2y=3.3977e-01 ppl_x2y=1.40 loss_y2x=2.8276e-01 ppl_y2x=1.33 dual_loss=1.5485e+00
Validation X2Y - loss=2.2142e+00 ppl=9.15 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6969e+00 ppl=5.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 216 - |param|=9.42e+02 |g_param|=5.64e+05 loss_x2y=3.4321e-01 ppl_x2y=1.41 loss_y2x=2.7948e-01 ppl_y2x=1.32 dual_loss=1.5570e+00
Validation X2Y - loss=2.1334e+00 ppl=8.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6963e+00 ppl=5.45 best_loss=1.0187e+00 best_ppl=2.77
Epoch 217 - |param|=9.42e+02 |g_param|=5.57e+05 loss_x2y=3.3117e-01 ppl_x2y=1.39 loss_y2x=2.7051e-01 ppl_y2x=1.31 dual_loss=1.4982e+00
Validation X2Y - loss=2.1845e+00 ppl=8.89 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6280e+00 ppl=5.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 218 - |param|=9.42e+02 |g_param|=5.82e+05 loss_x2y=3.5241e-01 ppl_x2y=1.42 loss_y2x=2.8658e-01 ppl_y2x=1.33 dual_loss=1.6958e+00
Validation X2Y - loss=2.1800e+00 ppl=8.85 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6633e+00 ppl=5.28 best_loss=1.0187e+00 best_ppl=2.77
Epoch 219 - |param|=9.43e+02 |g_param|=5.43e+05 loss_x2y=3.2882e-01 ppl_x2y=1.39 loss_y2x=2.6944e-01 ppl_y2x=1.31 dual_loss=1.4508e+00
Validation X2Y - loss=2.1328e+00 ppl=8.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6401e+00 ppl=5.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 220 - |param|=9.43e+02 |g_param|=5.64e+05 loss_x2y=3.4887e-01 ppl_x2y=1.42 loss_y2x=2.8496e-01 ppl_y2x=1.33 dual_loss=1.5881e+00
Validation X2Y - loss=2.1710e+00 ppl=8.77 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6591e+00 ppl=5.25 best_loss=1.0187e+00 best_ppl=2.77
Epoch 221 - |param|=9.43e+02 |g_param|=5.34e+05 loss_x2y=3.3375e-01 ppl_x2y=1.40 loss_y2x=2.7321e-01 ppl_y2x=1.31 dual_loss=1.5381e+00
Validation X2Y - loss=2.1726e+00 ppl=8.78 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6088e+00 ppl=5.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 222 - |param|=9.44e+02 |g_param|=5.67e+05 loss_x2y=3.5454e-01 ppl_x2y=1.43 loss_y2x=2.8156e-01 ppl_y2x=1.33 dual_loss=1.6464e+00
Validation X2Y - loss=2.2099e+00 ppl=9.11 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6835e+00 ppl=5.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 223 - |param|=9.44e+02 |g_param|=5.32e+05 loss_x2y=3.5617e-01 ppl_x2y=1.43 loss_y2x=2.9409e-01 ppl_y2x=1.34 dual_loss=1.7286e+00
Validation X2Y - loss=2.2001e+00 ppl=9.03 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6237e+00 ppl=5.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 224 - |param|=9.44e+02 |g_param|=5.65e+05 loss_x2y=3.4931e-01 ppl_x2y=1.42 loss_y2x=2.7835e-01 ppl_y2x=1.32 dual_loss=1.6009e+00
Validation X2Y - loss=2.1858e+00 ppl=8.90 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6202e+00 ppl=5.05 best_loss=1.0187e+00 best_ppl=2.77
Epoch 225 - |param|=9.44e+02 |g_param|=5.38e+05 loss_x2y=3.2840e-01 ppl_x2y=1.39 loss_y2x=2.7715e-01 ppl_y2x=1.32 dual_loss=1.5654e+00
Validation X2Y - loss=2.2189e+00 ppl=9.20 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6746e+00 ppl=5.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 226 - |param|=9.45e+02 |g_param|=5.64e+05 loss_x2y=3.6025e-01 ppl_x2y=1.43 loss_y2x=2.9406e-01 ppl_y2x=1.34 dual_loss=1.6903e+00
Validation X2Y - loss=2.1875e+00 ppl=8.91 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6813e+00 ppl=5.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 227 - |param|=9.45e+02 |g_param|=5.53e+05 loss_x2y=3.4666e-01 ppl_x2y=1.41 loss_y2x=2.9375e-01 ppl_y2x=1.34 dual_loss=1.7508e+00
Validation X2Y - loss=2.2313e+00 ppl=9.31 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6766e+00 ppl=5.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 228 - |param|=9.45e+02 |g_param|=5.56e+05 loss_x2y=3.7137e-01 ppl_x2y=1.45 loss_y2x=2.8990e-01 ppl_y2x=1.34 dual_loss=1.7246e+00
Validation X2Y - loss=2.2778e+00 ppl=9.75 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6912e+00 ppl=5.43 best_loss=1.0187e+00 best_ppl=2.77
Epoch 229 - |param|=9.46e+02 |g_param|=5.38e+05 loss_x2y=3.6367e-01 ppl_x2y=1.44 loss_y2x=2.9463e-01 ppl_y2x=1.34 dual_loss=1.7550e+00
Validation X2Y - loss=2.2714e+00 ppl=9.69 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7118e+00 ppl=5.54 best_loss=1.0187e+00 best_ppl=2.77
Epoch 230 - |param|=9.46e+02 |g_param|=5.42e+05 loss_x2y=3.3623e-01 ppl_x2y=1.40 loss_y2x=2.6756e-01 ppl_y2x=1.31 dual_loss=1.5812e+00
Validation X2Y - loss=2.2689e+00 ppl=9.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6704e+00 ppl=5.31 best_loss=1.0187e+00 best_ppl=2.77
Epoch 231 - |param|=9.46e+02 |g_param|=5.36e+05 loss_x2y=3.6100e-01 ppl_x2y=1.43 loss_y2x=2.8425e-01 ppl_y2x=1.33 dual_loss=1.7327e+00
Validation X2Y - loss=2.2354e+00 ppl=9.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6596e+00 ppl=5.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 232 - |param|=9.47e+02 |g_param|=7.15e+05 loss_x2y=3.5455e-01 ppl_x2y=1.43 loss_y2x=2.8159e-01 ppl_y2x=1.33 dual_loss=1.6831e+00
Validation X2Y - loss=2.2997e+00 ppl=9.97 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6583e+00 ppl=5.25 best_loss=1.0187e+00 best_ppl=2.77
Epoch 233 - |param|=9.47e+02 |g_param|=6.68e+05 loss_x2y=3.3713e-01 ppl_x2y=1.40 loss_y2x=2.6969e-01 ppl_y2x=1.31 dual_loss=1.5492e+00
Validation X2Y - loss=2.2824e+00 ppl=9.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6224e+00 ppl=5.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 234 - |param|=9.47e+02 |g_param|=6.91e+05 loss_x2y=3.3439e-01 ppl_x2y=1.40 loss_y2x=3.0582e-01 ppl_y2x=1.36 dual_loss=1.9398e+00
Validation X2Y - loss=2.2225e+00 ppl=9.23 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6454e+00 ppl=5.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 235 - |param|=9.48e+02 |g_param|=6.71e+05 loss_x2y=3.3384e-01 ppl_x2y=1.40 loss_y2x=2.7824e-01 ppl_y2x=1.32 dual_loss=1.6212e+00
Validation X2Y - loss=2.1935e+00 ppl=8.97 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6095e+00 ppl=5.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 236 - |param|=9.48e+02 |g_param|=6.94e+05 loss_x2y=3.5152e-01 ppl_x2y=1.42 loss_y2x=3.0212e-01 ppl_y2x=1.35 dual_loss=2.0078e+00
Validation X2Y - loss=2.2287e+00 ppl=9.29 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6710e+00 ppl=5.32 best_loss=1.0187e+00 best_ppl=2.77
Epoch 237 - |param|=9.48e+02 |g_param|=6.86e+05 loss_x2y=3.4601e-01 ppl_x2y=1.41 loss_y2x=2.8110e-01 ppl_y2x=1.32 dual_loss=1.7067e+00
Validation X2Y - loss=2.3119e+00 ppl=10.09 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.6869e+00 ppl=5.40 best_loss=1.0187e+00 best_ppl=2.77
Epoch 238 - |param|=9.49e+02 |g_param|=6.85e+05 loss_x2y=3.1768e-01 ppl_x2y=1.37 loss_y2x=2.6427e-01 ppl_y2x=1.30 dual_loss=1.5140e+00
Validation X2Y - loss=2.2143e+00 ppl=9.16 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6909e+00 ppl=5.42 best_loss=1.0187e+00 best_ppl=2.77
Epoch 239 - |param|=9.49e+02 |g_param|=6.76e+05 loss_x2y=3.9052e-01 ppl_x2y=1.48 loss_y2x=3.0301e-01 ppl_y2x=1.35 dual_loss=2.0147e+00
Validation X2Y - loss=2.2719e+00 ppl=9.70 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6770e+00 ppl=5.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 240 - |param|=9.49e+02 |g_param|=7.00e+05 loss_x2y=3.3858e-01 ppl_x2y=1.40 loss_y2x=2.7401e-01 ppl_y2x=1.32 dual_loss=1.6604e+00
Validation X2Y - loss=2.2913e+00 ppl=9.89 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7201e+00 ppl=5.59 best_loss=1.0187e+00 best_ppl=2.77
Epoch 241 - |param|=9.49e+02 |g_param|=6.69e+05 loss_x2y=3.5599e-01 ppl_x2y=1.43 loss_y2x=2.8876e-01 ppl_y2x=1.33 dual_loss=1.8724e+00
Validation X2Y - loss=2.2869e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7218e+00 ppl=5.59 best_loss=1.0187e+00 best_ppl=2.77
Epoch 242 - |param|=9.50e+02 |g_param|=6.78e+05 loss_x2y=3.1674e-01 ppl_x2y=1.37 loss_y2x=2.6723e-01 ppl_y2x=1.31 dual_loss=1.5585e+00
Validation X2Y - loss=2.2861e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6837e+00 ppl=5.39 best_loss=1.0187e+00 best_ppl=2.77
Epoch 243 - |param|=9.50e+02 |g_param|=6.53e+05 loss_x2y=3.2794e-01 ppl_x2y=1.39 loss_y2x=2.6193e-01 ppl_y2x=1.30 dual_loss=1.5899e+00
Validation X2Y - loss=2.2573e+00 ppl=9.56 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7091e+00 ppl=5.52 best_loss=1.0187e+00 best_ppl=2.77
Epoch 244 - |param|=9.50e+02 |g_param|=6.94e+05 loss_x2y=3.4022e-01 ppl_x2y=1.41 loss_y2x=2.9333e-01 ppl_y2x=1.34 dual_loss=1.9022e+00
Validation X2Y - loss=2.2419e+00 ppl=9.41 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7309e+00 ppl=5.65 best_loss=1.0187e+00 best_ppl=2.77
Epoch 245 - |param|=9.51e+02 |g_param|=6.50e+05 loss_x2y=3.2331e-01 ppl_x2y=1.38 loss_y2x=2.5715e-01 ppl_y2x=1.29 dual_loss=1.5270e+00
Validation X2Y - loss=2.2629e+00 ppl=9.61 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7420e+00 ppl=5.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 246 - |param|=9.51e+02 |g_param|=6.75e+05 loss_x2y=3.2314e-01 ppl_x2y=1.38 loss_y2x=2.7187e-01 ppl_y2x=1.31 dual_loss=1.6929e+00
Validation X2Y - loss=2.1992e+00 ppl=9.02 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7297e+00 ppl=5.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 247 - |param|=9.51e+02 |g_param|=6.45e+05 loss_x2y=3.2578e-01 ppl_x2y=1.39 loss_y2x=2.7712e-01 ppl_y2x=1.32 dual_loss=1.6908e+00
Validation X2Y - loss=2.2586e+00 ppl=9.57 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8099e+00 ppl=6.11 best_loss=1.0187e+00 best_ppl=2.77
Epoch 248 - |param|=9.52e+02 |g_param|=6.78e+05 loss_x2y=3.2426e-01 ppl_x2y=1.38 loss_y2x=2.7641e-01 ppl_y2x=1.32 dual_loss=1.7372e+00
Validation X2Y - loss=2.1899e+00 ppl=8.93 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7663e+00 ppl=5.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 249 - |param|=9.52e+02 |g_param|=6.56e+05 loss_x2y=3.6972e-01 ppl_x2y=1.45 loss_y2x=2.9384e-01 ppl_y2x=1.34 dual_loss=1.9760e+00
Validation X2Y - loss=2.1827e+00 ppl=8.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7904e+00 ppl=5.99 best_loss=1.0187e+00 best_ppl=2.77
Epoch 250 - |param|=9.52e+02 |g_param|=8.25e+05 loss_x2y=3.5165e-01 ppl_x2y=1.42 loss_y2x=3.0218e-01 ppl_y2x=1.35 dual_loss=2.0376e+00
Validation X2Y - loss=2.1861e+00 ppl=8.90 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7574e+00 ppl=5.80 best_loss=1.0187e+00 best_ppl=2.77
Epoch 251 - |param|=9.53e+02 |g_param|=7.32e+05 loss_x2y=3.7950e-01 ppl_x2y=1.46 loss_y2x=3.0008e-01 ppl_y2x=1.35 dual_loss=2.0352e+00
Validation X2Y - loss=2.2325e+00 ppl=9.32 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6979e+00 ppl=5.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 252 - |param|=9.53e+02 |g_param|=6.62e+05 loss_x2y=3.2914e-01 ppl_x2y=1.39 loss_y2x=2.6805e-01 ppl_y2x=1.31 dual_loss=1.6217e+00
Validation X2Y - loss=2.2223e+00 ppl=9.23 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7167e+00 ppl=5.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 253 - |param|=9.53e+02 |g_param|=6.51e+05 loss_x2y=3.1497e-01 ppl_x2y=1.37 loss_y2x=2.6070e-01 ppl_y2x=1.30 dual_loss=1.5645e+00
Validation X2Y - loss=2.1872e+00 ppl=8.91 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7429e+00 ppl=5.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 254 - |param|=9.53e+02 |g_param|=6.67e+05 loss_x2y=3.3589e-01 ppl_x2y=1.40 loss_y2x=2.7700e-01 ppl_y2x=1.32 dual_loss=1.8187e+00
Validation X2Y - loss=2.2293e+00 ppl=9.29 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7422e+00 ppl=5.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 255 - |param|=9.54e+02 |g_param|=6.43e+05 loss_x2y=3.1119e-01 ppl_x2y=1.37 loss_y2x=2.6838e-01 ppl_y2x=1.31 dual_loss=1.6320e+00
Validation X2Y - loss=2.2396e+00 ppl=9.39 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7544e+00 ppl=5.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 256 - |param|=9.54e+02 |g_param|=6.48e+05 loss_x2y=3.3870e-01 ppl_x2y=1.40 loss_y2x=2.6494e-01 ppl_y2x=1.30 dual_loss=1.7241e+00
Validation X2Y - loss=2.2356e+00 ppl=9.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7997e+00 ppl=6.05 best_loss=1.0187e+00 best_ppl=2.77
Epoch 257 - |param|=9.54e+02 |g_param|=6.47e+05 loss_x2y=3.2399e-01 ppl_x2y=1.38 loss_y2x=2.7490e-01 ppl_y2x=1.32 dual_loss=1.7002e+00
Validation X2Y - loss=2.1782e+00 ppl=8.83 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7641e+00 ppl=5.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 258 - |param|=9.55e+02 |g_param|=6.71e+05 loss_x2y=3.9063e-01 ppl_x2y=1.48 loss_y2x=3.1369e-01 ppl_y2x=1.37 dual_loss=2.2765e+00
Validation X2Y - loss=2.2344e+00 ppl=9.34 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7401e+00 ppl=5.70 best_loss=1.0187e+00 best_ppl=2.77
Epoch 259 - |param|=9.55e+02 |g_param|=6.32e+05 loss_x2y=3.4035e-01 ppl_x2y=1.41 loss_y2x=2.6811e-01 ppl_y2x=1.31 dual_loss=1.8264e+00
Validation X2Y - loss=2.2483e+00 ppl=9.47 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7312e+00 ppl=5.65 best_loss=1.0187e+00 best_ppl=2.77
Epoch 260 - |param|=9.55e+02 |g_param|=6.56e+05 loss_x2y=3.2236e-01 ppl_x2y=1.38 loss_y2x=2.7019e-01 ppl_y2x=1.31 dual_loss=1.7372e+00
Validation X2Y - loss=2.3288e+00 ppl=10.27 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.6971e+00 ppl=5.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 261 - |param|=9.56e+02 |g_param|=6.38e+05 loss_x2y=3.3648e-01 ppl_x2y=1.40 loss_y2x=2.7657e-01 ppl_y2x=1.32 dual_loss=1.7623e+00
Validation X2Y - loss=2.2556e+00 ppl=9.54 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6438e+00 ppl=5.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 262 - |param|=9.56e+02 |g_param|=6.82e+05 loss_x2y=3.6639e-01 ppl_x2y=1.44 loss_y2x=3.4133e-01 ppl_y2x=1.41 dual_loss=2.7232e+00
Validation X2Y - loss=2.2279e+00 ppl=9.28 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7181e+00 ppl=5.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 263 - |param|=9.56e+02 |g_param|=6.20e+05 loss_x2y=3.1215e-01 ppl_x2y=1.37 loss_y2x=2.5870e-01 ppl_y2x=1.30 dual_loss=1.6117e+00
Validation X2Y - loss=2.3010e+00 ppl=9.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6822e+00 ppl=5.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 264 - |param|=9.56e+02 |g_param|=7.26e+05 loss_x2y=3.1208e-01 ppl_x2y=1.37 loss_y2x=2.5472e-01 ppl_y2x=1.29 dual_loss=1.6075e+00
Validation X2Y - loss=2.2115e+00 ppl=9.13 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7313e+00 ppl=5.65 best_loss=1.0187e+00 best_ppl=2.77
Epoch 265 - |param|=9.57e+02 |g_param|=6.93e+05 loss_x2y=3.5042e-01 ppl_x2y=1.42 loss_y2x=2.9915e-01 ppl_y2x=1.35 dual_loss=2.0614e+00
Validation X2Y - loss=2.2055e+00 ppl=9.08 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7035e+00 ppl=5.49 best_loss=1.0187e+00 best_ppl=2.77
Epoch 266 - |param|=9.57e+02 |g_param|=6.55e+05 loss_x2y=3.5052e-01 ppl_x2y=1.42 loss_y2x=2.7704e-01 ppl_y2x=1.32 dual_loss=1.8580e+00
Validation X2Y - loss=2.2666e+00 ppl=9.65 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6694e+00 ppl=5.31 best_loss=1.0187e+00 best_ppl=2.77
Epoch 267 - |param|=9.57e+02 |g_param|=6.34e+05 loss_x2y=3.2773e-01 ppl_x2y=1.39 loss_y2x=2.6121e-01 ppl_y2x=1.30 dual_loss=1.7191e+00
Validation X2Y - loss=2.3479e+00 ppl=10.46 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7355e+00 ppl=5.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 268 - |param|=9.58e+02 |g_param|=6.32e+05 loss_x2y=3.0629e-01 ppl_x2y=1.36 loss_y2x=2.6081e-01 ppl_y2x=1.30 dual_loss=1.6514e+00
Validation X2Y - loss=2.3024e+00 ppl=10.00 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7072e+00 ppl=5.51 best_loss=1.0187e+00 best_ppl=2.77
Epoch 269 - |param|=9.58e+02 |g_param|=6.23e+05 loss_x2y=3.1134e-01 ppl_x2y=1.37 loss_y2x=2.5278e-01 ppl_y2x=1.29 dual_loss=1.6282e+00
Validation X2Y - loss=2.3566e+00 ppl=10.56 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7628e+00 ppl=5.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 270 - |param|=9.58e+02 |g_param|=6.43e+05 loss_x2y=3.0862e-01 ppl_x2y=1.36 loss_y2x=2.6493e-01 ppl_y2x=1.30 dual_loss=1.7004e+00
Validation X2Y - loss=2.3195e+00 ppl=10.17 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7217e+00 ppl=5.59 best_loss=1.0187e+00 best_ppl=2.77
Epoch 271 - |param|=9.59e+02 |g_param|=6.37e+05 loss_x2y=3.2902e-01 ppl_x2y=1.39 loss_y2x=2.6654e-01 ppl_y2x=1.31 dual_loss=1.7244e+00
Validation X2Y - loss=2.3456e+00 ppl=10.44 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7240e+00 ppl=5.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 272 - |param|=9.59e+02 |g_param|=6.26e+05 loss_x2y=3.2792e-01 ppl_x2y=1.39 loss_y2x=2.6196e-01 ppl_y2x=1.30 dual_loss=1.7202e+00
Validation X2Y - loss=2.3655e+00 ppl=10.65 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7476e+00 ppl=5.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 273 - |param|=9.59e+02 |g_param|=6.18e+05 loss_x2y=3.3471e-01 ppl_x2y=1.40 loss_y2x=2.8045e-01 ppl_y2x=1.32 dual_loss=1.9229e+00
Validation X2Y - loss=2.3185e+00 ppl=10.16 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7031e+00 ppl=5.49 best_loss=1.0187e+00 best_ppl=2.77
Epoch 274 - |param|=9.59e+02 |g_param|=6.31e+05 loss_x2y=3.2527e-01 ppl_x2y=1.38 loss_y2x=2.7124e-01 ppl_y2x=1.31 dual_loss=1.7823e+00
Validation X2Y - loss=2.3293e+00 ppl=10.27 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.6903e+00 ppl=5.42 best_loss=1.0187e+00 best_ppl=2.77
Epoch 275 - |param|=9.60e+02 |g_param|=6.09e+05 loss_x2y=3.7399e-01 ppl_x2y=1.45 loss_y2x=3.0004e-01 ppl_y2x=1.35 dual_loss=2.0579e+00
Validation X2Y - loss=2.2714e+00 ppl=9.69 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7232e+00 ppl=5.60 best_loss=1.0187e+00 best_ppl=2.77
Epoch 276 - |param|=9.60e+02 |g_param|=6.26e+05 loss_x2y=3.0137e-01 ppl_x2y=1.35 loss_y2x=2.5939e-01 ppl_y2x=1.30 dual_loss=1.6583e+00
Validation X2Y - loss=2.2985e+00 ppl=9.96 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.6998e+00 ppl=5.47 best_loss=1.0187e+00 best_ppl=2.77
Epoch 277 - |param|=9.60e+02 |g_param|=6.03e+05 loss_x2y=3.1657e-01 ppl_x2y=1.37 loss_y2x=2.6442e-01 ppl_y2x=1.30 dual_loss=1.8221e+00
Validation X2Y - loss=2.3110e+00 ppl=10.08 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.6951e+00 ppl=5.45 best_loss=1.0187e+00 best_ppl=2.77
Epoch 278 - |param|=9.61e+02 |g_param|=6.28e+05 loss_x2y=3.0627e-01 ppl_x2y=1.36 loss_y2x=2.4701e-01 ppl_y2x=1.28 dual_loss=1.6041e+00
Validation X2Y - loss=2.2863e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7198e+00 ppl=5.58 best_loss=1.0187e+00 best_ppl=2.77
Epoch 279 - |param|=9.61e+02 |g_param|=6.06e+05 loss_x2y=3.4588e-01 ppl_x2y=1.41 loss_y2x=2.8438e-01 ppl_y2x=1.33 dual_loss=1.9580e+00
Validation X2Y - loss=2.2656e+00 ppl=9.64 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7267e+00 ppl=5.62 best_loss=1.0187e+00 best_ppl=2.77
Epoch 280 - |param|=9.61e+02 |g_param|=6.37e+05 loss_x2y=3.2787e-01 ppl_x2y=1.39 loss_y2x=2.7306e-01 ppl_y2x=1.31 dual_loss=1.7954e+00
Validation X2Y - loss=2.2564e+00 ppl=9.55 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7628e+00 ppl=5.83 best_loss=1.0187e+00 best_ppl=2.77
Epoch 281 - |param|=9.61e+02 |g_param|=6.03e+05 loss_x2y=3.2647e-01 ppl_x2y=1.39 loss_y2x=2.7999e-01 ppl_y2x=1.32 dual_loss=1.9308e+00
Validation X2Y - loss=2.3043e+00 ppl=10.02 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7761e+00 ppl=5.91 best_loss=1.0187e+00 best_ppl=2.77
Epoch 282 - |param|=9.62e+02 |g_param|=6.43e+05 loss_x2y=3.6584e-01 ppl_x2y=1.44 loss_y2x=3.0070e-01 ppl_y2x=1.35 dual_loss=2.1777e+00
Validation X2Y - loss=2.2615e+00 ppl=9.60 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7748e+00 ppl=5.90 best_loss=1.0187e+00 best_ppl=2.77
Epoch 283 - |param|=9.62e+02 |g_param|=6.09e+05 loss_x2y=3.0333e-01 ppl_x2y=1.35 loss_y2x=2.5291e-01 ppl_y2x=1.29 dual_loss=1.7059e+00
Validation X2Y - loss=2.2994e+00 ppl=9.97 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7097e+00 ppl=5.53 best_loss=1.0187e+00 best_ppl=2.77
Epoch 284 - |param|=9.62e+02 |g_param|=9.68e+05 loss_x2y=3.0030e-01 ppl_x2y=1.35 loss_y2x=2.5257e-01 ppl_y2x=1.29 dual_loss=1.6445e+00
Validation X2Y - loss=2.2840e+00 ppl=9.82 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7861e+00 ppl=5.97 best_loss=1.0187e+00 best_ppl=2.77
Epoch 285 - |param|=9.63e+02 |g_param|=9.52e+05 loss_x2y=3.1311e-01 ppl_x2y=1.37 loss_y2x=2.5857e-01 ppl_y2x=1.30 dual_loss=1.7378e+00
Validation X2Y - loss=2.2752e+00 ppl=9.73 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7557e+00 ppl=5.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 286 - |param|=9.63e+02 |g_param|=7.83e+05 loss_x2y=3.5605e-01 ppl_x2y=1.43 loss_y2x=3.0294e-01 ppl_y2x=1.35 dual_loss=2.1696e+00
Validation X2Y - loss=2.3158e+00 ppl=10.13 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7215e+00 ppl=5.59 best_loss=1.0187e+00 best_ppl=2.77
Epoch 287 - |param|=9.63e+02 |g_param|=5.94e+05 loss_x2y=3.0043e-01 ppl_x2y=1.35 loss_y2x=2.5725e-01 ppl_y2x=1.29 dual_loss=1.7066e+00
Validation X2Y - loss=2.2801e+00 ppl=9.78 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7406e+00 ppl=5.70 best_loss=1.0187e+00 best_ppl=2.77
Epoch 288 - |param|=9.64e+02 |g_param|=6.37e+05 loss_x2y=3.3082e-01 ppl_x2y=1.39 loss_y2x=2.8522e-01 ppl_y2x=1.33 dual_loss=1.9937e+00
Validation X2Y - loss=2.2342e+00 ppl=9.34 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7533e+00 ppl=5.77 best_loss=1.0187e+00 best_ppl=2.77
Epoch 289 - |param|=9.64e+02 |g_param|=5.96e+05 loss_x2y=3.3695e-01 ppl_x2y=1.40 loss_y2x=2.7018e-01 ppl_y2x=1.31 dual_loss=1.9714e+00
Validation X2Y - loss=2.2855e+00 ppl=9.83 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7277e+00 ppl=5.63 best_loss=1.0187e+00 best_ppl=2.77
Epoch 290 - |param|=9.64e+02 |g_param|=6.08e+05 loss_x2y=3.0046e-01 ppl_x2y=1.35 loss_y2x=2.5344e-01 ppl_y2x=1.29 dual_loss=1.7318e+00
Validation X2Y - loss=2.2867e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7250e+00 ppl=5.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 291 - |param|=9.64e+02 |g_param|=6.01e+05 loss_x2y=3.3082e-01 ppl_x2y=1.39 loss_y2x=2.7248e-01 ppl_y2x=1.31 dual_loss=1.8652e+00
Validation X2Y - loss=2.2708e+00 ppl=9.69 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7276e+00 ppl=5.63 best_loss=1.0187e+00 best_ppl=2.77
Epoch 292 - |param|=9.65e+02 |g_param|=5.95e+05 loss_x2y=2.8184e-01 ppl_x2y=1.33 loss_y2x=2.3990e-01 ppl_y2x=1.27 dual_loss=1.5600e+00
Validation X2Y - loss=2.2458e+00 ppl=9.45 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7171e+00 ppl=5.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 293 - |param|=9.65e+02 |g_param|=6.05e+05 loss_x2y=3.0604e-01 ppl_x2y=1.36 loss_y2x=2.5066e-01 ppl_y2x=1.28 dual_loss=1.7638e+00
Validation X2Y - loss=2.2737e+00 ppl=9.72 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7246e+00 ppl=5.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 294 - |param|=9.65e+02 |g_param|=6.02e+05 loss_x2y=2.9031e-01 ppl_x2y=1.34 loss_y2x=2.4468e-01 ppl_y2x=1.28 dual_loss=1.6329e+00
Validation X2Y - loss=2.2340e+00 ppl=9.34 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7435e+00 ppl=5.72 best_loss=1.0187e+00 best_ppl=2.77
Epoch 295 - |param|=9.66e+02 |g_param|=5.85e+05 loss_x2y=3.1508e-01 ppl_x2y=1.37 loss_y2x=2.5567e-01 ppl_y2x=1.29 dual_loss=1.7824e+00
Validation X2Y - loss=2.2136e+00 ppl=9.15 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7378e+00 ppl=5.69 best_loss=1.0187e+00 best_ppl=2.77
Epoch 296 - |param|=9.66e+02 |g_param|=6.17e+05 loss_x2y=3.0148e-01 ppl_x2y=1.35 loss_y2x=2.5529e-01 ppl_y2x=1.29 dual_loss=1.7726e+00
Validation X2Y - loss=2.2104e+00 ppl=9.12 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7142e+00 ppl=5.55 best_loss=1.0187e+00 best_ppl=2.77
Epoch 297 - |param|=9.66e+02 |g_param|=7.04e+05 loss_x2y=3.0307e-01 ppl_x2y=1.35 loss_y2x=2.5228e-01 ppl_y2x=1.29 dual_loss=1.7188e+00
Validation X2Y - loss=2.2249e+00 ppl=9.25 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7694e+00 ppl=5.87 best_loss=1.0187e+00 best_ppl=2.77
Epoch 298 - |param|=9.66e+02 |g_param|=6.85e+05 loss_x2y=3.0893e-01 ppl_x2y=1.36 loss_y2x=2.4689e-01 ppl_y2x=1.28 dual_loss=1.7148e+00
Validation X2Y - loss=2.2355e+00 ppl=9.35 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7258e+00 ppl=5.62 best_loss=1.0187e+00 best_ppl=2.77
Epoch 299 - |param|=9.67e+02 |g_param|=5.86e+05 loss_x2y=2.8974e-01 ppl_x2y=1.34 loss_y2x=2.4317e-01 ppl_y2x=1.28 dual_loss=1.6817e+00
Validation X2Y - loss=2.2429e+00 ppl=9.42 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7600e+00 ppl=5.81 best_loss=1.0187e+00 best_ppl=2.77
Epoch 300 - |param|=9.67e+02 |g_param|=6.37e+05 loss_x2y=3.0667e-01 ppl_x2y=1.36 loss_y2x=2.5682e-01 ppl_y2x=1.29 dual_loss=1.8047e+00
Validation X2Y - loss=2.3041e+00 ppl=10.02 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7398e+00 ppl=5.70 best_loss=1.0187e+00 best_ppl=2.77
Epoch 301 - |param|=9.67e+02 |g_param|=5.77e+05 loss_x2y=3.7611e-01 ppl_x2y=1.46 loss_y2x=2.8114e-01 ppl_y2x=1.32 dual_loss=2.0722e+00
Validation X2Y - loss=2.2671e+00 ppl=9.65 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7671e+00 ppl=5.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 302 - |param|=9.68e+02 |g_param|=6.27e+05 loss_x2y=2.9747e-01 ppl_x2y=1.35 loss_y2x=2.5067e-01 ppl_y2x=1.28 dual_loss=1.7119e+00
Validation X2Y - loss=2.2691e+00 ppl=9.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7212e+00 ppl=5.59 best_loss=1.0187e+00 best_ppl=2.77
Epoch 303 - |param|=9.68e+02 |g_param|=5.71e+05 loss_x2y=2.8777e-01 ppl_x2y=1.33 loss_y2x=2.3950e-01 ppl_y2x=1.27 dual_loss=1.6403e+00
Validation X2Y - loss=2.2527e+00 ppl=9.51 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7605e+00 ppl=5.82 best_loss=1.0187e+00 best_ppl=2.77
Epoch 304 - |param|=9.68e+02 |g_param|=5.94e+05 loss_x2y=2.9347e-01 ppl_x2y=1.34 loss_y2x=2.3619e-01 ppl_y2x=1.27 dual_loss=1.6461e+00
Validation X2Y - loss=2.2334e+00 ppl=9.33 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7427e+00 ppl=5.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 305 - |param|=9.68e+02 |g_param|=5.74e+05 loss_x2y=3.0321e-01 ppl_x2y=1.35 loss_y2x=2.4797e-01 ppl_y2x=1.28 dual_loss=1.6734e+00
Validation X2Y - loss=2.3081e+00 ppl=10.06 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7295e+00 ppl=5.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 306 - |param|=9.69e+02 |g_param|=5.93e+05 loss_x2y=3.5676e-01 ppl_x2y=1.43 loss_y2x=3.1481e-01 ppl_y2x=1.37 dual_loss=2.2422e+00
Validation X2Y - loss=2.2445e+00 ppl=9.44 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8127e+00 ppl=6.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 307 - |param|=9.69e+02 |g_param|=5.72e+05 loss_x2y=3.2382e-01 ppl_x2y=1.38 loss_y2x=2.6050e-01 ppl_y2x=1.30 dual_loss=1.8168e+00
Validation X2Y - loss=2.2978e+00 ppl=9.95 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8123e+00 ppl=6.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 308 - |param|=9.69e+02 |g_param|=6.18e+05 loss_x2y=2.9014e-01 ppl_x2y=1.34 loss_y2x=2.3557e-01 ppl_y2x=1.27 dual_loss=1.6073e+00
Validation X2Y - loss=2.1993e+00 ppl=9.02 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7920e+00 ppl=6.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 309 - |param|=9.70e+02 |g_param|=5.70e+05 loss_x2y=3.3457e-01 ppl_x2y=1.40 loss_y2x=2.7551e-01 ppl_y2x=1.32 dual_loss=2.0361e+00
Validation X2Y - loss=2.2821e+00 ppl=9.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8183e+00 ppl=6.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 310 - |param|=9.70e+02 |g_param|=5.94e+05 loss_x2y=3.0024e-01 ppl_x2y=1.35 loss_y2x=2.4424e-01 ppl_y2x=1.28 dual_loss=1.7358e+00
Validation X2Y - loss=2.2951e+00 ppl=9.93 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8071e+00 ppl=6.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 311 - |param|=9.70e+02 |g_param|=5.99e+05 loss_x2y=3.2591e-01 ppl_x2y=1.39 loss_y2x=3.2240e-01 ppl_y2x=1.38 dual_loss=2.4238e+00
Validation X2Y - loss=2.2990e+00 ppl=9.96 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7956e+00 ppl=6.02 best_loss=1.0187e+00 best_ppl=2.77
Epoch 312 - |param|=9.70e+02 |g_param|=6.09e+05 loss_x2y=3.0454e-01 ppl_x2y=1.36 loss_y2x=2.5385e-01 ppl_y2x=1.29 dual_loss=1.8435e+00
Validation X2Y - loss=2.2722e+00 ppl=9.70 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8453e+00 ppl=6.33 best_loss=1.0187e+00 best_ppl=2.77
Epoch 313 - |param|=9.71e+02 |g_param|=5.71e+05 loss_x2y=2.9041e-01 ppl_x2y=1.34 loss_y2x=2.5147e-01 ppl_y2x=1.29 dual_loss=1.7006e+00
Validation X2Y - loss=2.2862e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8428e+00 ppl=6.31 best_loss=1.0187e+00 best_ppl=2.77
Epoch 314 - |param|=9.71e+02 |g_param|=5.87e+05 loss_x2y=3.1935e-01 ppl_x2y=1.38 loss_y2x=2.5425e-01 ppl_y2x=1.29 dual_loss=1.8913e+00
Validation X2Y - loss=2.2695e+00 ppl=9.67 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8339e+00 ppl=6.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 315 - |param|=9.71e+02 |g_param|=5.74e+05 loss_x2y=3.2832e-01 ppl_x2y=1.39 loss_y2x=2.7209e-01 ppl_y2x=1.31 dual_loss=2.0119e+00
Validation X2Y - loss=2.2890e+00 ppl=9.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8267e+00 ppl=6.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 316 - |param|=9.72e+02 |g_param|=5.94e+05 loss_x2y=2.9720e-01 ppl_x2y=1.35 loss_y2x=2.5649e-01 ppl_y2x=1.29 dual_loss=1.8736e+00
Validation X2Y - loss=2.3326e+00 ppl=10.30 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8529e+00 ppl=6.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 317 - |param|=9.72e+02 |g_param|=5.55e+05 loss_x2y=2.8678e-01 ppl_x2y=1.33 loss_y2x=2.2784e-01 ppl_y2x=1.26 dual_loss=1.5920e+00
Validation X2Y - loss=2.3084e+00 ppl=10.06 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8219e+00 ppl=6.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 318 - |param|=9.72e+02 |g_param|=5.89e+05 loss_x2y=2.9499e-01 ppl_x2y=1.34 loss_y2x=2.5319e-01 ppl_y2x=1.29 dual_loss=1.8282e+00
Validation X2Y - loss=2.2845e+00 ppl=9.82 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8118e+00 ppl=6.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 319 - |param|=9.72e+02 |g_param|=6.43e+05 loss_x2y=3.0581e-01 ppl_x2y=1.36 loss_y2x=2.5518e-01 ppl_y2x=1.29 dual_loss=1.8716e+00
Validation X2Y - loss=2.2559e+00 ppl=9.54 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8242e+00 ppl=6.20 best_loss=1.0187e+00 best_ppl=2.77
Epoch 320 - |param|=9.73e+02 |g_param|=5.69e+05 loss_x2y=2.9761e-01 ppl_x2y=1.35 loss_y2x=2.4386e-01 ppl_y2x=1.28 dual_loss=1.7435e+00
Validation X2Y - loss=2.2628e+00 ppl=9.61 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7661e+00 ppl=5.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 321 - |param|=9.73e+02 |g_param|=5.53e+05 loss_x2y=2.9530e-01 ppl_x2y=1.34 loss_y2x=2.5347e-01 ppl_y2x=1.29 dual_loss=1.7907e+00
Validation X2Y - loss=2.1957e+00 ppl=8.99 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8021e+00 ppl=6.06 best_loss=1.0187e+00 best_ppl=2.77
Epoch 322 - |param|=9.73e+02 |g_param|=5.85e+05 loss_x2y=3.3008e-01 ppl_x2y=1.39 loss_y2x=2.8273e-01 ppl_y2x=1.33 dual_loss=2.0521e+00
Validation X2Y - loss=2.3032e+00 ppl=10.01 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7789e+00 ppl=5.92 best_loss=1.0187e+00 best_ppl=2.77
Epoch 323 - |param|=9.74e+02 |g_param|=5.61e+05 loss_x2y=3.0816e-01 ppl_x2y=1.36 loss_y2x=2.5529e-01 ppl_y2x=1.29 dual_loss=1.8890e+00
Validation X2Y - loss=2.2819e+00 ppl=9.80 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8408e+00 ppl=6.30 best_loss=1.0187e+00 best_ppl=2.77
Epoch 324 - |param|=9.74e+02 |g_param|=5.78e+05 loss_x2y=2.9468e-01 ppl_x2y=1.34 loss_y2x=2.4272e-01 ppl_y2x=1.27 dual_loss=1.7555e+00
Validation X2Y - loss=2.2541e+00 ppl=9.53 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8403e+00 ppl=6.30 best_loss=1.0187e+00 best_ppl=2.77
Epoch 325 - |param|=9.74e+02 |g_param|=5.65e+05 loss_x2y=3.0382e-01 ppl_x2y=1.36 loss_y2x=2.6026e-01 ppl_y2x=1.30 dual_loss=1.8887e+00
Validation X2Y - loss=2.2572e+00 ppl=9.56 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8259e+00 ppl=6.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 326 - |param|=9.74e+02 |g_param|=5.86e+05 loss_x2y=2.8476e-01 ppl_x2y=1.33 loss_y2x=2.5168e-01 ppl_y2x=1.29 dual_loss=1.8669e+00
Validation X2Y - loss=2.2990e+00 ppl=9.96 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8067e+00 ppl=6.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 327 - |param|=9.75e+02 |g_param|=5.42e+05 loss_x2y=2.9574e-01 ppl_x2y=1.34 loss_y2x=2.4657e-01 ppl_y2x=1.28 dual_loss=1.8048e+00
Validation X2Y - loss=2.3251e+00 ppl=10.23 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8476e+00 ppl=6.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 328 - |param|=9.75e+02 |g_param|=5.73e+05 loss_x2y=2.9270e-01 ppl_x2y=1.34 loss_y2x=2.4590e-01 ppl_y2x=1.28 dual_loss=1.7616e+00
Validation X2Y - loss=2.3198e+00 ppl=10.17 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7793e+00 ppl=5.93 best_loss=1.0187e+00 best_ppl=2.77
Epoch 329 - |param|=9.75e+02 |g_param|=5.68e+05 loss_x2y=2.9621e-01 ppl_x2y=1.34 loss_y2x=2.5030e-01 ppl_y2x=1.28 dual_loss=1.7615e+00
Validation X2Y - loss=2.2900e+00 ppl=9.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7682e+00 ppl=5.86 best_loss=1.0187e+00 best_ppl=2.77
Epoch 330 - |param|=9.76e+02 |g_param|=6.26e+05 loss_x2y=2.8772e-01 ppl_x2y=1.33 loss_y2x=2.3373e-01 ppl_y2x=1.26 dual_loss=1.6804e+00
Validation X2Y - loss=2.3312e+00 ppl=10.29 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8620e+00 ppl=6.44 best_loss=1.0187e+00 best_ppl=2.77
Epoch 331 - |param|=9.76e+02 |g_param|=8.68e+05 loss_x2y=3.0616e-01 ppl_x2y=1.36 loss_y2x=2.5335e-01 ppl_y2x=1.29 dual_loss=1.9103e+00
Validation X2Y - loss=2.3244e+00 ppl=10.22 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8061e+00 ppl=6.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 332 - |param|=9.76e+02 |g_param|=9.28e+05 loss_x2y=3.1123e-01 ppl_x2y=1.37 loss_y2x=2.5737e-01 ppl_y2x=1.29 dual_loss=1.8882e+00
Validation X2Y - loss=2.2763e+00 ppl=9.74 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8518e+00 ppl=6.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 333 - |param|=9.76e+02 |g_param|=8.63e+05 loss_x2y=2.8099e-01 ppl_x2y=1.32 loss_y2x=2.3616e-01 ppl_y2x=1.27 dual_loss=1.6776e+00
Validation X2Y - loss=2.3387e+00 ppl=10.37 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8386e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 334 - |param|=9.77e+02 |g_param|=7.66e+05 loss_x2y=2.9584e-01 ppl_x2y=1.34 loss_y2x=2.4888e-01 ppl_y2x=1.28 dual_loss=1.8087e+00
Validation X2Y - loss=2.3658e+00 ppl=10.65 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8579e+00 ppl=6.41 best_loss=1.0187e+00 best_ppl=2.77
Epoch 335 - |param|=9.77e+02 |g_param|=5.65e+05 loss_x2y=2.7893e-01 ppl_x2y=1.32 loss_y2x=2.2698e-01 ppl_y2x=1.25 dual_loss=1.6494e+00
Validation X2Y - loss=2.3433e+00 ppl=10.42 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7639e+00 ppl=5.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 336 - |param|=9.77e+02 |g_param|=5.82e+05 loss_x2y=2.8581e-01 ppl_x2y=1.33 loss_y2x=2.4057e-01 ppl_y2x=1.27 dual_loss=1.7463e+00
Validation X2Y - loss=2.3329e+00 ppl=10.31 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8221e+00 ppl=6.18 best_loss=1.0187e+00 best_ppl=2.77
Epoch 337 - |param|=9.78e+02 |g_param|=5.45e+05 loss_x2y=3.2167e-01 ppl_x2y=1.38 loss_y2x=2.6944e-01 ppl_y2x=1.31 dual_loss=1.9253e+00
Validation X2Y - loss=2.3040e+00 ppl=10.01 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8346e+00 ppl=6.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 338 - |param|=9.78e+02 |g_param|=5.69e+05 loss_x2y=2.9069e-01 ppl_x2y=1.34 loss_y2x=2.4007e-01 ppl_y2x=1.27 dual_loss=1.6707e+00
Validation X2Y - loss=2.3001e+00 ppl=9.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8531e+00 ppl=6.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 339 - |param|=9.78e+02 |g_param|=5.56e+05 loss_x2y=3.4251e-01 ppl_x2y=1.41 loss_y2x=2.6773e-01 ppl_y2x=1.31 dual_loss=2.0316e+00
Validation X2Y - loss=2.3025e+00 ppl=10.00 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8076e+00 ppl=6.10 best_loss=1.0187e+00 best_ppl=2.77
Epoch 340 - |param|=9.78e+02 |g_param|=5.76e+05 loss_x2y=2.8488e-01 ppl_x2y=1.33 loss_y2x=2.4282e-01 ppl_y2x=1.27 dual_loss=1.7577e+00
Validation X2Y - loss=2.3053e+00 ppl=10.03 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7915e+00 ppl=6.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 341 - |param|=9.79e+02 |g_param|=5.46e+05 loss_x2y=2.7110e-01 ppl_x2y=1.31 loss_y2x=2.3382e-01 ppl_y2x=1.26 dual_loss=1.6433e+00
Validation X2Y - loss=2.3344e+00 ppl=10.32 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8078e+00 ppl=6.10 best_loss=1.0187e+00 best_ppl=2.77
Epoch 342 - |param|=9.79e+02 |g_param|=5.49e+05 loss_x2y=2.9162e-01 ppl_x2y=1.34 loss_y2x=2.4485e-01 ppl_y2x=1.28 dual_loss=1.8868e+00
Validation X2Y - loss=2.3706e+00 ppl=10.70 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7614e+00 ppl=5.82 best_loss=1.0187e+00 best_ppl=2.77
Epoch 343 - |param|=9.79e+02 |g_param|=5.39e+05 loss_x2y=2.8906e-01 ppl_x2y=1.34 loss_y2x=2.4128e-01 ppl_y2x=1.27 dual_loss=1.7857e+00
Validation X2Y - loss=2.3254e+00 ppl=10.23 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7282e+00 ppl=5.63 best_loss=1.0187e+00 best_ppl=2.77
Epoch 344 - |param|=9.79e+02 |g_param|=5.71e+05 loss_x2y=2.9660e-01 ppl_x2y=1.35 loss_y2x=2.4534e-01 ppl_y2x=1.28 dual_loss=1.8024e+00
Validation X2Y - loss=2.2895e+00 ppl=9.87 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7985e+00 ppl=6.04 best_loss=1.0187e+00 best_ppl=2.77
Epoch 345 - |param|=9.80e+02 |g_param|=5.43e+05 loss_x2y=3.0970e-01 ppl_x2y=1.36 loss_y2x=2.4895e-01 ppl_y2x=1.28 dual_loss=1.8685e+00
Validation X2Y - loss=2.2648e+00 ppl=9.63 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7199e+00 ppl=5.58 best_loss=1.0187e+00 best_ppl=2.77
Epoch 346 - |param|=9.80e+02 |g_param|=5.69e+05 loss_x2y=3.0078e-01 ppl_x2y=1.35 loss_y2x=2.4973e-01 ppl_y2x=1.28 dual_loss=1.8794e+00
Validation X2Y - loss=2.3455e+00 ppl=10.44 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.6917e+00 ppl=5.43 best_loss=1.0187e+00 best_ppl=2.77
Epoch 347 - |param|=9.80e+02 |g_param|=5.35e+05 loss_x2y=2.9570e-01 ppl_x2y=1.34 loss_y2x=2.4366e-01 ppl_y2x=1.28 dual_loss=1.8069e+00
Validation X2Y - loss=2.3069e+00 ppl=10.04 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7293e+00 ppl=5.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 348 - |param|=9.81e+02 |g_param|=5.62e+05 loss_x2y=3.3478e-01 ppl_x2y=1.40 loss_y2x=2.8322e-01 ppl_y2x=1.33 dual_loss=2.2935e+00
Validation X2Y - loss=2.2730e+00 ppl=9.71 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7686e+00 ppl=5.86 best_loss=1.0187e+00 best_ppl=2.77
Epoch 349 - |param|=9.81e+02 |g_param|=5.23e+05 loss_x2y=2.9439e-01 ppl_x2y=1.34 loss_y2x=2.4006e-01 ppl_y2x=1.27 dual_loss=1.7457e+00
Validation X2Y - loss=2.2595e+00 ppl=9.58 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7963e+00 ppl=6.03 best_loss=1.0187e+00 best_ppl=2.77
Epoch 350 - |param|=9.81e+02 |g_param|=5.60e+05 loss_x2y=3.0199e-01 ppl_x2y=1.35 loss_y2x=2.5282e-01 ppl_y2x=1.29 dual_loss=1.9452e+00
Validation X2Y - loss=2.2871e+00 ppl=9.85 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8023e+00 ppl=6.06 best_loss=1.0187e+00 best_ppl=2.77
Epoch 351 - |param|=9.81e+02 |g_param|=5.23e+05 loss_x2y=2.7187e-01 ppl_x2y=1.31 loss_y2x=2.3205e-01 ppl_y2x=1.26 dual_loss=1.7408e+00
Validation X2Y - loss=2.2442e+00 ppl=9.43 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8222e+00 ppl=6.19 best_loss=1.0187e+00 best_ppl=2.77
Epoch 352 - |param|=9.82e+02 |g_param|=8.35e+05 loss_x2y=2.7892e-01 ppl_x2y=1.32 loss_y2x=2.3751e-01 ppl_y2x=1.27 dual_loss=1.7352e+00
Validation X2Y - loss=2.3139e+00 ppl=10.11 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7420e+00 ppl=5.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 353 - |param|=9.82e+02 |g_param|=8.72e+05 loss_x2y=3.2011e-01 ppl_x2y=1.38 loss_y2x=2.6337e-01 ppl_y2x=1.30 dual_loss=2.0817e+00
Validation X2Y - loss=2.3173e+00 ppl=10.15 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7552e+00 ppl=5.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 354 - |param|=9.82e+02 |g_param|=9.21e+05 loss_x2y=2.8487e-01 ppl_x2y=1.33 loss_y2x=2.3663e-01 ppl_y2x=1.27 dual_loss=1.8512e+00
Validation X2Y - loss=2.2869e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7983e+00 ppl=6.04 best_loss=1.0187e+00 best_ppl=2.77
Epoch 355 - |param|=9.83e+02 |g_param|=8.39e+05 loss_x2y=2.9963e-01 ppl_x2y=1.35 loss_y2x=2.4186e-01 ppl_y2x=1.27 dual_loss=1.8003e+00
Validation X2Y - loss=2.2997e+00 ppl=9.97 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8383e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 356 - |param|=9.83e+02 |g_param|=8.76e+05 loss_x2y=3.7309e-01 ppl_x2y=1.45 loss_y2x=2.8681e-01 ppl_y2x=1.33 dual_loss=2.4777e+00
Validation X2Y - loss=2.2770e+00 ppl=9.75 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8178e+00 ppl=6.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 357 - |param|=9.83e+02 |g_param|=8.35e+05 loss_x2y=2.7405e-01 ppl_x2y=1.32 loss_y2x=2.2663e-01 ppl_y2x=1.25 dual_loss=1.7374e+00
Validation X2Y - loss=2.3002e+00 ppl=9.98 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8449e+00 ppl=6.33 best_loss=1.0187e+00 best_ppl=2.77
Epoch 358 - |param|=9.83e+02 |g_param|=7.53e+05 loss_x2y=3.0718e-01 ppl_x2y=1.36 loss_y2x=3.0175e-01 ppl_y2x=1.35 dual_loss=2.4945e+00
Validation X2Y - loss=2.2791e+00 ppl=9.77 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8404e+00 ppl=6.30 best_loss=1.0187e+00 best_ppl=2.77
Epoch 359 - |param|=9.84e+02 |g_param|=5.36e+05 loss_x2y=3.6322e-01 ppl_x2y=1.44 loss_y2x=2.8142e-01 ppl_y2x=1.33 dual_loss=2.1622e+00
Validation X2Y - loss=2.2859e+00 ppl=9.83 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7936e+00 ppl=6.01 best_loss=1.0187e+00 best_ppl=2.77
Epoch 360 - |param|=9.84e+02 |g_param|=5.72e+05 loss_x2y=3.3041e-01 ppl_x2y=1.39 loss_y2x=2.6555e-01 ppl_y2x=1.30 dual_loss=2.2058e+00
Validation X2Y - loss=2.3086e+00 ppl=10.06 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8196e+00 ppl=6.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 361 - |param|=9.84e+02 |g_param|=5.17e+05 loss_x2y=2.8255e-01 ppl_x2y=1.33 loss_y2x=2.3505e-01 ppl_y2x=1.26 dual_loss=1.7679e+00
Validation X2Y - loss=2.3420e+00 ppl=10.40 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7462e+00 ppl=5.73 best_loss=1.0187e+00 best_ppl=2.77
Epoch 362 - |param|=9.84e+02 |g_param|=5.29e+05 loss_x2y=3.0215e-01 ppl_x2y=1.35 loss_y2x=2.4074e-01 ppl_y2x=1.27 dual_loss=1.7739e+00
Validation X2Y - loss=2.3590e+00 ppl=10.58 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7686e+00 ppl=5.86 best_loss=1.0187e+00 best_ppl=2.77
Epoch 363 - |param|=9.85e+02 |g_param|=5.24e+05 loss_x2y=3.0123e-01 ppl_x2y=1.35 loss_y2x=2.5488e-01 ppl_y2x=1.29 dual_loss=1.9106e+00
Validation X2Y - loss=2.3422e+00 ppl=10.40 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8256e+00 ppl=6.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 364 - |param|=9.85e+02 |g_param|=5.36e+05 loss_x2y=3.2926e-01 ppl_x2y=1.39 loss_y2x=2.7174e-01 ppl_y2x=1.31 dual_loss=2.1238e+00
Validation X2Y - loss=2.3694e+00 ppl=10.69 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8463e+00 ppl=6.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 365 - |param|=9.85e+02 |g_param|=5.33e+05 loss_x2y=3.0038e-01 ppl_x2y=1.35 loss_y2x=2.6065e-01 ppl_y2x=1.30 dual_loss=2.1002e+00
Validation X2Y - loss=2.3661e+00 ppl=10.66 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7918e+00 ppl=6.00 best_loss=1.0187e+00 best_ppl=2.77
Epoch 366 - |param|=9.85e+02 |g_param|=5.47e+05 loss_x2y=2.8346e-01 ppl_x2y=1.33 loss_y2x=2.3044e-01 ppl_y2x=1.26 dual_loss=1.7405e+00
Validation X2Y - loss=2.3411e+00 ppl=10.39 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8284e+00 ppl=6.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 367 - |param|=9.86e+02 |g_param|=7.64e+05 loss_x2y=3.1781e-01 ppl_x2y=1.37 loss_y2x=2.5793e-01 ppl_y2x=1.29 dual_loss=2.1090e+00
Validation X2Y - loss=2.3832e+00 ppl=10.84 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8115e+00 ppl=6.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 368 - |param|=9.86e+02 |g_param|=8.77e+05 loss_x2y=2.8973e-01 ppl_x2y=1.34 loss_y2x=2.4605e-01 ppl_y2x=1.28 dual_loss=1.8952e+00
Validation X2Y - loss=2.3564e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8121e+00 ppl=6.12 best_loss=1.0187e+00 best_ppl=2.77
Epoch 369 - |param|=9.86e+02 |g_param|=8.47e+05 loss_x2y=3.2726e-01 ppl_x2y=1.39 loss_y2x=2.7373e-01 ppl_y2x=1.31 dual_loss=2.2421e+00
Validation X2Y - loss=2.3188e+00 ppl=10.16 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7820e+00 ppl=5.94 best_loss=1.0187e+00 best_ppl=2.77
Epoch 370 - |param|=9.87e+02 |g_param|=8.48e+05 loss_x2y=3.2140e-01 ppl_x2y=1.38 loss_y2x=2.6649e-01 ppl_y2x=1.31 dual_loss=2.1938e+00
Validation X2Y - loss=2.2785e+00 ppl=9.76 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7810e+00 ppl=5.94 best_loss=1.0187e+00 best_ppl=2.77
Epoch 371 - |param|=9.87e+02 |g_param|=7.82e+05 loss_x2y=3.6185e-01 ppl_x2y=1.44 loss_y2x=2.7943e-01 ppl_y2x=1.32 dual_loss=2.2261e+00
Validation X2Y - loss=2.3227e+00 ppl=10.20 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8370e+00 ppl=6.28 best_loss=1.0187e+00 best_ppl=2.77
Epoch 372 - |param|=9.87e+02 |g_param|=8.26e+05 loss_x2y=2.7138e-01 ppl_x2y=1.31 loss_y2x=2.3372e-01 ppl_y2x=1.26 dual_loss=1.7741e+00
Validation X2Y - loss=2.3404e+00 ppl=10.38 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8059e+00 ppl=6.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 373 - |param|=9.87e+02 |g_param|=7.92e+05 loss_x2y=2.7065e-01 ppl_x2y=1.31 loss_y2x=2.2567e-01 ppl_y2x=1.25 dual_loss=1.7124e+00
Validation X2Y - loss=2.3460e+00 ppl=10.44 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7938e+00 ppl=6.01 best_loss=1.0187e+00 best_ppl=2.77
Epoch 374 - |param|=9.88e+02 |g_param|=8.26e+05 loss_x2y=2.7902e-01 ppl_x2y=1.32 loss_y2x=2.3502e-01 ppl_y2x=1.26 dual_loss=1.7905e+00
Validation X2Y - loss=2.3651e+00 ppl=10.65 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7462e+00 ppl=5.73 best_loss=1.0187e+00 best_ppl=2.77
Epoch 375 - |param|=9.88e+02 |g_param|=8.40e+05 loss_x2y=2.8407e-01 ppl_x2y=1.33 loss_y2x=2.4481e-01 ppl_y2x=1.28 dual_loss=1.8795e+00
Validation X2Y - loss=2.3650e+00 ppl=10.64 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7883e+00 ppl=5.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 376 - |param|=9.88e+02 |g_param|=8.78e+05 loss_x2y=3.3452e-01 ppl_x2y=1.40 loss_y2x=2.7166e-01 ppl_y2x=1.31 dual_loss=2.2411e+00
Validation X2Y - loss=2.2931e+00 ppl=9.91 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.7949e+00 ppl=6.02 best_loss=1.0187e+00 best_ppl=2.77
Epoch 377 - |param|=9.88e+02 |g_param|=5.57e+05 loss_x2y=2.7292e-01 ppl_x2y=1.31 loss_y2x=2.3206e-01 ppl_y2x=1.26 dual_loss=1.7929e+00
Validation X2Y - loss=2.3339e+00 ppl=10.32 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7504e+00 ppl=5.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 378 - |param|=9.89e+02 |g_param|=5.25e+05 loss_x2y=2.6687e-01 ppl_x2y=1.31 loss_y2x=2.2921e-01 ppl_y2x=1.26 dual_loss=1.6875e+00
Validation X2Y - loss=2.3561e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7768e+00 ppl=5.91 best_loss=1.0187e+00 best_ppl=2.77
Epoch 379 - |param|=9.89e+02 |g_param|=5.19e+05 loss_x2y=3.0340e-01 ppl_x2y=1.35 loss_y2x=2.5589e-01 ppl_y2x=1.29 dual_loss=2.0292e+00
Validation X2Y - loss=2.3810e+00 ppl=10.82 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7804e+00 ppl=5.93 best_loss=1.0187e+00 best_ppl=2.77
Epoch 380 - |param|=9.89e+02 |g_param|=5.42e+05 loss_x2y=2.7457e-01 ppl_x2y=1.32 loss_y2x=2.4556e-01 ppl_y2x=1.28 dual_loss=1.8879e+00
Validation X2Y - loss=2.3366e+00 ppl=10.35 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8192e+00 ppl=6.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 381 - |param|=9.90e+02 |g_param|=5.05e+05 loss_x2y=2.9140e-01 ppl_x2y=1.34 loss_y2x=2.3588e-01 ppl_y2x=1.27 dual_loss=1.8456e+00
Validation X2Y - loss=2.3602e+00 ppl=10.59 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7939e+00 ppl=6.01 best_loss=1.0187e+00 best_ppl=2.77
Epoch 382 - |param|=9.90e+02 |g_param|=5.42e+05 loss_x2y=2.7297e-01 ppl_x2y=1.31 loss_y2x=2.3446e-01 ppl_y2x=1.26 dual_loss=1.7862e+00
Validation X2Y - loss=2.3377e+00 ppl=10.36 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8389e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 383 - |param|=9.90e+02 |g_param|=5.09e+05 loss_x2y=2.6707e-01 ppl_x2y=1.31 loss_y2x=2.2564e-01 ppl_y2x=1.25 dual_loss=1.7698e+00
Validation X2Y - loss=2.3857e+00 ppl=10.87 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7895e+00 ppl=5.99 best_loss=1.0187e+00 best_ppl=2.77
Epoch 384 - |param|=9.90e+02 |g_param|=5.41e+05 loss_x2y=2.8109e-01 ppl_x2y=1.32 loss_y2x=2.3506e-01 ppl_y2x=1.26 dual_loss=1.7707e+00
Validation X2Y - loss=2.3747e+00 ppl=10.75 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8184e+00 ppl=6.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 385 - |param|=9.91e+02 |g_param|=5.23e+05 loss_x2y=3.8397e-01 ppl_x2y=1.47 loss_y2x=2.8477e-01 ppl_y2x=1.33 dual_loss=2.4614e+00
Validation X2Y - loss=2.3897e+00 ppl=10.91 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7468e+00 ppl=5.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 386 - |param|=9.91e+02 |g_param|=5.58e+05 loss_x2y=3.0682e-01 ppl_x2y=1.36 loss_y2x=2.6747e-01 ppl_y2x=1.31 dual_loss=2.2635e+00
Validation X2Y - loss=2.3592e+00 ppl=10.58 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8150e+00 ppl=6.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 387 - |param|=9.91e+02 |g_param|=5.06e+05 loss_x2y=2.7626e-01 ppl_x2y=1.32 loss_y2x=2.3613e-01 ppl_y2x=1.27 dual_loss=1.9177e+00
Validation X2Y - loss=2.3681e+00 ppl=10.68 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8259e+00 ppl=6.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 388 - |param|=9.91e+02 |g_param|=5.13e+05 loss_x2y=2.5678e-01 ppl_x2y=1.29 loss_y2x=2.2673e-01 ppl_y2x=1.25 dual_loss=1.7269e+00
Validation X2Y - loss=2.3328e+00 ppl=10.31 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8169e+00 ppl=6.15 best_loss=1.0187e+00 best_ppl=2.77
Epoch 389 - |param|=9.92e+02 |g_param|=4.97e+05 loss_x2y=2.8375e-01 ppl_x2y=1.33 loss_y2x=2.3917e-01 ppl_y2x=1.27 dual_loss=1.9504e+00
Validation X2Y - loss=2.3456e+00 ppl=10.44 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8255e+00 ppl=6.21 best_loss=1.0187e+00 best_ppl=2.77
Epoch 390 - |param|=9.92e+02 |g_param|=5.27e+05 loss_x2y=2.9286e-01 ppl_x2y=1.34 loss_y2x=2.5511e-01 ppl_y2x=1.29 dual_loss=2.1339e+00
Validation X2Y - loss=2.3438e+00 ppl=10.42 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8366e+00 ppl=6.28 best_loss=1.0187e+00 best_ppl=2.77
Epoch 391 - |param|=9.92e+02 |g_param|=7.68e+05 loss_x2y=3.1576e-01 ppl_x2y=1.37 loss_y2x=2.5639e-01 ppl_y2x=1.29 dual_loss=2.0933e+00
Validation X2Y - loss=2.3369e+00 ppl=10.35 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8334e+00 ppl=6.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 392 - |param|=9.93e+02 |g_param|=8.24e+05 loss_x2y=2.6329e-01 ppl_x2y=1.30 loss_y2x=2.2781e-01 ppl_y2x=1.26 dual_loss=1.7483e+00
Validation X2Y - loss=2.3670e+00 ppl=10.67 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8715e+00 ppl=6.50 best_loss=1.0187e+00 best_ppl=2.77
Epoch 393 - |param|=9.93e+02 |g_param|=8.09e+05 loss_x2y=2.9644e-01 ppl_x2y=1.35 loss_y2x=2.6372e-01 ppl_y2x=1.30 dual_loss=2.2842e+00
Validation X2Y - loss=2.4177e+00 ppl=11.22 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8650e+00 ppl=6.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 394 - |param|=9.93e+02 |g_param|=8.21e+05 loss_x2y=2.6120e-01 ppl_x2y=1.30 loss_y2x=2.2421e-01 ppl_y2x=1.25 dual_loss=1.7263e+00
Validation X2Y - loss=2.4206e+00 ppl=11.25 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8221e+00 ppl=6.19 best_loss=1.0187e+00 best_ppl=2.77
Epoch 395 - |param|=9.93e+02 |g_param|=8.10e+05 loss_x2y=2.9380e-01 ppl_x2y=1.34 loss_y2x=2.3622e-01 ppl_y2x=1.27 dual_loss=1.8644e+00
Validation X2Y - loss=2.3741e+00 ppl=10.74 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8274e+00 ppl=6.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 396 - |param|=9.94e+02 |g_param|=8.05e+05 loss_x2y=2.6918e-01 ppl_x2y=1.31 loss_y2x=2.2918e-01 ppl_y2x=1.26 dual_loss=1.8122e+00
Validation X2Y - loss=2.3881e+00 ppl=10.89 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8533e+00 ppl=6.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 397 - |param|=9.94e+02 |g_param|=8.09e+05 loss_x2y=2.9038e-01 ppl_x2y=1.34 loss_y2x=2.4694e-01 ppl_y2x=1.28 dual_loss=2.0036e+00
Validation X2Y - loss=2.3815e+00 ppl=10.82 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8223e+00 ppl=6.19 best_loss=1.0187e+00 best_ppl=2.77
Epoch 398 - |param|=9.94e+02 |g_param|=8.29e+05 loss_x2y=3.0719e-01 ppl_x2y=1.36 loss_y2x=2.5318e-01 ppl_y2x=1.29 dual_loss=1.9625e+00
Validation X2Y - loss=2.3915e+00 ppl=10.93 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8397e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 399 - |param|=9.94e+02 |g_param|=8.01e+05 loss_x2y=2.7282e-01 ppl_x2y=1.31 loss_y2x=2.3079e-01 ppl_y2x=1.26 dual_loss=1.8638e+00
Validation X2Y - loss=2.4252e+00 ppl=11.30 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9136e+00 ppl=6.78 best_loss=1.0187e+00 best_ppl=2.77
Epoch 400 - |param|=9.95e+02 |g_param|=8.59e+05 loss_x2y=3.1373e-01 ppl_x2y=1.37 loss_y2x=2.7504e-01 ppl_y2x=1.32 dual_loss=2.4458e+00
Validation X2Y - loss=2.4022e+00 ppl=11.05 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8883e+00 ppl=6.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 401 - |param|=9.95e+02 |g_param|=7.99e+05 loss_x2y=2.7328e-01 ppl_x2y=1.31 loss_y2x=2.2215e-01 ppl_y2x=1.25 dual_loss=1.7088e+00
Validation X2Y - loss=2.3750e+00 ppl=10.75 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8285e+00 ppl=6.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 402 - |param|=9.95e+02 |g_param|=8.39e+05 loss_x2y=3.0315e-01 ppl_x2y=1.35 loss_y2x=2.5150e-01 ppl_y2x=1.29 dual_loss=2.1136e+00
Validation X2Y - loss=2.4418e+00 ppl=11.49 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8518e+00 ppl=6.37 best_loss=1.0187e+00 best_ppl=2.77
Epoch 403 - |param|=9.96e+02 |g_param|=7.73e+05 loss_x2y=3.3343e-01 ppl_x2y=1.40 loss_y2x=3.0726e-01 ppl_y2x=1.36 dual_loss=2.3186e+00
Validation X2Y - loss=2.3920e+00 ppl=10.93 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7840e+00 ppl=5.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 404 - |param|=9.96e+02 |g_param|=7.83e+05 loss_x2y=2.8204e-01 ppl_x2y=1.33 loss_y2x=2.2740e-01 ppl_y2x=1.26 dual_loss=1.8144e+00
Validation X2Y - loss=2.3485e+00 ppl=10.47 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8061e+00 ppl=6.09 best_loss=1.0187e+00 best_ppl=2.77
Epoch 405 - |param|=9.96e+02 |g_param|=7.71e+05 loss_x2y=2.7003e-01 ppl_x2y=1.31 loss_y2x=2.2440e-01 ppl_y2x=1.25 dual_loss=1.7525e+00
Validation X2Y - loss=2.4150e+00 ppl=11.19 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.7521e+00 ppl=5.77 best_loss=1.0187e+00 best_ppl=2.77
Epoch 406 - |param|=9.96e+02 |g_param|=8.30e+05 loss_x2y=2.9698e-01 ppl_x2y=1.35 loss_y2x=2.5777e-01 ppl_y2x=1.29 dual_loss=2.1549e+00
Validation X2Y - loss=2.3662e+00 ppl=10.66 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8087e+00 ppl=6.10 best_loss=1.0187e+00 best_ppl=2.77
Epoch 407 - |param|=9.97e+02 |g_param|=7.90e+05 loss_x2y=3.0772e-01 ppl_x2y=1.36 loss_y2x=2.5523e-01 ppl_y2x=1.29 dual_loss=2.1797e+00
Validation X2Y - loss=2.3238e+00 ppl=10.21 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8396e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 408 - |param|=9.97e+02 |g_param|=7.99e+05 loss_x2y=2.9316e-01 ppl_x2y=1.34 loss_y2x=2.5260e-01 ppl_y2x=1.29 dual_loss=2.0924e+00
Validation X2Y - loss=2.3523e+00 ppl=10.51 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8895e+00 ppl=6.62 best_loss=1.0187e+00 best_ppl=2.77
Epoch 409 - |param|=9.97e+02 |g_param|=7.82e+05 loss_x2y=2.8050e-01 ppl_x2y=1.32 loss_y2x=2.3057e-01 ppl_y2x=1.26 dual_loss=1.8516e+00
Validation X2Y - loss=2.3757e+00 ppl=10.76 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8619e+00 ppl=6.44 best_loss=1.0187e+00 best_ppl=2.77
Epoch 410 - |param|=9.97e+02 |g_param|=9.99e+05 loss_x2y=2.7552e-01 ppl_x2y=1.32 loss_y2x=2.4286e-01 ppl_y2x=1.27 dual_loss=1.9592e+00
Validation X2Y - loss=2.4064e+00 ppl=11.09 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8335e+00 ppl=6.26 best_loss=1.0187e+00 best_ppl=2.77
Epoch 411 - |param|=9.98e+02 |g_param|=9.94e+05 loss_x2y=2.7290e-01 ppl_x2y=1.31 loss_y2x=2.3319e-01 ppl_y2x=1.26 dual_loss=1.8389e+00
Validation X2Y - loss=2.3798e+00 ppl=10.80 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8671e+00 ppl=6.47 best_loss=1.0187e+00 best_ppl=2.77
Epoch 412 - |param|=9.98e+02 |g_param|=9.82e+05 loss_x2y=2.5542e-01 ppl_x2y=1.29 loss_y2x=2.1090e-01 ppl_y2x=1.23 dual_loss=1.6253e+00
Validation X2Y - loss=2.3981e+00 ppl=11.00 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8721e+00 ppl=6.50 best_loss=1.0187e+00 best_ppl=2.77
Epoch 413 - |param|=9.98e+02 |g_param|=9.78e+05 loss_x2y=2.6800e-01 ppl_x2y=1.31 loss_y2x=2.2813e-01 ppl_y2x=1.26 dual_loss=1.8159e+00
Validation X2Y - loss=2.3527e+00 ppl=10.51 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8506e+00 ppl=6.36 best_loss=1.0187e+00 best_ppl=2.77
Epoch 414 - |param|=9.98e+02 |g_param|=1.00e+06 loss_x2y=2.6730e-01 ppl_x2y=1.31 loss_y2x=2.1223e-01 ppl_y2x=1.24 dual_loss=1.7298e+00
Validation X2Y - loss=2.3565e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8146e+00 ppl=6.14 best_loss=1.0187e+00 best_ppl=2.77
Epoch 415 - |param|=9.99e+02 |g_param|=8.14e+05 loss_x2y=2.5453e-01 ppl_x2y=1.29 loss_y2x=2.1056e-01 ppl_y2x=1.23 dual_loss=1.6954e+00
Validation X2Y - loss=2.3454e+00 ppl=10.44 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8134e+00 ppl=6.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 416 - |param|=9.99e+02 |g_param|=7.74e+05 loss_x2y=2.7835e-01 ppl_x2y=1.32 loss_y2x=2.2997e-01 ppl_y2x=1.26 dual_loss=1.9025e+00
Validation X2Y - loss=2.3843e+00 ppl=10.85 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8712e+00 ppl=6.50 best_loss=1.0187e+00 best_ppl=2.77
Epoch 417 - |param|=9.99e+02 |g_param|=5.23e+05 loss_x2y=2.6464e-01 ppl_x2y=1.30 loss_y2x=2.1784e-01 ppl_y2x=1.24 dual_loss=1.7149e+00
Validation X2Y - loss=2.3294e+00 ppl=10.27 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8136e+00 ppl=6.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 418 - |param|=9.99e+02 |g_param|=4.99e+05 loss_x2y=2.7092e-01 ppl_x2y=1.31 loss_y2x=2.2254e-01 ppl_y2x=1.25 dual_loss=1.7585e+00
Validation X2Y - loss=2.3117e+00 ppl=10.09 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8462e+00 ppl=6.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 419 - |param|=1.00e+03 |g_param|=5.01e+05 loss_x2y=3.3874e-01 ppl_x2y=1.40 loss_y2x=2.7558e-01 ppl_y2x=1.32 dual_loss=2.4403e+00
Validation X2Y - loss=2.3285e+00 ppl=10.26 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8303e+00 ppl=6.24 best_loss=1.0187e+00 best_ppl=2.77
Epoch 420 - |param|=1.00e+03 |g_param|=4.96e+05 loss_x2y=2.5774e-01 ppl_x2y=1.29 loss_y2x=2.1872e-01 ppl_y2x=1.24 dual_loss=1.7665e+00
Validation X2Y - loss=2.3608e+00 ppl=10.60 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8944e+00 ppl=6.65 best_loss=1.0187e+00 best_ppl=2.77
Epoch 421 - |param|=1.00e+03 |g_param|=4.86e+05 loss_x2y=2.7731e-01 ppl_x2y=1.32 loss_y2x=2.3608e-01 ppl_y2x=1.27 dual_loss=1.9159e+00
Validation X2Y - loss=2.3312e+00 ppl=10.29 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8892e+00 ppl=6.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 422 - |param|=1.00e+03 |g_param|=5.14e+05 loss_x2y=2.7901e-01 ppl_x2y=1.32 loss_y2x=2.3673e-01 ppl_y2x=1.27 dual_loss=1.9615e+00
Validation X2Y - loss=2.3181e+00 ppl=10.16 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8747e+00 ppl=6.52 best_loss=1.0187e+00 best_ppl=2.77
Epoch 423 - |param|=1.00e+03 |g_param|=4.84e+05 loss_x2y=2.7853e-01 ppl_x2y=1.32 loss_y2x=2.3729e-01 ppl_y2x=1.27 dual_loss=1.9637e+00
Validation X2Y - loss=2.2323e+00 ppl=9.32 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8689e+00 ppl=6.48 best_loss=1.0187e+00 best_ppl=2.77
Epoch 424 - |param|=1.00e+03 |g_param|=4.97e+05 loss_x2y=2.7015e-01 ppl_x2y=1.31 loss_y2x=2.2660e-01 ppl_y2x=1.25 dual_loss=1.8255e+00
Validation X2Y - loss=2.3576e+00 ppl=10.57 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8813e+00 ppl=6.56 best_loss=1.0187e+00 best_ppl=2.77
Epoch 425 - |param|=1.00e+03 |g_param|=4.91e+05 loss_x2y=3.1126e-01 ppl_x2y=1.37 loss_y2x=2.5609e-01 ppl_y2x=1.29 dual_loss=2.2576e+00
Validation X2Y - loss=2.3850e+00 ppl=10.86 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9206e+00 ppl=6.82 best_loss=1.0187e+00 best_ppl=2.77
Epoch 426 - |param|=1.00e+03 |g_param|=4.97e+05 loss_x2y=2.5247e-01 ppl_x2y=1.29 loss_y2x=2.1550e-01 ppl_y2x=1.24 dual_loss=1.7265e+00
Validation X2Y - loss=2.3542e+00 ppl=10.53 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8498e+00 ppl=6.36 best_loss=1.0187e+00 best_ppl=2.77
Epoch 427 - |param|=1.00e+03 |g_param|=4.73e+05 loss_x2y=2.7478e-01 ppl_x2y=1.32 loss_y2x=2.3035e-01 ppl_y2x=1.26 dual_loss=1.8868e+00
Validation X2Y - loss=2.2972e+00 ppl=9.95 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8999e+00 ppl=6.69 best_loss=1.0187e+00 best_ppl=2.77
Epoch 428 - |param|=1.00e+03 |g_param|=4.92e+05 loss_x2y=2.8372e-01 ppl_x2y=1.33 loss_y2x=2.4677e-01 ppl_y2x=1.28 dual_loss=2.1610e+00
Validation X2Y - loss=2.3194e+00 ppl=10.17 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8691e+00 ppl=6.48 best_loss=1.0187e+00 best_ppl=2.77
Epoch 429 - |param|=1.00e+03 |g_param|=4.81e+05 loss_x2y=2.6776e-01 ppl_x2y=1.31 loss_y2x=2.2648e-01 ppl_y2x=1.25 dual_loss=1.8260e+00
Validation X2Y - loss=2.2875e+00 ppl=9.85 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.9110e+00 ppl=6.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 430 - |param|=1.00e+03 |g_param|=4.94e+05 loss_x2y=2.5857e-01 ppl_x2y=1.30 loss_y2x=2.2403e-01 ppl_y2x=1.25 dual_loss=1.8159e+00
Validation X2Y - loss=2.3085e+00 ppl=10.06 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8867e+00 ppl=6.60 best_loss=1.0187e+00 best_ppl=2.77
Epoch 431 - |param|=1.00e+03 |g_param|=4.91e+05 loss_x2y=2.9000e-01 ppl_x2y=1.34 loss_y2x=2.4003e-01 ppl_y2x=1.27 dual_loss=1.9746e+00
Validation X2Y - loss=2.3310e+00 ppl=10.29 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8690e+00 ppl=6.48 best_loss=1.0187e+00 best_ppl=2.77
Epoch 432 - |param|=1.00e+03 |g_param|=4.93e+05 loss_x2y=2.8010e-01 ppl_x2y=1.32 loss_y2x=2.4565e-01 ppl_y2x=1.28 dual_loss=2.0358e+00
Validation X2Y - loss=2.3261e+00 ppl=10.24 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8935e+00 ppl=6.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 433 - |param|=1.00e+03 |g_param|=4.85e+05 loss_x2y=2.8616e-01 ppl_x2y=1.33 loss_y2x=2.3797e-01 ppl_y2x=1.27 dual_loss=1.9862e+00
Validation X2Y - loss=2.3076e+00 ppl=10.05 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8773e+00 ppl=6.54 best_loss=1.0187e+00 best_ppl=2.77
Epoch 434 - |param|=1.00e+03 |g_param|=4.91e+05 loss_x2y=3.3682e-01 ppl_x2y=1.40 loss_y2x=2.9467e-01 ppl_y2x=1.34 dual_loss=2.6095e+00
Validation X2Y - loss=2.3554e+00 ppl=10.54 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8598e+00 ppl=6.42 best_loss=1.0187e+00 best_ppl=2.77
Epoch 435 - |param|=1.00e+03 |g_param|=4.87e+05 loss_x2y=3.2620e-01 ppl_x2y=1.39 loss_y2x=2.5294e-01 ppl_y2x=1.29 dual_loss=2.1968e+00
Validation X2Y - loss=2.3649e+00 ppl=10.64 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8476e+00 ppl=6.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 436 - |param|=1.00e+03 |g_param|=5.05e+05 loss_x2y=2.6145e-01 ppl_x2y=1.30 loss_y2x=2.2107e-01 ppl_y2x=1.25 dual_loss=1.7893e+00
Validation X2Y - loss=2.2748e+00 ppl=9.73 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8534e+00 ppl=6.38 best_loss=1.0187e+00 best_ppl=2.77
Epoch 437 - |param|=1.00e+03 |g_param|=4.81e+05 loss_x2y=2.7020e-01 ppl_x2y=1.31 loss_y2x=2.2734e-01 ppl_y2x=1.26 dual_loss=1.9120e+00
Validation X2Y - loss=2.3627e+00 ppl=10.62 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8250e+00 ppl=6.20 best_loss=1.0187e+00 best_ppl=2.77
Epoch 438 - |param|=1.00e+03 |g_param|=4.90e+05 loss_x2y=2.7472e-01 ppl_x2y=1.32 loss_y2x=2.2181e-01 ppl_y2x=1.25 dual_loss=1.8569e+00
Validation X2Y - loss=2.3263e+00 ppl=10.24 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8231e+00 ppl=6.19 best_loss=1.0187e+00 best_ppl=2.77
Epoch 439 - |param|=1.00e+03 |g_param|=4.66e+05 loss_x2y=2.7439e-01 ppl_x2y=1.32 loss_y2x=2.2677e-01 ppl_y2x=1.25 dual_loss=1.9593e+00
Validation X2Y - loss=2.3106e+00 ppl=10.08 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9244e+00 ppl=6.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 440 - |param|=1.01e+03 |g_param|=4.97e+05 loss_x2y=2.8473e-01 ppl_x2y=1.33 loss_y2x=2.3900e-01 ppl_y2x=1.27 dual_loss=1.9935e+00
Validation X2Y - loss=2.2431e+00 ppl=9.42 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8864e+00 ppl=6.60 best_loss=1.0187e+00 best_ppl=2.77
Epoch 441 - |param|=1.01e+03 |g_param|=4.61e+05 loss_x2y=2.6357e-01 ppl_x2y=1.30 loss_y2x=2.2929e-01 ppl_y2x=1.26 dual_loss=1.9086e+00
Validation X2Y - loss=2.3174e+00 ppl=10.15 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8790e+00 ppl=6.55 best_loss=1.0187e+00 best_ppl=2.77
Epoch 442 - |param|=1.01e+03 |g_param|=4.91e+05 loss_x2y=2.6651e-01 ppl_x2y=1.31 loss_y2x=2.2862e-01 ppl_y2x=1.26 dual_loss=1.8733e+00
Validation X2Y - loss=2.3129e+00 ppl=10.10 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8671e+00 ppl=6.47 best_loss=1.0187e+00 best_ppl=2.77
Epoch 443 - |param|=1.01e+03 |g_param|=4.70e+05 loss_x2y=2.5893e-01 ppl_x2y=1.30 loss_y2x=2.1694e-01 ppl_y2x=1.24 dual_loss=1.7923e+00
Validation X2Y - loss=2.3230e+00 ppl=10.21 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9081e+00 ppl=6.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 444 - |param|=1.01e+03 |g_param|=4.91e+05 loss_x2y=2.9779e-01 ppl_x2y=1.35 loss_y2x=2.4495e-01 ppl_y2x=1.28 dual_loss=2.1900e+00
Validation X2Y - loss=2.3159e+00 ppl=10.13 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8395e+00 ppl=6.29 best_loss=1.0187e+00 best_ppl=2.77
Epoch 445 - |param|=1.01e+03 |g_param|=4.73e+05 loss_x2y=2.6790e-01 ppl_x2y=1.31 loss_y2x=2.2070e-01 ppl_y2x=1.25 dual_loss=1.8670e+00
Validation X2Y - loss=2.2864e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8321e+00 ppl=6.25 best_loss=1.0187e+00 best_ppl=2.77
Epoch 446 - |param|=1.01e+03 |g_param|=4.74e+05 loss_x2y=2.6617e-01 ppl_x2y=1.30 loss_y2x=2.2339e-01 ppl_y2x=1.25 dual_loss=1.8371e+00
Validation X2Y - loss=2.3144e+00 ppl=10.12 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8193e+00 ppl=6.17 best_loss=1.0187e+00 best_ppl=2.77
Epoch 447 - |param|=1.01e+03 |g_param|=4.51e+05 loss_x2y=2.5868e-01 ppl_x2y=1.30 loss_y2x=2.1133e-01 ppl_y2x=1.24 dual_loss=1.7360e+00
Validation X2Y - loss=2.3557e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8485e+00 ppl=6.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 448 - |param|=1.01e+03 |g_param|=7.45e+05 loss_x2y=2.6794e-01 ppl_x2y=1.31 loss_y2x=2.2193e-01 ppl_y2x=1.25 dual_loss=1.8604e+00
Validation X2Y - loss=2.3581e+00 ppl=10.57 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8740e+00 ppl=6.51 best_loss=1.0187e+00 best_ppl=2.77
Epoch 449 - |param|=1.01e+03 |g_param|=8.27e+05 loss_x2y=2.9408e-01 ppl_x2y=1.34 loss_y2x=2.6140e-01 ppl_y2x=1.30 dual_loss=2.1561e+00
Validation X2Y - loss=2.3367e+00 ppl=10.35 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9063e+00 ppl=6.73 best_loss=1.0187e+00 best_ppl=2.77
Epoch 450 - |param|=1.01e+03 |g_param|=9.91e+05 loss_x2y=2.9069e-01 ppl_x2y=1.34 loss_y2x=2.5302e-01 ppl_y2x=1.29 dual_loss=2.2347e+00
Validation X2Y - loss=2.3447e+00 ppl=10.43 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8796e+00 ppl=6.55 best_loss=1.0187e+00 best_ppl=2.77
Epoch 451 - |param|=1.01e+03 |g_param|=9.47e+05 loss_x2y=2.8926e-01 ppl_x2y=1.34 loss_y2x=2.4868e-01 ppl_y2x=1.28 dual_loss=2.2190e+00
Validation X2Y - loss=2.3108e+00 ppl=10.08 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8875e+00 ppl=6.60 best_loss=1.0187e+00 best_ppl=2.77
Epoch 452 - |param|=1.01e+03 |g_param|=9.69e+05 loss_x2y=2.7267e-01 ppl_x2y=1.31 loss_y2x=2.3009e-01 ppl_y2x=1.26 dual_loss=1.9099e+00
Validation X2Y - loss=2.3530e+00 ppl=10.52 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8971e+00 ppl=6.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 453 - |param|=1.01e+03 |g_param|=9.12e+05 loss_x2y=2.6054e-01 ppl_x2y=1.30 loss_y2x=2.3045e-01 ppl_y2x=1.26 dual_loss=1.8837e+00
Validation X2Y - loss=2.3564e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9363e+00 ppl=6.93 best_loss=1.0187e+00 best_ppl=2.77
Epoch 454 - |param|=1.01e+03 |g_param|=7.83e+05 loss_x2y=2.6141e-01 ppl_x2y=1.30 loss_y2x=2.2806e-01 ppl_y2x=1.26 dual_loss=1.8891e+00
Validation X2Y - loss=2.3496e+00 ppl=10.48 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9302e+00 ppl=6.89 best_loss=1.0187e+00 best_ppl=2.77
Epoch 455 - |param|=1.01e+03 |g_param|=7.34e+05 loss_x2y=2.8918e-01 ppl_x2y=1.34 loss_y2x=2.4166e-01 ppl_y2x=1.27 dual_loss=2.1242e+00
Validation X2Y - loss=2.3631e+00 ppl=10.62 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8917e+00 ppl=6.63 best_loss=1.0187e+00 best_ppl=2.77
Epoch 456 - |param|=1.01e+03 |g_param|=7.54e+05 loss_x2y=2.6684e-01 ppl_x2y=1.31 loss_y2x=2.4848e-01 ppl_y2x=1.28 dual_loss=2.1858e+00
Validation X2Y - loss=2.3257e+00 ppl=10.23 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8468e+00 ppl=6.34 best_loss=1.0187e+00 best_ppl=2.77
Epoch 457 - |param|=1.01e+03 |g_param|=7.24e+05 loss_x2y=2.9011e-01 ppl_x2y=1.34 loss_y2x=2.4938e-01 ppl_y2x=1.28 dual_loss=2.0100e+00
Validation X2Y - loss=2.3654e+00 ppl=10.65 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8662e+00 ppl=6.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 458 - |param|=1.01e+03 |g_param|=7.59e+05 loss_x2y=2.9757e-01 ppl_x2y=1.35 loss_y2x=2.5938e-01 ppl_y2x=1.30 dual_loss=2.4534e+00
Validation X2Y - loss=2.3423e+00 ppl=10.40 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9237e+00 ppl=6.85 best_loss=1.0187e+00 best_ppl=2.77
Epoch 459 - |param|=1.01e+03 |g_param|=7.48e+05 loss_x2y=2.9343e-01 ppl_x2y=1.34 loss_y2x=2.5903e-01 ppl_y2x=1.30 dual_loss=2.3799e+00
Validation X2Y - loss=2.3087e+00 ppl=10.06 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9105e+00 ppl=6.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 460 - |param|=1.01e+03 |g_param|=7.12e+05 loss_x2y=2.6599e-01 ppl_x2y=1.30 loss_y2x=2.1510e-01 ppl_y2x=1.24 dual_loss=1.7894e+00
Validation X2Y - loss=2.3773e+00 ppl=10.78 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8653e+00 ppl=6.46 best_loss=1.0187e+00 best_ppl=2.77
Epoch 461 - |param|=1.01e+03 |g_param|=7.36e+05 loss_x2y=3.0965e-01 ppl_x2y=1.36 loss_y2x=2.5337e-01 ppl_y2x=1.29 dual_loss=2.2712e+00
Validation X2Y - loss=2.3166e+00 ppl=10.14 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8925e+00 ppl=6.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 462 - |param|=1.01e+03 |g_param|=7.26e+05 loss_x2y=2.7073e-01 ppl_x2y=1.31 loss_y2x=2.2349e-01 ppl_y2x=1.25 dual_loss=1.9126e+00
Validation X2Y - loss=2.3558e+00 ppl=10.55 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8973e+00 ppl=6.67 best_loss=1.0187e+00 best_ppl=2.77
Epoch 463 - |param|=1.01e+03 |g_param|=7.25e+05 loss_x2y=2.7802e-01 ppl_x2y=1.32 loss_y2x=2.4122e-01 ppl_y2x=1.27 dual_loss=1.9174e+00
Validation X2Y - loss=2.3294e+00 ppl=10.27 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9276e+00 ppl=6.87 best_loss=1.0187e+00 best_ppl=2.77
Epoch 464 - |param|=1.01e+03 |g_param|=7.38e+05 loss_x2y=2.7952e-01 ppl_x2y=1.32 loss_y2x=2.2681e-01 ppl_y2x=1.25 dual_loss=1.9551e+00
Validation X2Y - loss=2.3872e+00 ppl=10.88 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9393e+00 ppl=6.95 best_loss=1.0187e+00 best_ppl=2.77
Epoch 465 - |param|=1.01e+03 |g_param|=7.85e+05 loss_x2y=3.1217e-01 ppl_x2y=1.37 loss_y2x=3.1320e-01 ppl_y2x=1.37 dual_loss=2.8866e+00
Validation X2Y - loss=2.3850e+00 ppl=10.86 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9774e+00 ppl=7.22 best_loss=1.0187e+00 best_ppl=2.77
Epoch 466 - |param|=1.01e+03 |g_param|=7.19e+05 loss_x2y=2.6988e-01 ppl_x2y=1.31 loss_y2x=2.3695e-01 ppl_y2x=1.27 dual_loss=2.0625e+00
Validation X2Y - loss=2.3969e+00 ppl=10.99 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9130e+00 ppl=6.77 best_loss=1.0187e+00 best_ppl=2.77
Epoch 467 - |param|=1.01e+03 |g_param|=7.22e+05 loss_x2y=2.6514e-01 ppl_x2y=1.30 loss_y2x=2.2265e-01 ppl_y2x=1.25 dual_loss=1.8453e+00
Validation X2Y - loss=2.3627e+00 ppl=10.62 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9073e+00 ppl=6.74 best_loss=1.0187e+00 best_ppl=2.77
Epoch 468 - |param|=1.01e+03 |g_param|=7.47e+05 loss_x2y=2.7626e-01 ppl_x2y=1.32 loss_y2x=2.4677e-01 ppl_y2x=1.28 dual_loss=2.2093e+00
Validation X2Y - loss=2.3784e+00 ppl=10.79 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9113e+00 ppl=6.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 469 - |param|=1.01e+03 |g_param|=6.99e+05 loss_x2y=3.2141e-01 ppl_x2y=1.38 loss_y2x=2.8824e-01 ppl_y2x=1.33 dual_loss=2.4975e+00
Validation X2Y - loss=2.3775e+00 ppl=10.78 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9151e+00 ppl=6.79 best_loss=1.0187e+00 best_ppl=2.77
Epoch 470 - |param|=1.01e+03 |g_param|=7.29e+05 loss_x2y=2.5567e-01 ppl_x2y=1.29 loss_y2x=2.1845e-01 ppl_y2x=1.24 dual_loss=1.8581e+00
Validation X2Y - loss=2.3583e+00 ppl=10.57 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8696e+00 ppl=6.49 best_loss=1.0187e+00 best_ppl=2.77
Epoch 471 - |param|=1.01e+03 |g_param|=7.17e+05 loss_x2y=3.4554e-01 ppl_x2y=1.41 loss_y2x=2.8338e-01 ppl_y2x=1.33 dual_loss=2.7042e+00
Validation X2Y - loss=2.3672e+00 ppl=10.67 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9221e+00 ppl=6.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 472 - |param|=1.01e+03 |g_param|=7.38e+05 loss_x2y=2.9082e-01 ppl_x2y=1.34 loss_y2x=2.3832e-01 ppl_y2x=1.27 dual_loss=2.0360e+00
Validation X2Y - loss=2.3553e+00 ppl=10.54 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9563e+00 ppl=7.07 best_loss=1.0187e+00 best_ppl=2.77
Epoch 473 - |param|=1.01e+03 |g_param|=7.31e+05 loss_x2y=2.8665e-01 ppl_x2y=1.33 loss_y2x=2.3549e-01 ppl_y2x=1.27 dual_loss=2.0343e+00
Validation X2Y - loss=2.3702e+00 ppl=10.70 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8985e+00 ppl=6.68 best_loss=1.0187e+00 best_ppl=2.77
Epoch 474 - |param|=1.01e+03 |g_param|=7.38e+05 loss_x2y=2.6529e-01 ppl_x2y=1.30 loss_y2x=2.3134e-01 ppl_y2x=1.26 dual_loss=1.9858e+00
Validation X2Y - loss=2.3941e+00 ppl=10.96 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9527e+00 ppl=7.05 best_loss=1.0187e+00 best_ppl=2.77
Epoch 475 - |param|=1.01e+03 |g_param|=6.91e+05 loss_x2y=2.6159e-01 ppl_x2y=1.30 loss_y2x=2.1591e-01 ppl_y2x=1.24 dual_loss=1.8055e+00
Validation X2Y - loss=2.3824e+00 ppl=10.83 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9537e+00 ppl=7.06 best_loss=1.0187e+00 best_ppl=2.77
Epoch 476 - |param|=1.01e+03 |g_param|=7.37e+05 loss_x2y=2.3680e-01 ppl_x2y=1.27 loss_y2x=2.0626e-01 ppl_y2x=1.23 dual_loss=1.7195e+00
Validation X2Y - loss=2.2866e+00 ppl=9.84 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.9108e+00 ppl=6.76 best_loss=1.0187e+00 best_ppl=2.77
Epoch 477 - |param|=1.01e+03 |g_param|=7.16e+05 loss_x2y=2.6244e-01 ppl_x2y=1.30 loss_y2x=2.1691e-01 ppl_y2x=1.24 dual_loss=1.8249e+00
Validation X2Y - loss=2.3134e+00 ppl=10.11 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8931e+00 ppl=6.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 478 - |param|=1.02e+03 |g_param|=7.36e+05 loss_x2y=2.5844e-01 ppl_x2y=1.29 loss_y2x=2.2351e-01 ppl_y2x=1.25 dual_loss=1.8878e+00
Validation X2Y - loss=2.2837e+00 ppl=9.81 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.8829e+00 ppl=6.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 479 - |param|=1.02e+03 |g_param|=7.22e+05 loss_x2y=2.8234e-01 ppl_x2y=1.33 loss_y2x=2.4461e-01 ppl_y2x=1.28 dual_loss=2.2542e+00
Validation X2Y - loss=2.3429e+00 ppl=10.41 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8635e+00 ppl=6.45 best_loss=1.0187e+00 best_ppl=2.77
Epoch 480 - |param|=1.02e+03 |g_param|=7.38e+05 loss_x2y=2.6906e-01 ppl_x2y=1.31 loss_y2x=2.2541e-01 ppl_y2x=1.25 dual_loss=1.8973e+00
Validation X2Y - loss=2.3387e+00 ppl=10.37 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8925e+00 ppl=6.64 best_loss=1.0187e+00 best_ppl=2.77
Epoch 481 - |param|=1.02e+03 |g_param|=6.95e+05 loss_x2y=2.7960e-01 ppl_x2y=1.32 loss_y2x=2.3955e-01 ppl_y2x=1.27 dual_loss=2.1228e+00
Validation X2Y - loss=2.3343e+00 ppl=10.32 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9252e+00 ppl=6.86 best_loss=1.0187e+00 best_ppl=2.77
Epoch 482 - |param|=1.02e+03 |g_param|=7.25e+05 loss_x2y=2.6421e-01 ppl_x2y=1.30 loss_y2x=2.2015e-01 ppl_y2x=1.25 dual_loss=1.8828e+00
Validation X2Y - loss=2.2911e+00 ppl=9.89 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.9232e+00 ppl=6.84 best_loss=1.0187e+00 best_ppl=2.77
Epoch 483 - |param|=1.02e+03 |g_param|=7.11e+05 loss_x2y=2.7446e-01 ppl_x2y=1.32 loss_y2x=2.3852e-01 ppl_y2x=1.27 dual_loss=2.1314e+00
Validation X2Y - loss=2.3649e+00 ppl=10.64 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8921e+00 ppl=6.63 best_loss=1.0187e+00 best_ppl=2.77
Epoch 484 - |param|=1.02e+03 |g_param|=7.32e+05 loss_x2y=2.5155e-01 ppl_x2y=1.29 loss_y2x=2.1940e-01 ppl_y2x=1.25 dual_loss=1.8369e+00
Validation X2Y - loss=2.3269e+00 ppl=10.25 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9033e+00 ppl=6.71 best_loss=1.0187e+00 best_ppl=2.77
Epoch 485 - |param|=1.02e+03 |g_param|=7.06e+05 loss_x2y=2.4571e-01 ppl_x2y=1.28 loss_y2x=2.1819e-01 ppl_y2x=1.24 dual_loss=1.8835e+00
Validation X2Y - loss=2.3451e+00 ppl=10.43 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9261e+00 ppl=6.86 best_loss=1.0187e+00 best_ppl=2.77
Epoch 486 - |param|=1.02e+03 |g_param|=7.63e+05 loss_x2y=2.6859e-01 ppl_x2y=1.31 loss_y2x=2.2710e-01 ppl_y2x=1.25 dual_loss=1.9272e+00
Validation X2Y - loss=2.3248e+00 ppl=10.22 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8953e+00 ppl=6.65 best_loss=1.0187e+00 best_ppl=2.77
Epoch 487 - |param|=1.02e+03 |g_param|=8.98e+05 loss_x2y=2.5316e-01 ppl_x2y=1.29 loss_y2x=2.1396e-01 ppl_y2x=1.24 dual_loss=1.8573e+00
Validation X2Y - loss=2.3769e+00 ppl=10.77 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8823e+00 ppl=6.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 488 - |param|=1.02e+03 |g_param|=7.90e+05 loss_x2y=2.6372e-01 ppl_x2y=1.30 loss_y2x=2.2973e-01 ppl_y2x=1.26 dual_loss=1.9028e+00
Validation X2Y - loss=2.3168e+00 ppl=10.14 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8888e+00 ppl=6.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 489 - |param|=1.02e+03 |g_param|=7.02e+05 loss_x2y=2.5780e-01 ppl_x2y=1.29 loss_y2x=2.2323e-01 ppl_y2x=1.25 dual_loss=1.8654e+00
Validation X2Y - loss=2.3025e+00 ppl=10.00 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8812e+00 ppl=6.56 best_loss=1.0187e+00 best_ppl=2.77
Epoch 490 - |param|=1.02e+03 |g_param|=7.52e+05 loss_x2y=3.2541e-01 ppl_x2y=1.38 loss_y2x=2.7886e-01 ppl_y2x=1.32 dual_loss=2.5731e+00
Validation X2Y - loss=2.3373e+00 ppl=10.35 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9643e+00 ppl=7.13 best_loss=1.0187e+00 best_ppl=2.77
Epoch 491 - |param|=1.02e+03 |g_param|=6.94e+05 loss_x2y=2.5039e-01 ppl_x2y=1.28 loss_y2x=2.2721e-01 ppl_y2x=1.26 dual_loss=1.8909e+00
Validation X2Y - loss=2.2961e+00 ppl=9.93 best_loss=1.3035e+00 best_ppl=3.68                                            
Validation Y2X - loss=1.9536e+00 ppl=7.05 best_loss=1.0187e+00 best_ppl=2.77
Epoch 492 - |param|=1.02e+03 |g_param|=7.41e+05 loss_x2y=2.5834e-01 ppl_x2y=1.29 loss_y2x=2.2613e-01 ppl_y2x=1.25 dual_loss=1.9940e+00
Validation X2Y - loss=2.3378e+00 ppl=10.36 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9311e+00 ppl=6.90 best_loss=1.0187e+00 best_ppl=2.77
Epoch 493 - |param|=1.02e+03 |g_param|=7.15e+05 loss_x2y=2.8883e-01 ppl_x2y=1.33 loss_y2x=2.4037e-01 ppl_y2x=1.27 dual_loss=2.2436e+00
Validation X2Y - loss=2.3841e+00 ppl=10.85 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9427e+00 ppl=6.98 best_loss=1.0187e+00 best_ppl=2.77
Epoch 494 - |param|=1.02e+03 |g_param|=7.42e+05 loss_x2y=2.5519e-01 ppl_x2y=1.29 loss_y2x=2.2360e-01 ppl_y2x=1.25 dual_loss=1.9738e+00
Validation X2Y - loss=2.3302e+00 ppl=10.28 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9683e+00 ppl=7.16 best_loss=1.0187e+00 best_ppl=2.77
Epoch 495 - |param|=1.02e+03 |g_param|=7.00e+05 loss_x2y=2.7387e-01 ppl_x2y=1.32 loss_y2x=2.1579e-01 ppl_y2x=1.24 dual_loss=1.8636e+00
Validation X2Y - loss=2.3550e+00 ppl=10.54 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9942e+00 ppl=7.35 best_loss=1.0187e+00 best_ppl=2.77
Epoch 496 - |param|=1.02e+03 |g_param|=7.26e+05 loss_x2y=2.8551e-01 ppl_x2y=1.33 loss_y2x=2.4102e-01 ppl_y2x=1.27 dual_loss=2.1500e+00
Validation X2Y - loss=2.3863e+00 ppl=10.87 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8882e+00 ppl=6.61 best_loss=1.0187e+00 best_ppl=2.77
Epoch 497 - |param|=1.02e+03 |g_param|=7.13e+05 loss_x2y=2.8644e-01 ppl_x2y=1.33 loss_y2x=2.3635e-01 ppl_y2x=1.27 dual_loss=2.1300e+00
Validation X2Y - loss=2.3505e+00 ppl=10.49 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8831e+00 ppl=6.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 498 - |param|=1.02e+03 |g_param|=7.58e+05 loss_x2y=2.9950e-01 ppl_x2y=1.35 loss_y2x=2.4526e-01 ppl_y2x=1.28 dual_loss=2.2248e+00
Validation X2Y - loss=2.3769e+00 ppl=10.77 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8820e+00 ppl=6.57 best_loss=1.0187e+00 best_ppl=2.77
Epoch 499 - |param|=1.02e+03 |g_param|=6.76e+05 loss_x2y=2.4074e-01 ppl_x2y=1.27 loss_y2x=2.1342e-01 ppl_y2x=1.24 dual_loss=1.8472e+00
Validation X2Y - loss=2.3548e+00 ppl=10.54 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.9005e+00 ppl=6.69 best_loss=1.0187e+00 best_ppl=2.77
Epoch 500 - |param|=1.02e+03 |g_param|=7.43e+05 loss_x2y=2.8842e-01 ppl_x2y=1.33 loss_y2x=2.4920e-01 ppl_y2x=1.28 dual_loss=2.2342e+00
Validation X2Y - loss=2.3257e+00 ppl=10.23 best_loss=1.3035e+00 best_ppl=3.68                                           
Validation Y2X - loss=1.8949e+00 ppl=6.65 best_loss=1.0187e+00 best_ppl=2.77

real	163m45.981s
user	157m22.948s
sys	3m1.726s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Testing/Evaluation for Seq2Seq-DSL 500 Models (my-bk, bk-my)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-xy-transformer-mybk-500epoch.sh
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-500epoch
Evaluation result for the model: dsl-model-mybk.01.4.45-85.22.4.10-60.24.3.54-34.35.3.21-24.77.pth, mybk
BLEU = 2.20, 11.4/2.8/1.3/0.6 (BP=1.000, ratio=1.838, hyp_len=21013, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.45-85.22.4.10-60.24.3.54-34.35.3.21-24.77.pth, bkmy
BLEU = 4.49, 30.1/8.9/2.8/0.7 (BP=0.920, ratio=0.923, hyp_len=11290, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.67-39.16.3.17-23.90.3.00-20.18.2.68-14.53.pth, mybk
BLEU = 4.52, 21.8/6.5/2.6/1.1 (BP=1.000, ratio=1.198, hyp_len=13698, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.67-39.16.3.17-23.90.3.00-20.18.2.68-14.53.pth, bkmy
BLEU = 6.49, 32.8/10.8/4.0/1.5 (BP=0.958, ratio=0.959, hyp_len=11724, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.23-25.40.2.86-17.47.2.60-13.51.2.34-10.43.pth, mybk
BLEU = 5.61, 24.0/8.0/3.3/1.5 (BP=1.000, ratio=1.215, hyp_len=13886, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.23-25.40.2.86-17.47.2.60-13.51.2.34-10.43.pth, bkmy
BLEU = 8.58, 35.0/13.8/5.5/2.0 (BP=1.000, ratio=1.108, hyp_len=13553, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.2.96-19.37.2.58-13.23.2.29-9.84.2.00-7.42.pth, mybk
BLEU = 5.35, 19.2/7.4/3.5/1.7 (BP=1.000, ratio=1.826, hyp_len=20878, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.2.96-19.37.2.58-13.23.2.29-9.84.2.00-7.42.pth, bkmy
BLEU = 14.04, 43.7/20.5/9.9/4.9 (BP=0.973, ratio=0.973, hyp_len=11900, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.82-16.72.2.49-12.10.2.08-7.97.1.84-6.28.pth, mybk
BLEU = 13.26, 38.0/17.6/9.2/5.0 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.82-16.72.2.49-12.10.2.08-7.97.1.84-6.28.pth, bkmy
BLEU = 16.00, 44.3/21.6/11.2/6.1 (BP=1.000, ratio=1.022, hyp_len=12501, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.54-12.66.2.22-9.16.1.84-6.27.1.63-5.09.pth, mybk
BLEU = 16.02, 40.9/20.6/11.6/6.8 (BP=1.000, ratio=1.144, hyp_len=13078, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.54-12.66.2.22-9.16.1.84-6.27.1.63-5.09.pth, bkmy
BLEU = 20.13, 47.8/26.0/14.8/8.9 (BP=1.000, ratio=1.067, hyp_len=13048, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.36.2.12-8.31.1.73-5.64.1.50-4.47.pth, mybk
BLEU = 9.71, 24.4/12.6/7.2/4.0 (BP=1.000, ratio=2.032, hyp_len=23227, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.36.2.12-8.31.1.73-5.64.1.50-4.47.pth, bkmy
BLEU = 25.91, 54.8/32.4/19.8/12.8 (BP=1.000, ratio=1.019, hyp_len=12467, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.29-9.90.2.01-7.45.1.61-5.00.1.38-3.96.pth, mybk
BLEU = 21.73, 48.2/26.6/16.5/10.5 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.29-9.90.2.01-7.45.1.61-5.00.1.38-3.96.pth, bkmy
BLEU = 29.23, 56.8/35.4/23.0/15.8 (BP=1.000, ratio=1.038, hyp_len=12690, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.17-8.73.1.89-6.60.1.54-4.66.1.30-3.67.pth, mybk
BLEU = 25.82, 53.9/31.1/20.0/13.2 (BP=1.000, ratio=1.015, hyp_len=11600, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.17-8.73.1.89-6.60.1.54-4.66.1.30-3.67.pth, bkmy
BLEU = 30.67, 56.8/36.7/24.5/17.3 (BP=1.000, ratio=1.074, hyp_len=13133, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.100.0.54-1.71.0.43-1.53.1.91-6.78.1.43-4.19.pth, mybk
BLEU = 29.80, 56.6/35.0/23.6/16.9 (BP=1.000, ratio=1.070, hyp_len=12234, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.100.0.54-1.71.0.43-1.53.1.91-6.78.1.43-4.19.pth, bkmy
BLEU = 33.53, 58.8/38.9/27.3/20.2 (BP=1.000, ratio=1.064, hyp_len=13011, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.101.0.50-1.65.0.42-1.52.1.93-6.87.1.45-4.27.pth, mybk
BLEU = 28.71, 55.0/33.8/22.7/16.1 (BP=1.000, ratio=1.080, hyp_len=12349, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.101.0.50-1.65.0.42-1.52.1.93-6.87.1.45-4.27.pth, bkmy
BLEU = 32.99, 57.7/38.3/27.0/19.8 (BP=1.000, ratio=1.104, hyp_len=13497, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.102.0.54-1.71.0.43-1.53.1.87-6.50.1.49-4.43.pth, mybk
BLEU = 31.22, 57.5/36.2/25.1/18.2 (BP=1.000, ratio=1.060, hyp_len=12118, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.102.0.54-1.71.0.43-1.53.1.87-6.50.1.49-4.43.pth, bkmy
BLEU = 31.45, 57.3/37.4/25.4/18.0 (BP=1.000, ratio=1.114, hyp_len=13629, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.12-8.36.1.83-6.23.1.47-4.37.1.24-3.46.pth, mybk
BLEU = 27.12, 55.5/32.5/21.0/14.3 (BP=1.000, ratio=1.029, hyp_len=11763, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.12-8.36.1.83-6.23.1.47-4.37.1.24-3.46.pth, bkmy
BLEU = 34.61, 61.6/40.9/28.2/20.2 (BP=1.000, ratio=1.005, hyp_len=12287, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.103.0.50-1.65.0.41-1.51.1.87-6.52.1.44-4.24.pth, mybk
BLEU = 28.11, 54.5/32.9/22.1/15.7 (BP=1.000, ratio=1.101, hyp_len=12586, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.103.0.50-1.65.0.41-1.51.1.87-6.52.1.44-4.24.pth, bkmy
BLEU = 33.09, 58.6/38.7/26.9/19.7 (BP=1.000, ratio=1.072, hyp_len=13107, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.104.0.51-1.67.0.43-1.54.1.86-6.44.1.44-4.21.pth, mybk
BLEU = 29.69, 56.2/34.8/23.6/16.8 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.104.0.51-1.67.0.43-1.54.1.86-6.44.1.44-4.21.pth, bkmy
BLEU = 33.11, 58.1/38.4/27.0/20.0 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.105.0.51-1.67.0.41-1.51.1.89-6.62.1.45-4.26.pth, mybk
BLEU = 28.86, 55.4/33.9/22.9/16.2 (BP=1.000, ratio=1.077, hyp_len=12317, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.105.0.51-1.67.0.41-1.51.1.89-6.62.1.45-4.26.pth, bkmy
BLEU = 32.36, 57.8/38.1/26.3/18.9 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.106.0.52-1.68.0.42-1.51.1.88-6.53.1.47-4.33.pth, mybk
BLEU = 29.65, 56.1/34.6/23.6/16.8 (BP=1.000, ratio=1.076, hyp_len=12302, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.106.0.52-1.68.0.42-1.51.1.88-6.53.1.47-4.33.pth, bkmy
BLEU = 30.61, 55.4/35.8/24.7/17.9 (BP=1.000, ratio=1.140, hyp_len=13948, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.107.0.52-1.69.0.41-1.50.1.93-6.89.1.45-4.25.pth, mybk
BLEU = 28.45, 54.7/33.6/22.5/15.9 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.107.0.52-1.69.0.41-1.50.1.93-6.89.1.45-4.25.pth, bkmy
BLEU = 32.44, 57.9/37.8/26.3/19.3 (BP=1.000, ratio=1.087, hyp_len=13292, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.108.0.53-1.70.0.44-1.55.1.88-6.52.1.47-4.36.pth, mybk
BLEU = 29.28, 56.3/34.5/23.1/16.4 (BP=1.000, ratio=1.081, hyp_len=12357, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.108.0.53-1.70.0.44-1.55.1.88-6.52.1.47-4.36.pth, bkmy
BLEU = 32.59, 58.4/38.4/26.4/19.0 (BP=1.000, ratio=1.087, hyp_len=13294, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.109.0.48-1.62.0.40-1.49.1.91-6.75.1.44-4.21.pth, mybk
BLEU = 28.63, 54.7/33.6/22.8/16.0 (BP=1.000, ratio=1.102, hyp_len=12595, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.109.0.48-1.62.0.40-1.49.1.91-6.75.1.44-4.21.pth, bkmy
BLEU = 32.47, 57.8/37.8/26.4/19.2 (BP=1.000, ratio=1.101, hyp_len=13461, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.110.0.50-1.65.0.39-1.48.1.94-6.97.1.45-4.28.pth, mybk
BLEU = 29.32, 55.3/34.2/23.3/16.8 (BP=1.000, ratio=1.076, hyp_len=12303, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.110.0.50-1.65.0.39-1.48.1.94-6.97.1.45-4.28.pth, bkmy
BLEU = 34.71, 60.1/40.1/28.4/21.2 (BP=1.000, ratio=1.068, hyp_len=13061, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.111.0.50-1.64.0.40-1.50.1.94-6.98.1.43-4.16.pth, mybk
BLEU = 29.95, 56.6/35.0/23.8/17.1 (BP=1.000, ratio=1.064, hyp_len=12158, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.111.0.50-1.64.0.40-1.50.1.94-6.98.1.43-4.16.pth, bkmy
BLEU = 32.21, 57.7/37.6/26.1/19.0 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.112.0.57-1.77.0.45-1.57.1.98-7.24.1.49-4.42.pth, mybk
BLEU = 28.29, 54.8/33.4/22.3/15.7 (BP=1.000, ratio=1.095, hyp_len=12514, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.112.0.57-1.77.0.45-1.57.1.98-7.24.1.49-4.42.pth, bkmy
BLEU = 31.63, 56.8/36.8/25.6/18.7 (BP=1.000, ratio=1.103, hyp_len=13493, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.10-8.15.1.77-5.87.1.45-4.26.1.20-3.33.pth, mybk
BLEU = 23.97, 49.1/28.9/18.6/12.5 (BP=1.000, ratio=1.183, hyp_len=13523, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.10-8.15.1.77-5.87.1.45-4.26.1.20-3.33.pth, bkmy
BLEU = 35.69, 62.6/42.1/29.3/21.0 (BP=1.000, ratio=1.025, hyp_len=12537, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.113.0.48-1.62.0.41-1.50.1.94-6.94.1.47-4.35.pth, mybk
BLEU = 28.70, 55.2/33.7/22.7/16.1 (BP=1.000, ratio=1.083, hyp_len=12384, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.113.0.48-1.62.0.41-1.50.1.94-6.94.1.47-4.35.pth, bkmy
BLEU = 34.04, 59.4/39.8/27.8/20.4 (BP=1.000, ratio=1.058, hyp_len=12935, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.114.0.47-1.60.0.39-1.48.2.01-7.44.1.45-4.27.pth, mybk
BLEU = 28.20, 54.5/33.0/22.2/15.8 (BP=1.000, ratio=1.054, hyp_len=12051, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.114.0.47-1.60.0.39-1.48.2.01-7.44.1.45-4.27.pth, bkmy
BLEU = 34.27, 59.2/39.7/28.2/20.8 (BP=1.000, ratio=1.070, hyp_len=13086, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.115.0.48-1.62.0.39-1.47.1.94-6.98.1.55-4.69.pth, mybk
BLEU = 30.20, 56.4/35.1/24.0/17.5 (BP=1.000, ratio=1.051, hyp_len=12019, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.115.0.48-1.62.0.39-1.47.1.94-6.98.1.55-4.69.pth, bkmy
BLEU = 32.45, 58.0/37.8/26.3/19.2 (BP=1.000, ratio=1.085, hyp_len=13265, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.116.0.50-1.65.0.39-1.48.1.95-7.05.1.54-4.67.pth, mybk
BLEU = 28.85, 54.8/33.5/22.9/16.4 (BP=1.000, ratio=1.078, hyp_len=12325, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.116.0.50-1.65.0.39-1.48.1.95-7.05.1.54-4.67.pth, bkmy
BLEU = 30.98, 55.5/36.1/25.1/18.3 (BP=1.000, ratio=1.122, hyp_len=13720, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.117.0.48-1.61.0.37-1.45.1.98-7.28.1.52-4.56.pth, mybk
BLEU = 29.54, 55.6/34.3/23.5/17.0 (BP=1.000, ratio=1.061, hyp_len=12126, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.117.0.48-1.61.0.37-1.45.1.98-7.28.1.52-4.56.pth, bkmy
BLEU = 32.53, 58.2/37.8/26.4/19.3 (BP=1.000, ratio=1.071, hyp_len=13105, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.118.0.48-1.62.0.39-1.47.1.95-7.02.1.53-4.62.pth, mybk
BLEU = 27.31, 53.4/32.3/21.5/15.0 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.118.0.48-1.62.0.39-1.47.1.95-7.02.1.53-4.62.pth, bkmy
BLEU = 32.70, 57.9/38.1/26.7/19.4 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.119.0.47-1.60.0.38-1.47.1.97-7.14.1.52-4.58.pth, mybk
BLEU = 29.17, 56.0/34.3/23.1/16.3 (BP=1.000, ratio=1.065, hyp_len=12176, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.119.0.47-1.60.0.38-1.47.1.97-7.14.1.52-4.58.pth, bkmy
BLEU = 32.32, 58.0/37.7/26.2/19.0 (BP=1.000, ratio=1.093, hyp_len=13371, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.120.0.47-1.60.0.41-1.50.1.93-6.92.1.53-4.63.pth, mybk
BLEU = 28.57, 54.9/33.6/22.6/16.0 (BP=1.000, ratio=1.079, hyp_len=12331, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.120.0.47-1.60.0.41-1.50.1.93-6.92.1.53-4.63.pth, bkmy
BLEU = 31.25, 56.6/36.5/25.3/18.3 (BP=1.000, ratio=1.104, hyp_len=13507, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.121.0.48-1.62.0.38-1.46.1.98-7.25.1.48-4.41.pth, mybk
BLEU = 27.45, 53.5/32.4/21.7/15.1 (BP=1.000, ratio=1.095, hyp_len=12522, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.121.0.48-1.62.0.38-1.46.1.98-7.25.1.48-4.41.pth, bkmy
BLEU = 32.26, 57.0/37.3/26.3/19.4 (BP=1.000, ratio=1.089, hyp_len=13317, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.122.0.46-1.58.0.37-1.45.2.04-7.67.1.50-4.46.pth, mybk
BLEU = 26.92, 52.8/31.7/21.2/14.8 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.122.0.46-1.58.0.37-1.45.2.04-7.67.1.50-4.46.pth, bkmy
BLEU = 31.66, 56.9/37.0/25.7/18.6 (BP=1.000, ratio=1.086, hyp_len=13278, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.2.05-7.73.1.77-5.89.1.44-4.21.1.15-3.17.pth, mybk
BLEU = 25.01, 50.0/30.1/19.7/13.2 (BP=1.000, ratio=1.175, hyp_len=13435, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.2.05-7.73.1.77-5.89.1.44-4.21.1.15-3.17.pth, bkmy
BLEU = 36.27, 61.5/42.6/30.1/21.9 (BP=1.000, ratio=1.059, hyp_len=12958, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.123.0.46-1.58.0.37-1.45.2.01-7.49.1.54-4.65.pth, mybk
BLEU = 27.63, 54.2/32.7/21.8/15.1 (BP=1.000, ratio=1.075, hyp_len=12295, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.123.0.46-1.58.0.37-1.45.2.01-7.49.1.54-4.65.pth, bkmy
BLEU = 32.20, 57.9/37.5/26.0/19.0 (BP=1.000, ratio=1.092, hyp_len=13361, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.124.0.48-1.61.0.40-1.49.1.99-7.30.1.55-4.69.pth, mybk
BLEU = 27.68, 53.4/32.6/21.9/15.4 (BP=1.000, ratio=1.094, hyp_len=12502, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.124.0.48-1.61.0.40-1.49.1.99-7.30.1.55-4.69.pth, bkmy
BLEU = 31.60, 56.8/36.9/25.6/18.5 (BP=1.000, ratio=1.114, hyp_len=13622, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.125.0.49-1.64.0.39-1.47.2.00-7.41.1.56-4.74.pth, mybk
BLEU = 29.10, 54.7/34.1/23.3/16.5 (BP=1.000, ratio=1.066, hyp_len=12181, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.125.0.49-1.64.0.39-1.47.2.00-7.41.1.56-4.74.pth, bkmy
BLEU = 32.17, 57.7/37.4/26.1/19.0 (BP=1.000, ratio=1.071, hyp_len=13102, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.126.0.46-1.59.0.37-1.45.1.99-7.30.1.58-4.83.pth, mybk
BLEU = 28.40, 54.3/33.5/22.6/15.8 (BP=1.000, ratio=1.099, hyp_len=12567, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.126.0.46-1.59.0.37-1.45.1.99-7.30.1.58-4.83.pth, bkmy
BLEU = 32.73, 58.2/38.3/26.6/19.4 (BP=1.000, ratio=1.074, hyp_len=13134, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.127.0.45-1.58.0.37-1.44.2.03-7.64.1.59-4.92.pth, mybk
BLEU = 28.17, 53.6/33.0/22.4/15.9 (BP=1.000, ratio=1.092, hyp_len=12480, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.127.0.45-1.58.0.37-1.44.2.03-7.64.1.59-4.92.pth, bkmy
BLEU = 32.22, 57.1/37.4/26.2/19.3 (BP=1.000, ratio=1.096, hyp_len=13406, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.128.0.45-1.56.0.36-1.44.1.98-7.25.1.54-4.68.pth, mybk
BLEU = 27.73, 53.3/32.4/21.9/15.6 (BP=1.000, ratio=1.083, hyp_len=12380, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.128.0.45-1.56.0.36-1.44.1.98-7.25.1.54-4.68.pth, bkmy
BLEU = 34.26, 59.2/39.4/28.1/21.0 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.129.0.46-1.58.0.37-1.45.1.98-7.23.1.54-4.67.pth, mybk
BLEU = 28.54, 55.0/33.5/22.6/15.9 (BP=1.000, ratio=1.053, hyp_len=12039, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.129.0.46-1.58.0.37-1.45.1.98-7.23.1.54-4.67.pth, bkmy
BLEU = 33.73, 59.2/39.2/27.5/20.3 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.130.0.45-1.57.0.36-1.43.1.94-6.99.1.56-4.78.pth, mybk
BLEU = 29.50, 55.7/34.5/23.4/16.9 (BP=1.000, ratio=1.076, hyp_len=12304, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.130.0.45-1.57.0.36-1.43.1.94-6.99.1.56-4.78.pth, bkmy
BLEU = 32.59, 57.4/37.7/26.6/19.5 (BP=1.000, ratio=1.100, hyp_len=13460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.131.0.51-1.67.0.40-1.48.1.99-7.33.1.56-4.78.pth, mybk
BLEU = 29.02, 55.0/33.9/23.1/16.5 (BP=1.000, ratio=1.078, hyp_len=12329, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.131.0.51-1.67.0.40-1.48.1.99-7.33.1.56-4.78.pth, bkmy
BLEU = 31.74, 57.0/37.1/25.8/18.6 (BP=1.000, ratio=1.093, hyp_len=13368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.93-6.92.1.73-5.62.1.35-3.86.1.10-3.00.pth, mybk
BLEU = 30.54, 58.2/36.4/24.2/17.0 (BP=1.000, ratio=1.057, hyp_len=12079, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.93-6.92.1.73-5.62.1.35-3.86.1.10-3.00.pth, bkmy
BLEU = 38.99, 65.9/45.5/32.5/24.0 (BP=0.997, ratio=0.997, hyp_len=12197, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.132.0.44-1.56.0.36-1.44.1.95-7.06.1.57-4.80.pth, mybk
BLEU = 27.86, 53.4/32.7/22.0/15.7 (BP=1.000, ratio=1.084, hyp_len=12394, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.132.0.44-1.56.0.36-1.44.1.95-7.06.1.57-4.80.pth, bkmy
BLEU = 33.33, 58.2/38.7/27.3/20.0 (BP=1.000, ratio=1.081, hyp_len=13223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.133.0.43-1.54.0.36-1.44.2.00-7.36.1.58-4.86.pth, mybk
BLEU = 27.72, 53.6/32.6/21.9/15.4 (BP=1.000, ratio=1.083, hyp_len=12376, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.133.0.43-1.54.0.36-1.44.2.00-7.36.1.58-4.86.pth, bkmy
BLEU = 32.57, 57.9/37.9/26.5/19.4 (BP=1.000, ratio=1.080, hyp_len=13212, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.134.0.46-1.58.0.37-1.45.1.96-7.09.1.55-4.71.pth, mybk
BLEU = 27.40, 53.3/32.2/21.6/15.2 (BP=1.000, ratio=1.105, hyp_len=12627, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.134.0.46-1.58.0.37-1.45.1.96-7.09.1.55-4.71.pth, bkmy
BLEU = 32.37, 57.7/37.7/26.4/19.1 (BP=1.000, ratio=1.087, hyp_len=13290, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.135.0.43-1.53.0.37-1.45.1.96-7.08.1.56-4.74.pth, mybk
BLEU = 28.63, 54.9/33.7/22.7/16.0 (BP=1.000, ratio=1.070, hyp_len=12230, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.135.0.43-1.53.0.37-1.45.1.96-7.08.1.56-4.74.pth, bkmy
BLEU = 32.45, 57.4/37.7/26.5/19.3 (BP=1.000, ratio=1.084, hyp_len=13257, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.136.0.46-1.58.0.39-1.47.1.99-7.31.1.59-4.90.pth, mybk
BLEU = 27.63, 53.9/32.8/21.7/15.2 (BP=1.000, ratio=1.096, hyp_len=12525, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.136.0.46-1.58.0.39-1.47.1.99-7.31.1.59-4.90.pth, bkmy
BLEU = 32.30, 57.4/37.6/26.3/19.2 (BP=1.000, ratio=1.076, hyp_len=13163, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.137.0.45-1.57.0.36-1.43.2.01-7.47.1.54-4.67.pth, mybk
BLEU = 28.93, 55.3/34.0/22.9/16.2 (BP=1.000, ratio=1.063, hyp_len=12157, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.137.0.45-1.57.0.36-1.43.2.01-7.47.1.54-4.67.pth, bkmy
BLEU = 32.39, 57.7/37.8/26.3/19.1 (BP=1.000, ratio=1.078, hyp_len=13179, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.138.0.43-1.54.0.35-1.42.2.05-7.79.1.57-4.79.pth, mybk
BLEU = 29.19, 54.9/34.2/23.3/16.6 (BP=1.000, ratio=1.098, hyp_len=12558, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.138.0.43-1.54.0.35-1.42.2.05-7.79.1.57-4.79.pth, bkmy
BLEU = 32.85, 58.4/38.4/26.7/19.4 (BP=1.000, ratio=1.084, hyp_len=13257, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.139.0.42-1.52.0.34-1.41.2.09-8.07.1.56-4.74.pth, mybk
BLEU = 27.22, 53.1/32.2/21.4/15.0 (BP=1.000, ratio=1.096, hyp_len=12535, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.139.0.42-1.52.0.34-1.41.2.09-8.07.1.56-4.74.pth, bkmy
BLEU = 31.91, 56.9/37.3/26.1/18.8 (BP=1.000, ratio=1.087, hyp_len=13296, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.140.0.45-1.57.0.38-1.47.2.06-7.87.1.57-4.79.pth, mybk
BLEU = 28.67, 55.1/33.9/22.8/15.9 (BP=1.000, ratio=1.076, hyp_len=12300, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.140.0.45-1.57.0.38-1.47.2.06-7.87.1.57-4.79.pth, bkmy
BLEU = 32.70, 58.2/38.1/26.6/19.4 (BP=1.000, ratio=1.071, hyp_len=13098, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.141.0.48-1.61.0.37-1.45.2.06-7.87.1.58-4.87.pth, mybk
BLEU = 27.66, 53.5/32.3/21.8/15.5 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.141.0.48-1.61.0.37-1.45.2.06-7.87.1.58-4.87.pth, bkmy
BLEU = 33.01, 58.2/38.3/27.0/19.8 (BP=1.000, ratio=1.077, hyp_len=13167, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.79-5.98.1.52-4.56.1.35-3.84.1.11-3.03.pth, mybk
BLEU = 28.87, 54.7/33.9/22.9/16.4 (BP=1.000, ratio=1.081, hyp_len=12356, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.79-5.98.1.52-4.56.1.35-3.84.1.11-3.03.pth, bkmy
BLEU = 39.40, 65.7/46.0/32.9/24.3 (BP=1.000, ratio=1.019, hyp_len=12462, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.142.0.41-1.50.0.33-1.39.1.98-7.26.1.55-4.70.pth, mybk
BLEU = 28.51, 55.2/33.8/22.4/15.8 (BP=1.000, ratio=1.075, hyp_len=12292, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.142.0.41-1.50.0.33-1.39.1.98-7.26.1.55-4.70.pth, bkmy
BLEU = 32.96, 57.9/38.4/27.0/19.7 (BP=1.000, ratio=1.083, hyp_len=13251, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.143.0.43-1.53.0.34-1.41.2.02-7.55.1.60-4.98.pth, mybk
BLEU = 28.93, 55.0/34.1/23.0/16.3 (BP=1.000, ratio=1.086, hyp_len=12420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.143.0.43-1.53.0.34-1.41.2.02-7.55.1.60-4.98.pth, bkmy
BLEU = 31.80, 57.1/37.0/25.8/18.7 (BP=1.000, ratio=1.086, hyp_len=13285, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.144.0.42-1.52.0.34-1.40.2.07-7.92.1.63-5.12.pth, mybk
BLEU = 28.83, 54.4/33.7/23.0/16.4 (BP=1.000, ratio=1.082, hyp_len=12373, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.144.0.42-1.52.0.34-1.40.2.07-7.92.1.63-5.12.pth, bkmy
BLEU = 32.71, 57.7/37.9/26.7/19.6 (BP=1.000, ratio=1.077, hyp_len=13171, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.145.0.48-1.61.0.37-1.45.2.07-7.93.1.56-4.76.pth, mybk
BLEU = 26.94, 53.1/31.9/21.0/14.8 (BP=1.000, ratio=1.088, hyp_len=12437, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.145.0.48-1.61.0.37-1.45.2.07-7.93.1.56-4.76.pth, bkmy
BLEU = 32.19, 57.1/37.3/26.2/19.2 (BP=1.000, ratio=1.064, hyp_len=13011, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.146.0.43-1.54.0.34-1.41.2.06-7.88.1.61-4.98.pth, mybk
BLEU = 28.50, 54.1/33.4/22.7/16.1 (BP=1.000, ratio=1.074, hyp_len=12276, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.146.0.43-1.54.0.34-1.41.2.06-7.88.1.61-4.98.pth, bkmy
BLEU = 31.84, 56.5/36.7/25.9/19.2 (BP=1.000, ratio=1.098, hyp_len=13427, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.147.0.43-1.54.0.36-1.43.2.09-8.09.1.59-4.92.pth, mybk
BLEU = 27.38, 52.4/31.8/21.6/15.6 (BP=1.000, ratio=1.088, hyp_len=12439, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.147.0.43-1.54.0.36-1.43.2.09-8.09.1.59-4.92.pth, bkmy
BLEU = 32.45, 58.0/38.1/26.4/19.1 (BP=1.000, ratio=1.074, hyp_len=13130, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.148.0.44-1.55.0.35-1.41.2.07-7.96.1.58-4.85.pth, mybk
BLEU = 29.28, 54.9/34.0/23.2/16.9 (BP=1.000, ratio=1.073, hyp_len=12268, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.148.0.44-1.55.0.35-1.41.2.07-7.96.1.58-4.85.pth, bkmy
BLEU = 31.67, 57.1/37.1/25.6/18.5 (BP=1.000, ratio=1.075, hyp_len=13150, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.149.0.40-1.49.0.33-1.40.2.07-7.96.1.64-5.16.pth, mybk
BLEU = 27.25, 53.0/32.0/21.4/15.2 (BP=1.000, ratio=1.084, hyp_len=12395, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.149.0.40-1.49.0.33-1.40.2.07-7.96.1.64-5.16.pth, bkmy
BLEU = 30.21, 54.7/35.4/24.4/17.7 (BP=1.000, ratio=1.122, hyp_len=13723, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.150.0.43-1.53.0.35-1.41.2.12-8.30.1.62-5.03.pth, mybk
BLEU = 26.70, 52.4/31.4/20.9/14.8 (BP=1.000, ratio=1.100, hyp_len=12573, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.150.0.43-1.53.0.35-1.41.2.12-8.30.1.62-5.03.pth, bkmy
BLEU = 31.76, 56.7/36.9/25.9/18.8 (BP=1.000, ratio=1.090, hyp_len=13329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.151.0.41-1.50.0.33-1.39.2.08-8.01.1.62-5.03.pth, mybk
BLEU = 27.46, 53.3/32.2/21.7/15.2 (BP=1.000, ratio=1.078, hyp_len=12326, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.151.0.41-1.50.0.33-1.39.2.08-8.01.1.62-5.03.pth, bkmy
BLEU = 31.67, 56.8/36.9/25.7/18.7 (BP=1.000, ratio=1.077, hyp_len=13174, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.79-5.97.1.54-4.66.1.30-3.68.1.08-2.95.pth, mybk
BLEU = 31.16, 59.1/36.8/24.8/17.5 (BP=1.000, ratio=1.043, hyp_len=11924, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.79-5.97.1.54-4.66.1.30-3.68.1.08-2.95.pth, bkmy
BLEU = 38.16, 64.4/44.5/31.7/23.3 (BP=1.000, ratio=1.054, hyp_len=12891, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.152.0.41-1.50.0.32-1.38.2.13-8.40.1.60-4.95.pth, mybk
BLEU = 28.64, 54.1/33.5/22.8/16.2 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.152.0.41-1.50.0.32-1.38.2.13-8.40.1.60-4.95.pth, bkmy
BLEU = 31.84, 56.9/37.3/25.9/18.6 (BP=1.000, ratio=1.105, hyp_len=13517, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.153.0.42-1.52.0.32-1.37.2.10-8.14.1.63-5.13.pth, mybk
BLEU = 27.83, 53.0/32.5/22.1/15.8 (BP=1.000, ratio=1.099, hyp_len=12560, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.153.0.42-1.52.0.32-1.37.2.10-8.14.1.63-5.13.pth, bkmy
BLEU = 32.48, 57.3/37.6/26.5/19.5 (BP=1.000, ratio=1.084, hyp_len=13259, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.154.0.40-1.49.0.32-1.38.2.06-7.84.1.61-5.00.pth, mybk
BLEU = 28.65, 54.8/33.8/22.7/16.0 (BP=1.000, ratio=1.075, hyp_len=12290, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.154.0.40-1.49.0.32-1.38.2.06-7.84.1.61-5.00.pth, bkmy
BLEU = 31.38, 56.4/36.5/25.3/18.6 (BP=1.000, ratio=1.106, hyp_len=13529, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.155.0.42-1.52.0.32-1.38.2.06-7.86.1.53-4.62.pth, mybk
BLEU = 28.94, 54.8/33.8/23.0/16.5 (BP=1.000, ratio=1.079, hyp_len=12337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.155.0.42-1.52.0.32-1.38.2.06-7.86.1.53-4.62.pth, bkmy
BLEU = 34.81, 59.8/40.3/28.7/21.2 (BP=1.000, ratio=1.057, hyp_len=12933, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.156.0.42-1.52.0.33-1.39.2.01-7.43.1.60-4.93.pth, mybk
BLEU = 28.35, 54.1/33.2/22.5/16.0 (BP=1.000, ratio=1.087, hyp_len=12428, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.156.0.42-1.52.0.33-1.39.2.01-7.43.1.60-4.93.pth, bkmy
BLEU = 30.42, 55.3/35.6/24.6/17.6 (BP=1.000, ratio=1.100, hyp_len=13448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.157.0.39-1.47.0.32-1.37.2.07-7.90.1.59-4.91.pth, mybk
BLEU = 28.77, 55.0/33.7/22.7/16.3 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.157.0.39-1.47.0.32-1.37.2.07-7.90.1.59-4.91.pth, bkmy
BLEU = 31.73, 57.1/37.0/25.8/18.6 (BP=1.000, ratio=1.076, hyp_len=13164, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.158.0.38-1.47.0.31-1.36.2.07-7.94.1.63-5.09.pth, mybk
BLEU = 28.38, 54.1/33.3/22.6/15.9 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.158.0.38-1.47.0.31-1.36.2.07-7.94.1.63-5.09.pth, bkmy
BLEU = 32.06, 57.4/37.3/26.0/19.0 (BP=1.000, ratio=1.065, hyp_len=13020, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.159.0.39-1.47.0.33-1.38.2.10-8.15.1.57-4.79.pth, mybk
BLEU = 26.99, 53.3/31.8/21.0/14.9 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.159.0.39-1.47.0.33-1.38.2.10-8.15.1.57-4.79.pth, bkmy
BLEU = 32.08, 57.2/37.5/26.1/18.9 (BP=1.000, ratio=1.084, hyp_len=13254, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.160.0.39-1.47.0.31-1.37.2.10-8.16.1.56-4.76.pth, mybk
BLEU = 27.74, 54.3/33.0/21.8/15.2 (BP=1.000, ratio=1.064, hyp_len=12158, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.160.0.39-1.47.0.31-1.37.2.10-8.16.1.56-4.76.pth, bkmy
BLEU = 31.73, 56.4/36.7/25.9/18.9 (BP=1.000, ratio=1.103, hyp_len=13486, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.161.0.39-1.48.0.32-1.38.2.08-8.00.1.58-4.87.pth, mybk
BLEU = 27.07, 52.7/31.9/21.3/15.0 (BP=1.000, ratio=1.094, hyp_len=12512, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.161.0.39-1.48.0.32-1.38.2.08-8.00.1.58-4.87.pth, bkmy
BLEU = 31.66, 56.8/36.9/25.6/18.7 (BP=1.000, ratio=1.099, hyp_len=13439, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.70-5.45.1.46-4.31.1.36-3.88.1.09-2.97.pth, mybk
BLEU = 30.39, 57.5/35.9/24.2/17.0 (BP=1.000, ratio=1.069, hyp_len=12221, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.70-5.45.1.46-4.31.1.36-3.88.1.09-2.97.pth, bkmy
BLEU = 37.20, 63.5/44.0/30.8/22.3 (BP=1.000, ratio=1.088, hyp_len=13303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.162.0.41-1.50.0.33-1.39.2.01-7.47.1.60-4.95.pth, mybk
BLEU = 28.49, 54.6/33.6/22.5/16.0 (BP=1.000, ratio=1.084, hyp_len=12390, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.162.0.41-1.50.0.33-1.39.2.01-7.47.1.60-4.95.pth, bkmy
BLEU = 31.67, 56.8/36.8/25.7/18.7 (BP=1.000, ratio=1.081, hyp_len=13226, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.163.0.38-1.47.0.31-1.36.2.11-8.21.1.61-5.01.pth, mybk
BLEU = 27.25, 52.7/31.8/21.4/15.4 (BP=1.000, ratio=1.104, hyp_len=12624, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.163.0.38-1.47.0.31-1.36.2.11-8.21.1.61-5.01.pth, bkmy
BLEU = 30.73, 55.7/35.9/24.9/17.9 (BP=1.000, ratio=1.098, hyp_len=13426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.164.0.41-1.51.0.36-1.44.2.07-7.94.1.60-4.95.pth, mybk
BLEU = 27.38, 53.0/32.2/21.6/15.3 (BP=1.000, ratio=1.093, hyp_len=12494, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.164.0.41-1.51.0.36-1.44.2.07-7.94.1.60-4.95.pth, bkmy
BLEU = 32.76, 58.2/38.0/26.6/19.6 (BP=1.000, ratio=1.065, hyp_len=13026, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.165.0.39-1.47.0.32-1.37.2.10-8.16.1.62-5.07.pth, mybk
BLEU = 26.69, 53.0/31.4/20.8/14.6 (BP=1.000, ratio=1.080, hyp_len=12341, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.165.0.39-1.47.0.32-1.37.2.10-8.16.1.62-5.07.pth, bkmy
BLEU = 31.67, 56.2/36.8/25.8/18.9 (BP=1.000, ratio=1.088, hyp_len=13312, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.166.0.38-1.47.0.32-1.38.2.04-7.68.1.60-4.94.pth, mybk
BLEU = 28.40, 54.7/33.4/22.5/15.8 (BP=1.000, ratio=1.063, hyp_len=12148, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.166.0.38-1.47.0.32-1.38.2.04-7.68.1.60-4.94.pth, bkmy
BLEU = 32.26, 57.2/37.4/26.2/19.3 (BP=1.000, ratio=1.085, hyp_len=13267, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.167.0.40-1.49.0.33-1.39.2.09-8.11.1.65-5.23.pth, mybk
BLEU = 28.19, 53.8/32.7/22.3/16.1 (BP=1.000, ratio=1.067, hyp_len=12197, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.167.0.40-1.49.0.33-1.39.2.09-8.11.1.65-5.23.pth, bkmy
BLEU = 30.13, 54.9/35.3/24.4/17.5 (BP=1.000, ratio=1.112, hyp_len=13601, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.168.0.39-1.47.0.31-1.37.2.12-8.29.1.62-5.04.pth, mybk
BLEU = 28.16, 53.4/32.9/22.4/15.9 (BP=1.000, ratio=1.078, hyp_len=12322, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.168.0.39-1.47.0.31-1.37.2.12-8.29.1.62-5.04.pth, bkmy
BLEU = 32.37, 57.2/37.6/26.3/19.4 (BP=1.000, ratio=1.089, hyp_len=13321, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.169.0.40-1.49.0.33-1.39.2.07-7.94.1.64-5.15.pth, mybk
BLEU = 28.29, 54.5/33.0/22.4/15.9 (BP=1.000, ratio=1.054, hyp_len=12052, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.169.0.40-1.49.0.33-1.39.2.07-7.94.1.64-5.15.pth, bkmy
BLEU = 32.36, 57.4/37.8/26.4/19.1 (BP=1.000, ratio=1.085, hyp_len=13273, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.170.0.40-1.50.0.33-1.39.2.12-8.35.1.62-5.06.pth, mybk
BLEU = 28.23, 54.1/33.1/22.4/15.8 (BP=1.000, ratio=1.079, hyp_len=12337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.170.0.40-1.50.0.33-1.39.2.12-8.35.1.62-5.06.pth, bkmy
BLEU = 31.05, 56.0/36.2/25.1/18.2 (BP=1.000, ratio=1.095, hyp_len=13388, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.171.0.37-1.44.0.30-1.36.2.05-7.80.1.61-5.00.pth, mybk
BLEU = 28.50, 53.9/33.2/22.7/16.2 (BP=1.000, ratio=1.078, hyp_len=12318, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.171.0.37-1.44.0.30-1.36.2.05-7.80.1.61-5.00.pth, bkmy
BLEU = 32.22, 56.9/37.4/26.2/19.3 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.67-5.30.1.43-4.16.1.34-3.82.1.09-2.98.pth, mybk
BLEU = 30.40, 57.9/36.1/24.2/16.8 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.67-5.30.1.43-4.16.1.34-3.82.1.09-2.98.pth, bkmy
BLEU = 38.85, 64.7/45.1/32.4/24.1 (BP=1.000, ratio=1.059, hyp_len=12949, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.172.0.38-1.47.0.31-1.37.2.10-8.19.1.62-5.03.pth, mybk
BLEU = 28.22, 54.2/33.3/22.3/15.7 (BP=1.000, ratio=1.097, hyp_len=12540, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.172.0.38-1.47.0.31-1.37.2.10-8.19.1.62-5.03.pth, bkmy
BLEU = 31.63, 56.7/37.1/25.6/18.6 (BP=1.000, ratio=1.110, hyp_len=13579, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.173.0.38-1.46.0.31-1.36.2.10-8.20.1.65-5.20.pth, mybk
BLEU = 27.76, 53.2/32.4/21.9/15.7 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.173.0.38-1.46.0.31-1.36.2.10-8.20.1.65-5.20.pth, bkmy
BLEU = 31.20, 56.4/36.6/25.2/18.2 (BP=1.000, ratio=1.082, hyp_len=13238, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.174.0.44-1.55.0.34-1.41.2.10-8.17.1.55-4.70.pth, mybk
BLEU = 27.63, 53.5/32.4/21.7/15.5 (BP=1.000, ratio=1.095, hyp_len=12520, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.174.0.44-1.55.0.34-1.41.2.10-8.17.1.55-4.70.pth, bkmy
BLEU = 31.47, 56.4/36.8/25.4/18.6 (BP=1.000, ratio=1.093, hyp_len=13368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.175.0.38-1.46.0.34-1.41.2.14-8.47.1.56-4.77.pth, mybk
BLEU = 27.56, 53.3/32.3/21.7/15.4 (BP=1.000, ratio=1.087, hyp_len=12427, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.175.0.38-1.46.0.34-1.41.2.14-8.47.1.56-4.77.pth, bkmy
BLEU = 32.42, 57.2/37.6/26.4/19.4 (BP=1.000, ratio=1.091, hyp_len=13346, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.176.0.38-1.47.0.31-1.37.2.15-8.61.1.64-5.15.pth, mybk
BLEU = 26.76, 52.5/31.5/21.0/14.7 (BP=1.000, ratio=1.112, hyp_len=12710, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.176.0.38-1.47.0.31-1.37.2.15-8.61.1.64-5.15.pth, bkmy
BLEU = 29.96, 54.7/34.9/24.1/17.5 (BP=1.000, ratio=1.102, hyp_len=13476, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.177.0.36-1.43.0.31-1.36.2.10-8.20.1.67-5.30.pth, mybk
BLEU = 27.91, 53.9/32.6/22.1/15.6 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.177.0.36-1.43.0.31-1.36.2.10-8.20.1.67-5.30.pth, bkmy
BLEU = 31.44, 56.3/36.6/25.5/18.6 (BP=1.000, ratio=1.088, hyp_len=13306, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.178.0.45-1.56.0.35-1.42.2.09-8.09.1.68-5.37.pth, mybk
BLEU = 27.69, 53.7/32.3/21.8/15.5 (BP=1.000, ratio=1.071, hyp_len=12238, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.178.0.45-1.56.0.35-1.42.2.09-8.09.1.68-5.37.pth, bkmy
BLEU = 31.82, 56.7/36.7/25.8/19.1 (BP=1.000, ratio=1.069, hyp_len=13074, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.179.0.44-1.55.0.35-1.42.2.14-8.50.1.62-5.07.pth, mybk
BLEU = 26.70, 52.3/31.5/20.9/14.7 (BP=1.000, ratio=1.121, hyp_len=12820, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.179.0.44-1.55.0.35-1.42.2.14-8.50.1.62-5.07.pth, bkmy
BLEU = 31.04, 56.3/36.2/25.1/18.2 (BP=1.000, ratio=1.083, hyp_len=13251, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.180.0.38-1.46.0.30-1.35.2.16-8.67.1.63-5.09.pth, mybk
BLEU = 27.20, 52.7/32.0/21.5/15.1 (BP=1.000, ratio=1.107, hyp_len=12658, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.180.0.38-1.46.0.30-1.35.2.16-8.67.1.63-5.09.pth, bkmy
BLEU = 31.86, 56.9/37.1/25.9/18.9 (BP=1.000, ratio=1.064, hyp_len=13017, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.181.0.39-1.48.0.34-1.40.2.17-8.72.1.63-5.12.pth, mybk
BLEU = 27.03, 52.7/31.8/21.3/15.0 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.181.0.39-1.48.0.34-1.40.2.17-8.72.1.63-5.12.pth, bkmy
BLEU = 30.98, 55.8/36.0/25.0/18.4 (BP=1.000, ratio=1.092, hyp_len=13356, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.61-4.99.1.38-3.98.1.31-3.72.1.02-2.77.pth, mybk
BLEU = 30.70, 57.1/36.0/24.7/17.5 (BP=1.000, ratio=1.090, hyp_len=12464, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.61-4.99.1.38-3.98.1.31-3.72.1.02-2.77.pth, bkmy
BLEU = 40.28, 66.5/47.0/33.7/25.0 (BP=1.000, ratio=1.039, hyp_len=12707, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.182.0.37-1.44.0.30-1.35.2.15-8.57.1.66-5.24.pth, mybk
BLEU = 27.90, 53.8/33.0/22.2/15.4 (BP=1.000, ratio=1.089, hyp_len=12451, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.182.0.37-1.44.0.30-1.35.2.15-8.57.1.66-5.24.pth, bkmy
BLEU = 31.84, 56.5/37.1/25.8/19.0 (BP=1.000, ratio=1.101, hyp_len=13472, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.183.0.37-1.45.0.30-1.34.2.18-8.82.1.61-5.02.pth, mybk
BLEU = 26.29, 51.7/31.1/20.8/14.4 (BP=1.000, ratio=1.122, hyp_len=12832, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.183.0.37-1.45.0.30-1.34.2.18-8.82.1.61-5.02.pth, bkmy
BLEU = 32.15, 57.3/37.4/26.2/19.1 (BP=1.000, ratio=1.086, hyp_len=13285, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.184.0.36-1.43.0.29-1.34.2.15-8.58.1.64-5.16.pth, mybk
BLEU = 27.12, 52.9/32.0/21.3/15.0 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.184.0.36-1.43.0.29-1.34.2.15-8.58.1.64-5.16.pth, bkmy
BLEU = 32.37, 57.1/37.5/26.3/19.5 (BP=1.000, ratio=1.087, hyp_len=13293, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.185.0.37-1.45.0.29-1.34.2.13-8.41.1.61-4.99.pth, mybk
BLEU = 28.37, 54.3/33.4/22.5/15.9 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.185.0.37-1.45.0.29-1.34.2.13-8.41.1.61-4.99.pth, bkmy
BLEU = 32.34, 57.1/37.5/26.4/19.4 (BP=1.000, ratio=1.082, hyp_len=13240, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.186.0.40-1.50.0.34-1.40.2.15-8.54.1.64-5.18.pth, mybk
BLEU = 26.90, 52.3/31.5/21.2/15.0 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.186.0.40-1.50.0.34-1.40.2.15-8.54.1.64-5.18.pth, bkmy
BLEU = 32.19, 57.2/37.5/26.2/19.1 (BP=1.000, ratio=1.091, hyp_len=13350, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.187.0.37-1.45.0.30-1.36.2.17-8.74.1.65-5.21.pth, mybk
BLEU = 27.68, 53.1/32.4/22.0/15.5 (BP=1.000, ratio=1.091, hyp_len=12475, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.187.0.37-1.45.0.30-1.36.2.17-8.74.1.65-5.21.pth, bkmy
BLEU = 31.56, 56.1/36.6/25.7/18.9 (BP=1.000, ratio=1.104, hyp_len=13508, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.188.0.38-1.46.0.30-1.34.2.10-8.18.1.66-5.29.pth, mybk
BLEU = 27.85, 53.9/32.7/22.1/15.4 (BP=1.000, ratio=1.094, hyp_len=12504, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.188.0.38-1.46.0.30-1.34.2.10-8.18.1.66-5.29.pth, bkmy
BLEU = 33.29, 58.4/38.6/27.2/20.1 (BP=1.000, ratio=1.075, hyp_len=13143, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.189.0.36-1.43.0.29-1.33.2.21-9.15.1.65-5.22.pth, mybk
BLEU = 26.05, 51.5/30.6/20.5/14.3 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.189.0.36-1.43.0.29-1.33.2.21-9.15.1.65-5.22.pth, bkmy
BLEU = 31.49, 56.5/36.6/25.5/18.7 (BP=1.000, ratio=1.106, hyp_len=13524, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.190.0.38-1.47.0.32-1.37.2.15-8.57.1.66-5.27.pth, mybk
BLEU = 27.32, 52.8/32.0/21.5/15.4 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.190.0.38-1.47.0.32-1.37.2.15-8.57.1.66-5.27.pth, bkmy
BLEU = 31.02, 55.6/35.9/25.1/18.5 (BP=1.000, ratio=1.107, hyp_len=13540, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.191.0.36-1.44.0.29-1.34.2.14-8.49.1.69-5.41.pth, mybk
BLEU = 28.26, 53.6/33.0/22.4/16.0 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.191.0.36-1.44.0.29-1.34.2.14-8.49.1.69-5.41.pth, bkmy
BLEU = 31.81, 56.5/36.9/25.9/19.0 (BP=1.000, ratio=1.075, hyp_len=13150, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.48-4.40.1.26-3.54.1.31-3.72.1.02-2.78.pth, mybk
BLEU = 31.33, 58.9/36.8/25.1/17.7 (BP=1.000, ratio=1.064, hyp_len=12159, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.48-4.40.1.26-3.54.1.31-3.72.1.02-2.78.pth, bkmy
BLEU = 41.93, 68.3/48.9/35.3/26.2 (BP=1.000, ratio=1.020, hyp_len=12471, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.192.0.35-1.43.0.30-1.35.2.11-8.25.1.66-5.26.pth, mybk
BLEU = 27.42, 53.0/32.3/21.7/15.2 (BP=1.000, ratio=1.083, hyp_len=12379, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.192.0.35-1.43.0.30-1.35.2.11-8.25.1.66-5.26.pth, bkmy
BLEU = 31.75, 56.3/36.8/25.8/19.0 (BP=1.000, ratio=1.066, hyp_len=13038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.193.0.36-1.43.0.30-1.35.2.13-8.42.1.64-5.15.pth, mybk
BLEU = 27.96, 54.0/33.0/22.2/15.5 (BP=1.000, ratio=1.077, hyp_len=12310, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.193.0.36-1.43.0.30-1.35.2.13-8.42.1.64-5.15.pth, bkmy
BLEU = 31.26, 56.6/36.5/25.1/18.4 (BP=1.000, ratio=1.080, hyp_len=13211, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.194.0.37-1.45.0.30-1.35.2.14-8.49.1.65-5.23.pth, mybk
BLEU = 28.42, 54.1/33.5/22.7/15.9 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.194.0.37-1.45.0.30-1.35.2.14-8.49.1.65-5.23.pth, bkmy
BLEU = 31.51, 56.6/37.1/25.6/18.4 (BP=1.000, ratio=1.104, hyp_len=13502, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.195.0.38-1.46.0.31-1.37.2.20-8.99.1.66-5.26.pth, mybk
BLEU = 27.32, 52.9/32.1/21.6/15.2 (BP=1.000, ratio=1.092, hyp_len=12480, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.195.0.38-1.46.0.31-1.37.2.20-8.99.1.66-5.26.pth, bkmy
BLEU = 31.36, 56.5/36.6/25.4/18.4 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.196.0.39-1.48.0.31-1.37.2.20-9.03.1.66-5.25.pth, mybk
BLEU = 26.99, 52.6/31.7/21.3/15.0 (BP=1.000, ratio=1.101, hyp_len=12585, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.196.0.39-1.48.0.31-1.37.2.20-9.03.1.66-5.25.pth, bkmy
BLEU = 31.45, 56.4/36.4/25.5/18.7 (BP=1.000, ratio=1.078, hyp_len=13182, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.197.0.36-1.44.0.29-1.34.2.16-8.67.1.68-5.35.pth, mybk
BLEU = 26.45, 52.4/31.3/20.8/14.4 (BP=1.000, ratio=1.096, hyp_len=12532, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.197.0.36-1.44.0.29-1.34.2.16-8.67.1.68-5.35.pth, bkmy
BLEU = 31.22, 56.2/36.5/25.3/18.3 (BP=1.000, ratio=1.091, hyp_len=13345, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.198.0.37-1.45.0.33-1.39.2.16-8.65.1.66-5.26.pth, mybk
BLEU = 27.81, 53.8/32.6/22.0/15.5 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.198.0.37-1.45.0.33-1.39.2.16-8.65.1.66-5.26.pth, bkmy
BLEU = 30.22, 55.0/35.4/24.5/17.5 (BP=1.000, ratio=1.107, hyp_len=13541, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.199.0.35-1.43.0.29-1.34.2.16-8.68.1.64-5.16.pth, mybk
BLEU = 27.05, 52.7/32.0/21.2/15.0 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.199.0.35-1.43.0.29-1.34.2.16-8.68.1.64-5.16.pth, bkmy
BLEU = 32.28, 57.6/37.5/26.3/19.2 (BP=1.000, ratio=1.063, hyp_len=13003, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.200.0.34-1.41.0.29-1.34.2.17-8.74.1.64-5.18.pth, mybk
BLEU = 28.72, 54.1/33.2/22.8/16.6 (BP=1.000, ratio=1.076, hyp_len=12297, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.200.0.34-1.41.0.29-1.34.2.17-8.74.1.64-5.18.pth, bkmy
BLEU = 31.95, 56.4/36.8/26.1/19.3 (BP=1.000, ratio=1.098, hyp_len=13429, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.201.0.37-1.45.0.30-1.34.2.14-8.53.1.61-4.98.pth, mybk
BLEU = 28.39, 54.5/33.1/22.5/16.0 (BP=1.000, ratio=1.072, hyp_len=12252, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.201.0.37-1.45.0.30-1.34.2.14-8.53.1.61-4.98.pth, bkmy
BLEU = 31.42, 56.0/36.3/25.4/18.9 (BP=1.000, ratio=1.098, hyp_len=13426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.47.1.28-3.59.1.33-3.80.1.07-2.92.pth, mybk
BLEU = 29.34, 56.2/34.8/23.3/16.3 (BP=1.000, ratio=1.114, hyp_len=12738, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.47.1.28-3.59.1.33-3.80.1.07-2.92.pth, bkmy
BLEU = 37.84, 63.6/44.3/31.5/23.1 (BP=1.000, ratio=1.084, hyp_len=13256, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.202.0.35-1.42.0.29-1.34.2.13-8.40.1.61-4.99.pth, mybk
BLEU = 27.44, 53.3/32.1/21.5/15.4 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.202.0.35-1.42.0.29-1.34.2.13-8.40.1.61-4.99.pth, bkmy
BLEU = 31.30, 55.7/36.5/25.5/18.5 (BP=1.000, ratio=1.101, hyp_len=13470, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.203.0.36-1.43.0.30-1.34.2.17-8.74.1.64-5.14.pth, mybk
BLEU = 27.07, 52.8/31.8/21.3/15.0 (BP=1.000, ratio=1.087, hyp_len=12422, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.203.0.36-1.43.0.30-1.34.2.17-8.74.1.64-5.14.pth, bkmy
BLEU = 32.18, 57.3/37.4/26.2/19.1 (BP=1.000, ratio=1.078, hyp_len=13181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.204.0.36-1.44.0.30-1.35.2.14-8.46.1.63-5.09.pth, mybk
BLEU = 27.82, 54.0/32.8/21.8/15.5 (BP=1.000, ratio=1.088, hyp_len=12442, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.204.0.36-1.44.0.30-1.35.2.14-8.46.1.63-5.09.pth, bkmy
BLEU = 32.71, 56.9/37.6/26.7/20.1 (BP=1.000, ratio=1.100, hyp_len=13448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.205.0.36-1.43.0.29-1.33.2.12-8.35.1.61-4.99.pth, mybk
BLEU = 27.08, 53.4/32.2/21.3/14.7 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.205.0.36-1.43.0.29-1.33.2.12-8.35.1.61-4.99.pth, bkmy
BLEU = 31.37, 56.7/37.0/25.4/18.2 (BP=1.000, ratio=1.105, hyp_len=13511, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.206.0.35-1.43.0.28-1.33.2.13-8.39.1.61-5.00.pth, mybk
BLEU = 29.07, 54.6/33.8/23.2/16.7 (BP=1.000, ratio=1.100, hyp_len=12575, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.206.0.35-1.43.0.28-1.33.2.13-8.39.1.61-5.00.pth, bkmy
BLEU = 33.29, 58.1/38.5/27.2/20.2 (BP=1.000, ratio=1.073, hyp_len=13121, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.207.0.38-1.46.0.29-1.34.2.12-8.36.1.64-5.15.pth, mybk
BLEU = 27.76, 53.1/32.4/22.0/15.7 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.207.0.38-1.46.0.29-1.34.2.12-8.36.1.64-5.15.pth, bkmy
BLEU = 32.51, 57.1/37.5/26.5/19.6 (BP=1.000, ratio=1.087, hyp_len=13301, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.208.0.33-1.40.0.29-1.33.2.14-8.53.1.64-5.14.pth, mybk
BLEU = 27.15, 52.8/31.8/21.4/15.1 (BP=1.000, ratio=1.090, hyp_len=12460, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.208.0.33-1.40.0.29-1.33.2.14-8.53.1.64-5.14.pth, bkmy
BLEU = 31.46, 56.1/36.6/25.5/18.7 (BP=1.000, ratio=1.094, hyp_len=13382, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.209.0.34-1.40.0.27-1.31.2.12-8.31.1.70-5.50.pth, mybk
BLEU = 27.77, 53.1/32.3/22.0/15.7 (BP=1.000, ratio=1.086, hyp_len=12411, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.209.0.34-1.40.0.27-1.31.2.12-8.31.1.70-5.50.pth, bkmy
BLEU = 29.82, 55.2/35.1/23.9/17.1 (BP=1.000, ratio=1.094, hyp_len=13382, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.210.0.36-1.43.0.29-1.33.2.16-8.69.1.68-5.37.pth, mybk
BLEU = 26.48, 52.2/31.1/20.7/14.7 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.210.0.36-1.43.0.29-1.33.2.16-8.69.1.68-5.37.pth, bkmy
BLEU = 31.41, 55.8/36.5/25.6/18.7 (BP=1.000, ratio=1.089, hyp_len=13323, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.211.0.34-1.40.0.27-1.32.2.16-8.64.1.68-5.37.pth, mybk
BLEU = 27.50, 53.4/32.3/21.6/15.3 (BP=1.000, ratio=1.076, hyp_len=12306, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.211.0.34-1.40.0.27-1.32.2.16-8.64.1.68-5.37.pth, bkmy
BLEU = 33.01, 58.1/38.1/27.0/19.9 (BP=1.000, ratio=1.076, hyp_len=13159, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.45-4.25.1.22-3.39.1.33-3.76.1.03-2.81.pth, mybk
BLEU = 32.09, 60.1/38.1/25.8/18.0 (BP=1.000, ratio=1.052, hyp_len=12031, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.45-4.25.1.22-3.39.1.33-3.76.1.03-2.81.pth, bkmy
BLEU = 40.83, 67.5/47.5/34.2/25.4 (BP=1.000, ratio=1.028, hyp_len=12574, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.212.0.34-1.40.0.29-1.33.2.16-8.70.1.67-5.29.pth, mybk
BLEU = 26.02, 52.1/30.9/20.3/14.0 (BP=1.000, ratio=1.071, hyp_len=12249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.212.0.34-1.40.0.29-1.33.2.16-8.70.1.67-5.29.pth, bkmy
BLEU = 31.20, 55.9/36.3/25.3/18.4 (BP=1.000, ratio=1.089, hyp_len=13316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.213.0.35-1.42.0.28-1.32.2.22-9.17.1.69-5.45.pth, mybk
BLEU = 26.56, 52.0/31.3/20.8/14.7 (BP=1.000, ratio=1.110, hyp_len=12684, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.213.0.35-1.42.0.28-1.32.2.22-9.17.1.69-5.45.pth, bkmy
BLEU = 31.95, 56.2/36.9/26.0/19.3 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.214.0.34-1.41.0.28-1.33.2.30-9.94.1.66-5.26.pth, mybk
BLEU = 26.54, 51.8/31.0/21.0/14.7 (BP=1.000, ratio=1.099, hyp_len=12563, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.214.0.34-1.41.0.28-1.33.2.30-9.94.1.66-5.26.pth, bkmy
BLEU = 30.59, 56.0/35.9/24.6/17.7 (BP=1.000, ratio=1.091, hyp_len=13343, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.215.0.34-1.40.0.28-1.33.2.21-9.15.1.70-5.46.pth, mybk
BLEU = 27.59, 53.3/32.1/21.8/15.5 (BP=1.000, ratio=1.082, hyp_len=12368, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.215.0.34-1.40.0.28-1.33.2.21-9.15.1.70-5.46.pth, bkmy
BLEU = 32.04, 56.9/37.3/26.1/19.0 (BP=1.000, ratio=1.072, hyp_len=13112, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.216.0.34-1.41.0.28-1.32.2.13-8.44.1.70-5.45.pth, mybk
BLEU = 28.08, 53.7/32.9/22.4/15.7 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.216.0.34-1.41.0.28-1.32.2.13-8.44.1.70-5.45.pth, bkmy
BLEU = 31.64, 56.3/36.7/25.7/18.9 (BP=1.000, ratio=1.103, hyp_len=13488, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.217.0.33-1.39.0.27-1.31.2.18-8.89.1.63-5.09.pth, mybk
BLEU = 28.04, 53.8/32.7/22.2/15.8 (BP=1.000, ratio=1.096, hyp_len=12530, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.217.0.33-1.39.0.27-1.31.2.18-8.89.1.63-5.09.pth, bkmy
BLEU = 31.75, 57.3/37.3/25.7/18.5 (BP=1.000, ratio=1.092, hyp_len=13352, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.218.0.35-1.42.0.29-1.33.2.18-8.85.1.66-5.28.pth, mybk
BLEU = 26.36, 52.2/31.1/20.6/14.4 (BP=1.000, ratio=1.099, hyp_len=12562, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.218.0.35-1.42.0.29-1.33.2.18-8.85.1.66-5.28.pth, bkmy
BLEU = 30.33, 55.2/35.6/24.7/17.5 (BP=1.000, ratio=1.100, hyp_len=13460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.219.0.33-1.39.0.27-1.31.2.13-8.44.1.64-5.16.pth, mybk
BLEU = 26.87, 53.3/31.8/21.1/14.6 (BP=1.000, ratio=1.104, hyp_len=12626, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.219.0.33-1.39.0.27-1.31.2.13-8.44.1.64-5.16.pth, bkmy
BLEU = 32.89, 58.0/38.1/26.8/19.7 (BP=1.000, ratio=1.087, hyp_len=13300, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.220.0.35-1.42.0.28-1.33.2.17-8.77.1.66-5.25.pth, mybk
BLEU = 28.44, 54.8/33.4/22.5/15.9 (BP=1.000, ratio=1.067, hyp_len=12194, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.220.0.35-1.42.0.28-1.33.2.17-8.77.1.66-5.25.pth, bkmy
BLEU = 31.12, 56.3/36.5/25.2/18.1 (BP=1.000, ratio=1.087, hyp_len=13297, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.221.0.33-1.40.0.27-1.31.2.17-8.78.1.61-5.00.pth, mybk
BLEU = 28.11, 54.2/33.2/22.2/15.6 (BP=1.000, ratio=1.083, hyp_len=12380, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.221.0.33-1.40.0.27-1.31.2.17-8.78.1.61-5.00.pth, bkmy
BLEU = 30.39, 55.0/35.3/24.5/18.0 (BP=1.000, ratio=1.101, hyp_len=13472, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.43-4.18.1.24-3.46.1.32-3.74.1.07-2.91.pth, mybk
BLEU = 30.50, 58.0/36.0/24.3/17.1 (BP=1.000, ratio=1.088, hyp_len=12440, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.43-4.18.1.24-3.46.1.32-3.74.1.07-2.91.pth, bkmy
BLEU = 42.45, 69.1/49.3/35.9/27.0 (BP=0.996, ratio=0.996, hyp_len=12180, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.222.0.35-1.43.0.28-1.33.2.21-9.11.1.68-5.38.pth, mybk
BLEU = 27.26, 53.1/32.0/21.5/15.1 (BP=1.000, ratio=1.096, hyp_len=12529, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.222.0.35-1.43.0.28-1.33.2.21-9.11.1.68-5.38.pth, bkmy
BLEU = 32.18, 56.4/37.2/26.3/19.4 (BP=1.000, ratio=1.103, hyp_len=13492, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.223.0.36-1.43.0.29-1.34.2.20-9.03.1.62-5.07.pth, mybk
BLEU = 27.59, 53.5/32.3/21.8/15.4 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.223.0.36-1.43.0.29-1.34.2.20-9.03.1.62-5.07.pth, bkmy
BLEU = 32.38, 57.2/37.8/26.4/19.3 (BP=1.000, ratio=1.079, hyp_len=13199, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.224.0.35-1.42.0.28-1.32.2.19-8.90.1.62-5.05.pth, mybk
BLEU = 27.15, 52.6/31.9/21.4/15.2 (BP=1.000, ratio=1.104, hyp_len=12624, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.224.0.35-1.42.0.28-1.32.2.19-8.90.1.62-5.05.pth, bkmy
BLEU = 31.65, 57.2/37.3/25.7/18.3 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.225.0.33-1.39.0.28-1.32.2.22-9.20.1.67-5.34.pth, mybk
BLEU = 27.65, 52.7/32.1/22.0/15.7 (BP=1.000, ratio=1.073, hyp_len=12265, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.225.0.33-1.39.0.28-1.32.2.22-9.20.1.67-5.34.pth, bkmy
BLEU = 31.96, 57.3/37.4/25.9/18.8 (BP=1.000, ratio=1.089, hyp_len=13320, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.226.0.36-1.43.0.29-1.34.2.19-8.91.1.68-5.37.pth, mybk
BLEU = 27.26, 52.8/31.8/21.5/15.3 (BP=1.000, ratio=1.098, hyp_len=12548, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.226.0.36-1.43.0.29-1.34.2.19-8.91.1.68-5.37.pth, bkmy
BLEU = 30.59, 55.5/35.7/24.6/17.9 (BP=1.000, ratio=1.104, hyp_len=13499, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.227.0.35-1.41.0.29-1.34.2.23-9.31.1.68-5.35.pth, mybk
BLEU = 27.15, 52.5/31.8/21.4/15.2 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.227.0.35-1.41.0.29-1.34.2.23-9.31.1.68-5.35.pth, bkmy
BLEU = 31.06, 55.8/36.3/25.2/18.3 (BP=1.000, ratio=1.094, hyp_len=13377, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.228.0.37-1.45.0.29-1.34.2.28-9.75.1.69-5.43.pth, mybk
BLEU = 28.14, 53.4/32.7/22.3/16.1 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.228.0.37-1.45.0.29-1.34.2.28-9.75.1.69-5.43.pth, bkmy
BLEU = 31.95, 56.9/37.2/25.9/19.0 (BP=1.000, ratio=1.090, hyp_len=13336, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.229.0.36-1.44.0.29-1.34.2.27-9.69.1.71-5.54.pth, mybk
BLEU = 27.69, 53.8/32.7/21.8/15.3 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.229.0.36-1.44.0.29-1.34.2.27-9.69.1.71-5.54.pth, bkmy
BLEU = 30.05, 55.0/35.2/24.2/17.4 (BP=1.000, ratio=1.113, hyp_len=13608, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.230.0.34-1.40.0.27-1.31.2.27-9.67.1.67-5.31.pth, mybk
BLEU = 28.09, 53.7/32.7/22.2/15.9 (BP=1.000, ratio=1.078, hyp_len=12322, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.230.0.34-1.40.0.27-1.31.2.27-9.67.1.67-5.31.pth, bkmy
BLEU = 31.66, 56.4/36.8/25.7/18.8 (BP=1.000, ratio=1.086, hyp_len=13280, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.231.0.36-1.43.0.28-1.33.2.24-9.35.1.66-5.26.pth, mybk
BLEU = 26.84, 53.3/31.9/21.1/14.5 (BP=1.000, ratio=1.091, hyp_len=12471, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.231.0.36-1.43.0.28-1.33.2.24-9.35.1.66-5.26.pth, bkmy
BLEU = 31.18, 56.4/36.4/25.3/18.2 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.40-4.04.1.17-3.21.1.36-3.90.1.06-2.88.pth, mybk
BLEU = 32.86, 60.5/38.7/26.4/18.9 (BP=1.000, ratio=1.052, hyp_len=12021, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.40-4.04.1.17-3.21.1.36-3.90.1.06-2.88.pth, bkmy
BLEU = 40.95, 67.5/47.7/34.2/25.5 (BP=1.000, ratio=1.026, hyp_len=12545, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.232.0.35-1.43.0.28-1.33.2.30-9.97.1.66-5.25.pth, mybk
BLEU = 26.82, 52.5/31.6/21.0/14.8 (BP=1.000, ratio=1.084, hyp_len=12393, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.232.0.35-1.43.0.28-1.33.2.30-9.97.1.66-5.25.pth, bkmy
BLEU = 31.08, 56.1/36.3/25.2/18.2 (BP=1.000, ratio=1.096, hyp_len=13407, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.233.0.34-1.40.0.27-1.31.2.28-9.80.1.62-5.07.pth, mybk
BLEU = 27.66, 53.8/32.6/21.8/15.3 (BP=1.000, ratio=1.050, hyp_len=12003, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.233.0.34-1.40.0.27-1.31.2.28-9.80.1.62-5.07.pth, bkmy
BLEU = 32.21, 56.9/37.3/26.2/19.3 (BP=1.000, ratio=1.080, hyp_len=13208, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.234.0.33-1.40.0.31-1.36.2.22-9.23.1.65-5.18.pth, mybk
BLEU = 27.37, 53.1/32.2/21.6/15.2 (BP=1.000, ratio=1.092, hyp_len=12479, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.234.0.33-1.40.0.31-1.36.2.22-9.23.1.65-5.18.pth, bkmy
BLEU = 30.54, 55.3/35.6/24.6/17.9 (BP=1.000, ratio=1.100, hyp_len=13448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.235.0.33-1.40.0.28-1.32.2.19-8.97.1.61-5.00.pth, mybk
BLEU = 28.62, 54.8/33.9/22.7/15.9 (BP=1.000, ratio=1.079, hyp_len=12340, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.235.0.33-1.40.0.28-1.32.2.19-8.97.1.61-5.00.pth, bkmy
BLEU = 31.90, 56.8/37.1/26.0/18.9 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.236.0.35-1.42.0.30-1.35.2.23-9.29.1.67-5.32.pth, mybk
BLEU = 27.22, 52.2/31.9/21.6/15.3 (BP=1.000, ratio=1.106, hyp_len=12648, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.236.0.35-1.42.0.30-1.35.2.23-9.29.1.67-5.32.pth, bkmy
BLEU = 31.74, 57.0/37.2/25.7/18.6 (BP=1.000, ratio=1.073, hyp_len=13122, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.237.0.35-1.41.0.28-1.32.2.31-10.09.1.69-5.40.pth, mybk
BLEU = 25.70, 50.6/30.0/20.1/14.3 (BP=1.000, ratio=1.096, hyp_len=12528, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.237.0.35-1.41.0.28-1.32.2.31-10.09.1.69-5.40.pth, bkmy
BLEU = 30.88, 55.7/36.1/25.0/18.1 (BP=1.000, ratio=1.107, hyp_len=13536, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.238.0.32-1.37.0.26-1.30.2.21-9.16.1.69-5.42.pth, mybk
BLEU = 27.89, 54.0/33.0/21.9/15.5 (BP=1.000, ratio=1.091, hyp_len=12467, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.238.0.32-1.37.0.26-1.30.2.21-9.16.1.69-5.42.pth, bkmy
BLEU = 31.97, 56.9/37.3/26.0/19.0 (BP=1.000, ratio=1.095, hyp_len=13395, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.239.0.39-1.48.0.30-1.35.2.27-9.70.1.68-5.35.pth, mybk
BLEU = 26.92, 52.6/32.0/21.2/14.7 (BP=1.000, ratio=1.087, hyp_len=12428, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.239.0.39-1.48.0.30-1.35.2.27-9.70.1.68-5.35.pth, bkmy
BLEU = 31.94, 56.5/36.9/26.1/19.2 (BP=1.000, ratio=1.078, hyp_len=13187, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.240.0.34-1.40.0.27-1.32.2.29-9.89.1.72-5.59.pth, mybk
BLEU = 26.84, 52.5/31.5/21.1/14.9 (BP=1.000, ratio=1.074, hyp_len=12277, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.240.0.34-1.40.0.27-1.32.2.29-9.89.1.72-5.59.pth, bkmy
BLEU = 31.03, 55.8/36.1/25.2/18.3 (BP=1.000, ratio=1.082, hyp_len=13234, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.241.0.36-1.43.0.29-1.33.2.29-9.84.1.72-5.59.pth, mybk
BLEU = 27.13, 53.0/32.3/21.4/14.8 (BP=1.000, ratio=1.088, hyp_len=12442, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.241.0.36-1.43.0.29-1.33.2.29-9.84.1.72-5.59.pth, bkmy
BLEU = 30.38, 55.0/35.3/24.7/17.7 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.42-4.12.1.19-3.30.1.35-3.85.1.07-2.91.pth, mybk
BLEU = 30.70, 57.5/36.3/24.7/17.3 (BP=1.000, ratio=1.095, hyp_len=12520, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.42-4.12.1.19-3.30.1.35-3.85.1.07-2.91.pth, bkmy
BLEU = 39.01, 65.1/45.7/32.6/23.9 (BP=1.000, ratio=1.066, hyp_len=13039, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.242.0.32-1.37.0.27-1.31.2.29-9.84.1.68-5.39.pth, mybk
BLEU = 27.03, 52.7/31.9/21.3/14.9 (BP=1.000, ratio=1.079, hyp_len=12334, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.242.0.32-1.37.0.27-1.31.2.29-9.84.1.68-5.39.pth, bkmy
BLEU = 32.37, 57.3/37.7/26.4/19.2 (BP=1.000, ratio=1.082, hyp_len=13240, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.243.0.33-1.39.0.26-1.30.2.26-9.56.1.71-5.52.pth, mybk
BLEU = 27.74, 53.1/32.3/22.0/15.7 (BP=1.000, ratio=1.084, hyp_len=12396, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.243.0.33-1.39.0.26-1.30.2.26-9.56.1.71-5.52.pth, bkmy
BLEU = 30.84, 56.0/36.1/24.9/18.0 (BP=1.000, ratio=1.098, hyp_len=13435, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.244.0.34-1.41.0.29-1.34.2.24-9.41.1.73-5.65.pth, mybk
BLEU = 28.74, 54.3/33.3/22.9/16.5 (BP=1.000, ratio=1.068, hyp_len=12213, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.244.0.34-1.41.0.29-1.34.2.24-9.41.1.73-5.65.pth, bkmy
BLEU = 30.70, 56.1/35.9/24.8/17.8 (BP=1.000, ratio=1.087, hyp_len=13296, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.245.0.32-1.38.0.26-1.29.2.26-9.61.1.74-5.71.pth, mybk
BLEU = 27.50, 52.7/32.1/21.8/15.5 (BP=1.000, ratio=1.085, hyp_len=12405, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.245.0.32-1.38.0.26-1.29.2.26-9.61.1.74-5.71.pth, bkmy
BLEU = 31.03, 55.9/36.2/25.2/18.2 (BP=1.000, ratio=1.101, hyp_len=13471, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.246.0.32-1.38.0.27-1.31.2.20-9.02.1.73-5.64.pth, mybk
BLEU = 27.43, 53.5/32.5/21.5/15.1 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.246.0.32-1.38.0.27-1.31.2.20-9.02.1.73-5.64.pth, bkmy
BLEU = 32.44, 57.6/37.8/26.4/19.3 (BP=1.000, ratio=1.099, hyp_len=13444, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.247.0.33-1.39.0.28-1.32.2.26-9.57.1.81-6.11.pth, mybk
BLEU = 27.82, 53.7/32.5/21.9/15.7 (BP=1.000, ratio=1.090, hyp_len=12462, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.247.0.33-1.39.0.28-1.32.2.26-9.57.1.81-6.11.pth, bkmy
BLEU = 31.73, 56.7/37.0/25.7/18.8 (BP=1.000, ratio=1.087, hyp_len=13292, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.248.0.32-1.38.0.28-1.32.2.19-8.93.1.77-5.85.pth, mybk
BLEU = 27.62, 52.9/32.3/21.8/15.6 (BP=1.000, ratio=1.077, hyp_len=12310, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.248.0.32-1.38.0.28-1.32.2.19-8.93.1.77-5.85.pth, bkmy
BLEU = 30.80, 55.6/36.1/25.0/18.0 (BP=1.000, ratio=1.092, hyp_len=13351, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.249.0.37-1.45.0.29-1.34.2.18-8.87.1.79-5.99.pth, mybk
BLEU = 27.80, 53.2/32.5/22.0/15.7 (BP=1.000, ratio=1.084, hyp_len=12388, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.249.0.37-1.45.0.29-1.34.2.18-8.87.1.79-5.99.pth, bkmy
BLEU = 30.94, 56.0/36.1/25.1/18.1 (BP=1.000, ratio=1.088, hyp_len=13308, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.250.0.35-1.42.0.30-1.35.2.19-8.90.1.76-5.80.pth, mybk
BLEU = 28.28, 54.1/33.1/22.3/16.0 (BP=1.000, ratio=1.071, hyp_len=12249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.250.0.35-1.42.0.30-1.35.2.19-8.90.1.76-5.80.pth, bkmy
BLEU = 31.99, 56.9/37.2/26.1/18.9 (BP=1.000, ratio=1.095, hyp_len=13388, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.251.0.38-1.46.0.30-1.35.2.23-9.32.1.70-5.46.pth, mybk
BLEU = 27.84, 53.9/32.9/22.1/15.4 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.251.0.38-1.46.0.30-1.35.2.23-9.32.1.70-5.46.pth, bkmy
BLEU = 31.32, 56.4/36.7/25.4/18.3 (BP=1.000, ratio=1.103, hyp_len=13489, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.82.1.14-3.11.1.35-3.88.1.05-2.85.pth, mybk
BLEU = 32.33, 60.2/38.1/25.9/18.4 (BP=1.000, ratio=1.063, hyp_len=12151, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.82.1.14-3.11.1.35-3.88.1.05-2.85.pth, bkmy
BLEU = 41.38, 67.1/47.6/34.8/26.4 (BP=1.000, ratio=1.019, hyp_len=12465, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.252.0.33-1.39.0.27-1.31.2.22-9.23.1.72-5.57.pth, mybk
BLEU = 27.18, 52.8/32.0/21.5/15.1 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.252.0.33-1.39.0.27-1.31.2.22-9.23.1.72-5.57.pth, bkmy
BLEU = 31.98, 57.0/37.4/26.1/18.8 (BP=1.000, ratio=1.097, hyp_len=13413, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.253.0.31-1.37.0.26-1.30.2.19-8.91.1.74-5.71.pth, mybk
BLEU = 26.49, 52.3/31.3/20.8/14.5 (BP=1.000, ratio=1.097, hyp_len=12542, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.253.0.31-1.37.0.26-1.30.2.19-8.91.1.74-5.71.pth, bkmy
BLEU = 31.02, 55.9/36.3/25.2/18.1 (BP=1.000, ratio=1.111, hyp_len=13591, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.254.0.34-1.40.0.28-1.32.2.23-9.29.1.74-5.71.pth, mybk
BLEU = 27.59, 53.6/32.6/21.8/15.2 (BP=1.000, ratio=1.092, hyp_len=12479, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.254.0.34-1.40.0.28-1.32.2.23-9.29.1.74-5.71.pth, bkmy
BLEU = 33.40, 58.2/38.7/27.3/20.2 (BP=1.000, ratio=1.074, hyp_len=13139, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.255.0.31-1.37.0.27-1.31.2.24-9.39.1.75-5.78.pth, mybk
BLEU = 26.10, 51.5/30.9/20.5/14.2 (BP=1.000, ratio=1.093, hyp_len=12497, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.255.0.31-1.37.0.27-1.31.2.24-9.39.1.75-5.78.pth, bkmy
BLEU = 30.24, 54.9/35.5/24.4/17.6 (BP=1.000, ratio=1.100, hyp_len=13458, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.256.0.34-1.40.0.26-1.30.2.24-9.35.1.80-6.05.pth, mybk
BLEU = 26.54, 51.9/31.2/20.9/14.6 (BP=1.000, ratio=1.082, hyp_len=12374, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.256.0.34-1.40.0.26-1.30.2.24-9.35.1.80-6.05.pth, bkmy
BLEU = 30.80, 56.0/36.0/24.9/17.9 (BP=1.000, ratio=1.095, hyp_len=13395, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.257.0.32-1.38.0.27-1.32.2.18-8.83.1.76-5.84.pth, mybk
BLEU = 27.45, 53.1/32.2/21.6/15.4 (BP=1.000, ratio=1.095, hyp_len=12523, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.257.0.32-1.38.0.27-1.32.2.18-8.83.1.76-5.84.pth, bkmy
BLEU = 31.00, 56.0/36.0/25.0/18.3 (BP=1.000, ratio=1.097, hyp_len=13421, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.258.0.39-1.48.0.31-1.37.2.23-9.34.1.74-5.70.pth, mybk
BLEU = 27.22, 52.6/32.0/21.5/15.2 (BP=1.000, ratio=1.086, hyp_len=12413, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.258.0.39-1.48.0.31-1.37.2.23-9.34.1.74-5.70.pth, bkmy
BLEU = 30.91, 56.0/36.3/25.1/17.9 (BP=1.000, ratio=1.104, hyp_len=13497, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.259.0.34-1.41.0.27-1.31.2.25-9.47.1.73-5.65.pth, mybk
BLEU = 27.27, 53.6/32.3/21.5/14.8 (BP=1.000, ratio=1.088, hyp_len=12438, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.259.0.34-1.41.0.27-1.31.2.25-9.47.1.73-5.65.pth, bkmy
BLEU = 32.11, 57.0/37.3/26.1/19.1 (BP=1.000, ratio=1.089, hyp_len=13314, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.260.0.32-1.38.0.27-1.31.2.33-10.27.1.70-5.46.pth, mybk
BLEU = 27.63, 54.0/32.7/21.8/15.2 (BP=1.000, ratio=1.077, hyp_len=12307, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.260.0.32-1.38.0.27-1.31.2.33-10.27.1.70-5.46.pth, bkmy
BLEU = 31.27, 56.0/36.4/25.3/18.5 (BP=1.000, ratio=1.074, hyp_len=13135, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.261.0.34-1.40.0.28-1.32.2.26-9.54.1.64-5.18.pth, mybk
BLEU = 27.47, 53.1/32.4/21.7/15.3 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.261.0.34-1.40.0.28-1.32.2.26-9.54.1.64-5.18.pth, bkmy
BLEU = 31.04, 55.7/36.0/25.2/18.3 (BP=1.000, ratio=1.109, hyp_len=13565, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.36-3.90.1.19-3.29.1.37-3.94.1.02-2.78.pth, mybk
BLEU = 32.48, 59.5/37.9/26.2/18.8 (BP=1.000, ratio=1.045, hyp_len=11942, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.36-3.90.1.19-3.29.1.37-3.94.1.02-2.78.pth, bkmy
BLEU = 40.15, 66.3/46.8/33.6/24.9 (BP=1.000, ratio=1.047, hyp_len=12810, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.262.0.37-1.44.0.34-1.41.2.23-9.28.1.72-5.57.pth, mybk
BLEU = 27.25, 53.1/32.0/21.4/15.1 (BP=1.000, ratio=1.070, hyp_len=12229, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.262.0.37-1.44.0.34-1.41.2.23-9.28.1.72-5.57.pth, bkmy
BLEU = 30.32, 55.2/35.5/24.5/17.6 (BP=1.000, ratio=1.105, hyp_len=13520, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.263.0.31-1.37.0.26-1.30.2.30-9.98.1.68-5.38.pth, mybk
BLEU = 27.78, 53.6/32.6/21.9/15.5 (BP=1.000, ratio=1.079, hyp_len=12333, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.263.0.31-1.37.0.26-1.30.2.30-9.98.1.68-5.38.pth, bkmy
BLEU = 31.43, 56.5/36.8/25.5/18.4 (BP=1.000, ratio=1.086, hyp_len=13280, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.264.0.31-1.37.0.25-1.29.2.21-9.13.1.73-5.65.pth, mybk
BLEU = 28.38, 54.2/33.4/22.5/16.0 (BP=1.000, ratio=1.099, hyp_len=12561, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.264.0.31-1.37.0.25-1.29.2.21-9.13.1.73-5.65.pth, bkmy
BLEU = 30.04, 54.6/35.2/24.2/17.4 (BP=1.000, ratio=1.094, hyp_len=13376, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.265.0.35-1.42.0.30-1.35.2.21-9.08.1.70-5.49.pth, mybk
BLEU = 27.64, 53.5/32.5/21.9/15.3 (BP=1.000, ratio=1.096, hyp_len=12526, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.265.0.35-1.42.0.30-1.35.2.21-9.08.1.70-5.49.pth, bkmy
BLEU = 31.15, 56.1/36.4/25.3/18.2 (BP=1.000, ratio=1.097, hyp_len=13416, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.266.0.35-1.42.0.28-1.32.2.27-9.65.1.67-5.31.pth, mybk
BLEU = 27.37, 53.5/32.4/21.6/15.0 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.266.0.35-1.42.0.28-1.32.2.27-9.65.1.67-5.31.pth, bkmy
BLEU = 30.81, 55.6/36.0/24.9/18.1 (BP=1.000, ratio=1.102, hyp_len=13482, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.267.0.33-1.39.0.26-1.30.2.35-10.46.1.74-5.67.pth, mybk
BLEU = 28.11, 53.2/32.8/22.3/16.0 (BP=1.000, ratio=1.094, hyp_len=12507, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.267.0.33-1.39.0.26-1.30.2.35-10.46.1.74-5.67.pth, bkmy
BLEU = 30.51, 55.0/35.7/24.7/17.9 (BP=1.000, ratio=1.117, hyp_len=13658, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.268.0.31-1.36.0.26-1.30.2.30-10.00.1.71-5.51.pth, mybk
BLEU = 27.36, 53.6/32.4/21.4/15.1 (BP=1.000, ratio=1.095, hyp_len=12514, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.268.0.31-1.36.0.26-1.30.2.30-10.00.1.71-5.51.pth, bkmy
BLEU = 31.14, 55.6/36.4/25.4/18.3 (BP=1.000, ratio=1.101, hyp_len=13471, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.269.0.31-1.37.0.25-1.29.2.36-10.56.1.76-5.83.pth, mybk
BLEU = 26.84, 52.4/31.6/21.1/14.8 (BP=1.000, ratio=1.087, hyp_len=12431, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.269.0.31-1.37.0.25-1.29.2.36-10.56.1.76-5.83.pth, bkmy
BLEU = 31.65, 56.4/36.9/25.7/18.8 (BP=1.000, ratio=1.094, hyp_len=13382, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.270.0.31-1.36.0.26-1.30.2.32-10.17.1.72-5.59.pth, mybk
BLEU = 29.01, 54.5/33.6/23.1/16.8 (BP=1.000, ratio=1.065, hyp_len=12176, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.270.0.31-1.36.0.26-1.30.2.32-10.17.1.72-5.59.pth, bkmy
BLEU = 32.39, 57.8/38.1/26.4/18.9 (BP=1.000, ratio=1.080, hyp_len=13206, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.271.0.33-1.39.0.27-1.31.2.35-10.44.1.72-5.61.pth, mybk
BLEU = 27.99, 53.3/32.6/22.1/15.9 (BP=1.000, ratio=1.091, hyp_len=12470, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.271.0.33-1.39.0.27-1.31.2.35-10.44.1.72-5.61.pth, bkmy
BLEU = 30.69, 56.0/36.0/24.8/17.7 (BP=1.000, ratio=1.092, hyp_len=13353, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.24-3.46.1.04-2.84.1.34-3.80.1.04-2.83.pth, mybk
BLEU = 32.48, 60.3/38.3/26.1/18.5 (BP=1.000, ratio=1.062, hyp_len=12145, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.24-3.46.1.04-2.84.1.34-3.80.1.04-2.83.pth, bkmy
BLEU = 41.84, 67.6/48.2/35.4/26.6 (BP=1.000, ratio=1.026, hyp_len=12554, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.272.0.33-1.39.0.26-1.30.2.37-10.65.1.75-5.74.pth, mybk
BLEU = 27.25, 52.9/32.1/21.5/15.1 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.272.0.33-1.39.0.26-1.30.2.37-10.65.1.75-5.74.pth, bkmy
BLEU = 30.74, 55.6/35.9/24.8/18.1 (BP=1.000, ratio=1.105, hyp_len=13511, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.273.0.33-1.40.0.28-1.32.2.32-10.16.1.70-5.49.pth, mybk
BLEU = 26.67, 52.6/31.5/20.8/14.6 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.273.0.33-1.40.0.28-1.32.2.32-10.16.1.70-5.49.pth, bkmy
BLEU = 31.35, 56.2/36.4/25.4/18.6 (BP=1.000, ratio=1.097, hyp_len=13414, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.274.0.33-1.38.0.27-1.31.2.33-10.27.1.69-5.42.pth, mybk
BLEU = 27.52, 53.5/32.6/21.7/15.1 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.274.0.33-1.38.0.27-1.31.2.33-10.27.1.69-5.42.pth, bkmy
BLEU = 31.99, 57.2/37.3/26.0/18.9 (BP=1.000, ratio=1.090, hyp_len=13334, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.275.0.37-1.45.0.30-1.35.2.27-9.69.1.72-5.60.pth, mybk
BLEU = 27.83, 53.6/32.7/21.9/15.6 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.275.0.37-1.45.0.30-1.35.2.27-9.69.1.72-5.60.pth, bkmy
BLEU = 30.58, 55.9/35.9/24.7/17.7 (BP=1.000, ratio=1.100, hyp_len=13457, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.276.0.30-1.35.0.26-1.30.2.30-9.96.1.70-5.47.pth, mybk
BLEU = 27.54, 53.9/32.7/21.5/15.2 (BP=1.000, ratio=1.092, hyp_len=12482, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.276.0.30-1.35.0.26-1.30.2.30-9.96.1.70-5.47.pth, bkmy
BLEU = 31.53, 56.7/37.0/25.5/18.5 (BP=1.000, ratio=1.090, hyp_len=13333, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.277.0.32-1.37.0.26-1.30.2.31-10.08.1.70-5.45.pth, mybk
BLEU = 27.63, 53.6/32.4/21.8/15.4 (BP=1.000, ratio=1.079, hyp_len=12334, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.277.0.32-1.37.0.26-1.30.2.31-10.08.1.70-5.45.pth, bkmy
BLEU = 30.81, 56.0/36.3/24.8/17.9 (BP=1.000, ratio=1.106, hyp_len=13524, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.278.0.31-1.36.0.25-1.28.2.29-9.84.1.72-5.58.pth, mybk
BLEU = 27.44, 53.4/32.4/21.7/15.1 (BP=1.000, ratio=1.091, hyp_len=12470, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.278.0.31-1.36.0.25-1.28.2.29-9.84.1.72-5.58.pth, bkmy
BLEU = 31.55, 56.2/36.7/25.6/18.8 (BP=1.000, ratio=1.102, hyp_len=13476, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.279.0.35-1.41.0.28-1.33.2.27-9.64.1.73-5.62.pth, mybk
BLEU = 27.00, 53.0/32.1/21.2/14.7 (BP=1.000, ratio=1.106, hyp_len=12640, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.279.0.35-1.41.0.28-1.33.2.27-9.64.1.73-5.62.pth, bkmy
BLEU = 31.83, 56.5/36.9/25.9/19.0 (BP=1.000, ratio=1.083, hyp_len=13250, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.280.0.33-1.39.0.27-1.31.2.26-9.55.1.76-5.83.pth, mybk
BLEU = 26.82, 52.7/31.7/21.1/14.7 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.280.0.33-1.39.0.27-1.31.2.26-9.55.1.76-5.83.pth, bkmy
BLEU = 31.91, 56.8/36.9/25.9/19.1 (BP=1.000, ratio=1.080, hyp_len=13206, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.281.0.33-1.39.0.28-1.32.2.30-10.02.1.78-5.91.pth, mybk
BLEU = 27.17, 53.1/32.0/21.3/15.0 (BP=1.000, ratio=1.098, hyp_len=12552, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.281.0.33-1.39.0.28-1.32.2.30-10.02.1.78-5.91.pth, bkmy
BLEU = 31.52, 56.4/36.8/25.6/18.6 (BP=1.000, ratio=1.093, hyp_len=13366, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.21-3.35.1.03-2.81.1.39-4.01.1.08-2.95.pth, mybk
BLEU = 31.77, 59.6/37.4/25.4/18.0 (BP=1.000, ratio=1.063, hyp_len=12149, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.21-3.35.1.03-2.81.1.39-4.01.1.08-2.95.pth, bkmy
BLEU = 39.66, 65.5/46.1/33.2/24.7 (BP=1.000, ratio=1.060, hyp_len=12968, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.282.0.37-1.44.0.30-1.35.2.26-9.60.1.77-5.90.pth, mybk
BLEU = 26.20, 51.9/31.3/20.5/14.2 (BP=1.000, ratio=1.132, hyp_len=12939, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.282.0.37-1.44.0.30-1.35.2.26-9.60.1.77-5.90.pth, bkmy
BLEU = 31.05, 55.9/36.2/25.2/18.3 (BP=1.000, ratio=1.099, hyp_len=13439, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.283.0.30-1.35.0.25-1.29.2.30-9.97.1.71-5.53.pth, mybk
BLEU = 26.70, 52.7/31.7/20.9/14.6 (BP=1.000, ratio=1.089, hyp_len=12449, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.283.0.30-1.35.0.25-1.29.2.30-9.97.1.71-5.53.pth, bkmy
BLEU = 33.39, 57.9/38.4/27.4/20.4 (BP=1.000, ratio=1.073, hyp_len=13121, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.284.0.30-1.35.0.25-1.29.2.28-9.82.1.79-5.97.pth, mybk
BLEU = 27.89, 53.9/32.8/21.9/15.6 (BP=1.000, ratio=1.074, hyp_len=12278, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.284.0.30-1.35.0.25-1.29.2.28-9.82.1.79-5.97.pth, bkmy
BLEU = 31.14, 55.8/36.0/25.3/18.5 (BP=1.000, ratio=1.097, hyp_len=13421, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.285.0.31-1.37.0.26-1.30.2.28-9.73.1.76-5.79.pth, mybk
BLEU = 26.75, 52.2/31.5/21.1/14.8 (BP=1.000, ratio=1.099, hyp_len=12569, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.285.0.31-1.37.0.26-1.30.2.28-9.73.1.76-5.79.pth, bkmy
BLEU = 31.72, 56.8/36.9/25.7/18.8 (BP=1.000, ratio=1.088, hyp_len=13308, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.286.0.36-1.43.0.30-1.35.2.32-10.13.1.72-5.59.pth, mybk
BLEU = 26.90, 52.1/31.4/21.2/15.1 (BP=1.000, ratio=1.076, hyp_len=12300, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.286.0.36-1.43.0.30-1.35.2.32-10.13.1.72-5.59.pth, bkmy
BLEU = 31.61, 56.7/37.0/25.7/18.6 (BP=1.000, ratio=1.093, hyp_len=13367, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.287.0.30-1.35.0.26-1.29.2.28-9.78.1.74-5.70.pth, mybk
BLEU = 28.37, 54.6/33.4/22.5/15.8 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.287.0.30-1.35.0.26-1.29.2.28-9.78.1.74-5.70.pth, bkmy
BLEU = 30.52, 55.5/35.4/24.7/17.8 (BP=1.000, ratio=1.083, hyp_len=13244, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.288.0.33-1.39.0.29-1.33.2.23-9.34.1.75-5.77.pth, mybk
BLEU = 28.21, 54.1/33.0/22.3/15.9 (BP=1.000, ratio=1.079, hyp_len=12339, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.288.0.33-1.39.0.29-1.33.2.23-9.34.1.75-5.77.pth, bkmy
BLEU = 31.70, 56.5/36.7/25.7/18.9 (BP=1.000, ratio=1.079, hyp_len=13203, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.289.0.34-1.40.0.27-1.31.2.29-9.83.1.73-5.63.pth, mybk
BLEU = 27.01, 53.2/32.1/21.2/14.7 (BP=1.000, ratio=1.103, hyp_len=12615, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.289.0.34-1.40.0.27-1.31.2.29-9.83.1.73-5.63.pth, bkmy
BLEU = 30.61, 54.8/35.6/24.9/18.1 (BP=1.000, ratio=1.117, hyp_len=13664, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.290.0.30-1.35.0.25-1.29.2.29-9.84.1.73-5.61.pth, mybk
BLEU = 27.99, 53.5/32.6/22.1/15.9 (BP=1.000, ratio=1.085, hyp_len=12404, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.290.0.30-1.35.0.25-1.29.2.29-9.84.1.73-5.61.pth, bkmy
BLEU = 32.17, 57.1/37.4/26.2/19.1 (BP=1.000, ratio=1.080, hyp_len=13215, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.291.0.33-1.39.0.27-1.31.2.27-9.69.1.73-5.63.pth, mybk
BLEU = 26.68, 52.3/31.5/21.0/14.6 (BP=1.000, ratio=1.093, hyp_len=12498, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.291.0.33-1.39.0.27-1.31.2.27-9.69.1.73-5.63.pth, bkmy
BLEU = 30.49, 54.8/35.4/24.7/18.0 (BP=1.000, ratio=1.118, hyp_len=13670, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.32-3.75.1.09-2.97.1.37-3.92.1.06-2.88.pth, mybk
BLEU = 32.33, 59.8/38.2/26.0/18.4 (BP=1.000, ratio=1.068, hyp_len=12206, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.32-3.75.1.09-2.97.1.37-3.92.1.06-2.88.pth, bkmy
BLEU = 41.72, 67.4/48.1/35.2/26.6 (BP=1.000, ratio=1.058, hyp_len=12935, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.292.0.28-1.33.0.24-1.27.2.25-9.45.1.72-5.57.pth, mybk
BLEU = 27.23, 53.0/32.0/21.4/15.1 (BP=1.000, ratio=1.105, hyp_len=12636, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.292.0.28-1.33.0.24-1.27.2.25-9.45.1.72-5.57.pth, bkmy
BLEU = 32.32, 57.2/37.4/26.3/19.4 (BP=1.000, ratio=1.080, hyp_len=13204, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.293.0.31-1.36.0.25-1.28.2.27-9.72.1.72-5.61.pth, mybk
BLEU = 27.98, 53.4/32.9/22.2/15.7 (BP=1.000, ratio=1.097, hyp_len=12542, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.293.0.31-1.36.0.25-1.28.2.27-9.72.1.72-5.61.pth, bkmy
BLEU = 32.15, 57.1/37.3/26.2/19.2 (BP=1.000, ratio=1.082, hyp_len=13238, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.294.0.29-1.34.0.24-1.28.2.23-9.34.1.74-5.72.pth, mybk
BLEU = 26.37, 51.6/31.1/20.6/14.6 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.294.0.29-1.34.0.24-1.28.2.23-9.34.1.74-5.72.pth, bkmy
BLEU = 31.27, 56.3/36.3/25.3/18.5 (BP=1.000, ratio=1.076, hyp_len=13161, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.295.0.32-1.37.0.26-1.29.2.21-9.15.1.74-5.69.pth, mybk
BLEU = 27.56, 53.4/32.6/21.8/15.2 (BP=1.000, ratio=1.080, hyp_len=12341, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.295.0.32-1.37.0.26-1.29.2.21-9.15.1.74-5.69.pth, bkmy
BLEU = 32.22, 56.8/37.5/26.3/19.2 (BP=1.000, ratio=1.086, hyp_len=13285, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.296.0.30-1.35.0.26-1.29.2.21-9.12.1.71-5.55.pth, mybk
BLEU = 26.29, 52.1/31.3/20.6/14.3 (BP=1.000, ratio=1.079, hyp_len=12336, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.296.0.30-1.35.0.26-1.29.2.21-9.12.1.71-5.55.pth, bkmy
BLEU = 32.31, 57.2/37.6/26.3/19.3 (BP=1.000, ratio=1.098, hyp_len=13424, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.297.0.30-1.35.0.25-1.29.2.22-9.25.1.77-5.87.pth, mybk
BLEU = 27.84, 54.2/33.0/21.8/15.4 (BP=1.000, ratio=1.072, hyp_len=12254, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.297.0.30-1.35.0.25-1.29.2.22-9.25.1.77-5.87.pth, bkmy
BLEU = 32.17, 56.7/37.3/26.2/19.3 (BP=1.000, ratio=1.100, hyp_len=13456, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.298.0.31-1.36.0.25-1.28.2.24-9.35.1.73-5.62.pth, mybk
BLEU = 27.37, 53.1/32.3/21.6/15.1 (BP=1.000, ratio=1.091, hyp_len=12476, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.298.0.31-1.36.0.25-1.28.2.24-9.35.1.73-5.62.pth, bkmy
BLEU = 31.42, 56.0/36.5/25.5/18.7 (BP=1.000, ratio=1.094, hyp_len=13379, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.299.0.29-1.34.0.24-1.28.2.24-9.42.1.76-5.81.pth, mybk
BLEU = 27.12, 53.4/32.1/21.3/14.8 (BP=1.000, ratio=1.072, hyp_len=12260, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.299.0.29-1.34.0.24-1.28.2.24-9.42.1.76-5.81.pth, bkmy
BLEU = 31.56, 56.5/36.7/25.6/18.7 (BP=1.000, ratio=1.094, hyp_len=13375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.300.0.31-1.36.0.26-1.29.2.30-10.02.1.74-5.70.pth, mybk
BLEU = 25.00, 50.4/29.7/19.5/13.4 (BP=1.000, ratio=1.103, hyp_len=12609, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.300.0.31-1.36.0.26-1.29.2.30-10.02.1.74-5.70.pth, bkmy
BLEU = 30.39, 55.1/35.6/24.5/17.7 (BP=1.000, ratio=1.101, hyp_len=13463, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.301.0.38-1.46.0.28-1.32.2.27-9.65.1.77-5.85.pth, mybk
BLEU = 26.33, 52.6/31.0/20.5/14.4 (BP=1.000, ratio=1.089, hyp_len=12446, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.301.0.38-1.46.0.28-1.32.2.27-9.65.1.77-5.85.pth, bkmy
BLEU = 32.17, 57.0/37.4/26.2/19.2 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.24-3.46.1.09-2.98.1.41-4.09.1.07-2.90.pth, mybk
BLEU = 28.35, 55.5/34.0/22.4/15.3 (BP=1.000, ratio=1.114, hyp_len=12734, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.24-3.46.1.09-2.98.1.41-4.09.1.07-2.90.pth, bkmy
BLEU = 41.60, 66.8/47.9/35.0/26.7 (BP=1.000, ratio=1.023, hyp_len=12507, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.302.0.30-1.35.0.25-1.28.2.27-9.67.1.72-5.59.pth, mybk
BLEU = 26.66, 52.5/31.4/20.9/14.7 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.302.0.30-1.35.0.25-1.28.2.27-9.67.1.72-5.59.pth, bkmy
BLEU = 31.89, 57.0/37.3/25.9/18.8 (BP=1.000, ratio=1.091, hyp_len=13345, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.303.0.29-1.33.0.24-1.27.2.25-9.51.1.76-5.82.pth, mybk
BLEU = 26.64, 53.0/31.7/20.8/14.4 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.303.0.29-1.33.0.24-1.27.2.25-9.51.1.76-5.82.pth, bkmy
BLEU = 30.53, 55.7/35.9/24.6/17.6 (BP=1.000, ratio=1.082, hyp_len=13235, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.304.0.29-1.34.0.24-1.27.2.23-9.33.1.74-5.71.pth, mybk
BLEU = 28.39, 53.7/33.0/22.5/16.3 (BP=1.000, ratio=1.080, hyp_len=12347, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.304.0.29-1.34.0.24-1.27.2.23-9.33.1.74-5.71.pth, bkmy
BLEU = 31.37, 55.7/36.5/25.4/18.7 (BP=1.000, ratio=1.080, hyp_len=13204, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.305.0.30-1.35.0.25-1.28.2.31-10.06.1.73-5.64.pth, mybk
BLEU = 26.58, 52.1/31.1/20.9/14.7 (BP=1.000, ratio=1.093, hyp_len=12493, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.305.0.30-1.35.0.25-1.28.2.31-10.06.1.73-5.64.pth, bkmy
BLEU = 30.89, 55.7/36.3/25.0/18.0 (BP=1.000, ratio=1.107, hyp_len=13545, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.306.0.36-1.43.0.31-1.37.2.24-9.44.1.81-6.13.pth, mybk
BLEU = 26.16, 52.0/30.9/20.3/14.3 (BP=1.000, ratio=1.096, hyp_len=12532, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.306.0.36-1.43.0.31-1.37.2.24-9.44.1.81-6.13.pth, bkmy
BLEU = 31.04, 55.8/36.0/25.3/18.3 (BP=1.000, ratio=1.086, hyp_len=13284, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.307.0.32-1.38.0.26-1.30.2.30-9.95.1.81-6.12.pth, mybk
BLEU = 26.85, 52.0/31.4/21.2/15.0 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.307.0.32-1.38.0.26-1.30.2.30-9.95.1.81-6.12.pth, bkmy
BLEU = 31.63, 57.0/37.1/25.6/18.5 (BP=1.000, ratio=1.093, hyp_len=13368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.308.0.29-1.34.0.24-1.27.2.20-9.02.1.79-6.00.pth, mybk
BLEU = 28.03, 53.7/32.7/22.1/15.9 (BP=1.000, ratio=1.094, hyp_len=12502, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.308.0.29-1.34.0.24-1.27.2.20-9.02.1.79-6.00.pth, bkmy
BLEU = 31.11, 56.0/36.2/25.2/18.3 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.309.0.33-1.40.0.28-1.32.2.28-9.80.1.82-6.16.pth, mybk
BLEU = 27.24, 53.0/32.0/21.4/15.2 (BP=1.000, ratio=1.110, hyp_len=12686, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.309.0.33-1.40.0.28-1.32.2.28-9.80.1.82-6.16.pth, bkmy
BLEU = 29.26, 53.6/34.3/23.7/16.8 (BP=1.000, ratio=1.129, hyp_len=13808, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.310.0.30-1.35.0.24-1.28.2.30-9.93.1.81-6.09.pth, mybk
BLEU = 27.09, 53.4/31.9/21.2/14.9 (BP=1.000, ratio=1.076, hyp_len=12297, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.310.0.30-1.35.0.24-1.28.2.30-9.93.1.81-6.09.pth, bkmy
BLEU = 31.70, 56.2/36.8/25.8/18.9 (BP=1.000, ratio=1.088, hyp_len=13310, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.311.0.33-1.39.0.32-1.38.2.30-9.96.1.80-6.02.pth, mybk
BLEU = 26.72, 52.3/31.5/21.0/14.8 (BP=1.000, ratio=1.092, hyp_len=12479, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.311.0.33-1.39.0.32-1.38.2.30-9.96.1.80-6.02.pth, bkmy
BLEU = 31.80, 56.1/36.7/25.8/19.2 (BP=1.000, ratio=1.085, hyp_len=13272, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.23-3.43.1.01-2.75.1.43-4.19.1.11-3.04.pth, mybk
BLEU = 31.60, 59.5/37.2/25.1/17.9 (BP=1.000, ratio=1.059, hyp_len=12102, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.23-3.43.1.01-2.75.1.43-4.19.1.11-3.04.pth, bkmy
BLEU = 38.28, 64.0/44.4/31.8/23.7 (BP=1.000, ratio=1.049, hyp_len=12828, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.312.0.30-1.36.0.25-1.29.2.27-9.70.1.85-6.33.pth, mybk
BLEU = 27.88, 53.9/32.8/22.0/15.6 (BP=1.000, ratio=1.077, hyp_len=12317, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.312.0.30-1.36.0.25-1.29.2.27-9.70.1.85-6.33.pth, bkmy
BLEU = 30.48, 55.1/35.5/24.6/17.9 (BP=1.000, ratio=1.105, hyp_len=13516, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.313.0.29-1.34.0.25-1.29.2.29-9.84.1.84-6.31.pth, mybk
BLEU = 27.27, 52.5/31.7/21.5/15.4 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.313.0.29-1.34.0.25-1.29.2.29-9.84.1.84-6.31.pth, bkmy
BLEU = 31.13, 56.1/36.4/25.3/18.2 (BP=1.000, ratio=1.088, hyp_len=13306, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.314.0.32-1.38.0.25-1.29.2.27-9.67.1.83-6.26.pth, mybk
BLEU = 26.95, 52.1/31.3/21.2/15.2 (BP=1.000, ratio=1.105, hyp_len=12627, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.314.0.32-1.38.0.25-1.29.2.27-9.67.1.83-6.26.pth, bkmy
BLEU = 30.87, 56.0/36.1/25.0/17.9 (BP=1.000, ratio=1.084, hyp_len=13256, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.315.0.33-1.39.0.27-1.31.2.29-9.87.1.83-6.21.pth, mybk
BLEU = 26.87, 52.9/31.6/21.1/14.8 (BP=1.000, ratio=1.089, hyp_len=12455, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.315.0.33-1.39.0.27-1.31.2.29-9.87.1.83-6.21.pth, bkmy
BLEU = 30.80, 55.1/35.8/25.1/18.2 (BP=1.000, ratio=1.101, hyp_len=13471, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.316.0.30-1.35.0.26-1.29.2.33-10.30.1.85-6.38.pth, mybk
BLEU = 27.58, 54.0/32.5/21.7/15.2 (BP=1.000, ratio=1.070, hyp_len=12227, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.316.0.30-1.35.0.26-1.29.2.33-10.30.1.85-6.38.pth, bkmy
BLEU = 31.42, 56.1/36.6/25.6/18.6 (BP=1.000, ratio=1.086, hyp_len=13288, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.317.0.29-1.33.0.23-1.26.2.31-10.06.1.82-6.18.pth, mybk
BLEU = 26.94, 52.8/31.8/21.1/14.8 (BP=1.000, ratio=1.096, hyp_len=12524, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.317.0.29-1.33.0.23-1.26.2.31-10.06.1.82-6.18.pth, bkmy
BLEU = 30.69, 55.6/35.8/24.8/18.0 (BP=1.000, ratio=1.108, hyp_len=13546, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.318.0.29-1.34.0.25-1.29.2.28-9.82.1.81-6.12.pth, mybk
BLEU = 27.79, 53.8/32.7/21.9/15.5 (BP=1.000, ratio=1.077, hyp_len=12307, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.318.0.29-1.34.0.25-1.29.2.28-9.82.1.81-6.12.pth, bkmy
BLEU = 29.78, 54.3/34.8/24.0/17.4 (BP=1.000, ratio=1.103, hyp_len=13495, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.319.0.31-1.36.0.26-1.29.2.26-9.54.1.82-6.20.pth, mybk
BLEU = 26.52, 52.8/31.4/20.7/14.4 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.319.0.31-1.36.0.26-1.29.2.26-9.54.1.82-6.20.pth, bkmy
BLEU = 31.55, 56.9/37.0/25.6/18.4 (BP=1.000, ratio=1.075, hyp_len=13153, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.320.0.30-1.35.0.24-1.28.2.26-9.61.1.77-5.85.pth, mybk
BLEU = 27.04, 52.7/31.8/21.3/15.0 (BP=1.000, ratio=1.103, hyp_len=12608, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.320.0.30-1.35.0.24-1.28.2.26-9.61.1.77-5.85.pth, bkmy
BLEU = 31.42, 56.2/36.3/25.4/18.8 (BP=1.000, ratio=1.076, hyp_len=13159, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.321.0.30-1.34.0.25-1.29.2.20-8.99.1.80-6.06.pth, mybk
BLEU = 27.39, 53.3/32.3/21.5/15.2 (BP=1.000, ratio=1.096, hyp_len=12529, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.321.0.30-1.34.0.25-1.29.2.20-8.99.1.80-6.06.pth, bkmy
BLEU = 31.31, 55.6/36.4/25.6/18.6 (BP=1.000, ratio=1.110, hyp_len=13573, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.12-3.07.0.93-2.54.1.38-3.98.1.09-2.98.pth, mybk
BLEU = 32.39, 60.8/38.6/25.9/18.1 (BP=1.000, ratio=1.055, hyp_len=12060, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.12-3.07.0.93-2.54.1.38-3.98.1.09-2.98.pth, bkmy
BLEU = 41.65, 67.2/47.9/35.1/26.7 (BP=1.000, ratio=1.022, hyp_len=12497, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.322.0.33-1.39.0.28-1.33.2.30-10.01.1.78-5.92.pth, mybk
BLEU = 25.74, 51.1/30.4/20.1/14.1 (BP=1.000, ratio=1.116, hyp_len=12756, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.322.0.33-1.39.0.28-1.33.2.30-10.01.1.78-5.92.pth, bkmy
BLEU = 31.64, 56.4/36.7/25.7/18.8 (BP=1.000, ratio=1.094, hyp_len=13376, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.323.0.31-1.36.0.26-1.29.2.28-9.80.1.84-6.30.pth, mybk
BLEU = 26.79, 52.1/31.6/21.1/14.9 (BP=1.000, ratio=1.093, hyp_len=12494, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.323.0.31-1.36.0.26-1.29.2.28-9.80.1.84-6.30.pth, bkmy
BLEU = 30.66, 55.3/36.0/24.8/17.9 (BP=1.000, ratio=1.106, hyp_len=13525, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.324.0.29-1.34.0.24-1.27.2.25-9.53.1.84-6.30.pth, mybk
BLEU = 27.36, 53.4/32.3/21.6/15.1 (BP=1.000, ratio=1.104, hyp_len=12620, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.324.0.29-1.34.0.24-1.27.2.25-9.53.1.84-6.30.pth, bkmy
BLEU = 30.88, 55.1/35.9/25.1/18.3 (BP=1.000, ratio=1.101, hyp_len=13472, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.325.0.30-1.36.0.26-1.30.2.26-9.56.1.83-6.21.pth, mybk
BLEU = 27.02, 52.9/31.7/21.2/15.0 (BP=1.000, ratio=1.056, hyp_len=12073, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.325.0.30-1.36.0.26-1.30.2.26-9.56.1.83-6.21.pth, bkmy
BLEU = 31.21, 55.5/36.1/25.5/18.6 (BP=1.000, ratio=1.113, hyp_len=13618, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.326.0.28-1.33.0.25-1.29.2.30-9.96.1.81-6.09.pth, mybk
BLEU = 27.51, 53.3/32.4/21.8/15.2 (BP=1.000, ratio=1.092, hyp_len=12482, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.326.0.28-1.33.0.25-1.29.2.30-9.96.1.81-6.09.pth, bkmy
BLEU = 31.26, 55.8/36.4/25.4/18.5 (BP=1.000, ratio=1.099, hyp_len=13438, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.327.0.30-1.34.0.25-1.28.2.33-10.23.1.85-6.34.pth, mybk
BLEU = 27.75, 53.6/32.5/21.9/15.5 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.327.0.30-1.34.0.25-1.28.2.33-10.23.1.85-6.34.pth, bkmy
BLEU = 30.59, 55.5/35.7/24.8/17.8 (BP=1.000, ratio=1.083, hyp_len=13243, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.328.0.29-1.34.0.25-1.28.2.32-10.17.1.78-5.93.pth, mybk
BLEU = 27.63, 53.4/32.6/21.7/15.4 (BP=1.000, ratio=1.075, hyp_len=12295, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.328.0.29-1.34.0.25-1.28.2.32-10.17.1.78-5.93.pth, bkmy
BLEU = 28.67, 53.9/33.8/23.0/16.1 (BP=1.000, ratio=1.119, hyp_len=13686, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.329.0.30-1.34.0.25-1.28.2.29-9.87.1.77-5.86.pth, mybk
BLEU = 26.12, 51.7/30.9/20.5/14.2 (BP=1.000, ratio=1.091, hyp_len=12478, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.329.0.30-1.34.0.25-1.28.2.29-9.87.1.77-5.86.pth, bkmy
BLEU = 31.69, 56.4/37.1/25.7/18.7 (BP=1.000, ratio=1.079, hyp_len=13195, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.330.0.29-1.33.0.23-1.26.2.33-10.29.1.86-6.44.pth, mybk
BLEU = 27.06, 52.7/31.9/21.4/14.9 (BP=1.000, ratio=1.093, hyp_len=12500, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.330.0.29-1.33.0.23-1.26.2.33-10.29.1.86-6.44.pth, bkmy
BLEU = 31.56, 56.0/36.7/25.7/18.8 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.331.0.31-1.36.0.25-1.29.2.32-10.22.1.81-6.09.pth, mybk
BLEU = 27.55, 53.5/32.3/21.7/15.4 (BP=1.000, ratio=1.100, hyp_len=12580, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.331.0.31-1.36.0.25-1.29.2.32-10.22.1.81-6.09.pth, bkmy
BLEU = 30.52, 55.3/35.7/24.7/17.8 (BP=1.000, ratio=1.105, hyp_len=13515, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.11-3.05.0.93-2.54.1.40-4.04.1.10-3.00.pth, mybk
BLEU = 32.63, 60.5/38.3/26.2/18.6 (BP=1.000, ratio=1.066, hyp_len=12185, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.11-3.05.0.93-2.54.1.40-4.04.1.10-3.00.pth, bkmy
BLEU = 40.71, 66.4/47.0/34.3/25.7 (BP=1.000, ratio=1.046, hyp_len=12798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.332.0.31-1.37.0.26-1.29.2.28-9.74.1.85-6.37.pth, mybk
BLEU = 26.97, 52.8/31.8/21.1/14.9 (BP=1.000, ratio=1.102, hyp_len=12596, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.332.0.31-1.37.0.26-1.29.2.28-9.74.1.85-6.37.pth, bkmy
BLEU = 30.47, 55.3/35.5/24.5/17.9 (BP=1.000, ratio=1.100, hyp_len=13449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.333.0.28-1.32.0.24-1.27.2.34-10.37.1.84-6.29.pth, mybk
BLEU = 26.48, 52.1/31.1/20.7/14.6 (BP=1.000, ratio=1.089, hyp_len=12450, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.333.0.28-1.32.0.24-1.27.2.34-10.37.1.84-6.29.pth, bkmy
BLEU = 31.27, 55.6/36.1/25.4/18.8 (BP=1.000, ratio=1.084, hyp_len=13260, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.334.0.30-1.34.0.25-1.28.2.37-10.65.1.86-6.41.pth, mybk
BLEU = 26.50, 51.4/31.1/20.9/14.8 (BP=1.000, ratio=1.122, hyp_len=12821, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.334.0.30-1.34.0.25-1.28.2.37-10.65.1.86-6.41.pth, bkmy
BLEU = 30.91, 55.3/36.0/25.0/18.3 (BP=1.000, ratio=1.102, hyp_len=13484, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.335.0.28-1.32.0.23-1.25.2.34-10.42.1.76-5.84.pth, mybk
BLEU = 28.40, 54.2/33.4/22.4/16.0 (BP=1.000, ratio=1.080, hyp_len=12345, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.335.0.28-1.32.0.23-1.25.2.34-10.42.1.76-5.84.pth, bkmy
BLEU = 33.31, 58.0/38.6/27.3/20.2 (BP=1.000, ratio=1.091, hyp_len=13341, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.336.0.29-1.33.0.24-1.27.2.33-10.31.1.82-6.18.pth, mybk
BLEU = 28.27, 53.4/32.9/22.4/16.2 (BP=1.000, ratio=1.078, hyp_len=12324, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.336.0.29-1.33.0.24-1.27.2.33-10.31.1.82-6.18.pth, bkmy
BLEU = 30.66, 55.3/35.9/24.7/18.0 (BP=1.000, ratio=1.118, hyp_len=13669, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.337.0.32-1.38.0.27-1.31.2.30-10.01.1.83-6.26.pth, mybk
BLEU = 26.63, 52.3/31.4/20.8/14.7 (BP=1.000, ratio=1.101, hyp_len=12591, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.337.0.32-1.38.0.27-1.31.2.30-10.01.1.83-6.26.pth, bkmy
BLEU = 31.07, 55.9/36.3/25.1/18.3 (BP=1.000, ratio=1.104, hyp_len=13508, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.338.0.29-1.34.0.24-1.27.2.30-9.98.1.85-6.38.pth, mybk
BLEU = 26.35, 52.0/31.0/20.6/14.5 (BP=1.000, ratio=1.089, hyp_len=12446, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.338.0.29-1.34.0.24-1.27.2.30-9.98.1.85-6.38.pth, bkmy
BLEU = 30.93, 55.4/35.9/25.0/18.4 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.339.0.34-1.41.0.27-1.31.2.30-10.00.1.81-6.10.pth, mybk
BLEU = 27.87, 53.6/32.8/22.0/15.6 (BP=1.000, ratio=1.077, hyp_len=12317, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.339.0.34-1.41.0.27-1.31.2.30-10.00.1.81-6.10.pth, bkmy
BLEU = 30.66, 55.6/35.7/24.7/18.0 (BP=1.000, ratio=1.093, hyp_len=13367, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.340.0.28-1.33.0.24-1.27.2.31-10.03.1.79-6.00.pth, mybk
BLEU = 27.09, 52.9/31.9/21.3/15.0 (BP=1.000, ratio=1.082, hyp_len=12368, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.340.0.28-1.33.0.24-1.27.2.31-10.03.1.79-6.00.pth, bkmy
BLEU = 31.16, 55.9/36.2/25.3/18.4 (BP=1.000, ratio=1.098, hyp_len=13425, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.341.0.27-1.31.0.23-1.26.2.33-10.32.1.81-6.10.pth, mybk
BLEU = 28.07, 53.6/32.8/22.3/15.8 (BP=1.000, ratio=1.087, hyp_len=12432, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.341.0.27-1.31.0.23-1.26.2.33-10.32.1.81-6.10.pth, bkmy
BLEU = 29.60, 54.1/34.5/23.8/17.3 (BP=1.000, ratio=1.105, hyp_len=13512, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.19-3.30.0.99-2.68.1.42-4.14.1.11-3.05.pth, mybk
BLEU = 31.44, 58.7/37.0/25.1/17.9 (BP=1.000, ratio=1.090, hyp_len=12466, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.19-3.30.0.99-2.68.1.42-4.14.1.11-3.05.pth, bkmy
BLEU = 40.65, 66.6/47.1/34.2/25.5 (BP=1.000, ratio=1.043, hyp_len=12761, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.342.0.29-1.34.0.24-1.28.2.37-10.70.1.76-5.82.pth, mybk
BLEU = 26.46, 52.2/31.2/20.8/14.5 (BP=1.000, ratio=1.095, hyp_len=12516, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.342.0.29-1.34.0.24-1.28.2.37-10.70.1.76-5.82.pth, bkmy
BLEU = 32.01, 56.3/37.0/26.1/19.3 (BP=1.000, ratio=1.092, hyp_len=13361, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.343.0.29-1.34.0.24-1.27.2.33-10.23.1.73-5.63.pth, mybk
BLEU = 26.90, 52.8/31.8/21.2/14.7 (BP=1.000, ratio=1.082, hyp_len=12371, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.343.0.29-1.34.0.24-1.27.2.33-10.23.1.73-5.63.pth, bkmy
BLEU = 31.71, 56.0/36.6/25.9/19.1 (BP=1.000, ratio=1.091, hyp_len=13341, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.344.0.30-1.35.0.25-1.28.2.29-9.87.1.80-6.04.pth, mybk
BLEU = 27.54, 53.2/32.3/21.7/15.4 (BP=1.000, ratio=1.088, hyp_len=12433, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.344.0.30-1.35.0.25-1.28.2.29-9.87.1.80-6.04.pth, bkmy
BLEU = 30.71, 56.0/36.0/24.8/17.8 (BP=1.000, ratio=1.102, hyp_len=13478, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.345.0.31-1.36.0.25-1.28.2.26-9.63.1.72-5.58.pth, mybk
BLEU = 26.85, 53.0/31.9/21.0/14.7 (BP=1.000, ratio=1.097, hyp_len=12544, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.345.0.31-1.36.0.25-1.28.2.26-9.63.1.72-5.58.pth, bkmy
BLEU = 31.46, 55.7/36.4/25.7/18.8 (BP=1.000, ratio=1.086, hyp_len=13281, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.346.0.30-1.35.0.25-1.28.2.35-10.44.1.69-5.43.pth, mybk
BLEU = 27.01, 52.5/31.9/21.2/15.0 (BP=1.000, ratio=1.096, hyp_len=12525, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.346.0.30-1.35.0.25-1.28.2.35-10.44.1.69-5.43.pth, bkmy
BLEU = 32.48, 57.2/37.7/26.6/19.4 (BP=1.000, ratio=1.084, hyp_len=13263, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.347.0.30-1.34.0.24-1.28.2.31-10.04.1.73-5.64.pth, mybk
BLEU = 28.06, 54.4/33.0/22.1/15.6 (BP=1.000, ratio=1.083, hyp_len=12376, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.347.0.30-1.34.0.24-1.28.2.31-10.04.1.73-5.64.pth, bkmy
BLEU = 32.61, 57.1/37.6/26.6/19.8 (BP=1.000, ratio=1.083, hyp_len=13249, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.348.0.33-1.40.0.28-1.33.2.27-9.71.1.77-5.86.pth, mybk
BLEU = 27.92, 53.7/32.8/22.2/15.6 (BP=1.000, ratio=1.084, hyp_len=12392, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.348.0.33-1.40.0.28-1.33.2.27-9.71.1.77-5.86.pth, bkmy
BLEU = 32.11, 56.5/37.0/26.1/19.5 (BP=1.000, ratio=1.087, hyp_len=13296, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.349.0.29-1.34.0.24-1.27.2.26-9.58.1.80-6.03.pth, mybk
BLEU = 27.34, 53.3/32.3/21.5/15.1 (BP=1.000, ratio=1.077, hyp_len=12311, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.349.0.29-1.34.0.24-1.27.2.26-9.58.1.80-6.03.pth, bkmy
BLEU = 31.82, 56.6/37.2/26.0/18.8 (BP=1.000, ratio=1.100, hyp_len=13454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.350.0.30-1.35.0.25-1.29.2.29-9.85.1.80-6.06.pth, mybk
BLEU = 27.71, 53.9/32.7/21.8/15.3 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.350.0.30-1.35.0.25-1.29.2.29-9.85.1.80-6.06.pth, bkmy
BLEU = 29.65, 54.2/34.5/23.9/17.3 (BP=1.000, ratio=1.095, hyp_len=13392, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.351.0.27-1.31.0.23-1.26.2.24-9.43.1.82-6.19.pth, mybk
BLEU = 27.44, 53.2/32.1/21.6/15.4 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.351.0.27-1.31.0.23-1.26.2.24-9.43.1.82-6.19.pth, bkmy
BLEU = 30.21, 55.1/35.5/24.4/17.5 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.11-3.03.0.92-2.51.1.46-4.29.1.14-3.14.pth, mybk
BLEU = 31.77, 59.3/37.7/25.5/17.9 (BP=1.000, ratio=1.100, hyp_len=12576, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.11-3.03.0.92-2.51.1.46-4.29.1.14-3.14.pth, bkmy
BLEU = 36.80, 63.1/43.2/30.3/22.2 (BP=1.000, ratio=1.075, hyp_len=13147, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.352.0.28-1.32.0.24-1.27.2.31-10.11.1.74-5.71.pth, mybk
BLEU = 26.84, 52.9/31.8/21.0/14.7 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.352.0.28-1.32.0.24-1.27.2.31-10.11.1.74-5.71.pth, bkmy
BLEU = 31.37, 56.1/36.5/25.4/18.6 (BP=1.000, ratio=1.095, hyp_len=13390, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.353.0.32-1.38.0.26-1.30.2.32-10.15.1.76-5.78.pth, mybk
BLEU = 26.64, 52.8/31.7/20.9/14.4 (BP=1.000, ratio=1.083, hyp_len=12382, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.353.0.32-1.38.0.26-1.30.2.32-10.15.1.76-5.78.pth, bkmy
BLEU = 32.73, 57.6/37.8/26.8/19.6 (BP=1.000, ratio=1.090, hyp_len=13331, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.354.0.28-1.33.0.24-1.27.2.29-9.84.1.80-6.04.pth, mybk
BLEU = 27.26, 52.8/32.1/21.5/15.1 (BP=1.000, ratio=1.102, hyp_len=12593, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.354.0.28-1.33.0.24-1.27.2.29-9.84.1.80-6.04.pth, bkmy
BLEU = 31.85, 56.6/37.1/25.9/18.9 (BP=1.000, ratio=1.099, hyp_len=13437, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.355.0.30-1.35.0.24-1.27.2.30-9.97.1.84-6.29.pth, mybk
BLEU = 27.43, 53.2/32.3/21.6/15.3 (BP=1.000, ratio=1.084, hyp_len=12398, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.355.0.30-1.35.0.24-1.27.2.30-9.97.1.84-6.29.pth, bkmy
BLEU = 30.75, 55.3/35.9/24.9/18.1 (BP=1.000, ratio=1.102, hyp_len=13481, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.356.0.37-1.45.0.29-1.33.2.28-9.75.1.82-6.16.pth, mybk
BLEU = 28.22, 54.4/33.2/22.3/15.7 (BP=1.000, ratio=1.092, hyp_len=12483, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.356.0.37-1.45.0.29-1.33.2.28-9.75.1.82-6.16.pth, bkmy
BLEU = 31.89, 56.7/37.1/25.9/18.9 (BP=1.000, ratio=1.078, hyp_len=13186, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.357.0.27-1.32.0.23-1.25.2.30-9.98.1.84-6.33.pth, mybk
BLEU = 27.05, 52.5/31.7/21.4/15.0 (BP=1.000, ratio=1.085, hyp_len=12406, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.357.0.27-1.32.0.23-1.25.2.30-9.98.1.84-6.33.pth, bkmy
BLEU = 30.84, 56.0/36.3/25.0/17.8 (BP=1.000, ratio=1.098, hyp_len=13435, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.358.0.31-1.36.0.30-1.35.2.28-9.77.1.84-6.30.pth, mybk
BLEU = 27.47, 52.7/32.2/21.8/15.4 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.358.0.31-1.36.0.30-1.35.2.28-9.77.1.84-6.30.pth, bkmy
BLEU = 32.11, 56.4/37.2/26.3/19.3 (BP=1.000, ratio=1.081, hyp_len=13226, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.359.0.36-1.44.0.28-1.33.2.29-9.83.1.79-6.01.pth, mybk
BLEU = 27.82, 53.4/32.4/22.1/15.7 (BP=1.000, ratio=1.077, hyp_len=12313, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.359.0.36-1.44.0.28-1.33.2.29-9.83.1.79-6.01.pth, bkmy
BLEU = 31.29, 55.6/36.4/25.4/18.6 (BP=1.000, ratio=1.098, hyp_len=13428, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.360.0.33-1.39.0.27-1.30.2.31-10.06.1.82-6.17.pth, mybk
BLEU = 27.56, 53.8/32.4/21.7/15.2 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.360.0.33-1.39.0.27-1.30.2.31-10.06.1.82-6.17.pth, bkmy
BLEU = 29.58, 54.5/34.6/23.6/17.2 (BP=1.000, ratio=1.098, hyp_len=13428, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.361.0.28-1.33.0.24-1.26.2.34-10.40.1.75-5.73.pth, mybk
BLEU = 27.55, 53.1/32.4/21.8/15.4 (BP=1.000, ratio=1.075, hyp_len=12291, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.361.0.28-1.33.0.24-1.26.2.34-10.40.1.75-5.73.pth, bkmy
BLEU = 30.77, 55.6/35.8/24.8/18.1 (BP=1.000, ratio=1.096, hyp_len=13405, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.04-2.82.0.85-2.34.1.39-4.03.1.16-3.17.pth, mybk
BLEU = 33.23, 60.6/38.7/26.8/19.4 (BP=1.000, ratio=1.051, hyp_len=12013, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.04-2.82.0.85-2.34.1.39-4.03.1.16-3.17.pth, bkmy
BLEU = 38.68, 65.1/45.0/32.1/23.8 (BP=1.000, ratio=1.042, hyp_len=12743, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.362.0.30-1.35.0.24-1.27.2.36-10.58.1.77-5.86.pth, mybk
BLEU = 27.50, 53.2/32.3/21.8/15.3 (BP=1.000, ratio=1.096, hyp_len=12532, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.362.0.30-1.35.0.24-1.27.2.36-10.58.1.77-5.86.pth, bkmy
BLEU = 32.90, 57.2/37.9/26.9/20.1 (BP=1.000, ratio=1.078, hyp_len=13181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.363.0.30-1.35.0.25-1.29.2.34-10.40.1.83-6.21.pth, mybk
BLEU = 27.13, 52.9/31.8/21.3/15.1 (BP=1.000, ratio=1.079, hyp_len=12336, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.363.0.30-1.35.0.25-1.29.2.34-10.40.1.83-6.21.pth, bkmy
BLEU = 30.99, 56.3/36.3/25.0/18.1 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.364.0.33-1.39.0.27-1.31.2.37-10.69.1.85-6.34.pth, mybk
BLEU = 27.12, 52.9/32.0/21.4/14.9 (BP=1.000, ratio=1.070, hyp_len=12236, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.364.0.33-1.39.0.27-1.31.2.37-10.69.1.85-6.34.pth, bkmy
BLEU = 31.24, 56.0/36.5/25.4/18.3 (BP=1.000, ratio=1.096, hyp_len=13407, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.365.0.30-1.35.0.26-1.30.2.37-10.66.1.79-6.00.pth, mybk
BLEU = 27.16, 52.3/31.8/21.6/15.2 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.365.0.30-1.35.0.26-1.30.2.37-10.66.1.79-6.00.pth, bkmy
BLEU = 30.27, 54.9/35.4/24.5/17.6 (BP=1.000, ratio=1.099, hyp_len=13436, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.366.0.28-1.33.0.23-1.26.2.34-10.39.1.83-6.22.pth, mybk
BLEU = 28.83, 54.2/33.6/22.9/16.6 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.366.0.28-1.33.0.23-1.26.2.34-10.39.1.83-6.22.pth, bkmy
BLEU = 32.16, 56.4/37.1/26.2/19.5 (BP=1.000, ratio=1.084, hyp_len=13253, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.367.0.32-1.37.0.26-1.29.2.38-10.84.1.81-6.12.pth, mybk
BLEU = 27.87, 53.1/32.8/22.2/15.6 (BP=1.000, ratio=1.094, hyp_len=12505, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.367.0.32-1.37.0.26-1.29.2.38-10.84.1.81-6.12.pth, bkmy
BLEU = 30.94, 55.0/35.6/25.0/18.7 (BP=1.000, ratio=1.094, hyp_len=13378, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.368.0.29-1.34.0.25-1.28.2.36-10.55.1.81-6.12.pth, mybk
BLEU = 26.66, 52.0/31.2/21.0/14.8 (BP=1.000, ratio=1.085, hyp_len=12402, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.368.0.29-1.34.0.25-1.28.2.36-10.55.1.81-6.12.pth, bkmy
BLEU = 30.00, 54.7/35.0/24.1/17.5 (BP=1.000, ratio=1.113, hyp_len=13609, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.369.0.33-1.39.0.27-1.31.2.32-10.16.1.78-5.94.pth, mybk
BLEU = 28.20, 54.1/33.3/22.4/15.7 (BP=1.000, ratio=1.067, hyp_len=12197, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.369.0.33-1.39.0.27-1.31.2.32-10.16.1.78-5.94.pth, bkmy
BLEU = 30.38, 54.6/35.4/24.6/18.0 (BP=1.000, ratio=1.108, hyp_len=13556, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.370.0.32-1.38.0.27-1.31.2.28-9.76.1.78-5.94.pth, mybk
BLEU = 27.58, 53.4/32.5/21.8/15.3 (BP=1.000, ratio=1.094, hyp_len=12508, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.370.0.32-1.38.0.27-1.31.2.28-9.76.1.78-5.94.pth, bkmy
BLEU = 30.69, 55.5/35.9/24.9/17.9 (BP=1.000, ratio=1.111, hyp_len=13592, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.371.0.36-1.44.0.28-1.32.2.32-10.20.1.84-6.28.pth, mybk
BLEU = 27.29, 53.2/32.1/21.4/15.2 (BP=1.000, ratio=1.082, hyp_len=12368, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.371.0.36-1.44.0.28-1.32.2.32-10.20.1.84-6.28.pth, bkmy
BLEU = 30.37, 55.2/35.6/24.6/17.6 (BP=1.000, ratio=1.100, hyp_len=13456, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.05-2.85.0.87-2.40.1.42-4.13.1.15-3.17.pth, mybk
BLEU = 31.17, 59.0/36.9/24.8/17.5 (BP=1.000, ratio=1.087, hyp_len=12423, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.05-2.85.0.87-2.40.1.42-4.13.1.15-3.17.pth, bkmy
BLEU = 37.89, 64.3/44.5/31.4/22.9 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.372.0.27-1.31.0.23-1.26.2.34-10.38.1.81-6.09.pth, mybk
BLEU = 28.40, 54.5/33.2/22.5/16.0 (BP=1.000, ratio=1.082, hyp_len=12372, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.372.0.27-1.31.0.23-1.26.2.34-10.38.1.81-6.09.pth, bkmy
BLEU = 31.13, 55.8/36.3/25.3/18.3 (BP=1.000, ratio=1.102, hyp_len=13473, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.373.0.27-1.31.0.23-1.25.2.35-10.44.1.79-6.01.pth, mybk
BLEU = 27.97, 53.4/32.7/22.2/15.8 (BP=1.000, ratio=1.079, hyp_len=12339, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.373.0.27-1.31.0.23-1.25.2.35-10.44.1.79-6.01.pth, bkmy
BLEU = 30.48, 55.0/35.5/24.6/18.0 (BP=1.000, ratio=1.100, hyp_len=13452, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.374.0.28-1.32.0.24-1.26.2.37-10.65.1.75-5.73.pth, mybk
BLEU = 28.05, 54.3/33.1/22.2/15.5 (BP=1.000, ratio=1.078, hyp_len=12329, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.374.0.28-1.32.0.24-1.26.2.37-10.65.1.75-5.73.pth, bkmy
BLEU = 32.23, 56.9/37.2/26.3/19.4 (BP=1.000, ratio=1.088, hyp_len=13310, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.375.0.28-1.33.0.24-1.28.2.37-10.64.1.79-5.98.pth, mybk
BLEU = 26.72, 52.7/31.7/20.9/14.6 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.375.0.28-1.33.0.24-1.28.2.37-10.64.1.79-5.98.pth, bkmy
BLEU = 30.13, 54.5/35.1/24.4/17.7 (BP=1.000, ratio=1.120, hyp_len=13702, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.376.0.33-1.40.0.27-1.31.2.29-9.91.1.79-6.02.pth, mybk
BLEU = 26.66, 52.1/31.5/21.0/14.6 (BP=1.000, ratio=1.103, hyp_len=12607, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.376.0.33-1.40.0.27-1.31.2.29-9.91.1.79-6.02.pth, bkmy
BLEU = 31.75, 56.4/36.9/25.8/19.0 (BP=1.000, ratio=1.099, hyp_len=13440, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.377.0.27-1.31.0.23-1.26.2.33-10.32.1.75-5.76.pth, mybk
BLEU = 27.40, 53.6/32.5/21.6/15.0 (BP=1.000, ratio=1.087, hyp_len=12423, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.377.0.27-1.31.0.23-1.26.2.33-10.32.1.75-5.76.pth, bkmy
BLEU = 31.47, 56.2/36.5/25.5/18.7 (BP=1.000, ratio=1.081, hyp_len=13221, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.378.0.27-1.31.0.23-1.26.2.36-10.55.1.78-5.91.pth, mybk
BLEU = 27.12, 52.6/31.9/21.3/15.1 (BP=1.000, ratio=1.089, hyp_len=12449, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.378.0.27-1.31.0.23-1.26.2.36-10.55.1.78-5.91.pth, bkmy
BLEU = 31.72, 56.4/36.6/25.8/19.0 (BP=1.000, ratio=1.078, hyp_len=13188, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.379.0.30-1.35.0.26-1.29.2.38-10.82.1.78-5.93.pth, mybk
BLEU = 27.24, 53.2/32.0/21.4/15.1 (BP=1.000, ratio=1.080, hyp_len=12344, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.379.0.30-1.35.0.26-1.29.2.38-10.82.1.78-5.93.pth, bkmy
BLEU = 32.21, 56.5/37.5/26.3/19.3 (BP=1.000, ratio=1.083, hyp_len=13242, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.380.0.27-1.32.0.25-1.28.2.34-10.35.1.82-6.17.pth, mybk
BLEU = 27.67, 53.6/32.5/21.8/15.4 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.380.0.27-1.32.0.25-1.28.2.34-10.35.1.82-6.17.pth, bkmy
BLEU = 31.25, 55.7/36.2/25.4/18.6 (BP=1.000, ratio=1.084, hyp_len=13254, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.381.0.29-1.34.0.24-1.27.2.36-10.59.1.79-6.01.pth, mybk
BLEU = 26.23, 52.0/31.1/20.5/14.2 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.381.0.29-1.34.0.24-1.27.2.36-10.59.1.79-6.01.pth, bkmy
BLEU = 31.20, 56.0/36.4/25.4/18.3 (BP=1.000, ratio=1.098, hyp_len=13434, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.04-2.84.0.85-2.35.1.46-4.31.1.14-3.13.pth, mybk
BLEU = 30.83, 58.1/36.2/24.5/17.5 (BP=1.000, ratio=1.091, hyp_len=12471, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.04-2.84.0.85-2.35.1.46-4.31.1.14-3.13.pth, bkmy
BLEU = 39.10, 64.8/45.5/32.7/24.3 (BP=1.000, ratio=1.081, hyp_len=13223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.382.0.27-1.31.0.23-1.26.2.34-10.36.1.84-6.29.pth, mybk
BLEU = 27.12, 52.5/32.1/21.4/15.0 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.382.0.27-1.31.0.23-1.26.2.34-10.36.1.84-6.29.pth, bkmy
BLEU = 30.78, 55.5/35.8/24.8/18.2 (BP=1.000, ratio=1.095, hyp_len=13394, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.383.0.27-1.31.0.23-1.25.2.39-10.87.1.79-5.99.pth, mybk
BLEU = 27.50, 53.1/32.4/21.7/15.3 (BP=1.000, ratio=1.083, hyp_len=12381, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.383.0.27-1.31.0.23-1.25.2.39-10.87.1.79-5.99.pth, bkmy
BLEU = 30.31, 55.1/35.5/24.5/17.6 (BP=1.000, ratio=1.082, hyp_len=13235, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.384.0.28-1.32.0.24-1.26.2.37-10.75.1.82-6.16.pth, mybk
BLEU = 27.27, 53.2/32.3/21.5/15.0 (BP=1.000, ratio=1.082, hyp_len=12371, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.384.0.28-1.32.0.24-1.26.2.37-10.75.1.82-6.16.pth, bkmy
BLEU = 31.20, 55.7/36.2/25.4/18.5 (BP=1.000, ratio=1.083, hyp_len=13242, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.385.0.38-1.47.0.28-1.33.2.39-10.91.1.75-5.74.pth, mybk
BLEU = 27.25, 52.9/31.9/21.5/15.2 (BP=1.000, ratio=1.068, hyp_len=12212, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.385.0.38-1.47.0.28-1.33.2.39-10.91.1.75-5.74.pth, bkmy
BLEU = 31.53, 56.5/37.0/25.6/18.5 (BP=1.000, ratio=1.107, hyp_len=13543, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.386.0.31-1.36.0.27-1.31.2.36-10.58.1.81-6.14.pth, mybk
BLEU = 26.64, 52.3/31.4/20.9/14.7 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.386.0.31-1.36.0.27-1.31.2.36-10.58.1.81-6.14.pth, bkmy
BLEU = 30.89, 55.4/36.0/25.1/18.2 (BP=1.000, ratio=1.090, hyp_len=13331, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.387.0.28-1.32.0.24-1.27.2.37-10.68.1.83-6.21.pth, mybk
BLEU = 28.04, 53.4/33.1/22.2/15.8 (BP=1.000, ratio=1.081, hyp_len=12360, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.387.0.28-1.32.0.24-1.27.2.37-10.68.1.83-6.21.pth, bkmy
BLEU = 31.67, 56.3/36.8/25.8/18.8 (BP=1.000, ratio=1.091, hyp_len=13345, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.388.0.26-1.29.0.23-1.25.2.33-10.31.1.82-6.15.pth, mybk
BLEU = 27.96, 54.2/32.9/22.1/15.5 (BP=1.000, ratio=1.076, hyp_len=12302, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.388.0.26-1.29.0.23-1.25.2.33-10.31.1.82-6.15.pth, bkmy
BLEU = 32.51, 57.4/37.7/26.5/19.5 (BP=1.000, ratio=1.071, hyp_len=13103, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.389.0.28-1.33.0.24-1.27.2.35-10.44.1.83-6.21.pth, mybk
BLEU = 27.48, 52.6/32.2/21.7/15.5 (BP=1.000, ratio=1.084, hyp_len=12398, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.389.0.28-1.33.0.24-1.27.2.35-10.44.1.83-6.21.pth, bkmy
BLEU = 31.76, 56.7/37.1/25.7/18.8 (BP=1.000, ratio=1.085, hyp_len=13272, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.390.0.29-1.34.0.26-1.29.2.34-10.42.1.84-6.28.pth, mybk
BLEU = 27.79, 53.6/32.8/22.0/15.4 (BP=1.000, ratio=1.079, hyp_len=12338, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.390.0.29-1.34.0.26-1.29.2.34-10.42.1.84-6.28.pth, bkmy
BLEU = 31.21, 56.0/36.3/25.3/18.4 (BP=1.000, ratio=1.101, hyp_len=13467, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.72.0.83-2.30.1.45-4.26.1.16-3.18.pth, mybk
BLEU = 32.58, 60.3/38.2/26.2/18.7 (BP=1.000, ratio=1.054, hyp_len=12053, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.72.0.83-2.30.1.45-4.26.1.16-3.18.pth, bkmy
BLEU = 41.79, 67.9/47.9/35.0/26.9 (BP=0.999, ratio=0.999, hyp_len=12215, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.391.0.32-1.37.0.26-1.29.2.34-10.35.1.83-6.26.pth, mybk
BLEU = 28.02, 53.5/32.9/22.2/15.7 (BP=1.000, ratio=1.088, hyp_len=12441, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.391.0.32-1.37.0.26-1.29.2.34-10.35.1.83-6.26.pth, bkmy
BLEU = 30.85, 55.7/36.0/25.0/18.1 (BP=1.000, ratio=1.079, hyp_len=13196, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.392.0.26-1.30.0.23-1.26.2.37-10.67.1.87-6.50.pth, mybk
BLEU = 27.29, 53.2/32.4/21.6/14.9 (BP=1.000, ratio=1.086, hyp_len=12413, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.392.0.26-1.30.0.23-1.26.2.37-10.67.1.87-6.50.pth, bkmy
BLEU = 31.20, 55.5/36.3/25.3/18.5 (BP=1.000, ratio=1.097, hyp_len=13417, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.393.0.30-1.35.0.26-1.30.2.42-11.22.1.86-6.46.pth, mybk
BLEU = 27.29, 52.9/32.1/21.6/15.2 (BP=1.000, ratio=1.092, hyp_len=12483, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.393.0.30-1.35.0.26-1.30.2.42-11.22.1.86-6.46.pth, bkmy
BLEU = 29.42, 54.7/34.7/23.6/16.7 (BP=1.000, ratio=1.094, hyp_len=13378, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.394.0.26-1.30.0.22-1.25.2.42-11.25.1.82-6.19.pth, mybk
BLEU = 26.36, 52.1/31.0/20.8/14.4 (BP=1.000, ratio=1.109, hyp_len=12673, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.394.0.26-1.30.0.22-1.25.2.42-11.25.1.82-6.19.pth, bkmy
BLEU = 31.08, 55.8/36.1/25.3/18.2 (BP=1.000, ratio=1.088, hyp_len=13309, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.395.0.29-1.34.0.24-1.27.2.37-10.74.1.83-6.22.pth, mybk
BLEU = 25.46, 51.5/30.3/19.8/13.6 (BP=1.000, ratio=1.108, hyp_len=12669, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.395.0.29-1.34.0.24-1.27.2.37-10.74.1.83-6.22.pth, bkmy
BLEU = 30.90, 55.9/36.5/24.9/17.9 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.396.0.27-1.31.0.23-1.26.2.39-10.89.1.85-6.38.pth, mybk
BLEU = 28.91, 55.0/34.1/22.9/16.3 (BP=1.000, ratio=1.078, hyp_len=12329, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.396.0.27-1.31.0.23-1.26.2.39-10.89.1.85-6.38.pth, bkmy
BLEU = 30.62, 55.8/35.8/24.7/17.8 (BP=1.000, ratio=1.083, hyp_len=13247, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.397.0.29-1.34.0.25-1.28.2.38-10.82.1.82-6.19.pth, mybk
BLEU = 26.24, 51.2/31.0/20.7/14.5 (BP=1.000, ratio=1.115, hyp_len=12749, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.397.0.29-1.34.0.25-1.28.2.38-10.82.1.82-6.19.pth, bkmy
BLEU = 31.50, 55.7/36.6/25.7/18.8 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.398.0.31-1.36.0.25-1.29.2.39-10.93.1.84-6.29.pth, mybk
BLEU = 26.68, 52.5/31.6/21.0/14.5 (BP=1.000, ratio=1.088, hyp_len=12438, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.398.0.31-1.36.0.25-1.29.2.39-10.93.1.84-6.29.pth, bkmy
BLEU = 31.21, 56.1/36.6/25.4/18.2 (BP=1.000, ratio=1.083, hyp_len=13246, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.399.0.27-1.31.0.23-1.26.2.43-11.30.1.91-6.78.pth, mybk
BLEU = 27.02, 52.4/31.6/21.3/15.1 (BP=1.000, ratio=1.101, hyp_len=12589, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.399.0.27-1.31.0.23-1.26.2.43-11.30.1.91-6.78.pth, bkmy
BLEU = 31.26, 55.9/36.3/25.4/18.5 (BP=1.000, ratio=1.089, hyp_len=13325, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.400.0.31-1.37.0.28-1.32.2.40-11.05.1.89-6.61.pth, mybk
BLEU = 28.23, 54.3/33.1/22.2/15.9 (BP=1.000, ratio=1.073, hyp_len=12263, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.400.0.31-1.37.0.28-1.32.2.40-11.05.1.89-6.61.pth, bkmy
BLEU = 30.06, 55.1/35.4/24.2/17.3 (BP=1.000, ratio=1.101, hyp_len=13464, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.70.0.84-2.31.1.45-4.25.1.14-3.14.pth, mybk
BLEU = 31.61, 59.3/37.3/25.2/18.0 (BP=1.000, ratio=1.058, hyp_len=12092, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.70.0.84-2.31.1.45-4.25.1.14-3.14.pth, bkmy
BLEU = 38.93, 65.1/45.2/32.4/24.1 (BP=1.000, ratio=1.050, hyp_len=12841, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.401.0.27-1.31.0.22-1.25.2.37-10.75.1.83-6.22.pth, mybk
BLEU = 27.28, 52.3/31.9/21.5/15.4 (BP=1.000, ratio=1.088, hyp_len=12433, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.401.0.27-1.31.0.22-1.25.2.37-10.75.1.83-6.22.pth, bkmy
BLEU = 32.01, 56.4/37.1/26.1/19.2 (BP=1.000, ratio=1.099, hyp_len=13447, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.402.0.30-1.35.0.25-1.29.2.44-11.49.1.85-6.37.pth, mybk
BLEU = 27.54, 53.2/32.2/21.7/15.5 (BP=1.000, ratio=1.076, hyp_len=12303, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.402.0.30-1.35.0.25-1.29.2.44-11.49.1.85-6.37.pth, bkmy
BLEU = 30.81, 55.7/35.9/25.0/18.1 (BP=1.000, ratio=1.099, hyp_len=13438, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.403.0.33-1.40.0.31-1.36.2.39-10.93.1.78-5.95.pth, mybk
BLEU = 27.21, 53.0/32.1/21.5/15.0 (BP=1.000, ratio=1.095, hyp_len=12519, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.403.0.33-1.40.0.31-1.36.2.39-10.93.1.78-5.95.pth, bkmy
BLEU = 30.65, 54.9/35.7/24.9/18.1 (BP=1.000, ratio=1.118, hyp_len=13672, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.404.0.28-1.33.0.23-1.26.2.35-10.47.1.81-6.09.pth, mybk
BLEU = 27.38, 53.0/32.1/21.6/15.3 (BP=1.000, ratio=1.087, hyp_len=12426, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.404.0.28-1.33.0.23-1.26.2.35-10.47.1.81-6.09.pth, bkmy
BLEU = 32.58, 57.1/37.6/26.7/19.7 (BP=1.000, ratio=1.085, hyp_len=13265, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.405.0.27-1.31.0.22-1.25.2.42-11.19.1.75-5.77.pth, mybk
BLEU = 27.43, 53.0/32.1/21.5/15.5 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.405.0.27-1.31.0.22-1.25.2.42-11.19.1.75-5.77.pth, bkmy
BLEU = 32.74, 57.4/37.9/26.7/19.8 (BP=1.000, ratio=1.081, hyp_len=13225, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.406.0.30-1.35.0.26-1.29.2.37-10.66.1.81-6.10.pth, mybk
BLEU = 27.72, 53.1/32.4/21.8/15.7 (BP=1.000, ratio=1.079, hyp_len=12334, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.406.0.30-1.35.0.26-1.29.2.37-10.66.1.81-6.10.pth, bkmy
BLEU = 31.96, 56.4/37.0/26.0/19.3 (BP=1.000, ratio=1.100, hyp_len=13458, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.407.0.31-1.36.0.26-1.29.2.32-10.21.1.84-6.29.pth, mybk
BLEU = 27.81, 53.5/32.7/21.8/15.7 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.407.0.31-1.36.0.26-1.29.2.32-10.21.1.84-6.29.pth, bkmy
BLEU = 31.98, 56.6/37.3/26.0/19.1 (BP=1.000, ratio=1.087, hyp_len=13299, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.408.0.29-1.34.0.25-1.29.2.35-10.51.1.89-6.62.pth, mybk
BLEU = 28.25, 54.0/33.2/22.4/15.9 (BP=1.000, ratio=1.068, hyp_len=12213, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.408.0.29-1.34.0.25-1.29.2.35-10.51.1.89-6.62.pth, bkmy
BLEU = 30.15, 54.5/35.0/24.4/17.7 (BP=1.000, ratio=1.106, hyp_len=13529, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.409.0.28-1.32.0.23-1.26.2.38-10.76.1.86-6.44.pth, mybk
BLEU = 27.10, 53.4/32.2/21.3/14.8 (BP=1.000, ratio=1.098, hyp_len=12548, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.409.0.28-1.32.0.23-1.26.2.38-10.76.1.86-6.44.pth, bkmy
BLEU = 29.60, 54.3/34.7/23.8/17.1 (BP=1.000, ratio=1.109, hyp_len=13568, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.410.0.28-1.32.0.24-1.27.2.41-11.09.1.83-6.26.pth, mybk
BLEU = 26.38, 52.6/31.1/20.6/14.4 (BP=1.000, ratio=1.098, hyp_len=12555, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.410.0.28-1.32.0.24-1.27.2.41-11.09.1.83-6.26.pth, bkmy
BLEU = 30.54, 54.8/35.6/24.8/18.0 (BP=1.000, ratio=1.107, hyp_len=13535, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.0.93-2.53.0.78-2.17.1.41-4.10.1.17-3.21.pth, mybk
BLEU = 32.96, 60.5/38.6/26.5/19.1 (BP=1.000, ratio=1.068, hyp_len=12207, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.0.93-2.53.0.78-2.17.1.41-4.10.1.17-3.21.pth, bkmy
BLEU = 38.28, 64.1/44.5/31.8/23.7 (BP=1.000, ratio=1.076, hyp_len=13157, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.411.0.27-1.31.0.23-1.26.2.38-10.80.1.87-6.47.pth, mybk
BLEU = 26.83, 52.7/31.6/21.1/14.8 (BP=1.000, ratio=1.071, hyp_len=12249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.411.0.27-1.31.0.23-1.26.2.38-10.80.1.87-6.47.pth, bkmy
BLEU = 30.99, 55.7/36.0/25.1/18.3 (BP=1.000, ratio=1.102, hyp_len=13481, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.412.0.26-1.29.0.21-1.23.2.40-11.00.1.87-6.50.pth, mybk
BLEU = 26.74, 52.0/31.3/21.0/15.0 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.412.0.26-1.29.0.21-1.23.2.40-11.00.1.87-6.50.pth, bkmy
BLEU = 31.85, 56.7/37.3/25.9/18.8 (BP=1.000, ratio=1.095, hyp_len=13388, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.413.0.27-1.31.0.23-1.26.2.35-10.51.1.85-6.36.pth, mybk
BLEU = 27.39, 52.9/32.3/21.6/15.2 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.413.0.27-1.31.0.23-1.26.2.35-10.51.1.85-6.36.pth, bkmy
BLEU = 30.71, 55.8/36.0/24.8/17.9 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.414.0.27-1.31.0.21-1.24.2.36-10.55.1.81-6.14.pth, mybk
BLEU = 26.57, 52.5/31.5/20.8/14.5 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.414.0.27-1.31.0.21-1.24.2.36-10.55.1.81-6.14.pth, bkmy
BLEU = 30.32, 54.9/35.3/24.6/17.8 (BP=1.000, ratio=1.100, hyp_len=13458, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.415.0.25-1.29.0.21-1.23.2.35-10.44.1.81-6.13.pth, mybk
BLEU = 27.83, 53.7/32.9/22.0/15.5 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.415.0.25-1.29.0.21-1.23.2.35-10.44.1.81-6.13.pth, bkmy
BLEU = 30.88, 56.0/36.2/25.0/18.0 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.416.0.28-1.32.0.23-1.26.2.38-10.85.1.87-6.50.pth, mybk
BLEU = 27.93, 53.1/32.6/22.1/15.9 (BP=1.000, ratio=1.080, hyp_len=12351, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.416.0.28-1.32.0.23-1.26.2.38-10.85.1.87-6.50.pth, bkmy
BLEU = 31.62, 56.3/36.9/25.8/18.7 (BP=1.000, ratio=1.109, hyp_len=13567, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.417.0.26-1.30.0.22-1.24.2.33-10.27.1.81-6.13.pth, mybk
BLEU = 27.10, 52.9/31.9/21.2/15.0 (BP=1.000, ratio=1.080, hyp_len=12348, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.417.0.26-1.30.0.22-1.24.2.33-10.27.1.81-6.13.pth, bkmy
BLEU = 32.77, 57.0/38.0/26.9/19.8 (BP=1.000, ratio=1.108, hyp_len=13547, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.418.0.27-1.31.0.22-1.25.2.31-10.09.1.85-6.34.pth, mybk
BLEU = 26.87, 52.4/31.6/21.1/14.9 (BP=1.000, ratio=1.078, hyp_len=12328, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.418.0.27-1.31.0.22-1.25.2.31-10.09.1.85-6.34.pth, bkmy
BLEU = 31.45, 56.2/36.7/25.5/18.6 (BP=1.000, ratio=1.082, hyp_len=13234, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.419.0.34-1.40.0.28-1.32.2.33-10.26.1.83-6.24.pth, mybk
BLEU = 26.16, 52.3/31.1/20.4/14.1 (BP=1.000, ratio=1.075, hyp_len=12290, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.419.0.34-1.40.0.28-1.32.2.33-10.26.1.83-6.24.pth, bkmy
BLEU = 31.26, 56.1/36.3/25.4/18.5 (BP=1.000, ratio=1.090, hyp_len=13332, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.420.0.26-1.29.0.22-1.24.2.36-10.60.1.89-6.65.pth, mybk
BLEU = 27.65, 53.0/32.5/21.9/15.5 (BP=1.000, ratio=1.093, hyp_len=12499, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.420.0.26-1.29.0.22-1.24.2.36-10.60.1.89-6.65.pth, bkmy
BLEU = 30.88, 55.4/36.0/25.1/18.2 (BP=1.000, ratio=1.090, hyp_len=13334, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.59.0.80-2.22.1.49-4.45.1.20-3.33.pth, mybk
BLEU = 30.44, 57.3/35.6/24.3/17.3 (BP=1.000, ratio=1.093, hyp_len=12491, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.59.0.80-2.22.1.49-4.45.1.20-3.33.pth, bkmy
BLEU = 37.67, 63.7/43.9/31.1/23.1 (BP=1.000, ratio=1.073, hyp_len=13126, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.421.0.28-1.32.0.24-1.27.2.33-10.29.1.89-6.61.pth, mybk
BLEU = 27.19, 52.7/31.8/21.4/15.3 (BP=1.000, ratio=1.093, hyp_len=12495, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.421.0.28-1.32.0.24-1.27.2.33-10.29.1.89-6.61.pth, bkmy
BLEU = 30.33, 54.3/35.3/24.7/17.9 (BP=1.000, ratio=1.109, hyp_len=13564, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.422.0.28-1.32.0.24-1.27.2.32-10.16.1.87-6.52.pth, mybk
BLEU = 25.92, 51.9/30.9/20.2/13.9 (BP=1.000, ratio=1.102, hyp_len=12594, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.422.0.28-1.32.0.24-1.27.2.32-10.16.1.87-6.52.pth, bkmy
BLEU = 30.08, 54.7/35.2/24.4/17.5 (BP=1.000, ratio=1.102, hyp_len=13482, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.423.0.28-1.32.0.24-1.27.2.23-9.32.1.87-6.48.pth, mybk
BLEU = 27.55, 53.5/32.4/21.7/15.3 (BP=1.000, ratio=1.066, hyp_len=12190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.423.0.28-1.32.0.24-1.27.2.23-9.32.1.87-6.48.pth, bkmy
BLEU = 32.12, 56.9/37.6/26.3/18.9 (BP=1.000, ratio=1.104, hyp_len=13502, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.424.0.27-1.31.0.23-1.25.2.36-10.57.1.88-6.56.pth, mybk
BLEU = 27.30, 52.6/31.8/21.6/15.4 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.424.0.27-1.31.0.23-1.25.2.36-10.57.1.88-6.56.pth, bkmy
BLEU = 31.24, 55.6/36.4/25.4/18.5 (BP=1.000, ratio=1.100, hyp_len=13456, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.425.0.31-1.37.0.26-1.29.2.39-10.86.1.92-6.82.pth, mybk
BLEU = 26.86, 52.6/31.7/21.1/14.8 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.425.0.31-1.37.0.26-1.29.2.39-10.86.1.92-6.82.pth, bkmy
BLEU = 31.67, 56.0/36.7/25.9/18.9 (BP=1.000, ratio=1.091, hyp_len=13346, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.426.0.25-1.29.0.22-1.24.2.35-10.53.1.85-6.36.pth, mybk
BLEU = 26.73, 52.4/31.4/21.0/14.8 (BP=1.000, ratio=1.107, hyp_len=12655, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.426.0.25-1.29.0.22-1.24.2.35-10.53.1.85-6.36.pth, bkmy
BLEU = 30.43, 55.3/35.5/24.5/17.8 (BP=1.000, ratio=1.101, hyp_len=13464, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.427.0.27-1.32.0.23-1.26.2.30-9.95.1.90-6.69.pth, mybk
BLEU = 26.70, 51.9/31.3/21.0/14.9 (BP=1.000, ratio=1.095, hyp_len=12522, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.427.0.27-1.32.0.23-1.26.2.30-9.95.1.90-6.69.pth, bkmy
BLEU = 31.44, 56.0/36.5/25.5/18.8 (BP=1.000, ratio=1.096, hyp_len=13401, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.428.0.28-1.33.0.25-1.28.2.32-10.17.1.87-6.48.pth, mybk
BLEU = 26.73, 52.2/31.4/20.9/14.9 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.428.0.28-1.33.0.25-1.28.2.32-10.17.1.87-6.48.pth, bkmy
BLEU = 32.00, 57.1/37.3/26.0/18.9 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.429.0.27-1.31.0.23-1.25.2.29-9.85.1.91-6.76.pth, mybk
BLEU = 27.17, 53.2/32.1/21.3/15.0 (BP=1.000, ratio=1.097, hyp_len=12540, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.429.0.27-1.31.0.23-1.25.2.29-9.85.1.91-6.76.pth, bkmy
BLEU = 31.86, 56.9/37.3/26.0/18.7 (BP=1.000, ratio=1.085, hyp_len=13274, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.430.0.26-1.30.0.22-1.25.2.31-10.06.1.89-6.60.pth, mybk
BLEU = 27.09, 52.4/31.7/21.3/15.2 (BP=1.000, ratio=1.091, hyp_len=12473, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.430.0.26-1.30.0.22-1.25.2.31-10.06.1.89-6.60.pth, bkmy
BLEU = 32.79, 58.2/38.2/26.7/19.5 (BP=1.000, ratio=1.066, hyp_len=13037, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.93-2.52.0.77-2.16.1.46-4.31.1.21-3.34.pth, mybk
BLEU = 32.88, 60.3/38.5/26.4/19.1 (BP=1.000, ratio=1.053, hyp_len=12040, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.93-2.52.0.77-2.16.1.46-4.31.1.21-3.34.pth, bkmy
BLEU = 37.58, 63.2/43.8/31.3/23.1 (BP=1.000, ratio=1.093, hyp_len=13364, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.431.0.29-1.34.0.24-1.27.2.33-10.29.1.87-6.48.pth, mybk
BLEU = 26.94, 52.8/31.7/21.1/14.9 (BP=1.000, ratio=1.086, hyp_len=12414, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.431.0.29-1.34.0.24-1.27.2.33-10.29.1.87-6.48.pth, bkmy
BLEU = 31.51, 55.8/36.6/25.6/18.8 (BP=1.000, ratio=1.098, hyp_len=13432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.432.0.28-1.32.0.25-1.28.2.33-10.24.1.89-6.64.pth, mybk
BLEU = 27.67, 53.6/32.7/21.7/15.4 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.432.0.28-1.32.0.25-1.28.2.33-10.24.1.89-6.64.pth, bkmy
BLEU = 32.22, 56.6/37.4/26.3/19.4 (BP=1.000, ratio=1.090, hyp_len=13335, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.433.0.29-1.33.0.24-1.27.2.31-10.05.1.88-6.54.pth, mybk
BLEU = 27.98, 54.0/33.0/22.1/15.5 (BP=1.000, ratio=1.095, hyp_len=12517, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.433.0.29-1.33.0.24-1.27.2.31-10.05.1.88-6.54.pth, bkmy
BLEU = 32.53, 57.6/37.9/26.6/19.3 (BP=1.000, ratio=1.068, hyp_len=13067, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.434.0.34-1.40.0.29-1.34.2.36-10.54.1.86-6.42.pth, mybk
BLEU = 27.63, 53.7/32.5/21.7/15.4 (BP=1.000, ratio=1.087, hyp_len=12431, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.434.0.34-1.40.0.29-1.34.2.36-10.54.1.86-6.42.pth, bkmy
BLEU = 31.84, 56.7/37.2/25.9/18.8 (BP=1.000, ratio=1.089, hyp_len=13316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.435.0.33-1.39.0.25-1.29.2.36-10.64.1.85-6.34.pth, mybk
BLEU = 27.71, 53.5/32.4/21.8/15.6 (BP=1.000, ratio=1.076, hyp_len=12301, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.435.0.33-1.39.0.25-1.29.2.36-10.64.1.85-6.34.pth, bkmy
BLEU = 31.01, 55.9/36.1/25.2/18.3 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.436.0.26-1.30.0.22-1.25.2.27-9.73.1.85-6.38.pth, mybk
BLEU = 26.67, 52.4/31.4/20.8/14.7 (BP=1.000, ratio=1.086, hyp_len=12413, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.436.0.26-1.30.0.22-1.25.2.27-9.73.1.85-6.38.pth, bkmy
BLEU = 31.30, 55.9/36.3/25.4/18.6 (BP=1.000, ratio=1.104, hyp_len=13505, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.437.0.27-1.31.0.23-1.26.2.36-10.62.1.83-6.20.pth, mybk
BLEU = 27.00, 52.8/31.9/21.3/14.8 (BP=1.000, ratio=1.100, hyp_len=12577, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.437.0.27-1.31.0.23-1.26.2.36-10.62.1.83-6.20.pth, bkmy
BLEU = 31.46, 55.7/36.6/25.6/18.7 (BP=1.000, ratio=1.100, hyp_len=13458, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.438.0.27-1.32.0.22-1.25.2.33-10.24.1.82-6.19.pth, mybk
BLEU = 27.06, 53.1/32.0/21.3/14.8 (BP=1.000, ratio=1.078, hyp_len=12319, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.438.0.27-1.32.0.22-1.25.2.33-10.24.1.82-6.19.pth, bkmy
BLEU = 32.07, 56.6/37.2/26.1/19.2 (BP=1.000, ratio=1.095, hyp_len=13395, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.439.0.27-1.32.0.23-1.25.2.31-10.08.1.92-6.85.pth, mybk
BLEU = 26.57, 52.3/31.3/20.8/14.6 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.439.0.27-1.32.0.23-1.25.2.31-10.08.1.92-6.85.pth, bkmy
BLEU = 31.86, 56.5/37.0/26.0/19.0 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.440.0.28-1.33.0.24-1.27.2.24-9.42.1.89-6.60.pth, mybk
BLEU = 27.82, 53.9/32.5/22.0/15.5 (BP=1.000, ratio=1.095, hyp_len=12514, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.440.0.28-1.33.0.24-1.27.2.24-9.42.1.89-6.60.pth, bkmy
BLEU = 31.38, 56.0/36.5/25.5/18.6 (BP=1.000, ratio=1.084, hyp_len=13258, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.95-2.59.0.80-2.24.1.46-4.32.1.20-3.32.pth, mybk
BLEU = 31.72, 59.2/37.6/25.5/17.9 (BP=1.000, ratio=1.088, hyp_len=12439, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.95-2.59.0.80-2.24.1.46-4.32.1.20-3.32.pth, bkmy
BLEU = 39.36, 65.0/45.4/32.8/24.8 (BP=1.000, ratio=1.033, hyp_len=12639, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.441.0.26-1.30.0.23-1.26.2.32-10.15.1.88-6.55.pth, mybk
BLEU = 27.74, 53.2/32.4/22.0/15.7 (BP=1.000, ratio=1.076, hyp_len=12298, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.441.0.26-1.30.0.23-1.26.2.32-10.15.1.88-6.55.pth, bkmy
BLEU = 32.10, 56.9/37.4/26.1/19.1 (BP=1.000, ratio=1.094, hyp_len=13384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.442.0.27-1.31.0.23-1.26.2.31-10.10.1.87-6.47.pth, mybk
BLEU = 26.18, 51.3/30.6/20.5/14.6 (BP=1.000, ratio=1.104, hyp_len=12623, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.442.0.27-1.31.0.23-1.26.2.31-10.10.1.87-6.47.pth, bkmy
BLEU = 31.95, 56.3/37.0/26.1/19.2 (BP=1.000, ratio=1.089, hyp_len=13324, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.443.0.26-1.30.0.22-1.24.2.32-10.21.1.91-6.74.pth, mybk
BLEU = 27.22, 53.1/32.2/21.4/15.0 (BP=1.000, ratio=1.087, hyp_len=12422, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.443.0.26-1.30.0.22-1.24.2.32-10.21.1.91-6.74.pth, bkmy
BLEU = 31.52, 55.9/36.5/25.6/18.9 (BP=1.000, ratio=1.106, hyp_len=13522, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.444.0.30-1.35.0.24-1.28.2.32-10.13.1.84-6.29.pth, mybk
BLEU = 26.16, 52.1/31.0/20.4/14.2 (BP=1.000, ratio=1.095, hyp_len=12519, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.444.0.30-1.35.0.24-1.28.2.32-10.13.1.84-6.29.pth, bkmy
BLEU = 30.88, 55.7/36.0/25.0/18.1 (BP=1.000, ratio=1.095, hyp_len=13398, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.445.0.27-1.31.0.22-1.25.2.29-9.84.1.83-6.25.pth, mybk
BLEU = 26.86, 52.2/31.6/21.2/14.9 (BP=1.000, ratio=1.113, hyp_len=12723, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.445.0.27-1.31.0.22-1.25.2.29-9.84.1.83-6.25.pth, bkmy
BLEU = 31.71, 56.7/36.8/25.8/18.8 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.446.0.27-1.30.0.22-1.25.2.31-10.12.1.82-6.17.pth, mybk
BLEU = 27.25, 53.1/32.1/21.4/15.1 (BP=1.000, ratio=1.102, hyp_len=12595, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.446.0.27-1.30.0.22-1.25.2.31-10.12.1.82-6.17.pth, bkmy
BLEU = 32.32, 57.0/37.5/26.4/19.3 (BP=1.000, ratio=1.089, hyp_len=13316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.447.0.26-1.30.0.21-1.24.2.36-10.55.1.85-6.35.pth, mybk
BLEU = 26.82, 52.4/31.4/21.1/14.9 (BP=1.000, ratio=1.090, hyp_len=12466, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.447.0.26-1.30.0.21-1.24.2.36-10.55.1.85-6.35.pth, bkmy
BLEU = 31.36, 55.9/36.5/25.5/18.6 (BP=1.000, ratio=1.094, hyp_len=13378, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.448.0.27-1.31.0.22-1.25.2.36-10.57.1.87-6.51.pth, mybk
BLEU = 26.03, 51.8/30.7/20.3/14.2 (BP=1.000, ratio=1.086, hyp_len=12410, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.448.0.27-1.31.0.22-1.25.2.36-10.57.1.87-6.51.pth, bkmy
BLEU = 31.83, 56.6/36.9/25.8/19.0 (BP=1.000, ratio=1.064, hyp_len=13019, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.449.0.29-1.34.0.26-1.30.2.34-10.35.1.91-6.73.pth, mybk
BLEU = 27.77, 53.9/32.6/21.9/15.4 (BP=1.000, ratio=1.069, hyp_len=12219, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.449.0.29-1.34.0.26-1.30.2.34-10.35.1.91-6.73.pth, bkmy
BLEU = 30.25, 55.2/35.3/24.4/17.6 (BP=1.000, ratio=1.110, hyp_len=13580, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.450.0.29-1.34.0.25-1.29.2.34-10.43.1.88-6.55.pth, mybk
BLEU = 26.80, 52.7/31.9/21.0/14.6 (BP=1.000, ratio=1.109, hyp_len=12682, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.450.0.29-1.34.0.25-1.29.2.34-10.43.1.88-6.55.pth, bkmy
BLEU = 31.72, 57.0/36.9/25.6/18.8 (BP=1.000, ratio=1.078, hyp_len=13184, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.46.0.74-2.10.1.49-4.46.1.19-3.29.pth, mybk
BLEU = 32.31, 59.7/37.7/26.0/18.6 (BP=1.000, ratio=1.057, hyp_len=12078, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.46.0.74-2.10.1.49-4.46.1.19-3.29.pth, bkmy
BLEU = 38.20, 64.1/44.3/31.7/23.7 (BP=1.000, ratio=1.049, hyp_len=12828, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.451.0.29-1.34.0.25-1.28.2.31-10.08.1.89-6.60.pth, mybk
BLEU = 26.97, 52.9/32.1/21.2/14.7 (BP=1.000, ratio=1.097, hyp_len=12545, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.451.0.29-1.34.0.25-1.28.2.31-10.08.1.89-6.60.pth, bkmy
BLEU = 30.96, 56.1/36.2/25.1/18.1 (BP=1.000, ratio=1.082, hyp_len=13231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.452.0.27-1.31.0.23-1.26.2.35-10.52.1.90-6.67.pth, mybk
BLEU = 26.99, 52.7/32.0/21.2/14.8 (BP=1.000, ratio=1.094, hyp_len=12512, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.452.0.27-1.31.0.23-1.26.2.35-10.52.1.90-6.67.pth, bkmy
BLEU = 31.97, 57.3/37.4/26.0/18.8 (BP=1.000, ratio=1.089, hyp_len=13323, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.453.0.26-1.30.0.23-1.26.2.36-10.55.1.94-6.93.pth, mybk
BLEU = 27.44, 53.4/32.4/21.5/15.2 (BP=1.000, ratio=1.079, hyp_len=12336, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.453.0.26-1.30.0.23-1.26.2.36-10.55.1.94-6.93.pth, bkmy
BLEU = 31.26, 55.6/36.5/25.4/18.5 (BP=1.000, ratio=1.102, hyp_len=13479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.454.0.26-1.30.0.23-1.26.2.35-10.48.1.93-6.89.pth, mybk
BLEU = 27.01, 52.9/31.8/21.2/15.0 (BP=1.000, ratio=1.076, hyp_len=12304, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.454.0.26-1.30.0.23-1.26.2.35-10.48.1.93-6.89.pth, bkmy
BLEU = 31.26, 56.4/36.5/25.3/18.3 (BP=1.000, ratio=1.097, hyp_len=13418, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.455.0.29-1.34.0.24-1.27.2.36-10.62.1.89-6.63.pth, mybk
BLEU = 26.75, 53.2/31.8/20.9/14.5 (BP=1.000, ratio=1.068, hyp_len=12211, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.455.0.29-1.34.0.24-1.27.2.36-10.62.1.89-6.63.pth, bkmy
BLEU = 31.21, 56.0/36.5/25.3/18.3 (BP=1.000, ratio=1.098, hyp_len=13428, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.456.0.27-1.31.0.25-1.28.2.33-10.23.1.85-6.34.pth, mybk
BLEU = 26.66, 51.9/31.2/21.0/14.9 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.456.0.27-1.31.0.25-1.28.2.33-10.23.1.85-6.34.pth, bkmy
BLEU = 31.90, 57.2/37.3/25.9/18.7 (BP=1.000, ratio=1.095, hyp_len=13392, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.457.0.29-1.34.0.25-1.28.2.37-10.65.1.87-6.46.pth, mybk
BLEU = 27.61, 53.4/32.6/21.8/15.3 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.457.0.29-1.34.0.25-1.28.2.37-10.65.1.87-6.46.pth, bkmy
BLEU = 30.75, 55.6/36.0/24.9/17.9 (BP=1.000, ratio=1.088, hyp_len=13304, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.458.0.30-1.35.0.26-1.30.2.34-10.40.1.92-6.85.pth, mybk
BLEU = 26.27, 51.9/31.0/20.6/14.4 (BP=1.000, ratio=1.108, hyp_len=12672, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.458.0.30-1.35.0.26-1.30.2.34-10.40.1.92-6.85.pth, bkmy
BLEU = 31.88, 56.3/37.0/26.0/19.1 (BP=1.000, ratio=1.091, hyp_len=13348, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.459.0.29-1.34.0.26-1.30.2.31-10.06.1.91-6.76.pth, mybk
BLEU = 26.77, 52.4/31.7/21.1/14.7 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.459.0.29-1.34.0.26-1.30.2.31-10.06.1.91-6.76.pth, bkmy
BLEU = 31.32, 56.5/36.8/25.4/18.2 (BP=1.000, ratio=1.086, hyp_len=13287, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.460.0.27-1.30.0.22-1.24.2.38-10.78.1.87-6.46.pth, mybk
BLEU = 26.94, 52.7/31.9/21.2/14.8 (BP=1.000, ratio=1.101, hyp_len=12581, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.460.0.27-1.30.0.22-1.24.2.38-10.78.1.87-6.46.pth, bkmy
BLEU = 32.15, 57.2/37.6/26.2/19.0 (BP=1.000, ratio=1.091, hyp_len=13338, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.87-2.38.0.72-2.06.1.48-4.38.1.22-3.38.pth, mybk
BLEU = 32.68, 60.1/38.1/26.3/19.0 (BP=1.000, ratio=1.063, hyp_len=12154, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.87-2.38.0.72-2.06.1.48-4.38.1.22-3.38.pth, bkmy
BLEU = 37.66, 63.1/43.8/31.3/23.3 (BP=1.000, ratio=1.073, hyp_len=13118, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.461.0.31-1.36.0.25-1.29.2.32-10.14.1.89-6.64.pth, mybk
BLEU = 27.00, 53.1/32.0/21.1/14.8 (BP=1.000, ratio=1.086, hyp_len=12412, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.461.0.31-1.36.0.25-1.29.2.32-10.14.1.89-6.64.pth, bkmy
BLEU = 31.22, 56.6/36.4/25.3/18.2 (BP=1.000, ratio=1.077, hyp_len=13176, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.462.0.27-1.31.0.22-1.25.2.36-10.55.1.90-6.67.pth, mybk
BLEU = 27.04, 53.2/32.0/21.2/14.8 (BP=1.000, ratio=1.101, hyp_len=12581, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.462.0.27-1.31.0.22-1.25.2.36-10.55.1.90-6.67.pth, bkmy
BLEU = 30.90, 55.9/36.2/25.1/18.0 (BP=1.000, ratio=1.104, hyp_len=13505, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.463.0.28-1.32.0.24-1.27.2.33-10.27.1.93-6.87.pth, mybk
BLEU = 27.98, 54.0/33.1/22.1/15.5 (BP=1.000, ratio=1.088, hyp_len=12443, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.463.0.28-1.32.0.24-1.27.2.33-10.27.1.93-6.87.pth, bkmy
BLEU = 31.14, 56.4/36.5/25.2/18.2 (BP=1.000, ratio=1.085, hyp_len=13270, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.464.0.28-1.32.0.23-1.25.2.39-10.88.1.94-6.95.pth, mybk
BLEU = 26.01, 51.9/30.8/20.3/14.1 (BP=1.000, ratio=1.095, hyp_len=12514, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.464.0.28-1.32.0.23-1.25.2.39-10.88.1.94-6.95.pth, bkmy
BLEU = 31.69, 56.7/37.2/25.8/18.5 (BP=1.000, ratio=1.098, hyp_len=13426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.465.0.31-1.37.0.31-1.37.2.39-10.86.1.98-7.22.pth, mybk
BLEU = 27.88, 53.0/32.5/22.2/15.8 (BP=1.000, ratio=1.077, hyp_len=12315, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.465.0.31-1.37.0.31-1.37.2.39-10.86.1.98-7.22.pth, bkmy
BLEU = 30.06, 55.0/35.4/24.3/17.3 (BP=1.000, ratio=1.104, hyp_len=13508, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.466.0.27-1.31.0.24-1.27.2.40-10.99.1.91-6.77.pth, mybk
BLEU = 27.85, 53.2/32.6/22.2/15.7 (BP=1.000, ratio=1.084, hyp_len=12393, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.466.0.27-1.31.0.24-1.27.2.40-10.99.1.91-6.77.pth, bkmy
BLEU = 30.78, 56.1/36.0/24.8/17.9 (BP=1.000, ratio=1.087, hyp_len=13291, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.467.0.27-1.30.0.22-1.25.2.36-10.62.1.91-6.74.pth, mybk
BLEU = 27.27, 53.1/32.1/21.5/15.1 (BP=1.000, ratio=1.092, hyp_len=12485, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.467.0.27-1.30.0.22-1.25.2.36-10.62.1.91-6.74.pth, bkmy
BLEU = 31.73, 56.8/37.0/25.7/18.8 (BP=1.000, ratio=1.068, hyp_len=13068, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.468.0.28-1.32.0.25-1.28.2.38-10.79.1.91-6.76.pth, mybk
BLEU = 27.52, 53.3/32.1/21.6/15.5 (BP=1.000, ratio=1.075, hyp_len=12291, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.468.0.28-1.32.0.25-1.28.2.38-10.79.1.91-6.76.pth, bkmy
BLEU = 30.37, 55.2/35.4/24.4/17.8 (BP=1.000, ratio=1.081, hyp_len=13216, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.469.0.32-1.38.0.29-1.33.2.38-10.78.1.92-6.79.pth, mybk
BLEU = 27.45, 52.9/32.2/21.7/15.3 (BP=1.000, ratio=1.102, hyp_len=12603, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.469.0.32-1.38.0.29-1.33.2.38-10.78.1.92-6.79.pth, bkmy
BLEU = 31.14, 55.7/36.3/25.3/18.3 (BP=1.000, ratio=1.094, hyp_len=13385, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.470.0.26-1.29.0.22-1.24.2.36-10.57.1.87-6.49.pth, mybk
BLEU = 26.72, 52.7/31.8/21.0/14.5 (BP=1.000, ratio=1.098, hyp_len=12547, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.470.0.26-1.29.0.22-1.24.2.36-10.57.1.87-6.49.pth, bkmy
BLEU = 31.69, 56.5/37.0/25.8/18.7 (BP=1.000, ratio=1.105, hyp_len=13521, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.87-2.39.0.72-2.05.1.51-4.55.1.22-3.37.pth, mybk
BLEU = 31.32, 58.0/36.6/25.0/18.2 (BP=1.000, ratio=1.083, hyp_len=12385, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.87-2.39.0.72-2.05.1.51-4.55.1.22-3.37.pth, bkmy
BLEU = 38.70, 64.8/44.9/32.0/24.1 (BP=1.000, ratio=1.032, hyp_len=12626, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.471.0.35-1.41.0.28-1.33.2.37-10.67.1.92-6.84.pth, mybk
BLEU = 27.63, 52.8/32.4/21.8/15.6 (BP=1.000, ratio=1.092, hyp_len=12483, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.471.0.35-1.41.0.28-1.33.2.37-10.67.1.92-6.84.pth, bkmy
BLEU = 30.92, 55.8/36.2/25.1/18.0 (BP=1.000, ratio=1.116, hyp_len=13644, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.472.0.29-1.34.0.24-1.27.2.36-10.54.1.96-7.07.pth, mybk
BLEU = 27.94, 53.8/32.9/22.1/15.6 (BP=1.000, ratio=1.063, hyp_len=12157, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.472.0.29-1.34.0.24-1.27.2.36-10.54.1.96-7.07.pth, bkmy
BLEU = 31.91, 56.5/37.3/26.1/18.9 (BP=1.000, ratio=1.088, hyp_len=13304, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.473.0.29-1.33.0.24-1.27.2.37-10.70.1.90-6.68.pth, mybk
BLEU = 26.80, 52.6/31.8/21.1/14.6 (BP=1.000, ratio=1.094, hyp_len=12506, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.473.0.29-1.33.0.24-1.27.2.37-10.70.1.90-6.68.pth, bkmy
BLEU = 32.69, 57.4/38.2/26.8/19.4 (BP=1.000, ratio=1.095, hyp_len=13393, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.474.0.27-1.30.0.23-1.26.2.39-10.96.1.95-7.05.pth, mybk
BLEU = 27.64, 53.3/32.5/21.9/15.4 (BP=1.000, ratio=1.110, hyp_len=12690, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.474.0.27-1.30.0.23-1.26.2.39-10.96.1.95-7.05.pth, bkmy
BLEU = 30.25, 54.7/35.3/24.4/17.8 (BP=1.000, ratio=1.106, hyp_len=13531, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.475.0.26-1.30.0.22-1.24.2.38-10.83.1.95-7.06.pth, mybk
BLEU = 26.91, 52.5/31.9/21.2/14.8 (BP=1.000, ratio=1.098, hyp_len=12549, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.475.0.26-1.30.0.22-1.24.2.38-10.83.1.95-7.06.pth, bkmy
BLEU = 31.00, 55.3/36.0/25.2/18.4 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.476.0.24-1.27.0.21-1.23.2.29-9.84.1.91-6.76.pth, mybk
BLEU = 28.11, 54.4/33.2/22.1/15.6 (BP=1.000, ratio=1.073, hyp_len=12262, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.476.0.24-1.27.0.21-1.23.2.29-9.84.1.91-6.76.pth, bkmy
BLEU = 31.81, 56.9/37.2/25.8/18.8 (BP=1.000, ratio=1.094, hyp_len=13379, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.477.0.26-1.30.0.22-1.24.2.31-10.11.1.89-6.64.pth, mybk
BLEU = 27.78, 53.6/32.6/21.9/15.6 (BP=1.000, ratio=1.084, hyp_len=12393, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.477.0.26-1.30.0.22-1.24.2.31-10.11.1.89-6.64.pth, bkmy
BLEU = 32.96, 57.3/38.1/26.9/20.0 (BP=1.000, ratio=1.101, hyp_len=13472, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.478.0.26-1.29.0.22-1.25.2.28-9.81.1.88-6.57.pth, mybk
BLEU = 27.65, 53.6/32.8/21.7/15.3 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.478.0.26-1.29.0.22-1.25.2.28-9.81.1.88-6.57.pth, bkmy
BLEU = 33.30, 58.1/38.6/27.3/20.1 (BP=1.000, ratio=1.071, hyp_len=13099, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.479.0.28-1.33.0.24-1.28.2.34-10.41.1.86-6.45.pth, mybk
BLEU = 27.32, 53.0/32.3/21.5/15.2 (BP=1.000, ratio=1.086, hyp_len=12411, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.479.0.28-1.33.0.24-1.28.2.34-10.41.1.86-6.45.pth, bkmy
BLEU = 32.94, 58.1/38.3/27.0/19.6 (BP=1.000, ratio=1.087, hyp_len=13289, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.480.0.27-1.31.0.23-1.25.2.34-10.37.1.89-6.64.pth, mybk
BLEU = 26.92, 52.2/31.7/21.3/14.9 (BP=1.000, ratio=1.100, hyp_len=12579, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.480.0.27-1.31.0.23-1.25.2.34-10.37.1.89-6.64.pth, bkmy
BLEU = 31.69, 56.4/37.0/25.9/18.7 (BP=1.000, ratio=1.091, hyp_len=13348, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.83-2.30.0.70-2.01.1.49-4.45.1.20-3.34.pth, mybk
BLEU = 31.93, 58.7/37.3/25.6/18.5 (BP=1.000, ratio=1.078, hyp_len=12323, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.83-2.30.0.70-2.01.1.49-4.45.1.20-3.34.pth, bkmy
BLEU = 39.04, 64.6/45.4/32.7/24.3 (BP=1.000, ratio=1.079, hyp_len=13193, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.481.0.28-1.32.0.24-1.27.2.33-10.32.1.93-6.86.pth, mybk
BLEU = 27.90, 53.4/32.8/22.0/15.7 (BP=1.000, ratio=1.095, hyp_len=12517, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.481.0.28-1.32.0.24-1.27.2.33-10.32.1.93-6.86.pth, bkmy
BLEU = 31.08, 55.5/36.2/25.3/18.3 (BP=1.000, ratio=1.102, hyp_len=13480, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.482.0.26-1.30.0.22-1.25.2.29-9.89.1.92-6.84.pth, mybk
BLEU = 25.55, 51.6/30.6/19.8/13.6 (BP=1.000, ratio=1.103, hyp_len=12607, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.482.0.26-1.30.0.22-1.25.2.29-9.89.1.92-6.84.pth, bkmy
BLEU = 31.58, 56.4/36.9/25.7/18.6 (BP=1.000, ratio=1.094, hyp_len=13376, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.483.0.27-1.32.0.24-1.27.2.36-10.64.1.89-6.63.pth, mybk
BLEU = 27.31, 53.0/32.1/21.4/15.2 (BP=1.000, ratio=1.071, hyp_len=12239, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.483.0.27-1.32.0.24-1.27.2.36-10.64.1.89-6.63.pth, bkmy
BLEU = 31.33, 56.1/36.3/25.4/18.6 (BP=1.000, ratio=1.082, hyp_len=13233, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.484.0.25-1.29.0.22-1.25.2.33-10.25.1.90-6.71.pth, mybk
BLEU = 28.08, 53.8/32.9/22.2/15.9 (BP=1.000, ratio=1.090, hyp_len=12463, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.484.0.25-1.29.0.22-1.25.2.33-10.25.1.90-6.71.pth, bkmy
BLEU = 30.64, 55.1/35.5/24.9/18.1 (BP=1.000, ratio=1.097, hyp_len=13416, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.485.0.25-1.28.0.22-1.24.2.35-10.43.1.93-6.86.pth, mybk
BLEU = 28.01, 54.1/32.9/22.2/15.6 (BP=1.000, ratio=1.087, hyp_len=12422, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.485.0.25-1.28.0.22-1.24.2.35-10.43.1.93-6.86.pth, bkmy
BLEU = 30.23, 55.0/35.4/24.5/17.6 (BP=1.000, ratio=1.106, hyp_len=13530, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.486.0.27-1.31.0.23-1.25.2.32-10.22.1.90-6.65.pth, mybk
BLEU = 26.37, 52.2/31.4/20.6/14.3 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.486.0.27-1.31.0.23-1.25.2.32-10.22.1.90-6.65.pth, bkmy
BLEU = 30.17, 54.5/35.0/24.4/17.8 (BP=1.000, ratio=1.115, hyp_len=13634, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.487.0.25-1.29.0.21-1.24.2.38-10.77.1.88-6.57.pth, mybk
BLEU = 27.63, 53.5/32.5/21.8/15.4 (BP=1.000, ratio=1.083, hyp_len=12377, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.487.0.25-1.29.0.21-1.24.2.38-10.77.1.88-6.57.pth, bkmy
BLEU = 30.04, 55.0/35.3/24.2/17.3 (BP=1.000, ratio=1.107, hyp_len=13536, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.488.0.26-1.30.0.23-1.26.2.32-10.14.1.89-6.61.pth, mybk
BLEU = 26.77, 52.6/31.6/21.1/14.7 (BP=1.000, ratio=1.090, hyp_len=12465, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.488.0.26-1.30.0.23-1.26.2.32-10.14.1.89-6.61.pth, bkmy
BLEU = 31.10, 55.7/36.4/25.3/18.2 (BP=1.000, ratio=1.104, hyp_len=13501, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.489.0.26-1.29.0.22-1.25.2.30-10.00.1.88-6.56.pth, mybk
BLEU = 26.69, 52.7/31.5/20.9/14.6 (BP=1.000, ratio=1.092, hyp_len=12482, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.489.0.26-1.29.0.22-1.25.2.30-10.00.1.88-6.56.pth, bkmy
BLEU = 31.35, 56.7/36.8/25.4/18.3 (BP=1.000, ratio=1.084, hyp_len=13262, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.490.0.33-1.38.0.28-1.32.2.34-10.35.1.96-7.13.pth, mybk
BLEU = 26.94, 52.6/31.7/21.2/14.9 (BP=1.000, ratio=1.099, hyp_len=12562, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.490.0.33-1.38.0.28-1.32.2.34-10.35.1.96-7.13.pth, bkmy
BLEU = 30.66, 55.2/35.8/24.8/18.0 (BP=1.000, ratio=1.103, hyp_len=13494, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.84-2.32.0.70-2.01.1.50-4.50.1.23-3.43.pth, mybk
BLEU = 32.50, 60.0/38.1/26.1/18.7 (BP=1.000, ratio=1.051, hyp_len=12010, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.84-2.32.0.70-2.01.1.50-4.50.1.23-3.43.pth, bkmy
BLEU = 37.97, 63.8/44.1/31.4/23.5 (BP=1.000, ratio=1.059, hyp_len=12950, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.491.0.25-1.28.0.23-1.26.2.30-9.93.1.95-7.05.pth, mybk
BLEU = 28.01, 53.7/32.8/22.1/15.8 (BP=1.000, ratio=1.085, hyp_len=12408, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.491.0.25-1.28.0.23-1.26.2.30-9.93.1.95-7.05.pth, bkmy
BLEU = 30.54, 55.0/35.5/24.7/18.0 (BP=1.000, ratio=1.095, hyp_len=13394, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.492.0.26-1.29.0.23-1.25.2.34-10.36.1.93-6.90.pth, mybk
BLEU = 28.42, 54.2/33.1/22.5/16.2 (BP=1.000, ratio=1.074, hyp_len=12279, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.492.0.26-1.29.0.23-1.25.2.34-10.36.1.93-6.90.pth, bkmy
BLEU = 31.59, 56.4/36.8/25.7/18.6 (BP=1.000, ratio=1.101, hyp_len=13464, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.493.0.29-1.33.0.24-1.27.2.38-10.85.1.94-6.98.pth, mybk
BLEU = 27.42, 53.5/32.2/21.5/15.3 (BP=1.000, ratio=1.067, hyp_len=12193, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.493.0.29-1.33.0.24-1.27.2.38-10.85.1.94-6.98.pth, bkmy
BLEU = 31.79, 56.5/37.0/25.9/18.9 (BP=1.000, ratio=1.096, hyp_len=13402, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.494.0.26-1.29.0.22-1.25.2.33-10.28.1.97-7.16.pth, mybk
BLEU = 26.18, 52.4/31.0/20.3/14.2 (BP=1.000, ratio=1.088, hyp_len=12443, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.494.0.26-1.29.0.22-1.25.2.33-10.28.1.97-7.16.pth, bkmy
BLEU = 32.86, 57.3/37.9/26.9/20.0 (BP=1.000, ratio=1.072, hyp_len=13110, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.495.0.27-1.32.0.22-1.24.2.35-10.54.1.99-7.35.pth, mybk
BLEU = 26.86, 52.4/31.6/21.1/14.9 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.495.0.27-1.32.0.22-1.24.2.35-10.54.1.99-7.35.pth, bkmy
BLEU = 31.79, 56.2/36.9/26.0/19.0 (BP=1.000, ratio=1.098, hyp_len=13429, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.496.0.29-1.33.0.24-1.27.2.39-10.87.1.89-6.61.pth, mybk
BLEU = 27.15, 52.9/32.1/21.3/15.0 (BP=1.000, ratio=1.085, hyp_len=12404, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.496.0.29-1.33.0.24-1.27.2.39-10.87.1.89-6.61.pth, bkmy
BLEU = 31.64, 56.1/36.7/25.6/19.0 (BP=1.000, ratio=1.094, hyp_len=13384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.497.0.29-1.33.0.24-1.27.2.35-10.49.1.88-6.57.pth, mybk
BLEU = 27.81, 53.2/32.6/22.0/15.7 (BP=1.000, ratio=1.083, hyp_len=12376, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.497.0.29-1.33.0.24-1.27.2.35-10.49.1.88-6.57.pth, bkmy
BLEU = 30.88, 55.5/36.0/25.2/18.1 (BP=1.000, ratio=1.105, hyp_len=13517, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.498.0.30-1.35.0.25-1.28.2.38-10.77.1.88-6.57.pth, mybk
BLEU = 28.49, 54.8/33.5/22.4/16.0 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.498.0.30-1.35.0.25-1.28.2.38-10.77.1.88-6.57.pth, bkmy
BLEU = 32.45, 57.2/37.7/26.5/19.4 (BP=1.000, ratio=1.100, hyp_len=13456, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.499.0.24-1.27.0.21-1.24.2.35-10.54.1.90-6.69.pth, mybk
BLEU = 27.56, 53.2/32.5/21.7/15.4 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.499.0.24-1.27.0.21-1.24.2.35-10.54.1.90-6.69.pth, bkmy
BLEU = 31.61, 56.1/36.7/25.7/18.8 (BP=1.000, ratio=1.084, hyp_len=13254, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.500.0.29-1.33.0.25-1.28.2.33-10.23.1.89-6.65.pth, mybk
BLEU = 27.25, 52.7/31.9/21.4/15.3 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.500.0.29-1.33.0.25-1.28.2.33-10.23.1.89-6.65.pth, bkmy
BLEU = 31.53, 56.4/36.9/25.6/18.5 (BP=1.000, ratio=1.088, hyp_len=13307, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.85-2.34.0.70-2.01.1.50-4.48.1.22-3.40.pth, mybk
BLEU = 31.94, 59.2/37.5/25.6/18.3 (BP=1.000, ratio=1.073, hyp_len=12271, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.85-2.34.0.70-2.01.1.50-4.48.1.22-3.40.pth, bkmy
BLEU = 38.27, 64.5/44.6/31.8/23.4 (BP=1.000, ratio=1.041, hyp_len=12727, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.82-2.27.0.67-1.96.1.53-4.64.1.24-3.46.pth, mybk
BLEU = 30.25, 56.8/35.6/24.2/17.1 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.82-2.27.0.67-1.96.1.53-4.64.1.24-3.46.pth, bkmy
BLEU = 36.96, 63.1/43.3/30.7/22.3 (BP=1.000, ratio=1.076, hyp_len=13163, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.84-2.31.0.72-2.05.1.56-4.78.1.24-3.44.pth, mybk
BLEU = 30.69, 57.1/35.9/24.5/17.7 (BP=1.000, ratio=1.103, hyp_len=12606, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.84-2.31.0.72-2.05.1.56-4.78.1.24-3.44.pth, bkmy
BLEU = 36.60, 62.1/42.4/30.3/22.6 (BP=1.000, ratio=1.070, hyp_len=13086, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.82-2.27.0.67-1.95.1.57-4.80.1.23-3.44.pth, mybk
BLEU = 29.69, 56.1/35.0/23.7/16.7 (BP=1.000, ratio=1.105, hyp_len=12638, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.82-2.27.0.67-1.95.1.57-4.80.1.23-3.44.pth, bkmy
BLEU = 36.10, 61.9/42.4/29.8/21.7 (BP=1.000, ratio=1.075, hyp_len=13151, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.81-2.25.0.66-1.94.1.55-4.73.1.24-3.45.pth, mybk
BLEU = 30.17, 56.8/35.7/24.1/17.0 (BP=1.000, ratio=1.098, hyp_len=12557, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.81-2.25.0.66-1.94.1.55-4.73.1.24-3.45.pth, bkmy
BLEU = 35.71, 61.8/41.7/29.3/21.6 (BP=1.000, ratio=1.065, hyp_len=13021, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.82-2.28.0.68-1.98.1.61-4.99.1.23-3.44.pth, mybk
BLEU = 29.73, 56.5/35.0/23.7/16.7 (BP=1.000, ratio=1.099, hyp_len=12569, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.82-2.28.0.68-1.98.1.61-4.99.1.23-3.44.pth, bkmy
BLEU = 37.61, 63.4/43.7/31.2/23.2 (BP=1.000, ratio=1.066, hyp_len=13035, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.19.0.65-1.91.1.59-4.92.1.26-3.52.pth, mybk
BLEU = 31.12, 58.2/36.6/24.8/17.7 (BP=1.000, ratio=1.086, hyp_len=12410, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.19.0.65-1.91.1.59-4.92.1.26-3.52.pth, bkmy
BLEU = 35.37, 61.3/41.4/29.0/21.2 (BP=1.000, ratio=1.075, hyp_len=13146, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.76-2.15.0.62-1.85.1.60-4.98.1.27-3.58.pth, mybk
BLEU = 32.08, 59.3/37.7/25.8/18.4 (BP=1.000, ratio=1.070, hyp_len=12227, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.76-2.15.0.62-1.85.1.60-4.98.1.27-3.58.pth, bkmy
BLEU = 36.12, 62.1/42.1/29.6/22.0 (BP=1.000, ratio=1.080, hyp_len=13210, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.79-2.20.0.65-1.91.1.58-4.87.1.29-3.64.pth, mybk
BLEU = 32.01, 59.2/37.5/25.6/18.4 (BP=1.000, ratio=1.063, hyp_len=12151, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.79-2.20.0.65-1.91.1.58-4.87.1.29-3.64.pth, bkmy
BLEU = 37.31, 62.9/43.2/31.0/23.0 (BP=1.000, ratio=1.047, hyp_len=12801, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.73-2.08.0.61-1.84.1.66-5.24.1.30-3.67.pth, mybk
BLEU = 31.06, 57.6/36.4/24.9/17.8 (BP=1.000, ratio=1.082, hyp_len=12373, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.73-2.08.0.61-1.84.1.66-5.24.1.30-3.67.pth, bkmy
BLEU = 35.53, 61.2/41.4/29.2/21.5 (BP=1.000, ratio=1.061, hyp_len=12977, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.79-2.20.0.65-1.92.1.64-5.14.1.35-3.84.pth, mybk
BLEU = 30.68, 57.3/36.0/24.5/17.5 (BP=1.000, ratio=1.096, hyp_len=12533, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.79-2.20.0.65-1.92.1.64-5.14.1.35-3.84.pth, bkmy
BLEU = 35.86, 61.3/41.5/29.5/22.0 (BP=1.000, ratio=1.064, hyp_len=13014, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.0.75-2.11.0.62-1.86.1.68-5.34.1.30-3.66.pth, mybk
BLEU = 30.87, 57.9/36.4/24.6/17.5 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.0.75-2.11.0.62-1.86.1.68-5.34.1.30-3.66.pth, bkmy
BLEU = 34.44, 60.6/40.4/28.0/20.5 (BP=1.000, ratio=1.075, hyp_len=13152, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.0.76-2.14.0.63-1.88.1.68-5.36.1.34-3.84.pth, mybk
BLEU = 29.92, 57.5/35.6/23.8/16.4 (BP=1.000, ratio=1.098, hyp_len=12556, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.0.76-2.14.0.63-1.88.1.68-5.36.1.34-3.84.pth, bkmy
BLEU = 35.02, 61.4/41.2/28.7/20.7 (BP=1.000, ratio=1.070, hyp_len=13090, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.0.74-2.10.0.60-1.82.1.69-5.44.1.33-3.78.pth, mybk
BLEU = 31.36, 58.2/36.6/25.1/18.1 (BP=1.000, ratio=1.065, hyp_len=12178, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.0.74-2.10.0.60-1.82.1.69-5.44.1.33-3.78.pth, bkmy
BLEU = 35.58, 61.1/41.5/29.2/21.6 (BP=1.000, ratio=1.081, hyp_len=13223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.0.69-1.98.0.58-1.79.1.68-5.36.1.27-3.58.pth, mybk
BLEU = 30.69, 57.7/36.0/24.5/17.4 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.0.69-1.98.0.58-1.79.1.68-5.36.1.27-3.58.pth, bkmy
BLEU = 36.78, 62.2/42.6/30.4/22.6 (BP=1.000, ratio=1.064, hyp_len=13010, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.04.0.59-1.81.1.69-5.40.1.28-3.60.pth, mybk
BLEU = 30.45, 57.7/35.8/24.2/17.2 (BP=1.000, ratio=1.074, hyp_len=12280, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.04.0.59-1.81.1.69-5.40.1.28-3.60.pth, bkmy
BLEU = 37.01, 62.4/43.0/30.7/22.8 (BP=1.000, ratio=1.068, hyp_len=13057, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.0.73-2.07.0.64-1.89.1.67-5.30.1.34-3.80.pth, mybk
BLEU = 29.91, 56.3/35.2/23.8/17.0 (BP=1.000, ratio=1.110, hyp_len=12685, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.0.73-2.07.0.64-1.89.1.67-5.30.1.34-3.80.pth, bkmy
BLEU = 35.53, 61.1/41.3/29.3/21.6 (BP=1.000, ratio=1.074, hyp_len=13138, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.0.73-2.08.0.59-1.81.1.71-5.52.1.32-3.73.pth, mybk
BLEU = 31.75, 58.3/37.0/25.6/18.4 (BP=1.000, ratio=1.055, hyp_len=12061, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.0.73-2.08.0.59-1.81.1.71-5.52.1.32-3.73.pth, bkmy
BLEU = 34.77, 60.5/40.8/28.5/20.8 (BP=1.000, ratio=1.095, hyp_len=13387, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.0.69-2.00.0.56-1.76.1.66-5.27.1.32-3.73.pth, mybk
BLEU = 30.20, 57.1/35.5/23.9/17.2 (BP=1.000, ratio=1.101, hyp_len=12582, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.0.69-2.00.0.56-1.76.1.66-5.27.1.32-3.73.pth, bkmy
BLEU = 34.70, 60.7/40.7/28.4/20.6 (BP=1.000, ratio=1.080, hyp_len=13209, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.98.0.59-1.80.1.68-5.38.1.33-3.77.pth, mybk
BLEU = 31.06, 57.4/36.1/24.9/18.0 (BP=1.000, ratio=1.082, hyp_len=12373, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.98.0.59-1.80.1.68-5.38.1.33-3.77.pth, bkmy
BLEU = 35.18, 61.1/41.0/28.8/21.3 (BP=1.000, ratio=1.069, hyp_len=13075, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.0.66-1.94.0.53-1.70.1.69-5.41.1.33-3.79.pth, mybk
BLEU = 29.10, 55.2/34.1/23.1/16.5 (BP=1.000, ratio=1.100, hyp_len=12577, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.0.66-1.94.0.53-1.70.1.69-5.41.1.33-3.79.pth, bkmy
BLEU = 35.98, 61.4/41.5/29.7/22.1 (BP=1.000, ratio=1.062, hyp_len=12994, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.0.70-2.01.0.56-1.76.1.73-5.63.1.37-3.92.pth, mybk
BLEU = 30.68, 57.4/36.1/24.5/17.4 (BP=1.000, ratio=1.077, hyp_len=12314, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.0.70-2.01.0.56-1.76.1.73-5.63.1.37-3.92.pth, bkmy
BLEU = 35.39, 61.2/41.2/29.1/21.4 (BP=1.000, ratio=1.062, hyp_len=12994, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.0.63-1.88.0.53-1.69.1.69-5.42.1.34-3.83.pth, mybk
BLEU = 30.18, 57.6/35.7/23.9/16.8 (BP=1.000, ratio=1.092, hyp_len=12488, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.0.63-1.88.0.53-1.69.1.69-5.42.1.34-3.83.pth, bkmy
BLEU = 34.69, 60.3/40.3/28.4/21.0 (BP=1.000, ratio=1.082, hyp_len=13230, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.0.70-2.01.0.58-1.78.1.74-5.69.1.34-3.83.pth, mybk
BLEU = 29.09, 55.1/34.1/23.2/16.4 (BP=1.000, ratio=1.112, hyp_len=12714, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.0.70-2.01.0.58-1.78.1.74-5.69.1.34-3.83.pth, bkmy
BLEU = 35.83, 61.3/41.6/29.6/21.9 (BP=1.000, ratio=1.048, hyp_len=12819, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.0.66-1.94.0.53-1.70.1.75-5.75.1.34-3.83.pth, mybk
BLEU = 29.31, 55.4/34.5/23.4/16.5 (BP=1.000, ratio=1.090, hyp_len=12457, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.0.66-1.94.0.53-1.70.1.75-5.75.1.34-3.83.pth, bkmy
BLEU = 33.65, 58.8/39.1/27.5/20.3 (BP=1.000, ratio=1.082, hyp_len=13239, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.0.62-1.85.0.51-1.66.1.74-5.72.1.34-3.83.pth, mybk
BLEU = 29.61, 56.9/35.1/23.4/16.4 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.0.62-1.85.0.51-1.66.1.74-5.72.1.34-3.83.pth, bkmy
BLEU = 36.18, 62.2/42.1/29.8/22.0 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.0.63-1.87.0.51-1.67.1.71-5.51.1.39-4.02.pth, mybk
BLEU = 29.77, 56.6/35.1/23.6/16.8 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.0.63-1.87.0.51-1.67.1.71-5.51.1.39-4.02.pth, bkmy
BLEU = 37.29, 62.8/43.1/30.9/23.1 (BP=1.000, ratio=1.033, hyp_len=12632, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.0.64-1.89.0.51-1.67.1.68-5.35.1.36-3.89.pth, mybk
BLEU = 29.56, 57.0/34.8/23.3/16.5 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.0.64-1.89.0.51-1.67.1.68-5.35.1.36-3.89.pth, bkmy
BLEU = 35.72, 61.2/41.6/29.6/21.6 (BP=1.000, ratio=1.074, hyp_len=13137, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.0.66-1.93.0.51-1.67.1.74-5.70.1.37-3.93.pth, mybk
BLEU = 29.53, 56.0/34.8/23.5/16.6 (BP=1.000, ratio=1.090, hyp_len=12457, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.0.66-1.93.0.51-1.67.1.74-5.70.1.37-3.93.pth, bkmy
BLEU = 34.88, 60.4/40.4/28.6/21.2 (BP=1.000, ratio=1.065, hyp_len=13028, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.0.61-1.84.0.50-1.65.1.74-5.68.1.39-4.01.pth, mybk
BLEU = 31.65, 58.7/37.0/25.4/18.2 (BP=1.000, ratio=1.046, hyp_len=11963, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.0.61-1.84.0.50-1.65.1.74-5.68.1.39-4.01.pth, bkmy
BLEU = 33.57, 58.7/38.9/27.5/20.2 (BP=1.000, ratio=1.085, hyp_len=13267, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.0.61-1.85.0.50-1.65.1.77-5.88.1.38-3.98.pth, mybk
BLEU = 29.62, 56.2/34.6/23.4/16.9 (BP=1.000, ratio=1.077, hyp_len=12314, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.0.61-1.85.0.50-1.65.1.77-5.88.1.38-3.98.pth, bkmy
BLEU = 36.50, 62.0/42.2/30.2/22.5 (BP=1.000, ratio=1.055, hyp_len=12903, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.0.60-1.82.0.50-1.64.1.81-6.13.1.41-4.09.pth, mybk
BLEU = 29.86, 56.5/34.9/23.6/17.1 (BP=1.000, ratio=1.078, hyp_len=12319, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.0.60-1.82.0.50-1.64.1.81-6.13.1.41-4.09.pth, bkmy
BLEU = 35.59, 61.4/41.3/29.2/21.7 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.0.60-1.82.0.49-1.63.1.80-6.08.1.40-4.04.pth, mybk
BLEU = 29.65, 56.0/34.8/23.6/16.9 (BP=1.000, ratio=1.083, hyp_len=12386, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.0.60-1.82.0.49-1.63.1.80-6.08.1.40-4.04.pth, bkmy
BLEU = 33.90, 59.8/39.7/27.7/20.1 (BP=1.000, ratio=1.082, hyp_len=13231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.0.61-1.84.0.50-1.65.1.82-6.16.1.43-4.17.pth, mybk
BLEU = 30.26, 56.4/35.3/24.1/17.5 (BP=1.000, ratio=1.070, hyp_len=12232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.0.61-1.84.0.50-1.65.1.82-6.16.1.43-4.17.pth, bkmy
BLEU = 34.27, 59.3/39.6/28.1/20.9 (BP=1.000, ratio=1.070, hyp_len=13082, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.0.60-1.83.0.48-1.62.1.77-5.88.1.40-4.06.pth, mybk
BLEU = 29.71, 56.4/34.8/23.5/16.9 (BP=1.000, ratio=1.087, hyp_len=12432, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.0.60-1.83.0.48-1.62.1.77-5.88.1.40-4.06.pth, bkmy
BLEU = 34.01, 59.3/39.6/27.9/20.4 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.0.59-1.80.0.48-1.62.1.77-5.89.1.40-4.07.pth, mybk
BLEU = 28.86, 55.8/34.0/22.7/16.1 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.0.59-1.80.0.48-1.62.1.77-5.89.1.40-4.07.pth, bkmy
BLEU = 34.67, 60.5/40.4/28.4/20.9 (BP=1.000, ratio=1.073, hyp_len=13124, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.0.59-1.80.0.48-1.61.1.83-6.25.1.43-4.17.pth, mybk
BLEU = 28.15, 54.4/33.2/22.2/15.7 (BP=1.000, ratio=1.096, hyp_len=12526, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.0.59-1.80.0.48-1.61.1.83-6.25.1.43-4.17.pth, bkmy
BLEU = 34.85, 59.8/40.2/28.5/21.5 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.0.60-1.82.0.51-1.66.1.86-6.40.1.45-4.27.pth, mybk
BLEU = 29.95, 56.3/34.9/23.9/17.1 (BP=1.000, ratio=1.059, hyp_len=12110, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.0.60-1.82.0.51-1.66.1.86-6.40.1.45-4.27.pth, bkmy
BLEU = 32.39, 57.7/37.8/26.3/19.2 (BP=1.000, ratio=1.076, hyp_len=13159, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.0.62-1.87.0.49-1.63.1.85-6.37.1.42-4.16.pth, mybk
BLEU = 28.63, 55.0/33.8/22.6/16.0 (BP=1.000, ratio=1.094, hyp_len=12507, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.0.62-1.87.0.49-1.63.1.85-6.37.1.42-4.16.pth, bkmy
BLEU = 33.54, 58.3/39.0/27.5/20.2 (BP=1.000, ratio=1.076, hyp_len=13156, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.0.56-1.75.0.45-1.57.1.86-6.40.1.41-4.09.pth, mybk
BLEU = 29.69, 56.5/34.8/23.5/16.8 (BP=1.000, ratio=1.076, hyp_len=12296, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.0.56-1.75.0.45-1.57.1.86-6.40.1.41-4.09.pth, bkmy
BLEU = 34.41, 59.3/39.6/28.3/21.1 (BP=1.000, ratio=1.065, hyp_len=13024, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.0.57-1.76.0.46-1.58.1.82-6.19.1.43-4.18.pth, mybk
BLEU = 28.55, 54.8/33.7/22.7/15.8 (BP=1.000, ratio=1.100, hyp_len=12575, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.0.57-1.76.0.46-1.58.1.82-6.19.1.43-4.18.pth, bkmy
BLEU = 33.59, 58.9/38.9/27.3/20.4 (BP=1.000, ratio=1.077, hyp_len=13175, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.91.0.57-1.77.0.46-1.59.1.84-6.29.1.43-4.20.pth, mybk
BLEU = 29.16, 55.8/34.2/23.1/16.4 (BP=1.000, ratio=1.057, hyp_len=12085, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.91.0.57-1.77.0.46-1.59.1.84-6.29.1.43-4.20.pth, bkmy
BLEU = 34.61, 59.5/40.0/28.4/21.2 (BP=1.000, ratio=1.073, hyp_len=13124, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.92.0.56-1.74.0.45-1.57.1.90-6.66.1.45-4.28.pth, mybk
BLEU = 28.86, 55.2/33.9/22.8/16.2 (BP=1.000, ratio=1.083, hyp_len=12379, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.92.0.56-1.74.0.45-1.57.1.90-6.66.1.45-4.28.pth, bkmy
BLEU = 33.17, 58.8/38.9/26.9/19.7 (BP=1.000, ratio=1.067, hyp_len=13056, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.93.0.59-1.80.0.44-1.56.1.84-6.27.1.42-4.15.pth, mybk
BLEU = 27.52, 53.5/32.4/21.7/15.3 (BP=1.000, ratio=1.108, hyp_len=12669, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.93.0.59-1.80.0.44-1.56.1.84-6.27.1.42-4.15.pth, bkmy
BLEU = 34.54, 60.1/40.4/28.3/20.7 (BP=1.000, ratio=1.066, hyp_len=13038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.94.0.56-1.75.0.44-1.56.1.86-6.45.1.51-4.51.pth, mybk
BLEU = 29.83, 55.9/34.7/23.9/17.1 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.94.0.56-1.75.0.44-1.56.1.86-6.45.1.51-4.51.pth, bkmy
BLEU = 32.88, 57.6/38.0/26.8/19.9 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.95.0.54-1.72.0.44-1.55.1.87-6.51.1.44-4.20.pth, mybk
BLEU = 28.87, 55.0/34.0/23.0/16.2 (BP=1.000, ratio=1.090, hyp_len=12462, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.95.0.54-1.72.0.44-1.55.1.87-6.51.1.44-4.20.pth, bkmy
BLEU = 33.99, 59.5/39.4/27.8/20.5 (BP=1.000, ratio=1.070, hyp_len=13085, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.96.0.55-1.74.0.43-1.53.1.85-6.37.1.46-4.29.pth, mybk
BLEU = 29.76, 56.4/34.8/23.6/17.0 (BP=1.000, ratio=1.079, hyp_len=12337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.96.0.55-1.74.0.43-1.53.1.85-6.37.1.46-4.29.pth, bkmy
BLEU = 34.06, 59.3/39.6/27.9/20.5 (BP=1.000, ratio=1.075, hyp_len=13143, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.97.0.55-1.72.0.47-1.61.1.89-6.62.1.42-4.14.pth, mybk
BLEU = 30.03, 55.8/34.8/24.0/17.4 (BP=1.000, ratio=1.065, hyp_len=12170, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.97.0.55-1.72.0.47-1.61.1.89-6.62.1.42-4.14.pth, bkmy
BLEU = 33.74, 59.0/39.2/27.5/20.4 (BP=1.000, ratio=1.071, hyp_len=13097, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.98.0.52-1.68.0.42-1.53.1.90-6.70.1.44-4.22.pth, mybk
BLEU = 29.80, 55.8/35.0/23.8/16.9 (BP=1.000, ratio=1.072, hyp_len=12256, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.98.0.52-1.68.0.42-1.53.1.90-6.70.1.44-4.22.pth, bkmy
BLEU = 33.37, 58.6/38.9/27.2/20.0 (BP=1.000, ratio=1.098, hyp_len=13432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.99.0.54-1.71.0.46-1.58.1.95-7.01.1.44-4.22.pth, mybk
BLEU = 28.16, 54.3/32.9/22.2/15.9 (BP=1.000, ratio=1.078, hyp_len=12319, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.99.0.54-1.71.0.46-1.58.1.95-7.01.1.44-4.22.pth, bkmy
BLEU = 32.32, 57.4/37.6/26.3/19.2 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
==========

real	272m43.771s
user	262m58.779s
sys	20m29.511s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-bk အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
bk-my အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   


## Seq2Seq-DSL Training for 500 Epochs (my-rk, rk-my)

```

```

testing/evaluation ...  

```

```

my-rk အတွက် Seq2Seq-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
rk-my အတွက် Seq2Seq-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   

## Transformer-DSL Training for 500 Epochs (my-rk, rk-my)

```

```

testing/evaluation ...  

```

```

my-rk အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
rk-my အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   


