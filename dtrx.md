Date: 26 Nov 2018 
# dtrx (Do the Right Extraction)

## Note in Myanmar language:
zip, tar စသည်ဖြင့်ချုံ့ထားတဲ့ ဖိုင်တွေကို ဖြေတဲ့အခါမှာ option တွေကို မှတ်ထားဖို့လိုအပ်ပါတယ်။  
တစ်ခါတစ်လေမှာ option တွေကို မေ့နေတဲ့အခါမှာ၊ အကြောင်းအမျိုးမျိုးကြောင့် ပေးလိုက်တဲ့ option နဲ့ ဖိုင်ကို extract လုပ်လို့မရတဲ့အခါမှာ  
အသုံးဝင်တဲ့ tool တစ်ခုကို မိတ်ဆက်ပေးလိုက်ပါတယ်။  

## Error:
(py3.6.5) lar@lar-air:/media/lar/Transcend/img-match/keras$ tar -xvzf ./17flowers.tgz 

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now

## Try with dtrx  

```bash
$sudo apt-get install dtrx

(py3.6.5) lar@lar-air:/media/lar/Transcend/img-match/keras$ dtrx ./17flowers.tgz 
./17flowers.tgz contains one directory but its name doesn't match.
 Expected: 17flowers
   Actual: jpg/
You can:
 * extract the directory _I_nside a new directory named 17flowers
 * extract the directory and _R_ename it 17flowers
 * extract the directory _H_ere
What do you want to do?  (I/r/h) I

```

