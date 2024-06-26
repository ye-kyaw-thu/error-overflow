# Ensembling Exp with XNMT

## 1st Test Run with Example Config

ပထမဆုံး ensembling config example ဖိုင်ကို နားလည်အောင် ဖတ်ကြည့်ခဲ့...  

### Study on config

```yaml
(base) ye@ye-System-Product-Name:~/tool/xnmt/examples$ cat ./16_ensembling.yaml 
# This example shows different ways to perform model ensembling

# First, let's a define a simple experiment with a single model
exp1-single: !ExperimentERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
  exp_global: &globals !ExpGlobal
    default_layer_dim: 32
  # Just use default model settings here
  model: &model1 !DefaultTranslator
    src_reader: &src_reader !PlainTextReader
      vocab: !Vocab {vocab_file: examples/data/head.ja.vocab}
    trg_reader: &trg_reader !PlainTextReader
      vocab: !Vocab {vocab_file: examples/data/head.en.vocab}
  train: &train !SimpleTrainingRegimenvocab ဖိုင်ကို manual စမ်းဆောက်
    run_for_epochs: 2
    src_file: examples/data/head.ja
    trg_file: examples/data/head.en
    dev_tasks:
      - !LossEvalTask
        src_file: examples/data/head.ja
        ref_file: examples/data/head.en

# Another single model, but with a different number of layers and some other
# different settings
exp2-single: !Experiment
  exp_global: *globals
  model: &model2 !DefaultTranslator
    src_reader: *src_reader
    trg_reader: *trg_reader
    encoder: !BiLSTMSeqTransducer
      layers: 3
      hidden_dim: 64
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder
        _xnmt_id: dense_embed
        emb_dim: 64
      rnn: !UniLSTMSeqTransducer
        hidden_dim: 64
      transform: !AuxNonLinear
        output_dim: 64
      scorer: !Softmax
        output_projector: !Ref {name: dense_embed}
  train: *train

# Load the previously trained models and combine them to an ensemble
exp3-ensemble-load: !Experiment
  exp_global: *globals
  model: !EnsembleTranslator
    src_reader: !Ref {path: model.models.0.src_reader}
    trg_reader: !Ref {path: model.models.0.trg_reader}
    models:
      - !LoadSerialized
        filename: 'examples/output/exp1-single.mod'
        path: model
      - !LoadSerialized
        filename: 'examples/output/exp2-single.mod'
        path: model
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,wer
      src_file: examples/data/head.ja
      ref_file: examples/data/head.en
      hyp_file: examples/output/{EXP}.test_hyp

# Alternatively, we can also hook up the models during training time already
exp4-ensemble-train: !Experiment
  exp_global: *globals
  model: !EnsembleTranslator
    src_reader: *src_reader
    trg_reader: *trg_reader
    models:
      - *model1
      - *model2vocab ဖိုင်ကို manual စမ်းဆောက်
  train: *train
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,wer
      src_file: examples/data/head.ja
      ref_file: examples/data/head.en
      hyp_file: examples/output/{EXP}.test_hyp
(base) ye@ye-System-Product-Name:~/tool/xnmt/examples$ 
```

အထက်ပါ config ဖိုင်နဲ့ run ကြည့်တော့အောက်ပါအတိုင်း vocab ဖိုင်က မရှိလို့ error ပေးတယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples$ time xnmt --backend torch --gpu ./16_ensembling.yaml | tee ensemble-tst-train.log
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 11:56:17
=> Running exp1-single
ERROR: ------ Error Report ------
ERROR: *** yaml_path ***
ERROR: model.src_reader.vocab
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
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1237, in initialize_object
    initialized = self.init_components_bottom_up(self.deserialized_yaml)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1337, in init_components_bottom_up
    initialized_component = self.init_component(path)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 1373, in init_component
    initialized_obj = obj.__class__(**init_params)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 92, in wrapper
    f(obj, **serialize_params)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/vocabs.py", line 39, in __init__
    i2w = Vocab.i2w_from_vocab_file(vocab_file, sentencepiece_vocab)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/vocabs.py", line 62, in i2w_from_vocab_file
    with open(vocab_file, encoding='utf-8') as f:
