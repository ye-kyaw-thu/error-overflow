## Split Word and Tag Files

```
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ ./mk-wordtag.pl ./myPOSTaged.txt "\/" w > myPOSTaged.word
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ ./mk-wordtag.pl ./myPOSTaged.txt "\/" t > myPOSTaged.tag
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
...
...
...
```

## Check the Splitted Files

```
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ head myPOSTaged.word 
ဒီ ဆေး က ၁၀၀ ရာခိုင်နှုန်း ဆေးဘက်ဝင် အပင် များ မှ ဖော်စပ် ထား တာ ဖြစ် တယ်
အသစ် ဝယ် ထား တဲ့ ဆွယ်တာ က အသီး ထ နေ ပါ ပေါ့
မ ကျန်းမာ လျှင် နတ် ဆရာ ထံ မေးမြန်း ၍ သက်ဆိုင်ရာ နတ် တို့ အား ပူဇော်ပသ ရ သည်
ပေဟိုင် ဥယျာဉ်
နဝမ အိပ်မက် ကောသလ မင်း အိပ်မက် ၉ နက်ရှိုင်း ကျယ်ဝန်း သော ရေကန် ကြီး တစ် ခု တွင် သတ္တဝါ တို့ ဆင်း ၍ ရေသောက် ကြ ၏
အပြင်ပန်း ကြည့် ရင် ခက် သလို ထင် ရ ပေမယ့် တကယ့် လက်တွေ့ အခြေအနေ က တော့ အဲဒီ လို မ ဟုတ် ပါ ဘူး
8 bit ပုံရိပ် တစ် ခု သည် 256 color သို့မဟုတ် gray scale များ ကို အထောက်အကူ ပြု သည်
ကိုရီးယား ဝတ်စုံ မှာ ပန်း ဒီဇိုင်း နဲ့ အဝါရောင် က လိုက်ဖက် လိမ့် မယ် ထင် တယ်
သို့နှင့် မဂ္ဂဇင်း မှ တစ်ဆင့် သတင်းစာ ကို ပါ တိုးချဲ့ လိုက် သောအခါ တွင် ဘက်ပတစ် ကျောင်း သို့ မ ပြန် တော့ ဘဲ ထို မဂ္ဂဇင်း သတင်းစာ နှစ် ခု စလုံး တွင် ပင် တည်းဖြတ် သည့် ဘက် မှ ဆက်လက် လုပ်ကိုင် လေ တော့ သည်
တစ် ကျပ်သား
```

```
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ head myPOSTaged.tag
B O O O O O O O O O N N N E
B O O O O O O N N N E
B O O O O O O O O O O N N N E
B E
B O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O O N N N E
B O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B E
```

## Number of Words are Different

```
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ wc myPOSTaged.word 
  43353  509784 7290137 myPOSTaged.word
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ wc myPOSTaged.tag 
  43353  509565 1021390 myPOSTaged.tag
```

## Error Lines

```
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$ ./mk-wordtag.pl ./myPOSTaged.txt "\/" t > myPOSTaged.tag
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1587.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1588.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1588.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1592.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1592.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1643.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1646.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1659.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1660.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 1697.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2268.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2270.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2274.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2289.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2290.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2290.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2290.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2292.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2296.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2328.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2341.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2342.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2343.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2346.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2359.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2362.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2379.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2398.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2405.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2405.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2405.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2405.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2421.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2453.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2467.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2470.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2470.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 2476.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 3391.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 5492.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7026.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7212.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7233.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7649.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7666.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7821.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 7821.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 8472.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10416.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10428.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10443.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10519.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10519.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10519.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10525.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10624.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10625.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10629.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10629.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10680.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10714.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10757.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10759.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 10759.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 14467.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 15833.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 15907.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 15958.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16124.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16138.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16141.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16147.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16656.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16944.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16945.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 16951.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 17207.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 17937.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 17943.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19039.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19039.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19039.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19040.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19121.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19195.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19212.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19254.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19257.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19419.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19624.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19624.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19624.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19745.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19745.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19745.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19747.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19751.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19751.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19801.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19801.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19804.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19817.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19835.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19880.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19880.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 19880.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20066.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20066.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20067.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20108.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20122.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20122.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20125.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20130.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20157.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20175.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20175.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20198.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 20199.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21017.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21328.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21351.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21478.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21478.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21479.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21480.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21480.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21481.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21482.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21486.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21535.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21536.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21553.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21553.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21571.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21589.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21589.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21613.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21828.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 21830.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24042.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24263.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24446.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24447.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24452.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24503.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24503.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24519.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24521.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24537.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24555.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24626.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24629.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24629.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24633.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24633.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24684.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24687.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24764.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24773.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24848.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24861.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 24864.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 25317.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29079.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29091.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29167.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29180.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29188.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29255.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29258.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29264.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29366.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29366.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29366.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29371.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29371.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29371.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29371.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29422.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29422.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29425.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29438.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29455.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29474.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29500.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29500.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 29980.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 30732.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 30753.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 30994.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31019.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31019.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31092.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31130.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31149.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31149.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31151.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31156.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31190.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31205.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 31283.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 34635.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 35029.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 37176.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 37265.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 37267.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 37958.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38056.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38332.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38348.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38349.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38997.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 38997.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 39054.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 39077.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 39166.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 39175.
Use of uninitialized value $tag in concatenation (.) or string at ./mk-wordtag.pl line 58, <$inputFILE> line 42787.
(base) ye@ykt-pro:/media/ye/project1/paper/isai-nlp2022/conf/thura/9Aug2022/preprocess$
```

## Error Example

