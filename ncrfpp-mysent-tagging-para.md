# Log of using NCRF++ for Burmese Sentence, Paragraph Level Tokenization

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
    Instance: 42500; Time: 3.41s; loss: 1638.4393; acc: 624165/751445=0.8306
     Instance: 43000; Time: 3.65s; loss: 1722.6729; acc: 631879/760791=0.8306
     Instance: 43500; Time: 3.75s; loss: 1799.8394; acc: 639670/770200=0.8305
     Instance: 44000; Time: 3.92s; loss: 1651.5987; acc: 647496/779460=0.8307
     Instance: 44500; Time: 3.03s; loss: 1641.1499; acc: 654382/787815=0.8306
     Instance: 45000; Time: 3.77s; loss: 1688.5475; acc: 661911/796987=0.8305
     Instance: 45500; Time: 3.48s; loss: 1650.3399; acc: 668837/805428=0.8304
     Instance: 46000; Time: 3.47s; loss: 1794.6227; acc: 676170/814348=0.8303
     Instance: 46500; Time: 3.78s; loss: 1719.5959; acc: 683966/823631=0.8304
     Instance: 46991; Time: 2.84s; loss: 1308.7112; acc: 690011/830865=0.8305
Epoch: 52 training finished. Time: 326.80s, speed: 143.79st/s,  total loss: 159282.6750640869
totalloss: 159282.6750640869
Right token =  50821  All token =  61166  acc =  0.8308700912271524
Dev: time: 6.25s, speed: 494.79st/s; acc: 0.8309, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  80645  All token =  95820  acc =  0.8416301398455437
Test: time: 9.65s, speed: 574.23st/s; acc: 0.8416, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 53/100
 Learning rate is set as: 0.00410958904109589
Shuffle: first input word list: [499, 211, 16, 227, 110, 264, 211, 39, 379]
     Instance: 500; Time: 3.40s; loss: 1567.9048; acc: 7092/8465=0.8378
     Instance: 1000; Time: 3.64s; loss: 1825.2925; acc: 14229/17075=0.8333
     Instance: 1500; Time: 3.20s; loss: 1706.8028; acc: 21011/25414=0.8267
     Instance: 2000; Time: 3.59s; loss: 1933.2480; acc: 28065/34233=0.8198
     Instance: 2500; Time: 3.41s; loss: 1519.4224; acc: 35435/42896=0.8261
     Instance: 3000; Time: 3.19s; loss: 1554.5344; acc: 42152/51057=0.8256
     Instance: 3500; Time: 3.48s; loss: 1749.9654; acc: 49295/59622=0.8268
     Instance: 4000; Time: 3.49s; loss: 1602.3575; acc: 55882/67690=0.8256
     Instance: 4500; Time: 3.57s; loss: 1680.1721; acc: 63701/76950=0.8278
...
...
...
     Instance: 35000; Time: 2.88s; loss: 1311.4248; acc: 536727/615220=0.8724
     Instance: 35500; Time: 3.20s; loss: 1477.0385; acc: 544412/624125=0.8723
     Instance: 36000; Time: 3.27s; loss: 1449.6358; acc: 552609/633543=0.8723
     Instance: 36500; Time: 2.94s; loss: 1399.5276; acc: 560098/642188=0.8722
     Instance: 37000; Time: 3.48s; loss: 1340.9169; acc: 568334/651553=0.8723
     Instance: 37500; Time: 3.68s; loss: 1531.5441; acc: 576813/661280=0.8723
     Instance: 38000; Time: 3.10s; loss: 1422.2231; acc: 584501/670190=0.8721
     Instance: 38500; Time: 3.43s; loss: 1486.9084; acc: 592599/679528=0.8721
     Instance: 39000; Time: 3.15s; loss: 1257.4983; acc: 600412/688416=0.8722
     Instance: 39500; Time: 3.28s; loss: 1378.8034; acc: 608324/697512=0.8721
     Instance: 40000; Time: 2.80s; loss: 1355.2287; acc: 615287/705583=0.8720
     Instance: 40500; Time: 3.00s; loss: 1368.2898; acc: 622404/713889=0.8718
     Instance: 41000; Time: 3.62s; loss: 1411.0026; acc: 631260/723934=0.8720
     Instance: 41500; Time: 3.16s; loss: 1278.3615; acc: 638756/732499=0.8720
     Instance: 42000; Time: 3.19s; loss: 1361.8578; acc: 646344/741220=0.8720
     Instance: 42500; Time: 3.26s; loss: 1329.2454; acc: 654608/750561=0.8722
     Instance: 43000; Time: 3.04s; loss: 1270.9861; acc: 662153/759167=0.8722
     Instance: 43500; Time: 3.08s; loss: 1358.5962; acc: 669418/767562=0.8721
     Instance: 44000; Time: 3.28s; loss: 1401.1083; acc: 677134/776526=0.8720
     Instance: 44500; Time: 3.01s; loss: 1298.2113; acc: 684852/785275=0.8721
     Instance: 45000; Time: 3.30s; loss: 1243.6690; acc: 692690/794097=0.8723
     Instance: 45500; Time: 3.35s; loss: 1322.9982; acc: 700104/802609=0.8723
     Instance: 46000; Time: 3.89s; loss: 1420.7540; acc: 708491/812146=0.8724
     Instance: 46500; Time: 3.36s; loss: 1389.8244; acc: 716503/821309=0.8724
     Instance: 46991; Time: 3.68s; loss: 1421.0689; acc: 724853/830865=0.8724
Epoch: 99 training finished. Time: 317.17s, speed: 148.16st/s,  total loss: 127352.55563354492
totalloss: 127352.55563354492
Right token =  52508  All token =  61166  acc =  0.8584507733054311
Dev: time: 6.34s, speed: 487.75st/s; acc: 0.8585, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  83091  All token =  95820  acc =  0.8671571696931747
Test: time: 9.79s, speed: 566.06st/s; acc: 0.8672, p: -1.0000, r: -1.0000, f: -1.0000

real    994m50.095s
user    572m20.855s
sys     0m43.869s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

GPU usage of during the training time:  

