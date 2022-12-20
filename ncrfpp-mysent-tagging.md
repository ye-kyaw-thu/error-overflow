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

## Study Details on Configuration

Reference: https://github.com/jiesutd/NCRFpp/blob/master/readme/Configuration.md  

Relating to I/O:  

```
train_dir=xx    #string (necessary in training). Set training file directory.
dev_dir=xx    #string (necessary in training). Set dev file directory.
test_dir=xx    #string . Set test file directory.
model_dir=xx    #string (optional). Set saved model file directory.
word_emb_dir=xx    #string (optional). Set pretrained word embedding file directory.

raw_dir=xx    #string (optional). Set input raw file directory.
decode_dir=xx    #string (necessary in decoding). Set decoded file directory.
dset_dir=xx    #string (necessary). Set saved model file directory.
load_model_dir=xx    #string (necessary in decoding). Set loaded model file directory. (when decoding)
char_emb_dir=xx    #string (optional). Set pretrained character embedding file directory.

norm_word_emb=False    #boolen. If normalize the pretrained word embedding.
norm_char_emb=False    #boolen. If normalize the pretrained character embedding.
number_normalized=True    #boolen. If normalize the digit into `0` for input files.
seg=True    #boolen. If task is segmentation like, tasks with token accuracy evaluation (e.g. POS, CCG) is False; tasks with F-value evaluation(e.g. Word Segmentation, NER, Chunking) is True .
word_emb_dim=50    #int. Word embedding dimension, if model use pretrained word embedding, word_emb_dim will be reset as the same dimension as pretrained embedidng.
char_emb_dim=30    #int. Character embedding dimension, if model use pretrained character embedding, char_emb_dim will be reset as the same dimension as pretrained embedidng.
```

Relating to Networking:  

```
use_crf=True    #boolen (necessary in training). Flag of if using CRF layer. If it is set as False, then Softmax is used in inference layer.
use_char=True    #boolen (necessary in training). Flag of if using character sequence layer. 
word_seq_feature=XX    #boolen (necessary in training): CNN/LSTM/GRU. Neural structure selection for word sequence. 
char_seq_feature=CNN    #boolen (necessary in training): CNN/LSTM/GRU. Neural structure selection for character sequence, it only be used when use_char=True.
feature=[POS] emb_size=20 emb_dir=xx   #feature configuration. It includes the feature prefix [POS], pretrained feature embedding file and the embedding size. 
feature=[Cap] emb_size=20 emb_dir=xx    #feature configuration. Another feature [Cap].
nbest=1    #int (necessary in decoding). Set the nbest size during decoding.
```

Relating to Training Setting:  

```
status=train    #string: train or decode. Set the program running in training or decoding mode.
optimizer=SGD    #string: SGD/Adagrad/AdaDelta/RMSprop/Adam. optimizer selection.
iteration=1    #int. Set the iteration number of training.
batch_size=10    #int. Set the batch size of training or decoding.
ave_batch_loss=False    #boolen. Set average the batched loss during training.
```

Relating to Hyperparameters:  

```
cnn_layer=4    #int. CNN layer number for word sequence layer.
char_hidden_dim=50    #int. Character hidden vector dimension for character sequence layer.
hidden_dim=200    #int. Word hidden vector dimension for word sequence layer.
dropout=0.5    #float. Dropout probability.
lstm_layer=1    #int. LSTM layer number for word sequence layer.
bilstm=True    #boolen. If use bidirection lstm for word seuquence layer.
learning_rate=0.015    #float. Learning rate.
lr_decay=0.05    #float. Learning rate decay rate, only works when optimizer=SGD.
momentum=0    #float. Momentum 
l2=1e-8    #float. L2-regulization.
#gpu=True  #boolen. If use GPU, generally it depends on the hardward environment.
#clip=     #float. Clip the gradient which is larger than the setted number.
```

## Preparing mySentence Data  

