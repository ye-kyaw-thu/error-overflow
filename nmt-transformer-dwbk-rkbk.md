# NMT Transformer dw-bk, rk-bk Baselines

Preparing baseline with Transformer architecture for dw-bk, rk-bk language pairs.  

y@CADT, Cambodia  
5 June 2022  

## bk-dw, Word Unit, Transformer Archi

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 5 June 2022


model_folder="model.transformer.bkdw.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="bk"; tgt="dw";

marian \
    --model ${model_folder}/model.npz --type transformer \
    --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
    --max-length 200 \
    --vocabs ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
    --valid-translation-output ${model_folder}/valid.${src}-${tgt}.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > ${model_folder}/${src}-${tgt}.config.yml

time marian -c ${model_folder}/${src}-${tgt}.config.yml  2>&1 | tee ${model_folder}/transformer-${src}-${tgt}.log
```

training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./transformer.bkdw.sh
...
...
...
[2022-06-05 12:50:37] Seen 5,452 samples
[2022-06-05 12:50:37] Starting data epoch 3925 in logical epoch 3925
[2022-06-05 12:50:37] [data] Shuffling data
[2022-06-05 12:50:37] [data] Done reading 5,452 sentences
[2022-06-05 12:50:37] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 12:50:39] Seen 5,452 samples
[2022-06-05 12:50:39] Starting data epoch 3926 in logical epoch 3926
[2022-06-05 12:50:39] [data] Shuffling data
[2022-06-05 12:50:39] [data] Done reading 5,452 sentences
[2022-06-05 12:50:39] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 12:50:40] Seen 5,452 samples
[2022-06-05 12:50:40] Starting data epoch 3927 in logical epoch 3927
[2022-06-05 12:50:40] [data] Shuffling data
[2022-06-05 12:50:40] [data] Done reading 5,452 sentences
[2022-06-05 12:50:40] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 12:50:41] Seen 5,452 samples
[2022-06-05 12:50:41] Starting data epoch 3928 in logical epoch 3928
[2022-06-05 12:50:41] [data] Shuffling data
[2022-06-05 12:50:41] [data] Done reading 5,452 sentences
[2022-06-05 12:50:42] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 12:50:43] Seen 5,452 samples
[2022-06-05 12:50:43] Starting data epoch 3929 in logical epoch 3929
[2022-06-05 12:50:43] [data] Shuffling data
[2022-06-05 12:50:43] [data] Done reading 5,452 sentences
[2022-06-05 12:50:43] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 12:50:44] Ep. 3929 : Up. 55000 : Sen. 3,580 : Cost 1.24684238 * 1,363,470 @ 4,088 after 149,547,454 : Time 52.07s : 26184.43 words/s : gNorm 0.0727 : L.r. 1.6181e-04
[2022-06-05 12:50:44] Saving model weights and runtime parameters to model.transformer.bkdw.1/model.iter55000.npz
[2022-06-05 12:50:44] Saving model weights and runtime parameters to model.transformer.bkdw.1/model.npz
[2022-06-05 12:50:45] Saving Adam parameters
[2022-06-05 12:50:45] [training] Saving training checkpoint to model.transformer.bkdw.1/model.npz and model.transformer.bkdw.1/model.npz.optimizer.npz
[2022-06-05 12:50:48] [valid] Ep. 3929 : Up. 55000 : cross-entropy : 33.0172 : stalled 10 times (last best: 29.1508)
[2022-06-05 12:50:48] [valid] Ep. 3929 : Up. 55000 : perplexity : 107.127 : stalled 10 times (last best: 61.9716)
[2022-06-05 12:50:48] [valid] Ep. 3929 : Up. 55000 : bleu : 15.8054 : stalled 9 times (last best: 17.332)
[2022-06-05 12:50:48] Training finished
[2022-06-05 12:50:48] Saving model weights and runtime parameters to model.transformer.bkdw.1/model.npz
[2022-06-05 12:50:49] Saving Adam parameters
[2022-06-05 12:50:49] [training] Saving training checkpoint to model.transformer.bkdw.1/model.npz and model.transformer.bkdw.1/model.npz.optimizer.npz

real    96m6.325s
user    116m9.763s
sys     2m9.870s
```

