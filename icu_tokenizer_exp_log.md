# ICU based Word Tokenizations

Actually, I tested ICU original C++ library around 2012 at the NICT. This is revisiting ICU based word tokenization with Python library.   

## Library Installation

```
(base) ye@lst-gpu-3090:~/exp/icu_tool$ pip install PyICU
Collecting PyICU
  Downloading PyICU-2.12.tar.gz (260 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 260.0/260.0 kB 3.0 MB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: PyICU
  Building wheel for PyICU (pyproject.toml) ... done
  Created wheel for PyICU: filename=PyICU-2.12-cp38-cp38-linux_x86_64.whl size=1836203 sha256=38704e0148119da077e6237a202c5e80426fb1f561acc21cdec57fbc9d1af799
  Stored in directory: /home/ye/.cache/pip/wheels/23/a9/a5/808a8046a4e1ba25dc551d100bf2dd8b78d80879e4620f146c
Successfully built PyICU
Installing collected packages: PyICU
Successfully installed PyICU-2.12
(base) ye@lst-gpu-3090:~/exp/icu_tool$
```

## Dictionary Based

### Dictionary Data Preparation

Check myWord Data ...   

```
လု သာ မောင်း ပြိုင် သာ ပြိုင် ကိုယ့် ကိုယ်ပိုင် ကား မ ဟုတ် ပြဿနာ ဖြစ် ရင် ထွက် ပြေး အေးအေးဆေးဆေး ဖြစ် သွား ရင် ပြန် မောင်း လု သာ မောင်း ။
သမ္မတ ဦးထင်ကျော်
အင်းလေး သူ ဆို လည်း ကောင်း တာ ပဲ ၊ ကစ်ကစ် က ဖြူဖြူ ဖွေးဖွေးလေး ဆို တော့ ၊ ရှမ်းမလေး တွေ တော့ ထိုင် ငို နေ တော့ မှာ ပဲ အင်းလေး ကို အရမ်း ချစ် တယ် အင်းလေး နဲ့ ကစ် နဲ့ လိုက် ပါ တယ် တသက်လုံး တကယ် လာ နေ ရင် အရမ်း ကောင်း မှာ ပဲ ချစ်﻿ တယ် မကစ် ဇင်ဇင် တို့ မွန် ပြည်နယ် လာလည် ပါ လား ဖိတ်ခေါ် ပါ တယ် ကျိုက်ထီးရိုး ဘုရား ဖူး ရင် မော်လမြိုင် မြို့ ကို လာလည် ပါ ရှမ်း က မဲ တာ လား အင်းသူမ က မဲ တာ လား မူကြို ကလေး မေး တောင် သိ တယ် အင်းသူမ က ဘယ်လောက် ပဲ ပိုက်ဆံ ရှိ ပါစေ အလောင်းစည်သူမင်း ကျိန်စာ တိုက် ခဲ့ လို့ ရေ ခြံ ရော ကုန်း ခြံ ရော ကုန်း နေ အောင် လုပ် ရ တာ ဖြူ နေ ဦး မယ် အသား က ကြည့် ပြော အင်းသူမ လုပ် ရင် ရေ ကူး တတ် ရ မယ် နော် ရေ မ ကူး တတ် ရင် အလောင်း တွေ ခု ချိန် ထိ ဆယ် မ ကုန် သေး ဘူး အသဲ 😍 😍 😍 😍 မမ ကစ် ချစ် လိုက် တာ ကောင်း တယ် လုပ် ပစ် လိုက် အမ 😁 😁 😁 😁 ကစ် သာ နေ ရင် ရှမ်း ပြည် အပြီး ပြန် လာ မယ် နေ နိုင် လား ဘဝ ကို ဖြတ်သန်း တဲ့ အခါ အရိုးဆုံး က အကောင်းဆုံး ပါ ပဲ မ လုပ် ပါ နဲ့ ကစ်လေး ရယ် ရန်ကုန် ကို အမြန် ပြန် လာ ပါ ကိုယ် အရမ်း သတိရ လို့ ပါ ကွာ ချစ် တာ 😍 😍 😘 😘 ချစ် စရာ လေး အရမ်း ကြိုက် မမ နေ ပါ ကစ်လေး ရယ် သာယာ လိုက် တာ အဲ့ နား မှာ အိမ် တစ် လုံး သွား ဝယ် လိုက် မှာ ပေါ့ ။
အင်းသား ဖြစ် ချင် လို့ အင်းသူမ ပဲ လုပ် တော့ မကစ် คุณน่ารักเสมอ 💟 ကြည့် လို့ မ ရ တော့ ဘူး နော် ကိုကြီး နေ ဖို့ လည်း မ ကောင်း ပဲ ရေ ထဲ မှာ ငါ မ ကြိုက် ဘူး ကောင်း သား ပဲ အင်းသူမလေး ဆို တော့ အေးအေးချမ်းချမ်း လေး ပေါ့ နော် မကစ် ကို က အင်းသား ဖြစ် ပါရစေ ကောင်း တာ ပေါ့ ကစ် ရဲ့ အင်းသူလေး တွေ က ဖြူစင် တယ် အင်းသူမလေး ဖြစ် တော့ မယ် ရွှေ ကစ်လေး :- * ကောင်း သလိုလို တော့ ရှိ သား နော်
ရွှေ ကစ်လေး ရဲ့ ကုသိုလ် ကြောင့် အစစအရာရာ ပြီးပြည့်စုံ မှာ ပါ ရွှေ ကစ်လေး ကို လည်း သေ တဲ့ ထိ အားပေး မှာ ပါ အရမ်း ချစ် တယ် သာဓု ပါ သာဓု ပါ သာဓု ပါ ဒီ ထက် မက လှူ နိုင် ပါစေ နော် 👏 👏 👏 👏 👏 👍 👍 👍 အခု လို ပြု ရ သော ကုသိုလ် ကောင်း မှု တွေ ကြောင့် ဘဝ မှာ တောင်းတ ခြင်း နဲ့ ကြောက် ရ ခြင်း ကင်းဝေး ပြီး တော့ မနက်ဖြန် တွေ တိုင်း မှာ ချစ် တဲ့ မိသားစု နဲ့ ပျော်ရွှင် စွာ ဖြတ်သန်း နိုင် ပါစေ မကစ် 😍 😍 😍 😍 😍
အနိုင်ရ မည့် အသင်း = ပြင်သစ် ဂိုး ရလဒ် = ပြင်သစ် ၂ - ၀ ခရိုအေးရှား
မွန် ရခိုင် ရခိုင် ရခိုင် ရခိုင်
ည အရမ်း တိုးတက် လို့ ပါ လား ခြင်္သေ့ အက တွေ နဲ့ တော့ ပြန် ကြည့် ချင် တယ် ယား နေ ရော ပဲ ဝမ်းစာရေး က အဓိက ပါ လေ ပြန် တော့ ဘူး တော် ပါ ပေ တယ် ဗျာ လေးစား တယ် ဝိုး လီး ဘဲ့ စောက် တရုတ် ပွဲ ကျ ခမ်းခမ်းနားနား ကျင်းပ ပေး တယ် တရုတ် ပြည် လည်း ဝင် တိုက် လိုက် လေ ဆယ်ဆ ပေး ရင် နိုင် မယ် လာ ။
အလုပ် လည်း လုပ် ပညာ လည်း ယူ ချမ်းသာ ရင် တရုတ် ပြည် သွား လည် ရင် မ ကောင်း ဘူး လား ။
အဲ့ အတွေး ပဲ လူ ဖြစ် ရင် ထမင်း စား လည်း အလကား ပဲ ။
(base) ye@lst-gpu-3090:~/exp/myNLP/data$
```

