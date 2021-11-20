# Extracting RE Rules Log

typo error-suggestion pair dictionary ကနေ correction rule ဆွဲထုတ်တဲ့ log ပါ။ ဒေါက်တာတန်း ကျောင်းသူ အိဖြူဖြူမွန် (Ph.D. candidate) နဲ့ အတူတွဲလုပ်နေတဲ့ spelling checking experiment တစ်ခုအတွက် စမ်းခဲ့တဲ့ log ပါ။

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
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./print-prefix-error-correction-suffix.sh | tee print-rules.log
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
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

ထွက်လာတဲ့ unique rule ဖိုင်တွေကို head, tail command သုံးပြီးတော့ confirmation လုပ်ခဲ့၊ လေ့လာခဲ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ head *.rule.uniq
==> con.rule.uniq <==
၀ 	[-၀န်း-]	{+ဝန်း+}	 ကျင်	pecs
[-၀က်-]	{+ဝက်+}	ec
[-၀က်-]	{+ဝက်+}	 ပိုး	ecs
[-၀က်-]	{+ဝက်+}	 သာ	ecs
၀ 	[-ခု-]	{+ပြည့် နှစ်+}	pec
၀ 	[-ခု-]	{+ပြည့်+}	 နှစ်	pecs
[-၀င်း-]	{+ဝင်း+}	 ကျော်	ecs
[-၀င်-]	{+ဝင်+}	 ကို	ecs
[-၀င်-]	{+ဝင်+}	 ချင်း	ecs
[-၀င်း-]	{+ဝင်း+}	 စား	ecs

==> dialect.rule.uniq <==
က 	[-ပါ-]	{+ဘာ+}	 မ	pecs
ကျန် 	[-သာ-]	{+တာ+}	 တွေ	pecs
ကြည့် 	[-ဇမ်-]	{+စမ်း+}	 မ	pecs
ကြမ်း 	[-သာ-]	{+တာ+}	 ပေါ့	pecs
ကား 	[-စင်း-]	{+စီး+}	 လုံး	pecs
ကို 	[-ဘဲ့-]	{+ပဲ+}	 လိုက်	pecs
ကို 	[-လေး-]	{+လဲ+}	 မ	pecs
ချင် 	[-သာ-]	{+တာ+}	 လုပ်	pecs
ခံ 	[-သာ-]	{+တာ+}	 ဂုဏ်	pecs
ခိုင် 	[-ရို-]	{+တို့+}	 ပြ	pecs

==> encode.rule.uniq <==
[-ǧ ကံ-]	{+သွေ ကြုံ+}	 ဆုံ	ecs
[- က ည့်-]	{+ကြည့်+}	 အ	ecs
ကန် 	[-နေ က-]	{+နေ ကြ+}	 ရ	pecs
[-က မာ့-]	{+ကမ္ဘာ့+}	 အ	ecs
ကျယ် 	[-ပြန့််-]	{+ပြန့်+}	 ပြ	pecs
ကျော် 	[-သ ဂြိၤုဟ်-]	{+သင်္ဂြိုဟ်+}	 ပေး	pecs
ကြည် 	[-ညိဳ-]	{+ညို+}	 ခွင့်	pecs
ကြီး 	[-တို့်-]	{+တို့+}	 များ	pecs
က 	[-လ တၩ-]	{+လတ်+}	pec
ကွန် 	[-ပျ-]	{+ပျူ+}	 တာ	pecs

==> pho.rule.uniq <==
၀ 	[-ဘိုး-]	{+ဖိုး+}	 မ	pecs
၀ 	[-ဘဲ-]	{+ပဲ+}	 စစ်	pecs
၀ 	[-မစ်-]	{+မိ+}	 နစ်	pecs
၀ 	[-မီး-]	{+မိ+}	 နစ်	pecs
၁ 	[-ပါတ်-]	{+ပတ်+}	 ၂	pecs
၂ 	[-ချမ်-]	{+ခြမ်း+}	 မ	pecs
၂ 	[-ပါတ်-]	{+ပတ်+}	 က	pecs
၂ 	[-ပါတ်-]	{+ပတ်+}	 ကျော်	pecs
၂ 	[-ပါတ်-]	{+ပတ်+}	 နား	pecs
၂ 	[-ပီး-]	{+ပြီး+}	 မှ	pecs

==> pho-typo.rule.uniq <==
၀ 	[-မစ်-]	{+မိ+}	 နစ်	pecs
၀ 	[-မီး-]	{+မိ+}	 နစ်	pecs
၂ 	[-ချမ်-]	{+ခြမ်း+}	 မ	pecs
၂ 	[-ပီး-]	{+ပြီး+}	 မှ	pecs
၃ 	[-ပီး-]	{+ပြီး+}	 မှ	pecs
၅ 	[-ပီး-]	{+ပြီး+}	 ရင်	pecs
၈ 	[-နစ်-]	{+နှစ်+}	 တိုင်	pecs
က 	[-ကာ လိုက်-]	{+ကန့် လန့်+}	 ကာ	pecs
[-က-]	{+ကိ+}	 ရိ	ecs
က 	[-ကို ရဲ-]	{+ကိုယ့် ရဲ့+}	pec

==> sensitive.rule.uniq <==
[-M a T a r P a w-]	{+မ သာ ပေါ်+}	 သွား	ecs
[-T a y S o n e-]	{+သေ ဆုံး+}	 ချင်	ecs
[-T a y S o n e-]	{+သေ ဆုံး+}	 ခဲ့	ecs
[-T a y-]	{+သေ+}	 တာ	ecs
[-T-]	{+တ+}	 ရုတ်	ecs
က 	[-d a-]	{+ဒ+}	 လန်	pecs
ကျော် 	[-M a T a r P a w-]	{+မ သာ ပေါ်+}	 ခဲ့	pecs
ကျော် 	[-T a y S o n e-]	{+သေ ဆုံး+}	 ခဲ့	pecs
ကွက် 	[-D a-]	{+ဒ+}	 လန်	pecs
ကို 	[-R-]	{+ရု+}	 ရှား	pecs

==> seq.rule.uniq <==
၀ 	[-၀ေ လျှာ့-]	{+၀ လျှော့+}	 ဈေး	pecs
၀ 	[-၀ေ လာက်-]	{+၀ လောက်+}	 အ	pecs
၀ 	[-ကျော်ေ သ-]	{+ကျော် သေ+}	 ဆုံး	pecs
၀ 	[-ကေျာ်-]	{+ကျော်+}	 ကို	pecs
၀ 	[-ကေျာ်-]	{+ကျော်+}	 နေ	pecs
၀ 	[-ကေျာ်-]	{+ကျော်+}	 ဖိ	pecs
၀ 	[-ကေျာ်-]	{+ကျော်+}	 လုပ်	pecs
၀ 	[-ကေျာ်-]	{+ကျော်+}	 လောက်	pecs
၀ 	[-ကေျာ် တောင်း-]	{+ကျော် တောင်+}	pec
၀ 	[-တန်းေ အာင်-]	{+တန်း အောင်+}	 လာ	pecs

==> short.rule.uniq <==
[-$-]	{+စောက်+}	 ကျ	ecs
[-4-]	{+ဖော+}	 ကြွက်	ecs
က 	[-$-]	{+စောက်+}	 သုံး	pecs
က 	[-စ ခ-]	{+စစ် ခွေး+}	 တွေ	pecs
က 	[-ဖ လ-]	{+ဖေ လိုး+}	 မ	pecs
ကျ 	[-စ ခ-]	{+စစ် ခွေး+}	 တစ်	pecs
ကျဉ်း 	[-၂-]	{+ကျဉ်း+}	 လေး	pecs
ကျ 	[-နာ ဘဲ-]	{+နေ တာ ပဲ+}	pec
က 	[-အာ-]	{+အဲ ဒီ+}	 ခါ	pecs
ကို 	[-$-]	{+စောက်+}	 အ	pecs

==> slang.rule.uniq <==
[-၀တ်-]	{+ကြ ဝဋ်+}	 လည်	ecs
က 	[-ကျော်-]	{+ကျွန် တော်+}	 တို့	pecs
က 	[-ကျော်-]	{+ကျွန် တော်+}	 အ	pecs
က 	[-ကွီး-]	{+ကို ကြီး+}	 ဖြိုး	pecs
က 	[-ကော် ရီး-]	{+ကို ကြီး+}	 လို့	pecs
က 	[-ခ ညား-]	{+ခင် ဗျား+}	 ပ	pecs
က 	[-ခေး လည်း-]	{+က လေး လဲ+}	pec
က 	[-ဂျင်း-]	{+ချင်း+}	 ထည့်	pecs
က 	[-ဂျင်း-]	{+ချင်း+}	 မိ	pecs
က 	[-ဂျစ်-]	{+ချစ်+}	 စ	pecs

