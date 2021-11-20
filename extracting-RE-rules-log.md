# Extracting RE Rules Log

typo error-suggestion pair dictionary ကနေ correction rule ဆွဲထုတ်တဲ့ log ပါ။
ဒေါက်တာတန်း ကျောင်းသူ အိဖြူဖြူနဲ့ အတူတွဲလုပ်နေတဲ့ spelling checking experiment တစ်ခုအတွက် စမ်းခဲ့တဲ့ log ပါ။

## Syllable Breaking

".err" နဲ့ ".sug" ဖိုင်တွေကို syllable breaking လုပ်ဖို့အတွက် အောက်ပါ shell script ကို ရေးခဲ့တယ်။  

```bash
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

```bash
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

mk-wdiff-chk.sh ကို အောက်ပါအတိုင်း run ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./mk-wdiff-chk.sh | tee ./extract-wdiff.log
wdiff ./con.err.syl ./con.sug.syl > con.wdiff
wc ./con.err.syl ./con.sug.syl ./con.wdiff
  3797  17815 166161 ./con.err.syl
  3797  16862 164951 ./con.sug.syl
  4272  21888 236392 ./con.wdiff
 11866  56565 567504 total
head ./con.wdiff
 ခဲ့ တဲ့ [-သြ-] {+ဩ+} စ တြေး
 သွင်း ခဲ့ [-၇-] {+ရ+} ဘူး ပေါ့
 က [-ဥက္က ဌ-] {+ဥက္ကဋ္ဌ+}
 က [-ဥက္က ဌ-] {+ဥက္ကဋ္ဌ+} တွေ က
 ခြံ ထဲ [-၀င်-] {+ဝင်+} ရင်
 က [-ဥက္က ဌ-] {+ဥက္ကဋ္ဌ+} တို့
 ရိုင် [-ဥက္က ဌ-] {+ဥက္ကဋ္ဌ+} တို့ က
 အ ဖွဲ့ [-၀င်-] {+ဝင်+} လွှတ် တော်
 ပြ [-သ-] {+ဿ+} နာ ကြောင့်
 ဘာ ပြ [-သ-] {+ဿ+} နာ မှ
==========

wdiff ./encode.err.syl ./encode.sug.syl > encode.wdiff
wc ./encode.err.syl ./encode.sug.syl ./encode.wdiff
  376  1524 15575 ./encode.err.syl
  376  1507 16217 ./encode.sug.syl
  512  2140 25917 ./encode.wdiff
 1264  5171 57709 total
head ./encode.wdiff
 တဲ့ ဒီ အ [-ဓိပ် ပါ ယျ-] {+ဓိပ္ပာယ်+} လေး ကို
 ခင် ကြီး [-တို့်-] {+တို့+} များ သိ
 သာ [-ဓဳ-] {+ဓု+} သာ ဓု
 တ [-န လာၤ-] {+နင်္လာ+} နေ့ က
 တိုင်း သာ [-စ ကာၤ-] {+စင်္ကာ+} ပူ မှာ လုပ်
 ခဲ့ တဲ့ တ [-န လာၤ-] {+နင်္လာ+} နေ့ တုန်း
 [-စ ကာၤ-]
 {+စင်္ကာ+} ပူ မှာ
 ခဲ့ တဲ့ တ [-န လာၤ-] {+နင်္လာ+} နေ့ က
 [-မ ရှိၾ ဘူးၾ-]
==========

wdiff ./pho-typo.err.syl ./pho-typo.sug.syl > pho-typo.wdiff
wc ./pho-typo.err.syl ./pho-typo.sug.syl ./pho-typo.wdiff
  3097  13252 129887 ./pho-typo.err.syl
  3097  13270 138041 ./pho-typo.sug.syl
  3475  16721 192898 ./pho-typo.wdiff
  9669  43243 460826 total
