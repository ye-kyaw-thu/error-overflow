# 2 FastText Model Experiment Log

By Ye Kyaw Thu.  
Last updated: 23 Mar 2024  

## Create New Conda Env

```
(base) ye@lst-gpu-server-197:~/ye$ conda create --name hs-fasttext python=3.10
```

```
(base) ye@lst-gpu-server-197:~/ye$ conda activate hs-fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/ye$
```


## FastText Installation

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ git clone https://github.com/facebookresearch/fastText.git
Cloning into 'fastText'...
remote: Enumerating objects: 3998, done.
remote: Counting objects: 100% (1026/1026), done.
remote: Compressing objects: 100% (195/195), done.
remote: Total 3998 (delta 890), reused 860 (delta 826), pack-reused 2972
Receiving objects: 100% (3998/3998), 8.30 MiB | 8.43 MiB/s, done.
Resolving deltas: 100% (2528/2528), done.
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cd fastText/
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/fastText$ make
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/args.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/autotune.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/matrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/dictionary.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/loss.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/productquantizer.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/densematrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/quantmatrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/vector.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/model.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/utils.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/meter.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/fasttext.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG args.o autotune.o matrix.o dictionary.o loss.o productquantizer.o densematrix.o quantmatrix.o vector.o model.o utils.o meter.o fasttext.o src/main.cc -o fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/fastText$
```

Check fasttext --help ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/fastText$ ./fasttext --help
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              train a supervised classifier
  quantize                quantize a model to reduce the memory usage
  test                    evaluate a supervised classifier
  test-label              print labels with precision and recall scores
  predict                 predict most likely labels
  predict-prob            predict most likely labels with probabilities
  skipgram                train a skipgram model
  cbow                    train a cbow model
  print-word-vectors      print word vectors given a trained model
  print-sentence-vectors  print sentence vectors given a trained model
  print-ngrams            print ngrams given a trained model and word
  nn                      query for nearest neighbors
  analogies               query for analogies
  dump                    dump arguments,dictionary,input/output vectors
```