==> stack.rule.uniq <==
၀ 	[-သ ကြ်န်-]	{+သင်္ကြန်+}	 မ	pecs
၀ 	[-သ ကြ်န်-]	{+သင်္ကြန်+}	 အ	pecs
၀ 	[-သင် ဂြို ဘို့-]	{+သင်္ဂြိုဟ် ဖို့+}	pec
၃ 	[-စ ကန့်-]	{+စက္ကန့်+}	 လွတ်	pecs
၄ 	[-စ ကန့်-]	{+စက္ကန့် နေ့+}	pec
၆ 	[-စ ကန့်-]	{+စက္ကန့်+}	 နေ	pecs
က 	[-က မာ-]	{+ကမ္ဘာ+}	 ကြီး	pecs
ကံ 	[-ကြ မာ တ-]	{+ကြမ္မာ တစ်+}	pec
က 	[-ကုမ္မ-]	{+ကုမ္ပ+}	 ဏီ	pecs
က 	[-ကုမ် ပ-]	{+ကုမ္ပ+}	 ဏီ	pecs

==> typo.rule.uniq <==
၀ 	[-ကျာ်-]	{+ကျော်+}	 ပြီ	pecs
၀ 	[-ကျော််-]	{+ကျော်+}	 နိုင်	pecs
၀ 	[-ဂဏ္ဏန်း-]	{+ဂ ဏန်း+}	 အ	pecs
၀ 	[-တန််း-]	{+တန်း+}	 က	pecs
၀ 	[-တွက်-]	{+တွင်+}	 ကွယ်	pecs
၀ 	[-နှစ်ေ ကြာ်-]	{+နှစ် ကျော်+}	 လောက်	pecs
၀ 	[-နှာ-]	{+မှာ+}	 ၂	pecs
၀ 	[-နှုန်ူ-]	{+နှုန်း+}	 လောက်	pecs
၀ 	[-နါ-]	{+နာ+}	 ရီ	pecs
၀ 	[-နိး-]	{+နီး+}	 ပါး	pecs
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ 
```

tail command ကို သုံးပြီး rule pattern တွေကို လေ့လာခဲ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ tail *.rule.uniq
==> con.rule.uniq <==
ဦး 	[-ဥာ-]	{+ဉာ+}	 ဏိ	pecs
ဦး 	[-ဥာဏ်-]	{+ဉာဏ်+}	 ထွန်း	pecs
ဧည့် 	[-၀တ်-]	{+ဝတ်+}	 မ	pecs
[-၏-]	{+ဧ+}	 ည့်	ecs
ဧ 	[-ယ ဥ်-]	{+ယင်+}	 ကျူး	pecs
ဧ 	[-ရာေ ၇-]	{+ရာ ရေ+}	pec
[-ေ ၇-]	{+ရေ+}	ec
[-ေ ၇-]	{+ရေ+}	 ကန်	ecs
[-ေ စျး-]	{+ဈေး+}	 က	ecs
[-ေြ သာ် ယောက်-]	{+ဪ ယောက်ျား+}	ec

==> dialect.rule.uniq <==
သေး 	[-ပါ တ-]	{+ဘာ သ+}	pec
[-သော စာ-]	{+တော့ ဓာ+}	ec
ဟယ် 	[-ယို-]	{+လို+}	 အဲ	pecs
ဟုတ် 	[-သာ-]	{+တာ+}	pec
ဟုတ် 	[-သာ-]	{+တာ+}	 မ	pecs
အ 	[-ကျဉ်း-]	{+ကျည်း+}	 တန်	pecs
အ 	[-သုန်း-]	{+တုံး+}	 အ	pecs
အား 	[-ပီး-]	{+ပေး+}	 လျက်	pecs
အဲ့ 	[-သာ-]	{+ဒါ+}	 ကြောင့်	pecs
အဲ့ 	[-သာ-]	{+ဒါ+}	 တွေ	pecs

==> encode.rule.uniq <==
[-အေ ကး-]	{+ညစ် အ ကြေး+}	 များ	ecs
[-အေ ကး-]	{+ညစ် အ ကြေး+}	 ရှင်း	ecs
[-အေ ကာင်း-]	{+ခံ အ ကြောင်း+}	 ရင်း	ecs
[-အေ ကာင်း-]	{+မှု အ ကြောင်း+}	 ရင်း	ecs
[-အေ တြး အျ မင္-]	{+အ တွေး အ မြင်+}	ec
[-အေ ရးခ်ိဳးေ ဖာက္-]	{+ခွင့် အ ရေး ချိုး+}	ec
ဦး 	[-ခြ သေ့ၤ-]	{+ခြင်္သေ့+}	 အောင်	pecs
ဦး 	[-ရြဲ မတ်-]	{+ရဲ မြတ်+}	 သူ	pecs
[-ိုင်-]	{+နိုင်+}	 ရည်	ecs
[-ေ ကာ င့်-]	{+ကြောင့်+}	ec

==> pho.rule.uniq <==
[-ဦ-]	{+ဦး+}	 နှောက်	ecs
ဧည့် 	[-သယ်-]	{+သည်+}	 တော်	pecs
[-ဧည်-]	{+ဧည့်+}	 စာ	ecs
ဧ 	[-ပ ရယ်-]	{+ပြီ+}	 လ	pecs
ဧ 	[-ယဉ် ကျုး-]	{+ယင် ကျူး+}	pec
ဧ 	[-ယဉ် ကျုး-]	{+ယင် ကျူး+}	 ပြီး	pecs
ဧ 	[-ယဉ်-]	{+ယင်+}	 ကျူး	pecs
ဩ 	[-တုံ-]	{+တုန်+}	 လှုပ်	pecs
ဪ 	[-ဆောက်-]	{+စောက်+}	 အ	pecs
[-ေက်း-]	{+ကျေး+}	 ဇူး	ecs

==> pho-typo.rule.uniq <==
ဥ 	[-ယဉ်-]	{+ယျာဉ်+}	 လဲ	pecs
ဦး 	[-ဇင်း-]	{+ပဉ္စင်း+}	 ကျော်	pecs
ဦး 	[-ဇင်း-]	{+ပဉ္စင်း+}	 ဘုန်း	pecs
ဦး 	[-ညွတ်-]	{+ညွှတ်+}	 ပါ	pecs
ဦး 	[-ညွတ်-]	{+ညွှတ်+}	 လိုက်	pecs
ဦး 	[-ညွတ်-]	{+ညွှတ်+}	 အ	pecs
ဦး 	[-ပီး-]	{+ပြီး+}	 ရင်	pecs
ဦး 	[-မာ-]	{+မှာ+}	pec
ဦး 	[-မာ-]	{+မှာ+}	 စိုး	pecs
ဦး 	[-မာ-]	{+မှာ+}	 လား	pecs

==> sensitive.rule.uniq <==
အောင် 	[-T a y S o n e-]	{+သေ ဆုံး+}	 ပြီး	pecs
ဦး 	[-M a T a r P a w-]	{+မ သာ ပေါ်+}	pec
ဦး 	[-M a T a r P a w-]	{+မ သာ ပေါ်+}	 ခဲ့	pecs
ဦး 	[-T a y S o n e-]	{+ဆုံး+}	 ဟု	pecs
ဦး 	[-T a y S o n e-]	{+သေ ဆုံး+}	 ခဲ့	pecs
ဦး 	[-T a y S o n e-]	{+သေ ဆုံး+}	 တဲ့	pecs
ဦး 	[-T a y S o n e-]	{+သေ ဆုံး+}	 ပြီး	pecs
ဦး 	[-T a y-]	{+သေ+}	 ၃	pecs
ဦး 	[-T a y-]	{+သေ+}	 ခဲ့	pecs
ဦး 	[-T a y-]	{+သေ+}	 ပြီး	pecs

==> seq.rule.uniq <==
[-ေ ဟး-]	{+ဟေး+}	 မင်း	ecs
[-ေ အး-]	{+အေး+}	ec
[-ေ အာက် ကြို့-]	{+အောက် ကျို့+}	ec
[-ေ အာက်-]	{+အောက်+}	 တန်း	ecs
[-ေ အာင်-]	{+အောင်+}	 မြင်	ecs
[-ေ အာ် ဒုက်-]	{+အော် ဒုက္ခ+}	ec
[-ေ အာ်-]	{+အော်+}	 စစ်	ecs
[-ေ ဩာ်-]	{+ဪ+}	 သူ	ecs
[-ေ ဩာ်-]	{+ဪ+}	 ဟို	ecs
[-ော ဆင်း-]	{+ဆောင်း+}	 ဘောက်	ecs

==> short.rule.uniq <==
လောက် 	[-% လည်း-]	{+ရာ ခိုင် နှုန်း လဲ+}	pec
လဲ 	[-ကွာ့-]	{+ကိုယ် ဟာ+}	 ကိုယ်	pecs
[-သ-]	{+စောက် သူ+}	ec
သား 	[-စ ခ-]	{+စစ် ခွေး+}	 တွေ	pecs
သာ 	[-သွ-]	{+သူ့ ဟာ+}	 သူ	pecs
သိ 	[-ပျ ဇေ-]	{+ပါ ရ စေ+}	pec
ဟို 	[-မှာိး-]	{+မှာ လီး+}	 တွေ	pecs
အ 	[-၆-]	{+ခြောက်+}	pec
အောင် 	[-ဘို-]	{+ဘယ် လို+}	 လို	pecs
[-ီး-]	{+လီး+}	 ရန်	ecs

==> slang.rule.uniq <==
[-အူး-]	{+လိုက် အုံး+}	ec
[-အူး-]	{+အုံး+}	ec
[-အူးးးး-]	{+အုံး+}	ec
[-အူး-]	{+အုံး+}	 မယ်	ecs
[-အူး-]	{+ဦး+}	 က	ecs
အေး 	[-ငါး-]	{+ငါ့+}	 ကောင်	pecs
အေး 	[-ဖ လူး-]	{+ဖေ လိုး+}	 မ	pecs
အေ 	[-ယိုး-]	{+လိုး+}	 မင်း	pecs
အော် 	[-နက်-]	{+နဲ့+}	 သေ	pecs
အဲ 	[-ဟု-]	{+ဟုတ်+}	 ပြီ	pecs

==> stack.rule.uniq <==
[-အိ္န္ဒိ-]	{+အိန္ဒိ+}	 ယ	ecs
အောင် 	[-စင် ကာ-]	{+စင်္ကာ+}	 ပူ	pecs
အော် 	[-ဒုက် ခ-]	{+ဒုက္ခ+}	 ပဲ	pecs
အဲ့ 	[-ပ စည်း-]	{+ပစ္စည်း+}	 လေး	pecs
အဲ့ 	[-ဘဂ်ါ-]	{+ဘင်္ဂါ+}	 လီ	pecs
ဤ 	[-ပုဒ္မ-]	{+ပုဒ် မ+}	 ကို	pecs
[-ဥ က-]	{+ဥက္က+}	 လာ	ecs
ဥ 	[-ပေက် ခါ-]	{+ပေက္ခာ+}	 ပြု	pecs
ဥ 	[-ရိ ခါ-]	{+ရိက္ခာ+}	 ဝေ	pecs
ဪ 	[-သင် ခါ-]	{+သင်္ခါ+}	 ရ	pecs

==> typo.rule.uniq <==
[-ု-]	{+လုံ+}	 ခြုံ	ecs
[-ူ-]	{+လူ+}	 ကြီး	ecs
[-ေက်း-]	{+ကျေး+}	 ဇူး	ecs
[-ေ ပါ့ ကျေ-]	{+ပေါ့ ကျွန်+}	ec
[-ေ မာတ္တာ ပို-]	{+မေတ္တာ ပို့+}	ec
[-ေ လ-]	{+ကွာ လေ+}	ec
[-ော ကး-]	{+ကြေး+}	 ညို	ecs
[-ေးာက်-]	{+စောက်+}	 ကျေး	ecs
[-ဲ-]	{+အဲ့+}	 ဒါ	ecs
[-္အား-]	{+အား+}	 တင်း	ecs
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

## Count Each Pattern

လက်ရှိ ငါတို့ ပြင်ထားတဲ့ spelling typo dictionary မှာ rule တစ်ခုချင်းစီအတွက် အရေအတွက် ဘယ်လောက် ရှိသလဲ ဆိုတာကို အောက်ပါအတိုင်း check လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cat *.rule.uniq | grep -w "pecs" | wc
  29936  155490 1761390
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cat *.rule.uniq | grep -w "pec" | wc
   3999   21531  235692
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cat *.rule.uniq | grep -w "ecs" | wc
   3624   15909  178012
(base) ye@:/media/ye/project2/exp/errant/my-data$/4github cat *.rule.uniq | grep -w "ec" | wc
    565    2714   29209
```

