# SwitchOut Experiment with ASEAN-MT Domain

## Data Preparation

ဒီဒေတာက ဇာဇာလှိုင် (KMITL) နဲ့ အတူလုပ်ခဲ့တဲ့ သူ့ပထမဂျာနယ် experiment အတွက် သုံးခဲ့ဒေတာထဲက (i.e. /home/ye/data/zzh/plan-to-use-for-switchout/1_TH-to-EN_Models_Reports/1_Transformer_Models_Reports/) ကနေ ယူထားတာ။  
ဆိုလိုတာက အဲဒီတုန်းက ခွဲထားခဲ့တဲ့ train, valid, test ပမာဏအတိုင်းပဲ ယူသုံးထားတာ။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc *
   1000    7176   37600 test.en
   1000    7169   99326 test.th
  20000  141098  737287 train.en
  20000  139767 1951027 train.th
   1031    7245   37663 valid.en
   1031    6809   98543 valid.th
  44062  309264 2961446 total

```

လက်ရှိ xnmt အတွက် သုံးထားတဲ့ config ဖိုင်တွေမှာ dev လို့ သုံးခဲ့တာကြောင့် ပြန်ပြင်ရမှာကို ပျင်းလို့၊ ပြင်ရင်းနဲ့ အမှားမဖြစ်အောင်လို့ valid ကိုပဲ dev အဖြစ် နာမည်ပြောင်းသိမ်းခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mv valid.en dev.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mv valid.th dev.th
```

## Confirm data

head command နဲ့ corpus အထဲက ဒေတာတွေကို တချက် မျက်လုံးနဲ့ကြည့်ပြီးတော့ confirm လုပ်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ head {train,dev,test}.en
==> train.en <==
Yes, I like playing Thai chess.
Can you recommend something for kids?
How can I get there?
I ache all over.
Thank you for all you've done for us.
I hope you enjoyed your dinner.
Can we walk to the harbour?
I'm sorry, sir. Your steamed fish isn't ready. If you don't really want it, we can cancel it.
A couple of hot dog.
Please drink the soup directly from the bowl.

==> dev.en <==
You have no diving tower, springboard nor any lanes there.
Can you make change for 50 baht bill?
How can I get to the National Museum?
This place is unique.
Do you have any other rooms available?
I'll have a One Exciting Night.
How much is the best toilet-soap you have?
We look forward to having you with us tonight.
This is my treat.
Hello, I'm the maid.

==> test.en <==
How much is the fare?
I'm looking for something to give as a present.
Is the train held up?
Stand back from the door, please.
A moment, please.
Don't worry.
Could we have a menu, please?
Let me help you with your luggage.
Can I have a first class berth on today's special express to New York?
I have some shirts that need laundering, and I'd like my suit pressed.
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ head {train,dev,test}.th
```

ထိုင်း ဘာသာဘက်အခြမ်းကိုလည်း ကြည့်ခဲ့...  

```
==> train.th <==
ใช่ , ฉัน ชอบ เล่น หมากรุก ไทย 
คุณ มี อะไร แนะนำ สำหรับ เด็ก ไหม ? 
ฉัน สามารถ ไป ที่ นั่น ได้ อย่างไร ? 
ฉัน ปวด เมื่อย ทั่ว ทั้งหมด 
ขอบคุณ สำหรับ ทั้งหมด ที่ คุณ ทำ เพื่อ พวก เรา 
ฉันหวังว่าคุณเพลิดเพลินอาหารเย็นของคุณ
เรา สามารถ เดิน ไป ยัง อ่าว ได้ ไหม ? 
ฉันเสียใจ, ท่าน. ปลานึ่งของคุณไม่พร้อม. ถ้าคุณไม่ต้องการมันจริงๆ, พวกเราสามารถยกเลิกมัน
ฮอทดอกหนึ่งคู่
กรุณาดื่มซุปโดยตรงจากชาม