check the model folders:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkdw.1$ ls *.npz | sort -V
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
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkdw.1$
```

test-eval script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="bk"; tgt="dw";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing/evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkdw.1$ time ./test-eval.sh
...
...
...
[2022-06-05 13:49:35] Best translation 636 : အဲမှာ ကင်းစာ ဟှှိုး အဲမှာ ဒေဟှှို ။
[2022-06-05 13:49:35] Best translation 637 : သူးနနိနို့ ဟှယ်သသူ့ ဝမ် ကေ့ဟှလား ။
[2022-06-05 13:49:35] Best translation 638 : ဟှယ်လူလေ အိ နေကေ့နူး ။
[2022-06-05 13:49:35] Best translation 639 : နန် ဂါး ပြော နေဇာ ။
[2022-06-05 13:49:35] Best translation 640 : သူ အအဲ့ဇာဝဝို ဆဆုံးဖြတ် ခခဲ့ရယ် ။
[2022-06-05 13:49:35] Best translation 641 : ငါ့ နား မှာ ပျော် လား ။
[2022-06-05 13:49:35] Best translation 642 : ငါ့ ဟှှို လလုံးဝ သစ္စာ ဖွတ်ဟှ ။
[2022-06-05 13:49:35] Best translation 643 : နန် ဂတိမပျက် ဟှ ။
[2022-06-05 13:49:35] Best translation 644 : ခန်ဗျား အအဲ့မာ ဟှှို ကေ့ ပါအူး ။
[2022-06-05 13:49:35] Best translation 645 : ခွပ်ပွတ် ဖွမ့် ဟှာ စိဆဆိုး ဟှှိှို့လား ။
[2022-06-05 13:49:35] Best translation 646 : မှန်ပေါ့ ။
[2022-06-05 13:49:35] Best translation 647 : နန် ဟှဲ လောက် လောက် ဟှားဟှယ် ။
[2022-06-05 13:49:35] Best translation 648 : ကျွန်တော်ဝဝိဝို့ အအဲ့ဇာဝဝို ကာကွယ် ဝဝိဝို့လား ။
[2022-06-05 13:49:35] Best translation 649 : နန် သတ်မွီးဝမ်းကြောင်း ဟှ ရှားနူး ။
[2022-06-05 13:49:35] Best translation 650 : နန် သတ်မွီးဝမ်းကြောင်း ဟှ ရှားနူး ။
[2022-06-05 13:49:35] Best translation 651 : ခန်ဗျား ဟှှို ရေ ဟှာ ကြြိုက် ဟှ ။
[2022-06-05 13:49:35] Best translation 652 : ကျွန်တော်ဟှားဒေ အဲမှာ ဟှှို ဖိဟှား ကေ့ဟှ ။
[2022-06-05 13:49:35] Best translation 653 : ငါ့တူ တူမ လေ ဟှှို မျှော်လင့် ဟှယ် ။
[2022-06-05 13:49:35] Best translation 654 : နန် ဒုက္ခ ရောက် လလီ့မယ် ။
[2022-06-05 13:49:35] Best translation 655 : ကျွန်တော် စစိုးရီသလော့ ခြေနေ ကော ဟှယ် ။
[2022-06-05 13:49:35] Best translation 656 : ကျွန်တော် စစိုးရီသလော့ ခြေနေ ကော ဟှယ် ။
[2022-06-05 13:49:35] Best translation 657 : ဟှယ်ဒဒူ့ လွှန်အီ နူး ။
[2022-06-05 13:49:35] Best translation 658 : နန် သသူ့ဟှှို မူး ဟှလား ။
[2022-06-05 13:49:35] Best translation 659 : နန့် မေ ဟှ ဟှယ်လူ လေ နူး ။
[2022-06-05 13:49:35] Best translation 660 : ဟှယ်လူလေ ဟှှို မေး ကေ့နူး ။
[2022-06-05 13:49:35] Best translation 661 : အဲဝယ်ဟှား ငယ်ဂျင်း ဟှှို လလိုရှင် ဟှယ် ။
[2022-06-05 13:49:35] Best translation 662 : ဟှယ်လော့ စိလှုပ်ရှား ဟှယ် ။
[2022-06-05 13:49:35] Best translation 663 : နန် ငါ့ ဟှှို ရှင်း ပြ ပါလား ။
[2022-06-05 13:49:35] Best translation 664 : အဲဟှှို သွား ဟှှိှို့ ငါ နန့် ဟှှို ငါ တတိုက်တွန်း ဟှ ။
[2022-06-05 13:49:35] Best translation 665 : နန် ခရီး ထွပ် ဟှလား ။
[2022-06-05 13:49:35] Best translation 666 : သူးနနိနို့ ဟှယ်လော့ ရဲရင့် ဟှယ် ။
[2022-06-05 13:49:35] Best translation 667 : အယ် စားသော့-က့့််ဆဆိုက်ဟှ ညညံ့ဇ ။
[2022-06-05 13:49:35] Best translation 668 : အယ် စားသော့-က့့််ဆဆိုက်ဟှ ညညံ့ဇ ။
[2022-06-05 13:49:35] Best translation 669 : အဲဝယ်ဟှားဟှှို ယူ လလိုက်လား ။
[2022-06-05 13:49:35] Total time: 3.99209s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    0m50.488s
user    1m18.157s
sys     0m12.283s
```

results are as follows ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkdw.1$ cat eval-result.txt
Evaluation with hyp.iter5000.dw, Transformer model:
BLEU = 19.95, 51.7/24.5/16.0/12.2 (BP=0.895, ratio=0.901, hyp_len=3614, ref_len=4013)
Evaluation with hyp.iter10000.dw, Transformer model:
BLEU = 19.57, 51.4/24.3/15.9/12.0 (BP=0.887, ratio=0.893, hyp_len=3582, ref_len=4013)
Evaluation with hyp.iter15000.dw, Transformer model:
BLEU = 19.14, 50.2/23.3/15.3/11.4 (BP=0.900, ratio=0.905, hyp_len=3632, ref_len=4013)
Evaluation with hyp.iter20000.dw, Transformer model:
BLEU = 19.00, 50.4/22.9/15.3/11.3 (BP=0.898, ratio=0.903, hyp_len=3625, ref_len=4013)
Evaluation with hyp.iter25000.dw, Transformer model:
BLEU = 18.86, 49.8/22.7/15.1/11.3 (BP=0.900, ratio=0.905, hyp_len=3630, ref_len=4013)
Evaluation with hyp.iter30000.dw, Transformer model:
BLEU = 18.88, 49.4/22.9/14.8/10.7 (BP=0.918, ratio=0.921, hyp_len=3695, ref_len=4013)
Evaluation with hyp.iter35000.dw, Transformer model:
BLEU = 19.31, 49.4/23.1/15.3/11.2 (BP=0.917, ratio=0.921, hyp_len=3694, ref_len=4013)
Evaluation with hyp.iter40000.dw, Transformer model:
BLEU = 19.30, 49.4/23.2/15.3/11.2 (BP=0.918, ratio=0.921, hyp_len=3697, ref_len=4013)
Evaluation with hyp.iter45000.dw, Transformer model:
BLEU = 19.53, 49.6/23.4/15.6/11.6 (BP=0.912, ratio=0.916, hyp_len=3675, ref_len=4013)
Evaluation with hyp.iter50000.dw, Transformer model:
BLEU = 19.21, 49.5/23.3/15.3/11.1 (BP=0.913, ratio=0.916, hyp_len=3677, ref_len=4013)
Evaluation with hyp.iter55000.dw, Transformer model:
BLEU = 19.15, 49.8/23.2/15.2/11.2 (BP=0.910, ratio=0.914, hyp_len=3666, ref_len=4013)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkdw.1$
```

**The Best BLEU Score for bk-dw, Word Unit, Transformer Archi is 19.95.**  

## bk-dw, Word Unit, Transformer Archi

training script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 5 June 2022


model_folder="model.transformer.dwbk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="dw"; tgt="bk";

marian \
    --model ${model_folder}/model.npz --type transformer \
    --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
    --max-length 200 \
    --vocabs ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
    --valid-translation-output ${model_folder}/valid.${src}-${tgt}.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > ${model_folder}/${src}-${tgt}.config.yml

time marian -c ${model_folder}/${src}-${tgt}.config.yml  2>&1 | tee ${model_folder}/transformer-${src}-${tgt}.log
```

