# ASEAN-MT Domain My-Th, Th-My, SwitchOut Experiment with Syllable Unit

## Syllable Breaking

I already downloaded sylbreak.pl and clean-space.pl tools ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ ls
clean-space.pl  dev.my  print-blank-lines.pl  sylbreak.pl  test.my  train.my
```

Currently, word segmented Myanmar data:  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 3 *.my
==> dev.my <==
ဒိုင်ဗင် ထိုး တဲ့ စင် ၊ ဒိုင်ဗင်ဘုတ် နဲ့ လမ်း တွေ မ ရှိ ဘူး ။
၅၀ ဘတ် ကို အကြွေ လဲ ပေး မလား ။
အမျိုးသားပြတိုက် ကို ဘယ်လို သွား ရ မလဲ ။

==> test.my <==
ကျသင့်ငွေ ဘယ်လောက် လဲ ။
ကျွန်တော် လက်ဆောင် အနေ နဲ့ ပေး လို့ ရ တဲ့ ပစ္စည်း မျိုး ကြည့် ချင် လို့ ။
ရထား က ကြာ နေ တာ လား ။

==> train.my <==
ဟုတ်ကဲ့ ၊ ကျွန်တော် ထိုင်း စစ်တုရင် ကစား ရ တာ ကြိုက် တယ် ။
ကလေးများ အတွက် တစ် ခု ခု အကြံပြု ပေး နိုင် မလား ။
အဲဒီ ကို ဘယ်လို ရောက် နိုင် မလဲ ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

Syllable Breaking ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./train.my -s " " > train.syl
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./dev.my -s " " > dev.syl
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./test.my -s " " > test.syl
```

confirmed with wc command ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ wc *.syl
   1031   13394  141200 dev.syl
   1000   13473  141923 test.syl
  19994  263503 2790412 train.syl
  22025  290370 3073535 total
```

no. of words should be bigger than word segmented files ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ wc *.my
   1031    9573  119279 dev.my
   1000    9579  119884 test.my
  19994  187544 2359638 train.my
  22025  206696 2598801 total
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

check the file content ... it looks OK ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 5 *.syl
==> dev.syl <==
 ဒိုင် ဗင်   ထိုး   တဲ့   စင်   ၊   ဒိုင် ဗင် ဘုတ်   နဲ့   လမ်း   တွေ   မ   ရှိ   ဘူး   ။
 ၅ ၀   ဘတ်   ကို   အ ကြွေ   လဲ   ပေး   မ လား   ။
 အ မျိုး သား ပြ တိုက်   ကို   ဘယ် လို   သွား   ရ   မ လဲ   ။
 ဒီ   နေ ရာ   က   ပြိုင် ဘက် ကင်း   ပဲ   ။
 တ ခြား   အ ခန်း   တွေ‌   ရော   ရ   နိုင်   မ လား   ။

==> test.syl <==
 ကျ သင့် ငွေ   ဘယ် လောက်   လဲ   ။
 ကျွန် တော်   လက် ဆောင်   အ နေ   နဲ့   ပေး   လို့   ရ   တဲ့   ပစ္စည်း   မျိုး   ကြည့်   ချင်   လို့   ။
 ရ ထား   က   ကြာ   နေ   တာ   လား   ။
 တံ ခါး   နောက်   မှာ   ရပ်   ပါ   ။
 ခ ဏ   လောက်   ။

==> train.syl <==
 ဟုတ် ကဲ့   ၊   ကျွန် တော်   ထိုင်း   စစ် တု ရင်   က စား   ရ   တာ   ကြိုက်   တယ်   ။
 က လေး များ   အ တွက်   တစ်   ခု   ခု   အ ကြံ ပြု   ပေး   နိုင်   မ လား   ။
 အဲ ဒီ   ကို   ဘယ် လို   ရောက်   နိုင်   မ လဲ   ။
 တစ် ကိုယ် လုံး   ကိုက် ခဲ   နေ   လို့   ။
 ကျွန် တော်   တို့   အ တွက်   လုပ်   ပေး   ခဲ့   တာ   တွေ   ကျေး ဇူး တင်   ပါ   တယ်   ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

## Cleaning Spaces

Current sylbreak program is just showing the concept of syllable breaking with regular expression and you need to make space cleaning ...    

changed file names of word segmented training, dev and test files:  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv train.my train.word
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv dev.my dev.word
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv test.my test.word
```