==> dev.th <==
คุณ ต้อง ไม่ กระโดด หอ หรือ แท่น กระโดด หรือ ลู่ ใด ๆ ที่ นั่น 
คุณ สามารถ ทำ การ แลก เหรียญ สำหรับ ธนบัตร ห้า สิบ บาท ได้ ไหม ? 
ฉัน จะ ไป ที่ พิพิธภัณฑ์ นานา ชาติ ได้ อย่างไร ? 
สถานที่ นี้ มี ความ พิเศษ 
คุณ มี ห้อง อื่น ว่าง ไหม ? 
ฉันจะขอเอ็กไซติ่งไนท์
สบู่ ห้องน้ำ ที่ ดี ที่สุด ที่ คุณ มี ราคา เท่าไหร่ ? 
เราตั้งตามีคุณกับเราคืนนี้
นี้คือคราวของฉัน
สวัสดี . ฉัน เป็น แม่บ้าน . 

==> test.th <==
ค่า โดยสาร ราคา เท่าไหร่ ? 
ฉัน กำลัง มอง หา ของขวัญ อยู่ 
รถไฟ มา แล้ว ใช่ ไหม ? 
กรุณา ยืน ข้าง หลังจาก ประตู 
รอ ซัก ครู่ , กรุณา ด้วย 
ไม่ ต้อง กังวล 
เราขอรายการอาหารได้ไหม?
ให้ ฉัน ช่วย คุณ กับ สัมภาระ ของ คุณ 
ฉัน ขอ ที่นั่ง นอน ขั้น หนึ่ง บน รถไฟ ด่วน พิเศษ ของ วัน นี้ ไป นิวยอร์ก ได้ ไหม ? 
ฉัน มี เสื้อ เชิ้ต ที่ ต้อง ซัก _ และ ฉัน ต้องการ ให้ รีด ชุด สูท 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

## Prepare Config Files (for SwitchOut)

အရင်ဆုံး ရှိပြီးသား config ဖိုင်တွေကို လက်ရှိ experiment အသစ်လုပ်မယ့် folder အောက်ကို ကူးယူခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ cp ../medical1/word_switchout/config.switchout.* .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ ls
config.switchout.en-my-word.yaml  config.switchout.my-en-word.yaml  data
```

ဒီတစ်ခေါက် လုပ်မယ့် NMT language-pair က ထိုင်းနဲ့ အင်္ဂလိပ် ဘာသာနှစ်ခုအကြားမို့လို့ ဖိုင်နာမည်ကို အောက်ပါအတိုင်း ပြောင်းသိမ်းခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ mv config.switchout.en-my-word.yaml config.switchout.en-th-word.yaml 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ mv config.switchout.my-en-word.yaml config.switchout.th-en-word.yaml 

```

## Update config Files (for SwitchOut)

အဓိက ပြင်ဆင်ခဲ့တာကတော့ experiment name နဲ့ "my" နေရာတွေမှာ "th" ကို အစားထိုးခဲ့တာပါ။  
ကျန်တဲ့ hyperparameter နဲ့ network architecture setting တွေကတော့ နှိုင်းယှဉ်လို့ ရအောင် (result comparison လုပ်လို့ ရအောင်အတွက်) ရှေ့က medical domain လုပ်ခဲ့တုန်းကနဲ့ အတူတူပဲ ထားခဲ့တယ်။  

အောက်ပါ config ဖိုင်ကတော့ en-th translation direction အတွက်ပါ။  

```yaml
# standard settings
switchout.asean.en-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.en'
      - '{EXP_DIR}/data/train.th'
      out_files:
      - '{EXP_DIR}/vocab.en'
      - '{EXP_DIR}/vocab.th'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
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
    src_file: '{EXP_DIR}/data/train.en'
    trg_file: '{EXP_DIR}/data/train.th'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.en'
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
      src_file: &test_src '{EXP_DIR}/data/test.en'
      ref_file: &test_trg '{EXP_DIR}/data/test.th'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.th'
```

