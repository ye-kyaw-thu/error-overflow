
# NMT Experiments for Burmese and Ethnic Languages

## my-sh, Transformer

Training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mysh.sh
...
...
...
[2022-05-23 12:02:52] [data] Done reading 13,244 sentences
[2022-05-23 12:02:52] [data] Done shuffling 13,244 sentences to temp files
[2022-05-23 12:02:56] Seen 13,244 samples
[2022-05-23 12:02:56] Starting data epoch 1039 in logical epoch 1039
[2022-05-23 12:02:56] [data] Shuffling data
[2022-05-23 12:02:56] [data] Done reading 13,244 sentences
[2022-05-23 12:02:56] [data] Done shuffling 13,244 sentences to temp files
[2022-05-23 12:02:59] Ep. 1039 : Up. 55000 : Sen. 8,748 : Cost 1.19892883 * 1,273,373 @ 1,884 after 141,178,711 : Time 43.52s : 29259.25 words/s : gNorm 0.2743 : L.r. 1.6181e-04
[2022-05-23 12:02:59] Saving model weights and runtime parameters to model.transformer/model.iter55000.npz
[2022-05-23 12:02:59] Saving model weights and runtime parameters to model.transformer/model.npz
[2022-05-23 12:03:00] Saving Adam parameters
[2022-05-23 12:03:00] [training] Saving training checkpoint to model.transformer/model.npz and model.transformer/model.npz.optimizer.npz
[2022-05-23 12:03:02] [valid] Ep. 1039 : Up. 55000 : cross-entropy : 40.0774 : stalled 10 times (last best: 33.4006)
[2022-05-23 12:03:02] [valid] Ep. 1039 : Up. 55000 : perplexity : 44.8722 : stalled 10 times (last best: 23.8101)
[2022-05-23 12:03:03] [valid] Ep. 1039 : Up. 55000 : bleu : 19.245 : stalled 7 times (last best: 19.6352)
[2022-05-23 12:03:03] Training finished
[2022-05-23 12:03:03] Saving model weights and runtime parameters to model.transformer/model.npz
[2022-05-23 12:03:03] Saving Adam parameters
[2022-05-23 12:03:03] [training] Saving training checkpoint to model.transformer/model.npz and model.transformer/model.npz.optimizer.npz

real    80m43.093s
user    100m20.907s
sys     1m11.143s
```

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysh$ ls model.iter*.npz | sort -V
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
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysh$
```

Testing ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysh$ time ./test-eval.sh | tee test-eval.log
...
...
...
[2022-05-23 12:44:11] Best translation 484 : ၵွပ်ႈ ပပိူဝ်ႈ ပဵၼ် ၽူႈ မီးၸ်ႂ သတ်ႉ ထႃႇ ယုမ်ႇ ယမ် ၼၼိူဝ် ၽႃႇ သႃႇႄ လႈ မၼ်း ပဵၼ် ၽြႃး ၼၼ်ႉ ယူႇ သေႇ ယဝ်ႈ
[2022-05-23 12:44:11] Best translation 485 : လူတ်ႉ မီး ဝႆႉ ၼႂ်း ၵူဝ်ႇ ၻွင်ႇ
[2022-05-23 12:44:11] Best translation 486 : ၶေႃႈ တွပ်ႇ ဢၼ် မႂ်း တၢင်ႇ
[2022-05-23 12:44:11] Best translation 487 : ဢၼ် ၼၼ်ႉ တႃႇ မၼ်း ငႆၢႈ ငႆၢႈ ၵူၺ်း
[2022-05-23 12:44:11] Best translation 488 : ၶဝ် လလိူၵ်ႈ ၶႃႈ ဢေႃႈ
[2022-05-23 12:44:11] Best translation 489 : သူ ဢၼ် ၼႆႉ ႁူႉ ယူႇ ၼေႃ ဢမ်ႇ ႁူႉ ႁႃႉ
[2022-05-23 12:44:11] Best translation 490 : ဢၼ် ၼႆႉ ႁဝ်း ၶႃႈ တေ ႁဵတ်း လႆႈ ဢမ်ႇ ၸႂ်ႈ
[2022-05-23 12:44:11] Best translation 491 : လွင်ႈ တၢင်း ဢၼ် ၼႆႉ တေ ယုမ်ႇ ၽႂ် ၼႆ ၵဝ် ၶႃႈ ႁဵတ်း လႆႈ ႁဵၻ်း ၵႂႃႇ လႄႈ
[2022-05-23 12:44:11] Best translation 492 : သူ ၸႂ် တူင်ႉ ယူႇ ႁႃႉ
[2022-05-23 12:44:11] Best translation 493 : တၢင်း ၼွၵ်ႈ တေ မႄး ၶၶိုၼ်း တၢင်း ၼွၵ်ႈ
[2022-05-23 12:44:11] Best translation 494 : ၵဝ် ၶႃႈ ၼႂ်း ႁွင်ႈ ၼွၼ်း ၵေႃႉ လဵဝ်
[2022-05-23 12:44:11] Best translation 495 : ထၢမ် မၼ်း ၼႆႉ သသိုဝ်ႈ လူး
[2022-05-23 12:44:11] Best translation 496 : ၶၢႆ ယူႇ ယဝ်ႉ ႁႃႉ
[2022-05-23 12:44:11] Best translation 497 : ၵဝ် ၶႃႈ ၼမ်ႉ တႃ တူၵ်း ႁႃႉ
[2022-05-23 12:44:11] Best translation 498 : မမိူဝ်ႈ ဝႃး ႁဝ်း လႆႈ ၶီႇ ၼမ်ႉ ၵမ်ႉ ၼၼိုင်ႈ သူ ထၢင်ႇ ၸၸိူင်ႉ ႁႁိုဝ်
[2022-05-23 12:44:11] Best translation 499 : သူ ဢမ်ႇ ႁဵတ်း ဢီႈ သင် ႁႃႉ
[2022-05-23 12:44:11] Total time: 3.76917s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    0m47.294s
user    1m14.845s
sys     0m10.427s
```

Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysh$ cat eval-result.txt
Evaluation with hyp.iter5000.sh, Transformer model:
BLEU = 18.79, 59.4/29.5/15.2/8.8 (BP=0.853, ratio=0.863, hyp_len=4096, ref_len=4748)
Evaluation with hyp.iter10000.sh, Transformer model:
BLEU = 19.26, 59.1/29.3/15.5/9.2 (BP=0.865, ratio=0.874, hyp_len=4148, ref_len=4748)
Evaluation with hyp.iter15000.sh, Transformer model:
BLEU = 18.79, 59.0/29.3/15.0/8.6 (BP=0.864, ratio=0.873, hyp_len=4144, ref_len=4748)
Evaluation with hyp.iter20000.sh, Transformer model:
BLEU = 18.11, 58.5/28.5/14.3/7.9 (BP=0.871, ratio=0.879, hyp_len=4173, ref_len=4748)
Evaluation with hyp.iter25000.sh, Transformer model:
BLEU = 18.04, 58.2/28.3/14.3/7.7 (BP=0.874, ratio=0.881, hyp_len=4185, ref_len=4748)
Evaluation with hyp.iter30000.sh, Transformer model:
BLEU = 18.28, 58.5/28.6/14.4/8.0 (BP=0.873, ratio=0.881, hyp_len=4182, ref_len=4748)
Evaluation with hyp.iter35000.sh, Transformer model:
BLEU = 18.25, 58.1/28.3/14.3/7.9 (BP=0.880, ratio=0.886, hyp_len=4208, ref_len=4748)
Evaluation with hyp.iter40000.sh, Transformer model:
BLEU = 18.80, 58.5/28.9/14.8/8.1 (BP=0.887, ratio=0.893, hyp_len=4239, ref_len=4748)
Evaluation with hyp.iter45000.sh, Transformer model:
BLEU = 18.55, 57.7/28.2/14.5/8.0 (BP=0.890, ratio=0.896, hyp_len=4252, ref_len=4748)
Evaluation with hyp.iter50000.sh, Transformer model:
BLEU = 18.49, 57.8/28.2/14.3/7.9 (BP=0.892, ratio=0.898, hyp_len=4263, ref_len=4748)
Evaluation with hyp.iter55000.sh, Transformer model:
BLEU = 18.06, 57.7/28.0/14.0/7.6 (BP=0.886, ratio=0.892, hyp_len=4234, ref_len=4748)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysh$
```

## sh-my, Transformer

updated shell script for training sh-my:

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework
## Last updated: 23 May 2022


model_folder="model.transformer.shmy";
mkdir ${model_folder};
data_path="/home/ye/exp/my-nmt/data/4nmt/my-sh/";
src="sh"; tgt="my";

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

```bash
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.shmy.sh
...
...
...
[2022-05-23 14:36:45] [data] Done reading 13,244 sentences
[2022-05-23 14:36:45] [data] Done shuffling 13,244 sentences to temp files
[2022-05-23 14:36:49] Seen 13,244 samples
[2022-05-23 14:36:49] Starting data epoch 1257 in logical epoch 1257
[2022-05-23 14:36:49] [data] Shuffling data
[2022-05-23 14:36:49] [data] Done reading 13,244 sentences
[2022-05-23 14:36:49] [data] Done shuffling 13,244 sentences to temp files
[2022-05-23 14:36:49] Ep. 1257 : Up. 55000 : Sen. 2,219 : Cost 1.08111274 * 1,910,373 @ 1,561 after 210,518,455 : Time 45.93s : 41590.54 words/s : gNorm 0.2351 : L.r. 1.6181e-04
[2022-05-23 14:36:49] Saving model weights and runtime parameters to model.transformer.shmy/model.iter55000.npz
[2022-05-23 14:36:49] Saving model weights and runtime parameters to model.transformer.shmy/model.npz
[2022-05-23 14:36:50] Saving Adam parameters
[2022-05-23 14:36:50] [training] Saving training checkpoint to model.transformer.shmy/model.npz and model.transformer.shmy/model.npz.optimizer.npz
[2022-05-23 14:36:52] [valid] Ep. 1257 : Up. 55000 : cross-entropy : 34.3263 : stalled 10 times (last best: 27.2658)
[2022-05-23 14:36:52] [valid] Ep. 1257 : Up. 55000 : perplexity : 14.0434 : stalled 10 times (last best: 8.15546)
[2022-05-23 14:36:53] [valid] Ep. 1257 : Up. 55000 : bleu : 36.4187 : stalled 8 times (last best: 36.8577)
[2022-05-23 14:36:53] Training finished
[2022-05-23 14:36:53] Saving model weights and runtime parameters to model.transformer.shmy/model.npz
[2022-05-23 14:36:53] Saving Adam parameters
[2022-05-23 14:36:54] [training] Saving training checkpoint to model.transformer.shmy/model.npz and model.transformer.shmy/model.npz.optimizer.npz

real    84m53.517s
user    107m33.430s
sys     1m34.236s
```

Testing and Evaluation for shan-to-burmese:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.shmy$ time ./test-eval.sh
...
...
...
[2022-05-23 14:49:52] Best translation 485 : ကား က ဂဂို ဒေါင် ထဲ မှာ ရှိ တယ်
[2022-05-23 14:49:52] Best translation 486 : အ သက် စေ့ စပ် ပြ တတဲ့ အ ဖြေ
[2022-05-23 14:49:52] Best translation 487 : အအဲ့ ဒါ သသူ့ အ တွက် လွယ် လွယ် လေး ပါ
[2022-05-23 14:49:52] Best translation 488 : သူ တတိတို့ စေ့ စပ် စု ဆောင်း ထား တတဲ့ အ ထိ ရွေး ချယ် နနိုင် တယ်
[2022-05-23 14:49:52] Best translation 489 : မင်း အဲ ဒါ ကကို သိ တယ် နော် မ သိ ဘူး လား
[2022-05-23 14:49:52] Best translation 490 : အအဲ့ ဒါ ကကို ကျွန် တော် တတိတို့ လုပ် ရ မှာ မ ဟုတ် ဘူး
[2022-05-23 14:49:52] Best translation 491 : သူ ရရဲ့ အ ကြောင်း အ ရာ က တော့ ကျွန် တော် အ ကြောင်း ကကို မ လုပ် နနိုင် လိလို့ ပါ
[2022-05-23 14:49:52] Best translation 492 : မင်း စိတ် လှုပ် ရှား နေ မှာ လား
[2022-05-23 14:49:52] Best translation 493 : အ ပြင် ကြီး မှာ ရောက် ဖဖိဖို့
[2022-05-23 14:49:52] Best translation 494 : ကျွန် တော် အဲ ဒါ ကကို အိပ် ရာ ဝင် တတဲ့ အိမ် နှစ် ယောက် ကကို စိတ် ဝင် စား ပါ တယ်
[2022-05-23 14:49:52] Best translation 495 : သသူ့ ကကို မေး ကြ ည့် မှာ မ ဟုတ် ဘူး
[2022-05-23 14:49:52] Best translation 496 : ရောင်း နေ ပြီ လား
[2022-05-23 14:49:52] Best translation 497 : ကျွန် တော့် မျက် ရည် ကျ သ လား
[2022-05-23 14:49:52] Best translation 498 : မ နေ့ ည က ကျွန် တော် တတိတို့ ရေ တစ် ခ ဏ လောက် အ ဖြစ် ခခဲ့ ရ သ လဲ
[2022-05-23 14:49:52] Best translation 499 : ခင် ဗျား ဘာ မှ မ လုပ် ဘူး လား
[2022-05-23 14:49:52] Total time: 4.44460s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    0m54.624s
user    1m29.715s
sys     0m10.451s
```

Evaluation result with BLEU Score: 

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.shmy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 34.00, 70.3/46.3/33.0/25.2 (BP=0.839, ratio=0.850, hyp_len=5125, ref_len=6026)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 34.96, 70.4/46.9/33.2/25.6 (BP=0.854, ratio=0.864, hyp_len=5207, ref_len=6026)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 35.05, 70.5/47.0/33.2/25.5 (BP=0.857, ratio=0.866, hyp_len=5218, ref_len=6026)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 35.79, 70.3/46.9/33.6/26.4 (BP=0.865, ratio=0.874, hyp_len=5265, ref_len=6026)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 36.01, 70.1/47.0/33.6/26.2 (BP=0.872, ratio=0.880, hyp_len=5302, ref_len=6026)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 36.31, 69.9/46.6/34.0/26.9 (BP=0.874, ratio=0.882, hyp_len=5312, ref_len=6026)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 36.18, 69.5/46.6/33.6/26.5 (BP=0.879, ratio=0.885, hyp_len=5335, ref_len=6026)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 36.46, 69.0/46.5/33.5/26.2 (BP=0.890, ratio=0.896, hyp_len=5398, ref_len=6026)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 36.00, 69.1/46.3/33.3/25.7 (BP=0.885, ratio=0.891, hyp_len=5369, ref_len=6026)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 35.94, 68.3/45.4/32.6/25.3 (BP=0.899, ratio=0.904, hyp_len=5445, ref_len=6026)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 35.95, 68.4/45.6/32.8/25.5 (BP=0.894, ratio=0.900, hyp_len=5421, ref_len=6026)
```

## my-ch (Mizo Chin), Transformer

training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mych.sh 
...
...
...
[2022-05-23 16:18:22] [data] Done reading 12,994 sentences
[2022-05-23 16:18:22] [data] Done shuffling 12,994 sentences to temp files
[2022-05-23 16:18:27] Seen 12,994 samples
[2022-05-23 16:18:27] Starting data epoch 985 in logical epoch 985
[2022-05-23 16:18:27] [data] Shuffling data
[2022-05-23 16:18:27] [data] Done reading 12,994 sentences
[2022-05-23 16:18:27] [data] Done shuffling 12,994 sentences to temp files
[2022-05-23 16:18:31] Ep. 985 : Up. 55000 : Sen. 11,474 : Cost 1.22914517 * 1,188,560 @ 2,384 after 130,754,934 : Time 44.93s : 26450.75 words/s : gNorm 0.2012 : L.r. 1.6181e-04
[2022-05-23 16:18:31] Saving model weights and runtime parameters to model.transformer.mych/model.iter55000.npz
[2022-05-23 16:18:31] Saving model weights and runtime parameters to model.transformer.mych/model.npz
[2022-05-23 16:18:32] Saving Adam parameters
[2022-05-23 16:18:32] [training] Saving training checkpoint to model.transformer.mych/model.npz and model.transformer.mych/model.npz.optimizer.npz
[2022-05-23 16:18:34] [valid] Ep. 985 : Up. 55000 : cross-entropy : 31.5306 : stalled 10 times (last best: 26.1109)
[2022-05-23 16:18:34] [valid] Ep. 985 : Up. 55000 : perplexity : 21.8057 : stalled 10 times (last best: 12.8377)
[2022-05-23 16:18:34] [valid] Ep. 985 : Up. 55000 : bleu : 30.6599 : stalled 2 times (last best: 30.9508)
[2022-05-23 16:18:34] Training finished
[2022-05-23 16:18:34] Saving model weights and runtime parameters to model.transformer.mych/model.npz
[2022-05-23 16:18:34] Saving Adam parameters
[2022-05-23 16:18:34] [training] Saving training checkpoint to model.transformer.mych/model.npz and model.transformer.mych/model.npz.optimizer.npz

