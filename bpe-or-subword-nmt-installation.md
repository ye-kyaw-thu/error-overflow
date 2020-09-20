## Installation

git clone လုပ်ပြီး ကိုယ့်စက်ထဲကို repository ကို ကော်ပီကူးယူတယ် 

```
(base) ye@ykt-pro:~/tool$ git clone https://github.com/rsennrich/subword-nmt
Cloning into 'subword-nmt'...
remote: Enumerating objects: 576, done.
remote: Total 576 (delta 0), reused 0 (delta 0), pack-reused 576
Receiving objects: 100% (576/576), 233.30 KiB | 254.00 KiB/s, done.
Resolving deltas: 100% (349/349), done.
```

Folder အထဲကို ဝင်ကြည့်ရအောင်    

```
(base) ye@ykt-pro:~/tool$ cd subword-nmt/
(base) ye@ykt-pro:~/tool/subword-nmt$ ls
apply_bpe.py  get_vocab.py  learn_joint_bpe_and_vocab.py  README.md  subword_nmt
CHANGELOG.md  learn_bpe.py  LICENSE                       setup.py
```

setup.py ကို သုံးပြီးတော့ install လုပ်မယ်...  

```
(base) ye@ykt-pro:~/tool/subword-nmt$ python ./setup.py install
running install
running bdist_egg
running egg_info
creating subword_nmt.egg-info
writing subword_nmt.egg-info/PKG-INFO
writing dependency_links to subword_nmt.egg-info/dependency_links.txt
writing entry points to subword_nmt.egg-info/entry_points.txt
writing top-level names to subword_nmt.egg-info/top_level.txt
writing manifest file 'subword_nmt.egg-info/SOURCES.txt'
reading manifest file 'subword_nmt.egg-info/SOURCES.txt'
writing manifest file 'subword_nmt.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/subword_nmt
copying subword_nmt/__init__.py -> build/lib/subword_nmt
copying subword_nmt/bpe_toy.py -> build/lib/subword_nmt
copying subword_nmt/apply_bpe.py -> build/lib/subword_nmt
copying subword_nmt/subword_nmt.py -> build/lib/subword_nmt
copying subword_nmt/learn_bpe.py -> build/lib/subword_nmt
copying subword_nmt/learn_joint_bpe_and_vocab.py -> build/lib/subword_nmt
copying subword_nmt/get_vocab.py -> build/lib/subword_nmt
copying subword_nmt/chrF.py -> build/lib/subword_nmt
copying subword_nmt/segment_char_ngrams.py -> build/lib/subword_nmt
creating build/lib/subword_nmt/tests
copying subword_nmt/tests/__init__.py -> build/lib/subword_nmt/tests
copying subword_nmt/tests/test_glossaries.py -> build/lib/subword_nmt/tests
copying subword_nmt/tests/test_bpe.py -> build/lib/subword_nmt/tests
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/__init__.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/bpe_toy.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/apply_bpe.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/subword_nmt.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/learn_bpe.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/learn_joint_bpe_and_vocab.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/get_vocab.py -> build/bdist.linux-x86_64/egg/subword_nmt
creating build/bdist.linux-x86_64/egg/subword_nmt/tests
copying build/lib/subword_nmt/tests/__init__.py -> build/bdist.linux-x86_64/egg/subword_nmt/tests
copying build/lib/subword_nmt/tests/test_glossaries.py -> build/bdist.linux-x86_64/egg/subword_nmt/tests
copying build/lib/subword_nmt/tests/test_bpe.py -> build/bdist.linux-x86_64/egg/subword_nmt/tests
copying build/lib/subword_nmt/chrF.py -> build/bdist.linux-x86_64/egg/subword_nmt
copying build/lib/subword_nmt/segment_char_ngrams.py -> build/bdist.linux-x86_64/egg/subword_nmt
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/bpe_toy.py to bpe_toy.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/apply_bpe.py to apply_bpe.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/subword_nmt.py to subword_nmt.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/learn_bpe.py to learn_bpe.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/learn_joint_bpe_and_vocab.py to learn_joint_bpe_and_vocab.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/get_vocab.py to get_vocab.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/tests/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/tests/test_glossaries.py to test_glossaries.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/tests/test_bpe.py to test_bpe.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/chrF.py to chrF.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/subword_nmt/segment_char_ngrams.py to segment_char_ngrams.cpython-37.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying subword_nmt.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying subword_nmt.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying subword_nmt.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying subword_nmt.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying subword_nmt.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
creating dist
creating 'dist/subword_nmt-0.3.7-py3.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing subword_nmt-0.3.7-py3.7.egg
Copying subword_nmt-0.3.7-py3.7.egg to /home/ye/tool/anaconda3/lib/python3.7/site-packages
Adding subword-nmt 0.3.7 to easy-install.pth file
Installing subword-nmt script to /home/ye/tool/anaconda3/bin

Installed /home/ye/tool/anaconda3/lib/python3.7/site-packages/subword_nmt-0.3.7-py3.7.egg
Processing dependencies for subword-nmt==0.3.7
Finished processing dependencies for subword-nmt==0.3.7
(base) ye@ykt-pro:~/tool/subword-nmt$ ls
apply_bpe.py  CHANGELOG.md  get_vocab.py  learn_joint_bpe_and_vocab.py  README.md  subword_nmt
build         dist          learn_bpe.py  LICENSE                       setup.py   subword_nmt.egg-info
```