သေချာအောင် total လိုင်းအရေအတွက်နဲ့ ပြန်တိုက်စစ်ဆေးခဲ့...  
rule.uniq ဖိုင် အားလုံးက လိုင်းအရေအတွက် 38124 ရှိတယ်။  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cat *.rule.uniq | wc
  38124  195644 2204303
```

ဆွဲထုတ်ထားတဲ့ rule pattern တစ်ခုချင်းကို ပြန်စစ်ကြည့်တော့ အောက်ပါအတိုင်း ညီတာကို တွေ့ရတယ်။ အဲဒါကြောင့် grep နဲ့ ဆွဲထုတ်တဲ့ နေရာမှာ error မရှိတာကို confirmation လုပ်နိုင်ခဲ့...    

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ echo "29936+3999+3624+565" | bc
38124
```

## Histogram of Prefix and Suffix

လက်ရှိ ဒေတာမှာ prefix ပဲရှိတာ၊ suffix ပဲ ရှိတာ၊ prefix-suffix နှစ်ခုညှပ်ရှိတာ၊ prefix-suffix နှစ်ခုစလုံး မပါတာတွေက တကယ်က spelling error detection အတွက်ရော၊ spelling suggestion အတွက်ရော အရေးပါတယ်။ အဲဒါကြောင့် လက်ရှိ ရှိနေတဲ့ prefix, suffix distribution ကို histogram graph အကြမ်းထုတ်ထားပြီး နောက်ပိုင်း ဒေတာထပ်ဖြည့် ပြင်တဲ့အခါမှာ ဂရုစိုက်ရမယ့် အချက်တွေကို ဆွေးနွေးတဲ့အခါ ပြန်ကြည့်ရန်...  

python code ကို အောက်ပါအတိုင်း ရေးခဲ့...  

```python
import matplotlib.pyplot as plt
import pandas as pd

data = pd.read_csv('pattern-dist.csv', sep = '\t', index_col = 0)
# if you want to change font size globally
#plt.rcParams['font.size'] = '16'


data.plot(kind = 'bar')
plt.xlabel('Pattern', fontsize=16)
plt.ylabel('Frequency', fontsize=16)
plt.xticks(fontsize= 14)
plt.title('Prefix, Suffix Distribution')
#plt.margins(0.9)

#plt.gca().axes.get_xaxis().set_visible(False) # label တွေကို ဖျောက်ချင်ရင် သုံးတာ
#plt.gca().axes.get_yaxis().set_visible(False)
plt.tight_layout() # မဟုတ်ရင် x-axis label က မပေါ်လို့...
plt.savefig('prefix-suffix-pattern-distribution.png', dpi = 150)
plt.show()
```

အထက်ပါ python code ကို run လိုက်ရင် ရလာမယ့် histogram က အောက်ပါအတိုင်း...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/prefix-suffix-pattern-distribution.png" alt="prefix, suffix distribution histogram" width="540"/>  
</p>  
<div align="center">
  Fig. Histogram graph of prefix, suffix distributions on current typo dictionary
</div> 

<br />

## Unique Rules to RE Search-Replace Pairs

လက်ရှိ ဆွဲထုတ်ထားတဲ့ rule တွေကို perl script သုံးပြီး ပထမတော့ တိုက်ရိုက် RE rule ထုတ်ကြည့်ခဲ့တယ်။ သို့သော် အဲဒီ RE rules ကို ဖိုင်ထဲကနေ တိုက်ရိုက်ခေါ်ပြီး eval လုပ်တာက သိပ်အလွယ်ကြီးမဟုတ်တော့ (security ပြဿနာလည်း ရှိလို့) search လုပ်ရမယ့် စာလုံးနဲ့ replace လုပ်ရမယ့် စာလုံး တွဲ အဖြစ်ပဲ ပြင်ရေးခဲ့တယ်။ updated perl script က အောက်ပါအတိုင်းပါ။  

```perl 
#!/usr/bin/env perl

# Conversion of unique rules to Regular Expression search-replace rules
# dummy step for writing final perl script
# Ye Kyaw Thu, LST, NECTEC, Thailand
#
# How to run: 
# e.g. $ perl uniq2RE.pl <uniq-rule-filename>

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

open (my $inputFILE,"<:encoding(UTF-8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

while (!eof($inputFILE)) {
    my $line = <$inputFILE>;
    if (($line ne '') & ($line !~ /^ *$/)) {
        chomp($line);
        my @fields = split(/\t/, $line);
        my $pattern = $fields[-1];

        if ($pattern eq "pecs") {
            my ($prefix, $error, $correction, $suffix) = split ("\t", $line);
            $error =~ s/[\[\-\]]//g;
            $correction =~ s/[\{\+\}]//g;
            print("$prefix$error$suffix\t$prefix$correction$suffix\n");
        } elsif ($pattern eq "pec") {
            my ($prefix, $error, $correction) = split ("\t", $line);
            $error =~ s/[\[\-\]]//g;
            $correction =~ s/[\{\+\}]//g;            
            print("$prefix$error\t$prefix$correction\n");            
        } elsif ($pattern eq "ecs") {
            my ($error, $correction, $suffix) = split ("\t", $line);
            $error =~ s/[\[\-\]]//g;
            $correction =~ s/[\{\+\}]//g;
            print("$error$suffix\t$correction$suffix\n");
        } elsif ($pattern eq "ec") {
            my ($error, $correction) = split ("\t", $line);
            $error =~ s/[\[\-\]]//g;
            $correction =~ s/[\{\+\}]//g;
            print("$error\t$correction\n");
        }    
   }       
}

close ($inputFILE);

```

