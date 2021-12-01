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
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w
converting for my-bk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my-bk.co.normal
  9441: [9602, 2, 61, 246, 116, 6, 0],
  9442: [9, 711, 9603, 0],
  9443: [311, 239, 3943, 5438, 39, 2208, 14, 131, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my-bk.pmi.normal
  9441: [9602, 246, 116, 61, 6, 2, 0],
  9442: [9603, 711, 9, 0],
  9443: [5438, 3943, 2208, 311, 239, 131, 39, 14, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my-bk.cpe.normal
  9441: [9602, 246, 61, 2, 116, 6, 0],
  9442: [9603, 711, 9, 0],
  9443: [5438, 2208, 39, 3943, 131, 239, 311, 14, 0]})
converting for bk-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk-my.co.normal
  9604: [9, 31, 1, 3, 46, 403, 0],
  9605: [316, 2201, 90, 5576, 237, 2388, 64, 9300, 0],
  9606: [2, 60, 144, 195, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk-my.pmi.normal
  9604: [403, 46, 31, 9, 3, 1, 0],
  9605: [9300, 5576, 2388, 2201, 316, 237, 90, 64, 0],
  9606: [195, 144, 60, 2, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk-my.cpe.normal
  9604: [403, 46, 31, 1, 9, 3, 0],
  9605: [5576, 9300, 2201, 237, 2388, 90, 316, 64, 0],
  9606: [195, 144, 60, 2, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w
converting for my-ch lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my-ch.co.normal
  14429: [531, 2382, 2902, 16, 472, 27, 3818, 4509, 14, 50],
  14430: [1, 115, 116, 33, 11, 650, 4341, 75, 9, 521],
  14431: [3, 248, 11, 174, 27, 1, 276, 13, 68, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my-ch.pmi.normal
  14429: [4509, 3818, 2902, 2382, 531, 472, 50, 27, 16, 14],
  14430: [4375, 4341, 1878, 1098, 754, 650, 521, 414, 384, 345],
  14431: [276, 248, 174, 68, 27, 13, 11, 3, 1, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my-ch.cpe.normal
  14429: [531, 3818, 4509, 2382, 2902, 472, 27, 50, 16, 14],
  14430: [1, 115, 4341, 1098, 4375, 1878, 384, 414, 228, 650],
  14431: [3, 248, 11, 174, 27, 1, 276, 13, 68, 0]})
converting for ch-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch-my.co.normal
  5699: [856, 5, 8436, 12943, 300, 1489, 487, 0],
  5700: [7113, 2640, 50, 0],
  5701: [230, 5155, 689, 1572, 1078, 1571, 1, 752, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch-my.pmi.normal
  5699: [12943, 8436, 856, 1489, 487, 300, 5, 0],
  5700: [7113, 2640, 50, 0],
  5701: [5155, 1572, 1571, 1078, 752, 689, 230, 1, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch-my.cpe.normal
  5699: [856, 8436, 12943, 487, 300, 1489, 5, 0],
  5700: [7113, 2640, 50, 0],
  5701: [5155, 1572, 1571, 689, 752, 230, 1078, 1, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w
converting for my-kc lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my-kc.co.normal
  10723: [3, 4, 32, 6, 644, 340, 4004, 205, 1, 10],
  10724: [355, 4669],
  10725: [4647, 4670, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my-kc.pmi.normal
  10723: [4004, 2559, 1079, 650, 644, 452, 451, 340, 205, 43],
  10724: [4669, 355],
  10725: [4670, 4647, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my-kc.cpe.normal
  10723: [4004, 2559, 644, 1079, 205, 650, 340, 452, 451, 43],
  10724: [4669, 355],
  10725: [4647, 4670, 0]})
converting for kc-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc-my.co.normal
  4670: [407, 827, 2463, 10725, 0],
  4671: [3, 5, 67, 32, 33, 4873, 1, 35, 826, 31],
  4672: [9821, 1, 2, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc-my.pmi.normal
  4670: [10725, 2463, 827, 407, 0],
  4671: [9862, 9733, 4873, 3066, 2756, 2157, 2138, 1928, 1361, 1315],
  4672: [9821, 2, 1, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc-my.cpe.normal
  4670: [10725, 2463, 827, 407, 0],
  4671: [4873, 9733, 9862, 2138, 2157, 1315, 1000, 3066, 459, 376],
  4672: [9821, 1, 2, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w
converting for my-ky lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my-ky.co.normal
  9497: [755, 13, 11267, 15, 65, 1],
  9498: [279, 12, 0, 11272, 4, 32, 65, 1],
  9499: [2, 7977, 10540, 4185, 252, 595, 11072, 3726, 3133, 266]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my-ky.pmi.normal
  9497: [11267, 755, 65, 15, 13, 1],
  9498: [11272, 279, 65, 32, 12, 4, 1, 0],
  9499: [11072, 10540, 7977, 4185, 3726, 3133, 1254, 1119, 595, 266]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my-ky.cpe.normal
  9497: [11267, 755, 65, 15, 13, 1],
  9498: [11272, 279, 32, 65, 12, 4, 1, 0],
  9499: [7977, 10540, 4185, 11072, 3133, 1254, 266, 1119, 595, 3726]})
converting for ky-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky-my.co.normal
  11384: [4225],
  11385: [36, 43, 21, 8, 48, 565, 0],
  11386: [175, 3, 0, 1732, 5, 377, 2, 1226, 711, 143]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky-my.pmi.normal
  11384: [4225],
  11385: [565, 48, 43, 36, 21, 8, 0],
  11386: [9389, 7322, 4033, 1732, 1226, 1472, 1433, 711, 377, 476]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky-my.cpe.normal
  11384: [4225],
  11385: [565, 43, 48, 21, 36, 8, 0],
  11386: [4033, 7322, 9389, 1472, 1433, 476, 372, 104, 375, 287]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w
converting for my-mo lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my-mo.co.normal
  9830: [1, 25, 15, 1487, 2453, 14, 1886, 2565, 0],
  9831: [1, 32, 20, 854, 1144, 444, 2810, 62, 0],
  9835: [70, 2355, 2821, 6353, 3000, 1650, 7, 3095, 500, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my-mo.pmi.normal
  9830: [2565, 2453, 1886, 1487, 25, 15, 14, 1, 0],
  9831: [2810, 1144, 854, 444, 62, 32, 20, 1, 0],
  9835: [6353, 3095, 3000, 2821, 2355, 1650, 500, 70, 7, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my-mo.cpe.normal
  9830: [2453, 1886, 2565, 25, 1487, 14, 15, 1, 0],
  9831: [2810, 444, 1144, 20, 32, 62, 854, 1, 0],
  9835: [6353, 3000, 3095, 2821, 1650, 2355, 500, 70, 7, 0]})
converting for mo-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo-my.co.normal
  9664: [3, 8849, 564, 306, 181, 628, 0],
  9665: [810, 3235, 222, 1466, 13, 0],
  9666: [65, 1037, 286, 1634, 2483, 978, 689, 2085, 2050, 1234]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo-my.pmi.normal
  9664: [8849, 628, 564, 306, 181, 3, 0],
  9665: [3235, 1466, 810, 222, 13, 0],
  9666: [2483, 2085, 2050, 1634, 1418, 1234, 1037, 978, 689, 286]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo-my.cpe.normal
  9664: [8849, 306, 564, 628, 181, 3, 0],
  9665: [810, 3235, 222, 1466, 13, 0],
  9666: [978, 2050, 2085, 1234, 2483, 1634, 1037, 1418, 286, 65]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w
converting for my-pk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my-pk.co.normal
  16250: [1922, 8609, 3, 3235, 10665, 3409, 17157, 0],
  16251: [2, 18, 29, 139, 3, 51],
  16252: [7304, 18631, 15, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my-pk.pmi.normal
  16250: [17157, 10665, 8609, 3409, 3235, 1922, 3, 0],
  16251: [139, 51, 29, 18, 3, 2],
  16252: [18631, 7304, 15, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my-pk.cpe.normal
  16250: [1922, 8609, 3235, 10665, 3409, 17157, 3, 0],
  16251: [139, 51, 29, 18, 3, 2],
  16252: [7304, 18631, 15, 0]})
converting for pk-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk-my.co.normal
  19763: [12, 68, 26, 8703],
  19764: [5, 8727, 43, 8472, 190, 18, 589, 775, 2201, 212],
  19765: [33, 726, 158, 37]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk-my.pmi.normal
  19763: [8703, 68, 26, 12],
  19764: [8727, 8472, 2201, 775, 589, 518, 212, 190, 43, 18],
  19765: [726, 158, 37, 33]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk-my.cpe.normal
  19763: [8703, 68, 26, 12],
  19764: [8727, 8472, 2201, 589, 775, 518, 190, 212, 18, 43],
  19765: [726, 158, 37, 33]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w
converting for my-po lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my-po.co.normal
  16281: [50, 248, 289],
  16282: [0, 3, 298, 13398, 26621, 349],
  16283: [1773, 26717, 20115, 11816, 4838, 14]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my-po.pmi.normal
  16281: [289, 248, 50],
  16282: [26621, 13398, 349, 298, 3, 0],
  16283: [26717, 20115, 11816, 4838, 1773, 14]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my-po.cpe.normal
  16281: [289, 50, 248],
  16282: [13398, 26621, 349, 298, 3, 0],
  16283: [26717, 20115, 11816, 4838, 1773, 14]})
converting for po-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po-my.co.normal
  26720: [1111, 101, 852, 14, 11, 21, 565],
  26721: [2, 8, 14, 1048, 15],
  26722: [5075, 136, 581, 12133, 3025, 1834, 6237, 1436, 6, 3325]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po-my.pmi.normal
  26720: [1111, 852, 565, 101, 21, 14, 11],
  26721: [1048, 15, 14, 8, 2],
  26722: [12133, 6237, 5075, 3325, 3025, 1834, 1436, 581, 136, 20]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po-my.cpe.normal
  26720: [852, 565, 1111, 101, 21, 11, 14],
  26721: [1048, 8, 15, 14, 2],
  26722: [5075, 12133, 3025, 6237, 3325, 1834, 581, 6, 20, 136]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w
converting for my-rk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my-rk.co.normal
  16508: [1, 243, 4252],
  16509: [1792, 17990, 184, 1406, 7, 0],
  16510: [11, 10245, 17991, 17, 14164, 16, 17391, 20, 7, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my-rk.pmi.normal
  16508: [4252, 243, 1],
  16509: [17990, 1792, 1406, 184, 7, 0],
  16510: [17991, 17391, 14164, 10245, 20, 17, 16, 11, 7, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my-rk.cpe.normal
  16508: [4252, 243, 1],
  16509: [17990, 1406, 184, 1792, 7, 0],
  16510: [10245, 17991, 14164, 17391, 11, 16, 17, 7, 20, 0]})
converting for rk-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk-my.co.normal
  17990: [595, 16509, 12069, 0],
  17991: [1416, 16510, 12, 13157, 15, 16039, 18, 10, 0],
  17992: [6, 32, 1, 133, 6012, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk-my.pmi.normal
  17990: [16509, 12069, 595, 0],
  17991: [16510, 16039, 13157, 1416, 18, 15, 12, 10, 0],
  17992: [6012, 133, 32, 6, 1, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk-my.cpe.normal
  17990: [16509, 12069, 595, 0],
  17991: [16510, 13157, 16039, 1416, 10, 15, 18, 12, 0],
  17992: [6012, 133, 6, 32, 1, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w
converting for my-rw lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my-rw.co.normal
  3566: [60, 11, 1, 350, 5, 21, 79, 28, 141, 0],
  3567: [500, 8, 28, 35, 210, 18, 328, 507, 20, 0],
  3568: [4040, 4071]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my-rw.pmi.normal
  3566: [350, 141, 79, 60, 28, 21, 11, 5, 1, 0],
  3567: [507, 500, 328, 210, 35, 28, 20, 18, 8, 0],
  3568: [4071, 4040]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my-rw.cpe.normal
  3566: [350, 60, 141, 79, 28, 21, 1, 11, 5, 0],
  3567: [500, 507, 35, 210, 28, 18, 8, 20, 328, 0],
  3568: [4040, 4071]})
converting for rw-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw-my.co.normal
  4071: [298, 3568, 0],
  4072: [9, 135, 113, 231, 54, 6, 112, 5, 44, 20],
  4073: [2487, 474, 1164, 101, 370, 21, 6, 518, 69, 2368]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw-my.pmi.normal
  4071: [3568, 298, 0],
  4072: [135, 231, 113, 112, 54, 44, 9, 20, 6, 5],
  4073: [2487, 2368, 1164, 714, 518, 474, 370, 101, 69, 29]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw-my.cpe.normal
  4071: [298, 3568, 0],
  4072: [231, 112, 54, 20, 44, 113, 135, 5, 6, 9],
  4073: [2487, 2368, 1164, 714, 474, 518, 69, 370, 29, 101]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w
converting for my-sh lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my-sh.co.normal
  15078: [552, 1, 21, 983, 16, 1258, 0],
  15079: [1, 1512, 3616, 0],
  15080: [2704, 3784, 3381, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my-sh.pmi.normal
  15078: [1258, 983, 552, 21, 16, 1, 0],
  15079: [3616, 1512, 1, 0],
  15080: [3784, 3381, 2704, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my-sh.cpe.normal
  15078: [1258, 21, 552, 983, 16, 1, 0],
  15079: [3616, 1512, 1, 0],
  15080: [2704, 3784, 3381, 0]})
converting for sh-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh-my.co.normal
  24195: [665, 8528, 100, 1853, 1, 4495, 48, 1734, 11611, 32],
  24196: [20, 1062, 127, 447, 3711, 8, 9074, 271, 0],
  24197: [14, 36, 412, 3750, 513, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh-my.pmi.normal
  24195: [11611, 8528, 4495, 1853, 1734, 665, 184, 100, 48, 32],
  24196: [9074, 3711, 1062, 447, 271, 127, 20, 8, 0],
  24197: [3750, 513, 412, 36, 14, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh-my.cpe.normal
  24195: [8528, 11611, 4495, 1853, 1734, 665, 184, 100, 48, 32],
  24196: [9074, 3711, 271, 447, 1062, 127, 8, 20, 0],
  24197: [3750, 412, 513, 36, 14, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w
converting for my-sk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my-sk.co.normal
  20903: [46059],
  20904: [1055, 703, 509, 15784, 261],
  20905: [261, 73164, 386, 15784, 2208]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my-sk.pmi.normal
  20903: [46059],
  20904: [15784, 1055, 703, 509, 261],
  20905: [73164, 15784, 2208, 386, 261]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my-sk.cpe.normal
  20903: [46059],
  20904: [703, 15784, 1055, 509, 261],
  20905: [73164, 15784, 2208, 386, 261]})
converting for sk-my lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk-my.co.normal
  81656: [7350, 2989, 10315, 193, 7, 6, 1186, 11181],
  81657: [5549, 1, 75, 37, 32, 701, 4],
  81658: [34, 17, 4, 17216, 9, 61, 7, 27]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk-my.pmi.normal
  81656: [11181, 10315, 7350, 2989, 1186, 193, 7, 6],
  81657: [5549, 701, 75, 37, 32, 4, 1],
  81658: [17216, 61, 34, 27, 17, 9, 7, 4]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk-my.cpe.normal
  81656: [7350, 2989, 10315, 6, 1186, 11181, 7, 193],
  81657: [5549, 1, 75, 37, 32, 701, 4],
  81658: [17216, 27, 9, 61, 7, 34, 4, 17]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w
converting for rk-bk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk-bk.co.normal
  9934: [954, 1632, 6242, 3322, 495, 9099, 6577, 5495, 16, 0],
  9935: [311, 239, 3943, 5438, 39, 2208, 14, 131, 0],
  9936: [23, 75, 7, 94, 76, 130, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk-bk.pmi.normal
  9934: [9099, 6577, 6242, 5495, 3322, 1632, 954, 495, 16, 0],
  9935: [5438, 3943, 2208, 311, 239, 131, 39, 14, 0],
  9936: [130, 94, 76, 75, 23, 7, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk-bk.cpe.normal
  9934: [6242, 3322, 9099, 6577, 5495, 495, 954, 1632, 16, 0],
  9935: [5438, 2208, 39, 3943, 131, 239, 311, 14, 0],
  9936: [130, 76, 94, 75, 23, 7, 0]})
converting for bk-rk lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk-rk.co.normal
  9604: [11, 28, 1, 3, 42, 199, 0],
  9605: [216, 2172, 321, 4727, 219, 4504, 175, 354, 0],
  9606: [2, 60, 142, 273, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk-rk.pmi.normal
  9604: [199, 42, 28, 11, 3, 1, 0],
  9605: [4727, 4504, 2172, 354, 321, 219, 216, 175, 0],
  9606: [273, 142, 60, 2, 0]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk-rk.cpe.normal
  9604: [199, 28, 42, 11, 1, 3, 0],
  9605: [4727, 4504, 2172, 354, 219, 321, 175, 216, 0],
  9606: [273, 60, 142, 2, 0]})
==========
ref_path: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w
converting for rw-kc lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw-kc.co.normal
  4736: [1, 13, 782, 7, 222, 203, 42, 31, 157, 114],
  4737: [1, 116, 22, 14, 817, 46, 9, 30, 4, 62],
  4738: [2183]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw-kc.pmi.normal
  4736: [782, 461, 222, 203, 157, 114, 91, 78, 51, 42],
  4737: [817, 116, 62, 57, 46, 30, 22, 16, 14, 10],
  4738: [2183]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw-kc.cpe.normal
  4736: [782, 461, 114, 42, 157, 222, 203, 91, 51, 39],
  4737: [817, 30, 116, 46, 57, 62, 22, 16, 10, 14],
  4738: [2183]})
converting for kc-rw lexicons: co, pmi and cpe order... 
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc-rw.co.normal
  2229: [707, 3030, 255, 614, 3664, 1825, 218, 3651, 48, 483],
  2230: [617, 13, 1509, 652, 295, 84, 0],
  2231: [93, 188, 2, 723, 0, 49, 3, 53, 13, 4641]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc-rw.pmi.normal
  2229: [3664, 3651, 3030, 1825, 707, 614, 483, 255, 249, 218],
  2230: [1509, 652, 617, 295, 84, 13, 0],
  2231: [4641, 1383, 1232, 1160, 723, 497, 488, 474, 188, 93]})
/media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc-rw.cpe.normal
  2229: [3030, 3664, 3651, 483, 1825, 707, 614, 249, 48, 218],
  2230: [1509, 617, 652, 84, 295, 13, 0],
  2231: [4641, 1383, 1160, 488, 1232, 53, 474, 497, 66, 20]})