အောက်ပါ config ဖိုင်ကတော့ th-en translation direction အတွက်ပါ။  

```yaml
# standard settings
switchout.asean.th-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.th'
      - '{EXP_DIR}/data/train.en'
      out_files:
      - '{EXP_DIR}/vocab.th'
      - '{EXP_DIR}/vocab.en'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.th'}
      tau: 0.8      
    trg_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
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
    src_file: '{EXP_DIR}/data/train.th'
    trg_file: '{EXP_DIR}/data/train.en'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.th'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.en'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.th'
      ref_file: &test_trg '{EXP_DIR}/data/test.en'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.en'
```

## Training But Got Error!!!

(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ time xnmt --backend torch --gpu ./config.switchout.en-th-word.yaml | tee asean-en-th-switchout-exp1.log ဆိုတဲ့ command ပေးလိုက်တော့ အောက်ပါအတိုင်း error ပေးတယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ time xnmt --backend torch --gpu ./config.switchout.en-th-word.yaml | tee asean-en-th-switchout-exp1.log
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 20:08:04
=> Running switchout.asean.en-th
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 20656222
> Training
Starting to read ./data/train.en and ./data/train.th
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 121, in main
    raise e
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/xnmt_run_experiments.py", line 115, in main
    eval_scores = experiment(save_fct = lambda: save_to_file(model_file, experiment))
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/experiments.py", line 108, in __call__
    self.train.run_training(save_fct = save_fct)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/train/regimens.py", line 147, in run_training
    for src, trg in self.next_minibatch():
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/train/tasks.py", line 277, in next_minibatch
    self._advance_epoch()
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/train/tasks.py", line 255, in _advance_epoch
    max_src_len=self.max_src_len, max_trg_len=self.max_trg_len)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/input_readers.py", line 697, in read_parallel_corpus
    for src_sent, trg_sent in zip_longest(src_train_iterator, trg_train_iterator):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/input_readers.py", line 89, in iterate_filtered
    yield self.read_sent(line=line, idx=sent_count)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/input_readers.py", line 271, in read_sent
    logits = np.exp(logits - np.max(logits))
  File "<__array_function__ internals>", line 6, in amax
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/numpy/core/fromnumeric.py", line 2706, in amax
    keepdims=keepdims, initial=initial, where=where)
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/numpy/core/fromnumeric.py", line 87, in _wrapreduction
    return ufunc.reduce(obj, axis, dtype, out, **passkwargs)
ValueError: zero-size array to reduction operation maximum which has no identity