real    82m56.408s
user    102m20.336s
sys     1m3.715s
```

Testing and Evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mych$ time ./test-eval.sh
...
...
...
[2022-05-23 16:36:06] Best translation 1472 : min hmangaih emaw, hmangaih lo emaw i ngaih ?
[2022-05-23 16:36:06] Best translation 1473 : a theih alawm .
[2022-05-23 16:36:06] Best translation 1474 : anni hmuh chu i hreh deuh em ni ?
[2022-05-23 16:36:06] Best translation 1475 : i hriat ang angin ti rawh .
[2022-05-23 16:36:06] Best translation 1476 : nimin chhuna TV kan en .
[2022-05-23 16:36:06] Best translation 1477 : eng vang nge ani ( hmeichhia ) chu a titau a ?
[2022-05-23 16:36:06] Best translation 1478 : ani ( hmeichhia ) chuan hei hi a pawt thler em ni ?
[2022-05-23 16:36:06] Best translation 1479 : hei hi engtik hunah pawh nise hun a rawn tangkai ngei ang .
[2022-05-23 16:36:06] Best translation 1480 : TV en hi nuam ka ti .
[2022-05-23 16:36:06] Best translation 1481 : kum 10 vel a ni tawh .
[2022-05-23 16:36:06] Best translation 1482 : i tawng lo va .
[2022-05-23 16:36:06] Best translation 1483 : tun ang zanah te chuan anni pawhin a nawi an nei thei bik nang .
[2022-05-23 16:36:06] Best translation 1484 : ani chuan chibai a rawn tawng .
[2022-05-23 16:36:06] Best translation 1485 : hei hi zaninah a rawn kal dawn em ?
[2022-05-23 16:36:06] Best translation 1486 : naktukah i hna thar i chhuah ka ring .
[2022-05-23 16:36:06] Best translation 1487 : kan thawmhnawte hi min zarsak ta che .
[2022-05-23 16:36:06] Best translation 1488 : hei hi i lo man na nge ?
[2022-05-23 16:36:06] Total time: 10.19546s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m58.218s
user    3m23.739s
sys     0m22.046s
```

Evaluation result with BLEU Score:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mych$ cat eval-result.txt
Evaluation with hyp.iter5000.ch, Transformer model:
BLEU = 30.79, 67.0/40.7/27.7/19.7 (BP=0.882, ratio=0.889, hyp_len=12228, ref_len=13759)
Evaluation with hyp.iter10000.ch, Transformer model:
BLEU = 31.25, 66.5/40.7/27.8/19.8 (BP=0.895, ratio=0.900, hyp_len=12379, ref_len=13759)
Evaluation with hyp.iter15000.ch, Transformer model:
BLEU = 31.16, 66.4/40.4/27.8/19.8 (BP=0.894, ratio=0.899, hyp_len=12375, ref_len=13759)
Evaluation with hyp.iter20000.ch, Transformer model:
BLEU = 30.94, 66.1/40.1/27.5/19.4 (BP=0.897, ratio=0.902, hyp_len=12411, ref_len=13759)
Evaluation with hyp.iter25000.ch, Transformer model:
BLEU = 31.26, 66.2/40.4/27.6/19.6 (BP=0.901, ratio=0.906, hyp_len=12459, ref_len=13759)
Evaluation with hyp.iter30000.ch, Transformer model:
BLEU = 31.21, 66.0/40.1/27.5/19.6 (BP=0.903, ratio=0.908, hyp_len=12488, ref_len=13759)
Evaluation with hyp.iter35000.ch, Transformer model:
BLEU = 30.97, 65.9/39.9/27.2/19.4 (BP=0.903, ratio=0.907, hyp_len=12479, ref_len=13759)
Evaluation with hyp.iter40000.ch, Transformer model:
BLEU = 31.32, 66.0/40.1/27.5/19.6 (BP=0.906, ratio=0.910, hyp_len=12524, ref_len=13759)
Evaluation with hyp.iter45000.ch, Transformer model:
BLEU = 31.15, 66.0/40.0/27.2/19.2 (BP=0.909, ratio=0.913, hyp_len=12562, ref_len=13759)
Evaluation with hyp.iter50000.ch, Transformer model:
BLEU = 31.29, 66.2/40.1/27.4/19.4 (BP=0.908, ratio=0.912, hyp_len=12550, ref_len=13759)
Evaluation with hyp.iter55000.ch, Transformer model:
BLEU = 30.85, 65.8/39.7/27.0/19.0 (BP=0.907, ratio=0.911, hyp_len=12535, ref_len=13759)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mych$
```

## ch-my, Transformer

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.chmy.sh
...
...
...
[2022-05-23 18:09:41] [data] Done reading 12,994 sentences
[2022-05-23 18:09:41] [data] Done shuffling 12,994 sentences to temp files
[2022-05-23 18:09:46] Seen 12,994 samples
[2022-05-23 18:09:46] Starting data epoch 1215 in logical epoch 1215
[2022-05-23 18:09:46] [data] Shuffling data
[2022-05-23 18:09:46] [data] Done reading 12,994 sentences
[2022-05-23 18:09:46] [data] Done shuffling 12,994 sentences to temp files
[2022-05-23 18:09:49] Ep. 1215 : Up. 55000 : Sen. 9,528 : Cost 1.08088219 * 1,819,327 @ 5,381 after 200,869,489 : Time 47.12s : 38606.68 words/s : gNorm 0.2217 : L.r. 1.6181e-04
[2022-05-23 18:09:49] Saving model weights and runtime parameters to model.transformer.chmy/model.iter55000.npz
[2022-05-23 18:09:49] Saving model weights and runtime parameters to model.transformer.chmy/model.npz
[2022-05-23 18:09:49] Saving Adam parameters
[2022-05-23 18:09:49] [training] Saving training checkpoint to model.transformer.chmy/model.npz and model.transformer.chmy/model.npz.optimizer.npz
[2022-05-23 18:09:51] [valid] Ep. 1215 : Up. 55000 : cross-entropy : 33.6062 : stalled 10 times (last best: 26.756)
[2022-05-23 18:09:51] [valid] Ep. 1215 : Up. 55000 : perplexity : 14.4234 : stalled 10 times (last best: 8.37159)
[2022-05-23 18:09:51] [valid] Ep. 1215 : Up. 55000 : bleu : 36.7631 : stalled 9 times (last best: 37.657)
[2022-05-23 18:09:51] Training finished
[2022-05-23 18:09:51] Saving model weights and runtime parameters to model.transformer.chmy/model.npz
[2022-05-23 18:09:52] Saving Adam parameters
[2022-05-23 18:09:52] [training] Saving training checkpoint to model.transformer.chmy/model.npz and model.transformer.chmy/model.npz.optimizer.npz

real    87m2.904s
user    108m24.973s
sys     1m16.436s
```

Testing and Evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.chmy$ time ./test-eval.sh
...
...
...
[2022-05-23 18:15:22] Best translation 1472 : ကျွန် တော့် ကကို ချစ် တတဲ့ ကောင် မ လေး က ဘယ် လလို ထင် လဲ
[2022-05-23 18:15:22] Best translation 1473 : ရ ပါ တယ်
[2022-05-23 18:15:22] Best translation 1474 : သူ တတိတို့ ကကို တွေ့ ဖဖိဖို့ ဝန် လေး နေ တယ်
[2022-05-23 18:15:22] Best translation 1475 : မင်း သိ သ လလို လုပ် ပါ
[2022-05-23 18:15:22] Best translation 1476 : မ နေ့ နေ့ လည် က ကျွန် တော် တတိတို့ တီ ဗွီ ကြ ည့် ခခဲ့ ကြ တယ်
[2022-05-23 18:15:22] Best translation 1477 : ဘာ့ ကြော င့် သူ မ ကကို အ ရူး လုပ် တာ လဲ
[2022-05-23 18:15:22] Best translation 1478 : သူ မ အအဲ့ ဒါ ကကို ဆွဲ လလိုက် တာ လား
[2022-05-23 18:15:22] Best translation 1479 : အဲ ဒါ ကကို လွှ င့် ပစ် မ ပစ် နနိုင် သေး
[2022-05-23 18:15:22] Best translation 1480 : ကျွန် တော် တီ ဗွီ ကြ ည့် တာ ကြြိုက် တယ်
[2022-05-23 18:15:22] Best translation 1481 : ဆယ် နှစ် လောက် ရှိ ပါ ပြီ
[2022-05-23 18:15:22] Best translation 1482 : မင်း မ ပြော ဘူး
[2022-05-23 18:15:22] Best translation 1483 : ဒီ လလို ည မျျိုး မှာ အ ကြွေ မ ရှိ တော့ ဘူး
[2022-05-23 18:15:22] Best translation 1484 : သူ နှုတ် ဆက် စ ကား ပြော နေ တယ်
[2022-05-23 18:15:22] Best translation 1485 : ဒါ ဒီ ည လာ မှာ လား
[2022-05-23 18:15:22] Best translation 1486 : မ နက် ဖြန် အ လုပ် အ သစ် ကကို သွား မယ် လလိလို့ ကြား တယ်
[2022-05-23 18:15:22] Best translation 1487 : မင်း ကကို လျှော် ပြီး သား အ ကကိုင်း တွေ ကကို လှမ်း ပေး ပါ
[2022-05-23 18:15:22] Best translation 1488 : အအဲ့ ဒါ ကကို သူ မ ဖမ်း ထား လလိုက် ဘူး လား
[2022-05-23 18:15:22] Total time: 12.22413s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m19.479s
user    4m5.839s
sys     0m22.240s
```

Evaluation result with BLEU score are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.chmy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 32.78, 67.6/45.5/32.0/23.7 (BP=0.838, ratio=0.850, hyp_len=14954, ref_len=17592)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 33.76, 67.8/45.6/32.5/24.5 (BP=0.852, ratio=0.862, hyp_len=15170, ref_len=17592)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 34.08, 67.4/45.3/32.2/23.9 (BP=0.871, ratio=0.878, hyp_len=15454, ref_len=17592)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 33.98, 66.3/44.5/31.7/23.8 (BP=0.879, ratio=0.886, hyp_len=15584, ref_len=17592)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 34.08, 66.6/44.8/31.7/23.8 (BP=0.879, ratio=0.886, hyp_len=15586, ref_len=17592)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 33.72, 66.2/44.4/31.4/23.4 (BP=0.880, ratio=0.887, hyp_len=15596, ref_len=17592)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 33.83, 66.0/44.5/31.6/23.6 (BP=0.880, ratio=0.886, hyp_len=15593, ref_len=17592)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 34.06, 66.0/44.5/31.7/23.9 (BP=0.882, ratio=0.889, hyp_len=15632, ref_len=17592)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 34.14, 66.1/44.6/31.6/23.7 (BP=0.886, ratio=0.892, hyp_len=15685, ref_len=17592)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 34.18, 66.0/44.3/31.6/23.9 (BP=0.887, ratio=0.893, hyp_len=15713, ref_len=17592)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 34.12, 65.7/44.4/31.5/23.7 (BP=0.889, ratio=0.895, hyp_len=15741, ref_len=17592)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.chmy$
```

## my-sh, Seq2Seq

Training ...  

```
[2022-05-24 01:52:49] Best translation 3 : ႁဝ်း ၶႃႈ ပႂ်ႉ တူၺ်း တီႈ ၼႆ ၼႄ တၢင်း ၶႅၵ်ႇ ၼႆႉ ၼၼ်ႉ ၵွၼ်ႇ
[2022-05-24 01:52:49] Best translation 4 : ၵပ်း ၵၢႆႇ လွင်ႈ ၼႆႉ သေ ၼၼ်ႉ ဢမ် ထၢမ် ၸႃး ၼႃႇ ႁႃႉ
[2022-05-24 01:52:49] Best translation 5 : သူ ႁဵတ်း သင် ယူႇ
[2022-05-24 01:52:49] Best translation 10 : မၼ်း ၼၢင်း တေ ၶိုၼ်ႈ ယႂ်ႇ မႃး တင်း မေႃ ယႃ လူင် ၼႆ ၵႂႃႈ
[2022-05-24 01:52:49] Best translation 20 : မၼ်း ၼၢင်း ၼႆႉ တီႈ ႁဵတ်း ၵၢၼ် ၼၼ်ႉ တၼ်း မႃး ယဝ်ႉ
[2022-05-24 01:52:49] Best translation 40 : ၵဝ် ၶႃႈ ၶႆႈ လႆႈ ႁွင်ႈ သဝ်း ႁွင်ႈ ၼိုင်ႈ
[2022-05-24 01:52:49] Best translation 80 : ၵဝ် ၶႃႈ ဢၼ် ၼႆႉ လႆႈ ႁူႉ ဝႆႉ
[2022-05-24 01:52:49] Best translation 160 : မၼ်း ၼႆႉ တူၵ်း လိုၼ်း ၵၢပ်ႈ ပၢၼ် ၼႃႇ ယဝ်ႉ
[2022-05-24 01:52:49] Best translation 320 : သင် ဢမ်ႇ မီး သူႄ တႉ ၶႃႈ ဢမ်ႇ လႆႈ ထၢမ် ၶေႃႈ ထၢမ် ၸဝ်ႈ ဝႆႉ ၶေႃႈ ၼိုင်ႈ ဢေႃႈ
[2022-05-24 01:52:50] Best translation 640 : သင်မ်ႂး ဢမ်ႇ မႃး ၼႆ ၵဝ် တေၸ်ႂ ထိုင်မ်ႂး ႄ တႉႄ တႉ ၼၼ်ႉ ယဝ်ႈ
[2022-05-24 01:52:50] Best translation 1280 : ၵဝ် ထင်ႇ တႃႇ ရႃႇ သီႇ ဢု တု တေ လီ ၶိုၼ်ႈ ၼႆႉ ႁဝ်း မီး တိုဝ်ႉ တၢင်း ဝႆႉ ၶိုင်ႈ ၼိုင်ႈ ယူႇ
[2022-05-24 01:52:52] Best translation 2560 : မိူဝ်ႈ ႁဝ်း ဢမ်ႇ ယူႇ လီ ၼၼ်ႉ သူ ဢမ်ႇ ယုမ်ႇ ႁႃႉ
[2022-05-24 01:52:52] Total translation time: 3.04721s
[2022-05-24 01:52:52] [valid] Ep. 260 : Up. 60000 : bleu : 11.314 : stalled 10 times (last best: 15.5918)
[2022-05-24 01:52:52] Training finished
[2022-05-24 01:52:52] Saving model weights and runtime parameters to model.seq2seq.mysh/model.npz
[2022-05-24 01:52:55] Saving Adam parameters
[2022-05-24 01:52:55] [training] Saving training checkpoint to model.seq2seq.mysh/model.npz and model.seq2seq.mysh/model.npz.optimizer.npz

real    386m50.499s
user    455m20.978s
sys     0m43.651s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$
```

