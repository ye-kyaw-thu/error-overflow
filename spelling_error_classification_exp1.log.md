# Spelling Error Type Classification Log

## Data Cleaning

Python script + Manual label cleaning ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python ./print_uniq_labels.py ./error_type.txt
con
con_pho
con_seq
con_typo
dialect
encode
pho
pho_seq
pho_typo
p့o
sensitive
seq
seq_typo
short
slang
slang_seq
slang_typo
stack
typo
typoက်
သ
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Manual search and found:  

```
နှ မျှော် တာ ||| p့o
မှာ   ||| typoက် 
အ   သတ် ||| typo သ 
```

After cleaning labels:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python ./print_uniq_labels.py ./error_type.txt
con
con_pho
con_seq
con_typo
dialect
encode
pho
pho_seq
pho_typo
sensitive
seq
seq_typo
short
slang
slang_seq
slang_typo
stack
typo
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Trailing Spaces Cleaning

label တွေရဲ့ နောက်မှာ trailing spaces တွေက အောက်ပါအတိုင်း ရှိနေတဲ့အတွက် ...   

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head error_type.txt
မား က ဟာ ||| typo
မား တ ယောက် ||| pho
ပါ ဟယ်လ် ။ ||| slang
ပါ ဟယ်လ် ။ ||| slang
တော့ အ သိ ||| typo
ဒီ စ နီး ||| pho
ပြင် စဉ် နေ ||| pho
စာ တ မျက် ||| pho
ပန် စု ||| typo
တ ခု ||| pho
```

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ tail error_type.txt
လည်း ကွီး ယား သွား ||| slang
ကွီး ယား မှာ ||| slang
တဲ့ ကွီး ယား ပဲ ||| slang
  အား ||| typo
ကောင်း မှု့ တို့ ||| pho_typo
မှ မ -ေ _ သ ရုံ ||| sensitive
ခ န ဆို ||| pho
ကို မိ တိ ဆက် ||| typo
ခြေ   နေ ||| typo
တွက် အိမ် မက် ||| pho
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

အောက်ပါ command နဲ့ ရှင်းခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ awk '{$1=$1};1' ./error_type.txt > error_type.clean.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ wc ./error_type.clean.txt
 107957  524005 3941536 ./error_type.clean.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ wc ./error_type.txt
 107957  524005 4054140 ./error_type.txt
```

## FastText Installation

```
(base) ye@lst-gpu-3090:~/tool$ git clone https://github.com/facebookresearch/fastText.git
Cloning into 'fastText'...
remote: Enumerating objects: 3962, done.
remote: Counting objects: 100% (1021/1021), done.
remote: Compressing objects: 100% (164/164), done.
remote: Total 3962 (delta 909), reused 869 (delta 853), pack-reused 2941
Receiving objects: 100% (3962/3962), 8.27 MiB | 11.49 MiB/s, done.
Resolving deltas: 100% (2516/2516), done.
(base) ye@lst-gpu-3090:~/tool$
```

```
(base) ye@lst-gpu-3090:~/tool$ cd fastText/
(base) ye@lst-gpu-3090:~/tool/fastText$ mkdir build && cd build && cmake ..
CMake Deprecation Warning at CMakeLists.txt:9 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.8s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ye/tool/fastText/build
(base) ye@lst-gpu-3090:~/tool/fastText/build$
```

```
(base) ye@lst-gpu-3090:~/tool/fastText/build$ make && sudo make install
[ 31%] Built target fasttext-shared
[ 63%] Built target fasttext-static
[ 95%] Built target fasttext-static_pic
[100%] Built target fasttext-bin
[sudo] password for ye:
[ 31%] Built target fasttext-shared
[ 63%] Built target fasttext-static
[ 95%] Built target fasttext-static_pic
[100%] Built target fasttext-bin
Install the project...
-- Install configuration: ""
-- Installing: /usr/local/lib/pkgconfig/fasttext.pc
-- Installing: /usr/local/lib/libfasttext.so.0
-- Installing: /usr/local/lib/libfasttext.so
-- Installing: /usr/local/lib/libfasttext.a
-- Installing: /usr/local/lib/libfasttext_pic.a
-- Installing: /usr/local/bin/fasttext
-- Installing: /usr/local/include/fasttext/args.h
-- Installing: /usr/local/include/fasttext/autotune.h
-- Installing: /usr/local/include/fasttext/densematrix.h
-- Installing: /usr/local/include/fasttext/dictionary.h
-- Installing: /usr/local/include/fasttext/fasttext.h
-- Installing: /usr/local/include/fasttext/loss.h
-- Installing: /usr/local/include/fasttext/matrix.h
-- Installing: /usr/local/include/fasttext/meter.h
-- Installing: /usr/local/include/fasttext/model.h
-- Installing: /usr/local/include/fasttext/productquantizer.h
-- Installing: /usr/local/include/fasttext/quantmatrix.h
-- Installing: /usr/local/include/fasttext/real.h
-- Installing: /usr/local/include/fasttext/utils.h
-- Installing: /usr/local/include/fasttext/vector.h
(base) ye@lst-gpu-3090:~/tool/fastText/build$
```

call --help  

```
(base) ye@lst-gpu-3090:~/tool/fastText/build$ fasttext --help
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

(base) ye@lst-gpu-3090:~/tool/fastText/build$
```

```
(base) ye@lst-gpu-3090:~/tool/fastText/build$ fasttext supervised --help
Unknown argument: --help

The following arguments are mandatory:
  -input              training file path
  -output             output file path

The following arguments are optional:
  -verbose            verbosity level [2]

The following arguments for the dictionary are optional:
  -minCount           minimal number of word occurences [1]
  -minCountLabel      minimal number of label occurences [0]
  -wordNgrams         max length of word ngram [1]
  -bucket             number of buckets [2000000]
  -minn               min length of char ngram [0]
  -maxn               max length of char ngram [0]
  -t                  sampling threshold [0.0001]
  -label              labels prefix [__label__]

The following arguments for training are optional:
  -lr                 learning rate [0.1]
  -lrUpdateRate       change the rate of updates for the learning rate [100]
  -dim                size of word vectors [100]
  -ws                 size of the context window [5]
  -epoch              number of epochs [5]
  -neg                number of negatives sampled [5]
  -loss               loss function {ns, hs, softmax, one-vs-all} [softmax]
  -thread             number of threads (set to 1 to ensure reproducible results) [12]
  -pretrainedVectors  pretrained word vectors for supervised learning []
  -saveOutput         whether output params should be saved [false]
  -seed               random generator seed  [0]

The following arguments are for autotune:
  -autotune-validation            validation file to be used for evaluation
  -autotune-metric                metric objective {f1, f1:labelname} [f1]
  -autotune-predictions           number of predictions used for evaluation  [1]
  -autotune-duration              maximum duration in seconds [300]
  -autotune-modelsize             constraint model file size [] (empty = do not quantize)

The following arguments for quantization are optional:
  -cutoff             number of words and ngrams to retain [0]
  -retrain            whether embeddings are finetuned if a cutoff is applied [false]
  -qnorm              whether the norm is quantized separately [false]
  -qout               whether the classifier is quantized [false]
  -dsub               size of each sub-vector [2]
(base) ye@lst-gpu-3090:~/tool/fastText/build$
```

## Changed into FastText Label Format