run space cleaning perl script ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./train.syl > train.my
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./dev.syl > dev.my
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./test.syl > test.my
```

Check the cleaned files...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 5 {train,dev,test}.my
==> train.my <==
ဟုတ် ကဲ့ ၊ ကျွန် တော် ထိုင်း စစ် တု ရင် က စား ရ တာ ကြိုက် တယ် ။
က လေး များ အ တွက် တစ် ခု ခု အ ကြံ ပြု ပေး နိုင် မ လား ။
အဲ ဒီ ကို ဘယ် လို ရောက် နိုင် မ လဲ ။
တစ် ကိုယ် လုံး ကိုက် ခဲ နေ လို့ ။
ကျွန် တော် တို့ အ တွက် လုပ် ပေး ခဲ့ တာ တွေ ကျေး ဇူး တင် ပါ တယ် ။

==> dev.my <==
ဒိုင် ဗင် ထိုး တဲ့ စင် ၊ ဒိုင် ဗင် ဘုတ် နဲ့ လမ်း တွေ မ ရှိ ဘူး ။
၅ ၀ ဘတ် ကို အ ကြွေ လဲ ပေး မ လား ။
အ မျိုး သား ပြ တိုက် ကို ဘယ် လို သွား ရ မ လဲ ။
ဒီ နေ ရာ က ပြိုင် ဘက် ကင်း ပဲ ။
တ ခြား အ ခန်း တွေ‌ ရော ရ နိုင် မ လား ။

==> test.my <==
ကျ သင့် ငွေ ဘယ် လောက် လဲ ။
ကျွန် တော် လက် ဆောင် အ နေ နဲ့ ပေး လို့ ရ တဲ့ ပစ္စည်း မျိုး ကြည့် ချင် လို့ ။
ရ ထား က ကြာ နေ တာ လား ။
တံ ခါး နောက် မှာ ရပ် ပါ ။
ခ ဏ လောက် ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

copied syllable breaked Myanmar files to the path data/  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ cp *.my ../
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ cd ..
```

make confirmation ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$ wc *.my
   1031   13394  123100 dev.my
   1000   13473  123778 test.my
  19994  263503 2435597 train.my
  22025  290370 2682475 total
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$
```

confirmation the no. of sentences with Thai corpus also ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$ wc *.th
   1031    6809   98543 dev.th
   1000    7169   99326 test.th
  19994  139767 1951021 train.th
  22025  153745 2148890 total
```

## Prepare Configuration Files for Syllable Unit Experiments 

Generally same configuration files with word unit experiments, I just added "syl" to the name of the experiments ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ head -3 config.*
==> config.baseline.my-th-syl.yaml <==
# standard settings
asean.baseline.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.nodropout.my-th-syl.yaml <==
# standard settings
asean.baseline.nodropout.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.nodropout.th-my-syl.yaml <==
# standard settings
asean.baseline.nodropout.syl.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.th-my-syl.yaml <==
# standard settings
asean.baseline.syl.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.my-th-syl.yaml <==
# standard settings
switchout.asean.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.nodropout.my-th-syl.yaml <==
# standard settings
switchout.nodropout.syl.asean.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.nodropout.th-my-syl.yaml <==
# standard settings
switchout.nodropout.syl.asean.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.th-my-syl.yaml <==
# standard settings
switchout.asean.syl.th-my: !Experiment
  exp_global: !ExpGlobal
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$
```

## Training Baseline, Syllable with Dropout  

Configuration file for ASEAN-MT domain, my-th, syllable, dropout  

```yaml
# standard settings
asean.baseline.syl.my-th: !Experiment
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

result ...  

