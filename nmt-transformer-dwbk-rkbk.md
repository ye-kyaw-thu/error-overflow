# NMT Transformer dw-bk, rk-bk Baselines

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

```

check the model folders:  

```

```

test-eval script ...  

```bash

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

