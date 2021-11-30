# Log File of Word-to-Word Translation Experiment for Myanmar Ethnic Languages

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

## Folder Structure for Data

w2w ဆိုတဲ့ folder ထဲမှာ ရှိတဲ့ train.x နဲ့ test.x ဒေတာတွေကိုပဲ word-to-word lexicon building/translation experiment အတွက် သုံးသွားမှာပါ။  
Folder structure ကို မြင်ရအောင် tree command နဲ့ရိုက်ပြရရင် အောက်ပါအတိုင်းပါ။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x$ tree -d -L 2 -P *w2w
.
├── my-bk
│   ├── 1
│   └── w2w
├── my-ch
│   └── w2w
├── my-kc
│   ├── one-file
│   └── w2w
├── my-ky
│   └── w2w
├── my-mo
│   ├── 12Dec2020
│   ├── 22Aug2021
│   └── w2w
├── my-pk
│   ├── 18Jan2021
│   └── w2w
├── my-po
│   ├── latest
│   ├── old-ver
│   └── w2w
├── my-rk
│   ├── data
│   └── w2w
├── my-rw
│   ├── data
│   └── w2w
├── my-sh
│   ├── data
│   └── w2w
├── my-sk
│   ├── data
│   └── w2w
├── rk-bk
│   ├── 1
│   └── w2w
└── rw-kc
    ├── data
    └── w2w

39 directories
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x$
```

## Lexicon Building (i.e. word-to-word)

shell script တစ်ပုဒ် ရေးခဲ့တယ်။  

```bash
#!/bin/bash