==========

real	0m43.965s
user	0m42.575s
sys	0m1.406s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$

```

အထက်ပါအတိုင်း lexicon တွေကို count လုပ်ကြည့်တော့ approach သုံးမျိုးအကြားမှာ အဘိဓာန်ရဲ့ size စာလုံးအရေအတွက်က ကွဲပြားမှု မရှိတာကို တွေ့ရပါတယ်။  
သို့သော် approach တစ်ခုချင်းစီပေါ်ကို မူတည်ပြီး ဆွဲထုတ်ထားပြီး word-to-word mapping လုပ်ထားတာတွေကတော့ တူမှာ မဟုတ်ပါဘူး...  

## Conversion of Column Format into Line

လက်ရှိ word-to-word ဘာသာပြန်ပြီးထွက်လာတဲ့ hypothesis (i.e. .hyp) ဖိုင်တွေရဲ့ format က အောက်ပါအတိုင်း nbest-X translation output အနေနဲ့ သို့မဟုတ် ကော်လံအလိုက် ရှိနေတာပါ။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ head -n 20 ./my-x/my-rk/w2w/lex/rk.cpe.hyp
src:  my , trg:  rk , lexicon path: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/
Loaded word2word custom bilingual lexicon from /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my-rk.pkl
['ဇာဖြစ်လို့လည်းဆိုကေ', 'ယင်းချင့်', 'ဇာဖြစ်လို့ကေ', 'မတ', 'ူကတ်လို့ပါ။']
['သူရို့', 'သူ့ရို့', 'ကတ်ပါရေ။', 'ခကတ်လေ', 'ဇာပိုင်နည်း']
OOV
['ကကောင်း', 'တဗျင်း', 'ကကကောင်း', 'နောက်ကျနီယာ', 'ချစ်တေ']
OOV
['လို့', 'မရပါ', 'ကံကောင်းပါစီ', 'ယင်းမမချေ', 'ထင်ရေ']
['ငါ', 'စိတ်မကောင်းပါ', 'ပြောစွာ', 'စွာကို', 'မိန့်']
['ထင်', 'နိုင်ဖို့လို့', 'ထောင်ချောက်ကို', 'တချို့က', 'ကောင်းဖို့']
['တေ။', 'တေ', 'ရေ။', 'ကံကောင်း', 'ဆန္ဒဟိ']
['ဇာသူ', 'ဒေချင့်', 'ဖို့လေး။', 'ခပါလား', 'ကိုယ်']


['ဒေချင့်', 'ဒေချင့်', 'ဒေစွာ', 'ဒေစော်', 'အမှန်ပါ']
['ဒေ', 'တိုက်တာ', 'အရသာ', 'ချင်ပါရေ', 'ညနီ']
['အပတ်မာ', 'အပတ်မှာ', 'နက်ဖန်က', 'နောက်အပတ်မာ', 'လာစား']
['တတိယ', 'ကဒေ', 'အကြိမ်', 'ဒေချင်', 'တစ်ဦးရာ']
['ပြန်ဖတ်', 'စတုတ္တ', 'ပျက်စွာ', 'လာလည်စွာ', 'အကြိမ်လား']
['ယာ', 'ရာ', 'ယာ။', 'ပဲ', 'ယင်းချင့်က']
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

အထက်ပါ format အတိုင်းမို့ hypothesis ဖိုင်ကို sentence level translation အနေနဲ့ BLEU score တွက်ကြည့်ချင်တယ်ဆိုရင် ပုံမှန် left-to-right စာကြောင်း အဖြစ် format ပြောင်းပေးဖို့ လိုအပ်ပါတယ်။  
BLEU score ရလဒ်က မကောင်းနိုင်ပေမဲ့ nbest 1 (ရှေ့ဆုံး စာလုံး) ကိုပဲ ဖြစ်ဖြစ် ယူပြီးတော့ reference နဲ့ နှိုင်းယှဉ်လို့ ရအောင် ပြင်ဆင်ပြီး evaluation လုပ်ကြည့်သင့်တယ်လို့ ထင်ပါတယ်။ 

column format ကနေ line format အဖြစ် ပြောင်းဖို့ အတွက် ရေးခဲ့တဲ့ shell script က အောက်ပါအတိုင်းပါ။  

```bash
#!/bin/bash

