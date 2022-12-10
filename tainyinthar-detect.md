# ဗမာစာ နဲ့ တိုင်းရင်းသား ဘာသာ စကားတွေကို classification လုပ်ကြည့်ခဲ့တဲ့ Log

## Preprocessing

paste train and dev data and save as new training data:   

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/original/dw-bk$ cat train.bk dev.bk > ./tmp/train.bk
```

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/original/my-rk$ cat train.rk dev.rk > ./tmp/train.rk
```

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ wc *
    670    6818   62657 test.bk
    670    6769   66903 test.dw
   1812   23545  221538 test.my
   1812   23157  217510 test.rk
   5952   61257  560161 train.bk
   5952   60474  597185 train.dw
  16561  211718 1990762 train.my
  16561  208477 1959575 train.rk
  49990  602215 5676291 total
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ 
```

## Prepare the Labels

I defined the labels as follows:  

```
__label__bk
__label__dw
__label__my
__label__rk
```

prepared label only files:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ wc *.label*
   670    670   8040 test.label.bk
   670    670   8040 test.label.dw
  1812   1812  21744 test.label.my
  1812   1812  21744 test.label.rk
  5952   5952  71424 train.label.bk
  5952   5952  71424 train.label.dw
 16561  16561 198732 train.label.my
 16561  16561 198732 train.label.rk
 49990  49990 599880 total
```

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ head -n 2 *.label*
==> test.label.bk <==
__label__bk
__label__bk

==> test.label.dw <==
__label__dw
__label__dw

==> test.label.my <==
__label__my
__label__my

==> test.label.rk <==
__label__rk
__label__rk

==> train.label.bk <==
__label__bk
__label__bk

==> train.label.dw <==
__label__dw
__label__dw

==> train.label.my <==
__label__my
__label__my

==> train.label.rk <==
__label__rk
__label__rk
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$
```

create a new folder and paste with the syllable segmented sentences:  
write a shell script:  
```bash
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ cat paste-all.sh 
#!/bin/bash

paste -d " " test.label.bk test.bk > ./fasttext/test.fasttext.bk
paste -d " " test.label.dw test.dw > ./fasttext/test.fasttext.dw
paste -d " " test.label.my test.my > ./fasttext/test.fasttext.my
paste -d " " test.label.rk test.rk > ./fasttext/test.fasttext.rk

paste -d " " train.label.bk train.bk > ./fasttext/train.fasttext.bk
paste -d " " train.label.dw train.dw > ./fasttext/train.fasttext.dw
paste -d " " train.label.my train.my > ./fasttext/train.fasttext.my
paste -d " " train.label.rk train.rk > ./fasttext/train.fasttext.rk

