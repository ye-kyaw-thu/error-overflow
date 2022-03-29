# Baseline for Myanmar-Rakhine language pair

## Seq2Seq Baseline (my-rk)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train/media/ye/project2/exp/myrk-transformer/data/syl/train \
> --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev \
> --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 100 \
> --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
> --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
> --use_adam --rl_n_epochs 0 \
> --model_fn ./model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.pth | tee ./model/seq2seq/baseline/myrk-100epoch/myrk-seq2seq-baseline-train.log;
usage: train.py [-h] --model_fn MODEL_FN --train TRAIN --valid VALID --lang
                LANG [--gpu_id GPU_ID] [--off_autocast]
                [--batch_size BATCH_SIZE] [--n_epochs N_EPOCHS]
                [--verbose VERBOSE] [--init_epoch INIT_EPOCH]
                [--max_length MAX_LENGTH] [--dropout DROPOUT]
                [--word_vec_size WORD_VEC_SIZE] [--hidden_size HIDDEN_SIZE]
                [--n_layers N_LAYERS] [--max_grad_norm MAX_GRAD_NORM]
                [--iteration_per_update ITERATION_PER_UPDATE] [--lr LR]
                [--lr_step LR_STEP] [--lr_gamma LR_GAMMA]
                [--lr_decay_start LR_DECAY_START] [--use_adam] [--use_radam]
                [--rl_lr RL_LR] [--rl_n_samples RL_N_SAMPLES]
                [--rl_n_epochs RL_N_EPOCHS] [--rl_n_gram RL_N_GRAM]
                [--rl_reward RL_REWARD] [--use_transformer]
                [--n_splits N_SPLITS]
train.py: error: the following arguments are required: --train

