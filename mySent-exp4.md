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

at first, check the GPU status:  

```
root@57452252667f:/home/ye/exp/mysent# nvidia-smi
Wed Dec 14 13:24:44 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.86.01    Driver Version: 515.86.01    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
|  0%   39C    P8    25W / 480W |     58MiB / 24564MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
+-----------------------------------------------------------------------------+
root@57452252667f:/home/ye/exp/mysent#
```

start training ...  

```
root@57452252667f:/home/ye/exp/mysent# ./seq2seq.sent1.sh
...
...
[2022-12-14 14:40:55] Seen 39,999 samples
[2022-12-14 14:40:55] Starting data epoch 62 in logical epoch 62
[2022-12-14 14:40:55] [data] Shuffling data
[2022-12-14 14:40:55] [data] Done reading 40,000 sentences
[2022-12-14 14:40:56] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 14:41:34] Ep. 62 : Up. 20000 : Sen. 21,587 : Cost 0.06380463 * 898,943 @ 2,380 after 35,885,885 : Time 111.22s : 8082.72 words/s : gNorm 0.6358
[2022-12-14 14:41:34] Saving model weights and runtime parameters to model.seq2seq.sent1/model.iter20000.npz
[2022-12-14 14:41:36] Saving model weights and runtime parameters to model.seq2seq.sent1/model.npz
[2022-12-14 14:41:41] Saving Adam parameters
[2022-12-14 14:41:44] [training] Saving training checkpoint to model.seq2seq.sent1/model.npz and model.seq2seq.sent1/model.npz.optimizer.npz
[2022-12-14 14:42:05] [valid] Ep. 62 : Up. 20000 : cross-entropy : 0.243329 : new best
[2022-12-14 14:42:08] [valid] Ep. 62 : Up. 20000 : perplexity : 1.01706 : new best
[2022-12-14 14:42:08] Translating validation set...
[2022-12-14 14:42:09] Best translation 0 : B O O O O O O O O O N N N E
[2022-12-14 14:42:09] Best translation 1 : B O O N N N E
[2022-12-14 14:42:09] Best translation 2 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 14:42:09] Best translation 3 : B O O O O O O O O O O O O O O O O N N N E
[2022-12-14 14:42:09] Best translation 4 : B O O N N N E
[2022-12-14 14:42:09] Best translation 5 : B O O O N N N E
[2022-12-14 14:42:09] Best translation 10 : B N N E
[2022-12-14 14:42:09] Best translation 20 : B O O O N N N E
[2022-12-14 14:42:09] Best translation 40 : B N N N E
[2022-12-14 14:42:09] Best translation 80 : B O O O O O O O O O O N N N E
[2022-12-14 14:42:09] Best translation 160 : B O O O O O O O O O O N N N E
[2022-12-14 14:42:09] Best translation 320 : B O O O O O N N N E
[2022-12-14 14:42:10] Best translation 640 : B O O O O O O O O O N N N E
[2022-12-14 14:42:11] Best translation 1280 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 14:42:13] Total translation time: 5.00986s
[2022-12-14 14:42:13] [valid] Ep. 62 : Up. 20000 : bleu : 99.5307 : new best
...
...
...
[2022-12-14 15:06:09] Seen 39,999 samples
[2022-12-14 15:06:09] Starting data epoch 82 in logical epoch 82
[2022-12-14 15:06:09] [data] Shuffling data
[2022-12-14 15:06:09] [data] Done reading 40,000 sentences
[2022-12-14 15:06:09] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:06:45] Ep. 82 : Up. 26500 : Sen. 20,648 : Cost 0.10021749 * 895,289 @ 1,560 after 47,533,924 : Time 110.36s : 8112.12 words/s : gNorm 1.5826
[2022-12-14 15:07:20] Seen 39,999 samples
[2022-12-14 15:07:20] Starting data epoch 83 in logical epoch 83
[2022-12-14 15:07:20] [data] Shuffling data
[2022-12-14 15:07:20] [data] Done reading 40,000 sentences
[2022-12-14 15:07:20] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:08:31] Seen 39,999 samples
[2022-12-14 15:08:31] Starting data epoch 84 in logical epoch 84
[2022-12-14 15:08:31] [data] Shuffling data
[2022-12-14 15:08:31] [data] Done reading 40,000 sentences
[2022-12-14 15:08:31] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:08:36] Ep. 84 : Up. 27000 : Sen. 1,990 : Cost 0.08448897 * 898,072 @ 2,001 after 48,431,996 : Time 110.08s : 8158.63 words/s : gNorm 1.3917
[2022-12-14 15:09:43] Seen 39,999 samples
[2022-12-14 15:09:43] Starting data epoch 85 in logical epoch 85
[2022-12-14 15:09:43] [data] Shuffling data
[2022-12-14 15:09:43] [data] Done reading 40,000 sentences
[2022-12-14 15:09:43] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:10:26] Ep. 85 : Up. 27500 : Sen. 23,481 : Cost 0.07476421 * 895,516 @ 1,768 after 49,327,512 : Time 110.27s : 8121.41 words/s : gNorm 1.6711
[2022-12-14 15:10:56] Seen 39,999 samples
[2022-12-14 15:10:56] Starting data epoch 86 in logical epoch 86
[2022-12-14 15:10:56] [data] Shuffling data
[2022-12-14 15:10:56] [data] Done reading 40,000 sentences
[2022-12-14 15:10:56] [data] Done shuffling 40,000 sentences to temp files
...
...
...
[2022-12-14 15:50:19] Ep. 117 : Up. 38000 : Sen. 35,497 : Cost 0.07857694 * 894,744 @ 2,005 after 68,163,031 : Time 111.14s : 8050.45 words/s : gNorm 1.7157
[2022-12-14 15:50:27] Seen 39,999 samples
[2022-12-14 15:50:27] Starting data epoch 118 in logical epoch 118
[2022-12-14 15:50:27] [data] Shuffling data
[2022-12-14 15:50:27] [data] Done reading 40,000 sentences
[2022-12-14 15:50:27] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:51:39] Seen 39,999 samples
[2022-12-14 15:51:39] Starting data epoch 119 in logical epoch 119
[2022-12-14 15:51:39] [data] Shuffling data
[2022-12-14 15:51:39] [data] Done reading 40,000 sentences
[2022-12-14 15:51:39] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:52:10] Ep. 119 : Up. 38500 : Sen. 16,806 : Cost 0.05813313 * 899,959 @ 1,872 after 69,062,990 : Time 110.33s : 8157.17 words/s : gNorm 1.5185
[2022-12-14 15:52:50] Seen 39,999 samples
[2022-12-14 15:52:50] Starting data epoch 120 in logical epoch 120
[2022-12-14 15:52:50] [data] Shuffling data
[2022-12-14 15:52:50] [data] Done reading 40,000 sentences
[2022-12-14 15:52:50] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:53:59] Ep. 120 : Up. 39000 : Sen. 38,869 : Cost 0.06746861 * 899,108 @ 2,127 after 69,962,098 : Time 109.67s : 8198.26 words/s : gNorm 0.9314
[2022-12-14 15:54:01] Seen 39,999 samples
[2022-12-14 15:54:01] Starting data epoch 121 in logical epoch 121
[2022-12-14 15:54:01] [data] Shuffling data
[2022-12-14 15:54:01] [data] Done reading 40,000 sentences
[2022-12-14 15:54:01] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 15:55:13] Seen 39,999 samples
[2022-12-14 15:55:13] Starting data epoch 122 in logical epoch 122
[2022-12-14 15:55:13] [data] Shuffling data
[2022-12-14 15:55:13] [data] Done reading 40,000 sentences
[2022-12-14 15:55:13] [data] Done shuffling 40,000 sentences to temp files
...
...
...
[2022-12-14 17:11:51] Ep. 184 : Up. 59500 : Sen. 836 : Cost 0.04712217 * 896,282 @ 2,142 after 106,723,761 : Time 109.18s : 8208.89 words/s : gNorm 0.7498
[2022-12-14 17:13:02] Seen 39,999 samples
[2022-12-14 17:13:02] Starting data epoch 185 in logical epoch 185
[2022-12-14 17:13:02] [data] Shuffling data
[2022-12-14 17:13:02] [data] Done reading 40,000 sentences
[2022-12-14 17:13:02] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 17:13:42] Ep. 185 : Up. 60000 : Sen. 22,137 : Cost 0.04233031 * 898,372 @ 1,963 after 107,622,133 : Time 110.95s : 8096.90 words/s : gNorm 0.9273
[2022-12-14 17:13:42] Saving model weights and runtime parameters to model.seq2seq.sent1/model.iter60000.npz
[2022-12-14 17:13:43] Saving model weights and runtime parameters to model.seq2seq.sent1/model.npz
[2022-12-14 17:13:48] Saving Adam parameters
[2022-12-14 17:13:52] [training] Saving training checkpoint to model.seq2seq.sent1/model.npz and model.seq2seq.sent1/model.npz.optimizer.npz
[2022-12-14 17:14:12] [valid] Ep. 185 : Up. 60000 : cross-entropy : 0.200939 : new best
[2022-12-14 17:14:15] [valid] Ep. 185 : Up. 60000 : perplexity : 1.01407 : new best
[2022-12-14 17:14:15] Translating validation set...
[2022-12-14 17:14:16] Best translation 0 : B O O O O O O O O O N N N E
[2022-12-14 17:14:16] Best translation 1 : B O O N N N E
[2022-12-14 17:14:16] Best translation 2 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 17:14:16] Best translation 3 : B O O O O O O O O O O O O O O O O N N N E
[2022-12-14 17:14:16] Best translation 4 : B O O N N N E
[2022-12-14 17:14:16] Best translation 5 : B O O O N N N E
...
...
...
[2022-12-14 20:43:03] Best translation 80 : B O O O O O O O O O O N N N E
[2022-12-14 20:43:03] Best translation 160 : B O O O O O O O O O O N N N E
[2022-12-14 20:43:04] Best translation 320 : B O O O O O N N N E
[2022-12-14 20:43:04] Best translation 640 : B O O O O O O O O O N N N E
[2022-12-14 20:43:05] Best translation 1280 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 20:43:07] Total translation time: 4.74008s
[2022-12-14 20:43:07] [valid] Ep. 354 : Up. 115000 : bleu : 99.7362 : stalled 5 times (last best: 99.7636)
[2022-12-14 20:43:22] Seen 39,999 samples
[2022-12-14 20:43:22] Starting data epoch 355 in logical epoch 355
[2022-12-14 20:43:22] [data] Shuffling data
[2022-12-14 20:43:22] [data] Done reading 40,000 sentences
[2022-12-14 20:43:22] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 20:44:33] Seen 39,999 samples
[2022-12-14 20:44:33] Starting data epoch 356 in logical epoch 356
[2022-12-14 20:44:33] [data] Shuffling data
[2022-12-14 20:44:33] [data] Done reading 40,000 sentences
[2022-12-14 20:44:33] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 20:44:59] Ep. 356 : Up. 115500 : Sen. 13,546 : Cost 0.02967916 * 899,464 @ 1,762 after 207,218,356 : Time 149.92s : 5999.73 words/s : gNorm 0.6979
[2022-12-14 20:45:45] Seen 39,999 samples
[2022-12-14 20:45:45] Starting data epoch 357 in logical epoch 357
[2022-12-14 20:45:45] [data] Shuffling data
[2022-12-14 20:45:45] [data] Done reading 40,000 sentences
[2022-12-14 20:45:45] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 20:46:47] Ep. 357 : Up. 116000 : Sen. 35,249 : Cost 0.02715895 * 897,464 @ 960 after 208,115,820 : Time 108.33s : 8284.39 words/s : gNorm 0.5315
[2022-12-14 20:46:56] Seen 39,999 samples
[2022-12-14 20:46:56] Starting data epoch 358 in logical epoch 358
[2022-12-14 20:46:56] [data] Shuffling data
[2022-12-14 20:46:56] [data] Done reading 40,000 sentences
[2022-12-14 20:46:56] [data] Done shuffling 40,000 sentences to temp files
...
...
...
[2022-12-14 21:58:25] Saving Adam parameters
[2022-12-14 21:58:28] [training] Saving training checkpoint to model.seq2seq.sent1/model.npz and model.seq2seq.sent1/model.npz.optimizer.npz
[2022-12-14 21:58:49] [valid] Ep. 416 : Up. 135000 : cross-entropy : 0.21255 : stalled 10 times (last best: 0.195737)
[2022-12-14 21:58:52] [valid] Ep. 416 : Up. 135000 : perplexity : 1.01488 : stalled 10 times (last best: 1.0137)
[2022-12-14 21:58:52] Translating validation set...
[2022-12-14 21:58:53] Best translation 0 : B O O O O O O O O O N N N E
[2022-12-14 21:58:53] Best translation 1 : B O O N N N E
[2022-12-14 21:58:53] Best translation 2 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 21:58:53] Best translation 3 : B O O O O O O O O O O O O O O O O N N N E
[2022-12-14 21:58:53] Best translation 4 : B O O N N N E
[2022-12-14 21:58:53] Best translation 5 : B O O O N N N E
[2022-12-14 21:58:53] Best translation 10 : B N N E
[2022-12-14 21:58:53] Best translation 20 : B O O O N N N E
[2022-12-14 21:58:53] Best translation 40 : B N N N E
[2022-12-14 21:58:53] Best translation 80 : B O O O O O O O O O O N N N E
[2022-12-14 21:58:53] Best translation 160 : B O O O O O O O O O O N N N E
[2022-12-14 21:58:53] Best translation 320 : B O O O O O N N N E
[2022-12-14 21:58:54] Best translation 640 : B O O O O O O O O O N N N E
[2022-12-14 21:58:55] Best translation 1280 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 21:58:57] Total translation time: 4.71705s
[2022-12-14 21:58:57] [valid] Ep. 416 : Up. 135000 : bleu : 99.8157 : stalled 2 times (last best: 99.8297)
[2022-12-14 21:58:57] Training finished
[2022-12-14 21:58:57] Saving model weights and runtime parameters to model.seq2seq.sent1/model.npz
[2022-12-14 21:59:02] Saving Adam parameters
[2022-12-14 21:59:05] [training] Saving training checkpoint to model.seq2seq.sent1/model.npz and model.seq2seq.sent1/model.npz.optimizer.npz

real    513m43.765s
user    504m31.305s
sys     5m17.232s
root@57452252667f:/home/ye/exp/mysent#
```

