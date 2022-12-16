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
root@d7ccd8169efe:/home/ye/exp/mysent# ./transformer.sent1.sh
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
[2022-12-14 23:15:18] Ep. 355 : Up. 84500 : Sen. 30,247 : Cost 0.43526506 * 1,229,177 @ 3,415 after 206,866,413 : Time 9.15s : 134392.88 words/s : gNorm 1.0762 : L.r. 1.3054e-04
[2022-12-14 23:15:19] Seen 39,999 samples
[2022-12-14 23:15:19] Starting data epoch 356 in logical epoch 356
[2022-12-14 23:15:19] [data] Shuffling data
[2022-12-14 23:15:19] [data] Done reading 40,000 sentences
[2022-12-14 23:15:19] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 23:15:23] Seen 39,999 samples
[2022-12-14 23:15:23] Starting data epoch 357 in logical epoch 357
[2022-12-14 23:15:23] [data] Shuffling data
[2022-12-14 23:15:23] [data] Done reading 40,000 sentences
[2022-12-14 23:15:23] [data] Done shuffling 40,000 sentences to temp files
[2022-12-14 23:15:27] Ep. 357 : Up. 85000 : Sen. 34,104 : Cost 0.43605182 * 1,225,329 @ 3,002 after 208,091,742 : Time 9.19s : 133277.71 words/s : gNorm 1.2420 : L.r. 1.3016e-04
[2022-12-14 23:15:27] Saving model weights and runtime parameters to model.transformer.sent1/model.iter85000.npz
[2022-12-14 23:15:27] Saving model weights and runtime parameters to model.transformer.sent1/model.npz
[2022-12-14 23:15:28] Saving Adam parameters
[2022-12-14 23:15:28] [training] Saving training checkpoint to model.transformer.sent1/model.npz and model.transformer.sent1/model.npz.optimizer.npz
[2022-12-14 23:15:31] [valid] Ep. 357 : Up. 85000 : cross-entropy : 1.8711 : stalled 10 times (last best: 1.44142)
[2022-12-14 23:15:32] [valid] Ep. 357 : Up. 85000 : perplexity : 1.1389 : stalled 10 times (last best: 1.10538)
[2022-12-14 23:15:34] [valid] Ep. 357 : Up. 85000 : bleu : 70.8777 : stalled 10 times (last best: 74.3342)
[2022-12-14 23:15:34] Training finished
[2022-12-14 23:15:34] Saving model weights and runtime parameters to model.transformer.sent1/model.npz
[2022-12-14 23:15:35] Saving Adam parameters
[2022-12-14 23:15:35] [training] Saving training checkpoint to model.transformer.sent1/model.npz and model.transformer.sent1/model.npz.optimizer.npz

real    27m56.728s
user    28m38.814s
sys     1m1.540s
root@d7ccd8169efe:/home/ye/exp/mysent#
```

GPU usage information when training Transformer model ...  

```
Every 2.0s: nvidia-smi                                                                  lst-gpu-3090: Thu Dec 15 05:53:47 2022
Thu Dec 15 05:53:47 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.86.01    Driver Version: 515.86.01    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
| 60%   80C    P2   388W / 480W |   2607MiB / 24564MiB |     91%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      3639      G   /usr/lib/xorg/Xorg                 46MiB |
|    0   N/A  N/A      3771      G   /usr/bin/gnome-shell               11MiB |
|    0   N/A  N/A   3958979      C   marian                           2545MiB |
+-----------------------------------------------------------------------------+
```

Training time is very quick and the result is not good compare with Seq2Seq ...  

Check the validation results ...  

```
  1 [2022-12-14 22:49:16] [valid] Ep. 22 : Up. 5000 : cross-entropy : 14.7751 : new best
  2 [2022-12-14 22:49:16] [valid] Ep. 22 : Up. 5000 : perplexity : 2.79271 : new best
  3 [2022-12-14 22:49:16] [valid] First sentence's tokens as scored:
  4 [2022-12-14 22:49:16] [valid] DefaultVocab keeps original segments for scoring
  5 [2022-12-14 22:49:16] [valid]   Hyp: B O O O O O O O O O O O O O O N N N E
  6 [2022-12-14 22:49:16] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O O O O O O O O O N N N E
  7 [2022-12-14 22:49:17] [valid] Ep. 22 : Up. 5000 : bleu : 44.6635 : new best
  8 [2022-12-14 22:50:52] [valid] Ep. 43 : Up. 10000 : cross-entropy : 6.31625 : new best
  9 [2022-12-14 22:50:52] [valid] Ep. 43 : Up. 10000 : perplexity : 1.55122 : new best
 10 [2022-12-14 22:50:54] [valid] Ep. 43 : Up. 10000 : bleu : 73.7783 : new best
 11 [2022-12-14 22:52:29] [valid] Ep. 64 : Up. 15000 : cross-entropy : 3.17262 : new best
 12 [2022-12-14 22:52:30] [valid] Ep. 64 : Up. 15000 : perplexity : 1.24673 : new best
 13 [2022-12-14 22:52:32] [valid] Ep. 64 : Up. 15000 : bleu : 70.1275 : stalled 1 times (last best: 73.7783)
 14 [2022-12-14 22:54:07] [valid] Ep. 84 : Up. 20000 : cross-entropy : 2.06925 : new best
 15 [2022-12-14 22:54:08] [valid] Ep. 84 : Up. 20000 : perplexity : 1.15469 : new best
 16 [2022-12-14 22:54:11] [valid] Ep. 84 : Up. 20000 : bleu : 71.7483 : stalled 2 times (last best: 73.7783)
 17 [2022-12-14 22:55:46] [valid] Ep. 105 : Up. 25000 : cross-entropy : 1.58498 : new best
 18 [2022-12-14 22:55:46] [valid] Ep. 105 : Up. 25000 : perplexity : 1.11647 : new best
 19 [2022-12-14 22:55:49] [valid] Ep. 105 : Up. 25000 : bleu : 73.7227 : stalled 3 times (last best: 73.7783)
 20 [2022-12-14 22:57:25] [valid] Ep. 126 : Up. 30000 : cross-entropy : 1.44841 : new best
 21 [2022-12-14 22:57:25] [valid] Ep. 126 : Up. 30000 : perplexity : 1.10592 : new best
 22 [2022-12-14 22:57:28] [valid] Ep. 126 : Up. 30000 : bleu : 72.4195 : stalled 4 times (last best: 73.7783)
 23 [2022-12-14 22:59:03] [valid] Ep. 147 : Up. 35000 : cross-entropy : 1.44142 : new best
 24 [2022-12-14 22:59:04] [valid] Ep. 147 : Up. 35000 : perplexity : 1.10538 : new best
 25 [2022-12-14 22:59:06] [valid] Ep. 147 : Up. 35000 : bleu : 74.3342 : new best
 26 [2022-12-14 23:00:42] [valid] Ep. 168 : Up. 40000 : cross-entropy : 1.5815 : stalled 1 times (last best: 1.44142)
 27 [2022-12-14 23:00:42] [valid] Ep. 168 : Up. 40000 : perplexity : 1.1162 : stalled 1 times (last best: 1.10538)
 28 [2022-12-14 23:00:45] [valid] Ep. 168 : Up. 40000 : bleu : 73.3137 : stalled 1 times (last best: 74.3342)
 29 [2022-12-14 23:02:20] [valid] Ep. 189 : Up. 45000 : cross-entropy : 1.68953 : stalled 2 times (last best: 1.44142)
 30 [2022-12-14 23:02:21] [valid] Ep. 189 : Up. 45000 : perplexity : 1.12461 : stalled 2 times (last best: 1.10538)
  31 [2022-12-14 23:02:23] [valid] Ep. 189 : Up. 45000 : bleu : 71.7748 : stalled 2 times (last best: 74.3342)
 32 [2022-12-14 23:03:59] [valid] Ep. 210 : Up. 50000 : cross-entropy : 1.80328 : stalled 3 times (last best: 1.44142)
 33 [2022-12-14 23:04:00] [valid] Ep. 210 : Up. 50000 : perplexity : 1.13354 : stalled 3 times (last best: 1.10538)
 34 [2022-12-14 23:04:02] [valid] Ep. 210 : Up. 50000 : bleu : 70.4578 : stalled 3 times (last best: 74.3342)
 35 [2022-12-14 23:05:38] [valid] Ep. 231 : Up. 55000 : cross-entropy : 2.11138 : stalled 4 times (last best: 1.44142)
 36 [2022-12-14 23:05:38] [valid] Ep. 231 : Up. 55000 : perplexity : 1.15808 : stalled 4 times (last best: 1.10538)
 37 [2022-12-14 23:05:41] [valid] Ep. 231 : Up. 55000 : bleu : 69.7287 : stalled 4 times (last best: 74.3342)
 38 [2022-12-14 23:07:17] [valid] Ep. 252 : Up. 60000 : cross-entropy : 2.12543 : stalled 5 times (last best: 1.44142)
 39 [2022-12-14 23:07:17] [valid] Ep. 252 : Up. 60000 : perplexity : 1.15921 : stalled 5 times (last best: 1.10538)
 40 [2022-12-14 23:07:20] [valid] Ep. 252 : Up. 60000 : bleu : 70.613 : stalled 5 times (last best: 74.3342)
 41 [2022-12-14 23:08:56] [valid] Ep. 273 : Up. 65000 : cross-entropy : 2.0917 : stalled 6 times (last best: 1.44142)
 42 [2022-12-14 23:08:56] [valid] Ep. 273 : Up. 65000 : perplexity : 1.15649 : stalled 6 times (last best: 1.10538)
 43 [2022-12-14 23:08:59] [valid] Ep. 273 : Up. 65000 : bleu : 68.2936 : stalled 6 times (last best: 74.3342)
 44 [2022-12-14 23:10:35] [valid] Ep. 294 : Up. 70000 : cross-entropy : 1.87904 : stalled 7 times (last best: 1.44142)
 45 [2022-12-14 23:10:35] [valid] Ep. 294 : Up. 70000 : perplexity : 1.13953 : stalled 7 times (last best: 1.10538)
 46 [2022-12-14 23:10:38] [valid] Ep. 294 : Up. 70000 : bleu : 68.8524 : stalled 7 times (last best: 74.3342)
 47 [2022-12-14 23:12:14] [valid] Ep. 315 : Up. 75000 : cross-entropy : 1.97382 : stalled 8 times (last best: 1.44142)
 48 [2022-12-14 23:12:14] [valid] Ep. 315 : Up. 75000 : perplexity : 1.14706 : stalled 8 times (last best: 1.10538)
 49 [2022-12-14 23:12:16] [valid] Ep. 315 : Up. 75000 : bleu : 70.2999 : stalled 8 times (last best: 74.3342)
 50 [2022-12-14 23:13:52] [valid] Ep. 336 : Up. 80000 : cross-entropy : 2.10864 : stalled 9 times (last best: 1.44142)
 51 [2022-12-14 23:13:53] [valid] Ep. 336 : Up. 80000 : perplexity : 1.15786 : stalled 9 times (last best: 1.10538)
 52 [2022-12-14 23:13:55] [valid] Ep. 336 : Up. 80000 : bleu : 70.4615 : stalled 9 times (last best: 74.3342)
 53 [2022-12-14 23:15:31] [valid] Ep. 357 : Up. 85000 : cross-entropy : 1.8711 : stalled 10 times (last best: 1.44142)
 54 [2022-12-14 23:15:32] [valid] Ep. 357 : Up. 85000 : perplexity : 1.1389 : stalled 10 times (last best: 1.10538)
 55 [2022-12-14 23:15:34] [valid] Ep. 357 : Up. 85000 : bleu : 70.8777 : stalled 10 times (last best: 74.3342)