FileNotFoundError: [Errno 2] No such file or directory: 'examples/data/head.ja.vocab'

real	0m1.583s
user	0m1.842s
sys	0m0.650s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples$
```

တကယ်ကတော့ examples ဖိုလ်ဒါအောက်ထဲ ဝင်ပြီးမှ run လို့ ပေးတဲ့ error လို့ ယူဆပါတယ်။ ဘာကြောင့်လဲ ဆိုတော့ examples/data/ အောက်မှာက vocab ဖိုင်တွေက ရှိနေလို့ပါ။ အောက်ပါအတိုင်းပါ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ wc ./head.en.vocab 
 66  66 360 ./head.en.vocab
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ wc ./head.ja.vocab 
 70  70 409 ./head.ja.vocab
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ head ./head.en.vocab 
.
you
?
a
do
the
in
it
to
with
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ head ./head.ja.vocab 
。
い
で
を
が
は
た
な
し
す
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$
```

### How to Build Vocab Manually? 

အထက်ပါ error ကနေ လိုအပ်တဲ့အခါ သုံးလို့ ရဖို့အတွက် xnmt က support လုပ်ထားတဲ့ vocab ဆောက်ပေးတဲ့ python script တွေကိုလည်း လေ့လာခဲ့တယ်။  
vocab ဖိုင်ကို manual စမ်းဆောက်ဖို့အတွက်က ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples$ python ../script/vocab/make_vocab.py --help
usage: make_vocab.py [-h] [--min_count MIN_COUNT]

optional arguments:
  -h, --help            show this help message and exit
  --min_count MIN_COUNT
```

minimum count အတွက် default က ဘယ်လောက် ထားထားသလဲ ဆိုတာကို သိချင်လို့ source code ကို ဝင်ကြည့်ခဲ့...  

```python
#!/usr/bin/env python3

"""
Simple script to generate vocabulary that can be used in most of the xnmt.input_readers

--min_count Is a filter based on count of words that need to be at least min_count to appear in the vocab.

"""


import sys
import argparse
from collections import Counter

parser = argparse.ArgumentParser()
parser.add_argument("--min_count", type=int, default=1)
```

default တန်ဖိုးက စာလုံး တစ်လုံး တွေ့တာနဲ့ ယူမယ်ဆိုတဲ့ setting ဆိုတာကို သိခဲ့ရတယ်။  
ပြီးတော့ character ngram vocab ဆောက်ဖို့အတွက် script လည်း ရှိတယ်။  
link ကနေ ဆိုရင်တော့ [https://github.com/neulab/xnmt/blob/master/script/vocab/make_charngram_vocab.py](https://github.com/neulab/xnmt/blob/master/script/vocab/make_charngram_vocab.py)  


```python
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples$ cat ../script/vocab/make_charngram_vocab.py 
#!/usr/bin/env python3

"""
By: Philip Arthur

Script to generate CHARAGRAM vocabulary.
For example if we have 2 words corpus: ["ab", "deac"]
Then it wil produce the char n gram vocabulary.

a
b
c
d
e
ab
de
ea
ac
dea
eac
deac

This is useful to be used in CharNGramSegmentComposer.

Args:
  ngram - The size of the ngram.
  top - Prin only the top ngram.
"""



import sys
import argparse
from collections import Counter

parser = argparse.ArgumentParser()
parser.add_argument("ngram", type=int, default=4)
parser.add_argument("--top", type=int, default=-1)
args = parser.parse_args()

k = args.ngram
counts = Counter()
for line in sys.stdin:
  words = line.strip().split()
  for word in words:
    for i in range(len(word)):
      for j in range(i+1, min(i+k+1, len(word)+1)):
        counts[word[i:j]] += 1