Training of Seq2Seq model finished successfully!  

Config yml file for reference:  

```
# Marian configuration file generated at 2022-12-14 13:25:39 +0000 with version v1.11.0 f00d0621 2022-02-08 08:39:24 -0800
# General options
authors: false
cite: false
build-info: ""
workspace: 4500
log: model.seq2seq.sent1/train.log
log-level: info
log-time-zone: ""
quiet: false
quiet-translation: false
seed: 1111
check-nan: false
interpolate-env-vars: false
relative-paths: false
sigterm: save-and-exit
# Model options
model: model.seq2seq.sent1/model.npz
pretrained-model: ""
ignore-model-config: false
type: s2s
dim-vocabs:
  - 0
  - 0
dim-emb: 512
factors-dim-emb: 0
factors-combine: sum
lemma-dependency: ""
lemma-dim-emb: 0
dim-rnn: 1024
enc-type: alternating
enc-cell: lstm
enc-cell-depth: 4
enc-depth: 3
dec-cell: lstm
dec-cell-base-depth: 4
dec-cell-high-depth: 2
dec-depth: 3
skip: true
layer-normalization: true
right-left: false
input-types:
  []
best-deep: false
tied-embeddings: true
tied-embeddings-src: false
tied-embeddings-all: false
output-omit-bias: false
transformer-heads: 8
transformer-no-projection: false
transformer-pool: false
transformer-dim-ffn: 2048
transformer-decoder-dim-ffn: 0
transformer-ffn-depth: 2
transformer-decoder-ffn-depth: 0
transformer-ffn-activation: swish
transformer-dim-aan: 2048
transformer-aan-depth: 2
transformer-aan-activation: swish
transformer-aan-nogate: false
transformer-decoder-autoreg: self-attention
transformer-tied-layers:
  []
transformer-guided-alignment-layer: last
transformer-preprocess: ""
transformer-postprocess-emb: d
transformer-postprocess: dan
transformer-postprocess-top: ""
transformer-train-position-embeddings: false
transformer-depth-scaling: false
bert-mask-symbol: "[MASK]"
bert-sep-symbol: "[SEP]"
bert-class-symbol: "[CLS]"
bert-masking-fraction: 0.15
bert-train-type-embeddings: true
bert-type-vocab-size: 2
dropout-rnn: 0.3
dropout-src: 0.3
dropout-trg: 0
transformer-dropout: 0
transformer-dropout-attention: 0
transformer-dropout-ffn: 0
# Training options
cost-type: ce-sum
multi-loss-type: sum
unlikelihood-loss: false
overwrite: false
no-reload: false
train-sets:
  - /home/ye/exp/mysent/data-sent/train.my
  - /home/ye/exp/mysent/data-sent/train.tg
vocabs:
  - /home/ye/exp/mysent/data-sent/vocab/vocab.my.yml
  - /home/ye/exp/mysent/data-sent/vocab/vocab.tg.yml
sentencepiece-alphas:
  []
sentencepiece-options: ""
sentencepiece-max-lines: 2000000
after-epochs: 0
after-batches: 0
after: 0e
disp-freq: 500
disp-first: 0
disp-label-counts: true
save-freq: 5000
logical-epoch:
  - 1e
  - 0
max-length: 200
max-length-crop: false
tsv: false
tsv-fields: 0
shuffle: data
no-shuffle: false
no-restore-corpus: false
tempdir: /tmp
sqlite: ""
sqlite-drop: false
devices:
  - 0
num-devices: 0
no-nccl: false
sharding: global
sync-freq: 200u
cpu-threads: 0
mini-batch: 64
mini-batch-words: 0
mini-batch-fit: true
mini-batch-fit-step: 10
gradient-checkpointing: false
maxi-batch: 100
maxi-batch-sort: trg
shuffle-in-ram: false
data-threads: 8
all-caps-every: 0
english-title-case-every: 0
mini-batch-words-ref: 0
mini-batch-warmup: 0
mini-batch-track-lr: false
mini-batch-round-up: true
optimizer: adam
optimizer-params:
  []
optimizer-delay: 1
sync-sgd: true
learn-rate: 0.0001
lr-report: false
lr-decay: 0
lr-decay-strategy: epoch+stalled
lr-decay-start:
  - 10
  - 1
lr-decay-freq: 50000
lr-decay-reset-optimizer: false
lr-decay-repeat-warmup: false
lr-decay-inv-sqrt:
  - 0
lr-warmup: 0
lr-warmup-start-rate: 0
lr-warmup-cycle: false
lr-warmup-at-reload: false
label-smoothing: 0
factor-weight: 1
clip-norm: 1
exponential-smoothing: 0.0001
guided-alignment: none
guided-alignment-cost: mse
guided-alignment-weight: 0.1
data-weighting: ""
data-weighting-type: sentence
embedding-vectors:
  []
embedding-normalization: false
embedding-fix-src: false
embedding-fix-trg: false
fp16: false
precision:
  - float32
  - float32
cost-scaling:
  []
gradient-norm-average-window: 100
dynamic-gradient-scaling:
  []
check-gradient-nan: false
normalize-gradient: false
train-embedder-rank:
  []
quantize-bits: 0
quantize-optimization-steps: 0
quantize-log-based: false
quantize-biases: false
ulr: false
ulr-query-vectors: ""
ulr-keys-vectors: ""
ulr-trainable-transformation: false
ulr-dim-emb: 0
ulr-dropout: 0
ulr-softmax-temperature: 1
task:
  []
# Validation set options
valid-sets:
  - /home/ye/exp/mysent/data-sent/valid.my
  - /home/ye/exp/mysent/data-sent/valid.tg
valid-freq: 5000
valid-metrics:
  - cross-entropy
  - perplexity
  - bleu
valid-reset-stalled: false
early-stopping: 10
early-stopping-on: first
beam-size: 12
normalize: 0
max-length-factor: 3
word-penalty: 0
allow-unk: false
n-best: false
word-scores: false
valid-mini-batch: 32
valid-max-length: 1000
valid-script-path: ""
valid-script-args:
  []
valid-translation-output: ""
keep-best: false
valid-log: model.seq2seq.sent1/valid.log
```

