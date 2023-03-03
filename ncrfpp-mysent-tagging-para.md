# Log of using NCRF++ for Burmese Sentence, Paragraph level Tokenization

## Check the data

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/data/para$ ls
test.col  train.col  valid.col
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/data/para$ wc *.col
  102144   193264  1578958 test.col
  881245  1668486 13659721 train.col
   64861   123564  1004217 valid.col
 1048250  1985314 16242896 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/data/para$
```

Check the content and you can see some are containing more than one sentence boundary or paragraph level:  

```
553 မျာ O
   554 က O
   555 မူ O
   556 နိမ့် O
   557 ကျ O
   558 နေ O
   559 မည် N
   560 သာ N
   561 ဖြစ် N
   562 သည် E
   563 ဂျီဒီပီ B
   564 ကို O
   565 ဖောညွှန်း O
   566 ရာတွင် O
   567 ၎င်း O
   568 သည် O
   569 လူနေမှု O
   570 အဆင့်အတန်း O
   571 ကို O
   572 မှန်ကန် O
   573 စွာ O
   574 ပြသ O
   575 နိုင် O
   576 ခြင်း O
   577 ကြေင့် O

```

Paragraph level data folder path is here:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/data/para$ pwd
/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para
```

## 1. Word-LSTM, Char-CNN Model for Para

updated configuration file is as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat ./word-lstm.char-cnn.train.config 
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
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
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

Start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.char-cnn.train.config | tee word-lstm.char-cnn.train.log
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
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
Traceback (most recent call last):
  File "main.py", line 554, in <module>
    train(data)
  File "main.py", line 359, in train
    data.save(save_data_name)
  File "/home/yekyaw.thu/tool/NCRFpp/utils/data.py", line 348, in save
    f = open(save_file, 'wb')
FileNotFoundError: [Errno 2] No such file or directory: '/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.dset'

real	0m19.214s
user	0m13.190s
sys	0m3.539s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 

```

The error was caused by the folder not existing ... 
we can solve by creating a new folder.  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ mkdir mysent-para-model
```