# converting hypothesis column files to line format
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 1 Dec 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; 
    trg=${fd#*-}; 
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; #echo "ref_path: $ref_path";

    # run ရတဲ့ ပုံစံက အောက်ပါအတိုင်း
    #python -m pickle  <lexicon_path> > <converted-filename>
    
    # for source-to-target lexicon
    echo "converting for $ref_path/lex/co/$trg.co.hyp ... ";
    cut -d "," -f1 $ref_path/lex/co/$trg.co.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/co/$trg.co.hyp.line;
    wc $ref_path/lex/co/$trg.co.hyp.line; 
    head -n 3 $ref_path/lex/co/$trg.co.hyp.line; 
    echo "converting for $ref_path/lex/pmi/$trg.pmi.hyp ... ";   
    cut -d "," -f1 $ref_path/lex/pmi/$trg.pmi.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/pmi/$trg.pmi.hyp.line;
    wc $ref_path/lex/pmi/$trg.pmi.hyp.line;
    head -n 3 $ref_path/lex/pmi/$trg.pmi.hyp.line;
    echo "converting for $ref_path/lex/$trg.cpe.hyp ... ";
    cut -d "," -f1 $ref_path/lex/$trg.cpe.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/$trg.cpe.hyp.line;
    wc $ref_path/lex/$trg.cpe.hyp.line;
    head -n 3 $ref_path/lex/$trg.cpe.hyp.line;

    
    # for target-to-source lexicon
    echo "converting for $ref_path/lex/co/$src.co.hyp ... ";
    cut -d "," -f1 $ref_path/lex/co/$src.co.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/co/$src.co.hyp.line;
    wc $ref_path/lex/co/$src.co.hyp.line;
    head -n 3 $ref_path/lex/co/$src.co.hyp.line; 
    echo "converting for $ref_path/lex/pmi/$src.pmi.hyp ... ";   
    cut -d "," -f1 $ref_path/lex/pmi/$src.pmi.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/pmi/$src.pmi.hyp.line;
    wc $ref_path/lex/pmi/$src.pmi.hyp.line;
    head -n 3 $ref_path/lex/pmi/$src.pmi.hyp.line;
    echo "converting for $ref_path/lex/$src.cpe.hyp ... ";
    cut -d "," -f1 $ref_path/lex/$src.cpe.hyp | tail -n +3 | sed '/OOV/d' | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' > $ref_path/lex/$src.cpe.hyp.line;
    wc $ref_path/lex/$src.cpe.hyp.line;
    head -n 3 $ref_path/lex/$src.cpe.hyp.line;
    echo "=========="
    
done

```

လိုင်ပြောင်းကြည့်တဲ့အခါမှာ ဘာသွားတွေ့ရသလဲ ဆိုတော့ တချို့ word2word translation OOV ကြောင့်လို့ ယူဆတယ်၊ စာကြောင်းရေ ၁၀၀ မရှိတဲ့ line ဖိုင်တွေကို တွေ့ရတယ်။  
test data (or) reference data က အကြောင်း ၁၀၀ စီနဲ့ word-to-word translation လုပ်ထားခဲ့တာမို့ hypothesis ဖိုင်ကို line အဖြစ်ပြောင်းတဲ့အခါမှာ တကယ်က အကြောင်း ၁၀၀ စီရှိရမယ်။ သို့သော် တချို့ language pair တွေအတွက်က လိုင်း ၁၀၀ မရှိတာကို အောက်ပါအတိုင်းတွေ့ရတယ်... အကြောင်းအရင်းက convert လုပ်တဲ့ shell script မှာက OOV တွေ့ရင် တစ်လိုင်းလုံးဖြုတ်ထားတာမို့လို့...   
(line အဖြစ် ပြောင်းထားပြီးသား ဖိုင်တွေကို head -n3 နဲ့ ရိုက်မပြခင်မှာ အရင်ဆုံး wc command ကို run ထားတာမို့ converted line ဖိုင်တွေရဲ့ file size information ကို အရင်တွေ့ရမှာ ဖြစ်ပါတယ်)  

```
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk.co.hyp ... 
 100  607 3346 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk.pmi.hyp ... 
  100   607 13471 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk.pmi.hyp.line
မင့် ကာလတွေကို တွေနိုင်တဲ့သစ်တောတစ်ခုရှိရယ် ကြည် လဲ
မင့် ကြော် ကြော် နေ့ကျောင်း လဲ
ဒါ့မှာ ကိုးကား ဘာသာရေး ဟုတ်ရ ကျဒေါ်ရို့ ကြော်ငြာ တစ်စောင်လောက် လဲ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk.cpe.hyp ... 
  100   607 12976 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk.cpe.hyp.line
ခဲ့ရယ်လား မေ့ ထားတဲ့ ဖြေ ဘာဖြစ်ရိ
ခဲ့ရယ်လား ကြော် ကြော် ရယ်လား ဘာဖြစ်ရိ
ဒယ်မှာ ဘယ် နေလဲ သူလို့ဝို ကျဒေါ်ဒို့ တွေ့ နိုင်ရယ်လား ဘာဖြစ်ရိ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my.co.hyp ... 
 100  577 3235 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my.pmi.hyp ... 
  100   577 13651 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my.pmi.hyp.line
နင် ကာလတွေကို ဘယ်တော့မှသစ္စာမဖောက် ဖြေပါ ဒါ
ထမင်း ကြားရသလောက် ကြော် ကစားတာ ဒါ
စဉ်းစားမိ မို့လို့လဲ ငိုကြွေး ဟုတ်ဘူး ကြီးပွားဖြစ်ထွန်းမှု တွေ့ချင်ရင် ဖြစ်မလဲ ဒါ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my.cpe.hyp ... 
  100   577 12121 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my.cpe.hyp.line
နင် မေ့ စကားတွေကို အဖြေ နေတာလဲ
ထမင်း ကြော် ကြော် တာလား နေတာလဲ
ဖတ်ဖတ် ဘာ ပြောရင်း ရမှာလား မွန်မြတ်တဲ့ တွေ့ နိုင်သလဲ နေတာလဲ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch.co.hyp ... 
 100  598 1576 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch.co.hyp.line
i . . lo . lo .
a .
. ka nge engtik .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch.pmi.hyp ... 
 100  598 3846 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch.pmi.hyp.line
result hma-ngaih ko suh 331-4060-ah mahin nang
kensak nang
car ka inngaihzawn pawimawh nang
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch.cpe.hyp ... 
 100  598 3327 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch.cpe.hyp.line
result hma-ngaih ko engmah be tawng suh
kensak suh
chutah nain engtik pawimawh suh
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my.co.hyp ... 
 100  756 3351 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my.co.hyp.line
။ ။ ။ ။ ။ ။ ။ ။
။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my.pmi.hyp ... 
  100   756 19590 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my.pmi.hyp.line
ဒါဟာ ငါ့ကို ပြန်ရောက် ကျွန်မတို့အနေနဲ့ ကြက်သွန် မဟုတ်ပါဘူး ဒီကျောင်း ဒါပေမဲ့
စားပါ ဒါပေမဲ့
လှလိုက်တဲ့ သူ့ကို ထွက်သလဲ ခြောက်သွား မဆို ပြန်ရောက်ပြီ ပါရဲ့ ဒါပေမဲ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my.cpe.hyp ... 
  100   756 16860 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my.cpe.hyp.line
ဒါဟာ ကိုယ့်ကို ပြန်ရောက် စကား သိတာ ခဲ့ပါဘူး ဘူးလဲ ပါနဲ့
လိုက်ပါ ပါနဲ့
အဲဒီနေရာ ခဲ့ကြတယ် ဘယ်အချိန် စာသင်ချိန် ဘယ်မှာပဲ ရောက် ကြရအောင် ပါနဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc.co.hyp ... 
 121  778 2433 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc.co.hyp.line
. na gaw ai . yu ai ai .
ai ai gawk .
ai gaw ai langai ai . .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc.pmi.hyp ... 
 118  784 4400 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc.pmi.hyp.line
telepo gaalw gaw hpe mat yu mayu grai nten
laning marai single nten
shanhte gaw kabugaranga lani marai magang nten
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc.cpe.hyp ... 
 100  802 4526 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc.cpe.hyp.line
yadapon thit kyaw chying rung yu mayu chyeju hkyit
lahkawng marai marai hkyit
shanhte kyaw lakasha lani marai magang hkyit
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my.co.hyp ... 
 100  969 4032 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my.co.hyp.line
။ ။ ။ ပို့ ။ ။ ။ ။ ။ ။ ။ ။
။ ။ ။ ။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my.pmi.hyp ... 
  100   969 19647 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my.pmi.hyp.line
ယခု ထား နားရွက် မှတ်ပုံတင် အမျိုးသားပြတိုက် ကြိုးမဲ့ နားရွက် မနက်ဖြန် ပို့ ချင် တဲ့ ဟုတ်ပါတယ်
နှစ်ယောက် ဟုတ်ပါတယ် တဲ့ အမျိုးသားပြတိုက် ဟုတ်ပါတယ်
သူ့ အရာ ယူ အစားအစာ ယာဉ် ဟုတ်ပါတယ် လေ ဟုတ်ပါတယ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my.cpe.hyp ... 
  100   969 17568 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my.cpe.hyp.line
ယခု ချိန်း နားရွက် ပို့ မျိုးရိုး အသစ် နားရွက် ကြွ စို့ ချင် ကြိုက် ပါးစပ်
နှစ် သနည်း ကြိုက် အခန်း ပါးစပ်
ဦးချစ် အမည် ယူ အစားအစာ ရွက် တစ်ထည် မီမီ ပါးစပ်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky.co.hyp ... 
  74  793 3429 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky.co.hyp.line
꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯
꤯ ꤯ ꤯ ꤯ . ꤯ ꤔꤢ ꤯ ꤘꤣ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤘꤣ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ( ꤯ ꤯
꤯ ꤯ ꤯ ꤯ ꤯ ? ? ꤯ ꤯
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky.pmi.hyp ... 
   74   793 19413 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky.pmi.hyp.line
ꤙꤤꤛꤢꤩ꤭ꤗꤢ꤬ ꤓꤝꤟꤥ꤭ꤓꤛꤢ꤬ꤚꤢꤪ ꤊꤢ꤬ꤚꤟꤢꤧꤠꤟꤤ꤭ ꤁꤂꤉꤂ ꤘꤢꤍꤟꤢꤦ꤬ ꤘꤢꤍꤟꤢꤦ꤬ ꤊꤟꤢꤩꤑꤢꤩ꤬ꤋꤢꤨ꤬ ꤏꤝꤢꤩ꤬ꤒꤢ꤬ꤊꤥ꤬ ꤙꤥ꤭ꤡꤤ꤬ ꤤ꤬ꤏꤢꤪ ”
pꤊꤚꤟꤋꤞꤙꤎ ꤒꤟꤢꤧ꤬ꤚꤛꤢꤙꤢꤧ꤬ ” ꤒꤟꤢꤧ꤬ꤥ꤬ꤊꤟꤢꤨꤘꤢꤨ꤬ ꤊꤢ꤬ꤒꤢꤪ꤬ꤡꤤ꤭ ꤘꤢꤍꤟꤢꤦ꤬ ꤒꤢ꤬ꤊꤝꤥꤑꤢꤩ꤭ ꤀꤉꤅꤀꤀꤃꤃꤃꤈ ꤃꤀꤂ ꤘꤢꤍꤟꤢꤦ꤬ ꤟꤤ꤬ꤗꤢꤪ꤬ꤊꤢ꤭ ꤒꤟꤢꤧ꤬ꤚꤛꤢꤙꤢꤧ꤬ ” “ꤛꤢ꤬ꤊꤢꤨ꤭ꤊꤟꤢꤩ “ꤓꤢ꤬ꤢ꤬ꤗꤢꤩ꤭ ꤊꤢ꤬ꤒꤟꤢ꤭ꤙꤤꤒꤢꤩ꤭ ꤋꤝꤤꤗꤟꤌꤣ ꤊꤜꤛꤢ꤬ ꤎꤢꤩꤊꤢꤨꤗꤢꤩ꤭ ꤒꤟꤢꤧ꤬ꤚꤛꤢꤙꤢꤧ꤬ ” ꤎꤢꤩꤊꤢꤨꤗꤢꤩ꤭ “ꤓꤢ꤬ꤢ꤬ꤗꤢꤩ꤭ ꤘꤢꤍꤟꤢꤦ꤬ ꤅.꤄ ꤔꤣ꤬ ꤔꤛꤢꤩ꤭ꤊꤜꤢꤧ ”
ꤍꤟꤥꤋꤢꤍꤟꤥꤋꤥ꤬ ꤡꤤꤓꤥ꤭ ꤍꤟꤥꤋꤢ ꤊꤢ꤭ꤛꤢ꤭ꤚꤢꤦ꤬ꤘꤢꤦ꤭ ꤋꤥ ꤤ꤭ꤒꤢꤩ꤭ꤒꤢꤩ꤭꤮ ꤓꤢꤨ꤬ꤜꤟꤛꤢ꤬ꤚꤢꤦ꤭ ꤐꤟꤢꤑꤟꤢ ”
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky.cpe.hyp ... 
   74   793 19496 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky.cpe.hyp.line
ꤙꤤꤛꤢꤩ꤭ꤗꤢ꤬ ꤒꤟꤢꤧ꤬ꤏꤝꤤꤒꤟꤢꤧ꤬ꤏꤢꤧ꤭ ꤢꤛꤢꤩ꤭ꤗꤢ꤬ ꤕꤢ꤬ꤡꤟꤢꤧ ꤊꤚꤟꤢ ꤙꤤꤛꤢꤩ꤭ ꤗꤟꤢꤩ꤬ꤒꤢꤩ꤭ ꤛꤢꤩ꤭ꤒꤣ꤬ꤟꤢꤩ꤬ ꤒꤣ꤬ꤕꤚꤟꤢꤧ꤬ ꤊꤥ꤭ꤜꤢꤩ꤬ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭
ꤋꤥ꤭ꤗꤟꤢꤧ꤭ ꤔꤌꤣꤢꤧ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭ ꤒꤟꤢꤧ꤬ꤏꤝꤤꤟꤤ꤬ꤘꤢꤨ꤬ ꤊꤢ꤬ꤒꤢꤪ꤬ꤡꤤ꤭ ꤙꤤꤛꤢꤩ꤭ ꤙꤢꤎꤢꤊꤢ꤭ ꤖꤥ꤭ꤘꤛꤢꤗꤢ ꤃꤀꤂ ꤔꤌꤣꤢꤧ ꤟꤤ꤬ꤗꤢꤪ꤬ꤊꤢ꤭ ꤔꤌꤣꤢꤧ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭ ꤛꤢ꤬ꤊꤢꤨ꤭ꤊꤟꤢꤩ ꤏꤛꤢꤩ꤬ꤒꤢ꤬ꤡꤥ꤬ ꤜꤟꤢꤩꤥ꤬ꤊꤟꤌꤣ ꤗꤥ ꤕꤢ꤭ꤒꤥ꤬ ꤔꤟꤢꤧ꤬ꤋꤢꤨ꤬ꤊꤜꤛꤢ ꤔꤌꤣꤢꤧ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭ ꤢ꤬ꤏꤢꤦ꤭ ꤏꤛꤢꤩ꤬ꤒꤢ꤬ꤡꤥ꤬ ꤔꤌꤣꤢꤧ ꤥ꤬ꤗꤛꤢꤩ꤭ꤊꤢ꤬ꤓꤢꤪ꤬ ꤟꤢꤋꤛꤢ꤬ ꤒꤣ꤬ꤊꤜꤢꤧ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭
ꤜꤢꤩ ꤒꤢꤧ꤭ ꤍꤟꤥꤜꤟꤛꤢꤩ꤬ ꤢ꤬ꤟꤢꤩꤙꤢꤧ꤬ ꤊꤥ꤬ꤕꤢ꤬ꤔꤤ꤬ ꤤ꤬ꤒꤢꤩ꤭ ꤗꤢ꤬ꤒꤢꤩ꤭ ꤢ꤬ꤕꤜꤝꤥ꤭ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my.co.hyp ... 
  99  765 4372 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my.co.hyp.line
။ ။ ။ ။ ။ ။ ။ ။ ။
။
။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my.pmi.hyp ... 
   99   765 19570 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my.pmi.hyp.line
ခဏခဏ ခိုင်မဲ့ ကန်တော့ ခင်ဗျားဒီလိုလုပ်ရင်အထင်လွဲစရာဖြစ်သွားလိမ့်မယ်။ ခိုး တာက " ကလေးဆိုတာရောဂါကူးဖို့အလွယ်ဆုံးပဲ။ "
"
လွယ် အတိုးငွေ "
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my.cpe.hyp ... 
   99   765 18106 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my.cpe.hyp.line
ဆီချိုရောဂါ ဘဏ်စာရင်း ဒေါ်လာ မကောင်း အမြင်မရှင်း ဒိထက် အိမ် ကလေးတစ်ဝက်ခပါ။ ဟုတ်ကဲ့
ဟုတ်ကဲ့
ဆရာဝန် အတိုးရငွေ ဟုတ်ကဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo.co.hyp ... 
  99  477 2175 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo.co.hyp.line
။ ။ ။
။ ။ ။ ။ ။
။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo.pmi.hyp ... 
   99   477 13734 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo.pmi.hyp.line
ကၠောန်တ္ၚဲ စၞစဖာသဝ်တ္ၚဲဂှ် သွက်ဂွံ
ပလၚ်သ္ၚေက် ပလၚ်သ္ၚေက် ဟွံဍုဟ် ပလၚ်သ္ၚေက် သွက်ဂွံ
ကၠိုဟ်လဝ် ပလၚ်သ္ၚေက် မံၚ်သေၚ် သွက်ဂွံ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo.cpe.hyp ... 
  99  477 8670 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo.cpe.hyp.line
ကၠောန်တ္ၚဲ သၠးဟာ ညိဟာ
အထေၚ်သ္ၚေဲာ ရီုဗၚ်လဝ် ဍုဟ် လံယျဟာ ညိဟာ
ဣဇှ် ရီုဗၚ်လဝ် မုဟွံ ညိဟာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my.co.hyp ... 
  99  449 2251 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my.co.hyp.line
မင်း ။ ။
မုန်း ။ ။ ။
။ ။ မ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my.pmi.hyp ... 
  99  449 9345 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my.pmi.hyp.line
ဖန်တီး တာလား ပါနဲ့
ကြောင်က ကိုယ် တာလား ပါနဲ့
လု ။\x01ဍေံတံ နှစ်သက်ဘူး ထားဘူးလား ပါနဲ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my.cpe.hyp ... 
  99  449 9224 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my.cpe.hyp.line
ဖန်တီး တာလား ပါနဲ့
မုန်း ရမှာလား တာလား ပါနဲ့
အဲ့ဒါ သဘောကျ နှစ်သက်ဘူး ခဲ့မိဘူးလား ပါနဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk.co.hyp ... 
 100  522 4968 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk.co.hyp.line
လီၫ အဝ့ၫ လီၫ လီၫ
ဂဲၫထဲၩ့ဎွ့ၩန့ လီၫ
လဲၪ ဧၪ ဧၪ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk.pmi.hyp ... 
  100   522 13164 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk.pmi.hyp.line
ယီၩနီၪ ဖီၡီၪနီၪ အအီၪ ချီယၪနီၪ
ဆဲၫ့ဖၭဒိၪ ကဘၪထဲးလိၬၥၭ
ကစီၪ့စီၪ့တၭ ကဒိၪထၪ့ထီၫထၪ့ ကစီၪ့စီၪ့တၭ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk.cpe.hyp ... 
  100   522 10305 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk.cpe.hyp.line
ယီၩနီၪ ဖီၡီၪ အအီၪ မွဲအ့ၬဧၪ
ဂဲၫထဲၩ့ဎွ့ၩန့ ကခိၪ
မပၩၥံၪ အၪ့ယၫ အၪ့စၪ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my.co.hyp ... 
 100  453 6129 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my.co.hyp.line
ကျွန်တော့်မှာ မင်း မ မင်း ကို
ကို မှာ ကို
ငါတို့တော့ ကို
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my.pmi.hyp ... 
  100   453 11550 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my.pmi.hyp.line
တုန်းပဲ လိုက်ဖမ်းမယ် မင်းမှာ နေရတော့မယ် ချင်တယ်
မှာလဲ ကြည့်ကောင်းတယ် ရမလား
လွတ်တော့မှာပဲ ကျွန်တော်မှာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my.cpe.hyp ... 
  100   453 10032 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my.cpe.hyp.line
ကျွန်တော့်မှာ ပိုက်ဆံ မင်းမှာ အများကြီး ရတာ
မင်းတို့ မဟုတ် ခဲ့တာလား
ငါတို့တော့ ပေါ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po.co.hyp ... 
  99  498 7035 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po.co.hyp.line
နဝ်ꩻ ဝွေꩻသီး ခွေ ခွေ ခွေ ခွေ ခွေ
ယိုနဝ်ꩻ ခွေ နာꩻ တတိယ နဝ်ꩻ ဒျာႏ
အတန်ꩻ ၁၀ မိနစ် နဝ်ꩻ အတန်ꩻ ခွေ ခွေ နာꩻ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po.pmi.hyp ... 
   99   498 16758 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po.pmi.hyp.line
ခွေနဝ်ꩻတဒေါ်လာတဲ့တအဲဥ်ထဝ်းက ဝွေꩻသီးဟောင်း ကဆွိုက်လွဉ်ဒါႏဖုန်း ကော့ꩻမောင်ꩻဒျာႏ ခွေ တဲမ်ႏဗာႏလိတ်နဝ်ꩻ ထင်းနုဲင်းနဝ်ꩻ
ခင်ႏခဲဥ်း လိတ်ယိုနဝ်ꩻ ကုဲင်းထဲ့ꩻဆုဲင်ꩻငါႏ ကတောင် ကတောင် ရွစ်ဒါႏကွို့ꩻ
ကိုတဲင်ꩻ ခွဲးအဝ်ႏ ကနွုမ်နဝ်ꩻ ၇ ကိုတဲင်ꩻ တသေငါꩻတဝ်း ကလွောင်ႏဗူႏဖေႏ ခါꩻလာႏ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po.cpe.hyp ... 
   99   498 12975 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po.cpe.hyp.line
ရုပ်မွန် ဝွေꩻသီး ထာꩻ ရို မွေးစွဉ်ႏ ထင်း ယိင်းဟဝ်
ယိုနဝ်ꩻ ယို တပတ်ကို တတိယ \u200cယိုနဝ်ꩻ အွဗွော့ꩻ
အတန်ꩻ ၁၀ ဆီမိနစ် အီးသေငါꩻ အတန်ꩻ ပါꩻမုဲင်ꩻဟောင်း တွိုႏ ဗာႏဒျာႏ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my.co.hyp ... 
  94  242 3524 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my.co.hyp.line
ဆိုတာ သူတို့ မင်း ငါ ထင်
တွေ ပြီးခဲ့တဲ့ ဒါနဲ့ဆို
၁၀ သူတို့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my.pmi.hyp ... 
  94  242 6206 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my.pmi.hyp.line
လုပ်နေခဲ့လဲလို့ သူတို့ရဲ့ စကားပြောနေတာ ငါရဲ့ ခဲ့မလားလို့
ကြက်မကို အခေါက် ဒါနဲ့ဆို
ကုန်မာဆိုင် ငြိမ်သက်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my.cpe.hyp ... 
  94  242 4697 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my.cpe.hyp.line
ဆိုတာ သူတို့ စကားပြောနေတာ နိုင်ဘူး ထင်
တွေ အခေါက် ဒါနဲ့ဆို
၁၀ အတန်း
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk.co.hyp ... 
 100  604 6121 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk.co.hyp.line
သူရို့ ။ ကကောင်း လို့ ငါ ထင် ။ ။
။ ဒေ ။ တတိယ အကြိမ် ။ ။
အတန်း ၁၀ မိနစ် ။ အတန်း ကို ရောက် ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk.pmi.hyp ... 
  100   604 14146 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk.pmi.hyp.line
ဇာဖြစ်လို့ကေ ခကတ်ပါလား ကကကောင်း ကံကောင်းပါစီ ငါ ထောင်ချောက်ကို တေ။ သူက
မျက်နှာကျက် ဒေ ကဒေ ကဒေ ကလေး ဖူးသမျှထဲမာ သူက
ငြိမ်သက် ကုန်မာဆိုင် ကြက်ဥတိစွာ မာ ငြိမ်သက် ကို ကောင်းမွန်စွာ ရဖို့။ သူက
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk.cpe.hyp ... 
  100   604 10846 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk.cpe.hyp.line
ဇာဖြစ်လို့လည်းဆိုကေ သူရို့ ကကောင်း လို့ ငါ ထင် တေ။ ဇာသူ
ဒေချင့် ဒေ အပတ်မာ တတိယ ပြန်ဖတ် ယာ ဇာသူ
အတန်း ၁၀ အဖျစ်ခံရဖို့စွာက မဟုတ်ပါလား။ အတန်း လိုက်ပါ ရောက် ရဖို့ ဇာသူ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my.co.hyp ... 
 100  589 4693 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my.co.hyp.line
။ ။ ရထားကြီး ။ ။ ။ ။ ။
။ ဒါ အပတ်မှာ တတိယ ။ ။ ။
။ ။ မိနစ် ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my.pmi.hyp ... 
  100   589 13762 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my.pmi.hyp.line
သူရို့ တော်တော်လေး မြန်တဲ့ လို့ ငါ စာရေးရတာ တောင်းပန်ထားတယ် နော်
ကားပါလား အကြိမ်ပဲ တွေ့ကောင်းတွေ့ ခုန်စရာတောင် ကလဲ ပါ နော်
ငြိမ်သက် စက်တင်ဘာ ကြက်ဥတွေဟာ ဘဝ ငြိမ်သက် ကို ကြိုးစားရင်း ကန့်သတ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp ... 
  100   589 10990 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp.line
သူတို့ သိပ် ရထားကြီး လို့ ငါ ထင် ခက်ခဲတယ် တာလား
ဒါ အကြိမ်ပဲ အပတ်မှာ တတိယ ပျက်တာ ပါ တာလား
အတန်း ရုံးချိန်းက မိနစ် ရှိနေတဲ့အတွက်ကြောင့် အတန်း ခဲ့ပါဘူး ရောက် ရမယ်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw.co.hyp ... 
 108  716 2114 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw.co.hyp.line
yà nà . . .
yà . tìq tìq . .
yàngōn yà . . ngà . má .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw.pmi.hyp ... 
  99  727 5001 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw.pmi.hyp.line
yàgǿnø̀ bvnlīàngkàngshvlā ídvng gvza shaq
yàgǿnø̀ shvq ídvng bàngdāy óqà shaq
cìrongtē toshī aníla nvng bikin pí íma shaq
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw.cpe.hyp ... 
  99  727 5109 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw.cpe.hyp.line
yàmē bvnlīàngkàngshvlā bøn vdūngrv́m nàrī
yàmē ngā tìqní mg-tunshēn svpō nàrī
zingvbi íma lvngcha shíní nvm pí pàmvrà nàrī
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my.co.hyp ... 
 94  99 396 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my.co.hyp.line
။
။
။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my.pmi.hyp ... 
  94   99 1728 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my.pmi.hyp.line
ပြန်
ပြန်
ကုတ်အင်္ကျီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my.cpe.hyp ... 
 94  99 693 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my.cpe.hyp.line
၏
၏
ဒီအရာ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh.co.hyp ... 
 100  606 3120 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh.co.hyp.line
။ ၊ ။ ။ ။
။ ။ ။ ။
။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh.pmi.hyp ... 
  100   606 20913 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh.pmi.hyp.line
တင်းၼ်ႂးႄလႈ ၊ မၼ်းၶႅမ်ႉလႅပ်ႈယူႇ တင်းၼၢင်းယိင်း မိူဝ်ႈၽုၵ်ႈ
မူတ်ႉ တေလႆႈၶိုၼ်းႄမးယႃႉဢိူဝ်ႈ ဢၼ်ငၢႆႈ မိူဝ်ႈၽုၵ်ႈ
ၵဝ်ထၢင်ႇႄတႉ ပၢင်ႇလၢႆ တူၵ်းၼႂ်း တီႈၼွင် ပွတ်းၵုင်းလိၼ် မိူဝ်ႈၽုၵ်ႈ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh.cpe.hyp ... 
  100   606 13707 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh.cpe.hyp.line
ယိၼ်းၸူမ်းၶႃႈ လီယူႇ တီႈၼႆႈ ငိုၼ်း ၼႆႉပဵၼ်
ၶႃႈၶဝ်ႈ ဢၼ်ႁဝ်းလႆႈၶိၼ်းဝႆႉၼၼ်ႉ မၼ်းတေ ၼႆႉပဵၼ်
ၵဝ် ပႃလုၺ်းၼမ်ႉ တေသႂ်ႇ လုၺ်းၼမ်ႉ ယူႇၼႆႉ ၼႆႉပဵၼ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my.co.hyp ... 
 100  578 2987 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my.co.hyp.line
၊ ။ ။
။ ။ ။ ။ ။ ။
။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my.pmi.hyp ... 
  100   578 14097 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my.pmi.hyp.line
၊ ငါးရာ မေး
အဖြေ ကိုယ်တို့ ပေးရမလား တံတားတွေကို အင်း မေး
ငါက ကူးပါ ထွက်မှာ နေတာလဲ မေး
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my.cpe.hyp ... 
  100   578 11112 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my.cpe.hyp.line
ဟုတ်တယ် ငွေ မှာလဲ
ဘယ်ဟာကို ငါတို့ ရမလဲ စေနဲ့ အင်း မှာလဲ
ငါ ရေကူး ထဲမှာ နေတာလဲ မှာလဲ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp ... 
 100  588 8775 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp.line
အံၤ တၢ်ဆါဟံၣ် န့ၣ် ကသံၣ်သရၣ် လၢတၢ်ဆါဟံၣ် တၢ်မၤ မၤ န့ၣ်လီၤ
တၢ်ဝဲန့ၣ် ကွဲးကွဲး တ ကွဲးကွဲး
ဟ့ၣ်လီၤယၤ ဟ့ၣ်ခီဂာ် ဝံသးစူၤ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk.pmi.hyp ... 
  100   588 20756 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk.pmi.hyp.line
ဖဲအံၤဆူ ကဘၣ်အိၣ်ဖဲတၢ်ဆါဟံၣ် ဖဲဝ့ၢ်တကူၣ်န့ၣ် ဆဲးကသံၣ်သရၣ် ကသံၣ်သရၣ်သၢဂၤ တၢ်မၤဘၣ် ကမၤတၢ်မနုၤလဲၣ် နၢ်ဟူလၢ
ကးတံာ်တံာ် မ့ၢ်ကွဲးဝဲတၢ်န့ၣ်မ့ၢ်ဂ့ၤ လၢၤဘၣ်ဧါ မ့ၢ်ကွဲးဝဲတၢ်န့ၣ်မ့ၢ်ဂ့ၤ
လံာ်ဖိ ထိၣ်ဒံးဘိတက့ၢ် ကျဲမ့ၢ်ဖျိန့ၣ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk.cpe.hyp ... 
  100   588 13503 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk.cpe.hyp.line
အံၤ တၢ်ဆါဟံၣ် အဝဲတမ့ၢ် ကသံၣ်သရၣ် ကသံၣ်သရၣ်သၢဂၤ တၢ်မၤ မၤ န့ၣ်ကစီဒီ
တၢ်ဝဲန့ၣ် ကွဲးကွဲး ဘၣ်လဲၣ် ကွဲးကွဲး
ဟ့ၣ်လီၤယၤ ဟ့ၣ်ခီဂာ် မီၤ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp ... 
 100  525 7674 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp.line
ဆေးရုံ ဒီ ကို ဆရာဝန် ယောက် လုပ် အလုပ်
မ မ
စာအုပ်ကလေး နော်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my.pmi.hyp ... 
  100   525 13080 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my.pmi.hyp.line
ခဲ့ရလို့ပေါ့ ခဲ့ကြလဲ ဆိုတာ စိတ်ဖိစီးမှု ယောက်ရှိတယ် လုပ်နေ လုပ်ခဲ့သည်
ခက်ခဲတယ် ခဲ့ကြဘူးလား
စာအုပ်ကလေး ဟောင်တာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my.cpe.hyp ... 
 100  525 9675 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my.cpe.hyp.line
ဆေးရုံ ဒီ ဘယ်သူ ဆရာဝန် သုံး လုပ် အလုပ်
အဲဒါ ခဲ့ကြဘူးလား
စာအုပ်ကလေး နော်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk.co.hyp ... 
 100  584 3314 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk.pmi.hyp ... 
  100   584 13145 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk.pmi.hyp.line
မင်း ကာလတွေကို ရမ်း ကြည် ဖြေ
မင်း ကြော် ကြော် ကိုယ့်ဘက်ပါအောင် ဖြေ
ဒါ့မှာ ထားရိ အသီး ဟုတ်ရ ဒါလဲ ကြော်ငြာ တိုင်စီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk.cpe.hyp ... 
  100   584 11951 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk.cpe.hyp.line
ခဲ့ရယ်လား မေ့ သိပ် ဖြေ အယ့်ဒါ
ခဲ့ရယ်လား ငါး ကြော် ဇာလား အယ့်ဒါ
ဒယ်မှာ ဘာ ဘာတွေ တာလဲ ကျွန်တော်ဝို့ တွေ့ တိုင်စီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk.co.hyp ... 
 100  577 3952 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk.co.hyp.line
မင်း ။ ။ ။ ။
မင်း ။ ငါး ။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk.pmi.hyp ... 
  100   577 13373 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk.pmi.hyp.line
မင်းဇာတိ ကာလတိကို ဆွဲယူ ဖြေပါ ၊
ထမင်း ကျွန်တော်ကြားရစွာက ကြော် ကစားစွာ ၊
စဉ်းစားမိ ချင်လေး ငိုကြွေး တောင်းပန်ထား ကျွန်တော်ရို့တိုင်းပြည်ကို ဇာအချိန်မဆို ဖြစ်ဖို့လေး ၊
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk.cpe.hyp ... 
  100   577 13028 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk.cpe.hyp.line
မဟုတ်ပါလား။ မိန့် ကြိုက်ရေ အဖြေ နီစွာလေး
ထမင်း ကြော် ကြော် စွာလား နီစွာလေး
ယင်းချင့်ကို ဇာ ငိုကြွေး တောင်းပန်ထား မွန်မြတ်ရေ တွိ နိုင်လေး နီစွာလေး
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc.co.hyp ... 
100 100 200 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc.co.hyp.line
.
.
.
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc.pmi.hyp ... 
100 100 700 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc.pmi.hyp.line
chyeju
chyeju
chyeju
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc.cpe.hyp ... 
100 100 500 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc.cpe.hyp.line
nsam
nsam
nsam
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp ... 
 100  629 1873 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp.line
nø̀ ngà . . . .
nø̀ ngà . . . . .
nø̀ ngà . . . . . .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw.pmi.hyp ... 
 100  629 4085 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw.pmi.hyp.line
ídvng vpèq dvpvt būsmōdò ídvng shàm
ídvng vpèq dvpvt būsmōdò ídvng gø shàm
ídvng vpèq dvpvt būsmōdò ídvng ngā gø shàm
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw.cpe.hyp ... 
 100  629 3976 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw.cpe.hyp.line
tø̀ng ayē nī wāq lvgōlíng shàm
tø̀ng ayē nī wāq lvgōlíng mí shàm
tø̀ng ayē nī wāq lvgōlíng ngā mí shàm
==========
```

## Keep OOV and Make Conversion Again

script ထဲကနေ "sed '/OOV/d' " ဆိုတဲ့ OOV တွေဖြစ်နေတဲ့ line ကို delete လုပ်တဲ့ code ကို ဖယ်လိုက်တာပါပဲ...  
အဲဒီ တစ်ခုပဲ update လုပ်ခဲ့ရင် တစ်ခုရှိတာက format converted output မှာက 101 လိုင်းဖြစ်နေလိမ့်မယ်။ ဘာကြောင့်လဲ ဆိုတော့ OOV % ကို ပြတဲ့ လိုင်းပါနေလို့။   
အောက်ပါအတိုင်း...  

```
နာꩻအတာႏ တမုဲင်ꩻ မာꩻ နေးမုဲင်ꩻဟောင်း
ယိုခါꩻ မွေးစွဉ်ႏ မွိုးဖြား အီးအုံလင် OOV လိုပေႏဖုံႏ တေ့ꩻတေ့ꩻ ဆရာႏမူႏဖုံႏ
ဝွေꩻမူႏ နဝ်ꩻနဝ်ꩻ ပါꩻမုဲင်ꩻဟောင်း သဘော်ꩻတူႏ နေဟောင်း
အခေႏနေႏ ကျူႏ လုံးဝ OOV ထွာ လဲဉ်း
OOV percentage: 12.65%
```

အဲဒါကြောင့် နောက်ဆုံး ဖိုင်ကို မသိမ်းခင်မှာ head -n -1 ဆိုတာကို piping လုပ်ပေးဖို့ လိုအပ်ပါတယ်။ ပြင်ဆင်ပြီးသား code က အောက်ပါပုံစံမျိုးပါ...  

```bash
cut -d "," -f1 $ref_path/lex/co/$trg.co.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/co/$trg.co.hyp.line;
```

Updated လုပ်ထားတဲ့ shell script တစ်ခုလုံးက အောက်ပါအတိုင်းပါ ...  

```bash
#!/bin/bash

# converting hypothesis column files to line format
# for this script I keep OOV
# (OOV ကို keep လုပ်ချင်းအားဖြင့် reference နဲ့ line အရေအတွက် တူအောင် ညှိလို့ ရမလား ဆိုတာကို သိချင်လို့ update လုပ်ခဲ့)
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 1 Dec 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; 
    trg=${fd#*-}; 
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; #echo "ref_path: $ref_path";

    # run ရတဲ့ ပုံစံက အောက်ပါအတိုင်း
    #python -m pickle  <lexicon_path> > <converted-filename>
    
    # for source-to-target lexicon
    echo "converting for $ref_path/lex/co/$trg.co.hyp ... ";
    cut -d "," -f1 $ref_path/lex/co/$trg.co.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/co/$trg.co.hyp.line;
    wc $ref_path/lex/co/$trg.co.hyp.line; 
    head -n 3 $ref_path/lex/co/$trg.co.hyp.line; 
    echo "converting for $ref_path/lex/pmi/$trg.pmi.hyp ... ";   
    cut -d "," -f1 $ref_path/lex/pmi/$trg.pmi.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/pmi/$trg.pmi.hyp.line;
    wc $ref_path/lex/pmi/$trg.pmi.hyp.line;
    head -n 3 $ref_path/lex/pmi/$trg.pmi.hyp.line;
    echo "converting for $ref_path/lex/$trg.cpe.hyp ... ";
    cut -d "," -f1 $ref_path/lex/$trg.cpe.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/$trg.cpe.hyp.line;
    wc $ref_path/lex/$trg.cpe.hyp.line;
    head -n 3 $ref_path/lex/$trg.cpe.hyp.line;

    
    # for target-to-source lexicon
    echo "converting for $ref_path/lex/co/$src.co.hyp ... ";
    cut -d "," -f1 $ref_path/lex/co/$src.co.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/co/$src.co.hyp.line;
    wc $ref_path/lex/co/$src.co.hyp.line;
    head -n 3 $ref_path/lex/co/$src.co.hyp.line; 
    echo "converting for $ref_path/lex/pmi/$src.pmi.hyp ... ";   
    cut -d "," -f1 $ref_path/lex/pmi/$src.pmi.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/pmi/$src.pmi.hyp.line;
    wc $ref_path/lex/pmi/$src.pmi.hyp.line;
    head -n 3 $ref_path/lex/pmi/$src.pmi.hyp.line;
    echo "converting for $ref_path/lex/$src.cpe.hyp ... ";
    cut -d "," -f1 $ref_path/lex/$src.cpe.hyp | tail -n +3 | sed "s/^\\['\|'$//g" | awk  'BEGIN { RS = ""; OFS = " "} {$1 = $1; print }' | head -n -1 > $ref_path/lex/$src.cpe.hyp.line;
    wc $ref_path/lex/$src.cpe.hyp.line;
    head -n 3 $ref_path/lex/$src.cpe.hyp.line;
    echo "=========="
    
done

```

အထက်ပါ script ကို run ခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time ./column-to-nbest-word-sentence-with-OOV.sh | tee ./column-to-line-with-OOV.log
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk.co.hyp ... 
 100  649 3514 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ OOV ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk.pmi.hyp ... 
  100   649 13639 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk.pmi.hyp.line
မင့် ကာလတွေကို တွေနိုင်တဲ့သစ်တောတစ်ခုရှိရယ် ကြည် လဲ
မင့် ကြော် ကြော် နေ့ကျောင်း လဲ
ဒါ့မှာ ကိုးကား OOV ဘာသာရေး ဟုတ်ရ ကျဒေါ်ရို့ ကြော်ငြာ တစ်စောင်လောက် လဲ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk.cpe.hyp ... 
  100   649 13144 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk.cpe.hyp.line
ခဲ့ရယ်လား မေ့ ထားတဲ့ ဖြေ ဘာဖြစ်ရိ
ခဲ့ရယ်လား ကြော် ကြော် ရယ်လား ဘာဖြစ်ရိ
ဒယ်မှာ ဘယ် OOV နေလဲ သူလို့ဝို ကျဒေါ်ဒို့ တွေ့ နိုင်ရယ်လား ဘာဖြစ်ရိ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my.co.hyp ... 
 100  633 3459 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ OOV ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my.pmi.hyp ... 
  100   633 13875 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my.pmi.hyp.line
နင် ကာလတွေကို ဘယ်တော့မှသစ္စာမဖောက် ဖြေပါ ဒါ
ထမင်း ကြားရသလောက် ကြော် ကစားတာ ဒါ
စဉ်းစားမိ မို့လို့လဲ OOV ငိုကြွေး ဟုတ်ဘူး ကြီးပွားဖြစ်ထွန်းမှု တွေ့ချင်ရင် ဖြစ်မလဲ ဒါ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my.cpe.hyp ... 
  100   633 12345 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my.cpe.hyp.line
နင် မေ့ စကားတွေကို အဖြေ နေတာလဲ
ထမင်း ကြော် ကြော် တာလား နေတာလဲ
ဖတ်ဖတ် ဘာ OOV ပြောရင်း ရမှာလား မွန်မြတ်တဲ့ တွေ့ နိုင်သလဲ နေတာလဲ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch.co.hyp ... 
 100  643 1756 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch.co.hyp.line
i . . lo . lo .
a .
. ka nge engtik .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch.pmi.hyp ... 
 100  643 4026 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch.pmi.hyp.line
result hma-ngaih ko suh 331-4060-ah mahin nang
kensak nang
car ka inngaihzawn pawimawh nang
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch.cpe.hyp ... 
 100  643 3507 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch.cpe.hyp.line
result hma-ngaih ko engmah be tawng suh
kensak suh
chutah nain engtik pawimawh suh
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my.co.hyp ... 
 100  871 3811 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my.co.hyp.line
OOV ။ ။ ။ ။ ။ ။ ။ ။
OOV ။ ။
OOV ။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my.pmi.hyp ... 
  100   871 20050 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my.pmi.hyp.line
OOV ဒါဟာ ငါ့ကို ပြန်ရောက် ကျွန်မတို့အနေနဲ့ ကြက်သွန် မဟုတ်ပါဘူး ဒီကျောင်း ဒါပေမဲ့
OOV စားပါ ဒါပေမဲ့
OOV လှလိုက်တဲ့ သူ့ကို ထွက်သလဲ ခြောက်သွား မဆို ပြန်ရောက်ပြီ ပါရဲ့ ဒါပေမဲ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my.cpe.hyp ... 
  100   871 17320 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my.cpe.hyp.line
OOV ဒါဟာ ကိုယ့်ကို ပြန်ရောက် စကား သိတာ ခဲ့ပါဘူး ဘူးလဲ ပါနဲ့
OOV လိုက်ပါ ပါနဲ့
OOV အဲဒီနေရာ ခဲ့ကြတယ် ဘယ်အချိန် စာသင်ချိန် ဘယ်မှာပဲ ရောက် ကြရအောင် ပါနဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc.co.hyp ... 
 121  795 2501 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc.co.hyp.line
. na gaw OOV ai . yu ai ai .
ai ai gawk .
ai gaw ai langai ai . .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc.pmi.hyp ... 
 118  801 4468 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc.pmi.hyp.line
telepo gaalw gaw OOV hpe mat yu mayu grai nten
laning marai single nten
shanhte gaw kabugaranga lani marai magang nten
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc.cpe.hyp ... 
 100  819 4594 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc.cpe.hyp.line
yadapon thit kyaw OOV chying rung yu mayu chyeju hkyit
lahkawng marai marai hkyit
shanhte kyaw lakasha lani marai magang hkyit
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my.co.hyp ... 
 100  972 4044 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my.co.hyp.line
။ ။ ။ ပို့ ။ ။ ။ OOV ။ ။ ။ ။ ။
။ ။ ။ ။ ။
။ ။ ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my.pmi.hyp ... 
  100   972 19659 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my.pmi.hyp.line
ယခု ထား နားရွက် မှတ်ပုံတင် အမျိုးသားပြတိုက် ကြိုးမဲ့ နားရွက် OOV မနက်ဖြန် ပို့ ချင် တဲ့ ဟုတ်ပါတယ်
နှစ်ယောက် ဟုတ်ပါတယ် တဲ့ အမျိုးသားပြတိုက် ဟုတ်ပါတယ်
သူ့ အရာ ယူ အစားအစာ ယာဉ် ဟုတ်ပါတယ် လေ ဟုတ်ပါတယ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my.cpe.hyp ... 
  100   972 17580 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my.cpe.hyp.line
ယခု ချိန်း နားရွက် ပို့ မျိုးရိုး အသစ် နားရွက် OOV ကြွ စို့ ချင် ကြိုက် ပါးစပ်
နှစ် သနည်း ကြိုက် အခန်း ပါးစပ်
ဦးချစ် အမည် ယူ အစားအစာ ရွက် တစ်ထည် မီမီ ပါးစပ်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky.co.hyp ... 
 100  872 3745 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky.co.hyp.line
꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯ ꤯
OOV
OOV
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky.pmi.hyp ... 
  100   872 19729 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky.pmi.hyp.line
ꤙꤤꤛꤢꤩ꤭ꤗꤢ꤬ ꤓꤝꤟꤥ꤭ꤓꤛꤢ꤬ꤚꤢꤪ ꤊꤢ꤬ꤚꤟꤢꤧꤠꤟꤤ꤭ ꤁꤂꤉꤂ ꤘꤢꤍꤟꤢꤦ꤬ ꤘꤢꤍꤟꤢꤦ꤬ ꤊꤟꤢꤩꤑꤢꤩ꤬ꤋꤢꤨ꤬ ꤏꤝꤢꤩ꤬ꤒꤢ꤬ꤊꤥ꤬ ꤙꤥ꤭ꤡꤤ꤬ ꤤ꤬ꤏꤢꤪ ”
OOV
OOV
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky.cpe.hyp ... 
  100   872 19812 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky.cpe.hyp.line
ꤙꤤꤛꤢꤩ꤭ꤗꤢ꤬ ꤒꤟꤢꤧ꤬ꤏꤝꤤꤒꤟꤢꤧ꤬ꤏꤢꤧ꤭ ꤢꤛꤢꤩ꤭ꤗꤢ꤬ ꤕꤢ꤬ꤡꤟꤢꤧ ꤊꤚꤟꤢ ꤙꤤꤛꤢꤩ꤭ ꤗꤟꤢꤩ꤬ꤒꤢꤩ꤭ ꤛꤢꤩ꤭ꤒꤣ꤬ꤟꤢꤩ꤬ ꤒꤣ꤬ꤕꤚꤟꤢꤧ꤬ ꤊꤥ꤭ꤜꤢꤩ꤬ ꤋꤛꤢꤞꤢꤧꤘꤥ꤭
OOV
OOV
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my.co.hyp ... 
 100  859 4748 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my.co.hyp.line
။ ။ ။ ။ ။ ။ ။ ။ ။
OOV ။
။ OOV ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my.pmi.hyp ... 
  100   859 19946 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my.pmi.hyp.line
ခဏခဏ ခိုင်မဲ့ ကန်တော့ ခင်ဗျားဒီလိုလုပ်ရင်အထင်လွဲစရာဖြစ်သွားလိမ့်မယ်။ ခိုး တာက " ကလေးဆိုတာရောဂါကူးဖို့အလွယ်ဆုံးပဲ။ "
OOV "
လွယ် OOV အတိုးငွေ "
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my.cpe.hyp ... 
  100   859 18482 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my.cpe.hyp.line
ဆီချိုရောဂါ ဘဏ်စာရင်း ဒေါ်လာ မကောင်း အမြင်မရှင်း ဒိထက် အိမ် ကလေးတစ်ဝက်ခပါ။ ဟုတ်ကဲ့
OOV ဟုတ်ကဲ့
ဆရာဝန် OOV အတိုးရငွေ ဟုတ်ကဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo.co.hyp ... 
  99  498 2259 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo.co.hyp.line
OOV ။ ။ ။
။ ။ ။ ။ ။
။ ။ OOV ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo.pmi.hyp ... 
   99   498 13818 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo.pmi.hyp.line
OOV ကၠောန်တ္ၚဲ စၞစဖာသဝ်တ္ၚဲဂှ် သွက်ဂွံ
ပလၚ်သ္ၚေက် ပလၚ်သ္ၚေက် ဟွံဍုဟ် ပလၚ်သ္ၚေက် သွက်ဂွံ
ကၠိုဟ်လဝ် ပလၚ်သ္ၚေက် OOV မံၚ်သေၚ် သွက်ဂွံ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo.cpe.hyp ... 
  99  498 8754 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo.cpe.hyp.line
OOV ကၠောန်တ္ၚဲ သၠးဟာ ညိဟာ
အထေၚ်သ္ၚေဲာ ရီုဗၚ်လဝ် ဍုဟ် လံယျဟာ ညိဟာ
ဣဇှ် ရီုဗၚ်လဝ် OOV မုဟွံ ညိဟာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my.co.hyp ... 
  99  488 2407 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my.co.hyp.line
မင်း OOV ။ ။
မုန်း ။ ။ ။
။ ။ မ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my.pmi.hyp ... 
  99  488 9501 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my.pmi.hyp.line
ဖန်တီး OOV တာလား ပါနဲ့
ကြောင်က ကိုယ် တာလား ပါနဲ့
လု ။\x01ဍေံတံ နှစ်သက်ဘူး ထားဘူးလား ပါနဲ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my.cpe.hyp ... 
  99  488 9380 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my.cpe.hyp.line
ဖန်တီး OOV တာလား ပါနဲ့
မုန်း ရမှာလား တာလား ပါနဲ့
အဲ့ဒါ သဘောကျ နှစ်သက်ဘူး ခဲ့မိဘူးလား ပါနဲ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk.co.hyp ... 
 100  580 5200 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk.co.hyp.line
လီၫ OOV အဝ့ၫ လီၫ လီၫ
ဂဲၫထဲၩ့ဎွ့ၩန့ OOV လီၫ OOV
လဲၪ ဧၪ ဧၪ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk.pmi.hyp ... 
  100   580 13396 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk.pmi.hyp.line
ယီၩနီၪ OOV ဖီၡီၪနီၪ အအီၪ ချီယၪနီၪ
ဆဲၫ့ဖၭဒိၪ OOV ကဘၪထဲးလိၬၥၭ OOV
ကစီၪ့စီၪ့တၭ ကဒိၪထၪ့ထီၫထၪ့ ကစီၪ့စီၪ့တၭ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk.cpe.hyp ... 
  100   580 10537 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk.cpe.hyp.line
ယီၩနီၪ OOV ဖီၡီၪ အအီၪ မွဲအ့ၬဧၪ
ဂဲၫထဲၩ့ဎွ့ၩန့ OOV ကခိၪ OOV
မပၩၥံၪ အၪ့ယၫ အၪ့စၪ့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my.co.hyp ... 
 100  562 6565 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my.co.hyp.line
ကျွန်တော့်မှာ မင်း မ မင်း ကို
ကို OOV OOV မှာ ကို
OOV OOV ငါတို့တော့ ကို
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my.pmi.hyp ... 
  100   562 11986 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my.pmi.hyp.line
တုန်းပဲ လိုက်ဖမ်းမယ် မင်းမှာ နေရတော့မယ် ချင်တယ်
မှာလဲ OOV OOV ကြည့်ကောင်းတယ် ရမလား
OOV OOV လွတ်တော့မှာပဲ ကျွန်တော်မှာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my.cpe.hyp ... 
  100   562 10468 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my.cpe.hyp.line
ကျွန်တော့်မှာ ပိုက်ဆံ မင်းမှာ အများကြီး ရတာ
မင်းတို့ OOV OOV မဟုတ် ခဲ့တာလား
OOV OOV ငါတို့တော့ ပေါ့
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po.co.hyp ... 
 100  561 7287 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po.co.hyp.line
နဝ်ꩻ ဝွေꩻသီး OOV ခွေ OOV ခွေ ခွေ ခွေ ခွေ
ယိုနဝ်ꩻ ခွေ နာꩻ တတိယ နဝ်ꩻ ဒျာႏ
အတန်ꩻ OOV ၁၀ မိနစ် နဝ်ꩻ အတန်ꩻ ခွေ ခွေ နာꩻ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po.pmi.hyp ... 
  100   561 17010 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po.pmi.hyp.line
ခွေနဝ်ꩻတဒေါ်လာတဲ့တအဲဥ်ထဝ်းက ဝွေꩻသီးဟောင်း OOV ကဆွိုက်လွဉ်ဒါႏဖုန်း OOV ကော့ꩻမောင်ꩻဒျာႏ ခွေ တဲမ်ႏဗာႏလိတ်နဝ်ꩻ ထင်းနုဲင်းနဝ်ꩻ
ခင်ႏခဲဥ်း လိတ်ယိုနဝ်ꩻ ကုဲင်းထဲ့ꩻဆုဲင်ꩻငါႏ ကတောင် ကတောင် ရွစ်ဒါႏကွို့ꩻ
ကိုတဲင်ꩻ OOV ခွဲးအဝ်ႏ ကနွုမ်နဝ်ꩻ ၇ ကိုတဲင်ꩻ တသေငါꩻတဝ်း ကလွောင်ႏဗူႏဖေႏ ခါꩻလာႏ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po.cpe.hyp ... 
  100   561 13227 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po.cpe.hyp.line
ရုပ်မွန် ဝွေꩻသီး OOV ထာꩻ OOV ရို မွေးစွဉ်ႏ ထင်း ယိင်းဟဝ်
ယိုနဝ်ꩻ ယို တပတ်ကို တတိယ \u200cယိုနဝ်ꩻ အွဗွော့ꩻ
အတန်ꩻ OOV ၁၀ ဆီမိနစ် အီးသေငါꩻ အတန်ꩻ ပါꩻမုဲင်ꩻဟောင်း တွိုႏ ဗာႏဒျာႏ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my.co.hyp ... 
 100  391 4120 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my.co.hyp.line
OOV ဆိုတာ သူတို့ မင်း OOV ငါ ထင်
တွေ ပြီးခဲ့တဲ့ ဒါနဲ့ဆို
OOV ၁၀ OOV OOV သူတို့
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my.pmi.hyp ... 
 100  391 6802 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my.pmi.hyp.line
OOV လုပ်နေခဲ့လဲလို့ သူတို့ရဲ့ စကားပြောနေတာ OOV ငါရဲ့ ခဲ့မလားလို့
ကြက်မကို အခေါက် ဒါနဲ့ဆို
OOV ကုန်မာဆိုင် OOV OOV ငြိမ်သက်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my.cpe.hyp ... 
 100  391 5293 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my.cpe.hyp.line
OOV ဆိုတာ သူတို့ စကားပြောနေတာ OOV နိုင်ဘူး ထင်
တွေ အခေါက် ဒါနဲ့ဆို
OOV ၁၀ OOV OOV အတန်း
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk.co.hyp ... 
 100  666 6369 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk.co.hyp.line
သူရို့ ။ OOV ကကောင်း OOV လို့ ငါ ထင် ။ ။
။ ဒေ ။ တတိယ အကြိမ် ။ ။
အတန်း OOV ၁၀ မိနစ် ။ အတန်း ကို ရောက် ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk.pmi.hyp ... 
  100   666 14394 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk.pmi.hyp.line
ဇာဖြစ်လို့ကေ ခကတ်ပါလား OOV ကကကောင်း OOV ကံကောင်းပါစီ ငါ ထောင်ချောက်ကို တေ။ သူက
မျက်နှာကျက် ဒေ ကဒေ ကဒေ ကလေး ဖူးသမျှထဲမာ သူက
ငြိမ်သက် OOV ကုန်မာဆိုင် ကြက်ဥတိစွာ မာ ငြိမ်သက် ကို ကောင်းမွန်စွာ ရဖို့။ သူက
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk.cpe.hyp ... 
  100   666 11094 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk.cpe.hyp.line
ဇာဖြစ်လို့လည်းဆိုကေ သူရို့ OOV ကကောင်း OOV လို့ ငါ ထင် တေ။ ဇာသူ
ဒေချင့် ဒေ အပတ်မာ တတိယ ပြန်ဖတ် ယာ ဇာသူ
အတန်း OOV ၁၀ အဖျစ်ခံရဖို့စွာက မဟုတ်ပါလား။ အတန်း လိုက်ပါ ရောက် ရဖို့ ဇာသူ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my.co.hyp ... 
 100  660 4977 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my.co.hyp.line
OOV ။ OOV ။ ရထားကြီး ။ ။ ။ ။ ။
။ ဒါ အပတ်မှာ တတိယ ။ ။ ။
။ OOV ။ မိနစ် ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my.pmi.hyp ... 
  100   660 14046 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my.pmi.hyp.line
OOV သူရို့ OOV တော်တော်လေး မြန်တဲ့ လို့ ငါ စာရေးရတာ တောင်းပန်ထားတယ် နော်
ကားပါလား အကြိမ်ပဲ တွေ့ကောင်းတွေ့ ခုန်စရာတောင် ကလဲ ပါ နော်
ငြိမ်သက် OOV စက်တင်ဘာ ကြက်ဥတွေဟာ ဘဝ ငြိမ်သက် ကို ကြိုးစားရင်း ကန့်သတ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp ... 
  100   660 11274 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp.line
OOV သူတို့ OOV သိပ် ရထားကြီး လို့ ငါ ထင် ခက်ခဲတယ် တာလား
ဒါ အကြိမ်ပဲ အပတ်မှာ တတိယ ပျက်တာ ပါ တာလား
အတန်း OOV ရုံးချိန်းက မိနစ် ရှိနေတဲ့အတွက်ကြောင့် အတန်း ခဲ့ပါဘူး ရောက် ရမယ်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw.co.hyp ... 
 109  743 2222 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw.co.hyp.line
yà nà OOV . . .
yà . tìq tìq . .
yàngōn yà . . ngà . má .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw.pmi.hyp ... 
 100  754 5109 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw.pmi.hyp.line
yàgǿnø̀ bvnlīàngkàngshvlā OOV ídvng gvza shaq
yàgǿnø̀ shvq ídvng bàngdāy óqà shaq
cìrongtē toshī aníla nvng bikin pí íma shaq
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw.cpe.hyp ... 
 100  754 5217 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw.cpe.hyp.line
yàmē bvnlīàngkàngshvlā OOV bøn vdūngrv́m nàrī
yàmē ngā tìqní mg-tunshēn svpō nàrī
zingvbi íma lvngcha shíní nvm pí pàmvrà nàrī
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my.co.hyp ... 
 100  744 2976 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my.co.hyp.line
OOV OOV OOV OOV ။
OOV OOV OOV OOV OOV OOV ။
OOV OOV OOV OOV OOV OOV OOV OOV ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my.pmi.hyp ... 
 100  744 4308 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my.pmi.hyp.line
OOV OOV OOV OOV ပြန်
OOV OOV OOV OOV OOV OOV ပြန်
OOV OOV OOV OOV OOV OOV OOV OOV ကုတ်အင်္ကျီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my.cpe.hyp ... 
 100  744 3273 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my.cpe.hyp.line
OOV OOV OOV OOV ၏
OOV OOV OOV OOV OOV OOV ၏
OOV OOV OOV OOV OOV OOV OOV OOV ဒီအရာ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh.co.hyp ... 
 100  649 3292 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh.co.hyp.line
။ ၊ ။ ။ ။
။ ။ OOV ။ ။
။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh.pmi.hyp ... 
  100   649 21085 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh.pmi.hyp.line
တင်းၼ်ႂးႄလႈ ၊ မၼ်းၶႅမ်ႉလႅပ်ႈယူႇ တင်းၼၢင်းယိင်း မိူဝ်ႈၽုၵ်ႈ
မူတ်ႉ တေလႆႈၶိုၼ်းႄမးယႃႉဢိူဝ်ႈ OOV ဢၼ်ငၢႆႈ မိူဝ်ႈၽုၵ်ႈ
ၵဝ်ထၢင်ႇႄတႉ ပၢင်ႇလၢႆ တူၵ်းၼႂ်း တီႈၼွင် ပွတ်းၵုင်းလိၼ် မိူဝ်ႈၽုၵ်ႈ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh.cpe.hyp ... 
  100   649 13879 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh.cpe.hyp.line
ယိၼ်းၸူမ်းၶႃႈ လီယူႇ တီႈၼႆႈ ငိုၼ်း ၼႆႉပဵၼ်
ၶႃႈၶဝ်ႈ ဢၼ်ႁဝ်းလႆႈၶိၼ်းဝႆႉၼၼ်ႉ OOV မၼ်းတေ ၼႆႉပဵၼ်
ၵဝ် ပႃလုၺ်းၼမ်ႉ တေသႂ်ႇ လုၺ်းၼမ်ႉ ယူႇၼႆႉ ၼႆႉပဵၼ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my.co.hyp ... 
 100  643 3247 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my.co.hyp.line
OOV ၊ OOV ။ ။
။ ။ OOV ။ ။ ။ ။
။ ။ ။ OOV ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my.pmi.hyp ... 
  100   643 14357 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my.pmi.hyp.line
OOV ၊ OOV ငါးရာ မေး
အဖြေ ကိုယ်တို့ OOV ပေးရမလား တံတားတွေကို အင်း မေး
ငါက ကူးပါ ထွက်မှာ OOV နေတာလဲ မေး
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my.cpe.hyp ... 
  100   643 11372 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my.cpe.hyp.line
OOV ဟုတ်တယ် OOV ငွေ မှာလဲ
ဘယ်ဟာကို ငါတို့ OOV ရမလဲ စေနဲ့ အင်း မှာလဲ
ငါ ရေကူး ထဲမှာ OOV နေတာလဲ မှာလဲ
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp ... 
 100  588 8775 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp.line
အံၤ တၢ်ဆါဟံၣ် န့ၣ် ကသံၣ်သရၣ် လၢတၢ်ဆါဟံၣ် တၢ်မၤ မၤ န့ၣ်လီၤ
တၢ်ဝဲန့ၣ် ကွဲးကွဲး တ ကွဲးကွဲး
ဟ့ၣ်လီၤယၤ ဟ့ၣ်ခီဂာ် ဝံသးစူၤ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk.pmi.hyp ... 
  100   588 20756 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk.pmi.hyp.line
ဖဲအံၤဆူ ကဘၣ်အိၣ်ဖဲတၢ်ဆါဟံၣ် ဖဲဝ့ၢ်တကူၣ်န့ၣ် ဆဲးကသံၣ်သရၣ် ကသံၣ်သရၣ်သၢဂၤ တၢ်မၤဘၣ် ကမၤတၢ်မနုၤလဲၣ် နၢ်ဟူလၢ
ကးတံာ်တံာ် မ့ၢ်ကွဲးဝဲတၢ်န့ၣ်မ့ၢ်ဂ့ၤ လၢၤဘၣ်ဧါ မ့ၢ်ကွဲးဝဲတၢ်န့ၣ်မ့ၢ်ဂ့ၤ
လံာ်ဖိ ထိၣ်ဒံးဘိတက့ၢ် ကျဲမ့ၢ်ဖျိန့ၣ်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk.cpe.hyp ... 
  100   588 13503 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk.cpe.hyp.line
အံၤ တၢ်ဆါဟံၣ် အဝဲတမ့ၢ် ကသံၣ်သရၣ် ကသံၣ်သရၣ်သၢဂၤ တၢ်မၤ မၤ န့ၣ်ကစီဒီ
တၢ်ဝဲန့ၣ် ကွဲးကွဲး ဘၣ်လဲၣ် ကွဲးကွဲး
ဟ့ၣ်လီၤယၤ ဟ့ၣ်ခီဂာ် မီၤ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp ... 
 100  575 7874 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp.line
ဆေးရုံ ဒီ ကို ဆရာဝန် ယောက် လုပ် အလုပ်
မ OOV မ OOV
OOV စာအုပ်ကလေး နော်
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my.pmi.hyp ... 
  100   575 13280 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my.pmi.hyp.line
ခဲ့ရလို့ပေါ့ ခဲ့ကြလဲ ဆိုတာ စိတ်ဖိစီးမှု ယောက်ရှိတယ် လုပ်နေ လုပ်ခဲ့သည်
ခက်ခဲတယ် OOV ခဲ့ကြဘူးလား OOV
OOV စာအုပ်ကလေး ဟောင်တာ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my.cpe.hyp ... 
 100  575 9875 /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my.cpe.hyp.line
ဆေးရုံ ဒီ ဘယ်သူ ဆရာဝန် သုံး လုပ် အလုပ်
အဲဒါ OOV ခဲ့ကြဘူးလား OOV
OOV စာအုပ်ကလေး နော်
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk.co.hyp ... 
 100  635 3518 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk.co.hyp.line
။ ။ ။ ။ ။
။ ။ ငါး ။ ။
။ ။ OOV ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk.pmi.hyp ... 
  100   635 13349 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk.pmi.hyp.line
မင်း ကာလတွေကို ရမ်း ကြည် ဖြေ
မင်း ကြော် ကြော် ကိုယ့်ဘက်ပါအောင် ဖြေ
ဒါ့မှာ ထားရိ OOV အသီး ဟုတ်ရ ဒါလဲ ကြော်ငြာ တိုင်စီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk.cpe.hyp ... 
  100   635 12155 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk.cpe.hyp.line
ခဲ့ရယ်လား မေ့ သိပ် ဖြေ အယ့်ဒါ
ခဲ့ရယ်လား ငါး ကြော် ဇာလား အယ့်ဒါ
ဒယ်မှာ ဘာ OOV ဘာတွေ တာလဲ ကျွန်တော်ဝို့ တွေ့ တိုင်စီ
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk.co.hyp ... 
 100  633 4176 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk.co.hyp.line
မင်း ။ ။ ။ ။
မင်း ။ ငါး ။ ။
။ ။ OOV ။ ။ ။ ။ ။ ။
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk.pmi.hyp ... 
  100   633 13597 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk.pmi.hyp.line
မင်းဇာတိ ကာလတိကို ဆွဲယူ ဖြေပါ ၊
ထမင်း ကျွန်တော်ကြားရစွာက ကြော် ကစားစွာ ၊
စဉ်းစားမိ ချင်လေး OOV ငိုကြွေး တောင်းပန်ထား ကျွန်တော်ရို့တိုင်းပြည်ကို ဇာအချိန်မဆို ဖြစ်ဖို့လေး ၊
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk.cpe.hyp ... 
  100   633 13252 /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk.cpe.hyp.line
မဟုတ်ပါလား။ မိန့် ကြိုက်ရေ အဖြေ နီစွာလေး
ထမင်း ကြော် ကြော် စွာလား နီစွာလေး
ယင်းချင့်ကို ဇာ OOV ငိုကြွေး တောင်းပန်ထား မွန်မြတ်ရေ တွိ နိုင်လေး နီစွာလေး
==========
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc.co.hyp ... 
 100  728 2712 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc.co.hyp.line
OOV OOV OOV OOV OOV OOV OOV .
OOV OOV OOV OOV OOV OOV OOV .
OOV OOV OOV OOV OOV OOV OOV .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc.pmi.hyp ... 
 100  728 3212 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc.pmi.hyp.line
OOV OOV OOV OOV OOV OOV OOV chyeju
OOV OOV OOV OOV OOV OOV OOV chyeju
OOV OOV OOV OOV OOV OOV OOV chyeju
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc.cpe.hyp ... 
 100  728 3012 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc.cpe.hyp.line
OOV OOV OOV OOV OOV OOV OOV nsam
OOV OOV OOV OOV OOV OOV OOV nsam
OOV OOV OOV OOV OOV OOV OOV nsam
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp ... 
 100  729 2273 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp.line
OOV nø̀ ngà . . . .
OOV nø̀ ngà . . . . .
OOV nø̀ ngà . . . . . .
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw.pmi.hyp ... 
 100  729 4485 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw.pmi.hyp.line
OOV ídvng vpèq dvpvt būsmōdò ídvng shàm
OOV ídvng vpèq dvpvt būsmōdò ídvng gø shàm
OOV ídvng vpèq dvpvt būsmōdò ídvng ngā gø shàm
converting for /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw.cpe.hyp ... 
 100  729 4376 /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw.cpe.hyp.line
OOV tø̀ng ayē nī wāq lvgōlíng shàm
OOV tø̀ng ayē nī wāq lvgōlíng mí shàm
OOV tø̀ng ayē nī wāq lvgōlíng ngā mí shàm
==========
```

## Evaluation on Word-to-Word Translation as Sentence Level

လက်ရှိ experiment က word-to-word lexicon ဆောက်တာ တနည်းအားဖြင့် word-to-word translation ဆိုပေမဲ့ sentence level evaluation လည်း လုပ်ကြည့်ချင်လို့ BLEU score တွက်ကြည့်ဖို့ အောက်ပါအတိုင်း shell script ကို ရေးခဲ့တယ်။  

```bash
#!/bin/bash

# Evaluation with BLEU Metric
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 1 Dec 2021

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do

    src=${fd%%-*}; 
    trg=${fd#*-}; 
    ref_path=/media/ye/project2/exp/word2word-tran/word2word/my-x/$fd/w2w; #echo "ref_path: $ref_path";

    # BLEU score တွက်ဖို့အတွက် perl script ကို run ရတဲ့ ပုံစံက အောက်ပါအတိုင်း
    # usage: multi-bleu.pl [-lc] reference < hypothesis
    # -lc ဆိုတာက lower-case အနေနဲ့ တွက်တဲ့ option မို့လို့ ဗမာစာနဲ့ တိုင်းရင်းသား ဘာသာစကားတွေအတွက်က မဆိုင်လို့ မသုံးခဲ့ဘူး
    
    # for source-to-target lexicon
    echo "reference filename: $ref_path/test.$trg";
    echo "BLEU calculation for $src-$trg word-to-word translation with co-occurrence:";
    echo "hyp filename: $ref_path/lex/co/$trg.co.hyp.line"; 
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$trg < $ref_path/lex/co/$trg.co.hyp.line;
    
    echo "BLEU calculation for $src-$trg word-to-word translation with PMI:";
    echo "hyp filename: $ref_path/lex/pmi/$trg.pmi.hyp.line";
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$trg < $ref_path/lex/pmi/$trg.pmi.hyp.line;
    
    echo "BLEU calculation for $src-$trg word-to-word translation with CPE:";
    echo "hyp filename: $ref_path/lex/$trg.cpe.hyp.line";
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$trg < $ref_path/lex/$trg.cpe.hyp.line;
    echo "----------------------------";
    # for target-to-source lexicon
    echo "reference filename: $ref_path/test.$src";
    echo "BLEU calculation for $trg-$src word-to-word translation with co-occurrence:";
    echo "hyp filename: $ref_path/lex/co/$src.co.hyp.line"; 
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$src < $ref_path/lex/co/$src.co.hyp.line;

    echo "BLEU calculation for $trg-$src word-to-word translation with PMI:";
    echo "hyp filename: $ref_path/lex/pmi/$src.pmi.hyp.line";
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$src < $ref_path/lex/pmi/$src.pmi.hyp.line;

    echo "BLEU calculation for $src-$trg word-to-word translation with CPE:";
    echo "hyp filename: $ref_path/lex/$src.cpe.hyp.line";
    perl ~/tool/mosesdecoder/scripts/generic/multi-bleu.perl $ref_path/test.$src < $ref_path/lex/$src.cpe.hyp.line;
    echo "==========";
    echo "";
done

```

running as follows...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ ./evaluation-with-BLEU.sh | tee bleu.log
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/test.bk
BLEU calculation for my-bk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/bk.co.hyp.line
BLEU = 0.00, 19.7/0.0/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=649, ref_len=633)
BLEU calculation for my-bk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/bk.pmi.hyp.line
BLEU = 0.00, 4.0/0.0/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=649, ref_len=633)
BLEU calculation for my-bk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/bk.cpe.hyp.line
BLEU = 0.00, 22.8/6.9/0.9/0.0 (BP=1.000, ratio=1.025, hyp_len=649, ref_len=633)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/test.my
BLEU calculation for bk-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 21.8/0.6/0.0/0.0 (BP=0.975, ratio=0.975, hyp_len=633, ref_len=649)
BLEU calculation for bk-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 4.7/0.0/0.0/0.0 (BP=0.975, ratio=0.975, hyp_len=633, ref_len=649)
BLEU calculation for my-bk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/lex/my.cpe.hyp.line
BLEU = 3.33, 26.4/8.3/2.1/0.3 (BP=0.975, ratio=0.975, hyp_len=633, ref_len=649)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/test.ch
BLEU calculation for my-ch word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/ch.co.hyp.line
BLEU = 0.00, 37.0/2.8/0.7/0.0 (BP=0.701, ratio=0.738, hyp_len=643, ref_len=871)
BLEU calculation for my-ch word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/ch.pmi.hyp.line
BLEU = 0.00, 4.2/0.6/0.0/0.0 (BP=0.701, ratio=0.738, hyp_len=643, ref_len=871)
BLEU calculation for my-ch word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/ch.cpe.hyp.line
BLEU = 0.00, 14.8/1.1/0.0/0.0 (BP=0.701, ratio=0.738, hyp_len=643, ref_len=871)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/test.my
BLEU calculation for ch-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 11.9/0.0/0.0/0.0 (BP=1.000, ratio=1.355, hyp_len=871, ref_len=643)
BLEU calculation for ch-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 0.8/0.0/0.0/0.0 (BP=1.000, ratio=1.355, hyp_len=871, ref_len=643)
BLEU calculation for my-ch word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ch/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 7.3/0.3/0.0/0.0 (BP=1.000, ratio=1.355, hyp_len=871, ref_len=643)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/test.kc
BLEU calculation for my-kc word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/kc.co.hyp.line
BLEU = 0.00, 23.6/5.9/1.6/0.7 (BP=0.000, ratio=0.004, hyp_len=795, ref_len=210951)
BLEU calculation for my-kc word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/kc.pmi.hyp.line
BLEU = 0.00, 4.2/0.9/0.2/0.0 (BP=0.000, ratio=0.004, hyp_len=801, ref_len=180954)
BLEU calculation for my-kc word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/kc.cpe.hyp.line
BLEU = 0.00, 15.5/1.3/0.0/0.0 (BP=0.830, ratio=0.843, hyp_len=819, ref_len=972)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/test.my
BLEU calculation for kc-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 13.6/0.3/0.0/0.0 (BP=1.000, ratio=1.187, hyp_len=972, ref_len=819)
BLEU calculation for kc-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 6.3/0.5/0.0/0.0 (BP=1.000, ratio=1.187, hyp_len=972, ref_len=819)
BLEU calculation for my-kc word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-kc/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 10.8/0.8/0.0/0.0 (BP=1.000, ratio=1.187, hyp_len=972, ref_len=819)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/test.ky
BLEU calculation for my-ky word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/ky.co.hyp.line
BLEU = 0.00, 14.4/0.3/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=872, ref_len=859)
BLEU calculation for my-ky word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/ky.pmi.hyp.line
BLEU = 0.00, 1.5/0.1/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=872, ref_len=859)
BLEU calculation for my-ky word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/ky.cpe.hyp.line
BLEU = 0.00, 4.4/0.1/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=872, ref_len=859)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/test.my
BLEU calculation for ky-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 16.3/0.1/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=859, ref_len=872)
BLEU calculation for ky-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 2.2/0.0/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=859, ref_len=872)
BLEU calculation for my-ky word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-ky/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 5.6/0.0/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=859, ref_len=872)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/test.mo
BLEU calculation for my-mo word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/mo.co.hyp.line
BLEU = 0.00, 20.3/0.5/0.0/0.0 (BP=1.000, ratio=1.031, hyp_len=498, ref_len=483)
BLEU calculation for my-mo word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/mo.pmi.hyp.line
BLEU = 0.00, 1.0/0.0/0.0/0.0 (BP=1.000, ratio=1.031, hyp_len=498, ref_len=483)
BLEU calculation for my-mo word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/mo.cpe.hyp.line
BLEU = 0.00, 8.8/0.0/0.0/0.0 (BP=1.000, ratio=1.031, hyp_len=498, ref_len=483)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/test.my
BLEU calculation for mo-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 21.3/0.0/0.0/0.0 (BP=0.992, ratio=0.992, hyp_len=488, ref_len=492)
BLEU calculation for mo-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 4.9/0.0/0.0/0.0 (BP=0.992, ratio=0.992, hyp_len=488, ref_len=492)
BLEU calculation for my-mo word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-mo/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 11.7/0.3/0.0/0.0 (BP=0.992, ratio=0.992, hyp_len=488, ref_len=492)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/test.pk
BLEU calculation for my-pk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/pk.co.hyp.line
BLEU = 0.00, 7.6/0.0/0.0/0.0 (BP=1.000, ratio=1.032, hyp_len=580, ref_len=562)
BLEU calculation for my-pk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/pk.pmi.hyp.line
BLEU = 0.00, 0.2/0.0/0.0/0.0 (BP=1.000, ratio=1.032, hyp_len=580, ref_len=562)
BLEU calculation for my-pk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pk.cpe.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=1.000, ratio=1.032, hyp_len=580, ref_len=562)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/test.my
BLEU calculation for pk-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 5.2/0.2/0.0/0.0 (BP=0.968, ratio=0.969, hyp_len=562, ref_len=580)
BLEU calculation for pk-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.968, ratio=0.969, hyp_len=562, ref_len=580)
BLEU calculation for my-pk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-pk/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 0.4/0.0/0.0/0.0 (BP=0.968, ratio=0.969, hyp_len=562, ref_len=580)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/test.po
BLEU calculation for my-po word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/po.co.hyp.line
BLEU = 0.00, 19.8/1.3/0.0/0.0 (BP=1.000, ratio=1.435, hyp_len=561, ref_len=391)
BLEU calculation for my-po word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/po.pmi.hyp.line
BLEU = 0.00, 3.2/0.0/0.0/0.0 (BP=1.000, ratio=1.435, hyp_len=561, ref_len=391)
BLEU calculation for my-po word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/po.cpe.hyp.line
BLEU = 0.00, 11.6/0.7/0.3/0.0 (BP=1.000, ratio=1.435, hyp_len=561, ref_len=391)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/test.my
BLEU calculation for po-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 29.2/3.1/1.0/0.0 (BP=0.647, ratio=0.697, hyp_len=391, ref_len=561)
BLEU calculation for po-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 1.5/0.0/0.0/0.0 (BP=0.647, ratio=0.697, hyp_len=391, ref_len=561)
BLEU calculation for my-po word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 22.8/2.7/0.5/0.0 (BP=0.647, ratio=0.697, hyp_len=391, ref_len=561)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/test.rk
BLEU calculation for my-rk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/rk.co.hyp.line
BLEU = 14.28, 50.8/20.8/10.3/3.8 (BP=1.000, ratio=1.009, hyp_len=666, ref_len=660)
BLEU calculation for my-rk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/rk.pmi.hyp.line
BLEU = 1.44, 12.5/1.9/0.6/0.3 (BP=1.000, ratio=1.009, hyp_len=666, ref_len=660)
BLEU calculation for my-rk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/rk.cpe.hyp.line
BLEU = 15.21, 44.3/23.1/10.1/5.2 (BP=1.000, ratio=1.009, hyp_len=666, ref_len=660)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/test.my
BLEU calculation for rk-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 29.4/1.8/0.4/0.0 (BP=0.991, ratio=0.991, hyp_len=660, ref_len=666)
BLEU calculation for rk-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 17.6/4.3/0.9/0.0 (BP=0.991, ratio=0.991, hyp_len=660, ref_len=666)
BLEU calculation for my-rk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp.line
BLEU = 14.14, 44.1/22.7/9.3/4.4 (BP=0.991, ratio=0.991, hyp_len=660, ref_len=666)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/test.rw
BLEU calculation for my-rw word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/rw.co.hyp.line
BLEU = 0.00, 9.7/0.0/0.0/0.0 (BP=0.000, ratio=0.008, hyp_len=743, ref_len=90735)
BLEU calculation for my-rw word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/rw.pmi.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=754, ref_len=744)
BLEU calculation for my-rw word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/rw.cpe.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=754, ref_len=744)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/test.my
BLEU calculation for rw-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 13.3/0.0/0.0/0.0 (BP=0.987, ratio=0.987, hyp_len=744, ref_len=754)
BLEU calculation for rw-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 0.1/0.0/0.0/0.0 (BP=0.987, ratio=0.987, hyp_len=744, ref_len=754)
BLEU calculation for my-rw word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rw/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 0.3/0.0/0.0/0.0 (BP=0.987, ratio=0.987, hyp_len=744, ref_len=754)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/test.sh
BLEU calculation for my-sh word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/sh.co.hyp.line
BLEU = 0.00, 16.8/0.0/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=649, ref_len=643)
BLEU calculation for my-sh word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/sh.pmi.hyp.line
BLEU = 0.00, 1.5/0.0/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=649, ref_len=643)
BLEU calculation for my-sh word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/sh.cpe.hyp.line
BLEU = 0.00, 19.3/1.5/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=649, ref_len=643)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/test.my
BLEU calculation for sh-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/co/my.co.hyp.line
BLEU = 0.00, 18.8/0.4/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=643, ref_len=649)
BLEU calculation for sh-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 2.5/0.0/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=643, ref_len=649)
BLEU calculation for my-sh word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sh/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 21.3/1.1/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=643, ref_len=649)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/test.sk
BLEU calculation for my-sk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp.line
BLEU = 7.47, 42.7/10.2/4.1/1.7 (BP=1.000, ratio=1.023, hyp_len=588, ref_len=575)
BLEU calculation for my-sk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/sk.pmi.hyp.line
BLEU = 0.00, 2.0/0.0/0.0/0.0 (BP=1.000, ratio=1.023, hyp_len=588, ref_len=575)
BLEU calculation for my-sk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/sk.cpe.hyp.line
BLEU = 0.00, 25.9/3.5/0.5/0.0 (BP=1.000, ratio=1.023, hyp_len=588, ref_len=575)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/test.my
BLEU calculation for sk-my word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp.line
BLEU = 6.40, 43.8/9.1/3.2/1.4 (BP=0.978, ratio=0.978, hyp_len=575, ref_len=588)
BLEU calculation for sk-my word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/pmi/my.pmi.hyp.line
BLEU = 0.00, 8.9/0.2/0.0/0.0 (BP=0.978, ratio=0.978, hyp_len=575, ref_len=588)
BLEU calculation for my-sk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/my.cpe.hyp.line
BLEU = 0.00, 37.6/6.3/2.1/0.0 (BP=0.978, ratio=0.978, hyp_len=575, ref_len=588)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/test.bk
BLEU calculation for rk-bk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/bk.co.hyp.line
BLEU = 0.00, 20.8/0.4/0.2/0.0 (BP=1.000, ratio=1.003, hyp_len=635, ref_len=633)
BLEU calculation for rk-bk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/bk.pmi.hyp.line
BLEU = 0.00, 5.2/0.2/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=635, ref_len=633)
BLEU calculation for rk-bk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/bk.cpe.hyp.line
BLEU = 0.00, 20.8/5.4/1.1/0.0 (BP=1.000, ratio=1.003, hyp_len=635, ref_len=633)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/test.rk
BLEU calculation for bk-rk word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/co/rk.co.hyp.line
BLEU = 0.00, 27.0/1.7/0.5/0.0 (BP=0.997, ratio=0.997, hyp_len=633, ref_len=635)
BLEU calculation for bk-rk word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/pmi/rk.pmi.hyp.line
BLEU = 0.00, 5.1/0.0/0.0/0.0 (BP=0.997, ratio=0.997, hyp_len=633, ref_len=635)
BLEU calculation for rk-bk word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rk-bk/w2w/lex/rk.cpe.hyp.line
BLEU = 2.91, 23.4/6.4/1.6/0.3 (BP=0.997, ratio=0.997, hyp_len=633, ref_len=635)
==========

reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/test.kc
BLEU calculation for rw-kc word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/kc.co.hyp.line
BLEU = 0.00, 13.7/0.0/0.0/0.0 (BP=0.999, ratio=0.999, hyp_len=728, ref_len=729)
BLEU calculation for rw-kc word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/kc.pmi.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.999, ratio=0.999, hyp_len=728, ref_len=729)
BLEU calculation for rw-kc word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/kc.cpe.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.999, ratio=0.999, hyp_len=728, ref_len=729)
----------------------------
reference filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/test.rw
BLEU calculation for kc-rw word-to-word translation with co-occurrence:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp.line
BLEU = 0.00, 13.7/0.0/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=729, ref_len=728)
BLEU calculation for kc-rw word-to-word translation with PMI:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/pmi/rw.pmi.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=729, ref_len=728)
BLEU calculation for rw-kc word-to-word translation with CPE:
hyp filename: /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/rw.cpe.hyp.line
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=729, ref_len=728)
==========
```

BLEU score တွေက အထက်ပါအတိုင်း သုညမကွဲတာတွေ များတယ်။ သို့သော် တချို့ရလဒ်တွေက BLEU score 14, 15 ထိ ရတာလည်း တွေ့ရတယ်။  

သုညမကွဲတဲ့ ရလဒ်တွေထဲက ကချင်-ရဝမ် co-occurrence ရဲ့ ရလဒ်နဲ့ reference ကို head -n x လုပ်ပြီး ကြည့်ကြည့်ရအောင်။   
Reference ကချင် က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/test.rw
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
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

word-to-word ရဝမ် translated output က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/rw-kc/w2w/lex/co/rw.co.hyp.line
OOV nø̀ ngà . . . .
OOV nø̀ ngà . . . . .
OOV nø̀ ngà . . . . . .
OOV nø̀ ngà . . . .
OOV nø̀ ngà . yà . .
OOV nø̀ ngà . yà . . .
OOV nø̀ ngà . yà . . . .
OOV nø̀ ngà . yà . .
OOV nø̀ ngà . yà . .
OOV nø̀ ngà . yà . . .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

-------------

စကောကရင် ကနေ ဗမာ ကို co-occurrence နဲ့ ဘာသာပြန်ပြီး ရလာတာကို စာကြောင်းအဖြစ်တွဲကြည့်ထားတာကို ကြည့်ကြရအောင်...  
Reference ဗမာ က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/test.my
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
```

