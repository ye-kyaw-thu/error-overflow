# Exp with Medical Domain

## data preparation

original data က  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver$ wc data.*
  14592  200101 1003108 data.en
  14592  232999 3579344 data.my
  14592  186871 2489211 data.th
  43776  619971 7071663 total
```

### shuffling

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver$ mkdir prepare
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver$ cd prepare/
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ paste ../data.en ../data.my ../data-seg.th  > ./data.all
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head -3 data.all
Hello	မင်္ဂလာပါ ။	สวัสดี
Are you Mr.Tun Tun ?	ခင်ဗျား က မစ္စတာ ထွန်းထွန်း ဖြစ် ပါ သလား ။	คุณ คือ นาย ตุน   ตุ น?
Nice to meet you .	ခင်ဗျား ကို တွေ့ ရတာ ဝမ်းသာ ပါ တယ် ။	ยิน ดี ที่ ได้ พบ คุ ณ.
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ tail -3 data.all
Is there anything else you would like to ask me ? Thank you very much .	ခင်ဗျား ကျွန်တော့် ကို မေးချင်တာ တစ်ခုခု ရှိသေး လား ။ ကျေးဇူး အများကြီး တင် ပါ တယ် ။	มีอะไร จะ ถาม ฉัน อีก ไหม   ขอบคุณ มา ก.
Mrs. Monas is a 30-year-old lady who is 36 weeks pregnant and has eclampsia .	မစ္စစ် မိုနပ်စ် က အသက် ၃၀ အရွယ် အမျိုးသမီး တစ်ဦး ဖြစ် ပြီး ကိုယ်ဝန် ၃၆ ပတ် ရ နေ ပြီးတော့ ကိုယ်ဝန်ဆောင်များ ကိုယ်ဝန် အဆိပ် ကြောင့် တက် တဲ့ ရောဂါ ရှိ နေ ပါ တယ် ။	นา งโ มนัส เป็น สตรี อายุ  30   ปี ที่ ตั้งครรภ์ ได้  36   สัปดาห์ และ มี ภาวะ ครรภ์ เป็นพิษ
She has been admitted for delivery .	သူ မွေးဖွား ဖို့ကို ဆေးရုံ တင်လိုက် ပါ ပြီ ။	เธอ ได้รับ การตอบรับ ให้ คลอด แล้ว
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

shuffle လုပ်ပြီးတော့ head, tail နဲ့ ပြန်ရိုက်ထုတ်ပြီး ဘာသာပြန်ထားတာတွေက ကိုက်နေသေးရဲ့လားဆိုတာကို အကြမ်းစစ်ကြည့်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ shuf ./data.all > ./data.shuf.all
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head ./data.shuf.all 
As you know that we checked your blood sugar levels .	ခင်ဗျား ရဲ့ သွေးတွင်း သကြားဓာတ် ပမာဏ ကို ကျွန်တော် တို့ စစ်ဆေးပြီး တာကို ခင်ဗျား သိမှာ ပါ ။อย่าง ที่ คุณ ทราบ   เรา ตรวจสอบ ระดับ น้ำตาล ใน เลือด ของคุณ
The vas deferens ( sperm tubes ) can be seen quite easily under the cut skin .	ခွဲစိတ် ထား သော အရေပြား အောက် တွင် သုတ်ပိုး ပြွန် ကို တွေ့နိုင် ပါ တယ် ။	vas   deferens  ( หลอ ดสเปิร์ ม)   สามารถ มอง เห็น ได้ ค่อนข้าง ง่าย ภาย ใต้ ผิวหนัง ที่ ถูก ตัด
Today ’ s X-ray showed an ankle fracture .	ဒီနေ့ ဓာတ်မှန်ကတော့ ခြေကျင်းဝတ် အရိုးကျိုး တယ် လို့ ပြ ခဲ့ တယ် ။	วันนี้  X- ray   พบ ข้อเท้า หัก
I knew it . How to help indian girls have orgasm ?	ကျွန်တော် သိနှင့် နေ တယ် ။ အိန္ဒိယ မိန်းကလေး တွေကို လိင်ဆန္ဒ ပြီးမြောက် အောင် ဘယ်လို ကူညီပေး ရလဲ ။ฉัน รู้ แล้ว   วิธี ช่วย สาว อินเดีย ถึง จุด สุด ยอ ด?
Reassure her and tell her to confide in people whom she trusts and seek help from her family and social services .	သူမ ကို စိတ် သက်သာအောင် လုပ်ပြီး သူမ ရဲ့ မိသားစု နဲ့ လူမှုဝန်ဆောင် မှု တွေ ဆီ က အကူအညီ ယူရန် နဲ့ သူမ ယုံကြည် တဲ့ လူတွေ ကို ရင်ဖွင့် ပြော ပါ ။	สร้าง ความมั่นใจ และ บอก ให้ เธอ วางใจ กับ คน ที่ เธอ ไว้ วางใจ และ ขอ ความช่วยเหลือ จาก ครอบครัว และ บริการ ทางสังคม ของเธอ
Do you have fever ?	ခင်ဗျား မှာ အဖျား ရှိ လား ။	คุณ มี ไข ้หรื อไม ่?
After the operation you will be taken to the recovery room , where you will continue recovering from the general anaesthesia .ခွဲစိတ်မှု ပြီးနောက် ခင်ဗျား ကို နားနေဆောင် သို့ ခေါ်ဆောင် သွား ပါ မယ် ၊ ခင်ဗျား မေ့ဆေး မှ ပြန်လည် သက်သာ လာ ရင် ခင်ဗျား ကို လူနာဆောင် သို့ ခေါ်သွား ပါ လိမ့် မယ် ။	หลังจาก การผ่าตัด   คุณ จะ ถูก นำ ตัว ไป ที่ ห้อง พักฟื้น   ซึ่ง คุณ จะ ได้ พักฟื้น จาก การดม ยาสลบ ต่อไป
Is there still pain here ?	ဒီ မှာ နာ သေး လား ။	ยัง เจ็บ อยู่ ไหม นี ่?
No , doctor , I am fine , just tell me .	မဟုတ်ဘူး ၊ ဒေါက်တာ ။ ကျွန်မ အဆင်ပြေ ပါ တယ် ၊ ကျွန်မ ကို ပြော ပါ ။	ไม่ เป็น ไร   หมอ   ฉัน สบาย ดี   บอก ฉัน ที
You can read it and if you come up with any questions , please let us know .	ခင်ဗျား ဒါ ကို ဖတ် ပြီး မေးခွန်း ရှိ ရင် ကျေးဇူးပြုပြီး ကျွန်တော် တို့ သိ ပါ ရ စေ ။	คุณ สามารถ อ่าน และ หาก คุณ มี คำถาม ใด  ๆ   โปรด แจ้ง ให้ เรา ทราบ
```

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ tail ./data.shuf.all
Do you sometimes feel the need to cut down on your drinking ?	တစ်ခါတစ်ရံ မှာ အရက် သောက် တာ ကို ဖြတ် ဖို့ လို တယ် လို့ ခင်ဗျား ခံစား ရ လား ။	บางครั้ง คุณ รู้สึก ว่า จำเป็น ต้อง ลด การดื่ม ของ คุ ณหรื อไม ่?
You are Mr. Johnson , a 55-year-old who has been scheduled to undergo a TURP procedure .	ခင်ဗျား က မစ်စတာ ဂျွန်ဆင် ၊ အသက် ၅၅ နှစ် ဖြစ်ပြီး တီယူအာပီ လုပ်ဆောင် မှု ကို ပြုလုပ် ရန် စီစဉ်ထား သူ ဖြစ် ပါ တယ် ။	คุณ คือ คุณ จอห์น สัน   อายุ  55   ปี   ที่ ต้อง เข้า รับ การผ่าตัด   TURP
Gastroenteritis : any diarrhoea or vomiting ?	အစာအိမ် အူလမ်းကြောင်း ရောင် ခြင်း - ဝမ်းလျှော ခြင်း ၊ ပျို့အန် ခြင်း ရှိ လား ။	กระเพาะ และ ลำไส้ อัก เส บ:   ท้อง เสีย หรือ อา เจีย นหรื อไม ่?
Ah , I know this one . You can &apos;t .	အာ ၊ ကျွန်တော် ဒါကို သိ ပါ တယ် ။ ခင်ဗျား အဲဒါ ကို မလုပ် နိုင် ပါ ဘူး ။	อา   ฉัน รู้ อัน นี้   คุณ ไม่สามารถ
Pneumonia ( cough , fever , sputum )	အဆုတ်ရောင် ရောဂါ ( ချောင်းဆိုး ခြင်း ၊ ဖျား ခြင်း ၊ ချွဲကျပ် ခြင်း ) ။	โรค ปอดบวม  (ไ อ,   มี ไข ้,   เส มห ะ)
If it lies below the line , then no treatment is required .	မျဉ်းကြောင်းအောက် ရောက် နေ ပါက ၊ ကုသ ရန် မ လိုအပ် ပါ ။	ถ้า มัน อยู่ ใต้ เส้น   ก็ ไม่ ต้อง รักษา
Hopefully your children will not get it .	 ခင်ဗျား ရဲ့ ကလေး တွေ ကို မ ကူးစက် ဘူး လို့ မျှော်လင့် တယ် ။	หวัง ว่า ลูก  ๆ   ของคุณ จะ ไม่ ได้รับ มัน
Operations for weight loss are not without complications and are reserved for people who are extremely obese and they have tried to lose weight using diet and exercises without success .	ကိုယ် အလေးချိန် ကျ ဖို့ ခွဲစိတ် မှု တွေ က နောက်ဆက်တွဲ ရောဂါ တွေ မ ရှိ ဘဲ မ နေ ဘူး ပြီးတော့ အလွန်အမင်း အဝလွန် နေ တဲ့ သူတွေ အတွက် အရန်ထား ထား တာ ဖြစ် တယ် ပြီးတော့ သူ တို့ က မျှတ တဲ့ အစားအစာ နဲ့ လေ့ကျင့်ခန်း တွေ သုံး ပြီး ကိုယ် အလေးချိန် ကျ ဖို့ ကြိုးစား ပြီး မအောင်မြင် တဲ့ လူ တွေ ဖြစ် တယ် ။	การผ่าตัด ลดน้ำหนัก ไม่ได้ ไม่มี ภาวะ แทรก ซ้อน   และ สงวนไว้ สำหรับ ผู้ ที่ อ้วน มาก   และ พยายาม ลดน้ำหนัก โดย ใช้ อาหาร และ ออกกำลังกาย แต่ ไม่ ประสบผลสำเร็จ
I understand your child has swallowed a coin .	ခင်ဗျား ကလေး အကြွေစေ့ မျို ချ ခဲ့ တာ ကို ကျွန်တော် နားလည် တယ် ။	ฉัน เข้าใจ ว่า ลูก ของคุณ กลืน เหรียญ
HYPERTENSION : This is a condition in which your blood pressure is constantly high .	သွေးအားနည်း ခြင်း - ဒါ က တော့ ခင်ဗျား ရဲ့ သွေးဖိအား က ဆက်တိုက် မြင့်တက် နေ တဲ့ အခြေအနေ တစ်ခု ဖြစ် တယ် ။	ความ ดัน โลหิต สู ง:   นี่ เป็น ภาวะ ที่ ความ ดัน โลหิต ของคุณ สูง อย่างต่อเนื่อง
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