head ./pho-typo.wdiff
 လူ ကြီး [-တေ ကို-] {+တွေ ကိုယ်+}
 ရ မ [-လည်-] {+လဲ+} သမ္မ တ
 မူ တည် [-ပီး-] {+ပြီး+} သူ နဲ့
 ခံ [-ပီး-] {+ပြီး+} အ ဓိပ္ပာယ်
 ချိန် မှာ [-လည်-] {+လဲ+} ရိုး သား
 ရ မ [-လည် ဖေ့-] {+လဲ ဖေ့စ်+}
 ငွေ အ [-လွှဲ-] {+လွဲ+} သုံး စား
 ငွေ အ [-လွှဲ-] {+လွဲ+} သုံး
 ဒေ တာ [-တေ-] {+တွေ+} ကို ရ
 စွာ ပိတ် [-ပီး-] {+ပြီး+} သ တိ
==========

wdiff ./seq.err.syl ./seq.sug.syl > seq.wdiff
wc ./seq.err.syl ./seq.sug.syl ./seq.wdiff
  2058   9266  95698 ./seq.err.syl
  2058   8938  95682 ./seq.sug.syl
  2524  12474 149562 ./seq.wdiff
  6640  30678 340942 total
head ./seq.wdiff
 ရန် ကုန် မြို့ ကြီး က
 လေး [-တောေ တာင်-] {+တော တောင်+} ပေါ် ခြံ
 ညီ ထောက် [-ပ့ံ-] {+ပံ့+} ကြ
 ဒါ [-မေ လး-] {+မ လေး+} စား တာ
[-ေ လး-]
 {+လေး+} စား
 မွေး [-ဝမ်းေ ကျာင်း-] {+ဝမ်း ကျောင်း+} မယ် မေတ္တာ
 ဖြစ် [-ပါ်ေ-] {+ပေါ်+} နေ သာ
 [-လုးံ-]
 {+လုံး+} ကို တောင်
==========

wdiff ./slang.err.syl ./slang.sug.syl > slang.wdiff
wc ./slang.err.syl ./slang.sug.syl ./slang.wdiff
  1150   4546  46684 ./slang.err.syl
  1150   4990  51057 ./slang.sug.syl
  1501   6395  74768 ./slang.wdiff
  3801  15931 172509 total
head ./slang.wdiff
 အဲ့ တော့ [-ဘိုလ်-] {+ဘယ် လို+} ပြော ရ
 [-တား ဂို-]
 {+သား ကို+}
 ကြီး ကြောက် [-လတ်-] {+လိုက်+} တာ
 ကျက် သ [-တုန်း-] {+ရေ တုံး+} ကွန်
 ရှေး ရှေး [-ဘျင် ဒေ-] {+ဘု ရင် တွေ+}
 လဲ ပါ [-တရ်-] {+တယ်+}
 မို့ တူ [-တရ်
 မွင်း-] {+တယ်
 မုန့် ဟင်း+} ခါး တွေ ရ
==========

wdiff ./typo.err.syl ./typo.sug.syl > typo.wdiff
wc ./typo.err.syl ./typo.sug.syl ./typo.wdiff
  18677   81661  858050 ./typo.err.syl
  18677   81574  860528 ./typo.sug.syl
  20913  101138 1226374 ./typo.wdiff
  58267  264373 2944952 total
head ./typo.wdiff
 သ မား [-က-] ဟာ အ
 ကြီး ပါ [-ဟယ်လ်-] {+ဟယ်+}
 တွေ ပါ [-ဟယ်လ်-] {+ဟယ်+}
 က တော့ [-အ-] {+မ+} သိ ခဲ့
 တောင်း ပန် [-စု တ-] {+စာ တစ်+}
 ကို လိုက် [-လော-] {+လျော+} မယ် ဆို
 ဆို ဂုဏ် [-ပြ-] {+ပြု+} တာ ခံ
 လိုက် တာ [-ဈေူ-] {+ဈေး+} ကွက် ထဲ
[-က်ု-]
 {+ကို+} အ ခြေ
==========

wdiff ./dialect.err.syl ./dialect.sug.syl > dialect.wdiff
wc ./dialect.err.syl ./dialect.sug.syl ./dialect.wdiff
  55  224 2139 ./dialect.err.syl
  55  226 2180 ./dialect.sug.syl
  66  293 3182 ./dialect.wdiff
 176  743 7501 total