Hypothesis output ဗမာ စာကြောင်းတချို့ကို လေ့လာ ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/my.co.hyp.line
ဆေးရုံ ဒီ ကို ဆရာဝန် ယောက် လုပ် အလုပ်
မ OOV မ OOV
OOV စာအုပ်ကလေး နော်
သွား တက် သင်တန်း
ဘယ်သူ လို့ သူ ရှက် ကျွန်တော်
ဆင်း ဘယ်လောက် လဲ
သူ ရှိ တဲ့ လမ်း မှာ လဲ
စောင့် ပါရစေ
သူ မ OOV ကို ကို အဲ့ဒါ
မ ကျ ဘယ်လောက် လဲ
```

-------------

မြန်မာ ကနေ စကောကရင် ဘာသာပြန်ပြီး ထွက်လာတဲ့ output ကိုလည်း လေ့လာကြည့်ရအောင်...  

စကောကရင် Reference:  
```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/test.sk
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
```

စကောကရင် Hypothesis:  
```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-sk/w2w/lex/co/sk.co.hyp.line
အံၤ တၢ်ဆါဟံၣ် န့ၣ် ကသံၣ်သရၣ် လၢတၢ်ဆါဟံၣ် တၢ်မၤ မၤ န့ၣ်လီၤ
တၢ်ဝဲန့ၣ် ကွဲးကွဲး တ ကွဲးကွဲး
ဟ့ၣ်လီၤယၤ ဟ့ၣ်ခီဂာ် ဝံသးစူၤ
တၢ်မၤလိ လဲၤ လဲၤထီၣ်ဝဲ
မတၤ ဘၣ်တၢ်နၢမူဝဲအဃိ အဝဲ အဂီၢ် ယ
န န့ၣ်လီၤ လဲၣ်
အဝဲ လဲၣ် ကျဲ န့ၣ် န့ၣ်လီၤ လဲၣ်
အဝဲ န
အဝဲ တၢ်ဝဲန့ၣ် န့ၣ် တ အဝဲ တ
တၢ်ဝဲန့ၣ် လဲၣ် လီၤ လဲၣ်
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-po/w2w/lex$
```

-------------

ရခိုင်-ဗမာ language pair ကို လေ့လာရအောင်...  
ဗမာစာ reference ဖိုင်ရဲ့ စာကြောင်းတချို့ကို ကြည့်ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/test.my
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
```

