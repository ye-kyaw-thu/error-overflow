# Sequence-to-Sequence NMT Experiment between MuHaung and Myanmar

## Seq2Seq for my-br

အရင်ဆုံး training လုပ်ဖို့အတွက် bash script (seq2seq-mybr.sh) ကို ပြင်ဆင်ခဲ့...  

```bash
#!/bin/bash

# Preparation for seq2seq NMT experiment between MuHaung Braille and Burmese
# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
## for Word Unit
## Last Updated: 17 April 2022
## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

mkdir model.s2s-mybr;

marian \
  --type s2s \
  --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br \
  --max-length 200 \
  --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br \
  --vocabs  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
  --model model.s2s-mybr/model.npz \
  --workspace 500 \
  --enc-depth 2 --enc-type alternating --enc-cell lstm --enc-cell-depth 2 \
  --dec-depth 2 --dec-cell lstm --dec-cell-base-depth 2 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log model.s2s-mybr/train.log --valid-log model.s2s-mybr/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > model.s2s-mybr/config.yml
  
time marian -c model.s2s-mybr/config.yml  2>&1 | tee s2s.mybr.log
```

Training စလုပ်ပြီး GPU usage က အောက်ပါအတိုင်း...  

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/multi-source/gpu-usage-of-seq2seq-mybr.png" alt="GPU usage for Seq2Seq Architecture my-br" width="600"/>  
</p>  
<div align="center">
  Fig.1 GPU usage of Seq2Seq Architecture NMT training for my-br (MuHaung) translation <br />  
</div> 

<br />