(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$
```

change mode for the shell script:  
```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ chmod +x paste-all.sh 
```

run paste-all.sh ...  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ ./paste-all.sh 
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess$ cd fasttext/
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ wc *
    670    7488   70697 test.fasttext.bk
    670    7439   74943 test.fasttext.dw
   1812   25357  243282 test.fasttext.my
   1812   24969  239254 test.fasttext.rk
   5952   67209  631585 train.fasttext.bk
   5952   66426  668609 train.fasttext.dw
  16561  228279 2189494 train.fasttext.my
  16561  225038 2158307 train.fasttext.rk
  49990  652205 6276171 total
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ 
```

check the content:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ head -n 3 *.bk
==> test.fasttext.bk <==
__label__bk သူ ခင် ဗျား ကို ဒယ် ဇာ ပေး ဟုတ် ဝ ။
__label__bk နင် ဖယ် သူ့ ဝို စိတ် ညစ် ပေး ခဲ့ လဲ ။
__label__bk သိပ် ပြေ တာ ပေါ့ ။

==> train.fasttext.bk <==
__label__bk နင် ဘာ စီ စဉ် နေ ရယ် ဆို တာ ငါ့ ဝို ပြော သင့် ပေါ့ လန်း ။
__label__bk သူ လို့ စာ အုပ် သုံး ထောင် ကျော် ရောင်း ပီး ဟော ဘီ ။
__label__bk ငယ် ငယ် တည်း က မင်း သား လုပ် ဝို့ ဝါ သ နာ ပါ စ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ head -n 3 *.dw
==> test.fasttext.dw <==
__label__dw အဲ ဝယ် ဟှား ခံ ဗျား ဟှို အဲ ဇာ ပေး ဟှို့ မှု ဝ ။
__label__dw နန် ဟှယ် လူ့ ဟှို ဒုက္ခ ပေး ရစ် ဇာ နူး ။
__label__dw သိပ် ပြေ တာ ပေါ့ ။

==> train.fasttext.dw <==
__label__dw နန် ဟှဲ ဇာ စီ စဉ် နေ ဟှယ် ဆို တာ ငါ့ ကို ပြော သင့် ဟှယ် ။
__label__dw သူး နို့ စာ အုပ် သုံး ထော် ကျော် ရော ပီး ပီ ။
__label__dw ချို့ လူ လေ ဟှာ မွီး ရာ ပါ ဇာတ် မှန်း သား လေ မား ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ head -n 3 *.my
==> test.fasttext.my <==
__label__my  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ဘူး လား ။
__label__my  ကျွန် တော် သာ ဆို ပြန် ပေး လိုက် မှာ ။
__label__my  ဆူ ပြီး တဲ့ ရေ ကို သောက် သ င့် တယ် ။

==> train.fasttext.my <==
__label__my  မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
__label__my  သူ မ ဘယ် သူ့ ကို မှ မ မှတ် မိ တော့ ဘူး ။
__label__my  အဲ့ ဒါ ကျွန် တော် တို့ အ တွက် ခက် ခဲ တယ် ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ head -n 3 *.rk
==> test.fasttext.rk <==
__label__rk  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
__label__rk  ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
__label__rk  ဆူ ပြီး ရီ ကို သောက် သ င့် ရေ ။

==> train.fasttext.rk <==
__label__rk  မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
__label__rk  ထို မ ချေ တစ် ယောက် လေ့ မ မှတ် မိ ပါ ယာ ။
__label__rk  ယင်း ချင့် ကျွန် တော် ရို့ အ တွက် ခက် ခ ရေ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$
```

## Combine All Languages and Make Shuffle

First, combine all languages into a one big file as follows:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ mkdir final
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ cat train.fasttext.{bk,dw,my,rk} > ./final/train.fasttext.all
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ cat test.fasttext.{bk,dw,my,rk} > ./final/test.fasttext.all
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext$ cd final/
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final$ wc *
   4964   65253  628176 test.fasttext.all
  45026  586952 5647995 train.fasttext.all
  49990  652205 6276171 total
```

Shuffle for training and testing:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final$ mkdir shuffle
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final$ ls
shuffle  test.fasttext.all  train.fasttext.all
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final$ shuf ./test.fasttext.all > ./shuffle/test.shuf.all
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final$ shuf ./train.fasttext.all > ./shuffle/train.shuf.all
```

Check the content of the final test data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final/shuffle$ head ./test.shuf.all 
__label__rk  ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။
__label__my  ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။
__label__rk  ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။
__label__dw ကျွန် တော် မွန်း လန်း ဇာ စား နေ တူး ဟှ သူ ဖောင်း ပြော နေ ဟှယ် ။
__label__bk အ မှား လုပ် ဝယ့် ကျောင်း သား ဒေ ဝို ဆ ရာ ဂ ရိုက် ရယ် ။
__label__my  ခင် ဗျား မှာ ကျွန် တော့် နံ ပါတ် ရှိ တယ် လေ ။
__label__rk  ဒေ က လိန့် မေ စွာ စိတ် ရှုပ် လား ဗျာယ် ။
__label__my  သူ တို့ က ဝံ ပု လွေ ကြီး ထွက် ပြေး အောင် ပန်း သီး တွေ နဲ့ ဗုံး ကြဲ သ လို ပစ် ပေါက် ကြ တယ် ။
__label__rk  ဒေ မာ ငါး မျှား စွာ ကို ခွ င့် မ ပြု ပါ ။
__label__bk အယ့် ဒါ ဘ ဇာ လောက် ထင် ရှား ရိ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final/shuffle$ 
```

Check the final content of the training data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final/shuffle$ head ./train.shuf.all 
__label__dw နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။
__label__my  လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။
__label__my  သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။
__label__my  ဒါ ဘယ် သူ့ သွား တိုက် ဆေး လဲ ။
__label__my  ဘယ် အ ချိန် ငွေ လာ ပေး ရ မ လဲ ဆို တာ ကျွန် တော် စဉ်း စား နေ တယ် ။
__label__rk  ယင်း ချင့် ဇာ လောက် တန် ဖိုး ဟိ လေး ။
__label__my  ငါ အိပ် ချင် တယ် ဒါ ပေ မ ယ့် မ အိပ် နိုင် ဘူး ။
__label__rk  ဂီ တ ဟာ မြူး ကြွ စီ ရေ အ ထိ အ ရှိန် မြ င့် ခ ရေ ။
__label__my  ကျွန် တော် တို့ အဲ ဒါ ကို တောင်း ဆို ထား လား ။
__label__dw တ ပည့် ဂန်း များ ရ စာ ရေး တတ် ဝို့ နဲ့ ဖတ် တက် ဝို့ သန် ယူ နေ ရယ် ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/fasttext/final/shuffle$
```

After uploading to the server, I found there are some 2 spaces in training file and thus, I made clean space:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/data/shuffle/clean$ perl ./clean-space.pl ./test.shuf.all > test.shuf.all.clean
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/data/shuffle/clean$ perl ./clean-space.pl ./train.shuf.all > train.shuf.all.clean
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/data/shuffle/clean$ 
```

Check the filesize again:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/data/shuffle/clean$ wc *.clean
   4964   65253  624596 test.shuf.all.clean
  45026  586952 5615376 train.shuf.all.clean
  49990  652205 6239972 total
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/data/shuffle/clean$
```

## Training with FastText

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext supervised -input ../data/shuffle/clean/train.shuf.all.clean -output model-default
Read 0M words
Number of words:  2430
Number of labels: 4
Progress: 100.0% words/sec/thread: 1311061 lr:  0.000000 avg.loss:  0.178538 ETA:   0h 0m 0s

real	0m0.399s
user	0m2.391s
sys	0m0.048s
```

Check the output model:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ ls
model-default.bin  model-default.vec
```

## Testing with Testdata  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext test ./model-default.bin ../data/shuffle/clean/test.shuf.all.clean 
N	4964
P@1	0.954
R@1	0.954

real	0m0.018s
user	0m0.014s
sys	0m0.004s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ 
```

## Training with 3gram

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext supervised -input ../data/shuffle/clean/train.shuf.all.clean -output model-3gram -wordNgrams 3
Read 0M words
Number of words:  2430
Number of labels: 4
Progress: 100.0% words/sec/thread:  874331 lr:  0.000000 avg.loss:  0.143056 ETA:   0h 0m 0s

real	0m5.585s
user	0m4.692s
sys	0m0.681s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$
```

Testing with 3-gram model ...  

Wow! Now we got 97 precision and recall! :)  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext test ./model-3gram.bin ../data/shuffle/clean/test.shuf.all.clean 
N	4964
P@1	0.97
R@1	0.97

real	0m0.367s
user	0m0.056s
sys	0m0.310s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$
```

## Training/Testing with 3-gram and 25 epoch

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext supervised -input ../data/shuffle/clean/train.shuf.all.clean -output model-3gram-25epoch -wordNgrams 3 -epoch 25
Read 0M words
Number of words:  2430
Number of labels: 4
Progress: 100.0% words/sec/thread: 1010528 lr:  0.000000 avg.loss:  0.053030 ETA:   0h 0m 0s

real	0m6.342s
user	0m16.184s
sys	0m0.721s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ 
```

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$ time ../../fasttext test ./model-3gram-25epoch.bin ../data/shuffle/clean/test.shuf.all.clean 
N	4964
P@1	0.968
R@1	0.968

real	0m0.365s
user	0m0.056s
sys	0m0.308s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/dialect-detection/model$
```