*** Installation က pip install နဲ့လည်း လုပ်လို့ရတယ်။

## Build Syllable based BPE Units

Syllable ဖြတ်ထားတဲ့ ဒေတာနဲ့ BPE unit build လုပ်တာ

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ head big-lm2.my.syl.clean 
မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
သူ မ ဘယ် သူ့ ကို မှ မ မှတ် မိ တော့ ဘူး ။
အဲ့ ဒါ ကျွန် တော် တို့ အ တွက် ခက် ခဲ တယ် ။
ခင် ဗျား ပြော ခဲ့ သ လို ကျွန် တော် ရှင်း ပြ ခဲ့ တယ် ။
သူ့ ကို ထိန်း ဖို့ မင်း ပဲ တတ် နိုင် တယ် ။
အဲ့ ဒါ ကို ကိုယ် တက် နင်း မိ သွား လား ။
ငါ စဉ်း စား သ လို စဉ်း စား ပါ ။
အ တင်း ပြော ရ တာ မုန်း တယ် ။
 နောက် ဆုံး တစ် ကြိမ် သူ့ ကို ချစ် ပါ တယ် လို့ ပြော ခွ င့် တောင် မ ရ တော့ ဘူး ။
နာ ဆာ မှ ဒုံး ပျံ စ တက် တာ နဲ့ သူ မှတ် တမ်း ရေး ခဲ့ တယ် ။
```

BPE Unit ကို တခြား ဘာ parameter မှ မပေးတော့ပဲ ရိုးရိုးလေးဆောက်မယ်ဆိုရင်  
Python script နဲ့ပဲ run ကြည့်ကြရအောင်   

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ time python ./learn_bpe.py -i ./y-test/big-lm2.my -o ./y-test/big-lm2.syl.bpe-model

real	0m16.046s
user	0m15.895s
sys	0m0.148s
```

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ ls ./y-test/
big-lm2.my  big-lm2.my.syl.clean  big-lm2.syl.bpe-model
```

မော်ဒယ်ဖိုင် အထဲကို ကြည့်ကြည့်ရအောင်   

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ head -20 ./big-lm2.syl.bpe-model 
#version: 0.2
ေ ာ
င ်
 ု
ယ ်</w>
ာ း</w>
န ်
တ ယ်</w>
 ု</w>
က ်</w>
 ့</w>
င ်</w>
က ျ
ပ ါ</w>
င် း</w>
ပ ြ
စ ်</w>
တ ော
မ ှ
က ို</w>
```

## Segmenting with Syllable based BPE

test ဖိုင် နံပါတ်၁ က အောက်ပါအတိုင်း  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat test1.txt 
မင်း ကို ငါ ဘယ်လို ခေါ် ရ မ လဲ
စာ တော် တဲ့ ကျောင်း သူ တစ် ယောက် ပါ
အ ရမ်း ဆော့ တဲ့ ကလေး က ကျန်း မာ တယ်
အခု တော့ ပါ နက် ဆ ရာ ဟာ စက် တင် ဘာ လ ၁၉ ရက် နေ့ မှာ ဆန္ဒ ပြ ပွဲ ကျင်း ပ ဖို့ အ တွက် ပြင် ဆင် နေ ပါ တယ် ။
ဘတ်စ် ကား စီး ပြီး ရုံး တက် တဲ့ ဘိလပ် ပြန် ညွှန် ကြား ရေး မှူး ချုပ်
```

test1.txt ဖိုင်ကို BPE နဲ့ ဖြတ်ခိုင်းကြည့်ရအောင်  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ python ../apply_bpe.py -i ./test1.txt -c ./big-lm2.syl.bpe-model -o ./test1.bpe
```