```
(base) ye@lst-gpu-3090:~/exp/myNLP/data$ shuf ./segmentation-data-updated2 | head
နောက် နှစ် ပေါင်း ၅ ဘီလီယံ လောက် ကြာ ရင် က ကျွန်တော် တို့ နေမင်းကြီး က လောင်စာ ကုန် လို့ ပွတက် လာ မှာ ဖြစ် ပြီး ကမ္ဘာ ကို လည်း ဝါးမြို သွား မှာ ဖြစ် ပြီး လူသား တို့ အပါအဝင် သက်ရှိ များ အားလုံး ကို ဖျောက်ပစ် လိုက် ပါ လိမ့် မယ် ။
ဒီ လို ဖြစ်ရပ် ကြီး ပြီး တိုင်း မှာ မ တူညီ တဲ့ သက်ရှိ မျိုးစိတ် များ ပြန်လည် တိုးထွက် လာ ခြင်း ဟာ လည်း အတော် လေး ကို များပြား ခဲ့ ပါ တယ် ။
အခု လို ရွှံ့စေး များ ကို ရှာဖွေ ခြင်း ဟာ မားစ် ပေါ် က ရေ များ ရဲ့ သမိုင်း တစ် လျှောက် ဖြစ်တည် ပြောင်းလဲ မှု များ ကို အသေးစိတ် သိရှိ နိုင် မှာ လည်း ဖြစ် ပါ တယ် ။
မင်း တို့ က မောင်ချို ကြိုက် တာ ကို ကွ အန်ကယ် က အမှန်တရား ပြော တာ
မ ကောင်း သော်လည်း ချမ်း အေးအေး ည တွင် ပူပူနွေးနွေး စား ကြ ရ သော ကြောင့် လုံးဝ မ စား ရ သည် ထက် တော့ တော် ပါ သေး ၏ ။
စစ်ဝတ်ချပ်မိန် ကို အပြည့် ဆင်ယင် ထား ပြီး သတ္တဓနု လေး ကြီး ၏ လေး မြို့ တွင် မြား တစ် ချောင်း ကို တပ်ဆင် ကာ လေး ချို့ ကို ငင် နေ သည့် သမိန်စက္ကဝတ် ၏ ရုပ်ပုံ ။
သူခိုး ၊ ဓားပြ များ ထကြွ သောင်းကျန်း နေ ကြ သည် ။
လင်းလွန်း က ဧည့်ခန်း နောက်ဘက် ကို လှမ်း ကြည့် လိုက် တော့ အသင့် ရပ် စောင့် နေ သော ဒေါ်သန်း နှင့် အေးယဉ် ကို တွေ့ ရ သည် ။
သားရဲတွင်း ထဲ မှာ သမင် အုပ် များ ကို လေ့ကျင့် ပေး နေ ပါ တယ် နောင်တော် ဘုရင်မင်းမြတ်
အဲ့ဒီ အချိန် မှာ အမတ် ကြီး က သူ ဆောင် ယူ လာ တဲ့ သားရေ ပြား ချပ် လေး ကို ပေး လိုက် ရင်း ဒါ ကမ္ဘာ အရပ်ရပ် က လူသား သမိုင်း ပါ အရှင် မင်းကြီး မင်းကြီး မျက်မှောင် ကုပ် သွား တယ် ။
(base) ye@lst-gpu-3090:~/exp/myNLP/data$
```

Check myG2P dictionary data ...  

```
(base) ye@lst-gpu-3090:~/exp/myNLP/data$ head myg2p.f2
...ဖြစ်စေ...ဖြစ်စေ
...ရိုး...စဉ်
...ရိုး...စဉ်
...လို...ငြား
ကကတစ်
ကကတိုး
ကကုသန်
ကကုသန်
ကကူရံ
ကကြိုး
```

Deleted top 4 lines of myg2p.f2 data.  

Check with tail command:  

```
(base) ye@lst-gpu-3090:~/exp/myNLP/data$ tail ./myg2p.f2
ဧည့်မထ
ဧည့်မြေ
ဧည့်မြှောင်
ဧည့်ရိပ်သာ
ဧည့်လာဂမုန်း
ဧည့်ဝတ်
ဧည့်ဝတ်ဆောင်ဝတ်
ဧည့်သည်
ဧည့်သည်စောင်သည်
ဪလဲ
(base) ye@lst-gpu-3090:~/exp/myNLP/data$
```

```
(base) ye@lst-gpu-3090:~/exp/myNLP/data$ wc ./myg2p.f2
 24798  24798 691632 ./myg2p.f2
```