file format ကိုလည်း စစ်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ file ./data.shuf.all 
./data.shuf.all: Unicode text, UTF-8 text, with very long lines (844)
```

### Splitting train/dev/test

training data, dev data, test data ခွဲခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head -n 13592 ./data.shuf.all > train.all
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ tail -n 500 ./data.shuf.all > test.all
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ tail -n 1000 ./data.shuf.all | head -n 500 > ./dev.all
```

file size ကို ပြန် confirm လုပ်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ wc {train,dev,test}.all
  13592  578212 6593535 train.all
    500   20614  235230 dev.all
    500   21404  243157 test.all
  14592  620230 7071922 total
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

အင်္ဂလိပ်စာ ဒေတာကို ပြင်ဆင်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f1 ./train.all > train.en
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f1 ./dev.all > dev.en
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f1 ./test.all > test.en
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head -n 1 {train,dev,test}.en
==> train.en <==
As you know that we checked your blood sugar levels .

==> dev.en <==
I plan to insert a chest drain with the help of the seniors .

==> test.en <==
The patient is not happy and she has complained to you .
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

မြန်မာစာဒေတာကို ပြင်ဆင်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f2 ./train.all > train.my
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f2 ./dev.all > dev.my
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f2 ./test.all > test.my
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head -n 1 {train,dev,test}.my
==> train.my <==
ခင်ဗျား ရဲ့ သွေးတွင်း သကြားဓာတ် ပမာဏ ကို ကျွန်တော် တို့ စစ်ဆေးပြီး တာကို ခင်ဗျား သိမှာ ပါ ။

==> dev.my <==
စီနီယာ တွေ ရဲ့ အကူအညီ နဲ့ ရင်ဘတ် ကို အပေါက်ဖောက် ပြီး ပိုက် ထည့် ဖို့ စီစဉ် ထား ပါ တယ် ။

==> test.my <==
လူနာ က မကျေနပ် ဘူး ပြီးတော့ သူမ က ခင်ဗျား ကို တိုင်ပါတယ်။
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

ထိုင်း ဒေတာကို ပြင်ဆင်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f3 ./train.all > train.th
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f3 ./dev.all > dev.th
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cut -f3 ./test.all > test.th
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ head -n 1 {train,dev,test}.th
==> train.th <==
อย่าง ที่ คุณ ทราบ   เรา ตรวจสอบ ระดับ น้ำตาล ใน เลือด ของคุณ

==> dev.th <==
ฉัน วางแผน ที่จะ ใส่ ท่อระบายน้ำ หน้าอก ด้วย ความช่วยเหลือ ของ ผู้อาวุโส

==> test.th <==
ผู้ป่วย ไม่ พอใจ และ เธอ บ่น กับ คุณ
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

file size တွေကို ပြန် confirm လုပ်ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ wc {train,dev,test}.{en,my,th}
  13592  186515  935132 train.en
  13592  217238 3337665 train.my
  13592  174448 2320541 train.th
    500    6658   33466 dev.en
    500    7744  118989 dev.my
    500    6212   82775 dev.th
    500    6928   34510 test.en
    500    8017  122689 test.my
    500    6459   85958 test.th
  43776  620219 7071725 total
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

အထက်ပါ အင်္ဂလိပ်စာနဲ့ မြန်မာစာ ဒေတာက manual word segmentation ပါ။ ဘာသာပြန်စဉ်က လူက ဖြတ်ထားခဲ့တဲ့ စာလုံးတွေအတိုင်းပါပဲ။  
ထိုင်းစာက လောလောဆယ် ဘာသာပြန်နေဆဲမို့ GoogleTranslate ကိုပဲ ယူသုံးထားပါတယ်။ ပြီးတော့ ထိုင်း word segmenter ကို သုံးထားပါတယ်။  

## Copy Word Data to Experiment Path

အထက်ပါ ပြင်ခဲ့တဲ့ ဒေတာတွေကို experiment လုပ်မယ့် folder နဲ့ နီးတဲ့ဘက်ကို copy ကူးပြီးရွှေ့ခဲ့...  

```
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ cp *.{en,my,th} /home/ye/tool/xnmt/exp/medical1/word/data/
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$ ls /home/ye/tool/xnmt/exp/medical1/word/data
dev.en  dev.my  dev.th  test.en  test.my  test.th  train.en  train.my  train.th
(base) ye@ye-System-Product-Name:~/data/medical/corpus_checking_final_ver/prepare$
```

## config file preparation (word, en-my)

အရင်ဆုံး ဖိုလ်ဒါ အသစ်ဆောက် ပြီး kftt recipe ရဲ့ config ဖိုင်ကိုပဲ ကော်ပီကူးယူခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ cp ../../recipes/kftt/config.kftt.en-ja.yaml .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

ဖိုင်နာမည်ကို အောက်ပါအတိုင်း ပေးခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ mv config.kftt.en-ja.yaml config.medical.en-my-word.yaml
```

အောက်ပါအချက်တွေကို update လုပ်ခဲ့...  


updated config ဖိုင်က အောက်ပါအတိုင်း...  

```yaml
# standard settings
medical.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
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
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
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