head ./dialect.wdiff
 ခိုး ထား [-သာ-] {+တာ+} များ လို့
 တန် အ [-ကျဉ်း-] {+ကျည်း+} တန် လွန်း
 ရေ မ [-တွိ့-] {+တွိ+} စော် ကြာ
 ကြည့် [-ဇမ်-] {+စမ်း+} မ နာ
 အ ရာ [-တ-] {+တစ်+} ခါ စု
 အား [-ပီး-] {+ပေး+} လျက် ပါ
 ပြော [-သာ-] {+တာ+} က
 [-သော စာ-]
 {+တော့ ဓာ+}
 အ တွက် [-ဒေ-] {+ဒီ+} ဟင်း ကို
==========

wdiff ./pho.err.syl ./pho.sug.syl > pho.wdiff
wc ./pho.err.syl ./pho.sug.syl ./pho.wdiff
  22789  101157 1004498 ./pho.err.syl
  22789  100769 1023392 ./pho.sug.syl
  25703  126631 1451378 ./pho.wdiff
  71281  328557 3479268 total
head ./pho.wdiff
 သ မား [-တ-] {+တစ်+} ယောက် လို့
 ဘူး ဒီ [-စ-] {+ဇ+} နီး မောင်
 တွေ ပြင် [-စဉ်-] {+ဆင်+} နေ ရ
 ရဲ့ စာ [-တ-] {+တစ်+} မျက် နှာ
 [-ကျ နော်-]
 {+ကျွန် တော်+} တို့
 ရင် [-ကျ နော်-] {+ကျွန် တော်+} တို့ ဘက်
 ဒီ [-တ-] {+တစ်+} ပတ် မြန်
 တဲ့ လူ [-တ-] {+တစ်+} စု
 လူ ကြီး [-တေ ကို-] {+တွေ ကိုယ်+}
==========

wdiff ./sensitive.err.syl ./sensitive.sug.syl > sensitive.wdiff
wc ./sensitive.err.syl ./sensitive.sug.syl ./sensitive.wdiff
   73   644  3293 ./sensitive.err.syl
   73   381  3619 ./sensitive.sug.syl
   82   771  5008 ./sensitive.wdiff
  228  1796 11920 total
head ./sensitive.wdiff
 မှာ ပစ် [-T a t-] {+သတ်+} ခံ ရ
 ၁ ဦး [-T a y S o n e-] {+ဆုံး+} ဟု သိ
 ကြမ်း ဖက် [-T a t-] {+သတ်+} ဖြတ် မှု
 ၀ ကျော် [-M a T a r P a w-] {+မ သာ ပေါ်+} ခဲ့ ကြောင်း
 မ သိ [-M a T a r-] {+မ သာ+} တေ
 ပဲ လေ [-M a T a r-] {+မ သာ+}
 ဦး ကို [-T a t-] {+သတ်+} ဖြတ် ခြင်း
 ရပ် ကွက် [-D a-] {+ဒ+} လန် အုပ်
 မှာ မ [-T a y-] {+သေ+} သေး ဟု
 [-T-]
==========

wdiff ./short.err.syl ./short.sug.syl > short.wdiff
wc ./short.err.syl ./short.sug.syl ./short.wdiff
  144   590  5370 ./short.err.syl
  144   680  6964 ./short.sug.syl
  161   830  8955 ./short.wdiff
  449  2100 21289 total
head ./short.wdiff
 စား {+ပြီး+} တာ နဲ့
 ရီ ပြန် {+ပြီး+} လေ့ ကျင့်
 တွေ ရယ် [-$-] {+စောက်+} ရှက်
 တွေ ကို [-$-] {+စောက်+} အ လုပ်
 [-4-]
 {+ဖော+} ကြွက် များ
 ရ အောင် [-ဘို-] {+ဘယ် လို+} လို လုပ်
 စောင့် ရင်း [-$-] {+ဒေါ် လာ+} ဈေး တွေ
 ပြော လိုက် [-ပြ-] {+ပါ ရ+} စေ
 အ ရ [-စ-] {+စောက်+} ဆ [-ရ က-] {+ရာ ကြီး+} လုပ် မိ
==========

wdiff ./stack.err.syl ./stack.sug.syl > stack.wdiff
wc ./stack.err.syl ./stack.sug.syl ./stack.wdiff
   789   3857  38102 ./stack.err.syl
   789   3455  39705 ./stack.sug.syl
   973   4763  59372 ./stack.wdiff
  2551  12075 137179 total