ရခိုင် ကနေ ဗမာ ကို CPE approach နဲ့ ဘာသာပြန် Hypothesis က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ head /media/ye/project2/exp/word2word-tran/word2word/my-x/my-rk/w2w/lex/my.cpe.hyp.line 
OOV သူတို့ OOV သိပ် ရထားကြီး လို့ ငါ ထင် ခက်ခဲတယ် တာလား
ဒါ အကြိမ်ပဲ အပတ်မှာ တတိယ ပျက်တာ ပါ တာလား
အတန်း OOV ရုံးချိန်းက မိနစ် ရှိနေတဲ့အတွက်ကြောင့် အတန်း ခဲ့ပါဘူး ရောက် ရမယ်
OOV မရှိဘူး ဘူးလား တာလား
ပါ့မယ် တစ်နည်းနည်း ကျွန်တော့် မိသားစု အပေါ် မင်းရဲ့ ဧည့်ဝတ်ကျေပွန်မှု အတွက် ကျေးဇူးတင်ပါတယ် တာလား
ကျွန်တော့် အတွက် စာမေးပွဲ အောင် ဖို့ရာ လွယ်လွယ်လေးပါ တာလား
သူ နေလို့ ရှိဘူး ကောင်း ထင်တယ်
သူ သူ့ စားပွဲ ရှိနေတဲ့အတွက်ကြောင့် ရှိဘူး ရှိဘူး တာလား
ရှင် စကား ပြောနေ တာ တာလား
အဲ့ဒါ တိ ခဲ့ပါဘူး အလွတ် OOV ပါ တာလား
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Discussion-1

