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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