## training (word, en-my)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ time xnmt --backend torch --gpu ./config.medical.en-my-word.yaml 
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-01 20:08:21
=> Running medical.en-my
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 22454378
> Training
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
[medical.en-my] Epoch 0.0756: train_loss/word=8.308530 (steps=19, words/sec=8054.45, time=0-00:00:05)
[medical.en-my] Epoch 0.1495: train_loss/word=7.248179 (steps=42, words/sec=9667.54, time=0-00:00:07)
[medical.en-my] Epoch 0.2253: train_loss/word=7.156715 (steps=62, words/sec=11728.33, time=0-00:00:08)
[medical.en-my] Epoch 0.3016: train_loss/word=6.972519 (steps=82, words/sec=11321.24, time=0-00:00:10)
[medical.en-my] Epoch 0.3771: train_loss/word=6.930852 (steps=105, words/sec=10411.19, time=0-00:00:12)
...
...
...
[medical.en-my] Epoch 22.1580: train_loss/word=2.095366 (steps=6375, words/sec=10159.91, time=0-00:22:21)
[medical.en-my] Epoch 22.2345: train_loss/word=2.097726 (steps=6397, words/sec=10376.35, time=0-00:22:23)
[medical.en-my] Epoch 22.3081: train_loss/word=2.082870 (steps=6419, words/sec=10836.96, time=0-00:22:24)
[medical.en-my] Epoch 22.3829: train_loss/word=2.107120 (steps=6440, words/sec=9968.44, time=0-00:22:26)
[medical.en-my] Epoch 22.4591: train_loss/word=2.109191 (steps=6462, words/sec=10411.41, time=0-00:22:28)
[medical.en-my] Epoch 22.5354: train_loss/word=2.106494 (steps=6484, words/sec=10633.67, time=0-00:22:30)
[medical.en-my] Epoch 22.6111: train_loss/word=2.082040 (steps=6505, words/sec=10450.13, time=0-00:22:31)
[medical.en-my] Epoch 22.6871: train_loss/word=2.136538 (steps=6530, words/sec=9484.46, time=0-00:22:34)
[medical.en-my] Epoch 22.7663: train_loss/word=2.117738 (steps=6552, words/sec=10104.65, time=0-00:22:35)
[medical.en-my] Epoch 22.8455: train_loss/word=2.140536 (steps=6573, words/sec=10766.29, time=0-00:22:37)
[medical.en-my] Epoch 22.9206: train_loss/word=2.152174 (steps=6596, words/sec=10557.51, time=0-00:22:39)
[medical.en-my] Epoch 22.9971: train_loss/word=2.105358 (steps=6616, words/sec=11486.60, time=0-00:22:41)
[medical.en-my] Epoch 23.0000: train_loss/word=2.039247 (steps=6617, words/sec=6039.86, time=0-00:22:41)
> Checkpoint [medical.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.en-my] Epoch 23.0000 dev BLEU4: 0.1654160488338149, 0.484379/0.230994/0.113738/0.060763 (BP = 0.991962, ratio=0.99, hyp_len=7682, ref_len=7744) (time=0-00:23:10)
[medical.en-my]              dev auxiliary GLEU: 0.212490
[medical.en-my]              dev auxiliary Loss: 4.961 (ref_len=7744)
             checkpoint took 0-00:00:28
  best dev score, writing out model
[medical.en-my] Epoch 23.0048: train_loss/word=1.879858 (steps=6618, words/sec=12665.02, time=0-00:23:16)
[medical.en-my] Epoch 23.0796: train_loss/word=2.048255 (steps=6640, words/sec=10917.83, time=0-00:23:18)
[medical.en-my] Epoch 23.1572: train_loss/word=2.036476 (steps=6661, words/sec=11402.94, time=0-00:23:19)
[medical.en-my] Epoch 23.2330: train_loss/word=2.055041 (steps=6682, words/sec=10552.75, time=0-00:23:21)
[medical.en-my] Epoch 23.3088: train_loss/word=2.087028 (steps=6706, words/sec=10045.82, time=0-00:23:23)
[medical.en-my] Epoch 23.3843: train_loss/word=2.084240 (steps=6728, words/sec=9480.43, time=0-00:23:25)
[medical.en-my] Epoch 23.4592: train_loss/word=2.053002 (steps=6749, words/sec=11395.85, time=0-00:23:27)
[medical.en-my] Epoch 23.5347: train_loss/word=2.089701 (steps=6771, words/sec=9927.01, time=0-00:23:29)
[medical.en-my] Epoch 23.6105: train_loss/word=2.071363 (steps=6794, words/sec=10838.63, time=0-00:23:31)
[medical.en-my] Epoch 23.6842: train_loss/word=2.085453 (steps=6814, words/sec=11016.97, time=0-00:23:32)
[medical.en-my] Epoch 23.7593: train_loss/word=2.028352 (steps=6832, words/sec=10384.23, time=0-00:23:34)
[medical.en-my] Epoch 23.8334: train_loss/word=2.135896 (steps=6856, words/sec=9032.56, time=0-00:23:36)
[medical.en-my] Epoch 23.9083: train_loss/word=2.112552 (steps=6879, words/sec=10213.01, time=0-00:23:38)
[medical.en-my] Epoch 23.9838: train_loss/word=2.085825 (steps=6901, words/sec=9921.69, time=0-00:23:39)
[medical.en-my] Epoch 24.0000: train_loss/word=1.986090 (steps=6905, words/sec=11278.84, time=0-00:23:40)
> Checkpoint [medical.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.en-my] Epoch 24.0000 dev BLEU4: 0.16276316199456278, 0.480612/0.227430/0.111575/0.058540 (BP = 0.995730, ratio=1.00, hyp_len=7711, ref_len=7744) (time=0-00:24:09)
[medical.en-my]              dev auxiliary GLEU: 0.209674
[medical.en-my]              dev auxiliary Loss: 4.982 (ref_len=7744)
             checkpoint took 0-00:00:29
  new learning rate: 0.25
[medical.en-my] Epoch 24.0024: train_loss/word=2.066955 (steps=6906, words/sec=8440.61, time=0-00:24:09)
[medical.en-my] Epoch 24.0782: train_loss/word=2.039585 (steps=6930, words/sec=9589.89, time=0-00:24:12)
[medical.en-my] Epoch 24.1538: train_loss/word=2.033877 (steps=6953, words/sec=9958.25, time=0-00:24:13)
[medical.en-my] Epoch 24.2283: train_loss/word=1.984496 (steps=6974, words/sec=10925.91, time=0-00:24:15)
[medical.en-my] Epoch 24.3021: train_loss/word=2.008411 (steps=6996, words/sec=9804.98, time=0-00:24:17)
[medical.en-my] Epoch 24.3788: train_loss/word=1.978109 (steps=7016, words/sec=11262.46, time=0-00:24:19)
[medical.en-my] Epoch 24.4564: train_loss/word=1.974875 (steps=7036, words/sec=11889.51, time=0-00:24:20)
[medical.en-my] Epoch 24.5327: train_loss/word=1.998383 (steps=7055, words/sec=10874.14, time=0-00:24:22)
[medical.en-my] Epoch 24.6083: train_loss/word=1.994888 (steps=7078, words/sec=10305.02, time=0-00:24:23)
[medical.en-my] Epoch 24.6829: train_loss/word=1.985619 (steps=7098, words/sec=10650.34, time=0-00:24:25)
[medical.en-my] Epoch 24.7599: train_loss/word=2.044122 (steps=7120, words/sec=9985.26, time=0-00:24:27)
[medical.en-my] Epoch 24.8337: train_loss/word=2.005496 (steps=7141, words/sec=11223.45, time=0-00:24:29)
[medical.en-my] Epoch 24.9081: train_loss/word=2.047698 (steps=7165, words/sec=8835.48, time=0-00:24:31)
[medical.en-my] Epoch 24.9834: train_loss/word=2.050738 (steps=7188, words/sec=10328.98, time=0-00:24:33)
[medical.en-my] Epoch 25.0000: train_loss/word=1.993698 (steps=7193, words/sec=11161.07, time=0-00:24:33)
> Checkpoint [medical.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.en-my] Epoch 25.0000 dev BLEU4: 0.16508281183319762, 0.487811/0.233116/0.116031/0.062448 (BP = 0.974367, ratio=0.97, hyp_len=7548, ref_len=7744) (time=0-00:25:02)
[medical.en-my]              dev auxiliary GLEU: 0.213272
[medical.en-my]              dev auxiliary Loss: 4.972 (ref_len=7744)
             checkpoint took 0-00:00:29
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.en-my                 | BLEU4: 0.1654160488338149, 0.484379/0.230994/0.113738/0.060763 (BP = 0.991962, ratio=0.99, hyp_len=7682, ref_len=7744)
                              | GLEU: 0.212490
                              | WER: 71.44% ( C/S/I/D: 3194/3506/982/1044; hyp_len=7682, ref_len=7744 )
                              | CER: 58.03% ( C/S/I/D: 19664/10508/4077/6968; hyp_len=34249, ref_len=37140 )
                              | BLEU4: 0.17699824231899827, 0.486881/0.240633/0.121469/0.068966 (BP = 1.000000, ratio=1.01, hyp_len=8080, ref_len=8017)
                              | GLEU: 0.220710
                              | WER: 71.00% ( C/S/I/D: 3394/3617/1069/1006; hyp_len=8080, ref_len=8017 )
                              | CER: 58.23% ( C/S/I/D: 20641/11172/4651/6467; hyp_len=36464, ref_len=38280 )