```
ဥရောပ/n ကို/ppm တစ်/tn ခါ/part လောက်/part သွား/v ကြည့်/part ချင်/part တယ်/ppm ။/punc
ဥရောပ/B ကို/O တစ်/O ခါ/O လောက်/O သွားNN ကြည့်/NEချင်/N တယB/E
```

```
ဓူဝံ/n|ကြယ်/n သည်/ppm ကမ္ဘာ/n မှ/ppm အလင်းနှစ်/n ပေါင်း/n ၄၃၀/num ကွာဝေး/v သည်/ppm ။/punc
ဓူဝံ/B ကBယ်/O သည်/O ကမ္ဘာ/O မှ/O အလင်းနှစ်/O ပေါင်း/N ၄၃၀NN ကွာဝေE/N သညB/E
```

```
စာအုပ်/n ဝယ်/v ဖို့/part အထူးတလည်/adv ရည်ရွယ်/v ပြီး/conj သွား/v ခဲ့/part ပေမဲ့/conj တံခါး/n ပိတ်ထား/v ခဲ့/part တယ်/ppm ။/punc
စာအုပ်/B ဝယ်/O ဖို့/O အထူးတလည်/O ရည်ရွယ်/O ပြီး/O သွား/O ခဲ့/O ပေမဲ့/E တံခါး/N ပိတB ား/N ခဲ့/N တယ်/N
```

```
စာအုပ်/n ဝယ်/v ဖို့/part အထူးတလည်/adv ရည်ရွယ်/v ပြီး/conj သွား/v ခဲ့/part ပေမဲ့/conj တံခါး/n ပိတ်ထား/v ခဲ့/part တယ်/ppm ။/punc
စာအုပ်/B ဝယ်/O ဖို့/O အထူးတလည်/O ရည်ရွယ်/O ပြီး/O သွား/O ခဲ့/O ပေမဲ့/E တံခါး/N ပိတB ား/N ခဲ့/N တယ်/N
```

```
ကျွန်တော်/pron ဒါ/pron ကို/ppm မ/part ကြိုက်/v ဘူး/part ။/punc
ကျွန်တော်/B ဒN/O ကို/N မNN ကြိုကE/N ဘူး/E
```

```
ဒီ/pron ကလေး/n ကြောင့်/ppm စိတ်မော/v ရ/part တယ်/ppm ။/punc
ဒီ/B ကလေး/O ကြောင့်NN စိတNမော/NNရ/N Eယ်/E
```

```
သူ/pron တို့/part အားလုံး/adj အာကာသ/n ကို/ppm ပျံသန်း/v ချင်/part တယ်/ppm ။/punc
သူ/B တို့/O အားလုံး/O အာကာသ/O ကို/N ပျံသန်း/N ချင်EN တယ်/E
```

```
ကျန်/v တာ/part ခင်ဗျား/pron မိတ်ဆွေ/n ကို/ppm ပြန်ယူ/v သွား/part ခိုင်း/part ပါ/part ။/punc
ကျန်B  တာ/O Nင်ဗျားNO မိတ်ဆွေNO ကို/E ပြန်ယူ/B သွား/N ခိုင်း/N ပါ/E
```