training ကြာချိန်က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./seq2seq-mybr.sh
...
...
...
[2022-04-18 05:54:48] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 05:57:15] Ep. 184 : Up. 60500 : Sen. 7,624 : Cost 0.00429036 * 358,013 after 43,403,154 : Time 567.45s : 630.91 words/s
[2022-04-18 06:00:02] Seen 16415 samples
[2022-04-18 06:00:02] Starting data epoch 185 in logical epoch 185
[2022-04-18 06:00:02] [data] Shuffling data
[2022-04-18 06:00:02] [data] Done reading 16,415 sentences
[2022-04-18 06:00:02] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:05:11] Ep. 185 : Up. 61000 : Sen. 16,204 : Cost 0.00491026 * 359,316 after 43,762,470 : Time 476.10s : 754.71 words/s
[2022-04-18 06:05:16] Seen 16415 samples
[2022-04-18 06:05:16] Starting data epoch 186 in logical epoch 186
[2022-04-18 06:05:16] [data] Shuffling data
[2022-04-18 06:05:16] [data] Done reading 16,415 sentences
[2022-04-18 06:05:16] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:10:30] Seen 16415 samples
[2022-04-18 06:10:30] Starting data epoch 187 in logical epoch 187
[2022-04-18 06:10:30] [data] Shuffling data
[2022-04-18 06:10:30] [data] Done reading 16,415 sentences
[2022-04-18 06:10:30] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:13:04] Ep. 187 : Up. 61500 : Sen. 8,358 : Cost 0.00299245 * 358,936 after 44,121,406 : Time 473.36s : 758.27 words/s
[2022-04-18 06:15:45] Seen 16415 samples
[2022-04-18 06:15:45] Starting data epoch 188 in logical epoch 188
[2022-04-18 06:15:45] [data] Shuffling data
[2022-04-18 06:15:45] [data] Done reading 16,415 sentences
[2022-04-18 06:15:45] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:20:59] Seen 16415 samples
[2022-04-18 06:20:59] Starting data epoch 189 in logical epoch 189
[2022-04-18 06:20:59] [data] Shuffling data
[2022-04-18 06:20:59] [data] Done reading 16,415 sentences
[2022-04-18 06:20:59] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:21:04] Ep. 189 : Up. 62000 : Sen. 120 : Cost 0.00289217 * 357,570 after 44,478,976 : Time 480.03s : 744.89 words/s
[2022-04-18 06:26:12] Seen 16415 samples
[2022-04-18 06:26:12] Starting data epoch 190 in logical epoch 190
[2022-04-18 06:26:12] [data] Shuffling data
[2022-04-18 06:26:12] [data] Done reading 16,415 sentences
[2022-04-18 06:26:12] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:29:00] Ep. 190 : Up. 62500 : Sen. 8,582 : Cost 0.00665823 * 359,006 after 44,837,982 : Time 475.78s : 754.56 words/s
[2022-04-18 06:31:27] Seen 16415 samples
[2022-04-18 06:31:27] Starting data epoch 191 in logical epoch 191
[2022-04-18 06:31:27] [data] Shuffling data
[2022-04-18 06:31:27] [data] Done reading 16,415 sentences
[2022-04-18 06:31:27] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:36:41] Seen 16415 samples
[2022-04-18 06:36:41] Starting data epoch 192 in logical epoch 192
[2022-04-18 06:36:41] [data] Shuffling data
[2022-04-18 06:36:41] [data] Done reading 16,415 sentences
[2022-04-18 06:36:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:36:55] Ep. 192 : Up. 63000 : Sen. 708 : Cost 0.00686512 * 357,910 after 45,195,892 : Time 474.65s : 754.04 words/s
[2022-04-18 06:41:55] Seen 16415 samples
[2022-04-18 06:41:55] Starting data epoch 193 in logical epoch 193
[2022-04-18 06:41:55] [data] Shuffling data
[2022-04-18 06:41:55] [data] Done reading 16,415 sentences
[2022-04-18 06:41:55] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:44:53] Ep. 193 : Up. 63500 : Sen. 9,012 : Cost 0.00255246 * 359,573 after 45,555,465 : Time 478.08s : 752.12 words/s
[2022-04-18 06:47:10] Seen 16415 samples
[2022-04-18 06:47:10] Starting data epoch 194 in logical epoch 194
[2022-04-18 06:47:10] [data] Shuffling data
[2022-04-18 06:47:10] [data] Done reading 16,415 sentences
[2022-04-18 06:47:10] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:52:24] Seen 16415 samples
[2022-04-18 06:52:24] Starting data epoch 195 in logical epoch 195
[2022-04-18 06:52:24] [data] Shuffling data
[2022-04-18 06:52:24] [data] Done reading 16,415 sentences
[2022-04-18 06:52:24] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 06:52:49] Ep. 195 : Up. 64000 : Sen. 1,202 : Cost 0.00352235 * 358,597 after 45,914,062 : Time 476.03s : 753.31 words/s
[2022-04-18 06:57:36] Seen 16415 samples
[2022-04-18 06:57:36] Starting data epoch 196 in logical epoch 196
[2022-04-18 06:57:36] [data] Shuffling data
[2022-04-18 06:57:36] [data] Done reading 16,415 sentences
[2022-04-18 06:57:36] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 07:00:44] Ep. 196 : Up. 64500 : Sen. 9,780 : Cost 0.00406838 * 358,734 after 46,272,796 : Time 475.07s : 755.12 words/s
[2022-04-18 07:02:51] Seen 16415 samples
[2022-04-18 07:02:51] Starting data epoch 197 in logical epoch 197
[2022-04-18 07:02:51] [data] Shuffling data
[2022-04-18 07:02:51] [data] Done reading 16,415 sentences
[2022-04-18 07:02:51] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 07:08:06] Seen 16415 samples
[2022-04-18 07:08:06] Starting data epoch 198 in logical epoch 198
[2022-04-18 07:08:06] [data] Shuffling data
[2022-04-18 07:08:06] [data] Done reading 16,415 sentences
[2022-04-18 07:08:06] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 07:08:36] Ep. 198 : Up. 65000 : Sen. 1,932 : Cost 0.00201767 * 356,297 after 46,629,093 : Time 472.01s : 754.85 words/s
[2022-04-18 07:08:36] Saving model weights and runtime parameters to model.s2s-mybr/model.npz.orig.npz
[2022-04-18 07:08:43] Saving model weights and runtime parameters to model.s2s-mybr/model.iter65000.npz
[2022-04-18 07:08:48] Saving model weights and runtime parameters to model.s2s-mybr/model.npz
[2022-04-18 07:08:55] Saving Adam parameters to model.s2s-mybr/model.npz.optimizer.npz
[2022-04-18 07:09:17] [valid] Ep. 198 : Up. 65000 : cross-entropy : 10.1405 : stalled 10 times (last best: 8.13354)
[2022-04-18 07:09:26] [valid] Ep. 198 : Up. 65000 : perplexity : 2.01128 : stalled 10 times (last best: 1.7515)
[2022-04-18 07:09:26] Translating validation set...
[2022-04-18 07:09:30] Best translation 0 : ⠼⠊ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-18 07:09:30] Best translation 1 : ⠶ ⠨⠣ ⠶ ⠽⠉ ⠗ ⠇⠱⠅ ⠲
[2022-04-18 07:09:30] Best translation 2 : ⠚⠣⠏⠋ ⠝⠌ ⠏⠔⠷⠁ ⠶ ⠙⠻⠨⠔⠍⠕⠆⠏⠺⠔⠂ ⠶ ⠼⠓ ⠲
[2022-04-18 07:09:30] Best translation 3 : ⠶ ⠅⠣ ⠶ ⠏⠥⠂⠛⠋ ⠾⠕⠂ ⠹ ⠷⠶⠥⠆ ⠾⠕⠂⠝⠮ ⠱⠗⠁⠺⠣⠞⠪ ⠾⠭ ⠤⠤⠤⠤⠤⠤ ⠏⠻ ⠞⠺ ⠩ ⠹ ⠲ ⠶ ⠅⠋⠆ ⠒ ⠅⠋⠆ ⠶ ⠲
[2022-04-18 07:09:30] Best translation 4 : ⠥⠂⠻⠆ ⠔⠛⠣⠇⠱⠅ ⠭⠭ ⠒ ⠚⠣⠏⠋ ⠭⠭ ⠒ ⠃⠮ ⠝⠌⠡⠹⠁⠆ ⠏⠮⠆ ⠭⠭ ⠟⠞⠚ ⠞⠖⠆⠿⠪ ⠅ ⠹⠨ ⠇⠦ ⠿⠪⠆ ⠇⠁ ⠕⠅⠡⠦ ⠝⠱ ⠞⠁ ⠅ ⠞⠻⠂ ⠣⠇⠕ ⠋ ⠩ ⠃⠥⠆ ⠇⠕⠂ ⠽⠔⠽⠔⠟⠱⠆⠟⠱⠆ ⠿⠋ ⠿⠻⠆ ⠇⠬ ⠹⠣ ⠞⠮⠂ ⠲
[2022-04-18 07:09:30] Best translation 5 : ⠇⠱⠿⠔⠆⠍⠉⠞⠖⠆ ⠒ ⠹⠉⠆⠈⠶ ⠒ ⠡⠪⠆⠍⠥⠝⠆ ⠒ ⠱⠆⠾⠣ ⠒ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠲
[2022-04-18 07:09:30] Best translation 10 : ⠗⠱⠹⠮ ⠽⠴⠟⠁⠆ ⠱⠝⠩⠱⠂ ⠍⠔⠆ ⠭ ⠿⠪⠆⠝⠴ ⠥⠂⠽⠔ ⠞ ⠞⠺ ⠍⠔⠆⠟⠪⠆ ⠗⠣⠞⠥ ⠩ ⠎⠔ ⠱⠅⠿⠻ ⠝⠱ ⠹⠻⠆ ⠍⠔⠆⠟⠪⠆ ⠅ ⠹⠣⠞⠯ ⠁⠪⠆⠝⠋⠆ ⠽⠥ ⠗⠋ ⠹⠉⠆ ⠟⠢ ⠟⠋⠎⠪ ⠹ ⠲
[2022-04-18 07:09:30] Best translation 20 : ⠍⠻⠆ ⠍⠻⠂ ⠍⠻ ⠲
[2022-04-18 07:09:30] Best translation 40 : ⠁⠮⠂⠇⠬ ⠋⠇ ⠅⠺⠮⠂ ⠹⠁⠆ ⠍⠶ ⠅ ⠲
[2022-04-18 07:09:30] Best translation 80 : ⠝⠱ ⠨⠥⠂ ⠞⠻⠂ ⠿⠓ ⠃⠪⠇⠥⠆⠍⠣ ⠑ ⠅⠬ ⠞⠓⠁⠆ ⠹⠣⠇⠕ ⠾⠑⠠⠣⠁ ⠅ ⠷⠁ ⠞⠥⠝⠂ ⠝⠱ ⠞⠁ ⠏⠮⠆ ⠓⠥⠯ ⠭ ⠏ ⠹⠞ ⠲
[2022-04-18 07:09:30] Best translation 160 : ⠣⠈⠉⠆⠹⠣⠞ ⠲
[2022-04-18 07:09:34] Best translation 320 : ⠞⠮⠂ ⠅⠣ ⠹⠥ ⠿⠋ ⠏⠉ ⠰⠣⠁ ⠲
[2022-04-18 07:09:36] Best translation 640 : ⠕⠆ ⠅⠣⠇⠱⠆ ⠠⠣⠭ ⠇⠉⠆ ⠰⠣⠁ ⠞⠭ ⠇⠉⠆ ⠅⠣ ⠞⠻⠂ ⠕⠆ ⠅⠶⠆ ⠅⠣⠇⠱⠆ ⠭ ⠏⠱⠍⠮⠂ ⠝⠴ ⠞⠭ ⠇⠉⠆ ⠅⠣ ⠞⠻⠂ ⠴⠡⠱ ⠰⠣⠁ ⠑ ⠱ ⠹⠣ ⠞⠮⠂ ⠲
[2022-04-18 07:09:49] Best translation 1280 : ⠎⠁⠕⠅⠾ ⠅ ⠏⠬ ⠰⠣ ⠅⠖ ⠟⠣ ⠏ ⠹ ⠲
[2022-04-18 07:10:06] Best translation 2560 : ⠇⠥⠂⠇⠔ ⠹ ⠍⠊⠍⠊ ⠣⠎⠺⠋⠆ ⠅ ⠗⠺⠁ ⠫ ⠩⠱⠆⠥⠆⠎ ⠿⠣ ⠊ ⠲
[2022-04-18 07:10:07] Total translation time: 40.39035s
[2022-04-18 07:10:07] [valid] Ep. 198 : Up. 65000 : bleu : 87.9275 : stalled 3 times (last best: 88.1486)
[2022-04-18 07:10:08] Training finished
[2022-04-18 07:10:09] Saving model weights and runtime parameters to model.s2s-mybr/model.npz.orig.npz
[2022-04-18 07:10:14] Saving model weights and runtime parameters to model.s2s-mybr/model.npz
[2022-04-18 07:10:20] Saving Adam parameters to model.s2s-mybr/model.npz.optimizer.npz