real	26m20.354s
user	26m11.305s
sys	0m10.275s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

## Check Folders and Results for en-my

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ tree models/
models/
├── medical.en-my.mod
└── medical.en-my.mod.data
    ├── AuxNonLinear-1c337c1e
    ├── DenseWordEmbedder-d9c7571c
    ├── Linear-d60ef28d
    ├── MlpAttender-fb62be0f
    ├── SimpleWordEmbedder-fde647e7
    ├── UniLSTMSeqTransducer-40ad363e
    ├── UniLSTMSeqTransducer-9d3f78e1
    ├── UniLSTMSeqTransducer-c362637e
    ├── UniLSTMSeqTransducer-cd34fbea
    └── UniLSTMSeqTransducer-fbe4bf5d

1 directory, 11 files
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ tree hyp/
hyp/
├── medical.en-my.dev.my
└── medical.en-my.test.my

0 directories, 2 files
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ head ./data/test.en
The patient is not happy and she has complained to you .
You have problems with coordination on your right side .
Do you use recreational drugs ?
The procedure has advantages over traditional open surgery .
Hmm . How come some kids dont brush thier teeth and still don &apos;t have cavities ?
What does a priapism indicate ?
Well , gym .
Alright . Why might my eyes be watering so much ?
If you have some free time , you can hang out with me and my friends , we are planning to go to the cinema .
I &apos;m not sure , but urine infection , uti , kidney infection , std , this is just a few things go to the dr ! .
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ head ./hyp/medical.en-my.test.my 
လူနာ က မကျေနပ် ပါ ဘူး ပြီးတော့ သူမ က ခင်ဗျား ကို တိုင်တန်း ခဲ့ တယ် ။
ခင်ဗျား ရဲ့ ညာဘက် အလုပ် မှာ ဒီလို ပြဿနာတွေ ရှိ နေ တယ် ။
ခင်ဗျား စိတ်ဖြေဆေး တွေ ကို သုံး ပါ သလား ။
ဒီ ခွဲစိတ်ကုထုံး ကို ခွဲစိတ် ရန် ဒါမှမဟုတ် ခွဲစိတ် မှု မရှိ အောင် လုပ်ဆောင် နိုင် ပါ တယ် ။
ဟမ် ။ ကျန်းမာရေး မှာ ရုပ်ပိုင်း ဆိုင်ရာ ပြဿနာ တွေ က ဘာ တွေ မှာ ရှိ နေ ပေမဲ့ တခြား အရာ တွေ မ ရှိ မလဲ ။
ပီရီတွန် ကျဆင်း ခြင်း အတွက် ဘယ်လို လဲ ။
ကောင်းပြီ ၊ လေ့ကျင့်ခန်း လုပ် ပါ ။
ကောင်းပြီ ။ ကျွန်တော့် မျက်လုံး တွေ က ဘာကြောင့် အရမ်း အမွှေးထူ တာလဲ ။
ခင်ဗျား မှာ အချိန်ယူ နေရ ရင် ၊ ခင်ဗျား က ကျွန်တော့် သူငယ်ချင်း တွေ နဲ့ တွေ့ဖို့ ကျွန်တော် တို့ စစ်ဆေး မှု ပြု လုပ် နိုင် ပါ တယ် ၊ ကျွန်တော် တို့ က နမူနာ ကို သွား ဖို့ လိုအပ် တယ် ။
ကျွန်တော် သေချာ မပြော နိုင် ဘူး ၊ ဒါပေမဲ့ ဆီး လမ်းကြောင်း ပိုး ဝင် ခြင်း ၊ ကူးစက် သော ရောဂါ ပိုး တွေ က တစ်ယောက် နဲ့ တစ်ယောက် ပဲ ဖြစ် ပါ တယ် ။
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ tail ./data/test.en 
Do you sometimes feel the need to cut down on your drinking ?
You are Mr. Johnson , a 55-year-old who has been scheduled to undergo a TURP procedure .
Gastroenteritis : any diarrhoea or vomiting ?
Ah , I know this one . You can &apos;t .
Pneumonia ( cough , fever , sputum )
If it lies below the line , then no treatment is required .
Hopefully your children will not get it .
Operations for weight loss are not without complications and are reserved for people who are extremely obese and they have tried to lose weight using diet and exercises without success .
I understand your child has swallowed a coin .
HYPERTENSION : This is a condition in which your blood pressure is constantly high .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ tail ./hyp/medical.en-my.test.my 
တစ်ခါတလေ ခင်ဗျား အရက်သောက် နေတာ ကို ဖြတ် ဖို့ လိုတယ် လို့ ခင်ဗျား ခံစားမိ ပါ သလား ။
ခင်ဗျား က ၅၅ နှစ် အရွယ် ရှိ တဲ့ မစ္စတာ ဂျွန်ဆင် ဖြစ် ပြီး တီယူအာပီ လုပ်ဆောင် မှု ကို ပြုလုပ် ဖို့ စီစဉ်ထား ပါ တယ် ။
အစာအိမ် အူလမ်းကြောင်း ရောင် ခြင်း - ဝမ်းလျှော ခြင်း ဒါမှမဟုတ် ပျို့အန် ခြင်း ရှိ လား ။
အား ၊ ကျွန်တော် ဒါကို သိ တယ် ။ ခင်ဗျား မလုပ်နိုင် ဘူး ။
အဆုတ်ရောင် ရောဂါ ( ချောင်းဆိုး ခြင်း ၊ အဖျား ၊ ချွဲ )
၎င်း က သေးငယ် တဲ့ ကျူအာအက်စ် ကွန်ပလက် ဖြစ် ရင် ၊ အဲဒီနောက် ကုသ မှု ခံယူ ရန် မလိုအပ် ပါ ။
ခင်ဗျား ရဲ့ ကလေး တွေ မှာ မ ဖြစ် မှာ မဟုတ် ဘူး လို့ မျှော်လင့် ပါ တယ် ။
ကိုယ်အလေးချိန် အကူအညီ တွေ မရှိ ဘဲ အလေးချိန် ကျ ခြင်း က လူ တွေ က ကြာကြာ ကောင်း တယ် ပြီးတော့ သူ တို့ က ကိုယ်အလေးချိန် ကျ ဖို့ ကြိုးစား ဖို့ ကြိုးစား ကြ တယ် ပြီးတော့ သူ တို့ က ကိုယ်အလေးချိန် အစားထိုး ဖို့ ကြိုးစား ဖို့ ကြိုးစား နေ ကြ တယ် ။
ခင်ဗျား ကလေး က အကြွေစေ့ ကို မျိုချ ခဲ့ တယ် လို့ ကျွန်တော် သိထား တယ် ။
အိပ်ငိုက် ခြင်း - ဒါ က ခင်ဗျား ရဲ့ သွေးပမာဏ လျော့နည်း နေ တဲ့ အခြေအနေ တစ်ခု ဖြစ် တယ် ။
```

## Preparing config (word, my-en)

```yaml
# standard settings
medical.my-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.my'
      - '{EXP_DIR}/data/train.en'
      out_files:
      - '{EXP_DIR}/vocab.my'
      - '{EXP_DIR}/vocab.en'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
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
    src_file: '{EXP_DIR}/data/train.my'
    trg_file: '{EXP_DIR}/data/train.en'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.my'
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
      src_file: &test_src '{EXP_DIR}/data/test.my'
      ref_file: &test_trg '{EXP_DIR}/data/test.en'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.en'