training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./transformer.dwbk.sh
...
...
...
[2022-06-05 15:35:42] Seen 5,452 samples
[2022-06-05 15:35:42] Starting data epoch 3663 in logical epoch 3663
[2022-06-05 15:35:42] [data] Shuffling data
[2022-06-05 15:35:42] [data] Done reading 5,452 sentences
[2022-06-05 15:35:42] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 15:35:44] Seen 5,452 samples
[2022-06-05 15:35:44] Starting data epoch 3664 in logical epoch 3664
[2022-06-05 15:35:44] [data] Shuffling data
[2022-06-05 15:35:44] [data] Done reading 5,452 sentences
[2022-06-05 15:35:44] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 15:35:45] Seen 5,452 samples
[2022-06-05 15:35:45] Starting data epoch 3665 in logical epoch 3665
[2022-06-05 15:35:45] [data] Shuffling data
[2022-06-05 15:35:45] [data] Done reading 5,452 sentences
[2022-06-05 15:35:45] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 15:35:47] Seen 5,452 samples
[2022-06-05 15:35:47] Starting data epoch 3666 in logical epoch 3666
[2022-06-05 15:35:47] [data] Shuffling data
[2022-06-05 15:35:47] [data] Done reading 5,452 sentences
[2022-06-05 15:35:47] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 15:35:48] Seen 5,452 samples
[2022-06-05 15:35:48] Starting data epoch 3667 in logical epoch 3667
[2022-06-05 15:35:48] [data] Shuffling data
[2022-06-05 15:35:48] [data] Done reading 5,452 sentences
[2022-06-05 15:35:48] [data] Done shuffling 5,452 sentences to temp files
[2022-06-05 15:35:49] Ep. 3667 : Up. 55000 : Sen. 3,332 : Cost 1.20016611 * 1,325,243 @ 452 after 146,388,795 : Time 50.43s : 26281.21 words/s : gNorm 0.1497 : L.r. 1.6181e-04
[2022-06-05 15:35:49] Saving model weights and runtime parameters to model.transformer.dwbk.1/model.iter55000.npz
[2022-06-05 15:35:49] Saving model weights and runtime parameters to model.transformer.dwbk.1/model.npz
[2022-06-05 15:35:50] Saving Adam parameters
[2022-06-05 15:35:50] [training] Saving training checkpoint to model.transformer.dwbk.1/model.npz and model.transformer.dwbk.1/model.npz.optimizer.npz
[2022-06-05 15:35:53] [valid] Ep. 3667 : Up. 55000 : cross-entropy : 34.3566 : stalled 10 times (last best: 29.5591)
[2022-06-05 15:35:53] [valid] Ep. 3667 : Up. 55000 : perplexity : 102.159 : stalled 10 times (last best: 53.5433)
[2022-06-05 15:35:53] [valid] Ep. 3667 : Up. 55000 : bleu : 17.3745 : stalled 8 times (last best: 18.3092)
[2022-06-05 15:35:53] Training finished
[2022-06-05 15:35:53] Saving model weights and runtime parameters to model.transformer.dwbk.1/model.npz
[2022-06-05 15:35:54] Saving Adam parameters
[2022-06-05 15:35:54] [training] Saving training checkpoint to model.transformer.dwbk.1/model.npz and model.transformer.dwbk.1/model.npz.optimizer.npz

real    93m26.098s
user    112m8.491s
sys     2m1.018s
```

check the models ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.dwbk.1$ ls *.npz | sort -V
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
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.dwbk.1$
```

testing/evaluation ...  

