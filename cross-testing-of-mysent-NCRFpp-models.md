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

sed -i '7s#^.*$#decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp#' *.config
```

run the shell script:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ chmod +x ./update-decode-config.sh 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ ./update-decode-config.sh 
```

checked the update files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$ find .  -maxdepth 1 -type f -name '*.config' -exec sed -n '4p;7p'  {} \;
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
raw_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-config/data/para/test.col
decode_dir=/home/yekyaw.thu/tool/NCRFpp/mysent-hyp/wordlstm-crf-charcnn.cross-test.hyp
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp/mysent-config/cross-test$
```

အထက်ပါ မြင်ရတဲ့အတိုင်း decode config ဖိုင်အားလုံးကို အဆင်ပြေပြေနဲ့ update လုပ်ပေးသွားပုံ ရတယ်။  

## Prepare cross-test.sh

cross testing လုပ်ဖို့ shell script ကို အောက်ပါအတိုင်း ရေးခဲ့ ...  

```bash
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ cat cross-test.sh 
#!/bin/bash

time python ./main.py --config $1 | tee ./mysent-model/$1.cross.log
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Cross-testing for mySent Model

run above shell script as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ chmod +x ./cross-test.sh 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ 
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ find ./mysent-config/cross-test/  -maxdepth 1 -type f -name '*.config' -exec ./cross-test.sh  {} \; | tee cross-test-mysent.log
```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


```

```

```

```

```

```

```

```

```

```


