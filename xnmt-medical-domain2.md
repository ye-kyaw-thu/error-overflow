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

## Training Transformer (en-my)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_tran$ time xnmt --backend torch --gpu ./transformer-word-en-my.yaml 
ERROR: for proper deserialization of a class object, make sure the class is a subclass of xnmt.serialize.serializable.Serializable, specifies a proper yaml_tag with leading '!', and its module is imported under xnmt/__init__.py
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 62, in main
    config_experiment_names = YamlPreloader.experiment_names_from_file(args.experiments_file)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 875, in experiment_names_from_file
    experiments = yaml.load(stream, Loader=yaml.Loader)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/__init__.py", line 81, in load
    return loader.get_single_data()
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 51, in get_single_data
    return self.construct_document(node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 60, in construct_document
    for dummy in generator:
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 423, in construct_yaml_object
    state = self.construct_mapping(node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 218, in construct_mapping
    return super().construct_mapping(node, deep=deep)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 143, in construct_mapping
    value = self.construct_object(value_node, deep=deep)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 100, in construct_object
    data = constructor(self, node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 429, in construct_undefined
    node.start_mark)
yaml.constructor.ConstructorError: could not determine a constructor for the tag '!SimpleInference'
  in "./transformer-word-en-my.yaml", line 37, column 16

real	0m1.436s
user	0m1.700s
sys	0m0.640s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_tran$
```

အထက်ပါအတိုင်း error ပေးနေလို့ အောက်ပါ စာကြောင်းကို ဖြုတ်ကြည့်ရင် မရ။ error ဆက်ပေးနေခဲ့တယ်...  

```yxaml
    inference: !SimpleInference {}    
```

ပေးတဲ့ Error ကတော့ အောက်ပါအတိုင်း...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_tran$ time xnmt --backend torch --gpu ./transformer-word-en-my.yaml 
ERROR: for proper deserialization of a class object, make sure the class is a subclass of xnmt.serialize.serializable.Serializable, specifies a proper yaml_tag with leading '!', and its module is imported under xnmt/__init__.py
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 62, in main
    config_experiment_names = YamlPreloader.experiment_names_from_file(args.experiments_file)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 875, in experiment_names_from_file
    experiments = yaml.load(stream, Loader=yaml.Loader)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/__init__.py", line 81, in load
    return loader.get_single_data()
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 51, in get_single_data
    return self.construct_document(node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 60, in construct_document
    for dummy in generator:
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 423, in construct_yaml_object
    state = self.construct_mapping(node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 218, in construct_mapping
    return super().construct_mapping(node, deep=deep)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 143, in construct_mapping
    value = self.construct_object(value_node, deep=deep)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 100, in construct_object
    data = constructor(self, node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/yaml/constructor.py", line 429, in construct_undefined
    node.start_mark)
yaml.constructor.ConstructorError: could not determine a constructor for the tag '!TransformerAdamTrainer'
  in "./transformer-word-en-my.yaml", line 42, column 14

real	0m1.438s
user	0m1.814s
sys	0m0.532s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_tran$
```


## Reference

- https://github.com/neulab/xnmt/blob/transformer-optimizations/examples/16_transformer.yaml
- https://msperber-xnmt.readthedocs.io/en/latest/_modules/xnmt/optimizer.html
- 