ထွက်လာတဲ့ output က အောက်ပါအတိုင်း   
မြန်မာစာအတွက် syllable unite က strong ဖြစ်ပြီးသားပါ။  
```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test1.bpe 
မင်း ကို ငါ ဘယ်လို ခေါ် ရ မ လဲ
စာ တော် တဲ့ ကျောင်း သူ တစ် ယောက် ပါ
အ ရမ်း ဆော့ တဲ့ ကလေး က ကျန်း မာ တယ်
အခု တော့ ပါ နက် ဆ ရာ ဟာ စက် တင် ဘာ လ ၁၉ ရက် နေ့ မှာ ဆန္ဒ ပြ ပွဲ ကျင်း ပ ဖို့ အ တွက် ပြင် ဆင် နေ ပါ တယ် ။
ဘတ်စ် ကား စီး ပြီး ရုံး တက် တဲ့ ဘိ@@ လပ် ပြန် ညွှန် ကြား ရေး မှူး ချုပ်
```
နောက်ထပ် test ဖိုင် တစ်ဖိုင်ကို BBC မြန်မာရဲ့သတင်း website ကနေ စာကြောင်းတချို့ကို ယူပြီး အောက်ပါအတိုင်း ပြင်ခဲ့တယ်။
syllable segmentation လည်းမလုပ်ထားပဲ အရင်စမ်းကြည့်ရအောင်။  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test2.raw
နိုင်ငံတခု ထူထောင်တဲ့အခါမှာ စစ်တပ်၊ စီးပွားရေးလုပ်ငန်းတွေနဲ့ တရားရုံးစတဲ့ ပင်မအဖွဲ့အစည်းတွေသာမက စာပေ ယဉ်ကျေးမှု စိတ်ဓာတ်ပိုင်းကလည်း နိုင်ငံသိစိတ် ချစ်စိတ်တွေ ပေါ်လာအောင် ဆော်ဩ ပေးရပါတယ်။ ဒါကိုသိတဲ့ လူကြီးပိုင်းက မြန်မာပြည်အတွက် ပြတိုက် စာကြည့်တိုက်နဲ့ အနုပညာတိုက်တွေ ရှိဖို့လိုတဲ့အကြောင်း ကိုလိုနီခေတ်ကစပြီး တိုက်တွန်းခဲ့ကြသလို ဒီယဉ်ကျေးမှု အဆောက်အဦတွေကို ကွပ်ကဲဖို့ အတွက် ပညာရှင်တွေ ပေါ်ထွက်ဖို့လည်း ကမ္ဘာစစ် မဖြစ်ခင်ကတည်းက စိုင်းပြင်းခဲ့ကြပါတယ်။ ဒါကြောင့် ဦးခင်ဇော်နဲ့ ဦးသိန်းဟန်ကို ပိဋကတ်တိုက်ပညာလို့ ခေါ်တဲ့ စာကြည့်တိုက်လုပ်ငန်းအတွက် ဗြိတိန်ကို စေလွှတ်ခဲ့ သလို ပန်းချီပညာသင်အဖြစ် ဦးဘဉာဏ်နဲ့ ဦးဘဇော်ကိုလည်း ဒီ့အရင်ကတည်းက လန်ဒန်ကို ပို့ခဲ့ပါတယ်။

ဒါပေမဲ့ ကိုလိုနီခေတ်မြန်မာနိုင်ငံမှာ အဲဒီအချိန်ထိ အမျိုးသားစာကြည့်တိုက်နဲ့ ပြတိုက်၊ အနုပညာပြခန်းတွေ မရှိသေးဘဲ ရန်ကုန် တက္ကသိုလ် ပိဋကတ်တိုက်နဲ့ ရန်ကုန်မြို့ထဲက ဗားနတ်ပိဋကတ်တိုက်နဲ့ ပြတိုက်အပြင် ပြည်နားက မှော်ဇာ၊ ရခိုင်က မြောက်ဦးနဲ့ အညာက ပုဂံ၊ ရွှေဘိုနဲ့ မန္တလေးမှာ ကမ္ပည်းကျောက်စာဌာန ပြတိုက်ကလေးတွေပဲ ရှိခဲ့ပါတယ်။
```

Syllable BPE unit အတိုင်း ဖြတ်ကြည့်ခဲ့တော့ အောက်ပါ output ကို ရခဲ့တယ်။  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ python ../apply_bpe.py -c ./big-lm2.syl.bpe-model -i ./test2.raw 
နိုင်ငံ@@ တ@@ ခု ထူထောင်@@ တဲ့@@ အခါမှာ စစ်@@ တပ်@@ ၊ စီးပွားရေး@@ လုပ်ငန်း@@ တွေ@@ နဲ့ တရား@@ ရုံး@@ စတဲ့ ပင်@@ မ@@ အဖွဲ့@@ အစည်း@@ တွေ@@ သာမက စာပေ ယဉ်ကျေးမှု စိတ်ဓာတ်@@ ပိုင်း@@ ကလည်း နိုင်ငံ@@ သိ@@ စိတ် ချစ်@@ စိတ်@@ တွေ ပေါ်@@ လာ@@ အောင် ဆော်@@ ဩ ပေး@@ ရ@@ ပါ@@ တယ်။ ဒါ@@ ကို@@ သိ@@ တဲ့ လူကြီး@@ ပိုင်း@@ က မြန်မာ@@ ပြည်@@ အတွက် ပြတိုက် စာကြည့်@@ တိုက်@@ နဲ့ အနုပညာ@@ တိုက်@@ တွေ ရှိ@@ ဖို့@@ လို@@ တဲ့@@ အကြောင်း ကိုလို@@ နီ@@ ခေတ်@@ က@@ စပြီး တိုက်@@ တွန်း@@ ခဲ့ကြ@@ သလို ဒီ@@ ယဉ်ကျေးမှု အဆောက်အ@@ ဦ@@ တွေကို ကွ@@ ပ်@@ ကဲ@@ ဖို့ အတွက် ပညာ@@ ရှင်@@ တွေ ပေါ်@@ ထွက်@@ ဖို့@@ လည်း ကမ္ဘာ@@ စစ် မဖြစ်@@ ခင်@@ ကတည်းက စိုင်း@@ ပြင်း@@ ခဲ့ကြ@@ ပါ@@ တယ်။ ဒါကြောင့် ဦး@@ ခင်@@ ဇော်@@ နဲ့ ဦး@@ သိန်း@@ ဟန်@@ ကို ပိ@@ ဋ@@ ကတ်@@ တိုက်@@ ပညာ@@ လို့ ခေါ်@@ တဲ့ စာကြည့်@@ တိုက်@@ လုပ်ငန်း@@ အတွက် ဗြိတိ@@ န်@@ ကို စေ@@ လွှတ်@@ ခဲ့ သလို ပန်းချီ@@ ပညာသင်@@ အဖြစ် ဦး@@ ဘ@@ ဉာဏ်@@ နဲ့ ဦး@@ ဘ@@ ဇော်@@ ကိုလည်း ဒီ@@ ့@@ အရင်@@ ကတည်းက လန်@@ ဒန်@@ ကို ပို့@@ ခဲ့@@ ပါ@@ တယ်။

ဒါပေမဲ့ ကိုလို@@ နီ@@ ခေတ်@@ မြန်မာ@@ နိုင်ငံ@@ မှာ အဲဒီ@@ အချိန်@@ ထိ အမျိုးသား@@ စာကြည့်@@ တိုက်@@ နဲ့ ပြ@@ တိုက်@@ ၊ အနုပညာ@@ ပြ@@ ခန်း@@ တွေ မရှိ@@ သေး@@ ဘဲ ရန်ကုန် တက္ကသိုလ် ပိ@@ ဋ@@ ကတ်@@ တိုက်@@ နဲ့ ရန်@@ ကုန်@@ မြို့@@ ထဲက ဗား@@ နတ်@@ ပိ@@ ဋ@@ ကတ်@@ တိုက်@@ နဲ့ ပြ@@ တိုက်@@ အပြင် ပြည်@@ နား@@ က မှ@@ ော်@@ ဇာ@@ ၊ ရ@@ ခိုင်@@ က မြောက်@@ ဦး@@ နဲ့ အ@@ ညာ@@ က ပုဂံ@@ ၊ ရွှေ@@ ဘို@@ နဲ့ မန္တ@@ လေး@@ မှာ ကမ္@@ ပ@@ ည်း@@ ကျောက်@@ စာ@@ ဌာန ပြ@@ တိုက်@@ ကလေး@@ တွေ@@ ပဲ ရှိ@@ ခဲ့@@ ပါ@@ တယ်။
```

