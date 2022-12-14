# Testing Sentence Tokenization for Burmese with Updated Data

Thura Aung updated/cleaned the corpus and thus, we need to run all the experiments again with the updated data.  

## Move the Old Data

```
root@48e31407fc14:/home/ye/exp/mysent# mv data-{sent,para} ./old-exp1-data/
root@48e31407fc14:/home/ye/exp/mysent# tree ./old-exp1-data/
./old-exp1-data/
|-- data-para
|   |-- combind-process
|   |   |-- test.my-tg
|   |   |-- test.my-tg.shuf
|   |   |-- test.my.combi
|   |   |-- test.my.final
|   |   |-- test.tg.combi
|   |   |-- test.tg.final
|   |   |-- train.my-tg
|   |   |-- train.my-tg.shuf
|   |   |-- train.my.combi
|   |   |-- train.my.final
|   |   |-- train.tg.combi
|   |   |-- train.tg.final
|   |   |-- valid.my-tg
|   |   |-- valid.my-tg.shuf
|   |   |-- valid.my.combi
|   |   |-- valid.my.final
|   |   |-- valid.tg.combi
|   |   `-- valid.tg.final
|   |-- paragraph.txt
|   |-- paragraph.txt.error
|   |-- preprocessing
|   |   |-- mk-wordtag2.pl
|   |   |-- para.tag
|   |   |-- para.word
|   |   |-- paragraph.txt
|   |   |-- paragraph.txt.shuf
|   |   |-- test.my
|   |   |-- test.tg
|   |   |-- train.my
|   |   |-- train.tg
|   |   |-- valid.my
|   |   `-- valid.tg
|   |-- test.my
|   |-- test.tg
|   |-- train.my
|   |-- train.tg
|   |-- valid.my
|   |-- valid.tg
|   `-- vocab
|       |-- all.my
|       |-- all.tg
|       |-- vocab.my.yml
|       `-- vocab.tg.yml
`-- data-sent
    |-- test.my
    |-- test.tg
    |-- train.my
    |-- train.tg
    |-- valid.my
    |-- valid.tg
    `-- vocab
        |-- all.my
        |-- all.tg
        |-- vocab.my.yml
        `-- vocab.tg.yml

6 directories, 51 files
root@48e31407fc14:/home/ye/exp/mysent#
```

## Prepare New Dataset

Copy data to the GPU machine:  

```
C:\Users\801680>scp [12Dec]mySentence_data_results.zip ye@10.222.xx.xx:/home/ye/
ye@10.222.xx.xx's password:
[12Dec]mySentence_data_results.zip                                                          100%   10MB   2.7MB/s   00:03

C:\Users\801680>
```

Check on server side:  

```
root@48e31407fc14:/home/ye/exp/mysent/tmp# mv /home/ye/\[12Dec\]mySentence_data_results.zip .
root@48e31407fc14:/home/ye/exp/mysent/tmp# ls
'[12Dec]mySentence_data_results.zip'
root@48e31407fc14:/home/ye/exp/mysent/tmp# unzip \[12Dec\]mySentence_data_results.zip
Archive:  [12Dec]mySentence_data_results.zip
  inflating: [12Dec]Results_mySentence.pdf
  inflating: clean-data-rdy2train.zip
