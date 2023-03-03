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

## Prepare Config File for Word-LSTM, Char-CNN Model

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