```
(xnmt-py3.6) (base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ time xnmt --backend torch --gpu ./config.baseline.my-th-syl.yaml | tee my-th.dropout-syl.log
...
...
...
[asean.baseline.syl.my-th] Epoch 23.0000: train_loss/word=1.981130 (steps=9830, words/sec=7388.01, time=0-00:20:27)
> Checkpoint [asean.baseline.syl.my-th]
Performing inference on ./data/dev.my and ./data/dev.th
Starting to read ./data/dev.my and ./data/dev.th
Done reading ./data/dev.my and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.syl.my-th] Epoch 23.0000 dev BLEU4: 0.22922427960529682, 0.452423/0.269354/0.176910/0.128062 (BP = 1.000000, ratio=1.07, hyp_len=7283, ref_len=6809) (time=0-00:20:57)
[asean.baseline.syl.my-th]              dev auxiliary GLEU: 0.238062
[asean.baseline.syl.my-th]              dev auxiliary Loss: 4.642 (ref_len=6809)
             checkpoint took 0-00:00:30
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.th
Performing inference on ./data/test.my and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.syl.my-th      | BLEU4: 0.23014186330201042, 0.456549/0.270465/0.176129/0.128989 (BP = 1.000000, ratio=1.07, hyp_len=7261, ref_len=6809)
                              | GLEU: 0.241488
                              | WER: 79.76% ( C/S/I/D: 3002/2635/1624/1172; hyp_len=7261, ref_len=6809 )
                              | CER: 63.41% ( C/S/I/D: 14988/10059/3713/5767; hyp_len=28760, ref_len=30814 )
                              | BLEU4: 0.2283041114724462, 0.472327/0.278864/0.175812/0.117320 (BP = 1.000000, ratio=1.04, hyp_len=7444, ref_len=7169)
                              | GLEU: 0.243820
                              | WER: 76.75% ( C/S/I/D: 3193/2725/1526/1251; hyp_len=7444, ref_len=7169 )
                              | CER: 63.49% ( C/S/I/D: 15273/9786/3939/5982; hyp_len=28998, ref_len=31041 )

real    22m7.352s
user    22m6.139s
sys     0m2.383s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$
```

Configuration file for ASEAN-MT domain, th-my, syllable, dropout  

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ cat ./config.baseline.th-my-syl.yaml
# standard settings
asean.baseline.syl.th-my: !Experiment
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

result for baseline, th-my, dropout=0.3  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ time xnmt --backend torch --gpu ./config.baseline.th-my-syl.yaml | tee th-my.dropout-syl.log
...
...
...
[asean.baseline.syl.th-my] Epoch 18.0000: train_loss/word=1.760576 (steps=9507, words/sec=8107.18, time=0-00:24:03)
> Checkpoint [asean.baseline.syl.th-my]
Performing inference on ./data/dev.th and ./data/dev.my
Starting to read ./data/dev.th and ./data/dev.my
Done reading ./data/dev.th and ./data/dev.my. Packing into batches.
Done packing batches.
[asean.baseline.syl.th-my] Epoch 18.0000 dev BLEU4: 0.2566258276500028, 0.505264/0.310275/0.199814/0.138456 (BP = 1.000000, ratio=1.04, hyp_len=13868, ref_len=13394) (time=0-00:24:45)
[asean.baseline.syl.th-my]              dev auxiliary GLEU: 0.266111
[asean.baseline.syl.th-my]              dev auxiliary Loss: 3.351 (ref_len=13394)
             checkpoint took 0-00:00:42
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.my
Performing inference on ./data/test.th and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.syl.th-my      | BLEU4: 0.2652767701968845, 0.518840/0.322356/0.207617/0.142615 (BP = 1.000000, ratio=1.02, hyp_len=13694, ref_len=13394)
                              | GLEU: 0.274291
                              | WER: 70.05% ( C/S/I/D: 6420/4866/2408/2108; hyp_len=13694, ref_len=13394 )
                              | CER: 65.79% ( C/S/I/D: 20462/10162/7846/6256; hyp_len=38470, ref_len=36880 )
                              | BLEU4: 0.26469023060014685, 0.529932/0.326540/0.205251/0.138570 (BP = 0.999332, ratio=1.00, hyp_len=13464, ref_len=13473)
                              | GLEU: 0.273250
                              | WER: 69.21% ( C/S/I/D: 6381/4851/2232/2241; hyp_len=13464, ref_len=13473 )
                              | CER: 63.96% ( C/S/I/D: 20358/10132/6992/6597; hyp_len=37482, ref_len=37087 )

real    26m15.653s
user    26m14.548s
sys     0m2.289s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$
```

## Training for Baseline, no-dropout and Syllable Unit

Configuration file for my-th, seq2seq, no-dropout ...  

```yaml(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ cat ./config.baseline.nodropout.my-th-syl.yaml
# standard settings
asean.baseline.nodropout.syl.my-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
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