```

Later I plan to make change the configuration file and try to get the better performance. At first, I wanna finished all 4 models.  

## Training Seq2Seq Model with Sent+Para Dataset

check the shell script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for Myanmar Sentence Segmentation with NMT Seq2Seq Model
## used Marian NMT Framework for seq2seq training with Sent+Para
## Last updated: 25 Oct 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.para1";
mkdir ${model_folder};
data_path="/home/ye/exp/mysent/data-para";
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

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.para.log1
```

Start training ...  

```
...
...
...
[2022-12-15 02:54:07] [valid] Ep. 87 : Up. 40000 : perplexity : 1.38108 : stalled 1 times (last best: 1.07179)
[2022-12-15 02:54:07] Translating validation set...
[2022-12-15 02:54:09] Best translation 0 : B N N N E
[2022-12-15 02:54:09] Best translation 1 : B O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 2 : B N N N E
[2022-12-15 02:54:09] Best translation 3 : B O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 4 : B O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 5 : B O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 10 : B N E B O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 20 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 40 : B O N N N E
[2022-12-15 02:54:09] Best translation 80 : B O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:09] Best translation 160 : B O O N N N E
[2022-12-15 02:54:10] Best translation 320 : B O O O O O O O N N N E B O O O O O O O O O O O O O N N N E
[2022-12-15 02:54:11] Best translation 640 : B O O O O O O O O O O N N N E
[2022-12-15 02:54:14] Best translation 1280 : B O N N N E
[2022-12-15 02:54:21] Best translation 2560 : B O O O N N N E
[2022-12-15 02:54:23] Total translation time: 16.00999s
[2022-12-15 02:54:23] [valid] Ep. 87 : Up. 40000 : bleu : 76.9431 : stalled 2 times (last best: 88.5089)
[2022-12-15 02:56:02] Seen 46,972 samples
[2022-12-15 02:56:02] Starting data epoch 88 in logical epoch 88
[2022-12-15 02:56:02] [data] Shuffling data
[2022-12-15 02:56:02] [data] Done reading 47,002 sentences
[2022-12-15 02:56:03] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 02:56:56] Ep. 88 : Up. 40500 : Sen. 17,517 : Cost 0.07111049 * 942,782 @ 2,216 after 76,337,432 : Time 211.42s : 4459.36 words/s : gNorm 0.7128
[2022-12-15 02:58:23] Seen 46,972 samples
[2022-12-15 02:58:23] Starting data epoch 89 in logical epoch 89
[2022-12-15 02:58:23] [data] Shuffling data
[2022-12-15 02:58:23] [data] Done reading 47,002 sentences
[2022-12-15 02:58:23] [data] Done shuffling 47,002 sentences to temp files
...
...
[2022-12-15 05:31:54] [data] Done reading 47,002 sentences
[2022-12-15 05:31:54] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 05:31:55] Ep. 152 : Up. 70000 : Sen. 1,116 : Cost 0.03759788 * 943,213 @ 1,910 after 131,931,354 : Time 153.02s : 6164.04 words/s : gNorm 0.5551
[2022-12-15 05:31:55] Saving model weights and runtime parameters to model.seq2seq.para1/model.iter70000.npz
[2022-12-15 05:31:57] Saving model weights and runtime parameters to model.seq2seq.para1/model.npz
[2022-12-15 05:32:02] Saving Adam parameters
[2022-12-15 05:32:05] [training] Saving training checkpoint to model.seq2seq.para1/model.npz and model.seq2seq.para1/model.npz.optimizer.npz
[2022-12-15 05:32:31] [valid] Ep. 152 : Up. 70000 : cross-entropy : 1.51153 : stalled 4 times (last best: 1.44147)
[2022-12-15 05:32:38] [valid] Ep. 152 : Up. 70000 : perplexity : 1.07439 : stalled 4 times (last best: 1.07082)
[2022-12-15 05:32:38] Translating validation set...
[2022-12-15 05:32:40] Best translation 0 : B N N N E
[2022-12-15 05:32:40] Best translation 1 : B O O O O O O O O O O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 2 : B N N N E
[2022-12-15 05:32:40] Best translation 3 : B O O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 4 : B O O O O O O O O O O O O O N N N E B O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 5 : B O O O O O O N N N E B O O O O O O O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 10 : B N E B O O O O O N N N E
[2022-12-15 05:32:40] Best translation 20 : B O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 40 : B O N N N E
[2022-12-15 05:32:40] Best translation 80 : B O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O N N N E
[2022-12-15 05:32:40] Best translation 160 : B O O N N N E
[2022-12-15 05:32:41] Best translation 320 : B O O O O O O O O O O O O N N N E B O O O O O N N N E B O O O N N N E B O O O O O O O O O O N N N E
[2022-12-15 05:32:42] Best translation 640 : B O O O O O O O O O O N N N E
[2022-12-15 05:32:45] Best translation 1280 : B O N N N E
[2022-12-15 05:32:50] Best translation 2560 : B O O O N N N E
[2022-12-15 05:32:52] Total translation time: 13.64662s
[2022-12-15 05:32:52] [valid] Ep. 152 : Up. 70000 : bleu : 91.7101 : new best
...
...
...
[2022-12-15 08:10:56] [valid] Ep. 216 : Up. 100000 : perplexity : 1.08698 : stalled 10 times (last best: 1.07082)
[2022-12-15 08:10:56] Translating validation set...
[2022-12-15 08:10:58] Best translation 0 : B N N N E
[2022-12-15 08:10:58] Best translation 1 : B O O O O O O O O O O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 2 : B N N N E
[2022-12-15 08:10:58] Best translation 3 : B O O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 4 : B O O O O O O O O O O O O O N N N E B O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 5 : B O O O O O O N N N E B O O O O O O O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 10 : B N E B O O O O O N N N E
[2022-12-15 08:10:58] Best translation 20 : B O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 40 : B O N N N E
[2022-12-15 08:10:58] Best translation 80 : B O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O N N N E
[2022-12-15 08:10:58] Best translation 160 : B O O N N N E
[2022-12-15 08:10:59] Best translation 320 : B O O O O O O O O O O O O N N N E B O O O O O N N N E B O O O N N N E B O O O O O O O O O O N N N E
[2022-12-15 08:11:00] Best translation 640 : B O O O O O O O O O O N N N E
[2022-12-15 08:11:02] Best translation 1280 : B O N N N E
[2022-12-15 08:11:08] Best translation 2560 : B O O O N N N E
[2022-12-15 08:11:10] Total translation time: 13.27260s
[2022-12-15 08:11:10] [valid] Ep. 216 : Up. 100000 : bleu : 91.7906 : new best
[2022-12-15 08:11:10] Training finished
[2022-12-15 08:11:10] Saving model weights and runtime parameters to model.seq2seq.para1/model.npz
[2022-12-15 08:11:15] Saving Adam parameters
[2022-12-15 08:11:18] [training] Saving training checkpoint to model.seq2seq.para1/model.npz and model.seq2seq.para1/model.npz.optimizer.npz

real    529m48.062s
user    519m19.765s
sys     7m9.349s
root@d7ccd8169efe:/home/ye/exp/mysent#
```