head ./stack.wdiff
 အ ခု [-ကု မ-] {+ကုမ္ပ+} ဏီ ထဲ
 ရေ ငုပ် [-သင် ဘော-] {+သင်္ဘော+} ပျောက် သွား
 တွင်း ချင်း [-သ ဂြိုလ်-] {+သင်္ဂြိုဟ်+} လိုက် ရ
 ဒီ နေ့ တ [-နင်း ဂ-] {+နင်္ဂ+} နွေ မင်း
 အ တွက် [-စင် ကာ-] {+စင်္ကာ+} ပူ
 [-ကျမ္မာ-]
 {+ကျန်း မာ+} ပါ စေ
 ဏာ ရူး [-သ မ-] {+သမ္မ+} တ ရူး
 စိုး [-မင် ဂ-] {+မင်္ဂ+} လာ ပါ
 ဓိ က [-သင် ချိုင်း-] {+သင်္ချိုင်း+} က
==========


real	0m1.254s
user	0m1.241s
sys	0m0.039s
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

အထက်ပါအတိုင်း typo-error စာလုံးနဲ့ အဲဒါကို correction လုပ်ရမယ့် စာလုံးတွေကို set အလိုက် မြင်ရတာမို့ အရမ်းအဆင်ပြေတယ်။   
အဲဒါကြောင့် linux command တွေကို ချစ်တာ...  <3 

## wdiff Pattern to Prefix-Error-Correction-Suffix Pattern Conversion

လက်ရှိ ရှိနေတဲ့ wdiff pattern ကို လေ့လာကြည့်တော့ ငါတို့ manual ပြင်ဆင်ပြီး ဆွဲထုတ်ထားတဲ့ ဒေတာမှာက တချို့ မှာက prefix ပါတယ်၊ တချို့မှာက prefix ရော suffix ရော ပါတယ်။ တချို့မှာက suffix ပဲ ပါပြီးတော့ တချို့ စာလုံးတွဲတွေမှာက prefix ရော suffix ရော မပါပဲနဲ့ error နဲ့ correction ဆိုတဲ့ pattern မျိုးဖြစ်နေတာတွေကို တွေ့ရတယ်။ အဲဒါကြောင့် prefix syllable, suffix syllable တွေကို လိုအပ်တဲ့အခါမှာ ဆွဲထုတ်သုံးလို့ ရအောင် ပြီးတော့ pattern တွေရဲ့ distribution ကိုလည်း ကြည့်ချင်လို့ အောက်ပါ perl script ကို ရေးခဲ့တယ်။  

