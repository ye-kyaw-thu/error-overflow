# Additional DSL Experiment No. 1

ရှေ့မှာ လုပ်ခဲ့တဲ့ Epoch-100 experiment မှာ Seq2Seq-DSL ရဲ့ ရလဒ်က Transformer-DSL နဲ့ ရလဒ်နဲ့ အများကြီးကွာနေတာကို တွေ့ရတယ်။ အဲဒါကြောင့် epoch ကို ၅၀၀ ထိ တိုးကြည့်ရင်ကော Seq2Seq-DSL နဲ့ Transformer-DSL ရဲ့အကြားမှာ ဘယ်လိုနေမလဲ ဆိုတာကို သိရအောင်လို့ additional experiment အနေနဲ့ ထပ် run ခဲ့တယ်။ ဒီ markdown ဖိုင်က အဲဒီ run ခဲ့တဲ့ log ဖိုင်ဖြစ်တယ်။  

## Seq2Seq-DSL Training for 500 Epochs

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

```

my-bk အတွက် Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
bk-my အတွက် Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   

## Transformer-DSL Training for 500 Epochs

```

```

## Testing/Evaluation for Seq2Seq-DSL 500 Models 

```

```

my-bk အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။  
bk-my အတွက် Transformer-DSL Best model က epoch model ဖြစ်ပြီးတော့ Best Score က  BLEU ပါ။   