check the models ... 

```
root@d7ccd8169efe:/home/ye/exp/mysent/model.seq2seq.para1# ls
config.yml            model.iter30000.npz  model.iter55000.npz  model.iter85000.npz      model.npz.progress.yml
model.iter10000.npz   model.iter35000.npz  model.iter60000.npz  model.iter90000.npz      model.npz.yml
model.iter100000.npz  model.iter40000.npz  model.iter65000.npz  model.iter95000.npz      s2s.my-tg.para.log1
model.iter15000.npz   model.iter45000.npz  model.iter70000.npz  model.npz                train.log
model.iter20000.npz   model.iter5000.npz   model.iter75000.npz  model.npz.decoder.yml    valid.log
model.iter25000.npz   model.iter50000.npz  model.iter80000.npz  model.npz.optimizer.npz
root@d7ccd8169efe:/home/ye/exp/mysent/model.seq2seq.para1#
```

check the validation scores ...  

```
  1 [2022-12-14 23:48:20] [valid] Ep. 11 : Up. 5000 : cross-entropy : 3.40338 : new best
  2 [2022-12-14 23:48:27] [valid] Ep. 11 : Up. 5000 : perplexity : 1.17534 : new best
  3 [2022-12-14 23:48:29] [valid] First sentence's tokens as scored:
  4 [2022-12-14 23:48:29] [valid] DefaultVocab keeps original segments for scoring
  5 [2022-12-14 23:48:29] [valid]   Hyp:
  6 [2022-12-14 23:48:29] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O N N N E B O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O N N N E B O O O O O O O O O O O O O O O O N N N E
  7 [2022-12-14 23:48:48] [valid] Ep. 11 : Up. 5000 : bleu : 70.682 : new best
  8 [2022-12-15 00:14:55] [valid] Ep. 22 : Up. 10000 : cross-entropy : 2.40332 : new best
  9 [2022-12-15 00:15:02] [valid] Ep. 22 : Up. 10000 : perplexity : 1.12085 : new best
 10 [2022-12-15 00:15:22] [valid] Ep. 22 : Up. 10000 : bleu : 81.6246 : new best
 11 [2022-12-15 00:41:32] [valid] Ep. 33 : Up. 15000 : cross-entropy : 1.94765 : new best
 12 [2022-12-15 00:41:39] [valid] Ep. 33 : Up. 15000 : perplexity : 1.09687 : new best
 13 [2022-12-15 00:41:58] [valid] Ep. 33 : Up. 15000 : bleu : 71.8415 : stalled 1 times (last best: 81.6246)
 14 [2022-12-15 01:08:09] [valid] Ep. 44 : Up. 20000 : cross-entropy : 1.87281 : new best
 15 [2022-12-15 01:08:16] [valid] Ep. 44 : Up. 20000 : perplexity : 1.09298 : new best
 16 [2022-12-15 01:08:33] [valid] Ep. 44 : Up. 20000 : bleu : 78.3936 : stalled 2 times (last best: 81.6246)
 17 [2022-12-15 01:34:41] [valid] Ep. 54 : Up. 25000 : cross-entropy : 2.64215 : stalled 1 times (last best: 1.87281)
 18 [2022-12-15 01:34:48] [valid] Ep. 54 : Up. 25000 : perplexity : 1.13363 : stalled 1 times (last best: 1.09298)
 19 [2022-12-15 01:35:05] [valid] Ep. 54 : Up. 25000 : bleu : 85.0342 : new best
 20 [2022-12-15 02:01:09] [valid] Ep. 65 : Up. 30000 : cross-entropy : 1.75544 : new best
 21 [2022-12-15 02:01:17] [valid] Ep. 65 : Up. 30000 : perplexity : 1.0869 : new best
 22 [2022-12-15 02:01:33] [valid] Ep. 65 : Up. 30000 : bleu : 88.5089 : new best
 23 [2022-12-15 02:27:37] [valid] Ep. 76 : Up. 35000 : cross-entropy : 1.46053 : new best
 24 [2022-12-15 02:27:44] [valid] Ep. 76 : Up. 35000 : perplexity : 1.07179 : new best
 25 [2022-12-15 02:27:59] [valid] Ep. 76 : Up. 35000 : bleu : 88.1811 : stalled 1 times (last best: 88.5089)
 26 [2022-12-15 02:54:00] [valid] Ep. 87 : Up. 40000 : cross-entropy : 6.8014 : stalled 1 times (last best: 1.46053)
 27 [2022-12-15 02:54:07] [valid] Ep. 87 : Up. 40000 : perplexity : 1.38108 : stalled 1 times (last best: 1.07179)
 28 [2022-12-15 02:54:23] [valid] Ep. 87 : Up. 40000 : bleu : 76.9431 : stalled 2 times (last best: 88.5089)
  29 [2022-12-15 03:20:29] [valid] Ep. 98 : Up. 45000 : cross-entropy : 1.97473 : stalled 2 times (last best: 1.46053)
 30 [2022-12-15 03:20:37] [valid] Ep. 98 : Up. 45000 : perplexity : 1.09828 : stalled 2 times (last best: 1.07179)
 31 [2022-12-15 03:20:52] [valid] Ep. 98 : Up. 45000 : bleu : 88.5734 : new best
 32 [2022-12-15 03:46:57] [valid] Ep. 108 : Up. 50000 : cross-entropy : 1.44147 : new best
 33 [2022-12-15 03:47:04] [valid] Ep. 108 : Up. 50000 : perplexity : 1.07082 : new best
 34 [2022-12-15 03:47:18] [valid] Ep. 108 : Up. 50000 : bleu : 88.8615 : new best
 35 [2022-12-15 04:13:23] [valid] Ep. 119 : Up. 55000 : cross-entropy : 1.4456 : stalled 1 times (last best: 1.44147)
 36 [2022-12-15 04:13:30] [valid] Ep. 119 : Up. 55000 : perplexity : 1.07103 : stalled 1 times (last best: 1.07082)
 37 [2022-12-15 04:13:44] [valid] Ep. 119 : Up. 55000 : bleu : 88.892 : new best
 38 [2022-12-15 04:39:44] [valid] Ep. 130 : Up. 60000 : cross-entropy : 1.47262 : stalled 2 times (last best: 1.44147)
 39 [2022-12-15 04:39:52] [valid] Ep. 130 : Up. 60000 : perplexity : 1.07241 : stalled 2 times (last best: 1.07082)
 40 [2022-12-15 04:40:05] [valid] Ep. 130 : Up. 60000 : bleu : 89.4978 : new best
 41 [2022-12-15 05:06:10] [valid] Ep. 141 : Up. 65000 : cross-entropy : 1.48691 : stalled 3 times (last best: 1.44147)
 42 [2022-12-15 05:06:17] [valid] Ep. 141 : Up. 65000 : perplexity : 1.07314 : stalled 3 times (last best: 1.07082)
 43 [2022-12-15 05:06:31] [valid] Ep. 141 : Up. 65000 : bleu : 91.2848 : new best
 44 [2022-12-15 05:32:31] [valid] Ep. 152 : Up. 70000 : cross-entropy : 1.51153 : stalled 4 times (last best: 1.44147)
 45 [2022-12-15 05:32:38] [valid] Ep. 152 : Up. 70000 : perplexity : 1.07439 : stalled 4 times (last best: 1.07082)
 46 [2022-12-15 05:32:52] [valid] Ep. 152 : Up. 70000 : bleu : 91.7101 : new best
 47 [2022-12-15 05:58:55] [valid] Ep. 162 : Up. 75000 : cross-entropy : 1.55779 : stalled 5 times (last best: 1.44147)
 48 [2022-12-15 05:59:03] [valid] Ep. 162 : Up. 75000 : perplexity : 1.07675 : stalled 5 times (last best: 1.07082)
 49 [2022-12-15 05:59:16] [valid] Ep. 162 : Up. 75000 : bleu : 90.3265 : stalled 1 times (last best: 91.7101)
 50 [2022-12-15 06:25:15] [valid] Ep. 173 : Up. 80000 : cross-entropy : 1.60584 : stalled 6 times (last best: 1.44147)
 51 [2022-12-15 06:25:22] [valid] Ep. 173 : Up. 80000 : perplexity : 1.07921 : stalled 6 times (last best: 1.07082)
 52 [2022-12-15 06:25:36] [valid] Ep. 173 : Up. 80000 : bleu : 90.3494 : stalled 2 times (last best: 91.7101)
 53 [2022-12-15 06:51:41] [valid] Ep. 184 : Up. 85000 : cross-entropy : 1.65398 : stalled 7 times (last best: 1.44147)
 54 [2022-12-15 06:51:48] [valid] Ep. 184 : Up. 85000 : perplexity : 1.08168 : stalled 7 times (last best: 1.07082)
 55 [2022-12-15 06:52:02] [valid] Ep. 184 : Up. 85000 : bleu : 91.0552 : stalled 3 times (last best: 91.7101)
 56 [2022-12-15 07:18:06] [valid] Ep. 195 : Up. 90000 : cross-entropy : 1.67899 : stalled 8 times (last best: 1.44147)
 57 [2022-12-15 07:18:13] [valid] Ep. 195 : Up. 90000 : perplexity : 1.08297 : stalled 8 times (last best: 1.07082)
  58 [2022-12-15 07:18:27] [valid] Ep. 195 : Up. 90000 : bleu : 91.0288 : stalled 4 times (last best: 91.7101)
 59 [2022-12-15 07:44:29] [valid] Ep. 205 : Up. 95000 : cross-entropy : 1.7204 : stalled 9 times (last best: 1.44147)
 60 [2022-12-15 07:44:37] [valid] Ep. 205 : Up. 95000 : perplexity : 1.0851 : stalled 9 times (last best: 1.07082)
 61 [2022-12-15 07:44:50] [valid] Ep. 205 : Up. 95000 : bleu : 91.5024 : stalled 5 times (last best: 91.7101)
 62 [2022-12-15 08:10:49] [valid] Ep. 216 : Up. 100000 : cross-entropy : 1.75694 : stalled 10 times (last best: 1.44147)
 63 [2022-12-15 08:10:56] [valid] Ep. 216 : Up. 100000 : perplexity : 1.08698 : stalled 10 times (last best: 1.07082)
 64 [2022-12-15 08:11:10] [valid] Ep. 216 : Up. 100000 : bleu : 91.7906 : new best
```