```perl
#!/usr/bin/env perl

# making Regular Expression rules based on wdiff output
# Ye Kyaw Thu, LST, NECTEC, Thailand
#
# How to run: 
# e.g. $ perl mk-re.pl <wdiff-output-filename>

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

# function for printing Regular Expression
sub print_RE_old {
    my ($sent) = @_;
    my @words = split (" ", $sent);
    # filtering @words
    my @pattern = grep { $_ =~ /\[\-.*\-\]|\{\+.*\+\}/ } @words;
    $pattern[0] =~ s/\[|\-|\]//g;
    $pattern[1] =~  s/\{|\+|\}//g;
    print("/$pattern[0]/$pattern[1]/\n");
    exit();
    #print("@pattern\n"); exit();
}

sub print_RE {
    my ($sent) = @_;
    #print("$sent\n");
    if ($sent =~ m/([က-၏A-Za-z0-9]+\s){1,5}(\[\-.*\-\])\s(\{\+.*\+\})(\s[က-၏A-Za-z0-9]+){1,5}/ugm) {
#    if ($sent =~ m/([က-၏A-Za-z0-9]+\s){1,}(\[\-[က-၏A-Za-z0-9\s]+\-\])\s(\{\+[က-၏A-Za-z0-9\s]+\+\})(\s[က-၏A-Za-z0-9]+){1,}/g) {
    my ($prefix_syl, $error, $correction, $suffix_syl) = $sent =~ /([က-၏A-Za-z0-9]+\s){1}(\[\-.*\-\])\s(\{\+.*\+\})(\s[က-၏A-Za-z0-9]+){1}/;
#    print("prefix_syl: $prefix_syl, error: $error, correction: $correction, suffix_syl: $suffix_syl\n");
    print("$prefix_syl\t$error\t$correction\t$suffix_syl\tpecs\n");    
    } elsif ($sent =~ m/([က-၏A-Za-z0-9]+\s){1,5}(\[\-.*\-\])\s(\{\+.*\+\})/ugm) {

    my ($prefix_syl, $error, $correction) = $sent =~ /([က-၏A-Za-z0-9]+\s){1}(\[\-.*\-\])\s(\{\+.*\+\})/;
#    print("prefix_syl: $prefix_syl, error: $error, correction: $correction\n");
    print("$prefix_syl\t$error\t$correction\tpec\n");
    
    } elsif ($sent =~ m/(\[\-.*\-\])\s(\{\+.*\+\})(\s[က-၏A-Za-z0-9]+){1,5}/ugm) {

    my ($error, $correction, $suffix_syl) = $sent =~ /(\[\-.*\-\])\s(\{\+.*\+\})(\s[က-၏A-Za-z0-9]+){1}/;
#    print("error: $error, correction: $correction, suffix_syl: $suffix_syl\n");
    print("$error\t$correction\t$suffix_syl\tecs\n");            
    
    } elsif ($sent =~ m/(\[\-.*\-\])\s(\{\+.*\+\})/ugm) {

    my ($error, $correction) = $sent =~ /(\[\-.*\-\])\s(\{\+.*\+\})/;
    #print("error: $error, correction: $correction\n");
    print("$error\t$correction\tec\n");          
    } else {
        #print("ELSE: $sent\n");
    
    }
}

open (my $inputFILE,"<:encoding(UTF-8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

my $read_2nd_line=0; my $first_line="";

while (!eof($inputFILE)) {
    my $line = <$inputFILE>;
    if (($line ne '') & ($line !~ /^ *$/)) {
        chomp($line);
        $line =~ s/^\s+|\s+$//g;
        #$line =~ s/\t/ /g;
        if ($read_2nd_line == 0) {
            if ($line !~ m/^\[-.*-\]$/) {
               #print("$line\n");
               print_RE($line);
            } else {
                $read_2nd_line = 1;
                $first_line = $line; 
            }
         } elsif ($read_2nd_line == 1) {
             #print ($first_line." ".$line."\n");
             print_RE($first_line." ".$line);
             $read_2nd_line = 0; $first_line = "";
         }
    }
}

close ($inputFILE);
```

ငါတို့ ခွဲထားတဲ့ spelling error type အကုန်ကို run ဖို့အတွက် အောက်ပါ shell script ကို ရေးခဲ့တယ်။  

```bash
#!/bin/bash

for f in {con,encode,pho-typo,seq,slang,typo,dialect,pho,sensitive,short,stack}
do
   echo "printing for $f.wdiff ...";
   perl ./mk-re.pl ./$f.wdiff > $f.rule
   sort ./$f.rule | uniq > $f.rule.uniq
done
```

အထက်မှာ မြင်ရတဲ့အတိုင်း rule ဖိုင်တွေကိုလည်း ထပ်နေတာတွေကို ဖယ်လိုက်ပြီး uniq rule ဘယ်နှစ်ခု ရလာမလဲ ဆိုတာကို သိချင်လို့၊ အဲဒီဖိုင်ကိုပဲ သုံးချင်လို့ uniq command ကို လည်း သုံးပြီး unique လုပ်ခဲ့တယ်။  

အထက်ပါ shell ကို အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/errant/my-data$ time ./print-prefix-error-correction-suffix.sh | tee print-rules.log
printing for con.wdiff ...
printing for encode.wdiff ...
printing for pho-typo.wdiff ...
printing for seq.wdiff ...
printing for slang.wdiff ...
printing for typo.wdiff ...
printing for dialect.wdiff ...
printing for pho.wdiff ...
printing for sensitive.wdiff ...
printing for short.wdiff ...
printing for stack.wdiff ...

real	0m4.558s
user	0m1.768s
sys	0m0.041s
(base) ye@:/media/ye/project2/exp/errant/my-data$
```
