# XNMT ASEAN my-th Experiment Log

Plan to add Myanmar-Thai language pair of ASEAN-MT Domain for SwitchOver Experiment ...  

## Data Preparation

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ mkdir asean-myth
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ cd asean-myth/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ mkdir data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cd data/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ cp /home/ye/data/zzh/plan-to-use-for-switchout/5_TH-MY_myPOS-V3_Reports/DATA/data-word/*.{th,my} .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ ls
test.my  test.th  train.my  train.th  valid.my  valid.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc *
   1000    9579  119884 test.my
   1000    7169   99326 test.th
  20000  187574 2360049 train.my
  20000  139767 1951027 train.th
   1031    9573  119279 valid.my
   1031    6809   98543 valid.th
  44062  360471 4748108 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

## Checking on Data

Sometimes, it might contain blank lines and we need to check it before we train NMT model ...  

1st copying the perl script ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline/data$ cp print-blank-lines.pl ../../asean-myth/data/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline/data$ cd ../../asean-myth/data/
```

check blank line exist or not with that perl script ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./train.th
4616
6863
8076
10007
13347
19555
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./valid.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./test.th
```

As above, we found some blank lines when we checked with train.th.  
And also check for the Myanmar data and it looks OK as follows:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./train.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./valid.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./test.my
```

Make parallel training data for deleting blank lines of Thai side together with the parallel Myanmar sentences ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ paste train.th train.my > train.thmy
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ head ./train.thmy
ใช่ , ฉัน ชอบ เล่น หมากรุก ไทย  ဟုတ်ကဲ့ ၊ ကျွန်တော် ထိုင်း စစ်တုရင် ကစား ရ တာ ကြိုက် တယ် ။
คุณ มี อะไร แนะนำ สำหรับ เด็ก ไหม ?     ကလေးများ အတွက် တစ် ခု ခု အကြံပြု ပေး နိုင် မလား ။
ฉัน สามารถ ไป ที่ นั่น ได้ อย่างไร ?    အဲဒီ ကို ဘယ်လို ရောက် နိုင် မလဲ ။
ฉัน ปวด เมื่อย ทั่ว ทั้งหมด     တစ်ကိုယ်လုံး ကိုက်ခဲ နေ လို့ ။
ขอบคุณ สำหรับ ทั้งหมด ที่ คุณ ทำ เพื่อ พวก เรา  ကျွန်တော် တို့ အတွက် လုပ် ပေး ခဲ့ တာ တွေ ကျေးဇူးတင် ပါ တယ် ။
ฉันหวังว่าคุณเพลิดเพลินอาหารเย็นของคุณ  ခင်ဗျား ရဲ့ ညစာ ကို နှစ်သက် မယ် လို့ မျှော်လင့် ပါ တယ် ။
เรา สามารถ เดิน ไป ยัง อ่าว ได้ ไหม ?   ဆိပ်ကမ်း ကို လမ်းလျှောက် သွား နိုင် လား ။
ฉันเสียใจ, ท่าน. ปลานึ่งของคุณไม่พร้อม. ถ้าคุณไม่ต้องการมันจริงๆ, พวกเราสามารถยกเลิกมัน စိတ်မကောင်း ပါ ဘူး ဆရာ ။ ခင်ဗျား ရဲ့ ငါးပေါင်း က အဆင်သင့် မ ဖြစ် သေး ပါ ဘူး ။ ခင်ဗျား မ မှာ ချင် တော့ ဘူး ဆို ရင် တော့ ဖျက် လိုက် လို့ ရ ပါ တယ် ။
ฮอทดอกหนึ่งคู่  hot dog နှစ် ခု လောက် ။
กรุณาดื่มซุปโดยตรงจากชาม        စွပ်ပြုတ် ကို ပန်းကန်လုံး ထဲ က နေ တိုက်ရိုက် သောက် ပါ ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

keep current data that contained blank lines ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ mkdir blank-line
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ mv train.my ./blank-line/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ mv train.th ./blank-line/
```

delete blank lines according to their line numbers ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc ./train.thmy
  20000  327341 4311076 ./train.thmy
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ sed -i '4616d;6863d;8076d;10007d;13347d;19555d;' ./train.thmy
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc ./train.thmy
  19994  327311 4310659 ./train.thmy
```

Split th and my as two files. After deletion blank lines ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ cut -f1 ./train.thmy > train.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ cut -f2 ./train.thmy > train.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc train.{th,my}
  19994  139767 1951021 train.th
  19994  187544 2359638 train.my
  39988  327311 4310659 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

wc of train, valid, test is as follows:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc {train,valid,test}.{th,my}
  19994  139767 1951021 train.th
  19994  187544 2359638 train.my
   1031    6809   98543 valid.th
   1031    9573  119279 valid.my
   1000    7169   99326 test.th
   1000    9579  119884 test.my
  44050  360441 4747691 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

## Preparing config files  

preparing config files ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cp ../asean-mt-baseline/config.baseline.en-th-word.yaml ./config.baseline.my-th-word.yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cp ../asean-mt-baseline/config.baseline.th-en-word.yaml ./config.baseline.th-my-word.yaml
```

updated config file for my-th, ASEAN-MT domain, dropout=0.3, baseline  

```yaml
# standard settings
asean.baseline.my-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.my'
      - '{EXP_DIR}/data/train.th'
      out_files:
      - '{EXP_DIR}/vocab.my'
      - '{EXP_DIR}/vocab.th'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.th'}
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 30  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/data/train.my'
    trg_file: '{EXP_DIR}/data/train.th'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.my'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.th'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.th'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.th'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.my'
      ref_file: &test_trg '{EXP_DIR}/data/test.th'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.th'
```

for the direction of th-my:  

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cat ./config.baseline.th-my-word.yaml
# standard settings
asean.baseline.th-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.th'
      - '{EXP_DIR}/data/train.my'
      out_files:
      - '{EXP_DIR}/vocab.th'
      - '{EXP_DIR}/vocab.my'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.th'}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 30  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/data/train.th'
    trg_file: '{EXP_DIR}/data/train.my'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.th'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.my'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.my'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.my'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.th'
      ref_file: &test_trg '{EXP_DIR}/data/test.my'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.my'
```

change valid to dev, adjusting with config file ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ mv valid.my dev.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ mv valid.th dev.th
```

## Training  

command ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ time xnmt --backend torch --gpu ./config.baseline.my-th-word.yaml | tee my-th.dropout-word.log
```

result ...  

```
[asean.baseline.my-th] Epoch 16.7719: train_loss/word=2.323018 (steps=7530, words/sec=7169.06, time=0-00:14:45)
[asean.baseline.my-th] Epoch 16.8224: train_loss/word=2.354590 (steps=7553, words/sec=6744.07, time=0-00:14:46)
[asean.baseline.my-th] Epoch 16.8729: train_loss/word=2.351877 (steps=7577, words/sec=6755.44, time=0-00:14:48)
[asean.baseline.my-th] Epoch 16.9239: train_loss/word=2.297239 (steps=7599, words/sec=7792.73, time=0-00:14:49)
[asean.baseline.my-th] Epoch 16.9762: train_loss/word=2.347510 (steps=7624, words/sec=7885.17, time=0-00:14:50)
[asean.baseline.my-th] Epoch 17.0000: train_loss/word=2.299110 (steps=7633, words/sec=8949.01, time=0-00:14:50)
> Checkpoint [asean.baseline.my-th]
Performing inference on ./data/dev.my and ./data/dev.th
Starting to read ./data/dev.my and ./data/dev.th
Done reading ./data/dev.my and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.my-th] Epoch 17.0000 dev BLEU4: 0.20172180917679228, 0.455431/0.258125/0.151442/0.093006 (BP = 1.000000, ratio=1.01, hyp_len=6877, ref_len=6809) (time=0-00:15:17)
[asean.baseline.my-th]              dev auxiliary GLEU: 0.219040
[asean.baseline.my-th]              dev auxiliary Loss: 4.623 (ref_len=6809)
             checkpoint took 0-00:00:27
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.th
Performing inference on ./data/test.my and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.my-th          | BLEU4: 0.20203486452368793, 0.455994/0.258342/0.152916/0.092491 (BP = 1.000000, ratio=1.02, hyp_len=6965, ref_len=6809)
                              | GLEU: 0.221651
                              | WER: 80.25% ( C/S/I/D: 2850/2610/1505/1349; hyp_len=6965, ref_len=6809 )
                              | CER: 65.10% ( C/S/I/D: 14425/10126/3672/6263; hyp_len=28223, ref_len=30814 )
                              | BLEU4: 0.22506257721500164, 0.483277/0.279062/0.174677/0.116119 (BP = 0.984113, ratio=0.98, hyp_len=7056, ref_len=7169)
                              | GLEU: 0.242567
                              | WER: 73.92% ( C/S/I/D: 3086/2754/1216/1329; hyp_len=7056, ref_len=7169 )
                              | CER: 63.75% ( C/S/I/D: 14848/9869/3596/6324; hyp_len=28313, ref_len=31041 )

real    16m23.986s
user    16m22.851s
sys     0m2.234s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$
```

command for th-my:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ time xnmt --backend torch --gpu ./config.baseline.th-my-word.yaml | tee th-my.dropout-word.log
```

result is as follows:  

```
[asean.baseline.th-my] Epoch 20.8716: train_loss/word=1.889703 (steps=10016, words/sec=9418.34, time=0-00:21:03)
[asean.baseline.th-my] Epoch 20.9234: train_loss/word=1.921971 (steps=10041, words/sec=9097.48, time=0-00:21:04)
[asean.baseline.th-my] Epoch 20.9747: train_loss/word=1.921831 (steps=10066, words/sec=8264.88, time=0-00:21:05)
[asean.baseline.th-my] Epoch 21.0000: train_loss/word=1.982251 (steps=10078, words/sec=8481.19, time=0-00:21:06)
> Checkpoint [asean.baseline.th-my]
Performing inference on ./data/dev.th and ./data/dev.my
Starting to read ./data/dev.th and ./data/dev.my
Done reading ./data/dev.th and ./data/dev.my. Packing into batches.
Done packing batches.
[asean.baseline.th-my] Epoch 21.0000 dev BLEU4: 0.1914505704883847, 0.470950/0.244157/0.139027/0.084040 (BP = 1.000000, ratio=1.04, hyp_len=9931, ref_len=9573) (time=0-00:21:40)
[asean.baseline.th-my]              dev auxiliary GLEU: 0.226395
[asean.baseline.th-my]              dev auxiliary Loss: 4.420 (ref_len=9573)
             checkpoint took 0-00:00:33
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.my
Performing inference on ./data/test.th and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.th-my          | BLEU4: 0.19669169444262083, 0.501321/0.263197/0.150997/0.093260 (BP = 0.947372, ratio=0.95, hyp_len=9082, ref_len=9573)
                              | GLEU: 0.234573
                              | WER: 66.62% ( C/S/I/D: 4281/3715/1086/1577; hyp_len=9082, ref_len=9573 )
                              | CER: 61.24% ( C/S/I/D: 19143/9822/4847/7915; hyp_len=33812, ref_len=36880 )
                              | BLEU4: 0.20307924386482126, 0.516104/0.274670/0.158236/0.093724 (BP = 0.948395, ratio=0.95, hyp_len=9097, ref_len=9579)
                              | GLEU: 0.242634
                              | WER: 65.95% ( C/S/I/D: 4353/3653/1091/1573; hyp_len=9097, ref_len=9579 )
                              | CER: 60.84% ( C/S/I/D: 19324/9861/4800/7902; hyp_len=33985, ref_len=37087 )

real    22m59.149s
user    22m57.968s
sys     0m2.375s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$
```

## No Dropout

## Update Configuration Files

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ head ./config.baseline.nodropout.my-th-word.yaml
# standard settings
asean.baseline.nodropout.my-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ head ./config.baseline.nodropout.th-my-word.yaml
# standard settings
asean.baseline.nodropout.th-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

## Training

command for ASEAN-MT domain, my-th, baseline, nodropout training, developing and testing ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ time xnmt --backend torch --gpu ./config.baseline.nodropout.my-th-word.yaml | tee my-th.nodropout-word.log
```

result:  

```
[asean.baseline.nodropout.my-th] Epoch 22.0000: train_loss/word=1.558586 (steps=9886, words/sec=9570.28, time=0-00:18:19)
> Checkpoint [asean.baseline.nodropout.my-th]
Performing inference on ./data/dev.my and ./data/dev.th
Starting to read ./data/dev.my and ./data/dev.th
Done reading ./data/dev.my and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.nodropout.my-th] Epoch 22.0000 dev BLEU4: 0.2101315519557975, 0.438703/0.249130/0.158752/0.112370 (BP = 1.000000, ratio=1.04, hyp_len=7064, ref_len=6809) (time=0-00:18:48)
[asean.baseline.nodropout.my-th]              dev auxiliary GLEU: 0.222889
[asean.baseline.nodropout.my-th]              dev auxiliary Loss: 5.221 (ref_len=6809)
             checkpoint took 0-00:00:28
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.th
Performing inference on ./data/test.my and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.nodropout.my-th| BLEU4: 0.21606688933375506, 0.446223/0.256901/0.162897/0.116714 (BP = 1.000000, ratio=1.02, hyp_len=6936, ref_len=6809)
                              | GLEU: 0.227172
                              | WER: 79.20% ( C/S/I/D: 2809/2734/1393/1266; hyp_len=6936, ref_len=6809 )
                              | CER: 66.75% ( C/S/I/D: 14231/10543/3985/6040; hyp_len=28759, ref_len=30814 )
                              | BLEU4: 0.23035157520273358, 0.469646/0.276815/0.177735/0.125536 (BP = 0.992580, ratio=0.99, hyp_len=7116, ref_len=7169)
                              | GLEU: 0.241452
                              | WER: 75.27% ( C/S/I/D: 3006/2877/1233/1286; hyp_len=7116, ref_len=7169 )
                              | CER: 65.40% ( C/S/I/D: 14638/10327/3899/6076; hyp_len=28864, ref_len=31041 )

real    19m56.165s
user    19m54.828s
sys     0m2.495s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$
```

command for ASEAN-MT domain, th-my, baseline, nodropout training, developing and testing ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ time xnmt --backend torch --gpu ./config.baseline.nodropout.th-my-word.yaml | tee th-my.nodropout-word.log
```

result:  

```
[asean.baseline.nodropout.th-my] Epoch 20.0000: train_loss/word=1.523459 (steps=9588, words/sec=10398.03, time=0-00:18:33)
> Checkpoint [asean.baseline.nodropout.th-my]
Performing inference on ./data/dev.th and ./data/dev.my
Starting to read ./data/dev.th and ./data/dev.my
Done reading ./data/dev.th and ./data/dev.my. Packing into batches.
Done packing batches.
[asean.baseline.nodropout.th-my] Epoch 20.0000 dev BLEU4: 0.18478946453988845, 0.451635/0.234740/0.134345/0.081868 (BP = 1.000000, ratio=1.08, hyp_len=10369, ref_len=9573) (time=0-00:19:07)
[asean.baseline.nodropout.th-my]              dev auxiliary GLEU: 0.219028
[asean.baseline.nodropout.th-my]              dev auxiliary Loss: 4.860 (ref_len=9573)
             checkpoint took 0-00:00:34
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.my
Performing inference on ./data/test.th and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.nodropout.th-my| BLEU4: 0.1965397432007515, 0.477448/0.247689/0.142230/0.088711 (BP = 1.000000, ratio=1.00, hyp_len=9578, ref_len=9573)
                              | GLEU: 0.229072
                              | WER: 69.72% ( C/S/I/D: 4270/3937/1371/1366; hyp_len=9578, ref_len=9573 )
                              | CER: 64.85% ( C/S/I/D: 19023/10934/6061/6923; hyp_len=36018, ref_len=36880 )
                              | BLEU4: 0.18707112108997567, 0.483076/0.248048/0.135229/0.079684 (BP = 0.986865, ratio=0.99, hyp_len=9454, ref_len=9579)
                              | GLEU: 0.224308
                              | WER: 70.06% ( C/S/I/D: 4224/3874/1356/1481; hyp_len=9454, ref_len=9579 )
                              | CER: 64.56% ( C/S/I/D: 18971/10735/5827/7381; hyp_len=35533, ref_len=37087 )

real    20m25.896s
user    20m24.716s
sys     0m2.339s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$
```

## SwitchOut with DropOut

Preparing two configuration files ...  
1st copied switchout config from the previous experiment and then rename the filename ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cp ../asean-mt-switchout/config.switchout.en-th-word.yaml .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ mv ./config.switchout.en-th-word.yaml ./config.switchout.my-th-word.yaml
```

updated configuration file:  

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cat ./config.switchout.my-th-word.yaml
# standard settings
switchout.asean.my-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.my'
      - '{EXP_DIR}/data/train.th'
      out_files:
      - '{EXP_DIR}/vocab.my'
      - '{EXP_DIR}/vocab.th'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
      tau: 0.8
    trg_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.th'}
      tau: 0.8
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 30  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/data/train.my'
    trg_file: '{EXP_DIR}/data/train.th'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.my'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.th'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.th'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.th'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.my'
      ref_file: &test_trg '{EXP_DIR}/data/test.th'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.th'
```

## Training

training for ASEAN-MT domain, my-th, switchout, dropout=0.3, word unit ...  

```
 time xnmt --backend torch --gpu ./config.switchout.my-th-word.yaml | tee my-th.switchout.dropout-word.log
```

Evaluation results are as follows:  

```

```

```

```

```

```

```

```

```

```

```

```