## Checked FastText Python Library

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/fastText$ python
Python 3.10.14 (main, Mar 21 2024, 16:24:04) [GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fasttext
>>> print(dir(fasttext))
['BOW', 'EOS', 'EOW', 'FastText', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__', 'absolute_import', 'cbow', 'division', 'load_model', 'print_function', 'skipgram', 'supervised', 'tokenize', 'train_supervised', 'train_unsupervised', 'unicode_literals']
>>>
```

## Data Preparation

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc hs_data_Mar19.txt
  10140  181470 2251295 hs_data_Mar19.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ file ./hs_data_Mar19.txt
./hs_data_Mar19.txt: Unicode text, UTF-8 text, with very long lines (489)
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Current Format:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt
ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣  ab
နား ကို မ လည် တာ        no
ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ       ab
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်      no
ဖလော်မော်/ab next version       ab
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂    no
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
no
ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬  ab
sမွေး/ab ကြီး တဲ့ 😂    ab
$မွှေး/ab ပါ    ab
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Prepared FastText label format:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./fasttext_format_converter.py --help
usage: fasttext_format_converter.py [-h] [--input INPUT] [--output OUTPUT]
                                    [--reverse]

Converts text data for FastText format.

options:
  -h, --help       show this help message and exit
  --input INPUT    Input file path. If not provided, reads from stdin.
  --output OUTPUT  Output file path. If not provided, writes to stdout.
  --reverse        Reverse conversion (from FastText format to original).
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./fasttext_format_converter.py --input ./hs_data_Mar19.txt --output ./hs_data_Mar19.txt.fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Checked the converted format:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext
__label__ab     ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣
__label__no     နား ကို မ လည် တာ
__label__ab     ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ
__label__no     ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab     ဖလော်မော်/ab next version
__label__no     ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no     ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab     ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab     sမွေး/ab ကြီး တဲ့ 😂
__label__ab     $မွှေး/ab ပါ
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Check filesize:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt
  10140  181470 2251295 ./hs_data_Mar19.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt.fasttext
  10137  181411 2341789 ./hs_data_Mar19.txt.fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

filesize တော့ ပြောင်းသွားတယ်။  

Remove tags ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./rm-tags.py --input ./hs_data_Mar19.txt.fasttext | head
__label__ab ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
__label__no နား ကို မ လည် တာ
__label__ab ဆောက်မြင်ကပ် ထင် တာ ပဲ
__label__no ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab ဖလော်မော် next version
__label__no ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab ဖော်လော်မော် နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab sမွေး ကြီး တဲ့ 😂
__label__ab $မွှေး ပါ
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./rm-tags.py --input ./hs_data_Mar19.txt.fasttext --output ./hs_data_Mar19.txt.fasttext.rm-tag
```

Checked the tag removed file:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt.fasttext
  10137  181411 2341789 ./hs_data_Mar19.txt.fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt.fasttext.rm-tag
  10137  181374 2292036 ./hs_data_Mar19.txt.fasttext.rm-tag
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Confirm the tag removed file:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext.rm-tag
__label__ab ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
__label__no နား ကို မ လည် တာ
__label__ab ဆောက်မြင်ကပ် ထင် တာ ပဲ
__label__no ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab ဖလော်မော် next version
__label__no ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab ဖော်လော်မော် နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab sမွေး ကြီး တဲ့ 😂
__label__ab $မွှေး ပါ
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Confirm with tail command:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail ./hs_data_Mar19.txt.fasttext.rm-tag
__label__ab သူ့ ကို ဘာ ကြည့် ပြီး vote ပေး ကြ တာ ပါ လိမ့် $ရူးမ ဘာ မ ဟုတ် တဲ့ ကိစ္စ ကြောင့် ရွှေကြို အခွင့်အရေး ကို ဆုံးရှုံး မ ခံ နိုင် လို့ ဆို ပြီး ပြော တဲ့ $ရူးမ
__label__ab ဖင်အရှည်ကြီးခံလိုက် တစ်ခါတည်း အကုန် ကြို ပြီး သား ပဲ 🦭
__label__no အိပ်မက် က အမ တစ် ယောက် ပဲ ရှိ တာ လား 🥲
__label__ab SattPatt !! ဘာ မ ဟုတ် တဲ့ ပြဿနာ တဲ့ PayloeeeMaaaGGG
__label__ab စောက်ဆင့်မရှိ တဲ့ ဟာ တွေ က လည်း အခုတလော ခပ်စိပ်စိပ် တွေ့ လာ ရ တယ် 🤣🤣🤣🤣🤣 ရေး ချင် လွန်း လို့ မ ဟုတ် ဘူး နော် ရှက် တတ် ဦး မ လား လို့ ဝင့် မန့် တာ
__label__ab ဘာ မ ဟုတ် တာ လေး တဲ့ အာ့ ဆို ဟုတ် တဲ့ ဟာ ဘောပဲမနေ နော် အမကြီး
__label__le ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး ဆို တာ ခု မှ အရှင်လတ်လတ် မြင် ဖူး တော့ တယ် ကောင်မ မွေးကတည်းကအသေလေးမွေးလာရမှာ
__label__ab အော် ဘာ မ ဟုတ် တာ တဲ့ လား ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်
__label__ab ဗန်းကိုင် နဲ့ မအလ ဘောကိုင်
__label__bo စိတ်မပူ နဲ့ ရွှေကြို ပြီး ရင် ဖင်ခံ ရ မှာ ညီမလေး fighting 22 နှစ် က ငါ 25 နှစ် ထက် အို နေ တော့ အား တောင် နာ တယ် 😂 😂
```

## Thinking for One More Input File  

အိုက်ဒီယာ အကြမ်းကတော့ စာကြောင်း အရှည်ကနေ hatespeech နဲ့ ဆိုင်တဲ့ စာလုံးနဲ့ သူနဲ့ တွဲနေတဲ့ tag information ကို နောက်ထပ် သပ်သပ် training ဖိုင်တစ်ခုအနေနဲ့ ထားချင်တာ ...

သို့သော် လက်တွေ့မှာက စာကြောင်း တစ်ကြောင်းတည်းမှာတင် multiple tag, multiple word ပါနိုင်တယ်။ အဲဒါနဲ့ final decision လုပ်ရမယ့် hatespeech tag နဲ့ ဘယ်လိုညှိကြမလဲ ဆိုတဲ့အချက် ... 

စဉ်းစား၊ စဉ်းစား၊ စဉ်းစား ... 

For this time, I wanna you to write a new python code for different task. I have following utf-8 text file:

I have following format utf-8 text file:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext
__label__ab     ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣
__label__no     နား ကို မ လည် တာ
__label__ab     ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ
__label__no     ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab     ဖလော်မော်/ab next version
__label__no     ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no     ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab     ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab     sမွေး/ab ကြီး တဲ့ 😂
__label__ab     $မွှေး/ab ပါ
__label__se     ဖင်ကြီး/se နှစ် လုံး ပဲ တွေ့ တယ်

============

I wanna you to write a python code for removing no tagged words from each sentence. For the sentence that not contain any tag should replace with For example for the above example intpu, the output will be as follows:

I have following format utf-8 text file:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext
__label__ab     ဖော်လော်မော်/ab
__label__no     နား ကို မ လည် တာ
__label__ab     ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ
__label__no     ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab     ဖလော်မော်/ab next version
__label__no     ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no     ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab     ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab     sမွေး/ab ကြီး တဲ့ 😂
__label__ab     $မွှေး/ab ပါ
__label__se     ဖင်ကြီး/se နှစ် လုံး ပဲ တွေ့ တယ်


## Creating Hatespeech Dictionary 

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cut -f2 ./hs_data_Mar19.txt.fasttext > ./hs_data_Mar19.txt.fasttext.f2
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext.f2
ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣
နား ကို မ လည် တာ
ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
ဖလော်မော်/ab next version
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬
sမွေး/ab ကြီး တဲ့ 😂
$မွှေး/ab ပါ
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail ./hs_data_Mar19.txt.fasttext.f2
သူ့ ကို ဘာ ကြည့် ပြီး vote ပေး ကြ တာ ပါ လိမ့် $ရူးမ/ab ဘာ မ ဟုတ် တဲ့ ကိစ္စ ကြောင့် ရွှေကြို အခွင့်အရေး ကို ဆုံးရှုံး မ ခံ နိုင် လို့ ဆို ပြီး ပြော တဲ့ $ရူးမ/ab
ဖင်အရှည်ကြီးခံလိုက်/ab တစ်ခါတည်း အကုန် ကြို ပြီး သား ပဲ 🦭
အိပ်မက် က အမ တစ် ယောက် ပဲ ရှိ တာ လား 🥲
SattPatt/ab !! ဘာ မ ဟုတ် တဲ့ ပြဿနာ တဲ့ PayloeeeMaaaGGG/ab
စောက်ဆင့်မရှိ/ab တဲ့ ဟာ တွေ က လည်း အခုတလော ခပ်စိပ်စိပ် တွေ့ လာ ရ တယ် 🤣🤣🤣🤣🤣 ရေး ချင် လွန်း လို့ မ ဟုတ် ဘူး နော် ရှက် တတ် ဦး မ လား လို့ ဝင့် မန့် တာ
ဘာ မ ဟုတ် တာ လေး တဲ့ အာ့ ဆို ဟုတ် တဲ့ ဟာ ဘောပဲမနေ/ab နော် အမကြီး
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး/ab ဆို တာ ခု မှ အရှင်လတ်လတ် မြင် ဖူး တော့ တယ် ကောင်မ/ab မွေးကတည်းကအသေလေးမွေးလာရမှာ/le
အော် ဘာ မ ဟုတ် တာ တဲ့ လား ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်/ab
ဗန်းကိုင် နဲ့ မအလ/ab|po ဘောကိုင်/ab
စိတ်မပူ နဲ့ ရွှေကြို ပြီး ရင် ဖင်ခံ/ab ရ မှာ ညီမလေး fighting 22 နှစ် က ငါ 25 နှစ် ထက် အို/bo နေ တော့ အား တောင် နာ တယ် 😂 😂
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

အဲဒီကနေ အောက်ပါလိုမျိုး အဘိဓာန်ဆောက်ချင်တယ် ...  

```
ဖော်လော်မော်<TAB>ab
ဆောက်မြင်ကပ်<TAB>ab
ဖလော်မော်<TAB>ab
ဖော်လော်မော်<TAB>ab
sမွေး<TAB>ab
$မွှေး<TAB>ab
$ရူးမ<TAB>ab
$ရူးမ<TAB>ab
ဖင်အရှည်ကြီးခံလိုက်<TAB>ab
SattPatt<TAB>ab
PayloeeeMaaaGGG<TAB>ab
စောက်ဆင့်မရှိ<TAB>ab
ဘောပဲမနေ<TAB>ab
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး<TAB>ab
ကောင်မ<TAB>ab
မွေးကတည်းကအသေလေးမွေးလာရမှာ<TAB>le
ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်<TAB>ab
မအလ<TAB>ab|po
ဘောကိုင်<TAB>ab
ဖင်ခံ<TAB>ab
အို<TAB>bo
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./mk_hatespeech_dict.py --input ./hs_data_Mar19.txt.fasttext.f2 --output hs_dict.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_dict.txt
  5492  10981 214776 ./hs_dict.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_dict.txt
ဖော်လော်မော်    ab
ဆောက်မြင်ကပ်    ab
ဖလော်မော်       ab
sမွေး   ab
$မွှေး  ab
စ-ပပြဲမ ab
မဘသအရိုးကိုက်   re
လူကမွေးထားတဲ့ဟာတွေလား   ab
ကောင်မ  ab
ဖင်စောင့်       ab
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail ./hs_dict.txt
zb      ab
သော်ဒေါ်စော်    ab
အားတန်းစောက်မ   ab
SattPatt        ab
PayloeeeMaaaGGG ab
ဘောပဲမနေ        ab
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး   ab
မွေးကတည်းကအသေလေးမွေးလာရမှာ      le
ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်        ab
အို     bo
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

ဆွဲထုတ်ထားတဲ့ dictionry ကို စစ်ကြည့်တော့ cleaning လုပ်ဖို့ လိုအပ်တယ်။  

```
တစ်ကိုယ်လုံးချွတ်	ab|se
	|ab|abကြ|abတဲ့
‌ေ-သ	ab
မအေလိုး	ab|ab​|po
💩စား🐕‍🦺	ab
```

အချိန်မရှိတော့လို့၊ ပြီးတော့ cleaning လုပ်မယ်ဆိုရင် dictionary တစ်ခုတည်းမဟုတ်ပဲ စာကြောင်းအလိုက်ရှိနေတဲ့ data ဖိုင်ကိုလည်း cleaning လုပ်ဖို့ လိုအပ်တယ်။  
အဲဒါကြောင့် cleaning step ကို skip လုပ်ခဲ့တယ်။  

make Sorting/Unique ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ sort hs_dict.txt | uniq > hs_dict.txt.uniq
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_dict.txt
  5492  10981 214776 ./hs_dict.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_dict.txt.uniq
  5492  10981 214776 ./hs_dict.txt.uniq
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail ./hs_dict.txt
zb      ab
သော်ဒေါ်စော်    ab
အားတန်းစောက်မ   ab
SattPatt        ab
PayloeeeMaaaGGG ab
ဘောပဲမနေ        ab
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး   ab
မွေးကတည်းကအသေလေးမွေးလာရမှာ      le
ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်        ab
အို     bo
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail ./hs_dict.txt.uniq
ောက်ပေါ ab
ေ-ာက်ပေါက်      ab
ေ-ာက်မြင်အကတ်ဆုံး       ab
ေ-ာက်ရူး        ab
ေ-ာက်ရူးချေးပန်း        ab
ေ-ာက်ရူးမ       ab
‌ောက်ရေးပါ      ab
ေ-ာက်ရေးမပါ     ab
ေ-ာက်သုံးမကျ    ab
ေ-ာက်အခွင့်အလမ်း        ab
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_dict.txt.uniq
$$$$ကျက်သတုံး   ab
$$$$ရှက်        ab
$$$$အပို        ab
$       ab
$P      ab
$paw    ab
$ph     ab
$pw     ab
$shat   ab
$ကမ     ab
```

## Filter Hatespeech Word/Phrase

$ cat filter_hatespeech.py  

```python
"""
For filtering hatespeech only.
Written by Ye Kyaw Thu, NECTEC, Thailand.
Last updated: 22 Mar 2024
Usage:
python ./filter_hatespeech.py --help

python ./filter_hatespeech.py -d hs_dict.txt.uniq \
-i hs_data_Mar19.txt.fasttext.rm-tag \
-o ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
"""

import argparse

def load_hate_speech_dictionary(dict_file):
    """
    Load hate speech dictionary from file.
    Returns a set of hate speech words.
    """
    hate_speech_words = set()
    with open(dict_file, 'r', encoding='utf-8') as f:
        for line in f:
            parts = line.strip().split('\t')
            if len(parts) == 2:
                word = parts[0]
                hate_speech_words.add(word)
    return hate_speech_words

def filter_hate_speech_only(input_file, output_file, hate_speech_words):
    """
    Filter input sentences, keeping only words present in hate speech dictionary.
    Writes the filtered sentences to the output file or stdout.
    """
    with open(input_file, 'r', encoding='utf-8') as f:
        lines = f.readlines()

    with open(output_file, 'w', encoding='utf-8') as f_out:
        for line in lines:
            label, sentence = line.strip().split(' ', 1)
            if label != "__label__no":
                filtered_sentence = ' '.join(word for word in sentence.split() if word in hate_speech_words)
                f_out.write(f"{label} {filtered_sentence}\n")
            else:
                f_out.write(f"{label} {sentence}\n")  # Write the line as is

def main():
    parser = argparse.ArgumentParser(description="Filter input sentences to keep only hate speech words.")
    parser.add_argument("-d", "--dict", required=True, help="Path to the hate speech dictionary file")
    parser.add_argument("-i", "--input", required=True, help="Path to the input file containing sentences")
    parser.add_argument("-o", "--output", help="Path to the output file to save filtered sentences")
    args = parser.parse_args()

    hate_speech_words = load_hate_speech_dictionary(args.dict)

    if args.output:
        filter_hate_speech_only(args.input, args.output, hate_speech_words)
        print(f"Filtered sentences saved to {args.output}")
    else:
        filter_hate_speech_only(args.input, None, hate_speech_words)

if __name__ == "__main__":
    main()

```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ python ./filter_hatespeech.py -d hs_dict.txt.uniq -i hs_data_Mar19.txt.fasttext.rm-tag -o ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
Filtered sentences saved to ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Let's see the filtered outputs:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
__label__ab ဖော်လော်မော် မ
__label__no နား ကို မ လည် တာ
__label__ab ဆောက်မြင်ကပ် ပဲ
__label__no ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab ဖလော်မော်
__label__no ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab ဖော်လော်မော်
__label__ab sမွေး
__label__ab $မွှေး
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

## Training with Two Models

Now, I have following two corpora:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt.fasttext.rm-tag
  10137  181374 2292036 ./hs_data_Mar19.txt.fasttext.rm-tag
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ wc ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
 10137  68620 998009 ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Long sentence data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt
.fasttext.rm-tag
__label__ab ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
__label__no နား ကို မ လည် တာ
__label__ab ဆောက်မြင်ကပ် ထင် တာ ပဲ
__label__no ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab ဖလော်မော် next version
__label__no ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab ဖော်လော်မော် နဲ့ ညီမ တော် တယ် လေ 😬
__label__ab sမွေး ကြီး တဲ့ 😂
__label__ab $မွှေး ပါ
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Filtered Hatespeech Only Data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head ./hs_data_Mar19.txt.fasttext.rm-tag.filtered
__label__ab ဖော်လော်မော် မ
__label__no နား ကို မ လည် တာ
__label__ab ဆောက်မြင်ကပ် ပဲ
__label__no ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
__label__ab ဖလော်မော်
__label__no ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
__label__no ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
__label__ab ဖော်လော်မော်
__label__ab sမွေး
__label__ab $မွှေး
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Training/Testing Data Splitting ...  
For long-data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head -n 9137 ./hs_data_Mar19.txt.fasttext.rm-tag > ./long-data/ltrain.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail -n 1000 ./hs_data_M
ar19.txt.fasttext.rm-tag > ./long-data/ltest.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

For short-data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head -n 9137 ./hs_data_M
ar19.txt.fasttext.rm-tag.filtered > ./short-data/strain.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail -n 1000 ./hs_data_M
ar19.txt.fasttext.rm-tag.filtered > ./short-data/stest.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Training with two dataset and let's see the results ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat run-2models.sh
#!/bin/bash

## Training
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt

## Testing
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt
```

Run the above shell script ...  
1st-time result is as follows:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-2models.sh
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  24.7% words/sec/thread:  343550 lr:  0.075267 avg.loss:  1.294877 ETA: Progress:  49.9% words/sec/thread:  348613 lr:  0.050080 avg.loss:  0.815104 ETA: Progress:  74.9% words/sec/thread:  349665 lr:  0.025125 avg.loss:  0.627692 ETA: Progress: 100.0% words/sec/thread:  350778 lr:  0.000033 avg.loss:  0.504076 ETA: Progress: 100.0% words/sec/thread:  281093 lr: -0.000018 avg.loss:  0.503959 ETA: Progress: 100.0% words/sec/thread:  280877 lr:  0.000000 avg.loss:  0.503959 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  31.5% words/sec/thread:  179264 lr:  0.068461 avg.loss:  0.554960 ETA: Progress:  63.4% words/sec/thread:  183341 lr:  0.036612 avg.loss:  0.333089 ETA: Progress:  96.0% words/sec/thread:  186459 lr:  0.003996 avg.loss:  0.257902 ETA: Progress: 100.0% words/sec/thread:  146147 lr: -0.000013 avg.loss:  0.250880 ETA: Progress: 100.0% words/sec/thread:  146005 lr:  0.000000 avg.loss:  0.250880 ETA:   0h 0m 0s

real    0m5.038s
user    0m29.255s
sys     0m4.743s
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.674
Short Word Model Accuracy: 0.736

real    0m1.585s
user    0m1.797s
sys     0m3.251s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

I updated the bash shell script as follows:  

```bash
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat run-2models.sh
#!/bin/bash

## Training with default parameters
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt

## Testing
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt

## Training with ngram 3
echo "Training with --word_ngrams 3"
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 3

## Testing
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt

## Training with ngram 5
echo "Training with --word_ngrams 5"
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 5

## Testing
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt

```

The results with epoch 30, and play ngrams 2, 3, 5:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-2models.sh
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  37.9% words/sec/thread:  632216 lr:  0.062054 avg.loss:  0.837589 ETA: Progress:  75.9% words/sec/thread:  637307 lr:  0.024115 avg.loss:  0.507291 ETA: Progress: 100.0% words/sec/thread:  561485 lr: -0.000020 avg.loss:  0.418874 ETA: Progress: 100.0% words/sec/thread:  560772 lr:  0.000000 avg.loss:  0.418874 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  45.5% words/sec/thread:  320261 lr:  0.054504 avg.loss:  0.405338 ETA: Progress:  91.4% words/sec/thread:  322945 lr:  0.008633 avg.loss:  0.261803 ETA: Progress: 100.0% words/sec/thread:  235957 lr: -0.000007 avg.loss:  0.246743 ETA: Progress: 100.0% words/sec/thread:  235773 lr:  0.000000 avg.loss:  0.246743 ETA:   0h 0m 0s

real    0m1.846s
user    0m17.952s
sys     0m2.813s
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.672
Short Word Model Accuracy: 0.743

real    0m0.594s
user    0m1.675s
sys     0m2.283s
Training with --word_ngrams 3
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  31.5% words/sec/thread:  525667 lr:  0.068511 avg.loss:  1.064385 ETA: Progress:  62.8% words/sec/thread:  528056 lr:  0.037180 avg.loss:  0.675345 ETA: Progress:  94.1% words/sec/thread:  528465 lr:  0.005929 avg.loss:  0.485843 ETA: Progress: 100.0% words/sec/thread:  421865 lr: -0.000015 avg.loss:  0.469110 ETA: Progress: 100.0% words/sec/thread:  421439 lr:  0.000000 avg.loss:  0.469110 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  40.3% words/sec/thread:  284123 lr:  0.059666 avg.loss:  0.470902 ETA: Progress:  80.7% words/sec/thread:  284399 lr:  0.019317 avg.loss:  0.300377 ETA: Progress: 100.0% words/sec/thread:  235040 lr: -0.000028 avg.loss:  0.252427 ETA: Progress: 100.0% words/sec/thread:  234846 lr:  0.000000 avg.loss:  0.252427 ETA:   0h 0m 0s

real    0m1.982s
user    0m20.610s
sys     0m2.779s
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.686
Short Word Model Accuracy: 0.747

real    0m0.571s
user    0m1.730s
sys     0m2.305s
Training with --word_ngrams 5
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  31.1% words/sec/thread:  516671 lr:  0.068941 avg.loss:  1.178801 ETA: Progress:  62.3% words/sec/thread:  522520 lr:  0.037731 avg.loss:  0.824853 ETA: Progress:  94.0% words/sec/thread:  527494 lr:  0.006004 avg.loss:  0.605173 ETA: Progress: 100.0% words/sec/thread:  421594 lr: -0.000015 avg.loss:  0.578723 ETA: Progress: 100.0% words/sec/thread:  421246 lr:  0.000000 avg.loss:  0.578723 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  55.4% words/sec/thread:  389639 lr:  0.044641 avg.loss:  0.417890 ETA: Progress: 100.0% words/sec/thread:  352724 lr: -0.000029 avg.loss:  0.302633 ETA: Progress: 100.0% words/sec/thread:  352016 lr:  0.000000 avg.loss:  0.302633 ETA:   0h 0m 0s

real    0m1.888s
user    0m18.559s
sys     0m2.851s
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.674
Short Word Model Accuracy: 0.745

real    0m0.597s
user    0m1.624s
sys     0m2.342s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

## Two Model Comparison Code

The code is as follows:  

```python
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat ./two-models.py
"""
Building two fasttext models with two types of input corpus.
Long format is as follows:

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ head -n 3 ltra
in.txt
__label__ab လီး တောင် ရိုးရိုး မ ဟုတ် ဘူး တပတ်လည် လီး ပဲ
__label__ab ဆူ စရာ ရှိ လည်း ကွယ်ရာ မှာ ပြော ပါ လား ကွာ စိတ် နု တဲ့ သူ ဆို ရှက် ပြီး သတ်သေ လောက် တယ် တစ် နိုင်ငံ လုံး မြင် အောင် ပြ နေ ကြ တာ မှား ရင် လည်း မှား မယ် အမှား ဆို အမှန် ကို ထောက်ပြ ပေး မှ ဆရာ ဖြစ် မှာ ခု ဟာ က ဆောက်ရှက်ခွဲ နေ တာ
__label__ab သေခါနီး ရိက္ခာ ယူ နေ ကြ တယ် GL

Short format is as follows:

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/short-data$ shuf ./strain.txt | head
__label__ab အမြင်ကပ် လုပ်
__label__ab စောင်ကြီးစောင်ကျယ် မ လုပ် စောင်ရူး
__label__no ပါတီ မှတ်ပုံတင်ကြေး စပွန်ဆာ ရ သွား တဲ့ ရုပ် ။ 🤮🤮🤮
__label__ab စက်ဖုတ် ရိုက် ဖင်ရိုက် မ
__label__po ဉာဏ်ရည်နိမ့် တောသား ချီးပေါက်
__label__le ဝဋ်တွေလည်ပါစေ သေပြီးလို့လူဘဝပြန်မလာပါစေနဲ့
__label__ab ပဲ မ စောက်ရှက် မ
__label__ab စောက်ရေးမပါ ပဲ အဆင့်တန်းမရှိ
__label__no တကယ့် ဟာ သူ့ အပူ မှ သူ့ အပူ နော်
__label__ab မ ဖော်လော်မ ဆဲ ဆဲ ပဲ

==========

Written by Ye Kyaw Thu, NECTEC, Thailand.
Last updated: 23 Mar 2024
Usage:
python two-models.py --help
"""

import fasttext
import argparse

def train_model(train_data, model_name, epochs=30, lr=0.1, word_ngrams=2, min_count=1, dim=25, neg=10, ws=15, loss='softmax', verbose=3):
    model = fasttext.train_supervised(input=train_data, epoch=epochs, lr=lr, wordNgrams=word_ngrams, minCount=min_count, dim=dim, neg=neg, ws=ws, loss=loss, verbose=verbose)
    model.save_model(model_name)

def test_model(test_data, model_name):
    model = fasttext.load_model(model_name)
    result = model.test(test_data)
    return result[1]

def main(args):
    # Train or load models based on mode
    if args.mode == 'train':
        train_model(args.long_train_data, 'long_sentence_model.bin', epochs=args.epochs, lr=args.lr, word_ngrams=args.word_ngrams, min_count=args.min_count, dim=args.dim, neg=args.neg, ws=args.ws, loss=args.loss, verbose=args.verbose)
        train_model(args.short_train_data, 'short_word_model.bin', epochs=args.epochs, lr=args.lr, word_ngrams=args.word_ngrams, min_count=args.min_count, dim=args.dim, neg=args.neg, ws=args.ws, loss=args.loss, verbose=args.verbose)
    elif args.mode == 'test':
        long_sentence_acc = test_model(args.long_test_data, 'long_sentence_model.bin')
        short_word_acc = test_model(args.short_test_data, 'short_word_model.bin')
        print("Long Sentence Model Accuracy:", long_sentence_acc)
        print("Short Word Model Accuracy:", short_word_acc)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Train or test FastText models for hate speech classification")
    parser.add_argument("--mode", choices=['train', 'test'], help="Mode: train or test")
    parser.add_argument("--long_train_data", help="Path to the training data for long sentence model")
    parser.add_argument("--short_train_data", help="Path to the training data for short word/phrase model")
    parser.add_argument("--long_test_data", help="Path to the testing data for long sentence model")
    parser.add_argument("--short_test_data", help="Path to the testing data for short word/phrase model")
    parser.add_argument("--epochs", type=int, default=30, help="Number of epochs")
    parser.add_argument("--lr", type=float, default=0.1, help="Learning rate")
    parser.add_argument("--word_ngrams", type=int, default=2, help="Max length of word ngram")
    parser.add_argument("--min_count", type=int, default=1, help="Minimal number of word occurences")
    parser.add_argument("--dim", type=int, default=25, help="Size of word vectors")
    parser.add_argument("--neg", type=int, default=10, help="Number of negatives sampled")
    parser.add_argument("--ws", type=int, default=15, help="Size of the context window")
    parser.add_argument("--loss", default='softmax', help="Loss function {ns, hs, softmax}")
    parser.add_argument("--verbose", type=int, default=3, help="Verbose level {0, 1, 2, 3}")
    args = parser.parse_args()

    main(args)

```

## Two Models Results (in Details)

I updated the shell script to show label wise scores ...

```bash
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat ./run-2models.sh
#!/bin/bash

## Training with default parameters
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt

## Testing
echo "Test result with ngram=2:"
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt
echo "labels with precision and recall scores for long model, ngram=2:"
./fastText/fasttext test-label ./long_sentence_model.bin ./long-data/ltest.txt
echo "labels with precision and recall scores for short model, ngram=2:"
./fastText/fasttext test-label ./short_word_model.bin ./short-data/stest.txt

## Training with ngram 3
echo "Training with --word_ngrams 3"
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 3

## Testing
echo "Test result with ngram=3:"
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt
echo "labels with precision and recall scores for long model, ngram=3:"
./fastText/fasttext test-label ./long_sentence_model.bin ./long-data/ltest.txt
echo "labels with precision and recall scores for short model, ngram=3:"
./fastText/fasttext test-label ./short_word_model.bin ./short-data/stest.txt

## Training with ngram 5
echo "Training with --word_ngrams 5"
time python two-models.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 5

## Testing
echo "Test result with ngram=5:"
time python two-models.py --mode test \
--long_test_data ./long-data/ltest.txt \
--short_test_data ./short-data/stest.txt
echo "labels with precision and recall scores for long model, ngram=5:"
./fastText/fasttext test-label ./long_sentence_model.bin ./long-data/ltest.txt
echo "labels with precision and recall scores for short model, ngram=5:"
./fastText/fasttext test-label ./short_word_model.bin ./short-data/stest.txt


```

The results with two models ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-2models.sh
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  40.3% words/sec/thread:  667620 lr:  0.059695 avg.loss:  0.822607 ETA: Progress:  80.2% words/sec/thread:  669528 lr:  0.019826 avg.loss:  0.498255 ETA: Progress: 100.0% words/sec/thread:  558410 lr: -0.000007 avg.loss:  0.430203 ETA: Progress: 100.0% words/sec/thread:  557646 lr:  0.000000 avg.loss:  0.430203 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  40.4% words/sec/thread:  284512 lr:  0.059565 avg.loss:  0.443430 ETA: Progress:  81.9% words/sec/thread:  287086 lr:  0.018057 avg.loss:  0.276226 ETA: Progress: 100.0% words/sec/thread:  234152 lr: -0.000019 avg.loss:  0.238598 ETA: Progress: 100.0% words/sec/thread:  233947 lr:  0.000000 avg.loss:  0.238598 ETA:   0h 0m 0s

real    0m1.856s
user    0m18.529s
sys     0m2.755s
Test result with ngram=2:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.674
Short Word Model Accuracy: 0.74

real    0m0.572s
user    0m1.775s
sys     0m2.203s
labels with precision and recall scores for long model, ngram=2:
F1-Score : 0.807692  Precision : 0.775726  Recall : 0.842407   __label__ab
F1-Score : 0.246154  Precision : 0.163265  Recall : 0.500000   __label__no
F1-Score : 0.413223  Precision : 0.416667  Recall : 0.409836   __label__po
F1-Score : 0.330097  Precision : 0.472222  Recall : 0.253731   __label__bo
F1-Score : 0.090909  Precision : 0.200000  Recall : 0.058824   __label__se
F1-Score : 0.421875  Precision : 0.750000  Recall : 0.293478   __label__le
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ed
F1-Score : --------  Precision : --------  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.674
R@1     0.674
labels with precision and recall scores for short model, ngram=2:
F1-Score : 0.843871  Precision : 0.767606  Recall : 0.936963   __label__ab
F1-Score : 1.000000  Precision : 1.000000  Recall : 1.000000   __label__no
F1-Score : 0.208000  Precision : 0.203125  Recall : 0.213115   __label__po
F1-Score : 0.133333  Precision : 0.625000  Recall : 0.074627   __label__bo
F1-Score : 0.260870  Precision : 0.500000  Recall : 0.176471   __label__se
F1-Score : 0.503937  Precision : 0.914286  Recall : 0.347826   __label__le
F1-Score : 0.064516  Precision : 0.500000  Recall : 0.034483   __label__ed
F1-Score : 0.000000  Precision : 0.000000  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.740
R@1     0.740
Training with --word_ngrams 3
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  31.7% words/sec/thread:  529221 lr:  0.068261 avg.loss:  1.068868 ETA: Progress:  63.3% words/sec/thread:  531401 lr:  0.036742 avg.loss:  0.685651 ETA: Progress:  95.1% words/sec/thread:  533998 lr:  0.004915 avg.loss:  0.491392 ETA: Progress: 100.0% words/sec/thread:  421888 lr: -0.000023 avg.loss:  0.478899 ETA: Progress: 100.0% words/sec/thread:  421473 lr:  0.000000 avg.loss:  0.478899 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  40.0% words/sec/thread:  281483 lr:  0.060005 avg.loss:  0.466191 ETA: Progress:  80.5% words/sec/thread:  284440 lr:  0.019526 avg.loss:  0.306141 ETA: Progress: 100.0% words/sec/thread:  235980 lr: -0.000016 avg.loss:  0.255897 ETA: Progress: 100.0% words/sec/thread:  235804 lr:  0.000000 avg.loss:  0.255897 ETA:   0h 0m 0s

real    0m2.028s
user    0m20.696s
sys     0m2.781s
Test result with ngram=3:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.68
Short Word Model Accuracy: 0.746

real    0m0.575s
user    0m1.764s
sys     0m2.276s
labels with precision and recall scores for long model, ngram=3:
F1-Score : 0.817694  Precision : 0.768262  Recall : 0.873926   __label__ab
F1-Score : 0.245614  Precision : 0.170732  Recall : 0.437500   __label__no
F1-Score : 0.366667  Precision : 0.372881  Recall : 0.360656   __label__po
F1-Score : 0.255319  Precision : 0.444444  Recall : 0.179104   __label__bo
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__se
F1-Score : 0.366667  Precision : 0.785714  Recall : 0.239130   __label__le
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ed
F1-Score : --------  Precision : --------  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.680
R@1     0.680
labels with precision and recall scores for short model, ngram=3:
F1-Score : 0.845809  Precision : 0.764162  Recall : 0.946991   __label__ab
F1-Score : 1.000000  Precision : 1.000000  Recall : 1.000000   __label__no
F1-Score : 0.210526  Precision : 0.226415  Recall : 0.196721   __label__po
F1-Score : 0.133333  Precision : 0.625000  Recall : 0.074627   __label__bo
F1-Score : 0.200000  Precision : 0.666667  Recall : 0.117647   __label__se
F1-Score : 0.503937  Precision : 0.914286  Recall : 0.347826   __label__le
F1-Score : 0.121212  Precision : 0.500000  Recall : 0.068966   __label__ed
F1-Score : --------  Precision : --------  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.746
R@1     0.746
Training with --word_ngrams 5
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  30.6% words/sec/thread:  511863 lr:  0.069360 avg.loss:  1.190327 ETA: Progress:  61.4% words/sec/thread:  515061 lr:  0.038579 avg.loss:  0.826018 ETA: Progress:  92.5% words/sec/thread:  517740 lr:  0.007461 avg.loss:  0.605986 ETA: Progress: 100.0% words/sec/thread:  420592 lr: -0.000010 avg.loss:  0.569288 ETA: Progress: 100.0% words/sec/thread:  420252 lr:  0.000000 avg.loss:  0.569288 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  54.6% words/sec/thread:  384534 lr:  0.045384 avg.loss:  0.452696 ETA: Progress: 100.0% words/sec/thread:  353167 lr: -0.000010 avg.loss:  0.303619 ETA: Progress: 100.0% words/sec/thread:  352546 lr:  0.000000 avg.loss:  0.303619 ETA:   0h 0m 0s

real    0m1.892s
user    0m18.756s
sys     0m2.800s
Test result with ngram=5:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.677
Short Word Model Accuracy: 0.743

real    0m0.577s
user    0m1.761s
sys     0m2.281s
labels with precision and recall scores for long model, ngram=5:
F1-Score : 0.816809  Precision : 0.753939  Recall : 0.891117   __label__ab
F1-Score : 0.252427  Precision : 0.183099  Recall : 0.406250   __label__no
F1-Score : 0.325581  Precision : 0.308824  Recall : 0.344262   __label__po
F1-Score : 0.232558  Precision : 0.526316  Recall : 0.149254   __label__bo
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__se
F1-Score : 0.213592  Precision : 1.000000  Recall : 0.119565   __label__le
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__ed
F1-Score : --------  Precision : --------  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.677
R@1     0.677
labels with precision and recall scores for short model, ngram=5:
F1-Score : 0.848369  Precision : 0.766474  Recall : 0.949857   __label__ab
F1-Score : 1.000000  Precision : 1.000000  Recall : 1.000000   __label__no
F1-Score : 0.206897  Precision : 0.218182  Recall : 0.196721   __label__po
F1-Score : 0.131579  Precision : 0.555556  Recall : 0.074627   __label__bo
F1-Score : 0.200000  Precision : 0.666667  Recall : 0.117647   __label__se
F1-Score : 0.442623  Precision : 0.900000  Recall : 0.293478   __label__le
F1-Score : 0.114286  Precision : 0.333333  Recall : 0.068966   __label__ed
F1-Score : --------  Precision : --------  Recall : --------   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : --------  Precision : --------  Recall : --------   __label__
N       1000
P@1     0.743
R@1     0.743
```

## Ensemble Model  

```python
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat ./run-ensemble.sh
#!/bin/bash

## Training with default parameters
time python ensemble.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt

## Testing
echo "Testing with ltest.txt ..."
time python ensemble.py --mode test --test_data ./long-data/ltest.txt \
--weights 8.0 2.0
echo "Testing with stest.txt ..."
time python ensemble.py --mode test --test_data ./short-data/stest.txt \
--weights 2.0 8.0

## Training with ngram 3
time python ensemble.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 3

## Testing
echo "Testing with ltest.txt ..."
time python ensemble.py --mode test --test_data ./long-data/ltest.txt \
--weights 8.0 2.0
echo "Testing with stest.txt ..."
time python ensemble.py --mode test --test_data ./short-data/stest.txt \
--weights 2.0 8.0

## Training with ngram 5
time python ensemble.py --mode train \
--long_train_data ./long-data/ltrain.txt \
--short_train_data ./short-data/strain.txt --word_ngrams 5

## Testing
echo "Testing with ltest.txt ..."
time python ensemble.py --mode test --test_data ./long-data/ltest.txt \
--weights 8.0 2.0
echo "Testing with stest.txt ..."
time python ensemble.py --mode test --test_data ./short-data/stest.txt \
--weights 2.0 8.0
```

Running with Ensemble Results: 

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-ensemble.sh
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  45.2% words/sec/thread:  752346 lr:  0.054822 avg.loss:  0.770561 ETA: Progress:  90.9% words/sec/thread:  763200 lr:  0.009092 avg.loss:  0.459875 ETA: Progress: 100.0% words/sec/thread:  561243 lr: -0.000009 avg.loss:  0.432221 ETA: Progress: 100.0% words/sec/thread:  560835 lr:  0.000000 avg.loss:  0.432221 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  52.5% words/sec/thread:  369359 lr:  0.047541 avg.loss:  0.359934 ETA: Progress: 100.0% words/sec/thread:  353481 lr: -0.000014 avg.loss:  0.228272 ETA: Progress: 100.0% words/sec/thread:  352835 lr:  0.000000 avg.loss:  0.228272 ETA:   0h 0m 0s

real    0m1.776s
user    0m15.822s
sys     0m2.799s
Testing with ltest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5670000000000001

real    0m0.583s
user    0m1.680s
sys     0m2.367s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7368

real    0m0.599s
user    0m1.807s
sys     0m2.235s
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  39.4% words/sec/thread:  655527 lr:  0.060606 avg.loss:  0.935714 ETA: Progress:  78.7% words/sec/thread:  658891 lr:  0.021288 avg.loss:  0.567798 ETA: Progress: 100.0% words/sec/thread:  559398 lr: -0.000014 avg.loss:  0.479502 ETA: Progress: 100.0% words/sec/thread:  558668 lr:  0.000000 avg.loss:  0.479502 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  52.4% words/sec/thread:  369343 lr:  0.047552 avg.loss:  0.404404 ETA: Progress: 100.0% words/sec/thread:  353609 lr: -0.000049 avg.loss:  0.256094 ETA: Progress: 100.0% words/sec/thread:  353212 lr:  0.000000 avg.loss:  0.256094 ETA:   0h 0m 0s

real    0m1.783s
user    0m16.848s
sys     0m2.802s
Testing with ltest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5680000000000001

real    0m0.579s
user    0m1.753s
sys     0m2.288s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7394000000000001

real    0m0.590s
user    0m1.643s
sys     0m2.314s
Read 0M words
Number of words:  11339
Number of labels: 10
Progress:  30.4% words/sec/thread:  506888 lr:  0.069602 avg.loss:  1.192140 ETA: Progress:  61.1% words/sec/thread:  513530 lr:  0.038876 avg.loss:  0.821282 ETA: Progress:  91.9% words/sec/thread:  516101 lr:  0.008081 avg.loss:  0.598950 ETA: Progress: 100.0% words/sec/thread:  421758 lr: -0.000024 avg.loss:  0.556466 ETA: Progress: 100.0% words/sec/thread:  421509 lr:  0.000000 avg.loss:  0.556466 ETA:   0h 0m 0s
Read 0M words
Number of words:  7858
Number of labels: 10
Progress:  50.6% words/sec/thread:  356263 lr:  0.049397 avg.loss:  0.471675 ETA: Progress: 100.0% words/sec/thread:  353221 lr: -0.000025 avg.loss:  0.303901 ETA: Progress: 100.0% words/sec/thread:  352585 lr:  0.000000 avg.loss:  0.303901 ETA:   0h 0m 0s

real    0m1.883s
user    0m19.257s
sys     0m2.847s
Testing with ltest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5642

real    0m0.586s
user    0m1.752s
sys     0m2.300s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7346

real    0m0.589s
user    0m1.777s
sys     0m2.276s
```

Experiment အနေနဲ့ run လို့တော့ ရသွားပြီ။  
result တွေကို label အလိုက်လည်း ပြနိုင်အောင် shell script မှာ fasttext commandline ကိုသုံးပြီးပြနိုင်အောင် update လုပ်ရလိမ့်မယ်။  

## Found Class Umbalance between Training and Test Data

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ cut -f1 -d " " ./ltrain.txt | sort | uniq | wc
     10      10     118
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ cut -f1 -d " " ./ltest.txt | sort | uniq | wc
      8       8      96
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ cd ..
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cd short-data/
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/short-data$ cut -f1 -d " " ./strain.txt | sort | uniq | wc
     10      10     118
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/short-data$ cut -f1 -d " " ./stest.txt | sort | uniq | wc
      8       8      96
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/short-data$
```

Test data မှာက class ၈မျိုးပဲရှိလို့ test-set အနေနဲ့ မကောင်းဘူး။  

## Resplitting the Training and Testing

Shuffling the whole dataset:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ shuf ./hs_data_Mar19.txt.fasttext.rm-tag > ./hs_data_Mar19.txt.fasttext.rm-tag.shuf
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Preparing for long-data ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head -n 9137 ./hs_data_Mar19.txt.fasttext.rm-tag.shuf > ./long-data/ltrain.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail -n 1000 ./hs_data_Mar19.txt.fasttext.rm-tag.shuf > ./long-data/ltest.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

Preparing for short-data:  

```
python ./filter_hatespeech.py -d hs_dict.txt.uniq \
-i hs_data_Mar19.txt.fasttext.rm-tag.shuf \
-o ./hs_data_Mar19.txt.fasttext.rm-tag.shuf.filtered
```

Splitting training/testing for short-data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ head -n 9137 ./hs_data_Mar19.txt.fasttext.rm-tag.shuf.filtered > ./short-data/strain.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ tail -n 1000 ./hs_data_M
ar19.txt.fasttext.rm-tag.shuf.filtered > ./short-data/stest.txt
```

Check the no. of labes between training and testing ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ cut -f1 -d " " ./ltrain.txt | sort | uniq | wc
     10      10     118
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$ cut -f1 -d " " ./ltest.txt | sort | uniq | wc
     10      10     118
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext/long-data$
```

prepared a bash script for future usage:  

```bash
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat ./chk-labels.sh
#!/bin/bash

cut -f1 -d " " ./long-data/ltrain.txt | sort | uniq | wc
cut -f1 -d " " ./long-data/ltest.txt | sort | uniq | wc

cut -f1 -d " " ./short-data/strain.txt | sort | uniq | wc
cut -f1 -d " " ./short-data/stest.txt | sort | uniq | wc
```

Checking ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./chk-labels.sh
     10      10     118
     10      10     118
     10      10     118
     10      10     118
```

## Final Result for Two-Model Approach

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-2models.sh | tee 2models.result.txt
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  45.2% words/sec/thread:  743864 lr:  0.054818 avg.loss:  0.725350 ETA: Progress:  90.7% words/sec/thread:  750901 lr:  0.009328 avg.loss:  0.435998 ETA: Progress: 100.0% words/sec/thread:  553370 lr: -0.000022 avg.loss:  0.405980 ETA: Progress: 100.0% words/sec/thread:  552651 lr:  0.000000 avg.loss:  0.405980 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  50.4% words/sec/thread:  342992 lr:  0.049609 avg.loss:  0.474351 ETA: Progress: 100.0% words/sec/thread:  341642 lr: -0.000005 avg.loss:  0.272830 ETA: Progress: 100.0% words/sec/thread:  341285 lr:  0.000000 avg.loss:  0.272830 ETA:   0h 0m 0s

real    0m1.804s
user    0m15.831s
sys     0m2.808s
Test result with ngram=2:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.652
Short Word Model Accuracy: 0.759

real    0m0.576s
user    0m1.760s
sys     0m2.281s
labels with precision and recall scores for long model, ngram=2:
F1-Score : 0.777321  Precision : 0.708084  Recall : 0.861566   __label__ab
F1-Score : 0.566845  Precision : 0.563830  Recall : 0.569892   __label__no
F1-Score : 0.526946  Precision : 0.571429  Recall : 0.488889   __label__po
F1-Score : 0.356436  Precision : 0.486486  Recall : 0.281250   __label__bo
F1-Score : 0.285714  Precision : 0.583333  Recall : 0.189189   __label__le
F1-Score : 0.250000  Precision : 0.500000  Recall : 0.166667   __label__se
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ed
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ra
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.652
R@1     0.652
labels with precision and recall scores for short model, ngram=2:
F1-Score : 0.822764  Precision : 0.743025  Recall : 0.921676   __label__ab
F1-Score : 0.997305  Precision : 1.000000  Recall : 0.994624   __label__no
F1-Score : 0.409639  Precision : 0.447368  Recall : 0.377778   __label__po
F1-Score : 0.302326  Precision : 0.590909  Recall : 0.203125   __label__bo
F1-Score : 0.266667  Precision : 0.750000  Recall : 0.162162   __label__le
F1-Score : 0.457143  Precision : 0.727273  Recall : 0.333333   __label__se
F1-Score : 0.066667  Precision : 0.111111  Recall : 0.047619   __label__ed
F1-Score : 0.416667  Precision : 0.714286  Recall : 0.294118   __label__ra
F1-Score : 0.166667  Precision : 1.000000  Recall : 0.090909   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.759
R@1     0.759
Training with --word_ngrams 3
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  37.9% words/sec/thread:  621895 lr:  0.062055 avg.loss:  0.875632 ETA: Progress:  76.3% words/sec/thread:  630369 lr:  0.023714 avg.loss:  0.557171 ETA: Progress: 100.0% words/sec/thread:  552516 lr: -0.000018 avg.loss:  0.456778 ETA: Progress: 100.0% words/sec/thread:  551928 lr:  0.000000 avg.loss:  0.456778 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  50.8% words/sec/thread:  345248 lr:  0.049186 avg.loss:  0.444305 ETA: Progress: 100.0% words/sec/thread:  341443 lr: -0.000029 avg.loss:  0.271576 ETA: Progress: 100.0% words/sec/thread:  341076 lr:  0.000000 avg.loss:  0.271576 ETA:   0h 0m 0s

real    0m1.796s
user    0m17.262s
sys     0m2.690s
Test result with ngram=3:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.634
Short Word Model Accuracy: 0.771

real    0m0.580s
user    0m1.762s
sys     0m2.282s
labels with precision and recall scores for long model, ngram=3:
F1-Score : 0.760357  Precision : 0.686217  Recall : 0.852459   __label__ab
F1-Score : 0.558011  Precision : 0.573864  Recall : 0.543011   __label__no
F1-Score : 0.488372  Precision : 0.512195  Recall : 0.466667   __label__po
F1-Score : 0.309278  Precision : 0.454545  Recall : 0.234375   __label__bo
F1-Score : 0.244898  Precision : 0.500000  Recall : 0.162162   __label__le
F1-Score : 0.129032  Precision : 0.285714  Recall : 0.083333   __label__se
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ed
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.634
R@1     0.634
labels with precision and recall scores for short model, ngram=3:
F1-Score : 0.831065  Precision : 0.741429  Recall : 0.945355   __label__ab
F1-Score : 0.997305  Precision : 1.000000  Recall : 0.994624   __label__no
F1-Score : 0.427673  Precision : 0.492754  Recall : 0.377778   __label__po
F1-Score : 0.289157  Precision : 0.631579  Recall : 0.187500   __label__bo
F1-Score : 0.272727  Precision : 0.857143  Recall : 0.162162   __label__le
F1-Score : 0.437500  Precision : 0.875000  Recall : 0.291667   __label__se
F1-Score : 0.076923  Precision : 0.200000  Recall : 0.047619   __label__ed
F1-Score : 0.521739  Precision : 1.000000  Recall : 0.352941   __label__ra
F1-Score : 0.166667  Precision : 1.000000  Recall : 0.090909   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.771
R@1     0.771
Training with --word_ngrams 5
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  30.4% words/sec/thread:  499922 lr:  0.069572 avg.loss:  1.101689 ETA: Progress:  61.0% words/sec/thread:  504203 lr:  0.039029 avg.loss:  0.743842 ETA: Progress:  91.6% words/sec/thread:  506243 lr:  0.008371 avg.loss:  0.562258 ETA: Progress: 100.0% words/sec/thread:  415018 lr: -0.000020 avg.loss:  0.529506 ETA: Progress: 100.0% words/sec/thread:  414618 lr:  0.000000 avg.loss:  0.529506 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  49.2% words/sec/thread:  334678 lr:  0.050810 avg.loss:  0.488723 ETA: Progress:  98.4% words/sec/thread:  336245 lr:  0.001562 avg.loss:  0.288436 ETA: Progress: 100.0% words/sec/thread:  228062 lr: -0.000030 avg.loss:  0.285249 ETA: Progress: 100.0% words/sec/thread:  227783 lr:  0.000000 avg.loss:  0.285249 ETA:   0h 0m 0s

real    0m1.974s
user    0m19.374s
sys     0m2.948s
Test result with ngram=5:
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Long Sentence Model Accuracy: 0.63
Short Word Model Accuracy: 0.766

real    0m0.583s
user    0m1.837s
sys     0m2.208s
labels with precision and recall scores for long model, ngram=5:
F1-Score : 0.764800  Precision : 0.681883  Recall : 0.870674   __label__ab
F1-Score : 0.494253  Precision : 0.530864  Recall : 0.462366   __label__no
F1-Score : 0.500000  Precision : 0.489362  Recall : 0.511111   __label__po
F1-Score : 0.307692  Precision : 0.518519  Recall : 0.218750   __label__bo
F1-Score : 0.217391  Precision : 0.555556  Recall : 0.135135   __label__le
F1-Score : 0.071429  Precision : 0.250000  Recall : 0.041667   __label__se
F1-Score : 0.000000  Precision : 0.000000  Recall : 0.000000   __label__ed
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__ra
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.630
R@1     0.630
labels with precision and recall scores for short model, ngram=5:
F1-Score : 0.826539  Precision : 0.736467  Recall : 0.941712   __label__ab
F1-Score : 0.997305  Precision : 1.000000  Recall : 0.994624   __label__no
F1-Score : 0.405229  Precision : 0.492063  Recall : 0.344444   __label__po
F1-Score : 0.271605  Precision : 0.647059  Recall : 0.171875   __label__bo
F1-Score : 0.272727  Precision : 0.857143  Recall : 0.162162   __label__le
F1-Score : 0.444444  Precision : 0.666667  Recall : 0.333333   __label__se
F1-Score : 0.074074  Precision : 0.166667  Recall : 0.047619   __label__ed
F1-Score : 0.434783  Precision : 0.833333  Recall : 0.294118   __label__ra
F1-Score : 0.307692  Precision : 1.000000  Recall : 0.181818   __label__re
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__
N       1000
P@1     0.766
R@1     0.766
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$
```

## Updating the Ensemble Python code

```python
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ cat ./ensemble.py
"""
For ensembling two fasttext models.
Written by Ye Kyaw Thu, NECTEC, Thailand.
Last updated: 23 Mar 2024
Usage:
python ./ensemble.py --help
"""

import fasttext
import argparse

def train_model(train_data, model_name, epochs=30, lr=0.1, word_ngrams=2, min_count=1, dim=25, neg=10, ws=15, loss='softmax', verbose=3):
    model = fasttext.train_supervised(input=train_data, epoch=epochs, lr=lr, wordNgrams=word_ngrams, minCount=min_count, dim=dim, neg=neg, ws=ws, loss=loss, verbose=verbose)
    model.save_model(model_name)

def test_model(test_data, model_name):
    model = fasttext.load_model(model_name)
    result = model.test(test_data)
    return result[1]

def ensemble_test(long_model, short_model, test_data, weights):
    long_model_acc = test_model(test_data, long_model)
    short_model_acc = test_model(test_data, short_model)
    ensemble_acc = (weights[0] * long_model_acc + weights[1] * short_model_acc) / sum(weights)
    return ensemble_acc

def main(args):
    # Train or load models based on mode
    if args.mode == 'train':
        train_model(args.long_train_data, 'long_sentence_model.bin', epochs=args.epochs, lr=args.lr, word_ngrams=args.word_ngrams, min_count=args.min_count, dim=args.dim, neg=args.neg, ws=args.ws, loss=args.loss, verbose=args.verbose)
        train_model(args.short_train_data, 'short_word_model.bin', epochs=args.epochs, lr=args.lr, word_ngrams=args.word_ngrams, min_count=args.min_count, dim=args.dim, neg=args.neg, ws=args.ws, loss=args.loss, verbose=args.verbose)
    elif args.mode == 'test':
        ensemble_acc = ensemble_test('long_sentence_model.bin', 'short_word_model.bin', args.test_data, args.weights)
        print("Ensemble Model Accuracy:", ensemble_acc)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Train or test FastText models for hate speech classification")
    parser.add_argument("--mode", choices=['train', 'test'], help="Mode: train or test")
    parser.add_argument("--long_train_data", help="Path to the training data for long sentence model")
    parser.add_argument("--short_train_data", help="Path to the training data for short word/phrase model")
    parser.add_argument("--test_data", help="Path to the testing data")
    parser.add_argument("--epochs", type=int, default=30, help="Number of epochs")
    parser.add_argument("--lr", type=float, default=0.1, help="Learning rate")
    parser.add_argument("--word_ngrams", type=int, default=2, help="Max length of word ngram")
    parser.add_argument("--min_count", type=int, default=1, help="Minimal number of word occurences")
    parser.add_argument("--dim", type=int, default=25, help="Size of word vectors")
    parser.add_argument("--neg", type=int, default=10, help="Number of negatives sampled")
    parser.add_argument("--ws", type=int, default=15, help="Size of the context window")
    parser.add_argument("--loss", default='softmax', help="Loss function {ns, hs, softmax}")
    parser.add_argument("--verbose", type=int, default=3, help="Verbose level {0, 1, 2, 3}")
    parser.add_argument("--weights", nargs='+', type=float, default=[1.0, 1.0], help="Weights for ensemble testing")
    args = parser.parse_args()

    main(args)

```

## Final Result for Ensemble Approach  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/hs-fasttext$ ./run-ensemble.sh | tee ensemble.result.txt
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  40.5% words/sec/thread:  665946 lr:  0.059528 avg.loss:  0.776064 ETA: Progress:  81.0% words/sec/thread:  669467 lr:  0.018959 avg.loss:  0.480156 ETA: Progress: 100.0% words/sec/thread:  551608 lr: -0.000022 avg.loss:  0.409747 ETA: Progress: 100.0% words/sec/thread:  551220 lr:  0.000000 avg.loss:  0.409747 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  42.5% words/sec/thread:  289261 lr:  0.057484 avg.loss:  0.515708 ETA: Progress:  84.8% words/sec/thread:  289836 lr:  0.015163 avg.loss:  0.322966 ETA: Progress: 100.0% words/sec/thread:  228089 lr: -0.000023 avg.loss:  0.285641 ETA: Progress: 100.0% words/sec/thread:  227886 lr:  0.000000 avg.loss:  0.285641 ETA:   0h 0m 0s

real    0m1.856s
user    0m18.006s
sys     0m2.832s
Testing with ltest.txt --weights 8.0, 2.0 ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5712

real    0m0.573s
user    0m1.761s
sys     0m2.277s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7434000000000001

real    0m0.600s
user    0m1.701s
sys     0m2.292s
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  35.4% words/sec/thread:  581550 lr:  0.064613 avg.loss:  0.909102 ETA: Progress:  70.9% words/sec/thread:  586235 lr:  0.029147 avg.loss:  0.570265 ETA: Progress: 100.0% words/sec/thread:  552927 lr: -0.000012 avg.loss:  0.449354 ETA: Progress: 100.0% words/sec/thread:  552400 lr:  0.000000 avg.loss:  0.449354 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  38.6% words/sec/thread:  262409 lr:  0.061413 avg.loss:  0.555494 ETA: Progress:  77.2% words/sec/thread:  263678 lr:  0.022809 avg.loss:  0.342644 ETA: Progress: 100.0% words/sec/thread:  227594 lr: -0.000014 avg.loss:  0.279735 ETA: Progress: 100.0% words/sec/thread:  227295 lr:  0.000000 avg.loss:  0.279735 ETA:   0h 0m 0s

real    0m1.848s
user    0m19.867s
sys     0m2.750s
Testing with ltest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5544

real    0m0.575s
user    0m1.790s
sys     0m2.250s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7445999999999999

real    0m0.585s
user    0m1.760s
sys     0m2.289s
Read 0M words
Number of words:  11409
Number of labels: 10
Progress:  28.9% words/sec/thread:  473318 lr:  0.071072 avg.loss:  1.138251 ETA: Progress:  57.9% words/sec/thread:  476731 lr:  0.042103 avg.loss:  0.779736 ETA: Progress:  87.0% words/sec/thread:  478580 lr:  0.013032 avg.loss:  0.590322 ETA: Progress: 100.0% words/sec/thread:  413641 lr: -0.000021 avg.loss:  0.539521 ETA: Progress: 100.0% words/sec/thread:  413294 lr:  0.000000 avg.loss:  0.539521 ETA:   0h 0m 0s
Read 0M words
Number of words:  7855
Number of labels: 10
Progress:  38.9% words/sec/thread:  264804 lr:  0.061054 avg.loss:  0.548662 ETA: Progress:  77.8% words/sec/thread:  264892 lr:  0.022220 avg.loss:  0.347601 ETA: Progress: 100.0% words/sec/thread:  227171 lr: -0.000022 avg.loss:  0.284916 ETA: Progress: 100.0% words/sec/thread:  226907 lr:  0.000000 avg.loss:  0.284916 ETA:   0h 0m 0s

real    0m2.004s
user    0m21.787s
sys     0m2.793s
Testing with ltest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.5472

real    0m0.582s
user    0m1.771s
sys     0m2.273s
Testing with stest.txt ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Ensemble Model Accuracy: 0.7456

real    0m0.589s
user    0m1.817s
sys     0m2.233s
```

FIN! 