## Dummy Test Data

```
စတီရီယိုကဖီးနဲ့အဆိုတော်အောင်ရင်စကားဝိုင်း။ 
(အပိုင်း-၁)
အလုပ်လည်းလုပ်ပညာလည်းယူချမ်းသာရင်တရုတ်ပြည်သွားလည်ရင်မကောင်းဘူးလား။
ရှင်ရှင်ဒေါ်သထာဖြူကွယ်လွန်ခြင်း၄၅နှစ်မြောက်နေ့ပါလား!
သမ္မတဦးထင်ကျော်
အနိုင်ရမည့်အသင်း=ပြင်သစ်ဂိုးရလဒ်=ပြင်သစ်၂-၀ခရိုအေးရှား
အားပေးမှာပါအရမ်းချစ်တယ်သာဓုပါသာဓုပါသာဓုပါဒီထက်မကလှူနိုင်ပါစေနော်👏👏👏👏👏👍👍👍အခုလိုပြုရသောကုသိုလ်ကောင်းမှုတွေကြောင့်ဘဝမှာတောင်းတခြင်းနဲ့ကြောက်ရခြင်းကင်းဝေးပြီးတော့မနက်ဖြန်တွေတိုင်းမှာချစ်တဲ့မိသားစုနဲ့ပျော်ရွှင်စွာဖြတ်သန် နိုင်ပါစေမကစ်😍😍😍😍😍
စစ်ဝတ်ချပ်မိန်ကိုအပြည့်ဆင်ယင်ထားပြီးသတ္တဓနုလေးကြီး၏လေးမြို့တွင်မြားတစ်ချောင်းကိုတပ်ဆင်ကာလေးချို့ကိုငင်နေသည့် သမိန်စက္ကဝတ်၏ရုပ်ပုံ။
အခုလိုရွှံ့စေးများကိုရှာဖွေခြင်းဟာမားစ်ပေါ်ကရေများရဲ့သမိုင်းတစ်လျှောက်ဖြစ်တည်ပြောင်းလဲမှုများကိုအသေးစိတ်သိရှိနိုင်မှာလည်းဖြစ်ပါတယ်။
နောက်နှစ်ပေါင်း၅ဘီလီယံလောက်ကြာရင်ကကျွန်တော်တို့နေမင်းကြီးကလောင်စာကုန်လို့ပွတက်လာမှာဖြစ်ပြီးကမ္ဘာကိုလည်းဝါးမြိုသွားမှာဖြစ်ပြီးလူသားတို့အပါအဝင်သက်ရှိများအားလုံးကိုဖျောက်ပစ်လိုက်ပါလိမ့်မယ်။
```

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ cat 10lines.txt
စတီရီယိုကဖီးနဲ့အဆိုတော်အောင်ရင်စကားဝိုင်း။
(အပိုင်း-၁)
အလုပ်လည်းလုပ်ပညာလည်းယူချမ်းသာရင်တရုတ်ပြည်သွားလည်ရင်မကောင်းဘူးလား။
ရှင်ရှင်ဒေါ်သထာဖြူကွယ်လွန်ခြင်း၄၅နှစ်မြောက်နေ့ပါလား!
သမ္မတဦးထင်ကျော်
အနိုင်ရမည့်အသင်း=ပြင်သစ်ဂိုးရလဒ်=ပြင်သစ်၂-၀ခရိုအေးရှား
အားပေးမှာပါအရမ်းချစ်တယ်သာဓုပါသာဓုပါသာဓုပါဒီထက်မကလှူနိုင်ပါစေနော်👏👏👏👏👏👍👍👍အခုလိုပြုရသောကုသိုလ်ကောင်းမှုတွေကြောင့်ဘဝမှာတောင်းတခြင်းနဲ့ကြောက်ရခြင်းကင်းဝေးပြီးတော့မနက်ဖြန်တွေတိုင်းမှာချစ်တဲ့မိသားစုနဲ့ပျော်ရွှင်စွာဖြတ်သန် နိုင်ပါစေမကစ်😍😍😍😍😍
စစ်ဝတ်ချပ်မိန်ကိုအပြည့်ဆင်ယင်ထားပြီးသတ္တဓနုလေးကြီး၏လေးမြို့တွင်မြားတစ်ချောင်းကိုတပ်ဆင်ကာလေးချို့ကိုငင်နေသည့် သမိန်စက္ကဝတ်၏ရုပ်ပုံ။
အခုလိုရွှံ့စေးများကိုရှာဖွေခြင်းဟာမားစ်ပေါ်ကရေများရဲ့သမိုင်းတစ်လျှောက်ဖြစ်တည်ပြောင်းလဲမှုများကိုအသေးစိတ်သိရှိနိုင်မှာလည်းဖြစ်ပါတယ်။
နောက်နှစ်ပေါင်း၅ဘီလီယံလောက်ကြာရင်ကကျွန်တော်တို့နေမင်းကြီးကလောင်စာကုန်လို့ပွတက်လာမှာဖြစ်ပြီးကမ္ဘာကိုလည်းဝါးမြိုသွားမှာဖြစ်ပြီးလူသားတို့အပါအဝင်သက်ရှိများအားလုံးကိုဖျောက်ပစ်လိုက်ပါလိမ့်မယ်။
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

### Testing with myG2P Dictionary Only

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ time python ./icu_word_tokenizer.py --diction
ary ../data/myg2p.f2 ./10lines.txt ./10lines.txt.word

