# Some Screen Outputs of RL-exp-for-mybk

## Seq2Seq Baseline Training Log (my-bk, bk-my)
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

## Seq2Seq-RL Training Log (my-bk, bk-my)

```
mybk, seq2seq-RL training start for 30 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/mybk-30epoch/seq-model-mybk.30.2.80-16.52.2.38-10.84.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/mybk-30epoch/seq-rl-model-mybk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 31
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 31,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'load_fn': './model/rl2/baseline/seq2seq/mybk-30epoch/seq-model-mybk.30.2.80-16.52.2.38-10.84.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/mybk-30epoch/seq-rl-model-mybk.pth',
    'n_epochs': 100,
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
Epoch 31 - |param|=6.14e+02 |g_param|=3.60e+05 loss=2.7029e+00 ppl=14.92
Validation - loss=2.3686e+00 ppl=10.68 best_loss=inf best_ppl=inf
Epoch 32 - |param|=6.14e+02 |g_param|=3.72e+05 loss=2.6680e+00 ppl=14.41
Validation - loss=2.3233e+00 ppl=10.21 best_loss=2.3686e+00 best_ppl=10.68
Epoch 33 - |param|=6.15e+02 |g_param|=3.77e+05 loss=2.5703e+00 ppl=13.07
Validation - loss=2.3081e+00 ppl=10.06 best_loss=2.3233e+00 best_ppl=10.21
Epoch 34 - |param|=6.15e+02 |g_param|=4.56e+05 loss=2.6214e+00 ppl=13.75
Validation - loss=2.2884e+00 ppl=9.86 best_loss=2.3081e+00 best_ppl=10.06
Epoch 35 - |param|=6.16e+02 |g_param|=3.84e+05 loss=2.4948e+00 ppl=12.12
Validation - loss=2.2512e+00 ppl=9.50 best_loss=2.2884e+00 best_ppl=9.86
Epoch 36 - |param|=6.16e+02 |g_param|=3.97e+05 loss=2.4535e+00 ppl=11.63
Validation - loss=2.2369e+00 ppl=9.36 best_loss=2.2512e+00 best_ppl=9.50
Epoch 37 - |param|=6.17e+02 |g_param|=3.91e+05 loss=2.4023e+00 ppl=11.05
Validation - loss=2.2166e+00 ppl=9.18 best_loss=2.2369e+00 best_ppl=9.36
Epoch 38 - |param|=6.17e+02 |g_param|=5.19e+05 loss=2.5035e+00 ppl=12.22
Validation - loss=2.2157e+00 ppl=9.17 best_loss=2.2166e+00 best_ppl=9.18
Epoch 39 - |param|=6.18e+02 |g_param|=4.16e+05 loss=2.3686e+00 ppl=10.68
Validation - loss=2.1848e+00 ppl=8.89 best_loss=2.2157e+00 best_ppl=9.17
Epoch 40 - |param|=6.18e+02 |g_param|=4.17e+05 loss=2.3522e+00 ppl=10.51
Validation - loss=2.1610e+00 ppl=8.68 best_loss=2.1848e+00 best_ppl=8.89
Epoch 41 - |param|=6.19e+02 |g_param|=4.18e+05 loss=2.3059e+00 ppl=10.03
Validation - loss=2.1490e+00 ppl=8.58 best_loss=2.1610e+00 best_ppl=8.68
Epoch 42 - |param|=6.19e+02 |g_param|=4.17e+05 loss=2.2649e+00 ppl=9.63
Validation - loss=2.1470e+00 ppl=8.56 best_loss=2.1490e+00 best_ppl=8.58
Epoch 43 - |param|=6.20e+02 |g_param|=4.04e+05 loss=2.1624e+00 ppl=8.69
Validation - loss=2.1399e+00 ppl=8.50 best_loss=2.1470e+00 best_ppl=8.56
Epoch 44 - |param|=6.20e+02 |g_param|=4.03e+05 loss=2.1527e+00 ppl=8.61
Validation - loss=2.1145e+00 ppl=8.29 best_loss=2.1399e+00 best_ppl=8.50
Epoch 45 - |param|=6.20e+02 |g_param|=4.18e+05 loss=2.0887e+00 ppl=8.07
Validation - loss=2.1054e+00 ppl=8.21 best_loss=2.1145e+00 best_ppl=8.29
Epoch 46 - |param|=6.21e+02 |g_param|=4.72e+05 loss=2.1054e+00 ppl=8.21
Validation - loss=2.1049e+00 ppl=8.21 best_loss=2.1054e+00 best_ppl=8.21
Epoch 47 - |param|=6.21e+02 |g_param|=4.74e+05 loss=2.1432e+00 ppl=8.53
Validation - loss=2.0940e+00 ppl=8.12 best_loss=2.1049e+00 best_ppl=8.21
Epoch 48 - |param|=6.22e+02 |g_param|=4.43e+05 loss=2.0150e+00 ppl=7.50
Validation - loss=2.0609e+00 ppl=7.85 best_loss=2.0940e+00 best_ppl=8.12
Epoch 49 - |param|=6.22e+02 |g_param|=4.61e+05 loss=2.1512e+00 ppl=8.59
Validation - loss=2.0683e+00 ppl=7.91 best_loss=2.0609e+00 best_ppl=7.85
Epoch 50 - |param|=6.23e+02 |g_param|=4.63e+05 loss=1.9844e+00 ppl=7.27
Validation - loss=2.0776e+00 ppl=7.99 best_loss=2.0609e+00 best_ppl=7.85
Epoch 51 - |param|=6.23e+02 |g_param|=4.97e+05 loss=2.0571e+00 ppl=7.82
Validation - loss=2.0552e+00 ppl=7.81 best_loss=2.0609e+00 best_ppl=7.85
Epoch 52 - |param|=6.24e+02 |g_param|=4.71e+05 loss=1.9417e+00 ppl=6.97
Validation - loss=2.0524e+00 ppl=7.79 best_loss=2.0552e+00 best_ppl=7.81
Epoch 53 - |param|=6.24e+02 |g_param|=4.72e+05 loss=1.9757e+00 ppl=7.21
Validation - loss=2.0262e+00 ppl=7.59 best_loss=2.0524e+00 best_ppl=7.79
Epoch 54 - |param|=6.25e+02 |g_param|=4.87e+05 loss=1.9797e+00 ppl=7.24
Validation - loss=2.0351e+00 ppl=7.65 best_loss=2.0262e+00 best_ppl=7.59
Epoch 55 - |param|=6.25e+02 |g_param|=4.56e+05 loss=1.9145e+00 ppl=6.78
Validation - loss=2.0066e+00 ppl=7.44 best_loss=2.0262e+00 best_ppl=7.59
Epoch 56 - |param|=6.25e+02 |g_param|=5.13e+05 loss=1.8554e+00 ppl=6.39
Validation - loss=2.0458e+00 ppl=7.74 best_loss=2.0066e+00 best_ppl=7.44
Epoch 57 - |param|=6.26e+02 |g_param|=4.81e+05 loss=1.8369e+00 ppl=6.28
Validation - loss=2.0365e+00 ppl=7.66 best_loss=2.0066e+00 best_ppl=7.44
Epoch 58 - |param|=6.26e+02 |g_param|=4.81e+05 loss=1.8185e+00 ppl=6.16
Validation - loss=2.0325e+00 ppl=7.63 best_loss=2.0066e+00 best_ppl=7.44
Epoch 59 - |param|=6.27e+02 |g_param|=4.92e+05 loss=1.8410e+00 ppl=6.30
Validation - loss=2.0594e+00 ppl=7.84 best_loss=2.0066e+00 best_ppl=7.44
Epoch 60 - |param|=6.27e+02 |g_param|=4.95e+05 loss=1.7983e+00 ppl=6.04
Validation - loss=2.0196e+00 ppl=7.53 best_loss=2.0066e+00 best_ppl=7.44
Epoch 61 - |param|=6.28e+02 |g_param|=5.42e+05 loss=1.8033e+00 ppl=6.07
Validation - loss=2.0303e+00 ppl=7.62 best_loss=2.0066e+00 best_ppl=7.44
Epoch 62 - |param|=6.28e+02 |g_param|=5.37e+05 loss=1.7841e+00 ppl=5.95
Validation - loss=2.0627e+00 ppl=7.87 best_loss=2.0066e+00 best_ppl=7.44
Epoch 63 - |param|=6.28e+02 |g_param|=7.22e+05 loss=1.8127e+00 ppl=6.13
Validation - loss=2.0029e+00 ppl=7.41 best_loss=2.0066e+00 best_ppl=7.44
Epoch 64 - |param|=6.29e+02 |g_param|=4.95e+05 loss=1.7040e+00 ppl=5.50
Validation - loss=2.0002e+00 ppl=7.39 best_loss=2.0029e+00 best_ppl=7.41
Epoch 65 - |param|=6.29e+02 |g_param|=5.07e+05 loss=1.6350e+00 ppl=5.13
Validation - loss=2.0362e+00 ppl=7.66 best_loss=2.0002e+00 best_ppl=7.39
Epoch 66 - |param|=6.30e+02 |g_param|=2.86e+05 loss=1.6661e+00 ppl=5.29
Validation - loss=2.0165e+00 ppl=7.51 best_loss=2.0002e+00 best_ppl=7.39
Epoch 67 - |param|=6.30e+02 |g_param|=2.68e+05 loss=1.7143e+00 ppl=5.55
Validation - loss=2.0188e+00 ppl=7.53 best_loss=2.0002e+00 best_ppl=7.39
Epoch 68 - |param|=6.30e+02 |g_param|=2.73e+05 loss=1.5977e+00 ppl=4.94
Validation - loss=1.9952e+00 ppl=7.35 best_loss=2.0002e+00 best_ppl=7.39
Epoch 69 - |param|=6.31e+02 |g_param|=2.65e+05 loss=1.6512e+00 ppl=5.21
Validation - loss=2.0176e+00 ppl=7.52 best_loss=1.9952e+00 best_ppl=7.35
Epoch 70 - |param|=6.31e+02 |g_param|=2.61e+05 loss=1.5987e+00 ppl=4.95
Validation - loss=2.0186e+00 ppl=7.53 best_loss=1.9952e+00 best_ppl=7.35
Epoch 71 - |param|=6.32e+02 |g_param|=2.53e+05 loss=1.5530e+00 ppl=4.73
Validation - loss=2.0504e+00 ppl=7.77 best_loss=1.9952e+00 best_ppl=7.35
Epoch 72 - |param|=6.32e+02 |g_param|=2.77e+05 loss=1.5471e+00 ppl=4.70
Validation - loss=2.0201e+00 ppl=7.54 best_loss=1.9952e+00 best_ppl=7.35
Epoch 73 - |param|=6.33e+02 |g_param|=2.79e+05 loss=1.5448e+00 ppl=4.69
Validation - loss=2.0212e+00 ppl=7.55 best_loss=1.9952e+00 best_ppl=7.35
Epoch 74 - |param|=6.33e+02 |g_param|=2.83e+05 loss=1.5015e+00 ppl=4.49
Validation - loss=2.0055e+00 ppl=7.43 best_loss=1.9952e+00 best_ppl=7.35
Epoch 75 - |param|=6.33e+02 |g_param|=2.69e+05 loss=1.5338e+00 ppl=4.64
Validation - loss=2.0210e+00 ppl=7.55 best_loss=1.9952e+00 best_ppl=7.35
Epoch 76 - |param|=6.34e+02 |g_param|=2.79e+05 loss=1.5031e+00 ppl=4.50
Validation - loss=2.0126e+00 ppl=7.48 best_loss=1.9952e+00 best_ppl=7.35
Epoch 77 - |param|=6.34e+02 |g_param|=2.69e+05 loss=1.5989e+00 ppl=4.95
Validation - loss=2.0291e+00 ppl=7.61 best_loss=1.9952e+00 best_ppl=7.35
Epoch 78 - |param|=6.34e+02 |g_param|=2.83e+05 loss=1.5925e+00 ppl=4.92
Validation - loss=2.0267e+00 ppl=7.59 best_loss=1.9952e+00 best_ppl=7.35
Epoch 79 - |param|=6.35e+02 |g_param|=2.87e+05 loss=1.4521e+00 ppl=4.27
Validation - loss=2.0732e+00 ppl=7.95 best_loss=1.9952e+00 best_ppl=7.35
Epoch 80 - |param|=6.35e+02 |g_param|=2.81e+05 loss=1.4982e+00 ppl=4.47
Validation - loss=2.0482e+00 ppl=7.75 best_loss=1.9952e+00 best_ppl=7.35
Epoch 81 - |param|=6.36e+02 |g_param|=2.70e+05 loss=1.3992e+00 ppl=4.05
Validation - loss=1.9994e+00 ppl=7.38 best_loss=1.9952e+00 best_ppl=7.35
Epoch 82 - |param|=6.36e+02 |g_param|=2.83e+05 loss=1.4042e+00 ppl=4.07
Validation - loss=1.9994e+00 ppl=7.38 best_loss=1.9952e+00 best_ppl=7.35
Epoch 83 - |param|=6.36e+02 |g_param|=2.69e+05 loss=1.4483e+00 ppl=4.26
Validation - loss=2.0470e+00 ppl=7.74 best_loss=1.9952e+00 best_ppl=7.35
Epoch 84 - |param|=6.37e+02 |g_param|=2.69e+05 loss=1.3784e+00 ppl=3.97
Validation - loss=2.0751e+00 ppl=7.97 best_loss=1.9952e+00 best_ppl=7.35
Epoch 85 - |param|=6.37e+02 |g_param|=2.74e+05 loss=1.4008e+00 ppl=4.06
Validation - loss=2.0540e+00 ppl=7.80 best_loss=1.9952e+00 best_ppl=7.35
Epoch 86 - |param|=6.38e+02 |g_param|=2.85e+05 loss=1.3665e+00 ppl=3.92
Validation - loss=2.0184e+00 ppl=7.53 best_loss=1.9952e+00 best_ppl=7.35
Epoch 87 - |param|=6.38e+02 |g_param|=3.24e+05 loss=1.3814e+00 ppl=3.98
Validation - loss=2.0366e+00 ppl=7.66 best_loss=1.9952e+00 best_ppl=7.35
Epoch 88 - |param|=6.38e+02 |g_param|=2.82e+05 loss=1.3254e+00 ppl=3.76
Validation - loss=2.0270e+00 ppl=7.59 best_loss=1.9952e+00 best_ppl=7.35
Epoch 89 - |param|=6.39e+02 |g_param|=2.73e+05 loss=1.3541e+00 ppl=3.87
Validation - loss=2.0636e+00 ppl=7.87 best_loss=1.9952e+00 best_ppl=7.35
Epoch 90 - |param|=6.39e+02 |g_param|=2.72e+05 loss=1.2541e+00 ppl=3.50
Validation - loss=2.0207e+00 ppl=7.54 best_loss=1.9952e+00 best_ppl=7.35
Epoch 91 - |param|=6.39e+02 |g_param|=2.86e+05 loss=1.3891e+00 ppl=4.01
Validation - loss=2.0839e+00 ppl=8.04 best_loss=1.9952e+00 best_ppl=7.35
Epoch 92 - |param|=6.40e+02 |g_param|=2.85e+05 loss=1.3081e+00 ppl=3.70
Validation - loss=2.0769e+00 ppl=7.98 best_loss=1.9952e+00 best_ppl=7.35
Epoch 93 - |param|=6.40e+02 |g_param|=2.80e+05 loss=1.2752e+00 ppl=3.58
Validation - loss=2.0512e+00 ppl=7.78 best_loss=1.9952e+00 best_ppl=7.35
Epoch 94 - |param|=6.40e+02 |g_param|=2.82e+05 loss=1.2097e+00 ppl=3.35
Validation - loss=2.0364e+00 ppl=7.66 best_loss=1.9952e+00 best_ppl=7.35
Epoch 95 - |param|=6.41e+02 |g_param|=2.79e+05 loss=1.2754e+00 ppl=3.58
Validation - loss=2.0561e+00 ppl=7.82 best_loss=1.9952e+00 best_ppl=7.35
Epoch 96 - |param|=6.41e+02 |g_param|=2.97e+05 loss=1.2075e+00 ppl=3.35
Validation - loss=2.0532e+00 ppl=7.79 best_loss=1.9952e+00 best_ppl=7.35
Epoch 97 - |param|=6.42e+02 |g_param|=2.81e+05 loss=1.2369e+00 ppl=3.44
Validation - loss=2.0921e+00 ppl=8.10 best_loss=1.9952e+00 best_ppl=7.35
Epoch 98 - |param|=6.42e+02 |g_param|=4.56e+05 loss=1.1808e+00 ppl=3.26
Validation - loss=2.1185e+00 ppl=8.32 best_loss=1.9952e+00 best_ppl=7.35
Epoch 99 - |param|=6.42e+02 |g_param|=5.40e+05 loss=1.1946e+00 ppl=3.30
Validation - loss=2.0573e+00 ppl=7.83 best_loss=1.9952e+00 best_ppl=7.35
Epoch 100 - |param|=6.43e+02 |g_param|=6.09e+05 loss=1.2394e+00 ppl=3.45
Validation - loss=2.0965e+00 ppl=8.14 best_loss=1.9952e+00 best_ppl=7.35
mybk, seq2seq-RL training start for 40 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/mybk-40epoch/seq-model-mybk.40.2.49-12.05.2.17-8.77.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/mybk-40epoch/seq-rl-model-mybk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 41
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 41,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'load_fn': './model/rl2/baseline/seq2seq/mybk-40epoch/seq-model-mybk.40.2.49-12.05.2.17-8.77.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/mybk-40epoch/seq-rl-model-mybk.pth',
    'n_epochs': 100,
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
Epoch 41 - |param|=6.17e+02 |g_param|=4.29e+05 loss=2.4002e+00 ppl=11.03
Validation - loss=2.2207e+00 ppl=9.21 best_loss=inf best_ppl=inf
Epoch 42 - |param|=6.17e+02 |g_param|=4.33e+05 loss=2.3692e+00 ppl=10.69
Validation - loss=2.1467e+00 ppl=8.56 best_loss=2.2207e+00 best_ppl=9.21
Epoch 43 - |param|=6.17e+02 |g_param|=4.21e+05 loss=2.2517e+00 ppl=9.50
Validation - loss=2.1509e+00 ppl=8.59 best_loss=2.1467e+00 best_ppl=8.56
Epoch 44 - |param|=6.18e+02 |g_param|=4.16e+05 loss=2.1498e+00 ppl=8.58
Validation - loss=2.1060e+00 ppl=8.22 best_loss=2.1467e+00 best_ppl=8.56
Epoch 45 - |param|=6.18e+02 |g_param|=4.21e+05 loss=2.2194e+00 ppl=9.20
Validation - loss=2.0905e+00 ppl=8.09 best_loss=2.1060e+00 best_ppl=8.22
Epoch 46 - |param|=6.19e+02 |g_param|=4.30e+05 loss=2.1209e+00 ppl=8.34
Validation - loss=2.0765e+00 ppl=7.98 best_loss=2.0905e+00 best_ppl=8.09
Epoch 47 - |param|=6.19e+02 |g_param|=4.28e+05 loss=2.1169e+00 ppl=8.31
Validation - loss=2.0953e+00 ppl=8.13 best_loss=2.0765e+00 best_ppl=7.98
Epoch 48 - |param|=6.20e+02 |g_param|=4.57e+05 loss=2.0652e+00 ppl=7.89
Validation - loss=2.0416e+00 ppl=7.70 best_loss=2.0765e+00 best_ppl=7.98
Epoch 49 - |param|=6.20e+02 |g_param|=4.45e+05 loss=2.0495e+00 ppl=7.76
Validation - loss=2.0558e+00 ppl=7.81 best_loss=2.0416e+00 best_ppl=7.70
Epoch 50 - |param|=6.21e+02 |g_param|=4.60e+05 loss=2.0282e+00 ppl=7.60
Validation - loss=2.0548e+00 ppl=7.81 best_loss=2.0416e+00 best_ppl=7.70
Epoch 51 - |param|=6.21e+02 |g_param|=4.62e+05 loss=2.0039e+00 ppl=7.42
Validation - loss=2.0147e+00 ppl=7.50 best_loss=2.0416e+00 best_ppl=7.70
Epoch 52 - |param|=6.22e+02 |g_param|=4.94e+05 loss=2.0030e+00 ppl=7.41
Validation - loss=2.0245e+00 ppl=7.57 best_loss=2.0147e+00 best_ppl=7.50
Epoch 53 - |param|=6.22e+02 |g_param|=5.03e+05 loss=2.1004e+00 ppl=8.17
Validation - loss=2.0078e+00 ppl=7.45 best_loss=2.0147e+00 best_ppl=7.50
Epoch 54 - |param|=6.23e+02 |g_param|=4.94e+05 loss=1.9432e+00 ppl=6.98
Validation - loss=2.0328e+00 ppl=7.64 best_loss=2.0078e+00 best_ppl=7.45
Epoch 55 - |param|=6.23e+02 |g_param|=4.58e+05 loss=1.9462e+00 ppl=7.00
Validation - loss=2.0328e+00 ppl=7.64 best_loss=2.0078e+00 best_ppl=7.45
Epoch 56 - |param|=6.23e+02 |g_param|=4.85e+05 loss=1.9070e+00 ppl=6.73
Validation - loss=1.9900e+00 ppl=7.32 best_loss=2.0078e+00 best_ppl=7.45
Epoch 57 - |param|=6.24e+02 |g_param|=4.86e+05 loss=1.9819e+00 ppl=7.26
Validation - loss=2.0479e+00 ppl=7.75 best_loss=1.9900e+00 best_ppl=7.32
Epoch 58 - |param|=6.24e+02 |g_param|=5.29e+05 loss=1.9111e+00 ppl=6.76
Validation - loss=2.0265e+00 ppl=7.59 best_loss=1.9900e+00 best_ppl=7.32
Epoch 59 - |param|=6.25e+02 |g_param|=4.83e+05 loss=1.8332e+00 ppl=6.25
Validation - loss=2.0231e+00 ppl=7.56 best_loss=1.9900e+00 best_ppl=7.32
Epoch 60 - |param|=6.25e+02 |g_param|=3.98e+05 loss=1.7693e+00 ppl=5.87
Validation - loss=2.0201e+00 ppl=7.54 best_loss=1.9900e+00 best_ppl=7.32
Epoch 61 - |param|=6.26e+02 |g_param|=2.46e+05 loss=1.8948e+00 ppl=6.65
Validation - loss=1.9976e+00 ppl=7.37 best_loss=1.9900e+00 best_ppl=7.32
Epoch 62 - |param|=6.26e+02 |g_param|=2.51e+05 loss=1.7807e+00 ppl=5.93
Validation - loss=1.9841e+00 ppl=7.27 best_loss=1.9900e+00 best_ppl=7.32
Epoch 63 - |param|=6.27e+02 |g_param|=2.60e+05 loss=1.7040e+00 ppl=5.50
Validation - loss=1.9759e+00 ppl=7.21 best_loss=1.9841e+00 best_ppl=7.27
Epoch 64 - |param|=6.27e+02 |g_param|=2.60e+05 loss=1.7013e+00 ppl=5.48
Validation - loss=2.0418e+00 ppl=7.70 best_loss=1.9759e+00 best_ppl=7.21
Epoch 65 - |param|=6.27e+02 |g_param|=2.65e+05 loss=1.7353e+00 ppl=5.67
Validation - loss=1.9997e+00 ppl=7.39 best_loss=1.9759e+00 best_ppl=7.21
Epoch 66 - |param|=6.28e+02 |g_param|=2.68e+05 loss=1.6911e+00 ppl=5.43
Validation - loss=2.0149e+00 ppl=7.50 best_loss=1.9759e+00 best_ppl=7.21
Epoch 67 - |param|=6.28e+02 |g_param|=2.48e+05 loss=1.7100e+00 ppl=5.53
Validation - loss=2.0059e+00 ppl=7.43 best_loss=1.9759e+00 best_ppl=7.21
Epoch 68 - |param|=6.29e+02 |g_param|=2.63e+05 loss=1.5974e+00 ppl=4.94
Validation - loss=2.0246e+00 ppl=7.57 best_loss=1.9759e+00 best_ppl=7.21
Epoch 69 - |param|=6.29e+02 |g_param|=2.62e+05 loss=1.6423e+00 ppl=5.17
Validation - loss=2.0044e+00 ppl=7.42 best_loss=1.9759e+00 best_ppl=7.21
Epoch 70 - |param|=6.30e+02 |g_param|=2.53e+05 loss=1.5986e+00 ppl=4.95
Validation - loss=1.9987e+00 ppl=7.38 best_loss=1.9759e+00 best_ppl=7.21
Epoch 71 - |param|=6.30e+02 |g_param|=2.49e+05 loss=1.6000e+00 ppl=4.95
Validation - loss=2.0046e+00 ppl=7.42 best_loss=1.9759e+00 best_ppl=7.21
Epoch 72 - |param|=6.30e+02 |g_param|=2.70e+05 loss=1.5453e+00 ppl=4.69
Validation - loss=2.0149e+00 ppl=7.50 best_loss=1.9759e+00 best_ppl=7.21
Epoch 73 - |param|=6.31e+02 |g_param|=2.79e+05 loss=1.5599e+00 ppl=4.76
Validation - loss=1.9987e+00 ppl=7.38 best_loss=1.9759e+00 best_ppl=7.21
Epoch 74 - |param|=6.31e+02 |g_param|=2.53e+05 loss=1.5039e+00 ppl=4.50
Validation - loss=2.0246e+00 ppl=7.57 best_loss=1.9759e+00 best_ppl=7.21
Epoch 75 - |param|=6.32e+02 |g_param|=2.50e+05 loss=1.4820e+00 ppl=4.40
Validation - loss=2.0048e+00 ppl=7.42 best_loss=1.9759e+00 best_ppl=7.21
Epoch 76 - |param|=6.32e+02 |g_param|=2.80e+05 loss=1.4956e+00 ppl=4.46
Validation - loss=2.0454e+00 ppl=7.73 best_loss=1.9759e+00 best_ppl=7.21
Epoch 77 - |param|=6.32e+02 |g_param|=2.64e+05 loss=1.5628e+00 ppl=4.77
Validation - loss=2.0055e+00 ppl=7.43 best_loss=1.9759e+00 best_ppl=7.21
Epoch 78 - |param|=6.33e+02 |g_param|=2.59e+05 loss=1.5020e+00 ppl=4.49
Validation - loss=1.9882e+00 ppl=7.30 best_loss=1.9759e+00 best_ppl=7.21
Epoch 79 - |param|=6.33e+02 |g_param|=2.58e+05 loss=1.4364e+00 ppl=4.21
Validation - loss=2.0363e+00 ppl=7.66 best_loss=1.9759e+00 best_ppl=7.21
Epoch 80 - |param|=6.34e+02 |g_param|=2.68e+05 loss=1.4688e+00 ppl=4.34
Validation - loss=2.0326e+00 ppl=7.63 best_loss=1.9759e+00 best_ppl=7.21
Epoch 81 - |param|=6.34e+02 |g_param|=2.63e+05 loss=1.4390e+00 ppl=4.22
Validation - loss=1.9984e+00 ppl=7.38 best_loss=1.9759e+00 best_ppl=7.21
Epoch 82 - |param|=6.34e+02 |g_param|=2.68e+05 loss=1.4342e+00 ppl=4.20
Validation - loss=2.0356e+00 ppl=7.66 best_loss=1.9759e+00 best_ppl=7.21
Epoch 83 - |param|=6.35e+02 |g_param|=2.80e+05 loss=1.3705e+00 ppl=3.94
Validation - loss=2.0449e+00 ppl=7.73 best_loss=1.9759e+00 best_ppl=7.21
Epoch 84 - |param|=6.35e+02 |g_param|=2.78e+05 loss=1.4431e+00 ppl=4.23
Validation - loss=2.0459e+00 ppl=7.74 best_loss=1.9759e+00 best_ppl=7.21
Epoch 85 - |param|=6.36e+02 |g_param|=2.68e+05 loss=1.3998e+00 ppl=4.05
Validation - loss=2.0178e+00 ppl=7.52 best_loss=1.9759e+00 best_ppl=7.21
Epoch 86 - |param|=6.36e+02 |g_param|=2.88e+05 loss=1.3317e+00 ppl=3.79
Validation - loss=2.0566e+00 ppl=7.82 best_loss=1.9759e+00 best_ppl=7.21
Epoch 87 - |param|=6.36e+02 |g_param|=2.72e+05 loss=1.3024e+00 ppl=3.68
Validation - loss=2.0354e+00 ppl=7.66 best_loss=1.9759e+00 best_ppl=7.21
Epoch 88 - |param|=6.37e+02 |g_param|=3.04e+05 loss=1.3609e+00 ppl=3.90
Validation - loss=2.0366e+00 ppl=7.66 best_loss=1.9759e+00 best_ppl=7.21
Epoch 89 - |param|=6.37e+02 |g_param|=2.71e+05 loss=1.3742e+00 ppl=3.95
Validation - loss=2.0918e+00 ppl=8.10 best_loss=1.9759e+00 best_ppl=7.21
Epoch 90 - |param|=6.37e+02 |g_param|=2.97e+05 loss=1.3408e+00 ppl=3.82
Validation - loss=2.0868e+00 ppl=8.06 best_loss=1.9759e+00 best_ppl=7.21
Epoch 91 - |param|=6.38e+02 |g_param|=2.89e+05 loss=1.3231e+00 ppl=3.76
Validation - loss=2.0470e+00 ppl=7.74 best_loss=1.9759e+00 best_ppl=7.21
Epoch 92 - |param|=6.38e+02 |g_param|=2.98e+05 loss=1.2818e+00 ppl=3.60
Validation - loss=2.0327e+00 ppl=7.63 best_loss=1.9759e+00 best_ppl=7.21
Epoch 93 - |param|=6.39e+02 |g_param|=5.30e+05 loss=1.3363e+00 ppl=3.81
Validation - loss=2.0603e+00 ppl=7.85 best_loss=1.9759e+00 best_ppl=7.21
Epoch 94 - |param|=6.39e+02 |g_param|=5.84e+05 loss=1.2433e+00 ppl=3.47
Validation - loss=2.1159e+00 ppl=8.30 best_loss=1.9759e+00 best_ppl=7.21
Epoch 95 - |param|=6.39e+02 |g_param|=5.54e+05 loss=1.2498e+00 ppl=3.49
Validation - loss=2.0273e+00 ppl=7.59 best_loss=1.9759e+00 best_ppl=7.21
Epoch 96 - |param|=6.40e+02 |g_param|=5.50e+05 loss=1.2657e+00 ppl=3.55
Validation - loss=2.0344e+00 ppl=7.65 best_loss=1.9759e+00 best_ppl=7.21
Epoch 97 - |param|=6.40e+02 |g_param|=5.59e+05 loss=1.2228e+00 ppl=3.40
Validation - loss=2.0792e+00 ppl=8.00 best_loss=1.9759e+00 best_ppl=7.21
Epoch 98 - |param|=6.41e+02 |g_param|=5.60e+05 loss=1.1913e+00 ppl=3.29
Validation - loss=2.0856e+00 ppl=8.05 best_loss=1.9759e+00 best_ppl=7.21
Epoch 99 - |param|=6.41e+02 |g_param|=6.11e+05 loss=1.2319e+00 ppl=3.43
Validation - loss=2.0502e+00 ppl=7.77 best_loss=1.9759e+00 best_ppl=7.21
Epoch 100 - |param|=6.41e+02 |g_param|=3.50e+05 loss=1.2183e+00 ppl=3.38
Validation - loss=2.1215e+00 ppl=8.34 best_loss=1.9759e+00 best_ppl=7.21
mybk, seq2seq-RL training start for 50 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/mybk-50epoch/seq-model-mybk.50.2.26-9.59.2.46-11.68.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/mybk-50epoch/seq-rl-model-mybk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 51
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 51,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'load_fn': './model/rl2/baseline/seq2seq/mybk-50epoch/seq-model-mybk.50.2.26-9.59.2.46-11.68.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/mybk-50epoch/seq-rl-model-mybk.pth',
    'n_epochs': 100,
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
Epoch 51 - |param|=6.21e+02 |g_param|=4.45e+05 loss=2.2152e+00 ppl=9.16
Validation - loss=2.4504e+00 ppl=11.59 best_loss=inf best_ppl=inf
Epoch 52 - |param|=6.22e+02 |g_param|=4.51e+05 loss=2.1141e+00 ppl=8.28
Validation - loss=2.4842e+00 ppl=11.99 best_loss=2.4504e+00 best_ppl=11.59
Epoch 53 - |param|=6.22e+02 |g_param|=4.43e+05 loss=2.1442e+00 ppl=8.53
Validation - loss=2.4941e+00 ppl=12.11 best_loss=2.4504e+00 best_ppl=11.59
Epoch 54 - |param|=6.23e+02 |g_param|=4.59e+05 loss=2.1808e+00 ppl=8.85
Validation - loss=2.4829e+00 ppl=11.98 best_loss=2.4504e+00 best_ppl=11.59
Epoch 55 - |param|=6.23e+02 |g_param|=4.65e+05 loss=2.1456e+00 ppl=8.55
Validation - loss=2.5210e+00 ppl=12.44 best_loss=2.4504e+00 best_ppl=11.59
Epoch 56 - |param|=6.23e+02 |g_param|=4.52e+05 loss=2.0402e+00 ppl=7.69
Validation - loss=2.5339e+00 ppl=12.60 best_loss=2.4504e+00 best_ppl=11.59
Epoch 57 - |param|=6.24e+02 |g_param|=4.69e+05 loss=2.0262e+00 ppl=7.59
Validation - loss=2.5142e+00 ppl=12.36 best_loss=2.4504e+00 best_ppl=11.59
Epoch 58 - |param|=6.24e+02 |g_param|=5.21e+05 loss=2.0739e+00 ppl=7.96
Validation - loss=2.5056e+00 ppl=12.25 best_loss=2.4504e+00 best_ppl=11.59
Epoch 59 - |param|=6.25e+02 |g_param|=4.65e+05 loss=2.0056e+00 ppl=7.43
Validation - loss=2.4926e+00 ppl=12.09 best_loss=2.4504e+00 best_ppl=11.59
Epoch 60 - |param|=6.25e+02 |g_param|=5.21e+05 loss=1.9924e+00 ppl=7.33
Validation - loss=2.4699e+00 ppl=11.82 best_loss=2.4504e+00 best_ppl=11.59
Epoch 61 - |param|=6.26e+02 |g_param|=4.93e+05 loss=1.9544e+00 ppl=7.06
Validation - loss=2.4856e+00 ppl=12.01 best_loss=2.4504e+00 best_ppl=11.59
Epoch 62 - |param|=6.26e+02 |g_param|=5.17e+05 loss=1.9162e+00 ppl=6.80
Validation - loss=2.4994e+00 ppl=12.17 best_loss=2.4504e+00 best_ppl=11.59
Epoch 63 - |param|=6.26e+02 |g_param|=4.84e+05 loss=1.9043e+00 ppl=6.71
Validation - loss=2.4952e+00 ppl=12.12 best_loss=2.4504e+00 best_ppl=11.59
Epoch 64 - |param|=6.27e+02 |g_param|=5.44e+05 loss=1.9415e+00 ppl=6.97
Validation - loss=2.4926e+00 ppl=12.09 best_loss=2.4504e+00 best_ppl=11.59
Epoch 65 - |param|=6.27e+02 |g_param|=4.88e+05 loss=1.8515e+00 ppl=6.37
Validation - loss=2.4982e+00 ppl=12.16 best_loss=2.4504e+00 best_ppl=11.59
Epoch 66 - |param|=6.28e+02 |g_param|=5.43e+05 loss=1.9386e+00 ppl=6.95
Validation - loss=2.4808e+00 ppl=11.95 best_loss=2.4504e+00 best_ppl=11.59
Epoch 67 - |param|=6.28e+02 |g_param|=5.03e+05 loss=1.8330e+00 ppl=6.25
Validation - loss=2.4992e+00 ppl=12.17 best_loss=2.4504e+00 best_ppl=11.59
Epoch 68 - |param|=6.29e+02 |g_param|=5.36e+05 loss=1.8076e+00 ppl=6.10
Validation - loss=2.4923e+00 ppl=12.09 best_loss=2.4504e+00 best_ppl=11.59
Epoch 69 - |param|=6.29e+02 |g_param|=5.19e+05 loss=1.7824e+00 ppl=5.94
Validation - loss=2.4831e+00 ppl=11.98 best_loss=2.4504e+00 best_ppl=11.59
Epoch 70 - |param|=6.29e+02 |g_param|=5.41e+05 loss=1.8016e+00 ppl=6.06
Validation - loss=2.5270e+00 ppl=12.52 best_loss=2.4504e+00 best_ppl=11.59
Epoch 71 - |param|=6.30e+02 |g_param|=5.15e+05 loss=1.7488e+00 ppl=5.75
Validation - loss=2.5272e+00 ppl=12.52 best_loss=2.4504e+00 best_ppl=11.59
Epoch 72 - |param|=6.30e+02 |g_param|=5.24e+05 loss=1.6856e+00 ppl=5.40
Validation - loss=2.4975e+00 ppl=12.15 best_loss=2.4504e+00 best_ppl=11.59
Epoch 73 - |param|=6.31e+02 |g_param|=5.16e+05 loss=1.7046e+00 ppl=5.50
Validation - loss=2.5131e+00 ppl=12.34 best_loss=2.4504e+00 best_ppl=11.59
Epoch 74 - |param|=6.31e+02 |g_param|=5.37e+05 loss=1.6816e+00 ppl=5.37
Validation - loss=2.5298e+00 ppl=12.55 best_loss=2.4504e+00 best_ppl=11.59
Epoch 75 - |param|=6.31e+02 |g_param|=5.32e+05 loss=1.7266e+00 ppl=5.62
Validation - loss=2.5492e+00 ppl=12.80 best_loss=2.4504e+00 best_ppl=11.59
Epoch 76 - |param|=6.32e+02 |g_param|=5.49e+05 loss=1.6464e+00 ppl=5.19
Validation - loss=2.5192e+00 ppl=12.42 best_loss=2.4504e+00 best_ppl=11.59
Epoch 77 - |param|=6.32e+02 |g_param|=5.55e+05 loss=1.7043e+00 ppl=5.50
Validation - loss=2.5383e+00 ppl=12.66 best_loss=2.4504e+00 best_ppl=11.59
Epoch 78 - |param|=6.32e+02 |g_param|=5.49e+05 loss=1.5916e+00 ppl=4.91
Validation - loss=2.5035e+00 ppl=12.23 best_loss=2.4504e+00 best_ppl=11.59
Epoch 79 - |param|=6.33e+02 |g_param|=5.56e+05 loss=1.6405e+00 ppl=5.16
Validation - loss=2.5361e+00 ppl=12.63 best_loss=2.4504e+00 best_ppl=11.59
Epoch 80 - |param|=6.33e+02 |g_param|=5.48e+05 loss=1.6012e+00 ppl=4.96
Validation - loss=2.5422e+00 ppl=12.71 best_loss=2.4504e+00 best_ppl=11.59
Epoch 81 - |param|=6.34e+02 |g_param|=5.52e+05 loss=1.5673e+00 ppl=4.79
Validation - loss=2.5372e+00 ppl=12.64 best_loss=2.4504e+00 best_ppl=11.59
Epoch 82 - |param|=6.34e+02 |g_param|=5.81e+05 loss=1.5746e+00 ppl=4.83
Validation - loss=2.5538e+00 ppl=12.86 best_loss=2.4504e+00 best_ppl=11.59
Epoch 83 - |param|=6.34e+02 |g_param|=9.46e+05 loss=1.5323e+00 ppl=4.63
Validation - loss=2.5613e+00 ppl=12.95 best_loss=2.4504e+00 best_ppl=11.59
Epoch 84 - |param|=6.35e+02 |g_param|=6.62e+05 loss=1.5148e+00 ppl=4.55
Validation - loss=2.5653e+00 ppl=13.00 best_loss=2.4504e+00 best_ppl=11.59
Epoch 85 - |param|=6.35e+02 |g_param|=5.72e+05 loss=1.5155e+00 ppl=4.55
Validation - loss=2.5447e+00 ppl=12.74 best_loss=2.4504e+00 best_ppl=11.59
Epoch 86 - |param|=6.36e+02 |g_param|=5.94e+05 loss=1.4830e+00 ppl=4.41
Validation - loss=2.5822e+00 ppl=13.23 best_loss=2.4504e+00 best_ppl=11.59
Epoch 87 - |param|=6.36e+02 |g_param|=6.01e+05 loss=1.4916e+00 ppl=4.44
Validation - loss=2.5579e+00 ppl=12.91 best_loss=2.4504e+00 best_ppl=11.59
Epoch 88 - |param|=6.36e+02 |g_param|=6.23e+05 loss=1.5893e+00 ppl=4.90
Validation - loss=2.5880e+00 ppl=13.30 best_loss=2.4504e+00 best_ppl=11.59
Epoch 89 - |param|=6.37e+02 |g_param|=5.68e+05 loss=1.4472e+00 ppl=4.25
Validation - loss=2.6085e+00 ppl=13.58 best_loss=2.4504e+00 best_ppl=11.59
Epoch 90 - |param|=6.37e+02 |g_param|=6.13e+05 loss=1.4494e+00 ppl=4.26
Validation - loss=2.5694e+00 ppl=13.06 best_loss=2.4504e+00 best_ppl=11.59
Epoch 91 - |param|=6.37e+02 |g_param|=6.11e+05 loss=1.4905e+00 ppl=4.44
Validation - loss=2.5960e+00 ppl=13.41 best_loss=2.4504e+00 best_ppl=11.59
Epoch 92 - |param|=6.38e+02 |g_param|=6.09e+05 loss=1.4212e+00 ppl=4.14
Validation - loss=2.6306e+00 ppl=13.88 best_loss=2.4504e+00 best_ppl=11.59
Epoch 93 - |param|=6.38e+02 |g_param|=6.07e+05 loss=1.4778e+00 ppl=4.38
Validation - loss=2.6025e+00 ppl=13.50 best_loss=2.4504e+00 best_ppl=11.59
Epoch 94 - |param|=6.38e+02 |g_param|=6.08e+05 loss=1.4042e+00 ppl=4.07
Validation - loss=2.6127e+00 ppl=13.64 best_loss=2.4504e+00 best_ppl=11.59
Epoch 95 - |param|=6.39e+02 |g_param|=6.11e+05 loss=1.4490e+00 ppl=4.26
Validation - loss=2.6167e+00 ppl=13.69 best_loss=2.4504e+00 best_ppl=11.59
Epoch 96 - |param|=6.39e+02 |g_param|=6.06e+05 loss=1.3614e+00 ppl=3.90
Validation - loss=2.6365e+00 ppl=13.96 best_loss=2.4504e+00 best_ppl=11.59
Epoch 97 - |param|=6.40e+02 |g_param|=6.03e+05 loss=1.3330e+00 ppl=3.79
Validation - loss=2.6469e+00 ppl=14.11 best_loss=2.4504e+00 best_ppl=11.59
Epoch 98 - |param|=6.40e+02 |g_param|=6.22e+05 loss=1.3548e+00 ppl=3.88
Validation - loss=2.6053e+00 ppl=13.54 best_loss=2.4504e+00 best_ppl=11.59
Epoch 99 - |param|=6.40e+02 |g_param|=6.31e+05 loss=1.3697e+00 ppl=3.93
Validation - loss=2.6176e+00 ppl=13.70 best_loss=2.4504e+00 best_ppl=11.59
Epoch 100 - |param|=6.41e+02 |g_param|=6.72e+05 loss=1.3855e+00 ppl=4.00
Validation - loss=2.6340e+00 ppl=13.93 best_loss=2.4504e+00 best_ppl=11.59
mybk, seq2seq-RL training start for 60 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/mybk-60epoch/seq-model-mybk.57.2.06-7.84.2.58-13.15.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/mybk-60epoch/seq-rl-model-mybk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 58
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 58,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'load_fn': './model/rl2/baseline/seq2seq/mybk-60epoch/seq-model-mybk.57.2.06-7.84.2.58-13.15.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/mybk-60epoch/seq-rl-model-mybk.pth',
    'n_epochs': 100,
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
Epoch 58 - |param|=6.25e+02 |g_param|=4.77e+05 loss=2.0450e+00 ppl=7.73
Validation - loss=2.5917e+00 ppl=13.35 best_loss=inf best_ppl=inf
Epoch 59 - |param|=6.26e+02 |g_param|=5.02e+05 loss=2.1015e+00 ppl=8.18
Validation - loss=2.6003e+00 ppl=13.47 best_loss=2.5917e+00 best_ppl=13.35
Epoch 60 - |param|=6.26e+02 |g_param|=5.16e+05 loss=1.9835e+00 ppl=7.27
Validation - loss=2.5811e+00 ppl=13.21 best_loss=2.5917e+00 best_ppl=13.35
Epoch 61 - |param|=6.26e+02 |g_param|=5.05e+05 loss=2.0212e+00 ppl=7.55
Validation - loss=2.5832e+00 ppl=13.24 best_loss=2.5811e+00 best_ppl=13.21
Epoch 62 - |param|=6.27e+02 |g_param|=5.26e+05 loss=1.9622e+00 ppl=7.11
Validation - loss=2.5810e+00 ppl=13.21 best_loss=2.5811e+00 best_ppl=13.21
Epoch 63 - |param|=6.27e+02 |g_param|=5.09e+05 loss=1.9784e+00 ppl=7.23
Validation - loss=2.5918e+00 ppl=13.35 best_loss=2.5810e+00 best_ppl=13.21
Epoch 64 - |param|=6.28e+02 |g_param|=5.12e+05 loss=1.9073e+00 ppl=6.74
Validation - loss=2.5775e+00 ppl=13.16 best_loss=2.5810e+00 best_ppl=13.21
Epoch 65 - |param|=6.28e+02 |g_param|=5.04e+05 loss=1.9177e+00 ppl=6.81
Validation - loss=2.6070e+00 ppl=13.56 best_loss=2.5775e+00 best_ppl=13.16
Epoch 66 - |param|=6.28e+02 |g_param|=5.51e+05 loss=1.9247e+00 ppl=6.85
Validation - loss=2.6201e+00 ppl=13.74 best_loss=2.5775e+00 best_ppl=13.16
Epoch 67 - |param|=6.29e+02 |g_param|=5.19e+05 loss=1.8520e+00 ppl=6.37
Validation - loss=2.6065e+00 ppl=13.55 best_loss=2.5775e+00 best_ppl=13.16
Epoch 68 - |param|=6.29e+02 |g_param|=5.35e+05 loss=1.8259e+00 ppl=6.21
Validation - loss=2.6435e+00 ppl=14.06 best_loss=2.5775e+00 best_ppl=13.16
Epoch 69 - |param|=6.30e+02 |g_param|=5.23e+05 loss=1.8219e+00 ppl=6.18
Validation - loss=2.6249e+00 ppl=13.80 best_loss=2.5775e+00 best_ppl=13.16
Epoch 70 - |param|=6.30e+02 |g_param|=5.67e+05 loss=1.8854e+00 ppl=6.59
Validation - loss=2.6249e+00 ppl=13.80 best_loss=2.5775e+00 best_ppl=13.16
Epoch 71 - |param|=6.30e+02 |g_param|=5.19e+05 loss=1.7815e+00 ppl=5.94
Validation - loss=2.6194e+00 ppl=13.73 best_loss=2.5775e+00 best_ppl=13.16
Epoch 72 - |param|=6.31e+02 |g_param|=5.49e+05 loss=1.7686e+00 ppl=5.86
Validation - loss=2.6175e+00 ppl=13.70 best_loss=2.5775e+00 best_ppl=13.16
Epoch 73 - |param|=6.31e+02 |g_param|=5.57e+05 loss=1.8102e+00 ppl=6.11
Validation - loss=2.6293e+00 ppl=13.86 best_loss=2.5775e+00 best_ppl=13.16
Epoch 74 - |param|=6.32e+02 |g_param|=5.61e+05 loss=1.7327e+00 ppl=5.66
Validation - loss=2.6367e+00 ppl=13.97 best_loss=2.5775e+00 best_ppl=13.16
Epoch 75 - |param|=6.32e+02 |g_param|=5.35e+05 loss=1.6992e+00 ppl=5.47
Validation - loss=2.6552e+00 ppl=14.23 best_loss=2.5775e+00 best_ppl=13.16
Epoch 76 - |param|=6.32e+02 |g_param|=5.61e+05 loss=1.7129e+00 ppl=5.55
Validation - loss=2.6390e+00 ppl=14.00 best_loss=2.5775e+00 best_ppl=13.16
Epoch 77 - |param|=6.33e+02 |g_param|=5.51e+05 loss=1.7210e+00 ppl=5.59
Validation - loss=2.6747e+00 ppl=14.51 best_loss=2.5775e+00 best_ppl=13.16
Epoch 78 - |param|=6.33e+02 |g_param|=5.71e+05 loss=1.7201e+00 ppl=5.58
Validation - loss=2.6746e+00 ppl=14.51 best_loss=2.5775e+00 best_ppl=13.16
Epoch 79 - |param|=6.33e+02 |g_param|=5.61e+05 loss=1.6682e+00 ppl=5.30
Validation - loss=2.6738e+00 ppl=14.49 best_loss=2.5775e+00 best_ppl=13.16
Epoch 80 - |param|=6.34e+02 |g_param|=5.88e+05 loss=1.6600e+00 ppl=5.26
Validation - loss=2.7090e+00 ppl=15.01 best_loss=2.5775e+00 best_ppl=13.16
Epoch 81 - |param|=6.34e+02 |g_param|=5.46e+05 loss=1.6048e+00 ppl=4.98
Validation - loss=2.6634e+00 ppl=14.35 best_loss=2.5775e+00 best_ppl=13.16
Epoch 82 - |param|=6.35e+02 |g_param|=5.84e+05 loss=1.6835e+00 ppl=5.38
Validation - loss=2.6919e+00 ppl=14.76 best_loss=2.5775e+00 best_ppl=13.16
Epoch 83 - |param|=6.35e+02 |g_param|=5.83e+05 loss=1.5906e+00 ppl=4.91
Validation - loss=2.7066e+00 ppl=14.98 best_loss=2.5775e+00 best_ppl=13.16
Epoch 84 - |param|=6.35e+02 |g_param|=6.05e+05 loss=1.6546e+00 ppl=5.23
Validation - loss=2.7323e+00 ppl=15.37 best_loss=2.5775e+00 best_ppl=13.16
Epoch 85 - |param|=6.36e+02 |g_param|=5.72e+05 loss=1.6206e+00 ppl=5.06
Validation - loss=2.6979e+00 ppl=14.85 best_loss=2.5775e+00 best_ppl=13.16
Epoch 86 - |param|=6.36e+02 |g_param|=6.18e+05 loss=1.6147e+00 ppl=5.03
Validation - loss=2.7071e+00 ppl=14.99 best_loss=2.5775e+00 best_ppl=13.16
Epoch 87 - |param|=6.36e+02 |g_param|=6.06e+05 loss=1.5965e+00 ppl=4.94
Validation - loss=2.7070e+00 ppl=14.98 best_loss=2.5775e+00 best_ppl=13.16
Epoch 88 - |param|=6.37e+02 |g_param|=6.42e+05 loss=1.5826e+00 ppl=4.87
Validation - loss=2.7407e+00 ppl=15.50 best_loss=2.5775e+00 best_ppl=13.16
Epoch 89 - |param|=6.37e+02 |g_param|=5.93e+05 loss=1.5227e+00 ppl=4.58
Validation - loss=2.7590e+00 ppl=15.78 best_loss=2.5775e+00 best_ppl=13.16
Epoch 90 - |param|=6.38e+02 |g_param|=1.10e+06 loss=1.5923e+00 ppl=4.91
Validation - loss=2.7572e+00 ppl=15.76 best_loss=2.5775e+00 best_ppl=13.16
Epoch 91 - |param|=6.38e+02 |g_param|=1.25e+06 loss=1.5784e+00 ppl=4.85
Validation - loss=2.7553e+00 ppl=15.73 best_loss=2.5775e+00 best_ppl=13.16
Epoch 92 - |param|=6.38e+02 |g_param|=1.27e+06 loss=1.5105e+00 ppl=4.53
Validation - loss=2.7789e+00 ppl=16.10 best_loss=2.5775e+00 best_ppl=13.16
Epoch 93 - |param|=6.39e+02 |g_param|=8.73e+05 loss=1.4935e+00 ppl=4.45
Validation - loss=2.7629e+00 ppl=15.85 best_loss=2.5775e+00 best_ppl=13.16
Epoch 94 - |param|=6.39e+02 |g_param|=6.14e+05 loss=1.4659e+00 ppl=4.33
Validation - loss=2.7834e+00 ppl=16.17 best_loss=2.5775e+00 best_ppl=13.16
Epoch 95 - |param|=6.39e+02 |g_param|=6.39e+05 loss=1.5349e+00 ppl=4.64
Validation - loss=2.7832e+00 ppl=16.17 best_loss=2.5775e+00 best_ppl=13.16
Epoch 96 - |param|=6.40e+02 |g_param|=6.30e+05 loss=1.4525e+00 ppl=4.27
Validation - loss=2.7935e+00 ppl=16.34 best_loss=2.5775e+00 best_ppl=13.16
Epoch 97 - |param|=6.40e+02 |g_param|=5.99e+05 loss=1.4072e+00 ppl=4.08
Validation - loss=2.7873e+00 ppl=16.24 best_loss=2.5775e+00 best_ppl=13.16
Epoch 98 - |param|=6.41e+02 |g_param|=6.62e+05 loss=1.4293e+00 ppl=4.18
Validation - loss=2.8176e+00 ppl=16.74 best_loss=2.5775e+00 best_ppl=13.16
Epoch 99 - |param|=6.41e+02 |g_param|=6.40e+05 loss=1.4900e+00 ppl=4.44
Validation - loss=2.8414e+00 ppl=17.14 best_loss=2.5775e+00 best_ppl=13.16
Epoch 100 - |param|=6.41e+02 |g_param|=6.51e+05 loss=1.3789e+00 ppl=3.97
Validation - loss=2.7831e+00 ppl=16.17 best_loss=2.5775e+00 best_ppl=13.16
mybk, seq2seq-RL training start for 70 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/mybk-70epoch/seq-model-mybk.68.1.77-5.87.2.39-10.87.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/mybk-70epoch/seq-rl-model-mybk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 69
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 69,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'load_fn': './model/rl2/baseline/seq2seq/mybk-70epoch/seq-model-mybk.68.1.77-5.87.2.39-10.87.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/mybk-70epoch/seq-rl-model-mybk.pth',
    'n_epochs': 100,
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
Epoch 69 - |param|=6.31e+02 |g_param|=5.31e+05 loss=1.6617e+00 ppl=5.27
Validation - loss=2.3699e+00 ppl=10.70 best_loss=inf best_ppl=inf
Epoch 70 - |param|=6.31e+02 |g_param|=5.34e+05 loss=1.5975e+00 ppl=4.94
Validation - loss=2.3592e+00 ppl=10.58 best_loss=2.3699e+00 best_ppl=10.70
Epoch 71 - |param|=6.32e+02 |g_param|=5.41e+05 loss=1.6186e+00 ppl=5.05
Validation - loss=2.4033e+00 ppl=11.06 best_loss=2.3592e+00 best_ppl=10.58
Epoch 72 - |param|=6.32e+02 |g_param|=5.24e+05 loss=1.5818e+00 ppl=4.86
Validation - loss=2.3780e+00 ppl=10.78 best_loss=2.3592e+00 best_ppl=10.58
Epoch 73 - |param|=6.32e+02 |g_param|=5.60e+05 loss=1.6462e+00 ppl=5.19
Validation - loss=2.4260e+00 ppl=11.31 best_loss=2.3592e+00 best_ppl=10.58
Epoch 74 - |param|=6.33e+02 |g_param|=5.47e+05 loss=1.5254e+00 ppl=4.60
Validation - loss=2.3935e+00 ppl=10.95 best_loss=2.3592e+00 best_ppl=10.58
Epoch 75 - |param|=6.33e+02 |g_param|=5.58e+05 loss=1.5558e+00 ppl=4.74
Validation - loss=2.3914e+00 ppl=10.93 best_loss=2.3592e+00 best_ppl=10.58
Epoch 76 - |param|=6.34e+02 |g_param|=5.73e+05 loss=1.5331e+00 ppl=4.63
Validation - loss=2.4182e+00 ppl=11.23 best_loss=2.3592e+00 best_ppl=10.58
Epoch 77 - |param|=6.34e+02 |g_param|=5.77e+05 loss=1.5944e+00 ppl=4.93
Validation - loss=2.4288e+00 ppl=11.34 best_loss=2.3592e+00 best_ppl=10.58
Epoch 78 - |param|=6.34e+02 |g_param|=5.86e+05 loss=1.5070e+00 ppl=4.51
Validation - loss=2.3946e+00 ppl=10.96 best_loss=2.3592e+00 best_ppl=10.58
Epoch 79 - |param|=6.35e+02 |g_param|=5.78e+05 loss=1.4674e+00 ppl=4.34
Validation - loss=2.4135e+00 ppl=11.17 best_loss=2.3592e+00 best_ppl=10.58
Epoch 80 - |param|=6.35e+02 |g_param|=5.76e+05 loss=1.5639e+00 ppl=4.78
Validation - loss=2.4148e+00 ppl=11.19 best_loss=2.3592e+00 best_ppl=10.58
Epoch 81 - |param|=6.36e+02 |g_param|=5.65e+05 loss=1.4775e+00 ppl=4.38
Validation - loss=2.4288e+00 ppl=11.35 best_loss=2.3592e+00 best_ppl=10.58
Epoch 82 - |param|=6.36e+02 |g_param|=5.72e+05 loss=1.3840e+00 ppl=3.99
Validation - loss=2.4149e+00 ppl=11.19 best_loss=2.3592e+00 best_ppl=10.58
Epoch 83 - |param|=6.36e+02 |g_param|=5.62e+05 loss=1.4015e+00 ppl=4.06
Validation - loss=2.4481e+00 ppl=11.57 best_loss=2.3592e+00 best_ppl=10.58
Epoch 84 - |param|=6.37e+02 |g_param|=5.77e+05 loss=1.4321e+00 ppl=4.19
Validation - loss=2.4039e+00 ppl=11.07 best_loss=2.3592e+00 best_ppl=10.58
Epoch 85 - |param|=6.37e+02 |g_param|=5.88e+05 loss=1.3893e+00 ppl=4.01
Validation - loss=2.4287e+00 ppl=11.34 best_loss=2.3592e+00 best_ppl=10.58
Epoch 86 - |param|=6.37e+02 |g_param|=6.05e+05 loss=1.3911e+00 ppl=4.02
Validation - loss=2.4469e+00 ppl=11.55 best_loss=2.3592e+00 best_ppl=10.58
Epoch 87 - |param|=6.38e+02 |g_param|=5.59e+05 loss=1.3608e+00 ppl=3.90
Validation - loss=2.4496e+00 ppl=11.58 best_loss=2.3592e+00 best_ppl=10.58
Epoch 88 - |param|=6.38e+02 |g_param|=5.92e+05 loss=1.3304e+00 ppl=3.78
Validation - loss=2.4365e+00 ppl=11.43 best_loss=2.3592e+00 best_ppl=10.58
Epoch 89 - |param|=6.39e+02 |g_param|=5.82e+05 loss=1.3081e+00 ppl=3.70
Validation - loss=2.4320e+00 ppl=11.38 best_loss=2.3592e+00 best_ppl=10.58
Epoch 90 - |param|=6.39e+02 |g_param|=6.42e+05 loss=1.3316e+00 ppl=3.79
Validation - loss=2.4491e+00 ppl=11.58 best_loss=2.3592e+00 best_ppl=10.58
Epoch 91 - |param|=6.39e+02 |g_param|=6.00e+05 loss=1.3229e+00 ppl=3.75
Validation - loss=2.4133e+00 ppl=11.17 best_loss=2.3592e+00 best_ppl=10.58
Epoch 92 - |param|=6.40e+02 |g_param|=6.00e+05 loss=1.3024e+00 ppl=3.68
Validation - loss=2.4432e+00 ppl=11.51 best_loss=2.3592e+00 best_ppl=10.58
Epoch 93 - |param|=6.40e+02 |g_param|=5.88e+05 loss=1.2633e+00 ppl=3.54
Validation - loss=2.4602e+00 ppl=11.71 best_loss=2.3592e+00 best_ppl=10.58
Epoch 94 - |param|=6.40e+02 |g_param|=6.28e+05 loss=1.3514e+00 ppl=3.86
Validation - loss=2.4859e+00 ppl=12.01 best_loss=2.3592e+00 best_ppl=10.58
Epoch 95 - |param|=6.41e+02 |g_param|=5.89e+05 loss=1.2618e+00 ppl=3.53
Validation - loss=2.4907e+00 ppl=12.07 best_loss=2.3592e+00 best_ppl=10.58
Epoch 96 - |param|=6.41e+02 |g_param|=6.31e+05 loss=1.2814e+00 ppl=3.60
Validation - loss=2.5086e+00 ppl=12.29 best_loss=2.3592e+00 best_ppl=10.58
Epoch 97 - |param|=6.42e+02 |g_param|=6.29e+05 loss=1.2515e+00 ppl=3.50
Validation - loss=2.4730e+00 ppl=11.86 best_loss=2.3592e+00 best_ppl=10.58
Epoch 98 - |param|=6.42e+02 |g_param|=6.19e+05 loss=1.2132e+00 ppl=3.36
Validation - loss=2.5138e+00 ppl=12.35 best_loss=2.3592e+00 best_ppl=10.58
Epoch 99 - |param|=6.42e+02 |g_param|=6.04e+05 loss=1.1956e+00 ppl=3.31
Validation - loss=2.4984e+00 ppl=12.16 best_loss=2.3592e+00 best_ppl=10.58
Epoch 100 - |param|=6.43e+02 |g_param|=6.31e+05 loss=1.1830e+00 ppl=3.26
Validation - loss=2.5048e+00 ppl=12.24 best_loss=2.3592e+00 best_ppl=10.58
####################
bkmy, seq2seq-RL training start for 30 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-30epoch/seq-model-bkmy.30.2.69-14.67.2.53-12.59.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-30epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 31
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 31,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-30epoch/seq-model-bkmy.30.2.69-14.67.2.53-12.59.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-30epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 31 - |param|=6.11e+02 |g_param|=3.30e+05 loss=2.6182e+00 ppl=13.71
Validation - loss=2.5012e+00 ppl=12.20 best_loss=inf best_ppl=inf
Epoch 32 - |param|=6.12e+02 |g_param|=3.43e+05 loss=2.6420e+00 ppl=14.04
Validation - loss=2.4896e+00 ppl=12.06 best_loss=2.5012e+00 best_ppl=12.20
Epoch 33 - |param|=6.12e+02 |g_param|=3.50e+05 loss=2.6407e+00 ppl=14.02
Validation - loss=2.4813e+00 ppl=11.96 best_loss=2.4896e+00 best_ppl=12.06
Epoch 34 - |param|=6.13e+02 |g_param|=3.57e+05 loss=2.5575e+00 ppl=12.90
Validation - loss=2.4616e+00 ppl=11.72 best_loss=2.4813e+00 best_ppl=11.96
Epoch 35 - |param|=6.13e+02 |g_param|=3.64e+05 loss=2.5625e+00 ppl=12.97
Validation - loss=2.4657e+00 ppl=11.77 best_loss=2.4616e+00 best_ppl=11.72
Epoch 36 - |param|=6.13e+02 |g_param|=3.72e+05 loss=2.4484e+00 ppl=11.57
Validation - loss=2.4374e+00 ppl=11.44 best_loss=2.4616e+00 best_ppl=11.72
Epoch 37 - |param|=6.14e+02 |g_param|=3.49e+05 loss=2.4349e+00 ppl=11.42
Validation - loss=2.4349e+00 ppl=11.41 best_loss=2.4374e+00 best_ppl=11.44
Epoch 38 - |param|=6.14e+02 |g_param|=3.95e+05 loss=2.3645e+00 ppl=10.64
Validation - loss=2.4069e+00 ppl=11.10 best_loss=2.4349e+00 best_ppl=11.41
Epoch 39 - |param|=6.15e+02 |g_param|=3.69e+05 loss=2.3535e+00 ppl=10.52
Validation - loss=2.4019e+00 ppl=11.04 best_loss=2.4069e+00 best_ppl=11.10
Epoch 40 - |param|=6.15e+02 |g_param|=3.81e+05 loss=2.3105e+00 ppl=10.08
Validation - loss=2.4137e+00 ppl=11.18 best_loss=2.4019e+00 best_ppl=11.04
Epoch 41 - |param|=6.16e+02 |g_param|=3.63e+05 loss=2.2639e+00 ppl=9.62
Validation - loss=2.3895e+00 ppl=10.91 best_loss=2.4019e+00 best_ppl=11.04
Epoch 42 - |param|=6.16e+02 |g_param|=4.12e+05 loss=2.3327e+00 ppl=10.31
Validation - loss=2.4137e+00 ppl=11.18 best_loss=2.3895e+00 best_ppl=10.91
Epoch 43 - |param|=6.17e+02 |g_param|=4.01e+05 loss=2.2705e+00 ppl=9.68
Validation - loss=2.3699e+00 ppl=10.70 best_loss=2.3895e+00 best_ppl=10.91
Epoch 44 - |param|=6.17e+02 |g_param|=4.31e+05 loss=2.2906e+00 ppl=9.88
Validation - loss=2.3641e+00 ppl=10.63 best_loss=2.3699e+00 best_ppl=10.70
Epoch 45 - |param|=6.17e+02 |g_param|=4.41e+05 loss=2.3333e+00 ppl=10.31
Validation - loss=2.3627e+00 ppl=10.62 best_loss=2.3641e+00 best_ppl=10.63
Epoch 46 - |param|=6.18e+02 |g_param|=4.14e+05 loss=2.1562e+00 ppl=8.64
Validation - loss=2.3471e+00 ppl=10.46 best_loss=2.3627e+00 best_ppl=10.62
Epoch 47 - |param|=6.18e+02 |g_param|=3.99e+05 loss=2.1995e+00 ppl=9.02
Validation - loss=2.3632e+00 ppl=10.62 best_loss=2.3471e+00 best_ppl=10.46
Epoch 48 - |param|=6.19e+02 |g_param|=4.26e+05 loss=2.0981e+00 ppl=8.15
Validation - loss=2.3706e+00 ppl=10.70 best_loss=2.3471e+00 best_ppl=10.46
Epoch 49 - |param|=6.19e+02 |g_param|=4.30e+05 loss=2.1473e+00 ppl=8.56
Validation - loss=2.3466e+00 ppl=10.45 best_loss=2.3471e+00 best_ppl=10.46
Epoch 50 - |param|=6.20e+02 |g_param|=4.23e+05 loss=2.0113e+00 ppl=7.47
Validation - loss=2.3301e+00 ppl=10.28 best_loss=2.3466e+00 best_ppl=10.45
Epoch 51 - |param|=6.20e+02 |g_param|=4.31e+05 loss=2.0209e+00 ppl=7.55
Validation - loss=2.3332e+00 ppl=10.31 best_loss=2.3301e+00 best_ppl=10.28
Epoch 52 - |param|=6.20e+02 |g_param|=4.61e+05 loss=2.0635e+00 ppl=7.87
Validation - loss=2.3363e+00 ppl=10.34 best_loss=2.3301e+00 best_ppl=10.28
Epoch 53 - |param|=6.21e+02 |g_param|=4.45e+05 loss=2.0137e+00 ppl=7.49
Validation - loss=2.3214e+00 ppl=10.19 best_loss=2.3301e+00 best_ppl=10.28
Epoch 54 - |param|=6.21e+02 |g_param|=4.64e+05 loss=1.9541e+00 ppl=7.06
Validation - loss=2.3285e+00 ppl=10.26 best_loss=2.3214e+00 best_ppl=10.19
Epoch 55 - |param|=6.22e+02 |g_param|=4.60e+05 loss=1.9474e+00 ppl=7.01
Validation - loss=2.3109e+00 ppl=10.08 best_loss=2.3214e+00 best_ppl=10.19
Epoch 56 - |param|=6.22e+02 |g_param|=4.52e+05 loss=1.9166e+00 ppl=6.80
Validation - loss=2.3599e+00 ppl=10.59 best_loss=2.3109e+00 best_ppl=10.08
Epoch 57 - |param|=6.23e+02 |g_param|=4.54e+05 loss=1.9248e+00 ppl=6.85
Validation - loss=2.3129e+00 ppl=10.10 best_loss=2.3109e+00 best_ppl=10.08
Epoch 58 - |param|=6.23e+02 |g_param|=5.08e+05 loss=1.8968e+00 ppl=6.66
Validation - loss=2.3541e+00 ppl=10.53 best_loss=2.3109e+00 best_ppl=10.08
Epoch 59 - |param|=6.23e+02 |g_param|=4.66e+05 loss=1.8511e+00 ppl=6.37
Validation - loss=2.3431e+00 ppl=10.41 best_loss=2.3109e+00 best_ppl=10.08
Epoch 60 - |param|=6.24e+02 |g_param|=4.73e+05 loss=1.8570e+00 ppl=6.40
Validation - loss=2.3376e+00 ppl=10.36 best_loss=2.3109e+00 best_ppl=10.08
Epoch 61 - |param|=6.24e+02 |g_param|=4.65e+05 loss=1.7679e+00 ppl=5.86
Validation - loss=2.3523e+00 ppl=10.51 best_loss=2.3109e+00 best_ppl=10.08
Epoch 62 - |param|=6.25e+02 |g_param|=4.89e+05 loss=1.7831e+00 ppl=5.95
Validation - loss=2.3313e+00 ppl=10.29 best_loss=2.3109e+00 best_ppl=10.08
Epoch 63 - |param|=6.25e+02 |g_param|=8.00e+05 loss=1.8044e+00 ppl=6.08
Validation - loss=2.3465e+00 ppl=10.45 best_loss=2.3109e+00 best_ppl=10.08
Epoch 64 - |param|=6.25e+02 |g_param|=1.01e+06 loss=1.7267e+00 ppl=5.62
Validation - loss=2.3474e+00 ppl=10.46 best_loss=2.3109e+00 best_ppl=10.08
Epoch 65 - |param|=6.26e+02 |g_param|=1.01e+06 loss=1.7887e+00 ppl=5.98
Validation - loss=2.3381e+00 ppl=10.36 best_loss=2.3109e+00 best_ppl=10.08
Epoch 66 - |param|=6.26e+02 |g_param|=1.02e+06 loss=1.7619e+00 ppl=5.82
Validation - loss=2.3655e+00 ppl=10.65 best_loss=2.3109e+00 best_ppl=10.08
Epoch 67 - |param|=6.27e+02 |g_param|=5.65e+05 loss=1.6851e+00 ppl=5.39
Validation - loss=2.3526e+00 ppl=10.51 best_loss=2.3109e+00 best_ppl=10.08
Epoch 68 - |param|=6.27e+02 |g_param|=5.11e+05 loss=1.7365e+00 ppl=5.68
Validation - loss=2.3613e+00 ppl=10.60 best_loss=2.3109e+00 best_ppl=10.08
Epoch 69 - |param|=6.27e+02 |g_param|=5.00e+05 loss=1.6909e+00 ppl=5.42
Validation - loss=2.3387e+00 ppl=10.37 best_loss=2.3109e+00 best_ppl=10.08
Epoch 70 - |param|=6.28e+02 |g_param|=5.33e+05 loss=1.6375e+00 ppl=5.14
Validation - loss=2.3547e+00 ppl=10.54 best_loss=2.3109e+00 best_ppl=10.08
Epoch 71 - |param|=6.28e+02 |g_param|=5.14e+05 loss=1.7014e+00 ppl=5.48
Validation - loss=2.3590e+00 ppl=10.58 best_loss=2.3109e+00 best_ppl=10.08
Epoch 72 - |param|=6.29e+02 |g_param|=5.52e+05 loss=1.6096e+00 ppl=5.00
Validation - loss=2.3581e+00 ppl=10.57 best_loss=2.3109e+00 best_ppl=10.08
Epoch 73 - |param|=6.29e+02 |g_param|=5.08e+05 loss=1.5618e+00 ppl=4.77
Validation - loss=2.3635e+00 ppl=10.63 best_loss=2.3109e+00 best_ppl=10.08
Epoch 74 - |param|=6.30e+02 |g_param|=5.07e+05 loss=1.5616e+00 ppl=4.77
Validation - loss=2.3993e+00 ppl=11.02 best_loss=2.3109e+00 best_ppl=10.08
Epoch 75 - |param|=6.30e+02 |g_param|=5.25e+05 loss=1.5980e+00 ppl=4.94
Validation - loss=2.3880e+00 ppl=10.89 best_loss=2.3109e+00 best_ppl=10.08
Epoch 76 - |param|=6.30e+02 |g_param|=5.28e+05 loss=1.5110e+00 ppl=4.53
Validation - loss=2.4034e+00 ppl=11.06 best_loss=2.3109e+00 best_ppl=10.08
Epoch 77 - |param|=6.31e+02 |g_param|=5.43e+05 loss=1.5939e+00 ppl=4.92
Validation - loss=2.3907e+00 ppl=10.92 best_loss=2.3109e+00 best_ppl=10.08
Epoch 78 - |param|=6.31e+02 |g_param|=5.62e+05 loss=1.5340e+00 ppl=4.64
Validation - loss=2.4166e+00 ppl=11.21 best_loss=2.3109e+00 best_ppl=10.08
Epoch 79 - |param|=6.31e+02 |g_param|=5.34e+05 loss=1.4984e+00 ppl=4.47
Validation - loss=2.4185e+00 ppl=11.23 best_loss=2.3109e+00 best_ppl=10.08
Epoch 80 - |param|=6.32e+02 |g_param|=5.51e+05 loss=1.4760e+00 ppl=4.38
Validation - loss=2.4334e+00 ppl=11.40 best_loss=2.3109e+00 best_ppl=10.08
Epoch 81 - |param|=6.32e+02 |g_param|=5.70e+05 loss=1.5557e+00 ppl=4.74
Validation - loss=2.4107e+00 ppl=11.14 best_loss=2.3109e+00 best_ppl=10.08
Epoch 82 - |param|=6.33e+02 |g_param|=3.60e+05 loss=1.4590e+00 ppl=4.30
Validation - loss=2.4581e+00 ppl=11.68 best_loss=2.3109e+00 best_ppl=10.08
Epoch 83 - |param|=6.33e+02 |g_param|=2.94e+05 loss=1.5422e+00 ppl=4.67
Validation - loss=2.4709e+00 ppl=11.83 best_loss=2.3109e+00 best_ppl=10.08
Epoch 84 - |param|=6.33e+02 |g_param|=2.92e+05 loss=1.4784e+00 ppl=4.39
Validation - loss=2.4162e+00 ppl=11.20 best_loss=2.3109e+00 best_ppl=10.08
Epoch 85 - |param|=6.34e+02 |g_param|=2.75e+05 loss=1.4289e+00 ppl=4.17
Validation - loss=2.4032e+00 ppl=11.06 best_loss=2.3109e+00 best_ppl=10.08
Epoch 86 - |param|=6.34e+02 |g_param|=2.92e+05 loss=1.4477e+00 ppl=4.25
Validation - loss=2.4339e+00 ppl=11.40 best_loss=2.3109e+00 best_ppl=10.08
Epoch 87 - |param|=6.35e+02 |g_param|=2.78e+05 loss=1.3642e+00 ppl=3.91
Validation - loss=2.4648e+00 ppl=11.76 best_loss=2.3109e+00 best_ppl=10.08
Epoch 88 - |param|=6.35e+02 |g_param|=3.11e+05 loss=1.4602e+00 ppl=4.31
Validation - loss=2.5007e+00 ppl=12.19 best_loss=2.3109e+00 best_ppl=10.08
Epoch 89 - |param|=6.35e+02 |g_param|=2.96e+05 loss=1.4061e+00 ppl=4.08
Validation - loss=2.5034e+00 ppl=12.22 best_loss=2.3109e+00 best_ppl=10.08
Epoch 90 - |param|=6.36e+02 |g_param|=3.02e+05 loss=1.3529e+00 ppl=3.87
Validation - loss=2.4724e+00 ppl=11.85 best_loss=2.3109e+00 best_ppl=10.08
Epoch 91 - |param|=6.36e+02 |g_param|=3.08e+05 loss=1.4119e+00 ppl=4.10
Validation - loss=2.4931e+00 ppl=12.10 best_loss=2.3109e+00 best_ppl=10.08
Epoch 92 - |param|=6.36e+02 |g_param|=2.92e+05 loss=1.3644e+00 ppl=3.91
Validation - loss=2.4732e+00 ppl=11.86 best_loss=2.3109e+00 best_ppl=10.08
Epoch 93 - |param|=6.37e+02 |g_param|=3.03e+05 loss=1.3316e+00 ppl=3.79
Validation - loss=2.4970e+00 ppl=12.15 best_loss=2.3109e+00 best_ppl=10.08
Epoch 94 - |param|=6.37e+02 |g_param|=2.92e+05 loss=1.2799e+00 ppl=3.60
Validation - loss=2.4993e+00 ppl=12.17 best_loss=2.3109e+00 best_ppl=10.08
Epoch 95 - |param|=6.38e+02 |g_param|=2.88e+05 loss=1.2612e+00 ppl=3.53
Validation - loss=2.4833e+00 ppl=11.98 best_loss=2.3109e+00 best_ppl=10.08
Epoch 96 - |param|=6.38e+02 |g_param|=2.94e+05 loss=1.2593e+00 ppl=3.52
Validation - loss=2.4974e+00 ppl=12.15 best_loss=2.3109e+00 best_ppl=10.08
Epoch 97 - |param|=6.38e+02 |g_param|=2.95e+05 loss=1.3030e+00 ppl=3.68
Validation - loss=2.5175e+00 ppl=12.40 best_loss=2.3109e+00 best_ppl=10.08
Epoch 98 - |param|=6.39e+02 |g_param|=3.01e+05 loss=1.2262e+00 ppl=3.41
Validation - loss=2.5416e+00 ppl=12.70 best_loss=2.3109e+00 best_ppl=10.08
Epoch 99 - |param|=6.39e+02 |g_param|=3.04e+05 loss=1.2276e+00 ppl=3.41
Validation - loss=2.5136e+00 ppl=12.35 best_loss=2.3109e+00 best_ppl=10.08
Epoch 100 - |param|=6.39e+02 |g_param|=3.23e+05 loss=1.3031e+00 ppl=3.68
Validation - loss=2.5151e+00 ppl=12.37 best_loss=2.3109e+00 best_ppl=10.08
bkmy, seq2seq-RL training start for 40 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-40epoch/seq-model-bkmy.29.2.67-14.48.2.59-13.38.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-40epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-40epoch/seq-model-bkmy.29.2.67-14.48.2.59-13.38.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-40epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 30 - |param|=6.12e+02 |g_param|=3.35e+05 loss=2.6201e+00 ppl=13.74
Validation - loss=2.5664e+00 ppl=13.02 best_loss=inf best_ppl=inf
Epoch 31 - |param|=6.12e+02 |g_param|=3.33e+05 loss=2.6350e+00 ppl=13.94
Validation - loss=2.5617e+00 ppl=12.96 best_loss=2.5664e+00 best_ppl=13.02
Epoch 32 - |param|=6.12e+02 |g_param|=3.59e+05 loss=2.5465e+00 ppl=12.76
Validation - loss=2.5811e+00 ppl=13.21 best_loss=2.5617e+00 best_ppl=12.96
Epoch 33 - |param|=6.13e+02 |g_param|=3.43e+05 loss=2.5718e+00 ppl=13.09
Validation - loss=2.5436e+00 ppl=12.73 best_loss=2.5617e+00 best_ppl=12.96
Epoch 34 - |param|=6.13e+02 |g_param|=3.64e+05 loss=2.4910e+00 ppl=12.07
Validation - loss=2.5366e+00 ppl=12.64 best_loss=2.5436e+00 best_ppl=12.73
Epoch 35 - |param|=6.14e+02 |g_param|=3.70e+05 loss=2.4926e+00 ppl=12.09
Validation - loss=2.5439e+00 ppl=12.73 best_loss=2.5366e+00 best_ppl=12.64
Epoch 36 - |param|=6.14e+02 |g_param|=3.90e+05 loss=2.4453e+00 ppl=11.53
Validation - loss=2.5081e+00 ppl=12.28 best_loss=2.5366e+00 best_ppl=12.64
Epoch 37 - |param|=6.15e+02 |g_param|=3.87e+05 loss=2.4207e+00 ppl=11.25
Validation - loss=2.5073e+00 ppl=12.27 best_loss=2.5081e+00 best_ppl=12.28
Epoch 38 - |param|=6.15e+02 |g_param|=3.93e+05 loss=2.3704e+00 ppl=10.70
Validation - loss=2.5177e+00 ppl=12.40 best_loss=2.5073e+00 best_ppl=12.27
Epoch 39 - |param|=6.16e+02 |g_param|=3.67e+05 loss=2.3269e+00 ppl=10.25
Validation - loss=2.5151e+00 ppl=12.37 best_loss=2.5073e+00 best_ppl=12.27
Epoch 40 - |param|=6.16e+02 |g_param|=3.96e+05 loss=2.3015e+00 ppl=9.99
Validation - loss=2.5081e+00 ppl=12.28 best_loss=2.5073e+00 best_ppl=12.27
Epoch 41 - |param|=6.17e+02 |g_param|=3.72e+05 loss=2.2743e+00 ppl=9.72
Validation - loss=2.5026e+00 ppl=12.21 best_loss=2.5073e+00 best_ppl=12.27
Epoch 42 - |param|=6.17e+02 |g_param|=3.86e+05 loss=2.2539e+00 ppl=9.52
Validation - loss=2.5111e+00 ppl=12.32 best_loss=2.5026e+00 best_ppl=12.21
Epoch 43 - |param|=6.17e+02 |g_param|=4.16e+05 loss=2.2580e+00 ppl=9.56
Validation - loss=2.4930e+00 ppl=12.10 best_loss=2.5026e+00 best_ppl=12.21
Epoch 44 - |param|=6.18e+02 |g_param|=4.18e+05 loss=2.2345e+00 ppl=9.34
Validation - loss=2.4688e+00 ppl=11.81 best_loss=2.4930e+00 best_ppl=12.10
Epoch 45 - |param|=6.18e+02 |g_param|=4.09e+05 loss=2.2243e+00 ppl=9.25
Validation - loss=2.5058e+00 ppl=12.25 best_loss=2.4688e+00 best_ppl=11.81
Epoch 46 - |param|=6.19e+02 |g_param|=4.52e+05 loss=2.1846e+00 ppl=8.89
Validation - loss=2.4857e+00 ppl=12.01 best_loss=2.4688e+00 best_ppl=11.81
Epoch 47 - |param|=6.19e+02 |g_param|=4.35e+05 loss=2.2022e+00 ppl=9.04
Validation - loss=2.4512e+00 ppl=11.60 best_loss=2.4688e+00 best_ppl=11.81
Epoch 48 - |param|=6.20e+02 |g_param|=4.52e+05 loss=2.1150e+00 ppl=8.29
Validation - loss=2.4708e+00 ppl=11.83 best_loss=2.4512e+00 best_ppl=11.60
Epoch 49 - |param|=6.20e+02 |g_param|=4.46e+05 loss=2.0895e+00 ppl=8.08
Validation - loss=2.4585e+00 ppl=11.69 best_loss=2.4512e+00 best_ppl=11.60
Epoch 50 - |param|=6.20e+02 |g_param|=4.50e+05 loss=2.1168e+00 ppl=8.30
Validation - loss=2.4695e+00 ppl=11.82 best_loss=2.4512e+00 best_ppl=11.60
Epoch 51 - |param|=6.21e+02 |g_param|=4.38e+05 loss=2.0328e+00 ppl=7.64
Validation - loss=2.4731e+00 ppl=11.86 best_loss=2.4512e+00 best_ppl=11.60
Epoch 52 - |param|=6.21e+02 |g_param|=4.68e+05 loss=2.0165e+00 ppl=7.51
Validation - loss=2.4587e+00 ppl=11.69 best_loss=2.4512e+00 best_ppl=11.60
Epoch 53 - |param|=6.22e+02 |g_param|=4.39e+05 loss=1.9921e+00 ppl=7.33
Validation - loss=2.4571e+00 ppl=11.67 best_loss=2.4512e+00 best_ppl=11.60
Epoch 54 - |param|=6.22e+02 |g_param|=4.70e+05 loss=2.0398e+00 ppl=7.69
Validation - loss=2.4683e+00 ppl=11.80 best_loss=2.4512e+00 best_ppl=11.60
Epoch 55 - |param|=6.23e+02 |g_param|=4.42e+05 loss=1.9284e+00 ppl=6.88
Validation - loss=2.4408e+00 ppl=11.48 best_loss=2.4512e+00 best_ppl=11.60
Epoch 56 - |param|=6.23e+02 |g_param|=4.91e+05 loss=1.9222e+00 ppl=6.84
Validation - loss=2.4493e+00 ppl=11.58 best_loss=2.4408e+00 best_ppl=11.48
Epoch 57 - |param|=6.23e+02 |g_param|=4.80e+05 loss=1.9511e+00 ppl=7.04
Validation - loss=2.4611e+00 ppl=11.72 best_loss=2.4408e+00 best_ppl=11.48
Epoch 58 - |param|=6.24e+02 |g_param|=4.79e+05 loss=1.9327e+00 ppl=6.91
Validation - loss=2.4840e+00 ppl=11.99 best_loss=2.4408e+00 best_ppl=11.48
Epoch 59 - |param|=6.24e+02 |g_param|=4.79e+05 loss=1.8578e+00 ppl=6.41
Validation - loss=2.4788e+00 ppl=11.93 best_loss=2.4408e+00 best_ppl=11.48
Epoch 60 - |param|=6.25e+02 |g_param|=5.18e+05 loss=1.8991e+00 ppl=6.68
Validation - loss=2.4793e+00 ppl=11.93 best_loss=2.4408e+00 best_ppl=11.48
Epoch 61 - |param|=6.25e+02 |g_param|=4.87e+05 loss=1.8584e+00 ppl=6.41
Validation - loss=2.4996e+00 ppl=12.18 best_loss=2.4408e+00 best_ppl=11.48
Epoch 62 - |param|=6.25e+02 |g_param|=8.35e+05 loss=1.7988e+00 ppl=6.04
Validation - loss=2.4840e+00 ppl=11.99 best_loss=2.4408e+00 best_ppl=11.48
Epoch 63 - |param|=6.26e+02 |g_param|=7.66e+05 loss=1.8112e+00 ppl=6.12
Validation - loss=2.5030e+00 ppl=12.22 best_loss=2.4408e+00 best_ppl=11.48
Epoch 64 - |param|=6.26e+02 |g_param|=5.10e+05 loss=1.7992e+00 ppl=6.04
Validation - loss=2.5128e+00 ppl=12.34 best_loss=2.4408e+00 best_ppl=11.48
Epoch 65 - |param|=6.27e+02 |g_param|=4.87e+05 loss=1.7363e+00 ppl=5.68
Validation - loss=2.5017e+00 ppl=12.20 best_loss=2.4408e+00 best_ppl=11.48
Epoch 66 - |param|=6.27e+02 |g_param|=5.32e+05 loss=1.7681e+00 ppl=5.86
Validation - loss=2.5428e+00 ppl=12.72 best_loss=2.4408e+00 best_ppl=11.48
Epoch 67 - |param|=6.27e+02 |g_param|=5.26e+05 loss=1.8164e+00 ppl=6.15
Validation - loss=2.5354e+00 ppl=12.62 best_loss=2.4408e+00 best_ppl=11.48
Epoch 68 - |param|=6.28e+02 |g_param|=5.09e+05 loss=1.7253e+00 ppl=5.61
Validation - loss=2.5273e+00 ppl=12.52 best_loss=2.4408e+00 best_ppl=11.48
Epoch 69 - |param|=6.28e+02 |g_param|=5.11e+05 loss=1.6850e+00 ppl=5.39
Validation - loss=2.5030e+00 ppl=12.22 best_loss=2.4408e+00 best_ppl=11.48
Epoch 70 - |param|=6.29e+02 |g_param|=5.21e+05 loss=1.6516e+00 ppl=5.22
Validation - loss=2.5466e+00 ppl=12.76 best_loss=2.4408e+00 best_ppl=11.48
Epoch 71 - |param|=6.29e+02 |g_param|=5.07e+05 loss=1.6447e+00 ppl=5.18
Validation - loss=2.5043e+00 ppl=12.24 best_loss=2.4408e+00 best_ppl=11.48
Epoch 72 - |param|=6.29e+02 |g_param|=5.32e+05 loss=1.6170e+00 ppl=5.04
Validation - loss=2.5169e+00 ppl=12.39 best_loss=2.4408e+00 best_ppl=11.48
Epoch 73 - |param|=6.30e+02 |g_param|=5.03e+05 loss=1.5968e+00 ppl=4.94
Validation - loss=2.5051e+00 ppl=12.24 best_loss=2.4408e+00 best_ppl=11.48
Epoch 74 - |param|=6.30e+02 |g_param|=5.36e+05 loss=1.5974e+00 ppl=4.94
Validation - loss=2.5724e+00 ppl=13.10 best_loss=2.4408e+00 best_ppl=11.48
Epoch 75 - |param|=6.31e+02 |g_param|=5.29e+05 loss=1.6197e+00 ppl=5.05
Validation - loss=2.5505e+00 ppl=12.81 best_loss=2.4408e+00 best_ppl=11.48
Epoch 76 - |param|=6.31e+02 |g_param|=5.56e+05 loss=1.5774e+00 ppl=4.84
Validation - loss=2.5331e+00 ppl=12.59 best_loss=2.4408e+00 best_ppl=11.48
Epoch 77 - |param|=6.31e+02 |g_param|=5.29e+05 loss=1.5821e+00 ppl=4.86
Validation - loss=2.5656e+00 ppl=13.01 best_loss=2.4408e+00 best_ppl=11.48
Epoch 78 - |param|=6.32e+02 |g_param|=5.82e+05 loss=1.5723e+00 ppl=4.82
Validation - loss=2.5575e+00 ppl=12.90 best_loss=2.4408e+00 best_ppl=11.48
Epoch 79 - |param|=6.32e+02 |g_param|=5.55e+05 loss=1.5606e+00 ppl=4.76
Validation - loss=2.5618e+00 ppl=12.96 best_loss=2.4408e+00 best_ppl=11.48
Epoch 80 - |param|=6.33e+02 |g_param|=5.80e+05 loss=1.5244e+00 ppl=4.59
Validation - loss=2.5302e+00 ppl=12.56 best_loss=2.4408e+00 best_ppl=11.48
Epoch 81 - |param|=6.33e+02 |g_param|=5.70e+05 loss=1.5318e+00 ppl=4.63
Validation - loss=2.5729e+00 ppl=13.10 best_loss=2.4408e+00 best_ppl=11.48
Epoch 82 - |param|=6.33e+02 |g_param|=5.69e+05 loss=1.5399e+00 ppl=4.66
Validation - loss=2.5809e+00 ppl=13.21 best_loss=2.4408e+00 best_ppl=11.48
Epoch 83 - |param|=6.34e+02 |g_param|=5.51e+05 loss=1.4843e+00 ppl=4.41
Validation - loss=2.6111e+00 ppl=13.61 best_loss=2.4408e+00 best_ppl=11.48
Epoch 84 - |param|=6.34e+02 |g_param|=5.81e+05 loss=1.4440e+00 ppl=4.24
Validation - loss=2.5722e+00 ppl=13.09 best_loss=2.4408e+00 best_ppl=11.48
Epoch 85 - |param|=6.34e+02 |g_param|=5.53e+05 loss=1.4498e+00 ppl=4.26
Validation - loss=2.6057e+00 ppl=13.54 best_loss=2.4408e+00 best_ppl=11.48
Epoch 86 - |param|=6.35e+02 |g_param|=6.11e+05 loss=1.5461e+00 ppl=4.69
Validation - loss=2.6236e+00 ppl=13.78 best_loss=2.4408e+00 best_ppl=11.48
Epoch 87 - |param|=6.35e+02 |g_param|=5.74e+05 loss=1.4941e+00 ppl=4.46
Validation - loss=2.6291e+00 ppl=13.86 best_loss=2.4408e+00 best_ppl=11.48
Epoch 88 - |param|=6.36e+02 |g_param|=6.02e+05 loss=1.4952e+00 ppl=4.46
Validation - loss=2.6074e+00 ppl=13.56 best_loss=2.4408e+00 best_ppl=11.48
Epoch 89 - |param|=6.36e+02 |g_param|=6.09e+05 loss=1.4893e+00 ppl=4.43
Validation - loss=2.6382e+00 ppl=13.99 best_loss=2.4408e+00 best_ppl=11.48
Epoch 90 - |param|=6.36e+02 |g_param|=5.84e+05 loss=1.3960e+00 ppl=4.04
Validation - loss=2.6283e+00 ppl=13.85 best_loss=2.4408e+00 best_ppl=11.48
Epoch 91 - |param|=6.37e+02 |g_param|=5.92e+05 loss=1.3949e+00 ppl=4.03
Validation - loss=2.6541e+00 ppl=14.21 best_loss=2.4408e+00 best_ppl=11.48
Epoch 92 - |param|=6.37e+02 |g_param|=5.89e+05 loss=1.3662e+00 ppl=3.92
Validation - loss=2.6681e+00 ppl=14.41 best_loss=2.4408e+00 best_ppl=11.48
Epoch 93 - |param|=6.37e+02 |g_param|=5.68e+05 loss=1.3502e+00 ppl=3.86
Validation - loss=2.6962e+00 ppl=14.82 best_loss=2.4408e+00 best_ppl=11.48
Epoch 94 - |param|=6.38e+02 |g_param|=6.16e+05 loss=1.3816e+00 ppl=3.98
Validation - loss=2.6880e+00 ppl=14.70 best_loss=2.4408e+00 best_ppl=11.48
Epoch 95 - |param|=6.38e+02 |g_param|=5.92e+05 loss=1.3641e+00 ppl=3.91
Validation - loss=2.6637e+00 ppl=14.35 best_loss=2.4408e+00 best_ppl=11.48
Epoch 96 - |param|=6.39e+02 |g_param|=1.10e+06 loss=1.3116e+00 ppl=3.71
Validation - loss=2.6630e+00 ppl=14.34 best_loss=2.4408e+00 best_ppl=11.48
Epoch 97 - |param|=6.39e+02 |g_param|=1.19e+06 loss=1.3053e+00 ppl=3.69
Validation - loss=2.6842e+00 ppl=14.65 best_loss=2.4408e+00 best_ppl=11.48
Epoch 98 - |param|=6.39e+02 |g_param|=1.31e+06 loss=1.3479e+00 ppl=3.85
Validation - loss=2.6767e+00 ppl=14.54 best_loss=2.4408e+00 best_ppl=11.48
Epoch 99 - |param|=6.40e+02 |g_param|=1.20e+06 loss=1.2801e+00 ppl=3.60
Validation - loss=2.6532e+00 ppl=14.20 best_loss=2.4408e+00 best_ppl=11.48
Epoch 100 - |param|=6.40e+02 |g_param|=1.31e+06 loss=1.3374e+00 ppl=3.81
Validation - loss=2.6753e+00 ppl=14.52 best_loss=2.4408e+00 best_ppl=11.48
bkmy, seq2seq-RL training start for 50 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-50epoch/seq-model-bkmy.47.2.18-8.88.2.44-11.52.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-50epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 48
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 48,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-50epoch/seq-model-bkmy.47.2.18-8.88.2.44-11.52.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-50epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 48 - |param|=6.19e+02 |g_param|=4.39e+05 loss=2.1334e+00 ppl=8.44
Validation - loss=2.4393e+00 ppl=11.47 best_loss=inf best_ppl=inf
Epoch 49 - |param|=6.19e+02 |g_param|=4.19e+05 loss=2.0805e+00 ppl=8.01
Validation - loss=2.4530e+00 ppl=11.62 best_loss=2.4393e+00 best_ppl=11.47
Epoch 50 - |param|=6.20e+02 |g_param|=4.78e+05 loss=2.1100e+00 ppl=8.25
Validation - loss=2.4411e+00 ppl=11.49 best_loss=2.4393e+00 best_ppl=11.47
Epoch 51 - |param|=6.20e+02 |g_param|=4.38e+05 loss=2.0594e+00 ppl=7.84
Validation - loss=2.4499e+00 ppl=11.59 best_loss=2.4393e+00 best_ppl=11.47
Epoch 52 - |param|=6.20e+02 |g_param|=4.78e+05 loss=2.0778e+00 ppl=7.99
Validation - loss=2.4651e+00 ppl=11.76 best_loss=2.4393e+00 best_ppl=11.47
Epoch 53 - |param|=6.21e+02 |g_param|=4.54e+05 loss=2.0525e+00 ppl=7.79
Validation - loss=2.4415e+00 ppl=11.49 best_loss=2.4393e+00 best_ppl=11.47
Epoch 54 - |param|=6.21e+02 |g_param|=4.96e+05 loss=2.0358e+00 ppl=7.66
Validation - loss=2.4585e+00 ppl=11.69 best_loss=2.4393e+00 best_ppl=11.47
Epoch 55 - |param|=6.22e+02 |g_param|=4.80e+05 loss=1.9620e+00 ppl=7.11
Validation - loss=2.4558e+00 ppl=11.66 best_loss=2.4393e+00 best_ppl=11.47
Epoch 56 - |param|=6.22e+02 |g_param|=4.59e+05 loss=1.9589e+00 ppl=7.09
Validation - loss=2.4524e+00 ppl=11.62 best_loss=2.4393e+00 best_ppl=11.47
Epoch 57 - |param|=6.22e+02 |g_param|=4.82e+05 loss=1.9805e+00 ppl=7.25
Validation - loss=2.4768e+00 ppl=11.90 best_loss=2.4393e+00 best_ppl=11.47
Epoch 58 - |param|=6.23e+02 |g_param|=4.78e+05 loss=1.9570e+00 ppl=7.08
Validation - loss=2.4443e+00 ppl=11.52 best_loss=2.4393e+00 best_ppl=11.47
Epoch 59 - |param|=6.23e+02 |g_param|=4.72e+05 loss=1.8674e+00 ppl=6.47
Validation - loss=2.4498e+00 ppl=11.59 best_loss=2.4393e+00 best_ppl=11.47
Epoch 60 - |param|=6.24e+02 |g_param|=5.16e+05 loss=1.8992e+00 ppl=6.68
Validation - loss=2.4621e+00 ppl=11.73 best_loss=2.4393e+00 best_ppl=11.47
Epoch 61 - |param|=6.24e+02 |g_param|=4.82e+05 loss=1.8358e+00 ppl=6.27
Validation - loss=2.4565e+00 ppl=11.66 best_loss=2.4393e+00 best_ppl=11.47
Epoch 62 - |param|=6.24e+02 |g_param|=5.14e+05 loss=1.8179e+00 ppl=6.16
Validation - loss=2.4588e+00 ppl=11.69 best_loss=2.4393e+00 best_ppl=11.47
Epoch 63 - |param|=6.25e+02 |g_param|=5.08e+05 loss=1.8167e+00 ppl=6.15
Validation - loss=2.4537e+00 ppl=11.63 best_loss=2.4393e+00 best_ppl=11.47
Epoch 64 - |param|=6.25e+02 |g_param|=5.28e+05 loss=1.8023e+00 ppl=6.06
Validation - loss=2.4616e+00 ppl=11.72 best_loss=2.4393e+00 best_ppl=11.47
Epoch 65 - |param|=6.26e+02 |g_param|=5.24e+05 loss=1.8020e+00 ppl=6.06
Validation - loss=2.4830e+00 ppl=11.98 best_loss=2.4393e+00 best_ppl=11.47
Epoch 66 - |param|=6.26e+02 |g_param|=5.44e+05 loss=1.7362e+00 ppl=5.68
Validation - loss=2.4581e+00 ppl=11.68 best_loss=2.4393e+00 best_ppl=11.47
Epoch 67 - |param|=6.26e+02 |g_param|=5.19e+05 loss=1.7277e+00 ppl=5.63
Validation - loss=2.4861e+00 ppl=12.01 best_loss=2.4393e+00 best_ppl=11.47
Epoch 68 - |param|=6.27e+02 |g_param|=5.44e+05 loss=1.7847e+00 ppl=5.96
Validation - loss=2.4699e+00 ppl=11.82 best_loss=2.4393e+00 best_ppl=11.47
Epoch 69 - |param|=6.27e+02 |g_param|=5.32e+05 loss=1.6950e+00 ppl=5.45
Validation - loss=2.4816e+00 ppl=11.96 best_loss=2.4393e+00 best_ppl=11.47
Epoch 70 - |param|=6.28e+02 |g_param|=5.47e+05 loss=1.7021e+00 ppl=5.49
Validation - loss=2.4692e+00 ppl=11.81 best_loss=2.4393e+00 best_ppl=11.47
Epoch 71 - |param|=6.28e+02 |g_param|=5.33e+05 loss=1.6453e+00 ppl=5.18
Validation - loss=2.5094e+00 ppl=12.30 best_loss=2.4393e+00 best_ppl=11.47
Epoch 72 - |param|=6.28e+02 |g_param|=5.45e+05 loss=1.6306e+00 ppl=5.11
Validation - loss=2.5090e+00 ppl=12.29 best_loss=2.4393e+00 best_ppl=11.47
Epoch 73 - |param|=6.29e+02 |g_param|=5.39e+05 loss=1.6248e+00 ppl=5.08
Validation - loss=2.5115e+00 ppl=12.32 best_loss=2.4393e+00 best_ppl=11.47
Epoch 74 - |param|=6.29e+02 |g_param|=5.27e+05 loss=1.5878e+00 ppl=4.89
Validation - loss=2.5180e+00 ppl=12.40 best_loss=2.4393e+00 best_ppl=11.47
Epoch 75 - |param|=6.30e+02 |g_param|=5.45e+05 loss=1.5916e+00 ppl=4.91
Validation - loss=2.5048e+00 ppl=12.24 best_loss=2.4393e+00 best_ppl=11.47
Epoch 76 - |param|=6.30e+02 |g_param|=5.51e+05 loss=1.5793e+00 ppl=4.85
Validation - loss=2.5157e+00 ppl=12.37 best_loss=2.4393e+00 best_ppl=11.47
Epoch 77 - |param|=6.30e+02 |g_param|=5.51e+05 loss=1.5834e+00 ppl=4.87
Validation - loss=2.5193e+00 ppl=12.42 best_loss=2.4393e+00 best_ppl=11.47
Epoch 78 - |param|=6.31e+02 |g_param|=5.72e+05 loss=1.5745e+00 ppl=4.83
Validation - loss=2.5320e+00 ppl=12.58 best_loss=2.4393e+00 best_ppl=11.47
Epoch 79 - |param|=6.31e+02 |g_param|=5.69e+05 loss=1.6049e+00 ppl=4.98
Validation - loss=2.5082e+00 ppl=12.28 best_loss=2.4393e+00 best_ppl=11.47
Epoch 80 - |param|=6.31e+02 |g_param|=9.77e+05 loss=1.5639e+00 ppl=4.78
Validation - loss=2.5157e+00 ppl=12.38 best_loss=2.4393e+00 best_ppl=11.47
Epoch 81 - |param|=6.32e+02 |g_param|=6.56e+05 loss=1.5267e+00 ppl=4.60
Validation - loss=2.5227e+00 ppl=12.46 best_loss=2.4393e+00 best_ppl=11.47
Epoch 82 - |param|=6.32e+02 |g_param|=6.05e+05 loss=1.4845e+00 ppl=4.41
Validation - loss=2.5452e+00 ppl=12.75 best_loss=2.4393e+00 best_ppl=11.47
Epoch 83 - |param|=6.33e+02 |g_param|=5.68e+05 loss=1.5071e+00 ppl=4.51
Validation - loss=2.5631e+00 ppl=12.98 best_loss=2.4393e+00 best_ppl=11.47
Epoch 84 - |param|=6.33e+02 |g_param|=5.69e+05 loss=1.4328e+00 ppl=4.19
Validation - loss=2.5618e+00 ppl=12.96 best_loss=2.4393e+00 best_ppl=11.47
Epoch 85 - |param|=6.33e+02 |g_param|=5.74e+05 loss=1.4349e+00 ppl=4.20
Validation - loss=2.5578e+00 ppl=12.91 best_loss=2.4393e+00 best_ppl=11.47
Epoch 86 - |param|=6.34e+02 |g_param|=5.89e+05 loss=1.4651e+00 ppl=4.33
Validation - loss=2.5717e+00 ppl=13.09 best_loss=2.4393e+00 best_ppl=11.47
Epoch 87 - |param|=6.34e+02 |g_param|=6.03e+05 loss=1.4350e+00 ppl=4.20
Validation - loss=2.5377e+00 ppl=12.65 best_loss=2.4393e+00 best_ppl=11.47
Epoch 88 - |param|=6.34e+02 |g_param|=5.90e+05 loss=1.4646e+00 ppl=4.33
Validation - loss=2.5773e+00 ppl=13.16 best_loss=2.4393e+00 best_ppl=11.47
Epoch 89 - |param|=6.35e+02 |g_param|=5.77e+05 loss=1.3942e+00 ppl=4.03
Validation - loss=2.5934e+00 ppl=13.37 best_loss=2.4393e+00 best_ppl=11.47
Epoch 90 - |param|=6.35e+02 |g_param|=5.88e+05 loss=1.3714e+00 ppl=3.94
Validation - loss=2.5904e+00 ppl=13.34 best_loss=2.4393e+00 best_ppl=11.47
Epoch 91 - |param|=6.35e+02 |g_param|=6.27e+05 loss=1.4411e+00 ppl=4.23
Validation - loss=2.6049e+00 ppl=13.53 best_loss=2.4393e+00 best_ppl=11.47
Epoch 92 - |param|=6.36e+02 |g_param|=5.89e+05 loss=1.3370e+00 ppl=3.81
Validation - loss=2.5912e+00 ppl=13.35 best_loss=2.4393e+00 best_ppl=11.47
Epoch 93 - |param|=6.36e+02 |g_param|=6.02e+05 loss=1.3651e+00 ppl=3.92
Validation - loss=2.6182e+00 ppl=13.71 best_loss=2.4393e+00 best_ppl=11.47
Epoch 94 - |param|=6.36e+02 |g_param|=6.43e+05 loss=1.3649e+00 ppl=3.92
Validation - loss=2.5862e+00 ppl=13.28 best_loss=2.4393e+00 best_ppl=11.47
Epoch 95 - |param|=6.37e+02 |g_param|=6.08e+05 loss=1.3666e+00 ppl=3.92
Validation - loss=2.5884e+00 ppl=13.31 best_loss=2.4393e+00 best_ppl=11.47
Epoch 96 - |param|=6.37e+02 |g_param|=6.22e+05 loss=1.3297e+00 ppl=3.78
Validation - loss=2.5997e+00 ppl=13.46 best_loss=2.4393e+00 best_ppl=11.47
Epoch 97 - |param|=6.38e+02 |g_param|=6.16e+05 loss=1.3435e+00 ppl=3.83
Validation - loss=2.6178e+00 ppl=13.71 best_loss=2.4393e+00 best_ppl=11.47
Epoch 98 - |param|=6.38e+02 |g_param|=6.48e+05 loss=1.3374e+00 ppl=3.81
Validation - loss=2.6153e+00 ppl=13.67 best_loss=2.4393e+00 best_ppl=11.47
Epoch 99 - |param|=6.38e+02 |g_param|=6.34e+05 loss=1.3436e+00 ppl=3.83
Validation - loss=2.6123e+00 ppl=13.63 best_loss=2.4393e+00 best_ppl=11.47
Epoch 100 - |param|=6.39e+02 |g_param|=6.26e+05 loss=1.2755e+00 ppl=3.58
Validation - loss=2.6457e+00 ppl=14.09 best_loss=2.4393e+00 best_ppl=11.47
bkmy, seq2seq-RL training start for 60 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-60epoch/seq-model-bkmy.57.1.85-6.35.2.36-10.55.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-60epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 58
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 58,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-60epoch/seq-model-bkmy.57.1.85-6.35.2.36-10.55.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-60epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 58 - |param|=6.25e+02 |g_param|=4.94e+05 loss=1.8148e+00 ppl=6.14
Validation - loss=2.3749e+00 ppl=10.75 best_loss=inf best_ppl=inf
Epoch 59 - |param|=6.26e+02 |g_param|=4.96e+05 loss=1.8790e+00 ppl=6.55
Validation - loss=2.3834e+00 ppl=10.84 best_loss=2.3749e+00 best_ppl=10.75
Epoch 60 - |param|=6.26e+02 |g_param|=5.04e+05 loss=1.7632e+00 ppl=5.83
Validation - loss=2.3852e+00 ppl=10.86 best_loss=2.3749e+00 best_ppl=10.75
Epoch 61 - |param|=6.26e+02 |g_param|=4.80e+05 loss=1.7693e+00 ppl=5.87
Validation - loss=2.4039e+00 ppl=11.07 best_loss=2.3749e+00 best_ppl=10.75
Epoch 62 - |param|=6.27e+02 |g_param|=5.08e+05 loss=1.7519e+00 ppl=5.77
Validation - loss=2.4068e+00 ppl=11.10 best_loss=2.3749e+00 best_ppl=10.75
Epoch 63 - |param|=6.27e+02 |g_param|=4.99e+05 loss=1.8101e+00 ppl=6.11
Validation - loss=2.3555e+00 ppl=10.54 best_loss=2.3749e+00 best_ppl=10.75
Epoch 64 - |param|=6.28e+02 |g_param|=5.29e+05 loss=1.7776e+00 ppl=5.92
Validation - loss=2.3945e+00 ppl=10.96 best_loss=2.3555e+00 best_ppl=10.54
Epoch 65 - |param|=6.28e+02 |g_param|=4.95e+05 loss=1.6599e+00 ppl=5.26
Validation - loss=2.3875e+00 ppl=10.89 best_loss=2.3555e+00 best_ppl=10.54
Epoch 66 - |param|=6.28e+02 |g_param|=5.20e+05 loss=1.6691e+00 ppl=5.31
Validation - loss=2.3928e+00 ppl=10.94 best_loss=2.3555e+00 best_ppl=10.54
Epoch 67 - |param|=6.29e+02 |g_param|=5.17e+05 loss=1.6767e+00 ppl=5.35
Validation - loss=2.3912e+00 ppl=10.93 best_loss=2.3555e+00 best_ppl=10.54
Epoch 68 - |param|=6.29e+02 |g_param|=5.41e+05 loss=1.6589e+00 ppl=5.25
Validation - loss=2.3889e+00 ppl=10.90 best_loss=2.3555e+00 best_ppl=10.54
Epoch 69 - |param|=6.30e+02 |g_param|=5.01e+05 loss=1.6127e+00 ppl=5.02
Validation - loss=2.4180e+00 ppl=11.22 best_loss=2.3555e+00 best_ppl=10.54
Epoch 70 - |param|=6.30e+02 |g_param|=5.40e+05 loss=1.6136e+00 ppl=5.02
Validation - loss=2.4339e+00 ppl=11.40 best_loss=2.3555e+00 best_ppl=10.54
Epoch 71 - |param|=6.30e+02 |g_param|=5.36e+05 loss=1.6050e+00 ppl=4.98
Validation - loss=2.4037e+00 ppl=11.06 best_loss=2.3555e+00 best_ppl=10.54
Epoch 72 - |param|=6.31e+02 |g_param|=5.54e+05 loss=1.5801e+00 ppl=4.86
Validation - loss=2.4041e+00 ppl=11.07 best_loss=2.3555e+00 best_ppl=10.54
Epoch 73 - |param|=6.31e+02 |g_param|=5.71e+05 loss=1.6630e+00 ppl=5.28
Validation - loss=2.4293e+00 ppl=11.35 best_loss=2.3555e+00 best_ppl=10.54
Epoch 74 - |param|=6.32e+02 |g_param|=5.57e+05 loss=1.5383e+00 ppl=4.66
Validation - loss=2.4430e+00 ppl=11.51 best_loss=2.3555e+00 best_ppl=10.54
Epoch 75 - |param|=6.32e+02 |g_param|=5.54e+05 loss=1.5952e+00 ppl=4.93
Validation - loss=2.4645e+00 ppl=11.76 best_loss=2.3555e+00 best_ppl=10.54
Epoch 76 - |param|=6.32e+02 |g_param|=5.66e+05 loss=1.5093e+00 ppl=4.52
Validation - loss=2.4622e+00 ppl=11.73 best_loss=2.3555e+00 best_ppl=10.54
Epoch 77 - |param|=6.33e+02 |g_param|=5.65e+05 loss=1.5381e+00 ppl=4.66
Validation - loss=2.4721e+00 ppl=11.85 best_loss=2.3555e+00 best_ppl=10.54
Epoch 78 - |param|=6.33e+02 |g_param|=5.62e+05 loss=1.5150e+00 ppl=4.55
Validation - loss=2.5166e+00 ppl=12.39 best_loss=2.3555e+00 best_ppl=10.54
Epoch 79 - |param|=6.34e+02 |g_param|=5.69e+05 loss=1.5563e+00 ppl=4.74
Validation - loss=2.4821e+00 ppl=11.97 best_loss=2.3555e+00 best_ppl=10.54
Epoch 80 - |param|=6.34e+02 |g_param|=5.90e+05 loss=1.4834e+00 ppl=4.41
Validation - loss=2.4606e+00 ppl=11.71 best_loss=2.3555e+00 best_ppl=10.54
Epoch 81 - |param|=6.34e+02 |g_param|=5.55e+05 loss=1.4457e+00 ppl=4.24
Validation - loss=2.4704e+00 ppl=11.83 best_loss=2.3555e+00 best_ppl=10.54
Epoch 82 - |param|=6.35e+02 |g_param|=6.25e+05 loss=1.5856e+00 ppl=4.88
Validation - loss=2.4660e+00 ppl=11.77 best_loss=2.3555e+00 best_ppl=10.54
Epoch 83 - |param|=6.35e+02 |g_param|=5.88e+05 loss=1.5288e+00 ppl=4.61
Validation - loss=2.5125e+00 ppl=12.34 best_loss=2.3555e+00 best_ppl=10.54
Epoch 84 - |param|=6.36e+02 |g_param|=5.94e+05 loss=1.4783e+00 ppl=4.39
Validation - loss=2.4754e+00 ppl=11.89 best_loss=2.3555e+00 best_ppl=10.54
Epoch 85 - |param|=6.36e+02 |g_param|=5.85e+05 loss=1.5067e+00 ppl=4.51
Validation - loss=2.5451e+00 ppl=12.74 best_loss=2.3555e+00 best_ppl=10.54
Epoch 86 - |param|=6.36e+02 |g_param|=6.09e+05 loss=1.4256e+00 ppl=4.16
Validation - loss=2.5168e+00 ppl=12.39 best_loss=2.3555e+00 best_ppl=10.54
Epoch 87 - |param|=6.37e+02 |g_param|=5.74e+05 loss=1.3743e+00 ppl=3.95
Validation - loss=2.5296e+00 ppl=12.55 best_loss=2.3555e+00 best_ppl=10.54
Epoch 88 - |param|=6.37e+02 |g_param|=6.04e+05 loss=1.3916e+00 ppl=4.02
Validation - loss=2.5221e+00 ppl=12.45 best_loss=2.3555e+00 best_ppl=10.54
Epoch 89 - |param|=6.37e+02 |g_param|=5.92e+05 loss=1.3638e+00 ppl=3.91
Validation - loss=2.5422e+00 ppl=12.71 best_loss=2.3555e+00 best_ppl=10.54
Epoch 90 - |param|=6.38e+02 |g_param|=1.03e+06 loss=1.3468e+00 ppl=3.85
Validation - loss=2.5309e+00 ppl=12.56 best_loss=2.3555e+00 best_ppl=10.54
Epoch 91 - |param|=6.38e+02 |g_param|=6.31e+05 loss=1.3162e+00 ppl=3.73
Validation - loss=2.5320e+00 ppl=12.58 best_loss=2.3555e+00 best_ppl=10.54
Epoch 92 - |param|=6.39e+02 |g_param|=6.12e+05 loss=1.3751e+00 ppl=3.96
Validation - loss=2.5347e+00 ppl=12.61 best_loss=2.3555e+00 best_ppl=10.54
Epoch 93 - |param|=6.39e+02 |g_param|=5.95e+05 loss=1.3171e+00 ppl=3.73
Validation - loss=2.5504e+00 ppl=12.81 best_loss=2.3555e+00 best_ppl=10.54
Epoch 94 - |param|=6.39e+02 |g_param|=6.43e+05 loss=1.3873e+00 ppl=4.00
Validation - loss=2.5545e+00 ppl=12.87 best_loss=2.3555e+00 best_ppl=10.54
Epoch 95 - |param|=6.40e+02 |g_param|=6.21e+05 loss=1.2943e+00 ppl=3.65
Validation - loss=2.5574e+00 ppl=12.90 best_loss=2.3555e+00 best_ppl=10.54
Epoch 96 - |param|=6.40e+02 |g_param|=6.06e+05 loss=1.2603e+00 ppl=3.53
Validation - loss=2.5686e+00 ppl=13.05 best_loss=2.3555e+00 best_ppl=10.54
Epoch 97 - |param|=6.40e+02 |g_param|=6.19e+05 loss=1.3048e+00 ppl=3.69
Validation - loss=2.5798e+00 ppl=13.19 best_loss=2.3555e+00 best_ppl=10.54
Epoch 98 - |param|=6.41e+02 |g_param|=6.31e+05 loss=1.2796e+00 ppl=3.60
Validation - loss=2.6101e+00 ppl=13.60 best_loss=2.3555e+00 best_ppl=10.54
Epoch 99 - |param|=6.41e+02 |g_param|=6.16e+05 loss=1.2934e+00 ppl=3.65
Validation - loss=2.5930e+00 ppl=13.37 best_loss=2.3555e+00 best_ppl=10.54
Epoch 100 - |param|=6.42e+02 |g_param|=6.22e+05 loss=1.2950e+00 ppl=3.65
Validation - loss=2.6141e+00 ppl=13.66 best_loss=2.3555e+00 best_ppl=10.54
bkmy, seq2seq-RL training start for 70 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-70epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 65
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 65,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-70epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 65 - |param|=6.27e+02 |g_param|=4.77e+05 loss=1.6796e+00 ppl=5.36
Validation - loss=2.0957e+00 ppl=8.13 best_loss=inf best_ppl=inf
Epoch 66 - |param|=6.27e+02 |g_param|=4.81e+05 loss=1.7481e+00 ppl=5.74
Validation - loss=2.0908e+00 ppl=8.09 best_loss=2.0957e+00 best_ppl=8.13
Epoch 67 - |param|=6.28e+02 |g_param|=4.91e+05 loss=1.6466e+00 ppl=5.19
Validation - loss=2.0845e+00 ppl=8.04 best_loss=2.0908e+00 best_ppl=8.09
Epoch 68 - |param|=6.28e+02 |g_param|=4.86e+05 loss=1.5973e+00 ppl=4.94
Validation - loss=2.0882e+00 ppl=8.07 best_loss=2.0845e+00 best_ppl=8.04
Epoch 69 - |param|=6.29e+02 |g_param|=5.03e+05 loss=1.5823e+00 ppl=4.87
Validation - loss=2.0731e+00 ppl=7.95 best_loss=2.0845e+00 best_ppl=8.04
Epoch 70 - |param|=6.29e+02 |g_param|=5.27e+05 loss=1.6710e+00 ppl=5.32
Validation - loss=2.0807e+00 ppl=8.01 best_loss=2.0731e+00 best_ppl=7.95
Epoch 71 - |param|=6.29e+02 |g_param|=4.88e+05 loss=1.5371e+00 ppl=4.65
Validation - loss=2.0869e+00 ppl=8.06 best_loss=2.0731e+00 best_ppl=7.95
Epoch 72 - |param|=6.30e+02 |g_param|=5.08e+05 loss=1.6173e+00 ppl=5.04
Validation - loss=2.0820e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95
Epoch 73 - |param|=6.30e+02 |g_param|=5.68e+05 loss=1.6505e+00 ppl=5.21
Validation - loss=2.0880e+00 ppl=8.07 best_loss=2.0731e+00 best_ppl=7.95
Epoch 74 - |param|=6.31e+02 |g_param|=4.99e+05 loss=1.5553e+00 ppl=4.74
Validation - loss=2.0823e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95
Epoch 75 - |param|=6.31e+02 |g_param|=5.00e+05 loss=1.4954e+00 ppl=4.46
Validation - loss=2.0823e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95
Epoch 76 - |param|=6.31e+02 |g_param|=5.12e+05 loss=1.5131e+00 ppl=4.54
Validation - loss=2.0804e+00 ppl=8.01 best_loss=2.0731e+00 best_ppl=7.95
Epoch 77 - |param|=6.32e+02 |g_param|=5.11e+05 loss=1.5670e+00 ppl=4.79
Validation - loss=2.0953e+00 ppl=8.13 best_loss=2.0731e+00 best_ppl=7.95
Epoch 78 - |param|=6.32e+02 |g_param|=5.64e+05 loss=1.4101e+00 ppl=4.10
Validation - loss=2.0921e+00 ppl=8.10 best_loss=2.0731e+00 best_ppl=7.95
Epoch 79 - |param|=6.33e+02 |g_param|=5.07e+05 loss=1.4307e+00 ppl=4.18
Validation - loss=2.0976e+00 ppl=8.15 best_loss=2.0731e+00 best_ppl=7.95
Epoch 80 - |param|=6.33e+02 |g_param|=5.25e+05 loss=1.3833e+00 ppl=3.99
Validation - loss=2.1271e+00 ppl=8.39 best_loss=2.0731e+00 best_ppl=7.95
Epoch 81 - |param|=6.33e+02 |g_param|=5.34e+05 loss=1.4005e+00 ppl=4.06
Validation - loss=2.1233e+00 ppl=8.36 best_loss=2.0731e+00 best_ppl=7.95
Epoch 82 - |param|=6.34e+02 |g_param|=5.40e+05 loss=1.4110e+00 ppl=4.10
Validation - loss=2.1043e+00 ppl=8.20 best_loss=2.0731e+00 best_ppl=7.95
Epoch 83 - |param|=6.34e+02 |g_param|=5.23e+05 loss=1.3662e+00 ppl=3.92
Validation - loss=2.1241e+00 ppl=8.37 best_loss=2.0731e+00 best_ppl=7.95
Epoch 84 - |param|=6.35e+02 |g_param|=5.27e+05 loss=1.3184e+00 ppl=3.74
Validation - loss=2.1029e+00 ppl=8.19 best_loss=2.0731e+00 best_ppl=7.95
Epoch 85 - |param|=6.35e+02 |g_param|=5.20e+05 loss=1.2926e+00 ppl=3.64
Validation - loss=2.1314e+00 ppl=8.43 best_loss=2.0731e+00 best_ppl=7.95
Epoch 86 - |param|=6.35e+02 |g_param|=5.53e+05 loss=1.2931e+00 ppl=3.64
Validation - loss=2.1005e+00 ppl=8.17 best_loss=2.0731e+00 best_ppl=7.95
Epoch 87 - |param|=6.36e+02 |g_param|=5.39e+05 loss=1.3500e+00 ppl=3.86
Validation - loss=2.1060e+00 ppl=8.22 best_loss=2.0731e+00 best_ppl=7.95
Epoch 88 - |param|=6.36e+02 |g_param|=5.64e+05 loss=1.2832e+00 ppl=3.61
Validation - loss=2.1276e+00 ppl=8.40 best_loss=2.0731e+00 best_ppl=7.95
Epoch 89 - |param|=6.37e+02 |g_param|=5.58e+05 loss=1.2727e+00 ppl=3.57
Validation - loss=2.1434e+00 ppl=8.53 best_loss=2.0731e+00 best_ppl=7.95
Epoch 90 - |param|=6.37e+02 |g_param|=5.56e+05 loss=1.2030e+00 ppl=3.33
Validation - loss=2.1229e+00 ppl=8.36 best_loss=2.0731e+00 best_ppl=7.95
Epoch 91 - |param|=6.37e+02 |g_param|=5.35e+05 loss=1.2204e+00 ppl=3.39
Validation - loss=2.0999e+00 ppl=8.17 best_loss=2.0731e+00 best_ppl=7.95
Epoch 92 - |param|=6.38e+02 |g_param|=5.90e+05 loss=1.2290e+00 ppl=3.42
Validation - loss=2.1183e+00 ppl=8.32 best_loss=2.0731e+00 best_ppl=7.95
Epoch 93 - |param|=6.38e+02 |g_param|=5.49e+05 loss=1.1836e+00 ppl=3.27
Validation - loss=2.1541e+00 ppl=8.62 best_loss=2.0731e+00 best_ppl=7.95
Epoch 94 - |param|=6.38e+02 |g_param|=3.62e+05 loss=1.2032e+00 ppl=3.33
Validation - loss=2.1366e+00 ppl=8.47 best_loss=2.0731e+00 best_ppl=7.95
Epoch 95 - |param|=6.39e+02 |g_param|=2.83e+05 loss=1.1877e+00 ppl=3.28
Validation - loss=2.1312e+00 ppl=8.42 best_loss=2.0731e+00 best_ppl=7.95
Epoch 96 - |param|=6.39e+02 |g_param|=3.03e+05 loss=1.2826e+00 ppl=3.61
Validation - loss=2.1215e+00 ppl=8.34 best_loss=2.0731e+00 best_ppl=7.95
Epoch 97 - |param|=6.40e+02 |g_param|=2.86e+05 loss=1.2256e+00 ppl=3.41
Validation - loss=2.1507e+00 ppl=8.59 best_loss=2.0731e+00 best_ppl=7.95
Epoch 98 - |param|=6.40e+02 |g_param|=2.02e+05 loss=1.1788e+00 ppl=3.25
Validation - loss=2.1397e+00 ppl=8.50 best_loss=2.0731e+00 best_ppl=7.95
Epoch 99 - |param|=6.40e+02 |g_param|=1.46e+05 loss=1.2412e+00 ppl=3.46
Validation - loss=2.1317e+00 ppl=8.43 best_loss=2.0731e+00 best_ppl=7.95
Epoch 100 - |param|=6.41e+02 |g_param|=1.41e+05 loss=1.1487e+00 ppl=3.15
Validation - loss=2.1882e+00 ppl=8.92 best_loss=2.0731e+00 best_ppl=7.95
```

Continue-Training of Seq2Seq-RL ရဲ့ ကြာချိန်က အောက်ပါအတိုင်း...  

```
real	89m41.581s
user	87m52.417s
sys	1m56.495s
```

## Transformer Baseline Training Log (for my-bk, bk-my)
