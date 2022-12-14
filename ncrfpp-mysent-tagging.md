# Log of using NCRF++ for Burmese Sentence Tokenization

## git clone

```
(ncrfpp) yekyaw.thu@gpu:~/tool$ git clone https://github.com/jiesutd/NCRFpp
Cloning into 'NCRFpp'...
remote: Enumerating objects: 768, done.
remote: Total 768 (delta 0), reused 0 (delta 0), pack-reused 768
Receiving objects: 100% (768/768), 6.89 MiB | 12.92 MiB/s, done.
Resolving deltas: 100% (484/484), done.
(ncrfpp) yekyaw.thu@gpu:~/tool$
```

checked the cloned files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ ls
demo.clf.config     demo.train.config  main_parse.py  model   README.md    utils
demo.decode.config  LICENCE            main.py        readme  sample_data
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Prepare a New Conda Environment

I create an Anaconda new environment with Python version 3.8 as follows:  

```
(base) yekyaw.thu@gpu:~/tool/NCRFpp$ conda create --name ncrfpp python==3.8
...
...
...
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.8-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libedit-3.1.20221030 | 181 KB    | ################################################################################### | 100%
xz-5.2.8             | 429 KB    | ################################################################################### | 100%
sqlite-3.33.0        | 1.1 MB    | ################################################################################### | 100%
libffi-3.2.1         | 48 KB     | ################################################################################### | 100%
python-3.8.0         | 34.9 MB   | ################################################################################### | 100%
pip-22.3.1           | 2.7 MB    | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate ncrfpp
#
# To deactivate an active environment, use
#
#     $ conda deactivate

```

When I try to install torch==1.0, I got an error as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.0
ERROR: Could not find a version that satisfies the requirement torch==1.0 (from versions: 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0)
ERROR: No matching distribution found for torch==1.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

How about trying with 1.4.0 ?!  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.0
ERROR: Could not find a version that satisfies the requirement torch==1.0 (from versions: 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0)
ERROR: No matching distribution found for torch==1.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install --upgrade pip
Requirement already satisfied: pip in /home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages (22.3.1)
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.4.0
Collecting torch==1.4.0
  Downloading torch-1.4.0-cp38-cp38-manylinux1_x86_64.whl (753.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 753.4/753.4 MB 1.9 MB/s eta 0:00:00
Installing collected packages: torch
Successfully installed torch-1.4.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Test Training with Demo Configuration

Check the demo config file ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ cat demo.train.config
### use # to comment out the configure item

### I/O ###
train_dir=sample_data/train.bmes
dev_dir=sample_data/dev.bmes
test_dir=sample_data/test.bmes
model_dir=sample_data/lstmcrf
word_emb_dir=sample_data/sample.word.emb

#raw_dir=
#decode_dir=
#dset_dir=
#load_model_dir=
#char_emb_dir=

norm_word_emb=False
norm_char_emb=False
number_normalized=True
seg=True
word_emb_dim=50
char_emb_dim=30

###NetworkConfiguration###
use_crf=True
use_char=True
word_seq_feature=LSTM
char_seq_feature=CNN
#feature=[POS] emb_size=20
#feature=[Cap] emb_size=20
#nbest=1

###TrainingSetting###
status=train
optimizer=SGD
iteration=1
batch_size=10
ave_batch_loss=False

###Hyperparameters###
cnn_layer=4
char_hidden_dim=50
hidden_dim=200
dropout=0.5
lstm_layer=1
bilstm=True
learning_rate=0.015
lr_decay=0.05
momentum=0
l2=1e-8
#gpu
#clip=
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

checck the GPU status:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ nvidia-smi
Wed Dec 14 21:20:23 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 30%   45C    P0    58W / 300W |      0MiB / 11019MiB |      1%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 62%   69C    P0    72W / 257W |      0MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 22%   64C    P0    72W / 250W |      0MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

test training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config demo.train.config
Traceback (most recent call last):
  File "main.py", line 12, in <module>
    import torch
  File "/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/__init__.py", line 81, in <module>
    from torch._C import *
ImportError: numpy.core.multiarray failed to import

real    0m0.218s
user    0m0.160s
sys     0m0.017s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

numpy library required ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install numpy
Collecting numpy
  Using cached numpy-1.23.5-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.1 MB)
Installing collected packages: numpy
Successfully installed numpy-1.23.5
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

test training again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config demo.train.config
Seed num: 42
MODEL: train
Load pretrained word embedding, norm: False, dir: sample_data/sample.word.emb
Embedding:
     pretrain word:15093, prefect match:847, case_match:433, oov:1834, oov%:0.5887640449438202
Training model...
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: BMES
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 3115
     Char  alphabet size: 71
     Label alphabet size: 18
     Word embedding  dir: sample_data/sample.word.emb
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: sample_data/train.bmes
     Dev    file directory: sample_data/dev.bmes
     Test   file directory: sample_data/test.bmes
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: sample_data/lstmcrf
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 484
     Dev   instance number: 112
     Test  instance number: 186
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: True
     Model word extractor: LSTM
     Model       use_char: True
     Model char extractor: CNN
     Model char_hidden_dim: 50
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 1
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.015
     Hyper        lr_decay: 0.05
     Hyper         HP_clip: None
     Hyper        momentum: 0.0
     Hyper              l2: 1e-08
     Hyper      hidden_dim: 200
     Hyper         dropout: 0.5
     Hyper      lstm_layer: 1
     Hyper          bilstm: True
     Hyper             GPU: True
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
build CRF...
Epoch: 0/1
 Learning rate is set as: 0.015