```
၎င်း/adj အစီအစဉ်/n မှာ/ppm ဗြိတိသျှ/n|နယ်ချဲ့/n|စနစ်/n ကို/ppm တပြည်လုံး/n တွင်/ppm ဆန့်ကျင်/v ရန်/conj ၊/punc ဤ/adj လှုပ်ရှား/v|မှု/part ကို/ppm ကမ္ဘာ့/n|အခြေအနေ/n ဗမာ့/n|အခြေအနေ/n နှင့်/ppm အညီ/adv တစ်စတစ်စ/adv တိုးချဲ့/v ရန်/conj ၊/punc မြို့/n နေ/v အလုပ်သမား/n တော/n နေ/v အလုပ်သမား/n တို့/part ၏/ppm ဒေသ/n အလိုက်/ppm သပိတ်/n များ/part မှ/conj စ/v ၍/conj အထွေထွေသပိတ်/n များ/part ၊/punc အခွန်အခ/n|ပေး/v|ရေး/part|သပိတ်/n များ/part အထိ/ppm တိုးချဲ့/v ဆင်နွှဲ/v ရန်/conj ၊/punc တက်ကြွ/v လာ/part သော/part ဝါဒ/n|ဖြန့်ချိ/v|မှု/part များ/part ဖြစ်/v သည့်/part လူထု/n|ဆန္ဒပြပွဲ/n များ/part ချီတက်ပွဲ/n များ/part မှ/ppm စ/v ၍/conj ပြည်သူ/n တို့/part ၏/ppm အာဏာ/n|ဖီဆန်/v|ရေး/part|တိုက်ပွဲ/n အထိ/ppm ဆက်လက်/adv ဆင်နွှဲ/v ရန်/conj ၊/punc စီးပွား/n|ရေး/part အရ/ppm တွင်/ppm လည်း/part ဗြိတိသျှ/n|ကုန်ပစ္စည်း/n များ/part ကို/ppm သပိတ်မှောက်/v ရာ/conj မှ/conj စ/v ၍/conj လူထု/n နှင့်/ppm ချီ/part ၍/conj အခွန်/n|မ/part|ပေး/v|ရေး/part|တိုက်ပွဲ/n အထိ/ppm ဆင်နွှဲ/v ရန်/conj စစ်ဖက်/n|အုပ်ချုပ်/v|ရေး/part ဖက်/part နှင့်/conj ပုလိပ်/n ဖက်/part ကင်းစခန်း/n များ/part ဆက်သွယ်/v|ရေး/part|လမ်းကြောင်း/n များ/part ကို/ppm ပြောက်ကျား/n နည်း/n နှင့်/ppm ဝင်ရောက်/v တိုက်ခိုက်/v ၍/conj ဗမာ/n|ပြည်/n အတွင်း/n ဗြိတိသျှ/n|အုပ်ချုပ်/v|မှု/part|စနစ်/n ကို/ppm လုံးဝ/adv သွက်ချာပါလိုက်/v သည်/ppm အထိ/ppm တိုက်ပွဲ/n ဆင်နွှဲ/v ရန်/conj ၊/punc ထိုအခါ/conj ကမ္ဘာ/n ဖြစ်ပေါ်/v|တိုးတက်/v|မှု/part နှင့်/ppm တစ်ပြိုင်နက်/adv နောက်ဆုံးပိတ်/n အာဏာသိမ်းပွဲ/n ကို/ppm ဆင်နွှဲ/v ရန်/conj အစီအစဉ်/n ပင်/part ဖြစ်/v သည်/ppm ။/punc
၎င်းNB အစီEစဉ်/O မှာ/O ဗြBတိသျှ/O နယ်ချဲ့/O စနစ်/O ကို/O တပြည်လုံး/O တွင်/O ဆန့်ကျင်/O ရန်/O ဤ/O လှုပ်ရှား/O မှု/O ကို/O ကမ္ဘာ့/O အခြေအနေ/O ဗမာ့/O အခြေအနေ/O နှင့်/O အညီ/O တစ်စတစ်စ/O တိုးချဲ့/O ရန်/O မြို့/O နေ/O အလုပ်သမား/O တော/O နေ/O အလုပ်သမား/O တို့/O ၏/O ဒေသ/O အလိုက်/O သပိတ်/O များ/O မှ/O စ/O ၍/O အထွေထွေသပိတ်/O များ/O အခွန်အခ/O ပေး/O ရေး/O သပိတ်/O များ/O အထိ/O တိုးချဲ့/O ဆင်နွှဲ/O ရန်/O တက်ကြွ/O လာ/O သော/O ဝါဒ/O ဖြန့်ချိ/O မှု/O များ/O ဖြစ်/O သည့်/O လူထု/O ဆန္ဒပြပွဲ/O များ/O ချီတက်ပွဲ/O များ/O မှ/O စ/O ၍/O ပြည်သူ/O တို့/O ၏/O အာဏာ/O ဖီဆန်/O ရေး/O တိုက်ပွဲ/O အထိ/O ဆက်လက်/O ဆင်နွှဲ/O ရန်/O စီးပွား/O ရေး/O အရ/O တွင်/O လည်း/O ဗြိတိသျှ/O ကုန်ပစ္စည်း/O များ/O ကို/O သပိတ်မှောက်/O ရာ/O မှ/O စ/O ၍/O လူထု/O နှင့်/O ချီ/O ၍/O အခွန်/O မ/O ပေး/O ရေး/O တိုက်ပွဲ/O အထိ/O ဆင်နွှဲ/O ရန်/O စစ်ဖက်/O အုပ်ချုပ်/O ရေး/O ဖက်/O နှင့်/O ပုလိပ်/O ဖက်/O ကင်းစခန်း/O များ/O ဆက်သွယ်/O ရေး/O လမ်းကြောင်း/O များ/O ကို/O ပြောက်ကျား/O နည်း/O နှင့်/O ဝင်ရောက်/O တိုက်ခိုက်/O ၍/O ဗမာ/O ပြည်/O အတွင်း/O ဗြိတိသျှ/O အုပ်ချုပ်/O မှု/O စနစ်/O ကို/O လုံးဝ/O သွက်ချာပါလိုက်/O သည်/O အထိ/O တိုက်ပွဲ/O ဆင်နွှဲ/O ရန်/O ထိုအခါ/O ကမ္ဘာ/O ဖြစ်ပေါ်/O တိုးတက်/O မှု/O နှင့်/O တစ်ပြိုင်နက်/O နောက်ဆုံးပိတ်/O အာဏာသိမ်းပွဲ/O ကို/O ဆင်နွှဲ/O ရန်/O အစီအစဉ်/N ပင်/N ဖြစ်/N သည်/E
```

```
ဘယ်လို/adv ပဲ/part ကြည့်/v ကြည့်/v ရုပ်ရှင်မင်းသား/n နဲ့/ppm တူ/v တယ်/ppm ။/punc
ဘယ်လိုNB ပဲ/N ကြည့်/E ကြည့်/O ရုပBရှင်မင်းသား/N နဲ့/N တူ/N တယ်/E
```

```
မင်း/pron ရဲ့/ppm လစာ/n က/ppm အိမ်/n ကို/ppm ပို့/v ပေး/part လား/part ။/punc
မင်း/B ရဲ့/O လစာ/O က/O/O ကို/N ပို့/N ပE
```

