# Ensembling Exp with XNMT

## 1st Test Run with Example Config

ပထမဆုံး ensembling config example ဖိုင်ကို နားလည်အောင် ဖတ်ကြည့်ခဲ့...  

### Study on config

```yaml
(base) ye@ye-System-Product-Name:~/tool/xnmt/examples$ cat ./16_ensembling.yaml 
# This example shows different ways to perform model ensembling

# First, let's a define a simple experiment with a single model
exp1-single: !Experiment
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

### How to Build Vocab Manually? 

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

```
