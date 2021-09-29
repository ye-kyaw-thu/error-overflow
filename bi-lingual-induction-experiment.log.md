# Bi-lingual Induction Experiment Log

Github Link:  [https://github.com/cardiffnlp/en-cy-bilingual-embeddings](https://github.com/cardiffnlp/en-cy-bilingual-embeddings)  
Last Updated: 28 Sept 2021  

## Check Dictionary Format

```
meatus	meatws
mechanic	peiriannydd
mechanical	mecanyddol
mechanical	mecanyddol
mechanical advantage	mantais fecanyddol
```

dictionary ကိုလည်း train, test ခွဲဖို့ လိုအပ်တယ် ဆိုတာကို တွေ့ရ   

အင်္ဂလိပ်-မြန်မာ အဘိဓာန်တစ်ခုကို ပြင်ဆင်ခဲ့...  
/media/ye/project1/data/Dictionary/ အောက်ကနေ copy ကူးခဲ့...   

```
(base)  ye@~/tool/en-cy-bilingual-embeddings/my-data$ wc en1.txt en2.txt
  65535  117603  798109 en1.txt
  44105   84037  568166 en2.txt
 109640  201640 1366275 total

(base)  ye@~/tool/en-cy-bilingual-embeddings/my-data$ wc my1.txt my2.txt
  65535  110553 3688544 my1.txt
  44105   77240 2517953 my2.txt
 109640  187793 6206497 total
```

## Prepare a Big Corpus

copy the corpus...   

```
(base)  ye@/media/ye/SP PHD U3/tool/word-seg-tool/python-wordsegment/wordsegment/y-test/ref/viterbi/dev4github/4release$ cp corpus2 /home/ye/tool/en-cy-bilingual-embeddings/my-data/
```

copy and check the data...   

```
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/big-myanmar$ cp /media/ye/SP\ PHD\ U3/tool/word-seg-tool/python-wordsegment/wordsegment/y-test/ref/viterbi/dev4github/4release/corpus2 .
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/big-myanmar$ wc corpus2 
   525626  12185589 159532418 corpus2
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/big-myanmar$ head corpus2
လု သာ မောင်း ပြိုင် သာ ပြိုင် ကိုယ့် ကိုယ်ပိုင် ကား မ ဟုတ် ပြဿနာ ဖြစ် ရင် ထွက် ပြေး အေးအေးဆေးဆေး ဖြစ် သွား ရင် ပြန် မောင်း လု သာ မောင်း ။
သမ္မတ ဦးထင်ကျော်
အင်းလေး သူ ဆို လည်း ကောင်း တာ ပဲ ၊ ကစ်ကစ် က ဖြူဖြူ ဖွေးဖွေးလေး ဆို တော့ ၊ ရှမ်းမလေး တွေ တော့ ထိုင် ငို နေ တော့ မှာ ပဲ အင်းလေး ကို အရမ်း ချစ် တယ် အင်းလေး နဲ့ ကစ် နဲ့ လိုက် ပါ တယ် တသက်လုံး တကယ် လာ နေ ရင် အရမ်း ကောင်း မှာ ပဲ ချစ်﻿ တယ် မကစ် ဇင်ဇင် တို့ မွန် ပြည်နယ် လာလည် ပါ လား ဖိတ်ခေါ် ပါ တယ် ကျိုက်ထီးရိုး ဘုရား ဖူး ရင် မော်လမြိုင် မြို့ ကို လာလည် ပါ ရှမ်း က မဲ တာ လား အင်းသူမ က မဲ တာ လား မူကြို ကလေး မေး တောင် သိ တယ် အင်းသူမ က ဘယ်လောက် ပဲ ပိုက်ဆံ ရှိ ပါစေ အလောင်းစည်သူမင်း ကျိန်စာ တိုက် ခဲ့ လို့ ရေ ခြံ ရော ကုန်း ခြံ ရော ကုန်း နေ အောင် လုပ် ရ တာ ဖြူ နေ ဦး မယ် အသား က ကြည့် ပြော အင်းသူမ လုပ် ရင် ရေ ကူး တတ် ရ မယ် နော် ရေ မ ကူး တတ် ရင် အလောင်း တွေ ခု ချိန် ထိ ဆယ် မ ကုန် သေး ဘူး အသဲ 😍 😍 😍 😍 မမ ကစ် ချစ် လိုက် တာ ကောင်း တယ် လုပ် ပစ် လိုက် အမ 😁 😁 😁 😁 ကစ် သာ နေ ရင် ရှမ်း ပြည် အပြီး ပြန် လာ မယ် နေ နိုင် လား ဘဝ ကို ဖြတ်သန်း တဲ့ အခါ အရိုးဆုံး က အကောင်းဆုံး ပါ ပဲ မ လုပ် ပါ နဲ့ ကစ်လေး ရယ် ရန်ကုန် ကို အမြန် ပြန် လာ ပါ ကိုယ် အရမ်း သတိရ လို့ ပါ ကွာ ချစ် တာ 😍 😍 😘 😘 ချစ် စရာ လေး အရမ်း ကြိုက် မမ နေ ပါ ကစ်လေး ရယ် သာယာ လိုက် တာ အဲ့ နား မှာ အိမ် တစ် လုံး သွား ဝယ် လိုက် မှာ ပေါ့ ။
အင်းသား ဖြစ် ချင် လို့ အင်းသူမ ပဲ လုပ် တော့ မကစ် คุณน่ารักเสมอ 💟 ကြည့် လို့ မ ရ တော့ ဘူး နော် ကိုကြီး နေ ဖို့ လည်း မ ကောင်း ပဲ ရေ ထဲ မှာ ငါ မ ကြိုက် ဘူး ကောင်း သား ပဲ အင်းသူမလေး ဆို တော့ အေးအေးချမ်းချမ်း လေး ပေါ့ နော် မကစ် ကို က အင်းသား ဖြစ် ပါရစေ ကောင်း တာ ပေါ့ ကစ် ရဲ့ အင်းသူလေး တွေ က ဖြူစင် တယ် အင်းသူမလေး ဖြစ် တော့ မယ် ရွှေ ကစ်လေး :- * ကောင်း သလိုလို တော့ ရှိ သား နော်
ရွှေ ကစ်လေး ရဲ့ ကုသိုလ် ကြောင့် အစစအရာရာ ပြီးပြည့်စုံ မှာ ပါ ရွှေ ကစ်လေး ကို လည်း သေ တဲ့ ထိ အားပေး မှာ ပါ အရမ်း ချစ် တယ် သာဓု ပါ သာဓု ပါ သာဓု ပါ ဒီ ထက် မက လှူ နိုင် ပါစေ နော် 👏 👏 👏 👏 👏 👍 👍 👍 အခု လို ပြု ရ သော ကုသိုလ် ကောင်း မှု တွေ ကြောင့် ဘဝ မှာ တောင်းတ ခြင်း နဲ့ ကြောက် ရ ခြင်း ကင်းဝေး ပြီး တော့ မနက်ဖြန် တွေ တိုင်း မှာ ချစ် တဲ့ မိသားစု နဲ့ ပျော်ရွှင် စွာ ဖြတ်သန်း နိုင် ပါစေ မကစ် 😍 😍 😍 😍 😍
အနိုင်ရ မည့် အသင်း = ပြင်သစ် ဂိုး ရလဒ် = ပြင်သစ် ၂ - ၀ ခရိုအေးရှား
မွန် ရခိုင် ရခိုင် ရခိုင် ရခိုင်
ည အရမ်း တိုးတက် လို့ ပါ လား ခြင်္သေ့ အက တွေ နဲ့ တော့ ပြန် ကြည့် ချင် တယ် ယား နေ ရော ပဲ ဝမ်းစာရေး က အဓိက ပါ လေ ပြန် တော့ ဘူး တော် ပါ ပေ တယ် ဗျာ လေးစား တယ် ဝိုး လီး ဘဲ့ စောက် တရုတ် ပွဲ ကျ ခမ်းခမ်းနားနား ကျင်းပ ပေး တယ် တရုတ် ပြည် လည်း ဝင် တိုက် လိုက် လေ ဆယ်ဆ ပေး ရင် နိုင် မယ် လာ ။
အလုပ် လည်း လုပ် ပညာ လည်း ယူ ချမ်းသာ ရင် တရုတ် ပြည် သွား လည် ရင် မ ကောင်း ဘူး လား ။
အဲ့ အတွေး ပဲ လူ ဖြစ် ရင် ထမင်း စား လည်း အလကား ပဲ ။
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/big-myanmar$
```

copy and check paraphrase data...    

```
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/mypara-word$ cp mypara-all.manual.word ../big-myanmar/
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/mypara-word$ wc ./mypara-all.manual.word 
  84921  753196 8699990 ./mypara-all.manual.word
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/mypara-word$ head ./mypara-all.manual.word 
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။
ကျေးဇူး အများကြီး တင် ပါ တယ် ။
ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။
 ကောင်း သော ည ပါ ။
ကောင် လေး က လူ ကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။
ခဏ အကြာ မှာ ကျွန်တော် ခင်ဗျား ကို ပြန် ဆက် ပါ ရ စေ ။
ခေါင်မိုး ပေါ် မှာ ကြောင် တစ် ကောင် ရှိ တယ် ။
ငါ ခိုင်း တာ မင်း လုပ် ခဲ့ လား ။
```

combine two corpora...   

```
(base)  ye@/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext/big-myanmar$ wc corpus2-and-para 
   610547  12938785 168232408 corpus2-and-para
```

## make a Big word2vec and fasttext models  for Burmese

```
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ time python ./Sherlock_Holmes_fasttext.py ./big-myanmar/corpus2-and-para
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 13M words
Number of words:  37457
Number of labels: 0
Progress: 100.0% words/sec/thread:   33021 lr:  0.000000 avg.loss:  1.704674 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('စာသင်', 0.6664983630180359), ('ကျူရှင်', 0.6439144015312195), ('သင်တန်း', 0.6167402267456055), ('အထက်တန်း', 0.6155328154563904), ('ကောလိပ်', 0.6092570424079895), ('မူလတန်း', 0.6051368713378906), ('တက္ကသိုလ်', 0.5800604820251465), ('စာသင်ကျောင်း', 0.5697867274284363), ('အထက်တန်းကျောင်း', 0.5548005104064941), ('စာကြည့်တိုက်', 0.5527700185775757), ('အတန်း', 0.5506138801574707), ('ဘုန်းကြီးကျောင်း', 0.5431583523750305), ('ဂေဟာ', 0.537689745426178), ('ရဟန်း၊', 0.5304527878761292), ('ပညာသင်', 0.5243661999702454), ('သိမ်၊', 0.5216583013534546), ('အလယ်တန်း', 0.5190342664718628), ('ကျောင်းဆရာ', 0.5150541067123413), ('သူငယ်တန်း', 0.5135067105293274), ('ကျောင်း၊', 0.5103265643119812)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.8418470025062561, '\u200dကျောင်း'), (0.801422119140625, '\u200bကျောင်း'), (0.7977048754692078, 'ကျောင်းအပ်'), (0.7898997068405151, 'ကျောင်းတက်'), (0.7829453945159912, 'ကျောင်းနေ'), (0.7780985236167908, 'ကျောင်းဆင်း'), (0.7755478024482727, 'မြို့ကျောင်း'), (0.7677992582321167, 'ကျောင်းစု'), (0.7650551795959473, 'ကျောင်းကန်'), (0.7607253193855286, 'ကျောင်းဝင်း'), (0.758015513420105, 'ကျောင်းပျက်'), (0.7567769885063171, 'ကောလိပ်ကျောင်း'), (0.756318211555481, 'ကျွဲကျောင်း'), (0.7486361265182495, 'ကျောင်းတွင်း'), (0.7475395798683167, 'ကျောင်းထိုင်'), (0.7461807131767273, 'စာသင်ကျောင်း'), (0.7436200976371765, 'ကျောင်းပိုင်'), (0.7380182147026062, 'ကျောင်းစာ'), (0.7373899221420288, 'ကျောင်းပို့'), (0.7369712591171265, 'ကျောင်းခန်း')] 


real	7m11.755s
user	37m22.920s
sys	0m8.094s
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$
```

check the output. OK!  

```
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ ls
all-para.fasttext.bin   mypara-all.word    mypara-syl.tmp   scandal_in_bohemia_sentences_no_stopwords.txt  word_embeddings_SVD.R
all-para.word2vec       mypara-manual      mypara-word      scandal_in_bohemia_sentences.txt
big-myanmar             mypara-manual.tmp  mypara-word.tmp  scandal_in_bohemia_tokens.csv
fasttext_bin-to-vec.py  mypara-syl         old-bk           Sherlock_Holmes_fasttext.py
```

ဖိုင်နာမည်ပြောင်းခဲ့...   

```
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ mv all-para.word2vec corpus2-para.word2vec
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ mv all-para.fasttext.bin corpus2-para.fasttext.bin
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ ll -h corpus2-para.word2vec 
-rwxr-xr-x 1 ye ye 711M စက်   23 19:56 corpus2-para.word2vec*
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ ll -h corpus2-para.fasttext.bin 
-rwxr-xr-x 1 ye ye 3.9G စက်   23 20:02 corpus2-para.fasttext.bin*
```

လိုအပ်ရင် သုံးလို့ ရအောင်လို့ fasttext.bin ကို vector text format အဖြစ် ပြောင်းထားခဲ့...   

```
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ time python ./fasttext_bin-to-vec.py ./corpus2-para.fasttext.bin ./corpus2-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.

real	0m12.874s
user	0m11.201s
sys	0m1.673s
(base) ye@:/media/ye/SP PHD U3/4github/syl-ngram/ref/playing_with_fasttext$ wc ./corpus2-para.fasttext.vector 
    37458  18765959 218718957 ./corpus2-para.fasttext.vector
```

-----------------

## Prepare a New Python Environment

```
(base)  ye@~/tool/en-cy-bilingual-embeddings$ conda create -n bilingual-emb python=3
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/bilingual-emb

  added / updated specs:
    - python=3


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2021.5.30          |   py39h06a4308_0         139 KB
    pip-21.2.4                 |   py37h06a4308_0         1.8 MB
    python-3.9.7               |       h12debd9_1        18.6 MB
    setuptools-58.0.4          |   py39h06a4308_0         790 KB
    tzdata-2021a               |       h5d7bf9c_0         111 KB
    ------------------------------------------------------------
                                           Total:        21.4 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.7.5-h06a4308_1
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py39h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.4-py37h06a4308_0
  python             pkgs/main/linux-64::python-3.9.7-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.1-h27cfd23_0
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py39h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.36.0-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  tzdata             pkgs/main/noarch::tzdata-2021a-h5d7bf9c_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.9.7         | 18.6 MB   | ############################################################################################################# | 100% 
pip-21.2.4           | 1.8 MB    | ############################################################################################################# | 100% 
certifi-2021.5.30    | 139 KB    | ############################################################################################################# | 100% 
tzdata-2021a         | 111 KB    | ############################################################################################################# | 100% 
setuptools-58.0.4    | 790 KB    | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate bilingual-emb
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base)  ye@~/tool/en-cy-bilingual-embeddings$ conda activate bilingual-emb
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings$ pip install -r requirements.txt
Collecting absl-py==0.13.0
  Using cached absl_py-0.13.0-py3-none-any.whl (132 kB)
Collecting astunparse==1.6.3
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting cachetools==4.2.2
  Using cached cachetools-4.2.2-py3-none-any.whl (11 kB)
Requirement already satisfied: certifi==2021.5.30 in /home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages (from -r requirements.txt (line 4)) (2021.5.30)
Collecting charset-normalizer==2.0.4
  Using cached charset_normalizer-2.0.4-py3-none-any.whl (36 kB)
Collecting clang==5.0
  Using cached clang-5.0.tar.gz (30 kB)
Collecting click==8.0.1
  Using cached click-8.0.1-py3-none-any.whl (97 kB)
Collecting flatbuffers==1.12
  Using cached flatbuffers-1.12-py2.py3-none-any.whl (15 kB)
Collecting gast==0.4.0
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting gensim==3.8.3
  Downloading gensim-3.8.3.tar.gz (23.4 MB)
     |████████████████████████████████| 23.4 MB 1.7 MB/s 
Collecting google-auth==1.35.0
  Using cached google_auth-1.35.0-py2.py3-none-any.whl (152 kB)
Collecting google-auth-oauthlib==0.4.6
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting google-pasta==0.2.0
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting grpcio==1.40.0
  Downloading grpcio-1.40.0-cp39-cp39-manylinux2014_x86_64.whl (4.3 MB)
     |████████████████████████████████| 4.3 MB 102.6 MB/s 
Collecting h5py==3.1.0
  Downloading h5py-3.1.0-cp39-cp39-manylinux1_x86_64.whl (4.4 MB)
     |████████████████████████████████| 4.4 MB 111.3 MB/s 
Collecting idna==3.2
  Using cached idna-3.2-py3-none-any.whl (59 kB)
Collecting joblib==1.0.1
  Using cached joblib-1.0.1-py3-none-any.whl (303 kB)
Collecting keras==2.6.0
  Using cached keras-2.6.0-py2.py3-none-any.whl (1.3 MB)
Collecting Keras-Preprocessing==1.1.2
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting Markdown==3.3.4
  Using cached Markdown-3.3.4-py3-none-any.whl (97 kB)
Collecting nltk==3.6.2
  Using cached nltk-3.6.2-py3-none-any.whl (1.5 MB)
Collecting numpy==1.19.5
  Downloading numpy-1.19.5-cp39-cp39-manylinux2010_x86_64.whl (14.9 MB)
     |████████████████████████████████| 14.9 MB 70.6 MB/s 
Collecting oauthlib==3.1.1
  Using cached oauthlib-3.1.1-py2.py3-none-any.whl (146 kB)
Collecting opt-einsum==3.3.0
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting pandas==1.3.2
  Downloading pandas-1.3.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.5 MB)
     |████████████████████████████████| 11.5 MB 33.2 MB/s 
Collecting protobuf==3.17.3
  Downloading protobuf-3.17.3-cp39-cp39-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.0 MB)
     |████████████████████████████████| 1.0 MB 111.2 MB/s 
Collecting pyasn1==0.4.8
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Collecting pyasn1-modules==0.2.8
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting python-dateutil==2.8.2
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pytz==2021.1
  Using cached pytz-2021.1-py2.py3-none-any.whl (510 kB)
Collecting regex==2021.8.28
  Downloading regex-2021.8.28-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (759 kB)
     |████████████████████████████████| 759 kB 93.7 MB/s 
Collecting requests==2.26.0
  Using cached requests-2.26.0-py2.py3-none-any.whl (62 kB)
Collecting requests-oauthlib==1.3.0
  Using cached requests_oauthlib-1.3.0-py2.py3-none-any.whl (23 kB)
Collecting rsa==4.7.2
  Using cached rsa-4.7.2-py3-none-any.whl (34 kB)
Collecting scikit-learn==0.24.2
  Downloading scikit_learn-0.24.2-cp39-cp39-manylinux2010_x86_64.whl (23.8 MB)
     |████████████████████████████████| 23.8 MB 21.2 MB/s 
Collecting scipy==1.7.1
  Downloading scipy-1.7.1-cp39-cp39-manylinux_2_5_x86_64.manylinux1_x86_64.whl (28.5 MB)
     |████████████████████████████████| 28.5 MB 83.6 MB/s 
Collecting six==1.15.0
  Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting sklearn==0.0
  Using cached sklearn-0.0.tar.gz (1.1 kB)
Collecting smart-open==5.2.1
  Using cached smart_open-5.2.1-py3-none-any.whl (58 kB)
Collecting tensorboard==2.6.0
  Using cached tensorboard-2.6.0-py3-none-any.whl (5.6 MB)
Collecting tensorboard-data-server==0.6.1
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting tensorboard-plugin-wit==1.8.0
  Using cached tensorboard_plugin_wit-1.8.0-py3-none-any.whl (781 kB)
Collecting tensorflow==2.6.0
  Downloading tensorflow-2.6.0-cp39-cp39-manylinux2010_x86_64.whl (458.4 MB)
     |████████████████████████████████| 458.4 MB 27 kB/s 
Collecting tensorflow-estimator==2.6.0
  Using cached tensorflow_estimator-2.6.0-py2.py3-none-any.whl (462 kB)
Collecting termcolor==1.1.0
  Using cached termcolor-1.1.0.tar.gz (3.9 kB)
Collecting threadpoolctl==2.2.0
  Using cached threadpoolctl-2.2.0-py3-none-any.whl (12 kB)
Collecting tqdm==4.62.2
  Using cached tqdm-4.62.2-py2.py3-none-any.whl (76 kB)
Collecting typing-extensions==3.7.4.3
  Using cached typing_extensions-3.7.4.3-py3-none-any.whl (22 kB)
Collecting urllib3==1.26.6
  Using cached urllib3-1.26.6-py2.py3-none-any.whl (138 kB)
Collecting Werkzeug==2.0.1
  Using cached Werkzeug-2.0.1-py3-none-any.whl (288 kB)
Collecting wrapt==1.12.1
  Using cached wrapt-1.12.1.tar.gz (27 kB)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages (from astunparse==1.6.3->-r requirements.txt (line 2)) (0.37.0)
Requirement already satisfied: setuptools>=40.3.0 in /home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages (from google-auth==1.35.0->-r requirements.txt (line 11)) (58.0.4)
Building wheels for collected packages: clang, gensim, sklearn, termcolor, wrapt
  Building wheel for clang (setup.py) ... done
  Created wheel for clang: filename=clang-5.0-py3-none-any.whl size=30692 sha256=07fc6dee7f4e16cae0e5bdaed5d0971363c0ad02176de60629ffb0a1c717e990
  Stored in directory: /home/ye/.cache/pip/wheels/3a/ce/7a/27094f689461801c934296d07078773603663dfcaca63bb064
  Building wheel for gensim (setup.py) ... done
  Created wheel for gensim: filename=gensim-3.8.3-cp39-cp39-linux_x86_64.whl size=24308043 sha256=6bb167185bb744a1cad2fb894c7fe0c73f0d4f045e83ac29f728c629fd8afd05
  Stored in directory: /home/ye/.cache/pip/wheels/ca/5d/af/618594ec2f28608c1d6ee7d2b7e95a3e9b06551e3b80a491d6
  Building wheel for sklearn (setup.py) ... done
  Created wheel for sklearn: filename=sklearn-0.0-py2.py3-none-any.whl size=1309 sha256=e2eb5896644dcf86409353702cb44a96c833e9bf55bd420b4e3538ab97bc0360
  Stored in directory: /home/ye/.cache/pip/wheels/e4/7b/98/b6466d71b8d738a0c547008b9eb39bf8676d1ff6ca4b22af1c
  Building wheel for termcolor (setup.py) ... done
  Created wheel for termcolor: filename=termcolor-1.1.0-py3-none-any.whl size=4847 sha256=3e246e50f0b7a6ef2974c76a0d95eaf91743c6a6e2bdac741862b089d191a449
  Stored in directory: /home/ye/.cache/pip/wheels/b6/0d/90/0d1bbd99855f99cb2f6c2e5ff96f8023fad8ec367695f7d72d
  Building wheel for wrapt (setup.py) ... done
  Created wheel for wrapt: filename=wrapt-1.12.1-cp39-cp39-linux_x86_64.whl size=37173 sha256=d6d59a5b844bf8ed654834cf0d676f922a7f3214a374841e39f43b18bab06fa1
  Stored in directory: /home/ye/.cache/pip/wheels/98/23/68/efe259aaca055e93b08e74fbe512819c69a2155c11ba3c0f10
Successfully built clang gensim sklearn termcolor wrapt
Installing collected packages: urllib3, pyasn1, idna, charset-normalizer, six, rsa, requests, pyasn1-modules, oauthlib, cachetools, requests-oauthlib, numpy, google-auth, Werkzeug, threadpoolctl, tensorboard-plugin-wit, tensorboard-data-server, scipy, protobuf, Markdown, joblib, grpcio, google-auth-oauthlib, absl-py, wrapt, typing-extensions, tqdm, termcolor, tensorflow-estimator, tensorboard, smart-open, scikit-learn, regex, pytz, python-dateutil, opt-einsum, Keras-Preprocessing, keras, h5py, google-pasta, gast, flatbuffers, click, clang, astunparse, tensorflow, sklearn, pandas, nltk, gensim
Successfully installed Keras-Preprocessing-1.1.2 Markdown-3.3.4 Werkzeug-2.0.1 absl-py-0.13.0 astunparse-1.6.3 cachetools-4.2.2 charset-normalizer-2.0.4 clang-5.0 click-8.0.1 flatbuffers-1.12 gast-0.4.0 gensim-3.8.3 google-auth-1.35.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.40.0 h5py-3.1.0 idna-3.2 joblib-1.0.1 keras-2.6.0 nltk-3.6.2 numpy-1.19.5 oauthlib-3.1.1 opt-einsum-3.3.0 pandas-1.3.2 protobuf-3.17.3 pyasn1-0.4.8 pyasn1-modules-0.2.8 python-dateutil-2.8.2 pytz-2021.1 regex-2021.8.28 requests-2.26.0 requests-oauthlib-1.3.0 rsa-4.7.2 scikit-learn-0.24.2 scipy-1.7.1 six-1.15.0 sklearn-0.0 smart-open-5.2.1 tensorboard-2.6.0 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.0 tensorflow-2.6.0 tensorflow-estimator-2.6.0 termcolor-1.1.0 threadpoolctl-2.2.0 tqdm-4.62.2 typing-extensions-3.7.4.3 urllib3-1.26.6 wrapt-1.12.1
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings$
```

-------------------
-------------------

## Moved All Data to Portable USB HDD and Start a New Experiment

အရင်ဆုံး ဒေတာ ပြင်ဆင်ခဲ့...  

corpus အတွက်က ASEAN-MT ဒေတာရယ် (en, th, my), TALPCo ဒေတာရယ် (en, th, my), BEST thai corpus ရယ်, myword+para (for my),

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ cp data_eng.txt ../../exp1/en/  
```

```
(base) ye@:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py word /home/ye/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus/data_myn.txt /home/ye/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus/data_myn.word.txt
```

ဒါပေမဲ့ myWord နဲ့ ဖြတ်တဲ့ output ထက် manual ဖြတ်ထားပြီးသား ရှိတာမို့ အဲဒါကိုပဲ ယူသုံးဖို့ ဆုံးဖြတ်ခဲ့...  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ wget https://raw.githubusercontent.com/matbahasa/TALPCo/master/myn/data_myn-token.txt 
--2021-09-26 04:13:59--  https://raw.githubusercontent.com/matbahasa/TALPCo/master/myn/data_myn-token.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.110.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 188242 (184K) [text/plain]
Saving to: ‘data_myn-token.txt’

data_myn-token.txt                    100%[=========================================================================>] 183.83K  --.-KB/s    in 0.1s    

2021-09-26 04:13:59 (1.51 MB/s) - ‘data_myn-token.txt’ saved [188242/188242]

(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head data_myn-token.txt 
1176
မစ္စတာ
တာနာခါ
ဟာ
ကျောင်းသား
မ
ဟုတ်
ပါ
ဘူး
။
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ 
```

column to line conversion:  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ perl ./col2line.pl ./data_myn-token.txt > ./data_myn-token.txt.line
```

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_myn-token.txt.line 
1176 မစ္စတာ တာနာခါ ဟာ ကျောင်းသား မ ဟုတ် ပါ ဘူး ။
1178 အဖေ က ကျောင်းဆရာ ပါ ။
1180 ကျောင်း ပိတ် တယ် ။
1194 တိုကျို မှာ နေ သာ တယ် ။
1222 ပန်းခြံ မှာ သစ်ပင် တွေ ရှိ တယ် ။
1229 မစ္စတာ တာနာခါ ဘယ် မှာ ရှိ သ လဲ ။
1233 ပိုက်ဆံ မ ရှိ ဘူး ။
1244 စာရေးခုံ ပေါ် မှာ စာအုပ် ရှိ တယ် ။
1245 စာရေးခုံ အောက် မှာ လွယ်အိတ် ရှိ တယ် ။
1246 အိတ် ထဲ မှာ မှတ်စုစာအုပ် ရှိ တယ် ။
```

Remove line no:  

```
$ sed 's/^ *[0-9]\+.//g' ./data_myn-token.txt.line > ./data_myn-token.txt.line.rm-lineno 
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_myn-token.txt.line.rm-lineno 
မစ္စတာ တာနာခါ ဟာ ကျောင်းသား မ ဟုတ် ပါ ဘူး ။
အဖေ က ကျောင်းဆရာ ပါ ။
ကျောင်း ပိတ် တယ် ။
တိုကျို မှာ နေ သာ တယ် ။
ပန်းခြံ မှာ သစ်ပင် တွေ ရှိ တယ် ။
မစ္စတာ တာနာခါ ဘယ် မှာ ရှိ သ လဲ ။
ပိုက်ဆံ မ ရှိ ဘူး ။
စာရေးခုံ ပေါ် မှာ စာအုပ် ရှိ တယ် ။
စာရေးခုံ အောက် မှာ လွယ်အိတ် ရှိ တယ် ။
အိတ် ထဲ မှာ မှတ်စုစာအုပ် ရှိ တယ် ။
```

စာလုံးဖြတ်ပြီး ကော်လံအလိုက်ဖြစ်နေတဲ့ ထိုင်း ဖိုင်ကိုလည်း ပုံမှန် left-to-right line တွေအဖြစ် အောက်ပါအတိုင်း ပြောင်းခဲ့...  

```
$ perl ./col2line.pl ./data_tha-token.txt > ./data_tha-token.txt.line 
$ sed 's/^ *[0-9]\+.//g' ./data_tha-token.txt.line > ./data_tha-token.txt.line.rm-lineno

(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_tha-token.txt.line.rm-lineno 
คุณ ทานากะ ไม่ ใช่ นัก เรียน ครับ
พ่อ เป็น อาจารย์ ครับ
โรง เรียน หยุด ครับ
โตเกียว อากาศ แจ่มใส ครับ
ที่ สวน สาธารณะ มี ต้น ไม้ ครับ
คุณ ทานากะ อยู่ ที่ ไหน ครับ
ไม่ มี เงิน ครับ
บน โต๊ะ มี หนังสือ ครับ
ใต้ โต๊ะ มี กระเป๋า ครับ
ใน กระเป๋า มี สมุด โน้ต ครับ
```

## Downloading UMBC English Corpus

အင်္ဂလိပ်စာကိုလည်း ကိုယ့်စက်ထဲမှာ word2vec နဲ့ fasttext မော်ဒယ်ကို ဆောက်မယ်ဆိုရင် download လုပ်ဖို့ လိုအပ်တယ်။  

```
(base) ye@:/media/ye/project2/data/umbc-en$ wc UMBC_tokenized_full.txt 
    40599164  3337113760 18786225225 UMBC_tokenized_full.txt
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ ll -h  UMBC_tokenized_full.txt 
-rwxr-xr-x 1 ye ye 18G စက်   26 14:45 UMBC_tokenized_full.txt*
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ head ./UMBC_tokenized_full.txt 
Caucasian skin color on the penis can vary , with the glans being darker than the shaft of the penis , primarily due to increased surface vascularity . Scarring and inflammation can leave less pigmented areas on the penile skin which can look like skin color variation . 
If what you are noticing is new to you , it bears an exam to confirm that you do not have a skin infection causing the change . If it has always been that way for you since adolescence , then this is simply your coloration and it is normal . 
This has only happened in the last 3 weeks or so . The end of my penis ( the helmet ) is a white/blue colour . Even when I get an erection the end is still white/blue . On one side it is very rough . The rest of the head goes a normal blood filled red apart from these 2 patches either side . Also my foreskin seems to be a little tighter than usual . 
The following courses are required as the Core for concentrations with a Law , Diversity and Justice emphasis . This Core , combined with other courses through the Fairhaven concentration process and close faculty advisement , provides the basis for varied paths of study exploring the issues of law , diversity and justice in our society . 
This interdisciplinary seminar is an introduction to modern social theory . It employs critical social theories to explore social relationships and examine society from positions of race , class , gender , and sexuality , focusing specifically on the rights , responsibilities and obligations of individuals and communities . Integral to this examination are the experiences of those excluded from the Western ideals of freedom and equality that , arguably , form the basis of liberal democracy . This seminar must be taken either the first quarter or second quarter of enrollment at Fairhaven . 
Study of the American legal system and how it affects individuals and society , the structure and evolving nature of the legal system , and legal reasoning and the role of courts in government . Skill development in reading and analyzing court opinions . 
Study of American ideas of rights and liberties , what they mean in practice , competing principles and ideologies at work in the arena of constitutional rights , the history of our justice system with regard to rights and liberties and an exploration of where it is currently headed . 
Through the Concentration process and in close consultation with faculty advisors , students will add courses to the Core and Focus courses from the Fairhaven and WWU course catalogues to develop a concentration tailored to their career or graduate education goals . Faculty advisors will provide detailed information to their advisees about the courses available to them . 
`` I strongly believe that the underlying structures and philosophy of Fairhaven College , the abilities of my professors and the support they provided , coupled with my own interests and approach to learning were critical components to what made college such a positive experience for me . 
The knowledge and skills of my professors , and their manner of communicating , of questioning , and of teaching has many times served significantly as inspiration and motivation for me to learn more , to push beyond my supposed boundaries , and most importantly , to feel able to make mistakes . I feel very lucky to have attended Fairhaven College and for the education I gained from it . '' 
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ tail ./UMBC_tokenized_full.txt 
Whither went Tammuz ? His destination has already been referred to as `` the bosom of the earth '' , and in the Assyrian version of the `` Descent of Ishtar '' he dwells in `` the house of darkness '' among the dead , `` where dust is their nourishment and their food mud '' , and `` the light is never seen '' -- the gloomy Babylonian Hades . In one of the Sumerian hymns , however , it is stated that Tammuz `` upon the flood was cast out '' . The reference may be to the submarine `` house of Ea '' , or the Blessed Island to which the Babylonian Noah was carried . In this Hades bloomed the nether `` garden of Adonis '' . 
`` I am Sargon , the mighty King of Akkad . My mother was a vestal ( priestess ) , my father an alien , whose brother inhabited the mountain . . . . When my mother had conceived me , she bare me in a hidden place . She laid me in a vessel of rushes , stopped the door thereof with pitch , and cast me adrift on the river . . . . The river floated me to Akki , the water drawer , who , in drawing water , drew me forth . Akki , the water drawer , educated me as his son , and made me his gardener . As a gardener , I was beloved by the goddess Ishtar . '' 
It is unlikely that this story was invented by Sargon . Like the many variants of it found in other countries , it was probably founded on a form of the Tammuz-Adonis myth . Indeed , a new myth would not have suited Sargon 's purpose so well as the adaptation of an old one , which was more likely to make popular appeal when connected with his name . The references to the goddess Ishtar , and Sargon 's early life as a gardener , suggest that the king desired to be remembered as an agricultural Patriarch , if not of divine , at any rate of semi-divine origin . 
Heimdal , watchman of the Teutonic gods , also dwelt for a time among men as `` Rig '' , and had human offspring , his son Thrall being the ancestor of the Thralls , his son Churl of churls , and Jarl of noblemen . 
I spread like a bird my hands . I descend , I descend to the house of darkness , the dwelling of the god Irkalla : To the house out of which there is no exit , To the road from which there is no return : To the house from whose entrance the light is taken , The place where dust is their nourishment and their food mud . Its chiefs also are like birds covered with feathers ; The light is never seen , in darkness they dwell . . . . 
Keeper of the waters , open thy gate , Open thy gate that I may enter . If thou openest not the gate that I may enter I will strike the door , the bolts I will shatter , p. 96 I will strike the threshold and will pass through the doors ; I will raise up the dead to devour the living , Above the living the dead shall exceed in numbers . 
Let me weep over the strong who have left their wives , Let me weep over the handmaidens who have lost the embraces of their husbands , Over the only son let me mourn , who ere his days are come is taken away . 
May I imprison thee in the great prison , May the garbage of the foundations of the city be thy food , May the drains of the city be thy drink , May the darkness of the dungeon be thy dwelling , May the stake be thy seat , May hunger and thirst strike thy offspring . 
Since thou hast not paid a ransom for thy deliverance to her ( Allatu ) , so to her again turn back , For Tammuz the husband of thy youth . The glistening waters ( of life ) pour over him . In splendid clothing dress him , with a ring of crystal adorn him . 
A Sumerian hymn to Tammuz throws light on this narrative . It sets forth that Ishtar descended to Hades to entreat him to be glad and to resume care of his flocks , but Tammuz refused or was unable to return . 
(base) ye@:/media/ye/project2/data/umbc-en$ 
```

--------------

filesize တွေက အရမ်းကြီးလို့ နောက် မော်ဒယ်တွေ ထွက်လာတဲ့ အခါမှာလည်း နေရာယူနိုင်လို့ ဖိုင်တွေကို project2/ HDD အောက်ကို ရွှေ့လိုက်တယ်။  

မြန်မာစာ corpus က အောက်ပါအတိုင်း...   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ cat corpus2-and-para 3_all.my.word data_myn-token.txt.line.rm-lineno > my_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ wc my_corpus.txt 
   633956  13158666 170988793 my_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ 
```


## Building word2vec and fasttext models

shell script ရေးခဲ့...  

```bash
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ cat ./mk-word2vec-fasttext.sh 
#!/bin/bash

# STEP No. 1: building word2vec and fasttext models
#
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date 25 Sept 2021
# How to run: ./mk-word2vec-fasttext.sh <source-corpus>  <src-output-folder> <target-corpus> <trg-output-folder>
# e.g. ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt /media/ye/project2/exp/bilingual-induction/exp1/en/ 2>&1 | tee my-en.exp1.log
#./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ 2>&1 | tee my-th.exp1.log


echo "change python environment...";
#conda activate bilingual-emb

# Building word2vec
# python3 -i src/train_embeddings.py --corpus YOUR-CORPUS --model YOUR-MODEL --output-directory YOUR-OUTPUT-DIR

# for source
echo "start building a word2vec model for SRC language ...  ";
#time python3 src/train_embeddings.py --corpus $1 --model word2vec --output-directory $2

# for target
echo "start building a word2vec model for TRG language ...  ";
time python3 src/train_embeddings.py --corpus $3 --model word2vec --output-directory $4
 
 # Building fasttext
echo "building a fasttext model for SRC language..."
#time python3 src/train_embeddings.py --corpus $1 --model fasttext --output-directory $2;

echo "building a fasttext model for TRG language..."
time python3 src/train_embeddings.py --corpus $3 --model fasttext --output-directory $4;

echo "check for SRC:  see word2vec and fastext models...";
 ls $2;
echo "check for TRG:  see word2vec and fastext models...";
 ls $4;


(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

Run above shell script...  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings$ ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt /media/ye/project2/exp/bilingual-induction/exp1/en/
...
...
...
2021-09-26 15:58:31,102 : INFO : PROGRESS: at sentence #10570000, processed 50822549 words, keeping 39505036 word types
2021-09-26 15:58:31,445 : INFO : PROGRESS: at sentence #10580000, processed 50866439 words, keeping 39538482 word types
2021-09-26 15:58:31,928 : INFO : PROGRESS: at sentence #10590000, processed 50910957 words, keeping 39572544 word types
2021-09-26 15:58:32,726 : INFO : PROGRESS: at sentence #10600000, processed 50954727 words, keeping 39606533 word types
./mk-word2vec-fasttext.sh: line 23: 172990 Killed                  python3 src/train_embeddings.py --corpus $3 --model word2vec --output-directory $4

real	6m7.060s
user	4m42.179s
sys	0m15.686s
building a fasttext model for SRC language...
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt
2021-09-26 15:59:52,598 : INFO : resetting layer weights
./mk-word2vec-fasttext.sh: line 27: 173138 Killed                  python3 src/train_embeddings.py --corpus $1 --model fasttext --output-directory $2

real	0m12.280s
user	0m4.140s
sys	0m8.344s
building a fasttext model for TRG language...
Loading corpus: /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt
2021-09-26 16:00:04,857 : INFO : resetting layer weights
./mk-word2vec-fasttext.sh: line 30: 173169 Killed                  python3 src/train_embeddings.py --corpus $3 --model fasttext --output-directory $4

real	0m6.203s
user	0m4.110s
sys	0m2.202s
check for SRC:  see word2vec and fastext models...
 3_all.my.word	 corpus2-and-para   data_myn-token.txt.line.rm-lineno   my_corpus.txt  'my_corpus.txt_model=word2vec_vectors.vec'
check for TRG:  see word2vec and fastext models...
1_all.en.word  data_eng.txt
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ memory မနိုင်တာကြောင့်လား?! killed ဖြစ်ကုန်တယ်။
မြန်မာစာအတွက် word2vec model တော့ ဆောက်တာ ပြီးသွားတယ်။
အင်္ဂလိပ်စာအတွက် word2vec မဆောက်နိုင်ခဲ့...
ပြီးတော့ မြန်မာစာအတွက် fasttext မဆောက်နိုင်ခဲ့...
ပြီးတော့ အင်္ဂလိပ်စာအတွက် fasttext မော်ဒယ်လည်း မဆောက်နိုင်ခဲ့တာကို တွေ့ရ...  

coding ကို စစ်ရင်းနဲ့ အောက်ပါ စာကြောင်းကို ပြင်ရမယ်ဆိုတာလည်း သွားတွေ့...  

	corpus = data_manager.ExampleCorpus(args.corpus, sep=', ')
	
sep=' ' ဖြစ်ရမယ် မြန်မာစာအတွက်လည်း...  

## Trying with Thai

အင်္ဂလိပ်စာ ဒေတာ က text တင်ပဲ 17GB ယူတော့ လုပ်မယ်ဆိုရင် ဆောက်ပြီးသား word2vec ကိုပဲ သုံးလိုက်တော့မယ်..  
ထိုင်း corpus ဒေတာနဲ့ run ကြည့်ခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ 2>&1 | tee my-th.exp1.log
...
...
...
2021-09-26 22:19:25,736 : INFO : EPOCH 10 - PROGRESS: at 40.37% examples, 333182 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:26,748 : INFO : EPOCH 10 - PROGRESS: at 46.76% examples, 332569 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:27,772 : INFO : EPOCH 10 - PROGRESS: at 51.86% examples, 331631 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:28,784 : INFO : EPOCH 10 - PROGRESS: at 56.06% examples, 330183 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:29,788 : INFO : EPOCH 10 - PROGRESS: at 63.62% examples, 333872 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:30,796 : INFO : EPOCH 10 - PROGRESS: at 74.36% examples, 340404 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:31,798 : INFO : EPOCH 10 - PROGRESS: at 83.27% examples, 345196 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:32,445 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-26 22:19:32,457 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-26 22:19:32,467 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-26 22:19:32,467 : INFO : EPOCH - 10 : training on 5230564 raw words (4125830 effective words) took 11.8s, 349305 effective words/s
2021-09-26 22:19:32,467 : INFO : training on a 52305640 raw words (41259675 effective words) took 119.1s, 346492 effective words/s
2021-09-26 22:19:33,229 : INFO : storing 28721x300 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=fasttext_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=fasttext_vectors.vec

real	2m28.727s
user	7m12.536s
sys	0m5.877s
check for SRC:  see word2vec and fastext models...
3_all.my.word
corpus2-and-para
corpus2-and-para_model=fasttext_vectors.vec
data_myn-token.txt.line.rm-lineno
my_corpus.txt
my_corpus.txt_model=word2vec_vectors.vec
check for TRG:  see word2vec and fastext models...
2_all.th.word
best.clean.corpus
data_tha-token.txt.line.rm-lineno
th_corpus.txt
th_corpus.txt_model=fasttext_vectors.vec
th_corpus.txt_model=word2vec_vectors.vec
```

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/th$ ll -h *
-rwxr-xr-x 1 ye ye 2.1M စက်   26 03:33  2_all.th.word*
-rwxr-xr-x 1 ye ye  62M စက်   26 03:31  best.clean.corpus*
-rwxr-xr-x 1 ye ye 130K စက်   26 04:36  data_tha-token.txt.line.rm-lineno*
-rwxr-xr-x 1 ye ye  64M စက်   26 21:23  th_corpus.txt*
-rwxr-xr-x 1 ye ye  95M စက်   26 22:19 'th_corpus.txt_model=fasttext_vectors.vec'*
-rwxr-xr-x 1 ye ye  99M စက်   26 22:17 'th_corpus.txt_model=word2vec_vectors.vec'*
```

## Do next Step for my-th

မြန်မာ-ထိုင်း run ဖို့ဆိုရင် dictionary လည်း လိုအပ်တယ်။  
အဲဒါကြောင့် အရင်ဆုံး အင်္ဂလိပ်-ထိုင်း အဘိဓာန်ကနေ အင်္ဂလိပ်စာလုံးတွေကိုပဲ ဖြတ်ထုတ်လိုက်ပြီးတော့ google translate နဲ့ manual ဘာသာပြန်ခိုင်းခဲ့...  
copy/paste English --> google translate into Myanmar ---> copy/paste အလုပ်ကို တရက် လောက် လုပ်လိုက်ရ...   
ပြီးသွားတဲ့အခါမှာ English-Myanmar dictionary ရလာခဲ့...   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ paste ./en-th.dict.f1 ./en2my.google.txt > en-my.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc en-my.raw1
 125530  326180 5231117 en-my.raw1
```

တစ်ခုရှိတာက အဲဒီအထဲမှာ အင်္ဂလိပ်စာလုံးတွေကို ဘာသာပြန်မပေးနိုင်လို့ input ထည့်လိုက်တဲ့ အင်္ဂလိပ်စာလုံးအတိုင်းပဲ ထွက်လာတာတွေလည်း ရှိလို့  
အဲဒီလို ဖြစ်နေတဲ့ pair တွေကို အောက်ပါအတိုင်း awk နဲ့ remove လုပ်လို့ရတယ်...    

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ awk '$1 == $2 { next } { print }' ./test.txt 
abstinent	ထင်ရှားသော
aka	(ခေါ်)
halt	ရပ်နား
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
anesthesiologist	မေ့ဆေးဆရာဝန်
haughtily	မာနကြီး
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

နောက်တစ်ခုက uniq လုပ်ဖို့လည်း လိုအပ်တယ်။  
shell script အဖြစ် ရေးခဲ့...  

```bash
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ cat rm-same-column-and-uniq.sh 
#!/bin/bash

# written by Ye, LST, NECTEC, Thailand
# removing if column1 and column2 are the same. make a uniq file.
# Date: 27 Sept 2021
# How to run: ./rm-same-column-and-uniq.sh <input-file>


inputFile=$1;

awk '$1 == $2 { next } { print }' $inputFile > tmp.out
sort ./tmp.out | uniq > $inputFile.clean

rm tmp.out;
#cat $inputFile.clean
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

test file as follows:   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ cat ./test.txt
Aberdeen	Aberdeen
abstinent	ထင်ရှားသော
AJAX	AJAX
aka	(ခေါ်)
halt	ရပ်နား
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
anagram	anagram
anchovy	anchovy
anesthesiologist	မေ့ဆေးဆရာဝန်
haughtily	မာနကြီး
```

test run...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ ./rm-same-column-and-uniq.sh ./test.txt
abstinent	ထင်ရှားသော
aka	(ခေါ်)
anesthesiologist	မေ့ဆေးဆရာဝန်
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
haughtily	မာနကြီး
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

running for the en-my dictionary:   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ time ./rm-same-column-and-uniq.sh ./en-my.raw1

real	0m0.221s
user	0m0.208s
sys	0m0.025s
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc ./en-my.raw1
 125530  326180 5231117 ./en-my.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc ./en-my.raw1.clean 
  57326  173067 2977748 ./en-my.raw1.clean
```

## Prepare my-th dictionary

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ paste ./en2my.google.txt ./en-th.dict.f2 > ./my-th.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ head ./my-th.raw1 
cheese အကြီးကြီး	เป็นสำนวนแปลว่า คนที่สำคัญมาก
cart la carte	|มีที่มาจากภาษาฝรั่งเศส| การสั่งอาหารที่มีอยู่ในเมนูได้ตามใจชอบ โดยไม่ต้องสั่งเป็นชุดตามที่ร้านอาหารจัดไว้ (ทางประเทศแถบตะวันตก มักมีรายการอาหารเป็นชุดจัดไว้ให้), เมนูหรือรายการอาหารที่มีราคาแยกเฉพาะสำหรับอาหารแต่ละจาน
a la carte ပါ	ดู à la carte (ภาษาฝรั่งเศส), Related: S. à la carte , 
ဝန်တစ်ခု	มาก, มากมาย เช่น a load of rubbish, What a load of muggles.
(တစ်ယောက်) ရဲ့စိတ်တစ်ပိုင်း	คำวิจารณ์หรือตำหนิอย่างตรงไปตรงมาและรุนแรง, เช่น She gave him a piece of her mind. เธอตำหนิเขาตรงๆ อย่างรุนแรง
aardwolf	สัตว์เลี้ยงลูกด้วยนม ออกหากินเวลากลางคืน อาศัยอยู่ในที่ราบตอนใต้ของแอฟริกา กินปลวกและแมลงตัวอ่อนเป็นอาหาร เป็นสัตว์ตระกูลเดียวกับไฮยีน่า
စွန့်လွှတ်ဧကရာဇ်	จักรพรรดิ์ผู้ที่สละราชสมบัติ
Aberdeen	เมืองท่าในตะวันออกเฉียงเหนือของสก็อตแลนด์
ထင်ရှားသော	ที่ค่อยๆกินอย่างไม่มูมมาม, ที่สามารถระงับอารมณ์หรือความอยากได้ดี เช่น the longer the intake, the greater the likelihood that a patient will stay continuously abstinent even after termination of alcohol deterrents.
accordian တံခါး	บานเฟี๊ยม เช่น  The accordion door is pleated with many vertical folds and supported by rollers inserted in a track mounted at the top., Related: S.accordion door 
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ tail ./my-th.raw1 
zootomy	กายวิภาคศาสตร์ที่เกี่ยวกับสัตว์
Zoroaster	ผู้สอนศาสนาชาวเปอร์เซีย
Zoroastrianism	หลักความเชื่อของ Zoroaster
zoster	โรคงูสวัด
ဇူ	เผ่าซูลูในแอฟริกา
ဇူး	เมืองซูริคในประเทศสวิตเซอร์แลนด์
zwitterion	ไอออนซึ่งมีประจุบวกและลบ
zygote	เซลล์ที่เกิดจากการรวมกันของเซลล์เพศสองเซลล์
zygotic ဖြစ်သည်	เกี่ยวกับ zygote
zymurgy	การหมักสุรา
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ 
```

mk-bilingual-dict-train-test.sh ကို run တော့ error ပေးနေခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec/ 2>&1 | tee my-th.mk-bi-dict.log
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/3_all.my.word
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/corpus2-and-para
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/src/get_vocab_from_vectors.py", line 34, in <module>
    w = line.split()[0]
IndexError: list index out of range

real	0m3.662s
user	0m0.632s
sys	0m0.033s
source_vocab.txt
target_vocab.txt
Loading source vocab
Source vocab has 0 words
---
Loading target vocab
Target vocab has 0 words
Loading dictionary - Done 1000 of 125516
Loading dictionary - Done 2000 of 125516
Loading dictionary - Done 3000 of 125516
Loading dictionary - Done 4000 of 125516
...
...
...
Loading dictionary - Done 118000 of 125516
Loading dictionary - Done 119000 of 125516
Loading dictionary - Done 120000 of 125516
Loading dictionary - Done 121000 of 125516
Loading dictionary - Done 122000 of 125516
Loading dictionary - Done 123000 of 125516
Loading dictionary - Done 124000 of 125516
Loading dictionary - Done 125000 of 125516
Loaded 0 entries from the original dictionary, which had: 125516
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/src/split-dictionary.py", line 54, in <module>
    fdf.columns = ['english', 'welsh']
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/generic.py", line 5500, in __setattr__
    return object.__setattr__(self, name, value)
  File "pandas/_libs/properties.pyx", line 70, in pandas._libs.properties.AxisProperty.__set__
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/generic.py", line 766, in _set_axis
    self._mgr.set_axis(axis, labels)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/internals/managers.py", line 216, in set_axis
    self._validate_set_axis(axis, new_labels)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/internals/base.py", line 57, in _validate_set_axis
    raise ValueError(
ValueError: Length mismatch: Expected axis has 0 elements, new values have 2 elements
>>> exit()

real	0m23.072s
user	0m0.832s
sys	0m1.036s
source_vocab.txt
target_vocab.txt
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

အောက်ပါ အတွဲကြောင့်လား?!  

```
zing	้เกิดเสียงดังหวือผ่านไป
```
(vi နဲ့ စစ်ကြည့်တော့ TAB မမြင်ရ)

မဆိုင်ဘူး ပြဿနာက .... mk-bilingual-dict-train-test.sh shell script မှာ note မှတ်ထားခဲ့တဲ့အတိုင်းပါပဲ...   

```
# How to run: ./mk-bilingual-dict-train-test.sh <dictionary> <folder-with-SRC-embeddings> <folder-with-TRG-embeddings> <output-folder-name>
# ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/ 2>&1 | tee my-th.mk-bi-dict.log
# သတိထားရမှာက $2, $3 argument တွေကို ပေးတဲ့အခါမှာ folder name ပေးရမယ်။ ပြီးတော့ အဲဒီ folder အောက်မှာက word2vec ဆိုရင်လည်း word2vec ဖိုင်ပဲ ရှိသင့်တယ်။
# ထိုနည်းလည်းကောင်း fastext နဲ့ bi-lingual induction experiment လုပ်တာဆိုရင်လည်း fasttext model ဖိုင်ပဲ ရှိသင့်တယ်။ ပေးလိုက်တဲ့ folder path အောက်မှာ တခြားဖိုင်တွေရှိနေရင် error ပေးလိမ့်မယ်
```

ဒီတစ်ခေါက် word2vec folder အောက်မှာ word2vec ဖိုင် တစ်ဖိုင်ပဲ ထားပြီး run တော့ အောက်ပါအတိုင်း OK သွားခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/ 2>&1 | tee my-th.mk-bi-dict.log
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/my_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/th_corpus.txt_model=word2vec_vectors.vec
Source vocab is 56038 tokens
Target vocab is 28721 tokens

real	0m3.034s
user	0m1.849s
sys	0m0.161s
source_vocab.txt
target_vocab.txt
Loading source vocab
Source vocab has 56038 words
---
Loading target vocab
Target vocab has 28721 words
Loading dictionary - Done 1000 of 125516
Loading dictionary - Done 2000 of 125516
Loading dictionary - Done 3000 of 125516
Loading dictionary - Done 4000 of 125516
Loading dictionary - Done 5000 of 125516
Loading dictionary - Done 6000 of 125516
Loading dictionary - Done 7000 of 125516
Loading dictionary - Done 8000 of 125516
Loading dictionary - Done 9000 of 125516
Loading dictionary - Done 10000 of 125516
Loading dictionary - Done 11000 of 125516
Loading dictionary - Done 12000 of 125516
Loading dictionary - Done 13000 of 125516
Loading dictionary - Done 14000 of 125516
Loading dictionary - Done 15000 of 125516
Loading dictionary - Done 16000 of 125516
Loading dictionary - Done 17000 of 125516
Loading dictionary - Done 18000 of 125516
Loading dictionary - Done 19000 of 125516
Loading dictionary - Done 20000 of 125516
Loading dictionary - Done 21000 of 125516
Loading dictionary - Done 22000 of 125516
Loading dictionary - Done 23000 of 125516
Loading dictionary - Done 24000 of 125516
Loading dictionary - Done 25000 of 125516
Loading dictionary - Done 26000 of 125516
Loading dictionary - Done 27000 of 125516
Loading dictionary - Done 28000 of 125516
Loading dictionary - Done 29000 of 125516
Loading dictionary - Done 30000 of 125516
Loading dictionary - Done 31000 of 125516
Loading dictionary - Done 32000 of 125516
Loading dictionary - Done 33000 of 125516
Loading dictionary - Done 34000 of 125516
Loading dictionary - Done 35000 of 125516
Loading dictionary - Done 36000 of 125516
Loading dictionary - Done 37000 of 125516
Loading dictionary - Done 38000 of 125516
Loading dictionary - Done 39000 of 125516
Loading dictionary - Done 40000 of 125516
Loading dictionary - Done 41000 of 125516
Loading dictionary - Done 42000 of 125516
Loading dictionary - Done 43000 of 125516
Loading dictionary - Done 44000 of 125516
Loading dictionary - Done 45000 of 125516
Loading dictionary - Done 46000 of 125516
Loading dictionary - Done 47000 of 125516
Loading dictionary - Done 48000 of 125516
Loading dictionary - Done 49000 of 125516
Loading dictionary - Done 50000 of 125516
Loading dictionary - Done 51000 of 125516
Loading dictionary - Done 52000 of 125516
Loading dictionary - Done 53000 of 125516
Loading dictionary - Done 54000 of 125516
Loading dictionary - Done 55000 of 125516
Loading dictionary - Done 56000 of 125516
Loading dictionary - Done 57000 of 125516
Loading dictionary - Done 58000 of 125516
Loading dictionary - Done 59000 of 125516
Loading dictionary - Done 60000 of 125516
Loading dictionary - Done 61000 of 125516
Loading dictionary - Done 62000 of 125516
Loading dictionary - Done 63000 of 125516
Loading dictionary - Done 64000 of 125516
Loading dictionary - Done 65000 of 125516
Loading dictionary - Done 66000 of 125516
Loading dictionary - Done 67000 of 125516
Loading dictionary - Done 68000 of 125516
Loading dictionary - Done 69000 of 125516
Loading dictionary - Done 70000 of 125516
Loading dictionary - Done 71000 of 125516
Loading dictionary - Done 72000 of 125516
Loading dictionary - Done 73000 of 125516
Loading dictionary - Done 74000 of 125516
Loading dictionary - Done 75000 of 125516
Loading dictionary - Done 76000 of 125516
Loading dictionary - Done 77000 of 125516
Loading dictionary - Done 78000 of 125516
Loading dictionary - Done 79000 of 125516
Loading dictionary - Done 80000 of 125516
Loading dictionary - Done 81000 of 125516
Loading dictionary - Done 82000 of 125516
Loading dictionary - Done 83000 of 125516
Loading dictionary - Done 84000 of 125516
Loading dictionary - Done 85000 of 125516
Loading dictionary - Done 86000 of 125516
Loading dictionary - Done 87000 of 125516
Loading dictionary - Done 88000 of 125516
Loading dictionary - Done 89000 of 125516
Loading dictionary - Done 90000 of 125516
Loading dictionary - Done 91000 of 125516
Loading dictionary - Done 92000 of 125516
Loading dictionary - Done 93000 of 125516
Loading dictionary - Done 94000 of 125516
Loading dictionary - Done 95000 of 125516
Loading dictionary - Done 96000 of 125516
Loading dictionary - Done 97000 of 125516
Loading dictionary - Done 98000 of 125516
Loading dictionary - Done 99000 of 125516
Loading dictionary - Done 100000 of 125516
Loading dictionary - Done 101000 of 125516
Loading dictionary - Done 102000 of 125516
Loading dictionary - Done 103000 of 125516
Loading dictionary - Done 104000 of 125516
Loading dictionary - Done 105000 of 125516
Loading dictionary - Done 106000 of 125516
Loading dictionary - Done 107000 of 125516
Loading dictionary - Done 108000 of 125516
Loading dictionary - Done 109000 of 125516
Loading dictionary - Done 110000 of 125516
Loading dictionary - Done 111000 of 125516
Loading dictionary - Done 112000 of 125516
Loading dictionary - Done 113000 of 125516
Loading dictionary - Done 114000 of 125516
Loading dictionary - Done 115000 of 125516
Loading dictionary - Done 116000 of 125516
Loading dictionary - Done 117000 of 125516
Loading dictionary - Done 118000 of 125516
Loading dictionary - Done 119000 of 125516
Loading dictionary - Done 120000 of 125516
Loading dictionary - Done 121000 of 125516
Loading dictionary - Done 122000 of 125516
Loading dictionary - Done 123000 of 125516
Loading dictionary - Done 124000 of 125516
Loading dictionary - Done 125000 of 125516
Loaded 14801 entries from the original dictionary, which had: 125516
>>> 

```

အထက်ပါအတိုင်းဖြစ်နေရင် exit() နဲ့ ထွက်လိုက်ပါ။  


```
>>> exit()

real	4m29.994s
user	0m0.861s
sys	0m1.075s
source_vocab.txt
target_vocab.txt
test_dict.csv
train_dict.csv
```

check the output folder:  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ ls
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ wc *
  56038   56038 1335612 source_vocab.txt
  28721   28721  648843 target_vocab.txt
   2360    4720   97988 test_dict.csv
   9436   18872  390844 train_dict.csv
  96555  108351 2473287 total
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ 
```

ဖိုင်အထဲက စာကြောင်းတွေကိုလည်း head command နဲ့ ဝင်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ head *
==> source_vocab.txt <==
🤠
ရှာလင်ဘတ်
ပေါ်လွင်
ကာဗွန်ဒိုင်အောက်ဆိုက်
မိုင်းယော
အိစ်
စလင်းကွင်း
အဖြူ
သက်ဆိုး
ဆီးကြို

==> target_vocab.txt <==
คากัน
เออร์วิ่ง
ไพรกว้าง
กรมทพ
เซนต์ปีเตอร์
ภายใต้
ธัช
อพยุหะคีรี
เซอร์เบีย
นายกล้านรงค์

==> test_dict.csv <==
english welsh
သဘာဝ ธาตุแท้
ထုပ်ပိုး ห่อหุ้ม
နေ့လည် เที่ยง
ကျော့ကွင်း กับดัก
တောင်ပို့ โคก
ပတ္တာ บานพับ
တိုင်းပြည် ภูมิลำเนา
ဖိနပ် เกือก
မြောက်ဘက် อุดร

==> train_dict.csv <==
english welsh
အလှဆင် ประดับ
ယဲ့ယဲ့ แบบบาง
ပီကင်း กรุงปักกิ่ง
ပို့စ် แจ้ง
သံသယ พิรุธ
ကြည့် สีหน้า
ဝါး เคี้ยว
ဝမ်းနည်း โศกสลด
ရှေးခေတ် โบราณกาล
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$
```

## Study on VecMap Tool

GitHub Link: [https://github.com/artetxem/vecmap](https://github.com/artetxem/vecmap)  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ python ./vecmap/map_embeddings.py --help
usage: map_embeddings.py [-h] [--encoding ENCODING] [--precision {fp16,fp32,fp64}] [--cuda] [--batch_size BATCH_SIZE] [--seed SEED]
                         [--supervised DICTIONARY | --semi_supervised DICTIONARY | --identical | --unsupervised | --acl2018 | --aaai2018 DICTIONARY | --acl2017 | --acl2017_seed DICTIONARY | --emnlp2016 DICTIONARY]
                         [-d DICTIONARY | --init_identical | --init_numerals | --init_unsupervised] [--unsupervised_vocab UNSUPERVISED_VOCAB]
                         [--normalize [{unit,center,unitdim,centeremb,none} ...]] [--whiten] [--src_reweight [SRC_REWEIGHT]]
                         [--trg_reweight [TRG_REWEIGHT]] [--src_dewhiten {src,trg}] [--trg_dewhiten {src,trg}] [--dim_reduction DIM_REDUCTION]
                         [-c | -u] [--self_learning] [--vocabulary_cutoff VOCABULARY_CUTOFF] [--direction {forward,backward,union}]
                         [--csls [NEIGHBORHOOD_SIZE]] [--threshold THRESHOLD] [--validation DICTIONARY] [--stochastic_initial STOCHASTIC_INITIAL]
                         [--stochastic_multiplier STOCHASTIC_MULTIPLIER] [--stochastic_interval STOCHASTIC_INTERVAL] [--log LOG] [-v]
                         src_input trg_input src_output trg_output

Map word embeddings in two languages into a shared space

positional arguments:
  src_input             the input source embeddings
  trg_input             the input target embeddings
  src_output            the output source embeddings
  trg_output            the output target embeddings

optional arguments:
  -h, --help            show this help message and exit
  --encoding ENCODING   the character encoding for input/output (defaults to utf-8)
  --precision {fp16,fp32,fp64}
                        the floating-point precision (defaults to fp32)
  --cuda                use cuda (requires cupy)
  --batch_size BATCH_SIZE
                        batch size (defaults to 10000); does not affect results, larger is usually faster but uses more memory
  --seed SEED           the random seed (defaults to 0)

recommended settings:
  Recommended settings for different scenarios

  --supervised DICTIONARY
                        recommended if you have a large training dictionary
  --semi_supervised DICTIONARY
                        recommended if you have a small seed dictionary
  --identical           recommended if you have no seed dictionary but can rely on identical words
  --unsupervised        recommended if you have no seed dictionary and do not want to rely on identical words
  --acl2018             reproduce our ACL 2018 system
  --aaai2018 DICTIONARY
                        reproduce our AAAI 2018 system
  --acl2017             reproduce our ACL 2017 system with numeral initialization
  --acl2017_seed DICTIONARY
                        reproduce our ACL 2017 system with a seed dictionary
  --emnlp2016 DICTIONARY
                        reproduce our EMNLP 2016 system

advanced initialization arguments:
  Advanced initialization arguments

  -d DICTIONARY, --init_dictionary DICTIONARY
                        the training dictionary file (defaults to stdin)
  --init_identical      use identical words as the seed dictionary
  --init_numerals       use latin numerals (i.e. words matching [0-9]+) as the seed dictionary
  --init_unsupervised   use unsupervised initialization
  --unsupervised_vocab UNSUPERVISED_VOCAB
                        restrict the vocabulary to the top k entries for unsupervised initialization

advanced mapping arguments:
  Advanced embedding mapping arguments

  --normalize [{unit,center,unitdim,centeremb,none} ...]
                        the normalization actions to perform in order
  --whiten              whiten the embeddings
  --src_reweight [SRC_REWEIGHT]
                        re-weight the source language embeddings
  --trg_reweight [TRG_REWEIGHT]
                        re-weight the target language embeddings
  --src_dewhiten {src,trg}
                        de-whiten the source language embeddings
  --trg_dewhiten {src,trg}
                        de-whiten the target language embeddings
  --dim_reduction DIM_REDUCTION
                        apply dimensionality reduction
  -c, --orthogonal      use orthogonal constrained mapping
  -u, --unconstrained   use unconstrained mapping

advanced self-learning arguments:
  Advanced arguments for self-learning

  --self_learning       enable self-learning
  --vocabulary_cutoff VOCABULARY_CUTOFF
                        restrict the vocabulary to the top k entries
  --direction {forward,backward,union}
                        the direction for dictionary induction (defaults to union)
  --csls [NEIGHBORHOOD_SIZE]
                        use CSLS for dictionary induction
  --threshold THRESHOLD
                        the convergence threshold (defaults to 0.000001)
  --validation DICTIONARY
                        a dictionary file for validation at each iteration
  --stochastic_initial STOCHASTIC_INITIAL
                        initial keep probability stochastic dictionary induction (defaults to 0.1)
  --stochastic_multiplier STOCHASTIC_MULTIPLIER
                        stochastic dictionary induction multiplier (defaults to 2.0)
  --stochastic_interval STOCHASTIC_INTERVAL
                        stochastic dictionary induction interval (defaults to 50)
  --log LOG             write to a log file in tsv format at each iteration
  -v, --verbose         write log information to stderr at each iteration
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

## Install CuPy Before Running VeccMap

GPU သုံးမယ်ဆိုရင် လိုအပ်လို့ လက်ရှိ environment မှာ မရှိသေးလို့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ pip install cupy
Collecting cupy
  Downloading cupy-9.4.0.tar.gz (1.7 MB)
     |████████████████████████████████| 1.7 MB 1.8 MB/s 
Requirement already satisfied: numpy<1.24,>=1.17 in /home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages (from cupy) (1.21.2)
Collecting fastrlock>=0.5
  Using cached fastrlock-0.6-cp39-cp39-manylinux1_x86_64.whl (42 kB)
Building wheels for collected packages: cupy
  Building wheel for cupy (setup.py) ... done
  Created wheel for cupy: filename=cupy-9.4.0-cp39-cp39-linux_x86_64.whl size=59578607 sha256=faf3d463d944b6061c5109e920c524d80ffc3fadf05ca3ec7d48bacdee45809f
  Stored in directory: /home/ye/.cache/pip/wheels/26/46/d7/e279499ab39f81388e4b29f0f8d335b5253aa791b68dced02e
Successfully built cupy
Installing collected packages: fastrlock, cupy
Successfully installed cupy-9.4.0 fastrlock-0.6
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

--cuda option နဲ့ run တဲ့အခါမှာ memory error ဆိုပြီးအောက်ပါအတိုင်း ERROR!   

```
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 422, in <module>
    main()
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 349, in main
    dropout(simfwd[:j-i], 1 - keep_prob).argmax(axis=1, out=trg_indices_forward[i:j])
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 32, in dropout
    mask = xp.random.rand(*m.shape) >= p
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_sample.py", line 44, in rand
    return random_sample(size=size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_sample.py", line 156, in random_sample
    return rs.random_sample(size=size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_generator.py", line 618, in random_sample
    out = self._random_sample_raw(size, dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_generator.py", line 600, in _random_sample_raw
    out = cupy.empty(size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/_creation/basic.py", line 22, in empty
    return cupy.ndarray(shape, dtype, order=order)
  File "cupy/_core/core.pyx", line 163, in cupy._core.core.ndarray.__init__
  File "cupy/cuda/memory.pyx", line 718, in cupy.cuda.memory.alloc
  File "cupy/cuda/memory.pyx", line 1395, in cupy.cuda.memory.MemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1416, in cupy.cuda.memory.MemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1096, in cupy.cuda.memory.SingleDeviceMemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1117, in cupy.cuda.memory.SingleDeviceMemoryPool._malloc
  File "cupy/cuda/memory.pyx", line 1355, in cupy.cuda.memory.SingleDeviceMemoryPool._try_malloc
cupy.cuda.memory.OutOfMemoryError: Out of memory allocating 1,600,000,000 bytes (allocated so far: 2,281,307,136 bytes).

real	0m5.425s
user	0m5.231s
sys	0m1.389s
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

အဲဒါကြောင့် --cuda option ကို ဖြုတ်ပြီး run ခဲ့တယ်...  
Running time က semi ကစပြီး ကြာလိမ့်မယ်။  

## Running VecMap

I wrote a shell script as follow:  

```bash
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ cat mk-vecmap.sh 
#!/bin/bash

# STEP No. 3: Doing VecMap (cross-lingual word embedding mappings)
#
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date 28 Sept 2021
# before you run this shell script, I do suggest to learn map_embeddings.py script with "python ./vecmap/map_embeddings.py --help"
# Moreover, don't forget the filename suffixes for running with vecmap_launcher.py python script
# model name - word2vec or fasttext -, and the mc, s and w parameters
# here, mc = mincount, s = size, w - window

# How to run: bash ./mk-vecmap.sh <bilingual-dictionary-filename> <source-embedding-filename> <target-embedding-filename> <output-folder>
# e.g. bash ./mk-vecmap.sh  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/'my_corpus.txt_model=word2vec_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/'th_corpus.txt_model=word2vec_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/ 2>&1 | tee my-th_vecmap.log1
#
# e.g. bash ./mk-vecmap.sh  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my/fasttext/'corpus2-and-para_model=fasttext_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/th/fasttext/'th_corpus.txt_model=fasttext_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-fasttext-output/ 2>&1 | tee my-th_vecmap.log2

# supervised
# Ref: python3 map_embeddings.py --supervised TRAIN.DICT SRC.EMB TRG.EMB SRC_MAPPED.EMB TRG_MAPPED.EMB
time python3 ./vecmap/map_embeddings.py --supervised $1 $2 $3 $4/src_mapped_supervised.emb $4/trg_mapped_supervised.emb

# semi-supervised
# Ref: python3 map_embeddings.py --semi_supervised TRAIN.DICT SRC.EMB TRG.EMB SRC_MAPPED.EMB TRG_MAPPED.EMB
time python3 ./vecmap/map_embeddings.py --semi_supervised $1 $2 $3 $4/src_mapped_semi-supervised.emb $4/trg_mapped_semi-supervised.emb

# identical
# Ref: python3 map_embeddings.py --identical SRC.EMB TRG.EMB SRC_MAPPED.EMB TRG_MAPPED.EMB
time python3 ./vecmap/map_embeddings.py --identical $2 $3 $4/src_mapped_identical.emb $4/trg_mapped_identical.emb

# unsupervised
# Ref: python3 map_embeddings.py --unsupervised SRC.EMB TRG.EMB SRC_MAPPED.EMB TRG_MAPPED.EMB
time python3 ./vecmap/map_embeddings.py --unsupervised $2 $3 $4/src_mapped_unsupervised.emb $4/trg_mapped_unsupervised.emb


(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

Running ...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ bash ./mk-vecmap.sh  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/'my_corpus.txt_model=word2vec_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/'th_corpus.txt_model=word2vec_vectors.vec' /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/ 2>&1 | tee my-th_vecmap.log1
WARNING: OOV dictionary entry (english - welsh)

real	0m9.984s
user	0m13.251s
sys	0m2.689s
WARNING: OOV dictionary entry (english - welsh)
```

အချိန်ကြာတယ် CPU ပေါ်မှာပဲမို့ ပိုကြာလိမ့်မယ်...  
အဲဒါကြောင့် ဒီ shell script ကို run ထားရင်းနဲ့ပဲ နောက် လုပ်စရာရှိတဲ့ အလုပ်တွေကို ဆက်လုပ်ခဲ့...  


## word2vec filenaming

လက်ရှိ word2vec ကို training လုပ်ထားတာက အောက်ပါ settting နဲ့  
(see train_embeddings.py python script)  

```python
	model = modelmap[args.model](size=300, window=5, min_count=3, sentences=corpus, iter=10)
```

အဲဒါကြောင့် ဆောက်ထားတဲ့ word2vec model ကို သတ်မှတ်ထားတဲ့ format အတိုင်း filename ကို ပြောင်းခဲ့...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super$ mv src_mapped_supervised.emb word2vec_s300_mc3_w5.vec
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super$ cd ../trg_super/
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super$ mv trg_mapped_supervised.emb word2vec_s300_mc3_w5.vec
```

## Dictionary Induction and Evaluation

ကျောင်းသားလည်း လိုက်လုပ်ရင် အဆင်ပြေအောင်လို့နဲ့ ကိုယ်တိုင်လည်း ထပ်ခါထပ်ခါ run ရအုံးမှာမို့...  experiment1.sh ဆိုတဲ့ shell script ကို ရေးခဲ့...   

```bash
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ cat experiment1.sh 
#!/bin/bash

# STEP No. 4: bilingual embeddings (e.g. Myanmar-English, Myanmar-Thai)
#
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date 26 Sept 2021
# How to run: ./experiment1.sh <training-dictionary> <mapped-SRC-folder> <mapped-TRG-folder> <test-dictionary> <result-folder>
# e.g. ./experiment1.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/

# Note: vecmap's repository in the home directory of this repo.
# ဒီအဆင့်ကို မလုပ်ခင်မှာ ရှေ့က အဆင်နှစ်ဆင့်ကို (i.e. running mk-word2vec-fasttext.sh နဲ့ mk-bilingual-dict-test.sh) မှန်မှန်ကန်ကန်နဲ့ ကြိုလုပ်ထားမှ ရပါလိမ့်မယ်
# ပြီးတော့ အခု bash script ကို မ run ခင်မှာ vecmap repository ကို လက်ရှိ en-cy-bilingual-embeddings/ ဆိုတဲ့ folder အောက်မှာ git clone လုပ်ထားရပါလိမ့်မယ်။  

# Launch batch VecMap mappings
# The below command will first scan MAPPED-SRC-FOLDER and MAPPED-TRG-FOLDER for embeddings of the same config 
# (model name - word2vec or fasttext -, and the mc, s and w parameters), then apply the supervised variant of VecMap using the --traindict dictionary as supervision.
# 
#python3 src/vecmap_launcher.py --traindict data/resources/dictionaries/train_dict_freqsplit.csv --source-vectors-folder MAPPED-ENG-FOLDER --target-vectors-folder MAPPED-WEL-FOLDER

echo "run vecmap_launcher.py ...";
python3 src/vecmap_launcher.py --traindict $1 --source-vectors-folder $2 --target-vectors-folder $3

# Launch batch dictionary induction evaluation
# REF: python3 src/vecmap_eval_launcher.py --testdict TEST-DICT --source-vectors-folder MAPPED-ENG-FOLDER --target-vectors-folder MAPPED-WEL-FOLDER --results-folder RESULTS-FOLDER

echo "run vecmap_eval_launcher.py ...";
python3 src/vecmap_eval_launcher.py --testdict $4 --source-vectors-folder $2 --target-vectors-folder $3 --results-folder $5


(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```


ဒီ log မမှတ်ခင် ပထမဆုံး run ကြည့်တုန်းက ပေးတဲ့ error က ဖိုင်နာမည်ကို သူသတ်မှတ်ထားတဲ့အတိုင်း မပေးခဲ့လို့ဆိုတာ coding ဝင်ဖတ်ရင်း သိခဲ့ရလို့...   
ဒီတစ်ခါတော့ ဖိုင်နာမည်တွေကို \_s, \_mc, \_w နောက်မှာ parameter တွေကို ထည့်ပေးတာလုပ်ခဲ့...  

လောလောဆယ်က သူ့ default parameter တွေနဲ့ပဲ word2vec မော်ဒယ်ကို ဆောက်ခဲ့တာမို့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./experiment1.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
run vecmap_launcher.py ...
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec
=== CMD ===
python3 vecmap/map_embeddings.py --supervised /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec"
WARNING: OOV dictionary entry (english - welsh)
run vecmap_eval_launcher.py ...

arguments:  Namespace(testdict='/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv', source_vectors_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/', target_vectors_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/', results_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/')
envecs:  ['/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec']
welvecs:  ['/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec']
env:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
enprefix:  word2vec_s ens:  300 enmc:  3 enw:  5
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  nn
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval nn
--------
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  invsoftmax
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval invsoftmax
--------
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  csls
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval csls
--------
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ ls
'model=word2vec_s__retrieval=csls__s=300_mc=3_w=5.txt'        'model=word2vec_s__retrieval=nn__s=300_mc=3_w=5.txt'
'model=word2vec_s__retrieval=invsoftmax__s=300_mc=3_w=5.txt'
```

See the results:  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ cat model\=word2vec_s__retrieval\=nn__s\=300_mc\=3_w\=5.txt 
Coverage: 99.94%  Accuracy:  2.44%
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ cat model\=word2vec_s__retrieval\=invsoftmax__s\=300_mc\=3_w\=5.txt
Coverage: 99.94%  Accuracy:  2.32%
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ cat model\=word2vec_s__retrieval\=csls__s\=300_mc\=3_w\=5.txt 
Coverage: 99.94%  Accuracy:  2.50%
```

Running Process အစအဆုံးတော့ ရသွားပြီ။  

## Current Tree of Myanmar-Thai Experiment Folder

Experiment လုပ်ခဲ့တဲ့ folder tree က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1$ tree
.
├── dict
│   ├── bk
│   │   └── en2my.google.txt.backup
│   ├── en2my.google.txt
│   ├── en-my.raw1
│   ├── en-my.raw1.clean
│   ├── en-th.dict
│   ├── en-th.dict.f1
│   ├── en-th.dict.f2
│   ├── my-en_dict.txt
│   ├── my-th.raw1
│   ├── out
│   ├── rm-same-column-and-uniq.sh
│   ├── test.txt
│   └── test.txt.clean
├── en
│   ├── 1_all.en.word
│   └── data_eng.txt
├── my
│   ├── 3_all.my.word
│   ├── corpus2-and-para
│   ├── data_myn-token.txt.line.rm-lineno
│   ├── fasttext
│   │   └── corpus2-and-para_model=fasttext_vectors.vec
│   ├── my_corpus.txt
│   └── word2vec
│       └── my_corpus.txt_model=word2vec_vectors.vec
├── my-th
│   ├── induction
│   │   ├── model=word2vec_s__retrieval=csls__s=300_mc=3_w=5.txt
│   │   ├── model=word2vec_s__retrieval=invsoftmax__s=300_mc=3_w=5.txt
│   │   └── model=word2vec_s__retrieval=nn__s=300_mc=3_w=5.txt
│   ├── vecmap-fasttext-output
│   ├── vecmap-output
│   │   ├── src_mapped_identical.emb
│   │   ├── src_mapped_semi-supervised.emb
│   │   ├── src_mapped_supervised.emb
│   │   ├── src_super
│   │   │   ├── word2vec_s300_mc3_w5.vec
│   │   │   └── word2vec_s300_mc3_w5.vec_mapped.vec
│   │   ├── trg_mapped_identical.emb
│   │   ├── trg_mapped_semi-supervised.emb
│   │   ├── trg_mapped_supervised.emb
│   │   └── trg_super
│   │       ├── word2vec_s300_mc3_w5.vec
│   │       └── word2vec_s300_mc3_w5.vec_mapped.vec
│   └── word2vec-output
│       ├── model=word2vec_s__retrieval=csls__s=300_mc=3_w=5.txt
│       ├── model=word2vec_s__retrieval=invsoftmax__s=300_mc=3_w=5.txt
│       ├── model=word2vec_s__retrieval=nn__s=300_mc=3_w=5.txt
│       ├── source_vocab.txt
│       ├── target_vocab.txt
│       ├── test_dict.csv
│       └── train_dict.csv
├── note.txt
└── th
    ├── 2_all.th.word
    ├── best.clean.corpus
    ├── data_tha-token.txt.line.rm-lineno
    ├── fasttext
    │   └── th_corpus.txt_model=fasttext_vectors.vec
    ├── th_corpus.txt
    └── word2vec
        └── th_corpus.txt_model=word2vec_vectors.vec

16 directories, 48 files
```

## To Do

- Word2Vec မော်ဒယ်ကို parameter အမျိုးမျိုး ထား model ဆောက်ပြီး evaluation လုပ်ကြည့်ရန်
- fasttext မော်ဒယ်နဲ့လည်း embedding လုပ်ပြီး induction ကို evaluation လုပ်ကြည့်ရန်
- အချိန်ရရင် VecMap mapping ကိုလည်း Supervised, Semi-Supervised, Identical နဲ့ Unsupervised အားလုံးနဲ့ experiment လုပ်ကြည့်ရန်

## Updating the train_embeddings.py

To Do မှာ ရေးထားတဲ့ အချက်တွေကို အကောင်အထည်ဖော်ဖို့အတွက် train_embeddings.py ကို အောက်ပါ argument အသစ်တွေ ထပ်ဖြည့်ခဲ့...  

```python
parser.add_argument('-s', '--size', type=int, default=300, help='Vector Size', required=True)
parser.add_argument('-w', '--window', type=int, default=5, help='Window Size', required=True)
parser.add_argument('-mc', '--min_count', type=int, default=3, help='Minimum Count', required=True)
parser.add_argument('-i', '--iteration', type=int, default=10, help='Iteration', required=True)	
...
...
model = modelmap[args.model](size=args.size, window=args.window, min_count=args.min_count, sentences=corpus, iter=args.iteration)
```

အဲဒါမှလည်း command line ကနေ သို့မဟုတ် shell script ကနေ size, window, min_count နဲ့ iteration တန်ဖိုးတွေကို argument အဖြစ် pass လုပ်လို့ ရမှာမို့...  

## Testing Updated train_embeddings.py

argument အသစ်တွေထည့်ထားတဲ့ train_embeddings.py ကို စမ်းရင်း parameter တွေကို ပြောင်းပြီး word2vec မော်ဒယ်ကို မြန်မာစာအတွက်ကော၊ ထိုင်းစာအတွက်ကော ဆောက်ကြည့်ခဲ့...  
--size 500 --window 4 --min_count 2 ထားကြည့်ခဲ့ --iteration ကိုတော့ ရှေ့က experiment နဲ့ အတူတူ 10 ပဲထားထားခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ 500 4 2 10 2>&1 | tee my-th.exp1.log2
change python environment...
start building a word2vec model for SRC language ...  
2021-09-28 16:07:32,933 : INFO : collecting all words and their counts
2021-09-28 16:07:33,088 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-28 16:07:33,693 : INFO : PROGRESS: at sentence #10000, processed 404396 words, keeping 14939 word types
2021-09-28 16:07:34,239 : INFO : PROGRESS: at sentence #20000, processed 795992 words, keeping 22404 word types
2021-09-28 16:07:34,786 : INFO : PROGRESS: at sentence #30000, processed 1185635 words, keeping 28543 word types
2021-09-28 16:07:35,314 : INFO : PROGRESS: at sentence #40000, processed 1565097 words, keeping 31906 word types
2021-09-28 16:07:35,844 : INFO : PROGRESS: at sentence #50000, processed 1942659 words, keeping 34985 word types
2021-09-28 16:07:36,083 : INFO : PROGRESS: at sentence #60000, processed 2110765 words, keeping 37539 word types
2021-09-28 16:07:36,431 : INFO : PROGRESS: at sentence #70000, processed 2356771 words, keeping 45277 word types
2021-09-28 16:07:36,761 : INFO : PROGRESS: at sentence #80000, processed 2587997 words, keeping 50975 word types
2021-09-28 16:07:37,073 : INFO : PROGRESS: at sentence #90000, processed 2807378 words, keeping 55860 word types
2021-09-28 16:07:37,439 : INFO : PROGRESS: at sentence #100000, processed 3063817 words, keeping 62206 word types
2021-09-28 16:07:37,723 : INFO : PROGRESS: at sentence #110000, processed 3264765 words, keeping 65474 word types
2021-09-28 16:07:37,994 : INFO : PROGRESS: at sentence #120000, processed 3454083 words, keeping 68501 word types
2021-09-28 16:07:38,258 : INFO : PROGRESS: at sentence #130000, processed 3638371 words, keeping 71517 word types
2021-09-28 16:07:38,540 : INFO : PROGRESS: at sentence #140000, processed 3833731 words, keeping 74424 word types
2021-09-28 16:07:38,800 : INFO : PROGRESS: at sentence #150000, processed 4015385 words, keeping 76225 word types
2021-09-28 16:07:39,046 : INFO : PROGRESS: at sentence #160000, processed 4188425 words, keeping 78178 word types
2021-09-28 16:07:39,335 : INFO : PROGRESS: at sentence #170000, processed 4390456 words, keeping 80136 word types
2021-09-28 16:07:39,699 : INFO : PROGRESS: at sentence #180000, processed 4646631 words, keeping 87082 word types
2021-09-28 16:07:40,132 : INFO : PROGRESS: at sentence #190000, processed 4950304 words, keeping 93402 word types
2021-09-28 16:07:40,455 : INFO : PROGRESS: at sentence #200000, processed 5175174 words, keeping 96795 word types
2021-09-28 16:07:40,661 : INFO : PROGRESS: at sentence #210000, processed 5312555 words, keeping 100982 word types
2021-09-28 16:07:40,940 : INFO : PROGRESS: at sentence #220000, processed 5502552 words, keeping 105536 word types
2021-09-28 16:07:41,094 : INFO : PROGRESS: at sentence #230000, processed 5607012 words, keeping 107965 word types
2021-09-28 16:07:41,487 : INFO : PROGRESS: at sentence #240000, processed 5880528 words, keeping 110626 word types
2021-09-28 16:07:41,866 : INFO : PROGRESS: at sentence #250000, processed 6143958 words, keeping 114520 word types
2021-09-28 16:07:42,414 : INFO : PROGRESS: at sentence #260000, processed 6534771 words, keeping 116197 word types
2021-09-28 16:07:42,966 : INFO : PROGRESS: at sentence #270000, processed 6930916 words, keeping 116225 word types
2021-09-28 16:07:43,507 : INFO : PROGRESS: at sentence #280000, processed 7318094 words, keeping 116254 word types
2021-09-28 16:07:44,046 : INFO : PROGRESS: at sentence #290000, processed 7701231 words, keeping 116270 word types
2021-09-28 16:07:44,589 : INFO : PROGRESS: at sentence #300000, processed 8088365 words, keeping 116283 word types
2021-09-28 16:07:44,894 : INFO : PROGRESS: at sentence #310000, processed 8301041 words, keeping 116293 word types
2021-09-28 16:07:45,214 : INFO : PROGRESS: at sentence #320000, processed 8526343 words, keeping 116400 word types
2021-09-28 16:07:45,547 : INFO : PROGRESS: at sentence #330000, processed 8761044 words, keeping 116472 word types
2021-09-28 16:07:45,846 : INFO : PROGRESS: at sentence #340000, processed 8969964 words, keeping 116504 word types
2021-09-28 16:07:46,217 : INFO : PROGRESS: at sentence #350000, processed 9228172 words, keeping 116532 word types
2021-09-28 16:07:46,535 : INFO : PROGRESS: at sentence #360000, processed 9450439 words, keeping 116558 word types
2021-09-28 16:07:46,782 : INFO : PROGRESS: at sentence #370000, processed 9621180 words, keeping 116574 word types
2021-09-28 16:07:47,067 : INFO : PROGRESS: at sentence #380000, processed 9819398 words, keeping 116589 word types
2021-09-28 16:07:47,345 : INFO : PROGRESS: at sentence #390000, processed 10013810 words, keeping 116601 word types
2021-09-28 16:07:47,609 : INFO : PROGRESS: at sentence #400000, processed 10197753 words, keeping 116611 word types
2021-09-28 16:07:47,861 : INFO : PROGRESS: at sentence #410000, processed 10373478 words, keeping 116634 word types
2021-09-28 16:07:48,122 : INFO : PROGRESS: at sentence #420000, processed 10553764 words, keeping 116648 word types
2021-09-28 16:07:48,497 : INFO : PROGRESS: at sentence #430000, processed 10816871 words, keeping 116665 word types
2021-09-28 16:07:48,903 : INFO : PROGRESS: at sentence #440000, processed 11100208 words, keeping 116703 word types
2021-09-28 16:07:49,269 : INFO : PROGRESS: at sentence #450000, processed 11355526 words, keeping 116724 word types
2021-09-28 16:07:49,444 : INFO : PROGRESS: at sentence #460000, processed 11472977 words, keeping 117201 word types
2021-09-28 16:07:49,706 : INFO : PROGRESS: at sentence #470000, processed 11653157 words, keeping 120451 word types
2021-09-28 16:07:49,859 : INFO : PROGRESS: at sentence #480000, processed 11756694 words, keeping 120953 word types
2021-09-28 16:07:49,985 : INFO : PROGRESS: at sentence #490000, processed 11843806 words, keeping 121253 word types
2021-09-28 16:07:50,135 : INFO : PROGRESS: at sentence #500000, processed 11945450 words, keeping 122251 word types
2021-09-28 16:07:50,304 : INFO : PROGRESS: at sentence #510000, processed 12059808 words, keeping 123004 word types
2021-09-28 16:07:50,423 : INFO : PROGRESS: at sentence #520000, processed 12140699 words, keeping 123218 word types
2021-09-28 16:07:50,550 : INFO : PROGRESS: at sentence #530000, processed 12227537 words, keeping 123537 word types
2021-09-28 16:07:50,666 : INFO : PROGRESS: at sentence #540000, processed 12307214 words, keeping 123548 word types
2021-09-28 16:07:50,788 : INFO : PROGRESS: at sentence #550000, processed 12390648 words, keeping 123557 word types
2021-09-28 16:07:50,924 : INFO : PROGRESS: at sentence #560000, processed 12484502 words, keeping 123573 word types
2021-09-28 16:07:51,067 : INFO : PROGRESS: at sentence #570000, processed 12582381 words, keeping 123583 word types
2021-09-28 16:07:51,187 : INFO : PROGRESS: at sentence #580000, processed 12664130 words, keeping 123593 word types
2021-09-28 16:07:51,312 : INFO : PROGRESS: at sentence #590000, processed 12748588 words, keeping 123601 word types
2021-09-28 16:07:51,452 : INFO : PROGRESS: at sentence #600000, processed 12844413 words, keeping 123604 word types
2021-09-28 16:07:51,586 : INFO : PROGRESS: at sentence #610000, processed 12935798 words, keeping 123611 word types
2021-09-28 16:07:51,724 : INFO : PROGRESS: at sentence #620000, processed 13028189 words, keeping 124636 word types
2021-09-28 16:07:51,864 : INFO : PROGRESS: at sentence #630000, processed 13121681 words, keeping 125801 word types
2021-09-28 16:07:51,920 : INFO : collected 126033 word types from a corpus of 13159108 raw words and 633956 sentences
2021-09-28 16:07:51,920 : INFO : Loading a fresh vocabulary
2021-09-28 16:07:52,077 : INFO : effective_min_count=2 retains 105879 unique words (84% of original 126033, drops 20154)
2021-09-28 16:07:52,077 : INFO : effective_min_count=2 leaves 13138954 word corpus (99% of original 13159108, drops 20154)
2021-09-28 16:07:52,216 : INFO : deleting the raw counts dictionary of 126033 items
2021-09-28 16:07:52,218 : INFO : sample=0.001 downsamples 65 most-common words
2021-09-28 16:07:52,218 : INFO : downsampling leaves estimated 9842694 word corpus (74.9% of prior 13138954)
2021-09-28 16:07:52,345 : INFO : estimated required memory for 105879 words and 500 dimensions: 476455500 bytes
2021-09-28 16:07:52,345 : INFO : resetting layer weights
2021-09-28 16:08:04,024 : INFO : training model with 3 workers on 105879 vocabulary and 500 features, using sg=0 hs=0 sample=0.001 negative=5 window=4
2021-09-28 16:08:05,061 : INFO : EPOCH 1 - PROGRESS: at 1.99% examples, 373314 words/s, in_qsize 5, out_qsize 3
2021-09-28 16:08:06,071 : INFO : EPOCH 1 - PROGRESS: at 4.55% examples, 425349 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:07,184 : INFO : EPOCH 1 - PROGRESS: at 7.07% examples, 424152 words/s, in_qsize 5, out_qsize 7
2021-09-28 16:08:08,194 : INFO : EPOCH 1 - PROGRESS: at 11.37% examples, 438778 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:09,362 : INFO : EPOCH 1 - PROGRESS: at 15.97% examples, 441301 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:08:10,369 : INFO : EPOCH 1 - PROGRESS: at 21.16% examples, 444960 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:11,384 : INFO : EPOCH 1 - PROGRESS: at 26.46% examples, 444946 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:08:12,467 : INFO : EPOCH 1 - PROGRESS: at 29.98% examples, 442727 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:08:13,472 : INFO : EPOCH 1 - PROGRESS: at 36.02% examples, 446080 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:08:14,523 : INFO : EPOCH 1 - PROGRESS: at 39.71% examples, 447981 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:15,565 : INFO : EPOCH 1 - PROGRESS: at 42.19% examples, 448556 words/s, in_qsize 4, out_qsize 6
2021-09-28 16:08:16,644 : INFO : EPOCH 1 - PROGRESS: at 44.91% examples, 450936 words/s, in_qsize 4, out_qsize 4
2021-09-28 16:08:17,674 : INFO : EPOCH 1 - PROGRESS: at 47.41% examples, 450655 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:08:18,686 : INFO : EPOCH 1 - PROGRESS: at 51.65% examples, 449787 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:08:19,696 : INFO : EPOCH 1 - PROGRESS: at 55.98% examples, 453187 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:20,724 : INFO : EPOCH 1 - PROGRESS: at 60.95% examples, 451375 words/s, in_qsize 6, out_qsize 2
2021-09-28 16:08:21,753 : INFO : EPOCH 1 - PROGRESS: at 66.38% examples, 451536 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:22,800 : INFO : EPOCH 1 - PROGRESS: at 70.01% examples, 451856 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:23,865 : INFO : EPOCH 1 - PROGRESS: at 77.26% examples, 450594 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:24,872 : INFO : EPOCH 1 - PROGRESS: at 87.51% examples, 448619 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:25,932 : INFO : EPOCH 1 - PROGRESS: at 98.36% examples, 446260 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:25,973 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:08:25,975 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:08:25,976 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:08:25,976 : INFO : EPOCH - 1 : training on 13159108 raw words (9842320 effective words) took 22.0s, 448380 effective words/s
2021-09-28 16:08:27,019 : INFO : EPOCH 2 - PROGRESS: at 2.12% examples, 392608 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:08:28,061 : INFO : EPOCH 2 - PROGRESS: at 4.48% examples, 410121 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:08:29,095 : INFO : EPOCH 2 - PROGRESS: at 7.19% examples, 436747 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:30,135 : INFO : EPOCH 2 - PROGRESS: at 11.24% examples, 436165 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:31,185 : INFO : EPOCH 2 - PROGRESS: at 15.59% examples, 442472 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:32,185 : INFO : EPOCH 2 - PROGRESS: at 20.54% examples, 445214 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:08:33,194 : INFO : EPOCH 2 - PROGRESS: at 25.43% examples, 441393 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:34,219 : INFO : EPOCH 2 - PROGRESS: at 29.34% examples, 442313 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:35,245 : INFO : EPOCH 2 - PROGRESS: at 33.90% examples, 441839 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:08:36,268 : INFO : EPOCH 2 - PROGRESS: at 38.49% examples, 440493 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:08:37,348 : INFO : EPOCH 2 - PROGRESS: at 41.41% examples, 442518 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:08:38,376 : INFO : EPOCH 2 - PROGRESS: at 44.06% examples, 446115 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:08:39,425 : INFO : EPOCH 2 - PROGRESS: at 46.66% examples, 447250 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:40,440 : INFO : EPOCH 2 - PROGRESS: at 50.77% examples, 448740 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:41,460 : INFO : EPOCH 2 - PROGRESS: at 54.65% examples, 446696 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:08:42,468 : INFO : EPOCH 2 - PROGRESS: at 59.43% examples, 448981 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:43,556 : INFO : EPOCH 2 - PROGRESS: at 64.78% examples, 447249 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:44,562 : INFO : EPOCH 2 - PROGRESS: at 68.66% examples, 445795 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:08:45,577 : INFO : EPOCH 2 - PROGRESS: at 73.61% examples, 447384 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:08:46,610 : INFO : EPOCH 2 - PROGRESS: at 81.48% examples, 442451 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:08:47,615 : INFO : EPOCH 2 - PROGRESS: at 92.80% examples, 441520 words/s, in_qsize 4, out_qsize 6
2021-09-28 16:08:48,148 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:08:48,159 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:08:48,160 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:08:48,160 : INFO : EPOCH - 2 : training on 13159108 raw words (9841660 effective words) took 22.2s, 443644 effective words/s
2021-09-28 16:08:49,163 : INFO : EPOCH 3 - PROGRESS: at 1.91% examples, 370691 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:08:50,208 : INFO : EPOCH 3 - PROGRESS: at 4.71% examples, 439733 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:08:51,282 : INFO : EPOCH 3 - PROGRESS: at 7.23% examples, 438921 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:08:52,337 : INFO : EPOCH 3 - PROGRESS: at 11.53% examples, 443510 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:08:53,369 : INFO : EPOCH 3 - PROGRESS: at 15.71% examples, 445770 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:08:54,415 : INFO : EPOCH 3 - PROGRESS: at 20.89% examples, 446715 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:08:55,467 : INFO : EPOCH 3 - PROGRESS: at 26.58% examples, 450248 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:08:56,514 : INFO : EPOCH 3 - PROGRESS: at 30.15% examples, 450387 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:08:57,551 : INFO : EPOCH 3 - PROGRESS: at 35.58% examples, 446763 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:08:58,556 : INFO : EPOCH 3 - PROGRESS: at 39.64% examples, 450894 words/s, in_qsize 3, out_qsize 1
2021-09-28 16:08:59,571 : INFO : EPOCH 3 - PROGRESS: at 42.07% examples, 451699 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:00,601 : INFO : EPOCH 3 - PROGRESS: at 44.51% examples, 451367 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:01,605 : INFO : EPOCH 3 - PROGRESS: at 46.98% examples, 451979 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:02,618 : INFO : EPOCH 3 - PROGRESS: at 51.02% examples, 451637 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:03,688 : INFO : EPOCH 3 - PROGRESS: at 55.44% examples, 452546 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:04,742 : INFO : EPOCH 3 - PROGRESS: at 60.57% examples, 452387 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:09:05,864 : INFO : EPOCH 3 - PROGRESS: at 65.95% examples, 449677 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:09:06,911 : INFO : EPOCH 3 - PROGRESS: at 69.96% examples, 452075 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:09:08,010 : INFO : EPOCH 3 - PROGRESS: at 76.91% examples, 449777 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:09:09,061 : INFO : EPOCH 3 - PROGRESS: at 87.13% examples, 446829 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:09:10,123 : INFO : EPOCH 3 - PROGRESS: at 98.02% examples, 444537 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:10,238 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:09:10,240 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:09:10,248 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:09:10,248 : INFO : EPOCH - 3 : training on 13159108 raw words (9842148 effective words) took 22.1s, 445609 effective words/s
2021-09-28 16:09:11,301 : INFO : EPOCH 4 - PROGRESS: at 2.00% examples, 367003 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:09:12,324 : INFO : EPOCH 4 - PROGRESS: at 4.55% examples, 419177 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:09:13,370 : INFO : EPOCH 4 - PROGRESS: at 7.27% examples, 441231 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:14,486 : INFO : EPOCH 4 - PROGRESS: at 11.29% examples, 429722 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:09:15,491 : INFO : EPOCH 4 - PROGRESS: at 15.90% examples, 447512 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:09:16,497 : INFO : EPOCH 4 - PROGRESS: at 20.47% examples, 441100 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:09:17,553 : INFO : EPOCH 4 - PROGRESS: at 26.27% examples, 445239 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:09:18,617 : INFO : EPOCH 4 - PROGRESS: at 29.67% examples, 441016 words/s, in_qsize 6, out_qsize 7
2021-09-28 16:09:19,685 : INFO : EPOCH 4 - PROGRESS: at 35.72% examples, 445182 words/s, in_qsize 3, out_qsize 3
2021-09-28 16:09:20,744 : INFO : EPOCH 4 - PROGRESS: at 39.59% examples, 445741 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:09:21,762 : INFO : EPOCH 4 - PROGRESS: at 42.14% examples, 448867 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:22,925 : INFO : EPOCH 4 - PROGRESS: at 44.67% examples, 445296 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:09:23,938 : INFO : EPOCH 4 - PROGRESS: at 47.62% examples, 451466 words/s, in_qsize 3, out_qsize 1
2021-09-28 16:09:24,979 : INFO : EPOCH 4 - PROGRESS: at 51.47% examples, 446667 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:09:26,035 : INFO : EPOCH 4 - PROGRESS: at 56.02% examples, 450279 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:09:27,061 : INFO : EPOCH 4 - PROGRESS: at 61.36% examples, 450488 words/s, in_qsize 4, out_qsize 4
2021-09-28 16:09:28,192 : INFO : EPOCH 4 - PROGRESS: at 66.75% examples, 448527 words/s, in_qsize 4, out_qsize 7
2021-09-28 16:09:29,192 : INFO : EPOCH 4 - PROGRESS: at 70.37% examples, 450541 words/s, in_qsize 2, out_qsize 1
2021-09-28 16:09:30,273 : INFO : EPOCH 4 - PROGRESS: at 78.15% examples, 447991 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:09:31,315 : INFO : EPOCH 4 - PROGRESS: at 88.14% examples, 445123 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:09:32,308 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:09:32,310 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:09:32,318 : INFO : EPOCH 4 - PROGRESS: at 100.00% examples, 445906 words/s, in_qsize 0, out_qsize 1
2021-09-28 16:09:32,318 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:09:32,318 : INFO : EPOCH - 4 : training on 13159108 raw words (9840983 effective words) took 22.1s, 445904 effective words/s
2021-09-28 16:09:33,380 : INFO : EPOCH 5 - PROGRESS: at 2.12% examples, 385516 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:09:34,478 : INFO : EPOCH 5 - PROGRESS: at 4.71% examples, 416932 words/s, in_qsize 4, out_qsize 7
2021-09-28 16:09:35,484 : INFO : EPOCH 5 - PROGRESS: at 7.39% examples, 442181 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:09:36,517 : INFO : EPOCH 5 - PROGRESS: at 11.64% examples, 442814 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:09:37,529 : INFO : EPOCH 5 - PROGRESS: at 15.78% examples, 447187 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:38,539 : INFO : EPOCH 5 - PROGRESS: at 20.79% examples, 447992 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:39,543 : INFO : EPOCH 5 - PROGRESS: at 25.87% examples, 446280 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:40,596 : INFO : EPOCH 5 - PROGRESS: at 29.56% examples, 444119 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:09:41,611 : INFO : EPOCH 5 - PROGRESS: at 34.27% examples, 444808 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:09:42,676 : INFO : EPOCH 5 - PROGRESS: at 39.13% examples, 445529 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:09:43,711 : INFO : EPOCH 5 - PROGRESS: at 41.65% examples, 445768 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:09:44,733 : INFO : EPOCH 5 - PROGRESS: at 44.39% examples, 450511 words/s, in_qsize 4, out_qsize 4
2021-09-28 16:09:45,734 : INFO : EPOCH 5 - PROGRESS: at 46.91% examples, 451819 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:46,739 : INFO : EPOCH 5 - PROGRESS: at 50.75% examples, 450179 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:09:47,763 : INFO : EPOCH 5 - PROGRESS: at 54.71% examples, 448465 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:09:48,766 : INFO : EPOCH 5 - PROGRESS: at 59.27% examples, 449369 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:09:49,766 : INFO : EPOCH 5 - PROGRESS: at 64.42% examples, 449015 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:50,777 : INFO : EPOCH 5 - PROGRESS: at 68.66% examples, 448945 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:51,781 : INFO : EPOCH 5 - PROGRESS: at 73.31% examples, 449126 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:09:52,817 : INFO : EPOCH 5 - PROGRESS: at 82.48% examples, 447134 words/s, in_qsize 3, out_qsize 2
2021-09-28 16:09:53,819 : INFO : EPOCH 5 - PROGRESS: at 92.95% examples, 444747 words/s, in_qsize 4, out_qsize 2
2021-09-28 16:09:54,409 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:09:54,420 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:09:54,421 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:09:54,421 : INFO : EPOCH - 5 : training on 13159108 raw words (9842998 effective words) took 22.1s, 445338 effective words/s
2021-09-28 16:09:55,464 : INFO : EPOCH 6 - PROGRESS: at 2.03% examples, 378802 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:09:56,565 : INFO : EPOCH 6 - PROGRESS: at 4.51% examples, 402610 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:09:57,593 : INFO : EPOCH 6 - PROGRESS: at 7.35% examples, 439180 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:58,617 : INFO : EPOCH 6 - PROGRESS: at 11.55% examples, 441575 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:09:59,751 : INFO : EPOCH 6 - PROGRESS: at 15.95% examples, 442011 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:10:00,805 : INFO : EPOCH 6 - PROGRESS: at 21.30% examples, 444734 words/s, in_qsize 4, out_qsize 6
2021-09-28 16:10:01,902 : INFO : EPOCH 6 - PROGRESS: at 26.81% examples, 443873 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:10:02,972 : INFO : EPOCH 6 - PROGRESS: at 30.31% examples, 442741 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:10:03,975 : INFO : EPOCH 6 - PROGRESS: at 36.47% examples, 443365 words/s, in_qsize 3, out_qsize 4
2021-09-28 16:10:05,017 : INFO : EPOCH 6 - PROGRESS: at 39.67% examples, 443215 words/s, in_qsize 4, out_qsize 6
2021-09-28 16:10:06,026 : INFO : EPOCH 6 - PROGRESS: at 42.31% examples, 448103 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:07,043 : INFO : EPOCH 6 - PROGRESS: at 44.55% examples, 445571 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:10:08,149 : INFO : EPOCH 6 - PROGRESS: at 47.41% examples, 448207 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:10:09,182 : INFO : EPOCH 6 - PROGRESS: at 51.98% examples, 449344 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:10:10,212 : INFO : EPOCH 6 - PROGRESS: at 56.03% examples, 450313 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:10:11,248 : INFO : EPOCH 6 - PROGRESS: at 60.73% examples, 446733 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:10:12,253 : INFO : EPOCH 6 - PROGRESS: at 66.44% examples, 449365 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:13,268 : INFO : EPOCH 6 - PROGRESS: at 69.85% examples, 448992 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:10:14,298 : INFO : EPOCH 6 - PROGRESS: at 75.81% examples, 447280 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:10:15,315 : INFO : EPOCH 6 - PROGRESS: at 86.61% examples, 446041 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:10:16,315 : INFO : EPOCH 6 - PROGRESS: at 96.85% examples, 443833 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:16,536 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:10:16,537 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:10:16,538 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:10:16,538 : INFO : EPOCH - 6 : training on 13159108 raw words (9843940 effective words) took 22.1s, 445099 effective words/s
2021-09-28 16:10:17,540 : INFO : EPOCH 7 - PROGRESS: at 2.12% examples, 408851 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:10:18,589 : INFO : EPOCH 7 - PROGRESS: at 4.43% examples, 413322 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:19,618 : INFO : EPOCH 7 - PROGRESS: at 6.94% examples, 427732 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:20,701 : INFO : EPOCH 7 - PROGRESS: at 10.64% examples, 418353 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:10:21,801 : INFO : EPOCH 7 - PROGRESS: at 15.07% examples, 423652 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:10:22,802 : INFO : EPOCH 7 - PROGRESS: at 20.13% examples, 435716 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:23,805 : INFO : EPOCH 7 - PROGRESS: at 25.35% examples, 437568 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:10:24,822 : INFO : EPOCH 7 - PROGRESS: at 29.35% examples, 440324 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:10:25,911 : INFO : EPOCH 7 - PROGRESS: at 34.20% examples, 440342 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:10:26,928 : INFO : EPOCH 7 - PROGRESS: at 38.89% examples, 441093 words/s, in_qsize 5, out_qsize 3
2021-09-28 16:10:27,931 : INFO : EPOCH 7 - PROGRESS: at 41.45% examples, 442496 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:10:28,958 : INFO : EPOCH 7 - PROGRESS: at 44.15% examples, 446742 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:30,045 : INFO : EPOCH 7 - PROGRESS: at 46.78% examples, 447161 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:10:31,074 : INFO : EPOCH 7 - PROGRESS: at 51.04% examples, 449194 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:10:32,112 : INFO : EPOCH 7 - PROGRESS: at 55.20% examples, 449068 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:10:33,142 : INFO : EPOCH 7 - PROGRESS: at 60.41% examples, 450955 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:10:34,142 : INFO : EPOCH 7 - PROGRESS: at 65.63% examples, 450986 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:35,245 : INFO : EPOCH 7 - PROGRESS: at 69.42% examples, 449065 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:10:36,258 : INFO : EPOCH 7 - PROGRESS: at 75.07% examples, 449098 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:10:37,262 : INFO : EPOCH 7 - PROGRESS: at 85.07% examples, 446923 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:10:38,310 : INFO : EPOCH 7 - PROGRESS: at 95.90% examples, 444731 words/s, in_qsize 5, out_qsize 3
2021-09-28 16:10:38,557 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:10:38,559 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:10:38,567 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:10:38,567 : INFO : EPOCH - 7 : training on 13159108 raw words (9842882 effective words) took 22.0s, 446837 effective words/s
2021-09-28 16:10:39,587 : INFO : EPOCH 8 - PROGRESS: at 2.08% examples, 393760 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:40,627 : INFO : EPOCH 8 - PROGRESS: at 4.55% examples, 422416 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:10:41,696 : INFO : EPOCH 8 - PROGRESS: at 7.23% examples, 437829 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:10:42,706 : INFO : EPOCH 8 - PROGRESS: at 11.45% examples, 445739 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:10:43,733 : INFO : EPOCH 8 - PROGRESS: at 15.40% examples, 441184 words/s, in_qsize 3, out_qsize 7
2021-09-28 16:10:44,811 : INFO : EPOCH 8 - PROGRESS: at 20.63% examples, 443933 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:10:45,832 : INFO : EPOCH 8 - PROGRESS: at 25.96% examples, 444735 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:10:46,847 : INFO : EPOCH 8 - PROGRESS: at 29.72% examples, 446745 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:47,874 : INFO : EPOCH 8 - PROGRESS: at 34.43% examples, 444767 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:48,949 : INFO : EPOCH 8 - PROGRESS: at 39.21% examples, 445092 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:10:49,991 : INFO : EPOCH 8 - PROGRESS: at 41.87% examples, 447732 words/s, in_qsize 5, out_qsize 3
2021-09-28 16:10:51,024 : INFO : EPOCH 8 - PROGRESS: at 44.43% examples, 449449 words/s, in_qsize 4, out_qsize 3
2021-09-28 16:10:52,033 : INFO : EPOCH 8 - PROGRESS: at 46.79% examples, 448311 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:10:53,034 : INFO : EPOCH 8 - PROGRESS: at 50.99% examples, 450623 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:10:54,062 : INFO : EPOCH 8 - PROGRESS: at 55.03% examples, 449574 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:10:55,125 : INFO : EPOCH 8 - PROGRESS: at 60.00% examples, 449825 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:56,157 : INFO : EPOCH 8 - PROGRESS: at 65.38% examples, 449963 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:10:57,191 : INFO : EPOCH 8 - PROGRESS: at 69.26% examples, 449679 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:10:58,210 : INFO : EPOCH 8 - PROGRESS: at 74.45% examples, 449348 words/s, in_qsize 3, out_qsize 4
2021-09-28 16:10:59,310 : INFO : EPOCH 8 - PROGRESS: at 84.24% examples, 445108 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:11:00,322 : INFO : EPOCH 8 - PROGRESS: at 94.91% examples, 443177 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:11:00,685 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:11:00,686 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:11:00,688 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:11:00,688 : INFO : EPOCH - 8 : training on 13159108 raw words (9842162 effective words) took 22.1s, 444938 effective words/s
2021-09-28 16:11:01,696 : INFO : EPOCH 9 - PROGRESS: at 2.11% examples, 406092 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:11:02,764 : INFO : EPOCH 9 - PROGRESS: at 4.59% examples, 422902 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:11:03,883 : INFO : EPOCH 9 - PROGRESS: at 7.19% examples, 426544 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:11:04,900 : INFO : EPOCH 9 - PROGRESS: at 11.29% examples, 432850 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:11:05,903 : INFO : EPOCH 9 - PROGRESS: at 15.78% examples, 446891 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:06,945 : INFO : EPOCH 9 - PROGRESS: at 20.62% examples, 443179 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:11:07,959 : INFO : EPOCH 9 - PROGRESS: at 26.27% examples, 447546 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:08,981 : INFO : EPOCH 9 - PROGRESS: at 29.55% examples, 443517 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:11:10,013 : INFO : EPOCH 9 - PROGRESS: at 34.19% examples, 442602 words/s, in_qsize 5, out_qsize 5
2021-09-28 16:11:11,103 : INFO : EPOCH 9 - PROGRESS: at 39.08% examples, 442268 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:11:12,105 : INFO : EPOCH 9 - PROGRESS: at 41.78% examples, 446894 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:13,115 : INFO : EPOCH 9 - PROGRESS: at 44.31% examples, 448924 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:14,129 : INFO : EPOCH 9 - PROGRESS: at 46.79% examples, 449369 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:15,140 : INFO : EPOCH 9 - PROGRESS: at 50.83% examples, 449783 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:16,160 : INFO : EPOCH 9 - PROGRESS: at 54.90% examples, 449424 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:11:17,166 : INFO : EPOCH 9 - PROGRESS: at 59.72% examples, 450848 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:18,169 : INFO : EPOCH 9 - PROGRESS: at 64.68% examples, 449493 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:11:19,190 : INFO : EPOCH 9 - PROGRESS: at 68.65% examples, 447952 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:11:20,285 : INFO : EPOCH 9 - PROGRESS: at 73.67% examples, 447970 words/s, in_qsize 5, out_qsize 7
2021-09-28 16:11:21,361 : INFO : EPOCH 9 - PROGRESS: at 84.24% examples, 446737 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:11:22,403 : INFO : EPOCH 9 - PROGRESS: at 95.56% examples, 445319 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:11:22,686 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:11:22,688 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:11:22,697 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:11:22,697 : INFO : EPOCH - 9 : training on 13159108 raw words (9844178 effective words) took 22.0s, 447294 effective words/s
2021-09-28 16:11:23,703 : INFO : EPOCH 10 - PROGRESS: at 2.07% examples, 399675 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:24,719 : INFO : EPOCH 10 - PROGRESS: at 4.59% examples, 434271 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:25,760 : INFO : EPOCH 10 - PROGRESS: at 6.95% examples, 429961 words/s, in_qsize 6, out_qsize 6
2021-09-28 16:11:26,771 : INFO : EPOCH 10 - PROGRESS: at 11.08% examples, 439953 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:11:27,784 : INFO : EPOCH 10 - PROGRESS: at 15.19% examples, 441490 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:11:28,837 : INFO : EPOCH 10 - PROGRESS: at 20.22% examples, 445573 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:11:29,904 : INFO : EPOCH 10 - PROGRESS: at 25.51% examples, 443157 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:11:30,970 : INFO : EPOCH 10 - PROGRESS: at 29.39% examples, 441669 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:11:32,042 : INFO : EPOCH 10 - PROGRESS: at 34.27% examples, 442369 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:11:33,108 : INFO : EPOCH 10 - PROGRESS: at 39.08% examples, 442425 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:11:34,139 : INFO : EPOCH 10 - PROGRESS: at 41.82% examples, 446463 words/s, in_qsize 4, out_qsize 6
2021-09-28 16:11:35,164 : INFO : EPOCH 10 - PROGRESS: at 44.43% examples, 449242 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:11:36,167 : INFO : EPOCH 10 - PROGRESS: at 47.10% examples, 452801 words/s, in_qsize 4, out_qsize 2
2021-09-28 16:11:37,226 : INFO : EPOCH 10 - PROGRESS: at 51.04% examples, 449364 words/s, in_qsize 4, out_qsize 7
2021-09-28 16:11:38,270 : INFO : EPOCH 10 - PROGRESS: at 55.31% examples, 450157 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:11:39,363 : INFO : EPOCH 10 - PROGRESS: at 60.73% examples, 450990 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:11:40,377 : INFO : EPOCH 10 - PROGRESS: at 66.44% examples, 453177 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:11:41,380 : INFO : EPOCH 10 - PROGRESS: at 69.69% examples, 451630 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:11:42,472 : INFO : EPOCH 10 - PROGRESS: at 75.37% examples, 448484 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:11:43,484 : INFO : EPOCH 10 - PROGRESS: at 87.14% examples, 449251 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:11:44,516 : INFO : EPOCH 10 - PROGRESS: at 97.35% examples, 446201 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:11:44,648 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:11:44,651 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:11:44,659 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:11:44,659 : INFO : EPOCH - 10 : training on 13159108 raw words (9842063 effective words) took 22.0s, 448145 effective words/s
2021-09-28 16:11:44,659 : INFO : training on a 131591080 raw words (98425334 effective words) took 220.6s, 446101 effective words/s
2021-09-28 16:11:44,659 : INFO : storing 105879x500 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=word2vec_vectors.vec

real	4m31.132s
user	8m23.835s
sys	0m3.375s
start building a word2vec model for TRG language ...  
2021-09-28 16:12:03,915 : INFO : collecting all words and their counts
2021-09-28 16:12:03,915 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-28 16:12:04,891 : INFO : PROGRESS: at sentence #10000, processed 610756 words, keeping 19454 word types
2021-09-28 16:12:05,592 : INFO : PROGRESS: at sentence #20000, processed 1101607 words, keeping 27158 word types
2021-09-28 16:12:05,883 : INFO : PROGRESS: at sentence #30000, processed 1286807 words, keeping 31927 word types
2021-09-28 16:12:06,197 : INFO : PROGRESS: at sentence #40000, processed 1489810 words, keeping 35328 word types
2021-09-28 16:12:06,510 : INFO : PROGRESS: at sentence #50000, processed 1705793 words, keeping 38701 word types
2021-09-28 16:12:06,846 : INFO : PROGRESS: at sentence #60000, processed 1933905 words, keeping 42599 word types
2021-09-28 16:12:07,207 : INFO : PROGRESS: at sentence #70000, processed 2180748 words, keeping 46212 word types
2021-09-28 16:12:07,752 : INFO : PROGRESS: at sentence #80000, processed 2555380 words, keeping 54008 word types
2021-09-28 16:12:08,435 : INFO : PROGRESS: at sentence #90000, processed 3027559 words, keeping 62852 word types
2021-09-28 16:12:09,209 : INFO : PROGRESS: at sentence #100000, processed 3564854 words, keeping 70996 word types
2021-09-28 16:12:09,659 : INFO : PROGRESS: at sentence #110000, processed 3876595 words, keeping 74656 word types
2021-09-28 16:12:10,029 : INFO : PROGRESS: at sentence #120000, processed 4135019 words, keeping 76320 word types
2021-09-28 16:12:10,469 : INFO : PROGRESS: at sentence #130000, processed 4448732 words, keeping 78290 word types
2021-09-28 16:12:10,904 : INFO : PROGRESS: at sentence #140000, processed 4764187 words, keeping 79958 word types
2021-09-28 16:12:11,320 : INFO : PROGRESS: at sentence #150000, processed 5056619 words, keeping 81906 word types
2021-09-28 16:12:11,434 : INFO : PROGRESS: at sentence #160000, processed 5133769 words, keeping 84736 word types
2021-09-28 16:12:11,549 : INFO : PROGRESS: at sentence #170000, processed 5211641 words, keeping 87195 word types
2021-09-28 16:12:11,579 : INFO : collected 87462 word types from a corpus of 5230564 raw words and 172373 sentences
2021-09-28 16:12:11,579 : INFO : Loading a fresh vocabulary
2021-09-28 16:12:11,638 : INFO : effective_min_count=2 retains 40665 unique words (46% of original 87462, drops 46797)
2021-09-28 16:12:11,638 : INFO : effective_min_count=2 leaves 5183767 word corpus (99% of original 5230564, drops 46797)
2021-09-28 16:12:11,691 : INFO : deleting the raw counts dictionary of 87462 items
2021-09-28 16:12:11,693 : INFO : sample=0.001 downsamples 58 most-common words
2021-09-28 16:12:11,693 : INFO : downsampling leaves estimated 4153223 word corpus (80.1% of prior 5183767)
2021-09-28 16:12:11,740 : INFO : estimated required memory for 40665 words and 500 dimensions: 182992500 bytes
2021-09-28 16:12:11,740 : INFO : resetting layer weights
2021-09-28 16:12:16,366 : INFO : training model with 3 workers on 40665 vocabulary and 500 features, using sg=0 hs=0 sample=0.001 negative=5 window=4
2021-09-28 16:12:17,374 : INFO : EPOCH 1 - PROGRESS: at 4.78% examples, 398484 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:18,377 : INFO : EPOCH 1 - PROGRESS: at 13.65% examples, 450758 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:12:19,391 : INFO : EPOCH 1 - PROGRESS: at 30.91% examples, 461371 words/s, in_qsize 4, out_qsize 2
2021-09-28 16:12:20,402 : INFO : EPOCH 1 - PROGRESS: at 42.88% examples, 458048 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:21,412 : INFO : EPOCH 1 - PROGRESS: at 51.20% examples, 463461 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:12:22,453 : INFO : EPOCH 1 - PROGRESS: at 59.27% examples, 473509 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:23,474 : INFO : EPOCH 1 - PROGRESS: at 72.78% examples, 478986 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:12:24,531 : INFO : EPOCH 1 - PROGRESS: at 82.77% examples, 471502 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:12:24,922 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:12:24,926 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:12:24,931 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:12:24,931 : INFO : EPOCH - 1 : training on 5230564 raw words (4154503 effective words) took 8.6s, 485108 effective words/s
2021-09-28 16:12:25,993 : INFO : EPOCH 2 - PROGRESS: at 5.09% examples, 400070 words/s, in_qsize 6, out_qsize 4
2021-09-28 16:12:27,004 : INFO : EPOCH 2 - PROGRESS: at 15.49% examples, 460069 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:12:28,021 : INFO : EPOCH 2 - PROGRESS: at 32.26% examples, 464220 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:29,064 : INFO : EPOCH 2 - PROGRESS: at 45.41% examples, 472210 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:12:30,074 : INFO : EPOCH 2 - PROGRESS: at 53.28% examples, 480836 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:12:31,092 : INFO : EPOCH 2 - PROGRESS: at 61.67% examples, 484314 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:12:32,109 : INFO : EPOCH 2 - PROGRESS: at 73.83% examples, 480815 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:12:33,151 : INFO : EPOCH 2 - PROGRESS: at 85.40% examples, 481619 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:33,392 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:12:33,395 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:12:33,400 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:12:33,400 : INFO : EPOCH - 2 : training on 5230564 raw words (4152648 effective words) took 8.5s, 490364 effective words/s
2021-09-28 16:12:34,463 : INFO : EPOCH 3 - PROGRESS: at 4.81% examples, 378177 words/s, in_qsize 6, out_qsize 7
2021-09-28 16:12:35,509 : INFO : EPOCH 3 - PROGRESS: at 14.80% examples, 444734 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:12:36,530 : INFO : EPOCH 3 - PROGRESS: at 33.02% examples, 465968 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:37,572 : INFO : EPOCH 3 - PROGRESS: at 45.32% examples, 465972 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:12:38,583 : INFO : EPOCH 3 - PROGRESS: at 53.20% examples, 475620 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:39,654 : INFO : EPOCH 3 - PROGRESS: at 61.84% examples, 478527 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:40,756 : INFO : EPOCH 3 - PROGRESS: at 74.97% examples, 476895 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:12:41,773 : INFO : EPOCH 3 - PROGRESS: at 89.94% examples, 483346 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:12:41,902 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:12:41,905 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:12:41,910 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:12:41,910 : INFO : EPOCH - 3 : training on 5230564 raw words (4153741 effective words) took 8.5s, 488135 effective words/s
2021-09-28 16:12:42,951 : INFO : EPOCH 4 - PROGRESS: at 4.98% examples, 400847 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:43,966 : INFO : EPOCH 4 - PROGRESS: at 13.61% examples, 440288 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:12:44,992 : INFO : EPOCH 4 - PROGRESS: at 31.66% examples, 460222 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:46,024 : INFO : EPOCH 4 - PROGRESS: at 44.69% examples, 464567 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:47,070 : INFO : EPOCH 4 - PROGRESS: at 52.51% examples, 468360 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:12:48,126 : INFO : EPOCH 4 - PROGRESS: at 61.13% examples, 476211 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:12:49,146 : INFO : EPOCH 4 - PROGRESS: at 74.50% examples, 481376 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:12:50,170 : INFO : EPOCH 4 - PROGRESS: at 85.57% examples, 480247 words/s, in_qsize 5, out_qsize 4
2021-09-28 16:12:50,387 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:12:50,395 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:12:50,401 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:12:50,401 : INFO : EPOCH - 4 : training on 5230564 raw words (4152531 effective words) took 8.5s, 489105 effective words/s
2021-09-28 16:12:51,427 : INFO : EPOCH 5 - PROGRESS: at 5.09% examples, 413910 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:12:52,453 : INFO : EPOCH 5 - PROGRESS: at 11.82% examples, 417855 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:12:53,472 : INFO : EPOCH 5 - PROGRESS: at 31.02% examples, 453898 words/s, in_qsize 5, out_qsize 1
2021-09-28 16:12:54,482 : INFO : EPOCH 5 - PROGRESS: at 44.53% examples, 464475 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:12:55,491 : INFO : EPOCH 5 - PROGRESS: at 52.12% examples, 470118 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:12:56,494 : INFO : EPOCH 5 - PROGRESS: at 59.50% examples, 473921 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:12:57,556 : INFO : EPOCH 5 - PROGRESS: at 72.16% examples, 472299 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:12:58,577 : INFO : EPOCH 5 - PROGRESS: at 82.76% examples, 470640 words/s, in_qsize 5, out_qsize 7
2021-09-28 16:12:58,997 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:12:58,998 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:12:59,003 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:12:59,003 : INFO : EPOCH - 5 : training on 5230564 raw words (4152647 effective words) took 8.6s, 482751 effective words/s
2021-09-28 16:13:00,011 : INFO : EPOCH 6 - PROGRESS: at 4.90% examples, 406311 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:01,056 : INFO : EPOCH 6 - PROGRESS: at 11.82% examples, 417907 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:13:02,062 : INFO : EPOCH 6 - PROGRESS: at 29.37% examples, 440126 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:13:03,108 : INFO : EPOCH 6 - PROGRESS: at 42.88% examples, 450314 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:13:04,110 : INFO : EPOCH 6 - PROGRESS: at 51.85% examples, 465580 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:05,148 : INFO : EPOCH 6 - PROGRESS: at 59.27% examples, 468807 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:13:06,161 : INFO : EPOCH 6 - PROGRESS: at 72.16% examples, 472240 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:07,217 : INFO : EPOCH 6 - PROGRESS: at 82.18% examples, 465713 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:13:07,671 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:13:07,672 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:13:07,679 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:13:07,679 : INFO : EPOCH - 6 : training on 5230564 raw words (4153587 effective words) took 8.7s, 478820 effective words/s
2021-09-28 16:13:08,734 : INFO : EPOCH 7 - PROGRESS: at 5.27% examples, 417190 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:13:09,849 : INFO : EPOCH 7 - PROGRESS: at 15.19% examples, 435565 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:13:10,890 : INFO : EPOCH 7 - PROGRESS: at 34.32% examples, 468556 words/s, in_qsize 4, out_qsize 1
2021-09-28 16:13:11,904 : INFO : EPOCH 7 - PROGRESS: at 45.31% examples, 459966 words/s, in_qsize 6, out_qsize 8
2021-09-28 16:13:12,909 : INFO : EPOCH 7 - PROGRESS: at 53.59% examples, 477261 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:13,914 : INFO : EPOCH 7 - PROGRESS: at 62.20% examples, 482271 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:14,919 : INFO : EPOCH 7 - PROGRESS: at 74.53% examples, 481007 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:13:15,934 : INFO : EPOCH 7 - PROGRESS: at 86.00% examples, 483311 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:16,171 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:13:16,175 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:13:16,179 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:13:16,180 : INFO : EPOCH - 7 : training on 5230564 raw words (4151700 effective words) took 8.5s, 488420 effective words/s
2021-09-28 16:13:17,235 : INFO : EPOCH 8 - PROGRESS: at 4.78% examples, 380206 words/s, in_qsize 6, out_qsize 6
2021-09-28 16:13:18,251 : INFO : EPOCH 8 - PROGRESS: at 15.21% examples, 456591 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:13:19,294 : INFO : EPOCH 8 - PROGRESS: at 32.79% examples, 465743 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:20,342 : INFO : EPOCH 8 - PROGRESS: at 45.19% examples, 465241 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:13:21,404 : INFO : EPOCH 8 - PROGRESS: at 53.37% examples, 475054 words/s, in_qsize 4, out_qsize 5
2021-09-28 16:13:22,446 : INFO : EPOCH 8 - PROGRESS: at 62.45% examples, 481431 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:23,460 : INFO : EPOCH 8 - PROGRESS: at 75.24% examples, 484058 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:24,565 : INFO : EPOCH 8 - PROGRESS: at 86.00% examples, 476019 words/s, in_qsize 5, out_qsize 8
2021-09-28 16:13:24,669 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:13:24,672 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:13:24,677 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:13:24,677 : INFO : EPOCH - 8 : training on 5230564 raw words (4153946 effective words) took 8.5s, 488879 effective words/s
2021-09-28 16:13:25,722 : INFO : EPOCH 9 - PROGRESS: at 5.09% examples, 407097 words/s, in_qsize 6, out_qsize 3
2021-09-28 16:13:26,738 : INFO : EPOCH 9 - PROGRESS: at 14.91% examples, 455225 words/s, in_qsize 4, out_qsize 2
2021-09-28 16:13:27,743 : INFO : EPOCH 9 - PROGRESS: at 32.01% examples, 465503 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:28,760 : INFO : EPOCH 9 - PROGRESS: at 44.83% examples, 468423 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:13:29,764 : INFO : EPOCH 9 - PROGRESS: at 52.25% examples, 472296 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:30,835 : INFO : EPOCH 9 - PROGRESS: at 60.21% examples, 474540 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:31,859 : INFO : EPOCH 9 - PROGRESS: at 73.29% examples, 477431 words/s, in_qsize 5, out_qsize 2
2021-09-28 16:13:32,902 : INFO : EPOCH 9 - PROGRESS: at 84.06% examples, 474825 words/s, in_qsize 5, out_qsize 6
2021-09-28 16:13:33,244 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:13:33,250 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:13:33,252 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:13:33,252 : INFO : EPOCH - 9 : training on 5230564 raw words (4154688 effective words) took 8.6s, 484560 effective words/s
2021-09-28 16:13:34,263 : INFO : EPOCH 10 - PROGRESS: at 4.98% examples, 412178 words/s, in_qsize 6, out_qsize 1
2021-09-28 16:13:35,273 : INFO : EPOCH 10 - PROGRESS: at 13.55% examples, 448023 words/s, in_qsize 6, out_qsize 0
2021-09-28 16:13:36,276 : INFO : EPOCH 10 - PROGRESS: at 29.27% examples, 444891 words/s, in_qsize 6, out_qsize 5
2021-09-28 16:13:37,401 : INFO : EPOCH 10 - PROGRESS: at 43.95% examples, 452985 words/s, in_qsize 6, out_qsize 7
2021-09-28 16:13:38,416 : INFO : EPOCH 10 - PROGRESS: at 52.91% examples, 472671 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:39,431 : INFO : EPOCH 10 - PROGRESS: at 60.54% examples, 475142 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:40,444 : INFO : EPOCH 10 - PROGRESS: at 73.31% examples, 476506 words/s, in_qsize 5, out_qsize 0
2021-09-28 16:13:41,452 : INFO : EPOCH 10 - PROGRESS: at 84.24% examples, 476902 words/s, in_qsize 4, out_qsize 4
2021-09-28 16:13:41,825 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-28 16:13:41,827 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-28 16:13:41,833 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-28 16:13:41,833 : INFO : EPOCH - 10 : training on 5230564 raw words (4152206 effective words) took 8.6s, 483910 effective words/s
2021-09-28 16:13:41,833 : INFO : training on a 52305640 raw words (41532197 effective words) took 85.5s, 485944 effective words/s
2021-09-28 16:13:41,833 : INFO : storing 40665x500 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=word2vec_vectors.vec

real	1m45.570s
user	3m16.045s
sys	0m2.221s
check for SRC:  see word2vec and fastext models...
3_all.my.word
corpus2-and-para
data_myn-token.txt.line.rm-lineno
fasttext
my_corpus.txt
my_corpus.txt_model=word2vec_vectors.vec
word2vec
check for TRG:  see word2vec and fastext models...
2_all.th.word
best.clean.corpus
data_tha-token.txt.line.rm-lineno
fasttext
th_corpus.txt
th_corpus.txt_model=word2vec_vectors.vec
word2vec
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

## Write a Shell Script for Evaluation

Evaluation ကို VecMap က ပြင်ဆင်ပေးထားတဲ့ python script ရှိလို့ အဲဒါကို တိုက်ရိုက်သုံးတာလည်း လုပ်လို့ ရလို့ အဲဒီအတွက် shell script တစ်ပုဒ်စမ်းရေးပြီး th-my အတွက် ပြီးနေတဲ့ မော်ဒယ်တွေနဲ့ test run လုပ်ခဲ့။  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date: 28 Sept 2021
# How to run:  ./eval-mapped-embedding.sh <SRC_MAPPED_EMBEDDING> <TRG_MAPPED_EMBEDDING> <TEST_DICT>
# e.g. bash ./eval-mapped-embedding.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv

for ret in {'nn','invnn','invsoftmax','csls'}
do
    echo "--retrieval $ret:";
    time python3 ./vecmap/eval_translation.py $1 $2 -d $3 --retrieval $ret
done
```

အဲဒီလိုလုပ်ရင် ဘာကောင်းသွားလဲ ဆိုတော့ ဖိုင်နာမည်ကို တစ်ခေါက် တစ်ခေါက် \_s, \_w, \_mc format တွေနဲ့ ပြောင်းပေးစရာ မလိုတော့ဘူးပေါ့။ အဲဒီအစား folder မတူတဲ့အထဲမှာပဲ ဖြစ်ဖြစ် ထားထားပြီး evaluation လေးမျိုးစလုံးကို လုပ်လို့ ရတာပေါ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ bash ./eval-mapped-embedding.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv
--retrieval nn:
Coverage: 99.94%  Accuracy:  2.44%

real	0m2.851s
user	0m3.775s
sys	0m1.421s
--retrieval invnn:
Coverage: 99.94%  Accuracy:  1.31%

real	3m19.791s
user	3m39.415s
sys	0m34.057s
--retrieval invsoftmax:
Coverage: 99.94%  Accuracy:  2.32%

real	0m11.953s
user	0m48.297s
sys	0m26.611s
--retrieval csls:
Coverage: 99.94%  Accuracy:  2.50%

real	0m19.903s
user	0m42.891s
sys	0m33.329s
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

## Corpus Info

မြန်မာစာနဲ့ ထိုင်း အတွက်က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ wc my_corpus.txt
   633956  13158666 170988793 my_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ cd ../th
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/th$ wc th_corpus.txt
  172373  5213500 66285708 th_corpus.txt
```

အင်္ဂလိပ်စာအတွက်က အောက်ပါအတိုင်း...    

UMBC ကနေ download လုပ်ယူခဲ့...  

SOURCE: http://ebiquity.umbc.edu/blogger/2013/05/01/umbc-webbase-corpus-of-3b-english-words  
DESCRIPTION: Data from the web, which includes blog posts, news stories, Wikipedia, etc.  
EXTRACTION: Cleaned, tokenized and pre-processed.  

```
(base) ye@:/media/ye/project2/data/umbc-en$ wc ./UMBC_tokenized_full.txt 
   40599164  3337113760 18786225225 ./UMBC_tokenized_full.txt
```

အကုန်လုံးကို သုံးရင် word2vec, fasttext မော်ဒယ်ဆောက်တာ ကြာတာနဲ့ မော်ဒယ်တွေရဲ့ ဖိုင်အရွယ်အစားက အရမ်းကြီးလို့ စာကြောင်းရေ တစ်သန်းကိုပဲ ယူခဲ့...   
ပြီးတော့ experiment က သုံးနေတဲ့ data တွေသိမ်းထားတဲ့ PATH အောက်ကို ကော်ပီကူးယူခဲ့...  
```
(base) ye@:/media/ye/project2/data/umbc-en$ head -n 1000000 ./UMBC_tokenized_full.txt > ./UMBC_tokenized_1million.txt 
(base) ye@:/media/ye/project2/data/umbc-en$ cp ./UMBC_tokenized_1million.txt /media/ye/project2/exp/bilingual-induction/exp1/en/
```

parallel အနည်းငယ်ဖြစ်အောင် ကိုယ်ဖာသာကို ကြိုပြင်ထားတဲ့ အင်္ဂလိပ်စာ ဒေတာက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/en$ wc data_eng.txt 
 1372 12042 60878 data_eng.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/en$ wc 1_all.en.word 
 22031 155519 812550 1_all.en.word
```

သုံးဖိုင်ပေါင်းပြီး ဖြစ်လာတဲ့ corpus size က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/en$ ls
1_all.en.word  big-model  data_eng.txt  UMBC_tokenized_1million.txt  word2vec
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/en$ cat ./UMBC_tokenized_1million.txt 1_all.en.word ./data_eng.txt > en_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/en$ wc ./en_corpus.txt 
  1023403  95322951 529456595 ./en_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induct
```

## Dictionary Info

Experiment လုပ်တဲ့ အခါမှာ word2vec မော်ဒယ်တွေနဲ့ fasttext မော်ဒယ်တွေကသာ အမျိုးမျိုး ပြောင်းသွားပေမဲ့ training/testing အတွက် သုံးခဲ့တဲ့ အဘိဓာန်က အတူတူပါပဲ။ အဲဒါကြောင့် no. of sentences, no. of words က အောက်ပါအတိုင်း ညီပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output2$ wc *
  56038   56038 1335612 source_vocab.txt
  28721   28721  648843 target_vocab.txt
   2360    4720   97988 test_dict.csv
   9436   18872  390844 train_dict.csv
  96555  108351 2473287 total
```

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5$ wc *
  24097   24097 6093336 source_vocab.txt
  28721   28721  648842 target_vocab.txt
   2360    4720   97988 test_dict.csv
   9436   18872  390844 train_dict.csv
  64614   76410 7231010 total
 ```

Format က အောက်ပါအတိုင်းပါ...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5$ head -3 ./train_dict.csv 
english welsh
အလှဆင် ประดับ
ယဲ့ယဲ့ แบบบาง
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5$ head -3 test_dict.csv 
english welsh
သဘာဝ ธาตุแท้
ထုပ်ပိုး ห่อหุ้ม
```

## Write a New Shell Script

Experiment ကို ထပ်ခါထပ်ခါ run ဖို့အတွက်က အောက်ပါ shell script တစ်ခုချင်းစီကို  

 - mk-word2vec-fasttext.sh
 - mk-bilingual-dict-train-test.sh
 - mk-vecmap.sh
 - experiment1.sh

run နေရတာက အရမ်းအဆင်အပြေကြီး မဟုတ်လို့ အားလုံးကို တစ်စုတည်းထားပြီး shell script တစ်ခုတည်းကနေပဲ run ဖို့ ပြင်ဆင်ခဲ့တယ်။   
နာမည်က ./repeat-train-eval.sh    

```bash
#!/bin/bash

# for repeated experiments...
# Written by Ye, LST, NECTEC, Thailand
# Date: 28 Sept 2021
#
# Important Note: run မလုပ်ခင်မှာ အောက်ပါ argument တွေကို စစ်တာ၊ update လုပ်တာ လုပ်ရမယ်။
# ဒီနေရာမှာ အရေးကြီးတာက vector_size, window, min_count, iteration and folder#
# e.g. ./repeat-train-eval.sh 200 3 2 10 4
# e.g. ./repeat-train-eval.sh 100 3 2 10 4
# e.g. ./repeat-train-eval.sh 100 3 2 10 5
# folder အသစ်နာမည်တွေက ... (e.g. word2vec-output$5 နဲ့ vecmap-output$5 တို့အနေနဲ့ ဖြစ်လာလိမ့်မယ်)
# နောက်ပြီးတော့ vecmap ကို run နေတဲ့အချိန်မှာ supervised ပဲ လက်ရှိမှာ ယူခဲ့တယ်။ တကယ်လို့ တခြား approach တွေပါ ယူချင်ရင် mk-vecmap.sh မှာ comment တွေကို ဝင်ဖြုတ်ပါ

echo "build word2vec or fasttext model ...";
./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ $1 $2 $3 $4 2>&1 | tee my-th.exp1.log6

#echo "mkdir word2vec-output$5/";
#mkdir /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$5/;
echo "mkdir fasttext-output$5/";
mkdir /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output$5/;
# if you run for the 1st time, you need to run following statement:  
#./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/fasttext/ /media/ye/project2/exp/bilingual-induction/exp1/th/fasttext/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output$5/

echo "run get_vocab_from_vectors.py ..."
#time python3 src/get_vocab_from_vectors.py --dict /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 --source-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/ --target-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/ --output-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$5/
time python3 src/get_vocab_from_vectors.py --dict /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 --source-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my/fasttext/ --target-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/th/fasttext/ --output-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output$5/

echo "mkdir vecmap-output$5/";
mkdir /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/;

echo "run mk-vecmap.sh ...";
# အဘိဓာန်က ထပ်မဆောက်ချင်လို့ အရင် ရှိပြီးသား path ကိုပဲ fixed လုပ်ပြီးပေးတယ်...
#./mk-vecmap.sh  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=word2vec_vectors.vec /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=word2vec_vectors.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/ 2>&1 | tee my-th_vecmap.log4

./mk-vecmap.sh  /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=fasttext_vectors.vec /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=fasttext_vectors.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/ 2>&1 | tee my-th_vecmap.log6

#Ctrl+C နဲ့ ရပ်လိုက်ပြီး supervised output ပဲ ယူလိုက်...  တာကို မလုပ်ချင်လို့ mk-vecmap.sh ဖိုင်ထဲမှာပဲ comment ပိတ်ထားခဲ့...  

echo "prepare folders and cp ... ";
mkdir /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super;
mkdir /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super;
#cp /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_mapped_supervised.emb /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/word2vec_s$1_mc$3_w$2.vec
#cp /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_mapped_supervised.emb /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/word2vec_s$1_mc$3_w$2.vec
cp /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_mapped_supervised.emb /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/fasttext_s$1_mc$3_w$2.vec
cp /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_mapped_supervised.emb /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/fasttext_s$1_mc$3_w$2.vec

echo "run vecmap_launcher.py script ...";
# အဘိဓာန်က ထပ်မဆောက်ချင်လို့ အရင် ရှိပြီးသား path ကိုပဲ fixed လုပ်ပြီးပေးတယ်...
#python3 src/vecmap_launcher.py --traindict /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv --source-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/ --target-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/
python3 src/vecmap_launcher.py --traindict /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5/train_dict.csv --source-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/ --target-vectors-folder /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/

#output အနေနဲ့က အောက်ပါလိုမျိုး...   
tree /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/

## Evaluation
echo "Evaluation ... "
# အဘိဓာန်က ထပ်မဆောက်ချင်လို့ အရင် ရှိပြီးသား path ကိုပဲ fixed လုပ်ပြီးပေးတယ်...
#bash ./eval-mapped-embedding.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/word2vec_s200_mc2_w3.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/word2vec_s200_mc2_w3.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv
bash ./eval-mapped-embedding.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/src_super/fasttext_s$1_mc$3_w$2.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output$5/trg_super/fasttext_s$1_mc$3_w$2.vec_mapped.vec /media/ye/project2/exp/bilingual-induction/exp1/my-th/fasttext-output5/test_dict.csv

```

run တဲ့အခါမှာတော့  ./repeat-train-eval.sh 200 3 2 10 6   

## All Results

### for Myanmar-Thai (word2vec)

| Vector Size | Window | Min-Count | Retrieval | Coverage | Accuracy |
|-----------:|----------:|--------:|:----------:|---------:|---------:|
| 100 | 3 | 2 | NN | 99.94% | 2.50% |
| 100 | 3 | 2 | Inv-NN | 99.94% | 1.49% |
| 100 | 3 | 2 | Inv-Softmax | 99.94% | 2.03% |
| 100 | 3 | 2 | CSLS | 99.94% | 2.44% |
| 200 | 3 | 2 | NN | 99.94% | 2.80% |
| 200 | 3 | 2 | Inv-NN | 99.94% | 1.91% |
| 200 | 3 | 2 | Inv-Softmax | 99.94% | 2.32% |
| 200 | 3 | 2 | CSLS | 99.94% | 3.16% |
| 300 | 5 | 3 | NN | 99.94% | 2.44% |
| 300 | 5 | 3 | Inv-NN | 99.94% | 1.31% |
| 300 | 5 | 3 | Inv-Softmax | 99.94% | 2.32% |
| 300 | 5 | 3 | CSLS | 99.94% | 2.50% |
| 500 | 4 | 2 | NN | 99.94% | 1.85% |
| 500 | 4 | 2 | Inv-NN | 99.94% | 1.13% |
| 500 | 4 | 2 | Inv-Softmax | 99.94% | 1.49% |
| 500 | 4 | 2 | CSLS | 99.94% | 1.61% |


### for Myanmar-Thai (fasttext)

| Vector Size | Window | Min-Count | Retrieval | Coverage | Accuracy |
|-----------:|----------:|--------:|:----------:|---------:|---------:|
| 100 | 3 | 2 | NN | 99.94% | 1.31% |
| 100 | 3 | 2 | Inv-NN | 99.94% | 0.95% |
| 100 | 3 | 2 | Inv-Softmax | 99.94% | 0.77% |
| 100 | 3 | 2 | CSLS | 99.94% | 1.25% |
| 200 | 3 | 2 | NN | 99.94% | 1.85% |
| 200 | 3 | 2 | Inv-NN | 99.94% | 1.31% |
| 200 | 3 | 2 | Inv-Softmax | 99.94% | 1.73% |
| 200 | 3 | 2 | CSLS | 99.94% | 1.97% |
| 300 | 5 | 3 | NN | 99.94% | 2.14% |
| 300 | 5 | 3 | Inv-NN | 99.94% | 2.14% |
| 300 | 5 | 3 | Inv-Softmax | 99.94% | 2.03% |
| 300 | 5 | 3 | CSLS | 99.94% | 2.68% |
| 500 | 4 | 2 | NN | 99.94% | 2.14% |
| 500 | 4 | 2 | Inv-NN | 99.94% | 2.14% |
| 500 | 4 | 2 | Inv-Softmax | 99.94% | 2.03% |
| 500 | 4 | 2 | CSLS | 99.94% | 2.68% |

### for Myanmar-English (word2vec)

| Vector Size | Window | Min-Count | Retrieval | Coverage | Accuracy |
|-----------:|----------:|--------:|:----------:|---------:|---------:|
| 100 | 3 | 2 | NN | 92.44% | 2.77% |
| 100 | 3 | 2 | Inv-NN | 92.44% | 1.92% |
| 100 | 3 | 2 | Inv-Softmax | 92.44% | 2.31% |
| 100 | 3 | 2 | CSLS | 92.44% | 2.31% |
| 200 | 3 | 2 | NN | 92.64% | 3.28% |
| 200 | 3 | 2 | Inv-NN | 92.64% | 2.28% |
| 200 | 3 | 2 | Inv-Softmax | 92.64% | 3.11% |
| 200 | 3 | 2 | CSLS | 92.64% | 3.50% |
| 300 | 5 | 3 | NN | 91.04% | 3.28% |
| 300 | 5 | 3 | Inv-NN | 91.04% | 1.72% |
| 300 | 5 | 3 | Inv-Softmax | 91.04% | 3.22% |
| 300 | 5 | 3 | CSLS | 91.04% | 3.06% |
| 500 | 4 | 2 | NN | 92.73% | 2.74% |
| 500 | 4 | 2 | Inv-NN | 92.73% | 2.25% |
| 500 | 4 | 2 | Inv-Softmax | 92.73% | 2.74% |
| 500 | 4 | 2 | CSLS | 92.73% | 3.07% |

### for English-Thai (word2vec)

| Vector Size | Window | Min-Count | Retrieval | Coverage | Accuracy |
|-----------:|----------:|--------:|:----------:|---------:|---------:|
| 100 | 3 | 2 | NN | % | % |
| 100 | 3 | 2 | Inv-NN | % | % |
| 100 | 3 | 2 | Inv-Softmax | % | % |
| 100 | 3 | 2 | CSLS | % | % |
| 200 | 3 | 2 | NN | % | % |
| 200 | 3 | 2 | Inv-NN | % | % |
| 200 | 3 | 2 | Inv-Softmax | % | % |
| 200 | 3 | 2 | CSLS | % | % |
| 300 | 5 | 3 | NN | % | % |
| 300 | 5 | 3 | Inv-NN | % | % |
| 300 | 5 | 3 | Inv-Softmax | % | % |
| 300 | 5 | 3 | CSLS | % | % |
| 500 | 4 | 2 | NN | % | % |
| 500 | 4 | 2 | Inv-NN | % | % |
| 500 | 4 | 2 | Inv-Softmax | % | % |
| 500 | 4 | 2 | CSLS | % | % |

## Reference

https://github.com/marekrei/convertvec

Do We Really Need Fully Unsupervised Cross-Lingual Embeddings?:  
https://ie.technion.ac.il/~roiri/papers/EMNLP-Ivan-CLWE.pdf

PanLex-based bilingual lexicons for 210 language pairs (15 languages):  
https://github.com/ivulic/panlex-bli

Low Supervision, Low Corpus size, Low Similarity! Challenges in cross-lingual alignment of word embeddings:  
http://uu.diva-portal.org/smash/get/diva2:1365879/FULLTEXT01.pdf

Cross-lingual word and document embeddings:  
https://www.youtube.com/watch?v=2a-D7L8rdko

How to (Properly) Evaluate Cross-Lingual Word Embeddings:
On Strong Baselines, Comparative Analyses, and Some Misconceptions
https://aclanthology.org/P19-1070.pdf

Lost in Embedding Space: Explaining Cross-Lingual Task Performance with Eigenvalue Divergence:  
https://arxiv.org/pdf/2001.11136v1.pdf