အဓိက ကတော့ segmentation မလုပ်ထားတဲ့ဒေတာကို input လုပ်တဲ့အခါမျိုးမှာ apply ကောင်းကောင်းဖြစ်တဲ့ပုံရှိတယ်။  

ဒီတစ်ခါတော့ syllable ဖြတ်ပြီးမှာ BPE unit ပြောင်းတာကို လုပ်ကြည့်ချင်တယ်။  
syllable မဖြတ်ခင်မှာ ရှိနေတဲ့ space တွေကို ဖျက်လိုက်ကြရအောင် ...   

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ sed 's/ //g' ./test2.raw > test2.raw.nospace
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test2.raw.nospace 
နိုင်ငံတခုထူထောင်တဲ့အခါမှာစစ်တပ်၊စီးပွားရေးလုပ်ငန်းတွေနဲ့တရားရုံးစတဲ့ပင်မအဖွဲ့အစည်းတွေသာမကစာပေယဉ်ကျေးမှုစိတ်ဓာတ်ပိုင်းကလည်းနိုင်ငံသိစိတ်ချစ်စိတ်တွေပေါ်လာအောင်ဆော်ဩပေးရပါတယ်။ဒါကိုသိတဲ့လူကြီးပိုင်းကမြန်မာပြည်အတွက်ပြတိုက်စာကြည့်တိုက်နဲ့အနုပညာတိုက်တွေရှိဖို့လိုတဲ့အကြောင်းကိုလိုနီခေတ်ကစပြီးတိုက်တွန်းခဲ့ကြသလိုဒီယဉ်ကျေးမှုအဆောက်အဦတွေကိုကွပ်ကဲဖို့အတွက်ပညာရှင်တွေပေါ်ထွက်ဖို့လည်းကမ္ဘာစစ်မဖြစ်ခင်ကတည်းကစိုင်းပြင်းခဲ့ကြပါတယ်။ဒါကြောင့်ဦးခင်ဇော်နဲ့ဦးသိန်းဟန်ကိုပိဋကတ်တိုက်ပညာလို့ခေါ်တဲ့စာကြည့်တိုက်လုပ်ငန်းအတွက်ဗြိတိန်ကိုစေလွှတ်ခဲ့သလိုပန်းချီပညာသင်အဖြစ်ဦးဘဉာဏ်နဲ့ဦးဘဇော်ကိုလည်းဒီ့အရင်ကတည်းကလန်ဒန်ကိုပို့ခဲ့ပါတယ်။