```
စစ်/n|ခေါင်းဆောင်/n သန်းရွှေ/n နှင့်/conj စစ်/n|အစိုးရ/n ၏/ppm ဆိုင်ကလုန်း/n|နာဂစ်/n|ဒဏ်/n ခံ/v|ရ/part|သော/part|သူ/n များ/part အား/ppm အကူအညီ/n|ပေး/v|ခြင်း/part ကို/ppm တားမြစ်/v|ခြင်း/part အား/ppm ထင်ရှား/v သော/part တု့ံပြန်/v|မှု/part တစ်/tn ရပ်/part အဖြစ်/n အပြည်ပြည်/n|ဆိုင်ရာ/n လူ့/n|အဖွဲ့အစည်း/n များ/part မှ/ppm နေ/v ၍/conj မြန်မာ/n|နိုင်ငံ/n ၏/ppm အပြင်းထန်ဆုံး/adj ရိုက်ခတ်/v|ခြင်း/part ခံ/v ရ/part သည့်/part နေရာ/n|ဒေသ/n များ/part သို့/ppm အကူအညီ/n များ/part ရောက်/v ရှိ/part စေရန်/conj လူသား/n|ချင်း/part|စာနာ/v|ထောက်ထား/v သည့်/part ဝင်ရောက်/v|စွက်ဖက်/v|မှု/part တစ်/tn ရပ်/part ကို/ppm တောင်းဆို/v ခဲ့/part သည်/ppm ။/punc
စစ်/B ခေါင်းဆောင်/O သန်းရွှေ/O နှင့်/O စစ်/ONအစိုးရ/OE၏/O ဆိုင်Bလုန်း/N နာဂစ်/E ဒဏ်/O ခံ/B ရ/ONသော/O သူEO မျာB/O အား/O အကူအညီ/O ပေး/O ခြင်း/O ကို/O တားမြစ်/O ခြင်း/O အား/O ထင်ရှား/O သော/O တု့ံပြန်/O မှု/O တစ်/O ရပ်/O အဖြစ်/O အပြည်ပြည်/O ဆိုင်ရာ/O လူ့/O အဖွဲ့အစည်း/O များ/O မှ/O နေ/O ၍/O မြန်မာ/O နိုင်ငံ/O ၏/O အပြင်းထန်ဆုံး/O ရိုက်ခတ်/O ခြင်း/O ခံ/O ရ/O သည့်/O နေရာ/O ဒေသ/O များ/O သို့/O အကူအညီ/O များ/O ရောက်/O ရှိ/O စေရန်/O လူသား/O ချင်း/O စာနာ/O ထောက်ထား/O သည့်/O ဝင်ရောက်/O စွက်ဖက်/O မှု/O တစ်/O ရပ်/O ကို/N တောင်းဆို/N ခဲ့/N သည်/E
```

```
ဒီ/adj ဒေသ/n ရဲ့/ppm ကိုယ်စားပြု/n ထွက်ကုန်/n က/ppm တော့/part စပျစ်သီး/n ပါ/part ။/punc
ဒီ/B ဒေသ/O ရဲ့/O ကိုယ်စားပြု/O ထွက်ကုန်/O EN တော့/N စပျစ်သီး/N ပါ/E
```

```
လူ/n ရှေ့/n မှာ/ppm အရှက်/n ရ/v စေ/part သည်/ppm ။/punc
လူ/B ရှေ့/O မှာ/O အရှက်/N ရ/N စေBN သည်/E
```

```
သို့သော်လည်း/conj သတိထား/v ရ/part မည်/ppm မှာ/ppm စစ်/n|အစိုးရ/n သည်/ppm နိုင်ငံ/n နာမည်/n အား/ppm မြန်မာ/n လို/ppm နိုင်ငံ/n ၏/ppm အမည်/n ကို/ppm ပြောင်း/v|ခြင်း/part မ/part ဟုတ်/v ဘဲ/part အင်္ဂလိပ်/n လို/ppm သာ/part ပြောင်းလဲ/v|ခြင်း/part သာ/part ဖြစ်/v သည်/ppm ။/punc
သို့သော်လည်း/B သတိထား/O E  မည်/O မBာ/O စစ်/O အစိုးရ/O သည်/O နိုင်ငံ/O နာမည်/O အား/O မြန်မာ/O လို/O နိုင်ငံ/O ၏/O အမည်/O ကို/O ပြောင်း/O ခြင်း/O မ/O ဟုတ်/O ဘဲ/O အင်္ဂလိပ်/O လို/O သာ/O ပြောင်းလဲ/O ခြင်း/N သာ/N ဖြစ်/N သည်/E
```

```
ထို/pron မှ/ppm တစ်ဆင့်/adv BASIC/fw interpreter/fw အဖြစ်/n အသုံးပြု/v နိုင်/part ခဲ့/part သည်/ppm ။/punc
ထို/B မှ/O တစ်ဆင့်/O BASIC/O interpreter/O အဖြစ်/O အသုံးပြု/N နိုင်
```

```
ဝက်ဝံ/n ကလေး/part များ/part ကို/ppm မွေးဖွား/v ရာတွင်/conj များသောအားဖြင့်/adv နှစ်/tn ကောင်/part သာ/part မွေး/v လေ့/part ရှိ/v သည်/ppm ။/punc
ဝက်ဝံ/B ကလေး/O များ/O ကိN/O မွေးဖွEး/O ရာတBင်/O မNားသောအ/Eဖြင့်/O နှစ်/B ကောင်NO သာ/OEမွေး/NBလေ့/N ရှိ/N သည်/E
```

```
ပင်လယ်လိပ်/n များ/part ၌/ppm အထီး/n များ/part သည်/ppm ရေ/n နှင့်/ppm မ/part ခွဲခွာ/v ဘဲ/part နေ/v ကြ/part သော်လည်း/conj လိပ်မ/n များ/part မှာ/ppm မူ/part သဲ/n ပေါ/adj သော/part ကမ်းစပ်/n ၌/ppm ဖြစ်စေ/conj ၊/punc လူသူ/n မ/part ရောက်/v သော/part ကျွန်း/n များ/part ၌/ppm ဖြစ်စေ/conj ဥ/n များ/part ကို/ppm ဥ/v ရန်/part လာရောက်/v ကြ/part ၏/ppm ။/punc
ပင်လယ်လိပ်/B မျNး/O ၌EO အထီB/O များ/O သည်/O ရေ/O နှင့်/O မ/O ခွဲခွာ/O ဘဲ/O နေ/O ကြ/O သော်လည်း/O လိပ်မ/O များ/O မှာ/O မူ/O သဲ/O ပေါ/O သော/O ကမ်းစပ်/O ၌/O ဖြစ်စေ/O လူသူ/O မ/O ရောက်/O သော/O ကျွန်း/O များ/O ၌/O ဖြစ်စေ/O ဥ/O များ/O ကို/O ဥ/O ရန်/N လာရောက်/N ကြ/N ၏/E
```

