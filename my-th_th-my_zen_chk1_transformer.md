# my-th, th-my Zen-Data Checked-1 NMT

Date: 2 July 2024.  

## Data Preparation

path: /home/ye/exp/nmt/my-th/data/zen  

ပထမဆုံး Experiment အနေနဲ့ Zen ဆီက ဒေတာကိုပဲ သုံးပြီး baseline ထုတ်ထားမယ်။  

/home/ye/exp/nmt/my-th/data/zen/4hayman  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$ wc *
   80626   995689  9261619 my-mahidol.txt
   80626   566563  6589494 th-mahidol.txt
  161252  1562252 15851113 total
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$
```

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$ head ./my-mahidol.txt
my
အ နာ ပတ် လည် ကို သ န့် ရှင်း ရေး လုပ် ပါ
ကျွန် တော် ပင် လယ် ထဲ မှာ ရေ ဆော့ နေ ခဲ့ တယ် ။
ဓာတ် မ တ ည့် မှု ကြော င့် နှာ ခေါင်း ပေါက် ထဲ က မြူး ကပ် လွှာ‌ ရောင် ရမ်း ခြင်း ။
ဒီ လို လက္ခ ဏာ ဖြစ် နေ တာ 2 ရက် လောက် တော့ ရှိ ပါ ပြီ
သူ့ ပါး ပြင် မှာ ဖောင်း ရောင် ပြီး နာ ကျင် နေ တယ် ။
အ ချိန် မှီ ပစ္စည်း မ ရောက် လို့ က တော့ ငွေ ဖြတ် ခံ ရ ပါ တယ်
ဘယ် လောက် လောက် လွဲ ရ မ လဲ ရှင်
မွေး ခါ စ က လေး နဲ့ ငယ် ငယ် လေး တွေ မှာ‌ တော့ မ ရှိ တတ် ပါ ဘူး ။
အ သက် ရှု တဲ့ ပိုက် တပ် ထား ပါ တယ် ။
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$
```

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$ head ./th-mahidol.txt
th
ทำ ความ สะอาด ริม ขอบ แผล
ผม เล่น น้ำ ใน ทะเล ครับ
โรค จมูก อักเสบ จาก ภูมิ แพ้
มี อาการ เมื่อ 2 วัน ที่ แล้ว
แก้ม ของ เขา บวม และ เจ็บ
ถ้า ส่ง ไม่ ทัน จะ ไม่ ได้ เงิน ครับ
ต้อง แกว่ง แบบ นี้ กี่ ครั้ง คะ
ใน ทารก หรือ เด็ก จะ ไม่ เจอ อาการ ไอ
หมอ ใส่ ท่อ ช่วย หายใจ ให้
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/4hayman$
```

Copy ကူးပြီး data splitting လုပ်မယ် ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen$ mkdir preprocess
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen$ cp ./4hayman/*.txt ./preprocess/
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen$ cd preprocess/
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ ls
my-mahidol.txt  th-mahidol.txt
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$
```

ZWNJ, ZWSP, HSP စတာတွေကို cleaning လုပ်ခဲ့...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ python ./rm_zwnj_zwsp_hsp.py --input my-mahidol.txt --output my-mahidol.txt.clean1
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ python ./rm_zwnj_zwsp_hsp.py --input ./th-mahidol.txt --output th-mahidol.txt.clean1
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$

```

Paste လုပ်ခဲ့ ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ paste ./my-mahidol.txt.clean1 ./th-mahidol.txt.clean1 > myth.all.txt
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ wc myth.all.txt
   80626  1561976 15837717 myth.all.txt
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$
```

Checking the output ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ head myth.all.txt
my      th
အ နာ ပတ် လည် ကို သ န့် ရှင်း ရေး လုပ် ပါ        ทำ ความ สะอาด ริม ขอบ แผล
ကျွန် တော် ပင် လယ် ထဲ မှာ ရေ ဆော့ နေ ခဲ့ တယ် ။  ผม เล่น น้ำ ใน ทะเล ครับ
ဓာတ် မ တ ည့် မှု ကြော င့် နှာ ခေါင်း ပေါက် ထဲ က မြူး ကပ် လွှာ ရောင် ရမ်း ခြင်း ။        โรค จมูก อักเสบ จาก ภูมิ แพ้
ဒီ လို လက္ခ ဏာ ဖြစ် နေ တာ 2 ရက် လောက် တော့ ရှိ ပါ ပြီ   มี อาการ เมื่อ 2 วัน ที่ แล้ว
သူ့ ပါး ပြင် မှာ ဖောင်း ရောင် ပြီး နာ ကျင် နေ တယ် ။     แก้ม ของ เขา บวม และ เจ็บ
အ ချိန် မှီ ပစ္စည်း မ ရောက် လို့ က တော့ ငွေ ဖြတ် ခံ ရ ပါ တယ်    ถ้า ส่ง ไม่ ทัน จะ ไม่ ได้ เงิน ครับ
ဘယ် လောက် လောက် လွဲ ရ မ လဲ ရှင် ต้อง แกว่ง แบบ นี้ กี่ ครั้ง คะ
မွေး ခါ စ က လေး နဲ့ ငယ် ငယ် လေး တွေ မှာ တော့ မ ရှိ တတ် ပါ ဘူး ။ ใน ทารก หรือ เด็ก จะ ไม่ เจอ อาการ ไอ
အ သက် ရှု တဲ့ ပိုက် တပ် ထား ပါ တယ် ။    หมอ ใส่ ท่อ ช่วย หายใจ ให้
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$
```

Removed header, pote-htee (3463), pote-ma (45408), 

```