```
(base) yekyaw.thu@gpu:~$ nvidia-smi
Sat Mar  4 06:12:09 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 47%   52C    P2    62W / 300W |   1070MiB / 11019MiB |     18%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   59C    P8    23W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 29%   42C    P8    27W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   1610644      C   python                           1067MiB |
+-----------------------------------------------------------------------------+
(base) yekyaw.thu@gpu:~$
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

check the model:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ ls ./mysent-para-model/
word-lstm.crf.char-cnn.train.log  wordlstm-charcnn.dset      wordlstm-crf-charcnn.0.model  wordlstm-nochar.dset
word-lstm.no-char.train.log       wordlstm-charlstm.0.model  wordlstm-crf-charcnn.dset
wordlstm-charcnn.0.model          wordlstm-charlstm.dset     wordlstm-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

decoding/testing as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-lstm.crf.char-cnn.decode.config  | tee ./mysent-para-hyp/word-lstm.crf.char-cnn.decode.log
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn
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
Right token =  79652  All token =  95820  acc =  0.8312669588812357
raw: time:9.91s, speed:559.16st/s; acc: 0.8313, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charcnn.hyp

real    0m21.362s
user    0m17.307s
sys     0m4.069s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## 5. Word-LSTM, CRF, char-LSTM for Para

updated the training config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.crf.char-lstm.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
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

training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.char-lstm.train.config | tee ./mysent-para-model/word-lstm.crf.char-lstm.train.log
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.char-lstm.train.confi
g | tee ./mysent-para-model/word-lstm.crf.char-lstm.train.log
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
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
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build char sequence feature extractor: LSTM ...
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 3.75s; loss: 14276.9692; acc: 5666/8986=0.6305
     Instance: 1000; Time: 3.95s; loss: 5370.2555; acc: 12576/18422=0.6827
     Instance: 1500; Time: 3.96s; loss: 3484.2863; acc: 19765/27720=0.7130
     Instance: 2000; Time: 3.57s; loss: 3154.0246; acc: 27226/36837=0.7391
     Instance: 2500; Time: 3.61s; loss: 2034.0629; acc: 34257/45333=0.7557
     Instance: 3000; Time: 4.02s; loss: 2552.0627; acc: 42369/55086=0.7691
     Instance: 3500; Time: 3.56s; loss: 2405.4625; acc: 49949/64013=0.7803
     Instance: 4000; Time: 3.37s; loss: 1488.8825; acc: 57514/72548=0.7928
     Instance: 4500; Time: 3.42s; loss: 1323.6360; acc: 65468/81330=0.8050
     Instance: 5000; Time: 3.47s; loss: 1107.8257; acc: 73464/90054=0.8158
     Instance: 5500; Time: 3.81s; loss: 868.8950; acc: 82177/99330=0.8273
     Instance: 6000; Time: 3.31s; loss: 714.7874; acc: 89965/107637=0.8358
     Instance: 6500; Time: 4.06s; loss: 1470.1029; acc: 98920/117489=0.8420
     Instance: 7000; Time: 3.85s; loss: 1115.1653; acc: 107385/126691=0.8476
     Instance: 7500; Time: 3.12s; loss: 507.4101; acc: 114983/134642=0.8540
     Instance: 8000; Time: 3.74s; loss: 509.0321; acc: 123482/143526=0.8603
     Instance: 8500; Time: 4.20s; loss: 582.5710; acc: 132618/153140=0.8660
...
...
...
     Instance: 38000; Time: 3.84s; loss: 396.9952; acc: 631573/675031=0.9356
     Instance: 38500; Time: 3.51s; loss: 373.7010; acc: 639807/683594=0.9359
     Instance: 39000; Time: 4.04s; loss: 704.6858; acc: 648405/692759=0.9360
     Instance: 39500; Time: 3.46s; loss: 367.8224; acc: 656689/701354=0.9363
     Instance: 40000; Time: 3.24s; loss: 277.8111; acc: 664499/709420=0.9367
     Instance: 40500; Time: 3.38s; loss: 222.3538; acc: 672090/717207=0.9371
     Instance: 41000; Time: 3.37s; loss: 188.3755; acc: 680300/725578=0.9376
     Instance: 41500; Time: 3.42s; loss: 283.8201; acc: 688614/734127=0.9380
     Instance: 42000; Time: 3.76s; loss: 315.6052; acc: 697241/742998=0.9384
     Instance: 42500; Time: 3.27s; loss: 298.0320; acc: 705132/751145=0.9387
     Instance: 43000; Time: 3.58s; loss: 408.6880; acc: 713828/760169=0.9390
     Instance: 43500; Time: 3.66s; loss: 331.0091; acc: 722236/768845=0.9394
     Instance: 44000; Time: 3.60s; loss: 306.2902; acc: 730548/777474=0.9396
     Instance: 44500; Time: 4.15s; loss: 337.7666; acc: 739474/786667=0.9400
     Instance: 45000; Time: 3.75s; loss: 406.3377; acc: 748119/795694=0.9402
     Instance: 45500; Time: 3.49s; loss: 190.1212; acc: 756625/804405=0.9406
     Instance: 46000; Time: 3.43s; loss: 468.9996; acc: 764732/812921=0.9407
     Instance: 46500; Time: 3.74s; loss: 386.0850; acc: 773455/821965=0.9410
     Instance: 46991; Time: 3.74s; loss: 427.0599; acc: 781972/830865=0.9412
Epoch: 0 training finished. Time: 344.35s, speed: 136.46st/s,  total loss: 78174.59733581543
totalloss: 78174.59733581543
Right token =  58492  All token =  61166  acc =  0.9562829022659648
Dev: time: 7.16s, speed: 432.05st/s; acc: 0.9563, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.0.model
Right token =  92576  All token =  95820  acc =  0.966144854936339
Test: time: 11.09s, speed: 499.70st/s; acc: 0.9661, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 1/100
 Learning rate is set as: 0.014285714285714285
Shuffle: first input word list: [2020, 2395, 1947, 75, 14205, 287, 213, 211, 10]
     Instance: 500; Time: 3.63s; loss: 423.2202; acc: 8580/8917=0.9622
     Instance: 1000; Time: 4.00s; loss: 349.2446; acc: 16851/17478=0.9641
     Instance: 1500; Time: 3.84s; loss: 345.2303; acc: 25539/26480=0.9645
     Instance: 2000; Time: 3.36s; loss: 312.0641; acc: 33458/34684=0.9647
     Instance: 2500; Time: 3.67s; loss: 388.1206; acc: 42049/43631=0.9637
...
...
...
     Instance: 40500; Time: 3.84s; loss: 51.8544; acc: 712155/715880=0.9948
     Instance: 41000; Time: 4.09s; loss: 28.6877; acc: 722138/725884=0.9948
     Instance: 41500; Time: 3.21s; loss: 53.1214; acc: 730465/734254=0.9948
     Instance: 42000; Time: 3.45s; loss: 63.3383; acc: 738621/742444=0.9949
     Instance: 42500; Time: 3.44s; loss: 78.3049; acc: 746962/750830=0.9948
     Instance: 43000; Time: 3.71s; loss: 73.3126; acc: 755818/759729=0.9949
     Instance: 43500; Time: 3.90s; loss: 58.7230; acc: 764838/768805=0.9948
     Instance: 44000; Time: 3.40s; loss: 90.8388; acc: 773361/777365=0.9948
     Instance: 44500; Time: 3.80s; loss: 49.8689; acc: 782122/786172=0.9948
     Instance: 45000; Time: 3.57s; loss: 41.8989; acc: 791113/795228=0.9948
     Instance: 45500; Time: 3.66s; loss: 61.7054; acc: 800099/804246=0.9948
     Instance: 46000; Time: 3.69s; loss: 43.3694; acc: 808700/812886=0.9949
     Instance: 46500; Time: 3.87s; loss: 34.6245; acc: 817850/822068=0.9949
     Instance: 46991; Time: 3.69s; loss: 47.4368; acc: 826592/830865=0.9949
Epoch: 93 training finished. Time: 341.47s, speed: 137.61st/s,  total loss: 5597.382923126221
totalloss: 5597.382923126221
Right token =  59552  All token =  61166  acc =  0.97361279142007
Dev: time: 7.11s, speed: 434.85st/s; acc: 0.9736, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93703  All token =  95820  acc =  0.9779064913379253
Test: time: 11.00s, speed: 503.63st/s; acc: 0.9779, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 94/100
 Learning rate is set as: 0.002631578947368421
Shuffle: first input word list: [698, 1173, 6, 414, 2826, 17]
     Instance: 500; Time: 3.29s; loss: 56.5557; acc: 8293/8335=0.9950
     Instance: 1000; Time: 3.65s; loss: 52.6010; acc: 17082/17152=0.9959
     Instance: 1500; Time: 4.14s; loss: 47.4343; acc: 26784/26898=0.9958
     Instance: 2000; Time: 3.54s; loss: 54.5467; acc: 35564/35720=0.9956
     Instance: 2500; Time: 3.96s; loss: 71.7267; acc: 44925/45136=0.9953
     Instance: 3000; Time: 3.80s; loss: 53.7801; acc: 53553/53798=0.9954
     Instance: 3500; Time: 3.55s; loss: 54.5492; acc: 62320/62633=0.9950
     Instance: 4000; Time: 3.96s; loss: 58.6943; acc: 71222/71583=0.9950
     Instance: 4500; Time: 3.42s; loss: 42.6348; acc: 79838/80236=0.9950
     Instance: 5000; Time: 3.22s; loss: 76.6777; acc: 87816/88262=0.9949
     Instance: 5500; Time: 3.68s; loss: 66.2483; acc: 96721/97239=0.9947
     Instance: 6000; Time: 3.72s; loss: 68.6164; acc: 105995/106601=0.9943
...
...
...
     Instance: 42000; Time: 3.70s; loss: 84.0823; acc: 737398/741220=0.9948
     Instance: 42500; Time: 3.80s; loss: 44.1889; acc: 746693/750561=0.9948
     Instance: 43000; Time: 3.58s; loss: 45.6605; acc: 755267/759167=0.9949
     Instance: 43500; Time: 3.58s; loss: 54.0104; acc: 763590/767562=0.9948
     Instance: 44000; Time: 3.82s; loss: 61.5463; acc: 772471/776526=0.9948
     Instance: 44500; Time: 3.51s; loss: 61.1354; acc: 781163/785275=0.9948
     Instance: 45000; Time: 3.76s; loss: 46.9988; acc: 789966/794097=0.9948
     Instance: 45500; Time: 3.51s; loss: 44.3897; acc: 798439/802609=0.9948
     Instance: 46000; Time: 4.18s; loss: 80.7507; acc: 807901/812146=0.9948
     Instance: 46500; Time: 3.90s; loss: 77.7663; acc: 817012/821309=0.9948
     Instance: 46991; Time: 4.22s; loss: 66.7824; acc: 826516/830865=0.9948
Epoch: 99 training finished. Time: 347.41s, speed: 135.26st/s,  total loss: 5490.974273681641
totalloss: 5490.974273681641
Right token =  59562  All token =  61166  acc =  0.9737762809403917
Dev: time: 7.11s, speed: 434.76st/s; acc: 0.9738, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93624  All token =  95820  acc =  0.9770820288040075
Test: time: 11.02s, speed: 502.61st/s; acc: 0.9771, p: -1.0000, r: -1.0000, f: -1.0000

real    607m38.155s
user    606m45.274s
sys     0m52.858s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

updated decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.crf.char-lstm.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

decoding or testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.char-lstm.decode.conf
ig | tee ./mysent-para-hyp/word-lstm.crf.char-lstm.decode.log
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
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charlstm.hyp
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
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
Right token =  92576  All token =  95820  acc =  0.966144854936339
raw: time:10.68s, speed:518.51st/s; acc: 0.9661, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charlstm.hyp

real    0m20.819s
user    0m18.107s
sys     0m3.418s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

## 6. Word-LSTM, CRF, no-char for Para

update the training config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.crf.nochar.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar
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
use_char=False
word_seq_feature=LSTM
#char_seq_feature=LSTM
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

training NCRF++ model ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.nochar.train.config | tee ./mysent-para-model/word-lstm.crf.nochar.train.log
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar
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
     Model       use_char: False
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
use_char:  False
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build CRF...
Epoch: 0/100
 Learning rate is set as: 0.015
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 3.56s; loss: 13380.8050; acc: 5623/8986=0.6258
     Instance: 1000; Time: 3.80s; loss: 4842.2639; acc: 12699/18422=0.6893
     Instance: 1500; Time: 3.79s; loss: 3626.8603; acc: 19884/27720=0.7173
     Instance: 2000; Time: 3.43s; loss: 2728.5185; acc: 27408/36837=0.7440
     Instance: 2500; Time: 3.46s; loss: 1655.6122; acc: 34731/45333=0.7661
     Instance: 3000; Time: 3.85s; loss: 1923.1299; acc: 43319/55086=0.7864
     Instance: 3500; Time: 3.40s; loss: 1829.0894; acc: 51205/64013=0.7999
     Instance: 4000; Time: 3.21s; loss: 1283.5985; acc: 58936/72548=0.8124
     Instance: 4500; Time: 3.27s; loss: 1050.9283; acc: 67028/81330=0.8241
     Instance: 5000; Time: 3.31s; loss: 1151.1816; acc: 74993/90054=0.8328
     Instance: 5500; Time: 3.60s; loss: 1038.9179; acc: 83622/99330=0.8419
     Instance: 6000; Time: 3.11s; loss: 739.1563; acc: 91405/107637=0.8492
     Instance: 6500; Time: 3.89s; loss: 1212.1253; acc: 100434/117489=0.8548
     Instance: 7000; Time: 3.69s; loss: 1217.2444; acc: 108890/126691=0.8595
     Instance: 7500; Time: 2.95s; loss: 554.1054; acc: 116489/134642=0.8652
     Instance: 8000; Time: 3.55s; loss: 506.7917; acc: 124969/143526=0.8707
     Instance: 8500; Time: 3.98s; loss: 781.1161; acc: 134083/153140=0.8756
     Instance: 9000; Time: 3.29s; loss: 741.5675; acc: 141993/161594=0.8787
...
...
...
     Instance: 42500; Time: 2.89s; loss: 233.3054; acc: 730604/750689=0.9732
     Instance: 43000; Time: 3.67s; loss: 230.5071; acc: 739872/760164=0.9733
     Instance: 43500; Time: 3.33s; loss: 214.1456; acc: 748751/769227=0.9734
     Instance: 44000; Time: 3.35s; loss: 249.7282; acc: 757535/778290=0.9733
     Instance: 44500; Time: 3.04s; loss: 229.3465; acc: 766060/787036=0.9733
     Instance: 45000; Time: 3.55s; loss: 188.5981; acc: 775049/796203=0.9734
     Instance: 45500; Time: 3.30s; loss: 190.7173; acc: 783931/805287=0.9735
     Instance: 46000; Time: 2.61s; loss: 212.6500; acc: 791267/812805=0.9735
     Instance: 46500; Time: 3.67s; loss: 288.6054; acc: 800622/822417=0.9735
     Instance: 46991; Time: 3.21s; loss: 195.8808; acc: 808895/830865=0.9736
Epoch: 3 training finished. Time: 317.84s, speed: 147.84st/s,  total loss: 23818.703735351562
totalloss: 23818.703735351562
Right token =  59030  All token =  61166  acc =  0.9650786384592748
Dev: time: 6.42s, speed: 481.95st/s; acc: 0.9651, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93171  All token =  95820  acc =  0.9723544145272386
Test: time: 9.88s, speed: 560.60st/s; acc: 0.9724, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 4/100
 Learning rate is set as: 0.0125
Shuffle: first input word list: [3645, 339, 6, 1225, 62, 399, 26, 727, 6, 161, 62, 209]
     Instance: 500; Time: 2.97s; loss: 194.6525; acc: 8503/8724=0.9747
     Instance: 1000; Time: 3.01s; loss: 213.2381; acc: 16994/17406=0.9763
     Instance: 1500; Time: 3.39s; loss: 322.2999; acc: 26072/26790=0.9732
     Instance: 2000; Time: 2.97s; loss: 300.5726; acc: 34344/35328=0.9721
     Instance: 2500; Time: 3.31s; loss: 299.9358; acc: 43335/44602=0.9716
     Instance: 3000; Time: 3.11s; loss: 197.0675; acc: 51970/53462=0.9721
...
...
...
     Instance: 36000; Time: 3.76s; loss: 54.3616; acc: 630321/633543=0.9949
     Instance: 36500; Time: 3.47s; loss: 50.9158; acc: 638890/642188=0.9949
     Instance: 37000; Time: 4.00s; loss: 58.1296; acc: 648211/651553=0.9949
     Instance: 37500; Time: 4.17s; loss: 74.5347; acc: 657883/661280=0.9949
     Instance: 38000; Time: 3.60s; loss: 64.1405; acc: 666746/670190=0.9949
     Instance: 38500; Time: 3.96s; loss: 85.0800; acc: 676037/679528=0.9949
     Instance: 39000; Time: 3.65s; loss: 35.6143; acc: 684900/688416=0.9949
     Instance: 39500; Time: 3.83s; loss: 51.0587; acc: 693941/697512=0.9949
     Instance: 40000; Time: 3.31s; loss: 73.4226; acc: 701973/705583=0.9949
     Instance: 40500; Time: 3.50s; loss: 51.0468; acc: 710220/713889=0.9949
     Instance: 41000; Time: 4.16s; loss: 40.2164; acc: 720223/723934=0.9949
     Instance: 41500; Time: 3.70s; loss: 86.1519; acc: 728722/732499=0.9948
     Instance: 42000; Time: 3.70s; loss: 84.0823; acc: 737398/741220=0.9948
     Instance: 42500; Time: 3.80s; loss: 44.1889; acc: 746693/750561=0.9948
     Instance: 43000; Time: 3.58s; loss: 45.6605; acc: 755267/759167=0.9949
     Instance: 43500; Time: 3.58s; loss: 54.0104; acc: 763590/767562=0.9948
     Instance: 44000; Time: 3.82s; loss: 61.5463; acc: 772471/776526=0.9948
     Instance: 44500; Time: 3.51s; loss: 61.1354; acc: 781163/785275=0.9948
     Instance: 45000; Time: 3.76s; loss: 46.9988; acc: 789966/794097=0.9948
     Instance: 45500; Time: 3.51s; loss: 44.3897; acc: 798439/802609=0.9948
     Instance: 46000; Time: 4.18s; loss: 80.7507; acc: 807901/812146=0.9948
     Instance: 46500; Time: 3.90s; loss: 77.7663; acc: 817012/821309=0.9948
     Instance: 46991; Time: 4.22s; loss: 66.7824; acc: 826516/830865=0.9948
Epoch: 99 training finished. Time: 347.41s, speed: 135.26st/s,  total loss: 5490.974273681641
totalloss: 5490.974273681641
Right token =  59562  All token =  61166  acc =  0.9737762809403917
Dev: time: 7.11s, speed: 434.76st/s; acc: 0.9738, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93624  All token =  95820  acc =  0.9770820288040075
Test: time: 11.02s, speed: 502.61st/s; acc: 0.9771, p: -1.0000, r: -1.0000, f: -1.0000

real    607m38.155s
user    606m45.274s
sys     0m52.858s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

During the training time, GPU usage is as follows:  

```
(base) yekyaw.thu@gpu:~$ nvidia-smi
Sun Mar  5 10:41:43 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 46%   51C    P2    61W / 300W |    908MiB / 11019MiB |     17%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   55C    P8    21W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 32%   44C    P8    29W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   1712407      C   python                            905MiB |
+-----------------------------------------------------------------------------+
(base) yekyaw.thu@gpu:~$
```

updated decode/testing config file is as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-lstm.crf.nochar.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-nochar.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

decoding/testing results:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-lstm.crf.char-lstm.decode.config | tee ./mysent-para-hyp/word-lstm.crf.char-lstm.decode.log
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
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charlstm.hyp
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
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
Right token =  92576  All token =  95820  acc =  0.966144854936339
raw: time:11.07s, speed:500.38st/s; acc: 0.9661, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordlstm-crf-charlstm.hyp

real    0m19.461s
user    0m18.891s
sys     0m1.793s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

check the hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head ./wordlstm-crf-charlstm.hyp 
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ 
```