```
[2022-06-05 16:12:08] Best translation 636 : လေးစားစရာ ကောင်း ပါ ။
[2022-06-05 16:12:08] Best translation 637 : ဒါကြောင့် ရေလမ်း က ဝင် နေရယ် ။
[2022-06-05 16:12:08] Best translation 638 : ဖယ်သူလေ စိတ်နှောင့်ယှက်ပေး ရိလဲ ။
[2022-06-05 16:12:08] Best translation 639 : မင်း စကား ပြော နေစာ ။
[2022-06-05 16:12:08] Best translation 640 : သူ ဒယ်စာ ဝဝို ဆဆုံးဖြတ် ခခဲ့ဟယ် ။
[2022-06-05 16:12:08] Best translation 641 : ငါ့ နား နေ့ဒဒိုင်း ပျော် လား ။
[2022-06-05 16:12:08] Best translation 642 : ငါ့ ဝဝို ယယုံ တတဲ့ သူ ဒေ ဂဂို ဘယ်ခါမှ သစ္စာ မ ဖောက် ရ ။
[2022-06-05 16:12:08] Best translation 643 : မင့် ဘာကြောင့် ဘာမှမပြောမိလလိုက်ပါလိမ့် ။
[2022-06-05 16:12:08] Best translation 644 : ခင်ဗျား ဒယ် အကြောင်း ဝဝို စဉ်းစား နေရယ် ။
[2022-06-05 16:12:09] Best translation 645 : တံခါးပေါက် ဖွင့် ရင် စိတ်ဆဆိုး နေလား ။
[2022-06-05 16:12:09] Best translation 646 : စိတ်မပေါက် က ဆဆို ။
[2022-06-05 16:12:09] Best translation 647 : နင် ဘာ ဇာ လုပ် ။
[2022-06-05 16:12:09] Best translation 648 : ကျွန်တော်လလိလို့ ဒယ်စာ ဝဝို ကာကွယ် ကြရလား ။
[2022-06-05 16:12:09] Best translation 649 : ခင်ဗျား ဘာ လုပ် နေရယ် ။
[2022-06-05 16:12:09] Best translation 650 : ခင်ဗျား ဘာ လုပ် နေရယ် ။
[2022-06-05 16:12:09] Best translation 651 : နင် အေး ရင် ရေ ကကို လာ ဖဖိဖို့ လလိုအပ် ရယ် ။
[2022-06-05 16:12:09] Best translation 652 : ကျွန်တော်ဝဝိဝို့ အအဲ့ဒါဝဝို ပထမတော့ မ ပြု ခခဲ့ရ ။
[2022-06-05 16:12:09] Best translation 653 : ကျွန်တော် မမျှော်လင့် ဟားတတဲ့ ဖဖိဖို့ မျှော်လင့် တယ် ။
[2022-06-05 16:12:09] Best translation 654 : နင် ဒုက္ခ မ ဒုက္ခပေး ရ ။
[2022-06-05 16:12:09] Best translation 655 : ငါ ကကိုး နာရီမှာ တာဝန် တစ်ရပ် ဖြစ်ရယ် ။
[2022-06-05 16:12:09] Best translation 656 : ငါ စည်းဝေးပွဲ နောက်ကျ နေရယ် ။
[2022-06-05 16:12:09] Best translation 657 : အယ့်ဒါ ဘယ်သသူ့ ယောက်မ ရိ ။
[2022-06-05 16:12:09] Best translation 658 : နင် သသူ့ကကို မုန်းက လဲ မ ဟုတ် ဝလား ။
[2022-06-05 16:12:09] Best translation 659 : နင့် မိဘတွေ က ဖယ်သူ တွေ ။
[2022-06-05 16:12:09] Best translation 660 : ဖယ်သူတွေ စိတ်လှုပ်ရှားသွား ရိလဲ ။
[2022-06-05 16:12:09] Best translation 661 : ဒယ်ကောင်မငယ် အိမ်ရှင်မ တစ်ယောက်ဖြစ်ရယ် ။
[2022-06-05 16:12:09] Best translation 662 : ဘဇာလောက် စိတ်မလှုပ်ရှား ရိ ။
[2022-06-05 16:12:09] Best translation 663 : မင်း ငါ့ ကကို ရှင်းပြ ပါလား ။
[2022-06-05 16:12:09] Best translation 664 : အဲဒီ ကကို သော ဖဖိဖို့ မ တတိုက်တွန်း ရ ။
[2022-06-05 16:12:09] Best translation 665 : ခရီးမထွက် ရလား ။
[2022-06-05 16:12:09] Best translation 666 : သူတတိတို့ ဘယ်လောက် သတ္တိရှိ လဲ ။
[2022-06-05 16:12:09] Best translation 667 : နင့်ဟာနင် အားငယ် နေစာ ။
[2022-06-05 16:12:09] Best translation 668 : ဒယ် အကြောင်း ပြော ရမယ်ဆဆို သိလား ။
[2022-06-05 16:12:09] Best translation 669 : သူ မင်္ဂလာဆောင် ကကို လာကြ လလိုက်ရယ်လား ။
[2022-06-05 16:12:09] Total time: 4.06537s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    0m50.702s
user    1m18.666s
sys     0m12.274s
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.dwbk.1$ time ./test-eval.sh
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.dwbk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 20.90, 56.7/27.3/18.4/13.2 (BP=0.843, ratio=0.854, hyp_len=3646, ref_len=4267)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 20.21, 55.7/26.5/17.9/12.4 (BP=0.845, ratio=0.856, hyp_len=3652, ref_len=4267)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 19.71, 55.5/25.9/17.0/11.9 (BP=0.849, ratio=0.859, hyp_len=3665, ref_len=4267)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 19.28, 54.6/24.8/16.3/11.3 (BP=0.862, ratio=0.871, hyp_len=3715, ref_len=4267)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 19.10, 54.4/24.4/15.5/10.6 (BP=0.884, ratio=0.890, hyp_len=3799, ref_len=4267)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 19.01, 53.3/24.2/15.3/10.5 (BP=0.892, ratio=0.897, hyp_len=3829, ref_len=4267)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 19.07, 53.5/24.2/15.6/10.8 (BP=0.883, ratio=0.889, hyp_len=3793, ref_len=4267)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 18.94, 53.4/24.1/15.4/10.5 (BP=0.886, ratio=0.892, hyp_len=3806, ref_len=4267)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 18.65, 53.1/23.8/15.1/10.1 (BP=0.889, ratio=0.895, hyp_len=3817, ref_len=4267)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 19.23, 53.3/24.3/15.6/10.5 (BP=0.896, ratio=0.901, hyp_len=3845, ref_len=4267)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 19.18, 53.0/24.1/15.4/10.6 (BP=0.897, ratio=0.902, hyp_len=3849, ref_len=4267)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.dwbk.1$
```

**BEST BLEU Score of dw-bk, word unit, transformer archi is 20.90.**  

## rk-bk, Word Unit, Transformer Archi

Training script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 5 June 2022


model_folder="model.transformer.rkbk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="rk"; tgt="bk";

marian \
    --model ${model_folder}/model.npz --type transformer \
    --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
    --max-length 200 \
    --vocabs ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
    --valid-translation-output ${model_folder}/valid.${src}-${tgt}.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > ${model_folder}/${src}-${tgt}.config.yml