Train again and now it looks OK ...   

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ mkdir mysent-para-model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.char-cnn.train.config | tee word-lstm.char-cnn.train.log
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
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 1.76s; loss: 10790.0235; acc: 5384/8986=0.5992
     Instance: 1000; Time: 1.09s; loss: 12297.4426; acc: 11267/18422=0.6116
     Instance: 1500; Time: 1.08s; loss: 8075.7405; acc: 17846/27720=0.6438
     Instance: 2000; Time: 1.00s; loss: 5275.8963; acc: 25201/36837=0.6841
     Instance: 2500; Time: 1.03s; loss: 4471.8586; acc: 32198/45333=0.7103
     Instance: 3000; Time: 1.09s; loss: 3475.3374; acc: 40807/55086=0.7408
     Instance: 3500; Time: 1.03s; loss: 3418.2947; acc: 48680/64013=0.7605
     Instance: 4000; Time: 0.94s; loss: 1926.9387; acc: 56657/72548=0.7810
     Instance: 4500; Time: 0.97s; loss: 1897.5351; acc: 64927/81330=0.7983
     Instance: 5000; Time: 0.98s; loss: 2097.1930; acc: 73021/90054=0.8109
     Instance: 5500; Time: 1.05s; loss: 1671.1433; acc: 81815/99330=0.8237
     Instance: 6000; Time: 0.96s; loss: 1355.5104; acc: 89730/107637=0.8336
     Instance: 6500; Time: 1.14s; loss: 2283.6650; acc: 98903/117489=0.8418
     Instance: 7000; Time: 1.05s; loss: 1684.7256; acc: 107639/126691=0.8496
     Instance: 7500; Time: 0.85s; loss: 1203.1433; acc: 115265/134642=0.8561
     Instance: 8000; Time: 1.04s; loss: 1221.1892; acc: 123818/143526=0.8627
     Instance: 8500; Time: 1.15s; loss: 1298.6809; acc: 133060/153140=0.8689
     Instance: 9000; Time: 0.96s; loss: 1492.4648; acc: 141071/161594=0.8730
     Instance: 9500; Time: 0.99s; loss: 1441.0668; acc: 149495/170409=0.8773
     Instance: 10000; Time: 1.01s; loss: 1291.3247; acc: 157725/179025=0.8810
     Instance: 10500; Time: 1.05s; loss: 1407.5102; acc: 166322/188031=0.8845
     Instance: 11000; Time: 1.02s; loss: 1538.7158; acc: 174379/196518=0.8873
     Instance: 11500; Time: 1.00s; loss: 1217.8906; acc: 182800/205293=0.8904
     Instance: 12000; Time: 1.14s; loss: 1248.6998; acc: 191827/214657=0.8936
     Instance: 12500; Time: 1.08s; loss: 1070.5011; acc: 199992/223137=0.8963
     Instance: 13000; Time: 1.00s; loss: 898.5888; acc: 208421/231856=0.8989
     Instance: 13500; Time: 1.04s; loss: 1744.1111; acc: 217227/241147=0.9008
     Instance: 14000; Time: 0.94s; loss: 1127.0457; acc: 225113/249342=0.9028
     Instance: 14500; Time: 1.05s; loss: 1255.2128; acc: 234171/258771=0.9049
     Instance: 15000; Time: 1.07s; loss: 1248.0089; acc: 243328/268300=0.9069
     Instance: 15500; Time: 1.08s; loss: 1352.4110; acc: 252421/277791=0.9087
     Instance: 16000; Time: 1.02s; loss: 978.1289; acc: 260892/286523=0.9105
     Instance: 16500; Time: 0.87s; loss: 760.7298; acc: 268752/294589=0.9123
     Instance: 17000; Time: 0.99s; loss: 1286.3216; acc: 277101/303313=0.9136
     Instance: 17500; Time: 1.02s; loss: 847.0396; acc: 285497/311971=0.9151
     Instance: 18000; Time: 0.99s; loss: 1228.2156; acc: 293798/320643=0.9163
     Instance: 18500; Time: 1.02s; loss: 1382.5466; acc: 302703/329931=0.9175
     Instance: 19000; Time: 1.05s; loss: 936.8404; acc: 311454/338955=0.9189
     Instance: 19500; Time: 1.00s; loss: 814.2907; acc: 319756/347494=0.9202
     Instance: 20000; Time: 1.10s; loss: 1220.1704; acc: 328626/356767=0.9211
     Instance: 20500; Time: 1.00s; loss: 996.7514; acc: 336965/365383=0.9222
     Instance: 21000; Time: 0.92s; loss: 910.7727; acc: 345203/373870=0.9233
     Instance: 21500; Time: 1.04s; loss: 1306.6395; acc: 353750/382752=0.9242
     Instance: 22000; Time: 1.00s; loss: 862.0979; acc: 362006/391246=0.9253
     Instance: 22500; Time: 1.00s; loss: 844.4382; acc: 370363/399868=0.9262
     Instance: 23000; Time: 1.05s; loss: 1023.2634; acc: 379020/408790=0.9272
     Instance: 23500; Time: 1.02s; loss: 1235.7338; acc: 387682/417834=0.9278
     Instance: 24000; Time: 1.06s; loss: 1088.3663; acc: 396004/426458=0.9286
     Instance: 24500; Time: 0.99s; loss: 950.0223; acc: 404517/435249=0.9294
     Instance: 25000; Time: 0.84s; loss: 780.2522; acc: 411822/442766=0.9301
     Instance: 25500; Time: 0.98s; loss: 1086.0028; acc: 420541/451849=0.9307
     Instance: 26000; Time: 1.03s; loss: 1029.9263; acc: 429129/460748=0.9314
     Instance: 26500; Time: 1.09s; loss: 1034.1390; acc: 438296/470217=0.9321
     Instance: 27000; Time: 1.01s; loss: 831.1940; acc: 446988/479158=0.9329
     Instance: 27500; Time: 1.08s; loss: 926.9705; acc: 455968/488411=0.9336
     Instance: 28000; Time: 0.87s; loss: 737.0355; acc: 463491/496155=0.9342
     Instance: 28500; Time: 1.00s; loss: 976.0128; acc: 471947/504926=0.9347
     Instance: 29000; Time: 1.10s; loss: 1085.2103; acc: 481130/514484=0.9352
     Instance: 29500; Time: 1.02s; loss: 1289.5396; acc: 489994/523716=0.9356
     Instance: 30000; Time: 0.92s; loss: 1249.5083; acc: 498399/532520=0.9359
     Instance: 30500; Time: 1.01s; loss: 5536.0288; acc: 506588/541568=0.9354
     Instance: 31000; Time: 1.11s; loss: 24623.8233; acc: 511727/551041=0.9287
     Instance: 31500; Time: 0.98s; loss: 10790.1060; acc: 516944/559822=0.9234
     Instance: 32000; Time: 1.04s; loss: 9763.5663; acc: 522687/568802=0.9189
     Instance: 32500; Time: 1.00s; loss: 9667.8669; acc: 528012/577324=0.9146
     Instance: 33000; Time: 0.93s; loss: 8900.7370; acc: 533149/585642=0.9104
     Instance: 33500; Time: 0.96s; loss: 9537.6716; acc: 538584/594254=0.9063
     Instance: 34000; Time: 1.04s; loss: 9195.0570; acc: 544583/603374=0.9026
     Instance: 34500; Time: 0.93s; loss: 8899.0011; acc: 549723/611606=0.8988
