# Multi-Source MuHaung Braille Post Editing Experiment

## Some References

multi-source experiment ကို ရှေ့မှာလည်း လုပ်ခဲ့ပေမဲ့ မြန်မာမျက်မမြင်စာ မူဟောင်း post-editing အလုပ်အတွက် ပြန်လေ့လာခဲ့တယ်။  
တချို့ link တွေက အောက်ပါအတိုင်း...  

- [https://github.com/marian-nmt/marian-regression-tests/blob/master/tests/training/models/multi-source/test_multi-transformer.sh](https://github.com/marian-nmt/marian-regression-tests/blob/master/tests/training/models/multi-source/test_multi-transformer.sh)

```
$MRT_MARIAN/marian \
    --seed 1111 --no-shuffle --clip-norm 0 \
    --type multi-transformer --dim-emb 128 --dim-rnn 256 --cost-type ce-mean \
    -m multi-transformer/model.npz -t train.bpe.{en,xx,de} -v vocab.en.yml vocab.xx.yml vocab.de.yml \
    --disp-freq 20 --after-batches 100 \
    --log multi-transformer.log
```

- [https://marian-nmt.github.io/examples/postedit/](https://marian-nmt.github.io/examples/postedit/)
- [https://marian-nmt.github.io/examples/exploration/](https://marian-nmt.github.io/examples/exploration/)
- [https://groups.google.com/g/marian-nmt/c/_mYpKj21suY?pli=1](https://groups.google.com/g/marian-nmt/c/_mYpKj21suY?pli=1)
- [https://cris.fbk.eu/retrieve/handle/11582/316423/25741/WMT080.pdf](https://cris.fbk.eu/retrieve/handle/11582/316423/25741/WMT080.pdf)
- [opus-cat-a-state-of-the-art-neural-machine-translation-engine-on-your-local-computer](https://www.ata-chronicle.online/highlights/opus-cat-a-state-of-the-art-neural-machine-translation-engine-on-your-local-computer/)

