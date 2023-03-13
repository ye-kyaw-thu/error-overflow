# Cross Testing Between mySent and mySent-Para Models

## Preparation for mySent Model

အရင်ဆုံး mySent decode/test configuration file တွေကို ဖိုလ်ဒါအသစ်အောက်ကို ကော်ပီကူးထည့်ခဲ့ ...  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ ls
word-cnn.char-cnn.decode.config       word-lstm.char-cnn.decode.config
word-cnn.char-lstm.decode.config      word-lstm.char-lstm.decode.config
word-cnn.crf.char-cnn.decode.config   word-lstm.crf.char-cnn.decode.config
word-cnn.crf.char-lstm.decode.config  word-lstm.crf.char-lstm.decode.config
word-cnn.crf.nochar.decode.config     word-lstm.crf.nochar.decode.config
word-cnn.nochar.decode.config	      word-lstm.no-char.decode.config
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$
```

check no. of decode files:  
မော်ဒယ် ၁၂ ခုအတွက်မို့လို့ ၁၂ ဖိုင် ရှိရမယ်။  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ ls | wc
     12      12     411

```

configuration ဖိုင်ရဲ့ content က အောက်ပါအတိုင်း ရှိတယ်။  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ cat -n ./word-cnn.char-cnn.decode.config 
     1	### Decode ###
     2	status=decode
     3	#raw_dir=sample_data/raw.bmes
     4	raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     5	#nbest=1
     6	#nbest=10
     7	decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charcnn.hyp
     8	#dset_dir=sample_data/lstmcrf.dset
     9	dset_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.dset
    10	#load_model_dir=sample_data/lstmcrf.0.model
    11	load_model_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.0.model
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$
```

တကယ်တမ်း ငါ ဝင်ပြင်ရမှာက line no. 4 နဲ့ line no. 7 လို့ နားလည်တယ်။ line no. 4 မှာ sent အောက်က test data ကို ယူတာ မဟုတ်ပဲ para အောက်က test ဖိုင်ကို ယူရမှာ။ line no. 7 မှာက ဖြစ်နိုင်ရင် ဖိုင်နာမည် အသစ်နဲ့ hyp ဖိုင်ကို သိမ်းသင့်တယ်။  

အဲဒါကြောင့် configration file အားလုံးက line no. တူတူမှာ ရှိမရှိကို အောက်ပါအတိုင်း confirmation လုပ်ခဲ့တယ်။  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ find . -type f -name '*.config' -exec sed -n '4p;7p'  {} \;
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordcnn-charcnn.hyp
```

အထက်ပါအတိုင်း line no. 4 နဲ့ 7 က အားလုံး အတူတူပဲ ဆိုတာကို တွေ့ရတယ်။ အဲဒါဆိုရင် ငါ sed command ကိုပဲ ဖြစ်ဖြစ် သုံးပြီး decode confi ဖိုင်အားလုံးကို တစ်ခါတည်း ဝင်ပြင်ဖို့ ဖြစ်နိုင်တယ်။  

bash shell script တစ်ပုဒ် အောက်ပါအတိုင်း ရေးခဲ့ ...  

```bash
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ cat update-decode-config.sh 
#!/bin/bash

sed -i '4s#^.*$#raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col#' *.config

# error
#sed -i '7s#^.*$#decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp#' *.config

sed -i '7s#mysent-hyp#mysent-hyp/cross-test#' *.config
```

run the shell script:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ chmod +x ./update-decode-config.sh 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ ./update-decode-config.sh 
```

checked the update files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ find . -type f -name '*.config' -exec sed -n '4p;7p'  {} \;
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charcnn.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$
```

အထက်ပါ မြင်ရတဲ့အတိုင်း decode config ဖိုင်အားလုံးကို အဆင်ပြေပြေနဲ့ update လုပ်ပေးသွားပုံ ရတယ်။  

## Prepare cross-test.sh

cross testing လုပ်ဖို့ shell script ကို အောက်ပါအတိုင်း ရေးခဲ့ ...  

