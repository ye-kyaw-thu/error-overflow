# Word-to-Word Translation Experiment Note

## Data Preparation

Preprocessing အသေးစိတ်တွေကိုတော့ ဒီနေရာမှာ မဖော်ပြတော့ဘူး။ train နဲ့ test data နဲ့ ပတ်သက်တဲ့ information ကိုပဲ အဓိကထား ပြောသွားမယ်။  

- Path က "/media/ye/project2/exp/word2word-tran/word2word/my-x/" ဆိုတဲ့ အောက်မှာ ဒေတာတွေကို ပြင်ဆင်သွားမယ်။  
- train နဲ့ စတဲ့ ဖိုင်တွေက word2word နဲ့ phrase level lexicon building အတွက် သုံးရန်  
- test နဲ့ စတဲ့ ဖိုင်တွေက evaluation အတွက် သုံးရန်  

### Myanmar-Beik

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$ wc *.bk
  10722   70447 1047992 all.bk
    100     633    9763 test.bk
  10622   69814 1038229 train.bk
  21444  140894 2095984 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$ wc *.my
  10722   69951 1126789 all.my
    100     649   10326 test.my
  10622   69302 1116463 train.my
  21444  139902 2253578 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$
```

check data ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$ head test.my 
မင်း မေ့ တဲ့ အဖြေ ။
မင်း ငါး ကြော် တာလား ။
ဒီမှာ ဘယ် လူမျိုးစု တွေ ကို ကျွန်တော်ရို့ တွေ့ နိုင်မလဲ ။
သူမ က ကျွန်တော့် ကို သိ ခဲ့တယ် ။
ကိုယ်က သူတို့ကို ပိုက်ဆံ ထပ် မယူပဲ စစ်ဆေးချက်တွေ ပြန်လုပ်ပေးဖို့ အတင်းအကြပ် ပြော လိုက်တယ် ။
မင်း အခု ဘာ လုပ်နေ လဲ ။
သူတို့က ခင်ဗျား ကို မ သိ ခဲ့ဘူး ။
ကျွန်တော်ရို့အပြေးအလွှားလုပ် ဖို့ မ လို ပါဘူး ။
စားပွဲထိုးအမျိုးသမီး ခဏဆို ရောက်လာ ပါလိမ့်မယ် ။
မင်းရဲ့ အောင်မြင်မှုအတွက် မင်းကို ငါ ချီးကျူး ပါတယ် ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$ head test.bk
နင် မေ့ တဲ့ ဖြေ  ။
မင်း ငါး ကြော် ရယ်လား ။
ဒါကို ဘာ လူမျိုးစု ဒေ ကို ကျွန်တော်ဝို့ တွေ့ နိုင်လဲ ။
အဲ့အမ ကျွန်တော့် ကို သိ ရယ် ။
ငါ က သူကို ကြီးပြား မယူဝ စစ်ဆေးချက် ပြန်လုပ်ဝို တအား ပြော ရရယ်  ။
နင် အခု ဘာ လုပ် နေရယ်  ။
သူတို့လေ ခင်များ ကို မ သိ ရ ။
ကျနော်ဝို့ အပြေးအလွှား လုပ် ဝို့ မ လို ပီလန်း  ။
စားပွဲထိုး ကောင်မငယ် နည်းနည်းငယ်ကြာ လာ မယ်တဲ့  ။
မင်းရဲ့ အောင်မြင်မှု တွက် မင်းကို ငါ ချီးကျူး ရယ်  ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$
```

### Myanmar-Chin (Mizo)

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ wc train.{my,ch}
  14883  101610 1686356 train.my
  14883  135869  584182 train.ch
  29766  237479 2270538 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ wc test.{my,ch}
  100   643 10432 test.my
  100   871  3745 test.ch
  200  1514 14177 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$
```

check the data ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ head test.my
မင်း ငါ့ ကို မ ဆက်သွယ် ဘူး ။
ကိုင်ထား ။
အဲဒီကို ကျွန်တော် ဘယ်အချိန် ရောက်ရောက် ။
ခင်ဗျား ဘယ်ကို သွားမယ် ဆိုတာ ဆုံးဖြတ် ပြီးပြီလား ။
သူတို့ကို တောင်းပန် ဖို့ ကျွန်တော် ကြိုးစား မယ် ။
မင်း အဲ့ဒီမှာ အပြင်ထွက် ရမှာ မ ဟုတ်ပါဘူး ။
သိပ်ကောင်း ၊ မင်း မိသားစု ကော နေကောင်း ရဲ့လား ။
အဲဒီ လမ်းဆုံ မှာ ရပ်ဆိုတဲ့ ဆိုင်းဘုတ် လေးဘက်လေးလံမှာ ရှိ တယ် ။
မင်း ဘယ် အတန်းမှာ သင်နေ သလဲ ။
ဒါ ဘယ်သူ့ ဘလောက်အင်္ကျီ လဲ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ head test.ch
Nang hi min rawn be pawp lo va .
Vuan rawh .
Chulai hmun chu engtik hunah pawh thleng ila .
Khawiah nge i kalna tur chu i tifel tawh em ?
Anniho chu ngaihdam dil ka tum ang .
Hetah chuan pawn i chhuak thei dawn lo ania .
Tha lutuk . I chhungte teh an dam maw ?
Hemi kawngpuiah hian ‘ding rawh’ tih signboard kil tinah a awm .
Eng class-ah nge i zir ?
Hei hi tu block kawr nge ni a ?
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$
```