real	0m11.494s
user	0m11.187s
sys	0m1.198s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$
```

မသင်္ကာဘူး။ ဒေတာထဲမှာ blank line ရှိနေတယ်လို့ ယူဆခဲ့...  
အဲဒါကြောင့် blank line ရှိမရှိကို check လုပ်ဖို့အတွက် ငါ့ရဲ့ GitHub အောက်က tool ဆိုတဲ့ repository အောက်က perl script ပရိုဂရမ် တစ်ပုဒ်ကို လက်ရှိ ဒေတာ path ထဲကို download လုပ်ယူခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/print-blank-lines.pl
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-03 20:15:42--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/print-blank-lines.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.108.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 595 [text/plain]
Saving to: ‘print-blank-lines.pl’

print-blank-lines.pl            100%[=====================================================>]     595  --.-KB/s    in 0s      

2022-05-03 20:15:42 (24.2 MB/s) - ‘print-blank-lines.pl’ saved [595/595]

(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

ပြီးတော့ blank line ရှိမရှိကို စစ်ဆေးကြည့်တော့ အောက်ပါအတိုင်း ထိုင်းဘာသာစကားအတွက် trainining ဖိုင်မှာ blank line ရှိနေတာကို တွေ့ခဲ့ရ။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./train.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./train.th
4616	
6863	
8076	
10007	
13347	
19555	
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./dev.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./dev.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./test.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ perl ./print-blank-lines.pl ./test.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

train.th ထဲက blank ဖြစ်နေတဲ့ နေရာတွေက အောက်ပါအတိုင်း ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 4615,4617p train.th
ร้าน ขาย ของ ที่ ระลึก อยู่ ที่ไหน 

มี สถานที่ ทาง ประวัติศาสตร์ เยอะ ไหม ใน บ้าน เกิด ของ คุณ ? 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6862,6864p train.th
มี จุด ที่ น่า สนใจ ไหม ระหว่าง การ เดินทาง ไป เอฟ ? 

ค่า โดยสาร เท่าไหร่ ? 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 8075,8077p train.th
ฉัน มา เช็คอิน ที่ นี่ สำหรับ เที่ยวบิน ไป แอลเอ 

ฉัน ควร โทร เรียก รถ พยาบาล ไหม ? 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 10006,10008p train.th
ฉัน จะ ส่ง คน ไป ที่ ห้อง คุณ ทันที . 

ให้ ฉัน ดู ก่อน ว่า จะ ช่วย คุณ อย่างไร 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 13346,13348p train.th
ฉัน ต้องการ ไป ตาม ที่ อยู่ ที่ นี่ 

ฉันต้องจ่ายทั้งหมดเท่าไร
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 19554,19556p train.th
มี สถานที่ ที่ น่า สนใจ มากมาย ระหว่าง ทาง ไป ดี , เช่น อี , เอฟ 

มัน ง่าย กว่า ที่ ทาง ข้าม 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

## Cleaning the Corpus

အထက်ပါအတိုင်း ထိုင်းဘက်အခြမ်းမှာ blank line တွေ ပါနေတာကြောင့် corpus ကို cleaning လုပ်ဖို့ လိုအပ်တယ်။  
တစ်ခု သတိထားကြရမှာက ထိုင်းဘက်အခြမ်းတစ်ခုထဲကို clean လုပ်လို့ မရဘူး။ English ဒေတာနဲ့ parallel လုပ်ထားတာမို့လို့ တဖက်တည်းဖျက်လိုက်ရင် parallel မဖြစ်တော့ပဲအကုန်လွဲကုန်လိမ့်မယ်။ ပြီးတော့ no. of sentence လည်း တူတော့မှာ မဟုတ်ပါဘူး။ အဲဒါကြောင့် အရင်ဆုံး paste command နဲ့ en-th ကို parallel အဖြစ် တွဲလိုက်ပြီးမှသာ command နဲ့ ဖြစ်ဖြစ် သို့မဟုတ် text editor တစ်ခုခုကို သုံးပြီးတော့ manual ဝင်ဖျက်တာ ဖြစ်ဖြစ် လုပ်ပေးရလိမ့်မယ်။  

in case တစ်ခုခု ဖြစ်နိုင်လို့ မဖျက်ခင်မှာ လက်ရှိ data ကို backup ကူးထားခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mkdir bk
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ cp train.* ./bk
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc ./bk/*
  20000  141098  737287 ./bk/train.en
  20000  139767 1951027 ./bk/train.th
  40000  280865 2688314 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

en-th အဖြစ် parallel ပြန်တွဲခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ paste ./train.en ./train.th > train.enth
```

လက်ရှိ en, th ဖိုင်နှစ်ဖိုင်ကို delete လုပ်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ rm train.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ rm train.th
```

ပြီးတော့ paste command နဲ့ တွဲထားတဲ့ ဖိုင်ရဲ့ size ကိုလည်း confirm လုပ်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc ./train.enth
  20000  280865 2688314 ./train.enth
```