root@48e31407fc14:/home/ye/exp/mysent/tmp# ls
'[12Dec]Results_mySentence.pdf'  '[12Dec]mySentence_data_results.zip'   clean-data-rdy2train.zip
root@48e31407fc14:/home/ye/exp/mysent/tmp# unzip ./clean-data-rdy2train.zip
Archive:  ./clean-data-rdy2train.zip
   creating: clean-data-rdy2train/
   creating: clean-data-rdy2train/data-sent/
  inflating: clean-data-rdy2train/data-sent/test.my~
  inflating: clean-data-rdy2train/data-sent/train.txt~
   creating: clean-data-rdy2train/data-sent/sent_tagged/
  inflating: clean-data-rdy2train/data-sent/sent_tagged/test.tagged
  inflating: clean-data-rdy2train/data-sent/sent_tagged/train.tagged
  inflating: clean-data-rdy2train/data-sent/sent_tagged/valid.tagged
   creating: clean-data-rdy2train/data-sent/sent_parallel/
  inflating: clean-data-rdy2train/data-sent/sent_parallel/train.my
  inflating: clean-data-rdy2train/data-sent/sent_parallel/test.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/valid.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/valid.my
  inflating: clean-data-rdy2train/data-sent/sent_parallel/train.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/test.my
   creating: clean-data-rdy2train/data-sent+para/
   creating: clean-data-rdy2train/data-sent+para/sent+para_tagged/
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/valid.tagged
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/train.tagged
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/test.tagged
   creating: clean-data-rdy2train/data-sent+para/sent+para_parallel/
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/valid.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/valid.my
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/train.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/train.my
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/test.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/test.my
root@48e31407fc14:/home/ye/exp/mysent/tmp#
```

copied sentence and parallel data to the folder called by the NMT framework marian:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent# cp ../tmp/clean-data-rdy2train/data-sent/sent_parallel/* .
root@48e31407fc14:/home/ye/exp/mysent/data-sent# ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
root@48e31407fc14:/home/ye/exp/mysent/data-sent# wc *
    4712      448   919423 test.my
    4712    63622   127244 test.tg
   40000     3688  7868628 train.my
   40000   543541  1087082 train.tg
    2414      257   466536 valid.my
    2414    32315    64630 valid.tg
   94252   643871 10533543 total
root@48e31407fc14:/home/ye/exp/mysent/data-sent#
```

for sent+para data:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para# cp ../tmp/clean-data-rdy2train/data-sent+para/sent+para_parallel/* .
root@48e31407fc14:/home/ye/exp/mysent/data-para# wc *
    5512      758  1380183 test.my
    5512    96632   193264 test.tg
   47002     6031 11944271 train.my
   47002   834243  1668486 train.tg
    3079      518   877576 valid.my
    3079    61782   123564 valid.tg
  111186   999964 16187344 total
root@48e31407fc14:/home/ye/exp/mysent/data-para#
```

## make Vocab

for sent only dataset:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent# cat train.my valid.my test.my > ./vocab/all.my
root@48e31407fc14:/home/ye/exp/mysent/data-sent# cat train.tg valid.tg test.tg > ./vocab/all.tg
root@48e31407fc14:/home/ye/exp/mysent/data-sent# cd vocab
```

Practical engineering thing running under container env:  

```
root@48e31407fc14:/temp/build# cp marian* /usr/bin/
```

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# time marian-vocab < all.my > vocab.my.yml
[2022-12-14 12:30:31] Creating vocabulary...
[2022-12-14 12:30:31] [data] Creating vocabulary stdout from stdin
[2022-12-14 12:30:31] Finished

real    0m0.388s
user    0m0.308s
sys     0m0.033s
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab#
```

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# time marian-vocab < all.tg > vocab.tg.yml
[2022-12-14 12:32:11] Creating vocabulary...
[2022-12-14 12:32:11] [data] Creating vocabulary stdout from stdin
[2022-12-14 12:32:11] Finished

real    0m0.051s
user    0m0.047s
sys     0m0.004s
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab#
```

check the file content:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# head vocab.my.yml
</s>: 0
<unk>: 1
ကို: 2
သည်: 3
တယ်: 4
က: 5
ပါ: 6
မှာ: 7
များ: 8
ရှိ: 9
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# head vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab#
```

check the vocab filesize:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# head vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab# wc *.yml
  32592   65186 1071971 vocab.my.yml
      5      12      36 vocab.tg.yml
  32597   65198 1072007 total
root@48e31407fc14:/home/ye/exp/mysent/data-sent/vocab#
```

