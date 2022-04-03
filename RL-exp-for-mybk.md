# RL Experiment for Myanmar-Beik Language Pair

ရှေ့မှာ လုပ်ခဲ့တဲ့ ရခိုင်-မြန်မာ RL experiment ရဲ့ အဆက်ပါ။ ရှေ့မှာလုပ်ခဲ့တဲ့ experiment တွေရဲ့ log က အောက်ပါအတိုင်းပါ။  

- [simple-nmt-experiment.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/simple-nmt-experiment.md)
- [simple-nmt-40-60-to-70-30-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/simple-nmt-40-60-to-70-30-log.md)

ဒီတစ်ခါတော့ မြန်မာ-ဘိတ် အတွဲအတွက်လုပ်ခဲ့စဉ်က မှတ်သားခဲ့တဲ့ running log ဖိုင်ပါ။  

## Folder Preparation

training မလုပ်ခင်မှာ အရင်ဆုံး အောက်ပါ folder-structure အတိုင်း ဖိုလ်ဒါတွေကိုဆောက်ထားလိုက်ပါတယ်။ ရှေ့က run ခဲ့တဲ့ မြန်မာ-ရခိုင်အတွဲရဲ့ folder-structure နဲ့တော့ အတိအကျမတူပါဘူး။ ဒီနေရာမှာ baseline/ က baseline model တွေကိုသိမ်းဖို့ ဖြစ်ပြီး၊ rl/ အောက်မှာကက reinforcement learning model တွေကို သိမ်းဖို့အတွက် ဖြစ်ပါတယ်။  

```
(base) ye@:~/exp/simple-nmt/model/rl2$ tree
.
├── baseline
│   ├── seq2seq
│   │   ├── bkmy-30epoch
│   │   ├── bkmy-40epoch
│   │   ├── bkmy-50epoch
│   │   ├── bkmy-60epoch
│   │   ├── bkmy-70epoch
│   │   ├── mybk-30epoch
│   │   ├── mybk-40epoch
│   │   ├── mybk-50epoch
│   │   ├── mybk-60epoch
│   │   └── mybk-70epoch
│   └── transformer
│       ├── bkmy-30epoch
│       ├── bkmy-40epoch
│       ├── bkmy-50epoch
│       ├── bkmy-60epoch
│       ├── bkmy-70epoch
│       ├── mybk-30epoch
│       ├── mybk-40epoch
│       ├── mybk-50epoch
│       ├── mybk-60epoch
│       └── mybk-70epoch
└── rl
    ├── seq2seq
    │   ├── bkmy-30epoch
    │   ├── bkmy-40epoch
    │   ├── bkmy-50epoch
    │   ├── bkmy-60epoch
    │   ├── bkmy-70epoch
    │   ├── mybk-30epoch
    │   ├── mybk-40epoch
    │   ├── mybk-50epoch
    │   ├── mybk-60epoch
    │   └── mybk-70epoch
    └── transformer
        ├── bkmy-30epoch
        ├── bkmy-40epoch
        ├── bkmy-50epoch
        ├── bkmy-60epoch
        ├── bkmy-70epoch
        ├── mybk-30epoch
        ├── mybk-40epoch
        ├── mybk-50epoch
        ├── mybk-60epoch
        └── mybk-70epoch

46 directories, 0 files

```

## for Seq2Seq Baseline
### Bash Script Writing

အရင်ဆုံး 30 epoch ကနေ 70 epoch အထိ seq2seq training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 3 April 2022
# Seq2Seq-Reinforcement Learning exp for Myanmar-Beik, Beik-Myanmar

# training baseline for my-bk

for i in {30,40,50,60,70}
do
      echo "mybk, seq2seq-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang mybk \
   --gpu_id 0 --batch_size 64 --n_epochs ${i} \
   --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
   --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
   --use_adam --rl_n_epochs 0 \
   --model_fn ./model/rl2/baseline/seq2seq/mybk-${i}epoch/seq-model-mybk.pth  | tee ./model/rl2/baseline/seq2seq/mybk-${i}epoch/mybk-training.log;
done

echo "####################";

# training baseline for bk-my
for i in {30,40,50,60,70}
do
      echo "bkmy, seq2seq-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang bkmy \
   --gpu_id 1 --batch_size 64 --n_epochs ${i} \
   --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
   --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
   --use_adam --rl_n_epochs 0 \
   --model_fn ./model/rl2/baseline/seq2seq/bkmy-${i}epoch/seq-model-bkmy.pth | tee ./model/rl2/baseline/seq2seq/bkmy-${i}epoch/bkmy-training.log;
done
```

### Training

output အကုန်ကိုတော့ ဒီနေရာမှာ မသိမ်းတော့ဘူး။ လိုင်းအရေအတွက်က တအားများလွန်းလို့...  
running process နဲ့ အဓိကကျတဲ့ အပိုင်းကို follow လိုက်လို့ ရအောင်ပဲ log မှတ်သွားမယ်။  
မော်ဒယ်တစ်ခုချင်းစီအတွက်က training လုပ်ရင်းနဲ့ tee command နဲ့ သိမ်းထားပြီးသားလည်း သက်ဆိုင်ရာ ဖိုလ်ဒါအောက်မှာ ရှိတယ်။  

```

```

## Seq2Seq-RL

နောက်ဆက်တွဲ continuous-training တွေရဲ့ model တွေကိုလည်း ရှေ့မှာ training လုပ်ခဲ့တဲ့ ဖိုလ်ဒါထဲမှာပဲအတူတူ သိမ်းခဲ့တယ်။ အဲဒါကြောင့် 30-epoch ရဲ့ RL model တွေက 30-epoch/ အောက်မှာပဲ ဆက်ရှိမယ်။   


## for Transformer Baseline
### Bash Script Writing

30 epoch ကနေ 70 epoch အထိ transformer training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...   

```bash

```

## Transformer-RL