testing and evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mysh$ time ./test-eval.sh
...
...
...
[2022-05-24 11:17:26] Best translation 485 : လူတ်ႉ မီး ဝႆႉ ၼႂ်း ၵူဝ်ႇ ၻွင်ႇ
[2022-05-24 11:17:26] Best translation 486 : ၶေႃႈ တွၵ်ႇ ဢၼ် သူ သၢင်း လၢင်း ၼႄ
[2022-05-24 11:17:26] Best translation 487 : ဢၼ် ၼၼ်ႉ တႃႇ ၸၸိူဝ်း ၶဝ် ၼၼ်ႉ ငႆၢႈ ငႆၢႈ ၵူၺ်း
[2022-05-24 11:17:26] Best translation 488 : ၶဝ် ဢၼ် ၼႆႉ ဢဝ် ၵႂႃႇ ဢဢိူဝ်ႈ ၼႆ လႅပ်ႈ ဢမ်ႇ ၸႂ်ႈ
[2022-05-24 11:17:26] Best translation 489 : သူ ဢၼ် ၼႆႉ ႁူႉ ယူႇ ၼေႃ ဢမ်ႇ ႁူႉ ႁႃႉ
[2022-05-24 11:17:26] Best translation 490 : ဢၼ် ၼႆႉ ႁဝ်း ၶႃႈ တေ ၼႄ ဢမ်ႇ ၸႂ်ႈ ႁႃႉ
[2022-05-24 11:17:26] Best translation 491 : ၽႂ် ၸၸိူဝ်း လႂ် တေ လႆႈ ဢဝ် ဢွၵ်ႇ ပႅတ်ႈ ၵၢၼ် ၼႆ ႁဝ်း ၶႃႈ တေ လႆႈ ႁဵတ်း ယဝ်ႉ
[2022-05-24 11:17:26] Best translation 492 : သူ တူင်ႉ ၼၼိုင် ႁဵတ်း သင် လႃႇ
[2022-05-24 11:17:26] Best translation 493 : ၵူႈ ၽၢၵ်ႇ ၽၢၵ်ႇ လီ လလိူဝ် ယူႇ
[2022-05-24 11:17:26] Best translation 494 : ၵဝ် ၶႃႈ မီး လုၵ်ႈ ဢွၼ်ႇ ႓ ၵေႃႉ ႁႁိူၼ်း လႄႈ လူဝ်ႇ ပၼ် ၼီႈ ထႅင်ႈ ၵွၼ်ႇ
[2022-05-24 11:17:26] Best translation 495 : ထၢမ် တီႈ မၼ်း လူး
[2022-05-24 11:17:26] Best translation 496 : ၶၢႆ ယူႇ ယဝ်ႉ ႁႃႉ
[2022-05-24 11:17:26] Best translation 497 : ၵဝ် ၶႃႈ ၼမ်ႉ တႃ ဢမ်ႇ ယၢမ်ႈ တူၵ်း ႁႃႉ
[2022-05-24 11:17:26] Best translation 498 : ၼမ်ႉ ၼဵင်ႈ မၼ်း ဢမ်ႇ လလိူတ်ႇ လီ လီ သသိူဝ်ႇ တီႈ ၼွၼ်း ဢမ်ႇ ၸၸိုဝ်ႈ ၸၸိူင်ႉ ၼႆ ဢၼ် ဢွၼ်ႇ ဢၼ် ဢိတ်း လွင်ႈ ၼႆႉ သေ ပၼ် တၢင်း မႆႈ ၸႂ် ယူႇ ဢဢိူဝ်ႈ
[2022-05-24 11:17:26] Best translation 499 : ၸဝ်ႈ ဢမ်ႇ ႁဵတ်း သင် ႁႃႉ
[2022-05-24 11:17:26] Total time: 5.41033s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m19.580s
usr    2m9.064s
sys     0m17.263s
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mysh$ cat eval-result.txt
Evaluation with hyp.iter5000.sh, Transformer model:
BLEU = 12.25, 50.0/22.3/10.6/5.2 (BP=0.779, ratio=0.800, hyp_len=3799, ref_len=4748)
Evaluation with hyp.iter10000.sh, Transformer model:
BLEU = 15.82, 54.2/26.1/13.3/7.2 (BP=0.826, ratio=0.839, hyp_len=3985, ref_len=4748)
Evaluation with hyp.iter15000.sh, Transformer model:
BLEU = 14.68, 49.7/23.1/11.4/6.4 (BP=0.863, ratio=0.871, hyp_len=4137, ref_len=4748)
Evaluation with hyp.iter20000.sh, Transformer model:
BLEU = 13.16, 45.9/20.4/9.6/5.2 (BP=0.895, ratio=0.900, hyp_len=4275, ref_len=4748)
Evaluation with hyp.iter25000.sh, Transformer model:
BLEU = 13.46, 43.8/20.0/9.7/5.5 (BP=0.915, ratio=0.918, hyp_len=4361, ref_len=4748)
Evaluation with hyp.iter30000.sh, Transformer model:
BLEU = 12.38, 42.2/18.8/8.9/4.7 (BP=0.919, ratio=0.922, hyp_len=4378, ref_len=4748)
Evaluation with hyp.iter35000.sh, Transformer model:
BLEU = 12.33, 41.5/18.4/8.6/4.7 (BP=0.933, ratio=0.935, hyp_len=4440, ref_len=4748)
Evaluation with hyp.iter40000.sh, Transformer model:
BLEU = 11.66, 40.4/17.4/8.0/4.2 (BP=0.942, ratio=0.944, hyp_len=4480, ref_len=4748)
Evaluation with hyp.iter45000.sh, Transformer model:
BLEU = 11.23, 39.4/16.7/7.4/3.9 (BP=0.956, ratio=0.957, hyp_len=4545, ref_len=4748)
Evaluation with hyp.iter50000.sh, Transformer model:
BLEU = 11.10, 39.8/16.7/7.4/3.9 (BP=0.943, ratio=0.945, hyp_len=4487, ref_len=4748)
Evaluation with hyp.iter55000.sh, Transformer model:
BLEU = 11.15, 39.1/16.2/7.4/4.0 (BP=0.955, ratio=0.956, hyp_len=4541, ref_len=4748)
Evaluation with hyp.iter60000.sh, Transformer model:
BLEU = 11.16, 38.9/16.4/7.5/3.9 (BP=0.958, ratio=0.959, hyp_len=4551, ref_len=4748)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mysh$
```

## sh-my, Seq2Seq

```
[2022-05-24 11:11:52] Best translation 4 : ငါ ပြု မူ လိုက် တာ နဲ့ ပတ် သက် ပြီး တောင်း ပန် ထား တာ လား ဒါ မှ မ ဟုတ် တ ခြား အ ရေး ကြီး တဲ့ ကိစ္စ တစ် ခု များ လား
[2022-05-24 11:11:52] Best translation 5 : မင်း ဘာ တွေ ဖတ် နေ တာ လဲ
[2022-05-24 11:11:52] Best translation 10 : သူ မ သည် ထူး ခြား တဲ့ အ တွေး အ ခေါ် ရှိ တယ်
[2022-05-24 11:11:52] Best translation 20 : သူ မ က အ ရ သာ ရှိ တဲ့ ည စာ ဖြစ် လာ မှာ
[2022-05-24 11:11:52] Best translation 40 : ကျွန် တော် ဒေါ် လာ တစ် ထောင် ဝန်း ကျင် စိတ် ချ ရ တဲ့ တစ် ပတ် ရစ် ကား တစ် စီး လို ချင် တယ်
[2022-05-24 11:11:52] Best translation 80 : ကျွန် တော် တို့ အဲ့ ဒါ ကို သိ မှာ ပါ
[2022-05-24 11:11:52] Best translation 160 : သူ က သိပ် ခေတ် နောက် ကျ တာ ပဲ
[2022-05-24 11:11:52] Best translation 320 : ဒါ ပေ မ ယ့် ဘာ ပြ ဿ နာ ရှိ လို့ လဲ ဆို တာ ကျွန် တော် သူ တို့ ကို မေး ချင် တယ်
[2022-05-24 11:11:52] Best translation 640 : ငါ ပြော တာ မင်း ကြား ပုံ မ ပေါ် ဘူး
[2022-05-24 11:11:53] Best translation 1280 : ဒါ ဆို ခင် ဗျား နေ လို့ ထိုင် လို့ သိပ် ကောင်း သွား မယ် လို့ ကျွန် တော် ထင် တယ်
[2022-05-24 11:11:54] Best translation 2560 : မင်း သူ့ ကို မ တွေ့ တာ တို့ ယုံ ကြည် ကြ တယ် နော် မ ယုံ ကြည် ဘူး လား
[2022-05-24 11:11:55] Total translation time: 3.33280s
[2022-05-24 11:11:55] [valid] Ep. 281 : Up. 60000 : bleu : 27.0105 : stalled 9 times (last best: 32.5606)
[2022-05-24 11:11:55] Training finished
[2022-05-24 11:11:55] Saving model weights and runtime parameters to model.seq2seq.shmy/model.npz
[2022-05-24 11:11:57] Saving Adam parameters
[2022-05-24 11:11:58] [training] Saving training checkpoint to model.seq2seq.shmy/model.npz and model.seq2seq.shmy/model.npz.optimizer.npz

real    385m52.479s
user    453m3.194s
sys     0m44.565s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$
```

Testing and Evaluation ...  

```
[2022-05-24 11:26:54] Best translation 485 : ကား ဂဂို ဒေါင် ထဲ မှာ ကား ရှိ လား
[2022-05-24 11:26:54] Best translation 486 : မင်း အ သက် ရှင် ပြ တတဲ့ အ ဖြေ
[2022-05-24 11:26:54] Best translation 487 : အအဲ့ ဒါ သူ မ အ တွက် လွယ် လွယ် လေး ပါ
[2022-05-24 11:26:54] Best translation 488 : သူ တတိတို့ အ စား အ သောက် ကျွေး တတဲ့ အ ချိန် ထိ ခ ဏ နေ ကြ ရ အောင်
[2022-05-24 11:26:54] Best translation 489 : မင်း အဲ ဒါ ကကို သိ တယ် နော် မ သိ ဘူး လား
[2022-05-24 11:26:54] Best translation 490 : အအဲ့ ဒါ ကကို ကျွန် တော် တတိတို့ ပြ မှာ မ ဟုတ် ဘူး
[2022-05-24 11:26:54] Best translation 491 : အဲ ဒါ က ကျွန် တော် တတိတို့ မိ သား စု ကျ င့် သသုံး လာ တတဲ့ အ ကျ င့် ဟောင်း တစ် ခု ဖြစ် တယ်
[2022-05-24 11:26:54] Best translation 492 : မင်း ရရဲ့ အန် ကယ် ကကို နှုတ် မ ဆက် ဘူး လား
[2022-05-24 11:26:54] Best translation 493 : အ ပြင် ကကို ထွက် ခဲ ပါ တယ်
[2022-05-24 11:26:54] Best translation 494 : ကျွန် တော် အိမ် အ ပြန် မှာ သသူ့ အိမ် ကကို ဝင် လလိုက် တယ်
[2022-05-24 11:26:54] Best translation 495 : ဘယ် သူ တွေ နောက် ကျ မှာ လဲ
[2022-05-24 11:26:54] Best translation 496 : ရောင်း နေ ပြီ လား
[2022-05-24 11:26:55] Best translation 497 : ကျွန် တော့် မျက် ရည် က ကျ လလိလို့
[2022-05-24 11:26:55] Best translation 498 : ခင် ဗျား မ နေ့ ည က တင် ပြ သွား စွာ သိပ် ကောင်း တာ ပဲ
[2022-05-24 11:26:55] Best translation 499 : မင်း ဘာ မှ မ လုပ် ဘူး လား
[2022-05-24 11:26:55] Total time: 5.82408s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m23.991s
user    2m17.692s
sys     0m17.356s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.shmy$ time ./test-eval.sh
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.shmy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 25.10, 59.1/36.4/24.7/18.8 (BP=0.795, ratio=0.813, hyp_len=4901, ref_len=6026)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 32.45, 63.9/42.1/30.6/23.7 (BP=0.868, ratio=0.876, hyp_len=5277, ref_len=6026)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 32.96, 62.3/41.4/30.7/24.6 (BP=0.882, ratio=0.889, hyp_len=5356, ref_len=6026)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 31.42, 59.3/39.1/28.6/22.8 (BP=0.896, ratio=0.901, hyp_len=5431, ref_len=6026)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 29.85, 56.7/36.5/26.3/20.9 (BP=0.913, ratio=0.917, hyp_len=5526, ref_len=6026)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 29.56, 55.1/35.4/25.6/20.3 (BP=0.931, ratio=0.933, hyp_len=5624, ref_len=6026)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 28.91, 53.5/34.0/24.7/19.4 (BP=0.946, ratio=0.947, hyp_len=5709, ref_len=6026)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 28.51, 52.7/33.4/24.2/19.3 (BP=0.947, ratio=0.948, hyp_len=5714, ref_len=6026)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 28.46, 52.2/33.3/24.2/19.2 (BP=0.949, ratio=0.950, hyp_len=5725, ref_len=6026)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 28.20, 52.0/32.7/23.6/18.7 (BP=0.957, ratio=0.958, hyp_len=5775, ref_len=6026)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 27.95, 51.6/32.7/23.6/18.6 (BP=0.953, ratio=0.954, hyp_len=5748, ref_len=6026)
Evaluation with hyp.iter60000.my, Transformer model:
BLEU = 28.00, 51.1/32.1/23.2/18.4 (BP=0.967, ratio=0.968, hyp_len=5833, ref_len=6026)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.shmy$
```

## my-ch, Seq2Seq

Training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./seq2seq.mych.sh 
...
...
...
[2022-05-24 17:58:29] [valid] Ep. 258 : Up. 60000 : cross-entropy : 37.8913 : stalled 10 times (last best: 25.8669)
[2022-05-24 17:58:30] [valid] Ep. 258 : Up. 60000 : perplexity : 40.6069 : stalled 10 times (last best: 12.5352)
[2022-05-24 17:58:30] Translating validation set...
[2022-05-24 17:58:30] Best translation 0 : hei chu idea tha tak a ni .
[2022-05-24 17:58:30] Best translation 1 : anni chu chawlh an la dawn em ?
[2022-05-24 17:58:30] Best translation 2 : eng pawh thawk la ka dem lo vang che .
[2022-05-24 17:58:30] Best translation 3 : thil pakhat khat ka ei chak .
[2022-05-24 17:58:30] Best translation 4 : stage-ah i lam na nge ?
[2022-05-24 17:58:30] Best translation 5 : thahnem in ngai dawn a ni lo vem ni ?
[2022-05-24 17:58:30] Best translation 10 : anni chuan hei hi an zawng lo em ni ?
[2022-05-24 17:58:30] Best translation 20 : ka la hman lo .
[2022-05-24 17:58:30] Best translation 40 : sayama chuan zirlaite chu zawhna awl te a zawt ang .
[2022-05-24 17:58:30] Best translation 80 : ka au che em ?
[2022-05-24 17:58:30] Best translation 160 : eng vang nge anni chu ngaihdam i dil loh ?
[2022-05-24 17:58:30] Best translation 320 : khawngaihin dollar nga chuanna mi lu lem sawm min pe thei ang em ?
[2022-05-24 17:58:30] Total translation time: 0.55016s
[2022-05-24 17:58:30] [valid] Ep. 258 : Up. 60000 : bleu : 21.6185 : stalled 10 times (last best: 26.0684)
[2022-05-24 17:58:30] Training finished
[2022-05-24 17:58:30] Saving model weights and runtime parameters to model.seq2seq.mych/model.npz
[2022-05-24 17:58:33] Saving Adam parameters
[2022-05-24 17:58:33] [training] Saving training checkpoint to model.seq2seq.mych/model.npz and model.seq2seq.mych/model.npz.optimizer.npz

real    388m31.719s
user    456m13.256s
sys     0m41.484s
```

Testing and evaluation:  

```
[2022-05-24 20:04:50] Best translation 1473 : a theih alawm .
[2022-05-24 20:04:50] Best translation 1474 : anni hmuh chu i hreh deuh em ni ?
[2022-05-24 20:04:50] Best translation 1475 : i duh duhin ti rawh .
[2022-05-24 20:04:50] Best translation 1476 : nimin chhuna TV kan en thin .
[2022-05-24 20:04:50] Best translation 1477 : eng vang nge ani ( hmeichhia ) chu a titau thin em ni ?
[2022-05-24 20:04:50] Best translation 1478 : ani ( hmeichhia ) chu a room rawng an hnawih laiin hetiang hi a thleng ta a ni .
[2022-05-24 20:04:50] Best translation 1479 : hemi thla hian ani chu a hna tum li a pelh ang .
[2022-05-24 20:04:50] Best translation 1480 : TV en hi nuam ka ti .
[2022-05-24 20:04:50] Best translation 1481 : kum 10 vel a ni tawh .
[2022-05-24 20:04:50] Best translation 1482 : i tawng lo va .
[2022-05-24 20:04:50] Best translation 1483 : tun ang zanah te chuan anni pawhin a nawi an nei thei bik nang .
[2022-05-24 20:04:50] Best translation 1484 : ani chuan chibai a rawn sem lo .
[2022-05-24 20:04:50] Best translation 1485 : hei hi zaninah a rawn kal dawn em ?
[2022-05-24 20:04:50] Best translation 1486 : naktukah hna chungchanga interview pawimawh tak pakhatah ka kal dawn .
[2022-05-24 20:04:50] Best translation 1487 : khawngaihin thawmhnaw hi min zarsak ta che .
[2022-05-24 20:04:50] Best translation 1488 : hei hi i lo man na nge ?
[2022-05-24 20:04:50] Total time: 15.04693s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    3m15.305s
user    5m47.131s
sys     0m30.349s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mych$ time ./test-eval.sh
```

result ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mych$ cat ./eval-result.txt
Evaluation with hyp.iter5000.ch, Transformer model:
BLEU = 19.64, 58.0/29.9/18.2/11.7 (BP=0.797, ratio=0.815, hyp_len=11217, ref_len=13759)
Evaluation with hyp.iter10000.ch, Transformer model:
BLEU = 25.49, 61.6/35.0/22.8/15.8 (BP=0.859, ratio=0.868, hyp_len=11941, ref_len=13759)
Evaluation with hyp.iter15000.ch, Transformer model:
BLEU = 24.59, 57.9/32.2/21.0/14.4 (BP=0.897, ratio=0.902, hyp_len=12415, ref_len=13759)
Evaluation with hyp.iter20000.ch, Transformer model:
BLEU = 24.06, 56.1/30.5/19.8/13.4 (BP=0.927, ratio=0.930, hyp_len=12794, ref_len=13759)
Evaluation with hyp.iter25000.ch, Transformer model:
BLEU = 22.98, 54.4/28.7/18.3/12.3 (BP=0.945, ratio=0.946, hyp_len=13019, ref_len=13759)
Evaluation with hyp.iter30000.ch, Transformer model:
BLEU = 22.49, 53.6/27.9/17.7/11.9 (BP=0.949, ratio=0.951, hyp_len=13081, ref_len=13759)
Evaluation with hyp.iter35000.ch, Transformer model:
BLEU = 21.76, 52.3/26.7/16.8/11.3 (BP=0.960, ratio=0.961, hyp_len=13219, ref_len=13759)
Evaluation with hyp.iter40000.ch, Transformer model:
BLEU = 21.80, 52.0/26.5/16.7/11.1 (BP=0.970, ratio=0.970, hyp_len=13351, ref_len=13759)
Evaluation with hyp.iter45000.ch, Transformer model:
BLEU = 21.43, 51.3/26.2/16.4/10.7 (BP=0.974, ratio=0.974, hyp_len=13405, ref_len=13759)
Evaluation with hyp.iter50000.ch, Transformer model:
BLEU = 21.30, 51.2/25.9/16.2/10.6 (BP=0.975, ratio=0.975, hyp_len=13416, ref_len=13759)
Evaluation with hyp.iter55000.ch, Transformer model:
BLEU = 21.35, 51.3/25.9/16.2/10.8 (BP=0.972, ratio=0.972, hyp_len=13374, ref_len=13759)
Evaluation with hyp.iter60000.ch, Transformer model:
BLEU = 21.01, 50.9/25.5/15.9/10.4 (BP=0.977, ratio=0.977, hyp_len=13447, ref_len=13759)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.mych$
```

## Training for ch-my, Seq2Seq

```
[2022-05-25 02:33:29] [valid] Ep. 283 : Up. 60000 : perplexity : 18.2232 : stalled 10 times (last best: 6.36893)
[2022-05-25 02:33:29] Translating validation set...
[2022-05-25 02:33:30] Best translation 0 : ဒါ တ ကယ် ကောင်း တဲ့ အ ကြံ ဉာဏ် ပါ ပဲ
[2022-05-25 02:33:30] Best translation 1 : သူ တို့ အ နား ယူ ကြ ရဲ့ လား
[2022-05-25 02:33:30] Best translation 2 : ကျွန် တော် တို့ ဘာ မှ ရ ဖို့ မ လို အပ် တော့ ပါ ဘူး
[2022-05-25 02:33:30] Best translation 3 : တစ် ခု သ တိ ပေး ပါ ရ စေ
[2022-05-25 02:33:30] Best translation 4 : ဓါတ် ပုံ ရိုက် ဖို့ အ သ င့် မ ဖြစ် သေး ဘူး လား
[2022-05-25 02:33:30] Best translation 5 : ကျွန် တော် တို့ ထပ် ကြိုး စား မှာ မ ဟုတ် ဘူး လား
[2022-05-25 02:33:30] Best translation 10 : သူ တို့ အဲ့ ဒါ ကို မ ပြောင်း လိုက် ဘူး လား
[2022-05-25 02:33:30] Best translation 20 : ကျွန် တော် အ ခု ပျော် ပွဲ စား သွား တော့ မယ်
[2022-05-25 02:33:30] Best translation 40 : ဆ ရာ မ က ကျောင်း သား တွေ ကို လွယ် တဲ့ မေး ခွန်း မေး လိ မ့် မယ်
[2022-05-25 02:33:30] Best translation 80 : ငါ မင်း ကို မျက် နှာ သာ မ ပေး ခဲ့ လို့ လား
[2022-05-25 02:33:30] Best translation 160 : မင်း ဘာ့ ကြော င့် သူ မ ကို မ တောင်း ပန် တာ လဲ
[2022-05-25 02:33:30] Best translation 320 : ကျေး ဇူး ပြု ပြီး ခ ဏ လောက် ဖုန်း ကိုင် ထား ပေး ပါ ဦး
[2022-05-25 02:33:30] Total translation time: 0.59955s
[2022-05-25 02:33:30] [valid] Ep. 283 : Up. 60000 : bleu : 29.7934 : stalled 9 times (last best: 32.7955)
[2022-05-25 02:33:30] Training finished
[2022-05-25 02:33:30] Saving model weights and runtime parameters to model.seq2seq.chmy/model.npz
[2022-05-25 02:33:33] Saving Adam parameters
[2022-05-25 02:33:33] [training] Saving training checkpoint to model.seq2seq.chmy/model.npz and model.seq2seq.chmy/model.npz.optimizer.npz

real    385m44.428s
user    451m1.428s
sys     0m42.141s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./seq2seq.chmy.sh
```

Testing and evaluation ...  

```
[2022-05-25 06:51:49] Best translation 1473 : ရ ပါ တယ်
[2022-05-25 06:51:49] Best translation 1474 : သူ တတိတို့ ကကို တွေ့ ဖဖိဖို့ ဝန် လေး နေ လား
[2022-05-25 06:51:49] Best translation 1475 : ခင် ဗျား ကြြိုက် သ လလို လုပ် ပါ
[2022-05-25 06:51:49] Best translation 1476 : မ နေ့ က ကျွန် တော် ရုပ် ရှင် ကြ ည့် ခခဲ့ တယ်
[2022-05-25 06:51:49] Best translation 1477 : ဘာ့ ကြော င့် သူ မ ကကို တတိုင် ပင် ခခဲ့ တာ လဲ
[2022-05-25 06:51:49] Best translation 1478 : သူ မ အအဲ့ ဒါ ကကို မ ရွေး ခခဲ့ ဘူး လား
[2022-05-25 06:51:49] Best translation 1479 : ကု လား အုပ် ဟာ ကြီး ကျယ် တတဲ့ ဝန် ကကို သယ် ဆောင် နေ တယ်
[2022-05-25 06:51:49] Best translation 1480 : ကျွန် တော် တီ ဗွီ ကြ ည့် တာ ကြြိုက် တယ်
[2022-05-25 06:51:49] Best translation 1481 : ဆယ် နှစ် လောက် ရှိ ပါ ပြီ
[2022-05-25 06:51:49] Best translation 1482 : မင်း စ ကား မ ပြော ဘူး
[2022-05-25 06:51:49] Best translation 1483 : ဒီ လလို ည အ ချိန် ခါ မှာ သူ တတိတို့ အ ကြွေ မ ရှိ နနိုင် တော့ ဘူး
[2022-05-25 06:51:49] Best translation 1484 : သူ စ ကား ပြော နေ တာ
[2022-05-25 06:51:49] Best translation 1485 : အဲ ဒါ ဒီ ည လာ မှာ လား
[2022-05-25 06:51:49] Best translation 1486 : ခင် ဗျား မ နက် ဖြန် က အ လုပ် သစ် ရှာ ရ ရင် ကောင်း မ လား လလိလို့ စဉ်း စား နေ တယ်
       [2022-05-25 06:51:49] Best translation 1487 : ကျေး ဇူး ပြု ပြီး လျှော် ပြီး သား အ ဝတ် တွေ ကကို လှမ်း ပေး ပါ
[2022-05-25 06:51:49] Best translation 1488 : အအဲ့ ဒါ ကကို သူ မ ဖမ်း ထား လလိုက် ဘူး လား
[2022-05-25 06:51:49] Total time: 16.23311s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    3m26.542s
user    6m9.200s
sys     0m30.527s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.chmy$ time ./test-eval.sh
```

results:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.chmy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 23.71, 61.6/37.5/24.9/17.8 (BP=0.745, ratio=0.773, hyp_len=13593, ref_len=17592)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 29.73, 63.0/41.2/29.5/22.7 (BP=0.818, ratio=0.833, hyp_len=14654, ref_len=17592)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 31.00, 61.8/40.7/29.8/23.3 (BP=0.853, ratio=0.862, hyp_len=15171, ref_len=17592)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 31.15, 59.4/39.2/28.7/22.7 (BP=0.887, ratio=0.893, hyp_len=15709, ref_len=17592)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 29.71, 57.0/36.9/26.6/20.9 (BP=0.903, ratio=0.908, hyp_len=15968, ref_len=17592)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 29.09, 55.5/35.6/25.4/19.8 (BP=0.922, ratio=0.924, hyp_len=16263, ref_len=17592)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 28.97, 54.8/35.2/25.3/19.8 (BP=0.924, ratio=0.927, hyp_len=16305, ref_len=17592)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 28.30, 54.1/34.5/24.7/19.3 (BP=0.921, ratio=0.924, hyp_len=16252, ref_len=17592)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 28.74, 53.7/34.4/24.6/19.3 (BP=0.939, ratio=0.941, hyp_len=16558, ref_len=17592)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 28.14, 53.0/33.7/24.0/18.7 (BP=0.941, ratio=0.942, hyp_len=16576, ref_len=17592)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 28.05, 52.5/33.2/23.6/18.5 (BP=0.950, ratio=0.951, hyp_len=16729, ref_len=17592)
Evaluation with hyp.iter60000.my, Transformer model:
BLEU = 27.59, 51.9/32.5/23.1/17.9 (BP=0.954, ratio=0.955, hyp_len=16801, ref_len=17592)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.seq2seq.chmy$
```

## my-po, Transformer

Training ...  

```
[2022-05-25 08:24:08] [data] Done reading 14,683 sentences                                                            [2022-05-25 08:24:08] [data] Done shuffling 14,683 sentences to temp files                                            [2022-05-25 08:24:13] Seen 14,683 samples                                                                             [2022-05-25 08:24:13] Starting data epoch 932 in logical epoch 932                                                    [2022-05-25 08:24:13] [data] Shuffling data                                                                           [2022-05-25 08:24:13] [data] Done reading 14,683 sentences                                                            [2022-05-25 08:24:13] [data] Done shuffling 14,683 sentences to temp files                                            [2022-05-25 08:24:17] Ep. 932 : Up. 55000 : Sen. 11,078 : Cost 1.19751966 * 1,383,939 @ 2,627 after 152,783,168 : Time 43.43s : 31863.49 words/s : gNorm 0.2974 : L.r. 1.6181e-04                                                           [2022-05-25 08:24:17] Saving model weights and runtime parameters to model.transformer.mypo/model.iter55000.npz       [2022-05-25 08:24:17] Saving model weights and runtime parameters to model.transformer.mypo/model.npz                 [2022-05-25 08:24:17] Saving Adam parameters                                                                          [2022-05-25 08:24:17] [training] Saving training checkpoint to model.transformer.mypo/model.npz and model.transformer.mypo/model.npz.optimizer.npz                                                                                          [2022-05-25 08:24:19] [valid] Ep. 932 : Up. 55000 : cross-entropy : 35.0058 : stalled 10 times (last best: 28.6436)   [2022-05-25 08:24:19] [valid] Ep. 932 : Up. 55000 : perplexity : 24.2252 : stalled 10 times (last best: 13.5732)      [2022-05-25 08:24:20] [valid] Ep. 932 : Up. 55000 : bleu : 30.6819 : stalled 10 times (last best: 30.9519)            [2022-05-25 08:24:20] Training finished                                                                               [2022-05-25 08:24:20] Saving model weights and runtime parameters to model.transformer.mypo/model.npz                 [2022-05-25 08:24:21] Saving Adam parameters                                                                          [2022-05-25 08:24:21] [training] Saving training checkpoint to model.transformer.mypo/model.npz and model.transformer.mypo/model.npz.optimizer.npz                                                                                                                                                                                                                real    80m29.773s                                                                                                    user    100m2.556s                                                                                                    sys     1m16.578s                                                                                                     (marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mypo.sh 
```

testing and evaluation with test data:  

```
[2022-05-25 08:54:44] Best translation 1818 : ခွေ အ တာႏ ဒွွိုႏ ဗာႏ သွတ် နဝ်ꩻ အ ဆင်ႏ ပြေႏ ဒျာႏ
[2022-05-25 08:54:44] Best translation 1819 : နာꩻ အဝ်ႏ လလိုႏ အအုံ ပ ဆား
[2022-05-25 08:54:44] Best translation 1820 : ယယို ခါꩻ ထထဲ့ꩻ ဆဆုဲင်ꩻ ထထိုꩻ လဲဉ်း
[2022-05-25 08:54:44] Best translation 1821 : ဝွေꩻ မူႏ တ ပေ့ꩻ တဝ်း တ ခါꩻ
[2022-05-25 08:54:44] Best translation 1822 : ခွေ အအုံ လမ်း ယယို ကကို နဝ်ꩻ အဝ်ႏ လဲဉ်း တ ဆီ
[2022-05-25 08:54:44] Best translation 1823 : နီ အဝ်ႏ ဒေါ့ꩻ နယ် ရေ သန် သန် အ ကျောင်ꩻ လ ဒျာႏ
[2022-05-25 08:54:44] Best translation 1824 : ခွေ မွွိုး နဝ်ꩻ နုတ် ဆက် ဝင်ꩻ စူ နဝ်ꩻ ငွွိုး ထာꩻ
[2022-05-25 08:54:44] Best translation 1825 : ဝွေꩻ အဝ်ႏ ထောင် တ ဖူꩻ တွင်ꩻ နဝ်ꩻ ရရိုင်ꩻ ငါႏ
[2022-05-25 08:54:44] Best translation 1826 : နာꩻ နား ဟွွိုန် တ စု သာႏ ဖဖုံႏ ကကို နဝ်ꩻ ထွာ နေ ဟောင်း
[2022-05-25 08:54:44] Best translation 1827 : ယယို ခါꩻ ငတ်ꩻ နား ရီႏ အဝ်ႏ လဲဉ်း
[2022-05-25 08:54:44] Best translation 1828 : ကွပ် ထွာ တိ ရေ ပီ တဲင်ꩻ တွော့ꩻ
[2022-05-25 08:54:44] Best translation 1829 : ခွေ ဖေႏ ဗာႏ သီ ဒုက္ခ ဟောင်း
[2022-05-25 08:54:44] Best translation 1830 : နီ ဖာ နဝ်ꩻ တ ခိန်ႏ လွုမ်း ဒေါ့ꩻ ရီ ဒျာႏ ခွေ တွမ်ႏ အင်္ဂ လိပ်
[2022-05-25 08:54:44] Best translation 1831 : အွွိုး အ မွူး သူꩻ လောင်း ကား က အဝ်ႏ တ ဖြြုံႏ ငါꩻ တတဲ့ တ အဝ်ႏ တဝ်း
[2022-05-25 08:54:44] Best translation 1832 : နာꩻ ထူႏ ယင်း ဟန် အအို ထ ပေႏ ဆေ့ ဆေ့ ဟောင်း
[2022-05-25 08:54:44] Best translation 1833 : ဟန် နေင်ႏ က လလိလို့ ကကုဲင် မွေး စွဉ်ႏ ထာꩻ နောႏ
[2022-05-25 08:54:44] Best translation 1834 : ပွွိုး ထ မမုဲင်ꩻ အွဉ်ႏ ဖေင်ꩻ ဟောင်း
[2022-05-25 08:54:44] Total time: 13.09760s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m31.265s
user    4m25.408s
sys     0m25.758s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mypo$ time ./test-eval.sh
```

results are as follows:

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mypo$ cat eval-result.txt
Evaluation with hyp.iter5000.po, Transformer model:
BLEU = 30.45, 70.5/42.3/25.9/16.5 (BP=0.906, ratio=0.911, hyp_len=16792, ref_len=18442)
Evaluation with hyp.iter10000.po, Transformer model:
BLEU = 30.55, 70.3/42.2/25.9/16.5 (BP=0.910, ratio=0.914, hyp_len=16850, ref_len=18442)
Evaluation with hyp.iter15000.po, Transformer model:
BLEU = 30.45, 70.2/42.1/25.8/16.4 (BP=0.910, ratio=0.914, hyp_len=16858, ref_len=18442)
Evaluation with hyp.iter20000.po, Transformer model:
BLEU = 30.77, 70.2/42.1/25.7/16.2 (BP=0.923, ratio=0.926, hyp_len=17081, ref_len=18442)
Evaluation with hyp.iter25000.po, Transformer model:
BLEU = 30.43, 69.7/41.7/25.5/16.1 (BP=0.921, ratio=0.924, hyp_len=17041, ref_len=18442)
Evaluation with hyp.iter30000.po, Transformer model:
BLEU = 30.47, 69.5/41.6/25.4/15.9 (BP=0.927, ratio=0.929, hyp_len=17138, ref_len=18442)
Evaluation with hyp.iter35000.po, Transformer model:
BLEU = 30.70, 69.8/41.9/25.7/16.2 (BP=0.924, ratio=0.927, hyp_len=17098, ref_len=18442)
Evaluation with hyp.iter40000.po, Transformer model:
BLEU = 30.42, 69.5/41.4/25.3/15.8 (BP=0.930, ratio=0.932, hyp_len=17193, ref_len=18442)
Evaluation with hyp.iter45000.po, Transformer model:
BLEU = 30.52, 69.7/41.7/25.4/15.9 (BP=0.927, ratio=0.929, hyp_len=17141, ref_len=18442)
Evaluation with hyp.iter50000.po, Transformer model:
BLEU = 30.51, 69.7/41.7/25.4/15.9 (BP=0.927, ratio=0.929, hyp_len=17135, ref_len=18442)
Evaluation with hyp.iter55000.po, Transformer model:
BLEU = 30.54, 69.5/41.7/25.5/16.0 (BP=0.925, ratio=0.928, hyp_len=17113, ref_len=18442)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mypo$
```

## po-my, Transformer

Training ...  

```
[2022-05-25 10:24:14] [data] Done reading 14,683 sentences
[2022-05-25 10:24:14] [data] Done shuffling 14,683 sentences to temp files
[2022-05-25 10:24:19] Seen 14,683 samples
[2022-05-25 10:24:19] Starting data epoch 1103 in logical epoch 1103
[2022-05-25 10:24:19] [data] Shuffling data
[2022-05-25 10:24:19] [data] Done reading 14,683 sentences
[2022-05-25 10:24:19] [data] Done shuffling 14,683 sentences to temp files
[2022-05-25 10:24:21] Ep. 1103 : Up. 55000 : Sen. 8,416 : Cost 1.08669972 * 1,814,587 @ 2,782 after 200,132,480 : Time 45.47s : 39905.99 words/s : gNorm 0.2903 : L.r. 1.6181e-04
[2022-05-25 10:24:21] Saving model weights and runtime parameters to model.transformer.pomy/model.iter55000.npz
[2022-05-25 10:24:21] Saving model weights and runtime parameters to model.transformer.pomy/model.npz
[2022-05-25 10:24:22] Saving Adam parameters
[2022-05-25 10:24:22] [training] Saving training checkpoint to model.transformer.pomy/model.npz and model.transformer.pomy/model.npz.optimizer.npz
[2022-05-25 10:24:24] [valid] Ep. 1103 : Up. 55000 : cross-entropy : 28.254 : stalled 10 times (last best: 22.1105)
[2022-05-25 10:24:24] [valid] Ep. 1103 : Up. 55000 : perplexity : 10.2207 : stalled 10 times (last best: 6.16566)
[2022-05-25 10:24:25] [valid] Ep. 1103 : Up. 55000 : bleu : 41.0474 : stalled 8 times (last best: 41.9958)
[2022-05-25 10:24:25] Training finished
[2022-05-25 10:24:25] Saving model weights and runtime parameters to model.transformer.pomy/model.npz
[2022-05-25 10:24:25] Saving Adam parameters
[2022-05-25 10:24:25] [training] Saving training checkpoint to model.transformer.pomy/model.npz and model.transformer.pomy/model.npz.optimizer.npz

