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
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-baseline-myrk.sh 
Evaluation result for the model: seq-model-myrk.01.4.21-67.32.3.58-35.86.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.0/1.8/0.0/0.0 (BP=1.000, ratio=1.070, hyp_len=24779, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.3.98-53.72.3.37-29.13.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.6/2.0/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=23375, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.3.89-49.04.3.25-25.76.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/1.7/0.0/0.0 (BP=1.000, ratio=1.006, hyp_len=23302, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.79-44.04.3.10-22.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/2.6/0.1/0.0 (BP=1.000, ratio=1.003, hyp_len=23218, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.63-37.82.2.97-19.59.pth
BLEU = 1.34, 26.5/4.7/0.7/0.0 (BP=1.000, ratio=1.005, hyp_len=23269, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.54-34.43.2.82-16.81.pth
BLEU = 2.94, 29.1/7.3/1.5/0.2 (BP=1.000, ratio=1.011, hyp_len=23417, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.32-27.63.2.62-13.68.pth
BLEU = 3.59, 34.8/10.9/2.1/0.2 (BP=1.000, ratio=1.001, hyp_len=23172, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.2.95-19.04.2.30-9.93.pth
BLEU = 8.62, 40.2/16.2/5.3/1.6 (BP=1.000, ratio=1.001, hyp_len=23188, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.2.67-14.42.2.01-7.48.pth
BLEU = 12.90, 45.8/20.8/8.6/3.4 (BP=1.000, ratio=1.002, hyp_len=23214, ref_len=23160)
Evaluation result for the model: seq-model-myrk.100.0.22-1.24.0.41-1.51.pth
BLEU = 74.95, 87.7/78.6/71.0/64.5 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.2.48-11.91.1.87-6.46.pth
BLEU = 16.31, 49.0/24.2/11.4/5.3 (BP=1.000, ratio=1.005, hyp_len=23277, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.2.28-9.73.1.74-5.69.pth
BLEU = 20.41, 53.2/28.6/15.2/7.7 (BP=0.993, ratio=0.993, hyp_len=22998, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.2.00-7.41.1.52-4.57.pth
BLEU = 24.05, 56.6/32.4/18.3/10.0 (BP=1.000, ratio=1.002, hyp_len=23204, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.1.94-6.94.1.40-4.05.pth
BLEU = 28.88, 60.7/37.1/22.8/13.6 (BP=0.997, ratio=0.997, hyp_len=23099, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.1.81-6.12.1.30-3.68.pth
BLEU = 32.25, 62.9/40.4/25.8/16.5 (BP=1.000, ratio=1.005, hyp_len=23268, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.1.65-5.19.1.22-3.40.pth
BLEU = 35.92, 65.8/44.1/29.4/19.5 (BP=1.000, ratio=1.002, hyp_len=23198, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.1.62-5.05.1.16-3.19.pth
BLEU = 38.40, 67.9/46.4/31.9/21.7 (BP=1.000, ratio=1.006, hyp_len=23308, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.1.46-4.31.1.16-3.18.pth
BLEU = 40.32, 70.0/48.9/34.2/23.8 (BP=0.987, ratio=0.987, hyp_len=22856, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.37-3.94.0.99-2.70.pth
BLEU = 46.51, 73.1/53.8/40.0/29.8 (BP=0.999, ratio=0.999, hyp_len=23139, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.37-3.94.1.11-3.02.pth
BLEU = 39.36, 68.8/48.2/32.9/22.0 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.23-3.44.0.94-2.56.pth
BLEU = 48.44, 74.0/55.7/42.0/31.8 (BP=1.000, ratio=1.016, hyp_len=23540, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.12-3.05.0.85-2.34.pth
BLEU = 55.27, 78.4/61.6/49.1/39.3 (BP=1.000, ratio=1.003, hyp_len=23237, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.1.06-2.87.0.83-2.30.pth
BLEU = 56.86, 79.3/63.0/50.8/41.2 (BP=1.000, ratio=1.003, hyp_len=23234, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.0.97-2.65.0.80-2.22.pth
BLEU = 56.74, 79.2/63.1/50.6/41.0 (BP=1.000, ratio=1.011, hyp_len=23424, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.1.01-2.73.0.82-2.28.pth
BLEU = 57.69, 79.5/63.9/51.8/42.1 (BP=1.000, ratio=1.011, hyp_len=23406, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.0.91-2.48.0.77-2.17.pth
BLEU = 60.15, 81.9/66.8/55.0/45.5 (BP=0.989, ratio=0.989, hyp_len=22898, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.0.84-2.32.0.70-2.01.pth
BLEU = 62.21, 81.9/67.8/56.7/47.6 (BP=1.000, ratio=1.014, hyp_len=23478, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.0.78-2.17.0.65-1.92.pth
BLEU = 65.19, 83.7/70.5/59.9/51.1 (BP=1.000, ratio=1.009, hyp_len=23371, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.74-2.09.0.61-1.85.pth
BLEU = 66.29, 84.3/71.4/61.1/52.5 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.72-2.06.0.62-1.85.pth
BLEU = 65.55, 83.8/70.7/60.2/51.7 (BP=1.000, ratio=1.012, hyp_len=23441, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.73-2.07.0.59-1.81.pth
BLEU = 66.00, 83.9/71.1/60.8/52.3 (BP=1.000, ratio=1.016, hyp_len=23534, ref_len=23160)
Evaluation result for the model: seq-model-myrk.31.0.66-1.93.0.60-1.82.pth
BLEU = 68.07, 85.1/72.9/63.1/54.8 (BP=1.000, ratio=1.008, hyp_len=23334, ref_len=23160)
Evaluation result for the model: seq-model-myrk.32.0.63-1.88.0.58-1.78.pth
BLEU = 65.74, 83.5/70.9/60.6/52.1 (BP=1.000, ratio=1.018, hyp_len=23579, ref_len=23160)
Evaluation result for the model: seq-model-myrk.33.0.71-2.03.0.60-1.83.pth
BLEU = 66.81, 84.3/72.0/61.7/53.2 (BP=1.000, ratio=1.018, hyp_len=23573, ref_len=23160)
Evaluation result for the model: seq-model-myrk.34.0.68-1.98.0.65-1.92.pth
BLEU = 66.53, 84.7/71.7/61.3/52.6 (BP=1.000, ratio=1.003, hyp_len=23227, ref_len=23160)
Evaluation result for the model: seq-model-myrk.35.0.59-1.81.0.54-1.72.pth
BLEU = 69.57, 85.7/74.2/64.8/56.9 (BP=1.000, ratio=1.015, hyp_len=23516, ref_len=23160)
Evaluation result for the model: seq-model-myrk.36.0.57-1.78.0.53-1.70.pth
BLEU = 69.91, 85.7/74.4/65.2/57.4 (BP=1.000, ratio=1.016, hyp_len=23538, ref_len=23160)
Evaluation result for the model: seq-model-myrk.37.0.63-1.87.0.62-1.85.pth
BLEU = 65.38, 83.6/71.1/60.2/51.0 (BP=1.000, ratio=1.029, hyp_len=23825, ref_len=23160)
Evaluation result for the model: seq-model-myrk.38.0.56-1.75.0.53-1.69.pth
BLEU = 70.09, 86.0/74.6/65.4/57.5 (BP=1.000, ratio=1.014, hyp_len=23493, ref_len=23160)
Evaluation result for the model: seq-model-myrk.39.0.52-1.69.0.52-1.67.pth
BLEU = 70.09, 85.8/74.6/65.4/57.7 (BP=1.000, ratio=1.020, hyp_len=23622, ref_len=23160)
Evaluation result for the model: seq-model-myrk.40.0.53-1.69.0.54-1.72.pth
BLEU = 69.84, 85.8/74.6/65.2/57.1 (BP=1.000, ratio=1.024, hyp_len=23706, ref_len=23160)
Evaluation result for the model: seq-model-myrk.41.0.51-1.67.0.55-1.73.pth
BLEU = 69.55, 86.0/74.4/64.7/56.6 (BP=1.000, ratio=1.010, hyp_len=23402, ref_len=23160)
Evaluation result for the model: seq-model-myrk.42.0.47-1.59.0.49-1.63.pth
BLEU = 71.52, 86.3/75.8/67.1/59.6 (BP=1.000, ratio=1.026, hyp_len=23761, ref_len=23160)
Evaluation result for the model: seq-model-myrk.43.0.45-1.57.0.50-1.64.pth
BLEU = 72.15, 86.8/76.3/67.7/60.4 (BP=1.000, ratio=1.020, hyp_len=23612, ref_len=23160)
Evaluation result for the model: seq-model-myrk.44.0.45-1.57.0.48-1.62.pth
BLEU = 71.96, 86.5/76.1/67.5/60.3 (BP=1.000, ratio=1.027, hyp_len=23778, ref_len=23160)
Evaluation result for the model: seq-model-myrk.45.0.43-1.54.0.48-1.61.pth
BLEU = 73.07, 87.4/77.2/68.8/61.5 (BP=1.000, ratio=1.023, hyp_len=23686, ref_len=23160)
Evaluation result for the model: seq-model-myrk.46.0.44-1.56.0.50-1.65.pth
BLEU = 70.64, 86.0/75.1/66.1/58.3 (BP=1.000, ratio=1.026, hyp_len=23758, ref_len=23160)
Evaluation result for the model: seq-model-myrk.47.0.43-1.54.0.47-1.61.pth
BLEU = 73.08, 87.2/77.1/68.8/61.6 (BP=1.000, ratio=1.024, hyp_len=23724, ref_len=23160)
Evaluation result for the model: seq-model-myrk.48.0.41-1.50.0.47-1.60.pth
BLEU = 73.59, 87.5/77.6/69.3/62.3 (BP=1.000, ratio=1.021, hyp_len=23645, ref_len=23160)
Evaluation result for the model: seq-model-myrk.49.0.40-1.49.0.46-1.58.pth
BLEU = 73.29, 87.4/77.3/69.0/61.9 (BP=1.000, ratio=1.021, hyp_len=23647, ref_len=23160)
Evaluation result for the model: seq-model-myrk.50.0.43-1.54.0.48-1.62.pth
BLEU = 72.31, 86.9/76.5/67.8/60.6 (BP=1.000, ratio=1.019, hyp_len=23589, ref_len=23160)
Evaluation result for the model: seq-model-myrk.51.0.40-1.49.0.46-1.58.pth
BLEU = 71.73, 86.6/76.1/67.3/59.7 (BP=1.000, ratio=1.024, hyp_len=23726, ref_len=23160)
Evaluation result for the model: seq-model-myrk.52.0.38-1.47.0.45-1.57.pth
BLEU = 72.63, 86.8/76.8/68.3/61.1 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq-model-myrk.53.0.45-1.56.0.47-1.60.pth
BLEU = 70.99, 86.0/75.4/66.5/58.9 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: seq-model-myrk.54.0.42-1.52.0.46-1.58.pth
BLEU = 70.57, 85.8/75.0/66.1/58.4 (BP=1.000, ratio=1.024, hyp_len=23720, ref_len=23160)
Evaluation result for the model: seq-model-myrk.55.0.40-1.50.0.44-1.56.pth
BLEU = 72.67, 86.7/76.7/68.4/61.3 (BP=1.000, ratio=1.030, hyp_len=23849, ref_len=23160)
Evaluation result for the model: seq-model-myrk.56.0.37-1.45.0.47-1.60.pth
BLEU = 72.73, 87.1/76.7/68.4/61.2 (BP=1.000, ratio=1.014, hyp_len=23473, ref_len=23160)
Evaluation result for the model: seq-model-myrk.57.0.40-1.49.0.44-1.56.pth
BLEU = 70.75, 85.7/75.0/66.3/58.7 (BP=1.000, ratio=1.026, hyp_len=23769, ref_len=23160)
Evaluation result for the model: seq-model-myrk.58.0.37-1.45.0.45-1.57.pth
BLEU = 72.55, 86.8/76.6/68.2/61.1 (BP=1.000, ratio=1.021, hyp_len=23651, ref_len=23160)
Evaluation result for the model: seq-model-myrk.59.0.38-1.46.0.44-1.56.pth
BLEU = 73.34, 87.2/77.3/69.1/62.2 (BP=1.000, ratio=1.025, hyp_len=23743, ref_len=23160)
Evaluation result for the model: seq-model-myrk.60.0.35-1.41.0.43-1.54.pth
BLEU = 73.76, 87.3/77.7/69.6/62.7 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
Evaluation result for the model: seq-model-myrk.61.0.34-1.40.0.44-1.56.pth
BLEU = 73.40, 87.3/77.3/69.1/62.2 (BP=1.000, ratio=1.022, hyp_len=23677, ref_len=23160)
Evaluation result for the model: seq-model-myrk.62.0.32-1.37.0.43-1.54.pth
BLEU = 73.09, 87.0/77.0/68.9/61.8 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq-model-myrk.63.0.32-1.37.0.44-1.55.pth
BLEU = 73.14, 87.2/77.2/68.8/61.8 (BP=1.000, ratio=1.023, hyp_len=23703, ref_len=23160)
Evaluation result for the model: seq-model-myrk.64.0.33-1.39.0.46-1.58.pth
BLEU = 72.74, 87.0/76.9/68.4/61.2 (BP=1.000, ratio=1.025, hyp_len=23747, ref_len=23160)
Evaluation result for the model: seq-model-myrk.65.0.35-1.42.0.49-1.63.pth
BLEU = 72.44, 87.2/76.7/68.0/60.6 (BP=1.000, ratio=1.011, hyp_len=23414, ref_len=23160)
Evaluation result for the model: seq-model-myrk.66.0.42-1.52.0.47-1.61.pth
BLEU = 71.44, 86.4/75.8/67.0/59.5 (BP=1.000, ratio=1.020, hyp_len=23623, ref_len=23160)
Evaluation result for the model: seq-model-myrk.67.0.33-1.39.0.41-1.51.pth
BLEU = 73.16, 87.0/77.2/68.9/61.9 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq-model-myrk.68.0.31-1.37.0.41-1.51.pth
BLEU = 74.36, 87.7/78.1/70.2/63.6 (BP=1.000, ratio=1.026, hyp_len=23751, ref_len=23160)
Evaluation result for the model: seq-model-myrk.69.0.30-1.35.0.43-1.53.pth
BLEU = 72.47, 86.4/76.4/68.2/61.2 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq-model-myrk.70.0.30-1.35.0.41-1.51.pth
BLEU = 74.16, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.031, hyp_len=23869, ref_len=23160)
Evaluation result for the model: seq-model-myrk.71.0.29-1.33.0.42-1.52.pth
BLEU = 74.00, 87.5/77.8/69.9/63.0 (BP=1.000, ratio=1.025, hyp_len=23749, ref_len=23160)
Evaluation result for the model: seq-model-myrk.72.0.29-1.34.0.42-1.52.pth
BLEU = 73.62, 87.2/77.5/69.5/62.6 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq-model-myrk.73.0.29-1.34.0.42-1.52.pth
BLEU = 74.66, 87.7/78.3/70.6/64.0 (BP=1.000, ratio=1.029, hyp_len=23827, ref_len=23160)
Evaluation result for the model: seq-model-myrk.74.0.28-1.32.0.41-1.50.pth
BLEU = 73.91, 87.2/77.7/69.8/63.1 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: seq-model-myrk.75.0.27-1.31.0.40-1.49.pth
BLEU = 73.85, 87.1/77.6/69.8/63.0 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq-model-myrk.76.0.29-1.33.0.43-1.53.pth
BLEU = 73.69, 87.1/77.5/69.6/62.8 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: seq-model-myrk.77.0.28-1.32.0.42-1.52.pth
BLEU = 72.32, 86.4/76.4/68.0/61.0 (BP=1.000, ratio=1.040, hyp_len=24083, ref_len=23160)
Evaluation result for the model: seq-model-myrk.78.0.28-1.33.0.44-1.55.pth
BLEU = 72.77, 86.5/76.8/68.6/61.5 (BP=1.000, ratio=1.038, hyp_len=24043, ref_len=23160)
Evaluation result for the model: seq-model-myrk.79.0.27-1.31.0.42-1.52.pth
BLEU = 73.91, 87.2/77.7/69.9/63.1 (BP=1.000, ratio=1.035, hyp_len=23961, ref_len=23160)
Evaluation result for the model: seq-model-myrk.80.0.26-1.30.0.40-1.50.pth
BLEU = 74.47, 87.7/78.3/70.4/63.7 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-model-myrk.81.0.25-1.28.0.42-1.52.pth
BLEU = 73.37, 86.7/77.2/69.3/62.5 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq-model-myrk.82.0.34-1.41.0.45-1.57.pth
BLEU = 71.06, 86.2/75.5/66.5/58.9 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)
Evaluation result for the model: seq-model-myrk.83.0.29-1.34.0.41-1.51.pth
BLEU = 73.25, 86.6/77.1/69.2/62.3 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq-model-myrk.84.0.25-1.28.0.42-1.52.pth
BLEU = 74.11, 87.5/77.9/70.0/63.3 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: seq-model-myrk.85.0.26-1.29.0.41-1.51.pth
BLEU = 73.38, 87.0/77.2/69.2/62.4 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: seq-model-myrk.86.0.24-1.28.0.42-1.52.pth
BLEU = 73.10, 86.8/77.1/68.9/61.9 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq-model-myrk.87.0.24-1.27.0.40-1.49.pth
BLEU = 74.29, 87.5/78.0/70.2/63.6 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq-model-myrk.88.0.23-1.26.0.42-1.52.pth
BLEU = 74.26, 87.3/78.0/70.2/63.5 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq-model-myrk.89.0.23-1.26.0.42-1.52.pth
BLEU = 74.92, 87.9/78.5/70.9/64.3 (BP=1.000, ratio=1.026, hyp_len=23770, ref_len=23160)
Evaluation result for the model: seq-model-myrk.90.0.23-1.26.0.41-1.51.pth
BLEU = 74.06, 87.3/77.8/69.9/63.3 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: seq-model-myrk.91.0.24-1.27.0.42-1.53.pth
BLEU = 73.59, 87.0/77.4/69.5/62.7 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: seq-model-myrk.92.0.26-1.29.0.42-1.52.pth
BLEU = 73.80, 87.7/77.7/69.5/62.6 (BP=1.000, ratio=1.022, hyp_len=23671, ref_len=23160)
Evaluation result for the model: seq-model-myrk.93.0.23-1.26.0.43-1.53.pth
BLEU = 72.46, 86.2/76.4/68.2/61.4 (BP=1.000, ratio=1.038, hyp_len=24041, ref_len=23160)
Evaluation result for the model: seq-model-myrk.94.0.24-1.27.0.43-1.54.pth
BLEU = 72.34, 86.4/76.4/68.1/60.9 (BP=1.000, ratio=1.039, hyp_len=24059, ref_len=23160)
Evaluation result for the model: seq-model-myrk.95.0.23-1.26.0.41-1.50.pth
BLEU = 74.02, 87.3/77.7/69.9/63.3 (BP=1.000, ratio=1.034, hyp_len=23946, ref_len=23160)
Evaluation result for the model: seq-model-myrk.96.0.23-1.25.0.42-1.52.pth
BLEU = 74.92, 87.8/78.5/70.9/64.5 (BP=1.000, ratio=1.028, hyp_len=23813, ref_len=23160)
Evaluation result for the model: seq-model-myrk.97.0.22-1.24.0.41-1.51.pth
BLEU = 74.17, 87.3/77.9/70.1/63.5 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: seq-model-myrk.98.0.25-1.29.0.46-1.58.pth
BLEU = 69.99, 84.9/74.5/65.6/57.8 (BP=1.000, ratio=1.038, hyp_len=24037, ref_len=23160)
Evaluation result for the model: seq-model-myrk.99.0.26-1.30.0.44-1.55.pth
BLEU = 72.90, 86.6/76.8/68.7/61.8 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
/home/ye/exp/simple-nmt

real	32m38.427s
user	31m50.859s
sys	1m54.285s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-rk, 100 epoch training မှာ Best model က 96 epoch ဖြစ်ပြီးတော့ Best Score က 74.92   

## Seq2Seq Baseline (rk-my)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 100 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.pth | tee ./model/seq2seq/baseline/rkmy-100epoch/rkmy-seq2seq-baseline-train.log;
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
    'model_fn': './model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.pth',
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
  (emb_src): Embedding(1693, 128)
  (emb_dec): Embedding(1587, 128)
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
    (output): Linear(in_features=128, out_features=1587, bias=True)
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
Epoch 1 - |param|=6.52e+02 |g_param|=2.19e+05 loss=4.3197e+00 ppl=75.17                                                 
Validation - loss=3.6617e+00 ppl=38.93 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.52e+02 |g_param|=1.86e+05 loss=4.0504e+00 ppl=57.42                                                 
Validation - loss=3.4650e+00 ppl=31.98 best_loss=3.6617e+00 best_ppl=38.93                                              
Epoch 3 - |param|=6.52e+02 |g_param|=1.83e+05 loss=3.9344e+00 ppl=51.13                                                 
Validation - loss=3.3596e+00 ppl=28.78 best_loss=3.4650e+00 best_ppl=31.98                                              
Epoch 4 - |param|=6.53e+02 |g_param|=1.85e+05 loss=3.8580e+00 ppl=47.37                                                 
Validation - loss=3.2741e+00 ppl=26.42 best_loss=3.3596e+00 best_ppl=28.78                                              
Epoch 5 - |param|=6.53e+02 |g_param|=1.79e+05 loss=3.7200e+00 ppl=41.27                                                 
Validation - loss=3.1426e+00 ppl=23.16 best_loss=3.2741e+00 best_ppl=26.42                                              
Epoch 6 - |param|=6.54e+02 |g_param|=1.75e+05 loss=3.5327e+00 ppl=34.22                                                 
Validation - loss=2.9748e+00 ppl=19.59 best_loss=3.1426e+00 best_ppl=23.16                                              
Epoch 7 - |param|=6.55e+02 |g_param|=1.61e+05 loss=3.3303e+00 ppl=27.95                                                 
Validation - loss=2.8102e+00 ppl=16.61 best_loss=2.9748e+00 best_ppl=19.59                                              
Epoch 8 - |param|=6.55e+02 |g_param|=1.57e+05 loss=3.1832e+00 ppl=24.12                                                 
Validation - loss=2.6956e+00 ppl=14.81 best_loss=2.8102e+00 best_ppl=16.61                                              
Epoch 9 - |param|=6.56e+02 |g_param|=1.72e+05 loss=3.0627e+00 ppl=21.39                                                 
Validation - loss=2.5191e+00 ppl=12.42 best_loss=2.6956e+00 best_ppl=14.81                                              
Epoch 10 - |param|=6.57e+02 |g_param|=1.83e+05 loss=2.8894e+00 ppl=17.98                                                
Validation - loss=2.4184e+00 ppl=11.23 best_loss=2.5191e+00 best_ppl=12.42                                              
Epoch 11 - |param|=6.57e+02 |g_param|=1.94e+05 loss=2.7297e+00 ppl=15.33                                                
Validation - loss=2.2345e+00 ppl=9.34 best_loss=2.4184e+00 best_ppl=11.23                                               
Epoch 12 - |param|=6.58e+02 |g_param|=1.69e+05 loss=2.5310e+00 ppl=12.57                                                
Validation - loss=2.0188e+00 ppl=7.53 best_loss=2.2345e+00 best_ppl=9.34                                                
Epoch 13 - |param|=6.59e+02 |g_param|=1.10e+05 loss=2.3189e+00 ppl=10.16                                                
Validation - loss=1.8145e+00 ppl=6.14 best_loss=2.0188e+00 best_ppl=7.53                                                
Epoch 14 - |param|=6.59e+02 |g_param|=8.19e+04 loss=2.0722e+00 ppl=7.94                                                 
Validation - loss=1.6415e+00 ppl=5.16 best_loss=1.8145e+00 best_ppl=6.14                                                
Epoch 15 - |param|=6.60e+02 |g_param|=1.19e+05 loss=1.9128e+00 ppl=6.77                                                 
Validation - loss=1.4748e+00 ppl=4.37 best_loss=1.6415e+00 best_ppl=5.16                                                
Epoch 16 - |param|=6.61e+02 |g_param|=8.81e+04 loss=1.6503e+00 ppl=5.21                                                 
Validation - loss=1.2662e+00 ppl=3.55 best_loss=1.4748e+00 best_ppl=4.37                                                
Epoch 17 - |param|=6.61e+02 |g_param|=7.64e+04 loss=1.4526e+00 ppl=4.27                                                 
Validation - loss=1.1612e+00 ppl=3.19 best_loss=1.2662e+00 best_ppl=3.55                                                
Epoch 18 - |param|=6.62e+02 |g_param|=8.58e+04 loss=1.3779e+00 ppl=3.97                                                 
Validation - loss=1.0843e+00 ppl=2.96 best_loss=1.1612e+00 best_ppl=3.19                                                
Epoch 19 - |param|=6.63e+02 |g_param|=7.30e+04 loss=1.2490e+00 ppl=3.49                                                 
Validation - loss=1.0188e+00 ppl=2.77 best_loss=1.0843e+00 best_ppl=2.96                                                
Epoch 20 - |param|=6.63e+02 |g_param|=9.35e+04 loss=1.1503e+00 ppl=3.16                                                 
Validation - loss=9.2572e-01 ppl=2.52 best_loss=1.0188e+00 best_ppl=2.77                                                
Epoch 21 - |param|=6.64e+02 |g_param|=9.71e+04 loss=1.0694e+00 ppl=2.91                                                 
Validation - loss=9.5470e-01 ppl=2.60 best_loss=9.2572e-01 best_ppl=2.52                                                
Epoch 22 - |param|=6.64e+02 |g_param|=8.83e+04 loss=1.0001e+00 ppl=2.72                                                 
Validation - loss=8.2798e-01 ppl=2.29 best_loss=9.2572e-01 best_ppl=2.52                                                
Epoch 23 - |param|=6.65e+02 |g_param|=4.61e+04 loss=9.2819e-01 ppl=2.53                                                 
Validation - loss=9.0303e-01 ppl=2.47 best_loss=8.2798e-01 best_ppl=2.29                                                
Epoch 24 - |param|=6.65e+02 |g_param|=3.80e+04 loss=8.3441e-01 ppl=2.30                                                 
Validation - loss=7.4650e-01 ppl=2.11 best_loss=8.2798e-01 best_ppl=2.29                                                
Epoch 25 - |param|=6.66e+02 |g_param|=3.82e+04 loss=8.0018e-01 ppl=2.23                                                 
Validation - loss=7.2128e-01 ppl=2.06 best_loss=7.4650e-01 best_ppl=2.11                                                
Epoch 26 - |param|=6.66e+02 |g_param|=3.64e+04 loss=7.2934e-01 ppl=2.07                                                 
Validation - loss=6.8753e-01 ppl=1.99 best_loss=7.2128e-01 best_ppl=2.06                                                
Epoch 27 - |param|=6.67e+02 |g_param|=5.15e+04 loss=7.5486e-01 ppl=2.13                                                 
Validation - loss=6.6105e-01 ppl=1.94 best_loss=6.8753e-01 best_ppl=1.99                                                
Epoch 28 - |param|=6.67e+02 |g_param|=4.12e+04 loss=7.0867e-01 ppl=2.03                                                 
Validation - loss=6.6776e-01 ppl=1.95 best_loss=6.6105e-01 best_ppl=1.94                                                
Epoch 29 - |param|=6.68e+02 |g_param|=3.19e+04 loss=6.2888e-01 ppl=1.88                                                 
Validation - loss=6.5740e-01 ppl=1.93 best_loss=6.6105e-01 best_ppl=1.94                                                
Epoch 30 - |param|=6.68e+02 |g_param|=3.08e+04 loss=6.1779e-01 ppl=1.85                                                 
Validation - loss=6.2558e-01 ppl=1.87 best_loss=6.5740e-01 best_ppl=1.93                                                
Epoch 31 - |param|=6.69e+02 |g_param|=3.23e+04 loss=6.0380e-01 ppl=1.83                                                 
Validation - loss=5.8325e-01 ppl=1.79 best_loss=6.2558e-01 best_ppl=1.87                                                
Epoch 32 - |param|=6.69e+02 |g_param|=2.75e+04 loss=5.8019e-01 ppl=1.79                                                 
Validation - loss=5.6696e-01 ppl=1.76 best_loss=5.8325e-01 best_ppl=1.79                                                
Epoch 33 - |param|=6.70e+02 |g_param|=2.87e+04 loss=5.5527e-01 ppl=1.74                                                 
Validation - loss=5.9470e-01 ppl=1.81 best_loss=5.6696e-01 best_ppl=1.76                                                
Epoch 34 - |param|=6.70e+02 |g_param|=3.04e+04 loss=5.3343e-01 ppl=1.70                                                 
Validation - loss=5.8101e-01 ppl=1.79 best_loss=5.6696e-01 best_ppl=1.76                                                
Epoch 35 - |param|=6.70e+02 |g_param|=3.24e+04 loss=5.1917e-01 ppl=1.68                                                 
Validation - loss=5.8710e-01 ppl=1.80 best_loss=5.6696e-01 best_ppl=1.76                                                
Epoch 36 - |param|=6.71e+02 |g_param|=3.94e+04 loss=5.3315e-01 ppl=1.70                                                 
Validation - loss=5.4104e-01 ppl=1.72 best_loss=5.6696e-01 best_ppl=1.76                                                
Epoch 37 - |param|=6.71e+02 |g_param|=3.62e+04 loss=5.1819e-01 ppl=1.68                                                 
Validation - loss=5.7525e-01 ppl=1.78 best_loss=5.4104e-01 best_ppl=1.72                                                
Epoch 38 - |param|=6.72e+02 |g_param|=3.05e+04 loss=4.9765e-01 ppl=1.64                                                 
Validation - loss=5.4198e-01 ppl=1.72 best_loss=5.4104e-01 best_ppl=1.72                                                
Epoch 39 - |param|=6.72e+02 |g_param|=3.71e+04 loss=4.7950e-01 ppl=1.62                                                 
Validation - loss=5.3302e-01 ppl=1.70 best_loss=5.4104e-01 best_ppl=1.72                                                
Epoch 40 - |param|=6.72e+02 |g_param|=2.72e+04 loss=4.4688e-01 ppl=1.56                                                 
Validation - loss=5.5314e-01 ppl=1.74 best_loss=5.3302e-01 best_ppl=1.70                                                
Epoch 41 - |param|=6.73e+02 |g_param|=2.63e+04 loss=4.2635e-01 ppl=1.53                                                 
Validation - loss=5.6450e-01 ppl=1.76 best_loss=5.3302e-01 best_ppl=1.70                                                
Epoch 42 - |param|=6.73e+02 |g_param|=2.36e+04 loss=4.2151e-01 ppl=1.52                                                 
Validation - loss=5.4534e-01 ppl=1.73 best_loss=5.3302e-01 best_ppl=1.70                                                
Epoch 43 - |param|=6.74e+02 |g_param|=2.30e+04 loss=4.1518e-01 ppl=1.51                                                 
Validation - loss=5.3978e-01 ppl=1.72 best_loss=5.3302e-01 best_ppl=1.70                                                
Epoch 44 - |param|=6.74e+02 |g_param|=2.66e+04 loss=4.0287e-01 ppl=1.50                                                 
Validation - loss=5.1838e-01 ppl=1.68 best_loss=5.3302e-01 best_ppl=1.70                                                
Epoch 45 - |param|=6.74e+02 |g_param|=6.01e+04 loss=4.7035e-01 ppl=1.60                                                 
Validation - loss=4.9119e-01 ppl=1.63 best_loss=5.1838e-01 best_ppl=1.68                                                
Epoch 46 - |param|=6.75e+02 |g_param|=2.62e+04 loss=4.0407e-01 ppl=1.50                                                 
Validation - loss=4.9140e-01 ppl=1.63 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 47 - |param|=6.75e+02 |g_param|=2.47e+04 loss=3.9155e-01 ppl=1.48                                                 
Validation - loss=5.3334e-01 ppl=1.70 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 48 - |param|=6.76e+02 |g_param|=2.65e+04 loss=3.9394e-01 ppl=1.48                                                 
Validation - loss=4.9612e-01 ppl=1.64 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 49 - |param|=6.76e+02 |g_param|=2.44e+04 loss=3.5889e-01 ppl=1.43                                                 
Validation - loss=5.0055e-01 ppl=1.65 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 50 - |param|=6.76e+02 |g_param|=3.22e+04 loss=3.9249e-01 ppl=1.48                                                 
Validation - loss=5.0741e-01 ppl=1.66 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 51 - |param|=6.77e+02 |g_param|=4.61e+04 loss=4.1547e-01 ppl=1.52                                                 
Validation - loss=4.9847e-01 ppl=1.65 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 52 - |param|=6.77e+02 |g_param|=2.65e+04 loss=3.6621e-01 ppl=1.44                                                 
Validation - loss=4.8033e-01 ppl=1.62 best_loss=4.9119e-01 best_ppl=1.63                                                
Epoch 53 - |param|=6.78e+02 |g_param|=2.88e+04 loss=3.7748e-01 ppl=1.46                                                 
Validation - loss=4.9455e-01 ppl=1.64 best_loss=4.8033e-01 best_ppl=1.62                                                
Epoch 54 - |param|=6.78e+02 |g_param|=2.26e+04 loss=3.3952e-01 ppl=1.40                                                 
Validation - loss=4.9300e-01 ppl=1.64 best_loss=4.8033e-01 best_ppl=1.62                                                
Epoch 55 - |param|=6.78e+02 |g_param|=2.18e+04 loss=3.2354e-01 ppl=1.38                                                 
Validation - loss=4.8381e-01 ppl=1.62 best_loss=4.8033e-01 best_ppl=1.62                                                
Epoch 56 - |param|=6.79e+02 |g_param|=4.68e+04 loss=3.2607e-01 ppl=1.39                                                 
Validation - loss=4.8509e-01 ppl=1.62 best_loss=4.8033e-01 best_ppl=1.62                                                
Epoch 57 - |param|=6.79e+02 |g_param|=4.15e+04 loss=3.2336e-01 ppl=1.38                                                 
Validation - loss=4.7956e-01 ppl=1.62 best_loss=4.8033e-01 best_ppl=1.62                                                
Epoch 58 - |param|=6.79e+02 |g_param|=4.00e+04 loss=3.1161e-01 ppl=1.37                                                 
Validation - loss=4.8955e-01 ppl=1.63 best_loss=4.7956e-01 best_ppl=1.62                                                
Epoch 59 - |param|=6.80e+02 |g_param|=3.86e+04 loss=3.0226e-01 ppl=1.35                                                 
Validation - loss=5.0542e-01 ppl=1.66 best_loss=4.7956e-01 best_ppl=1.62                                                
Epoch 60 - |param|=6.80e+02 |g_param|=4.34e+04 loss=3.0628e-01 ppl=1.36                                                 
Validation - loss=4.9002e-01 ppl=1.63 best_loss=4.7956e-01 best_ppl=1.62                                                
Epoch 61 - |param|=6.80e+02 |g_param|=3.93e+04 loss=3.0469e-01 ppl=1.36                                                 
Validation - loss=4.7762e-01 ppl=1.61 best_loss=4.7956e-01 best_ppl=1.62                                                
Epoch 62 - |param|=6.81e+02 |g_param|=3.72e+04 loss=2.9902e-01 ppl=1.35                                                 
Validation - loss=5.0581e-01 ppl=1.66 best_loss=4.7762e-01 best_ppl=1.61                                                
Epoch 63 - |param|=6.81e+02 |g_param|=4.35e+04 loss=2.9835e-01 ppl=1.35                                                 
Validation - loss=4.8168e-01 ppl=1.62 best_loss=4.7762e-01 best_ppl=1.61                                                
Epoch 64 - |param|=6.81e+02 |g_param|=4.84e+04 loss=3.1015e-01 ppl=1.36                                                 
Validation - loss=4.9483e-01 ppl=1.64 best_loss=4.7762e-01 best_ppl=1.61                                                
Epoch 65 - |param|=6.82e+02 |g_param|=3.85e+04 loss=2.8259e-01 ppl=1.33                                                 
Validation - loss=4.5573e-01 ppl=1.58 best_loss=4.7762e-01 best_ppl=1.61                                                
Epoch 66 - |param|=6.82e+02 |g_param|=4.52e+04 loss=2.9788e-01 ppl=1.35                                                 
Validation - loss=4.4004e-01 ppl=1.55 best_loss=4.5573e-01 best_ppl=1.58                                                
Epoch 67 - |param|=6.82e+02 |g_param|=3.78e+04 loss=2.6677e-01 ppl=1.31                                                 
Validation - loss=4.6538e-01 ppl=1.59 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 68 - |param|=6.83e+02 |g_param|=5.92e+04 loss=2.8081e-01 ppl=1.32                                                 
Validation - loss=4.7062e-01 ppl=1.60 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 69 - |param|=6.83e+02 |g_param|=4.21e+04 loss=2.6954e-01 ppl=1.31                                                 
Validation - loss=4.7547e-01 ppl=1.61 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 70 - |param|=6.84e+02 |g_param|=3.96e+04 loss=2.7321e-01 ppl=1.31                                                 
Validation - loss=4.8370e-01 ppl=1.62 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 71 - |param|=6.84e+02 |g_param|=4.03e+04 loss=2.5717e-01 ppl=1.29                                                 
Validation - loss=4.6989e-01 ppl=1.60 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 72 - |param|=6.84e+02 |g_param|=4.90e+04 loss=2.6683e-01 ppl=1.31                                                 
Validation - loss=4.6874e-01 ppl=1.60 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 73 - |param|=6.85e+02 |g_param|=4.76e+04 loss=2.6572e-01 ppl=1.30                                                 
Validation - loss=4.4609e-01 ppl=1.56 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 74 - |param|=6.85e+02 |g_param|=5.21e+04 loss=2.6298e-01 ppl=1.30                                                 
Validation - loss=4.4751e-01 ppl=1.56 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 75 - |param|=6.85e+02 |g_param|=5.15e+04 loss=2.7011e-01 ppl=1.31                                                 
Validation - loss=4.7838e-01 ppl=1.61 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 76 - |param|=6.86e+02 |g_param|=3.91e+04 loss=2.8166e-01 ppl=1.33                                                 
Validation - loss=4.7118e-01 ppl=1.60 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 77 - |param|=6.86e+02 |g_param|=3.03e+04 loss=2.7486e-01 ppl=1.32                                                 
Validation - loss=4.6635e-01 ppl=1.59 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 78 - |param|=6.87e+02 |g_param|=2.40e+04 loss=2.5724e-01 ppl=1.29                                                 
Validation - loss=4.6809e-01 ppl=1.60 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 79 - |param|=6.87e+02 |g_param|=3.52e+04 loss=2.9991e-01 ppl=1.35                                                 
Validation - loss=4.7608e-01 ppl=1.61 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 80 - |param|=6.87e+02 |g_param|=2.23e+04 loss=2.5116e-01 ppl=1.29                                                 
Validation - loss=4.6393e-01 ppl=1.59 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 81 - |param|=6.88e+02 |g_param|=1.92e+04 loss=2.4103e-01 ppl=1.27                                                 
Validation - loss=4.4555e-01 ppl=1.56 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 82 - |param|=6.88e+02 |g_param|=1.82e+04 loss=2.2665e-01 ppl=1.25                                                 
Validation - loss=4.5229e-01 ppl=1.57 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 83 - |param|=6.88e+02 |g_param|=1.83e+04 loss=2.3169e-01 ppl=1.26                                                 
Validation - loss=4.5533e-01 ppl=1.58 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 84 - |param|=6.89e+02 |g_param|=1.71e+04 loss=2.1982e-01 ppl=1.25                                                 
Validation - loss=4.4545e-01 ppl=1.56 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 85 - |param|=6.89e+02 |g_param|=1.56e+04 loss=2.2017e-01 ppl=1.25                                                 
Validation - loss=4.3180e-01 ppl=1.54 best_loss=4.4004e-01 best_ppl=1.55                                                
Epoch 86 - |param|=6.89e+02 |g_param|=1.58e+04 loss=2.0891e-01 ppl=1.23                                                 
Validation - loss=4.3509e-01 ppl=1.55 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 87 - |param|=6.90e+02 |g_param|=1.86e+04 loss=2.1654e-01 ppl=1.24                                                 
Validation - loss=4.4656e-01 ppl=1.56 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 88 - |param|=6.90e+02 |g_param|=1.86e+04 loss=2.0954e-01 ppl=1.23                                                 
Validation - loss=4.5524e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 89 - |param|=6.90e+02 |g_param|=1.65e+04 loss=2.1219e-01 ppl=1.24                                                 
Validation - loss=4.6678e-01 ppl=1.59 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 90 - |param|=6.91e+02 |g_param|=1.92e+04 loss=1.9995e-01 ppl=1.22                                                 
Validation - loss=4.5641e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 91 - |param|=6.91e+02 |g_param|=1.83e+04 loss=2.0531e-01 ppl=1.23                                                 
Validation - loss=4.5832e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 92 - |param|=6.91e+02 |g_param|=2.16e+04 loss=2.0340e-01 ppl=1.23                                                 
Validation - loss=4.5896e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 93 - |param|=6.92e+02 |g_param|=3.58e+04 loss=1.9304e-01 ppl=1.21                                                 
Validation - loss=4.4651e-01 ppl=1.56 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 94 - |param|=6.92e+02 |g_param|=4.22e+04 loss=1.9899e-01 ppl=1.22                                                 
Validation - loss=4.6890e-01 ppl=1.60 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 95 - |param|=6.92e+02 |g_param|=3.73e+04 loss=1.9760e-01 ppl=1.22                                                 
Validation - loss=4.6287e-01 ppl=1.59 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 96 - |param|=6.93e+02 |g_param|=4.31e+04 loss=2.0399e-01 ppl=1.23                                                 
Validation - loss=4.5540e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 97 - |param|=6.93e+02 |g_param|=3.77e+04 loss=1.9514e-01 ppl=1.22                                                 
Validation - loss=4.6006e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 98 - |param|=6.93e+02 |g_param|=3.44e+04 loss=1.9974e-01 ppl=1.22                                                 
Validation - loss=4.5946e-01 ppl=1.58 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 99 - |param|=6.94e+02 |g_param|=3.72e+04 loss=1.9470e-01 ppl=1.21                                                 
Validation - loss=4.8413e-01 ppl=1.62 best_loss=4.3180e-01 best_ppl=1.54                                                
Epoch 100 - |param|=6.94e+02 |g_param|=4.01e+04 loss=1.8278e-01 ppl=1.20                                                
Validation - loss=4.6886e-01 ppl=1.60 best_loss=4.3180e-01 best_ppl=1.54                                                

real	21m20.453s
user	21m3.729s
sys	0m17.127s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-baseline-rkmy.sh 
Evaluation result for the model: seq-model-rkmy.01.4.32-75.17.3.66-38.93.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.4/1.9/0.0/0.0 (BP=1.000, ratio=1.052, hyp_len=24740, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.05-57.42.3.46-31.98.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/2.5/0.0/0.0 (BP=0.982, ratio=0.982, hyp_len=23093, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.3.93-51.13.3.36-28.78.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.1/4.4/0.4/0.0 (BP=0.977, ratio=0.977, hyp_len=22980, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.3.86-47.37.3.27-26.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.2/3.0/0.2/0.0 (BP=0.986, ratio=0.986, hyp_len=23177, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.72-41.27.3.14-23.16.pth
BLEU = 0.83, 23.1/4.5/0.4/0.0 (BP=1.000, ratio=1.010, hyp_len=23734, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.53-34.22.2.97-19.59.pth
BLEU = 1.75, 26.9/6.6/1.0/0.1 (BP=0.960, ratio=0.961, hyp_len=22585, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.33-27.95.2.81-16.61.pth
BLEU = 2.79, 30.1/8.4/1.6/0.1 (BP=0.998, ratio=0.998, hyp_len=23470, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.18-24.12.2.70-14.81.pth
BLEU = 4.47, 30.2/10.2/2.4/0.5 (BP=1.000, ratio=1.022, hyp_len=24016, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.06-21.39.2.52-12.42.pth
BLEU = 6.10, 34.4/12.7/3.3/0.9 (BP=1.000, ratio=1.020, hyp_len=23975, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.100.0.18-1.20.0.47-1.60.pth
BLEU = 74.58, 87.5/78.5/70.4/63.9 (BP=1.000, ratio=1.036, hyp_len=24359, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.2.89-17.98.2.42-11.23.pth
BLEU = 6.52, 33.9/13.6/3.8/1.0 (BP=1.000, ratio=1.029, hyp_len=24201, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.2.73-15.33.2.23-9.34.pth
BLEU = 8.87, 38.9/16.4/5.4/1.8 (BP=1.000, ratio=1.025, hyp_len=24092, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.53-12.57.2.02-7.53.pth
BLEU = 12.05, 42.8/19.9/7.9/3.1 (BP=1.000, ratio=1.026, hyp_len=24127, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.32-10.16.1.81-6.14.pth
BLEU = 15.46, 47.2/23.8/10.7/4.8 (BP=1.000, ratio=1.016, hyp_len=23890, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.07-7.94.1.64-5.16.pth
BLEU = 18.35, 49.8/27.0/13.2/6.4 (BP=1.000, ratio=1.050, hyp_len=24677, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.1.91-6.77.1.47-4.37.pth
BLEU = 23.88, 55.2/32.7/18.1/10.0 (BP=1.000, ratio=1.015, hyp_len=23870, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.1.65-5.21.1.27-3.55.pth
BLEU = 33.95, 63.6/42.6/27.5/17.8 (BP=1.000, ratio=1.014, hyp_len=23834, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.1.45-4.27.1.16-3.19.pth
BLEU = 37.83, 66.4/46.1/31.2/21.4 (BP=1.000, ratio=1.017, hyp_len=23910, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.38-3.97.1.08-2.96.pth
BLEU = 41.23, 68.6/49.2/34.6/24.7 (BP=1.000, ratio=1.017, hyp_len=23906, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.25-3.49.1.02-2.77.pth
BLEU = 43.54, 70.1/51.3/36.9/27.1 (BP=1.000, ratio=1.023, hyp_len=24044, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.15-3.16.0.93-2.52.pth
BLEU = 51.19, 75.0/58.3/44.9/35.0 (BP=1.000, ratio=1.022, hyp_len=24016, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.07-2.91.0.95-2.60.pth
BLEU = 50.81, 74.8/58.0/44.4/34.6 (BP=1.000, ratio=1.013, hyp_len=23824, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.00-2.72.0.83-2.29.pth
BLEU = 55.66, 77.9/62.5/49.5/39.8 (BP=1.000, ratio=1.011, hyp_len=23764, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.0.93-2.53.0.90-2.47.pth
BLEU = 53.42, 76.0/60.8/47.4/37.2 (BP=1.000, ratio=1.048, hyp_len=24646, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.0.83-2.30.0.75-2.11.pth
BLEU = 60.02, 80.1/66.2/54.3/45.1 (BP=1.000, ratio=1.022, hyp_len=24026, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.0.80-2.23.0.72-2.06.pth
BLEU = 63.01, 81.8/68.8/57.5/48.7 (BP=1.000, ratio=1.022, hyp_len=24033, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.0.73-2.07.0.69-1.99.pth
BLEU = 64.09, 82.5/69.7/58.6/50.0 (BP=1.000, ratio=1.023, hyp_len=24059, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.0.75-2.13.0.66-1.94.pth
BLEU = 64.99, 82.9/70.5/59.6/51.2 (BP=1.000, ratio=1.022, hyp_len=24031, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.0.71-2.03.0.67-1.95.pth
BLEU = 64.94, 82.6/70.4/59.7/51.3 (BP=1.000, ratio=1.029, hyp_len=24198, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.63-1.88.0.66-1.93.pth
BLEU = 66.74, 83.5/72.1/61.6/53.5 (BP=1.000, ratio=1.041, hyp_len=24464, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.62-1.85.0.63-1.87.pth
BLEU = 66.81, 83.8/72.1/61.7/53.5 (BP=1.000, ratio=1.024, hyp_len=24067, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.31.0.60-1.83.0.58-1.79.pth
BLEU = 69.97, 85.7/74.8/65.1/57.4 (BP=1.000, ratio=1.018, hyp_len=23922, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.32.0.58-1.79.0.57-1.76.pth
BLEU = 69.52, 85.1/74.3/64.7/57.2 (BP=1.000, ratio=1.023, hyp_len=24056, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.33.0.56-1.74.0.59-1.81.pth
BLEU = 70.56, 85.7/75.3/65.9/58.3 (BP=1.000, ratio=1.029, hyp_len=24189, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.34.0.53-1.70.0.58-1.79.pth
BLEU = 71.10, 86.0/75.7/66.4/59.2 (BP=1.000, ratio=1.025, hyp_len=24089, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.35.0.52-1.68.0.59-1.80.pth
BLEU = 69.49, 85.1/74.3/64.7/57.0 (BP=1.000, ratio=1.036, hyp_len=24358, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.36.0.53-1.70.0.54-1.72.pth
BLEU = 70.93, 85.8/75.6/66.3/58.9 (BP=1.000, ratio=1.032, hyp_len=24261, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.37.0.52-1.68.0.58-1.78.pth
BLEU = 71.26, 86.1/75.8/66.5/59.4 (BP=1.000, ratio=1.027, hyp_len=24147, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.38.0.50-1.64.0.54-1.72.pth
BLEU = 71.88, 86.2/76.3/67.3/60.3 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.39.0.48-1.62.0.53-1.70.pth
BLEU = 71.30, 85.9/75.8/66.7/59.5 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.40.0.45-1.56.0.55-1.74.pth
BLEU = 71.22, 86.0/75.8/66.6/59.3 (BP=1.000, ratio=1.037, hyp_len=24373, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.41.0.43-1.53.0.56-1.76.pth
BLEU = 71.03, 85.9/75.6/66.4/59.1 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.42.0.42-1.52.0.55-1.73.pth
BLEU = 72.60, 86.5/76.8/68.2/61.2 (BP=1.000, ratio=1.033, hyp_len=24274, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.43.0.42-1.51.0.54-1.72.pth
BLEU = 72.45, 86.5/76.8/67.9/61.0 (BP=1.000, ratio=1.038, hyp_len=24405, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.44.0.40-1.50.0.52-1.68.pth
BLEU = 73.03, 87.0/77.3/68.6/61.7 (BP=1.000, ratio=1.029, hyp_len=24201, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.45.0.47-1.60.0.49-1.63.pth
BLEU = 71.71, 86.3/76.3/67.1/59.9 (BP=1.000, ratio=1.036, hyp_len=24365, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.46.0.40-1.50.0.49-1.63.pth
BLEU = 73.65, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.030, hyp_len=24214, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.47.0.39-1.48.0.53-1.70.pth
BLEU = 71.64, 85.9/76.0/67.1/60.1 (BP=1.000, ratio=1.045, hyp_len=24574, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.48.0.39-1.48.0.50-1.64.pth
BLEU = 73.89, 87.3/78.0/69.6/62.9 (BP=1.000, ratio=1.032, hyp_len=24260, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.49.0.36-1.43.0.50-1.65.pth
BLEU = 73.63, 87.2/77.8/69.3/62.5 (BP=1.000, ratio=1.031, hyp_len=24249, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.50.0.39-1.48.0.51-1.66.pth
BLEU = 69.33, 83.5/73.8/64.9/57.8 (BP=1.000, ratio=1.073, hyp_len=25223, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.51.0.42-1.52.0.50-1.65.pth
BLEU = 72.65, 86.7/77.0/68.3/61.1 (BP=1.000, ratio=1.022, hyp_len=24027, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.52.0.37-1.44.0.48-1.62.pth
BLEU = 72.74, 86.6/77.0/68.2/61.6 (BP=1.000, ratio=1.043, hyp_len=24511, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.53.0.38-1.46.0.49-1.64.pth
BLEU = 73.99, 87.2/78.1/69.7/63.1 (BP=1.000, ratio=1.031, hyp_len=24243, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.54.0.34-1.40.0.49-1.64.pth
BLEU = 71.94, 86.1/76.3/67.5/60.4 (BP=1.000, ratio=1.046, hyp_len=24581, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.55.0.32-1.38.0.48-1.62.pth
BLEU = 73.62, 87.0/77.8/69.3/62.6 (BP=1.000, ratio=1.041, hyp_len=24466, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.56.0.33-1.39.0.49-1.62.pth
BLEU = 74.80, 87.8/78.8/70.6/64.1 (BP=1.000, ratio=1.031, hyp_len=24233, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.57.0.32-1.38.0.48-1.62.pth
BLEU = 74.34, 87.6/78.4/70.1/63.5 (BP=1.000, ratio=1.034, hyp_len=24304, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.58.0.31-1.37.0.49-1.63.pth
BLEU = 74.94, 87.7/79.0/70.8/64.3 (BP=1.000, ratio=1.032, hyp_len=24272, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.59.0.30-1.35.0.51-1.66.pth
BLEU = 72.45, 86.3/76.7/68.0/61.2 (BP=1.000, ratio=1.045, hyp_len=24563, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.60.0.31-1.36.0.49-1.63.pth
BLEU = 73.59, 87.1/77.8/69.3/62.5 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.61.0.30-1.36.0.48-1.61.pth
BLEU = 73.67, 87.1/77.8/69.3/62.7 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.62.0.30-1.35.0.51-1.66.pth
BLEU = 73.20, 86.7/77.4/68.8/62.1 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.63.0.30-1.35.0.48-1.62.pth
BLEU = 74.12, 87.3/78.2/69.9/63.2 (BP=1.000, ratio=1.039, hyp_len=24425, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.64.0.31-1.36.0.49-1.64.pth
BLEU = 72.64, 86.5/77.0/68.3/61.2 (BP=1.000, ratio=1.045, hyp_len=24562, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.65.0.28-1.33.0.46-1.58.pth
BLEU = 74.37, 87.4/78.3/70.1/63.7 (BP=1.000, ratio=1.036, hyp_len=24362, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.66.0.30-1.35.0.44-1.55.pth
BLEU = 75.01, 87.8/78.9/70.9/64.5 (BP=1.000, ratio=1.031, hyp_len=24239, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.67.0.27-1.31.0.47-1.59.pth
BLEU = 74.55, 87.6/78.6/70.4/63.7 (BP=1.000, ratio=1.032, hyp_len=24268, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.68.0.28-1.32.0.47-1.60.pth
BLEU = 71.22, 85.7/75.8/66.8/59.3 (BP=1.000, ratio=1.049, hyp_len=24659, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.69.0.27-1.31.0.48-1.61.pth
BLEU = 72.84, 86.6/77.1/68.4/61.6 (BP=1.000, ratio=1.046, hyp_len=24598, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.70.0.27-1.31.0.48-1.62.pth
BLEU = 74.46, 87.4/78.5/70.3/63.8 (BP=1.000, ratio=1.034, hyp_len=24317, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.71.0.26-1.29.0.47-1.60.pth
BLEU = 73.81, 87.2/77.9/69.5/62.9 (BP=1.000, ratio=1.039, hyp_len=24427, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.72.0.27-1.31.0.47-1.60.pth
BLEU = 74.14, 87.3/78.2/69.9/63.3 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.73.0.27-1.30.0.45-1.56.pth
BLEU = 73.48, 86.9/77.6/69.1/62.5 (BP=1.000, ratio=1.044, hyp_len=24555, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.74.0.26-1.30.0.45-1.56.pth
BLEU = 72.87, 86.6/77.1/68.5/61.6 (BP=1.000, ratio=1.044, hyp_len=24535, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.75.0.27-1.31.0.48-1.61.pth
BLEU = 72.51, 86.4/76.9/68.1/61.1 (BP=1.000, ratio=1.047, hyp_len=24605, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.76.0.28-1.33.0.47-1.60.pth
BLEU = 73.15, 87.0/77.5/68.8/61.8 (BP=1.000, ratio=1.041, hyp_len=24473, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.77.0.27-1.32.0.47-1.59.pth
BLEU = 73.42, 87.2/77.7/69.0/62.2 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.78.0.26-1.29.0.47-1.60.pth
BLEU = 73.37, 86.9/77.6/69.1/62.1 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.79.0.30-1.35.0.48-1.61.pth
BLEU = 70.87, 85.3/75.3/66.4/59.1 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.80.0.25-1.29.0.46-1.59.pth
BLEU = 73.85, 87.0/77.9/69.6/63.1 (BP=1.000, ratio=1.042, hyp_len=24487, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.81.0.24-1.27.0.45-1.56.pth
BLEU = 74.04, 87.2/78.1/69.8/63.2 (BP=1.000, ratio=1.039, hyp_len=24432, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.82.0.23-1.25.0.45-1.57.pth
BLEU = 73.67, 87.1/77.9/69.4/62.6 (BP=1.000, ratio=1.044, hyp_len=24537, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.83.0.23-1.26.0.46-1.58.pth
BLEU = 73.19, 86.7/77.4/68.8/62.1 (BP=1.000, ratio=1.049, hyp_len=24661, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.84.0.22-1.25.0.45-1.56.pth
BLEU = 73.70, 87.1/77.8/69.4/62.8 (BP=1.000, ratio=1.044, hyp_len=24539, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.85.0.22-1.25.0.43-1.54.pth
BLEU = 73.83, 87.1/78.0/69.6/62.9 (BP=1.000, ratio=1.043, hyp_len=24526, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.86.0.21-1.23.0.44-1.55.pth
BLEU = 74.21, 87.5/78.3/69.9/63.3 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.87.0.22-1.24.0.45-1.56.pth
BLEU = 74.29, 87.5/78.3/70.1/63.4 (BP=1.000, ratio=1.038, hyp_len=24414, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.88.0.21-1.23.0.46-1.58.pth
BLEU = 74.35, 87.6/78.4/70.1/63.5 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.89.0.21-1.24.0.47-1.59.pth
BLEU = 74.14, 87.3/78.2/69.9/63.3 (BP=1.000, ratio=1.042, hyp_len=24498, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.90.0.20-1.22.0.46-1.58.pth
BLEU = 73.97, 87.3/78.1/69.7/63.0 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.91.0.21-1.23.0.46-1.58.pth
BLEU = 73.94, 87.3/78.0/69.6/63.1 (BP=1.000, ratio=1.043, hyp_len=24520, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.92.0.20-1.23.0.46-1.58.pth
BLEU = 74.64, 87.7/78.7/70.4/63.9 (BP=1.000, ratio=1.036, hyp_len=24349, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.93.0.19-1.21.0.45-1.56.pth
BLEU = 73.72, 87.2/77.9/69.4/62.6 (BP=1.000, ratio=1.039, hyp_len=24421, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.94.0.20-1.22.0.47-1.60.pth
BLEU = 73.53, 87.0/77.7/69.2/62.4 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.95.0.20-1.22.0.46-1.59.pth
BLEU = 73.87, 87.2/78.0/69.6/62.8 (BP=1.000, ratio=1.042, hyp_len=24496, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.96.0.20-1.23.0.46-1.58.pth
BLEU = 74.56, 87.5/78.5/70.4/63.9 (BP=1.000, ratio=1.036, hyp_len=24362, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.97.0.20-1.22.0.46-1.58.pth
BLEU = 73.39, 86.8/77.6/69.1/62.3 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.98.0.20-1.22.0.46-1.58.pth
BLEU = 74.56, 87.5/78.6/70.4/63.9 (BP=1.000, ratio=1.038, hyp_len=24395, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.99.0.19-1.21.0.48-1.62.pth
BLEU = 74.43, 87.4/78.4/70.2/63.8 (BP=1.000, ratio=1.037, hyp_len=24382, ref_len=23509)
/home/ye/exp/simple-nmt

real	34m23.840s
user	33m40.211s
sys	1m54.405s
(simple-nmt) ye@:~/exp/simple-nmt$
```

rk-my, 100 epoch training မှာ Best model က 66 epoch model ဖြစ်ပြီးတော့ Best score က 75.01   


## Transformer Baseline (my-rk)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.pth
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
    'model_fn': './model/transformer/baseline/myrk-100epoch/myrk-transformer-model.pth',
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.59e+05 loss=5.8161e+00 ppl=335.66                                                
Validation - loss=5.8523e+00 ppl=348.02 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.37e+05 loss=5.0398e+00 ppl=154.44                                                
Validation - loss=5.0518e+00 ppl=156.31 best_loss=5.8523e+00 best_ppl=348.02                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.38e+05 loss=4.5175e+00 ppl=91.61                                                 
Validation - loss=4.5995e+00 ppl=99.43 best_loss=5.0518e+00 best_ppl=156.31                                             
Epoch 4 - |param|=3.24e+02 |g_param|=1.85e+05 loss=4.2012e+00 ppl=66.76                                                 
Validation - loss=4.3084e+00 ppl=74.32 best_loss=4.5995e+00 best_ppl=99.43                                              
Epoch 5 - |param|=3.24e+02 |g_param|=1.68e+05 loss=3.9832e+00 ppl=53.69                                                 
Validation - loss=4.0866e+00 ppl=59.54 best_loss=4.3084e+00 best_ppl=74.32                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.71e+05 loss=3.7342e+00 ppl=41.86                                                 
Validation - loss=3.8842e+00 ppl=48.63 best_loss=4.0866e+00 best_ppl=59.54                                              
Epoch 7 - |param|=3.24e+02 |g_param|=2.18e+05 loss=3.6190e+00 ppl=37.30                                                 
Validation - loss=3.7290e+00 ppl=41.64 best_loss=3.8842e+00 best_ppl=48.63                                              
Epoch 8 - |param|=3.24e+02 |g_param|=1.44e+05 loss=3.4594e+00 ppl=31.80                                                 
Validation - loss=3.5774e+00 ppl=35.78 best_loss=3.7290e+00 best_ppl=41.64                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.95e+05 loss=3.3204e+00 ppl=27.67                                                 
Validation - loss=3.4382e+00 ppl=31.13 best_loss=3.5774e+00 best_ppl=35.78                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.74e+05 loss=3.1556e+00 ppl=23.47                                                
Validation - loss=3.3183e+00 ppl=27.61 best_loss=3.4382e+00 best_ppl=31.13                                              
Epoch 11 - |param|=3.24e+02 |g_param|=1.99e+05 loss=3.1534e+00 ppl=23.42                                                
Validation - loss=3.2046e+00 ppl=24.65 best_loss=3.3183e+00 best_ppl=27.61                                              
Epoch 12 - |param|=3.24e+02 |g_param|=2.44e+05 loss=3.0590e+00 ppl=21.31                                                
Validation - loss=3.1120e+00 ppl=22.47 best_loss=3.2046e+00 best_ppl=24.65                                              
Epoch 13 - |param|=3.25e+02 |g_param|=2.34e+05 loss=2.9457e+00 ppl=19.02                                                
Validation - loss=3.0091e+00 ppl=20.27 best_loss=3.1120e+00 best_ppl=22.47                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.57e+05 loss=2.8864e+00 ppl=17.93                                                
Validation - loss=2.9291e+00 ppl=18.71 best_loss=3.0091e+00 best_ppl=20.27                                              
Epoch 15 - |param|=3.25e+02 |g_param|=2.65e+05 loss=2.7800e+00 ppl=16.12                                                
Validation - loss=2.8329e+00 ppl=16.99 best_loss=2.9291e+00 best_ppl=18.71                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.70e+05 loss=2.7531e+00 ppl=15.69                                                
Validation - loss=2.7678e+00 ppl=15.92 best_loss=2.8329e+00 best_ppl=16.99                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.58e+05 loss=2.6467e+00 ppl=14.11                                                
Validation - loss=2.6962e+00 ppl=14.82 best_loss=2.7678e+00 best_ppl=15.92                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.98e+05 loss=2.6598e+00 ppl=14.29                                                
Validation - loss=2.6244e+00 ppl=13.80 best_loss=2.6962e+00 best_ppl=14.82                                              
Epoch 19 - |param|=3.25e+02 |g_param|=3.05e+05 loss=2.5181e+00 ppl=12.40                                                
Validation - loss=2.5601e+00 ppl=12.94 best_loss=2.6244e+00 best_ppl=13.80                                              
Epoch 20 - |param|=3.25e+02 |g_param|=2.51e+05 loss=2.5340e+00 ppl=12.60                                                
Validation - loss=2.5061e+00 ppl=12.26 best_loss=2.5601e+00 best_ppl=12.94                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.19e+05 loss=2.4687e+00 ppl=11.81                                                
Validation - loss=2.4518e+00 ppl=11.61 best_loss=2.5061e+00 best_ppl=12.26                                              
Epoch 22 - |param|=3.25e+02 |g_param|=2.24e+05 loss=2.4046e+00 ppl=11.07                                                
Validation - loss=2.3908e+00 ppl=10.92 best_loss=2.4518e+00 best_ppl=11.61                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.83e+05 loss=2.3901e+00 ppl=10.91                                                
Validation - loss=2.3358e+00 ppl=10.34 best_loss=2.3908e+00 best_ppl=10.92                                              
Epoch 24 - |param|=3.25e+02 |g_param|=3.34e+05 loss=2.3502e+00 ppl=10.49                                                
Validation - loss=2.2810e+00 ppl=9.79 best_loss=2.3358e+00 best_ppl=10.34                                               
Epoch 25 - |param|=3.25e+02 |g_param|=2.75e+05 loss=2.2331e+00 ppl=9.33                                                 
Validation - loss=2.2361e+00 ppl=9.36 best_loss=2.2810e+00 best_ppl=9.79                                                
Epoch 26 - |param|=3.25e+02 |g_param|=5.51e+05 loss=2.2425e+00 ppl=9.42                                                 
Validation - loss=2.2308e+00 ppl=9.31 best_loss=2.2361e+00 best_ppl=9.36                                                
Epoch 27 - |param|=3.25e+02 |g_param|=3.39e+05 loss=2.2013e+00 ppl=9.04                                                 
Validation - loss=2.1410e+00 ppl=8.51 best_loss=2.2308e+00 best_ppl=9.31                                                
Epoch 28 - |param|=3.25e+02 |g_param|=4.18e+05 loss=2.1986e+00 ppl=9.01                                                 
Validation - loss=2.1120e+00 ppl=8.27 best_loss=2.1410e+00 best_ppl=8.51                                                
Epoch 29 - |param|=3.25e+02 |g_param|=3.89e+05 loss=2.1622e+00 ppl=8.69                                                 
Validation - loss=2.0575e+00 ppl=7.83 best_loss=2.1120e+00 best_ppl=8.27                                                
Epoch 30 - |param|=3.25e+02 |g_param|=3.74e+05 loss=2.1092e+00 ppl=8.24                                                 
Validation - loss=2.0237e+00 ppl=7.57 best_loss=2.0575e+00 best_ppl=7.83                                                
Epoch 31 - |param|=3.25e+02 |g_param|=4.18e+05 loss=2.1000e+00 ppl=8.17                                                 
Validation - loss=1.9734e+00 ppl=7.20 best_loss=2.0237e+00 best_ppl=7.57                                                
Epoch 32 - |param|=3.25e+02 |g_param|=5.68e+05 loss=2.0321e+00 ppl=7.63                                                 
Validation - loss=1.9313e+00 ppl=6.90 best_loss=1.9734e+00 best_ppl=7.20                                                
Epoch 33 - |param|=3.25e+02 |g_param|=5.81e+05 loss=2.0193e+00 ppl=7.53                                                 
Validation - loss=1.8953e+00 ppl=6.65 best_loss=1.9313e+00 best_ppl=6.90                                                
Epoch 34 - |param|=3.25e+02 |g_param|=4.36e+05 loss=1.8988e+00 ppl=6.68                                                 
Validation - loss=1.8527e+00 ppl=6.38 best_loss=1.8953e+00 best_ppl=6.65                                                
Epoch 35 - |param|=3.25e+02 |g_param|=3.94e+05 loss=1.9562e+00 ppl=7.07                                                 
Validation - loss=1.8271e+00 ppl=6.22 best_loss=1.8527e+00 best_ppl=6.38                                                
Epoch 36 - |param|=3.25e+02 |g_param|=3.82e+05 loss=1.9552e+00 ppl=7.07                                                 
Validation - loss=1.7955e+00 ppl=6.02 best_loss=1.8271e+00 best_ppl=6.22                                                
Epoch 37 - |param|=3.25e+02 |g_param|=6.32e+05 loss=1.8556e+00 ppl=6.40                                                 
Validation - loss=1.7554e+00 ppl=5.79 best_loss=1.7955e+00 best_ppl=6.02                                                
Epoch 38 - |param|=3.25e+02 |g_param|=3.58e+05 loss=1.9063e+00 ppl=6.73                                                 
Validation - loss=1.7289e+00 ppl=5.63 best_loss=1.7554e+00 best_ppl=5.79                                                
Epoch 39 - |param|=3.25e+02 |g_param|=4.96e+05 loss=1.7919e+00 ppl=6.00                                                 
Validation - loss=1.6962e+00 ppl=5.45 best_loss=1.7289e+00 best_ppl=5.63                                                
Epoch 40 - |param|=3.25e+02 |g_param|=4.08e+05 loss=1.8293e+00 ppl=6.23                                                 
Validation - loss=1.6903e+00 ppl=5.42 best_loss=1.6962e+00 best_ppl=5.45                                                
Epoch 41 - |param|=3.25e+02 |g_param|=4.55e+05 loss=1.7270e+00 ppl=5.62                                                 
Validation - loss=1.6318e+00 ppl=5.11 best_loss=1.6903e+00 best_ppl=5.42                                                
Epoch 42 - |param|=3.25e+02 |g_param|=6.79e+05 loss=1.7900e+00 ppl=5.99                                                 
Validation - loss=1.6294e+00 ppl=5.10 best_loss=1.6318e+00 best_ppl=5.11                                                
Epoch 43 - |param|=3.25e+02 |g_param|=5.11e+05 loss=1.7157e+00 ppl=5.56                                                 
Validation - loss=1.6008e+00 ppl=4.96 best_loss=1.6294e+00 best_ppl=5.10                                                
Epoch 44 - |param|=3.25e+02 |g_param|=5.18e+05 loss=1.5915e+00 ppl=4.91                                                 
Validation - loss=1.5535e+00 ppl=4.73 best_loss=1.6008e+00 best_ppl=4.96                                                
Epoch 45 - |param|=3.25e+02 |g_param|=4.15e+05 loss=1.6673e+00 ppl=5.30                                                 
Validation - loss=1.5315e+00 ppl=4.63 best_loss=1.5535e+00 best_ppl=4.73                                                
Epoch 46 - |param|=3.25e+02 |g_param|=5.11e+05 loss=1.6786e+00 ppl=5.36                                                 
Validation - loss=1.5063e+00 ppl=4.51 best_loss=1.5315e+00 best_ppl=4.63                                                
Epoch 47 - |param|=3.25e+02 |g_param|=6.43e+05 loss=1.6508e+00 ppl=5.21                                                 
Validation - loss=1.4839e+00 ppl=4.41 best_loss=1.5063e+00 best_ppl=4.51                                                
Epoch 48 - |param|=3.25e+02 |g_param|=5.59e+05 loss=1.5920e+00 ppl=4.91                                                 
Validation - loss=1.4659e+00 ppl=4.33 best_loss=1.4839e+00 best_ppl=4.41                                                
Epoch 49 - |param|=3.25e+02 |g_param|=5.07e+05 loss=1.5523e+00 ppl=4.72                                                 
Validation - loss=1.4538e+00 ppl=4.28 best_loss=1.4659e+00 best_ppl=4.33                                                
Epoch 50 - |param|=3.25e+02 |g_param|=6.86e+05 loss=1.5727e+00 ppl=4.82                                                 
Validation - loss=1.4322e+00 ppl=4.19 best_loss=1.4538e+00 best_ppl=4.28                                                
Epoch 51 - |param|=3.25e+02 |g_param|=5.25e+05 loss=1.5918e+00 ppl=4.91                                                 
Validation - loss=1.4145e+00 ppl=4.11 best_loss=1.4322e+00 best_ppl=4.19                                                
Epoch 52 - |param|=3.25e+02 |g_param|=6.64e+05 loss=1.5369e+00 ppl=4.65                                                 
Validation - loss=1.3807e+00 ppl=3.98 best_loss=1.4145e+00 best_ppl=4.11                                                
Epoch 53 - |param|=3.25e+02 |g_param|=6.29e+05 loss=1.4797e+00 ppl=4.39                                                 
Validation - loss=1.3732e+00 ppl=3.95 best_loss=1.3807e+00 best_ppl=3.98                                                
Epoch 54 - |param|=3.25e+02 |g_param|=5.96e+05 loss=1.5475e+00 ppl=4.70                                                 
Validation - loss=1.3559e+00 ppl=3.88 best_loss=1.3732e+00 best_ppl=3.95                                                
Epoch 55 - |param|=3.25e+02 |g_param|=7.89e+05 loss=1.5028e+00 ppl=4.49                                                 
Validation - loss=1.3645e+00 ppl=3.91 best_loss=1.3559e+00 best_ppl=3.88                                                
Epoch 56 - |param|=3.25e+02 |g_param|=7.34e+05 loss=1.4254e+00 ppl=4.16                                                 
Validation - loss=1.3380e+00 ppl=3.81 best_loss=1.3559e+00 best_ppl=3.88                                                
Epoch 57 - |param|=3.25e+02 |g_param|=7.19e+05 loss=1.4431e+00 ppl=4.23                                                 
Validation - loss=1.3427e+00 ppl=3.83 best_loss=1.3380e+00 best_ppl=3.81                                                
Epoch 58 - |param|=3.25e+02 |g_param|=7.80e+05 loss=1.4275e+00 ppl=4.17                                                 
Validation - loss=1.2925e+00 ppl=3.64 best_loss=1.3380e+00 best_ppl=3.81                                                
Epoch 59 - |param|=3.25e+02 |g_param|=5.00e+05 loss=1.5003e+00 ppl=4.48                                                 
Validation - loss=1.2786e+00 ppl=3.59 best_loss=1.2925e+00 best_ppl=3.64                                                
Epoch 60 - |param|=3.25e+02 |g_param|=5.67e+05 loss=1.3914e+00 ppl=4.02                                                 
Validation - loss=1.2810e+00 ppl=3.60 best_loss=1.2786e+00 best_ppl=3.59                                                
Epoch 61 - |param|=3.25e+02 |g_param|=5.74e+05 loss=1.4224e+00 ppl=4.15                                                 
Validation - loss=1.2486e+00 ppl=3.49 best_loss=1.2786e+00 best_ppl=3.59                                                
Epoch 62 - |param|=3.25e+02 |g_param|=1.07e+06 loss=1.4208e+00 ppl=4.14                                                 
Validation - loss=1.2958e+00 ppl=3.65 best_loss=1.2486e+00 best_ppl=3.49                                                
Epoch 63 - |param|=3.25e+02 |g_param|=6.14e+05 loss=1.3768e+00 ppl=3.96                                                 
Validation - loss=1.2372e+00 ppl=3.45 best_loss=1.2486e+00 best_ppl=3.49                                                
Epoch 64 - |param|=3.25e+02 |g_param|=3.57e+05 loss=1.3536e+00 ppl=3.87                                                 
Validation - loss=1.2181e+00 ppl=3.38 best_loss=1.2372e+00 best_ppl=3.45                                                
Epoch 65 - |param|=3.25e+02 |g_param|=3.73e+05 loss=1.3559e+00 ppl=3.88                                                 
Validation - loss=1.2067e+00 ppl=3.34 best_loss=1.2181e+00 best_ppl=3.38                                                
Epoch 66 - |param|=3.25e+02 |g_param|=2.77e+05 loss=1.3232e+00 ppl=3.76                                                 
Validation - loss=1.1985e+00 ppl=3.32 best_loss=1.2067e+00 best_ppl=3.34                                                
Epoch 67 - |param|=3.25e+02 |g_param|=5.17e+05 loss=1.3341e+00 ppl=3.80                                                 
Validation - loss=1.2415e+00 ppl=3.46 best_loss=1.1985e+00 best_ppl=3.32                                                
Epoch 68 - |param|=3.25e+02 |g_param|=2.43e+05 loss=1.3069e+00 ppl=3.69                                                 
Validation - loss=1.1763e+00 ppl=3.24 best_loss=1.1985e+00 best_ppl=3.32                                                
Epoch 69 - |param|=3.25e+02 |g_param|=3.55e+05 loss=1.2795e+00 ppl=3.59                                                 
Validation - loss=1.1612e+00 ppl=3.19 best_loss=1.1763e+00 best_ppl=3.24                                                
Epoch 70 - |param|=3.25e+02 |g_param|=3.01e+05 loss=1.3052e+00 ppl=3.69                                                 
Validation - loss=1.1659e+00 ppl=3.21 best_loss=1.1612e+00 best_ppl=3.19                                                
Epoch 71 - |param|=3.25e+02 |g_param|=3.86e+05 loss=1.2540e+00 ppl=3.50                                                 
Validation - loss=1.1735e+00 ppl=3.23 best_loss=1.1612e+00 best_ppl=3.19                                                
Epoch 72 - |param|=3.25e+02 |g_param|=4.36e+05 loss=1.3437e+00 ppl=3.83                                                 
Validation - loss=1.1477e+00 ppl=3.15 best_loss=1.1612e+00 best_ppl=3.19                                                
Epoch 73 - |param|=3.25e+02 |g_param|=2.90e+05 loss=1.2927e+00 ppl=3.64                                                 
Validation - loss=1.1342e+00 ppl=3.11 best_loss=1.1477e+00 best_ppl=3.15                                                
Epoch 74 - |param|=3.25e+02 |g_param|=3.34e+05 loss=1.2578e+00 ppl=3.52                                                 
Validation - loss=1.1536e+00 ppl=3.17 best_loss=1.1342e+00 best_ppl=3.11                                                
Epoch 75 - |param|=3.25e+02 |g_param|=4.10e+05 loss=1.2539e+00 ppl=3.50                                                 
Validation - loss=1.1278e+00 ppl=3.09 best_loss=1.1342e+00 best_ppl=3.11                                                
Epoch 76 - |param|=3.25e+02 |g_param|=3.68e+05 loss=1.1950e+00 ppl=3.30                                                 
Validation - loss=1.1045e+00 ppl=3.02 best_loss=1.1278e+00 best_ppl=3.09                                                
Epoch 77 - |param|=3.25e+02 |g_param|=3.85e+05 loss=1.2359e+00 ppl=3.44                                                 
Validation - loss=1.0967e+00 ppl=2.99 best_loss=1.1045e+00 best_ppl=3.02                                                
Epoch 78 - |param|=3.25e+02 |g_param|=5.61e+05 loss=1.2783e+00 ppl=3.59                                                 
Validation - loss=1.1258e+00 ppl=3.08 best_loss=1.0967e+00 best_ppl=2.99                                                
Epoch 79 - |param|=3.25e+02 |g_param|=3.27e+05 loss=1.2424e+00 ppl=3.46                                                 
Validation - loss=1.0809e+00 ppl=2.95 best_loss=1.0967e+00 best_ppl=2.99                                                
Epoch 80 - |param|=3.25e+02 |g_param|=5.16e+05 loss=1.2225e+00 ppl=3.40                                                 
Validation - loss=1.0822e+00 ppl=2.95 best_loss=1.0809e+00 best_ppl=2.95                                                
Epoch 81 - |param|=3.25e+02 |g_param|=3.59e+05 loss=1.1969e+00 ppl=3.31                                                 
Validation - loss=1.1021e+00 ppl=3.01 best_loss=1.0809e+00 best_ppl=2.95                                                
Epoch 82 - |param|=3.25e+02 |g_param|=5.72e+05 loss=1.2191e+00 ppl=3.38                                                 
Validation - loss=1.0618e+00 ppl=2.89 best_loss=1.0809e+00 best_ppl=2.95                                                
Epoch 83 - |param|=3.25e+02 |g_param|=4.48e+05 loss=1.1349e+00 ppl=3.11                                                 
Validation - loss=1.1121e+00 ppl=3.04 best_loss=1.0618e+00 best_ppl=2.89                                                
Epoch 84 - |param|=3.25e+02 |g_param|=4.31e+05 loss=1.1540e+00 ppl=3.17                                                 
Validation - loss=1.0574e+00 ppl=2.88 best_loss=1.0618e+00 best_ppl=2.89                                                
Epoch 85 - |param|=3.25e+02 |g_param|=3.56e+05 loss=1.1543e+00 ppl=3.17                                                 
Validation - loss=1.0440e+00 ppl=2.84 best_loss=1.0574e+00 best_ppl=2.88                                                
Epoch 86 - |param|=3.25e+02 |g_param|=4.15e+05 loss=1.1612e+00 ppl=3.19                                                 
Validation - loss=1.0465e+00 ppl=2.85 best_loss=1.0440e+00 best_ppl=2.84                                                
Epoch 87 - |param|=3.25e+02 |g_param|=4.46e+05 loss=1.1561e+00 ppl=3.18                                                 
Validation - loss=1.0671e+00 ppl=2.91 best_loss=1.0440e+00 best_ppl=2.84                                                
Epoch 88 - |param|=3.25e+02 |g_param|=5.16e+05 loss=1.1595e+00 ppl=3.19                                                 
Validation - loss=1.0363e+00 ppl=2.82 best_loss=1.0440e+00 best_ppl=2.84                                                
Epoch 89 - |param|=3.25e+02 |g_param|=4.08e+05 loss=1.1004e+00 ppl=3.01                                                 
Validation - loss=1.0260e+00 ppl=2.79 best_loss=1.0363e+00 best_ppl=2.82                                                
Epoch 90 - |param|=3.25e+02 |g_param|=5.16e+05 loss=1.0945e+00 ppl=2.99                                                 
Validation - loss=1.0264e+00 ppl=2.79 best_loss=1.0260e+00 best_ppl=2.79                                                
Epoch 91 - |param|=3.25e+02 |g_param|=3.96e+05 loss=1.0735e+00 ppl=2.93                                                 
Validation - loss=1.0145e+00 ppl=2.76 best_loss=1.0260e+00 best_ppl=2.79                                                
Epoch 92 - |param|=3.25e+02 |g_param|=4.21e+05 loss=1.1339e+00 ppl=3.11                                                 
Validation - loss=1.0038e+00 ppl=2.73 best_loss=1.0145e+00 best_ppl=2.76                                                
Epoch 93 - |param|=3.25e+02 |g_param|=4.30e+05 loss=1.1057e+00 ppl=3.02                                                 
Validation - loss=1.0124e+00 ppl=2.75 best_loss=1.0038e+00 best_ppl=2.73                                                
Epoch 94 - |param|=3.25e+02 |g_param|=4.59e+05 loss=1.0707e+00 ppl=2.92                                                 
Validation - loss=9.9822e-01 ppl=2.71 best_loss=1.0038e+00 best_ppl=2.73                                                
Epoch 95 - |param|=3.26e+02 |g_param|=2.72e+05 loss=1.0272e+00 ppl=2.79                                                 
Validation - loss=1.0038e+00 ppl=2.73 best_loss=9.9822e-01 best_ppl=2.71                                                
Epoch 96 - |param|=3.26e+02 |g_param|=4.65e+05 loss=1.1242e+00 ppl=3.08                                                 
Validation - loss=9.9094e-01 ppl=2.69 best_loss=9.9822e-01 best_ppl=2.71                                                
Epoch 97 - |param|=3.26e+02 |g_param|=5.57e+05 loss=1.1387e+00 ppl=3.12                                                 
Validation - loss=9.9752e-01 ppl=2.71 best_loss=9.9094e-01 best_ppl=2.69                                                
Epoch 98 - |param|=3.26e+02 |g_param|=3.74e+05 loss=1.0639e+00 ppl=2.90                                                 
Validation - loss=9.8740e-01 ppl=2.68 best_loss=9.9094e-01 best_ppl=2.69                                                
Epoch 99 - |param|=3.26e+02 |g_param|=4.62e+05 loss=1.0391e+00 ppl=2.83                                                 
Validation - loss=9.9123e-01 ppl=2.69 best_loss=9.8740e-01 best_ppl=2.68                                                
Epoch 100 - |param|=3.26e+02 |g_param|=5.01e+05 loss=1.0429e+00 ppl=2.84                                                
Validation - loss=9.7015e-01 ppl=2.64 best_loss=9.8740e-01 best_ppl=2.68                                                

real	55m13.726s
user	52m29.214s
sys	0m44.539s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation... 

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-baseline-transformer-myrk.sh 
Evaluation result for the model: myrk-transformer-model.01.5.82-335.66.5.85-348.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 97.1/0.0/0.0/0.0 (BP=0.000, ratio=0.081, hyp_len=1873, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.5.04-154.44.5.05-156.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 78.8/14.1/0.0/0.0 (BP=0.001, ratio=0.122, hyp_len=2827, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.52-91.61.4.60-99.43.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 54.8/18.2/0.3/0.0 (BP=0.057, ratio=0.259, hyp_len=5998, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.20-66.76.4.31-74.32.pth
BLEU = 1.48, 38.1/10.2/1.4/0.1 (BP=0.564, ratio=0.636, hyp_len=14725, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.3.98-53.69.4.09-59.54.pth
BLEU = 2.99, 40.2/11.7/2.2/0.2 (BP=0.757, ratio=0.782, hyp_len=18122, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.73-41.86.3.88-48.63.pth
BLEU = 4.42, 37.5/12.3/2.9/0.4 (BP=0.893, ratio=0.898, hyp_len=20806, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.62-37.30.3.73-41.64.pth
BLEU = 5.26, 31.0/11.3/3.1/0.7 (BP=1.000, ratio=1.164, hyp_len=26964, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.46-31.80.3.58-35.78.pth
BLEU = 5.91, 32.3/12.3/3.6/0.9 (BP=1.000, ratio=1.144, hyp_len=26490, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.32-27.67.3.44-31.13.pth
BLEU = 6.47, 33.5/13.2/4.0/1.0 (BP=1.000, ratio=1.131, hyp_len=26205, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.100.1.04-2.84.0.97-2.64.pth
BLEU = 59.35, 80.6/65.4/53.5/44.0 (BP=1.000, ratio=1.024, hyp_len=23718, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.16-23.47.3.32-27.61.pth
BLEU = 7.19, 35.2/14.1/4.4/1.2 (BP=1.000, ratio=1.128, hyp_len=26114, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.15-23.42.3.20-24.65.pth
BLEU = 8.60, 38.6/16.0/5.5/1.6 (BP=1.000, ratio=1.066, hyp_len=24698, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.06-21.31.3.11-22.47.pth
BLEU = 9.71, 39.9/17.2/6.3/2.1 (BP=1.000, ratio=1.085, hyp_len=25125, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.2.95-19.02.3.01-20.27.pth
BLEU = 11.78, 45.7/20.3/8.0/2.8 (BP=0.980, ratio=0.981, hyp_len=22709, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.89-17.93.2.93-18.71.pth
BLEU = 11.42, 41.7/18.7/7.6/2.9 (BP=1.000, ratio=1.117, hyp_len=25878, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.78-16.12.2.83-16.99.pth
BLEU = 13.43, 45.1/21.0/9.2/3.7 (BP=1.000, ratio=1.067, hyp_len=24713, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.75-15.69.2.77-15.92.pth
BLEU = 14.67, 46.2/22.2/10.1/4.5 (BP=1.000, ratio=1.076, hyp_len=24930, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.65-14.11.2.70-14.82.pth
BLEU = 16.59, 50.2/24.9/11.6/5.2 (BP=1.000, ratio=1.013, hyp_len=23453, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.66-14.29.2.62-13.80.pth
BLEU = 16.86, 48.9/24.9/12.0/5.5 (BP=1.000, ratio=1.066, hyp_len=24680, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.52-12.40.2.56-12.94.pth
BLEU = 17.55, 49.6/25.7/12.6/5.9 (BP=1.000, ratio=1.066, hyp_len=24691, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.53-12.60.2.51-12.26.pth
BLEU = 20.10, 54.5/28.9/14.9/7.3 (BP=0.986, ratio=0.986, hyp_len=22847, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.47-11.81.2.45-11.61.pth
BLEU = 19.31, 51.4/27.3/14.1/7.0 (BP=1.000, ratio=1.073, hyp_len=24856, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.40-11.07.2.39-10.92.pth
BLEU = 20.33, 52.4/28.6/15.0/7.6 (BP=1.000, ratio=1.068, hyp_len=24727, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.39-10.91.2.34-10.34.pth
BLEU = 21.48, 53.7/29.7/15.9/8.4 (BP=1.000, ratio=1.061, hyp_len=24563, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.35-10.49.2.28-9.79.pth
BLEU = 24.02, 57.4/32.6/18.1/9.9 (BP=1.000, ratio=1.005, hyp_len=23281, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.23-9.33.2.24-9.36.pth
BLEU = 23.05, 54.5/31.1/17.3/9.6 (BP=1.000, ratio=1.081, hyp_len=25043, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.24-9.42.2.23-9.31.pth
BLEU = 22.25, 52.9/30.3/16.8/9.1 (BP=1.000, ratio=1.142, hyp_len=26457, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.20-9.04.2.14-8.51.pth
BLEU = 26.55, 59.3/35.0/20.3/11.8 (BP=1.000, ratio=1.014, hyp_len=23483, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.20-9.01.2.11-8.27.pth
BLEU = 25.37, 56.3/33.4/19.5/11.3 (BP=1.000, ratio=1.099, hyp_len=25461, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.16-8.69.2.06-7.83.pth
BLEU = 27.80, 59.7/36.1/21.6/12.8 (BP=1.000, ratio=1.041, hyp_len=24101, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.11-8.24.2.02-7.57.pth
BLEU = 27.59, 58.3/35.7/21.6/12.9 (BP=1.000, ratio=1.090, hyp_len=25240, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.10-8.17.1.97-7.20.pth
BLEU = 29.91, 61.3/38.3/23.6/14.5 (BP=1.000, ratio=1.049, hyp_len=24298, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.03-7.63.1.93-6.90.pth
BLEU = 31.58, 62.9/39.9/25.1/15.7 (BP=1.000, ratio=1.026, hyp_len=23755, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.02-7.53.1.90-6.65.pth
BLEU = 31.19, 62.1/39.4/24.8/15.6 (BP=1.000, ratio=1.061, hyp_len=24573, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.1.90-6.68.1.85-6.38.pth
BLEU = 33.96, 65.0/42.1/27.3/17.8 (BP=1.000, ratio=1.014, hyp_len=23483, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.1.96-7.07.1.83-6.22.pth
BLEU = 33.00, 63.7/41.5/26.6/16.8 (BP=1.000, ratio=1.054, hyp_len=24422, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.96-7.07.1.80-6.02.pth
BLEU = 33.55, 63.8/42.0/27.2/17.4 (BP=1.000, ratio=1.064, hyp_len=24639, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.1.86-6.40.1.76-5.79.pth
BLEU = 35.38, 65.9/43.6/28.8/18.9 (BP=1.000, ratio=1.028, hyp_len=23809, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.91-6.73.1.73-5.63.pth
BLEU = 35.28, 65.3/43.5/28.8/18.9 (BP=1.000, ratio=1.053, hyp_len=24397, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.79-6.00.1.70-5.45.pth
BLEU = 36.53, 66.3/44.7/30.0/20.0 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.83-6.23.1.69-5.42.pth
BLEU = 35.26, 64.5/43.5/29.0/19.0 (BP=1.000, ratio=1.091, hyp_len=25261, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.41.1.73-5.62.1.63-5.11.pth
BLEU = 38.60, 67.7/46.7/32.1/21.9 (BP=1.000, ratio=1.041, hyp_len=24117, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.42.1.79-5.99.1.63-5.10.pth
BLEU = 37.22, 66.2/45.4/30.8/20.7 (BP=1.000, ratio=1.073, hyp_len=24850, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.43.1.72-5.56.1.60-4.96.pth
BLEU = 37.85, 66.1/45.7/31.5/21.6 (BP=1.000, ratio=1.091, hyp_len=25268, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.44.1.59-4.91.1.55-4.73.pth
BLEU = 40.58, 69.3/48.5/33.9/23.8 (BP=1.000, ratio=1.034, hyp_len=23938, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.45.1.67-5.30.1.53-4.63.pth
BLEU = 39.81, 68.2/47.8/33.3/23.1 (BP=1.000, ratio=1.061, hyp_len=24565, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.46.1.68-5.36.1.51-4.51.pth
BLEU = 42.02, 69.7/49.6/35.5/25.4 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.47.1.65-5.21.1.48-4.41.pth
BLEU = 41.28, 69.3/49.3/34.8/24.4 (BP=1.000, ratio=1.054, hyp_len=24412, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.48.1.59-4.91.1.47-4.33.pth
BLEU = 42.42, 70.1/50.3/35.9/25.6 (BP=1.000, ratio=1.053, hyp_len=24384, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.49.1.55-4.72.1.45-4.28.pth
BLEU = 42.55, 70.3/50.5/36.1/25.6 (BP=1.000, ratio=1.053, hyp_len=24394, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.50.1.57-4.82.1.43-4.19.pth
BLEU = 45.05, 72.4/52.5/38.3/28.3 (BP=1.000, ratio=1.019, hyp_len=23600, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.51.1.59-4.91.1.41-4.11.pth
BLEU = 43.54, 70.9/51.4/37.1/26.6 (BP=1.000, ratio=1.055, hyp_len=24423, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.52.1.54-4.65.1.38-3.98.pth
BLEU = 46.12, 73.2/53.8/39.5/29.1 (BP=1.000, ratio=1.022, hyp_len=23660, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.53.1.48-4.39.1.37-3.95.pth
BLEU = 46.45, 73.2/53.9/39.8/29.6 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.54.1.55-4.70.1.36-3.88.pth
BLEU = 45.52, 72.3/53.3/39.0/28.5 (BP=1.000, ratio=1.046, hyp_len=24235, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.55.1.50-4.49.1.36-3.91.pth
BLEU = 44.69, 71.6/52.7/38.4/27.6 (BP=1.000, ratio=1.061, hyp_len=24575, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.56.1.43-4.16.1.34-3.81.pth
BLEU = 46.06, 72.3/53.7/39.7/29.2 (BP=1.000, ratio=1.056, hyp_len=24462, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.57.1.44-4.23.1.34-3.83.pth
BLEU = 45.62, 71.9/53.3/39.4/28.7 (BP=1.000, ratio=1.069, hyp_len=24767, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.58.1.43-4.17.1.29-3.64.pth
BLEU = 50.16, 75.8/57.2/43.5/33.5 (BP=1.000, ratio=1.008, hyp_len=23337, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.59.1.50-4.48.1.28-3.59.pth
BLEU = 47.79, 73.6/55.3/41.5/30.9 (BP=1.000, ratio=1.051, hyp_len=24347, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.60.1.39-4.02.1.28-3.60.pth
BLEU = 46.85, 72.7/54.4/40.6/30.0 (BP=1.000, ratio=1.064, hyp_len=24652, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.61.1.42-4.15.1.25-3.49.pth
BLEU = 49.84, 75.4/57.2/43.4/33.0 (BP=1.000, ratio=1.024, hyp_len=23713, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.62.1.42-4.14.1.30-3.65.pth
BLEU = 46.43, 72.5/54.5/40.3/29.2 (BP=1.000, ratio=1.076, hyp_len=24920, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.63.1.38-3.96.1.24-3.45.pth
BLEU = 50.86, 76.4/58.0/44.3/34.1 (BP=1.000, ratio=1.015, hyp_len=23501, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.64.1.35-3.87.1.22-3.38.pth
BLEU = 50.02, 75.2/57.4/43.7/33.2 (BP=1.000, ratio=1.040, hyp_len=24082, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.65.1.36-3.88.1.21-3.34.pth
BLEU = 51.26, 76.5/58.6/44.8/34.3 (BP=1.000, ratio=1.022, hyp_len=23674, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.66.1.32-3.76.1.20-3.32.pth
BLEU = 50.61, 75.7/58.1/44.4/33.7 (BP=1.000, ratio=1.038, hyp_len=24031, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.67.1.33-3.80.1.24-3.46.pth
BLEU = 48.07, 73.0/55.7/42.1/31.2 (BP=1.000, ratio=1.085, hyp_len=25128, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.68.1.31-3.69.1.18-3.24.pth
BLEU = 51.96, 76.9/59.2/45.6/35.1 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.69.1.28-3.59.1.16-3.19.pth
BLEU = 52.03, 76.5/59.0/45.7/35.5 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.70.1.31-3.69.1.17-3.21.pth
BLEU = 53.71, 78.2/60.7/47.3/37.0 (BP=1.000, ratio=1.007, hyp_len=23321, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.71.1.25-3.50.1.17-3.23.pth
BLEU = 50.73, 75.4/58.2/44.6/33.8 (BP=1.000, ratio=1.060, hyp_len=24558, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.72.1.34-3.83.1.15-3.15.pth
BLEU = 51.56, 75.9/58.7/45.4/34.9 (BP=1.000, ratio=1.054, hyp_len=24416, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.73.1.29-3.64.1.13-3.11.pth
BLEU = 52.79, 77.1/60.0/46.6/36.0 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.74.1.26-3.52.1.15-3.17.pth
BLEU = 51.55, 76.2/59.2/45.5/34.4 (BP=1.000, ratio=1.055, hyp_len=24425, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.75.1.25-3.50.1.13-3.09.pth
BLEU = 55.15, 78.8/61.9/48.8/38.8 (BP=1.000, ratio=1.013, hyp_len=23457, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.76.1.19-3.30.1.10-3.02.pth
BLEU = 54.13, 77.8/61.0/47.9/37.7 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.77.1.24-3.44.1.10-2.99.pth
BLEU = 55.15, 78.5/61.8/49.0/38.9 (BP=1.000, ratio=1.024, hyp_len=23714, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.78.1.28-3.59.1.13-3.08.pth
BLEU = 52.02, 76.0/59.5/46.0/35.2 (BP=1.000, ratio=1.063, hyp_len=24620, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.79.1.24-3.46.1.08-2.95.pth
BLEU = 56.56, 79.7/63.1/50.3/40.5 (BP=1.000, ratio=1.011, hyp_len=23422, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.80.1.22-3.40.1.08-2.95.pth
BLEU = 55.19, 78.5/61.8/49.0/39.0 (BP=1.000, ratio=1.027, hyp_len=23779, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.81.1.20-3.31.1.10-3.01.pth
BLEU = 52.31, 76.0/59.7/46.4/35.6 (BP=1.000, ratio=1.074, hyp_len=24876, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.82.1.22-3.38.1.06-2.89.pth
BLEU = 54.63, 77.7/61.4/48.6/38.5 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.83.1.13-3.11.1.11-3.04.pth
BLEU = 51.36, 75.4/59.0/45.5/34.4 (BP=1.000, ratio=1.081, hyp_len=25041, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.84.1.15-3.17.1.06-2.88.pth
BLEU = 55.32, 78.2/61.9/49.2/39.3 (BP=1.000, ratio=1.039, hyp_len=24052, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.85.1.15-3.17.1.04-2.84.pth
BLEU = 55.97, 78.8/62.7/49.9/39.8 (BP=1.000, ratio=1.038, hyp_len=24043, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.86.1.16-3.19.1.05-2.85.pth
BLEU = 56.14, 78.9/62.8/50.1/40.0 (BP=1.000, ratio=1.030, hyp_len=23856, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.87.1.16-3.18.1.07-2.91.pth
BLEU = 53.12, 76.4/60.4/47.2/36.6 (BP=1.000, ratio=1.070, hyp_len=24790, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.88.1.16-3.19.1.04-2.82.pth
BLEU = 56.01, 78.6/62.5/50.0/40.1 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.89.1.10-3.01.1.03-2.79.pth
BLEU = 56.28, 79.0/63.2/50.4/39.9 (BP=1.000, ratio=1.036, hyp_len=23996, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.90.1.09-2.99.1.03-2.79.pth
BLEU = 57.37, 79.9/63.9/51.3/41.4 (BP=1.000, ratio=1.023, hyp_len=23687, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.91.1.07-2.93.1.01-2.76.pth
BLEU = 56.63, 79.2/63.4/50.7/40.5 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.92.1.13-3.11.1.00-2.73.pth
BLEU = 56.67, 78.5/62.9/50.8/41.1 (BP=1.000, ratio=1.046, hyp_len=24234, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.93.1.11-3.02.1.01-2.75.pth
BLEU = 58.07, 80.1/64.7/52.2/42.1 (BP=1.000, ratio=1.022, hyp_len=23672, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.94.1.07-2.92.1.00-2.71.pth
BLEU = 56.73, 78.9/63.3/50.8/40.8 (BP=1.000, ratio=1.044, hyp_len=24178, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.95.1.03-2.79.1.00-2.73.pth
BLEU = 56.41, 78.5/63.1/50.6/40.4 (BP=1.000, ratio=1.052, hyp_len=24359, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.96.1.12-3.08.0.99-2.69.pth
BLEU = 58.16, 79.9/64.3/52.2/42.7 (BP=1.000, ratio=1.029, hyp_len=23841, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.97.1.14-3.12.1.00-2.71.pth
BLEU = 56.42, 78.6/63.2/50.6/40.3 (BP=1.000, ratio=1.052, hyp_len=24359, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.98.1.06-2.90.0.99-2.68.pth
BLEU = 56.75, 79.1/63.5/50.9/40.6 (BP=1.000, ratio=1.047, hyp_len=24239, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.99.1.04-2.83.0.99-2.69.pth
BLEU = 55.75, 77.7/62.5/50.0/39.8 (BP=1.000, ratio=1.069, hyp_len=24747, ref_len=23160)
/home/ye/exp/simple-nmt

real	54m13.535s
user	53m10.438s
sys	2m10.106s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

## Transformer Baseline (rk-my)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.pth
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
    'model_fn': './model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.pth',
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.42e+05 loss=5.7605e+00 ppl=317.50                                                
Validation - loss=5.7667e+00 ppl=319.50 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.17e+05 loss=5.0013e+00 ppl=148.60                                                
Validation - loss=5.0280e+00 ppl=152.62 best_loss=5.7667e+00 best_ppl=319.50                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.29e+05 loss=4.5645e+00 ppl=96.02                                                 
Validation - loss=4.6510e+00 ppl=104.69 best_loss=5.0280e+00 best_ppl=152.62                                            
Epoch 4 - |param|=3.24e+02 |g_param|=2.07e+05 loss=4.2896e+00 ppl=72.94                                                 
Validation - loss=4.3877e+00 ppl=80.46 best_loss=4.6510e+00 best_ppl=104.69                                             
Epoch 5 - |param|=3.25e+02 |g_param|=1.72e+05 loss=4.0282e+00 ppl=56.16                                                 
Validation - loss=4.1634e+00 ppl=64.29 best_loss=4.3877e+00 best_ppl=80.46                                              
Epoch 6 - |param|=3.25e+02 |g_param|=1.56e+05 loss=3.8734e+00 ppl=48.10                                                 
Validation - loss=3.9540e+00 ppl=52.14 best_loss=4.1634e+00 best_ppl=64.29                                              
Epoch 7 - |param|=3.25e+02 |g_param|=2.00e+05 loss=3.7132e+00 ppl=40.98                                                 
Validation - loss=3.7754e+00 ppl=43.61 best_loss=3.9540e+00 best_ppl=52.14                                              
Epoch 8 - |param|=3.25e+02 |g_param|=2.47e+05 loss=3.5251e+00 ppl=33.96                                                 
Validation - loss=3.6264e+00 ppl=37.58 best_loss=3.7754e+00 best_ppl=43.61                                              
Epoch 9 - |param|=3.25e+02 |g_param|=2.21e+05 loss=3.3909e+00 ppl=29.69                                                 
Validation - loss=3.4787e+00 ppl=32.42 best_loss=3.6264e+00 best_ppl=37.58                                              
Epoch 10 - |param|=3.25e+02 |g_param|=2.07e+05 loss=3.2512e+00 ppl=25.82                                                
Validation - loss=3.3536e+00 ppl=28.61 best_loss=3.4787e+00 best_ppl=32.42                                              
Epoch 11 - |param|=3.25e+02 |g_param|=2.36e+05 loss=3.1942e+00 ppl=24.39                                                
Validation - loss=3.2512e+00 ppl=25.82 best_loss=3.3536e+00 best_ppl=28.61                                              
Epoch 12 - |param|=3.25e+02 |g_param|=2.34e+05 loss=3.1157e+00 ppl=22.55                                                
Validation - loss=3.1528e+00 ppl=23.40 best_loss=3.2512e+00 best_ppl=25.82                                              
Epoch 13 - |param|=3.25e+02 |g_param|=1.86e+05 loss=2.9803e+00 ppl=19.69                                                
Validation - loss=3.0616e+00 ppl=21.36 best_loss=3.1528e+00 best_ppl=23.40                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.12e+05 loss=2.8889e+00 ppl=17.97                                                
Validation - loss=2.9792e+00 ppl=19.67 best_loss=3.0616e+00 best_ppl=21.36                                              
Epoch 15 - |param|=3.25e+02 |g_param|=5.09e+05 loss=2.8773e+00 ppl=17.77                                                
Validation - loss=2.9290e+00 ppl=18.71 best_loss=2.9792e+00 best_ppl=19.67                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.63e+05 loss=2.7649e+00 ppl=15.88                                                
Validation - loss=2.8425e+00 ppl=17.16 best_loss=2.9290e+00 best_ppl=18.71                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.57e+05 loss=2.7382e+00 ppl=15.46                                                
Validation - loss=2.7672e+00 ppl=15.91 best_loss=2.8425e+00 best_ppl=17.16                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.18e+05 loss=2.6890e+00 ppl=14.72                                                
Validation - loss=2.7008e+00 ppl=14.89 best_loss=2.7672e+00 best_ppl=15.91                                              
Epoch 19 - |param|=3.26e+02 |g_param|=3.10e+05 loss=2.6390e+00 ppl=14.00                                                
Validation - loss=2.6460e+00 ppl=14.10 best_loss=2.7008e+00 best_ppl=14.89                                              
Epoch 20 - |param|=3.26e+02 |g_param|=3.19e+05 loss=2.5618e+00 ppl=12.96                                                
Validation - loss=2.5815e+00 ppl=13.22 best_loss=2.6460e+00 best_ppl=14.10                                              
Epoch 21 - |param|=3.26e+02 |g_param|=4.40e+05 loss=2.5495e+00 ppl=12.80                                                
Validation - loss=2.5272e+00 ppl=12.52 best_loss=2.5815e+00 best_ppl=13.22                                              
Epoch 22 - |param|=3.26e+02 |g_param|=2.73e+05 loss=2.5225e+00 ppl=12.46                                                
Validation - loss=2.4673e+00 ppl=11.79 best_loss=2.5272e+00 best_ppl=12.52                                              
Epoch 23 - |param|=3.26e+02 |g_param|=4.02e+05 loss=2.4489e+00 ppl=11.58                                                
Validation - loss=2.4207e+00 ppl=11.25 best_loss=2.4673e+00 best_ppl=11.79                                              
Epoch 24 - |param|=3.26e+02 |g_param|=5.42e+05 loss=2.3963e+00 ppl=10.98                                                
Validation - loss=2.3756e+00 ppl=10.76 best_loss=2.4207e+00 best_ppl=11.25                                              
Epoch 25 - |param|=3.26e+02 |g_param|=4.36e+05 loss=2.3570e+00 ppl=10.56                                                
Validation - loss=2.3175e+00 ppl=10.15 best_loss=2.3756e+00 best_ppl=10.76                                              
Epoch 26 - |param|=3.26e+02 |g_param|=3.99e+05 loss=2.3088e+00 ppl=10.06                                                
Validation - loss=2.2715e+00 ppl=9.69 best_loss=2.3175e+00 best_ppl=10.15                                               
Epoch 27 - |param|=3.26e+02 |g_param|=4.27e+05 loss=2.2228e+00 ppl=9.23                                                 
Validation - loss=2.2270e+00 ppl=9.27 best_loss=2.2715e+00 best_ppl=9.69                                                
Epoch 28 - |param|=3.26e+02 |g_param|=3.68e+05 loss=2.2545e+00 ppl=9.53                                                 
Validation - loss=2.1853e+00 ppl=8.89 best_loss=2.2270e+00 best_ppl=9.27                                                
Epoch 29 - |param|=3.26e+02 |g_param|=3.72e+05 loss=2.1648e+00 ppl=8.71                                                 
Validation - loss=2.1458e+00 ppl=8.55 best_loss=2.1853e+00 best_ppl=8.89                                                
Epoch 30 - |param|=3.26e+02 |g_param|=5.26e+05 loss=2.1417e+00 ppl=8.51                                                 
Validation - loss=2.1030e+00 ppl=8.19 best_loss=2.1458e+00 best_ppl=8.55                                                
Epoch 31 - |param|=3.26e+02 |g_param|=3.61e+05 loss=2.1454e+00 ppl=8.55                                                 
Validation - loss=2.0542e+00 ppl=7.80 best_loss=2.1030e+00 best_ppl=8.19                                                
Epoch 32 - |param|=3.26e+02 |g_param|=3.60e+05 loss=2.0830e+00 ppl=8.03                                                 
Validation - loss=2.0267e+00 ppl=7.59 best_loss=2.0542e+00 best_ppl=7.80                                                
Epoch 33 - |param|=3.26e+02 |g_param|=4.76e+05 loss=2.0673e+00 ppl=7.90                                                 
Validation - loss=1.9721e+00 ppl=7.19 best_loss=2.0267e+00 best_ppl=7.59                                                
Epoch 34 - |param|=3.26e+02 |g_param|=3.79e+05 loss=2.0101e+00 ppl=7.46                                                 
Validation - loss=1.9543e+00 ppl=7.06 best_loss=1.9721e+00 best_ppl=7.19                                                
Epoch 35 - |param|=3.26e+02 |g_param|=4.33e+05 loss=2.0239e+00 ppl=7.57                                                 
Validation - loss=1.9120e+00 ppl=6.77 best_loss=1.9543e+00 best_ppl=7.06                                                
Epoch 36 - |param|=3.27e+02 |g_param|=5.96e+05 loss=1.9820e+00 ppl=7.26                                                 
Validation - loss=1.8709e+00 ppl=6.49 best_loss=1.9120e+00 best_ppl=6.77                                                
Epoch 37 - |param|=3.27e+02 |g_param|=4.50e+05 loss=1.9032e+00 ppl=6.71                                                 
Validation - loss=1.8298e+00 ppl=6.23 best_loss=1.8709e+00 best_ppl=6.49                                                
Epoch 38 - |param|=3.27e+02 |g_param|=7.09e+05 loss=1.8742e+00 ppl=6.52                                                 
Validation - loss=1.8229e+00 ppl=6.19 best_loss=1.8298e+00 best_ppl=6.23                                                
Epoch 39 - |param|=3.27e+02 |g_param|=4.25e+05 loss=1.8650e+00 ppl=6.46                                                 
Validation - loss=1.7680e+00 ppl=5.86 best_loss=1.8229e+00 best_ppl=6.19                                                
Epoch 40 - |param|=3.27e+02 |g_param|=5.18e+05 loss=1.8404e+00 ppl=6.30                                                 
Validation - loss=1.7344e+00 ppl=5.67 best_loss=1.7680e+00 best_ppl=5.86                                                
Epoch 41 - |param|=3.27e+02 |g_param|=4.44e+05 loss=1.8633e+00 ppl=6.44                                                 
Validation - loss=1.7004e+00 ppl=5.48 best_loss=1.7344e+00 best_ppl=5.67                                                
Epoch 42 - |param|=3.27e+02 |g_param|=3.12e+05 loss=1.7912e+00 ppl=6.00                                                 
Validation - loss=1.6766e+00 ppl=5.35 best_loss=1.7004e+00 best_ppl=5.48                                                
Epoch 43 - |param|=3.27e+02 |g_param|=2.60e+05 loss=1.7399e+00 ppl=5.70                                                 
Validation - loss=1.6518e+00 ppl=5.22 best_loss=1.6766e+00 best_ppl=5.35                                                
Epoch 44 - |param|=3.27e+02 |g_param|=3.00e+05 loss=1.6743e+00 ppl=5.34                                                 
Validation - loss=1.6285e+00 ppl=5.10 best_loss=1.6518e+00 best_ppl=5.22                                                
Epoch 45 - |param|=3.27e+02 |g_param|=2.68e+05 loss=1.6685e+00 ppl=5.30                                                 
Validation - loss=1.5976e+00 ppl=4.94 best_loss=1.6285e+00 best_ppl=5.10                                                
Epoch 46 - |param|=3.27e+02 |g_param|=3.68e+05 loss=1.6495e+00 ppl=5.20                                                 
Validation - loss=1.5745e+00 ppl=4.83 best_loss=1.5976e+00 best_ppl=4.94                                                
Epoch 47 - |param|=3.27e+02 |g_param|=2.63e+05 loss=1.7434e+00 ppl=5.72                                                 
Validation - loss=1.5452e+00 ppl=4.69 best_loss=1.5745e+00 best_ppl=4.83                                                
Epoch 48 - |param|=3.27e+02 |g_param|=3.08e+05 loss=1.6673e+00 ppl=5.30                                                 
Validation - loss=1.5281e+00 ppl=4.61 best_loss=1.5452e+00 best_ppl=4.69                                                
Epoch 49 - |param|=3.27e+02 |g_param|=2.95e+05 loss=1.6355e+00 ppl=5.13                                                 
Validation - loss=1.5035e+00 ppl=4.50 best_loss=1.5281e+00 best_ppl=4.61                                                
Epoch 50 - |param|=3.27e+02 |g_param|=2.62e+05 loss=1.5802e+00 ppl=4.86                                                 
Validation - loss=1.4862e+00 ppl=4.42 best_loss=1.5035e+00 best_ppl=4.50                                                
Epoch 51 - |param|=3.27e+02 |g_param|=3.18e+05 loss=1.6030e+00 ppl=4.97                                                 
Validation - loss=1.4725e+00 ppl=4.36 best_loss=1.4862e+00 best_ppl=4.42                                                
Epoch 52 - |param|=3.27e+02 |g_param|=3.37e+05 loss=1.6035e+00 ppl=4.97                                                 
Validation - loss=1.4559e+00 ppl=4.29 best_loss=1.4725e+00 best_ppl=4.36                                                
Epoch 53 - |param|=3.27e+02 |g_param|=2.71e+05 loss=1.5137e+00 ppl=4.54                                                 
Validation - loss=1.4371e+00 ppl=4.21 best_loss=1.4559e+00 best_ppl=4.29                                                
Epoch 54 - |param|=3.27e+02 |g_param|=2.86e+05 loss=1.5316e+00 ppl=4.63                                                 
Validation - loss=1.4178e+00 ppl=4.13 best_loss=1.4371e+00 best_ppl=4.21                                                
Epoch 55 - |param|=3.27e+02 |g_param|=3.49e+05 loss=1.6022e+00 ppl=4.96                                                 
Validation - loss=1.4032e+00 ppl=4.07 best_loss=1.4178e+00 best_ppl=4.13                                                
Epoch 56 - |param|=3.27e+02 |g_param|=2.91e+05 loss=1.5111e+00 ppl=4.53                                                 
Validation - loss=1.3839e+00 ppl=3.99 best_loss=1.4032e+00 best_ppl=4.07                                                
Epoch 57 - |param|=3.27e+02 |g_param|=4.67e+05 loss=1.4950e+00 ppl=4.46                                                 
Validation - loss=1.3627e+00 ppl=3.91 best_loss=1.3839e+00 best_ppl=3.99                                                
Epoch 58 - |param|=3.27e+02 |g_param|=4.08e+05 loss=1.5085e+00 ppl=4.52                                                 
Validation - loss=1.3484e+00 ppl=3.85 best_loss=1.3627e+00 best_ppl=3.91                                                
Epoch 59 - |param|=3.27e+02 |g_param|=3.11e+05 loss=1.4758e+00 ppl=4.37                                                 
Validation - loss=1.3438e+00 ppl=3.83 best_loss=1.3484e+00 best_ppl=3.85                                                
Epoch 60 - |param|=3.27e+02 |g_param|=2.83e+05 loss=1.4623e+00 ppl=4.32                                                 
Validation - loss=1.3144e+00 ppl=3.72 best_loss=1.3438e+00 best_ppl=3.83                                                
Epoch 61 - |param|=3.27e+02 |g_param|=3.89e+05 loss=1.4360e+00 ppl=4.20                                                 
Validation - loss=1.3351e+00 ppl=3.80 best_loss=1.3144e+00 best_ppl=3.72                                                
Epoch 62 - |param|=3.27e+02 |g_param|=3.50e+05 loss=1.4777e+00 ppl=4.38                                                 
Validation - loss=1.2880e+00 ppl=3.63 best_loss=1.3144e+00 best_ppl=3.72                                                
Epoch 63 - |param|=3.27e+02 |g_param|=2.89e+05 loss=1.4442e+00 ppl=4.24                                                 
Validation - loss=1.2810e+00 ppl=3.60 best_loss=1.2880e+00 best_ppl=3.63                                                
Epoch 64 - |param|=3.27e+02 |g_param|=4.41e+05 loss=1.3813e+00 ppl=3.98                                                 
Validation - loss=1.2680e+00 ppl=3.55 best_loss=1.2810e+00 best_ppl=3.60                                                
Epoch 65 - |param|=3.27e+02 |g_param|=3.18e+05 loss=1.3791e+00 ppl=3.97                                                 
Validation - loss=1.2899e+00 ppl=3.63 best_loss=1.2680e+00 best_ppl=3.55                                                
Epoch 66 - |param|=3.27e+02 |g_param|=3.49e+05 loss=1.4288e+00 ppl=4.17                                                 
Validation - loss=1.2386e+00 ppl=3.45 best_loss=1.2680e+00 best_ppl=3.55                                                
Epoch 67 - |param|=3.27e+02 |g_param|=3.82e+05 loss=1.3214e+00 ppl=3.75                                                 
Validation - loss=1.2413e+00 ppl=3.46 best_loss=1.2386e+00 best_ppl=3.45                                                
Epoch 68 - |param|=3.28e+02 |g_param|=2.64e+05 loss=1.3289e+00 ppl=3.78                                                 
Validation - loss=1.2245e+00 ppl=3.40 best_loss=1.2386e+00 best_ppl=3.45                                                
Epoch 69 - |param|=3.28e+02 |g_param|=3.36e+05 loss=1.3742e+00 ppl=3.95                                                 
Validation - loss=1.2120e+00 ppl=3.36 best_loss=1.2245e+00 best_ppl=3.40                                                
Epoch 70 - |param|=3.28e+02 |g_param|=4.42e+05 loss=1.2653e+00 ppl=3.54                                                 
Validation - loss=1.2118e+00 ppl=3.36 best_loss=1.2120e+00 best_ppl=3.36                                                
Epoch 71 - |param|=3.28e+02 |g_param|=3.30e+05 loss=1.3452e+00 ppl=3.84                                                 
Validation - loss=1.1977e+00 ppl=3.31 best_loss=1.2118e+00 best_ppl=3.36                                                
Epoch 72 - |param|=3.28e+02 |g_param|=2.69e+05 loss=1.2741e+00 ppl=3.58                                                 
Validation - loss=1.1765e+00 ppl=3.24 best_loss=1.1977e+00 best_ppl=3.31                                                
Epoch 73 - |param|=3.28e+02 |g_param|=5.21e+05 loss=1.3732e+00 ppl=3.95                                                 
Validation - loss=1.1703e+00 ppl=3.22 best_loss=1.1765e+00 best_ppl=3.24                                                
Epoch 74 - |param|=3.28e+02 |g_param|=4.05e+05 loss=1.2888e+00 ppl=3.63                                                 
Validation - loss=1.1598e+00 ppl=3.19 best_loss=1.1703e+00 best_ppl=3.22                                                
Epoch 75 - |param|=3.28e+02 |g_param|=6.54e+05 loss=1.2817e+00 ppl=3.60                                                 
Validation - loss=1.1610e+00 ppl=3.19 best_loss=1.1598e+00 best_ppl=3.19                                                
Epoch 76 - |param|=3.28e+02 |g_param|=5.13e+05 loss=1.2851e+00 ppl=3.62                                                 
Validation - loss=1.1577e+00 ppl=3.18 best_loss=1.1598e+00 best_ppl=3.19                                                
Epoch 77 - |param|=3.28e+02 |g_param|=3.90e+05 loss=1.2192e+00 ppl=3.38                                                 
Validation - loss=1.1838e+00 ppl=3.27 best_loss=1.1577e+00 best_ppl=3.18                                                
Epoch 78 - |param|=3.28e+02 |g_param|=2.44e+05 loss=1.2020e+00 ppl=3.33                                                 
Validation - loss=1.1316e+00 ppl=3.10 best_loss=1.1577e+00 best_ppl=3.18                                                
Epoch 79 - |param|=3.28e+02 |g_param|=2.75e+05 loss=1.2149e+00 ppl=3.37                                                 
Validation - loss=1.1175e+00 ppl=3.06 best_loss=1.1316e+00 best_ppl=3.10                                                
Epoch 80 - |param|=3.28e+02 |g_param|=7.17e+05 loss=1.2248e+00 ppl=3.40                                                 
Validation - loss=1.1221e+00 ppl=3.07 best_loss=1.1175e+00 best_ppl=3.06                                                
Epoch 81 - |param|=3.28e+02 |g_param|=2.31e+05 loss=1.1524e+00 ppl=3.17                                                 
Validation - loss=1.1116e+00 ppl=3.04 best_loss=1.1175e+00 best_ppl=3.06                                                
Epoch 82 - |param|=3.28e+02 |g_param|=3.13e+05 loss=1.2491e+00 ppl=3.49                                                 
Validation - loss=1.0994e+00 ppl=3.00 best_loss=1.1116e+00 best_ppl=3.04                                                
Epoch 83 - |param|=3.28e+02 |g_param|=4.53e+05 loss=1.1966e+00 ppl=3.31                                                 
Validation - loss=1.1315e+00 ppl=3.10 best_loss=1.0994e+00 best_ppl=3.00                                                
Epoch 84 - |param|=3.28e+02 |g_param|=3.45e+05 loss=1.2112e+00 ppl=3.36                                                 
Validation - loss=1.0849e+00 ppl=2.96 best_loss=1.0994e+00 best_ppl=3.00                                                
Epoch 85 - |param|=3.28e+02 |g_param|=5.76e+05 loss=1.2424e+00 ppl=3.46                                                 
Validation - loss=1.0848e+00 ppl=2.96 best_loss=1.0849e+00 best_ppl=2.96                                                
Epoch 86 - |param|=3.28e+02 |g_param|=5.18e+05 loss=1.2311e+00 ppl=3.42                                                 
Validation - loss=1.0854e+00 ppl=2.96 best_loss=1.0848e+00 best_ppl=2.96                                                
Epoch 87 - |param|=3.28e+02 |g_param|=3.30e+05 loss=1.1407e+00 ppl=3.13                                                 
Validation - loss=1.0700e+00 ppl=2.92 best_loss=1.0848e+00 best_ppl=2.96                                                
Epoch 88 - |param|=3.28e+02 |g_param|=4.29e+05 loss=1.1901e+00 ppl=3.29                                                 
Validation - loss=1.0569e+00 ppl=2.88 best_loss=1.0700e+00 best_ppl=2.92                                                
Epoch 89 - |param|=3.28e+02 |g_param|=5.91e+05 loss=1.1857e+00 ppl=3.27                                                 
Validation - loss=1.0623e+00 ppl=2.89 best_loss=1.0569e+00 best_ppl=2.88                                                
Epoch 90 - |param|=3.28e+02 |g_param|=2.80e+05 loss=1.1735e+00 ppl=3.23                                                 
Validation - loss=1.0618e+00 ppl=2.89 best_loss=1.0569e+00 best_ppl=2.88                                                
Epoch 91 - |param|=3.28e+02 |g_param|=3.49e+05 loss=1.1382e+00 ppl=3.12                                                 
Validation - loss=1.0414e+00 ppl=2.83 best_loss=1.0569e+00 best_ppl=2.88                                                
Epoch 92 - |param|=3.28e+02 |g_param|=4.49e+05 loss=1.1457e+00 ppl=3.14                                                 
Validation - loss=1.0366e+00 ppl=2.82 best_loss=1.0414e+00 best_ppl=2.83                                                
Epoch 93 - |param|=3.28e+02 |g_param|=2.70e+05 loss=1.1333e+00 ppl=3.11                                                 
Validation - loss=1.0319e+00 ppl=2.81 best_loss=1.0366e+00 best_ppl=2.82                                                
Epoch 94 - |param|=3.28e+02 |g_param|=4.39e+05 loss=1.0393e+00 ppl=2.83                                                 
Validation - loss=1.0299e+00 ppl=2.80 best_loss=1.0319e+00 best_ppl=2.81                                                
Epoch 95 - |param|=3.28e+02 |g_param|=4.40e+05 loss=1.1172e+00 ppl=3.06                                                 
Validation - loss=1.0375e+00 ppl=2.82 best_loss=1.0299e+00 best_ppl=2.80                                                
Epoch 96 - |param|=3.28e+02 |g_param|=7.53e+05 loss=1.1543e+00 ppl=3.17                                                 
Validation - loss=1.0383e+00 ppl=2.82 best_loss=1.0299e+00 best_ppl=2.80                                                
Epoch 97 - |param|=3.28e+02 |g_param|=5.02e+05 loss=1.0615e+00 ppl=2.89                                                 
Validation - loss=1.0151e+00 ppl=2.76 best_loss=1.0299e+00 best_ppl=2.80                                                
Epoch 98 - |param|=3.28e+02 |g_param|=2.76e+05 loss=1.0562e+00 ppl=2.88                                                 
Validation - loss=1.0040e+00 ppl=2.73 best_loss=1.0151e+00 best_ppl=2.76                                                
Epoch 99 - |param|=3.28e+02 |g_param|=2.66e+05 loss=1.0760e+00 ppl=2.93                                                 
Validation - loss=9.9922e-01 ppl=2.72 best_loss=1.0040e+00 best_ppl=2.73                                                
Epoch 100 - |param|=3.28e+02 |g_param|=3.40e+05 loss=1.0983e+00 ppl=3.00                                                
Validation - loss=9.9959e-01 ppl=2.72 best_loss=9.9922e-01 best_ppl=2.72                                                

real	52m23.290s
user	52m9.593s
sys	0m9.563s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation...   

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-baseline-transformer-rkmy.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.76-317.50.5.77-319.50.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.0/0.0/0.0/0.0 (BP=0.036, ratio=0.231, hyp_len=5433, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.5.00-148.60.5.03-152.62.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.8/0.7/0.0/0.0 (BP=0.395, ratio=0.518, hyp_len=12184, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.56-96.02.4.65-104.69.pth
BLEU = 0.24, 22.5/1.9/0.1/0.0 (BP=0.509, ratio=0.597, hyp_len=14038, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.29-72.94.4.39-80.46.pth
BLEU = 0.57, 23.7/5.5/0.2/0.0 (BP=0.898, ratio=0.903, hyp_len=21217, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.03-56.16.4.16-64.29.pth
BLEU = 2.03, 30.5/9.3/1.0/0.1 (BP=0.854, ratio=0.864, hyp_len=20304, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.87-48.10.3.95-52.14.pth
BLEU = 2.88, 26.0/8.3/1.5/0.2 (BP=1.000, ratio=1.119, hyp_len=26302, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.71-40.98.3.78-43.61.pth
BLEU = 2.69, 21.0/7.1/1.5/0.2 (BP=1.000, ratio=1.520, hyp_len=35745, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.53-33.96.3.63-37.58.pth
BLEU = 2.84, 19.7/7.0/1.6/0.3 (BP=1.000, ratio=1.758, hyp_len=41331, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.39-29.69.3.48-32.42.pth
BLEU = 4.62, 28.6/10.6/2.6/0.6 (BP=1.000, ratio=1.249, hyp_len=29360, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.100.1.10-3.00.1.00-2.72.pth
BLEU = 55.26, 77.5/62.3/49.3/39.2 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.25-25.82.3.35-28.61.pth
BLEU = 5.22, 28.0/10.8/3.0/0.8 (BP=1.000, ratio=1.360, hyp_len=31966, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.19-24.39.3.25-25.82.pth
BLEU = 5.34, 25.8/10.3/3.2/1.0 (BP=1.000, ratio=1.579, hyp_len=37118, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.12-22.55.3.15-23.40.pth
BLEU = 7.58, 34.2/14.2/4.7/1.4 (BP=1.000, ratio=1.187, hyp_len=27915, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.2.98-19.69.3.06-21.36.pth
BLEU = 8.84, 36.2/15.6/5.6/1.9 (BP=1.000, ratio=1.172, hyp_len=27559, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.89-17.97.2.98-19.67.pth
BLEU = 9.82, 38.3/16.9/6.3/2.3 (BP=1.000, ratio=1.135, hyp_len=26676, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.88-17.77.2.93-18.71.pth
BLEU = 8.80, 32.4/14.6/5.8/2.2 (BP=1.000, ratio=1.412, hyp_len=33185, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.76-15.88.2.84-17.16.pth
BLEU = 10.51, 37.9/17.3/7.0/2.6 (BP=1.000, ratio=1.215, hyp_len=28574, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.74-15.46.2.77-15.91.pth
BLEU = 12.81, 43.5/20.3/8.6/3.5 (BP=1.000, ratio=1.075, hyp_len=25274, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.69-14.72.2.70-14.89.pth
BLEU = 13.18, 43.3/20.6/9.0/3.8 (BP=1.000, ratio=1.120, hyp_len=26320, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.64-14.00.2.65-14.10.pth
BLEU = 15.75, 48.6/23.9/10.9/4.9 (BP=1.000, ratio=1.004, hyp_len=23599, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.56-12.96.2.58-13.22.pth
BLEU = 16.36, 48.6/24.5/11.5/5.2 (BP=1.000, ratio=1.033, hyp_len=24280, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.55-12.80.2.53-12.52.pth
BLEU = 17.29, 49.7/25.3/12.2/5.8 (BP=1.000, ratio=1.025, hyp_len=24104, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.52-12.46.2.47-11.79.pth
BLEU = 17.37, 48.8/25.3/12.4/5.9 (BP=1.000, ratio=1.064, hyp_len=25014, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.45-11.58.2.42-11.25.pth
BLEU = 17.34, 47.6/25.1/12.5/6.1 (BP=1.000, ratio=1.117, hyp_len=26251, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.40-10.98.2.38-10.76.pth
BLEU = 17.37, 46.7/24.9/12.6/6.2 (BP=1.000, ratio=1.164, hyp_len=27373, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.36-10.56.2.32-10.15.pth
BLEU = 20.56, 52.6/28.8/15.0/7.8 (BP=1.000, ratio=1.039, hyp_len=24436, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.31-10.06.2.27-9.69.pth
BLEU = 21.12, 52.9/29.4/15.6/8.2 (BP=1.000, ratio=1.055, hyp_len=24812, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.22-9.23.2.23-9.27.pth
BLEU = 21.20, 52.5/29.5/15.6/8.4 (BP=1.000, ratio=1.078, hyp_len=25335, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.25-9.53.2.19-8.89.pth
BLEU = 21.87, 52.7/30.0/16.3/8.9 (BP=1.000, ratio=1.092, hyp_len=25680, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.16-8.71.2.15-8.55.pth
BLEU = 22.32, 53.1/30.5/16.7/9.2 (BP=1.000, ratio=1.103, hyp_len=25931, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.14-8.51.2.10-8.19.pth
BLEU = 24.24, 55.2/32.4/18.4/10.5 (BP=1.000, ratio=1.068, hyp_len=25119, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.31.2.15-8.55.2.05-7.80.pth
BLEU = 25.69, 57.0/34.1/19.6/11.4 (BP=1.000, ratio=1.051, hyp_len=24710, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.32.2.08-8.03.2.03-7.59.pth
BLEU = 25.42, 55.3/33.4/19.5/11.6 (BP=1.000, ratio=1.105, hyp_len=25976, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.33.2.07-7.90.1.97-7.19.pth
BLEU = 28.08, 58.6/36.3/21.8/13.4 (BP=1.000, ratio=1.050, hyp_len=24689, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.34.2.01-7.46.1.95-7.06.pth
BLEU = 27.53, 57.1/35.5/21.5/13.1 (BP=1.000, ratio=1.108, hyp_len=26047, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.35.2.02-7.57.1.91-6.77.pth
BLEU = 28.40, 58.3/36.6/22.3/13.7 (BP=1.000, ratio=1.086, hyp_len=25539, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.36.1.98-7.26.1.87-6.49.pth
BLEU = 29.33, 58.7/37.3/23.2/14.6 (BP=1.000, ratio=1.097, hyp_len=25800, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.37.1.90-6.71.1.83-6.23.pth
BLEU = 31.55, 61.7/39.7/25.1/16.1 (BP=1.000, ratio=1.053, hyp_len=24756, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.38.1.87-6.52.1.82-6.19.pth
BLEU = 30.71, 60.1/38.8/24.5/15.6 (BP=1.000, ratio=1.088, hyp_len=25575, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.39.1.86-6.46.1.77-5.86.pth
BLEU = 33.63, 63.1/41.6/27.2/17.9 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.40.1.84-6.30.1.73-5.67.pth
BLEU = 33.11, 62.0/41.0/26.7/17.7 (BP=1.000, ratio=1.072, hyp_len=25197, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.41.1.86-6.44.1.70-5.48.pth
BLEU = 35.84, 65.3/43.9/29.1/19.8 (BP=1.000, ratio=1.024, hyp_len=24078, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.42.1.79-6.00.1.68-5.35.pth
BLEU = 35.29, 64.3/43.4/28.8/19.3 (BP=1.000, ratio=1.051, hyp_len=24697, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.43.1.74-5.70.1.65-5.22.pth
BLEU = 36.15, 65.1/44.2/29.6/20.0 (BP=1.000, ratio=1.047, hyp_len=24617, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.44.1.67-5.34.1.63-5.10.pth
BLEU = 38.22, 67.6/46.2/31.4/21.7 (BP=1.000, ratio=1.013, hyp_len=23805, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.45.1.67-5.30.1.60-4.94.pth
BLEU = 38.16, 66.4/46.0/31.5/22.0 (BP=1.000, ratio=1.040, hyp_len=24447, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.46.1.65-5.20.1.57-4.83.pth
BLEU = 39.01, 67.4/46.9/32.4/22.6 (BP=1.000, ratio=1.031, hyp_len=24241, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.47.1.74-5.72.1.55-4.69.pth
BLEU = 39.36, 67.7/47.2/32.7/23.0 (BP=1.000, ratio=1.036, hyp_len=24358, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.48.1.67-5.30.1.53-4.61.pth
BLEU = 39.22, 67.5/47.3/32.6/22.8 (BP=1.000, ratio=1.047, hyp_len=24624, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.49.1.64-5.13.1.50-4.50.pth
BLEU = 40.82, 68.2/48.5/34.3/24.5 (BP=1.000, ratio=1.042, hyp_len=24499, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.50.1.58-4.86.1.49-4.42.pth
BLEU = 40.68, 68.3/48.5/34.1/24.3 (BP=1.000, ratio=1.048, hyp_len=24644, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.51.1.60-4.97.1.47-4.36.pth
BLEU = 41.07, 68.9/49.1/34.5/24.4 (BP=1.000, ratio=1.043, hyp_len=24509, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.52.1.60-4.97.1.46-4.29.pth
BLEU = 41.04, 68.4/49.0/34.6/24.5 (BP=1.000, ratio=1.057, hyp_len=24852, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.53.1.51-4.54.1.44-4.21.pth
BLEU = 42.17, 69.3/49.9/35.6/25.7 (BP=1.000, ratio=1.047, hyp_len=24606, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.54.1.53-4.63.1.42-4.13.pth
BLEU = 42.01, 68.7/49.5/35.5/25.7 (BP=1.000, ratio=1.060, hyp_len=24908, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.55.1.60-4.96.1.40-4.07.pth
BLEU = 42.28, 68.8/50.0/35.9/25.9 (BP=1.000, ratio=1.070, hyp_len=25160, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.56.1.51-4.53.1.38-3.99.pth
BLEU = 43.13, 69.8/50.9/36.7/26.5 (BP=1.000, ratio=1.056, hyp_len=24816, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.57.1.50-4.46.1.36-3.91.pth
BLEU = 44.57, 71.2/52.3/38.0/27.9 (BP=1.000, ratio=1.040, hyp_len=24447, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.58.1.51-4.52.1.35-3.85.pth
BLEU = 45.66, 72.2/53.3/39.0/29.0 (BP=1.000, ratio=1.027, hyp_len=24145, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.59.1.48-4.37.1.34-3.83.pth
BLEU = 44.05, 70.4/51.9/37.7/27.4 (BP=1.000, ratio=1.062, hyp_len=24969, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.60.1.46-4.32.1.31-3.72.pth
BLEU = 45.53, 71.4/52.9/39.0/29.2 (BP=1.000, ratio=1.047, hyp_len=24619, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.61.1.44-4.20.1.34-3.80.pth
BLEU = 43.13, 69.0/51.0/36.9/26.6 (BP=1.000, ratio=1.091, hyp_len=25644, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.62.1.48-4.38.1.29-3.63.pth
BLEU = 47.38, 73.3/54.9/40.8/30.6 (BP=1.000, ratio=1.027, hyp_len=24139, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.63.1.44-4.24.1.28-3.60.pth
BLEU = 46.57, 71.9/54.0/40.2/30.1 (BP=1.000, ratio=1.053, hyp_len=24744, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.64.1.38-3.98.1.27-3.55.pth
BLEU = 47.79, 73.3/55.2/41.3/31.2 (BP=1.000, ratio=1.034, hyp_len=24319, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.65.1.38-3.97.1.29-3.63.pth
BLEU = 45.92, 71.6/53.9/39.6/29.1 (BP=1.000, ratio=1.064, hyp_len=25007, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.66.1.43-4.17.1.24-3.45.pth
BLEU = 49.12, 74.1/56.3/42.6/32.7 (BP=1.000, ratio=1.027, hyp_len=24144, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.67.1.32-3.75.1.24-3.46.pth
BLEU = 49.52, 74.6/56.8/43.0/33.0 (BP=1.000, ratio=1.022, hyp_len=24030, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.68.1.33-3.78.1.22-3.40.pth
BLEU = 48.55, 73.6/55.9/42.2/32.1 (BP=1.000, ratio=1.044, hyp_len=24552, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.69.1.37-3.95.1.21-3.36.pth
BLEU = 50.63, 75.4/57.9/44.1/34.1 (BP=1.000, ratio=1.017, hyp_len=23917, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.70.1.27-3.54.1.21-3.36.pth
BLEU = 48.17, 73.0/55.8/41.9/31.6 (BP=1.000, ratio=1.060, hyp_len=24910, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.71.1.35-3.84.1.20-3.31.pth
BLEU = 49.09, 74.1/56.8/42.8/32.3 (BP=1.000, ratio=1.046, hyp_len=24589, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.72.1.27-3.58.1.18-3.24.pth
BLEU = 50.11, 74.5/57.4/43.8/33.7 (BP=1.000, ratio=1.043, hyp_len=24511, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.73.1.37-3.95.1.17-3.22.pth
BLEU = 49.85, 74.0/57.0/43.6/33.6 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.74.1.29-3.63.1.16-3.19.pth
BLEU = 49.84, 74.4/57.2/43.5/33.3 (BP=1.000, ratio=1.046, hyp_len=24591, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.75.1.28-3.60.1.16-3.19.pth
BLEU = 50.16, 74.6/57.6/43.9/33.5 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.76.1.29-3.62.1.16-3.18.pth
BLEU = 52.15, 76.3/59.3/45.8/35.7 (BP=1.000, ratio=1.020, hyp_len=23990, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.77.1.22-3.38.1.18-3.27.pth
BLEU = 48.15, 72.6/55.9/42.1/31.4 (BP=1.000, ratio=1.082, hyp_len=25436, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.78.1.20-3.33.1.13-3.10.pth
BLEU = 51.47, 75.5/58.8/45.3/35.0 (BP=1.000, ratio=1.041, hyp_len=24467, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.79.1.21-3.37.1.12-3.06.pth
BLEU = 52.14, 76.0/59.4/45.8/35.7 (BP=1.000, ratio=1.037, hyp_len=24386, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.80.1.22-3.40.1.12-3.07.pth
BLEU = 50.86, 74.4/58.0/44.7/34.7 (BP=1.000, ratio=1.061, hyp_len=24935, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.81.1.15-3.17.1.11-3.04.pth
BLEU = 51.71, 75.4/59.0/45.6/35.3 (BP=1.000, ratio=1.045, hyp_len=24578, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.82.1.25-3.49.1.10-3.00.pth
BLEU = 52.54, 76.0/59.7/46.3/36.3 (BP=1.000, ratio=1.041, hyp_len=24477, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.83.1.20-3.31.1.13-3.10.pth
BLEU = 49.63, 73.2/57.1/43.6/33.2 (BP=1.000, ratio=1.086, hyp_len=25529, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.84.1.21-3.36.1.08-2.96.pth
BLEU = 52.94, 76.0/60.0/46.8/36.8 (BP=1.000, ratio=1.049, hyp_len=24668, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.85.1.24-3.46.1.08-2.96.pth
BLEU = 54.61, 77.6/61.4/48.4/38.6 (BP=1.000, ratio=1.024, hyp_len=24083, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.86.1.23-3.42.1.09-2.96.pth
BLEU = 53.54, 76.4/60.4/47.4/37.6 (BP=1.000, ratio=1.038, hyp_len=24412, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.87.1.14-3.13.1.07-2.92.pth
BLEU = 53.31, 76.1/60.2/47.2/37.3 (BP=1.000, ratio=1.049, hyp_len=24655, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.88.1.19-3.29.1.06-2.88.pth
BLEU = 53.86, 76.9/60.8/47.7/37.7 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.89.1.19-3.27.1.06-2.89.pth
BLEU = 52.96, 76.1/60.1/46.9/36.7 (BP=1.000, ratio=1.054, hyp_len=24775, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.90.1.17-3.23.1.06-2.89.pth
BLEU = 52.24, 75.5/59.5/46.2/35.9 (BP=1.000, ratio=1.062, hyp_len=24957, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.91.1.14-3.12.1.04-2.83.pth
BLEU = 54.99, 77.6/61.8/48.8/39.1 (BP=1.000, ratio=1.036, hyp_len=24354, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.92.1.15-3.14.1.04-2.82.pth
BLEU = 55.66, 78.2/62.5/49.5/39.7 (BP=1.000, ratio=1.031, hyp_len=24230, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.93.1.13-3.11.1.03-2.81.pth
BLEU = 54.90, 77.1/61.7/48.9/39.1 (BP=1.000, ratio=1.050, hyp_len=24685, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.94.1.04-2.83.1.03-2.80.pth
BLEU = 54.60, 77.3/61.6/48.6/38.4 (BP=1.000, ratio=1.045, hyp_len=24564, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.95.1.12-3.06.1.04-2.82.pth
BLEU = 53.40, 76.4/60.8/47.4/36.9 (BP=1.000, ratio=1.057, hyp_len=24858, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.96.1.15-3.17.1.04-2.82.pth
BLEU = 53.48, 76.6/60.9/47.5/36.9 (BP=1.000, ratio=1.057, hyp_len=24841, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.97.1.06-2.89.1.02-2.76.pth
BLEU = 55.27, 77.5/62.1/49.3/39.4 (BP=1.000, ratio=1.045, hyp_len=24566, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.98.1.06-2.88.1.00-2.73.pth
BLEU = 55.68, 77.8/62.4/49.6/39.9 (BP=1.000, ratio=1.040, hyp_len=24458, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.99.1.08-2.93.1.00-2.72.pth
BLEU = 55.17, 77.4/62.1/49.1/39.2 (BP=1.000, ratio=1.052, hyp_len=24727, ref_len=23509)
/home/ye/exp/simple-nmt

real	59m59.250s
user	58m49.229s
sys	2m9.547s
(simple-nmt) ye@:~/exp/simple-nmt$
```