```

## Noted Error or Concern Examples

```
ကျုပ် က လေး က စိတ် က စ ဥ့် က လျား ဖြစ် နေ ပြီ 	ใจ ของ ลูก ฉัน แปรนปวน
F a v i p i r a v i r	Favipiravir
ကျွန် တော် တို့ က ထို သူ တွေ ကို C O V I D - 1 9 ရော ဂါ ရှိ သူ နဲ့ ထိ တွေ့ ခဲ့ တယ်	เรา จะ แจ้ง ให้ พวก เขา ทราบ ว่า พวก อาจ ได้ รับ เชื้อ COVID -19 เมื่อ เร็ว ๆ นี้ และ เช็ค อิน กับ พวก เขา เกี่ยว กับ อาการ ใด ๆ ที่ พวก เขา อาจ มี และ ส่ง ต่อ พวก เขา ไป ยัง การ ดูแล สุขภาพ หรือ แจ้ง ความ สำคัญ ของ การ กักตัว และ เฝ้า ระวัง อาการ เพื่อ ไม่ ให้ แพร่ไวรัส ไป ยัง ผู้ อื่น
ကျွန် မ ဆ ရာ ဝန် . . . . . . . . နဲ့ ပြ ဖို့ . . . . . . . . . မှာ ချိန်း ထား တာ ရှိ ပါ တယ် 	ดิฉัน มี นัด กับ คุณ หมอ … ตอน … โมง ค่ะ
N S A I D s များ	ยา กลุ่ม เอ็นเสด
ခ ဏ နေ တို့ ကတ် ယူ ပြီး လူ နာ မှတ် တမ်း ဖွ င့် ပေး ပါ မယ်	เดี๋ยว ดิฉัน จะ นำ บัตร ไป เปิด ประวัติ ให้
ပြင်း ထန် အ ဆ င့် လည်း ဖြစ် ပါ တယ် 	เป็น ระดับ รุนแรง
စမ်း ကြ ည့် ပါ မယ် 	ก็ ต้อง ลอง ดู ค่ะ
လွန် ခဲ့ တဲ့ နှစ် ရက် က အိမ် နာူ မှာ သင်္ဘော သီး ထောင်း ဆိုင် ဖွ င့် တာ နဲ့ သွား အား ပေး လိုက် တယ် ဗျာ	เมื่อ 2 วัน ก่อน มี ไป กิน ยำ ส้มตำร้าน เปิด ใหม่ แถว บ้าน มา ครับ
အ ဖျား တိုင်း ကြ ည့် သေး လား ရှ င့်	ไข้ สูง ได้ วัด อุณหภูมิ ไว้ บ้าง ไหม คะ
_ _ _ _ _ အ ချိန် အ ဆင် ပြေ နိုင် မ လား 	ขอ เป็น เวลา … ได้ ไหม
နောက် တစ် ခါ ပုံ စံ ခွက် အောက် ခံ ကို သီး သန့် လုပ် မယ်	อีก ที นึง
အို ဟိုး . .	โห
အင် . . .	อ๋อ
ဝမ်း ယူ သာ ပိုး စစ် ဆေး ချင် လို့ လား ခင် ဗျာ 	และ เก็บ อุจจาระ ส่ง ตรวจ หา เชื้อ นะ ครับ
သ မီး ဘယ် လို နေ လဲ ရှ င့် 	ลูก สาว เป็น อย่าง ไร บ้าง คะ
သ င့် ရဲ့ အ ပူ ချိန် က - - - - - ရှိ တယ် 	อุณหภูมิ ของ คุณ …
မိ နစ် ၃ ၀ လောက် ကြာ နိုင် ပါ လိ မ့် မယ် 	น่า จะ นาน 30 นาที
အ ကယ် ၍ ကြ ည့် ချင် ရင် မှန် မှာ ကြ ည့် လို့ ရ တယ် နော်	ถ้า อยาก ดู หยิบ กระจก ขึ้น มา ดู ได้ นะ
အ ဖက် တွေ လည်း ပါ တတ် တယ် 	มี เนื้อ ปน มา ด้วย
ညီ က အ ဖျား မြ င့် နေ မယ်	ผู้ ป่วย จะ มี ไข้ สูง
မ ရှိ ဘူး ရှ င့်	ไม่ มี เลย
နေ့ စ ဥ် စော င့် ကြ ည့် ရေး အ တွက် ကျွန် တော် တို့ မှာ < ဒေ သ ဆိုင် ရာ စော င့် ကြ ည့် ရေး	เรา มี < ชื่อ ระบบ ตรวจสอบ ใน พื้นที่ > เพื่อ ช่วย ใน การ เช็ค อิน ทุก วัน
ကျွန် တော့ သွေး က " A " သွေး ပါ 	กรุ๊ป เลือด ของ ผม คือ เอ ครับ
ပြ ည့် တင်း ပြီး အော င့် တာ မျိုး	ปวด จุก แน่น
သွေး ပေါင် ချိန် ၁ ၁ ၀ / ၆ ၄ ပါ	ความ ดัน เลือด 110 / 64 มิลลิเมตร ปรอท
န င့် ဖင် ကို သ န့် ရှင်း ရေး လုပ် ပါ 	คุณควร ล้าง ก้น กับ น้ำ อุ่น ให้ สะอาด
မ , ယား ပါ ဘူး ခင် ဗျာ	ไม่ คัน ครับ
အ ဆုတ် ကို x r a y ရိုက် ပါ 	เอ็กซเรย์ ปอด
အားး ဗိုက် တစ်် ပြင် လုံး နာ ကျင် နေ တာ ပဲ	โอ๊ย !!! ปวด ทั่ว ท้อง มาก คะ
အေ ၀း က အ ရာ ၀တ္ထု တွေ က ၀ါး နေ တယ် 	สิ่ง ที่ อยู่ ไกล ดู แล้ว เบลอ
အား… . နာ လိုက် တာ 	โอ๊ย ยยยย ปวด ๆ
သူ မ အ ပြင် အ ထန် ဖြစ် သ လား 	เขา ทำ รุง แรง ไหม
အ ပူ ချိန် က - - - - - ရှိ ပါ တယ် 	อุณหภูมิ ของ คุณ …
နာ မည် က . . . . . . . . . . . . . ဖြစ် တယ် ရှင်	ชื่อ .............. ค่ะ
```

အချိန်မရှိလို့ အကြမ်းစစ်ထားတဲ့ ဖိုင်ကို အောက်ပါဖိုင်နဲ့ သိမ်းခဲ့တယ်။  
myth.all.txt.rough-chk  

## Shuffling

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ shuf ./myth.all.txt.rough-chk > ./myth.all.txt.rough-chk.shuf
```