Check the model folder:  

```
root@57452252667f:/home/ye/exp/mysent/model.seq2seq.sent1# ls
config.yml            model.iter130000.npz  model.iter45000.npz  model.iter80000.npz      model.npz.yml
model.iter10000.npz   model.iter135000.npz  model.iter5000.npz   model.iter85000.npz      s2s.my-tg.log1
model.iter100000.npz  model.iter15000.npz   model.iter50000.npz  model.iter90000.npz      train.log
model.iter105000.npz  model.iter20000.npz   model.iter55000.npz  model.iter95000.npz      valid.log
model.iter110000.npz  model.iter25000.npz   model.iter60000.npz  model.npz
model.iter115000.npz  model.iter30000.npz   model.iter65000.npz  model.npz.decoder.yml
model.iter120000.npz  model.iter35000.npz   model.iter70000.npz  model.npz.optimizer.npz
model.iter125000.npz  model.iter40000.npz   model.iter75000.npz  model.npz.progress.yml
root@57452252667f:/home/ye/exp/mysent/model.seq2seq.sent1#
```

Check the validation log ...  

```
[2022-12-14 13:44:58] [valid] Ep. 16 : Up. 5000 : cross-entropy : 1.68563 : new best
[2022-12-14 13:45:01] [valid] Ep. 16 : Up. 5000 : perplexity : 1.12431 : new best
[2022-12-14 13:45:01] [valid] First sentence's tokens as scored:
[2022-12-14 13:45:01] [valid] DefaultVocab keeps original segments for scoring
[2022-12-14 13:45:01] [valid]   Hyp: B O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 13:45:01] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O >
[2022-12-14 13:45:07] [valid] Ep. 16 : Up. 5000 : bleu : 86.874 : new best
[2022-12-14 14:03:58] [valid] Ep. 31 : Up. 10000 : cross-entropy : 0.462362 : new best
[2022-12-14 14:04:01] [valid] Ep. 31 : Up. 10000 : perplexity : 1.03266 : new best
[2022-12-14 14:04:06] [valid] Ep. 31 : Up. 10000 : bleu : 98.3967 : new best
[2022-12-14 14:23:01] [valid] Ep. 47 : Up. 15000 : cross-entropy : 0.290361 : new best
[2022-12-14 14:23:05] [valid] Ep. 47 : Up. 15000 : perplexity : 1.02039 : new best
[2022-12-14 14:23:10] [valid] Ep. 47 : Up. 15000 : bleu : 99.2319 : new best
[2022-12-14 14:42:05] [valid] Ep. 62 : Up. 20000 : cross-entropy : 0.243329 : new best
[2022-12-14 14:42:08] [valid] Ep. 62 : Up. 20000 : perplexity : 1.01706 : new best
[2022-12-14 14:42:13] [valid] Ep. 62 : Up. 20000 : bleu : 99.5307 : new best
[2022-12-14 15:01:06] [valid] Ep. 77 : Up. 25000 : cross-entropy : 0.36264 : stalled 1 times (last best: 0.243329)
[2022-12-14 15:01:10] [valid] Ep. 77 : Up. 25000 : perplexity : 1.02553 : stalled 1 times (last best: 1.01706)
[2022-12-14 15:01:15] [valid] Ep. 77 : Up. 25000 : bleu : 98.5923 : stalled 1 times (last best: 99.5307)
[2022-12-14 15:20:08] [valid] Ep. 93 : Up. 30000 : cross-entropy : 0.472565 : stalled 2 times (last best: 0.243329)
[2022-12-14 15:20:12] [valid] Ep. 93 : Up. 30000 : perplexity : 1.03339 : stalled 2 times (last best: 1.01706)
[2022-12-14 15:20:17] [valid] Ep. 93 : Up. 30000 : bleu : 97.6784 : stalled 2 times (last best: 99.5307)
[2022-12-14 15:39:10] [valid] Ep. 108 : Up. 35000 : cross-entropy : 0.30005 : stalled 3 times (last best: 0.243329)
[2022-12-14 15:39:13] [valid] Ep. 108 : Up. 35000 : perplexity : 1.02108 : stalled 3 times (last best: 1.01706)
[2022-12-14 15:39:18] [valid] Ep. 108 : Up. 35000 : bleu : 98.845 : stalled 3 times (last best: 99.5307)
[2022-12-14 15:58:11] [valid] Ep. 124 : Up. 40000 : cross-entropy : 0.263489 : stalled 4 times (last best: 0.243329)
[2022-12-14 15:58:14] [valid] Ep. 124 : Up. 40000 : perplexity : 1.01848 : stalled 4 times (last best: 1.01706)
[2022-12-14 15:58:19] [valid] Ep. 124 : Up. 40000 : bleu : 99.1113 : stalled 4 times (last best: 99.5307)
[2022-12-14 16:17:12] [valid] Ep. 139 : Up. 45000 : cross-entropy : 0.234904 : new best
[2022-12-14 16:17:15] [valid] Ep. 139 : Up. 45000 : perplexity : 1.01646 : new best
[2022-12-14 16:17:20] [valid] Ep. 139 : Up. 45000 : bleu : 99.3629 : stalled 5 times (last best: 99.5307)
[2022-12-14 16:36:11] [valid] Ep. 154 : Up. 50000 : cross-entropy : 0.219318 : new best
[2022-12-14 16:36:15] [valid] Ep. 154 : Up. 50000 : perplexity : 1.01536 : new best
[2022-12-14 16:36:19] [valid] Ep. 154 : Up. 50000 : bleu : 99.4958 : stalled 6 times (last best: 99.5307)
[2022-12-14 16:55:12] [valid] Ep. 170 : Up. 55000 : cross-entropy : 0.216073 : new best
[2022-12-14 16:55:16] [valid] Ep. 170 : Up. 55000 : perplexity : 1.01513 : new best
[2022-12-14 16:55:20] [valid] Ep. 170 : Up. 55000 : bleu : 99.6284 : new best
[2022-12-14 17:14:12] [valid] Ep. 185 : Up. 60000 : cross-entropy : 0.200939 : new best
[2022-12-14 17:14:15] [valid] Ep. 185 : Up. 60000 : perplexity : 1.01407 : new best
[2022-12-14 17:14:20] [valid] Ep. 185 : Up. 60000 : bleu : 99.611 : stalled 1 times (last best: 99.6284)
[2022-12-14 17:33:14] [valid] Ep. 200 : Up. 65000 : cross-entropy : 0.204643 : stalled 1 times (last best: 0.200939)
[2022-12-14 17:33:17] [valid] Ep. 200 : Up. 65000 : perplexity : 1.01433 : stalled 1 times (last best: 1.01407)
[2022-12-14 17:33:22] [valid] Ep. 200 : Up. 65000 : bleu : 99.6407 : new best
[2022-12-14 17:52:14] [valid] Ep. 216 : Up. 70000 : cross-entropy : 0.208755 : stalled 2 times (last best: 0.200939)
[2022-12-14 17:52:17] [valid] Ep. 216 : Up. 70000 : perplexity : 1.01462 : stalled 2 times (last best: 1.01407)
[2022-12-14 17:52:22] [valid] Ep. 216 : Up. 70000 : bleu : 99.6003 : stalled 1 times (last best: 99.6407)
[2022-12-14 18:11:13] [valid] Ep. 231 : Up. 75000 : cross-entropy : 0.208598 : stalled 3 times (last best: 0.200939)
[2022-12-14 18:11:16] [valid] Ep. 231 : Up. 75000 : perplexity : 1.01461 : stalled 3 times (last best: 1.01407)
[2022-12-14 18:11:21] [valid] Ep. 231 : Up. 75000 : bleu : 99.6204 : stalled 2 times (last best: 99.6407)
[2022-12-14 18:30:14] [valid] Ep. 247 : Up. 80000 : cross-entropy : 0.208252 : stalled 4 times (last best: 0.200939)
[2022-12-14 18:30:18] [valid] Ep. 247 : Up. 80000 : perplexity : 1.01458 : stalled 4 times (last best: 1.01407)
[2022-12-14 18:30:22] [valid] Ep. 247 : Up. 80000 : bleu : 99.5666 : stalled 3 times (last best: 99.6407)
[2022-12-14 18:49:12] [valid] Ep. 262 : Up. 85000 : cross-entropy : 0.195737 : new best
[2022-12-14 18:49:16] [valid] Ep. 262 : Up. 85000 : perplexity : 1.0137 : new best
[2022-12-14 18:49:20] [valid] Ep. 262 : Up. 85000 : bleu : 99.6938 : new best
[2022-12-14 19:08:09] [valid] Ep. 277 : Up. 90000 : cross-entropy : 0.198068 : stalled 1 times (last best: 0.195737)
[2022-12-14 19:08:13] [valid] Ep. 277 : Up. 90000 : perplexity : 1.01386 : stalled 1 times (last best: 1.0137)
[2022-12-14 19:08:17] [valid] Ep. 277 : Up. 90000 : bleu : 99.7636 : new best
[2022-12-14 19:27:06] [valid] Ep. 293 : Up. 95000 : cross-entropy : 0.210209 : stalled 2 times (last best: 0.195737)
[2022-12-14 19:27:09] [valid] Ep. 293 : Up. 95000 : perplexity : 1.01472 : stalled 2 times (last best: 1.0137)
[2022-12-14 19:27:14] [valid] Ep. 293 : Up. 95000 : bleu : 99.6863 : stalled 1 times (last best: 99.7636)
[2022-12-14 19:46:03] [valid] Ep. 308 : Up. 100000 : cross-entropy : 0.214344 : stalled 3 times (last best: 0.195737)
[2022-12-14 19:46:06] [valid] Ep. 308 : Up. 100000 : perplexity : 1.01501 : stalled 3 times (last best: 1.0137)
[2022-12-14 19:46:11] [valid] Ep. 308 : Up. 100000 : bleu : 99.6619 : stalled 2 times (last best: 99.7636)
[2022-12-14 20:05:03] [valid] Ep. 324 : Up. 105000 : cross-entropy : 0.212723 : stalled 4 times (last best: 0.195737)
[2022-12-14 20:05:07] [valid] Ep. 324 : Up. 105000 : perplexity : 1.0149 : stalled 4 times (last best: 1.0137)
[2022-12-14 20:05:11] [valid] Ep. 324 : Up. 105000 : bleu : 99.6977 : stalled 3 times (last best: 99.7636)
[2022-12-14 20:24:02] [valid] Ep. 339 : Up. 110000 : cross-entropy : 0.214246 : stalled 5 times (last best: 0.195737)
[2022-12-14 20:24:05] [valid] Ep. 339 : Up. 110000 : perplexity : 1.015 : stalled 5 times (last best: 1.0137)
[2022-12-14 20:24:10] [valid] Ep. 339 : Up. 110000 : bleu : 99.7002 : stalled 4 times (last best: 99.7636)
[2022-12-14 20:42:59] [valid] Ep. 354 : Up. 115000 : cross-entropy : 0.213579 : stalled 6 times (last best: 0.195737)
[2022-12-14 20:43:03] [valid] Ep. 354 : Up. 115000 : perplexity : 1.01496 : stalled 6 times (last best: 1.0137)
[2022-12-14 20:43:07] [valid] Ep. 354 : Up. 115000 : bleu : 99.7362 : stalled 5 times (last best: 99.7636)
[2022-12-14 21:01:59] [valid] Ep. 370 : Up. 120000 : cross-entropy : 0.210968 : stalled 7 times (last best: 0.195737)
[2022-12-14 21:02:03] [valid] Ep. 370 : Up. 120000 : perplexity : 1.01477 : stalled 7 times (last best: 1.0137)
[2022-12-14 21:02:07] [valid] Ep. 370 : Up. 120000 : bleu : 99.7887 : new best
[2022-12-14 21:20:56] [valid] Ep. 385 : Up. 125000 : cross-entropy : 0.206392 : stalled 8 times (last best: 0.195737)
[2022-12-14 21:21:00] [valid] Ep. 385 : Up. 125000 : perplexity : 1.01445 : stalled 8 times (last best: 1.0137)
[2022-12-14 21:21:04] [valid] Ep. 385 : Up. 125000 : bleu : 99.8297 : new best
[2022-12-14 21:39:52] [valid] Ep. 400 : Up. 130000 : cross-entropy : 0.212311 : stalled 9 times (last best: 0.195737)
[2022-12-14 21:39:56] [valid] Ep. 400 : Up. 130000 : perplexity : 1.01487 : stalled 9 times (last best: 1.0137)
[2022-12-14 21:40:00] [valid] Ep. 400 : Up. 130000 : bleu : 99.8297 : stalled 1 times (last best: 99.8297)
[2022-12-14 21:58:49] [valid] Ep. 416 : Up. 135000 : cross-entropy : 0.21255 : stalled 10 times (last best: 0.195737)
[2022-12-14 21:58:52] [valid] Ep. 416 : Up. 135000 : perplexity : 1.01488 : stalled 10 times (last best: 1.0137)
[2022-12-14 21:58:57] [valid] Ep. 416 : Up. 135000 : bleu : 99.8157 : stalled 2 times (last best: 99.8297)
```