move to w2w folder...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ mv train.* ./w2w/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch$ mv test.* ./w2w/
```

### Myanmar-Kachin (ဂျိန်းဖော)

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ tail -n 100 ./all.kc > test.kc
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ tail -n 100 ./all.my > test.my
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ head -n 38073 ./all.kc > train.kc
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ head -n 38073 ./all.my > train.my
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ wc train.{my,kc}
  38073  309260 3721209 train.my
  38073  351019 1358068 train.kc
  76146  660279 5079277 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ wc test.{my,kc}
  100   819  9780 test.my
  100   972  3685 test.kc
  200  1791 13465 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$
```

check the data ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ head test.my
ရတနာပုံ မြို့သစ် က teleport ကို သွား ကြည့် ချင် တယ် ။
နှစ် ယောက် ခန်း ။
သူ က ယောက်ျားလေး တစ် ယောက် လေ ။
သည် ဟာ က ကျုပ် ၏ ခြေထောက် လေ ။
စုစုပေါင်း အခန်း ဘယ်နှ ခန်း ရှိ လဲ ။
သူ့ ရဲ့ အမည် က ဦးချစ် လေ ။
အဲ့ဒါဆို ကျွန်တော့ ကို ဆူးလေ ရောက် ရင် ပြော ပါ ။
သူ တစ် ယောက် တည်း သွား တယ် ။
ကိုလီ ရဲ့ စေ့စပ်ပွဲ နှင့် မင်္ဂလာဆောင်ပွဲ အတွက် ပြင်ဆင် နေ တာ ပါ ။
ဒါ ငါ့ လျှာ လေ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$ head test.kc
ya da na pon myo nnan na teleport de sa mayu ai .
lahkawng nga ai gawk .
shi gaw la sha langai re le .
n dai gaw ngai na lagaw le .
gawk yawng kade nga ai rai ?
shi na mying gaw u chit re le .
dai nga yang ngai hpe sue lay du yang tsun rit .
shi langai hkrai sa ai .
ko li na num hpyi ai hte hkrung ran na matu hkyen taw ai .
n dai ngai nga shing let le .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w$
```

### Myanmar-Kayah

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$ wc train.{my,ky}
  10131   81414 1279333 train.my
  10131   82828 1366507 train.ky
  20262  164242 2645840 total
  ```
  
  ```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$ wc test.{my,ky}
  100   872 13489 test.my
  100   859 14597 test.ky
  200  1731 28086 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$
```