...
...
...
     Instance: 39000; Time: 1.00s; loss: 8055.2369; acc: 446999/688416=0.6493
     Instance: 39500; Time: 1.07s; loss: 8405.9689; acc: 452941/697512=0.6494
     Instance: 40000; Time: 0.94s; loss: 7934.5509; acc: 457938/705583=0.6490
     Instance: 40500; Time: 1.01s; loss: 8180.0877; acc: 463049/713889=0.6486
     Instance: 41000; Time: 1.18s; loss: 9082.2049; acc: 469746/723934=0.6489
     Instance: 41500; Time: 1.02s; loss: 7958.0003; acc: 475267/732499=0.6488
     Instance: 42000; Time: 1.03s; loss: 8384.0976; acc: 480825/741220=0.6487
     Instance: 42500; Time: 1.04s; loss: 8284.9904; acc: 487120/750561=0.6490
     Instance: 43000; Time: 1.00s; loss: 7860.5160; acc: 492743/759167=0.6491
     Instance: 43500; Time: 1.02s; loss: 7940.9433; acc: 498053/767562=0.6489
     Instance: 44000; Time: 1.09s; loss: 8268.6946; acc: 503835/776526=0.6488
     Instance: 44500; Time: 1.00s; loss: 8276.1509; acc: 509478/785275=0.6488
     Instance: 45000; Time: 1.07s; loss: 7976.1302; acc: 515314/794097=0.6489
     Instance: 45500; Time: 1.00s; loss: 7924.1464; acc: 520775/802609=0.6489
     Instance: 46000; Time: 1.21s; loss: 8560.8406; acc: 527170/812146=0.6491
     Instance: 46500; Time: 1.13s; loss: 8330.1233; acc: 533190/821309=0.6492
     Instance: 46991; Time: 1.19s; loss: 8428.5512; acc: 539661/830865=0.6495
Epoch: 99 training finished. Time: 96.87s, speed: 485.07st/s,  total loss: 770966.3493289948
totalloss: 770966.3493289948
Right token =  41293  All token =  61166  acc =  0.6750972762645915
Dev: time: 4.36s, speed: 711.40st/s; acc: 0.6751, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  63320  All token =  95820  acc =  0.6608223752869965
Test: time: 6.76s, speed: 822.24st/s; acc: 0.6608, p: -1.0000, r: -1.0000, f: -1.0000