real    84m6.604s
user    105m53.008s
sys     1m24.719s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.pomy.sh
```

Testing and evaluation ...  

```
[2022-05-25 10:38:13] Best translation 1818 : ငါ အ တွက် အ ချက် အ ပြုတ် ရ တာ အ ဆင် ပြေ ပါ တယ်
[2022-05-25 10:38:13] Best translation 1819 : မင်း အ နား ယူ သ င့် တယ်
[2022-05-25 10:38:13] Best translation 1820 : အ ခု တောင် ကျ နေ ပြီ
[2022-05-25 10:38:13] Best translation 1821 : သူ မ တံ ခါး မ ပိတ် ခဲ့ ဘူး
[2022-05-25 10:38:13] Best translation 1822 : ငါ အိမ် မှာ တစ် ရက် တာ ၁ ၀ နှစ် ကြာ ပြီ
[2022-05-25 10:38:13] Best translation 1823 : ပ ညာ အ ရေး ကြီး တာ ငါ တို့ စ ကား ပြော ကြ တော့
[2022-05-25 10:38:13] Best translation 1824 : ငါ လက် ဝှေ့ သ မျှ ကို နှုတ် ဆက် ပြ ဖို့ အ မေ က ငို တယ်
[2022-05-25 10:38:13] Best translation 1825 : သူ လမ်း ပေါ် မှာ လမ်း လျှောက် ခဲ့ တယ်
[2022-05-25 10:38:13] Best translation 1826 : မင်း ရဲ့ မိ ဘ တွေ ထဲ မှာ ရော ဂါ ရှိ သ လား
[2022-05-25 10:38:13] Best translation 1827 : အ ခု ၅ နာ ရီ ရှိ ပြီ ဆို ရင် ပေါ့ စ ရာ သွား ဖို့ လို ပါ ပြီ
[2022-05-25 10:38:13] Best translation 1828 : ဝမ်း သာ တဲ့ အ တွက် ကြော င့်
[2022-05-25 10:38:13] Best translation 1829 : သေ ငါ မင်း တို့ ကို ဒုက္ခ ပေး လိုက် လား
[2022-05-25 10:38:13] Best translation 1830 : ငါ အ ဖေ က ငါ ကို အင်္ဂ လိပ် လို ပြော တယ်
[2022-05-25 10:38:13] Best translation 1831 : ဟော ဟို အ ပင် ပေါ် မှာ ဘီး တစ် လုံး မှ မ ရှိ ဘူး
[2022-05-25 10:38:13] Best translation 1832 : မင်း ငါး ဟင်း နည်း နည်း ယူ ပါ ဦး လား
[2022-05-25 10:38:13] Best translation 1833 : ဒီ နှစ် အား လုံး မြန် မြန် ကြီး သွား တယ် နော်
[2022-05-25 10:38:13] Best translation 1834 : ဘယ် လို အ မေ့ မ လဲ
[2022-05-25 10:38:13] Total time: 14.32560s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m42.266s
user    4m46.917s
sys     0m26.300s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.pomy$ time ./test-eval.sh
```

Results are as follows:

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.pomy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 40.80, 75.4/52.4/38.8/29.8 (BP=0.882, ratio=0.889, hyp_len=18395, ref_len=20700)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 41.63, 75.7/53.0/39.4/30.4 (BP=0.889, ratio=0.895, hyp_len=18526, ref_len=20700)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 41.50, 75.3/52.6/39.1/30.1 (BP=0.893, ratio=0.898, hyp_len=18587, ref_len=20700)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 40.97, 74.9/51.8/38.2/29.2 (BP=0.899, ratio=0.904, hyp_len=18705, ref_len=20700)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 41.60, 74.6/52.1/38.7/29.7 (BP=0.905, ratio=0.909, hyp_len=18815, ref_len=20700)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 41.14, 74.2/51.5/38.0/29.0 (BP=0.908, ratio=0.912, hyp_len=18886, ref_len=20700)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 41.24, 74.4/51.6/38.1/29.1 (BP=0.908, ratio=0.912, hyp_len=18881, ref_len=20700)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 41.40, 74.5/51.9/38.5/29.4 (BP=0.905, ratio=0.909, hyp_len=18825, ref_len=20700)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 41.55, 74.2/51.6/38.2/29.3 (BP=0.913, ratio=0.916, hyp_len=18970, ref_len=20700)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 41.76, 74.4/51.8/38.6/29.8 (BP=0.910, ratio=0.914, hyp_len=18925, ref_len=20700)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 41.71, 74.1/51.7/38.5/29.6 (BP=0.912, ratio=0.916, hyp_len=18963, ref_len=20700)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.pomy$
```

## my-sk, word unit, Transformer

Training ...  

```
[2022-05-25 14:26:27] [data] Done reading 48,000 sentences
[2022-05-25 14:26:28] [data] Done shuffling 48,000 sentences to temp files
[2022-05-25 14:27:39] Seen 48,000 samples
[2022-05-25 14:27:39] Starting data epoch 188 in logical epoch 188
[2022-05-25 14:27:39] [data] Shuffling data
[2022-05-25 14:27:39] [data] Done reading 48,000 sentences
[2022-05-25 14:27:39] [data] Done shuffling 48,000 sentences to temp files
[2022-05-25 14:28:01] Ep. 188 : Up. 55000 : Sen. 14,726 : Cost 1.65519023 * 336,622 @ 464 after 37,179,477 : Time 121.14s : 2778.86 words/s : gNorm 0.4957 : L.r. 1.6181e-04
[2022-05-25 14:28:01] Saving model weights and runtime parameters to model.transformer.mysk/model.iter55000.npz
[2022-05-25 14:28:01] Saving model weights and runtime parameters to model.transformer.mysk/model.npz
[2022-05-25 14:28:03] Saving Adam parameters
[2022-05-25 14:28:03] [training] Saving training checkpoint to model.transformer.mysk/model.npz and model.transformer.mysk/model.npz.optimizer.npz
[2022-05-25 14:28:11] [valid] Ep. 188 : Up. 55000 : cross-entropy : 51.4726 : stalled 10 times (last best: 46.009)
[2022-05-25 14:28:12] [valid] Ep. 188 : Up. 55000 : perplexity : 3278.78 : stalled 10 times (last best: 1388.45)
[2022-05-25 14:28:17] [valid] Ep. 188 : Up. 55000 : bleu : 0.653251 : stalled 10 times (last best: 1.44581)
[2022-05-25 14:28:17] Training finished
[2022-05-25 14:28:17] Saving model weights and runtime parameters to model.transformer.mysk/model.npz
[2022-05-25 14:28:19] Saving Adam parameters
[2022-05-25 14:28:20] [training] Saving training checkpoint to model.transformer.mysk/model.npz and model.transformer.mysk/model.npz.optimizer.npz

real    225m23.144s
user    245m54.821s
sys     1m7.813s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mysk.sh
```

testing and evaluation:

```
[2022-05-25 14:38:39] Best translation 6841 : အဝဲသ့ၣ် လၢအလီၤဘှံး သနာ်က့ အဝဲသ့ၣ် မၤတၢ် ဆူညါ န့ၢ်ဝဲလီၤ
[2022-05-25 14:38:39] Best translation 6842 : နဆိကမိၣ်လၢ အဝဲကအဲၣ်ဝဲယၤ န့ၣ်ဧါ
[2022-05-25 14:38:39] Best translation 6843 : ပဝဲသ့ၣ် ပတကးတံာ်ဝဲ ပဲတြီဘၣ်ဧါ
[2022-05-25 14:38:39] Best translation 6844 : တမ့ၢ်အဝဲအသ့ၣ်နီၣ်ဝဲ တၢ်လၢပဝဲသ့ၣ်ဘၣ်တၢ်ကဲထီၣ်ဝဲတဖၣ် န့ၣ်ဘၣ်
[2022-05-25 14:38:39] Best translation 6845 : ယတၢ်ပီးတၢ်လီၤတဖၣ် ဘၣ်စီၣ်လၢာ်လံၤ
[2022-05-25 14:38:39] Best translation 6846 : ဘၣ်မနုၤအဃိ တမၤဝဲတၢ်မၤ ဖဲန့ၣ်လဲၣ်လဲၣ်
[2022-05-25 14:38:39] Best translation 6847 : မုၢ်လၢ်တဃးလၢ အိၣ်ဒၣ် ကအိၣ်ဘှံးဝဲန့ၣ်လီၤ
[2022-05-25 14:38:39] Best translation 6848 : တလါ
[2022-05-25 14:38:39] Best translation 6849 : တမ့ၢ်အဝဲ ကသံကွၢ်ဝဲ ယၤဘၣ်
[2022-05-25 14:38:39] Best translation 6850 : ခဲမုၢ်ဆ့ၣ်ဟါ မ့ၢ်ချူးန့ၣ်ဒီး ယၤဒီးယမါ အဲၣ်ဒီးကွဲမုာ်ဝဲလၢ ဟါတၢ်အီၣ်အဂီၢန့ၣ်လီၤ
[2022-05-25 14:38:39] Best translation 6851 : ယပျံၤဝဲအဃိ ယခီၣ်လ့ၢ်ခိၣ် ကနိးဝဲန့ၣ်လီၤ
[2022-05-25 14:38:39] Best translation 6852 : ယတပျံၤဝဲ တၢ်မနုၤမးန့ၣ်ဘၣ်
[2022-05-25 14:38:39] Best translation 6853 : တၢ်စံးဆၢလၢ နတူၢ်လိာ်ဝဲ
[2022-05-25 14:38:39] Best translation 6854 : တၢ်ဂဲၤကလံၣ်မူး အိၣ်သးဒ်လဲၣ်
[2022-05-25 14:38:39] Best translation 6855 : ပိာ်မုၣ်ဖိလၢ အဲၣ်ဝဲယၤန့ၣ် နဆိကမိၣ်ဝဲဒ်လဲၣ်
[2022-05-25 14:38:39] Best translation 6856 : တၢ်ကူတၢ်ကၤတဖၣ် ဃံလၤဝဲဒိၣ်မးလီၤ
[2022-05-25 14:38:39] Total time: 37.59026s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    7m18.286s
user    12m48.478s
sys     1m26.700s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysk$ time ./test-eval.sh
```

Results with my-sk, word unit are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysk$ cat eval-result.txt
Evaluation with hyp.iter5000.sk, Transformer model:
BLEU = 1.37, 14.6/3.3/1.6/0.8 (BP=0.488, ratio=0.582, hyp_len=21463, ref_len=36850)
Evaluation with hyp.iter10000.sk, Transformer model:
BLEU = 0.51, 11.0/1.4/0.5/0.2 (BP=0.481, ratio=0.577, hyp_len=21270, ref_len=36850)
Evaluation with hyp.iter15000.sk, Transformer model:
BLEU = 0.51, 11.0/1.5/0.5/0.2 (BP=0.487, ratio=0.582, hyp_len=21441, ref_len=36850)
Evaluation with hyp.iter20000.sk, Transformer model:
BLEU = 0.52, 11.1/1.5/0.5/0.2 (BP=0.490, ratio=0.584, hyp_len=21505, ref_len=36850)
Evaluation with hyp.iter25000.sk, Transformer model:
BLEU = 0.52, 11.0/1.5/0.5/0.2 (BP=0.491, ratio=0.584, hyp_len=21526, ref_len=36850)
Evaluation with hyp.iter30000.sk, Transformer model:
BLEU = 0.46, 11.1/1.5/0.4/0.1 (BP=0.490, ratio=0.584, hyp_len=21515, ref_len=36850)
Evaluation with hyp.iter35000.sk, Transformer model:
BLEU = 0.48, 11.0/1.5/0.4/0.1 (BP=0.492, ratio=0.585, hyp_len=21551, ref_len=36850)
Evaluation with hyp.iter40000.sk, Transformer model:
BLEU = 0.30, 11.0/1.5/0.3/0.0 (BP=0.491, ratio=0.585, hyp_len=21546, ref_len=36850)
Evaluation with hyp.iter45000.sk, Transformer model:
BLEU = 0.50, 10.9/1.4/0.4/0.2 (BP=0.491, ratio=0.585, hyp_len=21539, ref_len=36850)
Evaluation with hyp.iter50000.sk, Transformer model:
BLEU = 0.47, 10.9/1.4/0.4/0.1 (BP=0.491, ratio=0.584, hyp_len=21537, ref_len=36850)
Evaluation with hyp.iter55000.sk, Transformer model:
BLEU = 0.36, 10.9/1.4/0.4/0.1 (BP=0.491, ratio=0.584, hyp_len=21534, ref_len=36850)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysk$
```

## my-sk, syllable unit, Transformer

preprocessing:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/data/4nmt$ mv my-sk my-sk-word
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/data/4nmt$ mv my-sk-syl my-sk
```

inside script:  

```bash
model_folder="model.transformer.mysk.syl";
mkdir ${model_folder};
data_path="/home/ye/exp/my-nmt/data/4nmt/my-sk/";
src="my"; tgt="sk";
```

vocab building:

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/data/4nmt/my-sk$ marian-vocab < ./train-dev.my > ./vocab/vocab.my.yml
[2022-05-25 14:45:19] Creating vocabulary...
[2022-05-25 14:45:19] [data] Creating vocabulary stdout from stdin
[2022-05-25 14:45:19] Finished
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/data/4nmt/my-sk$ marian-vocab < ./train-dev.sk > ./vocab/vocab.sk.yml
[2022-05-25 14:45:33] Creating vocabulary...
[2022-05-25 14:45:33] [data] Creating vocabulary stdout from stdin
[2022-05-25 14:45:33] Finished
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/data/4nmt/my-sk$
```

Training ...  

```
[2022-05-25 16:10:55] [data] Done reading 48,000 sentences
[2022-05-25 16:10:55] [data] Done shuffling 48,000 sentences to temp files
[2022-05-25 16:11:10] Seen 48,000 samples
[2022-05-25 16:11:10] Starting data epoch 318 in logical epoch 318
[2022-05-25 16:11:10] [data] Shuffling data
[2022-05-25 16:11:10] [data] Done reading 48,000 sentences
[2022-05-25 16:11:10] [data] Done shuffling 48,000 sentences to temp files
[2022-05-25 16:11:25] Ep. 318 : Up. 55000 : Sen. 47,100 : Cost 1.23544228 * 1,848,738 @ 3,877 after 204,187,244 : Time 44.26s : 41765.58 words/s : gNorm 0.4605 : L.r. 1.6181e-04
[2022-05-25 16:11:25] Saving model weights and runtime parameters to model.transformer.mysk.syl/model.iter55000.npz
[2022-05-25 16:11:25] Saving model weights and runtime parameters to model.transformer.mysk.syl/model.npz
[2022-05-25 16:11:26] Saving Adam parameters
[2022-05-25 16:11:26] [training] Saving training checkpoint to model.transformer.mysk.syl/model.npz and model.transformer.mysk.syl/model.npz.optimizer.npz
[2022-05-25 16:11:28] [valid] Ep. 318 : Up. 55000 : cross-entropy : 35.6114 : stalled 10 times (last best: 25.2102)
[2022-05-25 16:11:29] [valid] Ep. 318 : Up. 55000 : perplexity : 14.0796 : stalled 10 times (last best: 6.50302)
[2022-05-25 16:11:36] [valid] Ep. 318 : Up. 55000 : bleu : 25.3642 : stalled 10 times (last best: 29.5988)
[2022-05-25 16:11:36] Training finished
[2022-05-25 16:11:36] Saving model weights and runtime parameters to model.transformer.mysk.syl/model.npz
[2022-05-25 16:11:37] Saving Adam parameters
[2022-05-25 16:11:37] [training] Saving training checkpoint to model.transformer.mysk.syl/model.npz and model.transformer.mysk.syl/model.npz.optimizer.npz

