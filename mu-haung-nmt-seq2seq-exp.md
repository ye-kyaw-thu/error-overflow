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

training စလုပ်ခဲ့ ...  

```

```