# /media/ye/project2/exp/word2word-tran/word2word/my-x/ အောက်မှာ ရှိတဲ့ for loop နဲ့ looping ပတ်ထားတဲ့ src-trg ဖိုလ်ဒါတွေအောက်က
# train.src, train.trg ဖိုင်တွေကို သုံးပြီးတော့ lexicon တွေ ဆောက်ပေးသွားမှာပါ
# output folder ကတော့ w2w/lex/ အောက်မှာပါ
# 
# lexicon building between Myanmar (Burmese) and other ethnic languages
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 28 Nov 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; echo "src: $src";
    trg=${fd#*-}; echo "trg: $trg";
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; echo "ref_path: $ref_path";
    echo "time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 $src --lang2 $trg --datapref $ref_path/train --save_pmi --save_cooccurrence --savedir $ref_path/lex;";
    time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 $src --lang2 $trg --datapref $ref_path/train --save_pmi --save_cooccurrence --savedir $ref_path/lex;
    
done
```

အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x$ ./build-lexicon.sh 
src: my
trg: bk
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 bk --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.30s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 69825/69825 [00:00<00:00, 4284817.51it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9607/9607 [00:00<00:00, 3449886.86it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 69313/69313 [00:00<00:00, 4494948.64it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9444/9444 [00:00<00:00, 3262044.55it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 10622/10622 [00:00<00:00, 26209.05it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=9606)
Entering multiprocessing with 16 workers... (#words=9443)
Time taken for step 5: 2.93s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9606/9606 [00:00<00:00, 24098.13it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9443/9443 [00:00<00:00, 26541.28it/s]
Done!

real	0m6.084s
user	0m13.525s
sys	0m2.449s
src: my
trg: ch
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 ch --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.38s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 137912/137912 [00:00<00:00, 4730455.70it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 5702/5702 [00:00<00:00, 3485777.79it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 101624/101624 [00:00<00:00, 4415230.63it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 14432/14432 [00:00<00:00, 3249178.49it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 14883/14883 [00:00<00:00, 17643.62it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=5702)
Entering multiprocessing with 16 workers... (#words=14432)
Time taken for step 5: 4.45s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5702/5702 [00:00<00:00, 14983.81it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 14432/14432 [00:00<00:00, 20486.91it/s]
Done!

real	0m7.740s
user	0m22.570s
sys	0m2.477s
src: my
trg: kc
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 kc --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.68s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 351258/351258 [00:00<00:00, 3284098.77it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 4673/4673 [00:00<00:00, 3553296.34it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 309287/309287 [00:00<00:00, 4621344.32it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 10726/10726 [00:00<00:00, 3414916.10it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 38073/38073 [00:02<00:00, 15496.26it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=4673)
Entering multiprocessing with 16 workers... (#words=10726)
Time taken for step 5: 7.41s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4673/4673 [00:00<00:00, 11661.24it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 10726/10726 [00:00<00:00, 14977.72it/s]
Done!

real	0m12.818s
user	0m40.522s
sys	0m3.444s
src: my
trg: ky
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 ky --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.70s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 83988/83988 [00:00<00:00, 4221496.33it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 11387/11387 [00:00<00:00, 3120991.94it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 81431/81431 [00:00<00:00, 4455107.60it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9500/9500 [00:00<00:00, 3129094.39it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 10131/10131 [00:00<00:00, 11543.18it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=11387)
Entering multiprocessing with 16 workers... (#words=9500)
Time taken for step 5: 5.07s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 11387/11387 [00:00<00:00, 19873.10it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9500/9500 [00:00<00:00, 18704.73it/s]
Done!

real	0m8.684s
user	0m26.875s
sys	0m3.037s
src: my
trg: mo
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 mo --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.29s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 50351/50351 [00:00<00:00, 2733074.51it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9667/9667 [00:00<00:00, 2690890.41it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 61880/61880 [00:00<00:00, 4233574.72it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9836/9836 [00:00<00:00, 3401927.45it/s]
Step 4. Update count dictionaries
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████| 8873/8873 [00:01<00:00, 5072.41it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=9657)
Entering multiprocessing with 16 workers... (#words=9279)
Time taken for step 5: 5.40s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9657/9657 [00:00<00:00, 27610.98it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9279/9279 [00:00<00:00, 30398.40it/s]
Done!

real	0m9.082s
user	0m26.018s
sys	0m3.606s
src: my
trg: pk
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 pk --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.63s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 110197/110197 [00:00<00:00, 3027006.77it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 16253/16253 [00:00<00:00, 2778140.96it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 111754/111754 [00:00<00:00, 4322006.50it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 19766/19766 [00:00<00:00, 2721842.90it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 19039/19039 [00:00<00:00, 27371.60it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=16253)
Entering multiprocessing with 16 workers... (#words=19766)
Time taken for step 5: 5.42s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 16253/16253 [00:00<00:00, 26082.32it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 19766/19766 [00:00<00:00, 28641.49it/s]
Done!

real	0m9.209s
user	0m24.334s
sys	0m3.434s
src: my
trg: po
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 po --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 1.01s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 105965/105965 [00:00<00:00, 2524448.89it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 16284/16284 [00:00<00:00, 3043131.63it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 82888/82888 [00:00<00:00, 4027962.48it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 26723/26723 [00:00<00:00, 2413063.48it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 18254/18254 [00:00<00:00, 31078.81it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=16284)
Entering multiprocessing with 16 workers... (#words=26723)
Time taken for step 5: 4.93s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 16284/16284 [00:00<00:00, 27544.21it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 26723/26723 [00:00<00:00, 38011.84it/s]
Done!

real	0m9.016s
user	0m19.201s
sys	0m3.025s
src: my
trg: rk
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 rk --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.52s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 124683/124683 [00:00<00:00, 4325759.80it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 16511/16511 [00:00<00:00, 2999876.69it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 122412/122412 [00:00<00:00, 4482253.21it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 17993/17993 [00:00<00:00, 3191310.55it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 18273/18273 [00:00<00:00, 21995.05it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=16507)
Entering multiprocessing with 16 workers... (#words=17992)
Time taken for step 5: 5.63s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 16507/16507 [00:00<00:00, 25283.35it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 17992/17992 [00:00<00:00, 25036.82it/s]
Done!

real	0m9.450s
user	0m25.689s
sys	0m3.717s
src: my
trg: rw
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 rw --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.29s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 42693/42693 [00:00<00:00, 2201468.17it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 3569/3569 [00:00<00:00, 2247668.31it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 43361/43361 [00:00<00:00, 3743705.55it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 4074/4074 [00:00<00:00, 3336769.09it/s]
Step 4. Update count dictionaries
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5276/5276 [00:00<00:00, 17161.60it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=3569)
Entering multiprocessing with 16 workers... (#words=4074)
Time taken for step 5: 2.04s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3569/3569 [00:00<00:00, 18129.43it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4074/4074 [00:00<00:00, 20328.10it/s]
Done!

real	0m3.766s
user	0m10.488s
sys	0m2.275s
src: my
trg: sh
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 sh --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.27s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 112456/112456 [00:00<00:00, 4237753.26it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 15081/15081 [00:00<00:00, 3223970.37it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 91651/91651 [00:00<00:00, 4332722.70it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 24198/24198 [00:00<00:00, 2533164.48it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 16433/16433 [00:00<00:00, 25575.23it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=15081)
Entering multiprocessing with 16 workers... (#words=24198)
Time taken for step 5: 4.81s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 15081/15081 [00:00<00:00, 25525.38it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 24198/24198 [00:00<00:00, 34248.08it/s]
Done!

real	0m8.135s
user	0m21.056s
sys	0m3.273s
src: my
trg: sk
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 my --lang2 sk --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.94s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 405869/405869 [00:00<00:00, 3761889.96it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 20906/20906 [00:00<00:00, 3043811.42it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 260296/260296 [00:00<00:00, 4098784.94it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 81659/81659 [00:00<00:00, 2368048.33it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 68471/68471 [00:01<00:00, 34449.46it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=20906)
Entering multiprocessing with 16 workers... (#words=81659)
Time taken for step 5: 12.42s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 20906/20906 [00:01<00:00, 17607.39it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 81659/81659 [00:02<00:00, 38100.20it/s]
Done!

real	0m20.639s
user	0m52.105s
sys	0m5.725s
src: rk
trg: bk
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 rk --lang2 bk --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.30s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 69825/69825 [00:00<00:00, 3126552.26it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9607/9607 [00:00<00:00, 3392664.69it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 68372/68372 [00:00<00:00, 4545314.03it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 9937/9937 [00:00<00:00, 3384118.13it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 10622/10622 [00:00<00:00, 26527.92it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=9607)
Entering multiprocessing with 16 workers... (#words=9935)
Time taken for step 5: 3.06s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9607/9607 [00:00<00:00, 25497.20it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9935/9935 [00:00<00:00, 26991.65it/s]
Done!

real	0m5.387s
user	0m13.218s
sys	0m2.610s
src: rw
trg: kc
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w
time python /media/ye/project2/exp/word2word-tran/word2word/make.py --lang1 rw --lang2 kc --datapref /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/train --save_pmi --save_cooccurrence --savedir /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex;
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.29s
Step 3. Compute vocabularies
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 86399/86399 [00:00<00:00, 2613940.72it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 2232/2232 [00:00<00:00, 3267604.37it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 80096/80096 [00:00<00:00, 4706062.44it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 4739/4739 [00:00<00:00, 3707667.72it/s]
Step 4. Update count dictionaries
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9900/9900 [00:00<00:00, 18754.78it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=2232)
Entering multiprocessing with 16 workers... (#words=4739)
Time taken for step 5: 1.86s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2232/2232 [00:00<00:00, 12635.92it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4739/4739 [00:00<00:00, 19290.60it/s]
Done!

real	0m3.893s
user	0m10.158s
sys	0m1.700s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x$
```

ပြဿနာမရှိပဲ အဆင်ပြေပြေနဲ့ run လို့ ပြီးစီးသွားတယ် ဆိုရင် lexicon ဖိုင်တွေက source-target အသီးသီးအတွက် w2w/lex/ ဖိုလ်ဒါအောက်မှာ ရှိပါလိမ့်မယ်။  
ဥပမာ "မြန်မာ-ဘိတ်" အတွဲအတွက်ဆိုရင် အောက်ပါ path အောက်မှာ pkl ဖိုင်တွေကို lexicon ouput အနေနဲ့ ရလာမှာ ဖြစ်ပါတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w$ tree
.
├── all.bk
├── all.my
├── lex
│   ├── bk-my.pkl
│   ├── co
│   │   ├── bk-my.pkl
│   │   └── my-bk.pkl
│   ├── my-bk.pkl
│   └── pmi
│       ├── bk-my.pkl
│       └── my-bk.pkl
├── test.bk
├── test.my
├── train.bk
└── train.my

3 directories, 12 files
```

ထိုနည်းလည်းကောင်း "မြန်မာ-စကောကရင်" အတွဲအတွက်ဆိုရင် အောက်ပါ my-sk/w2w/lex အောက်မှာ lexicon ဖိုင်တွေ (.pkl) ရလာပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$ tree
.
├── all.my
├── all.sk
├── lex
│   ├── co
│   │   ├── my-sk.pkl
│   │   └── sk-my.pkl
│   ├── my-sk.pkl
│   ├── pmi
│   │   ├── my-sk.pkl
│   │   └── sk-my.pkl
│   └── sk-my.pkl
├── test.my
├── test.sk
├── train.my
└── train.sk

3 directories, 12 files
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w$
```

 For these reasons, we consider
approaches based on (monolingual and cross-lingual) cooccurrence counts: co-occurrences, pointwise mutual information (PMI), and co-occurrences with controlled predictive effects (CPE).

ဒီနေရာမှာ "lex/" အောက်မှာ ရှိတဲ့ ".pkl" ဖိုင်တွေက CPE (Controlled Predictive Effects) approach နဲ့ ဆွဲထုတ်ထားတဲ့ lexicon ဖိုင်တွေပါ။ "co/" ဖိုလ်ဒါအောက်မှာ ရှိတဲ့ ".pkl" တွေက co-occurrence count approach နဲ့ ဆွဲထုတ်ထားတာ ဖြစ်ပြီးတော့ "pmi/" ဖိုလ်ဒါအောက် က ".pkl" ဖိုင်တွေကတော့ PMI (Pointwise Mutual Information) approach နဲ့ ဆွဲထုတ်ထားတာ ဖြစ်ပါတယ်။  

## Prepare Some Running Scripts

translation လုပ်ဖို့အတွက် python ပရိုဂရမ်ကို အောက်ပါအတိုင်း ရေခဲ့တယ်။  

```python
import sys
from word2word import Word2word

# word-to-word translation with lexicon
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 28 Nov 2021
#
# How to run: python ./translate.py <source> <target> <lexicon_path> <test-data_path> > <hyp-filename>
# for Myanmar to Beik, python ./translate.py my bk ./my-x/my-bk/w2w/lex/ ./my-x/my-bk/w2w/test.my
# for Beik to Myanmar, python ./translate.py bk my ./my-x/my-bk/w2w/lex/ ./my-x/my-bk/w2w/test.bk
# for PMI approach, python ./translate.py bk my ./my-x/my-bk/w2w/lex/pmi/ ./my-x/my-bk/w2w/test.bk
# for co-occurrence approach, python ./translate.py bk my ./my-x/my-bk/w2w/lex/co/ ./my-x/my-bk/w2w/test.bk

src=sys.argv[1]
trg=sys.argv[2]
lexicon_path=sys.argv[3]
test_file_path=sys.argv[4]
#nbest=sys.argv[5] # nbest တန်ဖိုးပေးရင် စာလုံးတိုင်းကို OOV ဆိုပြီး ထွက်လာလို့ nbest တွက်တဲ့ module ကို ဝင်ပြင်မှရလိမ့်မယ်

print('src: ', src, ', trg: ', trg, ', lexicon path:', lexicon_path)
my2x = Word2word.load(src, trg, lexicon_path)

def percentage(oov, total):
  percentage = 100 * float(oov)/float(total)
  return percentage
  
with open(test_file_path, 'r') as f:
    count=0
    oov=0
    for line in f:
        word_list=line.strip().split()
        for word in word_list:
            try:
                target_word= my2x(word)
                count=count+1
            except:
                target_word='OOV'
                oov=oov+1
            print(target_word)
        print("\n")

oov_percentage=percentage(oov, count)
print(f'OOV percentage:  {oov_percentage:.2f}%')

```

အထက်ပါ python script ကို run ရင် အောက်ပါလိုမျိုး စာလုံးတစ်လုံးချင်းစီကို lexicon ကို သုံးပြီး ဘာသာပြန်ပေးသွားပါလိမ့်မယ်။
test ဖိုင်မှာက စာကြောင်းအလိုက် ရှိပေမဲ့ အထက်ပါ python script မှာ ရေးထားတဲ့ အတိုင်းပဲ စာကြောင်းကို space နဲ့ split လုပ်ချလိုက်ပြီး list အနေနဲ့ သိမ်းပြီးမှ အဲဒီ list ကို looping ပတ်ပြီး စာလုံး တစ်လုံးချင်းစီ translate လုပ်သွားတာမို့.... စာကြောင်း တစ်ကြောင်းနဲ့ တစ်ကြောင်းအကြားမှာ space ခြားပြီး print ထုတ်ထားပါတယ်။ default nbest=5 မို့လို့ ဘာသာပြန်ခိုင်းတဲ့ စာလုံးတစ်လုံးစီအတွက် ဖြစ်နိုင်တဲ့ target language ရဲ့ စာလုံး ၅လုံးအဖြစ် ဘာသာပြန်ပေးပါလိမ့်မယ်။   

အောက်ပါ ဥပမာက ဘိတ်ဘာသာကနေ မြန်မာ ဘာသာကို ဘာသာပြန်ပြီး ထွက်လာတဲ့ output တွေပါ။   
ပေးထားတဲ့ lexicon path က pmi path မို့လို့... PMI approach နဲ့ ဆောက်ထားတဲ့ lexicon ကို သုံးထားပါတယ်။

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python ./translate.py bk my ./my-x/my-bk/w2w/lex/pmi/ ./my-x/my-bk/w2w/test.bk

['နင်', 'အဖြေ', 'ဘယ်သူ့ကို', 'ဘာတွေ', 'နေတာလဲ']
['လူတွေက', 'ပေမယ့်', 'မနေ့', 'ကျပ်', 'က']
['မို့လို့လဲ', 'လိုချင်လဲ', 'ချင်သလဲ', 'ဘာ', 'သိဘူး']
['ကောင်းပုံ', 'ဒီအစားအစာတွေက', 'အကြောင်းကိစ္စနဲ့', 'အစားအစာက', 'ဝယ်']
['ခက်ပါတယ်', 'အရေးကြီးတယ်', 'စိတ်ရှည်', 'အသင့်ဖြစ်', 'ဖြစ်နေပြီ']
['ဒါ', '၊', 'ပါဘူး', 'ကျေးဇူးပြုပြီး', 'ဘယ်']


['ကြပါနဲ့ခင်ဗျာ', 'ငေးမှိုင်', 'စာဖတ်ခန်း', 'ဆက်နေလို့', 'တိတ်ဆိတ်တဲ့']
['ကျားလေးက', 'ချထား', 'တစ်မှေး', 'နေ့လည်ခင်းကြီး', 'နေ့လယ်ခင်း']
['ခက်ပါတယ်', 'အရေးကြီးတယ်', 'စိတ်ရှည်', 'အသင့်ဖြစ်', 'ဖြစ်နေပြီ']
['ဟုတ်ဘူး', 'သေးဘူးလား', 'ကြဘူးလား', 'တော့ဘူးလား', 'မ']
['သင့်တော်', 'မေး', 'ပါဘူး', 'ဖို့', 'သူမ']
['ဘယ်တော့မှ', 'ရှည်', 'ခဲ့ပါ', 'ခန်း', 'ဘယ်တုန်းကမှ']
['ဒါ', '၊', 'ပါဘူး', 'ကျေးဇူးပြုပြီး', 'ဘယ်']


['မိတ်ဆွေ', 'လွယ်လွယ်လေးပါ', 'အတွက်', 'အဲ့ဒါ', 'ကျွန်တော့်']
['သူမဟာ', 'အံ့ဩ', 'သူမက', 'ပါလိမ့်မယ်', 'ထားဘူး']
['ကျွန်တော်ရို့စာစီစာကုံး', 'လိုက်ဖက်မယ့်ဟာ', 'လိုက်မယ့်ဟာ', 'အရေးကြီးတယ်', 'လွယ်လွယ်လေးပါ']
['ကူးချ', 'လွယ်လွယ်လေးပါ', 'မြစ်ကို', 'ပန်းချီ', 'ဖြတ်ပြီး']
['ဒါ', '၊', 'ပါဘူး', 'ကျေးဇူးပြုပြီး', 'ဘယ်']


OOV percentage:  9.71%

```

language pair တွေ အားလုံးကို run ဖို့အတွက်က အထက်ပါ python ကို shell script ထဲကနေ ခေါ်run ခဲ့ပါတယ်။  
ရေးခဲ့တဲ့ shell script က အောက်ပါအတိုင်းပါ...  

```bash
#!/bin/bash

# testing or word-to-word translation with lexicon between Myanmar (Burmese) and other ethnic languages
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 28 Nov 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; 
    trg=${fd#*-}; 
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; echo "ref_path: $ref_path";

    # run ရတဲ့ ပုံစံက အောက်ပါအတိုင်း
    #python ./translate.py <source> <target> <lexicon_path> <test-data_path> > <hyp-filename>
    
    # for source-to-target translation
    echo "$src-$trg word2word translation results: co, pmi and cpe order... ";
    python ./translate.py $src $trg $ref_path/lex/co $ref_path/test.$src > $ref_path/lex/co/$src2$trg.co.hyp; tail -n 1 $ref_path/lex/co/$src2$trg.co.hyp;
    python ./translate.py $src $trg $ref_path/lex/pmi $ref_path/test.$src > $ref_path/lex/pmi/$src2$trg.pmi.hyp; tail -n 1 $ref_path/lex/pmi/$src2$trg.pmi.hyp;
    python ./translate.py $src $trg $ref_path/lex/ $ref_path/test.$src > $ref_path/lex/$src2$trg.cpe.hyp; tail -n 1 $ref_path/lex/$src2$trg.cpe.hyp;
    
    # for target-to-source translation
    echo "$trg-$src word2word translation results: co, pmi and cpe order... ";
    python ./translate.py $trg $src $ref_path/lex/co/ $ref_path/test.$trg > $ref_path/lex/co/$trg2$src.co.hyp; tail -n 1 $ref_path/lex/co/$trg2$src.co.hyp;
    python ./translate.py $trg $src $ref_path/lex/pmi/ $ref_path/test.$trg > $ref_path/lex/pmi/$trg2$src.pmi.hyp; tail -n 1 $ref_path/lex/pmi/$trg2$src.pmi.hyp;
    python ./translate.py $trg $src $ref_path/lex/ $ref_path/test.$trg > $ref_path/lex/$trg2$src.cpe.hyp; tail -n 1 $ref_path/lex/$trg2$src.cpe.hyp;
    echo "=========="
done

```

## Word2Word Translation Experiment

အထက်က shell script ကို သုံးပြီး ဆောက်ထားတဲ့ lexicon တွေနဲ့ ဘာသာပြန်ကြည့်တော့ ရလဒ်တွေက အောက်ပါအတိုင်း ရရှိပါတယ်။  
OOV % ရလဒ်တွေကို source-target တစ်တွဲစီအတွက် co-occurrences, PMI နဲ့ CPE ဆိုတဲ့ အစီအစဉ်နဲ့ print လုပ်ပြထားပါတယ်။  
test data က open test ပါ။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time ./test-lexicon.sh 
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w
my-bk word2word translation results: co, pmi and cpe order... 
OOV percentage:  6.92%
OOV percentage:  6.92%
OOV percentage:  6.92%
bk-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  9.71%
OOV percentage:  9.71%
OOV percentage:  9.71%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w
my-ch word2word translation results: co, pmi and cpe order... 
OOV percentage:  7.53%
OOV percentage:  7.53%
OOV percentage:  7.53%
ch-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  15.21%
OOV percentage:  15.21%
OOV percentage:  15.21%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w
my-kc word2word translation results: co, pmi and cpe order... 
OOV percentage:  2.12%
OOV percentage:  2.12%
OOV percentage:  2.12%
kc-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  0.31%
OOV percentage:  0.31%
OOV percentage:  0.31%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w
my-ky word2word translation results: co, pmi and cpe order... 
OOV percentage:  9.96%
OOV percentage:  9.96%
OOV percentage:  9.96%
ky-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  12.29%
OOV percentage:  12.29%
OOV percentage:  12.29%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w
my-mo word2word translation results: co, pmi and cpe order... 
OOV percentage:  4.40%
OOV percentage:  4.40%
OOV percentage:  4.40%
mo-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  8.69%
OOV percentage:  8.69%
OOV percentage:  8.69%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w
my-pk word2word translation results: co, pmi and cpe order... 
OOV percentage:  11.11%
OOV percentage:  11.11%
OOV percentage:  11.11%
pk-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  24.06%
OOV percentage:  24.06%
OOV percentage:  24.06%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w
my-po word2word translation results: co, pmi and cpe order... 
OOV percentage:  12.65%
OOV percentage:  12.65%
OOV percentage:  12.65%
po-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  61.57%
OOV percentage:  61.57%
OOV percentage:  61.57%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w
my-rk word2word translation results: co, pmi and cpe order... 
OOV percentage:  10.26%
OOV percentage:  10.26%
OOV percentage:  10.26%
rk-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  12.05%
OOV percentage:  12.05%
OOV percentage:  12.05%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w
my-rw word2word translation results: co, pmi and cpe order... 
OOV percentage:  3.71%
OOV percentage:  3.71%
OOV percentage:  3.71%
rw-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  651.52%
OOV percentage:  651.52%
OOV percentage:  651.52%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w
my-sh word2word translation results: co, pmi and cpe order... 
OOV percentage:  7.10%
OOV percentage:  7.10%
OOV percentage:  7.10%
sh-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  11.25%
OOV percentage:  11.25%
OOV percentage:  11.25%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w
my-sk word2word translation results: co, pmi and cpe order... 
OOV percentage:  0.00%
OOV percentage:  0.00%
OOV percentage:  0.00%
sk-my word2word translation results: co, pmi and cpe order... 
OOV percentage:  9.52%
OOV percentage:  9.52%
OOV percentage:  9.52%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w
rk-bk word2word translation results: co, pmi and cpe order... 
OOV percentage:  8.73%
OOV percentage:  8.73%
OOV percentage:  8.73%
bk-rk word2word translation results: co, pmi and cpe order... 
OOV percentage:  9.71%
OOV percentage:  9.71%
OOV percentage:  9.71%
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w
rw-kc word2word translation results: co, pmi and cpe order... 
OOV percentage:  628.00%
OOV percentage:  628.00%
OOV percentage:  628.00%
kc-rw word2word translation results: co, pmi and cpe order... 
OOV percentage:  15.90%
OOV percentage:  15.90%
OOV percentage:  15.90%
==========

real	0m12.027s
user	0m17.649s
sys	0m31.551s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Shell Script for Pickle to Human Readable Conversion

lexicon ဖိုင်တွေက .pkl နဲ့ သိမ်းထားပြီး လူကဖတ်နိုင်ဖို့အတွက်က conversion လုပ်ဖို့ လိုအပ်ပါတယ်။  
အဲဒီအတွက် shell script ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
#!/bin/bash

# converting pkl files to human readable text files
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 1 Dec 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; 
    trg=${fd#*-}; 
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; echo "ref_path: $ref_path";

    # run ရတဲ့ ပုံစံက အောက်ပါအတိုင်း
    #python -m pickle  <lexicon_path> > <converted-filename>
    
    # for source-to-target lexicon
    echo "converting for $src-$trg lexicons: co, pmi and cpe order... ";
    python -m pickle $ref_path/lex/co/$src-$trg.pkl > $ref_path/lex/co/$src-$trg.co.normal; 
    echo "$ref_path/lex/co/$src-$trg.co.normal"; tail -n 3 $ref_path/lex/co/$src-$trg.co.normal; 
    python -m pickle $ref_path/lex/pmi/$src-$trg.pkl > $ref_path/lex/pmi/$src-$trg.pmi.normal;
    echo "$ref_path/lex/pmi/$src-$trg.pmi.normal"; tail -n 3 $ref_path/lex/pmi/$src-$trg.pmi.normal;
    python -m pickle $ref_path/lex/$src-$trg.pkl > $ref_path/lex/$src-$trg.cpe.normal;
    echo "$ref_path/lex/$src-$trg.cpe.normal"; tail -n 3 $ref_path/lex/$src-$trg.cpe.normal;
    
    # for target-to-source lexicon
    echo "converting for $trg-$src lexicons: co, pmi and cpe order... ";
    python -m pickle $ref_path/lex/co/$trg-$src.pkl > $ref_path/lex/co/$trg-$src.co.normal;
    echo "$ref_path/lex/co/$trg-$src.co.normal"; tail -n 3 $ref_path/lex/co/$trg-$src.co.normal;
    python -m pickle $ref_path/lex/pmi/$trg-$src.pkl > $ref_path/lex/pmi/$trg-$src.pmi.normal;
    echo "$ref_path/lex/pmi/$trg-$src.pmi.normal"; tail -n 3 $ref_path/lex/pmi/$trg-$src.pmi.normal;
    python -m pickle $ref_path/lex/$trg-$src.pkl > $ref_path/lex/$trg-$src.cpe.normal;
    echo "$ref_path/lex/$trg-$src.cpe.normal"; tail -n 3 $ref_path/lex/$trg-$src.cpe.normal;
    echo "=========="
    
done


```

Conversion လုပ်ပြီးတဲ့အခါမှာ လူ့မျက်စိနဲ့ ဖိုင်တွေကို check လုပ်လို့ ရပါပြီ။  
format က ပထမဆုံး အပိုင်းမှာ source word စာလုံး တစ်လုံးချင်းစီအတွက် ID သတ်မှတ်ထားတာတွေကို တွေ့ရပါလိမ့်မယ်။  
ဥပမာ ဗမာ-ပအို့ဝ့် cpe lexicon ရဲ့ normal format ဆိုရင် ဗမာစာ စာလုံး တစ်လုံးစီအတွက် ID တွေကို အောက်ပါအတိုင်း မြင်တွေ့ရပါလိမ့်မယ်။    
(ဒီနေရာမှာ word segmentation ကတော့ parallel corpus ထဲမှာ ဖြတ်ထားတဲ့အတိုင်းကိုပဲ ယူချလာမှာ ဖြစ်ပါတယ်။)  

```
({'"': 600,
  '(': 1225,
  ')': 1224,
  ',': 6063,
  ':': 1374,
  'က': 9,
  'ကကတစ်': 16283,
  'ကကတစ်ကို': 16282,
  'ကကော': 16281,
  'ကကောင်း်ကို': 16280,
  'ကချင်': 16279,
  'ကချေသည်': 6062,
  'ကင်': 3596,
  'ကင်ဆာ': 6061,
  'ကင်မရာ': 1028,
```

ဗမာ စာလုံးတွေ ကုန်သွားတဲ့အခါမှာတော့ ပအို့ဝ့်စာလုံးတွေကို ID သတ်မှတ်ထားတာကို တွေ့ရပါလိမ့်မယ်။  

```
  '\u200bအဲဒါ': 3598,
  '\u200bအဲဒါက': 3597,
  '\u200bဪ': 6065,
  '…': 6064},
 {0: 'ခွေ',
  1: 'နာꩻ',
  2: 'ဟောင်း',
  3: 'နဝ်ꩻ',
  4: 'ဝွေꩻ',
  5: 'ဝွေꩻမူႏ',
  6: 'ဝွေꩻသီး',
  7: 'နီ',
  8: 'နဝ်ꩻနဝ်ꩻ',
  9: 'ဒျာႏ',
  10: 'အီး',
  11: 'တ',
  12: 'တဝ်း',
```

ပအိုဝ့် စာလုံးတွေ ကို ID သတ်မှတ်တာ ကုန်သွားရင်တော့ အခုကြည့်နေတဲ့ direction က ဗမာ-ပအို့ဝ့်မို့လို့ ဗမာစာလုံး တစ်လုံးစီအတွက် ဖြစ်နိုင်တဲ့ ပအို့ဝ့်စာလုံး အများဆုံး ၁၀လုံးအထိ ကို list နဲ့ learn လုပ်ထားတဲ့ အပိုင်းကို စတွေ့ရပါလိမ့်မယ်။  

```
  26713: 'ကကုဲင်ထိုꩻအခိန်ႏနဝ်ꩻ',
  26714: 'ကကုဲင်ထိုꩻဒါႏ',
  26715: 'ကကားတဖူꩻခိန်ႏ',
  26716: 'ကကာ',
  26717: 'ကကတစ်',
  26718: 'b',
  26719: '_',
  26720: '9',
  26721: '5144.',
  26722: '402'},
 {0: [132, 151, 190, 188, 164, 140, 110, 142, 124, 104],
  1: [230, 322, 315, 197, 176, 229, 209, 213, 195, 182],
  2: [274, 203, 230, 254, 188, 128, 232, 160, 136, 113],
  3: [424, 184, 387, 578, 385, 322, 315, 362, 364, 268],
  4: [5, 639, 744, 355, 307, 177, 374, 339, 191, 147],
  5: [840, 281, 390, 243, 333, 199, 215, 292, 171, 222],
  6: [1058, 402, 535, 222, 792, 1517, 462, 207, 258, 811],
  7: [8, 297, 205, 195, 809, 688, 1405, 279, 852, 562],
  8: [6, 487, 595, 395, 1086, 540, 539, 902, 296, 233],
  9: [474, 648, 296, 472, 503, 212, 255, 197, 177, 256],
  10: [345, 1251, 296, 673, 1626, 1560, 632, 822, 587, 393],
```

Format က အထက်ပါ ရှင်းပြထားတဲ့အတိုင်း သွားတာမို့ .normal ဖိုင်ကို tail လုပ်ကြည့်ရင် တွေ့ရတဲ့ နောက်ဆုံး စာကြောင်းမှာ ရှိနေတဲ့ ID နံပါတ်က "source-target word-to-word translation" အတွက် ဆောက်ထားတဲ့ dictionary size လို့ နားလည်လို့ ရပါလိမ့်မယ်။ အခု ဥပမာအဖြစ် ပြနေတဲ့ ဗမာ-ပအို့ဝ့် အတွက်ဆိုရင် စုစုပေါင်း 16283 (တစ်သောင်း ခြောက်ထောင် နှစ်ရာရှစ်ဆယ့်သုံး) လုံး ရှိတာကို တွေ့ရပါလိမ့်မယ်။  

```
  16274: [1378, 247, 497, 492],
  16275: [9518, 24582, 13148, 388, 60, 527, 88, 26, 7, 3],
  16276: [684, 609, 869, 497, 1888, 50, 25, 1116, 7, 0],
  16277: [18509, 23638, 3375, 25352, 3655, 247, 190, 3],
  16278: [25909, 19015, 1, 0],
  16279: [24057, 25133, 9174, 199, 103, 172, 90, 9],
  16280: [26658, 2910, 105, 3],
  16281: [289, 50, 248],
  16282: [13398, 26621, 349, 298, 3, 0],
  16283: [26717, 20115, 11816, 4838, 1773, 14]})
```

## Convert .pkl to .normal and Count the Lexicon Size

ဒီနေရာမှာတော့ အထက်မှာ ရေးပြခဲ့တဲ့ shell script ကို run ပြီး lexicon size တစ်ခုချင်းစီကို ရေတွက် ကြည့်ကြရအောင်။  
Experiment က approach သုံးမျိုးကို သုံးခဲ့တာမို့ language pair တစ်ခုစီအတွက် lexicon က စုစုပေါင်း အောက်ပါအတိုင်း ခြောက်ခု စီ ရှိပါလိမ့်မယ်။

### Source-Target Lexicons

1. Source-Target Co-occurrences Lexicon
2. Source-Target PMI Lexicon
3. Source-Target CPE Lexicon

### Target-Source Lexicons

4. Target-Source Co-occurrences Lexicon
5. Target-Source PMI Lexicon
6. Source-Target CPE Lexicon

Shell script ကို အောက်ပါအတိုင်း run ခဲ့ပါတယ်။  
Lexicon တစ်ခုချင်းစီရဲ့ size ကိုလည်း လေ့လာကြည့်ကြရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time ./pkl-to-human-readable.sh | tee lexicon-counting.log

```


## Reference

- [https://github.com/ye-kyaw-thu/error-overflow/blob/master/word2word_translation-exp-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/word2word_translation-exp-log.md)
- [word2word](https://github.com/kakaobrain/word2word)
- [https://stackoverflow.com/questions/918886/how-do-i-split-a-string-on-a-delimiter-in-bash](https://stackoverflow.com/questions/918886/how-do-i-split-a-string-on-a-delimiter-in-bash)
- [https://stackoverflow.com/questions/55126019/python3-to-find-number-of-features-in-pickle?noredirect=1&lq=1](https://stackoverflow.com/questions/55126019/python3-to-find-number-of-features-in-pickle?noredirect=1&lq=1)  
