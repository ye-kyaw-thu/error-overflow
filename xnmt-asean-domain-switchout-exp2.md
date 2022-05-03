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