real    0m0.074s
user    0m0.016s
sys     0m0.008s
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ cat ./10lines.txt.word
စတီရီယို
ကဖီး
နဲ့
အဆိုတော်
အောင်
ရင်
စကား
ဝိုင်း
။
```


After I updated the code:  

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ head ./10lines.txt.word
စတီရီယို ကဖီး နဲ့ အဆိုတော် အောင် ရင် စကား ဝိုင်း ။ ( အပိုင်း - ၁ ) အလုပ် လည်း လုပ် ပညာ လည်း ယူ ချမ်းသာ ရင် တရုတ် ပြည် သွား လည် ရင်မ ကောင်း ဘူး လား ။ ရှင်ရှင် ဒေါ် သထာ ဖြူ ကွယ်လွန် ခြင်း၄၅နှစ်မြောက် နေ့ ပါ လား ! သမ္မတ ဦး ထင် ကျော် အနိုင်ရ မည့် အသင်း = ပြင် သစ် ဂိုး ရလဒ် = ပြင် သစ်၂ - ၀ခ ရို အေး ရှား အားပေး မှာ ပါ အရမ်း ချစ် တယ် သာဓု ပါ သာဓု ပါ သာဓု ပါ ဒီ ထက် မက လှူ နိုင် ပါ စေ နော် 👏👏 👏👏 👏👍 👍👍 အခ ုလ ို ပြ ုရသ ောက ုသိ ု လ်က ောင်းမှ ုတွေကြောင ့်ဘ ဝမှာတော င် းတခ ြင်းနဲ ့ ကြောက ်ရခ ြင်းကင ် းဝေးပ ြီးတ ော့ မနက် ဖြန် တွေတိုင် းမှ ာချစ်တ ဲ့မ ိသား စုန ဲ့ပျော် ရွှ င်စွာ ဖြတ်သ န် နိုင ်ပါ စ ေမကစ် 😍😍 😍😍 😍 စစ ်ဝ တ် ချ ပ် မိ န ်ကိုအပ ြည့် ဆင်ယ င်ထ ားပြီး သတ္တဓန ုလေ းကြီ း၏လေ းမြ ို့ တွင် မ ြား တစ်ချ ောင် းကို တပ် ဆင်ကာလေ းချ ို့ ကို ငင ်နေ သည့် သမိ န်စ က္ ကဝတ် ၏ ရ ုပ်ပ ုံ။
အခု လ ိုရွှံ့ စ ေ းမျ ားက ိုရှာဖွေ ခြင် းဟာ မားစ်ပ ေါ်ကရ ေမ ျား ရဲ ့သမိ ု င် းတစ် လျှ ောက်ဖြစ ်တည်ပြောင် းလဲမ ှုမ ျားကိုအသေ းစိ တ်သိ ရှိ နိုင်မှာ လည်းဖ ြစ်ပါ တယ် ။
နေ ာက်န ှစ ်ပေ ါ င ်း၅ဘီ လီယံ လောက်ကြာရ င် ကက ျွန်တ ော် တို ့ နေမင်းကြီ းကလေ ာင်စာက ုန်လ ို့ပွတ က် လာမှ ာဖြစ ်ပ ြီး ကမ ္ဘာ ကိုလ ည်းဝ ါးမြိ ုသွ ားမှ ာဖြ စ်ပြ ီးလူ သား တို့ အပါအ ဝင်သက ်ရှိ များအား လုံးကိ ုဖျေ ာက်ပစ်လ ိုက ်ပါလိမ့်မ ယ်။(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

```

(
အပိုင်း
-
၁
)


အလုပ်
လည်း
လုပ်
ပညာ
လည်း
ယူ
ချမ်းသာ
ရင်
တရုတ်
ပြည်
သွား
လည်
ရင်မ
ကောင်း
ဘူး
လား
။


ရှင်ရှင်
ဒေါ်
သထာ
ဖြူ
ကွယ်လွန်
ခြင်း၄၅နှစ်မြောက်
နေ့
ပါ
လား
!


သမ္မတ
ဦး
ထင်
ကျော်


အနိုင်ရ
မည့်
အသင်း
=
ပြင်
သစ်
ဂိုး
ရလဒ်
=
ပြင်
သစ်၂
-
၀ခ
ရို
အေး
ရှား


အားပေး
မှာ
ပါ
အရမ်း
ချစ်
တယ်
သာဓု
ပါ
သာဓု
ပါ
သာဓု
ပါ
ဒီ
ထက်
မက
လှူ
နိုင်
ပါ
စေ
နော်
👏👏
👏👏
👏👍
👍👍
အခ
ုလ
ို
ပြ
ုရသ
ောက
ုသိ
ု
လ်က
ောင်းမှ
ုတွေကြောင
့်ဘ
ဝမှာတော
င်
းတခ
ြင်းနဲ
့
ကြောက
်ရခ
ြင်းကင
်
းဝေးပ
ြီးတ
ော့
မနက်
ဖြန်
တွေတိုင်
းမှ
ာချစ်တ
ဲ့မ
ိသား
စုန
ဲ့ပျော်
ရွှ
င်စွာ
ဖြတ်သ
န်
နိုင
်ပါ
စ
ေမကစ်
😍😍
😍😍
😍

စစ
်ဝ
တ်
ချ
ပ်
မိ
န
်ကိုအပ
ြည့်
ဆင်ယ
င်ထ
ားပြီး
သတ္တဓန
ုလေ
းကြီ
း၏လေ
းမြ
ို့
တွင်
မ
ြား
တစ်ချ
ောင်
းကို
တပ်
ဆင်ကာလေ
းချ
ို့
ကို
ငင
်နေ
သည့်
သမိ
န်စ
က္
ကဝတ်
၏
ရ
ုပ်ပ
ုံ။
အခု
လ
ိုရွှံ့
စ
ေ
းမျ
ားက
ိုရှာဖွေ
ခြင်
းဟာ
မားစ်ပ
ေါ်ကရ
ေမ
ျား
ရဲ
့သမိ
ု
င်
းတစ်
လျှ
ောက်ဖြစ
်တည်ပြောင်
းလဲမ
ှုမ
ျားကိုအသေ
းစိ
တ်သိ
ရှိ
နိုင်မှာ
လည်းဖ
ြစ်ပါ
တယ်
။
နေ
ာက်န
ှစ
်ပေ
ါ
င
်း၅ဘီ
လီယံ
လောက်ကြာရ
င်
ကက
ျွန်တ
ော်
တို
့
နေမင်းကြီ
းကလေ
ာင်စာက
ုန်လ
ို့ပွတ
က်
လာမှ
ာဖြစ
်ပ
ြီး
ကမ
္ဘာ
ကိုလ
ည်းဝ
ါးမြိ
ုသွ
ားမှ
ာဖြ
စ်ပြ
ီးလူ
သား
တို့
အပါအ
ဝင်သက
်ရှိ
များအား
လုံးကိ
ုဖျေ
ာက်ပစ်လ
ိုက
်ပါလိမ့်မ
ယ်။