## Splint Train/Valid/Test

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ tail -n 8000 ./myth.all.txt.rough-chk.shuf > myth.test
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ head -n 72625 ./myth.all.txt.rough-chk.shuf | tail -n 10000 > ./myth.dev
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ head -n 62625 ./myth.all.txt.rough-chk.shuf > ./myth.train
```

Check filesize ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ wc myth.{train,dev,test}
   62625  1174178 12178653 myth.train
   10000   188897  1959078 myth.dev
    8000   150032  1553364 myth.test
   80625  1513107 15691095 total
```

Split source/target ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ mkdir final
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f1 ./myth.train > ./final/train.my
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f2 ./myth.train > ./final/
train.th
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f1 ./myth.dev > ./final/de
v.my
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f2 ./myth.dev > ./final/de
v.th
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f1 ./myth.test > ./final/t
est.my
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cut -f2 ./myth.test > ./final/t
est.th
```

Check filesize ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess$ cd final
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/preprocess/final$ wc *
   10000   117884  1133121 dev.my
   10000    71013   825957 dev.th
    8000    93919   901455 test.my
    8000    56113   651909 test.th
   62625   734742  7067941 train.my
   62625   439436  5110712 train.th
  161250  1513107 15691095 total
```

Copying ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen$ mkdir chk1
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen$ cd chk1
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1$ cp ../preprocess/final/* .
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1$ ls
dev.my  dev.th  test.my  test.th  train.my  train.th
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1$
```

## Vocab File Building  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1$ cat train.my dev.my > ./vocab/train-dev.my
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1$ cat train.th dev.th > ./vocab/train-dev.th
```

Check filesize ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ wc *
   72625   852626  8201062 train-dev.my
   72625   510449  5936669 train-dev.th
  145250  1363075 14137731 total
```

Vocab building for Myanmar ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ time marian-vocab < ./train-dev
.my > vocab.my.yml
[2024-07-02 03:17:33] Creating vocabulary...
[2024-07-02 03:17:33] [data] Creating vocabulary stdout from stdin
[2024-07-02 03:17:33] Finished

real    0m0.271s
user    0m0.238s
sys     0m0.008s
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

Vocab building for Thai ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ time marian-vocab < ./train-dev.th > vocab.th.yml
[2024-07-02 03:17:54] Creating vocabulary...
[2024-07-02 03:17:54] [data] Creating vocabulary stdout from stdin
[2024-07-02 03:17:54] Finished

real    0m0.228s
user    0m0.228s
sys     0m0.001s
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

Check vocab files ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ head -n 30 ./vocab.my.yml
</s>: 0
<unk>: 1
အ: 2
ပါ: 3
တယ်: 4
မ: 5
တာ: 6
က: 7
နေ: 8
ကို: 9
ရ: 10
နာ: 11
တွေ: 12
ဖြစ်: 13
ပြီး: 14
တော့: 15
သ: 16
မယ်: 17
မှာ: 18
တဲ့: 19
င့်: 20
ရှိ: 21
လား: 22
ရင်: 23
လို့: 24
ဘူး: 25
ဆေး: 26
သွား: 27
လာ: 28
လဲ: 29
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ tail -n 30 ./vocab.my.yml
အာင်: 2090
အားးး: 2091
အားးးး: 2092
အာြ: 2093
အာ……: 2094
အိုး…: 2095
အို…: 2096
အီးးး: 2097
အူမ်း: 2098
အူး: 2099
အူးးး: 2100
အေင်: 2101
အေုင်: 2102
အေ့ာ: 2103
အးင်: 2104
အြော်: 2105
အွမ်: 2106
အွမ်း…: 2107
အွီး: 2108
အ…: 2109
ဥက္က: 2110
ဥ◌်: 2111
ဦ: 2112
ဦီး: 2113
ါာ: 2114
၀ီီ: 2115
၀ေး: 2116
၍့်: 2117
၍၎င်း: 2118
“: 2119(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

vocab size for Myanmar language ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ wc vocab.my.yml
 2119  4240 37985 vocab.my.yml
```

အထက်ပါအတိုင်း ဒေတာကို cleaning လုပ်ရမယ် ဆိုတာကို တွေ့ရလိမ့်မယ်။  

Let's check for the Thai side ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ head -n 30 ./vocab.th.yml
</s>: 0
<unk>: 1
ครับ: 2
มี: 3
ไม่: 4
ที่: 5
ได้: 6
จะ: 7
คะ: 8
นะ: 9
ค่ะ: 10
เป็น: 11
มา: 12
ให้: 13
คุณ: 14
ผม: 15
การ: 16
หมอ: 17
แล้ว: 18
ไหม: 19
ไป: 20
นี้: 21
และ: 22
อาการ: 23
เลย: 24
ๆ: 25
ของ: 26
ไข้: 27
หรือ: 28
ใน: 29
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

with tail command ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ tail -n 30 ./vocab.th.yml
ลงลายมือ: 4390
ลิ้นไก่: 4391
ศี: 4392
สกัดกั้น: 4393
สนาม: 4394
สไปโรเมทรีย์: 4395
หนองปะปน: 4396
หมวก: 4397
หมอจ่ายยาFavipiravir,Dextrometrophen: 4398
หัวใจวาย: 4399
หิย: 4400
องค์การอนามัยโลก: 4401
อวัยะเพศ: 4402
ออกตัว: 4403
เจ็บปวดร้าว: 4404
เรียบอร์ดเดเทลลา: 4405
เสลด: 4406
เหล็บขาว: 4407
เอออร์ติก: 4408
เอ็นเสด: 4409
แคลเซียม: 4410
แค๊ก: 4411
แรกเลี้ยว: 4412
โหนก: 4413
โอะ: 4414
ใส้ติ่ง: 4415
ไดนามิค: 4416
ไหปลาร้า: 4417
ไหมหมอ: 4418
ไหม้วอด: 4419(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$
```

Let's check vocab filesize for Thai side ... 

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/data/zen/chk1/vocab$ wc ./vocab.th.yml
 4419  8840 98729 ./vocab.th.yml
```

Vocab file path is "/home/ye/exp/nmt/my-th/data/zen/chk1/vocab".  

## Config File for Transformer

(base) ye@lst-hpc3090:~/exp/nmt/my-th$ cat ./tf.myth.zen.chk1.sh  

```
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for my-th with Zen data checked-1

## Old Notes
#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir zen-chk1/model.tf.myth;

marian \
    --model zen-chk1/model.tf.myth/model.npz --type transformer \
    --train-sets /home/ye/exp/nmt/my-th/data/zen/chk1/train.my \
    /home/ye/exp/nmt/my-th/data/zen/chk1/train.th \
    --max-length 200 \
    --vocabs /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.my.yml \
    /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.th.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /home/ye/exp/nmt/my-th/data/zen/chk1/dev.my \
    /home/ye/exp/nmt/my-th/data/zen/chk1/dev.th \
    --valid-translation-output zen-chk1/model.tf.myth/valid.my-th.output \
    --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log zen-chk1/model.tf.myth/train.log \
    --valid-log zen-chk1/model.tf.myth/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > zen-chk1/model.tf.myth/my-th.config.yml

time marian -c zen-chk1/model.tf.myth/my-th.config.yml  2>&1 | tee zen-chk1/model.tf.myth/transformer-myth.log

```

## Training Transformer  

လက်ရှိ server မှာ coda ကို သုံးလို့မရဘူး... လိုင်စင်ပြဿနာကြောင့် ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th$ ./tf.myth.zen.chk1.sh
...
...
...
[2024-07-02 04:08:46] Saving model weights and runtime parameters to zen-chk1/model.tf.myth/model.iter100000.npz
[2024-07-02 04:08:46] Saving model weights and runtime parameters to zen-chk1/model.tf.myth/model.npz
[2024-07-02 04:08:47] Saving Adam parameters
[2024-07-02 04:08:47] [training] Saving training checkpoint to zen-chk1/model.tf.myth/model.npz and zen-chk1/model.tf.myth/model.npz.optimizer.npz
[2024-07-02 04:08:48] [valid] Ep. 212 : Up. 100000 : cross-entropy : 2.3861 : stalled 10 times (last best: 2.24612)
[2024-07-02 04:08:49] [valid] Ep. 212 : Up. 100000 : perplexity : 1.3425 : stalled 10 times (last best: 1.3195)
[2024-07-02 04:08:53] [valid] Ep. 212 : Up. 100000 : bleu : 86.4593 : new best
[2024-07-02 04:08:53] Training finished
[2024-07-02 04:08:53] Saving model weights and runtime parameters to zen-chk1/model.tf.myth/model.npz
[2024-07-02 04:08:53] Saving Adam parameters
[2024-07-02 04:08:54] [training] Saving training checkpoint to zen-chk1/model.tf.myth/model.npz and zen-chk1/model.tf.myth/model.npz.optimizer.npz

real    25m16.856s
user    26m14.617s
sys     1m11.299s
```

Check models ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$ ls
model.iter100000.npz  model.iter45000.npz  model.iter80000.npz      model.npz.yml
model.iter10000.npz   model.iter50000.npz  model.iter85000.npz      my-th.config.yml
model.iter15000.npz   model.iter5000.npz   model.iter90000.npz      train.log
model.iter20000.npz   model.iter55000.npz  model.iter95000.npz      transformer-myth.log
model.iter25000.npz   model.iter60000.npz  model.npz                valid.log
model.iter30000.npz   model.iter65000.npz  model.npz.decoder.yml    valid.my-th.output
model.iter35000.npz   model.iter70000.npz  model.npz.optimizer.npz
model.iter40000.npz   model.iter75000.npz  model.npz.progress.yml
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$
```

## Testing Transformer for my-th

ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$ cat ./test-eval.sh

```bash
(base) #!/bin/bash

for i in {5000..100000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.my.yml /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.th.yml --devices 0 --output hyp.iter$i.th < /home/ye/exp/nmt/my-th/data/zen/chk1/test.my;
    echo "Evaluation with hyp.iter$i.th, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /home/ye/exp/nmt/my-th/data/zen/chk1/test.th < ./hyp.iter$i.th >> eval-result.txt;

done
```

/home/ye/exp/nmt/my-th/zen-chk1/model.tf.myth

Testing ...  

```
ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$ time ./test-eval.sh
...
...
[2024-07-02 05:28:56] Best translation 7986 : ก่อนหน้า นนี้ ก็ เดิน ได้ เกือบ ปกติ นะ คะ
[2024-07-02 05:28:56] Best translation 7987 : หนู ขขี่ รถ มอเตอร์ไซด์ ออก จาก บ้าน
[2024-07-02 05:28:56] Best translation 7988 : เรา มี วิธี การ บาง อย่าง ทที่ คุณ สามารถ รักษา อาการ ของ คุณ ทที่ บ้าน ได้
[2024-07-02 05:28:56] Best translation 7989 : คน ไข้ มา ด้วย อาการ อะไร คะ
[2024-07-02 05:28:56] Best translation 7990 : เออ
[2024-07-02 05:28:56] Best translation 7991 : ตัว แข็ง มา ค่ะ
[2024-07-02 05:28:56] Best translation 7992 : ต้อง อยยู่ ภาย ใต้ การ ดูแล อย่าง ใกล้ชิด ของ แพทย์ และ ผผู้ เชชี่ยวชาญ
[2024-07-02 05:28:56] Best translation 7993 : แล้ว ปวด บริเวณ ไหน ของ ท้อง
[2024-07-02 05:28:56] Best translation 7994 : ฝาก ครรภ์
[2024-07-02 05:28:56] Best translation 7995 : ผม ไม่ ขับ รถ ไป สัก พัก เลย
[2024-07-02 05:28:56] Best translation 7996 : ไม่ มี ใคร เคย ถาม ว่า หนู เป็น อะไร ด้วยซ้ำ
[2024-07-02 05:28:56] Best translation 7997 : มี อาการ อย่าง ออื่น ๆ
[2024-07-02 05:28:56] Best translation 7998 : ตาม ทที่ หมอ เคย อธิบาย
[2024-07-02 05:28:56] Best translation 7999 : นนิ่ง ไว้ นะ คะ อย่า ขยับ จนกว่า จะ เดิน เข้า มา เอา ทที่ กัด ออก ให้ นะ คะ
[2024-07-02 05:28:56] Total time: 61.59620s wall

real    20m45.024s
user    19m22.182s
sys     1m31.261s
(base) 
```

Testing Result for Transformer, my-th with Zen data Chk-1:  
```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$ cat ./eval-result.txt
Evaluation with hyp.iter5000.th, Transformer model:
BLEU = 32.73, 70.0/51.2/40.9/34.9 (BP=0.688, ratio=0.728, hyp_len=40855, ref_len=56113)
Evaluation with hyp.iter10000.th, Transformer model:
BLEU = 64.42, 83.6/75.4/71.8/70.5 (BP=0.857, ratio=0.867, hyp_len=48633, ref_len=56113)
Evaluation with hyp.iter15000.th, Transformer model:
BLEU = 76.02, 87.5/82.3/80.5/80.3 (BP=0.920, ratio=0.923, hyp_len=51808, ref_len=56113)
Evaluation with hyp.iter20000.th, Transformer model:
BLEU = 80.46, 89.2/85.1/83.8/83.8 (BP=0.942, ratio=0.943, hyp_len=52933, ref_len=56113)
Evaluation with hyp.iter25000.th, Transformer model:
BLEU = 82.87, 90.0/86.4/85.4/85.6 (BP=0.955, ratio=0.956, hyp_len=53618, ref_len=56113)
Evaluation with hyp.iter30000.th, Transformer model:
BLEU = 84.00, 90.3/86.9/86.1/86.4 (BP=0.961, ratio=0.962, hyp_len=53963, ref_len=56113)
Evaluation with hyp.iter35000.th, Transformer model:
BLEU = 84.48, 90.5/87.2/86.4/86.8 (BP=0.963, ratio=0.964, hyp_len=54079, ref_len=56113)
Evaluation with hyp.iter40000.th, Transformer model:
BLEU = 85.00, 90.5/87.4/86.7/87.0 (BP=0.967, ratio=0.967, hyp_len=54285, ref_len=56113)
Evaluation with hyp.iter45000.th, Transformer model:
BLEU = 85.14, 90.6/87.4/86.7/87.1 (BP=0.968, ratio=0.968, hyp_len=54344, ref_len=56113)
Evaluation with hyp.iter50000.th, Transformer model:
BLEU = 85.54, 90.8/87.8/87.2/87.6 (BP=0.968, ratio=0.969, hyp_len=54359, ref_len=56113)
Evaluation with hyp.iter55000.th, Transformer model:
BLEU = 85.58, 90.8/87.8/87.1/87.6 (BP=0.969, ratio=0.969, hyp_len=54401, ref_len=56113)
Evaluation with hyp.iter60000.th, Transformer model:
BLEU = 85.69, 90.8/87.8/87.1/87.6 (BP=0.970, ratio=0.971, hyp_len=54479, ref_len=56113)
Evaluation with hyp.iter65000.th, Transformer model:
BLEU = 85.53, 90.7/87.7/87.0/87.5 (BP=0.969, ratio=0.970, hyp_len=54426, ref_len=56113)
Evaluation with hyp.iter70000.th, Transformer model:
BLEU = 85.76, 90.8/87.7/87.1/87.6 (BP=0.971, ratio=0.972, hyp_len=54523, ref_len=56113)
Evaluation with hyp.iter75000.th, Transformer model:
BLEU = 85.83, 90.8/87.8/87.1/87.6 (BP=0.972, ratio=0.972, hyp_len=54569, ref_len=56113)
Evaluation with hyp.iter80000.th, Transformer model:
BLEU = 85.84, 90.8/87.8/87.1/87.6 (BP=0.972, ratio=0.972, hyp_len=54561, ref_len=56113)
Evaluation with hyp.iter85000.th, Transformer model:
BLEU = 85.88, 90.8/87.8/87.1/87.6 (BP=0.972, ratio=0.973, hyp_len=54586, ref_len=56113)
Evaluation with hyp.iter90000.th, Transformer model:
BLEU = 85.92, 90.8/87.7/86.9/87.4 (BP=0.974, ratio=0.975, hyp_len=54691, ref_len=56113)
Evaluation with hyp.iter95000.th, Transformer model:
BLEU = 86.03, 90.9/87.8/87.1/87.6 (BP=0.974, ratio=0.974, hyp_len=54673, ref_len=56113)
Evaluation with hyp.iter100000.th, Transformer model:
BLEU = 86.05, 90.9/87.8/87.1/87.5 (BP=0.974, ratio=0.975, hyp_len=54695, ref_len=56113)
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.myth$
```

ရလဒ်က ကောင်းတယ်။ အရမ်းပျော်။  
data cleaning လုပ်လိုက်တာနဲ့ ဒေတာကို ထပ်ဖြည့်နိုင်ရင် သေချာပေါက် ရလဒ် လက်ရှိထက် ကောင်းနိုင်တယ်။ :)  

## Transformer Model, th-my, Zen Data Chk-1

Config File for Transformer, th-my ...  

(base) ye@lst-hpc3090:~/exp/nmt/my-th$ cat ./tf.thmy.zen.chk1.sh  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for th-my with Zen data checked-1
## Last updated: 2 July 2024

## Old Notes
#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir zen-chk1/model.tf.thmy;

marian \
    --model zen-chk1/model.tf.thmy/model.npz --type transformer \
    --train-sets /home/ye/exp/nmt/my-th/data/zen/chk1/train.th \
    /home/ye/exp/nmt/my-th/data/zen/chk1/train.my \
    --max-length 200 \
    --vocabs /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.th.yml \
    /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /home/ye/exp/nmt/my-th/data/zen/chk1/dev.th \
    /home/ye/exp/nmt/my-th/data/zen/chk1/dev.my \
    --valid-translation-output zen-chk1/model.tf.thmy/valid.th-my.output \
    --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log zen-chk1/model.tf.thmy/train.log \
    --valid-log zen-chk1/model.tf.thmy/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > zen-chk1/model.tf.thmy/th-my.config.yml

time marian -c zen-chk1/model.tf.thmy/th-my.config.yml  2>&1 | tee zen-chk1/model.tf.thmy/transformer-thmy.log

```

## Training, th-my, Zen Data Chk-1

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th$ ./tf.thmy.zen.chk1.sh
...
...
...
y/model.iter70000.npz
[2024-07-02 05:58:52] Saving model weights and runtime parameters to zen-chk1/model.tf.thmy/model.npz
[2024-07-02 05:58:52] Saving Adam parameters
[2024-07-02 05:58:52] [training] Saving training checkpoint to zen-chk1/model.tf.thmy/model.npz and zen-chk1/model.tf.thmy/model.npz.optimizer.npz
[2024-07-02 05:58:54] [valid] Ep. 171 : Up. 70000 : cross-entropy : 16.6502 : stalled 10 times (last best: 15.1045)
[2024-07-02 05:58:55] [valid] Ep. 171 : Up. 70000 : perplexity : 3.67656 : stalled 10 times (last best: 3.25797)
[2024-07-02 05:59:01] [valid] Ep. 171 : Up. 70000 : bleu : 47.2613 : stalled 6 times (last best: 47.789)
[2024-07-02 05:59:01] Training finished
[2024-07-02 05:59:01] Saving model weights and runtime parameters to zen-chk1/model.tf.thmy/model.npz
[2024-07-02 05:59:01] Saving Adam parameters
[2024-07-02 05:59:01] [training] Saving training checkpoint to zen-chk1/model.tf.thmy/model.npz and zen-chk1/model.tf.thmy/model.npz.optimizer.npz

real    20m29.484s
user    21m17.911s
sys     0m56.657s
```

check trained models ...  

```
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$ ls
model.iter10000.npz  model.iter40000.npz  model.iter65000.npz      model.npz.yml
model.iter15000.npz  model.iter45000.npz  model.iter70000.npz      th-my.config.yml
model.iter20000.npz  model.iter50000.npz  model.npz                train.log
model.iter25000.npz  model.iter5000.npz   model.npz.decoder.yml    transformer-thmy.log
model.iter30000.npz  model.iter55000.npz  model.npz.optimizer.npz  valid.log
model.iter35000.npz  model.iter60000.npz  model.npz.progress.yml   valid.th-my.output
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$
```

## Testing th-my, Transformer, Zen Chk-1

(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$ cat ./test-eval.sh  

```bash
(base) #!/bin/bash

for i in {5000..70000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v /home/ye/exp/nmt/my-th/data/zen/chk1/vocab/vo>    echo "Evaluation with hyp.iter$i.my, Transformer model:" >> eval-result.txt;
</home/ye/exp/nmt/my-th/data/zen/chk1/test.my < ./hyp.iter$i.my >> eval-result.txt;

done

```

Testing ...  

(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$ time ./test-eval.sh  

```
 [2024-07-02 06:25:49] Best translation 7988 : သ င့် ရရဲ့ အ ခြေ အ နေ ကကို အိမ် မှာ နေ ထထိုင် ရင်း ကု သ နနိုင် မမဲ့ နည်း လမ်း တ ချျိျို့ ကျွန် တော် တတိတို့ မှာ ရှိ ပါ တယ်
[2024-07-02 06:25:49] Best translation 7989 : လူ နာ အ ခြေ အ နေ ဘယ် လလို ရှိ သ လဲ
[2024-07-02 06:25:49] Best translation 7990 : ဪ
[2024-07-02 06:25:49] Best translation 7991 : ကကိုယ် က လည်း မာ တော င့် နေ တယ် ရှ င့်
[2024-07-02 06:25:49] Best translation 7992 : ဆ ရာ ဝန် တွေ အ ထူး ကု တွေ နနဲ့ သေ ချာ ကု သ တာ
[2024-07-02 06:25:49] Best translation 7993 : ဘယ် နား လောက် က လဲ ရှင့်
[2024-07-02 06:25:49] Best translation 7994 : ကကိုယ် ဝန် အပ် ပါ
[2024-07-02 06:25:49] Best translation 7995 : ကျွန် တော် ဒါ ပြီး တော့ အ တော် ကြာ တတဲ့ အ ထိ ကား မ မောင်း ဖြစ် ဘူး
[2024-07-02 06:25:49] Best translation 7996 : သ မီး ခံ စား ချက် ကကို လည်း ဂ ရု မ စစိုက် ကြ ဘူး
[2024-07-02 06:25:49] Best translation 7997 : တ ခြား ဘာ တွေ ဖြစ် သေး လဲ ဗျ
[2024-07-02 06:25:49] Best translation 7998 : ဒေါက် တာ အ ရင် က ရှင်း ပြ ဖူး ပါ တယ်
[2024-07-02 06:25:49] Best translation 7999 : ကကိုက် ထား တာ ကကို လာ မ ထုတ် မ ချင်း ငြိမ် နေ ပေး ပါ လလုံး ဝ မ လှုပ် ပါ နနဲ့ ရှင်
[2024-07-02 06:25:49] Total time: 85.52128s wall

real    19m53.090s
user    18m56.466s
sys     1m2.310s
```

Results are as follows:  

ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$ cat ./eval-result.txt  

```
(base) 
Evaluation with hyp.iter5000.my, Transformer model:
BLEU = 26.14, 66.3/43.2/29.0/20.0 (BP=0.728, ratio=0.759, hyp_len=71310, ref_len=93920)
Evaluation with hyp.iter10000.my, Transformer model:
BLEU = 38.65, 72.6/52.8/39.8/31.1 (BP=0.829, ratio=0.842, hyp_len=79073, ref_len=93920)
Evaluation with hyp.iter15000.my, Transformer model:
BLEU = 43.70, 74.0/55.4/42.8/34.4 (BP=0.882, ratio=0.888, hyp_len=83430, ref_len=93920)
Evaluation with hyp.iter20000.my, Transformer model:
BLEU = 45.50, 74.2/55.8/43.4/35.0 (BP=0.909, ratio=0.913, hyp_len=85724, ref_len=93920)
Evaluation with hyp.iter25000.my, Transformer model:
BLEU = 46.42, 74.1/55.8/43.5/35.3 (BP=0.925, ratio=0.928, hyp_len=87158, ref_len=93920)
Evaluation with hyp.iter30000.my, Transformer model:
BLEU = 46.73, 73.8/55.5/43.2/35.0 (BP=0.936, ratio=0.938, hyp_len=88110, ref_len=93920)
Evaluation with hyp.iter35000.my, Transformer model:
BLEU = 46.85, 73.4/55.1/42.9/34.8 (BP=0.946, ratio=0.947, hyp_len=88937, ref_len=93920)
Evaluation with hyp.iter40000.my, Transformer model:
BLEU = 47.10, 73.2/55.0/42.9/34.8 (BP=0.952, ratio=0.953, hyp_len=89490, ref_len=93920)
Evaluation with hyp.iter45000.my, Transformer model:
BLEU = 46.96, 72.9/54.6/42.5/34.5 (BP=0.955, ratio=0.956, hyp_len=89786, ref_len=93920)
Evaluation with hyp.iter50000.my, Transformer model:
BLEU = 46.85, 72.7/54.4/42.3/34.3 (BP=0.958, ratio=0.959, hyp_len=90030, ref_len=93920)
Evaluation with hyp.iter55000.my, Transformer model:
BLEU = 46.73, 72.4/54.1/42.0/34.0 (BP=0.962, ratio=0.962, hyp_len=90382, ref_len=93920)
Evaluation with hyp.iter60000.my, Transformer model:
BLEU = 46.70, 72.2/53.8/41.7/33.8 (BP=0.965, ratio=0.966, hyp_len=90699, ref_len=93920)
Evaluation with hyp.iter65000.my, Transformer model:
BLEU = 46.57, 72.0/53.6/41.5/33.6 (BP=0.967, ratio=0.968, hyp_len=90872, ref_len=93920)
Evaluation with hyp.iter70000.my, Transformer model:
BLEU = 46.43, 71.9/53.4/41.3/33.4 (BP=0.968, ratio=0.968, hyp_len=90959, ref_len=93920)
(base) ye@lst-hpc3090:~/exp/nmt/my-th/zen-chk1/model.tf.thmy$
```

အခုချိန်ထိ မြန်မာ-ထိုင်း၊ ထိုင်း-မြန်မာ ရလဒ်တွေအကြားမှာ တိုးတက်မှုရှိတယ်။ ဒေတာကို ထပ်တိုးထားတာနဲ့ run ရန်။  