check the filesize of all hyp until now:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ wc *.hyp
 101330  191640 1565878 wordlstm-charcnn.hyp
 101330  191640 1565878 wordlstm-charlstm.hyp
 101330  191640 1565878 wordlstm-crf-charcnn.hyp
 101330  191640 1565878 wordlstm-crf-charlstm.hyp
 101330  191640 1565878 wordlstm-nochar.hyp
 506650  958200 7829390 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

## 7. Word-CNN, Char-CNN Model

update the training config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.char-cnn.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
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
#learning_rate=0.015
learning_rate=0.010
lr_decay=0.05
momentum=0
l2=1e-8
gpu=True
#clip=
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.char-cnn.train.config | tee 
./mysent-para-model/word-cnn.char-cnn.train.log
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
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
char feature extractor:  CNN
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.01
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.98s; loss: 21917.8533; acc: 5075/8986=0.5648
     Instance: 1000; Time: 0.84s; loss: 8712.6092; acc: 11587/18422=0.6290
     Instance: 1500; Time: 0.84s; loss: 7902.5994; acc: 18221/27720=0.6573
     Instance: 2000; Time: 0.78s; loss: 7290.8950; acc: 24894/36837=0.6758
     Instance: 2500; Time: 0.79s; loss: 7022.7807; acc: 30957/45333=0.6829
     Instance: 3000; Time: 0.85s; loss: 7562.7922; acc: 38225/55086=0.6939
     Instance: 3500; Time: 0.79s; loss: 7050.1962; acc: 44792/64013=0.6997
     Instance: 4000; Time: 0.74s; loss: 6862.9593; acc: 51016/72548=0.7032
     Instance: 4500; Time: 0.76s; loss: 6818.0427; acc: 57497/81330=0.7070
     Instance: 5000; Time: 0.76s; loss: 7026.1879; acc: 63851/90054=0.7090
     Instance: 5500; Time: 0.81s; loss: 7156.4938; acc: 70770/99330=0.7125
     Instance: 6000; Time: 0.74s; loss: 6562.9919; acc: 76793/107637=0.7134
     Instance: 6500; Time: 0.83s; loss: 7761.6377; acc: 84044/117489=0.7153
     Instance: 7000; Time: 0.83s; loss: 7098.7576; acc: 90847/126691=0.7171
     Instance: 7500; Time: 0.69s; loss: 6307.4122; acc: 96569/134642=0.7172
     Instance: 8000; Time: 0.82s; loss: 6947.2950; acc: 103074/143526=0.7182
     Instance: 8500; Time: 0.89s; loss: 7200.1042; acc: 110309/153140=0.7203
     Instance: 9000; Time: 0.76s; loss: 7035.8102; acc: 116270/161594=0.7195
     Instance: 9500; Time: 0.78s; loss: 6914.5889; acc: 122711/170409=0.7201
     Instance: 10000; Time: 0.78s; loss: 6905.4336; acc: 128960/179025=0.7203
     Instance: 10500; Time: 0.82s; loss: 7101.3592; acc: 135541/188031=0.7208
     Instance: 11000; Time: 0.77s; loss: 6873.3247; acc: 141626/196518=0.7207
...
...
...
     Instance: 39500; Time: 3.09s; loss: 83.8029; acc: 696020/701462=0.9922
     Instance: 40000; Time: 3.34s; loss: 67.2991; acc: 704350/709833=0.9923
     Instance: 40500; Time: 3.30s; loss: 80.1154; acc: 712771/718325=0.9923
     Instance: 41000; Time: 3.26s; loss: 78.5268; acc: 721190/726819=0.9923
     Instance: 41500; Time: 3.35s; loss: 65.1119; acc: 729272/734962=0.9923
     Instance: 42000; Time: 3.25s; loss: 77.8246; acc: 737981/743738=0.9923
     Instance: 42500; Time: 3.49s; loss: 87.3988; acc: 746619/752427=0.9923
     Instance: 43000; Time: 3.51s; loss: 74.1756; acc: 755281/761149=0.9923
     Instance: 43500; Time: 2.85s; loss: 95.3387; acc: 763183/769108=0.9923
     Instance: 44000; Time: 3.23s; loss: 68.8041; acc: 771293/777282=0.9923
     Instance: 44500; Time: 3.55s; loss: 83.9823; acc: 780066/786131=0.9923
     Instance: 45000; Time: 3.77s; loss: 77.6759; acc: 789304/795428=0.9923
     Instance: 45500; Time: 3.38s; loss: 68.5271; acc: 798153/804348=0.9923
     Instance: 46000; Time: 3.50s; loss: 97.8295; acc: 807064/813341=0.9923
     Instance: 46500; Time: 3.30s; loss: 74.5498; acc: 815049/821389=0.9923
     Instance: 46991; Time: 3.55s; loss: 71.8594; acc: 824470/830865=0.9923
Epoch: 61 training finished. Time: 321.37s, speed: 146.22st/s,  total loss: 7399.934005737305
totalloss: 7399.934005737305
Right token =  59630  All token =  61166  acc =  0.9748880096785796
Dev: time: 6.36s, speed: 486.38st/s; acc: 0.9749, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93700  All token =  95820  acc =  0.9778751826341057
Test: time: 9.83s, speed: 563.94st/s; acc: 0.9779, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 62/100
 Learning rate is set as: 0.003658536585365854
Shuffle: first input word list: [1365, 238, 115, 84, 21]
     Instance: 500; Time: 3.51s; loss: 107.0089; acc: 8522/8590=0.9921
     Instance: 1000; Time: 9236.14s; loss: 101.9697; acc: 17359/17487=0.9927
     Instance: 1500; Time: 3.46s; loss: 63.9081; acc: 26445/26635=0.9929
     Instance: 2000; Time: 3.34s; loss: 67.9844; acc: 34584/34816=0.9933
     Instance: 2500; Time: 3.33s; loss: 71.7928; acc: 42985/43280=0.9932
     Instance: 3000; Time: 3.82s; loss: 88.1224; acc: 52891/53253=0.9932
     Instance: 3500; Time: 3.98s; loss: 87.3102; acc: 62268/62706=0.9930
     Instance: 4000; Time: 3.67s; loss: 67.0410; acc: 71399/71890=0.9932
     Instance: 4500; Time: 3.72s; loss: 55.0688; acc: 80334/80876=0.9933
...
...
...
/home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages/torch/nn/_reduction.py:43: UserWarning: size_average and reduce args will be deprecated, please use reduction='sum' instead.
  warnings.warn(warning.format(ret))
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
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.89s; loss: 19156005918367067144192.0000; acc: 2789/8986=0.3104
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    0m19.880s
user    0m18.347s
sys     0m2.110s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

I got above error ...  
I have to update the config file.  
I changed the learning_rate as follows:  

```
###Hyperparameters###
cnn_layer=4
char_hidden_dim=50
hidden_dim=200
dropout=0.5
lstm_layer=1
bilstm=True
#learning_rate=0.015
#learning_rate=0.010
learning_rate=0.008
```

training again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ time python main.py --config ./mysent-para-config/word-cnn.char-cnn.
train.config | tee ./mysent-para-model/word-cnn.char-cnn.train.log3^C
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cd ..
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.char-cnn.train.config | tee 
./mysent-para-model/word-cnn.char-cnn.train.log3
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
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
     Hyper              lr: 0.008
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
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.008
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.87s; loss: 110083.1091; acc: 4527/8986=0.5038
     Instance: 1000; Time: 0.89s; loss: 13570.1252; acc: 10604/18422=0.5756
     Instance: 1500; Time: 0.86s; loss: 8334.3684; acc: 17147/27720=0.6186
     Instance: 2000; Time: 0.81s; loss: 7315.6183; acc: 23766/36837=0.6452
     Instance: 2500; Time: 0.83s; loss: 7082.4920; acc: 29777/45333=0.6569
     Instance: 3000; Time: 0.89s; loss: 7737.6215; acc: 36939/55086=0.6706
     Instance: 3500; Time: 0.82s; loss: 7105.4827; acc: 43431/64013=0.6785
     Instance: 4000; Time: 0.76s; loss: 6968.9652; acc: 49565/72548=0.6832
     Instance: 4500; Time: 0.79s; loss: 6971.4447; acc: 55932/81330=0.6877
     Instance: 5000; Time: 0.78s; loss: 7105.6136; acc: 62181/90054=0.6905
     Instance: 5500; Time: 0.85s; loss: 7154.5048; acc: 69021/99330=0.6949
     Instance: 6000; Time: 0.75s; loss: 6620.3812; acc: 74962/107637=0.6964
     Instance: 6500; Time: 0.91s; loss: 7821.4159; acc: 82143/117489=0.6992
     Instance: 7000; Time: 0.86s; loss: 7193.4735; acc: 88862/126691=0.7014
     Instance: 7500; Time: 0.74s; loss: 6331.7904; acc: 94506/134642=0.7019
     Instance: 8000; Time: 0.85s; loss: 7052.0173; acc: 100919/143526=0.7031