vocab preparation for sent+paragraph dataset:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para# ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
root@48e31407fc14:/home/ye/exp/mysent/data-para# mkdir vocab
root@48e31407fc14:/home/ye/exp/mysent/data-para# cat train.my valid.my test.my > ./vocab/all.my
root@48e31407fc14:/home/ye/exp/mysent/data-para# cat train.tg valid.tg test.tg > ./vocab/all.tg
```

check ...  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# ls
all.my  all.tg
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# wc *
   55593     7307 14202030 all.my
   55593   992657  1985314 all.tg
  111186   999964 16187344 total
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab#
```

make vocab ...  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# time marian-vocab < ./all.my > vocab.my.yml
[2022-12-14 12:40:34] Creating vocabulary...
[2022-12-14 12:40:34] [data] Creating vocabulary stdout from stdin
[2022-12-14 12:40:34] Finished

real    0m0.471s
user    0m0.458s
sys     0m0.012s
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# time marian-vocab < ./all.tg > vocab.tg.yml
[2022-12-14 12:40:47] Creating vocabulary...
[2022-12-14 12:40:47] [data] Creating vocabulary stdout from stdin
[2022-12-14 12:40:47] Finished

real    0m0.065s
user    0m0.053s
sys     0m0.012s
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab#
```

checck the vocab filesize:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# wc *.yml
  46104   92210 1559638 vocab.my.yml
      5      12      36 vocab.tg.yml
  46109   92222 1559674 total
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab#
```

check the voccab file content:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# head vocab.my.yml
</s>: 0
<unk>: 1
ကို: 2
တယ်: 3
က: 4
သည်: 5
ပါ: 6
မှာ: 7
တွေ: 8
တဲ့: 9
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# tail ./vocab.my.yml
⁠လုံးလျား⁠လျား: 46095
−ရှင်: 46096
−သမီးတော်: 46097
新加坡: 46098
昭南島: 46099
昭和の時代に得た南の島: 46100
禪: 46101
缅甸: 46102
"\ufeff": 46103
"\ufeffတင်ပို့": 46104root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab#
```

checck the file content of tag vocab file:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab# cat vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5root@48e31407fc14:/home/ye/exp/mysent/data-para/vocab#
```

Vocab file creation finished for both sentence and sent+para dataset!   

## Backup the Old Models

```
root@57452252667f:/home/ye/exp/mysent# mkdir backup
root@57452252667f:/home/ye/exp/mysent# mv model.* ./backup/
root@57452252667f:/home/ye/exp/mysent# ls ./backup/
model.seq2seq.para1  model.seq2seq.sent1  model.transformer.para1  model.transformer.para1.bk  model.transformer.sent1
root@57452252667f:/home/ye/exp/mysent#
```

backup old log files also ...  

```
root@57452252667f:/home/ye/exp/mysent# ls *log*
transformer.para1.log  transformer.para1.log.err1  transformer.sent1.log  transformer.sent1.log.err1
root@57452252667f:/home/ye/exp/mysent# mv *log* ./backup/
```

## Recheck the shell scripts for training marain 

I think I used following shell scripts for the previous experiments ...  

```
root@57452252667f:/home/ye/exp/mysent# ls *.sh
check-end-mark.sh  seq2seq.sent1.sh               test4paper.sh         transformer.sent1.sh
seq2seq.para1.sh   test4paper-with-para-vocab.sh  transformer.para1.sh
root@57452252667f:/home/ye/exp/mysent#
```

check the seq2seq training script ...  

```bash
root@57452252667f:/home/ye/exp/mysent# head -n 30 ./seq2seq.sent1.sh
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training
## Last updated: 24 Oct 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.sent1";
mkdir ${model_folder};
data_path="/home/ye/exp/mysent/data-sent";
src="my"; tgt="tg";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/valid.${src} ${data_path}/valid.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log1
root@57452252667f:/home/ye/exp/mysent#
```

## Training/Testing Seq2Seq for Sentence Only Dataset


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
