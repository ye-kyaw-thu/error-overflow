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

```yaml

```

```yaml

```

## Training

### for en-th, word unit

### for th-en, word unit

