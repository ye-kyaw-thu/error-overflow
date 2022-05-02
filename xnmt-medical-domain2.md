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

## Debugging the Error

xnmt ဖိုလ်ဒါ အထက်ကို တက်ကြည့်လိုက်ပြီးတော့ python source code တွေမှာပဲ ဖြစ်ဖြစ်၊ TransformerAdamTrainer ဆိုတာ ရှိသလား၊ ရှိရင် filename ရော line-no ပါ ရိုက်ထုတ်ပေးခိုင်းကြည့်ခဲ့ပေမဲ့... ရှိပုံမရ  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ grep -rnw './' -e 'TransformerAdamTrainer' 
./exp/medical1/word_tran/transformer-word-en-my.yaml:43:    trainer: !TransformerAdamTrainer
./exp/medical1/word_tran/transformer-word-my-en.yaml:43:    trainer: !TransformerAdamTrainer

```

အဲဒါကြောင့် ဘယ် source ဖိုင်မှာ Trainer တွေနဲ့ ပတ်သက်ပြီး ရေးထားသလဲ ဆိုတာကို သိချင်လို့ အောက်ပါအတိုင်း ရှာကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ grep -rnw './' -e 'AdamTrainer' 
./xnmt/optimizers.py:364:  yaml_tag = '!AdamTrainer'
./xnmt/optimizers.py:374:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(), alpha, beta_1, beta_2, eps),
./xnmt/optimizers.py:396:  yaml_tag = '!AdamTrainer'
./xnmt/optimizers.py:418:AdamTrainer = xnmt.resolve_backend(AdamTrainerDynet, AdamTrainerTorch)
./xnmt/optimizers.py:451:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(),
./xnmt/persistence.py:819:                [{"path" : "model.trainer", "val":AdamTrainer()},
./docs/experiment_config_files.rst:116:    trainer: !AdamTrainer
./test/test_training.py:355:    train_args['trainer'] = optimizers.AdamTrainer(alpha=0.1, rescale_grads=5.0, skip_noisy=True)
./test/config/speech_retrieval.yaml:32:    trainer: !AdamTrainer
./test/config/retrieval.yaml:19:    trainer: !AdamTrainer
./test/config/load_model.yaml:57:    val: !AdamTrainer
./test/config/speech.yaml:44:    trainer: !AdamTrainer {}
./test/config/classifier-torch.yaml:18:    trainer: !AdamTrainer
./test/config/multi_task_speech.yaml:6:    trainer: !AdamTrainer {}
./test/config/multi_task.yaml:8:    trainer: !AdamTrainer {}
./test/config/multi_task.yaml:106:    trainer: !AdamTrainer {}
./test/config/multi_task.yaml:113:    trainer: !AdamTrainer {}
./test/config/lm.yaml:15:    trainer: !AdamTrainer
./test/config/pretrained_embeddings.yaml:26:    trainer: !AdamTrainer
./test/config/lattice.yaml:36:    trainer: !AdamTrainer
./test/config/seq_labeler.yaml:21:    trainer: !AdamTrainer
./test/config/classifier.yaml:18:    trainer: !AdamTrainer
./examples/07_load_finetune.yaml:64:    val: !AdamTrainer
./examples/01_standard.yaml:41:    trainer: !AdamTrainer
./examples/22_switchout.yaml:43:    trainer: !AdamTrainer
./examples/13_speech.yaml:53:    trainer: !AdamTrainer {}
./examples/09_programmatic.py:37:from xnmt.optimizers import AdamTrainer
./examples/09_programmatic.py:91:  trainer=AdamTrainer(alpha=0.001),
./examples/12_multi_task.yaml:13:    trainer: !AdamTrainer {}
./examples/models/standard.mod:442:  trainer: !AdamTrainer
./examples/19_subword_sample.yaml:49:    trainer: !AdamTrainer
./examples/18_lexiconbias.yaml:39:    trainer: !AdamTrainer
./examples/logs/standard.log:46:initialized train.trainer: AdamTrainer@139669774376576({'alpha': 0.001})
./examples/logs/standard.log:54:initialized train: SimpleTrainingRegimen@139669774375568({'model': DefaultTranslator@139669774374672, 'src_file': 'examples/data/head.ja', 'trg_file': 'examples/data/head.en', 'batcher': SrcBatcher@139669774055520, 'loss_calculator': MLELoss@139669774054288, 'trainer': AdamTrainer@139669774055576, 'run_for_epochs': 2, 'dev_tasks': [LossEvalTask@139669774421296], 'name': 'standard', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@139669774419840, 'dev_loss_tracker': DevLossTracker@139669774057424})
./build/lib/xnmt/optimizers.py:364:  yaml_tag = '!AdamTrainer'
./build/lib/xnmt/optimizers.py:374:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(), alpha, beta_1, beta_2, eps),
./build/lib/xnmt/optimizers.py:396:  yaml_tag = '!AdamTrainer'
./build/lib/xnmt/optimizers.py:418:AdamTrainer = xnmt.resolve_backend(AdamTrainerDynet, AdamTrainerTorch)
./build/lib/xnmt/optimizers.py:451:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(),
./build/lib/xnmt/persistence.py:819:                [{"path" : "model.trainer", "val":AdamTrainer()},
./exp/medical1/word/config.medical.my-en-word.yaml:58:    trainer: !AdamTrainer
./exp/medical1/word/config.medical.en-my-word.yaml:58:    trainer: !AdamTrainer
./exp/medical1/word/models/medical.en-my.mod:26725:  trainer: !AdamTrainer
./exp/medical1/word/models/medical.my-en.mod:26725:  trainer: !AdamTrainer
./exp/medical1/word/logs/medical.en-my.log:68:initialized train.trainer: AdamTrainer@140560390124320({'alpha': 0.001})
./exp/medical1/word/logs/medical.en-my.log:78:initialized train: SimpleTrainingRegimen@140560390125104({'model': DefaultTranslator@140560390053448, 'src_file': './data/train.en', 'trg_file': './data/train.my', 'batcher': WordSrcBatcher@140560390067256, 'loss_calculator': MLELoss@140560390003232, 'trainer': AdamTrainer@140560380492824, 'run_for_epochs': 30, 'lr_decay': 0.5, 'lr_decay_times': 2, 'patience': 1, 'initial_patience': 2, 'dev_tasks': [AccuracyEvalTask@140560390001104, LossEvalTask@140560390002784], 'name': 'medical.en-my', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@140560390001552, 'dev_loss_tracker': DevLossTracker@140560390051040})
./exp/medical1/word/logs/medical.my-en.log:68:initialized train.trainer: AdamTrainer@140366526506432({'alpha': 0.001})
./exp/medical1/word/logs/medical.my-en.log:78:initialized train: SimpleTrainingRegimen@140366526505312({'model': DefaultTranslator@140366526442856, 'src_file': './data/train.my', 'trg_file': './data/train.en', 'batcher': WordSrcBatcher@140366576648032, 'loss_calculator': MLELoss@140366517927328, 'trainer': AdamTrainer@140366517926432, 'run_for_epochs': 30, 'lr_decay': 0.5, 'lr_decay_times': 2, 'patience': 1, 'initial_patience': 2, 'dev_tasks': [AccuracyEvalTask@140366517926096, LossEvalTask@140366526382992], 'name': 'medical.my-en', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@140366517926936, 'dev_loss_tracker': DevLossTracker@140366517927496})
./exp/medical1/syl/config.medical.my-en-syl.yaml:58:    trainer: !AdamTrainer
./exp/medical1/syl/config.medical.en-my-syl.yaml:58:    trainer: !AdamTrainer
./exp/medical1/syl/models/medical.syl.my-en.mod:12158:  trainer: !AdamTrainer
./exp/medical1/syl/models/medical.syl.en-my.mod:12158:  trainer: !AdamTrainer
./exp/medical1/syl/logs/medical.syl.my-en.log:68:initialized train.trainer: AdamTrainer@139619423188416({'alpha': 0.001})
./exp/medical1/syl/logs/medical.syl.my-en.log:78:initialized train: SimpleTrainingRegimen@139619423187296({'model': DefaultTranslator@139619423120744, 'src_file': './data/train.my', 'trg_file': './data/train.en', 'batcher': WordSrcBatcher@139619423154920, 'loss_calculator': MLELoss@139619418282864, 'trainer': AdamTrainer@139619418282584, 'run_for_epochs': 30, 'lr_decay': 0.5, 'lr_decay_times': 2, 'patience': 1, 'initial_patience': 2, 'dev_tasks': [AccuracyEvalTask@139619423187520, LossEvalTask@139619423154528], 'name': 'medical.syl.my-en', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@139619423060880, 'dev_loss_tracker': DevLossTracker@139619418283200})
./exp/medical1/syl/logs/medical.syl.en-my.log:68:initialized train.trainer: AdamTrainer@139754384610584({'alpha': 0.001})
./exp/medical1/syl/logs/medical.syl.en-my.log:78:initialized train: SimpleTrainingRegimen@139754384609408({'model': DefaultTranslator@139754384548696, 'src_file': './data/train.en', 'trg_file': './data/train.my', 'batcher': WordSrcBatcher@139754384549984, 'loss_calculator': MLELoss@139754384551440, 'trainer': AdamTrainer@139754384609968, 'run_for_epochs': 30, 'lr_decay': 0.5, 'lr_decay_times': 2, 'patience': 1, 'initial_patience': 2, 'dev_tasks': [AccuracyEvalTask@139754379710248, LossEvalTask@139754384491520], 'name': 'medical.syl.en-my', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@139754384491184, 'dev_loss_tracker': DevLossTracker@139754379709408})
./recipes/kftt/models/kftt.en-ja.mod:80433:  trainer: !AdamTrainer
./recipes/kftt/config.kftt.en-ja.yaml:58:    trainer: !AdamTrainer
./recipes/kftt/logs/kftt.en-ja.log:68:initialized train.trainer: AdamTrainer@140325776753944({'alpha': 0.001})
./recipes/kftt/logs/kftt.en-ja.log:78:initialized train: SimpleTrainingRegimen@140325776752768({'model': DefaultTranslator@140325776675672, 'src_file': './kftt-data-1.0/data/tok/kyoto-train.cln.en', 'trg_file': './kftt-data-1.0/data/tok/kyoto-train.cln.ja', 'batcher': WordSrcBatcher@140325826891616, 'loss_calculator': MLELoss@140325741185680, 'trainer': AdamTrainer@140325741184448, 'run_for_epochs': 20, 'lr_decay': 0.5, 'lr_decay_times': 2, 'patience': 1, 'initial_patience': 2, 'dev_tasks': [AccuracyEvalTask@140325776753832, LossEvalTask@140325741185008], 'name': 'kftt.en-ja', 'loss_comb_method': 'sum', 'train_loss_tracker': TrainLossTracker@140325741186296, 'dev_loss_tracker': DevLossTracker@140325741186072})
./recipes/stanford-iwslt/config.en-vi.yaml:24:    trainer: !AdamTrainer
./recipes/las-tedlium/config.las-pyramidal.yaml:60:    trainer: !AdamTrainer
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ 
```