(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

Updated the code again and check the segmented output:   

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ cat ./10lines.txt.word
စတီရီယို ကဖီး နဲ့ အဆိုတော် အောင် ရင် စကား ဝိုင်း ။
( အပိုင်း - ၁ )
အလုပ် လည်း လုပ် ပညာ လည်း ယူ ချမ်းသာ ရင် တရုတ် ပြည် သွား လည် ရင်မ ကောင်း ဘူး လား ။
ရှင်ရှင် ဒေါ် သထာ ဖြူ ကွယ်လွန် ခြင်း၄၅နှစ်မြောက် နေ့ ပါ လား !
သမ္မတ ဦး ထင် ကျော်
အနိုင်ရ မည့် အသင်း = ပြင် သစ် ဂိုး ရလဒ် = ပြင် သစ်၂ - ၀ခ ရို အေး ရှား
အားပေး မှာ ပါ အရမ်း ချစ် တယ် သာဓု ပါ သာဓု ပါ သာဓု ပါ ဒီ ထက် မက လှူ နိုင် ပါ စေ နော် 👏👏  👏  👏👍 👍👍 အခ ုလ ို ပြ ုရသ ောက ုသိ ု လ်က ောင်းမှ ုတွေကြောင ့်ဘ ဝမှာတော င် းတခ ြင်းနဲ ့ ကြောက ်ရခ ြင်းကင ် းဝေးပ ြီးတ ော့ မနက် ဖြန် တွေတိုင် းမှ ာချစ်တ ဲ့မ ိသား စုန ဲ့ပျော် ရွှ င်စွာ ဖြတ်သ န် နိုင ်ပါ စ ေမကစ် 😍😍 😍😍 😍
စစ်ဝတ် ချပ် မိန် ကို အပြည့် ဆင်ယင် ထား ပြီး သတ္တ ဓနု လေး ကြီး ၏ လေး မြို့ တွင် မြား တစ် ချောင်း ကို တပ် ဆင် ကာ လေး ချို့ ကို ငင် နေ သည့် သ မိန် စက္ကဝတ် ၏ ရုပ်ပုံ ။
အခု လို ရွှံ့စေး များ ကို ရှာဖွေ ခြင်း ဟာ မား စ် ပေါ် က ရေ များ ရဲ့ သမိုင်း တစ်လျှောက် ဖြစ် တည် ပြောင်းလဲ မှု များ ကို အသေးစိတ် သိရှိ နိုင် မှာ လည်း ဖြစ် ပါ တယ် ။
နောက် နှစ် ပေါင်း၅ဘီ လီ ယံ လောက် ကြာ ရင် က ကျွန်တော် တို့ နေမင်း ကြီး ကလောင် စာ ကုန် လို့ ပွ တက် လာ မှာ ဖြစ် ပြီး ကမ္ဘာ ကို လည်း ဝါး မြို သွား မှာ ဖြစ် ပြီး လူသား တို့ အပါအဝင် သက်ရှိ များ အားလုံး ကို ဖျောက်ပစ် လိုက်ပါ လိမ့် မယ် ။
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

Preparing another test file as follows:   

```
ရုပ်သံလိုင်းတိုက်ခိုက်ခံရမှုအပြီးမှာလူဆိုးဂိုဏ်းတွေကိုနှိမ်နင်းမယ်လို့အီကွေဒေါပြော
၁၀ဇန်နဝါရီ၂၀၂၄
အီကွေဒေါနိုင်ငံမှာရုပ်သံတိုက်ရိုက်ထုတ်လွှင့်နေတဲ့စတူရီယိုတစ်ခုထဲကိုမျက်နှာဖုံးစွပ်သေနတ်သမားတွေက ဝင်ရောက်စီးနင်းခဲ့တာကြောင့်ဝန်ထမ်းတွေအထိတ်တလန့်ဖြစ်ခဲ့ကြပါတယ်။
တိုက်ရိုက်ထုတ်လွှင့်မှုကိုမဖြုတ်ချခင်အထိဂွါယာကီးမြို့ကအများပိုင်ရုပ်သံလိုင်းTCရဲ့ဝန်ထမ်းတွေဟာကြမ်းပြင်မှာ ဝမ်းလျားမှောက်ဖို့စေခိုင်းခံခဲ့ရတာကိုလည်းတွေ့ရပါတယ်။
ရဲတပ်ဖွဲ့ကတော့သေနတ်သမားတွေဟာနောက်ပိုင်းမှာဝန်ထမ်းတွေအားလုံးကိုလွှတ်ပေးခဲ့ပြီးလူ၁၃ဦးနဲ့ သေနတ်သမားတွေကိုင်ဆောင်တဲ့လက်နက်တွေကိုဖမ်းဆီးခဲ့တယ်လို့ပြောပါတယ်။
တနင်္လာနေ့ကတည်းကရက်ပေါင်း၆၀အရေးပေါ်အခြေအနေကြေညာထားတဲ့အီကွေဒေါနိုင်ငံမှာအခုဆိုရင်သေဆုံးသူ၁၀ ဦးထက်မနည်းရှိနေပြီဖြစ်ပါတယ်။
နာမည်ဆိုးနဲ့ကျော်ကြားတဲ့လူဆိုးဂိုဏ်းခေါင်းဆောင်တစ်ဦးသူ့ကိုထိန်းသိမ်းထားတဲ့အကျဥ်းထောင်ထဲကနေ လွတ်သွားပြီးတဲ့နောက်မှာအရေးပေါ်အခြေအနေကြေညာထားတာဖြစ်ပါတယ်။ဖီတိုလို့လူသိများတဲ့လော့စ် ချွန်နေးရော့စ်လူဆိုးဂိုဏ်းအဖွဲ့ခေါင်းဆောင်အဒေါ်ဖိုမာစီယက်ဗီလမားလွတ်မြောက်သွားတဲ့ထောင်နဲ့ သေနတ်သမားတွေစီးနင်းတဲ့ရုပ်သံလိုင်းဟာတစ်မြို့တည်းမှာရှိတာဖြစ်ပေမဲ့အခုဖြစ်ရပ်၂ခုဆက်စပ်မှုရှိလားဆိုတာတော့ ရှင်းရှင်းလင်းလင်းမသိရသေးပါဘူး။
အီကွေဒေါအိမ်နီးချင်းပီရူးနိုင်ငံမှာတော့မတည်မငြိမ်ဖြစ်မှုကြောင့်ဖြစ်လာနိုင်ခြေရှိတဲ့နယ်စပ်ဖြတ်ကျော်မှုတွေကိုဟန့်တားနိုင်ဖို့ နှစ်နိုင်ငံနယ်စပ်မှာရဲတပ်ဖွဲ့ကိုချက်ချင်းဖြန့်ကြက်ချထားလိုက်ပြီဖြစ်ပါတယ်။
အမေရိကန်ပြည်ထောင်စုကတော့အီကွေဒေါမှာဖြစ်နေတဲ့အခုလို‘‘ပြောင်ပြောင်တင်းတင်းတိုက်ခိုက်မှုတွေ’’ကို ရှုတ်ချထားပြီးအီကွေဒေါအစိုးရကို‘‘အကူအညီအသင့်ပေးဖို့’’ရပ်တည်နေသလိုအီကွေဒေါသမ္မတဒန်နီယယ်နိုဘာနဲ့ ‘‘နီးနီးကပ်ကပ်ညှိနှိုင်းဆောင်ရွက်နေတယ်’’လို့ပြောထားပါတယ်။
အီကွေဒေါဟာကမ္ဘာမှာငှက်ပျောသီးတင်ပို့တဲ့ထိပ်တန်းနိုင်ငံတွေထဲကတစ်နိုင်ငံဖြစ်သလိုရေနံ၊ကော်ဖီ၊ကိုကာ၊ပုဇွန်နဲ့ ငါးထုတ်ကုန်တွေကိုလည်းတင်ပို့ပါတယ်။အန်ဒီးစ်တောင်တန်းတွေပေါ်မှာရှိတဲ့အီကွေဒေါဟာနိုင်ငံ့အကျဥ်းထောင်တွထဲမှာရော၊ ထောင်တွေရဲ့ပြင်ပမှာပါဖြစ်တဲ့အကြိမ်းဖက်မှုတွေဟာအမေရိကန်နဲ့ ဥရောပကိုသွားတဲ့ကိုကင်းလမ်းကြောင်းတွေကိုထိန်းချုပ်ဖို့ ကြိုးပမ်းရာကနေမူးယစ်ဆေးဂိုဏ်းတွေကြားဖြစ်ပွားတဲ့တိုက်ခိုက်မှုတွေနဲ့ဆက်နွယ်နေပါတယ်။
အင်္ဂါနေ့တုန်းကဖြစ်တဲ့ရုပ်သံထုတ်လွှင့်ရုံတိုက်ခိုက်ခံရမှုမှာသေနတ်သမားတစ်ယောက်ဟာ ကျည်မပြတ်ထိုးနိုင်တဲ့ပြောင်းချောသေနတ်နဲ့ဖမ်းထားသူတစ်ဦးရဲ့‌ခေါင်းကိုချိန်ထားခဲ့ပြီးအဲဒီဖမ်းထားသူဟာ နောက်ထပ်ဆုံလည်သေနတ်တစ်လက်နဲ့လည်းတစ်ချိန်တည်းမှာချိန်ရွယ်ခံခဲ့ရတယ်လို့အေအက်ဖ်ပီသတင်းမှာဖော်ပြပါတယ်။
```

Testing with BBC ll lines data:  

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ cat ./bbc_11_lines.txt
ရုပ်သံလိုင်းတိုက်ခိုက်ခံရမှုအပြီးမှာလူဆိုးဂိုဏ်းတွေကိုနှိမ်နင်းမယ်လို့အီကွေဒေါပြော
၁၀ဇန်နဝါရီ၂၀၂၄
အီကွေဒေါနိုင်ငံမှာရုပ်သံတိုက်ရိုက်ထုတ်လွှင့်နေတဲ့စတူရီယိုတစ်ခုထဲကိုမျက်နှာဖုံးစွပ်သေနတ်သမားတွေက ဝင်ရောက်စီးနင်းခဲ့တာကြောင့်ဝန်ထမ်းတွေအထိတ်တလန့်ဖြစ်ခဲ့ကြပါတယ်။
တိုက်ရိုက်ထုတ်လွှင့်မှုကိုမဖြုတ်ချခင်အထိဂွါယာကီးမြို့ကအများပိုင်ရုပ်သံလိုင်းTCရဲ့ဝန်ထမ်းတွေဟာကြမ်းပြင်မှာ ဝမ်းလျားမှောက်ဖို့စေခိုင်းခံခဲ့ရတာကိုလည်းတွေ့ရပါတယ်။
ရဲတပ်ဖွဲ့ကတော့သေနတ်သမားတွေဟာနောက်ပိုင်းမှာဝန်ထမ်းတွေအားလုံးကိုလွှတ်ပေးခဲ့ပြီးလူ၁၃ဦးနဲ့ သေနတ်သမားတွေကိုင်ဆောင်တဲ့လက်နက်တွေကိုဖမ်းဆီးခဲ့တယ်လို့ပြောပါတယ်။
တနင်္လာနေ့ကတည်းကရက်ပေါင်း၆၀အရေးပေါ်အခြေအနေကြေညာထားတဲ့အီကွေဒေါနိုင်ငံမှာအခုဆိုရင်သေဆုံးသူ၁၀ ဦးထက်မနည်းရှိနေပြီဖြစ်ပါတယ်။
နာမည်ဆိုးနဲ့ကျော်ကြားတဲ့လူဆိုးဂိုဏ်းခေါင်းဆောင်တစ်ဦးသူ့ကိုထိန်းသိမ်းထားတဲ့အကျဥ်းထောင်ထဲကနေ လွတ်သွားပြီးတဲ့နောက်မှာအရေးပေါ်အခြေအနေကြေညာထားတာဖြစ်ပါတယ်။ဖီတိုလို့လူသိများတဲ့လော့စ် ချွန်နေးရော့စ်လူဆိုးဂိုဏ်းအဖွဲ့ခေါင်းဆောင်အဒေါ်ဖိုမာစီယက်ဗီလမားလွတ်မြောက်သွားတဲ့ထောင်နဲ့ သေနတ်သမားတွေစီးနင်းတဲ့ရုပ်သံလိုင်းဟာတစ်မြို့တည်းမှာရှိတာဖြစ်ပေမဲ့အခုဖြစ်ရပ်၂ခုဆက်စပ်မှုရှိလားဆိုတာတော့ ရှင်းရှင်းလင်းလင်းမသိရသေးပါဘူး။
အီကွေဒေါအိမ်နီးချင်းပီရူးနိုင်ငံမှာတော့မတည်မငြိမ်ဖြစ်မှုကြောင့်ဖြစ်လာနိုင်ခြေရှိတဲ့နယ်စပ်ဖြတ်ကျော်မှုတွေကိုဟန့်တားနိုင်ဖို့ နှစ်နိုင်ငံနယ်စပ်မှာရဲတပ်ဖွဲ့ကိုချက်ချင်းဖြန့်ကြက်ချထားလိုက်ပြီဖြစ်ပါတယ်။
အမေရိကန်ပြည်ထောင်စုကတော့အီကွေဒေါမှာဖြစ်နေတဲ့အခုလို‘‘ပြောင်ပြောင်တင်းတင်းတိုက်ခိုက်မှုတွေ’’ကို ရှုတ်ချထားပြီးအီကွေဒေါအစိုးရကို‘‘အကူအညီအသင့်ပေးဖို့’’ရပ်တည်နေသလိုအီကွေဒေါသမ္မတဒန်နီယယ်နိုဘာနဲ့ ‘‘နီးနီးကပ်ကပ်ညှိနှိုင်းဆောင်ရွက်နေတယ်’’လို့ပြောထားပါတယ်။
အီကွေဒေါဟာကမ္ဘာမှာငှက်ပျောသီးတင်ပို့တဲ့ထိပ်တန်းနိုင်ငံတွေထဲကတစ်နိုင်ငံဖြစ်သလိုရေနံ၊ကော်ဖီ၊ကိုကာ၊ပုဇွန်နဲ့ ငါးထုတ်ကုန်တွေကိုလည်းတင်ပို့ပါတယ်။အန်ဒီးစ်တောင်တန်းတွေပေါ်မှာရှိတဲ့အီကွေဒေါဟာနိုင်ငံ့အကျဥ်းထောင်တွထဲမှာရော၊ ထောင်တွေရဲ့ပြင်ပမှာပါဖြစ်တဲ့အကြိမ်းဖက်မှုတွေဟာအမေရိကန်နဲ့ ဥရောပကိုသွားတဲ့ကိုကင်းလမ်းကြောင်းတွေကိုထိန်းချုပ်ဖို့ ကြိုးပမ်းရာကနေမူးယစ်ဆေးဂိုဏ်းတွေကြားဖြစ်ပွားတဲ့တိုက်ခိုက်မှုတွေနဲ့ဆက်နွယ်နေပါတယ်။
အင်္ဂါနေ့တုန်းကဖြစ်တဲ့ရုပ်သံထုတ်လွှင့်ရုံတိုက်ခိုက်ခံရမှုမှာသေနတ်သမားတစ်ယောက်ဟာ ကျည်မပြတ်ထိုးနိုင်တဲ့ပြောင်းချောသေနတ်နဲ့ဖမ်းထားသူတစ်ဦးရဲ့‌ခေါင်းကိုချိန်ထားခဲ့ပြီးအဲဒီဖမ်းထားသူဟာ နောက်ထပ်ဆုံလည်သေနတ်တစ်လက်နဲ့လည်းတစ်ချိန်တည်းမှာချိန်ရွယ်ခံခဲ့ရတယ်လို့အေအက်ဖ်ပီသတင်းမှာဖော်ပြပါတယ်။
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ cat bbc_11_lines.txt.word
ရုပ် သံ လိုင်း တိုက်ခိုက် ခံ ရ မှု အပြီး မှာ လူဆိုး ဂိုဏ်း တွေ ကို နှိမ်နင်း မယ် လို့ အီ ကွေ ဒေါ ပြော
၁၀ဇန်နဝါရီ၂၀၂၄
အီ ကွေ ဒေါ နိုင်ငံ မှာ ရုပ် သံ တိုက်ရိုက် ထုတ် လွှင့် နေ တဲ့ စ တူ ရီ ယို တစ် ခု ထဲ ကို မျက်နှာဖုံး စွပ် သေနတ် သမား တွေ က ဝင် ရောက် စီးနင်း ခဲ့ တာ ကြောင့် ဝန်ထမ်း တွေ အထိတ်တလန့် ဖြစ် ခဲ့ ကြ ပါ တယ် ။
တိုက်ရိုက် ထုတ် လွှင့် မှု ကို မ ဖြုတ် ချ ခင် အ ထိ ဂွါ ယာ ကီး မြို့ က အများ ပိုင် ရုပ် သံ လိုင်းTCရဲ့ ဝန်ထမ်း တွေ ဟာ ကြမ်းပြင် မှာ ဝမ်းလျားမှောက် ဖို့ စေခိုင်း ခံ ခဲ့ ရ တာ ကို လည်း တွေ့ ရ ပါ တယ် ။
ရဲတပ်ဖွဲ့ ကတော့ သေနတ် သမား တွေ ဟာ နောက်ပိုင်း မှာ ဝန်ထမ်း တွေ အားလုံး ကို လွှတ်ပေး ခဲ့ ပြီး လူ၁၃ဦး နဲ့ သေနတ် သမား တွေ ကိုင် ဆောင် တဲ့ လက်နက် တွေ ကို ဖမ်းဆီး ခဲ့ တယ် လို့ ပြော ပါ တယ် ။
တနင်္လာနေ့ ကတည်းက ရက် ပေါင်း၆၀အရေး ပေါ် အခြေအနေ ကြေညာ ထား တဲ့ အီ ကွေ ဒေါ နိုင်ငံ မှာ အခု ဆို ရင် သေဆုံး သူ၁၀ ဦး ထက် မနည်း ရှိ နေ ပြီ ဖြစ် ပါ တယ် ။
နာမည်ဆိုး နဲ့ ကျော်ကြား တဲ့ လူဆိုး ဂိုဏ်း ခေါင်းဆောင် တစ် ဦး သူ့ ကို ထိန်းသိမ်း ထား တဲ့ အ ကျ ဥ်း ထောင် ထဲ က နေ လွတ် သွား ပြီး တဲ့ နောက် မှာ အရေး ပေါ် အခြေအနေ ကြေညာ ထား တာ ဖြစ် ပါ တယ် ။ ဖီ တို လို့ လူ သိ များ တဲ့ လော့ စ် ချွန် နေး ရော့ စ် လူဆိုး ဂိုဏ်း အဖွဲ့ ခေါင်းဆောင် အဒေါ် ဖို မာ စီ ယက် ဗီ လ မား လွတ်မြောက် သွား တဲ့ ထောင် နဲ့ သေနတ် သမား တွေ စီးနင်း တဲ့ ရုပ် သံ လိုင်း ဟာ တစ် မြို့ တည်း မှာ ရှိ တာ ဖြစ် ပေ မဲ့ အခု ဖြစ်ရပ်၂ခု ဆက်စပ် မှု ရှိ လား ဆို တာ တော့ ရှင်းရှင်းလင်းလင်း မ သိ ရ သေးပါ ဘူး ။
အီ ကွေ ဒေါ အိမ်နီးချင်း ပီ ရူး နိုင်ငံ မှာ တော့ မ တည် မ ငြိမ် ဖြစ် မှု ကြောင့် ဖြစ်လာ နိုင်ခြေ ရှိ တဲ့ နယ်စပ် ဖြတ် ကျော် မှု တွေ ကို ဟန့်တား နိုင် ဖို့ နှစ် နိုင်ငံ နယ်စပ် မှာ ရဲတပ်ဖွဲ့ ကို ချက်ချင်း ဖြန့်ကြက် ချထား လိုက် ပြီ ဖြစ် ပါ တယ် ။
အ မေ ရိ ကန် ပြည်ထောင်စု ကတော့ အီ ကွေ ဒေါ မှာ ဖြစ် နေ တဲ့ အခု လို ‘ ‘ ပြောင်ပြောင်တင်းတင်း တိုက်ခိုက် မှု တွေ ’ ’ ကို ရှုတ်ချ ထား ပြီး အီ ကွေ ဒေါ အစိုးရ ကို ‘ ‘ အကူအညီ အသင့် ပေး ဖို့ ’ ’ ရပ်တည် နေ သလို အီ ကွေ ဒေါ သမ္မတ ဒန် နီ ယယ် နို ဘာ နဲ့ ‘ ‘ နီး နီးကပ် ကပ် ညှိနှိုင်း ဆောင်ရွက် နေ တယ် ’ ’ လို့ ပြောထား ပါ တယ် ။
အီ ကွေ ဒေါ ဟာ ကမ္ဘာ မှာ ငှက်ပျောသီး တင် ပို့ တဲ့ ထိပ်တန်း နိုင်ငံ တွေ ထဲ က တစ်နိုင် ငံ ဖြစ် သလို ရေနံ ၊ ကော်ဖီ ၊ ကို ကာ ၊ ပု ဇွန် နဲ့ ငါး ထုတ်ကုန် တွေ ကို လည်း တင် ပို့ ပါ တယ် ။ အန် ဒီး စ် တောင်တန်း တွေ ပေါ် မှာ ရှိ တဲ့ အီ ကွေ ဒေါ ဟာ နိုင် ငံ့ အ ကျ ဥ်း ထောင် တွ ထဲ မှာ ရော ၊ ထောင် တွေ ရဲ့ ပြင် ပ မှာ ပါ ဖြစ် တဲ့ အ ကြိမ်း ဖက် မှု တွေ ဟာ အ မေ ရိ ကန် နဲ့ ဥ ရော ပ ကို သွား တဲ့ ကိုကင်း လမ်းကြောင်း တွေ ကို ထိန်းချုပ် ဖို့ ကြိုးပမ်း ရာ က နေ မူးယစ် ဆေး ဂိုဏ်း တွေ ကြား ဖြစ်ပွား တဲ့ တိုက်ခိုက် မှု တွေ နဲ့ ဆက်နွယ် နေ ပါ တယ် ။
အင်္ဂါနေ့ တုန်း က ဖြစ် တဲ့ ရုပ် သံ ထုတ် လွှင့် ရုံ တိုက်ခိုက် ခံ ရ မှု မှာ သေနတ် သမား တစ် ယောက် ဟာ ကျည် မပြတ် ထိုး နိုင် တဲ့ ပြောင်း ချော သေနတ် နဲ့ ဖမ်းထား သူ တစ် ဦး ရဲ့‌ခေါင်း ကို ချိန် ထားခဲ့ ပြီး အဲဒီ ဖမ်းထား သူ ဟာ နောက်ထပ် ဆုံလည် သေနတ် တစ် လက် နဲ့ လည်း တစ် ချိန် တည်း မှာ ချိန် ရွယ် ခံ ခဲ့ ရ တယ် လို့ အေ အ က် ဖ် ပီသ တင်း မှာ ဖော်ပြ ပါ တယ် ။
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

Check spelling ...  

```
အ ကျ ဥ်း ထောင် 
correct word should be: အကျဉ်းထောင်
```


Confirmation as follows:   

```
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$ echo "အီကွေဒေါနိုင်ငံ့အကျဉ်းထောင်" | python ./icu_word_tokenizer.py --dictionary ../data/myg2p.f2
အီ ကွေ ဒေါ နိုင် ငံ့ အကျဉ်းထောင်
(base) ye@lst-gpu-3090:~/exp/myNLP/icu_tool$
```

Yes, working well. If we filled with name dictionary, the performance will better.  