## Training Transformr Model for Sent+Paragraph Dataset

check the shell script ...  

```bash
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

mkdir model.transformer.para1;

marian \
    --model model.transformer.para1/model.npz --type transformer \
    --train-sets data-para/train.my data-para/train.tg \
    --max-length 200 \
    --vocabs data-para/vocab/vocab.my.yml data-para/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-para/valid.my data-para/valid.tg \
    --valid-translation-output model.transformer.para1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 16 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.para1/train.log --valid-log model.transformer.para1/valid.log \
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
    --dump-config > model.transformer.para1/config.yml

time marian -c model.transformer.para1/config.yml  2>&1 | tee transformer.para1.log
```

start training ...  

```
[2022-12-15 15:13:45] Synced seed 1111
[2022-12-15 15:13:45] [data] Loading vocabulary from JSON/Yaml file data-para/vocab/vocab.my.yml
[2022-12-15 15:13:45] [data] Setting vocabulary size for input 0 to 46,105
[2022-12-15 15:13:45] [data] Loading vocabulary from JSON/Yaml file data-para/vocab/vocab.tg.yml
[2022-12-15 15:13:45] [data] Setting vocabulary size for input 1 to 6
[2022-12-15 15:13:45] [batching] Collecting statistics for batch fitting with step size 10
[2022-12-15 15:13:45] Error: Curand error 203 - /temp/marian/src/tensors/rand.cpp:74: curandCreateGenerator(&generator_, CURAND_RNG_PSEUDO_DEFAULT)
[2022-12-15 15:13:45] Error: Aborted from marian::CurandRandomGenerator::CurandRandomGenerator(size_t, marian::DeviceId) in /temp/marian/src/tensors/rand.cpp:74

[CALL STACK]
[0x56178b94d050]    marian::CurandRandomGenerator::  CurandRandomGenerator  (unsigned long,  marian::DeviceId) + 0x750
[0x56178b94d689]    marian::  createRandomGenerator  (unsigned long,  marian::DeviceId) + 0x69
[0x56178b947f20]    marian::  BackendByDeviceId  (marian::DeviceId,  unsigned long) + 0xa0
[0x56178b437220]    marian::ExpressionGraph::  setDevice  (marian::DeviceId,  std::shared_ptr<marian::Device>) + 0x80
[0x56178b730cd5]    marian::GraphGroup::  initGraphsAndOpts  ()        + 0x1e5
[0x56178b7321f8]    marian::GraphGroup::  GraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x548
[0x56178b710773]    marian::SyncGraphGroup::  SyncGraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x83
[0x56178b2698ab]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x1c2b
[0x56178b197347]    mainTrainer  (int,  char**)                        + 0x147
[0x7fd5b7dd5d90]                                                       + 0x29d90
[0x7fd5b7dd5e40]    __libc_start_main                                  + 0x80
[0x56178b190995]    _start                                             + 0x25


real    0m7.837s
user    0m0.193s
sys     0m0.057s
root@d7ccd8169efe:/home/ye/exp/mysent#
```

got error ... and thus, logout and then train again ...  