real    83m35.377s
user    107m51.687s
sys     1m28.097s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mysk.syl.sh
```

Testing and Evaluation:

```
[2022-05-25 16:31:32] Best translation 6842 : ပာ် ဖျါ တၢ် ထံၣ် အ ဝဲ ပိာ် မုၣ် အဲၣ် ယၤ ကီး ဧါ
[2022-05-25 16:31:32] Best translation 6843 : ပ တ ကး တံာ် ဝဲ ပဲ တြီ ဘၣ် ဧါ
[2022-05-25 16:31:32] Best translation 6844 : တ မ့ၢ် အ ဝဲ အ သ့ၣ် နီၣ် ဝဲ တၢ် လၢ ပ ဝဲ သ့ၣ် ဘၣ် တၢ် ကဲ ထီၣ် ဝဲ တ ဖၣ် န့ၣ် ဘၣ်
[2022-05-25 16:31:32] Best translation 6845 : ယ တၢ် ပီး တၢ် လီၤ တ ဖၣ် ဘၣ် စီၣ် လၢာ် လံၤ
[2022-05-25 16:31:32] Best translation 6846 : ဘၣ် မ နုၤ အ ဃိ တ မၤ တၢ် မၤ ဖဲ အံၤ ဘၣ် လဲၣ်
[2022-05-25 16:31:32] Best translation 6847 : မုၢ် လၢ် တ ဃး လၢ အိၣ် ဒၣ် က အိၣ် ဘှံး ဝဲ န့ၣ် လီၤ
[2022-05-25 16:31:32] Best translation 6848 : တ လါ
[2022-05-25 16:31:32] Best translation 6849 : တ မ့ၢ် အ ဝဲ က သံ ကွၢ် ဝဲ ယၤ ဘၣ်
[2022-05-25 16:31:32] Best translation 6850 : ခဲ မုၢ် ဆ့ၣ် ဟါ န မ့ၢ် ချူး န့ၣ် ယၤ ဒီး ယ မါ အဲၣ် ဒီး ကွဲ မုာ် ဝဲ လၢ ဟါ တၢ် အီၣ် အ ဂီၢ် န့ၣ် လီၤ
[2022-05-25 16:31:32] Best translation 6851 : ယ ပျံၤ တၢ် ခီၣ် လ့ၣ် ခိၣ် က နိး က စုာ် န့ၣ် လီၤ
[2022-05-25 16:31:32] Best translation 6852 : တၢ် တ မံၤ လၢ် လၢ် န့ၣ် ယ တ ပျံၤ တၢ် ဘၣ်
[2022-05-25 16:31:32] Best translation 6853 : တၢ် စံး ဆၢ လၢ န တူၢ် လိာ် တၢ် န့ၣ်
[2022-05-25 16:31:32] Best translation 6854 : တၢ် ဂဲၤ က လံၣ် မူး အိၣ် သး ဒ် လဲၣ်
[2022-05-25 16:31:32] Best translation 6855 : ပိာ် မုၣ် ဖိ သၣ် လၢ အဲၣ် တၢ် ယၤ န့ၣ် န ပာ် ဖျါ တၢ် ထံၣ် ဒ် လဲၣ်
[2022-05-25 16:31:32] Best translation 6856 : တၢ် ကူ တၢ် ကၤ တ ဖၣ် ဃံ လၤ ဝဲ ဒိၣ် မး လီၤ
[2022-05-25 16:31:32] Total time: 59.36037s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    11m0.500s
user    20m14.921s
sys     1m26.413s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysk.syl$ time ./test-eval.sh
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mysk.syl$ cat eval-result.txt
Evaluation with hyp.iter5000.sk, Transformer model:
BLEU = 31.19, 68.9/40.4/24.6/15.0 (BP=0.980, ratio=0.980, hyp_len=79351, ref_len=80936)
Evaluation with hyp.iter10000.sk, Transformer model:
BLEU = 30.87, 67.4/39.3/23.8/14.4 (BP=1.000, ratio=1.034, hyp_len=83679, ref_len=80936)
Evaluation with hyp.iter15000.sk, Transformer model:
BLEU = 29.75, 66.1/38.1/22.8/13.7 (BP=1.000, ratio=1.062, hyp_len=85951, ref_len=80936)
Evaluation with hyp.iter20000.sk, Transformer model:
BLEU = 28.79, 65.1/37.1/21.9/13.0 (BP=1.000, ratio=1.075, hyp_len=86992, ref_len=80936)
Evaluation with hyp.iter25000.sk, Transformer model:
BLEU = 28.42, 64.7/36.7/21.6/12.7 (BP=1.000, ratio=1.080, hyp_len=87449, ref_len=80936)
Evaluation with hyp.iter30000.sk, Transformer model:
BLEU = 28.09, 64.4/36.4/21.3/12.5 (BP=1.000, ratio=1.083, hyp_len=87638, ref_len=80936)
Evaluation with hyp.iter35000.sk, Transformer model:
BLEU = 27.99, 64.4/36.3/21.2/12.4 (BP=1.000, ratio=1.083, hyp_len=87687, ref_len=80936)
Evaluation with hyp.iter40000.sk, Transformer model:
BLEU = 27.87, 64.2/36.2/21.1/12.3 (BP=1.000, ratio=1.083, hyp_len=87642, ref_len=80936)
Evaluation with hyp.iter45000.sk, Transformer model:
BLEU = 27.84, 64.2/36.1/21.1/12.3 (BP=1.000, ratio=1.083, hyp_len=87684, ref_len=80936)
Evaluation with hyp.iter50000.sk, Transformer model:
BLEU = 27.72, 64.1/36.0/21.0/12.2 (BP=1.000, ratio=1.083, hyp_len=87684, ref_len=80936)
Evaluation with hyp.iter55000.sk, Transformer model:
BLEU = 27.78, 64.1/36.1/21.0/12.3 (BP=1.000, ratio=1.084, hyp_len=87720, ref_len=80936)
```

## my-dw, syllable, Transformer

training ...  

```
[2022-05-25 18:16:34] [data] Done reading 5,452 sentences
[2022-05-25 18:16:34] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 18:16:35] Seen 5,452 samples
[2022-05-25 18:16:35] Starting data epoch 2895 in logical epoch 2895
[2022-05-25 18:16:35] [data] Shuffling data
[2022-05-25 18:16:35] [data] Done reading 5,452 sentences
[2022-05-25 18:16:35] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 18:16:37] Ep. 2895 : Up. 55000 : Sen. 4,149 : Cost 1.07867610 * 1,602,562 @ 4,300 after 175,901,576 : Time 42.97s : 37295.08 words/s : gNorm 0.1228 : L.r. 1.6181e-04
[2022-05-25 18:16:37] Saving model weights and runtime parameters to model.transformer.mydw/model.iter55000.npz
[2022-05-25 18:16:37] Saving model weights and runtime parameters to model.transformer.mydw/model.npz
[2022-05-25 18:16:37] Saving Adam parameters
[2022-05-25 18:16:37] [training] Saving training checkpoint to model.transformer.mydw/model.npz and model.transformer.mydw/model.npz.optimizer.npz
[2022-05-25 18:16:39] [valid] Ep. 2895 : Up. 55000 : cross-entropy : 25.0437 : stalled 10 times (last best: 19.6475)
[2022-05-25 18:16:39] [valid] Ep. 2895 : Up. 55000 : perplexity : 9.13354 : stalled 10 times (last best: 5.67086)
[2022-05-25 18:16:39] [valid] Ep. 2895 : Up. 55000 : bleu : 45.126 : stalled 7 times (last best: 46.1209)
[2022-05-25 18:16:39] Training finished
[2022-05-25 18:16:39] Saving model weights and runtime parameters to model.transformer.mydw/model.npz
[2022-05-25 18:16:39] Saving Adam parameters
[2022-05-25 18:16:40] [training] Saving training checkpoint to model.transformer.mydw/model.npz and model.transformer.mydw/model.npz.optimizer.npz

real    79m19.981s
user    99m11.589s
sys     1m27.165s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mydw.sh
```

Testing and Evaluation:

```
[2022-05-25 18:32:04] Best translation 653 : ကျွန် တော့် ငယ် ဟှွန်း ဂဂို ဆစ် သွယ် ဟှှိှို့ မျှော် လင့် ဟှယ် ။
[2022-05-25 18:32:04] Best translation 654 : နန် ဒုက္ခ မ ရော့ ဟှ ။
[2022-05-25 18:32:04] Best translation 655 : ငါ ပြော ဟှှိှို့ စ နေ နေ့ မှာ ငါ တတိတို့ ကကိုး ။
[2022-05-25 18:32:04] Best translation 656 : ငါ ပြော ဟှှိှို့ စ နေ နေ့ မှာ ငါ တတိတို့ ကကိုး ။
[2022-05-25 18:32:04] Best translation 657 : ဟှယ် ဒဒူ့ လှော် အီ နူး ။
[2022-05-25 18:32:04] Best translation 658 : နန် အဲ ဝယ် ဟှား ဟှှို မူး ဟှှိှို့ မှု ဟှ လား ။
[2022-05-25 18:32:04] Best translation 659 : နန့် ကီး လေ ဟှ ဟှယ် လူ လေ နူး ။
[2022-05-25 18:32:04] Best translation 660 : ဟှယ် လူ လေ ဟှှို မေး ကေ့ နူး ။
[2022-05-25 18:32:04] Best translation 661 : အယ် ဝယ် ဟှား အဲ ဇာ ဟှှို လလို ရှင် ဟှှိှို့ မှု ဝ လား ။
[2022-05-25 18:32:04] Best translation 662 : ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
[2022-05-25 18:32:04] Best translation 663 : နန် ငါ့ ဟှှို ရှင်း ပြ ပါ လား ။
[2022-05-25 18:32:04] Best translation 664 : အဲ ဟှှို သွား ဟှှိှို့ နန် ဂဂို ငါ တတိုက် တွန်း ဟှ ။
[2022-05-25 18:32:04] Best translation 665 : ခန် ဗျား ခ ရီး ထွပ် ခခဲ့ ဟှ လား ။
[2022-05-25 18:32:04] Best translation 666 : သူး နနိနို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
[2022-05-25 18:32:04] Best translation 667 : အယ် ထဲ မှာ ဝေး ပြော ဇာ ဖုန်း ပြော ဇာ ဂဂို ရ ဟှယ် ။
[2022-05-25 18:32:04] Best translation 668 : အယ် ထဲ မှာ ဝေး ပြော ဇာ ဖုန်း ပြော ဇာ ဂဂို ရ ဟှယ် ။
[2022-05-25 18:32:04] Best translation 669 : အဲ ဝယ် ဟှား ဟှှို ယူ လလိုက် လား ။
[2022-05-25 18:32:04] Total time: 5.00403s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m0.582s
user    1m38.831s
sys     0m12.650s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mydw$ time ./test-eval.sh
```

Results for single source my-dw, syllable, Transformer:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mydw$ cat eval-result.txt
Evaluation with hyp.iter5000.dw, Transformer model:
BLEU = 46.91, 76.9/56.1/42.0/33.4 (BP=0.946, ratio=0.947, hyp_len=6412, ref_len=6769)
Evaluation with hyp.iter10000.dw, Transformer model:
BLEU = 47.00, 76.7/55.8/41.8/32.8 (BP=0.955, ratio=0.956, hyp_len=6468, ref_len=6769)
Evaluation with hyp.iter15000.dw, Transformer model:
BLEU = 46.76, 76.1/55.0/41.1/32.5 (BP=0.962, ratio=0.962, hyp_len=6514, ref_len=6769)
Evaluation with hyp.iter20000.dw, Transformer model:
BLEU = 46.93, 76.0/55.1/41.3/32.7 (BP=0.962, ratio=0.963, hyp_len=6516, ref_len=6769)
Evaluation with hyp.iter25000.dw, Transformer model:
BLEU = 47.38, 76.1/55.5/42.0/33.3 (BP=0.962, ratio=0.962, hyp_len=6514, ref_len=6769)
Evaluation with hyp.iter30000.dw, Transformer model:
BLEU = 47.02, 76.0/55.2/41.7/33.0 (BP=0.959, ratio=0.960, hyp_len=6498, ref_len=6769)
Evaluation with hyp.iter35000.dw, Transformer model:
BLEU = 47.35, 75.8/55.1/41.5/32.8 (BP=0.970, ratio=0.970, hyp_len=6566, ref_len=6769)
Evaluation with hyp.iter40000.dw, Transformer model:
BLEU = 47.15, 75.8/55.3/41.8/33.3 (BP=0.959, ratio=0.960, hyp_len=6500, ref_len=6769)
Evaluation with hyp.iter45000.dw, Transformer model:
BLEU = 47.10, 76.0/55.3/42.2/33.7 (BP=0.953, ratio=0.954, hyp_len=6458, ref_len=6769)
Evaluation with hyp.iter50000.dw, Transformer model:
BLEU = 46.53, 75.8/55.0/41.4/33.1 (BP=0.952, ratio=0.953, hyp_len=6449, ref_len=6769)
Evaluation with hyp.iter55000.dw, Transformer model:
BLEU = 46.46, 75.3/54.4/41.2/32.9 (BP=0.957, ratio=0.958, hyp_len=6483, ref_len=6769)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mydw$
```

## my,bk-dw, syllable, Multi-Source Transformer

training ...  

```
[2022-05-25 20:48:38] [data] Done reading 5,452 sentences
[2022-05-25 20:48:38] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 20:48:42] Seen 5,452 samples
[2022-05-25 20:48:42] Starting data epoch 1897 in logical epoch 1897
[2022-05-25 20:48:42] [data] Shuffling data
[2022-05-25 20:48:42] [data] Done reading 5,452 sentences
[2022-05-25 20:48:42] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 20:48:44] Ep. 1897 : Up. 55000 : Sen. 3,250 : Cost 1.07966948 * 1,050,236 @ 1,680 after 115,245,845 : Time 59.83s : 17554.15 words/s : gNorm 0.1554 : L.r. 1.6181e-04
[2022-05-25 20:48:44] Saving model weights and runtime parameters to model.transformer.mybk-dw/model.iter55000.npz
[2022-05-25 20:48:44] Saving model weights and runtime parameters to model.transformer.mybk-dw/model.npz
[2022-05-25 20:48:44] Saving Adam parameters
[2022-05-25 20:48:45] [training] Saving training checkpoint to model.transformer.mybk-dw/model.npz and model.transformer.mybk-dw/model.npz.optimizer.npz
[2022-05-25 20:48:47] [valid] Ep. 1897 : Up. 55000 : cross-entropy : 23.129 : stalled 10 times (last best: 18.5026)
[2022-05-25 20:48:47] [valid] Ep. 1897 : Up. 55000 : perplexity : 7.71249 : stalled 10 times (last best: 5.12543)
[2022-05-25 20:48:48] [valid] Ep. 1897 : Up. 55000 : bleu : 48.7572 : new best
[2022-05-25 20:48:48] Training finished
[2022-05-25 20:48:48] Saving model weights and runtime parameters to model.transformer.mybk-dw/model.npz
[2022-05-25 20:48:48] Saving Adam parameters
[2022-05-25 20:48:48] [training] Saving training checkpoint to model.transformer.mybk-dw/model.npz and model.transformer.mybk-dw/model.npz.optimizer.npz

real    110m28.647s
user    133m2.503s
sys     1m3.560s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mybk-dw.sh
```

testing evaluation ...  

