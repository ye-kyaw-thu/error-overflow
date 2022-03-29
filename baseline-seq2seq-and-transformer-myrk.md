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