real    178m12.415s
user    177m29.905s
sys     0m36.526s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Check the output models:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-model$ ls
wordlstm-charcnn.0.model  wordlstm-charcnn.dset
```

original decoder configuration file:  


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

I updated the word-lstm.char-cnn.decode.config file as follows:  

```
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.0.model
```

Testing for word-lstm, char-CNN ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ python main.py --config ./mysent-para-config/word-lstm.char-cnn.decode.config
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  ||| 
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charcnn.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Decode raw data, nbest: None ...
Right token =  71570  All token =  95820  acc =  0.7469213107910666
raw: time:6.67s, speed:832.95st/s; acc: 0.7469, p: -1.0000, r: -1.0000, f: -1.0000
Traceback (most recent call last):
  File "main.py", line 568, in <module>
    data.write_decoded_results(decode_results, 'raw')
  File "/home/yekyaw.thu/tool/NCRFpp/utils/data.py", line 326, in write_decoded_results
    fout = open(self.decode_dir,'w')
FileNotFoundError: [Errno 2] No such file or directory: '/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charcnn.hyp'
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

I just need to create a new folder named "mysent-para-hyp". After that testing process finished successfully.  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ python main.py --config ./mysent-para-config/word-lstm.char-cnn.decode.config
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  ||| 
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charcnn.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
build sequence labeling network...
use_char:  True
char feature extractor:  CNN
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
Decode raw data, nbest: None ...
Right token =  71570  All token =  95820  acc =  0.7469213107910666
raw: time:6.72s, speed:826.93st/s; acc: 0.7469, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charcnn.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

Check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head wordlstm-charcnn.hyp 
ရင်ဘတ် O
အောင့် O
လာ O
ရင် O
သတိထား O
ပါ E

ဘယ်လောက် O
နောက်ကျ O
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ tail ./wordlstm-charcnn.hyp 
ကို O
အာမခံ O
ရင်းနှီးမြှုပ်နှံ O
ခြင်း O
၌ O
သာ O
ထည့်သွင်း O
ခဲ့ N
သည် E

(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

## 2. Word-LSTM, Char-LSTM for Para

I updated the config file as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat ./word-lstm.char-lstm.train.config 
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm
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
char_seq_feature=LSTM
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
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

start training:  
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.char-lstm.train.config

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.char-lstm.train.config 
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
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
     Model word extractor: LSTM
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
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
     Instance: 500; Time: 1.31s; loss: 12459.2498; acc: 5275/8986=0.5870
     Instance: 1000; Time: 1.36s; loss: 7661.1749; acc: 12354/18422=0.6706
     Instance: 1500; Time: 1.35s; loss: 2991.5909; acc: 20766/27720=0.7491
     Instance: 2000; Time: 1.24s; loss: 3997.3874; acc: 28880/36837=0.7840
     Instance: 2500; Time: 1.26s; loss: 1826.3337; acc: 36817/45333=0.8121
     Instance: 3000; Time: 1.36s; loss: 1742.7966; acc: 46067/55086=0.8363
     Instance: 3500; Time: 1.29s; loss: 2150.3358; acc: 54374/64013=0.8494
     Instance: 4000; Time: 1.20s; loss: 1296.2241; acc: 62521/72548=0.8618
     Instance: 4500; Time: 1.22s; loss: 1327.6168; acc: 70932/81330=0.8722
     Instance: 5000; Time: 1.23s; loss: 1656.5050; acc: 79165/90054=0.8791
     Instance: 5500; Time: 1.29s; loss: 1381.3704; acc: 88050/99330=0.8864
     Instance: 6000; Time: 1.17s; loss: 1194.8294; acc: 96003/107637=0.8919
     Instance: 6500; Time: 1.38s; loss: 1941.5996; acc: 105267/117489=0.8960
     Instance: 7000; Time: 1.28s; loss: 1316.4940; acc: 114096/126691=0.9006
     Instance: 7500; Time: 1.04s; loss: 1075.1369; acc: 121751/134642=0.9043
     Instance: 8000; Time: 1.32s; loss: 1062.4804; acc: 130331/143526=0.9081
     Instance: 8500; Time: 1.43s; loss: 1092.1585; acc: 139625/153140=0.9117
     Instance: 9000; Time: 1.25s; loss: 1375.8386; acc: 147656/161594=0.9137
     Instance: 9500; Time: 1.26s; loss: 1353.0280; acc: 156065/170409=0.9158
     Instance: 10000; Time: 1.26s; loss: 1090.4099; acc: 164344/179025=0.9180
     Instance: 10500; Time: 1.34s; loss: 1158.3194; acc: 173017/188031=0.9202
     Instance: 11000; Time: 1.23s; loss: 1477.3702; acc: 181083/196518=0.9215
     Instance: 11500; Time: 1.20s; loss: 1125.6883; acc: 189535/205293=0.9232
     Instance: 12000; Time: 1.36s; loss: 1177.8499; acc: 198580/214657=0.9251
     Instance: 12500; Time: 1.25s; loss: 893.3073; acc: 206782/223137=0.9267
     Instance: 13000; Time: 1.24s; loss: 894.4175; acc: 215221/231856=0.9283
     Instance: 13500; Time: 1.26s; loss: 1466.7354; acc: 224104/241147=0.9293
     Instance: 14000; Time: 1.18s; loss: 1029.9115; acc: 232005/249342=0.9305
     Instance: 14500; Time: 1.29s; loss: 1182.0759; acc: 241057/258771=0.9315
     Instance: 15000; Time: 1.31s; loss: 1198.8035; acc: 250204/268300=0.9326
     Instance: 15500; Time: 1.34s; loss: 1227.4013; acc: 259330/277791=0.9335
     Instance: 16000; Time: 1.25s; loss: 992.2340; acc: 267785/286523=0.9346
     Instance: 16500; Time: 1.12s; loss: 744.5523; acc: 275656/294589=0.9357
     Instance: 17000; Time: 1.22s; loss: 1117.0356; acc: 284025/303313=0.9364
     Instance: 17500; Time: 1.29s; loss: 751.5129; acc: 292456/311971=0.9374
     Instance: 18000; Time: 1.22s; loss: 1188.1151; acc: 300772/320643=0.9380
     Instance: 18500; Time: 1.26s; loss: 1326.4613; acc: 309669/329931=0.9386
     Instance: 19000; Time: 1.28s; loss: 839.9887; acc: 318428/338955=0.9394
     Instance: 19500; Time: 1.24s; loss: 768.8566; acc: 326741/347494=0.9403
     Instance: 20000; Time: 1.35s; loss: 1150.8768; acc: 335655/356767=0.9408
     Instance: 20500; Time: 1.22s; loss: 970.0665; acc: 343975/365383=0.9414
     Instance: 21000; Time: 1.18s; loss: 814.2408; acc: 352249/373870=0.9422
     Instance: 21500; Time: 1.28s; loss: 1292.3664; acc: 360771/382752=0.9426
     Instance: 22000; Time: 1.21s; loss: 816.5467; acc: 369048/391246=0.9433
     Instance: 22500; Time: 1.23s; loss: 788.0702; acc: 377416/399868=0.9439
     Instance: 23000; Time: 1.28s; loss: 939.2576; acc: 386082/408790=0.9445
     Instance: 23500; Time: 1.26s; loss: 1186.4809; acc: 394754/417834=0.9448
...
...
...
     Instance: 36500; Time: 1.32s; loss: 444.2724; acc: 636573/647075=0.9838
     Instance: 37000; Time: 1.22s; loss: 497.9287; acc: 644802/655461=0.9837
     Instance: 37500; Time: 1.18s; loss: 357.5980; acc: 652760/663541=0.9838
     Instance: 38000; Time: 1.25s; loss: 395.0356; acc: 661446/672356=0.9838
     Instance: 38500; Time: 1.24s; loss: 636.2169; acc: 670075/681179=0.9837
     Instance: 39000; Time: 1.26s; loss: 363.0957; acc: 678467/689699=0.9837
     Instance: 39500; Time: 1.15s; loss: 473.6052; acc: 686551/697954=0.9837
     Instance: 40000; Time: 1.19s; loss: 350.0457; acc: 694588/706106=0.9837
     Instance: 40500; Time: 1.33s; loss: 472.1805; acc: 703502/715171=0.9837
     Instance: 41000; Time: 1.23s; loss: 480.3558; acc: 712003/723841=0.9836
     Instance: 41500; Time: 1.34s; loss: 507.1719; acc: 720772/732779=0.9836
     Instance: 42000; Time: 1.34s; loss: 534.5273; acc: 729763/741925=0.9836
     Instance: 42500; Time: 1.34s; loss: 412.0626; acc: 738721/751024=0.9836
     Instance: 43000; Time: 1.28s; loss: 470.7889; acc: 747516/759995=0.9836
     Instance: 43500; Time: 1.29s; loss: 427.7811; acc: 756098/768713=0.9836
     Instance: 44000; Time: 1.32s; loss: 392.9026; acc: 765022/777781=0.9836
     Instance: 44500; Time: 1.31s; loss: 487.6864; acc: 773994/786908=0.9836
     Instance: 45000; Time: 1.20s; loss: 360.1833; acc: 782176/795196=0.9836
     Instance: 45500; Time: 1.36s; loss: 578.3460; acc: 791479/804683=0.9836
     Instance: 46000; Time: 1.38s; loss: 498.9690; acc: 800417/813771=0.9836
     Instance: 46500; Time: 1.24s; loss: 384.5167; acc: 808807/822288=0.9836
     Instance: 46991; Time: 1.31s; loss: 276.4893; acc: 817296/830865=0.9837
Epoch: 7 training finished. Time: 119.63s, speed: 392.80st/s,  total loss: 41218.15336751938
totalloss: 41218.15336751938
...
...
...
     Instance: 46000; Time: 1.26s; loss: 229.1858; acc: 803351/812915=0.9882
     Instance: 46500; Time: 1.34s; loss: 381.4396; acc: 812667/822354=0.9882
     Instance: 46991; Time: 1.21s; loss: 263.6168; acc: 821086/830865=0.9882
Epoch: 13 training finished. Time: 119.92s, speed: 391.86st/s,  total loss: 29571.654337882996
totalloss: 29571.654337882996
Right token =  59667  All token =  61166  acc =  0.97549292090377
Dev: time: 5.03s, speed: 615.79st/s; acc: 0.9755, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93783  All token =  95820  acc =  0.9787413901064496
Test: time: 7.83s, speed: 708.98st/s; acc: 0.9787, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 14/100
 Learning rate is set as: 0.008823529411764704
Shuffle: first input word list: [217, 28, 1916, 1492, 218, 219, 727, 211, 6481, 161, 58, 1997, 26, 1101, 227, 615, 616, 16, 3, 17, 217, 28, 1916, 1492, 218, 219, 727, 224, 225, 387, 10820, 103, 2938, 8275, 125, 17, 75, 212, 76, 3, 17, 1303, 1009, 1814, 10968, 2521, 31, 381, 84, 350, 30, 26, 2701, 350, 8153, 3363, 3364, 84, 44, 1602, 615, 58, 103, 142, 403, 615, 1922, 7, 17, 75, 621, 103, 3, 17, 224, 736, 339, 17173, 614, 740, 742, 227, 615, 639, 740, 6645, 53, 339, 64, 6252, 74, 26, 35340, 26, 740, 745, 238, 211, 55, 418, 224, 74, 125, 1524, 39, 17, 75, 698, 3363, 3364, 84, 22, 103, 3, 17]
     Instance: 500; Time: 1.31s; loss: 257.4089; acc: 9365/9443=0.9917
     Instance: 1000; Time: 1.34s; loss: 262.9889; acc: 18418/18589=0.9908
     Instance: 1500; Time: 1.32s; loss: 310.1795; acc: 27845/28118=0.9903
     Instance: 2000; Time: 1.25s; loss: 277.2599; acc: 36539/36892=0.9904
...
...
...
     Instance: 38500; Time: 1.32s; loss: 60.8587; acc: 677609/679528=0.9972
     Instance: 39000; Time: 1.26s; loss: 54.4053; acc: 686477/688416=0.9972
     Instance: 39500; Time: 1.32s; loss: 90.9273; acc: 695543/697512=0.9972
     Instance: 40000; Time: 1.16s; loss: 107.0561; acc: 703573/705583=0.9972
     Instance: 40500; Time: 1.22s; loss: 95.3938; acc: 711849/713889=0.9971
     Instance: 41000; Time: 1.42s; loss: 43.6163; acc: 721879/723934=0.9972
     Instance: 41500; Time: 1.27s; loss: 100.5937; acc: 730411/732499=0.9971
     Instance: 42000; Time: 1.28s; loss: 115.8460; acc: 739094/741220=0.9971
     Instance: 42500; Time: 1.32s; loss: 76.2116; acc: 748406/750561=0.9971
     Instance: 43000; Time: 1.23s; loss: 45.2679; acc: 756997/759167=0.9971
     Instance: 43500; Time: 1.24s; loss: 70.9187; acc: 765369/767562=0.9971
     Instance: 44000; Time: 1.32s; loss: 93.0323; acc: 774301/776526=0.9971
     Instance: 44500; Time: 1.23s; loss: 87.3522; acc: 783022/785275=0.9971
     Instance: 45000; Time: 1.30s; loss: 60.2741; acc: 791824/794097=0.9971
     Instance: 45500; Time: 1.21s; loss: 85.2000; acc: 800307/802609=0.9971
     Instance: 46000; Time: 1.40s; loss: 117.7220; acc: 809814/812146=0.9971
     Instance: 46500; Time: 1.32s; loss: 93.3217; acc: 818944/821309=0.9971
     Instance: 46991; Time: 1.37s; loss: 82.0321; acc: 828474/830865=0.9971
Epoch: 99 training finished. Time: 115.00s, speed: 408.60st/s,  total loss: 7499.891728878021
totalloss: 7499.891728878021
Right token =  59588  All token =  61166  acc =  0.9742013536932282
Dev: time: 5.16s, speed: 600.23st/s; acc: 0.9742, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93725  All token =  95820  acc =  0.9781360884992695
Test: time: 8.02s, speed: 691.47st/s; acc: 0.9781, p: -1.0000, r: -1.0000, f: -1.0000

real	219m32.625s
user	218m28.939s
sys	0m59.616s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

During the above training, GPU usage info is as follows:  

```
(base) yekyaw.thu@gpu:~$ nvidia-smi 
Fri Mar  3 11:00:33 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 47%   52C    P2    62W / 300W |    972MiB / 11019MiB |     25%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   57C    P8    22W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 30%   42C    P8    28W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   1576443      C   python                            969MiB |
+-----------------------------------------------------------------------------+
```

Updating the decoding config file:  

```
(base) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.char-lstm.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.0.model
(base) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