```
root@756efe2086e0:/home/ye/exp/mysent# ./transformer.para1.sh
...
...
...
[2022-12-15 15:18:50] [comm] NCCLCommunicators constructed successfully
[2022-12-15 15:18:50] [training] Using 1 GPUs
[2022-12-15 15:18:50] [logits] Applying loss function for 1 factor(s)
[2022-12-15 15:18:50] [memory] Reserving 146 MB, device gpu0
[2022-12-15 15:18:51] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-15 15:18:51] [memory] Reserving 146 MB, device gpu0
[2022-12-15 15:18:52] [batching] Done. Typical MB size is 2,882 target words
[2022-12-15 15:18:52] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-12-15 15:18:52] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-15 15:18:52] [comm] Using global sharding
[2022-12-15 15:18:52] [comm] NCCLCommunicators constructed successfully
[2022-12-15 15:18:52] [training] Using 1 GPUs
[2022-12-15 15:18:52] Training started
[2022-12-15 15:18:52] [data] Shuffling data
[2022-12-15 15:18:52] [data] Done reading 47,002 sentences
[2022-12-15 15:18:52] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 15:18:52] [training] Batches are processed as 1 process(es) x 1 devices/process
[2022-12-15 15:18:52] [memory] Reserving 146 MB, device gpu0
[2022-12-15 15:18:52] [memory] Reserving 146 MB, device gpu0
[2022-12-15 15:18:52] Parameter type float32, optimization type float32, casting types false
[2022-12-15 15:18:52] Allocating memory for general optimizer shards
[2022-12-15 15:18:52] [memory] Reserving 146 MB, device gpu0
[2022-12-15 15:18:52] Allocating memory for Adam-specific shards
[2022-12-15 15:18:52] [memory] Reserving 292 MB, device gpu0
[2022-12-15 15:18:59] Seen 46,972 samples
[2022-12-15 15:18:59] Starting data epoch 2 in logical epoch 2
[2022-12-15 15:18:59] [data] Shuffling data
[2022-12-15 15:18:59] [data] Done reading 47,002 sentences
[2022-12-15 15:18:59] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 15:19:02] Ep. 2 : Up. 500 : Sen. 20,430 : Cost 0.78880912 * 1,256,206 @ 2,707 after 1,256,206 : Time 9.80s : 128193.45 words/s : gNorm 2.0274 : L.r. 3.0000e-04
...
...
...
[2022-12-15 15:51:51] Starting data epoch 243 in logical epoch 243
[2022-12-15 15:51:51] [data] Shuffling data
[2022-12-15 15:51:51] [data] Done reading 47,002 sentences
[2022-12-15 15:51:51] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 15:51:58] Seen 46,972 samples
[2022-12-15 15:51:58] Starting data epoch 244 in logical epoch 244
[2022-12-15 15:51:58] [data] Shuffling data
[2022-12-15 15:51:58] [data] Done reading 47,002 sentences
[2022-12-15 15:51:58] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 15:51:59] Ep. 244 : Up. 84500 : Sen. 4,823 : Cost 0.46749362 * 1,261,481 @ 2,203 after 212,384,120 : Time 9.58s : 131618.29 words/s : gNorm 0.8245 : L.r. 1.3054e-04
[2022-12-15 15:52:05] Seen 46,972 samples
[2022-12-15 15:52:05] Starting data epoch 245 in logical epoch 245
[2022-12-15 15:52:05] [data] Shuffling data
[2022-12-15 15:52:05] [data] Done reading 47,002 sentences
[2022-12-15 15:52:05] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 15:52:08] Ep. 245 : Up. 85000 : Sen. 25,565 : Cost 0.46630269 * 1,253,594 @ 2,742 after 213,637,714 : Time 9.43s : 132866.58 words/s : gNorm 0.8028 : L.r. 1.3016e-04
[2022-12-15 15:52:08] Saving model weights and runtime parameters to model.transformer.para1/model.iter85000.npz
[2022-12-15 15:52:08] Saving model weights and runtime parameters to model.transformer.para1/model.npz
[2022-12-15 15:52:10] Saving Adam parameters
[2022-12-15 15:52:10] [training] Saving training checkpoint to model.transformer.para1/model.npz and model.transformer.para1/model.npz.optimizer.npz
[2022-12-15 15:52:14] [valid] Ep. 245 : Up. 85000 : cross-entropy : 2.72421 : new best
[2022-12-15 15:52:15] [valid] Ep. 245 : Up. 85000 : perplexity : 1.13805 : new best
[2022-12-15 15:52:30] [valid] Ep. 245 : Up. 85000 : bleu : 76.0898 : stalled 16 times (last best: 80.883)
[2022-12-15 15:52:33] Seen 46,972 samples
[2022-12-15 15:52:33] Starting data epoch 246 in logical epoch 246
[2022-12-15 15:52:33] [data] Shuffling data
[2022-12-15 15:52:33] [data] Done reading 47,002 sentences
[2022-12-15 15:52:33] [data] Done shuffling 47,002 sentences to temp files
...
...
...
[2022-12-15 16:11:11] Seen 46,972 samples
[2022-12-15 16:11:11] Starting data epoch 388 in logical epoch 388
[2022-12-15 16:11:11] [data] Shuffling data
[2022-12-15 16:11:11] [data] Done reading 47,002 sentences
[2022-12-15 16:11:11] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 16:11:11] Ep. 388 : Up. 134500 : Sen. 895 : Cost 0.46053261 * 1,256,463 @ 2,443 after 338,112,857 : Time 9.54s : 131676.56 words/s : gNorm 0.6599 : L.r. 1.0347e-04
[2022-12-15 16:11:17] Seen 46,972 samples
[2022-12-15 16:11:17] Starting data epoch 389 in logical epoch 389
[2022-12-15 16:11:17] [data] Shuffling data
[2022-12-15 16:11:17] [data] Done reading 47,002 sentences
[2022-12-15 16:11:17] [data] Done shuffling 47,002 sentences to temp files
[2022-12-15 16:11:20] Ep. 389 : Up. 135000 : Sen. 21,103 : Cost 0.45912629 * 1,256,251 @ 2,397 after 339,369,108 : Time 9.42s : 133381.78 words/s : gNorm 0.7578 : L.r. 1.0328e-04
[2022-12-15 16:11:20] Saving model weights and runtime parameters to model.transformer.para1/model.iter135000.npz
[2022-12-15 16:11:21] Saving model weights and runtime parameters to model.transformer.para1/model.npz
[2022-12-15 16:11:22] Saving Adam parameters
[2022-12-15 16:11:22] [training] Saving training checkpoint to model.transformer.para1/model.npz and model.transformer.para1/model.npz.optimizer.npz
[2022-12-15 16:11:26] [valid] Ep. 389 : Up. 135000 : cross-entropy : 2.77554 : stalled 10 times (last best: 2.72421)
[2022-12-15 16:11:27] [valid] Ep. 389 : Up. 135000 : perplexity : 1.14083 : stalled 10 times (last best: 1.13805)
[2022-12-15 16:11:40] [valid] Ep. 389 : Up. 135000 : bleu : 86.2612 : stalled 3 times (last best: 86.8078)
[2022-12-15 16:11:40] Training finished
[2022-12-15 16:11:40] Saving model weights and runtime parameters to model.transformer.para1/model.npz
[2022-12-15 16:11:41] Saving Adam parameters
[2022-12-15 16:11:41] [training] Saving training checkpoint to model.transformer.para1/model.npz and model.transformer.para1/model.npz.optimizer.npz

real    52m55.054s
user    53m42.015s
sys     1m29.806s
root@756efe2086e0:/home/ye/exp/mysent#
```

checked the models ...  

```
root@756efe2086e0:/home/ye/exp/mysent/model.transformer.para1# ls
config.yml            model.iter130000.npz  model.iter45000.npz  model.iter80000.npz      model.npz.yml
model.iter10000.npz   model.iter135000.npz  model.iter5000.npz   model.iter85000.npz      train.log
model.iter100000.npz  model.iter15000.npz   model.iter50000.npz  model.iter90000.npz      valid.log
model.iter105000.npz  model.iter20000.npz   model.iter55000.npz  model.iter95000.npz      valid.my-tg.output
model.iter110000.npz  model.iter25000.npz   model.iter60000.npz  model.npz
model.iter115000.npz  model.iter30000.npz   model.iter65000.npz  model.npz.decoder.yml
model.iter120000.npz  model.iter35000.npz   model.iter70000.npz  model.npz.optimizer.npz
model.iter125000.npz  model.iter40000.npz   model.iter75000.npz  model.npz.progress.yml
root@756efe2086e0:/home/ye/exp/mysent/model.transformer.para1#
```

check/learn the validation scores ...  