```
[2022-05-26 05:14:45] Best translation 654 : နန် ဒုက္ခ ရော့ ဟှ ။
[2022-05-26 05:14:45] Best translation 655 : ငါ ပြော မယ် ။
[2022-05-26 05:14:45] Best translation 656 : ငါ ပြော မယ် ။
[2022-05-26 05:14:45] Best translation 657 : ဟှယ် ဒဒူ့ လှော် နူး ။
[2022-05-26 05:14:45] Best translation 658 : နန် အဲ ဝယ် ဟှား ဟှှို မူး လလိုက် ဟှှိှို့ မု ဟှ လား ။
[2022-05-26 05:14:45] Best translation 659 : နန့် ဂီး လေ ဟှ ဟှယ် လူ လေ နူး ။
[2022-05-26 05:14:45] Best translation 660 : ဟှယ် လူ လေ ဟှှို မေး ကေ့ နူး ။
[2022-05-26 05:14:45] Best translation 661 : အဲ ဝယ် ဟှား အဲ မူ ဇာ ဟှှို လလို ရှင် ဟှှိှို့ မှု ဝ ။
[2022-05-26 05:14:45] Best translation 662 : ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
[2022-05-26 05:14:45] Best translation 663 : နန် ငါ့ ဟှှို ရှင်း ပြ ပါ လား ။
[2022-05-26 05:14:45] Best translation 664 : အဲ ဟှှို သွား ဟှှိှို့ နန့် ဟှှို ငါ တတိုက် တွန်း ဟှ ။
[2022-05-26 05:14:45] Best translation 665 : ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
[2022-05-26 05:14:45] Best translation 666 : သူး နနိနို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
[2022-05-26 05:14:45] Best translation 667 : အယ် ထဲ မှာ ဝေး ပြော ဖောင်း ပြော ဇာ ရ တတိုင်း များ ဟှယ် ။
[2022-05-26 05:14:45] Best translation 668 : အယ် ထဲ မှာ ဝေး ပြော ဖောင်း ပြော ဇာ ရ တတိုင်း များ ဟှယ် ။
[2022-05-26 05:14:45] Best translation 669 : အဲ ဝယ် ဟှား ဟှှို ယူ လလိုက် လား ။
[2022-05-26 05:14:45] Total time: 6.17185s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m13.274s
user    2m4.116s
sys     0m13.128s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mybk-dw$ time ./test-eval.sh
```

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mybk-dw$ cat eval-result.txt
Evaluation with hyp.iter5000.dw, Transformer model:
BLEU = 48.87, 77.8/57.9/44.4/35.5 (BP=0.946, ratio=0.948, hyp_len=6414, ref_len=6769)
Evaluation with hyp.iter10000.dw, Transformer model:
BLEU = 49.57, 77.9/58.1/44.6/35.9 (BP=0.956, ratio=0.957, hyp_len=6476, ref_len=6769)
Evaluation with hyp.iter15000.dw, Transformer model:
BLEU = 49.39, 77.3/57.7/44.0/35.0 (BP=0.965, ratio=0.965, hyp_len=6535, ref_len=6769)
Evaluation with hyp.iter20000.dw, Transformer model:
BLEU = 49.79, 77.2/57.7/44.3/35.5 (BP=0.968, ratio=0.969, hyp_len=6557, ref_len=6769)
Evaluation with hyp.iter25000.dw, Transformer model:
BLEU = 49.71, 77.7/58.0/44.2/35.3 (BP=0.965, ratio=0.966, hyp_len=6539, ref_len=6769)
Evaluation with hyp.iter30000.dw, Transformer model:
BLEU = 50.14, 77.9/58.7/45.0/36.2 (BP=0.960, ratio=0.961, hyp_len=6502, ref_len=6769)
Evaluation with hyp.iter35000.dw, Transformer model:
BLEU = 50.43, 77.7/58.3/44.7/35.9 (BP=0.972, ratio=0.972, hyp_len=6580, ref_len=6769)
Evaluation with hyp.iter40000.dw, Transformer model:
BLEU = 50.35, 77.5/58.4/44.8/35.8 (BP=0.970, ratio=0.970, hyp_len=6569, ref_len=6769)
Evaluation with hyp.iter45000.dw, Transformer model:
BLEU = 49.32, 77.1/57.7/43.8/34.9 (BP=0.966, ratio=0.967, hyp_len=6544, ref_len=6769)
Evaluation with hyp.iter50000.dw, Transformer model:
BLEU = 49.39, 77.3/57.9/44.0/34.9 (BP=0.965, ratio=0.965, hyp_len=6534, ref_len=6769)
Evaluation with hyp.iter55000.dw, Transformer model:
BLEU = 49.33, 77.1/57.5/43.6/34.6 (BP=0.970, ratio=0.971, hyp_len=6570, ref_len=6769)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mybk-dw$
```

## dw-my, syllable unit, Transformer

Training ...  

```
[2022-05-25 22:11:49] [data] Done reading 5,452 sentences
[2022-05-25 22:11:49] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 22:11:50] Seen 5,452 samples
[2022-05-25 22:11:50] Starting data epoch 3236 in logical epoch 3236
[2022-05-25 22:11:50] [data] Shuffling data
[2022-05-25 22:11:50] [data] Done reading 5,452 sentences
[2022-05-25 22:11:50] [data] Done shuffling 5,452 sentences to temp files
[2022-05-25 22:11:51] Ep. 3236 : Up. 55000 : Sen. 1,668 : Cost 1.02863801 * 1,979,193 @ 3,560 after 217,828,391 : Time 43.80s : 45190.30 words/s : gNorm 0.0999 : L.r. 1.6181e-04
[2022-05-25 22:11:51] Saving model weights and runtime parameters to model.transformer.dwmy/model.iter55000.npz
[2022-05-25 22:11:51] Saving model weights and runtime parameters to model.transformer.dwmy/model.npz
[2022-05-25 22:11:51] Saving Adam parameters
[2022-05-25 22:11:51] [training] Saving training checkpoint to model.transformer.dwmy/model.npz and model.transformer.dwmy/model.npz.optimizer.npz
[2022-05-25 22:11:53] [valid] Ep. 3236 : Up. 55000 : cross-entropy : 20.6012 : stalled 10 times (last best: 16.5409)
[2022-05-25 22:11:53] [valid] Ep. 3236 : Up. 55000 : perplexity : 5.16839 : stalled 10 times (last best: 3.73912)
[2022-05-25 22:11:53] [valid] Ep. 3236 : Up. 55000 : bleu : 59.5539 : stalled 2 times (last best: 60.0722)
[2022-05-25 22:11:53] Training finished
[2022-05-25 22:11:53] Saving model weights and runtime parameters to model.transformer.dwmy/model.npz
[2022-05-25 22:11:54] Saving Adam parameters
[2022-05-25 22:11:54] [training] Saving training checkpoint to model.transformer.dwmy/model.npz and model.transformer.dwmy/model.npz.optimizer.npz

real    80m29.263s
user    102m41.691s
sys     1m22.923s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.dwmy.sh
```

Testing and evaluation ...  

```
[2022-05-26 05:18:37] Best translation 654 : မင်း ဒုက္ခ မ ကျ ဘူး ။
[2022-05-26 05:18:37] Best translation 655 : ကကိုယ် ပြော မယ် စ နေ နေ့ လည် မှာ ငါ တတိတို့ အ တွင်း က စား ရ မယ် ။
[2022-05-26 05:18:37] Best translation 656 : ကကိုယ် ပြော မယ် စ နေ နေ့ လယ် မှာ ငါ တတိတို့ ကကိုး တွင်း တွင်း ရေး ကြ မယ် ။
[2022-05-26 05:18:37] Best translation 657 : ဒါ ဘယ် သသူ့ လှောင် ပြောင် လဲ ။
[2022-05-26 05:18:37] Best translation 658 : မင်း သူ မ ကကို မုန်း ခခဲ့ ဘူး လား ။
[2022-05-26 05:18:37] Best translation 659 : မင်း ရရဲ့ မိ ဘ ကြီး တွေ က ဘယ် သူ တွေ လဲ ။
[2022-05-26 05:18:37] Best translation 660 : ဘယ် သူ တွေ ကကို မေး ကြ တာ လဲ ။
[2022-05-26 05:18:37] Best translation 661 : သူ မ အအဲ့ ဒါ ကကို လလို ချင် တယ် နော် မ ဟုတ် ဘူး လား ။
[2022-05-26 05:18:37] Best translation 662 : ဘယ် လောက် စိတ် လှုပ် ရှား သ လဲ ။
[2022-05-26 05:18:37] Best translation 663 : မင်း ငါ့ ကကို ရှင်း ပြ ပါ လား ။
[2022-05-26 05:18:37] Best translation 664 : အဲ ဒီ ကကို သွား ဖဖိဖို့ မင်း ကကို ငါ မ တတိုက် တွန်း ဘူး ။
[2022-05-26 05:18:37] Best translation 665 : ခင် ဗျား ခ ရီး မ ထွက် ဘူး လား ။
[2022-05-26 05:18:37] Best translation 666 : သူ တတိတို့ ဘယ် လောက် သတ္တိ ရှိ လဲ ။
[2022-05-26 05:18:37] Best translation 667 : အဲ ဒီ အ ဝေး ထဲ မှာ ဖုန်း အ ရမ်း များ လွန်း တယ် ။
[2022-05-26 05:18:37] Best translation 668 : အဲ ဒီ ထဲ မှာ ဖုန်း ပြော ရ တာ အ တော် များ လွန်း တယ် ။
[2022-05-26 05:18:37] Best translation 669 : သူ မ ကကို လက် ထပ် ခခဲ့ တာ လား ။
[2022-05-26 05:18:37] Total time: 5.69135s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m6.062s
user    1m50.035s
sys     0m12.728s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwmy$ time ./test-eval.sh
```

Results:  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwmy$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 60.26, 86.3/70.1/57.5/49.1 (BP=0.937, ratio=0.939, hyp_len=7123, ref_len=7585)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 60.08, 86.1/69.9/57.3/48.8 (BP=0.938, ratio=0.939, hyp_len=7126, ref_len=7585)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 60.19, 85.9/69.6/57.0/49.0 (BP=0.942, ratio=0.943, hyp_len=7156, ref_len=7585)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 60.21, 85.6/69.5/57.0/48.8 (BP=0.944, ratio=0.945, hyp_len=7170, ref_len=7585)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 60.48, 85.8/69.7/57.3/49.1 (BP=0.944, ratio=0.946, hyp_len=7172, ref_len=7585)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 60.03, 85.8/69.6/57.1/48.8 (BP=0.940, ratio=0.941, hyp_len=7141, ref_len=7585)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 60.82, 85.8/70.1/57.9/49.5 (BP=0.944, ratio=0.945, hyp_len=7170, ref_len=7585)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 60.43, 85.5/69.6/57.3/49.1 (BP=0.945, ratio=0.946, hyp_len=7179, ref_len=7585)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 60.93, 85.8/69.9/57.7/49.7 (BP=0.946, ratio=0.947, hyp_len=7184, ref_len=7585)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 60.87, 85.6/69.7/57.4/49.3 (BP=0.950, ratio=0.951, hyp_len=7212, ref_len=7585)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 60.74, 85.4/69.6/57.4/49.3 (BP=0.948, ratio=0.950, hyp_len=7202, ref_len=7585)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwmy$
```

## dw,bk to my, Transformer

Training ...  

```
[2022-05-26 07:14:50] [data] Done reading 5,452 sentences
[2022-05-26 07:14:50] [data] Done shuffling 5,452 sentences to temp files
[2022-05-26 07:14:54] Seen 5,452 samples
[2022-05-26 07:14:54] Starting data epoch 2038 in logical epoch 2038
[2022-05-26 07:14:54] [data] Shuffling data
[2022-05-26 07:14:54] [data] Done reading 5,452 sentences
[2022-05-26 07:14:54] [data] Done shuffling 5,452 sentences to temp files
[2022-05-26 07:14:54] Ep. 2038 : Up. 55000 : Sen. 428 : Cost 1.02814496 * 1,247,008 @ 3,332 after 137,152,505 : Time 60.65s : 20560.69 words/s : gNorm 0.1280 : L.r. 1.6181e-04
[2022-05-26 07:14:54] Saving model weights and runtime parameters to model.transformer.dwbk-my/model.iter55000.npz
[2022-05-26 07:14:54] Saving model weights and runtime parameters to model.transformer.dwbk-my/model.npz
[2022-05-26 07:14:55] Saving Adam parameters
[2022-05-26 07:14:55] [training] Saving training checkpoint to model.transformer.dwbk-my/model.npz and model.transformer.dwbk-my/model.npz.optimizer.npz
[2022-05-26 07:14:57] [valid] Ep. 2038 : Up. 55000 : cross-entropy : 15.4036 : stalled 10 times (last best: 12.6963)
[2022-05-26 07:14:57] [valid] Ep. 2038 : Up. 55000 : perplexity : 3.41494 : stalled 10 times (last best: 2.75194)
[2022-05-26 07:14:58] [valid] Ep. 2038 : Up. 55000 : bleu : 67.4342 : stalled 6 times (last best: 68.4184)
[2022-05-26 07:14:58] Training finished
[2022-05-26 07:14:58] Saving model weights and runtime parameters to model.transformer.dwbk-my/model.npz
[2022-05-26 07:14:58] Saving Adam parameters
[2022-05-26 07:14:58] [training] Saving training checkpoint to model.transformer.dwbk-my/model.npz and model.transformer.dwbk-my/model.npz.optimizer.npz

real    111m56.333s
user    135m12.179s
sys     1m6.907s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.dwbk-my.sh
```

Testing and Evaluation ...  

```
[2022-05-26 08:23:15] Best translation 653 : ကျွန် တော် ရရဲ့ ချစ် ကကို ဆက် သွယ် ဖဖိဖို့ မျှော် လ င့် ပါ တယ် ။
[2022-05-26 08:23:15] Best translation 654 : မင်း ဒုက္ခ မ ရောက် ပါ ဘူး ။
[2022-05-26 08:23:15] Best translation 655 : ကကိုယ် ပြော ပြ လိမ့် နေ နေ့ လည် မှာ ငါ တတိတို့ က စား မယ် ။
[2022-05-26 08:23:15] Best translation 656 : ကကိုယ် ပြော ပြ လိမ့် နေ နေ့ လည် မှာ ငါ တတိတို့ က စား မယ် ။
[2022-05-26 08:23:15] Best translation 657 : ဒါ ဘယ် သသူ့ အိမ် လဲ ။
[2022-05-26 08:23:15] Best translation 658 : မင်း သသူ့ ကကို မုန်း ခခဲ့ တာ မ ဟုတ် ဘူး လား ။
[2022-05-26 08:23:15] Best translation 659 : မင်း ရရဲ့ ကြီး တွေ က ဘယ် သူ တွေ လဲ ။
[2022-05-26 08:23:15] Best translation 660 : ဘယ် သူ တွေ ကကို မေး ကြ တာ လဲ ။
[2022-05-26 08:23:15] Best translation 661 : သူ မ အအဲ့ ဒါ ကကို လလို ချင် တယ် မ ဟုတ် ဘူး လား ။
[2022-05-26 08:23:15] Best translation 662 : ဘယ် လောက် စိတ် လှုပ် ရှား သ လဲ ။
[2022-05-26 08:23:15] Best translation 663 : မင်း ငါ့ ကကို ရှင်း ပြ နနိုင် မ လား ။
[2022-05-26 08:23:15] Best translation 664 : အဲ ဒီ ကကို သွား ဖဖိဖို့ ငါ မ တတိုက် တွန်း ဘူး ။
[2022-05-26 08:23:15] Best translation 665 : ခင် ဗျား ခ ရီး မ ထွက် ခခဲ့ ဘူး လား ။
[2022-05-26 08:23:15] Best translation 666 : သူ တတိတို့ ဘယ် လောက် သတ္တိ ရှိ လဲ ။
[2022-05-26 08:23:15] Best translation 667 : ဒီ ထဲ မှာ အ ဝေး ကကို ဖုန်း ပြော တာ သိပ် များ လွန်း တယ် ။
[2022-05-26 08:23:15] Best translation 668 : ဒီ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော ရ တာ ပဲ ။
[2022-05-26 08:23:15] Best translation 669 : သူ မ ကကို လက် ထပ် လလိုက် တာ လား ။
[2022-05-26 08:23:15] Total time: 7.19908s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m20.865s
user    2m18.942s
sys     0m13.395s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwbk-my$ time ./test-eval.sh
```

Results are ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwbk-my$ cat eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 66.07, 89.9/75.8/64.7/57.1 (BP=0.932, ratio=0.934, hyp_len=7088, ref_len=7585)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 66.59, 90.3/76.6/65.4/57.6 (BP=0.932, ratio=0.934, hyp_len=7088, ref_len=7585)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 66.86, 90.3/76.5/65.4/57.5 (BP=0.936, ratio=0.938, hyp_len=7116, ref_len=7585)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 66.64, 89.6/76.1/64.8/56.8 (BP=0.942, ratio=0.943, hyp_len=7155, ref_len=7585)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 66.59, 89.5/76.0/64.6/56.7 (BP=0.943, ratio=0.944, hyp_len=7162, ref_len=7585)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 67.23, 89.5/76.2/65.1/57.4 (BP=0.946, ratio=0.948, hyp_len=7188, ref_len=7585)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 67.05, 89.6/76.1/65.1/57.2 (BP=0.945, ratio=0.946, hyp_len=7177, ref_len=7585)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 67.27, 89.4/76.1/65.1/57.3 (BP=0.948, ratio=0.949, hyp_len=7201, ref_len=7585)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 66.86, 89.1/75.7/64.7/56.8 (BP=0.947, ratio=0.949, hyp_len=7196, ref_len=7585)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 67.09, 89.6/76.4/65.7/58.1 (BP=0.938, ratio=0.940, hyp_len=7131, ref_len=7585)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 67.29, 89.5/76.5/65.5/57.8 (BP=0.943, ratio=0.945, hyp_len=7166, ref_len=7585)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.dwbk-my$
```

## sk-my, Word, Transformer

training ...  

```
[2022-05-27 23:13:20] Saving model weights and runtime parameters to model.transformer.skmy/model.npz
[2022-05-27 23:13:22] Saving Adam parameters
[2022-05-27 23:13:22] [training] Saving training checkpoint to model.transformer.skmy/model.npz and model.transformer.skmy/model.npz.optimizer.npz
[2022-05-27 23:13:29] [valid] Ep. 432 : Up. 60000 : cross-entropy : 23.3281 : stalled 10 times (last best: 19.5287)
[2022-05-27 23:13:29] [valid] Ep. 432 : Up. 60000 : perplexity : 31.1036 : stalled 10 times (last best: 17.7695)
[2022-05-27 23:13:35] [valid] Ep. 432 : Up. 60000 : bleu : 11.7631 : stalled 9 times (last best: 13.6648)
[2022-05-27 23:13:35] Training finished
[2022-05-27 23:13:36] Saving model weights and runtime parameters to model.transformer.skmy/model.npz
[2022-05-27 23:13:37] Saving Adam parameters
[2022-05-27 23:13:38] [training] Saving training checkpoint to model.transformer.skmy/model.npz and model.transformer.skmy/model.npz.optimizer.npz