ဒါပေမဲ့ကိုလိုနီခေတ်မြန်မာနိုင်ငံမှာအဲဒီအချိန်ထိအမျိုးသားစာကြည့်တိုက်နဲ့ပြတိုက်၊အနုပညာပြခန်းတွေမရှိသေးဘဲရန်ကုန်တက္ကသိုလ်ပိဋကတ်တိုက်နဲ့ရန်ကုန်မြို့ထဲကဗားနတ်ပိဋကတ်တိုက်နဲ့ပြတိုက်အပြင်ပြည်နားကမှော်ဇာ၊ရခိုင်ကမြောက်ဦးနဲ့အညာကပုဂံ၊ရွှေဘိုနဲ့မန္တလေးမှာကမ္ပည်းကျောက်စာဌာနပြတိုက်ကလေးတွေပဲရှိခဲ့ပါတယ်။
```

syllable segmentation ဖြတ်မယ်  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ perl ./sylbreak.pl -i ./test2.raw.nospace -s " " > test2.raw.nospace.syl
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test2.raw.nospace.syl 
 နိုင် ငံ တ ခု ထူ ထောင် တဲ့ အ ခါ မှာ စစ် တပ် ၊ စီး ပွား ရေး လုပ် ငန်း တွေ နဲ့ တ ရား ရုံး စ တဲ့ ပင် မ အ ဖွဲ့ အ စည်း တွေ သာ မ က စာ ပေ ယဉ် ကျေး မှု စိတ် ဓာတ် ပိုင်း က လည်း နိုင် ငံ သိ စိတ် ချစ် စိတ် တွေ ပေါ် လာ အောင် ဆော် ဩ ပေး ရ ပါ တယ် ။ ဒါ ကို သိ တဲ့ လူ ကြီး ပိုင်း က မြန် မာ ပြည် အ တွက် ပြ တိုက် စာ ကြ ည့် တိုက် နဲ့ အ နု ပ ညာ တိုက် တွေ ရှိ ဖို့ လို တဲ့ အ ကြောင်း ကို လို နီ ခေတ် က စ ပြီး တိုက် တွန်း ခဲ့ ကြ သ လို ဒီ ယဉ် ကျေး မှု အ ဆောက် အ ဦ တွေ ကို ကွပ် ကဲ ဖို့ အ တွက် ပ ညာ ရှင် တွေ ပေါ် ထွက် ဖို့ လည်း ကမ္ဘာ စစ် မ ဖြစ် ခင် က တည်း က စိုင်း ပြင်း ခဲ့ ကြ ပါ တယ် ။ ဒါ ကြော င့် ဦး ခင် ဇော် နဲ့ ဦး သိန်း ဟန် ကို ပိ ဋ ကတ် တိုက် ပ ညာ လို့ ခေါ် တဲ့ စာ ကြ ည့် တိုက် လုပ် ငန်း အ တွက် ဗြိ တိန် ကို စေ လွှတ် ခဲ့ သ လို ပန်း ချီ ပ ညာ သင် အ ဖြစ် ဦး ဘ ဉာဏ် နဲ့ ဦး ဘ ဇော် ကို လည်း ဒီ့ အ ရင် က တည်း က လန် ဒန် ကို ပို့ ခဲ့ ပါ တယ် ။

 ဒါ ပေ မဲ့ ကို လို နီ ခေတ် မြန် မာ နိုင် ငံ မှာ အဲ ဒီ အ ချိန် ထိ အ မျိုး သား စာ ကြ ည့် တိုက် နဲ့ ပြ တိုက် ၊ အ နု ပ ညာ ပြ ခန်း တွေ မ ရှိ သေး ဘဲ ရန် ကုန် တက္က သိုလ် ပိ ဋ ကတ် တိုက် နဲ့ ရန် ကုန် မြို့ ထဲ က ဗား နတ် ပိ ဋ ကတ် တိုက် နဲ့ ပြ တိုက် အ ပြင် ပြည် နား က မှော် ဇာ ၊ ရ ခိုင် က မြောက် ဦး နဲ့ အ ညာ က ပု ဂံ ၊ ရွှေ ဘို နဲ့ မန္တ လေး မှာ ကမ္ပည်း ကျောက် စာ ဌာ န ပြ တိုက် က လေး တွေ ပဲ ရှိ ခဲ့ ပါ တယ် ။
```