```
  1 [2022-12-15 15:20:29] [valid] Ep. 15 : Up. 5000 : cross-entropy : 4.96333 : new best
  2 [2022-12-15 15:20:29] [valid] Ep. 15 : Up. 5000 : perplexity : 1.26568 : new best
  3 [2022-12-15 15:20:30] [valid] First sentence's tokens as scored:
  4 [2022-12-15 15:20:30] [valid] DefaultVocab keeps original segments for scoring
  5 [2022-12-15 15:20:30] [valid]   Hyp: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O     O O O O O O O O O O O O O O O N N N E
  6 [2022-12-15 15:20:30] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N     E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O     O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O     O N N N E
  7 [2022-12-15 15:20:52] [valid] Ep. 15 : Up. 5000 : bleu : 80.883 : new best
  8 [2022-12-15 15:22:32] [valid] Ep. 29 : Up. 10000 : cross-entropy : 3.60183 : new best
  9 [2022-12-15 15:22:33] [valid] Ep. 29 : Up. 10000 : perplexity : 1.18647 : new best
 10 [2022-12-15 15:22:55] [valid] Ep. 29 : Up. 10000 : bleu : 58.3665 : stalled 1 times (last best: 80.883)
 11 [2022-12-15 15:24:35] [valid] Ep. 44 : Up. 15000 : cross-entropy : 3.22426 : new best
 12 [2022-12-15 15:24:36] [valid] Ep. 44 : Up. 15000 : perplexity : 1.16539 : new best
 13 [2022-12-15 15:24:57] [valid] Ep. 44 : Up. 15000 : bleu : 61.4487 : stalled 2 times (last best: 80.883)
 14 [2022-12-15 15:26:38] [valid] Ep. 58 : Up. 20000 : cross-entropy : 3.12394 : new best
 15 [2022-12-15 15:26:38] [valid] Ep. 58 : Up. 20000 : perplexity : 1.15986 : new best
 16 [2022-12-15 15:26:56] [valid] Ep. 58 : Up. 20000 : bleu : 77.1502 : stalled 3 times (last best: 80.883)
 17 [2022-12-15 15:28:37] [valid] Ep. 72 : Up. 25000 : cross-entropy : 2.99776 : new best
 18 [2022-12-15 15:28:38] [valid] Ep. 72 : Up. 25000 : perplexity : 1.15293 : new best
 19 [2022-12-15 15:28:56] [valid] Ep. 72 : Up. 25000 : bleu : 71.1581 : stalled 4 times (last best: 80.883)
 20 [2022-12-15 15:30:36] [valid] Ep. 87 : Up. 30000 : cross-entropy : 2.89711 : new best
 21 [2022-12-15 15:30:37] [valid] Ep. 87 : Up. 30000 : perplexity : 1.14743 : new best
 22 [2022-12-15 15:30:55] [valid] Ep. 87 : Up. 30000 : bleu : 62.7227 : stalled 5 times (last best: 80.883)
 23 [2022-12-15 15:32:36] [valid] Ep. 101 : Up. 35000 : cross-entropy : 2.83347 : new best
 24 [2022-12-15 15:32:36] [valid] Ep. 101 : Up. 35000 : perplexity : 1.14397 : new best
 25 [2022-12-15 15:32:54] [valid] Ep. 101 : Up. 35000 : bleu : 60.2647 : stalled 6 times (last best: 80.883)
 26 [2022-12-15 15:34:35] [valid] Ep. 116 : Up. 40000 : cross-entropy : 2.80151 : new best
  27 [2022-12-15 15:34:36] [valid] Ep. 116 : Up. 40000 : perplexity : 1.14224 : new best
 28 [2022-12-15 15:34:54] [valid] Ep. 116 : Up. 40000 : bleu : 59.4293 : stalled 7 times (last best: 80.883)
 29 [2022-12-15 15:36:34] [valid] Ep. 130 : Up. 45000 : cross-entropy : 2.79327 : new best
 30 [2022-12-15 15:36:35] [valid] Ep. 130 : Up. 45000 : perplexity : 1.14179 : new best
 31 [2022-12-15 15:36:52] [valid] Ep. 130 : Up. 45000 : bleu : 63.1524 : stalled 8 times (last best: 80.883)
 32 [2022-12-15 15:38:33] [valid] Ep. 144 : Up. 50000 : cross-entropy : 2.7829 : new best
 33 [2022-12-15 15:38:34] [valid] Ep. 144 : Up. 50000 : perplexity : 1.14123 : new best
 34 [2022-12-15 15:38:50] [valid] Ep. 144 : Up. 50000 : bleu : 70.7739 : stalled 9 times (last best: 80.883)
 35 [2022-12-15 15:40:31] [valid] Ep. 159 : Up. 55000 : cross-entropy : 2.75332 : new best
 36 [2022-12-15 15:40:31] [valid] Ep. 159 : Up. 55000 : perplexity : 1.13963 : new best
 37 [2022-12-15 15:40:48] [valid] Ep. 159 : Up. 55000 : bleu : 72.2076 : stalled 10 times (last best: 80.883)
 38 [2022-12-15 15:42:28] [valid] Ep. 173 : Up. 60000 : cross-entropy : 2.74219 : new best
 39 [2022-12-15 15:42:29] [valid] Ep. 173 : Up. 60000 : perplexity : 1.13903 : new best
 40 [2022-12-15 15:42:45] [valid] Ep. 173 : Up. 60000 : bleu : 74.8474 : stalled 11 times (last best: 80.883)
 41 [2022-12-15 15:44:26] [valid] Ep. 188 : Up. 65000 : cross-entropy : 2.73809 : new best
 42 [2022-12-15 15:44:26] [valid] Ep. 188 : Up. 65000 : perplexity : 1.1388 : new best
 43 [2022-12-15 15:44:42] [valid] Ep. 188 : Up. 65000 : bleu : 74.8641 : stalled 12 times (last best: 80.883)
 44 [2022-12-15 15:46:23] [valid] Ep. 202 : Up. 70000 : cross-entropy : 2.73569 : new best
 45 [2022-12-15 15:46:24] [valid] Ep. 202 : Up. 70000 : perplexity : 1.13868 : new best
 46 [2022-12-15 15:46:40] [valid] Ep. 202 : Up. 70000 : bleu : 74.8497 : stalled 13 times (last best: 80.883)
 47 [2022-12-15 15:48:20] [valid] Ep. 216 : Up. 75000 : cross-entropy : 2.72687 : new best
 48 [2022-12-15 15:48:21] [valid] Ep. 216 : Up. 75000 : perplexity : 1.1382 : new best
 49 [2022-12-15 15:48:37] [valid] Ep. 216 : Up. 75000 : bleu : 77.1043 : stalled 14 times (last best: 80.883)
 50 [2022-12-15 15:50:17] [valid] Ep. 231 : Up. 80000 : cross-entropy : 2.72513 : new best
 51 [2022-12-15 15:50:18] [valid] Ep. 231 : Up. 80000 : perplexity : 1.1381 : new best
 52 [2022-12-15 15:50:33] [valid] Ep. 231 : Up. 80000 : bleu : 77.395 : stalled 15 times (last best: 80.883)
 53 [2022-12-15 15:52:14] [valid] Ep. 245 : Up. 85000 : cross-entropy : 2.72421 : new best
 54 [2022-12-15 15:52:15] [valid] Ep. 245 : Up. 85000 : perplexity : 1.13805 : new best
 55 [2022-12-15 15:52:30] [valid] Ep. 245 : Up. 85000 : bleu : 76.0898 : stalled 16 times (last best: 80.883)
  56 [2022-12-15 15:54:11] [valid] Ep. 259 : Up. 90000 : cross-entropy : 2.72782 : stalled 1 times (last best: 2.72421)
 57 [2022-12-15 15:54:12] [valid] Ep. 259 : Up. 90000 : perplexity : 1.13825 : stalled 1 times (last best: 1.13805)
 58 [2022-12-15 15:54:26] [valid] Ep. 259 : Up. 90000 : bleu : 80.0508 : stalled 17 times (last best: 80.883)
 59 [2022-12-15 15:56:07] [valid] Ep. 274 : Up. 95000 : cross-entropy : 2.73926 : stalled 2 times (last best: 2.72421)
 60 [2022-12-15 15:56:08] [valid] Ep. 274 : Up. 95000 : perplexity : 1.13887 : stalled 2 times (last best: 1.13805)
 61 [2022-12-15 15:56:22] [valid] Ep. 274 : Up. 95000 : bleu : 79.8181 : stalled 18 times (last best: 80.883)
 62 [2022-12-15 15:58:03] [valid] Ep. 288 : Up. 100000 : cross-entropy : 2.7442 : stalled 3 times (last best: 2.72421)
 63 [2022-12-15 15:58:04] [valid] Ep. 288 : Up. 100000 : perplexity : 1.13914 : stalled 3 times (last best: 1.13805)
 64 [2022-12-15 15:58:18] [valid] Ep. 288 : Up. 100000 : bleu : 80.0516 : stalled 19 times (last best: 80.883)
 65 [2022-12-15 15:59:58] [valid] Ep. 303 : Up. 105000 : cross-entropy : 2.74089 : stalled 4 times (last best: 2.72421)
 66 [2022-12-15 15:59:59] [valid] Ep. 303 : Up. 105000 : perplexity : 1.13896 : stalled 4 times (last best: 1.13805)
 67 [2022-12-15 16:00:13] [valid] Ep. 303 : Up. 105000 : bleu : 82.1205 : new best
 68 [2022-12-15 16:01:54] [valid] Ep. 317 : Up. 110000 : cross-entropy : 2.75681 : stalled 5 times (last best: 2.72421)
 69 [2022-12-15 16:01:54] [valid] Ep. 317 : Up. 110000 : perplexity : 1.13982 : stalled 5 times (last best: 1.13805)
 70 [2022-12-15 16:02:07] [valid] Ep. 317 : Up. 110000 : bleu : 85.3491 : new best
 71 [2022-12-15 16:03:48] [valid] Ep. 331 : Up. 115000 : cross-entropy : 2.75465 : stalled 6 times (last best: 2.72421)
 72 [2022-12-15 16:03:49] [valid] Ep. 331 : Up. 115000 : perplexity : 1.1397 : stalled 6 times (last best: 1.13805)
 73 [2022-12-15 16:04:02] [valid] Ep. 331 : Up. 115000 : bleu : 86.5717 : new best
 74 [2022-12-15 16:05:43] [valid] Ep. 346 : Up. 120000 : cross-entropy : 2.75603 : stalled 7 times (last best: 2.72421)
 75 [2022-12-15 16:05:44] [valid] Ep. 346 : Up. 120000 : perplexity : 1.13977 : stalled 7 times (last best: 1.13805)
 76 [2022-12-15 16:05:57] [valid] Ep. 346 : Up. 120000 : bleu : 86.8078 : new best
 77 [2022-12-15 16:07:38] [valid] Ep. 360 : Up. 125000 : cross-entropy : 2.76371 : stalled 8 times (last best: 2.72421)
 78 [2022-12-15 16:07:39] [valid] Ep. 360 : Up. 125000 : perplexity : 1.14019 : stalled 8 times (last best: 1.13805)
 79 [2022-12-15 16:07:52] [valid] Ep. 360 : Up. 125000 : bleu : 84.1684 : stalled 1 times (last best: 86.8078)
 80 [2022-12-15 16:09:32] [valid] Ep. 375 : Up. 130000 : cross-entropy : 2.76916 : stalled 9 times (last best: 2.72421)
 81 [2022-12-15 16:09:33] [valid] Ep. 375 : Up. 130000 : perplexity : 1.14049 : stalled 9 times (last best: 1.13805)
 82 [2022-12-15 16:09:46] [valid] Ep. 375 : Up. 130000 : bleu : 85.0151 : stalled 2 times (last best: 86.8078)
 83 [2022-12-15 16:11:26] [valid] Ep. 389 : Up. 135000 : cross-entropy : 2.77554 : stalled 10 times (last best: 2.72421)
 84 [2022-12-15 16:11:27] [valid] Ep. 389 : Up. 135000 : perplexity : 1.14083 : stalled 10 times (last best: 1.13805)
 85 [2022-12-15 16:11:40] [valid] Ep. 389 : Up. 135000 : bleu : 86.2612 : stalled 3 times (last best: 86.8078)
```

