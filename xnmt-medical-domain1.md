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

word ဖိုင်တွေကို backup ကူးထားပြီး၊ clean လုပ်ထားပြီးသား ဖိုင်တွေကို config ဖိုင်ကနေ ယူသုံးတဲ့ပုံစံ ညီအောင် နာမည်အသစ်ပေးပြီး copy ကူးယူခဲ့ ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ mkdir word
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ mv {train,dev,test}.my ./word/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ cp train.my.syl.clean train.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ cp dev.my.syl.clean dev.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ cp test.my.syl.clean test.my
```

word count လုပ်ကြည့်ရင်တော့ syllable ဖြတ်ထားတာမို့ word ထက်စာရင် များနေရမယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ wc {train,dev,test}.my
  13592  363914 3483167 train.my
    500   12957  124151 dev.my
    500   13404  128038 test.my
  14592  390275 3735356 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ wc ./word/*
    500    7744  118989 ./word/dev.my
    500    8017  122689 ./word/test.my
  13592  217238 3337665 ./word/train.my
  14592  232999 3579343 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

training မလုပ်ခင်မှာ ဖိုင်တွေကို မျက်လုံးနဲ့ တချက် ကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ head train.my
ခင် ဗျား ရဲ့ သွေး တွင်း သ ကြား ဓာတ် ပ မာ ဏ ကို ကျွန် တော် တို့ စစ် ဆေး ပြီး တာ ကို ခင် ဗျား သိ မှာ ပါ ။
ခွဲ စိတ် ထား သော အ ရေ ပြား အောက် တွင် သုတ် ပိုး ပြွန် ကို တွေ့ နိုင် ပါ တယ် ။
ဒီ နေ့ ဓာတ် မှန် က တော့ ခြေ ကျင်း ဝတ် အ ရိုး ကျိုး တယ် လို့ ပြ ခဲ့ တယ် ။
ကျွန် တော် သိ နှ င့် နေ တယ် ။ အိန္ဒိ ယ မိန်း က လေး တွေ ကို လိင် ဆန္ဒ ပြီး မြောက် အောင် ဘယ် လို ကူ ညီ ပေး ရ လဲ ။
သူ မ ကို စိတ် သက် သာ အောင် လုပ် ပြီး သူ မ ရဲ့ မိ သား စု နဲ့ လူ မှု ဝန် ဆောင် မှု တွေ ဆီ က အ ကူ အ ညီ ယူ ရန် နဲ့ သူ မ ယုံ ကြည် တဲ့ လူ တွေ ကို ရင် ဖွ င့် ပြော ပါ ။
ခင် ဗျား မှာ အ ဖျား ရှိ လား ။
ခွဲ စိတ် မှု ပြီး နောက် ခင် ဗျား ကို နား နေ ဆောင် သို့ ခေါ် ဆောင် သွား ပါ မယ် ၊ ခင် ဗျား မေ့ ဆေး မှ ပြန် လည် သက် သာ လာ ရင် ခင် ဗျား ကို လူ နာ ဆောင် သို့ ခေါ် သွား ပါ လိ မ့် မယ် ။
ဒီ မှာ နာ သေး လား ။
မ ဟုတ် ဘူး ၊ ဒေါက် တာ ။ ကျွန် မ အ ဆင် ပြေ ပါ တယ် ၊ ကျွန် မ ကို ပြော ပါ ။
ခင် ဗျား ဒါ ကို ဖတ် ပြီး မေး ခွန်း ရှိ ရင် ကျေး ဇူး ပြု ပြီး ကျွန် တော် တို့ သိ ပါ ရ စေ ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ head dev.my
စီ နီ ယာ တွေ ရဲ့ အ ကူ အ ညီ နဲ့ ရင် ဘတ် ကို အ ပေါက် ဖောက် ပြီး ပိုက် ထ ည့် ဖို့ စီ စဉ် ထား ပါ တယ် ။
သာ မန် ဆီး အိတ် က မ ထင် ရှား ပါ ဘူး ။
ခင် ဗျား မိ သား စု ထဲ မှာ က လေး တုန်း က တည်း က နှ လုံး ရော ဂါ သည် ဒါ မှ မ ဟုတ် နှ လုံး ခုန် သံ မူ မ မှန် ဖြစ် ဖူး တဲ့ သူ တစ် ယောက် ယောက် ရှိ လား ။
ခင် ဗျား အောင် မြင် စွာ ဆေး ဖြတ် နိုင် မှာ ကျွန် တော် သိ ပါ တယ် ၊ ဒါ ပေ မဲ့ ပြ ဿ နာ ဆို တာ အ ချိန် တိုင်း ရှိ စ မြဲ မို့ ဒီ ဆေး တွေ ကို စီ မံ ဖို့ ကျွန် တော် တို့ ထိုး ဆေး ကို အ သုံး ပြု ရ မယ် ၊ အဲ ဒါ ကို တော့ ဆေး ထိုး အပ် လဲ လှယ် တဲ့ ပ ရို ဂ ရမ် လို့ ကျွန် တော် တို့ ခေါ် ပါ တယ် ။
ခု က ဘာ နှစ် လဲ ။
ဟမ် ။ မေး ခွန်း ကောင်း ပဲ ။ ဆေး လိပ် သောက် တာ ကြော င့် ဖြစ် မယ် လို့ ကျွန် တော် ထင် ပါ တယ် ။
ကျေး ဇူး ပြု ပြီး ခင် ဗျား ရဲ့ ဘယ် ဘက် ဒါ မှ မ ဟုတ် ညာ ဘက် သို့ စောင်း ပြီး လှဲ ပေး နိုင် မ လား ။
အဲ ဒါ အ ဓိပ္ပာယ် မ ရှိ ဘူး ။ ခင် ဗျား ဘာ လို့ ဆန် ထ ရမ် ကို သောက် တာ လဲ ။
ပုံ မှန် အား ဖြ င့် သ င့် တော် တဲ့ ကြို တင် ကာ ကွယ် မှု တွေ လုပ် ပြီး မှ သာ ကျွန် တော် ဒီ အ ခန်း ထဲ ကို ဝင် လာ မှာ ဖြစ် တယ် ။
ဟမ် ။ မေး ခွန်း ကောင်း ပဲ ။ အဲ ဒါ အိတ် စီ ဒ ရင်း မိုင် ဂ ရိန်း လို့ ကျွန် တော် ထင် ပါ တယ် ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$ head test.my
လူ နာ က မ ကျေ နပ် ဘူး ပြီး တော့ သူ မ က ခင် ဗျား ကို တိုင် ပါ တယ် ။
ခင် ဗျား ညာ ဘက် ခြမ်း နဲ့ တွဲ ဖက် လုပ် ဆောင် တဲ့ နေ ရာ မှာ ခင် ဗျား မှာ ပြ ဿ နာ တွေ ရှိ နေ တယ် ။
စိတ် ကို အ ပန်း ဖြေ စေ တဲ့ ဆေး ဝါး တွေ ကို ခင် ဗျား အ သုံး ပြု ပါ သ လား ။
ခွဲ စိတ် မှု က ပုံ မှန် ခွဲ စိတ် မှု ထက် ကျော် လွန် ပြီး အ ကျိုး ကျေး ဇူး အ များ ကြီး ရှိ ပါ တယ် ။
ဟမ် ။ တ ချို့ က လေး တွေ က သွား မ တိုက် လည်း ဘာ လို့ သွား ပေါက် မ ဖြစ် တာ လဲ ။
လိင် တံ ကြာ ရှည် စွာ တော င့် တင်း ခြင်း က ဘာ ကို ဆို လို တာ လဲ ။
ကောင်း ပြီ ၊ အား က စား ရုံ ။
ဟုတ် ပြီ ။ ကျွန် တော့် မျက် လုံး တွေ က ဘာ လို့ ဒီ လောက် တောင် မျက် ရည် ဝဲ နေ ရ တာ လဲ ။
ခင် ဗျား မှာ အား တဲ့ အ ချိန် ရှိ ရင် ၊ ခင် ဗျား ကျွန် တော် နဲ့ ကျွန် တော် တို့ သူ ငယ် ချင်း တွေ နဲ့ အ ချိန် ဖြုန်း နိုင် ပါ တယ် ၊ ကျွန် တော် တို့ ရုပ် ရှင် သွား ကြည့် ဖို့ စီ စ ဥ် နေ ကြ တယ် ။
ကျွန် တော် သေ ချာ တော့ မ သိ ပေ မဲ့ ဆီး ပိုး ဝင် ခြင်း ၊ ဆီး လမ်း ကြောင်း ပိုး ဝင် ခြင်း ၊ ကျောက် ကပ် ပိုး ဝင် ခြင်း ၊ လိင် မှ တစ် ဆ င့် ကူး စက် တတ် တဲ့ ရော ဂါ များ ၊ ဒါ က ဆ ရာ ဝန် ဆီ သွား သ င့် တဲ့ ကိစ္စ ထဲ က အ နည်း ငယ် ပဲ ရှိ သေး တယ် ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl/data$
```

## Training (syl, en-my)