content ကိုလည်း တချက် မျက်လုံးနဲ့ confirmation လုပ်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ head train.enth
Yes, I like playing Thai chess.	ใช่ , ฉัน ชอบ เล่น หมากรุก ไทย 
Can you recommend something for kids?	คุณ มี อะไร แนะนำ สำหรับ เด็ก ไหม ? 
How can I get there?	ฉัน สามารถ ไป ที่ นั่น ได้ อย่างไร ? 
I ache all over.	ฉัน ปวด เมื่อย ทั่ว ทั้งหมด 
Thank you for all you've done for us.	ขอบคุณ สำหรับ ทั้งหมด ที่ คุณ ทำ เพื่อ พวก เรา 
I hope you enjoyed your dinner.	ฉันหวังว่าคุณเพลิดเพลินอาหารเย็นของคุณ
Can we walk to the harbour?	เรา สามารถ เดิน ไป ยัง อ่าว ได้ ไหม ? 
I'm sorry, sir. Your steamed fish isn't ready. If you don't really want it, we can cancel it.	ฉันเสียใจ, ท่าน. ปลานึ่งของคุณไม่พร้อม. ถ้าคุณไม่ต้องการมันจริงๆ, พวกเราสามารถยกเลิกมัน
A couple of hot dog.	ฮอทดอกหนึ่งคู่
Please drink the soup directly from the bowl.	กรุณาดื่มซุปโดยตรงจากชาม
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

ဖျက်ချင်တဲ့ blank ဖြစ်နေတဲ့ လိုင်းတွေကို လိုင်းနံပါတ် တစ်ခုချင်းစီပေးပြီးတော့ sed command နဲ့ ဖျက်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -i '4616d;6863d;8076d;10007d;13347d;19555d;' ./train.enth 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc ./train.enth 
  19994  280842 2688196 ./train.enth
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

confirmation တစ်ချက် လုပ်ခဲ့...  

မဖျက်ခင်က အနေအထားက အောက်ပါအတိုင်း...  
```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6862,6864p ./bk/train.th
มี จุด ที่ น่า สนใจ ไหม ระหว่าง การ เดินทาง ไป เอฟ ? 

ค่า โดยสาร เท่าไหร่ ? 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6862,6864p ./bk/train.en
Are there some scenic spots on the way to F?
We serve green tea.
How much is the fare?
```

ဖျက်ပြီးသွားတဲ့ အခါမှာ ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6862,6864p ./train.enth
How much is the fare?	ค่า โดยสาร เท่าไหร่ ? 
But the fried fish meuniere is very good.	แต่ปลาทอดมูเนียร์ดีมาก
Can I have something for a cough?	ฉัน ขอ ยา แก้ ไอ หน่อย ได้ ไหม ? 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

မဖျက်ခင်က အနေအထား  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6860,6865p ./bk/train.th 
คุณ สามารถ บอก ฉัน เกี่ยว กับ ดิสนี่ย์แลนด์ บาง อย่าง ได้ ไหม ? 
มัน ไม่ มี คน มา เลย 
มี จุด ที่ น่า สนใจ ไหม ระหว่าง การ เดินทาง ไป เอฟ ? 

ค่า โดยสาร เท่าไหร่ ? 
แต่ปลาทอดมูเนียร์ดีมาก
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6860,6865p ./bk/train.en
Can you tell me something about Disneyland?
It's dead in here.
Are there some scenic spots on the way to F?
We serve green tea.
How much is the fare?
But the fried fish meuniere is very good.
```

ဖျက်ပြီးသွားတဲ့ အခါမှာ  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ sed -n 6860,6865p ./train.enth 
It's dead in here.	มัน ไม่ มี คน มา เลย 
Are there some scenic spots on the way to F?	มี จุด ที่ น่า สนใจ ไหม ระหว่าง การ เดินทาง ไป เอฟ ? 
How much is the fare?	ค่า โดยสาร เท่าไหร่ ? 
But the fried fish meuniere is very good.	แต่ปลาทอดมูเนียร์ดีมาก
Can I have something for a cough?	ฉัน ขอ ยา แก้ ไอ หน่อย ได้ ไหม ? 
Which would you prefer?	สิ่งไหนที่คุณต้องการ?
```

