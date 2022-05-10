# XNMT ASEAN my-th Experiment Log

Plan to add Myanmar-Thai language pair of ASEAN-MT Domain for SwitchOver Experiment ...  

## Data Preparation

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ mkdir asean-myth
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp$ cd asean-myth/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ mkdir data
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth$ cd data/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ cp /home/ye/data/zzh/plan-to-use-for-switchout/5_TH-MY_myPOS-V3_Reports/DATA/data-word/*.{th,my} .
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ ls
test.my  test.th  train.my  train.th  valid.my  valid.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ wc *
   1000    9579  119884 test.my
   1000    7169   99326 test.th
  20000  187574 2360049 train.my
  20000  139767 1951027 train.th
   1031    9573  119279 valid.my
   1031    6809   98543 valid.th
  44062  360471 4748108 total
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

## Checking on Data

Sometimes, it might contain blank lines and we need to check it before we train NMT model ...  

1st copying the perl script ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline/data$ cp print-blank-lines.pl ../../asean-myth/data/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline/data$ cd ../../asean-myth/data/
```

check blank line exist or not with that perl script ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./train.th
4616
6863
8076
10007
13347
19555
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./valid.th
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./test.th
```

As above, we found some blank lines when we checked with train.th.  
And also check for the Myanmar data and it looks OK as follows:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./train.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./valid.my
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ perl ./print-blank-lines.pl ./test.my
```

Make parallel training data for deleting blank lines of Thai side together with the parallel Myanmar sentences ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ paste train.th train.my > train.thmy
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$ head ./train.thmy
ใช่ , ฉัน ชอบ เล่น หมากรุก ไทย  ဟုတ်ကဲ့ ၊ ကျွန်တော် ထိုင်း စစ်တုရင် ကစား ရ တာ ကြိုက် တယ် ။
คุณ มี อะไร แนะนำ สำหรับ เด็ก ไหม ?     ကလေးများ အတွက် တစ် ခု ခု အကြံပြု ပေး နိုင် မလား ။
ฉัน สามารถ ไป ที่ นั่น ได้ อย่างไร ?    အဲဒီ ကို ဘယ်လို ရောက် နိုင် မလဲ ။
ฉัน ปวด เมื่อย ทั่ว ทั้งหมด     တစ်ကိုယ်လုံး ကိုက်ခဲ နေ လို့ ။
ขอบคุณ สำหรับ ทั้งหมด ที่ คุณ ทำ เพื่อ พวก เรา  ကျွန်တော် တို့ အတွက် လုပ် ပေး ခဲ့ တာ တွေ ကျေးဇူးတင် ပါ တယ် ။
ฉันหวังว่าคุณเพลิดเพลินอาหารเย็นของคุณ  ခင်ဗျား ရဲ့ ညစာ ကို နှစ်သက် မယ် လို့ မျှော်လင့် ပါ တယ် ။
เรา สามารถ เดิน ไป ยัง อ่าว ได้ ไหม ?   ဆိပ်ကမ်း ကို လမ်းလျှောက် သွား နိုင် လား ။
ฉันเสียใจ, ท่าน. ปลานึ่งของคุณไม่พร้อม. ถ้าคุณไม่ต้องการมันจริงๆ, พวกเราสามารถยกเลิกมัน စိတ်မကောင်း ပါ ဘူး ဆရာ ။ ခင်ဗျား ရဲ့ ငါးပေါင်း က အဆင်သင့် မ ဖြစ် သေး ပါ ဘူး ။ ခင်ဗျား မ မှာ ချင် တော့ ဘူး ဆို ရင် တော့ ဖျက် လိုက် လို့ ရ ပါ တယ် ။
ฮอทดอกหนึ่งคู่  hot dog နှစ် ခု လောက် ။
กรุณาดื่มซุปโดยตรงจากชาม        စွပ်ပြုတ် ကို ပန်းကန်လုံး ထဲ က နေ တိုက်ရိုက် သောက် ပါ ။
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth/data$
```

delete blank lines according to their line numbers ...  

```

```

```

```

```

```

```

```

```

```