Testing word-lstm, char-lstm model ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ python main.py --config ./mysent-para-config/word-lstm.char-lstm.decode.config | tee ./mysent-para-hyp/word-lstm.char-lstm.decode.log
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  ||| 
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charlstm.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
     Model word extractor: LSTM
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
Decode raw data, nbest: None ...
Right token =  93219  All token =  95820  acc =  0.9728553537883532
raw: time:8.14s, speed:681.19st/s; acc: 0.9729, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-charlstm.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## 3. Word-LSTM, no-Char

updated the configuration file path:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ head word-lstm.no-char.train.config 
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar
#word_emb_dir=sample_data/sample.word.emb

#raw_dir=
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.no-char.train.config | tee ./mysent-para-model/word-lstm.no-char.train.log
...
...
...
    Instance: 42000; Time: 0.90s; loss: 100.6102; acc: 738983/742050=0.9959
     Instance: 42500; Time: 0.91s; loss: 94.4225; acc: 747586/750675=0.9959
     Instance: 43000; Time: 0.95s; loss: 89.8823; acc: 756448/759558=0.9959
     Instance: 43500; Time: 0.85s; loss: 136.5128; acc: 764588/767737=0.9959
     Instance: 44000; Time: 0.93s; loss: 118.1706; acc: 773311/776491=0.9959
     Instance: 44500; Time: 0.93s; loss: 131.3572; acc: 782306/785539=0.9959
     Instance: 45000; Time: 1.00s; loss: 137.2240; acc: 791110/794393=0.9959
     Instance: 45500; Time: 0.86s; loss: 131.9354; acc: 800389/803710=0.9959
     Instance: 46000; Time: 0.86s; loss: 112.1066; acc: 809515/812873=0.9959
     Instance: 46500; Time: 0.83s; loss: 140.0418; acc: 818168/821577=0.9959
     Instance: 46991; Time: 0.85s; loss: 160.2210; acc: 827405/830865=0.9958
