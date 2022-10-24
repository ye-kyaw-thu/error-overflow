# sequence to Sequence Modeling for Myanmar Sentence Segmentation

## Prepare a Training Script

```bash
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
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
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
```

## Training and Got Error as Usual

```
[CALL STACK]
[0x55efa8ee47d7]    marian::io::InputFileStream::  InputFileStream  (std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>> const&) + 0xaf7
[0x55efa8f3a45f]    marian::data::CorpusBase::  CorpusBase  (std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>> const&,  std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>> const&,  std::shared_ptr<marian::Options>,  unsigned long) + 0xb9f
[0x55efa8f4f198]    marian::data::Corpus::  Corpus  (std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>>,  std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>,  unsigned long) + 0x78
[0x55efa9313395]    marian::CrossEntropyValidator::  CrossEntropyValidator  (std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>) + 0x185
[0x55efa9316785]    marian::  Validators  (std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>) + 0x845
[0x55efa8e2845f]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x17df
[0x55efa8d56347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f8b0b0eed90]                                                       + 0x29d90
[0x7f8b0b0eee40]    __libc_start_main                                  + 0x80
[0x55efa8d4f995]    _start                                             + 0x25


real    0m53.890s
user    0m51.347s
sys     0m1.942s
root@2328f1decde9:/home/ye/exp/mysent# ./seq2seq.sent1.sh
```

The error reason is as follows:  

```
[2022-10-24 09:52:32] Error: File '/home/ye/exp/mysent/data-sent/dev.my' does not exist
```

## Updating the Bash Script

```bash
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
```

## Retraining

For this time, successfully finished training seq2seq model as follows:  

```
root@2328f1decde9:/home/ye/exp/mysent# ./seq2seq.sent1.sh
...
...
...
[2022-10-24 19:17:53] Best translation 0 : B O O O O O O O O O N N N E
[2022-10-24 19:17:53] Best translation 1 : B O O O N N N E
[2022-10-24 19:17:53] Best translation 2 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 19:17:53] Best translation 3 : B O O O O O O O O O O O O O O O O N N N E
[2022-10-24 19:17:53] Best translation 4 : B O O O N N N E
[2022-10-24 19:17:53] Best translation 5 : B O O O O N N N E
[2022-10-24 19:17:53] Best translation 10 : B N N E
[2022-10-24 19:17:53] Best translation 20 : B O O O O N N N E
[2022-10-24 19:17:53] Best translation 40 : B O N N N E
[2022-10-24 19:17:53] Best translation 80 : B O O O O O O O O O O N N N E
[2022-10-24 19:17:53] Best translation 160 : B O O O O O O O O O O N N N E
[2022-10-24 19:17:54] Best translation 320 : B O O O O O O N N N E
[2022-10-24 19:17:54] Best translation 640 : B O O O O O O O O O N N N E
[2022-10-24 19:17:56] Best translation 1280 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 19:17:58] Total translation time: 5.49156s
[2022-10-24 19:17:58] [valid] Ep. 431 : Up. 140000 : bleu : 93.9267 : stalled 8 times (last best: 99.7262)
[2022-10-24 19:17:58] Training finished
[2022-10-24 19:17:58] Saving model weights and runtime parameters to model.seq2seq.sent1/model.npz
[2022-10-24 19:18:06] Saving Adam parameters
[2022-10-24 19:18:09] [training] Saving training checkpoint to model.seq2seq.sent1/model.npz and model.seq2seq.sent1/model.npz.optimizer.npz

real    542m50.953s
user    523m14.446s
sys     5m35.168s
```

## Check Validation Results

