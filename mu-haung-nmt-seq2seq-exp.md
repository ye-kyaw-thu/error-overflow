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
[2022-04-18 20:27:34] Seen 16415 samples
[2022-04-18 20:27:34] Starting data epoch 4 in logical epoch 4
[2022-04-18 20:27:34] [data] Shuffling data
[2022-04-18 20:27:34] [data] Done reading 16,415 sentences
[2022-04-18 20:27:34] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:27:46] Ep. 4 : Up. 1000 : Sen. 614 : Cost 5.31393194 * 359,931 after 718,565 : Time 487.34s : 738.56 words/s
[2022-04-18 20:32:56] Seen 16415 samples
[2022-04-18 20:32:56] Starting data epoch 5 in logical epoch 5
[2022-04-18 20:32:56] [data] Shuffling data
[2022-04-18 20:32:56] [data] Done reading 16,415 sentences
[2022-04-18 20:32:56] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:35:47] Ep. 5 : Up. 1500 : Sen. 9,378 : Cost 4.33697367 * 357,067 after 1,075,632 : Time 481.10s : 742.19 words/s
[2022-04-18 20:38:18] Seen 16415 samples
[2022-04-18 20:38:18] Starting data epoch 6 in logical epoch 6
[2022-04-18 20:38:18] [data] Shuffling data
[2022-04-18 20:38:18] [data] Done reading 16,415 sentences
[2022-04-18 20:38:18] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:43:39] Seen 16415 samples
[2022-04-18 20:43:39] Starting data epoch 7 in logical epoch 7
[2022-04-18 20:43:39] [data] Shuffling data
[2022-04-18 20:43:39] [data] Done reading 16,415 sentences
[2022-04-18 20:43:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-18 20:44:02] Ep. 7 : Up. 2000 : Sen. 1,174 : Cost 3.41581845 * 360,787 after 1,436,419 : Time 494.66s : 729.37 words/s
...
...
...
[2022-04-19 05:32:01] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 05:35:22] Ep. 105 : Up. 34500 : Sen. 10,268 : Cost 0.00579593 * 360,637 after 24,754,409 : Time 479.94s : 751.42 words/s
[2022-04-19 05:37:16] Seen 16415 samples
[2022-04-19 05:37:16] Starting data epoch 106 in logical epoch 106
[2022-04-19 05:37:16] [data] Shuffling data
[2022-04-19 05:37:16] [data] Done reading 16,415 sentences
[2022-04-19 05:37:16] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 05:42:31] Seen 16415 samples
[2022-04-19 05:42:31] Starting data epoch 107 in logical epoch 107
[2022-04-19 05:42:31] [data] Shuffling data
[2022-04-19 05:42:31] [data] Done reading 16,415 sentences
[2022-04-19 05:42:31] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 05:43:18] Ep. 107 : Up. 35000 : Sen. 2,530 : Cost 0.00640339 * 358,208 after 25,112,617 : Time 476.48s : 751.77 words/s
[2022-04-19 05:43:18] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 05:43:25] Saving model weights and runtime parameters to model.s2s-brmy/model.iter35000.npz
[2022-04-19 05:43:31] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 05:43:38] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 05:44:02] [valid] Ep. 107 : Up. 35000 : cross-entropy : 9.40685 : stalled 5 times (last best: 8.16755)
[2022-04-19 05:44:11] [valid] Ep. 107 : Up. 35000 : perplexity : 1.91213 : stalled 5 times (last best: 1.75561)
[2022-04-19 05:44:11] Translating validation set...
[2022-04-19 05:44:15] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 05:44:15] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 05:44:15] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ၂ ) ။
[2022-04-19 05:44:15] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 05:44:15] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 05:44:15] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 05:44:15] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 05:44:15] Best translation 20 : မော မော့ မော် ။
[2022-04-19 05:44:15] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 05:44:15] Best translation 80 : လင်း ခု တော့ ဖြင့် ဘီလူးမ လူရွယ် ကိုက် ထား သလို မျက်နှာ ကို လည်း တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 05:44:15] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 05:44:19] Best translation 320 : မြေ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 05:44:21] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 05:44:36] Best translation 1280 : စာအုပ်များ ကို ကောင်း အောင် ကိုင် ကြ ပါ သည် ။
[2022-04-19 05:44:52] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 05:44:53] Total translation time: 42.25673s
[2022-04-19 05:44:53] [valid] Ep. 107 : Up. 35000 : bleu : 87.0127 : stalled 4 times (last best: 87.9496)
[2022-04-19 05:49:22] Seen 16415 samples
[2022-04-19 05:49:22] Starting data epoch 108 in logical epoch 108
[2022-04-19 05:49:22] [data] Shuffling data
[2022-04-19 05:49:23] [data] Done reading 16,415 sentences
[2022-04-19 05:49:23] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 05:52:54] Ep. 108 : Up. 35500 : Sen. 10,814 : Cost 0.01375661 * 359,294 after 25,471,911 : Time 575.99s : 623.79 words/s
[2022-04-19 05:54:38] Seen 16415 samples
[2022-04-19 05:54:38] Starting data epoch 109 in logical epoch 109
[2022-04-19 05:54:38] [data] Shuffling data
[2022-04-19 05:54:38] [data] Done reading 16,415 sentences
[2022-04-19 05:54:38] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 05:59:53] Seen 16415 samples
[2022-04-19 05:59:53] Starting data epoch 110 in logical epoch 110
[2022-04-19 05:59:53] [data] Shuffling data
[2022-04-19 05:59:53] [data] Done reading 16,415 sentences
[2022-04-19 05:59:53] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:00:53] Ep. 110 : Up. 36000 : Sen. 3,014 : Cost 0.01161062 * 358,623 after 25,830,534 : Time 478.53s : 749.42 words/s
[2022-04-19 06:05:08] Seen 16415 samples
[2022-04-19 06:05:08] Starting data epoch 111 in logical epoch 111
[2022-04-19 06:05:08] [data] Shuffling data
[2022-04-19 06:05:08] [data] Done reading 16,415 sentences
[2022-04-19 06:05:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:08:48] Ep. 111 : Up. 36500 : Sen. 11,590 : Cost 0.00668656 * 358,142 after 26,188,676 : Time 475.61s : 753.01 words/s
[2022-04-19 06:10:23] Seen 16415 samples
[2022-04-19 06:10:24] Starting data epoch 112 in logical epoch 112
[2022-04-19 06:10:24] [data] Shuffling data
[2022-04-19 06:10:24] [data] Done reading 16,415 sentences
[2022-04-19 06:10:24] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:15:39] Seen 16415 samples
[2022-04-19 06:15:40] Starting data epoch 113 in logical epoch 113
[2022-04-19 06:15:40] [data] Shuffling data
[2022-04-19 06:15:40] [data] Done reading 16,415 sentences
[2022-04-19 06:15:40] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:16:47] Ep. 113 : Up. 37000 : Sen. 3,656 : Cost 0.00636050 * 358,766 after 26,547,442 : Time 478.48s : 749.81 words/s
[2022-04-19 06:20:54] Seen 16415 samples
[2022-04-19 06:20:54] Starting data epoch 114 in logical epoch 114
[2022-04-19 06:20:54] [data] Shuffling data
[2022-04-19 06:20:55] [data] Done reading 16,415 sentences
[2022-04-19 06:20:55] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:24:45] Ep. 114 : Up. 37500 : Sen. 12,018 : Cost 0.00822530 * 359,206 after 26,906,648 : Time 477.58s : 752.13 words/s
[2022-04-19 06:26:09] Seen 16415 samples
[2022-04-19 06:26:10] Starting data epoch 115 in logical epoch 115
[2022-04-19 06:26:10] [data] Shuffling data
[2022-04-19 06:26:10] [data] Done reading 16,415 sentences
[2022-04-19 06:26:10] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:31:25] Seen 16415 samples
[2022-04-19 06:31:25] Starting data epoch 116 in logical epoch 116
[2022-04-19 06:31:25] [data] Shuffling data
[2022-04-19 06:31:25] [data] Done reading 16,415 sentences
[2022-04-19 06:31:25] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:32:44] Ep. 116 : Up. 38000 : Sen. 4,184 : Cost 0.00656674 * 357,329 after 27,263,977 : Time 479.10s : 745.84 words/s
[2022-04-19 06:36:40] Seen 16415 samples
[2022-04-19 06:36:40] Starting data epoch 117 in logical epoch 117
[2022-04-19 06:36:40] [data] Shuffling data
[2022-04-19 06:36:40] [data] Done reading 16,415 sentences
[2022-04-19 06:36:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:40:41] Ep. 117 : Up. 38500 : Sen. 12,568 : Cost 0.01617317 * 359,751 after 27,623,728 : Time 476.61s : 754.81 words/s
[2022-04-19 06:41:55] Seen 16415 samples
[2022-04-19 06:41:55] Starting data epoch 118 in logical epoch 118
[2022-04-19 06:41:55] [data] Shuffling data
[2022-04-19 06:41:56] [data] Done reading 16,415 sentences
[2022-04-19 06:41:56] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:47:10] Seen 16415 samples
[2022-04-19 06:47:10] Starting data epoch 119 in logical epoch 119
[2022-04-19 06:47:10] [data] Shuffling data
[2022-04-19 06:47:10] [data] Done reading 16,415 sentences
[2022-04-19 06:47:10] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:48:43] Ep. 119 : Up. 39000 : Sen. 4,686 : Cost 0.02516662 * 360,610 after 27,984,338 : Time 481.26s : 749.30 words/s
[2022-04-19 06:52:25] Seen 16415 samples
[2022-04-19 06:52:25] Starting data epoch 120 in logical epoch 120
[2022-04-19 06:52:25] [data] Shuffling data
[2022-04-19 06:52:26] [data] Done reading 16,415 sentences
[2022-04-19 06:52:26] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 06:56:40] Ep. 120 : Up. 39500 : Sen. 13,138 : Cost 0.01320441 * 359,152 after 28,343,490 : Time 477.29s : 752.48 words/s
[2022-04-19 06:57:40] Seen 16415 samples
[2022-04-19 06:57:40] Starting data epoch 121 in logical epoch 121
[2022-04-19 06:57:40] [data] Shuffling data
[2022-04-19 06:57:41] [data] Done reading 16,415 sentences
[2022-04-19 06:57:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:02:56] Seen 16415 samples
[2022-04-19 07:02:56] Starting data epoch 122 in logical epoch 122
[2022-04-19 07:02:56] [data] Shuffling data
[2022-04-19 07:02:57] [data] Done reading 16,415 sentences
[2022-04-19 07:02:57] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:04:37] Ep. 122 : Up. 40000 : Sen. 5,454 : Cost 0.00377337 * 358,782 after 28,702,272 : Time 476.47s : 753.00 words/s
[2022-04-19 07:04:37] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 07:04:44] Saving model weights and runtime parameters to model.s2s-brmy/model.iter40000.npz
[2022-04-19 07:04:50] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 07:04:57] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 07:05:21] [valid] Ep. 122 : Up. 40000 : cross-entropy : 9.5574 : stalled 6 times (last best: 8.16755)
[2022-04-19 07:05:30] [valid] Ep. 122 : Up. 40000 : perplexity : 1.93207 : stalled 6 times (last best: 1.75561)
[2022-04-19 07:05:30] Translating validation set...
[2022-04-19 07:05:34] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 07:05:34] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 07:05:34] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ၂ ) ။
[2022-04-19 07:05:34] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 07:05:34] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 07:05:34] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 07:05:34] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 07:05:34] Best translation 20 : မော မော့ မော် ။
[2022-04-19 07:05:34] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 07:05:34] Best translation 80 : ရှက် ခု တော့ ဖြင့် ဘီလူးမ လူရွယ် ကိုက် ထား သလို မျက်နှာ ကို လည်း တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 07:05:34] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 07:05:38] Best translation 320 : မြေ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 07:05:40] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 07:05:55] Best translation 1280 : စာအုပ်များ ကို သွေး သင် ကိုင် ကြ ပါ သည် ။
[2022-04-19 07:06:12] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 07:06:13] Total translation time: 42.13990s
[2022-04-19 07:06:13] [valid] Ep. 122 : Up. 40000 : bleu : 87.5724 : stalled 5 times (last best: 87.9496)
[2022-04-19 07:09:49] Seen 16415 samples
[2022-04-19 07:09:49] Starting data epoch 123 in logical epoch 123
[2022-04-19 07:09:49] [data] Shuffling data
[2022-04-19 07:09:50] [data] Done reading 16,415 sentences
[2022-04-19 07:09:50] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:14:13] Ep. 123 : Up. 40500 : Sen. 13,618 : Cost 0.00967115 * 358,346 after 29,060,618 : Time 575.93s : 622.21 words/s
[2022-04-19 07:15:05] Seen 16415 samples
[2022-04-19 07:15:05] Starting data epoch 124 in logical epoch 124
[2022-04-19 07:15:05] [data] Shuffling data
[2022-04-19 07:15:05] [data] Done reading 16,415 sentences
[2022-04-19 07:15:05] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:20:21] Seen 16415 samples
[2022-04-19 07:20:21] Starting data epoch 125 in logical epoch 125
[2022-04-19 07:20:21] [data] Shuffling data
[2022-04-19 07:20:21] [data] Done reading 16,415 sentences
[2022-04-19 07:20:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:22:08] Ep. 125 : Up. 41000 : Sen. 5,852 : Cost 0.00782283 * 356,826 after 29,417,444 : Time 475.22s : 750.86 words/s
[2022-04-19 07:25:37] Seen 16415 samples
[2022-04-19 07:25:37] Starting data epoch 126 in logical epoch 126
[2022-04-19 07:25:37] [data] Shuffling data
[2022-04-19 07:25:37] [data] Done reading 16,415 sentences
[2022-04-19 07:25:37] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:30:08] Ep. 126 : Up. 41500 : Sen. 14,204 : Cost 0.00728250 * 359,586 after 29,777,030 : Time 480.13s : 748.94 words/s
[2022-04-19 07:30:51] Seen 16415 samples
[2022-04-19 07:30:51] Starting data epoch 127 in logical epoch 127
[2022-04-19 07:30:51] [data] Shuffling data
[2022-04-19 07:30:51] [data] Done reading 16,415 sentences
[2022-04-19 07:30:51] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:36:06] Seen 16415 samples
[2022-04-19 07:36:09] Starting data epoch 128 in logical epoch 128
[2022-04-19 07:36:09] [data] Shuffling data
[2022-04-19 07:36:09] [data] Done reading 16,415 sentences
[2022-04-19 07:36:09] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:38:10] Ep. 128 : Up. 42000 : Sen. 6,190 : Cost 0.00997623 * 357,446 after 30,134,476 : Time 481.25s : 742.74 words/s
[2022-04-19 07:41:25] Seen 16415 samples
[2022-04-19 07:41:25] Starting data epoch 129 in logical epoch 129
[2022-04-19 07:41:25] [data] Shuffling data
[2022-04-19 07:41:25] [data] Done reading 16,415 sentences
[2022-04-19 07:41:25] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:46:09] Ep. 129 : Up. 42500 : Sen. 14,503 : Cost 0.01050175 * 357,346 after 30,491,822 : Time 479.80s : 744.79 words/s
[2022-04-19 07:46:41] Seen 16415 samples
[2022-04-19 07:46:41] Starting data epoch 130 in logical epoch 130
[2022-04-19 07:46:41] [data] Shuffling data
[2022-04-19 07:46:41] [data] Done reading 16,415 sentences
[2022-04-19 07:46:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:51:55] Seen 16415 samples
[2022-04-19 07:51:56] Starting data epoch 131 in logical epoch 131
[2022-04-19 07:51:56] [data] Shuffling data
[2022-04-19 07:51:56] [data] Done reading 16,415 sentences
[2022-04-19 07:51:56] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 07:54:05] Ep. 131 : Up. 43000 : Sen. 6,710 : Cost 0.00569302 * 358,632 after 30,850,454 : Time 475.97s : 753.47 words/s
[2022-04-19 07:57:11] Seen 16415 samples
[2022-04-19 07:57:11] Starting data epoch 132 in logical epoch 132
[2022-04-19 07:57:11] [data] Shuffling data
[2022-04-19 07:57:11] [data] Done reading 16,415 sentences
[2022-04-19 07:57:11] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:02:02] Ep. 132 : Up. 43500 : Sen. 15,017 : Cost 0.00752387 * 358,714 after 31,209,168 : Time 476.47s : 752.86 words/s
[2022-04-19 08:02:27] Seen 16415 samples
[2022-04-19 08:02:27] Starting data epoch 133 in logical epoch 133
[2022-04-19 08:02:27] [data] Shuffling data
[2022-04-19 08:02:27] [data] Done reading 16,415 sentences
[2022-04-19 08:02:27] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:07:41] Seen 16415 samples
[2022-04-19 08:07:41] Starting data epoch 134 in logical epoch 134
[2022-04-19 08:07:41] [data] Shuffling data
[2022-04-19 08:07:41] [data] Done reading 16,415 sentences
[2022-04-19 08:07:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:10:00] Ep. 134 : Up. 44000 : Sen. 7,186 : Cost 0.01204873 * 358,683 after 31,567,851 : Time 478.36s : 749.82 words/s
[2022-04-19 08:12:56] Seen 16415 samples
[2022-04-19 08:12:56] Starting data epoch 135 in logical epoch 135
[2022-04-19 08:12:56] [data] Shuffling data
[2022-04-19 08:12:56] [data] Done reading 16,415 sentences
[2022-04-19 08:12:56] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:17:56] Ep. 135 : Up. 44500 : Sen. 15,718 : Cost 0.00346227 * 360,321 after 31,928,172 : Time 476.01s : 756.97 words/s
[2022-04-19 08:18:14] Seen 16415 samples
[2022-04-19 08:18:14] Starting data epoch 136 in logical epoch 136
[2022-04-19 08:18:14] [data] Shuffling data
[2022-04-19 08:18:14] [data] Done reading 16,415 sentences
[2022-04-19 08:18:14] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:23:28] Seen 16415 samples
[2022-04-19 08:23:28] Starting data epoch 137 in logical epoch 137
[2022-04-19 08:23:28] [data] Shuffling data
[2022-04-19 08:23:28] [data] Done reading 16,415 sentences
[2022-04-19 08:23:28] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:25:58] Ep. 137 : Up. 45000 : Sen. 7,866 : Cost 0.00833671 * 358,665 after 32,286,837 : Time 479.32s : 748.28 words/s
[2022-04-19 08:25:58] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 08:26:05] Saving model weights and runtime parameters to model.s2s-brmy/model.iter45000.npz
[2022-04-19 08:26:11] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 08:26:18] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 08:26:41] [valid] Ep. 137 : Up. 45000 : cross-entropy : 9.65798 : stalled 7 times (last best: 8.16755)
[2022-04-19 08:26:50] [valid] Ep. 137 : Up. 45000 : perplexity : 1.9455 : stalled 7 times (last best: 1.75561)
[2022-04-19 08:26:50] Translating validation set...
[2022-04-19 08:26:54] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 08:26:54] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 08:26:54] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ဝါ ) ။
[2022-04-19 08:26:54] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 08:26:54] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 08:26:54] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 08:26:54] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 08:26:54] Best translation 20 : မော မော့ မော် ။
[2022-04-19 08:26:54] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 08:26:54] Best translation 80 : ကျေး ခု တော့ ဖြင့် ဘီလူးမ လူရွယ် ကိုက် ထား သလို မျက်နှာ ကို လည်း တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 08:26:54] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 08:26:58] Best translation 320 : ရှေးဘဝ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 08:27:00] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 08:27:14] Best translation 1280 : စာအုပ်များ ကို တစ် မည် ကိုင် ကြ ပါ သည် ။
[2022-04-19 08:27:31] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 08:27:32] Total translation time: 42.10913s
[2022-04-19 08:27:32] [valid] Ep. 137 : Up. 45000 : bleu : 87.5217 : stalled 6 times (last best: 87.9496)
[2022-04-19 08:30:17] Seen 16415 samples
[2022-04-19 08:30:17] Starting data epoch 138 in logical epoch 138
[2022-04-19 08:30:17] [data] Shuffling data
[2022-04-19 08:30:17] [data] Done reading 16,415 sentences
[2022-04-19 08:30:17] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:35:30] Ep. 138 : Up. 45500 : Sen. 16,309 : Cost 0.01288649 * 358,961 after 32,645,798 : Time 571.90s : 627.66 words/s
[2022-04-19 08:35:33] Seen 16415 samples
[2022-04-19 08:35:33] Starting data epoch 139 in logical epoch 139
[2022-04-19 08:35:33] [data] Shuffling data
[2022-04-19 08:35:33] [data] Done reading 16,415 sentences
[2022-04-19 08:35:33] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:40:49] Seen 16415 samples
[2022-04-19 08:40:49] Starting data epoch 140 in logical epoch 140
[2022-04-19 08:40:49] [data] Shuffling data
[2022-04-19 08:40:49] [data] Done reading 16,415 sentences
[2022-04-19 08:40:49] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:43:30] Ep. 140 : Up. 46000 : Sen. 8,334 : Cost 0.00885615 * 358,498 after 33,004,296 : Time 479.97s : 746.92 words/s
[2022-04-19 08:46:03] Seen 16415 samples
[2022-04-19 08:46:03] Starting data epoch 141 in logical epoch 141
[2022-04-19 08:46:03] [data] Shuffling data
[2022-04-19 08:46:03] [data] Done reading 16,415 sentences
[2022-04-19 08:46:03] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:51:19] Seen 16415 samples
[2022-04-19 08:51:20] Starting data epoch 142 in logical epoch 142
[2022-04-19 08:51:20] [data] Shuffling data
[2022-04-19 08:51:20] [data] Done reading 16,415 sentences
[2022-04-19 08:51:20] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:51:25] Ep. 142 : Up. 46500 : Sen. 470 : Cost 0.01039035 * 357,400 after 33,361,696 : Time 474.92s : 752.54 words/s
[2022-04-19 08:56:36] Seen 16415 samples
[2022-04-19 08:56:37] Starting data epoch 143 in logical epoch 143
[2022-04-19 08:56:37] [data] Shuffling data
[2022-04-19 08:56:37] [data] Done reading 16,415 sentences
[2022-04-19 08:56:37] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 08:59:26] Ep. 143 : Up. 47000 : Sen. 8,862 : Cost 0.00496950 * 358,554 after 33,720,250 : Time 480.67s : 745.95 words/s
[2022-04-19 09:01:52] Seen 16415 samples
[2022-04-19 09:01:52] Starting data epoch 144 in logical epoch 144
[2022-04-19 09:01:52] [data] Shuffling data
[2022-04-19 09:01:52] [data] Done reading 16,415 sentences
[2022-04-19 09:01:52] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:07:08] Seen 16415 samples
[2022-04-19 09:07:08] Starting data epoch 145 in logical epoch 145
[2022-04-19 09:07:08] [data] Shuffling data
[2022-04-19 09:07:08] [data] Done reading 16,415 sentences
[2022-04-19 09:07:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:07:22] Ep. 145 : Up. 47500 : Sen. 814 : Cost 0.00667131 * 358,119 after 34,078,369 : Time 476.27s : 751.92 words/s
[2022-04-19 09:12:23] Seen 16415 samples
[2022-04-19 09:12:23] Starting data epoch 146 in logical epoch 146
[2022-04-19 09:12:23] [data] Shuffling data
[2022-04-19 09:12:23] [data] Done reading 16,415 sentences
[2022-04-19 09:12:23] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:15:24] Ep. 146 : Up. 48000 : Sen. 9,202 : Cost 0.01635033 * 358,987 after 34,437,356 : Time 481.76s : 745.16 words/s
[2022-04-19 09:17:38] Seen 16415 samples
[2022-04-19 09:17:38] Starting data epoch 147 in logical epoch 147
[2022-04-19 09:17:38] [data] Shuffling data
[2022-04-19 09:17:38] [data] Done reading 16,415 sentences
[2022-04-19 09:17:38] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:22:54] Seen 16415 samples
[2022-04-19 09:22:54] Starting data epoch 148 in logical epoch 148
[2022-04-19 09:22:54] [data] Shuffling data
[2022-04-19 09:22:54] [data] Done reading 16,415 sentences
[2022-04-19 09:22:54] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:23:19] Ep. 148 : Up. 48500 : Sen. 1,398 : Cost 0.04934620 * 359,058 after 34,796,414 : Time 474.97s : 755.96 words/s
[2022-04-19 09:28:10] Seen 16415 samples
[2022-04-19 09:28:10] Starting data epoch 149 in logical epoch 149
[2022-04-19 09:28:10] [data] Shuffling data
[2022-04-19 09:28:10] [data] Done reading 16,415 sentences
[2022-04-19 09:28:10] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:31:18] Ep. 149 : Up. 49000 : Sen. 9,650 : Cost 0.00485301 * 357,661 after 35,154,075 : Time 479.23s : 746.33 words/s
[2022-04-19 09:33:25] Seen 16415 samples
[2022-04-19 09:33:25] Starting data epoch 150 in logical epoch 150
[2022-04-19 09:33:25] [data] Shuffling data
[2022-04-19 09:33:25] [data] Done reading 16,415 sentences
[2022-04-19 09:33:25] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:38:42] Seen 16415 samples
[2022-04-19 09:38:42] Starting data epoch 151 in logical epoch 151
[2022-04-19 09:38:42] [data] Shuffling data
[2022-04-19 09:38:42] [data] Done reading 16,415 sentences
[2022-04-19 09:38:42] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:39:18] Ep. 151 : Up. 49500 : Sen. 1,556 : Cost 0.00863618 * 358,321 after 35,512,396 : Time 480.01s : 746.49 words/s
[2022-04-19 09:43:57] Seen 16415 samples
[2022-04-19 09:43:57] Starting data epoch 152 in logical epoch 152
[2022-04-19 09:43:57] [data] Shuffling data
[2022-04-19 09:43:57] [data] Done reading 16,415 sentences
[2022-04-19 09:43:58] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:47:18] Ep. 152 : Up. 50000 : Sen. 10,016 : Cost 0.00677686 * 359,496 after 35,871,892 : Time 479.77s : 749.30 words/s
[2022-04-19 09:47:18] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 09:47:24] Saving model weights and runtime parameters to model.s2s-brmy/model.iter50000.npz
[2022-04-19 09:47:30] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 09:47:37] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 09:48:01] [valid] Ep. 152 : Up. 50000 : cross-entropy : 9.77975 : stalled 8 times (last best: 8.16755)
[2022-04-19 09:48:10] [valid] Ep. 152 : Up. 50000 : perplexity : 1.9619 : stalled 8 times (last best: 1.75561)
[2022-04-19 09:48:10] Translating validation set...
[2022-04-19 09:48:14] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 09:48:14] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 09:48:14] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ဝါ ) ။
[2022-04-19 09:48:14] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 09:48:14] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 09:48:14] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 09:48:14] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 09:48:14] Best translation 20 : မော မော့ မော် ။
[2022-04-19 09:48:14] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 09:48:14] Best translation 80 : ကျေး ခု တော့ ဖြင့် ဘီလူးမ သမား ကိုက် ထား သလို မျက်နှာ ကို လည်း တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 09:48:14] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 09:48:18] Best translation 320 : မြေ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 09:48:19] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 09:48:34] Best translation 1280 : စာအုပ်များ ကို ထောင်း လေ့လာ ကိုင် ကြ ပါ သည် ။
[2022-04-19 09:48:51] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 09:48:52] Total translation time: 41.66643s
[2022-04-19 09:48:52] [valid] Ep. 152 : Up. 50000 : bleu : 87.5727 : stalled 7 times (last best: 87.9496)
[2022-04-19 09:50:48] Seen 16415 samples
[2022-04-19 09:50:48] Starting data epoch 153 in logical epoch 153
[2022-04-19 09:50:48] [data] Shuffling data
[2022-04-19 09:50:48] [data] Done reading 16,415 sentences
[2022-04-19 09:50:48] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:56:04] Seen 16415 samples
[2022-04-19 09:56:04] Starting data epoch 154 in logical epoch 154
[2022-04-19 09:56:04] [data] Shuffling data
[2022-04-19 09:56:04] [data] Done reading 16,415 sentences
[2022-04-19 09:56:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 09:56:48] Ep. 154 : Up. 50500 : Sen. 2,290 : Cost 0.01242262 * 357,085 after 36,228,977 : Time 570.24s : 626.20 words/s
[2022-04-19 10:01:18] Seen 16415 samples
[2022-04-19 10:01:18] Starting data epoch 155 in logical epoch 155
[2022-04-19 10:01:18] [data] Shuffling data
[2022-04-19 10:01:18] [data] Done reading 16,415 sentences
[2022-04-19 10:01:19] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:04:47] Ep. 155 : Up. 51000 : Sen. 10,612 : Cost 0.00826027 * 359,406 after 36,588,383 : Time 479.23s : 749.97 words/s
[2022-04-19 10:06:32] Seen 16415 samples
[2022-04-19 10:06:32] Starting data epoch 156 in logical epoch 156
[2022-04-19 10:06:32] [data] Shuffling data
[2022-04-19 10:06:32] [data] Done reading 16,415 sentences
[2022-04-19 10:06:32] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:11:47] Seen 16415 samples
[2022-04-19 10:11:47] Starting data epoch 157 in logical epoch 157
[2022-04-19 10:11:47] [data] Shuffling data
[2022-04-19 10:11:47] [data] Done reading 16,415 sentences
[2022-04-19 10:11:47] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:12:38] Ep. 157 : Up. 51500 : Sen. 3,038 : Cost 0.00921857 * 357,117 after 36,945,500 : Time 470.47s : 759.07 words/s
[2022-04-19 10:17:03] Seen 16415 samples
[2022-04-19 10:17:03] Starting data epoch 158 in logical epoch 158
[2022-04-19 10:17:03] [data] Shuffling data
[2022-04-19 10:17:03] [data] Done reading 16,415 sentences
[2022-04-19 10:17:03] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:20:38] Ep. 158 : Up. 52000 : Sen. 11,398 : Cost 0.00709909 * 359,029 after 37,304,529 : Time 480.30s : 747.52 words/s
[2022-04-19 10:22:18] Seen 16415 samples
[2022-04-19 10:22:18] Starting data epoch 159 in logical epoch 159
[2022-04-19 10:22:18] [data] Shuffling data
[2022-04-19 10:22:18] [data] Done reading 16,415 sentences
[2022-04-19 10:22:18] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:27:33] Seen 16415 samples
[2022-04-19 10:27:33] Starting data epoch 160 in logical epoch 160
[2022-04-19 10:27:33] [data] Shuffling data
[2022-04-19 10:27:33] [data] Done reading 16,415 sentences
[2022-04-19 10:27:33] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:28:36] Ep. 160 : Up. 52500 : Sen. 3,358 : Cost 0.00349240 * 359,773 after 37,664,302 : Time 478.00s : 752.66 words/s
[2022-04-19 10:32:49] Seen 16415 samples
[2022-04-19 10:32:49] Starting data epoch 161 in logical epoch 161
[2022-04-19 10:32:49] [data] Shuffling data
[2022-04-19 10:32:49] [data] Done reading 16,415 sentences
[2022-04-19 10:32:49] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:36:29] Ep. 161 : Up. 53000 : Sen. 12,000 : Cost 0.00649655 * 356,745 after 38,021,047 : Time 472.73s : 754.65 words/s
[2022-04-19 10:38:04] Seen 16415 samples
[2022-04-19 10:38:04] Starting data epoch 162 in logical epoch 162
[2022-04-19 10:38:04] [data] Shuffling data
[2022-04-19 10:38:04] [data] Done reading 16,415 sentences
[2022-04-19 10:38:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:43:19] Seen 16415 samples
[2022-04-19 10:43:19] Starting data epoch 163 in logical epoch 163
[2022-04-19 10:43:19] [data] Shuffling data
[2022-04-19 10:43:19] [data] Done reading 16,415 sentences
[2022-04-19 10:43:19] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:44:32] Ep. 163 : Up. 53500 : Sen. 3,916 : Cost 0.00893078 * 360,306 after 38,381,353 : Time 483.31s : 745.49 words/s
[2022-04-19 10:48:34] Seen 16415 samples
[2022-04-19 10:48:34] Starting data epoch 164 in logical epoch 164
[2022-04-19 10:48:34] [data] Shuffling data
[2022-04-19 10:48:34] [data] Done reading 16,415 sentences
[2022-04-19 10:48:35] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:52:31] Ep. 164 : Up. 54000 : Sen. 12,362 : Cost 0.00788511 * 358,468 after 38,739,821 : Time 478.48s : 749.18 words/s
[2022-04-19 10:53:49] Seen 16415 samples
[2022-04-19 10:53:49] Starting data epoch 165 in logical epoch 165
[2022-04-19 10:53:49] [data] Shuffling data
[2022-04-19 10:53:49] [data] Done reading 16,415 sentences
[2022-04-19 10:53:49] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 10:59:04] Seen 16415 samples
[2022-04-19 10:59:04] Starting data epoch 166 in logical epoch 166
[2022-04-19 10:59:04] [data] Shuffling data
[2022-04-19 10:59:04] [data] Done reading 16,415 sentences
[2022-04-19 10:59:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:00:28] Ep. 166 : Up. 54500 : Sen. 4,560 : Cost 0.00846430 * 356,506 after 39,096,327 : Time 477.48s : 746.64 words/s
[2022-04-19 11:04:18] Seen 16415 samples
[2022-04-19 11:04:18] Starting data epoch 167 in logical epoch 167
[2022-04-19 11:04:18] [data] Shuffling data
[2022-04-19 11:04:18] [data] Done reading 16,415 sentences
[2022-04-19 11:04:18] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:08:25] Ep. 167 : Up. 55000 : Sen. 12,898 : Cost 0.00435004 * 361,156 after 39,457,483 : Time 476.45s : 758.02 words/s
[2022-04-19 11:08:25] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 11:08:34] Saving model weights and runtime parameters to model.s2s-brmy/model.iter55000.npz
[2022-04-19 11:08:40] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 11:08:47] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 11:09:10] [valid] Ep. 167 : Up. 55000 : cross-entropy : 9.80487 : stalled 9 times (last best: 8.16755)
[2022-04-19 11:09:20] [valid] Ep. 167 : Up. 55000 : perplexity : 1.9653 : stalled 9 times (last best: 1.75561)
[2022-04-19 11:09:20] Translating validation set...
[2022-04-19 11:09:23] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 11:09:24] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 11:09:24] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ဝါ ) ။
[2022-04-19 11:09:24] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 11:09:24] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 11:09:24] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 11:09:24] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 11:09:24] Best translation 20 : မော မော့ မော် ။
[2022-04-19 11:09:24] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 11:09:24] Best translation 80 : ကျေး ခု တော့ ဖြင့် ဘီလူးမ သမား ကိုက် ထား သလို မျက်နှာ ကို လည်း တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 11:09:24] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 11:09:28] Best translation 320 : မြေ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 11:09:30] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 11:09:42] Best translation 1280 : စာအုပ်များ ကို တစ် မည် ကိုင် ကြ ပါ သည် ။
[2022-04-19 11:09:59] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 11:10:00] Total translation time: 39.94498s
[2022-04-19 11:10:00] [valid] Ep. 167 : Up. 55000 : bleu : 88.392 : new best
[2022-04-19 11:11:08] Seen 16415 samples
[2022-04-19 11:11:08] Starting data epoch 168 in logical epoch 168
[2022-04-19 11:11:08] [data] Shuffling data
[2022-04-19 11:11:09] [data] Done reading 16,415 sentences
[2022-04-19 11:11:09] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:16:24] Seen 16415 samples
[2022-04-19 11:16:24] Starting data epoch 169 in logical epoch 169
[2022-04-19 11:16:24] [data] Shuffling data
[2022-04-19 11:16:24] [data] Done reading 16,415 sentences
[2022-04-19 11:16:24] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:18:01] Ep. 169 : Up. 55500 : Sen. 4,858 : Cost 0.00332597 * 358,522 after 39,816,005 : Time 576.42s : 621.98 words/s
[2022-04-19 11:21:38] Seen 16415 samples
[2022-04-19 11:21:38] Starting data epoch 170 in logical epoch 170
[2022-04-19 11:21:38] [data] Shuffling data
[2022-04-19 11:21:38] [data] Done reading 16,415 sentences
[2022-04-19 11:21:38] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:25:57] Ep. 170 : Up. 56000 : Sen. 13,524 : Cost 0.00275971 * 360,517 after 40,176,522 : Time 476.18s : 757.10 words/s
[2022-04-19 11:26:53] Seen 16415 samples
[2022-04-19 11:26:53] Starting data epoch 171 in logical epoch 171
[2022-04-19 11:26:53] [data] Shuffling data
[2022-04-19 11:26:53] [data] Done reading 16,415 sentences
[2022-04-19 11:26:53] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:32:08] Seen 16415 samples
[2022-04-19 11:32:08] Starting data epoch 172 in logical epoch 172
[2022-04-19 11:32:08] [data] Shuffling data
[2022-04-19 11:32:08] [data] Done reading 16,415 sentences
[2022-04-19 11:32:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:33:55] Ep. 172 : Up. 56500 : Sen. 5,504 : Cost 0.00936100 * 357,520 after 40,534,042 : Time 477.60s : 748.58 words/s
[2022-04-19 11:37:22] Seen 16415 samples
[2022-04-19 11:37:22] Starting data epoch 173 in logical epoch 173
[2022-04-19 11:37:22] [data] Shuffling data
[2022-04-19 11:37:22] [data] Done reading 16,415 sentences
[2022-04-19 11:37:22] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:41:49] Ep. 173 : Up. 57000 : Sen. 14,164 : Cost 0.00497883 * 359,731 after 40,893,773 : Time 474.42s : 758.25 words/s
[2022-04-19 11:42:36] Seen 16415 samples
[2022-04-19 11:42:36] Starting data epoch 174 in logical epoch 174
[2022-04-19 11:42:36] [data] Shuffling data
[2022-04-19 11:42:36] [data] Done reading 16,415 sentences
[2022-04-19 11:42:36] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:47:51] Seen 16415 samples
[2022-04-19 11:47:51] Starting data epoch 175 in logical epoch 175
[2022-04-19 11:47:51] [data] Shuffling data
[2022-04-19 11:47:51] [data] Done reading 16,415 sentences
[2022-04-19 11:47:51] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:49:47] Ep. 175 : Up. 57500 : Sen. 6,246 : Cost 0.01125178 * 358,639 after 41,252,412 : Time 477.86s : 750.52 words/s
[2022-04-19 11:53:06] Seen 16415 samples
[2022-04-19 11:53:06] Starting data epoch 176 in logical epoch 176
[2022-04-19 11:53:06] [data] Shuffling data
[2022-04-19 11:53:06] [data] Done reading 16,415 sentences
[2022-04-19 11:53:06] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 11:57:46] Ep. 176 : Up. 58000 : Sen. 14,521 : Cost 0.00786911 * 357,086 after 41,609,498 : Time 479.14s : 745.26 words/s
[2022-04-19 11:58:21] Seen 16415 samples
[2022-04-19 11:58:21] Starting data epoch 177 in logical epoch 177
[2022-04-19 11:58:21] [data] Shuffling data
[2022-04-19 11:58:21] [data] Done reading 16,415 sentences
[2022-04-19 11:58:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:03:37] Seen 16415 samples
[2022-04-19 12:03:39] Starting data epoch 178 in logical epoch 178
[2022-04-19 12:03:39] [data] Shuffling data
[2022-04-19 12:03:39] [data] Done reading 16,415 sentences
[2022-04-19 12:03:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:05:46] Ep. 178 : Up. 58500 : Sen. 6,674 : Cost 0.00946860 * 360,029 after 41,969,527 : Time 479.93s : 750.18 words/s
[2022-04-19 12:08:53] Seen 16415 samples
[2022-04-19 12:08:53] Starting data epoch 179 in logical epoch 179
[2022-04-19 12:08:53] [data] Shuffling data
[2022-04-19 12:08:53] [data] Done reading 16,415 sentences
[2022-04-19 12:08:53] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:13:42] Ep. 179 : Up. 59000 : Sen. 15,302 : Cost 0.00533194 * 359,372 after 42,328,899 : Time 475.33s : 756.04 words/s
[2022-04-19 12:14:08] Seen 16415 samples
[2022-04-19 12:14:08] Starting data epoch 180 in logical epoch 180
[2022-04-19 12:14:08] [data] Shuffling data
[2022-04-19 12:14:08] [data] Done reading 16,415 sentences
[2022-04-19 12:14:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:19:24] Seen 16415 samples
[2022-04-19 12:19:24] Starting data epoch 181 in logical epoch 181
[2022-04-19 12:19:24] [data] Shuffling data
[2022-04-19 12:19:24] [data] Done reading 16,415 sentences
[2022-04-19 12:19:24] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:21:38] Ep. 181 : Up. 59500 : Sen. 7,286 : Cost 0.00724726 * 356,179 after 42,685,078 : Time 476.08s : 748.15 words/s
[2022-04-19 12:24:39] Seen 16415 samples
[2022-04-19 12:24:39] Starting data epoch 182 in logical epoch 182
[2022-04-19 12:24:39] [data] Shuffling data
[2022-04-19 12:24:39] [data] Done reading 16,415 sentences
[2022-04-19 12:24:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-19 12:29:39] Ep. 182 : Up. 60000 : Sen. 15,636 : Cost 0.00466096 * 360,063 after 43,045,141 : Time 481.24s : 748.20 words/s
[2022-04-19 12:29:39] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 12:29:48] Saving model weights and runtime parameters to model.s2s-brmy/model.iter60000.npz
[2022-04-19 12:29:54] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 12:30:02] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz
[2022-04-19 12:30:26] [valid] Ep. 182 : Up. 60000 : cross-entropy : 9.86535 : stalled 10 times (last best: 8.16755)
[2022-04-19 12:30:35] [valid] Ep. 182 : Up. 60000 : perplexity : 1.9735 : stalled 10 times (last best: 1.75561)
[2022-04-19 12:30:35] Translating validation set...
[2022-04-19 12:30:39] Best translation 0 : ၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 12:30:39] Best translation 1 : ( ခ ) ယုန် နှင့် လိပ် ။
[2022-04-19 12:30:39] Best translation 2 : ဂျပန် နိုင်ငံ ပညာ ( ဝါ ) ။
[2022-04-19 12:30:39] Best translation 3 : ( က ) ပုဂံ မြို့ သည် ညောင်ဦး မြို့နယ် ဧရာဝတီ မြစ် ------ ပေါ် တွင် ရှိ သည် ။ ( ကမ်း ၊ ကမ်း ) ။
[2022-04-19 12:30:39] Best translation 4 : ဒါပေမဲ့ အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
[2022-04-19 12:30:39] Best translation 5 : လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
[2022-04-19 12:30:39] Best translation 10 : ရေသည် ယောက်ျား အိမ်ရှေ့ မင်း ဖြစ် ပြီးနောက် ဥယျာဉ် တော် တွင် မင်းကြီး နှင့်အတူ ရှိ စဉ် အိပ်ပျော် နေ သော မင်းကြီး ကို သတ်၍ ထီးနန်း ယူ ရန် သုံး ကြိမ် ကြံစည် သည် ။
[2022-04-19 12:30:39] Best translation 20 : မော မော့ မော် ။
[2022-04-19 12:30:39] Best translation 40 : ထည့်လိုက် မလား ကွဲ့ သား မောင် ကို ။
[2022-04-19 12:30:39] Best translation 80 : အက် ခု တော့ ဖြင့် ဘီလူးမ သမား ကိုက် ထား သလို မျက်နှာ ကို ကဗျာ တွန့် နေ တာ ပဲ ဟူ၍ ဖြစ် ပါ သတည်း ။
[2022-04-19 12:30:39] Best translation 160 : အဆုံးသတ် ။
[2022-04-19 12:30:43] Best translation 320 : မြေ က သူ ပြန် ပုံ မှာ ။
[2022-04-19 12:30:45] Best translation 640 : အိုး ကလေး နှစ် လုံး မှာ တစ် လုံး က တော့ အိုး ကောင်း ကလေး ဖြစ် ပေမဲ့ နောက် တစ် လုံး က တော့ အောက်ခြေ မှာ လျက် နေ သ တဲ့ ။
[2022-04-19 12:30:59] Best translation 1280 : စာအုပ်များ ကို တစ် မည် ကိုင် ကြ ပါ သည် ။
[2022-04-19 12:31:15] Best translation 2560 : လုလင် သည် မိမိ အစွမ်း ကို ရွာ ၌ ရှေးဦးစွာ ပြ ၏ ။
[2022-04-19 12:31:16] Total translation time: 41.00232s
[2022-04-19 12:31:16] [valid] Ep. 182 : Up. 60000 : bleu : 87.5398 : stalled 1 times (last best: 88.392)
[2022-04-19 12:31:17] Training finished
[2022-04-19 12:31:19] Saving model weights and runtime parameters to model.s2s-brmy/model.npz.orig.npz
[2022-04-19 12:31:25] Saving model weights and runtime parameters to model.s2s-brmy/model.npz
[2022-04-19 12:31:32] Saving Adam parameters to model.s2s-brmy/model.npz.optimizer.npz