time marian -c ${model_folder}/${src}-${tgt}.config.yml  2>&1 | tee ${model_folder}/transformer-${src}-${tgt}.log
```

Training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./transformer.rkbk.sh
...
...
...
[2022-06-05 18:08:43] Seen 8,850 samples
[2022-06-05 18:08:43] Starting data epoch 2037 in logical epoch 2037
[2022-06-05 18:08:43] [data] Shuffling data
[2022-06-05 18:08:43] [data] Done reading 8,850 sentences
[2022-06-05 18:08:43] [data] Done shuffling 8,850 sentences to temp files
[2022-06-05 18:08:46] Seen 8,850 samples
[2022-06-05 18:08:46] Starting data epoch 2038 in logical epoch 2038
[2022-06-05 18:08:46] [data] Shuffling data
[2022-06-05 18:08:46] [data] Done reading 8,850 sentences
[2022-06-05 18:08:46] [data] Done shuffling 8,850 sentences to temp files
[2022-06-05 18:08:48] Seen 8,850 samples
[2022-06-05 18:08:48] Starting data epoch 2039 in logical epoch 2039
[2022-06-05 18:08:48] [data] Shuffling data
[2022-06-05 18:08:48] [data] Done reading 8,850 sentences
[2022-06-05 18:08:48] [data] Done shuffling 8,850 sentences to temp files
[2022-06-05 18:08:51] Seen 8,850 samples
[2022-06-05 18:08:51] Starting data epoch 2040 in logical epoch 2040
[2022-06-05 18:08:51] [data] Shuffling data
[2022-06-05 18:08:51] [data] Done reading 8,850 sentences
[2022-06-05 18:08:52] [data] Done shuffling 8,850 sentences to temp files
[2022-06-05 18:08:54] Seen 8,850 samples
[2022-06-05 18:08:54] Starting data epoch 2041 in logical epoch 2041
[2022-06-05 18:08:54] [data] Shuffling data
[2022-06-05 18:08:54] [data] Done reading 8,850 sentences
[2022-06-05 18:08:54] [data] Done shuffling 8,850 sentences to temp files
[2022-06-05 18:08:55] Ep. 2041 : Up. 55000 : Sen. 1,406 : Cost 1.24907100 * 1,245,012 @ 3,384 after 136,761,428 : Time 55.74s : 22336.16 words/s : gNorm 0.0957 : L.r. 1.6181e-04
[2022-06-05 18:08:55] Saving model weights and runtime parameters to model.transformer.rkbk.1/model.iter55000.npz
[2022-06-05 18:08:55] Saving model weights and runtime parameters to model.transformer.rkbk.1/model.npz
[2022-06-05 18:08:56] Saving Adam parameters
[2022-06-05 18:08:56] [training] Saving training checkpoint to model.transformer.rkbk.1/model.npz and model.transformer.rkbk.1/model.npz.optimizer.npz
[2022-06-05 18:08:59] [valid] Ep. 2041 : Up. 55000 : cross-entropy : 26.7789 : stalled 10 times (last best: 22.468)
[2022-06-05 18:08:59] [valid] Ep. 2041 : Up. 55000 : perplexity : 33.3991 : stalled 10 times (last best: 18.9865)
[2022-06-05 18:09:00] [valid] Ep. 2041 : Up. 55000 : bleu : 31.169 : stalled 10 times (last best: 33.3424)
[2022-06-05 18:09:00] Training finished
[2022-06-05 18:09:00] Saving model weights and runtime parameters to model.transformer.rkbk.1/model.npz
[2022-06-05 18:09:01] Saving Adam parameters
[2022-06-05 18:09:01] [training] Saving training checkpoint to model.transformer.rkbk.1/model.npz and model.transformer.rkbk.1/model.npz.optimizer.npz

real    102m54.624s
user    123m4.786s
sys     1m48.896s
```

check models ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.rkbk.1$ ls *.npz | sort -V
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
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.rkbk.1$
```

prepare test-eval bash script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="rk"; tgt="bk";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing/evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.rkbk.1$ time ./test-eval.sh
...
...
...
[2022-06-05 22:37:48] Best translation 1038 : နင် ဖယ်သသူ့ကကို ခွင့်ပြု ဝဝိဝို့ ။
[2022-06-05 22:37:48] Best translation 1039 : နင် က ဘာ သင် ခခဲ့ရယ် ။
[2022-06-05 22:37:48] Best translation 1040 : သူလလိလို့ ခင်ဗျား ကကို သံသယ ဖြစ်မယ်နား ။
[2022-06-05 22:37:48] Best translation 1041 : သူတတိတို့ ဘဇာလောက် အမြော်အမြင်ကြီး လည်း ။
[2022-06-05 22:37:48] Best translation 1042 : ဘုရင် တင်မြှောက် လလိုက်ကြရယ် ။
[2022-06-05 22:37:48] Best translation 1043 : တစ်နေ့ ရေချျိုးချိန် တတဲ့ လူ တစ်ယောက် နှိပ်ပေးတတဲ့ လူ ဝ ။
[2022-06-05 22:37:48] Best translation 1044 : အေး ပြန်ဖြစ် လာပီတတဲ့ လလိလို့ မင်း မ ခံစား ရလား ။
[2022-06-05 22:37:48] Best translation 1045 : ဟိတ် နင် ဘာ တင်ပြ အုန်း ။
[2022-06-05 22:37:48] Best translation 1046 : နင်ဝဝိဝို့ အအဲ့ဇာဝဝို ရောင်း ဝဝိဝို့လား ။
[2022-06-05 22:37:48] Best translation 1047 : မင်း ဒုက္ခ တေ ကကို သည်းမခံ နနိုင်လား ။
[2022-06-05 22:37:48] Best translation 1048 : ဒါကကို မင်းကြြိုက်ချင်ကြြိုက် မကြြိုက်ချင်နေ ။
[2022-06-05 22:37:48] Best translation 1049 : ဒယ်ကောင်မငယ် နေ့က လလို ခခဲ့ရယ်လား ။
[2022-06-05 22:37:48] Best translation 1050 : သူ နေမကောင်းဝ ရိ စာမေးပွဲ မ ကြြိုးစား ရ ။
[2022-06-05 22:37:48] Best translation 1051 : သူ ဒယ်ကောင်မငယ် ဝဝို ရှာ ခခဲ့ဇာလား ။
[2022-06-05 22:37:48] Best translation 1052 : ဒါမမဲ့ သူ တစ် ပတ် ကြာ စာ ။
[2022-06-05 22:37:48] Best translation 1053 : အအဲ့ဇာဝဝို မေ့ဟားဇာ ပပိုကောင်း ရယ် ။
[2022-06-05 22:37:48] Best translation 1054 : သူဒဒိဒို့ ဆရာ ဖြစ် လာရယ် ။
[2022-06-05 22:37:48] Best translation 1055 : မင်း ဒယ်စာ ဝဝို သွား သင့်ပြီလန်း ။
[2022-06-05 22:37:48] Best translation 1056 : အဲဒါ ဘာလလို လဲ ။
[2022-06-05 22:37:48] Best translation 1057 : သူတတိတို့ ဖယ်သသူ့ ကကို ကူညီ ဝဝိဝို့လဲ ။
[2022-06-05 22:37:48] Best translation 1058 : သားငယ် လေ ဟဟုံး ပေါ်မှာ ကစား နေခခဲ့ရယ် ။
[2022-06-05 22:37:48] Best translation 1059 : ကျွန်တော်လလိလို့က ခင်ဗျား ကကို တောင်းပန် ရမယ်လား ။
[2022-06-05 22:37:48] Best translation 1060 : ကျွန်တော်ဝဝိဝို့ မ ကြြိုးစား ခခဲ့ဟိလား ။
[2022-06-05 22:37:48] Best translation 1061 : ဘာ စာတွေ ရိ ။
[2022-06-05 22:37:48] Best translation 1062 : ကျွန်တော်ဝဝိဝို့ ဝယ် ဟားတတဲ့ နေရာ လေ ။
[2022-06-05 22:37:48] Best translation 1063 : ကျွန်တော်ဝဝိဝို့ သသူ့ ကကို ဘုရားကျောင်း မှာ ခေါ် ရယ် ။
[2022-06-05 22:37:48] Best translation 1064 : နင် သူဝဝိဝို့ နနဲ့ ဆဆုံ ခခဲ့ရယ်လား ။
[2022-06-05 22:37:48] Best translation 1065 : တခါတလေ သော နနိုင်ရယ် ။
[2022-06-05 22:37:48] Best translation 1066 : ဒါမယ့် ကျွန်တော့်ရရဲ့ မယ် ၊ ဒါမမဲ့ အမှန်ပပဲ့ ။
[2022-06-05 22:37:48] Best translation 1067 : လူကြီးမင်း ခဏငယ် ကကိုင်ထား ပေးလန်း ။
[2022-06-05 22:37:48] Best translation 1068 : သော က ။
[2022-06-05 22:37:48] Best translation 1069 : နင် ဘာ ဝယ် ဝဝိဝို့ ။
[2022-06-05 22:37:48] Best translation 1070 : ဒယ်ကောင်မငယ် မ အိပ် သင့်ရ ။
[2022-06-05 22:37:48] Best translation 1071 : အအဲ့ဇာက ဒယ်ကောင်မငယ် အတွက် လွယ်လွယ်ငယ်ပဲ ။
[2022-06-05 22:37:48] Total time: 6.20151s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m15.053s
user    2m1.907s
sys     0m17.183s
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.rkbk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 33.43, 64.2/39.7/30.6/24.9 (BP=0.897, ratio=0.902, hyp_len=6271, ref_len=6956)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 33.57, 64.1/39.7/30.8/24.9 (BP=0.898, ratio=0.903, hyp_len=6281, ref_len=6956)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 33.71, 64.5/39.9/31.0/25.4 (BP=0.893, ratio=0.898, hyp_len=6248, ref_len=6956)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 33.69, 64.2/39.9/31.2/25.3 (BP=0.893, ratio=0.899, hyp_len=6250, ref_len=6956)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 33.31, 63.2/38.9/30.3/24.5 (BP=0.906, ratio=0.910, hyp_len=6329, ref_len=6956)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 32.95, 63.0/38.6/29.9/24.0 (BP=0.907, ratio=0.911, hyp_len=6337, ref_len=6956)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 32.94, 63.0/38.5/29.6/23.7 (BP=0.912, ratio=0.915, hyp_len=6367, ref_len=6956)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 32.51, 62.5/37.9/29.0/23.3 (BP=0.914, ratio=0.917, hyp_len=6382, ref_len=6956)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 32.29, 62.5/37.7/28.7/23.0 (BP=0.915, ratio=0.918, hyp_len=6386, ref_len=6956)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 32.21, 62.0/37.5/28.6/22.4 (BP=0.922, ratio=0.925, hyp_len=6434, ref_len=6956)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 31.84, 61.8/36.9/27.9/21.9 (BP=0.926, ratio=0.929, hyp_len=6461, ref_len=6956)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.rkbk.1$
```