config ဖိုင်တွေက word နဲ့ train လုပ်စဉ်က သုံးခဲ့တဲ့ ဖိုင်တွေကိုပဲ သုံးလို့ ရမယ်လို့ ထင်တယ်။  
အကြမ်းမျဉ်းအားဖြင့်က အတူတူပါပဲ သို့သော် experiment name ပြောင်းတာတို့ config ဖိုင်ကိုယ်တိုင်ရဲ့ နာမည်ကိုလည်း နောက်ပိုင်းမှာ ပြန်ကြည့်ရင် ရှင်းနေအောင် နာမည်ပြောင်းပေးခဲ့...  


```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ cp ../word/config.medical.* .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ ls
config.medical.en-my-word.yaml  config.medical.my-en-word.yaml  data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ mv config.medical.en-my-word.yaml config.medical.en-my-syl.yaml 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ mv config.medical.my-en-word.yaml config.medical.my-en-syl.yaml 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ ls 
config.medical.en-my-syl.yaml  config.medical.my-en-syl.yaml  data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

တကယ်တမ်းက config ဖိုင်မှာ experiment name တစ်ခုကိုပဲ syl ဆိုတာ ထပ်ဖြည့်လိုက်တာပါ။  
en-my direction အတွက် updated config ဖိုင်က အောက်ပါအတိုင်း  

```yaml
# standard settings
medical.syl.en-my: !Experiment
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

training စလုပ် ...  