```bash
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ cat cross-test.sh 
#!/bin/bash

time python ./main.py --config $1

(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Cross-testing for mySent Model

run above shell script as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ chmod +x ./cross-test.sh 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ find /home/yekyaw.thu/tool/NCRFpp/mysent-config/cross-test/ -maxdepth 1 -type f -name '*.config' -exec ./cross-test.sh  {} \; | tee cross-test-mysent.log2
```

## Cross-testing Result for mySent Model

အောက်ပါ ရလဒ်တွေက mySent model ကို paragraph level test data နဲ့ decode/testing လုပ်ကြည့်ပြီး ရလာတဲ့ ရလဒ်တွေပါ။  

```
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charcnn.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
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
Right token =  83987  All token =  95820  acc =  0.8765080359006471
raw: time:9.52s, speed:582.15st/s; acc: 0.8765, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charcnn.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-nochar.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:9.38s, speed:590.77st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-nochar.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charlstm.hyp
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:7.76s, speed:714.94st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charlstm.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-nochar.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
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
Right token =  89665  All token =  95820  acc =  0.9357649759966604
raw: time:6.20s, speed:896.03st/s; acc: 0.9358, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-nochar.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charcnn.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:9.21s, speed:602.08st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charcnn.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charlstm.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
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
Right token =  89682  All token =  95820  acc =  0.9359423919849719
raw: time:10.82s, speed:511.76st/s; acc: 0.9359, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-crf-charlstm.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-nochar.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: True
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
CNN layer:  4
build CRF...
Decode raw data, nbest: None ...
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:9.41s, speed:589.15st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-nochar.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charcnn.hyp
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:6.70s, speed:828.88st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-charcnn.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-nochar.hyp
     Train instance number: 39999
     Dev   instance number: 2414
     Test  instance number: 4712
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordlstm-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
Decode raw data, nbest: None ...
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:6.55s, speed:848.15st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordlstm-nochar.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charlstm.hyp
     Train instance number: 39999
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-crf-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: LSTM ...
CNN layer:  4
build CRF...
Decode raw data, nbest: None ...
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:10.27s, speed:539.21st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-crf-charlstm.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charlstm.hyp
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:7.44s, speed:745.85st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charlstm.hyp
Seed num: 42
MODEL: decode
/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-model/wordcnn-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charcnn.hyp
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
Right token =  89713  All token =  95820  acc =  0.936265915257775
raw: time:6.29s, speed:884.17st/s; acc: 0.9363, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-hyp/cross-test/wordcnn-charcnn.hyp
```

သူရအောင်ရေ အထက်ပါ log ဖိုင်ထဲက ရလဒ်တွေကို အမှားအယွင်းမရှိအောင် ကူယူပြီး စာတမ်းကို update လုပ်ပါ။  
mySent model တစ်ခုပြီး တစ်ခု သုံးပြီး paragraph level test ဖိုင်နဲ့ run ခဲ့တာမို့လို့ model filename ကို confirm လုပ်ပြီး သွားမှ ဖြစ်လိမ့်မယ်။  

## Preparation for mySent-Para Model  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$ ls
word-cnn.char-cnn.decode.config       word-lstm.char-cnn.decode.config
word-cnn.char-lstm.decode.config      word-lstm.char-lstm.decode.config
word-cnn.crf.char-cnn.decode.config   word-lstm.crf.char-cnn.decode.config
word-cnn.crf.char-lstm.decode.config  word-lstm.crf.char-lstm.decode.config
word-cnn.crf.nochar.decode.config     word-lstm.crf.nochar.decode.config
word-cnn.no-char.decode.config	      word-lstm.no-char.decode.config
```

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$ ls | wc
     12      12     412
```

## Update the shell script

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$ cat ./update-decode-config.sh 
#!/bin/bash

sed -i '4s#^.*$#raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col#' *.config

sed -i '7s#mysent-para-hyp#mysent-para-hyp/cross-test#' *.config
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$
```

run above shell script as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$ ./update-decode-config.sh 
```

after running, checked line no. 4 and 7 of all config files as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$ find . -type f -name '*.config' -exec sed -n '4p;7p'  {} \;
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charcnn.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-nochar.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charlstm.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charcnn.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-config/cross-test$
```

## Create a New Folder

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-para-hyp$ mkdir cross-test
```