...
...
...
     Instance: 43500; Time: 0.86s; loss: 3837.8805; acc: 581991/768845=0.7570
     Instance: 44000; Time: 0.82s; loss: 3261.6421; acc: 589781/777474=0.7586
     Instance: 44500; Time: 0.94s; loss: 3375.3772; acc: 598126/786667=0.7603
     Instance: 45000; Time: 0.87s; loss: 3361.6613; acc: 606316/795694=0.7620
     Instance: 45500; Time: 0.80s; loss: 2425.5052; acc: 614465/804405=0.7639
     Instance: 46000; Time: 0.81s; loss: 3266.1919; acc: 622202/812921=0.7654
     Instance: 46500; Time: 0.88s; loss: 3104.7823; acc: 630540/821965=0.7671
     Instance: 46991; Time: 0.85s; loss: 8282603.4120; acc: 638630/830865=0.7686
Epoch: 0 training finished. Time: 78.25s, speed: 600.50st/s,  total loss: 8953630.858570099
totalloss: 8953630.858570099
Right token =  4119  All token =  61166  acc =  0.06734133342052774
Dev: time: 4.14s, speed: 748.35st/s; acc: 0.0673, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.0.model
Right token =  6760  All token =  95820  acc =  0.07054894594030474
Test: time: 6.48s, speed: 864.50st/s; acc: 0.0705, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 1/100
 Learning rate is set as: 0.007619047619047619
Shuffle: first input word list: [2020, 2395, 1947, 75, 14205, 287, 213, 211, 10]
     Instance: 500; Time: 0.85s; loss: 29253162709906552.0000; acc: 3689/8917=0.4137
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    1m51.686s
user    1m47.588s
sys     0m4.109s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

Got above error again ...  
I checked the previous experiment for sentence level config file and found as follows:  

```
###Hyperparameters###
cnn_layer=4
char_hidden_dim=50
hidden_dim=200
dropout=0.5
lstm_layer=1
bilstm=True
#learning_rate=0.015
learning_rate=0.010
lr_decay=0.05
momentum=0
l2=1e-8
gpu=True
#clip=
```

It looks at that time, 0.010 worked.  
I give 0.005 ...  

