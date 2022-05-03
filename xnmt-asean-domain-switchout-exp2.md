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

## Prepare Config Files

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

## Update config Files

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

## Training

### for en-th, word unit

### for th-en, word unit