## Testing  

check testing shell script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for Transformer and Seq2Seq modeling
## this script is wrote for cross validation with the updated test-data by Thura Aung
## Last updated: 25 Oct 2022

data_path="/home/ye/exp/mysent/new-test-data";
hyp_path="/home/ye/exp/mysent/results4ws1";
src="my"; tgt="tg";

# Testing for NMT models trained with sentence-only
for model_path in {model.transformer.sent1,model.seq2seq.sent1}
do

# Evaluation with Sentence-Only Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-sent/vocab.${src}.yml ${data_path}/vocab-sent/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.sent.${tgt} < ${data_path}/test.sent.${src};
   echo "Evaluation on ${model_path}, with sentence-only test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.sent.${tgt} \
< ${hyp_path}/hyp.${model_path}.sent.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

# Evaluation with Sentence+Parallel Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-sent/vocab.${src}.yml ${data_path}/vocab-sent/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.para.${tgt} < ${data_path}/test.para.${src};
   echo "Evaluation on ${model_path}, with sentence+parallel test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.para.${tgt} \
< ${hyp_path}/hyp.${model_path}.para.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

done

# Testing for NMT models that trained with sentence+parallel data
for model_path in {model.transformer.para1,model.seq2seq.para1}
do

# Evaluation with Sentence-Only Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-para/vocab.${src}.yml ${data_path}/vocab-para/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.sent.${tgt} < ${data_path}/test.sent.${src};
   echo "Evaluation on ${model_path}, with sentence-only test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.sent.${tgt} \
< ${hyp_path}/hyp.${model_path}.sent.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

# Evaluation with Sentence+Parallel Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-para/vocab.${src}.yml ${data_path}/vocab-para/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.para.${tgt} < ${data_path}/test.para.${src};
   echo "Evaluation on ${model_path}, with sentence+parallel test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.para.${tgt} \
< ${hyp_path}/hyp.${model_path}.para.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