```
[2022-10-24 10:35:04] [valid] Ep. 16 : Up. 5000 : cross-entropy : 2.09086 : new best
[2022-10-24 10:35:08] [valid] Ep. 16 : Up. 5000 : perplexity : 1.15643 : new best
[2022-10-24 10:35:08] [valid] First sentence's tokens as scored:
[2022-10-24 10:35:08] [valid] DefaultVocab keeps original segments for scoring
[2022-10-24 10:35:08] [valid]   Hyp: B O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 10:35:08] [valid]   Ref: B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O >
[2022-10-24 10:35:15] [valid] Ep. 16 : Up. 5000 : bleu : 86.0347 : new best
[2022-10-24 10:54:27] [valid] Ep. 31 : Up. 10000 : cross-entropy : 0.935163 : new best
[2022-10-24 10:54:31] [valid] Ep. 31 : Up. 10000 : perplexity : 1.06716 : new best
[2022-10-24 10:54:37] [valid] Ep. 31 : Up. 10000 : bleu : 95.941 : new best
[2022-10-24 11:13:50] [valid] Ep. 47 : Up. 15000 : cross-entropy : 0.49526 : new best
[2022-10-24 11:13:53] [valid] Ep. 47 : Up. 15000 : perplexity : 1.03502 : new best
[2022-10-24 11:13:59] [valid] Ep. 47 : Up. 15000 : bleu : 98.5226 : new best
[2022-10-24 11:33:12] [valid] Ep. 62 : Up. 20000 : cross-entropy : 0.27442 : new best
[2022-10-24 11:33:15] [valid] Ep. 62 : Up. 20000 : perplexity : 1.01926 : new best
[2022-10-24 11:33:21] [valid] Ep. 62 : Up. 20000 : bleu : 99.1142 : new best
[2022-10-24 11:52:33] [valid] Ep. 77 : Up. 25000 : cross-entropy : 0.249116 : new best
[2022-10-24 11:52:36] [valid] Ep. 77 : Up. 25000 : perplexity : 1.01747 : new best
[2022-10-24 11:52:42] [valid] Ep. 77 : Up. 25000 : bleu : 99.3228 : new best
[2022-10-24 12:11:54] [valid] Ep. 93 : Up. 30000 : cross-entropy : 0.245955 : new best
[2022-10-24 12:11:57] [valid] Ep. 93 : Up. 30000 : perplexity : 1.01724 : new best
[2022-10-24 12:12:04] [valid] Ep. 93 : Up. 30000 : bleu : 99.3782 : new best
[2022-10-24 12:31:19] [valid] Ep. 108 : Up. 35000 : cross-entropy : 1.61564 : stalled 1 times (last best: 0.245955)
[2022-10-24 12:31:22] [valid] Ep. 108 : Up. 35000 : perplexity : 1.11885 : stalled 1 times (last best: 1.01724)
[2022-10-24 12:31:28] [valid] Ep. 108 : Up. 35000 : bleu : 90.0603 : stalled 1 times (last best: 99.3782)
[2022-10-24 12:50:36] [valid] Ep. 124 : Up. 40000 : cross-entropy : 0.53689 : stalled 2 times (last best: 0.245955)
[2022-10-24 12:50:39] [valid] Ep. 124 : Up. 40000 : perplexity : 1.03802 : stalled 2 times (last best: 1.01724)
[2022-10-24 12:50:46] [valid] Ep. 124 : Up. 40000 : bleu : 97.4693 : stalled 2 times (last best: 99.3782)
[2022-10-24 13:09:59] [valid] Ep. 139 : Up. 45000 : cross-entropy : 0.271084 : stalled 3 times (last best: 0.245955)
[2022-10-24 13:10:02] [valid] Ep. 139 : Up. 45000 : perplexity : 1.01902 : stalled 3 times (last best: 1.01724)
[2022-10-24 13:10:08] [valid] Ep. 139 : Up. 45000 : bleu : 99.2008 : stalled 3 times (last best: 99.3782)
[2022-10-24 13:29:22] [valid] Ep. 154 : Up. 50000 : cross-entropy : 0.230504 : new best
[2022-10-24 13:29:25] [valid] Ep. 154 : Up. 50000 : perplexity : 1.01615 : new best
[2022-10-24 13:29:32] [valid] Ep. 154 : Up. 50000 : bleu : 99.554 : new best
[2022-10-24 13:48:46] [valid] Ep. 170 : Up. 55000 : cross-entropy : 0.224514 : new best
[2022-10-24 13:48:49] [valid] Ep. 170 : Up. 55000 : perplexity : 1.01573 : new best
[2022-10-24 13:48:55] [valid] Ep. 170 : Up. 55000 : bleu : 99.5587 : new best
[2022-10-24 14:08:07] [valid] Ep. 185 : Up. 60000 : cross-entropy : 0.227645 : stalled 1 times (last best: 0.224514)
[2022-10-24 14:08:11] [valid] Ep. 185 : Up. 60000 : perplexity : 1.01595 : stalled 1 times (last best: 1.01573)
[2022-10-24 14:08:17] [valid] Ep. 185 : Up. 60000 : bleu : 99.5929 : new best
[2022-10-24 14:27:31] [valid] Ep. 200 : Up. 65000 : cross-entropy : 0.222047 : new best
[2022-10-24 14:27:35] [valid] Ep. 200 : Up. 65000 : perplexity : 1.01555 : new best
[2022-10-24 14:27:40] [valid] Ep. 200 : Up. 65000 : bleu : 99.588 : stalled 1 times (last best: 99.5929)
[2022-10-24 14:46:53] [valid] Ep. 216 : Up. 70000 : cross-entropy : 0.217974 : new best
[2022-10-24 14:46:57] [valid] Ep. 216 : Up. 70000 : perplexity : 1.01527 : new best
[2022-10-24 14:47:03] [valid] Ep. 216 : Up. 70000 : bleu : 99.5615 : stalled 2 times (last best: 99.5929)
[2022-10-24 15:06:16] [valid] Ep. 231 : Up. 75000 : cross-entropy : 0.206032 : new best
[2022-10-24 15:06:19] [valid] Ep. 231 : Up. 75000 : perplexity : 1.01442 : new best
[2022-10-24 15:06:25] [valid] Ep. 231 : Up. 75000 : bleu : 99.612 : new best
[2022-10-24 15:25:39] [valid] Ep. 247 : Up. 80000 : cross-entropy : 0.200221 : new best
[2022-10-24 15:25:42] [valid] Ep. 247 : Up. 80000 : perplexity : 1.01401 : new best
[2022-10-24 15:25:48] [valid] Ep. 247 : Up. 80000 : bleu : 99.6322 : new best
[2022-10-24 15:44:59] [valid] Ep. 262 : Up. 85000 : cross-entropy : 0.191917 : new best
[2022-10-24 15:45:03] [valid] Ep. 262 : Up. 85000 : perplexity : 1.01343 : new best
[2022-10-24 15:45:09] [valid] Ep. 262 : Up. 85000 : bleu : 99.6642 : new best
[2022-10-24 16:04:19] [valid] Ep. 277 : Up. 90000 : cross-entropy : 0.19092 : new best
[2022-10-24 16:04:23] [valid] Ep. 277 : Up. 90000 : perplexity : 1.01336 : new best
[2022-10-24 16:04:28] [valid] Ep. 277 : Up. 90000 : bleu : 99.684 : new best
[2022-10-24 16:23:38] [valid] Ep. 293 : Up. 95000 : cross-entropy : 0.192416 : stalled 1 times (last best: 0.19092)
[2022-10-24 16:23:41] [valid] Ep. 293 : Up. 95000 : perplexity : 1.01346 : stalled 1 times (last best: 1.01336)
[2022-10-24 16:23:47] [valid] Ep. 293 : Up. 95000 : bleu : 99.683 : stalled 1 times (last best: 99.684)
[2022-10-24 16:42:58] [valid] Ep. 308 : Up. 100000 : cross-entropy : 0.194022 : stalled 2 times (last best: 0.19092)
[2022-10-24 16:43:02] [valid] Ep. 308 : Up. 100000 : perplexity : 1.01358 : stalled 2 times (last best: 1.01336)
[2022-10-24 16:43:07] [valid] Ep. 308 : Up. 100000 : bleu : 99.7262 : new best
[2022-10-24 17:02:22] [valid] Ep. 324 : Up. 105000 : cross-entropy : 0.192045 : stalled 3 times (last best: 0.19092)
[2022-10-24 17:02:25] [valid] Ep. 324 : Up. 105000 : perplexity : 1.01344 : stalled 3 times (last best: 1.01336)
[2022-10-24 17:02:31] [valid] Ep. 324 : Up. 105000 : bleu : 99.7134 : stalled 1 times (last best: 99.7262)
[2022-10-24 17:21:41] [valid] Ep. 339 : Up. 110000 : cross-entropy : 0.194436 : stalled 4 times (last best: 0.19092)
[2022-10-24 17:21:44] [valid] Ep. 339 : Up. 110000 : perplexity : 1.01361 : stalled 4 times (last best: 1.01336)
[2022-10-24 17:21:50] [valid] Ep. 339 : Up. 110000 : bleu : 99.6928 : stalled 2 times (last best: 99.7262)
[2022-10-24 17:41:01] [valid] Ep. 354 : Up. 115000 : cross-entropy : 0.193672 : stalled 5 times (last best: 0.19092)
[2022-10-24 17:41:04] [valid] Ep. 354 : Up. 115000 : perplexity : 1.01355 : stalled 5 times (last best: 1.01336)
[2022-10-24 17:41:09] [valid] Ep. 354 : Up. 115000 : bleu : 99.6928 : stalled 3 times (last best: 99.7262)
[2022-10-24 18:00:23] [valid] Ep. 370 : Up. 120000 : cross-entropy : 0.199348 : stalled 6 times (last best: 0.19092)
[2022-10-24 18:00:26] [valid] Ep. 370 : Up. 120000 : perplexity : 1.01395 : stalled 6 times (last best: 1.01336)
[2022-10-24 18:00:32] [valid] Ep. 370 : Up. 120000 : bleu : 99.6916 : stalled 4 times (last best: 99.7262)
[2022-10-24 18:19:42] [valid] Ep. 385 : Up. 125000 : cross-entropy : 0.196199 : stalled 7 times (last best: 0.19092)
[2022-10-24 18:19:46] [valid] Ep. 385 : Up. 125000 : perplexity : 1.01373 : stalled 7 times (last best: 1.01336)
[2022-10-24 18:19:51] [valid] Ep. 385 : Up. 125000 : bleu : 99.6915 : stalled 5 times (last best: 99.7262)
[2022-10-24 18:39:04] [valid] Ep. 400 : Up. 130000 : cross-entropy : 0.197044 : stalled 8 times (last best: 0.19092)
[2022-10-24 18:39:08] [valid] Ep. 400 : Up. 130000 : perplexity : 1.01379 : stalled 8 times (last best: 1.01336)
[2022-10-24 18:39:13] [valid] Ep. 400 : Up. 130000 : bleu : 99.6893 : stalled 6 times (last best: 99.7262)
[2022-10-24 18:58:26] [valid] Ep. 416 : Up. 135000 : cross-entropy : 0.191972 : stalled 9 times (last best: 0.19092)
[2022-10-24 18:58:30] [valid] Ep. 416 : Up. 135000 : perplexity : 1.01343 : stalled 9 times (last best: 1.01336)
[2022-10-24 18:58:35] [valid] Ep. 416 : Up. 135000 : bleu : 99.6973 : stalled 7 times (last best: 99.7262)
[2022-10-24 19:17:49] [valid] Ep. 431 : Up. 140000 : cross-entropy : 1.74229 : stalled 10 times (last best: 0.19092)
[2022-10-24 19:17:52] [valid] Ep. 431 : Up. 140000 : perplexity : 1.12874 : stalled 10 times (last best: 1.01336)
[2022-10-24 19:17:58] [valid] Ep. 431 : Up. 140000 : bleu : 93.9267 : stalled 8 times (last best: 99.7262)
```

