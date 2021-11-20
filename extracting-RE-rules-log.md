# Extracting RE Rules Log

typo error-suggestion pair dictionary ကနေ correction rule ဆွဲထုတ်တဲ့ log ပါ။
ဒေါက်တာတန်း ကျောင်းသူ အိဖြူဖြူနဲ့ အတူတွဲလုပ်နေတဲ့ spelling checking experiment တစ်ခုအတွက် စမ်းခဲ့တဲ့ log ပါ။

## Syllable Breaking

".err" နဲ့ ".sug" ဖိုင်တွေကို syllable breaking လုပ်ဖို့အတွက် အောက်ပါ shell script ကို ရေးခဲ့တယ်။  

```
#!/bin/bash

# syllable breaking for all error types
# written by Ye, LST, NECTEC, Thailand

for f in {con,encode,pho-typo,seq,slang,typo,dialect,pho,sensitive,short,stack};
do
   echo "syllable breaking for $f.err ...";
   perl ./sylbreak.pl -i ./$f.err -s " " > ./$f.err.syl;
   head $f.err.syl;
   perl ./sylbreak.pl -i ./$f.sug -s " " > ./$f.sug.syl;
   echo "syllable breaking for $f.sug ...";
   head $f.sug.syl;
   echo "";
done;
```

./sylbreak-all.sh ကို run တော့ အောက်ပါအတိုင်း syllable break လုပ်ပြီးထွက်လာတဲ့ output ဖိုင်တွေကို head နဲ့ ရိုက်ပြပေးလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ ./sylbreak-all.sh 
syllable breaking for con.err ...
 ခဲ့ တဲ့ သြ စ တြေး
 သွင်း ခဲ့ ၇ ဘူး ပေါ့
 က ဥက္က ဌ
 က ဥက္က ဌ တွေ က
 ခြံ ထဲ ၀င် ရင်
 က ဥက္က ဌ တို့
 ရိုင် ဥက္က ဌ တို့ က
 အ ဖွဲ့ ၀င် လွှတ် တော်
 ပြ သ နာ ကြောင့်
 ဘာ ပြ သ နာ မှ
syllable breaking for con.sug ...
 ခဲ့ တဲ့ ဩ စ တြေး
 သွင်း ခဲ့ ရ ဘူး ပေါ့
 က ဥက္ကဋ္ဌ
 က ဥက္ကဋ္ဌ တွေ က
 ခြံ ထဲ ဝင် ရင်
 က ဥက္ကဋ္ဌ တို့
 ရိုင် ဥက္ကဋ္ဌ တို့ က
 အ ဖွဲ့ ဝင် လွှတ် တော်
 ပြ ဿ နာ ကြောင့်
 ဘာ ပြ ဿ နာ မှ

syllable breaking for encode.err ...
 တဲ့ ဒီ အ ဓိပ် ပါ ယျ လေး ကို
 ခင် ကြီး တို့် များ သိ
 သာ ဓဳ သာ ဓု
 တ န လာၤ နေ့ က
 တိုင်း သာ စ ကာၤ ပူ မှာ လုပ်
 ခဲ့ တဲ့ တ န လာၤ နေ့ တုန်း
 စ ကာၤ ပူ မှာ
 ခဲ့ တဲ့ တ န လာၤ နေ့ က
 မ ရှိၾ ဘူးၾ ဘူး
 သူ ဦး ခြ သေ့ၤ အောင် က
syllable breaking for encode.sug ...
 တဲ့ ဒီ အ ဓိပ္ပာယ် လေး ကို
 ခင် ကြီး တို့ များ သိ
 သာ ဓု သာ ဓု
 တ နင်္လာ နေ့ က
 တိုင်း သာ စင်္ကာ ပူ မှာ လုပ်
 ခဲ့ တဲ့ တ နင်္လာ နေ့ တုန်း
 စင်္ကာ ပူ မှာ
 ခဲ့ တဲ့ တ နင်္လာ နေ့ က
 ကြ ဘူး ဘူး
 သူ ဦး ခြင်္သေ့ အောင် က

syllable breaking for pho-typo.err ...
 လူ ကြီး တေ ကို
 ရ မ လည် သမ္မ တ
 မူ တည် ပီး သူ နဲ့
 ခံ ပီး အ ဓိပ္ပာယ်
 ချိန် မှာ လည် ရိုး သား
 ရ မ လည် ဖေ့
 ငွေ အ လွှဲ သုံး စား
 ငွေ အ လွှဲ သုံး
 ဒေ တာ တေ ကို ရ
 စွာ ပိတ် ပီး သ တိ
syllable breaking for pho-typo.sug ...
 လူ ကြီး တွေ ကိုယ်
 ရ မ လဲ သမ္မ တ
 မူ တည် ပြီး သူ နဲ့
 ခံ ပြီး အ ဓိပ္ပာယ်
 ချိန် မှာ လဲ ရိုး သား
 ရ မ လဲ ဖေ့စ်
 ငွေ အ လွဲ သုံး စား
 ငွေ အ လွဲ သုံး
 ဒေ တာ တွေ ကို ရ
 စွာ ပိတ် ပြီး သ တိ