```

## Training (word, my-en)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ time xnmt --backend torch --gpu ./config.medical.my-en-word.yaml 
...
...
...
[medical.my-en] Epoch 22.0013: train_loss/word=2.310877 (steps=5959, words/sec=3974.40, time=0-00:18:47)
[medical.my-en] Epoch 22.0752: train_loss/word=2.053983 (steps=5982, words/sec=10304.32, time=0-00:18:49)
[medical.my-en] Epoch 22.1493: train_loss/word=2.044981 (steps=6004, words/sec=10232.90, time=0-00:18:51)
[medical.my-en] Epoch 22.2248: train_loss/word=2.000528 (steps=6024, words/sec=11363.16, time=0-00:18:52)
[medical.my-en] Epoch 22.2991: train_loss/word=2.098441 (steps=6047, words/sec=9504.37, time=0-00:18:54)
[medical.my-en] Epoch 22.3746: train_loss/word=2.037682 (steps=6068, words/sec=11350.71, time=0-00:18:56)
[medical.my-en] Epoch 22.4487: train_loss/word=2.052730 (steps=6087, words/sec=11078.34, time=0-00:18:57)
[medical.my-en] Epoch 22.5237: train_loss/word=1.989413 (steps=6105, words/sec=11211.64, time=0-00:18:58)
[medical.my-en] Epoch 22.6007: train_loss/word=2.043678 (steps=6125, words/sec=11514.99, time=0-00:18:59)
[medical.my-en] Epoch 22.6743: train_loss/word=2.076515 (steps=6143, words/sec=11706.49, time=0-00:19:01)
[medical.my-en] Epoch 22.7507: train_loss/word=2.128261 (steps=6163, words/sec=10044.00, time=0-00:19:02)
[medical.my-en] Epoch 22.8245: train_loss/word=2.078870 (steps=6181, words/sec=10722.51, time=0-00:19:03)
[medical.my-en] Epoch 22.8991: train_loss/word=2.138306 (steps=6200, words/sec=10527.14, time=0-00:19:05)
[medical.my-en] Epoch 22.9745: train_loss/word=2.114491 (steps=6222, words/sec=10305.35, time=0-00:19:07)
[medical.my-en] Epoch 23.0000: train_loss/word=2.139771 (steps=6229, words/sec=10786.38, time=0-00:19:07)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 23.0000 dev BLEU4: 0.2169980569666539, 0.499298/0.253597/0.168454/0.121589 (BP = 0.961582, ratio=0.96, hyp_len=6407, ref_len=6658) (time=0-00:19:30)
[medical.my-en]              dev auxiliary GLEU: 0.244311
[medical.my-en]              dev auxiliary Loss: 4.689 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
[medical.my-en] Epoch 23.0041: train_loss/word=1.872687 (steps=6230, words/sec=12386.97, time=0-00:19:37)
[medical.my-en] Epoch 23.0837: train_loss/word=1.959264 (steps=6251, words/sec=10165.98, time=0-00:19:39)
[medical.my-en] Epoch 23.1577: train_loss/word=1.927998 (steps=6270, words/sec=11282.00, time=0-00:19:40)
[medical.my-en] Epoch 23.2320: train_loss/word=1.960704 (steps=6290, words/sec=10497.96, time=0-00:19:42)
[medical.my-en] Epoch 23.3075: train_loss/word=1.985891 (steps=6310, words/sec=11126.27, time=0-00:19:43)
[medical.my-en] Epoch 23.3839: train_loss/word=1.989181 (steps=6330, words/sec=10774.02, time=0-00:19:44)
[medical.my-en] Epoch 23.4612: train_loss/word=1.988882 (steps=6350, words/sec=10160.71, time=0-00:19:46)
[medical.my-en] Epoch 23.5352: train_loss/word=2.042182 (steps=6372, words/sec=9856.19, time=0-00:19:48)
[medical.my-en] Epoch 23.6135: train_loss/word=2.081523 (steps=6395, words/sec=9486.85, time=0-00:19:49)
[medical.my-en] Epoch 23.6894: train_loss/word=2.013661 (steps=6415, words/sec=11016.05, time=0-00:19:51)
[medical.my-en] Epoch 23.7653: train_loss/word=2.075714 (steps=6436, words/sec=10155.79, time=0-00:19:52)
[medical.my-en] Epoch 23.8421: train_loss/word=2.011913 (steps=6456, words/sec=11030.56, time=0-00:19:54)
[medical.my-en] Epoch 23.9219: train_loss/word=2.065805 (steps=6477, words/sec=9857.50, time=0-00:19:55)
[medical.my-en] Epoch 23.9954: train_loss/word=2.090919 (steps=6498, words/sec=9889.60, time=0-00:19:57)
[medical.my-en] Epoch 24.0000: train_loss/word=2.220699 (steps=6500, words/sec=7346.03, time=0-00:19:57)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 24.0000 dev BLEU4: 0.22510146958854743, 0.497478/0.258977/0.174391/0.122599 (BP = 0.982578, ratio=0.98, hyp_len=6543, ref_len=6658) (time=0-00:20:21)
[medical.my-en]              dev auxiliary GLEU: 0.251196
[medical.my-en]              dev auxiliary Loss: 4.713 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
[medical.my-en] Epoch 24.0035: train_loss/word=1.838008 (steps=6501, words/sec=11391.85, time=0-00:20:28)
[medical.my-en] Epoch 24.0806: train_loss/word=1.936026 (steps=6523, words/sec=8888.15, time=0-00:20:30)
[medical.my-en] Epoch 24.1597: train_loss/word=1.884284 (steps=6542, words/sec=12174.59, time=0-00:20:31)
[medical.my-en] Epoch 24.2340: train_loss/word=1.949056 (steps=6564, words/sec=10408.43, time=0-00:20:33)
[medical.my-en] Epoch 24.3096: train_loss/word=1.977282 (steps=6585, words/sec=9787.12, time=0-00:20:34)
[medical.my-en] Epoch 24.3858: train_loss/word=1.962542 (steps=6604, words/sec=11302.69, time=0-00:20:35)
[medical.my-en] Epoch 24.4662: train_loss/word=1.959690 (steps=6623, words/sec=11900.91, time=0-00:20:37)
[medical.my-en] Epoch 24.5402: train_loss/word=1.946185 (steps=6641, words/sec=11930.35, time=0-00:20:38)
[medical.my-en] Epoch 24.6181: train_loss/word=2.038783 (steps=6666, words/sec=9399.25, time=0-00:20:40)
[medical.my-en] Epoch 24.6928: train_loss/word=1.979639 (steps=6685, words/sec=11141.32, time=0-00:20:41)
[medical.my-en] Epoch 24.7700: train_loss/word=1.989715 (steps=6707, words/sec=10712.47, time=0-00:20:43)
[medical.my-en] Epoch 24.8451: train_loss/word=1.957184 (steps=6728, words/sec=11431.91, time=0-00:20:44)
[medical.my-en] Epoch 24.9193: train_loss/word=2.036628 (steps=6748, words/sec=9833.29, time=0-00:20:46)
[medical.my-en] Epoch 24.9931: train_loss/word=2.010197 (steps=6768, words/sec=10231.56, time=0-00:20:47)
[medical.my-en] Epoch 25.0000: train_loss/word=2.005641 (steps=6770, words/sec=10221.44, time=0-00:20:48)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 25.0000 dev BLEU4: 0.21815446282825027, 0.505843/0.258916/0.172698/0.123036 (BP = 0.949818, ratio=0.95, hyp_len=6332, ref_len=6658) (time=0-00:21:12)
[medical.my-en]              dev auxiliary GLEU: 0.247546
[medical.my-en]              dev auxiliary Loss: 4.728 (ref_len=6658)
             checkpoint took 0-00:00:23
[medical.my-en] Epoch 25.0033: train_loss/word=1.856336 (steps=6771, words/sec=9962.47, time=0-00:21:12)
[medical.my-en] Epoch 25.0811: train_loss/word=1.866136 (steps=6791, words/sec=10272.18, time=0-00:21:13)
[medical.my-en] Epoch 25.1560: train_loss/word=1.918509 (steps=6814, words/sec=9672.49, time=0-00:21:15)
[medical.my-en] Epoch 25.2311: train_loss/word=1.918185 (steps=6835, words/sec=9899.52, time=0-00:21:17)
[medical.my-en] Epoch 25.3084: train_loss/word=1.905576 (steps=6855, words/sec=10984.54, time=0-00:21:18)
[medical.my-en] Epoch 25.3846: train_loss/word=1.920882 (steps=6875, words/sec=10801.86, time=0-00:21:20)
[medical.my-en] Epoch 25.4582: train_loss/word=1.978196 (steps=6895, words/sec=8926.48, time=0-00:21:21)
[medical.my-en] Epoch 25.5333: train_loss/word=1.952992 (steps=6918, words/sec=9757.37, time=0-00:21:23)
[medical.my-en] Epoch 25.6093: train_loss/word=1.942111 (steps=6936, words/sec=9745.28, time=0-00:21:24)
[medical.my-en] Epoch 25.6853: train_loss/word=1.983538 (steps=6960, words/sec=9002.28, time=0-00:21:26)
[medical.my-en] Epoch 25.7621: train_loss/word=1.868893 (steps=6977, words/sec=11769.09, time=0-00:21:27)
[medical.my-en] Epoch 25.8376: train_loss/word=1.884302 (steps=6995, words/sec=11795.64, time=0-00:21:29)
[medical.my-en] Epoch 25.9133: train_loss/word=1.955285 (steps=7016, words/sec=9969.76, time=0-00:21:30)
[medical.my-en] Epoch 25.9882: train_loss/word=1.975953 (steps=7037, words/sec=9692.97, time=0-00:21:32)
[medical.my-en] Epoch 26.0000: train_loss/word=2.026834 (steps=7041, words/sec=9110.09, time=0-00:21:32)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 26.0000 dev BLEU4: 0.22208094875882312, 0.509955/0.265181/0.175618/0.122006 (BP = 0.957205, ratio=0.96, hyp_len=6379, ref_len=6658) (time=0-00:21:56)
[medical.my-en]              dev auxiliary GLEU: 0.251883
[medical.my-en]              dev auxiliary Loss: 4.731 (ref_len=6658)
             checkpoint took 0-00:00:23
  new learning rate: 0.5
[medical.my-en] Epoch 26.0025: train_loss/word=1.918487 (steps=7042, words/sec=10088.80, time=0-00:21:56)
[medical.my-en] Epoch 26.0764: train_loss/word=1.815540 (steps=7064, words/sec=9756.12, time=0-00:21:58)
[medical.my-en] Epoch 26.1520: train_loss/word=1.863050 (steps=7085, words/sec=9630.63, time=0-00:22:00)
[medical.my-en] Epoch 26.2276: train_loss/word=1.821635 (steps=7107, words/sec=10453.92, time=0-00:22:01)
[medical.my-en] Epoch 26.3019: train_loss/word=1.844054 (steps=7126, words/sec=11015.90, time=0-00:22:03)
[medical.my-en] Epoch 26.3824: train_loss/word=1.843067 (steps=7148, words/sec=9598.87, time=0-00:22:04)
[medical.my-en] Epoch 26.4585: train_loss/word=1.806884 (steps=7167, words/sec=11218.06, time=0-00:22:06)
[medical.my-en] Epoch 26.5338: train_loss/word=1.814521 (steps=7187, words/sec=11112.99, time=0-00:22:07)
[medical.my-en] Epoch 26.6109: train_loss/word=1.847881 (steps=7209, words/sec=10472.12, time=0-00:22:09)
[medical.my-en] Epoch 26.6846: train_loss/word=1.874677 (steps=7231, words/sec=10010.40, time=0-00:22:11)
[medical.my-en] Epoch 26.7593: train_loss/word=1.796629 (steps=7249, words/sec=11706.03, time=0-00:22:12)
[medical.my-en] Epoch 26.8338: train_loss/word=1.772523 (steps=7265, words/sec=12971.26, time=0-00:22:13)
[medical.my-en] Epoch 26.9091: train_loss/word=1.839712 (steps=7286, words/sec=9829.46, time=0-00:22:14)
[medical.my-en] Epoch 26.9843: train_loss/word=1.850824 (steps=7308, words/sec=10221.40, time=0-00:22:16)
[medical.my-en] Epoch 27.0000: train_loss/word=1.813846 (steps=7312, words/sec=11822.32, time=0-00:22:16)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 27.0000 dev BLEU4: 0.23062638144158745, 0.519685/0.275043/0.184383/0.130327 (BP = 0.952654, ratio=0.95, hyp_len=6350, ref_len=6658) (time=0-00:22:40)
[medical.my-en]              dev auxiliary GLEU: 0.259406
[medical.my-en]              dev auxiliary Loss: 4.678 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
[medical.my-en] Epoch 27.0078: train_loss/word=1.709737 (steps=7313, words/sec=20489.15, time=0-00:22:47)
[medical.my-en] Epoch 27.0820: train_loss/word=1.775199 (steps=7335, words/sec=10181.88, time=0-00:22:49)
[medical.my-en] Epoch 27.1561: train_loss/word=1.724345 (steps=7353, words/sec=11995.32, time=0-00:22:50)
[medical.my-en] Epoch 27.2346: train_loss/word=1.713322 (steps=7371, words/sec=13171.19, time=0-00:22:51)
[medical.my-en] Epoch 27.3083: train_loss/word=1.795290 (steps=7391, words/sec=9188.63, time=0-00:22:52)
[medical.my-en] Epoch 27.3833: train_loss/word=1.781081 (steps=7411, words/sec=8806.51, time=0-00:22:54)
[medical.my-en] Epoch 27.4612: train_loss/word=1.794350 (steps=7434, words/sec=9130.02, time=0-00:22:56)
[medical.my-en] Epoch 27.5351: train_loss/word=1.757980 (steps=7453, words/sec=10574.66, time=0-00:22:57)
[medical.my-en] Epoch 27.6104: train_loss/word=1.773122 (steps=7474, words/sec=9789.21, time=0-00:22:59)
[medical.my-en] Epoch 27.6842: train_loss/word=1.819699 (steps=7498, words/sec=9131.65, time=0-00:23:01)
[medical.my-en] Epoch 27.7590: train_loss/word=1.808365 (steps=7518, words/sec=9664.13, time=0-00:23:02)
[medical.my-en] Epoch 27.8342: train_loss/word=1.778370 (steps=7539, words/sec=10923.84, time=0-00:23:04)
[medical.my-en] Epoch 27.9094: train_loss/word=1.814300 (steps=7561, words/sec=9313.02, time=0-00:23:06)
[medical.my-en] Epoch 27.9871: train_loss/word=1.771493 (steps=7580, words/sec=10565.54, time=0-00:23:07)
[medical.my-en] Epoch 28.0000: train_loss/word=1.785003 (steps=7583, words/sec=9781.42, time=0-00:23:07)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 28.0000 dev BLEU4: 0.2314798253936729, 0.511430/0.270003/0.181304/0.128488 (BP = 0.971979, ratio=0.97, hyp_len=6474, ref_len=6658) (time=0-00:23:31)
[medical.my-en]              dev auxiliary GLEU: 0.257936
[medical.my-en]              dev auxiliary Loss: 4.698 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
[medical.my-en] Epoch 28.0020: train_loss/word=1.875994 (steps=7584, words/sec=6725.69, time=0-00:23:37)
[medical.my-en] Epoch 28.0774: train_loss/word=1.763878 (steps=7606, words/sec=9756.25, time=0-00:23:39)
[medical.my-en] Epoch 28.1513: train_loss/word=1.716351 (steps=7625, words/sec=11281.21, time=0-00:23:40)
[medical.my-en] Epoch 28.2290: train_loss/word=1.767261 (steps=7644, words/sec=10019.54, time=0-00:23:42)
[medical.my-en] Epoch 28.3055: train_loss/word=1.736814 (steps=7666, words/sec=10169.77, time=0-00:23:43)
[medical.my-en] Epoch 28.3847: train_loss/word=1.740645 (steps=7688, words/sec=10299.69, time=0-00:23:45)
[medical.my-en] Epoch 28.4629: train_loss/word=1.737522 (steps=7706, words/sec=11828.45, time=0-00:23:46)
[medical.my-en] Epoch 28.5386: train_loss/word=1.718186 (steps=7723, words/sec=11772.09, time=0-00:23:47)
[medical.my-en] Epoch 28.6143: train_loss/word=1.750896 (steps=7745, words/sec=11118.75, time=0-00:23:49)
[medical.my-en] Epoch 28.6897: train_loss/word=1.763715 (steps=7766, words/sec=10684.95, time=0-00:23:50)
[medical.my-en] Epoch 28.7637: train_loss/word=1.754847 (steps=7787, words/sec=10469.26, time=0-00:23:52)
[medical.my-en] Epoch 28.8393: train_loss/word=1.758896 (steps=7807, words/sec=11220.58, time=0-00:23:53)
[medical.my-en] Epoch 28.9135: train_loss/word=1.756181 (steps=7828, words/sec=10670.43, time=0-00:23:55)
[medical.my-en] Epoch 28.9878: train_loss/word=1.798540 (steps=7850, words/sec=9873.85, time=0-00:23:57)
[medical.my-en] Epoch 29.0000: train_loss/word=1.768854 (steps=7854, words/sec=10634.39, time=0-00:23:57)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 29.0000 dev BLEU4: 0.2289417867588579, 0.504644/0.263062/0.175615/0.124557 (BP = 0.986238, ratio=0.99, hyp_len=6567, ref_len=6658) (time=0-00:24:21)
[medical.my-en]              dev auxiliary GLEU: 0.255646
[medical.my-en]              dev auxiliary Loss: 4.693 (ref_len=6658)
             checkpoint took 0-00:00:23
  new learning rate: 0.25
[medical.my-en] Epoch 29.0032: train_loss/word=1.706153 (steps=7855, words/sec=11256.61, time=0-00:24:21)
[medical.my-en] Epoch 29.0792: train_loss/word=1.714396 (steps=7876, words/sec=10457.51, time=0-00:24:23)
[medical.my-en] Epoch 29.1566: train_loss/word=1.697903 (steps=7898, words/sec=10514.45, time=0-00:24:24)
[medical.my-en] Epoch 29.2302: train_loss/word=1.684303 (steps=7916, words/sec=11143.44, time=0-00:24:25)
[medical.my-en] Epoch 29.3071: train_loss/word=1.710583 (steps=7935, words/sec=10522.31, time=0-00:24:27)
[medical.my-en] Epoch 29.3814: train_loss/word=1.700165 (steps=7955, words/sec=10663.83, time=0-00:24:28)
[medical.my-en] Epoch 29.4589: train_loss/word=1.745893 (steps=7976, words/sec=9322.47, time=0-00:24:30)
[medical.my-en] Epoch 29.5335: train_loss/word=1.696469 (steps=7998, words/sec=10534.58, time=0-00:24:32)
[medical.my-en] Epoch 29.6093: train_loss/word=1.689514 (steps=8016, words/sec=10870.84, time=0-00:24:33)
[medical.my-en] Epoch 29.6837: train_loss/word=1.708627 (steps=8037, words/sec=9865.84, time=0-00:24:34)
[medical.my-en] Epoch 29.7621: train_loss/word=1.713516 (steps=8059, words/sec=10138.78, time=0-00:24:36)
[medical.my-en] Epoch 29.8405: train_loss/word=1.735793 (steps=8083, words/sec=9401.51, time=0-00:24:38)
[medical.my-en] Epoch 29.9141: train_loss/word=1.714032 (steps=8103, words/sec=9219.14, time=0-00:24:40)
[medical.my-en] Epoch 29.9923: train_loss/word=1.699536 (steps=8123, words/sec=10478.83, time=0-00:24:41)
[medical.my-en] Epoch 30.0000: train_loss/word=1.756190 (steps=8125, words/sec=9097.65, time=0-00:24:41)
> Checkpoint [medical.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.my-en] Epoch 30.0000 dev BLEU4: 0.23651943640021703, 0.513891/0.271322/0.184702/0.132669 (BP = 0.978290, ratio=0.98, hyp_len=6515, ref_len=6658) (time=0-00:25:06)
[medical.my-en]              dev auxiliary GLEU: 0.262422
[medical.my-en]              dev auxiliary Loss: 4.677 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.en
Performing inference on ./data/test.my and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.my-en                 | BLEU4: 0.23651943640021703, 0.513891/0.271322/0.184702/0.132669 (BP = 0.978290, ratio=0.98, hyp_len=6515, ref_len=6658)
                              | GLEU: 0.262422
                              | WER: 65.06% ( C/S/I/D: 2996/2849/670/813; hyp_len=6515, ref_len=6658 )
                              | CER: 59.09% ( C/S/I/D: 13643/8225/2686/4918; hyp_len=24554, ref_len=26786 )
                              | BLEU4: 0.22773123029482975, 0.506559/0.268524/0.178953/0.125983 (BP = 0.967735, ratio=0.97, hyp_len=6708, ref_len=6928)
                              | GLEU: 0.256017
                              | WER: 64.97% ( C/S/I/D: 3089/2957/662/882; hyp_len=6708, ref_len=6928 )
                              | CER: 59.00% ( C/S/I/D: 14100/8166/2809/5275; hyp_len=25075, ref_len=27541 )

real	26m18.618s
user	26m16.717s
sys	0m3.084s
```