Checked the example data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/eg_data$ wget https://dl.fbaipublicfiles.com/fasttext/data/cooking.stackexchange.tar.gz && tar xvzf cooking.stackexchange.tar.gz
--2023-10-31 21:10:43--  https://dl.fbaipublicfiles.com/fasttext/data/cooking.stackexchange.tar.gz
Resolving dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)... 18.172.202.54, 18.172.202.63, 18.172.202.93, ...
Connecting to dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)|18.172.202.54|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 457609 (447K) [application/x-tar]
Saving to: ‘cooking.stackexchange.tar.gz’

cooking.stackexchange. 100%[==========================>] 446.88K   669KB/s    in 0.7s

2023-10-31 21:10:45 (669 KB/s) - ‘cooking.stackexchange.tar.gz’ saved [457609/457609]

cooking.stackexchange.id
cooking.stackexchange.txt
readme.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/eg_data$
```

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/eg_data$ ls
cooking.stackexchange.id      cooking.stackexchange.txt
cooking.stackexchange.tar.gz  readme.txt
```

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/eg_data$ head cooking.stackexchange.txt
__label__sauce __label__cheese How much does potato starch affect a cheese sauce recipe?
__label__food-safety __label__acidity Dangerous pathogens capable of growing in acidic environments
__label__cast-iron __label__stove How do I cover up the white spots on my cast iron stove?
__label__restaurant Michelin Three Star Restaurant; but if the chef is not there
__label__knife-skills __label__dicing Without knife skills, how can I quickly and accurately dice vegetables?
__label__storage-method __label__equipment __label__bread What's the purpose of a bread box?
__label__baking __label__food-safety __label__substitutions __label__peanuts how to seperate peanut oil from roasted peanuts at home?
__label__chocolate American equivalent for British chocolate terms
__label__baking __label__oven __label__convection Fan bake vs bake
__label__sauce __label__storage-lifetime __label__acidity __label__mayonnaise Regulation and balancing of readymade packed mayonnaise and other sauces
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/eg_data$
```

အရင်ဆုံး ကိုယ့်မှာ ရှိနေတဲ့ ဒေတာကို အောက်ပါပုံစံအတိုင်း ပြင်ဆင်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head error_type.clean.label.txt
မား က ဟာ ||| __label__typo
မား တ ယောက် ||| __label__pho
ပါ ဟယ်လ် ။ ||| __label__slang
ပါ ဟယ်လ် ။ ||| __label__slang
တော့ အ သိ ||| __label__typo
ဒီ စ နီး ||| __label__pho
ပြင် စဉ် နေ ||| __label__pho
စာ တ မျက် ||| __label__pho
ပန် စု ||| __label__typo
တ ခု ||| __label__pho
```

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ tail error_type.clean.label.txt
လည်း ကွီး ယား သွား ||| __label__slang
ကွီး ယား မှာ ||| __label__slang
တဲ့ ကွီး ယား ပဲ ||| __label__slang
အား ||| __label__typo
ကောင်း မှု့ တို့ ||| __label__pho __label__typo
မှ မ -ေ _ သ ရုံ ||| __label__sensitive
ခ န ဆို ||| __label__pho
ကို မိ တိ ဆက် ||| __label__typo
ခြေ နေ ||| __label__typo
တွက် အိမ် မက် ||| __label__pho
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

အဲဒါကိုမှ python script တစ်ပုဒ် ရေးပြီး ကော်လံနှစ်ခုကို swap လုပ်ခဲ့တယ်။  

```python
## Making fasttext training/testing data format
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 31 Oct 2023

import argparse

def convert_format(input_filename, output_filename):
    with open(input_filename, 'r', encoding='utf-8') as infile, open(output_filename, 'w', encoding='utf-8') as outfile:
        for line in infile:
            parts = line.strip().split(' ||| ')
            if len(parts) == 2:
                labels, text = parts[1], parts[0]
                outfile.write(f'{labels} {text}\n')

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Convert file format.')
    parser.add_argument('input_filename', help='The name of the input file')
    parser.add_argument('output_filename', help='The name of the output file')
    args = parser.parse_args()

    convert_format(args.input_filename, args.output_filename)

```

Change the format with following command:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python ./mk_fasttext_format.py error_type.clean.label.txt error_type.all.txt
```


```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head error_type.all.txt
__label__typo မား က ဟာ
__label__pho မား တ ယောက်
__label__slang ပါ ဟယ်လ် ။
__label__slang ပါ ဟယ်လ် ။
__label__typo တော့ အ သိ
__label__pho ဒီ စ နီး
__label__pho ပြင် စဉ် နေ
__label__pho စာ တ မျက်
__label__typo ပန် စု
__label__pho တ ခု
```

Check with tail command:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ tail ./error_type.all.txt
__label__slang လည်း ကွီး ယား သွား
__label__slang ကွီး ယား မှာ
__label__slang တဲ့ ကွီး ယား ပဲ
__label__typo အား
__label__pho __label__typo ကောင်း မှု့ တို့
__label__sensitive မှ မ -ေ _ သ ရုံ
__label__pho ခ န ဆို
__label__typo ကို မိ တိ ဆက်
__label__typo ခြေ နေ
__label__pho တွက် အိမ် မက်
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Shuffling the Corpus

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ shuf ./error_type.all.txt > ./error_type.all.shuf.txt
```

Checked the shuffled data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head ./error_type.all.shuf.txt
__label__typo ကျော် နိင် ပါ
__label__seq ေ န ကို
__label__typo ငယ် ချ ငိး ရေ
__label__pho ထား တ ခု
__label__pho __label__typo သန်း မှု့ တွေ
__label__typo တာ ပဲ့ မြင်
__label__pho ကို ပစ် ဒဏ်
__label__pho တာ တ ခါ
__label__pho အ မ
__label__stack တယ် သ ဘော် သီး
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Checked again with tail command:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ tail ./error_type.all.shuf.txt
__label__typo ရှိ မြို နဲ့
__label__typo အ မ ျိုး သ
__label__typo က ဒါဏ် ရာ
__label__slang လိုက် ထှာ မြင်
__label__typo ကို တး ထ
__label__typo မာ သီး ချင်း
__label__pho နော် အ ကို
__label__typo နှင့် မျှ့ မ
__label__pho ပေါင်း အို ခ
__label__typo ပြ တောင် ခံ
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Check the size of the data/corpus:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ wc ./error_type.all.shuf.txt
 107935  424334 4555783 ./error_type.all.shuf.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Split Training/Testing Data

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head -n 97141 ./error_type.all.shuf.txt > ./train.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ tail -n 10794 ./error_type.all.shuf.txt > ./test.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Check the filesize:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ wc ./train.txt
  97141  381842 4100337 ./train.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ wc test.txt
 10794  42492 455446 test.txt
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Check the file content of train.txt:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head train.txt
__label__typo ကျော် နိင် ပါ
__label__seq ေ န ကို
__label__typo ငယ် ချ ငိး ရေ
__label__pho ထား တ ခု
__label__pho __label__typo သန်း မှု့ တွေ
__label__typo တာ ပဲ့ မြင်
__label__pho ကို ပစ် ဒဏ်
__label__pho တာ တ ခါ
__label__pho အ မ
__label__stack တယ် သ ဘော် သီး
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Check the test.txt:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ head test.txt
__label__typo ကို လှည့် ပ
__label__pho ဝန် ကြ ရာ
__label__pho __label__typo ပုန်း တေ ရှိ
__label__pho နဲ့ အ မ
__label__seq မ အေ ကြာင်း ကို
__label__pho တော့ အဲ နား
__label__slang အာ့ ကြောင့်
__label__pho မွတ် ဆ လင်
__label__pho လူ တ ယောက်
__label__pho တတ် ကျ ဘူး
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

