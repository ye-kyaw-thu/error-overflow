# XNMT Experiment with Transformer Architecture

ဒီတစ်ခါတော့ XNMT ကို Transformer architecture နဲ့ run ကြည့်မယ်။  
Corpus ကတော့ မြအိစံနဲ့အတူ ဆောက်ထားကြတဲ့ medical domain ပါပဲ။  
ရှေ့မှာ run ခဲ့တဲ့ seq2seq ရဲ့ အဆက်ပါ။   

y@LST Lab., Thailand  
2 May 2022

## Folder preparation

folder အသစ်ဆောက်ပြီး data တွေကိုလည်း ကော်ပီကူးခဲ့တယ်။  
```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ mkdir word_tran
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ mkdir syl_tran
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ cp -r syl/data/ ./syl_tran/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ cp -r word/data/ ./word_tran/
```

## config File Preparation (word, transformer)

config ဖိုင်က အောက်ပါ link ကို reference လုပ်ခဲ့တယ်။  
https://github.com/neulab/xnmt/blob/transformer-optimizations/examples/16_transformer.yaml  


အဓိက update လုပ်ခဲ့တာက   
- training, dev, test ဖိုင်တွေရဲ့ data path
- Vocab ကို ကိုယ်သတ်မှတ်ထားတဲ့ segmentation unit နဲ့ပဲ ဆောက်ချင်လို့ !PreprocRunner ကို ထည့်ခဲ့တယ်။  
- dropout rate ကို ရှေ့က run ခဲ့တဲ့ seq2seq နဲ့ တူအောင်လို့ 0.2 ကနေ 0.3 အဖြစ် ပြောင်းခဲ့တယ်။
- refer လုပ်ခဲ့တဲ့ original transformer config ဖိုင်မှာက dev အတွက်ပဲ evaluation လုပ်ထားလို့ !AccuracyEvalTask အသစ်တစ်ခု အနေနဲ့ test set အတွက်ပါ ဖြည့်ခဲ့


Transformer architecture နဲ့ en-my အတွက် update လုပ်ခဲ့တဲ့ config ဖိုင်က အောက်ပါအတိုင်း ...  

```yaml
# This example demonstrates how to use the Transformer architecture following
# https://arxiv.org/abs/1706.03762
# modify by Ye Kyaw Thu, LST, NECTEC for NMT Medical Domain Experiment
# Last updated: 2 May 2022
transformer.word.en-my: !Experiment
  exp_global: !ExpGlobal
    dropout: 0.3
    default_layer_dim: 512
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.en'
      - '{EXP_DIR}/data/train.my'
      out_files:
      - '{EXP_DIR}/vocab.en'
      - '{EXP_DIR}/vocab.my'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words    
  model: !TransformerTranslator
    src_embedder: !SimpleWordEmbedder
      param_init: !LeCunUniformInitializer {}
    encoder: !TransformerEncoder
      layers: 1
    trg_embedder: !SimpleWordEmbedder
      param_init: !LeCunUniformInitializer {}
    decoder: !TransformerDecoder
      layers: 1
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
    inference: !SimpleInference {}
  train: !SimpleTrainingRegimen
    run_for_epochs: 30
    batcher: !SentShuffleBatcher
      batch_size: 100
    restart_trainer: False
    trainer: !TransformerAdamTrainer
      alpha: 1.0
      warmup_steps: 4000
    lr_decay: 1.0
    src_file: '{EXP_DIR}/data/train.en'
    trg_file: '{EXP_DIR}/data/train.my'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.en'
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
      src_file: &test_src '{EXP_DIR}/data/test.en'
      ref_file: &test_trg '{EXP_DIR}/data/test.my'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.my'
```