for i, (key, count) in enumerate(sorted(counts.items(), key=lambda x: -x[1])):
  if args.top != -1:
    if i == args.top:
      break
  print(key)


(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples$
```

[https://xnmt.readthedocs.io/en/latest/experiment_config_files.html#](https://xnmt.readthedocs.io/en/latest/experiment_config_files.html#) မှာ ရှင်းပြထားတဲ့ Char Segment အပိုင်းက script ကို ကြည့်ပြီး နားလည်တာက အောက်ပါလိုမျိုး ရေးထားတာက နည်းနည်းလွဲနေသလားလို့...  

```yaml
# Examples of using SegmentingSeqTransducer
# Look available composition functions at xnmt/specialized_encoders/segmenting_encoder/segmenting_composer.py

# Looking up characters from word vocabulary
# Basically this is the same as 01_standard.yaml
seg_lookup: !Experiment
  exp_global: !ExpGlobal {}
  model: !DefaultTranslator
    src_reader: !CharFromWordTextReader
      # Can be produced by script/vocab/make_vocab.py --char_vocab < [CORPUS]
      vocab: !Vocab {vocab_file: examples/data/head.ja.charvocab}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: examples/data/head.en.vocab}
    # It reads in characters and produce word embeddings
    encoder: !SegmentingSeqTransducer
      segment_composer: !LookupComposer
        word_vocab: !Vocab {vocab_file: examples/data/head.ja.vocab}
      final_transducer: !BiLSTMSeqTransducer {}
```

Note: ```--char_vocab``` option ကို make_vocab.py ပရိုဂရမ်မှာ မတွေ့လို့။ အဲဒါကြောင့် char level vocab ဆောက်မယ်ဆိုရင် make_charngram_vocab.py ပရိုဂရမ်ကိုပဲ သုံးရလိမ့်မယ်။  

### Build Vocab Manually

vocab ဖိုင်ကို manual စမ်းဆောက်ကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ python ../../script/vocab/make_vocab.py < ./head.en > head.en.vocab
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ python ../../script/vocab/make_vocab.py < ./head.ja > head.ja.vocab
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ wc ./head.en.vocab 
 66  66 360 ./head.en.vocab
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/examples/data$ wc ./head.ja.vocab 
 70  70 409 ./head.ja.vocab
```

### Training Again

ဒီတစ်ခါတော့ example ဖိုလ်ဒါရဲ့ အထက်ကို တက်လိုက်ပြီး ensembling exp ကို စမ်း run ကြည့်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ time xnmt --backend torch --gpu ./examples/16_ensembling.yaml | tee ensemble-tst-train.log
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 12:32:03
=> Running exp1-single
WARNING: log file(s) ./examples/logs/exp1-single.log already exists, skipping experiment; please delete log file by hand if you want to overwrite it (or activate OVERWRITE_LOG, by either specifying an environment variable OVERWRITE_LOG=1, or specifying --settings=debug, or changing xnmt.settings.Standard.OVERWRITE_LOG manually)
=> Running exp2-single
> use randomly initialized neural network parameters for all components
  neural network param count: 135973
> Training
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
[exp2-single] Epoch 1.0000: train_loss/word=4.698348 (steps=1, words/sec=204.73, time=0-00:00:00)
> Checkpoint [exp2-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp2-single] Epoch 1.0000 dev Loss: 4.585 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
[exp2-single] Epoch 2.0000: train_loss/word=4.587391 (steps=2, words/sec=1270.49, time=0-00:00:00)
> Checkpoint [exp2-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp2-single] Epoch 2.0000 dev Loss: 4.467 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
reverting learned weights to best checkpoint..
Experiment                    | Final Scores
-----------------------------------------------------------------------
exp2-single                   | Not evaluated
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 996, in _load_serialized
    with open(node.filename) as stream:
FileNotFoundError: [Errno 2] No such file or directory: 'examples/output/exp1-single.mod'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 80, in main
    resume=args.resume)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 937, in preload_experiment_from_file
    resume=resume)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 971, in preload_obj
    root = YamlPreloader._load_serialized(root)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 999, in _load_serialized
    raise RuntimeError(f"Could not read configuration file {node.filename}: {e}")