ပိုနေတဲ့ space တွေကို ရှင်းကြရအောင်  
အခု သုံးပြထားတဲ့ clean-space.pl ကလည်း ဆရာ့ GitHub ရဲ့ tool/perl မှာ ရှိတဲ့ perl script တစ်ပုဒ်ပါ။  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ perl ./clean-space.pl ./test2.raw.nospace.syl > ./test2.raw.nospace.syl.clean
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test2.raw.nospace.syl.clean 
နိုင် ငံ တ ခု ထူ ထောင် တဲ့ အ ခါ မှာ စစ် တပ် ၊ စီး ပွား ရေး လုပ် ငန်း တွေ နဲ့ တ ရား ရုံး စ တဲ့ ပင် မ အ ဖွဲ့ အ စည်း တွေ သာ မ က စာ ပေ ယဉ် ကျေး မှု စိတ် ဓာတ် ပိုင်း က လည်း နိုင် ငံ သိ စိတ် ချစ် စိတ် တွေ ပေါ် လာ အောင် ဆော် ဩ ပေး ရ ပါ တယ် ။ ဒါ ကို သိ တဲ့ လူ ကြီး ပိုင်း က မြန် မာ ပြည် အ တွက် ပြ တိုက် စာ ကြ ည့် တိုက် နဲ့ အ နု ပ ညာ တိုက် တွေ ရှိ ဖို့ လို တဲ့ အ ကြောင်း ကို လို နီ ခေတ် က စ ပြီး တိုက် တွန်း ခဲ့ ကြ သ လို ဒီ ယဉ် ကျေး မှု အ ဆောက် အ ဦ တွေ ကို ကွပ် ကဲ ဖို့ အ တွက် ပ ညာ ရှင် တွေ ပေါ် ထွက် ဖို့ လည်း ကမ္ဘာ စစ် မ ဖြစ် ခင် က တည်း က စိုင်း ပြင်း ခဲ့ ကြ ပါ တယ် ။ ဒါ ကြော င့် ဦး ခင် ဇော် နဲ့ ဦး သိန်း ဟန် ကို ပိ ဋ ကတ် တိုက် ပ ညာ လို့ ခေါ် တဲ့ စာ ကြ ည့် တိုက် လုပ် ငန်း အ တွက် ဗြိ တိန် ကို စေ လွှတ် ခဲ့ သ လို ပန်း ချီ ပ ညာ သင် အ ဖြစ် ဦး ဘ ဉာဏ် နဲ့ ဦး ဘ ဇော် ကို လည်း ဒီ့ အ ရင် က တည်း က လန် ဒန် ကို ပို့ ခဲ့ ပါ တယ် ။
ဒါ ပေ မဲ့ ကို လို နီ ခေတ် မြန် မာ နိုင် ငံ မှာ အဲ ဒီ အ ချိန် ထိ အ မျိုး သား စာ ကြ ည့် တိုက် နဲ့ ပြ တိုက် ၊ အ နု ပ ညာ ပြ ခန်း တွေ မ ရှိ သေး ဘဲ ရန် ကုန် တက္က သိုလ် ပိ ဋ ကတ် တိုက် နဲ့ ရန် ကုန် မြို့ ထဲ က ဗား နတ် ပိ ဋ ကတ် တိုက် နဲ့ ပြ တိုက် အ ပြင် ပြည် နား က မှော် ဇာ ၊ ရ ခိုင် က မြောက် ဦး နဲ့ အ ညာ က ပု ဂံ ၊ ရွှေ ဘို နဲ့ မန္တ လေး မှာ ကမ္ပည်း ကျောက် စာ ဌာ န ပြ တိုက် က လေး တွေ ပဲ ရှိ ခဲ့ ပါ တယ် ။
```

BPE Unit ပြောင်းကြည့်တော့ output က အောက်ပါအတိုင်းပါ    
```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ python ../apply_bpe.py -c ./big-lm2.syl.bpe-model -i ./test2.raw.nospace.syl.clean 
နိုင် င@@ ံ တ ခု ထူ ထောင် တဲ့ အ ခါ မှာ စစ် တပ် ၊ စီး ပွား ရေး လုပ် င@@ န်း တွေ နဲ့ တ ရား ရုံး စ တဲ့ ပင် မ အ ဖွဲ့ အ စည်း တွေ သာ မ က စာ ပေ ယဉ် ကျေး မှု စိတ် ဓာတ် ပိုင်း က လည်း နိုင် င@@ ံ သိ စိတ် ချစ် စိတ် တွေ ပေါ် လာ အောင် ဆော် ဩ ပေး ရ ပါ တယ် ။ ဒါ ကို သိ တဲ့ လူ ကြီး ပိုင်း က မြန် မာ ပြည် အ တွက် ပြ တိုက် စာ ကြ ည့် တိုက် နဲ့ အ နု ပ ညာ တိုက် တွေ ရှိ ဖို့ လို တဲ့ အ ကြောင်း ကို လို နီ ခေတ် က စ ပြီး တိုက် တွန်း ခဲ့ ကြ သ လို ဒီ ယဉ် ကျေး မှု အ ဆောက် အ ဦ တွေ ကို ကွ@@ ပ် ကဲ ဖို့ အ တွက် ပ ညာ ရှင် တွေ ပေါ် ထွက် ဖို့ လည်း ကမ္ဘာ စစ် မ ဖြစ် ခင် က တည်း က စိုင်း ပြင်း ခဲ့ ကြ ပါ တယ် ။ ဒါ ကြော င့် ဦး ခင် ဇော် နဲ့ ဦး သိန်း ဟန် ကို ပိ ဋ ကတ် တိုက် ပ ညာ လို့ ခေါ် တဲ့ စာ ကြ ည့် တိုက် လုပ် င@@ န်း အ တွက် ဗြ@@ ိ တိန် ကို စေ လွှတ် ခဲ့ သ လို ပန်း ချီ ပ ညာ သင် အ ဖြစ် ဦး ဘ ဉာဏ် နဲ့ ဦး ဘ ဇော် ကို လည်း ဒီ@@ ့ အ ရင် က တည်း က လန် ဒန် ကို ပို့ ခဲ့ ပါ တယ် ။
ဒါ ပေ မဲ့ ကို လို နီ ခေတ် မြန် မာ နိုင် င@@ ံ မှာ အဲ ဒီ အ ချိန် ထိ အ မျိုး သား စာ ကြ ည့် တိုက် နဲ့ ပြ တိုက် ၊ အ နု ပ ညာ ပြ ခန်း တွေ မ ရှိ သေး ဘဲ ရန် ကုန် တက@@ ္@@ က သ@@ ိုလ် ပိ ဋ ကတ် တိုက် နဲ့ ရန် ကုန် မြို့ ထဲ က ဗား နတ် ပိ ဋ ကတ် တိုက် နဲ့ ပြ တိုက် အ ပြင် ပြည် နား က မှ@@ ော် ဇာ ၊ ရ ခိုင် က မြောက် ဦး နဲ့ အ ညာ က ပု ဂ@@ ံ ၊ ရွှေ ဘို နဲ့ မန@@ ္@@ တ လေး မှာ ကမ္@@ ပ@@ ည်း ကျောက် စာ ဌ@@ ာ န ပြ တိုက် က လေး တွေ ပဲ ရှိ ခဲ့ ပါ တယ် ။
```

####################  
####################  

## Character Segmentation

Character segmentation ကို အောက်ပါအတိုင်း လုပ်ခဲ့  
```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ ./char-segmentation.sh ./big-lm2.my.syl.clean > ./big-lm2.my.char
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ head ./big-lm2.my.char 
မ င ် း အ ဲ ့ ဒ ါ က ိ ု အ ခ ြ ာ း တ စ ် ခ ု န ဲ ့ မ ခ ျ ိ တ ် ဘ ူ း လ ာ း ။ 
သ ူ မ ဘ ယ ် သ ူ ့ က ိ ု မ ှ မ မ ှ တ ် မ ိ တ ေ ာ ့ ဘ ူ း ။ 
အ ဲ ့ ဒ ါ က ျ ွ န ် တ ေ ာ ် တ ိ ု ့ အ တ ွ က ် ခ က ် ခ ဲ တ ယ ် ။ 
ခ င ် ဗ ျ ာ း ပ ြ ေ ာ ခ ဲ ့ သ လ ိ ု က ျ ွ န ် တ ေ ာ ် ရ ှ င ် း ပ ြ ခ ဲ ့ တ ယ ် ။ 
သ ူ ့ က ိ ု ထ ိ န ် း ဖ ိ ု ့ မ င ် း ပ ဲ တ တ ် န ိ ု င ် တ ယ ် ။ 
အ ဲ ့ ဒ ါ က ိ ု က ိ ု ယ ် တ က ် န င ် း မ ိ သ ွ ာ း လ ာ း ။ 
င ါ စ ဉ ် း စ ာ း သ လ ိ ု စ ဉ ် း စ ာ း ပ ါ ။ 
အ တ င ် း ပ ြ ေ ာ ရ တ ာ မ ု န ် း တ ယ ် ။ 
 န ေ ာ က ် ဆ ု ံ း တ စ ် က ြ ိ မ ် သ ူ ့ က ိ ု ခ ျ စ ် ပ ါ တ ယ ် လ ိ ု ့ ပ ြ ေ ာ ခ ွ င ့ ် တ ေ ာ င ် မ ရ တ ေ ာ ့ ဘ ူ း ။ 