```
     Instance: 44000; Time: 0.80s; loss: 2484.2924; acc: 720218/777474=0.9264
     Instance: 44500; Time: 0.89s; loss: 2778.7358; acc: 728791/786667=0.9264
     Instance: 45000; Time: 0.84s; loss: 2804.0292; acc: 737187/795694=0.9265
     Instance: 45500; Time: 0.81s; loss: 2036.2368; acc: 745479/804405=0.9267
     Instance: 46000; Time: 0.78s; loss: 2882.3172; acc: 753330/812921=0.9267
     Instance: 46500; Time: 0.84s; loss: 2821.5394; acc: 761750/821965=0.9267
     Instance: 46991; Time: 0.81s; loss: 100558.7343; acc: 769895/830865=0.9266
Epoch: 0 training finished. Time: 77.10s, speed: 609.51st/s,  total loss: 365949.233530283
totalloss: 365949.233530283
Right token =  41293  All token =  61166  acc =  0.6750972762645915
Dev: time: 4.01s, speed: 774.83st/s; acc: 0.6751, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.0.model
Right token =  63320  All token =  95820  acc =  0.6608223752869965
Test: time: 6.25s, speed: 894.24st/s; acc: 0.6608, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 1/100
 Learning rate is set as: 0.0047619047619047615
Shuffle: first input word list: [2020, 2395, 1947, 75, 14205, 287, 213, 211, 10]
     Instance: 500; Time: 0.82s; loss: 247533202.2734; acc: 4427/8917=0.4965
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    1m49.922s
user    1m46.260s
sys     0m4.051s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

Not working and got same error as above ...  
I updated the learning rate as follows and train again:  
ဒီတစ်ခါတော့ အဆင်ပြေတဲ့ပုံရှိတယ်။   

```
learning_rate=0.0005      
lr_decay=0.05
```

train again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-cnn.char-cnn.train.config | te
e ./mysent-para-model/word-cnn.char-cnn.train.log5
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
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
     Hyper              lr: 0.0005
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
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: CNN ...
CNN layer:  4
Epoch: 0/100
 Learning rate is set as: 0.0005
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.90s; loss: 8585.3003; acc: 6063/8986=0.6747
     Instance: 1000; Time: 0.91s; loss: 5433.2205; acc: 13802/18422=0.7492
     Instance: 1500; Time: 0.88s; loss: 3905.7002; acc: 21966/27720=0.7924
     Instance: 2000; Time: 0.83s; loss: 3192.6864; acc: 30204/36837=0.8199
     Instance: 2500; Time: 0.84s; loss: 2521.7409; acc: 38044/45333=0.8392
     Instance: 3000; Time: 0.88s; loss: 2640.4239; acc: 47107/55086=0.8552
     Instance: 3500; Time: 0.81s; loss: 2564.5093; acc: 55393/64013=0.8653
     Instance: 4000; Time: 0.77s; loss: 1899.8711; acc: 63457/72548=0.8747
     Instance: 4500; Time: 0.83s; loss: 1977.8924; acc: 71727/81330=0.8819
     Instance: 5000; Time: 0.82s; loss: 2159.7114; acc: 79918/90054=0.8874
     Instance: 5500; Time: 0.87s; loss: 2007.2732; acc: 88696/99330=0.8929
     Instance: 6000; Time: 0.78s; loss: 1789.9100; acc: 96529/107637=0.8968
     Instance: 6500; Time: 0.92s; loss: 2759.7930; acc: 105616/117489=0.8989
     Instance: 7000; Time: 0.87s; loss: 1847.5619; acc: 114295/126691=0.9022
     Instance: 7500; Time: 0.75s; loss: 1504.0640; acc: 121845/134642=0.9050
     Instance: 8000; Time: 0.86s; loss: 1686.0040; acc: 130294/143526=0.9078
     Instance: 8500; Time: 0.93s; loss: 1643.8270; acc: 139499/153140=0.9109
     Instance: 9000; Time: 0.82s; loss: 2056.9370; acc: 147368/161594=0.9120
     Instance: 9500; Time: 0.83s; loss: 1880.4949; acc: 155669/170409=0.9135
     Instance: 10000; Time: 0.82s; loss: 1841.5256; acc: 163785/179025=0.9149
     Instance: 10500; Time: 0.86s; loss: 1467.9635; acc: 172366/188031=0.9167
     Instance: 11000; Time: 0.84s; loss: 1920.9328; acc: 180337/196518=0.9177
     Instance: 11500; Time: 0.81s; loss: 1672.3228; acc: 188661/205293=0.9190
     Instance: 12000; Time: 0.94s; loss: 1664.6814; acc: 197600/214657=0.9205
     Instance: 12500; Time: 0.84s; loss: 1469.9970; acc: 205645/223137=0.9216
     Instance: 13000; Time: 0.82s; loss: 1179.8665; acc: 214006/231856=0.9230
     Instance: 13500; Time: 0.82s; loss: 1921.6567; acc: 222762/241147=0.9238
...
...
...
     Instance: 46000; Time: 0.67s; loss: 1031.8306; acc: 783825/813061=0.9640
     Instance: 46500; Time: 0.73s; loss: 1231.3961; acc: 792565/822151=0.9640
     Instance: 46991; Time: 0.66s; loss: 728.5183; acc: 801055/830865=0.9641
Epoch: 1 training finished. Time: 76.96s, speed: 610.56st/s,  total loss: 102591.59290361404
totalloss: 102591.59290361404
Right token =  58823  All token =  61166  acc =  0.9616944053886146
Dev: time: 4.09s, speed: 758.10st/s; acc: 0.9617, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  92537  All token =  95820  acc =  0.9657378417866833
Test: time: 6.35s, speed: 875.24st/s; acc: 0.9657, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 2/100
 Learning rate is set as: 0.00045454545454545455
Shuffle: first input word list: [443, 136, 151, 3227, 64, 3228, 11, 3229, 2694, 39, 59, 43]
     Instance: 500; Time: 0.87s; loss: 923.8742; acc: 8761/9020=0.9713
     Instance: 1000; Time: 0.89s; loss: 1135.4343; acc: 18002/18585=0.9686
     Instance: 1500; Time: 0.75s; loss: 972.1685; acc: 25537/26418=0.9667
     Instance: 2000; Time: 0.82s; loss: 762.5909; acc: 34265/35385=0.9683
     Instance: 2500; Time: 0.80s; loss: 948.6560; acc: 42276/43710=0.9672
     Instance: 3000; Time: 0.79s; loss: 1126.8299; acc: 50649/52427=0.9661
     Instance: 3500; Time: 0.86s; loss: 1206.8917; acc: 58942/61041=0.9656
     Instance: 4000; Time: 0.72s; loss: 1132.6899; acc: 66433/68840=0.9650
     Instance: 4500; Time: 0.82s; loss: 905.0213; acc: 75142/77793=0.9659
     Instance: 5000; Time: 0.81s; loss: 1067.3792; acc: 84040/87026=0.9657
     Instance: 5500; Time: 0.79s; loss: 983.3950; acc: 92467/95765=0.9656
     Instance: 6000; Time: 0.83s; loss: 1043.0312; acc: 101121/104716=0.9657
     Instance: 6500; Time: 0.77s; loss: 1285.6504; acc: 109138/113127=0.9647
...
...
...
     Instance: 45000; Time: 0.89s; loss: 781.5592; acc: 771497/796203=0.9690
     Instance: 45500; Time: 0.84s; loss: 749.0727; acc: 780358/805287=0.9690
     Instance: 46000; Time: 0.73s; loss: 816.3146; acc: 787645/812805=0.9690
     Instance: 46500; Time: 0.89s; loss: 1106.3000; acc: 796910/822417=0.9690
     Instance: 46991; Time: 0.81s; loss: 795.8082; acc: 805124/830865=0.9690
Epoch: 3 training finished. Time: 76.31s, speed: 615.79st/s,  total loss: 86954.75834441185
totalloss: 86954.75834441185
Right token =  59104  All token =  61166  acc =  0.9662884609096557
Dev: time: 4.09s, speed: 758.40st/s; acc: 0.9663, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93312  All token =  95820  acc =  0.9738259236067627
Test: time: 6.37s, speed: 872.82st/s; acc: 0.9738, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 4/100
 Learning rate is set as: 0.0004166666666666667
Shuffle: first input word list: [3645, 339, 6, 1225, 62, 399, 26, 727, 6, 161, 62, 209]
     Instance: 500; Time: 0.80s; loss: 773.7539; acc: 8482/8724=0.9723
     Instance: 1000; Time: 0.78s; loss: 795.3751; acc: 16959/17406=0.9743
     Instance: 1500; Time: 0.86s; loss: 1064.4772; acc: 26023/26790=0.9714
     Instance: 2000; Time: 0.75s; loss: 879.4716; acc: 34287/35328=0.9705
     Instance: 2500; Time: 0.81s; loss: 1026.2727; acc: 43281/44602=0.9704
     Instance: 3000; Time: 0.80s; loss: 775.6900; acc: 51896/53462=0.9707
     Instance: 3500; Time: 0.82s; loss: 1121.2593; acc: 60266/62142=0.9698
     Instance: 4000; Time: 0.81s; loss: 913.8526; acc: 68475/70661=0.9691
     Instance: 4500; Time: 0.80s; loss: 847.8999; acc: 76854/79299=0.9692
     Instance: 5000; Time: 0.78s; loss: 881.7406; acc: 84485/87169=0.9692
...
...
...
     Instance: 41500; Time: 0.63s; loss: 553.3214; acc: 715881/736774=0.9716
     Instance: 42000; Time: 0.69s; loss: 813.2179; acc: 724808/745960=0.9716
     Instance: 42500; Time: 0.58s; loss: 670.4339; acc: 732688/754031=0.9717
     Instance: 43000; Time: 0.68s; loss: 1004.7039; acc: 741293/762949=0.9716
     Instance: 43500; Time: 0.64s; loss: 915.2277; acc: 749581/771485=0.9716
     Instance: 44000; Time: 0.68s; loss: 860.0994; acc: 757828/779999=0.9716
     Instance: 44500; Time: 0.65s; loss: 907.4215; acc: 766338/788792=0.9715
     Instance: 45000; Time: 0.66s; loss: 746.0545; acc: 774685/797341=0.9716
     Instance: 45500; Time: 0.64s; loss: 929.6202; acc: 782438/805408=0.9715
     Instance: 46000; Time: 0.68s; loss: 1010.8860; acc: 790429/813714=0.9714
     Instance: 46500; Time: 0.68s; loss: 686.8522; acc: 798840/822336=0.9714
     Instance: 46991; Time: 0.66s; loss: 682.4202; acc: 807164/830865=0.9715
Epoch: 6 training finished. Time: 74.12s, speed: 634.02st/s,  total loss: 78288.24773526192
totalloss: 78288.24773526192
Right token =  59309  All token =  61166  acc =  0.9696399960762515
Dev: time: 4.07s, speed: 761.54st/s; acc: 0.9696, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93416  All token =  95820  acc =  0.9749112920058443
Test: time: 6.32s, speed: 878.67st/s; acc: 0.9749, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 7/100
 Learning rate is set as: 0.00037037037037037035
Shuffle: first input word list: [372, 1100, 21]
     Instance: 500; Time: 0.66s; loss: 799.9260; acc: 8272/8541=0.9685
     Instance: 1000; Time: 0.71s; loss: 913.0689; acc: 16965/17484=0.9703
     Instance: 1500; Time: 0.69s; loss: 885.6762; acc: 26047/26826=0.9710
     Instance: 2000; Time: 0.63s; loss: 596.6385; acc: 34177/35131=0.9728
     Instance: 2500; Time: 0.69s; loss: 769.2017; acc: 42765/43958=0.9729
     Instance: 3000; Time: 0.67s; loss: 731.2803; acc: 51466/52921=0.9725
     Instance: 3500; Time: 0.64s; loss: 783.3775; acc: 59522/61225=0.9722
     Instance: 4000; Time: 0.68s; loss: 627.9854; acc: 67796/69694=0.9728
...
...
...
     Instance: 45000; Time: 0.72s; loss: 715.1859; acc: 778135/796011=0.9775
     Instance: 45500; Time: 0.66s; loss: 560.1591; acc: 786084/804133=0.9776
     Instance: 46000; Time: 0.73s; loss: 810.0012; acc: 794840/813116=0.9775
     Instance: 46500; Time: 0.74s; loss: 605.6596; acc: 803959/822432=0.9775
     Instance: 46991; Time: 0.68s; loss: 552.1006; acc: 812204/830865=0.9775
Epoch: 41 training finished. Time: 67.26s, speed: 698.67st/s,  total loss: 58832.85360765457
totalloss: 58832.85360765457
Right token =  59611  All token =  61166  acc =  0.9745773795899683
Dev: time: 4.08s, speed: 759.82st/s; acc: 0.9746, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93679  All token =  95820  acc =  0.977656021707368
Test: time: 6.33s, speed: 878.28st/s; acc: 0.9777, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 42/100
 Learning rate is set as: 0.00016129032258064516
Shuffle: first input word list: [1089, 64, 316, 5007, 12283, 84, 10, 2307, 76, 84, 485, 18878, 6, 22, 68, 17]
     Instance: 500; Time: 0.74s; loss: 762.5111; acc: 9004/9220=0.9766
     Instance: 1000; Time: 0.83s; loss: 685.9506; acc: 17367/17813=0.9750
     Instance: 1500; Time: 0.86s; loss: 537.6221; acc: 26471/27110=0.9764
     Instance: 2000; Time: 0.73s; loss: 622.5618; acc: 34318/35145=0.9765
     Instance: 2500; Time: 0.86s; loss: 901.9333; acc: 43312/44435=0.9747
     Instance: 3000; Time: 0.81s; loss: 565.5090; acc: 51908/53204=0.9756
     Instance: 3500; Time: 0.86s; loss: 736.4798; acc: 60830/62368=0.9753
     Instance: 4000; Time: 0.81s; loss: 560.0787; acc: 69515/71254=0.9756
     Instance: 4500; Time: 0.82s; loss: 531.4246; acc: 77989/79903=0.9760
...
...
...
     Instance: 40500; Time: 0.69s; loss: 568.8948; acc: 703445/718285=0.9793
     Instance: 41000; Time: 0.72s; loss: 591.8758; acc: 712463/727520=0.9793
     Instance: 41500; Time: 0.62s; loss: 471.7119; acc: 720581/735825=0.9793
     Instance: 42000; Time: 0.69s; loss: 710.2314; acc: 728990/744427=0.9793
     Instance: 42500; Time: 0.63s; loss: 432.1841; acc: 737231/752805=0.9793
     Instance: 43000; Time: 0.65s; loss: 406.7828; acc: 745271/760965=0.9794
     Instance: 43500; Time: 0.64s; loss: 644.3992; acc: 753552/769437=0.9794
     Instance: 44000; Time: 0.66s; loss: 628.9831; acc: 761828/777918=0.9793
     Instance: 44500; Time: 0.71s; loss: 517.1820; acc: 770522/786757=0.9794
     Instance: 45000; Time: 0.69s; loss: 463.8569; acc: 778987/795394=0.9794
     Instance: 45500; Time: 0.65s; loss: 651.3430; acc: 787738/804350=0.9793
     Instance: 46000; Time: 0.65s; loss: 379.9577; acc: 795946/812683=0.9794
     Instance: 46500; Time: 0.67s; loss: 619.7938; acc: 804725/821639=0.9794
     Instance: 46991; Time: 0.72s; loss: 505.1375; acc: 813771/830865=0.9794
Epoch: 76 training finished. Time: 68.99s, speed: 681.10st/s,  total loss: 52599.99955892563
totalloss: 52599.99955892563
Right token =  59654  All token =  61166  acc =  0.9752803845273518
Dev: time: 4.09s, speed: 758.46st/s; acc: 0.9753, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93811  All token =  95820  acc =  0.9790336046754331
Test: time: 6.35s, speed: 875.35st/s; acc: 0.9790, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 77/100
 Learning rate is set as: 0.00010309278350515464
Shuffle: first input word list: [135, 114, 337, 1053, 84, 185, 39, 17]
     Instance: 500; Time: 0.67s; loss: 582.4746; acc: 8139/8329=0.9772
     Instance: 1000; Time: 0.75s; loss: 615.5011; acc: 17131/17486=0.9797
     Instance: 1500; Time: 0.68s; loss: 382.8663; acc: 25547/26024=0.9817
     Instance: 2000; Time: 0.65s; loss: 548.7620; acc: 33441/34122=0.9800
     Instance: 2500; Time: 0.73s; loss: 644.3307; acc: 42456/43361=0.9791
     Instance: 3000; Time: 0.65s; loss: 496.6392; acc: 50581/51629=0.9797
     Instance: 3500; Time: 0.71s; loss: 560.3969; acc: 58843/60087=0.9793
...
...
...
     Instance: 37000; Time: 0.88s; loss: 555.5913; acc: 638599/651553=0.9801
     Instance: 37500; Time: 0.92s; loss: 539.1188; acc: 648155/661280=0.9802
     Instance: 38000; Time: 0.80s; loss: 584.2119; acc: 656871/670190=0.9801
     Instance: 38500; Time: 0.87s; loss: 571.6658; acc: 666030/679528=0.9801
     Instance: 39000; Time: 0.83s; loss: 363.8419; acc: 674812/688416=0.9802
     Instance: 39500; Time: 0.85s; loss: 532.6723; acc: 683737/697512=0.9803
     Instance: 40000; Time: 0.77s; loss: 545.8867; acc: 691636/705583=0.9802
     Instance: 40500; Time: 0.78s; loss: 540.1772; acc: 699775/713889=0.9802
     Instance: 41000; Time: 0.92s; loss: 554.2299; acc: 709658/723934=0.9803
     Instance: 41500; Time: 0.83s; loss: 468.3346; acc: 718059/732499=0.9803
     Instance: 42000; Time: 0.82s; loss: 590.5979; acc: 726578/741220=0.9802
     Instance: 42500; Time: 0.84s; loss: 603.6258; acc: 735701/750561=0.9802
     Instance: 43000; Time: 0.79s; loss: 397.8979; acc: 744190/759167=0.9803
     Instance: 43500; Time: 0.80s; loss: 586.1005; acc: 752395/767562=0.9802
     Instance: 44000; Time: 0.84s; loss: 725.6683; acc: 761129/776526=0.9802
     Instance: 44500; Time: 0.80s; loss: 457.5099; acc: 769735/785275=0.9802
     Instance: 45000; Time: 0.85s; loss: 452.8880; acc: 778407/794097=0.9802
     Instance: 45500; Time: 0.79s; loss: 442.2041; acc: 786774/802609=0.9803
     Instance: 46000; Time: 0.93s; loss: 557.3239; acc: 796121/812146=0.9803
     Instance: 46500; Time: 0.87s; loss: 655.0185; acc: 805091/821309=0.9803
     Instance: 46991; Time: 0.91s; loss: 493.0488; acc: 814474/830865=0.9803
Epoch: 99 training finished. Time: 78.35s, speed: 599.78st/s,  total loss: 50117.29450893402
totalloss: 50117.29450893402
Right token =  59645  All token =  61166  acc =  0.9751332439590622
Dev: time: 4.09s, speed: 759.07st/s; acc: 0.9751, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93853  All token =  95820  acc =  0.9794719265289084
Test: time: 6.37s, speed: 873.11st/s; acc: 0.9795, p: -1.0000, r: -1.0000, f: -1.0000

real    141m39.777s
user    141m30.291s
sys     0m18.204s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the output model:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-model$ ls -lh *.model
-rw-r--r-- 1 yekyaw.thu domain users  11M Mar  6 08:20 wordcnn-charcnn.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.2M Feb 23 07:49 wordlstm-charcnn.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.3M Mar  3 10:55 wordlstm-charlstm.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.2M Mar  3 18:03 wordlstm-crf-charcnn.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.3M Mar  5 00:17 wordlstm-crf-charlstm.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.0M Mar  5 10:44 wordlstm-crf-nochar.0.model
-rw-r--r-- 1 yekyaw.thu domain users 9.0M Mar  3 14:51 wordlstm-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-model$ 
```

updated decode/test config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.char-cnn.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

testing/decoding ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.char-cnn.decode.config | tee
 ./mysent-para-hyp/word-cnn.char-cnn.decode.log
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
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charcnn.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
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
     Hyper              lr: 0.0005
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
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
Right token =  92818  All token =  95820  acc =  0.968670423711125
raw: time:6.15s, speed:904.13st/s; acc: 0.9687, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charcnn.hyp

real    0m16.393s
user    0m13.968s
sys     0m2.120s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