real	1068m9.327s
user	1788m19.311s
sys	1m38.674s
```

output model တွေကို လေ့လာခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$ ls
config.yml           model.iter25000.npz  model.iter45000.npz  model.iter60000.npz    model.npz.optimizer.npz         model.npz.yml
model.iter10000.npz  model.iter30000.npz  model.iter50000.npz  model.iter65000.npz    model.npz.orig.npz              train.log
model.iter15000.npz  model.iter35000.npz  model.iter5000.npz   model.npz              model.npz.orig.npz.decoder.yml  valid.log
model.iter20000.npz  model.iter40000.npz  model.iter55000.npz  model.npz.decoder.yml  model.npz.progress.yml
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$ ls *.npz | sort -V
model.iter5000.npz
model.iter10000.npz
model.iter15000.npz
model.iter20000.npz
model.iter25000.npz
model.iter30000.npz
model.iter35000.npz
model.iter40000.npz
model.iter45000.npz
model.iter50000.npz
model.iter55000.npz
model.iter60000.npz
model.iter65000.npz
model.npz
model.npz.optimizer.npz
model.npz.orig.npz
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$
```

## Testing/Evaluation of Seq2Seq my-br

bash script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung, MuHaung-Myanmar
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Seq2Seq Model for my-br
## 18 April 2022
# model.iter5000.npz

