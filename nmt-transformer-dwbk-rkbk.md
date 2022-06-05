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

```

results are as follows ...  

```

```

## bk-dw, Word Unit, Transformer Archi

training script ...  

```bash

```

training ...  

```

```

check the models ...  

```

```

test-eval script ...  

```bash

```

testing/evaluation ...  

```

```

results are as follows:  

```

```

## rk-bk, Word Unit, Transformer Archi

Training script ...  

```bash

```

Training ...  

```

```

check models ...  

```

```

prepare test-eval bash script ...  

```bash

```

testing/evaluation ...  

```

```

results are as follows:  

```

```

## rk-bk, Word Unit, Transformer Archi  

Prepare model training bash script ...  

```bash

```

start training ...  

```

```

check the output models ...  

```

```

prepare test-eval script ...  

```bash

```

testing/evaluation ...  

```

```

results are as follows:  

```

```

## Evaluation with chrF score 

```

```

```

```
```

```
```

```