check the hyp files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head wordcnn-charcnn.hyp 
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ tail ./wordcnn-charcnn.hyp 
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

check filesize, wc of hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ ls -lh *.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  6 10:52 wordcnn-charcnn.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  3 10:44 wordlstm-charcnn.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  3 14:41 wordlstm-charlstm.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  5 00:01 wordlstm-crf-charcnn.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  5 13:21 wordlstm-crf-charlstm.hyp
-rw-r--r-- 1 yekyaw.thu domain users 1.5M Mar  3 17:40 wordlstm-nochar.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ wc *.hyp
 101330  191640 1565878 wordcnn-charcnn.hyp
 101330  191640 1565878 wordlstm-charcnn.hyp
 101330  191640 1565878 wordlstm-charlstm.hyp
 101330  191640 1565878 wordlstm-crf-charcnn.hyp
 101330  191640 1565878 wordlstm-crf-charlstm.hyp
 101330  191640 1565878 wordlstm-nochar.hyp
 607980 1149840 9395268 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

## 8. Word-CNN, Char-LSTM

updated the training config file for running with paragraph level data:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.char-lstm.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm
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
#learning_rate=0.015
learning_rate=0.010
lr_decay=0.05
momentum=0
l2=1e-8
gpu=True
#clip=
```

start training ...  

```
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
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 1.09s; loss: 41064165519.5750; acc: 3007/8986=0.3346
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    0m21.253s
user    0m18.418s
sys     0m3.792s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

I have to update the learning rate ...

```
learning_rate=0.0005
```

train again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-cnn.char-lstm.train.config | tee ./mysent-para-model/word-cnn.char-lstm.train.log2
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm
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
     Hyper              lr: 0.0005
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
 Learning rate is set as: 0.0005
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 1.10s; loss: 8359.9939; acc: 6140/8986=0.6833
     Instance: 1000; Time: 1.10s; loss: 5290.0962; acc: 13991/18422=0.7595
     Instance: 1500; Time: 1.11s; loss: 3839.5685; acc: 22234/27720=0.8021
     Instance: 2000; Time: 1.02s; loss: 3103.4275; acc: 30535/36837=0.8289
     Instance: 2500; Time: 1.04s; loss: 2416.7022; acc: 38426/45333=0.8476
     Instance: 3000; Time: 1.09s; loss: 2642.9386; acc: 47521/55086=0.8627
     Instance: 3500; Time: 1.03s; loss: 2547.2129; acc: 55843/64013=0.8724
     Instance: 4000; Time: 0.97s; loss: 1911.9936; acc: 63887/72548=0.8806
     Instance: 4500; Time: 1.01s; loss: 1890.4043; acc: 72177/81330=0.8875
     Instance: 5000; Time: 1.01s; loss: 2132.9553; acc: 80402/90054=0.8928
     Instance: 5500; Time: 1.06s; loss: 2107.1703; acc: 89151/99330=0.8975
     Instance: 6000; Time: 0.96s; loss: 1815.8733; acc: 96975/107637=0.9009
     Instance: 6500; Time: 1.12s; loss: 2747.2214; acc: 106109/117489=0.9031
     Instance: 7000; Time: 1.07s; loss: 1913.5415; acc: 114822/126691=0.9063
     Instance: 7500; Time: 0.94s; loss: 1535.2501; acc: 122375/134642=0.9089
     Instance: 8000; Time: 1.04s; loss: 1610.9017; acc: 130859/143526=0.9117
     Instance: 8500; Time: 1.15s; loss: 1689.1319; acc: 140052/153140=0.9145
     Instance: 9000; Time: 1.00s; loss: 2035.0876; acc: 147960/161594=0.9156
     Instance: 9500; Time: 1.02s; loss: 1944.8737; acc: 156264/170409=0.9170
     Instance: 10000; Time: 1.01s; loss: 1866.2145; acc: 164358/179025=0.9181
     Instance: 10500; Time: 1.08s; loss: 1475.1766; acc: 172948/188031=0.9198
     Instance: 11000; Time: 1.02s; loss: 1974.5388; acc: 180918/196518=0.9206
     Instance: 11500; Time: 1.00s; loss: 1653.3219; acc: 189247/205293=0.9218
     Instance: 12000; Time: 1.12s; loss: 1673.6396; acc: 198178/214657=0.9232
     Instance: 12500; Time: 1.04s; loss: 1522.6759; acc: 206220/223137=0.9242
     Instance: 13000; Time: 1.01s; loss: 1267.1788; acc: 214548/231856=0.9254
     Instance: 13500; Time: 1.05s; loss: 1961.0633; acc: 223306/241147=0.9260
...
...
...
     Instance: 44500; Time: 0.99s; loss: 537.8339; acc: 766762/788427=0.9725
     Instance: 45000; Time: 0.99s; loss: 683.5047; acc: 774622/796491=0.9725
     Instance: 45500; Time: 0.97s; loss: 683.5277; acc: 782338/804453=0.9725
     Instance: 46000; Time: 1.06s; loss: 763.5732; acc: 791595/813941=0.9725
     Instance: 46500; Time: 0.99s; loss: 557.4799; acc: 799681/822194=0.9726
     Instance: 46991; Time: 1.07s; loss: 600.2484; acc: 808163/830865=0.9727
Epoch: 8 training finished. Time: 96.61s, speed: 486.41st/s,  total loss: 74858.32611203194
totalloss: 74858.32611203194
Right token =  59433  All token =  61166  acc =  0.9716672661282412
Dev: time: 4.74s, speed: 654.08st/s; acc: 0.9717, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93546  All token =  95820  acc =  0.9762680025046963
Test: time: 7.39s, speed: 750.94st/s; acc: 0.9763, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 9/100
 Learning rate is set as: 0.0003448275862068966
Shuffle: first input word list: [26759, 64, 16, 75, 211, 216, 3, 379]
     Instance: 500; Time: 1.10s; loss: 780.7376; acc: 9319/9565=0.9743
     Instance: 1000; Time: 0.99s; loss: 837.7561; acc: 17248/17754=0.9715
     Instance: 1500; Time: 1.04s; loss: 918.4032; acc: 25595/26358=0.9711
     Instance: 2000; Time: 1.02s; loss: 823.9095; acc: 33648/34664=0.9707
     Instance: 2500; Time: 0.95s; loss: 631.6493; acc: 41585/42801=0.9716
     Instance: 3000; Time: 1.07s; loss: 946.8949; acc: 50209/51706=0.9710
     Instance: 3500; Time: 0.99s; loss: 632.8338; acc: 58333/60039=0.9716
     Instance: 4000; Time: 1.03s; loss: 724.4812; acc: 67014/68925=0.9723
     Instance: 4500; Time: 1.11s; loss: 733.4030; acc: 76355/78485=0.9729
     Instance: 5000; Time: 1.00s; loss: 815.9153; acc: 84469/86855=0.9725
     Instance: 5500; Time: 1.08s; loss: 680.2522; acc: 93418/96012=0.9730
     Instance: 6000; Time: 1.17s; loss: 668.0188; acc: 102797/105598=0.9735
...
...
...
     Instance: 45000; Time: 1.14s; loss: 628.7539; acc: 776653/796093=0.9756
     Instance: 45500; Time: 1.05s; loss: 724.9332; acc: 785122/804787=0.9756
     Instance: 46000; Time: 0.97s; loss: 544.0354; acc: 793148/813016=0.9756
     Instance: 46500; Time: 1.01s; loss: 715.1054; acc: 801643/821740=0.9755
     Instance: 46991; Time: 1.04s; loss: 587.9432; acc: 810561/830865=0.9756
Epoch: 20 training finished. Time: 98.34s, speed: 477.84st/s,  total loss: 65330.623722076416
totalloss: 65330.623722076416
Right token =  59516  All token =  61166  acc =  0.9730242291469117
Dev: time: 4.77s, speed: 650.27st/s; acc: 0.9730, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93684  All token =  95820  acc =  0.9777082028804007
Test: time: 7.43s, speed: 746.73st/s; acc: 0.9777, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 21/100
 Learning rate is set as: 0.00024390243902439027
Shuffle: first input word list: [271, 355, 356, 11, 7, 56, 2279, 76, 11, 7, 84, 866, 50, 8986, 7, 55, 62, 7625, 3522, 136, 151
, 1218, 991, 6843, 192, 192, 5323, 606, 33, 10542, 7, 233, 109, 39, 47, 43, 56, 22, 325, 43]
     Instance: 500; Time: 1.08s; loss: 694.5383; acc: 8942/9153=0.9769
     Instance: 1000; Time: 1.06s; loss: 651.2477; acc: 17813/18221=0.9776
     Instance: 1500; Time: 0.98s; loss: 645.1052; acc: 26171/26796=0.9767
     Instance: 2000; Time: 1.01s; loss: 728.0793; acc: 34687/35541=0.9760
     Instance: 2500; Time: 1.00s; loss: 789.1890; acc: 43198/44313=0.9748
     Instance: 3000; Time: 1.04s; loss: 642.9028; acc: 51960/53279=0.9752
     Instance: 3500; Time: 1.07s; loss: 575.8320; acc: 60999/62516=0.9757
     Instance: 4000; Time: 1.02s; loss: 711.8530; acc: 69953/71678=0.9759
     Instance: 4500; Time: 1.10s; loss: 650.9657; acc: 79618/81552=0.9763
...
...
...
     Instance: 36000; Time: 1.04s; loss: 624.3588; acc: 620845/633543=0.9800
     Instance: 36500; Time: 0.99s; loss: 680.1621; acc: 629284/642188=0.9799
     Instance: 37000; Time: 1.10s; loss: 541.4936; acc: 638444/651553=0.9799
     Instance: 37500; Time: 1.13s; loss: 585.7429; acc: 647963/661280=0.9799
     Instance: 38000; Time: 1.02s; loss: 624.0655; acc: 656673/670190=0.9798
     Instance: 38500; Time: 1.08s; loss: 650.8090; acc: 665812/679528=0.9798
     Instance: 39000; Time: 1.03s; loss: 401.2834; acc: 674580/688416=0.9799
     Instance: 39500; Time: 1.06s; loss: 518.2868; acc: 683502/697512=0.9799
     Instance: 40000; Time: 0.96s; loss: 572.0539; acc: 691395/705583=0.9799
     Instance: 40500; Time: 1.01s; loss: 576.5778; acc: 699529/713889=0.9799
     Instance: 41000; Time: 1.14s; loss: 542.1192; acc: 709396/723934=0.9799
     Instance: 41500; Time: 1.03s; loss: 467.8854; acc: 717813/732499=0.9800
     Instance: 42000; Time: 1.04s; loss: 569.9144; acc: 726351/741220=0.9799
     Instance: 42500; Time: 1.06s; loss: 577.7256; acc: 735497/750561=0.9799
     Instance: 43000; Time: 1.01s; loss: 410.6599; acc: 743982/759167=0.9800
     Instance: 43500; Time: 1.02s; loss: 573.7857; acc: 752172/767562=0.9799
     Instance: 44000; Time: 1.08s; loss: 718.3493; acc: 760888/776526=0.9799
     Instance: 44500; Time: 1.01s; loss: 422.8844; acc: 769510/785275=0.9799
     Instance: 45000; Time: 1.07s; loss: 409.3544; acc: 778189/794097=0.9800
     Instance: 45500; Time: 1.00s; loss: 476.0115; acc: 786540/802609=0.9800
     Instance: 46000; Time: 1.14s; loss: 582.6927; acc: 795877/812146=0.9800
     Instance: 46500; Time: 1.10s; loss: 618.9162; acc: 804851/821309=0.9800
     Instance: 46991; Time: 1.14s; loss: 501.7796; acc: 814235/830865=0.9800
