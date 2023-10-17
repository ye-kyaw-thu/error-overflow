# myNER (9 tags version) Bi-LSTM Experiment-1

## Change Python Env

Change Anaconda python environment for bi-LSTM:  

```
(base) ye@lst-gpu-3090:~/exp/myNER$ conda activate bi_lstm_ner
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER$ ls
bi-LSTM  data  exp1.log.txt  xgboost
```

## Confirm Training/Testing Data

အရေးကြီးတာက bi-LSTM အတွက် သုံးတဲ့ training/testing ဒေတာကလည်း xg-boost အတွက် သုံးတာနဲ့ တူရမယ်။ အဲဒါမှသာ comparison လုပ်လို့ ရမှာမို့လို့ ...  

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ wc train.txt
   9201  137697 2195376 train.txt
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ wc test.txt
  1000  14925 237194 test.txt
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

## Head/Tail of the Training/Testing Data

Training data ရဲ့ head command output:  

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ head -n 5 ./train.txt
ပစ္စည်း/O ကောင်း/O ဝယ်/O ချင်/O ရင်/O ဘယ်/O ကို/O သွား/O ရ/O မ/O လဲ/O ။/O
သူ/O ဟာ/O လူသတ်/O မှု/O ကို/O မြင်/O ခဲ့/O တယ်/O ။/O
ကျွန်တော်/O က/O ကြိုးစားပမ်းစား/O သီဆို/O နေ/O တဲ့/O အဆိုတော်/O ကို/O လက်ခုပ်သြဘာ/O ပေး/O ခဲ့/O တယ်/O ။/O
ဟုတ်ကဲ့/O ။/O ဧည့်ခန်း/O ပါ/O ။/O
ရှီအတ်/O အစ္စလာမ်/O တွင်/O ဂိုဏ်း/O ခွဲ/O များ/O များ/O စွာ/O ရှိ/O သည်/O ။/O
```

tail command output:  

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ tail -n 5 ./train.txt
ပြင်သစ်/S-LOC သည်/O နော်ဝေး/S-LOC ထက်/O ပို/O ၍/O အလှမ်းဝေး/O သော/O ဘာသာ/O ရေး/O နှင့်/O မ/O ဆိုင်/O သော/O လူ့/O အဖွဲ့အစည်း/O တစ်/O ခု/O ဖြစ်/O ပြီး/O ၊/O ပြင်သစ်/O လူမျိုး/O များ/O သည်/O ၎င်း/O တို့/O ၏/O တရားစွဲ/O ဆို/O မှု/O တွင်/O အလွန်/O အလှမ်းဝေး/O ကွာ/O သွား/O လိမ့်/O မည်/O ဟု/O မတ်သိစ်ဖို့စီ/S-PER သည်/O ပြော/O ခဲ့/O သည်/O ။/O
များ/O ပြား/O လှ/O သော/O မြို့/O ကြီး/O များ/O ၊/O အထူးသဖြင့်/O နယူးယော့ခ်/B-LOC မြို့တော်/E-LOC ၌/O ကွင်းစ်/S-LOC နှင့်/O စတတ်တန်/B-LOC ကျွန်း/E-LOC ရှိ/O အချို့/O နေ/O ရာ/O များ/O သည်/O ဇူလိုင်/B-DATE လ/E-DATE လယ်/O ၏/O အပူလှိုင်း/O ကျ/O ရောက်/O ချိန်/O မှ/O စတင်/O ၍/O လျှပ်စစ်ဓါတ်အား/O ပြတ်တောက်/O မှု/O များ/O ကြောင့်/O ကြိုးစား/O ရုန်းကန်/O လှုပ်ရှား/O နေ/O ကြ/O ရ/O သည်/O ။/O
ပြည်ပ/O နိုင်ငံ/O များ/O ၏/O ယဉ်ကျေး/O မှု/O များ/O စိမ့်ဝင်/O ပျံ့နှံ/O လာ/O ခြင်း/O ကို/O တိုက်ဖျက်/O ရန်/O မြောက်ကိုရီးယား/S-LOC က/O ပြီး/O ခဲ့/O သည့်/O နှစ်/O က/O ဥပဒေ/O သစ်/O တစ်/O ရပ်/O ပြဌာန်း/O ထား/O ပြီး/O ၎င်း/O ဥပဒေ/O အရ/O တောင်ကိုရီးယား/S-LOC ဇာတ်ကား/O ဗီဒီယို/O များ/O ဖြန့်ဝေ/O ပါ/O က/O သေဒဏ်/O အထိ/O အပြစ်/O ပေး/O နိုင်/O ပြီး/O ကြည့်ရှု/O လျှင်/O လည်း/O ထောင်ဒဏ်/O ၁၅/S-NUM နှစ်/O အထိ/O အပြစ်/O ပေး/O နိုင်/O သည်/O ။/O
ထို/O ရောဂါ/O ခံစား/O နေ/O ရ/O သူ/O များ/O မှ/O အနည်းဆုံး/O ၈၀/S-NUM ရာခိုင်နှုန်း/O သည်/O အခြား/O ဆေး/O များ/O အား/O ခံနိုင်ရည်/O ရှိ/O မှု/O ကို/O ပြသ/O ခဲ့/O ပြီး/O ပြီ/O ဖြစ်/O သည်/O ။/O
ဝီကီ/B-ORG နယူး/E-ORG မှ/O ပထမဆုံး/O ဖော်ပြ/O ခဲ့/O သည့်/O စုံစမ်း/O စစ်ဆေး/O ခြင်း/O တစ်/O ခု/O တွင်/O ဝီကီလိခ်/S-ORG က/O ယနေ့/O ဂွမ်တာနာမို/B-LOC စခန်း/E-LOC မှာ/O မြစ်ဝကျွန်းပေါ်/O စက်ရုံ/O များ/O အတွက်/O အဆင့်/O မီ/O သော/O လုပ်ငန်းစဉ်/O များ/O (/O အက်စ်အိုပီ/O )/O ကို/O ယင်း/O အကြောင်းအရာ/O ၏/O အခြား/O အခန်း/O တွင်/O ဖော်ပြ/O ထား/O သည်/O ။/O
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

Testing data အတွက် ...  

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ head -n 5 test.txt
အပေါ်ထပ်/O မှာ/O ပြင်/O ထား/O ပါ/O တယ်/O ။/O လိုက်/O ပို့/O ပေး/O ပါ/O မယ်/O ။/O
လွယ်/O တဲ့/O စကား/O တွေ/O ရှိ/O သလို/O ခက်ခဲ/O တဲ့/O စကား/O လည်း/O ရှိ/O တာ/O သဘာဝ/O ပဲ/O ။/O
သခင်/B-PER အောင်ဆန်း/E-PER သည်/O ကိုယ်ခန္ဓာ/O ညှက်/O ပြီး/O အားကောင်း/O သန်မာ/O လှ/O ခြင်း/O မ/O ရှိ/O သော်လည်း/O တိုက်ရေးခိုက်ရေး/O ကျွမ်းကျင်/O ကာ/O သတ္တိ/O ရှိ/O ၍/O အပင်ပန်း/O ခံ/O နိုင်/O သော/O စစ်သား/O တစ်/O ဦး/O ဖြစ်/O လာ/O ၏/O ။/O
အရင်/O တုန်း/O က/O သူ/O မကြာခဏ/O အလည်လာ/O လေ့/O ရှိ/O ပေမဲ့/O အခုတလော/O တော့/O လုံးဝ/O သူ့/O မျက်နှာ/O ကို/O မ/O မြင်/O ရ/O ဘူး/O ။/O
ဥပဒေ/O အရ/O ထိမ်းမြား/O ခြင်း/O ဖြင့်/O ဖြစ်စေ/O အခြား/O နည်း/O ဖြင့်/O ဖြစ်စေ/O မွေးဖွား/O သော/O ကလေး/O အားလုံး/O သည်/O တူညီ/O သော/O လူမှု/O ကာကွယ်/O စောင့်ရှောက်/O ရေး/O ကို/O ရယူ/O ခံစား/O ကြ/O ရ/O မည်/O ။/O
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ tail -n 5 test.txt
ဒီ/O အညိုရောင်/O လေး/O ပြော/O တာ/O လား/O ။/O
ညှပ်/O ပြီး/O ရိတ်/O ပေး/O ပါ/O ။/O
ပူတောင်း/O ဆို/O သည်/O မှာ/O ရှမ်း/O ဘာသာ/O အားဖြင့်/O ပူ/O အဘိုး/O ၊/O တောင်း/O စောင့်/O သည်/O အဘိုး/O မျှော်/O မြို့/O ဟု/O အဓိပ္ပါယ်ရ/O သည်/O ။/O
အဲဒီ/O လူ/O ရဲ့/O စကား/O က/O တချက်/O မှ/O မ/O မှား/O ဘူး/O ။/O
အတော်/O ပါ/O ပဲ/O ။/Oဒါပေမဲ့/O အမှန်/O မှာ/O သူ/O တို့/O သည်/O ဘာသာ/O ရေး/O သမား/O များ/O ဖြစ်/O တယ်/O လို့/O ဒင်ဗာ/S-LOC ၏/O ဘာသာ/O ရေး/O လေ့လာ/O မှု/O တက္ကသိုလ်/O ပါမောက္ခ/B-PER ကားရပ်ချက်ခ်/E-PER က/O ဝေါစထရစ်/B-ORG ဂျာနယ်/E-ORG မှ/O ကြေညာ/O ချက်/O တစ်/O ခု/O ထဲ/O မှာ/O ဖော်ပြ/O ထား/O ပါ/O တယ်/O ။/O
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

## Training Bi-LSTM Model

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ python ./bi-lstm_ner.py --help
2023-10-17 15:50:04.660660: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcudart.so.11.0
usage: bi-lstm_ner.py [-h] [-a ACTIVATION_FUNC] [-lr LEARNING_RATE] [-hu HIDDEN_UNITS]
                      [-ed EMBEDDING_DIM]
                      {train,test} ...

Bi-LSTM for NER in Burmese

positional arguments:
  {train,test}          Task to be performed ('train' or 'test')
    train               Train the model
    test                Test the model

optional arguments:
  -h, --help            show this help message and exit
  -a ACTIVATION_FUNC, --activation_func ACTIVATION_FUNC
                        Activation function for output layer
  -lr LEARNING_RATE, --learning_rate LEARNING_RATE
                        Learning rate for optimizer
  -hu HIDDEN_UNITS, --hidden_units HIDDEN_UNITS
                        Number of hidden units in LSTM layer
  -ed EMBEDDING_DIM, --embedding_dim EMBEDDING_DIM
                        Dimension of embedding layer
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```


```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