RuntimeError: Could not read configuration file examples/output/exp1-single.mod: [Errno 2] No such file or directory: 'examples/output/exp1-single.mod'

real	0m4.560s
user	0m4.089s
sys	0m1.353s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

အထက်ပါ အတိုင်း error ပေးနေတယ်။  
log ဖိုင်တွေက ရှိနေတဲ့အတွက် ပေးတဲ့ error လားလို့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ ls ./examples/logs/*
./examples/logs/exp1-single.log       ./examples/logs/exp2-single.log       ./examples/logs/standard.log
./examples/logs/exp1-single.log.yaml  ./examples/logs/exp2-single.log.yaml  ./examples/logs/standard.log.yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ rm ./examples/logs/exp1*.log
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ rm ./examples/logs/exp2*.log
```

နောက်တစ်ခါ ထပ် run ခဲ့ ....  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ time xnmt --backend torch --gpu ./examples/16_ensembling.yaml | tee ensemble-tst-train.log
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 12:37:02
=> Running exp1-single
> use randomly initialized neural network parameters for all components
  neural network param count: 29957
> Training
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
[exp1-single] Epoch 1.0000: train_loss/word=4.693406 (steps=1, words/sec=216.76, time=0-00:00:00)
> Checkpoint [exp1-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp1-single] Epoch 1.0000 dev Loss: 4.598 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
[exp1-single] Epoch 2.0000: train_loss/word=4.600169 (steps=2, words/sec=2667.67, time=0-00:00:00)
> Checkpoint [exp1-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp1-single] Epoch 2.0000 dev Loss: 4.497 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
reverting learned weights to best checkpoint..
Experiment                    | Final Scores
-----------------------------------------------------------------------
exp1-single                   | Not evaluated
=> Running exp2-single
> use randomly initialized neural network parameters for all components
  neural network param count: 135973
> Training
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp2-single] Epoch 1.0000: train_loss/word=4.699435 (steps=1, words/sec=1286.58, time=0-00:00:00)
> Checkpoint [exp2-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp2-single] Epoch 1.0000 dev Loss: 4.597 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
[exp2-single] Epoch 2.0000: train_loss/word=4.597915 (steps=2, words/sec=1288.45, time=0-00:00:00)
> Checkpoint [exp2-single]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[exp2-single] Epoch 2.0000 dev Loss: 4.493 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
reverting learned weights to best checkpoint..
Experiment                    | Final Scores
-----------------------------------------------------------------------
exp1-single                   | Not evaluated
exp2-single                   | Not evaluated
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 996, in _load_serialized
    with open(node.filename) as stream:
FileNotFoundError: [Errno 2] No such file or directory: 'examples/output/exp1-single.mod'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 80, in main
    resume=args.resume)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 937, in preload_experiment_from_file
    resume=resume)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 971, in preload_obj
    root = YamlPreloader._load_serialized(root)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/persistence.py", line 999, in _load_serialized
    raise RuntimeError(f"Could not read configuration file {node.filename}: {e}")
RuntimeError: Could not read configuration file examples/output/exp1-single.mod: [Errno 2] No such file or directory: 'examples/output/exp1-single.mod'

real	0m5.091s
user	0m4.674s
sys	0m1.306s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ 
```

အဓိက ပေးနေတဲ့ ERROR က အောက်ပါအတိုင်းလို့ ယူဆ...  

```
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
```

Note: အချိန်ထပ်ရမှ လေ့လာမယ်။ segmentation unit မတူရင် vocab ဖိုင်တွေကိုလည်း ရှဲလုပ်တာ သို့မဟုတ် ပေါင်းဆောက်တာလည်း လုပ်ရမှာမို့ marian ကိုပဲ သုံးပြီး exp လုပ်ဖို့ ဆုံးဖြတ်ခဲ့ ...  