Epoch: 99 training finished. Time: 97.77s, speed: 480.64st/s,  total loss: 50218.95497465134
totalloss: 50218.95497465134
Right token =  59649  All token =  61166  acc =  0.9751986397671909
Dev: time: 4.73s, speed: 654.84st/s; acc: 0.9752, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93830  All token =  95820  acc =  0.9792318931329577
Test: time: 7.38s, speed: 752.03st/s; acc: 0.9792, p: -1.0000, r: -1.0000, f: -1.0000

real    183m54.568s
user    183m14.152s
sys     0m35.895s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

I update the decode/testing config file as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.char-lstm.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charlstm.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

decoding/testing as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-cnn.char-lstm.decode.config | 
tee ./mysent-para-hyp/word-cnn.char-lstm.decode.log
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
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charlstm.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
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
     Hyper              lr: 0.0005
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm
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
Right token =  92329  All token =  95820  acc =  0.9635671049885202
raw: time:7.46s, speed:743.86st/s; acc: 0.9636, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-charlstm.hyp

real    0m17.754s
user    0m15.300s
sys     0m3.586s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
```

check the hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head ./wordcnn-charlstm.hyp 
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ tail ./wordcnn-charlstm.hyp 
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

check the hyp filesize:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ wc *.hyp
  101330   191640  1565878 wordcnn-charcnn.hyp
  101330   191640  1565878 wordcnn-charlstm.hyp
  101330   191640  1565878 wordlstm-charcnn.hyp
  101330   191640  1565878 wordlstm-charlstm.hyp
  101330   191640  1565878 wordlstm-crf-charcnn.hyp
  101330   191640  1565878 wordlstm-crf-charlstm.hyp
  101330   191640  1565878 wordlstm-nochar.hyp
  709310  1341480 10961146 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

## 9. Word-CNN, No-Char

I update the training config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.no-char.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar
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
#learning_rate=0.015
learning_rate=0.010
lr_decay=0.05
momentum=0
l2=1e-8
gpu=True
#clip=
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

start training ...  

```
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
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.71s; loss: 656385915052.5908; acc: 2520/8986=0.2804
ERROR: LOSS EXPLOSION (>1e8) ! PLEASE SET PROPER PARAMETERS AND STRUCTURE! EXIT....

real    0m20.759s
user    0m18.020s
sys     0m3.798s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.no-char.train.config | tee ./mysent-para-model/word-cnn.no-char.train.log
```

Got error as shown in above. And thus, I need to change the learning rate ...  

```
learning_rate=0.0005
lr_decay=0.05
```

training again ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.no-char.train.config | tee .
/mysent-para-model/word-cnn.no-char.train.log
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar
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
     Model word extractor: CNN
     Model       use_char: False
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 100
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.0005
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
 Learning rate is set as: 0.0005
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 0.74s; loss: 8415.4459; acc: 6152/8986=0.6846
     Instance: 1000; Time: 0.75s; loss: 5220.4668; acc: 13994/18422=0.7596
     Instance: 1500; Time: 0.75s; loss: 3654.4554; acc: 22273/27720=0.8035
     Instance: 2000; Time: 0.69s; loss: 3055.3731; acc: 30557/36837=0.8295
     Instance: 2500; Time: 0.70s; loss: 2452.2483; acc: 38362/45333=0.8462
     Instance: 3000; Time: 0.78s; loss: 2606.1247; acc: 47432/55086=0.8611
     Instance: 3500; Time: 0.68s; loss: 2649.6013; acc: 55725/64013=0.8705
     Instance: 4000; Time: 0.67s; loss: 2008.9421; acc: 63762/72548=0.8789
     Instance: 4500; Time: 0.67s; loss: 1935.9616; acc: 72050/81330=0.8859
     Instance: 5000; Time: 0.68s; loss: 2228.8663; acc: 80219/90054=0.8908
     Instance: 5500; Time: 0.73s; loss: 2009.8109; acc: 88988/99330=0.8959
     Instance: 6000; Time: 0.64s; loss: 1745.1964; acc: 96836/107637=0.8997
     Instance: 6500; Time: 0.75s; loss: 2729.7877; acc: 105953/117489=0.9018
     Instance: 7000; Time: 0.75s; loss: 1850.3731; acc: 114698/126691=0.9053
     Instance: 7500; Time: 0.62s; loss: 1593.5917; acc: 122259/134642=0.9080
     Instance: 8000; Time: 0.71s; loss: 1631.2833; acc: 130720/143526=0.9108
     Instance: 8500; Time: 0.77s; loss: 1471.3181; acc: 139929/153140=0.9137
     Instance: 9000; Time: 0.67s; loss: 1983.9170; acc: 147833/161594=0.9148
     Instance: 9500; Time: 0.69s; loss: 1864.7781; acc: 156149/170409=0.9163
     Instance: 10000; Time: 0.70s; loss: 1834.8485; acc: 164264/179025=0.9175
     Instance: 10500; Time: 0.72s; loss: 1650.4748; acc: 172808/188031=0.9190
     Instance: 11000; Time: 0.71s; loss: 1820.5590; acc: 180806/196518=0.9200
     Instance: 11500; Time: 0.69s; loss: 1718.5017; acc: 189119/205293=0.9212
     Instance: 12000; Time: 0.75s; loss: 1652.9689; acc: 198069/214657=0.9227
     Instance: 12500; Time: 0.57s; loss: 1487.9664; acc: 206154/223137=0.9239
     Instance: 13000; Time: 0.56s; loss: 1187.4217; acc: 214523/231856=0.9252
     Instance: 13500; Time: 0.58s; loss: 1854.8844; acc: 223315/241147=0.9261
     Instance: 14000; Time: 0.53s; loss: 1501.8138; acc: 231125/249342=0.9269
...
...
...
     Instance: 45000; Time: 0.61s; loss: 1198.6172; acc: 767449/794362=0.9661
     Instance: 45500; Time: 0.67s; loss: 751.3657; acc: 776289/803447=0.9662
     Instance: 46000; Time: 0.68s; loss: 1106.1418; acc: 784894/812393=0.9662
     Instance: 46500; Time: 0.70s; loss: 1068.3737; acc: 793684/821489=0.9662
     Instance: 46991; Time: 0.71s; loss: 1030.5005; acc: 802780/830865=0.9662
Epoch: 2 training finished. Time: 63.03s, speed: 745.49st/s,  total loss: 95880.75673890114
totalloss: 95880.75673890114
Right token =  59031  All token =  61166  acc =  0.965094987411307
Dev: time: 3.98s, speed: 778.96st/s; acc: 0.9651, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93212  All token =  95820  acc =  0.9727823001461073
Test: time: 6.17s, speed: 900.71st/s; acc: 0.9728, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 3/100
 Learning rate is set as: 0.0004347826086956522
Shuffle: first input word list: [13261, 7650, 103, 26, 5730, 6, 13262, 4812, 16, 17]
     Instance: 500; Time: 0.74s; loss: 1099.9879; acc: 8507/8837=0.9627
     Instance: 1000; Time: 0.68s; loss: 829.5015; acc: 17214/17797=0.9672
     Instance: 1500; Time: 0.56s; loss: 911.0848; acc: 25955/26785=0.9690
     Instance: 2000; Time: 0.55s; loss: 1095.4788; acc: 34003/35154=0.9673
     Instance: 2500; Time: 0.62s; loss: 931.3814; acc: 43359/44793=0.9680
...
...
...
     Instance: 42500; Time: 0.58s; loss: 848.4536; acc: 732505/753364=0.9723
     Instance: 43000; Time: 0.61s; loss: 915.7798; acc: 741605/762712=0.9723
     Instance: 43500; Time: 0.53s; loss: 617.4366; acc: 749582/770887=0.9724
     Instance: 44000; Time: 0.61s; loss: 940.1630; acc: 758326/779916=0.9723
     Instance: 44500; Time: 0.54s; loss: 570.5586; acc: 766646/788427=0.9724
     Instance: 45000; Time: 0.53s; loss: 689.8203; acc: 774527/796491=0.9724
     Instance: 45500; Time: 0.53s; loss: 699.1299; acc: 782245/804453=0.9724
     Instance: 46000; Time: 0.60s; loss: 746.4920; acc: 791481/813941=0.9724
     Instance: 46500; Time: 0.55s; loss: 575.7472; acc: 799545/822194=0.9725
     Instance: 46991; Time: 0.59s; loss: 563.0955; acc: 808047/830865=0.9725
Epoch: 8 training finished. Time: 57.10s, speed: 823.00st/s,  total loss: 75998.797488451
totalloss: 75998.797488451
Right token =  59411  All token =  61166  acc =  0.9713075891835333
Dev: time: 4.01s, speed: 772.92st/s; acc: 0.9713, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93498  All token =  95820  acc =  0.9757670632435818
Test: time: 6.22s, speed: 893.93st/s; acc: 0.9758, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 9/100
 Learning rate is set as: 0.0003448275862068966
Shuffle: first input word list: [26759, 64, 16, 75, 211, 216, 3, 379]
     Instance: 500; Time: 0.63s; loss: 815.1136; acc: 9337/9565=0.9762
     Instance: 1000; Time: 0.53s; loss: 876.5737; acc: 17246/17754=0.9714
     Instance: 1500; Time: 0.57s; loss: 858.3005; acc: 25608/26358=0.9715
...
...
...
     Instance: 45000; Time: 0.69s; loss: 616.7257; acc: 775930/795780=0.9751
     Instance: 45500; Time: 0.68s; loss: 903.5691; acc: 784470/804590=0.9750
     Instance: 46000; Time: 0.67s; loss: 828.5598; acc: 792823/813209=0.9749
     Instance: 46500; Time: 0.74s; loss: 769.4925; acc: 801834/822463=0.9749
     Instance: 46991; Time: 0.69s; loss: 721.5108; acc: 810022/830865=0.9749
Epoch: 18 training finished. Time: 63.15s, speed: 744.06st/s,  total loss: 66998.49112558365
totalloss: 66998.49112558365
Right token =  59515  All token =  61166  acc =  0.9730078801948795
Dev: time: 4.02s, speed: 771.57st/s; acc: 0.9730, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93678  All token =  95820  acc =  0.9776455854727615
Test: time: 6.23s, speed: 892.15st/s; acc: 0.9776, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 19/100
 Learning rate is set as: 0.0002564102564102564
Shuffle: first input word list: [2701, 84, 696, 6, 4264, 68, 26, 239, 526, 6, 19303, 64, 252, 1401, 227, 19304, 700, 44, 531, 
55, 19305, 16612, 2383, 62, 525, 1492, 68, 17]
     Instance: 500; Time: 0.75s; loss: 668.2180; acc: 8671/8889=0.9755
     Instance: 1000; Time: 0.69s; loss: 556.3098; acc: 16971/17369=0.9771
     Instance: 1500; Time: 0.71s; loss: 690.5915; acc: 25508/26104=0.9772
     Instance: 2000; Time: 0.70s; loss: 672.8671; acc: 34372/35170=0.9773
     Instance: 2500; Time: 0.76s; loss: 815.2938; acc: 43493/44490=0.9776
     Instance: 3000; Time: 0.69s; loss: 600.0155; acc: 51775/52957=0.9777
     Instance: 3500; Time: 0.73s; loss: 706.6709; acc: 60362/61779=0.9771
...
...
...
     Instance: 36000; Time: 0.58s; loss: 607.9513; acc: 621007/633543=0.9802
     Instance: 36500; Time: 0.53s; loss: 647.0824; acc: 629470/642188=0.9802
     Instance: 37000; Time: 0.62s; loss: 589.2231; acc: 638640/651553=0.9802
     Instance: 37500; Time: 0.64s; loss: 619.2996; acc: 648186/661280=0.9802
     Instance: 38000; Time: 0.56s; loss: 660.7468; acc: 656872/670190=0.9801
     Instance: 38500; Time: 0.61s; loss: 664.4786; acc: 666014/679528=0.9801
     Instance: 39000; Time: 0.56s; loss: 380.5135; acc: 674781/688416=0.9802
     Instance: 39500; Time: 0.59s; loss: 510.2928; acc: 683704/697512=0.9802
     Instance: 40000; Time: 0.51s; loss: 518.0878; acc: 691600/705583=0.9802
     Instance: 40500; Time: 0.55s; loss: 520.8861; acc: 699744/713889=0.9802
     Instance: 41000; Time: 0.64s; loss: 567.6292; acc: 709612/723934=0.9802
     Instance: 41500; Time: 0.57s; loss: 438.1961; acc: 718029/732499=0.9802
     Instance: 42000; Time: 0.58s; loss: 579.3417; acc: 726574/741220=0.9802
     Instance: 42500; Time: 0.58s; loss: 494.4875; acc: 735735/750561=0.9802
     Instance: 43000; Time: 0.55s; loss: 427.8789; acc: 744218/759167=0.9803
     Instance: 43500; Time: 0.60s; loss: 525.4481; acc: 752420/767562=0.9803
     Instance: 44000; Time: 0.68s; loss: 678.3970; acc: 761161/776526=0.9802
     Instance: 44500; Time: 0.67s; loss: 378.2953; acc: 769762/785275=0.9802
     Instance: 45000; Time: 0.73s; loss: 380.9596; acc: 778447/794097=0.9803
     Instance: 45500; Time: 0.65s; loss: 479.5132; acc: 786789/802609=0.9803
     Instance: 46000; Time: 0.81s; loss: 526.2376; acc: 796155/812146=0.9803
     Instance: 46500; Time: 0.75s; loss: 659.6373; acc: 805091/821309=0.9803
     Instance: 46991; Time: 0.78s; loss: 523.2467; acc: 814470/830865=0.9803
Epoch: 99 training finished. Time: 62.05s, speed: 757.32st/s,  total loss: 50395.268538713455
totalloss: 50395.268538713455
Right token =  59604  All token =  61166  acc =  0.974462936925743
Dev: time: 3.98s, speed: 778.85st/s; acc: 0.9745, p: -1.0000, r: -1.0000, f: -1.0000
Right token =  93805  All token =  95820  acc =  0.9789709872677937
Test: time: 6.18s, speed: 900.21st/s; acc: 0.9790, p: -1.0000, r: -1.0000, f: -1.0000

real    153m53.778s
user    123m5.620s
sys     0m17.316s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

GPU usage while training time is as follows:  

```
(base) yekyaw.thu@gpu:~$ nvidia-smi
Mon Mar  6 22:15:34 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 47%   52C    P2    63W / 300W |    944MiB / 11019MiB |     15%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   56C    P8    21W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 31%   42C    P8    28W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   1768685      C   python                            941MiB |
+-----------------------------------------------------------------------------+
(base) yekyaw.thu@gpu:~$
```

I also updated the decode config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.no-char.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-nochar.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

decoding/testing ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python main.py --config ./mysent-para-config/word-cnn.no-char.decode.config | tee 
./mysent-para-hyp/word-cnn.no-char.decode.log
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
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-nochar.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
     Model word extractor: CNN
     Model       use_char: False
 ++++++++++++++++++++++++++++++++++++++++
 Training:
     Optimizer: SGD
     Iteration: 100
     BatchSize: 10
     Average  batch   loss: False
 ++++++++++++++++++++++++++++++++++++++++
 Hyperparameters:
     Hyper              lr: 0.0005
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  CNN
use crf:  False
build word sequence feature extractor: CNN...
build word representation...
CNN layer:  4
Decode raw data, nbest: None ...
Right token =  92774  All token =  95820  acc =  0.9682112293884366
raw: time:6.08s, speed:913.76st/s; acc: 0.9682, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-nochar.hyp

real    0m16.372s
user    0m13.804s
sys     0m3.765s
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

check the hyp file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ wc *.hyp
  101330   191640  1565878 wordcnn-charcnn.hyp
  101330   191640  1565878 wordcnn-charlstm.hyp
  101330   191640  1565878 wordcnn-nochar.hyp
  101330   191640  1565878 wordlstm-charcnn.hyp
  101330   191640  1565878 wordlstm-charlstm.hyp
  101330   191640  1565878 wordlstm-crf-charcnn.hyp
  101330   191640  1565878 wordlstm-crf-charlstm.hyp
  101330   191640  1565878 wordlstm-nochar.hyp
  810640  1533120 12527024 total
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$
```