FastText ရဲ့ ဖိုင်နာမည်ပေးတဲ့ ပုံစံအတိုင်းပဲ ထားလိုက်တယ်။  
တကယ်က supervised training မို့လို့ valid ဆိုတာက ပိုမှန်လို့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ cp train.txt error_type.train
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ cp test.txt error_type.valid
```

backup လည်း ကူးထားခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ mv train.txt ./bk
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ mv test.txt ./bk
```

## Training with FastText

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ time fasttext supervised -input error_type.
train -output model.error_type
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:  48.2% words/sec/thread:  957304 lr:  0.051771 avg.loss:  0.738287 ETA:   0h 0m Progress:  95.3% words/sec/thread:  948330 lr:  0.004658 avg.loss:  0.628767 ETA:   0h 0m Progress: 100.0% words/sec/thread:  663220 lr: -0.000002 avg.loss:  0.621014 ETA:   0h 0m Progress: 100.0% words/sec/thread:  662659 lr:  0.000000 avg.loss:  0.621014 ETA:   0h 0m 0s

real    0m0.490s
user    0m2.681s
sys     0m0.036s
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Online Testing

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ fasttext predict model.error_type.bin -
မ အေ ကြာင်း ကို
__label__seq
တတ် ကျ ဘူး
__label__pho
အာ့ ကြောင့်
__label__slang
```

အလုပ်လုပ်ပေးတယ်။  
အိုကေ ဒီတစ်ခါတော့ test file or validation file တစ်ဖိုင်လုံးနဲ့ စမ်းကြည့်မယ်။  

## Testing with Validation File

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ time fasttext test model.error_type.bin err
or_type.valid
N       10794
P@1     0.834
R@1     0.773

real    0m0.021s
user    0m0.012s
sys     0m0.008s
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Compute the precision at five and recall at five with following command:   

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ time fasttext test model.error_type.bin error_type.valid 5
N       10794
P@5     0.214
R@5     0.993

real    0m0.023s
user    0m0.015s
sys     0m0.008s
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Experiment 1

I wrote a shell script as follows:  

```bash
#!/bin/bash

## bash shell script for experiment 1 from epoch 10 to 100 with fastText model
## this is for spelling error type classification
## written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 31 Oct 2023

# Define the input and validation files
train_file="error_type.train"
valid_file="error_type.valid"

# Loop through epochs 10 to 100 with increments of 10
for epoch in $(seq 10 10 100)
do
    echo "Training with epoch $epoch"
    model_file="model.error_type_ep${epoch}"

    # Train the model
    echo "Command: time fasttext supervised -input $train_file -output $model_file -epoch $epoch"
    time fasttext supervised -input $train_file -output $model_file -epoch $epoch

    echo "Testing with epoch $epoch"

    # Test the model
    echo "Command: time fasttext test ${model_file}.bin $valid_file"
    time fasttext test ${model_file}.bin $valid_file

    echo "=========="
done