check the data...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$ head test.my
ဒီ ရောဂါ ဟာ ကလေး တွေ မှာ ဖြစ် လေ့ ရှိ တယ် ။
ဆေးတောင့်။
သူငွေတိုးပေးစားတယ်။
မင်္ဂလာ ပါ ။ ပြည်သူ့ ရင်ပြင် မှာ လိုင်းကား နံပါတ် ၃၀၂ ကို စီး ပါ ။ ရန်ကုန် တက္ကသိုလ်ကျောင်း ရှေ့ မှတ်တိုင် ရောက် တော့ ဆင်း ပါ ။ ပြီးရင် ရှေ့ ကို မီတာ ၅၀ လောက် ဆက်လျှောက်ရင် ရောက်ပြီ ။
စကားပုံ နဲ့ ဆိုရိုး စကား ကွာခြားမှု က ဘာ လဲ ဆရာကြီး ။
ကျေးဇူးတင် ပါ တယ် ဗျာ ။
အော် ၊ ကောင်း ပါ တယ် ။ ည မှာ ပို ကောင်း ပါ တယ် ။ ကျွန်တော် လာ ခဲ့ မယ် ။
နာမည် သိ ပါရစေ ခင်ဗျာ ။
အသွားအပြန် လက်မှတ် ။
ပြင်ပ လူနာ ဌာန ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$ head test.ky
ꤒꤟꤢꤧ꤬ꤏꤢꤧ꤭ ꤛꤢꤩ꤭ꤒꤢ꤬ꤟꤢꤩ꤬ ꤗꤢ꤬ ꤢ꤬ꤓꤝꤟꤥ꤭ꤓꤛꤢ꤬ ꤡꤟꤛꤢ ꤊꤜꤢꤪ꤭ ꤘꤣ ꤕꤢ꤬ꤡꤟꤢꤧ ꤯
ꤒꤟꤢꤧ꤬ꤋꤢꤨ꤬ꤕꤜꤢꤪꤢꤧ ꤯
ꤢ꤬ ꤕꤜꤥ꤭ꤙꤢꤪ꤬ꤢꤩ꤬ ꤚꤢꤦ꤭ꤖꤢꤨ ꤯
ꤒꤟꤢꤧ꤬ꤚꤛꤢꤙꤢꤧ꤬ ꤔꤟꤢꤧ꤬ ꤯ ꤘꤣ ꤕꤛꤢꤩ꤬ꤒꤢꤨꤛꤢꤩ꤬ꤕꤛꤢꤩ꤬ ꤔꤌꤣ꤬ ꤘꤛꤢ ꤙꤢꤎꤢ꤬ꤊꤢ꤭ (꤃꤀꤂) ꤔꤌꤣ꤬ ꤯ ꤢꤦ꤬ꤒꤟꤌꤣ ꤟꤢꤪ ꤘꤣ ꤛꤢ꤭ꤊꤢꤨ꤭ꤊꤟꤢꤩ ꤞꤛꤥꤜꤤ꤬ꤟꤥ꤭ ꤒꤟꤥꤓꤛꤢ꤬ꤜꤣ꤭ ꤑꤢꤩ꤭ ꤚꤢꤪ ꤏꤤꤒꤟꤢ꤭ ꤙꤤꤔꤌꤣ꤬ ꤯ ꤓꤌꤣ꤭ ꤚꤢꤪ ꤘꤣꤑꤢꤩ꤭ ꤡꤛꤣ ꤕꤟꤥ ꤗꤤ꤬ꤒꤢ꤬ (꤅꤀) ꤟꤢꤩ ꤗꤢ꤬ ꤢ꤬ꤒꤟꤌꤣ ꤟꤢꤪ ꤯
ꤍꤟꤥꤗꤟꤌꤣꤕꤚꤟꤢꤧ ꤔꤢ ꤒꤟꤢꤧ꤬ꤜꤢꤩꤊꤜꤥ꤭ ꤟꤢꤩꤙꤢꤧ꤬ ꤗꤢ꤬ ꤢ꤬ꤋꤥ ꤜꤢꤨ꤭ ꤖꤢꤨꤒꤢꤩ꤭ ꤞꤢꤚꤢꤘꤢꤨ꤬ ꤯
ꤒꤟꤢꤧ꤬ꤙꤝꤤꤒꤟꤢꤧ꤬ꤒꤢ꤬ꤚꤛꤢꤩ꤭ ꤯
ꤢꤪ꤬ . ꤢ꤬ꤔꤟꤤ ꤕꤚꤢꤧ ꤯ ꤗꤟꤢꤪꤋꤤ ꤗꤢ꤬ ꤢ꤬ꤚꤛꤢ ꤊꤜꤢꤪꤊꤜꤢꤪ꤭ ꤯ ꤠꤢ꤭ ꤟꤛꤢ꤭ ꤕꤢ꤭ ꤯
ꤘꤛꤢꤩꤞꤢꤧꤑꤢꤩ꤭ ꤗꤛꤢ ꤗꤝꤟꤤ꤬ ꤯
ꤜꤟꤢꤩꤡꤛꤣꤜꤟꤢꤩꤊꤟꤢ꤬ ꤜꤤ꤬ꤙꤢ꤬ ꤯
ꤜꤟꤢꤩꤟꤛꤢ꤭ꤘꤛꤢꤩꤜꤟꤌꤣ꤭ ꤕꤚꤟꤢꤧ꤬ꤏꤝꤤ ꤘꤣꤢ꤬ꤊꤜꤢꤪ꤭ ꤗꤢꤙꤥ꤭ ꤯
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w$
```

### Myanmar-Mon

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ tail -n 100 ./all.mo > test.mo
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ head -n 8873 ./all.mo > train.mo
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ head -n 8873 ./all.my > train.my
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ wc train.{my,mo}
   8873   61870 1012895 train.my
   8873   50344  804865 train.mo
  17746  112214 1817760 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ wc test.{my,mo}
  100   498  6964 test.my
  100   488  6495 test.mo
  200   986 13459 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$
```