Shuffle: first input word list: [1728, 131, 1661, 133]
     Instance: 484; Time: 2.61s; loss: 5349.0192; acc: 5449/6640=0.8206
Epoch: 0 training finished. Time: 2.62s, speed: 185.08st/s,  total loss: 5349.019195556641
totalloss: 5349.019195556641
Right token =  1225  All token =  1458  acc =  0.8401920438957476
Dev: time: 0.13s, speed: 874.52st/s; acc: 0.8402, p: 0.6026, r: 0.2238, f: 0.3264
Exceed previous best f score: -10
Save current best model in file: sample_data/lstmcrf.0.model
Right token =  3238  All token =  3610  acc =  0.8969529085872576
Test: time: 0.30s, speed: 625.11st/s; acc: 0.8970, p: 0.6645, r: 0.2919, f: 0.4056

real    0m7.784s
user    0m5.019s
sys     0m2.777s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

test training with demo configuration looks OK.  

## Testing with Demo Configuration File  

checck the demo decode configuration file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ cat demo.decode.config
### Decode ###
status=decode
raw_dir=sample_data/raw.bmes
nbest=10
decode_dir=sample_data/raw.out
dset_dir=sample_data/lstmcrf.dset
load_model_dir=sample_data/lstmcrf.0.model(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

let's test ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config demo.decode.config
Seed num: 42
MODEL: decode
sample_data/raw.bmes
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: BMES
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 3115
     Char  alphabet size: 71
     Label alphabet size: 18
     Word embedding  dir: sample_data/sample.word.emb
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: sample_data/train.bmes
     Dev    file directory: sample_data/dev.bmes
     Test   file directory: sample_data/test.bmes
     Raw    file directory: sample_data/raw.bmes
     Dset   file directory: sample_data/lstmcrf.dset
     Model  file directory: sample_data/lstmcrf
     Loadmodel   directory: sample_data/lstmcrf.0.model
     Decode file directory: sample_data/raw.out
     Train instance number: 484
     Dev   instance number: 112
     Test  instance number: 186
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: True
     Model word extractor: LSTM
     Model       use_char: True
     Model char extractor: CNN
     Model char_hidden_dim: 50
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 1
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.015
     Hyper        lr_decay: 0.05
     Hyper         HP_clip: None
     Hyper        momentum: 0.0
     Hyper              l2: 1e-08
     Hyper      hidden_dim: 200
     Hyper         dropout: 0.5
     Hyper      lstm_layer: 1
     Hyper          bilstm: True
     Hyper             GPU: True
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
nbest: 10
Load Model from file:  sample_data/lstmcrf
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
build CRF...
Decode raw data, nbest: 10 ...
Right token =  1225  All token =  1458  acc =  0.8401920438957476
raw: time:0.22s, speed:511.40st/s; acc: 0.8402, p: 0.6026, r: 0.2238, f: 0.3264
Predict raw 10-best result has been written into file. sample_data/raw.out

real    0m5.310s
user    0m1.903s
sys     0m3.298s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Check the Data Format 

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$ head -n 30 ./train.bmes
EU S-ORG
rejects O
German S-MISC
call O
to O
boycott O
British S-MISC
lamb O
. O

Peter B-PER
Blackburn E-PER

BRUSSELS S-LOC
1996-08-22 O

The O
European B-ORG
Commission E-ORG
said O
on O
Thursday O
it O
disagreed O
with O
German S-MISC
advice O
to O
consumers O
to O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$
```

Chek the training data format:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$ head -n 50 ./test.bmes
Aziz S-PER
said O
Iraq S-LOC
's O
military O
intervention O
, O
the O
first O
on O
such O
scale O
since O
the O
U.S. S-LOC
and O
allies O
decided O
to O
protect O
Iraqi B-MISC
Kurds E-MISC
against O
Baghdad S-LOC
, O
was O
in O
response O
to O
a O
plea O
from O
Barzani S-PER
to O
President O
Saddam B-PER
Hussein E-PER
to O
back O
him O
militarily O
and O
save O
his O
people O
from O
attacks O
by O
Iran S-LOC
and O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$
```

Check the test data format:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$ head -n 100 ./test.bmes
Aziz S-PER
said O
Iraq S-LOC
's O
military O
intervention O
, O
the O
first O
on O
such O
scale O
since O
the O
U.S. S-LOC
and O
allies O
decided O
to O
protect O
Iraqi B-MISC
Kurds E-MISC
against O
Baghdad S-LOC
, O
was O
in O
response O
to O
a O
plea O
from O
Barzani S-PER
to O
President O
Saddam B-PER
Hussein E-PER
to O
back O
him O
militarily O
and O
save O
his O
people O
from O
attacks O
by O
Iran S-LOC
and O
Talabani S-PER
. O

He O
said O
Barzani S-PER
sent O
a O
message O
to O
Saddam S-PER
on O
August O
22 O
in O
which O
he O
said O
: O
" O
The O
conspiracy O
is O
beyond O
our O
capability O
therefore O
we O
plead O
with O
your O
excellency O
to O
order O
Iraqi S-MISC
armed O
forces O
to O
interfere O
to O
help O
us O
to O
evade O
the O
foreign O
threat O
and O
put O
an O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/sample_data$
```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```