```
xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ time xnmt --backend torch --gpu ./config.medical.en-my-syl.yaml 
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-01 23:46:18
=> Running medical.syl.en-my
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 15725870
> Training
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
[medical.syl.en-my] Epoch 0.0770: train_loss/word=6.449455 (steps=25, words/sec=10757.61, time=0-00:00:04)
[medical.syl.en-my] Epoch 0.1508: train_loss/word=6.042576 (steps=49, words/sec=11939.57, time=0-00:00:07)
[medical.syl.en-my] Epoch 0.2293: train_loss/word=5.983436 (steps=75, words/sec=11062.98, time=0-00:00:10)
[medical.syl.en-my] Epoch 0.3032: train_loss/word=5.812195 (steps=98, words/sec=11882.33, time=0-00:00:12)
[medical.syl.en-my] Epoch 0.3773: train_loss/word=5.662924 (steps=120, words/sec=12773.39, time=0-00:00:14)
[medical.syl.en-my] Epoch 0.4539: train_loss/word=5.431385 (steps=140, words/sec=12428.67, time=0-00:00:16)
[medical.syl.en-my] Epoch 0.5275: train_loss/word=5.361574 (steps=161, words/sec=13303.17, time=0-00:00:18)
[medical.syl.en-my] Epoch 0.6047: train_loss/word=5.226443 (steps=184, words/sec=12503.40, time=0-00:00:20)
[medical.syl.en-my] Epoch 0.6789: train_loss/word=5.120733 (steps=205, words/sec=13020.61, time=0-00:00:22)
[medical.syl.en-my] Epoch 0.7565: train_loss/word=5.012428 (steps=229, words/sec=13403.80, time=0-00:00:25)
[medical.syl.en-my] Epoch 0.8351: train_loss/word=4.937770 (steps=253, words/sec=11353.02, time=0-00:00:27)
[medical.syl.en-my] Epoch 0.9105: train_loss/word=4.829199 (steps=277, words/sec=12469.63, time=0-00:00:30)
[medical.syl.en-my] Epoch 0.9844: train_loss/word=4.790692 (steps=298, words/sec=12521.43, time=0-00:00:32)
[medical.syl.en-my] Epoch 1.0000: train_loss/word=4.782508 (steps=303, words/sec=13834.74, time=0-00:00:32)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 1.0000 dev BLEU4: 0.01099024124992242, 0.064975/0.024005/0.006791/0.001377 (BP = 1.000000, ratio=2.86, hyp_len=37076, ref_len=12957) (time=0-00:02:10)
[medical.syl.en-my]              dev auxiliary GLEU: 0.024515
[medical.syl.en-my]              dev auxiliary Loss: 4.713 (ref_len=12957)
             checkpoint took 0-00:01:37
  best dev score, writing out model
[medical.syl.en-my] Epoch 1.0027: train_loss/word=4.665554 (steps=304, words/sec=9582.11, time=0-00:02:19)
[medical.syl.en-my] Epoch 1.0791: train_loss/word=4.655997 (steps=328, words/sec=12032.22, time=0-00:02:22)
[medical.syl.en-my] Epoch 1.1550: train_loss/word=4.630332 (steps=352, words/sec=11175.63, time=0-00:02:24)
[medical.syl.en-my] Epoch 1.2318: train_loss/word=4.483023 (steps=373, words/sec=13953.66, time=0-00:02:26)
[medical.syl.en-my] Epoch 1.3055: train_loss/word=4.525351 (steps=395, words/sec=12570.71, time=0-00:02:28)
[medical.syl.en-my] Epoch 1.3796: train_loss/word=4.447316 (steps=418, words/sec=11936.46, time=0-00:02:31)
[medical.syl.en-my] Epoch 1.4542: train_loss/word=4.442305 (steps=440, words/sec=12245.45, time=0-00:02:33)
[medical.syl.en-my] Epoch 1.5294: train_loss/word=4.344111 (steps=465, words/sec=12151.93, time=0-00:02:36)
[medical.syl.en-my] Epoch 1.6061: train_loss/word=4.322758 (steps=489, words/sec=12236.89, time=0-00:02:38)
[medical.syl.en-my] Epoch 1.6819: train_loss/word=4.256598 (steps=509, words/sec=14299.89, time=0-00:02:40)
[medical.syl.en-my] Epoch 1.7582: train_loss/word=4.191670 (steps=530, words/sec=13407.48, time=0-00:02:42)
[medical.syl.en-my] Epoch 1.8369: train_loss/word=4.225763 (steps=555, words/sec=12281.29, time=0-00:02:44)
[medical.syl.en-my] Epoch 1.9111: train_loss/word=4.170138 (steps=578, words/sec=11913.10, time=0-00:02:46)
[medical.syl.en-my] Epoch 1.9861: train_loss/word=4.131441 (steps=601, words/sec=12569.92, time=0-00:02:49)
[medical.syl.en-my] Epoch 2.0000: train_loss/word=4.342649 (steps=608, words/sec=7148.38, time=0-00:02:50)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 2.0000 dev BLEU4: 0.09168901023230502, 0.340148/0.157660/0.071213/0.033942 (BP = 0.859305, ratio=0.87, hyp_len=11251, ref_len=12957) (time=0-00:03:25)
[medical.syl.en-my]              dev auxiliary GLEU: 0.121011
[medical.syl.en-my]              dev auxiliary Loss: 4.089 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[medical.syl.en-my] Epoch 2.0025: train_loss/word=4.136420 (steps=609, words/sec=13020.92, time=0-00:03:29)
[medical.syl.en-my] Epoch 2.0805: train_loss/word=4.005873 (steps=632, words/sec=12240.65, time=0-00:03:31)
[medical.syl.en-my] Epoch 2.1552: train_loss/word=4.010615 (steps=657, words/sec=11514.31, time=0-00:03:34)
[medical.syl.en-my] Epoch 2.2298: train_loss/word=3.983417 (steps=681, words/sec=12401.82, time=0-00:03:36)
[medical.syl.en-my] Epoch 2.3036: train_loss/word=3.922187 (steps=704, words/sec=11467.57, time=0-00:03:39)
[medical.syl.en-my] Epoch 2.3804: train_loss/word=3.895779 (steps=725, words/sec=12046.03, time=0-00:03:41)
[medical.syl.en-my] Epoch 2.4572: train_loss/word=3.917246 (steps=749, words/sec=11602.44, time=0-00:03:43)
[medical.syl.en-my] Epoch 2.5336: train_loss/word=3.931775 (steps=772, words/sec=12204.00, time=0-00:03:45)
[medical.syl.en-my] Epoch 2.6072: train_loss/word=3.920406 (steps=795, words/sec=12703.53, time=0-00:03:48)
[medical.syl.en-my] Epoch 2.6854: train_loss/word=3.830536 (steps=816, words/sec=12911.88, time=0-00:03:50)
[medical.syl.en-my] Epoch 2.7604: train_loss/word=3.798772 (steps=837, words/sec=12923.81, time=0-00:03:52)
[medical.syl.en-my] Epoch 2.8344: train_loss/word=3.805916 (steps=859, words/sec=12497.59, time=0-00:03:54)
[medical.syl.en-my] Epoch 2.9086: train_loss/word=3.872956 (steps=885, words/sec=11404.95, time=0-00:03:57)
[medical.syl.en-my] Epoch 2.9837: train_loss/word=3.808479 (steps=908, words/sec=11953.99, time=0-00:03:59)
[medical.syl.en-my] Epoch 3.0000: train_loss/word=3.679333 (steps=912, words/sec=16569.56, time=0-00:03:59)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 3.0000 dev BLEU4: 0.1308309731594243, 0.396426/0.206009/0.105213/0.058485 (BP = 0.873815, ratio=0.88, hyp_len=11417, ref_len=12957) (time=0-00:04:36)
[medical.syl.en-my]              dev auxiliary GLEU: 0.155865
[medical.syl.en-my]              dev auxiliary Loss: 3.757 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
[medical.syl.en-my] Epoch 3.0029: train_loss/word=3.730231 (steps=913, words/sec=12623.54, time=0-00:04:39)
[medical.syl.en-my] Epoch 3.0781: train_loss/word=3.694070 (steps=939, words/sec=10841.65, time=0-00:04:42)
[medical.syl.en-my] Epoch 3.1531: train_loss/word=3.709771 (steps=963, words/sec=11293.49, time=0-00:04:45)
[medical.syl.en-my] Epoch 3.2304: train_loss/word=3.601261 (steps=987, words/sec=13199.34, time=0-00:04:47)
[medical.syl.en-my] Epoch 3.3052: train_loss/word=3.598760 (steps=1011, words/sec=11545.28, time=0-00:04:49)
[medical.syl.en-my] Epoch 3.3800: train_loss/word=3.564337 (steps=1031, words/sec=12860.07, time=0-00:04:51)
[medical.syl.en-my] Epoch 3.4536: train_loss/word=3.560421 (steps=1052, words/sec=12209.74, time=0-00:04:53)
[medical.syl.en-my] Epoch 3.5276: train_loss/word=3.565409 (steps=1073, words/sec=12506.76, time=0-00:04:55)
[medical.syl.en-my] Epoch 3.6020: train_loss/word=3.463567 (steps=1093, words/sec=12402.65, time=0-00:04:57)
[medical.syl.en-my] Epoch 3.6758: train_loss/word=3.540402 (steps=1116, words/sec=11972.46, time=0-00:04:59)
[medical.syl.en-my] Epoch 3.7506: train_loss/word=3.536281 (steps=1140, words/sec=12081.54, time=0-00:05:02)
[medical.syl.en-my] Epoch 3.8275: train_loss/word=3.565021 (steps=1165, words/sec=11029.85, time=0-00:05:05)
[medical.syl.en-my] Epoch 3.9044: train_loss/word=3.566181 (steps=1190, words/sec=11398.91, time=0-00:05:07)
[medical.syl.en-my] Epoch 3.9785: train_loss/word=3.549159 (steps=1212, words/sec=12421.41, time=0-00:05:10)
[medical.syl.en-my] Epoch 4.0000: train_loss/word=3.441866 (steps=1218, words/sec=15069.63, time=0-00:05:10)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 4.0000 dev BLEU4: 0.1651003546724009, 0.472842/0.261429/0.142772/0.083429 (BP = 0.842830, ratio=0.85, hyp_len=11065, ref_len=12957) (time=0-00:05:46)
[medical.syl.en-my]              dev auxiliary GLEU: 0.195598
[medical.syl.en-my]              dev auxiliary Loss: 3.527 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[medical.syl.en-my] Epoch 4.0051: train_loss/word=3.027872 (steps=1219, words/sec=18685.24, time=0-00:05:49)
[medical.syl.en-my] Epoch 4.0791: train_loss/word=3.373485 (steps=1243, words/sec=12336.90, time=0-00:05:51)
[medical.syl.en-my] Epoch 4.1546: train_loss/word=3.392860 (steps=1266, words/sec=12408.55, time=0-00:05:54)
[medical.syl.en-my] Epoch 4.2293: train_loss/word=3.437794 (steps=1290, words/sec=11924.03, time=0-00:05:56)
[medical.syl.en-my] Epoch 4.3030: train_loss/word=3.385536 (steps=1313, words/sec=10683.05, time=0-00:05:59)
[medical.syl.en-my] Epoch 4.3774: train_loss/word=3.291455 (steps=1334, words/sec=13248.45, time=0-00:06:01)
[medical.syl.en-my] Epoch 4.4539: train_loss/word=3.264868 (steps=1357, words/sec=12768.68, time=0-00:06:03)
[medical.syl.en-my] Epoch 4.5285: train_loss/word=3.373045 (steps=1381, words/sec=12000.96, time=0-00:06:06)
[medical.syl.en-my] Epoch 4.6026: train_loss/word=3.273367 (steps=1403, words/sec=13542.82, time=0-00:06:08)
[medical.syl.en-my] Epoch 4.6763: train_loss/word=3.323933 (steps=1428, words/sec=11425.77, time=0-00:06:10)
[medical.syl.en-my] Epoch 4.7518: train_loss/word=3.312043 (steps=1450, words/sec=11559.66, time=0-00:06:13)
[medical.syl.en-my] Epoch 4.8303: train_loss/word=3.292932 (steps=1472, words/sec=12216.43, time=0-00:06:15)
[medical.syl.en-my] Epoch 4.9052: train_loss/word=3.208125 (steps=1494, words/sec=12758.01, time=0-00:06:17)
[medical.syl.en-my] Epoch 4.9810: train_loss/word=3.271132 (steps=1517, words/sec=12030.68, time=0-00:06:19)
[medical.syl.en-my] Epoch 5.0000: train_loss/word=3.274344 (steps=1523, words/sec=12361.14, time=0-00:06:20)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 5.0000 dev BLEU4: 0.2009904562247608, 0.482384/0.276610/0.158015/0.094312 (BP = 0.951796, ratio=0.95, hyp_len=12347, ref_len=12957) (time=0-00:06:58)
[medical.syl.en-my]              dev auxiliary GLEU: 0.225232
[medical.syl.en-my]              dev auxiliary Loss: 3.368 (ref_len=12957)
             checkpoint took 0-00:00:37
  best dev score, writing out model
[medical.syl.en-my] Epoch 5.0049: train_loss/word=3.033296 (steps=1524, words/sec=17438.83, time=0-00:07:01)
[medical.syl.en-my] Epoch 5.0797: train_loss/word=3.186673 (steps=1547, words/sec=11760.43, time=0-00:07:03)
[medical.syl.en-my] Epoch 5.1571: train_loss/word=3.114829 (steps=1570, words/sec=12569.33, time=0-00:07:05)
[medical.syl.en-my] Epoch 5.2338: train_loss/word=3.100167 (steps=1593, words/sec=12461.96, time=0-00:07:08)
[medical.syl.en-my] Epoch 5.3082: train_loss/word=3.103512 (steps=1615, words/sec=12742.61, time=0-00:07:10)
[medical.syl.en-my] Epoch 5.3857: train_loss/word=3.112627 (steps=1640, words/sec=12727.83, time=0-00:07:12)
[medical.syl.en-my] Epoch 5.4614: train_loss/word=3.206031 (steps=1666, words/sec=10527.77, time=0-00:07:15)
[medical.syl.en-my] Epoch 5.5356: train_loss/word=3.137171 (steps=1690, words/sec=11961.65, time=0-00:07:18)
[medical.syl.en-my] Epoch 5.6131: train_loss/word=3.024104 (steps=1710, words/sec=13603.81, time=0-00:07:19)
[medical.syl.en-my] Epoch 5.6881: train_loss/word=3.119931 (steps=1733, words/sec=12251.95, time=0-00:07:22)
[medical.syl.en-my] Epoch 5.7640: train_loss/word=3.062264 (steps=1756, words/sec=11637.19, time=0-00:07:24)
[medical.syl.en-my] Epoch 5.8418: train_loss/word=3.180205 (steps=1783, words/sec=10967.49, time=0-00:07:27)
[medical.syl.en-my] Epoch 5.9193: train_loss/word=3.068629 (steps=1806, words/sec=12898.50, time=0-00:07:29)
[medical.syl.en-my] Epoch 5.9940: train_loss/word=3.033971 (steps=1826, words/sec=13675.79, time=0-00:07:31)
[medical.syl.en-my] Epoch 6.0000: train_loss/word=3.080540 (steps=1828, words/sec=13529.93, time=0-00:07:31)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 6.0000 dev BLEU4: 0.22759180632624595, 0.548301/0.330471/0.196251/0.122206 (BP = 0.886427, ratio=0.89, hyp_len=11563, ref_len=12957) (time=0-00:08:07)
[medical.syl.en-my]              dev auxiliary GLEU: 0.256951
[medical.syl.en-my]              dev auxiliary Loss: 3.242 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[medical.syl.en-my] Epoch 6.0040: train_loss/word=2.805032 (steps=1829, words/sec=16885.27, time=0-00:08:10)
[medical.syl.en-my] Epoch 6.0822: train_loss/word=2.960468 (steps=1853, words/sec=12354.62, time=0-00:08:12)
[medical.syl.en-my] Epoch 6.1600: train_loss/word=2.984009 (steps=1879, words/sec=11237.54, time=0-00:08:15)
[medical.syl.en-my] Epoch 6.2343: train_loss/word=2.903008 (steps=1900, words/sec=13422.74, time=0-00:08:17)
[medical.syl.en-my] Epoch 6.3084: train_loss/word=2.879579 (steps=1921, words/sec=12933.32, time=0-00:08:19)
[medical.syl.en-my] Epoch 6.3840: train_loss/word=2.835366 (steps=1941, words/sec=14204.71, time=0-00:08:21)
[medical.syl.en-my] Epoch 6.4603: train_loss/word=2.961677 (steps=1966, words/sec=12179.51, time=0-00:08:23)
[medical.syl.en-my] Epoch 6.5380: train_loss/word=2.963696 (steps=1990, words/sec=12203.66, time=0-00:08:26)
[medical.syl.en-my] Epoch 6.6131: train_loss/word=2.956896 (steps=2013, words/sec=12544.13, time=0-00:08:28)
[medical.syl.en-my] Epoch 6.6883: train_loss/word=2.919949 (steps=2036, words/sec=12813.02, time=0-00:08:30)
[medical.syl.en-my] Epoch 6.7643: train_loss/word=2.967431 (steps=2058, words/sec=12444.88, time=0-00:08:32)
[medical.syl.en-my] Epoch 6.8383: train_loss/word=2.916672 (steps=2080, words/sec=12292.15, time=0-00:08:35)
[medical.syl.en-my] Epoch 6.9124: train_loss/word=2.973231 (steps=2103, words/sec=11285.39, time=0-00:08:37)
[medical.syl.en-my] Epoch 6.9878: train_loss/word=2.928396 (steps=2127, words/sec=11823.53, time=0-00:08:40)
[medical.syl.en-my] Epoch 7.0000: train_loss/word=3.024202 (steps=2131, words/sec=10570.51, time=0-00:08:40)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 7.0000 dev BLEU4: 0.259986032686756, 0.551666/0.340037/0.209770/0.135106 (BP = 0.962820, ratio=0.96, hyp_len=12484, ref_len=12957) (time=0-00:09:18)
[medical.syl.en-my]              dev auxiliary GLEU: 0.279629
[medical.syl.en-my]              dev auxiliary Loss: 3.145 (ref_len=12957)
             checkpoint took 0-00:00:38
  best dev score, writing out model
[medical.syl.en-my] Epoch 7.0026: train_loss/word=2.832834 (steps=2132, words/sec=11970.30, time=0-00:09:21)
[medical.syl.en-my] Epoch 7.0800: train_loss/word=2.753453 (steps=2156, words/sec=12266.11, time=0-00:09:24)
[medical.syl.en-my] Epoch 7.1561: train_loss/word=2.817156 (steps=2181, words/sec=12478.23, time=0-00:09:26)
[medical.syl.en-my] Epoch 7.2302: train_loss/word=2.806054 (steps=2203, words/sec=12929.19, time=0-00:09:29)
[medical.syl.en-my] Epoch 7.3058: train_loss/word=2.693140 (steps=2223, words/sec=14007.94, time=0-00:09:30)
[medical.syl.en-my] Epoch 7.3814: train_loss/word=2.670823 (steps=2243, words/sec=14609.74, time=0-00:09:32)
[medical.syl.en-my] Epoch 7.4559: train_loss/word=2.792532 (steps=2268, words/sec=11537.35, time=0-00:09:34)
[medical.syl.en-my] Epoch 7.5310: train_loss/word=2.793217 (steps=2290, words/sec=12442.53, time=0-00:09:37)
[medical.syl.en-my] Epoch 7.6068: train_loss/word=2.897852 (steps=2316, words/sec=10727.31, time=0-00:09:40)
[medical.syl.en-my] Epoch 7.6830: train_loss/word=2.773273 (steps=2339, words/sec=12611.27, time=0-00:09:42)
[medical.syl.en-my] Epoch 7.7571: train_loss/word=2.843442 (steps=2364, words/sec=12258.11, time=0-00:09:44)
[medical.syl.en-my] Epoch 7.8341: train_loss/word=2.809284 (steps=2386, words/sec=11265.98, time=0-00:09:47)
[medical.syl.en-my] Epoch 7.9097: train_loss/word=2.726823 (steps=2407, words/sec=13786.08, time=0-00:09:49)
[medical.syl.en-my] Epoch 7.9844: train_loss/word=2.839620 (steps=2431, words/sec=10950.47, time=0-00:09:51)
[medical.syl.en-my] Epoch 8.0000: train_loss/word=2.776074 (steps=2436, words/sec=13583.76, time=0-00:09:52)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 8.0000 dev BLEU4: 0.2791858122781454, 0.556212/0.351103/0.225520/0.149915 (BP = 0.979416, ratio=0.98, hyp_len=12693, ref_len=12957) (time=0-00:10:29)
[medical.syl.en-my]              dev auxiliary GLEU: 0.292199
[medical.syl.en-my]              dev auxiliary Loss: 3.079 (ref_len=12957)
             checkpoint took 0-00:00:37
  best dev score, writing out model
[medical.syl.en-my] Epoch 8.0057: train_loss/word=2.197822 (steps=2437, words/sec=20339.60, time=0-00:10:32)
[medical.syl.en-my] Epoch 8.0824: train_loss/word=2.640290 (steps=2461, words/sec=11779.81, time=0-00:10:35)
[medical.syl.en-my] Epoch 8.1588: train_loss/word=2.557991 (steps=2482, words/sec=12677.92, time=0-00:10:37)
[medical.syl.en-my] Epoch 8.2340: train_loss/word=2.655938 (steps=2504, words/sec=12473.58, time=0-00:10:39)
[medical.syl.en-my] Epoch 8.3094: train_loss/word=2.649001 (steps=2525, words/sec=13060.05, time=0-00:10:41)
[medical.syl.en-my] Epoch 8.3836: train_loss/word=2.667929 (steps=2549, words/sec=12531.22, time=0-00:10:43)
[medical.syl.en-my] Epoch 8.4600: train_loss/word=2.706156 (steps=2574, words/sec=11991.40, time=0-00:10:46)
[medical.syl.en-my] Epoch 8.5346: train_loss/word=2.654573 (steps=2595, words/sec=14203.35, time=0-00:10:48)
[medical.syl.en-my] Epoch 8.6109: train_loss/word=2.740205 (steps=2620, words/sec=11232.83, time=0-00:10:51)
[medical.syl.en-my] Epoch 8.6877: train_loss/word=2.603345 (steps=2642, words/sec=13082.54, time=0-00:10:53)
[medical.syl.en-my] Epoch 8.7636: train_loss/word=2.771747 (steps=2670, words/sec=10554.22, time=0-00:10:56)
[medical.syl.en-my] Epoch 8.8399: train_loss/word=2.582838 (steps=2691, words/sec=13263.39, time=0-00:10:58)
[medical.syl.en-my] Epoch 8.9137: train_loss/word=2.675331 (steps=2714, words/sec=11718.27, time=0-00:11:00)
[medical.syl.en-my] Epoch 8.9876: train_loss/word=2.647733 (steps=2736, words/sec=12278.63, time=0-00:11:03)
[medical.syl.en-my] Epoch 9.0000: train_loss/word=2.731488 (steps=2740, words/sec=11827.02, time=0-00:11:03)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 9.0000 dev BLEU4: 0.29187098885511936, 0.590451/0.380497/0.247346/0.166744 (BP = 0.940736, ratio=0.94, hyp_len=12211, ref_len=12957) (time=0-00:11:39)
[medical.syl.en-my]              dev auxiliary GLEU: 0.309567
[medical.syl.en-my]              dev auxiliary Loss: 3.040 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
[medical.syl.en-my] Epoch 9.0024: train_loss/word=2.649746 (steps=2741, words/sec=11026.24, time=0-00:11:43)
[medical.syl.en-my] Epoch 9.0767: train_loss/word=2.520530 (steps=2763, words/sec=11765.36, time=0-00:11:45)
[medical.syl.en-my] Epoch 9.1506: train_loss/word=2.575722 (steps=2787, words/sec=12085.19, time=0-00:11:47)
[medical.syl.en-my] Epoch 9.2262: train_loss/word=2.394225 (steps=2806, words/sec=14794.10, time=0-00:11:49)
[medical.syl.en-my] Epoch 9.3014: train_loss/word=2.551423 (steps=2831, words/sec=11735.34, time=0-00:11:51)
[medical.syl.en-my] Epoch 9.3771: train_loss/word=2.541972 (steps=2854, words/sec=12326.55, time=0-00:11:54)
[medical.syl.en-my] Epoch 9.4546: train_loss/word=2.523453 (steps=2877, words/sec=12365.41, time=0-00:11:56)
[medical.syl.en-my] Epoch 9.5290: train_loss/word=2.581678 (steps=2900, words/sec=11636.38, time=0-00:11:58)
[medical.syl.en-my] Epoch 9.6026: train_loss/word=2.538374 (steps=2922, words/sec=12594.82, time=0-00:12:00)
[medical.syl.en-my] Epoch 9.6762: train_loss/word=2.595419 (steps=2946, words/sec=12758.51, time=0-00:12:03)
[medical.syl.en-my] Epoch 9.7521: train_loss/word=2.487244 (steps=2966, words/sec=14520.21, time=0-00:12:05)
[medical.syl.en-my] Epoch 9.8298: train_loss/word=2.598979 (steps=2991, words/sec=12534.96, time=0-00:12:07)
[medical.syl.en-my] Epoch 9.9044: train_loss/word=2.584240 (steps=3015, words/sec=11259.88, time=0-00:12:10)
[medical.syl.en-my] Epoch 9.9787: train_loss/word=2.589362 (steps=3037, words/sec=11010.71, time=0-00:12:12)
[medical.syl.en-my] Epoch 10.0000: train_loss/word=2.551735 (steps=3043, words/sec=14918.04, time=0-00:12:13)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 10.0000 dev BLEU4: 0.30903745779669795, 0.602820/0.393871/0.259159/0.176810 (BP = 0.956880, ratio=0.96, hyp_len=12410, ref_len=12957) (time=0-00:12:49)
[medical.syl.en-my]              dev auxiliary GLEU: 0.324445
[medical.syl.en-my]              dev auxiliary Loss: 2.986 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
[medical.syl.en-my] Epoch 10.0032: train_loss/word=2.337345 (steps=3044, words/sec=14652.46, time=0-00:12:53)
[medical.syl.en-my] Epoch 10.0792: train_loss/word=2.416294 (steps=3067, words/sec=11934.29, time=0-00:12:55)
[medical.syl.en-my] Epoch 10.1560: train_loss/word=2.434408 (steps=3089, words/sec=12012.04, time=0-00:12:57)
[medical.syl.en-my] Epoch 10.2310: train_loss/word=2.434208 (steps=3112, words/sec=13221.91, time=0-00:12:59)
[medical.syl.en-my] Epoch 10.3050: train_loss/word=2.402848 (steps=3136, words/sec=11624.44, time=0-00:13:02)
[medical.syl.en-my] Epoch 10.3804: train_loss/word=2.434217 (steps=3158, words/sec=12623.96, time=0-00:13:04)
[medical.syl.en-my] Epoch 10.4558: train_loss/word=2.415425 (steps=3181, words/sec=12941.25, time=0-00:13:06)
[medical.syl.en-my] Epoch 10.5310: train_loss/word=2.466543 (steps=3203, words/sec=12718.13, time=0-00:13:08)
[medical.syl.en-my] Epoch 10.6074: train_loss/word=2.414537 (steps=3225, words/sec=12556.16, time=0-00:13:11)
[medical.syl.en-my] Epoch 10.6829: train_loss/word=2.546193 (steps=3250, words/sec=11587.49, time=0-00:13:13)
[medical.syl.en-my] Epoch 10.7588: train_loss/word=2.422036 (steps=3273, words/sec=11728.17, time=0-00:13:16)
[medical.syl.en-my] Epoch 10.8353: train_loss/word=2.447641 (steps=3295, words/sec=13082.86, time=0-00:13:18)
[medical.syl.en-my] Epoch 10.9138: train_loss/word=2.399208 (steps=3316, words/sec=12944.25, time=0-00:13:20)
[medical.syl.en-my] Epoch 10.9889: train_loss/word=2.556407 (steps=3342, words/sec=10901.12, time=0-00:13:23)
[medical.syl.en-my] Epoch 11.0000: train_loss/word=2.471342 (steps=3346, words/sec=12563.34, time=0-00:13:23)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 11.0000 dev BLEU4: 0.3166131276818528, 0.618060/0.407303/0.269737/0.186546 (BP = 0.943757, ratio=0.95, hyp_len=12248, ref_len=12957) (time=0-00:14:00)
[medical.syl.en-my]              dev auxiliary GLEU: 0.331921
[medical.syl.en-my]              dev auxiliary Loss: 2.957 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
[medical.syl.en-my] Epoch 11.0035: train_loss/word=2.160998 (steps=3347, words/sec=13537.04, time=0-00:14:03)
[medical.syl.en-my] Epoch 11.0802: train_loss/word=2.320361 (steps=3371, words/sec=12409.04, time=0-00:14:05)
[medical.syl.en-my] Epoch 11.1544: train_loss/word=2.347400 (steps=3393, words/sec=11635.38, time=0-00:14:08)
[medical.syl.en-my] Epoch 11.2282: train_loss/word=2.407927 (steps=3418, words/sec=11166.33, time=0-00:14:11)
[medical.syl.en-my] Epoch 11.3054: train_loss/word=2.323089 (steps=3440, words/sec=11621.74, time=0-00:14:13)
[medical.syl.en-my] Epoch 11.3809: train_loss/word=2.391509 (steps=3465, words/sec=10817.85, time=0-00:14:16)
[medical.syl.en-my] Epoch 11.4563: train_loss/word=2.284138 (steps=3485, words/sec=13009.81, time=0-00:14:18)
[medical.syl.en-my] Epoch 11.5308: train_loss/word=2.345199 (steps=3507, words/sec=11497.96, time=0-00:14:20)
[medical.syl.en-my] Epoch 11.6081: train_loss/word=2.382391 (steps=3531, words/sec=11594.72, time=0-00:14:22)
[medical.syl.en-my] Epoch 11.6824: train_loss/word=2.386444 (steps=3553, words/sec=11921.59, time=0-00:14:25)
[medical.syl.en-my] Epoch 11.7595: train_loss/word=2.363131 (steps=3576, words/sec=12334.64, time=0-00:14:27)
[medical.syl.en-my] Epoch 11.8345: train_loss/word=2.348422 (steps=3598, words/sec=11980.90, time=0-00:14:29)
[medical.syl.en-my] Epoch 11.9093: train_loss/word=2.426716 (steps=3623, words/sec=11102.29, time=0-00:14:32)
[medical.syl.en-my] Epoch 11.9852: train_loss/word=2.380454 (steps=3646, words/sec=13051.14, time=0-00:14:34)
[medical.syl.en-my] Epoch 12.0000: train_loss/word=2.249631 (steps=3650, words/sec=14443.84, time=0-00:14:35)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 12.0000 dev BLEU4: 0.32350438039645757, 0.625568/0.420019/0.281483/0.195966 (BP = 0.932365, ratio=0.93, hyp_len=12109, ref_len=12957) (time=0-00:15:10)
[medical.syl.en-my]              dev auxiliary GLEU: 0.336888
[medical.syl.en-my]              dev auxiliary Loss: 2.945 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[medical.syl.en-my] Epoch 12.0029: train_loss/word=2.195766 (steps=3651, words/sec=13508.49, time=0-00:15:13)
[medical.syl.en-my] Epoch 12.0773: train_loss/word=2.275557 (steps=3674, words/sec=11105.29, time=0-00:15:16)
[medical.syl.en-my] Epoch 12.1512: train_loss/word=2.224351 (steps=3696, words/sec=13213.79, time=0-00:15:18)
[medical.syl.en-my] Epoch 12.2271: train_loss/word=2.264343 (steps=3718, words/sec=12610.11, time=0-00:15:20)
[medical.syl.en-my] Epoch 12.3028: train_loss/word=2.266407 (steps=3740, words/sec=13098.99, time=0-00:15:22)
[medical.syl.en-my] Epoch 12.3786: train_loss/word=2.299483 (steps=3763, words/sec=11204.09, time=0-00:15:25)
[medical.syl.en-my] Epoch 12.4523: train_loss/word=2.213619 (steps=3783, words/sec=13516.90, time=0-00:15:27)
[medical.syl.en-my] Epoch 12.5269: train_loss/word=2.264760 (steps=3805, words/sec=12389.71, time=0-00:15:29)
[medical.syl.en-my] Epoch 12.6040: train_loss/word=2.316799 (steps=3830, words/sec=10726.06, time=0-00:15:32)
[medical.syl.en-my] Epoch 12.6781: train_loss/word=2.278767 (steps=3852, words/sec=12378.78, time=0-00:15:34)
[medical.syl.en-my] Epoch 12.7526: train_loss/word=2.361983 (steps=3877, words/sec=11783.91, time=0-00:15:36)
[medical.syl.en-my] Epoch 12.8304: train_loss/word=2.356508 (steps=3904, words/sec=10756.53, time=0-00:15:40)
[medical.syl.en-my] Epoch 12.9058: train_loss/word=2.231190 (steps=3926, words/sec=12803.31, time=0-00:15:42)
[medical.syl.en-my] Epoch 12.9798: train_loss/word=2.304073 (steps=3949, words/sec=11832.37, time=0-00:15:44)
[medical.syl.en-my] Epoch 13.0000: train_loss/word=2.243739 (steps=3954, words/sec=13069.73, time=0-00:15:45)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 13.0000 dev BLEU4: 0.3308049211439105, 0.629691/0.423226/0.288180/0.205176 (BP = 0.933683, ratio=0.94, hyp_len=12125, ref_len=12957) (time=0-00:16:21)
[medical.syl.en-my]              dev auxiliary GLEU: 0.340204
[medical.syl.en-my]              dev auxiliary Loss: 2.942 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
[medical.syl.en-my] Epoch 13.0018: train_loss/word=2.563223 (steps=3955, words/sec=8053.05, time=0-00:16:24)
[medical.syl.en-my] Epoch 13.0781: train_loss/word=2.147999 (steps=3978, words/sec=12239.30, time=0-00:16:26)
[medical.syl.en-my] Epoch 13.1546: train_loss/word=2.166690 (steps=4001, words/sec=12811.66, time=0-00:16:28)
[medical.syl.en-my] Epoch 13.2284: train_loss/word=2.181812 (steps=4025, words/sec=12287.46, time=0-00:16:31)
[medical.syl.en-my] Epoch 13.3033: train_loss/word=2.246368 (steps=4049, words/sec=11808.01, time=0-00:16:34)
[medical.syl.en-my] Epoch 13.3771: train_loss/word=2.132147 (steps=4069, words/sec=12718.56, time=0-00:16:35)
[medical.syl.en-my] Epoch 13.4512: train_loss/word=2.257139 (steps=4094, words/sec=10816.30, time=0-00:16:38)
[medical.syl.en-my] Epoch 13.5263: train_loss/word=2.231661 (steps=4117, words/sec=11794.65, time=0-00:16:41)
[medical.syl.en-my] Epoch 13.6034: train_loss/word=2.239490 (steps=4142, words/sec=11070.22, time=0-00:16:43)
[medical.syl.en-my] Epoch 13.6792: train_loss/word=2.217012 (steps=4165, words/sec=12101.37, time=0-00:16:46)
[medical.syl.en-my] Epoch 13.7541: train_loss/word=2.214404 (steps=4187, words/sec=11424.40, time=0-00:16:48)
[medical.syl.en-my] Epoch 13.8301: train_loss/word=2.199153 (steps=4209, words/sec=12487.09, time=0-00:16:50)
[medical.syl.en-my] Epoch 13.9052: train_loss/word=2.218125 (steps=4232, words/sec=11414.77, time=0-00:16:53)
[medical.syl.en-my] Epoch 13.9820: train_loss/word=2.223519 (steps=4253, words/sec=12666.46, time=0-00:16:55)
[medical.syl.en-my] Epoch 14.0000: train_loss/word=2.270893 (steps=4259, words/sec=10236.15, time=0-00:16:55)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 14.0000 dev BLEU4: 0.34288163059709825, 0.637286/0.431266/0.294850/0.209685 (BP = 0.949690, ratio=0.95, hyp_len=12321, ref_len=12957) (time=0-00:17:32)
[medical.syl.en-my]              dev auxiliary GLEU: 0.354195
[medical.syl.en-my]              dev auxiliary Loss: 2.918 (ref_len=12957)
             checkpoint took 0-00:00:37
  best dev score, writing out model
[medical.syl.en-my] Epoch 14.0034: train_loss/word=2.056669 (steps=4260, words/sec=15425.41, time=0-00:17:35)
[medical.syl.en-my] Epoch 14.0792: train_loss/word=2.069215 (steps=4282, words/sec=14250.62, time=0-00:17:37)
[medical.syl.en-my] Epoch 14.1542: train_loss/word=2.148128 (steps=4306, words/sec=11381.77, time=0-00:17:40)
[medical.syl.en-my] Epoch 14.2287: train_loss/word=2.159312 (steps=4329, words/sec=11988.73, time=0-00:17:43)
[medical.syl.en-my] Epoch 14.3039: train_loss/word=2.068653 (steps=4349, words/sec=14624.44, time=0-00:17:44)
[medical.syl.en-my] Epoch 14.3807: train_loss/word=2.055412 (steps=4371, words/sec=13121.61, time=0-00:17:46)
[medical.syl.en-my] Epoch 14.4567: train_loss/word=2.176916 (steps=4395, words/sec=12544.74, time=0-00:17:49)
[medical.syl.en-my] Epoch 14.5319: train_loss/word=2.187749 (steps=4421, words/sec=10010.82, time=0-00:17:52)
[medical.syl.en-my] Epoch 14.6096: train_loss/word=2.172742 (steps=4446, words/sec=10373.04, time=0-00:17:55)
[medical.syl.en-my] Epoch 14.6834: train_loss/word=2.126842 (steps=4468, words/sec=12069.09, time=0-00:17:57)
[medical.syl.en-my] Epoch 14.7571: train_loss/word=2.183985 (steps=4491, words/sec=11954.03, time=0-00:17:59)
[medical.syl.en-my] Epoch 14.8327: train_loss/word=2.128527 (steps=4513, words/sec=12824.52, time=0-00:18:01)
[medical.syl.en-my] Epoch 14.9095: train_loss/word=2.175420 (steps=4536, words/sec=12278.42, time=0-00:18:04)
[medical.syl.en-my] Epoch 14.9835: train_loss/word=2.168867 (steps=4557, words/sec=12016.10, time=0-00:18:06)
[medical.syl.en-my] Epoch 15.0000: train_loss/word=2.179272 (steps=4563, words/sec=11484.35, time=0-00:18:06)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 15.0000 dev BLEU4: 0.34265942765356794, 0.615438/0.413156/0.280235/0.197542 (BP = 0.994816, ratio=0.99, hyp_len=12890, ref_len=12957) (time=0-00:18:45)
[medical.syl.en-my]              dev auxiliary GLEU: 0.347935
[medical.syl.en-my]              dev auxiliary Loss: 2.916 (ref_len=12957)
             checkpoint took 0-00:00:38
[medical.syl.en-my] Epoch 15.0024: train_loss/word=2.164566 (steps=4564, words/sec=10924.50, time=0-00:18:45)
[medical.syl.en-my] Epoch 15.0760: train_loss/word=2.014039 (steps=4585, words/sec=12058.09, time=0-00:18:47)
[medical.syl.en-my] Epoch 15.1496: train_loss/word=2.014804 (steps=4606, words/sec=12492.52, time=0-00:18:49)
[medical.syl.en-my] Epoch 15.2248: train_loss/word=2.084567 (steps=4629, words/sec=11361.79, time=0-00:18:52)
[medical.syl.en-my] Epoch 15.2990: train_loss/word=1.994144 (steps=4650, words/sec=12385.27, time=0-00:18:54)
[medical.syl.en-my] Epoch 15.3727: train_loss/word=2.053292 (steps=4673, words/sec=12829.42, time=0-00:18:56)
[medical.syl.en-my] Epoch 15.4496: train_loss/word=2.040003 (steps=4696, words/sec=11465.20, time=0-00:18:58)
[medical.syl.en-my] Epoch 15.5257: train_loss/word=2.106320 (steps=4719, words/sec=11541.80, time=0-00:19:01)
[medical.syl.en-my] Epoch 15.6006: train_loss/word=2.097597 (steps=4742, words/sec=10984.91, time=0-00:19:03)
[medical.syl.en-my] Epoch 15.6761: train_loss/word=2.034884 (steps=4763, words/sec=11979.59, time=0-00:19:05)
[medical.syl.en-my] Epoch 15.7499: train_loss/word=2.130263 (steps=4787, words/sec=11494.62, time=0-00:19:08)
[medical.syl.en-my] Epoch 15.8261: train_loss/word=2.110267 (steps=4810, words/sec=11206.37, time=0-00:19:11)
[medical.syl.en-my] Epoch 15.9010: train_loss/word=2.192263 (steps=4836, words/sec=10161.62, time=0-00:19:14)
[medical.syl.en-my] Epoch 15.9773: train_loss/word=2.128308 (steps=4860, words/sec=11947.48, time=0-00:19:16)
[medical.syl.en-my] Epoch 16.0000: train_loss/word=2.161387 (steps=4868, words/sec=10914.39, time=0-00:19:17)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 16.0000 dev BLEU4: 0.35418342712655027, 0.636701/0.431203/0.297281/0.211847 (BP = 0.976734, ratio=0.98, hyp_len=12659, ref_len=12957) (time=0-00:19:55)
[medical.syl.en-my]              dev auxiliary GLEU: 0.363138
[medical.syl.en-my]              dev auxiliary Loss: 2.900 (ref_len=12957)
             checkpoint took 0-00:00:38
  best dev score, writing out model
[medical.syl.en-my] Epoch 16.0032: train_loss/word=1.969204 (steps=4869, words/sec=14970.61, time=0-00:19:59)
[medical.syl.en-my] Epoch 16.0769: train_loss/word=1.999472 (steps=4895, words/sec=11179.59, time=0-00:20:02)
[medical.syl.en-my] Epoch 16.1509: train_loss/word=1.941389 (steps=4917, words/sec=12681.88, time=0-00:20:04)
[medical.syl.en-my] Epoch 16.2256: train_loss/word=2.066995 (steps=4941, words/sec=10738.37, time=0-00:20:06)
[medical.syl.en-my] Epoch 16.3025: train_loss/word=1.963000 (steps=4964, words/sec=11692.25, time=0-00:20:09)
[medical.syl.en-my] Epoch 16.3771: train_loss/word=2.046694 (steps=4987, words/sec=11228.29, time=0-00:20:11)
[medical.syl.en-my] Epoch 16.4514: train_loss/word=1.973139 (steps=5006, words/sec=13128.60, time=0-00:20:13)
[medical.syl.en-my] Epoch 16.5266: train_loss/word=2.065607 (steps=5030, words/sec=11589.95, time=0-00:20:16)
[medical.syl.en-my] Epoch 16.6027: train_loss/word=2.040019 (steps=5053, words/sec=11196.62, time=0-00:20:18)
[medical.syl.en-my] Epoch 16.6766: train_loss/word=2.014010 (steps=5073, words/sec=12572.45, time=0-00:20:20)
[medical.syl.en-my] Epoch 16.7545: train_loss/word=2.035461 (steps=5096, words/sec=12473.99, time=0-00:20:22)
[medical.syl.en-my] Epoch 16.8291: train_loss/word=2.118397 (steps=5121, words/sec=11493.46, time=0-00:20:25)
[medical.syl.en-my] Epoch 16.9035: train_loss/word=2.017593 (steps=5143, words/sec=12971.71, time=0-00:20:27)
[medical.syl.en-my] Epoch 16.9777: train_loss/word=2.041071 (steps=5166, words/sec=12864.69, time=0-00:20:29)
[medical.syl.en-my] Epoch 17.0000: train_loss/word=2.054715 (steps=5173, words/sec=11685.08, time=0-00:20:30)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 17.0000 dev BLEU4: 0.33759971909724634, 0.654678/0.441285/0.299323/0.212121 (BP = 0.917349, ratio=0.92, hyp_len=11928, ref_len=12957) (time=0-00:21:06)
[medical.syl.en-my]              dev auxiliary GLEU: 0.353930
[medical.syl.en-my]              dev auxiliary Loss: 2.921 (ref_len=12957)
             checkpoint took 0-00:00:35
[medical.syl.en-my] Epoch 17.0035: train_loss/word=1.819227 (steps=5174, words/sec=14128.11, time=0-00:21:06)
[medical.syl.en-my] Epoch 17.0780: train_loss/word=1.952232 (steps=5199, words/sec=11323.47, time=0-00:21:09)
[medical.syl.en-my] Epoch 17.1526: train_loss/word=1.953578 (steps=5223, words/sec=12727.50, time=0-00:21:11)
[medical.syl.en-my] Epoch 17.2263: train_loss/word=1.963069 (steps=5245, words/sec=12669.00, time=0-00:21:13)
[medical.syl.en-my] Epoch 17.3023: train_loss/word=1.988894 (steps=5267, words/sec=11986.98, time=0-00:21:15)
[medical.syl.en-my] Epoch 17.3772: train_loss/word=1.890124 (steps=5286, words/sec=12688.80, time=0-00:21:17)
[medical.syl.en-my] Epoch 17.4515: train_loss/word=1.965508 (steps=5310, words/sec=11400.51, time=0-00:21:20)
[medical.syl.en-my] Epoch 17.5287: train_loss/word=1.923171 (steps=5332, words/sec=13574.55, time=0-00:21:22)
[medical.syl.en-my] Epoch 17.6040: train_loss/word=2.014063 (steps=5357, words/sec=11610.65, time=0-00:21:24)
[medical.syl.en-my] Epoch 17.6811: train_loss/word=2.003048 (steps=5380, words/sec=11776.21, time=0-00:21:27)
[medical.syl.en-my] Epoch 17.7553: train_loss/word=1.984107 (steps=5403, words/sec=12130.15, time=0-00:21:29)
[medical.syl.en-my] Epoch 17.8312: train_loss/word=1.987220 (steps=5425, words/sec=12125.07, time=0-00:21:31)
[medical.syl.en-my] Epoch 17.9051: train_loss/word=1.958663 (steps=5448, words/sec=11001.12, time=0-00:21:34)
[medical.syl.en-my] Epoch 17.9829: train_loss/word=2.030871 (steps=5472, words/sec=12558.99, time=0-00:21:36)
[medical.syl.en-my] Epoch 18.0000: train_loss/word=2.142120 (steps=5479, words/sec=8578.63, time=0-00:21:37)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 18.0000 dev BLEU4: 0.348276483708428, 0.637111/0.432975/0.298439/0.213460 (BP = 0.956558, ratio=0.96, hyp_len=12406, ref_len=12957) (time=0-00:22:13)
[medical.syl.en-my]              dev auxiliary GLEU: 0.358470
[medical.syl.en-my]              dev auxiliary Loss: 2.916 (ref_len=12957)
             checkpoint took 0-00:00:36
  new learning rate: 0.5
[medical.syl.en-my] Epoch 18.0041: train_loss/word=1.785648 (steps=5480, words/sec=16132.88, time=0-00:22:14)
[medical.syl.en-my] Epoch 18.0801: train_loss/word=1.792592 (steps=5500, words/sec=12786.55, time=0-00:22:15)
[medical.syl.en-my] Epoch 18.1556: train_loss/word=1.815709 (steps=5523, words/sec=12488.93, time=0-00:22:18)
[medical.syl.en-my] Epoch 18.2312: train_loss/word=1.904288 (steps=5548, words/sec=11287.14, time=0-00:22:20)
[medical.syl.en-my] Epoch 18.3061: train_loss/word=1.861056 (steps=5570, words/sec=12298.13, time=0-00:22:22)
[medical.syl.en-my] Epoch 18.3815: train_loss/word=1.849769 (steps=5592, words/sec=13123.11, time=0-00:22:25)
[medical.syl.en-my] Epoch 18.4553: train_loss/word=1.855886 (steps=5614, words/sec=12684.96, time=0-00:22:27)
[medical.syl.en-my] Epoch 18.5329: train_loss/word=1.857755 (steps=5637, words/sec=12272.78, time=0-00:22:29)
[medical.syl.en-my] Epoch 18.6087: train_loss/word=1.880363 (steps=5662, words/sec=11820.62, time=0-00:22:32)
[medical.syl.en-my] Epoch 18.6844: train_loss/word=1.843506 (steps=5684, words/sec=12998.24, time=0-00:22:34)
[medical.syl.en-my] Epoch 18.7597: train_loss/word=1.933848 (steps=5710, words/sec=10741.20, time=0-00:22:37)
[medical.syl.en-my] Epoch 18.8378: train_loss/word=1.904873 (steps=5735, words/sec=11794.21, time=0-00:22:39)
[medical.syl.en-my] Epoch 18.9122: train_loss/word=1.895218 (steps=5757, words/sec=11529.55, time=0-00:22:42)
[medical.syl.en-my] Epoch 18.9876: train_loss/word=1.805952 (steps=5778, words/sec=13884.97, time=0-00:22:44)
[medical.syl.en-my] Epoch 19.0000: train_loss/word=2.018422 (steps=5783, words/sec=11051.14, time=0-00:22:44)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 19.0000 dev BLEU4: 0.35011939243601775, 0.657258/0.446876/0.305775/0.218081 (BP = 0.935902, ratio=0.94, hyp_len=12152, ref_len=12957) (time=0-00:23:19)
[medical.syl.en-my]              dev auxiliary GLEU: 0.365076
[medical.syl.en-my]              dev auxiliary Loss: 2.903 (ref_len=12957)
             checkpoint took 0-00:00:34
  new learning rate: 0.25
[medical.syl.en-my] Epoch 19.0042: train_loss/word=1.658584 (steps=5784, words/sec=19355.34, time=0-00:23:19)
[medical.syl.en-my] Epoch 19.0807: train_loss/word=1.736440 (steps=5806, words/sec=13106.81, time=0-00:23:21)
[medical.syl.en-my] Epoch 19.1589: train_loss/word=1.807006 (steps=5829, words/sec=13013.12, time=0-00:23:23)
[medical.syl.en-my] Epoch 19.2330: train_loss/word=1.758344 (steps=5851, words/sec=13208.30, time=0-00:23:25)
[medical.syl.en-my] Epoch 19.3078: train_loss/word=1.738429 (steps=5874, words/sec=13242.79, time=0-00:23:28)
[medical.syl.en-my] Epoch 19.3817: train_loss/word=1.817417 (steps=5897, words/sec=12095.88, time=0-00:23:30)
[medical.syl.en-my] Epoch 19.4553: train_loss/word=1.845529 (steps=5920, words/sec=12205.73, time=0-00:23:32)
[medical.syl.en-my] Epoch 19.5311: train_loss/word=1.821739 (steps=5946, words/sec=11533.90, time=0-00:23:35)
[medical.syl.en-my] Epoch 19.6050: train_loss/word=1.822337 (steps=5969, words/sec=11179.02, time=0-00:23:38)
[medical.syl.en-my] Epoch 19.6797: train_loss/word=1.718418 (steps=5988, words/sec=14086.29, time=0-00:23:39)
[medical.syl.en-my] Epoch 19.7544: train_loss/word=1.831908 (steps=6012, words/sec=9978.65, time=0-00:23:42)
[medical.syl.en-my] Epoch 19.8295: train_loss/word=1.820122 (steps=6038, words/sec=11357.12, time=0-00:23:45)
[medical.syl.en-my] Epoch 19.9050: train_loss/word=1.807687 (steps=6061, words/sec=11459.17, time=0-00:23:47)
[medical.syl.en-my] Epoch 19.9817: train_loss/word=1.714277 (steps=6081, words/sec=14881.46, time=0-00:23:49)
[medical.syl.en-my] Epoch 20.0000: train_loss/word=1.853978 (steps=6087, words/sec=9997.47, time=0-00:23:50)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 20.0000 dev BLEU4: 0.3576129113504674, 0.651159/0.442721/0.305935/0.220157 (BP = 0.958006, ratio=0.96, hyp_len=12424, ref_len=12957) (time=0-00:24:26)
[medical.syl.en-my]              dev auxiliary GLEU: 0.369846
[medical.syl.en-my]              dev auxiliary Loss: 2.896 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
[medical.syl.en-my] Epoch 20.0057: train_loss/word=1.511653 (steps=6088, words/sec=15058.16, time=0-00:24:29)
[medical.syl.en-my] Epoch 20.0804: train_loss/word=1.705625 (steps=6108, words/sec=14004.98, time=0-00:24:31)
[medical.syl.en-my] Epoch 20.1595: train_loss/word=1.746556 (steps=6133, words/sec=11631.13, time=0-00:24:33)
[medical.syl.en-my] Epoch 20.2341: train_loss/word=1.718253 (steps=6154, words/sec=10841.94, time=0-00:24:35)
[medical.syl.en-my] Epoch 20.3099: train_loss/word=1.718538 (steps=6176, words/sec=12955.44, time=0-00:24:37)
[medical.syl.en-my] Epoch 20.3840: train_loss/word=1.809958 (steps=6201, words/sec=11473.62, time=0-00:24:40)
[medical.syl.en-my] Epoch 20.4579: train_loss/word=1.786267 (steps=6225, words/sec=11396.84, time=0-00:24:43)
[medical.syl.en-my] Epoch 20.5319: train_loss/word=1.803707 (steps=6248, words/sec=10591.62, time=0-00:24:45)
[medical.syl.en-my] Epoch 20.6065: train_loss/word=1.740303 (steps=6269, words/sec=12745.87, time=0-00:24:47)
[medical.syl.en-my] Epoch 20.6822: train_loss/word=1.748449 (steps=6291, words/sec=12305.35, time=0-00:24:49)
[medical.syl.en-my] Epoch 20.7574: train_loss/word=1.791710 (steps=6314, words/sec=12360.06, time=0-00:24:52)
[medical.syl.en-my] Epoch 20.8317: train_loss/word=1.744807 (steps=6336, words/sec=13250.90, time=0-00:24:54)
[medical.syl.en-my] Epoch 20.9069: train_loss/word=1.783588 (steps=6361, words/sec=12267.86, time=0-00:24:56)
[medical.syl.en-my] Epoch 20.9823: train_loss/word=1.819895 (steps=6387, words/sec=11016.56, time=0-00:24:59)
[medical.syl.en-my] Epoch 21.0000: train_loss/word=1.857592 (steps=6393, words/sec=10553.82, time=0-00:25:00)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 21.0000 dev BLEU4: 0.36375391673239676, 0.647598/0.440523/0.304478/0.221674 (BP = 0.976497, ratio=0.98, hyp_len=12656, ref_len=12957) (time=0-00:25:38)
[medical.syl.en-my]              dev auxiliary GLEU: 0.372705
[medical.syl.en-my]              dev auxiliary Loss: 2.907 (ref_len=12957)
             checkpoint took 0-00:00:37
  best dev score, writing out model
[medical.syl.en-my] Epoch 21.0021: train_loss/word=1.842596 (steps=6394, words/sec=9694.54, time=0-00:25:41)
[medical.syl.en-my] Epoch 21.0780: train_loss/word=1.745794 (steps=6419, words/sec=11302.02, time=0-00:25:44)
[medical.syl.en-my] Epoch 21.1521: train_loss/word=1.718242 (steps=6441, words/sec=13098.95, time=0-00:25:46)
[medical.syl.en-my] Epoch 21.2280: train_loss/word=1.713376 (steps=6461, words/sec=12915.82, time=0-00:25:48)
[medical.syl.en-my] Epoch 21.3048: train_loss/word=1.695708 (steps=6483, words/sec=12599.22, time=0-00:25:50)
[medical.syl.en-my] Epoch 21.3812: train_loss/word=1.728886 (steps=6505, words/sec=11471.32, time=0-00:25:52)
[medical.syl.en-my] Epoch 21.4565: train_loss/word=1.739670 (steps=6530, words/sec=11430.41, time=0-00:25:55)
[medical.syl.en-my] Epoch 21.5305: train_loss/word=1.752269 (steps=6552, words/sec=12545.80, time=0-00:25:57)
[medical.syl.en-my] Epoch 21.6043: train_loss/word=1.789362 (steps=6575, words/sec=11864.65, time=0-00:25:59)
[medical.syl.en-my] Epoch 21.6787: train_loss/word=1.774606 (steps=6600, words/sec=10668.86, time=0-00:26:02)
[medical.syl.en-my] Epoch 21.7540: train_loss/word=1.755943 (steps=6623, words/sec=12024.45, time=0-00:26:05)
[medical.syl.en-my] Epoch 21.8278: train_loss/word=1.746289 (steps=6645, words/sec=11007.61, time=0-00:26:07)
[medical.syl.en-my] Epoch 21.9025: train_loss/word=1.764884 (steps=6668, words/sec=10848.19, time=0-00:26:09)
[medical.syl.en-my] Epoch 21.9765: train_loss/word=1.766709 (steps=6690, words/sec=12633.42, time=0-00:26:12)
[medical.syl.en-my] Epoch 22.0000: train_loss/word=1.808633 (steps=6698, words/sec=10585.96, time=0-00:26:13)
> Checkpoint [medical.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.en-my] Epoch 22.0000 dev BLEU4: 0.3635562261340307, 0.647345/0.444730/0.308158/0.223528 (BP = 0.968806, ratio=0.97, hyp_len=12559, ref_len=12957) (time=0-00:26:50)
[medical.syl.en-my]              dev auxiliary GLEU: 0.371236
[medical.syl.en-my]              dev auxiliary Loss: 2.913 (ref_len=12957)
             checkpoint took 0-00:00:37
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.syl.en-my             | BLEU4: 0.36375391673239676, 0.647598/0.440523/0.304478/0.221674 (BP = 0.976497, ratio=0.98, hyp_len=12656, ref_len=12957)
                              | GLEU: 0.372705
                              | WER: 58.85% ( C/S/I/D: 7057/3874/1725/2026; hyp_len=12656, ref_len=12957 )
                              | CER: 53.36% ( C/S/I/D: 22375/8440/5053/6325; hyp_len=35868, ref_len=37140 )
                              | BLEU4: 0.3669128759686029, 0.652303/0.443451/0.307870/0.220885 (BP = 0.979729, ratio=0.98, hyp_len=13135, ref_len=13404)
                              | GLEU: 0.376249
                              | WER: 58.39% ( C/S/I/D: 7325/4063/1747/2016; hyp_len=13135, ref_len=13404 )
                              | CER: 53.03% ( C/S/I/D: 23025/9022/5043/6233; hyp_len=37090, ref_len=38280 )

real	28m17.790s
user	28m16.641s
sys	0m2.399s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

## Check the hyp

test hyp ဖိုင် ရဲ့ ထိပ်ဆုံး စာကြောင်း ၁၀ကြောင်း...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ head ./hyp/medical.syl.en-my.test.my 
လူ နာ က မ ကျေ နပ် ပါ ဘူး ပြီး တော့ သူ မ က ခင် ဗျား ကို တိုင် တန်း ခဲ့ တယ် ။
ခင် ဗျား ရဲ့ ညာ ဘက် ခြမ်း မှာ ခန္ဓာ ကိုယ် လှုပ် ရှား မှု တွေ နဲ့ တူ ညီ တဲ့ ပြ ဿ နာ တွေ ရှိ တယ် ။
ခင် ဗျား စိတ် ကြွ ဆေး တွေ ကို အ သုံး ပြု ပါ သ လား ။
ကု သ မှု က ခွဲ စိတ် ခြင်း က ခွဲ စိတ် မှု များ ကို လျော့ ကျ စေ ပါ တယ် ။
ဟမ် ။ တ ချို့ က လေး တွေ က ဘာ ကို မ ကြိုက် ဘူး ပြီး တော့ သွား ပိုး ဝင် တာ မ ရှိ သေး ဘူး ပြီး တော့ သွား ပိုး ပေါက် တွေ မ ရှိ သေး ဘူး ။
ဦး နှောက် အ တွင်း ရှိ အ ဖွဲ့ ကို ညွှန် ပြ တဲ့ အ ရာ က ဘာ လဲ ။
ကောင်း ပြီ ၊ အား က စား ရုံ ။
ကောင်း ပြီ ။ ကျွန် တော့် မျက် လုံး တွေ က ဘာ လို့ ဒီ လောက် ပဲ ဖြစ် နေ တာ လဲ ။
ခင် ဗျား မှာ အ ချိန် အ ချို့ ရှိ ရင် ၊ ခင် ဗျား ကျွန် တော့် ကို သူ ငယ် ချင်း တွေ နဲ့ အ တူ ခင် ဗျား အ ပြင် ထွက် လာ လို့ ရ တယ် ၊ ကျွန် တော် တို့ က အဲ ဒီ လို ဆို ရင် တော့ ကျွန် တော် တို့ က အဲ ဒီ လို ဆို တာ ကို ရပ် ဖို့ စီ စ ဥ် နေ တယ် ။
ကျွန် တော် မ သေ ချာ ပေ မဲ့ ဆီး လမ်း ကြောင်း ပိုး ဝင် ခြင်း ၊ ဆီး လမ်း ကြောင်း ပိုး ဝင် ခြင်း ၊ အက်စ် တီ ဒီ ကူး စက် ခြင်း ၊ အက်စ် တီ ဒီ ကူး စက် ခြင်း ၊ အက်စ် တီ ဒီ ကူး စက် မှု အ နည်း ငယ် ပဲ ဖြစ် ပါ တယ် ။
```

input ဖိုင်နဲ့ အထက်က မော်ဒယ်က ဘာသာပြန်ပြီးထွက်လာတဲ့ စာကြောင်းတွေကို နှိုင်းယှဉ်ကြည့်...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ head ./data/test.en
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
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

## Training (syl, my-en)

