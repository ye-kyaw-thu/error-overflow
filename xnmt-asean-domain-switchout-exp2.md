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
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline$ time xnmt --backend torch --gpu ./config.baseline.en-th-word.yaml | tee baseline.en-th.log1
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 21:22:40
=> Running asean.baseline.en-th
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 20655710
> Training
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 0.0509: train_loss/word=8.596564 (steps=23, words/sec=5060.50, time=0-00:00:04)
[asean.baseline.en-th] Epoch 0.1021: train_loss/word=7.260851 (steps=49, words/sec=7195.74, time=0-00:00:05)
[asean.baseline.en-th] Epoch 0.1544: train_loss/word=7.077968 (steps=73, words/sec=7739.35, time=0-00:00:06)
[asean.baseline.en-th] Epoch 0.2063: train_loss/word=6.990507 (steps=94, words/sec=8988.29, time=0-00:00:07)
[asean.baseline.en-th] Epoch 0.2574: train_loss/word=7.009603 (steps=117, words/sec=7810.50, time=0-00:00:08)
[asean.baseline.en-th] Epoch 0.3081: train_loss/word=6.738230 (steps=139, words/sec=8374.17, time=0-00:00:09)
[asean.baseline.en-th] Epoch 0.3597: train_loss/word=6.774648 (steps=163, words/sec=7785.12, time=0-00:00:10)
[asean.baseline.en-th] Epoch 0.4107: train_loss/word=6.605139 (steps=184, words/sec=8566.15, time=0-00:00:11)
[asean.baseline.en-th] Epoch 0.4612: train_loss/word=6.515629 (steps=206, words/sec=8548.72, time=0-00:00:12)
[asean.baseline.en-th] Epoch 0.5120: train_loss/word=6.563339 (steps=227, words/sec=8016.82, time=0-00:00:13)
[asean.baseline.en-th] Epoch 0.5640: train_loss/word=6.379323 (steps=254, words/sec=7056.55, time=0-00:00:14)
[asean.baseline.en-th] Epoch 0.6143: train_loss/word=6.308015 (steps=276, words/sec=8343.73, time=0-00:00:15)
[asean.baseline.en-th] Epoch 0.6674: train_loss/word=6.191286 (steps=296, words/sec=9031.58, time=0-00:00:16)
[asean.baseline.en-th] Epoch 0.7194: train_loss/word=6.209881 (steps=317, words/sec=8208.57, time=0-00:00:17)
[asean.baseline.en-th] Epoch 0.7701: train_loss/word=6.117926 (steps=338, words/sec=7981.96, time=0-00:00:18)
[asean.baseline.en-th] Epoch 0.8234: train_loss/word=6.101644 (steps=364, words/sec=7510.60, time=0-00:00:19)
[asean.baseline.en-th] Epoch 0.8739: train_loss/word=5.964764 (steps=386, words/sec=8173.69, time=0-00:00:20)
[asean.baseline.en-th] Epoch 0.9259: train_loss/word=5.911331 (steps=407, words/sec=8918.37, time=0-00:00:21)
[asean.baseline.en-th] Epoch 0.9778: train_loss/word=5.947149 (steps=433, words/sec=7171.83, time=0-00:00:22)
[asean.baseline.en-th] Epoch 1.0000: train_loss/word=6.173023 (steps=441, words/sec=8430.61, time=0-00:00:22)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 1.0000 dev BLEU4: 0.022339089084574184, 0.150414/0.041335/0.012554/0.003191 (BP = 1.000000, ratio=1.31, hyp_len=8942, ref_len=6809) (time=0-00:00:56)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.054192
[asean.baseline.en-th]              dev auxiliary Loss: 5.904 (ref_len=6809)
             checkpoint took 0-00:00:34
  best dev score, writing out model
[asean.baseline.en-th] Epoch 1.0024: train_loss/word=5.721522 (steps=442, words/sec=9244.81, time=0-00:01:16)
[asean.baseline.en-th] Epoch 1.0573: train_loss/word=5.870278 (steps=466, words/sec=8122.20, time=0-00:01:17)
[asean.baseline.en-th] Epoch 1.1088: train_loss/word=5.698316 (steps=488, words/sec=7426.15, time=0-00:01:18)
[asean.baseline.en-th] Epoch 1.1614: train_loss/word=5.779186 (steps=510, words/sec=7951.13, time=0-00:01:19)
[asean.baseline.en-th] Epoch 1.2128: train_loss/word=5.504260 (steps=531, words/sec=9273.35, time=0-00:01:20)
[asean.baseline.en-th] Epoch 1.2628: train_loss/word=5.679554 (steps=550, words/sec=8838.90, time=0-00:01:20)
[asean.baseline.en-th] Epoch 1.3146: train_loss/word=5.674396 (steps=573, words/sec=8040.78, time=0-00:01:21)
[asean.baseline.en-th] Epoch 1.3657: train_loss/word=5.432730 (steps=595, words/sec=8786.51, time=0-00:01:22)
[asean.baseline.en-th] Epoch 1.4165: train_loss/word=5.518498 (steps=617, words/sec=8146.74, time=0-00:01:23)
[asean.baseline.en-th] Epoch 1.4676: train_loss/word=5.494753 (steps=642, words/sec=7708.54, time=0-00:01:24)
[asean.baseline.en-th] Epoch 1.5183: train_loss/word=5.488386 (steps=665, words/sec=7710.46, time=0-00:01:25)
[asean.baseline.en-th] Epoch 1.5691: train_loss/word=5.375744 (steps=688, words/sec=7596.19, time=0-00:01:26)
[asean.baseline.en-th] Epoch 1.6191: train_loss/word=5.374062 (steps=709, words/sec=8239.55, time=0-00:01:27)
[asean.baseline.en-th] Epoch 1.6707: train_loss/word=5.450741 (steps=732, words/sec=7661.92, time=0-00:01:28)
[asean.baseline.en-th] Epoch 1.7217: train_loss/word=5.268990 (steps=753, words/sec=8949.10, time=0-00:01:29)
[asean.baseline.en-th] Epoch 1.7742: train_loss/word=5.395941 (steps=777, words/sec=7396.18, time=0-00:01:30)
[asean.baseline.en-th] Epoch 1.8257: train_loss/word=5.229081 (steps=802, words/sec=7792.24, time=0-00:01:31)
[asean.baseline.en-th] Epoch 1.8774: train_loss/word=5.341344 (steps=824, words/sec=7964.33, time=0-00:01:32)
[asean.baseline.en-th] Epoch 1.9290: train_loss/word=5.222419 (steps=847, words/sec=8649.07, time=0-00:01:33)
[asean.baseline.en-th] Epoch 1.9805: train_loss/word=5.130517 (steps=871, words/sec=7241.28, time=0-00:01:34)
[asean.baseline.en-th] Epoch 2.0000: train_loss/word=5.300243 (steps=881, words/sec=6464.32, time=0-00:01:35)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 2.0000 dev BLEU4: 0.056723595350849, 0.269203/0.103544/0.033961/0.010936 (BP = 1.000000, ratio=1.21, hyp_len=8254, ref_len=6809) (time=0-00:02:06)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.105161
[asean.baseline.en-th]              dev auxiliary Loss: 5.278 (ref_len=6809)
             checkpoint took 0-00:00:31
  best dev score, writing out model
[asean.baseline.en-th] Epoch 2.0029: train_loss/word=4.573283 (steps=882, words/sec=11887.11, time=0-00:02:12)
[asean.baseline.en-th] Epoch 2.0551: train_loss/word=5.044831 (steps=909, words/sec=6730.50, time=0-00:02:14)
[asean.baseline.en-th] Epoch 2.1066: train_loss/word=4.799418 (steps=930, words/sec=8738.87, time=0-00:02:14)
[asean.baseline.en-th] Epoch 2.1582: train_loss/word=5.002048 (steps=953, words/sec=8105.91, time=0-00:02:15)
[asean.baseline.en-th] Epoch 2.2089: train_loss/word=4.809707 (steps=977, words/sec=7346.78, time=0-00:02:17)
[asean.baseline.en-th] Epoch 2.2598: train_loss/word=4.902366 (steps=1000, words/sec=7993.50, time=0-00:02:18)
[asean.baseline.en-th] Epoch 2.3102: train_loss/word=4.854712 (steps=1021, words/sec=8318.04, time=0-00:02:18)
[asean.baseline.en-th] Epoch 2.3610: train_loss/word=4.929176 (steps=1042, words/sec=7599.49, time=0-00:02:19)
[asean.baseline.en-th] Epoch 2.4127: train_loss/word=4.839135 (steps=1063, words/sec=7981.35, time=0-00:02:20)
[asean.baseline.en-th] Epoch 2.4642: train_loss/word=4.829859 (steps=1086, words/sec=8410.07, time=0-00:02:21)
[asean.baseline.en-th] Epoch 2.5174: train_loss/word=4.775761 (steps=1110, words/sec=7983.82, time=0-00:02:22)
[asean.baseline.en-th] Epoch 2.5705: train_loss/word=4.746229 (steps=1132, words/sec=8721.23, time=0-00:02:23)
[asean.baseline.en-th] Epoch 2.6217: train_loss/word=4.840253 (steps=1157, words/sec=7281.69, time=0-00:02:24)
[asean.baseline.en-th] Epoch 2.6731: train_loss/word=4.757069 (steps=1178, words/sec=8490.22, time=0-00:02:25)
[asean.baseline.en-th] Epoch 2.7241: train_loss/word=4.699525 (steps=1199, words/sec=8723.57, time=0-00:02:26)
[asean.baseline.en-th] Epoch 2.7742: train_loss/word=4.726980 (steps=1220, words/sec=8648.36, time=0-00:02:27)
[asean.baseline.en-th] Epoch 2.8255: train_loss/word=4.676762 (steps=1243, words/sec=8282.78, time=0-00:02:28)
[asean.baseline.en-th] Epoch 2.8766: train_loss/word=4.621002 (steps=1265, words/sec=8233.62, time=0-00:02:29)
[asean.baseline.en-th] Epoch 2.9289: train_loss/word=4.667714 (steps=1287, words/sec=8832.83, time=0-00:02:29)
[asean.baseline.en-th] Epoch 2.9800: train_loss/word=4.769784 (steps=1312, words/sec=7148.22, time=0-00:02:31)
[asean.baseline.en-th] Epoch 3.0000: train_loss/word=4.670095 (steps=1322, words/sec=7310.95, time=0-00:02:31)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 3.0000 dev BLEU4: 0.1030861453176373, 0.349903/0.160150/0.067770/0.029737 (BP = 1.000000, ratio=1.13, hyp_len=7705, ref_len=6809) (time=0-00:03:00)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.149613
[asean.baseline.en-th]              dev auxiliary Loss: 4.870 (ref_len=6809)
             checkpoint took 0-00:00:28
  best dev score, writing out model
[asean.baseline.en-th] Epoch 3.0037: train_loss/word=4.014717 (steps=1323, words/sec=13742.34, time=0-00:03:06)
[asean.baseline.en-th] Epoch 3.0552: train_loss/word=4.358066 (steps=1345, words/sec=8279.39, time=0-00:03:07)
[asean.baseline.en-th] Epoch 3.1069: train_loss/word=4.343438 (steps=1367, words/sec=8700.06, time=0-00:03:08)
[asean.baseline.en-th] Epoch 3.1580: train_loss/word=4.271189 (steps=1391, words/sec=7827.68, time=0-00:03:09)
[asean.baseline.en-th] Epoch 3.2097: train_loss/word=4.435951 (steps=1413, words/sec=8023.97, time=0-00:03:10)
[asean.baseline.en-th] Epoch 3.2626: train_loss/word=4.095751 (steps=1435, words/sec=8783.61, time=0-00:03:11)
[asean.baseline.en-th] Epoch 3.3148: train_loss/word=4.235776 (steps=1459, words/sec=7201.05, time=0-00:03:12)
[asean.baseline.en-th] Epoch 3.3657: train_loss/word=4.237296 (steps=1482, words/sec=8274.94, time=0-00:03:13)
[asean.baseline.en-th] Epoch 3.4172: train_loss/word=4.333487 (steps=1501, words/sec=9004.91, time=0-00:03:14)
[asean.baseline.en-th] Epoch 3.4674: train_loss/word=4.428987 (steps=1524, words/sec=7454.14, time=0-00:03:15)
[asean.baseline.en-th] Epoch 3.5181: train_loss/word=4.349430 (steps=1548, words/sec=7315.49, time=0-00:03:16)
[asean.baseline.en-th] Epoch 3.5688: train_loss/word=4.247220 (steps=1573, words/sec=6583.54, time=0-00:03:17)
[asean.baseline.en-th] Epoch 3.6204: train_loss/word=4.445282 (steps=1598, words/sec=6659.02, time=0-00:03:18)
[asean.baseline.en-th] Epoch 3.6706: train_loss/word=4.248831 (steps=1622, words/sec=7692.31, time=0-00:03:19)
[asean.baseline.en-th] Epoch 3.7207: train_loss/word=4.168361 (steps=1642, words/sec=8050.47, time=0-00:03:20)
[asean.baseline.en-th] Epoch 3.7713: train_loss/word=4.262140 (steps=1666, words/sec=7375.59, time=0-00:03:21)
[asean.baseline.en-th] Epoch 3.8227: train_loss/word=4.168057 (steps=1685, words/sec=8392.87, time=0-00:03:22)
[asean.baseline.en-th] Epoch 3.8738: train_loss/word=4.270024 (steps=1707, words/sec=7961.88, time=0-00:03:23)
[asean.baseline.en-th] Epoch 3.9258: train_loss/word=4.141150 (steps=1730, words/sec=8591.10, time=0-00:03:24)
[asean.baseline.en-th] Epoch 3.9764: train_loss/word=4.196585 (steps=1753, words/sec=8230.24, time=0-00:03:25)
[asean.baseline.en-th] Epoch 4.0000: train_loss/word=4.188820 (steps=1763, words/sec=7686.82, time=0-00:03:25)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 4.0000 dev BLEU4: 0.1429749688073204, 0.397255/0.202252/0.099162/0.052448 (BP = 1.000000, ratio=1.16, hyp_len=7869, ref_len=6809) (time=0-00:03:55)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.184107
[asean.baseline.en-th]              dev auxiliary Loss: 4.613 (ref_len=6809)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.en-th] Epoch 4.0010: train_loss/word=4.673448 (steps=1764, words/sec=5755.24, time=0-00:04:02)
[asean.baseline.en-th] Epoch 4.0513: train_loss/word=3.790193 (steps=1788, words/sec=6614.96, time=0-00:04:03)
[asean.baseline.en-th] Epoch 4.1029: train_loss/word=3.801089 (steps=1809, words/sec=6411.84, time=0-00:04:04)
[asean.baseline.en-th] Epoch 4.1539: train_loss/word=3.728619 (steps=1829, words/sec=7814.51, time=0-00:04:05)
[asean.baseline.en-th] Epoch 4.2044: train_loss/word=3.840371 (steps=1851, words/sec=7342.65, time=0-00:04:06)
[asean.baseline.en-th] Epoch 4.2564: train_loss/word=3.806364 (steps=1870, words/sec=8498.77, time=0-00:04:06)
[asean.baseline.en-th] Epoch 4.3070: train_loss/word=3.788478 (steps=1891, words/sec=7956.12, time=0-00:04:07)
[asean.baseline.en-th] Epoch 4.3572: train_loss/word=3.844822 (steps=1915, words/sec=7075.27, time=0-00:04:08)
[asean.baseline.en-th] Epoch 4.4106: train_loss/word=3.876338 (steps=1936, words/sec=6829.23, time=0-00:04:09)
[asean.baseline.en-th] Epoch 4.4609: train_loss/word=3.859958 (steps=1959, words/sec=6291.91, time=0-00:04:11)
[asean.baseline.en-th] Epoch 4.5113: train_loss/word=3.821492 (steps=1983, words/sec=7188.55, time=0-00:04:12)
[asean.baseline.en-th] Epoch 4.5616: train_loss/word=3.900514 (steps=2010, words/sec=6102.08, time=0-00:04:13)
[asean.baseline.en-th] Epoch 4.6124: train_loss/word=3.817622 (steps=2032, words/sec=7527.94, time=0-00:04:14)
[asean.baseline.en-th] Epoch 4.6642: train_loss/word=3.799200 (steps=2057, words/sec=7289.43, time=0-00:04:16)
[asean.baseline.en-th] Epoch 4.7151: train_loss/word=3.814377 (steps=2077, words/sec=7754.82, time=0-00:04:16)
[asean.baseline.en-th] Epoch 4.7670: train_loss/word=3.774145 (steps=2099, words/sec=7749.34, time=0-00:04:17)
[asean.baseline.en-th] Epoch 4.8177: train_loss/word=3.767023 (steps=2120, words/sec=8326.13, time=0-00:04:18)
[asean.baseline.en-th] Epoch 4.8693: train_loss/word=3.877318 (steps=2145, words/sec=7484.73, time=0-00:04:19)
[asean.baseline.en-th] Epoch 4.9210: train_loss/word=4.001746 (steps=2169, words/sec=6693.22, time=0-00:04:21)
[asean.baseline.en-th] Epoch 4.9734: train_loss/word=3.891398 (steps=2192, words/sec=7803.71, time=0-00:04:22)
[asean.baseline.en-th] Epoch 5.0000: train_loss/word=3.915439 (steps=2206, words/sec=7021.19, time=0-00:04:22)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 5.0000 dev BLEU4: 0.17840340483051745, 0.436217/0.239942/0.130230/0.074318 (BP = 1.000000, ratio=1.17, hyp_len=7941, ref_len=6809) (time=0-00:04:52)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.218886
[asean.baseline.en-th]              dev auxiliary Loss: 4.440 (ref_len=6809)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.en-th] Epoch 5.0023: train_loss/word=3.527595 (steps=2207, words/sec=9618.89, time=0-00:04:58)
[asean.baseline.en-th] Epoch 5.0537: train_loss/word=3.473017 (steps=2231, words/sec=7532.38, time=0-00:04:59)
[asean.baseline.en-th] Epoch 5.1037: train_loss/word=3.356626 (steps=2252, words/sec=8781.99, time=0-00:05:00)
[asean.baseline.en-th] Epoch 5.1541: train_loss/word=3.543182 (steps=2274, words/sec=7137.51, time=0-00:05:01)
[asean.baseline.en-th] Epoch 5.2043: train_loss/word=3.578195 (steps=2295, words/sec=8175.92, time=0-00:05:02)
[asean.baseline.en-th] Epoch 5.2557: train_loss/word=3.363920 (steps=2316, words/sec=9016.18, time=0-00:05:03)
[asean.baseline.en-th] Epoch 5.3069: train_loss/word=3.559304 (steps=2342, words/sec=7036.06, time=0-00:05:04)
[asean.baseline.en-th] Epoch 5.3597: train_loss/word=3.392613 (steps=2363, words/sec=8885.80, time=0-00:05:05)
[asean.baseline.en-th] Epoch 5.4104: train_loss/word=3.365045 (steps=2382, words/sec=9599.19, time=0-00:05:06)
[asean.baseline.en-th] Epoch 5.4610: train_loss/word=3.651729 (steps=2407, words/sec=7314.09, time=0-00:05:07)
[asean.baseline.en-th] Epoch 5.5130: train_loss/word=3.521256 (steps=2430, words/sec=7128.88, time=0-00:05:08)
[asean.baseline.en-th] Epoch 5.5650: train_loss/word=3.458585 (steps=2454, words/sec=7596.70, time=0-00:05:09)
[asean.baseline.en-th] Epoch 5.6163: train_loss/word=3.480109 (steps=2479, words/sec=7644.66, time=0-00:05:10)
[asean.baseline.en-th] Epoch 5.6684: train_loss/word=3.464690 (steps=2501, words/sec=7932.37, time=0-00:05:11)
[asean.baseline.en-th] Epoch 5.7184: train_loss/word=3.549101 (steps=2523, words/sec=7029.16, time=0-00:05:12)
[asean.baseline.en-th] Epoch 5.7685: train_loss/word=3.461556 (steps=2543, words/sec=8540.53, time=0-00:05:13)
[asean.baseline.en-th] Epoch 5.8200: train_loss/word=3.493153 (steps=2566, words/sec=7733.26, time=0-00:05:14)
[asean.baseline.en-th] Epoch 5.8715: train_loss/word=3.510841 (steps=2592, words/sec=7770.42, time=0-00:05:15)
[asean.baseline.en-th] Epoch 5.9250: train_loss/word=3.440510 (steps=2613, words/sec=9242.48, time=0-00:05:16)
[asean.baseline.en-th] Epoch 5.9767: train_loss/word=3.443401 (steps=2636, words/sec=8332.63, time=0-00:05:17)
[asean.baseline.en-th] Epoch 6.0000: train_loss/word=3.341614 (steps=2646, words/sec=8978.25, time=0-00:05:17)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 6.0000 dev BLEU4: 0.20711838425328358, 0.458673/0.266265/0.157106/0.095910 (BP = 1.000000, ratio=1.15, hyp_len=7840, ref_len=6809) (time=0-00:05:47)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.240260
[asean.baseline.en-th]              dev auxiliary Loss: 4.344 (ref_len=6809)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.en-th] Epoch 6.0018: train_loss/word=3.585700 (steps=2647, words/sec=6620.16, time=0-00:05:53)
[asean.baseline.en-th] Epoch 6.0518: train_loss/word=3.242188 (steps=2671, words/sec=7971.61, time=0-00:05:54)
[asean.baseline.en-th] Epoch 6.1023: train_loss/word=3.164021 (steps=2692, words/sec=7299.88, time=0-00:05:55)
[asean.baseline.en-th] Epoch 6.1533: train_loss/word=3.165229 (steps=2712, words/sec=7963.94, time=0-00:05:56)
[asean.baseline.en-th] Epoch 6.2046: train_loss/word=2.986633 (steps=2732, words/sec=8853.02, time=0-00:05:56)
[asean.baseline.en-th] Epoch 6.2563: train_loss/word=3.011263 (steps=2754, words/sec=7741.83, time=0-00:05:57)
[asean.baseline.en-th] Epoch 6.3077: train_loss/word=3.226634 (steps=2779, words/sec=7473.62, time=0-00:05:58)
[asean.baseline.en-th] Epoch 6.3613: train_loss/word=3.174301 (steps=2803, words/sec=8426.23, time=0-00:05:59)
[asean.baseline.en-th] Epoch 6.4128: train_loss/word=3.249530 (steps=2827, words/sec=7669.01, time=0-00:06:00)
[asean.baseline.en-th] Epoch 6.4636: train_loss/word=3.111363 (steps=2848, words/sec=9280.37, time=0-00:06:01)
[asean.baseline.en-th] Epoch 6.5143: train_loss/word=3.093578 (steps=2867, words/sec=9274.03, time=0-00:06:02)
[asean.baseline.en-th] Epoch 6.5659: train_loss/word=3.201079 (steps=2891, words/sec=7633.79, time=0-00:06:03)
[asean.baseline.en-th] Epoch 6.6166: train_loss/word=3.285984 (steps=2916, words/sec=6909.84, time=0-00:06:04)
[asean.baseline.en-th] Epoch 6.6674: train_loss/word=3.345154 (steps=2938, words/sec=7556.95, time=0-00:06:05)
[asean.baseline.en-th] Epoch 6.7176: train_loss/word=3.176548 (steps=2961, words/sec=8841.97, time=0-00:06:06)
[asean.baseline.en-th] Epoch 6.7714: train_loss/word=3.227974 (steps=2984, words/sec=8801.40, time=0-00:06:07)
[asean.baseline.en-th] Epoch 6.8217: train_loss/word=3.230313 (steps=3008, words/sec=8432.52, time=0-00:06:08)
[asean.baseline.en-th] Epoch 6.8723: train_loss/word=3.291716 (steps=3031, words/sec=7816.22, time=0-00:06:09)
[asean.baseline.en-th] Epoch 6.9254: train_loss/word=3.149516 (steps=3053, words/sec=8780.95, time=0-00:06:10)
[asean.baseline.en-th] Epoch 6.9761: train_loss/word=3.247445 (steps=3076, words/sec=7545.18, time=0-00:06:11)
[asean.baseline.en-th] Epoch 7.0000: train_loss/word=3.130369 (steps=3087, words/sec=7337.16, time=0-00:06:12)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 7.0000 dev BLEU4: 0.24289854358164203, 0.507073/0.308480/0.186129/0.119560 (BP = 1.000000, ratio=1.07, hyp_len=7281, ref_len=6809) (time=0-00:06:39)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.266702
[asean.baseline.en-th]              dev auxiliary Loss: 4.271 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 7.0032: train_loss/word=2.646110 (steps=3088, words/sec=9783.26, time=0-00:06:44)
[asean.baseline.en-th] Epoch 7.0535: train_loss/word=2.888265 (steps=3110, words/sec=7734.80, time=0-00:06:45)
[asean.baseline.en-th] Epoch 7.1051: train_loss/word=2.829697 (steps=3131, words/sec=8732.16, time=0-00:06:46)
[asean.baseline.en-th] Epoch 7.1564: train_loss/word=2.862822 (steps=3154, words/sec=8859.69, time=0-00:06:47)
[asean.baseline.en-th] Epoch 7.2083: train_loss/word=2.899114 (steps=3178, words/sec=8876.88, time=0-00:06:48)
[asean.baseline.en-th] Epoch 7.2606: train_loss/word=3.008506 (steps=3202, words/sec=7782.58, time=0-00:06:49)
[asean.baseline.en-th] Epoch 7.3109: train_loss/word=3.063679 (steps=3226, words/sec=7762.53, time=0-00:06:50)
[asean.baseline.en-th] Epoch 7.3620: train_loss/word=2.926296 (steps=3248, words/sec=8820.54, time=0-00:06:51)
[asean.baseline.en-th] Epoch 7.4122: train_loss/word=3.012612 (steps=3272, words/sec=8291.88, time=0-00:06:52)
[asean.baseline.en-th] Epoch 7.4625: train_loss/word=3.024303 (steps=3294, words/sec=7980.26, time=0-00:06:53)
[asean.baseline.en-th] Epoch 7.5126: train_loss/word=2.948840 (steps=3313, words/sec=9512.41, time=0-00:06:54)
[asean.baseline.en-th] Epoch 7.5641: train_loss/word=2.904105 (steps=3333, words/sec=9029.03, time=0-00:06:55)
[asean.baseline.en-th] Epoch 7.6153: train_loss/word=2.908759 (steps=3355, words/sec=9106.29, time=0-00:06:55)
[asean.baseline.en-th] Epoch 7.6677: train_loss/word=2.895323 (steps=3380, words/sec=9073.86, time=0-00:06:57)
[asean.baseline.en-th] Epoch 7.7208: train_loss/word=2.988147 (steps=3400, words/sec=8379.49, time=0-00:06:57)
[asean.baseline.en-th] Epoch 7.7722: train_loss/word=3.003519 (steps=3423, words/sec=8173.80, time=0-00:06:58)
[asean.baseline.en-th] Epoch 7.8246: train_loss/word=3.081111 (steps=3447, words/sec=7202.58, time=0-00:06:59)
[asean.baseline.en-th] Epoch 7.8749: train_loss/word=2.943240 (steps=3470, words/sec=8777.86, time=0-00:07:00)
[asean.baseline.en-th] Epoch 7.9256: train_loss/word=3.023810 (steps=3494, words/sec=8116.74, time=0-00:07:01)
[asean.baseline.en-th] Epoch 7.9774: train_loss/word=3.007958 (steps=3518, words/sec=8028.89, time=0-00:07:02)
[asean.baseline.en-th] Epoch 8.0000: train_loss/word=2.878678 (steps=3528, words/sec=9738.35, time=0-00:07:03)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 8.0000 dev BLEU4: 0.2535372176106112, 0.517459/0.320472/0.195903/0.127192 (BP = 1.000000, ratio=1.07, hyp_len=7303, ref_len=6809) (time=0-00:07:29)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.278063
[asean.baseline.en-th]              dev auxiliary Loss: 4.237 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 8.0017: train_loss/word=2.774643 (steps=3529, words/sec=8537.48, time=0-00:07:35)
[asean.baseline.en-th] Epoch 8.0520: train_loss/word=2.688861 (steps=3550, words/sec=8648.59, time=0-00:07:36)
[asean.baseline.en-th] Epoch 8.1031: train_loss/word=2.701130 (steps=3573, words/sec=8388.37, time=0-00:07:37)
[asean.baseline.en-th] Epoch 8.1551: train_loss/word=2.649359 (steps=3597, words/sec=8975.10, time=0-00:07:38)
[asean.baseline.en-th] Epoch 8.2073: train_loss/word=2.728345 (steps=3622, words/sec=8356.16, time=0-00:07:39)
[asean.baseline.en-th] Epoch 8.2587: train_loss/word=2.757686 (steps=3645, words/sec=8648.21, time=0-00:07:40)
[asean.baseline.en-th] Epoch 8.3108: train_loss/word=2.662058 (steps=3665, words/sec=9687.64, time=0-00:07:41)
[asean.baseline.en-th] Epoch 8.3614: train_loss/word=2.841526 (steps=3687, words/sec=8755.60, time=0-00:07:41)
[asean.baseline.en-th] Epoch 8.4127: train_loss/word=2.754633 (steps=3711, words/sec=8065.21, time=0-00:07:42)
[asean.baseline.en-th] Epoch 8.4634: train_loss/word=2.818855 (steps=3734, words/sec=8230.63, time=0-00:07:43)
[asean.baseline.en-th] Epoch 8.5151: train_loss/word=2.766566 (steps=3757, words/sec=8895.94, time=0-00:07:44)
[asean.baseline.en-th] Epoch 8.5651: train_loss/word=2.690418 (steps=3779, words/sec=9211.77, time=0-00:07:45)
[asean.baseline.en-th] Epoch 8.6151: train_loss/word=2.725684 (steps=3801, words/sec=7690.03, time=0-00:07:46)
[asean.baseline.en-th] Epoch 8.6661: train_loss/word=2.825352 (steps=3823, words/sec=7761.22, time=0-00:07:47)
[asean.baseline.en-th] Epoch 8.7176: train_loss/word=2.837658 (steps=3847, words/sec=7974.42, time=0-00:07:48)
[asean.baseline.en-th] Epoch 8.7694: train_loss/word=2.828945 (steps=3868, words/sec=8694.51, time=0-00:07:49)
[asean.baseline.en-th] Epoch 8.8194: train_loss/word=2.799865 (steps=3893, words/sec=7938.16, time=0-00:07:50)
[asean.baseline.en-th] Epoch 8.8710: train_loss/word=2.733488 (steps=3914, words/sec=9274.76, time=0-00:07:51)
[asean.baseline.en-th] Epoch 8.9231: train_loss/word=2.784879 (steps=3936, words/sec=8192.39, time=0-00:07:52)
[asean.baseline.en-th] Epoch 8.9747: train_loss/word=2.772701 (steps=3958, words/sec=8590.04, time=0-00:07:53)
[asean.baseline.en-th] Epoch 9.0000: train_loss/word=2.979341 (steps=3968, words/sec=7440.09, time=0-00:07:53)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 9.0000 dev BLEU4: 0.26260397672443936, 0.522765/0.323790/0.204767/0.137207 (BP = 1.000000, ratio=1.06, hyp_len=7248, ref_len=6809) (time=0-00:08:20)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.283208
[asean.baseline.en-th]              dev auxiliary Loss: 4.246 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 9.0021: train_loss/word=2.542506 (steps=3969, words/sec=8120.85, time=0-00:08:26)
[asean.baseline.en-th] Epoch 9.0550: train_loss/word=2.525896 (steps=3993, words/sec=7345.93, time=0-00:08:27)
[asean.baseline.en-th] Epoch 9.1062: train_loss/word=2.524296 (steps=4014, words/sec=8767.74, time=0-00:08:28)
[asean.baseline.en-th] Epoch 9.1580: train_loss/word=2.541053 (steps=4035, words/sec=9044.59, time=0-00:08:28)
[asean.baseline.en-th] Epoch 9.2087: train_loss/word=2.563336 (steps=4059, words/sec=8076.89, time=0-00:08:29)
[asean.baseline.en-th] Epoch 9.2589: train_loss/word=2.498509 (steps=4080, words/sec=9308.08, time=0-00:08:30)
[asean.baseline.en-th] Epoch 9.3093: train_loss/word=2.511516 (steps=4102, words/sec=9034.08, time=0-00:08:31)
[asean.baseline.en-th] Epoch 9.3601: train_loss/word=2.653523 (steps=4122, words/sec=8579.43, time=0-00:08:32)
[asean.baseline.en-th] Epoch 9.4121: train_loss/word=2.544765 (steps=4141, words/sec=10203.21, time=0-00:08:33)
[asean.baseline.en-th] Epoch 9.4643: train_loss/word=2.621036 (steps=4166, words/sec=8168.19, time=0-00:08:34)
[asean.baseline.en-th] Epoch 9.5155: train_loss/word=2.545332 (steps=4187, words/sec=9378.21, time=0-00:08:34)
[asean.baseline.en-th] Epoch 9.5671: train_loss/word=2.567899 (steps=4208, words/sec=9160.89, time=0-00:08:35)
[asean.baseline.en-th] Epoch 9.6192: train_loss/word=2.625962 (steps=4232, words/sec=8283.37, time=0-00:08:36)
[asean.baseline.en-th] Epoch 9.6695: train_loss/word=2.648066 (steps=4255, words/sec=7918.92, time=0-00:08:37)
[asean.baseline.en-th] Epoch 9.7203: train_loss/word=2.569421 (steps=4277, words/sec=8594.28, time=0-00:08:38)
[asean.baseline.en-th] Epoch 9.7703: train_loss/word=2.659128 (steps=4302, words/sec=8351.29, time=0-00:08:39)
[asean.baseline.en-th] Epoch 9.8213: train_loss/word=2.635397 (steps=4327, words/sec=7732.65, time=0-00:08:40)
[asean.baseline.en-th] Epoch 9.8728: train_loss/word=2.659610 (steps=4351, words/sec=8629.05, time=0-00:08:41)
[asean.baseline.en-th] Epoch 9.9250: train_loss/word=2.711617 (steps=4374, words/sec=7609.08, time=0-00:08:42)
[asean.baseline.en-th] Epoch 9.9770: train_loss/word=2.664599 (steps=4398, words/sec=8161.62, time=0-00:08:44)
[asean.baseline.en-th] Epoch 10.0000: train_loss/word=2.759871 (steps=4409, words/sec=7179.64, time=0-00:08:44)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 10.0000 dev BLEU4: 0.2744914377709162, 0.530177/0.332696/0.214312/0.150176 (BP = 1.000000, ratio=1.07, hyp_len=7307, ref_len=6809) (time=0-00:09:11)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.294756
[asean.baseline.en-th]              dev auxiliary Loss: 4.243 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
[asean.baseline.en-th] Epoch 10.0018: train_loss/word=2.251122 (steps=4410, words/sec=8068.58, time=0-00:09:17)
[asean.baseline.en-th] Epoch 10.0536: train_loss/word=2.474963 (steps=4438, words/sec=7992.92, time=0-00:09:18)
[asean.baseline.en-th] Epoch 10.1036: train_loss/word=2.396329 (steps=4461, words/sec=7625.41, time=0-00:09:19)
[asean.baseline.en-th] Epoch 10.1559: train_loss/word=2.374673 (steps=4483, words/sec=8916.17, time=0-00:09:20)
[asean.baseline.en-th] Epoch 10.2069: train_loss/word=2.460750 (steps=4508, words/sec=7856.35, time=0-00:09:21)
[asean.baseline.en-th] Epoch 10.2589: train_loss/word=2.428047 (steps=4529, words/sec=8336.08, time=0-00:09:22)
[asean.baseline.en-th] Epoch 10.3090: train_loss/word=2.379196 (steps=4550, words/sec=8742.50, time=0-00:09:23)
[asean.baseline.en-th] Epoch 10.3598: train_loss/word=2.458123 (steps=4573, words/sec=8010.18, time=0-00:09:24)
[asean.baseline.en-th] Epoch 10.4114: train_loss/word=2.378717 (steps=4594, words/sec=9571.46, time=0-00:09:25)
[asean.baseline.en-th] Epoch 10.4616: train_loss/word=2.428222 (steps=4616, words/sec=8859.81, time=0-00:09:25)
[asean.baseline.en-th] Epoch 10.5139: train_loss/word=2.511118 (steps=4642, words/sec=7668.74, time=0-00:09:27)
[asean.baseline.en-th] Epoch 10.5643: train_loss/word=2.514396 (steps=4665, words/sec=8357.50, time=0-00:09:28)
[asean.baseline.en-th] Epoch 10.6150: train_loss/word=2.484312 (steps=4686, words/sec=9049.66, time=0-00:09:28)
[asean.baseline.en-th] Epoch 10.6655: train_loss/word=2.496848 (steps=4710, words/sec=7972.75, time=0-00:09:30)
[asean.baseline.en-th] Epoch 10.7166: train_loss/word=2.566821 (steps=4733, words/sec=7570.40, time=0-00:09:31)
[asean.baseline.en-th] Epoch 10.7671: train_loss/word=2.527949 (steps=4753, words/sec=9024.66, time=0-00:09:31)
[asean.baseline.en-th] Epoch 10.8189: train_loss/word=2.411762 (steps=4771, words/sec=10079.15, time=0-00:09:32)
[asean.baseline.en-th] Epoch 10.8692: train_loss/word=2.497252 (steps=4791, words/sec=9040.70, time=0-00:09:33)
[asean.baseline.en-th] Epoch 10.9210: train_loss/word=2.530374 (steps=4815, words/sec=7809.50, time=0-00:09:34)
[asean.baseline.en-th] Epoch 10.9715: train_loss/word=2.506773 (steps=4838, words/sec=8139.03, time=0-00:09:35)
[asean.baseline.en-th] Epoch 11.0000: train_loss/word=2.542801 (steps=4850, words/sec=8425.32, time=0-00:09:35)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 11.0000 dev BLEU4: 0.2971675604102752, 0.554647/0.358357/0.235968/0.166272 (BP = 1.000000, ratio=1.02, hyp_len=6972, ref_len=6809) (time=0-00:10:01)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.305442
[asean.baseline.en-th]              dev auxiliary Loss: 4.228 (ref_len=6809)
             checkpoint took 0-00:00:25
  best dev score, writing out model
[asean.baseline.en-th] Epoch 11.0026: train_loss/word=2.128107 (steps=4851, words/sec=9943.53, time=0-00:10:07)
[asean.baseline.en-th] Epoch 11.0548: train_loss/word=2.180928 (steps=4873, words/sec=9578.31, time=0-00:10:08)
[asean.baseline.en-th] Epoch 11.1068: train_loss/word=2.324921 (steps=4896, words/sec=8104.26, time=0-00:10:09)
[asean.baseline.en-th] Epoch 11.1570: train_loss/word=2.311764 (steps=4921, words/sec=7536.98, time=0-00:10:10)
[asean.baseline.en-th] Epoch 11.2077: train_loss/word=2.248713 (steps=4943, words/sec=8694.81, time=0-00:10:11)
[asean.baseline.en-th] Epoch 11.2592: train_loss/word=2.299016 (steps=4965, words/sec=8970.12, time=0-00:10:12)
[asean.baseline.en-th] Epoch 11.3109: train_loss/word=2.387967 (steps=4991, words/sec=8393.83, time=0-00:10:13)
[asean.baseline.en-th] Epoch 11.3620: train_loss/word=2.334229 (steps=5013, words/sec=8051.08, time=0-00:10:14)
[asean.baseline.en-th] Epoch 11.4126: train_loss/word=2.330305 (steps=5035, words/sec=8853.61, time=0-00:10:15)
[asean.baseline.en-th] Epoch 11.4635: train_loss/word=2.377264 (steps=5059, words/sec=8016.03, time=0-00:10:16)
[asean.baseline.en-th] Epoch 11.5151: train_loss/word=2.389601 (steps=5080, words/sec=8154.21, time=0-00:10:16)
[asean.baseline.en-th] Epoch 11.5652: train_loss/word=2.339006 (steps=5100, words/sec=9437.14, time=0-00:10:17)
[asean.baseline.en-th] Epoch 11.6156: train_loss/word=2.396802 (steps=5125, words/sec=7944.09, time=0-00:10:18)
[asean.baseline.en-th] Epoch 11.6690: train_loss/word=2.341984 (steps=5147, words/sec=8590.12, time=0-00:10:19)
[asean.baseline.en-th] Epoch 11.7197: train_loss/word=2.403185 (steps=5167, words/sec=8483.92, time=0-00:10:20)
[asean.baseline.en-th] Epoch 11.7704: train_loss/word=2.394214 (steps=5189, words/sec=8657.03, time=0-00:10:21)
[asean.baseline.en-th] Epoch 11.8213: train_loss/word=2.453460 (steps=5211, words/sec=6940.95, time=0-00:10:22)
[asean.baseline.en-th] Epoch 11.8726: train_loss/word=2.306226 (steps=5232, words/sec=9407.94, time=0-00:10:23)
[asean.baseline.en-th] Epoch 11.9233: train_loss/word=2.421801 (steps=5256, words/sec=7674.89, time=0-00:10:24)
[asean.baseline.en-th] Epoch 11.9741: train_loss/word=2.488002 (steps=5279, words/sec=7697.46, time=0-00:10:25)
[asean.baseline.en-th] Epoch 12.0000: train_loss/word=2.390568 (steps=5291, words/sec=8817.62, time=0-00:10:25)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 12.0000 dev BLEU4: 0.3121032964256869, 0.560035/0.369309/0.250850/0.182883 (BP = 1.000000, ratio=1.01, hyp_len=6896, ref_len=6809) (time=0-00:10:51)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.313931
[asean.baseline.en-th]              dev auxiliary Loss: 4.224 (ref_len=6809)
             checkpoint took 0-00:00:25
  best dev score, writing out model
[asean.baseline.en-th] Epoch 12.0024: train_loss/word=1.966666 (steps=5292, words/sec=9704.16, time=0-00:10:57)
[asean.baseline.en-th] Epoch 12.0537: train_loss/word=2.124538 (steps=5312, words/sec=9944.24, time=0-00:10:57)
[asean.baseline.en-th] Epoch 12.1063: train_loss/word=2.284863 (steps=5338, words/sec=7082.63, time=0-00:10:59)
[asean.baseline.en-th] Epoch 12.1571: train_loss/word=2.272451 (steps=5362, words/sec=7406.48, time=0-00:11:00)
[asean.baseline.en-th] Epoch 12.2080: train_loss/word=2.171920 (steps=5383, words/sec=9432.35, time=0-00:11:00)
[asean.baseline.en-th] Epoch 12.2591: train_loss/word=2.196126 (steps=5405, words/sec=9061.61, time=0-00:11:01)
[asean.baseline.en-th] Epoch 12.3098: train_loss/word=2.256552 (steps=5429, words/sec=7653.15, time=0-00:11:02)
[asean.baseline.en-th] Epoch 12.3601: train_loss/word=2.244846 (steps=5451, words/sec=8019.39, time=0-00:11:03)
[asean.baseline.en-th] Epoch 12.4130: train_loss/word=2.180335 (steps=5473, words/sec=8130.96, time=0-00:11:04)
[asean.baseline.en-th] Epoch 12.4643: train_loss/word=2.240710 (steps=5498, words/sec=8772.68, time=0-00:11:05)
[asean.baseline.en-th] Epoch 12.5145: train_loss/word=2.280850 (steps=5523, words/sec=7928.44, time=0-00:11:06)
[asean.baseline.en-th] Epoch 12.5651: train_loss/word=2.205935 (steps=5545, words/sec=8870.41, time=0-00:11:07)
[asean.baseline.en-th] Epoch 12.6152: train_loss/word=2.246524 (steps=5565, words/sec=8764.54, time=0-00:11:08)
[asean.baseline.en-th] Epoch 12.6660: train_loss/word=2.351746 (steps=5587, words/sec=8254.78, time=0-00:11:09)
[asean.baseline.en-th] Epoch 12.7170: train_loss/word=2.365115 (steps=5609, words/sec=7927.80, time=0-00:11:10)
[asean.baseline.en-th] Epoch 12.7683: train_loss/word=2.294450 (steps=5630, words/sec=8435.88, time=0-00:11:11)
[asean.baseline.en-th] Epoch 12.8194: train_loss/word=2.256601 (steps=5652, words/sec=8618.72, time=0-00:11:12)
[asean.baseline.en-th] Epoch 12.8721: train_loss/word=2.292005 (steps=5677, words/sec=8030.98, time=0-00:11:13)
[asean.baseline.en-th] Epoch 12.9249: train_loss/word=2.361029 (steps=5701, words/sec=8268.30, time=0-00:11:14)
[asean.baseline.en-th] Epoch 12.9759: train_loss/word=2.307752 (steps=5724, words/sec=8119.52, time=0-00:11:15)
[asean.baseline.en-th] Epoch 13.0000: train_loss/word=2.258826 (steps=5733, words/sec=9524.66, time=0-00:11:15)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 13.0000 dev BLEU4: 0.30781896584898844, 0.545670/0.360586/0.249715/0.182725 (BP = 1.000000, ratio=1.05, hyp_len=7171, ref_len=6809) (time=0-00:11:41)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.314853
[asean.baseline.en-th]              dev auxiliary Loss: 4.220 (ref_len=6809)
             checkpoint took 0-00:00:26
[asean.baseline.en-th] Epoch 13.0021: train_loss/word=1.952673 (steps=5734, words/sec=8041.63, time=0-00:11:42)
[asean.baseline.en-th] Epoch 13.0522: train_loss/word=2.179238 (steps=5755, words/sec=7772.22, time=0-00:11:42)
[asean.baseline.en-th] Epoch 13.1027: train_loss/word=2.127164 (steps=5778, words/sec=8701.00, time=0-00:11:43)
[asean.baseline.en-th] Epoch 13.1527: train_loss/word=2.139600 (steps=5800, words/sec=8538.73, time=0-00:11:44)
[asean.baseline.en-th] Epoch 13.2047: train_loss/word=2.139995 (steps=5822, words/sec=8831.56, time=0-00:11:45)
[asean.baseline.en-th] Epoch 13.2558: train_loss/word=2.157392 (steps=5847, words/sec=7099.56, time=0-00:11:46)
[asean.baseline.en-th] Epoch 13.3086: train_loss/word=2.085961 (steps=5867, words/sec=9002.53, time=0-00:11:47)
[asean.baseline.en-th] Epoch 13.3602: train_loss/word=2.179469 (steps=5891, words/sec=8176.38, time=0-00:11:48)
[asean.baseline.en-th] Epoch 13.4106: train_loss/word=2.249472 (steps=5913, words/sec=7727.85, time=0-00:11:49)
[asean.baseline.en-th] Epoch 13.4614: train_loss/word=2.138939 (steps=5936, words/sec=8617.76, time=0-00:11:50)
[asean.baseline.en-th] Epoch 13.5120: train_loss/word=2.138296 (steps=5958, words/sec=8785.59, time=0-00:11:51)
[asean.baseline.en-th] Epoch 13.5630: train_loss/word=2.110578 (steps=5978, words/sec=9243.79, time=0-00:11:52)
[asean.baseline.en-th] Epoch 13.6144: train_loss/word=2.144985 (steps=6001, words/sec=8601.89, time=0-00:11:53)
[asean.baseline.en-th] Epoch 13.6665: train_loss/word=2.249046 (steps=6025, words/sec=7410.73, time=0-00:11:54)
[asean.baseline.en-th] Epoch 13.7170: train_loss/word=2.166804 (steps=6049, words/sec=7905.76, time=0-00:11:55)
[asean.baseline.en-th] Epoch 13.7676: train_loss/word=2.248683 (steps=6071, words/sec=7736.28, time=0-00:11:56)
[asean.baseline.en-th] Epoch 13.8189: train_loss/word=2.224960 (steps=6092, words/sec=8179.44, time=0-00:11:57)
[asean.baseline.en-th] Epoch 13.8700: train_loss/word=2.252077 (steps=6120, words/sec=7277.95, time=0-00:11:58)
[asean.baseline.en-th] Epoch 13.9222: train_loss/word=2.181907 (steps=6142, words/sec=8944.08, time=0-00:11:59)
[asean.baseline.en-th] Epoch 13.9745: train_loss/word=2.204842 (steps=6161, words/sec=9409.36, time=0-00:12:00)
[asean.baseline.en-th] Epoch 14.0000: train_loss/word=2.182924 (steps=6173, words/sec=8582.47, time=0-00:12:00)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 14.0000 dev BLEU4: 0.3147863013923644, 0.555634/0.368655/0.253645/0.188985 (BP = 1.000000, ratio=1.05, hyp_len=7118, ref_len=6809) (time=0-00:12:26)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.321683
[asean.baseline.en-th]              dev auxiliary Loss: 4.240 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 14.0019: train_loss/word=1.927214 (steps=6174, words/sec=9101.59, time=0-00:12:32)
[asean.baseline.en-th] Epoch 14.0524: train_loss/word=2.027207 (steps=6197, words/sec=8808.78, time=0-00:12:33)
[asean.baseline.en-th] Epoch 14.1025: train_loss/word=2.021262 (steps=6216, words/sec=9018.73, time=0-00:12:34)
[asean.baseline.en-th] Epoch 14.1533: train_loss/word=2.020567 (steps=6238, words/sec=9095.91, time=0-00:12:35)
[asean.baseline.en-th] Epoch 14.2044: train_loss/word=2.054966 (steps=6259, words/sec=9120.15, time=0-00:12:35)
[asean.baseline.en-th] Epoch 14.2570: train_loss/word=2.129496 (steps=6283, words/sec=7912.26, time=0-00:12:36)
[asean.baseline.en-th] Epoch 14.3074: train_loss/word=2.090971 (steps=6305, words/sec=8105.97, time=0-00:12:37)
[asean.baseline.en-th] Epoch 14.3594: train_loss/word=2.081591 (steps=6325, words/sec=9150.23, time=0-00:12:38)
[asean.baseline.en-th] Epoch 14.4111: train_loss/word=2.088930 (steps=6350, words/sec=8397.53, time=0-00:12:39)
[asean.baseline.en-th] Epoch 14.4613: train_loss/word=2.063348 (steps=6371, words/sec=8972.27, time=0-00:12:40)
[asean.baseline.en-th] Epoch 14.5116: train_loss/word=2.132948 (steps=6395, words/sec=7376.30, time=0-00:12:41)
[asean.baseline.en-th] Epoch 14.5634: train_loss/word=2.204747 (steps=6421, words/sec=7481.74, time=0-00:12:42)
[asean.baseline.en-th] Epoch 14.6147: train_loss/word=2.142631 (steps=6440, words/sec=9219.03, time=0-00:12:43)
[asean.baseline.en-th] Epoch 14.6651: train_loss/word=2.104463 (steps=6463, words/sec=8366.49, time=0-00:12:44)
[asean.baseline.en-th] Epoch 14.7153: train_loss/word=2.089890 (steps=6484, words/sec=8857.51, time=0-00:12:45)
[asean.baseline.en-th] Epoch 14.7662: train_loss/word=2.117302 (steps=6507, words/sec=8458.12, time=0-00:12:46)
[asean.baseline.en-th] Epoch 14.8164: train_loss/word=2.166871 (steps=6530, words/sec=8254.91, time=0-00:12:47)
[asean.baseline.en-th] Epoch 14.8682: train_loss/word=2.114693 (steps=6552, words/sec=9119.50, time=0-00:12:48)
[asean.baseline.en-th] Epoch 14.9185: train_loss/word=2.200182 (steps=6577, words/sec=6917.37, time=0-00:12:49)
[asean.baseline.en-th] Epoch 14.9696: train_loss/word=2.174895 (steps=6602, words/sec=8553.78, time=0-00:12:50)
[asean.baseline.en-th] Epoch 15.0000: train_loss/word=2.138369 (steps=6615, words/sec=9017.67, time=0-00:12:50)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 15.0000 dev BLEU4: 0.3125275462923356, 0.546066/0.363279/0.253201/0.189934 (BP = 1.000000, ratio=1.05, hyp_len=7142, ref_len=6809) (time=0-00:13:17)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.314051
[asean.baseline.en-th]              dev auxiliary Loss: 4.264 (ref_len=6809)
             checkpoint took 0-00:00:26
[asean.baseline.en-th] Epoch 15.0034: train_loss/word=1.903504 (steps=6616, words/sec=11517.65, time=0-00:13:17)
[asean.baseline.en-th] Epoch 15.0552: train_loss/word=2.038929 (steps=6639, words/sec=8191.82, time=0-00:13:18)
[asean.baseline.en-th] Epoch 15.1059: train_loss/word=1.968478 (steps=6661, words/sec=9329.85, time=0-00:13:19)
[asean.baseline.en-th] Epoch 15.1579: train_loss/word=1.992717 (steps=6685, words/sec=8544.09, time=0-00:13:20)
[asean.baseline.en-th] Epoch 15.2112: train_loss/word=1.994300 (steps=6706, words/sec=9384.17, time=0-00:13:21)
[asean.baseline.en-th] Epoch 15.2624: train_loss/word=2.032442 (steps=6730, words/sec=7568.97, time=0-00:13:22)
[asean.baseline.en-th] Epoch 15.3136: train_loss/word=2.043929 (steps=6751, words/sec=8820.53, time=0-00:13:23)
[asean.baseline.en-th] Epoch 15.3654: train_loss/word=2.070932 (steps=6775, words/sec=7616.45, time=0-00:13:24)
[asean.baseline.en-th] Epoch 15.4169: train_loss/word=1.995160 (steps=6796, words/sec=9479.37, time=0-00:13:24)
[asean.baseline.en-th] Epoch 15.4686: train_loss/word=2.027105 (steps=6822, words/sec=8380.59, time=0-00:13:26)
[asean.baseline.en-th] Epoch 15.5205: train_loss/word=2.033554 (steps=6845, words/sec=7845.34, time=0-00:13:27)
[asean.baseline.en-th] Epoch 15.5715: train_loss/word=2.046160 (steps=6866, words/sec=9093.29, time=0-00:13:27)
[asean.baseline.en-th] Epoch 15.6225: train_loss/word=2.082103 (steps=6884, words/sec=9669.05, time=0-00:13:28)
[asean.baseline.en-th] Epoch 15.6751: train_loss/word=2.073745 (steps=6907, words/sec=8359.81, time=0-00:13:29)
[asean.baseline.en-th] Epoch 15.7264: train_loss/word=2.060714 (steps=6930, words/sec=8324.92, time=0-00:13:30)
[asean.baseline.en-th] Epoch 15.7773: train_loss/word=2.042917 (steps=6954, words/sec=8543.49, time=0-00:13:31)
[asean.baseline.en-th] Epoch 15.8289: train_loss/word=2.111174 (steps=6977, words/sec=7654.35, time=0-00:13:32)
[asean.baseline.en-th] Epoch 15.8809: train_loss/word=2.111311 (steps=7000, words/sec=8390.55, time=0-00:13:33)
[asean.baseline.en-th] Epoch 15.9314: train_loss/word=2.023705 (steps=7023, words/sec=9112.74, time=0-00:13:34)
[asean.baseline.en-th] Epoch 15.9820: train_loss/word=2.130087 (steps=7049, words/sec=7291.39, time=0-00:13:35)
[asean.baseline.en-th] Epoch 16.0000: train_loss/word=2.145818 (steps=7057, words/sec=8547.50, time=0-00:13:35)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 16.0000 dev BLEU4: 0.319274561983077, 0.554096/0.367794/0.258101/0.197550 (BP = 1.000000, ratio=1.05, hyp_len=7154, ref_len=6809) (time=0-00:14:02)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.323348
[asean.baseline.en-th]              dev auxiliary Loss: 4.292 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 16.0032: train_loss/word=1.923943 (steps=7058, words/sec=12244.52, time=0-00:14:08)
[asean.baseline.en-th] Epoch 16.0544: train_loss/word=1.951258 (steps=7079, words/sec=8103.45, time=0-00:14:08)
[asean.baseline.en-th] Epoch 16.1045: train_loss/word=1.953560 (steps=7103, words/sec=8250.26, time=0-00:14:09)
[asean.baseline.en-th] Epoch 16.1551: train_loss/word=2.009912 (steps=7124, words/sec=8093.53, time=0-00:14:10)
[asean.baseline.en-th] Epoch 16.2072: train_loss/word=1.938238 (steps=7145, words/sec=8852.40, time=0-00:14:11)
[asean.baseline.en-th] Epoch 16.2574: train_loss/word=1.982005 (steps=7169, words/sec=8423.04, time=0-00:14:12)
[asean.baseline.en-th] Epoch 16.3100: train_loss/word=1.964606 (steps=7193, words/sec=8051.43, time=0-00:14:13)
[asean.baseline.en-th] Epoch 16.3606: train_loss/word=1.922935 (steps=7215, words/sec=9079.60, time=0-00:14:14)
[asean.baseline.en-th] Epoch 16.4107: train_loss/word=2.022057 (steps=7236, words/sec=8669.08, time=0-00:14:15)
[asean.baseline.en-th] Epoch 16.4620: train_loss/word=1.990959 (steps=7262, words/sec=6804.82, time=0-00:14:16)
[asean.baseline.en-th] Epoch 16.5126: train_loss/word=2.007576 (steps=7284, words/sec=8953.01, time=0-00:14:17)
[asean.baseline.en-th] Epoch 16.5638: train_loss/word=1.995500 (steps=7306, words/sec=8342.80, time=0-00:14:18)
[asean.baseline.en-th] Epoch 16.6152: train_loss/word=2.010516 (steps=7326, words/sec=9143.16, time=0-00:14:19)
[asean.baseline.en-th] Epoch 16.6676: train_loss/word=2.036461 (steps=7351, words/sec=7956.45, time=0-00:14:20)
[asean.baseline.en-th] Epoch 16.7196: train_loss/word=1.970755 (steps=7374, words/sec=8670.86, time=0-00:14:21)
[asean.baseline.en-th] Epoch 16.7704: train_loss/word=2.001619 (steps=7399, words/sec=8450.96, time=0-00:14:22)
[asean.baseline.en-th] Epoch 16.8212: train_loss/word=2.031755 (steps=7422, words/sec=8153.79, time=0-00:14:23)
[asean.baseline.en-th] Epoch 16.8722: train_loss/word=1.993533 (steps=7445, words/sec=8426.77, time=0-00:14:24)
[asean.baseline.en-th] Epoch 16.9235: train_loss/word=2.058891 (steps=7467, words/sec=8463.09, time=0-00:14:25)
[asean.baseline.en-th] Epoch 16.9739: train_loss/word=1.997501 (steps=7488, words/sec=9377.99, time=0-00:14:25)
[asean.baseline.en-th] Epoch 17.0000: train_loss/word=2.016624 (steps=7499, words/sec=9094.91, time=0-00:14:26)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 17.0000 dev BLEU4: 0.3263862373105527, 0.564535/0.377197/0.264735/0.201306 (BP = 1.000000, ratio=1.03, hyp_len=7004, ref_len=6809) (time=0-00:14:52)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.328728
[asean.baseline.en-th]              dev auxiliary Loss: 4.292 (ref_len=6809)
             checkpoint took 0-00:00:25
  best dev score, writing out model
[asean.baseline.en-th] Epoch 17.0021: train_loss/word=1.813055 (steps=7500, words/sec=9515.61, time=0-00:14:57)
[asean.baseline.en-th] Epoch 17.0539: train_loss/word=1.915319 (steps=7524, words/sec=7826.52, time=0-00:14:58)
[asean.baseline.en-th] Epoch 17.1065: train_loss/word=1.941597 (steps=7547, words/sec=8188.13, time=0-00:14:59)
[asean.baseline.en-th] Epoch 17.1574: train_loss/word=1.870220 (steps=7569, words/sec=8549.55, time=0-00:15:00)
[asean.baseline.en-th] Epoch 17.2092: train_loss/word=1.908559 (steps=7596, words/sec=6955.75, time=0-00:15:02)
[asean.baseline.en-th] Epoch 17.2602: train_loss/word=1.939116 (steps=7620, words/sec=7852.07, time=0-00:15:03)
[asean.baseline.en-th] Epoch 17.3106: train_loss/word=1.934224 (steps=7640, words/sec=9072.58, time=0-00:15:04)
[asean.baseline.en-th] Epoch 17.3612: train_loss/word=1.963291 (steps=7664, words/sec=6940.56, time=0-00:15:05)
[asean.baseline.en-th] Epoch 17.4121: train_loss/word=1.956811 (steps=7687, words/sec=8100.39, time=0-00:15:06)
[asean.baseline.en-th] Epoch 17.4635: train_loss/word=1.915266 (steps=7709, words/sec=8838.43, time=0-00:15:07)
[asean.baseline.en-th] Epoch 17.5147: train_loss/word=1.941041 (steps=7730, words/sec=9026.60, time=0-00:15:07)
[asean.baseline.en-th] Epoch 17.5656: train_loss/word=1.953803 (steps=7751, words/sec=8644.15, time=0-00:15:08)
[asean.baseline.en-th] Epoch 17.6165: train_loss/word=1.932598 (steps=7773, words/sec=8750.50, time=0-00:15:09)
[asean.baseline.en-th] Epoch 17.6671: train_loss/word=1.959831 (steps=7795, words/sec=8502.54, time=0-00:15:10)
[asean.baseline.en-th] Epoch 17.7187: train_loss/word=1.945921 (steps=7818, words/sec=8251.38, time=0-00:15:11)
[asean.baseline.en-th] Epoch 17.7688: train_loss/word=1.940607 (steps=7838, words/sec=9125.44, time=0-00:15:12)
[asean.baseline.en-th] Epoch 17.8196: train_loss/word=1.947855 (steps=7857, words/sec=9921.36, time=0-00:15:12)
[asean.baseline.en-th] Epoch 17.8701: train_loss/word=1.973771 (steps=7878, words/sec=8263.59, time=0-00:15:13)
[asean.baseline.en-th] Epoch 17.9212: train_loss/word=2.022941 (steps=7904, words/sec=7462.93, time=0-00:15:15)
[asean.baseline.en-th] Epoch 17.9718: train_loss/word=2.010242 (steps=7926, words/sec=8074.18, time=0-00:15:16)
[asean.baseline.en-th] Epoch 18.0000: train_loss/word=1.999901 (steps=7939, words/sec=7551.01, time=0-00:15:16)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 18.0000 dev BLEU4: 0.3296978856206305, 0.557491/0.377218/0.270333/0.207843 (BP = 1.000000, ratio=1.04, hyp_len=7062, ref_len=6809) (time=0-00:15:43)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.326165
[asean.baseline.en-th]              dev auxiliary Loss: 4.299 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 18.0011: train_loss/word=1.960043 (steps=7940, words/sec=5101.32, time=0-00:15:48)
[asean.baseline.en-th] Epoch 18.0529: train_loss/word=1.864486 (steps=7962, words/sec=8772.67, time=0-00:15:49)
[asean.baseline.en-th] Epoch 18.1033: train_loss/word=1.884888 (steps=7983, words/sec=7973.24, time=0-00:15:50)
[asean.baseline.en-th] Epoch 18.1548: train_loss/word=1.865453 (steps=8006, words/sec=8368.76, time=0-00:15:51)
[asean.baseline.en-th] Epoch 18.2049: train_loss/word=1.876720 (steps=8028, words/sec=8249.87, time=0-00:15:52)
[asean.baseline.en-th] Epoch 18.2569: train_loss/word=1.874841 (steps=8050, words/sec=8998.68, time=0-00:15:53)
[asean.baseline.en-th] Epoch 18.3078: train_loss/word=1.899703 (steps=8073, words/sec=8246.33, time=0-00:15:54)
[asean.baseline.en-th] Epoch 18.3600: train_loss/word=1.889824 (steps=8098, words/sec=7717.83, time=0-00:15:55)
[asean.baseline.en-th] Epoch 18.4101: train_loss/word=1.887371 (steps=8117, words/sec=9785.81, time=0-00:15:56)
[asean.baseline.en-th] Epoch 18.4624: train_loss/word=1.870836 (steps=8139, words/sec=9155.13, time=0-00:15:57)
[asean.baseline.en-th] Epoch 18.5125: train_loss/word=1.926123 (steps=8164, words/sec=7743.94, time=0-00:15:58)
[asean.baseline.en-th] Epoch 18.5634: train_loss/word=1.929173 (steps=8185, words/sec=8593.43, time=0-00:15:59)
[asean.baseline.en-th] Epoch 18.6142: train_loss/word=1.913765 (steps=8208, words/sec=7846.38, time=0-00:16:00)
[asean.baseline.en-th] Epoch 18.6672: train_loss/word=1.965244 (steps=8233, words/sec=7990.59, time=0-00:16:01)
[asean.baseline.en-th] Epoch 18.7181: train_loss/word=1.918216 (steps=8255, words/sec=8741.03, time=0-00:16:01)
[asean.baseline.en-th] Epoch 18.7687: train_loss/word=1.949822 (steps=8279, words/sec=7796.34, time=0-00:16:03)
[asean.baseline.en-th] Epoch 18.8207: train_loss/word=1.939991 (steps=8300, words/sec=8931.34, time=0-00:16:03)
[asean.baseline.en-th] Epoch 18.8721: train_loss/word=1.896153 (steps=8323, words/sec=8262.39, time=0-00:16:04)
[asean.baseline.en-th] Epoch 18.9235: train_loss/word=1.936092 (steps=8343, words/sec=9170.94, time=0-00:16:05)
[asean.baseline.en-th] Epoch 18.9736: train_loss/word=1.909385 (steps=8367, words/sec=8119.57, time=0-00:16:06)
[asean.baseline.en-th] Epoch 19.0000: train_loss/word=1.919383 (steps=8380, words/sec=7823.72, time=0-00:16:07)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 19.0000 dev BLEU4: 0.3221998529019082, 0.553774/0.373690/0.260101/0.200223 (BP = 1.000000, ratio=1.06, hyp_len=7234, ref_len=6809) (time=0-00:16:34)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.326913
[asean.baseline.en-th]              dev auxiliary Loss: 4.310 (ref_len=6809)
             checkpoint took 0-00:00:27
[asean.baseline.en-th] Epoch 19.0037: train_loss/word=1.833616 (steps=8381, words/sec=13257.50, time=0-00:16:34)
[asean.baseline.en-th] Epoch 19.0543: train_loss/word=1.867795 (steps=8400, words/sec=9445.47, time=0-00:16:35)
[asean.baseline.en-th] Epoch 19.1049: train_loss/word=1.825882 (steps=8422, words/sec=8566.39, time=0-00:16:36)
[asean.baseline.en-th] Epoch 19.1551: train_loss/word=1.872012 (steps=8448, words/sec=6995.17, time=0-00:16:37)
[asean.baseline.en-th] Epoch 19.2056: train_loss/word=1.838269 (steps=8472, words/sec=8515.92, time=0-00:16:38)
[asean.baseline.en-th] Epoch 19.2565: train_loss/word=1.807573 (steps=8493, words/sec=9188.42, time=0-00:16:39)
[asean.baseline.en-th] Epoch 19.3082: train_loss/word=1.876155 (steps=8517, words/sec=8252.69, time=0-00:16:40)
[asean.baseline.en-th] Epoch 19.3610: train_loss/word=1.852004 (steps=8540, words/sec=8709.75, time=0-00:16:41)
[asean.baseline.en-th] Epoch 19.4140: train_loss/word=1.868678 (steps=8561, words/sec=9236.12, time=0-00:16:42)
[asean.baseline.en-th] Epoch 19.4658: train_loss/word=1.853693 (steps=8586, words/sec=8389.42, time=0-00:16:43)
[asean.baseline.en-th] Epoch 19.5168: train_loss/word=1.849159 (steps=8608, words/sec=8664.48, time=0-00:16:43)
[asean.baseline.en-th] Epoch 19.5672: train_loss/word=1.897804 (steps=8631, words/sec=7377.88, time=0-00:16:45)
[asean.baseline.en-th] Epoch 19.6177: train_loss/word=1.893831 (steps=8656, words/sec=7018.89, time=0-00:16:46)
[asean.baseline.en-th] Epoch 19.6692: train_loss/word=1.861807 (steps=8679, words/sec=8376.76, time=0-00:16:47)
[asean.baseline.en-th] Epoch 19.7221: train_loss/word=1.876281 (steps=8701, words/sec=9210.99, time=0-00:16:48)
[asean.baseline.en-th] Epoch 19.7743: train_loss/word=1.928121 (steps=8723, words/sec=7755.73, time=0-00:16:49)
[asean.baseline.en-th] Epoch 19.8256: train_loss/word=1.886084 (steps=8742, words/sec=9663.57, time=0-00:16:49)
[asean.baseline.en-th] Epoch 19.8771: train_loss/word=1.864589 (steps=8766, words/sec=8876.03, time=0-00:16:50)
[asean.baseline.en-th] Epoch 19.9272: train_loss/word=1.890814 (steps=8790, words/sec=8547.53, time=0-00:16:51)
[asean.baseline.en-th] Epoch 19.9786: train_loss/word=1.914923 (steps=8812, words/sec=8671.83, time=0-00:16:52)
[asean.baseline.en-th] Epoch 20.0000: train_loss/word=1.868632 (steps=8820, words/sec=10025.84, time=0-00:16:52)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 20.0000 dev BLEU4: 0.3216448926879766, 0.552526/0.372134/0.261851/0.198792 (BP = 1.000000, ratio=1.06, hyp_len=7225, ref_len=6809) (time=0-00:17:19)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.326048
[asean.baseline.en-th]              dev auxiliary Loss: 4.306 (ref_len=6809)
             checkpoint took 0-00:00:26
  new learning rate: 0.5
[asean.baseline.en-th] Epoch 20.0016: train_loss/word=1.810870 (steps=8821, words/sec=7023.44, time=0-00:17:19)
[asean.baseline.en-th] Epoch 20.0530: train_loss/word=1.830802 (steps=8846, words/sec=7323.61, time=0-00:17:20)
[asean.baseline.en-th] Epoch 20.1034: train_loss/word=1.803973 (steps=8867, words/sec=8746.27, time=0-00:17:21)
[asean.baseline.en-th] Epoch 20.1543: train_loss/word=1.776801 (steps=8888, words/sec=8683.40, time=0-00:17:22)
[asean.baseline.en-th] Epoch 20.2064: train_loss/word=1.764385 (steps=8909, words/sec=9161.51, time=0-00:17:23)
[asean.baseline.en-th] Epoch 20.2580: train_loss/word=1.773354 (steps=8930, words/sec=9395.24, time=0-00:17:24)
[asean.baseline.en-th] Epoch 20.3087: train_loss/word=1.760287 (steps=8955, words/sec=7921.08, time=0-00:17:25)
[asean.baseline.en-th] Epoch 20.3599: train_loss/word=1.792559 (steps=8980, words/sec=7550.39, time=0-00:17:26)
[asean.baseline.en-th] Epoch 20.4103: train_loss/word=1.779857 (steps=9005, words/sec=7790.28, time=0-00:17:27)
[asean.baseline.en-th] Epoch 20.4625: train_loss/word=1.759978 (steps=9027, words/sec=9156.07, time=0-00:17:28)
[asean.baseline.en-th] Epoch 20.5127: train_loss/word=1.768979 (steps=9051, words/sec=8164.41, time=0-00:17:29)
[asean.baseline.en-th] Epoch 20.5634: train_loss/word=1.747470 (steps=9073, words/sec=9393.50, time=0-00:17:30)
[asean.baseline.en-th] Epoch 20.6136: train_loss/word=1.752903 (steps=9095, words/sec=8894.92, time=0-00:17:31)
[asean.baseline.en-th] Epoch 20.6640: train_loss/word=1.758601 (steps=9119, words/sec=7663.38, time=0-00:17:32)
[asean.baseline.en-th] Epoch 20.7156: train_loss/word=1.788661 (steps=9142, words/sec=8360.40, time=0-00:17:33)
[asean.baseline.en-th] Epoch 20.7664: train_loss/word=1.785640 (steps=9165, words/sec=8249.98, time=0-00:17:34)
[asean.baseline.en-th] Epoch 20.8173: train_loss/word=1.741040 (steps=9188, words/sec=8487.21, time=0-00:17:35)
[asean.baseline.en-th] Epoch 20.8688: train_loss/word=1.763418 (steps=9211, words/sec=8902.19, time=0-00:17:35)
[asean.baseline.en-th] Epoch 20.9192: train_loss/word=1.806298 (steps=9229, words/sec=9506.21, time=0-00:17:36)
[asean.baseline.en-th] Epoch 20.9700: train_loss/word=1.756369 (steps=9249, words/sec=9766.17, time=0-00:17:37)
[asean.baseline.en-th] Epoch 21.0000: train_loss/word=1.798991 (steps=9262, words/sec=7769.29, time=0-00:17:37)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 21.0000 dev BLEU4: 0.3308879750477376, 0.553337/0.377806/0.271450/0.211240 (BP = 1.000000, ratio=1.07, hyp_len=7312, ref_len=6809) (time=0-00:18:04)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.334720
[asean.baseline.en-th]              dev auxiliary Loss: 4.282 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 21.0011: train_loss/word=1.750826 (steps=9263, words/sec=4381.63, time=0-00:18:10)
[asean.baseline.en-th] Epoch 21.0524: train_loss/word=1.674472 (steps=9286, words/sec=9111.41, time=0-00:18:11)
[asean.baseline.en-th] Epoch 21.1040: train_loss/word=1.683415 (steps=9309, words/sec=8825.38, time=0-00:18:12)
[asean.baseline.en-th] Epoch 21.1548: train_loss/word=1.715634 (steps=9331, words/sec=8487.22, time=0-00:18:13)
[asean.baseline.en-th] Epoch 21.2073: train_loss/word=1.713118 (steps=9354, words/sec=8401.59, time=0-00:18:14)
[asean.baseline.en-th] Epoch 21.2586: train_loss/word=1.718431 (steps=9381, words/sec=7055.78, time=0-00:18:15)
[asean.baseline.en-th] Epoch 21.3096: train_loss/word=1.707261 (steps=9405, words/sec=8460.02, time=0-00:18:16)
[asean.baseline.en-th] Epoch 21.3599: train_loss/word=1.727736 (steps=9427, words/sec=8575.26, time=0-00:18:17)
[asean.baseline.en-th] Epoch 21.4116: train_loss/word=1.748482 (steps=9446, words/sec=9683.85, time=0-00:18:18)
[asean.baseline.en-th] Epoch 21.4631: train_loss/word=1.712647 (steps=9467, words/sec=9182.93, time=0-00:18:18)
[asean.baseline.en-th] Epoch 21.5139: train_loss/word=1.712183 (steps=9490, words/sec=8708.56, time=0-00:18:19)
[asean.baseline.en-th] Epoch 21.5639: train_loss/word=1.742004 (steps=9514, words/sec=7757.67, time=0-00:18:21)
[asean.baseline.en-th] Epoch 21.6155: train_loss/word=1.705898 (steps=9540, words/sec=7863.78, time=0-00:18:22)
[asean.baseline.en-th] Epoch 21.6669: train_loss/word=1.734583 (steps=9561, words/sec=8741.17, time=0-00:18:22)
[asean.baseline.en-th] Epoch 21.7183: train_loss/word=1.725419 (steps=9585, words/sec=8496.97, time=0-00:18:23)
[asean.baseline.en-th] Epoch 21.7704: train_loss/word=1.712146 (steps=9610, words/sec=7662.88, time=0-00:18:25)
[asean.baseline.en-th] Epoch 21.8222: train_loss/word=1.719354 (steps=9631, words/sec=9733.29, time=0-00:18:25)
[asean.baseline.en-th] Epoch 21.8732: train_loss/word=1.757520 (steps=9652, words/sec=9223.68, time=0-00:18:26)
[asean.baseline.en-th] Epoch 21.9246: train_loss/word=1.701819 (steps=9676, words/sec=8872.87, time=0-00:18:27)
[asean.baseline.en-th] Epoch 21.9763: train_loss/word=1.787725 (steps=9695, words/sec=8754.58, time=0-00:18:28)
[asean.baseline.en-th] Epoch 22.0000: train_loss/word=1.864824 (steps=9703, words/sec=8152.11, time=0-00:18:28)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 22.0000 dev BLEU4: 0.3370160624188604, 0.558852/0.383695/0.277851/0.216525 (BP = 1.000000, ratio=1.06, hyp_len=7213, ref_len=6809) (time=0-00:18:55)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.336082
[asean.baseline.en-th]              dev auxiliary Loss: 4.289 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
[asean.baseline.en-th] Epoch 22.0030: train_loss/word=1.744714 (steps=9704, words/sec=10308.69, time=0-00:19:01)
[asean.baseline.en-th] Epoch 22.0540: train_loss/word=1.647550 (steps=9730, words/sec=8126.46, time=0-00:19:02)
[asean.baseline.en-th] Epoch 22.1054: train_loss/word=1.676827 (steps=9754, words/sec=8417.98, time=0-00:19:03)
[asean.baseline.en-th] Epoch 22.1556: train_loss/word=1.679117 (steps=9775, words/sec=9118.75, time=0-00:19:04)
[asean.baseline.en-th] Epoch 22.2070: train_loss/word=1.709569 (steps=9797, words/sec=8032.64, time=0-00:19:05)
[asean.baseline.en-th] Epoch 22.2581: train_loss/word=1.694374 (steps=9821, words/sec=8316.37, time=0-00:19:06)
[asean.baseline.en-th] Epoch 22.3094: train_loss/word=1.680497 (steps=9845, words/sec=7993.15, time=0-00:19:07)
[asean.baseline.en-th] Epoch 22.3597: train_loss/word=1.722141 (steps=9868, words/sec=7902.38, time=0-00:19:08)
[asean.baseline.en-th] Epoch 22.4117: train_loss/word=1.674602 (steps=9890, words/sec=9351.80, time=0-00:19:08)
[asean.baseline.en-th] Epoch 22.4620: train_loss/word=1.696557 (steps=9911, words/sec=7766.61, time=0-00:19:09)
[asean.baseline.en-th] Epoch 22.5127: train_loss/word=1.700790 (steps=9933, words/sec=8584.07, time=0-00:19:10)
[asean.baseline.en-th] Epoch 22.5643: train_loss/word=1.693332 (steps=9956, words/sec=8756.16, time=0-00:19:11)
[asean.baseline.en-th] Epoch 22.6146: train_loss/word=1.692256 (steps=9980, words/sec=7950.54, time=0-00:19:12)
[asean.baseline.en-th] Epoch 22.6662: train_loss/word=1.687214 (steps=10004, words/sec=8405.09, time=0-00:19:13)
[asean.baseline.en-th] Epoch 22.7174: train_loss/word=1.705120 (steps=10026, words/sec=8581.44, time=0-00:19:14)
[asean.baseline.en-th] Epoch 22.7683: train_loss/word=1.743408 (steps=10047, words/sec=8468.46, time=0-00:19:15)
[asean.baseline.en-th] Epoch 22.8210: train_loss/word=1.709280 (steps=10068, words/sec=9513.54, time=0-00:19:16)
[asean.baseline.en-th] Epoch 22.8715: train_loss/word=1.709867 (steps=10092, words/sec=7733.86, time=0-00:19:17)
[asean.baseline.en-th] Epoch 22.9227: train_loss/word=1.721754 (steps=10116, words/sec=8061.74, time=0-00:19:18)
[asean.baseline.en-th] Epoch 22.9728: train_loss/word=1.754292 (steps=10136, words/sec=7818.27, time=0-00:19:19)
[asean.baseline.en-th] Epoch 23.0000: train_loss/word=1.797878 (steps=10145, words/sec=9741.21, time=0-00:19:19)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 23.0000 dev BLEU4: 0.33341275259338493, 0.557447/0.384714/0.273133/0.210967 (BP = 1.000000, ratio=1.07, hyp_len=7285, ref_len=6809) (time=0-00:19:46)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.335724
[asean.baseline.en-th]              dev auxiliary Loss: 4.308 (ref_len=6809)
             checkpoint took 0-00:00:26
  new learning rate: 0.25
[asean.baseline.en-th] Epoch 23.0015: train_loss/word=1.629682 (steps=10146, words/sec=8056.13, time=0-00:19:46)
[asean.baseline.en-th] Epoch 23.0530: train_loss/word=1.678128 (steps=10167, words/sec=8408.71, time=0-00:19:47)
[asean.baseline.en-th] Epoch 23.1037: train_loss/word=1.641625 (steps=10190, words/sec=8119.56, time=0-00:19:48)
[asean.baseline.en-th] Epoch 23.1583: train_loss/word=1.653188 (steps=10215, words/sec=7655.13, time=0-00:19:49)
[asean.baseline.en-th] Epoch 23.2086: train_loss/word=1.660002 (steps=10237, words/sec=8798.14, time=0-00:19:50)
[asean.baseline.en-th] Epoch 23.2603: train_loss/word=1.653632 (steps=10261, words/sec=8029.34, time=0-00:19:51)
[asean.baseline.en-th] Epoch 23.3114: train_loss/word=1.666757 (steps=10283, words/sec=8616.65, time=0-00:19:52)
[asean.baseline.en-th] Epoch 23.3619: train_loss/word=1.680437 (steps=10306, words/sec=7145.95, time=0-00:19:53)
[asean.baseline.en-th] Epoch 23.4143: train_loss/word=1.643204 (steps=10329, words/sec=9058.92, time=0-00:19:54)
[asean.baseline.en-th] Epoch 23.4657: train_loss/word=1.680778 (steps=10351, words/sec=8087.19, time=0-00:19:55)
[asean.baseline.en-th] Epoch 23.5159: train_loss/word=1.646906 (steps=10376, words/sec=8106.95, time=0-00:19:56)
[asean.baseline.en-th] Epoch 23.5662: train_loss/word=1.629419 (steps=10400, words/sec=8503.23, time=0-00:19:57)
[asean.baseline.en-th] Epoch 23.6171: train_loss/word=1.678464 (steps=10419, words/sec=10213.85, time=0-00:19:57)
[asean.baseline.en-th] Epoch 23.6675: train_loss/word=1.637492 (steps=10445, words/sec=8048.14, time=0-00:19:59)
[asean.baseline.en-th] Epoch 23.7192: train_loss/word=1.662382 (steps=10467, words/sec=8797.49, time=0-00:19:59)
[asean.baseline.en-th] Epoch 23.7697: train_loss/word=1.685001 (steps=10487, words/sec=9392.64, time=0-00:20:00)
[asean.baseline.en-th] Epoch 23.8209: train_loss/word=1.674234 (steps=10511, words/sec=7870.98, time=0-00:20:01)
[asean.baseline.en-th] Epoch 23.8724: train_loss/word=1.688923 (steps=10531, words/sec=8821.51, time=0-00:20:02)
[asean.baseline.en-th] Epoch 23.9243: train_loss/word=1.676270 (steps=10552, words/sec=9208.24, time=0-00:20:03)
[asean.baseline.en-th] Epoch 23.9766: train_loss/word=1.660561 (steps=10574, words/sec=8893.35, time=0-00:20:04)
[asean.baseline.en-th] Epoch 24.0000: train_loss/word=1.667304 (steps=10586, words/sec=7276.41, time=0-00:20:04)
> Checkpoint [asean.baseline.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[asean.baseline.en-th] Epoch 24.0000 dev BLEU4: 0.33681661848028566, 0.559967/0.384923/0.277416/0.215232 (BP = 1.000000, ratio=1.07, hyp_len=7279, ref_len=6809) (time=0-00:20:31)
[asean.baseline.en-th]              dev auxiliary GLEU: 0.338838
[asean.baseline.en-th]              dev auxiliary Loss: 4.298 (ref_len=6809)
             checkpoint took 0-00:00:27
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.th
Performing inference on ./data/test.en and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.en-th          | BLEU4: 0.3370160624188604, 0.558852/0.383695/0.277851/0.216525 (BP = 1.000000, ratio=1.06, hyp_len=7213, ref_len=6809)
                              | GLEU: 0.336082
                              | WER: 64.39% ( C/S/I/D: 3869/1900/1444/1040; hyp_len=7213, ref_len=6809 )
                              | CER: 50.32% ( C/S/I/D: 18747/7580/3439/4487; hyp_len=29766, ref_len=30814 )
                              | BLEU4: 0.3580679884400774, 0.595108/0.408515/0.295922/0.228497 (BP = 1.000000, ratio=1.02, hyp_len=7318, ref_len=7169)
                              | GLEU: 0.357811
                              | WER: 58.77% ( C/S/I/D: 4169/1936/1213/1064; hyp_len=7318, ref_len=7169 )
                              | CER: 47.90% ( C/S/I/D: 19191/7059/3019/4791; hyp_len=29269, ref_len=31041 )

```

## Training for th-en, word unit (Baseline)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline$ time xnmt --backend torch --gpu ./config.baseline.th-en-word.yaml | tee baseline.th-en.log1
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 21:47:39
=> Running asean.baseline.th-en
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 20659460
> Training
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 0.0512: train_loss/word=9.041227 (steps=23, words/sec=5411.19, time=0-00:00:04)
[asean.baseline.th-en] Epoch 0.1028: train_loss/word=7.953733 (steps=46, words/sec=8096.36, time=0-00:00:05)
[asean.baseline.th-en] Epoch 0.1529: train_loss/word=7.638606 (steps=70, words/sec=8097.83, time=0-00:00:06)
[asean.baseline.th-en] Epoch 0.2036: train_loss/word=7.542161 (steps=91, words/sec=9138.26, time=0-00:00:07)
[asean.baseline.th-en] Epoch 0.2540: train_loss/word=7.515797 (steps=113, words/sec=8402.10, time=0-00:00:08)
[asean.baseline.th-en] Epoch 0.3052: train_loss/word=7.435911 (steps=136, words/sec=8487.40, time=0-00:00:09)
[asean.baseline.th-en] Epoch 0.3559: train_loss/word=7.273364 (steps=160, words/sec=7434.36, time=0-00:00:10)
[asean.baseline.th-en] Epoch 0.4092: train_loss/word=7.141827 (steps=186, words/sec=6772.83, time=0-00:00:11)
[asean.baseline.th-en] Epoch 0.4601: train_loss/word=7.096162 (steps=210, words/sec=7947.94, time=0-00:00:12)
[asean.baseline.th-en] Epoch 0.5125: train_loss/word=7.120195 (steps=236, words/sec=7389.68, time=0-00:00:13)
[asean.baseline.th-en] Epoch 0.5632: train_loss/word=6.901426 (steps=259, words/sec=8532.19, time=0-00:00:14)
[asean.baseline.th-en] Epoch 0.6154: train_loss/word=6.828043 (steps=285, words/sec=7386.84, time=0-00:00:16)
[asean.baseline.th-en] Epoch 0.6656: train_loss/word=6.878164 (steps=309, words/sec=7883.72, time=0-00:00:17)
[asean.baseline.th-en] Epoch 0.7171: train_loss/word=6.716918 (steps=333, words/sec=8011.66, time=0-00:00:18)
[asean.baseline.th-en] Epoch 0.7681: train_loss/word=6.608228 (steps=354, words/sec=9009.36, time=0-00:00:18)
[asean.baseline.th-en] Epoch 0.8194: train_loss/word=6.539059 (steps=377, words/sec=8468.60, time=0-00:00:19)
[asean.baseline.th-en] Epoch 0.8702: train_loss/word=6.590628 (steps=400, words/sec=8464.24, time=0-00:00:20)
[asean.baseline.th-en] Epoch 0.9205: train_loss/word=6.441869 (steps=422, words/sec=9095.89, time=0-00:00:21)
[asean.baseline.th-en] Epoch 0.9707: train_loss/word=6.282051 (steps=443, words/sec=9126.34, time=0-00:00:22)
[asean.baseline.th-en] Epoch 1.0000: train_loss/word=6.456410 (steps=456, words/sec=8058.90, time=0-00:00:23)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 1.0000 dev BLEU4: 0.005577474375100524, 0.051017/0.011849/0.003208/0.000499 (BP = 1.000000, ratio=2.90, hyp_len=21032, ref_len=7245) (time=0-00:01:48)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.017076
[asean.baseline.th-en]              dev auxiliary Loss: 6.307 (ref_len=7245)
             checkpoint took 0-00:01:25
  best dev score, writing out model
[asean.baseline.th-en] Epoch 1.0010: train_loss/word=6.947172 (steps=457, words/sec=4964.82, time=0-00:02:06)
[asean.baseline.th-en] Epoch 1.0527: train_loss/word=6.269581 (steps=481, words/sec=7310.43, time=0-00:02:08)
[asean.baseline.th-en] Epoch 1.1030: train_loss/word=6.092869 (steps=502, words/sec=8979.33, time=0-00:02:08)
[asean.baseline.th-en] Epoch 1.1546: train_loss/word=6.089249 (steps=525, words/sec=8254.48, time=0-00:02:09)
[asean.baseline.th-en] Epoch 1.2076: train_loss/word=6.074701 (steps=551, words/sec=7642.11, time=0-00:02:11)
[asean.baseline.th-en] Epoch 1.2579: train_loss/word=6.057353 (steps=574, words/sec=8150.91, time=0-00:02:12)
[asean.baseline.th-en] Epoch 1.3092: train_loss/word=6.104577 (steps=598, words/sec=7648.54, time=0-00:02:13)
[asean.baseline.th-en] Epoch 1.3602: train_loss/word=5.910841 (steps=620, words/sec=9090.77, time=0-00:02:14)
[asean.baseline.th-en] Epoch 1.4109: train_loss/word=5.912568 (steps=643, words/sec=8074.81, time=0-00:02:15)
[asean.baseline.th-en] Epoch 1.4615: train_loss/word=5.778236 (steps=665, words/sec=8704.33, time=0-00:02:15)
[asean.baseline.th-en] Epoch 1.5124: train_loss/word=5.817820 (steps=688, words/sec=7982.90, time=0-00:02:16)
[asean.baseline.th-en] Epoch 1.5641: train_loss/word=5.900090 (steps=712, words/sec=7957.27, time=0-00:02:17)
[asean.baseline.th-en] Epoch 1.6142: train_loss/word=5.906331 (steps=736, words/sec=6961.85, time=0-00:02:19)
[asean.baseline.th-en] Epoch 1.6672: train_loss/word=5.794959 (steps=760, words/sec=8273.57, time=0-00:02:20)
[asean.baseline.th-en] Epoch 1.7179: train_loss/word=5.714368 (steps=782, words/sec=7963.21, time=0-00:02:20)
[asean.baseline.th-en] Epoch 1.7681: train_loss/word=5.744250 (steps=806, words/sec=8413.02, time=0-00:02:21)
[asean.baseline.th-en] Epoch 1.8185: train_loss/word=5.714598 (steps=829, words/sec=8324.84, time=0-00:02:22)
[asean.baseline.th-en] Epoch 1.8688: train_loss/word=5.650063 (steps=852, words/sec=8324.13, time=0-00:02:23)
[asean.baseline.th-en] Epoch 1.9191: train_loss/word=5.922932 (steps=877, words/sec=6864.79, time=0-00:02:25)
[asean.baseline.th-en] Epoch 1.9707: train_loss/word=5.717003 (steps=900, words/sec=8124.01, time=0-00:02:26)
[asean.baseline.th-en] Epoch 2.0000: train_loss/word=5.558463 (steps=913, words/sec=9127.20, time=0-00:02:26)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 2.0000 dev BLEU4: 0.03388102268083235, 0.201654/0.063040/0.021280/0.004871 (BP = 1.000000, ratio=1.10, hyp_len=7979, ref_len=7245) (time=0-00:03:02)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.074845
[asean.baseline.th-en]              dev auxiliary Loss: 5.689 (ref_len=7245)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[asean.baseline.th-en] Epoch 2.0021: train_loss/word=5.881651 (steps=914, words/sec=5599.05, time=0-00:03:08)
[asean.baseline.th-en] Epoch 2.0533: train_loss/word=5.503037 (steps=939, words/sec=7191.35, time=0-00:03:09)
[asean.baseline.th-en] Epoch 2.1041: train_loss/word=5.407206 (steps=963, words/sec=7437.45, time=0-00:03:10)
[asean.baseline.th-en] Epoch 2.1565: train_loss/word=5.345283 (steps=986, words/sec=8696.61, time=0-00:03:11)
[asean.baseline.th-en] Epoch 2.2075: train_loss/word=5.234749 (steps=1010, words/sec=7955.26, time=0-00:03:12)
[asean.baseline.th-en] Epoch 2.2582: train_loss/word=5.320360 (steps=1035, words/sec=6910.01, time=0-00:03:13)
[asean.baseline.th-en] Epoch 2.3098: train_loss/word=5.188320 (steps=1059, words/sec=7420.80, time=0-00:03:14)
[asean.baseline.th-en] Epoch 2.3612: train_loss/word=5.082039 (steps=1080, words/sec=9303.72, time=0-00:03:15)
[asean.baseline.th-en] Epoch 2.4114: train_loss/word=5.133915 (steps=1102, words/sec=7914.60, time=0-00:03:16)
[asean.baseline.th-en] Epoch 2.4626: train_loss/word=5.365956 (steps=1124, words/sec=8412.92, time=0-00:03:17)
[asean.baseline.th-en] Epoch 2.5136: train_loss/word=5.272347 (steps=1148, words/sec=8148.30, time=0-00:03:18)
[asean.baseline.th-en] Epoch 2.5645: train_loss/word=5.266895 (steps=1171, words/sec=8018.79, time=0-00:03:19)
[asean.baseline.th-en] Epoch 2.6152: train_loss/word=5.207582 (steps=1196, words/sec=7059.82, time=0-00:03:20)
[asean.baseline.th-en] Epoch 2.6663: train_loss/word=5.028013 (steps=1219, words/sec=8612.95, time=0-00:03:21)
[asean.baseline.th-en] Epoch 2.7182: train_loss/word=5.103695 (steps=1244, words/sec=7393.55, time=0-00:03:22)
[asean.baseline.th-en] Epoch 2.7693: train_loss/word=5.180906 (steps=1268, words/sec=7481.88, time=0-00:03:23)
[asean.baseline.th-en] Epoch 2.8209: train_loss/word=5.253600 (steps=1292, words/sec=7710.17, time=0-00:03:25)
[asean.baseline.th-en] Epoch 2.8726: train_loss/word=4.982751 (steps=1314, words/sec=8084.74, time=0-00:03:25)
[asean.baseline.th-en] Epoch 2.9233: train_loss/word=5.063516 (steps=1338, words/sec=8501.12, time=0-00:03:26)
[asean.baseline.th-en] Epoch 2.9763: train_loss/word=5.038360 (steps=1362, words/sec=8128.99, time=0-00:03:28)
[asean.baseline.th-en] Epoch 3.0000: train_loss/word=5.095595 (steps=1374, words/sec=7933.04, time=0-00:03:28)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 3.0000 dev BLEU4: 0.06436098606122566, 0.264441/0.095596/0.041879/0.016208 (BP = 1.000000, ratio=1.04, hyp_len=7548, ref_len=7245) (time=0-00:04:01)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.105449
[asean.baseline.th-en]              dev auxiliary Loss: 5.362 (ref_len=7245)
             checkpoint took 0-00:00:32
  best dev score, writing out model
[asean.baseline.th-en] Epoch 3.0026: train_loss/word=4.444925 (steps=1375, words/sec=10273.18, time=0-00:04:06)
[asean.baseline.th-en] Epoch 3.0536: train_loss/word=4.663537 (steps=1399, words/sec=8198.69, time=0-00:04:07)
[asean.baseline.th-en] Epoch 3.1038: train_loss/word=4.734108 (steps=1421, words/sec=8493.61, time=0-00:04:08)
[asean.baseline.th-en] Epoch 3.1545: train_loss/word=4.714766 (steps=1444, words/sec=8334.18, time=0-00:04:09)
[asean.baseline.th-en] Epoch 3.2061: train_loss/word=4.832736 (steps=1468, words/sec=7981.74, time=0-00:04:10)
[asean.baseline.th-en] Epoch 3.2564: train_loss/word=4.719988 (steps=1493, words/sec=8494.87, time=0-00:04:11)
[asean.baseline.th-en] Epoch 3.3067: train_loss/word=4.573088 (steps=1516, words/sec=7938.25, time=0-00:04:12)
[asean.baseline.th-en] Epoch 3.3576: train_loss/word=4.643589 (steps=1539, words/sec=7564.22, time=0-00:04:13)
[asean.baseline.th-en] Epoch 3.4099: train_loss/word=4.704369 (steps=1564, words/sec=8068.46, time=0-00:04:14)
[asean.baseline.th-en] Epoch 3.4613: train_loss/word=4.550186 (steps=1588, words/sec=7822.89, time=0-00:04:15)
[asean.baseline.th-en] Epoch 3.5126: train_loss/word=4.520438 (steps=1610, words/sec=8876.38, time=0-00:04:16)
[asean.baseline.th-en] Epoch 3.5652: train_loss/word=4.677894 (steps=1633, words/sec=8468.76, time=0-00:04:17)
[asean.baseline.th-en] Epoch 3.6160: train_loss/word=4.672296 (steps=1656, words/sec=8200.22, time=0-00:04:18)
[asean.baseline.th-en] Epoch 3.6681: train_loss/word=4.634925 (steps=1678, words/sec=9207.60, time=0-00:04:19)
[asean.baseline.th-en] Epoch 3.7192: train_loss/word=4.758535 (steps=1702, words/sec=7921.59, time=0-00:04:20)
[asean.baseline.th-en] Epoch 3.7701: train_loss/word=4.590686 (steps=1725, words/sec=8557.09, time=0-00:04:21)
[asean.baseline.th-en] Epoch 3.8208: train_loss/word=4.613171 (steps=1748, words/sec=8894.81, time=0-00:04:22)
[asean.baseline.th-en] Epoch 3.8715: train_loss/word=4.544312 (steps=1770, words/sec=8296.68, time=0-00:04:23)
[asean.baseline.th-en] Epoch 3.9220: train_loss/word=4.741644 (steps=1796, words/sec=6637.05, time=0-00:04:24)
[asean.baseline.th-en] Epoch 3.9721: train_loss/word=4.641303 (steps=1819, words/sec=8433.28, time=0-00:04:25)
[asean.baseline.th-en] Epoch 4.0000: train_loss/word=4.829526 (steps=1833, words/sec=7388.71, time=0-00:04:26)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 4.0000 dev BLEU4: 0.09451787497260426, 0.295704/0.129175/0.065328/0.031983 (BP = 1.000000, ratio=1.02, hyp_len=7379, ref_len=7245) (time=0-00:04:56)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.127802
[asean.baseline.th-en]              dev auxiliary Loss: 5.121 (ref_len=7245)
             checkpoint took 0-00:00:30
  best dev score, writing out model
[asean.baseline.th-en] Epoch 4.0024: train_loss/word=3.779757 (steps=1834, words/sec=6131.60, time=0-00:05:02)
[asean.baseline.th-en] Epoch 4.0527: train_loss/word=4.092020 (steps=1857, words/sec=8806.50, time=0-00:05:03)
[asean.baseline.th-en] Epoch 4.1041: train_loss/word=4.052028 (steps=1880, words/sec=8355.80, time=0-00:05:04)
[asean.baseline.th-en] Epoch 4.1548: train_loss/word=4.183057 (steps=1902, words/sec=8202.61, time=0-00:05:05)
[asean.baseline.th-en] Epoch 4.2073: train_loss/word=4.136158 (steps=1926, words/sec=7781.14, time=0-00:05:06)
[asean.baseline.th-en] Epoch 4.2583: train_loss/word=4.371499 (steps=1950, words/sec=7468.92, time=0-00:05:07)
[asean.baseline.th-en] Epoch 4.3094: train_loss/word=4.319290 (steps=1974, words/sec=8306.87, time=0-00:05:08)
[asean.baseline.th-en] Epoch 4.3599: train_loss/word=4.132676 (steps=1997, words/sec=7992.22, time=0-00:05:09)
[asean.baseline.th-en] Epoch 4.4120: train_loss/word=4.231389 (steps=2021, words/sec=8796.14, time=0-00:05:10)
[asean.baseline.th-en] Epoch 4.4622: train_loss/word=4.315262 (steps=2044, words/sec=8490.54, time=0-00:05:11)
[asean.baseline.th-en] Epoch 4.5135: train_loss/word=4.278158 (steps=2066, words/sec=8106.34, time=0-00:05:12)
[asean.baseline.th-en] Epoch 4.5652: train_loss/word=4.168122 (steps=2088, words/sec=8658.41, time=0-00:05:13)
[asean.baseline.th-en] Epoch 4.6155: train_loss/word=4.205282 (steps=2111, words/sec=8034.00, time=0-00:05:14)
[asean.baseline.th-en] Epoch 4.6660: train_loss/word=4.280810 (steps=2135, words/sec=8243.25, time=0-00:05:15)
[asean.baseline.th-en] Epoch 4.7170: train_loss/word=4.059815 (steps=2156, words/sec=10000.33, time=0-00:05:16)
[asean.baseline.th-en] Epoch 4.7676: train_loss/word=4.213059 (steps=2180, words/sec=8194.03, time=0-00:05:17)
[asean.baseline.th-en] Epoch 4.8177: train_loss/word=4.258697 (steps=2203, words/sec=8175.98, time=0-00:05:18)
[asean.baseline.th-en] Epoch 4.8692: train_loss/word=4.263851 (steps=2227, words/sec=8435.33, time=0-00:05:19)
[asean.baseline.th-en] Epoch 4.9194: train_loss/word=4.229970 (steps=2251, words/sec=8125.45, time=0-00:05:20)
[asean.baseline.th-en] Epoch 4.9696: train_loss/word=4.244958 (steps=2276, words/sec=6884.22, time=0-00:05:21)
[asean.baseline.th-en] Epoch 5.0000: train_loss/word=4.143152 (steps=2291, words/sec=8057.15, time=0-00:05:21)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 5.0000 dev BLEU4: 0.11853608290801357, 0.339836/0.160887/0.084510/0.042727 (BP = 1.000000, ratio=1.03, hyp_len=7433, ref_len=7245) (time=0-00:05:54)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.155772
[asean.baseline.th-en]              dev auxiliary Loss: 4.969 (ref_len=7245)
             checkpoint took 0-00:00:32
  best dev score, writing out model
[asean.baseline.th-en] Epoch 5.0014: train_loss/word=4.148327 (steps=2292, words/sec=7135.79, time=0-00:06:00)
[asean.baseline.th-en] Epoch 5.0530: train_loss/word=3.751101 (steps=2314, words/sec=7243.57, time=0-00:06:01)
[asean.baseline.th-en] Epoch 5.1056: train_loss/word=3.829542 (steps=2337, words/sec=7707.91, time=0-00:06:02)
[asean.baseline.th-en] Epoch 5.1574: train_loss/word=3.674336 (steps=2360, words/sec=8742.00, time=0-00:06:03)
[asean.baseline.th-en] Epoch 5.2096: train_loss/word=3.697292 (steps=2381, words/sec=8663.88, time=0-00:06:04)
[asean.baseline.th-en] Epoch 5.2604: train_loss/word=3.777280 (steps=2404, words/sec=8223.49, time=0-00:06:05)
[asean.baseline.th-en] Epoch 5.3121: train_loss/word=3.764286 (steps=2426, words/sec=9012.93, time=0-00:06:06)
[asean.baseline.th-en] Epoch 5.3632: train_loss/word=3.794981 (steps=2449, words/sec=7172.56, time=0-00:06:07)
[asean.baseline.th-en] Epoch 5.4151: train_loss/word=3.820177 (steps=2472, words/sec=8323.29, time=0-00:06:08)
[asean.baseline.th-en] Epoch 5.4657: train_loss/word=3.966784 (steps=2497, words/sec=6005.51, time=0-00:06:09)
[asean.baseline.th-en] Epoch 5.5173: train_loss/word=3.935305 (steps=2522, words/sec=6691.51, time=0-00:06:11)
[asean.baseline.th-en] Epoch 5.5673: train_loss/word=3.913813 (steps=2546, words/sec=7607.03, time=0-00:06:12)
[asean.baseline.th-en] Epoch 5.6184: train_loss/word=3.826214 (steps=2570, words/sec=8010.76, time=0-00:06:13)
[asean.baseline.th-en] Epoch 5.6695: train_loss/word=3.840251 (steps=2595, words/sec=7672.53, time=0-00:06:14)
[asean.baseline.th-en] Epoch 5.7200: train_loss/word=3.846579 (steps=2619, words/sec=8252.13, time=0-00:06:15)
[asean.baseline.th-en] Epoch 5.7707: train_loss/word=3.941512 (steps=2644, words/sec=6640.70, time=0-00:06:16)
[asean.baseline.th-en] Epoch 5.8207: train_loss/word=3.787543 (steps=2666, words/sec=8696.63, time=0-00:06:17)
[asean.baseline.th-en] Epoch 5.8724: train_loss/word=3.800063 (steps=2690, words/sec=7492.82, time=0-00:06:18)
[asean.baseline.th-en] Epoch 5.9244: train_loss/word=3.758392 (steps=2714, words/sec=8771.13, time=0-00:06:19)
[asean.baseline.th-en] Epoch 5.9764: train_loss/word=3.805974 (steps=2738, words/sec=8176.90, time=0-00:06:20)
[asean.baseline.th-en] Epoch 6.0000: train_loss/word=4.062088 (steps=2749, words/sec=7347.38, time=0-00:06:21)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 6.0000 dev BLEU4: 0.14834767720117115, 0.382133/0.206075/0.120500/0.070939 (BP = 0.920984, ratio=0.92, hyp_len=6694, ref_len=7245) (time=0-00:06:50)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.182048
[asean.baseline.th-en]              dev auxiliary Loss: 4.896 (ref_len=7245)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.th-en] Epoch 6.0023: train_loss/word=3.303079 (steps=2750, words/sec=9474.32, time=0-00:06:56)
[asean.baseline.th-en] Epoch 6.0524: train_loss/word=3.359694 (steps=2771, words/sec=8696.37, time=0-00:06:57)
[asean.baseline.th-en] Epoch 6.1031: train_loss/word=3.414367 (steps=2795, words/sec=7614.60, time=0-00:06:58)
[asean.baseline.th-en] Epoch 6.1533: train_loss/word=3.445125 (steps=2816, words/sec=9009.72, time=0-00:06:59)
[asean.baseline.th-en] Epoch 6.2039: train_loss/word=3.537024 (steps=2839, words/sec=7935.07, time=0-00:07:00)
[asean.baseline.th-en] Epoch 6.2549: train_loss/word=3.479910 (steps=2862, words/sec=7858.12, time=0-00:07:01)
[asean.baseline.th-en] Epoch 6.3055: train_loss/word=3.513387 (steps=2887, words/sec=7540.81, time=0-00:07:02)
[asean.baseline.th-en] Epoch 6.3557: train_loss/word=3.600177 (steps=2912, words/sec=7243.36, time=0-00:07:03)
[asean.baseline.th-en] Epoch 6.4057: train_loss/word=3.448319 (steps=2933, words/sec=8862.83, time=0-00:07:04)
[asean.baseline.th-en] Epoch 6.4568: train_loss/word=3.555642 (steps=2957, words/sec=7293.55, time=0-00:07:05)
[asean.baseline.th-en] Epoch 6.5069: train_loss/word=3.478140 (steps=2979, words/sec=8747.28, time=0-00:07:06)
[asean.baseline.th-en] Epoch 6.5587: train_loss/word=3.536165 (steps=3004, words/sec=8071.44, time=0-00:07:07)
[asean.baseline.th-en] Epoch 6.6092: train_loss/word=3.664846 (steps=3030, words/sec=7158.15, time=0-00:07:08)
[asean.baseline.th-en] Epoch 6.6592: train_loss/word=3.562300 (steps=3052, words/sec=7925.65, time=0-00:07:09)
[asean.baseline.th-en] Epoch 6.7107: train_loss/word=3.535093 (steps=3077, words/sec=7938.32, time=0-00:07:10)
[asean.baseline.th-en] Epoch 6.7614: train_loss/word=3.415891 (steps=3099, words/sec=8512.57, time=0-00:07:11)
[asean.baseline.th-en] Epoch 6.8141: train_loss/word=3.426424 (steps=3122, words/sec=8799.59, time=0-00:07:12)
[asean.baseline.th-en] Epoch 6.8652: train_loss/word=3.543475 (steps=3147, words/sec=7498.12, time=0-00:07:13)
[asean.baseline.th-en] Epoch 6.9159: train_loss/word=3.563559 (steps=3172, words/sec=7260.84, time=0-00:07:14)
[asean.baseline.th-en] Epoch 6.9663: train_loss/word=3.455181 (steps=3195, words/sec=8125.53, time=0-00:07:15)
[asean.baseline.th-en] Epoch 7.0000: train_loss/word=3.450608 (steps=3210, words/sec=8844.26, time=0-00:07:16)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 7.0000 dev BLEU4: 0.16272978621611944, 0.382128/0.213823/0.128426/0.074645 (BP = 0.972719, ratio=0.97, hyp_len=7050, ref_len=7245) (time=0-00:07:45)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.189521
[asean.baseline.th-en]              dev auxiliary Loss: 4.841 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
[asean.baseline.th-en] Epoch 7.0014: train_loss/word=3.431657 (steps=3211, words/sec=6826.18, time=0-00:07:50)
[asean.baseline.th-en] Epoch 7.0535: train_loss/word=3.198862 (steps=3235, words/sec=8147.38, time=0-00:07:52)
[asean.baseline.th-en] Epoch 7.1036: train_loss/word=3.170818 (steps=3259, words/sec=8102.76, time=0-00:07:53)
[asean.baseline.th-en] Epoch 7.1564: train_loss/word=3.120068 (steps=3283, words/sec=8165.70, time=0-00:07:54)
[asean.baseline.th-en] Epoch 7.2070: train_loss/word=3.224556 (steps=3308, words/sec=7997.47, time=0-00:07:55)
[asean.baseline.th-en] Epoch 7.2571: train_loss/word=3.219106 (steps=3330, words/sec=8438.94, time=0-00:07:56)
[asean.baseline.th-en] Epoch 7.3071: train_loss/word=3.256043 (steps=3351, words/sec=9099.68, time=0-00:07:56)
[asean.baseline.th-en] Epoch 7.3592: train_loss/word=3.271427 (steps=3375, words/sec=7697.22, time=0-00:07:57)
[asean.baseline.th-en] Epoch 7.4093: train_loss/word=3.264398 (steps=3397, words/sec=7987.74, time=0-00:07:58)
[asean.baseline.th-en] Epoch 7.4611: train_loss/word=3.136769 (steps=3419, words/sec=8724.26, time=0-00:07:59)
[asean.baseline.th-en] Epoch 7.5117: train_loss/word=3.254409 (steps=3444, words/sec=7411.63, time=0-00:08:00)
[asean.baseline.th-en] Epoch 7.5639: train_loss/word=3.271853 (steps=3468, words/sec=9022.10, time=0-00:08:01)
[asean.baseline.th-en] Epoch 7.6144: train_loss/word=3.261904 (steps=3492, words/sec=7821.66, time=0-00:08:03)
[asean.baseline.th-en] Epoch 7.6657: train_loss/word=3.262435 (steps=3515, words/sec=8539.08, time=0-00:08:04)
[asean.baseline.th-en] Epoch 7.7168: train_loss/word=3.290557 (steps=3537, words/sec=8125.66, time=0-00:08:04)
[asean.baseline.th-en] Epoch 7.7699: train_loss/word=3.127153 (steps=3561, words/sec=7724.74, time=0-00:08:05)
[asean.baseline.th-en] Epoch 7.8215: train_loss/word=3.286835 (steps=3586, words/sec=7671.16, time=0-00:08:07)
[asean.baseline.th-en] Epoch 7.8738: train_loss/word=3.234504 (steps=3609, words/sec=7888.59, time=0-00:08:08)
[asean.baseline.th-en] Epoch 7.9254: train_loss/word=3.386453 (steps=3634, words/sec=7196.16, time=0-00:08:09)
[asean.baseline.th-en] Epoch 7.9765: train_loss/word=3.100096 (steps=3656, words/sec=8324.42, time=0-00:08:10)
[asean.baseline.th-en] Epoch 8.0000: train_loss/word=3.228174 (steps=3667, words/sec=7253.81, time=0-00:08:10)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 8.0000 dev BLEU4: 0.18267419161525147, 0.396977/0.226489/0.141150/0.087743 (BP = 1.000000, ratio=1.02, hyp_len=7411, ref_len=7245) (time=0-00:08:42)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.206835
[asean.baseline.th-en]              dev auxiliary Loss: 4.811 (ref_len=7245)
             checkpoint took 0-00:00:31
  best dev score, writing out model
[asean.baseline.th-en] Epoch 8.0032: train_loss/word=2.542059 (steps=3668, words/sec=13443.78, time=0-00:08:47)
[asean.baseline.th-en] Epoch 8.0559: train_loss/word=2.945627 (steps=3693, words/sec=7872.24, time=0-00:08:48)
[asean.baseline.th-en] Epoch 8.1066: train_loss/word=2.914568 (steps=3716, words/sec=8524.31, time=0-00:08:49)
[asean.baseline.th-en] Epoch 8.1577: train_loss/word=3.008690 (steps=3740, words/sec=8470.47, time=0-00:08:50)
[asean.baseline.th-en] Epoch 8.2090: train_loss/word=2.957009 (steps=3764, words/sec=8102.46, time=0-00:08:51)
[asean.baseline.th-en] Epoch 8.2595: train_loss/word=2.896986 (steps=3785, words/sec=9421.13, time=0-00:08:52)
[asean.baseline.th-en] Epoch 8.3100: train_loss/word=2.899988 (steps=3805, words/sec=9438.76, time=0-00:08:53)
[asean.baseline.th-en] Epoch 8.3604: train_loss/word=2.939803 (steps=3826, words/sec=9235.39, time=0-00:08:54)
[asean.baseline.th-en] Epoch 8.4109: train_loss/word=3.054926 (steps=3849, words/sec=7770.50, time=0-00:08:55)
[asean.baseline.th-en] Epoch 8.4619: train_loss/word=2.976986 (steps=3871, words/sec=8471.41, time=0-00:08:56)
[asean.baseline.th-en] Epoch 8.5142: train_loss/word=2.993556 (steps=3895, words/sec=7864.94, time=0-00:08:57)
[asean.baseline.th-en] Epoch 8.5665: train_loss/word=3.084859 (steps=3919, words/sec=7906.12, time=0-00:08:58)
[asean.baseline.th-en] Epoch 8.6165: train_loss/word=3.052888 (steps=3941, words/sec=7479.54, time=0-00:08:59)
[asean.baseline.th-en] Epoch 8.6683: train_loss/word=3.025706 (steps=3966, words/sec=7422.26, time=0-00:09:00)
[asean.baseline.th-en] Epoch 8.7193: train_loss/word=2.988459 (steps=3990, words/sec=7550.88, time=0-00:09:01)
[asean.baseline.th-en] Epoch 8.7700: train_loss/word=3.021496 (steps=4012, words/sec=8254.14, time=0-00:09:02)
[asean.baseline.th-en] Epoch 8.8204: train_loss/word=3.040261 (steps=4037, words/sec=7469.55, time=0-00:09:03)
[asean.baseline.th-en] Epoch 8.8719: train_loss/word=3.129501 (steps=4064, words/sec=6679.02, time=0-00:09:05)
[asean.baseline.th-en] Epoch 8.9243: train_loss/word=3.069324 (steps=4089, words/sec=7478.10, time=0-00:09:06)
[asean.baseline.th-en] Epoch 8.9761: train_loss/word=3.084829 (steps=4113, words/sec=7433.63, time=0-00:09:07)
[asean.baseline.th-en] Epoch 9.0000: train_loss/word=3.116741 (steps=4124, words/sec=6861.46, time=0-00:09:07)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 9.0000 dev BLEU4: 0.19693601662584975, 0.410570/0.240486/0.155420/0.098021 (BP = 1.000000, ratio=1.01, hyp_len=7285, ref_len=7245) (time=0-00:09:38)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.217916
[asean.baseline.th-en]              dev auxiliary Loss: 4.819 (ref_len=7245)
             checkpoint took 0-00:00:30
  best dev score, writing out model
[asean.baseline.th-en] Epoch 9.0024: train_loss/word=2.476194 (steps=4125, words/sec=6425.17, time=0-00:09:44)
[asean.baseline.th-en] Epoch 9.0529: train_loss/word=2.687529 (steps=4148, words/sec=8126.83, time=0-00:09:45)
[asean.baseline.th-en] Epoch 9.1035: train_loss/word=2.727327 (steps=4170, words/sec=8332.95, time=0-00:09:46)
[asean.baseline.th-en] Epoch 9.1559: train_loss/word=2.770746 (steps=4194, words/sec=7613.62, time=0-00:09:47)
[asean.baseline.th-en] Epoch 9.2088: train_loss/word=2.865746 (steps=4221, words/sec=6936.38, time=0-00:09:48)
[asean.baseline.th-en] Epoch 9.2599: train_loss/word=2.734385 (steps=4243, words/sec=7122.36, time=0-00:09:49)
[asean.baseline.th-en] Epoch 9.3102: train_loss/word=2.813257 (steps=4266, words/sec=8079.48, time=0-00:09:50)
[asean.baseline.th-en] Epoch 9.3620: train_loss/word=2.764535 (steps=4288, words/sec=8265.30, time=0-00:09:51)
[asean.baseline.th-en] Epoch 9.4121: train_loss/word=2.714036 (steps=4310, words/sec=8225.74, time=0-00:09:52)
[asean.baseline.th-en] Epoch 9.4633: train_loss/word=2.765714 (steps=4334, words/sec=7657.57, time=0-00:09:53)
[asean.baseline.th-en] Epoch 9.5151: train_loss/word=2.801743 (steps=4358, words/sec=7825.90, time=0-00:09:54)
[asean.baseline.th-en] Epoch 9.5668: train_loss/word=2.924844 (steps=4383, words/sec=7437.78, time=0-00:09:55)
[asean.baseline.th-en] Epoch 9.6175: train_loss/word=2.878647 (steps=4408, words/sec=6792.08, time=0-00:09:56)
[asean.baseline.th-en] Epoch 9.6694: train_loss/word=2.887109 (steps=4433, words/sec=7180.96, time=0-00:09:57)
[asean.baseline.th-en] Epoch 9.7210: train_loss/word=2.924191 (steps=4456, words/sec=7437.52, time=0-00:09:58)
[asean.baseline.th-en] Epoch 9.7730: train_loss/word=2.867396 (steps=4479, words/sec=7403.56, time=0-00:10:00)
[asean.baseline.th-en] Epoch 9.8248: train_loss/word=2.825841 (steps=4502, words/sec=8216.27, time=0-00:10:00)
[asean.baseline.th-en] Epoch 9.8775: train_loss/word=2.946462 (steps=4529, words/sec=7051.76, time=0-00:10:02)
[asean.baseline.th-en] Epoch 9.9276: train_loss/word=2.851420 (steps=4552, words/sec=7705.05, time=0-00:10:03)
[asean.baseline.th-en] Epoch 9.9778: train_loss/word=2.844691 (steps=4575, words/sec=7458.36, time=0-00:10:04)
[asean.baseline.th-en] Epoch 10.0000: train_loss/word=2.937100 (steps=4586, words/sec=7685.98, time=0-00:10:04)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 10.0000 dev BLEU4: 0.20822462540438078, 0.443197/0.268280/0.174719/0.113475 (BP = 0.944987, ratio=0.95, hyp_len=6857, ref_len=7245) (time=0-00:10:33)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.235108
[asean.baseline.th-en]              dev auxiliary Loss: 4.802 (ref_len=7245)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.th-en] Epoch 10.0032: train_loss/word=2.357811 (steps=4587, words/sec=12687.81, time=0-00:10:39)
[asean.baseline.th-en] Epoch 10.0548: train_loss/word=2.596948 (steps=4611, words/sec=7447.51, time=0-00:10:40)
[asean.baseline.th-en] Epoch 10.1050: train_loss/word=2.577026 (steps=4635, words/sec=7439.03, time=0-00:10:41)
[asean.baseline.th-en] Epoch 10.1565: train_loss/word=2.582916 (steps=4658, words/sec=8178.05, time=0-00:10:42)
[asean.baseline.th-en] Epoch 10.2067: train_loss/word=2.646761 (steps=4683, words/sec=6639.54, time=0-00:10:44)
[asean.baseline.th-en] Epoch 10.2572: train_loss/word=2.562920 (steps=4705, words/sec=7385.33, time=0-00:10:45)
[asean.baseline.th-en] Epoch 10.3074: train_loss/word=2.622322 (steps=4726, words/sec=8271.75, time=0-00:10:46)
[asean.baseline.th-en] Epoch 10.3587: train_loss/word=2.638344 (steps=4750, words/sec=7161.07, time=0-00:10:47)
[asean.baseline.th-en] Epoch 10.4090: train_loss/word=2.587846 (steps=4772, words/sec=8514.48, time=0-00:10:48)
[asean.baseline.th-en] Epoch 10.4606: train_loss/word=2.632249 (steps=4795, words/sec=7420.35, time=0-00:10:49)
[asean.baseline.th-en] Epoch 10.5131: train_loss/word=2.585244 (steps=4817, words/sec=9124.67, time=0-00:10:49)
[asean.baseline.th-en] Epoch 10.5632: train_loss/word=2.663360 (steps=4841, words/sec=7667.09, time=0-00:10:50)
[asean.baseline.th-en] Epoch 10.6150: train_loss/word=2.751987 (steps=4866, words/sec=7432.72, time=0-00:10:52)
[asean.baseline.th-en] Epoch 10.6665: train_loss/word=2.638160 (steps=4890, words/sec=8440.94, time=0-00:10:53)
[asean.baseline.th-en] Epoch 10.7180: train_loss/word=2.748802 (steps=4911, words/sec=8329.41, time=0-00:10:53)
[asean.baseline.th-en] Epoch 10.7702: train_loss/word=2.601980 (steps=4933, words/sec=8787.40, time=0-00:10:54)
[asean.baseline.th-en] Epoch 10.8205: train_loss/word=2.745955 (steps=4958, words/sec=7482.33, time=0-00:10:56)
[asean.baseline.th-en] Epoch 10.8715: train_loss/word=2.771869 (steps=4982, words/sec=7790.23, time=0-00:10:57)
[asean.baseline.th-en] Epoch 10.9217: train_loss/word=2.755154 (steps=5006, words/sec=7308.35, time=0-00:10:58)
[asean.baseline.th-en] Epoch 10.9727: train_loss/word=2.793320 (steps=5032, words/sec=7671.16, time=0-00:10:59)
[asean.baseline.th-en] Epoch 11.0000: train_loss/word=2.748086 (steps=5045, words/sec=6387.70, time=0-00:11:00)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 11.0000 dev BLEU4: 0.21876016315403943, 0.431400/0.266010/0.178642/0.119774 (BP = 0.982737, ratio=0.98, hyp_len=7121, ref_len=7245) (time=0-00:11:30)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.236566
[asean.baseline.th-en]              dev auxiliary Loss: 4.814 (ref_len=7245)
             checkpoint took 0-00:00:30
  best dev score, writing out model
[asean.baseline.th-en] Epoch 11.0017: train_loss/word=2.594304 (steps=5046, words/sec=3075.21, time=0-00:11:36)
[asean.baseline.th-en] Epoch 11.0549: train_loss/word=2.503479 (steps=5072, words/sec=7454.86, time=0-00:11:37)
[asean.baseline.th-en] Epoch 11.1069: train_loss/word=2.452836 (steps=5097, words/sec=8113.37, time=0-00:11:38)
[asean.baseline.th-en] Epoch 11.1584: train_loss/word=2.546053 (steps=5123, words/sec=6412.53, time=0-00:11:39)
[asean.baseline.th-en] Epoch 11.2091: train_loss/word=2.494594 (steps=5145, words/sec=8969.60, time=0-00:11:40)
[asean.baseline.th-en] Epoch 11.2598: train_loss/word=2.520964 (steps=5169, words/sec=8508.81, time=0-00:11:41)
[asean.baseline.th-en] Epoch 11.3103: train_loss/word=2.501336 (steps=5191, words/sec=7879.35, time=0-00:11:42)
[asean.baseline.th-en] Epoch 11.3612: train_loss/word=2.544917 (steps=5216, words/sec=8144.12, time=0-00:11:43)
[asean.baseline.th-en] Epoch 11.4118: train_loss/word=2.507804 (steps=5237, words/sec=9260.20, time=0-00:11:44)
[asean.baseline.th-en] Epoch 11.4619: train_loss/word=2.563574 (steps=5262, words/sec=7708.76, time=0-00:11:45)
[asean.baseline.th-en] Epoch 11.5133: train_loss/word=2.473416 (steps=5284, words/sec=9219.83, time=0-00:11:46)
[asean.baseline.th-en] Epoch 11.5654: train_loss/word=2.570512 (steps=5306, words/sec=8584.65, time=0-00:11:47)
[asean.baseline.th-en] Epoch 11.6158: train_loss/word=2.569030 (steps=5328, words/sec=8483.04, time=0-00:11:48)
[asean.baseline.th-en] Epoch 11.6663: train_loss/word=2.482757 (steps=5351, words/sec=8257.72, time=0-00:11:49)
[asean.baseline.th-en] Epoch 11.7186: train_loss/word=2.566548 (steps=5374, words/sec=8355.61, time=0-00:11:50)
[asean.baseline.th-en] Epoch 11.7696: train_loss/word=2.500223 (steps=5396, words/sec=8446.15, time=0-00:11:51)
[asean.baseline.th-en] Epoch 11.8207: train_loss/word=2.521574 (steps=5420, words/sec=7371.38, time=0-00:11:52)
[asean.baseline.th-en] Epoch 11.8718: train_loss/word=2.627492 (steps=5444, words/sec=7351.70, time=0-00:11:53)
[asean.baseline.th-en] Epoch 11.9233: train_loss/word=2.546089 (steps=5466, words/sec=8643.32, time=0-00:11:54)
[asean.baseline.th-en] Epoch 11.9739: train_loss/word=2.573671 (steps=5488, words/sec=8201.39, time=0-00:11:55)
[asean.baseline.th-en] Epoch 12.0000: train_loss/word=2.597867 (steps=5501, words/sec=7308.12, time=0-00:11:55)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 12.0000 dev BLEU4: 0.23066215898063697, 0.456140/0.285714/0.196200/0.135465 (BP = 0.950795, ratio=0.95, hyp_len=6897, ref_len=7245) (time=0-00:12:25)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.251841
[asean.baseline.th-en]              dev auxiliary Loss: 4.835 (ref_len=7245)
             checkpoint took 0-00:00:29
  best dev score, writing out model
[asean.baseline.th-en] Epoch 12.0026: train_loss/word=2.350551 (steps=5502, words/sec=11179.10, time=0-00:12:30)
[asean.baseline.th-en] Epoch 12.0527: train_loss/word=2.370951 (steps=5524, words/sec=8535.11, time=0-00:12:31)
[asean.baseline.th-en] Epoch 12.1034: train_loss/word=2.326856 (steps=5548, words/sec=7939.51, time=0-00:12:32)
[asean.baseline.th-en] Epoch 12.1549: train_loss/word=2.368505 (steps=5572, words/sec=8153.80, time=0-00:12:33)
[asean.baseline.th-en] Epoch 12.2069: train_loss/word=2.335554 (steps=5595, words/sec=8625.47, time=0-00:12:34)
[asean.baseline.th-en] Epoch 12.2588: train_loss/word=2.397421 (steps=5618, words/sec=6922.59, time=0-00:12:35)
[asean.baseline.th-en] Epoch 12.3105: train_loss/word=2.504960 (steps=5647, words/sec=6427.38, time=0-00:12:37)
[asean.baseline.th-en] Epoch 12.3607: train_loss/word=2.363204 (steps=5669, words/sec=8996.22, time=0-00:12:38)
[asean.baseline.th-en] Epoch 12.4111: train_loss/word=2.370719 (steps=5690, words/sec=7816.15, time=0-00:12:39)
[asean.baseline.th-en] Epoch 12.4613: train_loss/word=2.429609 (steps=5714, words/sec=7175.40, time=0-00:12:40)
[asean.baseline.th-en] Epoch 12.5115: train_loss/word=2.459414 (steps=5738, words/sec=7568.78, time=0-00:12:41)
[asean.baseline.th-en] Epoch 12.5623: train_loss/word=2.442217 (steps=5763, words/sec=8164.58, time=0-00:12:42)
[asean.baseline.th-en] Epoch 12.6125: train_loss/word=2.456757 (steps=5785, words/sec=8516.67, time=0-00:12:43)
[asean.baseline.th-en] Epoch 12.6643: train_loss/word=2.462696 (steps=5808, words/sec=8175.65, time=0-00:12:44)
[asean.baseline.th-en] Epoch 12.7149: train_loss/word=2.445188 (steps=5832, words/sec=8684.83, time=0-00:12:45)
[asean.baseline.th-en] Epoch 12.7664: train_loss/word=2.453983 (steps=5856, words/sec=6943.98, time=0-00:12:46)
[asean.baseline.th-en] Epoch 12.8178: train_loss/word=2.408725 (steps=5879, words/sec=8360.96, time=0-00:12:47)
[asean.baseline.th-en] Epoch 12.8688: train_loss/word=2.432749 (steps=5902, words/sec=8329.00, time=0-00:12:48)
[asean.baseline.th-en] Epoch 12.9219: train_loss/word=2.406035 (steps=5923, words/sec=9437.15, time=0-00:12:49)
[asean.baseline.th-en] Epoch 12.9724: train_loss/word=2.498211 (steps=5947, words/sec=7651.57, time=0-00:12:50)
[asean.baseline.th-en] Epoch 13.0000: train_loss/word=2.445406 (steps=5958, words/sec=8870.16, time=0-00:12:50)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 13.0000 dev BLEU4: 0.2296280188066882, 0.444775/0.278977/0.190238/0.131336 (BP = 0.973145, ratio=0.97, hyp_len=7053, ref_len=7245) (time=0-00:13:20)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.247231
[asean.baseline.th-en]              dev auxiliary Loss: 4.841 (ref_len=7245)
             checkpoint took 0-00:00:29
[asean.baseline.th-en] Epoch 13.0021: train_loss/word=2.163611 (steps=5959, words/sec=8698.09, time=0-00:13:20)
[asean.baseline.th-en] Epoch 13.0524: train_loss/word=2.304956 (steps=5982, words/sec=6861.13, time=0-00:13:21)
[asean.baseline.th-en] Epoch 13.1046: train_loss/word=2.294990 (steps=6006, words/sec=7289.34, time=0-00:13:22)
[asean.baseline.th-en] Epoch 13.1550: train_loss/word=2.292314 (steps=6030, words/sec=7055.01, time=0-00:13:23)
[asean.baseline.th-en] Epoch 13.2062: train_loss/word=2.300355 (steps=6055, words/sec=7071.31, time=0-00:13:25)
[asean.baseline.th-en] Epoch 13.2570: train_loss/word=2.301955 (steps=6077, words/sec=8327.75, time=0-00:13:25)
[asean.baseline.th-en] Epoch 13.3080: train_loss/word=2.262647 (steps=6099, words/sec=8382.51, time=0-00:13:26)
[asean.baseline.th-en] Epoch 13.3594: train_loss/word=2.277821 (steps=6123, words/sec=8335.63, time=0-00:13:27)
[asean.baseline.th-en] Epoch 13.4108: train_loss/word=2.304217 (steps=6147, words/sec=7521.17, time=0-00:13:28)
[asean.baseline.th-en] Epoch 13.4614: train_loss/word=2.293683 (steps=6171, words/sec=8317.64, time=0-00:13:29)
[asean.baseline.th-en] Epoch 13.5120: train_loss/word=2.368734 (steps=6195, words/sec=7757.00, time=0-00:13:31)
[asean.baseline.th-en] Epoch 13.5638: train_loss/word=2.297416 (steps=6217, words/sec=8375.49, time=0-00:13:31)
[asean.baseline.th-en] Epoch 13.6155: train_loss/word=2.322228 (steps=6240, words/sec=7793.82, time=0-00:13:32)
[asean.baseline.th-en] Epoch 13.6658: train_loss/word=2.396181 (steps=6263, words/sec=7784.48, time=0-00:13:33)
[asean.baseline.th-en] Epoch 13.7169: train_loss/word=2.359660 (steps=6288, words/sec=7312.42, time=0-00:13:35)
[asean.baseline.th-en] Epoch 13.7672: train_loss/word=2.345230 (steps=6311, words/sec=7680.90, time=0-00:13:36)
[asean.baseline.th-en] Epoch 13.8185: train_loss/word=2.395359 (steps=6335, words/sec=7410.39, time=0-00:13:37)
[asean.baseline.th-en] Epoch 13.8703: train_loss/word=2.291819 (steps=6354, words/sec=8661.89, time=0-00:13:38)
[asean.baseline.th-en] Epoch 13.9222: train_loss/word=2.381877 (steps=6380, words/sec=6957.50, time=0-00:13:39)
[asean.baseline.th-en] Epoch 13.9746: train_loss/word=2.384202 (steps=6403, words/sec=8429.23, time=0-00:13:40)
[asean.baseline.th-en] Epoch 14.0000: train_loss/word=2.358491 (steps=6414, words/sec=8659.03, time=0-00:13:40)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 14.0000 dev BLEU4: 0.228397651737553, 0.427793/0.271807/0.187721/0.131252 (BP = 0.987221, ratio=0.99, hyp_len=7153, ref_len=7245) (time=0-00:14:10)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.242371
[asean.baseline.th-en]              dev auxiliary Loss: 4.824 (ref_len=7245)
             checkpoint took 0-00:00:29
  new learning rate: 0.5
[asean.baseline.th-en] Epoch 14.0032: train_loss/word=2.163680 (steps=6415, words/sec=11557.55, time=0-00:14:10)
[asean.baseline.th-en] Epoch 14.0543: train_loss/word=2.175109 (steps=6437, words/sec=7869.68, time=0-00:14:11)
[asean.baseline.th-en] Epoch 14.1043: train_loss/word=2.139678 (steps=6460, words/sec=8252.45, time=0-00:14:12)
[asean.baseline.th-en] Epoch 14.1561: train_loss/word=2.198526 (steps=6486, words/sec=6979.81, time=0-00:14:13)
[asean.baseline.th-en] Epoch 14.2081: train_loss/word=2.161067 (steps=6511, words/sec=6839.43, time=0-00:14:14)
[asean.baseline.th-en] Epoch 14.2581: train_loss/word=2.184161 (steps=6536, words/sec=6810.16, time=0-00:14:16)
[asean.baseline.th-en] Epoch 14.3084: train_loss/word=2.173340 (steps=6560, words/sec=6516.43, time=0-00:14:17)
[asean.baseline.th-en] Epoch 14.3595: train_loss/word=2.100692 (steps=6581, words/sec=9692.13, time=0-00:14:18)
[asean.baseline.th-en] Epoch 14.4104: train_loss/word=2.193071 (steps=6607, words/sec=6722.33, time=0-00:14:19)
[asean.baseline.th-en] Epoch 14.4614: train_loss/word=2.152771 (steps=6630, words/sec=8579.25, time=0-00:14:20)
[asean.baseline.th-en] Epoch 14.5126: train_loss/word=2.099384 (steps=6651, words/sec=9331.01, time=0-00:14:21)
[asean.baseline.th-en] Epoch 14.5645: train_loss/word=2.152212 (steps=6675, words/sec=7990.14, time=0-00:14:22)
[asean.baseline.th-en] Epoch 14.6164: train_loss/word=2.153458 (steps=6697, words/sec=7997.77, time=0-00:14:23)
[asean.baseline.th-en] Epoch 14.6677: train_loss/word=2.110272 (steps=6718, words/sec=8762.75, time=0-00:14:24)
[asean.baseline.th-en] Epoch 14.7178: train_loss/word=2.114386 (steps=6740, words/sec=8204.85, time=0-00:14:25)
[asean.baseline.th-en] Epoch 14.7707: train_loss/word=2.145470 (steps=6763, words/sec=8244.57, time=0-00:14:26)
[asean.baseline.th-en] Epoch 14.8238: train_loss/word=2.178159 (steps=6789, words/sec=7029.27, time=0-00:14:27)
[asean.baseline.th-en] Epoch 14.8753: train_loss/word=2.129752 (steps=6812, words/sec=8747.64, time=0-00:14:28)
[asean.baseline.th-en] Epoch 14.9260: train_loss/word=2.158403 (steps=6836, words/sec=7870.51, time=0-00:14:29)
[asean.baseline.th-en] Epoch 14.9769: train_loss/word=2.167607 (steps=6861, words/sec=7065.28, time=0-00:14:30)
[asean.baseline.th-en] Epoch 15.0000: train_loss/word=2.152966 (steps=6872, words/sec=7271.64, time=0-00:14:30)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 15.0000 dev BLEU4: 0.26385955492796165, 0.469102/0.314585/0.234091/0.177262 (BP = 0.943238, ratio=0.94, hyp_len=6845, ref_len=7245) (time=0-00:15:01)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.274095
[asean.baseline.th-en]              dev auxiliary Loss: 4.780 (ref_len=7245)
             checkpoint took 0-00:00:30
  best dev score, writing out model
[asean.baseline.th-en] Epoch 15.0018: train_loss/word=2.081119 (steps=6873, words/sec=9087.30, time=0-00:15:07)
[asean.baseline.th-en] Epoch 15.0526: train_loss/word=2.021609 (steps=6896, words/sec=8172.50, time=0-00:15:08)
[asean.baseline.th-en] Epoch 15.1027: train_loss/word=2.055779 (steps=6919, words/sec=8345.38, time=0-00:15:09)
[asean.baseline.th-en] Epoch 15.1545: train_loss/word=2.090929 (steps=6943, words/sec=7280.66, time=0-00:15:10)
[asean.baseline.th-en] Epoch 15.2071: train_loss/word=2.062061 (steps=6968, words/sec=8528.47, time=0-00:15:11)
[asean.baseline.th-en] Epoch 15.2582: train_loss/word=2.040752 (steps=6990, words/sec=9077.78, time=0-00:15:12)
[asean.baseline.th-en] Epoch 15.3107: train_loss/word=2.073434 (steps=7015, words/sec=8207.84, time=0-00:15:13)
[asean.baseline.th-en] Epoch 15.3618: train_loss/word=2.038073 (steps=7039, words/sec=7352.40, time=0-00:15:14)
[asean.baseline.th-en] Epoch 15.4126: train_loss/word=2.060269 (steps=7063, words/sec=7992.10, time=0-00:15:15)
[asean.baseline.th-en] Epoch 15.4634: train_loss/word=2.062265 (steps=7088, words/sec=7449.26, time=0-00:15:17)
[asean.baseline.th-en] Epoch 15.5161: train_loss/word=2.068236 (steps=7110, words/sec=9301.85, time=0-00:15:17)
[asean.baseline.th-en] Epoch 15.5675: train_loss/word=2.050894 (steps=7134, words/sec=8094.60, time=0-00:15:18)
[asean.baseline.th-en] Epoch 15.6190: train_loss/word=2.072697 (steps=7158, words/sec=8195.18, time=0-00:15:19)
[asean.baseline.th-en] Epoch 15.6698: train_loss/word=2.085335 (steps=7181, words/sec=7996.35, time=0-00:15:20)
[asean.baseline.th-en] Epoch 15.7207: train_loss/word=2.034657 (steps=7203, words/sec=8846.36, time=0-00:15:21)
[asean.baseline.th-en] Epoch 15.7715: train_loss/word=2.077248 (steps=7226, words/sec=8003.56, time=0-00:15:22)
[asean.baseline.th-en] Epoch 15.8230: train_loss/word=2.103579 (steps=7249, words/sec=8171.27, time=0-00:15:23)
[asean.baseline.th-en] Epoch 15.8752: train_loss/word=2.090608 (steps=7274, words/sec=7219.88, time=0-00:15:25)
[asean.baseline.th-en] Epoch 15.9257: train_loss/word=2.110297 (steps=7296, words/sec=8398.63, time=0-00:15:25)
[asean.baseline.th-en] Epoch 15.9775: train_loss/word=2.086421 (steps=7320, words/sec=8491.34, time=0-00:15:26)
[asean.baseline.th-en] Epoch 16.0000: train_loss/word=2.165545 (steps=7331, words/sec=6477.92, time=0-00:15:27)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 16.0000 dev BLEU4: 0.25349280770348104, 0.446499/0.288425/0.207736/0.154347 (BP = 1.000000, ratio=1.02, hyp_len=7355, ref_len=7245) (time=0-00:15:57)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.263535
[asean.baseline.th-en]              dev auxiliary Loss: 4.788 (ref_len=7245)
             checkpoint took 0-00:00:30
  new learning rate: 0.25
[asean.baseline.th-en] Epoch 16.0023: train_loss/word=2.068007 (steps=7332, words/sec=7869.32, time=0-00:15:58)
[asean.baseline.th-en] Epoch 16.0546: train_loss/word=2.010402 (steps=7354, words/sec=9081.98, time=0-00:15:58)
[asean.baseline.th-en] Epoch 16.1064: train_loss/word=2.020420 (steps=7379, words/sec=7649.24, time=0-00:16:00)
[asean.baseline.th-en] Epoch 16.1591: train_loss/word=1.995333 (steps=7404, words/sec=7631.67, time=0-00:16:01)
[asean.baseline.th-en] Epoch 16.2108: train_loss/word=1.981721 (steps=7428, words/sec=7777.70, time=0-00:16:02)
[asean.baseline.th-en] Epoch 16.2611: train_loss/word=1.966729 (steps=7450, words/sec=8898.54, time=0-00:16:03)
[asean.baseline.th-en] Epoch 16.3118: train_loss/word=1.995226 (steps=7473, words/sec=8042.28, time=0-00:16:04)
[asean.baseline.th-en] Epoch 16.3623: train_loss/word=1.982111 (steps=7496, words/sec=7738.49, time=0-00:16:05)
[asean.baseline.th-en] Epoch 16.4131: train_loss/word=1.999482 (steps=7520, words/sec=7552.07, time=0-00:16:06)
[asean.baseline.th-en] Epoch 16.4659: train_loss/word=1.953551 (steps=7543, words/sec=8191.89, time=0-00:16:07)
[asean.baseline.th-en] Epoch 16.5176: train_loss/word=1.992763 (steps=7568, words/sec=7636.77, time=0-00:16:08)
[asean.baseline.th-en] Epoch 16.5687: train_loss/word=1.985207 (steps=7593, words/sec=6904.70, time=0-00:16:09)
[asean.baseline.th-en] Epoch 16.6188: train_loss/word=1.994924 (steps=7616, words/sec=7874.69, time=0-00:16:10)
[asean.baseline.th-en] Epoch 16.6705: train_loss/word=2.003964 (steps=7641, words/sec=7473.89, time=0-00:16:11)
[asean.baseline.th-en] Epoch 16.7210: train_loss/word=1.986697 (steps=7665, words/sec=7571.83, time=0-00:16:12)
[asean.baseline.th-en] Epoch 16.7719: train_loss/word=1.968228 (steps=7687, words/sec=9168.16, time=0-00:16:13)
[asean.baseline.th-en] Epoch 16.8226: train_loss/word=1.990918 (steps=7710, words/sec=8181.85, time=0-00:16:14)
[asean.baseline.th-en] Epoch 16.8739: train_loss/word=1.973023 (steps=7733, words/sec=8098.35, time=0-00:16:15)
[asean.baseline.th-en] Epoch 16.9247: train_loss/word=2.028304 (steps=7757, words/sec=7345.28, time=0-00:16:16)
[asean.baseline.th-en] Epoch 16.9768: train_loss/word=1.979667 (steps=7780, words/sec=8366.88, time=0-00:16:17)
[asean.baseline.th-en] Epoch 17.0000: train_loss/word=1.991229 (steps=7790, words/sec=7913.85, time=0-00:16:18)
> Checkpoint [asean.baseline.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[asean.baseline.th-en] Epoch 17.0000 dev BLEU4: 0.26369633638529455, 0.456863/0.297992/0.218185/0.162780 (BP = 1.000000, ratio=1.00, hyp_len=7256, ref_len=7245) (time=0-00:16:48)
[asean.baseline.th-en]              dev auxiliary GLEU: 0.270755
[asean.baseline.th-en]              dev auxiliary Loss: 4.783 (ref_len=7245)
             checkpoint took 0-00:00:30
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.en
Performing inference on ./data/test.th and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.th-en          | BLEU4: 0.26385955492796165, 0.469102/0.314585/0.234091/0.177262 (BP = 0.943238, ratio=0.94, hyp_len=6845, ref_len=7245)
                              | GLEU: 0.274095
                              | WER: 65.29% ( C/S/I/D: 3182/2996/667/1067; hyp_len=6845, ref_len=7245 )
                              | CER: 52.88% ( C/S/I/D: 17012/7455/2689/5928; hyp_len=27156, ref_len=30395 )
                              | BLEU4: 0.2739701584690131, 0.489638/0.331681/0.238898/0.175448 (BP = 0.953815, ratio=0.95, hyp_len=6852, ref_len=7176)
                              | GLEU: 0.288053
                              | WER: 62.32% ( C/S/I/D: 3338/2880/634/958; hyp_len=6852, ref_len=7176 )
                              | CER: 51.61% ( C/S/I/D: 17645/7169/2932/5594; hyp_len=27746, ref_len=30408 )
```

## Training for en-th, word unit (SwitchOut)

run ထားတယ်... go back home ...  
(22:10, Thai time)  

shell ရေးပြီး run ထားခဲ့တယ်။   

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$ cat ./train.sh 
#!/bin/bash

time xnmt --backend torch --gpu ./config.switchout.en-th-word.yaml | tee ./switchout.en-th.log1
time xnmt --backend torch --gpu ./config.switchout.th-en-word.yaml | tee ./switchout.th-en.log1
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$
```

အင်္ဂလိပ် ကနေ ထိုင်း SwitchOut argumentation running log က အောက်ပါအတိုင်း...   

```
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 22:09:14
=> Running switchout.asean.en-th
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 20656222
> Training
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 0.0509: train_loss/word=8.889112 (steps=23, words/sec=5097.16, time=0-00:00:07)
[switchout.asean.en-th] Epoch 0.1015: train_loss/word=7.662451 (steps=45, words/sec=8760.88, time=0-00:00:08)
[switchout.asean.en-th] Epoch 0.1538: train_loss/word=7.545909 (steps=68, words/sec=8133.68, time=0-00:00:09)
[switchout.asean.en-th] Epoch 0.2039: train_loss/word=7.447060 (steps=90, words/sec=8326.01, time=0-00:00:10)
[switchout.asean.en-th] Epoch 0.2540: train_loss/word=7.393307 (steps=113, words/sec=7815.15, time=0-00:00:11)
[switchout.asean.en-th] Epoch 0.3044: train_loss/word=7.135340 (steps=138, words/sec=7896.35, time=0-00:00:12)
[switchout.asean.en-th] Epoch 0.3556: train_loss/word=7.206891 (steps=161, words/sec=7871.47, time=0-00:00:13)
[switchout.asean.en-th] Epoch 0.4069: train_loss/word=7.081344 (steps=183, words/sec=8926.88, time=0-00:00:14)
[switchout.asean.en-th] Epoch 0.4570: train_loss/word=7.029870 (steps=208, words/sec=7690.84, time=0-00:00:15)
[switchout.asean.en-th] Epoch 0.5078: train_loss/word=6.995432 (steps=229, words/sec=8667.49, time=0-00:00:16)
[switchout.asean.en-th] Epoch 0.5586: train_loss/word=6.938276 (steps=250, words/sec=8832.63, time=0-00:00:17)
[switchout.asean.en-th] Epoch 0.6096: train_loss/word=6.791519 (steps=272, words/sec=9121.24, time=0-00:00:18)
[switchout.asean.en-th] Epoch 0.6644: train_loss/word=6.771207 (steps=297, words/sec=8227.18, time=0-00:00:19)
[switchout.asean.en-th] Epoch 0.7168: train_loss/word=6.661481 (steps=321, words/sec=8005.82, time=0-00:00:20)
[switchout.asean.en-th] Epoch 0.7682: train_loss/word=6.699413 (steps=343, words/sec=8785.12, time=0-00:00:21)
[switchout.asean.en-th] Epoch 0.8220: train_loss/word=6.705498 (steps=365, words/sec=9370.45, time=0-00:00:22)
[switchout.asean.en-th] Epoch 0.8734: train_loss/word=6.615140 (steps=385, words/sec=8784.47, time=0-00:00:22)
[switchout.asean.en-th] Epoch 0.9238: train_loss/word=6.598193 (steps=407, words/sec=8220.14, time=0-00:00:23)
[switchout.asean.en-th] Epoch 0.9741: train_loss/word=6.550363 (steps=428, words/sec=8905.76, time=0-00:00:24)
[switchout.asean.en-th] Epoch 1.0000: train_loss/word=6.499779 (steps=441, words/sec=7233.67, time=0-00:00:25)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 1.0000 dev BLEU4: 0.022390376169156657, 0.161639/0.045133/0.011853/0.002906 (BP = 1.000000, ratio=1.25, hyp_len=8519, ref_len=6809) (time=0-00:00:56)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.057217
[switchout.asean.en-th]              dev auxiliary Loss: 6.053 (ref_len=6809)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 1.0027: train_loss/word=6.395937 (steps=442, words/sec=10304.18, time=0-00:01:18)
[switchout.asean.en-th] Epoch 1.0538: train_loss/word=6.491305 (steps=464, words/sec=7969.44, time=0-00:01:19)
[switchout.asean.en-th] Epoch 1.1059: train_loss/word=6.409280 (steps=488, words/sec=8189.06, time=0-00:01:20)
[switchout.asean.en-th] Epoch 1.1571: train_loss/word=6.278436 (steps=511, words/sec=8804.93, time=0-00:01:21)
[switchout.asean.en-th] Epoch 1.2098: train_loss/word=6.451135 (steps=532, words/sec=8494.08, time=0-00:01:22)
[switchout.asean.en-th] Epoch 1.2618: train_loss/word=6.300471 (steps=558, words/sec=8215.51, time=0-00:01:23)
[switchout.asean.en-th] Epoch 1.3147: train_loss/word=6.263375 (steps=584, words/sec=7997.39, time=0-00:01:24)
[switchout.asean.en-th] Epoch 1.3663: train_loss/word=6.310035 (steps=609, words/sec=7657.38, time=0-00:01:26)
[switchout.asean.en-th] Epoch 1.4167: train_loss/word=6.316686 (steps=629, words/sec=8843.75, time=0-00:01:26)
[switchout.asean.en-th] Epoch 1.4694: train_loss/word=6.203519 (steps=651, words/sec=9166.20, time=0-00:01:27)
[switchout.asean.en-th] Epoch 1.5220: train_loss/word=6.340102 (steps=673, words/sec=8449.47, time=0-00:01:28)
[switchout.asean.en-th] Epoch 1.5733: train_loss/word=6.235230 (steps=695, words/sec=8151.53, time=0-00:01:29)
[switchout.asean.en-th] Epoch 1.6255: train_loss/word=6.205953 (steps=719, words/sec=7876.37, time=0-00:01:30)
[switchout.asean.en-th] Epoch 1.6776: train_loss/word=6.253342 (steps=741, words/sec=7205.14, time=0-00:01:31)
[switchout.asean.en-th] Epoch 1.7287: train_loss/word=6.164840 (steps=764, words/sec=8326.34, time=0-00:01:32)
[switchout.asean.en-th] Epoch 1.7805: train_loss/word=6.198974 (steps=787, words/sec=8704.06, time=0-00:01:33)
[switchout.asean.en-th] Epoch 1.8320: train_loss/word=6.093419 (steps=812, words/sec=7665.51, time=0-00:01:34)
[switchout.asean.en-th] Epoch 1.8827: train_loss/word=6.149699 (steps=832, words/sec=9369.10, time=0-00:01:35)
[switchout.asean.en-th] Epoch 1.9356: train_loss/word=6.022475 (steps=855, words/sec=8465.12, time=0-00:01:36)
[switchout.asean.en-th] Epoch 1.9866: train_loss/word=6.100604 (steps=879, words/sec=7794.47, time=0-00:01:37)
[switchout.asean.en-th] Epoch 2.0000: train_loss/word=6.372032 (steps=883, words/sec=10965.31, time=0-00:01:37)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 2.0000 dev BLEU4: 0.037392759771153056, 0.218459/0.071977/0.020828/0.005970 (BP = 1.000000, ratio=1.36, hyp_len=9242, ref_len=6809) (time=0-00:02:08)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.082014
[switchout.asean.en-th]              dev auxiliary Loss: 5.550 (ref_len=6809)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 2.0011: train_loss/word=5.909178 (steps=884, words/sec=5378.65, time=0-00:02:18)
[switchout.asean.en-th] Epoch 2.0525: train_loss/word=5.937221 (steps=906, words/sec=8753.62, time=0-00:02:19)
[switchout.asean.en-th] Epoch 2.1050: train_loss/word=5.832024 (steps=931, words/sec=8265.97, time=0-00:02:20)
[switchout.asean.en-th] Epoch 2.1567: train_loss/word=5.874654 (steps=953, words/sec=8222.67, time=0-00:02:21)
[switchout.asean.en-th] Epoch 2.2089: train_loss/word=5.889713 (steps=974, words/sec=8918.02, time=0-00:02:21)
[switchout.asean.en-th] Epoch 2.2608: train_loss/word=5.798262 (steps=996, words/sec=8967.23, time=0-00:02:22)
[switchout.asean.en-th] Epoch 2.3116: train_loss/word=5.911977 (steps=1017, words/sec=8626.38, time=0-00:02:23)
[switchout.asean.en-th] Epoch 2.3628: train_loss/word=5.813498 (steps=1044, words/sec=7515.23, time=0-00:02:24)
[switchout.asean.en-th] Epoch 2.4134: train_loss/word=5.839255 (steps=1067, words/sec=8125.18, time=0-00:02:25)
[switchout.asean.en-th] Epoch 2.4652: train_loss/word=5.838579 (steps=1090, words/sec=8383.97, time=0-00:02:26)
[switchout.asean.en-th] Epoch 2.5169: train_loss/word=5.745016 (steps=1116, words/sec=7475.75, time=0-00:02:28)
[switchout.asean.en-th] Epoch 2.5690: train_loss/word=5.782934 (steps=1139, words/sec=8492.66, time=0-00:02:29)
[switchout.asean.en-th] Epoch 2.6202: train_loss/word=5.765694 (steps=1161, words/sec=8207.78, time=0-00:02:29)
[switchout.asean.en-th] Epoch 2.6705: train_loss/word=5.797725 (steps=1182, words/sec=9320.13, time=0-00:02:30)
[switchout.asean.en-th] Epoch 2.7239: train_loss/word=5.769183 (steps=1203, words/sec=9170.42, time=0-00:02:31)
[switchout.asean.en-th] Epoch 2.7744: train_loss/word=5.765012 (steps=1227, words/sec=7713.29, time=0-00:02:32)
[switchout.asean.en-th] Epoch 2.8265: train_loss/word=5.762308 (steps=1251, words/sec=7427.92, time=0-00:02:33)
[switchout.asean.en-th] Epoch 2.8799: train_loss/word=5.836543 (steps=1273, words/sec=8879.70, time=0-00:02:34)
[switchout.asean.en-th] Epoch 2.9308: train_loss/word=5.666702 (steps=1296, words/sec=8548.86, time=0-00:02:35)
[switchout.asean.en-th] Epoch 2.9831: train_loss/word=5.727287 (steps=1318, words/sec=7565.14, time=0-00:02:36)
[switchout.asean.en-th] Epoch 3.0000: train_loss/word=5.753874 (steps=1325, words/sec=9062.77, time=0-00:02:36)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 3.0000 dev BLEU4: 0.06945311820410695, 0.289657/0.114735/0.042499/0.016474 (BP = 1.000000, ratio=1.16, hyp_len=7899, ref_len=6809) (time=0-00:03:05)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.115828
[switchout.asean.en-th]              dev auxiliary Loss: 5.162 (ref_len=6809)
             checkpoint took 0-00:00:29
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 3.0010: train_loss/word=5.616173 (steps=1326, words/sec=4797.03, time=0-00:03:15)
[switchout.asean.en-th] Epoch 3.0514: train_loss/word=5.566293 (steps=1348, words/sec=7768.43, time=0-00:03:16)
[switchout.asean.en-th] Epoch 3.1017: train_loss/word=5.548424 (steps=1370, words/sec=9049.58, time=0-00:03:17)
[switchout.asean.en-th] Epoch 3.1527: train_loss/word=5.476753 (steps=1394, words/sec=7831.77, time=0-00:03:18)
[switchout.asean.en-th] Epoch 3.2029: train_loss/word=5.429432 (steps=1419, words/sec=7966.89, time=0-00:03:19)
[switchout.asean.en-th] Epoch 3.2535: train_loss/word=5.464525 (steps=1441, words/sec=8561.63, time=0-00:03:20)
[switchout.asean.en-th] Epoch 3.3044: train_loss/word=5.602820 (steps=1463, words/sec=7300.01, time=0-00:03:21)
[switchout.asean.en-th] Epoch 3.3554: train_loss/word=5.451109 (steps=1488, words/sec=8095.42, time=0-00:03:22)
[switchout.asean.en-th] Epoch 3.4069: train_loss/word=5.537639 (steps=1511, words/sec=8316.99, time=0-00:03:23)
[switchout.asean.en-th] Epoch 3.4570: train_loss/word=5.515962 (steps=1530, words/sec=9258.98, time=0-00:03:24)
[switchout.asean.en-th] Epoch 3.5089: train_loss/word=5.402288 (steps=1553, words/sec=8794.73, time=0-00:03:24)
[switchout.asean.en-th] Epoch 3.5610: train_loss/word=5.411224 (steps=1575, words/sec=8880.04, time=0-00:03:25)
[switchout.asean.en-th] Epoch 3.6132: train_loss/word=5.458384 (steps=1595, words/sec=8969.53, time=0-00:03:26)
[switchout.asean.en-th] Epoch 3.6639: train_loss/word=5.504914 (steps=1615, words/sec=9333.17, time=0-00:03:27)
[switchout.asean.en-th] Epoch 3.7142: train_loss/word=5.520939 (steps=1633, words/sec=9489.34, time=0-00:03:27)
[switchout.asean.en-th] Epoch 3.7648: train_loss/word=5.359593 (steps=1658, words/sec=7572.71, time=0-00:03:29)
[switchout.asean.en-th] Epoch 3.8153: train_loss/word=5.452018 (steps=1678, words/sec=8736.21, time=0-00:03:29)
[switchout.asean.en-th] Epoch 3.8656: train_loss/word=5.447593 (steps=1701, words/sec=7268.05, time=0-00:03:30)
[switchout.asean.en-th] Epoch 3.9183: train_loss/word=5.393468 (steps=1725, words/sec=8149.04, time=0-00:03:31)
[switchout.asean.en-th] Epoch 3.9702: train_loss/word=5.380896 (steps=1750, words/sec=6783.12, time=0-00:03:33)
[switchout.asean.en-th] Epoch 4.0000: train_loss/word=5.440189 (steps=1765, words/sec=7870.03, time=0-00:03:33)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 4.0000 dev BLEU4: 0.08684871060655969, 0.312507/0.140118/0.056754/0.022893 (BP = 1.000000, ratio=1.29, hyp_len=8803, ref_len=6809) (time=0-00:04:05)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.137327
[switchout.asean.en-th]              dev auxiliary Loss: 4.902 (ref_len=6809)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 4.0015: train_loss/word=5.126780 (steps=1766, words/sec=7518.24, time=0-00:04:14)
[switchout.asean.en-th] Epoch 4.0522: train_loss/word=5.239128 (steps=1788, words/sec=7948.41, time=0-00:04:15)
[switchout.asean.en-th] Epoch 4.1037: train_loss/word=5.316377 (steps=1809, words/sec=8712.40, time=0-00:04:16)
[switchout.asean.en-th] Epoch 4.1560: train_loss/word=5.259661 (steps=1831, words/sec=8781.37, time=0-00:04:17)
[switchout.asean.en-th] Epoch 4.2095: train_loss/word=5.228003 (steps=1854, words/sec=8320.75, time=0-00:04:18)
[switchout.asean.en-th] Epoch 4.2611: train_loss/word=5.282011 (steps=1876, words/sec=8479.99, time=0-00:04:19)
[switchout.asean.en-th] Epoch 4.3111: train_loss/word=5.189207 (steps=1899, words/sec=8526.10, time=0-00:04:20)
[switchout.asean.en-th] Epoch 4.3625: train_loss/word=5.110170 (steps=1922, words/sec=8457.55, time=0-00:04:21)
[switchout.asean.en-th] Epoch 4.4138: train_loss/word=5.247117 (steps=1946, words/sec=8180.22, time=0-00:04:22)
[switchout.asean.en-th] Epoch 4.4657: train_loss/word=5.193843 (steps=1970, words/sec=7020.09, time=0-00:04:23)
[switchout.asean.en-th] Epoch 4.5193: train_loss/word=5.292974 (steps=1993, words/sec=7714.70, time=0-00:04:24)
[switchout.asean.en-th] Epoch 4.5704: train_loss/word=5.130403 (steps=2018, words/sec=7289.83, time=0-00:04:25)
[switchout.asean.en-th] Epoch 4.6218: train_loss/word=5.168489 (steps=2040, words/sec=9016.05, time=0-00:04:26)
[switchout.asean.en-th] Epoch 4.6746: train_loss/word=5.158280 (steps=2064, words/sec=7693.27, time=0-00:04:27)
[switchout.asean.en-th] Epoch 4.7254: train_loss/word=5.070960 (steps=2086, words/sec=8650.68, time=0-00:04:28)
[switchout.asean.en-th] Epoch 4.7762: train_loss/word=5.312513 (steps=2107, words/sec=8128.56, time=0-00:04:29)
[switchout.asean.en-th] Epoch 4.8280: train_loss/word=5.173197 (steps=2128, words/sec=8913.74, time=0-00:04:30)
[switchout.asean.en-th] Epoch 4.8786: train_loss/word=5.101403 (steps=2153, words/sec=7018.52, time=0-00:04:31)
[switchout.asean.en-th] Epoch 4.9301: train_loss/word=5.107080 (steps=2174, words/sec=8973.08, time=0-00:04:32)
[switchout.asean.en-th] Epoch 4.9845: train_loss/word=5.136562 (steps=2199, words/sec=7675.74, time=0-00:04:33)
[switchout.asean.en-th] Epoch 5.0000: train_loss/word=4.950922 (steps=2207, words/sec=7795.21, time=0-00:04:33)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 5.0000 dev BLEU4: 0.14398237378843629, 0.390505/0.199668/0.101436/0.054338 (BP = 1.000000, ratio=1.13, hyp_len=7667, ref_len=6809) (time=0-00:05:01)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.180523
[switchout.asean.en-th]              dev auxiliary Loss: 4.661 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 5.0010: train_loss/word=5.186537 (steps=2208, words/sec=4826.31, time=0-00:05:10)
[switchout.asean.en-th] Epoch 5.0513: train_loss/word=4.904518 (steps=2229, words/sec=9260.67, time=0-00:05:11)
[switchout.asean.en-th] Epoch 5.1015: train_loss/word=4.961696 (steps=2253, words/sec=7941.05, time=0-00:05:12)
[switchout.asean.en-th] Epoch 5.1541: train_loss/word=4.889700 (steps=2275, words/sec=8545.59, time=0-00:05:13)
[switchout.asean.en-th] Epoch 5.2057: train_loss/word=5.184162 (steps=2293, words/sec=9802.29, time=0-00:05:14)
[switchout.asean.en-th] Epoch 5.2563: train_loss/word=4.862555 (steps=2317, words/sec=8242.99, time=0-00:05:15)
[switchout.asean.en-th] Epoch 5.3075: train_loss/word=4.997995 (steps=2336, words/sec=9851.62, time=0-00:05:15)
[switchout.asean.en-th] Epoch 5.3578: train_loss/word=4.913363 (steps=2358, words/sec=7904.75, time=0-00:05:16)
[switchout.asean.en-th] Epoch 5.4082: train_loss/word=4.900398 (steps=2381, words/sec=8415.40, time=0-00:05:17)
[switchout.asean.en-th] Epoch 5.4603: train_loss/word=4.963779 (steps=2404, words/sec=7720.61, time=0-00:05:18)
[switchout.asean.en-th] Epoch 5.5106: train_loss/word=5.064572 (steps=2424, words/sec=8241.76, time=0-00:05:19)
[switchout.asean.en-th] Epoch 5.5619: train_loss/word=5.038692 (steps=2445, words/sec=8816.64, time=0-00:05:20)
[switchout.asean.en-th] Epoch 5.6137: train_loss/word=4.934272 (steps=2471, words/sec=7485.47, time=0-00:05:21)
[switchout.asean.en-th] Epoch 5.6645: train_loss/word=4.986663 (steps=2492, words/sec=8119.40, time=0-00:05:22)
[switchout.asean.en-th] Epoch 5.7150: train_loss/word=4.905803 (steps=2519, words/sec=7439.90, time=0-00:05:23)
[switchout.asean.en-th] Epoch 5.7652: train_loss/word=4.898232 (steps=2541, words/sec=8185.29, time=0-00:05:24)
[switchout.asean.en-th] Epoch 5.8172: train_loss/word=4.869975 (steps=2564, words/sec=8869.38, time=0-00:05:25)
[switchout.asean.en-th] Epoch 5.8685: train_loss/word=5.037649 (steps=2585, words/sec=8444.14, time=0-00:05:26)
[switchout.asean.en-th] Epoch 5.9193: train_loss/word=4.887094 (steps=2609, words/sec=7999.55, time=0-00:05:27)
[switchout.asean.en-th] Epoch 5.9699: train_loss/word=4.869900 (steps=2633, words/sec=8189.30, time=0-00:05:28)
[switchout.asean.en-th] Epoch 6.0000: train_loss/word=4.966499 (steps=2648, words/sec=7674.63, time=0-00:05:29)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 6.0000 dev BLEU4: 0.1610973941409846, 0.408452/0.218859/0.117407/0.064173 (BP = 1.000000, ratio=1.16, hyp_len=7903, ref_len=6809) (time=0-00:05:57)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.197093
[switchout.asean.en-th]              dev auxiliary Loss: 4.490 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 6.0026: train_loss/word=4.672691 (steps=2649, words/sec=9773.47, time=0-00:06:06)
[switchout.asean.en-th] Epoch 6.0540: train_loss/word=4.815094 (steps=2670, words/sec=8621.12, time=0-00:06:07)
[switchout.asean.en-th] Epoch 6.1043: train_loss/word=4.770992 (steps=2691, words/sec=8652.32, time=0-00:06:07)
[switchout.asean.en-th] Epoch 6.1557: train_loss/word=4.654245 (steps=2713, words/sec=8998.79, time=0-00:06:08)
[switchout.asean.en-th] Epoch 6.2062: train_loss/word=4.721359 (steps=2732, words/sec=9643.07, time=0-00:06:09)
[switchout.asean.en-th] Epoch 6.2562: train_loss/word=4.832535 (steps=2752, words/sec=9160.58, time=0-00:06:10)
[switchout.asean.en-th] Epoch 6.3102: train_loss/word=4.683936 (steps=2778, words/sec=7739.80, time=0-00:06:11)
[switchout.asean.en-th] Epoch 6.3606: train_loss/word=4.744519 (steps=2799, words/sec=8003.43, time=0-00:06:12)
[switchout.asean.en-th] Epoch 6.4111: train_loss/word=4.889856 (steps=2819, words/sec=8792.88, time=0-00:06:13)
[switchout.asean.en-th] Epoch 6.4614: train_loss/word=4.718903 (steps=2841, words/sec=7729.18, time=0-00:06:14)
[switchout.asean.en-th] Epoch 6.5130: train_loss/word=4.728427 (steps=2867, words/sec=7134.30, time=0-00:06:15)
[switchout.asean.en-th] Epoch 6.5640: train_loss/word=4.769186 (steps=2890, words/sec=8096.87, time=0-00:06:16)
[switchout.asean.en-th] Epoch 6.6174: train_loss/word=4.837114 (steps=2912, words/sec=8309.33, time=0-00:06:17)
[switchout.asean.en-th] Epoch 6.6690: train_loss/word=4.716203 (steps=2937, words/sec=7676.20, time=0-00:06:18)
[switchout.asean.en-th] Epoch 6.7202: train_loss/word=4.758514 (steps=2963, words/sec=7108.76, time=0-00:06:19)
[switchout.asean.en-th] Epoch 6.7727: train_loss/word=4.713395 (steps=2987, words/sec=8096.19, time=0-00:06:20)
[switchout.asean.en-th] Epoch 6.8231: train_loss/word=4.690875 (steps=3009, words/sec=8252.54, time=0-00:06:21)
[switchout.asean.en-th] Epoch 6.8748: train_loss/word=4.723971 (steps=3033, words/sec=7121.78, time=0-00:06:22)
[switchout.asean.en-th] Epoch 6.9250: train_loss/word=4.740772 (steps=3056, words/sec=8126.94, time=0-00:06:23)
[switchout.asean.en-th] Epoch 6.9762: train_loss/word=4.694241 (steps=3078, words/sec=8655.36, time=0-00:06:24)
[switchout.asean.en-th] Epoch 7.0000: train_loss/word=4.515318 (steps=3090, words/sec=8827.72, time=0-00:06:25)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 7.0000 dev BLEU4: 0.1845856839739022, 0.432264/0.244626/0.138207/0.079435 (BP = 1.000000, ratio=1.18, hyp_len=8009, ref_len=6809) (time=0-00:06:53)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.219154
[switchout.asean.en-th]              dev auxiliary Loss: 4.353 (ref_len=6809)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 7.0023: train_loss/word=4.092556 (steps=3091, words/sec=8331.18, time=0-00:07:03)
[switchout.asean.en-th] Epoch 7.0538: train_loss/word=4.455702 (steps=3116, words/sec=8024.83, time=0-00:07:04)
[switchout.asean.en-th] Epoch 7.1044: train_loss/word=4.506213 (steps=3139, words/sec=8284.43, time=0-00:07:05)
[switchout.asean.en-th] Epoch 7.1550: train_loss/word=4.595454 (steps=3160, words/sec=8994.20, time=0-00:07:06)
[switchout.asean.en-th] Epoch 7.2066: train_loss/word=4.562909 (steps=3183, words/sec=7010.56, time=0-00:07:07)
[switchout.asean.en-th] Epoch 7.2571: train_loss/word=4.529214 (steps=3206, words/sec=7838.01, time=0-00:07:08)
[switchout.asean.en-th] Epoch 7.3086: train_loss/word=4.506091 (steps=3228, words/sec=8297.04, time=0-00:07:09)
[switchout.asean.en-th] Epoch 7.3602: train_loss/word=4.457961 (steps=3251, words/sec=8494.07, time=0-00:07:10)
[switchout.asean.en-th] Epoch 7.4120: train_loss/word=4.558911 (steps=3275, words/sec=7635.95, time=0-00:07:11)
[switchout.asean.en-th] Epoch 7.4631: train_loss/word=4.590051 (steps=3296, words/sec=9224.67, time=0-00:07:12)
[switchout.asean.en-th] Epoch 7.5143: train_loss/word=4.514417 (steps=3321, words/sec=8105.57, time=0-00:07:13)
[switchout.asean.en-th] Epoch 7.5648: train_loss/word=4.573985 (steps=3343, words/sec=8048.79, time=0-00:07:14)
[switchout.asean.en-th] Epoch 7.6168: train_loss/word=4.500195 (steps=3367, words/sec=8253.90, time=0-00:07:15)
[switchout.asean.en-th] Epoch 7.6683: train_loss/word=4.551549 (steps=3388, words/sec=9611.05, time=0-00:07:15)
[switchout.asean.en-th] Epoch 7.7189: train_loss/word=4.576179 (steps=3409, words/sec=8937.65, time=0-00:07:16)
[switchout.asean.en-th] Epoch 7.7692: train_loss/word=4.606546 (steps=3431, words/sec=7926.37, time=0-00:07:17)
[switchout.asean.en-th] Epoch 7.8200: train_loss/word=4.594694 (steps=3456, words/sec=7118.91, time=0-00:07:18)
[switchout.asean.en-th] Epoch 7.8712: train_loss/word=4.428590 (steps=3480, words/sec=7899.98, time=0-00:07:19)
[switchout.asean.en-th] Epoch 7.9224: train_loss/word=4.528145 (steps=3503, words/sec=8151.78, time=0-00:07:20)
[switchout.asean.en-th] Epoch 7.9728: train_loss/word=4.711233 (steps=3520, words/sec=8928.11, time=0-00:07:21)
[switchout.asean.en-th] Epoch 8.0000: train_loss/word=4.704697 (steps=3531, words/sec=9651.32, time=0-00:07:21)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 8.0000 dev BLEU4: 0.20313222261396785, 0.453345/0.263950/0.153005/0.092995 (BP = 1.000000, ratio=1.16, hyp_len=7877, ref_len=6809) (time=0-00:07:49)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.234197
[switchout.asean.en-th]              dev auxiliary Loss: 4.281 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 8.0026: train_loss/word=4.585329 (steps=3532, words/sec=7866.99, time=0-00:07:59)
[switchout.asean.en-th] Epoch 8.0536: train_loss/word=4.314049 (steps=3556, words/sec=8150.73, time=0-00:08:00)
[switchout.asean.en-th] Epoch 8.1036: train_loss/word=4.398544 (steps=3580, words/sec=6895.62, time=0-00:08:01)
[switchout.asean.en-th] Epoch 8.1546: train_loss/word=4.405075 (steps=3602, words/sec=8321.85, time=0-00:08:02)
[switchout.asean.en-th] Epoch 8.2051: train_loss/word=4.611439 (steps=3622, words/sec=8146.22, time=0-00:08:03)
[switchout.asean.en-th] Epoch 8.2562: train_loss/word=4.477620 (steps=3642, words/sec=9292.40, time=0-00:08:03)
[switchout.asean.en-th] Epoch 8.3071: train_loss/word=4.354634 (steps=3665, words/sec=8731.90, time=0-00:08:04)
[switchout.asean.en-th] Epoch 8.3588: train_loss/word=4.353189 (steps=3688, words/sec=8325.50, time=0-00:08:05)
[switchout.asean.en-th] Epoch 8.4108: train_loss/word=4.374071 (steps=3710, words/sec=9085.41, time=0-00:08:06)
[switchout.asean.en-th] Epoch 8.4628: train_loss/word=4.437063 (steps=3732, words/sec=9069.90, time=0-00:08:07)
[switchout.asean.en-th] Epoch 8.5137: train_loss/word=4.363980 (steps=3756, words/sec=7366.17, time=0-00:08:08)
[switchout.asean.en-th] Epoch 8.5654: train_loss/word=4.427128 (steps=3775, words/sec=9810.08, time=0-00:08:09)
[switchout.asean.en-th] Epoch 8.6156: train_loss/word=4.435943 (steps=3799, words/sec=7090.87, time=0-00:08:10)
[switchout.asean.en-th] Epoch 8.6669: train_loss/word=4.359603 (steps=3821, words/sec=8243.13, time=0-00:08:11)
[switchout.asean.en-th] Epoch 8.7169: train_loss/word=4.411283 (steps=3844, words/sec=7250.34, time=0-00:08:12)
[switchout.asean.en-th] Epoch 8.7675: train_loss/word=4.333606 (steps=3865, words/sec=8724.03, time=0-00:08:13)
[switchout.asean.en-th] Epoch 8.8181: train_loss/word=4.486278 (steps=3888, words/sec=8569.84, time=0-00:08:14)
[switchout.asean.en-th] Epoch 8.8682: train_loss/word=4.412063 (steps=3912, words/sec=7986.46, time=0-00:08:15)
[switchout.asean.en-th] Epoch 8.9183: train_loss/word=4.511735 (steps=3933, words/sec=8883.75, time=0-00:08:16)
[switchout.asean.en-th] Epoch 8.9700: train_loss/word=4.410471 (steps=3957, words/sec=8147.48, time=0-00:08:17)
[switchout.asean.en-th] Epoch 9.0000: train_loss/word=4.317626 (steps=3971, words/sec=8714.38, time=0-00:08:17)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 9.0000 dev BLEU4: 0.21919285262754554, 0.470843/0.277989/0.167436/0.105330 (BP = 1.000000, ratio=1.12, hyp_len=7614, ref_len=6809) (time=0-00:08:45)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.245513
[switchout.asean.en-th]              dev auxiliary Loss: 4.232 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 9.0024: train_loss/word=4.290457 (steps=3972, words/sec=9516.17, time=0-00:08:54)
[switchout.asean.en-th] Epoch 9.0526: train_loss/word=4.234083 (steps=3994, words/sec=8015.40, time=0-00:08:55)
[switchout.asean.en-th] Epoch 9.1043: train_loss/word=4.310328 (steps=4018, words/sec=6732.46, time=0-00:08:56)
[switchout.asean.en-th] Epoch 9.1549: train_loss/word=4.208496 (steps=4039, words/sec=8656.83, time=0-00:08:57)
[switchout.asean.en-th] Epoch 9.2064: train_loss/word=4.331324 (steps=4060, words/sec=8689.28, time=0-00:08:58)
[switchout.asean.en-th] Epoch 9.2576: train_loss/word=4.274759 (steps=4080, words/sec=8673.07, time=0-00:08:59)
[switchout.asean.en-th] Epoch 9.3077: train_loss/word=4.173212 (steps=4103, words/sec=8426.08, time=0-00:09:00)
[switchout.asean.en-th] Epoch 9.3577: train_loss/word=4.222949 (steps=4124, words/sec=8650.79, time=0-00:09:01)
[switchout.asean.en-th] Epoch 9.4103: train_loss/word=4.295601 (steps=4145, words/sec=9586.32, time=0-00:09:01)
[switchout.asean.en-th] Epoch 9.4605: train_loss/word=4.291786 (steps=4163, words/sec=9195.04, time=0-00:09:02)
[switchout.asean.en-th] Epoch 9.5135: train_loss/word=4.306076 (steps=4188, words/sec=7885.01, time=0-00:09:03)
[switchout.asean.en-th] Epoch 9.5640: train_loss/word=4.224327 (steps=4211, words/sec=7585.65, time=0-00:09:04)
[switchout.asean.en-th] Epoch 9.6152: train_loss/word=4.235885 (steps=4235, words/sec=7811.13, time=0-00:09:05)
[switchout.asean.en-th] Epoch 9.6669: train_loss/word=4.092271 (steps=4259, words/sec=8254.54, time=0-00:09:06)
[switchout.asean.en-th] Epoch 9.7176: train_loss/word=4.281507 (steps=4281, words/sec=8530.58, time=0-00:09:07)
[switchout.asean.en-th] Epoch 9.7679: train_loss/word=4.234256 (steps=4302, words/sec=8086.42, time=0-00:09:08)
[switchout.asean.en-th] Epoch 9.8180: train_loss/word=4.189476 (steps=4327, words/sec=7703.26, time=0-00:09:09)
[switchout.asean.en-th] Epoch 9.8682: train_loss/word=4.304491 (steps=4350, words/sec=8006.94, time=0-00:09:10)
[switchout.asean.en-th] Epoch 9.9193: train_loss/word=4.197938 (steps=4374, words/sec=7823.32, time=0-00:09:11)
[switchout.asean.en-th] Epoch 9.9702: train_loss/word=4.152709 (steps=4399, words/sec=7885.01, time=0-00:09:13)
[switchout.asean.en-th] Epoch 10.0000: train_loss/word=4.294939 (steps=4413, words/sec=8351.13, time=0-00:09:13)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 10.0000 dev BLEU4: 0.23161754821176317, 0.484837/0.294284/0.178225/0.113176 (BP = 1.000000, ratio=1.14, hyp_len=7749, ref_len=6809) (time=0-00:09:41)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.259930
[switchout.asean.en-th]              dev auxiliary Loss: 4.143 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 10.0023: train_loss/word=3.972173 (steps=4414, words/sec=9575.76, time=0-00:09:50)
[switchout.asean.en-th] Epoch 10.0524: train_loss/word=4.001277 (steps=4438, words/sec=7885.85, time=0-00:09:51)
[switchout.asean.en-th] Epoch 10.1045: train_loss/word=4.097950 (steps=4460, words/sec=8589.52, time=0-00:09:52)
[switchout.asean.en-th] Epoch 10.1549: train_loss/word=4.157062 (steps=4482, words/sec=8770.35, time=0-00:09:53)
[switchout.asean.en-th] Epoch 10.2058: train_loss/word=4.184987 (steps=4503, words/sec=8516.25, time=0-00:09:54)
[switchout.asean.en-th] Epoch 10.2567: train_loss/word=4.108164 (steps=4528, words/sec=7445.46, time=0-00:09:55)
[switchout.asean.en-th] Epoch 10.3077: train_loss/word=4.169720 (steps=4550, words/sec=8544.51, time=0-00:09:56)
[switchout.asean.en-th] Epoch 10.3581: train_loss/word=4.175859 (steps=4573, words/sec=7928.17, time=0-00:09:57)
[switchout.asean.en-th] Epoch 10.4102: train_loss/word=4.149665 (steps=4595, words/sec=8262.67, time=0-00:09:58)
[switchout.asean.en-th] Epoch 10.4623: train_loss/word=4.218543 (steps=4616, words/sec=9018.45, time=0-00:09:59)
[switchout.asean.en-th] Epoch 10.5131: train_loss/word=4.125487 (steps=4639, words/sec=7580.96, time=0-00:10:00)
[switchout.asean.en-th] Epoch 10.5633: train_loss/word=4.159749 (steps=4659, words/sec=8740.17, time=0-00:10:00)
[switchout.asean.en-th] Epoch 10.6144: train_loss/word=4.022529 (steps=4684, words/sec=7464.82, time=0-00:10:02)
[switchout.asean.en-th] Epoch 10.6652: train_loss/word=4.038269 (steps=4708, words/sec=8297.92, time=0-00:10:03)
[switchout.asean.en-th] Epoch 10.7165: train_loss/word=4.039754 (steps=4731, words/sec=8617.78, time=0-00:10:04)
[switchout.asean.en-th] Epoch 10.7714: train_loss/word=4.200525 (steps=4749, words/sec=8023.00, time=0-00:10:04)
[switchout.asean.en-th] Epoch 10.8214: train_loss/word=4.249304 (steps=4770, words/sec=9114.10, time=0-00:10:05)
[switchout.asean.en-th] Epoch 10.8716: train_loss/word=4.227981 (steps=4794, words/sec=7213.42, time=0-00:10:06)
[switchout.asean.en-th] Epoch 10.9230: train_loss/word=4.094457 (steps=4819, words/sec=7604.89, time=0-00:10:07)
[switchout.asean.en-th] Epoch 10.9735: train_loss/word=4.145707 (steps=4843, words/sec=7740.58, time=0-00:10:08)
[switchout.asean.en-th] Epoch 11.0000: train_loss/word=4.169765 (steps=4855, words/sec=8269.49, time=0-00:10:09)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 11.0000 dev BLEU4: 0.24418340501340072, 0.501639/0.304974/0.188509/0.123276 (BP = 1.000000, ratio=1.12, hyp_len=7625, ref_len=6809) (time=0-00:10:36)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.269618
[switchout.asean.en-th]              dev auxiliary Loss: 4.124 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 11.0024: train_loss/word=4.612216 (steps=4856, words/sec=7515.65, time=0-00:10:46)
[switchout.asean.en-th] Epoch 11.0544: train_loss/word=3.901640 (steps=4880, words/sec=8065.68, time=0-00:10:47)
[switchout.asean.en-th] Epoch 11.1069: train_loss/word=3.926542 (steps=4899, words/sec=8214.99, time=0-00:10:48)
[switchout.asean.en-th] Epoch 11.1591: train_loss/word=4.102644 (steps=4921, words/sec=8009.01, time=0-00:10:48)
[switchout.asean.en-th] Epoch 11.2114: train_loss/word=4.008595 (steps=4942, words/sec=8125.73, time=0-00:10:49)
[switchout.asean.en-th] Epoch 11.2647: train_loss/word=3.971469 (steps=4967, words/sec=6858.92, time=0-00:10:51)
[switchout.asean.en-th] Epoch 11.3172: train_loss/word=4.035332 (steps=4991, words/sec=8315.98, time=0-00:10:52)
[switchout.asean.en-th] Epoch 11.3703: train_loss/word=3.913407 (steps=5014, words/sec=7538.43, time=0-00:10:53)
[switchout.asean.en-th] Epoch 11.4216: train_loss/word=4.066691 (steps=5037, words/sec=8406.97, time=0-00:10:54)
[switchout.asean.en-th] Epoch 11.4719: train_loss/word=4.066752 (steps=5058, words/sec=6948.10, time=0-00:10:55)
[switchout.asean.en-th] Epoch 11.5225: train_loss/word=4.064016 (steps=5079, words/sec=7303.79, time=0-00:10:55)
[switchout.asean.en-th] Epoch 11.5726: train_loss/word=4.072081 (steps=5102, words/sec=7970.07, time=0-00:10:56)
[switchout.asean.en-th] Epoch 11.6238: train_loss/word=3.885947 (steps=5125, words/sec=8424.56, time=0-00:10:57)
[switchout.asean.en-th] Epoch 11.6741: train_loss/word=3.806297 (steps=5152, words/sec=6528.68, time=0-00:10:59)
[switchout.asean.en-th] Epoch 11.7254: train_loss/word=3.913087 (steps=5175, words/sec=7755.28, time=0-00:11:00)
[switchout.asean.en-th] Epoch 11.7758: train_loss/word=4.157458 (steps=5197, words/sec=7738.64, time=0-00:11:01)
[switchout.asean.en-th] Epoch 11.8262: train_loss/word=4.009823 (steps=5222, words/sec=7395.09, time=0-00:11:02)
[switchout.asean.en-th] Epoch 11.8774: train_loss/word=4.092336 (steps=5244, words/sec=7672.09, time=0-00:11:03)
[switchout.asean.en-th] Epoch 11.9294: train_loss/word=4.255223 (steps=5264, words/sec=9189.69, time=0-00:11:04)
[switchout.asean.en-th] Epoch 11.9800: train_loss/word=3.991399 (steps=5287, words/sec=8273.74, time=0-00:11:05)
[switchout.asean.en-th] Epoch 12.0000: train_loss/word=3.908027 (steps=5297, words/sec=7673.60, time=0-00:11:05)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 12.0000 dev BLEU4: 0.2567971073631453, 0.509530/0.314980/0.200211/0.135338 (BP = 1.000000, ratio=1.12, hyp_len=7660, ref_len=6809) (time=0-00:11:33)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.282349
[switchout.asean.en-th]              dev auxiliary Loss: 4.105 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 12.0017: train_loss/word=3.587619 (steps=5298, words/sec=7402.71, time=0-00:11:43)
[switchout.asean.en-th] Epoch 12.0523: train_loss/word=4.047974 (steps=5318, words/sec=8617.73, time=0-00:11:43)
[switchout.asean.en-th] Epoch 12.1036: train_loss/word=3.909300 (steps=5340, words/sec=8390.80, time=0-00:11:44)
[switchout.asean.en-th] Epoch 12.1549: train_loss/word=3.864091 (steps=5364, words/sec=7587.76, time=0-00:11:45)
[switchout.asean.en-th] Epoch 12.2065: train_loss/word=3.867685 (steps=5387, words/sec=7663.03, time=0-00:11:46)
[switchout.asean.en-th] Epoch 12.2565: train_loss/word=3.858124 (steps=5409, words/sec=8097.70, time=0-00:11:47)
[switchout.asean.en-th] Epoch 12.3067: train_loss/word=3.813228 (steps=5431, words/sec=8522.59, time=0-00:11:48)
[switchout.asean.en-th] Epoch 12.3582: train_loss/word=3.867918 (steps=5456, words/sec=7342.29, time=0-00:11:49)
[switchout.asean.en-th] Epoch 12.4106: train_loss/word=3.859883 (steps=5477, words/sec=8820.59, time=0-00:11:50)
[switchout.asean.en-th] Epoch 12.4618: train_loss/word=4.015721 (steps=5497, words/sec=9244.75, time=0-00:11:51)
[switchout.asean.en-th] Epoch 12.5146: train_loss/word=4.008920 (steps=5517, words/sec=9459.40, time=0-00:11:52)
[switchout.asean.en-th] Epoch 12.5656: train_loss/word=3.817951 (steps=5544, words/sec=7069.15, time=0-00:11:53)
[switchout.asean.en-th] Epoch 12.6161: train_loss/word=3.986467 (steps=5566, words/sec=6880.71, time=0-00:11:54)
[switchout.asean.en-th] Epoch 12.6695: train_loss/word=3.858802 (steps=5589, words/sec=8244.06, time=0-00:11:55)
[switchout.asean.en-th] Epoch 12.7199: train_loss/word=3.966361 (steps=5610, words/sec=8046.13, time=0-00:11:56)
[switchout.asean.en-th] Epoch 12.7701: train_loss/word=3.912659 (steps=5633, words/sec=7752.02, time=0-00:11:57)
[switchout.asean.en-th] Epoch 12.8223: train_loss/word=3.746898 (steps=5661, words/sec=7346.95, time=0-00:11:58)
[switchout.asean.en-th] Epoch 12.8732: train_loss/word=3.883330 (steps=5684, words/sec=7683.35, time=0-00:11:59)
[switchout.asean.en-th] Epoch 12.9244: train_loss/word=4.048621 (steps=5705, words/sec=7890.09, time=0-00:12:00)
[switchout.asean.en-th] Epoch 12.9750: train_loss/word=3.966268 (steps=5727, words/sec=8165.75, time=0-00:12:01)
[switchout.asean.en-th] Epoch 13.0000: train_loss/word=4.109697 (steps=5737, words/sec=9524.61, time=0-00:12:02)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 13.0000 dev BLEU4: 0.26885017894475793, 0.517435/0.328788/0.212581/0.144459 (BP = 1.000000, ratio=1.10, hyp_len=7485, ref_len=6809) (time=0-00:12:29)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.289048
[switchout.asean.en-th]              dev auxiliary Loss: 4.101 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 13.0027: train_loss/word=3.824143 (steps=5738, words/sec=10263.99, time=0-00:12:39)
[switchout.asean.en-th] Epoch 13.0528: train_loss/word=3.632943 (steps=5762, words/sec=8216.56, time=0-00:12:40)
[switchout.asean.en-th] Epoch 13.1042: train_loss/word=3.747092 (steps=5782, words/sec=8902.99, time=0-00:12:40)
[switchout.asean.en-th] Epoch 13.1545: train_loss/word=3.738633 (steps=5806, words/sec=8040.69, time=0-00:12:41)
[switchout.asean.en-th] Epoch 13.2051: train_loss/word=3.777737 (steps=5828, words/sec=8269.10, time=0-00:12:42)
[switchout.asean.en-th] Epoch 13.2593: train_loss/word=3.707014 (steps=5852, words/sec=7923.28, time=0-00:12:43)
[switchout.asean.en-th] Epoch 13.3103: train_loss/word=3.926052 (steps=5873, words/sec=9058.10, time=0-00:12:44)
[switchout.asean.en-th] Epoch 13.3617: train_loss/word=3.812268 (steps=5897, words/sec=8006.84, time=0-00:12:45)
[switchout.asean.en-th] Epoch 13.4135: train_loss/word=3.946171 (steps=5919, words/sec=8299.93, time=0-00:12:46)
[switchout.asean.en-th] Epoch 13.4652: train_loss/word=3.722507 (steps=5945, words/sec=7643.94, time=0-00:12:47)
[switchout.asean.en-th] Epoch 13.5167: train_loss/word=3.934927 (steps=5966, words/sec=8310.39, time=0-00:12:48)
[switchout.asean.en-th] Epoch 13.5682: train_loss/word=3.859856 (steps=5989, words/sec=7943.16, time=0-00:12:49)
[switchout.asean.en-th] Epoch 13.6211: train_loss/word=3.965180 (steps=6010, words/sec=8175.23, time=0-00:12:50)
[switchout.asean.en-th] Epoch 13.6719: train_loss/word=3.846411 (steps=6036, words/sec=5808.61, time=0-00:12:51)
[switchout.asean.en-th] Epoch 13.7248: train_loss/word=3.976438 (steps=6057, words/sec=8590.24, time=0-00:12:52)
[switchout.asean.en-th] Epoch 13.7760: train_loss/word=3.815181 (steps=6080, words/sec=9136.81, time=0-00:12:53)
[switchout.asean.en-th] Epoch 13.8275: train_loss/word=3.692615 (steps=6104, words/sec=8104.37, time=0-00:12:54)
[switchout.asean.en-th] Epoch 13.8785: train_loss/word=3.773553 (steps=6129, words/sec=7654.15, time=0-00:12:55)
[switchout.asean.en-th] Epoch 13.9312: train_loss/word=3.904677 (steps=6151, words/sec=8693.20, time=0-00:12:56)
[switchout.asean.en-th] Epoch 13.9847: train_loss/word=3.866085 (steps=6173, words/sec=9258.22, time=0-00:12:57)
[switchout.asean.en-th] Epoch 14.0000: train_loss/word=3.871169 (steps=6179, words/sec=9522.02, time=0-00:12:57)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 14.0000 dev BLEU4: 0.2756717861478297, 0.522049/0.332875/0.218049/0.152413 (BP = 1.000000, ratio=1.11, hyp_len=7574, ref_len=6809) (time=0-00:13:25)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.297276
[switchout.asean.en-th]              dev auxiliary Loss: 4.102 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 14.0016: train_loss/word=3.181609 (steps=6180, words/sec=6948.15, time=0-00:13:34)
[switchout.asean.en-th] Epoch 14.0519: train_loss/word=3.619870 (steps=6202, words/sec=8474.78, time=0-00:13:35)
[switchout.asean.en-th] Epoch 14.1035: train_loss/word=3.706019 (steps=6225, words/sec=8752.09, time=0-00:13:36)
[switchout.asean.en-th] Epoch 14.1544: train_loss/word=3.681713 (steps=6249, words/sec=7194.57, time=0-00:13:37)
[switchout.asean.en-th] Epoch 14.2047: train_loss/word=3.779736 (steps=6269, words/sec=9198.11, time=0-00:13:38)
[switchout.asean.en-th] Epoch 14.2565: train_loss/word=3.896721 (steps=6290, words/sec=7714.76, time=0-00:13:39)
[switchout.asean.en-th] Epoch 14.3070: train_loss/word=3.736016 (steps=6313, words/sec=8464.75, time=0-00:13:40)
[switchout.asean.en-th] Epoch 14.3578: train_loss/word=3.591179 (steps=6340, words/sec=7681.80, time=0-00:13:41)
[switchout.asean.en-th] Epoch 14.4079: train_loss/word=3.671031 (steps=6364, words/sec=8251.65, time=0-00:13:42)
[switchout.asean.en-th] Epoch 14.4606: train_loss/word=3.801716 (steps=6387, words/sec=7935.93, time=0-00:13:43)
[switchout.asean.en-th] Epoch 14.5128: train_loss/word=3.803698 (steps=6409, words/sec=8923.50, time=0-00:13:44)
[switchout.asean.en-th] Epoch 14.5658: train_loss/word=3.811512 (steps=6432, words/sec=7647.93, time=0-00:13:45)
[switchout.asean.en-th] Epoch 14.6171: train_loss/word=3.730168 (steps=6454, words/sec=8826.92, time=0-00:13:46)
[switchout.asean.en-th] Epoch 14.6684: train_loss/word=3.744022 (steps=6477, words/sec=8330.40, time=0-00:13:47)
[switchout.asean.en-th] Epoch 14.7190: train_loss/word=3.555729 (steps=6503, words/sec=7487.23, time=0-00:13:48)
[switchout.asean.en-th] Epoch 14.7709: train_loss/word=3.793149 (steps=6526, words/sec=8283.30, time=0-00:13:49)
[switchout.asean.en-th] Epoch 14.8243: train_loss/word=3.868062 (steps=6548, words/sec=8471.76, time=0-00:13:50)
[switchout.asean.en-th] Epoch 14.8756: train_loss/word=3.834814 (steps=6568, words/sec=8932.34, time=0-00:13:51)
[switchout.asean.en-th] Epoch 14.9276: train_loss/word=3.809247 (steps=6591, words/sec=8555.87, time=0-00:13:52)
[switchout.asean.en-th] Epoch 14.9787: train_loss/word=3.930949 (steps=6611, words/sec=9501.00, time=0-00:13:53)
[switchout.asean.en-th] Epoch 15.0000: train_loss/word=3.932894 (steps=6620, words/sec=7952.02, time=0-00:13:53)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 15.0000 dev BLEU4: 0.2916109418240777, 0.534969/0.348826/0.234161/0.165487 (BP = 1.000000, ratio=1.08, hyp_len=7335, ref_len=6809) (time=0-00:14:20)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.303533
[switchout.asean.en-th]              dev auxiliary Loss: 4.030 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 15.0018: train_loss/word=3.484472 (steps=6621, words/sec=6827.13, time=0-00:14:30)
[switchout.asean.en-th] Epoch 15.0519: train_loss/word=3.701978 (steps=6641, words/sec=7732.02, time=0-00:14:30)
[switchout.asean.en-th] Epoch 15.1035: train_loss/word=3.678458 (steps=6663, words/sec=7855.60, time=0-00:14:31)
[switchout.asean.en-th] Epoch 15.1559: train_loss/word=3.572009 (steps=6688, words/sec=8049.09, time=0-00:14:33)
[switchout.asean.en-th] Epoch 15.2077: train_loss/word=3.715377 (steps=6709, words/sec=8744.01, time=0-00:14:33)
[switchout.asean.en-th] Epoch 15.2610: train_loss/word=3.667954 (steps=6732, words/sec=8691.57, time=0-00:14:34)
[switchout.asean.en-th] Epoch 15.3123: train_loss/word=3.701585 (steps=6754, words/sec=8834.90, time=0-00:14:35)
[switchout.asean.en-th] Epoch 15.3629: train_loss/word=3.746158 (steps=6776, words/sec=8053.54, time=0-00:14:36)
[switchout.asean.en-th] Epoch 15.4138: train_loss/word=3.487626 (steps=6800, words/sec=8364.60, time=0-00:14:37)
[switchout.asean.en-th] Epoch 15.4650: train_loss/word=3.650741 (steps=6822, words/sec=8754.24, time=0-00:14:38)
[switchout.asean.en-th] Epoch 15.5165: train_loss/word=3.527959 (steps=6847, words/sec=8141.01, time=0-00:14:39)
[switchout.asean.en-th] Epoch 15.5697: train_loss/word=3.675289 (steps=6869, words/sec=9212.25, time=0-00:14:40)
[switchout.asean.en-th] Epoch 15.6214: train_loss/word=3.687987 (steps=6890, words/sec=9193.09, time=0-00:14:41)
[switchout.asean.en-th] Epoch 15.6740: train_loss/word=3.666800 (steps=6912, words/sec=8095.47, time=0-00:14:42)
[switchout.asean.en-th] Epoch 15.7247: train_loss/word=3.732257 (steps=6934, words/sec=7724.45, time=0-00:14:43)
[switchout.asean.en-th] Epoch 15.7757: train_loss/word=3.670912 (steps=6958, words/sec=8505.42, time=0-00:14:44)
[switchout.asean.en-th] Epoch 15.8273: train_loss/word=3.642922 (steps=6984, words/sec=7758.44, time=0-00:14:45)
[switchout.asean.en-th] Epoch 15.8809: train_loss/word=3.649719 (steps=7007, words/sec=8337.76, time=0-00:14:46)
[switchout.asean.en-th] Epoch 15.9338: train_loss/word=3.708629 (steps=7030, words/sec=8524.48, time=0-00:14:47)
[switchout.asean.en-th] Epoch 15.9844: train_loss/word=3.643511 (steps=7053, words/sec=8550.43, time=0-00:14:48)
[switchout.asean.en-th] Epoch 16.0000: train_loss/word=3.780595 (steps=7061, words/sec=6058.53, time=0-00:14:48)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 16.0000 dev BLEU4: 0.2952694542883858, 0.546608/0.354352/0.234157/0.167593 (BP = 1.000000, ratio=1.08, hyp_len=7327, ref_len=6809) (time=0-00:15:15)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.312145
[switchout.asean.en-th]              dev auxiliary Loss: 4.020 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 16.0029: train_loss/word=2.971554 (steps=7062, words/sec=12230.40, time=0-00:15:24)
[switchout.asean.en-th] Epoch 16.0543: train_loss/word=3.611048 (steps=7085, words/sec=8608.34, time=0-00:15:25)
[switchout.asean.en-th] Epoch 16.1066: train_loss/word=3.415189 (steps=7112, words/sec=7501.87, time=0-00:15:26)
[switchout.asean.en-th] Epoch 16.1577: train_loss/word=3.509994 (steps=7135, words/sec=9051.14, time=0-00:15:27)
[switchout.asean.en-th] Epoch 16.2089: train_loss/word=3.624496 (steps=7157, words/sec=8865.98, time=0-00:15:28)
[switchout.asean.en-th] Epoch 16.2600: train_loss/word=3.676174 (steps=7180, words/sec=7379.10, time=0-00:15:29)
[switchout.asean.en-th] Epoch 16.3120: train_loss/word=3.632881 (steps=7202, words/sec=8340.62, time=0-00:15:30)
[switchout.asean.en-th] Epoch 16.3627: train_loss/word=3.654576 (steps=7223, words/sec=8080.12, time=0-00:15:31)
[switchout.asean.en-th] Epoch 16.4139: train_loss/word=3.562705 (steps=7244, words/sec=9830.33, time=0-00:15:32)
[switchout.asean.en-th] Epoch 16.4648: train_loss/word=3.469942 (steps=7271, words/sec=7378.10, time=0-00:15:33)
[switchout.asean.en-th] Epoch 16.5159: train_loss/word=3.716676 (steps=7291, words/sec=9156.16, time=0-00:15:34)
[switchout.asean.en-th] Epoch 16.5669: train_loss/word=3.566319 (steps=7312, words/sec=9161.89, time=0-00:15:35)
[switchout.asean.en-th] Epoch 16.6173: train_loss/word=3.688785 (steps=7331, words/sec=9384.24, time=0-00:15:35)
[switchout.asean.en-th] Epoch 16.6681: train_loss/word=3.538613 (steps=7354, words/sec=8255.83, time=0-00:15:36)
[switchout.asean.en-th] Epoch 16.7183: train_loss/word=3.497114 (steps=7380, words/sec=8008.24, time=0-00:15:37)
[switchout.asean.en-th] Epoch 16.7696: train_loss/word=3.584931 (steps=7402, words/sec=7915.54, time=0-00:15:38)
[switchout.asean.en-th] Epoch 16.8209: train_loss/word=3.550936 (steps=7424, words/sec=8714.04, time=0-00:15:39)
[switchout.asean.en-th] Epoch 16.8711: train_loss/word=3.594458 (steps=7448, words/sec=7582.24, time=0-00:15:40)
[switchout.asean.en-th] Epoch 16.9232: train_loss/word=3.639249 (steps=7470, words/sec=8091.59, time=0-00:15:41)
[switchout.asean.en-th] Epoch 16.9740: train_loss/word=3.699004 (steps=7491, words/sec=8811.75, time=0-00:15:42)
[switchout.asean.en-th] Epoch 17.0000: train_loss/word=3.661245 (steps=7502, words/sec=9211.47, time=0-00:15:43)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 17.0000 dev BLEU4: 0.2953183702114832, 0.537593/0.352778/0.236984/0.169234 (BP = 1.000000, ratio=1.11, hyp_len=7528, ref_len=6809) (time=0-00:16:10)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.312396
[switchout.asean.en-th]              dev auxiliary Loss: 4.024 (ref_len=6809)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 17.0026: train_loss/word=3.946170 (steps=7503, words/sec=8571.96, time=0-00:16:20)
[switchout.asean.en-th] Epoch 17.0526: train_loss/word=3.395217 (steps=7526, words/sec=7735.70, time=0-00:16:21)
[switchout.asean.en-th] Epoch 17.1031: train_loss/word=3.359592 (steps=7547, words/sec=8503.10, time=0-00:16:22)
[switchout.asean.en-th] Epoch 17.1548: train_loss/word=3.592441 (steps=7569, words/sec=8843.44, time=0-00:16:22)
[switchout.asean.en-th] Epoch 17.2060: train_loss/word=3.337186 (steps=7594, words/sec=8363.06, time=0-00:16:24)
[switchout.asean.en-th] Epoch 17.2585: train_loss/word=3.630902 (steps=7616, words/sec=8430.67, time=0-00:16:24)
[switchout.asean.en-th] Epoch 17.3094: train_loss/word=3.647958 (steps=7636, words/sec=9662.99, time=0-00:16:25)
[switchout.asean.en-th] Epoch 17.3613: train_loss/word=3.430300 (steps=7659, words/sec=8968.93, time=0-00:16:26)
[switchout.asean.en-th] Epoch 17.4127: train_loss/word=3.553835 (steps=7682, words/sec=7934.37, time=0-00:16:27)
[switchout.asean.en-th] Epoch 17.4638: train_loss/word=3.539159 (steps=7707, words/sec=7936.55, time=0-00:16:28)
[switchout.asean.en-th] Epoch 17.5155: train_loss/word=3.646934 (steps=7727, words/sec=9641.57, time=0-00:16:29)
[switchout.asean.en-th] Epoch 17.5662: train_loss/word=3.570782 (steps=7749, words/sec=8625.41, time=0-00:16:30)
[switchout.asean.en-th] Epoch 17.6178: train_loss/word=3.585998 (steps=7771, words/sec=8944.23, time=0-00:16:31)
[switchout.asean.en-th] Epoch 17.6686: train_loss/word=3.568298 (steps=7793, words/sec=8500.52, time=0-00:16:32)
[switchout.asean.en-th] Epoch 17.7192: train_loss/word=3.529187 (steps=7816, words/sec=8494.55, time=0-00:16:33)
[switchout.asean.en-th] Epoch 17.7704: train_loss/word=3.483740 (steps=7842, words/sec=6999.28, time=0-00:16:34)
[switchout.asean.en-th] Epoch 17.8217: train_loss/word=3.533830 (steps=7866, words/sec=7703.86, time=0-00:16:35)
[switchout.asean.en-th] Epoch 17.8737: train_loss/word=3.395085 (steps=7890, words/sec=8068.68, time=0-00:16:36)
[switchout.asean.en-th] Epoch 17.9267: train_loss/word=3.641431 (steps=7915, words/sec=7642.31, time=0-00:16:37)
[switchout.asean.en-th] Epoch 17.9767: train_loss/word=3.769792 (steps=7934, words/sec=8837.86, time=0-00:16:38)
[switchout.asean.en-th] Epoch 18.0000: train_loss/word=3.697983 (steps=7943, words/sec=9298.02, time=0-00:16:38)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 18.0000 dev BLEU4: 0.31018853154548076, 0.548432/0.364858/0.249810/0.185202 (BP = 1.000000, ratio=1.06, hyp_len=7206, ref_len=6809) (time=0-00:17:04)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.317082
[switchout.asean.en-th]              dev auxiliary Loss: 3.988 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 18.0026: train_loss/word=3.453762 (steps=7944, words/sec=10488.46, time=0-00:17:14)
[switchout.asean.en-th] Epoch 18.0535: train_loss/word=3.437669 (steps=7966, words/sec=8253.72, time=0-00:17:14)
[switchout.asean.en-th] Epoch 18.1056: train_loss/word=3.431111 (steps=7990, words/sec=7980.81, time=0-00:17:15)
[switchout.asean.en-th] Epoch 18.1573: train_loss/word=3.534677 (steps=8012, words/sec=9016.53, time=0-00:17:16)
[switchout.asean.en-th] Epoch 18.2078: train_loss/word=3.365012 (steps=8036, words/sec=8760.78, time=0-00:17:17)
[switchout.asean.en-th] Epoch 18.2581: train_loss/word=3.597873 (steps=8057, words/sec=7477.08, time=0-00:17:18)
[switchout.asean.en-th] Epoch 18.3095: train_loss/word=3.346799 (steps=8082, words/sec=7884.61, time=0-00:17:19)
[switchout.asean.en-th] Epoch 18.3625: train_loss/word=3.526025 (steps=8105, words/sec=7650.27, time=0-00:17:20)
[switchout.asean.en-th] Epoch 18.4127: train_loss/word=3.429270 (steps=8127, words/sec=8666.67, time=0-00:17:21)
[switchout.asean.en-th] Epoch 18.4633: train_loss/word=3.487490 (steps=8149, words/sec=8897.75, time=0-00:17:22)
[switchout.asean.en-th] Epoch 18.5158: train_loss/word=3.675312 (steps=8167, words/sec=10114.62, time=0-00:17:23)
[switchout.asean.en-th] Epoch 18.5673: train_loss/word=3.647951 (steps=8186, words/sec=9666.26, time=0-00:17:23)
[switchout.asean.en-th] Epoch 18.6187: train_loss/word=3.478804 (steps=8208, words/sec=8949.69, time=0-00:17:24)
[switchout.asean.en-th] Epoch 18.6705: train_loss/word=3.629050 (steps=8229, words/sec=8334.02, time=0-00:17:25)
[switchout.asean.en-th] Epoch 18.7229: train_loss/word=3.533526 (steps=8253, words/sec=8335.86, time=0-00:17:26)
[switchout.asean.en-th] Epoch 18.7743: train_loss/word=3.268358 (steps=8279, words/sec=8531.30, time=0-00:17:27)
[switchout.asean.en-th] Epoch 18.8264: train_loss/word=3.489242 (steps=8304, words/sec=7905.37, time=0-00:17:28)
[switchout.asean.en-th] Epoch 18.8784: train_loss/word=3.514567 (steps=8327, words/sec=7990.86, time=0-00:17:29)
[switchout.asean.en-th] Epoch 18.9298: train_loss/word=3.351294 (steps=8354, words/sec=7281.05, time=0-00:17:31)
[switchout.asean.en-th] Epoch 18.9799: train_loss/word=3.542673 (steps=8374, words/sec=9006.52, time=0-00:17:32)
[switchout.asean.en-th] Epoch 19.0000: train_loss/word=3.550822 (steps=8384, words/sec=7806.68, time=0-00:17:32)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 19.0000 dev BLEU4: 0.3163784257225973, 0.560165/0.374394/0.255390/0.187059 (BP = 1.000000, ratio=1.03, hyp_len=7014, ref_len=6809) (time=0-00:17:58)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.320837
[switchout.asean.en-th]              dev auxiliary Loss: 4.008 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 19.0021: train_loss/word=2.787358 (steps=8385, words/sec=10248.71, time=0-00:18:07)
[switchout.asean.en-th] Epoch 19.0542: train_loss/word=3.384794 (steps=8408, words/sec=8624.00, time=0-00:18:08)
[switchout.asean.en-th] Epoch 19.1058: train_loss/word=3.381632 (steps=8430, words/sec=9110.59, time=0-00:18:09)
[switchout.asean.en-th] Epoch 19.1575: train_loss/word=3.557239 (steps=8453, words/sec=8280.10, time=0-00:18:10)
[switchout.asean.en-th] Epoch 19.2076: train_loss/word=3.240312 (steps=8477, words/sec=7613.97, time=0-00:18:11)
[switchout.asean.en-th] Epoch 19.2594: train_loss/word=3.421024 (steps=8498, words/sec=8280.64, time=0-00:18:12)
[switchout.asean.en-th] Epoch 19.3099: train_loss/word=3.403777 (steps=8520, words/sec=9284.67, time=0-00:18:13)
[switchout.asean.en-th] Epoch 19.3637: train_loss/word=3.538358 (steps=8539, words/sec=9594.30, time=0-00:18:14)
[switchout.asean.en-th] Epoch 19.4152: train_loss/word=3.349647 (steps=8564, words/sec=7626.60, time=0-00:18:15)
[switchout.asean.en-th] Epoch 19.4682: train_loss/word=3.494522 (steps=8587, words/sec=8489.66, time=0-00:18:16)
[switchout.asean.en-th] Epoch 19.5185: train_loss/word=3.348434 (steps=8611, words/sec=7581.23, time=0-00:18:17)
[switchout.asean.en-th] Epoch 19.5706: train_loss/word=3.315785 (steps=8637, words/sec=7440.42, time=0-00:18:18)
[switchout.asean.en-th] Epoch 19.6213: train_loss/word=3.330372 (steps=8660, words/sec=8681.30, time=0-00:18:19)
[switchout.asean.en-th] Epoch 19.6720: train_loss/word=3.761507 (steps=8678, words/sec=10048.87, time=0-00:18:20)
[switchout.asean.en-th] Epoch 19.7236: train_loss/word=3.357256 (steps=8704, words/sec=7109.65, time=0-00:18:21)
[switchout.asean.en-th] Epoch 19.7746: train_loss/word=3.349461 (steps=8729, words/sec=8340.51, time=0-00:18:22)
[switchout.asean.en-th] Epoch 19.8264: train_loss/word=3.639984 (steps=8750, words/sec=8484.84, time=0-00:18:23)
[switchout.asean.en-th] Epoch 19.8767: train_loss/word=3.398938 (steps=8774, words/sec=8405.17, time=0-00:18:24)
[switchout.asean.en-th] Epoch 19.9285: train_loss/word=3.586365 (steps=8795, words/sec=8967.34, time=0-00:18:25)
[switchout.asean.en-th] Epoch 19.9793: train_loss/word=3.547082 (steps=8816, words/sec=8503.79, time=0-00:18:25)
[switchout.asean.en-th] Epoch 20.0000: train_loss/word=3.561644 (steps=8826, words/sec=8046.09, time=0-00:18:26)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 20.0000 dev BLEU4: 0.3184701320253347, 0.555525/0.374576/0.258630/0.191140 (BP = 1.000000, ratio=1.06, hyp_len=7222, ref_len=6809) (time=0-00:18:52)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.327814
[switchout.asean.en-th]              dev auxiliary Loss: 4.018 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 20.0030: train_loss/word=3.820234 (steps=8827, words/sec=11002.74, time=0-00:19:02)
[switchout.asean.en-th] Epoch 20.0533: train_loss/word=3.480205 (steps=8848, words/sec=9215.17, time=0-00:19:02)
[switchout.asean.en-th] Epoch 20.1036: train_loss/word=3.354479 (steps=8869, words/sec=8757.48, time=0-00:19:03)
[switchout.asean.en-th] Epoch 20.1536: train_loss/word=3.331780 (steps=8891, words/sec=8399.95, time=0-00:19:04)
[switchout.asean.en-th] Epoch 20.2046: train_loss/word=3.270055 (steps=8914, words/sec=8864.28, time=0-00:19:05)
[switchout.asean.en-th] Epoch 20.2560: train_loss/word=3.370651 (steps=8938, words/sec=8202.16, time=0-00:19:06)
[switchout.asean.en-th] Epoch 20.3073: train_loss/word=3.314990 (steps=8962, words/sec=8113.38, time=0-00:19:07)
[switchout.asean.en-th] Epoch 20.3603: train_loss/word=3.366783 (steps=8984, words/sec=8798.66, time=0-00:19:08)
[switchout.asean.en-th] Epoch 20.4104: train_loss/word=3.447438 (steps=9005, words/sec=8204.14, time=0-00:19:09)
[switchout.asean.en-th] Epoch 20.4621: train_loss/word=3.453239 (steps=9026, words/sec=9108.97, time=0-00:19:10)
[switchout.asean.en-th] Epoch 20.5129: train_loss/word=3.236931 (steps=9055, words/sec=6824.85, time=0-00:19:11)
[switchout.asean.en-th] Epoch 20.5646: train_loss/word=3.287723 (steps=9080, words/sec=8375.76, time=0-00:19:12)
[switchout.asean.en-th] Epoch 20.6149: train_loss/word=3.486522 (steps=9100, words/sec=8400.28, time=0-00:19:13)
[switchout.asean.en-th] Epoch 20.6654: train_loss/word=3.442326 (steps=9123, words/sec=8206.42, time=0-00:19:14)
[switchout.asean.en-th] Epoch 20.7185: train_loss/word=3.244075 (steps=9148, words/sec=7991.13, time=0-00:19:15)
[switchout.asean.en-th] Epoch 20.7692: train_loss/word=3.431236 (steps=9170, words/sec=8333.88, time=0-00:19:16)
[switchout.asean.en-th] Epoch 20.8212: train_loss/word=3.462173 (steps=9192, words/sec=8011.29, time=0-00:19:17)
[switchout.asean.en-th] Epoch 20.8727: train_loss/word=3.522512 (steps=9214, words/sec=8961.74, time=0-00:19:18)
[switchout.asean.en-th] Epoch 20.9236: train_loss/word=3.596934 (steps=9234, words/sec=9007.61, time=0-00:19:19)
[switchout.asean.en-th] Epoch 20.9753: train_loss/word=3.399881 (steps=9257, words/sec=8414.92, time=0-00:19:20)
[switchout.asean.en-th] Epoch 21.0000: train_loss/word=3.320070 (steps=9269, words/sec=8152.11, time=0-00:19:20)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 21.0000 dev BLEU4: 0.3166909614817618, 0.546767/0.367121/0.259287/0.193264 (BP = 1.000000, ratio=1.08, hyp_len=7345, ref_len=6809) (time=0-00:19:47)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.324507
[switchout.asean.en-th]              dev auxiliary Loss: 4.008 (ref_len=6809)
             checkpoint took 0-00:00:27
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 21.0029: train_loss/word=3.247267 (steps=9270, words/sec=12074.73, time=0-00:19:51)
[switchout.asean.en-th] Epoch 21.0547: train_loss/word=3.431100 (steps=9291, words/sec=8767.01, time=0-00:19:52)
[switchout.asean.en-th] Epoch 21.1051: train_loss/word=3.335128 (steps=9314, words/sec=8824.32, time=0-00:19:53)
[switchout.asean.en-th] Epoch 21.1558: train_loss/word=3.246499 (steps=9338, words/sec=8017.35, time=0-00:19:54)
[switchout.asean.en-th] Epoch 21.2071: train_loss/word=3.165812 (steps=9361, words/sec=8301.83, time=0-00:19:55)
[switchout.asean.en-th] Epoch 21.2586: train_loss/word=3.446921 (steps=9383, words/sec=8984.83, time=0-00:19:56)
[switchout.asean.en-th] Epoch 21.3090: train_loss/word=3.253710 (steps=9407, words/sec=7883.41, time=0-00:19:57)
[switchout.asean.en-th] Epoch 21.3635: train_loss/word=3.254111 (steps=9429, words/sec=8419.94, time=0-00:19:58)
[switchout.asean.en-th] Epoch 21.4136: train_loss/word=3.388109 (steps=9450, words/sec=9037.72, time=0-00:19:59)
[switchout.asean.en-th] Epoch 21.4649: train_loss/word=3.342122 (steps=9474, words/sec=7865.49, time=0-00:20:00)
[switchout.asean.en-th] Epoch 21.5151: train_loss/word=3.396413 (steps=9495, words/sec=8194.35, time=0-00:20:00)
[switchout.asean.en-th] Epoch 21.5652: train_loss/word=3.376283 (steps=9517, words/sec=7705.80, time=0-00:20:01)
[switchout.asean.en-th] Epoch 21.6154: train_loss/word=3.421751 (steps=9541, words/sec=7574.23, time=0-00:20:02)
[switchout.asean.en-th] Epoch 21.6665: train_loss/word=3.348143 (steps=9563, words/sec=9268.77, time=0-00:20:03)
[switchout.asean.en-th] Epoch 21.7171: train_loss/word=3.448693 (steps=9586, words/sec=7819.58, time=0-00:20:04)
[switchout.asean.en-th] Epoch 21.7686: train_loss/word=3.582854 (steps=9606, words/sec=8748.74, time=0-00:20:05)
[switchout.asean.en-th] Epoch 21.8191: train_loss/word=3.386476 (steps=9628, words/sec=8638.83, time=0-00:20:06)
[switchout.asean.en-th] Epoch 21.8705: train_loss/word=3.481307 (steps=9650, words/sec=8699.22, time=0-00:20:07)
[switchout.asean.en-th] Epoch 21.9222: train_loss/word=3.310915 (steps=9674, words/sec=8172.53, time=0-00:20:08)
[switchout.asean.en-th] Epoch 21.9723: train_loss/word=3.237220 (steps=9699, words/sec=8626.08, time=0-00:20:09)
[switchout.asean.en-th] Epoch 22.0000: train_loss/word=3.272431 (steps=9711, words/sec=9294.59, time=0-00:20:09)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 22.0000 dev BLEU4: 0.31306250603937746, 0.547793/0.366011/0.253436/0.189036 (BP = 1.000000, ratio=1.08, hyp_len=7386, ref_len=6809) (time=0-00:20:36)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.325606
[switchout.asean.en-th]              dev auxiliary Loss: 4.003 (ref_len=6809)
             checkpoint took 0-00:00:26
  new learning rate: 0.5
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 22.0028: train_loss/word=3.297937 (steps=9712, words/sec=11707.23, time=0-00:20:40)
[switchout.asean.en-th] Epoch 22.0530: train_loss/word=3.295205 (steps=9733, words/sec=8987.65, time=0-00:20:41)
[switchout.asean.en-th] Epoch 22.1042: train_loss/word=3.337801 (steps=9754, words/sec=8603.89, time=0-00:20:42)
[switchout.asean.en-th] Epoch 22.1580: train_loss/word=3.292278 (steps=9776, words/sec=8964.77, time=0-00:20:43)
[switchout.asean.en-th] Epoch 22.2095: train_loss/word=3.338063 (steps=9799, words/sec=8453.07, time=0-00:20:44)
[switchout.asean.en-th] Epoch 22.2596: train_loss/word=3.489244 (steps=9817, words/sec=9357.36, time=0-00:20:44)
[switchout.asean.en-th] Epoch 22.3096: train_loss/word=3.121153 (steps=9840, words/sec=8004.14, time=0-00:20:45)
[switchout.asean.en-th] Epoch 22.3610: train_loss/word=3.159641 (steps=9865, words/sec=8054.69, time=0-00:20:46)
[switchout.asean.en-th] Epoch 22.4135: train_loss/word=3.286971 (steps=9888, words/sec=8685.25, time=0-00:20:47)
[switchout.asean.en-th] Epoch 22.4662: train_loss/word=3.156559 (steps=9912, words/sec=8873.83, time=0-00:20:48)
[switchout.asean.en-th] Epoch 22.5168: train_loss/word=3.286881 (steps=9934, words/sec=9164.52, time=0-00:20:49)
[switchout.asean.en-th] Epoch 22.5668: train_loss/word=3.329868 (steps=9955, words/sec=9475.70, time=0-00:20:50)
[switchout.asean.en-th] Epoch 22.6180: train_loss/word=3.401808 (steps=9976, words/sec=9341.23, time=0-00:20:51)
[switchout.asean.en-th] Epoch 22.6692: train_loss/word=3.003563 (steps=10003, words/sec=7019.16, time=0-00:20:52)
[switchout.asean.en-th] Epoch 22.7194: train_loss/word=3.161076 (steps=10025, words/sec=8208.95, time=0-00:20:53)
[switchout.asean.en-th] Epoch 22.7694: train_loss/word=3.205177 (steps=10047, words/sec=8092.61, time=0-00:20:54)
[switchout.asean.en-th] Epoch 22.8201: train_loss/word=3.013086 (steps=10074, words/sec=7421.99, time=0-00:20:55)
[switchout.asean.en-th] Epoch 22.8721: train_loss/word=3.210152 (steps=10098, words/sec=7861.55, time=0-00:20:56)
[switchout.asean.en-th] Epoch 22.9229: train_loss/word=3.388582 (steps=10118, words/sec=9422.95, time=0-00:20:57)
[switchout.asean.en-th] Epoch 22.9735: train_loss/word=3.196560 (steps=10141, words/sec=7728.27, time=0-00:20:58)
[switchout.asean.en-th] Epoch 23.0000: train_loss/word=3.188359 (steps=10153, words/sec=8158.38, time=0-00:20:59)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 23.0000 dev BLEU4: 0.3353353642349963, 0.567977/0.388493/0.274120/0.209056 (BP = 1.000000, ratio=1.06, hyp_len=7201, ref_len=6809) (time=0-00:21:25)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.340412
[switchout.asean.en-th]              dev auxiliary Loss: 3.958 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 23.0024: train_loss/word=3.142662 (steps=10154, words/sec=10085.33, time=0-00:21:34)
[switchout.asean.en-th] Epoch 23.0544: train_loss/word=3.203370 (steps=10176, words/sec=9041.90, time=0-00:21:35)
[switchout.asean.en-th] Epoch 23.1051: train_loss/word=3.188496 (steps=10199, words/sec=8053.17, time=0-00:21:36)
[switchout.asean.en-th] Epoch 23.1565: train_loss/word=3.231854 (steps=10222, words/sec=7973.21, time=0-00:21:37)
[switchout.asean.en-th] Epoch 23.2075: train_loss/word=2.980854 (steps=10248, words/sec=8221.08, time=0-00:21:38)
[switchout.asean.en-th] Epoch 23.2600: train_loss/word=3.149030 (steps=10273, words/sec=8083.01, time=0-00:21:39)
[switchout.asean.en-th] Epoch 23.3114: train_loss/word=3.324002 (steps=10294, words/sec=8578.33, time=0-00:21:40)
[switchout.asean.en-th] Epoch 23.3635: train_loss/word=3.145853 (steps=10317, words/sec=7770.60, time=0-00:21:41)
[switchout.asean.en-th] Epoch 23.4146: train_loss/word=2.991605 (steps=10343, words/sec=7821.17, time=0-00:21:42)
[switchout.asean.en-th] Epoch 23.4654: train_loss/word=3.357074 (steps=10363, words/sec=8004.91, time=0-00:21:43)
[switchout.asean.en-th] Epoch 23.5160: train_loss/word=3.222806 (steps=10385, words/sec=8605.52, time=0-00:21:44)
[switchout.asean.en-th] Epoch 23.5686: train_loss/word=3.098404 (steps=10412, words/sec=7758.75, time=0-00:21:45)
[switchout.asean.en-th] Epoch 23.6189: train_loss/word=3.204631 (steps=10434, words/sec=8701.25, time=0-00:21:46)
[switchout.asean.en-th] Epoch 23.6715: train_loss/word=3.118991 (steps=10457, words/sec=8321.23, time=0-00:21:47)
[switchout.asean.en-th] Epoch 23.7235: train_loss/word=3.230985 (steps=10479, words/sec=9100.02, time=0-00:21:48)
[switchout.asean.en-th] Epoch 23.7747: train_loss/word=3.208642 (steps=10500, words/sec=8920.10, time=0-00:21:49)
[switchout.asean.en-th] Epoch 23.8260: train_loss/word=3.461776 (steps=10520, words/sec=9119.75, time=0-00:21:49)
[switchout.asean.en-th] Epoch 23.8771: train_loss/word=3.253199 (steps=10542, words/sec=8217.00, time=0-00:21:50)
[switchout.asean.en-th] Epoch 23.9288: train_loss/word=3.307117 (steps=10564, words/sec=8550.84, time=0-00:21:51)
[switchout.asean.en-th] Epoch 23.9805: train_loss/word=3.223924 (steps=10585, words/sec=9292.07, time=0-00:21:52)
[switchout.asean.en-th] Epoch 24.0000: train_loss/word=3.119836 (steps=10595, words/sec=8328.73, time=0-00:21:53)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 24.0000 dev BLEU4: 0.3313190491624186, 0.564053/0.382410/0.271694/0.205616 (BP = 1.000000, ratio=1.06, hyp_len=7205, ref_len=6809) (time=0-00:22:19)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.335207
[switchout.asean.en-th]              dev auxiliary Loss: 3.960 (ref_len=6809)
             checkpoint took 0-00:00:26
  new learning rate: 0.25
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 24.0014: train_loss/word=2.392110 (steps=10596, words/sec=6938.26, time=0-00:22:23)
[switchout.asean.en-th] Epoch 24.0535: train_loss/word=3.171286 (steps=10618, words/sec=8905.62, time=0-00:22:23)
[switchout.asean.en-th] Epoch 24.1036: train_loss/word=3.223321 (steps=10640, words/sec=8641.07, time=0-00:22:24)
[switchout.asean.en-th] Epoch 24.1557: train_loss/word=3.181940 (steps=10663, words/sec=8283.47, time=0-00:22:25)
[switchout.asean.en-th] Epoch 24.2079: train_loss/word=3.247748 (steps=10684, words/sec=8464.36, time=0-00:22:26)
[switchout.asean.en-th] Epoch 24.2591: train_loss/word=3.101395 (steps=10707, words/sec=8292.29, time=0-00:22:27)
[switchout.asean.en-th] Epoch 24.3109: train_loss/word=3.103831 (steps=10729, words/sec=9257.17, time=0-00:22:28)
[switchout.asean.en-th] Epoch 24.3614: train_loss/word=3.303387 (steps=10749, words/sec=9089.22, time=0-00:22:29)
[switchout.asean.en-th] Epoch 24.4142: train_loss/word=3.209099 (steps=10771, words/sec=9277.22, time=0-00:22:30)
[switchout.asean.en-th] Epoch 24.4645: train_loss/word=2.931957 (steps=10797, words/sec=7246.17, time=0-00:22:31)
[switchout.asean.en-th] Epoch 24.5148: train_loss/word=3.164455 (steps=10821, words/sec=8457.07, time=0-00:22:32)
[switchout.asean.en-th] Epoch 24.5661: train_loss/word=3.281858 (steps=10842, words/sec=9592.25, time=0-00:22:33)
[switchout.asean.en-th] Epoch 24.6161: train_loss/word=3.016082 (steps=10866, words/sec=7521.48, time=0-00:22:34)
[switchout.asean.en-th] Epoch 24.6675: train_loss/word=2.947465 (steps=10893, words/sec=7512.98, time=0-00:22:35)
[switchout.asean.en-th] Epoch 24.7177: train_loss/word=3.028311 (steps=10918, words/sec=7055.92, time=0-00:22:36)
[switchout.asean.en-th] Epoch 24.7694: train_loss/word=3.159595 (steps=10940, words/sec=8862.88, time=0-00:22:37)
[switchout.asean.en-th] Epoch 24.8197: train_loss/word=3.149051 (steps=10961, words/sec=9436.72, time=0-00:22:38)
[switchout.asean.en-th] Epoch 24.8710: train_loss/word=3.214448 (steps=10983, words/sec=8084.97, time=0-00:22:39)
[switchout.asean.en-th] Epoch 24.9232: train_loss/word=3.226592 (steps=11004, words/sec=9101.99, time=0-00:22:40)
[switchout.asean.en-th] Epoch 24.9757: train_loss/word=3.211339 (steps=11026, words/sec=8473.00, time=0-00:22:41)
[switchout.asean.en-th] Epoch 25.0000: train_loss/word=3.083470 (steps=11037, words/sec=8095.01, time=0-00:22:41)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 25.0000 dev BLEU4: 0.3363337756483673, 0.567406/0.388089/0.277211/0.209627 (BP = 1.000000, ratio=1.06, hyp_len=7210, ref_len=6809) (time=0-00:23:08)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.339794
[switchout.asean.en-th]              dev auxiliary Loss: 3.944 (ref_len=6809)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.th
Done reading ./data/train.en and ./data/train.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 25.0024: train_loss/word=3.564449 (steps=11038, words/sec=9976.83, time=0-00:23:17)
[switchout.asean.en-th] Epoch 25.0531: train_loss/word=3.041628 (steps=11062, words/sec=7386.45, time=0-00:23:18)
[switchout.asean.en-th] Epoch 25.1045: train_loss/word=3.095655 (steps=11085, words/sec=8284.48, time=0-00:23:19)
[switchout.asean.en-th] Epoch 25.1549: train_loss/word=2.997284 (steps=11110, words/sec=7640.81, time=0-00:23:20)
[switchout.asean.en-th] Epoch 25.2057: train_loss/word=3.177309 (steps=11133, words/sec=8535.34, time=0-00:23:21)
[switchout.asean.en-th] Epoch 25.2560: train_loss/word=3.081419 (steps=11157, words/sec=7811.49, time=0-00:23:22)
[switchout.asean.en-th] Epoch 25.3074: train_loss/word=3.122722 (steps=11180, words/sec=8632.22, time=0-00:23:23)
[switchout.asean.en-th] Epoch 25.3576: train_loss/word=3.060722 (steps=11201, words/sec=7666.01, time=0-00:23:24)
[switchout.asean.en-th] Epoch 25.4098: train_loss/word=3.075785 (steps=11224, words/sec=9386.58, time=0-00:23:25)
[switchout.asean.en-th] Epoch 25.4605: train_loss/word=3.069463 (steps=11246, words/sec=8169.75, time=0-00:23:26)
[switchout.asean.en-th] Epoch 25.5113: train_loss/word=3.146869 (steps=11268, words/sec=8872.31, time=0-00:23:27)
[switchout.asean.en-th] Epoch 25.5614: train_loss/word=3.152807 (steps=11287, words/sec=9432.18, time=0-00:23:27)
[switchout.asean.en-th] Epoch 25.6127: train_loss/word=3.059771 (steps=11310, words/sec=8548.74, time=0-00:23:28)
[switchout.asean.en-th] Epoch 25.6646: train_loss/word=3.149670 (steps=11334, words/sec=8907.43, time=0-00:23:29)
[switchout.asean.en-th] Epoch 25.7156: train_loss/word=3.314657 (steps=11355, words/sec=9020.00, time=0-00:23:30)
[switchout.asean.en-th] Epoch 25.7656: train_loss/word=3.011991 (steps=11377, words/sec=8327.26, time=0-00:23:31)
[switchout.asean.en-th] Epoch 25.8160: train_loss/word=3.245606 (steps=11399, words/sec=8193.50, time=0-00:23:32)
[switchout.asean.en-th] Epoch 25.8675: train_loss/word=3.217340 (steps=11421, words/sec=9054.47, time=0-00:23:33)
[switchout.asean.en-th] Epoch 25.9186: train_loss/word=3.284618 (steps=11442, words/sec=8931.88, time=0-00:23:34)
[switchout.asean.en-th] Epoch 25.9688: train_loss/word=3.063743 (steps=11464, words/sec=8735.84, time=0-00:23:34)
[switchout.asean.en-th] Epoch 26.0000: train_loss/word=3.108436 (steps=11479, words/sec=7375.84, time=0-00:23:35)
> Checkpoint [switchout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.asean.en-th] Epoch 26.0000 dev BLEU4: 0.3325612037884462, 0.561125/0.383668/0.273581/0.207675 (BP = 1.000000, ratio=1.08, hyp_len=7362, ref_len=6809) (time=0-00:24:02)
[switchout.asean.en-th]              dev auxiliary GLEU: 0.340194
[switchout.asean.en-th]              dev auxiliary Loss: 3.933 (ref_len=6809)
             checkpoint took 0-00:00:27
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.th
Performing inference on ./data/test.en and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.asean.en-th         | BLEU4: 0.3363337756483673, 0.567406/0.388089/0.277211/0.209627 (BP = 1.000000, ratio=1.06, hyp_len=7210, ref_len=6809)
                              | GLEU: 0.339794
                              | WER: 62.74% ( C/S/I/D: 3925/1897/1388/987; hyp_len=7210, ref_len=6809 )
                              | CER: 49.11% ( C/S/I/D: 18878/7130/3196/4806; hyp_len=29204, ref_len=30814 )
                              | BLEU4: 0.35408899038973984, 0.594272/0.405529/0.292139/0.223282 (BP = 1.000000, ratio=1.03, hyp_len=7367, ref_len=7169)
                              | GLEU: 0.355862
                              | WER: 58.79% ( C/S/I/D: 4195/1931/1241/1043; hyp_len=7367, ref_len=7169 )
                              | CER: 48.17% ( C/S/I/D: 19169/7029/3080/4843; hyp_len=29278, ref_len=31041 )
```

## Training for th-en, word unit (SwitchOut)

ထိုင်း ကနေ အင်္ဂလိပ်ကို ဘာသာပြန်တဲ့ training/evaluation running log က အောက်ပါအတိုင်း...  

```
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 22:34:24
=> Running switchout.asean.th-en
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 20659973
> Training
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 0.0511: train_loss/word=10.115308 (steps=21, words/sec=6019.20, time=0-00:00:07)
[switchout.asean.th-en] Epoch 0.1021: train_loss/word=8.405801 (steps=45, words/sec=7783.59, time=0-00:00:08)
[switchout.asean.th-en] Epoch 0.1524: train_loss/word=8.089617 (steps=67, words/sec=9510.09, time=0-00:00:09)
[switchout.asean.th-en] Epoch 0.2027: train_loss/word=8.051759 (steps=91, words/sec=8121.04, time=0-00:00:10)
[switchout.asean.th-en] Epoch 0.2551: train_loss/word=7.852984 (steps=116, words/sec=7859.63, time=0-00:00:11)
[switchout.asean.th-en] Epoch 0.3065: train_loss/word=7.741527 (steps=140, words/sec=8525.46, time=0-00:00:12)
[switchout.asean.th-en] Epoch 0.3565: train_loss/word=7.722842 (steps=163, words/sec=7440.32, time=0-00:00:13)
[switchout.asean.th-en] Epoch 0.4074: train_loss/word=7.628305 (steps=188, words/sec=7908.90, time=0-00:00:14)
[switchout.asean.th-en] Epoch 0.4576: train_loss/word=7.674594 (steps=211, words/sec=7764.15, time=0-00:00:15)
[switchout.asean.th-en] Epoch 0.5095: train_loss/word=7.610376 (steps=234, words/sec=8409.46, time=0-00:00:16)
[switchout.asean.th-en] Epoch 0.5605: train_loss/word=7.488082 (steps=259, words/sec=7787.23, time=0-00:00:17)
[switchout.asean.th-en] Epoch 0.6112: train_loss/word=7.463017 (steps=283, words/sec=7769.61, time=0-00:00:18)
[switchout.asean.th-en] Epoch 0.6620: train_loss/word=7.354697 (steps=305, words/sec=8480.90, time=0-00:00:19)
[switchout.asean.th-en] Epoch 0.7136: train_loss/word=7.265898 (steps=328, words/sec=8191.15, time=0-00:00:20)
[switchout.asean.th-en] Epoch 0.7662: train_loss/word=7.322476 (steps=352, words/sec=7450.13, time=0-00:00:21)
[switchout.asean.th-en] Epoch 0.8169: train_loss/word=7.190456 (steps=374, words/sec=8500.66, time=0-00:00:22)
[switchout.asean.th-en] Epoch 0.8689: train_loss/word=7.249841 (steps=397, words/sec=8663.81, time=0-00:00:23)
[switchout.asean.th-en] Epoch 0.9191: train_loss/word=7.172729 (steps=422, words/sec=7284.86, time=0-00:00:24)
[switchout.asean.th-en] Epoch 0.9714: train_loss/word=7.142083 (steps=445, words/sec=8727.08, time=0-00:00:25)
[switchout.asean.th-en] Epoch 1.0000: train_loss/word=7.185655 (steps=458, words/sec=7278.41, time=0-00:00:26)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 1.0000 dev BLEU4: 0.0037621778010898934, 0.035046/0.007739/0.001817/0.000406 (BP = 1.000000, ratio=4.16, hyp_len=30103, ref_len=7245) (time=0-00:02:19)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.011590
[switchout.asean.th-en]              dev auxiliary Loss: 6.475 (ref_len=7245)
             checkpoint took 0-00:01:52
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 1.0015: train_loss/word=7.165461 (steps=459, words/sec=7773.64, time=0-00:02:41)
[switchout.asean.th-en] Epoch 1.0537: train_loss/word=6.986443 (steps=481, words/sec=8907.89, time=0-00:02:42)
[switchout.asean.th-en] Epoch 1.1052: train_loss/word=7.037034 (steps=507, words/sec=7476.85, time=0-00:02:43)
[switchout.asean.th-en] Epoch 1.1571: train_loss/word=6.868882 (steps=532, words/sec=7385.16, time=0-00:02:44)
[switchout.asean.th-en] Epoch 1.2090: train_loss/word=6.864823 (steps=557, words/sec=7660.36, time=0-00:02:45)
[switchout.asean.th-en] Epoch 1.2598: train_loss/word=6.951240 (steps=579, words/sec=8337.88, time=0-00:02:46)
[switchout.asean.th-en] Epoch 1.3118: train_loss/word=6.778139 (steps=603, words/sec=8157.57, time=0-00:02:47)
[switchout.asean.th-en] Epoch 1.3632: train_loss/word=6.854302 (steps=624, words/sec=8761.17, time=0-00:02:48)
[switchout.asean.th-en] Epoch 1.4143: train_loss/word=6.697906 (steps=647, words/sec=9230.58, time=0-00:02:49)
[switchout.asean.th-en] Epoch 1.4659: train_loss/word=6.763180 (steps=670, words/sec=8447.29, time=0-00:02:50)
[switchout.asean.th-en] Epoch 1.5172: train_loss/word=6.734772 (steps=694, words/sec=8025.56, time=0-00:02:51)
[switchout.asean.th-en] Epoch 1.5690: train_loss/word=6.701027 (steps=718, words/sec=8048.28, time=0-00:02:52)
[switchout.asean.th-en] Epoch 1.6204: train_loss/word=6.750749 (steps=743, words/sec=7139.88, time=0-00:02:53)
[switchout.asean.th-en] Epoch 1.6719: train_loss/word=6.765223 (steps=768, words/sec=7434.23, time=0-00:02:54)
[switchout.asean.th-en] Epoch 1.7231: train_loss/word=6.655846 (steps=793, words/sec=6814.31, time=0-00:02:56)
[switchout.asean.th-en] Epoch 1.7753: train_loss/word=6.489854 (steps=817, words/sec=8631.73, time=0-00:02:57)
[switchout.asean.th-en] Epoch 1.8271: train_loss/word=6.655369 (steps=840, words/sec=8377.38, time=0-00:02:57)
[switchout.asean.th-en] Epoch 1.8790: train_loss/word=6.672760 (steps=865, words/sec=7291.85, time=0-00:02:59)
[switchout.asean.th-en] Epoch 1.9298: train_loss/word=6.468380 (steps=887, words/sec=8186.05, time=0-00:03:00)
[switchout.asean.th-en] Epoch 1.9806: train_loss/word=6.554776 (steps=910, words/sec=8478.80, time=0-00:03:00)
[switchout.asean.th-en] Epoch 2.0000: train_loss/word=6.522682 (steps=919, words/sec=8352.04, time=0-00:03:01)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 2.0000 dev BLEU4: 0.019298229098425147, 0.124166/0.034049/0.011551/0.002840 (BP = 1.000000, ratio=1.63, hyp_len=11839, ref_len=7245) (time=0-00:04:04)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.044383
[switchout.asean.th-en]              dev auxiliary Loss: 5.913 (ref_len=7245)
             checkpoint took 0-00:01:03
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 2.0021: train_loss/word=6.279165 (steps=920, words/sec=7617.51, time=0-00:04:13)
[switchout.asean.th-en] Epoch 2.0543: train_loss/word=6.407449 (steps=945, words/sec=7277.21, time=0-00:04:15)
[switchout.asean.th-en] Epoch 2.1044: train_loss/word=6.323567 (steps=968, words/sec=8416.26, time=0-00:04:16)
[switchout.asean.th-en] Epoch 2.1555: train_loss/word=6.296857 (steps=994, words/sec=7229.94, time=0-00:04:17)
[switchout.asean.th-en] Epoch 2.2069: train_loss/word=6.356079 (steps=1018, words/sec=8218.21, time=0-00:04:18)
[switchout.asean.th-en] Epoch 2.2582: train_loss/word=6.369774 (steps=1041, words/sec=8151.85, time=0-00:04:19)
[switchout.asean.th-en] Epoch 2.3097: train_loss/word=6.284161 (steps=1063, words/sec=8956.41, time=0-00:04:20)
[switchout.asean.th-en] Epoch 2.3623: train_loss/word=6.416396 (steps=1086, words/sec=8875.52, time=0-00:04:21)
[switchout.asean.th-en] Epoch 2.4125: train_loss/word=6.337213 (steps=1107, words/sec=8405.49, time=0-00:04:21)
[switchout.asean.th-en] Epoch 2.4628: train_loss/word=6.327658 (steps=1131, words/sec=7935.90, time=0-00:04:23)
[switchout.asean.th-en] Epoch 2.5130: train_loss/word=6.248047 (steps=1154, words/sec=8594.63, time=0-00:04:24)
[switchout.asean.th-en] Epoch 2.5645: train_loss/word=6.353562 (steps=1178, words/sec=7583.43, time=0-00:04:25)
[switchout.asean.th-en] Epoch 2.6160: train_loss/word=6.241189 (steps=1203, words/sec=7077.42, time=0-00:04:26)
[switchout.asean.th-en] Epoch 2.6673: train_loss/word=6.267486 (steps=1227, words/sec=7815.95, time=0-00:04:27)
[switchout.asean.th-en] Epoch 2.7188: train_loss/word=6.122300 (steps=1251, words/sec=8054.99, time=0-00:04:28)
[switchout.asean.th-en] Epoch 2.7698: train_loss/word=6.178370 (steps=1274, words/sec=8038.90, time=0-00:04:29)
[switchout.asean.th-en] Epoch 2.8224: train_loss/word=6.193999 (steps=1298, words/sec=7795.38, time=0-00:04:30)
[switchout.asean.th-en] Epoch 2.8736: train_loss/word=6.131831 (steps=1321, words/sec=8403.06, time=0-00:04:31)
[switchout.asean.th-en] Epoch 2.9240: train_loss/word=6.134318 (steps=1342, words/sec=9020.32, time=0-00:04:32)
[switchout.asean.th-en] Epoch 2.9754: train_loss/word=6.226882 (steps=1365, words/sec=8176.16, time=0-00:04:33)
[switchout.asean.th-en] Epoch 3.0000: train_loss/word=6.051498 (steps=1376, words/sec=8983.96, time=0-00:04:33)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 3.0000 dev BLEU4: 0.04730286396067081, 0.229891/0.077321/0.031147/0.009043 (BP = 1.000000, ratio=1.08, hyp_len=7795, ref_len=7245) (time=0-00:05:07)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.091203
[switchout.asean.th-en]              dev auxiliary Loss: 5.540 (ref_len=7245)
             checkpoint took 0-00:00:33
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 3.0032: train_loss/word=5.689810 (steps=1377, words/sec=12368.21, time=0-00:05:16)
[switchout.asean.th-en] Epoch 3.0550: train_loss/word=5.993431 (steps=1401, words/sec=7890.37, time=0-00:05:17)
[switchout.asean.th-en] Epoch 3.1059: train_loss/word=5.996126 (steps=1422, words/sec=9664.44, time=0-00:05:18)
[switchout.asean.th-en] Epoch 3.1570: train_loss/word=5.820241 (steps=1446, words/sec=8538.98, time=0-00:05:19)
[switchout.asean.th-en] Epoch 3.2085: train_loss/word=5.926902 (steps=1469, words/sec=8317.56, time=0-00:05:20)
[switchout.asean.th-en] Epoch 3.2586: train_loss/word=5.934614 (steps=1491, words/sec=7914.86, time=0-00:05:21)
[switchout.asean.th-en] Epoch 3.3098: train_loss/word=5.996849 (steps=1512, words/sec=8361.68, time=0-00:05:22)
[switchout.asean.th-en] Epoch 3.3622: train_loss/word=5.829388 (steps=1536, words/sec=8760.88, time=0-00:05:23)
[switchout.asean.th-en] Epoch 3.4137: train_loss/word=5.764405 (steps=1560, words/sec=8426.63, time=0-00:05:24)
[switchout.asean.th-en] Epoch 3.4643: train_loss/word=5.846124 (steps=1581, words/sec=9085.40, time=0-00:05:24)
[switchout.asean.th-en] Epoch 3.5145: train_loss/word=5.927958 (steps=1606, words/sec=7536.47, time=0-00:05:26)
[switchout.asean.th-en] Epoch 3.5654: train_loss/word=5.702798 (steps=1629, words/sec=8356.82, time=0-00:05:27)
[switchout.asean.th-en] Epoch 3.6165: train_loss/word=5.846953 (steps=1654, words/sec=7191.44, time=0-00:05:28)
[switchout.asean.th-en] Epoch 3.6668: train_loss/word=5.764158 (steps=1679, words/sec=7826.99, time=0-00:05:29)
[switchout.asean.th-en] Epoch 3.7174: train_loss/word=6.038509 (steps=1703, words/sec=6826.78, time=0-00:05:30)
[switchout.asean.th-en] Epoch 3.7674: train_loss/word=5.865097 (steps=1727, words/sec=6844.84, time=0-00:05:31)
[switchout.asean.th-en] Epoch 3.8187: train_loss/word=5.865217 (steps=1749, words/sec=8608.37, time=0-00:05:32)
[switchout.asean.th-en] Epoch 3.8705: train_loss/word=5.904696 (steps=1773, words/sec=8634.56, time=0-00:05:33)
[switchout.asean.th-en] Epoch 3.9213: train_loss/word=5.805360 (steps=1794, words/sec=9194.84, time=0-00:05:34)
[switchout.asean.th-en] Epoch 3.9719: train_loss/word=5.754010 (steps=1817, words/sec=7788.91, time=0-00:05:35)
[switchout.asean.th-en] Epoch 4.0000: train_loss/word=5.810223 (steps=1832, words/sec=7003.11, time=0-00:05:36)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 4.0000 dev BLEU4: 0.061046937626053455, 0.244431/0.090746/0.038821/0.016129 (BP = 1.000000, ratio=1.14, hyp_len=8260, ref_len=7245) (time=0-00:06:10)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.101031
[switchout.asean.th-en]              dev auxiliary Loss: 5.286 (ref_len=7245)
             checkpoint took 0-00:00:34
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 4.0030: train_loss/word=5.012755 (steps=1833, words/sec=11943.76, time=0-00:06:19)
[switchout.asean.th-en] Epoch 4.0531: train_loss/word=5.605140 (steps=1854, words/sec=8992.74, time=0-00:06:20)
[switchout.asean.th-en] Epoch 4.1036: train_loss/word=5.616562 (steps=1880, words/sec=6701.60, time=0-00:06:21)
[switchout.asean.th-en] Epoch 4.1544: train_loss/word=5.588612 (steps=1904, words/sec=8059.75, time=0-00:06:22)
[switchout.asean.th-en] Epoch 4.2050: train_loss/word=5.614301 (steps=1927, words/sec=8246.60, time=0-00:06:23)
[switchout.asean.th-en] Epoch 4.2553: train_loss/word=5.481868 (steps=1949, words/sec=8922.06, time=0-00:06:24)
[switchout.asean.th-en] Epoch 4.3069: train_loss/word=5.687160 (steps=1970, words/sec=9330.94, time=0-00:06:25)
[switchout.asean.th-en] Epoch 4.3584: train_loss/word=5.592139 (steps=1992, words/sec=8793.97, time=0-00:06:26)
[switchout.asean.th-en] Epoch 4.4090: train_loss/word=5.512688 (steps=2015, words/sec=8230.97, time=0-00:06:27)
[switchout.asean.th-en] Epoch 4.4605: train_loss/word=5.568657 (steps=2039, words/sec=8528.35, time=0-00:06:28)
[switchout.asean.th-en] Epoch 4.5108: train_loss/word=5.519929 (steps=2064, words/sec=8196.95, time=0-00:06:29)
[switchout.asean.th-en] Epoch 4.5612: train_loss/word=5.638825 (steps=2087, words/sec=8025.72, time=0-00:06:30)
[switchout.asean.th-en] Epoch 4.6124: train_loss/word=5.747893 (steps=2114, words/sec=6947.46, time=0-00:06:31)
[switchout.asean.th-en] Epoch 4.6627: train_loss/word=5.518688 (steps=2138, words/sec=8107.01, time=0-00:06:32)
[switchout.asean.th-en] Epoch 4.7143: train_loss/word=5.578848 (steps=2162, words/sec=7542.50, time=0-00:06:33)
[switchout.asean.th-en] Epoch 4.7668: train_loss/word=5.595134 (steps=2185, words/sec=8470.76, time=0-00:06:34)
[switchout.asean.th-en] Epoch 4.8187: train_loss/word=5.535088 (steps=2209, words/sec=7600.49, time=0-00:06:35)
[switchout.asean.th-en] Epoch 4.8704: train_loss/word=5.522163 (steps=2231, words/sec=8378.13, time=0-00:06:36)
[switchout.asean.th-en] Epoch 4.9230: train_loss/word=5.520420 (steps=2253, words/sec=8675.73, time=0-00:06:37)
[switchout.asean.th-en] Epoch 4.9732: train_loss/word=5.382865 (steps=2275, words/sec=8923.44, time=0-00:06:38)
[switchout.asean.th-en] Epoch 5.0000: train_loss/word=5.454154 (steps=2289, words/sec=6526.09, time=0-00:06:39)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 5.0000 dev BLEU4: 0.09596365630104406, 0.311191/0.134859/0.065565/0.030821 (BP = 1.000000, ratio=1.03, hyp_len=7497, ref_len=7245) (time=0-00:07:11)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.136762
[switchout.asean.th-en]              dev auxiliary Loss: 5.131 (ref_len=7245)
             checkpoint took 0-00:00:32
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 5.0018: train_loss/word=5.506657 (steps=2290, words/sec=7530.41, time=0-00:07:20)
[switchout.asean.th-en] Epoch 5.0536: train_loss/word=5.196488 (steps=2312, words/sec=9120.57, time=0-00:07:21)
[switchout.asean.th-en] Epoch 5.1037: train_loss/word=5.325006 (steps=2335, words/sec=8534.78, time=0-00:07:22)
[switchout.asean.th-en] Epoch 5.1541: train_loss/word=5.309412 (steps=2357, words/sec=8949.62, time=0-00:07:23)
[switchout.asean.th-en] Epoch 5.2051: train_loss/word=5.296869 (steps=2382, words/sec=8214.36, time=0-00:07:24)
[switchout.asean.th-en] Epoch 5.2553: train_loss/word=5.238122 (steps=2405, words/sec=8438.02, time=0-00:07:25)
[switchout.asean.th-en] Epoch 5.3057: train_loss/word=5.385854 (steps=2428, words/sec=8255.03, time=0-00:07:26)
[switchout.asean.th-en] Epoch 5.3563: train_loss/word=5.318616 (steps=2451, words/sec=7796.84, time=0-00:07:27)
[switchout.asean.th-en] Epoch 5.4067: train_loss/word=5.367652 (steps=2475, words/sec=7706.42, time=0-00:07:28)
[switchout.asean.th-en] Epoch 5.4574: train_loss/word=5.366956 (steps=2499, words/sec=6929.56, time=0-00:07:29)
[switchout.asean.th-en] Epoch 5.5081: train_loss/word=5.447630 (steps=2522, words/sec=8019.72, time=0-00:07:30)
[switchout.asean.th-en] Epoch 5.5585: train_loss/word=5.233369 (steps=2546, words/sec=8438.80, time=0-00:07:31)
[switchout.asean.th-en] Epoch 5.6103: train_loss/word=5.230925 (steps=2569, words/sec=8689.22, time=0-00:07:32)
[switchout.asean.th-en] Epoch 5.6620: train_loss/word=5.366310 (steps=2594, words/sec=7030.27, time=0-00:07:33)
[switchout.asean.th-en] Epoch 5.7140: train_loss/word=5.284298 (steps=2616, words/sec=8203.45, time=0-00:07:34)
[switchout.asean.th-en] Epoch 5.7649: train_loss/word=5.215116 (steps=2637, words/sec=9544.73, time=0-00:07:35)
[switchout.asean.th-en] Epoch 5.8152: train_loss/word=5.466486 (steps=2658, words/sec=8873.87, time=0-00:07:36)
[switchout.asean.th-en] Epoch 5.8673: train_loss/word=5.334498 (steps=2684, words/sec=8073.12, time=0-00:07:37)
[switchout.asean.th-en] Epoch 5.9194: train_loss/word=5.164250 (steps=2709, words/sec=8211.35, time=0-00:07:38)
[switchout.asean.th-en] Epoch 5.9704: train_loss/word=5.384983 (steps=2731, words/sec=7835.21, time=0-00:07:39)
[switchout.asean.th-en] Epoch 6.0000: train_loss/word=5.334427 (steps=2745, words/sec=7684.87, time=0-00:07:40)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 6.0000 dev BLEU4: 0.09080558249088073, 0.282457/0.127891/0.063189/0.029787 (BP = 1.000000, ratio=1.22, hyp_len=8858, ref_len=7245) (time=0-00:08:18)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.128353
[switchout.asean.th-en]              dev auxiliary Loss: 5.001 (ref_len=7245)
             checkpoint took 0-00:00:38
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 6.0012: train_loss/word=4.888953 (steps=2746, words/sec=5903.29, time=0-00:08:22)
[switchout.asean.th-en] Epoch 6.0519: train_loss/word=5.096996 (steps=2770, words/sec=7210.19, time=0-00:08:23)
[switchout.asean.th-en] Epoch 6.1027: train_loss/word=5.201170 (steps=2793, words/sec=8061.69, time=0-00:08:24)
[switchout.asean.th-en] Epoch 6.1534: train_loss/word=5.104614 (steps=2817, words/sec=8085.31, time=0-00:08:25)
[switchout.asean.th-en] Epoch 6.2052: train_loss/word=5.135020 (steps=2840, words/sec=8722.23, time=0-00:08:26)
[switchout.asean.th-en] Epoch 6.2573: train_loss/word=5.052539 (steps=2864, words/sec=8477.95, time=0-00:08:27)
[switchout.asean.th-en] Epoch 6.3079: train_loss/word=4.989530 (steps=2888, words/sec=7635.78, time=0-00:08:28)
[switchout.asean.th-en] Epoch 6.3582: train_loss/word=5.150048 (steps=2913, words/sec=7167.65, time=0-00:08:29)
[switchout.asean.th-en] Epoch 6.4108: train_loss/word=5.214154 (steps=2935, words/sec=8322.11, time=0-00:08:30)
[switchout.asean.th-en] Epoch 6.4614: train_loss/word=5.135722 (steps=2957, words/sec=8243.15, time=0-00:08:31)
[switchout.asean.th-en] Epoch 6.5131: train_loss/word=5.089578 (steps=2981, words/sec=8156.99, time=0-00:08:32)
[switchout.asean.th-en] Epoch 6.5648: train_loss/word=5.103195 (steps=3006, words/sec=7349.40, time=0-00:08:33)
[switchout.asean.th-en] Epoch 6.6155: train_loss/word=5.157025 (steps=3029, words/sec=8038.84, time=0-00:08:34)
[switchout.asean.th-en] Epoch 6.6664: train_loss/word=5.070825 (steps=3052, words/sec=8451.19, time=0-00:08:35)
[switchout.asean.th-en] Epoch 6.7188: train_loss/word=5.029720 (steps=3074, words/sec=9197.12, time=0-00:08:36)
[switchout.asean.th-en] Epoch 6.7695: train_loss/word=5.088794 (steps=3096, words/sec=8208.36, time=0-00:08:37)
[switchout.asean.th-en] Epoch 6.8217: train_loss/word=5.026386 (steps=3121, words/sec=8135.20, time=0-00:08:38)
[switchout.asean.th-en] Epoch 6.8726: train_loss/word=4.989823 (steps=3143, words/sec=8741.03, time=0-00:08:39)
[switchout.asean.th-en] Epoch 6.9232: train_loss/word=5.092299 (steps=3164, words/sec=9045.30, time=0-00:08:40)
[switchout.asean.th-en] Epoch 6.9747: train_loss/word=5.110222 (steps=3189, words/sec=8072.42, time=0-00:08:41)
[switchout.asean.th-en] Epoch 7.0000: train_loss/word=5.143339 (steps=3202, words/sec=7753.32, time=0-00:08:42)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 7.0000 dev BLEU4: 0.12787367912040473, 0.346322/0.170249/0.093243/0.048634 (BP = 1.000000, ratio=1.04, hyp_len=7545, ref_len=7245) (time=0-00:09:13)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.163719
[switchout.asean.th-en]              dev auxiliary Loss: 4.928 (ref_len=7245)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 7.0021: train_loss/word=4.555476 (steps=3203, words/sec=8386.69, time=0-00:09:23)
[switchout.asean.th-en] Epoch 7.0536: train_loss/word=4.952723 (steps=3228, words/sec=7133.22, time=0-00:09:24)
[switchout.asean.th-en] Epoch 7.1039: train_loss/word=4.916030 (steps=3251, words/sec=7906.55, time=0-00:09:25)
[switchout.asean.th-en] Epoch 7.1541: train_loss/word=4.936841 (steps=3275, words/sec=7506.10, time=0-00:09:26)
[switchout.asean.th-en] Epoch 7.2042: train_loss/word=4.814462 (steps=3298, words/sec=8100.87, time=0-00:09:27)
[switchout.asean.th-en] Epoch 7.2550: train_loss/word=4.756728 (steps=3322, words/sec=7600.61, time=0-00:09:28)
[switchout.asean.th-en] Epoch 7.3067: train_loss/word=4.885287 (steps=3343, words/sec=9325.48, time=0-00:09:29)
[switchout.asean.th-en] Epoch 7.3571: train_loss/word=4.834145 (steps=3366, words/sec=8070.97, time=0-00:09:30)
[switchout.asean.th-en] Epoch 7.4087: train_loss/word=4.801658 (steps=3388, words/sec=9138.42, time=0-00:09:31)
[switchout.asean.th-en] Epoch 7.4589: train_loss/word=4.822263 (steps=3411, words/sec=8455.62, time=0-00:09:32)
[switchout.asean.th-en] Epoch 7.5102: train_loss/word=4.855410 (steps=3437, words/sec=7370.44, time=0-00:09:33)
[switchout.asean.th-en] Epoch 7.5606: train_loss/word=4.784439 (steps=3461, words/sec=8006.99, time=0-00:09:34)
[switchout.asean.th-en] Epoch 7.6132: train_loss/word=4.988061 (steps=3485, words/sec=7754.46, time=0-00:09:35)
[switchout.asean.th-en] Epoch 7.6637: train_loss/word=4.947472 (steps=3509, words/sec=7741.08, time=0-00:09:36)
[switchout.asean.th-en] Epoch 7.7149: train_loss/word=4.975971 (steps=3531, words/sec=8681.21, time=0-00:09:37)
[switchout.asean.th-en] Epoch 7.7663: train_loss/word=4.947810 (steps=3554, words/sec=7284.04, time=0-00:09:38)
[switchout.asean.th-en] Epoch 7.8178: train_loss/word=4.966513 (steps=3575, words/sec=8789.96, time=0-00:09:39)
[switchout.asean.th-en] Epoch 7.8692: train_loss/word=4.864018 (steps=3599, words/sec=7979.86, time=0-00:09:40)
[switchout.asean.th-en] Epoch 7.9201: train_loss/word=4.933900 (steps=3624, words/sec=7103.66, time=0-00:09:41)
[switchout.asean.th-en] Epoch 7.9713: train_loss/word=4.977087 (steps=3646, words/sec=8880.92, time=0-00:09:42)
[switchout.asean.th-en] Epoch 8.0000: train_loss/word=4.866890 (steps=3659, words/sec=7250.06, time=0-00:09:42)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 8.0000 dev BLEU4: 0.14251558293299904, 0.358593/0.183826/0.104383/0.059953 (BP = 1.000000, ratio=1.07, hyp_len=7733, ref_len=7245) (time=0-00:10:14)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.176827
[switchout.asean.th-en]              dev auxiliary Loss: 4.845 (ref_len=7245)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 8.0034: train_loss/word=4.469571 (steps=3660, words/sec=13312.54, time=0-00:10:23)
[switchout.asean.th-en] Epoch 8.0545: train_loss/word=4.639974 (steps=3685, words/sec=7674.73, time=0-00:10:25)
[switchout.asean.th-en] Epoch 8.1049: train_loss/word=4.614738 (steps=3710, words/sec=7932.35, time=0-00:10:26)
[switchout.asean.th-en] Epoch 8.1559: train_loss/word=4.642831 (steps=3733, words/sec=8540.60, time=0-00:10:27)
[switchout.asean.th-en] Epoch 8.2069: train_loss/word=4.718282 (steps=3758, words/sec=7550.72, time=0-00:10:28)
[switchout.asean.th-en] Epoch 8.2584: train_loss/word=4.777405 (steps=3783, words/sec=7115.59, time=0-00:10:29)
[switchout.asean.th-en] Epoch 8.3085: train_loss/word=4.723442 (steps=3806, words/sec=8015.36, time=0-00:10:30)
[switchout.asean.th-en] Epoch 8.3600: train_loss/word=4.827847 (steps=3829, words/sec=8286.80, time=0-00:10:31)
[switchout.asean.th-en] Epoch 8.4120: train_loss/word=4.749444 (steps=3852, words/sec=8028.21, time=0-00:10:32)
[switchout.asean.th-en] Epoch 8.4633: train_loss/word=4.704326 (steps=3876, words/sec=7487.22, time=0-00:10:33)
[switchout.asean.th-en] Epoch 8.5143: train_loss/word=4.714610 (steps=3899, words/sec=8460.56, time=0-00:10:34)
[switchout.asean.th-en] Epoch 8.5671: train_loss/word=4.640861 (steps=3922, words/sec=8945.58, time=0-00:10:35)
[switchout.asean.th-en] Epoch 8.6196: train_loss/word=4.806830 (steps=3945, words/sec=9104.69, time=0-00:10:36)
[switchout.asean.th-en] Epoch 8.6707: train_loss/word=4.651649 (steps=3967, words/sec=8918.30, time=0-00:10:37)
[switchout.asean.th-en] Epoch 8.7229: train_loss/word=4.726382 (steps=3990, words/sec=8659.42, time=0-00:10:38)
[switchout.asean.th-en] Epoch 8.7737: train_loss/word=4.719196 (steps=4013, words/sec=7780.46, time=0-00:10:39)
[switchout.asean.th-en] Epoch 8.8255: train_loss/word=4.689060 (steps=4037, words/sec=8764.08, time=0-00:10:40)
[switchout.asean.th-en] Epoch 8.8768: train_loss/word=4.821995 (steps=4062, words/sec=7292.46, time=0-00:10:41)
[switchout.asean.th-en] Epoch 8.9290: train_loss/word=4.799435 (steps=4085, words/sec=8236.93, time=0-00:10:42)
[switchout.asean.th-en] Epoch 8.9793: train_loss/word=4.691322 (steps=4109, words/sec=7874.21, time=0-00:10:43)
[switchout.asean.th-en] Epoch 9.0000: train_loss/word=4.538357 (steps=4117, words/sec=10225.96, time=0-00:10:43)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 9.0000 dev BLEU4: 0.16666493150971642, 0.395413/0.214274/0.127409/0.071752 (BP = 0.999033, ratio=1.00, hyp_len=7238, ref_len=7245) (time=0-00:11:13)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.196455
[switchout.asean.th-en]              dev auxiliary Loss: 4.778 (ref_len=7245)
             checkpoint took 0-00:00:29
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 9.0021: train_loss/word=3.535952 (steps=4118, words/sec=5674.46, time=0-00:11:22)
[switchout.asean.th-en] Epoch 9.0533: train_loss/word=4.496510 (steps=4141, words/sec=8186.37, time=0-00:11:23)
[switchout.asean.th-en] Epoch 9.1050: train_loss/word=4.664062 (steps=4165, words/sec=8117.08, time=0-00:11:24)
[switchout.asean.th-en] Epoch 9.1564: train_loss/word=4.458902 (steps=4189, words/sec=8104.26, time=0-00:11:25)
[switchout.asean.th-en] Epoch 9.2076: train_loss/word=4.533862 (steps=4211, words/sec=8530.28, time=0-00:11:26)
[switchout.asean.th-en] Epoch 9.2580: train_loss/word=4.533524 (steps=4235, words/sec=8233.98, time=0-00:11:27)
[switchout.asean.th-en] Epoch 9.3094: train_loss/word=4.421105 (steps=4261, words/sec=8175.76, time=0-00:11:28)
[switchout.asean.th-en] Epoch 9.3594: train_loss/word=4.680897 (steps=4284, words/sec=7517.74, time=0-00:11:29)
[switchout.asean.th-en] Epoch 9.4102: train_loss/word=4.519096 (steps=4307, words/sec=8488.92, time=0-00:11:30)
[switchout.asean.th-en] Epoch 9.4609: train_loss/word=4.512313 (steps=4329, words/sec=8447.87, time=0-00:11:31)
[switchout.asean.th-en] Epoch 9.5111: train_loss/word=4.583782 (steps=4352, words/sec=7147.73, time=0-00:11:32)
[switchout.asean.th-en] Epoch 9.5621: train_loss/word=4.542562 (steps=4377, words/sec=7141.21, time=0-00:11:33)
[switchout.asean.th-en] Epoch 9.6127: train_loss/word=4.625965 (steps=4400, words/sec=7221.01, time=0-00:11:35)
[switchout.asean.th-en] Epoch 9.6631: train_loss/word=4.480225 (steps=4424, words/sec=8356.82, time=0-00:11:36)
[switchout.asean.th-en] Epoch 9.7149: train_loss/word=4.610189 (steps=4445, words/sec=9200.84, time=0-00:11:36)
[switchout.asean.th-en] Epoch 9.7652: train_loss/word=4.587444 (steps=4470, words/sec=7998.52, time=0-00:11:37)
[switchout.asean.th-en] Epoch 9.8178: train_loss/word=4.554788 (steps=4494, words/sec=8375.07, time=0-00:11:39)
[switchout.asean.th-en] Epoch 9.8680: train_loss/word=4.609072 (steps=4516, words/sec=8324.53, time=0-00:11:39)
[switchout.asean.th-en] Epoch 9.9196: train_loss/word=4.557427 (steps=4538, words/sec=9304.36, time=0-00:11:40)
[switchout.asean.th-en] Epoch 9.9704: train_loss/word=4.456228 (steps=4562, words/sec=7834.37, time=0-00:11:41)
[switchout.asean.th-en] Epoch 10.0000: train_loss/word=4.610738 (steps=4575, words/sec=7811.35, time=0-00:11:42)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 10.0000 dev BLEU4: 0.181179279921715, 0.400552/0.226263/0.139942/0.084960 (BP = 1.000000, ratio=1.00, hyp_len=7245, ref_len=7245) (time=0-00:12:12)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.205974
[switchout.asean.th-en]              dev auxiliary Loss: 4.748 (ref_len=7245)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 10.0027: train_loss/word=4.194188 (steps=4576, words/sec=9283.73, time=0-00:12:22)
[switchout.asean.th-en] Epoch 10.0538: train_loss/word=4.348745 (steps=4599, words/sec=8515.99, time=0-00:12:22)
[switchout.asean.th-en] Epoch 10.1054: train_loss/word=4.440024 (steps=4625, words/sec=7214.69, time=0-00:12:24)
[switchout.asean.th-en] Epoch 10.1560: train_loss/word=4.421016 (steps=4647, words/sec=8666.99, time=0-00:12:25)
[switchout.asean.th-en] Epoch 10.2075: train_loss/word=4.415387 (steps=4670, words/sec=8815.51, time=0-00:12:26)
[switchout.asean.th-en] Epoch 10.2578: train_loss/word=4.386918 (steps=4692, words/sec=7854.53, time=0-00:12:26)
[switchout.asean.th-en] Epoch 10.3099: train_loss/word=4.255118 (steps=4718, words/sec=7846.34, time=0-00:12:28)
[switchout.asean.th-en] Epoch 10.3600: train_loss/word=4.412567 (steps=4742, words/sec=7393.16, time=0-00:12:29)
[switchout.asean.th-en] Epoch 10.4120: train_loss/word=4.440706 (steps=4767, words/sec=7824.28, time=0-00:12:30)
[switchout.asean.th-en] Epoch 10.4626: train_loss/word=4.452029 (steps=4790, words/sec=7984.51, time=0-00:12:31)
[switchout.asean.th-en] Epoch 10.5140: train_loss/word=4.480582 (steps=4815, words/sec=7246.94, time=0-00:12:32)
[switchout.asean.th-en] Epoch 10.5653: train_loss/word=4.319178 (steps=4840, words/sec=8100.38, time=0-00:12:33)
[switchout.asean.th-en] Epoch 10.6162: train_loss/word=4.390144 (steps=4864, words/sec=8004.85, time=0-00:12:34)
[switchout.asean.th-en] Epoch 10.6666: train_loss/word=4.359686 (steps=4887, words/sec=8492.20, time=0-00:12:35)
[switchout.asean.th-en] Epoch 10.7181: train_loss/word=4.401558 (steps=4911, words/sec=7838.35, time=0-00:12:36)
[switchout.asean.th-en] Epoch 10.7713: train_loss/word=4.406353 (steps=4935, words/sec=8295.98, time=0-00:12:37)
[switchout.asean.th-en] Epoch 10.8216: train_loss/word=4.538220 (steps=4957, words/sec=8266.41, time=0-00:12:38)
[switchout.asean.th-en] Epoch 10.8725: train_loss/word=4.418140 (steps=4979, words/sec=8983.51, time=0-00:12:39)
[switchout.asean.th-en] Epoch 10.9237: train_loss/word=4.412346 (steps=5002, words/sec=8120.42, time=0-00:12:40)
[switchout.asean.th-en] Epoch 10.9738: train_loss/word=4.578108 (steps=5023, words/sec=9039.90, time=0-00:12:41)
[switchout.asean.th-en] Epoch 11.0000: train_loss/word=4.329324 (steps=5036, words/sec=8026.70, time=0-00:12:41)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 11.0000 dev BLEU4: 0.19258143101405406, 0.421030/0.246248/0.158340/0.102651 (BP = 0.950505, ratio=0.95, hyp_len=6895, ref_len=7245) (time=0-00:13:11)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.217300
[switchout.asean.th-en]              dev auxiliary Loss: 4.738 (ref_len=7245)
             checkpoint took 0-00:00:29
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 11.0027: train_loss/word=4.029006 (steps=5037, words/sec=9477.79, time=0-00:13:20)
[switchout.asean.th-en] Epoch 11.0545: train_loss/word=4.231038 (steps=5061, words/sec=8156.75, time=0-00:13:21)
[switchout.asean.th-en] Epoch 11.1046: train_loss/word=4.277120 (steps=5082, words/sec=8515.05, time=0-00:13:22)
[switchout.asean.th-en] Epoch 11.1557: train_loss/word=4.283906 (steps=5106, words/sec=7823.68, time=0-00:13:23)
[switchout.asean.th-en] Epoch 11.2074: train_loss/word=4.274850 (steps=5130, words/sec=8229.45, time=0-00:13:24)
[switchout.asean.th-en] Epoch 11.2579: train_loss/word=4.146418 (steps=5153, words/sec=7984.37, time=0-00:13:25)
[switchout.asean.th-en] Epoch 11.3092: train_loss/word=4.206466 (steps=5177, words/sec=8065.19, time=0-00:13:26)
[switchout.asean.th-en] Epoch 11.3601: train_loss/word=4.276306 (steps=5201, words/sec=7790.01, time=0-00:13:27)
[switchout.asean.th-en] Epoch 11.4115: train_loss/word=4.290186 (steps=5225, words/sec=8356.63, time=0-00:13:28)
[switchout.asean.th-en] Epoch 11.4619: train_loss/word=4.275156 (steps=5248, words/sec=7747.78, time=0-00:13:29)
[switchout.asean.th-en] Epoch 11.5123: train_loss/word=4.326028 (steps=5270, words/sec=8423.43, time=0-00:13:30)
[switchout.asean.th-en] Epoch 11.5642: train_loss/word=4.250713 (steps=5295, words/sec=7621.57, time=0-00:13:31)
[switchout.asean.th-en] Epoch 11.6151: train_loss/word=4.365561 (steps=5319, words/sec=8113.59, time=0-00:13:32)
[switchout.asean.th-en] Epoch 11.6666: train_loss/word=4.218812 (steps=5342, words/sec=8662.15, time=0-00:13:33)
[switchout.asean.th-en] Epoch 11.7167: train_loss/word=4.232179 (steps=5365, words/sec=7509.48, time=0-00:13:34)
[switchout.asean.th-en] Epoch 11.7691: train_loss/word=4.335529 (steps=5390, words/sec=7444.40, time=0-00:13:35)
[switchout.asean.th-en] Epoch 11.8219: train_loss/word=4.338187 (steps=5412, words/sec=8779.28, time=0-00:13:36)
[switchout.asean.th-en] Epoch 11.8729: train_loss/word=4.422924 (steps=5435, words/sec=8060.78, time=0-00:13:37)
[switchout.asean.th-en] Epoch 11.9233: train_loss/word=4.366220 (steps=5459, words/sec=8099.89, time=0-00:13:38)
[switchout.asean.th-en] Epoch 11.9734: train_loss/word=4.352029 (steps=5481, words/sec=8755.52, time=0-00:13:39)
[switchout.asean.th-en] Epoch 12.0000: train_loss/word=4.342863 (steps=5495, words/sec=7858.25, time=0-00:13:40)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 12.0000 dev BLEU4: 0.21002091487115884, 0.444638/0.266212/0.175207/0.115215 (BP = 0.949926, ratio=0.95, hyp_len=6891, ref_len=7245) (time=0-00:14:08)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.234230
[switchout.asean.th-en]              dev auxiliary Loss: 4.816 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 12.0018: train_loss/word=4.117835 (steps=5496, words/sec=3812.46, time=0-00:14:17)
[switchout.asean.th-en] Epoch 12.0532: train_loss/word=4.096532 (steps=5518, words/sec=9076.88, time=0-00:14:18)
[switchout.asean.th-en] Epoch 12.1036: train_loss/word=4.209377 (steps=5540, words/sec=8863.77, time=0-00:14:19)
[switchout.asean.th-en] Epoch 12.1547: train_loss/word=4.137165 (steps=5565, words/sec=7432.83, time=0-00:14:20)
[switchout.asean.th-en] Epoch 12.2061: train_loss/word=4.292990 (steps=5587, words/sec=8675.31, time=0-00:14:21)
[switchout.asean.th-en] Epoch 12.2579: train_loss/word=4.237457 (steps=5613, words/sec=6799.04, time=0-00:14:23)
[switchout.asean.th-en] Epoch 12.3083: train_loss/word=4.084555 (steps=5637, words/sec=8643.78, time=0-00:14:24)
[switchout.asean.th-en] Epoch 12.3606: train_loss/word=4.261363 (steps=5661, words/sec=8050.72, time=0-00:14:25)
[switchout.asean.th-en] Epoch 12.4116: train_loss/word=4.184779 (steps=5685, words/sec=8012.57, time=0-00:14:26)
[switchout.asean.th-en] Epoch 12.4627: train_loss/word=4.141153 (steps=5708, words/sec=8114.99, time=0-00:14:27)
[switchout.asean.th-en] Epoch 12.5136: train_loss/word=4.189086 (steps=5733, words/sec=7683.95, time=0-00:14:28)
[switchout.asean.th-en] Epoch 12.5655: train_loss/word=4.191090 (steps=5755, words/sec=9014.53, time=0-00:14:29)
[switchout.asean.th-en] Epoch 12.6165: train_loss/word=4.328888 (steps=5777, words/sec=8186.25, time=0-00:14:30)
[switchout.asean.th-en] Epoch 12.6693: train_loss/word=4.213923 (steps=5801, words/sec=8403.19, time=0-00:14:31)
[switchout.asean.th-en] Epoch 12.7211: train_loss/word=4.077732 (steps=5824, words/sec=8316.77, time=0-00:14:32)
[switchout.asean.th-en] Epoch 12.7726: train_loss/word=4.171230 (steps=5849, words/sec=7945.48, time=0-00:14:33)
[switchout.asean.th-en] Epoch 12.8246: train_loss/word=4.070693 (steps=5873, words/sec=8299.41, time=0-00:14:34)
[switchout.asean.th-en] Epoch 12.8756: train_loss/word=4.327419 (steps=5895, words/sec=8524.77, time=0-00:14:35)
[switchout.asean.th-en] Epoch 12.9265: train_loss/word=4.211751 (steps=5920, words/sec=7019.64, time=0-00:14:36)
[switchout.asean.th-en] Epoch 12.9770: train_loss/word=4.439230 (steps=5943, words/sec=7851.38, time=0-00:14:37)
[switchout.asean.th-en] Epoch 13.0000: train_loss/word=4.250060 (steps=5953, words/sec=8695.41, time=0-00:14:37)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 13.0000 dev BLEU4: 0.21831009935127302, 0.434258/0.264296/0.176216/0.119520 (BP = 0.984561, ratio=0.98, hyp_len=7134, ref_len=7245) (time=0-00:15:06)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.236587
[switchout.asean.th-en]              dev auxiliary Loss: 4.771 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 13.0026: train_loss/word=4.742447 (steps=5954, words/sec=6916.88, time=0-00:15:15)
[switchout.asean.th-en] Epoch 13.0533: train_loss/word=4.065722 (steps=5976, words/sec=9143.47, time=0-00:15:16)
[switchout.asean.th-en] Epoch 13.1040: train_loss/word=3.906170 (steps=5999, words/sec=9296.92, time=0-00:15:17)
[switchout.asean.th-en] Epoch 13.1546: train_loss/word=4.100329 (steps=6020, words/sec=8711.15, time=0-00:15:18)
[switchout.asean.th-en] Epoch 13.2073: train_loss/word=3.991525 (steps=6045, words/sec=7343.97, time=0-00:15:19)
[switchout.asean.th-en] Epoch 13.2573: train_loss/word=4.135544 (steps=6067, words/sec=7986.58, time=0-00:15:20)
[switchout.asean.th-en] Epoch 13.3078: train_loss/word=3.988522 (steps=6091, words/sec=8168.38, time=0-00:15:21)
[switchout.asean.th-en] Epoch 13.3593: train_loss/word=3.968159 (steps=6116, words/sec=7792.57, time=0-00:15:22)
[switchout.asean.th-en] Epoch 13.4107: train_loss/word=4.169162 (steps=6139, words/sec=8144.30, time=0-00:15:23)
[switchout.asean.th-en] Epoch 13.4621: train_loss/word=4.012978 (steps=6161, words/sec=8883.85, time=0-00:15:24)
[switchout.asean.th-en] Epoch 13.5131: train_loss/word=4.279876 (steps=6187, words/sec=6522.12, time=0-00:15:25)
[switchout.asean.th-en] Epoch 13.5662: train_loss/word=3.981482 (steps=6211, words/sec=8434.04, time=0-00:15:26)
[switchout.asean.th-en] Epoch 13.6184: train_loss/word=4.119275 (steps=6234, words/sec=8723.76, time=0-00:15:27)
[switchout.asean.th-en] Epoch 13.6711: train_loss/word=4.303300 (steps=6257, words/sec=7922.78, time=0-00:15:28)
[switchout.asean.th-en] Epoch 13.7213: train_loss/word=4.123429 (steps=6279, words/sec=8465.31, time=0-00:15:29)
[switchout.asean.th-en] Epoch 13.7734: train_loss/word=4.070687 (steps=6305, words/sec=7171.22, time=0-00:15:30)
[switchout.asean.th-en] Epoch 13.8250: train_loss/word=4.248717 (steps=6330, words/sec=7371.29, time=0-00:15:32)
[switchout.asean.th-en] Epoch 13.8759: train_loss/word=3.968940 (steps=6354, words/sec=8810.34, time=0-00:15:33)
[switchout.asean.th-en] Epoch 13.9273: train_loss/word=4.183243 (steps=6377, words/sec=8810.60, time=0-00:15:33)
[switchout.asean.th-en] Epoch 13.9794: train_loss/word=4.095237 (steps=6401, words/sec=8951.08, time=0-00:15:34)
[switchout.asean.th-en] Epoch 14.0000: train_loss/word=4.154701 (steps=6410, words/sec=8355.11, time=0-00:15:35)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 14.0000 dev BLEU4: 0.23818068619924596, 0.489615/0.316338/0.225253/0.167228 (BP = 0.861807, ratio=0.87, hyp_len=6307, ref_len=7245) (time=0-00:16:02)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.255405
[switchout.asean.th-en]              dev auxiliary Loss: 4.793 (ref_len=7245)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 14.0037: train_loss/word=3.938255 (steps=6411, words/sec=14512.49, time=0-00:16:11)
[switchout.asean.th-en] Epoch 14.0537: train_loss/word=3.936561 (steps=6434, words/sec=7186.73, time=0-00:16:12)
[switchout.asean.th-en] Epoch 14.1052: train_loss/word=4.012576 (steps=6459, words/sec=8002.15, time=0-00:16:13)
[switchout.asean.th-en] Epoch 14.1575: train_loss/word=3.986008 (steps=6483, words/sec=7866.84, time=0-00:16:14)
[switchout.asean.th-en] Epoch 14.2096: train_loss/word=3.983863 (steps=6505, words/sec=9563.28, time=0-00:16:15)
[switchout.asean.th-en] Epoch 14.2615: train_loss/word=3.988158 (steps=6528, words/sec=8960.32, time=0-00:16:16)
[switchout.asean.th-en] Epoch 14.3139: train_loss/word=3.962688 (steps=6552, words/sec=8405.98, time=0-00:16:17)
[switchout.asean.th-en] Epoch 14.3654: train_loss/word=4.004480 (steps=6575, words/sec=7664.96, time=0-00:16:18)
[switchout.asean.th-en] Epoch 14.4175: train_loss/word=4.072705 (steps=6597, words/sec=8846.74, time=0-00:16:19)
[switchout.asean.th-en] Epoch 14.4687: train_loss/word=3.940168 (steps=6620, words/sec=8880.98, time=0-00:16:20)
[switchout.asean.th-en] Epoch 14.5201: train_loss/word=3.936558 (steps=6643, words/sec=8722.44, time=0-00:16:21)
[switchout.asean.th-en] Epoch 14.5708: train_loss/word=3.989095 (steps=6667, words/sec=7724.82, time=0-00:16:22)
[switchout.asean.th-en] Epoch 14.6230: train_loss/word=4.028295 (steps=6691, words/sec=8592.65, time=0-00:16:23)
[switchout.asean.th-en] Epoch 14.6734: train_loss/word=4.029153 (steps=6714, words/sec=7777.77, time=0-00:16:24)
[switchout.asean.th-en] Epoch 14.7250: train_loss/word=3.995600 (steps=6738, words/sec=8217.50, time=0-00:16:25)
[switchout.asean.th-en] Epoch 14.7760: train_loss/word=4.051805 (steps=6762, words/sec=7859.59, time=0-00:16:26)
[switchout.asean.th-en] Epoch 14.8278: train_loss/word=4.049773 (steps=6786, words/sec=8793.45, time=0-00:16:27)
[switchout.asean.th-en] Epoch 14.8786: train_loss/word=4.086075 (steps=6809, words/sec=8399.26, time=0-00:16:28)
[switchout.asean.th-en] Epoch 14.9300: train_loss/word=3.888954 (steps=6834, words/sec=7466.20, time=0-00:16:29)
[switchout.asean.th-en] Epoch 14.9803: train_loss/word=4.033423 (steps=6858, words/sec=7924.79, time=0-00:16:30)
[switchout.asean.th-en] Epoch 15.0000: train_loss/word=3.987800 (steps=6866, words/sec=9285.07, time=0-00:16:30)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 15.0000 dev BLEU4: 0.23010071022592046, 0.452176/0.281603/0.196302/0.139602 (BP = 0.946733, ratio=0.95, hyp_len=6869, ref_len=7245) (time=0-00:16:59)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.247487
[switchout.asean.th-en]              dev auxiliary Loss: 4.749 (ref_len=7245)
             checkpoint took 0-00:00:28
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 15.0026: train_loss/word=4.389529 (steps=6867, words/sec=10091.73, time=0-00:17:03)
[switchout.asean.th-en] Epoch 15.0541: train_loss/word=3.879056 (steps=6890, words/sec=8244.23, time=0-00:17:04)
[switchout.asean.th-en] Epoch 15.1053: train_loss/word=3.916262 (steps=6913, words/sec=8343.79, time=0-00:17:05)
[switchout.asean.th-en] Epoch 15.1575: train_loss/word=3.968878 (steps=6936, words/sec=8245.49, time=0-00:17:06)
[switchout.asean.th-en] Epoch 15.2095: train_loss/word=3.882271 (steps=6960, words/sec=8110.79, time=0-00:17:07)
[switchout.asean.th-en] Epoch 15.2600: train_loss/word=3.974317 (steps=6983, words/sec=8401.26, time=0-00:17:08)
[switchout.asean.th-en] Epoch 15.3122: train_loss/word=3.806744 (steps=7006, words/sec=8772.60, time=0-00:17:09)
[switchout.asean.th-en] Epoch 15.3631: train_loss/word=3.760891 (steps=7030, words/sec=8832.15, time=0-00:17:10)
[switchout.asean.th-en] Epoch 15.4140: train_loss/word=3.751488 (steps=7052, words/sec=8910.71, time=0-00:17:11)
[switchout.asean.th-en] Epoch 15.4653: train_loss/word=3.980983 (steps=7076, words/sec=7092.29, time=0-00:17:12)
[switchout.asean.th-en] Epoch 15.5163: train_loss/word=4.061954 (steps=7100, words/sec=7523.91, time=0-00:17:13)
[switchout.asean.th-en] Epoch 15.5668: train_loss/word=3.981636 (steps=7123, words/sec=8178.91, time=0-00:17:14)
[switchout.asean.th-en] Epoch 15.6189: train_loss/word=3.802484 (steps=7145, words/sec=9846.20, time=0-00:17:15)
[switchout.asean.th-en] Epoch 15.6691: train_loss/word=3.885059 (steps=7171, words/sec=6586.10, time=0-00:17:16)
[switchout.asean.th-en] Epoch 15.7214: train_loss/word=3.934402 (steps=7195, words/sec=8330.52, time=0-00:17:17)
[switchout.asean.th-en] Epoch 15.7726: train_loss/word=3.742558 (steps=7219, words/sec=7423.99, time=0-00:17:18)
[switchout.asean.th-en] Epoch 15.8235: train_loss/word=4.119758 (steps=7242, words/sec=7677.11, time=0-00:17:19)
[switchout.asean.th-en] Epoch 15.8749: train_loss/word=4.088073 (steps=7266, words/sec=8349.16, time=0-00:17:20)
[switchout.asean.th-en] Epoch 15.9271: train_loss/word=4.004640 (steps=7291, words/sec=8109.92, time=0-00:17:21)
[switchout.asean.th-en] Epoch 15.9782: train_loss/word=3.971889 (steps=7315, words/sec=8588.74, time=0-00:17:22)
[switchout.asean.th-en] Epoch 16.0000: train_loss/word=3.924525 (steps=7324, words/sec=9612.02, time=0-00:17:23)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 16.0000 dev BLEU4: 0.24439556308659838, 0.468470/0.300936/0.212089/0.154727 (BP = 0.937094, ratio=0.94, hyp_len=6803, ref_len=7245) (time=0-00:17:50)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.260668
[switchout.asean.th-en]              dev auxiliary Loss: 4.733 (ref_len=7245)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 16.0022: train_loss/word=3.663609 (steps=7325, words/sec=9032.88, time=0-00:17:59)
[switchout.asean.th-en] Epoch 16.0527: train_loss/word=3.737677 (steps=7349, words/sec=8577.27, time=0-00:18:01)
[switchout.asean.th-en] Epoch 16.1038: train_loss/word=3.826984 (steps=7372, words/sec=8613.91, time=0-00:18:01)
[switchout.asean.th-en] Epoch 16.1547: train_loss/word=3.772103 (steps=7396, words/sec=7943.16, time=0-00:18:02)
[switchout.asean.th-en] Epoch 16.2054: train_loss/word=3.961166 (steps=7417, words/sec=9236.50, time=0-00:18:03)
[switchout.asean.th-en] Epoch 16.2574: train_loss/word=3.774495 (steps=7441, words/sec=8099.26, time=0-00:18:04)
[switchout.asean.th-en] Epoch 16.3075: train_loss/word=3.929878 (steps=7463, words/sec=8616.67, time=0-00:18:05)
[switchout.asean.th-en] Epoch 16.3593: train_loss/word=3.588880 (steps=7488, words/sec=8670.11, time=0-00:18:06)
[switchout.asean.th-en] Epoch 16.4117: train_loss/word=3.926356 (steps=7511, words/sec=8123.84, time=0-00:18:07)
[switchout.asean.th-en] Epoch 16.4624: train_loss/word=3.850455 (steps=7536, words/sec=7303.97, time=0-00:18:08)
[switchout.asean.th-en] Epoch 16.5128: train_loss/word=3.870951 (steps=7558, words/sec=8664.77, time=0-00:18:09)
[switchout.asean.th-en] Epoch 16.5636: train_loss/word=4.011216 (steps=7580, words/sec=8153.96, time=0-00:18:10)
[switchout.asean.th-en] Epoch 16.6155: train_loss/word=3.842403 (steps=7605, words/sec=8076.18, time=0-00:18:11)
[switchout.asean.th-en] Epoch 16.6687: train_loss/word=3.792526 (steps=7628, words/sec=8651.37, time=0-00:18:12)
[switchout.asean.th-en] Epoch 16.7202: train_loss/word=3.908273 (steps=7651, words/sec=8801.20, time=0-00:18:13)
[switchout.asean.th-en] Epoch 16.7714: train_loss/word=3.949821 (steps=7675, words/sec=7505.69, time=0-00:18:14)
[switchout.asean.th-en] Epoch 16.8220: train_loss/word=3.874444 (steps=7698, words/sec=7945.50, time=0-00:18:15)
[switchout.asean.th-en] Epoch 16.8742: train_loss/word=3.856464 (steps=7723, words/sec=7819.65, time=0-00:18:16)
[switchout.asean.th-en] Epoch 16.9254: train_loss/word=3.917151 (steps=7747, words/sec=8293.18, time=0-00:18:17)
[switchout.asean.th-en] Epoch 16.9758: train_loss/word=3.876045 (steps=7772, words/sec=8291.72, time=0-00:18:19)
[switchout.asean.th-en] Epoch 17.0000: train_loss/word=3.851650 (steps=7782, words/sec=9249.19, time=0-00:18:19)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 17.0000 dev BLEU4: 0.25030554503931873, 0.472695/0.305656/0.218021/0.160691 (BP = 0.938414, ratio=0.94, hyp_len=6812, ref_len=7245) (time=0-00:18:46)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.264798
[switchout.asean.th-en]              dev auxiliary Loss: 4.609 (ref_len=7245)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 17.0016: train_loss/word=3.511498 (steps=7783, words/sec=8274.68, time=0-00:18:56)
[switchout.asean.th-en] Epoch 17.0535: train_loss/word=3.728911 (steps=7806, words/sec=8738.40, time=0-00:18:57)
[switchout.asean.th-en] Epoch 17.1035: train_loss/word=3.691863 (steps=7829, words/sec=8378.35, time=0-00:18:58)
[switchout.asean.th-en] Epoch 17.1549: train_loss/word=3.846885 (steps=7854, words/sec=7682.85, time=0-00:18:59)
[switchout.asean.th-en] Epoch 17.2055: train_loss/word=3.952828 (steps=7875, words/sec=8995.99, time=0-00:19:00)
[switchout.asean.th-en] Epoch 17.2578: train_loss/word=3.720258 (steps=7897, words/sec=9082.90, time=0-00:19:00)
[switchout.asean.th-en] Epoch 17.3089: train_loss/word=3.841695 (steps=7919, words/sec=8150.52, time=0-00:19:01)
[switchout.asean.th-en] Epoch 17.3589: train_loss/word=3.796479 (steps=7942, words/sec=8896.29, time=0-00:19:02)
[switchout.asean.th-en] Epoch 17.4101: train_loss/word=3.773974 (steps=7963, words/sec=9045.50, time=0-00:19:03)
[switchout.asean.th-en] Epoch 17.4615: train_loss/word=3.839232 (steps=7989, words/sec=7478.82, time=0-00:19:04)
[switchout.asean.th-en] Epoch 17.5131: train_loss/word=3.825572 (steps=8012, words/sec=8764.28, time=0-00:19:05)
[switchout.asean.th-en] Epoch 17.5636: train_loss/word=3.752238 (steps=8038, words/sec=7439.43, time=0-00:19:07)
[switchout.asean.th-en] Epoch 17.6146: train_loss/word=3.736504 (steps=8062, words/sec=8176.56, time=0-00:19:08)
[switchout.asean.th-en] Epoch 17.6656: train_loss/word=3.751611 (steps=8086, words/sec=7792.10, time=0-00:19:09)
[switchout.asean.th-en] Epoch 17.7164: train_loss/word=3.741583 (steps=8108, words/sec=8678.43, time=0-00:19:10)
[switchout.asean.th-en] Epoch 17.7668: train_loss/word=3.801903 (steps=8130, words/sec=8903.72, time=0-00:19:10)
[switchout.asean.th-en] Epoch 17.8171: train_loss/word=3.608726 (steps=8156, words/sec=7031.31, time=0-00:19:12)
[switchout.asean.th-en] Epoch 17.8697: train_loss/word=3.913453 (steps=8179, words/sec=8269.07, time=0-00:19:13)
[switchout.asean.th-en] Epoch 17.9203: train_loss/word=3.645384 (steps=8204, words/sec=7951.91, time=0-00:19:14)
[switchout.asean.th-en] Epoch 17.9707: train_loss/word=3.973182 (steps=8228, words/sec=8018.56, time=0-00:19:15)
[switchout.asean.th-en] Epoch 18.0000: train_loss/word=3.949586 (steps=8241, words/sec=8618.04, time=0-00:19:15)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 18.0000 dev BLEU4: 0.2483594840202067, 0.477563/0.312500/0.221909/0.162932 (BP = 0.916358, ratio=0.92, hyp_len=6663, ref_len=7245) (time=0-00:19:43)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.261877
[switchout.asean.th-en]              dev auxiliary Loss: 4.637 (ref_len=7245)
             checkpoint took 0-00:00:28
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 18.0020: train_loss/word=3.750072 (steps=8242, words/sec=4970.54, time=0-00:19:47)
[switchout.asean.th-en] Epoch 18.0550: train_loss/word=3.594673 (steps=8269, words/sec=7385.07, time=0-00:19:49)
[switchout.asean.th-en] Epoch 18.1063: train_loss/word=3.633434 (steps=8293, words/sec=8248.55, time=0-00:19:50)
[switchout.asean.th-en] Epoch 18.1588: train_loss/word=3.704745 (steps=8316, words/sec=8731.88, time=0-00:19:51)
[switchout.asean.th-en] Epoch 18.2101: train_loss/word=3.759294 (steps=8339, words/sec=7926.20, time=0-00:19:52)
[switchout.asean.th-en] Epoch 18.2615: train_loss/word=3.595685 (steps=8363, words/sec=8059.30, time=0-00:19:53)
[switchout.asean.th-en] Epoch 18.3124: train_loss/word=3.684657 (steps=8388, words/sec=6918.32, time=0-00:19:54)
[switchout.asean.th-en] Epoch 18.3644: train_loss/word=3.802375 (steps=8410, words/sec=8387.86, time=0-00:19:55)
[switchout.asean.th-en] Epoch 18.4155: train_loss/word=3.876643 (steps=8434, words/sec=7355.01, time=0-00:19:56)
[switchout.asean.th-en] Epoch 18.4670: train_loss/word=3.679216 (steps=8455, words/sec=8983.77, time=0-00:19:57)
[switchout.asean.th-en] Epoch 18.5175: train_loss/word=3.886401 (steps=8475, words/sec=10014.48, time=0-00:19:57)
[switchout.asean.th-en] Epoch 18.5691: train_loss/word=3.847087 (steps=8500, words/sec=7759.40, time=0-00:19:59)
[switchout.asean.th-en] Epoch 18.6203: train_loss/word=3.749718 (steps=8525, words/sec=7656.61, time=0-00:20:00)
[switchout.asean.th-en] Epoch 18.6722: train_loss/word=3.660541 (steps=8548, words/sec=8974.68, time=0-00:20:01)
[switchout.asean.th-en] Epoch 18.7228: train_loss/word=3.699516 (steps=8572, words/sec=8282.26, time=0-00:20:02)
[switchout.asean.th-en] Epoch 18.7740: train_loss/word=3.595641 (steps=8597, words/sec=7567.63, time=0-00:20:03)
[switchout.asean.th-en] Epoch 18.8264: train_loss/word=3.631184 (steps=8621, words/sec=7806.60, time=0-00:20:04)
[switchout.asean.th-en] Epoch 18.8785: train_loss/word=3.625055 (steps=8645, words/sec=9023.84, time=0-00:20:05)
[switchout.asean.th-en] Epoch 18.9290: train_loss/word=3.813236 (steps=8667, words/sec=9366.14, time=0-00:20:06)
[switchout.asean.th-en] Epoch 18.9793: train_loss/word=3.717256 (steps=8692, words/sec=7937.97, time=0-00:20:07)
[switchout.asean.th-en] Epoch 19.0000: train_loss/word=3.717214 (steps=8701, words/sec=9698.53, time=0-00:20:07)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 19.0000 dev BLEU4: 0.25326730111132123, 0.474039/0.305512/0.221336/0.164899 (BP = 0.939293, ratio=0.94, hyp_len=6818, ref_len=7245) (time=0-00:20:35)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.266869
[switchout.asean.th-en]              dev auxiliary Loss: 4.636 (ref_len=7245)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 19.0015: train_loss/word=3.429351 (steps=8702, words/sec=6809.13, time=0-00:20:44)
[switchout.asean.th-en] Epoch 19.0518: train_loss/word=3.632718 (steps=8727, words/sec=7930.34, time=0-00:20:45)
[switchout.asean.th-en] Epoch 19.1032: train_loss/word=3.706682 (steps=8749, words/sec=8619.17, time=0-00:20:46)
[switchout.asean.th-en] Epoch 19.1557: train_loss/word=3.823521 (steps=8771, words/sec=8599.55, time=0-00:20:47)
[switchout.asean.th-en] Epoch 19.2065: train_loss/word=3.606305 (steps=8795, words/sec=7978.23, time=0-00:20:48)
[switchout.asean.th-en] Epoch 19.2567: train_loss/word=3.669964 (steps=8816, words/sec=8900.80, time=0-00:20:49)
[switchout.asean.th-en] Epoch 19.3086: train_loss/word=3.557155 (steps=8841, words/sec=8114.76, time=0-00:20:50)
[switchout.asean.th-en] Epoch 19.3592: train_loss/word=3.722523 (steps=8866, words/sec=6909.28, time=0-00:20:51)
[switchout.asean.th-en] Epoch 19.4102: train_loss/word=3.763404 (steps=8889, words/sec=8828.30, time=0-00:20:52)
[switchout.asean.th-en] Epoch 19.4638: train_loss/word=3.614985 (steps=8914, words/sec=8216.58, time=0-00:20:53)
[switchout.asean.th-en] Epoch 19.5161: train_loss/word=3.794564 (steps=8937, words/sec=8700.30, time=0-00:20:54)
[switchout.asean.th-en] Epoch 19.5664: train_loss/word=3.559895 (steps=8961, words/sec=7999.28, time=0-00:20:55)
[switchout.asean.th-en] Epoch 19.6174: train_loss/word=3.604519 (steps=8987, words/sec=7421.38, time=0-00:20:56)
[switchout.asean.th-en] Epoch 19.6680: train_loss/word=3.748314 (steps=9007, words/sec=9133.83, time=0-00:20:57)
[switchout.asean.th-en] Epoch 19.7193: train_loss/word=3.611027 (steps=9031, words/sec=8247.17, time=0-00:20:58)
[switchout.asean.th-en] Epoch 19.7695: train_loss/word=3.667472 (steps=9055, words/sec=7351.28, time=0-00:20:59)
[switchout.asean.th-en] Epoch 19.8204: train_loss/word=3.647470 (steps=9079, words/sec=7694.53, time=0-00:21:00)
[switchout.asean.th-en] Epoch 19.8718: train_loss/word=3.667413 (steps=9102, words/sec=8731.78, time=0-00:21:01)
[switchout.asean.th-en] Epoch 19.9236: train_loss/word=3.665406 (steps=9125, words/sec=8678.78, time=0-00:21:02)
[switchout.asean.th-en] Epoch 19.9759: train_loss/word=3.792136 (steps=9147, words/sec=8442.51, time=0-00:21:03)
[switchout.asean.th-en] Epoch 20.0000: train_loss/word=3.745252 (steps=9158, words/sec=7955.11, time=0-00:21:04)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 20.0000 dev BLEU4: 0.25234813676694434, 0.474507/0.306846/0.219904/0.160000 (BP = 0.943238, ratio=0.94, hyp_len=6845, ref_len=7245) (time=0-00:21:32)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.266938
[switchout.asean.th-en]              dev auxiliary Loss: 4.615 (ref_len=7245)
             checkpoint took 0-00:00:28
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 20.0021: train_loss/word=3.363036 (steps=9159, words/sec=6012.74, time=0-00:21:36)
[switchout.asean.th-en] Epoch 20.0530: train_loss/word=3.534704 (steps=9184, words/sec=7209.18, time=0-00:21:37)
[switchout.asean.th-en] Epoch 20.1033: train_loss/word=3.347120 (steps=9209, words/sec=7691.49, time=0-00:21:38)
[switchout.asean.th-en] Epoch 20.1540: train_loss/word=3.606153 (steps=9233, words/sec=7497.62, time=0-00:21:40)
[switchout.asean.th-en] Epoch 20.2062: train_loss/word=3.620736 (steps=9257, words/sec=8117.72, time=0-00:21:41)
[switchout.asean.th-en] Epoch 20.2563: train_loss/word=3.650213 (steps=9280, words/sec=7918.17, time=0-00:21:42)
[switchout.asean.th-en] Epoch 20.3077: train_loss/word=3.588933 (steps=9302, words/sec=8300.45, time=0-00:21:43)
[switchout.asean.th-en] Epoch 20.3586: train_loss/word=3.818275 (steps=9323, words/sec=8846.41, time=0-00:21:43)
[switchout.asean.th-en] Epoch 20.4089: train_loss/word=3.744817 (steps=9344, words/sec=8423.29, time=0-00:21:44)
[switchout.asean.th-en] Epoch 20.4610: train_loss/word=3.639468 (steps=9368, words/sec=8087.51, time=0-00:21:45)
[switchout.asean.th-en] Epoch 20.5110: train_loss/word=3.515531 (steps=9393, words/sec=8357.78, time=0-00:21:46)
[switchout.asean.th-en] Epoch 20.5620: train_loss/word=3.595448 (steps=9416, words/sec=8887.47, time=0-00:21:47)
[switchout.asean.th-en] Epoch 20.6128: train_loss/word=3.613885 (steps=9439, words/sec=8902.97, time=0-00:21:48)
[switchout.asean.th-en] Epoch 20.6655: train_loss/word=3.679180 (steps=9462, words/sec=8714.31, time=0-00:21:49)
[switchout.asean.th-en] Epoch 20.7156: train_loss/word=3.628069 (steps=9483, words/sec=9649.71, time=0-00:21:50)
[switchout.asean.th-en] Epoch 20.7664: train_loss/word=3.704821 (steps=9505, words/sec=8348.98, time=0-00:21:51)
[switchout.asean.th-en] Epoch 20.8175: train_loss/word=3.722166 (steps=9527, words/sec=9214.82, time=0-00:21:52)
[switchout.asean.th-en] Epoch 20.8677: train_loss/word=3.800405 (steps=9549, words/sec=7792.11, time=0-00:21:53)
[switchout.asean.th-en] Epoch 20.9193: train_loss/word=3.634940 (steps=9572, words/sec=8854.61, time=0-00:21:54)
[switchout.asean.th-en] Epoch 20.9700: train_loss/word=3.573025 (steps=9598, words/sec=8048.83, time=0-00:21:55)
[switchout.asean.th-en] Epoch 21.0000: train_loss/word=3.616228 (steps=9612, words/sec=8160.72, time=0-00:21:56)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 21.0000 dev BLEU4: 0.26331797421856845, 0.503734/0.335742/0.247887/0.190659 (BP = 0.880645, ratio=0.89, hyp_len=6428, ref_len=7245) (time=0-00:22:24)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.275958
[switchout.asean.th-en]              dev auxiliary Loss: 4.596 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 21.0029: train_loss/word=3.360558 (steps=9613, words/sec=10344.64, time=0-00:22:33)
[switchout.asean.th-en] Epoch 21.0545: train_loss/word=3.479551 (steps=9637, words/sec=8148.79, time=0-00:22:34)
[switchout.asean.th-en] Epoch 21.1055: train_loss/word=3.751121 (steps=9658, words/sec=9334.37, time=0-00:22:35)
[switchout.asean.th-en] Epoch 21.1569: train_loss/word=3.499650 (steps=9682, words/sec=8038.63, time=0-00:22:36)
[switchout.asean.th-en] Epoch 21.2077: train_loss/word=3.645684 (steps=9708, words/sec=6998.85, time=0-00:22:37)
[switchout.asean.th-en] Epoch 21.2595: train_loss/word=3.533207 (steps=9734, words/sec=7034.06, time=0-00:22:39)
[switchout.asean.th-en] Epoch 21.3110: train_loss/word=3.619500 (steps=9756, words/sec=8547.92, time=0-00:22:39)
[switchout.asean.th-en] Epoch 21.3637: train_loss/word=3.547122 (steps=9779, words/sec=8449.21, time=0-00:22:40)
[switchout.asean.th-en] Epoch 21.4150: train_loss/word=3.633933 (steps=9802, words/sec=8589.00, time=0-00:22:41)
[switchout.asean.th-en] Epoch 21.4664: train_loss/word=3.571490 (steps=9827, words/sec=7926.88, time=0-00:22:42)
[switchout.asean.th-en] Epoch 21.5173: train_loss/word=3.496097 (steps=9850, words/sec=7714.55, time=0-00:22:43)
[switchout.asean.th-en] Epoch 21.5691: train_loss/word=3.673454 (steps=9871, words/sec=9322.06, time=0-00:22:44)
[switchout.asean.th-en] Epoch 21.6199: train_loss/word=3.579744 (steps=9895, words/sec=7771.87, time=0-00:22:45)
[switchout.asean.th-en] Epoch 21.6714: train_loss/word=3.571890 (steps=9921, words/sec=7534.86, time=0-00:22:46)
[switchout.asean.th-en] Epoch 21.7220: train_loss/word=3.433972 (steps=9946, words/sec=8311.12, time=0-00:22:48)
[switchout.asean.th-en] Epoch 21.7740: train_loss/word=3.662002 (steps=9969, words/sec=8884.29, time=0-00:22:49)
[switchout.asean.th-en] Epoch 21.8264: train_loss/word=3.539866 (steps=9994, words/sec=7295.78, time=0-00:22:50)
[switchout.asean.th-en] Epoch 21.8785: train_loss/word=3.715568 (steps=10016, words/sec=9548.18, time=0-00:22:51)
[switchout.asean.th-en] Epoch 21.9300: train_loss/word=3.541223 (steps=10038, words/sec=8109.58, time=0-00:22:52)
[switchout.asean.th-en] Epoch 21.9814: train_loss/word=3.703232 (steps=10061, words/sec=8157.14, time=0-00:22:52)
[switchout.asean.th-en] Epoch 22.0000: train_loss/word=3.610866 (steps=10070, words/sec=7900.29, time=0-00:22:53)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 22.0000 dev BLEU4: 0.26127962473941185, 0.479570/0.314061/0.227706/0.168322 (BP = 0.947895, ratio=0.95, hyp_len=6877, ref_len=7245) (time=0-00:23:22)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.273955
[switchout.asean.th-en]              dev auxiliary Loss: 4.614 (ref_len=7245)
             checkpoint took 0-00:00:28
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 22.0026: train_loss/word=4.101716 (steps=10071, words/sec=9647.24, time=0-00:23:26)
[switchout.asean.th-en] Epoch 22.0534: train_loss/word=3.624866 (steps=10095, words/sec=7664.14, time=0-00:23:27)
[switchout.asean.th-en] Epoch 22.1044: train_loss/word=3.613309 (steps=10117, words/sec=8748.04, time=0-00:23:27)
[switchout.asean.th-en] Epoch 22.1569: train_loss/word=3.469664 (steps=10142, words/sec=6933.34, time=0-00:23:29)
[switchout.asean.th-en] Epoch 22.2086: train_loss/word=3.625283 (steps=10166, words/sec=7558.15, time=0-00:23:30)
[switchout.asean.th-en] Epoch 22.2599: train_loss/word=3.541739 (steps=10190, words/sec=7937.87, time=0-00:23:31)
[switchout.asean.th-en] Epoch 22.3114: train_loss/word=3.405163 (steps=10217, words/sec=7329.94, time=0-00:23:32)
[switchout.asean.th-en] Epoch 22.3625: train_loss/word=3.522551 (steps=10241, words/sec=7924.43, time=0-00:23:33)
[switchout.asean.th-en] Epoch 22.4140: train_loss/word=3.647561 (steps=10266, words/sec=7642.66, time=0-00:23:34)
[switchout.asean.th-en] Epoch 22.4646: train_loss/word=3.451935 (steps=10290, words/sec=7841.47, time=0-00:23:35)
[switchout.asean.th-en] Epoch 22.5159: train_loss/word=3.547914 (steps=10314, words/sec=7864.84, time=0-00:23:36)
[switchout.asean.th-en] Epoch 22.5678: train_loss/word=3.750023 (steps=10337, words/sec=8243.55, time=0-00:23:37)
[switchout.asean.th-en] Epoch 22.6188: train_loss/word=3.533740 (steps=10359, words/sec=8484.30, time=0-00:23:38)
[switchout.asean.th-en] Epoch 22.6706: train_loss/word=3.516171 (steps=10382, words/sec=9118.71, time=0-00:23:39)
[switchout.asean.th-en] Epoch 22.7213: train_loss/word=3.497244 (steps=10405, words/sec=8865.22, time=0-00:23:40)
[switchout.asean.th-en] Epoch 22.7719: train_loss/word=3.451645 (steps=10430, words/sec=7699.35, time=0-00:23:41)
[switchout.asean.th-en] Epoch 22.8236: train_loss/word=3.521078 (steps=10454, words/sec=7467.36, time=0-00:23:42)
[switchout.asean.th-en] Epoch 22.8739: train_loss/word=3.624774 (steps=10474, words/sec=9123.75, time=0-00:23:43)
[switchout.asean.th-en] Epoch 22.9243: train_loss/word=3.604203 (steps=10494, words/sec=9635.02, time=0-00:23:44)
[switchout.asean.th-en] Epoch 22.9763: train_loss/word=3.520340 (steps=10519, words/sec=7918.19, time=0-00:23:45)
[switchout.asean.th-en] Epoch 23.0000: train_loss/word=3.611684 (steps=10530, words/sec=8617.40, time=0-00:23:45)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 23.0000 dev BLEU4: 0.26608437244658084, 0.504657/0.338939/0.251538/0.191821 (BP = 0.882805, ratio=0.89, hyp_len=6442, ref_len=7245) (time=0-00:24:13)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.276628
[switchout.asean.th-en]              dev auxiliary Loss: 4.618 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 23.0021: train_loss/word=4.168427 (steps=10531, words/sec=7641.71, time=0-00:24:23)
[switchout.asean.th-en] Epoch 23.0532: train_loss/word=3.403526 (steps=10553, words/sec=8864.82, time=0-00:24:24)
[switchout.asean.th-en] Epoch 23.1032: train_loss/word=3.444455 (steps=10577, words/sec=8211.17, time=0-00:24:25)
[switchout.asean.th-en] Epoch 23.1541: train_loss/word=3.338693 (steps=10600, words/sec=8135.39, time=0-00:24:26)
[switchout.asean.th-en] Epoch 23.2050: train_loss/word=3.460876 (steps=10622, words/sec=8818.00, time=0-00:24:27)
[switchout.asean.th-en] Epoch 23.2572: train_loss/word=3.538701 (steps=10644, words/sec=9755.28, time=0-00:24:27)
[switchout.asean.th-en] Epoch 23.3082: train_loss/word=3.665127 (steps=10667, words/sec=7913.03, time=0-00:24:28)
[switchout.asean.th-en] Epoch 23.3583: train_loss/word=3.484560 (steps=10692, words/sec=7591.62, time=0-00:24:29)
[switchout.asean.th-en] Epoch 23.4111: train_loss/word=3.611309 (steps=10716, words/sec=8547.03, time=0-00:24:30)
[switchout.asean.th-en] Epoch 23.4618: train_loss/word=3.337663 (steps=10740, words/sec=8543.37, time=0-00:24:31)
[switchout.asean.th-en] Epoch 23.5123: train_loss/word=3.566564 (steps=10764, words/sec=8249.40, time=0-00:24:33)
[switchout.asean.th-en] Epoch 23.5634: train_loss/word=3.605545 (steps=10787, words/sec=8832.02, time=0-00:24:33)
[switchout.asean.th-en] Epoch 23.6151: train_loss/word=3.567637 (steps=10808, words/sec=9389.61, time=0-00:24:34)
[switchout.asean.th-en] Epoch 23.6668: train_loss/word=3.439359 (steps=10833, words/sec=7298.82, time=0-00:24:35)
[switchout.asean.th-en] Epoch 23.7171: train_loss/word=3.505096 (steps=10858, words/sec=7269.07, time=0-00:24:37)
[switchout.asean.th-en] Epoch 23.7685: train_loss/word=3.465472 (steps=10881, words/sec=8080.97, time=0-00:24:38)
[switchout.asean.th-en] Epoch 23.8201: train_loss/word=3.738074 (steps=10904, words/sec=8395.56, time=0-00:24:39)
[switchout.asean.th-en] Epoch 23.8703: train_loss/word=3.546952 (steps=10926, words/sec=8162.50, time=0-00:24:39)
[switchout.asean.th-en] Epoch 23.9211: train_loss/word=3.600231 (steps=10949, words/sec=7750.95, time=0-00:24:41)
[switchout.asean.th-en] Epoch 23.9721: train_loss/word=3.506790 (steps=10972, words/sec=8319.34, time=0-00:24:42)
[switchout.asean.th-en] Epoch 24.0000: train_loss/word=3.621943 (steps=10985, words/sec=7739.63, time=0-00:24:42)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 24.0000 dev BLEU4: 0.2628367640429723, 0.513522/0.344104/0.252227/0.191873 (BP = 0.864316, ratio=0.87, hyp_len=6323, ref_len=7245) (time=0-00:25:10)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.277155
[switchout.asean.th-en]              dev auxiliary Loss: 4.586 (ref_len=7245)
             checkpoint took 0-00:00:27
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 24.0015: train_loss/word=3.295134 (steps=10986, words/sec=6431.19, time=0-00:25:13)
[switchout.asean.th-en] Epoch 24.0534: train_loss/word=3.521852 (steps=11009, words/sec=8456.28, time=0-00:25:14)
[switchout.asean.th-en] Epoch 24.1036: train_loss/word=3.527178 (steps=11033, words/sec=8204.89, time=0-00:25:15)
[switchout.asean.th-en] Epoch 24.1536: train_loss/word=3.424937 (steps=11055, words/sec=8641.36, time=0-00:25:16)
[switchout.asean.th-en] Epoch 24.2057: train_loss/word=3.501714 (steps=11078, words/sec=8380.34, time=0-00:25:17)
[switchout.asean.th-en] Epoch 24.2563: train_loss/word=3.495542 (steps=11101, words/sec=8948.09, time=0-00:25:18)
[switchout.asean.th-en] Epoch 24.3074: train_loss/word=3.427851 (steps=11127, words/sec=7609.97, time=0-00:25:19)
[switchout.asean.th-en] Epoch 24.3581: train_loss/word=3.554417 (steps=11149, words/sec=8418.31, time=0-00:25:20)
[switchout.asean.th-en] Epoch 24.4087: train_loss/word=3.249098 (steps=11174, words/sec=8252.37, time=0-00:25:21)
[switchout.asean.th-en] Epoch 24.4604: train_loss/word=3.639463 (steps=11198, words/sec=8062.43, time=0-00:25:22)
[switchout.asean.th-en] Epoch 24.5122: train_loss/word=3.417489 (steps=11221, words/sec=8269.73, time=0-00:25:23)
[switchout.asean.th-en] Epoch 24.5628: train_loss/word=3.496800 (steps=11241, words/sec=9619.45, time=0-00:25:24)
[switchout.asean.th-en] Epoch 24.6164: train_loss/word=3.443273 (steps=11266, words/sec=7786.60, time=0-00:25:25)
[switchout.asean.th-en] Epoch 24.6666: train_loss/word=3.470316 (steps=11289, words/sec=7915.18, time=0-00:25:26)
[switchout.asean.th-en] Epoch 24.7194: train_loss/word=3.718790 (steps=11313, words/sec=7903.99, time=0-00:25:27)
[switchout.asean.th-en] Epoch 24.7721: train_loss/word=3.633913 (steps=11337, words/sec=8123.82, time=0-00:25:28)
[switchout.asean.th-en] Epoch 24.8231: train_loss/word=3.526571 (steps=11361, words/sec=8553.07, time=0-00:25:29)
[switchout.asean.th-en] Epoch 24.8733: train_loss/word=3.303601 (steps=11387, words/sec=6934.14, time=0-00:25:31)
[switchout.asean.th-en] Epoch 24.9251: train_loss/word=3.759927 (steps=11410, words/sec=8426.78, time=0-00:25:32)
[switchout.asean.th-en] Epoch 24.9753: train_loss/word=3.493509 (steps=11433, words/sec=7945.92, time=0-00:25:33)
[switchout.asean.th-en] Epoch 25.0000: train_loss/word=3.691766 (steps=11445, words/sec=7429.41, time=0-00:25:33)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 25.0000 dev BLEU4: 0.27586839387130857, 0.503510/0.335629/0.249515/0.190789 (BP = 0.921133, ratio=0.92, hyp_len=6695, ref_len=7245) (time=0-00:26:01)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.288502
[switchout.asean.th-en]              dev auxiliary Loss: 4.571 (ref_len=7245)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 25.0025: train_loss/word=3.730522 (steps=11446, words/sec=10413.30, time=0-00:26:10)
[switchout.asean.th-en] Epoch 25.0549: train_loss/word=3.566911 (steps=11468, words/sec=9106.38, time=0-00:26:11)
[switchout.asean.th-en] Epoch 25.1051: train_loss/word=3.500323 (steps=11490, words/sec=8360.18, time=0-00:26:12)
[switchout.asean.th-en] Epoch 25.1571: train_loss/word=3.402871 (steps=11514, words/sec=8612.26, time=0-00:26:13)
[switchout.asean.th-en] Epoch 25.2091: train_loss/word=3.444209 (steps=11537, words/sec=8661.80, time=0-00:26:14)
[switchout.asean.th-en] Epoch 25.2603: train_loss/word=3.302186 (steps=11562, words/sec=7679.03, time=0-00:26:15)
[switchout.asean.th-en] Epoch 25.3117: train_loss/word=3.319602 (steps=11588, words/sec=7834.66, time=0-00:26:16)
[switchout.asean.th-en] Epoch 25.3637: train_loss/word=3.503170 (steps=11612, words/sec=7524.20, time=0-00:26:17)
[switchout.asean.th-en] Epoch 25.4152: train_loss/word=3.436401 (steps=11637, words/sec=8131.00, time=0-00:26:18)
[switchout.asean.th-en] Epoch 25.4662: train_loss/word=3.498274 (steps=11659, words/sec=8291.94, time=0-00:26:19)
[switchout.asean.th-en] Epoch 25.5183: train_loss/word=3.552619 (steps=11682, words/sec=7256.28, time=0-00:26:20)
[switchout.asean.th-en] Epoch 25.5697: train_loss/word=3.572263 (steps=11705, words/sec=8187.01, time=0-00:26:21)
[switchout.asean.th-en] Epoch 25.6218: train_loss/word=3.591071 (steps=11727, words/sec=8999.49, time=0-00:26:22)
[switchout.asean.th-en] Epoch 25.6741: train_loss/word=3.471432 (steps=11750, words/sec=8718.32, time=0-00:26:23)
[switchout.asean.th-en] Epoch 25.7267: train_loss/word=3.585970 (steps=11773, words/sec=9180.62, time=0-00:26:24)
[switchout.asean.th-en] Epoch 25.7771: train_loss/word=3.345708 (steps=11797, words/sec=8031.34, time=0-00:26:25)
[switchout.asean.th-en] Epoch 25.8289: train_loss/word=3.271684 (steps=11821, words/sec=8655.02, time=0-00:26:26)
[switchout.asean.th-en] Epoch 25.8801: train_loss/word=3.443874 (steps=11845, words/sec=8379.83, time=0-00:26:27)
[switchout.asean.th-en] Epoch 25.9316: train_loss/word=3.560513 (steps=11869, words/sec=7085.03, time=0-00:26:28)
[switchout.asean.th-en] Epoch 25.9817: train_loss/word=3.523961 (steps=11894, words/sec=7379.32, time=0-00:26:29)
[switchout.asean.th-en] Epoch 26.0000: train_loss/word=3.434397 (steps=11902, words/sec=8860.27, time=0-00:26:30)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 26.0000 dev BLEU4: 0.27098316760186447, 0.491145/0.328634/0.240262/0.183400 (BP = 0.933126, ratio=0.94, hyp_len=6776, ref_len=7245) (time=0-00:26:58)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.282661
[switchout.asean.th-en]              dev auxiliary Loss: 4.580 (ref_len=7245)
             checkpoint took 0-00:00:28
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 26.0021: train_loss/word=3.224068 (steps=11903, words/sec=8352.61, time=0-00:27:02)
[switchout.asean.th-en] Epoch 26.0533: train_loss/word=3.392595 (steps=11927, words/sec=7912.96, time=0-00:27:03)
[switchout.asean.th-en] Epoch 26.1051: train_loss/word=3.532205 (steps=11951, words/sec=7830.10, time=0-00:27:04)
[switchout.asean.th-en] Epoch 26.1567: train_loss/word=3.401955 (steps=11975, words/sec=7658.04, time=0-00:27:05)
[switchout.asean.th-en] Epoch 26.2082: train_loss/word=3.510842 (steps=11998, words/sec=8543.87, time=0-00:27:06)
[switchout.asean.th-en] Epoch 26.2601: train_loss/word=3.407663 (steps=12022, words/sec=8118.02, time=0-00:27:07)
[switchout.asean.th-en] Epoch 26.3125: train_loss/word=3.459208 (steps=12044, words/sec=9653.27, time=0-00:27:08)
[switchout.asean.th-en] Epoch 26.3631: train_loss/word=3.318694 (steps=12068, words/sec=8821.55, time=0-00:27:09)
[switchout.asean.th-en] Epoch 26.4143: train_loss/word=3.552905 (steps=12091, words/sec=8375.84, time=0-00:27:10)
[switchout.asean.th-en] Epoch 26.4643: train_loss/word=3.433298 (steps=12111, words/sec=9925.10, time=0-00:27:11)
[switchout.asean.th-en] Epoch 26.5151: train_loss/word=3.655719 (steps=12133, words/sec=9400.80, time=0-00:27:12)
[switchout.asean.th-en] Epoch 26.5671: train_loss/word=3.435782 (steps=12159, words/sec=7222.36, time=0-00:27:13)
[switchout.asean.th-en] Epoch 26.6181: train_loss/word=3.543748 (steps=12182, words/sec=8280.98, time=0-00:27:14)
[switchout.asean.th-en] Epoch 26.6696: train_loss/word=3.507817 (steps=12204, words/sec=8720.07, time=0-00:27:15)
[switchout.asean.th-en] Epoch 26.7220: train_loss/word=3.365710 (steps=12230, words/sec=7268.03, time=0-00:27:16)
[switchout.asean.th-en] Epoch 26.7733: train_loss/word=3.488690 (steps=12254, words/sec=7997.28, time=0-00:27:17)
[switchout.asean.th-en] Epoch 26.8249: train_loss/word=3.499949 (steps=12278, words/sec=7678.31, time=0-00:27:18)
[switchout.asean.th-en] Epoch 26.8753: train_loss/word=3.572457 (steps=12302, words/sec=7950.67, time=0-00:27:19)
[switchout.asean.th-en] Epoch 26.9271: train_loss/word=3.474380 (steps=12326, words/sec=7709.17, time=0-00:27:20)
[switchout.asean.th-en] Epoch 26.9794: train_loss/word=3.293532 (steps=12350, words/sec=8433.83, time=0-00:27:21)
[switchout.asean.th-en] Epoch 27.0000: train_loss/word=3.249895 (steps=12360, words/sec=7861.07, time=0-00:27:22)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 27.0000 dev BLEU4: 0.26491227434996795, 0.485689/0.317883/0.233403/0.176127 (BP = 0.938560, ratio=0.94, hyp_len=6813, ref_len=7245) (time=0-00:27:50)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.277513
[switchout.asean.th-en]              dev auxiliary Loss: 4.547 (ref_len=7245)
             checkpoint took 0-00:00:27
  new learning rate: 0.5
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 27.0023: train_loss/word=2.659011 (steps=12361, words/sec=6843.95, time=0-00:27:53)
[switchout.asean.th-en] Epoch 27.0539: train_loss/word=3.304775 (steps=12385, words/sec=8741.60, time=0-00:27:54)
[switchout.asean.th-en] Epoch 27.1062: train_loss/word=3.273533 (steps=12410, words/sec=7079.83, time=0-00:27:56)
[switchout.asean.th-en] Epoch 27.1573: train_loss/word=3.270612 (steps=12434, words/sec=8220.05, time=0-00:27:57)
[switchout.asean.th-en] Epoch 27.2074: train_loss/word=3.216440 (steps=12460, words/sec=6965.17, time=0-00:27:58)
[switchout.asean.th-en] Epoch 27.2578: train_loss/word=3.371356 (steps=12483, words/sec=8390.11, time=0-00:27:59)
[switchout.asean.th-en] Epoch 27.3093: train_loss/word=3.425916 (steps=12505, words/sec=9015.11, time=0-00:28:00)
[switchout.asean.th-en] Epoch 27.3599: train_loss/word=3.229042 (steps=12529, words/sec=7896.75, time=0-00:28:01)
[switchout.asean.th-en] Epoch 27.4119: train_loss/word=3.379083 (steps=12552, words/sec=8397.17, time=0-00:28:02)
[switchout.asean.th-en] Epoch 27.4637: train_loss/word=3.246025 (steps=12576, words/sec=7961.30, time=0-00:28:03)
[switchout.asean.th-en] Epoch 27.5156: train_loss/word=3.498559 (steps=12599, words/sec=8389.78, time=0-00:28:04)
[switchout.asean.th-en] Epoch 27.5679: train_loss/word=3.563119 (steps=12621, words/sec=9011.28, time=0-00:28:05)
[switchout.asean.th-en] Epoch 27.6184: train_loss/word=3.240945 (steps=12646, words/sec=7788.68, time=0-00:28:06)
[switchout.asean.th-en] Epoch 27.6705: train_loss/word=3.411273 (steps=12670, words/sec=8797.49, time=0-00:28:07)
[switchout.asean.th-en] Epoch 27.7228: train_loss/word=3.235877 (steps=12694, words/sec=8624.88, time=0-00:28:08)
[switchout.asean.th-en] Epoch 27.7752: train_loss/word=3.434028 (steps=12716, words/sec=8920.39, time=0-00:28:09)
[switchout.asean.th-en] Epoch 27.8260: train_loss/word=3.452040 (steps=12738, words/sec=8972.29, time=0-00:28:10)
[switchout.asean.th-en] Epoch 27.8770: train_loss/word=3.568763 (steps=12759, words/sec=8852.53, time=0-00:28:10)
[switchout.asean.th-en] Epoch 27.9285: train_loss/word=3.174255 (steps=12785, words/sec=7590.47, time=0-00:28:12)
[switchout.asean.th-en] Epoch 27.9792: train_loss/word=3.352341 (steps=12810, words/sec=7156.29, time=0-00:28:13)
[switchout.asean.th-en] Epoch 28.0000: train_loss/word=3.168307 (steps=12819, words/sec=8503.66, time=0-00:28:13)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 28.0000 dev BLEU4: 0.2761216910191997, 0.498235/0.333853/0.245470/0.184968 (BP = 0.936654, ratio=0.94, hyp_len=6800, ref_len=7245) (time=0-00:28:41)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.288350
[switchout.asean.th-en]              dev auxiliary Loss: 4.483 (ref_len=7245)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 28.0034: train_loss/word=3.495928 (steps=12820, words/sec=15190.28, time=0-00:28:51)
[switchout.asean.th-en] Epoch 28.0543: train_loss/word=3.095989 (steps=12846, words/sec=8024.58, time=0-00:28:52)
[switchout.asean.th-en] Epoch 28.1052: train_loss/word=3.124770 (steps=12871, words/sec=7591.49, time=0-00:28:53)
[switchout.asean.th-en] Epoch 28.1554: train_loss/word=3.300200 (steps=12894, words/sec=7876.40, time=0-00:28:54)
[switchout.asean.th-en] Epoch 28.2079: train_loss/word=3.384852 (steps=12918, words/sec=8174.56, time=0-00:28:55)
[switchout.asean.th-en] Epoch 28.2581: train_loss/word=3.175550 (steps=12940, words/sec=8915.47, time=0-00:28:56)
[switchout.asean.th-en] Epoch 28.3094: train_loss/word=3.316787 (steps=12963, words/sec=7971.16, time=0-00:28:57)
[switchout.asean.th-en] Epoch 28.3621: train_loss/word=3.267128 (steps=12988, words/sec=8052.94, time=0-00:28:58)
[switchout.asean.th-en] Epoch 28.4136: train_loss/word=3.263376 (steps=13012, words/sec=7560.76, time=0-00:28:59)
[switchout.asean.th-en] Epoch 28.4658: train_loss/word=3.474472 (steps=13034, words/sec=8665.23, time=0-00:29:00)
[switchout.asean.th-en] Epoch 28.5171: train_loss/word=3.381840 (steps=13057, words/sec=8281.63, time=0-00:29:01)
[switchout.asean.th-en] Epoch 28.5683: train_loss/word=3.411062 (steps=13080, words/sec=8370.25, time=0-00:29:02)
[switchout.asean.th-en] Epoch 28.6215: train_loss/word=3.411128 (steps=13103, words/sec=8586.40, time=0-00:29:03)
[switchout.asean.th-en] Epoch 28.6729: train_loss/word=3.224039 (steps=13126, words/sec=8875.74, time=0-00:29:04)
[switchout.asean.th-en] Epoch 28.7233: train_loss/word=3.156078 (steps=13150, words/sec=7942.38, time=0-00:29:05)
[switchout.asean.th-en] Epoch 28.7748: train_loss/word=3.273354 (steps=13173, words/sec=8478.22, time=0-00:29:06)
[switchout.asean.th-en] Epoch 28.8257: train_loss/word=3.516269 (steps=13194, words/sec=8675.71, time=0-00:29:07)
[switchout.asean.th-en] Epoch 28.8769: train_loss/word=3.458237 (steps=13216, words/sec=8790.53, time=0-00:29:08)
[switchout.asean.th-en] Epoch 28.9281: train_loss/word=3.267227 (steps=13241, words/sec=8007.57, time=0-00:29:09)
[switchout.asean.th-en] Epoch 28.9784: train_loss/word=3.218543 (steps=13264, words/sec=8784.73, time=0-00:29:10)
[switchout.asean.th-en] Epoch 29.0000: train_loss/word=3.704842 (steps=13274, words/sec=6883.71, time=0-00:29:10)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 29.0000 dev BLEU4: 0.2806523314430044, 0.499339/0.336159/0.249527/0.191122 (BP = 0.938267, ratio=0.94, hyp_len=6811, ref_len=7245) (time=0-00:29:38)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.291586
[switchout.asean.th-en]              dev auxiliary Loss: 4.506 (ref_len=7245)
             checkpoint took 0-00:00:27
  best dev score, writing out model
Starting to read ./data/train.th and ./data/train.en
Done reading ./data/train.th and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 29.0027: train_loss/word=4.546020 (steps=13275, words/sec=7279.09, time=0-00:29:47)
[switchout.asean.th-en] Epoch 29.0537: train_loss/word=3.362292 (steps=13298, words/sec=7409.51, time=0-00:29:48)
[switchout.asean.th-en] Epoch 29.1051: train_loss/word=3.379557 (steps=13320, words/sec=9136.81, time=0-00:29:49)
[switchout.asean.th-en] Epoch 29.1551: train_loss/word=3.353865 (steps=13340, words/sec=9587.26, time=0-00:29:50)
[switchout.asean.th-en] Epoch 29.2064: train_loss/word=3.202787 (steps=13363, words/sec=8000.93, time=0-00:29:51)
[switchout.asean.th-en] Epoch 29.2581: train_loss/word=3.180869 (steps=13388, words/sec=7520.38, time=0-00:29:52)
[switchout.asean.th-en] Epoch 29.3101: train_loss/word=3.354582 (steps=13411, words/sec=7665.94, time=0-00:29:53)
[switchout.asean.th-en] Epoch 29.3618: train_loss/word=3.264492 (steps=13433, words/sec=8952.76, time=0-00:29:54)
[switchout.asean.th-en] Epoch 29.4135: train_loss/word=3.282985 (steps=13456, words/sec=8820.45, time=0-00:29:55)
[switchout.asean.th-en] Epoch 29.4643: train_loss/word=3.241611 (steps=13482, words/sec=7401.44, time=0-00:29:56)
[switchout.asean.th-en] Epoch 29.5145: train_loss/word=3.225567 (steps=13504, words/sec=8987.29, time=0-00:29:57)
[switchout.asean.th-en] Epoch 29.5658: train_loss/word=3.254171 (steps=13530, words/sec=6835.40, time=0-00:29:58)
[switchout.asean.th-en] Epoch 29.6169: train_loss/word=3.359171 (steps=13553, words/sec=8783.06, time=0-00:29:59)
[switchout.asean.th-en] Epoch 29.6684: train_loss/word=3.369975 (steps=13576, words/sec=8571.54, time=0-00:30:00)
[switchout.asean.th-en] Epoch 29.7185: train_loss/word=3.282152 (steps=13600, words/sec=8014.99, time=0-00:30:01)
[switchout.asean.th-en] Epoch 29.7703: train_loss/word=3.306005 (steps=13625, words/sec=7787.98, time=0-00:30:02)
[switchout.asean.th-en] Epoch 29.8206: train_loss/word=3.131143 (steps=13648, words/sec=8077.16, time=0-00:30:03)
[switchout.asean.th-en] Epoch 29.8714: train_loss/word=3.316109 (steps=13671, words/sec=8291.62, time=0-00:30:04)
[switchout.asean.th-en] Epoch 29.9227: train_loss/word=3.394782 (steps=13693, words/sec=9289.13, time=0-00:30:05)
[switchout.asean.th-en] Epoch 29.9731: train_loss/word=3.273459 (steps=13717, words/sec=8254.32, time=0-00:30:06)
[switchout.asean.th-en] Epoch 30.0000: train_loss/word=3.260658 (steps=13729, words/sec=8142.61, time=0-00:30:06)
> Checkpoint [switchout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.asean.th-en] Epoch 30.0000 dev BLEU4: 0.2780394066139608, 0.496393/0.333565/0.247732/0.190120 (BP = 0.935626, ratio=0.94, hyp_len=6793, ref_len=7245) (time=0-00:30:34)
[switchout.asean.th-en]              dev auxiliary GLEU: 0.288748
[switchout.asean.th-en]              dev auxiliary Loss: 4.503 (ref_len=7245)
             checkpoint took 0-00:00:27
  new learning rate: 0.25
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.en
Performing inference on ./data/test.th and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.asean.th-en         | BLEU4: 0.2806523314430044, 0.499339/0.336159/0.249527/0.191122 (BP = 0.938267, ratio=0.94, hyp_len=6811, ref_len=7245)
                              | GLEU: 0.291586
                              | WER: 63.11% ( C/S/I/D: 3338/2808/665/1099; hyp_len=6811, ref_len=7245 )
                              | CER: 52.21% ( C/S/I/D: 17290/6976/2763/6129; hyp_len=27029, ref_len=30395 )
                              | BLEU4: 0.3089603850120307, 0.521637/0.364515/0.275432/0.217865 (BP = 0.945325, ratio=0.95, hyp_len=6794, ref_len=7176)
                              | GLEU: 0.315881
                              | WER: 59.73% ( C/S/I/D: 3508/2668/618/1000; hyp_len=6794, ref_len=7176 )
                              | CER: 48.97% ( C/S/I/D: 18122/6606/2606/5680; hyp_len=27334, ref_len=30408 )
```

## Results

Baseline နဲ့ SwitchOut ရလဒ်တွေကို နှိုင်းယှဉ်ကြည့်ရင် အောက်ပါအတိုင်း တွေ့ရလိမ့်မယ်။  



## Reference

- [https://stackoverflow.com/questions/22903114/overcome-valueerror-for-empty-array](https://stackoverflow.com/questions/22903114/overcome-valueerror-for-empty-array)
- [https://unix.stackexchange.com/questions/612680/remove-lines-with-specific-line-number-specified-in-a-file](https://unix.stackexchange.com/questions/612680/remove-lines-with-specific-line-number-specified-in-a-file)