န ာ ဆ ာ မ ှ ဒ ု ံ း ပ ျ ံ စ တ က ် တ ာ န ဲ ့ သ ူ မ ှ တ ် တ မ ် း ရ ေ း ခ ဲ ့ တ ယ ် ။ 
```

## Clean heading and trailing spaces etc.

ပိုနေတဲ့ space တွေကို အောက်ပါအတိုင်း ဖျက်ခဲ့

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ perl ./clean-space.pl ./big-lm2.my.char > ./big-lm2.my.char.clean
```

head လုပ်ကြည့်   

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ head ./big-lm2.my.char.clean 
မ င ် း အ ဲ ့ ဒ ါ က ိ ု အ ခ ြ ာ း တ စ ် ခ ု န ဲ ့ မ ခ ျ ိ တ ် ဘ ူ း လ ာ း ။
သ ူ မ ဘ ယ ် သ ူ ့ က ိ ု မ ှ မ မ ှ တ ် မ ိ တ ေ ာ ့ ဘ ူ း ။
အ ဲ ့ ဒ ါ က ျ ွ န ် တ ေ ာ ် တ ိ ု ့ အ တ ွ က ် ခ က ် ခ ဲ တ ယ ် ။
ခ င ် ဗ ျ ာ း ပ ြ ေ ာ ခ ဲ ့ သ လ ိ ု က ျ ွ န ် တ ေ ာ ် ရ ှ င ် း ပ ြ ခ ဲ ့ တ ယ ် ။
သ ူ ့ က ိ ု ထ ိ န ် း ဖ ိ ု ့ မ င ် း ပ ဲ တ တ ် န ိ ု င ် တ ယ ် ။
အ ဲ ့ ဒ ါ က ိ ု က ိ ု ယ ် တ က ် န င ် း မ ိ သ ွ ာ း လ ာ း ။
င ါ စ ဉ ် း စ ာ း သ လ ိ ု စ ဉ ် း စ ာ း ပ ါ ။
အ တ င ် း ပ ြ ေ ာ ရ တ ာ မ ု န ် း တ ယ ် ။
 န ေ ာ က ် ဆ ု ံ း တ စ ် က ြ ိ မ ် သ ူ ့ က ိ ု ခ ျ စ ် ပ ါ တ ယ ် လ ိ ု ့ ပ ြ ေ ာ ခ ွ င ့ ် တ ေ ာ င ် မ ရ တ ေ ာ ့ ဘ ူ း ။