real    250m32.321s
user    277m42.417s
sys     2m12.397s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.skmy.sh
```

testing and evaluation ...  

```
[2022-05-28 13:18:38] Best translation 6851 : ငါ ကြောက်ဒူး တုန် နေတယ်
[2022-05-28 13:18:38] Best translation 6852 : ကျွန်တော် စောစော မ ကြောက် နနိုင်ဘူး
[2022-05-28 13:18:38] Best translation 6853 : မင်း လက်ခံ တတဲ့ အဖြေ
[2022-05-28 13:18:38] Best translation 6854 : ခင်ဗျား ဘယ် အချိန် ကျ မလဲ
[2022-05-28 13:18:38] Best translation 6855 : ကျွန်မကကို ချစ် တတဲ့ ကောင်မလေးက ငါ့ကကို ဘယလို သဘောရ သလဲ
[2022-05-28 13:18:38] Best translation 6856 : ခင်ဗျား တတိတို့ မြန်မြန် တက် လိမ့်မယ်
[2022-05-28 13:18:38] Total time: 48.21635s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    9m44.151s
user    17m26.839s
sys     1m36.002s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.skmy$ time ./test-eval.sh
```

results ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.skmy$ cat ./eval-result.txt
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 14.52, 32.4/16.6/11.0/7.6 (BP=1.000, ratio=1.006, hyp_len=39333, ref_len=39092)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 15.88, 32.9/17.8/12.2/8.9 (BP=1.000, ratio=1.030, hyp_len=40275, ref_len=39092)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 16.29, 33.3/18.2/12.5/9.3 (BP=1.000, ratio=1.019, hyp_len=39818, ref_len=39092)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 16.05, 32.9/18.0/12.4/9.1 (BP=1.000, ratio=1.027, hyp_len=40150, ref_len=39092)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 16.12, 32.8/18.0/12.5/9.2 (BP=1.000, ratio=1.028, hyp_len=40180, ref_len=39092)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 15.58, 32.3/17.4/12.0/8.7 (BP=1.000, ratio=1.027, hyp_len=40156, ref_len=39092)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 15.47, 32.1/17.3/11.9/8.7 (BP=1.000, ratio=1.037, hyp_len=40544, ref_len=39092)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 15.24, 32.0/17.1/11.7/8.4 (BP=1.000, ratio=1.041, hyp_len=40687, ref_len=39092)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 14.92, 31.8/16.9/11.4/8.1 (BP=1.000, ratio=1.047, hyp_len=40912, ref_len=39092)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 14.73, 31.4/16.6/11.2/8.0 (BP=1.000, ratio=1.055, hyp_len=41259, ref_len=39092)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 14.57, 31.2/16.5/11.1/7.9 (BP=1.000, ratio=1.063, hyp_len=41573, ref_len=39092)
Evaluation with hyp.iter60000.my, Transformer model:
BLEU = 14.43, 31.2/16.4/11.0/7.7 (BP=1.000, ratio=1.062, hyp_len=41523, ref_len=39092)
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.skmy$
```


## sk-my, syllable, Transformer

training ...  

```
[2022-05-26 10:40:01] Saving model weights and runtime parameters to model.transformer.skmy.syl/model.npz
[2022-05-26 10:40:01] Saving Adam parameters
[2022-05-26 10:40:01] [training] Saving training checkpoint to model.transformer.skmy.syl/model.npz and model.transformer.skmy.syl/model.npz.optimizer.npz
[2022-05-26 10:40:04] [valid] Ep. 427 : Up. 80000 : cross-entropy : 9.2118 : stalled 10 times (last best: 8.61618)
[2022-05-26 10:40:04] [valid] Ep. 427 : Up. 80000 : perplexity : 2.05441 : stalled 10 times (last best: 1.96096)
[2022-05-26 10:40:10] [valid] Ep. 427 : Up. 80000 : bleu : 63.4707 : new best
[2022-05-26 10:40:10] Training finished
[2022-05-26 10:40:10] Saving model weights and runtime parameters to model.transformer.skmy.syl/model.npz
[2022-05-26 10:40:11] Saving Adam parameters
[2022-05-26 10:40:11] [training] Saving training checkpoint to model.transformer.skmy.syl/model.npz and model.transformer.skmy.syl/model.npz.optimizer.npz
```

results:
```
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 43.37, 77.4/57.9/45.6/36.9 (BP=0.828, ratio=0.841, hyp_len=66186, ref_len=78676)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 53.92, 81.2/66.0/56.0/48.6 (BP=0.873, ratio=0.880, hyp_len=69244, ref_len=78676)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 58.17, 82.7/69.2/60.1/53.4 (BP=0.889, ratio=0.894, hyp_len=70361, ref_len=78676)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 60.50, 83.5/70.8/62.3/56.0 (BP=0.898, ratio=0.903, hyp_len=71021, ref_len=78676)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 62.00, 84.1/71.9/63.7/57.6 (BP=0.903, ratio=0.908, hyp_len=71405, ref_len=78676)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 62.94, 84.3/72.4/64.3/58.4 (BP=0.909, ratio=0.913, hyp_len=71854, ref_len=78676)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 63.32, 84.5/72.7/64.6/58.8 (BP=0.911, ratio=0.915, hyp_len=71957, ref_len=78676)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 63.69, 84.6/72.9/65.0/59.2 (BP=0.913, ratio=0.916, hyp_len=72080, ref_len=78676)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 63.83, 84.7/73.0/65.1/59.4 (BP=0.913, ratio=0.916, hyp_len=72085, ref_len=78676)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 64.26, 84.7/73.2/65.4/59.7 (BP=0.916, ratio=0.920, hyp_len=72354, ref_len=78676)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 63.99, 84.6/73.0/65.2/59.4 (BP=0.915, ratio=0.918, hyp_len=72258, ref_len=78676)
Evaluation with hyp.iter60000.my, Transformer model:
BLEU = 64.13, 84.7/73.1/65.3/59.7 (BP=0.915, ratio=0.918, hyp_len=72256, ref_len=78676)
Evaluation with hyp.iter65000.my, Transformer model:
BLEU = 64.22, 84.7/73.2/65.4/59.6 (BP=0.916, ratio=0.919, hyp_len=72324, ref_len=78676)
Evaluation with hyp.iter70000.my, Transformer model:
BLEU = 64.23, 84.7/73.2/65.3/59.6 (BP=0.916, ratio=0.920, hyp_len=72366, ref_len=78676)
Evaluation with hyp.iter75000.my, Transformer model:
BLEU = 64.23, 84.6/73.1/65.4/59.7 (BP=0.916, ratio=0.919, hyp_len=72340, ref_len=78676)
Evaluation with hyp.iter80000.my, Transformer model:
BLEU = 64.10, 84.5/73.0/65.3/59.6 (BP=0.916, ratio=0.919, hyp_len=72299, ref_len=78676)
```

## my-bk, syllable unit, Transformer

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for training
## Last updated: 23 May 2022


model_folder="model.transformer.mybk";
mkdir ${model_folder};
data_path="/home/ye/exp/my-nmt/data/4nmt/my-bk/";
src="my"; tgt="bk";

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
[2022-05-28 15:57:52] Seen 5,452 samples
[2022-05-28 15:57:52] Starting data epoch 2746 in logical epoch 2746
[2022-05-28 15:57:52] [data] Shuffling data
[2022-05-28 15:57:52] [data] Done reading 5,452 sentences
[2022-05-28 15:57:52] [data] Done shuffling 5,452 sentences to temp files
[2022-05-28 15:57:53] Seen 5,452 samples
[2022-05-28 15:57:53] Starting data epoch 2747 in logical epoch 2747
[2022-05-28 15:57:53] [data] Shuffling data
[2022-05-28 15:57:53] [data] Done reading 5,452 sentences
[2022-05-28 15:57:53] [data] Done shuffling 5,452 sentences to temp files
[2022-05-28 15:57:55] Seen 5,452 samples
[2022-05-28 15:57:55] Starting data epoch 2748 in logical epoch 2748
[2022-05-28 15:57:55] [data] Shuffling data
[2022-05-28 15:57:55] [data] Done reading 5,452 sentences
[2022-05-28 15:57:55] [data] Done shuffling 5,452 sentences to temp files
[2022-05-28 15:57:57] Seen 5,452 samples
[2022-05-28 15:57:57] Starting data epoch 2749 in logical epoch 2749
[2022-05-28 15:57:57] [data] Shuffling data
[2022-05-28 15:57:57] [data] Done reading 5,452 sentences
[2022-05-28 15:57:57] [data] Done shuffling 5,452 sentences to temp files
[2022-05-28 15:57:58] Seen 5,452 samples
[2022-05-28 15:57:58] Starting data epoch 2750 in logical epoch 2750
[2022-05-28 15:57:58] [data] Shuffling data
[2022-05-28 15:57:58] [data] Done reading 5,452 sentences
[2022-05-28 15:57:59] [data] Done shuffling 5,452 sentences to temp files
[2022-05-28 15:58:00] Ep. 2750 : Up. 55000 : Sen. 5,452 : Cost 1.04303694 * 1,537,400 @ 3,500 after 169,114,000 : Time 41.96s : 36637.84 words/s : gNorm 0.1151 : L.r. 1.6181e-04
[2022-05-28 15:58:00] Saving model weights and runtime parameters to model.transformer.mybk/model.iter55000.npz
[2022-05-28 15:58:00] Saving model weights and runtime parameters to model.transformer.mybk/model.npz
[2022-05-28 15:58:01] Saving Adam parameters
[2022-05-28 15:58:01] [training] Saving training checkpoint to model.transformer.mybk/model.npz and model.transformer.mybk/model.npz.optimizer.npz
[2022-05-28 15:58:03] [valid] Ep. 2750 : Up. 55000 : cross-entropy : 27.1532 : stalled 10 times (last best: 21.7688)
[2022-05-28 15:58:03] [valid] Ep. 2750 : Up. 55000 : perplexity : 10.7665 : stalled 10 times (last best: 6.72077)
[2022-05-28 15:58:03] [valid] Ep. 2750 : Up. 55000 : bleu : 49.4682 : stalled 8 times (last best: 50.0873)
[2022-05-28 15:58:03] Training finished
[2022-05-28 15:58:03] Saving model weights and runtime parameters to model.transformer.mybk/model.npz
[2022-05-28 15:58:04] Saving Adam parameters
[2022-05-28 15:58:04] [training] Saving training checkpoint to model.transformer.mybk/model.npz and model.transformer.mybk/model.npz.optimizer.npz

real    77m38.136s
user    96m55.906s
sys     1m18.916s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt$ ./transformer.mybk.sh
```

testing and evaluation ...  
```
[2022-05-28 16:51:08] Best translation 638 : ဖယ် သူ တွေ အိပ် နေ ကြ ရိ လဲ ။
[2022-05-28 16:51:08] Best translation 639 : မင်း စ ကား ပြော နေ စာ ။
[2022-05-28 16:51:08] Best translation 640 : သူ ဒယ် စာ ဝဝို ဆဆုံး ဖြတ် ခခဲ့ ဟယ် ။
[2022-05-28 16:51:08] Best translation 641 : ငါ့ အ နား နေ ရ ဇာ ပျော် လား ။
[2022-05-28 16:51:08] Best translation 642 : ငါ့ ဝဝို ယယုံ တတဲ့ သူ ဒေ ဂဂို ဘယ် ခါ မှ သစ္စာ မ ဖောက် ရ ။
[2022-05-28 16:51:08] Best translation 643 : မင်း ဘိန် ရိ ဟင်း ချက် မ ချက် ။
[2022-05-28 16:51:08] Best translation 644 : နင် ဒယ် စာ ဝဝို စဉ်း စား ကြည့် ရရိုက် ။
[2022-05-28 16:51:08] Best translation 645 : တံ ခါး ဖွင့် ရင် စိတ် ဆဆိုး ဝဝိဝို့ လား ။
[2022-05-28 16:51:08] Best translation 646 : ဟုတ် ဝယ် ၊ ရ ရရ် ။
[2022-05-28 16:51:08] Best translation 647 : နင် ဘာ ဇာ လုပ် ထား ရယ် ။
[2022-05-28 16:51:08] Best translation 648 : ကျွန် တော် လလိလို့ ဒယ့် ဇာ ကကို ကာ ကွယ် ဝဝိဝို့ လား ။
[2022-05-28 16:51:08] Best translation 649 : နင် ဘာ ဇာ တွေ လုပ် နေ ရယ် ။
[2022-05-28 16:51:08] Best translation 650 : နင် ဘာ ဇာ တွေ လုပ် နေ ရယ် ။
[2022-05-28 16:51:08] Best translation 651 : ခင် ဗျား လလို အပ် ရင် ရေ လလို အပ် နနိုင် ရရ် ။
[2022-05-28 16:51:08] Best translation 652 : ကျွန် တော် ဝဝိဝို့ အအဲ့ ဒါ ဝဝို အ တည် မ ပြု ခခဲ့ ရ ။
[2022-05-28 16:51:08] Best translation 653 : ငါ ငယ် ချစ် ဝဝိဝို့ မျှော် လင့် သွယ် ဝဝိဝို့ မျှော် လင့် တယ် ။
[2022-05-28 16:51:08] Best translation 654 : နင် ဒုက္ခ မ ရောက် ဝ ။
[2022-05-28 16:51:08] Best translation 655 : ငါ ပြော ဟာ ည နေ နေ့ လည် မှာ ကကိုယ် တတိတို့ တွင်း က စား ကြ မယ် ။
[2022-05-28 16:51:08] Best translation 656 : ငါ ပြော ဟာ ည နေ နေ့ လည် မှာ ကကိုယ် တတိတို့ တွင်း က စား ကြ မယ် ။
[2022-05-28 16:51:08] Best translation 657 : အယ့် ဒါ ဘယ် သသူ့ လှောင် အိမ် ရိ ။
[2022-05-28 16:51:08] Best translation 658 : နင် သသူ့ ကကို မုန်း လလိုက် မယ် မ ဟုတ် ဝ လား ။
[2022-05-28 16:51:08] Best translation 659 : နင့် ကြီး တတိတို့ က ဖယ် သူ တွေ ။
[2022-05-28 16:51:08] Best translation 660 : ဖယ် သူ လေ ဝဝို မေး ကြ ရိ လဲ ။
[2022-05-28 16:51:08] Best translation 661 : သူ ဒယ့် ဇာ ကကို လလို ချင် ဟုတ် ဝ လား ။
[2022-05-28 16:51:08] Best translation 662 : ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
[2022-05-28 16:51:08] Best translation 663 : မင်း ငါ့ ကကို ရှင်း ပြ နနိုင် မ လား ။
[2022-05-28 16:51:08] Best translation 664 : အဲ ဒီ ကကို သော ဖဖိဖို့ မင်း ကကို ငါ မ တတိုက် တွန်း ရ ။
[2022-05-28 16:51:08] Best translation 665 : နင် ခ ရီး မ ထွက် ခခဲ့ ရ လား ။
[2022-05-28 16:51:08] Best translation 666 : သူ တတိတို့ ဘ ဇာ လောက်် သတ္တိ ရှိ လဲ ။
[2022-05-28 16:51:08] Best translation 667 : ဒယ် အ ထဲ မှာ အ ဝေး ဖုန်း ပြော ရယ် ။
[2022-05-28 16:51:08] Best translation 668 : ဒယ် အ ထဲ မှာ အ ဝေး ဖုန်း ပြော ရယ် ။
[2022-05-28 16:51:08] Best translation 669 : ဒယ် ကောင် မ ငယ် ကကို လက် ထပ် လလိုက် ရယ် လား ။
[2022-05-28 16:51:08] Total time: 5.12985s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m1.478s
user    1m41.286s
sys     0m12.201s
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mybk$
```

results ...  

```
(marian) ye@ye-System-Product-Name:~/exp/my-nmt/model.transformer.mybk$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 47.81, 75.3/54.1/41.5/33.9 (BP=0.977, ratio=0.978, hyp_len=6666, ref_len=6818)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 48.56, 75.8/54.9/42.4/34.6 (BP=0.976, ratio=0.977, hyp_len=6658, ref_len=6818)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 48.84, 75.7/55.0/42.7/34.9 (BP=0.978, ratio=0.979, hyp_len=6672, ref_len=6818)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 48.99, 75.4/54.7/42.4/34.5 (BP=0.988, ratio=0.988, hyp_len=6737, ref_len=6818)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 49.32, 75.4/55.1/43.0/35.2 (BP=0.985, ratio=0.985, hyp_len=6716, ref_len=6818)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 49.56, 75.6/55.5/43.1/35.1 (BP=0.987, ratio=0.987, hyp_len=6730, ref_len=6818)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 49.59, 75.5/55.1/42.9/35.1 (BP=0.991, ratio=0.991, hyp_len=6758, ref_len=6818)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 49.57, 75.8/55.5/43.1/35.4 (BP=0.985, ratio=0.985, hyp_len=6717, ref_len=6818)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 49.80, 75.8/56.0/43.7/35.8 (BP=0.981, ratio=0.981, hyp_len=6690, ref_len=6818)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 49.40, 75.5/55.1/42.9/35.0 (BP=0.988, ratio=0.988, hyp_len=6739, ref_len=6818)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 49.50, 75.6/55.2/43.0/35.4 (BP=0.986, ratio=0.986, hyp_len=6724, ref_len=6818)
```

## bk-my, syllable unit, Transformer

bash script  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for training
## Last updated: 28 May 2022


model_folder="model.transformer.bkmy";
mkdir ${model_folder};
data_path="/home/ye/exp/my-nmt/data/4nmt/bk-my/";
src="bk"; tgt="my";

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

```bash

```

testing and evaluation ...  

```

```

results ...  

```

```