Epoch: 64 training finished. Time: 88.40s, speed: 531.57st/s,  total loss: 11053.333110809326
totalloss: 11053.333110809326
Right token =  59610  All token =  61166  acc =  0.9745610306379361
Dev: time: 4.29s, speed: 722.73st/s; acc: 0.9746, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93671  All token =  95820  acc =  0.9775725318305155
Test: time: 6.64s, speed: 837.17st/s; acc: 0.9776, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 65/100
 Learning rate is set as: 0.003529411764705882
Shuffle: first input word list: [12, 13, 11, 136, 117, 1832, 652, 62, 928, 8127, 64, 213, 325, 43]
     Instance: 500; Time: 1.04s; loss: 94.6396; acc: 9057/9088=0.9966
     Instance: 1000; Time: 0.95s; loss: 123.1377; acc: 17824/17890=0.9963
     Instance: 1500; Time: 0.96s; loss: 96.7923; acc: 26296/26394=0.9963
     Instance: 2000; Time: 0.94s; loss: 138.5908; acc: 35206/35354=0.9958
     Instance: 2500; Time: 1.05s; loss: 84.9632; acc: 44819/44994=0.9961
     Instance: 3000; Time: 0.86s; loss: 100.2892; acc: 53209/53415=0.9961
     Instance: 3500; Time: 0.96s; loss: 135.6386; acc: 62466/62717=0.9960
     Instance: 4000; Time: 0.97s; loss: 129.2650; acc: 71108/71392=0.9960