## Training Transformer Model for Sentence Only Dataset  

check the shell script ...  

```bash
root@57452252667f:/home/ye/exp/mysent# head -n 30 ./transformer.sent1.sh
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for mySent, also preparation for 4th NLP/AI Workshop 2022

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer.sent1;

marian \
    --model model.transformer.sent1/model.npz --type transformer \
    --train-sets data-sent/train.my data-sent/train.tg \
    --max-length 200 \
    --vocabs data-sent/vocab/vocab.my.yml data-sent/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-sent/valid.my data-sent/valid.tg \
    --valid-translation-output model.transformer.sent1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 32 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.sent1/train.log --valid-log model.transformer.sent1/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.sent1/config.yml

time marian -c model.transformer.sent1/config.yml  2>&1 | tee transformer.sent1.log
root@57452252667f:/home/ye/exp/mysent#
```

Start training ...  

```
[2022-12-14 22:41:12] [batching] Collecting statistics for batch fitting with step size 10
[2022-12-14 22:41:12] Error: Curand error 203 - /temp/marian/src/tensors/rand.cpp:74: curandCreateGenerator(&generator_, CURAN
D_RNG_PSEUDO_DEFAULT)
[2022-12-14 22:41:12] Error: Aborted from marian::CurandRandomGenerator::CurandRandomGenerator(size_t, marian::DeviceId) in /temp/marian/src/tensors/rand.cpp:74

[CALL STACK]
[0x561f9e061050]    marian::CurandRandomGenerator::  CurandRandomGenerator  (unsigned long,  marian::DeviceId) + 0x750
[0x561f9e061689]    marian::  createRandomGenerator  (unsigned long,  marian::DeviceId) + 0x69
[0x561f9e05bf20]    marian::  BackendByDeviceId  (marian::DeviceId,  unsigned long) + 0xa0
[0x561f9db4b220]    marian::ExpressionGraph::  setDevice  (marian::DeviceId,  std::shared_ptr<marian::Device>) + 0x80
[0x561f9de44cd5]    marian::GraphGroup::  initGraphsAndOpts  ()        + 0x1e5
[0x561f9de461f8]    marian::GraphGroup::  GraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x548
[0x561f9de24773]    marian::SyncGraphGroup::  SyncGraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x83
[0x561f9d97d8ab]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x1c2b
[0x561f9d8ab347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f01da7d5d90]                                                       + 0x29d90
[0x7f01da7d5e40]    __libc_start_main                                  + 0x80
[0x561f9d8a4995]    _start                                             + 0x25
```

