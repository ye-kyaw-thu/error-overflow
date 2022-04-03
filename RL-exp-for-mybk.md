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

## for Seq2Seq
### Bash Script Writing

အရင်ဆုံး 30 epoch ကနေ 70 epoch အထိ seq2seq training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...  

```bash

```

## Seq2Seq-RL

နောက်ဆက်တွဲ continuous-training တွေရဲ့ model တွေကိုလည်း ရှေ့မှာ training လုပ်ခဲ့တဲ့ ဖိုလ်ဒါထဲမှာပဲအတူတူ သိမ်းခဲ့တယ်။ အဲဒါကြောင့် 30-epoch ရဲ့ RL model တွေက 30-epoch/ အောက်မှာပဲ ဆက်ရှိမယ်။   


## for Transformer
### Bash Script Writing

30 epoch ကနေ 70 epoch အထိ transformer training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...   

```bash

```

## Transformer-RL