လက်ရှိအချိန်ထိ လုပ်ခဲ့တဲ့ experiment နဲ့ ရလဒ်တွေကို ကြည့်ပြီး conclusion ချလို့ ရနိုင်တာက 

- ငါတို့ monolingual ရော crosslingual or bilingual co-occurrences တွေကိုကော ထည့်သွင်းစဉ်းစားပြီး approaches သုံးမျိုး ဖြစ်တဲ့ co-occurrences, PMI (Pointwise Mutual Information) နဲ့ CPE (Controlled Predictived Effects) တို့နဲ့ lexicon တွေ ဆောက်ခဲ့တယ်
- low-resourced ဒေတာနဲ့ word-to-word lexicon ဆောက်တာက word-to-word level translation အတွက် အတိုင်းအတာ တစ်ခုအထိ အထောက်အကူပြုတယ်
- lexicon building လုပ်တဲ့ speed ကလည်း မြန်တယ်
- Evaluation ကို နှစ်မျိုး လုပ်ကြည့်ခဲ့တယ် word-to-word translation လုပ်ကြည့်တော့ OOV ဘယ်နှစ်လုံးရှိသလဲ (ဆိုလိုတာက translation မလုပ်ပေးနိုင်တာက ဘယ်နှစ်လုံး ရှိသလဲ ဆိုတာကို count လုပ်တဲ့ ပုံစံနဲ့) ဆိုတာကို ရေတွက်တဲ့ OOV% နဲ့ နောက်တစ်မျိုးက စာလုံး တစ်လုံးစီအတွက် word-to-word translation လုပ်ထားတာတွေကို စာကြောင်းအဖြစ် (i.e. build as a sentence) ဆောက်လိုက်ပြီး BLEU score တွက်ကြည့်တာ
- OOV% တွေကို ကြည့်ရင် ရလဒ်ကောင်းတယ် သို့သော် ထင်ထားတဲ့အတိုင်း (as we expected) sentence level BLEU score တွေက တအားနည်းတယ်
- တချို့ parallel-data နည်းတာနဲ့ ဆောက်ထားတဲ့ corpus အပေါ်ကို မူတည်ပြီး အထူးသဖြင့် sentence level မှာတော့ သုံးလို့ မရနိုင်ဘူး
- မြန်မာ-ရခိုင်လို language pair မှာတော့ BLEU score က 14, 15 ရတာကို တွေ့ရပေမဲ့ အဲဒီလို အရမ်းဆင်တူတဲ့ dialect က လက်ရှိ parallel corpus အရွယ်အစားနဲ့ပဲ SMT တို့ကို training လုပ်ရင် ရလဒ်တအားကောင်းတာမို့... အရမ်းကြီး ထူးဆန်းတာတော့ မဟုတ်ဘူး
- လက်ရှိ word-to-word Evaluation က ထောက်ပြမယ်ဆိုရင် ထောက်ပြစရာတွေရှိတယ်။ OOV% ကိုတော့ တွက်ထားပေမဲ့ တကယ်တမ်း ဘာသာပြန်ထားတဲ့ စာလုံးတွေက မှန်တယ်/မှားတယ် ဆိုတာကို သေသေချာချာ analysis လုပ်မထားတဲ့ အချက်လိုမျိုး။ ခက်တာက ငါတို့မှာ သုံးဖို့ အဆင်သင့် ဖြစ်တဲ့ word-to-word အဘိဓာန်က လက်ထဲမှာ ရှိမနေတာနဲ့ human evaluation လုပ်မယ် ဆိုရင်လည်း ဘာသာစာကားတွဲ တစ်ခုချင်းစီအတွက် native speaker (ဥပမာ ကချင်စကား နားလည်တဲ့သူ၊ ရှမ်းစကား နားလည်တဲ့သူ၊ ရဝမ်စကား နားလည်တဲ့သူ ... ) တွေကို အကူအညီတောင်းဖို့အတွက်က research funds လိုအပ်တယ်။ အချိန်လည်း လိုအပ်တယ်
- experiment ကို နောက်ထပ် extension လုပ်လို့ ရနိုင်တာက phrase-level alignment လုပ်ချပြီး ဗမာစာနဲ့ တိုင်းရင်းသား ဘာသာစကားတွေအကြားကို ဘယ်လောက် ဘာသာပြန်ပေးနိုင်သလဲ ဆိုတဲ့ experiment လိုမျိုး
- လက်ရှိ parallel-corpus ရဲ့ size ကို တိုးနိုင်ရင်လည်း တကယ်တမ်း ပိုအသုံးဝင်တဲ့ အဘိဓာန် အကြီးကြီးတွေ အကြမ်းဆောက်တာမျိုးကို ကောင်းကောင်းလုပ်နိုင်တာမို့ future work အနေနဲ့က data extension လုပ်ကို လုပ်သင့်တယ်။ သိတဲ့အတိုင်းပဲ parallel corpus building က နှစ်နဲ့ချီ လုပ်ရလိမ့်မယ် ...  


## Reference

- [https://github.com/ye-kyaw-thu/error-overflow/blob/master/word2word_translation-exp-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/word2word_translation-exp-log.md)
- [word2word](https://github.com/kakaobrain/word2word)
- [https://stackoverflow.com/questions/918886/how-do-i-split-a-string-on-a-delimiter-in-bash](https://stackoverflow.com/questions/918886/how-do-i-split-a-string-on-a-delimiter-in-bash)
- [https://stackoverflow.com/questions/55126019/python3-to-find-number-of-features-in-pickle?noredirect=1&lq=1](https://stackoverflow.com/questions/55126019/python3-to-find-number-of-features-in-pickle?noredirect=1&lq=1)  
- [https://www.unix.com/shell-programming-and-scripting/105887-sed-awk-concatenate-lines-until-blank-line.html](https://www.unix.com/shell-programming-and-scripting/105887-sed-awk-concatenate-lines-until-blank-line.html)  
