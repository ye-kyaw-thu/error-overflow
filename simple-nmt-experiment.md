# Simple NMT Installation and Testing

## Create simple-nmt env

```
(base) ye@:~/exp$ conda create -n "simple-nmt" python
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/simple-nmt

  added / updated specs:
    - python


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libuuid-1.0.3              |       h7f8727e_2          17 KB
    pip-21.2.4                 |  py310h06a4308_0         1.8 MB
    python-3.10.0              |       h12debd9_5        23.5 MB
    setuptools-58.0.4          |  py310h06a4308_0         782 KB
    tzdata-2021e               |       hda174b7_0         112 KB
    ------------------------------------------------------------
                                           Total:        26.2 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h7b6447c_0
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.2.1-h06a4308_0
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  libuuid            pkgs/main/linux-64::libuuid-1.0.3-h7f8727e_2
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1m-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.4-py310h06a4308_0
  python             pkgs/main/linux-64::python-3.10.0-h12debd9_5
  readline           pkgs/main/linux-64::readline-8.1.2-h7f8727e_1
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py310h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.37.2-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  tzdata             pkgs/main/noarch::tzdata-2021e-hda174b7_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7f8727e_4


Proceed ([y]/n)? y


Downloading and Extracting Packages
tzdata-2021e         | 112 KB    | ############################################################################################################# | 100% 
libuuid-1.0.3        | 17 KB     | ############################################################################################################# | 100% 
python-3.10.0        | 23.5 MB   | ############################################################################################################# | 100% 
setuptools-58.0.4    | 782 KB    | ############################################################################################################# | 100% 
pip-21.2.4           | 1.8 MB    | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate simple-nmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@:~/exp$ conda activate simple-nmt
(simple-nmt) ye@:~/exp$ 
```

git clone  

```
(simple-nmt) ye@:~/exp$ git clone https://github.com/kh-kim/simple-nmt
Cloning into 'simple-nmt'...
remote: Enumerating objects: 1248, done.
remote: Counting objects: 100% (201/201), done.
remote: Compressing objects: 100% (124/124), done.
remote: Total 1248 (delta 118), reused 147 (delta 77), pack-reused 1047
Receiving objects: 100% (1248/1248), 440.13 KiB | 3.44 MiB/s, done.
Resolving deltas: 100% (847/847), done.
(simple-nmt) ye@:~/exp$ cd simple-nmt/
(simple-nmt) ye@:~/exp/simple-nmt$
```

torch installation လုပ်ကြည့်တော့ version မရှိဘူးလို့ပြော...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install torch
ERROR: Could not find a version that satisfies the requirement torch (from versions: none)
ERROR: No matching distribution found for torch
(simple-nmt) ye@:~/exp/simple-nmt$ python 
Python 3.10.0 (default, Mar  3 2022, 09:58:08) [GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
(simple-nmt) ye@:~/exp/simple-nmt$ pip install torch==1.6
ERROR: Could not find a version that satisfies the requirement torch==1.6 (from versions: none)
ERROR: No matching distribution found for torch==1.6
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

python version ကို downgrade လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ conda install python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/simple-nmt

  added / updated specs:
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    pip-21.2.2                 |   py36h06a4308_0         1.8 MB
    setuptools-58.0.4          |   py36h06a4308_0         788 KB
    ------------------------------------------------------------
                                           Total:         2.6 MB

The following packages will be DOWNGRADED:

  pip                                21.2.4-py310h06a4308_0 --> 21.2.2-py36h06a4308_0
  python                                  3.10.0-h12debd9_5 --> 3.6.13-h12debd9_1
  setuptools                         58.0.4-py310h06a4308_0 --> 58.0.4-py36h06a4308_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
pip-21.2.2           | 1.8 MB    | ############################################################################################################# | 100% 
setuptools-58.0.4    | 788 KB    | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

torch ကို install လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install torch
Collecting torch
  Downloading torch-1.10.2-cp36-cp36m-manylinux1_x86_64.whl (881.9 MB)
     |████████████████████████████████| 881.9 MB 36 kB/s 
Collecting typing-extensions
  Using cached typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting dataclasses
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Installing collected packages: typing-extensions, dataclasses, torch
Successfully installed dataclasses-0.8 torch-1.10.2 typing-extensions-4.1.1
(simple-nmt) ye@:~/exp/simple-nmt$
```

install torchtext ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install torchtext
Collecting torchtext
  Downloading torchtext-0.11.2-cp36-cp36m-manylinux1_x86_64.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 1.7 MB/s 
Collecting tqdm
  Using cached tqdm-4.63.0-py2.py3-none-any.whl (76 kB)
Requirement already satisfied: torch==1.10.2 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torchtext) (1.10.2)
Collecting numpy
  Using cached numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
Collecting requests
  Using cached requests-2.27.1-py2.py3-none-any.whl (63 kB)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch==1.10.2->torchtext) (0.8)
Requirement already satisfied: typing-extensions in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch==1.10.2->torchtext) (4.1.1)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from requests->torchtext) (2020.6.20)
Collecting urllib3<1.27,>=1.21.1
  Using cached urllib3-1.26.8-py2.py3-none-any.whl (138 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.3-py3-none-any.whl (61 kB)
Collecting charset-normalizer~=2.0.0
  Using cached charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Collecting importlib-resources
  Downloading importlib_resources-5.4.0-py3-none-any.whl (28 kB)
Collecting zipp>=3.1.0
  Using cached zipp-3.6.0-py3-none-any.whl (5.3 kB)
Installing collected packages: zipp, urllib3, importlib-resources, idna, charset-normalizer, tqdm, requests, numpy, torchtext
Successfully installed charset-normalizer-2.0.12 idna-3.3 importlib-resources-5.4.0 numpy-1.19.5 requests-2.27.1 torchtext-0.11.2 tqdm-4.63.0 urllib3-1.26.8 zipp-3.6.0
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

torch-optimizer ကို install လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install torch-optimizer
Collecting torch-optimizer
  Downloading torch_optimizer-0.3.0-py3-none-any.whl (61 kB)
     |████████████████████████████████| 61 kB 420 kB/s 
Collecting pytorch-ranger>=0.1.1
  Downloading pytorch_ranger-0.1.1-py3-none-any.whl (14 kB)
Requirement already satisfied: torch>=1.5.0 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch-optimizer) (1.10.2)
Requirement already satisfied: typing-extensions in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch>=1.5.0->torch-optimizer) (4.1.1)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch>=1.5.0->torch-optimizer) (0.8)
Installing collected packages: pytorch-ranger, torch-optimizer
Successfully installed pytorch-ranger-0.1.1 torch-optimizer-0.3.0
(simple-nmt) ye@:~/exp/simple-nmt$
```

pytorch-ignite ကို install လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install pytorch-ignite
Collecting pytorch-ignite
  Downloading pytorch_ignite-0.4.8-py3-none-any.whl (251 kB)
     |████████████████████████████████| 251 kB 1.8 MB/s 
Requirement already satisfied: torch<2,>=1.3 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from pytorch-ignite) (1.10.2)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch<2,>=1.3->pytorch-ignite) (0.8)
Requirement already satisfied: typing-extensions in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch<2,>=1.3->pytorch-ignite) (4.1.1)
Installing collected packages: pytorch-ignite
Successfully installed pytorch-ignite-0.4.8
(simple-nmt) ye@:~/exp/simple-nmt$
```

train.py ကို help ခေါ်ကြည့်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python ./train.py -h
Traceback (most recent call last):
  File "./train.py", line 18, in <module>
    from simple_nmt.rl_trainer import MinimumRiskTrainingEngine
  File "/home/ye/exp/simple-nmt/simple_nmt/rl_trainer.py", line 1, in <module>
    from nltk.translate.gleu_score import sentence_gleu
ModuleNotFoundError: No module named 'nltk'
(simple-nmt) ye@:~/exp/simple-nmt$
```

nltk လိုတယ် ဆိုတော့ install လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ pip install nltk
Collecting nltk
  Downloading nltk-3.6.7-py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 1.7 MB/s 
Requirement already satisfied: tqdm in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from nltk) (4.63.0)
Collecting click
  Using cached click-8.0.4-py3-none-any.whl (97 kB)
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting regex>=2021.8.3
  Downloading regex-2022.3.2-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (749 kB)
     |████████████████████████████████| 749 kB 132.3 MB/s 
Collecting importlib-metadata
  Downloading importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from importlib-metadata->click->nltk) (3.6.0)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from importlib-metadata->click->nltk) (4.1.1)
Requirement already satisfied: importlib-resources in /home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from tqdm->nltk) (5.4.0)
Installing collected packages: importlib-metadata, regex, joblib, click, nltk
Successfully installed click-8.0.4 importlib-metadata-4.8.3 joblib-1.1.0 nltk-3.6.7 regex-2022.3.2
(simple-nmt) ye@:~/exp/simple-nmt$
```

train.py ကို help ခေါ်ကြည့်တော့ ဒီတစ်ခါတော့ ရသွားပြီ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python ./train.py -h
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

optional arguments:
  -h, --help            show this help message and exit
  --model_fn MODEL_FN   Model file name to save. Additional information would
                        be annotated to the file name.
  --train TRAIN         Training set file name except the extention. (ex:
                        train.en --> train)
  --valid VALID         Validation set file name except the extention. (ex:
                        valid.en --> valid)
  --lang LANG           Set of extention represents language pair. (ex: en +
                        ko --> enko)
  --gpu_id GPU_ID       GPU ID to train. Currently, GPU parallel is not
                        supported. -1 for CPU. Default=-1
  --off_autocast        Turn-off Automatic Mixed Precision (AMP), which speed-
                        up training.
  --batch_size BATCH_SIZE
                        Mini batch size for gradient descent. Default=32
  --n_epochs N_EPOCHS   Number of epochs to train. Default=20
  --verbose VERBOSE     VERBOSE_SILENT, VERBOSE_EPOCH_WISE, VERBOSE_BATCH_WISE
                        = 0, 1, 2. Default=2
  --init_epoch INIT_EPOCH
                        Set initial epoch number, which can be useful in
                        continue training. Default=1
  --max_length MAX_LENGTH
                        Maximum length of the training sequence. Default=100
  --dropout DROPOUT     Dropout rate. Default=0.2
  --word_vec_size WORD_VEC_SIZE
                        Word embedding vector dimension. Default=512
  --hidden_size HIDDEN_SIZE
                        Hidden size of LSTM. Default=768
  --n_layers N_LAYERS   Number of layers in LSTM. Default=4
  --max_grad_norm MAX_GRAD_NORM
                        Threshold for gradient clipping. Default=5.0
  --iteration_per_update ITERATION_PER_UPDATE
                        Number of feed-forward iterations for one parameter
                        update. Default=1
  --lr LR               Initial learning rate. Default=1.0
  --lr_step LR_STEP     Number of epochs for each learning rate decay.
                        Default=1
  --lr_gamma LR_GAMMA   Learning rate decay rate. Default=0.5
  --lr_decay_start LR_DECAY_START
                        Learning rate decay start at. Default=10
  --use_adam            Use Adam as optimizer instead of SGD. Other lr
                        arguments should be changed.
  --use_radam           Use rectified Adam as optimizer. Other lr arguments
                        should be changed.
  --rl_lr RL_LR         Learning rate for reinforcement learning. Default=0.01
  --rl_n_samples RL_N_SAMPLES
                        Number of samples to get baseline. Default=1
  --rl_n_epochs RL_N_EPOCHS
                        Number of epochs for reinforcement learning.
                        Default=10
  --rl_n_gram RL_N_GRAM
                        Maximum number of tokens to calculate BLEU for
                        reinforcement learning. Default=6
  --rl_reward RL_REWARD
                        Method name to use as reward function for RL training.
                        Default=gleu
  --use_transformer     Set model architecture as Transformer.
  --n_splits N_SPLITS   Number of heads in multi-head attention in
                        Transformer. Default=8
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Build Seq-to-Seq Model

Example seq-to-seq run လုပ်ထားတဲ့ parameter တွေကို ကြည့်...  

```
Seq2Seq
>> python train.py --train ./data/corpus.shuf.train.tok.bpe --valid ./data/corpus.shuf.valid.tok.bpe --lang enko \
--gpu_id 0 --batch_size 128 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 512 --hidden_size 768 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
--lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 \
--model_fn ./model.pth
```

အထက်ပါ example ကို မြန်မာ-ရခိုင် seq-to-seq မော်ဒယ် ဆောက်ဖို့ ပြင်ဆင်ခဲ့...  
/media/ye/project2/exp/myrk-transformer/data/syl/train

```
time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
--valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 2 --max_grad_norm 1e+8 --iteration_per_update 2 \
--lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 \
--model_fn ./seq-model-myrk.pth
```

training လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 2 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./seq-model-myrk.pth
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
    'model_fn': './seq-model-myrk.pth',
    'n_epochs': 30,
    'n_layers': 2,
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
    (rnn): LSTM(128, 64, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=2, batch_first=True, dropout=0.2)
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
Epoch 1 - |param|=6.50e+02 |g_param|=1.82e+05 loss=4.2639e+00 ppl=71.09                                                 
Validation - loss=3.5788e+00 ppl=35.83 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.50e+02 |g_param|=1.62e+05 loss=3.8877e+00 ppl=48.80                                                 
Validation - loss=3.1852e+00 ppl=24.17 best_loss=3.5788e+00 best_ppl=35.83                                              
Epoch 3 - |param|=6.50e+02 |g_param|=1.76e+05 loss=3.5673e+00 ppl=35.42                                                 
Validation - loss=2.8637e+00 ppl=17.53 best_loss=3.1852e+00 best_ppl=24.17                                              
Epoch 4 - |param|=6.50e+02 |g_param|=1.52e+05 loss=3.2173e+00 ppl=24.96                                                 
Validation - loss=2.5414e+00 ppl=12.70 best_loss=2.8637e+00 best_ppl=17.53                                              
Epoch 5 - |param|=6.51e+02 |g_param|=1.58e+05 loss=2.8860e+00 ppl=17.92                                                 
Validation - loss=2.2750e+00 ppl=9.73 best_loss=2.5414e+00 best_ppl=12.70                                               
Epoch 6 - |param|=6.51e+02 |g_param|=1.91e+05 loss=2.7217e+00 ppl=15.21                                                 
Validation - loss=2.1000e+00 ppl=8.17 best_loss=2.2750e+00 best_ppl=9.73                                                
Epoch 7 - |param|=6.52e+02 |g_param|=1.65e+05 loss=2.4757e+00 ppl=11.89                                                 
Validation - loss=1.9377e+00 ppl=6.94 best_loss=2.1000e+00 best_ppl=8.17                                                
Epoch 8 - |param|=6.52e+02 |g_param|=1.78e+05 loss=2.3365e+00 ppl=10.35                                                 
Validation - loss=1.7930e+00 ppl=6.01 best_loss=1.9377e+00 best_ppl=6.94                                                
Epoch 9 - |param|=6.53e+02 |g_param|=1.19e+05 loss=2.1572e+00 ppl=8.65                                                  
Validation - loss=1.6542e+00 ppl=5.23 best_loss=1.7930e+00 best_ppl=6.01                                                
Epoch 10 - |param|=6.54e+02 |g_param|=1.01e+05 loss=2.0474e+00 ppl=7.75                                                 
Validation - loss=1.5456e+00 ppl=4.69 best_loss=1.6542e+00 best_ppl=5.23                                                
Epoch 11 - |param|=6.54e+02 |g_param|=1.13e+05 loss=1.9181e+00 ppl=6.81                                                 
Validation - loss=1.4686e+00 ppl=4.34 best_loss=1.5456e+00 best_ppl=4.69                                                
Epoch 12 - |param|=6.55e+02 |g_param|=9.80e+04 loss=1.7987e+00 ppl=6.04                                                 
Validation - loss=1.3577e+00 ppl=3.89 best_loss=1.4686e+00 best_ppl=4.34                                                
Epoch 13 - |param|=6.56e+02 |g_param|=1.04e+05 loss=1.6846e+00 ppl=5.39                                                 
Validation - loss=1.2915e+00 ppl=3.64 best_loss=1.3577e+00 best_ppl=3.89                                                
Epoch 14 - |param|=6.56e+02 |g_param|=1.10e+05 loss=1.6177e+00 ppl=5.04                                                 
Validation - loss=1.2062e+00 ppl=3.34 best_loss=1.2915e+00 best_ppl=3.64                                                
Epoch 15 - |param|=6.57e+02 |g_param|=1.29e+05 loss=1.3942e+00 ppl=4.03                                                 
Validation - loss=1.0327e+00 ppl=2.81 best_loss=1.2062e+00 best_ppl=3.34                                                
Epoch 16 - |param|=6.58e+02 |g_param|=1.28e+05 loss=1.1288e+00 ppl=3.09                                                 
Validation - loss=8.3761e-01 ppl=2.31 best_loss=1.0327e+00 best_ppl=2.81                                                
Epoch 17 - |param|=6.58e+02 |g_param|=1.34e+05 loss=9.2505e-01 ppl=2.52                                                 
Validation - loss=7.0560e-01 ppl=2.03 best_loss=8.3761e-01 best_ppl=2.31                                                
Epoch 18 - |param|=6.59e+02 |g_param|=1.56e+05 loss=7.9394e-01 ppl=2.21                                                 
Validation - loss=6.3538e-01 ppl=1.89 best_loss=7.0560e-01 best_ppl=2.03                                                
Epoch 19 - |param|=6.60e+02 |g_param|=1.41e+05 loss=6.4723e-01 ppl=1.91                                                 
Validation - loss=5.4626e-01 ppl=1.73 best_loss=6.3538e-01 best_ppl=1.89                                                
Epoch 20 - |param|=6.60e+02 |g_param|=1.03e+05 loss=5.4098e-01 ppl=1.72                                                 
Validation - loss=4.7126e-01 ppl=1.60 best_loss=5.4626e-01 best_ppl=1.73                                                
Epoch 21 - |param|=6.61e+02 |g_param|=1.30e+05 loss=5.4147e-01 ppl=1.72                                                 
Validation - loss=4.3915e-01 ppl=1.55 best_loss=4.7126e-01 best_ppl=1.60                                                
Epoch 22 - |param|=6.61e+02 |g_param|=9.72e+04 loss=4.6911e-01 ppl=1.60                                                 
Validation - loss=4.1326e-01 ppl=1.51 best_loss=4.3915e-01 best_ppl=1.55                                                
Epoch 23 - |param|=6.62e+02 |g_param|=7.32e+04 loss=4.4277e-01 ppl=1.56                                                 
Validation - loss=4.0132e-01 ppl=1.49 best_loss=4.1326e-01 best_ppl=1.51                                                
Epoch 24 - |param|=6.62e+02 |g_param|=4.01e+04 loss=3.9341e-01 ppl=1.48                                                 
Validation - loss=3.9795e-01 ppl=1.49 best_loss=4.0132e-01 best_ppl=1.49                                                
Epoch 25 - |param|=6.63e+02 |g_param|=4.93e+04 loss=3.8890e-01 ppl=1.48                                                 
Validation - loss=3.7694e-01 ppl=1.46 best_loss=3.9795e-01 best_ppl=1.49                                                
Epoch 26 - |param|=6.63e+02 |g_param|=5.46e+04 loss=3.7545e-01 ppl=1.46                                                 
Validation - loss=3.8197e-01 ppl=1.47 best_loss=3.7694e-01 best_ppl=1.46                                                
Epoch 27 - |param|=6.64e+02 |g_param|=4.91e+04 loss=3.5795e-01 ppl=1.43                                                 
Validation - loss=3.6208e-01 ppl=1.44 best_loss=3.7694e-01 best_ppl=1.46                                                
Epoch 28 - |param|=6.64e+02 |g_param|=3.52e+04 loss=3.2533e-01 ppl=1.38                                                 
Validation - loss=3.4723e-01 ppl=1.42 best_loss=3.6208e-01 best_ppl=1.44                                                
Epoch 29 - |param|=6.65e+02 |g_param|=3.79e+04 loss=3.1122e-01 ppl=1.37                                                 
Validation - loss=3.5664e-01 ppl=1.43 best_loss=3.4723e-01 best_ppl=1.42                                                
Epoch 30 - |param|=6.65e+02 |g_param|=4.28e+04 loss=2.9530e-01 ppl=1.34                                                 
Validation - loss=3.4211e-01 ppl=1.41 best_loss=3.4723e-01 best_ppl=1.42                                                

real	4m19.527s
user	4m16.007s
sys	0m4.003s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

Running time ကတော့ အရမ်းမြန်တယ်...  
လေးမိနစ်ပဲ ကြာတယ် Amazing!!!

မော်ဒယ်ကို folder path မပေးခဲ့တော့ run တဲ့ ဖိုလ်ဒါအောက်မှာပဲ သိမ်းပေးလို့ ဖိုလ်ဒါ သတ်သတ်မှတ်မှတ် ဆောက်ပြီး သိမ်းခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ mv *.pth ./model/seq2seq/
(simple-nmt) ye@:~/exp/simple-nmt$ ls ./model/seq2seq/
seq-model-myrk.01.4.26-71.09.3.58-35.83.pth  seq-model-myrk.11.1.92-6.81.1.47-4.34.pth  seq-model-myrk.21.0.54-1.72.0.44-1.55.pth
seq-model-myrk.02.3.89-48.80.3.19-24.17.pth  seq-model-myrk.12.1.80-6.04.1.36-3.89.pth  seq-model-myrk.22.0.47-1.60.0.41-1.51.pth
seq-model-myrk.03.3.57-35.42.2.86-17.53.pth  seq-model-myrk.13.1.68-5.39.1.29-3.64.pth  seq-model-myrk.23.0.44-1.56.0.40-1.49.pth
seq-model-myrk.04.3.22-24.96.2.54-12.70.pth  seq-model-myrk.14.1.62-5.04.1.21-3.34.pth  seq-model-myrk.24.0.39-1.48.0.40-1.49.pth
seq-model-myrk.05.2.89-17.92.2.27-9.73.pth   seq-model-myrk.15.1.39-4.03.1.03-2.81.pth  seq-model-myrk.25.0.39-1.48.0.38-1.46.pth
seq-model-myrk.06.2.72-15.21.2.10-8.17.pth   seq-model-myrk.16.1.13-3.09.0.84-2.31.pth  seq-model-myrk.26.0.38-1.46.0.38-1.47.pth
seq-model-myrk.07.2.48-11.89.1.94-6.94.pth   seq-model-myrk.17.0.93-2.52.0.71-2.03.pth  seq-model-myrk.27.0.36-1.43.0.36-1.44.pth
seq-model-myrk.08.2.34-10.35.1.79-6.01.pth   seq-model-myrk.18.0.79-2.21.0.64-1.89.pth  seq-model-myrk.28.0.33-1.38.0.35-1.42.pth
seq-model-myrk.09.2.16-8.65.1.65-5.23.pth    seq-model-myrk.19.0.65-1.91.0.55-1.73.pth  seq-model-myrk.29.0.31-1.37.0.36-1.43.pth
seq-model-myrk.10.2.05-7.75.1.55-4.69.pth    seq-model-myrk.20.0.54-1.72.0.47-1.60.pth  seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Translation of Seq2-to-Seq Model (for Myanmar-Rakhine)

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp

real	0m19.170s
user	0m18.703s
sys	0m1.105s
```

file size ကို စစ်ဆေးခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ wc ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp 
  1811  23887 221558 ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp
```

hypothesis ဖိုင်ကို head လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ head ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp 
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ဝံ့ ပါ လား ။
ကျွန် တော် သာ ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရေ ရီ ကို သောက် သ င့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ ဂ ယော င့် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ကျွန် တော် ဘတ်စ် ကား အ တွက် အ ကြွီ အ ချို့ လို ချင် လို့ ပါ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ ယင်း သူ ရို့ ဇာ တိ လုပ် နီ စွာ လေး ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
```

hyp ဖိုင်ကို tail လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ tail ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp
ယင်း ပြ ဿ နာ ကို မ စစ် ဆေး ခ ပါ လား ။
မင်း သူ ငယ် ချင်း တိ ဇာ အ ချိန် လာ ကတ် ဖို့ လေး ။
မင်း တစ် ရက် နှစ် ရက် အ လုပ် မ ဆင်း ပါ ကေ အ နား ယူ သ င့် ရေ ။
အို အ ရာ ပါ ရေ ၊ မင်း ရော ။
မင်း စာ ကို ထ ည့် ခ စွာ ငါ မှတ် မိ ပါ ရေ ။
မင်း အ တွက် အ ဂ ယော င့် နွီး ထွေး ရေ မွီး နိ ဖြစ် ဖို့ ဆု တောင်း ပီး ပါ ရေ ။
ခင် ဗျား ဇာ လုပ် ဖို့ လေး ။
အ ဂု ကျွန် တော့် အ ဘောင် တ ရား ထိုင် နီ စွာ ကြော င့် အ ချေ တိ တိတ် တိတ် နီ စီ ချင် ရေ ။
ထို မ ချေ ယင်း ချင့် ကို သ ဘော တူ ပါ လား ။
အ ခြေ အ နေ က လုံး ဝ ထိန်း မ နိုင် သိမ်း မ ရ ဖြစ် နီ ဗျာယ် ။
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Evaluation on Seq-to-Seq (Myanmar-Rakhine)

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk 
BLEU = 73.13, 87.0/77.3/68.9/61.7 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

မော်ဒယ်ကို ဆောက်တာက တကယ် မြန်တယ်။ evaluation လုပ်ကြည့်တော့လည်း ရလဒ်က မဆိုးဘူး။  
လက်ရှိထက် ပိုကောင်းအောင် parameter tuning လုပ်ဖို့တော့ လိုအပ်လိမ့်မယ်။  

## Training Continue with Reinforcement Learning for Seq-to-Seq (Myanmar-Rakhine)

continue_train.py ရဲ့ help ခေါ်ကြည့်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python continue_train.py -h
usage: continue_train.py [-h] --load_fn LOAD_FN [--model_fn MODEL_FN]
                         [--train TRAIN] [--valid VALID] [--lang LANG]
                         [--gpu_id GPU_ID] [--off_autocast]
                         [--batch_size BATCH_SIZE] [--n_epochs N_EPOCHS]
                         [--verbose VERBOSE] --init_epoch INIT_EPOCH
                         [--max_length MAX_LENGTH] [--dropout DROPOUT]
                         [--word_vec_size WORD_VEC_SIZE]
                         [--hidden_size HIDDEN_SIZE] [--n_layers N_LAYERS]
                         [--max_grad_norm MAX_GRAD_NORM]
                         [--iteration_per_update ITERATION_PER_UPDATE]
                         [--lr LR] [--lr_step LR_STEP] [--lr_gamma LR_GAMMA]
                         [--lr_decay_start LR_DECAY_START] [--use_adam]
                         [--use_radam] [--rl_lr RL_LR]
                         [--rl_n_samples RL_N_SAMPLES]
                         [--rl_n_epochs RL_N_EPOCHS] [--rl_n_gram RL_N_GRAM]
                         [--rl_reward RL_REWARD] [--use_transformer]
                         [--n_splits N_SPLITS]

optional arguments:
  -h, --help            show this help message and exit
  --load_fn LOAD_FN     Model file name to continue.
  --model_fn MODEL_FN   Model file name to save. Additional information would
                        be annotated to the file name.
  --train TRAIN         Training set file name except the extention. (ex:
                        train.en --> train)
  --valid VALID         Validation set file name except the extention. (ex:
                        valid.en --> valid)
  --lang LANG           Set of extention represents language pair. (ex: en +
                        ko --> enko)
  --gpu_id GPU_ID       GPU ID to train. Currently, GPU parallel is not
                        supported. -1 for CPU. Default=-1
  --off_autocast        Turn-off Automatic Mixed Precision (AMP), which speed-
                        up training.
  --batch_size BATCH_SIZE
                        Mini batch size for gradient descent. Default=32
  --n_epochs N_EPOCHS   Number of epochs to train. Default=20
  --verbose VERBOSE     VERBOSE_SILENT, VERBOSE_EPOCH_WISE, VERBOSE_BATCH_WISE
                        = 0, 1, 2. Default=2
  --init_epoch INIT_EPOCH
                        Set initial epoch number, which can be useful in
                        continue training. Default=1
  --max_length MAX_LENGTH
                        Maximum length of the training sequence. Default=100
  --dropout DROPOUT     Dropout rate. Default=0.2
  --word_vec_size WORD_VEC_SIZE
                        Word embedding vector dimension. Default=512
  --hidden_size HIDDEN_SIZE
                        Hidden size of LSTM. Default=768
  --n_layers N_LAYERS   Number of layers in LSTM. Default=4
  --max_grad_norm MAX_GRAD_NORM
                        Threshold for gradient clipping. Default=5.0
  --iteration_per_update ITERATION_PER_UPDATE
                        Number of feed-forward iterations for one parameter
                        update. Default=1
  --lr LR               Initial learning rate. Default=1.0
  --lr_step LR_STEP     Number of epochs for each learning rate decay.
                        Default=1
  --lr_gamma LR_GAMMA   Learning rate decay rate. Default=0.5
  --lr_decay_start LR_DECAY_START
                        Learning rate decay start at. Default=10
  --use_adam            Use Adam as optimizer instead of SGD. Other lr
                        arguments should be changed.
  --use_radam           Use rectified Adam as optimizer. Other lr arguments
                        should be changed.
  --rl_lr RL_LR         Learning rate for reinforcement learning. Default=0.01
  --rl_n_samples RL_N_SAMPLES
                        Number of samples to get baseline. Default=1
  --rl_n_epochs RL_N_EPOCHS
                        Number of epochs for reinforcement learning.
                        Default=10
  --rl_n_gram RL_N_GRAM
                        Maximum number of tokens to calculate BLEU for
                        reinforcement learning. Default=6
  --rl_reward RL_REWARD
                        Method name to use as reward function for RL training.
                        Default=gleu
  --use_transformer     Set model architecture as Transformer.
  --n_splits N_SPLITS   Number of heads in multi-head attention in
                        Transformer. Default=8
(simple-nmt) ye@:~/exp/simple-nmt$
```

```
time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth \
--model_fn ./model/rl/seq-rl-model-myrk.pth \
--init_epoch 31 --iteration_per_update 1 --max_grad_norm 5
```

RL model ကို သိမ်းဖို့အတွက် folder အသစ် ဝင်ဆောက်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model$ mkdir rl
```

Start RL training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 31 --iteration_per_update 1 --max_grad_norm 5 --gpu_id 0
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 31
WARNING!!! You changed value for argument "--max_grad_norm".	Use current value: 5.0
WARNING!!! You changed value for argument "--iteration_per_update".	Use current value: 1
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 31,
    'iteration_per_update': 1,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 5.0,
    'max_length': 100,
    'model_fn': './model/rl/seq-rl-model-myrk.pth',
    'n_epochs': 30,
    'n_layers': 2,
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
    (rnn): LSTM(128, 64, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=2, batch_first=True, dropout=0.2)
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

real	0m2.603s
user	0m2.100s
sys	0m1.113s
```

output model ထွက်သလား ကြည့်ခဲ့... ဘာမှ မတွေ့ရ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ls ./model/rl/
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

အလုပ် မလုပ်ဘူး...  
init_epoch ကို 30 ထားကြည့်မှ အလုပ်လုပ်သွား...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 1
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
WARNING!!! You changed value for argument "--iteration_per_update".	Use current value: 1
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 1,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq-rl-model-myrk.pth',
    'n_epochs': 30,
    'n_layers': 2,
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
    (rnn): LSTM(128, 64, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=2, batch_first=True, dropout=0.2)
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
Epoch 30 - |param|=6.66e+02 |g_param|=1.10e+05 loss=3.1562e-01 ppl=1.37                                                 
Validation - loss=3.4929e-01 ppl=1.42 best_loss=inf best_ppl=inf                                                        

real	0m11.588s
user	0m11.024s
sys	0m1.220s
(simple-nmt) ye@:~/exp/simple-nmt$ ls ./model/rl/
seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth
```

testing with RL model ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./model/rl/seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./model/rl/seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp

real	0m19.188s
user	0m18.679s
sys	0m1.147s
(simple-nmt) ye@:~/exp/simple-nmt$ ls ./model/rl/
seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth  seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp
(simple-nmt) ye@:~/exp/simple-nmt$ head ./model/rl/seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp 
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် သာ ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရေ ရေ ရီ ကို သောက် သ င့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ ဂ ယော င့် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ကျွန် တော် ဘတ်စ် ကား အ တွက် အ ကြွီ အ ချို့ လို ချင် လို့ ပါ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ လေး ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
(simple-nmt) ye@:~/exp/simple-nmt$
```

RL model ကို evaluation လုပ်ကြည့်ခဲ့...  

```
cat ./model/rl/seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
```

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 72.46, 86.4/76.6/68.3/61.0 (BP=1.000, ratio=1.036, hyp_len=23994, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

အလုပ်တော့ လုပ်သွားပြီ သို့သော် ရလဒ် က မကောင်း...  

ဒီတစ်ခါတော့ --max_grad_norm ကို 5 ထားပြီး RL training လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 1 --max_grad_norm 5
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
WARNING!!! You changed value for argument "--max_grad_norm".	Use current value: 5.0
WARNING!!! You changed value for argument "--iteration_per_update".	Use current value: 1
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 1,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 5.0,
    'max_length': 100,
    'model_fn': './model/rl/seq-rl-model-myrk.pth',
    'n_epochs': 30,
    'n_layers': 2,
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
    (rnn): LSTM(128, 64, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=2, batch_first=True, dropout=0.2)
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
Epoch 30 - |param|=6.65e+02 |g_param|=9.31e+04 loss=3.8520e-01 ppl=1.47                                                 
Validation - loss=3.7753e-01 ppl=1.46 best_loss=inf best_ppl=inf                                                        

real	0m11.503s
user	0m10.936s
sys	0m1.210s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./model/rl/seq-rl-model-myrk.30.0.39-1.47.0.38-1.46.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./model/rl/seq-rl-model-myrk.30.0.39-1.47.0.38-1.46.pth.hyp

real	0m19.267s
user	0m18.767s
sys	0m1.116s
(simple-nmt) ye@:~/exp/simple-nmt$
```

evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.30.0.39-1.47.0.38-1.46.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 69.01, 85.0/73.9/64.4/56.0 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

BLEU score က ပိုတောင် လျော့သွားတယ်...  

iteration ကို ဒီထက် ပိုတင်လို့ မရဘူးလား?!  
--n_epochs option ကို သုံးကြည့်ချင်တယ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 60
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 60
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
WARNING!!! You changed value for argument "--max_grad_norm".	Use current value: 5.0
WARNING!!! You changed value for argument "--iteration_per_update".	Use current value: 1
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 1,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 5.0,
    'max_length': 100,
    'model_fn': './model/rl/seq-rl-model-myrk.pth',
    'n_epochs': 60,
    'n_layers': 2,
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
    (rnn): LSTM(128, 64, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=2, batch_first=True, dropout=0.2)
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
Epoch 30 - |param|=6.65e+02 |g_param|=7.66e+04 loss=3.7007e-01 ppl=1.45                                                 
Validation - loss=3.7746e-01 ppl=1.46 best_loss=inf best_ppl=inf                                                        
Epoch 31 - |param|=6.65e+02 |g_param|=6.82e+04 loss=3.9482e-01 ppl=1.48                                                 
Validation - loss=3.7614e-01 ppl=1.46 best_loss=3.7746e-01 best_ppl=1.46                                                
Epoch 32 - |param|=6.65e+02 |g_param|=6.43e+04 loss=3.8250e-01 ppl=1.47                                                 
Validation - loss=3.7474e-01 ppl=1.45 best_loss=3.7614e-01 best_ppl=1.46                                                
Epoch 33 - |param|=6.65e+02 |g_param|=6.47e+04 loss=3.7074e-01 ppl=1.45                                                 
Validation - loss=3.7332e-01 ppl=1.45 best_loss=3.7474e-01 best_ppl=1.45                                                
Epoch 34 - |param|=6.65e+02 |g_param|=6.06e+04 loss=3.6816e-01 ppl=1.45                                                 
Validation - loss=3.7182e-01 ppl=1.45 best_loss=3.7332e-01 best_ppl=1.45                                                
Epoch 35 - |param|=6.65e+02 |g_param|=6.22e+04 loss=3.6952e-01 ppl=1.45                                                 
Validation - loss=3.7009e-01 ppl=1.45 best_loss=3.7182e-01 best_ppl=1.45                                                
Epoch 36 - |param|=6.65e+02 |g_param|=6.46e+04 loss=3.7452e-01 ppl=1.45                                                 
Validation - loss=3.6841e-01 ppl=1.45 best_loss=3.7009e-01 best_ppl=1.45                                                
Epoch 37 - |param|=6.65e+02 |g_param|=5.51e+04 loss=3.5929e-01 ppl=1.43                                                 
Validation - loss=3.6662e-01 ppl=1.44 best_loss=3.6841e-01 best_ppl=1.45                                                
Epoch 38 - |param|=6.65e+02 |g_param|=6.18e+04 loss=3.6008e-01 ppl=1.43                                                 
Validation - loss=3.6469e-01 ppl=1.44 best_loss=3.6662e-01 best_ppl=1.44                                                
Epoch 39 - |param|=6.65e+02 |g_param|=7.46e+04 loss=3.6643e-01 ppl=1.44                                                 
Validation - loss=3.6362e-01 ppl=1.44 best_loss=3.6469e-01 best_ppl=1.44                                                
Epoch 40 - |param|=6.65e+02 |g_param|=3.90e+04 loss=3.5772e-01 ppl=1.43                                                 
Validation - loss=3.6157e-01 ppl=1.44 best_loss=3.6362e-01 best_ppl=1.44                                                
Epoch 41 - |param|=6.65e+02 |g_param|=2.80e+04 loss=3.4771e-01 ppl=1.42                                                 
Validation - loss=3.5785e-01 ppl=1.43 best_loss=3.6157e-01 best_ppl=1.44                                                
Epoch 42 - |param|=6.65e+02 |g_param|=2.73e+04 loss=3.4037e-01 ppl=1.41                                                 
Validation - loss=3.5469e-01 ppl=1.43 best_loss=3.5785e-01 best_ppl=1.43                                                
Epoch 43 - |param|=6.65e+02 |g_param|=2.36e+04 loss=3.1648e-01 ppl=1.37                                                 
Validation - loss=3.5181e-01 ppl=1.42 best_loss=3.5469e-01 best_ppl=1.43                                                
Epoch 44 - |param|=6.65e+02 |g_param|=2.34e+04 loss=3.2827e-01 ppl=1.39                                                 
Validation - loss=3.4945e-01 ppl=1.42 best_loss=3.5181e-01 best_ppl=1.42                                                
Epoch 45 - |param|=6.65e+02 |g_param|=2.21e+04 loss=3.1812e-01 ppl=1.37                                                 
Validation - loss=3.4743e-01 ppl=1.42 best_loss=3.4945e-01 best_ppl=1.42                                                
Epoch 46 - |param|=6.65e+02 |g_param|=1.94e+04 loss=3.1174e-01 ppl=1.37                                                 
Validation - loss=3.4544e-01 ppl=1.41 best_loss=3.4743e-01 best_ppl=1.42                                                
Epoch 47 - |param|=6.65e+02 |g_param|=2.50e+04 loss=3.2432e-01 ppl=1.38                                                 
Validation - loss=3.4390e-01 ppl=1.41 best_loss=3.4544e-01 best_ppl=1.41                                                
Epoch 48 - |param|=6.65e+02 |g_param|=1.84e+04 loss=2.8822e-01 ppl=1.33                                                 
Validation - loss=3.4276e-01 ppl=1.41 best_loss=3.4390e-01 best_ppl=1.41                                                
Epoch 49 - |param|=6.65e+02 |g_param|=3.61e+04 loss=2.9209e-01 ppl=1.34                                                 
Validation - loss=3.4206e-01 ppl=1.41 best_loss=3.4276e-01 best_ppl=1.41                                                
Epoch 50 - |param|=6.65e+02 |g_param|=3.60e+04 loss=2.9081e-01 ppl=1.34                                                 
Validation - loss=3.4134e-01 ppl=1.41 best_loss=3.4206e-01 best_ppl=1.41                                                
Epoch 51 - |param|=6.65e+02 |g_param|=4.05e+04 loss=3.0840e-01 ppl=1.36                                                 
Validation - loss=3.4089e-01 ppl=1.41 best_loss=3.4134e-01 best_ppl=1.41                                                
Epoch 52 - |param|=6.65e+02 |g_param|=3.09e+04 loss=2.8526e-01 ppl=1.33                                                 
Validation - loss=3.4040e-01 ppl=1.41 best_loss=3.4089e-01 best_ppl=1.41                                                
Epoch 53 - |param|=6.65e+02 |g_param|=3.84e+04 loss=2.8899e-01 ppl=1.34                                                 
Validation - loss=3.3999e-01 ppl=1.40 best_loss=3.4040e-01 best_ppl=1.41                                                
Epoch 54 - |param|=6.65e+02 |g_param|=3.88e+04 loss=2.9731e-01 ppl=1.35                                                 
Validation - loss=3.3950e-01 ppl=1.40 best_loss=3.3999e-01 best_ppl=1.40                                                
Epoch 55 - |param|=6.65e+02 |g_param|=3.60e+04 loss=2.9166e-01 ppl=1.34                                                 
Validation - loss=3.3894e-01 ppl=1.40 best_loss=3.3950e-01 best_ppl=1.40                                                
Epoch 56 - |param|=6.65e+02 |g_param|=2.05e+04 loss=2.9095e-01 ppl=1.34                                                 
Validation - loss=3.3841e-01 ppl=1.40 best_loss=3.3894e-01 best_ppl=1.40                                                
Epoch 57 - |param|=6.65e+02 |g_param|=1.60e+04 loss=2.7740e-01 ppl=1.32                                                 
Validation - loss=3.3799e-01 ppl=1.40 best_loss=3.3841e-01 best_ppl=1.40                                                
Epoch 58 - |param|=6.65e+02 |g_param|=1.78e+04 loss=2.8178e-01 ppl=1.33                                                 
Validation - loss=3.3724e-01 ppl=1.40 best_loss=3.3799e-01 best_ppl=1.40                                                
Epoch 59 - |param|=6.65e+02 |g_param|=1.51e+04 loss=2.7692e-01 ppl=1.32                                                 
Validation - loss=3.3630e-01 ppl=1.40 best_loss=3.3724e-01 best_ppl=1.40                                                
Epoch 60 - |param|=6.65e+02 |g_param|=1.55e+04 loss=2.7863e-01 ppl=1.32                                                 
Validation - loss=3.3607e-01 ppl=1.40 best_loss=3.3630e-01 best_ppl=1.40                                                

real	4m42.284s
user	4m38.467s
sys	0m4.114s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

လိုချင်တဲ့ ပုံစံမျိုးတော့ training လုပ်သွားပြီ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ls ./model/rl/
seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth      seq-rl-model-myrk.37.0.36-1.43.0.37-1.44.pth  seq-rl-model-myrk.49.0.29-1.34.0.34-1.41.pth
seq-rl-model-myrk.30.0.32-1.37.0.35-1.42.pth.hyp  seq-rl-model-myrk.38.0.36-1.43.0.36-1.44.pth  seq-rl-model-myrk.50.0.29-1.34.0.34-1.41.pth
seq-rl-model-myrk.30.0.37-1.45.0.38-1.46.pth      seq-rl-model-myrk.39.0.37-1.44.0.36-1.44.pth  seq-rl-model-myrk.51.0.31-1.36.0.34-1.41.pth
seq-rl-model-myrk.30.0.39-1.47.0.38-1.46.pth      seq-rl-model-myrk.40.0.36-1.43.0.36-1.44.pth  seq-rl-model-myrk.52.0.29-1.33.0.34-1.41.pth
seq-rl-model-myrk.30.0.39-1.47.0.38-1.46.pth.hyp  seq-rl-model-myrk.41.0.35-1.42.0.36-1.43.pth  seq-rl-model-myrk.53.0.29-1.34.0.34-1.40.pth
seq-rl-model-myrk.30.0.39-1.48.0.38-1.46.pth      seq-rl-model-myrk.42.0.34-1.41.0.35-1.43.pth  seq-rl-model-myrk.54.0.30-1.35.0.34-1.40.pth
seq-rl-model-myrk.31.0.39-1.48.0.38-1.46.pth      seq-rl-model-myrk.43.0.32-1.37.0.35-1.42.pth  seq-rl-model-myrk.55.0.29-1.34.0.34-1.40.pth
seq-rl-model-myrk.32.0.38-1.47.0.37-1.45.pth      seq-rl-model-myrk.44.0.33-1.39.0.35-1.42.pth  seq-rl-model-myrk.56.0.29-1.34.0.34-1.40.pth
seq-rl-model-myrk.33.0.37-1.45.0.37-1.45.pth      seq-rl-model-myrk.45.0.32-1.37.0.35-1.42.pth  seq-rl-model-myrk.57.0.28-1.32.0.34-1.40.pth
seq-rl-model-myrk.34.0.37-1.45.0.37-1.45.pth      seq-rl-model-myrk.46.0.31-1.37.0.35-1.41.pth  seq-rl-model-myrk.58.0.28-1.33.0.34-1.40.pth
seq-rl-model-myrk.35.0.37-1.45.0.37-1.45.pth      seq-rl-model-myrk.47.0.32-1.38.0.34-1.41.pth  seq-rl-model-myrk.59.0.28-1.32.0.34-1.40.pth
seq-rl-model-myrk.36.0.37-1.45.0.37-1.45.pth      seq-rl-model-myrk.48.0.29-1.33.0.34-1.41.pth  seq-rl-model-myrk.60.0.28-1.32.0.34-1.40.pth
(simple-nmt) ye@:~/exp/simple-nmt$
```

ရလဒ်က တက်လာ မလာကိုတော့ testing/evaluation လုပ်ပြီးအောက်ပါအတိုင်း ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./model/rl/seq-rl-model-myrk.60.0.28-1.32.0.34-1.40.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./model/rl/seq-rl-model-myrk.60.0.28-1.32.0.34-1.40.pth.hyp

real	0m19.209s
user	0m18.737s
sys	0m1.083s
(simple-nmt) ye@:~/exp/simple-nmt$
```

evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.28-1.32.0.34-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.23, 86.9/77.2/69.1/62.0 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

seq-to-seq epoch 30 ရဲ့ ရလဒ် က အောက်ပါအတိုင်း...  
BLEU = 73.13, 87.0/77.3/68.9/61.7 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)  
RL နဲ့ training လုပ်တာ တက်တော့ တက်လာတယ် significantly တက်လာတာတော့ မဟုတ်ဘူး...  

## Playing with --max_grad_norm

--max_grad_norm ကို 1 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.31-1.37.0.34-1.41.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 72.06, 86.3/76.4/67.8/60.3 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
```

--max_grad_norm ကို 10 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.27-1.31.0.34-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.05, 86.8/77.1/68.9/61.8 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

--max_grad_norm ကို 12 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.27-1.32.0.33-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.23, 86.9/77.2/69.1/62.0 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

--max_grad_norm ကို 15 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.30-1.35.0.34-1.41.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 72.44, 86.5/76.7/68.2/60.9 (BP=1.000, ratio=1.033, hyp_len=23933, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

--max_grad_norm 30 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.29-1.33.0.34-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 72.72, 86.6/76.8/68.6/61.4 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

--max_grad_norm 100 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.60.0.26-1.30.0.33-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.32, 86.8/77.3/69.2/62.2 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Playing with --max_grad_norm and --n_epochs

time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 2 --max_grad_norm 5 --n_epochs 100

ရလဒ်က အောက်ပါအတိုင်း...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.100.0.28-1.32.0.33-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.19, 86.8/77.2/69.1/62.0 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 1 --max_grad_norm 6 --n_epochs 100

ရလဒ် က ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.100.0.20-1.23.0.34-1.40.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.61, 87.1/77.5/69.5/62.6 (BP=1.000, ratio=1.035, hyp_len=23975, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk.30.0.30-1.34.0.34-1.41.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 1 --max_grad_norm 7 --n_epochs 100


အခုချိန်ထိ run ခဲ့တဲ့ထဲမှာ ဒီ BLEU score က အများဆုံးပဲ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.100.0.16-1.18.0.35-1.42.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.98, 87.2/77.8/70.0/63.1 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
```

## Tuning Baseline Seq-to-Seq Model

time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 1000 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./seq-model-myrk2.pth

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 1000 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./seq-model-myrk2.pth
...
...
...
Epoch 907 - |param|=8.42e+02 |g_param|=8.35e+03 loss=1.4338e-02 ppl=1.01                                                
Validation - loss=7.5941e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 908 - |param|=8.42e+02 |g_param|=2.02e+04 loss=1.8187e-02 ppl=1.02                                                
Validation - loss=7.6835e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 909 - |param|=8.42e+02 |g_param|=1.97e+04 loss=1.8039e-02 ppl=1.02                                                
Validation - loss=7.7284e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 910 - |param|=8.42e+02 |g_param|=1.81e+04 loss=1.5983e-02 ppl=1.02                                                
Validation - loss=7.5070e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 911 - |param|=8.42e+02 |g_param|=1.62e+04 loss=1.6135e-02 ppl=1.02                                                
Validation - loss=7.6007e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 912 - |param|=8.42e+02 |g_param|=2.07e+04 loss=1.4904e-02 ppl=1.02                                                
Validation - loss=7.9212e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 913 - |param|=8.43e+02 |g_param|=1.85e+04 loss=1.5408e-02 ppl=1.02                                                
Validation - loss=7.7528e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 914 - |param|=8.43e+02 |g_param|=2.38e+04 loss=1.9566e-02 ppl=1.02                                                
Validation - loss=7.3382e-01 ppl=2.08 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 915 - |param|=8.43e+02 |g_param|=1.60e+04 loss=1.6911e-02 ppl=1.02                                                
Validation - loss=7.4430e-01 ppl=2.10 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 916 - |param|=8.43e+02 |g_param|=1.70e+04 loss=1.6711e-02 ppl=1.02                                                
Validation - loss=7.5026e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 917 - |param|=8.43e+02 |g_param|=1.58e+04 loss=1.4738e-02 ppl=1.01                                                
Validation - loss=7.7132e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 918 - |param|=8.43e+02 |g_param|=1.74e+04 loss=1.5198e-02 ppl=1.02                                                
Validation - loss=7.4867e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 919 - |param|=8.43e+02 |g_param|=2.04e+04 loss=1.3999e-02 ppl=1.01                                                
Validation - loss=7.4734e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 920 - |param|=8.43e+02 |g_param|=1.87e+04 loss=1.6061e-02 ppl=1.02                                                
Validation - loss=7.5622e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 921 - |param|=8.43e+02 |g_param|=1.82e+04 loss=1.5679e-02 ppl=1.02                                                
Validation - loss=7.5860e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 922 - |param|=8.43e+02 |g_param|=1.68e+04 loss=1.4832e-02 ppl=1.01                                                
Validation - loss=7.9302e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 923 - |param|=8.44e+02 |g_param|=1.46e+04 loss=1.6799e-02 ppl=1.02                                                
Validation - loss=7.8770e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 924 - |param|=8.44e+02 |g_param|=8.37e+03 loss=1.4763e-02 ppl=1.01                                                
Validation - loss=7.5376e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 925 - |param|=8.44e+02 |g_param|=8.02e+03 loss=1.5111e-02 ppl=1.02                                                
Validation - loss=7.7541e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 926 - |param|=8.44e+02 |g_param|=6.70e+03 loss=1.4026e-02 ppl=1.01                                                
Validation - loss=7.8666e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 927 - |param|=8.44e+02 |g_param|=7.63e+03 loss=1.4940e-02 ppl=1.02                                                
Validation - loss=7.4006e-01 ppl=2.10 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 928 - |param|=8.44e+02 |g_param|=7.61e+03 loss=1.3966e-02 ppl=1.01                                                
Validation - loss=7.3891e-01 ppl=2.09 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 929 - |param|=8.44e+02 |g_param|=7.64e+03 loss=1.4633e-02 ppl=1.01                                                
Validation - loss=7.7222e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 930 - |param|=8.44e+02 |g_param|=8.13e+03 loss=1.4819e-02 ppl=1.01                                                
Validation - loss=7.7994e-01 ppl=2.18 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 931 - |param|=8.44e+02 |g_param|=7.87e+03 loss=1.6248e-02 ppl=1.02                                                
Validation - loss=7.7372e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 932 - |param|=8.45e+02 |g_param|=7.34e+03 loss=1.3936e-02 ppl=1.01                                                
Validation - loss=7.6777e-01 ppl=2.15 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 933 - |param|=8.45e+02 |g_param|=1.25e+04 loss=1.7763e-02 ppl=1.02                                                
Validation - loss=7.4749e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 934 - |param|=8.45e+02 |g_param|=1.00e+04 loss=1.7909e-02 ppl=1.02                                                
Validation - loss=7.5722e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 935 - |param|=8.45e+02 |g_param|=1.07e+04 loss=1.8303e-02 ppl=1.02                                                
Validation - loss=7.5167e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 936 - |param|=8.45e+02 |g_param|=8.86e+03 loss=1.8822e-02 ppl=1.02                                                
Validation - loss=7.3930e-01 ppl=2.09 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 937 - |param|=8.45e+02 |g_param|=1.65e+04 loss=2.4088e-02 ppl=1.02                                                
Validation - loss=7.7041e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 938 - |param|=8.46e+02 |g_param|=1.18e+04 loss=2.5635e-02 ppl=1.03                                                
Validation - loss=7.7869e-01 ppl=2.18 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 939 - |param|=8.46e+02 |g_param|=1.03e+04 loss=1.8329e-02 ppl=1.02                                                
Validation - loss=7.6371e-01 ppl=2.15 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 940 - |param|=8.46e+02 |g_param|=2.07e+04 loss=2.0848e-02 ppl=1.02                                                
Validation - loss=7.6440e-01 ppl=2.15 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 941 - |param|=8.46e+02 |g_param|=1.82e+04 loss=1.7887e-02 ppl=1.02                                                
Validation - loss=7.4256e-01 ppl=2.10 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 942 - |param|=8.46e+02 |g_param|=1.59e+04 loss=1.5949e-02 ppl=1.02                                                
Validation - loss=7.7888e-01 ppl=2.18 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 943 - |param|=8.46e+02 |g_param|=1.50e+04 loss=1.6144e-02 ppl=1.02                                                
Validation - loss=8.0698e-01 ppl=2.24 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 944 - |param|=8.46e+02 |g_param|=1.23e+04 loss=1.4470e-02 ppl=1.01                                                
Validation - loss=7.9137e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 945 - |param|=8.46e+02 |g_param|=9.56e+03 loss=1.7222e-02 ppl=1.02                                                
Validation - loss=7.8246e-01 ppl=2.19 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 946 - |param|=8.47e+02 |g_param|=7.85e+03 loss=1.7374e-02 ppl=1.02                                                
Validation - loss=7.4791e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 947 - |param|=8.47e+02 |g_param|=9.35e+03 loss=1.8875e-02 ppl=1.02                                                
Validation - loss=7.2773e-01 ppl=2.07 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 948 - |param|=8.47e+02 |g_param|=9.72e+03 loss=1.7260e-02 ppl=1.02                                                
Validation - loss=7.3782e-01 ppl=2.09 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 949 - |param|=8.47e+02 |g_param|=1.25e+04 loss=1.7849e-02 ppl=1.02                                                
Validation - loss=7.2682e-01 ppl=2.07 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 950 - |param|=8.47e+02 |g_param|=9.60e+03 loss=1.9196e-02 ppl=1.02                                                
Validation - loss=7.9389e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 951 - |param|=8.47e+02 |g_param|=1.45e+04 loss=2.4228e-02 ppl=1.02                                                
Validation - loss=8.3279e-01 ppl=2.30 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 952 - |param|=8.47e+02 |g_param|=1.08e+04 loss=2.0192e-02 ppl=1.02                                                
Validation - loss=8.2810e-01 ppl=2.29 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 953 - |param|=8.48e+02 |g_param|=1.19e+04 loss=1.8644e-02 ppl=1.02                                                
Validation - loss=7.9862e-01 ppl=2.22 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 954 - |param|=8.48e+02 |g_param|=1.41e+04 loss=2.7433e-02 ppl=1.03                                                
Validation - loss=8.0436e-01 ppl=2.24 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 955 - |param|=8.48e+02 |g_param|=1.10e+04 loss=2.3687e-02 ppl=1.02                                                
Validation - loss=8.2001e-01 ppl=2.27 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 956 - |param|=8.48e+02 |g_param|=1.55e+04 loss=2.5624e-02 ppl=1.03                                                
Validation - loss=8.1233e-01 ppl=2.25 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 957 - |param|=8.48e+02 |g_param|=1.83e+04 loss=3.0705e-02 ppl=1.03                                                
Validation - loss=7.9397e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 958 - |param|=8.48e+02 |g_param|=1.54e+04 loss=2.7216e-02 ppl=1.03                                                
Validation - loss=8.1284e-01 ppl=2.25 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 959 - |param|=8.49e+02 |g_param|=1.04e+04 loss=3.5060e-02 ppl=1.04                                                
Validation - loss=7.7409e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 960 - |param|=8.49e+02 |g_param|=8.28e+03 loss=2.6587e-02 ppl=1.03                                                
Validation - loss=7.8645e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 961 - |param|=8.49e+02 |g_param|=6.31e+03 loss=2.3300e-02 ppl=1.02                                                
Validation - loss=7.7195e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 962 - |param|=8.49e+02 |g_param|=5.58e+03 loss=2.0968e-02 ppl=1.02                                                
Validation - loss=7.8632e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 963 - |param|=8.49e+02 |g_param|=4.98e+03 loss=1.6233e-02 ppl=1.02                                                
Validation - loss=7.4692e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 964 - |param|=8.49e+02 |g_param|=5.41e+03 loss=1.7974e-02 ppl=1.02                                                
Validation - loss=7.5674e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 965 - |param|=8.49e+02 |g_param|=4.57e+03 loss=1.5619e-02 ppl=1.02                                                
Validation - loss=7.9177e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 966 - |param|=8.49e+02 |g_param|=4.49e+03 loss=1.4207e-02 ppl=1.01                                                
Validation - loss=7.7743e-01 ppl=2.18 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 967 - |param|=8.49e+02 |g_param|=3.73e+03 loss=1.5769e-02 ppl=1.02                                                
Validation - loss=7.9579e-01 ppl=2.22 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 968 - |param|=8.49e+02 |g_param|=4.79e+03 loss=1.5986e-02 ppl=1.02                                                
Validation - loss=7.8499e-01 ppl=2.19 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 969 - |param|=8.50e+02 |g_param|=4.77e+03 loss=1.5151e-02 ppl=1.02                                                
Validation - loss=7.9060e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 970 - |param|=8.50e+02 |g_param|=3.21e+03 loss=1.3528e-02 ppl=1.01                                                
Validation - loss=7.9370e-01 ppl=2.21 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 971 - |param|=8.50e+02 |g_param|=3.97e+03 loss=1.4520e-02 ppl=1.01                                                
Validation - loss=8.2432e-01 ppl=2.28 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 972 - |param|=8.50e+02 |g_param|=3.20e+03 loss=1.3265e-02 ppl=1.01                                                
Validation - loss=8.1633e-01 ppl=2.26 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 973 - |param|=8.50e+02 |g_param|=5.90e+03 loss=1.3821e-02 ppl=1.01                                                
Validation - loss=7.8997e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 974 - |param|=8.50e+02 |g_param|=5.31e+03 loss=2.0858e-02 ppl=1.02                                                
Validation - loss=8.0296e-01 ppl=2.23 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 975 - |param|=8.50e+02 |g_param|=5.45e+03 loss=1.5474e-02 ppl=1.02                                                
Validation - loss=8.0643e-01 ppl=2.24 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 976 - |param|=8.50e+02 |g_param|=7.07e+03 loss=1.4410e-02 ppl=1.01                                                
Validation - loss=7.7591e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 977 - |param|=8.50e+02 |g_param|=7.64e+03 loss=1.4365e-02 ppl=1.01                                                
Validation - loss=7.5719e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 978 - |param|=8.50e+02 |g_param|=7.48e+03 loss=1.4543e-02 ppl=1.01                                                
Validation - loss=7.8594e-01 ppl=2.19 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 979 - |param|=8.50e+02 |g_param|=8.34e+03 loss=1.4299e-02 ppl=1.01                                                
Validation - loss=7.5199e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 980 - |param|=8.51e+02 |g_param|=1.46e+04 loss=1.7103e-02 ppl=1.02                                                
Validation - loss=7.6923e-01 ppl=2.16 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 981 - |param|=8.51e+02 |g_param|=1.36e+04 loss=1.8868e-02 ppl=1.02                                                
Validation - loss=7.2690e-01 ppl=2.07 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 982 - |param|=8.51e+02 |g_param|=1.21e+04 loss=2.1521e-02 ppl=1.02                                                
Validation - loss=7.9924e-01 ppl=2.22 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 983 - |param|=8.51e+02 |g_param|=2.39e+04 loss=3.0208e-02 ppl=1.03                                                
Validation - loss=7.8931e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 984 - |param|=8.51e+02 |g_param|=1.30e+04 loss=2.9576e-02 ppl=1.03                                                
Validation - loss=7.7967e-01 ppl=2.18 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 985 - |param|=8.52e+02 |g_param|=1.35e+04 loss=2.3967e-02 ppl=1.02                                                
Validation - loss=7.5856e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 986 - |param|=8.52e+02 |g_param|=1.04e+04 loss=2.2139e-02 ppl=1.02                                                
Validation - loss=7.3794e-01 ppl=2.09 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 987 - |param|=8.52e+02 |g_param|=1.05e+04 loss=2.2252e-02 ppl=1.02                                                
Validation - loss=7.5145e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 988 - |param|=8.52e+02 |g_param|=5.54e+03 loss=1.8045e-02 ppl=1.02                                                
Validation - loss=7.6208e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 989 - |param|=8.52e+02 |g_param|=4.26e+03 loss=1.5512e-02 ppl=1.02                                                
Validation - loss=7.4695e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 990 - |param|=8.52e+02 |g_param|=3.85e+03 loss=1.5102e-02 ppl=1.02                                                
Validation - loss=7.2786e-01 ppl=2.07 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 991 - |param|=8.52e+02 |g_param|=4.25e+03 loss=1.5069e-02 ppl=1.02                                                
Validation - loss=7.5217e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 992 - |param|=8.52e+02 |g_param|=4.16e+03 loss=1.5439e-02 ppl=1.02                                                
Validation - loss=7.5395e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 993 - |param|=8.52e+02 |g_param|=3.45e+03 loss=1.3772e-02 ppl=1.01                                                
Validation - loss=7.4814e-01 ppl=2.11 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 994 - |param|=8.52e+02 |g_param|=3.78e+03 loss=1.3066e-02 ppl=1.01                                                
Validation - loss=7.5146e-01 ppl=2.12 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 995 - |param|=8.52e+02 |g_param|=4.49e+03 loss=1.3644e-02 ppl=1.01                                                
Validation - loss=7.6170e-01 ppl=2.14 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 996 - |param|=8.52e+02 |g_param|=4.93e+03 loss=1.2981e-02 ppl=1.01                                                
Validation - loss=7.7406e-01 ppl=2.17 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 997 - |param|=8.53e+02 |g_param|=4.63e+03 loss=1.7511e-02 ppl=1.02                                                
Validation - loss=7.6677e-01 ppl=2.15 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 998 - |param|=8.53e+02 |g_param|=6.27e+03 loss=1.9336e-02 ppl=1.02                                                
Validation - loss=7.8994e-01 ppl=2.20 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 999 - |param|=8.53e+02 |g_param|=1.03e+04 loss=1.9356e-02 ppl=1.02                                                
Validation - loss=7.5412e-01 ppl=2.13 best_loss=3.5775e-01 best_ppl=1.43                                                
Epoch 1000 - |param|=8.53e+02 |g_param|=7.50e+03 loss=2.1157e-02 ppl=1.02                                               
Validation - loss=7.4237e-01 ppl=2.10 best_loss=3.5775e-01 best_ppl=1.43                                                

real	207m31.652s
user	204m55.505s
sys	2m37.044s
```

Testing ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./seq-model-myrk2.1000.0.02-1.02.0.74-2.10.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./seq-model-myrk2.1000.0.02-1.02.0.74-2.10.pth.hyp

real	0m22.420s
user	0m18.990s
sys	0m1.174s
```

Evaluation ...  
```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./seq-model-myrk2.1000.0.02-1.02.0.74-2.10.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 74.08, 87.7/77.9/69.9/63.0 (BP=1.000, ratio=1.029, hyp_len=23838, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

တခြား ကြား epoch မော်ဒယ် တချို့နဲ့လည်း testing/evaluation လုပ်ကြည့်ပြီး BLEU score ကို check လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./seq-model-myrk2.500.0.02-1.02.0.70-2.02.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./seq-model-myrk2.500.0.02-1.02.0.70-2.02.pth.hyp

real	0m19.664s
user	0m19.115s
sys	0m1.164s
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./seq-model-myrk2.500.0.02-1.02.0.70-2.02.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.91, 87.5/77.8/69.8/62.8 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ကို အကြိမ်ကြိမ်အခါခါ လုပ်ရမှာမို့ command ပေးရတဲ့ အချိန်သက်သာအောင် shell script ရေးခဲ့...  

```bash
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./test-eval.sh 
#!/bin/bash

MODEL=$1;

# Testing
time python translate.py --model_fn $MODEL --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > $MODEL.hyp

# Evaluation with BLEU Score
cat $MODEL.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
```

test-eval.sh ကို သုံးပြီး epoch 600 မော်ဒယ်သုံးပြီးတော့ testing/evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.600.0.03-1.03.0.69-1.99.pth

real	0m19.625s
user	0m19.132s
sys	0m1.116s
BLEU = 73.55, 87.4/77.5/69.3/62.3 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

epoch 700 မော်ဒယ်ကို သုံးပြီးတော့ testing/evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.700.0.02-1.02.0.77-2.16.pth

real	0m19.654s
user	0m19.056s
sys	0m1.197s
BLEU = 74.05, 87.6/77.9/69.9/63.1 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```
epoch 800 မော်ဒယ်နဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.800.0.02-1.02.0.72-2.06.pth

real	0m19.500s
user	0m19.062s
sys	0m1.071s
BLEU = 74.28, 87.7/78.0/70.1/63.4 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
```

epoch 810 မော်ဒယ်နဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.810.0.01-1.01.0.72-2.06.pth

real	0m19.256s
user	0m18.785s
sys	0m1.017s
BLEU = 74.10, 87.6/77.9/69.9/63.2 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
```

epoch 860 မော်ဒယ်နဲ့ evaluation result က ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.860.0.02-1.02.0.76-2.14.pth

real	0m19.417s
user	0m18.840s
sys	0m1.188s
BLEU = 73.91, 87.7/77.9/69.7/62.7 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
```

880 နဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.880.0.02-1.02.0.76-2.14.pth

real	0m19.663s
user	0m19.052s
sys	0m1.229s
BLEU = 73.97, 87.8/77.9/69.8/62.7 (BP=1.000, ratio=1.032, hyp_len=23903, ref_len=23160)
```

885 မော်ဒယ်နဲ့ ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ ./test-eval.sh seq-model-myrk2.885.0.01-1.01.0.75-2.12.pth

real	0m19.581s
user	0m19.108s
sys	0m1.084s
BLEU = 74.54, 87.9/78.3/70.4/63.7 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

မော်ဒယ် အကုန်ရဲ့ ရလဒ်တွေကို ကြည့်ချင်လို့ အောက်ပါအတိုင်း shell script ရေးခဲ့...  

```bash
#!/bin/bash

# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score

for i in *.pth; do
   MODEL=$i;

   # Testing
   time python translate.py --model_fn $MODEL --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-myrk-seq2seq-baseline-1000epoch.txt;
   cat $MODEL.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk | tee  -a eval-results-myrk-seq2seq-baseline-1000epoch.txt

done
```

run ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop.sh
...
...
...
Evaluation result for the model: seq-model-myrk2.996.0.01-1.01.0.77-2.17.pth
BLEU = 74.43, 88.0/78.2/70.3/63.4 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)

real	0m21.107s
user	0m21.263s
sys	0m1.222s
Evaluation result for the model: seq-model-myrk2.997.0.02-1.02.0.77-2.15.pth
BLEU = 74.13, 87.8/77.9/69.9/63.1 (BP=1.000, ratio=1.032, hyp_len=23904, ref_len=23160)

real	0m19.922s
user	0m18.823s
sys	0m1.162s
Evaluation result for the model: seq-model-myrk2.998.0.02-1.02.0.79-2.20.pth
BLEU = 74.25, 87.9/78.0/70.1/63.2 (BP=1.000, ratio=1.030, hyp_len=23846, ref_len=23160)

real	0m19.644s
user	0m19.207s
sys	0m1.111s
Evaluation result for the model: seq-model-myrk2.999.0.02-1.02.0.75-2.13.pth
BLEU = 73.89, 87.6/77.8/69.7/62.8 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)

real	0m19.505s
user	0m18.992s
sys	0m1.194s
Evaluation result for the model: seq-model-myrk.30.0.30-1.34.0.34-1.41.pth
BLEU = 73.13, 87.0/77.3/68.9/61.7 (BP=1.000, ratio=1.031, hyp_len=23887, ref_len=23160)

real	347m13.587s
user	327m11.204s
sys	21m12.131s
```

output ရေးထားတဲ့ ဖိုင်ကို လေ့လာတော့ အများဆုံးက 75.xx ပဲ ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ grep -B 1 "BLEU = 75." ./eval-results-myrk-seq2seq-baseline-1000epoch.txt
Evaluation result for the model: seq-model-myrk2.174.0.08-1.09.0.52-1.68.pth
BLEU = 75.12, 88.0/78.7/71.1/64.7 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth
BLEU = 75.35, 88.3/78.9/71.3/64.9 (BP=1.000, ratio=1.024, hyp_len=23712, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.359.0.03-1.03.0.66-1.93.pth
BLEU = 75.30, 88.2/78.9/71.3/64.8 (BP=1.000, ratio=1.030, hyp_len=23852, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.615.0.02-1.02.0.75-2.11.pth
BLEU = 75.31, 88.4/79.0/71.3/64.6 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.657.0.03-1.03.0.71-2.04.pth
BLEU = 75.00, 88.0/78.7/71.0/64.3 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.742.0.02-1.02.0.74-2.09.pth
BLEU = 75.03, 88.2/78.8/71.0/64.3 (BP=1.000, ratio=1.031, hyp_len=23869, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.765.0.02-1.02.0.77-2.16.pth
BLEU = 75.17, 88.4/78.9/71.1/64.4 (BP=1.000, ratio=1.026, hyp_len=23755, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.807.0.01-1.01.0.73-2.07.pth
BLEU = 75.00, 88.1/78.7/70.9/64.3 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.817.0.01-1.01.0.77-2.16.pth
BLEU = 75.12, 88.2/78.8/71.1/64.5 (BP=1.000, ratio=1.029, hyp_len=23829, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.835.0.02-1.02.0.76-2.15.pth
BLEU = 75.08, 88.3/78.8/71.0/64.3 (BP=1.000, ratio=1.028, hyp_len=23812, ref_len=23160)
--
Evaluation result for the model: seq-model-myrk2.945.0.02-1.02.0.78-2.19.pth
BLEU = 75.07, 88.2/78.7/71.1/64.4 (BP=1.000, ratio=1.027, hyp_len=23783, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

လက်ရှိ အချိန်ထိ ဒီ epoch 1000 မော်ဒယ်က BLEU score အများဆုံး ရတယ်။  
epoch 1000 ကို ၃နာရီကြာတယ်။  
epoch 321 မှာ 75.35 ထိ ရပြီ။ ဒါက အများဆုံးပဲ။  
တခြား parameter တွေကို ကစားကြည့်ရင်တော့ ထပ်တိုးနိုင်မယ်လို့ မျှော်လင့်တယ်...  


## RL with 1000 epoch Best Model

time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq2seq/seq-rl-model-myrk.pth --init_epoch 321 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 421

RL training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq2seq/seq-rl-model-myrk.pth --init_epoch 321 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 421
...
...
Epoch 408 - |param|=7.60e+02 |g_param|=3.79e+04 loss=4.4690e-02 ppl=1.05                                                
Validation - loss=6.8494e-01 ppl=1.98 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 409 - |param|=7.60e+02 |g_param|=2.80e+04 loss=4.6806e-02 ppl=1.05                                                
Validation - loss=6.8471e-01 ppl=1.98 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 410 - |param|=7.61e+02 |g_param|=2.64e+04 loss=4.5635e-02 ppl=1.05                                                
Validation - loss=6.5884e-01 ppl=1.93 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 411 - |param|=7.61e+02 |g_param|=3.52e+04 loss=4.7538e-02 ppl=1.05                                                
Validation - loss=6.6292e-01 ppl=1.94 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 412 - |param|=7.61e+02 |g_param|=2.49e+04 loss=4.0064e-02 ppl=1.04                                                
Validation - loss=7.2319e-01 ppl=2.06 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 413 - |param|=7.61e+02 |g_param|=2.62e+04 loss=4.3641e-02 ppl=1.04                                                
Validation - loss=6.6683e-01 ppl=1.95 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 414 - |param|=7.62e+02 |g_param|=3.01e+04 loss=4.1917e-02 ppl=1.04                                                
Validation - loss=6.6266e-01 ppl=1.94 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 415 - |param|=7.62e+02 |g_param|=3.02e+04 loss=4.3440e-02 ppl=1.04                                                
Validation - loss=6.8895e-01 ppl=1.99 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 416 - |param|=7.62e+02 |g_param|=2.67e+04 loss=3.9893e-02 ppl=1.04                                                
Validation - loss=7.1238e-01 ppl=2.04 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 417 - |param|=7.63e+02 |g_param|=3.81e+04 loss=3.1773e-02 ppl=1.03                                                
Validation - loss=6.9851e-01 ppl=2.01 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 418 - |param|=7.63e+02 |g_param|=3.20e+04 loss=3.1375e-02 ppl=1.03                                                
Validation - loss=6.9530e-01 ppl=2.00 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 419 - |param|=7.63e+02 |g_param|=2.70e+04 loss=4.2429e-02 ppl=1.04                                                
Validation - loss=6.8891e-01 ppl=1.99 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 420 - |param|=7.63e+02 |g_param|=2.63e+04 loss=4.1113e-02 ppl=1.04                                                
Validation - loss=6.7337e-01 ppl=1.96 best_loss=6.4399e-01 best_ppl=1.90                                                
Epoch 421 - |param|=7.64e+02 |g_param|=2.87e+04 loss=4.4784e-02 ppl=1.05                                                
Validation - loss=6.6101e-01 ppl=1.94 best_loss=6.4399e-01 best_ppl=1.90                                                

real	22m15.582s
user	22m0.061s
sys	0m15.959s
```

testing/eval လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq$ time ./test-eval-loop.sh
...
...
...
Evaluation result for the model: seq-rl-model-myrk.391.0.02-1.02.0.70-2.02.pth
BLEU = 74.39, 87.8/78.1/70.3/63.5 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.392.0.02-1.02.0.67-1.96.pth
BLEU = 74.48, 87.6/78.1/70.4/63.9 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.393.0.02-1.02.0.70-2.01.pth
BLEU = 74.70, 87.8/78.3/70.7/64.1 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.394.0.02-1.02.0.71-2.04.pth
BLEU = 74.64, 87.8/78.3/70.6/64.0 (BP=1.000, ratio=1.034, hyp_len=23945, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.395.0.02-1.02.0.71-2.04.pth
BLEU = 74.63, 87.9/78.3/70.5/63.9 (BP=1.000, ratio=1.032, hyp_len=23893, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.396.0.02-1.02.0.70-2.02.pth
BLEU = 74.81, 87.8/78.5/70.8/64.2 (BP=1.000, ratio=1.032, hyp_len=23908, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.397.0.02-1.02.0.68-1.98.pth
BLEU = 74.46, 87.8/78.2/70.4/63.6 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.398.0.02-1.02.0.70-2.02.pth
BLEU = 74.35, 87.8/78.1/70.2/63.5 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.399.0.03-1.03.0.70-2.01.pth
BLEU = 74.22, 87.6/77.9/70.1/63.4 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.400.0.05-1.05.0.71-2.03.pth
BLEU = 73.72, 87.4/77.5/69.5/62.7 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.401.0.06-1.06.0.76-2.14.pth
BLEU = 74.18, 87.7/77.9/70.0/63.3 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.402.0.06-1.06.0.70-2.02.pth
BLEU = 74.22, 87.8/78.0/70.1/63.2 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.403.0.05-1.05.0.65-1.92.pth
BLEU = 73.33, 87.4/77.3/69.0/62.1 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.404.0.05-1.05.0.68-1.97.pth
BLEU = 73.99, 87.5/77.8/69.8/63.0 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.405.0.05-1.05.0.68-1.98.pth
BLEU = 73.84, 87.5/77.7/69.7/62.8 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.406.0.04-1.05.0.65-1.92.pth
BLEU = 73.88, 87.6/77.7/69.7/62.8 (BP=1.000, ratio=1.031, hyp_len=23886, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.407.0.05-1.05.0.67-1.95.pth
BLEU = 73.20, 87.2/77.2/69.0/61.9 (BP=1.000, ratio=1.034, hyp_len=23940, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.408.0.04-1.05.0.68-1.98.pth
BLEU = 74.02, 87.5/77.9/69.9/63.0 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.409.0.05-1.05.0.68-1.98.pth
BLEU = 73.92, 87.5/77.7/69.7/62.9 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.410.0.05-1.05.0.66-1.93.pth
BLEU = 73.77, 87.5/77.6/69.5/62.7 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.411.0.05-1.05.0.66-1.94.pth
BLEU = 73.22, 87.2/77.2/68.9/61.9 (BP=1.000, ratio=1.034, hyp_len=23940, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.412.0.04-1.04.0.72-2.06.pth
BLEU = 73.77, 87.4/77.6/69.6/62.7 (BP=1.000, ratio=1.032, hyp_len=23898, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.413.0.04-1.04.0.67-1.95.pth
BLEU = 74.78, 88.0/78.5/70.7/64.1 (BP=1.000, ratio=1.027, hyp_len=23795, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.414.0.04-1.04.0.66-1.94.pth
BLEU = 73.92, 87.5/77.7/69.7/63.0 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.415.0.04-1.04.0.69-1.99.pth
BLEU = 72.97, 86.9/76.9/68.7/61.8 (BP=1.000, ratio=1.040, hyp_len=24088, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.416.0.04-1.04.0.71-2.04.pth
BLEU = 73.30, 87.1/77.2/69.1/62.1 (BP=1.000, ratio=1.036, hyp_len=23983, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.417.0.03-1.03.0.70-2.01.pth
BLEU = 74.58, 87.9/78.3/70.4/63.8 (BP=1.000, ratio=1.029, hyp_len=23840, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.418.0.03-1.03.0.70-2.00.pth
BLEU = 74.24, 87.7/78.0/70.1/63.3 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.419.0.04-1.04.0.69-1.99.pth
BLEU = 73.33, 87.3/77.3/69.1/62.0 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.420.0.04-1.04.0.67-1.96.pth
BLEU = 73.79, 87.5/77.7/69.6/62.7 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.421.0.04-1.05.0.66-1.94.pth
BLEU = 74.90, 88.1/78.6/70.9/64.2 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)

real	33m36.852s
user	32m52.757s
sys	1m46.175s
```

RL model ရဲ့ အများဆုံးက 375 epoch မှာ   

```
Evaluation result for the model: seq-rl-model-myrk.375.0.02-1.02.0.67-1.95.pth  
BLEU = 75.03, 88.0/78.6/71.0/64.5 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)  
```

epoch ကို တိုးကြည့်ရလိမ့်မယ်...  

ဒီတစ်ခါတော့ 300 အထိ တိုးကြည့်ခဲ့...  

time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq2seq/seq-rl-model-myrk.pth --init_epoch 321 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 621

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq2seq/seq-rl-model-myrk.pth --init_epoch 321 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 621
...
...
...
Epoch 597 - |param|=8.08e+02 |g_param|=9.61e+03 loss=2.5507e-02 ppl=1.03                                                
Validation - loss=7.2046e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 598 - |param|=8.08e+02 |g_param|=1.36e+04 loss=3.1855e-02 ppl=1.03                                                
Validation - loss=6.8067e-01 ppl=1.98 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 599 - |param|=8.08e+02 |g_param|=1.18e+04 loss=3.0825e-02 ppl=1.03                                                
Validation - loss=7.2226e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 600 - |param|=8.09e+02 |g_param|=1.57e+04 loss=3.2554e-02 ppl=1.03                                                
Validation - loss=7.1817e-01 ppl=2.05 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 601 - |param|=8.09e+02 |g_param|=1.16e+04 loss=2.9991e-02 ppl=1.03                                                
Validation - loss=7.1959e-01 ppl=2.05 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 602 - |param|=8.09e+02 |g_param|=1.27e+04 loss=3.1921e-02 ppl=1.03                                                
Validation - loss=7.4603e-01 ppl=2.11 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 603 - |param|=8.09e+02 |g_param|=1.83e+04 loss=2.3178e-02 ppl=1.02                                                
Validation - loss=7.2716e-01 ppl=2.07 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 604 - |param|=8.09e+02 |g_param|=1.66e+04 loss=1.9962e-02 ppl=1.02                                                
Validation - loss=7.1960e-01 ppl=2.05 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 605 - |param|=8.09e+02 |g_param|=1.53e+04 loss=2.1266e-02 ppl=1.02                                                
Validation - loss=7.2190e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 606 - |param|=8.10e+02 |g_param|=1.61e+04 loss=1.8249e-02 ppl=1.02                                                
Validation - loss=7.2150e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 607 - |param|=8.10e+02 |g_param|=1.49e+04 loss=1.8204e-02 ppl=1.02                                                
Validation - loss=7.1732e-01 ppl=2.05 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 608 - |param|=8.10e+02 |g_param|=1.78e+04 loss=2.0931e-02 ppl=1.02                                                
Validation - loss=7.1306e-01 ppl=2.04 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 609 - |param|=8.10e+02 |g_param|=1.84e+04 loss=2.1956e-02 ppl=1.02                                                
Validation - loss=7.3837e-01 ppl=2.09 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 610 - |param|=8.10e+02 |g_param|=1.68e+04 loss=2.0927e-02 ppl=1.02                                                
Validation - loss=7.2343e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 611 - |param|=8.10e+02 |g_param|=2.59e+04 loss=1.8098e-02 ppl=1.02                                                
Validation - loss=7.3965e-01 ppl=2.10 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 612 - |param|=8.10e+02 |g_param|=1.23e+04 loss=2.4061e-02 ppl=1.02                                                
Validation - loss=7.2429e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 613 - |param|=8.11e+02 |g_param|=1.52e+04 loss=3.9957e-02 ppl=1.04                                                
Validation - loss=7.2390e-01 ppl=2.06 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 614 - |param|=8.11e+02 |g_param|=1.34e+04 loss=3.9710e-02 ppl=1.04                                                
Validation - loss=7.7760e-01 ppl=2.18 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 615 - |param|=8.12e+02 |g_param|=1.48e+04 loss=3.7774e-02 ppl=1.04                                                
Validation - loss=7.2852e-01 ppl=2.07 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 616 - |param|=8.12e+02 |g_param|=1.92e+04 loss=4.2002e-02 ppl=1.04                                                
Validation - loss=7.5429e-01 ppl=2.13 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 617 - |param|=8.12e+02 |g_param|=1.49e+04 loss=3.6698e-02 ppl=1.04                                                
Validation - loss=7.6927e-01 ppl=2.16 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 618 - |param|=8.13e+02 |g_param|=1.14e+04 loss=3.4457e-02 ppl=1.04                                                
Validation - loss=7.4806e-01 ppl=2.11 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 619 - |param|=8.13e+02 |g_param|=1.49e+04 loss=3.4657e-02 ppl=1.04                                                
Validation - loss=7.2687e-01 ppl=2.07 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 620 - |param|=8.13e+02 |g_param|=1.13e+04 loss=3.0105e-02 ppl=1.03                                                
Validation - loss=7.3255e-01 ppl=2.08 best_loss=6.3875e-01 best_ppl=1.89                                                
Epoch 621 - |param|=8.13e+02 |g_param|=1.94e+04 loss=2.4675e-02 ppl=1.02                                                
Validation - loss=7.3488e-01 ppl=2.09 best_loss=6.3875e-01 best_ppl=1.89                                                

real	66m55.598s
user	66m5.426s
sys	0m46.511s

```

testing/evaluation လုပ်ပြီး RL မော်ဒယ်က baseline seq2seq ထက် သာနိုင်မလား လေ့လာခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq$ time ./test-eval-loop.sh 
...
...
Evaluation result for the model: seq-rl-model-myrk.609.0.02-1.02.0.74-2.09.pth
BLEU = 75.06, 88.2/78.7/71.0/64.4 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.610.0.02-1.02.0.72-2.06.pth
BLEU = 74.29, 87.8/78.1/70.2/63.4 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.611.0.02-1.02.0.74-2.10.pth
BLEU = 75.20, 88.3/78.9/71.2/64.4 (BP=1.000, ratio=1.029, hyp_len=23842, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.612.0.02-1.02.0.72-2.06.pth
BLEU = 74.22, 87.8/78.1/70.1/63.2 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.613.0.04-1.04.0.72-2.06.pth
BLEU = 72.70, 86.8/76.8/68.4/61.2 (BP=1.000, ratio=1.038, hyp_len=24044, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.614.0.04-1.04.0.78-2.18.pth
BLEU = 73.10, 87.1/77.1/68.8/61.7 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.615.0.04-1.04.0.73-2.07.pth
BLEU = 74.39, 87.9/78.2/70.2/63.4 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.616.0.04-1.04.0.75-2.13.pth
BLEU = 73.94, 87.7/77.9/69.8/62.7 (BP=1.000, ratio=1.030, hyp_len=23866, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.617.0.04-1.04.0.77-2.16.pth
BLEU = 74.30, 87.8/78.2/70.2/63.3 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.618.0.03-1.04.0.75-2.11.pth
BLEU = 73.95, 87.6/77.9/69.8/62.8 (BP=1.000, ratio=1.032, hyp_len=23898, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.619.0.03-1.04.0.73-2.07.pth
BLEU = 73.51, 87.3/77.4/69.3/62.4 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.620.0.03-1.03.0.73-2.08.pth
BLEU = 74.33, 87.9/78.2/70.2/63.3 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.621.0.02-1.02.0.73-2.09.pth
BLEU = 74.02, 87.8/78.0/69.8/62.8 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)

real	120m38.663s
user	118m12.537s
sys	6m35.231s

```

အများဆုံးက ...  

```
Evaluation result for the model: seq-rl-model-myrk.423.0.03-1.03.0.69-1.99.pth
BLEU = 75.23, 88.2/78.8/71.2/64.7 (BP=1.000, ratio=1.026, hyp_len=23766, ref_len=23160)
```

1000 epoch ထိ ထပ်တိုး run ခဲ့...  
(အတိအကျ ပြောရရင်တော့ 1000-321 = 679 epoch ပါ)
```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq2seq/seq-rl-model-myrk.pth --init_epoch 321 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 1000
...
...
...
Epoch 989 - |param|=8.88e+02 |g_param|=1.11e+04 loss=2.1766e-02 ppl=1.02                                                
Validation - loss=8.8889e-01 ppl=2.43 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 990 - |param|=8.88e+02 |g_param|=8.15e+03 loss=1.5449e-02 ppl=1.02                                                
Validation - loss=9.1211e-01 ppl=2.49 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 991 - |param|=8.88e+02 |g_param|=1.01e+04 loss=1.7198e-02 ppl=1.02                                                
Validation - loss=9.0046e-01 ppl=2.46 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 992 - |param|=8.88e+02 |g_param|=7.69e+03 loss=1.4566e-02 ppl=1.01                                                
Validation - loss=9.0977e-01 ppl=2.48 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 993 - |param|=8.88e+02 |g_param|=9.97e+03 loss=1.5941e-02 ppl=1.02                                                
Validation - loss=9.1653e-01 ppl=2.50 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 994 - |param|=8.88e+02 |g_param|=7.59e+03 loss=1.3759e-02 ppl=1.01                                                
Validation - loss=8.8128e-01 ppl=2.41 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 995 - |param|=8.88e+02 |g_param|=9.23e+03 loss=1.8875e-02 ppl=1.02                                                
Validation - loss=8.9639e-01 ppl=2.45 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 996 - |param|=8.88e+02 |g_param|=1.00e+04 loss=1.4790e-02 ppl=1.01                                                
Validation - loss=9.3133e-01 ppl=2.54 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 997 - |param|=8.89e+02 |g_param|=6.95e+03 loss=1.6642e-02 ppl=1.02                                                
Validation - loss=9.1985e-01 ppl=2.51 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 998 - |param|=8.89e+02 |g_param|=7.31e+03 loss=1.9985e-02 ppl=1.02                                                
Validation - loss=9.2265e-01 ppl=2.52 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 999 - |param|=8.89e+02 |g_param|=6.77e+03 loss=3.2371e-02 ppl=1.03                                                
Validation - loss=9.3265e-01 ppl=2.54 best_loss=6.4296e-01 best_ppl=1.90                                                
Epoch 1000 - |param|=8.89e+02 |g_param|=6.51e+03 loss=3.2904e-02 ppl=1.03                                               
Validation - loss=8.8388e-01 ppl=2.42 best_loss=6.4296e-01 best_ppl=1.90                                                

real	149m46.537s
user	148m4.387s
sys	1m41.063s
```

အတိအကျ ပြောရရင်တော့ 1000-321 = 679 epoch RL model ကို သုံးပြီးတော့ testing/evaluation ပြန်လုပ်ခဲ့...  
baseline 75.35 ထက် ကျော်မှဖြစ်လိမ့်မယ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq$ time ./test-eval-loop.sh 
...
...
...
Evaluation result for the model: seq-rl-model-myrk.987.0.02-1.02.0.91-2.47.pth
BLEU = 74.23, 87.8/78.2/70.1/63.1 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.988.0.03-1.03.0.88-2.42.pth
BLEU = 73.63, 87.6/77.7/69.4/62.3 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.989.0.02-1.02.0.89-2.43.pth
BLEU = 74.43, 88.0/78.3/70.3/63.4 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.990.0.02-1.02.0.91-2.49.pth
BLEU = 74.59, 88.1/78.5/70.4/63.6 (BP=1.000, ratio=1.031, hyp_len=23885, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.991.0.02-1.02.0.90-2.46.pth
BLEU = 74.55, 88.0/78.3/70.4/63.6 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.992.0.01-1.01.0.91-2.48.pth
BLEU = 73.89, 87.7/77.9/69.7/62.6 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.993.0.02-1.02.0.92-2.50.pth
BLEU = 74.61, 88.0/78.4/70.5/63.6 (BP=1.000, ratio=1.029, hyp_len=23843, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.994.0.01-1.01.0.88-2.41.pth
BLEU = 74.41, 87.9/78.2/70.3/63.4 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.995.0.02-1.02.0.90-2.45.pth
BLEU = 73.98, 87.8/77.9/69.8/62.7 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.996.0.01-1.01.0.93-2.54.pth
BLEU = 73.96, 87.7/77.9/69.8/62.7 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.997.0.02-1.02.0.92-2.51.pth
BLEU = 74.33, 87.8/78.2/70.3/63.3 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.998.0.02-1.02.0.92-2.52.pth
BLEU = 73.96, 87.7/77.8/69.8/62.9 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.999.0.03-1.03.0.93-2.54.pth
BLEU = 74.25, 87.9/78.2/70.1/63.1 (BP=1.000, ratio=1.030, hyp_len=23858, ref_len=23160)

real	220m53.433s
user	216m10.275s
sys	11m57.355s
```

BLEU score 75. ကျော်တာ ၁၂ ခုတွေ့ရပြီး အဲဒီအထဲကမှ အများဆုံးက 75.27 ဆိုတော့ baseline ကို မကျော်သေးဘူး...  

```
Evaluation result for the model: seq-rl-model-myrk.386.0.02-1.02.0.69-1.99.pth
BLEU = 75.27, 88.2/78.8/71.3/64.8 (BP=1.000, ratio=1.029, hyp_len=23833, ref_len=23160)
```

လက်ရှိ မော်ဒယ်ကို backup ကူးထည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq$ mv seq-rl-model-myrk.386.0.02-1.02.0.69-1.99.pth ./bk/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq$ mv seq-rl-model-myrk.386.0.02-1.02.0.69-1.99.pth.hyp ./bk/
```



## ERROR Example of RL Training

RL model ကို epoch များများ ပေးကြည့်မယ် ဆိုပြီး run ခဲ့ပေမဲ့ နောက်ပိုင်းမှ ပြဿနာကို ရှာတွေ့တာ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth --model_fn ./model/rl/seq-rl-model-myrk.pth --init_epoch 96 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 200
...
...
...
Validation - loss=7.0540e-01 ppl=2.02 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 190 - |param|=7.62e+02 |g_param|=2.80e+04 loss=4.8479e-02 ppl=1.05                                                
Validation - loss=7.0425e-01 ppl=2.02 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 191 - |param|=7.62e+02 |g_param|=2.97e+04 loss=4.7601e-02 ppl=1.05                                                
Validation - loss=6.6596e-01 ppl=1.95 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 192 - |param|=7.63e+02 |g_param|=2.72e+04 loss=4.3376e-02 ppl=1.04                                                
Validation - loss=6.8780e-01 ppl=1.99 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 193 - |param|=7.63e+02 |g_param|=3.00e+04 loss=4.5524e-02 ppl=1.05                                                
Validation - loss=7.1904e-01 ppl=2.05 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 194 - |param|=7.63e+02 |g_param|=3.83e+04 loss=3.1248e-02 ppl=1.03                                                
Validation - loss=7.2313e-01 ppl=2.06 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 195 - |param|=7.63e+02 |g_param|=3.45e+04 loss=2.7397e-02 ppl=1.03                                                
Validation - loss=7.0398e-01 ppl=2.02 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 196 - |param|=7.63e+02 |g_param|=2.97e+04 loss=3.3867e-02 ppl=1.03                                                
Validation - loss=7.0452e-01 ppl=2.02 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 197 - |param|=7.64e+02 |g_param|=2.61e+04 loss=4.5395e-02 ppl=1.05                                                
Validation - loss=6.9566e-01 ppl=2.01 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 198 - |param|=7.64e+02 |g_param|=3.00e+04 loss=4.6852e-02 ppl=1.05                                                
Validation - loss=6.6519e-01 ppl=1.94 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 199 - |param|=7.65e+02 |g_param|=2.25e+04 loss=4.2447e-02 ppl=1.04                                                
Validation - loss=6.9099e-01 ppl=2.00 best_loss=6.4219e-01 best_ppl=1.90                                                
Epoch 200 - |param|=7.65e+02 |g_param|=2.70e+04 loss=4.4714e-02 ppl=1.05                                                
Validation - loss=7.1278e-01 ppl=2.04 best_loss=6.4219e-01 best_ppl=1.90                                                

real	23m15.763s
user	22m57.277s
sys	0m17.367s

```

Testing ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python translate.py --model_fn ./model/rl/seq-rl-model-myrk.200.0.04-1.05.0.71-2.04.pth --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./model/rl/seq-rl-model-myrk.200.0.04-1.05.0.71-2.04.pth.hyp

real	0m20.792s
user	0m18.621s
sys	0m1.448s
```

Evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ cat ./model/rl/seq-rl-model-myrk.200.0.04-1.05.0.71-2.04.pth.hyp | perl ./test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
BLEU = 73.68, 87.5/77.6/69.5/62.5 (BP=1.000, ratio=1.030, hyp_len=23861, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt$
```

ရလဒ်က တက်မလာခဲ့တာကို ပြန်သတိထားမိမှ မသင်္ကာလို့ ဘာမှားခဲ့တာလဲ ဆိုတော့ ...  

```
--init_epoch 96 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 200
```

init ကို 96 က စထားတာက မှားတယ်။  
အကြောင်းအရင်းက မော်ဒယ် နာမည်က အောက်ပါအတိုင်း...  

```
seq-model-myrk2.321.0.05-1.05.0.67-1.96.pth  
```

321 က စ ရမယ်။ ခက်တာက အဲဒီလို setting ထားပြီးတော့ --n_epochs ကို 100 ထားရင် run မပေးဘူး...  
တကယ်မှန်ကန်တဲ့ setting အနေနဲ့က အောက်ပါအတိုင်း ဖြစ်ရမယ်...  

```
--init_epoch 321 နဲ့ --n_epochs 421
```

## Try to Load joey-nmt model

joey-nmt နဲ့ ဆောက်ထားတဲ့ မော်ဒယ်ကို baseline ထားပြီး continue_train လုပ်ကြည့်ခဲ့ပေမဲ့ မော်ဒယ်ကို load လုပ်တဲ့ နေရာမှာ ERROR ပေး...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn /home/ye/exp/joeynmt/models/wmt_myrk_default1/5000.pth --model_fn ./model/rl/seq-rl-joey-model-myrk.pth --init_epoch 30 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 100
Traceback (most recent call last):
  File "continue_train.py", line 55, in <module>
    continue_main(config, main)
  File "continue_train.py", line 42, in continue_main
    prev_config = saved_data['config']
KeyError: 'config'

real	0m0.874s
user	0m0.728s
sys	0m0.748s
(simple-nmt) ye@:~/exp/simple-nmt$
```

ငါအချိန်ရတဲ့အခါမှ source code ဖတ်ပြီး debug လုပ်ရန်...  

## Training Transformer for my-rk

python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
 --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 128 --n_epochs 30 --max_length 100 --dropout .2 \
--hidden_size 768 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 \
--lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
--model_fn ./model/transformer/myrk-transformer-model.pth

training လုပ်ကြည့်တော့ memory မနိုင်တဲ့ error ပေးတယ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
>  --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
> --gpu_id 0 --batch_size 128 --n_epochs 30 --max_length 100 --dropout .2 \
> --hidden_size 768 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 \
> --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
> --model_fn ./model/transformer/myrk-transformer-model.pth
{   'batch_size': 128,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 768,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/myrk-transformer-model.pth',
    'n_epochs': 30,
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
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/myrk-transformer/data/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1585, 768)
  (emb_dec): Embedding(1695, 768)
  (emb_dropout): Dropout(p=0.2, inplace=False)
  (encoder): MySequential(
    (0): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (decoder): MySequential(
    (0): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=768, out_features=768, bias=False)
        (K_linear): Linear(in_features=768, out_features=768, bias=False)
        (V_linear): Linear(in_features=768, out_features=768, bias=False)
        (linear): Linear(in_features=768, out_features=768, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=768, out_features=3072, bias=True)
        (1): ReLU()
        (2): Linear(in_features=3072, out_features=768, bias=True)
      )
      (fc_norm): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (generator): Sequential(
    (0): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=768, out_features=1695, bias=True)
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
Current run is terminating due to exception: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 465.47 MiB already allocated; 108.38 MiB free; 474.00 MiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
Engine run is terminating due to exception: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 465.47 MiB already allocated; 108.38 MiB free; 474.00 MiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
Traceback (most recent call last):
  File "train.py", line 361, in <module>
    main(config)
  File "train.py", line 340, in main
    lr_scheduler=lr_scheduler,
  File "/home/ye/exp/simple-nmt/simple_nmt/trainer.py", line 311, in train
    train_engine.run(train_loader, max_epochs=n_epochs)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 704, in run
    return self._internal_run()
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 783, in _internal_run
    self._handle_exception(e)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 466, in _handle_exception
    raise e
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 753, in _internal_run
    time_taken = self._run_once_on_dataset()
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 854, in _run_once_on_dataset
    self._handle_exception(e)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 466, in _handle_exception
    raise e
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/ignite/engine/engine.py", line 840, in _run_once_on_dataset
    self.state.output = self._process_function(self, self.state.batch)
  File "/home/ye/exp/simple-nmt/simple_nmt/trainer.py", line 62, in train
    y_hat = engine.model(x, mini_batch.tgt[0][:, :-1])
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/simple-nmt/simple_nmt/models/transformer.py", line 368, in forward
    h = self.emb_dropout(self._position_encoding(self.emb_dec(y)))
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/nn/modules/sparse.py", line 160, in forward
    self.norm_type, self.scale_grad_by_freq, self.sparse)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/nn/functional.py", line 2044, in embedding
    return torch.embedding(weight, input, padding_idx, scale_grad_by_freq, sparse)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 465.47 MiB already allocated; 108.38 MiB free; 474.00 MiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
(simple-nmt) ye@:~/exp/simple-nmt$ 

```

batch_size နဲ့ hidden_size ကို လျှော့ n_layers ကိုလည်း လျှော့တာတွေ လုပ်ကြည့်ပြီး အောက်ပါ config နဲ့မှ စ training လုပ်နိုင်တယ်...  

```
python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
 --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 \
--hidden_size 32 --n_layers 2 --max_grad_norm 1e+8 --iteration_per_update 32 \
--lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
--model_fn ./model/transformer/myrk-transformer-model.pth
```

training Transformer model with simple-nmt:  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
>  --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
> --gpu_id 0 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 \
> --hidden_size 32 --n_layers 2 --max_grad_norm 1e+8 --iteration_per_update 32 \
> --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
> --model_fn ./model/transformer/myrk-transformer-model.pth
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
    'model_fn': './model/transformer/myrk-transformer-model.pth',
    'n_epochs': 30,
    'n_layers': 2,
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
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/myrk-transformer/data/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1585, 32)
  (emb_dec): Embedding(1695, 32)
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
  )
  (generator): Sequential(
    (0): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=32, out_features=1695, bias=True)
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
Epoch 1 - |param|=3.28e+02 |g_param|=3.28e+05 loss=5.7089e+00 ppl=301.53                                                
Validation - loss=5.4560e+00 ppl=234.15 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.28e+02 |g_param|=2.85e+05 loss=4.7506e+00 ppl=115.65                                                
Validation - loss=4.5537e+00 ppl=94.99 best_loss=5.4560e+00 best_ppl=234.15                                             
Epoch 3 - |param|=3.28e+02 |g_param|=1.90e+05 loss=4.3546e+00 ppl=77.83                                                 
Validation - loss=4.1811e+00 ppl=65.44 best_loss=4.5537e+00 best_ppl=94.99                                              
Epoch 4 - |param|=3.28e+02 |g_param|=1.43e+05 loss=4.0684e+00 ppl=58.46                                                 
Validation - loss=3.9404e+00 ppl=51.44 best_loss=4.1811e+00 best_ppl=65.44                                              
Epoch 5 - |param|=3.28e+02 |g_param|=1.19e+05 loss=3.8762e+00 ppl=48.24                                                 
Validation - loss=3.7352e+00 ppl=41.90 best_loss=3.9404e+00 best_ppl=51.44                                              
Epoch 6 - |param|=3.28e+02 |g_param|=1.01e+05 loss=3.7073e+00 ppl=40.74                                                 
Validation - loss=3.5689e+00 ppl=35.48 best_loss=3.7352e+00 best_ppl=41.90                                              
Epoch 7 - |param|=3.28e+02 |g_param|=1.02e+05 loss=3.5567e+00 ppl=35.05                                                 
Validation - loss=3.4268e+00 ppl=30.78 best_loss=3.5689e+00 best_ppl=35.48                                              
Epoch 8 - |param|=3.28e+02 |g_param|=9.75e+04 loss=3.4226e+00 ppl=30.65                                                 
Validation - loss=3.2962e+00 ppl=27.01 best_loss=3.4268e+00 best_ppl=30.78                                              
Epoch 9 - |param|=3.28e+02 |g_param|=1.21e+05 loss=3.3298e+00 ppl=27.93                                                 
Validation - loss=3.1845e+00 ppl=24.16 best_loss=3.2962e+00 best_ppl=27.01                                              
Epoch 10 - |param|=3.28e+02 |g_param|=1.38e+05 loss=3.1712e+00 ppl=23.84                                                
Validation - loss=3.0895e+00 ppl=21.97 best_loss=3.1845e+00 best_ppl=24.16                                              
Epoch 11 - |param|=3.28e+02 |g_param|=1.29e+05 loss=3.1249e+00 ppl=22.76                                                
Validation - loss=2.9979e+00 ppl=20.04 best_loss=3.0895e+00 best_ppl=21.97                                              
Epoch 12 - |param|=3.28e+02 |g_param|=1.27e+05 loss=3.0109e+00 ppl=20.31                                                
Validation - loss=2.9006e+00 ppl=18.18 best_loss=2.9979e+00 best_ppl=20.04                                              
Epoch 13 - |param|=3.29e+02 |g_param|=1.34e+05 loss=2.9465e+00 ppl=19.04                                                
Validation - loss=2.8165e+00 ppl=16.72 best_loss=2.9006e+00 best_ppl=18.18                                              
Epoch 14 - |param|=3.29e+02 |g_param|=1.46e+05 loss=2.8337e+00 ppl=17.01                                                
Validation - loss=2.7453e+00 ppl=15.57 best_loss=2.8165e+00 best_ppl=16.72                                              
Epoch 15 - |param|=3.29e+02 |g_param|=1.46e+05 loss=2.7822e+00 ppl=16.15                                                
Validation - loss=2.6877e+00 ppl=14.70 best_loss=2.7453e+00 best_ppl=15.57                                              
Epoch 16 - |param|=3.29e+02 |g_param|=1.44e+05 loss=2.7334e+00 ppl=15.39                                                
Validation - loss=2.6151e+00 ppl=13.67 best_loss=2.6877e+00 best_ppl=14.70                                              
Epoch 17 - |param|=3.29e+02 |g_param|=1.55e+05 loss=2.6705e+00 ppl=14.45                                                
Validation - loss=2.5533e+00 ppl=12.85 best_loss=2.6151e+00 best_ppl=13.67                                              
Epoch 18 - |param|=3.29e+02 |g_param|=2.10e+05 loss=2.6178e+00 ppl=13.71                                                
Validation - loss=2.5077e+00 ppl=12.28 best_loss=2.5533e+00 best_ppl=12.85                                              
Epoch 19 - |param|=3.29e+02 |g_param|=1.86e+05 loss=2.5749e+00 ppl=13.13                                                
Validation - loss=2.4623e+00 ppl=11.73 best_loss=2.5077e+00 best_ppl=12.28                                              
Epoch 20 - |param|=3.29e+02 |g_param|=1.87e+05 loss=2.5507e+00 ppl=12.82                                                
Validation - loss=2.4146e+00 ppl=11.19 best_loss=2.4623e+00 best_ppl=11.73                                              
Epoch 21 - |param|=3.29e+02 |g_param|=1.83e+05 loss=2.4799e+00 ppl=11.94                                                
Validation - loss=2.3663e+00 ppl=10.66 best_loss=2.4146e+00 best_ppl=11.19                                              
Epoch 22 - |param|=3.29e+02 |g_param|=2.15e+05 loss=2.4337e+00 ppl=11.40                                                
Validation - loss=2.3508e+00 ppl=10.49 best_loss=2.3663e+00 best_ppl=10.66                                              
Epoch 23 - |param|=3.29e+02 |g_param|=1.69e+05 loss=2.3931e+00 ppl=10.95                                                
Validation - loss=2.2937e+00 ppl=9.91 best_loss=2.3508e+00 best_ppl=10.49                                               
Epoch 24 - |param|=3.29e+02 |g_param|=1.97e+05 loss=2.3497e+00 ppl=10.48                                                
Validation - loss=2.2567e+00 ppl=9.55 best_loss=2.2937e+00 best_ppl=9.91                                                
Epoch 25 - |param|=3.29e+02 |g_param|=1.96e+05 loss=2.3503e+00 ppl=10.49                                                
Validation - loss=2.2118e+00 ppl=9.13 best_loss=2.2567e+00 best_ppl=9.55                                                
Epoch 26 - |param|=3.29e+02 |g_param|=1.96e+05 loss=2.3258e+00 ppl=10.23                                                
Validation - loss=2.1814e+00 ppl=8.86 best_loss=2.2118e+00 best_ppl=9.13                                                
Epoch 27 - |param|=3.29e+02 |g_param|=2.33e+05 loss=2.2605e+00 ppl=9.59                                                 
Validation - loss=2.1539e+00 ppl=8.62 best_loss=2.1814e+00 best_ppl=8.86                                                
Epoch 28 - |param|=3.29e+02 |g_param|=2.10e+05 loss=2.1593e+00 ppl=8.67                                                 
Validation - loss=2.0917e+00 ppl=8.10 best_loss=2.1539e+00 best_ppl=8.62                                                
Epoch 29 - |param|=3.29e+02 |g_param|=2.63e+05 loss=2.1716e+00 ppl=8.77                                                 
Validation - loss=2.0944e+00 ppl=8.12 best_loss=2.0917e+00 best_ppl=8.10                                                
Epoch 30 - |param|=3.29e+02 |g_param|=2.19e+05 loss=2.1480e+00 ppl=8.57                                                 
Validation - loss=2.0422e+00 ppl=7.71 best_loss=2.0917e+00 best_ppl=8.10                                                
(simple-nmt) ye@:~/exp/simple-nmt$
```

shell script ကို update လုပ်ပြီး evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.71-301.53.5.46-234.15.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 32.8/0.0/0.0/0.0 (BP=0.154, ratio=0.348, hyp_len=8071, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.4.75-115.65.4.55-94.99.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.9/2.0/0.0/0.0 (BP=0.419, ratio=0.535, hyp_len=12389, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.35-77.83.4.18-65.44.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 31.8/6.1/0.1/0.0 (BP=0.757, ratio=0.782, hyp_len=18119, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.07-58.46.3.94-51.44.pth
BLEU = 0.70, 27.1/5.9/0.3/0.0 (BP=0.771, ratio=0.794, hyp_len=18386, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.3.88-48.24.3.74-41.90.pth
BLEU = 2.63, 26.1/7.3/1.0/0.3 (BP=0.986, ratio=0.986, hyp_len=22837, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.71-40.74.3.57-35.48.pth
BLEU = 2.10, 17.0/5.4/1.1/0.2 (BP=1.000, ratio=1.638, hyp_len=37943, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.56-35.05.3.43-30.78.pth
BLEU = 1.97, 14.1/4.6/1.0/0.2 (BP=1.000, ratio=2.134, hyp_len=49432, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.42-30.65.3.30-27.01.pth
BLEU = 1.94, 12.7/4.3/1.1/0.2 (BP=1.000, ratio=2.568, hyp_len=59483, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.33-27.93.3.18-24.16.pth
BLEU = 2.66, 15.4/5.5/1.4/0.4 (BP=1.000, ratio=2.237, hyp_len=51815, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.17-23.84.3.09-21.97.pth
BLEU = 3.43, 18.8/6.9/1.9/0.6 (BP=1.000, ratio=1.936, hyp_len=44829, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.12-22.76.3.00-20.04.pth
BLEU = 4.31, 20.9/8.1/2.5/0.8 (BP=1.000, ratio=1.850, hyp_len=42845, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.01-20.31.2.90-18.18.pth
BLEU = 6.46, 28.1/11.5/3.9/1.4 (BP=1.000, ratio=1.456, hyp_len=33716, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.2.95-19.04.2.82-16.72.pth
BLEU = 8.65, 34.0/14.6/5.4/2.1 (BP=1.000, ratio=1.255, hyp_len=29069, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.83-17.01.2.75-15.57.pth
BLEU = 10.23, 37.4/16.7/6.6/2.6 (BP=1.000, ratio=1.181, hyp_len=27358, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.78-16.15.2.69-14.70.pth
BLEU = 10.32, 36.4/16.6/6.8/2.8 (BP=1.000, ratio=1.251, hyp_len=28975, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.73-15.39.2.62-13.67.pth
BLEU = 13.20, 43.2/20.6/9.0/3.8 (BP=1.000, ratio=1.085, hyp_len=25118, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.67-14.45.2.55-12.85.pth
BLEU = 13.11, 41.4/20.2/9.1/3.9 (BP=1.000, ratio=1.161, hyp_len=26878, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.62-13.71.2.51-12.28.pth
BLEU = 15.81, 46.9/23.5/11.1/5.1 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.57-13.13.2.46-11.73.pth
BLEU = 14.74, 43.8/22.1/10.4/4.7 (BP=1.000, ratio=1.138, hyp_len=26353, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.55-12.82.2.41-11.19.pth
BLEU = 16.64, 47.4/24.5/11.9/5.6 (BP=1.000, ratio=1.070, hyp_len=24792, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.48-11.94.2.37-10.66.pth
BLEU = 18.20, 49.5/26.2/13.2/6.4 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.43-11.40.2.35-10.49.pth
BLEU = 17.80, 48.4/25.7/13.0/6.2 (BP=1.000, ratio=1.092, hyp_len=25282, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.39-10.95.2.29-9.91.pth
BLEU = 19.66, 51.5/27.9/14.4/7.2 (BP=1.000, ratio=1.036, hyp_len=24004, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.35-10.48.2.26-9.55.pth
BLEU = 19.93, 50.8/27.9/14.7/7.6 (BP=1.000, ratio=1.075, hyp_len=24907, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.35-10.49.2.21-9.13.pth
BLEU = 21.75, 53.7/30.0/16.2/8.6 (BP=1.000, ratio=1.030, hyp_len=23856, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.33-10.23.2.18-8.86.pth
BLEU = 22.06, 53.3/30.2/16.6/8.9 (BP=1.000, ratio=1.058, hyp_len=24493, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.26-9.59.2.15-8.62.pth
BLEU = 23.63, 55.2/31.9/17.9/9.9 (BP=1.000, ratio=1.042, hyp_len=24140, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.16-8.67.2.09-8.10.pth
BLEU = 25.46, 58.6/34.3/19.6/11.1 (BP=0.990, ratio=0.991, hyp_len=22940, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.17-8.77.2.09-8.12.pth
BLEU = 24.27, 55.6/32.5/18.5/10.4 (BP=1.000, ratio=1.064, hyp_len=24651, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.15-8.57.2.04-7.71.pth
BLEU = 26.37, 58.4/34.8/20.3/11.7 (BP=1.000, ratio=1.028, hyp_len=23811, ref_len=23160)

real	18m31.914s
user	18m10.704s
sys	0m35.898s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$
```

n_layers ကို 4 ထားပြီး epochs ကို 500 ထားပြီး နောက်တစ်ခေါက် ထပ် training လုပ်ခဲ့...  

python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
 --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 16 --n_epochs 500 --max_length 100 --dropout .2 \
--hidden_size 32 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 \
--lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
--model_fn ./model/transformer/myrk-transformer-model.pth  

```
(simple-nmt) ye@:~/exp/simple-nmt$ python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train  --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 500 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --model_fn ./model/transformer/myrk-transformer-model.pth
...
...
...
Validation - loss=5.8688e-01 ppl=1.80 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 432 - |param|=3.44e+02 |g_param|=1.24e+05 loss=4.7433e-01 ppl=1.61                                                
Validation - loss=5.7408e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 433 - |param|=3.44e+02 |g_param|=9.64e+04 loss=4.9410e-01 ppl=1.64                                                
Validation - loss=5.8105e-01 ppl=1.79 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 434 - |param|=3.44e+02 |g_param|=9.09e+04 loss=4.5806e-01 ppl=1.58                                                
Validation - loss=5.8170e-01 ppl=1.79 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 435 - |param|=3.44e+02 |g_param|=6.67e+04 loss=4.7692e-01 ppl=1.61                                                
Validation - loss=5.7447e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 436 - |param|=3.44e+02 |g_param|=1.05e+05 loss=4.6900e-01 ppl=1.60                                                
Validation - loss=5.8816e-01 ppl=1.80 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 437 - |param|=3.44e+02 |g_param|=7.88e+04 loss=4.5637e-01 ppl=1.58                                                
Validation - loss=5.7930e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 438 - |param|=3.44e+02 |g_param|=9.13e+04 loss=4.5348e-01 ppl=1.57                                                
Validation - loss=5.8138e-01 ppl=1.79 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 439 - |param|=3.44e+02 |g_param|=1.22e+05 loss=4.6535e-01 ppl=1.59                                                
Validation - loss=5.7734e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 440 - |param|=3.44e+02 |g_param|=2.11e+05 loss=4.8391e-01 ppl=1.62                                                
Validation - loss=5.8585e-01 ppl=1.80 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 441 - |param|=3.44e+02 |g_param|=1.21e+05 loss=4.8754e-01 ppl=1.63                                                
Validation - loss=5.7344e-01 ppl=1.77 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 442 - |param|=3.44e+02 |g_param|=3.07e+05 loss=4.6946e-01 ppl=1.60                                                
Validation - loss=5.8805e-01 ppl=1.80 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 443 - |param|=3.44e+02 |g_param|=1.30e+05 loss=4.9247e-01 ppl=1.64                                                
Validation - loss=5.7767e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 444 - |param|=3.44e+02 |g_param|=1.52e+05 loss=4.8234e-01 ppl=1.62                                                
Validation - loss=5.7610e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 445 - |param|=3.44e+02 |g_param|=2.23e+05 loss=4.8894e-01 ppl=1.63                                                
Validation - loss=5.8746e-01 ppl=1.80 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 446 - |param|=3.44e+02 |g_param|=1.68e+05 loss=4.9927e-01 ppl=1.65                                                
Validation - loss=5.7814e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 447 - |param|=3.45e+02 |g_param|=2.35e+05 loss=4.7725e-01 ppl=1.61                                                
Validation - loss=5.7937e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 448 - |param|=3.45e+02 |g_param|=1.71e+05 loss=4.9629e-01 ppl=1.64                                                
Validation - loss=5.7500e-01 ppl=1.78 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 449 - |param|=3.45e+02 |g_param|=1.95e+05 loss=4.5621e-01 ppl=1.58                                                
Validation - loss=5.8068e-01 ppl=1.79 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 450 - |param|=3.45e+02 |g_param|=1.71e+05 loss=4.3723e-01 ppl=1.55                                                
Validation - loss=5.6939e-01 ppl=1.77 best_loss=5.7001e-01 best_ppl=1.77                                                
Epoch 451 - |param|=3.45e+02 |g_param|=1.46e+05 loss=4.9131e-01 ppl=1.63                                                
Validation - loss=5.7076e-01 ppl=1.77 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 452 - |param|=3.45e+02 |g_param|=2.46e+05 loss=4.5393e-01 ppl=1.57                                                
Validation - loss=5.7735e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 453 - |param|=3.45e+02 |g_param|=2.09e+05 loss=4.7118e-01 ppl=1.60                                                
Validation - loss=5.7147e-01 ppl=1.77 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 454 - |param|=3.45e+02 |g_param|=1.20e+05 loss=4.8522e-01 ppl=1.62                                                
Validation - loss=5.7183e-01 ppl=1.77 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 455 - |param|=3.45e+02 |g_param|=1.66e+05 loss=4.8719e-01 ppl=1.63                                                
Validation - loss=5.7915e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 456 - |param|=3.45e+02 |g_param|=1.59e+05 loss=4.7685e-01 ppl=1.61                                                
Validation - loss=5.7990e-01 ppl=1.79 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 457 - |param|=3.45e+02 |g_param|=2.53e+05 loss=4.7739e-01 ppl=1.61                                                
Validation - loss=5.7655e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 458 - |param|=3.45e+02 |g_param|=1.10e+05 loss=4.5547e-01 ppl=1.58                                                
Validation - loss=5.7549e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 459 - |param|=3.45e+02 |g_param|=2.04e+05 loss=4.9499e-01 ppl=1.64                                                
Validation - loss=5.8718e-01 ppl=1.80 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 460 - |param|=3.45e+02 |g_param|=2.07e+05 loss=4.8656e-01 ppl=1.63                                                
Validation - loss=5.7765e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 461 - |param|=3.45e+02 |g_param|=2.32e+05 loss=4.8519e-01 ppl=1.62                                                
Validation - loss=5.7666e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 462 - |param|=3.45e+02 |g_param|=1.91e+05 loss=5.0903e-01 ppl=1.66                                                
Validation - loss=5.7745e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 463 - |param|=3.46e+02 |g_param|=2.05e+05 loss=4.9442e-01 ppl=1.64                                                
Validation - loss=5.8309e-01 ppl=1.79 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 464 - |param|=3.46e+02 |g_param|=1.56e+05 loss=4.7538e-01 ppl=1.61                                                
Validation - loss=5.7862e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 465 - |param|=3.46e+02 |g_param|=2.58e+05 loss=4.7323e-01 ppl=1.61                                                
Validation - loss=5.7001e-01 ppl=1.77 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 466 - |param|=3.46e+02 |g_param|=1.57e+05 loss=4.5506e-01 ppl=1.58                                                
Validation - loss=5.8122e-01 ppl=1.79 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 467 - |param|=3.46e+02 |g_param|=3.58e+05 loss=4.8396e-01 ppl=1.62                                                
Validation - loss=5.7548e-01 ppl=1.78 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 468 - |param|=3.46e+02 |g_param|=1.61e+05 loss=4.8746e-01 ppl=1.63                                                
Validation - loss=5.8273e-01 ppl=1.79 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 469 - |param|=3.46e+02 |g_param|=1.10e+05 loss=4.5314e-01 ppl=1.57                                                
Validation - loss=5.6770e-01 ppl=1.76 best_loss=5.6939e-01 best_ppl=1.77                                                
Epoch 470 - |param|=3.46e+02 |g_param|=2.17e+05 loss=4.2955e-01 ppl=1.54                                                
Validation - loss=5.8737e-01 ppl=1.80 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 471 - |param|=3.46e+02 |g_param|=2.37e+05 loss=4.8694e-01 ppl=1.63                                                
Validation - loss=5.9277e-01 ppl=1.81 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 472 - |param|=3.46e+02 |g_param|=1.45e+05 loss=4.6127e-01 ppl=1.59                                                
Validation - loss=5.7614e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 473 - |param|=3.46e+02 |g_param|=2.52e+05 loss=4.7518e-01 ppl=1.61                                                
Validation - loss=5.8019e-01 ppl=1.79 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 474 - |param|=3.46e+02 |g_param|=1.67e+05 loss=4.5077e-01 ppl=1.57                                                
Validation - loss=5.8194e-01 ppl=1.79 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 475 - |param|=3.46e+02 |g_param|=3.89e+05 loss=4.7479e-01 ppl=1.61                                                
Validation - loss=5.9290e-01 ppl=1.81 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 476 - |param|=3.46e+02 |g_param|=1.37e+05 loss=4.3526e-01 ppl=1.55                                                
Validation - loss=5.7422e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 477 - |param|=3.46e+02 |g_param|=2.65e+05 loss=4.9425e-01 ppl=1.64                                                
Validation - loss=5.7296e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 478 - |param|=3.46e+02 |g_param|=2.06e+05 loss=4.6831e-01 ppl=1.60                                                
Validation - loss=5.8319e-01 ppl=1.79 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 479 - |param|=3.47e+02 |g_param|=2.41e+05 loss=4.4763e-01 ppl=1.56                                                
Validation - loss=5.7528e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 480 - |param|=3.47e+02 |g_param|=1.48e+05 loss=4.6171e-01 ppl=1.59                                                
Validation - loss=5.7178e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 481 - |param|=3.47e+02 |g_param|=1.88e+05 loss=4.6442e-01 ppl=1.59                                                
Validation - loss=5.7531e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 482 - |param|=3.47e+02 |g_param|=1.82e+05 loss=4.6395e-01 ppl=1.59                                                
Validation - loss=5.6789e-01 ppl=1.76 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 483 - |param|=3.47e+02 |g_param|=1.54e+05 loss=4.7272e-01 ppl=1.60                                                
Validation - loss=5.7303e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 484 - |param|=3.47e+02 |g_param|=1.08e+05 loss=4.5241e-01 ppl=1.57                                                
Validation - loss=5.7211e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 485 - |param|=3.47e+02 |g_param|=6.26e+04 loss=4.3009e-01 ppl=1.54                                                
Validation - loss=5.7412e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 486 - |param|=3.47e+02 |g_param|=1.20e+05 loss=4.8299e-01 ppl=1.62                                                
Validation - loss=5.7857e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 487 - |param|=3.47e+02 |g_param|=6.04e+04 loss=4.7344e-01 ppl=1.61                                                
Validation - loss=5.7283e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 488 - |param|=3.47e+02 |g_param|=9.47e+04 loss=4.4521e-01 ppl=1.56                                                
Validation - loss=5.7738e-01 ppl=1.78 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 489 - |param|=3.47e+02 |g_param|=1.17e+05 loss=4.6967e-01 ppl=1.60                                                
Validation - loss=5.9618e-01 ppl=1.82 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 490 - |param|=3.47e+02 |g_param|=7.97e+04 loss=4.3066e-01 ppl=1.54                                                
Validation - loss=5.7236e-01 ppl=1.77 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 491 - |param|=3.47e+02 |g_param|=9.54e+04 loss=4.2107e-01 ppl=1.52                                                
Validation - loss=5.5975e-01 ppl=1.75 best_loss=5.6770e-01 best_ppl=1.76                                                
Epoch 492 - |param|=3.47e+02 |g_param|=1.41e+05 loss=4.7497e-01 ppl=1.61                                                
Validation - loss=5.7640e-01 ppl=1.78 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 493 - |param|=3.47e+02 |g_param|=8.59e+04 loss=4.4129e-01 ppl=1.55                                                
Validation - loss=5.7608e-01 ppl=1.78 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 494 - |param|=3.47e+02 |g_param|=7.50e+04 loss=4.6531e-01 ppl=1.59                                                
Validation - loss=5.7309e-01 ppl=1.77 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 495 - |param|=3.48e+02 |g_param|=9.18e+04 loss=4.4620e-01 ppl=1.56                                                
Validation - loss=5.8663e-01 ppl=1.80 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 496 - |param|=3.48e+02 |g_param|=6.18e+04 loss=4.8120e-01 ppl=1.62                                                
Validation - loss=5.6659e-01 ppl=1.76 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 497 - |param|=3.48e+02 |g_param|=9.98e+04 loss=4.6219e-01 ppl=1.59                                                
Validation - loss=5.7075e-01 ppl=1.77 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 498 - |param|=3.48e+02 |g_param|=1.03e+05 loss=4.8381e-01 ppl=1.62                                                
Validation - loss=5.6670e-01 ppl=1.76 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 499 - |param|=3.48e+02 |g_param|=9.24e+04 loss=4.5524e-01 ppl=1.58                                                
Validation - loss=5.7468e-01 ppl=1.78 best_loss=5.5975e-01 best_ppl=1.75                                                
Epoch 500 - |param|=3.48e+02 |g_param|=1.04e+05 loss=4.2693e-01 ppl=1.53                                                
Validation - loss=5.8161e-01 ppl=1.79 best_loss=5.5975e-01 best_ppl=1.75                                                
```

test-eval-loop.sh shell script ကို သိမ်းမယ့် ဖိုင်နာမည်ကို update လုပ်ခဲ့...  

```bash
#!/bin/bash

# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang myrk < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-myrk-transformer-baseline-500epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /media/ye/project2/exp/myrk-transformer/data/syl/test.rk | tee  -a eval-results-myrk-transformer-baseline-500epoch.txt

done

```

testing/evaluation လုပ်ပြီး BLEU score ဘယ်လောက်ထိ တက်လာသလဲ လေ့လာ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$ time ./test-eval-loop.sh 
...
...
...
Evaluation result for the model: myrk-transformer-model.55.1.35-3.86.1.04-2.83.pth
BLEU = 49.59, 75.1/57.0/43.3/32.7 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.56.1.39-4.01.1.05-2.87.pth
BLEU = 49.08, 74.6/56.8/42.8/32.0 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.57.1.31-3.71.1.05-2.86.pth
BLEU = 49.14, 74.2/56.7/43.0/32.3 (BP=1.000, ratio=1.053, hyp_len=24381, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.58.1.27-3.57.1.05-2.85.pth
BLEU = 48.26, 73.1/55.9/42.2/31.5 (BP=1.000, ratio=1.071, hyp_len=24796, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.59.1.31-3.72.1.02-2.77.pth
BLEU = 49.79, 74.4/57.1/43.7/33.1 (BP=1.000, ratio=1.056, hyp_len=24461, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.60.1.29-3.62.1.01-2.74.pth
BLEU = 50.44, 75.0/57.9/44.3/33.6 (BP=1.000, ratio=1.050, hyp_len=24314, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.61.1.27-3.55.0.99-2.69.pth
BLEU = 50.71, 75.2/58.3/44.6/33.8 (BP=1.000, ratio=1.046, hyp_len=24223, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.62.1.28-3.61.0.96-2.61.pth
BLEU = 53.25, 77.2/60.2/47.0/36.8 (BP=1.000, ratio=1.021, hyp_len=23641, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.63.1.21-3.36.0.99-2.68.pth
BLEU = 51.11, 75.6/58.7/45.0/34.2 (BP=1.000, ratio=1.049, hyp_len=24299, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.64.1.23-3.42.0.95-2.60.pth
BLEU = 52.64, 76.8/60.0/46.6/35.8 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.65.1.22-3.40.0.94-2.56.pth
BLEU = 52.70, 76.5/59.9/46.6/36.1 (BP=1.000, ratio=1.041, hyp_len=24114, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.66.1.29-3.64.0.93-2.55.pth
BLEU = 53.60, 77.3/60.7/47.5/37.1 (BP=1.000, ratio=1.025, hyp_len=23733, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.67.1.21-3.35.0.95-2.59.pth
BLEU = 52.08, 75.7/59.3/46.1/35.5 (BP=1.000, ratio=1.056, hyp_len=24464, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.68.1.24-3.46.0.95-2.58.pth
BLEU = 52.73, 76.8/60.1/46.7/35.9 (BP=1.000, ratio=1.043, hyp_len=24153, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.69.1.22-3.37.0.90-2.46.pth
BLEU = 54.15, 77.4/61.1/48.1/37.8 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.70.1.22-3.40.0.93-2.53.pth
BLEU = 53.75, 77.5/61.2/47.7/36.9 (BP=1.000, ratio=1.038, hyp_len=24033, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.71.1.17-3.22.0.92-2.52.pth
BLEU = 53.21, 76.9/60.6/47.2/36.5 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.72.1.12-3.07.0.90-2.47.pth
BLEU = 52.34, 75.4/59.5/46.5/36.0 (BP=1.000, ratio=1.070, hyp_len=24777, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.73.1.12-3.06.0.89-2.43.pth
BLEU = 53.07, 76.1/60.1/47.2/36.8 (BP=1.000, ratio=1.063, hyp_len=24624, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.74.1.15-3.16.0.88-2.41.pth
BLEU = 56.20, 78.8/62.9/50.2/40.1 (BP=1.000, ratio=1.022, hyp_len=23666, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.75.1.16-3.19.0.89-2.43.pth
BLEU = 54.04, 77.0/61.1/48.1/37.7 (BP=1.000, ratio=1.051, hyp_len=24350, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.76.1.19-3.29.0.90-2.46.pth
BLEU = 53.13, 76.3/60.3/47.2/36.7 (BP=1.000, ratio=1.063, hyp_len=24623, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.77.1.12-3.08.0.87-2.38.pth
BLEU = 57.25, 79.7/63.8/51.3/41.2 (BP=1.000, ratio=1.014, hyp_len=23486, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.78.1.09-2.96.0.88-2.40.pth
BLEU = 55.29, 78.0/62.3/49.4/38.9 (BP=1.000, ratio=1.041, hyp_len=24120, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.79.1.16-3.18.0.93-2.55.pth
BLEU = 51.85, 74.8/59.4/46.2/35.2 (BP=1.000, ratio=1.090, hyp_len=25251, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.80.1.09-2.97.0.85-2.35.pth
BLEU = 55.67, 78.1/62.5/49.9/39.5 (BP=1.000, ratio=1.049, hyp_len=24291, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.81.1.09-2.96.0.86-2.35.pth
BLEU = 54.42, 76.3/61.1/48.7/38.6 (BP=1.000, ratio=1.075, hyp_len=24887, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.82.1.11-3.03.0.85-2.34.pth
BLEU = 56.79, 78.8/63.4/51.0/40.9 (BP=1.000, ratio=1.040, hyp_len=24080, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.83.1.10-3.00.0.85-2.34.pth
BLEU = 56.85, 79.3/63.7/50.9/40.6 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.84.1.09-2.98.0.84-2.31.pth
BLEU = 58.74, 80.7/65.1/52.7/43.0 (BP=1.000, ratio=1.012, hyp_len=23439, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.85.1.08-2.94.0.86-2.37.pth
BLEU = 56.21, 78.7/63.3/50.4/39.8 (BP=1.000, ratio=1.040, hyp_len=24078, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.86.0.99-2.68.0.86-2.37.pth
BLEU = 57.26, 79.7/64.3/51.4/40.8 (BP=1.000, ratio=1.031, hyp_len=23871, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.87.1.07-2.93.0.84-2.31.pth
BLEU = 55.05, 77.2/62.0/49.4/38.9 (BP=1.000, ratio=1.069, hyp_len=24756, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.88.1.05-2.84.0.82-2.28.pth
BLEU = 57.85, 79.1/64.1/52.1/42.4 (BP=1.000, ratio=1.042, hyp_len=24133, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.89.1.02-2.78.0.83-2.29.pth
BLEU = 57.67, 79.3/64.4/52.0/41.7 (BP=1.000, ratio=1.044, hyp_len=24173, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.90.1.03-2.80.0.84-2.32.pth
BLEU = 55.04, 76.9/61.9/49.4/39.0 (BP=1.000, ratio=1.076, hyp_len=24910, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.91.1.00-2.72.0.83-2.30.pth
BLEU = 56.35, 78.3/63.2/50.6/40.2 (BP=1.000, ratio=1.053, hyp_len=24391, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.92.1.03-2.80.0.81-2.26.pth
BLEU = 59.06, 80.2/65.4/53.3/43.5 (BP=1.000, ratio=1.031, hyp_len=23870, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.93.0.98-2.67.0.81-2.24.pth
BLEU = 58.64, 79.7/64.8/52.9/43.3 (BP=1.000, ratio=1.038, hyp_len=24041, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.94.1.03-2.79.0.79-2.21.pth
BLEU = 57.92, 78.8/64.3/52.3/42.5 (BP=1.000, ratio=1.049, hyp_len=24302, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.95.0.96-2.60.0.83-2.28.pth
BLEU = 57.02, 78.3/63.8/51.4/41.2 (BP=1.000, ratio=1.059, hyp_len=24533, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.96.0.92-2.52.0.80-2.24.pth
BLEU = 58.66, 79.7/65.0/53.0/43.2 (BP=1.000, ratio=1.041, hyp_len=24100, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.97.0.94-2.56.0.80-2.22.pth
BLEU = 60.98, 81.7/67.0/55.2/45.7 (BP=1.000, ratio=1.012, hyp_len=23445, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.98.0.97-2.63.0.83-2.30.pth
BLEU = 57.04, 78.9/64.1/51.4/40.7 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.99.0.98-2.67.0.79-2.20.pth
BLEU = 57.49, 78.8/64.2/51.9/41.6 (BP=1.000, ratio=1.058, hyp_len=24500, ref_len=23160)

real	287m47.405s
user	272m48.280s
sys	12m37.769s
```

ဆက် training လုပ်ဖို့ လိုအပ်တယ်လို့ ယူဆတယ်...  
လေ့လာကြည့်တော့ training ကလည်း ရောက်နေပြီးသား epoch ကနေ ဆက် training လုပ်တာကို support လုပ်လို့ အတော်ပါပဲ...  

```
  --init_epoch INIT_EPOCH
                        Set initial epoch number, which can be useful in
                        continue training. Default=1

```

time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
 --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 16 --n_epochs 1000 --max_length 100 --dropout .2 \
--hidden_size 32 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 \
--lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
--init_epoch 500 \
--model_fn ./model/transformer/myrk-transformer-model.pth

epoch 1000 အထိ training လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train  --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 1000 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 500 --model_fn ./model/transformer/myrk-transformer-model.pth
...
...
...
Validation - loss=5.8572e-01 ppl=1.80 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 987 - |param|=3.49e+02 |g_param|=6.16e+04 loss=4.4124e-01 ppl=1.55                                                
Validation - loss=5.9191e-01 ppl=1.81 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 988 - |param|=3.49e+02 |g_param|=9.34e+04 loss=4.6972e-01 ppl=1.60                                                
Validation - loss=6.0779e-01 ppl=1.84 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 989 - |param|=3.49e+02 |g_param|=8.84e+04 loss=4.8799e-01 ppl=1.63                                                
Validation - loss=6.0236e-01 ppl=1.83 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 990 - |param|=3.49e+02 |g_param|=5.90e+04 loss=4.5021e-01 ppl=1.57                                                
Validation - loss=5.9618e-01 ppl=1.82 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 991 - |param|=3.49e+02 |g_param|=8.54e+04 loss=4.4378e-01 ppl=1.56                                                
Validation - loss=6.1863e-01 ppl=1.86 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 992 - |param|=3.49e+02 |g_param|=1.30e+05 loss=4.8649e-01 ppl=1.63                                                
Validation - loss=6.2275e-01 ppl=1.86 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 993 - |param|=3.49e+02 |g_param|=8.13e+04 loss=4.8138e-01 ppl=1.62                                                
Validation - loss=5.8946e-01 ppl=1.80 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 994 - |param|=3.50e+02 |g_param|=7.52e+04 loss=4.6172e-01 ppl=1.59                                                
Validation - loss=5.8569e-01 ppl=1.80 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 995 - |param|=3.50e+02 |g_param|=1.09e+05 loss=4.7565e-01 ppl=1.61                                                
Validation - loss=6.1411e-01 ppl=1.85 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 996 - |param|=3.50e+02 |g_param|=8.09e+04 loss=4.8715e-01 ppl=1.63                                                
Validation - loss=5.9161e-01 ppl=1.81 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 997 - |param|=3.50e+02 |g_param|=1.28e+05 loss=4.7410e-01 ppl=1.61                                                
Validation - loss=5.9515e-01 ppl=1.81 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 998 - |param|=3.50e+02 |g_param|=7.09e+04 loss=4.5065e-01 ppl=1.57                                                
Validation - loss=5.9033e-01 ppl=1.80 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 999 - |param|=3.50e+02 |g_param|=1.19e+05 loss=4.9994e-01 ppl=1.65                                                
Validation - loss=5.9936e-01 ppl=1.82 best_loss=5.8071e-01 best_ppl=1.79                                                
Epoch 1000 - |param|=3.50e+02 |g_param|=7.42e+04 loss=4.4498e-01 ppl=1.56                                               
Validation - loss=5.8277e-01 ppl=1.79 best_loss=5.8071e-01 best_ppl=1.79                                                

real	214m16.845s
user	212m14.025s
sys	0m44.360s
```

epoch 1000 အထိကို test/eval ထပ်လုပ် ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.1000.0.44-1.56.0.58-1.79.pth
BLEU = 69.38, 84.8/73.8/64.8/57.1 (BP=1.000, ratio=1.038, hyp_len=24046, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.501.4.67-106.66.4.52-91.84.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.2/0.7/0.0/0.0 (BP=0.458, ratio=0.562, hyp_len=13011, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.502.4.26-70.71.4.14-62.70.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.9/2.7/0.2/0.0 (BP=0.893, ratio=0.899, hyp_len=20812, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.503.3.98-53.57.3.85-46.83.pth
BLEU = 0.90, 15.6/3.6/0.5/0.0 (BP=1.000, ratio=1.716, hyp_len=39731, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.504.3.75-42.52.3.61-36.99.pth
BLEU = 1.81, 20.2/5.5/1.0/0.1 (BP=1.000, ratio=1.539, hyp_len=35638, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.505.3.60-36.60.3.42-30.66.pth
BLEU = 3.23, 25.0/8.1/1.8/0.3 (BP=1.000, ratio=1.344, hyp_len=31117, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.506.3.36-28.93.3.28-26.54.pth
BLEU = 4.42, 27.1/9.7/2.6/0.6 (BP=1.000, ratio=1.340, hyp_len=31031, ref_len=23160)
^Z
[5]+  Stopped                 ./test-eval-loop.sh

real	5m2.019s
user	0m0.000s
sys	0m0.001s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$
```

အထက်ပါအတိုင်း ဘာသွားတွေ့လဲ ဆိုတော့ epoch ကိုသာ ၅၀၁ က စပေမဲ့... တကယ်တမ်းက မော်ဒယ်ကို အသစ်ကနေ training လုပ်သွားတာကို တွေ့ရ...  
အဲဒါကြောင့် အခေါက် ၁၀၀၀ ကို နောက်တစ်ခေါက် epoch 1 ကနေ ပြန် run ခဲ့...  
ဒီတစ်ခါတော့ စက်ကို restart ပါ ပြန်လုပ်ခဲ့ပြီးတော့ --n_layers 6 အထိ တင်ပြီး training လုပ်ကြည့်ခဲ့...  

time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train \
 --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk \
--gpu_id 0 --batch_size 16 --n_epochs 1000 --max_length 100 --dropout .2 \
--hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 \
--lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 \
--init_epoch 1 \
--model_fn ./model/transformer/myrk-transformer-model.pth

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train  --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 1000 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/myrk-transformer-model.pth
...
...
...
Validation - loss=5.6086e-01 ppl=1.75 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 993 - |param|=3.92e+02 |g_param|=5.16e+04 loss=3.1570e-01 ppl=1.37                                                
Validation - loss=5.6344e-01 ppl=1.76 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 994 - |param|=3.92e+02 |g_param|=6.84e+04 loss=3.1980e-01 ppl=1.38                                                
Validation - loss=5.6576e-01 ppl=1.76 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 995 - |param|=3.92e+02 |g_param|=6.60e+04 loss=2.9123e-01 ppl=1.34                                                
Validation - loss=5.8111e-01 ppl=1.79 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 996 - |param|=3.92e+02 |g_param|=7.44e+04 loss=3.2001e-01 ppl=1.38                                                
Validation - loss=5.7921e-01 ppl=1.78 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 997 - |param|=3.92e+02 |g_param|=1.73e+05 loss=3.3958e-01 ppl=1.40                                                
Validation - loss=5.8741e-01 ppl=1.80 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 998 - |param|=3.92e+02 |g_param|=6.27e+04 loss=3.0256e-01 ppl=1.35                                                
Validation - loss=5.7504e-01 ppl=1.78 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 999 - |param|=3.92e+02 |g_param|=6.73e+04 loss=3.3306e-01 ppl=1.40                                                
Validation - loss=5.7471e-01 ppl=1.78 best_loss=5.5262e-01 best_ppl=1.74                                                
Epoch 1000 - |param|=3.92e+02 |g_param|=6.97e+04 loss=3.0069e-01 ppl=1.35                                               
Validation - loss=5.6837e-01 ppl=1.77 best_loss=5.5262e-01 best_ppl=1.74                                                

real	608m57.979s
user	607m34.593s
sys	1m3.578s
```

testing/evaluation and finding the highest BLEU score ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer$ time ./test-eval-loop.sh 
...
...
...
BLEU = 69.87, 85.0/74.3/65.4/57.8 (BP=1.000, ratio=1.049, hyp_len=24299, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.892.0.30-1.36.0.58-1.79.pth
BLEU = 71.51, 86.2/75.7/67.1/59.8 (BP=1.000, ratio=1.035, hyp_len=23979, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.893.0.31-1.36.0.57-1.77.pth
BLEU = 72.18, 86.4/76.2/67.8/60.8 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.894.0.31-1.37.0.55-1.74.pth
BLEU = 71.52, 86.0/75.6/67.1/59.9 (BP=1.000, ratio=1.040, hyp_len=24077, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.895.0.31-1.36.0.56-1.75.pth
BLEU = 71.29, 86.0/75.4/66.8/59.6 (BP=1.000, ratio=1.041, hyp_len=24102, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.896.0.33-1.39.0.57-1.76.pth
BLEU = 70.97, 85.7/75.2/66.5/59.1 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.897.0.32-1.37.0.58-1.78.pth
BLEU = 70.95, 85.8/75.2/66.5/59.1 (BP=1.000, ratio=1.044, hyp_len=24176, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.898.0.32-1.38.0.57-1.77.pth
BLEU = 71.89, 86.4/75.9/67.5/60.3 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.899.0.33-1.40.0.56-1.76.pth
BLEU = 71.47, 86.0/75.5/67.0/59.9 (BP=1.000, ratio=1.041, hyp_len=24104, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.900.0.30-1.35.0.60-1.82.pth
BLEU = 71.88, 86.2/75.9/67.5/60.4 (BP=1.000, ratio=1.034, hyp_len=23959, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.90.0.96-2.61.0.78-2.18.pth
BLEU = 57.28, 79.1/64.2/51.6/41.1 (BP=1.000, ratio=1.057, hyp_len=24474, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.901.0.34-1.41.0.57-1.78.pth
BLEU = 71.83, 86.2/75.9/67.4/60.3 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.902.0.34-1.40.0.58-1.78.pth
BLEU = 69.99, 85.2/74.4/65.5/57.9 (BP=1.000, ratio=1.049, hyp_len=24300, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.903.0.34-1.40.0.57-1.76.pth
BLEU = 71.54, 86.1/75.6/67.1/60.0 (BP=1.000, ratio=1.038, hyp_len=24029, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.904.0.31-1.37.0.59-1.80.pth
BLEU = 71.34, 86.0/75.5/66.9/59.7 (BP=1.000, ratio=1.038, hyp_len=24034, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.905.0.33-1.39.0.57-1.77.pth
BLEU = 70.56, 85.5/74.9/66.1/58.6 (BP=1.000, ratio=1.044, hyp_len=24177, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.906.0.33-1.39.0.59-1.80.pth
BLEU = 70.02, 85.2/74.5/65.5/57.8 (BP=1.000, ratio=1.051, hyp_len=24333, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.907.0.33-1.39.0.57-1.77.pth
BLEU = 71.39, 86.1/75.5/66.9/59.7 (BP=1.000, ratio=1.038, hyp_len=24040, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.908.0.31-1.37.0.57-1.77.pth
BLEU = 71.56, 86.1/75.6/67.1/60.0 (BP=1.000, ratio=1.038, hyp_len=24030, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.909.0.32-1.38.0.58-1.79.pth
BLEU = 71.92, 86.3/76.0/67.6/60.4 (BP=1.000, ratio=1.038, hyp_len=24043, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.910.0.31-1.36.0.58-1.78.pth
BLEU = 71.79, 86.2/75.9/67.4/60.2 (BP=1.000, ratio=1.037, hyp_len=24012, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.91.0.96-2.60.0.76-2.13.pth
BLEU = 59.42, 80.2/65.3/53.7/44.3 (BP=1.000, ratio=1.036, hyp_len=23987, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.911.0.30-1.36.0.57-1.77.pth
BLEU = 70.97, 85.6/75.1/66.5/59.3 (BP=1.000, ratio=1.043, hyp_len=24165, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.912.0.34-1.40.0.58-1.79.pth
BLEU = 71.44, 86.1/75.6/67.0/59.7 (BP=1.000, ratio=1.040, hyp_len=24081, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.913.0.36-1.44.0.57-1.77.pth
BLEU = 72.30, 86.5/76.2/68.0/61.0 (BP=1.000, ratio=1.031, hyp_len=23886, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.914.0.32-1.38.0.56-1.75.pth
BLEU = 72.37, 86.6/76.3/68.0/61.0 (BP=1.000, ratio=1.034, hyp_len=23957, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.915.0.33-1.39.0.58-1.79.pth
BLEU = 71.22, 86.0/75.4/66.7/59.5 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.916.0.34-1.40.0.57-1.76.pth
BLEU = 71.69, 86.1/75.7/67.3/60.2 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.917.0.31-1.37.0.56-1.76.pth
BLEU = 71.95, 86.2/75.9/67.6/60.6 (BP=1.000, ratio=1.037, hyp_len=24020, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.918.0.32-1.38.0.59-1.80.pth
BLEU = 70.51, 85.5/74.8/66.0/58.5 (BP=1.000, ratio=1.043, hyp_len=24156, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.919.0.33-1.38.0.57-1.77.pth
BLEU = 71.18, 86.0/75.4/66.7/59.4 (BP=1.000, ratio=1.042, hyp_len=24122, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.920.0.30-1.35.0.58-1.78.pth
BLEU = 71.53, 85.9/75.5/67.2/60.1 (BP=1.000, ratio=1.040, hyp_len=24094, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.92.0.95-2.59.0.77-2.17.pth
BLEU = 59.13, 80.5/65.3/53.3/43.6 (BP=1.000, ratio=1.028, hyp_len=23804, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.921.0.34-1.40.0.57-1.76.pth
BLEU = 72.46, 86.6/76.4/68.1/61.1 (BP=1.000, ratio=1.037, hyp_len=24011, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.922.0.34-1.41.0.58-1.79.pth
BLEU = 71.19, 85.9/75.3/66.7/59.5 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.923.0.31-1.36.0.58-1.78.pth
BLEU = 71.06, 85.8/75.2/66.6/59.3 (BP=1.000, ratio=1.042, hyp_len=24143, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.924.0.31-1.36.0.58-1.78.pth
BLEU = 71.24, 85.9/75.3/66.8/59.6 (BP=1.000, ratio=1.039, hyp_len=24058, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.925.0.32-1.37.0.57-1.77.pth
BLEU = 71.26, 86.0/75.4/66.8/59.5 (BP=1.000, ratio=1.040, hyp_len=24085, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.926.0.33-1.39.0.58-1.78.pth
BLEU = 71.10, 85.8/75.3/66.6/59.4 (BP=1.000, ratio=1.042, hyp_len=24126, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.927.0.30-1.35.0.58-1.79.pth
BLEU = 71.03, 85.9/75.3/66.5/59.2 (BP=1.000, ratio=1.039, hyp_len=24069, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.928.0.33-1.39.0.58-1.79.pth
BLEU = 71.38, 86.0/75.5/66.9/59.7 (BP=1.000, ratio=1.037, hyp_len=24009, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.929.0.32-1.37.0.58-1.79.pth
BLEU = 71.34, 86.2/75.6/66.8/59.5 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.930.0.31-1.37.0.56-1.75.pth
BLEU = 71.34, 85.8/75.4/66.9/59.8 (BP=1.000, ratio=1.042, hyp_len=24131, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.93.0.88-2.42.0.76-2.14.pth
BLEU = 57.96, 78.9/64.2/52.3/42.6 (BP=1.000, ratio=1.061, hyp_len=24564, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.931.0.33-1.39.0.60-1.82.pth
BLEU = 72.16, 86.6/76.1/67.7/60.8 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.932.0.34-1.40.0.57-1.76.pth
BLEU = 71.85, 86.2/75.8/67.4/60.5 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.933.0.33-1.39.0.56-1.76.pth
BLEU = 71.59, 86.2/75.7/67.2/59.9 (BP=1.000, ratio=1.040, hyp_len=24085, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.934.0.32-1.38.0.56-1.76.pth
BLEU = 71.55, 86.1/75.6/67.1/59.9 (BP=1.000, ratio=1.035, hyp_len=23979, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.935.0.34-1.40.0.57-1.77.pth
BLEU = 71.68, 86.2/75.8/67.2/60.1 (BP=1.000, ratio=1.038, hyp_len=24047, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.936.0.33-1.39.0.57-1.77.pth
BLEU = 71.92, 86.3/75.9/67.5/60.5 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.937.0.31-1.36.0.57-1.77.pth
BLEU = 72.03, 86.4/76.0/67.6/60.6 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.938.0.30-1.35.0.56-1.75.pth
BLEU = 71.28, 86.0/75.4/66.8/59.6 (BP=1.000, ratio=1.039, hyp_len=24063, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.939.0.31-1.37.0.57-1.76.pth
BLEU = 71.46, 86.0/75.5/67.0/60.0 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.940.0.35-1.41.0.57-1.77.pth
BLEU = 71.61, 86.0/75.6/67.2/60.1 (BP=1.000, ratio=1.039, hyp_len=24068, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.94.0.90-2.46.0.75-2.12.pth
BLEU = 59.34, 80.2/65.5/53.7/44.0 (BP=1.000, ratio=1.042, hyp_len=24139, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.941.0.33-1.39.0.58-1.79.pth
BLEU = 71.96, 86.5/76.0/67.5/60.4 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.942.0.33-1.39.0.57-1.76.pth
BLEU = 72.15, 86.6/76.2/67.8/60.6 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.943.0.29-1.33.0.56-1.76.pth
BLEU = 71.28, 85.8/75.4/66.9/59.7 (BP=1.000, ratio=1.041, hyp_len=24103, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.944.0.32-1.38.0.59-1.80.pth
BLEU = 70.39, 85.5/74.7/65.9/58.4 (BP=1.000, ratio=1.046, hyp_len=24228, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.945.0.32-1.38.0.57-1.77.pth
BLEU = 72.33, 86.5/76.3/68.0/61.0 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.946.0.33-1.39.0.59-1.81.pth
BLEU = 69.82, 85.1/74.3/65.3/57.6 (BP=1.000, ratio=1.050, hyp_len=24323, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.947.0.31-1.37.0.58-1.78.pth
BLEU = 72.05, 86.5/76.1/67.7/60.5 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.948.0.32-1.37.0.58-1.79.pth
BLEU = 71.23, 85.8/75.4/66.8/59.5 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.949.0.30-1.35.0.57-1.76.pth
BLEU = 71.02, 85.8/75.2/66.6/59.2 (BP=1.000, ratio=1.042, hyp_len=24144, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.950.0.34-1.41.0.59-1.80.pth
BLEU = 72.77, 86.8/76.6/68.5/61.6 (BP=1.000, ratio=1.030, hyp_len=23855, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.95.0.86-2.37.0.74-2.11.pth
BLEU = 58.69, 79.2/64.9/53.1/43.5 (BP=1.000, ratio=1.059, hyp_len=24527, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.951.0.29-1.34.0.57-1.77.pth
BLEU = 70.75, 85.7/75.0/66.3/58.8 (BP=1.000, ratio=1.044, hyp_len=24185, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.952.0.33-1.39.0.59-1.80.pth
BLEU = 71.93, 86.2/75.9/67.6/60.5 (BP=1.000, ratio=1.037, hyp_len=24021, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.953.0.32-1.38.0.57-1.77.pth
BLEU = 71.97, 86.3/76.0/67.6/60.5 (BP=1.000, ratio=1.035, hyp_len=23961, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.954.0.31-1.37.0.57-1.77.pth
BLEU = 71.43, 86.0/75.5/67.0/59.8 (BP=1.000, ratio=1.042, hyp_len=24128, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.955.0.31-1.36.0.57-1.76.pth
BLEU = 71.05, 85.8/75.3/66.6/59.3 (BP=1.000, ratio=1.041, hyp_len=24102, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
BLEU = 73.04, 86.9/76.8/68.8/62.0 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.957.0.32-1.38.0.58-1.79.pth
BLEU = 72.09, 86.3/76.0/67.7/60.8 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.958.0.32-1.38.0.57-1.77.pth
BLEU = 71.32, 86.0/75.4/66.9/59.7 (BP=1.000, ratio=1.040, hyp_len=24096, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.959.0.32-1.38.0.58-1.78.pth
BLEU = 71.05, 86.0/75.4/66.6/59.1 (BP=1.000, ratio=1.042, hyp_len=24125, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.960.0.31-1.37.0.57-1.77.pth
BLEU = 70.94, 85.8/75.2/66.5/59.1 (BP=1.000, ratio=1.042, hyp_len=24123, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.96.0.90-2.46.0.76-2.13.pth
BLEU = 57.69, 78.7/64.3/52.2/42.0 (BP=1.000, ratio=1.068, hyp_len=24745, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.961.0.31-1.36.0.57-1.76.pth
BLEU = 71.24, 85.7/75.3/66.9/59.7 (BP=1.000, ratio=1.043, hyp_len=24148, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.962.0.32-1.38.0.58-1.79.pth
BLEU = 71.72, 86.2/75.8/67.3/60.2 (BP=1.000, ratio=1.037, hyp_len=24020, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.963.0.32-1.38.0.57-1.77.pth
BLEU = 70.81, 85.5/75.0/66.4/59.0 (BP=1.000, ratio=1.046, hyp_len=24218, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.964.0.30-1.35.0.58-1.78.pth
BLEU = 70.42, 85.6/74.9/65.9/58.2 (BP=1.000, ratio=1.048, hyp_len=24268, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.965.0.34-1.40.0.56-1.76.pth
BLEU = 71.54, 86.1/75.6/67.1/59.9 (BP=1.000, ratio=1.038, hyp_len=24048, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.966.0.30-1.34.0.57-1.76.pth
BLEU = 70.96, 85.8/75.2/66.5/59.1 (BP=1.000, ratio=1.040, hyp_len=24086, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.967.0.31-1.36.0.57-1.76.pth
BLEU = 71.77, 86.2/75.8/67.4/60.2 (BP=1.000, ratio=1.036, hyp_len=24005, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.968.0.32-1.38.0.58-1.78.pth
BLEU = 71.28, 85.9/75.4/66.9/59.6 (BP=1.000, ratio=1.038, hyp_len=24030, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.969.0.31-1.36.0.58-1.79.pth
BLEU = 72.72, 86.7/76.6/68.4/61.5 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.970.0.31-1.36.0.57-1.77.pth
BLEU = 71.00, 85.8/75.2/66.5/59.2 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.97.0.92-2.52.0.75-2.12.pth
BLEU = 57.89, 78.8/64.4/52.3/42.3 (BP=1.000, ratio=1.066, hyp_len=24693, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.971.0.30-1.36.0.57-1.76.pth
BLEU = 72.07, 86.4/76.0/67.7/60.7 (BP=1.000, ratio=1.037, hyp_len=24013, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.972.0.30-1.35.0.57-1.78.pth
BLEU = 71.24, 86.0/75.3/66.7/59.6 (BP=1.000, ratio=1.041, hyp_len=24099, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.973.0.31-1.36.0.57-1.77.pth
BLEU = 72.74, 86.6/76.6/68.5/61.6 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.974.0.32-1.37.0.57-1.77.pth
BLEU = 72.60, 86.8/76.5/68.2/61.3 (BP=1.000, ratio=1.032, hyp_len=23908, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.975.0.32-1.37.0.57-1.77.pth
BLEU = 71.09, 86.0/75.3/66.6/59.2 (BP=1.000, ratio=1.039, hyp_len=24056, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.976.0.31-1.36.0.57-1.77.pth
BLEU = 71.77, 86.2/75.8/67.4/60.3 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.977.0.33-1.39.0.57-1.77.pth
BLEU = 70.37, 85.5/74.8/65.9/58.2 (BP=1.000, ratio=1.046, hyp_len=24227, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.978.0.30-1.34.0.58-1.78.pth
BLEU = 72.92, 87.1/76.8/68.6/61.7 (BP=1.000, ratio=1.026, hyp_len=23765, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.979.0.29-1.34.0.57-1.76.pth
BLEU = 71.74, 86.2/75.8/67.3/60.2 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.980.0.30-1.35.0.57-1.78.pth
BLEU = 71.96, 86.4/76.0/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24011, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.98.0.85-2.34.0.74-2.09.pth
BLEU = 58.52, 79.4/64.8/52.9/43.1 (BP=1.000, ratio=1.058, hyp_len=24498, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.981.0.30-1.36.0.58-1.79.pth
BLEU = 72.11, 86.3/76.1/67.8/60.8 (BP=1.000, ratio=1.035, hyp_len=23962, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.982.0.32-1.38.0.58-1.78.pth
BLEU = 70.52, 85.3/74.8/66.1/58.6 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.983.0.31-1.36.0.57-1.77.pth
BLEU = 71.71, 86.2/75.8/67.3/60.2 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.984.0.31-1.36.0.57-1.77.pth
BLEU = 72.23, 86.5/76.2/67.8/60.8 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.985.0.31-1.36.0.59-1.80.pth
BLEU = 72.34, 86.8/76.4/67.9/60.8 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.986.0.32-1.38.0.57-1.77.pth
BLEU = 72.23, 86.5/76.2/67.9/60.9 (BP=1.000, ratio=1.034, hyp_len=23938, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.987.0.32-1.38.0.57-1.77.pth
BLEU = 71.92, 86.3/76.0/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24021, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.988.0.30-1.36.0.57-1.77.pth
BLEU = 70.76, 85.8/75.1/66.3/58.7 (BP=1.000, ratio=1.043, hyp_len=24148, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.989.0.31-1.36.0.59-1.81.pth
BLEU = 71.93, 86.5/76.0/67.5/60.3 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.990.0.31-1.36.0.58-1.78.pth
BLEU = 72.09, 86.5/76.1/67.7/60.6 (BP=1.000, ratio=1.034, hyp_len=23951, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.99.0.86-2.35.0.73-2.08.pth
BLEU = 60.81, 81.3/66.8/55.2/45.7 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.991.0.30-1.35.0.57-1.77.pth
BLEU = 70.91, 85.5/75.0/66.5/59.2 (BP=1.000, ratio=1.043, hyp_len=24158, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.992.0.30-1.35.0.56-1.75.pth
BLEU = 72.43, 86.5/76.4/68.2/61.1 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.993.0.32-1.37.0.56-1.76.pth
BLEU = 71.75, 86.2/75.8/67.3/60.2 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.994.0.32-1.38.0.57-1.76.pth
BLEU = 71.40, 86.0/75.5/66.9/59.8 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.995.0.29-1.34.0.58-1.79.pth
BLEU = 71.47, 86.0/75.6/67.0/59.8 (BP=1.000, ratio=1.039, hyp_len=24052, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.996.0.32-1.38.0.58-1.78.pth
BLEU = 72.22, 86.6/76.2/67.8/60.8 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.997.0.34-1.40.0.59-1.80.pth
BLEU = 70.87, 85.9/75.3/66.3/58.8 (BP=1.000, ratio=1.041, hyp_len=24099, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.998.0.30-1.35.0.58-1.78.pth
BLEU = 72.43, 86.6/76.4/68.1/61.1 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.999.0.33-1.40.0.57-1.78.pth
BLEU = 72.14, 86.4/76.1/67.8/60.8 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)

real	557m46.397s
user	548m33.963s
sys	20m22.524s
```

Transformer မော်ဒယ် နဲ့ epoch 1000 training လုပ်ကြည့်ခဲ့တာမှာ Highest score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
BLEU = 73.04, 86.9/76.8/68.8/62.0 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
```

## RL with Transformer 1000 epoch Model (Myanmar-Rakhine)

အရင်ဆုံး memory နိုင်မနိုင်ကို သိချင်လို့... epoch 956 model ကို 960 အထိပဲ RL fine-tuning လုပ်ခိုင်းကြည့်ခဲ့...  

time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 960


```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 960
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/transformer-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 960
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 956
WARNING!!! You changed value for argument "--max_grad_norm".	Use current value: 5.0
WARNING!!! You changed value for argument "--iteration_per_update".	Use current value: 1
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 956,
    'iteration_per_update': 1,
    'lang': 'myrk',
    'load_fn': './model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 5.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/transformer-rl-model-myrk.pth',
    'n_epochs': 960,
    'n_layers': 6,
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
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/myrk-transformer/data/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1585, 32)
  (emb_dec): Embedding(1695, 32)
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
    (1): Linear(in_features=32, out_features=1695, bias=True)
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
Epoch 956 - |param|=3.89e+02 |g_param|=1.77e+04 loss=4.6227e-01 ppl=1.59                                                
Validation - loss=6.8054e-01 ppl=1.97 best_loss=inf best_ppl=inf                                                        
Epoch 957 - |param|=3.90e+02 |g_param|=1.62e+04 loss=4.9188e-01 ppl=1.64                                                
Validation - loss=6.1286e-01 ppl=1.85 best_loss=6.8054e-01 best_ppl=1.97                                                
Epoch 958 - |param|=3.90e+02 |g_param|=3.30e+04 loss=5.4664e-01 ppl=1.73                                                
Validation - loss=7.4770e-01 ppl=2.11 best_loss=6.1286e-01 best_ppl=1.85                                                
Epoch 959 - |param|=3.90e+02 |g_param|=2.52e+04 loss=5.4233e-01 ppl=1.72                                                
Validation - loss=6.0341e-01 ppl=1.83 best_loss=6.1286e-01 best_ppl=1.85                                                
Epoch 960 - |param|=3.91e+02 |g_param|=5.00e+04 loss=5.3513e-01 ppl=1.71                                                
Validation - loss=6.1122e-01 ppl=1.84 best_loss=6.0341e-01 best_ppl=1.83                                                

real	4m21.064s
user	4m17.144s
sys	0m1.442s
(simple-nmt) ye@:~/exp/simple-nmt$
```

baseline က 73.04 ဖြစ်ပြီးတော့... 
testing/evaluation with Transformer RL epoch 960 model...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-model-myrk.956.0.46-1.59.0.68-1.97.pth
BLEU = 66.49, 83.5/72.1/61.6/52.6 (BP=1.000, ratio=1.060, hyp_len=24539, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.957.0.49-1.64.0.61-1.85.pth
BLEU = 67.60, 83.7/72.4/62.9/54.8 (BP=1.000, ratio=1.059, hyp_len=24515, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.958.0.55-1.73.0.75-2.11.pth
BLEU = 65.53, 81.1/70.0/60.9/53.3 (BP=1.000, ratio=1.075, hyp_len=24907, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.959.0.54-1.72.0.60-1.83.pth
BLEU = 69.18, 84.7/73.6/64.5/56.9 (BP=1.000, ratio=1.039, hyp_len=24054, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.960.0.54-1.71.0.61-1.84.pth
BLEU = 68.22, 84.4/73.1/63.5/55.3 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)

real	3m3.452s
user	3m0.493s
sys	0m6.389s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$
```

epoch ကို အများကြီး တိုးလုပ်ကြည့်မယ်...  
baseline ထက် RL model က ကျော်ဖို့ မျှော်လင့်တယ်...  
epoch 2000 အထိ RL မော်ဒယ်ကို training လုပ်ကြည့်မယ်...  

(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 2000

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1 --max_grad_norm 5 --n_epochs 2000
...
...
...
Validation - loss=5.8926e-01 ppl=1.80 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1990 - |param|=2.32e+03 |g_param|=7.56e+03 loss=4.5184e-01 ppl=1.57                                               
Validation - loss=5.7727e-01 ppl=1.78 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1991 - |param|=2.32e+03 |g_param|=4.62e+03 loss=4.2194e-01 ppl=1.52                                               
Validation - loss=5.6858e-01 ppl=1.77 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1992 - |param|=2.32e+03 |g_param|=3.69e+03 loss=4.1810e-01 ppl=1.52                                               
Validation - loss=5.8679e-01 ppl=1.80 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1993 - |param|=2.33e+03 |g_param|=5.46e+03 loss=4.8183e-01 ppl=1.62                                               
Validation - loss=5.8511e-01 ppl=1.80 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1994 - |param|=2.33e+03 |g_param|=4.25e+03 loss=4.3804e-01 ppl=1.55                                               
Validation - loss=5.8420e-01 ppl=1.79 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1995 - |param|=2.33e+03 |g_param|=1.11e+04 loss=4.4132e-01 ppl=1.55                                               
Validation - loss=5.8395e-01 ppl=1.79 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1996 - |param|=2.33e+03 |g_param|=4.66e+03 loss=4.0515e-01 ppl=1.50                                               
Validation - loss=6.1136e-01 ppl=1.84 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1997 - |param|=2.33e+03 |g_param|=4.18e+03 loss=4.3161e-01 ppl=1.54                                               
Validation - loss=5.9366e-01 ppl=1.81 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1998 - |param|=2.34e+03 |g_param|=8.39e+03 loss=4.3229e-01 ppl=1.54                                               
Validation - loss=5.9933e-01 ppl=1.82 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 1999 - |param|=2.34e+03 |g_param|=4.92e+03 loss=4.4067e-01 ppl=1.55                                               
Validation - loss=5.7990e-01 ppl=1.79 best_loss=5.1290e-01 best_ppl=1.67                                                
Epoch 2000 - |param|=2.34e+03 |g_param|=4.39e+03 loss=4.1212e-01 ppl=1.51                                               
Validation - loss=6.0450e-01 ppl=1.83 best_loss=5.1290e-01 best_ppl=1.67                                                

real	890m29.017s
user	889m7.521s
sys	1m13.908s
```

2000 epoch model ကို testing/evaluation လုပ်ခဲ့...  

```
Evaluation result for the model: transformer-rl-model-myrk.984.0.57-1.76.0.60-1.82.pth
BLEU = 68.24, 84.3/72.8/63.5/55.7 (BP=1.000, ratio=1.028, hyp_len=23811, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.985.0.58-1.79.0.65-1.91.pth
BLEU = 67.30, 83.9/72.3/62.5/54.1 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.986.0.58-1.79.0.61-1.85.pth
BLEU = 64.94, 81.6/70.0/60.1/51.8 (BP=1.000, ratio=1.070, hyp_len=24783, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.987.0.60-1.82.0.63-1.88.pth
BLEU = 68.59, 84.3/73.1/63.9/56.2 (BP=1.000, ratio=1.034, hyp_len=23945, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.988.0.54-1.71.0.59-1.80.pth
BLEU = 67.65, 83.5/72.3/62.9/55.2 (BP=1.000, ratio=1.054, hyp_len=24401, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.989.0.58-1.78.0.64-1.89.pth
BLEU = 69.03, 84.7/73.4/64.3/56.8 (BP=1.000, ratio=1.023, hyp_len=23697, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.990.0.52-1.68.0.60-1.82.pth
BLEU = 68.72, 84.3/73.0/64.0/56.5 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.991.0.60-1.81.0.63-1.88.pth
BLEU = 68.06, 84.0/72.7/63.3/55.5 (BP=1.000, ratio=1.039, hyp_len=24065, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.59-1.80.0.66-1.93.pth
BLEU = 67.48, 83.7/72.1/62.7/54.8 (BP=1.000, ratio=1.037, hyp_len=24009, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.54-1.72.0.62-1.87.pth
BLEU = 65.04, 82.1/70.4/60.2/51.4 (BP=1.000, ratio=1.067, hyp_len=24702, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.55-1.74.0.59-1.81.pth
BLEU = 66.87, 82.7/71.4/62.1/54.5 (BP=1.000, ratio=1.059, hyp_len=24537, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.54-1.72.0.58-1.79.pth
BLEU = 68.43, 84.5/73.1/63.6/55.7 (BP=1.000, ratio=1.044, hyp_len=24172, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.60-1.83.0.60-1.81.pth
BLEU = 66.93, 83.3/71.7/62.2/54.0 (BP=1.000, ratio=1.053, hyp_len=24381, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.57-1.76.0.59-1.80.pth
BLEU = 68.35, 84.0/72.9/63.7/56.0 (BP=1.000, ratio=1.043, hyp_len=24160, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.56-1.75.0.61-1.84.pth
BLEU = 67.81, 84.2/72.6/63.0/55.0 (BP=1.000, ratio=1.035, hyp_len=23976, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.56-1.75.0.61-1.84.pth
BLEU = 68.79, 84.6/73.3/64.1/56.3 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)

real	574m48.142s
user	564m44.748s
sys	21m45.108s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 

```

Transformer model ရဲ့ baseline က 

```
Evaluation result for the model: myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
BLEU = 73.04, 86.9/76.8/68.8/62.0 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
```

Transformer ကို RL နဲ့ tuning, 2000 epoch နဲ့ လုပ်ခဲ့တဲ့ ရလဒ် တွေထဲမှာ...  
71.xx က စုစုပေါင်း ၅၂ ခု ရတယ်... အဲဒီ အထဲကမှ top score က ...  

```
Evaluation result for the model: transformer-rl-model-myrk.1582.0.43-1.53.0.55-1.74.pth
BLEU = 71.76, 86.6/76.0/67.3/59.9 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1588.0.45-1.57.0.57-1.77.pth
BLEU = 71.52, 86.3/75.8/67.1/59.6 (BP=1.000, ratio=1.025, hyp_len=23737, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1599.0.43-1.53.0.59-1.81.pth
BLEU = 71.78, 86.6/76.0/67.3/59.9 (BP=1.000, ratio=1.019, hyp_len=23591, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1600.0.44-1.56.0.57-1.77.pth
BLEU = 71.56, 86.4/75.7/67.1/59.7 (BP=1.000, ratio=1.020, hyp_len=23632, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1605.0.42-1.52.0.58-1.78.pth
BLEU = 71.68, 86.1/75.7/67.3/60.2 (BP=1.000, ratio=1.028, hyp_len=23797, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1612.0.46-1.58.0.57-1.77.pth
BLEU = 71.79, 86.4/75.9/67.4/60.1 (BP=1.000, ratio=1.024, hyp_len=23712, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1642.0.45-1.57.0.57-1.77.pth
BLEU = 71.65, 86.6/75.8/67.1/59.9 (BP=1.000, ratio=1.019, hyp_len=23589, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1680.0.43-1.54.0.57-1.76.pth
BLEU = 71.46, 86.1/75.6/67.0/59.7 (BP=1.000, ratio=1.026, hyp_len=23751, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1767.0.45-1.57.0.61-1.84.pth
BLEU = 71.67, 86.3/75.8/67.2/60.0 (BP=1.000, ratio=1.019, hyp_len=23611, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1777.0.42-1.52.0.56-1.75.pth
BLEU = 71.53, 86.1/75.6/67.2/59.9 (BP=1.000, ratio=1.027, hyp_len=23785, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1872.0.43-1.54.0.57-1.76.pth
BLEU = 71.63, 86.2/75.7/67.2/60.0 (BP=1.000, ratio=1.029, hyp_len=23831, ref_len=23160)

Evaluation result for the model: transformer-rl-model-myrk.1893.0.47-1.59.0.59-1.81.pth
BLEU = 71.56, 86.2/75.8/67.2/59.7 (BP=1.000, ratio=1.029, hyp_len=23830, ref_len=23160)
...
...
```

Transformer ကို RL နဲ့ tuning, 2000 epoch နဲ့ လုပ်ခဲ့တဲ့ ရလဒ် အကောင်းဆုံးက ...  

```
Evaluation result for the model: transformer-rl-model-myrk.1612.0.46-1.58.0.57-1.77.pth
BLEU = 71.79, 86.4/75.9/67.4/60.1 (BP=1.000, ratio=1.024, hyp_len=23712, ref_len=23160)
```

တချို့ကို backup ကူးထားပြီး ကျန်တဲ့ model တွေကို အကုန် ဖျက်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv bk bk-2000epoch
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1612.0.46-1.58.0.57-1.77.pth ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1612.0.46-1.58.0.57-1.77.pth.hyp ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1582.0.43-1.53.0.55-1.74.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1588.0.45-1.57.0.57-1.77.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1599.0.43-1.53.0.59-1.81.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1600.0.44-1.56.0.57-1.77.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1605.0.42-1.52.0.58-1.78.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1612.0.46-1.58.0.57-1.77.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1642.0.45-1.57.0.57-1.77.pth* ./bk-2000epoch/
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1767.0.45-1.57.0.61-1.84.pth* ./bk-2000epoch/
```

လက်ရှိ အချိန်ထိ seq2seq အတွက်ရော transformer အတွက်ရော RL fine-tuning လုပ်ကြည့်တာ ရလဒ်က baseline ကို မကျော်နိုင်ဘူး...  

ထပ် experiment လုပ်လို့ ရတာက ...  
--max_grad_norm 5 ကို လျှော့ပြီး training လုပ်ကြည့်တာမျိုး ...  
Transformer မော်ဒယ်ကို training လုပ်တုန်းကနဲ့ အတူတူပဲ ထားကြည့်တာမျိုး...  

အရင်ဆုံး အတူတူ setting နဲ့ ထပ် RL fine-tuning လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1  --max_grad_norm 1e+8 --n_epochs 1000
...
...
...
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
    (1): Linear(in_features=32, out_features=1695, bias=True)
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
Epoch 956 - |param|=3.90e+02 |g_param|=5.15e+04 loss=5.1030e-01 ppl=1.67                                                
Validation - loss=6.0869e-01 ppl=1.84 best_loss=inf best_ppl=inf                                                        
Epoch 957 - |param|=3.90e+02 |g_param|=5.35e+04 loss=5.5065e-01 ppl=1.73                                                
Validation - loss=5.9201e-01 ppl=1.81 best_loss=6.0869e-01 best_ppl=1.84                                                
Epoch 958 - |param|=3.90e+02 |g_param|=4.69e+04 loss=5.4620e-01 ppl=1.73                                                
Validation - loss=6.2222e-01 ppl=1.86 best_loss=5.9201e-01 best_ppl=1.81                                                
Epoch 959 - |param|=3.91e+02 |g_param|=4.37e+04 loss=5.1826e-01 ppl=1.68                                                
Validation - loss=5.7150e-01 ppl=1.77 best_loss=5.9201e-01 best_ppl=1.81                                                
Epoch 960 - |param|=3.92e+02 |g_param|=4.58e+04 loss=5.7528e-01 ppl=1.78                                                
Validation - loss=5.6630e-01 ppl=1.76 best_loss=5.7150e-01 best_ppl=1.77                                                
Epoch 961 - |param|=3.92e+02 |g_param|=4.64e+04 loss=5.9502e-01 ppl=1.81                                                
Validation - loss=6.2762e-01 ppl=1.87 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 962 - |param|=3.93e+02 |g_param|=5.23e+04 loss=5.8313e-01 ppl=1.79                                                
Validation - loss=5.9542e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 963 - |param|=3.94e+02 |g_param|=3.99e+04 loss=5.8759e-01 ppl=1.80                                                
Validation - loss=6.5682e-01 ppl=1.93 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 964 - |param|=3.94e+02 |g_param|=6.10e+04 loss=5.4250e-01 ppl=1.72                                                
Validation - loss=5.7521e-01 ppl=1.78 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 965 - |param|=3.95e+02 |g_param|=5.15e+04 loss=6.9720e-01 ppl=2.01                                                
Validation - loss=6.3042e-01 ppl=1.88 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 966 - |param|=3.95e+02 |g_param|=3.65e+04 loss=5.5322e-01 ppl=1.74                                                
Validation - loss=6.0291e-01 ppl=1.83 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 967 - |param|=3.96e+02 |g_param|=3.61e+04 loss=5.7221e-01 ppl=1.77                                                
Validation - loss=6.2881e-01 ppl=1.88 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 968 - |param|=3.97e+02 |g_param|=4.30e+04 loss=5.9421e-01 ppl=1.81                                                
Validation - loss=6.0423e-01 ppl=1.83 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 969 - |param|=3.98e+02 |g_param|=8.84e+04 loss=6.2997e-01 ppl=1.88                                                
Validation - loss=6.2233e-01 ppl=1.86 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 970 - |param|=3.99e+02 |g_param|=3.97e+04 loss=6.1365e-01 ppl=1.85                                                
Validation - loss=6.6532e-01 ppl=1.95 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 971 - |param|=4.00e+02 |g_param|=4.13e+04 loss=6.0862e-01 ppl=1.84                                                
Validation - loss=6.7157e-01 ppl=1.96 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 972 - |param|=4.01e+02 |g_param|=3.77e+04 loss=6.1897e-01 ppl=1.86                                                
Validation - loss=6.5046e-01 ppl=1.92 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 973 - |param|=4.02e+02 |g_param|=1.73e+04 loss=5.9600e-01 ppl=1.81                                                
Validation - loss=6.2755e-01 ppl=1.87 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 974 - |param|=4.04e+02 |g_param|=1.78e+04 loss=6.1020e-01 ppl=1.84                                                
Validation - loss=6.0367e-01 ppl=1.83 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 975 - |param|=4.05e+02 |g_param|=3.25e+04 loss=6.1045e-01 ppl=1.84                                                
Validation - loss=6.1900e-01 ppl=1.86 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 976 - |param|=4.06e+02 |g_param|=3.66e+04 loss=6.1830e-01 ppl=1.86                                                
Validation - loss=5.9437e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 977 - |param|=4.08e+02 |g_param|=1.80e+04 loss=5.5674e-01 ppl=1.74                                                
Validation - loss=6.0462e-01 ppl=1.83 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 978 - |param|=4.09e+02 |g_param|=2.10e+04 loss=6.2956e-01 ppl=1.88                                                
Validation - loss=6.1954e-01 ppl=1.86 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 979 - |param|=4.10e+02 |g_param|=3.49e+04 loss=5.7749e-01 ppl=1.78                                                
Validation - loss=5.9272e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 980 - |param|=4.11e+02 |g_param|=4.23e+04 loss=6.4139e-01 ppl=1.90                                                
Validation - loss=6.2659e-01 ppl=1.87 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 981 - |param|=4.13e+02 |g_param|=3.76e+04 loss=5.7831e-01 ppl=1.78                                                
Validation - loss=6.2992e-01 ppl=1.88 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 982 - |param|=4.14e+02 |g_param|=3.57e+04 loss=5.9149e-01 ppl=1.81                                                
Validation - loss=6.4177e-01 ppl=1.90 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 983 - |param|=4.15e+02 |g_param|=6.50e+04 loss=5.9149e-01 ppl=1.81                                                
Validation - loss=5.9206e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 984 - |param|=4.17e+02 |g_param|=3.97e+04 loss=5.7211e-01 ppl=1.77                                                
Validation - loss=6.0476e-01 ppl=1.83 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 985 - |param|=4.18e+02 |g_param|=4.02e+04 loss=6.1212e-01 ppl=1.84                                                
Validation - loss=6.8398e-01 ppl=1.98 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 986 - |param|=4.20e+02 |g_param|=3.52e+04 loss=5.5040e-01 ppl=1.73                                                
Validation - loss=6.1734e-01 ppl=1.85 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 987 - |param|=4.21e+02 |g_param|=3.33e+04 loss=5.6440e-01 ppl=1.76                                                
Validation - loss=6.4196e-01 ppl=1.90 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 988 - |param|=4.22e+02 |g_param|=1.71e+04 loss=5.6294e-01 ppl=1.76                                                
Validation - loss=5.9192e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 989 - |param|=4.24e+02 |g_param|=1.68e+04 loss=5.2813e-01 ppl=1.70                                                
Validation - loss=6.0790e-01 ppl=1.84 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 990 - |param|=4.25e+02 |g_param|=3.61e+04 loss=5.6327e-01 ppl=1.76                                                
Validation - loss=5.8195e-01 ppl=1.79 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 991 - |param|=4.26e+02 |g_param|=3.91e+04 loss=5.8339e-01 ppl=1.79                                                
Validation - loss=5.8995e-01 ppl=1.80 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 992 - |param|=4.28e+02 |g_param|=3.27e+04 loss=5.4672e-01 ppl=1.73                                                
Validation - loss=5.9353e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 993 - |param|=4.29e+02 |g_param|=3.68e+04 loss=5.5425e-01 ppl=1.74                                                
Validation - loss=6.2465e-01 ppl=1.87 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 994 - |param|=4.31e+02 |g_param|=4.61e+04 loss=5.7178e-01 ppl=1.77                                                
Validation - loss=5.8057e-01 ppl=1.79 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 995 - |param|=4.32e+02 |g_param|=3.75e+04 loss=5.9009e-01 ppl=1.80                                                
Validation - loss=6.2729e-01 ppl=1.87 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 996 - |param|=4.34e+02 |g_param|=1.77e+04 loss=5.9678e-01 ppl=1.82                                                
Validation - loss=5.9556e-01 ppl=1.81 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 997 - |param|=4.35e+02 |g_param|=1.78e+04 loss=5.7012e-01 ppl=1.77                                                
Validation - loss=5.8686e-01 ppl=1.80 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 998 - |param|=4.37e+02 |g_param|=3.47e+04 loss=5.7234e-01 ppl=1.77                                                
Validation - loss=5.7638e-01 ppl=1.78 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 999 - |param|=4.38e+02 |g_param|=3.92e+04 loss=5.6518e-01 ppl=1.76                                                
Validation - loss=5.6976e-01 ppl=1.77 best_loss=5.6630e-01 best_ppl=1.76                                                
Epoch 1000 - |param|=4.39e+02 |g_param|=3.80e+04 loss=5.4695e-01 ppl=1.73                                               
Validation - loss=6.0715e-01 ppl=1.84 best_loss=5.6630e-01 best_ppl=1.76                                                

real	37m36.911s
user	37m30.612s
sys	0m3.869s
```

အပြောင်းအလဲကို သိချင်လို့... နည်းနည်းပဲ fine-tuning လုပ်ပြီးတော့ ... testing/evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-model-myrk.1000.0.55-1.73.0.61-1.84.pth
BLEU = 66.12, 82.7/71.1/61.4/53.0 (BP=1.000, ratio=1.059, hyp_len=24522, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.956.0.51-1.67.0.61-1.84.pth
BLEU = 70.94, 86.5/75.4/66.2/58.7 (BP=1.000, ratio=1.011, hyp_len=23422, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.957.0.55-1.73.0.59-1.81.pth
BLEU = 68.69, 85.1/73.5/63.8/55.7 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.958.0.55-1.73.0.62-1.86.pth
BLEU = 65.61, 82.9/71.3/60.9/51.5 (BP=1.000, ratio=1.064, hyp_len=24634, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.959.0.52-1.68.0.57-1.77.pth
BLEU = 67.49, 83.3/72.0/62.8/55.1 (BP=1.000, ratio=1.055, hyp_len=24443, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.960.0.58-1.78.0.57-1.76.pth
BLEU = 66.44, 82.2/71.1/61.7/54.0 (BP=1.000, ratio=1.070, hyp_len=24775, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.961.0.60-1.81.0.63-1.87.pth
BLEU = 66.08, 82.4/71.0/61.4/53.1 (BP=1.000, ratio=1.067, hyp_len=24713, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.962.0.58-1.79.0.60-1.81.pth
BLEU = 67.50, 83.9/72.4/62.7/54.5 (BP=1.000, ratio=1.044, hyp_len=24182, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.963.0.59-1.80.0.66-1.93.pth
BLEU = 66.00, 83.2/71.1/61.0/52.6 (BP=1.000, ratio=1.042, hyp_len=24139, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.964.0.54-1.72.0.58-1.78.pth
BLEU = 68.68, 84.8/73.4/63.9/55.9 (BP=1.000, ratio=1.037, hyp_len=24008, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.965.0.70-2.01.0.63-1.88.pth
BLEU = 66.45, 82.8/71.2/61.7/53.6 (BP=1.000, ratio=1.054, hyp_len=24422, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.966.0.55-1.74.0.60-1.83.pth
BLEU = 66.95, 84.0/72.5/62.2/53.1 (BP=1.000, ratio=1.048, hyp_len=24275, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.967.0.57-1.77.0.63-1.88.pth
BLEU = 70.13, 86.0/74.7/65.4/57.6 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.968.0.59-1.81.0.60-1.83.pth
BLEU = 66.90, 83.2/71.7/62.1/54.0 (BP=1.000, ratio=1.055, hyp_len=24434, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.969.0.63-1.88.0.62-1.86.pth
BLEU = 64.29, 82.2/70.0/59.4/50.0 (BP=1.000, ratio=1.062, hyp_len=24600, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.970.0.61-1.85.0.67-1.95.pth
BLEU = 68.18, 84.4/72.9/63.4/55.4 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.971.0.61-1.84.0.67-1.96.pth
BLEU = 64.21, 81.7/69.7/59.3/50.3 (BP=1.000, ratio=1.069, hyp_len=24750, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.972.0.62-1.86.0.65-1.92.pth
BLEU = 61.83, 78.0/66.6/57.2/49.2 (BP=1.000, ratio=1.119, hyp_len=25910, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.973.0.60-1.81.0.63-1.87.pth
BLEU = 67.84, 84.3/72.5/63.0/55.0 (BP=1.000, ratio=1.028, hyp_len=23813, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.974.0.61-1.84.0.60-1.83.pth
BLEU = 67.10, 82.7/71.6/62.5/54.8 (BP=1.000, ratio=1.061, hyp_len=24578, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.975.0.61-1.84.0.62-1.86.pth
BLEU = 67.79, 84.3/72.5/62.9/54.9 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.976.0.62-1.86.0.59-1.81.pth
BLEU = 66.58, 83.7/71.7/61.6/53.1 (BP=1.000, ratio=1.047, hyp_len=24247, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.977.0.56-1.74.0.60-1.83.pth
BLEU = 67.92, 84.3/72.8/63.1/55.0 (BP=1.000, ratio=1.032, hyp_len=23894, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.978.0.63-1.88.0.62-1.86.pth
BLEU = 68.77, 84.7/73.4/64.0/56.2 (BP=1.000, ratio=1.028, hyp_len=23809, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.979.0.58-1.78.0.59-1.81.pth
BLEU = 68.12, 84.1/72.9/63.4/55.3 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.980.0.64-1.90.0.63-1.87.pth
BLEU = 67.28, 84.5/72.3/62.3/53.9 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.981.0.58-1.78.0.63-1.88.pth
BLEU = 63.05, 78.8/67.8/58.4/50.6 (BP=1.000, ratio=1.117, hyp_len=25863, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.982.0.59-1.81.0.64-1.90.pth
BLEU = 66.06, 83.0/71.3/61.3/52.6 (BP=1.000, ratio=1.056, hyp_len=24454, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.983.0.59-1.81.0.59-1.81.pth
BLEU = 68.84, 84.7/73.3/64.1/56.5 (BP=1.000, ratio=1.029, hyp_len=23832, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.984.0.57-1.77.0.60-1.83.pth
BLEU = 68.05, 84.4/72.9/63.2/55.1 (BP=1.000, ratio=1.041, hyp_len=24103, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.985.0.61-1.84.0.68-1.98.pth
BLEU = 59.39, 75.4/64.4/55.0/46.6 (BP=1.000, ratio=1.169, hyp_len=27068, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.986.0.55-1.73.0.62-1.85.pth
BLEU = 67.85, 84.4/72.7/63.0/54.8 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.987.0.56-1.76.0.64-1.90.pth
BLEU = 63.60, 80.3/68.7/58.9/50.4 (BP=1.000, ratio=1.090, hyp_len=25249, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.988.0.56-1.76.0.59-1.81.pth
BLEU = 69.97, 85.8/74.6/65.2/57.5 (BP=1.000, ratio=1.025, hyp_len=23735, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.989.0.53-1.70.0.61-1.84.pth
BLEU = 69.15, 85.1/73.8/64.4/56.5 (BP=1.000, ratio=1.023, hyp_len=23697, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.990.0.56-1.76.0.58-1.79.pth
BLEU = 68.65, 84.3/73.1/64.0/56.3 (BP=1.000, ratio=1.043, hyp_len=24157, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.991.0.58-1.79.0.59-1.80.pth
BLEU = 68.16, 84.6/73.0/63.3/55.1 (BP=1.000, ratio=1.044, hyp_len=24186, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.55-1.73.0.59-1.81.pth
BLEU = 69.31, 85.3/73.9/64.5/56.7 (BP=1.000, ratio=1.031, hyp_len=23879, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.55-1.74.0.62-1.87.pth
BLEU = 64.51, 80.3/69.1/59.9/52.0 (BP=1.000, ratio=1.095, hyp_len=25355, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.57-1.77.0.58-1.79.pth
BLEU = 69.48, 85.2/74.0/64.8/57.1 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.59-1.80.0.63-1.87.pth
BLEU = 69.31, 85.0/73.9/64.6/56.9 (BP=1.000, ratio=1.024, hyp_len=23705, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.60-1.82.0.60-1.81.pth
BLEU = 66.62, 83.2/71.8/61.9/53.3 (BP=1.000, ratio=1.064, hyp_len=24632, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.57-1.77.0.59-1.80.pth
BLEU = 67.76, 83.5/72.4/63.1/55.3 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.57-1.77.0.58-1.78.pth
BLEU = 66.84, 82.9/71.6/62.2/54.0 (BP=1.000, ratio=1.063, hyp_len=24630, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.57-1.76.0.57-1.77.pth
BLEU = 68.68, 84.3/73.2/64.1/56.3 (BP=1.000, ratio=1.044, hyp_len=24178, ref_len=23160)

real	26m57.557s
user	26m29.684s
sys	0m57.543s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 

```

အပြောင်းအလဲက သိပ်မထူးခြားလို့ --max_grad_norm 2 ထားကြည့်ပြီး run ကြည့်ခဲ့...  
ဒီတစ်ခါတော့ epoch ကို 1100 ထားခဲ့တော့ 144 epoch ထားပြီး စမ်း run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1  --max_grad_norm 2 --n_epochs 1100
...
...
...
Validation - loss=5.4409e-01 ppl=1.72 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1086 - |param|=5.11e+02 |g_param|=4.29e+04 loss=5.0369e-01 ppl=1.65                                               
Validation - loss=5.7310e-01 ppl=1.77 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1087 - |param|=5.13e+02 |g_param|=4.38e+04 loss=4.7309e-01 ppl=1.60                                               
Validation - loss=5.3869e-01 ppl=1.71 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1088 - |param|=5.14e+02 |g_param|=1.11e+04 loss=4.8590e-01 ppl=1.63                                               
Validation - loss=5.4483e-01 ppl=1.72 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1089 - |param|=5.16e+02 |g_param|=1.14e+04 loss=4.7614e-01 ppl=1.61                                               
Validation - loss=5.4981e-01 ppl=1.73 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1090 - |param|=5.17e+02 |g_param|=1.92e+04 loss=4.9140e-01 ppl=1.63                                               
Validation - loss=5.6042e-01 ppl=1.75 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1091 - |param|=5.19e+02 |g_param|=1.17e+04 loss=4.8855e-01 ppl=1.63                                               
Validation - loss=5.4373e-01 ppl=1.72 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1092 - |param|=5.20e+02 |g_param|=1.19e+04 loss=5.0307e-01 ppl=1.65                                               
Validation - loss=5.3523e-01 ppl=1.71 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1093 - |param|=5.22e+02 |g_param|=2.30e+04 loss=4.8507e-01 ppl=1.62                                               
Validation - loss=5.4463e-01 ppl=1.72 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1094 - |param|=5.23e+02 |g_param|=2.38e+04 loss=4.7473e-01 ppl=1.61                                               
Validation - loss=5.5461e-01 ppl=1.74 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1095 - |param|=5.24e+02 |g_param|=4.52e+04 loss=4.9588e-01 ppl=1.64                                               
Validation - loss=5.6457e-01 ppl=1.76 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1096 - |param|=5.25e+02 |g_param|=2.31e+04 loss=4.7876e-01 ppl=1.61                                               
Validation - loss=5.4439e-01 ppl=1.72 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1097 - |param|=5.27e+02 |g_param|=2.53e+04 loss=5.4051e-01 ppl=1.72                                               
Validation - loss=5.4555e-01 ppl=1.73 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1098 - |param|=5.28e+02 |g_param|=4.54e+04 loss=4.8298e-01 ppl=1.62                                               
Validation - loss=5.6794e-01 ppl=1.76 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1099 - |param|=5.29e+02 |g_param|=4.72e+04 loss=5.0051e-01 ppl=1.65                                               
Validation - loss=5.3772e-01 ppl=1.71 best_loss=5.3429e-01 best_ppl=1.71                                                
Epoch 1100 - |param|=5.30e+02 |g_param|=4.36e+04 loss=4.5732e-01 ppl=1.58                                               
Validation - loss=5.6835e-01 ppl=1.77 best_loss=5.3429e-01 best_ppl=1.71                                                

real	122m36.519s
user	122m23.097s
sys	0m11.951s
```

max_grad_norm 2, 144 epoch Transformer, RL fine-tuning model ကို testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh
...
...
Evaluation result for the model: transformer-rl-model-myrk.994.0.54-1.71.0.65-1.91.pth
BLEU = 64.80, 82.2/70.3/59.9/51.0 (BP=1.000, ratio=1.072, hyp_len=24822, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.54-1.72.0.58-1.78.pth
BLEU = 67.01, 83.4/71.9/62.3/54.0 (BP=1.000, ratio=1.048, hyp_len=24283, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.58-1.78.0.59-1.81.pth
BLEU = 67.26, 83.4/72.0/62.5/54.6 (BP=1.000, ratio=1.053, hyp_len=24394, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.51-1.67.0.59-1.81.pth
BLEU = 69.38, 85.1/73.8/64.7/57.0 (BP=1.000, ratio=1.021, hyp_len=23655, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.51-1.66.0.61-1.83.pth
BLEU = 68.61, 84.4/73.1/63.9/56.3 (BP=1.000, ratio=1.037, hyp_len=24022, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.55-1.73.0.62-1.86.pth
BLEU = 69.59, 85.9/74.1/64.7/56.9 (BP=1.000, ratio=1.017, hyp_len=23563, ref_len=23160)

real	83m7.972s
user	81m43.864s
sys	3m4.223s
```

အများဆုံး ရတာက ...  

```
Evaluation result for the model: transformer-rl-model-myrk.1061.0.47-1.60.0.57-1.77.pth
BLEU = 70.48, 85.8/74.7/65.8/58.5 (BP=1.000, ratio=1.024, hyp_len=23723, ref_len=23160)
```

baseline က  

```
Evaluation result for the model: myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
BLEU = 73.04, 86.9/76.8/68.8/62.0 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
```

max_grad_norm ကို နောက်ထပ် value တစ်ခု ပေးကြည့်မလား?! max_grad_norm က ဘယ်လို အသေးစိတ်အလုပ်လုပ်သွားတယ်ဆိုတာကို လေ့လာရန်  
--max_grad_norm 30 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 1  --max_grad_norm 30 --n_epochs 1200
...
...
Validation - loss=5.8368e-01 ppl=1.79 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1194 - |param|=7.30e+02 |g_param|=2.55e+04 loss=4.6596e-01 ppl=1.59                                               
Validation - loss=5.4417e-01 ppl=1.72 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1195 - |param|=7.32e+02 |g_param|=5.01e+04 loss=4.5583e-01 ppl=1.58                                               
Validation - loss=5.7249e-01 ppl=1.77 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1196 - |param|=7.33e+02 |g_param|=4.85e+04 loss=4.5036e-01 ppl=1.57                                               
Validation - loss=5.6944e-01 ppl=1.77 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1197 - |param|=7.35e+02 |g_param|=2.59e+04 loss=4.6567e-01 ppl=1.59                                               
Validation - loss=5.6671e-01 ppl=1.76 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1198 - |param|=7.37e+02 |g_param|=2.77e+04 loss=4.8148e-01 ppl=1.62                                               
Validation - loss=5.5173e-01 ppl=1.74 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1199 - |param|=7.39e+02 |g_param|=1.35e+04 loss=5.1092e-01 ppl=1.67                                               
Validation - loss=6.0033e-01 ppl=1.82 best_loss=5.3010e-01 best_ppl=1.70                                                
Epoch 1200 - |param|=7.41e+02 |g_param|=1.52e+04 loss=4.8869e-01 ppl=1.63                                               
Validation - loss=5.3971e-01 ppl=1.72 best_loss=5.3010e-01 best_ppl=1.70                                                

real	205m56.200s
user	205m39.185s
sys	0m16.576s
```

testing/evaluation လုပ်ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 
...
...
...
Evaluation result for the model: transformer-rl-model-myrk.990.0.55-1.74.0.62-1.86.pth
BLEU = 67.21, 83.5/72.0/62.5/54.3 (BP=1.000, ratio=1.044, hyp_len=24168, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.991.0.55-1.73.0.59-1.81.pth
BLEU = 65.05, 82.2/70.1/60.1/51.7 (BP=1.000, ratio=1.060, hyp_len=24544, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.58-1.78.0.55-1.74.pth
BLEU = 67.34, 83.7/72.2/62.5/54.4 (BP=1.000, ratio=1.047, hyp_len=24254, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.54-1.72.0.58-1.78.pth
BLEU = 67.09, 83.6/72.0/62.3/54.1 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.53-1.71.0.59-1.80.pth
BLEU = 64.99, 81.3/69.7/60.2/52.3 (BP=1.000, ratio=1.074, hyp_len=24877, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.58-1.79.0.58-1.78.pth
BLEU = 67.96, 84.5/73.0/63.1/54.8 (BP=1.000, ratio=1.038, hyp_len=24043, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.54-1.72.0.60-1.82.pth
BLEU = 68.19, 84.0/72.9/63.6/55.6 (BP=1.000, ratio=1.042, hyp_len=24124, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.56-1.76.0.59-1.80.pth
BLEU = 63.83, 80.0/68.8/59.2/50.9 (BP=1.000, ratio=1.093, hyp_len=25317, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.55-1.73.0.57-1.77.pth
BLEU = 67.13, 83.0/71.7/62.4/54.7 (BP=1.000, ratio=1.056, hyp_len=24448, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.52-1.68.0.59-1.81.pth
BLEU = 65.02, 81.7/70.1/60.2/51.9 (BP=1.000, ratio=1.073, hyp_len=24851, ref_len=23160)

real	143m0.489s
user	140m28.009s
sys	5m14.155s
```

အများဆုံးက 70.44 ပဲ ထုတ်ပေးနိုင်တယ်...  

```
Evaluation result for the model: transformer-rl-model-myrk.1087.0.47-1.60.0.54-1.71.pth
BLEU = 70.44, 86.3/75.1/65.6/57.9 (BP=1.000, ratio=1.023, hyp_len=23693, ref_len=23160)
```

ဒီတစ်ခါတော့ --max_grad_norm 1e+9 --n_epochs 1100 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 32  --max_grad_norm 1e+9 --n_epochs 1100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/transformer-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 1100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 956
WARNING!!! You changed value for argument "--max_grad_norm".	Use current value: 1000000000.0
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 956,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 1000000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/transformer-rl-model-myrk.pth',
    'n_epochs': 1100,
    'n_layers': 6,
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
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/myrk-transformer/data/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1585, 32)
  (emb_dec): Embedding(1695, 32)
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
    (1): Linear(in_features=32, out_features=1695, bias=True)
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
Epoch 956 - |param|=3.89e+02 |g_param|=2.28e+05 loss=3.3001e-01 ppl=1.39                                                
Validation - loss=5.7108e-01 ppl=1.77 best_loss=inf best_ppl=inf                                                        
Epoch 957 - |param|=3.89e+02 |g_param|=2.38e+05 loss=2.9994e-01 ppl=1.35                                                ^[[5~
Validation - loss=5.8140e-01 ppl=1.79 best_loss=5.7108e-01 best_ppl=1.77                                                
Epoch 958 - |param|=3.89e+02 |g_param|=1.31e+05 loss=3.1323e-01 ppl=1.37                                                
Validation - loss=5.7514e-01 ppl=1.78 best_loss=5.7108e-01 best_ppl=1.77                                                
Epoch 959 - |param|=3.89e+02 |g_param|=6.38e+04 loss=3.0863e-01 ppl=1.36                                                
Validation - loss=5.7330e-01 ppl=1.77 best_loss=5.7108e-01 best_ppl=1.77                                                
Epoch 960 - |param|=3.90e+02 |g_param|=6.56e+04 loss=3.0285e-01 ppl=1.35                                                
Validation - loss=5.6756e-01 ppl=1.76 best_loss=5.7108e-01 best_ppl=1.77                                                
Epoch 961 - |param|=3.90e+02 |g_param|=7.02e+04 loss=3.1989e-01 ppl=1.38                                                
Validation - loss=5.6887e-01 ppl=1.77 best_loss=5.6756e-01 best_ppl=1.76                                                
Epoch 962 - |param|=3.90e+02 |g_param|=1.11e+05 loss=3.3667e-01 ppl=1.40                                                
Validation - loss=5.7058e-01 ppl=1.77 best_loss=5.6756e-01 best_ppl=1.76                                                
Epoch 963 - |param|=3.90e+02 |g_param|=6.93e+04 loss=3.1003e-01 ppl=1.36                                                
Validation - loss=5.6088e-01 ppl=1.75 best_loss=5.6756e-01 best_ppl=1.76                                                
Epoch 964 - |param|=3.90e+02 |g_param|=9.84e+04 loss=3.0733e-01 ppl=1.36                                                
Validation - loss=5.8499e-01 ppl=1.79 best_loss=5.6088e-01 best_ppl=1.75                                                
Epoch 965 - |param|=3.90e+02 |g_param|=6.09e+04 loss=3.2087e-01 ppl=1.38                                                
Validation - loss=5.6074e-01 ppl=1.75 best_loss=5.6088e-01 best_ppl=1.75                                                
Epoch 966 - |param|=3.90e+02 |g_param|=6.22e+04 loss=3.0557e-01 ppl=1.36                                                
Validation - loss=5.6433e-01 ppl=1.76 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 967 - |param|=3.90e+02 |g_param|=1.06e+05 loss=3.3700e-01 ppl=1.40                                                
Validation - loss=5.8759e-01 ppl=1.80 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 968 - |param|=3.90e+02 |g_param|=5.23e+04 loss=3.0080e-01 ppl=1.35                                                
Validation - loss=5.6833e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 969 - |param|=3.90e+02 |g_param|=5.24e+04 loss=3.1269e-01 ppl=1.37                                                
Validation - loss=5.7230e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 970 - |param|=3.90e+02 |g_param|=4.53e+04 loss=3.2334e-01 ppl=1.38                                                
Validation - loss=5.8331e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 971 - |param|=3.90e+02 |g_param|=6.33e+04 loss=3.0074e-01 ppl=1.35                                                
Validation - loss=5.7882e-01 ppl=1.78 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 972 - |param|=3.90e+02 |g_param|=8.13e+04 loss=3.4502e-01 ppl=1.41                                                
Validation - loss=5.7125e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 973 - |param|=3.90e+02 |g_param|=5.11e+04 loss=2.9752e-01 ppl=1.35                                                
Validation - loss=5.7133e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 974 - |param|=3.90e+02 |g_param|=4.34e+04 loss=3.1096e-01 ppl=1.36                                                
Validation - loss=5.6514e-01 ppl=1.76 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 975 - |param|=3.90e+02 |g_param|=7.27e+04 loss=3.0902e-01 ppl=1.36                                                
Validation - loss=5.7983e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 976 - |param|=3.91e+02 |g_param|=1.28e+05 loss=3.5833e-01 ppl=1.43                                                
Validation - loss=6.1794e-01 ppl=1.86 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 977 - |param|=3.91e+02 |g_param|=6.41e+04 loss=2.8928e-01 ppl=1.34                                                
Validation - loss=5.7284e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 978 - |param|=3.91e+02 |g_param|=5.45e+04 loss=2.9500e-01 ppl=1.34                                                
Validation - loss=5.8484e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 979 - |param|=3.91e+02 |g_param|=7.20e+04 loss=3.1357e-01 ppl=1.37                                                
Validation - loss=5.8294e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 980 - |param|=3.91e+02 |g_param|=5.09e+04 loss=3.2856e-01 ppl=1.39                                                
Validation - loss=5.8209e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 981 - |param|=3.91e+02 |g_param|=8.10e+04 loss=3.2382e-01 ppl=1.38                                                
Validation - loss=6.0068e-01 ppl=1.82 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 982 - |param|=3.91e+02 |g_param|=7.41e+04 loss=3.1936e-01 ppl=1.38                                                
Validation - loss=5.9096e-01 ppl=1.81 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 983 - |param|=3.91e+02 |g_param|=8.70e+04 loss=3.2351e-01 ppl=1.38                                                
Validation - loss=5.6973e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 984 - |param|=3.91e+02 |g_param|=5.31e+04 loss=3.0210e-01 ppl=1.35                                                
Validation - loss=5.6612e-01 ppl=1.76 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 985 - |param|=3.91e+02 |g_param|=5.16e+04 loss=2.9720e-01 ppl=1.35                                                
Validation - loss=5.7067e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 986 - |param|=3.91e+02 |g_param|=5.22e+04 loss=2.9925e-01 ppl=1.35                                                
Validation - loss=5.8352e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 987 - |param|=3.91e+02 |g_param|=1.29e+05 loss=3.1123e-01 ppl=1.37                                                
Validation - loss=5.8626e-01 ppl=1.80 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 988 - |param|=3.91e+02 |g_param|=5.07e+04 loss=3.2151e-01 ppl=1.38                                                
Validation - loss=5.7033e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 989 - |param|=3.91e+02 |g_param|=5.80e+04 loss=3.0601e-01 ppl=1.36                                                
Validation - loss=5.7067e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 990 - |param|=3.91e+02 |g_param|=5.51e+04 loss=3.2192e-01 ppl=1.38                                                
Validation - loss=5.7774e-01 ppl=1.78 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 991 - |param|=3.91e+02 |g_param|=8.38e+04 loss=3.1501e-01 ppl=1.37                                                
Validation - loss=5.7427e-01 ppl=1.78 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 992 - |param|=3.92e+02 |g_param|=6.18e+04 loss=2.8903e-01 ppl=1.34                                                
Validation - loss=5.6887e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 993 - |param|=3.92e+02 |g_param|=6.65e+04 loss=3.0926e-01 ppl=1.36                                                
Validation - loss=5.7136e-01 ppl=1.77 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 994 - |param|=3.92e+02 |g_param|=5.74e+04 loss=2.9341e-01 ppl=1.34                                                
Validation - loss=5.7849e-01 ppl=1.78 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 995 - |param|=3.92e+02 |g_param|=5.64e+04 loss=3.2152e-01 ppl=1.38                                                
Validation - loss=5.7393e-01 ppl=1.78 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 996 - |param|=3.92e+02 |g_param|=7.50e+04 loss=3.1596e-01 ppl=1.37                                                
Validation - loss=5.7997e-01 ppl=1.79 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 997 - |param|=3.92e+02 |g_param|=1.03e+05 loss=3.1695e-01 ppl=1.37                                                
Validation - loss=5.5915e-01 ppl=1.75 best_loss=5.6074e-01 best_ppl=1.75                                                
Epoch 998 - |param|=3.92e+02 |g_param|=7.73e+04 loss=3.1224e-01 ppl=1.37                                                
Validation - loss=5.5870e-01 ppl=1.75 best_loss=5.5915e-01 best_ppl=1.75                                                
Epoch 999 - |param|=3.92e+02 |g_param|=5.36e+04 loss=3.1184e-01 ppl=1.37                                                
Validation - loss=5.6593e-01 ppl=1.76 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1000 - |param|=3.92e+02 |g_param|=5.13e+04 loss=3.1662e-01 ppl=1.37                                               
Validation - loss=5.7202e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1001 - |param|=3.92e+02 |g_param|=9.11e+04 loss=3.2709e-01 ppl=1.39                                               
Validation - loss=5.6842e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1002 - |param|=3.92e+02 |g_param|=1.01e+05 loss=3.1443e-01 ppl=1.37                                               
Validation - loss=5.7724e-01 ppl=1.78 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1003 - |param|=3.92e+02 |g_param|=9.23e+04 loss=3.1303e-01 ppl=1.37                                               
Validation - loss=5.7056e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1004 - |param|=3.92e+02 |g_param|=6.46e+04 loss=3.1168e-01 ppl=1.37                                               
Validation - loss=5.6818e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1005 - |param|=3.92e+02 |g_param|=6.44e+04 loss=3.0356e-01 ppl=1.35                                               
Validation - loss=5.6054e-01 ppl=1.75 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1006 - |param|=3.92e+02 |g_param|=6.09e+04 loss=2.8804e-01 ppl=1.33                                               
Validation - loss=5.7499e-01 ppl=1.78 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1007 - |param|=3.93e+02 |g_param|=1.24e+05 loss=3.0957e-01 ppl=1.36                                               
Validation - loss=5.8983e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1008 - |param|=3.93e+02 |g_param|=6.23e+04 loss=3.1585e-01 ppl=1.37                                               
Validation - loss=5.6766e-01 ppl=1.76 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1009 - |param|=3.93e+02 |g_param|=5.56e+04 loss=2.9578e-01 ppl=1.34                                               
Validation - loss=5.6971e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1010 - |param|=3.93e+02 |g_param|=4.69e+04 loss=3.1897e-01 ppl=1.38                                               
Validation - loss=5.6703e-01 ppl=1.76 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1011 - |param|=3.93e+02 |g_param|=7.23e+04 loss=3.3482e-01 ppl=1.40                                               
Validation - loss=5.7213e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1012 - |param|=3.93e+02 |g_param|=6.67e+04 loss=3.2244e-01 ppl=1.38                                               
Validation - loss=5.7757e-01 ppl=1.78 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1013 - |param|=3.93e+02 |g_param|=6.23e+04 loss=2.9744e-01 ppl=1.35                                               
Validation - loss=5.7337e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1014 - |param|=3.93e+02 |g_param|=5.43e+04 loss=3.0639e-01 ppl=1.36                                               
Validation - loss=5.8348e-01 ppl=1.79 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1015 - |param|=3.93e+02 |g_param|=8.39e+04 loss=3.0812e-01 ppl=1.36                                               
Validation - loss=6.0346e-01 ppl=1.83 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1016 - |param|=3.93e+02 |g_param|=6.60e+04 loss=3.0112e-01 ppl=1.35                                               
Validation - loss=5.9051e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1017 - |param|=3.93e+02 |g_param|=6.35e+04 loss=3.0457e-01 ppl=1.36                                               
Validation - loss=5.8870e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1018 - |param|=3.93e+02 |g_param|=6.10e+04 loss=3.0679e-01 ppl=1.36                                               
Validation - loss=5.8546e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1019 - |param|=3.93e+02 |g_param|=4.69e+04 loss=3.1398e-01 ppl=1.37                                               
Validation - loss=5.8848e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1020 - |param|=3.93e+02 |g_param|=7.21e+04 loss=3.1477e-01 ppl=1.37                                               
Validation - loss=5.7825e-01 ppl=1.78 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1021 - |param|=3.93e+02 |g_param|=6.38e+04 loss=3.1663e-01 ppl=1.37                                               
Validation - loss=5.7892e-01 ppl=1.78 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1022 - |param|=3.94e+02 |g_param|=8.03e+04 loss=2.9010e-01 ppl=1.34                                               
Validation - loss=5.9053e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1023 - |param|=3.94e+02 |g_param|=6.18e+04 loss=3.1018e-01 ppl=1.36                                               
Validation - loss=5.7144e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1024 - |param|=3.94e+02 |g_param|=7.96e+04 loss=3.1787e-01 ppl=1.37                                               
Validation - loss=5.8797e-01 ppl=1.80 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1025 - |param|=3.94e+02 |g_param|=1.39e+05 loss=3.1043e-01 ppl=1.36                                               
Validation - loss=5.6425e-01 ppl=1.76 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1026 - |param|=3.94e+02 |g_param|=1.22e+05 loss=2.9497e-01 ppl=1.34                                               
Validation - loss=5.6751e-01 ppl=1.76 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1027 - |param|=3.94e+02 |g_param|=1.12e+05 loss=3.1630e-01 ppl=1.37                                               
Validation - loss=5.6998e-01 ppl=1.77 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1028 - |param|=3.94e+02 |g_param|=1.90e+05 loss=3.0459e-01 ppl=1.36                                               
Validation - loss=5.5158e-01 ppl=1.74 best_loss=5.5870e-01 best_ppl=1.75                                                
Epoch 1029 - |param|=3.94e+02 |g_param|=2.03e+05 loss=3.0635e-01 ppl=1.36                                               
Validation - loss=5.7820e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1030 - |param|=3.94e+02 |g_param|=1.40e+05 loss=2.7356e-01 ppl=1.31                                               
Validation - loss=5.6943e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1031 - |param|=3.94e+02 |g_param|=1.17e+05 loss=2.9309e-01 ppl=1.34                                               
Validation - loss=5.7603e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1032 - |param|=3.94e+02 |g_param|=1.24e+05 loss=2.9141e-01 ppl=1.34                                               
Validation - loss=5.8338e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1033 - |param|=3.94e+02 |g_param|=2.23e+05 loss=3.0388e-01 ppl=1.36                                               
Validation - loss=5.7081e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1034 - |param|=3.94e+02 |g_param|=2.28e+05 loss=3.0640e-01 ppl=1.36                                               
Validation - loss=5.6594e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1035 - |param|=3.94e+02 |g_param|=9.25e+04 loss=3.0192e-01 ppl=1.35                                               
Validation - loss=5.6929e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1036 - |param|=3.94e+02 |g_param|=1.09e+05 loss=2.9230e-01 ppl=1.34                                               
Validation - loss=5.6374e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1037 - |param|=3.94e+02 |g_param|=1.17e+05 loss=3.4165e-01 ppl=1.41                                               
Validation - loss=5.7600e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1038 - |param|=3.95e+02 |g_param|=1.59e+05 loss=3.1016e-01 ppl=1.36                                               
Validation - loss=5.8531e-01 ppl=1.80 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1039 - |param|=3.95e+02 |g_param|=9.13e+04 loss=3.0697e-01 ppl=1.36                                               
Validation - loss=5.6451e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1040 - |param|=3.95e+02 |g_param|=1.14e+05 loss=3.3271e-01 ppl=1.39                                               
Validation - loss=5.7743e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1041 - |param|=3.95e+02 |g_param|=6.05e+04 loss=2.8383e-01 ppl=1.33                                               
Validation - loss=5.6298e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1042 - |param|=3.95e+02 |g_param|=1.13e+05 loss=3.1759e-01 ppl=1.37                                               
Validation - loss=5.7718e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1043 - |param|=3.95e+02 |g_param|=8.41e+04 loss=2.9635e-01 ppl=1.34                                               
Validation - loss=5.7780e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1044 - |param|=3.95e+02 |g_param|=6.14e+04 loss=3.0534e-01 ppl=1.36                                               
Validation - loss=5.8940e-01 ppl=1.80 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1045 - |param|=3.95e+02 |g_param|=5.42e+04 loss=2.8843e-01 ppl=1.33                                               
Validation - loss=6.0151e-01 ppl=1.82 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1046 - |param|=3.95e+02 |g_param|=9.01e+04 loss=3.1310e-01 ppl=1.37                                               
Validation - loss=5.8235e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1047 - |param|=3.95e+02 |g_param|=8.56e+04 loss=3.0686e-01 ppl=1.36                                               
Validation - loss=5.7511e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1048 - |param|=3.95e+02 |g_param|=5.57e+04 loss=2.9259e-01 ppl=1.34                                               
Validation - loss=5.5957e-01 ppl=1.75 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1049 - |param|=3.95e+02 |g_param|=6.57e+04 loss=2.9492e-01 ppl=1.34                                               
Validation - loss=5.9961e-01 ppl=1.82 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1050 - |param|=3.95e+02 |g_param|=7.90e+04 loss=2.9937e-01 ppl=1.35                                               
Validation - loss=5.6789e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1051 - |param|=3.95e+02 |g_param|=6.02e+04 loss=3.0417e-01 ppl=1.36                                               
Validation - loss=5.7424e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1052 - |param|=3.95e+02 |g_param|=7.98e+04 loss=2.7872e-01 ppl=1.32                                               
Validation - loss=5.7740e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1053 - |param|=3.96e+02 |g_param|=6.03e+04 loss=3.0783e-01 ppl=1.36                                               
Validation - loss=5.7643e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1054 - |param|=3.96e+02 |g_param|=5.99e+04 loss=3.0522e-01 ppl=1.36                                               
Validation - loss=5.7944e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1055 - |param|=3.96e+02 |g_param|=7.48e+04 loss=3.2001e-01 ppl=1.38                                               
Validation - loss=5.5920e-01 ppl=1.75 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1056 - |param|=3.96e+02 |g_param|=5.59e+04 loss=3.0612e-01 ppl=1.36                                               
Validation - loss=5.6924e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1057 - |param|=3.96e+02 |g_param|=8.89e+04 loss=3.1739e-01 ppl=1.37                                               
Validation - loss=5.6893e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1058 - |param|=3.96e+02 |g_param|=6.37e+04 loss=3.0671e-01 ppl=1.36                                               
Validation - loss=5.7662e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1059 - |param|=3.96e+02 |g_param|=7.30e+04 loss=2.7970e-01 ppl=1.32                                               
Validation - loss=5.8046e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1060 - |param|=3.96e+02 |g_param|=6.23e+04 loss=3.0890e-01 ppl=1.36                                               
Validation - loss=5.6790e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1061 - |param|=3.96e+02 |g_param|=6.75e+04 loss=3.0288e-01 ppl=1.35                                               
Validation - loss=5.7953e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1062 - |param|=3.96e+02 |g_param|=7.11e+04 loss=2.9495e-01 ppl=1.34                                               
Validation - loss=5.7883e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1063 - |param|=3.96e+02 |g_param|=6.67e+04 loss=3.3122e-01 ppl=1.39                                               
Validation - loss=5.8045e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1064 - |param|=3.96e+02 |g_param|=6.07e+04 loss=3.1356e-01 ppl=1.37                                               
Validation - loss=5.8323e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1065 - |param|=3.96e+02 |g_param|=6.37e+04 loss=2.9579e-01 ppl=1.34                                               
Validation - loss=5.7116e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1066 - |param|=3.96e+02 |g_param|=8.08e+04 loss=3.1791e-01 ppl=1.37                                               
Validation - loss=6.1451e-01 ppl=1.85 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1067 - |param|=3.96e+02 |g_param|=8.18e+04 loss=3.0190e-01 ppl=1.35                                               
Validation - loss=5.8929e-01 ppl=1.80 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1068 - |param|=3.96e+02 |g_param|=5.49e+04 loss=3.0192e-01 ppl=1.35                                               
Validation - loss=5.9059e-01 ppl=1.81 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1069 - |param|=3.97e+02 |g_param|=7.69e+04 loss=3.1085e-01 ppl=1.36                                               
Validation - loss=5.7781e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1070 - |param|=3.97e+02 |g_param|=1.02e+05 loss=3.1442e-01 ppl=1.37                                               
Validation - loss=5.8125e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1071 - |param|=3.97e+02 |g_param|=6.58e+04 loss=3.1573e-01 ppl=1.37                                               
Validation - loss=5.8798e-01 ppl=1.80 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1072 - |param|=3.97e+02 |g_param|=7.01e+04 loss=3.0923e-01 ppl=1.36                                               
Validation - loss=6.0831e-01 ppl=1.84 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1073 - |param|=3.97e+02 |g_param|=5.55e+04 loss=2.9484e-01 ppl=1.34                                               
Validation - loss=5.8424e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1074 - |param|=3.97e+02 |g_param|=5.76e+04 loss=3.0893e-01 ppl=1.36                                               
Validation - loss=5.9454e-01 ppl=1.81 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1075 - |param|=3.97e+02 |g_param|=1.30e+05 loss=3.1646e-01 ppl=1.37                                               
Validation - loss=5.8021e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1076 - |param|=3.97e+02 |g_param|=7.55e+04 loss=3.2513e-01 ppl=1.38                                               
Validation - loss=5.6961e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1077 - |param|=3.97e+02 |g_param|=5.87e+04 loss=2.8825e-01 ppl=1.33                                               
Validation - loss=5.7213e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1078 - |param|=3.97e+02 |g_param|=1.65e+05 loss=3.3170e-01 ppl=1.39                                               
Validation - loss=5.7856e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1079 - |param|=3.97e+02 |g_param|=4.91e+04 loss=3.1825e-01 ppl=1.37                                               
Validation - loss=5.8004e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1080 - |param|=3.97e+02 |g_param|=6.54e+04 loss=2.9757e-01 ppl=1.35                                               
Validation - loss=5.7735e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1081 - |param|=3.97e+02 |g_param|=9.73e+04 loss=3.1040e-01 ppl=1.36                                               
Validation - loss=5.9825e-01 ppl=1.82 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1082 - |param|=3.97e+02 |g_param|=5.96e+04 loss=2.9490e-01 ppl=1.34                                               
Validation - loss=5.6906e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1083 - |param|=3.97e+02 |g_param|=6.85e+04 loss=3.1502e-01 ppl=1.37                                               
Validation - loss=5.7658e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1084 - |param|=3.98e+02 |g_param|=5.52e+04 loss=3.0302e-01 ppl=1.35                                               
Validation - loss=5.7187e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1085 - |param|=3.98e+02 |g_param|=5.04e+04 loss=3.1782e-01 ppl=1.37                                               
Validation - loss=5.7893e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1086 - |param|=3.98e+02 |g_param|=6.36e+04 loss=3.0890e-01 ppl=1.36                                               
Validation - loss=5.8048e-01 ppl=1.79 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1087 - |param|=3.98e+02 |g_param|=6.23e+04 loss=2.9712e-01 ppl=1.35                                               
Validation - loss=5.7579e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1088 - |param|=3.98e+02 |g_param|=1.05e+05 loss=3.1488e-01 ppl=1.37                                               
Validation - loss=5.7725e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1089 - |param|=3.98e+02 |g_param|=1.03e+05 loss=2.9160e-01 ppl=1.34                                               
Validation - loss=5.7529e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1090 - |param|=3.98e+02 |g_param|=7.22e+04 loss=2.8346e-01 ppl=1.33                                               
Validation - loss=5.7132e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1091 - |param|=3.98e+02 |g_param|=8.07e+04 loss=3.1597e-01 ppl=1.37                                               
Validation - loss=5.7044e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1092 - |param|=3.98e+02 |g_param|=8.83e+04 loss=2.9659e-01 ppl=1.35                                               
Validation - loss=5.7235e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1093 - |param|=3.98e+02 |g_param|=6.49e+04 loss=2.8715e-01 ppl=1.33                                               
Validation - loss=5.7832e-01 ppl=1.78 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1094 - |param|=3.98e+02 |g_param|=6.13e+04 loss=2.7898e-01 ppl=1.32                                               
Validation - loss=5.7378e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1095 - |param|=3.98e+02 |g_param|=1.18e+05 loss=2.8338e-01 ppl=1.33                                               
Validation - loss=5.8572e-01 ppl=1.80 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1096 - |param|=3.98e+02 |g_param|=7.57e+04 loss=2.9771e-01 ppl=1.35                                               
Validation - loss=5.6452e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1097 - |param|=3.98e+02 |g_param|=5.10e+04 loss=3.0335e-01 ppl=1.35                                               
Validation - loss=5.6940e-01 ppl=1.77 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1098 - |param|=3.98e+02 |g_param|=5.27e+04 loss=2.7058e-01 ppl=1.31                                               
Validation - loss=5.6335e-01 ppl=1.76 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1099 - |param|=3.98e+02 |g_param|=7.00e+04 loss=2.9298e-01 ppl=1.34                                               
Validation - loss=6.0204e-01 ppl=1.83 best_loss=5.5158e-01 best_ppl=1.74                                                
Epoch 1100 - |param|=3.99e+02 |g_param|=7.39e+04 loss=3.1289e-01 ppl=1.37                                               
Validation - loss=5.9319e-01 ppl=1.81 best_loss=5.5158e-01 best_ppl=1.74                                                

real	88m8.073s
user	87m50.848s
sys	0m11.308s
```

ppl တော့ 1.37, 1.31 etc. ကျလာတာကို တွေ့ရတယ်...  
"--max_grad_norm 1e+9 --n_epochs 1100" RL fine-tuning မော်ဒယ်ကို testing/evaluation လုပ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-model-myrk.1000.0.32-1.37.0.57-1.77.pth
BLEU = 72.15, 86.4/76.2/67.8/60.8 (BP=1.000, ratio=1.034, hyp_len=23949, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1001.0.33-1.39.0.57-1.77.pth
BLEU = 71.98, 86.2/75.9/67.6/60.6 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1002.0.31-1.37.0.58-1.78.pth
BLEU = 71.83, 86.2/75.8/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1003.0.31-1.37.0.57-1.77.pth
BLEU = 71.72, 86.1/75.7/67.4/60.2 (BP=1.000, ratio=1.039, hyp_len=24074, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1004.0.31-1.37.0.57-1.77.pth
BLEU = 73.01, 86.9/76.8/68.7/62.0 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1005.0.30-1.35.0.56-1.75.pth
BLEU = 71.99, 86.3/75.9/67.6/60.6 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1006.0.29-1.33.0.57-1.78.pth
BLEU = 72.45, 86.8/76.3/68.0/61.1 (BP=1.000, ratio=1.032, hyp_len=23890, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1007.0.31-1.36.0.59-1.80.pth
BLEU = 71.30, 86.0/75.4/66.8/59.6 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1008.0.32-1.37.0.57-1.76.pth
BLEU = 72.89, 86.9/76.8/68.6/61.7 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1009.0.30-1.34.0.57-1.77.pth
BLEU = 72.10, 86.7/76.2/67.7/60.5 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1010.0.32-1.38.0.57-1.76.pth
BLEU = 71.61, 86.2/75.7/67.1/60.0 (BP=1.000, ratio=1.038, hyp_len=24032, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1011.0.33-1.40.0.57-1.77.pth
BLEU = 71.13, 85.8/75.3/66.7/59.4 (BP=1.000, ratio=1.042, hyp_len=24133, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1012.0.32-1.38.0.58-1.78.pth
BLEU = 72.22, 86.5/76.2/67.8/60.8 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1013.0.30-1.35.0.57-1.77.pth
BLEU = 71.04, 85.8/75.3/66.6/59.2 (BP=1.000, ratio=1.042, hyp_len=24134, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1014.0.31-1.36.0.58-1.79.pth
BLEU = 71.36, 85.9/75.5/66.9/59.8 (BP=1.000, ratio=1.041, hyp_len=24101, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1015.0.31-1.36.0.60-1.83.pth
BLEU = 70.79, 85.7/75.1/66.3/58.9 (BP=1.000, ratio=1.045, hyp_len=24192, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1016.0.30-1.35.0.59-1.80.pth
BLEU = 71.30, 86.0/75.4/66.8/59.6 (BP=1.000, ratio=1.043, hyp_len=24155, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1017.0.30-1.36.0.59-1.80.pth
BLEU = 71.11, 85.9/75.3/66.7/59.3 (BP=1.000, ratio=1.040, hyp_len=24084, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1018.0.31-1.36.0.59-1.80.pth
BLEU = 72.25, 86.5/76.2/67.8/60.9 (BP=1.000, ratio=1.035, hyp_len=23964, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1019.0.31-1.37.0.59-1.80.pth
BLEU = 71.71, 86.4/75.9/67.3/60.0 (BP=1.000, ratio=1.036, hyp_len=24003, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1020.0.31-1.37.0.58-1.78.pth
BLEU = 72.09, 86.4/76.1/67.7/60.7 (BP=1.000, ratio=1.037, hyp_len=24016, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1021.0.32-1.37.0.58-1.78.pth
BLEU = 72.51, 86.8/76.5/68.1/61.1 (BP=1.000, ratio=1.030, hyp_len=23856, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1022.0.29-1.34.0.59-1.80.pth
BLEU = 72.59, 86.8/76.5/68.2/61.3 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1023.0.31-1.36.0.57-1.77.pth
BLEU = 71.73, 86.1/75.8/67.3/60.3 (BP=1.000, ratio=1.039, hyp_len=24063, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1024.0.32-1.37.0.59-1.80.pth
BLEU = 71.27, 86.0/75.5/66.8/59.5 (BP=1.000, ratio=1.041, hyp_len=24113, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1025.0.31-1.36.0.56-1.76.pth
BLEU = 71.12, 86.1/75.4/66.6/59.2 (BP=1.000, ratio=1.042, hyp_len=24143, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1026.0.29-1.34.0.57-1.76.pth
BLEU = 71.83, 86.3/76.0/67.4/60.3 (BP=1.000, ratio=1.037, hyp_len=24024, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1027.0.32-1.37.0.57-1.77.pth
BLEU = 71.98, 86.2/75.9/67.6/60.6 (BP=1.000, ratio=1.037, hyp_len=24012, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1028.0.30-1.36.0.55-1.74.pth
BLEU = 72.27, 86.5/76.3/67.9/60.9 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1029.0.31-1.36.0.58-1.78.pth
BLEU = 71.47, 85.9/75.4/67.0/60.1 (BP=1.000, ratio=1.040, hyp_len=24083, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1030.0.27-1.31.0.57-1.77.pth
BLEU = 72.66, 86.7/76.6/68.3/61.4 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1031.0.29-1.34.0.58-1.78.pth
BLEU = 71.68, 86.2/75.7/67.2/60.1 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1032.0.29-1.34.0.58-1.79.pth
BLEU = 71.99, 86.5/76.0/67.6/60.5 (BP=1.000, ratio=1.036, hyp_len=24001, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1033.0.30-1.36.0.57-1.77.pth
BLEU = 72.39, 86.5/76.3/68.1/61.2 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1034.0.31-1.36.0.57-1.76.pth
BLEU = 71.66, 86.1/75.7/67.3/60.1 (BP=1.000, ratio=1.040, hyp_len=24088, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1035.0.30-1.35.0.57-1.77.pth
BLEU = 71.13, 85.9/75.3/66.7/59.4 (BP=1.000, ratio=1.042, hyp_len=24131, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1036.0.29-1.34.0.56-1.76.pth
BLEU = 71.50, 86.1/75.6/67.0/59.9 (BP=1.000, ratio=1.040, hyp_len=24095, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1037.0.34-1.41.0.58-1.78.pth
BLEU = 72.03, 86.5/76.0/67.6/60.6 (BP=1.000, ratio=1.036, hyp_len=24005, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1038.0.31-1.36.0.59-1.80.pth
BLEU = 70.98, 85.9/75.3/66.5/59.1 (BP=1.000, ratio=1.041, hyp_len=24113, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1039.0.31-1.36.0.56-1.76.pth
BLEU = 71.44, 86.2/75.6/66.9/59.7 (BP=1.000, ratio=1.039, hyp_len=24070, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1040.0.33-1.39.0.58-1.78.pth
BLEU = 71.60, 86.2/75.7/67.2/60.0 (BP=1.000, ratio=1.035, hyp_len=23972, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1041.0.28-1.33.0.56-1.76.pth
BLEU = 71.84, 86.1/75.8/67.5/60.5 (BP=1.000, ratio=1.035, hyp_len=23977, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1042.0.32-1.37.0.58-1.78.pth
BLEU = 70.79, 85.9/75.1/66.2/58.7 (BP=1.000, ratio=1.041, hyp_len=24119, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1043.0.30-1.34.0.58-1.78.pth
BLEU = 72.26, 86.5/76.2/67.9/60.9 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1044.0.31-1.36.0.59-1.80.pth
BLEU = 72.24, 86.6/76.2/67.8/60.9 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1045.0.29-1.33.0.60-1.82.pth
BLEU = 71.59, 86.1/75.7/67.1/60.0 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1046.0.31-1.37.0.58-1.79.pth
BLEU = 71.29, 86.1/75.5/66.8/59.5 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1047.0.31-1.36.0.58-1.78.pth
BLEU = 72.23, 86.3/76.1/67.9/61.0 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1048.0.29-1.34.0.56-1.75.pth
BLEU = 72.21, 86.4/76.2/67.9/60.8 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1049.0.29-1.34.0.60-1.82.pth
BLEU = 72.61, 86.8/76.6/68.2/61.3 (BP=1.000, ratio=1.028, hyp_len=23807, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1050.0.30-1.35.0.57-1.76.pth
BLEU = 72.97, 86.9/76.8/68.7/61.9 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1051.0.30-1.36.0.57-1.78.pth
BLEU = 72.20, 86.4/76.2/67.9/60.8 (BP=1.000, ratio=1.036, hyp_len=23984, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1052.0.28-1.32.0.58-1.78.pth
BLEU = 72.69, 86.8/76.5/68.3/61.6 (BP=1.000, ratio=1.029, hyp_len=23842, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1053.0.31-1.36.0.58-1.78.pth
BLEU = 72.50, 86.6/76.4/68.1/61.3 (BP=1.000, ratio=1.033, hyp_len=23918, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1054.0.31-1.36.0.58-1.79.pth
BLEU = 71.63, 86.1/75.7/67.2/60.1 (BP=1.000, ratio=1.041, hyp_len=24106, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1055.0.32-1.38.0.56-1.75.pth
BLEU = 71.64, 86.0/75.7/67.3/60.2 (BP=1.000, ratio=1.041, hyp_len=24103, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1056.0.31-1.36.0.57-1.77.pth
BLEU = 72.48, 86.7/76.4/68.1/61.2 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1057.0.32-1.37.0.57-1.77.pth
BLEU = 71.48, 86.0/75.6/67.1/59.9 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1058.0.31-1.36.0.58-1.78.pth
BLEU = 71.84, 86.3/75.9/67.5/60.2 (BP=1.000, ratio=1.039, hyp_len=24072, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1059.0.28-1.32.0.58-1.79.pth
BLEU = 72.38, 86.6/76.3/68.0/61.1 (BP=1.000, ratio=1.033, hyp_len=23924, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1060.0.31-1.36.0.57-1.76.pth
BLEU = 71.60, 86.1/75.7/67.2/60.0 (BP=1.000, ratio=1.039, hyp_len=24063, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1061.0.30-1.35.0.58-1.79.pth
BLEU = 70.82, 85.7/75.2/66.3/58.8 (BP=1.000, ratio=1.043, hyp_len=24159, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1062.0.29-1.34.0.58-1.78.pth
BLEU = 71.29, 85.8/75.4/66.9/59.7 (BP=1.000, ratio=1.044, hyp_len=24174, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1063.0.33-1.39.0.58-1.79.pth
BLEU = 71.49, 86.1/75.7/67.1/59.8 (BP=1.000, ratio=1.040, hyp_len=24076, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1064.0.31-1.37.0.58-1.79.pth
BLEU = 71.78, 86.4/75.9/67.3/60.1 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1065.0.30-1.34.0.57-1.77.pth
BLEU = 71.06, 85.7/75.2/66.6/59.4 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1066.0.32-1.37.0.61-1.85.pth
BLEU = 70.97, 85.7/75.2/66.5/59.2 (BP=1.000, ratio=1.044, hyp_len=24182, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1067.0.30-1.35.0.59-1.80.pth
BLEU = 72.27, 86.6/76.3/67.8/60.9 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1068.0.30-1.35.0.59-1.81.pth
BLEU = 71.74, 86.1/75.8/67.4/60.2 (BP=1.000, ratio=1.039, hyp_len=24060, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1069.0.31-1.36.0.58-1.78.pth
BLEU = 72.36, 86.6/76.3/68.0/61.0 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1070.0.31-1.37.0.58-1.79.pth
BLEU = 71.28, 86.1/75.5/66.7/59.5 (BP=1.000, ratio=1.043, hyp_len=24161, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1071.0.32-1.37.0.59-1.80.pth
BLEU = 70.81, 85.7/75.0/66.3/59.0 (BP=1.000, ratio=1.044, hyp_len=24173, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1072.0.31-1.36.0.61-1.84.pth
BLEU = 72.30, 86.7/76.4/67.9/60.8 (BP=1.000, ratio=1.036, hyp_len=23986, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1073.0.29-1.34.0.58-1.79.pth
BLEU = 72.31, 86.7/76.3/67.9/60.8 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1074.0.31-1.36.0.59-1.81.pth
BLEU = 72.07, 86.5/76.1/67.7/60.5 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1075.0.32-1.37.0.58-1.79.pth
BLEU = 71.12, 86.0/75.4/66.6/59.3 (BP=1.000, ratio=1.042, hyp_len=24124, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1076.0.33-1.38.0.57-1.77.pth
BLEU = 71.62, 85.9/75.5/67.3/60.3 (BP=1.000, ratio=1.041, hyp_len=24101, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1077.0.29-1.33.0.57-1.77.pth
BLEU = 72.13, 86.3/76.1/67.8/60.8 (BP=1.000, ratio=1.037, hyp_len=24016, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1078.0.33-1.39.0.58-1.78.pth
BLEU = 71.81, 86.0/75.8/67.5/60.4 (BP=1.000, ratio=1.042, hyp_len=24132, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1079.0.32-1.37.0.58-1.79.pth
BLEU = 71.77, 86.3/75.8/67.4/60.2 (BP=1.000, ratio=1.037, hyp_len=24016, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1080.0.30-1.35.0.58-1.78.pth
BLEU = 71.09, 85.7/75.2/66.7/59.5 (BP=1.000, ratio=1.044, hyp_len=24169, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1081.0.31-1.36.0.60-1.82.pth
BLEU = 72.91, 86.9/76.8/68.6/61.7 (BP=1.000, ratio=1.025, hyp_len=23729, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1082.0.29-1.34.0.57-1.77.pth
BLEU = 71.47, 85.9/75.6/67.1/59.9 (BP=1.000, ratio=1.044, hyp_len=24172, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1083.0.32-1.37.0.58-1.78.pth
BLEU = 72.24, 86.4/76.2/67.9/60.9 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1084.0.30-1.35.0.57-1.77.pth
BLEU = 71.80, 86.2/75.9/67.4/60.3 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1085.0.32-1.37.0.58-1.78.pth
BLEU = 72.02, 86.4/76.2/67.6/60.4 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1086.0.31-1.36.0.58-1.79.pth
BLEU = 71.70, 86.3/75.8/67.2/60.0 (BP=1.000, ratio=1.038, hyp_len=24042, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1087.0.30-1.35.0.58-1.78.pth
BLEU = 72.14, 86.3/76.1/67.8/60.8 (BP=1.000, ratio=1.038, hyp_len=24037, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1088.0.31-1.37.0.58-1.78.pth
BLEU = 71.78, 86.1/75.8/67.4/60.3 (BP=1.000, ratio=1.037, hyp_len=24010, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1089.0.29-1.34.0.58-1.78.pth
BLEU = 71.23, 85.9/75.4/66.8/59.5 (BP=1.000, ratio=1.043, hyp_len=24150, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1090.0.28-1.33.0.57-1.77.pth
BLEU = 71.56, 86.0/75.7/67.2/60.0 (BP=1.000, ratio=1.040, hyp_len=24090, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1091.0.32-1.37.0.57-1.77.pth
BLEU = 72.54, 86.8/76.5/68.2/61.1 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1092.0.30-1.35.0.57-1.77.pth
BLEU = 71.81, 86.2/75.9/67.5/60.3 (BP=1.000, ratio=1.039, hyp_len=24069, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1093.0.29-1.33.0.58-1.78.pth
BLEU = 71.88, 86.4/76.0/67.4/60.3 (BP=1.000, ratio=1.037, hyp_len=24006, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1094.0.28-1.32.0.57-1.77.pth
BLEU = 71.97, 86.3/75.9/67.6/60.6 (BP=1.000, ratio=1.035, hyp_len=23970, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1095.0.28-1.33.0.59-1.80.pth
BLEU = 70.55, 85.5/74.9/66.1/58.5 (BP=1.000, ratio=1.046, hyp_len=24234, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1096.0.30-1.35.0.56-1.76.pth
BLEU = 71.89, 86.2/76.0/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1097.0.30-1.35.0.57-1.77.pth
BLEU = 71.75, 86.2/75.9/67.4/60.2 (BP=1.000, ratio=1.037, hyp_len=24026, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1098.0.27-1.31.0.56-1.76.pth
BLEU = 72.28, 86.5/76.2/67.9/60.9 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1099.0.29-1.34.0.60-1.83.pth
BLEU = 72.34, 86.6/76.4/68.0/60.9 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.1100.0.31-1.37.0.59-1.81.pth
BLEU = 71.72, 86.3/75.9/67.3/60.0 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.956.0.33-1.39.0.57-1.77.pth
BLEU = 72.02, 86.4/76.1/67.6/60.5 (BP=1.000, ratio=1.034, hyp_len=23958, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.957.0.30-1.35.0.58-1.79.pth
BLEU = 72.01, 86.5/76.1/67.6/60.5 (BP=1.000, ratio=1.035, hyp_len=23974, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.958.0.31-1.37.0.58-1.78.pth
BLEU = 72.32, 86.3/76.2/68.0/61.1 (BP=1.000, ratio=1.036, hyp_len=23993, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.959.0.31-1.36.0.57-1.77.pth
BLEU = 72.78, 86.7/76.7/68.5/61.6 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.960.0.30-1.35.0.57-1.76.pth
BLEU = 71.47, 85.9/75.6/67.1/59.9 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.961.0.32-1.38.0.57-1.77.pth
BLEU = 71.31, 86.1/75.6/66.9/59.4 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.962.0.34-1.40.0.57-1.77.pth
BLEU = 70.54, 85.6/74.9/66.1/58.5 (BP=1.000, ratio=1.045, hyp_len=24194, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.963.0.31-1.36.0.56-1.75.pth
BLEU = 71.18, 85.9/75.3/66.7/59.5 (BP=1.000, ratio=1.040, hyp_len=24088, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.964.0.31-1.36.0.58-1.79.pth
BLEU = 72.85, 86.9/76.7/68.5/61.7 (BP=1.000, ratio=1.028, hyp_len=23811, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.965.0.32-1.38.0.56-1.75.pth
BLEU = 71.84, 86.2/75.8/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24027, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.966.0.31-1.36.0.56-1.76.pth
BLEU = 71.00, 85.8/75.2/66.5/59.2 (BP=1.000, ratio=1.042, hyp_len=24128, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.967.0.34-1.40.0.59-1.80.pth
BLEU = 70.12, 85.3/74.6/65.6/57.9 (BP=1.000, ratio=1.047, hyp_len=24240, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.968.0.30-1.35.0.57-1.77.pth
BLEU = 71.68, 86.1/75.7/67.3/60.2 (BP=1.000, ratio=1.038, hyp_len=24051, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.969.0.31-1.37.0.57-1.77.pth
BLEU = 71.92, 86.3/75.9/67.5/60.5 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.970.0.32-1.38.0.58-1.79.pth
BLEU = 71.94, 86.3/75.9/67.6/60.5 (BP=1.000, ratio=1.037, hyp_len=24027, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.971.0.30-1.35.0.58-1.78.pth
BLEU = 71.99, 86.4/76.1/67.6/60.5 (BP=1.000, ratio=1.036, hyp_len=23999, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.972.0.35-1.41.0.57-1.77.pth
BLEU = 72.93, 86.8/76.8/68.6/61.8 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.973.0.30-1.35.0.57-1.77.pth
BLEU = 71.42, 86.0/75.5/67.0/59.8 (BP=1.000, ratio=1.038, hyp_len=24045, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.974.0.31-1.36.0.57-1.76.pth
BLEU = 72.02, 86.4/76.1/67.6/60.5 (BP=1.000, ratio=1.036, hyp_len=23999, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.975.0.31-1.36.0.58-1.79.pth
BLEU = 71.88, 86.2/75.9/67.5/60.4 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.976.0.36-1.43.0.62-1.86.pth
BLEU = 70.27, 85.5/74.8/65.7/58.0 (BP=1.000, ratio=1.045, hyp_len=24205, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.977.0.29-1.34.0.57-1.77.pth
BLEU = 71.86, 86.2/75.9/67.5/60.4 (BP=1.000, ratio=1.039, hyp_len=24072, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.978.0.29-1.34.0.58-1.79.pth
BLEU = 70.98, 85.8/75.2/66.5/59.2 (BP=1.000, ratio=1.042, hyp_len=24128, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.979.0.31-1.37.0.58-1.79.pth
BLEU = 71.04, 85.5/75.1/66.7/59.5 (BP=1.000, ratio=1.045, hyp_len=24213, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.980.0.33-1.39.0.58-1.79.pth
BLEU = 71.19, 86.0/75.4/66.7/59.3 (BP=1.000, ratio=1.040, hyp_len=24088, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.981.0.32-1.38.0.60-1.82.pth
BLEU = 73.13, 87.0/76.9/68.9/62.1 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.982.0.32-1.38.0.59-1.81.pth
BLEU = 71.69, 86.0/75.7/67.3/60.3 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.983.0.32-1.38.0.57-1.77.pth
BLEU = 70.98, 85.8/75.2/66.5/59.1 (BP=1.000, ratio=1.043, hyp_len=24161, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.984.0.30-1.35.0.57-1.76.pth
BLEU = 71.17, 85.9/75.4/66.7/59.4 (BP=1.000, ratio=1.041, hyp_len=24117, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.985.0.30-1.35.0.57-1.77.pth
BLEU = 71.71, 86.2/75.7/67.3/60.2 (BP=1.000, ratio=1.037, hyp_len=24027, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.986.0.30-1.35.0.58-1.79.pth
BLEU = 71.46, 86.1/75.6/67.0/59.8 (BP=1.000, ratio=1.042, hyp_len=24129, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.987.0.31-1.37.0.59-1.80.pth
BLEU = 69.55, 85.0/74.1/65.0/57.1 (BP=1.000, ratio=1.051, hyp_len=24336, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.988.0.32-1.38.0.57-1.77.pth
BLEU = 71.90, 86.2/75.9/67.5/60.5 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.989.0.31-1.36.0.57-1.77.pth
BLEU = 71.60, 86.1/75.6/67.2/60.1 (BP=1.000, ratio=1.036, hyp_len=24004, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.990.0.32-1.38.0.58-1.78.pth
BLEU = 71.83, 86.3/75.8/67.4/60.3 (BP=1.000, ratio=1.036, hyp_len=23984, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.991.0.32-1.37.0.57-1.78.pth
BLEU = 71.05, 85.7/75.2/66.6/59.4 (BP=1.000, ratio=1.043, hyp_len=24155, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.29-1.34.0.57-1.77.pth
BLEU = 72.08, 86.4/76.1/67.7/60.6 (BP=1.000, ratio=1.035, hyp_len=23960, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.31-1.36.0.57-1.77.pth
BLEU = 72.86, 87.0/76.7/68.5/61.7 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.29-1.34.0.58-1.78.pth
BLEU = 71.39, 86.0/75.5/66.9/59.8 (BP=1.000, ratio=1.041, hyp_len=24117, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.32-1.38.0.57-1.78.pth
BLEU = 72.02, 86.5/76.1/67.6/60.5 (BP=1.000, ratio=1.035, hyp_len=23967, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.32-1.37.0.58-1.79.pth
BLEU = 70.94, 85.7/75.2/66.5/59.1 (BP=1.000, ratio=1.044, hyp_len=24187, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.32-1.37.0.56-1.75.pth
BLEU = 71.92, 86.5/76.0/67.5/60.3 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.31-1.37.0.56-1.75.pth
BLEU = 71.70, 86.1/75.6/67.3/60.3 (BP=1.000, ratio=1.039, hyp_len=24069, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.31-1.37.0.57-1.76.pth
BLEU = 71.57, 86.0/75.6/67.2/60.0 (BP=1.000, ratio=1.039, hyp_len=24065, ref_len=23160)

real	77m33.815s
user	76m7.525s
sys	3m4.740s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$
```

baseline က BLEU = 73.04 (Transformer model)... ဆိုတော့ အဲဒါကို ကျော်မှ ဖြစ်လိမ့်မယ်...  
ဒီ တစ်ခါတော့ baseline ကို ကျော်သွားပြီ... :)  

```
Evaluation result for the model: transformer-rl-model-myrk.1004.0.31-1.37.0.57-1.77.pth
BLEU = 73.01, 86.9/76.8/68.7/62.0 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
...
...
Evaluation result for the model: transformer-rl-model-myrk.981.0.32-1.38.0.60-1.82.pth
BLEU = 73.13, 87.0/76.9/68.9/62.1 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
```

baseline ကို ပထမဆုံး RL မော်ဒယ်က ကျော်သွားပေမဲ့ significant မဖြစ်သေးလို့ ဒီတစ်ခါတော့ ဒီတစ်ခါတော့ --max_grad_norm 1e+12 --n_epochs 1100 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 32  --max_grad_norm 1e+12 --n_epochs 1100
...
...
Validation - loss=5.6779e-01 ppl=1.76 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1086 - |param|=3.98e+02 |g_param|=8.51e+04 loss=2.9862e-01 ppl=1.35                                               
Validation - loss=5.7353e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1087 - |param|=3.98e+02 |g_param|=7.51e+04 loss=3.0574e-01 ppl=1.36                                               
Validation - loss=5.7313e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1088 - |param|=3.98e+02 |g_param|=6.44e+04 loss=2.9199e-01 ppl=1.34                                               
Validation - loss=5.6507e-01 ppl=1.76 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1089 - |param|=3.98e+02 |g_param|=7.03e+04 loss=3.2341e-01 ppl=1.38                                               
Validation - loss=5.6047e-01 ppl=1.75 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1090 - |param|=3.98e+02 |g_param|=4.66e+04 loss=2.9252e-01 ppl=1.34                                               
Validation - loss=5.6226e-01 ppl=1.75 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1091 - |param|=3.98e+02 |g_param|=5.49e+04 loss=2.8665e-01 ppl=1.33                                               
Validation - loss=5.6964e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1092 - |param|=3.98e+02 |g_param|=8.66e+04 loss=3.1080e-01 ppl=1.36                                               
Validation - loss=5.7659e-01 ppl=1.78 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1093 - |param|=3.98e+02 |g_param|=6.67e+04 loss=2.8891e-01 ppl=1.33                                               
Validation - loss=5.6215e-01 ppl=1.75 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1094 - |param|=3.98e+02 |g_param|=5.85e+04 loss=2.8933e-01 ppl=1.34                                               
Validation - loss=5.5602e-01 ppl=1.74 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1095 - |param|=3.98e+02 |g_param|=6.57e+04 loss=2.9367e-01 ppl=1.34                                               
Validation - loss=5.6567e-01 ppl=1.76 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1096 - |param|=3.98e+02 |g_param|=7.03e+04 loss=3.0648e-01 ppl=1.36                                               
Validation - loss=5.7516e-01 ppl=1.78 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1097 - |param|=3.98e+02 |g_param|=7.13e+04 loss=3.0740e-01 ppl=1.36                                               
Validation - loss=5.6942e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1098 - |param|=3.98e+02 |g_param|=7.20e+04 loss=2.8194e-01 ppl=1.33                                               
Validation - loss=5.6321e-01 ppl=1.76 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1099 - |param|=3.99e+02 |g_param|=1.24e+05 loss=3.1593e-01 ppl=1.37                                               
Validation - loss=5.7170e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                
Epoch 1100 - |param|=3.99e+02 |g_param|=1.09e+05 loss=3.1163e-01 ppl=1.37                                               
Validation - loss=5.7017e-01 ppl=1.77 best_loss=5.5596e-01 best_ppl=1.74                                                

real	86m51.232s
user	86m35.925s
sys	0m10.428s
```

testing/evaluation လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh
...
...
...
Evaluation result for the model: transformer-rl-model-myrk.984.0.31-1.37.0.58-1.78.pth
BLEU = 70.82, 85.7/75.1/66.4/58.9 (BP=1.000, ratio=1.041, hyp_len=24120, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.985.0.31-1.36.0.56-1.76.pth
BLEU = 72.30, 86.5/76.2/68.0/61.0 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.986.0.32-1.38.0.56-1.76.pth
BLEU = 72.24, 86.5/76.2/67.9/60.9 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.987.0.33-1.39.0.58-1.79.pth
BLEU = 71.76, 86.1/75.8/67.4/60.2 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.988.0.30-1.35.0.58-1.79.pth
BLEU = 72.57, 86.9/76.5/68.2/61.2 (BP=1.000, ratio=1.031, hyp_len=23882, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.989.0.34-1.41.0.58-1.78.pth
BLEU = 71.44, 86.1/75.6/67.0/59.7 (BP=1.000, ratio=1.043, hyp_len=24150, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.990.0.32-1.37.0.56-1.76.pth
BLEU = 71.77, 86.1/75.8/67.4/60.3 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.991.0.32-1.38.0.57-1.76.pth
BLEU = 71.86, 86.4/75.9/67.4/60.3 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.34-1.40.0.58-1.79.pth
BLEU = 72.02, 86.4/76.0/67.6/60.6 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.31-1.37.0.57-1.77.pth
BLEU = 71.39, 85.9/75.5/67.0/59.8 (BP=1.000, ratio=1.040, hyp_len=24075, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.30-1.36.0.57-1.76.pth
BLEU = 70.57, 85.6/74.9/66.1/58.6 (BP=1.000, ratio=1.045, hyp_len=24211, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.34-1.41.0.58-1.79.pth
BLEU = 70.06, 85.3/74.5/65.5/57.8 (BP=1.000, ratio=1.049, hyp_len=24293, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.28-1.32.0.57-1.76.pth
BLEU = 71.35, 86.0/75.5/66.9/59.7 (BP=1.000, ratio=1.040, hyp_len=24096, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.29-1.34.0.59-1.81.pth
BLEU = 69.90, 85.4/74.6/65.3/57.4 (BP=1.000, ratio=1.049, hyp_len=24302, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.30-1.35.0.60-1.82.pth
BLEU = 70.73, 85.6/75.1/66.3/58.8 (BP=1.000, ratio=1.041, hyp_len=24120, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.31-1.36.0.57-1.78.pth
BLEU = 71.51, 86.2/75.7/67.1/59.8 (BP=1.000, ratio=1.040, hyp_len=24085, ref_len=23160)

real	79m41.013s
user	78m6.944s
sys	3m8.264s
```

highest score တွေက 72.xx က ၄၅ ခုထိတက်ပေမဲ့ baseline ကို မကျော်နိုင်ဘူး...  
အများဆုံး ရတာက 72.85 ပါ။  

```
Evaluation result for the model: transformer-rl-model-myrk.1048.0.31-1.37.0.56-1.76.pth
BLEU = 72.85, 86.8/76.7/68.5/61.7 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
```

အကောင်းဆုံး မော်ဒယ်ကို backup ကူးခဲ့...  

```
(base) ye@:~/exp/simple-nmt/model/rl/transformer$ mkdir bk-max_grad_norm-1e12-1100epoch/
(base) ye@:~/exp/simple-nmt/model/rl/transformer$ mv transformer-rl-model-myrk.1048.0.31-1.37.0.56-1.76.pth.* ./bk-max_grad_norm-1e12-1100epoch/
```

ဒီတစ်ခါတော့ max_grad_norm 1e+10 --n_epochs 1106 ထားပြီး ထပ် RL fine-tuning လုပ်ကြည့်ခဲ့...  

```
Validation - loss=5.7122e-01 ppl=1.77 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1092 - |param|=3.98e+02 |g_param|=4.08e+04 loss=2.9246e-01 ppl=1.34                                               
Validation - loss=5.8744e-01 ppl=1.80 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1093 - |param|=3.98e+02 |g_param|=3.48e+04 loss=3.2353e-01 ppl=1.38                                               
Validation - loss=5.9728e-01 ppl=1.82 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1094 - |param|=3.98e+02 |g_param|=3.96e+04 loss=2.9609e-01 ppl=1.34                                               
Validation - loss=6.0942e-01 ppl=1.84 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1095 - |param|=3.98e+02 |g_param|=6.22e+04 loss=3.0770e-01 ppl=1.36                                               
Validation - loss=6.2016e-01 ppl=1.86 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1096 - |param|=3.98e+02 |g_param|=2.74e+04 loss=3.0940e-01 ppl=1.36                                               
Validation - loss=5.7867e-01 ppl=1.78 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1097 - |param|=3.98e+02 |g_param|=3.73e+04 loss=3.2875e-01 ppl=1.39                                               
Validation - loss=5.6743e-01 ppl=1.76 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1098 - |param|=3.98e+02 |g_param|=3.62e+04 loss=2.9882e-01 ppl=1.35                                               
Validation - loss=5.9447e-01 ppl=1.81 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1099 - |param|=3.98e+02 |g_param|=2.57e+04 loss=3.0633e-01 ppl=1.36                                               
Validation - loss=5.7953e-01 ppl=1.79 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1100 - |param|=3.98e+02 |g_param|=6.44e+04 loss=3.0906e-01 ppl=1.36                                               
Validation - loss=5.7243e-01 ppl=1.77 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1101 - |param|=3.99e+02 |g_param|=5.58e+04 loss=3.1273e-01 ppl=1.37                                               
Validation - loss=5.7011e-01 ppl=1.77 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1102 - |param|=3.99e+02 |g_param|=2.60e+04 loss=2.8758e-01 ppl=1.33                                               
Validation - loss=5.8796e-01 ppl=1.80 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1103 - |param|=3.99e+02 |g_param|=2.84e+04 loss=2.7435e-01 ppl=1.32                                               
Validation - loss=5.7241e-01 ppl=1.77 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1104 - |param|=3.99e+02 |g_param|=2.52e+04 loss=2.9018e-01 ppl=1.34                                               
Validation - loss=5.8136e-01 ppl=1.79 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1105 - |param|=3.99e+02 |g_param|=2.30e+04 loss=2.9526e-01 ppl=1.34                                               
Validation - loss=5.6066e-01 ppl=1.75 best_loss=5.5677e-01 best_ppl=1.75                                                
Epoch 1106 - |param|=3.99e+02 |g_param|=3.49e+04 loss=2.9223e-01 ppl=1.34                                               
Validation - loss=5.6771e-01 ppl=1.76 best_loss=5.5677e-01 best_ppl=1.75                                                

real	91m56.734s
user	91m39.869s
sys	0m12.832s
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/myrk-transformer-model.956.0.30-1.35.0.57-1.77.pth --model_fn ./model/rl/transformer/transformer-rl-model-myrk.pth --init_epoch 956 --iteration_per_update 32  --max_grad_norm 1e+10 --n_epochs 1106

```

max_grad_norm 1e+10 --n_epochs 1106 မော်ဒယ်ကို သုံးပြီးတော့ testing/evaluation လုပ်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer$ time ./test-eval-loop.sh
...
...
Evaluation result for the model: transformer-rl-model-myrk.991.0.32-1.37.0.57-1.76.pth
BLEU = 71.84, 86.3/75.8/67.4/60.4 (BP=1.000, ratio=1.036, hyp_len=23996, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.992.0.33-1.38.0.56-1.76.pth
BLEU = 72.42, 86.6/76.4/68.1/61.1 (BP=1.000, ratio=1.034, hyp_len=23951, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.993.0.32-1.38.0.56-1.76.pth
BLEU = 71.68, 86.1/75.7/67.3/60.1 (BP=1.000, ratio=1.041, hyp_len=24116, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.994.0.33-1.39.0.58-1.79.pth
BLEU = 72.76, 86.7/76.6/68.5/61.6 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.995.0.32-1.37.0.58-1.78.pth
BLEU = 71.50, 85.9/75.5/67.1/60.0 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.996.0.30-1.34.0.57-1.77.pth
BLEU = 72.38, 86.6/76.3/68.0/61.1 (BP=1.000, ratio=1.033, hyp_len=23932, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.997.0.30-1.35.0.56-1.75.pth
BLEU = 72.66, 86.8/76.5/68.3/61.4 (BP=1.000, ratio=1.032, hyp_len=23890, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.998.0.31-1.37.0.56-1.75.pth
BLEU = 72.20, 86.3/76.2/67.8/60.9 (BP=1.000, ratio=1.037, hyp_len=24017, ref_len=23160)
Evaluation result for the model: transformer-rl-model-myrk.999.0.30-1.35.0.57-1.76.pth
BLEU = 71.77, 86.1/75.7/67.4/60.4 (BP=1.000, ratio=1.037, hyp_len=24009, ref_len=23160)

real	81m16.647s
user	79m43.052s
sys	3m14.104s
```

The best score က ...  

```
Evaluation result for the model: transformer-rl-model-myrk.1062.0.32-1.38.0.57-1.76.pth
BLEU = 73.14, 87.0/77.0/68.9/62.1 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
```


## Thinking

နောက်တစ်မျိုး RL fine-tuning က တကယ် အလုပ်လုပ် မလုပ်ကို စမ်းလို့ ရနိုင်တာက development data, test data ရဲ့ ပမာဏကို လက်ရှိထက် ကြီးပေးတာမျိုး လုပ်လို့ ရတယ်...  
လက်ရှိ သုံးနေတဲ့ ဒေတာ ပမာဏက အောက်ပါအတိုင်း...  

```
(base) ye@:~/exp/simple-nmt/model/rl/transformer$ wc /media/ye/project2/exp/myrk-transformer/data/syl/*.my
   1000   12822  120331 /media/ye/project2/exp/myrk-transformer/data/syl/dev.my
   1811   23509  219399 /media/ye/project2/exp/myrk-transformer/data/syl/test.my
  15561  198624 1851216 /media/ye/project2/exp/myrk-transformer/data/syl/train.my
  18372  234955 2190946 total
(base) ye@:~/exp/simple-nmt/model/rl/transformer$ wc /media/ye/project2/exp/myrk-transformer/data/syl/*.rk
   1000   12629  118395 /media/ye/project2/exp/myrk-transformer/data/syl/dev.rk
   1811   23160  215711 /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
  15561  195887 1824944 /media/ye/project2/exp/myrk-transformer/data/syl/train.rk
  18372  231676 2159050 total
```

development ဒေတာကို သုံးပြီးမှ RL fine-tuning လုပ်တာမို့လို့ ...   
မြန်မာ-ရခိုင် မော်ဒယ်က ပြောရရင် baseline မော်ဒယ်ကိုက dialect translation မို့လို့ ရလဒ်က ကောင်းနေပြီးသား ဆိုတော့ RL fine-tuning က dev data နည်းနည်းနဲ့ ထပ်တိုးလုပ်ဖို့ ခက်နေတဲ့ အပိုင်းလည်း ပါတယ်။  
နောက်ထပ် အရေးကြီးတာက ငါက baseline မော်ဒယ်ကို epoch 1000 နဲ့ လုပ်ချလိုက်တော့ baseline model တွေကလည်း strong ဖြစ်ပြီးသားမို့လို့ ... RL မှာက ရလဒ် မတက်တာ...  

## Reduce Epoch of Baseline Models and RL Fine-Tuning

### Seq2Seq

epoch 100 ထားပြီး run ကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /media/ye/project2/exp/myrk-transformer/data/syl/train --valid /media/ye/project2/exp/myrk-transformer/data/syl/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 100 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/100epoch/seq-model-myrk2.pth
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
    'model_fn': './model/seq2seq/100epoch/seq-model-myrk2.pth',
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
Epoch 1 - |param|=6.51e+02 |g_param|=1.93e+05 loss=4.2883e+00 ppl=72.85                                                 
Validation - loss=3.6133e+00 ppl=37.09 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.51e+02 |g_param|=1.71e+05 loss=4.0107e+00 ppl=55.19                                                 
Validation - loss=3.4006e+00 ppl=29.98 best_loss=3.6133e+00 best_ppl=37.09                                              
Epoch 3 - |param|=6.51e+02 |g_param|=1.62e+05 loss=3.9028e+00 ppl=49.54                                                 
Validation - loss=3.2479e+00 ppl=25.74 best_loss=3.4006e+00 best_ppl=29.98                                              
Epoch 4 - |param|=6.52e+02 |g_param|=1.85e+05 loss=3.7602e+00 ppl=42.96                                                 
Validation - loss=3.0737e+00 ppl=21.62 best_loss=3.2479e+00 best_ppl=25.74                                              
Epoch 5 - |param|=6.52e+02 |g_param|=1.75e+05 loss=3.5927e+00 ppl=36.33                                                 
Validation - loss=2.9148e+00 ppl=18.44 best_loss=3.0737e+00 best_ppl=21.62                                              
Epoch 6 - |param|=6.53e+02 |g_param|=2.05e+05 loss=3.3838e+00 ppl=29.48                                                 
Validation - loss=2.7204e+00 ppl=15.19 best_loss=2.9148e+00 best_ppl=18.44                                              
Epoch 7 - |param|=6.54e+02 |g_param|=1.76e+05 loss=3.2038e+00 ppl=24.63                                                 
Validation - loss=2.4533e+00 ppl=11.63 best_loss=2.7204e+00 best_ppl=15.19                                              
Epoch 8 - |param|=6.55e+02 |g_param|=1.56e+05 loss=2.8959e+00 ppl=18.10                                                 
Validation - loss=2.1545e+00 ppl=8.62 best_loss=2.4533e+00 best_ppl=11.63                                               
Epoch 9 - |param|=6.55e+02 |g_param|=8.43e+04 loss=2.5888e+00 ppl=13.31                                                 
Validation - loss=1.9368e+00 ppl=6.94 best_loss=2.1545e+00 best_ppl=8.62                                                
Epoch 10 - |param|=6.56e+02 |g_param|=9.75e+04 loss=2.3771e+00 ppl=10.77                                                
Validation - loss=1.7919e+00 ppl=6.00 best_loss=1.9368e+00 best_ppl=6.94                                                
Epoch 11 - |param|=6.57e+02 |g_param|=1.01e+05 loss=2.2111e+00 ppl=9.13                                                 
Validation - loss=1.6101e+00 ppl=5.00 best_loss=1.7919e+00 best_ppl=6.00                                                
Epoch 12 - |param|=6.58e+02 |g_param|=1.11e+05 loss=2.0396e+00 ppl=7.69                                                 
Validation - loss=1.5761e+00 ppl=4.84 best_loss=1.6101e+00 best_ppl=5.00                                                
Epoch 13 - |param|=6.58e+02 |g_param|=1.25e+05 loss=1.8752e+00 ppl=6.52                                                 
Validation - loss=1.4459e+00 ppl=4.25 best_loss=1.5761e+00 best_ppl=4.84                                                
Epoch 14 - |param|=6.59e+02 |g_param|=9.66e+04 loss=1.7209e+00 ppl=5.59                                                 
Validation - loss=1.2683e+00 ppl=3.55 best_loss=1.4459e+00 best_ppl=4.25                                                
Epoch 15 - |param|=6.60e+02 |g_param|=1.17e+05 loss=1.5519e+00 ppl=4.72                                                 
Validation - loss=1.1859e+00 ppl=3.27 best_loss=1.2683e+00 best_ppl=3.55                                                
Epoch 16 - |param|=6.60e+02 |g_param|=1.16e+05 loss=1.4668e+00 ppl=4.34                                                 
Validation - loss=1.0892e+00 ppl=2.97 best_loss=1.1859e+00 best_ppl=3.27                                                
Epoch 17 - |param|=6.61e+02 |g_param|=1.03e+05 loss=1.3386e+00 ppl=3.81                                                 
Validation - loss=1.0047e+00 ppl=2.73 best_loss=1.0892e+00 best_ppl=2.97                                                
Epoch 18 - |param|=6.61e+02 |g_param|=8.99e+04 loss=1.5135e+00 ppl=4.54                                                 
Validation - loss=1.0991e+00 ppl=3.00 best_loss=1.0047e+00 best_ppl=2.73                                                
Epoch 19 - |param|=6.62e+02 |g_param|=3.90e+04 loss=1.1910e+00 ppl=3.29                                                 
Validation - loss=8.5998e-01 ppl=2.36 best_loss=1.0047e+00 best_ppl=2.73                                                
Epoch 20 - |param|=6.63e+02 |g_param|=5.55e+04 loss=1.1311e+00 ppl=3.10                                                 
Validation - loss=8.4805e-01 ppl=2.34 best_loss=8.5998e-01 best_ppl=2.36                                                
Epoch 21 - |param|=6.63e+02 |g_param|=4.47e+04 loss=1.0445e+00 ppl=2.84                                                 
Validation - loss=8.1017e-01 ppl=2.25 best_loss=8.4805e-01 best_ppl=2.34                                                
Epoch 22 - |param|=6.63e+02 |g_param|=4.21e+04 loss=9.8562e-01 ppl=2.68                                                 
Validation - loss=7.4788e-01 ppl=2.11 best_loss=8.1017e-01 best_ppl=2.25                                                
Epoch 23 - |param|=6.64e+02 |g_param|=6.18e+04 loss=9.5746e-01 ppl=2.61                                                 
Validation - loss=7.0029e-01 ppl=2.01 best_loss=7.4788e-01 best_ppl=2.11                                                
Epoch 24 - |param|=6.65e+02 |g_param|=4.10e+04 loss=8.8312e-01 ppl=2.42                                                 
Validation - loss=6.7933e-01 ppl=1.97 best_loss=7.0029e-01 best_ppl=2.01                                                
Epoch 25 - |param|=6.65e+02 |g_param|=3.82e+04 loss=8.2577e-01 ppl=2.28                                                 
Validation - loss=6.4235e-01 ppl=1.90 best_loss=6.7933e-01 best_ppl=1.97                                                
Epoch 26 - |param|=6.65e+02 |g_param|=3.82e+04 loss=7.7273e-01 ppl=2.17                                                 
Validation - loss=6.4135e-01 ppl=1.90 best_loss=6.4235e-01 best_ppl=1.90                                                
Epoch 27 - |param|=6.66e+02 |g_param|=4.28e+04 loss=7.5613e-01 ppl=2.13                                                 
Validation - loss=6.1947e-01 ppl=1.86 best_loss=6.4135e-01 best_ppl=1.90                                                
Epoch 28 - |param|=6.66e+02 |g_param|=3.79e+04 loss=7.1737e-01 ppl=2.05                                                 
Validation - loss=6.3823e-01 ppl=1.89 best_loss=6.1947e-01 best_ppl=1.86                                                
Epoch 29 - |param|=6.67e+02 |g_param|=5.78e+04 loss=7.3170e-01 ppl=2.08                                                 
Validation - loss=5.6623e-01 ppl=1.76 best_loss=6.1947e-01 best_ppl=1.86                                                
Epoch 30 - |param|=6.67e+02 |g_param|=5.82e+04 loss=7.2222e-01 ppl=2.06                                                 
Validation - loss=5.7493e-01 ppl=1.78 best_loss=5.6623e-01 best_ppl=1.76                                                
Epoch 31 - |param|=6.68e+02 |g_param|=3.10e+04 loss=6.4521e-01 ppl=1.91                                                 
Validation - loss=5.2398e-01 ppl=1.69 best_loss=5.6623e-01 best_ppl=1.76                                                
Epoch 32 - |param|=6.68e+02 |g_param|=3.73e+04 loss=6.0376e-01 ppl=1.83                                                 
Validation - loss=5.2334e-01 ppl=1.69 best_loss=5.2398e-01 best_ppl=1.69                                                
Epoch 33 - |param|=6.69e+02 |g_param|=3.03e+04 loss=5.9386e-01 ppl=1.81                                                 
Validation - loss=5.0725e-01 ppl=1.66 best_loss=5.2334e-01 best_ppl=1.69                                                
Epoch 34 - |param|=6.69e+02 |g_param|=3.68e+04 loss=5.4881e-01 ppl=1.73                                                 
Validation - loss=4.9682e-01 ppl=1.64 best_loss=5.0725e-01 best_ppl=1.66                                                
Epoch 35 - |param|=6.69e+02 |g_param|=5.70e+04 loss=5.5283e-01 ppl=1.74                                                 
Validation - loss=4.8131e-01 ppl=1.62 best_loss=4.9682e-01 best_ppl=1.64                                                
Epoch 36 - |param|=6.70e+02 |g_param|=5.60e+04 loss=5.3007e-01 ppl=1.70                                                 
Validation - loss=4.8445e-01 ppl=1.62 best_loss=4.8131e-01 best_ppl=1.62                                                
Epoch 37 - |param|=6.70e+02 |g_param|=6.88e+04 loss=5.3235e-01 ppl=1.70                                                 
Validation - loss=4.7779e-01 ppl=1.61 best_loss=4.8131e-01 best_ppl=1.62                                                
Epoch 38 - |param|=6.71e+02 |g_param|=6.65e+04 loss=5.0653e-01 ppl=1.66                                                 
Validation - loss=4.7339e-01 ppl=1.61 best_loss=4.7779e-01 best_ppl=1.61                                                
Epoch 39 - |param|=6.71e+02 |g_param|=5.75e+04 loss=4.9246e-01 ppl=1.64                                                 
Validation - loss=4.5714e-01 ppl=1.58 best_loss=4.7339e-01 best_ppl=1.61                                                
Epoch 40 - |param|=6.71e+02 |g_param|=7.67e+04 loss=4.9639e-01 ppl=1.64                                                 
Validation - loss=4.6287e-01 ppl=1.59 best_loss=4.5714e-01 best_ppl=1.58                                                
Epoch 41 - |param|=6.72e+02 |g_param|=7.31e+04 loss=4.6976e-01 ppl=1.60                                                 
Validation - loss=4.4148e-01 ppl=1.56 best_loss=4.5714e-01 best_ppl=1.58                                                
Epoch 42 - |param|=6.72e+02 |g_param|=6.00e+04 loss=4.5135e-01 ppl=1.57                                                 
Validation - loss=4.2340e-01 ppl=1.53 best_loss=4.4148e-01 best_ppl=1.56                                                
Epoch 43 - |param|=6.73e+02 |g_param|=6.83e+04 loss=4.5650e-01 ppl=1.58                                                 
Validation - loss=4.2797e-01 ppl=1.53 best_loss=4.2340e-01 best_ppl=1.53                                                
Epoch 44 - |param|=6.73e+02 |g_param|=6.85e+04 loss=4.3076e-01 ppl=1.54                                                 
Validation - loss=4.2009e-01 ppl=1.52 best_loss=4.2340e-01 best_ppl=1.53                                                
Epoch 45 - |param|=6.73e+02 |g_param|=7.02e+04 loss=4.5483e-01 ppl=1.58                                                 
Validation - loss=4.3897e-01 ppl=1.55 best_loss=4.2009e-01 best_ppl=1.52                                                
Epoch 46 - |param|=6.74e+02 |g_param|=6.06e+04 loss=4.1373e-01 ppl=1.51                                                 
Validation - loss=4.0048e-01 ppl=1.49 best_loss=4.2009e-01 best_ppl=1.52                                                
Epoch 47 - |param|=6.74e+02 |g_param|=5.79e+04 loss=4.0875e-01 ppl=1.50                                                 
Validation - loss=4.2250e-01 ppl=1.53 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 48 - |param|=6.75e+02 |g_param|=6.17e+04 loss=4.2601e-01 ppl=1.53                                                 
Validation - loss=4.1746e-01 ppl=1.52 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 49 - |param|=6.75e+02 |g_param|=5.18e+04 loss=4.0194e-01 ppl=1.49                                                 
Validation - loss=4.0072e-01 ppl=1.49 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 50 - |param|=6.75e+02 |g_param|=4.94e+04 loss=3.8194e-01 ppl=1.47                                                 
Validation - loss=4.1243e-01 ppl=1.51 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 51 - |param|=6.76e+02 |g_param|=6.69e+04 loss=3.8970e-01 ppl=1.48                                                 
Validation - loss=4.0103e-01 ppl=1.49 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 52 - |param|=6.76e+02 |g_param|=4.82e+04 loss=3.6700e-01 ppl=1.44                                                 
Validation - loss=4.0942e-01 ppl=1.51 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 53 - |param|=6.76e+02 |g_param|=7.42e+04 loss=4.2817e-01 ppl=1.53                                                 
Validation - loss=4.6602e-01 ppl=1.59 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 54 - |param|=6.77e+02 |g_param|=3.27e+04 loss=3.9045e-01 ppl=1.48                                                 
Validation - loss=4.1519e-01 ppl=1.51 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 55 - |param|=6.77e+02 |g_param|=3.12e+04 loss=3.7782e-01 ppl=1.46                                                 
Validation - loss=3.9714e-01 ppl=1.49 best_loss=4.0048e-01 best_ppl=1.49                                                
Epoch 56 - |param|=6.78e+02 |g_param|=2.58e+04 loss=3.5306e-01 ppl=1.42                                                 
Validation - loss=4.0031e-01 ppl=1.49 best_loss=3.9714e-01 best_ppl=1.49                                                
Epoch 57 - |param|=6.78e+02 |g_param|=2.57e+04 loss=3.4566e-01 ppl=1.41                                                 
Validation - loss=3.8802e-01 ppl=1.47 best_loss=3.9714e-01 best_ppl=1.49                                                
Epoch 58 - |param|=6.78e+02 |g_param|=2.31e+04 loss=3.3496e-01 ppl=1.40                                                 
Validation - loss=3.7350e-01 ppl=1.45 best_loss=3.8802e-01 best_ppl=1.47                                                
Epoch 59 - |param|=6.79e+02 |g_param|=1.98e+04 loss=3.3694e-01 ppl=1.40                                                 
Validation - loss=3.9001e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 60 - |param|=6.79e+02 |g_param|=2.51e+04 loss=3.3119e-01 ppl=1.39                                                 
Validation - loss=3.7977e-01 ppl=1.46 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 61 - |param|=6.79e+02 |g_param|=2.34e+04 loss=3.2731e-01 ppl=1.39                                                 
Validation - loss=3.9223e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 62 - |param|=6.80e+02 |g_param|=2.16e+04 loss=3.1518e-01 ppl=1.37                                                 
Validation - loss=3.9538e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 63 - |param|=6.80e+02 |g_param|=2.11e+04 loss=3.0600e-01 ppl=1.36                                                 
Validation - loss=3.8217e-01 ppl=1.47 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 64 - |param|=6.80e+02 |g_param|=2.17e+04 loss=3.1290e-01 ppl=1.37                                                 
Validation - loss=3.9289e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 65 - |param|=6.81e+02 |g_param|=2.54e+04 loss=3.1407e-01 ppl=1.37                                                 
Validation - loss=4.0602e-01 ppl=1.50 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 66 - |param|=6.81e+02 |g_param|=3.33e+04 loss=3.2770e-01 ppl=1.39                                                 
Validation - loss=4.0829e-01 ppl=1.50 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 67 - |param|=6.82e+02 |g_param|=2.86e+04 loss=3.2763e-01 ppl=1.39                                                 
Validation - loss=3.9105e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 68 - |param|=6.82e+02 |g_param|=2.36e+04 loss=3.0460e-01 ppl=1.36                                                 
Validation - loss=3.8082e-01 ppl=1.46 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 69 - |param|=6.82e+02 |g_param|=2.44e+04 loss=3.0087e-01 ppl=1.35                                                 
Validation - loss=3.8497e-01 ppl=1.47 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 70 - |param|=6.83e+02 |g_param|=3.73e+04 loss=2.8804e-01 ppl=1.33                                                 
Validation - loss=3.8196e-01 ppl=1.47 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 71 - |param|=6.83e+02 |g_param|=4.10e+04 loss=2.8236e-01 ppl=1.33                                                 
Validation - loss=3.7960e-01 ppl=1.46 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 72 - |param|=6.83e+02 |g_param|=4.25e+04 loss=2.6611e-01 ppl=1.30                                                 
Validation - loss=3.9263e-01 ppl=1.48 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 73 - |param|=6.84e+02 |g_param|=3.84e+04 loss=2.7272e-01 ppl=1.31                                                 
Validation - loss=3.8738e-01 ppl=1.47 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 74 - |param|=6.84e+02 |g_param|=4.17e+04 loss=2.8146e-01 ppl=1.33                                                 
Validation - loss=3.8187e-01 ppl=1.47 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 75 - |param|=6.84e+02 |g_param|=4.19e+04 loss=2.6144e-01 ppl=1.30                                                 
Validation - loss=4.0054e-01 ppl=1.49 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 76 - |param|=6.84e+02 |g_param|=4.31e+04 loss=2.6199e-01 ppl=1.30                                                 
Validation - loss=4.0231e-01 ppl=1.50 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 77 - |param|=6.85e+02 |g_param|=4.10e+04 loss=2.5655e-01 ppl=1.29                                                 
Validation - loss=3.7161e-01 ppl=1.45 best_loss=3.7350e-01 best_ppl=1.45                                                
Epoch 78 - |param|=6.85e+02 |g_param|=4.73e+04 loss=2.5653e-01 ppl=1.29                                                 
Validation - loss=3.7944e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 79 - |param|=6.86e+02 |g_param|=5.22e+04 loss=2.6877e-01 ppl=1.31                                                 
Validation - loss=3.8442e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 80 - |param|=6.86e+02 |g_param|=4.28e+04 loss=2.9150e-01 ppl=1.34                                                 
Validation - loss=3.7548e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 81 - |param|=6.86e+02 |g_param|=1.78e+04 loss=2.9965e-01 ppl=1.35                                                 
Validation - loss=4.0371e-01 ppl=1.50 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 82 - |param|=6.87e+02 |g_param|=1.36e+04 loss=2.6832e-01 ppl=1.31                                                 
Validation - loss=3.7356e-01 ppl=1.45 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 83 - |param|=6.87e+02 |g_param|=1.75e+04 loss=2.6876e-01 ppl=1.31                                                 
Validation - loss=3.7727e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 84 - |param|=6.87e+02 |g_param|=1.03e+04 loss=2.6093e-01 ppl=1.30                                                 
Validation - loss=3.8811e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 85 - |param|=6.88e+02 |g_param|=1.20e+04 loss=2.4974e-01 ppl=1.28                                                 
Validation - loss=3.8795e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 86 - |param|=6.88e+02 |g_param|=1.01e+04 loss=2.4247e-01 ppl=1.27                                                 
Validation - loss=3.9567e-01 ppl=1.49 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 87 - |param|=6.88e+02 |g_param|=8.64e+03 loss=2.3486e-01 ppl=1.26                                                 
Validation - loss=3.8007e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 88 - |param|=6.89e+02 |g_param|=8.81e+03 loss=2.3664e-01 ppl=1.27                                                 
Validation - loss=3.8466e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 89 - |param|=6.89e+02 |g_param|=8.21e+03 loss=2.2430e-01 ppl=1.25                                                 
Validation - loss=3.7865e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 90 - |param|=6.89e+02 |g_param|=7.84e+03 loss=2.1879e-01 ppl=1.24                                                 
Validation - loss=3.7377e-01 ppl=1.45 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 91 - |param|=6.90e+02 |g_param|=9.69e+03 loss=2.2068e-01 ppl=1.25                                                 
Validation - loss=3.8253e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 92 - |param|=6.90e+02 |g_param|=1.17e+04 loss=2.3213e-01 ppl=1.26                                                 
Validation - loss=3.8137e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 93 - |param|=6.90e+02 |g_param|=1.01e+04 loss=2.2442e-01 ppl=1.25                                                 
Validation - loss=3.9340e-01 ppl=1.48 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 94 - |param|=6.91e+02 |g_param|=9.75e+03 loss=2.2221e-01 ppl=1.25                                                 
Validation - loss=3.8862e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 95 - |param|=6.91e+02 |g_param|=9.67e+03 loss=2.1873e-01 ppl=1.24                                                 
Validation - loss=3.9119e-01 ppl=1.48 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 96 - |param|=6.91e+02 |g_param|=1.09e+04 loss=2.1535e-01 ppl=1.24                                                 
Validation - loss=3.8352e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 97 - |param|=6.92e+02 |g_param|=1.86e+04 loss=2.1338e-01 ppl=1.24                                                 
Validation - loss=3.7967e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 98 - |param|=6.92e+02 |g_param|=1.87e+04 loss=2.1576e-01 ppl=1.24                                                 
Validation - loss=3.8922e-01 ppl=1.48 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 99 - |param|=6.92e+02 |g_param|=2.56e+04 loss=2.1022e-01 ppl=1.23                                                 
Validation - loss=3.8195e-01 ppl=1.47 best_loss=3.7161e-01 best_ppl=1.45                                                
Epoch 100 - |param|=6.93e+02 |g_param|=1.77e+04 loss=2.0846e-01 ppl=1.23                                                
Validation - loss=3.7815e-01 ppl=1.46 best_loss=3.7161e-01 best_ppl=1.45                                                

real	21m8.160s
user	20m51.694s
sys	0m16.267s
(simple-nmt) ye@:~/exp/simple-nmt$
```

seq2seq model 100 epoch မော်ဒယ်ကို testing/evaluation လုပ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-myrk2.01.4.29-72.85.3.61-37.09.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.6/1.2/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=22952, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.02.4.01-55.19.3.40-29.98.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.1/1.7/0.0/0.0 (BP=1.000, ratio=1.028, hyp_len=23805, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.03.3.90-49.54.3.25-25.74.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.1/2.0/0.0/0.0 (BP=1.000, ratio=1.006, hyp_len=23305, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.04.3.76-42.96.3.07-21.62.pth
BLEU = 0.53, 23.7/3.8/0.2/0.0 (BP=1.000, ratio=1.019, hyp_len=23590, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.05.3.59-36.33.2.91-18.44.pth
BLEU = 1.19, 27.4/5.6/0.8/0.0 (BP=1.000, ratio=1.011, hyp_len=23417, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.06.3.38-29.48.2.72-15.19.pth
BLEU = 2.66, 31.2/8.0/1.4/0.1 (BP=1.000, ratio=1.002, hyp_len=23206, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.07.3.20-24.63.2.45-11.63.pth
BLEU = 5.57, 37.9/13.1/3.3/0.6 (BP=0.990, ratio=0.990, hyp_len=22931, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.08.2.90-18.10.2.15-8.62.pth
BLEU = 10.72, 42.8/18.1/6.7/2.5 (BP=1.000, ratio=1.003, hyp_len=23222, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.09.2.59-13.31.1.94-6.94.pth
BLEU = 14.55, 47.6/22.2/9.8/4.4 (BP=0.999, ratio=0.999, hyp_len=23142, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.100.0.21-1.23.0.38-1.46.pth
BLEU = 74.07, 87.3/77.9/70.0/63.3 (BP=1.000, ratio=1.036, hyp_len=23986, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.10.2.38-10.77.1.79-6.00.pth
BLEU = 16.81, 49.6/24.8/12.0/5.5 (BP=0.996, ratio=0.996, hyp_len=23074, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.11.2.21-9.13.1.61-5.00.pth
BLEU = 22.96, 55.6/31.0/17.3/9.4 (BP=1.000, ratio=1.002, hyp_len=23201, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.12.2.04-7.69.1.58-4.84.pth
BLEU = 22.93, 56.1/31.6/17.4/9.5 (BP=0.986, ratio=0.986, hyp_len=22831, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.13.1.88-6.52.1.45-4.25.pth
BLEU = 26.78, 59.9/35.8/20.8/11.6 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.14.1.72-5.59.1.27-3.55.pth
BLEU = 32.83, 63.5/41.0/26.5/16.8 (BP=1.000, ratio=1.028, hyp_len=23812, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.15.1.55-4.72.1.19-3.27.pth
BLEU = 36.29, 66.0/44.3/29.8/19.9 (BP=1.000, ratio=1.008, hyp_len=23350, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.16.1.47-4.34.1.09-2.97.pth
BLEU = 40.55, 69.1/48.5/33.9/23.8 (BP=1.000, ratio=1.009, hyp_len=23375, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.17.1.34-3.81.1.00-2.73.pth
BLEU = 44.46, 71.7/52.1/37.9/27.6 (BP=1.000, ratio=1.001, hyp_len=23188, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.18.1.51-4.54.1.10-3.00.pth
BLEU = 40.31, 69.8/48.5/33.6/23.5 (BP=0.997, ratio=0.997, hyp_len=23097, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.19.1.19-3.29.0.86-2.36.pth
BLEU = 52.54, 76.7/59.5/46.3/36.1 (BP=1.000, ratio=1.000, hyp_len=23153, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.20.1.13-3.10.0.85-2.34.pth
BLEU = 52.69, 77.0/59.6/46.4/36.4 (BP=0.999, ratio=0.999, hyp_len=23128, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.21.1.04-2.84.0.81-2.25.pth
BLEU = 55.38, 78.5/62.0/49.2/39.3 (BP=1.000, ratio=1.003, hyp_len=23221, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.22.0.99-2.68.0.75-2.11.pth
BLEU = 57.61, 79.7/64.0/51.6/41.8 (BP=1.000, ratio=1.009, hyp_len=23357, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.23.0.96-2.61.0.70-2.01.pth
BLEU = 59.44, 80.6/65.5/53.6/44.1 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.24.0.88-2.42.0.68-1.97.pth
BLEU = 61.35, 81.7/67.2/55.7/46.3 (BP=1.000, ratio=1.004, hyp_len=23261, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.25.0.83-2.28.0.64-1.90.pth
BLEU = 63.21, 82.6/68.9/57.7/48.6 (BP=1.000, ratio=1.011, hyp_len=23421, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.26.0.77-2.17.0.64-1.90.pth
BLEU = 64.02, 83.0/69.6/58.7/49.6 (BP=1.000, ratio=1.011, hyp_len=23425, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.27.0.76-2.13.0.62-1.86.pth
BLEU = 63.86, 83.0/69.5/58.4/49.3 (BP=1.000, ratio=1.009, hyp_len=23376, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.28.0.72-2.05.0.64-1.89.pth
BLEU = 61.74, 81.7/67.5/56.2/46.9 (BP=1.000, ratio=1.005, hyp_len=23276, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.29.0.73-2.08.0.57-1.76.pth
BLEU = 67.27, 84.7/72.4/62.2/53.6 (BP=1.000, ratio=1.013, hyp_len=23462, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.30.0.72-2.06.0.57-1.78.pth
BLEU = 68.22, 85.5/73.2/63.2/54.7 (BP=1.000, ratio=1.001, hyp_len=23177, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.31.0.65-1.91.0.52-1.69.pth
BLEU = 68.88, 85.4/73.8/64.1/55.8 (BP=1.000, ratio=1.017, hyp_len=23560, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.32.0.60-1.83.0.52-1.69.pth
BLEU = 68.92, 85.5/73.8/64.1/55.8 (BP=1.000, ratio=1.014, hyp_len=23479, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.33.0.59-1.81.0.51-1.66.pth
BLEU = 69.26, 85.5/74.1/64.5/56.3 (BP=1.000, ratio=1.022, hyp_len=23659, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.34.0.55-1.73.0.50-1.64.pth
BLEU = 69.05, 85.6/73.9/64.2/56.0 (BP=1.000, ratio=1.014, hyp_len=23479, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.35.0.55-1.74.0.48-1.62.pth
BLEU = 71.20, 86.4/75.6/66.7/59.0 (BP=1.000, ratio=1.017, hyp_len=23555, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.36.0.53-1.70.0.48-1.62.pth
BLEU = 71.51, 86.5/75.9/67.0/59.4 (BP=1.000, ratio=1.017, hyp_len=23545, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.37.0.53-1.70.0.48-1.61.pth
BLEU = 70.03, 85.8/74.7/65.4/57.5 (BP=1.000, ratio=1.020, hyp_len=23629, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.38.0.51-1.66.0.47-1.61.pth
BLEU = 71.98, 87.0/76.3/67.5/59.9 (BP=1.000, ratio=1.017, hyp_len=23552, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.39.0.49-1.64.0.46-1.58.pth
BLEU = 72.99, 87.2/77.1/68.7/61.4 (BP=1.000, ratio=1.018, hyp_len=23568, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.40.0.50-1.64.0.46-1.59.pth
BLEU = 71.60, 86.5/75.9/67.1/59.7 (BP=1.000, ratio=1.024, hyp_len=23712, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.41.0.47-1.60.0.44-1.56.pth
BLEU = 70.98, 85.9/75.4/66.5/58.9 (BP=1.000, ratio=1.030, hyp_len=23861, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.42.0.45-1.57.0.42-1.53.pth
BLEU = 72.18, 86.6/76.4/67.8/60.5 (BP=1.000, ratio=1.023, hyp_len=23692, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.43.0.46-1.58.0.43-1.53.pth
BLEU = 72.88, 87.1/77.1/68.6/61.2 (BP=1.000, ratio=1.021, hyp_len=23645, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.44.0.43-1.54.0.42-1.52.pth
BLEU = 73.95, 87.6/77.9/69.8/62.9 (BP=1.000, ratio=1.019, hyp_len=23609, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.45.0.45-1.58.0.44-1.55.pth
BLEU = 72.41, 86.6/76.5/68.1/60.9 (BP=1.000, ratio=1.021, hyp_len=23657, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.46.0.41-1.51.0.40-1.49.pth
BLEU = 73.51, 87.1/77.5/69.4/62.4 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.47.0.41-1.50.0.42-1.53.pth
BLEU = 73.24, 87.1/77.2/69.0/62.0 (BP=1.000, ratio=1.022, hyp_len=23660, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.48.0.43-1.53.0.42-1.52.pth
BLEU = 72.64, 86.9/76.8/68.3/61.1 (BP=1.000, ratio=1.026, hyp_len=23752, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.49.0.40-1.49.0.40-1.49.pth
BLEU = 73.65, 87.3/77.5/69.4/62.6 (BP=1.000, ratio=1.025, hyp_len=23738, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.50.0.38-1.47.0.41-1.51.pth
BLEU = 72.86, 87.0/77.0/68.6/61.4 (BP=1.000, ratio=1.025, hyp_len=23737, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.51.0.39-1.48.0.40-1.49.pth
BLEU = 73.88, 87.2/77.7/69.8/63.0 (BP=1.000, ratio=1.028, hyp_len=23808, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.52.0.37-1.44.0.41-1.51.pth
BLEU = 73.26, 87.2/77.3/69.0/61.9 (BP=1.000, ratio=1.024, hyp_len=23720, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.53.0.43-1.53.0.47-1.59.pth
BLEU = 71.17, 86.2/75.7/66.7/59.0 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.54.0.39-1.48.0.42-1.51.pth
BLEU = 73.97, 87.3/77.8/69.9/63.1 (BP=1.000, ratio=1.023, hyp_len=23683, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.55.0.38-1.46.0.40-1.49.pth
BLEU = 73.85, 87.4/77.8/69.7/62.7 (BP=1.000, ratio=1.023, hyp_len=23701, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.56.0.35-1.42.0.40-1.49.pth
BLEU = 74.58, 87.6/78.3/70.6/63.9 (BP=1.000, ratio=1.026, hyp_len=23757, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.57.0.35-1.41.0.39-1.47.pth
BLEU = 74.18, 87.4/77.9/70.1/63.4 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.58.0.33-1.40.0.37-1.45.pth
BLEU = 74.57, 87.5/78.3/70.5/64.0 (BP=1.000, ratio=1.027, hyp_len=23795, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.59.0.34-1.40.0.39-1.48.pth
BLEU = 74.93, 87.9/78.6/70.9/64.3 (BP=1.000, ratio=1.026, hyp_len=23771, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.60.0.33-1.39.0.38-1.46.pth
BLEU = 74.40, 87.5/78.1/70.4/63.7 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.61.0.33-1.39.0.39-1.48.pth
BLEU = 73.97, 87.4/77.8/69.9/63.1 (BP=1.000, ratio=1.027, hyp_len=23786, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.62.0.32-1.37.0.40-1.48.pth
BLEU = 74.78, 87.7/78.5/70.7/64.2 (BP=1.000, ratio=1.024, hyp_len=23715, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.63.0.31-1.36.0.38-1.47.pth
BLEU = 74.62, 87.7/78.3/70.6/64.0 (BP=1.000, ratio=1.028, hyp_len=23807, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.64.0.31-1.37.0.39-1.48.pth
BLEU = 73.49, 87.0/77.4/69.4/62.5 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.65.0.31-1.37.0.41-1.50.pth
BLEU = 73.53, 87.1/77.4/69.4/62.5 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.66.0.33-1.39.0.41-1.50.pth
BLEU = 72.92, 86.7/76.9/68.7/61.7 (BP=1.000, ratio=1.034, hyp_len=23956, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.67.0.33-1.39.0.39-1.48.pth
BLEU = 74.23, 87.4/77.9/70.2/63.5 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.68.0.30-1.36.0.38-1.46.pth
BLEU = 73.69, 87.2/77.5/69.5/62.8 (BP=1.000, ratio=1.027, hyp_len=23796, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.69.0.30-1.35.0.38-1.47.pth
BLEU = 74.80, 87.8/78.4/70.8/64.3 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.70.0.29-1.33.0.38-1.47.pth
BLEU = 74.48, 87.4/78.1/70.5/63.9 (BP=1.000, ratio=1.030, hyp_len=23855, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.71.0.28-1.33.0.38-1.46.pth
BLEU = 73.71, 87.0/77.4/69.6/62.9 (BP=1.000, ratio=1.031, hyp_len=23889, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.72.0.27-1.30.0.39-1.48.pth
BLEU = 73.90, 87.2/77.7/69.8/63.1 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.73.0.27-1.31.0.39-1.47.pth
BLEU = 75.28, 88.1/78.9/71.3/64.8 (BP=1.000, ratio=1.025, hyp_len=23738, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.74.0.28-1.33.0.38-1.47.pth
BLEU = 74.58, 87.5/78.3/70.6/64.0 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.75.0.26-1.30.0.40-1.49.pth
BLEU = 74.74, 87.6/78.4/70.8/64.2 (BP=1.000, ratio=1.029, hyp_len=23826, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.76.0.26-1.30.0.40-1.50.pth
BLEU = 74.60, 87.6/78.3/70.6/64.0 (BP=1.000, ratio=1.028, hyp_len=23814, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.77.0.26-1.29.0.37-1.45.pth
BLEU = 74.60, 87.3/78.2/70.7/64.2 (BP=1.000, ratio=1.033, hyp_len=23916, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.78.0.26-1.29.0.38-1.46.pth
BLEU = 74.29, 87.3/77.9/70.2/63.8 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.79.0.27-1.31.0.38-1.47.pth
BLEU = 74.88, 87.8/78.5/70.9/64.3 (BP=1.000, ratio=1.025, hyp_len=23733, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.80.0.29-1.34.0.38-1.46.pth
BLEU = 74.77, 87.7/78.5/70.8/64.2 (BP=1.000, ratio=1.028, hyp_len=23816, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.81.0.30-1.35.0.40-1.50.pth
BLEU = 73.62, 87.3/77.5/69.4/62.6 (BP=1.000, ratio=1.027, hyp_len=23784, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.82.0.27-1.31.0.37-1.45.pth
BLEU = 74.46, 87.4/78.1/70.4/63.9 (BP=1.000, ratio=1.030, hyp_len=23861, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.83.0.27-1.31.0.38-1.46.pth
BLEU = 74.51, 87.4/78.3/70.6/63.9 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.84.0.26-1.30.0.39-1.47.pth
BLEU = 75.02, 87.9/78.7/71.1/64.5 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.85.0.25-1.28.0.39-1.47.pth
BLEU = 74.20, 87.4/77.9/70.1/63.5 (BP=1.000, ratio=1.030, hyp_len=23848, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.86.0.24-1.27.0.40-1.49.pth
BLEU = 75.07, 88.0/78.7/71.1/64.5 (BP=1.000, ratio=1.024, hyp_len=23713, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.87.0.23-1.26.0.38-1.46.pth
BLEU = 74.13, 87.4/77.9/70.0/63.4 (BP=1.000, ratio=1.036, hyp_len=24000, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth
BLEU = 75.74, 88.1/79.3/71.9/65.5 (BP=1.000, ratio=1.026, hyp_len=23772, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.89.0.22-1.25.0.38-1.46.pth
BLEU = 75.33, 88.1/79.0/71.4/64.9 (BP=1.000, ratio=1.030, hyp_len=23855, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.90.0.22-1.24.0.37-1.45.pth
BLEU = 74.86, 87.7/78.5/70.9/64.4 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.91.0.22-1.25.0.38-1.47.pth
BLEU = 75.04, 87.7/78.6/71.1/64.6 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.92.0.23-1.26.0.38-1.46.pth
BLEU = 73.57, 86.9/77.5/69.5/62.6 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.93.0.22-1.25.0.39-1.48.pth
BLEU = 74.30, 87.3/78.0/70.3/63.7 (BP=1.000, ratio=1.031, hyp_len=23872, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.94.0.22-1.25.0.39-1.47.pth
BLEU = 74.88, 87.7/78.6/70.9/64.3 (BP=1.000, ratio=1.031, hyp_len=23877, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.95.0.22-1.24.0.39-1.48.pth
BLEU = 74.67, 87.6/78.3/70.7/64.1 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.96.0.22-1.24.0.38-1.47.pth
BLEU = 74.45, 87.4/78.1/70.5/63.9 (BP=1.000, ratio=1.033, hyp_len=23927, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.97.0.21-1.24.0.38-1.46.pth
BLEU = 73.93, 87.1/77.8/69.9/63.2 (BP=1.000, ratio=1.040, hyp_len=24083, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.98.0.22-1.24.0.39-1.48.pth
BLEU = 74.11, 87.3/77.8/70.1/63.4 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq-model-myrk2.99.0.21-1.23.0.38-1.47.pth
BLEU = 73.68, 87.0/77.6/69.6/62.7 (BP=1.000, ratio=1.036, hyp_len=23993, ref_len=23160)

real	32m36.037s
user	31m48.091s
sys	1m51.475s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/100epoch$
```

Best score က  

```
Evaluation result for the model: seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth
BLEU = 75.74, 88.1/79.3/71.9/65.5 (BP=1.000, ratio=1.026, hyp_len=23772, ref_len=23160)
```

### RL Fine-Tuning for Seq2Seq

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth --model_fn ./model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth --init_epoch 88 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 138
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 138
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 88
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 88,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth',
    'n_epochs': 138,
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
Epoch 88 - |param|=6.89e+02 |g_param|=1.10e+05 loss=2.2247e-01 ppl=1.25                                                 
Validation - loss=3.9549e-01 ppl=1.49 best_loss=inf best_ppl=inf                                                        
Epoch 89 - |param|=6.89e+02 |g_param|=5.70e+04 loss=2.2067e-01 ppl=1.25                                                 
Validation - loss=3.6748e-01 ppl=1.44 best_loss=3.9549e-01 best_ppl=1.49                                                
Epoch 90 - |param|=6.90e+02 |g_param|=3.33e+04 loss=2.1470e-01 ppl=1.24                                                 
Validation - loss=3.9607e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 91 - |param|=6.90e+02 |g_param|=2.13e+04 loss=2.2135e-01 ppl=1.25                                                 
Validation - loss=3.7194e-01 ppl=1.45 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 92 - |param|=6.90e+02 |g_param|=1.86e+04 loss=2.1177e-01 ppl=1.24                                                 
Validation - loss=3.7573e-01 ppl=1.46 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 93 - |param|=6.90e+02 |g_param|=1.87e+04 loss=2.2031e-01 ppl=1.25                                                 
Validation - loss=3.9690e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 94 - |param|=6.91e+02 |g_param|=1.63e+04 loss=2.0784e-01 ppl=1.23                                                 
Validation - loss=3.7830e-01 ppl=1.46 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 95 - |param|=6.91e+02 |g_param|=2.12e+04 loss=2.2997e-01 ppl=1.26                                                 
Validation - loss=4.0397e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 96 - |param|=6.92e+02 |g_param|=1.99e+04 loss=2.0698e-01 ppl=1.23                                                 
Validation - loss=3.9040e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 97 - |param|=6.92e+02 |g_param|=1.99e+04 loss=2.1649e-01 ppl=1.24                                                 
Validation - loss=3.8629e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 98 - |param|=6.92e+02 |g_param|=1.77e+04 loss=2.0915e-01 ppl=1.23                                                 
Validation - loss=3.8501e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 99 - |param|=6.93e+02 |g_param|=2.48e+04 loss=2.0064e-01 ppl=1.22                                                 
Validation - loss=4.0558e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 100 - |param|=6.93e+02 |g_param|=1.95e+04 loss=2.1027e-01 ppl=1.23                                                
Validation - loss=3.8852e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 101 - |param|=6.93e+02 |g_param|=1.84e+04 loss=1.9703e-01 ppl=1.22                                                
Validation - loss=3.9049e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 102 - |param|=6.94e+02 |g_param|=2.33e+04 loss=2.1020e-01 ppl=1.23                                                
Validation - loss=4.0995e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 103 - |param|=6.94e+02 |g_param|=3.01e+04 loss=2.2639e-01 ppl=1.25                                                
Validation - loss=4.1492e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 104 - |param|=6.94e+02 |g_param|=2.68e+04 loss=2.2235e-01 ppl=1.25                                                
Validation - loss=3.9320e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 105 - |param|=6.95e+02 |g_param|=2.24e+04 loss=2.0341e-01 ppl=1.23                                                
Validation - loss=3.8293e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 106 - |param|=6.95e+02 |g_param|=1.75e+04 loss=1.9633e-01 ppl=1.22                                                
Validation - loss=3.8392e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 107 - |param|=6.95e+02 |g_param|=1.83e+04 loss=1.9197e-01 ppl=1.21                                                
Validation - loss=3.9875e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 108 - |param|=6.96e+02 |g_param|=3.73e+04 loss=1.9094e-01 ppl=1.21                                                
Validation - loss=3.8809e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 109 - |param|=6.96e+02 |g_param|=4.53e+04 loss=1.9057e-01 ppl=1.21                                                
Validation - loss=3.8817e-01 ppl=1.47 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 110 - |param|=6.96e+02 |g_param|=4.61e+04 loss=1.8804e-01 ppl=1.21                                                
Validation - loss=3.9798e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 111 - |param|=6.97e+02 |g_param|=3.89e+04 loss=1.8591e-01 ppl=1.20                                                
Validation - loss=4.0466e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 112 - |param|=6.97e+02 |g_param|=2.53e+04 loss=1.7439e-01 ppl=1.19                                                
Validation - loss=3.9162e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 113 - |param|=6.97e+02 |g_param|=1.92e+04 loss=1.7640e-01 ppl=1.19                                                
Validation - loss=3.9651e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 114 - |param|=6.98e+02 |g_param|=1.60e+04 loss=1.7643e-01 ppl=1.19                                                
Validation - loss=4.0214e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 115 - |param|=6.98e+02 |g_param|=1.74e+04 loss=1.7456e-01 ppl=1.19                                                
Validation - loss=4.0727e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 116 - |param|=6.98e+02 |g_param|=1.96e+04 loss=1.7775e-01 ppl=1.19                                                
Validation - loss=3.9909e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 117 - |param|=6.99e+02 |g_param|=2.24e+04 loss=1.9090e-01 ppl=1.21                                                
Validation - loss=4.0419e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 118 - |param|=6.99e+02 |g_param|=2.11e+04 loss=1.8011e-01 ppl=1.20                                                
Validation - loss=4.0127e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 119 - |param|=6.99e+02 |g_param|=2.14e+04 loss=1.7654e-01 ppl=1.19                                                
Validation - loss=3.9736e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 120 - |param|=7.00e+02 |g_param|=2.52e+04 loss=1.6812e-01 ppl=1.18                                                
Validation - loss=4.0168e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 121 - |param|=7.00e+02 |g_param|=2.21e+04 loss=1.7704e-01 ppl=1.19                                                
Validation - loss=3.9448e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 122 - |param|=7.00e+02 |g_param|=2.67e+04 loss=1.8602e-01 ppl=1.20                                                
Validation - loss=4.1487e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 123 - |param|=7.01e+02 |g_param|=1.79e+04 loss=1.7367e-01 ppl=1.19                                                
Validation - loss=4.0105e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 124 - |param|=7.01e+02 |g_param|=2.25e+04 loss=1.6614e-01 ppl=1.18                                                
Validation - loss=4.1129e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 125 - |param|=7.01e+02 |g_param|=2.26e+04 loss=1.7292e-01 ppl=1.19                                                
Validation - loss=4.0765e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 126 - |param|=7.02e+02 |g_param|=2.51e+04 loss=1.7677e-01 ppl=1.19                                                
Validation - loss=4.0968e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 127 - |param|=7.02e+02 |g_param|=2.55e+04 loss=1.8203e-01 ppl=1.20                                                
Validation - loss=4.2144e-01 ppl=1.52 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 128 - |param|=7.03e+02 |g_param|=2.71e+04 loss=1.8538e-01 ppl=1.20                                                
Validation - loss=4.1877e-01 ppl=1.52 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 129 - |param|=7.03e+02 |g_param|=3.50e+04 loss=1.6376e-01 ppl=1.18                                                
Validation - loss=4.0522e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 130 - |param|=7.03e+02 |g_param|=3.42e+04 loss=1.5376e-01 ppl=1.17                                                
Validation - loss=3.9755e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 131 - |param|=7.04e+02 |g_param|=2.99e+04 loss=1.5370e-01 ppl=1.17                                                
Validation - loss=3.9799e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 132 - |param|=7.04e+02 |g_param|=3.18e+04 loss=1.4615e-01 ppl=1.16                                                
Validation - loss=4.0157e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 133 - |param|=7.04e+02 |g_param|=3.58e+04 loss=1.5168e-01 ppl=1.16                                                
Validation - loss=3.9399e-01 ppl=1.48 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 134 - |param|=7.04e+02 |g_param|=3.41e+04 loss=1.5445e-01 ppl=1.17                                                
Validation - loss=4.1831e-01 ppl=1.52 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 135 - |param|=7.05e+02 |g_param|=3.22e+04 loss=1.4483e-01 ppl=1.16                                                
Validation - loss=4.1230e-01 ppl=1.51 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 136 - |param|=7.05e+02 |g_param|=3.53e+04 loss=1.3769e-01 ppl=1.15                                                
Validation - loss=4.0042e-01 ppl=1.49 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 137 - |param|=7.05e+02 |g_param|=3.03e+04 loss=1.4092e-01 ppl=1.15                                                
Validation - loss=4.0342e-01 ppl=1.50 best_loss=3.6748e-01 best_ppl=1.44                                                
Epoch 138 - |param|=7.06e+02 |g_param|=4.35e+04 loss=1.5317e-01 ppl=1.17                                                
Validation - loss=4.5551e-01 ppl=1.58 best_loss=3.6748e-01 best_ppl=1.44                                                

real	10m54.285s
user	10m44.961s
sys	0m9.200s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation with 100 epoch RL-fine tuning...  
Baseline က BLEU = 75.74  

```
Evaluation result for the model: seq-rl-model-myrk.101.0.20-1.22.0.39-1.48.pth
BLEU = 75.35, 88.0/78.9/71.4/65.0 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
...
Evaluation result for the model: seq-rl-model-myrk.104.0.22-1.25.0.39-1.48.pth
BLEU = 75.41, 88.3/79.1/71.4/64.9 (BP=1.000, ratio=1.027, hyp_len=23795, ref_len=23160)
...
Evaluation result for the model: seq-rl-model-myrk.112.0.17-1.19.0.39-1.48.pth
BLEU = 75.23, 88.0/78.8/71.3/64.8 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.113.0.18-1.19.0.40-1.49.pth
BLEU = 75.27, 87.9/78.8/71.3/64.9 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
...
...

Evaluation result for the model: seq-rl-model-myrk.136.0.14-1.15.0.40-1.49.pth
BLEU = 75.35, 88.2/79.0/71.4/64.8 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)
...
...
Evaluation result for the model: seq-rl-model-myrk.90.0.21-1.24.0.40-1.49.pth
BLEU = 75.58, 88.2/79.2/71.7/65.2 (BP=1.000, ratio=1.027, hyp_len=23783, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.22-1.25.0.37-1.45.pth
BLEU = 75.38, 87.9/78.9/71.5/65.1 (BP=1.000, ratio=1.031, hyp_len=23872, ref_len=23160)
```

baseline ကို မကျော်နိုင်ဘူး...  

--max_grad_norm 2e+8 လုပ်ပြီး run ကြည့်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth --model_fn ./model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth --init_epoch 88 --iteration_per_update 2 --max_grad_norm 2e+8 --n_epochs 138
...
...
NLLLoss()
Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.999)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)
Epoch 88 - |param|=6.89e+02 |g_param|=9.97e+04 loss=2.2298e-01 ppl=1.25                                                 
Validation - loss=3.8332e-01 ppl=1.47 best_loss=inf best_ppl=inf                                                        
Epoch 89 - |param|=6.89e+02 |g_param|=4.72e+04 loss=2.2163e-01 ppl=1.25                                                 
Validation - loss=3.8430e-01 ppl=1.47 best_loss=3.8332e-01 best_ppl=1.47                                                
Epoch 90 - |param|=6.89e+02 |g_param|=4.72e+04 loss=2.2330e-01 ppl=1.25                                                 
Validation - loss=3.7670e-01 ppl=1.46 best_loss=3.8332e-01 best_ppl=1.47                                                
Epoch 91 - |param|=6.90e+02 |g_param|=3.74e+04 loss=2.1726e-01 ppl=1.24                                                 
Validation - loss=3.9497e-01 ppl=1.48 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 92 - |param|=6.90e+02 |g_param|=3.88e+04 loss=2.1994e-01 ppl=1.25                                                 
Validation - loss=3.9120e-01 ppl=1.48 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 93 - |param|=6.90e+02 |g_param|=3.71e+04 loss=2.2311e-01 ppl=1.25                                                 
Validation - loss=3.9311e-01 ppl=1.48 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 94 - |param|=6.91e+02 |g_param|=3.60e+04 loss=2.1674e-01 ppl=1.24                                                 
Validation - loss=3.8690e-01 ppl=1.47 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 95 - |param|=6.91e+02 |g_param|=3.47e+04 loss=2.1648e-01 ppl=1.24                                                 
Validation - loss=3.9141e-01 ppl=1.48 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 96 - |param|=6.92e+02 |g_param|=4.50e+04 loss=2.1817e-01 ppl=1.24                                                 
Validation - loss=3.8409e-01 ppl=1.47 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 97 - |param|=6.92e+02 |g_param|=3.95e+04 loss=2.1652e-01 ppl=1.24                                                 
Validation - loss=3.7911e-01 ppl=1.46 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 98 - |param|=6.92e+02 |g_param|=4.40e+04 loss=2.1260e-01 ppl=1.24                                                 
Validation - loss=4.0628e-01 ppl=1.50 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 99 - |param|=6.93e+02 |g_param|=4.28e+04 loss=2.1147e-01 ppl=1.24                                                 
Validation - loss=3.8796e-01 ppl=1.47 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 100 - |param|=6.93e+02 |g_param|=4.01e+04 loss=2.0213e-01 ppl=1.22                                                
Validation - loss=3.9611e-01 ppl=1.49 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 101 - |param|=6.93e+02 |g_param|=4.04e+04 loss=2.1029e-01 ppl=1.23                                                
Validation - loss=3.6884e-01 ppl=1.45 best_loss=3.7670e-01 best_ppl=1.46                                                
Epoch 102 - |param|=6.94e+02 |g_param|=2.42e+04 loss=1.9834e-01 ppl=1.22                                                
Validation - loss=3.9090e-01 ppl=1.48 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 103 - |param|=6.94e+02 |g_param|=2.11e+04 loss=1.9248e-01 ppl=1.21                                                
Validation - loss=4.0038e-01 ppl=1.49 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 104 - |param|=6.94e+02 |g_param|=1.84e+04 loss=1.9661e-01 ppl=1.22                                                
Validation - loss=3.9138e-01 ppl=1.48 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 105 - |param|=6.95e+02 |g_param|=3.52e+04 loss=2.4317e-01 ppl=1.28                                                
Validation - loss=4.2420e-01 ppl=1.53 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 106 - |param|=6.95e+02 |g_param|=2.07e+04 loss=2.6968e-01 ppl=1.31                                                
Validation - loss=4.2811e-01 ppl=1.53 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 107 - |param|=6.96e+02 |g_param|=1.18e+04 loss=2.2777e-01 ppl=1.26                                                
Validation - loss=4.2349e-01 ppl=1.53 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 108 - |param|=6.96e+02 |g_param|=9.08e+03 loss=2.0073e-01 ppl=1.22                                                
Validation - loss=3.9707e-01 ppl=1.49 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 109 - |param|=6.96e+02 |g_param|=8.69e+03 loss=1.8802e-01 ppl=1.21                                                
Validation - loss=4.0174e-01 ppl=1.49 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 110 - |param|=6.97e+02 |g_param|=7.95e+03 loss=1.9135e-01 ppl=1.21                                                
Validation - loss=3.8825e-01 ppl=1.47 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 111 - |param|=6.97e+02 |g_param|=1.01e+04 loss=1.8793e-01 ppl=1.21                                                
Validation - loss=3.8172e-01 ppl=1.46 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 112 - |param|=6.97e+02 |g_param|=9.07e+03 loss=1.7856e-01 ppl=1.20                                                
Validation - loss=3.6856e-01 ppl=1.45 best_loss=3.6884e-01 best_ppl=1.45                                                
Epoch 113 - |param|=6.97e+02 |g_param|=8.22e+03 loss=1.7349e-01 ppl=1.19                                                
Validation - loss=3.9333e-01 ppl=1.48 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 114 - |param|=6.98e+02 |g_param|=8.08e+03 loss=1.7737e-01 ppl=1.19                                                
Validation - loss=3.7260e-01 ppl=1.45 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 115 - |param|=6.98e+02 |g_param|=9.44e+03 loss=1.7960e-01 ppl=1.20                                                
Validation - loss=3.7774e-01 ppl=1.46 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 116 - |param|=6.98e+02 |g_param|=8.14e+03 loss=1.6927e-01 ppl=1.18                                                
Validation - loss=3.8353e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 117 - |param|=6.99e+02 |g_param|=7.74e+03 loss=1.6819e-01 ppl=1.18                                                
Validation - loss=3.7094e-01 ppl=1.45 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 118 - |param|=6.99e+02 |g_param|=8.86e+03 loss=1.7027e-01 ppl=1.19                                                
Validation - loss=3.8302e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 119 - |param|=6.99e+02 |g_param|=9.69e+03 loss=1.6734e-01 ppl=1.18                                                
Validation - loss=3.8799e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 120 - |param|=7.00e+02 |g_param|=1.00e+04 loss=1.8039e-01 ppl=1.20                                                
Validation - loss=3.8682e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 121 - |param|=7.00e+02 |g_param|=8.65e+03 loss=1.6935e-01 ppl=1.18                                                
Validation - loss=3.8467e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 122 - |param|=7.00e+02 |g_param|=1.61e+04 loss=1.6088e-01 ppl=1.17                                                
Validation - loss=3.7114e-01 ppl=1.45 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 123 - |param|=7.01e+02 |g_param|=1.79e+04 loss=1.6636e-01 ppl=1.18                                                
Validation - loss=3.9872e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 124 - |param|=7.01e+02 |g_param|=1.61e+04 loss=1.6022e-01 ppl=1.17                                                
Validation - loss=4.0037e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 125 - |param|=7.01e+02 |g_param|=1.70e+04 loss=1.6577e-01 ppl=1.18                                                
Validation - loss=3.8377e-01 ppl=1.47 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 126 - |param|=7.02e+02 |g_param|=1.50e+04 loss=1.5051e-01 ppl=1.16                                                
Validation - loss=3.9714e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 127 - |param|=7.02e+02 |g_param|=1.78e+04 loss=1.5808e-01 ppl=1.17                                                
Validation - loss=3.9795e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 128 - |param|=7.02e+02 |g_param|=2.00e+04 loss=1.5349e-01 ppl=1.17                                                
Validation - loss=3.9955e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 129 - |param|=7.03e+02 |g_param|=2.29e+04 loss=1.5885e-01 ppl=1.17                                                
Validation - loss=4.3872e-01 ppl=1.55 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 130 - |param|=7.03e+02 |g_param|=2.12e+04 loss=1.6074e-01 ppl=1.17                                                
Validation - loss=3.9937e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 131 - |param|=7.03e+02 |g_param|=2.10e+04 loss=1.6107e-01 ppl=1.17                                                
Validation - loss=4.1306e-01 ppl=1.51 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 132 - |param|=7.04e+02 |g_param|=2.21e+04 loss=1.4790e-01 ppl=1.16                                                
Validation - loss=3.9631e-01 ppl=1.49 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 133 - |param|=7.04e+02 |g_param|=2.55e+04 loss=1.6450e-01 ppl=1.18                                                
Validation - loss=4.0583e-01 ppl=1.50 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 134 - |param|=7.04e+02 |g_param|=1.61e+04 loss=1.4830e-01 ppl=1.16                                                
Validation - loss=4.1857e-01 ppl=1.52 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 135 - |param|=7.05e+02 |g_param|=1.53e+04 loss=1.4099e-01 ppl=1.15                                                
Validation - loss=3.9363e-01 ppl=1.48 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 136 - |param|=7.05e+02 |g_param|=1.82e+04 loss=1.3931e-01 ppl=1.15                                                
Validation - loss=4.1920e-01 ppl=1.52 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 137 - |param|=7.05e+02 |g_param|=1.56e+04 loss=1.3770e-01 ppl=1.15                                                
Validation - loss=4.2000e-01 ppl=1.52 best_loss=3.6856e-01 best_ppl=1.45                                                
Epoch 138 - |param|=7.06e+02 |g_param|=2.71e+04 loss=1.3783e-01 ppl=1.15                                                
Validation - loss=3.9234e-01 ppl=1.48 best_loss=3.6856e-01 best_ppl=1.45                                                

real	10m44.235s
user	10m36.044s
sys	0m8.614s
```

Baseline က BLEU = 75.74  
ဒီ တစ်ခေါက် BLEU score 75 တွေ အများကြီး ရလာတယ် ...  
အခုချိန်ထိ တစ်ခါမှာ ဒီလောက်ထိ များများ မရဖူးဘူး...  
သို့သော် baseline ကိုတော့ မကျော်ဘူး...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$ grep -B 1 "BLEU = 75." ./eval-results-myrk-seq2seq-100epoch-max_grad_norm-2e8-rl-138epoch-test.txt 
Evaluation result for the model: seq-rl-model-myrk.100.0.20-1.22.0.40-1.49.pth
BLEU = 75.07, 87.8/78.7/71.1/64.6 (BP=1.000, ratio=1.029, hyp_len=23842, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.103.0.19-1.21.0.40-1.49.pth
BLEU = 75.61, 88.1/79.1/71.7/65.4 (BP=1.000, ratio=1.026, hyp_len=23772, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.108.0.20-1.22.0.40-1.49.pth
BLEU = 75.17, 87.9/78.8/71.2/64.7 (BP=1.000, ratio=1.030, hyp_len=23862, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.109.0.19-1.21.0.40-1.49.pth
BLEU = 75.25, 87.8/78.8/71.4/65.0 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.113.0.17-1.19.0.39-1.48.pth
BLEU = 75.05, 87.7/78.7/71.1/64.6 (BP=1.000, ratio=1.030, hyp_len=23856, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.117.0.17-1.18.0.37-1.45.pth
BLEU = 75.46, 88.1/79.0/71.6/65.1 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.121.0.17-1.18.0.38-1.47.pth
BLEU = 75.27, 87.8/78.8/71.4/65.0 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.124.0.16-1.17.0.40-1.49.pth
BLEU = 75.07, 87.8/78.7/71.2/64.6 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.130.0.16-1.17.0.40-1.49.pth
BLEU = 75.12, 87.9/78.7/71.2/64.7 (BP=1.000, ratio=1.032, hyp_len=23903, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.134.0.15-1.16.0.42-1.52.pth
BLEU = 75.29, 87.9/78.9/71.4/64.9 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.88.0.22-1.25.0.38-1.47.pth
BLEU = 75.40, 88.1/79.0/71.4/65.0 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.93.0.22-1.25.0.39-1.48.pth
BLEU = 75.44, 88.3/79.1/71.4/64.9 (BP=1.000, ratio=1.027, hyp_len=23788, ref_len=23160)
--
Evaluation result for the model: seq-rl-model-myrk.97.0.22-1.24.0.38-1.46.pth
BLEU = 75.18, 87.9/78.8/71.2/64.8 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$
```

ဒီတစ်ခါတော့ 3e+8 ထားကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth --model_fn ./model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth --init_epoch 88 --iteration_per_update 2 --max_grad_norm 3e+8 --n_epochs 138
...
...
Epoch 88 - |param|=6.89e+02 |g_param|=1.33e+05 loss=2.2468e-01 ppl=1.25                                                 
Validation - loss=3.7779e-01 ppl=1.46 best_loss=inf best_ppl=inf                                                        
Epoch 89 - |param|=6.89e+02 |g_param|=8.22e+04 loss=2.2071e-01 ppl=1.25                                                 
Validation - loss=3.7833e-01 ppl=1.46 best_loss=3.7779e-01 best_ppl=1.46                                                
Epoch 90 - |param|=6.90e+02 |g_param|=3.73e+04 loss=2.2119e-01 ppl=1.25                                                 
Validation - loss=3.7524e-01 ppl=1.46 best_loss=3.7779e-01 best_ppl=1.46                                                
Epoch 91 - |param|=6.90e+02 |g_param|=4.16e+04 loss=2.4363e-01 ppl=1.28                                                 
Validation - loss=3.8150e-01 ppl=1.46 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 92 - |param|=6.90e+02 |g_param|=2.50e+04 loss=2.1390e-01 ppl=1.24                                                 
Validation - loss=3.7765e-01 ppl=1.46 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 93 - |param|=6.91e+02 |g_param|=1.98e+04 loss=2.2270e-01 ppl=1.25                                                 
Validation - loss=4.0026e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 94 - |param|=6.91e+02 |g_param|=2.34e+04 loss=2.2343e-01 ppl=1.25                                                 
Validation - loss=3.8715e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 95 - |param|=6.91e+02 |g_param|=2.13e+04 loss=2.1368e-01 ppl=1.24                                                 
Validation - loss=3.9112e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 96 - |param|=6.92e+02 |g_param|=1.88e+04 loss=2.2049e-01 ppl=1.25                                                 
Validation - loss=4.0008e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 97 - |param|=6.92e+02 |g_param|=1.61e+04 loss=2.0750e-01 ppl=1.23                                                 
Validation - loss=4.0252e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 98 - |param|=6.92e+02 |g_param|=1.78e+04 loss=2.0522e-01 ppl=1.23                                                 
Validation - loss=4.1099e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 99 - |param|=6.93e+02 |g_param|=2.08e+04 loss=2.0059e-01 ppl=1.22                                                 
Validation - loss=4.0321e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 100 - |param|=6.93e+02 |g_param|=2.35e+04 loss=2.1683e-01 ppl=1.24                                                
Validation - loss=3.8410e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 101 - |param|=6.93e+02 |g_param|=2.22e+04 loss=2.0889e-01 ppl=1.23                                                
Validation - loss=3.9369e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 102 - |param|=6.94e+02 |g_param|=2.09e+04 loss=2.0797e-01 ppl=1.23                                                
Validation - loss=3.8098e-01 ppl=1.46 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 103 - |param|=6.94e+02 |g_param|=1.95e+04 loss=2.0584e-01 ppl=1.23                                                
Validation - loss=3.8643e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 104 - |param|=6.94e+02 |g_param|=1.58e+04 loss=1.9350e-01 ppl=1.21                                                
Validation - loss=3.7571e-01 ppl=1.46 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 105 - |param|=6.95e+02 |g_param|=1.69e+04 loss=1.9394e-01 ppl=1.21                                                
Validation - loss=3.8339e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 106 - |param|=6.95e+02 |g_param|=1.77e+04 loss=1.8930e-01 ppl=1.21                                                
Validation - loss=3.8816e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 107 - |param|=6.95e+02 |g_param|=1.68e+04 loss=1.9157e-01 ppl=1.21                                                
Validation - loss=4.0409e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 108 - |param|=6.96e+02 |g_param|=1.70e+04 loss=1.8459e-01 ppl=1.20                                                
Validation - loss=4.0068e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 109 - |param|=6.96e+02 |g_param|=4.42e+04 loss=1.8801e-01 ppl=1.21                                                
Validation - loss=4.0019e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 110 - |param|=6.96e+02 |g_param|=4.89e+04 loss=2.0472e-01 ppl=1.23                                                
Validation - loss=4.1472e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 111 - |param|=6.97e+02 |g_param|=3.76e+04 loss=1.8406e-01 ppl=1.20                                                
Validation - loss=3.9316e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 112 - |param|=6.97e+02 |g_param|=3.25e+04 loss=1.7995e-01 ppl=1.20                                                
Validation - loss=3.8564e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 113 - |param|=6.97e+02 |g_param|=3.23e+04 loss=1.6837e-01 ppl=1.18                                                
Validation - loss=4.0184e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 114 - |param|=6.98e+02 |g_param|=3.71e+04 loss=1.7761e-01 ppl=1.19                                                
Validation - loss=3.9620e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 115 - |param|=6.98e+02 |g_param|=3.38e+04 loss=1.7737e-01 ppl=1.19                                                
Validation - loss=4.0938e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 116 - |param|=6.98e+02 |g_param|=3.98e+04 loss=1.7014e-01 ppl=1.19                                                
Validation - loss=3.8348e-01 ppl=1.47 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 117 - |param|=6.99e+02 |g_param|=3.34e+04 loss=1.7180e-01 ppl=1.19                                                
Validation - loss=4.0647e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 118 - |param|=6.99e+02 |g_param|=3.44e+04 loss=1.6663e-01 ppl=1.18                                                
Validation - loss=4.0133e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 119 - |param|=6.99e+02 |g_param|=3.17e+04 loss=1.7014e-01 ppl=1.19                                                
Validation - loss=4.0909e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 120 - |param|=7.00e+02 |g_param|=3.75e+04 loss=1.6120e-01 ppl=1.17                                                
Validation - loss=4.1526e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 121 - |param|=7.00e+02 |g_param|=4.49e+04 loss=1.6964e-01 ppl=1.18                                                
Validation - loss=4.0879e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 122 - |param|=7.00e+02 |g_param|=4.03e+04 loss=1.6334e-01 ppl=1.18                                                
Validation - loss=4.0453e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 123 - |param|=7.01e+02 |g_param|=3.62e+04 loss=1.6187e-01 ppl=1.18                                                
Validation - loss=3.9780e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 124 - |param|=7.01e+02 |g_param|=3.92e+04 loss=1.6440e-01 ppl=1.18                                                
Validation - loss=4.0220e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 125 - |param|=7.01e+02 |g_param|=3.49e+04 loss=1.5346e-01 ppl=1.17                                                
Validation - loss=4.0897e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 126 - |param|=7.02e+02 |g_param|=3.13e+04 loss=1.5430e-01 ppl=1.17                                                
Validation - loss=4.0508e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 127 - |param|=7.02e+02 |g_param|=3.32e+04 loss=1.5194e-01 ppl=1.16                                                
Validation - loss=3.9468e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 128 - |param|=7.02e+02 |g_param|=2.92e+04 loss=1.4875e-01 ppl=1.16                                                
Validation - loss=3.9797e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 129 - |param|=7.03e+02 |g_param|=1.59e+04 loss=1.4369e-01 ppl=1.15                                                
Validation - loss=3.9190e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 130 - |param|=7.03e+02 |g_param|=2.00e+04 loss=1.5481e-01 ppl=1.17                                                
Validation - loss=4.1189e-01 ppl=1.51 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 131 - |param|=7.03e+02 |g_param|=2.47e+04 loss=1.7123e-01 ppl=1.19                                                
Validation - loss=3.9953e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 132 - |param|=7.04e+02 |g_param|=2.43e+04 loss=1.5821e-01 ppl=1.17                                                
Validation - loss=4.2132e-01 ppl=1.52 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 133 - |param|=7.04e+02 |g_param|=2.13e+04 loss=1.4647e-01 ppl=1.16                                                
Validation - loss=4.0275e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 134 - |param|=7.04e+02 |g_param|=2.07e+04 loss=1.5197e-01 ppl=1.16                                                
Validation - loss=3.9090e-01 ppl=1.48 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 135 - |param|=7.05e+02 |g_param|=1.83e+04 loss=1.4282e-01 ppl=1.15                                                
Validation - loss=4.1962e-01 ppl=1.52 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 136 - |param|=7.05e+02 |g_param|=1.79e+04 loss=1.4504e-01 ppl=1.16                                                
Validation - loss=4.1677e-01 ppl=1.52 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 137 - |param|=7.05e+02 |g_param|=1.53e+04 loss=1.3351e-01 ppl=1.14                                                
Validation - loss=4.0380e-01 ppl=1.50 best_loss=3.7524e-01 best_ppl=1.46                                                
Epoch 138 - |param|=7.06e+02 |g_param|=1.58e+04 loss=1.3383e-01 ppl=1.14                                                
Validation - loss=3.9610e-01 ppl=1.49 best_loss=3.7524e-01 best_ppl=1.46                                                

real	10m54.247s
user	10m45.926s
sys	0m8.804s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.100.0.22-1.24.0.38-1.47.pth
BLEU = 74.53, 87.7/78.3/70.4/63.8 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.101.0.21-1.23.0.39-1.48.pth
BLEU = 73.69, 87.1/77.5/69.6/62.8 (BP=1.000, ratio=1.038, hyp_len=24038, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.102.0.21-1.23.0.38-1.46.pth
BLEU = 74.78, 87.8/78.5/70.7/64.1 (BP=1.000, ratio=1.033, hyp_len=23917, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.103.0.21-1.23.0.39-1.47.pth
BLEU = 74.97, 87.6/78.5/71.1/64.6 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.104.0.19-1.21.0.38-1.46.pth
BLEU = 75.06, 88.0/78.8/71.0/64.5 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.105.0.19-1.21.0.38-1.47.pth
BLEU = 74.07, 87.3/77.9/70.0/63.3 (BP=1.000, ratio=1.036, hyp_len=24001, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.106.0.19-1.21.0.39-1.47.pth
BLEU = 74.84, 87.6/78.5/70.9/64.3 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.107.0.19-1.21.0.40-1.50.pth
BLEU = 74.86, 87.7/78.5/70.9/64.3 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.108.0.18-1.20.0.40-1.49.pth
BLEU = 75.90, 88.3/79.4/72.0/65.7 (BP=1.000, ratio=1.029, hyp_len=23835, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.109.0.19-1.21.0.40-1.49.pth
BLEU = 74.10, 87.4/77.9/70.0/63.2 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.110.0.20-1.23.0.41-1.51.pth
BLEU = 74.72, 87.9/78.4/70.7/63.9 (BP=1.000, ratio=1.023, hyp_len=23699, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.111.0.18-1.20.0.39-1.48.pth
BLEU = 74.71, 87.8/78.4/70.7/64.0 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.112.0.18-1.20.0.39-1.47.pth
BLEU = 74.21, 87.3/77.9/70.2/63.6 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.113.0.17-1.18.0.40-1.49.pth
BLEU = 74.67, 87.6/78.4/70.7/64.1 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.114.0.18-1.19.0.40-1.49.pth
BLEU = 74.44, 87.5/78.2/70.4/63.7 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.115.0.18-1.19.0.41-1.51.pth
BLEU = 74.96, 87.8/78.6/71.0/64.4 (BP=1.000, ratio=1.029, hyp_len=23823, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.116.0.17-1.19.0.38-1.47.pth
BLEU = 74.62, 87.6/78.4/70.6/63.9 (BP=1.000, ratio=1.034, hyp_len=23941, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.117.0.17-1.19.0.41-1.50.pth
BLEU = 74.92, 87.7/78.6/71.0/64.4 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.118.0.17-1.18.0.40-1.49.pth
BLEU = 74.81, 87.6/78.5/70.9/64.3 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.119.0.17-1.19.0.41-1.51.pth
BLEU = 75.30, 88.1/79.0/71.3/64.8 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.120.0.16-1.17.0.42-1.51.pth
BLEU = 74.72, 87.7/78.4/70.8/64.1 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.121.0.17-1.18.0.41-1.51.pth
BLEU = 73.57, 87.0/77.5/69.5/62.6 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.122.0.16-1.18.0.40-1.50.pth
BLEU = 74.57, 87.6/78.3/70.5/64.0 (BP=1.000, ratio=1.035, hyp_len=23965, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.123.0.16-1.18.0.40-1.49.pth
BLEU = 74.54, 87.7/78.3/70.5/63.8 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.124.0.16-1.18.0.40-1.50.pth
BLEU = 74.91, 87.9/78.6/70.9/64.3 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.125.0.15-1.17.0.41-1.51.pth
BLEU = 74.64, 87.6/78.3/70.6/64.1 (BP=1.000, ratio=1.033, hyp_len=23919, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.126.0.15-1.17.0.41-1.50.pth
BLEU = 74.84, 87.7/78.5/70.9/64.3 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.127.0.15-1.16.0.39-1.48.pth
BLEU = 74.24, 87.6/78.0/70.1/63.4 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.128.0.15-1.16.0.40-1.49.pth
BLEU = 75.05, 88.0/78.8/71.0/64.4 (BP=1.000, ratio=1.032, hyp_len=23901, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.129.0.14-1.15.0.39-1.48.pth
BLEU = 75.22, 88.0/78.9/71.3/64.7 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.130.0.15-1.17.0.41-1.51.pth
BLEU = 74.63, 87.7/78.5/70.6/63.8 (BP=1.000, ratio=1.030, hyp_len=23846, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.131.0.17-1.19.0.40-1.49.pth
BLEU = 73.53, 87.2/77.4/69.3/62.4 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.132.0.16-1.17.0.42-1.52.pth
BLEU = 74.97, 87.7/78.6/71.0/64.5 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.133.0.15-1.16.0.40-1.50.pth
BLEU = 75.12, 88.0/78.8/71.1/64.6 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.134.0.15-1.16.0.39-1.48.pth
BLEU = 74.10, 87.3/77.9/70.1/63.3 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.135.0.14-1.15.0.42-1.52.pth
BLEU = 74.94, 87.9/78.6/71.0/64.3 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.136.0.15-1.16.0.42-1.52.pth
BLEU = 75.56, 88.1/79.1/71.7/65.3 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.137.0.13-1.14.0.40-1.50.pth
BLEU = 75.08, 88.0/78.7/71.1/64.6 (BP=1.000, ratio=1.032, hyp_len=23898, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.138.0.13-1.14.0.40-1.49.pth
BLEU = 75.22, 88.1/78.9/71.2/64.6 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.22-1.25.0.38-1.46.pth
BLEU = 74.87, 87.6/78.5/71.0/64.4 (BP=1.000, ratio=1.030, hyp_len=23848, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.22-1.25.0.38-1.46.pth
BLEU = 75.53, 88.1/79.1/71.6/65.2 (BP=1.000, ratio=1.028, hyp_len=23797, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.22-1.25.0.38-1.46.pth
BLEU = 75.16, 87.8/78.8/71.2/64.8 (BP=1.000, ratio=1.031, hyp_len=23878, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.24-1.28.0.38-1.46.pth
BLEU = 74.45, 87.4/78.2/70.4/63.8 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.21-1.24.0.38-1.46.pth
BLEU = 75.07, 88.0/78.8/71.0/64.5 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.22-1.25.0.40-1.49.pth
BLEU = 74.67, 87.5/78.3/70.7/64.2 (BP=1.000, ratio=1.032, hyp_len=23902, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.22-1.25.0.39-1.47.pth
BLEU = 74.33, 87.3/78.0/70.3/63.7 (BP=1.000, ratio=1.031, hyp_len=23888, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.21-1.24.0.39-1.48.pth
BLEU = 74.68, 87.5/78.4/70.7/64.1 (BP=1.000, ratio=1.033, hyp_len=23935, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.22-1.25.0.40-1.49.pth
BLEU = 74.52, 87.6/78.3/70.5/63.8 (BP=1.000, ratio=1.034, hyp_len=23946, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.21-1.23.0.40-1.50.pth
BLEU = 74.83, 87.6/78.4/70.9/64.4 (BP=1.000, ratio=1.030, hyp_len=23861, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.21-1.23.0.41-1.51.pth
BLEU = 74.63, 87.4/78.3/70.7/64.1 (BP=1.000, ratio=1.034, hyp_len=23950, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.20-1.22.0.40-1.50.pth
BLEU = 74.81, 87.8/78.6/70.7/64.1 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)

real	18m0.202s
user	17m34.902s
sys	0m56.526s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$ 
```

ဒီတစ်ခါတော့ 4e+8 ထားကြည့်ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/100epoch/seq-model-myrk2.88.0.24-1.27.0.38-1.47.pth --model_fn ./model/rl/seq2seq/100epoch/seq-rl-model-myrk.pth --init_epoch 88 --iteration_per_update 2 --max_grad_norm 4e+8 --n_epochs 138
...
...
...
Epoch 88 - |param|=6.89e+02 |g_param|=1.14e+05 loss=2.3036e-01 ppl=1.26                                                 
Validation - loss=3.8638e-01 ppl=1.47 best_loss=inf best_ppl=inf                                                        
Epoch 89 - |param|=6.89e+02 |g_param|=6.47e+04 loss=2.1413e-01 ppl=1.24                                                 
Validation - loss=3.8647e-01 ppl=1.47 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 90 - |param|=6.90e+02 |g_param|=5.01e+04 loss=2.1991e-01 ppl=1.25                                                 
Validation - loss=4.0027e-01 ppl=1.49 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 91 - |param|=6.90e+02 |g_param|=3.63e+04 loss=2.1927e-01 ppl=1.25                                                 
Validation - loss=4.0286e-01 ppl=1.50 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 92 - |param|=6.90e+02 |g_param|=3.79e+04 loss=2.2199e-01 ppl=1.25                                                 
Validation - loss=3.9934e-01 ppl=1.49 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 93 - |param|=6.90e+02 |g_param|=3.86e+04 loss=2.1095e-01 ppl=1.23                                                 
Validation - loss=3.9815e-01 ppl=1.49 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 94 - |param|=6.91e+02 |g_param|=2.74e+04 loss=2.1273e-01 ppl=1.24                                                 
Validation - loss=4.0101e-01 ppl=1.49 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 95 - |param|=6.91e+02 |g_param|=1.95e+04 loss=2.1064e-01 ppl=1.23                                                 
Validation - loss=3.9054e-01 ppl=1.48 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 96 - |param|=6.91e+02 |g_param|=1.85e+04 loss=2.1829e-01 ppl=1.24                                                 
Validation - loss=3.8632e-01 ppl=1.47 best_loss=3.8638e-01 best_ppl=1.47                                                
Epoch 97 - |param|=6.92e+02 |g_param|=2.20e+04 loss=2.0895e-01 ppl=1.23                                                 
Validation - loss=3.8826e-01 ppl=1.47 best_loss=3.8632e-01 best_ppl=1.47                                                
Epoch 98 - |param|=6.92e+02 |g_param|=2.18e+04 loss=2.1770e-01 ppl=1.24                                                 
Validation - loss=3.9335e-01 ppl=1.48 best_loss=3.8632e-01 best_ppl=1.47                                                
Epoch 99 - |param|=6.93e+02 |g_param|=1.76e+04 loss=2.1376e-01 ppl=1.24                                                 
Validation - loss=3.9321e-01 ppl=1.48 best_loss=3.8632e-01 best_ppl=1.47                                                
Epoch 100 - |param|=6.93e+02 |g_param|=1.81e+04 loss=2.1027e-01 ppl=1.23                                                
Validation - loss=4.0385e-01 ppl=1.50 best_loss=3.8632e-01 best_ppl=1.47                                                
Epoch 101 - |param|=6.93e+02 |g_param|=2.08e+04 loss=2.0853e-01 ppl=1.23                                                
Validation - loss=3.8209e-01 ppl=1.47 best_loss=3.8632e-01 best_ppl=1.47                                                
Epoch 102 - |param|=6.94e+02 |g_param|=1.99e+04 loss=1.9994e-01 ppl=1.22                                                
Validation - loss=3.9096e-01 ppl=1.48 best_loss=3.8209e-01 best_ppl=1.47                                                
Epoch 103 - |param|=6.94e+02 |g_param|=1.74e+04 loss=2.0063e-01 ppl=1.22                                                
Validation - loss=4.1309e-01 ppl=1.51 best_loss=3.8209e-01 best_ppl=1.47                                                
Epoch 104 - |param|=6.94e+02 |g_param|=1.87e+04 loss=2.0810e-01 ppl=1.23                                                
Validation - loss=3.7893e-01 ppl=1.46 best_loss=3.8209e-01 best_ppl=1.47                                                
Epoch 105 - |param|=6.95e+02 |g_param|=1.81e+04 loss=1.9233e-01 ppl=1.21                                                
Validation - loss=3.9911e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 106 - |param|=6.95e+02 |g_param|=2.01e+04 loss=1.8109e-01 ppl=1.20                                                
Validation - loss=3.9693e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 107 - |param|=6.95e+02 |g_param|=2.06e+04 loss=1.9934e-01 ppl=1.22                                                
Validation - loss=3.9913e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 108 - |param|=6.96e+02 |g_param|=2.12e+04 loss=1.9971e-01 ppl=1.22                                                
Validation - loss=4.2567e-01 ppl=1.53 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 109 - |param|=6.96e+02 |g_param|=1.87e+04 loss=2.1356e-01 ppl=1.24                                                
Validation - loss=4.0456e-01 ppl=1.50 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 110 - |param|=6.96e+02 |g_param|=1.12e+04 loss=1.9198e-01 ppl=1.21                                                
Validation - loss=4.1562e-01 ppl=1.52 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 111 - |param|=6.97e+02 |g_param|=9.96e+03 loss=1.7846e-01 ppl=1.20                                                
Validation - loss=4.2273e-01 ppl=1.53 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 112 - |param|=6.97e+02 |g_param|=1.03e+04 loss=1.8882e-01 ppl=1.21                                                
Validation - loss=4.0582e-01 ppl=1.50 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 113 - |param|=6.98e+02 |g_param|=8.27e+03 loss=1.8252e-01 ppl=1.20                                                
Validation - loss=4.0088e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 114 - |param|=6.98e+02 |g_param|=7.43e+03 loss=1.6762e-01 ppl=1.18                                                
Validation - loss=3.9606e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 115 - |param|=6.98e+02 |g_param|=8.52e+03 loss=1.7557e-01 ppl=1.19                                                
Validation - loss=4.0388e-01 ppl=1.50 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 116 - |param|=6.98e+02 |g_param|=8.14e+03 loss=1.7168e-01 ppl=1.19                                                
Validation - loss=3.9798e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 117 - |param|=6.99e+02 |g_param|=8.17e+03 loss=1.7055e-01 ppl=1.19                                                
Validation - loss=4.1251e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 118 - |param|=6.99e+02 |g_param|=9.44e+03 loss=1.7575e-01 ppl=1.19                                                
Validation - loss=4.1438e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 119 - |param|=6.99e+02 |g_param|=1.00e+04 loss=1.7468e-01 ppl=1.19                                                
Validation - loss=4.0385e-01 ppl=1.50 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 120 - |param|=7.00e+02 |g_param|=1.02e+04 loss=1.6919e-01 ppl=1.18                                                
Validation - loss=3.9541e-01 ppl=1.48 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 121 - |param|=7.00e+02 |g_param|=9.32e+03 loss=1.7063e-01 ppl=1.19                                                
Validation - loss=4.1289e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 122 - |param|=7.00e+02 |g_param|=7.14e+03 loss=1.5850e-01 ppl=1.17                                                
Validation - loss=3.9393e-01 ppl=1.48 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 123 - |param|=7.01e+02 |g_param|=7.68e+03 loss=1.6061e-01 ppl=1.17                                                
Validation - loss=3.8975e-01 ppl=1.48 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 124 - |param|=7.01e+02 |g_param|=8.71e+03 loss=1.5591e-01 ppl=1.17                                                
Validation - loss=3.8480e-01 ppl=1.47 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 125 - |param|=7.01e+02 |g_param|=8.16e+03 loss=1.5509e-01 ppl=1.17                                                
Validation - loss=3.9753e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 126 - |param|=7.02e+02 |g_param|=1.70e+04 loss=1.5732e-01 ppl=1.17                                                
Validation - loss=4.0122e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 127 - |param|=7.02e+02 |g_param|=1.91e+04 loss=1.5460e-01 ppl=1.17                                                
Validation - loss=4.1035e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 128 - |param|=7.02e+02 |g_param|=2.15e+04 loss=1.6673e-01 ppl=1.18                                                
Validation - loss=4.1295e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 129 - |param|=7.03e+02 |g_param|=1.85e+04 loss=1.5875e-01 ppl=1.17                                                
Validation - loss=4.0694e-01 ppl=1.50 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 130 - |param|=7.03e+02 |g_param|=1.69e+04 loss=1.5212e-01 ppl=1.16                                                
Validation - loss=4.0895e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 131 - |param|=7.03e+02 |g_param|=1.79e+04 loss=1.5442e-01 ppl=1.17                                                
Validation - loss=3.9539e-01 ppl=1.48 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 132 - |param|=7.04e+02 |g_param|=2.09e+04 loss=1.5151e-01 ppl=1.16                                                
Validation - loss=4.1507e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 133 - |param|=7.04e+02 |g_param|=2.06e+04 loss=1.5547e-01 ppl=1.17                                                
Validation - loss=3.9915e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 134 - |param|=7.04e+02 |g_param|=2.04e+04 loss=1.5022e-01 ppl=1.16                                                
Validation - loss=3.9952e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 135 - |param|=7.05e+02 |g_param|=1.64e+04 loss=1.4586e-01 ppl=1.16                                                
Validation - loss=3.9580e-01 ppl=1.49 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 136 - |param|=7.05e+02 |g_param|=1.45e+04 loss=1.3797e-01 ppl=1.15                                                
Validation - loss=4.1291e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 137 - |param|=7.05e+02 |g_param|=1.77e+04 loss=1.4254e-01 ppl=1.15                                                
Validation - loss=4.1032e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                
Epoch 138 - |param|=7.06e+02 |g_param|=2.16e+04 loss=1.5762e-01 ppl=1.17                                                
Validation - loss=4.0881e-01 ppl=1.51 best_loss=3.7893e-01 best_ppl=1.46                                                

real	10m51.696s
user	10m43.149s
sys	0m8.712s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation results ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.100.0.21-1.23.0.40-1.50.pth
BLEU = 75.04, 87.9/78.6/71.1/64.6 (BP=1.000, ratio=1.030, hyp_len=23852, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.101.0.21-1.23.0.38-1.47.pth
BLEU = 75.12, 87.8/78.7/71.2/64.8 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.102.0.20-1.22.0.39-1.48.pth
BLEU = 74.89, 87.5/78.4/71.0/64.6 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.103.0.20-1.22.0.41-1.51.pth
BLEU = 75.38, 88.0/79.0/71.5/65.0 (BP=1.000, ratio=1.027, hyp_len=23782, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.104.0.21-1.23.0.38-1.46.pth
BLEU = 74.40, 87.5/78.2/70.3/63.7 (BP=1.000, ratio=1.033, hyp_len=23920, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.105.0.19-1.21.0.40-1.49.pth
BLEU = 75.08, 87.8/78.7/71.1/64.6 (BP=1.000, ratio=1.033, hyp_len=23925, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.106.0.18-1.20.0.40-1.49.pth
BLEU = 75.03, 87.6/78.6/71.1/64.7 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.107.0.20-1.22.0.40-1.49.pth
BLEU = 75.28, 87.9/78.8/71.4/64.9 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.108.0.20-1.22.0.43-1.53.pth
BLEU = 73.69, 87.2/77.6/69.6/62.6 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.109.0.21-1.24.0.40-1.50.pth
BLEU = 75.59, 88.2/79.2/71.7/65.2 (BP=1.000, ratio=1.027, hyp_len=23782, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.110.0.19-1.21.0.42-1.52.pth
BLEU = 73.58, 87.1/77.5/69.5/62.5 (BP=1.000, ratio=1.039, hyp_len=24054, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.111.0.18-1.20.0.42-1.53.pth
BLEU = 74.16, 87.2/77.9/70.1/63.4 (BP=1.000, ratio=1.037, hyp_len=24014, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.112.0.19-1.21.0.41-1.50.pth
BLEU = 75.03, 87.9/78.7/71.0/64.5 (BP=1.000, ratio=1.030, hyp_len=23865, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.113.0.18-1.20.0.40-1.49.pth
BLEU = 75.26, 87.9/78.9/71.4/64.8 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.114.0.17-1.18.0.40-1.49.pth
BLEU = 74.60, 87.6/78.3/70.6/63.9 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.115.0.18-1.19.0.40-1.50.pth
BLEU = 74.83, 87.8/78.6/70.8/64.2 (BP=1.000, ratio=1.033, hyp_len=23913, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.116.0.17-1.19.0.40-1.49.pth
BLEU = 74.47, 87.5/78.2/70.5/63.7 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.117.0.17-1.19.0.41-1.51.pth
BLEU = 74.49, 87.4/78.2/70.5/63.9 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.118.0.18-1.19.0.41-1.51.pth
BLEU = 75.24, 88.2/78.9/71.2/64.7 (BP=1.000, ratio=1.029, hyp_len=23833, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.119.0.17-1.19.0.40-1.50.pth
BLEU = 74.57, 87.6/78.4/70.6/63.8 (BP=1.000, ratio=1.034, hyp_len=23947, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.120.0.17-1.18.0.40-1.48.pth
BLEU = 73.82, 87.0/77.6/69.8/63.0 (BP=1.000, ratio=1.038, hyp_len=24043, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.121.0.17-1.19.0.41-1.51.pth
BLEU = 75.18, 87.8/78.7/71.3/64.9 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.122.0.16-1.17.0.39-1.48.pth
BLEU = 74.85, 87.6/78.5/70.9/64.4 (BP=1.000, ratio=1.033, hyp_len=23923, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.123.0.16-1.17.0.39-1.48.pth
BLEU = 74.84, 87.9/78.5/70.8/64.3 (BP=1.000, ratio=1.033, hyp_len=23924, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.124.0.16-1.17.0.38-1.47.pth
BLEU = 75.39, 88.0/78.9/71.5/65.0 (BP=1.000, ratio=1.032, hyp_len=23894, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.125.0.16-1.17.0.40-1.49.pth
BLEU = 75.18, 87.9/78.8/71.3/64.8 (BP=1.000, ratio=1.031, hyp_len=23878, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.126.0.16-1.17.0.40-1.49.pth
BLEU = 74.81, 87.8/78.6/70.8/64.1 (BP=1.000, ratio=1.034, hyp_len=23955, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.127.0.15-1.17.0.41-1.51.pth
BLEU = 73.98, 87.3/77.8/69.8/63.1 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.128.0.17-1.18.0.41-1.51.pth
BLEU = 74.09, 87.5/77.9/70.0/63.1 (BP=1.000, ratio=1.034, hyp_len=23954, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.129.0.16-1.17.0.41-1.50.pth
BLEU = 75.25, 87.9/78.8/71.4/64.9 (BP=1.000, ratio=1.032, hyp_len=23905, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.130.0.15-1.16.0.41-1.51.pth
BLEU = 74.86, 87.6/78.4/70.9/64.4 (BP=1.000, ratio=1.032, hyp_len=23906, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.131.0.15-1.17.0.40-1.48.pth
BLEU = 73.72, 87.2/77.6/69.6/62.8 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.132.0.15-1.16.0.42-1.51.pth
BLEU = 74.03, 87.3/77.8/70.0/63.1 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.133.0.16-1.17.0.40-1.49.pth
BLEU = 74.21, 87.3/78.0/70.2/63.5 (BP=1.000, ratio=1.036, hyp_len=23988, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.134.0.15-1.16.0.40-1.49.pth
BLEU = 73.92, 87.2/77.7/69.9/63.1 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.135.0.15-1.16.0.40-1.49.pth
BLEU = 73.84, 87.1/77.6/69.8/63.1 (BP=1.000, ratio=1.038, hyp_len=24039, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.136.0.14-1.15.0.41-1.51.pth
BLEU = 74.60, 87.4/78.1/70.7/64.2 (BP=1.000, ratio=1.035, hyp_len=23976, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.137.0.14-1.15.0.41-1.51.pth
BLEU = 75.30, 88.0/78.8/71.4/65.0 (BP=1.000, ratio=1.028, hyp_len=23818, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.138.0.16-1.17.0.41-1.51.pth
BLEU = 74.41, 87.4/78.1/70.4/63.8 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.23-1.26.0.39-1.47.pth
BLEU = 74.77, 87.7/78.5/70.8/64.2 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.21-1.24.0.39-1.47.pth
BLEU = 75.17, 87.7/78.8/71.3/64.8 (BP=1.000, ratio=1.031, hyp_len=23886, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.22-1.25.0.40-1.49.pth
BLEU = 75.37, 88.0/78.9/71.4/65.0 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.22-1.25.0.40-1.50.pth
BLEU = 74.68, 87.8/78.4/70.6/64.0 (BP=1.000, ratio=1.030, hyp_len=23851, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.22-1.25.0.40-1.49.pth
BLEU = 75.02, 88.0/78.7/71.0/64.4 (BP=1.000, ratio=1.029, hyp_len=23828, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.21-1.23.0.40-1.49.pth
BLEU = 74.65, 87.6/78.3/70.7/64.0 (BP=1.000, ratio=1.031, hyp_len=23878, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.21-1.24.0.40-1.49.pth
BLEU = 75.13, 87.8/78.7/71.2/64.7 (BP=1.000, ratio=1.029, hyp_len=23829, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.21-1.23.0.39-1.48.pth
BLEU = 74.49, 87.5/78.3/70.5/63.7 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.22-1.24.0.39-1.47.pth
BLEU = 74.06, 87.2/77.9/70.0/63.2 (BP=1.000, ratio=1.035, hyp_len=23980, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.21-1.23.0.39-1.47.pth
BLEU = 74.23, 87.5/78.0/70.1/63.5 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.22-1.24.0.39-1.48.pth
BLEU = 74.74, 87.7/78.4/70.8/64.1 (BP=1.000, ratio=1.031, hyp_len=23881, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.21-1.24.0.39-1.48.pth
BLEU = 74.98, 87.8/78.7/71.1/64.4 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)

real	17m9.337s
user	16m44.585s
sys	0m57.669s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch$
```

4e+8 မော်ဒယ်အတွက် Best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: seq-rl-model-myrk.109.0.21-1.24.0.40-1.50.pth
BLEU = 75.59, 88.2/79.2/71.7/65.2 (BP=1.000, ratio=1.027, hyp_len=23782, ref_len=23160)
```

## Make Validation Data Bigger Size

Preparing a new training data:  

```
(base) ye@:~/exp/simple-nmt/data/original$ head -n 12561 ./train-dev.my > ../train.my
(base) ye@:~/exp/simple-nmt/data/original$ head -n 12561 ./train-dev.rk > ../train.rk
```

Preparing a new validation or development data:  

```
(base) ye@:~/exp/simple-nmt/data/original$ tail -n 3000 ./train-dev.my > ../dev.my
(base) ye@:~/exp/simple-nmt/data/original$ tail -n 3000 ./train-dev.rk > ../dev.rk
```

And thus, new training, validation and test data size will become as follows:  

```
(base) ye@:~/exp/simple-nmt/data$ wc *.my
   3000   38854  365611 dev.my
   1811   23509  219399 test.my
  12561  172592 1620497 train.my
  17372  234955 2205507 total
(base) ye@:~/exp/simple-nmt/data$ wc *.rk
   3000   38351  359940 dev.rk
   1811   23160  215711 test.rk
  12561  170165 1597960 train.rk
  17372  231676 2173611 total
```

Preparing a new training data:  

```
(base) ye@:~/exp/simple-nmt/data/original$ head -n 12561 ./train-dev.my > ../train.my
(base) ye@:~/exp/simple-nmt/data/original$ head -n 12561 ./train-dev.rk > ../train.rk
```

Preparing a new validation or development data:  

```
(base) ye@:~/exp/simple-nmt/data/original$ tail -n 3000 ./train-dev.my > ../dev.my
(base) ye@:~/exp/simple-nmt/data/original$ tail -n 3000 ./train-dev.rk > ../dev.rk
```

And thus, new training, validation and test data size will become as follows:  

```
(base) ye@:~/exp/simple-nmt/data$ wc *.my
   3000   38854  365611 dev.my
   1811   23509  219399 test.my
  12561  172592 1620497 train.my
  17372  234955 2205507 total
(base) ye@:~/exp/simple-nmt/data$ wc *.rk
   3000   38351  359940 dev.rk
   1811   23160  215711 test.rk
  12561  170165 1597960 train.rk
  17372  231676 2173611 total
```

## Training seq2seq baseline

### for my-rk

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.pth
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
Epoch 1 - |param|=6.41e+02 |g_param|=1.94e+05 loss=4.4329e+00 ppl=84.17                                                 
Validation - loss=4.0728e+00 ppl=58.72 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.41e+02 |g_param|=1.73e+05 loss=4.1307e+00 ppl=62.22                                                 
Validation - loss=3.8704e+00 ppl=47.96 best_loss=4.0728e+00 best_ppl=58.72                                              
Epoch 3 - |param|=6.42e+02 |g_param|=1.90e+05 loss=4.0060e+00 ppl=54.93                                                 
Validation - loss=3.8128e+00 ppl=45.28 best_loss=3.8704e+00 best_ppl=47.96                                              
Epoch 4 - |param|=6.42e+02 |g_param|=1.76e+05 loss=3.9399e+00 ppl=51.42                                                 
Validation - loss=3.6524e+00 ppl=38.57 best_loss=3.8128e+00 best_ppl=45.28                                              
Epoch 5 - |param|=6.42e+02 |g_param|=1.71e+05 loss=3.7517e+00 ppl=42.60                                                 
Validation - loss=3.5462e+00 ppl=34.68 best_loss=3.6524e+00 best_ppl=38.57                                              
Epoch 6 - |param|=6.43e+02 |g_param|=1.72e+05 loss=3.7079e+00 ppl=40.77                                                 
Validation - loss=3.4331e+00 ppl=30.97 best_loss=3.5462e+00 best_ppl=34.68                                              
Epoch 7 - |param|=6.43e+02 |g_param|=1.84e+05 loss=3.5528e+00 ppl=34.91                                                 
Validation - loss=3.2368e+00 ppl=25.45 best_loss=3.4331e+00 best_ppl=30.97                                              
Epoch 8 - |param|=6.44e+02 |g_param|=2.02e+05 loss=3.3070e+00 ppl=27.30                                                 
Validation - loss=3.0341e+00 ppl=20.78 best_loss=3.2368e+00 best_ppl=25.45                                              
Epoch 9 - |param|=6.45e+02 |g_param|=2.09e+05 loss=3.0124e+00 ppl=20.34                                                 
Validation - loss=2.7754e+00 ppl=16.05 best_loss=3.0341e+00 best_ppl=20.78                                              
Epoch 10 - |param|=6.46e+02 |g_param|=1.81e+05 loss=2.7655e+00 ppl=15.89                                                
Validation - loss=2.6106e+00 ppl=13.61 best_loss=2.7754e+00 best_ppl=16.05                                              
Epoch 11 - |param|=6.46e+02 |g_param|=1.85e+05 loss=2.4927e+00 ppl=12.09                                                
Validation - loss=2.4172e+00 ppl=11.21 best_loss=2.6106e+00 best_ppl=13.61                                              
Epoch 12 - |param|=6.47e+02 |g_param|=2.75e+05 loss=2.4314e+00 ppl=11.37                                                
Validation - loss=2.3029e+00 ppl=10.00 best_loss=2.4172e+00 best_ppl=11.21                                              
Epoch 13 - |param|=6.48e+02 |g_param|=2.37e+05 loss=2.1584e+00 ppl=8.66                                                 
Validation - loss=2.0653e+00 ppl=7.89 best_loss=2.3029e+00 best_ppl=10.00                                               
Epoch 14 - |param|=6.48e+02 |g_param|=2.29e+05 loss=1.9483e+00 ppl=7.02                                                 
Validation - loss=1.8847e+00 ppl=6.58 best_loss=2.0653e+00 best_ppl=7.89                                                
Epoch 15 - |param|=6.49e+02 |g_param|=1.84e+05 loss=1.7231e+00 ppl=5.60                                                 
Validation - loss=1.6856e+00 ppl=5.40 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 16 - |param|=6.50e+02 |g_param|=2.29e+05 loss=1.5826e+00 ppl=4.87                                                 
Validation - loss=1.5559e+00 ppl=4.74 best_loss=1.6856e+00 best_ppl=5.40                                                
Epoch 17 - |param|=6.50e+02 |g_param|=1.68e+05 loss=1.4928e+00 ppl=4.45                                                 
Validation - loss=1.5546e+00 ppl=4.73 best_loss=1.5559e+00 best_ppl=4.74                                                
Epoch 18 - |param|=6.51e+02 |g_param|=8.75e+04 loss=1.3055e+00 ppl=3.69                                                 
Validation - loss=1.3580e+00 ppl=3.89 best_loss=1.5546e+00 best_ppl=4.73                                                
Epoch 19 - |param|=6.51e+02 |g_param|=7.87e+04 loss=1.1579e+00 ppl=3.18                                                 
Validation - loss=1.2676e+00 ppl=3.55 best_loss=1.3580e+00 best_ppl=3.89                                                
Epoch 20 - |param|=6.52e+02 |g_param|=7.71e+04 loss=1.1086e+00 ppl=3.03                                                 
Validation - loss=1.2878e+00 ppl=3.62 best_loss=1.2676e+00 best_ppl=3.55                                                
Epoch 21 - |param|=6.52e+02 |g_param|=5.93e+04 loss=1.0764e+00 ppl=2.93                                                 
Validation - loss=1.1479e+00 ppl=3.15 best_loss=1.2676e+00 best_ppl=3.55                                                
Epoch 22 - |param|=6.53e+02 |g_param|=4.77e+04 loss=9.6700e-01 ppl=2.63                                                 
Validation - loss=1.1094e+00 ppl=3.03 best_loss=1.1479e+00 best_ppl=3.15                                                
Epoch 23 - |param|=6.53e+02 |g_param|=4.45e+04 loss=9.3488e-01 ppl=2.55                                                 
Validation - loss=1.0832e+00 ppl=2.95 best_loss=1.1094e+00 best_ppl=3.03                                                
Epoch 24 - |param|=6.54e+02 |g_param|=5.26e+04 loss=9.0523e-01 ppl=2.47                                                 
Validation - loss=1.0313e+00 ppl=2.80 best_loss=1.0832e+00 best_ppl=2.95                                                
Epoch 25 - |param|=6.54e+02 |g_param|=3.30e+04 loss=8.1084e-01 ppl=2.25                                                 
Validation - loss=1.0105e+00 ppl=2.75 best_loss=1.0313e+00 best_ppl=2.80                                                
Epoch 26 - |param|=6.55e+02 |g_param|=6.34e+04 loss=8.5620e-01 ppl=2.35                                                 
Validation - loss=9.8318e-01 ppl=2.67 best_loss=1.0105e+00 best_ppl=2.75                                                
Epoch 27 - |param|=6.55e+02 |g_param|=3.61e+04 loss=7.5890e-01 ppl=2.14                                                 
Validation - loss=9.4325e-01 ppl=2.57 best_loss=9.8318e-01 best_ppl=2.67                                                
Epoch 28 - |param|=6.55e+02 |g_param|=3.21e+04 loss=7.0359e-01 ppl=2.02                                                 
Validation - loss=9.1837e-01 ppl=2.51 best_loss=9.4325e-01 best_ppl=2.57                                                
Epoch 29 - |param|=6.56e+02 |g_param|=3.53e+04 loss=7.1951e-01 ppl=2.05                                                 
Validation - loss=8.9862e-01 ppl=2.46 best_loss=9.1837e-01 best_ppl=2.51                                                
Epoch 30 - |param|=6.56e+02 |g_param|=3.62e+04 loss=6.4107e-01 ppl=1.90                                                 
Validation - loss=8.7761e-01 ppl=2.41 best_loss=8.9862e-01 best_ppl=2.46
```

testing/evaluation on baseline model...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/myrk-100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-myrk.01.4.43-84.17.4.07-58.72.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 10.8/0.0/0.0/0.0 (BP=1.000, ratio=1.070, hyp_len=24788, ref_len=23160)
Evaluation result for the model: seq-model-myrk.02.4.13-62.22.3.87-47.96.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.0/2.0/0.0/0.0 (BP=1.000, ratio=1.011, hyp_len=23411, ref_len=23160)
Evaluation result for the model: seq-model-myrk.03.4.01-54.93.3.81-45.28.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.5/2.0/0.0/0.0 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)
Evaluation result for the model: seq-model-myrk.04.3.94-51.42.3.65-38.57.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/2.8/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23227, ref_len=23160)
Evaluation result for the model: seq-model-myrk.05.3.75-42.60.3.55-34.68.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.6/3.2/0.0/0.0 (BP=1.000, ratio=1.024, hyp_len=23726, ref_len=23160)
Evaluation result for the model: seq-model-myrk.06.3.71-40.77.3.43-30.97.pth
BLEU = 0.84, 26.0/5.2/0.7/0.0 (BP=1.000, ratio=1.005, hyp_len=23285, ref_len=23160)
Evaluation result for the model: seq-model-myrk.07.3.55-34.91.3.24-25.45.pth
BLEU = 2.40, 30.4/7.5/1.5/0.1 (BP=0.996, ratio=0.996, hyp_len=23072, ref_len=23160)
Evaluation result for the model: seq-model-myrk.08.3.31-27.30.3.03-20.78.pth
BLEU = 5.04, 34.3/10.7/2.9/0.6 (BP=1.000, ratio=1.013, hyp_len=23453, ref_len=23160)
Evaluation result for the model: seq-model-myrk.09.3.01-20.34.2.78-16.05.pth
BLEU = 8.26, 39.1/14.7/5.1/1.6 (BP=1.000, ratio=1.008, hyp_len=23335, ref_len=23160)
Evaluation result for the model: seq-model-myrk.10.2.77-15.89.2.61-13.61.pth
BLEU = 10.53, 42.1/17.4/6.7/2.5 (BP=1.000, ratio=1.019, hyp_len=23609, ref_len=23160)
Evaluation result for the model: seq-model-myrk.11.2.49-12.09.2.42-11.21.pth
BLEU = 14.13, 46.3/21.6/9.6/4.1 (BP=1.000, ratio=1.025, hyp_len=23729, ref_len=23160)
Evaluation result for the model: seq-model-myrk.12.2.43-11.37.2.30-10.00.pth
BLEU = 16.05, 49.1/24.3/11.2/5.0 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: seq-model-myrk.13.2.16-8.66.2.07-7.89.pth
BLEU = 22.27, 55.6/31.1/16.8/8.6 (BP=0.996, ratio=0.996, hyp_len=23070, ref_len=23160)
Evaluation result for the model: seq-model-myrk.14.1.95-7.02.1.88-6.58.pth
BLEU = 27.40, 59.1/36.2/21.3/12.4 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: seq-model-myrk.15.1.72-5.60.1.69-5.40.pth
BLEU = 34.18, 64.5/42.6/27.8/17.9 (BP=1.000, ratio=1.003, hyp_len=23218, ref_len=23160)
Evaluation result for the model: seq-model-myrk.16.1.58-4.87.1.56-4.74.pth
BLEU = 39.14, 68.2/47.3/32.6/22.3 (BP=1.000, ratio=1.009, hyp_len=23380, ref_len=23160)
Evaluation result for the model: seq-model-myrk.17.1.49-4.45.1.55-4.73.pth
BLEU = 41.67, 70.3/49.9/35.3/25.0 (BP=0.993, ratio=0.993, hyp_len=22999, ref_len=23160)
Evaluation result for the model: seq-model-myrk.18.1.31-3.69.1.36-3.89.pth
BLEU = 48.91, 74.6/56.2/42.5/32.2 (BP=0.999, ratio=0.999, hyp_len=23139, ref_len=23160)
Evaluation result for the model: seq-model-myrk.19.1.16-3.18.1.27-3.55.pth
BLEU = 51.75, 76.2/58.8/45.5/35.2 (BP=1.000, ratio=1.006, hyp_len=23301, ref_len=23160)
Evaluation result for the model: seq-model-myrk.20.1.11-3.03.1.29-3.62.pth
BLEU = 50.61, 75.4/58.0/44.3/33.9 (BP=1.000, ratio=1.019, hyp_len=23592, ref_len=23160)
Evaluation result for the model: seq-model-myrk.21.1.08-2.93.1.15-3.15.pth
BLEU = 56.93, 79.3/63.4/50.9/41.0 (BP=1.000, ratio=1.005, hyp_len=23275, ref_len=23160)
Evaluation result for the model: seq-model-myrk.22.0.97-2.63.1.11-3.03.pth
BLEU = 57.82, 79.6/64.2/51.9/42.1 (BP=1.000, ratio=1.015, hyp_len=23498, ref_len=23160)
Evaluation result for the model: seq-model-myrk.23.0.93-2.55.1.08-2.95.pth
BLEU = 59.94, 80.7/66.0/54.2/44.7 (BP=1.000, ratio=1.016, hyp_len=23523, ref_len=23160)
Evaluation result for the model: seq-model-myrk.24.0.91-2.47.1.03-2.80.pth
BLEU = 61.39, 81.5/67.2/55.8/46.6 (BP=1.000, ratio=1.015, hyp_len=23503, ref_len=23160)
Evaluation result for the model: seq-model-myrk.25.0.81-2.25.1.01-2.75.pth
BLEU = 63.60, 82.7/69.2/58.2/49.1 (BP=1.000, ratio=1.009, hyp_len=23366, ref_len=23160)
Evaluation result for the model: seq-model-myrk.26.0.86-2.35.0.98-2.67.pth
BLEU = 63.76, 82.9/69.4/58.3/49.2 (BP=1.000, ratio=1.010, hyp_len=23397, ref_len=23160)
Evaluation result for the model: seq-model-myrk.27.0.76-2.14.0.94-2.57.pth
BLEU = 65.32, 83.6/70.7/60.1/51.3 (BP=1.000, ratio=1.015, hyp_len=23513, ref_len=23160)
Evaluation result for the model: seq-model-myrk.28.0.70-2.02.0.92-2.51.pth
BLEU = 67.50, 84.9/72.6/62.5/54.0 (BP=1.000, ratio=1.011, hyp_len=23420, ref_len=23160)
Evaluation result for the model: seq-model-myrk.29.0.72-2.05.0.90-2.46.pth
BLEU = 66.97, 84.3/72.1/62.0/53.4 (BP=1.000, ratio=1.019, hyp_len=23591, ref_len=23160)
Evaluation result for the model: seq-model-myrk.30.0.64-1.90.0.88-2.41.pth
BLEU = 68.10, 84.7/72.9/63.2/55.1 (BP=1.000, ratio=1.016, hyp_len=23538, ref_len=23160)

real	9m33.712s
user	9m19.477s
sys	0m33.687s
```

Baseline model best score: BLEU = 68.10

### for rk-my

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.pth
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
    'n_epochs': 30,
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
Epoch 1 - |param|=6.41e+02 |g_param|=2.01e+05 loss=4.3979e+00 ppl=81.28                                                 
Validation - loss=4.0482e+00 ppl=57.29 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.41e+02 |g_param|=1.83e+05 loss=4.1819e+00 ppl=65.49                                                 
Validation - loss=3.9125e+00 ppl=50.02 best_loss=4.0482e+00 best_ppl=57.29                                              
Epoch 3 - |param|=6.41e+02 |g_param|=1.83e+05 loss=4.0673e+00 ppl=58.40                                                 
Validation - loss=3.8112e+00 ppl=45.21 best_loss=3.9125e+00 best_ppl=50.02                                              
Epoch 4 - |param|=6.42e+02 |g_param|=1.94e+05 loss=3.9407e+00 ppl=51.46                                                 
Validation - loss=3.7281e+00 ppl=41.60 best_loss=3.8112e+00 best_ppl=45.21                                              
Epoch 5 - |param|=6.42e+02 |g_param|=1.84e+05 loss=3.8664e+00 ppl=47.77                                                 
Validation - loss=3.6545e+00 ppl=38.65 best_loss=3.7281e+00 best_ppl=41.60                                              
Epoch 6 - |param|=6.42e+02 |g_param|=2.04e+05 loss=3.8766e+00 ppl=48.26                                                 
Validation - loss=3.6024e+00 ppl=36.69 best_loss=3.6545e+00 best_ppl=38.65                                              
Epoch 7 - |param|=6.43e+02 |g_param|=1.94e+05 loss=3.6958e+00 ppl=40.28                                                 
Validation - loss=3.5163e+00 ppl=33.66 best_loss=3.6024e+00 best_ppl=36.69                                              
Epoch 8 - |param|=6.43e+02 |g_param|=1.01e+05 loss=3.6633e+00 ppl=38.99                                                 
Validation - loss=3.4234e+00 ppl=30.67 best_loss=3.5163e+00 best_ppl=33.66                                              
Epoch 9 - |param|=6.44e+02 |g_param|=1.07e+05 loss=3.4660e+00 ppl=32.01                                                 
Validation - loss=3.2351e+00 ppl=25.41 best_loss=3.4234e+00 best_ppl=30.67                                              
Epoch 10 - |param|=6.44e+02 |g_param|=9.72e+04 loss=3.2258e+00 ppl=25.17                                                
Validation - loss=3.0688e+00 ppl=21.52 best_loss=3.2351e+00 best_ppl=25.41                                              
Epoch 11 - |param|=6.45e+02 |g_param|=1.10e+05 loss=3.1120e+00 ppl=22.47                                                
Validation - loss=2.9047e+00 ppl=18.26 best_loss=3.0688e+00 best_ppl=21.52                                              
Epoch 12 - |param|=6.46e+02 |g_param|=9.07e+04 loss=2.9708e+00 ppl=19.51                                                
Validation - loss=2.7381e+00 ppl=15.46 best_loss=2.9047e+00 best_ppl=18.26                                              
Epoch 13 - |param|=6.46e+02 |g_param|=8.18e+04 loss=2.7355e+00 ppl=15.42                                                
Validation - loss=2.5045e+00 ppl=12.24 best_loss=2.7381e+00 best_ppl=15.46                                              
Epoch 14 - |param|=6.47e+02 |g_param|=9.95e+04 loss=2.5747e+00 ppl=13.13                                                
Validation - loss=2.3648e+00 ppl=10.64 best_loss=2.5045e+00 best_ppl=12.24                                              
Epoch 15 - |param|=6.48e+02 |g_param|=9.01e+04 loss=2.4008e+00 ppl=11.03                                                
Validation - loss=2.2041e+00 ppl=9.06 best_loss=2.3648e+00 best_ppl=10.64                                               
Epoch 16 - |param|=6.48e+02 |g_param|=8.67e+04 loss=2.1681e+00 ppl=8.74                                                 
Validation - loss=2.0721e+00 ppl=7.94 best_loss=2.2041e+00 best_ppl=9.06                                                
Epoch 17 - |param|=6.49e+02 |g_param|=7.49e+04 loss=2.0399e+00 ppl=7.69                                                 
Validation - loss=1.9167e+00 ppl=6.80 best_loss=2.0721e+00 best_ppl=7.94                                                
Epoch 18 - |param|=6.49e+02 |g_param|=4.79e+04 loss=1.8771e+00 ppl=6.53                                                 
Validation - loss=1.8088e+00 ppl=6.10 best_loss=1.9167e+00 best_ppl=6.80                                                
Epoch 19 - |param|=6.50e+02 |g_param|=6.18e+04 loss=1.7668e+00 ppl=5.85                                                 
Validation - loss=1.7496e+00 ppl=5.75 best_loss=1.8088e+00 best_ppl=6.10                                                
Epoch 20 - |param|=6.51e+02 |g_param|=5.36e+04 loss=1.6578e+00 ppl=5.25                                                 
Validation - loss=1.6221e+00 ppl=5.06 best_loss=1.7496e+00 best_ppl=5.75                                                
Epoch 21 - |param|=6.51e+02 |g_param|=5.70e+04 loss=1.5772e+00 ppl=4.84                                                 
Validation - loss=1.5312e+00 ppl=4.62 best_loss=1.6221e+00 best_ppl=5.06                                                
Epoch 22 - |param|=6.52e+02 |g_param|=5.98e+04 loss=1.4846e+00 ppl=4.41                                                 
Validation - loss=1.4459e+00 ppl=4.25 best_loss=1.5312e+00 best_ppl=4.62                                                
Epoch 23 - |param|=6.52e+02 |g_param|=4.77e+04 loss=1.3073e+00 ppl=3.70                                                 
Validation - loss=1.3866e+00 ppl=4.00 best_loss=1.4459e+00 best_ppl=4.25                                                
Epoch 24 - |param|=6.53e+02 |g_param|=3.97e+04 loss=1.2168e+00 ppl=3.38                                                 
Validation - loss=1.2947e+00 ppl=3.65 best_loss=1.3866e+00 best_ppl=4.00                                                
Epoch 25 - |param|=6.53e+02 |g_param|=6.86e+04 loss=1.2231e+00 ppl=3.40                                                 
Validation - loss=1.2840e+00 ppl=3.61 best_loss=1.2947e+00 best_ppl=3.65                                                
Epoch 26 - |param|=6.54e+02 |g_param|=6.84e+04 loss=1.1324e+00 ppl=3.10                                                 
Validation - loss=1.2520e+00 ppl=3.50 best_loss=1.2840e+00 best_ppl=3.61                                                
Epoch 27 - |param|=6.54e+02 |g_param|=5.83e+04 loss=1.0814e+00 ppl=2.95                                                 
Validation - loss=1.1581e+00 ppl=3.18 best_loss=1.2520e+00 best_ppl=3.50                                                
Epoch 28 - |param|=6.55e+02 |g_param|=7.52e+04 loss=1.0701e+00 ppl=2.92                                                 
Validation - loss=1.1809e+00 ppl=3.26 best_loss=1.1581e+00 best_ppl=3.18                                                
Epoch 29 - |param|=6.55e+02 |g_param|=3.48e+04 loss=9.2454e-01 ppl=2.52                                                 
Validation - loss=1.0613e+00 ppl=2.89 best_loss=1.1581e+00 best_ppl=3.18                                                
Epoch 30 - |param|=6.56e+02 |g_param|=3.24e+04 loss=8.6101e-01 ppl=2.37                                                 
Validation - loss=1.0455e+00 ppl=2.84 best_loss=1.0613e+00 best_ppl=2.89                                                

real	5m47.008s
user	5m41.996s
sys	0m5.379s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

rk-my, baseline testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-model-rkmy.01.4.40-81.28.4.05-57.29.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.3/0.4/0.0/0.0 (BP=0.925, ratio=0.927, hyp_len=21802, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.02.4.18-65.49.3.91-50.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.8/1.5/0.0/0.0 (BP=0.993, ratio=0.993, hyp_len=23335, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.03.4.07-58.40.3.81-45.21.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.8/1.7/0.0/0.0 (BP=0.982, ratio=0.982, hyp_len=23085, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.04.3.94-51.46.3.73-41.60.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.9/2.8/0.0/0.0 (BP=0.978, ratio=0.978, hyp_len=22998, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.05.3.87-47.77.3.65-38.65.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.9/3.0/0.2/0.0 (BP=0.980, ratio=0.980, hyp_len=23049, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.06.3.88-48.26.3.60-36.69.pth
BLEU = 0.72, 23.1/4.0/0.5/0.0 (BP=0.995, ratio=0.995, hyp_len=23401, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.07.3.70-40.28.3.52-33.66.pth
BLEU = 0.72, 23.1/4.7/0.5/0.0 (BP=0.991, ratio=0.991, hyp_len=23299, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.08.3.66-38.99.3.42-30.67.pth
BLEU = 1.81, 26.1/6.4/1.2/0.1 (BP=0.987, ratio=0.987, hyp_len=23208, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.09.3.47-32.01.3.24-25.41.pth
BLEU = 2.24, 28.5/8.0/1.4/0.1 (BP=0.989, ratio=0.989, hyp_len=23259, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.10.3.23-25.17.3.07-21.52.pth
BLEU = 3.23, 31.6/9.1/1.9/0.2 (BP=0.974, ratio=0.974, hyp_len=22902, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.11.3.11-22.47.2.90-18.26.pth
BLEU = 5.17, 34.1/11.3/2.9/0.6 (BP=1.000, ratio=1.002, hyp_len=23567, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.12.2.97-19.51.2.74-15.46.pth
BLEU = 7.42, 36.8/14.4/4.5/1.3 (BP=1.000, ratio=1.030, hyp_len=24204, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.13.2.74-15.42.2.50-12.24.pth
BLEU = 11.00, 42.2/18.6/7.1/2.6 (BP=1.000, ratio=1.007, hyp_len=23684, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.14.2.57-13.13.2.36-10.64.pth
BLEU = 12.32, 44.6/20.4/8.1/3.1 (BP=1.000, ratio=1.013, hyp_len=23812, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.15.2.40-11.03.2.20-9.06.pth
BLEU = 16.11, 48.1/24.3/11.3/5.1 (BP=1.000, ratio=1.013, hyp_len=23813, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.16.2.17-8.74.2.07-7.94.pth
BLEU = 19.22, 51.5/27.8/13.9/6.9 (BP=1.000, ratio=1.014, hyp_len=23828, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.17.2.04-7.69.1.92-6.80.pth
BLEU = 23.64, 55.9/32.2/17.9/9.7 (BP=1.000, ratio=1.001, hyp_len=23530, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.18.1.88-6.53.1.81-6.10.pth
BLEU = 27.44, 58.9/36.0/21.4/12.5 (BP=1.000, ratio=1.006, hyp_len=23644, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.19.1.77-5.85.1.75-5.75.pth
BLEU = 29.45, 61.2/38.3/23.2/13.8 (BP=1.000, ratio=1.001, hyp_len=23525, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.20.1.66-5.25.1.62-5.06.pth
BLEU = 33.46, 63.8/42.1/26.9/17.3 (BP=1.000, ratio=1.007, hyp_len=23662, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.21.1.58-4.84.1.53-4.62.pth
BLEU = 37.48, 66.6/46.0/30.9/20.9 (BP=1.000, ratio=1.014, hyp_len=23845, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.22.1.48-4.41.1.45-4.25.pth
BLEU = 40.71, 68.6/48.8/34.2/24.0 (BP=1.000, ratio=1.013, hyp_len=23818, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.23.1.31-3.70.1.39-4.00.pth
BLEU = 44.56, 71.4/52.4/38.0/27.7 (BP=1.000, ratio=1.005, hyp_len=23620, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.24.1.22-3.38.1.29-3.65.pth
BLEU = 47.51, 73.4/55.3/41.0/30.7 (BP=1.000, ratio=1.014, hyp_len=23830, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.25.1.22-3.40.1.28-3.61.pth
BLEU = 47.63, 73.1/55.2/41.2/31.0 (BP=1.000, ratio=1.017, hyp_len=23916, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.26.1.13-3.10.1.25-3.50.pth
BLEU = 50.65, 75.0/58.2/44.4/34.0 (BP=1.000, ratio=1.031, hyp_len=24239, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.27.1.08-2.95.1.16-3.18.pth
BLEU = 54.32, 77.1/61.3/48.1/38.2 (BP=1.000, ratio=1.023, hyp_len=24045, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.28.1.07-2.92.1.18-3.26.pth
BLEU = 53.32, 76.2/60.3/47.2/37.3 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.29.0.92-2.52.1.06-2.89.pth
BLEU = 58.90, 79.8/65.4/53.0/43.5 (BP=1.000, ratio=1.019, hyp_len=23964, ref_len=23509)
Evaluation result for the model: seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth
BLEU = 59.48, 80.1/65.8/53.6/44.2 (BP=1.000, ratio=1.021, hyp_len=24003, ref_len=23509)

real	9m35.606s
user	9m23.143s
sys	0m33.230s
(simple-nmt) ye@:~/exp/simple-nmt/model/seq2seq/baseline/rkmy-100epoch$
```

rk-my, seq2seq baseline best score:  

```
Evaluation result for the model: seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth
BLEU = 59.48, 80.1/65.8/53.6/44.2 (BP=1.000, ratio=1.021, hyp_len=24003, ref_len=23509)
```


## RL Fine-tuning for seq2seq

### for my-rk

seq-model-myrk.30.0.64-1.90.0.88-2.41.pth ကို အခြေခံပြီး RL fine-tuning လုပ်ကြည့်မယ်...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.30.0.64-1.90.0.88-2.41.pth --model_fn ./model/rl/seq2seq/100epoch/baseline/seq-rl-model-myrk.pth --init_epoch 30 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.30.0.64-1.90.0.88-2.41.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/100epoch/baseline/seq-rl-model-myrk.pth
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'load_fn': './model/seq2seq/baseline/myrk-100epoch/seq-model-myrk.30.0.64-1.90.0.88-2.41.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/100epoch/baseline/seq-rl-model-myrk.pth',
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
Epoch 30 - |param|=6.57e+02 |g_param|=9.28e+04 loss=6.1173e-01 ppl=1.84                                                 
Validation - loss=8.3664e-01 ppl=2.31 best_loss=inf best_ppl=inf                                                        
Epoch 31 - |param|=6.57e+02 |g_param|=3.63e+04 loss=6.1199e-01 ppl=1.84                                                 
Validation - loss=8.2338e-01 ppl=2.28 best_loss=8.3664e-01 best_ppl=2.31                                                
Epoch 32 - |param|=6.57e+02 |g_param|=3.02e+04 loss=5.9156e-01 ppl=1.81                                                 
Validation - loss=8.3017e-01 ppl=2.29 best_loss=8.2338e-01 best_ppl=2.28                                                
Epoch 33 - |param|=6.58e+02 |g_param|=3.09e+04 loss=5.7732e-01 ppl=1.78                                                 
Validation - loss=8.2748e-01 ppl=2.29 best_loss=8.2338e-01 best_ppl=2.28                                                
Epoch 34 - |param|=6.58e+02 |g_param|=4.83e+04 loss=5.8555e-01 ppl=1.80                                                 
Validation - loss=8.0733e-01 ppl=2.24 best_loss=8.2338e-01 best_ppl=2.28                                                
Epoch 35 - |param|=6.58e+02 |g_param|=3.48e+04 loss=5.2953e-01 ppl=1.70                                                 
Validation - loss=8.2131e-01 ppl=2.27 best_loss=8.0733e-01 best_ppl=2.24                                                
Epoch 36 - |param|=6.59e+02 |g_param|=4.95e+04 loss=6.0553e-01 ppl=1.83                                                 
Validation - loss=8.0534e-01 ppl=2.24 best_loss=8.0733e-01 best_ppl=2.24                                                
Epoch 37 - |param|=6.59e+02 |g_param|=3.83e+04 loss=5.3482e-01 ppl=1.71                                                 
Validation - loss=7.9530e-01 ppl=2.22 best_loss=8.0534e-01 best_ppl=2.24                                                
Epoch 38 - |param|=6.60e+02 |g_param|=4.05e+04 loss=5.2285e-01 ppl=1.69                                                 
Validation - loss=7.6449e-01 ppl=2.15 best_loss=7.9530e-01 best_ppl=2.22                                                
Epoch 39 - |param|=6.60e+02 |g_param|=4.62e+04 loss=5.1116e-01 ppl=1.67                                                 
Validation - loss=7.7093e-01 ppl=2.16 best_loss=7.6449e-01 best_ppl=2.15                                                
Epoch 40 - |param|=6.60e+02 |g_param|=3.14e+04 loss=4.8150e-01 ppl=1.62                                                 
Validation - loss=7.5016e-01 ppl=2.12 best_loss=7.6449e-01 best_ppl=2.15                                                
Epoch 41 - |param|=6.61e+02 |g_param|=2.22e+04 loss=4.4327e-01 ppl=1.56                                                 
Validation - loss=7.3288e-01 ppl=2.08 best_loss=7.5016e-01 best_ppl=2.12                                                
Epoch 42 - |param|=6.61e+02 |g_param|=2.69e+04 loss=4.4580e-01 ppl=1.56                                                 
Validation - loss=7.3090e-01 ppl=2.08 best_loss=7.3288e-01 best_ppl=2.08                                                
Epoch 43 - |param|=6.61e+02 |g_param|=2.37e+04 loss=4.4395e-01 ppl=1.56                                                 
Validation - loss=7.2577e-01 ppl=2.07 best_loss=7.3090e-01 best_ppl=2.08                                                
Epoch 44 - |param|=6.62e+02 |g_param|=2.44e+04 loss=4.0175e-01 ppl=1.49                                                 
Validation - loss=7.2423e-01 ppl=2.06 best_loss=7.2577e-01 best_ppl=2.07                                                
Epoch 45 - |param|=6.62e+02 |g_param|=3.15e+04 loss=4.1867e-01 ppl=1.52                                                 
Validation - loss=7.4067e-01 ppl=2.10 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 46 - |param|=6.62e+02 |g_param|=4.81e+04 loss=4.4802e-01 ppl=1.57                                                 
Validation - loss=7.5398e-01 ppl=2.13 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 47 - |param|=6.63e+02 |g_param|=1.94e+04 loss=4.2095e-01 ppl=1.52                                                 
Validation - loss=7.4067e-01 ppl=2.10 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 48 - |param|=6.63e+02 |g_param|=1.35e+04 loss=3.9618e-01 ppl=1.49                                                 
Validation - loss=7.2608e-01 ppl=2.07 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 49 - |param|=6.63e+02 |g_param|=1.64e+04 loss=3.8271e-01 ppl=1.47                                                 
Validation - loss=7.2630e-01 ppl=2.07 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 50 - |param|=6.64e+02 |g_param|=1.39e+04 loss=3.7013e-01 ppl=1.45                                                 
Validation - loss=7.1931e-01 ppl=2.05 best_loss=7.2423e-01 best_ppl=2.06                                                
Epoch 51 - |param|=6.64e+02 |g_param|=1.37e+04 loss=3.7270e-01 ppl=1.45                                                 
Validation - loss=6.9755e-01 ppl=2.01 best_loss=7.1931e-01 best_ppl=2.05                                                
Epoch 52 - |param|=6.64e+02 |g_param|=1.23e+04 loss=3.6787e-01 ppl=1.44                                                 
Validation - loss=6.9079e-01 ppl=2.00 best_loss=6.9755e-01 best_ppl=2.01                                                
Epoch 53 - |param|=6.65e+02 |g_param|=1.05e+04 loss=3.4318e-01 ppl=1.41                                                 
Validation - loss=6.9537e-01 ppl=2.00 best_loss=6.9079e-01 best_ppl=2.00                                                
Epoch 54 - |param|=6.65e+02 |g_param|=1.39e+04 loss=3.4091e-01 ppl=1.41                                                 
Validation - loss=6.8965e-01 ppl=1.99 best_loss=6.9079e-01 best_ppl=2.00                                                
Epoch 55 - |param|=6.65e+02 |g_param|=1.33e+04 loss=3.6054e-01 ppl=1.43                                                 
Validation - loss=7.1215e-01 ppl=2.04 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 56 - |param|=6.65e+02 |g_param|=1.10e+04 loss=3.5344e-01 ppl=1.42                                                 
Validation - loss=7.1230e-01 ppl=2.04 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 57 - |param|=6.66e+02 |g_param|=1.32e+04 loss=3.5604e-01 ppl=1.43                                                 
Validation - loss=6.9661e-01 ppl=2.01 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 58 - |param|=6.66e+02 |g_param|=1.55e+04 loss=3.6042e-01 ppl=1.43                                                 
Validation - loss=7.1140e-01 ppl=2.04 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 59 - |param|=6.66e+02 |g_param|=2.99e+04 loss=4.2528e-01 ppl=1.53                                                 
Validation - loss=7.1637e-01 ppl=2.05 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 60 - |param|=6.67e+02 |g_param|=1.86e+04 loss=3.9882e-01 ppl=1.49                                                 
Validation - loss=7.0891e-01 ppl=2.03 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 61 - |param|=6.67e+02 |g_param|=1.32e+04 loss=3.3813e-01 ppl=1.40                                                 
Validation - loss=6.8711e-01 ppl=1.99 best_loss=6.8965e-01 best_ppl=1.99                                                
Epoch 62 - |param|=6.68e+02 |g_param|=1.34e+04 loss=3.2732e-01 ppl=1.39                                                 
Validation - loss=6.8712e-01 ppl=1.99 best_loss=6.8711e-01 best_ppl=1.99                                                
Epoch 63 - |param|=6.68e+02 |g_param|=1.12e+04 loss=3.3336e-01 ppl=1.40                                                 
Validation - loss=6.9029e-01 ppl=1.99 best_loss=6.8711e-01 best_ppl=1.99                                                
Epoch 64 - |param|=6.68e+02 |g_param|=1.28e+04 loss=3.1062e-01 ppl=1.36                                                 
Validation - loss=6.8490e-01 ppl=1.98 best_loss=6.8711e-01 best_ppl=1.99                                                
Epoch 65 - |param|=6.68e+02 |g_param|=1.13e+04 loss=3.1400e-01 ppl=1.37                                                 
Validation - loss=6.9850e-01 ppl=2.01 best_loss=6.8490e-01 best_ppl=1.98                                                
Epoch 66 - |param|=6.69e+02 |g_param|=1.32e+04 loss=2.9703e-01 ppl=1.35                                                 
Validation - loss=6.9538e-01 ppl=2.00 best_loss=6.8490e-01 best_ppl=1.98                                                
Epoch 67 - |param|=6.69e+02 |g_param|=1.40e+04 loss=2.9656e-01 ppl=1.35                                                 
Validation - loss=6.8139e-01 ppl=1.98 best_loss=6.8490e-01 best_ppl=1.98                                                
Epoch 68 - |param|=6.69e+02 |g_param|=1.91e+04 loss=2.8941e-01 ppl=1.34                                                 
Validation - loss=6.7890e-01 ppl=1.97 best_loss=6.8139e-01 best_ppl=1.98                                                
Epoch 69 - |param|=6.70e+02 |g_param|=1.89e+04 loss=2.8260e-01 ppl=1.33                                                 
Validation - loss=6.7864e-01 ppl=1.97 best_loss=6.7890e-01 best_ppl=1.97                                                
Epoch 70 - |param|=6.70e+02 |g_param|=2.30e+04 loss=2.8337e-01 ppl=1.33                                                 
Validation - loss=6.7765e-01 ppl=1.97 best_loss=6.7864e-01 best_ppl=1.97                                                
Epoch 71 - |param|=6.70e+02 |g_param|=3.05e+04 loss=3.0508e-01 ppl=1.36                                                 
Validation - loss=6.7891e-01 ppl=1.97 best_loss=6.7765e-01 best_ppl=1.97                                                
Epoch 72 - |param|=6.71e+02 |g_param|=2.69e+04 loss=2.9522e-01 ppl=1.34                                                 
Validation - loss=6.7655e-01 ppl=1.97 best_loss=6.7765e-01 best_ppl=1.97                                                
Epoch 73 - |param|=6.71e+02 |g_param|=2.15e+04 loss=2.6801e-01 ppl=1.31                                                 
Validation - loss=6.7691e-01 ppl=1.97 best_loss=6.7655e-01 best_ppl=1.97                                                
Epoch 74 - |param|=6.71e+02 |g_param|=1.86e+04 loss=2.6175e-01 ppl=1.30                                                 
Validation - loss=6.7862e-01 ppl=1.97 best_loss=6.7655e-01 best_ppl=1.97                                                
Epoch 75 - |param|=6.71e+02 |g_param|=2.02e+04 loss=2.5797e-01 ppl=1.29                                                 
Validation - loss=6.6501e-01 ppl=1.94 best_loss=6.7655e-01 best_ppl=1.97                                                
Epoch 76 - |param|=6.72e+02 |g_param|=2.00e+04 loss=2.4613e-01 ppl=1.28                                                 
Validation - loss=6.8101e-01 ppl=1.98 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 77 - |param|=6.72e+02 |g_param|=2.07e+04 loss=2.4531e-01 ppl=1.28                                                 
Validation - loss=6.9046e-01 ppl=1.99 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 78 - |param|=6.72e+02 |g_param|=2.29e+04 loss=2.5415e-01 ppl=1.29                                                 
Validation - loss=6.8877e-01 ppl=1.99 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 79 - |param|=6.72e+02 |g_param|=1.81e+04 loss=2.5104e-01 ppl=1.29                                                 
Validation - loss=6.8823e-01 ppl=1.99 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 80 - |param|=6.73e+02 |g_param|=1.94e+04 loss=2.3357e-01 ppl=1.26                                                 
Validation - loss=6.9471e-01 ppl=2.00 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 81 - |param|=6.73e+02 |g_param|=1.95e+04 loss=2.4579e-01 ppl=1.28                                                 
Validation - loss=6.9500e-01 ppl=2.00 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 82 - |param|=6.73e+02 |g_param|=2.04e+04 loss=2.4703e-01 ppl=1.28                                                 
Validation - loss=6.9485e-01 ppl=2.00 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 83 - |param|=6.74e+02 |g_param|=1.87e+04 loss=2.3179e-01 ppl=1.26                                                 
Validation - loss=7.0929e-01 ppl=2.03 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 84 - |param|=6.74e+02 |g_param|=2.24e+04 loss=2.4338e-01 ppl=1.28                                                 
Validation - loss=7.0387e-01 ppl=2.02 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 85 - |param|=6.74e+02 |g_param|=2.10e+04 loss=2.2838e-01 ppl=1.26                                                 
Validation - loss=6.9015e-01 ppl=1.99 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 86 - |param|=6.75e+02 |g_param|=6.07e+04 loss=3.8494e-01 ppl=1.47                                                 
Validation - loss=7.5270e-01 ppl=2.12 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 87 - |param|=6.75e+02 |g_param|=2.83e+04 loss=2.6356e-01 ppl=1.30                                                 
Validation - loss=7.9256e-01 ppl=2.21 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 88 - |param|=6.76e+02 |g_param|=4.63e+04 loss=2.6541e-01 ppl=1.30                                                 
Validation - loss=7.0142e-01 ppl=2.02 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 89 - |param|=6.76e+02 |g_param|=4.31e+04 loss=2.3255e-01 ppl=1.26                                                 
Validation - loss=7.0825e-01 ppl=2.03 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 90 - |param|=6.76e+02 |g_param|=3.63e+04 loss=2.1921e-01 ppl=1.25                                                 
Validation - loss=6.9714e-01 ppl=2.01 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 91 - |param|=6.76e+02 |g_param|=3.90e+04 loss=2.2873e-01 ppl=1.26                                                 
Validation - loss=7.0514e-01 ppl=2.02 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 92 - |param|=6.77e+02 |g_param|=3.62e+04 loss=2.0988e-01 ppl=1.23                                                 
Validation - loss=7.0226e-01 ppl=2.02 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 93 - |param|=6.77e+02 |g_param|=3.77e+04 loss=2.1734e-01 ppl=1.24                                                 
Validation - loss=7.1277e-01 ppl=2.04 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 94 - |param|=6.77e+02 |g_param|=3.87e+04 loss=2.0128e-01 ppl=1.22                                                 
Validation - loss=7.3682e-01 ppl=2.09 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 95 - |param|=6.77e+02 |g_param|=3.21e+04 loss=2.0735e-01 ppl=1.23                                                 
Validation - loss=7.0614e-01 ppl=2.03 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 96 - |param|=6.78e+02 |g_param|=3.80e+04 loss=2.1187e-01 ppl=1.24                                                 
Validation - loss=7.0411e-01 ppl=2.02 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 97 - |param|=6.78e+02 |g_param|=3.71e+04 loss=2.0584e-01 ppl=1.23                                                 
Validation - loss=7.2525e-01 ppl=2.07 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 98 - |param|=6.78e+02 |g_param|=3.85e+04 loss=1.9752e-01 ppl=1.22                                                 
Validation - loss=7.3375e-01 ppl=2.08 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 99 - |param|=6.79e+02 |g_param|=3.44e+04 loss=1.9314e-01 ppl=1.21                                                 
Validation - loss=7.1625e-01 ppl=2.05 best_loss=6.6501e-01 best_ppl=1.94                                                
Epoch 100 - |param|=6.79e+02 |g_param|=3.20e+04 loss=1.8826e-01 ppl=1.21                                                
Validation - loss=7.4060e-01 ppl=2.10 best_loss=6.6501e-01 best_ppl=1.94                                                

real	13m45.251s
user	13m34.067s
sys	0m11.258s
(simple-nmt) ye@:~/exp/simple-nmt$ 

```

testing/evaluation for RL fine-tuning for my-rk...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch/baseline$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-myrk.30.0.61-1.84.0.84-2.31.pth
BLEU = 69.38, 85.6/74.1/64.6/56.5 (BP=1.000, ratio=1.013, hyp_len=23472, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.31.0.61-1.84.0.82-2.28.pth
BLEU = 69.51, 85.5/74.2/64.8/56.8 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.32.0.59-1.81.0.83-2.29.pth
BLEU = 69.53, 85.3/74.1/64.9/57.0 (BP=1.000, ratio=1.024, hyp_len=23706, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.33.0.58-1.78.0.83-2.29.pth
BLEU = 70.24, 85.7/74.7/65.6/57.9 (BP=1.000, ratio=1.020, hyp_len=23627, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.34.0.59-1.80.0.81-2.24.pth
BLEU = 69.73, 85.6/74.3/65.0/57.2 (BP=1.000, ratio=1.020, hyp_len=23621, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.35.0.53-1.70.0.82-2.27.pth
BLEU = 68.64, 85.0/73.5/63.8/55.7 (BP=1.000, ratio=1.025, hyp_len=23750, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.36.0.61-1.83.0.81-2.24.pth
BLEU = 71.29, 86.6/75.7/66.7/59.0 (BP=1.000, ratio=1.012, hyp_len=23446, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.37.0.53-1.71.0.80-2.22.pth
BLEU = 70.77, 86.3/75.2/66.1/58.5 (BP=1.000, ratio=1.012, hyp_len=23442, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.38.0.52-1.69.0.76-2.15.pth
BLEU = 71.23, 86.3/75.6/66.7/59.2 (BP=1.000, ratio=1.017, hyp_len=23550, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.39.0.51-1.67.0.77-2.16.pth
BLEU = 71.91, 86.5/76.1/67.5/60.2 (BP=1.000, ratio=1.017, hyp_len=23553, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.40.0.48-1.62.0.75-2.12.pth
BLEU = 71.79, 86.4/76.0/67.4/60.0 (BP=1.000, ratio=1.025, hyp_len=23745, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.41.0.44-1.56.0.73-2.08.pth
BLEU = 72.57, 86.8/76.7/68.2/61.0 (BP=1.000, ratio=1.024, hyp_len=23718, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.42.0.45-1.56.0.73-2.08.pth
BLEU = 72.30, 86.5/76.4/68.0/60.8 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.43.0.44-1.56.0.73-2.07.pth
BLEU = 72.58, 86.7/76.6/68.3/61.2 (BP=1.000, ratio=1.024, hyp_len=23726, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.44.0.40-1.49.0.72-2.06.pth
BLEU = 72.46, 86.7/76.6/68.1/60.9 (BP=1.000, ratio=1.026, hyp_len=23771, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.45.0.42-1.52.0.74-2.10.pth
BLEU = 71.69, 86.1/75.9/67.3/60.1 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.46.0.45-1.57.0.75-2.13.pth
BLEU = 70.49, 85.5/74.8/66.0/58.5 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.47.0.42-1.52.0.74-2.10.pth
BLEU = 71.76, 86.0/75.9/67.5/60.2 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.48.0.40-1.49.0.73-2.07.pth
BLEU = 73.05, 87.0/77.0/68.8/61.8 (BP=1.000, ratio=1.020, hyp_len=23618, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.49.0.38-1.47.0.73-2.07.pth
BLEU = 73.43, 87.1/77.4/69.2/62.3 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.50.0.37-1.45.0.72-2.05.pth
BLEU = 73.23, 86.7/77.0/69.1/62.3 (BP=1.000, ratio=1.026, hyp_len=23770, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.51.0.37-1.45.0.70-2.01.pth
BLEU = 73.17, 87.0/77.1/68.9/62.0 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.52.0.37-1.44.0.69-2.00.pth
BLEU = 72.98, 86.7/76.9/68.8/61.8 (BP=1.000, ratio=1.027, hyp_len=23787, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.53.0.34-1.41.0.70-2.00.pth
BLEU = 73.62, 87.1/77.5/69.5/62.6 (BP=1.000, ratio=1.026, hyp_len=23753, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.54.0.34-1.41.0.69-1.99.pth
BLEU = 73.26, 86.7/77.1/69.1/62.3 (BP=1.000, ratio=1.030, hyp_len=23859, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.55.0.36-1.43.0.71-2.04.pth
BLEU = 74.48, 87.6/78.2/70.4/63.8 (BP=1.000, ratio=1.019, hyp_len=23592, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.56.0.35-1.42.0.71-2.04.pth
BLEU = 72.64, 86.5/76.7/68.4/61.4 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.57.0.36-1.43.0.70-2.01.pth
BLEU = 73.37, 87.0/77.3/69.2/62.3 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.58.0.36-1.43.0.71-2.04.pth
BLEU = 73.23, 86.7/77.1/69.1/62.3 (BP=1.000, ratio=1.030, hyp_len=23854, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.59.0.43-1.53.0.72-2.05.pth
BLEU = 70.64, 85.4/75.0/66.3/58.7 (BP=1.000, ratio=1.040, hyp_len=24079, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.60.0.40-1.49.0.71-2.03.pth
BLEU = 73.14, 86.9/77.1/68.9/62.0 (BP=1.000, ratio=1.026, hyp_len=23752, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.61.0.34-1.40.0.69-1.99.pth
BLEU = 74.20, 87.1/77.9/70.2/63.6 (BP=1.000, ratio=1.024, hyp_len=23724, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.62.0.33-1.39.0.69-1.99.pth
BLEU = 73.64, 87.0/77.4/69.5/62.8 (BP=1.000, ratio=1.026, hyp_len=23766, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.63.0.33-1.40.0.69-1.99.pth
BLEU = 73.27, 86.7/77.2/69.1/62.4 (BP=1.000, ratio=1.031, hyp_len=23882, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.64.0.31-1.36.0.68-1.98.pth
BLEU = 74.13, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.024, hyp_len=23708, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.65.0.31-1.37.0.70-2.01.pth
BLEU = 72.94, 86.5/76.9/68.8/61.9 (BP=1.000, ratio=1.036, hyp_len=23988, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.66.0.30-1.35.0.70-2.00.pth
BLEU = 73.12, 86.7/77.0/69.0/62.2 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.67.0.30-1.35.0.68-1.98.pth
BLEU = 74.11, 87.3/77.9/70.0/63.3 (BP=1.000, ratio=1.029, hyp_len=23832, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.68.0.29-1.34.0.68-1.97.pth
BLEU = 74.82, 87.6/78.5/70.9/64.3 (BP=1.000, ratio=1.025, hyp_len=23735, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.69.0.28-1.33.0.68-1.97.pth
BLEU = 74.40, 87.4/78.2/70.4/63.7 (BP=1.000, ratio=1.028, hyp_len=23798, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.70.0.28-1.33.0.68-1.97.pth
BLEU = 74.21, 87.2/77.9/70.2/63.6 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.71.0.31-1.36.0.68-1.97.pth
BLEU = 72.82, 86.5/76.8/68.6/61.7 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.72.0.30-1.34.0.68-1.97.pth
BLEU = 74.44, 87.3/78.1/70.5/63.9 (BP=1.000, ratio=1.030, hyp_len=23849, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.73.0.27-1.31.0.68-1.97.pth
BLEU = 74.51, 87.3/78.1/70.5/64.0 (BP=1.000, ratio=1.028, hyp_len=23797, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.74.0.26-1.30.0.68-1.97.pth
BLEU = 73.91, 86.9/77.6/69.9/63.3 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.75.0.26-1.29.0.67-1.94.pth
BLEU = 74.65, 87.4/78.3/70.7/64.2 (BP=1.000, ratio=1.029, hyp_len=23832, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.76.0.25-1.28.0.68-1.98.pth
BLEU = 74.45, 87.3/78.1/70.5/64.0 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.77.0.25-1.28.0.69-1.99.pth
BLEU = 74.07, 87.1/77.7/70.0/63.4 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.78.0.25-1.29.0.69-1.99.pth
BLEU = 73.99, 87.1/77.7/70.0/63.3 (BP=1.000, ratio=1.032, hyp_len=23912, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.79.0.25-1.29.0.69-1.99.pth
BLEU = 73.41, 86.7/77.2/69.3/62.6 (BP=1.000, ratio=1.036, hyp_len=23983, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.80.0.23-1.26.0.69-2.00.pth
BLEU = 74.38, 87.3/78.0/70.4/63.9 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.81.0.25-1.28.0.70-2.00.pth
BLEU = 74.87, 87.6/78.5/70.9/64.5 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.82.0.25-1.28.0.69-2.00.pth
BLEU = 74.39, 87.2/78.0/70.4/63.9 (BP=1.000, ratio=1.029, hyp_len=23837, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.83.0.23-1.26.0.71-2.03.pth
BLEU = 74.25, 87.1/77.9/70.3/63.7 (BP=1.000, ratio=1.027, hyp_len=23795, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.84.0.24-1.28.0.70-2.02.pth
BLEU = 73.61, 87.0/77.5/69.5/62.7 (BP=1.000, ratio=1.033, hyp_len=23928, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.85.0.23-1.26.0.69-1.99.pth
BLEU = 74.46, 87.4/78.1/70.5/63.9 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.86.0.38-1.47.0.75-2.12.pth
BLEU = 73.48, 87.2/77.4/69.3/62.4 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.87.0.26-1.30.0.79-2.21.pth
BLEU = 71.43, 85.4/75.7/67.3/59.9 (BP=1.000, ratio=1.051, hyp_len=24347, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.88.0.27-1.30.0.70-2.02.pth
BLEU = 74.39, 87.3/78.0/70.4/63.9 (BP=1.000, ratio=1.029, hyp_len=23843, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.89.0.23-1.26.0.71-2.03.pth
BLEU = 74.23, 87.2/77.9/70.2/63.7 (BP=1.000, ratio=1.032, hyp_len=23891, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.90.0.22-1.25.0.70-2.01.pth
BLEU = 74.18, 87.1/77.9/70.2/63.6 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.91.0.23-1.26.0.71-2.02.pth
BLEU = 73.63, 86.9/77.4/69.5/62.9 (BP=1.000, ratio=1.032, hyp_len=23904, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.92.0.21-1.23.0.70-2.02.pth
BLEU = 74.09, 87.2/77.9/70.1/63.3 (BP=1.000, ratio=1.031, hyp_len=23877, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.93.0.22-1.24.0.71-2.04.pth
BLEU = 73.91, 86.9/77.6/69.9/63.2 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.94.0.20-1.22.0.74-2.09.pth
BLEU = 73.67, 86.9/77.5/69.6/62.9 (BP=1.000, ratio=1.038, hyp_len=24042, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.95.0.21-1.23.0.71-2.03.pth
BLEU = 74.43, 87.2/78.1/70.5/63.9 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.96.0.21-1.24.0.70-2.02.pth
BLEU = 73.58, 86.7/77.3/69.5/62.9 (BP=1.000, ratio=1.037, hyp_len=24017, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.97.0.21-1.23.0.73-2.07.pth
BLEU = 74.17, 87.0/77.8/70.2/63.6 (BP=1.000, ratio=1.033, hyp_len=23919, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.98.0.20-1.22.0.73-2.08.pth
BLEU = 73.40, 86.7/77.2/69.3/62.6 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.99.0.19-1.21.0.72-2.05.pth
BLEU = 73.39, 86.6/77.2/69.3/62.6 (BP=1.000, ratio=1.036, hyp_len=24000, ref_len=23160)
Evaluation result for the model: seq-rl-model-myrk.100.0.19-1.21.0.74-2.10.pth
BLEU = 73.84, 86.8/77.5/69.8/63.3 (BP=1.000, ratio=1.038, hyp_len=24047, ref_len=23160)
real	23m42.961s
user	23m10.337s
sys	1m19.762s

```

အထက်ပါ list က sorting အစီအစဉ်အတိုင်း မဟုတ်ဘူး...  

myrk, Baseline model best score: BLEU = 68.10  
myrk, RL Fine-tuning best score: BLEU = 74.87 (seq-rl-model-myrk.81.0.25-1.28.0.70-2.00.pth မော်ဒယ်ရဲ့)   

```
Evaluation result for the model: seq-rl-model-myrk.81.0.25-1.28.0.70-2.00.pth
BLEU = 74.87, 87.6/78.5/70.9/64.5 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
```

To Do: baseline ကိုလည်း 100 epoch, RL fine-tuning ကိုလည်း 100 epoch ထားကြည့်ပြီး စမ်းချင်...  

### for rk-my

rk-my အတွဲအတွက် RL fine tuning လုပ် ...  

time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth --model_fn ./model/rl/seq2seq/100epoch/baseline/rkmy/seq-rl-model-rkmy.pth --init_epoch 30 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth --model_fn ./model/rl/seq2seq/100epoch/baseline/rkmy/seq-rl-model-rkmy.pth --init_epoch 30 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/seq2seq/100epoch/baseline/rkmy/seq-rl-model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 30,
    'iteration_per_update': 2,
    'lang': 'rkmy',
    'load_fn': './model/seq2seq/baseline/rkmy-100epoch/seq-model-rkmy.30.0.86-2.37.1.05-2.84.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/seq2seq/100epoch/baseline/rkmy/seq-rl-model-rkmy.pth',
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
Epoch 30 - |param|=6.56e+02 |g_param|=8.38e+04 loss=8.1420e-01 ppl=2.26                                                 
Validation - loss=9.9875e-01 ppl=2.71 best_loss=inf best_ppl=inf                                                        
Epoch 31 - |param|=6.56e+02 |g_param|=9.39e+04 loss=7.9605e-01 ppl=2.22                                                 
Validation - loss=1.0482e+00 ppl=2.85 best_loss=9.9875e-01 best_ppl=2.71                                                
Epoch 32 - |param|=6.57e+02 |g_param|=1.02e+05 loss=7.6071e-01 ppl=2.14                                                 
Validation - loss=1.0596e+00 ppl=2.89 best_loss=9.9875e-01 best_ppl=2.71                                                
Epoch 33 - |param|=6.57e+02 |g_param|=8.63e+04 loss=7.1626e-01 ppl=2.05                                                 
Validation - loss=9.2464e-01 ppl=2.52 best_loss=9.9875e-01 best_ppl=2.71                                                
Epoch 34 - |param|=6.57e+02 |g_param|=8.34e+04 loss=7.3581e-01 ppl=2.09                                                 
Validation - loss=9.2967e-01 ppl=2.53 best_loss=9.2464e-01 best_ppl=2.52                                                
Epoch 35 - |param|=6.58e+02 |g_param|=8.64e+04 loss=6.7980e-01 ppl=1.97                                                 
Validation - loss=9.0875e-01 ppl=2.48 best_loss=9.2464e-01 best_ppl=2.52                                                
Epoch 36 - |param|=6.58e+02 |g_param|=7.72e+04 loss=6.6560e-01 ppl=1.95                                                 
Validation - loss=9.0480e-01 ppl=2.47 best_loss=9.0875e-01 best_ppl=2.48                                                
Epoch 37 - |param|=6.59e+02 |g_param|=1.09e+05 loss=6.8680e-01 ppl=1.99                                                 
Validation - loss=9.4250e-01 ppl=2.57 best_loss=9.0480e-01 best_ppl=2.47                                                
Epoch 38 - |param|=6.59e+02 |g_param|=8.51e+04 loss=6.2424e-01 ppl=1.87                                                 
Validation - loss=8.9184e-01 ppl=2.44 best_loss=9.0480e-01 best_ppl=2.47                                                
Epoch 39 - |param|=6.59e+02 |g_param|=6.45e+04 loss=5.8946e-01 ppl=1.80                                                 
Validation - loss=8.7633e-01 ppl=2.40 best_loss=8.9184e-01 best_ppl=2.44                                                
Epoch 40 - |param|=6.60e+02 |g_param|=3.87e+04 loss=5.7399e-01 ppl=1.78                                                 
Validation - loss=8.4981e-01 ppl=2.34 best_loss=8.7633e-01 best_ppl=2.40                                                
Epoch 41 - |param|=6.60e+02 |g_param|=3.44e+04 loss=5.5463e-01 ppl=1.74                                                 
Validation - loss=8.3287e-01 ppl=2.30 best_loss=8.4981e-01 best_ppl=2.34                                                
Epoch 42 - |param|=6.60e+02 |g_param|=7.49e+04 loss=6.6912e-01 ppl=1.95                                                 
Validation - loss=9.1526e-01 ppl=2.50 best_loss=8.3287e-01 best_ppl=2.30                                                
Epoch 43 - |param|=6.61e+02 |g_param|=4.12e+04 loss=5.6067e-01 ppl=1.75                                                 
Validation - loss=8.4510e-01 ppl=2.33 best_loss=8.3287e-01 best_ppl=2.30                                                
Epoch 44 - |param|=6.61e+02 |g_param|=3.04e+04 loss=5.3502e-01 ppl=1.71                                                 
Validation - loss=8.0796e-01 ppl=2.24 best_loss=8.3287e-01 best_ppl=2.30                                                
Epoch 45 - |param|=6.62e+02 |g_param|=4.12e+04 loss=5.3002e-01 ppl=1.70                                                 
Validation - loss=8.1350e-01 ppl=2.26 best_loss=8.0796e-01 best_ppl=2.24                                                
Epoch 46 - |param|=6.62e+02 |g_param|=3.17e+04 loss=5.1146e-01 ppl=1.67                                                 
Validation - loss=8.0639e-01 ppl=2.24 best_loss=8.0796e-01 best_ppl=2.24                                                
Epoch 47 - |param|=6.62e+02 |g_param|=3.48e+04 loss=4.9541e-01 ppl=1.64                                                 
Validation - loss=8.0571e-01 ppl=2.24 best_loss=8.0639e-01 best_ppl=2.24                                                
Epoch 48 - |param|=6.62e+02 |g_param|=3.40e+04 loss=4.9995e-01 ppl=1.65                                                 
Validation - loss=8.0801e-01 ppl=2.24 best_loss=8.0571e-01 best_ppl=2.24                                                
Epoch 49 - |param|=6.63e+02 |g_param|=3.05e+04 loss=4.7392e-01 ppl=1.61                                                 
Validation - loss=7.8580e-01 ppl=2.19 best_loss=8.0571e-01 best_ppl=2.24                                                
Epoch 50 - |param|=6.63e+02 |g_param|=2.54e+04 loss=4.4361e-01 ppl=1.56                                                 
Validation - loss=7.8259e-01 ppl=2.19 best_loss=7.8580e-01 best_ppl=2.19                                                
Epoch 51 - |param|=6.63e+02 |g_param|=2.76e+04 loss=4.2383e-01 ppl=1.53                                                 
Validation - loss=7.8811e-01 ppl=2.20 best_loss=7.8259e-01 best_ppl=2.19                                                
Epoch 52 - |param|=6.64e+02 |g_param|=3.16e+04 loss=4.4039e-01 ppl=1.55                                                 
Validation - loss=7.6517e-01 ppl=2.15 best_loss=7.8259e-01 best_ppl=2.19                                                
Epoch 53 - |param|=6.64e+02 |g_param|=2.77e+04 loss=4.1433e-01 ppl=1.51                                                 
Validation - loss=7.7960e-01 ppl=2.18 best_loss=7.6517e-01 best_ppl=2.15                                                
Epoch 54 - |param|=6.64e+02 |g_param|=3.83e+04 loss=4.3657e-01 ppl=1.55                                                 
Validation - loss=7.7081e-01 ppl=2.16 best_loss=7.6517e-01 best_ppl=2.15                                                
Epoch 55 - |param|=6.65e+02 |g_param|=3.57e+04 loss=4.5010e-01 ppl=1.57                                                 
Validation - loss=7.5998e-01 ppl=2.14 best_loss=7.6517e-01 best_ppl=2.15                                                
Epoch 56 - |param|=6.65e+02 |g_param|=2.61e+04 loss=3.9350e-01 ppl=1.48                                                 
Validation - loss=7.6568e-01 ppl=2.15 best_loss=7.5998e-01 best_ppl=2.14                                                
Epoch 57 - |param|=6.65e+02 |g_param|=2.58e+04 loss=3.8674e-01 ppl=1.47                                                 
Validation - loss=7.5527e-01 ppl=2.13 best_loss=7.5998e-01 best_ppl=2.14                                                
Epoch 58 - |param|=6.66e+02 |g_param|=2.54e+04 loss=3.8396e-01 ppl=1.47                                                 
Validation - loss=7.5427e-01 ppl=2.13 best_loss=7.5527e-01 best_ppl=2.13                                                
Epoch 59 - |param|=6.66e+02 |g_param|=2.87e+04 loss=3.9071e-01 ppl=1.48                                                 
Validation - loss=7.6321e-01 ppl=2.15 best_loss=7.5427e-01 best_ppl=2.13                                                
Epoch 60 - |param|=6.66e+02 |g_param|=3.62e+04 loss=3.7694e-01 ppl=1.46                                                 
Validation - loss=7.4493e-01 ppl=2.11 best_loss=7.5427e-01 best_ppl=2.13                                                
Epoch 61 - |param|=6.67e+02 |g_param|=5.19e+04 loss=3.6225e-01 ppl=1.44                                                 
Validation - loss=7.3464e-01 ppl=2.08 best_loss=7.4493e-01 best_ppl=2.11                                                
Epoch 62 - |param|=6.67e+02 |g_param|=2.50e+04 loss=3.3992e-01 ppl=1.40                                                 
Validation - loss=7.4607e-01 ppl=2.11 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 63 - |param|=6.67e+02 |g_param|=2.34e+04 loss=3.5882e-01 ppl=1.43                                                 
Validation - loss=7.4597e-01 ppl=2.11 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 64 - |param|=6.68e+02 |g_param|=3.84e+04 loss=3.6512e-01 ppl=1.44                                                 
Validation - loss=7.6394e-01 ppl=2.15 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 65 - |param|=6.68e+02 |g_param|=4.07e+04 loss=4.1553e-01 ppl=1.52                                                 
Validation - loss=7.8568e-01 ppl=2.19 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 66 - |param|=6.68e+02 |g_param|=3.09e+04 loss=3.6809e-01 ppl=1.44                                                 
Validation - loss=7.5159e-01 ppl=2.12 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 67 - |param|=6.69e+02 |g_param|=3.48e+04 loss=3.5372e-01 ppl=1.42                                                 
Validation - loss=7.6346e-01 ppl=2.15 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 68 - |param|=6.69e+02 |g_param|=2.75e+04 loss=3.5023e-01 ppl=1.42                                                 
Validation - loss=7.5028e-01 ppl=2.12 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 69 - |param|=6.69e+02 |g_param|=2.28e+04 loss=3.1856e-01 ppl=1.38                                                 
Validation - loss=7.3812e-01 ppl=2.09 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 70 - |param|=6.69e+02 |g_param|=2.54e+04 loss=3.3057e-01 ppl=1.39                                                 
Validation - loss=7.3648e-01 ppl=2.09 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 71 - |param|=6.70e+02 |g_param|=2.72e+04 loss=3.3286e-01 ppl=1.39                                                 
Validation - loss=7.2742e-01 ppl=2.07 best_loss=7.3464e-01 best_ppl=2.08                                                
Epoch 72 - |param|=6.70e+02 |g_param|=3.30e+04 loss=3.2137e-01 ppl=1.38                                                 
Validation - loss=7.6149e-01 ppl=2.14 best_loss=7.2742e-01 best_ppl=2.07                                                
Epoch 73 - |param|=6.70e+02 |g_param|=2.53e+04 loss=3.0827e-01 ppl=1.36                                                 
Validation - loss=7.5267e-01 ppl=2.12 best_loss=7.2742e-01 best_ppl=2.07                                                
Epoch 74 - |param|=6.71e+02 |g_param|=3.48e+04 loss=3.3000e-01 ppl=1.39                                                 
Validation - loss=7.4367e-01 ppl=2.10 best_loss=7.2742e-01 best_ppl=2.07                                                
Epoch 75 - |param|=6.71e+02 |g_param|=2.39e+04 loss=2.9539e-01 ppl=1.34                                                 
Validation - loss=7.3330e-01 ppl=2.08 best_loss=7.2742e-01 best_ppl=2.07                                                
Epoch 76 - |param|=6.71e+02 |g_param|=2.62e+04 loss=3.0829e-01 ppl=1.36                                                 
Validation - loss=7.2044e-01 ppl=2.06 best_loss=7.2742e-01 best_ppl=2.07                                                
Epoch 77 - |param|=6.72e+02 |g_param|=3.78e+04 loss=3.1742e-01 ppl=1.37                                                 
Validation - loss=7.4394e-01 ppl=2.10 best_loss=7.2044e-01 best_ppl=2.06                                                
Epoch 78 - |param|=6.72e+02 |g_param|=2.26e+04 loss=3.0268e-01 ppl=1.35                                                 
Validation - loss=7.1640e-01 ppl=2.05 best_loss=7.2044e-01 best_ppl=2.06                                                
Epoch 79 - |param|=6.72e+02 |g_param|=2.34e+04 loss=3.0472e-01 ppl=1.36                                                 
Validation - loss=7.0595e-01 ppl=2.03 best_loss=7.1640e-01 best_ppl=2.05                                                
Epoch 80 - |param|=6.73e+02 |g_param|=2.12e+04 loss=2.8905e-01 ppl=1.34                                                 
Validation - loss=7.2044e-01 ppl=2.06 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 81 - |param|=6.73e+02 |g_param|=2.17e+04 loss=2.6808e-01 ppl=1.31                                                 
Validation - loss=7.1649e-01 ppl=2.05 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 82 - |param|=6.73e+02 |g_param|=3.90e+04 loss=2.8980e-01 ppl=1.34                                                 
Validation - loss=7.1824e-01 ppl=2.05 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 83 - |param|=6.74e+02 |g_param|=4.18e+04 loss=2.8128e-01 ppl=1.32                                                 
Validation - loss=7.0617e-01 ppl=2.03 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 84 - |param|=6.74e+02 |g_param|=4.50e+04 loss=2.6877e-01 ppl=1.31                                                 
Validation - loss=7.1757e-01 ppl=2.05 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 85 - |param|=6.74e+02 |g_param|=4.90e+04 loss=2.7407e-01 ppl=1.32                                                 
Validation - loss=7.1666e-01 ppl=2.05 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 86 - |param|=6.74e+02 |g_param|=6.97e+04 loss=3.0848e-01 ppl=1.36                                                 
Validation - loss=7.2276e-01 ppl=2.06 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 87 - |param|=6.75e+02 |g_param|=2.60e+04 loss=2.6364e-01 ppl=1.30                                                 
Validation - loss=7.1408e-01 ppl=2.04 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 88 - |param|=6.75e+02 |g_param|=2.17e+04 loss=2.7708e-01 ppl=1.32                                                 
Validation - loss=7.0303e-01 ppl=2.02 best_loss=7.0595e-01 best_ppl=2.03                                                
Epoch 89 - |param|=6.75e+02 |g_param|=3.64e+04 loss=2.9379e-01 ppl=1.34                                                 
Validation - loss=7.1425e-01 ppl=2.04 best_loss=7.0303e-01 best_ppl=2.02                                                
Epoch 90 - |param|=6.76e+02 |g_param|=2.87e+04 loss=2.8236e-01 ppl=1.33                                                 
Validation - loss=6.9280e-01 ppl=2.00 best_loss=7.0303e-01 best_ppl=2.02                                                
Epoch 91 - |param|=6.76e+02 |g_param|=2.44e+04 loss=2.7238e-01 ppl=1.31                                                 
Validation - loss=7.1167e-01 ppl=2.04 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 92 - |param|=6.76e+02 |g_param|=2.04e+04 loss=2.4168e-01 ppl=1.27                                                 
Validation - loss=7.2233e-01 ppl=2.06 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 93 - |param|=6.77e+02 |g_param|=1.98e+04 loss=2.4748e-01 ppl=1.28                                                 
Validation - loss=7.0352e-01 ppl=2.02 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 94 - |param|=6.77e+02 |g_param|=2.41e+04 loss=2.4770e-01 ppl=1.28                                                 
Validation - loss=7.2943e-01 ppl=2.07 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 95 - |param|=6.77e+02 |g_param|=2.37e+04 loss=2.4835e-01 ppl=1.28                                                 
Validation - loss=7.0185e-01 ppl=2.02 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 96 - |param|=6.77e+02 |g_param|=2.98e+04 loss=2.4120e-01 ppl=1.27                                                 
Validation - loss=7.2051e-01 ppl=2.06 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 97 - |param|=6.78e+02 |g_param|=2.81e+04 loss=2.4766e-01 ppl=1.28                                                 
Validation - loss=7.0530e-01 ppl=2.02 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 98 - |param|=6.78e+02 |g_param|=3.24e+04 loss=2.7545e-01 ppl=1.32                                                 
Validation - loss=7.3303e-01 ppl=2.08 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 99 - |param|=6.79e+02 |g_param|=2.79e+04 loss=2.3967e-01 ppl=1.27                                                 
Validation - loss=7.3776e-01 ppl=2.09 best_loss=6.9280e-01 best_ppl=2.00                                                
Epoch 100 - |param|=6.79e+02 |g_param|=3.60e+04 loss=2.8550e-01 ppl=1.33                                                
Validation - loss=7.3571e-01 ppl=2.09 best_loss=6.9280e-01 best_ppl=2.00                                                

real	13m40.779s
user	13m29.619s
sys	0m11.196s
(simple-nmt) ye@:~/exp/simple-nmt$
```

rk-my အတွက် testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch/baseline/rkmy$ time ./test-eval-loop.sh 
Evaluation result for the model: seq-rl-model-rkmy.100.0.29-1.33.0.74-2.09.pth
BLEU = 72.92, 86.7/77.1/68.5/61.8 (BP=1.000, ratio=1.042, hyp_len=24495, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.30.0.81-2.26.1.00-2.71.pth
BLEU = 62.88, 82.1/68.8/57.3/48.3 (BP=1.000, ratio=1.016, hyp_len=23893, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.31.0.80-2.22.1.05-2.85.pth
BLEU = 61.52, 81.2/67.7/55.9/46.7 (BP=1.000, ratio=1.027, hyp_len=24141, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.32.0.76-2.14.1.06-2.89.pth
BLEU = 62.19, 81.6/68.4/56.7/47.3 (BP=1.000, ratio=1.030, hyp_len=24221, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.33.0.72-2.05.0.92-2.52.pth
BLEU = 66.04, 83.7/71.5/60.8/52.3 (BP=1.000, ratio=1.018, hyp_len=23930, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.34.0.74-2.09.0.93-2.53.pth
BLEU = 65.52, 83.3/71.1/60.2/51.7 (BP=1.000, ratio=1.026, hyp_len=24115, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.35.0.68-1.97.0.91-2.48.pth
BLEU = 66.67, 83.9/72.0/61.5/53.2 (BP=1.000, ratio=1.020, hyp_len=23981, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.36.0.67-1.95.0.90-2.47.pth
BLEU = 67.40, 84.3/72.7/62.3/54.0 (BP=1.000, ratio=1.026, hyp_len=24126, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.37.0.69-1.99.0.94-2.57.pth
BLEU = 66.82, 83.9/72.2/61.7/53.4 (BP=1.000, ratio=1.033, hyp_len=24281, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.38.0.62-1.87.0.89-2.44.pth
BLEU = 67.27, 84.1/72.6/62.2/53.9 (BP=1.000, ratio=1.029, hyp_len=24202, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.39.0.59-1.80.0.88-2.40.pth
BLEU = 68.35, 84.7/73.4/63.4/55.4 (BP=1.000, ratio=1.030, hyp_len=24217, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.40.0.57-1.78.0.85-2.34.pth
BLEU = 68.76, 84.7/73.7/63.8/56.1 (BP=1.000, ratio=1.033, hyp_len=24281, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.41.0.55-1.74.0.83-2.30.pth
BLEU = 70.15, 85.5/74.9/65.4/57.8 (BP=1.000, ratio=1.025, hyp_len=24104, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.42.0.67-1.95.0.92-2.50.pth
BLEU = 66.91, 84.4/72.3/61.7/53.3 (BP=1.000, ratio=1.016, hyp_len=23892, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.43.0.56-1.75.0.85-2.33.pth
BLEU = 69.93, 85.6/74.9/65.1/57.3 (BP=1.000, ratio=1.019, hyp_len=23944, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.44.0.54-1.71.0.81-2.24.pth
BLEU = 70.88, 86.0/75.6/66.2/58.7 (BP=1.000, ratio=1.026, hyp_len=24128, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.45.0.53-1.70.0.81-2.26.pth
BLEU = 70.27, 85.6/75.1/65.5/57.9 (BP=1.000, ratio=1.031, hyp_len=24232, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.46.0.51-1.67.0.81-2.24.pth
BLEU = 70.76, 85.7/75.4/66.1/58.7 (BP=1.000, ratio=1.031, hyp_len=24244, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.47.0.50-1.64.0.81-2.24.pth
BLEU = 71.84, 86.3/76.3/67.2/60.1 (BP=1.000, ratio=1.028, hyp_len=24165, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.48.0.50-1.65.0.81-2.24.pth
BLEU = 71.36, 86.0/76.0/66.7/59.5 (BP=1.000, ratio=1.030, hyp_len=24220, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.49.0.47-1.61.0.79-2.19.pth
BLEU = 71.98, 86.3/76.4/67.4/60.4 (BP=1.000, ratio=1.029, hyp_len=24186, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.50.0.44-1.56.0.78-2.19.pth
BLEU = 72.26, 86.5/76.6/67.7/60.7 (BP=1.000, ratio=1.028, hyp_len=24163, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.51.0.42-1.53.0.79-2.20.pth
BLEU = 72.14, 86.3/76.6/67.6/60.5 (BP=1.000, ratio=1.036, hyp_len=24362, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.52.0.44-1.55.0.77-2.15.pth
BLEU = 72.66, 86.7/77.0/68.2/61.2 (BP=1.000, ratio=1.034, hyp_len=24308, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.53.0.41-1.51.0.78-2.18.pth
BLEU = 73.43, 87.2/77.7/69.0/62.2 (BP=1.000, ratio=1.027, hyp_len=24147, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.54.0.44-1.55.0.77-2.16.pth
BLEU = 72.58, 86.6/76.9/68.1/61.2 (BP=1.000, ratio=1.026, hyp_len=24110, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.55.0.45-1.57.0.76-2.14.pth
BLEU = 72.29, 86.5/76.7/67.8/60.8 (BP=1.000, ratio=1.030, hyp_len=24210, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.56.0.39-1.48.0.77-2.15.pth
BLEU = 73.12, 86.8/77.3/68.7/61.9 (BP=1.000, ratio=1.031, hyp_len=24245, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.57.0.39-1.47.0.76-2.13.pth
BLEU = 73.32, 87.0/77.5/68.9/62.2 (BP=1.000, ratio=1.028, hyp_len=24168, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.58.0.38-1.47.0.75-2.13.pth
BLEU = 73.24, 86.8/77.4/68.9/62.1 (BP=1.000, ratio=1.034, hyp_len=24315, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.59.0.39-1.48.0.76-2.15.pth
BLEU = 73.36, 87.1/77.5/68.9/62.2 (BP=1.000, ratio=1.025, hyp_len=24094, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.60.0.38-1.46.0.74-2.11.pth
BLEU = 73.58, 87.1/77.8/69.3/62.4 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.61.0.36-1.44.0.73-2.08.pth
BLEU = 73.31, 86.9/77.5/68.9/62.2 (BP=1.000, ratio=1.034, hyp_len=24307, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.62.0.34-1.40.0.75-2.11.pth
BLEU = 74.72, 87.8/78.7/70.5/63.9 (BP=1.000, ratio=1.025, hyp_len=24101, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.63.0.36-1.43.0.75-2.11.pth
BLEU = 72.97, 86.8/77.2/68.5/61.7 (BP=1.000, ratio=1.036, hyp_len=24355, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.64.0.37-1.44.0.76-2.15.pth
BLEU = 71.02, 85.8/75.6/66.4/59.1 (BP=1.000, ratio=1.033, hyp_len=24280, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.65.0.42-1.52.0.79-2.19.pth
BLEU = 71.82, 86.1/76.2/67.2/60.3 (BP=1.000, ratio=1.042, hyp_len=24490, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.66.0.37-1.44.0.75-2.12.pth
BLEU = 73.06, 86.9/77.3/68.6/61.9 (BP=1.000, ratio=1.033, hyp_len=24285, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.67.0.35-1.42.0.76-2.15.pth
BLEU = 72.56, 86.3/76.8/68.1/61.4 (BP=1.000, ratio=1.043, hyp_len=24513, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.68.0.35-1.42.0.75-2.12.pth
BLEU = 73.78, 87.2/77.9/69.5/62.8 (BP=1.000, ratio=1.032, hyp_len=24255, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.69.0.32-1.38.0.74-2.09.pth
BLEU = 74.53, 87.7/78.6/70.2/63.7 (BP=1.000, ratio=1.031, hyp_len=24228, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.70.0.33-1.39.0.74-2.09.pth
BLEU = 73.62, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.032, hyp_len=24267, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.71.0.33-1.39.0.73-2.07.pth
BLEU = 73.66, 87.1/77.8/69.3/62.6 (BP=1.000, ratio=1.033, hyp_len=24278, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.72.0.32-1.38.0.76-2.14.pth
BLEU = 72.01, 86.0/76.4/67.6/60.6 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.73.0.31-1.36.0.75-2.12.pth
BLEU = 73.76, 87.1/77.9/69.5/62.8 (BP=1.000, ratio=1.033, hyp_len=24294, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.74.0.33-1.39.0.74-2.10.pth
BLEU = 73.50, 87.0/77.7/69.2/62.5 (BP=1.000, ratio=1.038, hyp_len=24400, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.75.0.30-1.34.0.73-2.08.pth
BLEU = 72.85, 86.6/77.0/68.5/61.7 (BP=1.000, ratio=1.043, hyp_len=24515, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.76.0.31-1.36.0.72-2.06.pth
BLEU = 73.99, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.034, hyp_len=24310, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.77.0.32-1.37.0.74-2.10.pth
BLEU = 73.77, 87.2/77.8/69.4/62.9 (BP=1.000, ratio=1.031, hyp_len=24248, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.78.0.30-1.35.0.72-2.05.pth
BLEU = 73.50, 87.0/77.6/69.1/62.5 (BP=1.000, ratio=1.039, hyp_len=24421, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.79.0.30-1.36.0.71-2.03.pth
BLEU = 73.60, 86.9/77.6/69.2/62.8 (BP=1.000, ratio=1.040, hyp_len=24458, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.80.0.29-1.34.0.72-2.06.pth
BLEU = 72.23, 86.2/76.5/67.7/61.0 (BP=1.000, ratio=1.046, hyp_len=24585, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.81.0.27-1.31.0.72-2.05.pth
BLEU = 73.80, 87.2/77.9/69.5/62.9 (BP=1.000, ratio=1.036, hyp_len=24362, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.82.0.29-1.34.0.72-2.05.pth
BLEU = 74.55, 87.6/78.6/70.3/63.8 (BP=1.000, ratio=1.034, hyp_len=24306, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.83.0.28-1.32.0.71-2.03.pth
BLEU = 72.79, 86.5/76.9/68.3/61.8 (BP=1.000, ratio=1.045, hyp_len=24576, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.84.0.27-1.31.0.72-2.05.pth
BLEU = 73.37, 86.9/77.5/69.0/62.4 (BP=1.000, ratio=1.040, hyp_len=24438, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.85.0.27-1.32.0.72-2.05.pth
BLEU = 74.36, 87.4/78.3/70.1/63.6 (BP=1.000, ratio=1.037, hyp_len=24379, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.86.0.31-1.36.0.72-2.06.pth
BLEU = 73.18, 86.8/77.3/68.8/62.2 (BP=1.000, ratio=1.036, hyp_len=24348, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.87.0.26-1.30.0.71-2.04.pth
BLEU = 73.91, 87.2/77.9/69.6/63.1 (BP=1.000, ratio=1.039, hyp_len=24416, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.88.0.28-1.32.0.70-2.02.pth
BLEU = 73.89, 87.1/77.9/69.6/63.2 (BP=1.000, ratio=1.037, hyp_len=24382, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.89.0.29-1.34.0.71-2.04.pth
BLEU = 73.81, 87.3/78.0/69.4/62.8 (BP=1.000, ratio=1.033, hyp_len=24288, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.90.0.28-1.33.0.69-2.00.pth
BLEU = 72.83, 86.5/77.0/68.4/61.8 (BP=1.000, ratio=1.046, hyp_len=24580, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.91.0.27-1.31.0.71-2.04.pth
BLEU = 73.67, 86.9/77.6/69.4/62.9 (BP=1.000, ratio=1.040, hyp_len=24440, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.92.0.24-1.27.0.72-2.06.pth
BLEU = 74.74, 87.6/78.6/70.6/64.3 (BP=1.000, ratio=1.033, hyp_len=24290, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.93.0.25-1.28.0.70-2.02.pth
BLEU = 74.41, 87.4/78.4/70.1/63.8 (BP=1.000, ratio=1.037, hyp_len=24370, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.94.0.25-1.28.0.73-2.07.pth
BLEU = 73.92, 87.2/78.0/69.6/63.0 (BP=1.000, ratio=1.040, hyp_len=24451, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.95.0.25-1.28.0.70-2.02.pth
BLEU = 74.34, 87.4/78.3/70.1/63.7 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.96.0.24-1.27.0.72-2.06.pth
BLEU = 73.63, 87.1/77.7/69.4/62.6 (BP=1.000, ratio=1.039, hyp_len=24422, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.97.0.25-1.28.0.71-2.02.pth
BLEU = 73.07, 86.7/77.3/68.7/61.9 (BP=1.000, ratio=1.040, hyp_len=24455, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.98.0.28-1.32.0.73-2.08.pth
BLEU = 72.25, 86.1/76.5/67.9/61.0 (BP=1.000, ratio=1.050, hyp_len=24692, ref_len=23509)
Evaluation result for the model: seq-rl-model-rkmy.99.0.24-1.27.0.74-2.09.pth
BLEU = 73.17, 86.8/77.3/68.8/62.1 (BP=1.000, ratio=1.034, hyp_len=24304, ref_len=23509)

real	23m53.408s
user	23m19.643s
sys	1m19.156s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/seq2seq/100epoch/baseline/rkmy$
```

အထက်ပါ list က sorting order အတိုင်း run ထားတာ မဟုတ်ဘူး ဆိုတာကို ဂရုပြုပါ...  

Baseline Best Score က BLEU = 59.48  
rk-my အတွက် RL fine-tuning 100epoch မော်ဒယ်ရဲ့ best score က BLEU = 74.74

```
Evaluation result for the model: seq-rl-model-rkmy.92.0.24-1.27.0.72-2.06.pth
BLEU = 74.74, 87.6/78.6/70.6/64.3 (BP=1.000, ratio=1.033, hyp_len=24290, ref_len=23509)
```

## Training Transformer baseline

အထက်က seq2seq တုန်းကလိုပဲ baseline model ကို 30 epoch နဲ့ training လုပ်ပြီးတော့ RL fine-tuning ကို 70 နဲ့ပဲ သွားမယ်...  
data path ကိုလည်း dev data ဆိုက်တိုးထားတဲ့ path နဲ့ ပြောင်းခဲ့တယ်...  

### for my-rk

training baseline မော်ဒယ်...  
time python train.py --train /home/ye/exp/simple-nmt/data/train  --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.pth  

ဒါပေမဲ့ အထက်ပါ model နဲ့ training လုပ်ပြီး test/eval လုပ်ကြည့်တဲ့အခါမှာ epoch 30 နဲ့က BLEU score က 26.16 ပဲ ရတယ်။  

```
Evaluation result for the model: myrk-transformer-model.29.2.14-8.50.2.13-8.44.pth
BLEU = 26.16, 59.1/34.9/20.1/11.3 (BP=1.000, ratio=1.025, hyp_len=23748, ref_len=23160)
```

အဲဒါကြောင့် epoch ကို တိုးမှ ရလိမ့်မယ်...  


time python train.py --train /home/ye/exp/simple-nmt/data/train  --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.pth  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train  --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.pth
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
Epoch 1 - |param|=3.24e+02 |g_param|=3.48e+05 loss=5.7769e+00 ppl=322.76                                                
Validation - loss=5.7995e+00 ppl=330.12 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.24e+02 |g_param|=3.40e+05 loss=4.9644e+00 ppl=143.22                                                
Validation - loss=4.9990e+00 ppl=148.26 best_loss=5.7995e+00 best_ppl=330.12                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.38e+05 loss=4.4957e+00 ppl=89.63                                                 
Validation - loss=4.5900e+00 ppl=98.49 best_loss=4.9990e+00 best_ppl=148.26                                             
Epoch 4 - |param|=3.24e+02 |g_param|=1.84e+05 loss=4.2108e+00 ppl=67.41                                                 
Validation - loss=4.3247e+00 ppl=75.55 best_loss=4.5900e+00 best_ppl=98.49                                              
Epoch 5 - |param|=3.24e+02 |g_param|=1.59e+05 loss=4.0004e+00 ppl=54.62                                                 
Validation - loss=4.1212e+00 ppl=61.64 best_loss=4.3247e+00 best_ppl=75.55                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.85e+05 loss=3.8397e+00 ppl=46.51                                                 
Validation - loss=3.9395e+00 ppl=51.39 best_loss=4.1212e+00 best_ppl=61.64                                              
Epoch 7 - |param|=3.24e+02 |g_param|=1.51e+05 loss=3.6741e+00 ppl=39.41                                                 
Validation - loss=3.7814e+00 ppl=43.88 best_loss=3.9395e+00 best_ppl=51.39                                              
Epoch 8 - |param|=3.24e+02 |g_param|=2.27e+05 loss=3.5315e+00 ppl=34.18                                                 
Validation - loss=3.6349e+00 ppl=37.90 best_loss=3.7814e+00 best_ppl=43.88                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.41e+05 loss=3.4255e+00 ppl=30.74                                                 
Validation - loss=3.5026e+00 ppl=33.20 best_loss=3.6349e+00 best_ppl=37.90                                              
Epoch 10 - |param|=3.24e+02 |g_param|=1.72e+05 loss=3.3215e+00 ppl=27.70                                                
Validation - loss=3.3901e+00 ppl=29.67 best_loss=3.5026e+00 best_ppl=33.20                                              
Epoch 11 - |param|=3.24e+02 |g_param|=2.86e+05 loss=3.1924e+00 ppl=24.35                                                
Validation - loss=3.2881e+00 ppl=26.79 best_loss=3.3901e+00 best_ppl=29.67                                              
Epoch 12 - |param|=3.24e+02 |g_param|=1.91e+05 loss=3.0855e+00 ppl=21.88                                                
Validation - loss=3.1868e+00 ppl=24.21 best_loss=3.2881e+00 best_ppl=26.79                                              
Epoch 13 - |param|=3.25e+02 |g_param|=2.92e+05 loss=2.9961e+00 ppl=20.01                                                
Validation - loss=3.1000e+00 ppl=22.20 best_loss=3.1868e+00 best_ppl=24.21                                              
Epoch 14 - |param|=3.25e+02 |g_param|=2.43e+05 loss=2.9657e+00 ppl=19.41                                                
Validation - loss=3.0171e+00 ppl=20.43 best_loss=3.1000e+00 best_ppl=22.20                                              
Epoch 15 - |param|=3.25e+02 |g_param|=2.06e+05 loss=2.9336e+00 ppl=18.79                                                
Validation - loss=2.9440e+00 ppl=18.99 best_loss=3.0171e+00 best_ppl=20.43                                              
Epoch 16 - |param|=3.25e+02 |g_param|=3.54e+05 loss=2.8371e+00 ppl=17.07                                                
Validation - loss=2.8711e+00 ppl=17.66 best_loss=2.9440e+00 best_ppl=18.99                                              
Epoch 17 - |param|=3.25e+02 |g_param|=2.93e+05 loss=2.7649e+00 ppl=15.88                                                
Validation - loss=2.8016e+00 ppl=16.47 best_loss=2.8711e+00 best_ppl=17.66                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.49e+05 loss=2.6774e+00 ppl=14.55                                                
Validation - loss=2.7366e+00 ppl=15.43 best_loss=2.8016e+00 best_ppl=16.47                                              
Epoch 19 - |param|=3.25e+02 |g_param|=3.14e+05 loss=2.6352e+00 ppl=13.95                                                
Validation - loss=2.6721e+00 ppl=14.47 best_loss=2.7366e+00 best_ppl=15.43                                              
Epoch 20 - |param|=3.25e+02 |g_param|=2.85e+05 loss=2.5652e+00 ppl=13.00                                                
Validation - loss=2.6123e+00 ppl=13.63 best_loss=2.6721e+00 best_ppl=14.47                                              
Epoch 21 - |param|=3.25e+02 |g_param|=2.87e+05 loss=2.5878e+00 ppl=13.30                                                
Validation - loss=2.5529e+00 ppl=12.84 best_loss=2.6123e+00 best_ppl=13.63                                              
Epoch 22 - |param|=3.25e+02 |g_param|=2.81e+05 loss=2.4957e+00 ppl=12.13                                                
Validation - loss=2.4930e+00 ppl=12.10 best_loss=2.5529e+00 best_ppl=12.84                                              
Epoch 23 - |param|=3.25e+02 |g_param|=4.46e+05 loss=2.3569e+00 ppl=10.56                                                
Validation - loss=2.4440e+00 ppl=11.52 best_loss=2.4930e+00 best_ppl=12.10                                              
Epoch 24 - |param|=3.25e+02 |g_param|=2.99e+05 loss=2.3819e+00 ppl=10.82                                                
Validation - loss=2.3992e+00 ppl=11.01 best_loss=2.4440e+00 best_ppl=11.52                                              
Epoch 25 - |param|=3.25e+02 |g_param|=3.11e+05 loss=2.2924e+00 ppl=9.90                                                 
Validation - loss=2.3409e+00 ppl=10.39 best_loss=2.3992e+00 best_ppl=11.01                                              
Epoch 26 - |param|=3.25e+02 |g_param|=2.68e+05 loss=2.3106e+00 ppl=10.08                                                
Validation - loss=2.2895e+00 ppl=9.87 best_loss=2.3409e+00 best_ppl=10.39                                               
Epoch 27 - |param|=3.25e+02 |g_param|=3.68e+05 loss=2.2536e+00 ppl=9.52                                                 
Validation - loss=2.2380e+00 ppl=9.37 best_loss=2.2895e+00 best_ppl=9.87                                                
Epoch 28 - |param|=3.25e+02 |g_param|=4.60e+05 loss=2.2429e+00 ppl=9.42                                                 
Validation - loss=2.1980e+00 ppl=9.01 best_loss=2.2380e+00 best_ppl=9.37                                                
Epoch 29 - |param|=3.25e+02 |g_param|=3.06e+05 loss=2.1869e+00 ppl=8.91                                                 
Validation - loss=2.1614e+00 ppl=8.68 best_loss=2.1980e+00 best_ppl=9.01                                                
Epoch 30 - |param|=3.25e+02 |g_param|=5.27e+05 loss=2.1895e+00 ppl=8.93                                                 
Validation - loss=2.1229e+00 ppl=8.36 best_loss=2.1614e+00 best_ppl=8.68                                                
Epoch 31 - |param|=3.25e+02 |g_param|=3.59e+05 loss=2.1051e+00 ppl=8.21                                                 
Validation - loss=2.0748e+00 ppl=7.96 best_loss=2.1229e+00 best_ppl=8.36                                                
Epoch 32 - |param|=3.25e+02 |g_param|=6.16e+05 loss=2.0869e+00 ppl=8.06                                                 
Validation - loss=2.0443e+00 ppl=7.72 best_loss=2.0748e+00 best_ppl=7.96                                                
Epoch 33 - |param|=3.25e+02 |g_param|=4.83e+05 loss=2.0926e+00 ppl=8.11                                                 
Validation - loss=1.9862e+00 ppl=7.29 best_loss=2.0443e+00 best_ppl=7.72                                                
Epoch 34 - |param|=3.25e+02 |g_param|=4.40e+05 loss=1.9750e+00 ppl=7.21                                                 
Validation - loss=1.9587e+00 ppl=7.09 best_loss=1.9862e+00 best_ppl=7.29                                                
Epoch 35 - |param|=3.26e+02 |g_param|=6.58e+05 loss=1.9899e+00 ppl=7.31                                                 
Validation - loss=1.9519e+00 ppl=7.04 best_loss=1.9587e+00 best_ppl=7.09                                                
Epoch 36 - |param|=3.26e+02 |g_param|=4.38e+05 loss=1.9886e+00 ppl=7.31                                                 
Validation - loss=1.8902e+00 ppl=6.62 best_loss=1.9519e+00 best_ppl=7.04                                                
Epoch 37 - |param|=3.26e+02 |g_param|=4.12e+05 loss=2.0437e+00 ppl=7.72                                                 
Validation - loss=1.8599e+00 ppl=6.42 best_loss=1.8902e+00 best_ppl=6.62                                                
Epoch 38 - |param|=3.26e+02 |g_param|=4.59e+05 loss=1.9544e+00 ppl=7.06                                                 
Validation - loss=1.8283e+00 ppl=6.22 best_loss=1.8599e+00 best_ppl=6.42                                                
Epoch 39 - |param|=3.26e+02 |g_param|=3.61e+05 loss=1.8806e+00 ppl=6.56                                                 
Validation - loss=1.7932e+00 ppl=6.01 best_loss=1.8283e+00 best_ppl=6.22                                                
Epoch 40 - |param|=3.26e+02 |g_param|=4.76e+05 loss=1.8758e+00 ppl=6.53                                                 
Validation - loss=1.7551e+00 ppl=5.78 best_loss=1.7932e+00 best_ppl=6.01                                                
Epoch 41 - |param|=3.26e+02 |g_param|=3.54e+05 loss=1.7728e+00 ppl=5.89                                                 
Validation - loss=1.7243e+00 ppl=5.61 best_loss=1.7551e+00 best_ppl=5.78                                                
Epoch 42 - |param|=3.26e+02 |g_param|=4.41e+05 loss=1.7279e+00 ppl=5.63                                                 
Validation - loss=1.6970e+00 ppl=5.46 best_loss=1.7243e+00 best_ppl=5.61                                                
Epoch 43 - |param|=3.26e+02 |g_param|=4.49e+05 loss=1.7043e+00 ppl=5.50                                                 
Validation - loss=1.6805e+00 ppl=5.37 best_loss=1.6970e+00 best_ppl=5.46                                                
Epoch 44 - |param|=3.26e+02 |g_param|=3.94e+05 loss=1.7445e+00 ppl=5.72                                                 
Validation - loss=1.6445e+00 ppl=5.18 best_loss=1.6805e+00 best_ppl=5.37                                                
Epoch 45 - |param|=3.26e+02 |g_param|=4.14e+05 loss=1.7800e+00 ppl=5.93                                                 
Validation - loss=1.6174e+00 ppl=5.04 best_loss=1.6445e+00 best_ppl=5.18                                                
Epoch 46 - |param|=3.26e+02 |g_param|=4.56e+05 loss=1.6352e+00 ppl=5.13                                                 
Validation - loss=1.5927e+00 ppl=4.92 best_loss=1.6174e+00 best_ppl=5.04                                                
Epoch 47 - |param|=3.26e+02 |g_param|=4.47e+05 loss=1.6432e+00 ppl=5.17                                                 
Validation - loss=1.5625e+00 ppl=4.77 best_loss=1.5927e+00 best_ppl=4.92                                                
Epoch 48 - |param|=3.26e+02 |g_param|=6.34e+05 loss=1.7302e+00 ppl=5.64                                                 
Validation - loss=1.5478e+00 ppl=4.70 best_loss=1.5625e+00 best_ppl=4.77                                                
Epoch 49 - |param|=3.26e+02 |g_param|=5.48e+05 loss=1.6169e+00 ppl=5.04                                                 
Validation - loss=1.5422e+00 ppl=4.67 best_loss=1.5478e+00 best_ppl=4.70                                                
Epoch 50 - |param|=3.26e+02 |g_param|=6.91e+05 loss=1.6792e+00 ppl=5.36                                                 
Validation - loss=1.5041e+00 ppl=4.50 best_loss=1.5422e+00 best_ppl=4.67                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.43e+05 loss=1.5862e+00 ppl=4.88                                                 
Validation - loss=1.4788e+00 ppl=4.39 best_loss=1.5041e+00 best_ppl=4.50                                                
Epoch 52 - |param|=3.26e+02 |g_param|=4.08e+05 loss=1.5274e+00 ppl=4.61                                                 
Validation - loss=1.4703e+00 ppl=4.35 best_loss=1.4788e+00 best_ppl=4.39                                                
Epoch 53 - |param|=3.26e+02 |g_param|=7.77e+05 loss=1.6009e+00 ppl=4.96                                                 
Validation - loss=1.4823e+00 ppl=4.40 best_loss=1.4703e+00 best_ppl=4.35                                                
Epoch 54 - |param|=3.26e+02 |g_param|=6.86e+05 loss=1.6101e+00 ppl=5.00                                                 
Validation - loss=1.4605e+00 ppl=4.31 best_loss=1.4703e+00 best_ppl=4.35                                                
Epoch 55 - |param|=3.26e+02 |g_param|=5.47e+05 loss=1.4706e+00 ppl=4.35                                                 
Validation - loss=1.4088e+00 ppl=4.09 best_loss=1.4605e+00 best_ppl=4.31                                                
Epoch 56 - |param|=3.26e+02 |g_param|=6.29e+05 loss=1.4443e+00 ppl=4.24                                                 
Validation - loss=1.3888e+00 ppl=4.01 best_loss=1.4088e+00 best_ppl=4.09                                                
Epoch 57 - |param|=3.26e+02 |g_param|=4.76e+05 loss=1.5221e+00 ppl=4.58                                                 
Validation - loss=1.3778e+00 ppl=3.97 best_loss=1.3888e+00 best_ppl=4.01                                                
Epoch 58 - |param|=3.26e+02 |g_param|=6.06e+05 loss=1.4275e+00 ppl=4.17                                                 
Validation - loss=1.3699e+00 ppl=3.94 best_loss=1.3778e+00 best_ppl=3.97                                                
Epoch 59 - |param|=3.26e+02 |g_param|=5.99e+05 loss=1.4429e+00 ppl=4.23                                                 
Validation - loss=1.3539e+00 ppl=3.87 best_loss=1.3699e+00 best_ppl=3.94                                                
Epoch 60 - |param|=3.26e+02 |g_param|=2.59e+05 loss=1.4621e+00 ppl=4.31                                                 
Validation - loss=1.3375e+00 ppl=3.81 best_loss=1.3539e+00 best_ppl=3.87                                                
Epoch 61 - |param|=3.26e+02 |g_param|=3.45e+05 loss=1.5172e+00 ppl=4.56                                                 
Validation - loss=1.3293e+00 ppl=3.78 best_loss=1.3375e+00 best_ppl=3.81                                                
Epoch 62 - |param|=3.26e+02 |g_param|=3.38e+05 loss=1.4872e+00 ppl=4.42                                                 
Validation - loss=1.2987e+00 ppl=3.66 best_loss=1.3293e+00 best_ppl=3.78                                                
Epoch 63 - |param|=3.26e+02 |g_param|=2.99e+05 loss=1.3853e+00 ppl=4.00                                                 
Validation - loss=1.2969e+00 ppl=3.66 best_loss=1.2987e+00 best_ppl=3.66                                                
Epoch 64 - |param|=3.26e+02 |g_param|=7.21e+05 loss=1.4353e+00 ppl=4.20                                                 
Validation - loss=1.2792e+00 ppl=3.59 best_loss=1.2969e+00 best_ppl=3.66                                                
Epoch 65 - |param|=3.26e+02 |g_param|=2.84e+05 loss=1.4378e+00 ppl=4.21                                                 
Validation - loss=1.2784e+00 ppl=3.59 best_loss=1.2792e+00 best_ppl=3.59                                                
Epoch 66 - |param|=3.26e+02 |g_param|=3.39e+05 loss=1.4076e+00 ppl=4.09                                                 
Validation - loss=1.2539e+00 ppl=3.50 best_loss=1.2784e+00 best_ppl=3.59                                                
Epoch 67 - |param|=3.26e+02 |g_param|=3.92e+05 loss=1.3955e+00 ppl=4.04                                                 
Validation - loss=1.2579e+00 ppl=3.52 best_loss=1.2539e+00 best_ppl=3.50                                                
Epoch 68 - |param|=3.26e+02 |g_param|=4.18e+05 loss=1.3956e+00 ppl=4.04                                                 
Validation - loss=1.2474e+00 ppl=3.48 best_loss=1.2539e+00 best_ppl=3.50                                                
Epoch 69 - |param|=3.26e+02 |g_param|=3.26e+05 loss=1.3520e+00 ppl=3.87                                                 
Validation - loss=1.2216e+00 ppl=3.39 best_loss=1.2474e+00 best_ppl=3.48                                                
Epoch 70 - |param|=3.26e+02 |g_param|=4.13e+05 loss=1.3078e+00 ppl=3.70                                                 
Validation - loss=1.2104e+00 ppl=3.35 best_loss=1.2216e+00 best_ppl=3.39                                                
Epoch 71 - |param|=3.26e+02 |g_param|=3.24e+05 loss=1.4044e+00 ppl=4.07                                                 
Validation - loss=1.1994e+00 ppl=3.32 best_loss=1.2104e+00 best_ppl=3.35                                                
Epoch 72 - |param|=3.26e+02 |g_param|=3.32e+05 loss=1.2974e+00 ppl=3.66                                                 
Validation - loss=1.1976e+00 ppl=3.31 best_loss=1.1994e+00 best_ppl=3.32                                                
Epoch 73 - |param|=3.26e+02 |g_param|=3.36e+05 loss=1.2837e+00 ppl=3.61                                                 
Validation - loss=1.1959e+00 ppl=3.31 best_loss=1.1976e+00 best_ppl=3.31                                                
Epoch 74 - |param|=3.26e+02 |g_param|=2.55e+05 loss=1.2805e+00 ppl=3.60                                                 
Validation - loss=1.1695e+00 ppl=3.22 best_loss=1.1959e+00 best_ppl=3.31                                                
Epoch 75 - |param|=3.26e+02 |g_param|=2.55e+05 loss=1.2302e+00 ppl=3.42                                                 
Validation - loss=1.1699e+00 ppl=3.22 best_loss=1.1695e+00 best_ppl=3.22                                                
Epoch 76 - |param|=3.26e+02 |g_param|=3.93e+05 loss=1.3106e+00 ppl=3.71                                                 
Validation - loss=1.1749e+00 ppl=3.24 best_loss=1.1695e+00 best_ppl=3.22                                                
Epoch 77 - |param|=3.26e+02 |g_param|=3.94e+05 loss=1.2865e+00 ppl=3.62                                                 
Validation - loss=1.1904e+00 ppl=3.29 best_loss=1.1695e+00 best_ppl=3.22                                                
Epoch 78 - |param|=3.26e+02 |g_param|=2.83e+05 loss=1.2991e+00 ppl=3.67                                                 
Validation - loss=1.1463e+00 ppl=3.15 best_loss=1.1695e+00 best_ppl=3.22                                                
Epoch 79 - |param|=3.26e+02 |g_param|=3.54e+05 loss=1.2214e+00 ppl=3.39                                                 
Validation - loss=1.1519e+00 ppl=3.16 best_loss=1.1463e+00 best_ppl=3.15                                                
Epoch 80 - |param|=3.26e+02 |g_param|=4.04e+05 loss=1.2395e+00 ppl=3.45                                                 
Validation - loss=1.1831e+00 ppl=3.26 best_loss=1.1463e+00 best_ppl=3.15                                                
Epoch 81 - |param|=3.26e+02 |g_param|=4.45e+05 loss=1.2125e+00 ppl=3.36                                                 
Validation - loss=1.1293e+00 ppl=3.09 best_loss=1.1463e+00 best_ppl=3.15                                                
Epoch 82 - |param|=3.26e+02 |g_param|=5.07e+05 loss=1.2235e+00 ppl=3.40                                                 
Validation - loss=1.1152e+00 ppl=3.05 best_loss=1.1293e+00 best_ppl=3.09                                                
Epoch 83 - |param|=3.26e+02 |g_param|=4.22e+05 loss=1.2449e+00 ppl=3.47                                                 
Validation - loss=1.1134e+00 ppl=3.04 best_loss=1.1152e+00 best_ppl=3.05                                                
Epoch 84 - |param|=3.26e+02 |g_param|=4.17e+05 loss=1.2316e+00 ppl=3.43                                                 
Validation - loss=1.1002e+00 ppl=3.00 best_loss=1.1134e+00 best_ppl=3.04                                                
Epoch 85 - |param|=3.26e+02 |g_param|=4.18e+05 loss=1.1396e+00 ppl=3.13                                                 
Validation - loss=1.0908e+00 ppl=2.98 best_loss=1.1002e+00 best_ppl=3.00                                                
Epoch 86 - |param|=3.26e+02 |g_param|=4.43e+05 loss=1.1586e+00 ppl=3.19                                                 
Validation - loss=1.0887e+00 ppl=2.97 best_loss=1.0908e+00 best_ppl=2.98                                                
Epoch 87 - |param|=3.26e+02 |g_param|=3.83e+05 loss=1.1622e+00 ppl=3.20                                                 
Validation - loss=1.0886e+00 ppl=2.97 best_loss=1.0887e+00 best_ppl=2.97                                                
Epoch 88 - |param|=3.26e+02 |g_param|=4.23e+05 loss=1.1502e+00 ppl=3.16                                                 
Validation - loss=1.0653e+00 ppl=2.90 best_loss=1.0886e+00 best_ppl=2.97                                                
Epoch 89 - |param|=3.26e+02 |g_param|=2.81e+05 loss=1.0858e+00 ppl=2.96                                                 
Validation - loss=1.0739e+00 ppl=2.93 best_loss=1.0653e+00 best_ppl=2.90                                                
Epoch 90 - |param|=3.26e+02 |g_param|=3.49e+05 loss=1.1109e+00 ppl=3.04                                                 
Validation - loss=1.0605e+00 ppl=2.89 best_loss=1.0653e+00 best_ppl=2.90                                                
Epoch 91 - |param|=3.26e+02 |g_param|=4.47e+05 loss=1.1896e+00 ppl=3.29                                                 
Validation - loss=1.1210e+00 ppl=3.07 best_loss=1.0605e+00 best_ppl=2.89                                                
Epoch 92 - |param|=3.26e+02 |g_param|=4.08e+05 loss=1.1127e+00 ppl=3.04                                                 
Validation - loss=1.0561e+00 ppl=2.88 best_loss=1.0605e+00 best_ppl=2.89                                                
Epoch 93 - |param|=3.26e+02 |g_param|=2.60e+05 loss=1.0975e+00 ppl=3.00                                                 
Validation - loss=1.0496e+00 ppl=2.86 best_loss=1.0561e+00 best_ppl=2.88                                                
Epoch 94 - |param|=3.26e+02 |g_param|=5.31e+05 loss=1.1386e+00 ppl=3.12                                                 
Validation - loss=1.0438e+00 ppl=2.84 best_loss=1.0496e+00 best_ppl=2.86                                                
Epoch 95 - |param|=3.26e+02 |g_param|=3.03e+05 loss=1.0642e+00 ppl=2.90                                                 
Validation - loss=1.0339e+00 ppl=2.81 best_loss=1.0438e+00 best_ppl=2.84                                                
Epoch 96 - |param|=3.26e+02 |g_param|=3.30e+05 loss=1.1301e+00 ppl=3.10                                                 
Validation - loss=1.0368e+00 ppl=2.82 best_loss=1.0339e+00 best_ppl=2.81                                                
Epoch 97 - |param|=3.27e+02 |g_param|=2.79e+05 loss=1.1444e+00 ppl=3.14                                                 
Validation - loss=1.0264e+00 ppl=2.79 best_loss=1.0339e+00 best_ppl=2.81                                                
Epoch 98 - |param|=3.27e+02 |g_param|=5.24e+05 loss=1.0946e+00 ppl=2.99                                                 
Validation - loss=1.0374e+00 ppl=2.82 best_loss=1.0264e+00 best_ppl=2.79                                                
Epoch 99 - |param|=3.27e+02 |g_param|=4.04e+05 loss=1.0988e+00 ppl=3.00                                                 
Validation - loss=1.0039e+00 ppl=2.73 best_loss=1.0264e+00 best_ppl=2.79                                                
Epoch 100 - |param|=3.27e+02 |g_param|=3.94e+05 loss=1.0606e+00 ppl=2.89                                                
Validation - loss=1.0086e+00 ppl=2.74 best_loss=1.0039e+00 best_ppl=2.73                                                

real	51m12.475s
user	51m3.867s
sys	0m8.963s
(simple-nmt) ye@:~/exp/simple-nmt$ 

```

myrk, Transformer baseline testing/evaluation  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: myrk-transformer-model.01.5.78-322.76.5.80-330.12.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.9/0.0/0.0/0.0 (BP=0.215, ratio=0.394, hyp_len=9125, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.02.4.96-143.22.5.00-148.26.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.4/2.8/0.0/0.0 (BP=0.593, ratio=0.657, hyp_len=15215, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.03.4.50-89.63.4.59-98.49.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 30.4/4.4/0.0/0.0 (BP=0.592, ratio=0.656, hyp_len=15187, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.04.4.21-67.41.4.32-75.55.pth
BLEU = 1.66, 33.4/8.7/1.3/0.1 (BP=0.723, ratio=0.755, hyp_len=17493, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.05.4.00-54.62.4.12-61.64.pth
BLEU = 1.96, 32.6/9.8/1.4/0.1 (BP=0.843, ratio=0.854, hyp_len=19782, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.06.3.84-46.51.3.94-51.39.pth
BLEU = 1.98, 24.9/8.0/1.4/0.1 (BP=1.000, ratio=1.252, hyp_len=28985, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.07.3.67-39.41.3.78-43.88.pth
BLEU = 3.02, 26.2/9.0/1.9/0.2 (BP=1.000, ratio=1.269, hyp_len=29400, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.08.3.53-34.18.3.63-37.90.pth
BLEU = 3.16, 22.1/7.9/1.9/0.3 (BP=1.000, ratio=1.586, hyp_len=36733, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.09.3.43-30.74.3.50-33.20.pth
BLEU = 3.73, 23.2/8.5/2.3/0.4 (BP=1.000, ratio=1.585, hyp_len=36702, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.100.1.06-2.89.1.01-2.74.pth
BLEU = 55.64, 77.5/62.1/49.9/39.9 (BP=1.000, ratio=1.067, hyp_len=24705, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.10.3.32-27.70.3.39-29.67.pth
BLEU = 5.26, 28.7/11.0/3.2/0.8 (BP=1.000, ratio=1.342, hyp_len=31087, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.11.3.19-24.35.3.29-26.79.pth
BLEU = 5.20, 26.3/10.3/3.2/0.8 (BP=1.000, ratio=1.550, hyp_len=35896, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.12.3.09-21.88.3.19-24.21.pth
BLEU = 7.58, 34.4/14.1/4.8/1.4 (BP=1.000, ratio=1.201, hyp_len=27812, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.13.3.00-20.01.3.10-22.20.pth
BLEU = 7.26, 31.1/13.0/4.7/1.5 (BP=1.000, ratio=1.403, hyp_len=32499, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.14.2.97-19.41.3.02-20.43.pth
BLEU = 9.39, 37.2/16.2/6.2/2.1 (BP=1.000, ratio=1.202, hyp_len=27840, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.15.2.93-18.79.2.94-18.99.pth
BLEU = 9.63, 36.6/16.2/6.4/2.3 (BP=1.000, ratio=1.253, hyp_len=29027, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.16.2.84-17.07.2.87-17.66.pth
BLEU = 12.09, 42.6/19.6/8.1/3.1 (BP=1.000, ratio=1.121, hyp_len=25970, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.17.2.76-15.88.2.80-16.47.pth
BLEU = 11.95, 41.2/19.1/8.1/3.2 (BP=1.000, ratio=1.193, hyp_len=27628, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.18.2.68-14.55.2.74-15.43.pth
BLEU = 12.70, 40.8/19.7/8.8/3.7 (BP=1.000, ratio=1.240, hyp_len=28723, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.19.2.64-13.95.2.67-14.47.pth
BLEU = 13.51, 42.1/20.6/9.4/4.1 (BP=1.000, ratio=1.228, hyp_len=28445, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.20.2.57-13.00.2.61-13.63.pth
BLEU = 15.39, 46.1/23.0/10.9/4.9 (BP=1.000, ratio=1.128, hyp_len=26130, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.21.2.59-13.30.2.55-12.84.pth
BLEU = 14.94, 43.6/22.1/10.7/4.8 (BP=1.000, ratio=1.234, hyp_len=28569, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.22.2.50-12.13.2.49-12.10.pth
BLEU = 17.99, 49.9/26.1/13.0/6.2 (BP=1.000, ratio=1.094, hyp_len=25337, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.23.2.36-10.56.2.44-11.52.pth
BLEU = 19.39, 52.2/27.7/14.2/6.9 (BP=1.000, ratio=1.053, hyp_len=24379, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.24.2.38-10.82.2.40-11.01.pth
BLEU = 18.32, 49.0/26.2/13.5/6.5 (BP=1.000, ratio=1.138, hyp_len=26366, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.25.2.29-9.90.2.34-10.39.pth
BLEU = 19.60, 50.3/27.7/14.5/7.3 (BP=1.000, ratio=1.134, hyp_len=26265, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.26.2.31-10.08.2.29-9.87.pth
BLEU = 20.52, 51.3/28.6/15.3/7.9 (BP=1.000, ratio=1.129, hyp_len=26152, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.27.2.25-9.52.2.24-9.37.pth
BLEU = 21.66, 53.1/29.9/16.3/8.5 (BP=1.000, ratio=1.110, hyp_len=25706, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.28.2.24-9.42.2.20-9.01.pth
BLEU = 22.42, 53.0/30.4/17.0/9.2 (BP=1.000, ratio=1.126, hyp_len=26071, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.29.2.19-8.91.2.16-8.68.pth
BLEU = 24.72, 56.8/33.2/18.9/10.5 (BP=1.000, ratio=1.055, hyp_len=24428, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth
BLEU = 25.29, 57.4/33.7/19.5/10.9 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.31.2.11-8.21.2.07-7.96.pth
BLEU = 25.75, 57.5/34.2/19.9/11.2 (BP=1.000, ratio=1.069, hyp_len=24748, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.32.2.09-8.06.2.04-7.72.pth
BLEU = 24.36, 53.5/32.2/18.9/10.8 (BP=1.000, ratio=1.173, hyp_len=27175, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.33.2.09-8.11.1.99-7.29.pth
BLEU = 27.84, 59.0/36.0/21.7/13.0 (BP=1.000, ratio=1.074, hyp_len=24884, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.34.1.98-7.21.1.96-7.09.pth
BLEU = 26.92, 56.8/35.0/21.2/12.5 (BP=1.000, ratio=1.124, hyp_len=26030, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.35.1.99-7.31.1.95-7.04.pth
BLEU = 27.70, 57.7/35.9/21.9/13.0 (BP=1.000, ratio=1.130, hyp_len=26182, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.36.1.99-7.31.1.89-6.62.pth
BLEU = 29.89, 59.8/37.8/23.8/14.8 (BP=1.000, ratio=1.093, hyp_len=25307, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.37.2.04-7.72.1.86-6.42.pth
BLEU = 30.45, 60.5/38.5/24.3/15.2 (BP=1.000, ratio=1.097, hyp_len=25413, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.38.1.95-7.06.1.83-6.22.pth
BLEU = 31.36, 61.5/39.6/25.2/15.8 (BP=1.000, ratio=1.090, hyp_len=25244, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.39.1.88-6.56.1.79-6.01.pth
BLEU = 32.86, 62.9/40.9/26.6/17.0 (BP=1.000, ratio=1.073, hyp_len=24851, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.40.1.88-6.53.1.76-5.78.pth
BLEU = 33.82, 63.6/41.9/27.5/17.9 (BP=1.000, ratio=1.075, hyp_len=24904, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.41.1.77-5.89.1.72-5.61.pth
BLEU = 34.33, 63.9/42.2/27.9/18.4 (BP=1.000, ratio=1.071, hyp_len=24808, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.42.1.73-5.63.1.70-5.46.pth
BLEU = 34.83, 63.8/42.8/28.6/18.9 (BP=1.000, ratio=1.091, hyp_len=25272, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.43.1.70-5.50.1.68-5.37.pth
BLEU = 35.63, 65.0/43.7/29.3/19.4 (BP=1.000, ratio=1.066, hyp_len=24685, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.44.1.74-5.72.1.64-5.18.pth
BLEU = 37.28, 66.7/45.4/30.8/20.7 (BP=1.000, ratio=1.051, hyp_len=24333, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.45.1.78-5.93.1.62-5.04.pth
BLEU = 38.77, 68.3/46.9/32.1/21.9 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.46.1.64-5.13.1.59-4.92.pth
BLEU = 38.66, 67.8/46.9/32.1/21.9 (BP=1.000, ratio=1.053, hyp_len=24393, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.47.1.64-5.17.1.56-4.77.pth
BLEU = 39.51, 68.2/47.3/33.0/22.9 (BP=1.000, ratio=1.053, hyp_len=24386, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.48.1.73-5.64.1.55-4.70.pth
BLEU = 39.63, 68.2/47.6/33.1/23.0 (BP=1.000, ratio=1.058, hyp_len=24506, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.49.1.62-5.04.1.54-4.67.pth
BLEU = 38.85, 67.3/47.0/32.5/22.2 (BP=1.000, ratio=1.082, hyp_len=25070, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.50.1.68-5.36.1.50-4.50.pth
BLEU = 41.74, 70.0/49.5/35.1/24.9 (BP=1.000, ratio=1.041, hyp_len=24121, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.51.1.59-4.88.1.48-4.39.pth
BLEU = 42.42, 70.5/50.3/35.9/25.4 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.52.1.53-4.61.1.47-4.35.pth
BLEU = 40.71, 67.8/48.4/34.4/24.3 (BP=1.000, ratio=1.094, hyp_len=25335, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.53.1.60-4.96.1.48-4.40.pth
BLEU = 40.39, 67.8/48.5/34.2/23.6 (BP=1.000, ratio=1.100, hyp_len=25478, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.54.1.61-5.00.1.46-4.31.pth
BLEU = 41.01, 68.3/49.1/34.8/24.2 (BP=1.000, ratio=1.096, hyp_len=25373, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.55.1.47-4.35.1.41-4.09.pth
BLEU = 44.57, 71.7/52.1/38.1/27.7 (BP=1.000, ratio=1.042, hyp_len=24131, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.56.1.44-4.24.1.39-4.01.pth
BLEU = 44.62, 71.4/52.2/38.2/27.8 (BP=1.000, ratio=1.054, hyp_len=24422, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.57.1.52-4.58.1.38-3.97.pth
BLEU = 44.95, 71.6/52.5/38.5/28.2 (BP=1.000, ratio=1.055, hyp_len=24427, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.58.1.43-4.17.1.37-3.94.pth
BLEU = 46.30, 73.4/53.8/39.7/29.3 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.59.1.44-4.23.1.35-3.87.pth
BLEU = 47.52, 74.3/55.0/40.9/30.5 (BP=1.000, ratio=1.020, hyp_len=23621, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.60.1.46-4.31.1.34-3.81.pth
BLEU = 45.81, 72.0/53.4/39.5/29.0 (BP=1.000, ratio=1.067, hyp_len=24705, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.61.1.52-4.56.1.33-3.78.pth
BLEU = 48.18, 74.5/55.5/41.6/31.3 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.62.1.49-4.42.1.30-3.66.pth
BLEU = 46.84, 72.8/54.1/40.5/30.2 (BP=1.000, ratio=1.059, hyp_len=24529, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.63.1.39-4.00.1.30-3.66.pth
BLEU = 45.78, 71.5/53.3/39.6/29.1 (BP=1.000, ratio=1.082, hyp_len=25057, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.64.1.44-4.20.1.28-3.59.pth
BLEU = 48.56, 74.2/55.7/42.2/31.9 (BP=1.000, ratio=1.040, hyp_len=24087, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.65.1.44-4.21.1.28-3.59.pth
BLEU = 47.97, 73.7/55.4/41.6/31.1 (BP=1.000, ratio=1.053, hyp_len=24380, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.66.1.41-4.09.1.25-3.50.pth
BLEU = 49.26, 74.6/56.5/42.9/32.5 (BP=1.000, ratio=1.044, hyp_len=24185, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.67.1.40-4.04.1.26-3.52.pth
BLEU = 48.25, 73.9/55.9/42.0/31.2 (BP=1.000, ratio=1.059, hyp_len=24517, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.68.1.40-4.04.1.25-3.48.pth
BLEU = 48.24, 73.6/55.8/42.1/31.3 (BP=1.000, ratio=1.066, hyp_len=24697, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.69.1.35-3.87.1.22-3.39.pth
BLEU = 50.50, 75.7/57.6/44.1/33.8 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.70.1.31-3.70.1.21-3.35.pth
BLEU = 49.16, 74.0/56.5/43.0/32.5 (BP=1.000, ratio=1.064, hyp_len=24644, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.71.1.40-4.07.1.20-3.32.pth
BLEU = 50.22, 75.3/57.4/44.0/33.5 (BP=1.000, ratio=1.050, hyp_len=24310, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.72.1.30-3.66.1.20-3.31.pth
BLEU = 51.01, 76.0/58.3/44.8/34.1 (BP=1.000, ratio=1.035, hyp_len=23969, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.73.1.28-3.61.1.20-3.31.pth
BLEU = 49.42, 74.5/57.0/43.3/32.4 (BP=1.000, ratio=1.065, hyp_len=24655, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.74.1.28-3.60.1.17-3.22.pth
BLEU = 50.24, 74.7/57.4/44.1/33.7 (BP=1.000, ratio=1.065, hyp_len=24660, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.75.1.23-3.42.1.17-3.22.pth
BLEU = 50.76, 75.2/57.9/44.6/34.2 (BP=1.000, ratio=1.057, hyp_len=24474, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.76.1.31-3.71.1.17-3.24.pth
BLEU = 49.40, 73.5/56.7/43.5/32.8 (BP=1.000, ratio=1.091, hyp_len=25257, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.77.1.29-3.62.1.19-3.29.pth
BLEU = 49.22, 73.5/56.8/43.4/32.4 (BP=1.000, ratio=1.091, hyp_len=25262, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.78.1.30-3.67.1.15-3.15.pth
BLEU = 51.03, 75.1/58.3/45.1/34.4 (BP=1.000, ratio=1.069, hyp_len=24761, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.79.1.22-3.39.1.15-3.16.pth
BLEU = 51.40, 75.7/58.8/45.4/34.6 (BP=1.000, ratio=1.060, hyp_len=24540, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.80.1.24-3.45.1.18-3.26.pth
BLEU = 50.35, 74.9/58.0/44.4/33.3 (BP=1.000, ratio=1.072, hyp_len=24837, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.81.1.21-3.36.1.13-3.09.pth
BLEU = 54.65, 78.2/61.2/48.5/38.5 (BP=1.000, ratio=1.022, hyp_len=23669, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.82.1.22-3.40.1.12-3.05.pth
BLEU = 53.84, 77.6/60.7/47.7/37.4 (BP=1.000, ratio=1.035, hyp_len=23967, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.83.1.24-3.47.1.11-3.04.pth
BLEU = 53.41, 76.8/60.1/47.3/37.3 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.84.1.23-3.43.1.10-3.00.pth
BLEU = 52.46, 76.0/59.4/46.5/36.0 (BP=1.000, ratio=1.062, hyp_len=24598, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.85.1.14-3.13.1.09-2.98.pth
BLEU = 53.48, 77.1/60.5/47.6/36.9 (BP=1.000, ratio=1.050, hyp_len=24319, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.86.1.16-3.19.1.09-2.97.pth
BLEU = 53.60, 77.1/60.8/47.7/36.9 (BP=1.000, ratio=1.050, hyp_len=24311, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.87.1.16-3.20.1.09-2.97.pth
BLEU = 53.11, 76.6/60.1/47.2/36.6 (BP=1.000, ratio=1.058, hyp_len=24514, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.88.1.15-3.16.1.07-2.90.pth
BLEU = 55.92, 78.8/62.5/49.9/39.8 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.89.1.09-2.96.1.07-2.93.pth
BLEU = 54.22, 77.6/61.3/48.3/37.7 (BP=1.000, ratio=1.049, hyp_len=24295, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.90.1.11-3.04.1.06-2.89.pth
BLEU = 54.80, 77.8/61.5/48.9/38.5 (BP=1.000, ratio=1.049, hyp_len=24286, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.91.1.19-3.29.1.12-3.07.pth
BLEU = 51.42, 75.2/59.1/45.7/34.4 (BP=1.000, ratio=1.087, hyp_len=25182, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.92.1.11-3.04.1.06-2.88.pth
BLEU = 54.00, 76.8/60.7/48.1/37.9 (BP=1.000, ratio=1.065, hyp_len=24661, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.93.1.10-3.00.1.05-2.86.pth
BLEU = 55.79, 78.6/62.6/49.9/39.4 (BP=1.000, ratio=1.040, hyp_len=24078, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.94.1.14-3.12.1.04-2.84.pth
BLEU = 56.59, 78.9/62.9/50.7/40.7 (BP=1.000, ratio=1.033, hyp_len=23931, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.95.1.06-2.90.1.03-2.81.pth
BLEU = 56.35, 79.0/63.0/50.4/40.1 (BP=1.000, ratio=1.036, hyp_len=23997, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.96.1.13-3.10.1.04-2.82.pth
BLEU = 54.22, 77.3/61.4/48.4/37.6 (BP=1.000, ratio=1.066, hyp_len=24680, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.97.1.14-3.14.1.03-2.79.pth
BLEU = 55.63, 78.4/62.5/49.8/39.3 (BP=1.000, ratio=1.049, hyp_len=24296, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.98.1.09-2.99.1.04-2.82.pth
BLEU = 55.62, 78.3/62.5/49.8/39.3 (BP=1.000, ratio=1.051, hyp_len=24349, ref_len=23160)
Evaluation result for the model: myrk-transformer-model.99.1.10-3.00.1.00-2.73.pth
BLEU = 57.03, 79.2/63.4/51.2/41.1 (BP=1.000, ratio=1.040, hyp_len=24095, ref_len=23160)

real	63m14.759s
user	62m16.139s
sys	2m6.806s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/myrk-100epoch$
```

Best Score of the Transformer, my-rk, baseline 30 model:  

```
Evaluation result for the model: myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth
BLEU = 25.29, 57.4/33.7/19.5/10.9 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)
```

100 epoch ထိ ကြည့်မယ် ဆိုရင်တော့ အောက်ပါအတိုင်း...  

```
Evaluation result for the model: myrk-transformer-model.99.1.10-3.00.1.00-2.73.pth
BLEU = 57.03, 79.2/63.4/51.2/41.1 (BP=1.000, ratio=1.040, hyp_len=24095, ref_len=23160)
```

### for rk-my

command က အောက်ပါလိုမျိုး ပြင်ဆင်ခဲ့...  

time python train.py --train /home/ye/exp/simple-nmt/data/train  --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.pth  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/train  --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.pth
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
    'n_epochs': 30,
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
Epoch 1 - |param|=3.23e+02 |g_param|=3.38e+05 loss=5.7481e+00 ppl=313.59                                                
Validation - loss=5.7579e+00 ppl=316.68 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.23e+02 |g_param|=3.27e+05 loss=4.9385e+00 ppl=139.56                                                
Validation - loss=4.9994e+00 ppl=148.33 best_loss=5.7579e+00 best_ppl=316.68                                            
Epoch 3 - |param|=3.24e+02 |g_param|=2.43e+05 loss=4.5529e+00 ppl=94.91                                                 
Validation - loss=4.6102e+00 ppl=100.50 best_loss=4.9994e+00 best_ppl=148.33                                            
Epoch 4 - |param|=3.24e+02 |g_param|=2.13e+05 loss=4.2770e+00 ppl=72.02                                                 
Validation - loss=4.3327e+00 ppl=76.15 best_loss=4.6102e+00 best_ppl=100.50                                             
Epoch 5 - |param|=3.24e+02 |g_param|=1.85e+05 loss=3.9996e+00 ppl=54.57                                                 
Validation - loss=4.1132e+00 ppl=61.14 best_loss=4.3327e+00 best_ppl=76.15                                              
Epoch 6 - |param|=3.24e+02 |g_param|=1.49e+05 loss=3.7665e+00 ppl=43.23                                                 
Validation - loss=3.9091e+00 ppl=49.86 best_loss=4.1132e+00 best_ppl=61.14                                              
Epoch 7 - |param|=3.24e+02 |g_param|=1.91e+05 loss=3.6509e+00 ppl=38.51                                                 
Validation - loss=3.7357e+00 ppl=41.92 best_loss=3.9091e+00 best_ppl=49.86                                              
Epoch 8 - |param|=3.24e+02 |g_param|=2.87e+05 loss=3.4953e+00 ppl=32.96                                                 
Validation - loss=3.5811e+00 ppl=35.91 best_loss=3.7357e+00 best_ppl=41.92                                              
Epoch 9 - |param|=3.24e+02 |g_param|=1.90e+05 loss=3.2951e+00 ppl=26.98                                                 
Validation - loss=3.4341e+00 ppl=31.00 best_loss=3.5811e+00 best_ppl=35.91                                              
Epoch 10 - |param|=3.24e+02 |g_param|=2.32e+05 loss=3.2904e+00 ppl=26.85                                                
Validation - loss=3.3171e+00 ppl=27.58 best_loss=3.4341e+00 best_ppl=31.00                                              
Epoch 11 - |param|=3.24e+02 |g_param|=2.48e+05 loss=3.1018e+00 ppl=22.24                                                
Validation - loss=3.2106e+00 ppl=24.79 best_loss=3.3171e+00 best_ppl=27.58                                              
Epoch 12 - |param|=3.24e+02 |g_param|=2.16e+05 loss=3.0983e+00 ppl=22.16                                                
Validation - loss=3.1133e+00 ppl=22.49 best_loss=3.2106e+00 best_ppl=24.79                                              
Epoch 13 - |param|=3.24e+02 |g_param|=2.65e+05 loss=3.0294e+00 ppl=20.68                                                
Validation - loss=3.0368e+00 ppl=20.84 best_loss=3.1133e+00 best_ppl=22.49                                              
Epoch 14 - |param|=3.24e+02 |g_param|=2.91e+05 loss=2.9009e+00 ppl=18.19                                                
Validation - loss=2.9515e+00 ppl=19.14 best_loss=3.0368e+00 best_ppl=20.84                                              
Epoch 15 - |param|=3.24e+02 |g_param|=2.26e+05 loss=2.7932e+00 ppl=16.33                                                
Validation - loss=2.8764e+00 ppl=17.75 best_loss=2.9515e+00 best_ppl=19.14                                              
Epoch 16 - |param|=3.24e+02 |g_param|=4.39e+05 loss=2.7581e+00 ppl=15.77                                                
Validation - loss=2.7996e+00 ppl=16.44 best_loss=2.8764e+00 best_ppl=17.75                                              
Epoch 17 - |param|=3.24e+02 |g_param|=2.20e+05 loss=2.7365e+00 ppl=15.43                                                
Validation - loss=2.7478e+00 ppl=15.61 best_loss=2.7996e+00 best_ppl=16.44                                              
Epoch 18 - |param|=3.25e+02 |g_param|=3.03e+05 loss=2.6511e+00 ppl=14.17                                                
Validation - loss=2.6818e+00 ppl=14.61 best_loss=2.7478e+00 best_ppl=15.61                                              
Epoch 19 - |param|=3.25e+02 |g_param|=3.45e+05 loss=2.5744e+00 ppl=13.12                                                
Validation - loss=2.6171e+00 ppl=13.70 best_loss=2.6818e+00 best_ppl=14.61                                              
Epoch 20 - |param|=3.25e+02 |g_param|=3.22e+05 loss=2.5781e+00 ppl=13.17                                                
Validation - loss=2.5709e+00 ppl=13.08 best_loss=2.6171e+00 best_ppl=13.70                                              
Epoch 21 - |param|=3.25e+02 |g_param|=3.21e+05 loss=2.5050e+00 ppl=12.24                                                
Validation - loss=2.5066e+00 ppl=12.26 best_loss=2.5709e+00 best_ppl=13.08                                              
Epoch 22 - |param|=3.25e+02 |g_param|=3.63e+05 loss=2.4454e+00 ppl=11.54                                                
Validation - loss=2.4563e+00 ppl=11.66 best_loss=2.5066e+00 best_ppl=12.26                                              
Epoch 23 - |param|=3.25e+02 |g_param|=3.09e+05 loss=2.4305e+00 ppl=11.36                                                
Validation - loss=2.4043e+00 ppl=11.07 best_loss=2.4563e+00 best_ppl=11.66                                              
Epoch 24 - |param|=3.25e+02 |g_param|=3.77e+05 loss=2.4653e+00 ppl=11.77                                                
Validation - loss=2.3477e+00 ppl=10.46 best_loss=2.4043e+00 best_ppl=11.07                                              
Epoch 25 - |param|=3.25e+02 |g_param|=3.87e+05 loss=2.3556e+00 ppl=10.54                                                
Validation - loss=2.2952e+00 ppl=9.93 best_loss=2.3477e+00 best_ppl=10.46                                               
Epoch 26 - |param|=3.25e+02 |g_param|=2.76e+05 loss=2.2358e+00 ppl=9.35                                                 
Validation - loss=2.2601e+00 ppl=9.58 best_loss=2.2952e+00 best_ppl=9.93                                                
Epoch 27 - |param|=3.25e+02 |g_param|=3.89e+05 loss=2.2820e+00 ppl=9.80                                                 
Validation - loss=2.2090e+00 ppl=9.11 best_loss=2.2601e+00 best_ppl=9.58                                                
Epoch 28 - |param|=3.25e+02 |g_param|=3.29e+05 loss=2.2106e+00 ppl=9.12                                                 
Validation - loss=2.1611e+00 ppl=8.68 best_loss=2.2090e+00 best_ppl=9.11                                                
Epoch 29 - |param|=3.25e+02 |g_param|=5.53e+05 loss=2.2414e+00 ppl=9.41                                                 
Validation - loss=2.1154e+00 ppl=8.29 best_loss=2.1611e+00 best_ppl=8.68                                                
Epoch 30 - |param|=3.25e+02 |g_param|=3.89e+05 loss=2.1126e+00 ppl=8.27                                                 
Validation - loss=2.0720e+00 ppl=7.94 best_loss=2.1154e+00 best_ppl=8.29                                                

real	15m44.454s
user	15m40.310s
sys	0m3.577s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation for rk-my 30 epoch Transformer model...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-100epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: rkmy-transformer-model.01.5.75-313.59.5.76-316.68.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 33.2/0.0/0.0/0.0 (BP=0.036, ratio=0.231, hyp_len=5433, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.02.4.94-139.56.5.00-148.33.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 40.8/5.6/0.4/0.0 (BP=0.149, ratio=0.344, hyp_len=8098, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.03.4.55-94.91.4.61-100.50.pth
BLEU = 0.44, 24.0/3.5/0.3/0.0 (BP=0.640, ratio=0.691, hyp_len=16252, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.04.4.28-72.02.4.33-76.15.pth
BLEU = 1.60, 26.3/6.8/0.8/0.1 (BP=0.855, ratio=0.864, hyp_len=20322, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.05.4.00-54.57.4.11-61.14.pth
BLEU = 2.15, 23.2/7.3/1.2/0.1 (BP=1.000, ratio=1.184, hyp_len=27826, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.06.3.77-43.23.3.91-49.86.pth
BLEU = 2.06, 19.5/6.3/1.2/0.1 (BP=1.000, ratio=1.534, hyp_len=36067, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.07.3.65-38.51.3.74-41.92.pth
BLEU = 2.13, 15.6/5.4/1.2/0.2 (BP=1.000, ratio=2.064, hyp_len=48515, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.08.3.50-32.96.3.58-35.91.pth
BLEU = 2.04, 13.0/4.6/1.2/0.2 (BP=1.000, ratio=2.605, hyp_len=61241, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.09.3.30-26.98.3.43-31.00.pth
BLEU = 3.99, 22.0/8.4/2.4/0.6 (BP=1.000, ratio=1.617, hyp_len=38017, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.10.3.29-26.85.3.32-27.58.pth
BLEU = 3.38, 17.5/6.7/2.1/0.5 (BP=1.000, ratio=2.124, hyp_len=49932, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.11.3.10-22.24.3.21-24.79.pth
BLEU = 4.17, 19.4/7.8/2.6/0.8 (BP=1.000, ratio=2.030, hyp_len=47728, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.12.3.10-22.16.3.11-22.49.pth
BLEU = 5.76, 25.3/10.4/3.7/1.1 (BP=1.000, ratio=1.610, hyp_len=37856, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.13.3.03-20.68.3.04-20.84.pth
BLEU = 6.80, 28.2/12.0/4.3/1.5 (BP=1.000, ratio=1.507, hyp_len=35425, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.14.2.90-18.19.2.95-19.14.pth
BLEU = 8.07, 31.4/13.7/5.2/1.9 (BP=1.000, ratio=1.392, hyp_len=32714, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.15.2.79-16.33.2.88-17.75.pth
BLEU = 10.36, 37.8/17.1/6.8/2.6 (BP=1.000, ratio=1.186, hyp_len=27879, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.16.2.76-15.77.2.80-16.44.pth
BLEU = 11.57, 40.1/18.6/7.7/3.1 (BP=1.000, ratio=1.141, hyp_len=26825, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.17.2.74-15.43.2.75-15.61.pth
BLEU = 12.62, 41.2/19.6/8.6/3.7 (BP=1.000, ratio=1.142, hyp_len=26841, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.18.2.65-14.17.2.68-14.61.pth
BLEU = 13.00, 41.8/20.2/8.9/3.8 (BP=1.000, ratio=1.150, hyp_len=27024, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.19.2.57-13.12.2.62-13.70.pth
BLEU = 13.99, 43.0/21.4/9.7/4.3 (BP=1.000, ratio=1.146, hyp_len=26951, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.20.2.58-13.17.2.57-13.08.pth
BLEU = 15.42, 45.4/23.0/10.9/5.0 (BP=1.000, ratio=1.101, hyp_len=25878, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.21.2.51-12.24.2.51-12.26.pth
BLEU = 17.03, 48.5/25.1/12.1/5.7 (BP=1.000, ratio=1.053, hyp_len=24757, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.22.2.45-11.54.2.46-11.66.pth
BLEU = 17.59, 48.7/25.5/12.6/6.1 (BP=1.000, ratio=1.067, hyp_len=25077, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.23.2.43-11.36.2.40-11.07.pth
BLEU = 17.48, 47.1/25.1/12.6/6.3 (BP=1.000, ratio=1.127, hyp_len=26506, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.24.2.47-11.77.2.35-10.46.pth
BLEU = 19.30, 50.5/27.3/14.1/7.1 (BP=1.000, ratio=1.068, hyp_len=25104, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.25.2.36-10.54.2.30-9.93.pth
BLEU = 20.26, 51.3/28.2/14.9/7.8 (BP=1.000, ratio=1.073, hyp_len=25221, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.26.2.24-9.35.2.26-9.58.pth
BLEU = 21.00, 52.5/29.2/15.5/8.2 (BP=1.000, ratio=1.055, hyp_len=24798, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.27.2.28-9.80.2.21-9.11.pth
BLEU = 21.33, 51.9/29.4/15.9/8.5 (BP=1.000, ratio=1.103, hyp_len=25942, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.28.2.21-9.12.2.16-8.68.pth
BLEU = 22.57, 53.4/30.7/17.0/9.3 (BP=1.000, ratio=1.085, hyp_len=25519, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.29.2.24-9.41.2.12-8.29.pth
BLEU = 23.01, 52.7/30.8/17.4/9.9 (BP=1.000, ratio=1.120, hyp_len=26329, ref_len=23509)
Evaluation result for the model: rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth
BLEU = 25.23, 56.5/33.5/19.2/11.2 (BP=1.000, ratio=1.054, hyp_len=24770, ref_len=23509)

real	26m14.640s
user	25m56.488s
sys	0m37.911s
(simple-nmt) ye@:~/exp/simple-nmt/model/transformer/baseline/rkmy-100epoch$
```

Baseline က 25.23 ...  

### RL Fine-tuning for Transformer

### for my-rk

(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth --model_fn ./model/rl/transformer/100epoch/baseline/myrk/transformer-rl-30to100model-myrk.pth --init_epoch 30 --iteration_per_update 32  --max_grad_norm 1e+8 --n_epochs 100  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth --model_fn ./model/rl/transformer/100epoch/baseline/myrk/transformer-rl-30to100model-myrk.pth --init_epoch 30 --iteration_per_update 32  --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/myrk-100epoch/myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/100epoch/baseline/myrk/transformer-rl-30to100model-myrk.pth
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 30,
    'iteration_per_update': 32,
    'lang': 'myrk',
    'load_fn': './model/transformer/baseline/myrk-100epoch/myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/100epoch/baseline/myrk/transformer-rl-30to100model-myrk.pth',
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
Epoch 30 - |param|=3.25e+02 |g_param|=3.69e+05 loss=2.1989e+00 ppl=9.02                                                 
Validation - loss=2.0787e+00 ppl=7.99 best_loss=inf best_ppl=inf                                                        
Epoch 31 - |param|=3.25e+02 |g_param|=4.26e+05 loss=2.0784e+00 ppl=7.99                                                 
Validation - loss=2.0298e+00 ppl=7.61 best_loss=2.0787e+00 best_ppl=7.99                                                
Epoch 32 - |param|=3.25e+02 |g_param|=5.00e+05 loss=2.0379e+00 ppl=7.67                                                 
Validation - loss=1.9954e+00 ppl=7.36 best_loss=2.0298e+00 best_ppl=7.61                                                
Epoch 33 - |param|=3.25e+02 |g_param|=3.85e+05 loss=1.9771e+00 ppl=7.22                                                 
Validation - loss=1.9574e+00 ppl=7.08 best_loss=1.9954e+00 best_ppl=7.36                                                
Epoch 34 - |param|=3.26e+02 |g_param|=4.05e+05 loss=2.0008e+00 ppl=7.39                                                 
Validation - loss=1.9201e+00 ppl=6.82 best_loss=1.9574e+00 best_ppl=7.08                                                
Epoch 35 - |param|=3.26e+02 |g_param|=6.04e+05 loss=1.9950e+00 ppl=7.35                                                 
Validation - loss=1.8861e+00 ppl=6.59 best_loss=1.9201e+00 best_ppl=6.82                                                
Epoch 36 - |param|=3.26e+02 |g_param|=3.70e+05 loss=1.9037e+00 ppl=6.71                                                 
Validation - loss=1.8633e+00 ppl=6.44 best_loss=1.8861e+00 best_ppl=6.59                                                
Epoch 37 - |param|=3.26e+02 |g_param|=4.21e+05 loss=1.8932e+00 ppl=6.64                                                 
Validation - loss=1.8247e+00 ppl=6.20 best_loss=1.8633e+00 best_ppl=6.44                                                
Epoch 38 - |param|=3.26e+02 |g_param|=4.27e+05 loss=1.9175e+00 ppl=6.80                                                 
Validation - loss=1.7823e+00 ppl=5.94 best_loss=1.8247e+00 best_ppl=6.20                                                
Epoch 39 - |param|=3.26e+02 |g_param|=4.81e+05 loss=1.7703e+00 ppl=5.87                                                 
Validation - loss=1.7633e+00 ppl=5.83 best_loss=1.7823e+00 best_ppl=5.94                                                
Epoch 40 - |param|=3.26e+02 |g_param|=5.44e+05 loss=1.7706e+00 ppl=5.87                                                 
Validation - loss=1.7302e+00 ppl=5.64 best_loss=1.7633e+00 best_ppl=5.83                                                
Epoch 41 - |param|=3.26e+02 |g_param|=5.12e+05 loss=1.7835e+00 ppl=5.95                                                 
Validation - loss=1.7003e+00 ppl=5.48 best_loss=1.7302e+00 best_ppl=5.64                                                
Epoch 42 - |param|=3.26e+02 |g_param|=5.59e+05 loss=1.7302e+00 ppl=5.64                                                 
Validation - loss=1.6748e+00 ppl=5.34 best_loss=1.7003e+00 best_ppl=5.48                                                
Epoch 43 - |param|=3.26e+02 |g_param|=5.87e+05 loss=1.7267e+00 ppl=5.62                                                 
Validation - loss=1.6476e+00 ppl=5.19 best_loss=1.6748e+00 best_ppl=5.34                                                
Epoch 44 - |param|=3.26e+02 |g_param|=5.98e+05 loss=1.7515e+00 ppl=5.76                                                 
Validation - loss=1.6309e+00 ppl=5.11 best_loss=1.6476e+00 best_ppl=5.19                                                
Epoch 45 - |param|=3.26e+02 |g_param|=5.73e+05 loss=1.6389e+00 ppl=5.15                                                 
Validation - loss=1.6018e+00 ppl=4.96 best_loss=1.6309e+00 best_ppl=5.11                                                
Epoch 46 - |param|=3.26e+02 |g_param|=5.61e+05 loss=1.6803e+00 ppl=5.37                                                 
Validation - loss=1.5833e+00 ppl=4.87 best_loss=1.6018e+00 best_ppl=4.96                                                
Epoch 47 - |param|=3.26e+02 |g_param|=4.08e+05 loss=1.6920e+00 ppl=5.43                                                 
Validation - loss=1.5410e+00 ppl=4.67 best_loss=1.5833e+00 best_ppl=4.87                                                
Epoch 48 - |param|=3.26e+02 |g_param|=5.90e+05 loss=1.6204e+00 ppl=5.06                                                 
Validation - loss=1.5207e+00 ppl=4.58 best_loss=1.5410e+00 best_ppl=4.67                                                
Epoch 49 - |param|=3.26e+02 |g_param|=4.54e+05 loss=1.6108e+00 ppl=5.01                                                 
Validation - loss=1.5120e+00 ppl=4.54 best_loss=1.5207e+00 best_ppl=4.58                                                
Epoch 50 - |param|=3.26e+02 |g_param|=6.40e+05 loss=1.6125e+00 ppl=5.02                                                 
Validation - loss=1.4795e+00 ppl=4.39 best_loss=1.5120e+00 best_ppl=4.54                                                
Epoch 51 - |param|=3.26e+02 |g_param|=5.52e+05 loss=1.5398e+00 ppl=4.66                                                 
Validation - loss=1.4631e+00 ppl=4.32 best_loss=1.4795e+00 best_ppl=4.39                                                
Epoch 52 - |param|=3.26e+02 |g_param|=5.90e+05 loss=1.5939e+00 ppl=4.92                                                 
Validation - loss=1.4508e+00 ppl=4.27 best_loss=1.4631e+00 best_ppl=4.32                                                
Epoch 53 - |param|=3.26e+02 |g_param|=3.79e+05 loss=1.5430e+00 ppl=4.68                                                 
Validation - loss=1.4426e+00 ppl=4.23 best_loss=1.4508e+00 best_ppl=4.27                                                
Epoch 54 - |param|=3.26e+02 |g_param|=2.81e+05 loss=1.5152e+00 ppl=4.55                                                 
Validation - loss=1.4084e+00 ppl=4.09 best_loss=1.4426e+00 best_ppl=4.23                                                
Epoch 55 - |param|=3.26e+02 |g_param|=2.94e+05 loss=1.5244e+00 ppl=4.59                                                 
Validation - loss=1.4038e+00 ppl=4.07 best_loss=1.4084e+00 best_ppl=4.09                                                
Epoch 56 - |param|=3.26e+02 |g_param|=2.75e+05 loss=1.4505e+00 ppl=4.27                                                 
Validation - loss=1.3810e+00 ppl=3.98 best_loss=1.4038e+00 best_ppl=4.07                                                
Epoch 57 - |param|=3.26e+02 |g_param|=2.92e+05 loss=1.5086e+00 ppl=4.52                                                 
Validation - loss=1.3603e+00 ppl=3.90 best_loss=1.3810e+00 best_ppl=3.98                                                
Epoch 58 - |param|=3.26e+02 |g_param|=2.64e+05 loss=1.4304e+00 ppl=4.18                                                 
Validation - loss=1.3401e+00 ppl=3.82 best_loss=1.3603e+00 best_ppl=3.90                                                
Epoch 59 - |param|=3.26e+02 |g_param|=3.62e+05 loss=1.4744e+00 ppl=4.37                                                 
Validation - loss=1.3327e+00 ppl=3.79 best_loss=1.3401e+00 best_ppl=3.82                                                
Epoch 60 - |param|=3.26e+02 |g_param|=3.19e+05 loss=1.4787e+00 ppl=4.39                                                 
Validation - loss=1.3167e+00 ppl=3.73 best_loss=1.3327e+00 best_ppl=3.79                                                
Epoch 61 - |param|=3.26e+02 |g_param|=3.64e+05 loss=1.4401e+00 ppl=4.22                                                 
Validation - loss=1.3057e+00 ppl=3.69 best_loss=1.3167e+00 best_ppl=3.73                                                
Epoch 62 - |param|=3.26e+02 |g_param|=2.77e+05 loss=1.3793e+00 ppl=3.97                                                 
Validation - loss=1.2947e+00 ppl=3.65 best_loss=1.3057e+00 best_ppl=3.69                                                
Epoch 63 - |param|=3.26e+02 |g_param|=3.85e+05 loss=1.3744e+00 ppl=3.95                                                 
Validation - loss=1.2979e+00 ppl=3.66 best_loss=1.2947e+00 best_ppl=3.65                                                
Epoch 64 - |param|=3.26e+02 |g_param|=4.05e+05 loss=1.3371e+00 ppl=3.81                                                 
Validation - loss=1.2883e+00 ppl=3.63 best_loss=1.2947e+00 best_ppl=3.65                                                
Epoch 65 - |param|=3.26e+02 |g_param|=2.53e+05 loss=1.3929e+00 ppl=4.03                                                 
Validation - loss=1.2488e+00 ppl=3.49 best_loss=1.2883e+00 best_ppl=3.63                                                
Epoch 66 - |param|=3.26e+02 |g_param|=4.02e+05 loss=1.3123e+00 ppl=3.71                                                 
Validation - loss=1.2372e+00 ppl=3.45 best_loss=1.2488e+00 best_ppl=3.49                                                
Epoch 67 - |param|=3.26e+02 |g_param|=3.68e+05 loss=1.3659e+00 ppl=3.92                                                 
Validation - loss=1.2282e+00 ppl=3.41 best_loss=1.2372e+00 best_ppl=3.45                                                
Epoch 68 - |param|=3.26e+02 |g_param|=5.47e+05 loss=1.3426e+00 ppl=3.83                                                 
Validation - loss=1.2492e+00 ppl=3.49 best_loss=1.2282e+00 best_ppl=3.41                                                
Epoch 69 - |param|=3.26e+02 |g_param|=3.28e+05 loss=1.3371e+00 ppl=3.81                                                 
Validation - loss=1.2374e+00 ppl=3.45 best_loss=1.2282e+00 best_ppl=3.41                                                
Epoch 70 - |param|=3.26e+02 |g_param|=3.15e+05 loss=1.3773e+00 ppl=3.96                                                 
Validation - loss=1.2119e+00 ppl=3.36 best_loss=1.2282e+00 best_ppl=3.41                                                
Epoch 71 - |param|=3.26e+02 |g_param|=3.58e+05 loss=1.3292e+00 ppl=3.78                                                 
Validation - loss=1.1973e+00 ppl=3.31 best_loss=1.2119e+00 best_ppl=3.36                                                
Epoch 72 - |param|=3.26e+02 |g_param|=3.43e+05 loss=1.3203e+00 ppl=3.74                                                 
Validation - loss=1.1771e+00 ppl=3.24 best_loss=1.1973e+00 best_ppl=3.31                                                
Epoch 73 - |param|=3.26e+02 |g_param|=4.05e+05 loss=1.3428e+00 ppl=3.83                                                 
Validation - loss=1.1798e+00 ppl=3.25 best_loss=1.1771e+00 best_ppl=3.24                                                
Epoch 74 - |param|=3.26e+02 |g_param|=3.60e+05 loss=1.2581e+00 ppl=3.52                                                 
Validation - loss=1.1659e+00 ppl=3.21 best_loss=1.1771e+00 best_ppl=3.24                                                
Epoch 75 - |param|=3.26e+02 |g_param|=3.27e+05 loss=1.2906e+00 ppl=3.63                                                 
Validation - loss=1.1489e+00 ppl=3.15 best_loss=1.1659e+00 best_ppl=3.21                                                
Epoch 76 - |param|=3.26e+02 |g_param|=3.64e+05 loss=1.2810e+00 ppl=3.60                                                 
Validation - loss=1.1593e+00 ppl=3.19 best_loss=1.1489e+00 best_ppl=3.15                                                
Epoch 77 - |param|=3.26e+02 |g_param|=3.85e+05 loss=1.2234e+00 ppl=3.40                                                 
Validation - loss=1.1391e+00 ppl=3.12 best_loss=1.1489e+00 best_ppl=3.15                                                
Epoch 78 - |param|=3.26e+02 |g_param|=3.22e+05 loss=1.1857e+00 ppl=3.27                                                 
Validation - loss=1.1299e+00 ppl=3.10 best_loss=1.1391e+00 best_ppl=3.12                                                
Epoch 79 - |param|=3.26e+02 |g_param|=2.98e+05 loss=1.2395e+00 ppl=3.45                                                 
Validation - loss=1.1408e+00 ppl=3.13 best_loss=1.1299e+00 best_ppl=3.10                                                
Epoch 80 - |param|=3.26e+02 |g_param|=5.40e+05 loss=1.2233e+00 ppl=3.40                                                 
Validation - loss=1.1156e+00 ppl=3.05 best_loss=1.1299e+00 best_ppl=3.10                                                
Epoch 81 - |param|=3.26e+02 |g_param|=3.58e+05 loss=1.1703e+00 ppl=3.22                                                 
Validation - loss=1.1080e+00 ppl=3.03 best_loss=1.1156e+00 best_ppl=3.05                                                
Epoch 82 - |param|=3.26e+02 |g_param|=5.18e+05 loss=1.2639e+00 ppl=3.54                                                 
Validation - loss=1.1591e+00 ppl=3.19 best_loss=1.1080e+00 best_ppl=3.03                                                
Epoch 83 - |param|=3.26e+02 |g_param|=4.18e+05 loss=1.2255e+00 ppl=3.41                                                 
Validation - loss=1.1006e+00 ppl=3.01 best_loss=1.1080e+00 best_ppl=3.03                                                
Epoch 84 - |param|=3.26e+02 |g_param|=4.17e+05 loss=1.2212e+00 ppl=3.39                                                 
Validation - loss=1.0921e+00 ppl=2.98 best_loss=1.1006e+00 best_ppl=3.01                                                
Epoch 85 - |param|=3.26e+02 |g_param|=4.75e+05 loss=1.2340e+00 ppl=3.43                                                 
Validation - loss=1.0902e+00 ppl=2.97 best_loss=1.0921e+00 best_ppl=2.98                                                
Epoch 86 - |param|=3.26e+02 |g_param|=2.68e+05 loss=1.2413e+00 ppl=3.46                                                 
Validation - loss=1.0831e+00 ppl=2.95 best_loss=1.0902e+00 best_ppl=2.97                                                
Epoch 87 - |param|=3.26e+02 |g_param|=3.14e+05 loss=1.1120e+00 ppl=3.04                                                 
Validation - loss=1.0739e+00 ppl=2.93 best_loss=1.0831e+00 best_ppl=2.95                                                
Epoch 88 - |param|=3.26e+02 |g_param|=2.83e+05 loss=1.1766e+00 ppl=3.24                                                 
Validation - loss=1.0636e+00 ppl=2.90 best_loss=1.0739e+00 best_ppl=2.93                                                
Epoch 89 - |param|=3.26e+02 |g_param|=4.73e+05 loss=1.1575e+00 ppl=3.18                                                 
Validation - loss=1.0548e+00 ppl=2.87 best_loss=1.0636e+00 best_ppl=2.90                                                
Epoch 90 - |param|=3.26e+02 |g_param|=3.15e+05 loss=1.1574e+00 ppl=3.18                                                 
Validation - loss=1.0496e+00 ppl=2.86 best_loss=1.0548e+00 best_ppl=2.87                                                
Epoch 91 - |param|=3.26e+02 |g_param|=5.97e+05 loss=1.0921e+00 ppl=2.98                                                 
Validation - loss=1.0780e+00 ppl=2.94 best_loss=1.0496e+00 best_ppl=2.86                                                
Epoch 92 - |param|=3.26e+02 |g_param|=4.75e+05 loss=1.1335e+00 ppl=3.11                                                 
Validation - loss=1.0500e+00 ppl=2.86 best_loss=1.0496e+00 best_ppl=2.86                                                
Epoch 93 - |param|=3.26e+02 |g_param|=2.39e+05 loss=1.0771e+00 ppl=2.94                                                 
Validation - loss=1.0317e+00 ppl=2.81 best_loss=1.0496e+00 best_ppl=2.86                                                
Epoch 94 - |param|=3.26e+02 |g_param|=3.15e+05 loss=1.0937e+00 ppl=2.99                                                 
Validation - loss=1.0288e+00 ppl=2.80 best_loss=1.0317e+00 best_ppl=2.81                                                
Epoch 95 - |param|=3.26e+02 |g_param|=5.63e+05 loss=1.1455e+00 ppl=3.14                                                 
Validation - loss=1.0231e+00 ppl=2.78 best_loss=1.0288e+00 best_ppl=2.80                                                
Epoch 96 - |param|=3.26e+02 |g_param|=4.40e+05 loss=1.0675e+00 ppl=2.91                                                 
Validation - loss=1.0254e+00 ppl=2.79 best_loss=1.0231e+00 best_ppl=2.78                                                
Epoch 97 - |param|=3.26e+02 |g_param|=5.40e+05 loss=1.1090e+00 ppl=3.03                                                 
Validation - loss=1.0297e+00 ppl=2.80 best_loss=1.0231e+00 best_ppl=2.78                                                
Epoch 98 - |param|=3.26e+02 |g_param|=7.47e+05 loss=1.1175e+00 ppl=3.06                                                 
Validation - loss=1.0109e+00 ppl=2.75 best_loss=1.0231e+00 best_ppl=2.78                                                
Epoch 99 - |param|=3.27e+02 |g_param|=3.49e+05 loss=1.0805e+00 ppl=2.95                                                 
Validation - loss=1.0028e+00 ppl=2.73 best_loss=1.0109e+00 best_ppl=2.75                                                
Epoch 100 - |param|=3.27e+02 |g_param|=4.37e+05 loss=1.0718e+00 ppl=2.92                                                
Validation - loss=1.0265e+00 ppl=2.79 best_loss=1.0028e+00 best_ppl=2.73                                                

real	36m48.883s
user	36m41.531s
sys	0m6.574s
(simple-nmt) ye@:~/exp/simple-nmt$
```

testing/evaluation for my-rk, 30-100 RL fine-tuning model...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/100epoch/baseline/myrk$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-30to100model-myrk.30.2.20-9.02.2.08-7.99.pth
BLEU = 24.89, 55.4/32.9/19.2/11.0 (BP=1.000, ratio=1.111, hyp_len=25723, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.31.2.08-7.99.2.03-7.61.pth
BLEU = 27.06, 58.5/35.5/21.1/12.2 (BP=1.000, ratio=1.068, hyp_len=24725, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.32.2.04-7.67.2.00-7.36.pth
BLEU = 27.35, 58.4/35.6/21.4/12.6 (BP=1.000, ratio=1.082, hyp_len=25061, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.33.1.98-7.22.1.96-7.08.pth
BLEU = 28.68, 60.1/37.1/22.5/13.5 (BP=1.000, ratio=1.066, hyp_len=24688, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.34.2.00-7.39.1.92-6.82.pth
BLEU = 28.48, 58.7/36.5/22.5/13.7 (BP=1.000, ratio=1.100, hyp_len=25474, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.35.2.00-7.35.1.89-6.59.pth
BLEU = 31.04, 62.1/39.3/24.8/15.3 (BP=1.000, ratio=1.054, hyp_len=24408, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.36.1.90-6.71.1.86-6.44.pth
BLEU = 30.51, 60.5/38.5/24.4/15.3 (BP=1.000, ratio=1.098, hyp_len=25427, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.37.1.89-6.64.1.82-6.20.pth
BLEU = 33.01, 63.7/41.3/26.6/16.9 (BP=1.000, ratio=1.050, hyp_len=24324, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.38.1.92-6.80.1.78-5.94.pth
BLEU = 32.46, 62.2/40.5/26.2/16.8 (BP=1.000, ratio=1.086, hyp_len=25142, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.39.1.77-5.87.1.76-5.83.pth
BLEU = 32.47, 61.7/40.5/26.4/16.8 (BP=1.000, ratio=1.105, hyp_len=25602, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.40.1.77-5.87.1.73-5.64.pth
BLEU = 32.70, 61.5/40.4/26.5/17.3 (BP=1.000, ratio=1.115, hyp_len=25825, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.41.1.78-5.95.1.70-5.48.pth
BLEU = 37.14, 66.9/45.1/30.5/20.7 (BP=1.000, ratio=1.031, hyp_len=23886, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.42.1.73-5.64.1.67-5.34.pth
BLEU = 38.02, 67.8/46.1/31.3/21.3 (BP=1.000, ratio=1.022, hyp_len=23671, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.43.1.73-5.62.1.65-5.19.pth
BLEU = 36.03, 65.4/44.2/29.6/19.7 (BP=1.000, ratio=1.076, hyp_len=24911, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.44.1.75-5.76.1.63-5.11.pth
BLEU = 35.71, 64.3/43.8/29.6/19.5 (BP=1.000, ratio=1.104, hyp_len=25578, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.45.1.64-5.15.1.60-4.96.pth
BLEU = 37.83, 66.9/46.1/31.4/21.1 (BP=1.000, ratio=1.066, hyp_len=24685, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.46.1.68-5.37.1.58-4.87.pth
BLEU = 36.58, 64.7/44.6/30.4/20.4 (BP=1.000, ratio=1.119, hyp_len=25917, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.47.1.69-5.43.1.54-4.67.pth
BLEU = 40.20, 68.4/48.0/33.7/23.6 (BP=1.000, ratio=1.051, hyp_len=24340, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.48.1.62-5.06.1.52-4.58.pth
BLEU = 39.63, 67.9/47.5/33.2/23.0 (BP=1.000, ratio=1.068, hyp_len=24726, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.49.1.61-5.01.1.51-4.54.pth
BLEU = 40.32, 68.6/48.3/33.9/23.6 (BP=1.000, ratio=1.062, hyp_len=24596, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.50.1.61-5.02.1.48-4.39.pth
BLEU = 41.52, 69.2/49.3/35.1/24.8 (BP=1.000, ratio=1.064, hyp_len=24645, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.51.1.54-4.66.1.46-4.32.pth
BLEU = 41.22, 68.6/49.0/34.9/24.6 (BP=1.000, ratio=1.077, hyp_len=24944, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.52.1.59-4.92.1.45-4.27.pth
BLEU = 44.24, 72.0/52.2/37.7/27.0 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.53.1.54-4.68.1.44-4.23.pth
BLEU = 45.92, 73.4/53.5/39.2/28.9 (BP=1.000, ratio=1.007, hyp_len=23326, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.54.1.52-4.55.1.41-4.09.pth
BLEU = 44.52, 71.8/52.1/38.0/27.6 (BP=1.000, ratio=1.041, hyp_len=24103, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.55.1.52-4.59.1.40-4.07.pth
BLEU = 43.01, 69.6/50.7/36.7/26.4 (BP=1.000, ratio=1.087, hyp_len=25185, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.56.1.45-4.27.1.38-3.98.pth
BLEU = 42.36, 68.4/49.7/36.2/26.2 (BP=1.000, ratio=1.108, hyp_len=25658, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.57.1.51-4.52.1.36-3.90.pth
BLEU = 45.86, 72.4/53.3/39.4/29.1 (BP=1.000, ratio=1.047, hyp_len=24254, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.58.1.43-4.18.1.34-3.82.pth
BLEU = 46.34, 72.7/53.8/39.9/29.6 (BP=1.000, ratio=1.051, hyp_len=24330, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.59.1.47-4.37.1.33-3.79.pth
BLEU = 46.99, 73.2/54.3/40.5/30.3 (BP=1.000, ratio=1.041, hyp_len=24112, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.60.1.48-4.39.1.32-3.73.pth
BLEU = 45.37, 71.3/52.8/39.1/28.8 (BP=1.000, ratio=1.075, hyp_len=24886, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.61.1.44-4.22.1.31-3.69.pth
BLEU = 45.57, 71.2/52.9/39.3/29.1 (BP=1.000, ratio=1.084, hyp_len=25109, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.62.1.38-3.97.1.29-3.65.pth
BLEU = 46.98, 73.0/54.6/40.7/30.0 (BP=1.000, ratio=1.058, hyp_len=24505, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.63.1.37-3.95.1.30-3.66.pth
BLEU = 46.36, 72.3/54.2/40.2/29.3 (BP=1.000, ratio=1.076, hyp_len=24921, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.64.1.34-3.81.1.29-3.63.pth
BLEU = 46.13, 71.8/53.8/40.1/29.3 (BP=1.000, ratio=1.085, hyp_len=25127, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.65.1.39-4.03.1.25-3.49.pth
BLEU = 47.39, 72.6/54.6/41.2/30.9 (BP=1.000, ratio=1.077, hyp_len=24937, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.66.1.31-3.71.1.24-3.45.pth
BLEU = 49.34, 74.5/56.6/43.1/32.6 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.67.1.37-3.92.1.23-3.41.pth
BLEU = 50.51, 75.7/57.7/44.1/33.8 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.68.1.34-3.83.1.25-3.49.pth
BLEU = 50.86, 76.0/57.8/44.4/34.4 (BP=1.000, ratio=1.021, hyp_len=23639, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.69.1.34-3.81.1.24-3.45.pth
BLEU = 47.75, 73.1/55.5/41.7/30.7 (BP=1.000, ratio=1.076, hyp_len=24923, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.70.1.38-3.96.1.21-3.36.pth
BLEU = 49.88, 75.3/57.5/43.7/32.8 (BP=1.000, ratio=1.046, hyp_len=24219, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.71.1.33-3.78.1.20-3.31.pth
BLEU = 48.61, 73.3/56.1/42.6/31.9 (BP=1.000, ratio=1.080, hyp_len=25007, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.72.1.32-3.74.1.18-3.24.pth
BLEU = 51.44, 76.1/58.6/45.2/34.8 (BP=1.000, ratio=1.042, hyp_len=24130, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.73.1.34-3.83.1.18-3.25.pth
BLEU = 48.60, 72.9/55.8/42.6/32.2 (BP=1.000, ratio=1.091, hyp_len=25278, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.74.1.26-3.52.1.17-3.21.pth
BLEU = 50.28, 74.7/57.5/44.2/33.6 (BP=1.000, ratio=1.068, hyp_len=24729, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.75.1.29-3.63.1.15-3.15.pth
BLEU = 51.87, 76.1/58.7/45.7/35.5 (BP=1.000, ratio=1.049, hyp_len=24292, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.76.1.28-3.60.1.16-3.19.pth
BLEU = 50.72, 75.3/58.3/44.7/33.7 (BP=1.000, ratio=1.062, hyp_len=24598, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.77.1.22-3.40.1.14-3.12.pth
BLEU = 53.85, 77.9/60.7/47.6/37.4 (BP=1.000, ratio=1.023, hyp_len=23687, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.78.1.19-3.27.1.13-3.10.pth
BLEU = 52.59, 76.0/59.3/46.6/36.4 (BP=1.000, ratio=1.054, hyp_len=24417, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.79.1.24-3.45.1.14-3.13.pth
BLEU = 50.51, 74.3/57.6/44.5/34.1 (BP=1.000, ratio=1.082, hyp_len=25070, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.80.1.22-3.40.1.12-3.05.pth
BLEU = 53.91, 77.5/60.7/47.7/37.6 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.81.1.17-3.22.1.11-3.03.pth
BLEU = 53.62, 77.0/60.5/47.6/37.2 (BP=1.000, ratio=1.051, hyp_len=24333, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.82.1.26-3.54.1.16-3.19.pth
BLEU = 50.57, 74.6/58.2/44.8/33.6 (BP=1.000, ratio=1.089, hyp_len=25212, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.83.1.23-3.41.1.10-3.01.pth
BLEU = 52.68, 75.6/59.6/46.9/36.5 (BP=1.000, ratio=1.071, hyp_len=24807, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.84.1.22-3.39.1.09-2.98.pth
BLEU = 53.86, 77.6/61.0/47.8/37.2 (BP=1.000, ratio=1.040, hyp_len=24087, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.85.1.23-3.43.1.09-2.97.pth
BLEU = 53.25, 76.9/60.4/47.3/36.6 (BP=1.000, ratio=1.055, hyp_len=24424, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.86.1.24-3.46.1.08-2.95.pth
BLEU = 53.74, 77.1/60.7/47.9/37.2 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.87.1.11-3.04.1.07-2.93.pth
BLEU = 52.59, 75.5/59.5/46.8/36.4 (BP=1.000, ratio=1.083, hyp_len=25078, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.88.1.18-3.24.1.06-2.90.pth
BLEU = 54.96, 78.2/61.9/49.0/38.5 (BP=1.000, ratio=1.039, hyp_len=24071, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.89.1.16-3.18.1.05-2.87.pth
BLEU = 55.59, 78.2/62.2/49.7/39.5 (BP=1.000, ratio=1.041, hyp_len=24099, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.90.1.16-3.18.1.05-2.86.pth
BLEU = 55.40, 78.1/62.1/49.5/39.2 (BP=1.000, ratio=1.044, hyp_len=24187, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.91.1.09-2.98.1.08-2.94.pth
BLEU = 52.23, 75.3/59.5/46.5/35.7 (BP=1.000, ratio=1.091, hyp_len=25268, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.92.1.13-3.11.1.05-2.86.pth
BLEU = 54.34, 77.2/61.4/48.5/37.9 (BP=1.000, ratio=1.062, hyp_len=24592, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.93.1.08-2.94.1.03-2.81.pth
BLEU = 55.96, 78.8/62.6/50.0/39.7 (BP=1.000, ratio=1.038, hyp_len=24046, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.94.1.09-2.99.1.03-2.80.pth
BLEU = 56.39, 78.9/63.0/50.5/40.3 (BP=1.000, ratio=1.040, hyp_len=24078, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.95.1.15-3.14.1.02-2.78.pth
BLEU = 57.40, 79.8/64.0/51.5/41.3 (BP=1.000, ratio=1.025, hyp_len=23734, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.96.1.07-2.91.1.03-2.79.pth
BLEU = 54.72, 77.3/61.6/48.9/38.5 (BP=1.000, ratio=1.065, hyp_len=24668, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.97.1.11-3.03.1.03-2.80.pth
BLEU = 58.69, 80.5/64.9/52.8/43.0 (BP=1.000, ratio=1.015, hyp_len=23498, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.98.1.12-3.06.1.01-2.75.pth
BLEU = 57.82, 79.8/64.4/52.0/41.8 (BP=1.000, ratio=1.029, hyp_len=23829, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.99.1.08-2.95.1.00-2.73.pth
BLEU = 56.86, 78.8/63.5/51.1/40.9 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: transformer-rl-30to100model-myrk.100.1.07-2.92.1.03-2.79.pth
BLEU = 54.02, 76.3/61.0/48.4/37.8 (BP=1.000, ratio=1.086, hyp_len=25144, ref_len=23160)
real	42m32.866s
user	41m48.673s
sys	1m30.657s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/100epoch/baseline/myrk$
```

30 epoch Transformer မော်ဒယ်ရဲ့ baseline က 25.29  
```
Evaluation result for the model: myrk-transformer-model.30.2.19-8.93.2.12-8.36.pth
BLEU = 25.29, 57.4/33.7/19.5/10.9 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)
```

my-rk, 30-100 RL fine-tuning မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က 58.69 ရတယ်...  

```
Evaluation result for the model: transformer-rl-30to100model-myrk.97.1.11-3.03.1.03-2.80.pth
BLEU = 58.69, 80.5/64.9/52.8/43.0 (BP=1.000, ratio=1.015, hyp_len=23498, ref_len=23160)
```

### for rk-my

baseline ရဲ့ အကောင်းဆုံး ရလဒ်မော်ဒယ်က... rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth  

time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth --model_fn ./model/rl/transformer/100epoch/baseline/rkmy/transformer-rl-30to100model-rkmy.pth --init_epoch 30 --iteration_per_update 32  --max_grad_norm 1e+8 --n_epochs 100  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth --model_fn ./model/rl/transformer/100epoch/baseline/rkmy/transformer-rl-30to100model-rkmy.pth --init_epoch 30 --iteration_per_update 32  --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl/transformer/100epoch/baseline/rkmy/transformer-rl-30to100model-rkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 30
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 30,
    'iteration_per_update': 32,
    'lang': 'rkmy',
    'load_fn': './model/transformer/baseline/rkmy-100epoch/rkmy-transformer-model.30.2.11-8.27.2.07-7.94.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl/transformer/100epoch/baseline/rkmy/transformer-rl-30to100model-rkmy.pth',
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
Epoch 30 - |param|=3.25e+02 |g_param|=3.66e+05 loss=2.1276e+00 ppl=8.39                                                 
Validation - loss=2.0381e+00 ppl=7.68 best_loss=inf best_ppl=inf                                                        
Epoch 31 - |param|=3.25e+02 |g_param|=4.69e+05 loss=2.0639e+00 ppl=7.88                                                 
Validation - loss=2.0034e+00 ppl=7.41 best_loss=2.0381e+00 best_ppl=7.68                                                
Epoch 32 - |param|=3.25e+02 |g_param|=4.86e+05 loss=2.0245e+00 ppl=7.57                                                 
Validation - loss=1.9436e+00 ppl=6.98 best_loss=2.0034e+00 best_ppl=7.41                                                
Epoch 33 - |param|=3.25e+02 |g_param|=4.13e+05 loss=1.9998e+00 ppl=7.39                                                 
Validation - loss=1.9172e+00 ppl=6.80 best_loss=1.9436e+00 best_ppl=6.98                                                
Epoch 34 - |param|=3.25e+02 |g_param|=3.67e+05 loss=2.0111e+00 ppl=7.47                                                 
Validation - loss=1.8692e+00 ppl=6.48 best_loss=1.9172e+00 best_ppl=6.80                                                
Epoch 35 - |param|=3.25e+02 |g_param|=4.59e+05 loss=1.9815e+00 ppl=7.25                                                 
Validation - loss=1.8392e+00 ppl=6.29 best_loss=1.8692e+00 best_ppl=6.48                                                
Epoch 36 - |param|=3.25e+02 |g_param|=4.18e+05 loss=1.8111e+00 ppl=6.12                                                 
Validation - loss=1.8037e+00 ppl=6.07 best_loss=1.8392e+00 best_ppl=6.29                                                
Epoch 37 - |param|=3.25e+02 |g_param|=4.19e+05 loss=1.8813e+00 ppl=6.56                                                 
Validation - loss=1.7772e+00 ppl=5.91 best_loss=1.8037e+00 best_ppl=6.07                                                
Epoch 38 - |param|=3.25e+02 |g_param|=4.36e+05 loss=1.7941e+00 ppl=6.01                                                 
Validation - loss=1.7405e+00 ppl=5.70 best_loss=1.7772e+00 best_ppl=5.91                                                
Epoch 39 - |param|=3.25e+02 |g_param|=5.95e+05 loss=1.8217e+00 ppl=6.18                                                 
Validation - loss=1.7143e+00 ppl=5.55 best_loss=1.7405e+00 best_ppl=5.70                                                
Epoch 40 - |param|=3.25e+02 |g_param|=4.77e+05 loss=1.7821e+00 ppl=5.94                                                 
Validation - loss=1.6800e+00 ppl=5.37 best_loss=1.7143e+00 best_ppl=5.55                                                
Epoch 41 - |param|=3.25e+02 |g_param|=6.36e+05 loss=1.7733e+00 ppl=5.89                                                 
Validation - loss=1.6453e+00 ppl=5.18 best_loss=1.6800e+00 best_ppl=5.37                                                
Epoch 42 - |param|=3.25e+02 |g_param|=4.54e+05 loss=1.7589e+00 ppl=5.81                                                 
Validation - loss=1.6243e+00 ppl=5.07 best_loss=1.6453e+00 best_ppl=5.18                                                
Epoch 43 - |param|=3.25e+02 |g_param|=6.04e+05 loss=1.7074e+00 ppl=5.51                                                 
Validation - loss=1.6061e+00 ppl=4.98 best_loss=1.6243e+00 best_ppl=5.07                                                
Epoch 44 - |param|=3.25e+02 |g_param|=5.14e+05 loss=1.7115e+00 ppl=5.54                                                 
Validation - loss=1.5709e+00 ppl=4.81 best_loss=1.6061e+00 best_ppl=4.98                                                
Epoch 45 - |param|=3.25e+02 |g_param|=4.61e+05 loss=1.6848e+00 ppl=5.39                                                 
Validation - loss=1.5639e+00 ppl=4.78 best_loss=1.5709e+00 best_ppl=4.81                                                
Epoch 46 - |param|=3.25e+02 |g_param|=4.46e+05 loss=1.6608e+00 ppl=5.26                                                 
Validation - loss=1.5251e+00 ppl=4.60 best_loss=1.5639e+00 best_ppl=4.78                                                
Epoch 47 - |param|=3.25e+02 |g_param|=6.37e+05 loss=1.7082e+00 ppl=5.52                                                 
Validation - loss=1.5341e+00 ppl=4.64 best_loss=1.5251e+00 best_ppl=4.60                                                
Epoch 48 - |param|=3.25e+02 |g_param|=6.48e+05 loss=1.6572e+00 ppl=5.24                                                 
Validation - loss=1.4854e+00 ppl=4.42 best_loss=1.5251e+00 best_ppl=4.60                                                
Epoch 49 - |param|=3.25e+02 |g_param|=4.68e+05 loss=1.5589e+00 ppl=4.75                                                 
Validation - loss=1.4643e+00 ppl=4.32 best_loss=1.4854e+00 best_ppl=4.42                                                
Epoch 50 - |param|=3.25e+02 |g_param|=5.30e+05 loss=1.6060e+00 ppl=4.98                                                 
Validation - loss=1.4447e+00 ppl=4.24 best_loss=1.4643e+00 best_ppl=4.32                                                
Epoch 51 - |param|=3.25e+02 |g_param|=4.10e+05 loss=1.5644e+00 ppl=4.78                                                 
Validation - loss=1.4272e+00 ppl=4.17 best_loss=1.4447e+00 best_ppl=4.24                                                
Epoch 52 - |param|=3.25e+02 |g_param|=8.64e+05 loss=1.6041e+00 ppl=4.97                                                 
Validation - loss=1.4183e+00 ppl=4.13 best_loss=1.4272e+00 best_ppl=4.17                                                
Epoch 53 - |param|=3.25e+02 |g_param|=8.50e+05 loss=1.5042e+00 ppl=4.50                                                 
Validation - loss=1.3970e+00 ppl=4.04 best_loss=1.4183e+00 best_ppl=4.13                                                
Epoch 54 - |param|=3.25e+02 |g_param|=7.14e+05 loss=1.5166e+00 ppl=4.56                                                 
Validation - loss=1.4025e+00 ppl=4.07 best_loss=1.3970e+00 best_ppl=4.04                                                
Epoch 55 - |param|=3.25e+02 |g_param|=9.93e+05 loss=1.5297e+00 ppl=4.62                                                 
Validation - loss=1.3892e+00 ppl=4.01 best_loss=1.3970e+00 best_ppl=4.04                                                
Epoch 56 - |param|=3.25e+02 |g_param|=4.98e+05 loss=1.4576e+00 ppl=4.30                                                 
Validation - loss=1.3490e+00 ppl=3.85 best_loss=1.3892e+00 best_ppl=4.01                                                
Epoch 57 - |param|=3.25e+02 |g_param|=4.80e+05 loss=1.4172e+00 ppl=4.13                                                 
Validation - loss=1.3328e+00 ppl=3.79 best_loss=1.3490e+00 best_ppl=3.85                                                
Epoch 58 - |param|=3.25e+02 |g_param|=8.85e+05 loss=1.4701e+00 ppl=4.35                                                 
Validation - loss=1.3817e+00 ppl=3.98 best_loss=1.3328e+00 best_ppl=3.79                                                
Epoch 59 - |param|=3.25e+02 |g_param|=4.82e+05 loss=1.4762e+00 ppl=4.38                                                 
Validation - loss=1.3079e+00 ppl=3.70 best_loss=1.3328e+00 best_ppl=3.79                                                
Epoch 60 - |param|=3.25e+02 |g_param|=6.23e+05 loss=1.3903e+00 ppl=4.02                                                 
Validation - loss=1.3035e+00 ppl=3.68 best_loss=1.3079e+00 best_ppl=3.70                                                
Epoch 61 - |param|=3.25e+02 |g_param|=5.35e+05 loss=1.4136e+00 ppl=4.11                                                 
Validation - loss=1.2895e+00 ppl=3.63 best_loss=1.3035e+00 best_ppl=3.68                                                
Epoch 62 - |param|=3.25e+02 |g_param|=5.69e+05 loss=1.4178e+00 ppl=4.13                                                 
Validation - loss=1.2827e+00 ppl=3.61 best_loss=1.2895e+00 best_ppl=3.63                                                
Epoch 63 - |param|=3.25e+02 |g_param|=7.86e+05 loss=1.3857e+00 ppl=4.00                                                 
Validation - loss=1.2566e+00 ppl=3.51 best_loss=1.2827e+00 best_ppl=3.61                                                
Epoch 64 - |param|=3.25e+02 |g_param|=9.97e+05 loss=1.3740e+00 ppl=3.95                                                 
Validation - loss=1.2533e+00 ppl=3.50 best_loss=1.2566e+00 best_ppl=3.51                                                
Epoch 65 - |param|=3.25e+02 |g_param|=6.52e+05 loss=1.3935e+00 ppl=4.03                                                 
Validation - loss=1.2311e+00 ppl=3.42 best_loss=1.2533e+00 best_ppl=3.50                                                
Epoch 66 - |param|=3.25e+02 |g_param|=6.29e+05 loss=1.3697e+00 ppl=3.93                                                 
Validation - loss=1.2307e+00 ppl=3.42 best_loss=1.2311e+00 best_ppl=3.42                                                
Epoch 67 - |param|=3.25e+02 |g_param|=6.70e+05 loss=1.3169e+00 ppl=3.73                                                 
Validation - loss=1.2317e+00 ppl=3.43 best_loss=1.2307e+00 best_ppl=3.42                                                
Epoch 68 - |param|=3.25e+02 |g_param|=6.45e+05 loss=1.3208e+00 ppl=3.75                                                 
Validation - loss=1.2071e+00 ppl=3.34 best_loss=1.2307e+00 best_ppl=3.42                                                
Epoch 69 - |param|=3.25e+02 |g_param|=5.31e+05 loss=1.2987e+00 ppl=3.66                                                 
Validation - loss=1.1997e+00 ppl=3.32 best_loss=1.2071e+00 best_ppl=3.34                                                
Epoch 70 - |param|=3.25e+02 |g_param|=7.60e+05 loss=1.3522e+00 ppl=3.87                                                 
Validation - loss=1.2026e+00 ppl=3.33 best_loss=1.1997e+00 best_ppl=3.32                                                
Epoch 71 - |param|=3.25e+02 |g_param|=6.41e+05 loss=1.2807e+00 ppl=3.60                                                 
Validation - loss=1.1762e+00 ppl=3.24 best_loss=1.1997e+00 best_ppl=3.32                                                
Epoch 72 - |param|=3.25e+02 |g_param|=8.00e+05 loss=1.2959e+00 ppl=3.65                                                 
Validation - loss=1.1963e+00 ppl=3.31 best_loss=1.1762e+00 best_ppl=3.24                                                
Epoch 73 - |param|=3.25e+02 |g_param|=8.55e+05 loss=1.2693e+00 ppl=3.56                                                 
Validation - loss=1.1589e+00 ppl=3.19 best_loss=1.1762e+00 best_ppl=3.24                                                
Epoch 74 - |param|=3.25e+02 |g_param|=6.06e+05 loss=1.2534e+00 ppl=3.50                                                 
Validation - loss=1.1568e+00 ppl=3.18 best_loss=1.1589e+00 best_ppl=3.19                                                
Epoch 75 - |param|=3.25e+02 |g_param|=5.67e+05 loss=1.2109e+00 ppl=3.36                                                 
Validation - loss=1.1514e+00 ppl=3.16 best_loss=1.1568e+00 best_ppl=3.18                                                
Epoch 76 - |param|=3.25e+02 |g_param|=5.90e+05 loss=1.2135e+00 ppl=3.37                                                 
Validation - loss=1.1369e+00 ppl=3.12 best_loss=1.1514e+00 best_ppl=3.16                                                
Epoch 77 - |param|=3.25e+02 |g_param|=1.14e+06 loss=1.2330e+00 ppl=3.43                                                 
Validation - loss=1.1424e+00 ppl=3.13 best_loss=1.1369e+00 best_ppl=3.12                                                
Epoch 78 - |param|=3.25e+02 |g_param|=6.00e+05 loss=1.2167e+00 ppl=3.38                                                 
Validation - loss=1.1178e+00 ppl=3.06 best_loss=1.1369e+00 best_ppl=3.12                                                
Epoch 79 - |param|=3.26e+02 |g_param|=6.72e+05 loss=1.2441e+00 ppl=3.47                                                 
Validation - loss=1.1296e+00 ppl=3.09 best_loss=1.1178e+00 best_ppl=3.06                                                
Epoch 80 - |param|=3.26e+02 |g_param|=6.32e+05 loss=1.2262e+00 ppl=3.41                                                 
Validation - loss=1.1037e+00 ppl=3.02 best_loss=1.1178e+00 best_ppl=3.06                                                
Epoch 81 - |param|=3.26e+02 |g_param|=1.01e+06 loss=1.2459e+00 ppl=3.48                                                 
Validation - loss=1.1054e+00 ppl=3.02 best_loss=1.1037e+00 best_ppl=3.02                                                
Epoch 82 - |param|=3.26e+02 |g_param|=5.56e+05 loss=1.2075e+00 ppl=3.35                                                 
Validation - loss=1.0936e+00 ppl=2.99 best_loss=1.1037e+00 best_ppl=3.02                                                
Epoch 83 - |param|=3.26e+02 |g_param|=7.02e+05 loss=1.2169e+00 ppl=3.38                                                 
Validation - loss=1.0817e+00 ppl=2.95 best_loss=1.0936e+00 best_ppl=2.99                                                
Epoch 84 - |param|=3.26e+02 |g_param|=6.45e+05 loss=1.2203e+00 ppl=3.39                                                 
Validation - loss=1.0712e+00 ppl=2.92 best_loss=1.0817e+00 best_ppl=2.95                                                
Epoch 85 - |param|=3.26e+02 |g_param|=6.49e+05 loss=1.2123e+00 ppl=3.36                                                 
Validation - loss=1.0651e+00 ppl=2.90 best_loss=1.0712e+00 best_ppl=2.92                                                
Epoch 86 - |param|=3.26e+02 |g_param|=7.07e+05 loss=1.1354e+00 ppl=3.11                                                 
Validation - loss=1.0584e+00 ppl=2.88 best_loss=1.0651e+00 best_ppl=2.90                                                
Epoch 87 - |param|=3.26e+02 |g_param|=7.25e+05 loss=1.1192e+00 ppl=3.06                                                 
Validation - loss=1.0541e+00 ppl=2.87 best_loss=1.0584e+00 best_ppl=2.88                                                
Epoch 88 - |param|=3.26e+02 |g_param|=4.35e+05 loss=1.1784e+00 ppl=3.25                                                 
Validation - loss=1.0527e+00 ppl=2.87 best_loss=1.0541e+00 best_ppl=2.87                                                
Epoch 89 - |param|=3.26e+02 |g_param|=4.24e+05 loss=1.1494e+00 ppl=3.16                                                 
Validation - loss=1.0844e+00 ppl=2.96 best_loss=1.0527e+00 best_ppl=2.87                                                
Epoch 90 - |param|=3.26e+02 |g_param|=2.64e+05 loss=1.1533e+00 ppl=3.17                                                 
Validation - loss=1.0427e+00 ppl=2.84 best_loss=1.0527e+00 best_ppl=2.87                                                
Epoch 91 - |param|=3.26e+02 |g_param|=4.27e+05 loss=1.1444e+00 ppl=3.14                                                 
Validation - loss=1.0406e+00 ppl=2.83 best_loss=1.0427e+00 best_ppl=2.84                                                
Epoch 92 - |param|=3.26e+02 |g_param|=3.91e+05 loss=1.1675e+00 ppl=3.21                                                 
Validation - loss=1.0322e+00 ppl=2.81 best_loss=1.0406e+00 best_ppl=2.83                                                
Epoch 93 - |param|=3.26e+02 |g_param|=2.57e+05 loss=1.1344e+00 ppl=3.11                                                 
Validation - loss=1.0223e+00 ppl=2.78 best_loss=1.0322e+00 best_ppl=2.81                                                
Epoch 94 - |param|=3.26e+02 |g_param|=3.79e+05 loss=1.1266e+00 ppl=3.09                                                 
Validation - loss=1.0179e+00 ppl=2.77 best_loss=1.0223e+00 best_ppl=2.78                                                
Epoch 95 - |param|=3.26e+02 |g_param|=5.29e+05 loss=1.1075e+00 ppl=3.03                                                 
Validation - loss=1.0355e+00 ppl=2.82 best_loss=1.0179e+00 best_ppl=2.77                                                
Epoch 96 - |param|=3.26e+02 |g_param|=6.10e+05 loss=1.1105e+00 ppl=3.04                                                 
Validation - loss=1.0095e+00 ppl=2.74 best_loss=1.0179e+00 best_ppl=2.77                                                
Epoch 97 - |param|=3.26e+02 |g_param|=3.96e+05 loss=1.1144e+00 ppl=3.05                                                 
Validation - loss=1.0273e+00 ppl=2.79 best_loss=1.0095e+00 best_ppl=2.74                                                
Epoch 98 - |param|=3.26e+02 |g_param|=2.81e+05 loss=1.1142e+00 ppl=3.05                                                 
Validation - loss=1.0126e+00 ppl=2.75 best_loss=1.0095e+00 best_ppl=2.74                                                
Epoch 99 - |param|=3.26e+02 |g_param|=3.89e+05 loss=1.0864e+00 ppl=2.96                                                 
Validation - loss=9.9745e-01 ppl=2.71 best_loss=1.0095e+00 best_ppl=2.74                                                
Epoch 100 - |param|=3.26e+02 |g_param|=3.73e+05 loss=1.1342e+00 ppl=3.11                                                
Validation - loss=1.0233e+00 ppl=2.78 best_loss=9.9745e-01 best_ppl=2.71                                                

real	36m30.664s
user	36m22.422s
sys	0m7.062s
(simple-nmt) ye@:~/exp/simple-nmt$ 
```

testing/evaluation for rk-my, RL fine-tuning, 30-70 model ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/100epoch/baseline/rkmy$ time ./test-eval-loop.sh 
Evaluation result for the model: transformer-rl-30to100model-rkmy.100.1.13-3.11.1.02-2.78.pth
BLEU = 52.70, 74.6/59.8/46.9/36.9 (BP=1.000, ratio=1.093, hyp_len=25699, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.30.2.13-8.39.2.04-7.68.pth
BLEU = 24.32, 53.7/32.2/18.7/10.8 (BP=1.000, ratio=1.132, hyp_len=26608, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.31.2.06-7.88.2.00-7.41.pth
BLEU = 26.00, 55.7/33.8/20.1/12.1 (BP=1.000, ratio=1.107, hyp_len=26033, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.32.2.02-7.57.1.94-6.98.pth
BLEU = 28.11, 58.2/36.1/21.9/13.6 (BP=1.000, ratio=1.067, hyp_len=25090, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.33.2.00-7.39.1.92-6.80.pth
BLEU = 27.99, 58.0/36.1/21.9/13.4 (BP=1.000, ratio=1.087, hyp_len=25543, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.34.2.01-7.47.1.87-6.48.pth
BLEU = 30.87, 61.5/39.0/24.3/15.6 (BP=1.000, ratio=1.028, hyp_len=24169, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.35.1.98-7.25.1.84-6.29.pth
BLEU = 30.34, 60.2/38.4/24.1/15.2 (BP=1.000, ratio=1.072, hyp_len=25197, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.36.1.81-6.12.1.80-6.07.pth
BLEU = 31.01, 60.5/38.9/24.7/15.9 (BP=1.000, ratio=1.078, hyp_len=25343, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.37.1.88-6.56.1.78-5.91.pth
BLEU = 31.49, 61.1/39.7/25.2/16.1 (BP=1.000, ratio=1.080, hyp_len=25387, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.38.1.79-6.01.1.74-5.70.pth
BLEU = 34.30, 64.1/42.5/27.7/18.4 (BP=1.000, ratio=1.030, hyp_len=24224, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.39.1.82-6.18.1.71-5.55.pth
BLEU = 34.56, 64.5/42.8/28.0/18.5 (BP=1.000, ratio=1.033, hyp_len=24290, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.40.1.78-5.94.1.68-5.37.pth
BLEU = 34.80, 63.4/42.6/28.4/19.1 (BP=1.000, ratio=1.063, hyp_len=24982, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.41.1.77-5.89.1.65-5.18.pth
BLEU = 34.56, 62.9/42.4/28.2/18.9 (BP=1.000, ratio=1.089, hyp_len=25609, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.42.1.76-5.81.1.62-5.07.pth
BLEU = 36.09, 65.0/44.2/29.5/20.0 (BP=1.000, ratio=1.052, hyp_len=24726, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.43.1.71-5.51.1.61-4.98.pth
BLEU = 35.96, 64.4/44.0/29.6/19.9 (BP=1.000, ratio=1.074, hyp_len=25257, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.44.1.71-5.54.1.57-4.81.pth
BLEU = 36.87, 64.9/44.8/30.4/20.9 (BP=1.000, ratio=1.069, hyp_len=25141, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.45.1.68-5.39.1.56-4.78.pth
BLEU = 37.00, 65.2/45.0/30.6/20.9 (BP=1.000, ratio=1.075, hyp_len=25271, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.46.1.66-5.26.1.53-4.60.pth
BLEU = 38.24, 66.1/46.1/31.8/22.1 (BP=1.000, ratio=1.067, hyp_len=25081, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.47.1.71-5.52.1.53-4.64.pth
BLEU = 37.59, 65.5/45.8/31.3/21.3 (BP=1.000, ratio=1.084, hyp_len=25494, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.48.1.66-5.24.1.49-4.42.pth
BLEU = 41.18, 69.0/48.9/34.6/24.6 (BP=1.000, ratio=1.028, hyp_len=24156, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.49.1.56-4.75.1.46-4.32.pth
BLEU = 41.76, 69.8/49.7/35.1/25.0 (BP=1.000, ratio=1.020, hyp_len=23981, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.50.1.61-4.98.1.44-4.24.pth
BLEU = 41.37, 68.8/49.2/34.8/24.9 (BP=1.000, ratio=1.048, hyp_len=24647, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.51.1.56-4.78.1.43-4.17.pth
BLEU = 41.31, 68.7/49.2/34.8/24.8 (BP=1.000, ratio=1.055, hyp_len=24808, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.52.1.60-4.97.1.42-4.13.pth
BLEU = 42.77, 70.0/50.5/36.2/26.1 (BP=1.000, ratio=1.031, hyp_len=24248, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.53.1.50-4.50.1.40-4.04.pth
BLEU = 42.90, 69.8/50.6/36.4/26.3 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.54.1.52-4.56.1.40-4.07.pth
BLEU = 40.75, 67.6/48.9/34.5/24.2 (BP=1.000, ratio=1.086, hyp_len=25523, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.55.1.53-4.62.1.39-4.01.pth
BLEU = 45.61, 72.4/53.1/38.9/29.0 (BP=1.000, ratio=1.006, hyp_len=23658, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.56.1.46-4.30.1.35-3.85.pth
BLEU = 43.68, 69.9/51.4/37.3/27.1 (BP=1.000, ratio=1.059, hyp_len=24885, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.57.1.42-4.13.1.33-3.79.pth
BLEU = 44.24, 69.9/51.6/37.8/28.1 (BP=1.000, ratio=1.064, hyp_len=25012, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.58.1.47-4.35.1.38-3.98.pth
BLEU = 41.47, 67.8/49.6/35.4/24.9 (BP=1.000, ratio=1.106, hyp_len=26010, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.59.1.48-4.38.1.31-3.70.pth
BLEU = 45.22, 71.1/52.8/38.8/28.7 (BP=1.000, ratio=1.049, hyp_len=24664, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.60.1.39-4.02.1.30-3.68.pth
BLEU = 45.28, 71.1/52.9/38.9/28.8 (BP=1.000, ratio=1.059, hyp_len=24899, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.61.1.41-4.11.1.29-3.63.pth
BLEU = 44.78, 69.9/52.0/38.5/28.7 (BP=1.000, ratio=1.077, hyp_len=25314, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.62.1.42-4.13.1.28-3.61.pth
BLEU = 47.01, 72.6/54.5/40.6/30.4 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.63.1.39-4.00.1.26-3.51.pth
BLEU = 46.44, 71.8/54.0/40.1/29.9 (BP=1.000, ratio=1.058, hyp_len=24884, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.64.1.37-3.95.1.25-3.50.pth
BLEU = 46.68, 72.0/54.3/40.4/30.1 (BP=1.000, ratio=1.056, hyp_len=24823, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.65.1.39-4.03.1.23-3.42.pth
BLEU = 46.97, 72.1/54.3/40.5/30.6 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.66.1.37-3.93.1.23-3.42.pth
BLEU = 48.82, 74.0/56.3/42.4/32.2 (BP=1.000, ratio=1.031, hyp_len=24246, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.67.1.32-3.73.1.23-3.43.pth
BLEU = 50.48, 75.1/57.5/44.1/34.1 (BP=1.000, ratio=1.014, hyp_len=23835, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.68.1.32-3.75.1.21-3.34.pth
BLEU = 49.96, 74.6/57.1/43.6/33.5 (BP=1.000, ratio=1.028, hyp_len=24178, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.69.1.30-3.66.1.20-3.32.pth
BLEU = 48.06, 72.4/55.3/41.9/31.8 (BP=1.000, ratio=1.068, hyp_len=25098, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.70.1.35-3.87.1.20-3.33.pth
BLEU = 48.91, 73.6/56.4/42.7/32.3 (BP=1.000, ratio=1.048, hyp_len=24641, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.71.1.28-3.60.1.18-3.24.pth
BLEU = 50.24, 74.2/57.2/44.0/34.1 (BP=1.000, ratio=1.043, hyp_len=24531, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.72.1.30-3.65.1.20-3.31.pth
BLEU = 48.30, 72.9/56.0/42.1/31.6 (BP=1.000, ratio=1.072, hyp_len=25204, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.73.1.27-3.56.1.16-3.19.pth
BLEU = 51.40, 75.1/58.3/45.1/35.4 (BP=1.000, ratio=1.034, hyp_len=24318, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.74.1.25-3.50.1.16-3.18.pth
BLEU = 49.45, 73.5/56.9/43.3/33.0 (BP=1.000, ratio=1.060, hyp_len=24921, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.75.1.21-3.36.1.15-3.16.pth
BLEU = 48.43, 72.6/55.8/42.2/32.2 (BP=1.000, ratio=1.080, hyp_len=25380, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.76.1.21-3.37.1.14-3.12.pth
BLEU = 51.25, 74.7/58.0/45.0/35.4 (BP=1.000, ratio=1.046, hyp_len=24588, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.77.1.23-3.43.1.14-3.13.pth
BLEU = 50.16, 74.5/57.7/44.0/33.5 (BP=1.000, ratio=1.054, hyp_len=24778, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.78.1.22-3.38.1.12-3.06.pth
BLEU = 50.95, 74.7/58.1/44.8/34.7 (BP=1.000, ratio=1.056, hyp_len=24831, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.79.1.24-3.47.1.13-3.09.pth
BLEU = 49.95, 74.0/57.6/43.8/33.3 (BP=1.000, ratio=1.071, hyp_len=25172, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.80.1.23-3.41.1.10-3.02.pth
BLEU = 52.24, 75.1/59.0/46.1/36.5 (BP=1.000, ratio=1.053, hyp_len=24745, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.81.1.25-3.48.1.11-3.02.pth
BLEU = 52.09, 74.8/58.8/45.9/36.4 (BP=1.000, ratio=1.055, hyp_len=24797, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.82.1.21-3.35.1.09-2.99.pth
BLEU = 51.66, 74.6/58.7/45.6/35.7 (BP=1.000, ratio=1.063, hyp_len=24981, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.83.1.22-3.38.1.08-2.95.pth
BLEU = 52.96, 75.7/59.8/46.9/37.1 (BP=1.000, ratio=1.052, hyp_len=24740, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.84.1.22-3.39.1.07-2.92.pth
BLEU = 53.44, 76.1/60.2/47.4/37.6 (BP=1.000, ratio=1.048, hyp_len=24635, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.85.1.21-3.36.1.07-2.90.pth
BLEU = 53.62, 76.2/60.5/47.6/37.7 (BP=1.000, ratio=1.046, hyp_len=24596, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.86.1.14-3.11.1.06-2.88.pth
BLEU = 53.99, 76.5/60.7/47.9/38.2 (BP=1.000, ratio=1.045, hyp_len=24559, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.87.1.12-3.06.1.05-2.87.pth
BLEU = 53.98, 76.5/60.8/48.0/38.1 (BP=1.000, ratio=1.045, hyp_len=24570, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.88.1.18-3.25.1.05-2.87.pth
BLEU = 54.86, 77.5/61.7/48.7/38.8 (BP=1.000, ratio=1.031, hyp_len=24235, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.89.1.15-3.16.1.08-2.96.pth
BLEU = 50.74, 73.8/58.2/44.8/34.5 (BP=1.000, ratio=1.089, hyp_len=25607, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.90.1.15-3.17.1.04-2.84.pth
BLEU = 52.22, 74.4/59.1/46.4/36.5 (BP=1.000, ratio=1.083, hyp_len=25463, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.91.1.14-3.14.1.04-2.83.pth
BLEU = 53.12, 75.2/60.1/47.2/37.3 (BP=1.000, ratio=1.072, hyp_len=25192, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.92.1.17-3.21.1.03-2.81.pth
BLEU = 52.64, 74.5/59.4/46.8/37.1 (BP=1.000, ratio=1.085, hyp_len=25514, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.93.1.13-3.11.1.02-2.78.pth
BLEU = 54.93, 77.1/61.7/48.9/39.1 (BP=1.000, ratio=1.050, hyp_len=24675, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.94.1.13-3.09.1.02-2.77.pth
BLEU = 54.51, 76.7/61.4/48.5/38.6 (BP=1.000, ratio=1.054, hyp_len=24784, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.95.1.11-3.03.1.04-2.82.pth
BLEU = 54.95, 77.4/62.0/48.9/38.9 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.96.1.11-3.04.1.01-2.74.pth
BLEU = 54.20, 76.0/60.8/48.3/38.6 (BP=1.000, ratio=1.067, hyp_len=25089, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.97.1.11-3.05.1.03-2.79.pth
BLEU = 56.72, 78.4/63.2/50.8/41.2 (BP=1.000, ratio=1.030, hyp_len=24207, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.98.1.11-3.05.1.01-2.75.pth
BLEU = 54.46, 76.6/61.5/48.5/38.5 (BP=1.000, ratio=1.065, hyp_len=25026, ref_len=23509)
Evaluation result for the model: transformer-rl-30to100model-rkmy.99.1.09-2.96.1.00-2.71.pth
BLEU = 56.39, 77.9/62.9/50.5/40.9 (BP=1.000, ratio=1.042, hyp_len=24495, ref_len=23509)

real	41m29.688s
user	40m46.500s
sys	1m31.375s
(simple-nmt) ye@:~/exp/simple-nmt/model/rl/transformer/100epoch/baseline/rkmy$
```

rk-my, Transformer Baseline က 25.23 ...  
rk-my, RL fine-tuning 30-70 model ရဲ့ best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-rl-30to100model-rkmy.97.1.11-3.05.1.03-2.79.pth
BLEU = 56.72, 78.4/63.2/50.8/41.2 (BP=1.000, ratio=1.030, hyp_len=24207, ref_len=23509)
```


## seq2seq (40, 50, 60, 70 Baselines)

Note: ./model/seq2seq/baseline/myrk-100epoch/ path က တကယ်တမ်းက 30 epoch for baseline + 70 epoch for RL fine-tuning  

**for my-rk language pair:**   

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.pth;  

Baseline model best BLEU:   

```
Evaluation result for the model: seq-model-myrk.40.0.55-1.74.0.89-2.44.pth
BLEU = 70.40, 86.1/74.9/65.7/58.0 (BP=1.000, ratio=1.010, hyp_len=23388, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 50 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.pth;  

Best core of seq2seq 50 model က ...  

```
Evaluation result for the model: seq-model-myrk.48.0.43-1.54.0.76-2.14.pth
BLEU = 73.15, 87.2/77.1/68.9/61.8 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 60 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.pth;  

Best score of seq2seq 60 model က ...  

```
Evaluation result for the model: seq-model-myrk.55.0.29-1.33.0.65-1.91.pth
BLEU = 75.30, 88.3/79.0/71.3/64.7 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 70 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.pth;  

my-rk seq2seq 70 epoch model ရဲ့ Best score က  

```
Evaluation result for the model: seq-model-myrk.61.0.33-1.40.0.77-2.17.pth
BLEU = 74.36, 87.9/78.2/70.2/63.3 (BP=1.000, ratio=1.019, hyp_len=23602, ref_len=23160)
```

**for rk-my language pair:**   

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.pth;  

rk-my, seq2seq, 40 Best Score:  

```
Evaluation result for the model: seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth
BLEU = 69.39, 85.4/74.4/64.4/56.6 (BP=1.000, ratio=1.022, hyp_len=24037, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 50 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.pth;  

rk-my, seq2seq, 50 Best Score:  

```
Evaluation result for the model: seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth
BLEU = 74.04, 87.3/78.1/69.8/63.2 (BP=1.000, ratio=1.036, hyp_len=24361, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 60 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.pth;  

rk-my, seq2seq, 60 Best Score:  

```
Evaluation result for the model: seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth
BLEU = 72.06, 86.3/76.5/67.5/60.5 (BP=1.000, ratio=1.032, hyp_len=24261, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 64 --n_epochs 70 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.pth;  


rk-my, seq2seq, 70 Best Score:  

```
Evaluation result for the model: seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth
BLEU = 74.84, 87.8/78.8/70.6/64.3 (BP=1.000, ratio=1.031, hyp_len=24242, ref_len=23509)
```

## Transformer (40, 50, 60, 70 Baselines)

**for my-rk language pair**  

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.pth  

my-rk, transformer, 40 epoch ရဲ့ Best BLEU score:  

```
Evaluation result for the model: myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth
BLEU = 35.33, 65.7/43.6/28.8/18.9 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 50 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-50epoch/myrk-transformer-model.pth  

my-rk, transformer, 50 epoch ရဲ့ Best BLEU score:  

```
Evaluation result for the model: myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth
BLEU = 40.85, 69.4/48.7/34.3/24.0 (BP=1.000, ratio=1.028, hyp_len=23819, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 60 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-60epoch/myrk-transformer-model.pth  

my-rk, transformer, 60 epoch ရဲ့ Best BLEU score:  

```
Evaluation result for the model: myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth
BLEU = 47.13, 73.5/54.8/40.7/30.1 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 70 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-70epoch/myrk-transformer-model.pth  

my-rk, transformer, 70 epoch ရဲ့ Best BLEU score:  

```
Evaluation result for the model: myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth
BLEU = 50.51, 75.0/57.8/44.3/33.9 (BP=1.000, ratio=1.057, hyp_len=24476, ref_len=23160)
```

**for rk-my language pair**  

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.pth  

transformer, 40 epoch, rk-my မော်ဒယ်ရဲ့ အကောင်းဆုံး BLEU က  

```
Evaluation result for the model: rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth
BLEU = 34.17, 63.5/42.3/27.8/18.3 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 50 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.pth  

Transformer, rk-my, 50 epoch model ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth
BLEU = 40.40, 68.8/48.5/33.7/23.7 (BP=1.000, ratio=1.025, hyp_len=24088, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 60 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.pth  

Transformer, rk-my, 60 epoch ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth
BLEU = 45.70, 71.8/53.2/39.1/29.2 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
```

time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy --gpu_id 0 --batch_size 16 --n_epochs 70 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.pth  

Transformer, rk-my, 70 epoch မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth
BLEU = 51.15, 75.4/58.2/44.7/34.9 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
```

အထက်မှာ ဖော်ပြထားခဲ့တာက Simple NMT ကို installation လုပ်တဲ့အဆင့်ကနေ စပြီးတော့၊ test-run လုပ်ခဲ့တာတွေပါ အပါအဝင်ပါ။ Experiment လုပ်ထားတဲ့ running log ကိုလည်း အကုန် မှတ်ထားခဲ့တာမို့ follow လုပ်ရင်တော့ နည်းနည်းပင်ပန်းပါလိမ့်မယ်။ Run ခဲ့တဲ့ command တွေနဲ့ အခုချိန်ထိလုပ်ခဲ့တဲ့ အဓိက experiment တွေရဲ့ Result Summary ကတော့ အောက်ပါ အတိုင်းပါပဲ။  
(simple-NMT framework ကို သုံးဖူးပြီးသားသူ၊ နားလည်ပြီးသားသူ ဆိုရင်တော့ ဒီနေရာကနေပဲ စကြည့်ပါလို့ အကြံပြုချင်ပါတယ်)    

## Reinforcement Learning
### seq2seq

**for my-rk language pair**  

myrk, Baseline model best score: BLEU = 68.10  
myrk, RL Fine-tuning best score: BLEU = 74.87 (seq-rl-model-myrk.81.0.25-1.28.0.70-2.00.pth မော်ဒယ်ရဲ့)  

Evaluation result for the model: seq-rl-model-myrk.81.0.25-1.28.0.70-2.00.pth  
BLEU = 74.87, 87.6/78.5/70.9/64.5 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)  

baseline model က 40 epoch ဆိုရင် ဒီဘက် RL မော်ဒယ်ကိုလည်း 40 ဆိုတဲ့ ဖိုလ်ဒါအောက်မှာပဲ သိမ်းခဲ့တယ်။ တိုက်ကြည့်ရတာ လွယ်အောင်လို့...  
တကယ်တမ်းက basline က 40 epoch မို့လို့ 100 epoch က total epoch မို့လို့... RL မော်ဒယ်က 60 epoch ပါ  

time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth --model_fn ./model/rl/seq2seq/myrk-40epoch/seq-rl-model-myrk.pth --init_epoch 40 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

best score က  seq2seq 40 model (Baseline) က seq-model-myrk.40.0.55-1.74.0.89-2.44.pth: BLEU = 70.40   
RL, my-rk, 40-60 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: seq-rl-model-myrk.98.0.20-1.22.0.75-2.12.pth
BLEU = 74.53, 87.5/78.3/70.5/63.8 (BP=1.000, ratio=1.030, hyp_len=23845, ref_len=23160)
```

for 50-50 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-50epoch/seq-model-myrk.48.0.43-1.54.0.76-2.14.pth --model_fn ./model/rl/seq2seq/myrk-50epoch/seq-rl-model-myrk.pth --init_epoch 48 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

seq2seq 50 model (baseline), seq-model-myrk.48.0.43-1.54.0.76-2.14.pth က BLEU = 73.15  
RL, my-rk, 50-50 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: seq-rl-model-myrk.83.0.24-1.27.0.73-2.08.pth
BLEU = 74.72, 87.7/78.5/70.7/64.0 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
```

for 60-40 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-60epoch/seq-model-myrk.55.0.29-1.33.0.65-1.91.pth --model_fn ./model/rl/seq2seq/myrk-60epoch/seq-rl-model-myrk.pth --init_epoch 55 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

Baseline ရဲ့ အကောင်းဆုံး မော်ဒယ် ရဲ့ score က seq-model-myrk.55.0.29-1.33.0.65-1.91.pth: BLEU = 75.30  
RL ရဲ့ Best Score ပေးတဲ့ မော်ဒယ်က seq-rl-model-myrk.66.0.25-1.28.0.64-1.91.pth:  

```
Evaluation result for the model: seq-rl-model-myrk.66.0.25-1.28.0.64-1.91.pth
BLEU = 75.11, 88.0/78.7/71.1/64.6 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
```

for 70-30 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/myrk-70epoch/seq-model-myrk.61.0.33-1.40.0.77-2.17.pth --model_fn ./model/rl/seq2seq/myrk-70epoch/seq-rl-model-myrk.pth --init_epoch 61 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

seq2seq, my-rk, 70 epoch model or Baseline က seq-model-myrk.61.0.33-1.40.0.77-2.17.pth, BLEU = 74.36  
RL, my-rk, 30-70 ရဲ့ best score က  

```
Evaluation result for the model: seq-rl-model-myrk.98.0.21-1.24.0.76-2.13.pth
BLEU = 75.50, 88.2/79.1/71.6/65.1 (BP=1.000, ratio=1.023, hyp_len=23701, ref_len=23160)
```

**for rk-my language pair**  

for 30-70 model:  

Baseline Best Score က BLEU = 59.48  
rk-my အတွက် RL fine-tuning 100epoch မော်ဒယ်ရဲ့ best score က BLEU = 74.74  

Evaluation result for the model: seq-rl-model-rkmy.92.0.24-1.27.0.72-2.06.pth  
BLEU = 74.74, 87.6/78.6/70.6/64.3 (BP=1.000, ratio=1.033, hyp_len=24290, ref_len=23509)  

for 40-60 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-40epoch/seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth --model_fn ./model/rl/seq2seq/rkmy-40epoch/seq-rl-model-rkmy.pth --init_epoch 39 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: seq-model-rkmy.39.0.59-1.81.0.83-2.30.pth, BLEU = 69.39  
RL, rk-my, 40-60 model Best Score:  

```
Evaluation result for the model: seq-rl-model-rkmy.74.0.29-1.33.0.75-2.11.pth
BLEU = 74.98, 88.0/79.0/70.7/64.3 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
```

for 50-50 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-50epoch/seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth --model_fn ./model/rl/seq2seq/rkmy-50epoch/seq-rl-model-rkmy.pth --init_epoch 49 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: seq2seq, rk-my, 50 epoch, seq-model-rkmy.49.0.33-1.39.0.64-1.90.pth: BLEU = 74.04  
RL, rk-my, 50-50 model Best score:  

```
Evaluation result for the model: seq-rl-model-rkmy.98.0.15-1.16.0.65-1.92.pth
BLEU = 74.91, 87.7/78.8/70.8/64.4 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
```

for 60-40 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-60epoch/seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth --model_fn ./model/rl/seq2seq/rkmy-60epoch/seq-rl-model-rkmy.pth --init_epoch 58 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: seq-model-rkmy.58.0.39-1.48.0.81-2.24.pth, BLEU = 72.06  
RL rk-my, 60-40 model ရဲ့ အကောင်းဆုံး BLEU score က ...  

```
Evaluation result for the model: seq-rl-model-rkmy.84.0.28-1.33.0.76-2.14.pth
BLEU = 74.52, 87.6/78.5/70.2/63.9 (BP=1.000, ratio=1.029, hyp_len=24198, ref_len=23509)
```

for 70-30 model:  

time python continue_train.py --load_fn ./model/seq2seq/baseline/rkmy-70epoch/seq-model-rkmy.67.0.27-1.31.0.66-1.93.pth --model_fn ./model/rl/seq2seq/rkmy-70epoch/seq-rl-model-rkmy.pth --init_epoch 67 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100  

Baseline က : BLEU = 74.84  
RL 70-30, rk-my best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: seq-rl-model-rkmy.93.0.19-1.21.0.69-2.00.pth
BLEU = 74.48, 87.5/78.5/70.2/63.8 (BP=1.000, ratio=1.036, hyp_len=24351, ref_len=23509)
```

### Transformer

**for my-rk language pair**  

30 epoch Transformer မော်ဒယ်ရဲ့ baseline က 25.29  
BLEU = 25.29, 57.4/33.7/19.5/10.9 (BP=1.000, ratio=1.055, hyp_len=24426, ref_len=23160)  
my-rk, 30-70 RL fine-tuning မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က 58.69 ရတယ်...  

Evaluation result for the model: transformer-rl-30to100model-myrk.97.1.11-3.03.1.03-2.80.pth  
BLEU = 58.69, 80.5/64.9/52.8/43.0 (BP=1.000, ratio=1.015, hyp_len=23498, ref_len=23160)  

time python continue_train.py --load_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.39.1.86-6.41.1.77-5.87.pth --model_fn ./model/rl/transformer/myrk-40epoch/transformer-rl-myrk.pth --init_epoch 39 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: my-rk, transformer, 40 epoch ရဲ့ Best BLEU score: 35.33  
RL, my-rk, 40-60 model ရဲ့ အများဆုံးက  

```
Evaluation result for the model: transformer-rl-myrk.98.1.07-2.92.1.03-2.81.pth
BLEU = 59.13, 81.2/65.4/53.1/43.4 (BP=1.000, ratio=1.006, hyp_len=23292, ref_len=23160)
```

time python continue_train.py --load_fn ./model/transformer/baseline/myrk-50epoch/myrk-transformer-model.47.1.70-5.47.1.56-4.78.pth --model_fn ./model/rl/transformer/myrk-50epoch/transformer-rl-myrk.pth --init_epoch 47 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: my-rk, transformer, 50 epoch ရဲ့ Best BLEU score: BLEU = 40.85  
RL my-rk, 50-50 model ရဲ့ best score က ...  

```
Evaluation result for the model: transformer-rl-myrk.88.1.16-3.18.1.06-2.88.pth
BLEU = 56.79, 79.3/63.4/50.8/40.7 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
```

time python continue_train.py --load_fn ./model/transformer/baseline/myrk-60epoch/myrk-transformer-model.59.1.49-4.43.1.33-3.78.pth --model_fn ./model/rl/transformer/myrk-60epoch/transformer-rl-myrk.pth --init_epoch 59 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: my-rk, transformer, 60 epoch ရဲ့ Best BLEU score: BLEU = 47.13  
RL, my-rk, 60-40 model ရဲ့ အကောင်းဆုံး best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-rl-myrk.97.1.09-2.96.1.01-2.73.pth
BLEU = 58.22, 80.2/64.7/52.3/42.4 (BP=1.000, ratio=1.022, hyp_len=23667, ref_len=23160)
```

time python continue_train.py --load_fn ./model/transformer/baseline/myrk-70epoch/myrk-transformer-model.70.1.27-3.56.1.17-3.22.pth --model_fn ./model/rl/transformer/myrk-70epoch/transformer-rl-myrk.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: my-rk, transformer, 70 epoch ရဲ့ Best BLEU score: BLEU = 50.51  
RL, my-rk, 70-30 model ရဲ့ အကောင်းဆုံး BLEU score က  

```
Evaluation result for the model: transformer-rl-myrk.93.1.11-3.05.1.01-2.75.pth
BLEU = 58.20, 80.4/64.7/52.2/42.2 (BP=1.000, ratio=1.020, hyp_len=23617, ref_len=23160)
```

**for rk-my language pair**  

rk-my, Transformer Baseline က 25.23 ...  
rk-my, RL fine-tuning 30-70 model ရဲ့ best score က အောက်ပါအတိုင်း...  

Evaluation result for the model: transformer-rl-30to100model-rkmy.97.1.11-3.05.1.03-2.79.pth  
BLEU = 56.72, 78.4/63.2/50.8/41.2 (BP=1.000, ratio=1.030, hyp_len=24207, ref_len=23509)  

time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-40epoch/rkmy-transformer-model.39.1.89-6.62.1.69-5.40.pth --model_fn ./model/rl/transformer/rkmy-40epoch/transformer-rl-myrk.pth --init_epoch 39 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: rk-my, transformer, 40 epoch ရဲ့ Best BLEU Score = 34.17  
RL, rk-my, 40-60 model ရဲ့ အကောင်းဆုံး BLEU score က   

```
Evaluation result for the model: transformer-rl-myrk.100.1.10-3.00.0.96-2.62.pth
BLEU = 56.95, 78.4/63.4/51.0/41.5 (BP=1.000, ratio=1.038, hyp_len=24393, ref_len=23509)
```

time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-50epoch/rkmy-transformer-model.46.1.62-5.07.1.51-4.53.pth --model_fn ./model/rl/transformer/rkmy-50epoch/transformer-rl-myrk.pth --init_epoch 46 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: rk-my, transformer, 50 epoch ရဲ့ Best BLEU Score = 40.40  
RL, rk-my, 50-50 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: transformer-rl-myrk.99.1.06-2.89.0.99-2.70.pth
BLEU = 56.43, 78.5/63.1/50.4/40.6 (BP=1.000, ratio=1.034, hyp_len=24311, ref_len=23509)
```

time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-60epoch/rkmy-transformer-model.56.1.44-4.22.1.35-3.84.pth --model_fn ./model/rl/transformer/rkmy-60epoch/transformer-rl-myrk.pth --init_epoch 56 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: rk-my, transformer, 60 epoch ရဲ့ Best BLEU Score = 45.70  
RL, rk-my, 60-40 မော်ဒယ်ရဲ့ အကောင်းဆုံး ရလဒ်က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-rl-myrk.97.1.05-2.87.1.00-2.72.pth
BLEU = 58.26, 79.7/64.7/52.3/42.7 (BP=1.000, ratio=1.017, hyp_len=23909, ref_len=23509)
```

time python continue_train.py --load_fn ./model/transformer/baseline/rkmy-70epoch/rkmy-transformer-model.70.1.25-3.47.1.17-3.21.pth --model_fn ./model/rl/transformer/rkmy-70epoch/transformer-rl-myrk.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100  

Baseline: rk-my, transformer, 70 epoch ရဲ့ Best BLEU Score = 51.15  
RL, rk-my, 70-30 model ရဲ့ အကောင်းဆုံး ရလဒ်က  

```
Evaluation result for the model: transformer-rl-myrk.99.1.04-2.84.0.98-2.66.pth
BLEU = 57.20, 78.5/63.5/51.3/41.8 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
```

အထက်ပါ 40-60 ကနေ 70-30 အထိ run ခဲ့စဉ်က မှတ်ထားခဲ့တဲ့ running log ကိုတော့ နောက်ထပ် ဖိုင်တစ်ဖိုင် ခွဲပြီးသိမ်းခဲ့တယ်။ အောက်ပါ link ကို refer လုပ်ပါ။  
- [simple-nmt-40-60-to-70-30-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/simple-nmt-40-60-to-70-30-log.md) 

## Results

my-rk
| epoch (seq2seq+RL) | seq2seq | RL (MRT) |
|-----|-----|-----|
| (30+70) | 68.10 | 74.87 |
| (40+60) | 70.40 | 74.53 |
| (50+50) | 73.15 | 74.72 |
| (60+40) | 75.30 | 75.11 |
| (70+30) | 74.36 | 75.50 |

rk-my
| epoch (seq2seq+RL) | seq2seq | RL (MRT) |
|-----|-----|-----|
| (30+70) | 59.48 | 74.74 |
| (40+60) | 69.39 | 74.98 |
| (50+50) | 74.04 | 74.91 |
| (60+40) | 72.06 | 74.52 |
| (70+30) | 74.84 | 74.48 |

my-rk
| epoch (Transformer+RL) | Transformer | RL (MRT) |
|-----|-----|-----|
| (30+70) | 25.29 | 58.69 |
| (40+60) | 35.33 | 59.13 |
| (50+50) | 40.85 | 56.79 |
| (60+40) | 47.13 | 58.22 |
| (70+30) | 50.51 | 58.20 |

rk-my
| epoch (Transformer+RL) | Transformer | RL (MRT) |
|-----|-----|-----|
| (30+70) | 25.23 | 56.72 |
| (40+60) | 34.17 | 56.95 |
| (50+50) | 40.40 | 56.43 |
| (60+40) | 45.70 | 58.26 |
| (70+30) | 51.15 | 57.20 |


## Analysis of Performance of Two Models Combination

### Preparation

***for seq2seq, baseline model***  
evaluation result တွေကို ဖိုလ်ဒါတစ်ခုအောက်မှာ ကော်ပီကူးထည့်...  

seq2seq baseline my-rk အတွက်  
```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-40epoch/eval-results-myrk-seq2seq-40epoch.txt ./seq40.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-50epoch/eval-results-myrk-seq2seq-50epoch.txt ./seq50.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-60epoch/eval-results-myrk-seq2seq-60epoch.txt ./seq60.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-70epoch/eval-results-myrk-seq2seq-70epoch.txt ./seq70.txt

```

30 epoch အတွက်ကကျတော့ experiment စလုပ်စမှာ epoch 100 run ခဲ့လို့...  
```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-100epoch/eval-results-myrk-seq2seq-30epoch.txt ./seq30.txt
```

seq2seq baseline rk-my အတွက်  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/myrk-100epoch/eval-results-myrk-seq2seq-30epoch.txt ./seq100.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/rkmy-40epoch/eval-results-rkmy-seq2seq-40epoch.txt ./seq40rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/rkmy-50epoch/eval-results-rkmy-seq2seq-50epoch.txt ./seq50rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/rkmy-60epoch/eval-results-rkmy-seq2seq-60epoch.txt ./seq60rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/rkmy-70epoch/eval-results-rkmy-seq2seq-70epoch.txt ./seq70rkmy.txt
```

30 epoch အတွက်ကကျတော့ experiment စလုပ်စမှာ epoch 100 run ခဲ့လို့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../seq2seq/baseline/rkmy-100epoch/eval-results-rkmy-seq2seq-30epoch.txt ./seq30rkmy.txt
```

transformer baseline, my-rk အတွက်  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/myrk-100epoch/eval-results-myrk-transformer-30epoch-max_grad_norm-1e8-rl-100epoch-test.txt ./tran30.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/myrk-40epoch/eval-results-myrk-transformer-40epoch.txt ./tran40.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/myrk-50epoch/eval-results-myrk-transformer-50epoch.txt ./tran50.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/myrk-60epoch/eval-results-myrk-transformer-60epoch.txt ./tran60.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/myrk-70epoch/eval-results-myrk-transformer-70epoch.txt ./tran70.txt
```

transformer baseline, rk-my အတွက်  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/rkmy-100epoch/eval-results-rkmy-transformer-30epoch-max_grad_norm-1e8.txt ./tran30rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/rkmy-40epoch/eval-results-rkmy-transformer-40epoch.txt ./tran40rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/rkmy-50epoch/eval-results-rkmy-transformer-50epoch.txt ./tran50rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/rkmy-60epoch/eval-results-rkmy-transformer-60epoch.txt ./tran60rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../transformer/baseline/rkmy-70epoch/eval-results-rkmy-transformer-70epoch.txt ./tran70rkmy.txt
```

baseline model တွေရဲ့ ရလဒ်တွေအားလုံးကို my-rk အတွက်ရော၊ rk-my အတွက်ရော ကော်ပီကူးပြီးသွားပြီး။ ကျန်တာက နောက်ဆက်တွဲ RL မော်ဒယ်တွေရဲ့ ရလဒ်ဖိုင်တွေ...  

***seq2seq RL အတွက်***

for my-rk ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/100epoch/baseline/eval-results-myrk-seq2seq-30epoch-max_grad_norm-1e8-rl-100epoch-test.txt ./seq-rl30.txt
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/myrk-40epoch/eval-results-myrk-rl.txt ./seq-rl40.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/myrk-50epoch/eval-results-myrk-rl.txt ./seq-rl50.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/myrk-60epoch/eval-results-myrk-rl.txt ./seq-rl60.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/myrk-70epoch/eval-results-myrk-rl.txt ./seq-rl70.txt
```

for rk-my ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/100epoch/baseline/rkmy/eval-results-rkmy-seq2seq-30epoch-max_grad_norm-1e8-rl-100epoch-test.txt ./seq-rl30rkmy.txt
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/rkmy-40epoch/eval-results-rkmy-rl.txt ./seq-rl40rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/rkmy-50epoch/eval-results-rkmy-rl.txt ./seq-rl50rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/rkmy-60epoch/eval-results-rkmy-rl.txt ./seq-rl60rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cp ../../../rl/seq2seq/rkmy-70epoch/eval-results-rkmy-rl.txt ./seq-rl70rkmy.txt

```

***transformer RL အတွက်***  

for my-rk ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/100epoch/baseline/myrk/eval-results-myrk-transformer-30-100epoch-max_grad_norm-1e8.txt ./tran-rl30.txt
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/myrk-40epoch/eval-results-myrk-rl.txt ./tran-rl40.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/myrk-50epoch/eval-results-myrk-rl.txt ./tran-rl50.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/myrk-60epoch/eval-results-myrk-rl.txt ./tran-rl60.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/myrk-70epoch/eval-results-myrk-rl.txt ./tran-rl70.txt
```

for rk-my ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/100epoch/baseline/rkmy/eval-results-rkmy-transformer-30-100epoch-max_grad_norm-1e8.txt ./tran-rl30rkmy.txt
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/rkmy-40epoch/eval-results-rkmy-rl.txt ./tran-rl40rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/rkmy-50epoch/eval-results-rkmy-rl.txt ./tran-rl50rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/rkmy-60epoch/eval-results-rkmy-rl.txt ./tran-rl60rkmy.txt
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ cp ../../../rl/transformer/rkmy-70epoch/eval-results-rkmy-rl.txt ./tran-rl70rkmy.txt
```

ဖိုင်အရေအတွက်ကို စစ်ဆေး...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ls | wc
     20      20     270
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ cd ../tran/
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ls | wc
     20      20     290
```

အိုကေတယ်...  

### Script for Extracting BLEU scores

```bash
#!/bin/bash

# $1 is for the filename of the baseline model results
# $2 is for the filename of the RL model results
# $3 is start line number for the RL model bleu
# How to run: 
# e.g. 

# for baseline model
grep "BLEU =" $1 | cut -f1 -d "," | cut -f2 -d "=" | cat -n > $1.bleu
# for RL model
grep "BLEU =" $2 | cut -f1 -d "," | cut -f2 -d "=" | nl -v $3 > $2.bleu

# for confirmation
wc {$1,$2}.bleu
```

### Extracting BLEU Scores

***for my-rk, seq2seq+RL***  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq30.txt ./seq-rl30.txt 30
  30   60  411 ./seq30.txt.bleu
  71  142  994 ./seq-rl30.txt.bleu
 101  202 1405 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq40.txt ./seq-rl40.txt 40
  40   80  546 ./seq40.txt.bleu
  61  122  854 ./seq-rl40.txt.bleu
 101  202 1400 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq50.txt ./seq-rl50.txt 48
  50  100  689 ./seq50.txt.bleu
  53  106  742 ./seq-rl50.txt.bleu
 103  206 1431 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq60.txt ./seq-rl60.txt 55
  60  120  829 ./seq60.txt.bleu
  46   92  644 ./seq-rl60.txt.bleu
 106  212 1473 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq70.txt ./seq-rl70.txt 61
  70  140  970 ./seq70.txt.bleu
  40   80  560 ./seq-rl70.txt.bleu
 110  220 1530 total
```

***for rk-my, seq2seq+RL***  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq30rkmy.txt ./seq-rl30rkmy.txt 30
  30   60  408 ./seq30rkmy.txt.bleu
  71  142  994 ./seq-rl30rkmy.txt.bleu
 101  202 1402 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq40rkmy.txt ./seq-rl40rkmy.txt 39
  40   80  548 ./seq40rkmy.txt.bleu
  62  124  868 ./seq-rl40rkmy.txt.bleu
 102  204 1416 total

```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq50rkmy.txt ./seq-rl50rkmy.txt 49
  50  100  687 ./seq50rkmy.txt.bleu
  52  104  728 ./seq-rl50rkmy.txt.bleu
 102  204 1415 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq60rkmy.txt ./seq-rl60rkmy.txt 58
  60  120  830 ./seq60rkmy.txt.bleu
  43   86  602 ./seq-rl60rkmy.txt.bleu
 103  206 1432 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ ./extract-bleu-lines.sh ./seq70rkmy.txt ./seq-rl70rkmy.txt 67
  70  140  967 ./seq70rkmy.txt.bleu
  34   68  476 ./seq-rl70rkmy.txt.bleu
 104  208 1443 total
```

***for my-rk, Transformer***

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran30.txt ./tran-rl30.txt 30
  30   60  410 ./tran30.txt.bleu
  71  142  994 ./tran-rl30.txt.bleu
 101  202 1404 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran40.txt ./tran-rl40.txt 39
  40   80  547 ./tran40.txt.bleu
  62  124  868 ./tran-rl40.txt.bleu
 102  204 1415 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran50.txt ./tran-rl50.txt 47
  50  100  686 ./tran50.txt.bleu
  54  108  756 ./tran-rl50.txt.bleu
 104  208 1442 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran60.txt ./tran-rl60.txt 59
  60  120  827 ./tran60.txt.bleu
  42   84  588 ./tran-rl60.txt.bleu
 102  204 1415 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran70.txt ./tran-rl70.txt 70
  70  140  967 ./tran70.txt.bleu
  31   62  434 ./tran-rl70.txt.bleu
 101  202 1401 total
```

***for rk-my, Transformer*** 

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran30rkmy.txt ./tran-rl30rkmy.txt 30
  30   60  406 ./tran30rkmy.txt.bleu
  71  142  994 ./tran-rl30rkmy.txt.bleu
 101  202 1400 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran40rkmy.txt ./tran-rl40rkmy.txt 39
  40   80  547 ./tran40rkmy.txt.bleu
  62  124  868 ./tran-rl40rkmy.txt.bleu
 102  204 1415 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran50rkmy.txt ./tran-rl50rkmy.txt 46
  50  100  688 ./tran50rkmy.txt.bleu
  55  110  770 ./tran-rl50rkmy.txt.bleu
 105  210 1458 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran60rkmy.txt ./tran-rl60rkmy.txt 56
  60  120  827 ./tran60rkmy.txt.bleu
  45   90  630 ./tran-rl60rkmy.txt.bleu
 105  210 1457 total
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/tran$ ./extract-bleu-lines.sh ./tran70rkmy.txt ./tran-rl70rkmy.txt 70
  70  140  967 ./tran70rkmy.txt.bleu
  31   62  434 ./tran-rl70rkmy.txt.bleu
 101  202 1401 total
```

### Script for Graph Drawing

### Draw Graphs

***for Seq2Seq+RL, my-rk***  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq30.txt.bleu seq-rl30.txt.bleu "Seq2Seq 30 epochs + RL 70 epochs (my-rk)" seq2seq_RL-30-70-myrk
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq40.txt.bleu seq-rl40.txt.bleu "Seq2Seq 40 epochs + RL 60 epochs (my-rk)" seq2seq_RL-40-60-myrk
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq50.txt.bleu seq-rl50.txt.bleu "Seq2Seq 50 epochs + RL 50 epochs (my-rk)" seq2seq_RL-50-50-myrk
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq60.txt.bleu seq-rl60.txt.bleu "Seq2Seq 60 epochs + RL 40 epochs (my-rk)" seq2seq_RL-60-40-myrk
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq70.txt.bleu seq-rl30.txt.bleu "Seq2Seq 70 epochs + RL 30 epochs (my-rk)" seq2seq_RL-70-30-myrk
```

***for Seq2Seq+RL, rk-my***

```
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq30rkmy.txt.bleu seq-rl30rkmy.txt.bleu "Seq2Seq 30 epochs + RL 70 epochs (rk-my)" seq2seq_RL-30-70-rk-my
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq40rkmy.txt.bleu seq-rl40rkmy.txt.bleu "Seq2Seq 40 epochs + RL 60 epochs (rk-my)" seq2seq_RL-40-60-rkmy
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq50rkmy.txt.bleu seq-rl50rkmy.txt.bleu "Seq2Seq 50 epochs + RL 50 epochs (rk-my)" seq2seq_RL-50-50-rkmy
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq60rkmy.txt.bleu seq-rl60rkmy.txt.bleu "Seq2Seq 60 epochs + RL 40 epochs (rk-my)" seq2seq_RL-60-40-rkmy
(simple-nmt) ye@:~/exp/simple-nmt/model/graph/30-70exp/seq$ python ./draw.py seq70rkmy.txt.bleu seq-rl30rkmy.txt.bleu "Seq2Seq 70 epochs + RL 30 epochs (rk-my)" seq2seq_RL-70-30-rkmy

```


## Reference

- [https://github.com/kh-kim/simple-nmt](https://github.com/kh-kim/simple-nmt)  
- [Luong et al., 2015, Effective Approaches to Attention-based Neural Machine Translation](https://aclanthology.org/D15-1166/)
- [Shen et al., 2015, Minimum Risk Training for Neural Machine Translation](https://arxiv.org/abs/1512.02433)
- [Sennrich et al., 2016, Neural Machine Translation of Rare Words with Subword Units](https://arxiv.org/abs/1512.02433)
- [Wu et al, 2016, Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/abs/1609.08144)
- [Vaswani et al., 2017, Attention is All You Need](https://arxiv.org/abs/1706.03762)
- [Xia et al., 2017, Dual Supervised Learning](https://arxiv.org/abs/1707.00415)