နောက်ဆုံးပိုင်းက parallel ဖြစ်မဖြစ်ကိုလည်း သေချာအောင် print ထုတ်ကြည့်တာ၊ Google Translate နဲ့ ထိုင်းဘက်အခြမ်းကို ဘာသာပြန်ခိုင်းပြီး အင်္ဂလိပ်စာဘက်အခြမ်းနဲ့ ခန့်မှန်းခြေ တူရဲ့လား ဆိုတာကိုလည်း confirm လုပ်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ tail -n 3 ./train.enth 
How many hours does it take to complete that tour?	ทัวร์ ใช้ เวลา ทั้งหมด เท่าไร ? 
I don't want to watch a tragedy until we have finished the journey.	ฉัน ไม่ ต้องการ ดู เรื่อง เศร้า จนกว่า เรา จะ ท่องเที่ยว เสร็จ 
Passengers who have got the ticket for Express Number K please get on the train at once.	ผู้ โดยสาร ที่ มี ตั๋ว สำหรับ รถไฟ ด่วนหมายเลข เค กรุณา ขึ้น รถไฟ ตอน นี้ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ 
```

Google Translate output က အောက်ပါအတိုင်း...  

```
ทัวร์นี้ใช้เวลากี่ชั่วโมงจึงจะเสร็จสิ้น
ฉันไม่ต้องการดูโศกนาฏกรรมจนกว่าเราจะเสร็จสิ้นการเดินทาง
ผู้โดยสารที่ได้รับตั๋ว Express Number K โปรดขึ้นรถไฟทันที
```

Google Translate ကိုပဲ သုံးပြီး အထက်က ထိုင်းစာကြောင်းတွေကို အင်္ဂလိပ်လို ပြန်ခိုင်းကြည့်ခဲ့...  

```
How many hours does this tour take to complete?
I don't want to see a tragedy until we finish the journey.
Passengers receiving Express Number K tickets, please board the train immediately.
```

blank line ဖြစ်နေတာတွေကို ဖျက်တဲ့နေရာမှာ အမှားအယွင်း မလုပ်ခဲ့ဘူးလို့ ယုံကြည်။  
NMT လုပ်ဖို့အတွက် တစ်ဖိုင်စီ ပြန်ခွဲထုတ်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ cut -f1 ./train.enth > ./train.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ cut -f2 ./train.enth > ./train.th
```

cleaning လုပ်ထားတဲ့ parallel ဖိုင်ကိုလည်း backup လုပ်ထားခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mv train.enth ./bk/train.enth.clean
```

cleaning လုပ်ပြီးတဲ့အချိန်မှာ training data ရဲ့ size က အောက်ပါအတိုင်း ဖြစ်လိမ့်မယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc train.{en,th}
  19994  141075  737175 train.en
  19994  139767 1951021 train.th
  39988  280842 2688196 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc {train,dev,test}.en
 19994 141075 737175 train.en
  1031   7245  37663 dev.en
  1000   7176  37600 test.en
 22025 155496 812438 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc {train,dev,test}.th
  19994  139767 1951021 train.th
   1031    6809   98543 dev.th
   1000    7169   99326 test.th
  22025  153745 2148890 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$
```

## Baseline Config Files