...
...
...
     Instance: 39000; Time: 0.94s; loss: 48.0611; acc: 686233/688416=0.9968
     Instance: 39500; Time: 0.96s; loss: 105.7282; acc: 695298/697512=0.9968
     Instance: 40000; Time: 0.84s; loss: 120.2424; acc: 703331/705583=0.9968
     Instance: 40500; Time: 0.90s; loss: 97.6547; acc: 711606/713889=0.9968
     Instance: 41000; Time: 1.07s; loss: 64.1625; acc: 721633/723934=0.9968
     Instance: 41500; Time: 0.94s; loss: 109.0360; acc: 730170/732499=0.9968
     Instance: 42000; Time: 0.95s; loss: 109.5624; acc: 738859/741220=0.9968
     Instance: 42500; Time: 0.96s; loss: 85.8571; acc: 748165/750561=0.9968
     Instance: 43000; Time: 0.90s; loss: 56.2921; acc: 756754/759167=0.9968
     Instance: 43500; Time: 0.92s; loss: 78.4095; acc: 765123/767562=0.9968
     Instance: 44000; Time: 0.97s; loss: 82.6637; acc: 774063/776526=0.9968
     Instance: 44500; Time: 0.91s; loss: 73.7280; acc: 782788/785275=0.9968
     Instance: 45000; Time: 0.95s; loss: 53.0030; acc: 791593/794097=0.9968
     Instance: 45500; Time: 0.88s; loss: 60.8436; acc: 800088/802609=0.9969
     Instance: 46000; Time: 1.06s; loss: 98.0884; acc: 809598/812146=0.9969
     Instance: 46500; Time: 1.00s; loss: 101.0202; acc: 818725/821309=0.9969
     Instance: 46991; Time: 1.07s; loss: 124.1936; acc: 828248/830865=0.9969
Epoch: 99 training finished. Time: 88.42s, speed: 531.47st/s,  total loss: 8092.2655148506165
totalloss: 8092.2655148506165
Right token =  59643  All token =  61166  acc =  0.9751005460549979
Dev: time: 4.38s, speed: 707.54st/s; acc: 0.9751, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93657  All token =  95820  acc =  0.9774264245460238
Test: time: 6.79s, speed: 818.66st/s; acc: 0.9774, p: -1.0000, r: -1.0000, f: -1.0000

real    165m26.723s
user    164m42.235s
sys     0m39.334s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Check the output models:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ ls ./mysent-para-model/
word-lstm.no-char.train.log  wordlstm-charlstm.0.model  wordlstm-nochar.dset
wordlstm-charcnn.0.model     wordlstm-charlstm.dset
wordlstm-charcnn.dset        wordlstm-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

updated the decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.no-char.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-nochar.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

decoding or testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.
no-char.decode.config | tee ./mysent-para-hyp/word-lstm.no-char.decode.log
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
DATA SUMMARY START:
 I/O:
     Start   Sequence   Laebling   task...
     Tag          scheme: NoSeg
     Split         token:  |||
     MAX SENTENCE LENGTH: 250
     MAX   WORD   LENGTH: -1
     Number   normalized: True
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
...
...
...
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
Decode raw data, nbest: None ...
Right token =  93330  All token =  95820  acc =  0.9740137758296806
raw: time:6.54s, speed:850.34st/s; acc: 0.9740, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-nochar.hyp