for i in {5000..65000..5000}
do
   marian-decoder -m ./model.iter$i.npz -v  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter$i.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my
   echo "Evaluation with hyp.iter$i.br, Seq2Seq Model:" >> test-seq2seq-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./hyp.iter$i.br  >> test-seq2seq-results.txt
done
```

testing/evaluation ကို အောက်ပါအတိုင်း run ခဲ့ ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$ time ./tran-eval-seq2seq-mybr.sh 
...
...
...
[2022-04-18 19:55:37] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠡⠭ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-04-18 19:55:37] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-04-18 19:55:37] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-04-18 19:55:37] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠛⠥ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-04-18 19:55:37] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-04-18 19:55:37] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠡⠭ ⠹⠻⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠡⠭ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-04-18 19:55:37] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-18 19:55:37] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-04-18 19:55:37] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-04-18 19:55:38] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏ ⠇⠮⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌⠁ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏⠁ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-04-18 19:55:38] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠡⠭ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-04-18 19:55:38] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-18 19:55:38] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠿⠱ ⠍⠥⠞⠮ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-04-18 19:55:38] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟⠣ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠈⠉⠆⠿⠓⠣⠞ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-04-18 19:55:38] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-04-18 19:55:38] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-04-18 19:55:38] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-04-18 19:55:38] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-04-18 19:55:38] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-04-18 19:55:38] Best translation 2160 : ⠟⠁⠆ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-04-18 19:55:38] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-04-18 19:55:38] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-18 19:55:38] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-04-18 19:55:38] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-04-18 19:55:38] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-04-18 19:55:39] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠡⠭ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-04-18 19:55:39] Total time: 137.95682s wall

real	32m4.305s
user	60m9.064s
sys	0m49.562s
```

score တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$ cat ./test-seq2seq-results.txt 
Evaluation with hyp.iter5000.br, Seq2Seq Model:
BLEU = 79.89, 89.3/82.9/77.0/71.5 (BP=1.000, ratio=1.024, hyp_len=29506, ref_len=28803)
Evaluation with hyp.iter10000.br, Seq2Seq Model:
BLEU = 86.86, 94.0/89.2/84.6/80.2 (BP=1.000, ratio=1.007, hyp_len=29007, ref_len=28803)
Evaluation with hyp.iter15000.br, Seq2Seq Model:
BLEU = 86.92, 94.0/89.2/84.7/80.3 (BP=1.000, ratio=1.009, hyp_len=29062, ref_len=28803)
Evaluation with hyp.iter20000.br, Seq2Seq Model:
BLEU = 86.16, 93.3/88.5/83.9/79.6 (BP=1.000, ratio=1.016, hyp_len=29255, ref_len=28803)
Evaluation with hyp.iter25000.br, Seq2Seq Model:
BLEU = 87.64, 94.6/89.9/85.5/81.1 (BP=1.000, ratio=1.002, hyp_len=28863, ref_len=28803)
Evaluation with hyp.iter30000.br, Seq2Seq Model:
BLEU = 87.71, 94.6/90.0/85.5/81.3 (BP=1.000, ratio=1.002, hyp_len=28867, ref_len=28803)
Evaluation with hyp.iter35000.br, Seq2Seq Model:
BLEU = 88.24, 95.2/90.5/86.1/81.8 (BP=1.000, ratio=1.000, hyp_len=28795, ref_len=28803)
Evaluation with hyp.iter40000.br, Seq2Seq Model:
BLEU = 88.27, 95.3/90.6/86.2/82.0 (BP=0.999, ratio=0.999, hyp_len=28764, ref_len=28803)
Evaluation with hyp.iter45000.br, Seq2Seq Model:
BLEU = 88.32, 95.3/90.6/86.2/82.0 (BP=0.999, ratio=0.999, hyp_len=28779, ref_len=28803)
Evaluation with hyp.iter50000.br, Seq2Seq Model:
BLEU = 88.25, 95.3/90.6/86.2/81.9 (BP=0.999, ratio=0.999, hyp_len=28763, ref_len=28803)
Evaluation with hyp.iter55000.br, Seq2Seq Model:
BLEU = 88.27, 95.3/90.7/86.3/82.0 (BP=0.998, ratio=0.998, hyp_len=28752, ref_len=28803)
Evaluation with hyp.iter60000.br, Seq2Seq Model:
BLEU = 88.25, 95.3/90.7/86.3/82.1 (BP=0.997, ratio=0.997, hyp_len=28723, ref_len=28803)
Evaluation with hyp.iter65000.br, Seq2Seq Model:
BLEU = 88.33, 95.3/90.7/86.3/82.1 (BP=0.998, ratio=0.998, hyp_len=28754, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$
```

best model နဲ့ best score က အောက်ပါအတိုင်း...  

```
Evaluation with hyp.iter65000.br, Seq2Seq Model:
BLEU = 88.33, 95.3/90.7/86.3/82.1 (BP=0.998, ratio=0.998, hyp_len=28754, ref_len=28803)
```

## Training Seq2Seq for br-my

ဒီတစ်ခါတော့ မူဟောင်း ကနေ မြန်မာစာကို sequence-to-sequence architecture နဲ့ ဘာသာပြန်ဖို့အတွက် ပြင်ဆင်မယ်။  
training လုပ်ဖို့အတွက် bash script က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

# Preparation for seq2seq NMT experiment between MuHaung Braille and Burmese
# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
## for Word Unit
## Last Updated: 18 April 2022
## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

mkdir model.s2s-brmy;

marian \
  --type s2s \
  --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my \
  --max-length 200 \
  --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my \
  --vocabs  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
  --model model.s2s-brmy/model.npz \
  --workspace 500 \
  --enc-depth 2 --enc-type alternating --enc-cell lstm --enc-cell-depth 2 \
  --dec-depth 2 --dec-cell lstm --dec-cell-base-depth 2 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log model.s2s-brmy/train.log --valid-log model.s2s-brmy/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > model.s2s-brmy/config.yml
  
time marian -c model.s2s-brmy/config.yml  2>&1 | tee s2s.brmy.log

```

training ကို အောက်ပါအတိုင်း run ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ gedit seq2seq-brmy.sh
(base) ye@:/media/ye/project2/exp/braille-nmt$ chmod +x ./seq2seq-brmy.sh 
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./seq2seq-brmy.sh 
[2022-04-18 20:09:58] [marian] Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-04-18 20:09:58] [marian] Running on administrator-HP-Z2-Tower-G4-Workstation as process 365527 with command line:
[2022-04-18 20:09:58] [marian] marian -c model.s2s-brmy/config.yml
[2022-04-18 20:09:58] [config] after: 0e
[2022-04-18 20:09:58] [config] after-batches: 0
[2022-04-18 20:09:58] [config] after-epochs: 0
[2022-04-18 20:09:58] [config] all-caps-every: 0
[2022-04-18 20:09:58] [config] allow-unk: false
[2022-04-18 20:09:58] [config] authors: false
[2022-04-18 20:09:58] [config] beam-size: 12
[2022-04-18 20:09:58] [config] bert-class-symbol: "[CLS]"
[2022-04-18 20:09:58] [config] bert-mask-symbol: "[MASK]"
[2022-04-18 20:09:58] [config] bert-masking-fraction: 0.15
[2022-04-18 20:09:58] [config] bert-sep-symbol: "[SEP]"
[2022-04-18 20:09:58] [config] bert-train-type-embeddings: true
[2022-04-18 20:09:58] [config] bert-type-vocab-size: 2
[2022-04-18 20:09:58] [config] build-info: ""
[2022-04-18 20:09:58] [config] cite: false
[2022-04-18 20:09:58] [config] clip-norm: 1
[2022-04-18 20:09:58] [config] cost-scaling:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] cost-type: ce-sum
[2022-04-18 20:09:58] [config] cpu-threads: 0
[2022-04-18 20:09:58] [config] data-weighting: ""
[2022-04-18 20:09:58] [config] data-weighting-type: sentence
[2022-04-18 20:09:58] [config] dec-cell: lstm
[2022-04-18 20:09:58] [config] dec-cell-base-depth: 2
[2022-04-18 20:09:58] [config] dec-cell-high-depth: 2
[2022-04-18 20:09:58] [config] dec-depth: 2
[2022-04-18 20:09:58] [config] devices:
[2022-04-18 20:09:58] [config]   - 0
[2022-04-18 20:09:58] [config]   - 1
[2022-04-18 20:09:58] [config] dim-emb: 512
[2022-04-18 20:09:58] [config] dim-rnn: 1024
[2022-04-18 20:09:58] [config] dim-vocabs:
[2022-04-18 20:09:58] [config]   - 0
[2022-04-18 20:09:58] [config]   - 0
[2022-04-18 20:09:58] [config] disp-first: 0
[2022-04-18 20:09:58] [config] disp-freq: 500
[2022-04-18 20:09:58] [config] disp-label-counts: true
[2022-04-18 20:09:58] [config] dropout-rnn: 0.3
[2022-04-18 20:09:58] [config] dropout-src: 0.3
[2022-04-18 20:09:58] [config] dropout-trg: 0
[2022-04-18 20:09:58] [config] dump-config: ""
[2022-04-18 20:09:58] [config] early-stopping: 10
[2022-04-18 20:09:58] [config] embedding-fix-src: false
[2022-04-18 20:09:58] [config] embedding-fix-trg: false
[2022-04-18 20:09:58] [config] embedding-normalization: false
[2022-04-18 20:09:58] [config] embedding-vectors:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] enc-cell: lstm
[2022-04-18 20:09:58] [config] enc-cell-depth: 2
[2022-04-18 20:09:58] [config] enc-depth: 2
[2022-04-18 20:09:58] [config] enc-type: alternating
[2022-04-18 20:09:58] [config] english-title-case-every: 0
[2022-04-18 20:09:58] [config] exponential-smoothing: 0.0001
[2022-04-18 20:09:58] [config] factor-weight: 1
[2022-04-18 20:09:58] [config] grad-dropping-momentum: 0
[2022-04-18 20:09:58] [config] grad-dropping-rate: 0
[2022-04-18 20:09:58] [config] grad-dropping-warmup: 100
[2022-04-18 20:09:58] [config] gradient-checkpointing: false
[2022-04-18 20:09:58] [config] guided-alignment: none
[2022-04-18 20:09:58] [config] guided-alignment-cost: mse
[2022-04-18 20:09:58] [config] guided-alignment-weight: 0.1
[2022-04-18 20:09:58] [config] ignore-model-config: false
[2022-04-18 20:09:58] [config] input-types:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] interpolate-env-vars: false
[2022-04-18 20:09:58] [config] keep-best: false
[2022-04-18 20:09:58] [config] label-smoothing: 0
[2022-04-18 20:09:58] [config] layer-normalization: true
[2022-04-18 20:09:58] [config] learn-rate: 0.0001
[2022-04-18 20:09:58] [config] lemma-dim-emb: 0
[2022-04-18 20:09:58] [config] log: model.s2s-brmy/train.log
[2022-04-18 20:09:58] [config] log-level: info
[2022-04-18 20:09:58] [config] log-time-zone: ""
[2022-04-18 20:09:58] [config] logical-epoch:
[2022-04-18 20:09:58] [config]   - 1e
[2022-04-18 20:09:58] [config]   - 0
[2022-04-18 20:09:58] [config] lr-decay: 0
[2022-04-18 20:09:58] [config] lr-decay-freq: 50000
[2022-04-18 20:09:58] [config] lr-decay-inv-sqrt:
[2022-04-18 20:09:58] [config]   - 0
[2022-04-18 20:09:58] [config] lr-decay-repeat-warmup: false
[2022-04-18 20:09:58] [config] lr-decay-reset-optimizer: false
[2022-04-18 20:09:58] [config] lr-decay-start:
[2022-04-18 20:09:58] [config]   - 10
[2022-04-18 20:09:58] [config]   - 1
[2022-04-18 20:09:58] [config] lr-decay-strategy: epoch+stalled
[2022-04-18 20:09:58] [config] lr-report: false
[2022-04-18 20:09:58] [config] lr-warmup: 0
[2022-04-18 20:09:58] [config] lr-warmup-at-reload: false
[2022-04-18 20:09:58] [config] lr-warmup-cycle: false
[2022-04-18 20:09:58] [config] lr-warmup-start-rate: 0
[2022-04-18 20:09:58] [config] max-length: 200
[2022-04-18 20:09:58] [config] max-length-crop: false
[2022-04-18 20:09:58] [config] max-length-factor: 3
[2022-04-18 20:09:58] [config] maxi-batch: 100
[2022-04-18 20:09:58] [config] maxi-batch-sort: trg
[2022-04-18 20:09:58] [config] mini-batch: 64
[2022-04-18 20:09:58] [config] mini-batch-fit: true
[2022-04-18 20:09:58] [config] mini-batch-fit-step: 10
[2022-04-18 20:09:58] [config] mini-batch-track-lr: false
[2022-04-18 20:09:58] [config] mini-batch-warmup: 0
[2022-04-18 20:09:58] [config] mini-batch-words: 0
[2022-04-18 20:09:58] [config] mini-batch-words-ref: 0
[2022-04-18 20:09:58] [config] model: model.s2s-brmy/model.npz
[2022-04-18 20:09:58] [config] multi-loss-type: sum
[2022-04-18 20:09:58] [config] multi-node: false
[2022-04-18 20:09:58] [config] multi-node-overlap: true
[2022-04-18 20:09:58] [config] n-best: false
[2022-04-18 20:09:58] [config] no-nccl: false
[2022-04-18 20:09:58] [config] no-reload: false
[2022-04-18 20:09:58] [config] no-restore-corpus: false
[2022-04-18 20:09:58] [config] normalize: 0
[2022-04-18 20:09:58] [config] normalize-gradient: false
[2022-04-18 20:09:58] [config] num-devices: 0
[2022-04-18 20:09:58] [config] optimizer: adam
[2022-04-18 20:09:58] [config] optimizer-delay: 1
[2022-04-18 20:09:58] [config] optimizer-params:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] output-omit-bias: false
[2022-04-18 20:09:58] [config] overwrite: false
[2022-04-18 20:09:58] [config] precision:
[2022-04-18 20:09:58] [config]   - float32
[2022-04-18 20:09:58] [config]   - float32
[2022-04-18 20:09:58] [config]   - float32
[2022-04-18 20:09:58] [config] pretrained-model: ""
[2022-04-18 20:09:58] [config] quantize-biases: false
[2022-04-18 20:09:58] [config] quantize-bits: 0
[2022-04-18 20:09:58] [config] quantize-log-based: false
[2022-04-18 20:09:58] [config] quantize-optimization-steps: 0
[2022-04-18 20:09:58] [config] quiet: false
[2022-04-18 20:09:58] [config] quiet-translation: false
[2022-04-18 20:09:58] [config] relative-paths: false
[2022-04-18 20:09:58] [config] right-left: false
[2022-04-18 20:09:58] [config] save-freq: 5000
[2022-04-18 20:09:58] [config] seed: 1111
[2022-04-18 20:09:58] [config] sentencepiece-alphas:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] sentencepiece-max-lines: 2000000
[2022-04-18 20:09:58] [config] sentencepiece-options: ""
[2022-04-18 20:09:58] [config] shuffle: data
[2022-04-18 20:09:58] [config] shuffle-in-ram: false
[2022-04-18 20:09:58] [config] sigterm: save-and-exit
[2022-04-18 20:09:58] [config] skip: true
[2022-04-18 20:09:58] [config] sqlite: ""
[2022-04-18 20:09:58] [config] sqlite-drop: false
[2022-04-18 20:09:58] [config] sync-sgd: true
[2022-04-18 20:09:58] [config] tempdir: /tmp
[2022-04-18 20:09:58] [config] tied-embeddings: true
[2022-04-18 20:09:58] [config] tied-embeddings-all: false
[2022-04-18 20:09:58] [config] tied-embeddings-src: false
[2022-04-18 20:09:58] [config] train-embedder-rank:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] train-sets:
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my
[2022-04-18 20:09:58] [config] transformer-aan-activation: swish
[2022-04-18 20:09:58] [config] transformer-aan-depth: 2
[2022-04-18 20:09:58] [config] transformer-aan-nogate: false
[2022-04-18 20:09:58] [config] transformer-decoder-autoreg: self-attention
[2022-04-18 20:09:58] [config] transformer-depth-scaling: false
[2022-04-18 20:09:58] [config] transformer-dim-aan: 2048
[2022-04-18 20:09:58] [config] transformer-dim-ffn: 2048
[2022-04-18 20:09:58] [config] transformer-dropout: 0
[2022-04-18 20:09:58] [config] transformer-dropout-attention: 0
[2022-04-18 20:09:58] [config] transformer-dropout-ffn: 0
[2022-04-18 20:09:58] [config] transformer-ffn-activation: swish
[2022-04-18 20:09:58] [config] transformer-ffn-depth: 2
[2022-04-18 20:09:58] [config] transformer-guided-alignment-layer: last
[2022-04-18 20:09:58] [config] transformer-heads: 8
[2022-04-18 20:09:58] [config] transformer-no-projection: false
[2022-04-18 20:09:58] [config] transformer-pool: false
[2022-04-18 20:09:58] [config] transformer-postprocess: dan
[2022-04-18 20:09:58] [config] transformer-postprocess-emb: d
[2022-04-18 20:09:58] [config] transformer-postprocess-top: ""
[2022-04-18 20:09:58] [config] transformer-preprocess: ""
[2022-04-18 20:09:58] [config] transformer-tied-layers:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] transformer-train-position-embeddings: false
[2022-04-18 20:09:58] [config] tsv: false
[2022-04-18 20:09:58] [config] tsv-fields: 0
[2022-04-18 20:09:58] [config] type: s2s
[2022-04-18 20:09:58] [config] ulr: false
[2022-04-18 20:09:58] [config] ulr-dim-emb: 0
[2022-04-18 20:09:58] [config] ulr-dropout: 0
[2022-04-18 20:09:58] [config] ulr-keys-vectors: ""
[2022-04-18 20:09:58] [config] ulr-query-vectors: ""
[2022-04-18 20:09:58] [config] ulr-softmax-temperature: 1
[2022-04-18 20:09:58] [config] ulr-trainable-transformation: false
[2022-04-18 20:09:58] [config] unlikelihood-loss: false
[2022-04-18 20:09:58] [config] valid-freq: 5000
[2022-04-18 20:09:58] [config] valid-log: model.s2s-brmy/valid.log
[2022-04-18 20:09:58] [config] valid-max-length: 1000
[2022-04-18 20:09:58] [config] valid-metrics:
[2022-04-18 20:09:58] [config]   - cross-entropy
[2022-04-18 20:09:58] [config]   - perplexity
[2022-04-18 20:09:58] [config]   - bleu
[2022-04-18 20:09:58] [config] valid-mini-batch: 32
[2022-04-18 20:09:58] [config] valid-reset-stalled: false
[2022-04-18 20:09:58] [config] valid-script-args:
[2022-04-18 20:09:58] [config]   []
[2022-04-18 20:09:58] [config] valid-script-path: ""
[2022-04-18 20:09:58] [config] valid-sets:
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my
[2022-04-18 20:09:58] [config] valid-translation-output: ""
[2022-04-18 20:09:58] [config] vocabs:
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-04-18 20:09:58] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-04-18 20:09:58] [config] word-penalty: 0
[2022-04-18 20:09:58] [config] word-scores: false
[2022-04-18 20:09:58] [config] workspace: 500
[2022-04-18 20:09:58] [config] Model is being created with Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-04-18 20:09:58] Using synchronous SGD
[2022-04-18 20:09:58] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-04-18 20:09:58] [data] Setting vocabulary size for input 0 to 18,364
[2022-04-18 20:09:58] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-04-18 20:09:59] [data] Setting vocabulary size for input 1 to 18,602
[2022-04-18 20:09:59] [comm] Compiled without MPI support. Running as a single process on administrator-HP-Z2-Tower-G4-Workstation
[2022-04-18 20:09:59] [batching] Collecting statistics for batch fitting with step size 10
[2022-04-18 20:09:59] [memory] Extending reserved space to 512 MB (device gpu0)
[2022-04-18 20:09:59] [memory] Extending reserved space to 512 MB (device gpu1)
[2022-04-18 20:09:59] [comm] Using NCCL 2.8.3 for GPU communication
[2022-04-18 20:09:59] [comm] NCCLCommunicator constructed successfully
[2022-04-18 20:09:59] [training] Using 2 GPUs
[2022-04-18 20:09:59] [logits] Applying loss function for 1 factor(s)
[2022-04-18 20:09:59] [memory] Reserving 407 MB, device gpu0
[2022-04-18 20:09:59] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-04-18 20:10:00] [memory] Reserving 407 MB, device gpu0
[2022-04-18 20:11:24] [batching] Done. Typical MB size is 882 target words
[2022-04-18 20:11:24] [memory] Extending reserved space to 512 MB (device gpu0)
[2022-04-18 20:11:24] [memory] Extending reserved space to 512 MB (device gpu1)
[2022-04-18 20:11:24] [comm] Using NCCL 2.8.3 for GPU communication
[2022-04-18 20:11:24] [comm] NCCLCommunicator constructed successfully
[2022-04-18 20:11:24] [training] Using 2 GPUs
[2022-04-18 20:11:24] Training started
[2022-04-18 20:11:24] [data] Shuffling data
[2022-04-18 20:11:24] [data] Done reading 16,415 sentences
[2022-04-18 20:11:24] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:11:24] [training] Batches are processed as 1 process(es) x 2 devices/process
[2022-04-18 20:11:24] [memory] Reserving 407 MB, device gpu0
[2022-04-18 20:11:24] [memory] Reserving 407 MB, device gpu1
[2022-04-18 20:11:25] [memory] Reserving 407 MB, device gpu0
[2022-04-18 20:11:25] [memory] Reserving 407 MB, device gpu1
[2022-04-18 20:11:25] [memory] Reserving 203 MB, device gpu0
[2022-04-18 20:11:25] [memory] Reserving 203 MB, device gpu1
[2022-04-18 20:11:26] [memory] Reserving 407 MB, device gpu1
[2022-04-18 20:11:26] [memory] Reserving 407 MB, device gpu0
[2022-04-18 20:16:50] Seen 16415 samples
[2022-04-18 20:16:50] Starting data epoch 2 in logical epoch 2
[2022-04-18 20:16:50] [data] Shuffling data
[2022-04-18 20:16:50] [data] Done reading 16,415 sentences
[2022-04-18 20:16:50] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:19:39] Ep. 2 : Up. 500 : Sen. 8,466 : Cost 6.71785927 * 358,634 after 358,634 : Time 494.82s : 724.78 words/s
[2022-04-18 20:22:12] Seen 16415 samples
[2022-04-18 20:22:12] Starting data epoch 3 in logical epoch 3
[2022-04-18 20:22:12] [data] Shuffling data
[2022-04-18 20:22:12] [data] Done reading 16,415 sentences
[2022-04-18 20:22:12] [data] Done shuffling 16,415 sentences to temp files
...
...
...

```

output model တွေက အောက်ပါအတိုင်း...  

```

```

## Testing/Evaluation for Seq2Seq br-my

bash script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```bash

```

testing/evaluation for seq2seq br-my direction ...  

```

```
