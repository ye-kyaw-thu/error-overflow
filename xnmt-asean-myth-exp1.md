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

```

```

```

```

```

```

```

```