န ာ ဆ ာ မ ှ ဒ ု ံ း ပ ျ ံ စ တ က ် တ ာ န ဲ ့ သ ူ မ ှ တ ် တ မ ် း ရ ေ း ခ ဲ ့ တ ယ ် ။
```
## Learn Character based BPE for Myanmar Language

Error တက်တယ် အောက်ပါအတိုင်း...  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ time python ./learn_bpe.py -i ./y-test/big-lm2.my.char.clean -o ./y-test/big-lm2.char.bpe-model
Traceback (most recent call last):
  File "./learn_bpe.py", line 361, in <module>
    learn_bpe(args.input, args.output, args.symbols, args.min_frequency, args.verbose, is_dict=args.dict_input, total_symbols=args.total_symbols, num_workers=args.num_workers)
  File "./learn_bpe.py", line 296, in learn_bpe
    threshold = max(stats.values()) / 10
ValueError: max() arg is an empty sequence

real	0m1.920s
user	0m1.891s
sys	0m0.028s
```

Character segmentation ကြောင့်လို့ ယူဆတယ်။

## Extra Testing

character ဖြတ်ထားတာကို input လုပ်ပြီး syllable နဲ့ ဆောက်ထားတဲ့ BPE model ကိုသုံးပြီး pass လုပ်ရင်လည်း မဖြတ်ပေနိုင်တာကို အောက်ပါအတိုင်း တွေ့ရလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ python ../apply_bpe.py -c ./big-lm2.syl.bpe-model -i ./test1.char
မ င ် း က ိ ု င ါ ဘ ယ ် လ ိ ု ခ ေ ါ ် ရ မ လ ဲ 
စ ာ တ ေ ာ ် တ ဲ ့ က ျ ေ ာ င ် း သ ူ တ စ ် ယ ေ ာ က ် ပ ါ 
အ ရ မ ် း ဆ ေ ာ ့ တ ဲ ့ က လ ေ း က က ျ န ် း မ ာ တ ယ ် 
အ ခ ု တ ေ ာ ့ ပ ါ န က ် ဆ ရ ာ ဟ ာ စ က ် တ င ် ဘ ာ လ ၁ ၉ ရ က ် န ေ ့ မ ှ ာ ဆ န ္ ဒ ပ ြ ပ ွ ဲ က ျ င ် း ပ ဖ ိ ု ့ အ တ ွ က ် ပ ြ င ် ဆ င ် န ေ ပ ါ တ ယ ် ။ 
ဘ တ ် စ ် က ာ း စ ီ း ပ ြ ီ း ရ ု ံ း တ က ် တ ဲ ့ ဘ ိ လ ပ ် ပ ြ န ် ည ွ ှ န ် က ြ ာ း ရ ေ း မ ှ ူ း ခ ျ ု ပ ် 
```

## Building Syllable Vocab File

Vocab ဖိုင် ဆောက်ကြည့်မယ် ဆိုရင်  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ python ./get_vocab.py -i ./y-test/big-lm2.my.syl.clean -o ./y-test/big-lm2.my.syl.vocab
```

Syllable နဲ့ ဆောက်ထားတဲ့ ဖိုင်ဆိုက်ကို check ...  
```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ cd ./y-test/
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ wc ./big-lm2.my.syl.vocab 
 3301  6602 52427 ./big-lm2.my.syl.vocab
 ```
 
 head လုပ်ကြည့်တော့ freq အများဆုံးက ထိပ်ဆုံးမှာ ထားတာကို တွေ့ရ ...  
 
 ```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ head ./big-lm2.my.syl.vocab 
။ 99804
အ 47509
တယ် 36208
ပါ 33475
မ 31526
က 27813
ကို 26064
မှာ 17897
ကျွန် 17690
၊ 15364
```

freq အနည်းဆုံးက ဖိုင်ရဲ့ အောက်ဆုံးမှာ ...  

```
(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ tail ./big-lm2.my.syl.vocab 
ဘဲ့ 1
၆း 1
မိင် 1
ဘွမ် 1
ဖြယ် 1
ခေါ 1
ဘဲ” 1
ကင်္ြန် 1
၅း 1
ရဘ် 1
```

## Reference

Code:  
[https://github.com/rsennrich/subword-nmt](https://github.com/rsennrich/subword-nmt)  

> hxbai commented on Jun 27, 2019  
> I think your corpus is too small to learn the bpe, you cannot use the scripts directly since it learn the bpe on the training set and apply it to the dev and test set. You may need to change the scripts and learn the bpe on a relatively large training set, then apply the bpe codes to your selected sents.  

[https://github.com/hxbai/Deep_Enhanced_Repr_for_IDRR/issues/2(]https://github.com/hxbai/Deep_Enhanced_Repr_for_IDRR/issues/2)  

## Papers 

BPE-Dropout: Simple and Effective Subword Regularization:  
[https://arxiv.org/pdf/1910.13267.pdf](https://arxiv.org/pdf/1910.13267.pdf)  

Finding Better Subword Segmentation for Neural Machine Translation:  
[http://cips-cl.org/static/anthology/CCL-2018/CCL-18-074.pdf](http://cips-cl.org/static/anthology/CCL-2018/CCL-18-074.pdf)  

Neural Machine Translation of Rare Words with Subword Units:  
[https://arxiv.org/pdf/1508.07909v5.pdf](https://arxiv.org/pdf/1508.07909v5.pdf)  