## Cross Testing for mySent-Para Model 

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ find /home/yekyaw.thu/tool/NCRFpp/mysent-para-config/cross-test/ -maxdepth 1 -type f -name '*.config' -exec ./cross-test.sh  {} \; | tee cross-test-mysent-para.log
```

## Results for mySent-Para Testing with Sentence Level Data

testing ရလဒ်တွေက အောက်ပါအတိုင်း ....   

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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charcnn.hyp
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
Right token =  54994  All token =  63622  acc =  0.8643865329602968
raw: time:5.82s, speed:814.44st/s; acc: 0.8644, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charcnn.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-nochar.hyp
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  True
build word sequence feature extractor: LSTM...
build word representation...
build CRF...
Decode raw data, nbest: None ...
Right token =  63266  All token =  63622  acc =  0.9944044512904341
raw: time:5.57s, speed:852.22st/s; acc: 0.9944, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-nochar.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charlstm.hyp
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
Right token =  63295  All token =  63622  acc =  0.9948602684605954
raw: time:4.87s, speed:975.18st/s; acc: 0.9949, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charlstm.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charcnn.hyp
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charcnn
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
Right token =  63160  All token =  63622  acc =  0.9927383609443274
raw: time:5.65s, speed:839.97st/s; acc: 0.9927, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charcnn.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charlstm.hyp
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
Right token =  63344  All token =  63622  acc =  0.9956304422998334
raw: time:6.67s, speed:710.46st/s; acc: 0.9956, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-crf-charlstm.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-nochar.hyp
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
Right token =  63244  All token =  63622  acc =  0.9940586589544497
raw: time:3.75s, speed:1270.56st/s; acc: 0.9941, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-nochar.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-nochar.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: True
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
CNN layer:  4
build CRF...
Decode raw data, nbest: None ...
Right token =  63254  All token =  63622  acc =  0.9942158372889881
raw: time:5.43s, speed:874.27st/s; acc: 0.9942, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-nochar.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charcnn.hyp
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
Right token =  47596  All token =  63622  acc =  0.7481060010688126
raw: time:4.06s, speed:1171.61st/s; acc: 0.7481, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-charcnn.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-nochar.hyp
     Train instance number: 46991
     Dev   instance number: 3077
     Test  instance number: 5510
     Raw   instance number: 0
     FEATURE num: 0
 ++++++++++++++++++++++++++++++++++++++++
 Model Network:
     Model        use_crf: False
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
nbest: None
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordlstm-nochar
build sequence labeling network...
use_char:  False
word feature extractor:  LSTM
use crf:  False
build word sequence feature extractor: LSTM...
build word representation...
Decode raw data, nbest: None ...
Right token =  63268  All token =  63622  acc =  0.9944358869573418
raw: time:3.87s, speed:1228.48st/s; acc: 0.9944, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordlstm-nochar.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charlstm.hyp
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
Load Model from file:  /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-crf-charlstm
build sequence labeling network...
use_char:  True
char feature extractor:  LSTM
word feature extractor:  CNN
use crf:  True
build word sequence feature extractor: CNN...
build word representation...
build char sequence feature extractor: LSTM ...
CNN layer:  4
build CRF...
Decode raw data, nbest: None ...
Right token =  63300  All token =  63622  acc =  0.9949388576278646
raw: time:6.46s, speed:734.59st/s; acc: 0.9949, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-crf-charlstm.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charlstm.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charlstm.hyp
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
Right token =  63404  All token =  63622  acc =  0.9965735123070636
raw: time:4.56s, speed:1041.92st/s; acc: 0.9966, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charlstm.hyp
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
     Raw    file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-config/data/sent/test.col
     Dset   file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.dset
     Model  file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn
     Loadmodel   directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-model/wordcnn-charcnn.0.model
     Decode file directory: /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charcnn.hyp
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
Right token =  63154  All token =  63622  acc =  0.9926440539436044
raw: time:3.84s, speed:1240.06st/s; acc: 0.9926, p: -1.0000, r: -1.0000, f: -1.0000
Predict raw result has been written into file. /home/yekyaw.thu/tool/NCRFpp/mysent-para-hyp/cross-test/wordcnn-charcnn.hyp
```

==== Fin ====