```

ရလဒ် အပြောင်းအလဲတွေကို သိချင်လို့ epoch ကို 10 ကနေ 100 အထိ +10 လုပ်ပြီး classification experiment လုပ်ကြည့်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ ./exp1.sh | tee exp1.log
Training with epoch 10
Command: time fasttext supervised -input error_type.train -output model.error_type_ep10 -epoch 10
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:  24.0% words/sec/thread:  957258 lr:  0.075951 avg.loss:  0.731544 ETA:   0h 0m Progress:  46.8% words/sec/thread:  931841 lr:  0.053218 avg.loss:  0.638839 ETA:   0h 0m Progress:  69.3% words/sec/thread:  920731 lr:  0.030694 avg.loss:  0.584509 ETA:   0h 0m Progress:  91.8% words/sec/thread:  915345 lr:  0.008152 avg.loss:  0.552224 ETA:   0h 0m Progress: 100.0% words/sec/thread:  797097 lr: -0.000002 avg.loss:  0.541515 ETA:   0h 0m Progress: 100.0% words/sec/thread:  796683 lr:  0.000000 avg.loss:  0.541515 ETA:   0h 0m 0s

real    0m0.699s
user    0m5.399s
sys     0m0.041s
Testing with epoch 10
Command: time fasttext test model.error_type_ep10.bin error_type.valid
N       10794
P@1     0.839
R@1     0.778

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 20
Command: time fasttext supervised -input error_type.train -output model.error_type_ep20 -epoch 20
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:  12.1% words/sec/thread:  963070 lr:  0.087883 avg.loss:  0.743030 ETA:   0h 0m Progress:  23.9% words/sec/thread:  953347 lr:  0.076053 avg.loss:  0.643205 ETA:   0h 0m Progress:  35.6% words/sec/thread:  946218 lr:  0.064372 avg.loss:  0.591526 ETA:   0h 0m Progress:  47.3% words/sec/thread:  942279 lr:  0.052708 avg.loss:  0.562043 ETA:   0h 0m Progress:  59.0% words/sec/thread:  939996 lr:  0.041040 avg.loss:  0.536969 ETA:   0h 0m Progress:  70.6% words/sec/thread:  938580 lr:  0.029364 avg.loss:  0.515973 ETA:   0h 0m Progress:  82.0% words/sec/thread:  934173 lr:  0.017986 avg.loss:  0.504876 ETA:   0h 0m Progress:  93.4% words/sec/thread:  930931 lr:  0.006602 avg.loss:  0.494736 ETA:   0h 0m Progress: 100.0% words/sec/thread:  885909 lr: -0.000001 avg.loss:  0.489362 ETA:   0h 0m Progress: 100.0% words/sec/thread:  885757 lr:  0.000000 avg.loss:  0.489362 ETA:   0h 0m 0s

real    0m1.083s
user    0m10.443s
sys     0m0.048s
Testing with epoch 20
Command: time fasttext test model.error_type_ep20.bin error_type.valid
N       10794
P@1     0.842
R@1     0.781

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 30
Command: time fasttext supervised -input error_type.train -output model.error_type_ep30 -epoch 30
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   8.2% words/sec/thread:  984301 lr:  0.091764 avg.loss:  0.734889 ETA:   0h 0m Progress:  16.4% words/sec/thread:  982889 lr:  0.083559 avg.loss:  0.641134 ETA:   0h 0m Progress:  23.9% words/sec/thread:  953962 lr:  0.076071 avg.loss:  0.596052 ETA:   0h 0m Progress:  31.4% words/sec/thread:  939804 lr:  0.068573 avg.loss:  0.572166 ETA:   0h 0m Progress:  38.9% words/sec/thread:  931364 lr:  0.061073 avg.loss:  0.554712 ETA:   0h 0m Progress:  46.4% words/sec/thread:  925503 lr:  0.053584 avg.loss:  0.537690 ETA:   0h 0m Progress:  53.9% words/sec/thread:  921449 lr:  0.046087 avg.loss:  0.524798 ETA:   0h 0m Progress:  61.4% words/sec/thread:  918344 lr:  0.038595 avg.loss:  0.512023 ETA:   0h 0m Progress:  68.9% words/sec/thread:  915962 lr:  0.031100 avg.loss:  0.500851 ETA:   0h 0m Progress:  76.4% words/sec/thread:  913883 lr:  0.023620 avg.loss:  0.492542 ETA:   0h 0m Progress:  83.9% words/sec/thread:  912217 lr:  0.016135 avg.loss:  0.485644 ETA:   0h 0m Progress:  91.4% words/sec/thread:  910872 lr:  0.008645 avg.loss:  0.479052 ETA:   0h 0m Progress:  98.9% words/sec/thread:  909874 lr:  0.001139 avg.loss:  0.473559 ETA:   0h 0m Progress: 100.0% words/sec/thread:  854454 lr: -0.000000 avg.loss:  0.472646 ETA:   0h 0m Progress: 100.0% words/sec/thread:  854249 lr:  0.000000 avg.loss:  0.472646 ETA:   0h 0m 0s

real    0m1.593s
user    0m15.923s
sys     0m0.068s
Testing with epoch 30
Command: time fasttext test model.error_type_ep30.bin error_type.valid
N       10794
P@1     0.841
R@1     0.78

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 40
Command: time fasttext supervised -input error_type.train -output model.error_type_ep40 -epoch 40
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   6.2% words/sec/thread:  987623 lr:  0.093798 avg.loss:  0.737147 ETA:   0h 0m Progress:  12.2% words/sec/thread:  971753 lr:  0.087807 avg.loss:  0.649431 ETA:   0h 0m Progress:  18.0% words/sec/thread:  954604 lr:  0.082038 avg.loss:  0.600382 ETA:   0h 0m Progress:  23.7% words/sec/thread:  943268 lr:  0.076340 avg.loss:  0.571003 ETA:   0h 0m Progress:  29.3% words/sec/thread:  934244 lr:  0.070713 avg.loss:  0.552323 ETA:   0h 0m Progress:  34.9% words/sec/thread:  928287 lr:  0.065082 avg.loss:  0.537187 ETA:   0h 0m Progress:  40.5% words/sec/thread:  923847 lr:  0.059459 avg.loss:  0.524065 ETA:   0h 0m Progress:  46.2% words/sec/thread:  920266 lr:  0.053849 avg.loss:  0.512087 ETA:   0h 0m Progress:  51.8% words/sec/thread:  917807 lr:  0.048220 avg.loss:  0.502842 ETA:   0h 0m Progress:  57.4% words/sec/thread:  915908 lr:  0.042587 avg.loss:  0.492653 ETA:   0h 0m Progress:  63.0% words/sec/thread:  914253 lr:  0.036961 avg.loss:  0.482918 ETA:   0h 0m Progress:  68.7% words/sec/thread:  912817 lr:  0.031339 avg.loss:  0.476710 ETA:   0h 0m Progress:  74.3% words/sec/thread:  912364 lr:  0.025655 avg.loss:  0.471629 ETA:   0h 0m Progress:  80.0% words/sec/thread:  911490 lr:  0.020013 avg.loss:  0.466815 ETA:   0h 0m Progress:  85.6% words/sec/thread:  910825 lr:  0.014363 avg.loss:  0.462519 ETA:   0h 0m Progress:  91.3% words/sec/thread:  910203 lr:  0.008718 avg.loss:  0.458273 ETA:   0h 0m Progress:  96.9% words/sec/thread:  909581 lr:  0.003079 avg.loss:  0.454087 ETA:   0h 0m Progress: 100.0% words/sec/thread:  886250 lr: -0.000000 avg.loss:  0.452252 ETA:   0h 0m Progress: 100.0% words/sec/thread:  886125 lr:  0.000000 avg.loss:  0.452252 ETA:   0h 0m 0s

real    0m1.991s
user    0m21.205s
sys     0m0.056s
Testing with epoch 40
Command: time fasttext test model.error_type_ep40.bin error_type.valid
N       10794
P@1     0.841
R@1     0.78

real    0m0.016s
user    0m0.012s
sys     0m0.004s
==========
Training with epoch 50
Command: time fasttext supervised -input error_type.train -output model.error_type_ep50 -epoch 50
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   5.0% words/sec/thread:  993733 lr:  0.095005 avg.loss:  0.742041 ETA:   0h 0m Progress:   9.8% words/sec/thread:  974546 lr:  0.090214 avg.loss:  0.646465 ETA:   0h 0m Progress:  14.4% words/sec/thread:  958076 lr:  0.085575 avg.loss:  0.596940 ETA:   0h 0m Progress:  19.1% words/sec/thread:  949941 lr:  0.080934 avg.loss:  0.570091 ETA:   0h 0m Progress:  23.7% words/sec/thread:  945085 lr:  0.076293 avg.loss:  0.547320 ETA:   0h 0m Progress:  28.4% words/sec/thread:  941951 lr:  0.071649 avg.loss:  0.531865 ETA:   0h 0m Progress:  32.4% words/sec/thread:  922805 lr:  0.067598 avg.loss:  0.518936 ETA:   0h 0m Progress:  36.3% words/sec/thread:  904118 lr:  0.063721 avg.loss:  0.510455 ETA:   0h 0m Progress:  40.2% words/sec/thread:  889756 lr:  0.059837 avg.loss:  0.502422 ETA:   0h 0m Progress:  44.0% words/sec/thread:  878035 lr:  0.055963 avg.loss:  0.495317 ETA:   0h 0m Progress:  47.8% words/sec/thread:  867164 lr:  0.052160 avg.loss:  0.488574 ETA:   0h 0m Progress:  51.7% words/sec/thread:  858336 lr:  0.048344 avg.loss:  0.483843 ETA:   0h 0m Progress:  55.5% words/sec/thread:  850532 lr:  0.044548 avg.loss:  0.479069 ETA:   0h 0m Progress:  59.3% words/sec/thread:  844125 lr:  0.040734 avg.loss:  0.475356 ETA:   0h 0m Progress:  63.1% words/sec/thread:  838671 lr:  0.036911 avg.loss:  0.471658 ETA:   0h 0m Progress:  66.9% words/sec/thread:  833843 lr:  0.033094 avg.loss:  0.468337 ETA:   0h 0m Progress:  70.7% words/sec/thread:  829719 lr:  0.029264 avg.loss:  0.464456 ETA:   0h 0m Progress:  74.5% words/sec/thread:  825886 lr:  0.025452 avg.loss:  0.459741 ETA:   0h 0m Progress:  78.4% words/sec/thread:  822538 lr:  0.021630 avg.loss:  0.455910 ETA:   0h 0m Progress:  82.2% words/sec/thread:  819477 lr:  0.017812 avg.loss:  0.452119 ETA:   0h 0m Progress:  86.0% words/sec/thread:  816789 lr:  0.013987 avg.loss:  0.448983 ETA:   0h 0m Progress:  89.8% words/sec/thread:  814244 lr:  0.010172 avg.loss:  0.445871 ETA:   0h 0m Progress:  93.6% words/sec/thread:  811978 lr:  0.006351 avg.loss:  0.443627 ETA:   0h 0m Progress:  97.5% words/sec/thread:  809939 lr:  0.002525 avg.loss:  0.440976 ETA:   0h 0m Progress: 100.0% words/sec/thread:  797631 lr: -0.000000 avg.loss:  0.439714 ETA:   0h 0m Progress: 100.0% words/sec/thread:  797589 lr:  0.000000 avg.loss:  0.439714 ETA:   0h 0m 0s

real    0m2.683s
user    0m29.755s
sys     0m0.044s
Testing with epoch 50
Command: time fasttext test model.error_type_ep50.bin error_type.valid
N       10794
P@1     0.839
R@1     0.778

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 60
Command: time fasttext supervised -input error_type.train -output model.error_type_ep60 -epoch 60
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   3.6% words/sec/thread:  853309 lr:  0.096429 avg.loss:  0.759656 ETA:   0h 0m Progress:   6.7% words/sec/thread:  796604 lr:  0.093337 avg.loss:  0.665253 ETA:   0h 0m Progress:   9.8% words/sec/thread:  782460 lr:  0.090185 avg.loss:  0.617866 ETA:   0h 0m Progress:  13.0% words/sec/thread:  776914 lr:  0.087008 avg.loss:  0.591932 ETA:   0h 0m Progress:  16.2% words/sec/thread:  773969 lr:  0.083824 avg.loss:  0.573573 ETA:   0h 0m Progress:  19.4% words/sec/thread:  771768 lr:  0.080645 avg.loss:  0.558992 ETA:   0h 0m Progress:  22.5% words/sec/thread:  770145 lr:  0.077467 avg.loss:  0.545942 ETA:   0h 0m Progress:  25.7% words/sec/thread:  769033 lr:  0.074286 avg.loss:  0.535749 ETA:   0h 0m Progress:  28.9% words/sec/thread:  768296 lr:  0.071101 avg.loss:  0.524020 ETA:   0h 0m Progress:  32.1% words/sec/thread:  767700 lr:  0.067915 avg.loss:  0.515816 ETA:   0h 0m Progress:  35.3% words/sec/thread:  767099 lr:  0.064736 avg.loss:  0.508446 ETA:   0h 0m Progress:  38.4% words/sec/thread:  766673 lr:  0.061551 avg.loss:  0.502798 ETA:   0h 0m Progress:  41.6% words/sec/thread:  766372 lr:  0.058365 avg.loss:  0.497359 ETA:   0h 0m Progress:  44.8% words/sec/thread:  766141 lr:  0.055176 avg.loss:  0.493932 ETA:   0h 0m Progress:  48.0% words/sec/thread:  765785 lr:  0.051997 avg.loss:  0.490440 ETA:   0h 0m Progress:  51.2% words/sec/thread:  765532 lr:  0.048814 avg.loss:  0.487635 ETA:   0h 0m Progress:  54.4% words/sec/thread:  765206 lr:  0.045638 avg.loss:  0.485311 ETA:   0h 0m Progress:  57.6% words/sec/thread:  765109 lr:  0.042448 avg.loss:  0.482377 ETA:   0h 0m Progress:  60.7% words/sec/thread:  764905 lr:  0.039269 avg.loss:  0.480006 ETA:   0h 0m Progress:  63.9% words/sec/thread:  764751 lr:  0.036085 avg.loss:  0.476977 ETA:   0h 0m Progress:  67.1% words/sec/thread:  764657 lr:  0.032898 avg.loss:  0.474115 ETA:   0h 0m Progress:  70.3% words/sec/thread:  764517 lr:  0.029715 avg.loss:  0.471213 ETA:   0h 0m Progress:  73.5% words/sec/thread:  764302 lr:  0.026542 avg.loss:  0.468031 ETA:   0h 0m Progress:  76.6% words/sec/thread:  764221 lr:  0.023357 avg.loss:  0.464639 ETA:   0h 0m Progress:  79.8% words/sec/thread:  764104 lr:  0.020175 avg.loss:  0.462082 ETA:   0h 0m Progress:  83.0% words/sec/thread:  764010 lr:  0.016993 avg.loss:  0.459958 ETA:   0h 0m Progress:  86.2% words/sec/thread:  763890 lr:  0.013814 avg.loss:  0.458429 ETA:   0h 0m Progress:  89.4% words/sec/thread:  763788 lr:  0.010634 avg.loss:  0.456850 ETA:   0h 0m Progress:  92.5% words/sec/thread:  763709 lr:  0.007452 avg.loss:  0.454747 ETA:   0h 0m Progress:  95.7% words/sec/thread:  763664 lr:  0.004267 avg.loss:  0.453131 ETA:   0h 0m Progress:  98.9% words/sec/thread:  763592 lr:  0.001086 avg.loss:  0.451071 ETA:   0h 0m Progress: 100.0% words/sec/thread:  747814 lr: -0.000001 avg.loss:  0.450317 ETA:   0h 0m Progress: 100.0% words/sec/thread:  747751 lr:  0.000000 avg.loss:  0.450317 ETA:   0h 0m 0s

real    0m3.405s
user    0m37.776s
sys     0m0.068s
Testing with epoch 60
Command: time fasttext test model.error_type_ep60.bin error_type.valid
N       10794
P@1     0.84
R@1     0.779

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 70
Command: time fasttext supervised -input error_type.train -output model.error_type_ep70 -epoch 70
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   3.5% words/sec/thread:  982863 lr:  0.096463 avg.loss:  0.730109 ETA:   0h 0m Progress:   6.4% words/sec/thread:  891058 lr:  0.093601 avg.loss:  0.646387 ETA:   0h 0m Progress:   9.1% words/sec/thread:  849527 lr:  0.090857 avg.loss:  0.605473 ETA:   0h 0m Progress:  11.9% words/sec/thread:  828875 lr:  0.088110 avg.loss:  0.582351 ETA:   0h 0m Progress:  14.6% words/sec/thread:  816097 lr:  0.085371 avg.loss:  0.558511 ETA:   0h 0m Progress:  17.4% words/sec/thread:  807855 lr:  0.082625 avg.loss:  0.549935 ETA:   0h 0m Progress:  20.1% words/sec/thread:  802196 lr:  0.079874 avg.loss:  0.540031 ETA:   0h 0m Progress:  22.9% words/sec/thread:  797837 lr:  0.077126 avg.loss:  0.532345 ETA:   0h 0m Progress:  25.6% words/sec/thread:  794413 lr:  0.074379 avg.loss:  0.525630 ETA:   0h 0m Progress:  28.4% words/sec/thread:  791642 lr:  0.071633 avg.loss:  0.519932 ETA:   0h 0m Progress:  31.1% words/sec/thread:  789470 lr:  0.068884 avg.loss:  0.514735 ETA:   0h 0m Progress:  33.9% words/sec/thread:  787661 lr:  0.066134 avg.loss:  0.508121 ETA:   0h 0m Progress:  36.6% words/sec/thread:  786167 lr:  0.063383 avg.loss:  0.504093 ETA:   0h 0m Progress:  39.4% words/sec/thread:  784837 lr:  0.060634 avg.loss:  0.499541 ETA:   0h 0m Progress:  42.1% words/sec/thread:  783698 lr:  0.057884 avg.loss:  0.494838 ETA:   0h 0m Progress:  44.9% words/sec/thread:  782611 lr:  0.055140 avg.loss:  0.491935 ETA:   0h 0m Progress:  47.6% words/sec/thread:  781762 lr:  0.052388 avg.loss:  0.488368 ETA:   0h 0m Progress:  50.4% words/sec/thread:  781014 lr:  0.049637 avg.loss:  0.485019 ETA:   0h 0m Progress:  53.1% words/sec/thread:  780309 lr:  0.046888 avg.loss:  0.481340 ETA:   0h 0m Progress:  55.9% words/sec/thread:  779698 lr:  0.044137 avg.loss:  0.478876 ETA:   0h 0m Progress:  58.6% words/sec/thread:  779093 lr:  0.041390 avg.loss:  0.476323 ETA:   0h 0m Progress:  61.4% words/sec/thread:  778559 lr:  0.038642 avg.loss:  0.474127 ETA:   0h 0m Progress:  64.1% words/sec/thread:  778037 lr:  0.035896 avg.loss:  0.471848 ETA:   0h 0m Progress:  66.9% words/sec/thread:  777582 lr:  0.033149 avg.loss:  0.469494 ETA:   0h 0m Progress:  69.6% words/sec/thread:  777172 lr:  0.030401 avg.loss:  0.467128 ETA:   0h 0m Progress:  72.3% words/sec/thread:  776718 lr:  0.027660 avg.loss:  0.465408 ETA:   0h 0m Progress:  75.1% words/sec/thread:  776350 lr:  0.024913 avg.loss:  0.463324 ETA:   0h 0m Progress:  77.8% words/sec/thread:  776037 lr:  0.022164 avg.loss:  0.460632 ETA:   0h 0m Progress:  80.6% words/sec/thread:  775707 lr:  0.019419 avg.loss:  0.459059 ETA:   0h 0m Progress:  83.3% words/sec/thread:  775447 lr:  0.016669 avg.loss:  0.456930 ETA:   0h 0m Progress:  86.1% words/sec/thread:  775209 lr:  0.013918 avg.loss:  0.455138 ETA:   0h 0m Progress:  88.9% words/sec/thread:  775493 lr:  0.011109 avg.loss:  0.453201 ETA:   0h 0m Progress:  91.7% words/sec/thread:  775820 lr:  0.008293 avg.loss:  0.451421 ETA:   0h 0m Progress:  94.5% words/sec/thread:  775840 lr:  0.005512 avg.loss:  0.449716 ETA:   0h 0m Progress:  97.2% words/sec/thread:  775594 lr:  0.002765 avg.loss:  0.447817 ETA:   0h 0m Progress: 100.0% words/sec/thread:  775394 lr:  0.000012 avg.loss:  0.446351 ETA:   0h 0m Progress: 100.0% words/sec/thread:  754492 lr: -0.000000 avg.loss:  0.446361 ETA:   0h 0m Progress: 100.0% words/sec/thread:  754440 lr:  0.000000 avg.loss:  0.446361 ETA:   0h 0m 0s

real    0m3.887s
user    0m43.355s
sys     0m0.068s
Testing with epoch 70
Command: time fasttext test model.error_type_ep70.bin error_type.valid
N       10794
P@1     0.84
R@1     0.778

real    0m0.020s
user    0m0.019s
sys     0m0.000s
==========
Training with epoch 80
Command: time fasttext supervised -input error_type.train -output model.error_type_ep80 -epoch 80
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   3.1% words/sec/thread:  974095 lr:  0.096941 avg.loss:  0.730034 ETA:   0h 0m Progress:   5.7% words/sec/thread:  909475 lr:  0.094294 avg.loss:  0.645778 ETA:   0h 0m Progress:   8.1% words/sec/thread:  860302 lr:  0.091906 avg.loss:  0.602690 ETA:   0h 0m Progress:  10.5% words/sec/thread:  834339 lr:  0.089536 avg.loss:  0.577516 ETA:   0h 0m Progress:  12.8% words/sec/thread:  818872 lr:  0.087163 avg.loss:  0.556528 ETA:   0h 0m Progress:  15.2% words/sec/thread:  808716 lr:  0.084789 avg.loss:  0.540005 ETA:   0h 0m Progress:  17.6% words/sec/thread:  801366 lr:  0.082415 avg.loss:  0.525168 ETA:   0h 0m Progress:  20.0% words/sec/thread:  795830 lr:  0.080044 avg.loss:  0.512833 ETA:   0h 0m Progress:  22.3% words/sec/thread:  791673 lr:  0.077667 avg.loss:  0.500888 ETA:   0h 0m Progress:  24.7% words/sec/thread:  788393 lr:  0.075289 avg.loss:  0.488814 ETA:   0h 0m Progress:  27.1% words/sec/thread:  785567 lr:  0.072916 avg.loss:  0.485061 ETA:   0h 0m Progress:  29.4% words/sec/thread:  783006 lr:  0.070550 avg.loss:  0.480741 ETA:   0h 0m Progress:  31.8% words/sec/thread:  781021 lr:  0.068177 avg.loss:  0.479303 ETA:   0h 0m Progress:  34.2% words/sec/thread:  779188 lr:  0.065810 avg.loss:  0.476710 ETA:   0h 0m Progress:  36.6% words/sec/thread:  777810 lr:  0.063433 avg.loss:  0.474696 ETA:   0h 0m Progress:  38.9% words/sec/thread:  776581 lr:  0.061057 avg.loss:  0.472754 ETA:   0h 0m Progress:  41.3% words/sec/thread:  775506 lr:  0.058681 avg.loss:  0.470483 ETA:   0h 0m Progress:  43.7% words/sec/thread:  774489 lr:  0.056308 avg.loss:  0.468535 ETA:   0h 0m Progress:  46.1% words/sec/thread:  773588 lr:  0.053934 avg.loss:  0.466296 ETA:   0h 0m Progress:  48.4% words/sec/thread:  772805 lr:  0.051559 avg.loss:  0.464005 ETA:   0h 0m Progress:  50.8% words/sec/thread:  772059 lr:  0.049187 avg.loss:  0.461139 ETA:   0h 0m Progress:  53.2% words/sec/thread:  771404 lr:  0.046812 avg.loss:  0.458239 ETA:   0h 0m Progress:  55.6% words/sec/thread:  770823 lr:  0.044437 avg.loss:  0.455424 ETA:   0h 0m Progress:  57.9% words/sec/thread:  770197 lr:  0.042068 avg.loss:  0.453876 ETA:   0h 0m Progress:  60.3% words/sec/thread:  769654 lr:  0.039697 avg.loss:  0.451978 ETA:   0h 0m Progress:  62.7% words/sec/thread:  769129 lr:  0.037328 avg.loss:  0.451032 ETA:   0h 0m Progress:  65.0% words/sec/thread:  768698 lr:  0.034954 avg.loss:  0.451087 ETA:   0h 0m Progress:  67.4% words/sec/thread:  768328 lr:  0.032578 avg.loss:  0.450566 ETA:   0h 0m Progress:  69.8% words/sec/thread:  768350 lr:  0.030168 avg.loss:  0.450107 ETA:   0h 0m Progress:  72.2% words/sec/thread:  767977 lr:  0.027795 avg.loss:  0.449160 ETA:   0h 0m Progress:  74.6% words/sec/thread:  767640 lr:  0.025421 avg.loss:  0.448570 ETA:   0h 0m Progress:  77.0% words/sec/thread:  767313 lr:  0.023049 avg.loss:  0.447625 ETA:   0h 0m Progress:  79.3% words/sec/thread:  766985 lr:  0.020678 avg.loss:  0.446784 ETA:   0h 0m Progress:  81.7% words/sec/thread:  766662 lr:  0.018309 avg.loss:  0.445463 ETA:   0h 0m Progress:  84.1% words/sec/thread:  766381 lr:  0.015938 avg.loss:  0.443960 ETA:   0h 0m Progress:  86.4% words/sec/thread:  766108 lr:  0.013566 avg.loss:  0.442841 ETA:   0h 0m Progress:  88.8% words/sec/thread:  765824 lr:  0.011198 avg.loss:  0.441663 ETA:   0h 0m Progress:  91.2% words/sec/thread:  765526 lr:  0.008834 avg.loss:  0.440675 ETA:   0h 0m Progress:  93.5% words/sec/thread:  765296 lr:  0.006463 avg.loss:  0.439343 ETA:   0h 0m Progress:  95.9% words/sec/thread:  765082 lr:  0.004091 avg.loss:  0.438436 ETA:   0h 0m Progress:  98.3% words/sec/thread:  764864 lr:  0.001722 avg.loss:  0.437094 ETA:   0h 0m Progress: 100.0% words/sec/thread:  759708 lr: -0.000000 avg.loss:  0.436299 ETA:   0h 0m Progress: 100.0% words/sec/thread:  759685 lr:  0.000000 avg.loss:  0.436299 ETA:   0h 0m 0s

real    0m4.383s
user    0m50.200s
sys     0m0.092s
Testing with epoch 80
Command: time fasttext test model.error_type_ep80.bin error_type.valid
N       10794
P@1     0.84
R@1     0.778

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 90
Command: time fasttext supervised -input error_type.train -output model.error_type_ep90 -epoch 90
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.6% words/sec/thread:  922625 lr:  0.097417 avg.loss:  0.738078 ETA:   0h 0m Progress:   4.8% words/sec/thread:  866024 lr:  0.095162 avg.loss:  0.666684 ETA:   0h 0m Progress:   7.0% words/sec/thread:  840285 lr:  0.092963 avg.loss:  0.625938 ETA:   0h 0m Progress:   9.2% words/sec/thread:  820149 lr:  0.090846 avg.loss:  0.605299 ETA:   0h 0m Progress:  11.3% words/sec/thread:  808168 lr:  0.088728 avg.loss:  0.588039 ETA:   0h 0m Progress:  13.4% words/sec/thread:  800173 lr:  0.086609 avg.loss:  0.575876 ETA:   0h 0m Progress:  15.5% words/sec/thread:  794441 lr:  0.084491 avg.loss:  0.562598 ETA:   0h 0m Progress:  17.6% words/sec/thread:  790118 lr:  0.082373 avg.loss:  0.552551 ETA:   0h 0m Progress:  19.8% words/sec/thread:  788771 lr:  0.080205 avg.loss:  0.541357 ETA:   0h 0m Progress:  21.9% words/sec/thread:  786001 lr:  0.078084 avg.loss:  0.531564 ETA:   0h 0m Progress:  24.1% words/sec/thread:  785246 lr:  0.075917 avg.loss:  0.526940 ETA:   0h 0m Progress:  26.3% words/sec/thread:  784770 lr:  0.073744 avg.loss:  0.521062 ETA:   0h 0m Progress:  28.4% words/sec/thread:  784239 lr:  0.071577 avg.loss:  0.515610 ETA:   0h 0m Progress:  30.5% words/sec/thread:  782536 lr:  0.069457 avg.loss:  0.511513 ETA:   0h 0m Progress:  32.7% words/sec/thread:  780978 lr:  0.067342 avg.loss:  0.507373 ETA:   0h 0m Progress:  34.8% words/sec/thread:  779537 lr:  0.065230 avg.loss:  0.504791 ETA:   0h 0m Progress:  36.9% words/sec/thread:  778381 lr:  0.063112 avg.loss:  0.503000 ETA:   0h 0m Progress:  39.0% words/sec/thread:  777298 lr:  0.060998 avg.loss:  0.500240 ETA:   0h 0m Progress:  41.1% words/sec/thread:  776258 lr:  0.058887 avg.loss:  0.498076 ETA:   0h 0m Progress:  43.2% words/sec/thread:  775428 lr:  0.056770 avg.loss:  0.495264 ETA:   0h 0m Progress:  45.3% words/sec/thread:  774711 lr:  0.054651 avg.loss:  0.493215 ETA:   0h 0m Progress:  47.5% words/sec/thread:  774058 lr:  0.052532 avg.loss:  0.490987 ETA:   0h 0m Progress:  49.6% words/sec/thread:  773405 lr:  0.050417 avg.loss:  0.487709 ETA:   0h 0m Progress:  51.7% words/sec/thread:  772819 lr:  0.048301 avg.loss:  0.485494 ETA:   0h 0m Progress:  53.8% words/sec/thread:  772257 lr:  0.046187 avg.loss:  0.482589 ETA:   0h 0m Progress:  55.9% words/sec/thread:  771752 lr:  0.044072 avg.loss:  0.480073 ETA:   0h 0m Progress:  58.0% words/sec/thread:  771274 lr:  0.041957 avg.loss:  0.477355 ETA:   0h 0m Progress:  60.2% words/sec/thread:  770882 lr:  0.039839 avg.loss:  0.475689 ETA:   0h 0m Progress:  62.3% words/sec/thread:  771133 lr:  0.037669 avg.loss:  0.473442 ETA:   0h 0m Progress:  64.5% words/sec/thread:  771422 lr:  0.035495 avg.loss:  0.472089 ETA:   0h 0m Progress:  66.7% words/sec/thread:  771763 lr:  0.033315 avg.loss:  0.470332 ETA:   0h 0m Progress:  68.9% words/sec/thread:  772041 lr:  0.031139 avg.loss:  0.468720 ETA:   0h 0m Progress:  71.0% words/sec/thread:  772280 lr:  0.028965 avg.loss:  0.467443 ETA:   0h 0m Progress:  73.2% words/sec/thread:  772533 lr:  0.026788 avg.loss:  0.465769 ETA:   0h 0m Progress:  75.4% words/sec/thread:  772776 lr:  0.024610 avg.loss:  0.464501 ETA:   0h 0m Progress:  77.5% words/sec/thread:  772546 lr:  0.022479 avg.loss:  0.462924 ETA:   0h 0m Progress:  79.6% words/sec/thread:  772253 lr:  0.020356 avg.loss:  0.461569 ETA:   0h 0m Progress:  81.8% words/sec/thread:  771961 lr:  0.018234 avg.loss:  0.460233 ETA:   0h 0m Progress:  83.9% words/sec/thread:  771685 lr:  0.016112 avg.loss:  0.458894 ETA:   0h 0m Progress:  86.0% words/sec/thread:  771394 lr:  0.013993 avg.loss:  0.457273 ETA:   0h 0m Progress:  88.1% words/sec/thread:  771083 lr:  0.011879 avg.loss:  0.455800 ETA:   0h 0m Progress:  90.2% words/sec/thread:  770829 lr:  0.009758 avg.loss:  0.454308 ETA:   0h 0m Progress:  92.4% words/sec/thread:  770557 lr:  0.007644 avg.loss:  0.453222 ETA:   0h 0m Progress:  94.5% words/sec/thread:  770284 lr:  0.005529 avg.loss:  0.452062 ETA:   0h 0m Progress:  96.6% words/sec/thread:  770072 lr:  0.003408 avg.loss:  0.450641 ETA:   0h 0m Progress:  98.7% words/sec/thread:  769882 lr:  0.001286 avg.loss:  0.449590 ETA:   0h 0m Progress: 100.0% words/sec/thread:  763293 lr: -0.000000 avg.loss:  0.448685 ETA:   0h 0m Progress: 100.0% words/sec/thread:  763240 lr:  0.000000 avg.loss:  0.448685 ETA:   0h 0m 0s

real    0m4.895s
user    0m56.125s
sys     0m0.064s
Testing with epoch 90
Command: time fasttext test model.error_type_ep90.bin error_type.valid
N       10794
P@1     0.839
R@1     0.778

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 100
Command: time fasttext supervised -input error_type.train -output model.error_type_ep100 -epoch 100
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.4% words/sec/thread:  967756 lr:  0.097554 avg.loss:  0.747666 ETA:   0h 0m Progress:   4.4% words/sec/thread:  872752 lr:  0.095604 avg.loss:  0.661894 ETA:   0h 0m Progress:   6.3% words/sec/thread:  835008 lr:  0.093699 avg.loss:  0.612803 ETA:   0h 0m Progress:   8.2% words/sec/thread:  816325 lr:  0.091793 avg.loss:  0.593645 ETA:   0h 0m Progress:  10.1% words/sec/thread:  805186 lr:  0.089885 avg.loss:  0.580065 ETA:   0h 0m Progress:  12.0% words/sec/thread:  797527 lr:  0.087981 avg.loss:  0.569583 ETA:   0h 0m Progress:  13.9% words/sec/thread:  792109 lr:  0.086076 avg.loss:  0.559579 ETA:   0h 0m Progress:  15.8% words/sec/thread:  788093 lr:  0.084170 avg.loss:  0.551552 ETA:   0h 0m Progress:  17.7% words/sec/thread:  785005 lr:  0.082263 avg.loss:  0.543680 ETA:   0h 0m Progress:  19.6% words/sec/thread:  782655 lr:  0.080353 avg.loss:  0.538459 ETA:   0h 0m Progress:  21.6% words/sec/thread:  780559 lr:  0.078447 avg.loss:  0.531749 ETA:   0h 0m Progress:  23.5% words/sec/thread:  778750 lr:  0.076544 avg.loss:  0.525107 ETA:   0h 0m Progress:  25.4% words/sec/thread:  777330 lr:  0.074637 avg.loss:  0.518395 ETA:   0h 0m Progress:  27.3% words/sec/thread:  776095 lr:  0.072731 avg.loss:  0.513997 ETA:   0h 0m Progress:  29.2% words/sec/thread:  775109 lr:  0.070821 avg.loss:  0.510139 ETA:   0h 0m Progress:  31.1% words/sec/thread:  774102 lr:  0.068917 avg.loss:  0.508274 ETA:   0h 0m Progress:  33.0% words/sec/thread:  773264 lr:  0.067012 avg.loss:  0.505816 ETA:   0h 0m Progress:  34.9% words/sec/thread:  772461 lr:  0.065108 avg.loss:  0.502126 ETA:   0h 0m Progress:  36.8% words/sec/thread:  771689 lr:  0.063208 avg.loss:  0.500214 ETA:   0h 0m Progress:  38.7% words/sec/thread:  771230 lr:  0.061296 avg.loss:  0.498143 ETA:   0h 0m Progress:  40.6% words/sec/thread:  770813 lr:  0.059383 avg.loss:  0.496627 ETA:   0h 0m Progress:  42.5% words/sec/thread:  770479 lr:  0.057468 avg.loss:  0.495053 ETA:   0h 0m Progress:  44.4% words/sec/thread:  770100 lr:  0.055557 avg.loss:  0.494027 ETA:   0h 0m Progress:  46.4% words/sec/thread:  769765 lr:  0.053646 avg.loss:  0.491865 ETA:   0h 0m Progress:  48.3% words/sec/thread:  769448 lr:  0.051735 avg.loss:  0.490192 ETA:   0h 0m Progress:  50.2% words/sec/thread:  769181 lr:  0.049823 avg.loss:  0.487817 ETA:   0h 0m Progress:  52.1% words/sec/thread:  768927 lr:  0.047911 avg.loss:  0.484903 ETA:   0h 0m Progress:  54.0% words/sec/thread:  768659 lr:  0.046001 avg.loss:  0.482325 ETA:   0h 0m Progress:  55.9% words/sec/thread:  768426 lr:  0.044089 avg.loss:  0.481220 ETA:   0h 0m Progress:  57.8% words/sec/thread:  768222 lr:  0.042177 avg.loss:  0.479225 ETA:   0h 0m Progress:  59.7% words/sec/thread:  767988 lr:  0.040269 avg.loss:  0.478584 ETA:   0h 0m Progress:  61.6% words/sec/thread:  767809 lr:  0.038357 avg.loss:  0.477875 ETA:   0h 0m Progress:  63.6% words/sec/thread:  767624 lr:  0.036446 avg.loss:  0.476209 ETA:   0h 0m Progress:  65.5% words/sec/thread:  767470 lr:  0.034534 avg.loss:  0.474279 ETA:   0h 0m Progress:  67.4% words/sec/thread:  767319 lr:  0.032622 avg.loss:  0.472147 ETA:   0h 0m Progress:  69.3% words/sec/thread:  767294 lr:  0.030700 avg.loss:  0.470920 ETA:   0h 0m Progress:  71.2% words/sec/thread:  767155 lr:  0.028788 avg.loss:  0.469238 ETA:   0h 0m Progress:  73.1% words/sec/thread:  766981 lr:  0.026880 avg.loss:  0.467961 ETA:   0h 0m Progress:  75.0% words/sec/thread:  766816 lr:  0.024973 avg.loss:  0.466463 ETA:   0h 0m Progress:  76.9% words/sec/thread:  766623 lr:  0.023069 avg.loss:  0.465090 ETA:   0h 0m Progress:  78.8% words/sec/thread:  766479 lr:  0.021161 avg.loss:  0.463332 ETA:   0h 0m Progress:  80.7% words/sec/thread:  766305 lr:  0.019256 avg.loss:  0.461586 ETA:   0h 0m Progress:  82.7% words/sec/thread:  766163 lr:  0.017350 avg.loss:  0.459900 ETA:   0h 0m Progress:  84.6% words/sec/thread:  765979 lr:  0.015448 avg.loss:  0.458499 ETA:   0h 0m Progress:  86.5% words/sec/thread:  765833 lr:  0.013544 avg.loss:  0.457451 ETA:   0h 0m Progress:  88.4% words/sec/thread:  765730 lr:  0.011635 avg.loss:  0.455928 ETA:   0h 0m Progress:  90.3% words/sec/thread:  765600 lr:  0.009729 avg.loss:  0.454841 ETA:   0h 0m Progress:  92.2% words/sec/thread:  765513 lr:  0.007820 avg.loss:  0.453497 ETA:   0h 0m Progress:  94.1% words/sec/thread:  765391 lr:  0.005915 avg.loss:  0.452382 ETA:   0h 0m Progress:  96.0% words/sec/thread:  765293 lr:  0.004007 avg.loss:  0.451117 ETA:   0h 0m Progress:  97.9% words/sec/thread:  765171 lr:  0.002103 avg.loss:  0.449914 ETA:   0h 0m Progress:  99.8% words/sec/thread:  765055 lr:  0.000199 avg.loss:  0.448576 ETA:   0h 0m Progress: 100.0% words/sec/thread:  752100 lr: -0.000000 avg.loss:  0.448444 ETA:   0h 0m Progress: 100.0% words/sec/thread:  752052 lr:  0.000000 avg.loss:  0.448444 ETA:   0h 0m 0s

real    0m5.493s
user    1m2.692s
sys     0m0.100s
Testing with epoch 100
Command: time fasttext test model.error_type_ep100.bin error_type.valid
N       10794
P@1     0.838
R@1     0.777

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## F1-Score Calculation

```python
## For F1-score calculation
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 31 Oct 2023

import argparse

def calculate_f1(precision, recall):
    if precision + recall == 0:
        return 0.0  # Handle the special case where both precision and recall are zero to avoid division by zero
    return 2 * ((precision * recall) / (precision + recall))

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Calculate F1-score from Precision and Recall.')
    parser.add_argument('-p', '--precision', type=float, required=True, help='The precision value (a float between 0 and 1).')
    parser.add_argument('-r', '--recall', type=float, required=True, help='The recall value (a float between 0 and 1).')

    args = parser.parse_args()

    f1_score = calculate_f1(args.precision, args.recall)
    print(f'F1-score: {f1_score:.2f}')

```

for epoch 10 testing result:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python calc_f1.py -p 0.839 -r 0.778
F1-score: 0.81
```

for epoch 100 testing result:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python calc_f1.py -p 0.838 -r 0.777
F1-score: 0.81
```

## To Do



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