check the splitted files...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ head test.my
မွေးနေ့ပွဲ ကျင်းပ သလား ။
ငါ့ ကို မုန်း လား ။
အဲ့ဒါ ကို မကြိုက် ဘူးလား ။
ငါ့ ကို သတင်းပေး တာလား ။
သွား ဖို့ ရည်ရွယ် သလား ။
လာ ဖို့ ရည်ရွယ် သလား ။
မင်း ငါ့ကို မ လွမ်း ဘူးလား ။
မင်း သူမကို မ လွမ်း ဘူးလား ။
မင်း မ ငို ဘူးလား ။
သူ့ကို မ ခေါ် ဘူးလား ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$ head test.mo
ကၠောန်ဗဒှ် သဘၚ်တ္ၚဲက္တဵုဒှ်မၞိဟ် ဟာ ။
က္ဍုဟ် အဲ ဟာ ။
ဣဇှ် ဂှ် ဟွံဒးစိုတ် ပုဟ်ဟာ ။
ကဵု အဲ ပရိုၚ် ဟာ ။
ရန်တၟံလဝ် သွက်ဂွံ အာ ဟာ ။
ရန်တၟံလဝ် သွက်ဂွံ ကၠုၚ် ဟာ ။
ဗှေ် ဟွံ ဗှ်သနာ အဲ ပုဟ်ဟာ ။
ဗှေ် ဟွံ ဗှ်သနာ ဍေံ ပုဟ်ဟာ ။
ဗှေ် ဟွံ လရိုအ် ပုဟ်ဟာ ။
ဟွံ ကော် ဍေံ ပုဟ်ဟာ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w$
```

### Myanmar-Po_Kayin

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/18Jan2021/SMT_data_PWK$ cat train.mya dev.mya test.mya > ../../w2w/all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/18Jan2021/SMT_data_PWK$ cat train.pwk dev.pwk test.pwk > ../../w2w/all.pk
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ wc *
  19139  110777 2090004 all.my
  19139  112316 1850324 all.pk
  38278  223093 3940328 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ tail -n 100 ./all.pk > test.pk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ head -n 19039 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ head -n 19039 ./all.pk > train.pk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ wc train.{my,pk}
  19039  110197 2079122 train.my
  19039  111754 1840525 train.pk
  38078  221951 3919647 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ wc test.{my,pk}
  100   580 10882 test.my
  100   562  9799 test.pk
  200  1142 20681 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$
```

check the splitted files...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ head test.my
ဒီ အပိုဒ်ကို ရွတ် မှာ မဟုတ်ဘူးလား
လောလောဆယ်တော့ ဘတ်စ်ကားပဲ စီး ရတော့မှာပေါ့
ဘယ်သူတွေ တောင်းပန် ကြတာလဲ
ကျွန်တော် ခင်ဗျားကို နောက် တစ်ခွက် ယူပေး ရမလား
ယူရက်ကား ဒါ ငါတို့ လုပ် တာ
ငါ့ကို မ လှည့်စား ပါနဲ့
သူမ ကျွန်တော့် ကို မျက်စိမှိတ်ပြ သွားတယ်
ခင်ဗျား အဲဒီမှာ အလုပ်လုပ် ခဲ့တာလား
ဘာ အကြောင်းကြောင့်ပဲဖြစ်ဖြစ် မင်းရဲ့ စိတ်တွေကို မင်း ပြောင်းလဲမယ် ဆိုရင် ငါကို သိခွင့် တော့ပြုပါ
မင်းက ဘယ်လောက် တည်ငြိမ် လဲ
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$ head test.pk
ယအီၪနီၪ စ့ၩ အီၪ အၪလ့ၬ လီၫ
က ဖီၡီၫ အဆၧၫ့ယီၩ မွဲအ့ၬ ဧၪ
ထီယီၩအဘိၩ့ဘၭနီၪ ကဘၪထူၭဒၪ ဘၧၭစကၩလီၫ လၥၨၩ
မွဲၦလဖၪ အၪ့ကံၩ့အၪ့ယၫဆၧ လဲၪ
ယ ကဘၪ မၩန့အ့ၪ နၧၩ နးခွၭဒီၭ ဧၪ
ယူၫရဲၭခၩ အယီၩ မွဲ ပ မၩ
န ဘျံၭ ယၧၩ လဂ့ၩ
ၦမုၪနီၪ ထဲၩ့ဘံၪ့ထ့ ယၧၩ အမ့ၬၥၪ လီၫ
န ဂဲၫထဲၩ့ မၩဆၧမၩ ထနီၪ ဧၪ
မွဲဘဲၫ ဆၧအဂဲးမွဲမွဲ အ့ၪ န ကအၪ့လဲၩထၪ့ နၥၭတၭ ဒုၭၥ့ၪယၫဘၪလါ ယၧၩ ဆံၭ
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w$
```

## Myanmar-PaO

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ wc all.{my,po}
  18354  106500 1880099 all.my
  18354   83252 2057101 all.po
  36708  189752 3937200 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ tail -n 100 ./all.po > test.po
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ head -n 18254 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ head -n 18254 ./all.po > train.po
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ wc train.{my,po}
  18254  105939 1869709 train.my
  18254   82861 2045735 train.po
  36508  188800 3915444 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ wc test.{my,po}
  100   561 10390 test.my
  100   391 11366 test.po
  200   952 21756 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ head test.my
ဘာလို့လဲဆိုတော့ သူတို့ စကားပြောတာ အရမ်း မြန်တယ် လို့ ငါ ထင် တယ်
ဒါ ဒီ အပတ်မှာ တတိယ အကြိမ် ပဲ
အတန်း မစခင် ၁၀ မိနစ် မှာ အတန်း ကို ရောက် ရမယ်
တစ်ခုခုလေးတောင် မရှိ ဘူးလား
ငါ နဲ့ ငါ မိသားစု အပေါ် မင်းရဲ့ ဧည့်ဝတ်ကျေပွန်မှု အတွက် ကျေးဇူးတင်ပါတယ်
ငါ အတွက် စာမေးပွဲ အောင် ဖို့ရာ လွယ်လွယ်လေးပါ
သူ နေလို့ မ ကောင်းဘူး ထင်တယ်
သူ သူ့ စားပွဲ မှာ မ ရှိဘူး
မင်း စကား ပြော နေတာ
အဲဒါ တွေ ကို အလွတ် ကျက်မှတ် ပါ
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$ head test.po
ကွပ်တမုဲင်ꩻဟောင်း ကရိုနဝ်ꩻ ဝွေꩻသီး ဒေါ့ꩻငဝ်းနဝ်ꩻ မွိုင်မွေးလွဉ်ꩻငါႏ ခွေ ထင်းနုဲင်းနဝ်ꩻ
ပါꩻတွမ်ႏ ယိုတပတ်နဝ်ꩻ သွံလဲင်ႏလဲဉ်း
ခါးလားကစအတန်ꩻ ၁၀ မိနစ်ရပ်နဝ်ꩻ တွိုးဗာႏ အတန်ꩻကို
တစွိုးစွိုးငါꩻတဲ့ မဲဉ်ႏတဝ်းရင်ꩻဟောင်း
ခွေတွမ်ႏ ခွေဖူႏဝေးအလောင်းယို ထဉ်ႏဝတ်တရာꩻ ကေႏငါႏတွော့ꩻ ကေꩻဇူႏတင်ႏငါႏ နာꩻ
ခွေအတာႏ အီးအောင်ႏဗာႏ လိတ်ရီပွယ်ꩻနဝ်ꩻ ယိုယိုပေႏလွုမ်
ဝွေꩻ အုံဟဝ်တဝ်း အလွိုးဗာႏ
ဝွေꩻ တအဝ်ႏတဝ်း ဝွေꩻ အံꩻဒဲဉ်ခွုံႏထျꩻ
နာꩻ အဝ်ႏဒေါ့ꩻငဝ်းကျာꩻ
နဝ်ꩻနဝ်ꩻ ကျက်အွံနေးဟုဲင်း
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w$
```