တကယ် run ဖို့အတွက်ကျတော့ error အမျိုးအစား တစ်ခုချင်းစီကို ခေါ် run ဖို့ လိုအပ်တာကြောင့် အောက်ပါအတိုင်း shell script ကို ရေးခဲ့တယ်။  

```bash
#!/bin/bash

for uniq_file in *.uniq;
do
    echo "uniq2RE conversion for $uniq_file ...";
    perl ./uniq2RE.pl $uniq_file > $uniq_file.RE
    head $uniq_file.RE;
    echo "";
done
```

အထက်ပါ shell scrpt ကို သုံးပြီး search<TAB>replace ဖိုင်တွေကို အောက်ပါအတိုင်း ဆောက်ခဲ့တယ်။  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./uniq2RE-all.sh | tee making-uniq-to-RE-pattern.log
uniq2RE conversion for con.rule.uniq ...
၀ ၀န်း ကျင်	၀ ဝန်း ကျင်
၀က်	ဝက်
၀က် ပိုး	ဝက် ပိုး
၀က် သာ	ဝက် သာ
၀ ခု	၀ ပြည့် နှစ်
၀ ခု နှစ်	၀ ပြည့် နှစ်
၀င်း ကျော်	ဝင်း ကျော်
၀င် ကို	ဝင် ကို
၀င် ချင်း	ဝင် ချင်း
၀င်း စား	ဝင်း စား

uniq2RE conversion for dialect.rule.uniq ...
က ပါ မ	က ဘာ မ
ကျန် သာ တွေ	ကျန် တာ တွေ
ကြည့် ဇမ် မ	ကြည့် စမ်း မ
ကြမ်း သာ ပေါ့	ကြမ်း တာ ပေါ့
ကား စင်း လုံး	ကား စီး လုံး
ကို ဘဲ့ လိုက်	ကို ပဲ လိုက်
ကို လေး မ	ကို လဲ မ
ချင် သာ လုပ်	ချင် တာ လုပ်
ခံ သာ ဂုဏ်	ခံ တာ ဂုဏ်
ခိုင် ရို ပြ	ခိုင် တို့ ပြ

uniq2RE conversion for encode.rule.uniq ...
ǧ ကံ ဆုံ	သွေ ကြုံ ဆုံ
 က ည့် အ	ကြည့် အ
ကန် နေ က ရ	ကန် နေ ကြ ရ
က မာ့ အ	ကမ္ဘာ့ အ
ကျယ် ပြန့်် ပြ	ကျယ် ပြန့် ပြ
ကျော် သ ဂြိၤုဟ် ပေး	ကျော် သင်္ဂြိုဟ် ပေး
ကြည် ညိဳ ခွင့်	ကြည် ညို ခွင့်
ကြီး တို့် များ	ကြီး တို့ များ
က လ တၩ	က လတ်
ကွန် ပျ တာ	ကွန် ပျူ တာ

uniq2RE conversion for pho.rule.uniq ...
၀ ဘိုး မ	၀ ဖိုး မ
၀ ဘဲ စစ်	၀ ပဲ စစ်
၀ မစ် နစ်	၀ မိ နစ်
၀ မီး နစ်	၀ မိ နစ်
၁ ပါတ် ၂	၁ ပတ် ၂
၂ ချမ် မ	၂ ခြမ်း မ
၂ ပါတ် က	၂ ပတ် က
၂ ပါတ် ကျော်	၂ ပတ် ကျော်
၂ ပါတ် နား	၂ ပတ် နား
၂ ပီး မှ	၂ ပြီး မှ

uniq2RE conversion for pho-typo.rule.uniq ...
၀ မစ် နစ်	၀ မိ နစ်
၀ မီး နစ်	၀ မိ နစ်
၂ ချမ် မ	၂ ခြမ်း မ
၂ ပီး မှ	၂ ပြီး မှ
၃ ပီး မှ	၃ ပြီး မှ
၅ ပီး ရင်	၅ ပြီး ရင်
၈ နစ် တိုင်	၈ နှစ် တိုင်
က ကာ လိုက် ကာ	က ကန့် လန့် ကာ
က ရိ	ကိ ရိ
က ကို ရဲ	က ကိုယ့် ရဲ့

uniq2RE conversion for sensitive.rule.uniq ...
M a T a r P a w သွား	မ သာ ပေါ် သွား
T a y S o n e ချင်	သေ ဆုံး ချင်
T a y S o n e ခဲ့	သေ ဆုံး ခဲ့
T a y တာ	သေ တာ
T ရုတ်	တ ရုတ်
က d a လန်	က ဒ လန်
ကျော် M a T a r P a w ခဲ့	ကျော် မ သာ ပေါ် ခဲ့
ကျော် T a y S o n e ခဲ့	ကျော် သေ ဆုံး ခဲ့
ကွက် D a လန်	ကွက် ဒ လန်
ကို R ရှား	ကို ရု ရှား

uniq2RE conversion for seq.rule.uniq ...
၀ ၀ေ လျှာ့ ဈေး	၀ ၀ လျှော့ ဈေး
၀ ၀ေ လာက် အ	၀ ၀ လောက် အ
၀ ကျော်ေ သ ဆုံး	၀ ကျော် သေ ဆုံး
၀ ကေျာ် ကို	၀ ကျော် ကို
၀ ကေျာ် နေ	၀ ကျော် နေ
၀ ကေျာ် ဖိ	၀ ကျော် ဖိ
၀ ကေျာ် လုပ်	၀ ကျော် လုပ်
၀ ကေျာ် လောက်	၀ ကျော် လောက်
၀ ကေျာ် တောင်း	၀ ကျော် တောင်
၀ တန်းေ အာင် လာ	၀ တန်း အောင် လာ

uniq2RE conversion for short.rule.uniq ...
$ ကျ	စောက် ကျ
4 ကြွက်	ဖော ကြွက်
က $ သုံး	က စောက် သုံး
က စ ခ တွေ	က စစ် ခွေး တွေ
က ဖ လ မ	က ဖေ လိုး မ
ကျ စ ခ တစ်	ကျ စစ် ခွေး တစ်
ကျဉ်း ၂ လေး	ကျဉ်း ကျဉ်း လေး
ကျ နာ ဘဲ	ကျ နေ တာ ပဲ
က အာ ခါ	က အဲ ဒီ ခါ
ကို $ အ	ကို စောက် အ

uniq2RE conversion for slang.rule.uniq ...
၀တ် လည်	ကြ ဝဋ် လည်
က ကျော် တို့	က ကျွန် တော် တို့
က ကျော် အ	က ကျွန် တော် အ
က ကွီး ဖြိုး	က ကို ကြီး ဖြိုး
က ကော် ရီး လို့	က ကို ကြီး လို့
က ခ ညား ပ	က ခင် ဗျား ပ
က ခေး လည်း	က က လေး လဲ
က ဂျင်း ထည့်	က ချင်း ထည့်
က ဂျင်း မိ	က ချင်း မိ
က ဂျစ် စ	က ချစ် စ

uniq2RE conversion for stack.rule.uniq ...
၀ သ ကြ်န် မ	၀ သင်္ကြန် မ
၀ သ ကြ်န် အ	၀ သင်္ကြန် အ
၀ သင် ဂြို ဘို့	၀ သင်္ဂြိုဟ် ဖို့
၃ စ ကန့် လွတ်	၃ စက္ကန့် လွတ်
၄ စ ကန့်	၄ စက္ကန့် နေ့
၆ စ ကန့် နေ	၆ စက္ကန့် နေ
က က မာ ကြီး	က ကမ္ဘာ ကြီး
ကံ ကြ မာ တ	ကံ ကြမ္မာ တစ်
က ကုမ္မ ဏီ	က ကုမ္ပ ဏီ
က ကုမ် ပ ဏီ	က ကုမ္ပ ဏီ

uniq2RE conversion for typo.rule.uniq ...
၀ ကျာ် ပြီ	၀ ကျော် ပြီ
၀ ကျော်် နိုင်	၀ ကျော် နိုင်
၀ ဂဏ္ဏန်း အ	၀ ဂ ဏန်း အ
၀ တန််း က	၀ တန်း က
၀ တွက် ကွယ်	၀ တွင် ကွယ်
၀ နှစ်ေ ကြာ် လောက်	၀ နှစ် ကျော် လောက်
၀ နှာ ၂	၀ မှာ ၂
၀ နှုန်ူ လောက်	၀ နှုန်း လောက်
၀ နါ ရီ	၀ နာ ရီ
၀ နိး ပါး	၀ နီး ပါး


real	0m0.719s
user	0m0.248s
sys	0m0.047s
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