I got above error for the 1st time training ...  
Logout the LST GPU server and run again ...  

```

...
...
...
[2022-12-14 22:48:05] [data] Done reading 40,000 sentences
[2022-12-14 22:48:05] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:48:10] Seen 39,999 samples
[2022-12-14 22:48:10] Starting data epoch 7 in logical epoch 7
[2022-12-14 22:48:10] [data] Shuffling data
[2022-12-14 22:48:10] [data] Done reading 40,000 sentences
[2022-12-14 22:48:10] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:48:11] Ep. 7 : Up. 1500 : Sen. 12,425 : Cost 0.65929031 * 1,219,768 @ 3,178 after 3,680,385 : Time 8.93s : 136585.49 words/s : gNorm 1.9825 : L.r. 3.0000e-04
[2022-12-14 22:48:14] Seen 39,999 samples
[2022-12-14 22:48:14] Starting data epoch 8 in logical epoch 8
[2022-12-14 22:48:14] [data] Shuffling data
[2022-12-14 22:48:14] [data] Done reading 40,000 sentences
[2022-12-14 22:48:14] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:48:18] Seen 39,999 samples
[2022-12-14 22:48:18] Starting data epoch 9 in logical epoch 9
[2022-12-14 22:48:18] [data] Shuffling data
[2022-12-14 22:48:18] [data] Done reading 40,000 sentences
[2022-12-14 22:48:18] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:48:20] Ep. 9 : Up. 2000 : Sen. 16,159 : Cost 0.62157410 * 1,219,910 @ 2,016 after 4,900,295 : Time 8.97s : 136033.51 words/s : gNorm 2.0888 : L.r. 3.0000e-04
[2022-12-14 22:48:22] Seen 39,999 samples
[2022-12-14 22:48:22] Starting data epoch 10 in logical epoch 10
[2022-12-14 22:48:22] [data] Shuffling data
[2022-12-14 22:48:22] [data] Done reading 40,000 sentences
[2022-12-14 22:48:22] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:48:27] Seen 39,999 samples
[2022-12-14 22:48:27] Starting data epoch 11 in logical epoch 11
[2022-12-14 22:48:27] [data] Shuffling data
[2022-12-14 22:48:27] [data] Done reading 40,000 sentences
[2022-12-14 22:48:27] [data] Done shuffling 40,000 sentences to temp files
...
...
...
[2022-12-14 22:49:14] Starting data epoch 22 in logical epoch 22
[2022-12-14 22:49:14] [data] Shuffling data
[2022-12-14 22:49:14] [data] Done reading 40,000 sentences
[2022-12-14 22:49:14] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:49:14] Ep. 22 : Up. 5000 : Sen. 1,367 : Cost 0.55348921 * 1,221,496 @ 3,089 after 12,261,807 : Time 9.07s : 134679.56 words/s : gNorm 1.6216 : L.r. 3.0000e-04
[2022-12-14 22:49:14] Saving model weights and runtime parameters to model.transformer.sent1/model.iter5000.npz
[2022-12-14 22:49:14] Saving model weights and runtime parameters to model.transformer.sent1/model.npz
[2022-12-14 22:49:14] Saving Adam parameters
[2022-12-14 22:49:15] [training] Saving training checkpoint to model.transformer.sent1/model.npz and model.transformer.sent1/model.npz.optimizer.npz
[2022-12-14 22:49:16] [valid] Ep. 22 : Up. 5000 : cross-entropy : 14.7751 : new best
[2022-12-14 22:49:16] [valid] Ep. 22 : Up. 5000 : perplexity : 2.79271 : new best
[2022-12-14 22:49:16] [valid] First sentence's tokens as scored:
[2022-12-14 22:49:16] [valid] DefaultVocab keeps original segments for scoring
[2022-12-14 22:49:16] [valid]   Hyp: B O O O O O O O O O O O O O O N N N E
[2022-12-14 22:49:16] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-14 22:49:17] [valid] Ep. 22 : Up. 5000 : bleu : 44.6635 : new best
[2022-12-14 22:49:21] Seen 39,999 samples
[2022-12-14 22:49:21] Starting data epoch 23 in logical epoch 23
[2022-12-14 22:49:21] [data] Shuffling data
[2022-12-14 22:49:21] [data] Done reading 40,000 sentences
[2022-12-14 22:49:21] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:49:25] Seen 39,999 samples
[2022-12-14 22:49:25] Starting data epoch 24 in logical epoch 24
[2022-12-14 22:49:25] [data] Shuffling data
[2022-12-14 22:49:25] [data] Done reading 40,000 sentences
[2022-12-14 22:49:25] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 22:49:26] Ep. 24 : Up. 5500 : Sen. 4,930 : Cost 0.54646653 * 1,225,667 @ 1,602 after 13,487,474 : Time 11.91s : 102934.00 words/s : gNorm 1.5340 : L.r. 3.0000e-04
...
...
...

```

```

```

```

```

```

```

```

```

```

```


## Testing  

check testing shell script ...  

```bash

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