### Myanmar-Rakhine

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/data$ cat {train,dev,test}.my | wc
  18373  125320 2084293
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/data$ cat {train,dev,test}.my > ../w2w/all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/data$ cat {train,dev,test}.rk > ../w2w/all.rk
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ tail -n 100 ./all.rk > test.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ head -n 18273 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ head -n 18273 ./all.rk > train.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ head test.my
ဘာလို့လဲဆိုတော့ သူတို့ စကားပြောတာ အရမ်း မြန်တယ် လို့ ငါ ထင် တယ် ။
ဒါ ဒီ အပတ်မှာ တတိယ အကြိမ် ပဲ ။
အတန်း မစခင် ၁၀ မိနစ် မှာ အတန်း ကို ရောက် ရမယ် ။
တစ်ခုခုလေးတောင် မရှိ ဘူးလား ။
ကျွန်တော် နဲ့ ကျွန်တော့် မိသားစု အပေါ် ခင်ဗျားရဲ့ ဧည့်ဝတ်ကျေပွန်မှု အတွက် ကျေးဇူးတင်ပါတယ် ။
ကျွန်တော့် အတွက် စာမေးပွဲ အောင် ဖို့ရာ လွယ်လွယ်လေးပါ ။
သူ နေလို့ မ ကောင်းဘူး ထင်တယ် ။
သူ သူ့ စားပွဲ မှာ မ ရှိပါဘူး ။
မင်း စကား ပြော နေတာ ။
အဲ့ဒါ တွေ ကို အလွတ် ကျက်မှတ် ပါ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$ head test.rk
ဇာလို့လဲဆိုကေ သူရို့ စကားပြောစွာ ကကောင်း မြန်ရေ လို့ ငါ ထင် ရေ ။
 ဒေချင့် ကဒေ အပတ်မာ တတိယ အကြိမ် ပါ  ။