done
```

Backup the old results:  

```
root@756efe2086e0:/home/ye/exp/mysent# mkdir old-results
root@756efe2086e0:/home/ye/exp/mysent# mv results4ws1 ./old-results/
root@756efe2086e0:/home/ye/exp/mysent# cd old-results/results4ws1/
root@756efe2086e0:/home/ye/exp/mysent/old-results/results4ws1# ls
cross-evaluation-results.txt               hyp.model.seq2seq.sent1.para.tg      hyp.model.transformer.sent1.para.tg
cross-evaluation-results.with-2vocabs.txt  hyp.model.seq2seq.sent1.sent.tg      hyp.model.transformer.sent1.sent.tg
hyp.model.seq2seq.para1.para.tg            hyp.model.transformer.para1.para.tg
hyp.model.seq2seq.para1.sent.tg            hyp.model.transformer.para1.sent.tg
root@756efe2086e0:/home/ye/exp/mysent/old-results/results4ws1#
```

run testing ...  got error and I found that I have to update the test data ...  

```
root@5d94c7834a47:/home/ye/exp/mysent# mv new-test-data/ ./old-exp1-data/
root@5d94c7834a47:/home/ye/exp/mysent# mkdir new-test-data
root@5d94c7834a47:/home/ye/exp/mysent# cp ./data-sent/test.my ./new-test-data/test.sent.my
root@5d94c7834a47:/home/ye/exp/mysent# cp ./data-sent/test.tg ./new-test-data/test.sent.tg
root@5d94c7834a47:/home/ye/exp/mysent# cp ./data-para/test.my ./new-test-data/test.para.my
root@5d94c7834a47:/home/ye/exp/mysent# cp ./data-para/test.tg ./new-test-data/test.para.tg
root@5d94c7834a47:/home/ye/exp/mysent# cp -r ./data-sent/vocab/ ./new-test-data/vocab-sent
root@5d94c7834a47:/home/ye/exp/mysent# cp -r ./data-para/vocab/ ./new-test-data/vocab-para
```

and prepare the new result folder:  

```
root@5d94c7834a47:/home/ye/exp/mysent# mkdir results4ws1
```

run testing again ...  

```
root@5d94c7834a47:/home/ye/exp/mysent# time ./test4paper.sh
...
...
...
[2022-12-15 18:20:15] Best translation 5493 : B O O O O O N N N E B O O O O N N N E B O O O O N N N E
[2022-12-15 18:20:15] Best translation 5494 : B O O O O O O O O O O N N N E B O O O O O O O O O O O N N N E
[2022-12-15 18:20:15] Best translation 5495 : B O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:15] Best translation 5496 : B O N N N E
[2022-12-15 18:20:15] Best translation 5497 : B O N N N E
[2022-12-15 18:20:16] Best translation 5498 : B O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5499 : B O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5500 : B O O O O O O O O O O O N N N E B O N N N E B N N N E B O O N N N E B O O N N N E B O O N N N E B N N N E
[2022-12-15 18:20:16] Best translation 5501 : B O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5502 : B O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5503 : B N N N E
[2022-12-15 18:20:16] Best translation 5504 : B N N N E
[2022-12-15 18:20:16] Best translation 5505 : B O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5506 : B O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5507 : B O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5508 : B O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5509 : B O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5510 : B O O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Best translation 5511 : B O O O O O O O O O O O O O N N N E
[2022-12-15 18:20:16] Total time: 197.86422s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    16m11.619s
user    15m27.843s
sys     0m32.617s
root@5d94c7834a47:/home/ye/exp/mysent#
```

Results are as follows:  

```
Evaluation on model.transformer.sent1, with sentence-only test-data:
BLEU = 65.09, 99.8/99.8/99.8/99.7 (BP=0.652, ratio=0.701, hyp_len=44575, ref_len=63622)
Evaluation on model.transformer.sent1, with sentence+parallel test-data:
BLEU = 42.49, 95.9/94.8/93.7/92.4 (BP=0.451, ratio=0.557, hyp_len=53801, ref_len=96632)
Evaluation on model.seq2seq.sent1, with sentence-only test-data:
BLEU = 99.78, 99.8/99.8/99.8/99.8 (BP=1.000, ratio=1.001, hyp_len=63667, ref_len=63622)
Evaluation on model.seq2seq.sent1, with sentence+parallel test-data:
BLEU = 90.93, 93.9/92.4/90.9/89.3 (BP=0.992, ratio=0.992, hyp_len=95905, ref_len=96632)
Evaluation on model.transformer.para1, with sentence-only test-data:
BLEU = 95.67, 99.4/99.3/99.2/99.0 (BP=0.964, ratio=0.965, hyp_len=61371, ref_len=63622)
Evaluation on model.transformer.para1, with sentence+parallel test-data:
BLEU = 69.88, 97.0/96.2/95.3/94.4 (BP=0.730, ratio=0.761, hyp_len=73517, ref_len=96632)
Evaluation on model.seq2seq.para1, with sentence-only test-data:
BLEU = 99.38, 99.5/99.4/99.3/99.3 (BP=1.000, ratio=1.000, hyp_len=63609, ref_len=63622)
Evaluation on model.seq2seq.para1, with sentence+parallel test-data:
BLEU = 94.21, 97.4/96.8/96.1/95.5 (BP=0.977, ratio=0.977, hyp_len=94426, ref_len=96632)
```

## Testing with Using Big Vocab (i.e. sent+para) File

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for Transformer and Seq2Seq modeling
## this script is wrote for cross validation with the updated test-data by Thura Aung
## Important: for this time, I used only sent+para vocab file for all evaluation
## Important: for exploring the results defferences between using two vocab files and using big-common vocab file
## Last updated: 25 Oct 2022

data_path="/home/ye/exp/mysent/new-test-data";
hyp_path="/home/ye/exp/mysent/results4ws1";
src="my"; tgt="tg";

# Testing for NMT models trained with sentence-only
for model_path in {model.transformer.sent1,model.seq2seq.sent1,model.transformer.para1,model.seq2seq.para1}
do

# Evaluation with Sentence-Only Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-para/vocab.${src}.yml ${data_path}/vocab-para/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.sent.${tgt} < ${data_path}/test.sent.${src};
   echo "Evaluation on ${model_path}, with sentence-only test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.sent.${tgt} \
< ${hyp_path}/hyp.${model_path}.sent.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

# Evaluation with Sentence+Parallel Test Data
   marian-decoder -m ${model_path}/model.npz \
-v ${data_path}/vocab-para/vocab.${src}.yml ${data_path}/vocab-para/vocab.${tgt}.yml \
--devices 0 --output ${hyp_path}/hyp.${model_path}.para.${tgt} < ${data_path}/test.para.${src};
   echo "Evaluation on ${model_path}, with sentence+parallel test-data:" >> ${hyp_path}/cross-evaluation-results.txt;
   perl /home/ye/tool/multi-bleu.perl ${data_path}/test.para.${tgt} \
< ${hyp_path}/hyp.${model_path}.para.${tgt} >> ${hyp_path}/cross-evaluation-results.txt;

done
```

before running change the previous results filename:  

```
root@5d94c7834a47:/home/ye/exp/mysent/results4ws1# mv cross-evaluation-results.txt cross-evaluation-results.with-2vocabs.txt
```

start testing ...  

```
root@5d94c7834a47:/home/ye/exp/mysent# time ./test4paper-with-para-vocab.sh
...
...
...
[2022-12-15 19:07:14] Best translation 5493 : B O O O O O N N N E B O O O O N N N E B O O O O N N N E
[2022-12-15 19:07:14] Best translation 5494 : B O O O O O O O O O O N N N E B O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5495 : B O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5496 : B O N N N E
[2022-12-15 19:07:15] Best translation 5497 : B O N N N E
[2022-12-15 19:07:15] Best translation 5498 : B O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5499 : B O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5500 : B O O O O O O O O O O O N N N E B O N N N E B N N N E B O O N N N E B O O N N N E B O O N N N E B N N N E
[2022-12-15 19:07:15] Best translation 5501 : B O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5502 : B O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5503 : B N N N E
[2022-12-15 19:07:15] Best translation 5504 : B N N N E
[2022-12-15 19:07:15] Best translation 5505 : B O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5506 : B O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5507 : B O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5508 : B O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5509 : B O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5510 : B O O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Best translation 5511 : B O O O O O O O O O O O O O N N N E
[2022-12-15 19:07:15] Total time: 197.85991s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    16m10.365s
user    15m26.590s
sys     0m33.291s
root@5d94c7834a47:/home/ye/exp/mysent#
```

check the results with a big vocab (i.e. sent+para vocab file) ...  

```
root@5d94c7834a47:/home/ye/exp/mysent/results4ws1# cat cross-evaluation-results.txt
Evaluation on model.transformer.sent1, with sentence-only test-data:
BLEU = 64.52, 99.9/99.9/99.9/99.9 (BP=0.646, ratio=0.696, hyp_len=44273, ref_len=63622)
Evaluation on model.transformer.sent1, with sentence+parallel test-data:
BLEU = 42.08, 96.0/94.9/93.8/92.5 (BP=0.446, ratio=0.553, hyp_len=53482, ref_len=96632)
Evaluation on model.seq2seq.sent1, with sentence-only test-data:
BLEU = 99.79, 99.8/99.8/99.8/99.8 (BP=1.000, ratio=1.001, hyp_len=63662, ref_len=63622)
Evaluation on model.seq2seq.sent1, with sentence+parallel test-data:
BLEU = 90.92, 93.9/92.4/90.9/89.3 (BP=0.992, ratio=0.993, hyp_len=95909, ref_len=96632)
Evaluation on model.transformer.para1, with sentence-only test-data:
BLEU = 95.67, 99.4/99.3/99.2/99.0 (BP=0.964, ratio=0.965, hyp_len=61371, ref_len=63622)
Evaluation on model.transformer.para1, with sentence+parallel test-data:
BLEU = 69.88, 97.0/96.2/95.3/94.4 (BP=0.730, ratio=0.761, hyp_len=73517, ref_len=96632)
Evaluation on model.seq2seq.para1, with sentence-only test-data:
BLEU = 99.38, 99.5/99.4/99.3/99.3 (BP=1.000, ratio=1.000, hyp_len=63609, ref_len=63622)
Evaluation on model.seq2seq.para1, with sentence+parallel test-data:
BLEU = 94.21, 97.4/96.8/96.1/95.5 (BP=0.977, ratio=0.977, hyp_len=94426, ref_len=96632)
root@5d94c7834a47:/home/ye/exp/mysent/results4ws1#
```

## To Do

- make comparison between NMT and traditional ML approaches
- make comparison between using two vocab files (sent vocab, para vocab separately) and one big vocab file (i.e. sent+para vocab only)  
- update the paper with above NMT results