optimizers.py ဖိုင်ထဲမှာ ရှိတဲ့ Trainer အကုန်ကို grep command နဲ့ ဆွဲထုတ်ကြည့်ခဲ့တော့ error ပေးနေတဲ့ "TransformerAdamTrainer" ဆိုတာက ရှိပုံမရဘူး ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ grep -n "Trainer" ./build/lib/xnmt/optimizers.py 
28:  A base classe for trainers. Trainers are mostly simple wrappers of the backend trainers but can add extra
67:  A base classe for trainers. Trainers are mostly simple wrappers of DyNet trainers but can add extra functionality.
77:  def __init__(self, optimizer: 'dy.Trainer', skip_noisy: bool = False, rescale_grads: Optional[numbers.Real] = 5.0) \
143:  A base classe for trainers. Trainers are mostly simple wrappers of PyTorch trainers but can add extra functionality.
205:class SimpleSGDTrainerDynet(XnmtOptimizerDynet, Serializable):
218:  yaml_tag = '!SimpleSGDTrainer'
222:    super().__init__(optimizer=dy.SimpleSGDTrainer(ParamManager.global_collection(), e0),
227:class SimpleSGDTrainerTorch(XnmtOptimizerTorch, Serializable):
244:  yaml_tag = '!SimpleSGDTrainer'
264:SimpleSGDTrainer = xnmt.resolve_backend(SimpleSGDTrainerDynet, SimpleSGDTrainerTorch)
267:class MomentumSGDTrainer(XnmtOptimizerDynet, Serializable):
281:  yaml_tag = '!MomentumSGDTrainer'
289:    super().__init__(optimizer=dy.MomentumSGDTrainer(ParamManager.global_collection(), e0, mom),
294:class AdagradTrainer(XnmtOptimizerDynet, Serializable):
308:  yaml_tag = '!AdagradTrainer'
316:    super().__init__(optimizer=dy.AdagradTrainer(ParamManager.global_collection(), e0, eps=eps),
321:class AdadeltaTrainer(XnmtOptimizerDynet, Serializable):
335:  yaml_tag = '!AdadeltaTrainer'
343:    super().__init__(optimizer=dy.AdadeltaTrainer(ParamManager.global_collection(), eps, rho),
348:class AdamTrainerDynet(XnmtOptimizerDynet, Serializable):
364:  yaml_tag = '!AdamTrainer'
374:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(), alpha, beta_1, beta_2, eps),
378:class AdamTrainerTorch(XnmtOptimizerTorch, Serializable):
396:  yaml_tag = '!AdamTrainer'
418:AdamTrainer = xnmt.resolve_backend(AdamTrainerDynet, AdamTrainerTorch)
422:class NoamTrainerDynet(XnmtOptimizerDynet, Serializable):
439:  yaml_tag = '!NoamTrainer'
451:    super().__init__(optimizer=dy.AdamTrainer(ParamManager.global_collection(),
476:class NoamTrainerTorch(XnmtOptimizerTorch, Serializable):
493:  yaml_tag = '!NoamTrainer'
526:NoamTrainer = xnmt.resolve_backend(NoamTrainerDynet, NoamTrainerTorch)
529:class DummyTrainer(XnmtOptimizer, Serializable):
533:  yaml_tag = "!DummyTrainer"
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

အဲဒါကြောင့် optimizer က transformer ဖြစ်ကြောင်း သပ်သပ်ပြောစရာမလိုပဲ ရှိနေတဲ့ Trainer တစ်ခုခုနဲ့ပဲ OK တယ်လို့ ယူဆတယ်။  
ဆက်စပ်ပြီး architecture တွေနဲ့ ပတ်သက်ပြီးလည်း သိချင်လို့ အောက်ပါအတိုင်း ရှာကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ grep -rnw './' -e 'model: ' 
./xnmt/eval/tasks.py:43:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/eval/tasks.py:124:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/eval/tasks.py:173:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/loss_calculators.py:18:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:43:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:69:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:98:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:130:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:163:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:215:                model: 'model_base.ConditionedModel',
./xnmt/train/tasks.py:25:  def __init__(self, model: 'model_base.TrainableModel') -> None:
./xnmt/train/tasks.py:115:               model: 'model_base.ConditionedModel',
./docs/experiment_config_files.rst:22:      model: ...
./docs/experiment_config_files.rst:28:      model: ...
./docs/experiment_config_files.rst:76:  model: !DefaultTranslator
./test/data/tiny_jaen.model:8:  model: !Ref {default: 1928437192847, name: null, path: model}
./test/data/tiny_jaen.model:39:model: !DefaultTranslator
./test/config/cascade.yaml:11:        model: !DefaultTranslator
./test/config/cascade.yaml:39:        model: !DefaultTranslator
./test/config/cascade.yaml:68:      model: !CascadeGenerator
./test/config/speech_retrieval.yaml:6:  model: !DotProductRetriever
./test/config/reinforce.yaml:4:  model: !DefaultTranslator
./test/config/retrieval.yaml:5:  model: !DotProductRetriever
./test/config/score.yaml:2:exp1-model: !Experiment
./test/config/score.yaml:7:  model: !DefaultTranslator
./test/config/load_model.yaml:2:exp1-pretrain-model: !Experiment
./test/config/load_model.yaml:7:  model: !DefaultTranslator
./test/config/load_model.yaml:45:exp2-finetune-model: !LoadSerialized
./test/config/component_sharing.yaml:5:  model: !DefaultTranslator
./test/config/speech.yaml:15:  model: !DefaultTranslator
./test/config/autobatch-fail.yaml:7:    model: !DefaultTranslator
./test/config/simultaneous.yaml:5:  model: !SimultaneousTranslator
./test/config/classifier-torch.yaml:5:  model: !SequenceClassifier
./test/config/cudnn-lstm.yaml:5:  model: !DefaultTranslator
./test/config/multi_task_speech.yaml:16:      model: !DefaultTranslator
./test/config/multi_task_speech.yaml:54:          model: !Ref { name: first_task_model }
./test/config/multi_task_speech.yaml:66:      model: !DefaultTranslator
./test/config/multi_task_speech.yaml:92:          model: !Ref { name: second_task_model }
./test/config/multi_task_speech.yaml:99:      model: !Ref { name: first_task_model }
./test/config/multi_task_speech.yaml:107:exp2-finetune-model: !LoadSerialized
./test/config/multi_task.yaml:17:      model: !DefaultTranslator
./test/config/multi_task.yaml:49:          model: !Ref { name: first_task_model }
./test/config/multi_task.yaml:61:      model: !DefaultTranslator
./test/config/multi_task.yaml:86:          model: !Ref { name: second_task_model }
./test/config/multi_task.yaml:93:      model: !Ref { name: first_task_model }
./test/config/multi_task.yaml:99:exp2-finetune-model: !LoadSerialized
./test/config/lm.yaml:4:  model: !LanguageModel
./test/config/forced.yaml:4:  model: !DefaultTranslator
./test/config/pretrained_embeddings.yaml:5:  model: !DefaultTranslator
./test/config/report.yaml:4:  model: !DefaultTranslator
./test/config/assemble.yaml:5:  model: !DefaultTranslator
./test/config/assemble.yaml:37:  model: !DefaultTranslator
./test/config/assemble.yaml:68:  model: !DefaultTranslator
./test/config/assemble.yaml:102:  model: !DefaultTranslator
./test/config/transformer.yaml:5:  model: !TransformerTranslator
./test/config/encoders.yaml:25:    model: !DefaultTranslator
./test/config/encoders.yaml:37:    model: !DefaultTranslator
./test/config/encoders.yaml:59:    model: !DefaultTranslator
./test/config/encoders.yaml:82:    model: !DefaultTranslator
./test/config/seg_report.yaml:4:  model: !DefaultTranslator
./test/config/self_attentional_am.yaml:15:  model: !DefaultTranslator
./test/config/preproc.yaml:54:  model: !DefaultTranslator
./test/config/minrisk.yaml:5:  model: !DefaultTranslator
./test/config/autobatch.yaml:7:    model: !DefaultTranslator
./test/config/dev_combinator.yaml:5:  model: !DefaultTranslator
./test/config/lattice.yaml:14:  model: !DefaultTranslator
./test/config/random_search_test_params.yaml:5:  model: !DefaultTranslator
./test/config/seq_labeler.yaml:5:  model: !SeqLabeler
./test/config/classifier.yaml:5:  model: !SequenceClassifier
./test/config/seg_learn_debug.yaml:5:  model: !DefaultTranslator
./test/config/reload_exception.yaml:5:  model: !DefaultTranslator
./test/config/ensembling.yaml:6:  model: !DefaultTranslator
./test/config/ensembling.yaml:22:  model: !DefaultTranslator
./test/config/ensembling.yaml:45:  model: !EnsembleTranslator
./test/config/seg_debug.yaml:5:  model: !DefaultTranslator
./test/config/standard.yaml:5:  model: !DefaultTranslator
./test/config/random_search_train_params.yaml:6:  model: !DefaultTranslator
./test/config/reload.yaml:4:  model: !DefaultTranslator
./examples/06_early_stopping.yaml:10:  model: !DefaultTranslator
./examples/07_load_finetune.yaml:4:exp1-pretrain-model: !Experiment
./examples/07_load_finetune.yaml:11:  model: !DefaultTranslator
./examples/07_load_finetune.yaml:52:exp2-finetune-model: !LoadSerialized
./examples/03a_multiple_exp.yaml:20:  model: &my_model !DefaultTranslator
./examples/03a_multiple_exp.yaml:43:  model: *my_model
./examples/01_standard.yaml:14:  model: !DefaultTranslator
./examples/03c_multiple_exp.yaml:7:  model: &my_model !DefaultTranslator
./examples/16_ensembling.yaml:8:  model: &model1 !DefaultTranslator
./examples/16_ensembling.yaml:26:  model: &model2 !DefaultTranslator
./examples/16_ensembling.yaml:47:  model: !EnsembleTranslator
./examples/16_ensembling.yaml:67:  model: !EnsembleTranslator
./examples/14_report.yaml:7:  model: !DefaultTranslator
./examples/02_minimal.yaml:11:  model: !DefaultTranslator
./examples/05_preproc.yaml:78:  model: !DefaultTranslator
./examples/22_switchout.yaml:14:  model: !DefaultTranslator
./examples/21_char_segment.yaml:8:  model: !DefaultTranslator
./examples/21_char_segment.yaml:34:  model: !DefaultTranslator
./examples/21_char_segment.yaml:59:  model: !DefaultTranslator
./examples/21_char_segment.yaml:85:  model: !DefaultTranslator
./examples/21_char_segment.yaml:112:  model: !DefaultTranslator
./examples/15_score.yaml:8:exp1-model: !Experiment
./examples/15_score.yaml:15:  model: !DefaultTranslator
./examples/13_speech.yaml:22:  model: !DefaultTranslator
./examples/08_load_eval_beam.yaml:3:exp1-train-model: !Experiment
./examples/08_load_eval_beam.yaml:12:  model: !DefaultTranslator
./examples/08_load_eval_beam.yaml:58:exp2-eval-model: !LoadSerialized
./examples/04_settings.yaml:12:  model: !DefaultTranslator
./examples/12_multi_task.yaml:23:      model: !DefaultTranslator
./examples/12_multi_task.yaml:55:          model: !Ref { name: first_task_model }
./examples/12_multi_task.yaml:66:      model: !DefaultTranslator
./examples/12_multi_task.yaml:89:          model: !Ref { name: second_task_model }
./examples/12_multi_task.yaml:96:      model: !Ref { name: first_task_model }
./examples/12_multi_task.yaml:102:exp2-finetune-model: !LoadSerialized
./examples/models/standard.mod:10:  model: !Ref
./examples/models/standard.mod:42:model: !DefaultTranslator
./examples/models/standard.mod:411:    model: !Ref
./examples/models/standard.mod:426:  model: !Ref
./examples/20_self_attention.yaml:27:  model: !DefaultTranslator
./examples/19_subword_sample.yaml:10:  model: !DefaultTranslator
./examples/11_component_sharing.yaml:21:  model: !DefaultTranslator
./examples/18_lexiconbias.yaml:8:  model: !DefaultTranslator
./examples/03b_multiple_exp.yaml:8:  model: &my_model !DefaultTranslator
./examples/03b_multiple_exp.yaml:32:  model: *my_model
./examples/23_autobatch.yaml:14:  model: !DefaultTranslator &autobatch_model
./examples/23_autobatch.yaml:36:  model: *autobatch_model
./examples/17_minrisk.yaml:4:exp1-pretrain-model: !Experiment
./examples/17_minrisk.yaml:11:  model: !DefaultTranslator
./build/lib/xnmt/eval/tasks.py:43:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/eval/tasks.py:124:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/eval/tasks.py:173:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/loss_calculators.py:18:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:43:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:69:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:98:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:130:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:163:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:215:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/train/tasks.py:25:  def __init__(self, model: 'model_base.TrainableModel') -> None:
./build/lib/xnmt/train/tasks.py:115:               model: 'model_base.ConditionedModel',
./exp/medical1/word/config.medical.my-en-word.yaml:21:  model: !DefaultTranslator
./exp/medical1/word/config.medical.en-my-word.yaml:21:  model: !DefaultTranslator
./exp/medical1/word/models/medical.en-my.mod:10:  model: !Ref
./exp/medical1/word/models/medical.en-my.mod:28:  model: !Ref
./exp/medical1/word/models/medical.en-my.mod:64:model: !DefaultTranslator
./exp/medical1/word/models/medical.en-my.mod:26667:    model: !Ref
./exp/medical1/word/models/medical.en-my.mod:26688:    model: !Ref
./exp/medical1/word/models/medical.en-my.mod:26707:  model: !Ref
./exp/medical1/word/models/medical.my-en.mod:10:  model: !Ref
./exp/medical1/word/models/medical.my-en.mod:28:  model: !Ref
./exp/medical1/word/models/medical.my-en.mod:64:model: !DefaultTranslator
./exp/medical1/word/models/medical.my-en.mod:26667:    model: !Ref
./exp/medical1/word/models/medical.my-en.mod:26688:    model: !Ref
./exp/medical1/word/models/medical.my-en.mod:26707:  model: !Ref
./exp/medical1/word_tran/transformer-word-en-my.yaml:24:  model: !TransformerTranslator
./exp/medical1/word_tran/transformer-word-my-en.yaml:24:  model: !TransformerTranslator
./exp/medical1/syl/config.medical.my-en-syl.yaml:21:  model: !DefaultTranslator
./exp/medical1/syl/config.medical.en-my-syl.yaml:21:  model: !DefaultTranslator
./exp/medical1/syl/models/medical.syl.my-en.mod:10:  model: !Ref
./exp/medical1/syl/models/medical.syl.my-en.mod:28:  model: !Ref
./exp/medical1/syl/models/medical.syl.my-en.mod:64:model: !DefaultTranslator
./exp/medical1/syl/models/medical.syl.my-en.mod:12100:    model: !Ref
./exp/medical1/syl/models/medical.syl.my-en.mod:12121:    model: !Ref
./exp/medical1/syl/models/medical.syl.my-en.mod:12140:  model: !Ref
./exp/medical1/syl/models/medical.syl.en-my.mod:10:  model: !Ref
./exp/medical1/syl/models/medical.syl.en-my.mod:28:  model: !Ref
./exp/medical1/syl/models/medical.syl.en-my.mod:64:model: !DefaultTranslator
./exp/medical1/syl/models/medical.syl.en-my.mod:12100:    model: !Ref
./exp/medical1/syl/models/medical.syl.en-my.mod:12121:    model: !Ref
./exp/medical1/syl/models/medical.syl.en-my.mod:12140:  model: !Ref
./recipes/kftt/models/kftt.en-ja.mod:10:  model: !Ref
./recipes/kftt/models/kftt.en-ja.mod:28:  model: !Ref
./recipes/kftt/models/kftt.en-ja.mod:64:model: !DefaultTranslator
./recipes/kftt/models/kftt.en-ja.mod:80375:    model: !Ref
./recipes/kftt/models/kftt.en-ja.mod:80396:    model: !Ref
./recipes/kftt/models/kftt.en-ja.mod:80415:  model: !Ref
./recipes/kftt/config.kftt.en-ja.yaml:21:  model: !DefaultTranslator
./recipes/stanford-iwslt/config.en-vi.yaml:6:  model: !DefaultTranslator
./recipes/las-tedlium/config.las-pyramidal.yaml:20:  model: !DefaultTranslator
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ grep -rnw './' -e 'model: ' | grep ".py"
./xnmt/eval/tasks.py:43:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/eval/tasks.py:124:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/eval/tasks.py:173:               model: 'model_base.GeneratorModel' = Ref("model"),
./xnmt/loss_calculators.py:18:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:43:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:69:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:98:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:130:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:163:                model: 'model_base.ConditionedModel',
./xnmt/loss_calculators.py:215:                model: 'model_base.ConditionedModel',
./xnmt/train/tasks.py:25:  def __init__(self, model: 'model_base.TrainableModel') -> None:
./xnmt/train/tasks.py:115:               model: 'model_base.ConditionedModel',
./build/lib/xnmt/eval/tasks.py:43:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/eval/tasks.py:124:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/eval/tasks.py:173:               model: 'model_base.GeneratorModel' = Ref("model"),
./build/lib/xnmt/loss_calculators.py:18:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:43:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:69:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:98:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:130:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:163:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/loss_calculators.py:215:                model: 'model_base.ConditionedModel',
./build/lib/xnmt/train/tasks.py:25:  def __init__(self, model: 'model_base.TrainableModel') -> None:
./build/lib/xnmt/train/tasks.py:115:               model: 'model_base.ConditionedModel',
./recipes/las-tedlium/config.las-pyramidal.yaml:20:  model: !DefaultTranslator
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

tasks.py ဖိုင်ထဲကို ဝင်လေ့လာ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ gedit xnmt/train/tasks.py
```

regimens.py ဖိုင်ထဲမှာ ""TrainingRegimen"" ရှိတဲ့ စာကြောင်းတွေကို line-no နဲ့တကွ ဆွဲထုတ်ကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt/train$ grep -n "TrainingRegimen" ./regimens.py 
16:class TrainingRegimen(object):
47:class SimpleTrainingRegimen(train_tasks.SimpleTrainingTask, TrainingRegimen, Serializable):
83:  yaml_tag = '!SimpleTrainingRegimen'
144:    Main training loop (overwrites TrainingRegimen.run_training())
179:class AutobatchTrainingRegimen(SimpleTrainingRegimen):
181:  This regimen overrides SimpleTrainingRegimen by accumulating (summing) losses
220:  yaml_tag = '!AutobatchTrainingRegimen'
268:      raise ValueError("AutobatchTrainingRegimen forces the batcher to have batch_size 1. Use update_every to set the actual batch size in this regimen.")
277:    Main training loop (overwrites TrainingRegimen.run_training())
321:class MultiTaskTrainingRegimen(TrainingRegimen):
363:class SameBatchMultiTaskTrainingRegimen(MultiTaskTrainingRegimen, Serializable):
384:  yaml_tag = "!SameBatchMultiTaskTrainingRegimen"
450:class AlternatingBatchMultiTaskTrainingRegimen(MultiTaskTrainingRegimen, Serializable):
470:  yaml_tag = "!AlternatingBatchMultiTaskTrainingRegimen"
525:class SerialMultiTaskTrainingRegimen(MultiTaskTrainingRegimen, Serializable):
539:  yaml_tag = "!SerialMultiTaskTrainingRegimen"
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt/train$
```

အဲဲဒါနဲ့ trainer ကို AdamTrainer ပဲ ထားပြီး run ကြည့်ခဲ့...  

```yaml
    trainer: !AdamTrainer
```

ပြီးတော့ training လုပ်ခိုင်းကြည့်ခဲ့တော့ အောက်ပါအတိုင်း error ပေးတယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_tran$ time xnmt --backend torch --gpu ./transformer-word-en-my.yaml 
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-02 18:58:02
=> Running transformer.word.en-my
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 121, in main
    raise e
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 109, in main
    experiment = initialize_if_needed(uninitialized_exp_args)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1467, in initialize_if_needed
    return _YamlDeserializer().initialize_if_needed(root)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1194, in initialize_if_needed
    else: return self.initialize_object(deserialized_yaml_wrapper=obj)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1226, in initialize_object
    self.check_args(self.deserialized_yaml)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1243, in check_args
    _check_backend(node)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 517, in _check_backend
    raise ValueError(f"'{node.__class__.__name__}' is not supported by this backend.")
ValueError: 'TransformerTranslator' is not supported by this backend.

real	0m1.489s
user	0m1.757s
sys	0m0.639s

```

ဒီ backend က pytorch ကို ထားထားတာမို့ run လို့မရဘူးလို့ ပြောတာ...  

```

```

## Reference

- https://github.com/neulab/xnmt/blob/transformer-optimizations/examples/16_transformer.yaml
- https://msperber-xnmt.readthedocs.io/en/latest/_modules/xnmt/optimizer.html
- 