**Best score for rk-bk, word unit, transformer is 33.71.**

## bk-rk, Word Unit, Transformer Archi  

Prepare model training bash script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 5 June 2022


model_folder="model.transformer.bkrk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="bk"; tgt="rk";

marian \
    --model ${model_folder}/model.npz --type transformer \
    --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
    --max-length 200 \
    --vocabs ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
    --valid-translation-output ${model_folder}/valid.${src}-${tgt}.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > ${model_folder}/${src}-${tgt}.config.yml

time marian -c ${model_folder}/${src}-${tgt}.config.yml  2>&1 | tee ${model_folder}/transformer-${src}-${tgt}.log
```

start training ...  

```
[2022-06-05 23:00:38] [marian] Marian v1.11.0 f00d0621 2022-02-08 08:39:24 -0800
[2022-06-05 23:00:38] [marian] Running on ye-System-Product-Name as process 62812 with command line:
[2022-06-05 23:00:38] [marian] marian -c model.transformer.bkrk.1/bk-rk.config.yml
[2022-06-05 23:00:38] [config] after: 0e
[2022-06-05 23:00:38] [config] after-batches: 0
[2022-06-05 23:00:38] [config] after-epochs: 0
[2022-06-05 23:00:38] [config] all-caps-every: 0
[2022-06-05 23:00:38] [config] allow-unk: false
[2022-06-05 23:00:38] [config] authors: false
[2022-06-05 23:00:38] [config] beam-size: 6
[2022-06-05 23:00:38] [config] bert-class-symbol: "[CLS]"
[2022-06-05 23:00:38] [config] bert-mask-symbol: "[MASK]"
[2022-06-05 23:00:38] [config] bert-masking-fraction: 0.15
[2022-06-05 23:00:38] [config] bert-sep-symbol: "[SEP]"
[2022-06-05 23:00:38] [config] bert-train-type-embeddings: true
[2022-06-05 23:00:38] [config] bert-type-vocab-size: 2
[2022-06-05 23:00:38] [config] build-info: ""
[2022-06-05 23:00:38] [config] check-gradient-nan: false
[2022-06-05 23:00:38] [config] check-nan: false
[2022-06-05 23:00:38] [config] cite: false
[2022-06-05 23:00:38] [config] clip-norm: 5
[2022-06-05 23:00:38] [config] cost-scaling:
[2022-06-05 23:00:38] [config]   []
[2022-06-05 23:00:38] [config] cost-type: ce-sum
[2022-06-05 23:00:38] [config] cpu-threads: 0
[2022-06-05 23:00:38] [config] data-threads: 8
[2022-06-05 23:00:38] [config] data-weighting: ""
[2022-06-05 23:00:38] [config] data-weighting-type: sentence
[2022-06-05 23:00:38] [config] dec-cell: gru
[2022-06-05 23:00:38] [config] dec-cell-base-depth: 2
[2022-06-05 23:00:38] [config] dec-cell-high-depth: 1
[2022-06-05 23:00:38] [config] dec-depth: 2
[2022-06-05 23:00:38] [config] devices:
[2022-06-05 23:00:38] [config]   - 0
[2022-06-05 23:00:38] [config]   - 1
[2022-06-05 23:00:38] [config] dim-emb: 512
[2022-06-05 23:00:38] [config] dim-rnn: 1024
[2022-06-05 23:00:38] [config] dim-vocabs:
[2022-06-05 23:00:38] [config]   - 0
[2022-06-05 23:00:38] [config]   - 0
[2022-06-05 23:00:38] [config] disp-first: 0
[2022-06-05 23:00:38] [config] disp-freq: 500
...
...
...
[2022-06-06 00:44:46] Starting data epoch 2173 in logical epoch 2173
[2022-06-06 00:44:46] [data] Shuffling data
[2022-06-06 00:44:46] [data] Done reading 8,850 sentences
[2022-06-06 00:44:46] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:44:48] Seen 8,850 samples
[2022-06-06 00:44:48] Starting data epoch 2174 in logical epoch 2174
[2022-06-06 00:44:48] [data] Shuffling data
[2022-06-06 00:44:48] [data] Done reading 8,850 sentences
[2022-06-06 00:44:49] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:44:51] Seen 8,850 samples
[2022-06-06 00:44:51] Starting data epoch 2175 in logical epoch 2175
[2022-06-06 00:44:51] [data] Shuffling data
[2022-06-06 00:44:51] [data] Done reading 8,850 sentences
[2022-06-06 00:44:51] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:44:54] Seen 8,850 samples
[2022-06-06 00:44:54] Starting data epoch 2176 in logical epoch 2176
[2022-06-06 00:44:54] [data] Shuffling data
[2022-06-06 00:44:54] [data] Done reading 8,850 sentences
[2022-06-06 00:44:54] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:44:57] Seen 8,850 samples
[2022-06-06 00:44:57] Starting data epoch 2177 in logical epoch 2177
[2022-06-06 00:44:57] [data] Shuffling data
[2022-06-06 00:44:57] [data] Done reading 8,850 sentences
[2022-06-06 00:44:57] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:45:00] Seen 8,850 samples
[2022-06-06 00:45:00] Starting data epoch 2178 in logical epoch 2178
[2022-06-06 00:45:00] [data] Shuffling data
[2022-06-06 00:45:00] [data] Done reading 8,850 sentences
[2022-06-06 00:45:00] [data] Done shuffling 8,850 sentences to temp files
[2022-06-06 00:45:01] Ep. 2178 : Up. 55000 : Sen. 2,934 : Cost 1.26405466 * 1,310,942 @ 4,496 after 143,530,362 : Time 56.59s : 23166.99 words/s : gNorm 0.1065 : L.r. 1.6181e-04
[2022-06-06 00:45:01] Saving model weights and runtime parameters to model.transformer.bkrk.1/model.iter55000.npz
[2022-06-06 00:45:01] Saving model weights and runtime parameters to model.transformer.bkrk.1/model.npz
[2022-06-06 00:45:02] Saving Adam parameters
[2022-06-06 00:45:02] [training] Saving training checkpoint to model.transformer.bkrk.1/model.npz and model.transformer.bkrk.1/model.npz.optimizer.npz
[2022-06-06 00:45:05] [valid] Ep. 2178 : Up. 55000 : cross-entropy : 25.7818 : stalled 10 times (last best: 22.626)
[2022-06-06 00:45:05] [valid] Ep. 2178 : Up. 55000 : perplexity : 31.562 : stalled 10 times (last best: 20.6852)
[2022-06-06 00:45:06] [valid] Ep. 2178 : Up. 55000 : bleu : 33.2718 : stalled 10 times (last best: 34.1791)
[2022-06-06 00:45:06] Training finished
[2022-06-06 00:45:06] Saving model weights and runtime parameters to model.transformer.bkrk.1/model.npz
[2022-06-06 00:45:07] Saving Adam parameters
[2022-06-06 00:45:07] [training] Saving training checkpoint to model.transformer.bkrk.1/model.npz and model.transformer.bkrk.1/model.npz.optimizer.npz
```

check the output models ...  

```
(base) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkrk.1$ ls *.npz | sort -V
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
model.npz
model.npz.optimizer.npz
(base) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkrk.1$
```

prepare test-eval script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="bk"; tgt="rk";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing/evaluation ...  

```
(base) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkrk.1$ time ./test-eval.sh
...
...
...
[2022-06-06 08:58:02] Best translation 1038 : မင်း ဗလီ အတွက် ခွင့်ပြု ဖို့ ။
[2022-06-06 08:58:02] Best translation 1039 : မင်းဇာတိ သင် ခလေး ။
[2022-06-06 08:58:02] Best translation 1040 : သူရို့ မင်း ကို သံသယ ဖြိုက်လားမယ် ။
[2022-06-06 08:58:02] Best translation 1041 : သူရို့ ဇာလောက် သတ္တိ ဟိလေး ။
[2022-06-06 08:58:02] Best translation 1042 : အစောက ချိုမြိန်နီရေ ချောကလက်ပြားချေ ဖို့ ဖေသာ ကုန်ရေ။
[2022-06-06 08:58:02] Best translation 1043 : ​ကောင်းစွာတိ ရ ရေ လူ ဝကြီးကို မ ထိကေ။
[2022-06-06 08:58:02] Best translation 1044 : ကျွန်တော် ရို့ချမ်း ကေ မင်း မ ခံစားရ ပါလား ။
[2022-06-06 08:58:02] Best translation 1045 : မင်း တစ်ခုခု တင်ပြဖို့ ဟိ လား ။
[2022-06-06 08:58:02] Best translation 1046 : မင်းရို့ ယင်းချင့် ကို ရောင်း ဖို့လား ။
[2022-06-06 08:58:02] Best translation 1047 : မင်း ဒုက္ခ တိ ကို သည်းမခံ နိုင်ပါလာ ။
[2022-06-06 08:58:02] Best translation 1048 : ယင်းချင့်ကို လားကြည့်ပါ ။
[2022-06-06 08:58:02] Best translation 1049 : သူ ညက ပြောရေ ရေပိုင် ပြောပါ ။
[2022-06-06 08:58:02] Best translation 1050 : သူ ကကောင်း မ ကြိုးစား ခ ပါ ။
[2022-06-06 08:58:02] Best translation 1051 : သူ သူ့ ကို မိန့်ပစ် ခပါလား ။
[2022-06-06 08:58:02] Best translation 1052 : ယေကေလေ့ တစ်ပတ် သူ တစ်ပတ်မာ လား ရေ ။
[2022-06-06 08:58:02] Best translation 1053 : ယင်းကို မိန့်ထားစွာ ပိုကောင်း ပါရေ ။
[2022-06-06 08:58:02] Best translation 1054 : သူရို့ ဆရာ ဖြစ် လာရေ။
[2022-06-06 08:58:02] Best translation 1055 : မင်း ယင်းချင့် ကို လား စုံစမ်း နိုင်ဖို့လား ။
[2022-06-06 08:58:02] Best translation 1056 : ယင်းချင့် ဇာပိုင် လေး ။
[2022-06-06 08:58:03] Best translation 1057 : သူရို့ ဇာသူ့ ကို ကူညီ ဖို့ လေး ။
[2022-06-06 08:58:03] Best translation 1058 : ပုံနှိပ်ထား ရေ ။
[2022-06-06 08:58:03] Best translation 1059 : ကျွန်တော်ရို့ က မင်းကို တောင်းပန် ရဖို့လား ။
[2022-06-06 08:58:03] Best translation 1060 : ကျွန်တော်ရို့ မ ကြိုးစား ခ ပါလား။
[2022-06-06 08:58:03] Best translation 1061 : ဇာ အရွယ် ဝတ် ပါ လေး ။
[2022-06-06 08:58:03] Best translation 1062 : ကျွန်တော်ရို့ လိမ္မော်သီး တိ ဝယ် ခကတ်စွာပါ ။
[2022-06-06 08:58:03] Best translation 1063 : ကျွန်တော်ရို့ သူ့ကို မိန်းကြည့်ကတ်ဖို့။
[2022-06-06 08:58:03] Best translation 1064 : မင်း သူရို့ နန့် ဆုံ ခပါလား ။
[2022-06-06 08:58:03] Best translation 1065 : ညစာအတွက် ကုန်ကျစရိတ်ကိုမျှဝေကျခံ ဖို့ စိတ်ထက်သန် ပါရေ ။
[2022-06-06 08:58:03] Best translation 1066 : ယေကေလေ့ ကျွန်တော့်ရဲ့ ခန်းမ ထဲမာ တင်ဖို့အချိန် မီ ပြီးရဖို့ ။
[2022-06-06 08:58:03] Best translation 1067 : လူကြီးမင်း တစ်ချက်လောက် ကိုင်ထား ပီးပါ ။
[2022-06-06 08:58:03] Best translation 1068 : လား က လိုက် ဗျာယ် ။
[2022-06-06 08:58:03] Best translation 1069 : မင်း ဇာ ဝယ် ဖို့လေး။
[2022-06-06 08:58:03] Best translation 1070 : ဒေမာ အိပ် ဖို့ မ သင့်တော် ပါ ။
[2022-06-06 08:58:03] Best translation 1071 : ယင်းချင့် ထိုမချေ အတွက် အလွယ်ချေပါ ။
[2022-06-06 08:58:03] Total time: 6.24559s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m30.843s
user    2m3.003s
sys     0m17.517s
```

results are as follows:  

```
(base) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkrk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.rk, Transformer model:
BLEU = 33.32, 62.4/41.0/30.6/23.2 (BP=0.907, ratio=0.911, hyp_len=6142, ref_len=6739)
Evaluation with hyp.iter10000.rk, Transformer model:
BLEU = 32.54, 61.6/40.2/29.9/22.5 (BP=0.906, ratio=0.910, hyp_len=6131, ref_len=6739)
Evaluation with hyp.iter15000.rk, Transformer model:
BLEU = 32.78, 61.5/39.9/29.6/22.7 (BP=0.914, ratio=0.918, hyp_len=6186, ref_len=6739)
Evaluation with hyp.iter20000.rk, Transformer model:
BLEU = 33.26, 62.0/40.7/30.3/23.0 (BP=0.914, ratio=0.917, hyp_len=6181, ref_len=6739)
Evaluation with hyp.iter25000.rk, Transformer model:
BLEU = 32.79, 61.9/40.2/29.9/22.9 (BP=0.907, ratio=0.911, hyp_len=6142, ref_len=6739)
Evaluation with hyp.iter30000.rk, Transformer model:
BLEU = 32.52, 61.6/39.8/29.4/22.4 (BP=0.913, ratio=0.916, hyp_len=6175, ref_len=6739)
Evaluation with hyp.iter35000.rk, Transformer model:
BLEU = 32.40, 61.3/39.5/29.3/22.4 (BP=0.912, ratio=0.916, hyp_len=6173, ref_len=6739)
Evaluation with hyp.iter40000.rk, Transformer model:
BLEU = 32.36, 61.1/39.2/29.0/22.1 (BP=0.919, ratio=0.922, hyp_len=6215, ref_len=6739)
Evaluation with hyp.iter45000.rk, Transformer model:
BLEU = 32.75, 61.3/39.5/29.4/22.7 (BP=0.919, ratio=0.922, hyp_len=6214, ref_len=6739)
Evaluation with hyp.iter50000.rk, Transformer model:
BLEU = 32.87, 61.1/39.6/29.4/22.5 (BP=0.923, ratio=0.926, hyp_len=6242, ref_len=6739)
Evaluation with hyp.iter55000.rk, Transformer model:
BLEU = 32.56, 60.8/39.2/29.0/22.1 (BP=0.926, ratio=0.929, hyp_len=6261, ref_len=6739)
(base) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.transformer.bkrk.1$
```

**Best BLEU score for bk-rk, word unit, transformer archi is 33.32.**  

## Evaluation with chrF score 

```

```

```

```
```

```
```

```