```
ချွေး/n အရမ်း/adv ထွက်/v လို့/part ကိုယ်/n က/ppm စေးကပ်ကပ်/adv ဖြစ်/v နေ/part တယ်/ppm ။/punc
ရုရှား/n ။/punc
ဇွန်း/n ကို/ppm လိုအပ်/v တယ်/ppm ။/punc
ချွေး/B အရမ်း/O ထွက်/O လို့/O ကိုယ်/O က/O စေးကပ်ကပ်NN ဖြစE/N နေ/N တယ်/BNဇွန်း/BEကို/N လိBအပ်/N တယ်/E
```
(ဒီအမှားမှာတော့ နောက် တစ်ကြောင်းအထိပါ ဆက်သွားတာမို့လို့ Windows OS ပေါ်မှာ ဖိုင်ကို editing လုပ်ခဲ့တယ်လို့ ထင်တယ်။ ရုရှား ဆိုတဲ့ စာကြောင်းကတော့ စာလုံး တစ်လုံးတည်းရှိတာမို့ label ထိုးသူက တမင်တကာ ဖျက်ခဲ့တာလို့ ယူဆတယ်)  

```
အာရှတိုက်သား/n တွေ/part တစ်/tn ဦး/part နဲ့/ppm တစ်/tn ဦး/part ဘယ်လို/adv ဆက်စပ်/v|မှု/part ရှိ/v တယ်/ppm ဆို/v တာ/part လေ့လာ/v ရ/part မယ်/ppm ၊/punc ကျွန်တော်/pron လည်း/part အနုပညာသမား/n ပါ/part ဗျာ/part ’/punc ဟူ၍/part လည်း/part ဗိုလ်ချုပ်/n ပြောကြား/v ခဲ့/part ဖူး/part သည်/ppm ။/punc
အာရှတိုက်သား/B တွေNO တစ်NO ဦးEO နဲ့BO တစ်/O ဦး/O ဘယ်လို/O ဆက်စပ်/O မှု/O ရှိ/O တယ်/O ဆို/O တာ/N လေ့လာ/N ရ/N မယ်/E ကျွန်တော်/B လည်း/N အနုပညာသမား/N ပါ/N ဗျာ/E 
ဗိုလ်ချုပ်/B ပြောကြား/N ခဲ့/N ဖူး/N သည်/E
```

```
နန်ချောင်/n|နိုင်ငံ/n သည်/ppm တဖြည်းဖြည်း/adv အင်အားကြီး/v လာ/part ပြီး/conj တရုတ်/n တို့/part နှင့်/ppm ရင်ပေါင်တန်း/adv ဆက်ဆံ/v နိုင်/part ခဲ့/part သည်/ppm ။/punc
နန်ချောင်/B နိုင်ငံ/O သည်/O တဖြည်းဖြည်း/O အင်အားကြီး/O လာ/O ပြီး/O တရုတ်/O တို့NO နEင့်/O ရင်ပေBင်တန်း/O ဆက်ဆံ/N နိုင်/N ခဲ့/N သည်/E
```

```
ခင်ဗျား/pron သွားတု/n ကို/ppm တစ်နေကုန်/adv တပ်/v ထား/part ရ/part မယ်/ppm ။/punc
ခင်ဗျား/B သွားတု/O ကို/O တစ်နေကုန်/O တပ်/N ထား
```

```
သို့ရာတွင်/conj ငါး/n များ/part မှ/ppm ထူးခြား/adj သော/part အသံ/n တစ်/tn မျိုး/part ကို/ppm ကြား/v ရ/part တတ်/part သည်/ppm ။/punc
သို့ရာတွင်/B ငါး/O များ/O မှ/O ထူးခြO အသံ/O တစ်/O မျိုး/O ကို/O ကြား/N ရ/N တတ်/N သည်/E
```

```
ခင်ဗျား/pron က/ppm အမေ/n နဲ့/ppm ပို/adv တူ/v တာ/part လား/part ဒါမှမဟုတ်/conj အဖေ/n နဲ့/ppm ပို/adv တူ/v တာ/part လား/part ။/punc
ခင်ဗျား/B က/O အမေ/O နဲ့/O ပို/N တူ/N တာ/N လား/E ဒါမှမဟုတ်NB အဖN/O နဲN/O ပိုEN တူ/N တB/N လား/E
```

```
ဘယ်သူ/pron က/ppm ဆရာ/n ဘာ့ဂ်/part ပါ/part လဲ/part ။/punc
ဘယ်သူ/B က/O ဆရာ/N ဘာ
```