## Preparing a Bash SCript

Preparing a bash script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for Seq2Seq Sentence-Only training,
## Last updated: 25 Oct 2022

data_path="/home/ye/exp/mysent/data-sent";
src="my"; tgt="tg";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.${tgt}, Seq2Seq, Sentence model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.${tgt} >> eval-best-result.txt;
```

## Testing with Seq2Seq Sentence Model 

Testing ...  

```
Every 2.0s: nvidia-smi                                                                           lst-gpu-3090: Tue Oct 25 04:08:10 2022
Tue Oct 25 04:08:10 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.07    Driver Version: 515.65.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
| 32%   64C    P2   255W / 480W |   1999MiB / 24564MiB |     82%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1700      G   /usr/lib/xorg/Xorg                 59MiB |
|    0   N/A  N/A      2469      G   /usr/bin/gnome-shell               10MiB |
|    0   N/A  N/A     97101      C   marian-decoder                   1925MiB |
+-----------------------------------------------------------------------------+
```

Testing finished successfully as follows:   

```
root@2328f1decde9:/home/ye/exp/mysent/model.seq2seq.sent1# time ./test-eval-best.sh
...
...
...
[2022-10-24 21:09:39] Best translation 4696 : B O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4697 : B O O O O N N N E
[2022-10-24 21:09:39] Best translation 4698 : B O O O O N N N E
[2022-10-24 21:09:39] Best translation 4699 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4700 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4701 : B O O O N N N E
[2022-10-24 21:09:39] Best translation 4702 : B O O O N N N E
[2022-10-24 21:09:39] Best translation 4703 : B O O O O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4704 : B O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4705 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4706 : B N N N E
[2022-10-24 21:09:39] Best translation 4707 : B O N N N E
[2022-10-24 21:09:39] Best translation 4708 : B N N E
[2022-10-24 21:09:39] Best translation 4709 : B O O N N N E
[2022-10-24 21:09:39] Best translation 4710 : B O O O O O O N N N E
[2022-10-24 21:09:39] Best translation 4711 : B N N E
[2022-10-24 21:09:39] Total time: 143.89282s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m26.053s
user    2m21.522s
sys     0m4.231s
```

The BLEU score result is as follows:  

```
root@2328f1decde9:/home/ye/exp/mysent/model.seq2seq.sent1# cat eval-best-result.txt
Evaluation with hyp.best.tg, Seq2Seq, Sentence model:
BLEU = 93.52, 95.0/94.2/93.1/91.8 (BP=1.000, ratio=1.050, hyp_len=66799, ref_len=63620)
root@2328f1decde9:/home/ye/exp/mysent/model.seq2seq.sent1#
```

## Preparing a Training Script for Sent+Para Model 

```bash

```


```

```


```

```