အတန်း မစခင် ၁၀ မိနစ် မာ အတန်း ကို ရောက် ရဖို့။
တစ်ခုခုချေတောင် မဟိ ပါလား ။
ကျွန်တော် နဲ့ ကျွန်တော့် မိသားစု အပေါ် မင်းရဲ့ ဧည့်ဝတ်ကျေပွန်မှု အတွက် ကျေးဇူးတင်ပါရေ ။
ကျွန်တော့် အတွက် စာမိန်းပွဲ အောင် ဖို့ရာ အလွယ်ခေျပါ ။
သူ နီလို့ မ ကောင်း ထင်ရေ။
သူ သူ့ စားပွဲ မာ  မ ဟိပါ ။
မင်း စကား ပြောနီ စွာ ။
ယင်းချင့် တိ ကို အလွတ် ကျက်မှတ် ပါ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w$
```

### Myanmar-Rawang

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/data$ cat {train,dev,test}.my > ../w2w/all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/data$ cat {train,dev,test}.rw > ../w2w/all.rw
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/data$ cd ../w2w/
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ wc all.my
  5376  43447 527494 all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ tail -n 100 ./all.rw > test.rw
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ head -n 5276 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ head -n 5276 ./all.rw > train.rw
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ wc train.{my,rw}
  5276  42693 518586 train.my
  5276  42780 215411 train.rw
 10552  85473 733997 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ wc test.{my,rw}
  100   754  8908 test.my
  100   744  3789 test.rw
  200  1498 12697 total
 ```
  
 ```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ head ./test.my 
ဒါ အတွင်းရေးမှူး ရွှဲ ဖြစ် တယ် ။
ဒါ ငါး တစ် ကောင် ပါ ။
ရန်ကုန် ရဲ့ ရာသီဥတု နဲ့ ကျင့်သားရ ပြီ လား ။
သူတို့ သည် လွယ်အိတ် ၏ အထဲမှာ ဖြစ် သည် ။
ခင်ဗျား က မိန်းခလေး တစ် ယောက် လား ။
မနေ့တစ်နေ့ က ။
တစ်ဆယ့် ခြောက်
ဂျပန် ။
တော်တော် အေး တယ် ၊ ဒါပေမယ့် နှင်း အမြဲတမ်း တော့ လဲ မ ကျ ပါ ဘူး ။
ခင်ဗျား ကျွန်တော့် ကို အကြံပေး နိုင် မလား ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$ head ./test.rw
YÀGǾNØ̀ BVNLĪÀNGKÀNG YWĒ ÍÈ .
YÀ MÉ NGĀ TÌQ GŌ ÍÈ .
YÀNGŌN YÀ LVNGCHA O VL NVM BǾĪ MÁ ? 
ÀNGMÀQ NØ̀ YǾNG YÀ VDŪNGRV́M ÍÈ .
NÀ NØ̀ SVMÀRĒ TÌQ GØ̀ MÁ ? 
SANÍ VZXNGNÍ .
TÌQCÉ VCHÙQ
JABVN .
GAY ZØ-NGĒ , ÍWĒ TVWVN ÀNGWÀ NØ̀ MVJA RÀ Ē .
NÀ Í NGÀ KÀQ PÀQZÍ ZÍSHVLĀ DÀQ MÁ ? 
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w$
```