ဖိုင်အတွင်းပိုင်းကိုလည်း တချက် စစ်ကြည့်ခဲ့ ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ head ./wordcnn-nochar.hyp 
ရင်ဘတ် B
အောင့် O
လာ N
ရင် N
သတိထား N
ပါ E

ဘယ်လောက် B
နောက်ကျ N
သလဲ E
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ tail ./wordcnn-nochar.hyp 
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

## 10. Word-CNN, CRF, Char-CNN

prepared the training config file:  
ဒီတစ်ခါတော့ CNN လည်း သုံးထားတာမို့ learning_rate ကိုပါ တစ်ခါတည်း 0.0005 အဖြစ် setting လုပ်ထားခဲ့တယ်။  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ nano word-cnn.crf.char-cnn.train.config

### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn
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
  GNU nano 4.8                                  word-cnn.crf.char-cnn.train.config                                            
word_emb_dim=50
char_emb_dim=30

###NetworkConfiguration###
use_crf=True
use_char=True
word_seq_feature=CNN
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
#learning_rate=0.015
#learning_rate=0.010
learning_rate=0.0005
lr_decay=0.05


(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.crf.char-cnn.train.config
### use # to comment out the configure item

### I/O ###
train_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/train.col
dev_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/valid.col
test_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn
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
#learning_rate=0.015
#learning_rate=0.010
learning_rate=0.0005
lr_decay=0.05
momentum=0
l2=1e-8
gpu=True
#clip=
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ 
```

start training ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ time python ./main.py --config ./mysent-para-config/word-cnn.crf.char-cnn.train.config 
| tee ./mysent-para-model/word-cnn.crf.char-cnn.train.log
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
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn
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
     Hyper              lr: 0.0005
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
 Learning rate is set as: 0.0005
Shuffle: first input word list: [38397, 2325, 64, 132, 213, 76, 578]
     Instance: 500; Time: 3.16s; loss: 6929.8676; acc: 6155/8986=0.6850
     Instance: 1000; Time: 3.35s; loss: 4352.8872; acc: 13972/18422=0.7584
     Instance: 1500; Time: 3.37s; loss: 3015.8322; acc: 22158/27720=0.7994
     Instance: 2000; Time: 3.05s; loss: 2344.8986; acc: 30395/36837=0.8251
     Instance: 2500; Time: 3.12s; loss: 1913.9837; acc: 38191/45333=0.8425
     Instance: 3000; Time: 3.55s; loss: 1886.4187; acc: 47271/55086=0.8581
     Instance: 3500; Time: 3.12s; loss: 1778.8959; acc: 55565/64013=0.8680
     Instance: 4000; Time: 2.93s; loss: 1326.1832; acc: 63617/72548=0.8769
     Instance: 4500; Time: 2.96s; loss: 1409.3281; acc: 71892/81330=0.8840
     Instance: 5000; Time: 3.05s; loss: 1431.0194; acc: 80097/90054=0.8894
     Instance: 5500; Time: 3.31s; loss: 1320.7947; acc: 88872/99330=0.8947
...
...
...
     Instance: 39000; Time: 3.36s; loss: 772.1368; acc: 652567/692759=0.9420
     Instance: 39500; Time: 2.83s; loss: 562.2374; acc: 660774/701354=0.9421
     Instance: 40000; Time: 2.63s; loss: 470.1953; acc: 668485/709420=0.9423
     Instance: 40500; Time: 2.76s; loss: 420.2751; acc: 675995/717207=0.9425
     Instance: 41000; Time: 2.71s; loss: 432.5034; acc: 684067/725578=0.9428
     Instance: 41500; Time: 2.76s; loss: 486.0373; acc: 692294/734127=0.9430
     Instance: 42000; Time: 3.14s; loss: 489.1758; acc: 700845/742998=0.9433
     Instance: 42500; Time: 2.69s; loss: 532.6120; acc: 708619/751145=0.9434
     Instance: 43000; Time: 2.95s; loss: 646.0695; acc: 717195/760169=0.9435
     Instance: 43500; Time: 3.04s; loss: 548.6318; acc: 725481/768845=0.9436
     Instance: 44000; Time: 2.97s; loss: 522.9386; acc: 733705/777474=0.9437
     Instance: 44500; Time: 3.47s; loss: 615.1402; acc: 742504/786667=0.9439
     Instance: 45000; Time: 3.07s; loss: 633.2893; acc: 751056/795694=0.9439
     Instance: 45500; Time: 2.85s; loss: 391.5775; acc: 759485/804405=0.9442
     Instance: 46000; Time: 2.79s; loss: 714.1477; acc: 767554/812921=0.9442
     Instance: 46500; Time: 3.04s; loss: 610.5478; acc: 776118/821965=0.9442
     Instance: 46991; Time: 3.08s; loss: 631.7781; acc: 784604/830865=0.9443
Epoch: 0 training finished. Time: 287.57s, speed: 163.41st/s,  total loss: 89235.01435852051
totalloss: 89235.01435852051
Right token =  58234  All token =  61166  acc =  0.9520648726416636
Dev: time: 5.95s, speed: 520.89st/s; acc: 0.9521, p: -1.0000, r: -1.0000, f: -1.0000
Exceed previous best f score: -10
Save current best model in file: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn.0.model
Right token =  92150  All token =  95820  acc =  0.9616990189939469
Test: time: 9.21s, speed: 602.81st/s; acc: 0.9617, p: -1.0000, r: -1.0000, f: -1.0000
Epoch: 1/100
 Learning rate is set as: 0.0004761904761904762
Shuffle: first input word list: [2020, 2395, 1947, 75, 14205, 287, 213, 211, 10]
     Instance: 500; Time: 2.97s; loss: 599.3589; acc: 8534/8917=0.9570
     Instance: 1000; Time: 3.33s; loss: 630.3753; acc: 16653/17478=0.9528
     Instance: 1500; Time: 3.16s; loss: 553.4618; acc: 25243/26480=0.9533
     Instance: 2000; Time: 2.74s; loss: 534.5479; acc: 33106/34684=0.9545
     Instance: 2500; Time: 3.01s; loss: 606.1016; acc: 41605/43631=0.9536
     Instance: 3000; Time: 3.22s; loss: 650.6442; acc: 49871/52304=0.9535
...
...
...

```

prepared the decoding config file:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$ cat word-cnn.crf.char-cnn.decode.config 
### Decode ###
status=decode
#raw_dir=sample_data/raw.bmes
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-config/data/para/test.col
#nbest=1
#nbest=10
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/wordcnn-crf-charcnn.hyp
#dset_dir=sample_data/lstmcrf.dset
dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn.dset
#load_model_dir=sample_data/lstmcrf.0.model
load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config$
```

decoding/testing ...  

```

```

check the hyp file:  

```

```

## 11. Word-CNN, CRF, Char-LSTM

prepare the training config file:  

```

```

start training ...  

```

```

prepare the decode/test config file:  

```

```

testing ...  

```

```

check the output hyp file:  

```

```

## 12. Word-CNN, CRF, No-char  

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
