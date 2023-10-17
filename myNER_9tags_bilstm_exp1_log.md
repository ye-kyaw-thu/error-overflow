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

Start training ...  

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ time python ./bi-lstm_ner.py train -i train.txt -m ./exp1_bilstm.model
2023-10-17 15:54:50.669012: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcudart.so.11.0
Saved Tag Map during training: {'<PAD>': 0, 'B-DATE': 1, 'B-EVENT': 2, 'B-LOC': 3, 'B-NUM': 4, 'B-ORG': 5, 'B-PER': 6, 'B-PRODUCT': 7, 'B-TIME': 8, 'E-DATE': 9, 'E-EVENT': 10, 'E-LOC': 11, 'E-NUM': 12, 'E-ORG': 13, 'E-PER': 14, 'E-PRODUCT': 15, 'E-TIME': 16, 'I-DATE': 17, 'I-EVENT': 18, 'I-LOC': 19, 'I-NUM': 20, 'I-ORG': 21, 'I-PER': 22, 'I-PRODUCT': 23, 'I-TIME': 24, 'O': 25, 'S-DATE': 26, 'S-EVENT': 27, 'S-LOC': 28, 'S-NUM': 29, 'S-ORG': 30, 'S-PER': 31, 'S-PRODUCT': 32, 'S-TIME': 33}
2023-10-17 15:54:51.442871: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcuda.so.1
2023-10-17 15:54:51.482662: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:937] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-10-17 15:54:51.483015: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1733] Found device 0 with properties:
pciBusID: 0000:01:00.0 name: NVIDIA GeForce RTX 3090 Ti computeCapability: 8.6
coreClock: 1.95GHz coreCount: 84 deviceMemorySize: 23.68GiB deviceMemoryBandwidth: 938.86GiB/s
2023-10-17 15:54:51.483112: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcudart.so.11.0
2023-10-17 15:54:51.928175: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcublas.so.11
2023-10-17 15:54:51.928278: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcublasLt.so.11
2023-10-17 15:54:52.265716: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcufft.so.10
2023-10-17 15:54:52.369599: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcurand.so.10
2023-10-17 15:54:52.431944: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcusolver.so.11
2023-10-17 15:54:52.725307: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library libcusparse.so.11
2023-10-17 15:54:52.726032: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /usr/local/cuda-11.8/lib64:
2023-10-17 15:54:52.726063: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1766] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2023-10-17 15:54:52.726642: I tensorflow/core/platform/cpu_feature_guard.cc:142] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-10-17 15:54:52.730907: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1258] Device interconnect StreamExecutor with strength 1 edge matrix:
2023-10-17 15:54:52.730955: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1264]
2023-10-17 15:54:53.583429: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 182424960 exceeds 10% of free system memory.
2023-10-17 15:54:53.694903: I tensorflow/compiler/mlir/mlir_graph_optimization_pass.cc:176] None of the MLIR Optimization Passes are enabled (registered 2)
2023-10-17 15:54:53.702268: I tensorflow/core/platform/profile_utils/cpu_utils.cc:114] CPU Frequency: 2419200000 Hz
Epoch 1/10
130/130 [==============================] - 10s 56ms/step - loss: 0.0906 - accuracy: 0.9223 - val_loss: 0.0375 - val_accuracy: 0.9365
Epoch 2/10
130/130 [==============================] - 6s 48ms/step - loss: 0.0296 - accuracy: 0.9376 - val_loss: 0.0283 - val_accuracy: 0.9365
Epoch 3/10
130/130 [==============================] - 6s 48ms/step - loss: 0.0235 - accuracy: 0.9377 - val_loss: 0.0252 - val_accuracy: 0.9372
Epoch 4/10
130/130 [==============================] - 7s 52ms/step - loss: 0.0205 - accuracy: 0.9403 - val_loss: 0.0234 - val_accuracy: 0.9417
Epoch 5/10
130/130 [==============================] - 7s 55ms/step - loss: 0.0183 - accuracy: 0.9475 - val_loss: 0.0220 - val_accuracy: 0.9468
Epoch 6/10
130/130 [==============================] - 7s 52ms/step - loss: 0.0161 - accuracy: 0.9551 - val_loss: 0.0202 - val_accuracy: 0.9525
Epoch 7/10
130/130 [==============================] - 7s 52ms/step - loss: 0.0139 - accuracy: 0.9623 - val_loss: 0.0192 - val_accuracy: 0.9563
Epoch 8/10
130/130 [==============================] - 7s 52ms/step - loss: 0.0119 - accuracy: 0.9673 - val_loss: 0.0182 - val_accuracy: 0.9587
Epoch 9/10
130/130 [==============================] - 7s 53ms/step - loss: 0.0102 - accuracy: 0.9716 - val_loss: 0.0174 - val_accuracy: 0.9608
Epoch 10/10
130/130 [==============================] - 7s 52ms/step - loss: 0.0087 - accuracy: 0.9756 - val_loss: 0.0174 - val_accuracy: 0.9619
2023-10-17 15:56:06.334223: W tensorflow/python/util/util.cc:348] Sets are not currently considered sequences, but this may change in the future, so consider avoiding using them.
WARNING:absl:Found untraced functions such as lstm_cell_1_layer_call_and_return_conditional_losses, lstm_cell_1_layer_call_fn, lstm_cell_2_layer_call_and_return_conditional_losses, lstm_cell_2_layer_call_fn, lstm_cell_1_layer_call_fn while saving (showing 5 of 10). These functions will not be directly callable after loading.

real    1m22.599s
user    8m32.847s
sys     0m42.212s
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