### Myanmar-Shan

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/data$ ls
dev.my  dev.sh  test.my  test.sh  train.my  train.sh
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/data$ cat train.my dev.my test.my > ../w2w/all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/data$ cat train.sh dev.sh test.sh > ../w2w/all.sh
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/data$ cd ../w2w/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ wc all.{my,sh}
  16533  113085 1872484 all.my
  16533   92275 1916631 all.sh
  33066  205360 3789115 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ 
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ tail -n 100 ./all.sh > test.sh
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ head -n 16433 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ head -n 16433 ./all.sh > train.sh
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ head ./test.my
ကျေးဇူးပဲ ၊ ဒီမှာ ပိုက်ဆံ ။
တို့ ချိန်းထားတာကို ဖျက်ရ လိမ့်မယ် ။
ငါ ပင်လယ် ထဲ ရေကူး နေတာ ။
ခြောက်နာရီ မှာ အိပ်ယာထဖို့ ခင်ဗျား ကျွန်တော့်ကို အကြောင်းကြားပေး နိုင်မလား ။
သတင်း က မှန်ရင် မှန်မယ် ။
ဟိုက ခွေးကလေးက မ လှ ဘူးလား ။
သူ အဲဒါ့ ကို မ ပေး ဘူး ။
ဘာကြောင့် အဲဒီမှာ ဆူညံသလဲ ဆိုတာ မင်း သိ လား ။
မင်းကိုယ်မင်း သနား ရင် အဲ့ဒီလို မ လုပ် ပါနဲ့ ။
တို့တွေ နောက်ဆုံး တွေ့ ခဲ့ကြတာ တောင် အတော် ကြာ ပြီ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$ head ./test.sh
ယိၼ်းၸူမ်းဢေႃႈ ၊ ၼႆႉၼေ ငိုၼ်း ။
ဢၼ် ႁဝ်း ၶိၼ်းဝႆႉၼၼ်ႉ တေလႆႈ ယႃႇ ဢိူဝ်ႈ ။
ၵဝ် လုၺ်းၼမ်ႉ ၼႂ်း ပၢင်ႇလႆၢႇ ယူႇ ။
တႃႇတေလုၵ်ႉ ႁူၵ်းမူင်း ၸွင်ႇ သူ တေ ပူၵ်းပၼ် ၶႃႈႁဝ်း လႆႈယူႇႁႃႉ ။
ၶၢဝ်ႇ ၼၼ်ႉ မႅၼ်ႈၵေႃႇ တေမႅၼ်ႈယူႇ ။
မႃ တူဝ်ၼၼ်ႉ ဢမ်ႇ ႁၢင်ႈလီ ႁႃႉ ။
ၶဝ် ဢမ်ႇ ပၼ် ဢၼ်ၼၼ်ႉ ။
ၵွပ်ႈသင်လႄႈ တီႈၼႆႈ ဢူၼ်ဢၼ် ယူႇၼႆ မႂ်း ႁူႉ ႁႃႉ ။
ပေႃးဝႃႈ မႂ်း ဢီးလူ တူဝ်မႂ်း ၼႆၼႆႉ ယႃႇပေ ႁဵတ်း ၸိူင်ႉၼႆ ။
မိူဝ်ႈ ႁဝ်း ႁၼ်ၵၼ် ပႆၢးလိုၼ်းသုတ်း ၼၼ်ႉ ပေႃးႁိုင် ၼႃႇယဝ်ႉ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w$
```

### Myanmar-Sgaw Kayin

```
base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/18Jan2021/data_for_sgaw/run_SMT_data$ cat {train,dev,test}.mya > ../../../../my-sk/all.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/18Jan2021/data_for_sgaw/run_SMT_data$ cat {train,dev,test}.sgk > ../../../../my-sk/all.sk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/18Jan2021/data_for_sgaw/run_SMT_data$
```

ကော်ပီကူးခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ cp ../data/all.* .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ ls
all.my  all.sk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ tail -n 100 ./all.my > test.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ tail -n 100 ./all.sk > test.sk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ head -n 68471 ./all.my > train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ head -n 68471 ./all.sk > train.sk
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ wc train.{my,sk}
   68471   405858  6527553 train.my
   68471   260255  6724665 train.sk
  136942   666113 13252218 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ wc test.{my,sk}
  100   588 10584 test.my
  100   575  9857 test.sk
  200  1163 20441 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ head ./test.my
ဒီ ဆေးရုံ မှာ ဆရာဝန် သုံးဦး အလုပ် လုပ် တယ်
အဲဒါကို ရေးရေး မ ရေးရေး
စာအုပ်ကလေး လှမ်းပေး ပါလား
သင်တန်း သွား တက်ပါ
အနမ်းခံ လိုက်ရလို့ သူမ ရှက် သွားတယ်
ဘယ်တော့ ဆင်း သလဲ
သူ ဘယ် လမ်း မှာ နေ သလဲ
ခဏလေး စောင့်ပါ
သူ အဲ့ဒါ ကို မ ချိန် ခဲ့ဘူးလား
အဲ့ဒါ ဘယ်လောက် ကျ သလဲ
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ head ./test.sk
တၢ်ဆါဟံၣ် ဝဲအံၤ န့ၣ် ကသံၣ်သရၣ် သၢဂၤ မၤ တၢ်မၤလီၤ
တၢ်ဝဲန့ၣ် ကွဲးဂ့ၤ တ ကွဲးဂ့ၤ
ယူာ်ဃီၤန့ၢ် လံာ်ဖိ မီၤ
လဲၤ ထီၣ် တၢ်မၤလိတက့ၢ်
ဘၣ်တၢ်နၢမူ အဃိ အဝဲ မဲာ်ဆှး ဘၣ်သးလီၤ
စံၢ်လီၤ ဆံး လဲၣ်
အဝဲ အိၣ် လၢ ကျဲ ဖဲ လဲၣ်
ခိး တဘျးဖိတက့ၢ်
အဝဲ တ ကျဲၤလိၤ တ့ၢ် တၢ်ဝဲ န့ၣ်ဧဲၢ်
တၢ်ဝဲန့ၣ် လီၤတဲာ် ထဲ လဲၣ်
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$
```