```
စင်္ကာပူ/n English/fw :/sb Singapore/fw Chinese/fw :/sb 新加坡/fw pinyin/fw :/sb Xīnjiāpō/fw in/fw Malay/fw :/sb Singapura/fw in/fw Tamil/fw :/sb சிங்கப்பூர்/fw Cingkappūr/fw တရားဝင်/adj အမည်/n အားဖြင့်/ppm စင်္ကာပူ/n|သမ္မတနိုင်ငံ/n သည်/ppm ကျွန်း/n|နိုင်ငံ/n တစ်/tn နိုင်ငံ/part ဖြစ်/v ပြီး/conj မလေး/n|ကျွန်းဆွယ်/n ၏/ppm တောင်/n|ဘက်/n အစွန်ဆုံး/adj တွင်/ppm တည်ရှိ/v သည်/ppm ။/punc
စင်္ကာပူ/B English/O Singapo/O re/O Chinese/O 新加坡/O p/O inyin/O Xīnjiāp/O ō/O in/O Malay/O Singapu/O ra/O in/O Tamil/O சிங்கப்பூர்//O O Cingkappūr/O တရားဝင်/O အမည်/O အားဖြင့်/O စင်္ကာပူ/O သမ္မတနိုင်ငံ/O သည်/O ကျွန်း/O နိုင်ငံ/O တစ်/O နိုင်ငံ/O ဖြစ်/O ပြီး/O မလေး/O ကျွန်းဆွယ်/O ၏/O တောင်/O ဘက်/O အစွန်ဆုံး/N တွင်/N တည်ရှိ/N သည်/E
```

```
မြန်မာ/n|နိုင်ငံ/n အစိုးရ/n နှင့်/conj ရုံးသုံး/adj အဖြစ်/n ဝင်းအင်းဝ/n|ဖောင့်/n WinInwa/fw မျိုးဆက်/n များ/part ခေတ်စား/v ခဲ့/part သည်/ppm ။/punc
မြန်မာ/B နိုင်ငံ/O အစိုးရ/O နှင့်/O ရုံးO အဖြစ်/O ဝင်းအင်းဝ/O ဖောင့်/O WinInwa/O မျိုးဆက်/O များ/N ခေတ်စား/N ခဲ့/N သည်/E
```

```
များမကြာမီ/adv ကွန်မြူနစ်/n|ခေါင်းဆောင်/n များ/part နှင့်/conj ပြည်သူ့/n|အရေးတော်ပုံ/n|ပါတီ/n|ခေါင်းဆောင်/n များ/part အတူ/adv စည်းဝေး/v ရန်/conj စီစဉ်/v လိုက်/part ပြီး/conj ၊/punc ထို/adj အစည်းအဝေး/n ၌/ppm ဗိုလ်ချုပ်/n|အောင်ဆန်း/n သည်/ppm “/punc ဖက်ဆစ်/n|ဓါးပြ/n များ/part ကို/ppm တိုက်ထုတ်/v ကြ/part လော့/ppm ”/punc ခေါင်းစဉ်/n ပါ/part ကြေညာစာတမ်း/n ကို/ppm ဖတ်/v ကာ/conj တော်လှန်/v|ရေး/part ကို/ppm တရားဝင်/adv အကောင်အထည်ဖော်/v လိုက်/part ပါ/part သည်/ppm ။/punc
များမကြာမီ/B ကွန်မြူနစ်/O ခေါင်းဆောင်/O များ/O နှင့်/O ပြည်သူ့/O အရေးတော်ပုံ/O ပါတီ/O ခေါင်းဆောင်/O များ/O အတူ/O စည်းဝေးNO ရနN/O စီEဉ်/O လိုက်/O ပြီး/O ထို/O အစည်းအဝေး/O ၌/O ဗိုလ်ချုပ်/O အောင်ဆန်း/O သည်/O ဖက်ဆစ်/O ဓါးပြ/O များ/ONကို/O တိုက်ထုတ်/O ကြ/O လော့/E ခေါင်းစဉ်/O ပါ/O ကြေညာစာတမ်း/O ကို/O ဖတ်/O ကာ/O တော်လှန်/O ရေး/O ကို/O တရားဝင်/O အကောင်အထည်ဖော်/N လိုက်/N ပါ/N သည်/E
```

```
နံကာ/n|လ/n အကြောင်း/n ကို/ppm ဝေါဟာရ/n လိနတ္ထဒီပနီ/n ကျမ်း/n ၌/ppm ထို/adj နံကာ/n|လ/n သဘော/n အဓိပ္ပါယ်/n ကို/ppm ကြံ/v သော်/conj အဘိဓာန်/n ကျမ်း/n တွင်/ppm သာဝဏော/n ၊/punc နံကာ/n|လ/n ၊/punc နိက္ခမနီယော/n ၊/punc နံကာ/n|လ/n ဟူ၍/part ပရိယာယ်/n နှစ်/tn ပုဒ်/part ပြ/v သည်/ppm ။/punc
B လ/O အကြောင်း/O ကို/O ဝေါဟာရ/O လိနတ္ထဒီပနီ/O ကျမ်း/O ၌/O ထို/O နံကာ/O လ/O သဘော/O အဓိပ္ပါယ်/O ကို/O ကြံ/O သော်/O အဘိဓာန်/O ကျမ်း/O တွင်/O သာဝဏော/O နံကာ/O လ/O နိက္ခမနီယော/O နံကာ/O လ/O ဟူ၍/O ပရိယာယ်/O နှစ်/N ပုဒ်/N ပြ/N သည်/E
```

```
ခင်ဗျား/pron ဘယ်/adj အချိန်/n မှာ/ppm အဆင်ပြေ/v လဲ/part ။/punc
ခင်ဗျား/B ဘယ်/O အချိန်/N မှာ/N အဆင်E
```

```
ဒီ/adj အလုပ်/n က/ppm ကျွန်တော်/pron နဲ့/ppm ကိုက်/v တယ်/ppm ထင်/v တယ်/ppm ။/punc
ဒီ/B အလ က/O ကျွန်တော်/O နဲ့/O ကိုက်/N တယ်/N ထင်/N တယ်/E
```