for sentence dataset:  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ cp /home/yekyaw.thu/exp/mySent/ncrf/mySentence-data-crf-format/sent_data_crf_format/train-valid-test-style/* .
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ ls
test.col  train.col  valid.col
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ wc *
   68334   127244  1051379 test.col
  583541  1087082  8995710 train.col
   34729    64630   533580 valid.col
  686604  1278956 10580669 total
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$
```

check data format roughly ...  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ head train.col
ဘာ B
ရယ် O
လလိလို့ O
တိတိကျကျ O
ထောက်မပြ O
နနိုင် O
ပေမမဲ့ O
ပြဿနာ O
တစ် O
ခု O
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ head valid.col
ထထို B
အချိန် O
မှ O
စ O
၍ O
စင်္ကာပူ O
ကျွန်း O
၏ O
ခေတ်သစ် O
တစ် O
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$ head test.col
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/sent$
```

preparing for sent+para dataset:  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$ cp ../../mySentence-data-crf-format/sent+para_data_crf_format/train-valid-test-style/* .
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$ wc *
  102144   193264  1578958 test.col
  881245  1668486 13659721 train.col
   64861   123564  1004217 valid.col
 1048250  1985314 16242896 total
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$
```

check data format ...  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$ head -n 30 train.col
နားလည် B
ပါ N
ပြီ E

ဈေး B
က O
များ N
လှ N
ချေ N
လား E

သူ B
ဒီ O
နေ့ O
နည်းနည်း O
ပင်ပန်း O
နေ N
တယ် N
ထင် N
တယ် E

ဘာ B
ကြောင့် O
လဲ O
ဆဆို N
စမ်း N
ပါ N
ဦး E

စိတ်ကောက် B
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$
```

check valid.col  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$ head -n 30 valid.col
သူ B
ဘယ်သူ N
နနဲ့ N
အရင်းနှီးဆဆုံး N
လဲ E

ဒီ B
က O
နေ O
ရှေ့ O
ကကို O
တည့်တည့် O
သွား O
မီးပွွိုင့် O
တွေ့ O
ရင် O
ဘယ်ဘက် O
ကွေ့ O
၂ O
မှတ်တတိုင် O
ဆက်လက် O
သွား O
ရင် O
ရောက် N
ပါ N
လိမ့် N
မယ် E

ရေခဲ B
မ N
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$
```

check test.col file ...  

```
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$ head -n 30 test.col
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E

ကြြိုပပိပို့ B
ဘတ်စ်ကား N
က N
အဆင်အပြေဆဆုံး N
ပဲ E

အဲဒီ B
အဖွွဲ့ O
ရရဲ့ O
ဥက္ကဋ္ဌ O
ဖြစ် O
တတဲ့ O
ယယို O
ကကို O
ယာမာ့ O
အာကိဟီတတို O
YokoyamaAkihito O
က O
တခြား O
(ncrfpp) yekyaw.thu@gpu:~/exp/mySent/ncrf/data/para$
```

## 1. Prepare Config File for Word-LSTM, Char-CNN Model

training config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
#word_emb_dir=sample_data/sample.word.emb

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
use_crf=False
use_char=True
word_seq_feature=LSTM
char_seq_feature=CNN
#feature=[POS] emb_size=20
#feature=[Cap] emb_size=20
#nbest=1

###TrainingSetting###
status=train
# optimizer can be SGD/Adagrad/AdaDelta/RMSprop/Adam
optimizer=SGD
iteration=100
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
gpu=True
#clip=
```

training log ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.char-cnn.train.config
...
...
...
     Instance: 28000; Time: 0.68s; loss: 32.4567; acc: 287120/378246=0.7591
     Instance: 28500; Time: 0.77s; loss: 44.5083; acc: 294180/385311=0.7635
     Instance: 29000; Time: 0.72s; loss: 40.2403; acc: 300751/391890=0.7674
     Instance: 29500; Time: 0.73s; loss: 22.6643; acc: 307435/398578=0.7713
     Instance: 30000; Time: 0.77s; loss: 109.5681; acc: 314429/405583=0.7753
     Instance: 30500; Time: 0.73s; loss: 15.8874; acc: 321077/412235=0.7789
     Instance: 31000; Time: 0.79s; loss: 42.0999; acc: 328002/419166=0.7825
     Instance: 31500; Time: 0.73s; loss: 51.8857; acc: 334597/425768=0.7859
     Instance: 32000; Time: 0.82s; loss: 50.0649; acc: 341890/433072=0.7895
     Instance: 32500; Time: 0.80s; loss: 129.4838; acc: 348910/440108=0.7928
     Instance: 33000; Time: 0.79s; loss: 171.2889; acc: 355795/447015=0.7959
     Instance: 33500; Time: 0.79s; loss: 155.8194; acc: 362839/454076=0.7991
     Instance: 34000; Time: 0.73s; loss: 37.7461; acc: 369442/460685=0.8019
     Instance: 34500; Time: 0.76s; loss: 110.5981; acc: 376426/467678=0.8049
     Instance: 35000; Time: 0.81s; loss: 41.8031; acc: 383561/474819=0.8078
     Instance: 35500; Time: 0.80s; loss: 18.3619; acc: 390800/482061=0.8107
     Instance: 36000; Time: 0.76s; loss: 49.1879; acc: 397375/488644=0.8132
     Instance: 36500; Time: 0.76s; loss: 41.6815; acc: 404113/495386=0.8158
     Instance: 37000; Time: 0.77s; loss: 157.9075; acc: 410982/502268=0.8183
     Instance: 37500; Time: 0.77s; loss: 181.8122; acc: 417884/509202=0.8207
     Instance: 38000; Time: 0.71s; loss: 117.4134; acc: 424305/515634=0.8229
     Instance: 38500; Time: 0.77s; loss: 19.4450; acc: 431182/522512=0.8252
     Instance: 39000; Time: 0.77s; loss: 100.8025; acc: 437878/529223=0.8274
     Instance: 39500; Time: 0.77s; loss: 13.4660; acc: 444810/536159=0.8296
     Instance: 39999; Time: 0.77s; loss: 59.1358; acc: 451789/543142=0.8318
Epoch: 0 training finished. Time: 60.55s, speed: 660.64st/s,  total loss: 238730.19521450996
totalloss: 238730.19521450996
Right token =  32287  All token =  32315  acc =  0.9991335293207488
Dev: time: 1.98s, speed: 1230.65st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.0.model
...
...
...
     Instance: 35500; Time: 0.76s; loss: 70.0287; acc: 481987/482390=0.9992
     Instance: 36000; Time: 0.78s; loss: 25.3078; acc: 489048/489455=0.9992
     Instance: 36500; Time: 0.72s; loss: 35.9397; acc: 495493/495907=0.9992
     Instance: 37000; Time: 0.77s; loss: 10.8092; acc: 502462/502879=0.9992
     Instance: 37500; Time: 0.78s; loss: 59.3640; acc: 509334/509759=0.9992
     Instance: 38000; Time: 0.70s; loss: 14.0096; acc: 515855/516282=0.9992
     Instance: 38500; Time: 0.73s; loss: 7.5072; acc: 522564/522993=0.9992
     Instance: 39000; Time: 0.76s; loss: 19.6130; acc: 529289/529722=0.9992
     Instance: 39500; Time: 0.77s; loss: 40.5207; acc: 536107/536545=0.9992
     Instance: 39999; Time: 0.75s; loss: 48.6918; acc: 542695/543142=0.9992
Epoch: 8 training finished. Time: 60.34s, speed: 662.91st/s,  total loss: 2759.536283969879
totalloss: 2759.536283969879
Right token =  32287  All token =  32315  acc =  0.9991335293207488
Dev: time: 1.99s, speed: 1225.10st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63590  All token =  63622  acc =  0.9994970293294773
Test: time: 4.08s, speed: 1166.49st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 9/100
 Learning rate is set as: 0.010344827586206896
Shuffle: first input word list: [4022, 2988, 253, 81, 254]
     Instance: 500; Time: 0.77s; loss: 26.6937; acc: 7000/7005=0.9993
     Instance: 1000; Time: 0.78s; loss: 27.5530; acc: 13928/13941=0.9991
     Instance: 1500; Time: 0.75s; loss: 14.3770; acc: 20777/20792=0.9993
     Instance: 2000; Time: 0.75s; loss: 46.9566; acc: 27451/27471=0.9993
     Instance: 2500; Time: 0.74s; loss: 11.8214; acc: 34067/34089=0.9994
     Instance: 3000; Time: 0.78s; loss: 44.0794; acc: 41062/41090=0.9993
     Instance: 3500; Time: 0.71s; loss: 9.0670; acc: 47483/47512=0.9994
     Instance: 4000; Time: 0.78s; loss: 52.0679; acc: 54581/54615=0.9994
     Instance: 4500; Time: 0.77s; loss: 88.8468; acc: 61115/61161=0.9992
     Instance: 5000; Time: 0.75s; loss: 20.6342; acc: 67838/67888=0.9993
...
...
...
     Instance: 30000; Time: 0.76s; loss: 20.8148; acc: 406746/406922=0.9996
     Instance: 30500; Time: 0.75s; loss: 7.8250; acc: 413750/413929=0.9996
     Instance: 31000; Time: 0.72s; loss: 10.9805; acc: 420162/420344=0.9996
     Instance: 31500; Time: 0.78s; loss: 25.2875; acc: 426838/427023=0.9996
     Instance: 32000; Time: 0.73s; loss: 9.8244; acc: 433892/434078=0.9996
     Instance: 32500; Time: 0.79s; loss: 7.2981; acc: 440924/441114=0.9996
     Instance: 33000; Time: 0.70s; loss: 19.7985; acc: 447337/447533=0.9996
     Instance: 33500; Time: 0.73s; loss: 28.0911; acc: 454349/454551=0.9996
     Instance: 34000; Time: 0.75s; loss: 3.3515; acc: 461479/461681=0.9996
     Instance: 34500; Time: 0.72s; loss: 2.3600; acc: 468072/468274=0.9996
     Instance: 35000; Time: 0.75s; loss: 14.8842; acc: 474665/474870=0.9996
     Instance: 35500; Time: 0.71s; loss: 3.6203; acc: 481233/481439=0.9996
     Instance: 36000; Time: 0.71s; loss: 9.3795; acc: 487801/488010=0.9996
     Instance: 36500; Time: 0.74s; loss: 4.0125; acc: 494715/494925=0.9996
     Instance: 37000; Time: 0.72s; loss: 6.7776; acc: 501575/501787=0.9996
     Instance: 37500; Time: 0.75s; loss: 11.1597; acc: 508596/508809=0.9996
     Instance: 38000; Time: 0.75s; loss: 16.0169; acc: 515486/515702=0.9996
     Instance: 38500; Time: 0.73s; loss: 11.6874; acc: 522166/522385=0.9996
     Instance: 39000; Time: 0.74s; loss: 25.5515; acc: 529107/529333=0.9996
     Instance: 39500; Time: 0.78s; loss: 14.5840; acc: 536122/536351=0.9996
     Instance: 39999; Time: 0.75s; loss: 7.3349; acc: 542911/543142=0.9996
Epoch: 99 training finished. Time: 59.62s, speed: 670.94st/s,  total loss: 854.5173244476318
totalloss: 854.5173244476318
Right token =  32284  All token =  32315  acc =  0.9990406931765434
Dev: time: 2.00s, speed: 1218.49st/s; acc: 0.9990, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63580  All token =  63622  acc =  0.9993398509949388
Test: time: 4.07s, speed: 1167.93st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    111m21.157s
user    110m30.263s
sys     0m31.132s
```

check GPU status during training time ...   
and it looks using only GPU. I should findout how to set number of GPU in config file ...  


```
Every 2.0s: nvidia-smi                                                               gpu.cadt.edu.kh: Fri Dec 16 21:13:38 2022
Fri Dec 16 21:13:38 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 46%   51C    P2    62W / 300W |    908MiB / 11019MiB |     18%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   54C    P8    21W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 33%   44C    P8    29W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2702014      C   python                            905MiB |
+-----------------------------------------------------------------------------+
```

check the model file and output files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$ ls
wordlstm-charcnn.0.model  wordlstm-charcnn.dset
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$
```

decode config file:  

```
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.0.model
```

testing ...  

```
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 31439
     Char  alphabet size: 274
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charcnn.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
     Model word extractor: LSTM
     Model       use_char: True
     Model char extractor: CNN
     Model char_hidden_dim: 50
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 100
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.18s, speed:1137.11st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
```

hyp file cannot write as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ wc wordlstm-charcnn.hyp
0 0 0 wordlstm-charcnn.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

Error message is as follows:  

```
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.22s, speed:1128.19st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Traceback (most recent call last):
  File "main.py", line 568, in <module>
    data.write_decoded_results(decode_results, 'raw')
  File "/home/yekyaw.thu/tool/NCRFpp/utils/data.py", line 334, in write_decoded_results
    fout.write(content_list[idx][0][idy].encode('utf-8') + " " + predict_results[idx][idy] + '\n')
TypeError: can't concat str to bytes

real    0m12.807s
user    0m10.013s
sys     0m3.177s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Code debugging as follows:  

```
334                     #fout.write(content_list[idx][0][idy].encode('utf-8') + " " + predict_results[idx][idy] + '\n')
335                     fout.write(content_list[idx][0][idy] + " " + predict_results[idx][idy]     + '\n')
```

test again ...  

```
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.19s, speed:1135.83st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charcnn.hyp

real    0m12.621s
user    0m9.839s
sys     0m2.980s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the hypothesis output file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ wc wordlstm-charcnn.hyp
  68334  127244 1051379 wordlstm-charcnn.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

check the hyp file content:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head -n 30 ./wordlstm-charcnn.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
ရှိ O
မှု O
ကကို N
မ N
ကြြိုက် N
ဘူး E

ဒီ B
တစ် O
ခေါက် O
ကိစ္စ O
ကြောင့် O
ကျွန်တော့် O
ရရဲ့ O
သိက္ခာ O
အဖတ်ဆယ် O
လလိလို့ O
မ O
ရ O
အောင် N
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 2. Word-LSTM, Char-LSTM

update the config file: 

```
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
```

```
###NetworkConfiguration###
use_crf=False
use_char=True
word_seq_feature=LSTM
char_seq_feature=LSTM
```

training log ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.char-lstm.train.config | tee ./mysent-model/wordlstm-charlstm.training.log
...
...
...
     Hyper      lstm_layer: 1
     Hyper          bilstm: True
     Hyper             GPU: True
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 0.98s; loss: 6763.9298; acc: 4315/6598=0.6540
     Instance: 1000; Time: 0.99s; loss: 1224.9703; acc: 10795/13463=0.8018
     Instance: 1500; Time: 0.96s; loss: 573.6215; acc: 17310/20100=0.8612
     Instance: 2000; Time: 0.99s; loss: 255.3739; acc: 24278/27109=0.8956
     Instance: 2500; Time: 0.96s; loss: 150.8403; acc: 30765/33628=0.9149
     Instance: 3000; Time: 0.98s; loss: 82.3629; acc: 37755/40631=0.9292
     Instance: 3500; Time: 0.98s; loss: 60.5309; acc: 44862/47745=0.9396
     Instance: 4000; Time: 1.02s; loss: 48.2506; acc: 52091/54983=0.9474
     Instance: 4500; Time: 0.96s; loss: 70.9716; acc: 58559/61461=0.9528
     Instance: 5000; Time: 0.96s; loss: 127.8899; acc: 65131/68047=0.9571
     Instance: 5500; Time: 1.03s; loss: 68.3554; acc: 72496/75417=0.9613
     Instance: 6000; Time: 0.95s; loss: 37.4366; acc: 79385/82310=0.9645
...
...
...
     Instance: 34000; Time: 0.99s; loss: 14.4887; acc: 461272/461480=0.9995
     Instance: 34500; Time: 1.01s; loss: 8.4303; acc: 468217/468427=0.9996
     Instance: 35000; Time: 0.97s; loss: 4.9089; acc: 475359/475571=0.9996
     Instance: 35500; Time: 0.92s; loss: 13.4792; acc: 481895/482110=0.9996
     Instance: 36000; Time: 0.99s; loss: 8.3643; acc: 488674/488892=0.9996
     Instance: 36500; Time: 0.97s; loss: 2.2129; acc: 495312/495530=0.9996
     Instance: 37000; Time: 0.99s; loss: 8.1948; acc: 502248/502468=0.9996
     Instance: 37500; Time: 1.00s; loss: 3.1468; acc: 509004/509224=0.9996
     Instance: 38000; Time: 0.99s; loss: 8.3233; acc: 515815/516037=0.9996
     Instance: 38500; Time: 0.99s; loss: 28.5366; acc: 522582/522811=0.9996
     Instance: 39000; Time: 1.01s; loss: 41.0298; acc: 529512/529755=0.9995
     Instance: 39500; Time: 0.97s; loss: 17.6814; acc: 536158/536405=0.9995
     Instance: 39999; Time: 0.96s; loss: 5.8083; acc: 542892/543142=0.9995
Epoch: 87 training finished. Time: 77.25s, speed: 517.79st/s,  total loss: 915.7552361488342
totalloss: 915.7552361488342
Right token =  32283  All token =  32315  acc =  0.9990097477951416
Dev: time: 2.33s, speed: 1046.35st/s; acc: 0.9990, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63579  All token =  63622  acc =  0.999324133161485
Test: time: 4.72s, speed: 1005.99st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 88/100
 Learning rate is set as: 0.0027777777777777775
Shuffle: first input word list: [1628, 2225, 798, 42, 233, 290, 53, 855, 27796, 3702, 98, 53, 798, 44, 49, 47, 855, 10091, 2514, 798, 44, 222, 114, 3381, 119, 134, 745, 42]
     Instance: 500; Time: 0.95s; loss: 17.5519; acc: 6557/6562=0.9992
     Instance: 1000; Time: 0.91s; loss: 21.6322; acc: 13005/13013=0.9994
     Instance: 1500; Time: 0.99s; loss: 4.8008; acc: 19909/19918=0.9995
     Instance: 2000; Time: 0.98s; loss: 9.4800; acc: 26477/26491=0.9995
     Instance: 2500; Time: 0.96s; loss: 14.8256; acc: 33615/33632=0.9995
     Instance: 3000; Time: 0.94s; loss: 7.8938; acc: 40177/40198=0.9995
     Instance: 3500; Time: 0.95s; loss: 2.4266; acc: 46866/46887=0.9996
...
...
...
     Instance: 28000; Time: 0.98s; loss: 20.8923; acc: 379376/379527=0.9996
     Instance: 28500; Time: 1.00s; loss: 2.7063; acc: 386696/386847=0.9996
     Instance: 29000; Time: 0.96s; loss: 5.3790; acc: 393165/393317=0.9996
     Instance: 29500; Time: 0.93s; loss: 16.8582; acc: 399616/399772=0.9996
     Instance: 30000; Time: 0.97s; loss: 18.0675; acc: 406763/406922=0.9996
     Instance: 30500; Time: 0.96s; loss: 9.8058; acc: 413767/413929=0.9996
     Instance: 31000; Time: 0.94s; loss: 8.0381; acc: 420180/420344=0.9996
     Instance: 31500; Time: 0.98s; loss: 19.3071; acc: 426855/427023=0.9996
     Instance: 32000; Time: 0.99s; loss: 6.0914; acc: 433908/434078=0.9996
     Instance: 32500; Time: 1.04s; loss: 4.9224; acc: 440942/441114=0.9996
     Instance: 33000; Time: 0.94s; loss: 19.6826; acc: 447354/447533=0.9996
     Instance: 33500; Time: 0.96s; loss: 26.5260; acc: 454367/454551=0.9996
     Instance: 34000; Time: 0.99s; loss: 2.0317; acc: 461497/461681=0.9996
     Instance: 34500; Time: 0.97s; loss: 3.3676; acc: 468089/468274=0.9996
     Instance: 35000; Time: 1.00s; loss: 17.3917; acc: 474681/474870=0.9996
     Instance: 35500; Time: 0.96s; loss: 2.8269; acc: 481250/481439=0.9996
     Instance: 36000; Time: 0.95s; loss: 7.2310; acc: 487818/488010=0.9996
     Instance: 36500; Time: 0.98s; loss: 1.7408; acc: 494733/494925=0.9996
     Instance: 37000; Time: 0.96s; loss: 13.4167; acc: 501590/501787=0.9996
     Instance: 37500; Time: 1.00s; loss: 8.8884; acc: 508611/508809=0.9996
     Instance: 38000; Time: 0.96s; loss: 14.8639; acc: 515501/515702=0.9996
     Instance: 38500; Time: 0.94s; loss: 10.9465; acc: 522181/522385=0.9996
     Instance: 39000; Time: 1.00s; loss: 21.4621; acc: 529122/529333=0.9996
     Instance: 39500; Time: 1.00s; loss: 19.4401; acc: 536137/536351=0.9996
     Instance: 39999; Time: 0.94s; loss: 10.5016; acc: 542925/543142=0.9996
Epoch: 99 training finished. Time: 77.20s, speed: 518.13st/s,  total loss: 828.0619547367096
totalloss: 828.0619547367096
Right token =  32283  All token =  32315  acc =  0.9990097477951416
Dev: time: 2.32s, speed: 1049.03st/s; acc: 0.9990, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63579  All token =  63622  acc =  0.999324133161485
Test: time: 4.72s, speed: 1005.92st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000
```

prepare decoding configuration file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-lstm.char-lstm.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

manual decoding or testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.char-lstm.decode.config | tee ./mysent-model/wordlstm-charlstm.decode.log
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.96s, speed:957.04st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charlstm.hyp

real    0m19.159s
user    0m11.255s
sys     0m3.997s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

The whole decoding log:  

```
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 31439
     Char  alphabet size: 274
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.0.model
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 31439
     Char  alphabet size: 274
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.0.model
     Hyper      hidden_dim: 200
     Hyper         dropout: 0.5
     Hyper      lstm_layer: 1
     Hyper          bilstm: True
     Hyper             GPU: True
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.96s, speed:957.04st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charlstm.hyp
```

check the hype file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head ./wordlstm-charlstm.hyp
အခု B
သန့်စင်ခန်း N
ကို N
သုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 3. Word-LSTM, no-char  

updated the config file as follows:  

```
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar
...
...
norm_word_emb=False
norm_char_emb=False
number_normalized=True
seg=True
word_emb_dim=50
char_emb_dim=30
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.no-char.train.config | tee ./mysent-model/wordlstm-nochar.training.log
...
...
...
     Instance: 11500; Time: 0.68s; loss: 45.9094; acc: 153897/156911=0.9808
     Instance: 12000; Time: 0.67s; loss: 17.9875; acc: 160434/163450=0.9815
     Instance: 12500; Time: 0.69s; loss: 32.1635; acc: 167086/170107=0.9822
     Instance: 13000; Time: 0.67s; loss: 62.4728; acc: 174158/177185=0.9829
     Instance: 13500; Time: 0.75s; loss: 31.4787; acc: 180967/183998=0.9835
     Instance: 14000; Time: 0.66s; loss: 38.0288; acc: 187571/190606=0.9841
     Instance: 14500; Time: 0.61s; loss: 62.3357; acc: 193982/197025=0.9846
     Instance: 15000; Time: 0.61s; loss: 33.2049; acc: 200684/203732=0.9850
     Instance: 15500; Time: 0.60s; loss: 101.5641; acc: 207522/210579=0.9855
     Instance: 16000; Time: 0.58s; loss: 23.6539; acc: 214113/217171=0.9859
     Instance: 16500; Time: 0.60s; loss: 74.6310; acc: 220675/223739=0.9863
     Instance: 17000; Time: 0.59s; loss: 81.2837; acc: 227171/230242=0.9867
     Instance: 17500; Time: 0.60s; loss: 68.2723; acc: 233787/236869=0.9870
     Instance: 18000; Time: 0.62s; loss: 55.4200; acc: 240566/243654=0.9873
     Instance: 18500; Time: 0.61s; loss: 49.0099; acc: 247439/250533=0.9877
     Instance: 19000; Time: 0.64s; loss: 59.5998; acc: 254512/257613=0.9880
     Instance: 19500; Time: 0.60s; loss: 36.2397; acc: 261064/264169=0.9882
     Instance: 20000; Time: 0.58s; loss: 42.1274; acc: 267386/270497=0.9885
     Instance: 20500; Time: 0.61s; loss: 87.3023; acc: 274263/277384=0.9887
     Instance: 21000; Time: 0.56s; loss: 34.6933; acc: 280519/283647=0.9890
     Instance: 21500; Time: 0.62s; loss: 47.9778; acc: 287375/290511=0.9892
     Instance: 22000; Time: 0.60s; loss: 21.2712; acc: 294173/297313=0.9894
     Instance: 22500; Time: 0.60s; loss: 56.4415; acc: 300649/303798=0.9896
     Instance: 23000; Time: 0.64s; loss: 50.0748; acc: 307477/310636=0.9898
     Instance: 23500; Time: 0.65s; loss: 25.8181; acc: 314468/317630=0.9900
...
...
...
     Instance: 30000; Time: 0.69s; loss: 10.2924; acc: 406760/406922=0.9996
     Instance: 30500; Time: 0.69s; loss: 5.7964; acc: 413764/413929=0.9996
     Instance: 31000; Time: 0.64s; loss: 8.3327; acc: 420177/420344=0.9996
     Instance: 31500; Time: 0.72s; loss: 12.8702; acc: 426853/427023=0.9996
     Instance: 32000; Time: 0.68s; loss: 10.7969; acc: 433905/434078=0.9996
     Instance: 32500; Time: 0.74s; loss: 4.2581; acc: 440939/441114=0.9996
     Instance: 33000; Time: 0.64s; loss: 13.3785; acc: 447353/447533=0.9996
     Instance: 33500; Time: 0.68s; loss: 20.2858; acc: 454366/454551=0.9996
     Instance: 34000; Time: 0.69s; loss: 4.9878; acc: 461495/461681=0.9996
     Instance: 34500; Time: 0.66s; loss: 5.6717; acc: 468086/468274=0.9996
     Instance: 35000; Time: 0.68s; loss: 21.4708; acc: 474678/474870=0.9996
     Instance: 35500; Time: 0.65s; loss: 3.4203; acc: 481245/481439=0.9996
     Instance: 36000; Time: 0.64s; loss: 9.2008; acc: 487814/488010=0.9996
     Instance: 36500; Time: 0.69s; loss: 1.8054; acc: 494729/494925=0.9996
     Instance: 37000; Time: 0.66s; loss: 14.5209; acc: 501587/501787=0.9996
     Instance: 37500; Time: 0.71s; loss: 11.7103; acc: 508607/508809=0.9996
     Instance: 38000; Time: 0.70s; loss: 9.9241; acc: 515498/515702=0.9996
     Instance: 38500; Time: 0.68s; loss: 10.9779; acc: 522178/522385=0.9996
     Instance: 39000; Time: 0.69s; loss: 15.0097; acc: 529120/529333=0.9996
     Instance: 39500; Time: 0.69s; loss: 16.2991; acc: 536134/536351=0.9996
     Instance: 39999; Time: 0.68s; loss: 5.6317; acc: 542922/543142=0.9996
Epoch: 99 training finished. Time: 54.51s, speed: 733.80st/s,  total loss: 746.9416055679321
totalloss: 746.9416055679321
Right token =  32284  All token =  32315  acc =  0.9990406931765434
Dev: time: 1.95s, speed: 1252.95st/s; acc: 0.9990, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63578  All token =  63622  acc =  0.9993084153280312
Test: time: 3.99s, speed: 1193.74st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    101m55.815s
user    101m18.082s
sys     0m29.634s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Check the models ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$ ls
bk                        wordlstm-charlstm.0.model     wordlstm-charlstm.training.log  wordlstm-nochar.training.log
wordlstm-charcnn.0.model  wordlstm-charlstm.decode.log  wordlstm-nochar.0.model
wordlstm-charcnn.dset     wordlstm-charlstm.dset        wordlstm-nochar.dset
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$
```

Prepare configuration file for decoding:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat ./word-lstm.no-char.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-nochar.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

manual decoding ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.no-char.decode.config | tee ./mysent-model/wordlstm-nochar.decode.log
...
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:3.95s, speed:1204.46st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-nochar.hyp

real    0m12.364s
user    0m9.567s
sys     0m3.147s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head ./wordlstm-nochar.hyp
အခု B
သန့်စင်ခန်း N
ကို N
သုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 4. Word-LSTM, CRF, Char-CNN

preparing config file:  

```
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn
...
###NetworkConfiguration###
use_crf=True
use_char=True
word_seq_feature=LSTM
char_seq_feature=CNN
```

training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.crf.char-cnn.train.config | tee ./mysent-model/wordlstm-crf-charcnn.training.log
...
...
...
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
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 2.63s; loss: 2854.2836; acc: 4935/6598=0.7480
     Instance: 1000; Time: 2.62s; loss: 1355.7439; acc: 10843/13463=0.8054
...
...
...
     Instance: 30500; Time: 2.58s; loss: 8.3659; acc: 413707/413929=0.9995
     Instance: 31000; Time: 2.42s; loss: 18.4387; acc: 420118/420344=0.9995
     Instance: 31500; Time: 2.63s; loss: 16.5659; acc: 426794/427023=0.9995
     Instance: 32000; Time: 2.55s; loss: 17.0895; acc: 433845/434078=0.9995
     Instance: 32500; Time: 2.74s; loss: 14.4164; acc: 440875/441114=0.9995
     Instance: 33000; Time: 2.35s; loss: 22.5720; acc: 447285/447533=0.9994
     Instance: 33500; Time: 2.51s; loss: 23.6950; acc: 454298/454551=0.9994
     Instance: 34000; Time: 2.53s; loss: 5.4600; acc: 461427/461681=0.9994
     Instance: 34500; Time: 2.40s; loss: 12.0142; acc: 468017/468274=0.9995
     Instance: 35000; Time: 2.51s; loss: 22.8959; acc: 474610/474870=0.9995
     Instance: 35500; Time: 2.27s; loss: 7.5930; acc: 481177/481439=0.9995
     Instance: 36000; Time: 2.31s; loss: 19.3913; acc: 487743/488010=0.9995
     Instance: 36500; Time: 2.47s; loss: 2.4894; acc: 494658/494925=0.9995
     Instance: 37000; Time: 2.43s; loss: 8.1326; acc: 501518/501787=0.9995
     Instance: 37500; Time: 2.56s; loss: 14.0385; acc: 508537/508809=0.9995
     Instance: 38000; Time: 2.50s; loss: 11.3989; acc: 515426/515702=0.9995
     Instance: 38500; Time: 2.41s; loss: 10.7767; acc: 522106/522385=0.9995
     Instance: 39000; Time: 2.52s; loss: 28.8738; acc: 529046/529333=0.9995
     Instance: 39500; Time: 2.54s; loss: 22.3990; acc: 536061/536351=0.9995
     Instance: 39999; Time: 2.50s; loss: 8.9142; acc: 542850/543142=0.9995
Epoch: 99 training finished. Time: 198.87s, speed: 201.13st/s,  total loss: 1062.7795715332031
totalloss: 1062.7795715332031
Right token =  32285  All token =  32315  acc =  0.9990716385579452
Dev: time: 2.87s, speed: 846.90st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63580  All token =  63622  acc =  0.9993398509949388
Test: time: 5.86s, speed: 809.12st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    347m13.584s
user    346m31.274s
sys     0m31.970s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

during the training time, check the GPU status and as follows:  

```
Every 2.0s: nvidia-smi                                                               gpu.cadt.edu.kh: Sat Dec 17 16:04:18 2022
Sat Dec 17 16:04:18 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 45%   52C    P2    61W / 300W |    908MiB / 11019MiB |     17%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  8%   51C    P8    21W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 35%   51C    P8    29W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2715558      C   python                            905MiB |
+-----------------------------------------------------------------------------+
```

prepare config file for decoding ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-lstm.crf.char-cnn.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

manual testing for wordlstm-crf-charcnn model ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.crf.char-cnn.decode.config | tee ./mysent-model/wordlstm-crf-charcnn.decode.log
...
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
build CRF...
Decode raw data, nbest: None ...
Right token =  58547  All token =  63622  acc =  0.9202319952217787
raw: time:5.92s, speed:801.76st/s; acc: 0.9202, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.hyp

real    0m15.207s
user    0m11.987s
sys     0m3.684s
```

check the outpuot hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head -n 30 ./wordlstm-crf-charcnn.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
ရှိ O
မှု O
ကကို O
မ O
ကြြိုက် N
ဘူး E

ဒီ B
တစ် O
ခေါက် O
ကိစ္စ O
ကြောင့် O
ကျွန်တော့် O
ရရဲ့ O
သိက္ခာ O
အဖတ်ဆယ် O
လလိလို့ O
မ O
ရ O
အောင် O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

check all hyp files so far:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ wc *.hyp
  68334  127244 1051379 wordlstm-charcnn.hyp
  68334  127244 1051379 wordlstm-charlstm.hyp
  68334  127244 1051379 wordlstm-crf-charcnn.hyp
  68334  127244 1051379 wordlstm-nochar.hyp
 273336  508976 4205516 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 5. Word-LSTM, CRF, char-LSTM Training/Testing 

prepare config file:  

```
### I/O ###
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm
...
...
###NetworkConfiguration###
use_crf=True
use_char=True
word_seq_feature=LSTM
char_seq_feature=LSTM
```

training start ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.crf.char-lstm.train.config | tee ./mysent-model/wordlstm-crf-charlstm.training.log
...
...
     Iteration: 100
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
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 2.54s; loss: 2852.0717; acc: 4747/6598=0.7195
     Instance: 1000; Time: 2.66s; loss: 1393.6742; acc: 10592/13463=0.7867
...
...
...
     Instance: 30500; Time: 2.66s; loss: 8.9390; acc: 413727/413929=0.9995
     Instance: 31000; Time: 2.51s; loss: 17.0309; acc: 420138/420344=0.9995
     Instance: 31500; Time: 2.74s; loss: 21.9109; acc: 426813/427023=0.9995
     Instance: 32000; Time: 2.66s; loss: 10.6733; acc: 433866/434078=0.9995
     Instance: 32500; Time: 2.85s; loss: 10.1479; acc: 440898/441114=0.9995
     Instance: 33000; Time: 2.50s; loss: 15.6271; acc: 447312/447533=0.9995
     Instance: 33500; Time: 2.59s; loss: 22.0999; acc: 454325/454551=0.9995
     Instance: 34000; Time: 2.65s; loss: 4.1620; acc: 461453/461681=0.9995
     Instance: 34500; Time: 2.52s; loss: 6.2731; acc: 468044/468274=0.9995
     Instance: 35000; Time: 2.68s; loss: 24.2872; acc: 474637/474870=0.9995
     Instance: 35500; Time: 2.50s; loss: 6.6882; acc: 481203/481439=0.9995
     Instance: 36000; Time: 2.49s; loss: 25.8972; acc: 487768/488010=0.9995
     Instance: 36500; Time: 2.66s; loss: 2.4390; acc: 494683/494925=0.9995
     Instance: 37000; Time: 2.49s; loss: 9.3456; acc: 501543/501787=0.9995
     Instance: 37500; Time: 2.70s; loss: 15.8565; acc: 508563/508809=0.9995
     Instance: 38000; Time: 2.63s; loss: 16.7104; acc: 515453/515702=0.9995
     Instance: 38500; Time: 2.53s; loss: 10.2049; acc: 522133/522385=0.9995
     Instance: 39000; Time: 2.69s; loss: 31.6379; acc: 529071/529333=0.9995
     Instance: 39500; Time: 2.73s; loss: 15.4925; acc: 536084/536351=0.9995
     Instance: 39999; Time: 2.58s; loss: 5.8837; acc: 542873/543142=0.9995
Epoch: 99 training finished. Time: 207.21s, speed: 193.03st/s,  total loss: 1021.2640380859375
totalloss: 1021.2640380859375
Right token =  32285  All token =  32315  acc =  0.9990716385579452
Dev: time: 3.25s, speed: 746.70st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63576  All token =  63622  acc =  0.9992769796611235
Test: time: 6.64s, speed: 713.91st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    366m16.764s
user    365m24.837s
sys     0m42.253s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Preparing decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ cat ./mysent-config/word-lstm.crf.char-lstm.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Manual testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.crf.char-lstm.decode.config | tee ./mysent-model/wordlstm-crf-charlstm.decode.log
...
...
     Hyper      lstm_layer: 1
     Hyper          bilstm: True
     Hyper             GPU: True
DATA SUMMARY END.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
build CRF...
Decode raw data, nbest: None ...
Right token =  63563  All token =  63622  acc =  0.9990726478262236
raw: time:6.57s, speed:722.02st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charlstm.hyp

real    0m15.235s
user    0m12.522s
sys     0m3.079s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ head ./mysent-hyp/wordlstm-crf-charlstm.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## 6. Word-LSTM, CRF, no-char

Preparing config file:  

```
### I/O ###
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar
...
...
###NetworkConfiguration###
use_crf=True
use_char=False
word_seq_feature=LSTM
#char_seq_feature=LSTM
```

start training ...  

```

...
...
...
     Optimizer: SGD
     Iteration: 100
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
use_char:  False
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 2.34s; loss: 3149.8809; acc: 4772/6598=0.7232
     Instance: 1000; Time: 2.50s; loss: 1330.4052; acc: 10747/13463=0.7983
     Instance: 1500; Time: 2.38s; loss: 1028.0932; acc: 16734/20100=0.8325
...
...
...
     Instance: 39000; Time: 2.50s; loss: 41.3326; acc: 529325/529691=0.9993
     Instance: 39500; Time: 2.49s; loss: 25.9476; acc: 535969/536341=0.9993
     Instance: 39999; Time: 2.48s; loss: 18.9208; acc: 542764/543142=0.9993
Epoch: 26 training finished. Time: 200.88s, speed: 199.12st/s,  total loss: 1510.2309875488281
totalloss: 1510.2309875488281
Right token =  32286  All token =  32315  acc =  0.999102583939347
Dev: time: 2.76s, speed: 880.49st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63587  All token =  63622  acc =  0.9994498758291157
Test: time: 5.67s, speed: 837.40st/s; acc: 0.9994, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 27/100
 Learning rate is set as: 0.006382978723404255
Shuffle: first input word list: [464, 1019, 45, 1918, 33, 26, 743, 102, 4, 37, 2402, 70, 12, 13]
     Instance: 500; Time: 2.64s; loss: 29.0359; acc: 7113/7120=0.9990
     Instance: 1000; Time: 2.50s; loss: 25.7385; acc: 14020/14034=0.9990
     Instance: 1500; Time: 2.40s; loss: 20.6611; acc: 20551/20570=0.9991
     Instance: 2000; Time: 2.49s; loss: 23.0771; acc: 27082/27105=0.9992
     Instance: 2500; Time: 2.37s; loss: 22.4814; acc: 33565/33592=0.9992
     Instance: 3000; Time: 2.51s; loss: 16.6531; acc: 40092/40123=0.9992
     Instance: 3500; Time: 2.51s; loss: 9.8474; acc: 46945/46978=0.9993
     Instance: 4000; Time: 2.48s; loss: 24.1730; acc: 53701/53738=0.9993
     Instance: 4500; Time: 2.60s; loss: 17.0583; acc: 60530/60570=0.9993
     Instance: 5000; Time: 2.63s; loss: 22.4983; acc: 67633/67675=0.9994
     Instance: 5500; Time: 2.50s; loss: 8.9262; acc: 74514/74560=0.9994
     Instance: 6000; Time: 2.45s; loss: 22.0184; acc: 81046/81094=0.9994
     Instance: 6500; Time: 2.57s; loss: 16.4835; acc: 88030/88081=0.9994
     Instance: 7000; Time: 2.37s; loss: 8.8923; acc: 94884/94938=0.9994
     Instance: 7500; Time: 2.38s; loss: 10.2485; acc: 101885/101942=0.9994
     Instance: 8000; Time: 2.45s; loss: 13.0707; acc: 109028/109089=0.9994
     Instance: 8500; Time: 2.33s; loss: 5.8790; acc: 115951/116013=0.9995
     Instance: 9000; Time: 2.55s; loss: 6.4045; acc: 122915/122978=0.9995
     Instance: 9500; Time: 2.40s; loss: 13.6191; acc: 129379/129444=0.9995
...
...
...
     Instance: 30000; Time: 2.54s; loss: 11.4768; acc: 406742/406922=0.9996
     Instance: 30500; Time: 2.54s; loss: 5.7083; acc: 413747/413929=0.9996
     Instance: 31000; Time: 2.44s; loss: 14.2428; acc: 420159/420344=0.9996
     Instance: 31500; Time: 2.58s; loss: 7.7025; acc: 426835/427023=0.9996
     Instance: 32000; Time: 2.54s; loss: 5.4664; acc: 433888/434078=0.9996
     Instance: 32500; Time: 2.70s; loss: 4.4285; acc: 440922/441114=0.9996
     Instance: 33000; Time: 2.38s; loss: 13.7225; acc: 447335/447533=0.9996
     Instance: 33500; Time: 2.53s; loss: 16.0905; acc: 454350/454551=0.9996
     Instance: 34000; Time: 2.52s; loss: 4.6945; acc: 461477/461681=0.9996
     Instance: 34500; Time: 2.38s; loss: 4.5834; acc: 468069/468274=0.9996
     Instance: 35000; Time: 2.46s; loss: 25.4389; acc: 474661/474870=0.9996
     Instance: 35500; Time: 2.31s; loss: 3.7061; acc: 481229/481439=0.9996
     Instance: 36000; Time: 2.28s; loss: 12.3723; acc: 487795/488010=0.9996
     Instance: 36500; Time: 2.43s; loss: 3.0925; acc: 494710/494925=0.9996
     Instance: 37000; Time: 2.33s; loss: 12.0607; acc: 501569/501787=0.9996
     Instance: 37500; Time: 2.46s; loss: 10.4619; acc: 508589/508809=0.9996
     Instance: 38000; Time: 2.49s; loss: 7.9403; acc: 515480/515702=0.9996
     Instance: 38500; Time: 2.38s; loss: 8.8724; acc: 522160/522385=0.9996
     Instance: 39000; Time: 2.43s; loss: 20.8378; acc: 529099/529333=0.9996
     Instance: 39500; Time: 2.51s; loss: 13.6555; acc: 536113/536351=0.9996
     Instance: 39999; Time: 2.41s; loss: 4.3625; acc: 542902/543142=0.9996
Epoch: 99 training finished. Time: 199.39s, speed: 200.61st/s,  total loss: 782.2766418457031
totalloss: 782.2766418457031
Right token =  32285  All token =  32315  acc =  0.9990716385579452
Dev: time: 2.75s, speed: 884.41st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63580  All token =  63622  acc =  0.9993398509949388
Test: time: 5.63s, speed: 842.51st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    339m54.757s
user    339m12.320s
sys     0m31.127s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

prepare decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-lstm.crf.nochar.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-nochar.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

start manual testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-lstm.crf.nochar.decode.config | tee ./mysent-model/wordlstm-crf-nochar.decode.log
...
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build CRF...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:5.56s, speed:852.88st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-nochar.hyp

real    0m14.250s
user    0m11.479s
sys     0m3.106s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head ./wordlstm-crf-nochar.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 7. Word-CNN, Char-CNN Model

prepare config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn
#word_emb_dir=sample_data/sample.word.emb

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
use_crf=False
use_char=True
word_seq_feature=CNN
char_seq_feature=CNN
#feature=[POS] emb_size=20
...
...
...
```

start training and got error as follows ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.char-cnn.train.config | tee ./mysent-model/wordcnn-charcnn.training.log
Seed num: 42
MODEL: train
Training model...
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 31439
     Char  alphabet size: 274
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
     Model word extractor: CNN
     Model       use_char: True
     Model char extractor: CNN
     Model char_hidden_dim: 50
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 100
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
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 0.66s; loss: 25076740480520.8359; acc: 1733/6598=0.2627
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....
```

update the learning rate:  

```
#learning_rate=0.015
learning_rate=0.010
```

train again and it looks working ...  

```
...
...
...
     Instance: 20500; Time: 0.67s; loss: 111.9535; acc: 271255/277384=0.9779
     Instance: 21000; Time: 0.58s; loss: 37.9173; acc: 277511/283647=0.9784
     Instance: 21500; Time: 0.64s; loss: 57.2896; acc: 284363/290511=0.9788
     Instance: 22000; Time: 0.63s; loss: 39.8409; acc: 291155/297313=0.9793
     Instance: 22500; Time: 0.62s; loss: 52.6794; acc: 297629/303798=0.9797
     Instance: 23000; Time: 0.67s; loss: 40.9671; acc: 304457/310636=0.9801
     Instance: 23500; Time: 0.66s; loss: 27.7918; acc: 311446/317630=0.9805
     Instance: 24000; Time: 0.61s; loss: 118.8584; acc: 317936/324131=0.9809
     Instance: 24500; Time: 0.62s; loss: 159.1228; acc: 324613/330820=0.9812
     Instance: 25000; Time: 0.61s; loss: 56.5890; acc: 331645/337858=0.9816
     Instance: 25500; Time: 0.59s; loss: 53.2868; acc: 338068/344286=0.9819
     Instance: 26000; Time: 0.62s; loss: 60.5964; acc: 344780/351005=0.9823
     Instance: 26500; Time: 0.62s; loss: 19.5004; acc: 351573/357800=0.9826
     Instance: 27000; Time: 0.65s; loss: 79.3346; acc: 358649/364892=0.9829
     Instance: 27500; Time: 0.66s; loss: 69.7029; acc: 365715/371969=0.9832
     Instance: 28000; Time: 0.61s; loss: 25.8149; acc: 371987/378246=0.9835
     Instance: 28500; Time: 0.68s; loss: 44.8137; acc: 379046/385311=0.9837
     Instance: 29000; Time: 0.64s; loss: 72.8295; acc: 385613/391890=0.9840
     Instance: 29500; Time: 0.63s; loss: 29.0705; acc: 392296/398578=0.9842
     Instance: 30000; Time: 0.66s; loss: 82.0742; acc: 399292/405583=0.9845
     Instance: 30500; Time: 0.64s; loss: 9.9670; acc: 405944/412235=0.9847
     Instance: 31000; Time: 0.68s; loss: 34.5553; acc: 412869/419166=0.9850
     Instance: 31500; Time: 0.65s; loss: 28.2391; acc: 419464/425768=0.9852
     Instance: 32000; Time: 0.70s; loss: 41.5926; acc: 426758/433072=0.9854
     Instance: 32500; Time: 0.69s; loss: 102.9158; acc: 433784/440108=0.9856
     Instance: 33000; Time: 0.68s; loss: 126.6441; acc: 440679/447015=0.9858
     Instance: 33500; Time: 0.68s; loss: 124.7159; acc: 447726/454076=0.9860
     Instance: 34000; Time: 0.63s; loss: 43.2462; acc: 454325/460685=0.9862
     Instance: 34500; Time: 0.68s; loss: 104.8425; acc: 461310/467678=0.9864
     Instance: 35000; Time: 0.71s; loss: 44.8154; acc: 468443/474819=0.9866
...
...
...
     Instance: 31500; Time: 0.66s; loss: 39.0150; acc: 426695/427023=0.9992
     Instance: 32000; Time: 0.64s; loss: 98.0791; acc: 433741/434078=0.9992
     Instance: 32500; Time: 0.68s; loss: 40.7073; acc: 440771/441114=0.9992
     Instance: 33000; Time: 0.61s; loss: 39.6800; acc: 447183/447533=0.9992
     Instance: 33500; Time: 0.65s; loss: 25.8624; acc: 454197/454551=0.9992
     Instance: 34000; Time: 0.63s; loss: 37.1705; acc: 461324/461681=0.9992
     Instance: 34500; Time: 0.47s; loss: 14.6737; acc: 467914/468274=0.9992
     Instance: 35000; Time: 0.50s; loss: 27.9795; acc: 474506/474870=0.9992
     Instance: 35500; Time: 0.47s; loss: 28.1497; acc: 481072/481439=0.9992
     Instance: 36000; Time: 0.47s; loss: 36.1011; acc: 487637/488010=0.9992
     Instance: 36500; Time: 0.55s; loss: 7.0099; acc: 494552/494925=0.9992
     Instance: 37000; Time: 0.62s; loss: 22.0090; acc: 501411/501787=0.9993
     Instance: 37500; Time: 0.65s; loss: 25.4751; acc: 508430/508809=0.9993
     Instance: 38000; Time: 0.67s; loss: 22.8392; acc: 515319/515702=0.9993
     Instance: 38500; Time: 0.66s; loss: 16.3963; acc: 521998/522385=0.9993
     Instance: 39000; Time: 0.66s; loss: 141.7035; acc: 528928/529333=0.9992
     Instance: 39500; Time: 0.68s; loss: 43.6660; acc: 535941/536351=0.9992
     Instance: 39999; Time: 0.64s; loss: 18.7707; acc: 542728/543142=0.9992
Epoch: 99 training finished. Time: 50.60s, speed: 790.49st/s,  total loss: 3005.427954673767
totalloss: 3005.427954673767
Right token =  32287  All token =  32315  acc =  0.9991335293207488
Dev: time: 1.85s, speed: 1317.93st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63589  All token =  63622  acc =  0.9994813114960234
Test: time: 3.77s, speed: 1261.49st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000

real    92m0.469s
user    91m45.120s
sys     0m15.266s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the model folder:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$ ls
bk                                wordlstm-charlstm.dset             wordlstm-crf-charlstm.training.log
wordcnn-charcnn.0.model           wordlstm-charlstm.training.log     wordlstm-crf-nochar.0.model
wordcnn-charcnn.dset              wordlstm-crf-charcnn.0.model       wordlstm-crf-nochar.decode.log
wordcnn-charcnn.training.errlog1  wordlstm-crf-charcnn.decode.log    wordlstm-crf-nochar.dset
wordcnn-charcnn.training.log      wordlstm-crf-charcnn.dset          word-lstm.crf.nochar.training.log
wordlstm-charcnn.0.model          wordlstm-crf-charcnn.training.log  wordlstm-nochar.0.model
wordlstm-charcnn.dset             wordlstm-crf-charlstm.0.model      wordlstm-nochar.decode.log
wordlstm-charlstm.0.model         wordlstm-crf-charlstm.decode.log   wordlstm-nochar.dset
wordlstm-charlstm.decode.log      wordlstm-crf-charlstm.dset         wordlstm-nochar.training.log
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-model$
```

Prepare decode config ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-cnn.char-cnn.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

manual testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.char-cnn.decode.config | tee ./mysent-model/wordcnn-charcnn.decode.log
...
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:5.43s, speed:874.26st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charcnn.hyp

real    0m13.451s
user    0m11.597s
sys     0m1.538s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head ./wordcnn-charcnn.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 8. Word-CNN, Char-LSTM

prepare the config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm
#word_emb_dir=sample_data/sample.word.emb

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
use_crf=False
use_char=True
word_seq_feature=CNN
char_seq_feature=LSTM
#feature=[POS] emb_size=20
...
...
...
```

training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-config/word-cnn.char-lstm.train.config | tee ./mysent-model/wordcnn-charlstm.train.log
...
...
...
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.01
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
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: LSTM ...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.01
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 1.04s; loss: 46295.9573; acc: 4432/6598=0.6717
...
...
...
     Instance: 30500; Time: 0.93s; loss: 18.5849; acc: 413619/413929=0.9993
     Instance: 31000; Time: 0.83s; loss: 33.5528; acc: 420028/420344=0.9992
     Instance: 31500; Time: 0.87s; loss: 30.8974; acc: 426700/427023=0.9992
     Instance: 32000; Time: 0.86s; loss: 60.9885; acc: 433746/434078=0.9992
     Instance: 32500; Time: 0.87s; loss: 17.4721; acc: 440777/441114=0.9992
     Instance: 33000; Time: 0.77s; loss: 35.3249; acc: 447189/447533=0.9992
     Instance: 33500; Time: 0.83s; loss: 23.4311; acc: 454202/454551=0.9992
     Instance: 34000; Time: 0.81s; loss: 11.1323; acc: 461329/461681=0.9992
     Instance: 34500; Time: 0.84s; loss: 12.5343; acc: 467919/468274=0.9992
     Instance: 35000; Time: 0.84s; loss: 23.8477; acc: 474511/474870=0.9992
     Instance: 35500; Time: 0.83s; loss: 23.1941; acc: 481077/481439=0.9992
     Instance: 36000; Time: 0.81s; loss: 33.4580; acc: 487642/488010=0.9992
     Instance: 36500; Time: 0.86s; loss: 5.1792; acc: 494557/494925=0.9993
     Instance: 37000; Time: 0.93s; loss: 18.1748; acc: 501416/501787=0.9993
     Instance: 37500; Time: 0.93s; loss: 26.9669; acc: 508435/508809=0.9993
     Instance: 38000; Time: 0.90s; loss: 17.9885; acc: 515324/515702=0.9993
     Instance: 38500; Time: 0.84s; loss: 15.3559; acc: 522003/522385=0.9993
     Instance: 39000; Time: 0.88s; loss: 80.9564; acc: 528934/529333=0.9992
     Instance: 39500; Time: 0.87s; loss: 30.3917; acc: 535947/536351=0.9992
     Instance: 39999; Time: 0.88s; loss: 15.3817; acc: 542734/543142=0.9992
Epoch: 99 training finished. Time: 69.13s, speed: 578.58st/s,  total loss: 1997.4792351722717
totalloss: 1997.4792351722717
Right token =  32281  All token =  32315  acc =  0.9989478570323379
Dev: time: 2.47s, speed: 987.04st/s; acc: 0.9989, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63576  All token =  63622  acc =  0.9992769796611235
Test: time: 4.70s, speed: 1011.79st/s; acc: 0.9993, p: -1.0000, r: -1.0000, f: -1.0000

real    128m37.791s
user    127m32.000s
sys     0m37.373s
```

prepare decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-cnn.char-lstm.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

manual testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.char-lstm.decode.config | tee ./mysent-model/wordcnn-charlstm.decode.log
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: LSTM ...
CNN layer:  4
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:4.89s, speed:971.71st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charlstm.hyp

real    0m13.496s
user    0m11.743s
sys     0m1.405s
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head wordcnn-charlstm.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 9. Word-CNN, No-Char

prepare config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-nochar
#word_emb_dir=sample_data/sample.word.emb

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
use_crf=False
use_char=False
word_seq_feature=CNN
#char_seq_feature=LSTM
#feature=[POS] emb_size=20
...
...
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.no-char.train.config | tee ./mysent-model/wordcnn-nochar.train.log
...
...
 Hyperparameters:
     Hyper              lr: 0.01
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
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
build sequence labeling network...
use_char:  False
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.01
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 0.72s; loss: 183879.1970; acc: 3662/6598=0.5550
     Instance: 1000; Time: 0.62s; loss: 5917.1649; acc: 8716/13463=0.6474
     Instance: 1500; Time: 0.57s; loss: 4383.6639; acc: 13737/20100=0.6834
     Instance: 2000; Time: 0.53s; loss: 4228.5525; acc: 19241/27109=0.7098
     Instance: 2500; Time: 0.53s; loss: 3214.0498; acc: 24515/33628=0.7290
...
...
...
     Instance: 31000; Time: 0.43s; loss: 36.0379; acc: 420018/420344=0.9992
     Instance: 31500; Time: 0.48s; loss: 46.1417; acc: 426688/427023=0.9992
     Instance: 32000; Time: 0.58s; loss: 78.4269; acc: 433734/434078=0.9992
     Instance: 32500; Time: 0.63s; loss: 52.6536; acc: 440763/441114=0.9992
     Instance: 33000; Time: 0.54s; loss: 39.1081; acc: 447175/447533=0.9992
     Instance: 33500; Time: 0.49s; loss: 35.3635; acc: 454189/454551=0.9992
     Instance: 34000; Time: 0.45s; loss: 27.4643; acc: 461316/461681=0.9992
     Instance: 34500; Time: 0.44s; loss: 13.7139; acc: 467906/468274=0.9992
     Instance: 35000; Time: 0.46s; loss: 24.5363; acc: 474497/474870=0.9992
     Instance: 35500; Time: 0.53s; loss: 31.6647; acc: 481061/481439=0.9992
     Instance: 36000; Time: 0.53s; loss: 36.9760; acc: 487626/488010=0.9992
     Instance: 36500; Time: 0.56s; loss: 8.3417; acc: 494539/494925=0.9992
     Instance: 37000; Time: 0.55s; loss: 22.6988; acc: 501398/501787=0.9992
     Instance: 37500; Time: 0.55s; loss: 25.0444; acc: 508417/508809=0.9992
     Instance: 38000; Time: 0.46s; loss: 19.8509; acc: 515306/515702=0.9992
     Instance: 38500; Time: 0.45s; loss: 16.7377; acc: 521985/522385=0.9992
     Instance: 39000; Time: 0.46s; loss: 95.4117; acc: 528913/529333=0.9992
     Instance: 39500; Time: 0.46s; loss: 46.7911; acc: 535924/536351=0.9992
     Instance: 39999; Time: 0.45s; loss: 16.8303; acc: 542712/543142=0.9992
Epoch: 99 training finished. Time: 42.67s, speed: 937.38st/s,  total loss: 2424.9977610111237
totalloss: 2424.9977610111237
Right token =  32285  All token =  32315  acc =  0.9990716385579452
Dev: time: 1.88s, speed: 1298.77st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63589  All token =  63622  acc =  0.9994813114960234
Test: time: 4.00s, speed: 1189.38st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000

real    84m37.016s
user    83m56.073s
sys     0m14.902s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

prepare decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.nochar.decode.config
...
...
...
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.01
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
CNN layer:  4
Decode raw data, nbest: None ...
Right token =  63572  All token =  63622  acc =  0.9992141083273082
raw: time:3.75s, speed:1270.25st/s; acc: 0.9992, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-nochar.hyp

real    0m12.432s
user    0m9.680s
sys     0m3.054s
```

check the hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$ head wordcnn-nochar.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-hyp$
```

## 10. Word-CNN, CRF, Char-CNN

prepare training config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn
#word_emb_dir=sample_data/sample.word.emb

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
word_seq_feature=CNN
char_seq_feature=CNN
#feature=[POS] emb_size=20
...
...
...
```

start training word-cnn, crf, char-cnn model ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-config/word-cnn.crf.char-cnn.train.config | tee ./mysent-model/word-cnn.crf.char-cnn.training.log
...
...
...
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 2.16s; loss: 14709.3444; acc: 3933/6598=0.5961
     Instance: 1000; Time: 2.20s; loss: 679335847501542.1250; acc: 6127/13463=0.4551
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    0m19.259s
user    0m16.236s
sys     0m3.266s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Got ERROR as shown in above!  
And thus, update the learning rate as follows:  

```
#learning_rate=0.015
learning_rate=0.010
```

re-train again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-config/word-cnn.crf.char-cnn.train.config | tee ./mysent-model/word-cnn.crf.char-cnn.training.log
...
...
...
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.01
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
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.01
Shuffle: first input word list: [8895, 45, 226, 207, 1037, 644, 18, 253, 208, 254]
     Instance: 500; Time: 2.22s; loss: 9619.4552; acc: 4072/6598=0.6172
     Instance: 1000; Time: 2.29s; loss: 3674.8943; acc: 9391/13463=0.6975
...
...
...
     Instance: 30000; Time: 0.47s; loss: 20.1497; acc: 406608/406922=0.9992
     Instance: 30500; Time: 0.46s; loss: 15.6747; acc: 413610/413929=0.9992
     Instance: 31000; Time: 0.43s; loss: 36.0379; acc: 420018/420344=0.9992
     Instance: 31500; Time: 0.48s; loss: 46.1417; acc: 426688/427023=0.9992
     Instance: 32000; Time: 0.58s; loss: 78.4269; acc: 433734/434078=0.9992
     Instance: 32500; Time: 0.63s; loss: 52.6536; acc: 440763/441114=0.9992
     Instance: 33000; Time: 0.54s; loss: 39.1081; acc: 447175/447533=0.9992
     Instance: 33500; Time: 0.49s; loss: 35.3635; acc: 454189/454551=0.9992
     Instance: 34000; Time: 0.45s; loss: 27.4643; acc: 461316/461681=0.9992
     Instance: 34500; Time: 0.44s; loss: 13.7139; acc: 467906/468274=0.9992
     Instance: 35000; Time: 0.46s; loss: 24.5363; acc: 474497/474870=0.9992
     Instance: 35500; Time: 0.53s; loss: 31.6647; acc: 481061/481439=0.9992
     Instance: 36000; Time: 0.53s; loss: 36.9760; acc: 487626/488010=0.9992
     Instance: 36500; Time: 0.56s; loss: 8.3417; acc: 494539/494925=0.9992
     Instance: 37000; Time: 0.55s; loss: 22.6988; acc: 501398/501787=0.9992
     Instance: 37500; Time: 0.55s; loss: 25.0444; acc: 508417/508809=0.9992
     Instance: 38000; Time: 0.46s; loss: 19.8509; acc: 515306/515702=0.9992
     Instance: 38500; Time: 0.45s; loss: 16.7377; acc: 521985/522385=0.9992
     Instance: 39000; Time: 0.46s; loss: 95.4117; acc: 528913/529333=0.9992
     Instance: 39500; Time: 0.46s; loss: 46.7911; acc: 535924/536351=0.9992
     Instance: 39999; Time: 0.45s; loss: 16.8303; acc: 542712/543142=0.9992
Epoch: 99 training finished. Time: 42.67s, speed: 937.38st/s,  total loss: 2424.9977610111237
totalloss: 2424.9977610111237
Right token =  32285  All token =  32315  acc =  0.9990716385579452
Dev: time: 1.88s, speed: 1298.77st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63589  All token =  63622  acc =  0.9994813114960234
Test: time: 4.00s, speed: 1189.38st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000

real    84m37.016s
user    83m56.073s
sys     0m14.902s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

prepare manual checking. At 1st I need to create a decode configuration file as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$ cat word-cnn.crf.char-cnn.decode.config
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-crf-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config$
```

run manual testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-config/word-cnn.crf.char-cnn.decode.config | tee
./mysent-model/wordcnn.crf.charcnn.decode.log
...
...
...
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
build CRF...
Decode raw data, nbest: None ...
Right token =  63589  All token =  63622  acc =  0.9994813114960234
raw: time:5.57s, speed:852.53st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-crf-charcnn.hyp

real    0m14.296s
user    0m11.311s
sys     0m3.144s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ head ./mysent-hyp/wordcnn-crf-charcnn.hyp
အခု B
သန့်စင်ခန်း N
ကကို N
သသုံး N
ပါရစေ E

လူငယ် B
တွေ O
က O
ပပုံစံတကျ O
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## 11. Word-CNN, CRF, Char-LSTM

prepare the config file:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm
#word_emb_dir=sample_data/sample.word.emb

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
word_seq_feature=CNN
char_seq_feature=LSTM
#feature=[POS] emb_size=20
...
...
...
```

start training Word-CNN, CRF, Char-LSTM ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-config/word-cnn.crf.char-lstm.train.config | tee ./mysent-model/word-cnn.crf.char-lstm.training.log
...
...
...
     Dev   instance number: 2414
     Test  instance number: 4712
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: True
     Model word extractor: CNN
     Model       use_char: True
     Model char extractor: LSTM
     Model char_hidden_dim: 50
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 100
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.01
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
...
...
...
     Instance: 33500; Time: 2.71s; loss: 89.1120; acc: 450743/454076=0.9927
     Instance: 34000; Time: 2.47s; loss: 44.3172; acc: 457345/460685=0.9927
     Instance: 34500; Time: 2.68s; loss: 61.8543; acc: 464330/467678=0.9928
     Instance: 35000; Time: 2.80s; loss: 42.6160; acc: 471465/474819=0.9929
     Instance: 35500; Time: 2.75s; loss: 18.5766; acc: 478705/482061=0.9930
     Instance: 36000; Time: 2.65s; loss: 45.8868; acc: 485281/488644=0.9931
     Instance: 36500; Time: 2.68s; loss: 35.7804; acc: 492016/495386=0.9932
     Instance: 37000; Time: 2.61s; loss: 77.9952; acc: 498888/502268=0.9933
     Instance: 37500; Time: 2.64s; loss: 77.2073; acc: 505813/509202=0.9933
     Instance: 38000; Time: 2.51s; loss: 83.5568; acc: 512236/515634=0.9934
     Instance: 38500; Time: 2.69s; loss: 25.0363; acc: 519113/522512=0.9935
     Instance: 39000; Time: 2.68s; loss: 62.0210; acc: 525813/529223=0.9936
     Instance: 39500; Time: 2.64s; loss: 18.2599; acc: 532746/536159=0.9936
     Instance: 39999; Time: 2.72s; loss: 39.4828; acc: 539723/543142=0.9937
Epoch: 0 training finished. Time: 204.92s, speed: 195.19st/s,  total loss: 43944.579750061035
totalloss: 43944.579750061035
Right token =  32287  All token =  32315  acc =  0.9991335293207488
Dev: time: 3.12s, speed: 777.69st/s; acc: 0.9991, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm.0.model
Right token =  63589  All token =  63622  acc =  0.9994813114960234
Test: time: 6.39s, speed: 743.47st/s; acc: 0.9995, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 1/100
 Learning rate is set as: 0.009523809523809523
Shuffle: first input word list: [20733, 2180, 20734, 325, 130, 325, 872, 130, 872, 214]
     Instance: 500; Time: 2.73s; loss: 23.1693; acc: 7006/7008=0.9997
     Instance: 1000; Time: 2.47s; loss: 44.3065; acc: 13303/13314=0.9992
     Instance: 1500; Time: 2.75s; loss: 86.1397; acc: 20303/20328=0.9988
     Instance: 2000; Time: 2.71s; loss: 38.1606; acc: 26981/27011=0.9989
     Instance: 2500; Time: 2.51s; loss: 59.5888; acc: 33237/33274=0.9989
     Instance: 3000; Time: 2.75s; loss: 22.1511; acc: 40138/40177=0.9990
...
...
...

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