baseline ကို အရင် run သင့်တာမို့ baseline config ဖိုင် နှစ်ဖိုင်ကို အောက်ပါအတိုင်း ပြင်ဆင်ပြီးတော့ run ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ cp ../medical1/word/config.medical.
config.medical.en-my-word.yaml  config.medical.my-en-word.yaml  
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ cp ../medical1/word/config.medical.* .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ ls
asean-en-th-switchout-exp1.log  config.medical.my-en-word.yaml    config.switchout.th-en-word.yaml  logs      vocab.en
config.medical.en-my-word.yaml  config.switchout.en-th-word.yaml  data                              train.en  vocab.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ mv config.medical.en-my-word.yaml config.baseline.en-my-word.yaml 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ mv config.medical.my-en-word.yaml ./config.baseline.my-en-word.yaml 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt$ 
```

baseline ရဲ့ vocab တွေနဲ့ switchout experiment ရဲ့ vocab တွေကို သပ်သပ်စီ ခွဲထားချင်လို့... experiment folder အသစ်တစ်ခု ထပ်ဆောက်ပြီးတော့ config ဖိုင်တွေကိုလည်း အဲဒီအောက်ကို ရွှေ့ထားခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ mkdir asean-mt-baseline
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ mv ./asean-mt/config.baseline.* ./asean-mt-baseline/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ cp ./asean-mt/data/ ./asean-mt-baseline/ -r
```

မြင်သာအောင်လို့ tree structure အနေနဲ့ log မှတ်ထားခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ tree ./asean-mt-baseline/
./asean-mt-baseline/
├── config.baseline.en-th-word.yaml
├── config.baseline.th-en-word.yaml
└── data
    ├── bk
    │   ├── train.en
    │   ├── train.enth.clean
    │   └── train.th
    ├── dev.en
    ├── dev.th
    ├── print-blank-lines.pl
    ├── test.en
    ├── test.th
    ├── tmp
    │   └── test.txt
    ├── train.en
    └── train.th

3 directories, 13 files
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$
```

switchout experiment အတွက်က အောက်ပါအတိုင်း...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ tree ./asean-mt-switchout/
./asean-mt-switchout/
├── asean-en-th-switchout-exp1.log
├── config.switchout.en-th-word.yaml
├── config.switchout.th-en-word.yaml
├── data
│   ├── bk
│   │   ├── train.en
│   │   ├── train.enth.clean
│   │   └── train.th
│   ├── dev.en
│   ├── dev.th
│   ├── print-blank-lines.pl
│   ├── test.en
│   ├── test.th
│   ├── tmp
│   │   └── test.txt
│   ├── train.en
│   └── train.th
├── logs
│   ├── switchout.asean.en-th.log
│   └── switchout.asean.en-th.log.yaml
├── train.en
├── vocab.en
└── vocab.th

4 directories, 19 files
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$
```

manually edit ဝင်လုပ်ခဲ့တယ်။ 


for en-th **baseline** translation direction:  

```yaml
# standard settings
asean.baseline.en-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.en'
      - '{EXP_DIR}/data/train.th'
      out_files:
      - '{EXP_DIR}/vocab.en'
      - '{EXP_DIR}/vocab.th'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
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
    src_file: '{EXP_DIR}/data/train.en'
    trg_file: '{EXP_DIR}/data/train.th'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.en'
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
      src_file: &test_src '{EXP_DIR}/data/test.en'
      ref_file: &test_trg '{EXP_DIR}/data/test.th'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.th'
```

for th-en **baseline** translation direction:  

```yaml
# standard settings
asean.baseline.th-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.th'
      - '{EXP_DIR}/data/train.en'
      out_files:
      - '{EXP_DIR}/vocab.th'
      - '{EXP_DIR}/vocab.en'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.th'}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
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
    trg_file: '{EXP_DIR}/data/train.en'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.th'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.en'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.th'
      ref_file: &test_trg '{EXP_DIR}/data/test.en'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.en'
```

## Training for en-th, word unit (Baseline)

```

```

## Training for th-en, word unit (Baseline)

```

```

## Training for en-th, word unit (SwitchOut)

```

```

## Training for th-en, word unit (SwitchOut)

```

```

## Reference

- [https://stackoverflow.com/questions/22903114/overcome-valueerror-for-empty-array](https://stackoverflow.com/questions/22903114/overcome-valueerror-for-empty-array)
- [https://unix.stackexchange.com/questions/612680/remove-lines-with-specific-line-number-specified-in-a-file](https://unix.stackexchange.com/questions/612680/remove-lines-with-specific-line-number-specified-in-a-file)


