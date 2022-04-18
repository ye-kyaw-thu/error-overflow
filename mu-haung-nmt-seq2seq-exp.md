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