syllable breaking for seq.err ...
 ရန် ကုန် မြို့ ကြီး က
 လေး တောေ တာင် ပေါ် ခြံ
 ညီ ထောက် ပ့ံ ကြ
 ဒါ မေ လး စား တာ
ေ လး စား
 မွေး ဝမ်းေ ကျာင်း မယ် မေတ္တာ
 ဖြစ် ပါ်ေ နေ သာ
 လုးံ ကို တောင်
 ဘန်ေ တွ ထက် အ
ေ ကာင်ေ တွ
syllable breaking for seq.sug ...
 ရန် ကုန် မြို့ ကြီး က
 လေး တော တောင် ပေါ် ခြံ
 ညီ ထောက် ပံ့ ကြ
 ဒါ မ လေး စား တာ
 လေး စား
 မွေး ဝမ်း ကျောင်း မယ် မေတ္တာ
 ဖြစ် ပေါ် နေ သာ
 လုံး ကို တောင်
 ဘန် တွေ ထက် အ
 ကောင်း တွေ

syllable breaking for slang.err ...
 အဲ့ တော့ ဘိုလ် ပြော ရ
 တား ဂို
 ကြီး ကြောက် လတ် တာ
 ကျက် သ တုန်း ကွန်
 ရှေး ရှေး ဘျင် ဒေ
 လဲ ပါ တရ်
 မို့ တူ တရ်
 မွင်း ခါး တွေ ရ
 ဖြစ် တိုင်း သောက် ပြစ် တင်
 ကြား လောက် မွင်း ခါး ပွဲ များ
syllable breaking for slang.sug ...
 အဲ့ တော့ ဘယ် လို ပြော ရ
 သား ကို
 ကြီး ကြောက် လိုက် တာ
 ကျက် သ ရေ တုံး ကွန်
 ရှေး ရှေး ဘု ရင် တွေ
 လဲ ပါ တယ်
 မို့ တူ တယ်
 မုန့် ဟင်း ခါး တွေ ရ
 ဖြစ် တိုင်း စောက် ပြစ် တင်
 ကြား လောက် မုန့် ဟင်း ခါး ပွဲ များ

syllable breaking for typo.err ...
 သ မား က ဟာ အ
 ကြီး ပါ ဟယ်လ်
 တွေ ပါ ဟယ်လ်
 က တော့ အ သိ ခဲ့
 တောင်း ပန် စု တ
 ကို လိုက် လော မယ် ဆို
 ဆို ဂုဏ် ပြ တာ ခံ
 လိုက် တာ ဈေူ ကွက် ထဲ
က်ု အ ခြေ
 ကျပ် ကိူ ဆို လို
syllable breaking for typo.sug ...
 သ မား ဟာ အ
 ကြီး ပါ ဟယ်
 တွေ ပါ ဟယ်
 က တော့ မ သိ ခဲ့
 တောင်း ပန် စာ တစ်
 ကို လိုက် လျော မယ် ဆို
 ဆို ဂုဏ် ပြု တာ ခံ
 လိုက် တာ ဈေး ကွက် ထဲ
 ကို အ ခြေ
 ကျပ် ကို ဆို လို

syllable breaking for dialect.err ...
 ခိုး ထား သာ များ လို့
 တန် အ ကျဉ်း တန် လွန်း
 ရေ မ တွိ့ စော် ကြာ
 ကြည့် ဇမ် မ နာ
 အ ရာ တ ခါ စု
 အား ပီး လျက် ပါ
 ပြော သာ က
 သော စာ
 အ တွက် ဒေ ဟင်း ကို
 ချက် ဖို့ အ လွယ် ခေျ
syllable breaking for dialect.sug ...
 ခိုး ထား တာ များ လို့
 တန် အ ကျည်း တန် လွန်း
 ရေ မ တွိ စော် ကြာ
 ကြည့် စမ်း မ နာ
 အ ရာ တစ် ခါ စု
 အား ပေး လျက် ပါ
 ပြော တာ က
 တော့ ဓာ
 အ တွက် ဒီ ဟင်း ကို
 ချက် ဖို့ လွယ် လွယ် လေး

syllable breaking for pho.err ...
 သ မား တ ယောက် လို့
 ဘူး ဒီ စ နီး မောင်
 တွေ ပြင် စဉ် နေ ရ
 ရဲ့ စာ တ မျက် နှာ
 ကျ နော် တို့
 ရင် ကျ နော် တို့ ဘက်
 ဒီ တ ပတ် မြန်
 တဲ့ လူ တ စု
 လူ ကြီး တေ ကို
 ရ မ လည် သမ္မ တ
syllable breaking for pho.sug ...
 သ မား တစ် ယောက် လို့
 ဘူး ဒီ ဇ နီး မောင်
 တွေ ပြင် ဆင် နေ ရ
 ရဲ့ စာ တစ် မျက် နှာ
 ကျွန် တော် တို့
 ရင် ကျွန် တော် တို့ ဘက်
 ဒီ တစ် ပတ် မြန်
 တဲ့ လူ တစ် စု
 လူ ကြီး တွေ ကိုယ်
 ရ မ လဲ သမ္မ တ