```
ကျွန်တော်/pron ဟာ/part ကိုရီးယား/n|စာ/n စာသင်ကြားရေး/n လောက/n မှာ/ppm ဘဝ/n ကို/ppm မြုပ်နှံ/v သွား/part မှာ/ppm ပါ/part ။/punc
ကျွန်တော်E ဟာ/O ကိုရီးယား/O စာ/O စာသင်ကြားရေး/O လောက/O မှာ/O ဘဝ/O ကို/O မြုပ်နှံ/N သွား/N မှာ/N ပါ/E
```

```
သူ/pron တို့/part ရဲ့/ppm ချစ်ခင်/v|မှု/part က/ppm အင်မတန်/adv နွေးထွေးခိုင်မြဲ/v တယ်/ppm ။/punc
သူ/B တို့/O ရဲ့/O ချစ်ခင်/O မှု/O က/N အင်မတန်/N နွေးထွေးခိုင်မြဲNN တယ်NE
```

```
အခြား/adj အဖွဲ့/n|ဝင်/v နိုင်ငံ/n များ/part ၏/ppm စိုးရိမ်မကင်း/v|ဖြစ်/v|မှု/part ကြောင့်/ppm ၂ဝဝ၆/num ခုနှစ်/n အတွက်/ppm မိမိ/pron အလှည့်/n ရောက်/v ရှိ/part မည့်/part ဥက္ကဋ္ဌ/n နေရာ/n ကို/ppm စွန့်လွှတ်/v ခဲ့/part သည်/ppm ။/punc
အခြား/B အဖွဲ့/O ဝင်/O နိုင်ငံ/O များ/O ၏/O စိုးရိမ်မကင်း/O ဖြစ်/O မှု/O ကြောင့်/O ၂ဝဝ၆/O ခုနှစ်/O အတွက်/O မိမိ/O အလှည့်/O ရောက်/O ရှိ/O မည့်/O ဥက္ကဋ္ဌ/O နေရာ/O ကို/N စွန့်လွှတ်/N ခဲ့NN သညN/E
```

```
ထို/pron သို့/part သရအက္ခရာ/n ၏/ppm အရှည်/n ကို/ppm ပြောင်းလဲ/v|ခြင်း/part ဖြင့်/ppm စကားလုံး/n ၏/ppm အဓိပ္ပါယ်/n အား/ppm ပြောင်းလဲ/v စေ/part နိုင်/part သည်/ppm :/sb ojisan/fw おじさん/fw ဦးလေး/n and/fw ojiisan/fw おじいさん/fw အဘိုး/pron ။/punc
ထို/B သို့/O သရအက္ခရာ/O ၏/O အရှည်/O ကို/O ပြောင်းလဲ/O ခြင်း/O ဖြင့်/O စကားလုံး/O ၏/O အဓိပ္ပါယ်/O အား/O ပြောင်းလဲ/O စေ/O နိုင်/O သည်/O ojisan//O O おじさん/O ဦးလေး/O and/N ojiisan/N おじいさん/N အဘိုး/E
```

## Some Errors Cannot Detect with mk-wordtag.pl

အောက်ပါ လို error မျိုးကျတော့ mk-wordtag.pl ဖိုင်နဲ့ မတွေ့နိုင်ဘူး။  
ဘာကြောင့်လဲ ဆိုတော့ word နဲ့ tag က တူနေလို့ ...   

ကိုယ်ကာယ/n|လေ့ကျင့်ရေး/n အခန်း/n ကို/ppm သွား/v သည်/ppm ။/punc
ကိုယ်ကာN/B လေEကျင့်ရေး/B အခန်း/N ကို/N သွား/N သည်/E

ကိုရီးယား/n သတင်းစာ/n က/ppm ခက်/adj လို့/part မ/part ဖတ်/v နိုင်/part ဘူး/part ။/punc
ကိုရီBယား/B သတင်းစာ/O က/O ခက်/O လို့/O မ/N ဖတ်/N နိုင်/N ဘူး/E

အကြီးဆုံး/adj ငါး/n မှာ/ppm ဝေလငါးမန်း/n whale/fw shark/fw ဖြစ်/v ပြီး/conj ၁၅/num မီတာ/n ရှည်/adj ကာ/conj ၁၅/num တန်/n လေး/adj သည်/ppm ။/punc
အကြီးဆုBး/B ငါး/O မှာ/O ဝေလငါးမန်း/O whale/O shark/O ဖြစ်/O ပြီး/O ၁၅/O မီတာ/O ရှည်/O ကာ/O ၁၅/N တန်/N လေး/N သည်/E

မီးသတ်ပိုက်/n အဆင်သင့်/adv လုပ်/v ပါ/part ။/punc
မီးသတ်ပိုက်/B အဆင်သင့်/N လုပ်/NNပါ/E

ငါ့/pron ကို/ppm လာ/v မ/part ရှုပ်/v နဲ့/part ။/punc
ငါ့/B ကို/O လာ/N မ/Eရှုပ်/N နဲ့/E

ဗိုလ်ချုပ်/n|အောင်ဆန်း/n သည်/ppm သူ/pron ၏/ppm အနေအထား/n နှင့်/ppm ပတ်သက်/v ၍/conj လည်းကောင်း/conj ၊/punc မြန်မာ/n|နိုင်ငံ/n အခြေအနေ/n နှင့်/ppm ပတ်သက်/v ၍/conj လည်းကောင်း/conj စိတ်ကူးယဉ်/v ပြီး/conj ထင်ယောင်ထင်မှား/adv မ/part ဖြစ်/v ခဲ့/part ပါ/part ။/punc
ဗိုလ်ချုပ်/B အောင်ဆန်း/O သည်/O သူ/O ၏/O အနေအထား/O နှင့်/O ပတ်သက်/O ၍/O လည်းကောင်း/O ငံ/O အခြေအနေ/O နှင့်/O ပတ်သက်/O ၍/O လည်းကောင်း/O စိတ်ကူးယဉ်/O ပြီး/O ထင်ယောင်ထင်မှား/O မ/N ဖြစ်/N ခဲ့/N ပါ/E