file size တွေကိုလည်း check လုပ်ခဲ့...  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ wc *.RE
   2479   14906  143585 con.rule.uniq.RE
     47     271    2497 dialect.rule.uniq.RE
    276    1763   18715 encode.rule.uniq.RE
  15619   91299  922186 pho.rule.uniq.RE
   2395   13813  138602 pho-typo.rule.uniq.RE
     43     438    2574 sensitive.rule.uniq.RE
   1622   10873  114612 seq.rule.uniq.RE
     97     643    5901 short.rule.uniq.RE
    830    4945   50074 slang.rule.uniq.RE
    619    3908   42854 stack.rule.uniq.RE
  14097   82156  876435 typo.rule.uniq.RE
  38124  225015 2318035 total
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$   
```
   
## Spelling Correction with Extracted Rules

အထက်မှာ ဆွဲထုတ်ပြီး ရလာတဲ့ search-replace အတွဲတွေကို သုံးပြီး စာလုံးပေါင်း မှားနေတဲ့ ဖိုင်ကို RE ရဲ့ s/search/replace/g; ပုံစံနဲ့ spelling correction လုပ်ပေးတဲ့ perl script ကို အောက်ပါအတိုင်း ရေးခဲ့...  
   
```perl 
#!/usr/bin/env perl

# Spelling correction with Regular Expression rules
# Ye Kyaw Thu, LST, NECTEC, Thailand
#
# Last updated date: 18 Nov 2021
# How to run: 
# e.g. $ perl correction-with-RE.pl <RE-filename> <error-file>

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