syllable breaking for sensitive.err ...
 မှာ ပစ် T a t ခံ ရ
 ၁ ဦး T a y S o n e ဟု သိ
 ကြမ်း ဖက် T a t ဖြတ် မှု
 ၀ ကျော် M a T a r P a w ခဲ့ ကြောင်း
 မ သိ M a T a r တေ
 ပဲ လေ M a T a r
 ဦး ကို T a t ဖြတ် ခြင်း
 ရပ် ကွက် D a လန် အုပ်
 မှာ မ T a y သေး ဟု
 T ရုတ် မ
syllable breaking for sensitive.sug ...
 မှာ ပစ် သတ် ခံ ရ
 ၁ ဦး ဆုံး ဟု သိ
 ကြမ်း ဖက် သတ် ဖြတ် မှု
 ၀ ကျော် မ သာ ပေါ် ခဲ့ ကြောင်း
 မ သိ မ သာ တေ
 ပဲ လေ မ သာ
 ဦး ကို သတ် ဖြတ် ခြင်း
 ရပ် ကွက် ဒ လန် အုပ်
 မှာ မ သေ သေး ဟု
 တ ရုတ် မ

syllable breaking for short.err ...
 စား တာ နဲ့
 ရီ ပြန် လေ့ ကျင့်
 တွေ ရယ် $ ရှက်
 တွေ ကို $ အ လုပ်
 4 ကြွက် များ
 ရ အောင် ဘို လို လုပ်
 စောင့် ရင်း $ ဈေး တွေ
 ပြော လိုက် ပြ စေ
 အ ရ စ ဆ ရ က လုပ် မိ
 ရင် ဘာ
syllable breaking for short.sug ...
 စား ပြီး တာ နဲ့
 ရီ ပြန် ပြီး လေ့ ကျင့်
 တွေ ရယ် စောက် ရှက်
 တွေ ကို စောက် အ လုပ်
 ဖော ကြွက် များ
 ရ အောင် ဘယ် လို လို လုပ်
 စောင့် ရင်း ဒေါ် လာ ဈေး တွေ
 ပြော လိုက် ပါ ရ စေ
 အ ရ စောက် ဆ ရာ ကြီး လုပ် မိ
 အိပ် ရင် ဘာ

syllable breaking for stack.err ...
 အ ခု ကု မ ဏီ ထဲ
 ရေ ငုပ် သင် ဘော ပျောက် သွား
 တွင်း ချင်း သ ဂြိုလ် လိုက် ရ
 ဒီ နေ့ တ နင်း ဂ နွေ မင်း
 အ တွက် စင် ကာ ပူ
 ကျမ္မာ ပါ စေ
 ဏာ ရူး သ မ တ ရူး
 စိုး မင် ဂ လာ ပါ
 ဓိ က သင် ချိုင်း က
 နိုင် ငံ သစ် စာ ဖောက် အ
syllable breaking for stack.sug ...
 အ ခု ကုမ္ပ ဏီ ထဲ
 ရေ ငုပ် သင်္ဘော ပျောက် သွား
 တွင်း ချင်း သင်္ဂြိုဟ် လိုက် ရ
 ဒီ နေ့ တ နင်္ဂ နွေ မင်း
 အ တွက် စင်္ကာ ပူ
 ကျန်း မာ ပါ စေ
 ဏာ ရူး သမ္မ တ ရူး
 စိုး မင်္ဂ လာ ပါ
 ဓိ က သင်္ချိုင်း က
 နိုင် ငံ သစ္စာ ဖောက် အ

(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

## Preparing wdiff files

wdiff ပရိုဂရမ်က ကိုယ့်စက်ထဲမှာ မရှိသေးလို့ အောက်ပါအတိုင်း apt-get ဆိုတဲ့ command ကို သုံးပြီး install လုပ်ခဲ့...  

```
sudo apt-get install wdiff
```

".err.syl" နဲ့ ".sug.syl" နှစ်ဖိုင်တွဲကနေ word မတူတဲ့အပိုင်းတွေကိုပဲ (i.e. word difference) ဆွဲထုတ်တဲ့ အလုပ်ကို wdiff program ကို သုံးပြီး ဆွဲထုတ်ဖို့အတွက် bash shell script ကို အောက်ပါအတိုင်း ရေးခဲ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cat ./mk-wdiff-chk.sh 
#!/bin/bash

# running wdiff on error and suggestion parallel data
# Written by Ye, LST, NECTEC, Thailand
# 16 Nov 2021

for f in {con,encode,pho-typo,seq,slang,typo,dialect,pho,sensitive,short,stack}
do
   echo "wdiff ./$f.err.syl ./$f.sug.syl > $f.wdiff";
   wdiff ./$f.err.syl ./$f.sug.syl > $f.wdiff;
   
   echo "wc ./$f.err.syl ./$f.sug.syl ./$f.wdiff";
   wc ./$f.err.syl ./$f.sug.syl ./$f.wdiff;
   
   echo "head ./$f.wdiff";
   head ./$f.wdiff;
   echo "==========";
   echo "";
done


(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