## Preparing for Syllable Unit

အရင်ဆုံး manual word ဖြတ်ထားတဲ့ ဒေတာကို copy ကူးယူ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ mkdir syl
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ cd syl
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ mkdir data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ cp ../word/data/
dev.en    dev.my    dev.th    test.en   test.my   test.th   train.en  train.my  train.th  
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ cp ../word/data/*.{en,my,th} ./data/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ cd data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ ls
dev.en  dev.my  dev.th  test.en  test.my  test.th  train.en  train.my  train.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

sylbrea.pl ကို ကိုယ့်စက်ထဲကို Download လုပ်ယူ ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ wget https://raw.githubusercontent.com/ye-kyaw-thu/sylbreak/master/perl/sylbreak.pl
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-01 23:22:59--  https://raw.githubusercontent.com/ye-kyaw-thu/sylbreak/master/perl/sylbreak.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.108.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2189 (2.1K) [text/plain]
Saving to: ‘sylbreak.pl’

sylbreak.pl                     100%[=====================================================>]   2.14K  --.-KB/s    in 0s      

2022-05-01 23:23:00 (80.1 MB/s) - ‘sylbreak.pl’ saved [2189/2189]

(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

မြန်မာစာ ဒေတာကို syllable ဖြတ်ခဲ့ ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./sylbreak.pl -i ./train.my -s " " > ./train.my.syl
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./sylbreak.pl -i ./dev.my -s " " > ./dev.my.syl(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./sylbreak.pl -i ./test.my -s " " > ./test.my.syl
```

syllable ဖြတ်ထားတဲ ဖိုင်တွေမှာက space ပိုတာမျိုး ရှိတယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ head *.syl
==> dev.my.syl <==
 စီ နီ ယာ   တွေ   ရဲ့   အ ကူ အ ညီ   နဲ့   ရင် ဘတ်   ကို   အ ပေါက် ဖောက်   ပြီး   ပိုက်   ထ ည့်   ဖို့   စီ စဉ်   ထား   ပါ   တယ်   ။
 သာ မန်   ဆီး အိတ်   က   မ ထင် ရှား   ပါ   ဘူး   ။
 ခင် ဗျား   မိ သား စု   ထဲ မှာ   က လေး   တုန်း   က တည်း က   နှ လုံး   ရော ဂါ သည်   ဒါ မှ မ ဟုတ်   နှ လုံး ခုန် သံ   မူ မ မှန်   ဖြစ် ဖူး   တဲ့   သူ   တစ် ယောက် ယောက်   ရှိ   လား   ။
 ခင် ဗျား   အောင် မြင်   စွာ   ဆေး ဖြတ်   နိုင်   မှာ   ကျွန် တော်   သိ ပါ   တယ်   ၊   ဒါ ပေ မဲ့   ပြ ဿ နာ   ဆို တာ   အ ချိန် တိုင်း   ရှိ စ မြဲ   မို့   ဒီ ဆေး   တွေ   ကို   စီ မံ ဖို့   ကျွန် တော်   တို့   ထိုး ဆေး   ကို   အ သုံး ပြု ရ မယ်   ၊   အဲ ဒါ ကို တော့   ဆေး ထိုး အပ်   လဲ လှယ် တဲ့   ပ ရို ဂ ရမ်   လို့   ကျွန် တော်   တို့   ခေါ် ပါ   တယ်   ။
 ခု   က   ဘာ   နှစ်   လဲ   ။
 ဟမ်   ။   မေး ခွန်း ကောင်း ပဲ   ။   ဆေး လိပ် သောက်   တာ   ကြော င့်   ဖြစ် မယ်   လို့   ကျွန် တော်   ထင်   ပါ   တယ်   ။
 ကျေး ဇူး ပြု ပြီး   ခင် ဗျား   ရဲ့   ဘယ် ဘက်   ဒါ မှ မ ဟုတ်   ညာ ဘက်   သို့   စောင်း ပြီး   လှဲ ပေး   နိုင်   မ လား   ။
 အဲ ဒါ   အ ဓိပ္ပာယ်   မ ရှိ   ဘူး   ။   ခင် ဗျား   ဘာ လို့   ဆန် ထ ရမ်   ကို   သောက် တာ   လဲ   ။
 ပုံ မှန် အား ဖြ င့်   သ င့် တော်   တဲ့   ကြို တင်   ကာ ကွယ်   မှု   တွေ   လုပ်   ပြီး   မှ သာ   ကျွန် တော်   ဒီ အ ခန်း   ထဲ ကို   ဝင် လာ   မှာ   ဖြစ်   တယ်   ။
 ဟမ်   ။   မေး ခွန်း ကောင်း   ပဲ   ။   အဲ ဒါ   အိတ် စီ ဒ ရင်း   မိုင် ဂ ရိန်း   လို့   ကျွန် တော်   ထင်   ပါ   တယ်   ။

==> test.my.syl <==
 လူ နာ   က   မ ကျေ နပ်   ဘူး   ပြီး တော့   သူ မ   က   ခင် ဗျား   ကို   တိုင် ပါ တယ် ။
 ခင် ဗျား   ညာ ဘက် ခြမ်း   နဲ့   တွဲ ဖက်   လုပ် ဆောင်   တဲ့ နေ ရာ   မှာ   ခင် ဗျား   မှာ   ပြ ဿ နာ   တွေ   ရှိ   နေ   တယ်   ။
 စိတ်   ကို   အ ပန်း ဖြေ   စေ တဲ့   ဆေး ဝါး   တွေ   ကို   ခင် ဗျား   အ သုံး ပြု   ပါ   သ လား   ။
 ခွဲ စိတ်   မှု   က   ပုံ မှန်   ခွဲ စိတ်   မှု   ထက်   ကျော် လွန်   ပြီး   အ ကျိုး ကျေး ဇူး   အ များ ကြီး   ရှိ   ပါ   တယ်   ။
 ဟမ်   ။   တ ချို့   က လေး   တွေ   က   သွား မ တိုက်   လည်း   ဘာ လို့   သွား ပေါက်   မ ဖြစ်   တာ   လဲ   ။
 လိင် တံ   ကြာ ရှည်   စွာ   တော င့် တင်း   ခြင်း   က   ဘာ ကို   ဆို လို တာ   လဲ   ။
 ကောင်း ပြီ   ၊   အား က စား ရုံ   ။
 ဟုတ် ပြီ   ။   ကျွန် တော့်   မျက် လုံး   တွေ   က   ဘာ လို့   ဒီ လောက် တောင်   မျက် ရည် ဝဲ   နေ ရ   တာ လဲ   ။
 ခင် ဗျား   မှာ   အား   တဲ့   အ ချိန်   ရှိ   ရင်   ၊   ခင် ဗျား   ကျွန် တော်   နဲ့   ကျွန် တော်   တို့   သူ ငယ် ချင်း တွေ   နဲ့   အ ချိန် ဖြုန်း   နိုင်   ပါ   တယ်   ၊   ကျွန် တော်   တို့   ရုပ် ရှင်   သွား   ကြည့် ဖို့   စီ စ ဥ်   နေ   ကြ   တယ်   ။
 ကျွန် တော်   သေ ချာ တော့   မ သိ   ပေ မဲ့   ဆီး ပိုး ဝင်   ခြင်း   ၊   ဆီး လမ်း ကြောင်း   ပိုး ဝင်   ခြင်း   ၊   ကျောက် ကပ်   ပိုး ဝင်   ခြင်း   ၊   လိင် မှ တစ် ဆ င့်   ကူး စက်   တတ်   တဲ့   ရော ဂါ   များ   ၊   ဒါ က   ဆ ရာ ဝန် ဆီ   သွား သ င့်   တဲ့   ကိစ္စ ထဲ   က   အ နည်း ငယ်   ပဲ   ရှိ သေး   တယ်   ။

==> train.my.syl <==
 ခင် ဗျား   ရဲ့   သွေး တွင်း   သ ကြား ဓာတ်   ပ မာ ဏ   ကို   ကျွန် တော်   တို့   စစ် ဆေး ပြီး   တာ ကို   ခင် ဗျား   သိ မှာ   ပါ   ။
 ခွဲ စိတ်   ထား   သော   အ ရေ ပြား   အောက်   တွင်   သုတ် ပိုး   ပြွန်   ကို   တွေ့ နိုင်   ပါ   တယ်   ။
 ဒီ နေ့   ဓာတ် မှန် က တော့   ခြေ ကျင်း ဝတ်   အ ရိုး ကျိုး   တယ်   လို့   ပြ   ခဲ့   တယ်   ။
 ကျွန် တော်   သိ နှ င့်   နေ   တယ်   ။   အိန္ဒိ ယ   မိန်း က လေး   တွေ ကို   လိင် ဆန္ဒ   ပြီး မြောက်   အောင်   ဘယ် လို   ကူ ညီ ပေး   ရ လဲ   ။
 သူ မ   ကို   စိတ်   သက် သာ အောင်   လုပ် ပြီး   သူ မ   ရဲ့   မိ သား စု   နဲ့   လူ မှု ဝန် ဆောင်   မှု   တွေ   ဆီ   က   အ ကူ အ ညီ   ယူ ရန်   နဲ့   သူ မ   ယုံ ကြည်   တဲ့   လူ တွေ   ကို   ရင် ဖွ င့်   ပြော   ပါ   ။
 ခင် ဗျား   မှာ   အ ဖျား   ရှိ   လား   ။
 ခွဲ စိတ် မှု   ပြီး နောက်   ခင် ဗျား   ကို   နား နေ ဆောင်   သို့   ခေါ် ဆောင်   သွား   ပါ   မယ်   ၊   ခင် ဗျား   မေ့ ဆေး   မှ   ပြန် လည်   သက် သာ   လာ   ရင်   ခင် ဗျား   ကို   လူ နာ ဆောင်   သို့   ခေါ် သွား   ပါ   လိ မ့်   မယ်   ။
 ဒီ   မှာ   နာ   သေး   လား   ။
 မ ဟုတ် ဘူး   ၊   ဒေါက် တာ   ။   ကျွန် မ   အ ဆင် ပြေ   ပါ   တယ်   ၊   ကျွန် မ   ကို   ပြော   ပါ   ။
 ခင် ဗျား   ဒါ   ကို   ဖတ်   ပြီး   မေး ခွန်း   ရှိ   ရင်   ကျေး ဇူး ပြု ပြီး   ကျွန် တော်   တို့   သိ   ပါ   ရ   စေ   ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ 
```

အဲဒါကြောင့် space cleaning လုပ်ပေးတဲ့ script ကို GitHub ကနေ download လုပ်ယူခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/clean-space.pl
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-01 23:29:01--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/clean-space.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.108.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 686 [text/plain]
Saving to: ‘clean-space.pl’

clean-space.pl                  100%[=====================================================>]     686  --.-KB/s    in 0s      

2022-05-01 23:29:02 (94.2 MB/s) - ‘clean-space.pl’ saved [686/686]

(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

စောစောက syllable ဖြတ်ထားတဲ့ မြန်မာဒေတာဖိုင်တွေကို space cleaning လုပ်ခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./clean-space.pl ./train.my.syl > train.my.syl.clean
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./clean-space.pl ./dev.my.syl > dev.my.syl.clean
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ perl ./clean-space.pl ./test.my.syl > test.my.syl.clean
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ 
```

            