real	981m47.784s
user	1645m44.319s
sys	1m58.244s
```

output model တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-mybr$ cd ../model.s2s-brmy/
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-brmy$ ls
config.yml           model.iter25000.npz  model.iter45000.npz  model.iter60000.npz      model.npz.orig.npz              train.log
model.iter10000.npz  model.iter30000.npz  model.iter50000.npz  model.npz                model.npz.orig.npz.decoder.yml  valid.log
model.iter15000.npz  model.iter35000.npz  model.iter5000.npz   model.npz.decoder.yml    model.npz.progress.yml
model.iter20000.npz  model.iter40000.npz  model.iter55000.npz  model.npz.optimizer.npz  model.npz.yml
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-brmy$ ls *.npz | sort -V
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
model.npz
model.npz.optimizer.npz
model.npz.orig.npz
(base) ye@:/media/ye/project2/exp/braille-nmt/model.s2s-brmy$
```

## Testing/Evaluation for Seq2Seq br-my

bash script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung, MuHaung-Myanmar
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Seq2Seq Model for my-br
## 19 April 2022
# model.iter5000.npz

for i in {5000..60000..5000}
do
   marian-decoder -m ./model.iter$i.npz -v  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter$i.my < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br
   echo "Evaluation with hyp.iter$i.br, Seq2Seq Model, br-my:" >> test-seq2seq-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./hyp.iter$i.my  >> test-seq2seq-results.txt
done
```

testing/evaluation for seq2seq br-my direction ...  

```

```