### Rakhine-Beik

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/1$ ls
dev.bk  dev.rk  test.bk  test.rk  test-sgm  train.bk  train.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/1$ cat {train,dev,test}.bk > ../w2w/all.bk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/1$ cat {train,dev,test}.rk > ../w2w/all.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/1$ cd ../w2w/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ ls
all.bk  all.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ wc all*
  10722   70447 1047992 all.bk
  10722   68985 1124038 all.rk
  21444  139432 2172030 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ tail -n 100 ./all.bk > test.bk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ tail -n 100 ./all.rk > test.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ head -n 10622 ./all.bk > train.bk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ head -n 10622 ./all.rk > train.rk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ wc train.{bk,rk}
  10622   69814 1038229 train.bk
  10622   68350 1113721 train.rk
  21244  138164 2151950 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ wc test.{bk,rk}
  100   633  9763 test.bk
  100   635 10317 test.rk
  200  1268 20080 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$
```

check the file ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ head test.bk
နင် မေ့ တဲ့ ဖြေ  ။
မင်း ငါး ကြော် ရယ်လား ။
ဒါကို ဘာ လူမျိုးစု ဒေ ကို ကျွန်တော်ဝို့ တွေ့ နိုင်လဲ ။
အဲ့အမ ကျွန်တော့် ကို သိ ရယ် ။
ငါ က သူကို ကြီးပြား မယူဝ စစ်ဆေးချက် ပြန်လုပ်ဝို တအား ပြော ရရယ်  ။
နင် အခု ဘာ လုပ် နေရယ်  ။
သူတို့လေ ခင်များ ကို မ သိ ရ ။
ကျနော်ဝို့ အပြေးအလွှား လုပ် ဝို့ မ လို ပီလန်း  ။
စားပွဲထိုး ကောင်မငယ် နည်းနည်းငယ်ကြာ လာ မယ်တဲ့  ။
မင်းရဲ့ အောင်မြင်မှု တွက် မင်းကို ငါ ချီးကျူး ရယ်  ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$ head test.rk
မင်း မိန့် ရေ အဖြေ ။
မင်း ငါး ကြော် စွာလား ။
ဒေမာ ဇာ လူမျိုးစု တိ ကို ကျွန်တော်ရို့ တွိ နိုင်ဖို့လေး။
ထိုမချေ က ကျွန်တော့် ကို သိ ခရေ။
ကိုယ်က သူရို့  ကို ဖေသာ ထပ် မယူပဲ စစ်ဆေးချက်တိ  ပြန်လုပ်ပီးဖို့ အတင်းအကြပ် ပြော လိုက်ရေ ။
မင်း အဂု ဇာ လုပ်နီလေး ။
သူရို့ က  မင်း ကို မ သိ ခပါ ။
ကျွန်တော်ရို့ အပြီး အလွှားလုပ် ဖို့ မ လို ပါ ။
စားပွဲထိုးမိန်းမ  တနားကေ ရောက်လာ ပါဖို့။
မင်းရဲ့ အောင်မြင်မှုအတွက် မင်းကို ငါ ချီးကျူး ပါရေ ။
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w$
```

### Kachin-Rawang

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ ls
all.kc  all.rw
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ wc *
 10000  78912 331617 all.kc
 10000  79857 392588 all.rw
 20000 158769 724205 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ tail -n 100 ./all.kc > test.kc
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ tail -n 100 ./all.rw > test.rw
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ head -n 9900 ./all.kc > train.kc
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ head -n 9900 ./all.rw > train.rw
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ wc train.{kc,rw}
  9900  78183 328954 train.kc
  9900  79129 389353 train.rw
 19800 157312 718307 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ wc test.{kc,rw}
 100  729 2663 test.kc
 100  728 3235 test.rw
 200 1457 5898 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ head test.kc
Ndai gaw ngai na wa re .
Ndai gaw ngai na wa re ai .
Ndai gaw ngai na wa re nga ai .
Ndai gaw ngai na wa le .
Ndai gaw ngai na nten re .
Ndai gaw ngai na nten re ai .
Ndai gaw ngai na nten re nga ai .
Ndai gaw ngai na nten le .
Ndai gaw ngai na nten re .
Ndai gaw ngai na nten re ai .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$ head test.rw
YÀ MÉ NØ̀ NGÀ YÀ SHÀ ÍÈ .
YÀ MÉ NØ̀ NGÀ YÀ SHÀ ÍÈ .
YÀ MÉ NØ̀ NGÀ YÀ SHÀ ÍÈ .
YÀ MÉ NØ̀ NGÀ YÀ SHÀ LŌ .
YÀ MÉ NØ̀ NGÀ NĪTǾL ÍÈ .
YÀ MÉ NØ̀ NGÀ NĪTǾL ÍÈ .
YÀ MÉ NØ̀ NGÀ NĪTǾL ÍÈ .
YÀ MÉ NØ̀ NGÀ NĪTǾL LŌ .
YÀ MÉ NØ̀ NGÀ YÀ NĪTǾL ÍÈ .
YÀ MÉ NØ̀ NGÀ YÀ NĪTǾL ÍÈ .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w$
```

## Lexical Building (i.e. word-to-word)