real	0m0.841s
user	0m1.012s
sys	0m1.064s
(simple-nmt) ye@:~/exp/simple-nmt$ 
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
> --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev \
> --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 100 \
> --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
> --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
> --use_adam --rl_n_epochs 0 \
> --model_fn ./model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.pth | tee ./model/seq2seq/baseline/myrk-100epoch/myrk-seq2seq-baseline-train.log;
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
    'model_fn': './model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/media/ye/project2/exp/myrk-transformer/data/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/media/ye/project2/exp/myrk-transformer/data/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1585, 128)
  (emb_dec): Embedding(1695, 128)
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
    (output): Linear(in_features=128, out_features=1695, bias=True)
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
Epoch 1 - |param|=6.52e+02 |g_param|=2.04e+05 loss=4.2095e+00 ppl=67.32                                                 
Validation - loss=3.5795e+00 ppl=35.86 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.52e+02 |g_param|=1.73e+05 loss=3.9838e+00 ppl=53.72                                                 
Validation - loss=3.3718e+00 ppl=29.13 best_loss=3.5795e+00 best_ppl=35.86                                              
Epoch 3 - |param|=6.52e+02 |g_param|=1.80e+05 loss=3.8927e+00 ppl=49.04                                                 
Validation - loss=3.2486e+00 ppl=25.76 best_loss=3.3718e+00 best_ppl=29.13                                              
Epoch 4 - |param|=6.53e+02 |g_param|=1.75e+05 loss=3.7851e+00 ppl=44.04                                                 
Validation - loss=3.0991e+00 ppl=22.18 best_loss=3.2486e+00 best_ppl=25.76                                              
Epoch 5 - |param|=6.53e+02 |g_param|=1.12e+05 loss=3.6328e+00 ppl=37.82                                                 
Validation - loss=2.9749e+00 ppl=19.59 best_loss=3.0991e+00 best_ppl=22.18                                              
Epoch 6 - |param|=6.54e+02 |g_param|=1.02e+05 loss=3.5390e+00 ppl=34.43                                                 
Validation - loss=2.8221e+00 ppl=16.81 best_loss=2.9749e+00 best_ppl=19.59                                              
Epoch 7 - |param|=6.54e+02 |g_param|=1.28e+05 loss=3.3189e+00 ppl=27.63                                                 
Validation - loss=2.6161e+00 ppl=13.68 best_loss=2.8221e+00 best_ppl=16.81                                              
Epoch 8 - |param|=6.55e+02 |g_param|=1.62e+05 loss=2.9465e+00 ppl=19.04                                                 
Validation - loss=2.2958e+00 ppl=9.93 best_loss=2.6161e+00 best_ppl=13.68                                               
Epoch 9 - |param|=6.56e+02 |g_param|=1.84e+05 loss=2.6683e+00 ppl=14.42                                                 
Validation - loss=2.0126e+00 ppl=7.48 best_loss=2.2958e+00 best_ppl=9.93                                                
Epoch 10 - |param|=6.57e+02 |g_param|=2.33e+05 loss=2.4775e+00 ppl=11.91                                                
Validation - loss=1.8651e+00 ppl=6.46 best_loss=2.0126e+00 best_ppl=7.48                                                
Epoch 11 - |param|=6.58e+02 |g_param|=2.34e+05 loss=2.2755e+00 ppl=9.73                                                 
Validation - loss=1.7395e+00 ppl=5.69 best_loss=1.8651e+00 best_ppl=6.46                                                
Epoch 12 - |param|=6.59e+02 |g_param|=7.56e+04 loss=2.0028e+00 ppl=7.41                                                 
Validation - loss=1.5198e+00 ppl=4.57 best_loss=1.7395e+00 best_ppl=5.69                                                
Epoch 13 - |param|=6.59e+02 |g_param|=1.12e+05 loss=1.9367e+00 ppl=6.94                                                 
Validation - loss=1.3982e+00 ppl=4.05 best_loss=1.5198e+00 best_ppl=4.57                                                
Epoch 14 - |param|=6.60e+02 |g_param|=1.14e+05 loss=1.8114e+00 ppl=6.12                                                 
Validation - loss=1.3039e+00 ppl=3.68 best_loss=1.3982e+00 best_ppl=4.05                                                
Epoch 15 - |param|=6.61e+02 |g_param|=1.19e+05 loss=1.6465e+00 ppl=5.19                                                 
Validation - loss=1.2223e+00 ppl=3.40 best_loss=1.3039e+00 best_ppl=3.68                                                
Epoch 16 - |param|=6.61e+02 |g_param|=1.09e+05 loss=1.6186e+00 ppl=5.05                                                 
Validation - loss=1.1605e+00 ppl=3.19 best_loss=1.2223e+00 best_ppl=3.40                                                
Epoch 17 - |param|=6.62e+02 |g_param|=5.10e+04 loss=1.4601e+00 ppl=4.31                                                 
Validation - loss=1.1574e+00 ppl=3.18 best_loss=1.1605e+00 best_ppl=3.19                                                
Epoch 18 - |param|=6.62e+02 |g_param|=6.41e+04 loss=1.3701e+00 ppl=3.94                                                 
Validation - loss=9.9233e-01 ppl=2.70 best_loss=1.1574e+00 best_ppl=3.18                                                
Epoch 19 - |param|=6.63e+02 |g_param|=7.03e+04 loss=1.3722e+00 ppl=3.94                                                 
Validation - loss=1.1054e+00 ppl=3.02 best_loss=9.9233e-01 best_ppl=2.70                                                
Epoch 20 - |param|=6.64e+02 |g_param|=7.01e+04 loss=1.2345e+00 ppl=3.44                                                 
Validation - loss=9.3880e-01 ppl=2.56 best_loss=9.9233e-01 best_ppl=2.70                                                
Epoch 21 - |param|=6.64e+02 |g_param|=5.83e+04 loss=1.1163e+00 ppl=3.05                                                 
Validation - loss=8.4996e-01 ppl=2.34 best_loss=9.3880e-01 best_ppl=2.56                                                
Epoch 22 - |param|=6.65e+02 |g_param|=4.02e+04 loss=1.0552e+00 ppl=2.87                                                 
Validation - loss=8.3246e-01 ppl=2.30 best_loss=8.4996e-01 best_ppl=2.34                                                
Epoch 23 - |param|=6.65e+02 |g_param|=4.68e+04 loss=9.7298e-01 ppl=2.65                                                 
Validation - loss=7.9729e-01 ppl=2.22 best_loss=8.3246e-01 best_ppl=2.30                                                
Epoch 24 - |param|=6.66e+02 |g_param|=7.03e+04 loss=1.0051e+00 ppl=2.73                                                 
Validation - loss=8.2367e-01 ppl=2.28 best_loss=7.9729e-01 best_ppl=2.22                                                
Epoch 25 - |param|=6.66e+02 |g_param|=5.76e+04 loss=9.0730e-01 ppl=2.48                                                 
Validation - loss=7.7496e-01 ppl=2.17 best_loss=7.9729e-01 best_ppl=2.22                                                
Epoch 26 - |param|=6.67e+02 |g_param|=5.24e+04 loss=8.4228e-01 ppl=2.32                                                 
Validation - loss=6.9669e-01 ppl=2.01 best_loss=7.7496e-01 best_ppl=2.17                                                
Epoch 27 - |param|=6.67e+02 |g_param|=4.78e+04 loss=7.7683e-01 ppl=2.17                                                 
Validation - loss=6.5210e-01 ppl=1.92 best_loss=6.9669e-01 best_ppl=2.01                                                
Epoch 28 - |param|=6.68e+02 |g_param|=2.78e+04 loss=7.3617e-01 ppl=2.09                                                 
Validation - loss=6.1481e-01 ppl=1.85 best_loss=6.5210e-01 best_ppl=1.92                                                
Epoch 29 - |param|=6.68e+02 |g_param|=1.97e+04 loss=7.2329e-01 ppl=2.06                                                 
Validation - loss=6.1759e-01 ppl=1.85 best_loss=6.1481e-01 best_ppl=1.85                                                
Epoch 30 - |param|=6.69e+02 |g_param|=2.65e+04 loss=7.2986e-01 ppl=2.07                                                 
Validation - loss=5.9495e-01 ppl=1.81 best_loss=6.1481e-01 best_ppl=1.85                                                
Epoch 31 - |param|=6.69e+02 |g_param|=2.23e+04 loss=6.5804e-01 ppl=1.93                                                 
Validation - loss=5.9995e-01 ppl=1.82 best_loss=5.9495e-01 best_ppl=1.81                                                
Epoch 32 - |param|=6.70e+02 |g_param|=1.87e+04 loss=6.3006e-01 ppl=1.88                                                 
Validation - loss=5.7876e-01 ppl=1.78 best_loss=5.9495e-01 best_ppl=1.81                                                
Epoch 33 - |param|=6.70e+02 |g_param|=2.93e+04 loss=7.0973e-01 ppl=2.03                                                 
Validation - loss=6.0326e-01 ppl=1.83 best_loss=5.7876e-01 best_ppl=1.78                                                
Epoch 34 - |param|=6.70e+02 |g_param|=3.20e+04 loss=6.8083e-01 ppl=1.98                                                 
Validation - loss=6.5387e-01 ppl=1.92 best_loss=5.7876e-01 best_ppl=1.78                                                
Epoch 35 - |param|=6.71e+02 |g_param|=1.82e+04 loss=5.9429e-01 ppl=1.81                                                 
Validation - loss=5.4461e-01 ppl=1.72 best_loss=5.7876e-01 best_ppl=1.78                                                
Epoch 36 - |param|=6.71e+02 |g_param|=1.83e+04 loss=5.7385e-01 ppl=1.78                                                 
Validation - loss=5.3042e-01 ppl=1.70 best_loss=5.4461e-01 best_ppl=1.72                                                
Epoch 37 - |param|=6.72e+02 |g_param|=3.19e+04 loss=6.2856e-01 ppl=1.87                                                 
Validation - loss=6.1526e-01 ppl=1.85 best_loss=5.3042e-01 best_ppl=1.70                                                
Epoch 38 - |param|=6.72e+02 |g_param|=2.26e+04 loss=5.6084e-01 ppl=1.75                                                 
Validation - loss=5.2580e-01 ppl=1.69 best_loss=5.3042e-01 best_ppl=1.70                                                
Epoch 39 - |param|=6.73e+02 |g_param|=1.69e+04 loss=5.2352e-01 ppl=1.69                                                 
Validation - loss=5.1568e-01 ppl=1.67 best_loss=5.2580e-01 best_ppl=1.69                                                
Epoch 40 - |param|=6.73e+02 |g_param|=2.38e+04 loss=5.2507e-01 ppl=1.69                                                 
Validation - loss=5.4308e-01 ppl=1.72 best_loss=5.1568e-01 best_ppl=1.67                                                
Epoch 41 - |param|=6.73e+02 |g_param|=2.43e+04 loss=5.1465e-01 ppl=1.67                                                 
Validation - loss=5.4593e-01 ppl=1.73 best_loss=5.1568e-01 best_ppl=1.67                                                
Epoch 42 - |param|=6.74e+02 |g_param|=1.25e+04 loss=4.6617e-01 ppl=1.59                                                 
Validation - loss=4.9122e-01 ppl=1.63 best_loss=5.1568e-01 best_ppl=1.67                                                
Epoch 43 - |param|=6.74e+02 |g_param|=1.39e+04 loss=4.5231e-01 ppl=1.57                                                 
Validation - loss=4.9608e-01 ppl=1.64 best_loss=4.9122e-01 best_ppl=1.63                                                
Epoch 44 - |param|=6.74e+02 |g_param|=1.20e+04 loss=4.5123e-01 ppl=1.57                                                 
Validation - loss=4.8314e-01 ppl=1.62 best_loss=4.9122e-01 best_ppl=1.63                                                
Epoch 45 - |param|=6.75e+02 |g_param|=2.49e+04 loss=4.3162e-01 ppl=1.54                                                 
Validation - loss=4.7651e-01 ppl=1.61 best_loss=4.8314e-01 best_ppl=1.62                                                
Epoch 46 - |param|=6.75e+02 |g_param|=3.54e+04 loss=4.4484e-01 ppl=1.56                                                 
Validation - loss=5.0094e-01 ppl=1.65 best_loss=4.7651e-01 best_ppl=1.61                                                
Epoch 47 - |param|=6.76e+02 |g_param|=2.86e+04 loss=4.3253e-01 ppl=1.54                                                 
Validation - loss=4.7361e-01 ppl=1.61 best_loss=4.7651e-01 best_ppl=1.61                                                
Epoch 48 - |param|=6.76e+02 |g_param|=2.59e+04 loss=4.0607e-01 ppl=1.50                                                 
Validation - loss=4.6800e-01 ppl=1.60 best_loss=4.7361e-01 best_ppl=1.61                                                
Epoch 49 - |param|=6.76e+02 |g_param|=2.27e+04 loss=3.9774e-01 ppl=1.49                                                 
Validation - loss=4.5877e-01 ppl=1.58 best_loss=4.6800e-01 best_ppl=1.60                                                
Epoch 50 - |param|=6.77e+02 |g_param|=3.65e+04 loss=4.3320e-01 ppl=1.54                                                 
Validation - loss=4.8443e-01 ppl=1.62 best_loss=4.5877e-01 best_ppl=1.58                                                
Epoch 51 - |param|=6.77e+02 |g_param|=3.38e+04 loss=3.9617e-01 ppl=1.49                                                 
Validation - loss=4.6026e-01 ppl=1.58 best_loss=4.5877e-01 best_ppl=1.58                                                
Epoch 52 - |param|=6.77e+02 |g_param|=2.66e+04 loss=3.8471e-01 ppl=1.47                                                 
Validation - loss=4.5009e-01 ppl=1.57 best_loss=4.5877e-01 best_ppl=1.58                                                
Epoch 53 - |param|=6.78e+02 |g_param|=4.53e+04 loss=4.4539e-01 ppl=1.56                                                 
Validation - loss=4.6797e-01 ppl=1.60 best_loss=4.5009e-01 best_ppl=1.57                                                
Epoch 54 - |param|=6.78e+02 |g_param|=2.02e+04 loss=4.1854e-01 ppl=1.52                                                 
Validation - loss=4.5878e-01 ppl=1.58 best_loss=4.5009e-01 best_ppl=1.57                                                
Epoch 55 - |param|=6.79e+02 |g_param|=1.27e+04 loss=4.0358e-01 ppl=1.50                                                 
Validation - loss=4.4389e-01 ppl=1.56 best_loss=4.5009e-01 best_ppl=1.57                                                
Epoch 56 - |param|=6.79e+02 |g_param|=1.75e+04 loss=3.7055e-01 ppl=1.45                                                 
Validation - loss=4.7167e-01 ppl=1.60 best_loss=4.4389e-01 best_ppl=1.56                                                
Epoch 57 - |param|=6.79e+02 |g_param|=2.27e+04 loss=3.9555e-01 ppl=1.49                                                 
Validation - loss=4.4313e-01 ppl=1.56 best_loss=4.4389e-01 best_ppl=1.56                                                
Epoch 58 - |param|=6.80e+02 |g_param|=1.62e+04 loss=3.7164e-01 ppl=1.45                                                 
Validation - loss=4.4815e-01 ppl=1.57 best_loss=4.4313e-01 best_ppl=1.56                                                
Epoch 59 - |param|=6.80e+02 |g_param|=1.62e+04 loss=3.7851e-01 ppl=1.46                                                 
Validation - loss=4.4289e-01 ppl=1.56 best_loss=4.4313e-01 best_ppl=1.56                                                
Epoch 60 - |param|=6.80e+02 |g_param|=1.35e+04 loss=3.4698e-01 ppl=1.41                                                 
Validation - loss=4.2871e-01 ppl=1.54 best_loss=4.4289e-01 best_ppl=1.56                                                
Epoch 61 - |param|=6.81e+02 |g_param|=1.15e+04 loss=3.3644e-01 ppl=1.40                                                 
Validation - loss=4.4456e-01 ppl=1.56 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 62 - |param|=6.81e+02 |g_param|=1.02e+04 loss=3.1747e-01 ppl=1.37                                                 
Validation - loss=4.3163e-01 ppl=1.54 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 63 - |param|=6.81e+02 |g_param|=1.17e+04 loss=3.1575e-01 ppl=1.37                                                 
Validation - loss=4.3715e-01 ppl=1.55 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 64 - |param|=6.82e+02 |g_param|=1.63e+04 loss=3.3071e-01 ppl=1.39                                                 
Validation - loss=4.6026e-01 ppl=1.58 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 65 - |param|=6.82e+02 |g_param|=2.24e+04 loss=3.4899e-01 ppl=1.42                                                 
Validation - loss=4.8699e-01 ppl=1.63 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 66 - |param|=6.83e+02 |g_param|=2.88e+04 loss=4.1623e-01 ppl=1.52                                                 
Validation - loss=4.7478e-01 ppl=1.61 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 67 - |param|=6.83e+02 |g_param|=1.30e+04 loss=3.2580e-01 ppl=1.39                                                 
Validation - loss=4.1134e-01 ppl=1.51 best_loss=4.2871e-01 best_ppl=1.54                                                
Epoch 68 - |param|=6.83e+02 |g_param|=1.00e+04 loss=3.1257e-01 ppl=1.37                                                 
Validation - loss=4.1280e-01 ppl=1.51 best_loss=4.1134e-01 best_ppl=1.51                                                
Epoch 69 - |param|=6.84e+02 |g_param|=1.12e+04 loss=2.9735e-01 ppl=1.35                                                 
Validation - loss=4.2832e-01 ppl=1.53 best_loss=4.1134e-01 best_ppl=1.51                                                
Epoch 70 - |param|=6.84e+02 |g_param|=2.05e+04 loss=2.9896e-01 ppl=1.35                                                 
Validation - loss=4.0979e-01 ppl=1.51 best_loss=4.1134e-01 best_ppl=1.51                                                
Epoch 71 - |param|=6.84e+02 |g_param|=2.21e+04 loss=2.8548e-01 ppl=1.33                                                 
Validation - loss=4.1981e-01 ppl=1.52 best_loss=4.0979e-01 best_ppl=1.51                                                
Epoch 72 - |param|=6.85e+02 |g_param|=2.02e+04 loss=2.9056e-01 ppl=1.34                                                 
Validation - loss=4.1865e-01 ppl=1.52 best_loss=4.0979e-01 best_ppl=1.51                                                
Epoch 73 - |param|=6.85e+02 |g_param|=2.04e+04 loss=2.8897e-01 ppl=1.34                                                 
Validation - loss=4.2094e-01 ppl=1.52 best_loss=4.0979e-01 best_ppl=1.51                                                
Epoch 74 - |param|=6.85e+02 |g_param|=2.17e+04 loss=2.7818e-01 ppl=1.32                                                 
Validation - loss=4.0802e-01 ppl=1.50 best_loss=4.0979e-01 best_ppl=1.51                                                
Epoch 75 - |param|=6.86e+02 |g_param|=1.75e+04 loss=2.7106e-01 ppl=1.31                                                 
Validation - loss=3.9546e-01 ppl=1.49 best_loss=4.0802e-01 best_ppl=1.50                                                
Epoch 76 - |param|=6.86e+02 |g_param|=2.39e+04 loss=2.8646e-01 ppl=1.33                                                 
Validation - loss=4.2630e-01 ppl=1.53 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 77 - |param|=6.86e+02 |g_param|=2.73e+04 loss=2.7831e-01 ppl=1.32                                                 
Validation - loss=4.1965e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 78 - |param|=6.87e+02 |g_param|=2.66e+04 loss=2.8235e-01 ppl=1.33                                                 
Validation - loss=4.3534e-01 ppl=1.55 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 79 - |param|=6.87e+02 |g_param|=2.09e+04 loss=2.6800e-01 ppl=1.31                                                 
Validation - loss=4.1671e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 80 - |param|=6.87e+02 |g_param|=2.07e+04 loss=2.6127e-01 ppl=1.30                                                 
Validation - loss=4.0372e-01 ppl=1.50 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 81 - |param|=6.88e+02 |g_param|=1.87e+04 loss=2.4900e-01 ppl=1.28                                                 
Validation - loss=4.2140e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 82 - |param|=6.88e+02 |g_param|=4.59e+04 loss=3.4231e-01 ppl=1.41                                                 
Validation - loss=4.5091e-01 ppl=1.57 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 83 - |param|=6.88e+02 |g_param|=2.11e+04 loss=2.9409e-01 ppl=1.34                                                 
Validation - loss=4.1438e-01 ppl=1.51 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 84 - |param|=6.89e+02 |g_param|=1.10e+04 loss=2.4827e-01 ppl=1.28                                                 
Validation - loss=4.2090e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 85 - |param|=6.89e+02 |g_param|=1.30e+04 loss=2.5584e-01 ppl=1.29                                                 
Validation - loss=4.1286e-01 ppl=1.51 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 86 - |param|=6.89e+02 |g_param|=1.02e+04 loss=2.4314e-01 ppl=1.28                                                 
Validation - loss=4.1564e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 87 - |param|=6.90e+02 |g_param|=1.06e+04 loss=2.3777e-01 ppl=1.27                                                 
Validation - loss=4.0076e-01 ppl=1.49 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 88 - |param|=6.90e+02 |g_param|=9.15e+03 loss=2.3289e-01 ppl=1.26                                                 
Validation - loss=4.1782e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 89 - |param|=6.90e+02 |g_param|=1.06e+04 loss=2.3078e-01 ppl=1.26                                                 
Validation - loss=4.1671e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 90 - |param|=6.91e+02 |g_param|=9.50e+03 loss=2.3327e-01 ppl=1.26                                                 
Validation - loss=4.0936e-01 ppl=1.51 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 91 - |param|=6.91e+02 |g_param|=1.19e+04 loss=2.4294e-01 ppl=1.27                                                 
Validation - loss=4.2300e-01 ppl=1.53 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 92 - |param|=6.91e+02 |g_param|=1.73e+04 loss=2.5628e-01 ppl=1.29                                                 
Validation - loss=4.2069e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 93 - |param|=6.92e+02 |g_param|=1.06e+04 loss=2.3473e-01 ppl=1.26                                                 
Validation - loss=4.2608e-01 ppl=1.53 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 94 - |param|=6.92e+02 |g_param|=1.27e+04 loss=2.4175e-01 ppl=1.27                                                 
Validation - loss=4.2903e-01 ppl=1.54 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 95 - |param|=6.93e+02 |g_param|=1.04e+04 loss=2.3163e-01 ppl=1.26                                                 
Validation - loss=4.0874e-01 ppl=1.50 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 96 - |param|=6.93e+02 |g_param|=9.03e+03 loss=2.2531e-01 ppl=1.25                                                 
Validation - loss=4.2041e-01 ppl=1.52 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 97 - |param|=6.93e+02 |g_param|=1.14e+04 loss=2.1541e-01 ppl=1.24                                                 
Validation - loss=4.1324e-01 ppl=1.51 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 98 - |param|=6.94e+02 |g_param|=2.12e+04 loss=2.5188e-01 ppl=1.29                                                 
Validation - loss=4.6022e-01 ppl=1.58 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 99 - |param|=6.94e+02 |g_param|=1.67e+04 loss=2.5917e-01 ppl=1.30                                                 
Validation - loss=4.3651e-01 ppl=1.55 best_loss=3.9546e-01 best_ppl=1.49                                                
Epoch 100 - |param|=6.94e+02 |g_param|=1.74e+04 loss=2.1689e-01 ppl=1.24                                                
Validation - loss=4.1103e-01 ppl=1.51 best_loss=3.9546e-01 best_ppl=1.49                                                

real	21m14.452s
user	20m54.919s
sys	0m17.451s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```

```

## Seq2Seq Baseline (rk-my)

```

```

testing/evaluation...  

```

```


## Transformer Baseline (my-rk)

```

```

testing/evaluation... 

```

```

## Transformer Baseline (rk-my)

```

```

testing/evaluation...   

```

```