real    0m16.820s
user    0m14.047s
sys     0m3.989s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head wordlstm-nochar.hyp 
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ tail wordlstm-nochar.hyp 
ကို O
အာမခံ O
ရင်းှီးမှုပ်ှံ O
ခြင်း O
၌ O
သာ N
ထ့်သွင်း N
ခဲ့ N
သည် E

(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

## 4. Word-LSTM, CRF, Char-CNN for Para

update the training config file word-lstm.crf.char-cnn.train.config as follows:  

```
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn
#word_emb_dir=sample_data/sample.word.emb

#raw_dir=
#decode_dir=
#dset_dir=
#load_model_dir=
#char_emb_dir=
...
...
...
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.char-cnn.train.config | tee ./mysent-para-model/word-lstm.crf.char-cnn.train.log
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cd ..
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.
crf.char-cnn.train.config | tee ./mysent-para-model/word-lstm.crf.char-cnn.train.log
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
     Word  alphabet size: 44645
     Char  alphabet size: 289
     Label alphabet size: 5
     Word embedding  dir: None
     Char embedding  dir: None
     Word embedding size: 50
     Char embedding size: 30
     Norm   word     emb: False
     Norm   char     emb: False
     Train  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
     Dev    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
     Test   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
     Raw    file directory: None
     Dset   file directory: None
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn
     Loadmodel   directory: None
     Decode file directory: None
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: CNN ...
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 3.94s; loss: 7324.8873; acc: 5845/8986=0.6505
     Instance: 1000; Time: 3.94s; loss: 4510.3625; acc: 12959/18422=0.7035
     Instance: 1500; Time: 3.91s; loss: 4478.3415; acc: 19836/27720=0.7156
...
...
...
     Instance: 40000; Time: 2.97s; loss: 1504.8323; acc: 585476/707610=0.8274
     Instance: 40500; Time: 3.27s; loss: 1624.0425; acc: 592473/716015=0.8275
     Instance: 41000; Time: 3.33s; loss: 2043.9598; acc: 599740/725002=0.8272
     Instance: 41500; Time: 3.07s; loss: 1658.7612; acc: 606779/733507=0.8272
     Instance: 42000; Time: 3.36s; loss: 1736.5604; acc: 614820/743196=0.8273
     Instance: 42500; Time: 3.09s; loss: 1634.1801; acc: 622132/751968=0.8273
     Instance: 43000; Time: 3.25s; loss: 1959.0534; acc: 629611/761065=0.8273
     Instance: 43500; Time: 3.52s; loss: 1560.3316; acc: 637211/770039=0.8275
     Instance: 44000; Time: 2.98s; loss: 1614.4415; acc: 644050/778323=0.8275
     Instance: 44500; Time: 3.23s; loss: 1659.4012; acc: 651324/787054=0.8275
     Instance: 45000; Time: 3.54s; loss: 2181.1871; acc: 658855/796341=0.8274
     Instance: 45500; Time: 3.37s; loss: 1573.4761; acc: 665767/804592=0.8275
     Instance: 46000; Time: 3.22s; loss: 1604.5508; acc: 672681/813030=0.8274
     Instance: 46500; Time: 3.23s; loss: 1661.0756; acc: 679868/821589=0.8275
     Instance: 46991; Time: 3.46s; loss: 1955.6072; acc: 687362/830865=0.8273
Epoch: 42 training finished. Time: 322.57s, speed: 145.68st/s,  total loss: 164395.65701293945
totalloss: 164395.65701293945
Right token =  50337  All token =  61166  acc =  0.8229571984435797
Dev: time: 6.27s, speed: 493.63st/s; acc: 0.8230, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  79652  All token =  95820  acc =  0.8312669588812357
Test: time: 9.69s, speed: 571.89st/s; acc: 0.8313, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 43/100
 Learning rate is set as: 0.0047619047619047615
Shuffle: first input word list: [2157, 23545, 538, 7, 26767, 1112, 11, 136, 142, 3438, 1004, 148, 1994, 213, 40, 254, 354, 612, 33, 359, 538, 7, 26768, 1983, 16, 110, 43]
     Instance: 500; Time: 3.43s; loss: 1736.1742; acc: 7021/8758=0.8017
     Instance: 1000; Time: 3.36s; loss: 1708.7863; acc: 13775/17109=0.8051
     Instance: 1500; Time: 3.21s; loss: 1576.8992; acc: 20965/25640=0.8177
...
...
...

```

update the decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.crf.char-cnn.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
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
