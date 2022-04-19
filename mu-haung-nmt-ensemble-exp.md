## NMT Ensemble Experiment for MuHaung Translation

ဒီတစ်ခါတော့ seq2seq နဲ့ transformer architecture နှစ်မျိုးကိုနဲ့ ဆောက်ထားတဲ့ မော်ဒယ်တွေကို သုံးပြီး ensemble experiment လုပ်ကြည့်မယ်။  

### Ensemble Decoding Script for Seq2Seq and Transformer

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last Updated: 19 April 2022
# Ensemble decoding with s2s+transformer:


# my-br, seq2seq အတွက် best model က model.iter65000.npz
# my-br, transformer အတွက် best model က model0-mybr.iter95000.npz

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.4-0.6.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.4-0.6.log
    
# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.5-0.5.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.5-0.5.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.6-0.4.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.6-0.4.log
    
# br-my အတွက် best model က model.iter55000.npz
# br-my အတွက် best model က 

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.4-0.6.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.4-0.6.log

# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.5-0.5.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.5-0.5.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.6-0.4.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.6-0.4.log

```

Ensemble Decoding ...  

```

```

## Evaluation

အရင်ဆုံး bash script ရေးရမှာမို့ ရေးခဲ့...  

```bash

```

## Results