# read RE file and puto into an array
open (my $reFILE,"<:encoding(UTF-8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";
chomp(my @rules = <$reFILE>);
close ($reFILE);

open (my $errorFILE,"<:encoding(UTF-8)", $ARGV[1]) or die "Couldn't open input file $ARGV[1]!, $!\n";
while (!eof($errorFILE)) {
    my $line = <$errorFILE>;
    if (($line ne '') & ($line !~ /^ *$/)) {
        chomp($line);
        #print("input: $line\n");
        for my $rule (@rules) {
            my ($regex, $replacement) = split('\t', $rule);
            #print("regex: $regex, replacement: $replacement\n"); # for debugging
            $line =~ s/$regex/$replacement/g;
        }
        print("$line\n");
    }
    
}

close ($errorFILE);

```
   
errror type တစ်မျိုးစီကို ဖိုင်တစ်ဖိုင်စီ ခွဲသိမ်းထားတာမို့လို့ အဲဒီဖိုင်တွေအကုန်ကို run လို့ ရဖို့အတွက် အောက်ပါအတိုင်း shell script ကို ရေးခဲ့...  
   
```
#!/bin/bash

# written by Ye, LST, NECTEC, Thailand
# testing 1

for re in *.RE;
do
   re_file=${re%.*.*.*}; echo $re_file;
    echo "start checking";
    echo "input: $re_file.err.syl";
    head /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/$re_file.err.syl;
    perl ./correction-with-RE.pl ./total.RE.uniq /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/$re_file.err.syl > ./chk/$re_file.err.syl.chk
    echo "checked output:";
    head ./chk/$re_file.err.syl.chk; exit;
done
```
   
Run တော့ အောက်ပါလိုမျိုး error message တွေကို တွေ့ရ...  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./test-all-error-types.sh | tee test1.log
...
...
...
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1079.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1080.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1080.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1081.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1081.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1082.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1082.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1083.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1083.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1084.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1084.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1085.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1085.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1086.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1086.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1087.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1087.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1088.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1088.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1089.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1089.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1090.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1090.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1091.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1091.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1092.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1092.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1093.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1093.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1094.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1094.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1095.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1095.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1096.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1096.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1097.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1097.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1098.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1098.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1099.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1099.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1100.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1100.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1101.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1101.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1102.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1102.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1103.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1103.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1104.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1104.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1105.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1105.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1106.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1106.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1107.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1107.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1108.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1108.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1109.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1109.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1110.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1110.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1111.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1111.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1112.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1112.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1113.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1113.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1114.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1114.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1115.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1115.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1116.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1116.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1117.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1117.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1118.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1118.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1119.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1119.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1120.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1120.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1121.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1121.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1122.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1122.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1123.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1123.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1124.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1124.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1125.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1125.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1126.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1126.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1127.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1127.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1128.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1128.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1129.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1129.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1130.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1130.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1131.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1131.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1132.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1132.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1133.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1133.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1134.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1134.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1135.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1135.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1136.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1136.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1137.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1137.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1138.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1138.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1139.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1139.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1140.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1140.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1141.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1141.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1142.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1142.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1143.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1143.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1144.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1144.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1145.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1145.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1146.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1146.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1147.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1147.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1148.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1148.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1149.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1149.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1150.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 1150.
checked output:
 အဲ့ တော့ ဘယ် လို ပြော ရ
 သား ကို
 ကြီး ကြောက် လိုက် တာ
 ကျက် သ ရေ တုံး ကွန်
 ရှေး ရှေး ဘု ရင် တွေ
 လဲ ပါ တယ်
 မို့ တူ တရ်
 မုန့် ဟင်း ခါး တွေ ရ
 ဖြစ် တိုင်း စောက် ပြစ် တင်
 ကြား လောက် မုန့် ဟင်း ခါး ပွဲ များ
stack
start checking
input: stack.err.syl
RE file: stack.rule.uniq.RE
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
checked output:
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
typo
start checking
input: typo.err.syl
RE file: typo.rule.uniq.RE
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
checked output:
 သ မား က ဟာ အ
 ကြီး ပါ့ ဟယ်လ်
 တွေ ပါ့ ဟယ်လ်
 က တော့ မ သိ ခဲ့
 တောင်း ပန် အ စဉ်ု တ
 ကို လိုက် လျော မယ် ဆို
 ဆို ဂုဏ် ပြု ကိုယ် သာ ခံ
 လိုက် တာ ဈေး ကွက် ထဲ
ကို အ ခြေ
 ကျပ် ကို ဆို လို

real	21m43.270s
user	20m52.972s
sys	0m5.878s
```

အထက်ပါအတိုင်း error ထွက်နေပေမဲ့ လက်ရှိ rule နဲ့ pass လုပ်ထားတာကိုပဲ evaluation လုပ်ကြည့်ပြီး အလုပ်ဘယ်လောက် လုပ်သလဲ ဆိုတာကို တိုင်းတာကြည့်ချင်တယ်...  
   
## Evaluation on Automatic Extracted Rules
   
evaluation အတွက်က လောလောဆယ် F1-measure တွက်တဲ့ defecto script လိုဖြစ်နေတဲ့ အောက်ပါ python script ကိုပဲ သုံးထားတယ်။  
   
```python
#****************************************************************
#
# evaluate.py - the evaluation program.
#
# Author: Yue Zhang
#
# Computing lab, University of Oxford. 2006.11
#
#****************************************************************

#================================================================
#
# Import modules.
#
#================================================================

import sys
import os
sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), "..", "libs")))
import getopt

#----------------------------------------------------------------
#
# addTuples - add two tuples element by element.
#
# Inputs:  tuple1 - operand1
#          tuple2 - operand2
#
# Returns: tuple
#
#----------------------------------------------------------------

def addTuples(tuple1, tuple2):
   return tuple([tuple1[i]+tuple2[i] for i in xrange(len(tuple1))])

#----------------------------------------------------------------
#
# addListToList - add the second list to the first list.
#
# Inputs:  list1 - operand1, the one modified list
#          list2 - operand2, the list added 
#
#----------------------------------------------------------------

def addListToList(list1, list2):
   for i in xrange(len(list1)):
      list1[i] += list2[i]

#----------------------------------------------------------------
#
# subtractListFromList - subtract the second list from the first list.
#
# Inputs:  list1 - operand1, the one modified list
#          list2 - operand2, the list added 
#
#----------------------------------------------------------------

def subtractListFromList(list1, list2):
   for i in xrange(len(list1)):
      list1[i] -= list2[i]

#----------------------------------------------------------------
#
# dotProduct - compute the dot-product for lists/tuples.
#
# Inputs:  list1 - operand1
#          list2 - operand2
#
# Returns: int
#
#----------------------------------------------------------------

def dotProduct(list1, list2):
   nReturn = 0
   for i in xrange(len(list1)):
      nReturn += list1[i] * list2[i]
   return nReturn

#----------------------------------------------------------------
#
# addDictToDict - add a dictionary with int value to another dictionary
#
# Input: dict1 - operand1, the one that is added to
#        dict2 - operand2, the one to add
#
# Example:
# addDictToDict({'a':1,'b':2}, {'b':1,'c':2}) = {'a':1,'b':4,'c':2}
#
#----------------------------------------------------------------

def addDictToDict(dict1, dict2):
   for key in dict2:
      if key in dict1:
         dict1[key] += dict2[key]
      else:
         dict1[key] = dict2[key]

#----------------------------------------------------------------
#
# subtractDictFromDict - subtract a dictionary with int value from another dictionary
#
# Input: dict1 - operand1, the one that is modified to 
#        dict2 - operand2, the one to substract
#
# Example:
# subtractDictFromDict({'a':1,'b':2}, {'b':1,'c':2}) = {'a':1,'b':1,'c':-2}
#
#----------------------------------------------------------------

def subtractDictFromDict(dict1, dict2):
   for key in dict2:
      if key in dict1:
         dict1[key] -= dict2[key]
      else:
         dict1[key] = -dict2[key]

#================================================================
#
# CRawSentenceReader - the raw sentence reader
#
# This reader is aimed for Chinese. 
#
#================================================================

class CRawSentenceReader(object):

   #----------------------------------------------------------------
   #
   # __init__ - initialisation
   #
   # Inputs: sPath - the file for reading
   #
   #----------------------------------------------------------------

   def __init__(self, sPath, sEncoding="utf-8"):
      self.m_sPath = sPath
      self.m_oFile = open(sPath)
      self.m_sEncoding = sEncoding

   #----------------------------------------------------------------
   #
   # __del__ - destruction
   #
   #----------------------------------------------------------------

   def __del__(self):
      self.m_oFile.close()

   #----------------------------------------------------------------
   #
   # readNonEmptySentence - read the next sentence
   #
   # Returns: list of characters or None if the EOF symbol met.
   #
   #----------------------------------------------------------------

   def readNonEmptySentence(self):
      # 1. read one line
      sLine = "\n"                              # use a pseudo \n to start
      while sLine:                              # while there is a line
         sLine = sLine.strip()                  # strip the line
         if sLine:                              # if the line isn't empty
            break                               # break
         sLine = self.m_oFile.readline()        # read next line
         if not sLine:                          # if eof symbol met
            return None                         # return
      # 2. analyse this line
      uLine = sLine.decode(self.m_sEncoding)    # find unicode
      lLine = [sCharacter.encode(self.m_sEncoding) for sCharacter in uLine]
      return lLine

   #----------------------------------------------------------------
   #
   # readSentence - read the next sentence
   #
   # Returns: list of characters or None if the EOF symbol met.
   #
   #----------------------------------------------------------------

   def readSentence(self):
      # 1. read one line
      sLine = self.m_oFile.readline()           # read next line
      if not sLine:                             # if eof symbol met
         return None                            # return
      # 2. analyse this line
      uLine = sLine.strip().decode(self.m_sEncoding)    # find unicode
      lLine = [sCharacter.encode(self.m_sEncoding) for sCharacter in uLine]
      return lLine

#================================================================
#
# CPennTaggedSentenceReader - the tagged sentence reader
#
#================================================================

class CPennTaggedSentenceReader(object):

   #----------------------------------------------------------------
   #
   # __init__ - initialisation
   #
   # Inputs: sPath - the file for reading
   #
   #----------------------------------------------------------------

   def __init__(self, sPath):
      self.m_sPath = sPath
      self.m_oFile = open(sPath)

   #----------------------------------------------------------------
   #
   # __del__ - destruction
   #
   #----------------------------------------------------------------

   def __del__(self):
      self.m_oFile.close()

   #----------------------------------------------------------------
   #
   # readNonEmptySentence - read the next sentence
   #
   # Input: bIgnoreNoneTag - ignore _-NONE- tagged word?
   #
   # Returns: list of word, tag pairs or None if the EOF symbol met.
   #
   #----------------------------------------------------------------

   def readNonEmptySentence(self, bIgnoreNoneTag):
      # 1. read one line
      sLine = "\n"                              # use a pseudo \n to start
      while sLine:                              # while there is a line
         sLine = sLine.strip()                  # strip the line
         if sLine:                              # if the line isn't empty
            break                               # break
         sLine = self.m_oFile.readline()        # read next line
         if not sLine:                          # if eof symbol met
            return None                         # return
      # 2. analyse this line
      lLine = sLine.strip().split(" ")
      lNewLine = []
      for nIndex in xrange(len(lLine)):
         tTagged = tuple(lLine[nIndex].split("/"))
         if len(tTagged) >= 3:
            tTagged = ('/'.join(tTagged[:-1]), tTagged[-1])
         assert(len(tTagged)<3)
         if len(tTagged)==1:
            tTagged = (tTagged[0], "-NONE-")
         if (bIgnoreNoneTag==False) or (tTagged[0]): # if we take -NONE- tag, or if we find that the tag is not -NONE-
            lNewLine.append(tTagged)
      return lNewLine

   #----------------------------------------------------------------
   #
   # readNonEmptySentence - read the next sentence
   #
   # Input: bIgnoreNoneTag - ignore _-NONE- tagged word?
   #
   # Returns: list of word, tag pairs or None if the EOF symbol met.
   #
   #----------------------------------------------------------------

   def readSentence(self, bIgnoreNoneTag):
      # 1. read one line
      sLine = self.m_oFile.readline()           # read next line
      if not sLine:                             # if eof symbol met
         return None                            # return
      # 2. analyse this line
      lLine = sLine.strip().split(" ")
      lNewLine = []
      for nIndex in xrange(len(lLine)):
         tTagged = tuple(lLine[nIndex].split("/"))
         assert(len(tTagged)<3)
         if len(tTagged)==1:
            tTagged = (tTagged[0], "-NONE-")
         if (bIgnoreNoneTag==False) or (tTagged[0]): # if we take -NONE- tag, or if we find that the tag is not -NONE-
            lNewLine.append(tTagged)
      return lNewLine

#================================================================
#
# Global.
#
#================================================================

g_sInformation = "\nThe evaluation program for Chinese Tagger. \n\n\
  Yue Zhang 2006\n\
  Computing laboratory, Oxford\n\n\
evaluate.py candidate_text reference_text\n\n\
The candidate and reference text need to be files with tagged sentences. Each sentence takes one line, and each word is in the format of Word_Tag.\n\n\
"

#----------------------------------------------------------------
#
# evaluateSentence - evaluate one sentence
#
# Input: tCandidate - candidate sentence
#        tReference
#
# Return: int for correct words
#
#----------------------------------------------------------------

def evaluateSentence(lCandidate, lReference):
   nCorrectWords = 0
   nCorrectTags = 0
   nChar = 0
   indexCandidate = 0
   indexReference = 0
   while lCandidate and lReference:
      if lCandidate[0][0] == lReference[0][0]:  # words right
         nCorrectWords += 1
         if lCandidate[0][1] == lReference[0][1]: # tags 
            nCorrectTags += 1
         indexCandidate += len(lCandidate[0][0]) # move
         indexReference += len(lReference[0][0])
         lCandidate.pop(0)
         lReference.pop(0)
      else:
         if indexCandidate == indexReference:
            indexCandidate += len(lCandidate[0][0]) # move
            indexReference += len(lReference[0][0])
            lCandidate.pop(0)
            lReference.pop(0)
         elif indexCandidate < indexReference:
            indexCandidate += len(lCandidate[0][0])
            lCandidate.pop(0)
         elif indexCandidate > indexReference:
            indexReference += len(lReference[0][0]) # move
            lReference.pop(0)
   return nCorrectWords, nCorrectTags            

#================================================================
#
# Main.
#
#================================================================

if __name__ == '__main__':
   #
   # Parse command ......
   #
   opts, args = getopt.getopt(sys.argv[1:], "")
   for opt in opts:
      print opt
   if len(args) != 2:
      print g_sInformation
      sys.exit(1)
   sCandidate = args[0]
   sReference = args[1]
   if not os.path.exists(sCandidate):
      print "Candidate file %s does not exist." % sCandidate
      sys.exit(1)
   if not os.path.exists(sCandidate):
      print "Reference file %s does not exist." % sReference
      sys.exit(1)
   #
   # Compare candidate and reference
   #
   nTotalCorrectWords = 0
   nTotalCorrectTags = 0
   nCandidateWords = 0
   nReferenceWords = 0
   fReference = CPennTaggedSentenceReader(sReference); fCandidate = CPennTaggedSentenceReader(sCandidate)
   lReference = fReference.readNonEmptySentence(bIgnoreNoneTag=True); lCandidate = fCandidate.readNonEmptySentence(bIgnoreNoneTag=True)
   while lReference and lCandidate:
      n=len(lCandidate)
      nCandidateWords += len(lCandidate)
      nReferenceWords += len(lReference)
      nCorrectWords, nCorrectTags = evaluateSentence(lCandidate, lReference)
      nTotalCorrectWords += nCorrectWords
      nTotalCorrectTags += nCorrectTags
      lReference = fReference.readNonEmptySentence(bIgnoreNoneTag=True); lCandidate = fCandidate.readNonEmptySentence(bIgnoreNoneTag=True)

   if ( lReference and not lCandidate ) or ( lCandidate and not lReference ) : 
      print "Warning: the reference and the candidate consists of different number of lines!"

   word_precision = float(nTotalCorrectWords) / float(nCandidateWords)
   word_recall = float(nTotalCorrectWords) / float(nReferenceWords)
   tag_precision = float(nTotalCorrectTags) / float(nCandidateWords)
   tag_recall = float(nTotalCorrectTags) / float(nReferenceWords)
   word_fmeasure = (2*word_precision*word_recall)/(word_precision+word_recall)
   if tag_precision+tag_recall==0:
      tag_fmeasure = 0.0
   else:
      tag_fmeasure = (2*tag_precision*tag_recall)/(tag_precision+tag_recall)

   print "Tag precision:", tag_precision
   print "Tag recall:", tag_recall
   print "F-Measure:", tag_fmeasure

```
   
error type တစ်မျိုးစီအတွက် တွက်ကြည့်ဖို့ လိုအပ်တာကြောင့် eval.sh ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်...  
   
```
#!/bin/bash

echo "Checking with RE rules extracted from typo dictionary...";
for re in *.RE;
do
   re_file=${re%.*.*.*}; echo $re_file;
   
   echo "ref file: $re_file.sug.syl, hyp: $re_file.err.syl.chk";
   #python2.7 ./evaluate.py /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/suggestion/$re_file.sug.syl ./chk/$re_file.err.syl.chk
   python2.7 ./evaluate.py ./$re_file.sug.syl ./chk/$re_file.err.syl.chk
   #paste /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/suggestion/$re_file.sug.syl ./chk/$re_file.err.syl.chk > ./chk/$re_file.sug-chk
   paste ./$re_file.sug.syl ./chk/$re_file.err.syl.chk > ./chk/$re_file.sug-chk
   echo "==========";
   echo "";   
   
done
```

## Evaluation on Closed-Test Data

rule ဆွဲထုတ်ထားတဲ့ training data တွေရဲ့ အမှားတွေကိုပဲ spelling correction လုပ်ကြည့်တော့ ရလဒ်က အောက်ပါအတိုင်း ရရှိတယ်။  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./eval.sh | tee evaluation1.log
Checking with RE rules extracted from typo dictionary...
con
ref file: con.sug.syl, hyp: con.err.syl.chk
Tag precision: 0.965484521409
Tag recall: 0.962857818784
F-Measure: 0.964169381107
==========

dialect
ref file: dialect.sug.syl, hyp: dialect.err.syl.chk
Tag precision: 0.907079646018
Tag recall: 0.919282511211
F-Measure: 0.913140311804
==========

encode
ref file: encode.sug.syl, hyp: encode.err.syl.chk
Tag precision: 0.897810218978
Tag recall: 0.903204272363
F-Measure: 0.900499168053
==========

pho
ref file: pho.sug.syl, hyp: pho.err.syl.chk
Tag precision: 0.495717929125
Tag recall: 0.401380440809
F-Measure: 0.443588992194
==========

pho-typo
ref file: pho-typo.sug.syl, hyp: pho-typo.err.syl.chk
Tag precision: 0.94574227581
Tag recall: 0.941838649156
F-Measure: 0.94378642602
==========

sensitive
ref file: sensitive.sug.syl, hyp: sensitive.err.syl.chk
Tag precision: 0.979002624672
Tag recall: 0.958868894602
F-Measure: 0.968831168831
==========

seq
ref file: seq.sug.syl, hyp: seq.err.syl.chk
Tag precision: 0.939136272097
Tag recall: 0.941453566622
F-Measure: 0.940293491655
==========

short
ref file: short.sug.syl, hyp: short.err.syl.chk
Tag precision: 0.719117647059
Tag recall: 0.736445783133
F-Measure: 0.727678571429
==========

slang
ref file: slang.sug.syl, hyp: slang.err.syl.chk
Tag precision: 0.928456913828
Tag recall: 0.934449374748
F-Measure: 0.931443506232
==========

stack
ref file: stack.sug.syl, hyp: stack.err.syl.chk
Tag precision: 0.980607814761
Tag recall: 0.977777777778
F-Measure: 0.979190751445
==========

typo
ref file: typo.sug.syl, hyp: typo.err.syl.chk
Tag precision: 0.739071272709
Tag recall: 0.685772459449
F-Measure: 0.71142499764
==========


real	0m2.213s
user	0m0.856s
sys	0m0.060s
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

အထက်ပါ ရလဒ်က automatic extracted rule based approach ကိုပဲ closed-test data နဲ့ evaluation လုပ်ထားတာပါ။ ရလဒ်က ကောင်းပါတယ်။  
   
closed-test ဒေတာ ရဲ့ file size တွေက training data တွေရဲ့ ပမာဏနဲ့ အတူတူပါပဲ အောက်ပါအတိုင်းပါ။  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ wc ./*.err.syl
   3797   17815  166161 ./con.err.syl
     55     224    2139 ./dialect.err.syl
    376    1524   15575 ./encode.err.syl
  22789  101157 1004498 ./pho.err.syl
   3097   13252  129887 ./pho-typo.err.syl
     73     644    3293 ./sensitive.err.syl
   2058    9266   95698 ./seq.err.syl
    144     590    5370 ./short.err.syl
   1150    4546   46684 ./slang.err.syl
    789    3857   38102 ./stack.err.syl
  18677   81661  858050 ./typo.err.syl
  53005  234536 2365457 total
```

spelling correction လုပ်ခဲ့ပြီး သို့မဟုတ် spelling checked လုပ်ခဲ့ပြီး ပြန်ထွက်လာတဲ့ hyp ဖိုင်တွေရဲ့ ပမာဏကလည်း အထက်က intput လုပ်ခဲ့တဲ့ closed-test data အတိုင်းပဲ ပြန်ထွက်တာကို confirmation လုပ်ခဲ့တယ်။ အောက်ပါအတိုင်းပါ...  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ wc ./chk/*.chk
   3797   16908  165843 ./chk/con.err.syl.chk
     55     223    2150 ./chk/dialect.err.syl.chk
    376    1498   16045 ./chk/encode.err.syl.chk
  22789  124453 1506044 ./chk/pho.err.syl.chk
   3097   13325  139158 ./chk/pho-typo.err.syl.chk
     73     389    3587 ./chk/sensitive.err.syl.chk
   2058    8916   95402 ./chk/seq.err.syl.chk
    144     664    6530 ./chk/short.err.syl.chk
   1150    4958   50597 ./chk/slang.err.syl.chk
    789    3465   39603 ./chk/stack.err.syl.chk
  18676   87915  959037 ./chk/typo.err.syl.chk
  53004  262714 2983996 total
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```
   
## Evaluation on Open Test Data

ဒီတစ်ခါတော့ "open test data" နဲ့ နှိုင်းယှဉ်ကြည့်ချင်တယ်။  
အိဖြူဖြူမွန်က ပြင်ဆင်ထားတဲ့ open-test data ရဲ့ ပမာဏက အောက်ပါအတိုင်းပါ။  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ wc  /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/*.err.syl
   282   1293  11726 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/con.err.syl
     8     31    298 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/dialect.err.syl
    32    127   1226 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/encode.err.syl
  2096   9122  89403 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/pho.err.syl
   270   1142  11207 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/pho-typo.err.syl
    11     70    342 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/sensitive.err.syl
   206    922   9489 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/seq.err.syl
    16     64    580 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/short.err.syl
   127    500   5066 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/slang.err.syl
   109    513   4860 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/stack.err.syl
  2205   9341  96377 /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/typo.err.syl
  5362  23125 230574 total
```
   
Open-test ဒေတာကို သုံးပြီး automatic extracted rules တွေနဲ့ spelling correction လုပ်တဲ့အခါမှာလည်း closed-test နဲ့ testing လုပ်တုန်းကလိုပဲပေးတဲ့ error message တွေကို အောက်ပါအတိုင်း ထပ်မံတွေ့ရှိရပါတယ်။ ဖြစ်နိုင်တာက တချို့စာလုံးတွေကို escape မလုပ်ပဲနဲ့ "s/search/replace/g" ဆိုတဲ့ regular expression pattern ထဲကို တိုက်ရိုက် pass လုပ်လို့ ပေးတဲ့ error တွေလားလို့...  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ time ./test-all-error-types-open.sh | tee testing2-open-test-data.log
...
...
...
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 86.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 86.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 87.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 87.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 88.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 88.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 89.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 89.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 90.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 90.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 91.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 91.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 92.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 92.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 93.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 93.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 94.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 94.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 95.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 95.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 96.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 96.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 97.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 97.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 98.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 98.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 99.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 99.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 100.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 100.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 101.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 101.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 102.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 102.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 103.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 103.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 104.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 104.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 105.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 105.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 106.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 106.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 107.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 107.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 108.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 108.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 109.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 109.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 110.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 110.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 111.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 111.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 112.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 112.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 113.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 113.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 114.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 114.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 115.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 115.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 116.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 116.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 117.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 117.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 118.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 118.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 119.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 119.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 120.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 120.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 121.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 121.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 122.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 122.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 123.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 123.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 124.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 124.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 125.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 125.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 126.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 126.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/မျိုး သ { <-- HERE +သူ+} တောင်း လား လို/ at ./correction-with-RE.pl line 32, <$errorFILE> line 127.
Unescaped left brace in regex is passed through in regex; marked by <-- HERE in m/လေ သောက် { <-- HERE +စောက်+} ကျိုး နဲ ဆ/ at ./correction-with-RE.pl line 32, <$errorFILE> line 127.
checked output:
ဘာ တွေ ဖျင် နာ နေ
ငါ နက် မုန့် ဈေး
လှ ပြီး ကို ရီး ယား ဆန်
တွေ က စောင် ပေါ အ
လိုက် အုံး ညီ ဆီ
ပူ ပါ နဲ့
ဟာ ဂယ် ရီး
လား ဂယ် ကြီး
သ နား ဈ ကိုယ်
ဘွ
stack
start checking
input: stack.err.syl
RE file: stack.rule.uniq.RE
လက် ခ ဏာ ထူး
တွေ ကိတ် စ ဘယ် လို
တာ နဲ့ မင် က လာ ပါ
ကျမ္မာ ရေးဋ္ဌာ
မ ယု ကိစ် စ က
အ ကျီ် တွေ
စ ရာ လ ကာ် ဒီ ပ
ယ ခု ကိ စ ကို ထိ
ယ ခု ကိ စ ကို အ
ဟုတ် ကု ပ ဏီ က
checked output:
လက္ခ ဏာ ထူး
တွေ ကိတ် စ ဘယ် လို
တာ နဲ့ မင် က လာ ပါ
ကျမ္မာ ရေးဋ္ဌာ
မ ယု ပြီ ကိစ္စ က
အ ကျီ် တွေ
စ ရာ လ ကာ် ဒီ ပ
ယ ခု ကိ စ ကို ထိ
ယ ခု ကိ စ ကို အ
ဟုတ် ကု ပ ဏီ က
typo
start checking
input: typo.err.syl
RE file: typo.rule.uniq.RE
လုံး ခင် ဗျာ ကို ယုံ
က တော့ နိုင်
ကြ တာ ခူ ထက် ထိ
နဲ့ ကြည့်ရ် အောက် ပါ
မ သိ တ ပါ ဆ
နော က ၁ ၀
မယ် လို့ ခန် မှန်း တာ
တိုင် ယာ ခင် ထဲ ဆင်း
ရိက္ခာ ထောက် ပံ ရေး ကော်
ရှိ လို့ ကုန်း စျေး
checked output:
လုံး ခင် ဗျာ့ား့ာာ ကို ယုံ
က တော့ နိုင်
ကြ တာ ဟာ ခူ ထက် ထိ
နဲ့့ ကြည့်ရ် အောက် ပါ့
မ သိ တ ပါ့ ဆ
နေ့ာ က ၁ ၀
မယ် လို့ ခန် မှန်း တာ
တိုင် ယာ ခင် က တည်း ဆင်း
ရိက္ခာ ထောက် ပံ ရေး ကော်
ရှိ လို့ ကုန်း အ စဉ်ျေး

real	2m7.686s
user	2m6.685s
sys	0m0.085s
```
   
spelling correction လုပ်ပြီး ပြန်ထွက်လာတဲ့ output ဖိုင်တွေရဲ့ file size ကိုလည်း ပြန်တိုင်းကြည့်ခဲ့ပါတယ်။ input လုပ်လိုက်တဲ့အတိုင်းပဲ output ပြန်ထွက်တာမို့ evaluation လုပ်တဲ့အခါမှာ error မပေးလောက်ပါဘူး...  
   
```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ wc ./chk-open-test/*.chk
   282   1259  11755 ./chk-open-test/con.err.syl.chk
     8     31    301 ./chk-open-test/dialect.err.syl.chk
    32    126   1231 ./chk-open-test/encode.err.syl.chk
  2096  11192 132789 ./chk-open-test/pho.err.syl.chk
   270   1155  12015 ./chk-open-test/pho-typo.err.syl.chk
    11     55    360 ./chk-open-test/sensitive.err.syl.chk
   206    920   9487 ./chk-open-test/seq.err.syl.chk
    16     69    660 ./chk-open-test/short.err.syl.chk
   127    513   5289 ./chk-open-test/slang.err.syl.chk
   109    505   4987 ./chk-open-test/stack.err.syl.chk
  2205  10073 107594 ./chk-open-test/typo.err.syl.chk
  5362  25898 286468 total
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ 
```
   
## Manually Extracted Rules vs. Automatic Extracted Rules
     
လက်ရှိ experiment လုပ်လို့ ရထားတဲ့ ရလဒ်တွေကိုပဲ အခြေခံပြီး လက်နဲ့ဆောက်ထားတဲ့ spelling correction rules တွေနဲ့ အထက်မှာ လုပ်ပြခဲ့တဲ့အတိုင်း automatic extracted rules တွေအကြား ရလဒ်က ဘယ်လိုနေသလဲ ဆိုတာကို နှိုင်းယှဉ်ကြည့်ခဲ့တယ်။ ပြီးတော့ relative score ကိုလည်း သိရအောင် reference data နဲ့ ဘာမှ correction မလုပ်ရသေးတဲ့ test data (i.e. error data) ကိုလည်း F-measure အရင်ဆုံး လုပ်ခဲ့။ အဲဒါကြောင့် အောက်ပါ ရလဒ်တွေမှာ ပထမဆုံး လိုင်းက F-measure of original test input data, ဒုတိယလိုင်းက F-measure of manual rules နဲ့ တတိယလိုင်းက F-measure of automatic extracted rules တွေပါ။  
   
```
evaluation with error or input file: con.err.syl, F-Measure: 0.726195179771
evaluation on manual Rule-based hyp: con.err.hyp.syl, F-Measure: 0.853697749196
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: dialect.err.syl, F-Measure: 0.709677419355
evaluation on manual Rule-based hyp: dialect.err.hyp.syl, F-Measure: 0.838709677419
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: encode.err.syl, F-Measure: 0.599190283401
evaluation on manual Rule-based hyp: encode.err.hyp.syl, F-Measure: 0.603305785124
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: pho.err.syl, F-Measure: 0.739413859217
evaluation on manual Rule-based hyp: pho.err.hyp.syl, F-Measure: 0.775632635253
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: pho-typo.err.syl, F-Measure: 0.735783027122
evaluation on manual Rule-based hyp: pho-typo.err.hyp.syl, F-Measure: 0.87993064586
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: sensitive.err.syl, F-Measure: 0.486956521739
evaluation on manual Rule-based hyp: sensitive.err.hyp.syl, F-Measure: 0.850574712644
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: seq.err.syl, F-Measure: 0.687465790914
evaluation on manual Rule-based hyp: seq.err.hyp.syl, F-Measure: 0.877270225647
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: short.err.syl, F-Measure: 0.69696969697
evaluation on manual Rule-based hyp: short.err.hyp.syl, F-Measure: 0.721804511278
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: slang.err.syl, F-Measure: 0.624399615754
evaluation on manual Rule-based hyp: slang.err.hyp.syl, F-Measure: 0.767097966728
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: stack.err.syl, F-Measure: 0.690010298661
evaluation on manual Rule-based hyp: stack.err.hyp.syl, F-Measure: 0.712384851586
evaluation on automatic extracted Rule-based approach, F-Measure: 

evaluation with error or input file: typo.err.syl, F-Measure: 0.723285912932
evaluation on manual Rule-based hyp: typo.err.hyp.syl, F-Measure: 0.747112917023
evaluation on automatic extracted Rule-based approach, F-Measure: 

```
ရလဒ်တွေကို နှိုင်းယှဉ်ကြည့်တော့ automatic extracted rule-based approach က အများစုမှာ manually extracted rule-based approach ထက် ရလဒ်ကောင်း ပေးနိုင်တာကို တွေ့ရတယ်။ သို့သော် error type နှစ်မျိုးမှာတော့ (i.e. pho and typo) manual ဆွဲထုတ်ထားတဲ့ rule တွေက ပိုအားသာတာကို တွေ့ရတယ်။ အသေးစိတ် လေ့လာဖို့ လိုအပ်...  
   
## Error Analysis
   
တကယ်တမ်း manual rule-based နဲ့ automatic extracted rule-based နှစ်ခုအကြား spelling correction က ဘယ်လိုတွေဖြစ်နေတယ်၊ ဘယ်လိုတွေ ကွာခြားနေတာလဲ ဆိုတာကို သိရအောင် error|||manual|||automatic ဆိုတဲ့ format ချပြီး နှိုင်းယှဉ်ကြည့်ခဲ့တယ်။ စာကြောင်းရေတိုင်းကို ဒီနေရာမှာ ပြဖို့ခက်ပေမဲ့ Error Analysis လုပ်ခဲ့တာကို မြင်သာအောင်၊ လက်တွေ့ ဘယ်လိုတွေကွာနေတယ် ဆိုတာကို သိသာအောင် head နဲ့ပဲ ဖြစ်ဖြစ် ကြည့်ကြည့် ကြရအောင်။  
   

   
## Debugging 
   
အထက်မှာ မြင်ခဲ့ရတဲ့ error တွေက escape လုပ်ဖို့ လိုအပ်တဲ့ စာလုံးတွေကို escape မလုပ်ပဲနဲ့ "s/search/replace/" ဆိုတဲ့ Regular Expression pattern ထဲကို တိုက်ရိုက် pass လုပ်လို့ ဖြစ်တဲ့ error တွေလားလို့...။ သေချာအောင် debugging လုပ်ကြည့်ခဲ့တယ်။  
   
