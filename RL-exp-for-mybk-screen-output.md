# Some Screen Outputs of RL-exp-for-mybk

seq2seq baseline training ကို my-bk အတွက်ရော bk-my အတွက်ရော လုပ်စဉ်က screen output ကို ဖိုင်နာမည် "rl-seq2seq-baseline-training-for-mybk-bkmy.log" ပေးပြီးသိမ်းထားခဲ့တယ်။ rl-seq2seq-baseline-training-for-mybk-bkmy.log တစ်ခုလုံးက အောက်ပါအတိုင်း...  

```
mybk, seq2seq-baseline training start for 30 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/mybk-30epoch/seq-model-mybk.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1313, 128)
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
Epoch 1 - |param|=6.01e+02 |g_param|=3.32e+05 loss=4.9263e+00 ppl=137.87
Validation - loss=4.0864e+00 ppl=59.52 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.01e+02 |g_param|=3.77e+05 loss=4.4177e+00 ppl=82.91
Validation - loss=3.9483e+00 ppl=51.84 best_loss=4.0864e+00 best_ppl=59.52
Epoch 3 - |param|=6.01e+02 |g_param|=3.40e+05 loss=4.3770e+00 ppl=79.60
Validation - loss=3.8406e+00 ppl=46.55 best_loss=3.9483e+00 best_ppl=51.84
Epoch 4 - |param|=6.01e+02 |g_param|=2.62e+05 loss=4.3506e+00 ppl=77.52
Validation - loss=3.8642e+00 ppl=47.67 best_loss=3.8406e+00 best_ppl=46.55
Epoch 5 - |param|=6.01e+02 |g_param|=1.80e+05 loss=4.3643e+00 ppl=78.59
Validation - loss=3.8854e+00 ppl=48.69 best_loss=3.8406e+00 best_ppl=46.55
Epoch 6 - |param|=6.01e+02 |g_param|=1.87e+05 loss=4.2594e+00 ppl=70.77
Validation - loss=3.8080e+00 ppl=45.06 best_loss=3.8406e+00 best_ppl=46.55
Epoch 7 - |param|=6.01e+02 |g_param|=1.82e+05 loss=4.3559e+00 ppl=77.94
Validation - loss=3.8058e+00 ppl=44.96 best_loss=3.8080e+00 best_ppl=45.06
Epoch 8 - |param|=6.02e+02 |g_param|=1.93e+05 loss=4.2730e+00 ppl=71.74
Validation - loss=3.7649e+00 ppl=43.16 best_loss=3.8058e+00 best_ppl=44.96
Epoch 9 - |param|=6.02e+02 |g_param|=1.82e+05 loss=4.2371e+00 ppl=69.21
Validation - loss=3.7457e+00 ppl=42.34 best_loss=3.7649e+00 best_ppl=43.16
Epoch 10 - |param|=6.03e+02 |g_param|=2.00e+05 loss=4.1920e+00 ppl=66.16
Validation - loss=3.6743e+00 ppl=39.42 best_loss=3.7457e+00 best_ppl=42.34
Epoch 11 - |param|=6.03e+02 |g_param|=1.60e+05 loss=4.0483e+00 ppl=57.30
Validation - loss=3.4416e+00 ppl=31.24 best_loss=3.6743e+00 best_ppl=39.42
Epoch 12 - |param|=6.03e+02 |g_param|=1.54e+05 loss=3.8880e+00 ppl=48.81
Validation - loss=3.4232e+00 ppl=30.67 best_loss=3.4416e+00 best_ppl=31.24
Epoch 13 - |param|=6.04e+02 |g_param|=1.25e+05 loss=3.7603e+00 ppl=42.96
Validation - loss=3.3025e+00 ppl=27.18 best_loss=3.4232e+00 best_ppl=30.67
Epoch 14 - |param|=6.04e+02 |g_param|=1.38e+05 loss=3.6858e+00 ppl=39.88
Validation - loss=3.2476e+00 ppl=25.73 best_loss=3.3025e+00 best_ppl=27.18
Epoch 15 - |param|=6.05e+02 |g_param|=1.31e+05 loss=3.6330e+00 ppl=37.82
Validation - loss=3.1371e+00 ppl=23.04 best_loss=3.2476e+00 best_ppl=25.73
Epoch 16 - |param|=6.05e+02 |g_param|=1.39e+05 loss=3.6069e+00 ppl=36.85
Validation - loss=3.1109e+00 ppl=22.44 best_loss=3.1371e+00 best_ppl=23.04
Epoch 17 - |param|=6.06e+02 |g_param|=1.35e+05 loss=3.5559e+00 ppl=35.02
Validation - loss=3.0241e+00 ppl=20.57 best_loss=3.1109e+00 best_ppl=22.44
Epoch 18 - |param|=6.06e+02 |g_param|=1.28e+05 loss=3.3347e+00 ppl=28.07
Validation - loss=2.9254e+00 ppl=18.64 best_loss=3.0241e+00 best_ppl=20.57
Epoch 19 - |param|=6.07e+02 |g_param|=1.31e+05 loss=3.2886e+00 ppl=26.81
Validation - loss=2.8823e+00 ppl=17.86 best_loss=2.9254e+00 best_ppl=18.64
Epoch 20 - |param|=6.07e+02 |g_param|=1.42e+05 loss=3.2952e+00 ppl=26.98
Validation - loss=2.7986e+00 ppl=16.42 best_loss=2.8823e+00 best_ppl=17.86
Epoch 21 - |param|=6.08e+02 |g_param|=1.42e+05 loss=3.2145e+00 ppl=24.89
Validation - loss=2.7825e+00 ppl=16.16 best_loss=2.7986e+00 best_ppl=16.42
Epoch 22 - |param|=6.09e+02 |g_param|=1.51e+05 loss=3.1577e+00 ppl=23.52
Validation - loss=2.6882e+00 ppl=14.70 best_loss=2.7825e+00 best_ppl=16.16
Epoch 23 - |param|=6.09e+02 |g_param|=1.49e+05 loss=3.0840e+00 ppl=21.84
Validation - loss=2.6568e+00 ppl=14.25 best_loss=2.6882e+00 best_ppl=14.70
Epoch 24 - |param|=6.10e+02 |g_param|=1.58e+05 loss=3.0726e+00 ppl=21.60
Validation - loss=2.6104e+00 ppl=13.60 best_loss=2.6568e+00 best_ppl=14.25
Epoch 25 - |param|=6.10e+02 |g_param|=1.61e+05 loss=2.9941e+00 ppl=19.97
Validation - loss=2.5879e+00 ppl=13.30 best_loss=2.6104e+00 best_ppl=13.60
Epoch 26 - |param|=6.11e+02 |g_param|=1.74e+05 loss=2.9987e+00 ppl=20.06
Validation - loss=2.5528e+00 ppl=12.84 best_loss=2.5879e+00 best_ppl=13.30
Epoch 27 - |param|=6.11e+02 |g_param|=1.64e+05 loss=2.9000e+00 ppl=18.17
Validation - loss=2.5051e+00 ppl=12.24 best_loss=2.5528e+00 best_ppl=12.84
Epoch 28 - |param|=6.12e+02 |g_param|=1.73e+05 loss=2.8729e+00 ppl=17.69
Validation - loss=2.4463e+00 ppl=11.55 best_loss=2.5051e+00 best_ppl=12.24
Epoch 29 - |param|=6.12e+02 |g_param|=1.69e+05 loss=2.8103e+00 ppl=16.61
Validation - loss=2.4282e+00 ppl=11.34 best_loss=2.4463e+00 best_ppl=11.55
Epoch 30 - |param|=6.13e+02 |g_param|=1.95e+05 loss=2.8045e+00 ppl=16.52
Validation - loss=2.3833e+00 ppl=10.84 best_loss=2.4282e+00 best_ppl=11.34
mybk, seq2seq-baseline training start for 40 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/mybk-40epoch/seq-model-mybk.pth',
    'n_epochs': 40,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1313, 128)
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
Epoch 1 - |param|=5.99e+02 |g_param|=3.92e+05 loss=4.8868e+00 ppl=132.53
Validation - loss=4.0239e+00 ppl=55.92 best_loss=inf best_ppl=inf
Epoch 2 - |param|=5.99e+02 |g_param|=4.26e+05 loss=4.4127e+00 ppl=82.49
Validation - loss=3.8747e+00 ppl=48.17 best_loss=4.0239e+00 best_ppl=55.92
Epoch 3 - |param|=5.99e+02 |g_param|=2.28e+05 loss=4.4547e+00 ppl=86.03
Validation - loss=3.8499e+00 ppl=46.99 best_loss=3.8747e+00 best_ppl=48.17
Epoch 4 - |param|=5.99e+02 |g_param|=1.78e+05 loss=4.3263e+00 ppl=75.66
Validation - loss=3.8203e+00 ppl=45.62 best_loss=3.8499e+00 best_ppl=46.99
Epoch 5 - |param|=5.99e+02 |g_param|=2.07e+05 loss=4.3432e+00 ppl=76.95
Validation - loss=3.8216e+00 ppl=45.68 best_loss=3.8203e+00 best_ppl=45.62
Epoch 6 - |param|=5.99e+02 |g_param|=2.09e+05 loss=4.3085e+00 ppl=74.33
Validation - loss=3.8289e+00 ppl=46.01 best_loss=3.8203e+00 best_ppl=45.62
Epoch 7 - |param|=6.00e+02 |g_param|=1.83e+05 loss=4.2764e+00 ppl=71.98
Validation - loss=3.8159e+00 ppl=45.42 best_loss=3.8203e+00 best_ppl=45.62
Epoch 8 - |param|=6.00e+02 |g_param|=1.98e+05 loss=4.2742e+00 ppl=71.82
Validation - loss=3.7483e+00 ppl=42.45 best_loss=3.8159e+00 best_ppl=45.42
Epoch 9 - |param|=6.00e+02 |g_param|=1.78e+05 loss=4.2228e+00 ppl=68.22
Validation - loss=3.7249e+00 ppl=41.47 best_loss=3.7483e+00 best_ppl=42.45
Epoch 10 - |param|=6.01e+02 |g_param|=1.87e+05 loss=4.2461e+00 ppl=69.83
Validation - loss=3.7005e+00 ppl=40.47 best_loss=3.7249e+00 best_ppl=41.47
Epoch 11 - |param|=6.01e+02 |g_param|=1.79e+05 loss=4.2156e+00 ppl=67.73
Validation - loss=3.6715e+00 ppl=39.31 best_loss=3.7005e+00 best_ppl=40.47
Epoch 12 - |param|=6.02e+02 |g_param|=1.94e+05 loss=4.0898e+00 ppl=59.73
Validation - loss=3.6230e+00 ppl=37.45 best_loss=3.6715e+00 best_ppl=39.31
Epoch 13 - |param|=6.02e+02 |g_param|=1.54e+05 loss=3.9911e+00 ppl=54.11
Validation - loss=3.3996e+00 ppl=29.95 best_loss=3.6230e+00 best_ppl=37.45
Epoch 14 - |param|=6.03e+02 |g_param|=1.37e+05 loss=3.8096e+00 ppl=45.13
Validation - loss=3.2630e+00 ppl=26.13 best_loss=3.3996e+00 best_ppl=29.95
Epoch 15 - |param|=6.03e+02 |g_param|=1.38e+05 loss=3.6656e+00 ppl=39.08
Validation - loss=3.1895e+00 ppl=24.28 best_loss=3.2630e+00 best_ppl=26.13
Epoch 16 - |param|=6.04e+02 |g_param|=1.33e+05 loss=3.5959e+00 ppl=36.45
Validation - loss=3.1117e+00 ppl=22.46 best_loss=3.1895e+00 best_ppl=24.28
Epoch 17 - |param|=6.04e+02 |g_param|=1.26e+05 loss=3.4723e+00 ppl=32.21
Validation - loss=3.0265e+00 ppl=20.63 best_loss=3.1117e+00 best_ppl=22.46
Epoch 18 - |param|=6.05e+02 |g_param|=1.30e+05 loss=3.4388e+00 ppl=31.15
Validation - loss=2.9793e+00 ppl=19.67 best_loss=3.0265e+00 best_ppl=20.63
Epoch 19 - |param|=6.05e+02 |g_param|=1.38e+05 loss=3.3749e+00 ppl=29.22
Validation - loss=2.9258e+00 ppl=18.65 best_loss=2.9793e+00 best_ppl=19.67
Epoch 20 - |param|=6.06e+02 |g_param|=1.39e+05 loss=3.3110e+00 ppl=27.41
Validation - loss=2.8943e+00 ppl=18.07 best_loss=2.9258e+00 best_ppl=18.65
Epoch 21 - |param|=6.06e+02 |g_param|=1.34e+05 loss=3.2722e+00 ppl=26.37
Validation - loss=2.8673e+00 ppl=17.59 best_loss=2.8943e+00 best_ppl=18.07
Epoch 22 - |param|=6.07e+02 |g_param|=1.55e+05 loss=3.2713e+00 ppl=26.35
Validation - loss=2.8278e+00 ppl=16.91 best_loss=2.8673e+00 best_ppl=17.59
Epoch 23 - |param|=6.07e+02 |g_param|=1.39e+05 loss=3.0968e+00 ppl=22.13
Validation - loss=2.7403e+00 ppl=15.49 best_loss=2.8278e+00 best_ppl=16.91
Epoch 24 - |param|=6.08e+02 |g_param|=1.49e+05 loss=3.0489e+00 ppl=21.09
Validation - loss=2.6758e+00 ppl=14.52 best_loss=2.7403e+00 best_ppl=15.49
Epoch 25 - |param|=6.08e+02 |g_param|=1.58e+05 loss=3.1114e+00 ppl=22.45
Validation - loss=2.7004e+00 ppl=14.89 best_loss=2.6758e+00 best_ppl=14.52
Epoch 26 - |param|=6.09e+02 |g_param|=1.56e+05 loss=2.9190e+00 ppl=18.52
Validation - loss=2.6044e+00 ppl=13.52 best_loss=2.6758e+00 best_ppl=14.52
Epoch 27 - |param|=6.09e+02 |g_param|=1.68e+05 loss=2.9414e+00 ppl=18.94
Validation - loss=2.5641e+00 ppl=12.99 best_loss=2.6044e+00 best_ppl=13.52
Epoch 28 - |param|=6.10e+02 |g_param|=1.60e+05 loss=2.8995e+00 ppl=18.17
Validation - loss=2.5167e+00 ppl=12.39 best_loss=2.5641e+00 best_ppl=12.99
Epoch 29 - |param|=6.10e+02 |g_param|=1.59e+05 loss=2.7572e+00 ppl=15.76
Validation - loss=2.4918e+00 ppl=12.08 best_loss=2.5167e+00 best_ppl=12.39
Epoch 30 - |param|=6.11e+02 |g_param|=1.85e+05 loss=2.7910e+00 ppl=16.30
Validation - loss=2.4517e+00 ppl=11.61 best_loss=2.4918e+00 best_ppl=12.08
Epoch 31 - |param|=6.11e+02 |g_param|=1.67e+05 loss=2.7631e+00 ppl=15.85
Validation - loss=2.4197e+00 ppl=11.24 best_loss=2.4517e+00 best_ppl=11.61
Epoch 32 - |param|=6.12e+02 |g_param|=1.89e+05 loss=2.6329e+00 ppl=13.91
Validation - loss=2.4249e+00 ppl=11.30 best_loss=2.4197e+00 best_ppl=11.24
Epoch 33 - |param|=6.13e+02 |g_param|=1.88e+05 loss=2.6597e+00 ppl=14.29
Validation - loss=2.3610e+00 ppl=10.60 best_loss=2.4197e+00 best_ppl=11.24
Epoch 34 - |param|=6.13e+02 |g_param|=1.91e+05 loss=2.5788e+00 ppl=13.18
Validation - loss=2.3173e+00 ppl=10.15 best_loss=2.3610e+00 best_ppl=10.60
Epoch 35 - |param|=6.14e+02 |g_param|=2.81e+05 loss=2.5911e+00 ppl=13.34
Validation - loss=2.2737e+00 ppl=9.71 best_loss=2.3173e+00 best_ppl=10.15
Epoch 36 - |param|=6.14e+02 |g_param|=3.84e+05 loss=2.5653e+00 ppl=13.01
Validation - loss=2.2620e+00 ppl=9.60 best_loss=2.2737e+00 best_ppl=9.71
Epoch 37 - |param|=6.15e+02 |g_param|=4.01e+05 loss=2.5425e+00 ppl=12.71
Validation - loss=2.2409e+00 ppl=9.40 best_loss=2.2620e+00 best_ppl=9.60
Epoch 38 - |param|=6.15e+02 |g_param|=4.16e+05 loss=2.4556e+00 ppl=11.65
Validation - loss=2.1957e+00 ppl=8.99 best_loss=2.2409e+00 best_ppl=9.40
Epoch 39 - |param|=6.16e+02 |g_param|=4.01e+05 loss=2.3799e+00 ppl=10.80
Validation - loss=2.2040e+00 ppl=9.06 best_loss=2.1957e+00 best_ppl=8.99
Epoch 40 - |param|=6.16e+02 |g_param|=4.14e+05 loss=2.4891e+00 ppl=12.05
Validation - loss=2.1716e+00 ppl=8.77 best_loss=2.1957e+00 best_ppl=8.99
mybk, seq2seq-baseline training start for 50 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/mybk-50epoch/seq-model-mybk.pth',
    'n_epochs': 50,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1313, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.69e+05 loss=4.8679e+00 ppl=130.05
Validation - loss=4.0466e+00 ppl=57.21 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.00e+02 |g_param|=2.68e+05 loss=4.4409e+00 ppl=84.85
Validation - loss=3.8353e+00 ppl=46.31 best_loss=4.0466e+00 best_ppl=57.21
Epoch 3 - |param|=6.00e+02 |g_param|=2.13e+05 loss=4.3585e+00 ppl=78.14
Validation - loss=3.8882e+00 ppl=48.82 best_loss=3.8353e+00 best_ppl=46.31
Epoch 4 - |param|=6.00e+02 |g_param|=1.81e+05 loss=4.3441e+00 ppl=77.02
Validation - loss=3.8197e+00 ppl=45.59 best_loss=3.8353e+00 best_ppl=46.31
Epoch 5 - |param|=6.00e+02 |g_param|=2.00e+05 loss=4.2958e+00 ppl=73.39
Validation - loss=3.8651e+00 ppl=47.71 best_loss=3.8197e+00 best_ppl=45.59
Epoch 6 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.3548e+00 ppl=77.85
Validation - loss=3.7828e+00 ppl=43.94 best_loss=3.8197e+00 best_ppl=45.59
Epoch 7 - |param|=6.00e+02 |g_param|=1.76e+05 loss=4.2879e+00 ppl=72.81
Validation - loss=3.7852e+00 ppl=44.05 best_loss=3.7828e+00 best_ppl=43.94
Epoch 8 - |param|=6.01e+02 |g_param|=1.90e+05 loss=4.3066e+00 ppl=74.19
Validation - loss=3.7448e+00 ppl=42.30 best_loss=3.7828e+00 best_ppl=43.94
Epoch 9 - |param|=6.01e+02 |g_param|=1.81e+05 loss=4.2589e+00 ppl=70.73
Validation - loss=3.7587e+00 ppl=42.89 best_loss=3.7448e+00 best_ppl=42.30
Epoch 10 - |param|=6.02e+02 |g_param|=1.88e+05 loss=4.2687e+00 ppl=71.43
Validation - loss=3.6828e+00 ppl=39.76 best_loss=3.7448e+00 best_ppl=42.30
Epoch 11 - |param|=6.02e+02 |g_param|=1.64e+05 loss=4.0711e+00 ppl=58.62
Validation - loss=3.5836e+00 ppl=36.00 best_loss=3.6828e+00 best_ppl=39.76
Epoch 12 - |param|=6.02e+02 |g_param|=1.46e+05 loss=3.9895e+00 ppl=54.03
Validation - loss=3.3853e+00 ppl=29.53 best_loss=3.5836e+00 best_ppl=36.00
Epoch 13 - |param|=6.03e+02 |g_param|=1.31e+05 loss=3.7635e+00 ppl=43.10
Validation - loss=3.2661e+00 ppl=26.21 best_loss=3.3853e+00 best_ppl=29.53
Epoch 14 - |param|=6.03e+02 |g_param|=1.33e+05 loss=3.7062e+00 ppl=40.70
Validation - loss=3.2102e+00 ppl=24.78 best_loss=3.2661e+00 best_ppl=26.21
Epoch 15 - |param|=6.04e+02 |g_param|=1.26e+05 loss=3.6110e+00 ppl=37.00
Validation - loss=3.1431e+00 ppl=23.18 best_loss=3.2102e+00 best_ppl=24.78
Epoch 16 - |param|=6.04e+02 |g_param|=1.33e+05 loss=3.6333e+00 ppl=37.84
Validation - loss=3.1174e+00 ppl=22.59 best_loss=3.1431e+00 best_ppl=23.18
Epoch 17 - |param|=6.05e+02 |g_param|=1.33e+05 loss=3.4923e+00 ppl=32.86
Validation - loss=3.0786e+00 ppl=21.73 best_loss=3.1174e+00 best_ppl=22.59
Epoch 18 - |param|=6.05e+02 |g_param|=1.44e+05 loss=3.5135e+00 ppl=33.57
Validation - loss=3.0396e+00 ppl=20.90 best_loss=3.0786e+00 best_ppl=21.73
Epoch 19 - |param|=6.06e+02 |g_param|=1.26e+05 loss=3.3802e+00 ppl=29.38
Validation - loss=2.9874e+00 ppl=19.83 best_loss=3.0396e+00 best_ppl=20.90
Epoch 20 - |param|=6.06e+02 |g_param|=1.35e+05 loss=3.3860e+00 ppl=29.55
Validation - loss=2.9466e+00 ppl=19.04 best_loss=2.9874e+00 best_ppl=19.83
Epoch 21 - |param|=6.07e+02 |g_param|=1.42e+05 loss=3.3811e+00 ppl=29.40
Validation - loss=2.9441e+00 ppl=18.99 best_loss=2.9466e+00 best_ppl=19.04
Epoch 22 - |param|=6.07e+02 |g_param|=1.55e+05 loss=3.3151e+00 ppl=27.53
Validation - loss=2.8663e+00 ppl=17.57 best_loss=2.9441e+00 best_ppl=18.99
Epoch 23 - |param|=6.08e+02 |g_param|=1.42e+05 loss=3.2229e+00 ppl=25.10
Validation - loss=2.8647e+00 ppl=17.54 best_loss=2.8663e+00 best_ppl=17.57
Epoch 24 - |param|=6.08e+02 |g_param|=1.55e+05 loss=3.1447e+00 ppl=23.21
Validation - loss=2.8071e+00 ppl=16.56 best_loss=2.8647e+00 best_ppl=17.54
Epoch 25 - |param|=6.09e+02 |g_param|=1.40e+05 loss=3.0694e+00 ppl=21.53
Validation - loss=2.7647e+00 ppl=15.87 best_loss=2.8071e+00 best_ppl=16.56
Epoch 26 - |param|=6.09e+02 |g_param|=1.47e+05 loss=3.0052e+00 ppl=20.19
Validation - loss=2.7472e+00 ppl=15.60 best_loss=2.7647e+00 best_ppl=15.87
Epoch 27 - |param|=6.10e+02 |g_param|=1.55e+05 loss=3.0127e+00 ppl=20.34
Validation - loss=2.6920e+00 ppl=14.76 best_loss=2.7472e+00 best_ppl=15.60
Epoch 28 - |param|=6.10e+02 |g_param|=1.64e+05 loss=2.9483e+00 ppl=19.07
Validation - loss=2.6941e+00 ppl=14.79 best_loss=2.6920e+00 best_ppl=14.76
Epoch 29 - |param|=6.11e+02 |g_param|=1.58e+05 loss=2.9282e+00 ppl=18.69
Validation - loss=2.7005e+00 ppl=14.89 best_loss=2.6920e+00 best_ppl=14.76
Epoch 30 - |param|=6.11e+02 |g_param|=1.71e+05 loss=2.9172e+00 ppl=18.49
Validation - loss=2.6786e+00 ppl=14.57 best_loss=2.6920e+00 best_ppl=14.76
Epoch 31 - |param|=6.12e+02 |g_param|=1.63e+05 loss=2.8569e+00 ppl=17.41
Validation - loss=2.6354e+00 ppl=13.95 best_loss=2.6786e+00 best_ppl=14.57
Epoch 32 - |param|=6.12e+02 |g_param|=1.65e+05 loss=2.8041e+00 ppl=16.51
Validation - loss=2.6340e+00 ppl=13.93 best_loss=2.6354e+00 best_ppl=13.95
Epoch 33 - |param|=6.13e+02 |g_param|=1.72e+05 loss=2.7531e+00 ppl=15.69
Validation - loss=2.6163e+00 ppl=13.69 best_loss=2.6340e+00 best_ppl=13.93
Epoch 34 - |param|=6.13e+02 |g_param|=1.76e+05 loss=2.7181e+00 ppl=15.15
Validation - loss=2.6029e+00 ppl=13.50 best_loss=2.6163e+00 best_ppl=13.69
Epoch 35 - |param|=6.14e+02 |g_param|=3.17e+05 loss=2.7039e+00 ppl=14.94
Validation - loss=2.5797e+00 ppl=13.19 best_loss=2.6029e+00 best_ppl=13.50
Epoch 36 - |param|=6.14e+02 |g_param|=3.83e+05 loss=2.6545e+00 ppl=14.22
Validation - loss=2.5356e+00 ppl=12.62 best_loss=2.5797e+00 best_ppl=13.19
Epoch 37 - |param|=6.15e+02 |g_param|=3.58e+05 loss=2.6259e+00 ppl=13.82
Validation - loss=2.5684e+00 ppl=13.04 best_loss=2.5356e+00 best_ppl=12.62
Epoch 38 - |param|=6.15e+02 |g_param|=4.02e+05 loss=2.6169e+00 ppl=13.69
Validation - loss=2.5743e+00 ppl=13.12 best_loss=2.5356e+00 best_ppl=12.62
Epoch 39 - |param|=6.16e+02 |g_param|=3.73e+05 loss=2.5620e+00 ppl=12.96
Validation - loss=2.5292e+00 ppl=12.54 best_loss=2.5356e+00 best_ppl=12.62
Epoch 40 - |param|=6.16e+02 |g_param|=3.89e+05 loss=2.5685e+00 ppl=13.05
Validation - loss=2.5120e+00 ppl=12.33 best_loss=2.5292e+00 best_ppl=12.54
Epoch 41 - |param|=6.17e+02 |g_param|=3.70e+05 loss=2.4815e+00 ppl=11.96
Validation - loss=2.5375e+00 ppl=12.65 best_loss=2.5120e+00 best_ppl=12.33
Epoch 42 - |param|=6.17e+02 |g_param|=4.02e+05 loss=2.4201e+00 ppl=11.25
Validation - loss=2.4898e+00 ppl=12.06 best_loss=2.5120e+00 best_ppl=12.33
Epoch 43 - |param|=6.18e+02 |g_param|=3.95e+05 loss=2.4567e+00 ppl=11.67
Validation - loss=2.5184e+00 ppl=12.41 best_loss=2.4898e+00 best_ppl=12.06
Epoch 44 - |param|=6.18e+02 |g_param|=4.13e+05 loss=2.4067e+00 ppl=11.10
Validation - loss=2.5031e+00 ppl=12.22 best_loss=2.4898e+00 best_ppl=12.06
Epoch 45 - |param|=6.19e+02 |g_param|=3.99e+05 loss=2.3558e+00 ppl=10.55
Validation - loss=2.4953e+00 ppl=12.13 best_loss=2.4898e+00 best_ppl=12.06
Epoch 46 - |param|=6.19e+02 |g_param|=4.29e+05 loss=2.3966e+00 ppl=10.99
Validation - loss=2.4716e+00 ppl=11.84 best_loss=2.4898e+00 best_ppl=12.06
Epoch 47 - |param|=6.19e+02 |g_param|=4.20e+05 loss=2.3371e+00 ppl=10.35
Validation - loss=2.4844e+00 ppl=11.99 best_loss=2.4716e+00 best_ppl=11.84
Epoch 48 - |param|=6.20e+02 |g_param|=4.66e+05 loss=2.3044e+00 ppl=10.02
Validation - loss=2.4740e+00 ppl=11.87 best_loss=2.4716e+00 best_ppl=11.84
Epoch 49 - |param|=6.20e+02 |g_param|=4.30e+05 loss=2.2810e+00 ppl=9.79
Validation - loss=2.4781e+00 ppl=11.92 best_loss=2.4716e+00 best_ppl=11.84
Epoch 50 - |param|=6.21e+02 |g_param|=4.59e+05 loss=2.2603e+00 ppl=9.59
Validation - loss=2.4579e+00 ppl=11.68 best_loss=2.4716e+00 best_ppl=11.84
mybk, seq2seq-baseline training start for 60 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/mybk-60epoch/seq-model-mybk.pth',
    'n_epochs': 60,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1313, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.60e+05 loss=4.8877e+00 ppl=132.65
Validation - loss=4.1676e+00 ppl=64.56 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.01e+02 |g_param|=2.21e+05 loss=4.4861e+00 ppl=88.78
Validation - loss=3.9192e+00 ppl=50.36 best_loss=4.1676e+00 best_ppl=64.56
Epoch 3 - |param|=6.01e+02 |g_param|=1.83e+05 loss=4.3759e+00 ppl=79.51
Validation - loss=3.8564e+00 ppl=47.29 best_loss=3.9192e+00 best_ppl=50.36
Epoch 4 - |param|=6.01e+02 |g_param|=2.13e+05 loss=4.4573e+00 ppl=86.25
Validation - loss=3.8845e+00 ppl=48.64 best_loss=3.8564e+00 best_ppl=47.29
Epoch 5 - |param|=6.01e+02 |g_param|=1.88e+05 loss=4.3387e+00 ppl=76.61
Validation - loss=3.8121e+00 ppl=45.25 best_loss=3.8564e+00 best_ppl=47.29
Epoch 6 - |param|=6.01e+02 |g_param|=1.86e+05 loss=4.2755e+00 ppl=71.91
Validation - loss=3.7976e+00 ppl=44.59 best_loss=3.8121e+00 best_ppl=45.25
Epoch 7 - |param|=6.01e+02 |g_param|=1.87e+05 loss=4.2585e+00 ppl=70.70
Validation - loss=3.7903e+00 ppl=44.27 best_loss=3.7976e+00 best_ppl=44.59
Epoch 8 - |param|=6.02e+02 |g_param|=1.75e+05 loss=4.2466e+00 ppl=69.86
Validation - loss=3.7337e+00 ppl=41.83 best_loss=3.7903e+00 best_ppl=44.27
Epoch 9 - |param|=6.02e+02 |g_param|=1.78e+05 loss=4.1632e+00 ppl=64.28
Validation - loss=3.6580e+00 ppl=38.78 best_loss=3.7337e+00 best_ppl=41.83
Epoch 10 - |param|=6.02e+02 |g_param|=1.46e+05 loss=3.9745e+00 ppl=53.22
Validation - loss=3.4587e+00 ppl=31.78 best_loss=3.6580e+00 best_ppl=38.78
Epoch 11 - |param|=6.03e+02 |g_param|=1.31e+05 loss=3.8112e+00 ppl=45.20
Validation - loss=3.3740e+00 ppl=29.20 best_loss=3.4587e+00 best_ppl=31.78
Epoch 12 - |param|=6.03e+02 |g_param|=1.52e+05 loss=3.7437e+00 ppl=42.25
Validation - loss=3.3005e+00 ppl=27.13 best_loss=3.3740e+00 best_ppl=29.20
Epoch 13 - |param|=6.04e+02 |g_param|=1.34e+05 loss=3.6455e+00 ppl=38.30
Validation - loss=3.2381e+00 ppl=25.48 best_loss=3.3005e+00 best_ppl=27.13
Epoch 14 - |param|=6.04e+02 |g_param|=1.34e+05 loss=3.6945e+00 ppl=40.22
Validation - loss=3.2047e+00 ppl=24.65 best_loss=3.2381e+00 best_ppl=25.48
Epoch 15 - |param|=6.04e+02 |g_param|=1.30e+05 loss=3.5591e+00 ppl=35.13
Validation - loss=3.1432e+00 ppl=23.18 best_loss=3.2047e+00 best_ppl=24.65
Epoch 16 - |param|=6.05e+02 |g_param|=1.40e+05 loss=3.4937e+00 ppl=32.91
Validation - loss=3.1005e+00 ppl=22.21 best_loss=3.1432e+00 best_ppl=23.18
Epoch 17 - |param|=6.05e+02 |g_param|=1.32e+05 loss=3.3997e+00 ppl=29.95
Validation - loss=3.0158e+00 ppl=20.41 best_loss=3.1005e+00 best_ppl=22.21
Epoch 18 - |param|=6.06e+02 |g_param|=1.44e+05 loss=3.3433e+00 ppl=28.31
Validation - loss=2.9965e+00 ppl=20.01 best_loss=3.0158e+00 best_ppl=20.41
Epoch 19 - |param|=6.06e+02 |g_param|=1.43e+05 loss=3.2991e+00 ppl=27.09
Validation - loss=2.9590e+00 ppl=19.28 best_loss=2.9965e+00 best_ppl=20.01
Epoch 20 - |param|=6.07e+02 |g_param|=1.59e+05 loss=3.2522e+00 ppl=25.85
Validation - loss=2.9082e+00 ppl=18.32 best_loss=2.9590e+00 best_ppl=19.28
Epoch 21 - |param|=6.08e+02 |g_param|=1.45e+05 loss=3.1590e+00 ppl=23.55
Validation - loss=2.8392e+00 ppl=17.10 best_loss=2.9082e+00 best_ppl=18.32
Epoch 22 - |param|=6.08e+02 |g_param|=1.46e+05 loss=3.1216e+00 ppl=22.68
Validation - loss=2.8345e+00 ppl=17.02 best_loss=2.8392e+00 best_ppl=17.10
Epoch 23 - |param|=6.09e+02 |g_param|=1.63e+05 loss=3.1583e+00 ppl=23.53
Validation - loss=2.7821e+00 ppl=16.15 best_loss=2.8345e+00 best_ppl=17.02
Epoch 24 - |param|=6.09e+02 |g_param|=1.57e+05 loss=3.0570e+00 ppl=21.26
Validation - loss=2.7593e+00 ppl=15.79 best_loss=2.7821e+00 best_ppl=16.15
Epoch 25 - |param|=6.10e+02 |g_param|=1.53e+05 loss=2.9888e+00 ppl=19.86
Validation - loss=2.7456e+00 ppl=15.57 best_loss=2.7593e+00 best_ppl=15.79
Epoch 26 - |param|=6.10e+02 |g_param|=1.59e+05 loss=2.9449e+00 ppl=19.01
Validation - loss=2.7106e+00 ppl=15.04 best_loss=2.7456e+00 best_ppl=15.57
Epoch 27 - |param|=6.11e+02 |g_param|=1.57e+05 loss=2.9086e+00 ppl=18.33
Validation - loss=2.6889e+00 ppl=14.72 best_loss=2.7106e+00 best_ppl=15.04
Epoch 28 - |param|=6.11e+02 |g_param|=1.64e+05 loss=2.8820e+00 ppl=17.85
Validation - loss=2.6789e+00 ppl=14.57 best_loss=2.6889e+00 best_ppl=14.72
Epoch 29 - |param|=6.12e+02 |g_param|=1.59e+05 loss=2.8062e+00 ppl=16.55
Validation - loss=2.6493e+00 ppl=14.14 best_loss=2.6789e+00 best_ppl=14.57
Epoch 30 - |param|=6.12e+02 |g_param|=1.80e+05 loss=2.8610e+00 ppl=17.48
Validation - loss=2.6506e+00 ppl=14.16 best_loss=2.6493e+00 best_ppl=14.14
Epoch 31 - |param|=6.13e+02 |g_param|=1.73e+05 loss=2.7503e+00 ppl=15.65
Validation - loss=2.6477e+00 ppl=14.12 best_loss=2.6493e+00 best_ppl=14.14
Epoch 32 - |param|=6.13e+02 |g_param|=1.76e+05 loss=2.7066e+00 ppl=14.98
Validation - loss=2.6238e+00 ppl=13.79 best_loss=2.6477e+00 best_ppl=14.12
Epoch 33 - |param|=6.14e+02 |g_param|=1.70e+05 loss=2.7098e+00 ppl=15.03
Validation - loss=2.5919e+00 ppl=13.35 best_loss=2.6238e+00 best_ppl=13.79
Epoch 34 - |param|=6.14e+02 |g_param|=2.48e+05 loss=2.6281e+00 ppl=13.85
Validation - loss=2.5899e+00 ppl=13.33 best_loss=2.5919e+00 best_ppl=13.35
Epoch 35 - |param|=6.15e+02 |g_param|=3.69e+05 loss=2.6782e+00 ppl=14.56
Validation - loss=2.6181e+00 ppl=13.71 best_loss=2.5899e+00 best_ppl=13.33
Epoch 36 - |param|=6.15e+02 |g_param|=3.86e+05 loss=2.6005e+00 ppl=13.47
Validation - loss=2.5992e+00 ppl=13.45 best_loss=2.5899e+00 best_ppl=13.33
Epoch 37 - |param|=6.16e+02 |g_param|=3.72e+05 loss=2.5687e+00 ppl=13.05
Validation - loss=2.5832e+00 ppl=13.24 best_loss=2.5899e+00 best_ppl=13.33
Epoch 38 - |param|=6.16e+02 |g_param|=3.90e+05 loss=2.5662e+00 ppl=13.02
Validation - loss=2.5849e+00 ppl=13.26 best_loss=2.5832e+00 best_ppl=13.24
Epoch 39 - |param|=6.17e+02 |g_param|=3.85e+05 loss=2.5686e+00 ppl=13.05
Validation - loss=2.5826e+00 ppl=13.23 best_loss=2.5832e+00 best_ppl=13.24
Epoch 40 - |param|=6.17e+02 |g_param|=4.06e+05 loss=2.4820e+00 ppl=11.96
Validation - loss=2.6098e+00 ppl=13.60 best_loss=2.5826e+00 best_ppl=13.23
Epoch 41 - |param|=6.18e+02 |g_param|=3.91e+05 loss=2.4596e+00 ppl=11.70
Validation - loss=2.5835e+00 ppl=13.24 best_loss=2.5826e+00 best_ppl=13.23
Epoch 42 - |param|=6.18e+02 |g_param|=3.93e+05 loss=2.3559e+00 ppl=10.55
Validation - loss=2.5392e+00 ppl=12.67 best_loss=2.5826e+00 best_ppl=13.23
Epoch 43 - |param|=6.19e+02 |g_param|=3.98e+05 loss=2.3781e+00 ppl=10.78
Validation - loss=2.5649e+00 ppl=13.00 best_loss=2.5392e+00 best_ppl=12.67
Epoch 44 - |param|=6.19e+02 |g_param|=4.29e+05 loss=2.4177e+00 ppl=11.22
Validation - loss=2.5511e+00 ppl=12.82 best_loss=2.5392e+00 best_ppl=12.67
Epoch 45 - |param|=6.20e+02 |g_param|=4.10e+05 loss=2.3477e+00 ppl=10.46
Validation - loss=2.5602e+00 ppl=12.94 best_loss=2.5392e+00 best_ppl=12.67
Epoch 46 - |param|=6.20e+02 |g_param|=4.44e+05 loss=2.2752e+00 ppl=9.73
Validation - loss=2.5752e+00 ppl=13.13 best_loss=2.5392e+00 best_ppl=12.67
Epoch 47 - |param|=6.20e+02 |g_param|=4.35e+05 loss=2.2918e+00 ppl=9.89
Validation - loss=2.5626e+00 ppl=12.97 best_loss=2.5392e+00 best_ppl=12.67
Epoch 48 - |param|=6.21e+02 |g_param|=4.53e+05 loss=2.3543e+00 ppl=10.53
Validation - loss=2.5354e+00 ppl=12.62 best_loss=2.5392e+00 best_ppl=12.67
Epoch 49 - |param|=6.21e+02 |g_param|=4.38e+05 loss=2.2408e+00 ppl=9.40
Validation - loss=2.5649e+00 ppl=13.00 best_loss=2.5354e+00 best_ppl=12.62
Epoch 50 - |param|=6.22e+02 |g_param|=4.41e+05 loss=2.1866e+00 ppl=8.91
Validation - loss=2.5552e+00 ppl=12.87 best_loss=2.5354e+00 best_ppl=12.62
Epoch 51 - |param|=6.22e+02 |g_param|=4.60e+05 loss=2.2542e+00 ppl=9.53
Validation - loss=2.5606e+00 ppl=12.94 best_loss=2.5354e+00 best_ppl=12.62
Epoch 52 - |param|=6.23e+02 |g_param|=4.69e+05 loss=2.1902e+00 ppl=8.94
Validation - loss=2.5835e+00 ppl=13.24 best_loss=2.5354e+00 best_ppl=12.62
Epoch 53 - |param|=6.23e+02 |g_param|=4.60e+05 loss=2.1365e+00 ppl=8.47
Validation - loss=2.5749e+00 ppl=13.13 best_loss=2.5354e+00 best_ppl=12.62
Epoch 54 - |param|=6.23e+02 |g_param|=4.76e+05 loss=2.2040e+00 ppl=9.06
Validation - loss=2.5746e+00 ppl=13.13 best_loss=2.5354e+00 best_ppl=12.62
Epoch 55 - |param|=6.24e+02 |g_param|=4.59e+05 loss=2.0708e+00 ppl=7.93
Validation - loss=2.5809e+00 ppl=13.21 best_loss=2.5354e+00 best_ppl=12.62
Epoch 56 - |param|=6.24e+02 |g_param|=4.77e+05 loss=2.0622e+00 ppl=7.86
Validation - loss=2.5840e+00 ppl=13.25 best_loss=2.5354e+00 best_ppl=12.62
Epoch 57 - |param|=6.25e+02 |g_param|=4.81e+05 loss=2.0598e+00 ppl=7.84
Validation - loss=2.5763e+00 ppl=13.15 best_loss=2.5354e+00 best_ppl=12.62
Epoch 58 - |param|=6.25e+02 |g_param|=5.06e+05 loss=2.0284e+00 ppl=7.60
Validation - loss=2.6002e+00 ppl=13.47 best_loss=2.5354e+00 best_ppl=12.62
Epoch 59 - |param|=6.26e+02 |g_param|=4.73e+05 loss=2.0019e+00 ppl=7.40
Validation - loss=2.6124e+00 ppl=13.63 best_loss=2.5354e+00 best_ppl=12.62
Epoch 60 - |param|=6.26e+02 |g_param|=4.98e+05 loss=2.0047e+00 ppl=7.42
Validation - loss=2.5896e+00 ppl=13.32 best_loss=2.5354e+00 best_ppl=12.62
mybk, seq2seq-baseline training start for 70 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/mybk-70epoch/seq-model-mybk.pth',
    'n_epochs': 70,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1313, 128)
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
Epoch 1 - |param|=6.01e+02 |g_param|=3.41e+05 loss=4.9191e+00 ppl=136.88
Validation - loss=4.1010e+00 ppl=60.40 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.01e+02 |g_param|=3.76e+05 loss=4.4570e+00 ppl=86.23
Validation - loss=3.9003e+00 ppl=49.42 best_loss=4.1010e+00 best_ppl=60.40
Epoch 3 - |param|=6.01e+02 |g_param|=2.24e+05 loss=4.4544e+00 ppl=86.00
Validation - loss=3.8711e+00 ppl=48.00 best_loss=3.9003e+00 best_ppl=49.42
Epoch 4 - |param|=6.01e+02 |g_param|=2.12e+05 loss=4.4320e+00 ppl=84.10
Validation - loss=3.8126e+00 ppl=45.27 best_loss=3.8711e+00 best_ppl=48.00
Epoch 5 - |param|=6.01e+02 |g_param|=1.95e+05 loss=4.3668e+00 ppl=78.79
Validation - loss=3.8004e+00 ppl=44.72 best_loss=3.8126e+00 best_ppl=45.27
Epoch 6 - |param|=6.01e+02 |g_param|=1.88e+05 loss=4.3015e+00 ppl=73.81
Validation - loss=3.7710e+00 ppl=43.42 best_loss=3.8004e+00 best_ppl=44.72
Epoch 7 - |param|=6.02e+02 |g_param|=1.73e+05 loss=4.2630e+00 ppl=71.02
Validation - loss=3.7657e+00 ppl=43.20 best_loss=3.7710e+00 best_ppl=43.42
Epoch 8 - |param|=6.02e+02 |g_param|=2.05e+05 loss=4.3057e+00 ppl=74.12
Validation - loss=3.7595e+00 ppl=42.93 best_loss=3.7657e+00 best_ppl=43.20
Epoch 9 - |param|=6.02e+02 |g_param|=1.88e+05 loss=4.2449e+00 ppl=69.75
Validation - loss=3.7640e+00 ppl=43.12 best_loss=3.7595e+00 best_ppl=42.93
Epoch 10 - |param|=6.03e+02 |g_param|=1.86e+05 loss=4.2643e+00 ppl=71.12
Validation - loss=3.6906e+00 ppl=40.07 best_loss=3.7595e+00 best_ppl=42.93
Epoch 11 - |param|=6.03e+02 |g_param|=1.55e+05 loss=4.0118e+00 ppl=55.25
Validation - loss=3.5088e+00 ppl=33.41 best_loss=3.6906e+00 best_ppl=40.07
Epoch 12 - |param|=6.04e+02 |g_param|=1.40e+05 loss=3.8769e+00 ppl=48.28
Validation - loss=3.4036e+00 ppl=30.07 best_loss=3.5088e+00 best_ppl=33.41
Epoch 13 - |param|=6.04e+02 |g_param|=1.40e+05 loss=3.7751e+00 ppl=43.60
Validation - loss=3.3284e+00 ppl=27.89 best_loss=3.4036e+00 best_ppl=30.07
Epoch 14 - |param|=6.04e+02 |g_param|=1.38e+05 loss=3.6730e+00 ppl=39.37
Validation - loss=3.2566e+00 ppl=25.96 best_loss=3.3284e+00 best_ppl=27.89
Epoch 15 - |param|=6.05e+02 |g_param|=1.27e+05 loss=3.5440e+00 ppl=34.61
Validation - loss=3.1909e+00 ppl=24.31 best_loss=3.2566e+00 best_ppl=25.96
Epoch 16 - |param|=6.05e+02 |g_param|=1.36e+05 loss=3.5548e+00 ppl=34.98
Validation - loss=3.1271e+00 ppl=22.81 best_loss=3.1909e+00 best_ppl=24.31
Epoch 17 - |param|=6.06e+02 |g_param|=1.26e+05 loss=3.3683e+00 ppl=29.03
Validation - loss=3.0443e+00 ppl=21.00 best_loss=3.1271e+00 best_ppl=22.81
Epoch 18 - |param|=6.06e+02 |g_param|=1.45e+05 loss=3.4206e+00 ppl=30.59
Validation - loss=3.0013e+00 ppl=20.11 best_loss=3.0443e+00 best_ppl=21.00
Epoch 19 - |param|=6.07e+02 |g_param|=1.38e+05 loss=3.2916e+00 ppl=26.89
Validation - loss=2.9608e+00 ppl=19.31 best_loss=3.0013e+00 best_ppl=20.11
Epoch 20 - |param|=6.07e+02 |g_param|=1.44e+05 loss=3.2146e+00 ppl=24.89
Validation - loss=2.8970e+00 ppl=18.12 best_loss=2.9608e+00 best_ppl=19.31
Epoch 21 - |param|=6.08e+02 |g_param|=1.50e+05 loss=3.1654e+00 ppl=23.70
Validation - loss=2.8520e+00 ppl=17.32 best_loss=2.8970e+00 best_ppl=18.12
Epoch 22 - |param|=6.09e+02 |g_param|=1.58e+05 loss=3.1154e+00 ppl=22.54
Validation - loss=2.8230e+00 ppl=16.83 best_loss=2.8520e+00 best_ppl=17.32
Epoch 23 - |param|=6.09e+02 |g_param|=1.48e+05 loss=3.0742e+00 ppl=21.63
Validation - loss=2.7705e+00 ppl=15.97 best_loss=2.8230e+00 best_ppl=16.83
Epoch 24 - |param|=6.10e+02 |g_param|=1.55e+05 loss=3.0044e+00 ppl=20.17
Validation - loss=2.7312e+00 ppl=15.35 best_loss=2.7705e+00 best_ppl=15.97
Epoch 25 - |param|=6.10e+02 |g_param|=1.59e+05 loss=3.0057e+00 ppl=20.20
Validation - loss=2.7069e+00 ppl=14.98 best_loss=2.7312e+00 best_ppl=15.35
Epoch 26 - |param|=6.11e+02 |g_param|=1.60e+05 loss=2.8598e+00 ppl=17.46
Validation - loss=2.6607e+00 ppl=14.31 best_loss=2.7069e+00 best_ppl=14.98
Epoch 27 - |param|=6.11e+02 |g_param|=1.60e+05 loss=2.8291e+00 ppl=16.93
Validation - loss=2.6395e+00 ppl=14.01 best_loss=2.6607e+00 best_ppl=14.31
Epoch 28 - |param|=6.12e+02 |g_param|=1.69e+05 loss=2.8892e+00 ppl=17.98
Validation - loss=2.6069e+00 ppl=13.56 best_loss=2.6395e+00 best_ppl=14.01
Epoch 29 - |param|=6.12e+02 |g_param|=1.78e+05 loss=2.8687e+00 ppl=17.61
Validation - loss=2.5857e+00 ppl=13.27 best_loss=2.6069e+00 best_ppl=13.56
Epoch 30 - |param|=6.13e+02 |g_param|=1.79e+05 loss=2.7833e+00 ppl=16.17
Validation - loss=2.5556e+00 ppl=12.88 best_loss=2.5857e+00 best_ppl=13.27
Epoch 31 - |param|=6.13e+02 |g_param|=1.71e+05 loss=2.7031e+00 ppl=14.93
Validation - loss=2.5433e+00 ppl=12.72 best_loss=2.5556e+00 best_ppl=12.88
Epoch 32 - |param|=6.14e+02 |g_param|=1.79e+05 loss=2.6715e+00 ppl=14.46
Validation - loss=2.5194e+00 ppl=12.42 best_loss=2.5433e+00 best_ppl=12.72
Epoch 33 - |param|=6.14e+02 |g_param|=1.79e+05 loss=2.6463e+00 ppl=14.10
Validation - loss=2.5254e+00 ppl=12.50 best_loss=2.5194e+00 best_ppl=12.42
Epoch 34 - |param|=6.15e+02 |g_param|=1.82e+05 loss=2.6042e+00 ppl=13.52
Validation - loss=2.5016e+00 ppl=12.20 best_loss=2.5194e+00 best_ppl=12.42
Epoch 35 - |param|=6.15e+02 |g_param|=2.28e+05 loss=2.4849e+00 ppl=12.00
Validation - loss=2.4826e+00 ppl=11.97 best_loss=2.5016e+00 best_ppl=12.20
Epoch 36 - |param|=6.16e+02 |g_param|=3.79e+05 loss=2.4970e+00 ppl=12.15
Validation - loss=2.4773e+00 ppl=11.91 best_loss=2.4826e+00 best_ppl=11.97
Epoch 37 - |param|=6.16e+02 |g_param|=3.85e+05 loss=2.5252e+00 ppl=12.49
Validation - loss=2.4745e+00 ppl=11.88 best_loss=2.4773e+00 best_ppl=11.91
Epoch 38 - |param|=6.17e+02 |g_param|=4.02e+05 loss=2.4146e+00 ppl=11.19
Validation - loss=2.4333e+00 ppl=11.40 best_loss=2.4745e+00 best_ppl=11.88
Epoch 39 - |param|=6.17e+02 |g_param|=3.89e+05 loss=2.4061e+00 ppl=11.09
Validation - loss=2.4157e+00 ppl=11.20 best_loss=2.4333e+00 best_ppl=11.40
Epoch 40 - |param|=6.18e+02 |g_param|=4.03e+05 loss=2.3705e+00 ppl=10.70
Validation - loss=2.4328e+00 ppl=11.39 best_loss=2.4157e+00 best_ppl=11.20
Epoch 41 - |param|=6.18e+02 |g_param|=4.02e+05 loss=2.3445e+00 ppl=10.43
Validation - loss=2.4228e+00 ppl=11.28 best_loss=2.4157e+00 best_ppl=11.20
Epoch 42 - |param|=6.19e+02 |g_param|=4.15e+05 loss=2.3819e+00 ppl=10.83
Validation - loss=2.4252e+00 ppl=11.30 best_loss=2.4157e+00 best_ppl=11.20
Epoch 43 - |param|=6.19e+02 |g_param|=4.13e+05 loss=2.2953e+00 ppl=9.93
Validation - loss=2.4037e+00 ppl=11.06 best_loss=2.4157e+00 best_ppl=11.20
Epoch 44 - |param|=6.20e+02 |g_param|=4.28e+05 loss=2.2642e+00 ppl=9.62
Validation - loss=2.3946e+00 ppl=10.96 best_loss=2.4037e+00 best_ppl=11.06
Epoch 45 - |param|=6.20e+02 |g_param|=4.20e+05 loss=2.2280e+00 ppl=9.28
Validation - loss=2.3875e+00 ppl=10.89 best_loss=2.3946e+00 best_ppl=10.96
Epoch 46 - |param|=6.21e+02 |g_param|=4.60e+05 loss=2.1977e+00 ppl=9.00
Validation - loss=2.3966e+00 ppl=10.99 best_loss=2.3875e+00 best_ppl=10.89
Epoch 47 - |param|=6.21e+02 |g_param|=4.32e+05 loss=2.1848e+00 ppl=8.89
Validation - loss=2.4004e+00 ppl=11.03 best_loss=2.3875e+00 best_ppl=10.89
Epoch 48 - |param|=6.22e+02 |g_param|=4.53e+05 loss=2.1802e+00 ppl=8.85
Validation - loss=2.3773e+00 ppl=10.78 best_loss=2.3875e+00 best_ppl=10.89
Epoch 49 - |param|=6.22e+02 |g_param|=4.41e+05 loss=2.1111e+00 ppl=8.26
Validation - loss=2.3874e+00 ppl=10.89 best_loss=2.3773e+00 best_ppl=10.78
Epoch 50 - |param|=6.23e+02 |g_param|=4.58e+05 loss=2.0620e+00 ppl=7.86
Validation - loss=2.3664e+00 ppl=10.66 best_loss=2.3773e+00 best_ppl=10.78
Epoch 51 - |param|=6.23e+02 |g_param|=4.70e+05 loss=2.0421e+00 ppl=7.71
Validation - loss=2.3619e+00 ppl=10.61 best_loss=2.3664e+00 best_ppl=10.66
Epoch 52 - |param|=6.24e+02 |g_param|=4.79e+05 loss=2.0118e+00 ppl=7.48
Validation - loss=2.3808e+00 ppl=10.81 best_loss=2.3619e+00 best_ppl=10.61
Epoch 53 - |param|=6.24e+02 |g_param|=4.81e+05 loss=2.1114e+00 ppl=8.26
Validation - loss=2.3555e+00 ppl=10.54 best_loss=2.3619e+00 best_ppl=10.61
Epoch 54 - |param|=6.24e+02 |g_param|=4.91e+05 loss=2.0333e+00 ppl=7.64
Validation - loss=2.3432e+00 ppl=10.41 best_loss=2.3555e+00 best_ppl=10.54
Epoch 55 - |param|=6.25e+02 |g_param|=4.82e+05 loss=1.9887e+00 ppl=7.31
Validation - loss=2.3693e+00 ppl=10.69 best_loss=2.3432e+00 best_ppl=10.41
Epoch 56 - |param|=6.25e+02 |g_param|=5.07e+05 loss=1.9423e+00 ppl=6.97
Validation - loss=2.3537e+00 ppl=10.52 best_loss=2.3432e+00 best_ppl=10.41
Epoch 57 - |param|=6.26e+02 |g_param|=5.10e+05 loss=1.9584e+00 ppl=7.09
Validation - loss=2.3589e+00 ppl=10.58 best_loss=2.3432e+00 best_ppl=10.41
Epoch 58 - |param|=6.26e+02 |g_param|=5.13e+05 loss=1.9042e+00 ppl=6.71
Validation - loss=2.3652e+00 ppl=10.65 best_loss=2.3432e+00 best_ppl=10.41
Epoch 59 - |param|=6.27e+02 |g_param|=5.23e+05 loss=1.8569e+00 ppl=6.40
Validation - loss=2.3764e+00 ppl=10.77 best_loss=2.3432e+00 best_ppl=10.41
Epoch 60 - |param|=6.27e+02 |g_param|=5.47e+05 loss=1.8579e+00 ppl=6.41
Validation - loss=2.3578e+00 ppl=10.57 best_loss=2.3432e+00 best_ppl=10.41
Epoch 61 - |param|=6.27e+02 |g_param|=5.21e+05 loss=1.8475e+00 ppl=6.34
Validation - loss=2.3408e+00 ppl=10.39 best_loss=2.3432e+00 best_ppl=10.41
Epoch 62 - |param|=6.28e+02 |g_param|=5.09e+05 loss=1.7757e+00 ppl=5.90
Validation - loss=2.3673e+00 ppl=10.67 best_loss=2.3408e+00 best_ppl=10.39
Epoch 63 - |param|=6.28e+02 |g_param|=5.02e+05 loss=1.8228e+00 ppl=6.19
Validation - loss=2.3837e+00 ppl=10.84 best_loss=2.3408e+00 best_ppl=10.39
Epoch 64 - |param|=6.29e+02 |g_param|=5.18e+05 loss=1.7578e+00 ppl=5.80
Validation - loss=2.3324e+00 ppl=10.30 best_loss=2.3408e+00 best_ppl=10.39
Epoch 65 - |param|=6.29e+02 |g_param|=5.10e+05 loss=1.7497e+00 ppl=5.75
Validation - loss=2.3358e+00 ppl=10.34 best_loss=2.3324e+00 best_ppl=10.30
Epoch 66 - |param|=6.30e+02 |g_param|=5.58e+05 loss=1.7571e+00 ppl=5.80
Validation - loss=2.3840e+00 ppl=10.85 best_loss=2.3324e+00 best_ppl=10.30
Epoch 67 - |param|=6.30e+02 |g_param|=5.71e+05 loss=1.7528e+00 ppl=5.77
Validation - loss=2.3577e+00 ppl=10.57 best_loss=2.3324e+00 best_ppl=10.30
Epoch 68 - |param|=6.30e+02 |g_param|=9.69e+05 loss=1.7704e+00 ppl=5.87
Validation - loss=2.3861e+00 ppl=10.87 best_loss=2.3324e+00 best_ppl=10.30
Epoch 69 - |param|=6.31e+02 |g_param|=1.04e+06 loss=1.6519e+00 ppl=5.22
Validation - loss=2.3931e+00 ppl=10.95 best_loss=2.3324e+00 best_ppl=10.30
Epoch 70 - |param|=6.31e+02 |g_param|=5.60e+05 loss=1.6083e+00 ppl=4.99
Validation - loss=2.3572e+00 ppl=10.56 best_loss=2.3324e+00 best_ppl=10.30
####################
bkmy, seq2seq-baseline training start for 30 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-30epoch/seq-model-bkmy.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.64e+05 loss=4.7536e+00 ppl=116.00
Validation - loss=3.9671e+00 ppl=52.83 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.00e+02 |g_param|=3.76e+05 loss=4.2156e+00 ppl=67.74
Validation - loss=3.8207e+00 ppl=45.64 best_loss=3.9671e+00 best_ppl=52.83
Epoch 3 - |param|=6.00e+02 |g_param|=4.02e+05 loss=4.1755e+00 ppl=65.07
Validation - loss=3.7723e+00 ppl=43.48 best_loss=3.8207e+00 best_ppl=45.64
Epoch 4 - |param|=6.00e+02 |g_param|=2.37e+05 loss=4.1738e+00 ppl=64.96
Validation - loss=3.7450e+00 ppl=42.31 best_loss=3.7723e+00 best_ppl=43.48
Epoch 5 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.1612e+00 ppl=64.15
Validation - loss=3.7329e+00 ppl=41.80 best_loss=3.7450e+00 best_ppl=42.31
Epoch 6 - |param|=6.00e+02 |g_param|=2.16e+05 loss=4.1427e+00 ppl=62.97
Validation - loss=3.7487e+00 ppl=42.47 best_loss=3.7329e+00 best_ppl=41.80
Epoch 7 - |param|=6.01e+02 |g_param|=2.03e+05 loss=4.1111e+00 ppl=61.01
Validation - loss=3.7162e+00 ppl=41.11 best_loss=3.7329e+00 best_ppl=41.80
Epoch 8 - |param|=6.01e+02 |g_param|=1.95e+05 loss=4.0920e+00 ppl=59.86
Validation - loss=3.6638e+00 ppl=39.01 best_loss=3.7162e+00 best_ppl=41.11
Epoch 9 - |param|=6.01e+02 |g_param|=1.96e+05 loss=4.0315e+00 ppl=56.35
Validation - loss=3.6621e+00 ppl=38.94 best_loss=3.6638e+00 best_ppl=39.01
Epoch 10 - |param|=6.02e+02 |g_param|=1.95e+05 loss=4.0877e+00 ppl=59.60
Validation - loss=3.5902e+00 ppl=36.24 best_loss=3.6621e+00 best_ppl=38.94
Epoch 11 - |param|=6.02e+02 |g_param|=1.71e+05 loss=3.8371e+00 ppl=46.39
Validation - loss=3.4040e+00 ppl=30.08 best_loss=3.5902e+00 best_ppl=36.24
Epoch 12 - |param|=6.02e+02 |g_param|=1.54e+05 loss=3.7325e+00 ppl=41.78
Validation - loss=3.2666e+00 ppl=26.22 best_loss=3.4040e+00 best_ppl=30.08
Epoch 13 - |param|=6.03e+02 |g_param|=1.43e+05 loss=3.5034e+00 ppl=33.23
Validation - loss=3.1724e+00 ppl=23.86 best_loss=3.2666e+00 best_ppl=26.22
Epoch 14 - |param|=6.03e+02 |g_param|=1.43e+05 loss=3.4281e+00 ppl=30.82
Validation - loss=3.0765e+00 ppl=21.68 best_loss=3.1724e+00 best_ppl=23.86
Epoch 15 - |param|=6.04e+02 |g_param|=1.35e+05 loss=3.3434e+00 ppl=28.32
Validation - loss=3.0032e+00 ppl=20.15 best_loss=3.0765e+00 best_ppl=21.68
Epoch 16 - |param|=6.04e+02 |g_param|=1.43e+05 loss=3.3037e+00 ppl=27.21
Validation - loss=2.9577e+00 ppl=19.25 best_loss=3.0032e+00 best_ppl=20.15
Epoch 17 - |param|=6.04e+02 |g_param|=1.44e+05 loss=3.2829e+00 ppl=26.65
Validation - loss=2.9042e+00 ppl=18.25 best_loss=2.9577e+00 best_ppl=19.25
Epoch 18 - |param|=6.05e+02 |g_param|=1.47e+05 loss=3.1948e+00 ppl=24.41
Validation - loss=2.8708e+00 ppl=17.65 best_loss=2.9042e+00 best_ppl=18.25
Epoch 19 - |param|=6.05e+02 |g_param|=1.41e+05 loss=3.1317e+00 ppl=22.91
Validation - loss=2.8351e+00 ppl=17.03 best_loss=2.8708e+00 best_ppl=17.65
Epoch 20 - |param|=6.06e+02 |g_param|=1.49e+05 loss=3.0803e+00 ppl=21.76
Validation - loss=2.7945e+00 ppl=16.35 best_loss=2.8351e+00 best_ppl=17.03
Epoch 21 - |param|=6.06e+02 |g_param|=1.45e+05 loss=3.0569e+00 ppl=21.26
Validation - loss=2.7504e+00 ppl=15.65 best_loss=2.7945e+00 best_ppl=16.35
Epoch 22 - |param|=6.07e+02 |g_param|=1.61e+05 loss=2.9916e+00 ppl=19.92
Validation - loss=2.7487e+00 ppl=15.62 best_loss=2.7504e+00 best_ppl=15.65
Epoch 23 - |param|=6.07e+02 |g_param|=1.52e+05 loss=2.9387e+00 ppl=18.89
Validation - loss=2.7238e+00 ppl=15.24 best_loss=2.7487e+00 best_ppl=15.62
Epoch 24 - |param|=6.08e+02 |g_param|=1.60e+05 loss=2.9536e+00 ppl=19.17
Validation - loss=2.6828e+00 ppl=14.63 best_loss=2.7238e+00 best_ppl=15.24
Epoch 25 - |param|=6.08e+02 |g_param|=1.54e+05 loss=2.8706e+00 ppl=17.65
Validation - loss=2.6672e+00 ppl=14.40 best_loss=2.6828e+00 best_ppl=14.63
Epoch 26 - |param|=6.09e+02 |g_param|=1.60e+05 loss=2.7852e+00 ppl=16.20
Validation - loss=2.6303e+00 ppl=13.88 best_loss=2.6672e+00 best_ppl=14.40
Epoch 27 - |param|=6.09e+02 |g_param|=1.53e+05 loss=2.8088e+00 ppl=16.59
Validation - loss=2.6205e+00 ppl=13.74 best_loss=2.6303e+00 best_ppl=13.88
Epoch 28 - |param|=6.10e+02 |g_param|=1.66e+05 loss=2.7269e+00 ppl=15.28
Validation - loss=2.5753e+00 ppl=13.13 best_loss=2.6205e+00 best_ppl=13.74
Epoch 29 - |param|=6.10e+02 |g_param|=1.80e+05 loss=2.8036e+00 ppl=16.50
Validation - loss=2.5717e+00 ppl=13.09 best_loss=2.5753e+00 best_ppl=13.13
Epoch 30 - |param|=6.11e+02 |g_param|=1.76e+05 loss=2.6861e+00 ppl=14.67
Validation - loss=2.5330e+00 ppl=12.59 best_loss=2.5717e+00 best_ppl=13.09
bkmy, seq2seq-baseline training start for 40 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-40epoch/seq-model-bkmy.pth',
    'n_epochs': 40,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.26e+05 loss=4.7678e+00 ppl=117.66
Validation - loss=3.9860e+00 ppl=53.84 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.00e+02 |g_param|=3.70e+05 loss=4.3304e+00 ppl=75.97
Validation - loss=3.8507e+00 ppl=47.02 best_loss=3.9860e+00 best_ppl=53.84
Epoch 3 - |param|=6.00e+02 |g_param|=2.89e+05 loss=4.2082e+00 ppl=67.23
Validation - loss=3.7892e+00 ppl=44.22 best_loss=3.8507e+00 best_ppl=47.02
Epoch 4 - |param|=6.00e+02 |g_param|=1.94e+05 loss=4.1897e+00 ppl=66.01
Validation - loss=3.7654e+00 ppl=43.18 best_loss=3.7892e+00 best_ppl=44.22
Epoch 5 - |param|=6.00e+02 |g_param|=1.99e+05 loss=4.2190e+00 ppl=67.97
Validation - loss=3.7288e+00 ppl=41.63 best_loss=3.7654e+00 best_ppl=43.18
Epoch 6 - |param|=6.01e+02 |g_param|=2.09e+05 loss=4.2094e+00 ppl=67.32
Validation - loss=3.7103e+00 ppl=40.87 best_loss=3.7288e+00 best_ppl=41.63
Epoch 7 - |param|=6.01e+02 |g_param|=1.84e+05 loss=4.1909e+00 ppl=66.08
Validation - loss=3.6931e+00 ppl=40.17 best_loss=3.7103e+00 best_ppl=40.87
Epoch 8 - |param|=6.01e+02 |g_param|=2.07e+05 loss=4.0883e+00 ppl=59.64
Validation - loss=3.6709e+00 ppl=39.29 best_loss=3.6931e+00 best_ppl=40.17
Epoch 9 - |param|=6.02e+02 |g_param|=2.06e+05 loss=4.0533e+00 ppl=57.59
Validation - loss=3.6156e+00 ppl=37.18 best_loss=3.6709e+00 best_ppl=39.29
Epoch 10 - |param|=6.02e+02 |g_param|=1.57e+05 loss=3.9351e+00 ppl=51.17
Validation - loss=3.3933e+00 ppl=29.76 best_loss=3.6156e+00 best_ppl=37.18
Epoch 11 - |param|=6.02e+02 |g_param|=1.35e+05 loss=3.6036e+00 ppl=36.73
Validation - loss=3.2417e+00 ppl=25.58 best_loss=3.3933e+00 best_ppl=29.76
Epoch 12 - |param|=6.03e+02 |g_param|=1.45e+05 loss=3.5781e+00 ppl=35.81
Validation - loss=3.1380e+00 ppl=23.06 best_loss=3.2417e+00 best_ppl=25.58
Epoch 13 - |param|=6.03e+02 |g_param|=1.49e+05 loss=3.4171e+00 ppl=30.48
Validation - loss=3.0772e+00 ppl=21.70 best_loss=3.1380e+00 best_ppl=23.06
Epoch 14 - |param|=6.04e+02 |g_param|=1.54e+05 loss=3.3606e+00 ppl=28.81
Validation - loss=3.0251e+00 ppl=20.60 best_loss=3.0772e+00 best_ppl=21.70
Epoch 15 - |param|=6.04e+02 |g_param|=1.31e+05 loss=3.2705e+00 ppl=26.33
Validation - loss=2.9718e+00 ppl=19.53 best_loss=3.0251e+00 best_ppl=20.60
Epoch 16 - |param|=6.05e+02 |g_param|=1.38e+05 loss=3.2170e+00 ppl=24.95
Validation - loss=2.9129e+00 ppl=18.41 best_loss=2.9718e+00 best_ppl=19.53
Epoch 17 - |param|=6.05e+02 |g_param|=1.48e+05 loss=3.2078e+00 ppl=24.73
Validation - loss=2.9247e+00 ppl=18.63 best_loss=2.9129e+00 best_ppl=18.41
Epoch 18 - |param|=6.06e+02 |g_param|=1.50e+05 loss=3.2249e+00 ppl=25.15
Validation - loss=2.8449e+00 ppl=17.20 best_loss=2.9129e+00 best_ppl=18.41
Epoch 19 - |param|=6.06e+02 |g_param|=1.33e+05 loss=3.0763e+00 ppl=21.68
Validation - loss=2.8073e+00 ppl=16.56 best_loss=2.8449e+00 best_ppl=17.20
Epoch 20 - |param|=6.07e+02 |g_param|=1.58e+05 loss=3.0494e+00 ppl=21.10
Validation - loss=2.7844e+00 ppl=16.19 best_loss=2.8073e+00 best_ppl=16.56
Epoch 21 - |param|=6.07e+02 |g_param|=1.47e+05 loss=3.0196e+00 ppl=20.48
Validation - loss=2.7380e+00 ppl=15.46 best_loss=2.7844e+00 best_ppl=16.19
Epoch 22 - |param|=6.08e+02 |g_param|=1.53e+05 loss=2.9153e+00 ppl=18.45
Validation - loss=2.7427e+00 ppl=15.53 best_loss=2.7380e+00 best_ppl=15.46
Epoch 23 - |param|=6.08e+02 |g_param|=1.61e+05 loss=2.9293e+00 ppl=18.71
Validation - loss=2.7314e+00 ppl=15.35 best_loss=2.7380e+00 best_ppl=15.46
Epoch 24 - |param|=6.09e+02 |g_param|=1.66e+05 loss=2.9815e+00 ppl=19.72
Validation - loss=2.6582e+00 ppl=14.27 best_loss=2.7314e+00 best_ppl=15.35
Epoch 25 - |param|=6.09e+02 |g_param|=1.54e+05 loss=2.7978e+00 ppl=16.41
Validation - loss=2.6376e+00 ppl=13.98 best_loss=2.6582e+00 best_ppl=14.27
Epoch 26 - |param|=6.10e+02 |g_param|=1.62e+05 loss=2.8220e+00 ppl=16.81
Validation - loss=2.6545e+00 ppl=14.22 best_loss=2.6376e+00 best_ppl=13.98
Epoch 27 - |param|=6.10e+02 |g_param|=1.67e+05 loss=2.7572e+00 ppl=15.76
Validation - loss=2.6047e+00 ppl=13.53 best_loss=2.6376e+00 best_ppl=13.98
Epoch 28 - |param|=6.11e+02 |g_param|=1.65e+05 loss=2.7275e+00 ppl=15.29
Validation - loss=2.6034e+00 ppl=13.51 best_loss=2.6047e+00 best_ppl=13.53
Epoch 29 - |param|=6.11e+02 |g_param|=1.72e+05 loss=2.6730e+00 ppl=14.48
Validation - loss=2.5936e+00 ppl=13.38 best_loss=2.6034e+00 best_ppl=13.51
Epoch 30 - |param|=6.12e+02 |g_param|=1.77e+05 loss=2.6218e+00 ppl=13.76
Validation - loss=2.5937e+00 ppl=13.38 best_loss=2.5936e+00 best_ppl=13.38
Epoch 31 - |param|=6.12e+02 |g_param|=1.73e+05 loss=2.6750e+00 ppl=14.51
Validation - loss=2.5682e+00 ppl=13.04 best_loss=2.5936e+00 best_ppl=13.38
Epoch 32 - |param|=6.12e+02 |g_param|=1.71e+05 loss=2.5735e+00 ppl=13.11
Validation - loss=2.5351e+00 ppl=12.62 best_loss=2.5682e+00 best_ppl=13.04
Epoch 33 - |param|=6.13e+02 |g_param|=1.90e+05 loss=2.4930e+00 ppl=12.10
Validation - loss=2.5331e+00 ppl=12.59 best_loss=2.5351e+00 best_ppl=12.62
Epoch 34 - |param|=6.13e+02 |g_param|=1.91e+05 loss=2.5234e+00 ppl=12.47
Validation - loss=2.5377e+00 ppl=12.65 best_loss=2.5331e+00 best_ppl=12.59
Epoch 35 - |param|=6.14e+02 |g_param|=1.81e+05 loss=2.4651e+00 ppl=11.76
Validation - loss=2.5417e+00 ppl=12.70 best_loss=2.5331e+00 best_ppl=12.59
Epoch 36 - |param|=6.14e+02 |g_param|=3.48e+05 loss=2.4590e+00 ppl=11.69
Validation - loss=2.5192e+00 ppl=12.42 best_loss=2.5331e+00 best_ppl=12.59
Epoch 37 - |param|=6.15e+02 |g_param|=3.71e+05 loss=2.4368e+00 ppl=11.44
Validation - loss=2.5177e+00 ppl=12.40 best_loss=2.5192e+00 best_ppl=12.42
Epoch 38 - |param|=6.15e+02 |g_param|=3.83e+05 loss=2.3810e+00 ppl=10.82
Validation - loss=2.5313e+00 ppl=12.57 best_loss=2.5177e+00 best_ppl=12.40
Epoch 39 - |param|=6.16e+02 |g_param|=3.72e+05 loss=2.3495e+00 ppl=10.48
Validation - loss=2.5090e+00 ppl=12.29 best_loss=2.5177e+00 best_ppl=12.40
Epoch 40 - |param|=6.16e+02 |g_param|=3.92e+05 loss=2.3745e+00 ppl=10.75
Validation - loss=2.4814e+00 ppl=11.96 best_loss=2.5090e+00 best_ppl=12.29
bkmy, seq2seq-baseline training start for 50 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-50epoch/seq-model-bkmy.pth',
    'n_epochs': 50,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.49e+05 loss=4.7804e+00 ppl=119.15
Validation - loss=3.9855e+00 ppl=53.81 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.00e+02 |g_param|=3.73e+05 loss=4.3567e+00 ppl=78.00
Validation - loss=3.8301e+00 ppl=46.07 best_loss=3.9855e+00 best_ppl=53.81
Epoch 3 - |param|=6.00e+02 |g_param|=3.68e+05 loss=4.2041e+00 ppl=66.96
Validation - loss=3.7842e+00 ppl=44.00 best_loss=3.8301e+00 best_ppl=46.07
Epoch 4 - |param|=6.00e+02 |g_param|=2.62e+05 loss=4.2598e+00 ppl=70.80
Validation - loss=3.7934e+00 ppl=44.41 best_loss=3.7842e+00 best_ppl=44.00
Epoch 5 - |param|=6.00e+02 |g_param|=2.08e+05 loss=4.2150e+00 ppl=67.69
Validation - loss=3.7489e+00 ppl=42.47 best_loss=3.7842e+00 best_ppl=44.00
Epoch 6 - |param|=6.00e+02 |g_param|=2.07e+05 loss=4.2029e+00 ppl=66.88
Validation - loss=3.7393e+00 ppl=42.07 best_loss=3.7489e+00 best_ppl=42.47
Epoch 7 - |param|=6.00e+02 |g_param|=1.91e+05 loss=4.1079e+00 ppl=60.82
Validation - loss=3.6880e+00 ppl=39.97 best_loss=3.7393e+00 best_ppl=42.07
Epoch 8 - |param|=6.01e+02 |g_param|=1.92e+05 loss=4.1282e+00 ppl=62.06
Validation - loss=3.6396e+00 ppl=38.08 best_loss=3.6880e+00 best_ppl=39.97
Epoch 9 - |param|=6.01e+02 |g_param|=1.84e+05 loss=4.0086e+00 ppl=55.07
Validation - loss=3.5989e+00 ppl=36.56 best_loss=3.6396e+00 best_ppl=38.08
Epoch 10 - |param|=6.01e+02 |g_param|=1.57e+05 loss=3.8358e+00 ppl=46.33
Validation - loss=3.3923e+00 ppl=29.73 best_loss=3.5989e+00 best_ppl=36.56
Epoch 11 - |param|=6.02e+02 |g_param|=1.43e+05 loss=3.6376e+00 ppl=38.00
Validation - loss=3.2356e+00 ppl=25.42 best_loss=3.3923e+00 best_ppl=29.73
Epoch 12 - |param|=6.02e+02 |g_param|=1.53e+05 loss=3.5204e+00 ppl=33.80
Validation - loss=3.1393e+00 ppl=23.09 best_loss=3.2356e+00 best_ppl=25.42
Epoch 13 - |param|=6.02e+02 |g_param|=1.52e+05 loss=3.5105e+00 ppl=33.46
Validation - loss=3.0796e+00 ppl=21.75 best_loss=3.1393e+00 best_ppl=23.09
Epoch 14 - |param|=6.03e+02 |g_param|=1.46e+05 loss=3.4439e+00 ppl=31.31
Validation - loss=3.0209e+00 ppl=20.51 best_loss=3.0796e+00 best_ppl=21.75
Epoch 15 - |param|=6.03e+02 |g_param|=1.44e+05 loss=3.4151e+00 ppl=30.42
Validation - loss=2.9882e+00 ppl=19.85 best_loss=3.0209e+00 best_ppl=20.51
Epoch 16 - |param|=6.04e+02 |g_param|=1.56e+05 loss=3.2333e+00 ppl=25.36
Validation - loss=2.9481e+00 ppl=19.07 best_loss=2.9882e+00 best_ppl=19.85
Epoch 17 - |param|=6.04e+02 |g_param|=1.46e+05 loss=3.2726e+00 ppl=26.38
Validation - loss=2.8819e+00 ppl=17.85 best_loss=2.9481e+00 best_ppl=19.07
Epoch 18 - |param|=6.05e+02 |g_param|=1.51e+05 loss=3.1526e+00 ppl=23.40
Validation - loss=2.8399e+00 ppl=17.11 best_loss=2.8819e+00 best_ppl=17.85
Epoch 19 - |param|=6.05e+02 |g_param|=1.47e+05 loss=3.0902e+00 ppl=21.98
Validation - loss=2.7956e+00 ppl=16.37 best_loss=2.8399e+00 best_ppl=17.11
Epoch 20 - |param|=6.06e+02 |g_param|=1.62e+05 loss=3.0512e+00 ppl=21.14
Validation - loss=2.8075e+00 ppl=16.57 best_loss=2.7956e+00 best_ppl=16.37
Epoch 21 - |param|=6.06e+02 |g_param|=1.57e+05 loss=3.0885e+00 ppl=21.94
Validation - loss=2.7610e+00 ppl=15.82 best_loss=2.7956e+00 best_ppl=16.37
Epoch 22 - |param|=6.07e+02 |g_param|=1.59e+05 loss=2.9616e+00 ppl=19.33
Validation - loss=2.7190e+00 ppl=15.16 best_loss=2.7610e+00 best_ppl=15.82
Epoch 23 - |param|=6.07e+02 |g_param|=1.54e+05 loss=2.9229e+00 ppl=18.60
Validation - loss=2.7023e+00 ppl=14.91 best_loss=2.7190e+00 best_ppl=15.16
Epoch 24 - |param|=6.08e+02 |g_param|=1.82e+05 loss=2.8933e+00 ppl=18.05
Validation - loss=2.6615e+00 ppl=14.32 best_loss=2.7023e+00 best_ppl=14.91
Epoch 25 - |param|=6.08e+02 |g_param|=1.72e+05 loss=2.8835e+00 ppl=17.88
Validation - loss=2.6768e+00 ppl=14.54 best_loss=2.6615e+00 best_ppl=14.32
Epoch 26 - |param|=6.09e+02 |g_param|=1.65e+05 loss=2.8176e+00 ppl=16.74
Validation - loss=2.6336e+00 ppl=13.92 best_loss=2.6615e+00 best_ppl=14.32
Epoch 27 - |param|=6.09e+02 |g_param|=1.59e+05 loss=2.8115e+00 ppl=16.63
Validation - loss=2.6070e+00 ppl=13.56 best_loss=2.6336e+00 best_ppl=13.92
Epoch 28 - |param|=6.10e+02 |g_param|=1.82e+05 loss=2.7470e+00 ppl=15.60
Validation - loss=2.6430e+00 ppl=14.06 best_loss=2.6070e+00 best_ppl=13.56
Epoch 29 - |param|=6.10e+02 |g_param|=1.67e+05 loss=2.6974e+00 ppl=14.84
Validation - loss=2.5798e+00 ppl=13.19 best_loss=2.6070e+00 best_ppl=13.56
Epoch 30 - |param|=6.11e+02 |g_param|=2.10e+05 loss=2.6932e+00 ppl=14.78
Validation - loss=2.5846e+00 ppl=13.26 best_loss=2.5798e+00 best_ppl=13.19
Epoch 31 - |param|=6.11e+02 |g_param|=1.71e+05 loss=2.6224e+00 ppl=13.77
Validation - loss=2.5475e+00 ppl=12.78 best_loss=2.5798e+00 best_ppl=13.19
Epoch 32 - |param|=6.12e+02 |g_param|=1.84e+05 loss=2.5942e+00 ppl=13.39
Validation - loss=2.5473e+00 ppl=12.77 best_loss=2.5475e+00 best_ppl=12.78
Epoch 33 - |param|=6.12e+02 |g_param|=1.77e+05 loss=2.5767e+00 ppl=13.15
Validation - loss=2.5121e+00 ppl=12.33 best_loss=2.5473e+00 best_ppl=12.77
Epoch 34 - |param|=6.13e+02 |g_param|=1.85e+05 loss=2.5472e+00 ppl=12.77
Validation - loss=2.4991e+00 ppl=12.17 best_loss=2.5121e+00 best_ppl=12.33
Epoch 35 - |param|=6.13e+02 |g_param|=1.82e+05 loss=2.5136e+00 ppl=12.35
Validation - loss=2.5239e+00 ppl=12.48 best_loss=2.4991e+00 best_ppl=12.17
Epoch 36 - |param|=6.13e+02 |g_param|=2.31e+05 loss=2.5848e+00 ppl=13.26
Validation - loss=2.4913e+00 ppl=12.08 best_loss=2.4991e+00 best_ppl=12.17
Epoch 37 - |param|=6.14e+02 |g_param|=3.79e+05 loss=2.4602e+00 ppl=11.71
Validation - loss=2.4947e+00 ppl=12.12 best_loss=2.4913e+00 best_ppl=12.08
Epoch 38 - |param|=6.14e+02 |g_param|=4.04e+05 loss=2.4126e+00 ppl=11.16
Validation - loss=2.4725e+00 ppl=11.85 best_loss=2.4913e+00 best_ppl=12.08
Epoch 39 - |param|=6.15e+02 |g_param|=3.75e+05 loss=2.3622e+00 ppl=10.61
Validation - loss=2.4638e+00 ppl=11.75 best_loss=2.4725e+00 best_ppl=11.85
Epoch 40 - |param|=6.15e+02 |g_param|=4.15e+05 loss=2.3405e+00 ppl=10.39
Validation - loss=2.4758e+00 ppl=11.89 best_loss=2.4638e+00 best_ppl=11.75
Epoch 41 - |param|=6.16e+02 |g_param|=4.03e+05 loss=2.2935e+00 ppl=9.91
Validation - loss=2.4560e+00 ppl=11.66 best_loss=2.4638e+00 best_ppl=11.75
Epoch 42 - |param|=6.16e+02 |g_param|=4.24e+05 loss=2.3485e+00 ppl=10.47
Validation - loss=2.4539e+00 ppl=11.63 best_loss=2.4560e+00 best_ppl=11.66
Epoch 43 - |param|=6.17e+02 |g_param|=3.99e+05 loss=2.2538e+00 ppl=9.52
Validation - loss=2.4393e+00 ppl=11.46 best_loss=2.4539e+00 best_ppl=11.63
Epoch 44 - |param|=6.17e+02 |g_param|=4.48e+05 loss=2.2736e+00 ppl=9.71
Validation - loss=2.4430e+00 ppl=11.51 best_loss=2.4393e+00 best_ppl=11.46
Epoch 45 - |param|=6.17e+02 |g_param|=4.08e+05 loss=2.3017e+00 ppl=9.99
Validation - loss=2.4436e+00 ppl=11.51 best_loss=2.4393e+00 best_ppl=11.46
Epoch 46 - |param|=6.18e+02 |g_param|=4.31e+05 loss=2.1880e+00 ppl=8.92
Validation - loss=2.4390e+00 ppl=11.46 best_loss=2.4393e+00 best_ppl=11.46
Epoch 47 - |param|=6.18e+02 |g_param|=4.44e+05 loss=2.1836e+00 ppl=8.88
Validation - loss=2.4438e+00 ppl=11.52 best_loss=2.4390e+00 best_ppl=11.46
Epoch 48 - |param|=6.19e+02 |g_param|=4.51e+05 loss=2.0900e+00 ppl=8.09
Validation - loss=2.4366e+00 ppl=11.43 best_loss=2.4390e+00 best_ppl=11.46
Epoch 49 - |param|=6.19e+02 |g_param|=4.51e+05 loss=2.0987e+00 ppl=8.16
Validation - loss=2.4297e+00 ppl=11.36 best_loss=2.4366e+00 best_ppl=11.43
Epoch 50 - |param|=6.20e+02 |g_param|=4.72e+05 loss=2.0811e+00 ppl=8.01
Validation - loss=2.4534e+00 ppl=11.63 best_loss=2.4297e+00 best_ppl=11.36
bkmy, seq2seq-baseline training start for 60 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-60epoch/seq-model-bkmy.pth',
    'n_epochs': 60,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
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
Epoch 1 - |param|=6.01e+02 |g_param|=3.50e+05 loss=4.7428e+00 ppl=114.76
Validation - loss=3.9303e+00 ppl=50.92 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.01e+02 |g_param|=4.38e+05 loss=4.3090e+00 ppl=74.36
Validation - loss=3.8039e+00 ppl=44.87 best_loss=3.9303e+00 best_ppl=50.92
Epoch 3 - |param|=6.01e+02 |g_param|=3.76e+05 loss=4.1675e+00 ppl=64.56
Validation - loss=3.7878e+00 ppl=44.16 best_loss=3.8039e+00 best_ppl=44.87
Epoch 4 - |param|=6.01e+02 |g_param|=2.22e+05 loss=4.2286e+00 ppl=68.62
Validation - loss=3.7644e+00 ppl=43.14 best_loss=3.7878e+00 best_ppl=44.16
Epoch 5 - |param|=6.01e+02 |g_param|=1.94e+05 loss=4.1744e+00 ppl=65.00
Validation - loss=3.7296e+00 ppl=41.66 best_loss=3.7644e+00 best_ppl=43.14
Epoch 6 - |param|=6.01e+02 |g_param|=2.06e+05 loss=4.1754e+00 ppl=65.07
Validation - loss=3.6995e+00 ppl=40.43 best_loss=3.7296e+00 best_ppl=41.66
Epoch 7 - |param|=6.02e+02 |g_param|=1.82e+05 loss=4.0577e+00 ppl=57.84
Validation - loss=3.6574e+00 ppl=38.76 best_loss=3.6995e+00 best_ppl=40.43
Epoch 8 - |param|=6.02e+02 |g_param|=1.95e+05 loss=4.0216e+00 ppl=55.79
Validation - loss=3.5750e+00 ppl=35.70 best_loss=3.6574e+00 best_ppl=38.76
Epoch 9 - |param|=6.03e+02 |g_param|=1.53e+05 loss=3.8877e+00 ppl=48.80
Validation - loss=3.3820e+00 ppl=29.43 best_loss=3.5750e+00 best_ppl=35.70
Epoch 10 - |param|=6.03e+02 |g_param|=1.64e+05 loss=3.6901e+00 ppl=40.05
Validation - loss=3.2177e+00 ppl=24.97 best_loss=3.3820e+00 best_ppl=29.43
Epoch 11 - |param|=6.03e+02 |g_param|=1.48e+05 loss=3.5191e+00 ppl=33.75
Validation - loss=3.1225e+00 ppl=22.70 best_loss=3.2177e+00 best_ppl=24.97
Epoch 12 - |param|=6.04e+02 |g_param|=1.62e+05 loss=3.4273e+00 ppl=30.79
Validation - loss=3.0721e+00 ppl=21.59 best_loss=3.1225e+00 best_ppl=22.70
Epoch 13 - |param|=6.04e+02 |g_param|=1.46e+05 loss=3.3396e+00 ppl=28.21
Validation - loss=2.9972e+00 ppl=20.03 best_loss=3.0721e+00 best_ppl=21.59
Epoch 14 - |param|=6.05e+02 |g_param|=1.47e+05 loss=3.3258e+00 ppl=27.82
Validation - loss=2.9425e+00 ppl=18.96 best_loss=2.9972e+00 best_ppl=20.03
Epoch 15 - |param|=6.05e+02 |g_param|=1.46e+05 loss=3.2220e+00 ppl=25.08
Validation - loss=2.8781e+00 ppl=17.78 best_loss=2.9425e+00 best_ppl=18.96
Epoch 16 - |param|=6.06e+02 |g_param|=1.45e+05 loss=3.2331e+00 ppl=25.36
Validation - loss=2.8293e+00 ppl=16.93 best_loss=2.8781e+00 best_ppl=17.78
Epoch 17 - |param|=6.06e+02 |g_param|=1.42e+05 loss=3.1143e+00 ppl=22.52
Validation - loss=2.7871e+00 ppl=16.23 best_loss=2.8293e+00 best_ppl=16.93
Epoch 18 - |param|=6.07e+02 |g_param|=1.64e+05 loss=3.1418e+00 ppl=23.15
Validation - loss=2.7461e+00 ppl=15.58 best_loss=2.7871e+00 best_ppl=16.23
Epoch 19 - |param|=6.07e+02 |g_param|=1.54e+05 loss=3.0729e+00 ppl=21.60
Validation - loss=2.7146e+00 ppl=15.10 best_loss=2.7461e+00 best_ppl=15.58
Epoch 20 - |param|=6.08e+02 |g_param|=1.72e+05 loss=3.0431e+00 ppl=20.97
Validation - loss=2.6798e+00 ppl=14.58 best_loss=2.7146e+00 best_ppl=15.10
Epoch 21 - |param|=6.08e+02 |g_param|=1.57e+05 loss=2.9330e+00 ppl=18.78
Validation - loss=2.6415e+00 ppl=14.03 best_loss=2.6798e+00 best_ppl=14.58
Epoch 22 - |param|=6.09e+02 |g_param|=1.63e+05 loss=2.8578e+00 ppl=17.42
Validation - loss=2.6114e+00 ppl=13.62 best_loss=2.6415e+00 best_ppl=14.03
Epoch 23 - |param|=6.09e+02 |g_param|=1.52e+05 loss=2.8148e+00 ppl=16.69
Validation - loss=2.5883e+00 ppl=13.31 best_loss=2.6114e+00 best_ppl=13.62
Epoch 24 - |param|=6.10e+02 |g_param|=1.63e+05 loss=2.7585e+00 ppl=15.78
Validation - loss=2.5530e+00 ppl=12.85 best_loss=2.5883e+00 best_ppl=13.31
Epoch 25 - |param|=6.10e+02 |g_param|=1.66e+05 loss=2.8177e+00 ppl=16.74
Validation - loss=2.5180e+00 ppl=12.40 best_loss=2.5530e+00 best_ppl=12.85
Epoch 26 - |param|=6.11e+02 |g_param|=1.72e+05 loss=2.7885e+00 ppl=16.26
Validation - loss=2.4975e+00 ppl=12.15 best_loss=2.5180e+00 best_ppl=12.40
Epoch 27 - |param|=6.11e+02 |g_param|=1.62e+05 loss=2.6335e+00 ppl=13.92
Validation - loss=2.4799e+00 ppl=11.94 best_loss=2.4975e+00 best_ppl=12.15
Epoch 28 - |param|=6.12e+02 |g_param|=1.74e+05 loss=2.6349e+00 ppl=13.94
Validation - loss=2.4706e+00 ppl=11.83 best_loss=2.4799e+00 best_ppl=11.94
Epoch 29 - |param|=6.12e+02 |g_param|=1.78e+05 loss=2.6218e+00 ppl=13.76
Validation - loss=2.4530e+00 ppl=11.62 best_loss=2.4706e+00 best_ppl=11.83
Epoch 30 - |param|=6.13e+02 |g_param|=1.76e+05 loss=2.5859e+00 ppl=13.28
Validation - loss=2.4473e+00 ppl=11.56 best_loss=2.4530e+00 best_ppl=11.62
Epoch 31 - |param|=6.13e+02 |g_param|=1.75e+05 loss=2.4839e+00 ppl=11.99
Validation - loss=2.4415e+00 ppl=11.49 best_loss=2.4473e+00 best_ppl=11.56
Epoch 32 - |param|=6.14e+02 |g_param|=1.81e+05 loss=2.4543e+00 ppl=11.64
Validation - loss=2.4252e+00 ppl=11.30 best_loss=2.4415e+00 best_ppl=11.49
Epoch 33 - |param|=6.14e+02 |g_param|=1.87e+05 loss=2.4573e+00 ppl=11.67
Validation - loss=2.4031e+00 ppl=11.06 best_loss=2.4252e+00 best_ppl=11.30
Epoch 34 - |param|=6.14e+02 |g_param|=2.00e+05 loss=2.4774e+00 ppl=11.91
Validation - loss=2.4063e+00 ppl=11.09 best_loss=2.4031e+00 best_ppl=11.06
Epoch 35 - |param|=6.15e+02 |g_param|=1.93e+05 loss=2.4502e+00 ppl=11.59
Validation - loss=2.3750e+00 ppl=10.75 best_loss=2.4031e+00 best_ppl=11.06
Epoch 36 - |param|=6.15e+02 |g_param|=2.72e+05 loss=2.3483e+00 ppl=10.47
Validation - loss=2.3838e+00 ppl=10.85 best_loss=2.3750e+00 best_ppl=10.75
Epoch 37 - |param|=6.16e+02 |g_param|=3.83e+05 loss=2.2996e+00 ppl=9.97
Validation - loss=2.3637e+00 ppl=10.63 best_loss=2.3750e+00 best_ppl=10.75
Epoch 38 - |param|=6.16e+02 |g_param|=4.04e+05 loss=2.3442e+00 ppl=10.42
Validation - loss=2.3890e+00 ppl=10.90 best_loss=2.3637e+00 best_ppl=10.63
Epoch 39 - |param|=6.17e+02 |g_param|=4.04e+05 loss=2.2518e+00 ppl=9.50
Validation - loss=2.3806e+00 ppl=10.81 best_loss=2.3637e+00 best_ppl=10.63
Epoch 40 - |param|=6.17e+02 |g_param|=4.03e+05 loss=2.3215e+00 ppl=10.19
Validation - loss=2.3372e+00 ppl=10.35 best_loss=2.3637e+00 best_ppl=10.63
Epoch 41 - |param|=6.18e+02 |g_param|=3.87e+05 loss=2.1963e+00 ppl=8.99
Validation - loss=2.3627e+00 ppl=10.62 best_loss=2.3372e+00 best_ppl=10.35
Epoch 42 - |param|=6.18e+02 |g_param|=4.00e+05 loss=2.1490e+00 ppl=8.58
Validation - loss=2.3647e+00 ppl=10.64 best_loss=2.3372e+00 best_ppl=10.35
Epoch 43 - |param|=6.19e+02 |g_param|=4.08e+05 loss=2.1256e+00 ppl=8.38
Validation - loss=2.3613e+00 ppl=10.60 best_loss=2.3372e+00 best_ppl=10.35
Epoch 44 - |param|=6.19e+02 |g_param|=4.33e+05 loss=2.1727e+00 ppl=8.78
Validation - loss=2.3748e+00 ppl=10.75 best_loss=2.3372e+00 best_ppl=10.35
Epoch 45 - |param|=6.20e+02 |g_param|=4.20e+05 loss=2.0939e+00 ppl=8.12
Validation - loss=2.3693e+00 ppl=10.69 best_loss=2.3372e+00 best_ppl=10.35
Epoch 46 - |param|=6.20e+02 |g_param|=4.55e+05 loss=2.1568e+00 ppl=8.64
Validation - loss=2.3606e+00 ppl=10.60 best_loss=2.3372e+00 best_ppl=10.35
Epoch 47 - |param|=6.20e+02 |g_param|=4.47e+05 loss=2.0547e+00 ppl=7.80
Validation - loss=2.3549e+00 ppl=10.54 best_loss=2.3372e+00 best_ppl=10.35
Epoch 48 - |param|=6.21e+02 |g_param|=4.70e+05 loss=2.0320e+00 ppl=7.63
Validation - loss=2.3579e+00 ppl=10.57 best_loss=2.3372e+00 best_ppl=10.35
Epoch 49 - |param|=6.21e+02 |g_param|=4.37e+05 loss=1.9862e+00 ppl=7.29
Validation - loss=2.3463e+00 ppl=10.45 best_loss=2.3372e+00 best_ppl=10.35
Epoch 50 - |param|=6.22e+02 |g_param|=4.60e+05 loss=2.0230e+00 ppl=7.56
Validation - loss=2.3468e+00 ppl=10.45 best_loss=2.3372e+00 best_ppl=10.35
Epoch 51 - |param|=6.22e+02 |g_param|=4.56e+05 loss=2.0123e+00 ppl=7.48
Validation - loss=2.3377e+00 ppl=10.36 best_loss=2.3372e+00 best_ppl=10.35
Epoch 52 - |param|=6.23e+02 |g_param|=4.64e+05 loss=1.9432e+00 ppl=6.98
Validation - loss=2.3602e+00 ppl=10.59 best_loss=2.3372e+00 best_ppl=10.35
Epoch 53 - |param|=6.23e+02 |g_param|=4.82e+05 loss=1.9907e+00 ppl=7.32
Validation - loss=2.3681e+00 ppl=10.68 best_loss=2.3372e+00 best_ppl=10.35
Epoch 54 - |param|=6.23e+02 |g_param|=4.72e+05 loss=1.9625e+00 ppl=7.12
Validation - loss=2.3672e+00 ppl=10.67 best_loss=2.3372e+00 best_ppl=10.35
Epoch 55 - |param|=6.24e+02 |g_param|=4.85e+05 loss=1.9950e+00 ppl=7.35
Validation - loss=2.3739e+00 ppl=10.74 best_loss=2.3372e+00 best_ppl=10.35
Epoch 56 - |param|=6.24e+02 |g_param|=4.65e+05 loss=1.8616e+00 ppl=6.43
Validation - loss=2.3675e+00 ppl=10.67 best_loss=2.3372e+00 best_ppl=10.35
Epoch 57 - |param|=6.25e+02 |g_param|=4.68e+05 loss=1.8483e+00 ppl=6.35
Validation - loss=2.3562e+00 ppl=10.55 best_loss=2.3372e+00 best_ppl=10.35
Epoch 58 - |param|=6.25e+02 |g_param|=5.09e+05 loss=1.8452e+00 ppl=6.33
Validation - loss=2.4093e+00 ppl=11.13 best_loss=2.3372e+00 best_ppl=10.35
Epoch 59 - |param|=6.26e+02 |g_param|=5.03e+05 loss=1.7908e+00 ppl=5.99
Validation - loss=2.3624e+00 ppl=10.62 best_loss=2.3372e+00 best_ppl=10.35
Epoch 60 - |param|=6.26e+02 |g_param|=4.83e+05 loss=1.7543e+00 ppl=5.78
Validation - loss=2.3715e+00 ppl=10.71 best_loss=2.3372e+00 best_ppl=10.35
bkmy, seq2seq-baseline training start for 70 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.pth',
    'n_epochs': 70,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
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
Epoch 1 - |param|=6.00e+02 |g_param|=2.34e+05 loss=4.7526e+00 ppl=115.89
Validation - loss=3.9725e+00 ppl=53.12 best_loss=inf best_ppl=inf
Epoch 2 - |param|=6.00e+02 |g_param|=2.03e+05 loss=4.2449e+00 ppl=69.75
Validation - loss=3.8145e+00 ppl=45.36 best_loss=3.9725e+00 best_ppl=53.12
Epoch 3 - |param|=6.00e+02 |g_param|=1.97e+05 loss=4.1685e+00 ppl=64.62
Validation - loss=3.7949e+00 ppl=44.47 best_loss=3.8145e+00 best_ppl=45.36
Epoch 4 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.1432e+00 ppl=63.00
Validation - loss=3.7877e+00 ppl=44.15 best_loss=3.7949e+00 best_ppl=44.47
Epoch 5 - |param|=6.00e+02 |g_param|=1.92e+05 loss=4.1479e+00 ppl=63.30
Validation - loss=3.7642e+00 ppl=43.13 best_loss=3.7877e+00 best_ppl=44.15
Epoch 6 - |param|=6.01e+02 |g_param|=2.03e+05 loss=4.1539e+00 ppl=63.68
Validation - loss=3.7653e+00 ppl=43.18 best_loss=3.7642e+00 best_ppl=43.13
Epoch 7 - |param|=6.01e+02 |g_param|=2.00e+05 loss=4.1428e+00 ppl=62.98
Validation - loss=3.7332e+00 ppl=41.81 best_loss=3.7642e+00 best_ppl=43.13
Epoch 8 - |param|=6.01e+02 |g_param|=1.86e+05 loss=4.0900e+00 ppl=59.74
Validation - loss=3.7278e+00 ppl=41.59 best_loss=3.7332e+00 best_ppl=41.81
Epoch 9 - |param|=6.01e+02 |g_param|=2.16e+05 loss=4.1818e+00 ppl=65.49
Validation - loss=3.7151e+00 ppl=41.06 best_loss=3.7278e+00 best_ppl=41.59
Epoch 10 - |param|=6.02e+02 |g_param|=2.03e+05 loss=4.0789e+00 ppl=59.08
Validation - loss=3.6509e+00 ppl=38.51 best_loss=3.7151e+00 best_ppl=41.06
Epoch 11 - |param|=6.02e+02 |g_param|=1.88e+05 loss=4.0612e+00 ppl=58.04
Validation - loss=3.5849e+00 ppl=36.05 best_loss=3.6509e+00 best_ppl=38.51
Epoch 12 - |param|=6.02e+02 |g_param|=1.62e+05 loss=3.8638e+00 ppl=47.65
Validation - loss=3.3608e+00 ppl=28.81 best_loss=3.5849e+00 best_ppl=36.05
Epoch 13 - |param|=6.03e+02 |g_param|=1.46e+05 loss=3.7770e+00 ppl=43.68
Validation - loss=3.2356e+00 ppl=25.42 best_loss=3.3608e+00 best_ppl=28.81
Epoch 14 - |param|=6.03e+02 |g_param|=1.39e+05 loss=3.5337e+00 ppl=34.25
Validation - loss=3.1693e+00 ppl=23.79 best_loss=3.2356e+00 best_ppl=25.42
Epoch 15 - |param|=6.04e+02 |g_param|=1.33e+05 loss=3.4623e+00 ppl=31.89
Validation - loss=3.1107e+00 ppl=22.44 best_loss=3.1693e+00 best_ppl=23.79
Epoch 16 - |param|=6.04e+02 |g_param|=1.40e+05 loss=3.3927e+00 ppl=29.75
Validation - loss=3.0488e+00 ppl=21.09 best_loss=3.1107e+00 best_ppl=22.44
Epoch 17 - |param|=6.05e+02 |g_param|=1.33e+05 loss=3.3143e+00 ppl=27.50
Validation - loss=2.9850e+00 ppl=19.79 best_loss=3.0488e+00 best_ppl=21.09
Epoch 18 - |param|=6.05e+02 |g_param|=1.48e+05 loss=3.2833e+00 ppl=26.66
Validation - loss=2.9400e+00 ppl=18.92 best_loss=2.9850e+00 best_ppl=19.79
Epoch 19 - |param|=6.06e+02 |g_param|=1.50e+05 loss=3.2770e+00 ppl=26.50
Validation - loss=2.8964e+00 ppl=18.11 best_loss=2.9400e+00 best_ppl=18.92
Epoch 20 - |param|=6.06e+02 |g_param|=1.38e+05 loss=3.1533e+00 ppl=23.41
Validation - loss=2.8500e+00 ppl=17.29 best_loss=2.8964e+00 best_ppl=18.11
Epoch 21 - |param|=6.07e+02 |g_param|=1.34e+05 loss=3.1187e+00 ppl=22.62
Validation - loss=2.7906e+00 ppl=16.29 best_loss=2.8500e+00 best_ppl=17.29
Epoch 22 - |param|=6.07e+02 |g_param|=1.48e+05 loss=3.0963e+00 ppl=22.12
Validation - loss=2.7741e+00 ppl=16.02 best_loss=2.7906e+00 best_ppl=16.29
Epoch 23 - |param|=6.08e+02 |g_param|=1.42e+05 loss=3.1021e+00 ppl=22.24
Validation - loss=2.7135e+00 ppl=15.08 best_loss=2.7741e+00 best_ppl=16.02
Epoch 24 - |param|=6.08e+02 |g_param|=1.51e+05 loss=2.9268e+00 ppl=18.67
Validation - loss=2.6713e+00 ppl=14.46 best_loss=2.7135e+00 best_ppl=15.08
Epoch 25 - |param|=6.09e+02 |g_param|=1.50e+05 loss=2.9304e+00 ppl=18.73
Validation - loss=2.6566e+00 ppl=14.25 best_loss=2.6713e+00 best_ppl=14.46
Epoch 26 - |param|=6.09e+02 |g_param|=1.56e+05 loss=2.9592e+00 ppl=19.28
Validation - loss=2.6187e+00 ppl=13.72 best_loss=2.6566e+00 best_ppl=14.25
Epoch 27 - |param|=6.10e+02 |g_param|=1.48e+05 loss=2.8155e+00 ppl=16.70
Validation - loss=2.5866e+00 ppl=13.28 best_loss=2.6187e+00 best_ppl=13.72
Epoch 28 - |param|=6.10e+02 |g_param|=1.57e+05 loss=2.7734e+00 ppl=16.01
Validation - loss=2.5666e+00 ppl=13.02 best_loss=2.5866e+00 best_ppl=13.28
Epoch 29 - |param|=6.11e+02 |g_param|=1.53e+05 loss=2.8031e+00 ppl=16.50
Validation - loss=2.5365e+00 ppl=12.64 best_loss=2.5666e+00 best_ppl=13.02
Epoch 30 - |param|=6.11e+02 |g_param|=1.69e+05 loss=2.7295e+00 ppl=15.33
Validation - loss=2.5086e+00 ppl=12.29 best_loss=2.5365e+00 best_ppl=12.64
Epoch 31 - |param|=6.11e+02 |g_param|=1.66e+05 loss=2.6866e+00 ppl=14.68
Validation - loss=2.4812e+00 ppl=11.96 best_loss=2.5086e+00 best_ppl=12.29
Epoch 32 - |param|=6.12e+02 |g_param|=1.68e+05 loss=2.6123e+00 ppl=13.63
Validation - loss=2.4462e+00 ppl=11.54 best_loss=2.4812e+00 best_ppl=11.96
Epoch 33 - |param|=6.12e+02 |g_param|=1.63e+05 loss=2.5846e+00 ppl=13.26
Validation - loss=2.4160e+00 ppl=11.20 best_loss=2.4462e+00 best_ppl=11.54
Epoch 34 - |param|=6.13e+02 |g_param|=3.32e+05 loss=2.6263e+00 ppl=13.82
Validation - loss=2.4020e+00 ppl=11.05 best_loss=2.4160e+00 best_ppl=11.20
Epoch 35 - |param|=6.13e+02 |g_param|=3.24e+05 loss=2.5072e+00 ppl=12.27
Validation - loss=2.3667e+00 ppl=10.66 best_loss=2.4020e+00 best_ppl=11.05
Epoch 36 - |param|=6.14e+02 |g_param|=3.42e+05 loss=2.4872e+00 ppl=12.03
Validation - loss=2.3724e+00 ppl=10.72 best_loss=2.3667e+00 best_ppl=10.66
Epoch 37 - |param|=6.14e+02 |g_param|=3.52e+05 loss=2.4504e+00 ppl=11.59
Validation - loss=2.3285e+00 ppl=10.26 best_loss=2.3667e+00 best_ppl=10.66
Epoch 38 - |param|=6.15e+02 |g_param|=3.87e+05 loss=2.4685e+00 ppl=11.80
Validation - loss=2.3106e+00 ppl=10.08 best_loss=2.3285e+00 best_ppl=10.26
Epoch 39 - |param|=6.15e+02 |g_param|=3.63e+05 loss=2.4875e+00 ppl=12.03
Validation - loss=2.3081e+00 ppl=10.06 best_loss=2.3106e+00 best_ppl=10.08
Epoch 40 - |param|=6.16e+02 |g_param|=3.77e+05 loss=2.4473e+00 ppl=11.56
Validation - loss=2.3102e+00 ppl=10.08 best_loss=2.3081e+00 best_ppl=10.06
Epoch 41 - |param|=6.16e+02 |g_param|=3.82e+05 loss=2.4025e+00 ppl=11.05
Validation - loss=2.2973e+00 ppl=9.95 best_loss=2.3081e+00 best_ppl=10.06
Epoch 42 - |param|=6.17e+02 |g_param|=3.79e+05 loss=2.2405e+00 ppl=9.40
Validation - loss=2.2576e+00 ppl=9.56 best_loss=2.2973e+00 best_ppl=9.95
Epoch 43 - |param|=6.17e+02 |g_param|=3.68e+05 loss=2.2515e+00 ppl=9.50
Validation - loss=2.2452e+00 ppl=9.44 best_loss=2.2576e+00 best_ppl=9.56
Epoch 44 - |param|=6.18e+02 |g_param|=3.94e+05 loss=2.2012e+00 ppl=9.04
Validation - loss=2.2426e+00 ppl=9.42 best_loss=2.2452e+00 best_ppl=9.44
Epoch 45 - |param|=6.18e+02 |g_param|=3.90e+05 loss=2.2155e+00 ppl=9.17
Validation - loss=2.2179e+00 ppl=9.19 best_loss=2.2426e+00 best_ppl=9.42
Epoch 46 - |param|=6.19e+02 |g_param|=3.98e+05 loss=2.1933e+00 ppl=8.96
Validation - loss=2.2043e+00 ppl=9.06 best_loss=2.2179e+00 best_ppl=9.19
Epoch 47 - |param|=6.19e+02 |g_param|=4.23e+05 loss=2.1949e+00 ppl=8.98
Validation - loss=2.2048e+00 ppl=9.07 best_loss=2.2043e+00 best_ppl=9.06
Epoch 48 - |param|=6.19e+02 |g_param|=4.18e+05 loss=2.0881e+00 ppl=8.07
Validation - loss=2.2028e+00 ppl=9.05 best_loss=2.2043e+00 best_ppl=9.06
Epoch 49 - |param|=6.20e+02 |g_param|=4.00e+05 loss=2.0712e+00 ppl=7.93
Validation - loss=2.1868e+00 ppl=8.91 best_loss=2.2028e+00 best_ppl=9.05
Epoch 50 - |param|=6.20e+02 |g_param|=4.68e+05 loss=2.1152e+00 ppl=8.29
Validation - loss=2.1664e+00 ppl=8.73 best_loss=2.1868e+00 best_ppl=8.91
Epoch 51 - |param|=6.21e+02 |g_param|=4.46e+05 loss=2.1043e+00 ppl=8.20
Validation - loss=2.1766e+00 ppl=8.82 best_loss=2.1664e+00 best_ppl=8.73
Epoch 52 - |param|=6.21e+02 |g_param|=4.34e+05 loss=2.0109e+00 ppl=7.47
Validation - loss=2.1415e+00 ppl=8.51 best_loss=2.1664e+00 best_ppl=8.73
Epoch 53 - |param|=6.22e+02 |g_param|=4.32e+05 loss=1.9358e+00 ppl=6.93
Validation - loss=2.1707e+00 ppl=8.76 best_loss=2.1415e+00 best_ppl=8.51
Epoch 54 - |param|=6.22e+02 |g_param|=4.33e+05 loss=1.9718e+00 ppl=7.18
Validation - loss=2.1432e+00 ppl=8.53 best_loss=2.1415e+00 best_ppl=8.51
Epoch 55 - |param|=6.23e+02 |g_param|=4.18e+05 loss=1.8842e+00 ppl=6.58
Validation - loss=2.1293e+00 ppl=8.41 best_loss=2.1415e+00 best_ppl=8.51
Epoch 56 - |param|=6.23e+02 |g_param|=4.51e+05 loss=1.8979e+00 ppl=6.67
Validation - loss=2.1295e+00 ppl=8.41 best_loss=2.1293e+00 best_ppl=8.41
Epoch 57 - |param|=6.23e+02 |g_param|=4.64e+05 loss=1.9497e+00 ppl=7.03
Validation - loss=2.1349e+00 ppl=8.46 best_loss=2.1293e+00 best_ppl=8.41
Epoch 58 - |param|=6.24e+02 |g_param|=4.69e+05 loss=1.8234e+00 ppl=6.19
Validation - loss=2.1280e+00 ppl=8.40 best_loss=2.1293e+00 best_ppl=8.41
Epoch 59 - |param|=6.24e+02 |g_param|=4.49e+05 loss=1.7958e+00 ppl=6.02
Validation - loss=2.1213e+00 ppl=8.34 best_loss=2.1280e+00 best_ppl=8.40
Epoch 60 - |param|=6.25e+02 |g_param|=4.69e+05 loss=1.8134e+00 ppl=6.13
Validation - loss=2.1103e+00 ppl=8.25 best_loss=2.1213e+00 best_ppl=8.34
Epoch 61 - |param|=6.25e+02 |g_param|=4.57e+05 loss=1.7411e+00 ppl=5.70
Validation - loss=2.0984e+00 ppl=8.15 best_loss=2.1103e+00 best_ppl=8.25
Epoch 62 - |param|=6.26e+02 |g_param|=5.23e+05 loss=1.7246e+00 ppl=5.61
Validation - loss=2.1191e+00 ppl=8.32 best_loss=2.0984e+00 best_ppl=8.15
Epoch 63 - |param|=6.26e+02 |g_param|=4.90e+05 loss=1.8184e+00 ppl=6.16
Validation - loss=2.1026e+00 ppl=8.19 best_loss=2.0984e+00 best_ppl=8.15
Epoch 64 - |param|=6.26e+02 |g_param|=4.95e+05 loss=1.7018e+00 ppl=5.48
Validation - loss=2.0887e+00 ppl=8.07 best_loss=2.0984e+00 best_ppl=8.15
Epoch 65 - |param|=6.27e+02 |g_param|=5.04e+05 loss=1.8368e+00 ppl=6.28
Validation - loss=2.1053e+00 ppl=8.21 best_loss=2.0887e+00 best_ppl=8.07
Epoch 66 - |param|=6.27e+02 |g_param|=7.45e+05 loss=1.6616e+00 ppl=5.27
Validation - loss=2.1118e+00 ppl=8.26 best_loss=2.0887e+00 best_ppl=8.07
Epoch 67 - |param|=6.28e+02 |g_param|=7.24e+05 loss=1.7125e+00 ppl=5.54
Validation - loss=2.0842e+00 ppl=8.04 best_loss=2.0887e+00 best_ppl=8.07
Epoch 68 - |param|=6.28e+02 |g_param|=5.11e+05 loss=1.7545e+00 ppl=5.78
Validation - loss=2.1153e+00 ppl=8.29 best_loss=2.0842e+00 best_ppl=8.04
Epoch 69 - |param|=6.28e+02 |g_param|=4.90e+05 loss=1.6176e+00 ppl=5.04
Validation - loss=2.0986e+00 ppl=8.15 best_loss=2.0842e+00 best_ppl=8.04
Epoch 70 - |param|=6.29e+02 |g_param|=4.97e+05 loss=1.5501e+00 ppl=4.71
Validation - loss=2.1237e+00 ppl=8.36 best_loss=2.0842e+00 best_ppl=8.04
```