သားလေး/n ဟာ/ppm စာကြိုးစား/v ပြီး/conj တော့/part ဆရာဝန်/n အလုပ်/n နဲ့/conj အသက်မွေးကျောင်း/n ပြု/v နေ/part တယ်/ppm ။/punc
သားလေး/B ဟာ/ONစာကြိEးစား/O ပြBး/O တော့/O ဆရာဝန်/O အလုပ်/O နဲ့/O အသက်မွေးကျောင်း/N ပြု/N နေ/N တယ်/E

ခရစ်/n ၁၈ဝ၈/num ခုနှစ်/n လောက်/part တွင်/ppm မန်ချက်စတာ/n|မြို့/n|သား/n ကျောင်းဆရာ/n ဂျွန်ဒေါ်လတန်/n သည်/ppm သူ/pron ၏/ppm အက်တမ်/n|သီအိုရီ/n ကို/ppm စတင်/v တီထွင်/v ခဲ့/part ရာ၌/conj ဒြပ်စင်/n တို့/part တွင်/ppm အလေးချိန်/n တစ်/tn ခု/part ရှိ/v သော/part အက်တမ်/n တို့/part ပါဝင်/v ရ/part မည်/ppm ဟု/part ယူဆ/v ပြီးလျှင်/conj ၁/num ဓာတု/n|အချိုး/n မှန်/adj နိယာမ/n နှင့်/conj ၂/num ဓာတု/n|အချိုးအဆ/n တိုး/adj နိယာမ/n နှစ်/tn မျိုး/part ကို/ppm စတင်/v ကြံစည်/v ရှင်းလင်း/v ပြသ/v ခဲ့/part လေ/part သည်/ppm ။/punc
ခရစ်/B ၁၈ဝ၈/O ခုနှစ်/O လောက်/O တွင်/O မန်ချက်စတာ/O မြို့/O သား/O ကျောင်းဆရN/O ဂျNန်ဒေါ်လEန်/OBသည်/O သူ/O ၏/O အက်တမ်/O သီအိုရီ/O ကို/O စတင်/O တီထွင်/O ခဲ့/O ရာ၌/O ဒြပ်စင်/O တို့/O တွင်/O အလေးချိန်/O တစ်/O ခု/O ရှိ/O သော/O အက်တမ်/O တို့/O ပါဝင်/O ရ/O မည်/O ဟု/O ယူဆ/O ပြီးလျှင်/O ၁/O ဓာတု/O အချိုး/O မှန်/O နိယာမ/O နှင့်/O ၂/O ဓာတု/O အချိုးအဆ/O တိုး/O နိယာမ/O နှစ်/O မျိုး/O ကို/O စတင်/O ကြံစည်/O ရှင်းလင်း/O ပြသ/N ခဲ့/N လေ/N သည်/E

နယူးဇီလန်/n သည်/ppm ပထဝီ/n အနေအထား/n အရ/ppm ထူးခြား/v သည်/ppm ။/punc
နယEးဇီလန်/B သည်/O ပထဝီ/O အနေအထား/N အရ/N ထူးခြား/N သည်/E

ထို့ကြောင့်/conj “/punc ဖေဖေ/n ဟာ/part ဘယ်/pron လို/ppm လူစား/n|မျိုး/n ပါ/part လိမ့်/ppm ”/punc ဟူသော/part သိ/v ချင်/part စိတ်/n ဖြင့်/ppm ဖခင်/n ၏/ppm ဘဝ/n လုပ်ဆောင်/v|ချက်/part များ/part နှင့်/ppm ပတ်သက်/v သော/part စာပေ/n အထောက်အထား/n များ/part ကို/ppm ကျွန်မ/pron စတင်/v|စုဆောင်း/v|လေ့လာ/v|ဖတ်ရှု/v|ခြင်း/part ပင်/part ဖြစ်/v ပါ/part သည်/ppm ။/punc
ထို့ကြောင့်/B ဖေဖေ/O ဟာ/O ဘယ်/O လို/O လူNား/O မျိုး/O ပါ/O လိမ့်/E ဟူသော/O သိ/O ချင်/O စိတ်/O ဖြင့်/O ဖခင်/O ၏/O ဘဝ/O လုပ်ဆောင်/O ချက်/O များ/O နှင့်/O ပတ်သက်/O သော/O စာပေ/O အထောက်အထား/O များ/O ကို/O ကျွန်မ/O စတင်/O စုဆောင်း/O လေ့လာ/O ဖတ်ရှု/O ခြင်း/O ပင်/N ဖြစ်/N ပါ/N သည်/E

ထိုအခါ/conj လူ့/n|ယဉ်ကျေး/adj များ/part နှင့်/conj ငါ/pron လူရိုင်း/n ဟု/part ဇာတိ/n ခွဲ/v ပစ်/part ချင်/part သည့်/part စိတ်/n များ/part ရှိ/v လာ/part သည်/ppm ”/punc ဟု/part ရေးသား/v ခဲ့/part ဖူး/part ၏/ppm ။/punc
ထိုEခါ/B လူ့/O ယဉ်ကျေး/O များ/O နှင့်/O ငါ/O လူရိုင်း/O ဟု/O ဇာတိ/O ခွဲ/O ပစ်/O ချင်/O သည့်/O စိတ်/ONများ/O ရှိ/O လာ/O သည်/E ဟု/O ရေးသား/N ခဲ့/N ဖူး/N ၏/E

