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

## Prepare Config File for Word-LSTM, Char-CNN Model

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
335                     fout.write(content_list[idx][0][idy].encode('utf-8') + " " + predict_results[idx][idy].encode('utf-8')     + '\n')
```

test again ...  

```

```

```

```

## Word-LSTM, Char-LSTM

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
