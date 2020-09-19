## Installation

(base) ye@ykt-pro:~/tool$ git clone https://github.com/rsennrich/subword-nmt
Cloning into 'subword-nmt'...
remote: Enumerating objects: 576, done.
remote: Total 576 (delta 0), reused 0 (delta 0), pack-reused 576
Receiving objects: 100% (576/576), 233.30 KiB | 254.00 KiB/s, done.
Resolving deltas: 100% (349/349), done.

(base) ye@ykt-pro:~/tool$ cd subword-nmt/

(base) ye@ykt-pro:~/tool/subword-nmt$ ls
apply_bpe.py  get_vocab.py  learn_joint_bpe_and_vocab.py  README.md  subword_nmt
CHANGELOG.md  learn_bpe.py  LICENSE                       setup.py

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

*** Installation က pip install နဲ့လည်း လုပ်လို့ရတယ်။

## Build Syllable based BPE Units

word ဖြတ်ထားတဲ့ ဒေတာနဲ့ BPE unit build လုပ်တာ

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

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ time python ./learn_bpe.py -i ./y-test/big-lm2.my -o ./y-test/big-lm2.syl.bpe-model

real	0m16.046s
user	0m15.895s
sys	0m0.148s

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt$ ls ./y-test/
big-lm2.my  big-lm2.my.syl.clean  big-lm2.syl.bpe-model

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

## Segmenting with Syllable based BPE

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat test1.txt 
မင်း ကို ငါ ဘယ်လို ခေါ် ရ မ လဲ
စာ တော် တဲ့ ကျောင်း သူ တစ် ယောက် ပါ
အ ရမ်း ဆော့ တဲ့ ကလေး က ကျန်း မာ တယ်
အခု တော့ ပါ နက် ဆ ရာ ဟာ စက် တင် ဘာ လ ၁၉ ရက် နေ့ မှာ ဆန္ဒ ပြ ပွဲ ကျင်း ပ ဖို့ အ တွက် ပြင် ဆင် နေ ပါ တယ် ။
ဘတ်စ် ကား စီး ပြီး ရုံး တက် တဲ့ ဘိလပ် ပြန် ညွှန် ကြား ရေး မှူး ချုပ်

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ python ../apply_bpe.py -i ./test1.txt -c ./big-lm2.syl.bpe-model -o ./test1.bpe

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ cat ./test1.bpe 
မင်း ကို ငါ ဘယ်လို ခေါ် ရ မ လဲ
စာ တော် တဲ့ ကျောင်း သူ တစ် ယောက် ပါ
အ ရမ်း ဆော့ တဲ့ ကလေး က ကျန်း မာ တယ်
အခု တော့ ပါ နက် ဆ ရာ ဟာ စက် တင် ဘာ လ ၁၉ ရက် နေ့ မှာ ဆန္ဒ ပြ ပွဲ ကျင်း ပ ဖို့ အ တွက် ပြင် ဆင် နေ ပါ တယ် ။
ဘတ်စ် ကား စီး ပြီး ရုံး တက် တဲ့ ဘိ@@ လပ် ပြန် ညွှန် ကြား ရေး မှူး ချုပ်

####################
####################

## Character Segmentation

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

## Clean heading and trailing spaces etc.

ပိုနေတဲ့ space တွေကို အောက်ပါအတိုင်း ဖျက်ခဲ့

(base) ye@ykt-pro:~/tool/subword-nmt/build/lib/subword_nmt/y-test$ perl ./clean-space.pl ./big-lm2.my.char > ./big-lm2.my.char.clean

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

## Learn BPE

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

Character segmentation ကြောင့်လို့ ယူဆတယ်။

## Reference

Code:  
https://github.com/rsennrich/subword-nmt  

> hxbai commented on Jun 27, 2019  
> I think your corpus is too small to learn the bpe, you cannot use the scripts directly since it learn the bpe on the training set and apply it to the dev and test set. You may need to change the scripts and learn the bpe on a relatively large training set, then apply the bpe codes to your selected sents.  

https://github.com/hxbai/Deep_Enhanced_Repr_for_IDRR/issues/2  

## Papers 

BPE-Dropout: Simple and Effective Subword Regularization:
https://arxiv.org/pdf/1910.13267.pdf  

Finding Better Subword Segmentation for Neural Machine Translation:  
http://cips-cl.org/static/anthology/CCL-2018/CCL-18-074.pdf  

Neural Machine Translation of Rare Words with Subword Units:  
https://arxiv.org/pdf/1508.07909v5.pdf  
