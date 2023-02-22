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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
