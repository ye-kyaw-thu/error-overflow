# Language Detection for Languages of Myanmar (Experiment Log)

## Data Info

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/char_seg$ ls
beik.all.char   mon.all.char  po_kayin.all.char  segmentation-data-updated2.cleaned.syl  shan.all.char
dawei.all.char  pao.all.char  rakhine.all.char   sgaw_kayin.all.char
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/char_seg$
```

myWord data used for Bamar. Later I changed bamar.syl

## Revisiting Language Detection

ပထမဆုံး လုပ်ကြည့်ခဲ့တာက character based, syllable based ngram-LM ကို သုံးပြီးတော့ အဆင်မပြေဘူး ဖြစ်နေတာ အဲဒါကို ဒီနေ့ ပြန်စမ်းဖြစ်ခဲ့ ...  

Date: 20 Jan 2024  

I regenerate all syllable profiles again. Mainly, I changed input text for Burmese. For this time, I used Khin War War Htaik's my of zh-my dataset.  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ time ./generate_syl_profile.sh /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/beik.all.syl --ngram 3 --output ./syl_profile/beik.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/dawei.all.syl --ngram 3 --output ./syl_profile/dawei.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/mon.all.syl --ngram 3 --output ./syl_profile/mon.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/MyanmarTotal.my.clean.nosymbol.syl --ngram 3 --output ./syl_profile/MyanmarTotal.my.clean.nosymbol.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/pao.all.syl --ngram 3 --output ./syl_profile/pao.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/po_kayin.all.syl --ngram 3 --output ./syl_profile/po_kayin.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/rakhine.all.syl --ngram 3 --output ./syl_profile/rakhine.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/sgaw_kayin.all.syl --ngram 3 --output ./syl_profile/sgaw_kayin.all.syl.profile
Running: python ./language_detection.py --create_profile --input /home/ye/exp/sylbreak4all/lang_detection/lang_data/syl_seg/shan.all.syl --ngram 3 --output ./syl_profile/shan.all.syl.profile

real	0m3.737s
user	0m3.086s
sys	0m0.452s
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ ls ./syl_profile/
beik.all.syl.profile   MyanmarTotal.my.clean.nosymbol.syl.profile  rakhine.all.syl.profile
dawei.all.syl.profile  pao.all.syl.profile                         sgaw_kayin.all.syl.profile
mon.all.syl.profile    po_kayin.all.syl.profile                    shan.all.syl.profile
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$ wc *
   32997   131988  1706204 beik.all.syl.profile
   36481   145924  1959980 dawei.all.syl.profile
   58708   234832  3133439 mon.all.syl.profile
  302028  1208112 16269222 MyanmarTotal.my.clean.nosymbol.syl.profile
  112073   448292  6415454 pao.all.syl.profile
   91064   364256  4398675 po_kayin.all.syl.profile
   87738   350952  4407056 rakhine.all.syl.profile
  204543   818172 10317889 sgaw_kayin.all.syl.profile
  109143   436572  6672376 shan.all.syl.profile
 1034775  4139100 55280295 total
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$
```

I changed filename:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$ ls
bamar.syl.profile      mon.all.syl.profile       rakhine.all.syl.profile
beik.all.syl.profile   pao.all.syl.profile       sgaw_kayin.all.syl.profile
dawei.all.syl.profile  po_kayin.all.syl.profile  shan.all.syl.profile
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$ 
```

## Test-Run with Syllable LM

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ time ./detect_all.sh ./eg_input/
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//bamar_burmese.txt --profile ./syl_profile/
beik.all.syl: 79.94%
bamar.syl: 18.09%
dawei.all.syl: 0.60%
pao.all.syl: 0.15%
po_kayin.all.syl: 0.15%
sgaw_kayin.all.syl: 0.03%
mon.all.syl: 0.15%
shan.all.syl: 0.15%
rakhine.all.syl: 0.73%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//beik.txt --profile ./syl_profile/
beik.all.syl: 100.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//dawei.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 100.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//mon_tst.txt --profile ./syl_profile/
beik.all.syl: 11.47%
bamar.syl: 11.47%
dawei.all.syl: 11.47%
pao.all.syl: 11.47%
po_kayin.all.syl: 11.47%
sgaw_kayin.all.syl: 11.47%
mon.all.syl: 8.26%
shan.all.syl: 11.47%
rakhine.all.syl: 11.47%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//mon.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 100.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//pao.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 100.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//po_kayin.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 100.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//rakhine.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 100.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//sgaw_kayin.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 100.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//shan.txt --profile ./syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 100.00%
rakhine.all.syl: 0.00%

real	0m7.317s
user	0m6.395s
sys	0m0.844s
```

## Check the Input Data

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat bamar_burmese.txt 
နေ ကောင်း လား
ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
မင်္ဂ လာ ပါ ဆ ရာ မ
တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
ကျောင်း သား ကျောင်း သွား ပါ
က လေး က အိမ် မှာ ပါ
ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat dawei.txt 
ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat mon.txt 
ဗှ်ေ ဟယျ တုဲ မာန်ဟာ ။
ယဝ်ဗှ်ေ ဟွံပယှုက် အဲ ရတှ်ေ တုဲမာန်ဏောၚ် ။
အဲ ဟယျ ဗှ်ေ တိၚ်ဂီတာ လေပ်မံၚ် ။
လၟုဟ် အဲ ဗ္တောန် တိၚ်မံၚ် ဂီတာ ။
ပေါဲဂီတဂှ် ဂိတု ဂတမှ ကၠောန်ဏောၚ် ။
သွက်အဲ ဂွံအံၚ်ဇၞး ရာဒနာ ကဵုညိ ။
ခိုဟ်ယျ ဆက်ဂစာန် ညိပၠန် ။
ဂလာန် ဗှ်ေ ပတိုန်လဝ် နူဏေအ်ဗ္တံဂှ် ခိုဟ်ကွေံကွေံ။
ၜိုတ်အဲ ကၠောန်မာန် အဲဂစာန် လဝ်ရ။
ပ္ဍဲဗှ်ေဂှ် ကသပ် တၟေၚ်ၚ် နွံမံၚ်။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat po_kayin.txt 
ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat sgaw_kayin.txt 
တၢ်ဝဲန့ၣ်နတဘျးစဲဒီးအဂၤတခါဧဲၣ်.
ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
ပျဲတၢ်မၤစၢၤတက့ၢ်.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat beik.txt 
ဖယ် သူ လေ ကို မေး ရိ လဲ ။
သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat mon.txt 
ဗှ်ေ ဟယျ တုဲ မာန်ဟာ ။
ယဝ်ဗှ်ေ ဟွံပယှုက် အဲ ရတှ်ေ တုဲမာန်ဏောၚ် ။
အဲ ဟယျ ဗှ်ေ တိၚ်ဂီတာ လေပ်မံၚ် ။
လၟုဟ် အဲ ဗ္တောန် တိၚ်မံၚ် ဂီတာ ။
ပေါဲဂီတဂှ် ဂိတု ဂတမှ ကၠောန်ဏောၚ် ။
သွက်အဲ ဂွံအံၚ်ဇၞး ရာဒနာ ကဵုညိ ။
ခိုဟ်ယျ ဆက်ဂစာန် ညိပၠန် ။
ဂလာန် ဗှ်ေ ပတိုန်လဝ် နူဏေအ်ဗ္တံဂှ် ခိုဟ်ကွေံကွေံ။
ၜိုတ်အဲ ကၠောန်မာန် အဲဂစာန် လဝ်ရ။
ပ္ဍဲဗှ်ေဂှ် ကသပ် တၟေၚ်ၚ် နွံမံၚ်။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat pao.txt 
နဝ်ꩻနဝ်ꩻ နာꩻ တ အွဉ်ႏဖွို့ꩻ တဝ်းဟောင်း တွမ်ႏ အလင် တဗာႏ
ဝွေꩻမူႏ တ တောင်ချာတဝ်းဒွုမ် ပါꩻမုဲင်ꩻမုဲင်ꩻ
နဝ်ꩻနဝ်ꩻ နီ အတာႏ ယပ်ခုဲင်ႏငါႏ
နာꩻ ကဒေါ့ꩻ အတွိုင်ꩻ ခွေ သျင်ꩻပျ ဗာႏဒျာႏ
ကထိန်ꩻ‌နွောင်ꩻ ဝွေꩻနဝ်ꩻ အဝ်ႏဒျာႏ နာꩻ လွုမ်
နဝ်ꩻနဝ်ꩻ ခွေ ယမ်း မာႏဗာႏဟောင်း
ခွေ စဥ်ꩻစာꩻ အတွိုင်ꩻ စဥ်ꩻစာꩻဟုဲင်း
ဒေါ့ꩻဝင်ꩻမဉ်ꩻ နဝ်ꩻ လွထီႏငါႏ
ဆုဲင်ꩻသွတ် တ လဲင်ႏ ရက်ဒျာႏ ဝွေꩻနဝ်ꩻ တဲ့ ဒေါ့ꩻခွင်ꩻ တ လ တဝ်းဒွုမ်
တယ်ႏ နာဆာ ဒုံးပျံ ထင်ႏစခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏဒျာႏ မတ်တန်ꩻ
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat rakhine.txt 
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ cat shan.txt
မႂ်း လွင်ႈၼႆႉ လၢတ်ႈမႃး ႁိုဝ် ဢမ်ႇလၢတ်ႈမႃး ႁႃႉ ။
တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေလႆႈ ဢဝ် ပပ်ႉလႂ် ။
တွင်းပၢၼ်ႇၵဝ် ဢမ်ႇ တွင်းပၢၼ်ႇ ၵဝ် ။
ဢရသႃႇ မၼ်းတႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉဝၢၼ်ႇ ဝႆႉ ။
မိူဝ်ႈပူၼ်ႉ မႃး ဝၼ်းသုၵ်း ၵၢင်ၼႂ် ႑႑ မွင်း ၼၼ်ႉ သူ  မီးယူႇ တီႈလႂ် ။
ဢၼ်ၼႆႉ တႃႇမၼ်း ယၢပ်ႇ ဢိူဝ်ႈ ။
ဢမ်ႇမီး ၶပ်းမၢႆ တႃႇဢွၵ်ႇပၢႆႈ ႁႃႉ ။
တႃႇမၼ်းၼၢင်း ႁဝ်းတေ ထၢမ် ဢမ်ႇ ၸႂ်ႈ ။
ႁဝ်း မိူဝ်ႈၽုၵ်ႈ ၵၢင်ၼႂ် တေဢွၵ်ႇပႆတၢင်း ဢိူဝ်ႈ ။
ဢမ်ႇ မူတ်းသႂ် ႁႃႉ ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$
```

## Check the Current Profiles

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$ head -n 30 *.profile
==> bamar.syl.profile <==
နေ က မီး	1.5227715866140115e-06
က မီး ကျီး	1.5227715866140115e-06
မီး ကျီး ခဲ	1.5227715866140115e-06
ကျီး ခဲ လို	1.5227715866140115e-06
ခဲ လို ရဲ	1.5227715866140115e-06
လို ရဲ ရဲ	3.030466226825904e-06
ရဲ ရဲ တောက်	4.538160867037796e-06
ရဲ တောက် ပြီး	1.5227715866140115e-06
တောက် ပြီး တက်	1.5227715866140115e-06
ပြီး တက် လာ	1.5227715866140115e-06
တက် လာ တယ်	2.5645885830004295e-05
လာ တယ် ပြီး	1.8107412628944828e-05
တယ် ပြီး တော့	0.0004025695458829774
ပြီး တော့ ငါ	7.992289287763242e-05
တော့ ငါ တို့	5.579977863424214e-05
ငါ တို့ ရပ်	4.538160867037796e-06
တို့ ရပ် နိုင်	1.5227715866140115e-06
ရပ် နိုင် ရုံ	1.5227715866140115e-06
နိုင် ရုံ လောက်	1.5227715866140115e-06
ရုံ လောက် ပဲ	3.030466226825904e-06
လောက် ပဲ ရှိ	1.6599717988732936e-05
ပဲ ရှိ ပေ	1.5227715866140115e-06
ရှိ ပေ မဲ့	1.6599717988732936e-05
ပေ မဲ့ အ	0.00011912295352314163
မဲ့ အ ခု	1.5092023348521044e-05
အ ခု ဘယ်	4.52459161527589e-05
ခု ဘယ် နည်း	1.5227715866140115e-06
ဘယ် နည်း နဲ့	1.0568939427885366e-05
နည်း နဲ့ မ	6.045855507249689e-06
နဲ့ မ ဆို	9.061244787673474e-06

==> beik.all.syl.profile <==
နင် ဘာ စီ	4.400329396086221e-05
ဘာ စီ စဉ်	4.400329396086221e-05
စီ စဉ် နေ	1.4765224883877354e-05
စဉ် နေ ရယ်	1.4765224883877354e-05
နေ ရယ် ဆို	0.00013171750119181678
ရယ် ဆို တာ	0.0002632888120382487
ဆို တာ ငါ့	1.4765224883877354e-05
တာ ငါ့ ဝို	1.4765224883877354e-05
ငါ့ ဝို ပြော	4.400329396086221e-05
ဝို ပြော သင့်	1.4765224883877354e-05
ပြော သင့် ပေါ့	1.4765224883877354e-05
သင့် ပေါ့ လန်း	2.938425942236978e-05
ပေါ့ လန်း ။	7.324136303784707e-05
လန်း ။ သူ	0.0003363839847307108
။ သူ လို့	0.001637478058656537
သူ လို့ စာ	1.4765224883877354e-05
လို့ စာ အုပ်	2.938425942236978e-05
စာ အုပ် သုံး	2.938425942236978e-05
အုပ် သုံး ထောင်	1.4765224883877354e-05
သုံး ထောင် ကျော်	1.4765224883877354e-05
ထောင် ကျော် ရောင်း	1.4765224883877354e-05
ကျော် ရောင်း ပီး	1.4765224883877354e-05
ရောင်း ပီး ဟော	1.4765224883877354e-05
ပီး ဟော ဘီ	1.4765224883877354e-05
ဟော ဘီ ။	1.4765224883877354e-05
ဘီ ။ ငယ်	1.4765224883877354e-05
။ ငယ် ငယ်	2.938425942236978e-05
ငယ် ငယ် တည်း	2.938425942236978e-05
ငယ် တည်း က	2.938425942236978e-05
တည်း က မင်း	2.938425942236978e-05

==> dawei.all.syl.profile <==
နန် ဟှဲ ဇာ	0.001094696012191491
ဟှဲ ဇာ စီ	1.4939102449850099e-05
ဇာ စီ စဉ်	1.4939102449850099e-05
စီ စဉ် နေ	1.4939102449850099e-05
စဉ် နေ ဟှယ်	1.4939102449850099e-05
နေ ဟှယ် ဆို	0.0002663893417047528
ဟှယ် ဆို တာ	0.000355136484971189
ဆို တာ ငါ့	1.4939102449850099e-05
တာ ငါ့ ကို	1.4939102449850099e-05
ငါ့ ကို ပြော	1.4939102449850099e-05
ကို ပြော သင့်	1.4939102449850099e-05
ပြော သင့် ဟှယ်	2.9730292994256134e-05
သင့် ဟှယ် ။	0.0003255541038823769
ဟှယ် ။ သူး	0.0013017726798131755
။ သူး နို့	0.004245219598149977
သူး နို့ စာ	2.9730292994256134e-05
နို့ စာ အုပ်	1.4939102449850099e-05
စာ အုပ် သုံး	2.9730292994256134e-05
အုပ် သုံး ထော်	1.4939102449850099e-05
သုံး ထော် ကျော်	1.4939102449850099e-05
ထော် ကျော် ရော	1.4939102449850099e-05
ကျော် ရော ပီး	1.4939102449850099e-05
ရော ပီး ပီ	1.4939102449850099e-05
ပီး ပီ ။	0.00011847743626069236
ပီ ။ ချို့	1.4939102449850099e-05
။ ချို့ လူ	2.9730292994256134e-05
ချို့ လူ လေ	4.452148353866217e-05
လူ လေ ဟှာ	4.452148353866217e-05
လေ ဟှာ မွီး	2.9730292994256134e-05
ဟှာ မွီး ရာ	2.9730292994256134e-05

==> mon.all.syl.profile <==
၂ ၀ မိ	2.7112945143215798e-05
၀ မိ ဏေတ်	9.09769920087972e-06
မိ ဏေတ် ပၠန်	9.09769920087972e-06
ဏေတ် ပၠန် တှ်ေ	9.09769920087972e-06
ပၠန် တှ်ေ ဘာ	9.09769920087972e-06
တှ်ေ ဘာ ရပ်	9.09769920087972e-06
ဘာ ရပ် ဏောၚ်	9.09769920087972e-06
ရပ် ဏောၚ် ။	9.09769920087972e-06
ဏောၚ် ။ ဗှ်ေ	0.00011718917485489619
။ ဗှ်ေ ဟ	1.8105322172047758e-05
ဗှ်ေ ဟ ယျ	4.512819108555188e-05
ဟ ယျ တုဲ	9.09769920087972e-06
ယျ တုဲ မာန်	9.09769920087972e-06
တုဲ မာန် ဟာ	9.09769920087972e-06
မာန် ဟာ ။	0.0007026846679808188
ဟာ ။ ယဝ်	2.7112945143215798e-05
။ ယဝ် ဗှ်ေ	9.09769920087972e-06
ယဝ် ဗှ်ေ ဟွံ	9.09769920087972e-06
ဗှ်ေ ဟွံ ပ	9.016630594139208e-05
ဟွံ ပ ယှုက်	2.7112945143215798e-05
ပ ယှုက် အဲ	1.8105322172047758e-05
ယှုက် အဲ ရ	1.8105322172047758e-05
အဲ ရ တှ်ေ	9.09769920087972e-06
ရ တှ်ေ တုဲ	9.09769920087972e-06
တှ်ေ တုဲ မာန်	9.09769920087972e-06
တုဲ မာန် ဏောၚ်	9.09769920087972e-06
မာန် ဏောၚ် ။	0.000306349257249425
ဏောၚ် ။ အဲ	0.0007026846679808188
။ အဲ ဟ	3.612056811438384e-05
အဲ ဟ ယျ	4.512819108555188e-05

==> pao.all.syl.profile <==
လို မူႏ ပေႏ	0.00011767805007096772
မူႏ ပေႏ မာꩻ	5.400037736105288e-06
ပေႏ မာꩻ တ	1.609318176799695e-05
မာꩻ တ မုဲင်ꩻ	0.0003956997949001509
တ မုဲင်ꩻ ဟောင်း	0.0015291730622806667
မုဲင်ꩻ ဟောင်း ဝွေꩻ	0.0007753064080323048
ဟောင်း ဝွေꩻ သီး	0.0009303569964947339
ဝွေꩻ သီး အီး	0.0006309489636017674
သီး အီး ကွီႏ	5.400037736105288e-06
အီး ကွီႏ သ	5.400037736105288e-06
ကွီႏ သ ညင်ꩻ	5.400037736105288e-06
သ ညင်ꩻ နာꩻ	5.400037736105288e-06
ညင်ꩻ နာꩻ တ	5.400037736105288e-06
နာꩻ တ မွေး	0.0001871834862782635
တ မွေး တဝ်း	0.002336505436688487
မွေး တဝ်း နီ	0.00010163833402313023
တဝ်း နီ တ	4.817261386367193e-05
နီ တ ယူႏ	5.400037736105288e-06
တ ယူႏ လ	2.1439753783942778e-05
ယူႏ လ တဝ်း	5.886575789556359e-05
လ တဝ်း ခင်ႏ	1.609318176799695e-05
တဝ်း ခင်ႏ လမ်း	4.817261386367193e-05
ခင်ႏ လမ်း နဝ်ꩻ	0.00013371776611880522
လမ်း နဝ်ꩻ နာꩻ	5.400037736105288e-06
နဝ်ꩻ နာꩻ ပါꩻ	1.0746609752051117e-05
နာꩻ ပါꩻ မုဲင်ꩻ	2.1439753783942778e-05
ပါꩻ မုဲင်ꩻ မန်	5.400037736105288e-06
မုဲင်ꩻ မန် နေ	5.400037736105288e-06
မန် နေ ဂျာ	0.0001123314780550219
နေ ဂျာ ဟောင်း	1.0746609752051117e-05

==> po_kayin.all.syl.profile <==
န ဂဲၫ ထဲၩ့	0.0008742438370074405
ဂဲၫ ထဲၩ့ မၩ	0.0004626053136846808
ထဲၩ့ မၩ ဆၧ	0.00012310962434632227
မၩ ဆၧ လ	5.521048647865056e-05
ဆၧ လ ဖၪ	0.00013159701657978123
လ ဖၪ အ	0.00028861377289877207
ဖၪ အ ဂး	3.823570201173263e-05
အ ဂး န	0.000182521369980535
ဂး န နီၪ့	4.286133077896777e-06
န နီၪ့ ယါ	8.529829194626257e-06
နီၪ့ ယါ လၩ့	1.701722142808522e-05
ယါ လၩ့ န	8.529829194626257e-06
လၩ့ န ၥၭ	0.00012310962434632227
န ၥၭ အ့ၬ	9.764744764594537e-05
ၥၭ အ့ၬ ဧၪ	0.00010613483987940434
အ့ၬ ဧၪ ယ	0.0006026472855367536
ဧၪ ယ ခိၭ	1.277352531135574e-05
ယ ခိၭ နၧၩ	4.286133077896777e-06
ခိၭ နၧၩ လၧ	8.529829194626257e-06
နၧၩ လၧ ယ	1.701722142808522e-05
လၧ ယ က	0.00029285746901550156
ယ က ကိၭ	7.642896706229796e-05
က ကိၭ ဖံၭ	4.286133077896777e-06
ကိၭ ဖံၭ ၥိၭ	5.521048647865056e-05
ဖံၭ ၥိၭ နၧၩ	1.701722142808522e-05
ၥိၭ နၧၩ အ	4.286133077896777e-06
နၧၩ အ ဂး	2.9748309778273664e-05
အ ဂး လီၫ	0.0004668490098014103
ဂး လီၫ မ	1.701722142808522e-05
လီၫ မ နီၪ	2.5504613661544182e-05

==> rakhine.all.syl.profile <==
မင်း ယင်း ချင့်	0.0003527139187767928
ယင်း ချင့် ကို	0.0030321526628073
ချင့် ကို အ	0.000167776734196838
ကို အ ခြား	4.3438734052501e-06
အ ခြား တစ်	8.644738162923465e-06
ခြား တစ် ခု	1.72464676782702e-05
တစ် ခု နန့်	1.2945602920596831e-05
ခု နန့် မ	4.3438734052501e-06
နန့် မ ချိတ်	4.3438734052501e-06
မ ချိတ် ပါ	4.3438734052501e-06
ချိတ် ပါ လား	4.3438734052501e-06
ပါ လား ။	0.006180385665424204
လား ။ ထို	0.0008000038535748228
။ ထို မ	0.003797706589673159
ထို မ ချေ	0.005449238656619732
မ ချေ တစ်	6.88568447703506e-05
ချေ တစ် ယောက်	0.00012906895137777772
တစ် ယောက် လေ့	0.0002064845170158983
ယောက် လေ့ မ	0.0001075646275894109
လေ့ မ မှတ်	8.644738162923465e-06
မ မှတ် မိ	0.00011616635710475763
မှတ် မိ ပါ	9.036116855871744e-05
မိ ပါ ယာ	8.644738162923465e-06
ပါ ယာ ။	0.0003226078654730792
ယာ ။ ယင်း	6.455598001267723e-05
။ ယင်း ချင့်	0.002270899600699114
ယင်း ချင့် ကျွန်	6.455598001267723e-05
ချင့် ကျွန် တော်	2.5848197193616932e-05
ကျွန် တော် ရို့	0.0031095682284454206
တော် ရို့ အ	0.0002580948941079787

==> sgaw_kayin.all.syl.profile <==
န ဘၣ် သံ	3.5624403416993355e-06
ဘၣ် သံ ကွၢ်	7.812514516796451e-05
သံ ကွၢ် တၢ်	0.00011481473008247594
ကွၢ် တၢ် မ	4.0252025256210765e-05
တၢ် မ တၤ	4.0252025256210765e-05
မ တၤ န့ၣ်	0.0005361531891007362
တၤ န့ၣ် လဲၣ်	0.0005326025841090093
န့ၣ် လဲၣ် တၢ်	0.00011481473008247594
လဲၣ် တၢ် ဂ့ၢ်	2.6049605289303116e-05
တၢ် ဂ့ၢ် ဝဲ	9.232756513487215e-05
ဂ့ၢ် ဝဲ အံၤ	5.208737522863381e-05
ဝဲ အံၤ န	3.906849025896846e-05
အံၤ န ဘၣ်	1.1847185322395464e-05
န ဘၣ် တဲ	7.113045333426248e-06
ဘၣ် တဲ တၢ်	3.3150815272756944e-05
တဲ တၢ် မ	6.628979519554146e-05
န့ၣ် လဲၣ် န	0.0004734258342468941
လဲၣ် န ဘၣ်	8.404282015417602e-05
န ဘၣ် ထံၣ်	2.378905344457031e-06
ဘၣ် ထံၣ် လိာ်	1.066365032515316e-05
ထံၣ် လိာ် သး	0.0001680738049583796
လိာ် သး ဒီး	9.942877511832598e-05
သး ဒီး မ	1.8948395305849292e-05
ဒီး မ တၤ	6.155565520657224e-05
န ဘၣ် တၢ်	8.296580330668552e-06
ဘၣ် တၢ် ဃု	1.4214255316880073e-05
တၢ် ဃု ထၢ	3.906849025896846e-05
ဃု ထၢ မ	2.1315465300333902e-05
ထၢ မ တၤ	1.7764860308606985e-05
န ဘၣ် စံၣ်	1.1953703472147272e-06

==> shan.all.syl.profile <==
ယွင်ႈ ၵုင်ႇ ၵူၼ်း	6.5225914475393466e-06
ၵုင်ႇ ၵူၼ်း ႁတ်း	6.5225914475393466e-06
ၵူၼ်း ႁတ်း ႁၢၼ်	6.5225914475393466e-06
ႁတ်း ႁၢၼ် ႁႃႉ	6.5225914475393466e-06
ႁၢၼ် ႁႃႉ ဢၼ်	6.5225914475393466e-06
ႁႃႉ ဢၼ် ၸႅတ်ႈ	6.5225914475393466e-06
ဢၼ် ၸႅတ်ႈ တူၺ်း	6.5225914475393466e-06
ၸႅတ်ႈ တူၺ်း သူ	6.5225914475393466e-06
တူၺ်း သူ ႁေႃႈ	6.5225914475393466e-06
သူ ႁေႃႈ ၵႃး	6.5225914475393466e-06
ႁေႃႈ ၵႃး ၼႆႉ	1.943861411593409e-05
ၵႃး ၼႆႉ တွပ်ႇ	6.5225914475393466e-06
ၼႆႉ တွပ်ႇ ယဝ်ႉ	6.5225914475393466e-06
တွပ်ႇ ယဝ်ႉ ယဝ်ႉ	6.5225914475393466e-06
ယဝ်ႉ ယဝ်ႉ ႁႃႉ	5.8186682121118326e-05
ယဝ်ႉ ႁႃႉ လွင်ႈ	1.943861411593409e-05
ႁႃႉ လွင်ႈ ၶူင်	6.5225914475393466e-06
လွင်ႈ ၶူင် သၢင်ႈ	6.5225914475393466e-06
ၶူင် သၢင်ႈ မႂ်း	6.5225914475393466e-06
သၢင်ႈ မႂ်း ဢမ်ႇ	6.5225914475393466e-06
မႂ်း ဢမ်ႇ ႁိုင်	6.5225914475393466e-06
ဢမ်ႇ ႁိုင် သင်	5.172867078692095e-05
ႁိုင် သင် တေ	2.5896625450131462e-05
သင် တေ ဢွင်ႇ	6.5225914475393466e-06
တေ ဢွင်ႇ မၢၼ်	1.2980602781736717e-05
ဢွင်ႇ မၢၼ် ယဝ်ႉ	6.5225914475393466e-06
မၢၼ် ယဝ်ႉ ဢၼ်	6.5225914475393466e-06
ယဝ်ႉ ဢၼ် ၼၼ်ႉ	0.00010985077279469732
ဢၼ် ၼၼ်ႉ ပဵၼ်	0.00010985077279469732
ၼၼ်ႉ ပဵၼ် လွင်ႈ	1.2980602781736717e-05
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/syl_profile$ 
```

## Revisiting Character

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lang_data$ python ./char_segmentation.py --input ./MyanmarTotal.my.clean.nosymbol --output ./char_seg/MyanmarTotal.my.clean.nosymbol.char
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lang_data$ cd char_seg/
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lang_data/char_seg$ head MyanmarTotal.my.clean.nosymbol.char 
န ေ က မ ီ း က ျ ီ း ခ ဲ လ ိ ု ရ ဲ ရ ဲ တ ေ ာ က ် ပ ြ ီ း တ က ် လ ာ တ ယ ် ပ ြ ီ း တ ေ ာ ့ င ါ တ ိ ု ့ ရ ပ ် န ိ ု င ် ရ ု ံ လ ေ ာ က ် ပ ဲ ရ ှ ိ ပ ေ မ ဲ ့ အ ခ ု ဘ ယ ် န ည ် း န ဲ ့ မ ဆ ိ ု တ ိ ု က ် ခ ိ ု က ် ရ တ ေ ာ ့ မ ယ ် စ စ ် သ ည ် ရ ဲ မ က ် တ ွ ေ မ ဟ ု တ ် ဘ ူ း တ စ ် ယ ေ ာ က ် ခ ျ င ် း တ ိ ု က ် ခ ိ ု က ် တ ာ မ ဟ ု တ ် ဘ ူ း ဒ ါ က ရ န ် ပ ွ ဲ တ စ ် ပ ွ ဲ
တ ေ ာ မ ီ း တ ွ ေ န ဲ ့ ရ ေ က ြ ီ း မ ှ ု တ ွ ေ ရ ဲ ့ ဘ ေ း ဒ ဏ ် က ိ ု ခ ံ ခ ဲ ့ ရ တ ဲ ့ အ မ ေ ရ ိ က န ် ပ ြ ည ် ထ ေ ာ င ် စ ု တ စ ် ခ ွ င ် က မ ိ သ ာ း စ ု တ ွ ေ အ တ ွ က ် က ြ က ် ခ ြ ေ န ီ အ ဖ ွ ဲ ့ က ထ ေ ာ က ် ပ ံ ့ မ ှ ု တ ွ ေ ပ ေ း န ေ တ ယ ်
ဒ ီ ည န ေ က ျ ွ န ် တ ေ ာ ် တ ိ ု ့ ရ ဲ ့ ပ ွ ဲ က ိ ု အ စ ီ အ စ ဉ ် မ ှ ူ း အ ဖ ြ စ ် ဆ ေ ာ င ် ရ ွ က ် ပ ေ း သ ူ က တ ေ ာ ့ ခ ျ စ ် စ ရ ာ က ေ ာ င ် း တ ဲ ့ ဖ ြ စ ် ပ ါ တ ယ ်
ဒ ါ က ဘ ာ အ တ ွ က ် လ ဲ ဆ ိ ု တ ာ မ ှ န ် း က ြ ည ် ့
မ င ် း ရ ေ ာ င ါ ရ ေ ာ မ င ် း ရ ဲ ့ ခ ွ ေ း လ ေ း ရ ေ ာ င ါ တ ိ ု ့ ရ ဲ ့ သ ိ မ ြ င ် န ာ း လ ည ် မ ှ ု စ က ြ ဝ ဠ ာ န ယ ် ပ ယ ် တ စ ် ခ ု ထ ဲ မ ှ ာ ပ ိ တ ် မ ိ န ေ က ြ တ ယ ် င ါ တ ိ ု ့ လ ွ တ ် မ ြ ေ ာ က ် န ိ ု င ် ရ င ် အ ရ ာ ဝ တ ္ ထ ု တ ွ ေ က ိ ု မ ြ င ် န ိ ု င ် တ ဲ ့ တ ခ ြ ာ း န ည ် း လ မ ် း တ ွ ေ အ မ ျ ာ း က ြ ီ း ရ ှ ိ လ ာ မ ယ ်
သ ူ တ ိ ု ့ အ လ ု ပ ် ခ ွ င ် ရ ဲ ့ သ န ာ း စ ရ ာ အ ခ ြ ေ အ န ေ ဟ ာ အ ရ င ် က ထ က ် ပ ိ ု ပ ြ ီ း အ ခ က ် အ ခ ဲ တ ွ ေ န ဲ ့ ရ င ် ဆ ိ ု င ် လ ာ ရ တ ယ ်
လ ု ပ ် ဖ ေ ာ ် က ိ ု င ် ဖ က ် အ သ စ ် ဒ ီ န ေ ့ အ ပ ြ င ် မ ှ ာ အ ရ မ ် း အ ေ း တ ာ တ ေ ာ င ် မ ှ ပ တ ် ဝ န ် း က ျ င ် ထ ိ န ် း သ ိ မ ် း ရ ေ း အ တ ွ က ် က ြ ံ ့ က ြ ံ ့ ခ ံ န ေ တ ု န ် း ပ ဲ
တ န ် န ဲ ့ ခ ျ ီ တ ဲ ့ ပ ိ ု း က ေ ာ င ် တ ွ ေ င ါ ့ ရ ှ ေ ့ က န ေ ရ ာ တ ိ ု င ် း မ ှ ာ င ါ သ ေ တ ေ ာ ့ မ ယ ် လ ိ ု ့ င ါ ထ င ် တ ယ ်
သ ိ ု ့ ဟ ာ း ဟ ာ း ဟ ာ း မ င ် း င ါ ့ က ိ ု လ ွ မ ် း န ေ မ ှ ာ ပ ဲ အ ဲ ဒ ါ က ိ ု ဝ န ် ခ ံ လ ိ ု က ် တ ာ လ ု ံ း ဝ က ေ ာ င ် း ပ ါ တ ယ ်
အ ပ ြ င ် က စ ာ ရ ွ က ် အ ရ ွ ယ ် အ စ ာ း ထ က ် က ျ ေ ာ ် လ ွ န ် ပ ြ ီ း လ ျ ှ ံ ထ ွ က ် န ေ တ ဲ ့ စ ာ သ ာ း တ ွ ေ န ဲ ့ ဖ ွ ဲ ့ ပ ြ ီ း သ ာ း စ ာ မ ျ က ် န ှ ာ တ ွ ေ က ိ ု ခ ေ ါ က ် လ ိ ု က ် အ ဲ ဒ ါ က ိ ု လ ိ ု ့ လ ည ် း ခ ေ ါ ် တ ယ ်
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lang_data/char_seg$ 
```

## Building Character Level Profile

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection$ ./generate_char_profile.sh ./lang_data/char_seg/
Running: python ./language_detection.py -c -i ./lang_data/char_seg//beik.all.char -n 7 -o ./char_profile/beik.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//dawei.all.char -n 7 -o ./char_profile/dawei.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//mon.all.char -n 7 -o ./char_profile/mon.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//MyanmarTotal.my.clean.nosymbol.char -n 7 -o ./char_profile/MyanmarTotal.my.clean.nosymbol.char.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//pao.all.char -n 7 -o ./char_profile/pao.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//po_kayin.all.char -n 7 -o ./char_profile/po_kayin.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//rakhine.all.char -n 7 -o ./char_profile/rakhine.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//sgaw_kayin.all.char -n 7 -o ./char_profile/sgaw_kayin.profile
Running: python ./language_detection.py -c -i ./lang_data/char_seg//shan.all.char -n 7 -o ./char_profile/shan.profile
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection$ 
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_profile$ head *
==> beik.profile <==
နင် ဘာ စီ စဉ် နေ ရယ် ဆို	1.4702504287745186e-05
ဘာ စီ စဉ် နေ ရယ် ဆို တာ	1.4702504287745186e-05
စီ စဉ် နေ ရယ် ဆို တာ ငါ့	1.4702504287745186e-05
စဉ် နေ ရယ် ဆို တာ ငါ့ ဝို	1.4702504287745186e-05
နေ ရယ် ဆို တာ ငါ့ ဝို ပြော	1.4702504287745186e-05
ရယ် ဆို တာ ငါ့ ဝို ပြော သင့်	1.4702504287745186e-05
ဆို တာ ငါ့ ဝို ပြော သင့် ပေါ့	1.4702504287745186e-05
တာ ငါ့ ဝို ပြော သင့် ပေါ့ လန်း	1.4702504287745186e-05
ငါ့ ဝို ပြော သင့် ပေါ့ လန်း ။	1.4702504287745186e-05
ဝို ပြော သင့် ပေါ့ လန်း ။ သူ	1.4702504287745186e-05

==> dawei.profile <==
နန် ဟှဲ ဇာ စီ စဉ် နေ ဟှယ်	1.4878260475031923e-05
ဟှဲ ဇာ စီ စဉ် နေ ဟှယ် ဆို	1.4878260475031923e-05
ဇာ စီ စဉ် နေ ဟှယ် ဆို တာ	1.4878260475031923e-05
စီ စဉ် နေ ဟှယ် ဆို တာ ငါ့	1.4878260475031923e-05
စဉ် နေ ဟှယ် ဆို တာ ငါ့ ကို	1.4878260475031923e-05
နေ ဟှယ် ဆို တာ ငါ့ ကို ပြော	1.4878260475031923e-05
ဟှယ် ဆို တာ ငါ့ ကို ပြော သင့်	1.4878260475031923e-05
ဆို တာ ငါ့ ကို ပြော သင့် ဟှယ်	1.4878260475031923e-05
တာ ငါ့ ကို ပြော သင့် ဟှယ် ။	1.4878260475031923e-05
ငါ့ ကို ပြော သင့် ဟှယ် ။ သူး	1.4878260475031923e-05

==> mon.profile <==
၂ ၀ မိ ဏေတ် ပၠန် တှ်ေ ဘာ	9.059390403486412e-06
၀ မိ ဏေတ် ပၠန် တှ်ေ ဘာ ရပ်	9.059390403486412e-06
မိ ဏေတ် ပၠန် တှ်ေ ဘာ ရပ် ဏောၚ်	9.059390403486412e-06
ဏေတ် ပၠန် တှ်ေ ဘာ ရပ် ဏောၚ် ။	9.059390403486412e-06
ပၠန် တှ်ေ ဘာ ရပ် ဏောၚ် ။ ဗှ်ေ	9.059390403486412e-06
တှ်ေ ဘာ ရပ် ဏောၚ် ။ ဗှ်ေ ဟ	9.059390403486412e-06
ဘာ ရပ် ဏောၚ် ။ ဗှ်ေ ဟ ယျ	9.059390403486412e-06
ရပ် ဏောၚ် ။ ဗှ်ေ ဟ ယျ တုဲ	9.059390403486412e-06
ဏောၚ် ။ ဗှ်ေ ဟ ယျ တုဲ မာန်	9.059390403486412e-06
။ ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ	9.059390403486412e-06

==> MyanmarTotal.my.clean.nosymbol.char.profile <==
နေ က မီး ကျီး ခဲ လို ရဲ	1.5149294573098204e-06
က မီး ကျီး ခဲ လို ရဲ ရဲ	1.5149294573098204e-06
မီး ကျီး ခဲ လို ရဲ ရဲ တောက်	1.5149294573098204e-06
ကျီး ခဲ လို ရဲ ရဲ တောက် ပြီး	1.5149294573098204e-06
ခဲ လို ရဲ ရဲ တောက် ပြီး တက်	1.5149294573098204e-06
လို ရဲ ရဲ တောက် ပြီး တက် လာ	1.5149294573098204e-06
ရဲ ရဲ တောက် ပြီး တက် လာ တယ်	1.5149294573098204e-06
ရဲ တောက် ပြီး တက် လာ တယ် ပြီး	1.5149294573098204e-06
တောက် ပြီး တက် လာ တယ် ပြီး တော့	1.5149294573098204e-06
ပြီး တက် လာ တယ် ပြီး တော့ ငါ	1.5149294573098204e-06

==> pao.profile <==
လို မူႏ ပေႏ မာꩻ တ မုဲင်ꩻ ဟောင်း	5.379266230804075e-06
မူႏ ပေႏ မာꩻ တ မုဲင်ꩻ ဟောင်း ဝွေꩻ	5.379266230804075e-06
ပေႏ မာꩻ တ မုဲင်ꩻ ဟောင်း ဝွေꩻ သီး	5.379266230804075e-06
မာꩻ တ မုဲင်ꩻ ဟောင်း ဝွေꩻ သီး အီး	5.379266230804075e-06
တ မုဲင်ꩻ ဟောင်း ဝွေꩻ သီး အီး ကွီႏ	5.379266230804075e-06
မုဲင်ꩻ ဟောင်း ဝွေꩻ သီး အီး ကွီႏ သ	5.379266230804075e-06
ဟောင်း ဝွေꩻ သီး အီး ကွီႏ သ ညင်ꩻ	5.379266230804075e-06
ဝွေꩻ သီး အီး ကွီႏ သ ညင်ꩻ နာꩻ	5.379266230804075e-06
သီး အီး ကွီႏ သ ညင်ꩻ နာꩻ တ	5.379266230804075e-06
အီး ကွီႏ သ ညင်ꩻ နာꩻ တ မွေး	5.379266230804075e-06

==> po_kayin.profile <==
န ဂဲၫ ထဲၩ့ မၩ ဆၧ လ ဖၪ	4.263027082673391e-06
ဂဲၫ ထဲၩ့ မၩ ဆၧ လ ဖၪ အ	4.263027082673391e-06
ထဲၩ့ မၩ ဆၧ လ ဖၪ အ ဂး	4.263027082673391e-06
မၩ ဆၧ လ ဖၪ အ ဂး န	4.263027082673391e-06
ဆၧ လ ဖၪ အ ဂး န နီၪ့	4.263027082673391e-06
လ ဖၪ အ ဂး န နီၪ့ ယါ	4.263027082673391e-06
ဖၪ အ ဂး န နီၪ့ ယါ လၩ့	4.263027082673391e-06
အ ဂး န နီၪ့ ယါ လၩ့ န	4.263027082673391e-06
ဂး န နီၪ့ ယါ လၩ့ န ၥၭ	4.263027082673391e-06
န နီၪ့ ယါ လၩ့ န ၥၭ အ့ၬ	4.263027082673391e-06

==> rakhine.profile <==
မင်း ယင်း ချင့် ကို အ ခြား တစ်	4.320733987466792e-06
ယင်း ချင့် ကို အ ခြား တစ် ခု	4.320733987466792e-06
ချင့် ကို အ ခြား တစ် ခု နန့်	4.320733987466792e-06
ကို အ ခြား တစ် ခု နန့် မ	4.320733987466792e-06
အ ခြား တစ် ခု နန့် မ ချိတ်	4.320733987466792e-06
ခြား တစ် ခု နန့် မ ချိတ် ပါ	4.320733987466792e-06
တစ် ခု နန့် မ ချိတ် ပါ လား	4.320733987466792e-06
ခု နန့် မ ချိတ် ပါ လား ။	4.320733987466792e-06
နန့် မ ချိတ် ပါ လား ။ ထို	4.320733987466792e-06
မ ချိတ် ပါ လား ။ ထို မ	4.320733987466792e-06

==> sgaw_kayin.profile <==
န ဘၣ် သံ ကွၢ် တၢ် မ တၤ	1.1881138269511035e-06
ဘၣ် သံ ကွၢ် တၢ် မ တၤ န့ၣ်	1.1881138269511035e-06
သံ ကွၢ် တၢ် မ တၤ န့ၣ် လဲၣ်	2.364464150665067e-06
ကွၢ် တၢ် မ တၤ န့ၣ် လဲၣ် တၢ်	1.1881138269511035e-06
တၢ် မ တၤ န့ၣ် လဲၣ် တၢ် ဂ့ၢ်	1.1881138269511035e-06
မ တၤ န့ၣ် လဲၣ် တၢ် ဂ့ၢ် ဝဲ	1.1881138269511035e-06
တၤ န့ၣ် လဲၣ် တၢ် ဂ့ၢ် ဝဲ အံၤ	1.1881138269511035e-06
န့ၣ် လဲၣ် တၢ် ဂ့ၢ် ဝဲ အံၤ န	2.364464150665067e-06
လဲၣ် တၢ် ဂ့ၢ် ဝဲ အံၤ န ဘၣ်	1.1881138269511035e-06
တၢ် ဂ့ၢ် ဝဲ အံၤ န ဘၣ် တဲ	1.1881138269511035e-06

==> shan.profile <==
ယွင်ႈ ၵုင်ႇ ၵူၼ်း ႁတ်း ႁၢၼ် ႁႃႉ ဢၼ်	6.504169752390766e-06
ၵုင်ႇ ၵူၼ်း ႁတ်း ႁၢၼ် ႁႃႉ ဢၼ် ၸႅတ်ႈ	6.504169752390766e-06
ၵူၼ်း ႁတ်း ႁၢၼ် ႁႃႉ ဢၼ် ၸႅတ်ႈ တူၺ်း	6.504169752390766e-06
ႁတ်း ႁၢၼ် ႁႃႉ ဢၼ် ၸႅတ်ႈ တူၺ်း သူ	6.504169752390766e-06
ႁၢၼ် ႁႃႉ ဢၼ် ၸႅတ်ႈ တူၺ်း သူ ႁေႃႈ	6.504169752390766e-06
ႁႃႉ ဢၼ် ၸႅတ်ႈ တူၺ်း သူ ႁေႃႈ ၵႃး	6.504169752390766e-06
ဢၼ် ၸႅတ်ႈ တူၺ်း သူ ႁေႃႈ ၵႃး ၼႆႉ	6.504169752390766e-06
ၸႅတ်ႈ တူၺ်း သူ ႁေႃႈ ၵႃး ၼႆႉ တွပ်ႇ	6.504169752390766e-06
တူၺ်း သူ ႁေႃႈ ၵႃး ၼႆႉ တွပ်ႇ ယဝ်ႉ	6.504169752390766e-06
သူ ႁေႃႈ ၵႃး ၼႆႉ တွပ်ႇ ယဝ်ႉ ယဝ်ႉ	6.504169752390766e-06
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_profile$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_profile$ head *.profile
==> beik.profile <==
နင် ဘာ စီ	4.400329396086221e-05
ဘာ စီ စဉ်	4.400329396086221e-05
စီ စဉ် နေ	1.4765224883877354e-05
စဉ် နေ ရယ်	1.4765224883877354e-05
နေ ရယ် ဆို	0.00013171750119181678
ရယ် ဆို တာ	0.0002632888120382487
ဆို တာ ငါ့	1.4765224883877354e-05
တာ ငါ့ ဝို	1.4765224883877354e-05
ငါ့ ဝို ပြော	4.400329396086221e-05
ဝို ပြော သင့်	1.4765224883877354e-05

==> dawei.profile <==
နန် ဟှဲ ဇာ	0.001094696012191491
ဟှဲ ဇာ စီ	1.4939102449850099e-05
ဇာ စီ စဉ်	1.4939102449850099e-05
စီ စဉ် နေ	1.4939102449850099e-05
စဉ် နေ ဟှယ်	1.4939102449850099e-05
နေ ဟှယ် ဆို	0.0002663893417047528
ဟှယ် ဆို တာ	0.000355136484971189
ဆို တာ ငါ့	1.4939102449850099e-05
တာ ငါ့ ကို	1.4939102449850099e-05
ငါ့ ကို ပြော	1.4939102449850099e-05

==> mon.profile <==
၂ ၀ မိ	2.7112945143215798e-05
၀ မိ ဏေတ်	9.09769920087972e-06
မိ ဏေတ် ပၠန်	9.09769920087972e-06
ဏေတ် ပၠန် တှ်ေ	9.09769920087972e-06
ပၠန် တှ်ေ ဘာ	9.09769920087972e-06
တှ်ေ ဘာ ရပ်	9.09769920087972e-06
ဘာ ရပ် ဏောၚ်	9.09769920087972e-06
ရပ် ဏောၚ် ။	9.09769920087972e-06
ဏောၚ် ။ ဗှ်ေ	0.00011718917485489619
။ ဗှ်ေ ဟ	1.8105322172047758e-05

==> pao.profile <==
လို မူႏ ပေႏ	0.00011767805007096772
မူႏ ပေႏ မာꩻ	5.400037736105288e-06
ပေႏ မာꩻ တ	1.609318176799695e-05
မာꩻ တ မုဲင်ꩻ	0.0003956997949001509
တ မုဲင်ꩻ ဟောင်း	0.0015291730622806667
မုဲင်ꩻ ဟောင်း ဝွေꩻ	0.0007753064080323048
ဟောင်း ဝွေꩻ သီး	0.0009303569964947339
ဝွေꩻ သီး အီး	0.0006309489636017674
သီး အီး ကွီႏ	5.400037736105288e-06
အီး ကွီႏ သ	5.400037736105288e-06

==> po_kayin.profile <==
န ဂဲၫ ထဲၩ့	0.0008742438370074405
ဂဲၫ ထဲၩ့ မၩ	0.0004626053136846808
ထဲၩ့ မၩ ဆၧ	0.00012310962434632227
မၩ ဆၧ လ	5.521048647865056e-05
ဆၧ လ ဖၪ	0.00013159701657978123
လ ဖၪ အ	0.00028861377289877207
ဖၪ အ ဂး	3.823570201173263e-05
အ ဂး န	0.000182521369980535
ဂး န နီၪ့	4.286133077896777e-06
န နီၪ့ ယါ	8.529829194626257e-06

==> rakhine.profile <==
မင်း ယင်း ချင့်	0.0003527139187767928
ယင်း ချင့် ကို	0.0030321526628073
ချင့် ကို အ	0.000167776734196838
ကို အ ခြား	4.3438734052501e-06
အ ခြား တစ်	8.644738162923465e-06
ခြား တစ် ခု	1.72464676782702e-05
တစ် ခု နန့်	1.2945602920596831e-05
ခု နန့် မ	4.3438734052501e-06
နန့် မ ချိတ်	4.3438734052501e-06
မ ချိတ် ပါ	4.3438734052501e-06

==> sgaw_kayin.profile <==
န ဘၣ် သံ	3.5624403416993355e-06
ဘၣ် သံ ကွၢ်	7.812514516796451e-05
သံ ကွၢ် တၢ်	0.00011481473008247594
ကွၢ် တၢ် မ	4.0252025256210765e-05
တၢ် မ တၤ	4.0252025256210765e-05
မ တၤ န့ၣ်	0.0005361531891007362
တၤ န့ၣ် လဲၣ်	0.0005326025841090093
န့ၣ် လဲၣ် တၢ်	0.00011481473008247594
လဲၣ် တၢ် ဂ့ၢ်	2.6049605289303116e-05
တၢ် ဂ့ၢ် ဝဲ	9.232756513487215e-05

==> shan.profile <==
ယွင်ႈ ၵုင်ႇ ၵူၼ်း	6.5225914475393466e-06
ၵုင်ႇ ၵူၼ်း ႁတ်း	6.5225914475393466e-06
ၵူၼ်း ႁတ်း ႁၢၼ်	6.5225914475393466e-06
ႁတ်း ႁၢၼ် ႁႃႉ	6.5225914475393466e-06
ႁၢၼ် ႁႃႉ ဢၼ်	6.5225914475393466e-06
ႁႃႉ ဢၼ် ၸႅတ်ႈ	6.5225914475393466e-06
ဢၼ် ၸႅတ်ႈ တူၺ်း	6.5225914475393466e-06
ၸႅတ်ႈ တူၺ်း သူ	6.5225914475393466e-06
တူၺ်း သူ ႁေႃႈ	6.5225914475393466e-06
သူ ႁေႃႈ ၵႃး	6.5225914475393466e-06
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_profile$
```

## Test-Run with 7gram Profile

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ ./detect_all_7g.sh ./eg_input/
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//bamar_burmese.txt --profile ./7g_syl_profile/
shan.all: 11.11%
MyanmarTotal.my.clean.nosymbol: 11.11%
beik.all: 11.11%
dawei.all: 11.11%
po_kayin.all: 11.11%
pao.all: 11.11%
rakhine.all: 11.11%
mon.all: 11.11%
sgaw_kayin.all: 11.11%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//beik.txt --profile ./7g_syl_profile/
shan.all: 0.00%
MyanmarTotal.my.clean.nosymbol: 0.00%
beik.all: 100.00%
dawei.all: 0.00%
po_kayin.all: 0.00%
pao.all: 0.00%
rakhine.all: 0.00%
mon.all: 0.00%
sgaw_kayin.all: 0.00%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//dawei.txt --profile ./7g_syl_profile/
shan.all: 0.00%
MyanmarTotal.my.clean.nosymbol: 0.00%
beik.all: 0.00%
dawei.all: 100.00%
po_kayin.all: 0.00%
pao.all: 0.00%
rakhine.all: 0.00%
mon.all: 0.00%
sgaw_kayin.all: 0.00%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//mon_tst.txt --profile ./7g_syl_profile/
shan.all: 11.19%
MyanmarTotal.my.clean.nosymbol: 11.19%
beik.all: 11.19%
dawei.all: 11.19%
po_kayin.all: 11.19%
pao.all: 11.19%
rakhine.all: 11.19%
mon.all: 10.45%
sgaw_kayin.all: 11.19%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//mon.txt --profile ./7g_syl_profile/
shan.all: 12.50%
MyanmarTotal.my.clean.nosymbol: 12.50%
beik.all: 12.50%
dawei.all: 12.50%
po_kayin.all: 12.50%
pao.all: 12.50%
rakhine.all: 12.50%
mon.all: 0.02%
sgaw_kayin.all: 12.50%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//pao.txt --profile ./7g_syl_profile/
shan.all: 12.49%
MyanmarTotal.my.clean.nosymbol: 12.49%
beik.all: 12.49%
dawei.all: 12.49%
po_kayin.all: 12.49%
pao.all: 0.05%
rakhine.all: 12.49%
mon.all: 12.49%
sgaw_kayin.all: 12.49%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//po_kayin.txt --profile ./7g_syl_profile/
shan.all: 12.50%
MyanmarTotal.my.clean.nosymbol: 12.50%
beik.all: 12.50%
dawei.all: 12.50%
po_kayin.all: 0.00%
pao.all: 12.50%
rakhine.all: 12.50%
mon.all: 12.50%
sgaw_kayin.all: 12.50%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//rakhine.txt --profile ./7g_syl_profile/
shan.all: 10.84%
MyanmarTotal.my.clean.nosymbol: 10.84%
beik.all: 24.15%
dawei.all: 10.84%
po_kayin.all: 10.84%
pao.all: 10.84%
rakhine.all: 0.00%
mon.all: 10.84%
sgaw_kayin.all: 10.84%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//sgaw_kayin.txt --profile ./7g_syl_profile/
shan.all: 12.50%
MyanmarTotal.my.clean.nosymbol: 12.50%
beik.all: 12.50%
dawei.all: 12.50%
po_kayin.all: 12.50%
pao.all: 12.50%
rakhine.all: 12.50%
mon.all: 12.50%
sgaw_kayin.all: 0.00%
Running: python ./language_detection.py --detect --ngram 7 --input ./eg_input//shan.txt --profile ./7g_syl_profile/
shan.all: 11.11%
MyanmarTotal.my.clean.nosymbol: 11.11%
beik.all: 11.11%
dawei.all: 11.11%
po_kayin.all: 11.11%
pao.all: 11.11%
rakhine.all: 11.11%
mon.all: 11.11%
sgaw_kayin.all: 11.11%
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ 
```

## Test-Run with 3gram Syllable Profile

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ ./detect_all_3g.sh ./eg_input/
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//bamar_burmese.txt --profile ./3g_syl_profile/
beik.all.syl: 79.94%
bamar.syl: 18.09%
dawei.all.syl: 0.60%
pao.all.syl: 0.15%
po_kayin.all.syl: 0.15%
sgaw_kayin.all.syl: 0.03%
mon.all.syl: 0.15%
shan.all.syl: 0.15%
rakhine.all.syl: 0.73%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//beik.txt --profile ./3g_syl_profile/
beik.all.syl: 100.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//dawei.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 100.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//mon_tst.txt --profile ./3g_syl_profile/
beik.all.syl: 11.47%
bamar.syl: 11.47%
dawei.all.syl: 11.47%
pao.all.syl: 11.47%
po_kayin.all.syl: 11.47%
sgaw_kayin.all.syl: 11.47%
mon.all.syl: 8.26%
shan.all.syl: 11.47%
rakhine.all.syl: 11.47%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//mon.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 100.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//pao.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 100.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//po_kayin.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 100.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//rakhine.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 100.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//sgaw_kayin.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 100.00%
mon.all.syl: 0.00%
shan.all.syl: 0.00%
rakhine.all.syl: 0.00%
Running: python ./language_detection.py --detect --ngram 3 --input ./eg_input//shan.txt --profile ./3g_syl_profile/
beik.all.syl: 0.00%
bamar.syl: 0.00%
dawei.all.syl: 0.00%
pao.all.syl: 0.00%
po_kayin.all.syl: 0.00%
sgaw_kayin.all.syl: 0.00%
mon.all.syl: 0.00%
shan.all.syl: 100.00%
rakhine.all.syl: 0.00%
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib$ 
```

## Reheck the Test Files

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ set -x; for file in *.txt; do cat $file; done; set +x;
+ for file in *.txt
+ cat bamar_burmese.txt
နေ ကောင်း လား
ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
မင်္ဂ လာ ပါ ဆ ရာ မ
တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
ကျောင်း သား ကျောင်း သွား ပါ
က လေး က အိမ် မှာ ပါ
ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
+ for file in *.txt
+ cat beik.txt
ဖယ် သူ လေ ကို မေး ရိ လဲ ။
သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
+ for file in *.txt
+ cat dawei.txt
ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။
+ for file in *.txt
+ cat mon_tst.txt
လၟုဟ် အဲဗ္တောန် တိၚ်မံၚ် ဂီတာ ။
ကသပ်ပ္ဍဲဗှ်ေဂှ်
+ for file in *.txt
+ cat mon.txt
ဗှ်ေ ဟယျ တုဲ မာန်ဟာ ။
ယဝ်ဗှ်ေ ဟွံပယှုက် အဲ ရတှ်ေ တုဲမာန်ဏောၚ် ။
အဲ ဟယျ ဗှ်ေ တိၚ်ဂီတာ လေပ်မံၚ် ။
လၟုဟ် အဲ ဗ္တောန် တိၚ်မံၚ် ဂီတာ ။
ပေါဲဂီတဂှ် ဂိတု ဂတမှ ကၠောန်ဏောၚ် ။
သွက်အဲ ဂွံအံၚ်ဇၞး ရာဒနာ ကဵုညိ ။
ခိုဟ်ယျ ဆက်ဂစာန် ညိပၠန် ။
ဂလာန် ဗှ်ေ ပတိုန်လဝ် နူဏေအ်ဗ္တံဂှ် ခိုဟ်ကွေံကွေံ။
ၜိုတ်အဲ ကၠောန်မာန် အဲဂစာန် လဝ်ရ။
ပ္ဍဲဗှ်ေဂှ် ကသပ် တၟေၚ်ၚ် နွံမံၚ်။
+ for file in *.txt
+ cat pao.txt
နဝ်ꩻနဝ်ꩻ နာꩻ တ အွဉ်ႏဖွို့ꩻ တဝ်းဟောင်း တွမ်ႏ အလင် တဗာႏ
ဝွေꩻမူႏ တ တောင်ချာတဝ်းဒွုမ် ပါꩻမုဲင်ꩻမုဲင်ꩻ
နဝ်ꩻနဝ်ꩻ နီ အတာႏ ယပ်ခုဲင်ႏငါႏ
နာꩻ ကဒေါ့ꩻ အတွိုင်ꩻ ခွေ သျင်ꩻပျ ဗာႏဒျာႏ
ကထိန်ꩻ‌နွောင်ꩻ ဝွေꩻနဝ်ꩻ အဝ်ႏဒျာႏ နာꩻ လွုမ်
နဝ်ꩻနဝ်ꩻ ခွေ ယမ်း မာႏဗာႏဟောင်း
ခွေ စဥ်ꩻစာꩻ အတွိုင်ꩻ စဥ်ꩻစာꩻဟုဲင်း
ဒေါ့ꩻဝင်ꩻမဉ်ꩻ နဝ်ꩻ လွထီႏငါႏ
ဆုဲင်ꩻသွတ် တ လဲင်ႏ ရက်ဒျာႏ ဝွေꩻနဝ်ꩻ တဲ့ ဒေါ့ꩻခွင်ꩻ တ လ တဝ်းဒွုမ်
တယ်ႏ နာဆာ ဒုံးပျံ ထင်ႏစခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏဒျာႏ မတ်တန်ꩻ
+ for file in *.txt
+ cat po_kayin.txt
ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
+ for file in *.txt
+ cat rakhine.txt
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
+ for file in *.txt
+ cat sgaw_kayin.txt
တၢ်ဝဲန့ၣ်နတဘျးစဲဒီးအဂၤတခါဧဲၣ်.
ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
ပျဲတၢ်မၤစၢၤတက့ၢ်.
+ for file in *.txt
+ cat shan.txt
မႂ်း လွင်ႈၼႆႉ လၢတ်ႈမႃး ႁိုဝ် ဢမ်ႇလၢတ်ႈမႃး ႁႃႉ ။
တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေလႆႈ ဢဝ် ပပ်ႉလႂ် ။
တွင်းပၢၼ်ႇၵဝ် ဢမ်ႇ တွင်းပၢၼ်ႇ ၵဝ် ။
ဢရသႃႇ မၼ်းတႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉဝၢၼ်ႇ ဝႆႉ ။
မိူဝ်ႈပူၼ်ႉ မႃး ဝၼ်းသုၵ်း ၵၢင်ၼႂ် ႑႑ မွင်း ၼၼ်ႉ သူ  မီးယူႇ တီႈလႂ် ။
ဢၼ်ၼႆႉ တႃႇမၼ်း ယၢပ်ႇ ဢိူဝ်ႈ ။
ဢမ်ႇမီး ၶပ်းမၢႆ တႃႇဢွၵ်ႇပၢႆႈ ႁႃႉ ။
တႃႇမၼ်းၼၢင်း ႁဝ်းတေ ထၢမ် ဢမ်ႇ ၸႂ်ႈ ။
ႁဝ်း မိူဝ်ႈၽုၵ်ႈ ၵၢင်ၼႂ် တေဢွၵ်ႇပႆတၢင်း ဢိူဝ်ႈ ။
ဢမ်ႇ မူတ်းသႂ် ႁႃႉ ။
+ set +x
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ 
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ file *
bamar_burmese.txt: Unicode text, UTF-8 text
beik.txt:          Unicode text, UTF-8 text
dawei.txt:         Unicode text, UTF-8 text
mon_tst.txt:       Unicode text, UTF-8 text
mon.txt:           Unicode text, UTF-8 text
pao.txt:           Unicode text, UTF-8 text
po_kayin.txt:      Unicode text, UTF-8 text
rakhine.txt:       Unicode text, UTF-8 text
sgaw_kayin.txt:    Unicode text, UTF-8 text
shan.txt:          Unicode text, UTF-8 text
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$ wc *
   9   65  710 bamar_burmese.txt
  10  103  928 beik.txt
  10  100 1012 dawei.txt
   2    6  132 mon_tst.txt
  10   50  917 mon.txt
  10   57 1182 pao.txt
  10   10  957 po_kayin.txt
  10  103  934 rakhine.txt
  10   10  908 sgaw_kayin.txt
  10   61 1082 shan.txt
  91  565 8762 total
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/lib/eg_input$
```

## Brainstorming with ChatGPT

```
Yes, there are several other approaches to language detection besides the Naive Bayes classifier with n-gram analysis. These approaches can vary in complexity and suitability depending on the specific requirements and resources available. Here are some alternative methods:

1. **Machine Learning Models**:
   - **Support Vector Machines (SVMs)**: SVMs can be effective for language detection, especially when dealing with high-dimensional feature spaces.
   - **Neural Networks**: Deep learning models, especially Recurrent Neural Networks (RNNs) or Convolutional Neural Networks (CNNs), can be used for language detection. They are particularly good at capturing contextual information in text data.
   - **Transformer Models**: Models like BERT or GPT, which are based on the transformer architecture, can be fine-tuned for language detection tasks. They are highly effective due to their ability to understand context and semantics.

2. **Dictionary-Based Approach**: This method involves creating a comprehensive dictionary for each language and checking the presence of words in these dictionaries. It's more straightforward but may struggle with languages that share a lot of vocabulary.

3. **Rule-Based Systems**: These systems use a set of manually crafted linguistic rules for each language. They can be very accurate but are time-consuming to develop and maintain, and their effectiveness is limited by the completeness of the rules.

4. **Character Frequency Analysis**: Analyzing the frequency of character usage can be effective, especially for languages that have distinct alphabets or character sets.

5. **Language Identification via API Services**: There are several APIs available (like Google Cloud Translation API, Microsoft Azure Text Analytics API) that provide language detection as a service. These are often easy to use but may incur costs and require internet connectivity.

6. **Hybrid Approaches**: Combining multiple methods can often yield better results. For example, a machine learning model can be used in conjunction with a rule-based system to improve accuracy.

7. **Text Embeddings with Clustering**: Generating text embeddings using models like Word2Vec, FastText, or universal sentence encoders, and then using clustering algorithms to distinguish between languages.

8. **Linguistic Feature Analysis**: Analyzing linguistic features such as syntax, grammar, and sentence structure can also be effective, especially for languages that are structurally different.

9. **Text Length and Structure Analysis**: Sometimes, simple features like average word length, sentence length, and text structure can give clues about the language.

Each of these approaches has its strengths and weaknesses, and the choice of method often depends on the specific requirements of the task, the languages involved, the availability of training data, and computational resources. In practice, a combination of several methods is often used to achieve the best results.
```

## Try Frequency Based Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ ./build_dict.sh 
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/bamar_profile.json
Created language profile for bamar
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/beik_profile.json
Created language profile for beik
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/dawei_profile.json
Created language profile for dawei
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/mon_profile.json
Created language profile for mon
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/pao_profile.json
Created language profile for pao
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/po_kayin_profile.json
Created language profile for po_kayin
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/rakhine_profile.json
Created language profile for rakhine
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/sgaw_kayin_profile.json
Created language profile for sgaw_kayin
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/freq_dict/profile/shan_profile.json
Created language profile for shan
All language profiles have been created.
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ tree ./profile/
./profile/
├── bamar_profile.json
├── beik_profile.json
├── dawei_profile.json
├── mon_profile.json
├── pao_profile.json
├── po_kayin_profile.json
├── rakhine_profile.json
├── sgaw_kayin_profile.json
└── shan_profile.json

0 directories, 9 files
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$
```

## Try Embedding Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ ./mk_embeddings.py 
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/bamar_word2vec.model
Word2Vec model for bamar saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/bamar_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/bamar_fasttext.model
FastText model for bamar saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/bamar_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/beik_word2vec.model
Word2Vec model for beik saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/beik_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/beik_fasttext.model
FastText model for beik saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/beik_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/dawei_word2vec.model
Word2Vec model for dawei saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/dawei_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/dawei_fasttext.model
FastText model for dawei saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/dawei_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/mon_word2vec.model
Word2Vec model for mon saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/mon_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/mon_fasttext.model
FastText model for mon saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/mon_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/pao_word2vec.model
Word2Vec model for pao saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/pao_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/pao_fasttext.model
FastText model for pao saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/pao_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/po_kayin_word2vec.model
Word2Vec model for po_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/po_kayin_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/po_kayin_fasttext.model
FastText model for po_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/po_kayin_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/rakhine_word2vec.model
Word2Vec model for rakhine saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/rakhine_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/rakhine_fasttext.model
FastText model for rakhine saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/rakhine_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/sgaw_kayin_word2vec.model
Word2Vec model for sgaw_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/sgaw_kayin_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/sgaw_kayin_fasttext.model
FastText model for sgaw_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/sgaw_kayin_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/shan_word2vec.model
Word2Vec model for shan saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/shan_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/shan_fasttext.model
FastText model for shan saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/shan_fasttext.model
Training completed for all languages.
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ tree ./word2vec/
./word2vec/
├── bamar_word2vec.model
├── beik_word2vec.model
├── dawei_word2vec.model
├── mon_word2vec.model
├── pao_word2vec.model
├── po_kayin_word2vec.model
├── rakhine_word2vec.model
├── sgaw_kayin_word2vec.model
└── shan_word2vec.model

0 directories, 9 files
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ tree ./fasttext/
./fasttext/
├── bamar_fasttext.model
├── bamar_fasttext.model.wv.vectors_ngrams.npy
├── beik_fasttext.model
├── beik_fasttext.model.wv.vectors_ngrams.npy
├── dawei_fasttext.model
├── dawei_fasttext.model.wv.vectors_ngrams.npy
├── mon_fasttext.model
├── mon_fasttext.model.wv.vectors_ngrams.npy
├── pao_fasttext.model
├── pao_fasttext.model.wv.vectors_ngrams.npy
├── po_kayin_fasttext.model
├── po_kayin_fasttext.model.wv.vectors_ngrams.npy
├── rakhine_fasttext.model
├── rakhine_fasttext.model.wv.vectors_ngrams.npy
├── sgaw_kayin_fasttext.model
├── sgaw_kayin_fasttext.model.wv.vectors_ngrams.npy
├── shan_fasttext.model
└── shan_fasttext.model.wv.vectors_ngrams.npy

0 directories, 18 files
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ 
```

## Test-Run with Embedding Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ ./detect_languages.sh 
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
File: beik.txt - Detected Language with Word2Vec: Detected language: dawei_word2vec
File: dawei.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: mon_tst.txt - Detected Language with Word2Vec: Detected language: po_kayin_word2vec
File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: pao.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: po_kayin.txt - Detected Language with Word2Vec: Detected language: po_kayin_word2vec
File: rakhine.txt - Detected Language with Word2Vec: Detected language: sgaw_kayin_word2vec
File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: po_kayin_word2vec
File: shan.txt - Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
File: beik.txt - Detected Language with FastText: Detected language: pao_fasttext
File: dawei.txt - Detected Language with FastText: Detected language: pao_fasttext
File: mon_tst.txt - Detected Language with FastText: Detected language: beik_fasttext
File: mon.txt - Detected Language with FastText: Detected language: mon_fasttext
File: pao.txt - Detected Language with FastText: Detected language: pao_fasttext
File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: rakhine.txt - Detected Language with FastText: Detected language: pao_fasttext
File: sgaw_kayin.txt - Detected Language with FastText: Detected language: pao_fasttext
File: shan.txt - Detected Language with FastText: Detected language: rakhine_fasttext
Language detection completed for all files.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

## To Do

Input language ရဲ့ segmentation ကလည်း syllable ဖြတ်ထားမှ ဖြစ်လိမ့်မယ်။   

## Syllable Breaking for All Test Files

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ ./break4all.sh 
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/bamar_burmese.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/beik.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/dawei.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/mon_tst.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/mon.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/pao.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/po_kayin.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/rakhine.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/sgaw_kayin.txt
Processed: /home/ye/exp/sylbreak4all/lang_detection/embedding/eg_input/shan.txt
Syllable breaking completed for all files.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ cd eg_input/
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding/eg_input$ head *.txt
==> bamar_burmese.txt <==
နေ ကောင်း လား
ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
မင်္ဂ လာ ပါ ဆ ရာ မ
တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
ကျောင်း သား ကျောင်း သွား ပါ
က လေး က အိမ် မှာ ပါ
ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ

==> beik.txt <==
ဖယ် သူ လေ ကို မေး ရိ လဲ ။
သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။

==> dawei.txt <==
ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။

==> mon_tst.txt <==
လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်

==> mon.txt <==
ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။

==> pao.txt <==
နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
 နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ

==> po_kayin.txt <==
ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .

==> rakhine.txt <==
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။

==> sgaw_kayin.txt <==
တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .

==> shan.txt <==
မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding/eg_input$ 
```

## Copy for Freq Folder Also

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ rm -r eg_input/
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ cp ../embedding/eg_input/ . -r
```

## Testing Again for Frequency

test input ဖိုင်ကိုလည်း syllable ဖြတ်ထားပြီး ပြန် language detect လုပ်ကြည့်တာ။   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ time ./detect_languages.sh 
File: bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json
File: beik.txt - Detected Language: Detected language: rakhine_profile.json
File: dawei.txt - Detected Language: Detected language: beik_profile.json
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
File: mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json
File: pao.txt - Detected Language: Detected language: pao_profile.json
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
File: shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Language detection completed for all files.

real	0m0.196s
user	0m0.151s
sys	0m0.026s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ 
```

## Testing Again for Embedding Approach

syllable breaked လုပ်ထားပြီးသား ဖိုင်နဲ့ ပြန်စမ်းကြည့်တာ ...   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./detect_languages.sh 
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
File: beik.txt - Detected Language with Word2Vec: Detected language: dawei_word2vec
File: dawei.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: pao.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: rakhine.txt - Detected Language with Word2Vec: Detected language: sgaw_kayin_word2vec
File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: shan.txt - Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
File: beik.txt - Detected Language with FastText: Detected language: pao_fasttext
File: dawei.txt - Detected Language with FastText: Detected language: pao_fasttext
File: mon_tst.txt - Detected Language with FastText: Detected language: pao_fasttext
File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: rakhine.txt - Detected Language with FastText: Detected language: pao_fasttext
File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: shan.txt - Detected Language with FastText: Detected language: rakhine_fasttext
Language detection completed for all files.

real	0m27.112s
user	0m31.835s
sys	1m24.705s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ 
```

အဆင်မပြေဘူး။ ပြောရရင်တော့ corpus size ကသေးတာလည်း ပါတယ်။   
ပြီးတော့ ဗမာရယ်၊ ထားဝယ်ရယ်၊ ဘိတ်ရယ်၊ ရခိုင်ရယ်က ခွဲရခက်တယ်။  

## Try Word-Embedding Approach with Minimum Count = 2

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./mk_embeddings.sh 
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/bamar_word2vec.model
Word2Vec model for bamar saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/bamar_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/bamar_fasttext.model
FastText model for bamar saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/bamar_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/beik_word2vec.model
Word2Vec model for beik saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/beik_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/beik_fasttext.model
FastText model for beik saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/beik_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/dawei_word2vec.model
Word2Vec model for dawei saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/dawei_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/dawei_fasttext.model
FastText model for dawei saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/dawei_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/mon_word2vec.model
Word2Vec model for mon saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/mon_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/mon_fasttext.model
FastText model for mon saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/mon_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/pao_word2vec.model
Word2Vec model for pao saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/pao_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/pao_fasttext.model
FastText model for pao saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/pao_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/po_kayin_word2vec.model
Word2Vec model for po_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/po_kayin_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/po_kayin_fasttext.model
FastText model for po_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/po_kayin_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/rakhine_word2vec.model
Word2Vec model for rakhine saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/rakhine_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/rakhine_fasttext.model
FastText model for rakhine saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/rakhine_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/sgaw_kayin_word2vec.model
Word2Vec model for sgaw_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/sgaw_kayin_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/sgaw_kayin_fasttext.model
FastText model for sgaw_kayin saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/sgaw_kayin_fasttext.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/shan_word2vec.model
Word2Vec model for shan saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/word2vec/shan_word2vec.model
Model saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/shan_fasttext.model
FastText model for shan saved to /home/ye/exp/sylbreak4all/lang_detection/embedding/fasttext/shan_fasttext.model
Training completed for all languages.

real	0m27.970s
user	0m55.788s
sys	1m0.233s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./detect_languages.sh 
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: beik.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: dawei.txt - Detected Language with Word2Vec: Detected language: pao_word2vec
File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: pao.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: rakhine.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: shan.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
File: beik.txt - Detected Language with FastText: Detected language: mon_fasttext
File: dawei.txt - Detected Language with FastText: Detected language: mon_fasttext
File: mon_tst.txt - Detected Language with FastText: Detected language: mon_fasttext
File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: rakhine.txt - Detected Language with FastText: Detected language: mon_fasttext
File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: shan.txt - Detected Language with FastText: Detected language: mon_fasttext
Language detection completed for all files.

real	0m26.840s
user	0m32.244s
sys	1m20.651s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ 
```

minimum count = 2 ထားကြည့်လည်း အဆင်မပြေဘူး။   
ပြောရရင်တော့ corpus size ကသေးတာလည်း ပါတယ်။    


ပြီးတော့ ဗမာရယ်၊ ထားဝယ်ရယ်၊ ဘိတ်ရယ်၊ ရခိုင်ရယ်က ခွဲရခက်တယ်။   

## Try with Neural Network Based Classification Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural/syl_seg$ wc *
   35913   660272  6590499 bamar.all.syl
    6622    68076   622819 beik.all.syl
    6622    67245   664090 dawei.all.syl
   10631   110432  1089569 mon.all.syl
   18353   185917  2157437 pao.all.syl
   19141   234735  1973706 po_kayin.all.syl
   18373   231636  2158947 rakhine.all.syl
   68571   842883  7316575 sgaw_kayin.all.syl
   16555   153757  1924376 shan.all.syl
  200781  2554953 24498018 total
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural/syl_seg$
```

## Combine All Language Data as a Big File

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ ./combine_languages.sh 
Processed ./syl_seg/bamar.all.syl
Processed ./syl_seg/beik.all.syl
Processed ./syl_seg/dawei.all.syl
Processed ./syl_seg/mon.all.syl
Processed ./syl_seg/pao.all.syl
Processed ./syl_seg/po_kayin.all.syl
Processed ./syl_seg/rakhine.all.syl
Processed ./syl_seg/sgaw_kayin.all.syl
Processed ./syl_seg/shan.all.syl
All files have been combined into combined_language_data.txt
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ ls
combined_language_data.txt  model                  syl_seg  train_neural_models.sh
combine_languages.sh        neural_lang_detect.py  tmp
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ wc ./combined_language_data.txt 
  200781  2755734 26058583 ./combined_language_data.txt
```

Check the file content:    

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head combined_language_data.txt 
နေ က မီး ကျီး ခဲ လို ရဲ ရဲ တောက် ပြီး တက် လာ တယ် ပြီး တော့ ငါ တို့ ရပ် နိုင် ရုံ လောက် ပဲ ရှိ ပေ မဲ့ အ ခု ဘယ် နည်း နဲ့ မ ဆို တိုက် ခိုက် ရ တော့ မယ် စစ် သည် ရဲ မက် တွေ မ ဟုတ် ဘူး တစ် ယောက် ချင်း တိုက် ခိုက် တာ မ ဟုတ် ဘူး ဒါ က ရန် ပွဲ တစ် ပွဲ	bamar
တော မီး တွေ နဲ့ ရေ ကြီး မှု တွေ ရဲ့ ဘေး ဒဏ် ကို ခံ ခဲ့ ရ တဲ့ အ မေ ရိ ကန် ပြည် ထောင် စု တစ် ခွင် က မိ သား စု တွေ အ တွက် ကြက် ခြေ နီ အ ဖွဲ့ က ထောက် ပံ့ မှု တွေ ပေး နေ တယ်	bamar
ဒီ ည နေ ကျွန် တော် တို့ ရဲ့ ပွဲ ကို အ စီ အ စဉ် မှူး အ ဖြစ် ဆောင် ရွက် ပေး သူ က တော့ ချစ် စ ရာ ကောင်း တဲ့ ဖြစ် ပါ တယ်	bamar
ဒါ က ဘာ အ တွက် လဲ ဆို တာ မှန်း ကြည့်	bamar
မင်း ရော ငါ ရော မင်း ရဲ့ ခွေး လေး ရော ငါ တို့ ရဲ့ သိ မြင် နား လည် မှု စ ကြ ဝ ဠာ နယ် ပယ် တစ် ခု ထဲ မှာ ပိတ် မိ နေ ကြ တယ် ငါ တို့ လွတ် မြောက် နိုင် ရင် အ ရာ ဝတ္ထု တွေ ကို မြင် နိုင် တဲ့ တ ခြား နည်း လမ်း တွေ အ များ ကြီး ရှိ လာ မယ်	bamar
သူ တို့ အ လုပ် ခွင် ရဲ့ သ နား စ ရာ အ ခြေ အ နေ ဟာ အ ရင် က ထက် ပို ပြီး အ ခက် အ ခဲ တွေ နဲ့ ရင် ဆိုင် လာ ရ တယ်	bamar
လုပ် ဖော် ကိုင် ဖက် အ သစ် ဒီ နေ့ အ ပြင် မှာ အ ရမ်း အေး တာ တောင် မှ ပတ် ဝန်း ကျင် ထိန်း သိမ်း ရေး အ တွက် ကြံ့ ကြံ့ ခံ နေ တုန်း ပဲ	bamar
တန် နဲ့ ချီ တဲ့ ပိုး ကောင် တွေ ငါ့ ရှေ့ က နေ ရာ တိုင်း မှာ ငါ သေ တော့ မယ် လို့ ငါ ထင် တယ်	bamar
သို့ ဟား ဟား ဟား မင်း ငါ့ ကို လွမ်း နေ မှာ ပဲ အဲ ဒါ ကို ဝန် ခံ လိုက် တာ လုံး ဝ ကောင်း ပါ တယ်	bamar
အ ပြင် က စာ ရွက် အ ရွယ် အ စား ထက် ကျော် လွန် ပြီး လျှံ ထွက် နေ တဲ့ စာ သား တွေ နဲ့ ဖွဲ့ ပြီး သား စာ မျက် နှာ တွေ ကို ခေါက် လိုက် အဲ ဒါ ကို လို့ လည်း ခေါ် တယ်	bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ tail ./combined_language_data.txt 
ဢၼ် ၼႆႉ တႄႉ ႁဝ်း ၶႃႈ တေ ႁဵတ်း လႆႈ ဢမ်ႇ ၸႂ်ႈ	shan
လွင်ႈ တၢင်း မၼ်းႄ တႉ ၵွပ်ႈ ယုမ်ႇၽ်ႂ ၵေႃႈ ဢမ်ႇ လႆႈႄ လႈ ၶႃႈ ၸင်ႇ လႆႈ ႁဵတ်း ဢေႃႈ ဢၼ် ၼႆႉ	shan
ၸႂ် သူ တူင်ႉ ၽူင်ႉ ယူႇ ႁႃႉ	shan
ထိုင် ၼွၵ်ႈ တၢင်း လူင် ၼၼ်ႉ ဢိူဝ်ႈ	shan
ၶႃႈ ႁဝ်း ၶဝ်ႈ ၸႂ် ႁိူၼ်း ဢၼ် ပႃး ႁွင်ႈ ၼွၼ်း တႃႇ သွင် ၵေႃႉ ၼၼ်ႉ	shan
ယွၵ်ႇ ထၢမ် မၼ်း တူၺ်း လေႃႇ	shan
ၶၢႆ ယူႇ ယဝ်ႉ ႁႃႉ	shan
ၼမ်ႉ တႃ ၶႃႈ လႆႈ တူၵ်း ႁႃႉ	shan
မိူဝ်ႈ ၶမ်ႈ ဝႃး ၶီႇ မေႃႇ ၼမ်ႉ ၵမ်း ၼိုင်ႈ ပဵၼ် ႁိုဝ် လၢတ်ႈ​ႄ ၼေ ႁဝ်း တူၺ်း	shan
သူ ဢမ်ႇ ႁဵတ်း သင် ႁႃႉ	shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ 
```

## Shuffle

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ shuf ./combined_language_data.txt > ./all_languages.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./all_languages.txt 
၁ ၀ စက္ကန့်	bamar
သ လၣ် လီၤ ဖီ တ ဖၣ် ဧါ	sgaw_kayin
ကျွန် မ လာ ချင် ရယ် ပဲ့ လာ ဝို မ ရ က ။	beik
အဝ်ႏ အ ခန်ꩻ ဖဲ ချာ နဝ်ꩻ ဟွိုန် စဲင်း တဝ်း နာꩻ ငဝ်း	pao
တ သ့ ဖဲ အ သ့ တၢ် ဝဲ န့ၣ် ဆှၢ လီၤ ဒၣ် ချ့ ချ့ တ က့ၢ်	sgaw_kayin
အ ဝဲ လဲၤ ဝဲ ဖဲ လဲၣ် လဲၣ် န့ၣ် ယ တ သ့ၣ် ညါ ဝဲ တီ တီ ဘၣ်	sgaw_kayin
သူ က က ကောင်း ဟောင် နီ လို့ ငါ အိမ် နီး ချင်း တိ က ရက် ပြတ် က န့် ကွက် နီ ရေ ။	rakhine
ငါ့ ဘ ဝ ရဲ့ အ ကောင်း ဆုံး ည ကို စွန့် ခွာ ရ တော့ မယ် ငါ ငို မိ တော့ မယ်	bamar
နွံ က ထိ တ က ယၤ သၢ ဆံ	sgaw_kayin
ၶဝ် ဢမ်ႇ ၵူဝ် သူ	shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ tail ./all_languages.txt 
ယ က ဘၪ မၩ ပျၩ့ ခွံၬ ဆၧ နီၪ လ ဖၪ ဒံၭ လီၫ	po_kayin
အ ဝဲ မံ လီၤ လၢ လီၢ် ဆ့ၣ် နီၤ က ပုာ် လိၤ ဒီး တ ယံာ် ဘၣ် မံ ဘၣ် အ သး လီၤ	sgaw_kayin
အ ဝဲ န့ၣ် မ့ၢ် ဝဲ ပှၤ ကဲ ဒိၣ် အ နီၢ် ကီၢ် န့ၣ် လီၤ	sgaw_kayin
အင်း အ မဲ သား အ စပ် စပ် တဲ့ နေ ရာ မှာ တော့ ချုံ ကင်း က နာ မည် ကျော် ပဲ	bamar
လီၢ ဂၢ် အ သး ထီၣ်	sgaw_kayin
ၶဝ် လၢတ်ႈ ဢီႈ သင် ၵေႃႈ ယဝ်ႉ ႁဝ်း ယုမ်ႇ မၼ်း	shan
ယို နဝ်ꩻ ပို မုဲင်ꩻ တ သီႏ တ ငါꩻ ပွတ် နဲး	pao
အီ လၢ ခံ တၢ် မ့ၢ် လိၣ် န့ၣ် ဘျး စဲ ယၤ န့ၣ် တ က့ၢ်	sgaw_kayin
ဝွေꩻ မူႏ နဝ်ꩻ တ ရေ မွေး ငါႏ တွော့ꩻ ရက် ခꩻ ရာႏ ဟဝ် မွေး	pao
ကၠံ ဏံ ရာန် တုဲ မၞိဟ် စ ဍုၚ် ဂှ် မိက် ဂွံ ပံၚ် ထောံ ကဵု ကၠံ ညး ရ ။	mon
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

## Code

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ python ./neural_lang_detect.py --help
2024-01-20 21:05:02.988412: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:05:03.013218: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:05:03.335806: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
usage: neural_lang_detect.py [-h] --mode {train,detect} [--input INPUT] [--output OUTPUT]
                             [--model_folder MODEL_FOLDER] [--num_words NUM_WORDS]
                             [--max_len MAX_LEN] [--epochs EPOCHS] [--batch_size BATCH_SIZE]

Neural Network-based language detection.

optional arguments:
  -h, --help            show this help message and exit
  --mode {train,detect}
                        Mode of operation: train or detect
  --input INPUT         Input file path for training or detection.
  --output OUTPUT       Output file path for saving the model and artifacts (train mode only).
  --model_folder MODEL_FOLDER
                        Folder path containing saved model and artifacts (detect mode only).
  --num_words NUM_WORDS
                        Number of words to consider from the dataset (default: 10000)
  --max_len MAX_LEN     Maximum length of the sequences (default: 100)
  --epochs EPOCHS       Number of epochs for training (default: 10)
  --batch_size BATCH_SIZE
                        Batch size for training (default: 32)
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ 
```

Shell script ...   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat train.sh
#!/bin/bash

python ./neural_lang_detect.py --mode train --input ./all_languages.txt --output model
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

Training ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ time ./train.sh | tee train.log
2024-01-20 21:09:54.929897: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:09:54.955162: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:09:55.277479: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:09:56.685290: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:09:56.702281: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
Epoch 1/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.2118 - accuracy: 0.9361 - val_loss: 0.0222 - val_accuracy: 0.9944
Epoch 2/10
5018/5018 [==============================] - 7s 1ms/step - loss: 0.0187 - accuracy: 0.9942 - val_loss: 0.0217 - val_accuracy: 0.9930
Epoch 3/10
5018/5018 [==============================] - 8s 1ms/step - loss: 0.0128 - accuracy: 0.9958 - val_loss: 0.0165 - val_accuracy: 0.9945
Epoch 4/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0109 - accuracy: 0.9964 - val_loss: 0.0135 - val_accuracy: 0.9955
Epoch 5/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0091 - accuracy: 0.9970 - val_loss: 0.0125 - val_accuracy: 0.9957
Epoch 6/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0083 - accuracy: 0.9973 - val_loss: 0.0129 - val_accuracy: 0.9957
Epoch 7/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0077 - accuracy: 0.9974 - val_loss: 0.0178 - val_accuracy: 0.9946
Epoch 8/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0071 - accuracy: 0.9976 - val_loss: 0.0167 - val_accuracy: 0.9948
Epoch 9/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0067 - accuracy: 0.9977 - val_loss: 0.0146 - val_accuracy: 0.9951
Epoch 10/10
5018/5018 [==============================] - 8s 2ms/step - loss: 0.0064 - accuracy: 0.9978 - val_loss: 0.0135 - val_accuracy: 0.9957
/home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages/keras/src/engine/training.py:3000: UserWarning: You are saving your model as an HDF5 file via `model.save()`. This file format is considered legacy. We recommend using instead the native Keras format, e.g. `model.save('my_model.keras')`.
  saving_api.save_model(
Model and artifacts saved to model

real	1m19.423s
user	7m57.563s
sys	0m58.524s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

## Testing

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ time python neural_lang_detect.py --mode detect --input ./eg_input/bamar_burmese.txt --model_folder model
2024-01-20 21:18:27.642233: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:18:27.667426: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:18:27.989553: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:18:28.473618: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:18:28.490949: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 38ms/step
Detected language: bamar

real	0m1.352s
user	0m2.390s
sys	0m3.586s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

## Prepare a Shell Script for Testing all with Neural Network based Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat detect_languages.sh 
#!/bin/bash

# Directory containing the language files
input_dir="./eg_input/"

# Directory of the trained model
model_dir="model"

# Loop through each .txt file in the input directory
for file in "$input_dir"*.txt; do
    echo "Processing $file..."
    python neural_lang_detect.py --mode detect --input "$file" --model_folder "$model_dir"
    echo ""
done

echo "Language detection completed for all files."

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ 
```

## Testing for All Burmese Languages

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ time ./detect_languages.sh | tee detect.log
Processing ./eg_input/bamar_burmese.txt...
2024-01-20 21:22:21.608441: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:21.633258: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:21.952891: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:22.432631: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:22.450100: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 38ms/step
Detected language: bamar

Processing ./eg_input/beik.txt...
2024-01-20 21:22:22.944377: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:22.969053: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:23.289539: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:23.771992: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:23.789532: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: beik

Processing ./eg_input/dawei.txt...
2024-01-20 21:22:24.295844: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:24.320779: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:24.642128: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:25.123797: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:25.141616: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 39ms/step
Detected language: dawei

Processing ./eg_input/mon_tst.txt...
2024-01-20 21:22:25.637773: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:25.663649: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:25.983829: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:26.465161: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:26.482732: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing ./eg_input/mon.txt...
2024-01-20 21:22:26.970805: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:26.995944: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:27.317124: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:27.803254: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:27.820961: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing ./eg_input/pao.txt...
2024-01-20 21:22:28.311601: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:28.336882: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:28.660350: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:29.140149: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:29.157860: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 42ms/step
Detected language: pao

Processing ./eg_input/po_kayin.txt...
2024-01-20 21:22:29.673061: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:29.698125: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:30.018720: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:30.500767: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:30.518209: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin

Processing ./eg_input/rakhine.txt...
2024-01-20 21:22:31.005617: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:31.030484: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:31.349363: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:31.837688: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:31.855138: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine

Processing ./eg_input/sgaw_kayin.txt...
2024-01-20 21:22:32.340294: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:32.365132: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:32.686742: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:33.166553: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:33.184256: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 36ms/step
Detected language: sgaw_kayin

Processing ./eg_input/shan.txt...
2024-01-20 21:22:33.670888: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-01-20 21:22:33.695677: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-01-20 21:22:34.018121: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2024-01-20 21:22:34.497406: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2024-01-20 21:22:34.515329: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
1/1 [==============================] - 0s 37ms/step
Detected language: mon

Language detection completed for all files.

real	0m13.441s
user	0m23.905s
sys	0m36.886s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

## Check the Log File

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat detect.log 
Processing ./eg_input/bamar_burmese.txt...
1/1 [==============================] - 0s 38ms/step
Detected language: bamar

Processing ./eg_input/beik.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: beik

Processing ./eg_input/dawei.txt...
1/1 [==============================] - 0s 39ms/step
Detected language: dawei

Processing ./eg_input/mon_tst.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing ./eg_input/mon.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing ./eg_input/pao.txt...
1/1 [==============================] - 0s 42ms/step
Detected language: pao

Processing ./eg_input/po_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin

Processing ./eg_input/rakhine.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine

Processing ./eg_input/sgaw_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: sgaw_kayin

Processing ./eg_input/shan.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: mon

Language detection completed for all files.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

## To Do

-- Add Kachin, Rawang, Kayar-Li, Mizo Chin data and make experiment again  
-- Testing with some mixed test file (e.g. 30% bamar, 10% Rakhine, 60% Shan)    

## Experiment with Syllable Frequency Dictionary

Date: 22 Jan 2024  

I updated the char_freq_lang_detect.py for syllable units.  
Language profile buildings ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ time ./build_dict.sh
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/bamar_profile.json
Created syllable language profile for bamar
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/beik_profile.json
Created syllable language profile for beik
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/dawei_profile.json
Created syllable language profile for dawei
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/mon_profile.json
Created syllable language profile for mon
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/pao_profile.json
Created syllable language profile for pao
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/po_kayin_profile.json
Created syllable language profile for po_kayin
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/rakhine_profile.json
Created syllable language profile for rakhine
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/sgaw_kayin_profile.json
Created syllable language profile for sgaw_kayin
Syllable frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/syl_freq_dict/profile/shan_profile.json
Created syllable language profile for shan
All language profiles have been created.

real    0m3.114s
user    0m2.776s
sys     0m0.337s
```

Check the dictionary json file:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict/profile$ jq . ./bamar_profile.json | head
{
  "နေ ": 0.010775065583404521,
  "က ": 0.019714401691536862,
  "မီး ": 0.0012071587391022495,
  "ကျီး ": 1.8175539359130483e-05,
  "ခဲ ": 0.00042561054665963877,
  "လို ": 0.00487710306136668,
  "ရဲ ": 0.000395317981061088,
  "တောက် ": 0.00016660911079202943,
  "ပြီး ": 0.00696426083110683,
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict/profile$ jq . ./shan_profile.json | head
{
  "ယွင်ႈ ၵုင်ႇ ၵူၼ်း ႁတ်း ႁၢၼ် ႁႃႉ ဢၼ် ၸႅတ်ႈ ": 1.3365231686291281e-05,
  "တူၺ်း ": 0.0039694738108285105,
  "သူ ႁေႃႈ ၵႃး ၼႆႉ ": 1.3365231686291281e-05,
  "တွပ်ႇ ": 0.0012563317785113804,
  "ယဝ်ႉ ": 0.011039681372876598,
  "ယဝ်ႉ ႁႃႉ ": 0.0012162360834525067,
  "လွင်ႈ ၶူင် ": 1.3365231686291281e-05,
  "သၢင်ႈ ": 0.0002806698654121169,
  "မႂ်း ဢမ်ႇ ႁိုင် ": 1.3365231686291281e-05,
```

Recheck the character level profile:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict/profile$ jq . ./bamar_profile.json | head
{
  "န": 0.023469469401902053,
  "ေ": 0.03631757237178158,
  " ": 0.2367811218853845,
  "က": 0.03867437884023886,
  "မ": 0.0258740566611921,
  "ီ": 0.010828037313005514,
  "း": 0.04465342430897031,
  "ျ": 0.01338279277205567,
  "ခ": 0.011615661936494779,
```

For the comparison, the followings are the detection results for character freq dictionary approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ time ./detect_languages.sh
File: bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json
File: beik.txt - Detected Language: Detected language: rakhine_profile.json
File: dawei.txt - Detected Language: Detected language: beik_profile.json
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
File: mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json
File: pao.txt - Detected Language: Detected language: pao_profile.json
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
File: shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Language detection completed for all files.

real    0m0.251s
user    0m0.153s
sys     0m0.023s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$
```

OK. Let's make detection with syllable units ...   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ time ./detect_languages.sh
File: bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json
File: beik.txt - Detected Language: Detected language: beik_profile.json
File: dawei.txt - Detected Language: Detected language: dawei_profile.json
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
File: mon.txt - Detected Language: Detected language: mon_profile.json
File: pao.txt - Detected Language: Detected language: pao_profile.json
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
File: shan.txt - Detected Language: Detected language: beik_profile.json
Language detection with syllable freq dictionary approach completed for all files.

real    0m0.485s
user    0m0.411s
sys     0m0.075s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$
```

Syllable freq dictionary apprach provide the better results. Happy! :)  
ဒီတစ်ခါတော့ syllable freq dictionary based approach နဲ့ neural network classification approach နှစ်ခုရဲ့ ရလဒ်တွေကို နှိုင်းယှဉ်ကြည့်ချင်တယ်။  

Neural network result are as follows:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat detect2.log
Processing ./eg_input/bamar_burmese.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: bamar

Processing ./eg_input/beik.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: beik

Processing ./eg_input/dawei.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: dawei

Processing ./eg_input/mon_tst.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing ./eg_input/mon.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: mon

Processing ./eg_input/pao.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: pao

Processing ./eg_input/po_kayin.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: po_kayin

Processing ./eg_input/rakhine.txt...
1/1 [==============================] - 0s 42ms/step
Detected language: rakhine

Processing ./eg_input/sgaw_kayin.txt...
1/1 [==============================] - 0s 38ms/step
Detected language: sgaw_kayin

Processing ./eg_input/shan.txt...
1/1 [==============================] - 0s 38ms/step
Detected language: mon

Language detection completed for all files.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ Syllable-based Freq Dictionary ရော Neural Network Classification ရောက ရှမ်းဘာသာစကားကို detect လုပ်တဲ့အခါမှာ မှားနေတာကို သွားတွေ့ရတယ်။  
Syllable-based freq က ရှမ်းကို ဘိတ်ဘာသာစကားလို့ detect ဖြစ်တယ်။  
Neural Network Classification မှာကျတော့ ရှမ်းကို မွန် ဆိုပြီးတော့ detect သွားဖြစ်နေတယ်။  

## Let's Check Training and Testing Data Files of Shan, Mon and Beik

For Shan:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./syl_seg/shan.all.syl
ယွင်ႈ ၵုင်ႇ ၵူၼ်း ႁတ်း ႁၢၼ် ႁႃႉ
ဢၼ် ၸႅတ်ႈ တူၺ်း သူ ႁေႃႈ ၵႃး ၼႆႉ တွပ်ႇ ယဝ်ႉ ယဝ်ႉ ႁႃႉ
လွင်ႈ ၶူင် သၢင်ႈ မႂ်း ဢမ်ႇ ႁိုင် သင် တေ ဢွင်ႇ မၢၼ် ယဝ်ႉ
ဢၼ် ၼၼ်ႉ ပဵၼ် လွင်ႈ ၵိတ်ႇ ၶွင်ႈ သူ
တေ ၵိၼ် သေ ဢၼ် ဢၼ် ႁႃႉ
ဢွမ် မူင်း ၵဝ် ႁႃ ဢမ်ႇ ႁၼ်
ပဵၼ် ၵူၼ်း ဢၼ် လဵၼ်ႈ ၸိူင်း ၶႅၼ်ႇႄ တႉ ယဝ်ႈ
ၵုပ်ႉ ၵူႈ သူ ၼႆႉ တႄႇ ၽုၺ်ႇ သႅင်ႇ ၵိၼ် ယမ်ႉ ၼႆႉ မႃး တေႃႇ မိူဝ်ႈ လဵဝ် ဢၼ် ၽႅဝ် မႃး ၼႆႉ ပဵၼ် ႙ ႙ ႙ ၵူႈ ယဝ်ႉ
ၼင်ႈ ႁွင်ႈ တၢင်း ၼႃႈ ဢဝ် ၼႄႈ
လႆႈ ႁႅင်း လီ ၵႃႈ ႁိုဝ်
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./eg_input/shan.txt
မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

For Mon language:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./syl_seg/mon.all.syl
၂ ၀ မိ ဏေတ် ပၠန် တှ်ေ ဘာ ရပ် ဏောၚ် ။
ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./eg_input/mon.txt
ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

For Beik language:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./syl_seg/beik.all.syl
နင် ဘာ စီ စဉ် နေ ရယ် ဆို တာ ငါ့ ဝို ပြော သင့် ပေါ့ လန်း ။
သူ လို့ စာ အုပ် သုံး ထောင် ကျော် ရောင်း ပီး ဟော ဘီ ။
ငယ် ငယ် တည်း က မင်း သား လုပ် ဝို့ ဝါ သ နာ ပါ စ ။
ငယ် ငယ် တည်း က မင်း သား လုပ် ဝို့ ဝါ သ နာ ပါ စ ။
ဒယ် ကောင် မ ငယ် နင့် ဝို ဂ ရု စိုက် ရယ် လား ။
ဘ ဇာ လောက် မြ င့် မြတ် ရိ ။
နင် ဒယ် မှာ အ လုပ် လုပ် ဝယ် ။
ဒယ် ကောင် မ ငယ် ဟ မင်း ဟက် သ ဘော တူ မှာ မ ဟုတ် ဝ ။
နင့် ရဲ့ သွား နှစ် ချောင်း ကို နုတ် ပစ် ရ မရ် ။
သူ့ ဆီ ကို နင် ဖုန်း ဆက် မယ် မ ဟုတ် ဝ လား ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ head ./eg_input/beik.txt
ဖယ် သူ လေ ကို မေး ရိ လဲ ။
သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

ဒေတာဖိုင်တွေမှာတော့ အမှားမရှိဘူး။ freq, calculated probability တွေရဲ့ တန်ဖိုး နီးစပ်တာတွေကြောင့် ဖြစ်တဲ့ အမှားလို့ပဲ ယူဆတယ်။  
ခေါင်းစားတယ်ကွာ ...  

ဒီတခါတော့ FastText နဲ့ ကြိုးစားကြည့်မယ်။  

## Format Conversion into FastText

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ python ./fasttext_format_converter.py --input ./all_languages.txt --output ./all_languages.fasttext
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ head ./all_languages.fasttext
__label__bamar  ၁ ၀ စက္ကန့်
__label__sgaw_kayin     သ လၣ် လီၤ ဖီ တ ဖၣ် ဧါ
__label__beik   ကျွန် မ လာ ချင် ရယ် ပဲ့ လာ ဝို မ ရ က ။
__label__pao    အဝ်ႏ အ ခန်ꩻ ဖဲ ချာ နဝ်ꩻ ဟွိုန် စဲင်း တဝ်း နာꩻ ငဝ်း
__label__sgaw_kayin     တ သ့ ဖဲ အ သ့ တၢ် ဝဲ န့ၣ် ဆှၢ လီၤ ဒၣ် ချ့ ချ့ တ က့ၢ်
__label__sgaw_kayin     အ ဝဲ လဲၤ ဝဲ ဖဲ လဲၣ် လဲၣ် န့ၣ် ယ တ သ့ၣ် ညါ ဝဲ တီ တီ ဘၣ်
__label__rakhine        သူ က က ကောင်း ဟောင် နီ လို့ ငါ အိမ် နီး ချင်း တိ က ရက် ပြတ် က န့် ကွက် နီ ရေ ။
__label__bamar  ငါ့ ဘ ဝ ရဲ့ အ ကောင်း ဆုံး ည ကို စွန့် ခွာ ရ တော့ မယ် ငါ ငို မိ တော့ မယ်
__label__sgaw_kayin     နွံ က ထိ တ က ယၤ သၢ ဆံ
__label__shan   ၶဝ် ဢမ်ႇ ၵူဝ် သူ
```

input and output ဖိုင်တွေရဲ့ line no. ကို confirmation လုပ်ခဲ့...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ wc all_languages.txt
  200781  2755734 26058583 all_languages.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ wc all_languages.fasttext
  200721  2755674 27864739 all_languages.fasttext
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$
```

လက်ရှိ စက်ထဲမှာက fasttext ကို ငါ install လုပ်ထားပြီးသား ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ fasttext --help
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              train a supervised classifier
  quantize                quantize a model to reduce the memory usage
  test                    evaluate a supervised classifier
  test-label              print labels with precision and recall scores
  predict                 predict most likely labels
  predict-prob            predict most likely labels with probabilities
  skipgram                train a skipgram model
  cbow                    train a cbow model
  print-word-vectors      print word vectors given a trained model
  print-sentence-vectors  print sentence vectors given a trained model
  print-ngrams            print ngrams given a trained model and word
  nn                      query for nearest neighbors
  analogies               query for analogies
  dump                    dump arguments,dictionary,input/output vectors

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Python module လည်း ခေါ်သုံးတာ အိုကေမယ်လို့ ထင်တယ်။ import လုပ်ကြည့်တော့ အောက်ပါအတိုင်း ခေါ်သုံးလို့ ရတာကို တွေ့ရတယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fasttext as ft
>>> print(dir(ft))
['BOW', 'EOS', 'EOW', 'FastText', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__', 'absolute_import', 'cbow', 'division', 'load_model', 'print_function', 'skipgram', 'supervised', 'tokenize', 'train_supervised', 'train_unsupervised', 'unicode_literals']
>>>
```

Coding လုပ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --help
usage: fasttext_lang_detect.py [-h] --mode {train,test,predict} [--input INPUT]
                               [--output OUTPUT] [--model MODEL] [--epoch EPOCH]
                               [--lr LR] [--wordNgrams WORDNGRAMS]

Language identification using FastText.

optional arguments:
  -h, --help            show this help message and exit
  --mode {train,test,predict}
                        Mode of operation: train, test or predict
  --input INPUT         Input file path for training or testing. Input text for
                        prediction.
  --output OUTPUT       Output file path for saving the model (train mode only).
  --model MODEL         Model file path for testing or prediction.
  --epoch EPOCH         Number of epochs for training (default: 25)
  --lr LR               Learning rate for training (default: 1.0)
  --wordNgrams WORDNGRAMS
                        Max length of word ngram (default: 2)
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Training/Testing ခွဲပြီး experiment လုပ်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ head -n 200000 ./all_languages.fasttext > train.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ tail -n 721 ./all_languages.fasttext > test.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Training with FastText model ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time python ./fasttext_lang_detect.py --mode train --input ./train.txt --output ./train.model.bin --epoch 25 --lr 1.0 --wordNgrams 3
Read 2M words
Number of words:  15381
Number of labels: 9
Progress:   4.9% words/sec/thread: 1556984 lr:  0.950655 avg.loss:  0.059528 ETA:   0h 0m Progress:   9.9% words/sec/thread: 1562792 lr:  0.901482 avg.loss:  0.032610 ETA:   0h 0m Progress:  14.8% words/sec/thread: 1564407 lr:  0.852362 avg.loss:  0.023593 ETA:   0h 0m Progress:  19.7% words/sec/thread: 1565109 lr:  0.803305 avg.loss:  0.018418 ETA:   0h 0m Progress:  24.6% words/sec/thread: 1565488 lr:  0.754252 avg.loss:  0.015274 ETA:   0h 0m Progress:  29.4% words/sec/thread: 1563239 lr:  0.705680 avg.loss:  0.013234 ETA:   0h 0m Progress:  34.3% words/sec/thread: 1563254 lr:  0.656738 avg.loss:  0.011585 ETA:   0h 0m Progress:  39.2% words/sec/thread: 1563258 lr:  0.607850 avg.loss:  0.010342 ETA:   0h 0m Progress:  44.1% words/sec/thread: 1563400 lr:  0.558921 avg.loss:  0.009394 ETA:   0h 0m Progress:  49.0% words/sec/thread: 1563438 lr:  0.510034 avg.loss:  0.008639 ETA:   0h 0m Progress:  53.9% words/sec/thread: 1563514 lr:  0.461112 avg.loss:  0.008095 ETA:   0h 0m Progress:  58.8% words/sec/thread: 1563698 lr:  0.412156 avg.loss:  0.007537 ETA:   0h 0m Progress:  63.7% words/sec/thread: 1563641 lr:  0.363284 avg.loss:  0.007074 ETA:   0h 0m Progress:  68.6% words/sec/thread: 1563688 lr:  0.314375 avg.loss:  0.006743 ETA:   0h 0m Progress:  73.4% words/sec/thread: 1563648 lr:  0.265504 avg.loss:  0.006355 ETA:   0h 0m Progress:  78.2% words/sec/thread: 1561739 lr:  0.217579 avg.loss:  0.006029 ETA:   0h 0m Progress:  83.1% words/sec/thread: 1561460 lr:  0.168874 avg.loss:  0.005785 ETA:   0h 0m Progress:  88.0% words/sec/thread: 1561408 lr:  0.120084 avg.loss:  0.005508 ETA:   0h 0m Progress:  92.9% words/sec/thread: 1561391 lr:  0.071268 avg.loss:  0.005261 ETA:   0h 0m Progress:  97.8% words/sec/thread: 1561403 lr:  0.022439 avg.loss:  0.005048 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1521270 lr: -0.000012 avg.loss:  0.004959 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1520959 lr:  0.000000 avg.loss:  0.004959 ETA:   0h 0m 0s
Model saved to ./train.model.bin

real    0m3.016s
user    0m48.955s
sys     0m2.642s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Testing with 721 lines test data ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time python ./fasttext_
lang_detect.py --mode test --model ./train.model.bin --input test.txt | tee test.log
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Number of test examples: 721
Precision at 1: 0.997
Recall at 1: 0.997

real    0m0.385s
user    0m0.708s
sys     0m2.230s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for each line:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time python ./fasttext_
lang_detect.py --mode predict --model ./train.model.bin --input "တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: bamar

real    0m0.402s
user    0m0.778s
sys     0m2.176s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Beik dialect ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ (base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: beik
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Dawei dialect ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: dawei
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Mon dialect ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: mon
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Pao language ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: pao
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Po Kayin ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ ."
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: po_kayin
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Rakhine dialect ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "ထို မ ချေ ကို သူ အ မှန် မ မြတ် ။"ုး ခ ပါ"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: rakhine
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Rakhine again ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "မင်း တောင် တိ ကို တက် နီ ကျ လား ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: rakhine
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Sgaw Kayin ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ ."
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: sgaw_kayin
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Predicting for Shan language ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: mon
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: mon
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ််ႈ မႃး  ႁႃႉ ။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Predicted language: shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

အထက်ပါအတိုင်းပဲ FastText approach မှာလည်း ရှမ်းနဲ့ မွန်ကို input လုပ်တဲ့ စာကြောင်းပေါ် မူတည်ပြီးတော့ မှန်မှန်ကန်ကန် မခွဲခြားပေးနိုင်တာကို ရှာဖွေတွေ့ရှိရတယ်။  

## Updating the FastText Code

predicting လုပ်တဲ့အခါမှာ အထက်မှာ မြင်ရတဲ့အတိုင်း Warning တက်နေတယ်။  
Stackoverflow မှာ အောက်ပါ လင့်ကိုတွေ့တယ်။  
https://stackoverflow.com/questions/66353366/cant-suppress-fasttext-warning-load-model-does-not-return  

အရမ်းကြီးကောင်းတဲ့ solution မဟုတ်ပေမဲ့ ...  
အောက်ပါအတိုင်း update လုပ်ခဲ့ ...   

```python
import fasttext

fasttext.FastText.eprint = lambda x: None
```

After updating the code, predict again ...   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ််ႈ မႃး  ႁႃႉ ။"
Predicted language: shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Warning message တော့ မပေးတော့ဘူး ...  

## Updating the Code

လက်ရှိမှာက စာကြောင်း တစ်ကြောင်းချင်းစီ parse လုပ်ပြီးပဲ prediction or testing လုပ်ဖြစ်နေလို့ ဖိုင်နဲ့လည်း testing လုပ်လို့ ရအောင် code ကို update လုပ်ခဲ့တယ်။  
အောက်ပါအတိုင်း လက်ရှိမှာတော့ စာကြောင်း တစ်ကြောင်းစီနဲ့လည်း predict လုပ်လို့ ရသလို ဖိုင်ကို input ပေးပြီးလည်း input လုပ်လို့ ရသွားပြီ။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/mon.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/bamar_burmese.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ််ႈ မႃး  ႁႃႉ ။"
Predicted language: shan
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

ဖိုင် အားလုံးနဲ့ testing or prediction လုပ်ကြည့်ပြီးတော့ ရလာတဲ့ ရလဒ်က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input "./eg_input/bamar_burmese.txt
Predicted language: bamar
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/beik.txt
Predicted language: bamar
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/dawei.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/mon.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/pao.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/po_kayin.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/rakhine.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/sgaw_kayin.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ python ./fasttext_lang_detect.py --mode predict --model ./train.model.bin --input ./eg_input/shan.txt
Predicted language: bamar
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

အထက်ပါအတိုင်းပဲ ဖိုင်တစ်ဖိုင်လုံးကို ထည့်ပြီး predict လုပ်တဲ့အခါမှာတော့ fasttext model ရဲ့ ရလဒ်တွေက အားလုံးကို ဗမာ အဖြစ်ပဲ predict လုပ်ချလိုက်တာကို တွေ့ရတယ်။ အကြောင်းအရင်းကတော့ training လုပ်တုန်းက sentence level လုပ်ပြီး predict လုပ်တဲ့အခါမှာ ဖိုင် အနေနဲ့ (very long sentence) လုပ်တာမို့လို့။ ပြီးတော့ text file တွေထဲမှာက ဗမာစာအတွက် training လုပ်ထားတဲ့ ဖိုင်ရဲ့ ပမာဏက ကြီးတာမို့လို့ စသည်ဖြင့် ...  

## What I Learn Until Now

လက်ရှိအထိ character ngram, syllable ngram, character freq dict, syllable freq dict, embedding (word2vec, fasttext) with Cosine similarity, neural network based classification, FastText library based classification ဆိုပြီး နည်းလည်း အမျိုးမျိုးနဲ့ experiment လုပ်ကြည့်ခဲ့တယ်။  

ဗမာစာနဲ့ same Unicode table မှာ ရှဲလုပ်ပြီးသုံးထားတဲ့ တိုင်းရင်းသား ဘာသာစကားတွေနဲ့ dialect လို့ ခေါ်တဲ့ ဗမာနဲ့ ပိုနီးစပ်တဲ့ ရခိုင်၊ ထားဝယ်၊ ဘိတ် တို့ကို လက်ရှိ ရှိတဲ့ ဒေတာကို သုံးပြီး language identification or language classification experiment လုပ်ရတဲ့အခါမှာ 100% မှန်အောင် မလုပ်ပေးနိုင်သေးဘူး။  

အဲဒီအထဲမှာမှ ငါ မှတ်မိသလောက် လက်တွေ့မှာ သုံးလို့ရနိုင်တာတွေက syllable freq dictionary based approach, neural network based classification နဲ့ FastText library based Classification သုံးမျိုးလားလို့ .... အချိန်ရတဲ့အခါမှာ formal experiment ထပ်လုပ်ချင်တယ်။  

## To Do

- neural network based approach code ကိုလည်း sentence level (ဆိုလိုတာက စာကြောင်းတစ်ကြောင်းတည်းကို command line ကနေ ပေးပြီး) နဲ့ predict/testing လုပ်လို့ ရအောင် code ကို update လုပ်ရန်
- syllable frequency based approach code ကိုလည်း sentence level input ကို support လုပ်အောင် code ကို update လုပ်ရန်

## Updating Syllable Frequency Dictionary Based Approach Code  

File input only မဟုတ်ပဲ စာကြောင်း တစ်ကြောင်းတည်းနဲ့လည်း language detection လုပ်ပေးနိုင်အောင် code ကို ပြင်ရေးခဲ့တယ်။  

```python

    elif args.mode == 'detect':
        if not args.input or not args.profiles:
            print("For detection, both --input and --profiles arguments are required.")
        else:
            profiles = load_profiles(args.profiles)
            
            text = ''
            if os.path.isfile(args.input):
                with open(args.input, 'r', encoding='utf-8') as file:
                    text = file.read()
            else:
                text = args.input

            detected_language = detect_language(text, profiles)
            print(f"Detected language: {detected_language}")

```

I also updated shell script ...  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ cat detect_languages_exp.sh
#!/bin/bash

# Define the base directory, the Python script, and the input directory
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/syl_freq_dict"
PYTHON_SCRIPT="$BASE_DIR/syl_freq_lang_detect.py"
INPUT_DIR="$BASE_DIR/eg_input"
PROFILE_DIR="$BASE_DIR/profile"

# Loop through each file in the eg_input directory
for file in "$INPUT_DIR"/*; do
    # Extract the filename
    filename=$(basename -- "$file")

    # Run the Python script for language detection on the file
    echo "Processing file $filename..."
    detected_language_file=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$file" --profiles "$PROFILE_DIR")
    echo "File: $filename - Detected Language: $detected_language_file"

    # Extract a random sentence from the file
    random_sentence=$(shuf -n 1 "$file")

    # Run the Python script for language detection on the random sentence
    echo "Processing random sentence from $filename: $random_sentence"
    detected_language_sentence=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$random_sentence" --profiles "$PROFILE_DIR")
    echo "Random sentence from $filename - Detected Language: $detected_language_sentence"

    echo ""
done

echo "Language detection with syllable freq dictionary approach completed for all files."

```

Experiment with both input file and random string result for the Syllable Frequency Dictionary Based Approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ time ./detect_languages_exp.sh | tee ./exp1.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json
Processing random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Random sentence from bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Random sentence from beik.txt - Detected Language: Detected language: beik_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: dawei_profile.json
Processing random sentence from dawei.txt: ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Random sentence from dawei.txt - Detected Language: Detected language: dawei_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Random sentence from mon_tst.txt - Detected Language: Detected language: mon_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Random sentence from mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Random sentence from pao.txt - Detected Language: Detected language: pao_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Random sentence from shan.txt - Detected Language: Detected language: shan_profile.json

Language detection with syllable freq dictionary approach completed for all files.

real    0m0.946s
user    0m0.814s
sys     0m0.136s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$
```

Random sentence နဲ့ experiment လုပ်နေတာမို့လို့ ပိုသေချာအောင် အောက်ပါအတိုင်း experiment-2, experiment-3 ကို run ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ time ./detect_languages_exp.sh | tee ./exp2.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json
Processing random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Random sentence from bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Random sentence from beik.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: dawei_profile.json
Processing random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Random sentence from dawei.txt - Detected Language: Detected language: dawei_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Random sentence from mon_tst.txt - Detected Language: Detected language: mon_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon.txt: ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Random sentence from mon.txt - Detected Language: Detected language: mon_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Random sentence from pao.txt - Detected Language: Detected language: pao_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Random sentence from shan.txt - Detected Language: Detected language: shan_profile.json

Language detection with syllable freq dictionary approach completed for all files.

real    0m0.940s
user    0m0.791s
sys     0m0.154s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$
```

Experiment-3 ရဲ့ ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$ time ./detect_languages_exp.sh | tee ./exp3.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json
Processing random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Random sentence from bamar_burmese.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Random sentence from beik.txt - Detected Language: Detected language: rakhine_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: dawei_profile.json
Processing random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Random sentence from dawei.txt - Detected Language: Detected language: dawei_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Random sentence from mon_tst.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Random sentence from mon.txt - Detected Language: Detected language: mon_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Random sentence from pao.txt - Detected Language: Detected language: pao_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Random sentence from shan.txt - Detected Language: Detected language: shan_profile.json

Language detection with syllable freq dictionary approach completed for all files.

real    0m0.944s
user    0m0.805s
sys     0m0.143s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/syl_freq_dict$
```

## Updating Neural Network Based Approach Code  

File input only မဟုတ်ပဲ စာကြောင်း တစ်ကြောင်းတည်းနဲ့လည်း language detection လုပ်ပေးနိုင်အောင် code ကို ပြင်ရေးခဲ့တယ်။  
ပြီးတော့ ဖိုင်ကနေ ရော string အနေနဲ့ရော testing လုပ်နိုင်ဖို့ shell script ကိုလည်း အောက်ပါအတိုင်း ပြင်ရေးခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat detect_languages_exp.sh
#!/bin/bash

# Directory containing the language files
input_dir="./eg_input/"

# Directory of the trained model
model_dir="model"

# Loop through each .txt file in the input directory
for file in "$input_dir"*.txt; do
    echo "Processing file $file..."
    python neural_lang_detect.py --mode detect --input "$file" --model_folder "$model_dir"

    # Pick a random line from the file
    random_string=$(shuf -n 1 "$file")
    echo "Processing random string from $file: $random_string"
    python neural_lang_detect.py --mode detect --input "$random_string" --model_folder "$model_dir"

    echo ""
done
```

Testing/Experiment ကို updated python code, updated shell script နဲ့ ထပ်လုပ်ခဲ့ပြီး ရလာတဲ့ log output က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat ./experiment.log
Processing file ./eg_input/bamar_burmese.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: bamar
Processing random string from ./eg_input/bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
1/1 [==============================] - 0s 36ms/step
Detected language: bamar

Processing file ./eg_input/beik.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: beik
Processing random string from ./eg_input/beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
1/1 [==============================] - 0s 41ms/step
Detected language: beik

Processing file ./eg_input/dawei.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: dawei
Processing random string from ./eg_input/dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
1/1 [==============================] - 0s 37ms/step
Detected language: dawei

Processing file ./eg_input/mon_tst.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon
Processing random string from ./eg_input/mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing file ./eg_input/mon.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon
Processing random string from ./eg_input/mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing file ./eg_input/pao.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: pao
Processing random string from ./eg_input/pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
1/1 [==============================] - 0s 42ms/step
Detected language: pao

Processing file ./eg_input/po_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin
Processing random string from ./eg_input/po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
1/1 [==============================] - 0s 38ms/step
Detected language: po_kayin

Processing file ./eg_input/rakhine.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine
Processing random string from ./eg_input/rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine

Processing file ./eg_input/sgaw_kayin.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: sgaw_kayin
Processing random string from ./eg_input/sgaw_kayin.txt: ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
1/1 [==============================] - 0s 37ms/step
Detected language: sgaw_kayin

Processing file ./eg_input/shan.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: mon
Processing random string from ./eg_input/shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
1/1 [==============================] - 0s 35ms/step
Detected language: shan

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

String က input ဖိုင်ကနေ random ယူထားတာမို့လို့ သေချာအောင် နောက်ထပ် experiment နှစ်ခေါက် ထပ်လုပ်ကြည့်ခဲ့တယ်။  
ဒုတိယမြောက် expeirment ရလဒ်က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat ./experiment2.log
Processing file ./eg_input/bamar_burmese.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: bamar
Processing random string from ./eg_input/bamar_burmese.txt: ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
1/1 [==============================] - 0s 36ms/step
Detected language: bamar

Processing file ./eg_input/beik.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: beik
Processing random string from ./eg_input/beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
1/1 [==============================] - 0s 36ms/step
Detected language: beik

Processing file ./eg_input/dawei.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: dawei
Processing random string from ./eg_input/dawei.txt: ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
1/1 [==============================] - 0s 37ms/step
Detected language: dawei

Processing file ./eg_input/mon_tst.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon
Processing random string from ./eg_input/mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing file ./eg_input/mon.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon
Processing random string from ./eg_input/mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing file ./eg_input/pao.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: pao
Processing random string from ./eg_input/pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
1/1 [==============================] - 0s 36ms/step
Detected language: pao

Processing file ./eg_input/po_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin
Processing random string from ./eg_input/po_kayin.txt: ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin

Processing file ./eg_input/rakhine.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine
Processing random string from ./eg_input/rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
1/1 [==============================] - 0s 37ms/step
Detected language: rakhine

Processing file ./eg_input/sgaw_kayin.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: sgaw_kayin
Processing random string from ./eg_input/sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
1/1 [==============================] - 0s 36ms/step
Detected language: sgaw_kayin

Processing file ./eg_input/shan.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: mon
Processing random string from ./eg_input/shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
1/1 [==============================] - 0s 36ms/step
Detected language: shan

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

တတိယမြောက် Neural Network approach နဲ့ စမ်းကြည့်ခဲ့တဲ့ experimental result က အောက်ပါအတိုင်းပါ။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ cat ./experiment3.log
Processing file ./eg_input/bamar_burmese.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: bamar
Processing random string from ./eg_input/bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
1/1 [==============================] - 0s 36ms/step
Detected language: bamar

Processing file ./eg_input/beik.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: beik
Processing random string from ./eg_input/beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
1/1 [==============================] - 0s 37ms/step
Detected language: beik

Processing file ./eg_input/dawei.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: dawei
Processing random string from ./eg_input/dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
1/1 [==============================] - 0s 36ms/step
Detected language: dawei

Processing file ./eg_input/mon_tst.txt...
1/1 [==============================] - 0s 37ms/step
Detected language: mon
Processing random string from ./eg_input/mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
1/1 [==============================] - 0s 36ms/step
Detected language: mon

Processing file ./eg_input/mon.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: mon
Processing random string from ./eg_input/mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
1/1 [==============================] - 0s 37ms/step
Detected language: mon

Processing file ./eg_input/pao.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: pao
Processing random string from ./eg_input/pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
1/1 [==============================] - 0s 36ms/step
Detected language: pao

Processing file ./eg_input/po_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: po_kayin
Processing random string from ./eg_input/po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
1/1 [==============================] - 0s 44ms/step
Detected language: po_kayin

Processing file ./eg_input/rakhine.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: rakhine
Processing random string from ./eg_input/rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
1/1 [==============================] - 0s 37ms/step
Detected language: rakhine

Processing file ./eg_input/sgaw_kayin.txt...
1/1 [==============================] - 0s 36ms/step
Detected language: sgaw_kayin
Processing random string from ./eg_input/sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
1/1 [==============================] - 0s 41ms/step
Detected language: sgaw_kayin

Processing file ./eg_input/shan.txt...
1/1 [==============================] - 0s 35ms/step
Detected language: mon
Processing random string from ./eg_input/shan.txt: ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
1/1 [==============================] - 0s 36ms/step
Detected language: shan

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$
```

ခုဆိုရင် Neural Network based approach code မှာလည်း file input ရော string input ရော စမ်းလို့ ရသွားပြီ။   
ရလဒ်ကိုလည်း ပို confirm လုပ်လို့ ရတယ်။  

## Updating to Support Both Input filename and String for the Character Frequency Dictionary Based Approach

စာတမ်း ဘာညာ ရေးချင်ရင်လည်း ရေးလို့ ရနိုင်အောင်လို့ experiment အားလုံးကို ညီတူညီမျှ လုပ်နိုင်အောင်၊ char_freq_lang_detect.py ကိုလည်း update လုပ်ခဲ့တယ်။  

```python

    elif args.mode == 'detect':
        if not args.input or not args.profiles:
            print("For detection, both --input and --profiles arguments are required.")
        else:
            profiles = load_profiles(args.profiles)

            text = ''
            if os.path.isfile(args.input):
                with open(args.input, 'r', encoding='utf-8') as file:
                    text = file.read()
            else:
                text = args.input

            detected_language = detect_language(text, profiles)
            print(f"Detected language: {detected_language}")

```

Experiment လုပ်ဖို့အတွက် shell script ကိုလည်း ပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define the base directory, the Python script, and the input directory
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/freq_dict"
PYTHON_SCRIPT="$BASE_DIR/char_freq_lang_detect.py"
INPUT_DIR="$BASE_DIR/eg_input"
PROFILE_DIR="$BASE_DIR/profile"

# Loop through each file in the eg_input directory
for file in "$INPUT_DIR"/*; do
    # Extract the filename
    filename=$(basename -- "$file")

    # Run the Python script for language detection on the file
    echo "Processing file $filename..."
    detected_language_file=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$file" --profiles "$PROFILE_DIR")
    echo "File: $filename - Detected Language: $detected_language_file"

    # Extract a random sentence from the file
    random_sentence=$(shuf -n 1 "$file")

    # Run the Python script for language detection on the random sentence
    echo "Processing random sentence from $filename: $random_sentence"
    detected_language_sentence=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$random_sentence" --profiles "$PROFILE_DIR")
    echo "Random sentence from $filename - Detected Language: $detected_language_sentence"

    echo ""
done

echo "Language detection completed for all files."

```

Experiment-1 result with Character Frequency Dictionary Based Approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ time ./detect_languages_exp.sh | tee exp1.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Random sentence from bamar_burmese.txt - Detected Language: Detected language: beik_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Random sentence from beik.txt - Detected Language: Detected language: rakhine_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Random sentence from dawei.txt - Detected Language: Detected language: dawei_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Random sentence from mon_tst.txt - Detected Language: Detected language: mon_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Random sentence from mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Random sentence from pao.txt - Detected Language: Detected language: rakhine_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Random sentence from shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Language detection completed for all files.

real    0m0.362s
user    0m0.315s
sys     0m0.051s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$
```

Experiment-2 Result with Character Frequency Dictionary Based Approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ time ./detect_languages_exp.sh | tee exp2.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Random sentence from bamar_burmese.txt - Detected Language: Detected language: bamar_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Random sentence from beik.txt - Detected Language: Detected language: rakhine_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from dawei.txt: အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။
Random sentence from dawei.txt - Detected Language: Detected language: beik_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Random sentence from mon_tst.txt - Detected Language: Detected language: mon_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Random sentence from mon.txt - Detected Language: Detected language: mon_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Random sentence from pao.txt - Detected Language: Detected language: rakhine_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Random sentence from shan.txt - Detected Language: Detected language: shan_profile.json

Language detection completed for all files.

real    0m0.367s
user    0m0.298s
sys     0m0.073s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$
```

Experiment-3 Result with Character Frequency Dictionary Based Approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$ time ./detect_languages_exp.sh | tee exp3.log
Processing file bamar_burmese.txt...
File: bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Random sentence from bamar_burmese.txt - Detected Language: Detected language: rakhine_profile.json

Processing file beik.txt...
File: beik.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Random sentence from beik.txt - Detected Language: Detected language: rakhine_profile.json

Processing file dawei.txt...
File: dawei.txt - Detected Language: Detected language: beik_profile.json
Processing random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Random sentence from dawei.txt - Detected Language: Detected language: rakhine_profile.json

Processing file mon_tst.txt...
File: mon_tst.txt - Detected Language: Detected language: mon_profile.json
Processing random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Random sentence from mon_tst.txt - Detected Language: Detected language: mon_profile.json

Processing file mon.txt...
File: mon.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Random sentence from mon.txt - Detected Language: Detected language: mon_profile.json

Processing file pao.txt...
File: pao.txt - Detected Language: Detected language: pao_profile.json
Processing random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Random sentence from pao.txt - Detected Language: Detected language: rakhine_profile.json

Processing file po_kayin.txt...
File: po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json
Processing random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Random sentence from po_kayin.txt - Detected Language: Detected language: po_kayin_profile.json

Processing file rakhine.txt...
File: rakhine.txt - Detected Language: Detected language: rakhine_profile.json
Processing random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Random sentence from rakhine.txt - Detected Language: Detected language: rakhine_profile.json

Processing file sgaw_kayin.txt...
File: sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from sgaw_kayin.txt: ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Random sentence from sgaw_kayin.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Processing file shan.txt...
File: shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json
Processing random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Random sentence from shan.txt - Detected Language: Detected language: sgaw_kayin_profile.json

Language detection completed for all files.

real    0m0.325s
user    0m0.282s
sys     0m0.047s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/freq_dict$
```

## Rename Experiment Log File of Neural Network Based Approach

နောက်ပိုင်း ပြန်ကြည့်ရင် နားလည်လွယ်အောင်၊ experiment 1 မှန်း သိအောင် ဖိုင်နာမည်ကို အောက်ပါအတိုင်း ပြောင်းထားလိုက်တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/neural$ mv experiment.log experiment1.log
```

## Producing Experiment-1, Experiment-2, Experiment-3 Results for the FastText Lib Approach

လက်ရှိမှာ FastText Lib ကို သုံးပြီးတော့ experiment အကြမ်း လုပ်ခဲ့ပေမဲ့ စာတမ်းရေးဖို့အတွက် တခြား method တွေနဲ့ နှိုင်းယှဉ်ဖို့အတွက် ရလဒ်ကို မပြင်ဆင်ရသေးတာမို့ အဲဒီအတွက် ပြင်ဆင်ခဲ့တယ်။  

အရင်ဆုံး training လုပ်တဲ့အခါမှာ ဒေတာအကုန်ကို သုံးရလိမ့်မယ်။ အဲဒါမှ တခြား method တွေနဲ့ နှိုင်းယှဉ်လို့ ရမှာမို့လို့ ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ wc all_languages.fasttext
  200721  2755674 27864739 all_languages.fasttext
```

အထက်ပါ ဖိုင်ကို training အတွက် သုံးရလိမ့်မယ်။ 

Experiment အတွက် အောက်ပါအတိုင်း shell script ကို ရေးခဲ့တယ်။ ngram ကို 3gram ကနေ 7gram အထိ ထားပြီး training လုပ်ခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ cat train4exp.sh
#!/bin/bash

## Training with 3 gram
time python ./fasttext_lang_detect.py --mode train --input ./all_languages.fasttext \
--output ./3gram.model.bin --epoch 25 --lr 1.0 --wordNgrams 3

## Training with 4 gram
time python ./fasttext_lang_detect.py --mode train --input ./all_languages.fasttext \
--output ./4gram.model.bin --epoch 25 --lr 1.0 --wordNgrams 4

## Training with 5 gram
time python ./fasttext_lang_detect.py --mode train --input ./all_languages.fasttext \
--output ./5gram.model.bin --epoch 25 --lr 1.0 --wordNgrams 5

## Training with 6 gram
time python ./fasttext_lang_detect.py --mode train --input ./all_languages.fasttext \
--output ./6gram.model.bin --epoch 25 --lr 1.0 --wordNgrams 6

## Training with 7 gram
time python ./fasttext_lang_detect.py --mode train --input ./all_languages.fasttext \
--output ./7gram.model.bin --epoch 25 --lr 1.0 --wordNgrams 7

```

### Training Models for FastText Lib Based Approach  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./train4exp.sh | tee training4exp.log
Read 2M words
Number of words:  15399
Number of labels: 9
Progress:   4.9% words/sec/thread: 1565316 lr:  0.950535 avg.loss:  0.064191 ETA:   0h 0m Progress:   9.9% words/sec/thread: 1570717 lr:  0.901357 avg.loss:  0.034697 ETA:   0h 0m Progress:  14.8% words/sec/thread: 1571452 lr:  0.852311 avg.loss:  0.024052 ETA:   0h 0m Progress:  19.7% words/sec/thread: 1571361 lr:  0.803295 avg.loss:  0.019020 ETA:   0h 0m Progress:  24.6% words/sec/thread: 1571594 lr:  0.754250 avg.loss:  0.016184 ETA:   0h 0m Progress:  29.5% words/sec/thread: 1571572 lr:  0.705222 avg.loss:  0.014161 ETA:   0h 0m Progress:  34.4% words/sec/thread: 1571996 lr:  0.656120 avg.loss:  0.012337 ETA:   0h 0m Progress:  39.3% words/sec/thread: 1572164 lr:  0.607040 avg.loss:  0.010953 ETA:   0h 0m Progress:  44.2% words/sec/thread: 1571435 lr:  0.558216 avg.loss:  0.009918 ETA:   0h 0m Progress:  49.1% words/sec/thread: 1571511 lr:  0.509169 avg.loss:  0.009194 ETA:   0h 0m Progress:  54.0% words/sec/thread: 1571701 lr:  0.460086 avg.loss:  0.008495 ETA:   0h 0m Progress:  58.9% words/sec/thread: 1571693 lr:  0.411073 avg.loss:  0.007904 ETA:   0h 0m Progress:  63.8% words/sec/thread: 1571720 lr:  0.362045 avg.loss:  0.007420 ETA:   0h 0m Progress:  68.7% words/sec/thread: 1571631 lr:  0.313104 avg.loss:  0.007062 ETA:   0h 0m Progress:  73.6% words/sec/thread: 1571247 lr:  0.264257 avg.loss:  0.006667 ETA:   0h 0m Progress:  78.5% words/sec/thread: 1570923 lr:  0.215450 avg.loss:  0.006317 ETA:   0h 0m Progress:  83.3% words/sec/thread: 1570610 lr:  0.166660 avg.loss:  0.006022 ETA:   0h 0m Progress:  88.2% words/sec/thread: 1570403 lr:  0.117833 avg.loss:  0.005731 ETA:   0h 0m Progress:  93.1% words/sec/thread: 1570253 lr:  0.068980 avg.loss:  0.005470 ETA:   0h 0m Progress:  98.0% words/sec/thread: 1569995 lr:  0.020210 avg.loss:  0.005242 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1526029 lr: -0.000003 avg.loss:  0.005158 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1525717 lr:  0.000000 avg.loss:  0.005158 ETA:   0h 0m 0s
Model saved to ./3gram.model.bin

real    0m2.984s
user    0m48.972s
sys     0m2.656s
Read 2M words
Number of words:  15399
Number of labels: 9
Progress:   3.8% words/sec/thread: 1208165 lr:  0.961872 avg.loss:  0.075905 ETA:   0h 0m Progress:   7.6% words/sec/thread: 1213405 lr:  0.923856 avg.loss:  0.041515 ETA:   0h 0m Progress:  11.5% words/sec/thread: 1219157 lr:  0.885458 avg.loss:  0.029502 ETA:   0h 0m Progress:  15.2% words/sec/thread: 1217805 lr:  0.847591 avg.loss:  0.022728 ETA:   0h 0m Progress:  19.1% words/sec/thread: 1220902 lr:  0.809125 avg.loss:  0.019019 ETA:   0h 0m Progress:  22.9% words/sec/thread: 1222538 lr:  0.770741 avg.loss:  0.016393 ETA:   0h 0m Progress:  26.7% words/sec/thread: 1221875 lr:  0.732778 avg.loss:  0.014656 ETA:   0h 0m Progress:  30.5% words/sec/thread: 1222107 lr:  0.694633 avg.loss:  0.013468 ETA:   0h 0m Progress:  34.4% words/sec/thread: 1224880 lr:  0.655752 avg.loss:  0.012070 ETA:   0h 0m Progress:  38.3% words/sec/thread: 1227379 lr:  0.616792 avg.loss:  0.010959 ETA:   0h 0m Progress:  42.2% words/sec/thread: 1228615 lr:  0.578114 avg.loss:  0.010061 ETA:   0h 0m Progress:  46.1% words/sec/thread: 1230034 lr:  0.539281 avg.loss:  0.009692 ETA:   0h 0m Progress:  50.0% words/sec/thread: 1231785 lr:  0.500206 avg.loss:  0.009050 ETA:   0h 0m Progress:  53.8% words/sec/thread: 1230858 lr:  0.462193 avg.loss:  0.008483 ETA:   0h 0m Progress:  57.6% words/sec/thread: 1230175 lr:  0.424141 avg.loss:  0.008022 ETA:   0h 0m Progress:  61.4% words/sec/thread: 1229358 lr:  0.386197 avg.loss:  0.007835 ETA:   0h 0m Progress:  64.6% words/sec/thread: 1217468 lr:  0.354178 avg.loss:  0.007497 ETA:   0h 0m Progress:  67.7% words/sec/thread: 1205626 lr:  0.322880 avg.loss:  0.007299 ETA:   0h 0m Progress:  70.9% words/sec/thread: 1195501 lr:  0.291310 avg.loss:  0.007024 ETA:   0h 0m Progress:  74.0% words/sec/thread: 1186405 lr:  0.259727 avg.loss:  0.006752 ETA:   0h 0m Progress:  77.2% words/sec/thread: 1178799 lr:  0.227721 avg.loss:  0.006548 ETA:   0h 0m Progress:  80.4% words/sec/thread: 1171745 lr:  0.195812 avg.loss:  0.006318 ETA:   0h 0m Progress:  83.5% words/sec/thread: 1164102 lr:  0.164782 avg.loss:  0.006165 ETA:   0h 0m Progress:  86.6% words/sec/thread: 1156789 lr:  0.133981 avg.loss:  0.005967 ETA:   0h 0m Progress:  89.7% words/sec/thread: 1150047 lr:  0.103176 avg.loss:  0.005809 ETA:   0h 0m Progress:  92.8% words/sec/thread: 1144007 lr:  0.072205 avg.loss:  0.005638 ETA:   0h 0m Progress:  94.6% words/sec/thread: 1123657 lr:  0.053684 avg.loss:  0.005544 ETA:   0h 0m Progress:  97.9% words/sec/thread: 1120857 lr:  0.021104 avg.loss:  0.005387 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1105504 lr: -0.000006 avg.loss:  0.005301 ETA:   0h 0m Progress: 100.0% words/sec/thread: 1105376 lr:  0.000000 avg.loss:  0.005301 ETA:   0h 0m 0s
Model saved to ./4gram.model.bin

real    0m3.768s
user    1m7.724s
sys     0m2.782s
Read 2M words
Number of words:  15399
Number of labels: 9
Progress:   2.8% words/sec/thread:  873545 lr:  0.972256 avg.loss:  0.105095 ETA:   0h 0m Progress:   5.5% words/sec/thread:  875056 lr:  0.944917 avg.loss:  0.062621 ETA:   0h 0m Progress:   8.2% words/sec/thread:  869723 lr:  0.918144 avg.loss:  0.043468 ETA:   0h 0m Progress:  10.9% words/sec/thread:  869842 lr:  0.891023 avg.loss:  0.033486 ETA:   0h 0m Progress:  13.5% words/sec/thread:  864583 lr:  0.864720 avg.loss:  0.028732 ETA:   0h 0m Progress:  16.3% words/sec/thread:  866473 lr:  0.837407 avg.loss:  0.024119 ETA:   0h 0m Progress:  19.0% words/sec/thread:  867608 lr:  0.810153 avg.loss:  0.021417 ETA:   0h 0m Progress:  21.7% words/sec/thread:  868583 lr:  0.782862 avg.loss:  0.019610 ETA:   0h 0m Progress:  24.5% words/sec/thread:  871069 lr:  0.755098 avg.loss:  0.017907 ETA:   0h 0m Progress:  27.3% words/sec/thread:  873710 lr:  0.727118 avg.loss:  0.016229 ETA:   0h 0m Progress:  30.1% words/sec/thread:  875714 lr:  0.699201 avg.loss:  0.015240 ETA:   0h 0m Progress:  32.9% words/sec/thread:  877486 lr:  0.671242 avg.loss:  0.014064 ETA:   0h 0m Progress:  35.6% words/sec/thread:  878417 lr:  0.643521 avg.loss:  0.013128 ETA:   0h 0m Progress:  38.4% words/sec/thread:  878916 lr:  0.615921 avg.loss:  0.012320 ETA:   0h 0m Progress:  41.2% words/sec/thread:  879203 lr:  0.588383 avg.loss:  0.011564 ETA:   0h 0m Progress:  43.9% words/sec/thread:  879234 lr:  0.560971 avg.loss:  0.010965 ETA:   0h 0m Progress:  46.7% words/sec/thread:  880515 lr:  0.532882 avg.loss:  0.010584 ETA:   0h 0m Progress:  49.5% words/sec/thread:  881263 lr:  0.505018 avg.loss:  0.010102 ETA:   0h 0m Progress:  52.3% words/sec/thread:  882186 lr:  0.477004 avg.loss:  0.009605 ETA:   0h 0m Progress:  55.1% words/sec/thread:  883183 lr:  0.448884 avg.loss:  0.009194 ETA:   0h 0m Progress:  57.9% words/sec/thread:  883698 lr:  0.421027 avg.loss:  0.009057 ETA:   0h 0m Progress:  60.7% words/sec/thread:  884062 lr:  0.393230 avg.loss:  0.008679 ETA:   0h 0m Progress:  63.5% words/sec/thread:  884525 lr:  0.365348 avg.loss:  0.008494 ETA:   0h 0m Progress:  66.2% words/sec/thread:  884644 lr:  0.337684 avg.loss:  0.008237 ETA:   0h 0m Progress:  69.0% words/sec/thread:  884914 lr:  0.309903 avg.loss:  0.008048 ETA:   0h 0m Progress:  71.8% words/sec/thread:  884971 lr:  0.282281 avg.loss:  0.007775 ETA:   0h 0m Progress:  74.6% words/sec/thread:  885433 lr:  0.254316 avg.loss:  0.007527 ETA:   0h 0m Progress:  77.3% words/sec/thread:  885635 lr:  0.226544 avg.loss:  0.007287 ETA:   0h 0m Progress:  80.1% words/sec/thread:  885513 lr:  0.199037 avg.loss:  0.007065 ETA:   0h 0m Progress:  82.9% words/sec/thread:  885549 lr:  0.171403 avg.loss:  0.006860 ETA:   0h 0m Progress:  85.6% words/sec/thread:  885722 lr:  0.143643 avg.loss:  0.006664 ETA:   0h 0m Progress:  88.4% words/sec/thread:  885971 lr:  0.115788 avg.loss:  0.006479 ETA:   0h 0m Progress:  91.2% words/sec/thread:  885919 lr:  0.088233 avg.loss:  0.006340 ETA:   0h 0m Progress:  93.9% words/sec/thread:  885900 lr:  0.060645 avg.loss:  0.006182 ETA:   0h 0m Progress:  96.7% words/sec/thread:  886130 lr:  0.032790 avg.loss:  0.006029 ETA:   0h 0m Progress:  99.5% words/sec/thread:  886180 lr:  0.005117 avg.loss:  0.005885 ETA:   0h 0m Progress: 100.0% words/sec/thread:  866638 lr: -0.000010 avg.loss:  0.005860 ETA:   0h 0m Progress: 100.0% words/sec/thread:  866511 lr:  0.000000 avg.loss:  0.005860 ETA:   0h 0m 0s
Model saved to ./5gram.model.bin

real    0m4.695s
user    1m24.919s
sys     0m2.854s
Read 2M words
Number of words:  15399
Number of labels: 9
Progress:   2.3% words/sec/thread:  721993 lr:  0.977151 avg.loss:  0.146324 ETA:   0h 0m Progress:   4.5% words/sec/thread:  713804 lr:  0.955054 avg.loss:  0.092768 ETA:   0h 0m Progress:   6.8% words/sec/thread:  717733 lr:  0.932430 avg.loss:  0.061874 ETA:   0h 0m Progress:   9.0% words/sec/thread:  721004 lr:  0.909654 avg.loss:  0.046491 ETA:   0h 0m Progress:  11.3% words/sec/thread:  722419 lr:  0.886689 avg.loss:  0.038049 ETA:   0h 0m Progress:  13.6% words/sec/thread:  724009 lr:  0.863873 avg.loss:  0.032368 ETA:   0h 0m Progress:  15.9% words/sec/thread:  724911 lr:  0.841099 avg.loss:  0.028434 ETA:   0h 0m Progress:  18.0% words/sec/thread:  720829 lr:  0.819526 avg.loss:  0.025070 ETA:   0h 0m Progress:  20.3% words/sec/thread:  719547 lr:  0.797408 avg.loss:  0.023409 ETA:   0h 0m Progress:  22.5% words/sec/thread:  720869 lr:  0.774568 avg.loss:  0.021504 ETA:   0h 0m Progress:  24.8% words/sec/thread:  721772 lr:  0.751779 avg.loss:  0.019584 ETA:   0h 0m Progress:  27.1% words/sec/thread:  722260 lr:  0.729092 avg.loss:  0.018221 ETA:   0h 0m Progress:  29.4% words/sec/thread:  722872 lr:  0.706281 avg.loss:  0.017045 ETA:   0h 0m Progress:  31.6% words/sec/thread:  723205 lr:  0.683555 avg.loss:  0.016103 ETA:   0h 0m Progress:  33.9% words/sec/thread:  723453 lr:  0.660856 avg.loss:  0.015121 ETA:   0h 0m Progress:  36.2% words/sec/thread:  724011 lr:  0.637982 avg.loss:  0.014293 ETA:   0h 0m Progress:  38.5% words/sec/thread:  724453 lr:  0.615118 avg.loss:  0.013514 ETA:   0h 0m Progress:  40.8% words/sec/thread:  724688 lr:  0.592363 avg.loss:  0.012891 ETA:   0h 0m Progress:  43.0% words/sec/thread:  724304 lr:  0.569988 avg.loss:  0.012272 ETA:   0h 0m Progress:  45.3% words/sec/thread:  724701 lr:  0.547156 avg.loss:  0.011732 ETA:   0h 0m Progress:  47.6% words/sec/thread:  725340 lr:  0.524148 avg.loss:  0.011554 ETA:   0h 0m Progress:  49.9% words/sec/thread:  725694 lr:  0.501280 avg.loss:  0.011095 ETA:   0h 0m Progress:  52.1% words/sec/thread:  725485 lr:  0.478760 avg.loss:  0.010626 ETA:   0h 0m Progress:  54.5% words/sec/thread:  726337 lr:  0.455477 avg.loss:  0.010193 ETA:   0h 0m Progress:  56.8% words/sec/thread:  727181 lr:  0.432132 avg.loss:  0.009908 ETA:   0h 0m Progress:  59.1% words/sec/thread:  728074 lr:  0.408702 avg.loss:  0.009441 ETA:   0h 0m Progress:  61.5% words/sec/thread:  729208 lr:  0.385007 avg.loss:  0.008995 ETA:   0h 0m Progress:  63.9% words/sec/thread:  730498 lr:  0.361107 avg.loss:  0.008684 ETA:   0h 0m Progress:  66.3% words/sec/thread:  731679 lr:  0.337247 avg.loss:  0.008295 ETA:   0h 0m Progress:  68.7% words/sec/thread:  733520 lr:  0.312709 avg.loss:  0.007974 ETA:   0h 0m Progress:  71.1% words/sec/thread:  734573 lr:  0.288825 avg.loss:  0.007655 ETA:   0h 0m Progress:  73.5% words/sec/thread:  735683 lr:  0.264810 avg.loss:  0.007390 ETA:   0h 0m Progress:  75.9% words/sec/thread:  736064 lr:  0.241456 avg.loss:  0.007215 ETA:   0h 0m Progress:  78.2% words/sec/thread:  736748 lr:  0.217747 avg.loss:  0.007047 ETA:   0h 0m Progress:  80.6% words/sec/thread:  737490 lr:  0.193943 avg.loss:  0.006884 ETA:   0h 0m Progress:  83.0% words/sec/thread:  737918 lr:  0.170471 avg.loss:  0.006732 ETA:   0h 0m Progress:  85.3% words/sec/thread:  738391 lr:  0.146910 avg.loss:  0.006607 ETA:   0h 0m Progress:  87.6% words/sec/thread:  738628 lr:  0.123619 avg.loss:  0.006467 ETA:   0h 0m Progress:  90.0% words/sec/thread:  738883 lr:  0.100272 avg.loss:  0.006338 ETA:   0h 0m Progress:  92.3% words/sec/thread:  739324 lr:  0.076681 avg.loss:  0.006211 ETA:   0h 0m Progress:  94.7% words/sec/thread:  739598 lr:  0.053278 avg.loss:  0.006102 ETA:   0h 0m Progress:  97.0% words/sec/thread:  740068 lr:  0.029604 avg.loss:  0.006004 ETA:   0h 0m Progress:  99.4% words/sec/thread:  740638 lr:  0.005740 avg.loss:  0.005905 ETA:   0h 0m Progress: 100.0% words/sec/thread:  727979 lr: -0.000008 avg.loss:  0.005881 ETA:   0h 0m Progress: 100.0% words/sec/thread:  727906 lr:  0.000000 avg.loss:  0.005881 ETA:   0h 0m 0s
Model saved to ./6gram.model.bin

real    0m9.010s
user    1m41.219s
sys     0m2.949s
Read 2M words
Number of words:  15399
Number of labels: 9
Progress:   1.9% words/sec/thread:  612696 lr:  0.980641 avg.loss:  0.135104 ETA:   0h 0m Progress:   3.9% words/sec/thread:  614806 lr:  0.961361 avg.loss:  0.086207 ETA:   0h 0m Progress:   5.8% words/sec/thread:  614317 lr:  0.942200 avg.loss:  0.059502 ETA:   0h 0m Progress:   7.7% words/sec/thread:  614917 lr:  0.922941 avg.loss:  0.047796 ETA:   0h 0m Progress:   9.6% words/sec/thread:  615174 lr:  0.903699 avg.loss:  0.039604 ETA:   0h 0m Progress:  11.6% words/sec/thread:  615421 lr:  0.884442 avg.loss:  0.033929 ETA:   0h 0m Progress:  13.5% words/sec/thread:  616079 lr:  0.865086 avg.loss:  0.029394 ETA:   0h 0m Progress:  15.4% words/sec/thread:  613721 lr:  0.846469 avg.loss:  0.026471 ETA:   0h 0m Progress:  17.2% words/sec/thread:  612849 lr:  0.827540 avg.loss:  0.024603 ETA:   0h 0m Progress:  19.1% words/sec/thread:  612206 lr:  0.808602 avg.loss:  0.022777 ETA:   0h 0m Progress:  21.0% words/sec/thread:  610563 lr:  0.790080 avg.loss:  0.021210 ETA:   0h 0m Progress:  22.9% words/sec/thread:  610725 lr:  0.770984 avg.loss:  0.019890 ETA:   0h 0m Progress:  24.8% words/sec/thread:  611017 lr:  0.751822 avg.loss:  0.018525 ETA:   0h 0m Progress:  26.7% words/sec/thread:  611412 lr:  0.732599 avg.loss:  0.017402 ETA:   0h 0m Progress:  28.7% words/sec/thread:  611731 lr:  0.713391 avg.loss:  0.016484 ETA:   0h 0m Progress:  30.6% words/sec/thread:  611808 lr:  0.694277 avg.loss:  0.015738 ETA:   0h 0m Progress:  32.4% words/sec/thread:  610893 lr:  0.675694 avg.loss:  0.014903 ETA:   0h 0m Progress:  34.2% words/sec/thread:  608798 lr:  0.657822 avg.loss:  0.014249 ETA:   0h 0m Progress:  36.1% words/sec/thread:  609292 lr:  0.638538 avg.loss:  0.013554 ETA:   0h 0m Progress:  38.1% words/sec/thread:  610168 lr:  0.618994 avg.loss:  0.012940 ETA:   0h 0m Progress:  40.0% words/sec/thread:  610488 lr:  0.599755 avg.loss:  0.012378 ETA:   0h 0m Progress:  42.0% words/sec/thread:  611246 lr:  0.580196 avg.loss:  0.011847 ETA:   0h 0m Progress:  44.0% words/sec/thread:  612524 lr:  0.560224 avg.loss:  0.011378 ETA:   0h 0m Progress:  46.0% words/sec/thread:  613866 lr:  0.540090 avg.loss:  0.010960 ETA:   0h 0m Progress:  48.0% words/sec/thread:  615084 lr:  0.519967 avg.loss:  0.010746 ETA:   0h 0m Progress:  50.0% words/sec/thread:  616270 lr:  0.499803 avg.loss:  0.010395 ETA:   0h 0m Progress:  52.0% words/sec/thread:  617302 lr:  0.479695 avg.loss:  0.010035 ETA:   0h 0m Progress:  54.0% words/sec/thread:  618256 lr:  0.459576 avg.loss:  0.009700 ETA:   0h 0m Progress:  56.1% words/sec/thread:  619870 lr:  0.438815 avg.loss:  0.009428 ETA:   0h 0m Progress:  58.2% words/sec/thread:  621689 lr:  0.417768 avg.loss:  0.009295 ETA:   0h 0m Progress:  60.3% words/sec/thread:  623041 lr:  0.397057 avg.loss:  0.009044 ETA:   0h 0m Progress:  62.4% words/sec/thread:  624301 lr:  0.376376 avg.loss:  0.008802 ETA:   0h 0m Progress:  64.5% words/sec/thread:  626032 lr:  0.355133 avg.loss:  0.008571 ETA:   0h 0m Progress:  66.6% words/sec/thread:  627596 lr:  0.333964 avg.loss:  0.008384 ETA:   0h 0m Progress:  68.7% words/sec/thread:  629044 lr:  0.312821 avg.loss:  0.008207 ETA:   0h 0m Progress:  70.8% words/sec/thread:  630406 lr:  0.291688 avg.loss:  0.008121 ETA:   0h 0m Progress:  72.9% words/sec/thread:  631682 lr:  0.270577 avg.loss:  0.007927 ETA:   0h 0m Progress:  75.1% words/sec/thread:  633159 lr:  0.249130 avg.loss:  0.007747 ETA:   0h 0m Progress:  77.2% words/sec/thread:  634449 lr:  0.227827 avg.loss:  0.007678 ETA:   0h 0m Progress:  79.4% words/sec/thread:  635742 lr:  0.206446 avg.loss:  0.007531 ETA:   0h 0m Progress:  81.5% words/sec/thread:  636861 lr:  0.185207 avg.loss:  0.007392 ETA:   0h 0m Progress:  83.6% words/sec/thread:  638075 lr:  0.163759 avg.loss:  0.007237 ETA:   0h 0m Progress:  85.8% words/sec/thread:  639640 lr:  0.141771 avg.loss:  0.007088 ETA:   0h 0m Progress:  88.0% words/sec/thread:  641155 lr:  0.119759 avg.loss:  0.007016 ETA:   0h 0m Progress:  90.2% words/sec/thread:  642626 lr:  0.097713 avg.loss:  0.006877 ETA:   0h 0m Progress:  92.4% words/sec/thread:  643821 lr:  0.075970 avg.loss:  0.006746 ETA:   0h 0m Progress:  94.6% words/sec/thread:  644847 lr:  0.054403 avg.loss:  0.006617 ETA:   0h 0m Progress:  96.7% words/sec/thread:  645794 lr:  0.032879 avg.loss:  0.006515 ETA:   0h 0m Progress:  98.8% words/sec/thread:  646475 lr:  0.011723 avg.loss:  0.006401 ETA:   0h 0m Progress: 100.0% words/sec/thread:  641061 lr: -0.000008 avg.loss:  0.006340 ETA:   0h 0m Progress: 100.0% words/sec/thread:  641004 lr:  0.000000 avg.loss:  0.006340 ETA:   0h 0m 0s
Model saved to ./7gram.model.bin

real    0m5.954s
user    1m55.381s
sys     0m2.934s

real    0m26.417s
user    6m58.215s
sys     0m14.185s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

ထွက်လာတဲ့ မော်ဒယ်တွေရဲ့ filesize ကို လေ့လာခဲ့...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ ls *gram.model.bin -lh
-rw-rw-r-- 1 ye ye 770M ม.ค.  22 19:44 3gram.model.bin
-rw-rw-r-- 1 ye ye 770M ม.ค.  22 19:44 4gram.model.bin
-rw-rw-r-- 1 ye ye 770M ม.ค.  22 19:44 5gram.model.bin
-rw-rw-r-- 1 ye ye 770M ม.ค.  22 19:44 6gram.model.bin
-rw-rw-r-- 1 ye ye 770M ม.ค.  22 19:45 7gram.model.bin
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

### Convert Test File Data Format

test ဖိုင်တွေကိုလည်း FastText label format ပြောင်းဖို့လိုအပ်တယ်။   
shell script တစ်ပုဒ် ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing$ cat ./fasttext_format_converter_for_test_data.sh
#!/bin/bash

# Define the input directory
INPUT_DIR="./eg_input"

# Loop through each .txt file in the input directory
for file in "$INPUT_DIR"/*.txt; do
    # Extract the label from the filename (e.g., shan from shan.txt)
    label=$(basename "$file" .txt)

    # Define the output file with .fasttext extension
    output_file="${INPUT_DIR}/${label}.fasttext"

    # Process each line in the file
    while IFS= read -r line; do
        # Output the line in the format: __label__<label_name>\t<sentence>
        echo -e "__label__$label\t$line" >> "$output_file"
    done < "$file"
done

echo "Processing completed. Files saved in .fasttext format."
```

Convert လုပ်ပြီး ထွက်လာတဲ့ ဖိုင်တွေကို စစ်ကြည့်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ wc *.txt
  10   75  798 bamar_burmese.txt
  10  103  928 beik.txt
  10  100 1012 dawei.txt
   2   11  137 mon_tst.txt
  10  100  968 mon.txt
  10  105 1230 pao.txt
  10  133 1080 po_kayin.txt
  10  103  934 rakhine.txt
  10  126 1024 sgaw_kayin.txt
  10   85 1123 shan.txt
  92  941 9234 total
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ wc *.fasttext
   10    85  1028 bamar_burmese.fasttext
   10   113  1068 beik.fasttext
   10   110  1162 dawei.fasttext
   10   110  1098 mon.fasttext
    2    13   171 mon_tst.fasttext
   10   115  1360 pao.fasttext
   10   143  1260 po_kayin.fasttext
   10   113  1104 rakhine.fasttext
   10   136  1224 sgaw_kayin.fasttext
   10    95  1263 shan.fasttext
   92  1033 10738 total
```

ဖိုင် content ကိုလည်း confirm လုပ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ head -n 3 *.fasttext
==> bamar_burmese.fasttext <==
__label__bamar_burmese  နေ ကောင်း လား
__label__bamar_burmese  ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
__label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ

==> beik.fasttext <==
__label__beik   ဖယ် သူ လေ ကို မေး ရိ လဲ ။
__label__beik   သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
__label__beik   ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။

==> dawei.fasttext <==
__label__dawei  ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
__label__dawei  အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
__label__dawei  ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။

==> mon.fasttext <==
__label__mon    ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
__label__mon    ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
__label__mon    အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။

==> mon_tst.fasttext <==
__label__mon_tst        လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
__label__mon_tst        က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်

==> pao.fasttext <==
__label__pao    နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
__label__pao    ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
__label__pao    နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ

==> po_kayin.fasttext <==
__label__po_kayin       ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
__label__po_kayin       အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
__label__po_kayin       ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .

==> rakhine.fasttext <==
__label__rakhine        သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
__label__rakhine        ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
__label__rakhine        ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။

==> sgaw_kayin.fasttext <==
__label__sgaw_kayin     တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
__label__sgaw_kayin     ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
__label__sgaw_kayin     တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .

==> shan.fasttext <==
__label__shan   မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
__label__shan   တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
__label__shan   တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$
```

အထက်ပါ ဖိုင်တွေကို experiment လုပ်မယ့် folder ဆီကိုရွှေ့ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ mkdir eg_input
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ cp ./preprocessing/eg_input/*.fasttext ./eg_input/
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ ls ./eg_input/
bamar_burmese.fasttext  mon.fasttext      po_kayin.fasttext    shan.fasttext
beik.fasttext           mon_tst.fasttext  rakhine.fasttext
dawei.fasttext          pao.fasttext      sgaw_kayin.fasttext
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Testing or Language Detection အတွက်လည်း bash script ကို update လုပ်ရလိမ့်မယ်။ 


```bash
#!/bin/bash

# Define directories
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/fasttext"
INPUT_DIR="$BASE_DIR/eg_input"
PYTHON_SCRIPT="$BASE_DIR/fasttext_lang_detect.py"

# Loop through each model file
for model in "$BASE_DIR"/*gram.model.bin; do
    echo "Processing with model: $(basename "$model")"

    # Loop through each .fasttext file in the input directory
    for file in "$INPUT_DIR"/*.fasttext; do
        echo "Testing file: $(basename "$file") with model: $(basename "$model")"
        time python "$PYTHON_SCRIPT" --mode test --model "$model" --input "$file"
        
        # Get a random sentence from the current .fasttext file
        random_sentence=$(shuf -n 1 "$file")
        echo "Predicting random sentence from $(basename "$file"): $random_sentence"
        python "$PYTHON_SCRIPT" --mode predict --model "$model" --input "$random_sentence"
        
        echo ""
    done
    echo ""
done

echo "All processing completed."

```

### Testing or Language Detection with FastText Lib Approach

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test4exp.sh | tee test1.log
Processing with model: 3gram.model.bin
Testing file: bamar_burmese.fasttext with model: 3gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m1.955s
user    0m0.746s
sys     0m2.358s
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ
Predicted language: bamar

Testing file: beik.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.377s
user    0m0.785s
sys     0m2.144s
Predicting random sentence from beik.fasttext: __label__beik    ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.361s
user    0m0.661s
sys     0m2.198s
Predicting random sentence from dawei.fasttext: __label__dawei  အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.363s
user    0m0.763s
sys     0m2.153s
Predicting random sentence from mon.fasttext: __label__mon      ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 3gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.363s
user    0m0.686s
sys     0m2.206s
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.359s
user    0m0.748s
sys     0m2.163s
Predicting random sentence from pao.fasttext: __label__pao      နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.360s
user    0m0.756s
sys     0m2.153s
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.363s
user    0m0.759s
sys     0m2.150s
Predicting random sentence from rakhine.fasttext: __label__rakhine      ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.370s
user    0m0.768s
sys     0m2.153s
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 0.200
Recall at 1: 0.200

real    0m0.359s
user    0m0.762s
sys     0m2.124s
Predicting random sentence from shan.fasttext: __label__shan    ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Predicted language: mon


Processing with model: 4gram.model.bin
Testing file: bamar_burmese.fasttext with model: 4gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.437s
user    0m0.738s
sys     0m2.187s
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ
Predicted language: bamar

Testing file: beik.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.366s
user    0m0.673s
sys     0m2.245s
Predicting random sentence from beik.fasttext: __label__beik    ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Predicted language: beik

Testing file: dawei.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.357s
user    0m0.727s
sys     0m2.182s
Predicting random sentence from dawei.fasttext: __label__dawei  အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Predicted language: dawei

Testing file: mon.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.363s
user    0m0.762s
sys     0m2.153s
Predicting random sentence from mon.fasttext: __label__mon      အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 4gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.409s
user    0m0.655s
sys     0m2.213s
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.373s
user    0m0.714s
sys     0m2.179s
Predicting random sentence from pao.fasttext: __label__pao      နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.369s
user    0m0.789s
sys     0m2.133s
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.369s
user    0m0.695s
sys     0m2.227s
Predicting random sentence from rakhine.fasttext: __label__rakhine      ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.371s
user    0m0.745s
sys     0m2.175s
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100

real    0m0.373s
user    0m0.715s
sys     0m2.209s
Predicting random sentence from shan.fasttext: __label__shan    မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan


Processing with model: 5gram.model.bin
Testing file: bamar_burmese.fasttext with model: 5gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.402s
user    0m0.659s
sys     0m2.296s
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  က လေး က အိမ် မှာ ပါ
Predicted language: bamar

Testing file: beik.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.409s
user    0m0.740s
sys     0m2.214s
Predicting random sentence from beik.fasttext: __label__beik    နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Predicted language: beik

Testing file: dawei.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.390s
user    0m0.852s
sys     0m2.088s
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.394s
user    0m0.721s
sys     0m2.211s
Predicting random sentence from mon.fasttext: __label__mon      ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 5gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.390s
user    0m0.817s
sys     0m2.126s
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.390s
user    0m0.821s
sys     0m2.121s
Predicting random sentence from pao.fasttext: __label__pao      တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.391s
user    0m0.738s
sys     0m2.206s
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.388s
user    0m0.679s
sys     0m2.259s
Predicting random sentence from rakhine.fasttext: __label__rakhine      မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.392s
user    0m0.785s
sys     0m2.160s
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100

real    0m0.392s
user    0m0.754s
sys     0m2.180s
Predicting random sentence from shan.fasttext: __label__shan    မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan


Processing with model: 6gram.model.bin
Testing file: bamar_burmese.fasttext with model: 6gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.396s
user    0m0.774s
sys     0m2.152s
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Predicted language: bamar

Testing file: beik.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.397s
user    0m0.713s
sys     0m2.236s
Predicting random sentence from beik.fasttext: __label__beik    သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.389s
user    0m0.829s
sys     0m2.094s
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.399s
user    0m0.804s
sys     0m2.141s
Predicting random sentence from mon.fasttext: __label__mon      လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 6gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.392s
user    0m0.687s
sys     0m2.257s
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: pao.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.386s
user    0m0.750s
sys     0m2.163s
Predicting random sentence from pao.fasttext: __label__pao      ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Predicted language: pao

Testing file: po_kayin.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.389s
user    0m0.748s
sys     0m2.157s
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.387s
user    0m0.709s
sys     0m2.116s
Predicting random sentence from rakhine.fasttext: __label__rakhine      ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.395s
user    0m0.714s
sys     0m2.233s
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 0.200
Recall at 1: 0.200

real    0m0.390s
user    0m0.706s
sys     0m2.237s
Predicting random sentence from shan.fasttext: __label__shan    တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Predicted language: mon


Processing with model: 7gram.model.bin
Testing file: bamar_burmese.fasttext with model: 7gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.402s
user    0m0.815s
sys     0m2.137s
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Predicted language: bamar

Testing file: beik.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.407s
user    0m0.771s
sys     0m2.184s
Predicting random sentence from beik.fasttext: __label__beik    သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.389s
user    0m0.626s
sys     0m2.302s
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.384s
user    0m0.792s
sys     0m2.145s
Predicting random sentence from mon.fasttext: __label__mon      ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 7gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan

real    0m0.387s
user    0m0.737s
sys     0m2.202s
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: pao.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.388s
user    0m0.777s
sys     0m2.161s
Predicting random sentence from pao.fasttext: __label__pao      တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.386s
user    0m0.747s
sys     0m2.188s
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.386s
user    0m0.717s
sys     0m2.220s
Predicting random sentence from rakhine.fasttext: __label__rakhine      မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000

real    0m0.387s
user    0m0.746s
sys     0m2.191s
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100

real    0m0.398s
user    0m0.792s
sys     0m2.125s
Predicting random sentence from shan.fasttext: __label__shan    မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Predicted language: mon


All processing completed.

real    0m40.096s
user    1m13.572s
sys     3m39.210s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

Let's Check the log file also:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ cat test1.log
Processing with model: 3gram.model.bin
Testing file: bamar_burmese.fasttext with model: 3gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ
Predicted language: bamar

Testing file: beik.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from beik.fasttext: __label__beik    ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from dawei.fasttext: __label__dawei  အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from mon.fasttext: __label__mon      ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 3gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from pao.fasttext: __label__pao      နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from rakhine.fasttext: __label__rakhine      ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 3gram.model.bin
Number of test examples: 10
Precision at 1: 0.200
Recall at 1: 0.200
Predicting random sentence from shan.fasttext: __label__shan    ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Predicted language: mon


Processing with model: 4gram.model.bin
Testing file: bamar_burmese.fasttext with model: 4gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ
Predicted language: bamar

Testing file: beik.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from beik.fasttext: __label__beik    ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Predicted language: beik

Testing file: dawei.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from dawei.fasttext: __label__dawei  အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Predicted language: dawei

Testing file: mon.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from mon.fasttext: __label__mon      အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 4gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from pao.fasttext: __label__pao      နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from rakhine.fasttext: __label__rakhine      ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 4gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100
Predicting random sentence from shan.fasttext: __label__shan    မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan


Processing with model: 5gram.model.bin
Testing file: bamar_burmese.fasttext with model: 5gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  က လေး က အိမ် မှာ ပါ
Predicted language: bamar

Testing file: beik.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from beik.fasttext: __label__beik    နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Predicted language: beik

Testing file: dawei.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from mon.fasttext: __label__mon      ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 5gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Testing file: pao.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from pao.fasttext: __label__pao      တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from rakhine.fasttext: __label__rakhine      မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 5gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100
Predicting random sentence from shan.fasttext: __label__shan    မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan


Processing with model: 6gram.model.bin
Testing file: bamar_burmese.fasttext with model: 6gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Predicted language: bamar

Testing file: beik.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from beik.fasttext: __label__beik    သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from mon.fasttext: __label__mon      လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 6gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: pao.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from pao.fasttext: __label__pao      ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Predicted language: pao

Testing file: po_kayin.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from rakhine.fasttext: __label__rakhine      ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 6gram.model.bin
Number of test examples: 10
Precision at 1: 0.200
Recall at 1: 0.200
Predicting random sentence from shan.fasttext: __label__shan    တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Predicted language: mon


Processing with model: 7gram.model.bin
Testing file: bamar_burmese.fasttext with model: 7gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from bamar_burmese.fasttext: __label__bamar_burmese  ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Predicted language: bamar

Testing file: beik.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from beik.fasttext: __label__beik    သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Predicted language: beik

Testing file: dawei.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from dawei.fasttext: __label__dawei  ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei

Testing file: mon.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from mon.fasttext: __label__mon      ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Predicted language: mon

Testing file: mon_tst.fasttext with model: 7gram.model.bin
Number of test examples: 0
Precision at 1: nan
Recall at 1: nan
Predicting random sentence from mon_tst.fasttext: __label__mon_tst      လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

Testing file: pao.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from pao.fasttext: __label__pao      တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Predicted language: pao

Testing file: po_kayin.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from po_kayin.fasttext: __label__po_kayin    ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Predicted language: po_kayin

Testing file: rakhine.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from rakhine.fasttext: __label__rakhine      မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Predicted language: rakhine

Testing file: sgaw_kayin.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 1.000
Recall at 1: 1.000
Predicting random sentence from sgaw_kayin.fasttext: __label__sgaw_kayin        ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Predicted language: sgaw_kayin

Testing file: shan.fasttext with model: 7gram.model.bin
Number of test examples: 10
Precision at 1: 0.100
Recall at 1: 0.100
Predicting random sentence from shan.fasttext: __label__shan    မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Predicted language: mon


All processing completed.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

### Testing with Mixed Languages Data

အထက်မှာ မြင်ရတဲ့အတိုင်း တချို့ language တွေအတွက် ဖိုင်အလိုက် detect လုပ်ကြည့်တော့ nan ဆိုတဲ့ Precision, Recall တွေ ရခဲ့တာကို တွေ့ရတယ်။  
Fasttext ကို training လုပ်ထားတုန်းက ဘာသာစကားတွေ ရောထားတာတွေနဲ့ လုပ်ခဲ့တာ။  
အဲဒါကြောင့် test ဖိုင်မှာလည်း ရောထားတာနဲ့ စမ်းကြည့်ချင်တယ်။  

အောက်ပါအတိုင်း language အားလုံးကို ဖိုင်တစ်ဖိုင်အဖြစ် ရောခဲ့တယ်။  
```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ cat *.fasttext > all_test.fasttext
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ wc *.fasttext
   92  1033 10738 all_test.fasttext
   10    85  1028 bamar_burmese.fasttext
   10   113  1068 beik.fasttext
   10   110  1162 dawei.fasttext
   10   110  1098 mon.fasttext
    2    13   171 mon_tst.fasttext
   10   115  1360 pao.fasttext
   10   143  1260 po_kayin.fasttext
   10   113  1104 rakhine.fasttext
   10   136  1224 sgaw_kayin.fasttext
   10    95  1263 shan.fasttext
  184  2066 21476 total
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$
```

Testing မလုပ်ခင်မှာ shuffle လုပ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ shuf ./all_test.fasttext > ./all_test.fasttext.shuf
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ head all_test.fasttext.shuf
__label__po_kayin       ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
__label__beik   မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
__label__rakhine        မင်း တောင် တိ ကို တက် နီ ကျ လား ။
__label__sgaw_kayin     ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
__label__bamar_burmese  မင်္ဂ လာ ပါ ဆ ရာ မ
__label__rakhine        ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
__label__dawei  အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
__label__mon    အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
__label__rakhine        ငါ အ လုပ် မ ပြီး သိ ပါ ။
__label__po_kayin       ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext/preprocessing/eg_input$ 
```

Shell script အသစ် တစ်ပုဒ်ကို ပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define directories
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/fasttext"
PYTHON_SCRIPT="$BASE_DIR/fasttext_lang_detect.py"

# Define the test file
TEST_FILE="$BASE_DIR/all_test.fasttext.shuf"

# Loop through each model file
for model in "$BASE_DIR"/*gram.model.bin; do
    echo "Processing with model: $(basename "$model")"

    # Test the model with the specific test file
    echo "Testing with file: $(basename "$TEST_FILE") and model: $(basename "$model")"
    time python "$PYTHON_SCRIPT" --mode test --model "$model" --input "$TEST_FILE"

    # Get a random sentence from the test file
    random_sentence=$(shuf -n 1 "$TEST_FILE")
    echo "Predicting random sentence: $random_sentence"
    python "$PYTHON_SCRIPT" --mode predict --model "$model" --input "$random_sentence"

    echo ""
done

echo "All processing completed."

```

Testing or Prediction with mixed test-data and the result is as follows: 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test_mixed4exp.sh | tee test_mixed1.log
Processing with model: 3gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 3gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.375s
user    0m0.779s
sys     0m2.149s
Predicting random sentence: __label__pao        က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Predicted language: pao

Processing with model: 4gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 4gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.360s
user    0m0.843s
sys     0m2.057s
Predicting random sentence: __label__shan       ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
Predicted language: mon

Processing with model: 5gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 5gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.375s
user    0m0.778s
sys     0m2.146s
Predicting random sentence: __label__sgaw_kayin တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin

Processing with model: 6gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 6gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.382s
user    0m0.750s
sys     0m2.185s
Predicting random sentence: __label__rakhine    ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Predicted language: rakhine

Processing with model: 7gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 7gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.370s
user    0m0.734s
sys     0m2.149s
Predicting random sentence: __label__po_kayin   ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin

All processing completed.

real    0m3.737s
user    0m7.522s
sys     0m21.675s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

I updated the shell script for random test increasing for each ngram model as follows:  

```bash
#!/bin/bash

# Define directories
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/fasttext"
PYTHON_SCRIPT="$BASE_DIR/fasttext_lang_detect.py"

# Define the test file
TEST_FILE="$BASE_DIR/all_test.fasttext.shuf"

# Number of random sentences to predict
NUM_RANDOM_SENTENCES=10

# Loop through each model file
for model in "$BASE_DIR"/*gram.model.bin; do
    echo "Processing with model: $(basename "$model")"

    # Test the model with the specific test file
    echo "Testing with file: $(basename "$TEST_FILE") and model: $(basename "$model")"
    time python "$PYTHON_SCRIPT" --mode test --model "$model" --input "$TEST_FILE"

    # Predict with random sentences from the test file
    for i in $(seq 1 $NUM_RANDOM_SENTENCES); do
        random_sentence=$(shuf -n 1 "$TEST_FILE")
        echo "Predicting random sentence $i: $random_sentence"
        python "$PYTHON_SCRIPT" --mode predict --model "$model" --input "$random_sentence"
    done

    echo ""
done

echo "All processing completed."

```

test ဖိုင်ကလည်း မြန်မာနိုင်ငံမှာ သုံးတဲ့ ဘာသာစကားတွေကို mixed လုပ်ထားတဲ့ ဖိုင်နဲ့ ပြီးတော့ စာကြောင်း တစ်ကြောင်းစီနဲ့ random testing ကိုလည်း ngram မော်ဒယ် တစ်ခုစီအတွက် ၁၀ခါစီ ထားပြီး experiment လုပ်ခဲ့တယ်။   
ရလဒ်က အောက်ပါအတိုင်းပါ ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test_mixed_10random4exp.sh | tee test_mixed2_with_10_random.log
Processing with model: 3gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 3gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.367s
user    0m0.686s
sys     0m2.229s
Predicting random sentence 1: __label__bamar_burmese    က လေး က အိမ် မှာ ပါ
Predicted language: bamar
Predicting random sentence 2: __label__mon      ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Predicted language: mon
Predicting random sentence 3: __label__mon      ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Predicted language: mon
Predicting random sentence 4: __label__rakhine  ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Predicted language: rakhine
Predicting random sentence 5: __label__shan     ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
Predicted language: mon
Predicting random sentence 6: __label__dawei    ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Predicted language: dawei
Predicting random sentence 7: __label__pao      နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Predicted language: pao
Predicting random sentence 8: __label__pao      ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Predicted language: pao
Predicting random sentence 9: __label__beik     သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Predicted language: beik
Predicting random sentence 10: __label__sgaw_kayin      ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Predicted language: sgaw_kayin

Processing with model: 4gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 4gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.355s
user    0m0.742s
sys     0m2.163s
Predicting random sentence 1: __label__sgaw_kayin       ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 2: __label__beik     ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Predicted language: beik
Predicting random sentence 3: __label__shan     မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan
Predicting random sentence 4: __label__po_kayin ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Predicted language: po_kayin
Predicting random sentence 5: __label__dawei    ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Predicted language: dawei
Predicting random sentence 6: __label__shan     တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Predicted language: mon
Predicting random sentence 7: __label__pao      တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Predicted language: pao
Predicting random sentence 8: __label__pao      ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Predicted language: pao
Predicting random sentence 9: __label__beik     နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Predicted language: beik
Predicting random sentence 10: __label__po_kayin        နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin

Processing with model: 5gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 5gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.375s
user    0m0.785s
sys     0m2.142s
Predicting random sentence 1: __label__sgaw_kayin       ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 2: __label__shan     တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Predicted language: mon
Predicting random sentence 3: __label__rakhine  မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Predicted language: rakhine
Predicting random sentence 4: __label__dawei    နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Predicted language: dawei
Predicting random sentence 5: __label__dawei    နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Predicted language: dawei
Predicting random sentence 6: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 7: __label__rakhine  ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine
Predicting random sentence 8: __label__sgaw_kayin       ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 9: __label__po_kayin ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin
Predicting random sentence 10: __label__pao     ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Predicted language: pao

Processing with model: 6gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 6gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.387s
user    0m0.786s
sys     0m2.154s
Predicting random sentence 1: __label__rakhine  ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine
Predicting random sentence 2: __label__dawei    ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Predicted language: dawei
Predicting random sentence 3: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin
Predicting random sentence 4: __label__shan     ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Predicted language: dawei
Predicting random sentence 5: __label__beik     အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Predicted language: beik
Predicting random sentence 6: __label__beik     အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Predicted language: beik
Predicting random sentence 7: __label__mon      အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Predicted language: mon
Predicting random sentence 8: __label__po_kayin ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Predicted language: po_kayin
Predicting random sentence 9: __label__dawei    အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Predicted language: dawei
Predicting random sentence 10: __label__beik    အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Predicted language: beik

Processing with model: 7gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 7gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.390s
user    0m0.700s
sys     0m2.227s
Predicting random sentence 1: __label__pao      က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Predicted language: pao
Predicting random sentence 2: __label__beik     ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Predicted language: beik
Predicting random sentence 3: __label__beik     အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
Predicted language: beik
Predicting random sentence 4: __label__bamar_burmese    ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Predicted language: bamar
Predicting random sentence 5: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 6: __label__rakhine  ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine
Predicting random sentence 7: __label__beik     မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Predicted language: beik
Predicting random sentence 8: __label__rakhine  ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Predicted language: rakhine
Predicting random sentence 9: __label__mon      ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Predicted language: mon
Predicting random sentence 10: __label__mon_tst လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon

All processing completed.

real    0m20.826s
user    0m40.215s
sys     2m0.335s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

7gram နဲ့ စမ်းထားတဲ့ string random ရလဒ်တွေက အကုန် မှန်သလားလို့ ... 
သေချာအောင် နောက်ထပ် တစ်ခေါက် ထပ် experiment လုပ်ကြည့်ခဲ့တယ်။ ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test_mixed_10random4exp.sh | tee test_mixed3_with_10_random.log
Processing with model: 3gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 3gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.371s
user    0m0.762s
sys     0m2.159s
Predicting random sentence 1: __label__mon      ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Predicted language: mon
Predicting random sentence 2: __label__pao      ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Predicted language: pao
Predicting random sentence 3: __label__dawei    ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Predicted language: dawei
Predicting random sentence 4: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 5: __label__rakhine  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Predicted language: rakhine
Predicting random sentence 6: __label__beik     သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Predicted language: beik
Predicting random sentence 7: __label__bamar_burmese    တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Predicted language: bamar
Predicting random sentence 8: __label__sgaw_kayin       ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 9: __label__beik     အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Predicted language: beik
Predicting random sentence 10: __label__mon     ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Predicted language: mon

Processing with model: 4gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 4gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.353s
user    0m0.644s
sys     0m2.222s
Predicting random sentence 1: __label__mon      ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Predicted language: mon
Predicting random sentence 2: __label__shan     တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Predicted language: mon
Predicting random sentence 3: __label__po_kayin နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin
Predicting random sentence 4: __label__dawei    သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Predicted language: dawei
Predicting random sentence 5: __label__mon      သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon
Predicting random sentence 6: __label__bamar_burmese    ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Predicted language: bamar
Predicting random sentence 7: __label__bamar_burmese    ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar
Predicting random sentence 8: __label__bamar_burmese    ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Predicted language: bamar
Predicting random sentence 9: __label__rakhine  ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Predicted language: rakhine
Predicting random sentence 10: __label__beik    မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Predicted language: beik

Processing with model: 5gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 5gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.378s
user    0m0.663s
sys     0m2.259s
Predicting random sentence 1: __label__pao      နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Predicted language: pao
Predicting random sentence 2: __label__sgaw_kayin       လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 3: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 4: __label__shan     တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Predicted language: mon
Predicting random sentence 5: __label__shan     ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Predicted language: mon
Predicting random sentence 6: __label__rakhine  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Predicted language: rakhine
Predicting random sentence 7: __label__dawei    ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei
Predicting random sentence 8: __label__po_kayin ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Predicted language: po_kayin
Predicting random sentence 9: __label__dawei    ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Predicted language: dawei
Predicting random sentence 10: __label__po_kayin        ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Predicted language: po_kayin

Processing with model: 6gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 6gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.387s
user    0m0.672s
sys     0m2.230s
Predicting random sentence 1: __label__po_kayin ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Predicted language: po_kayin
Predicting random sentence 2: __label__beik     အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
Predicted language: beik
Predicting random sentence 3: __label__mon      သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon
Predicting random sentence 4: __label__beik     နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Predicted language: beik
Predicting random sentence 5: __label__pao      နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Predicted language: pao
Predicting random sentence 6: __label__bamar_burmese    ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Predicted language: bamar
Predicting random sentence 7: __label__pao      ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Predicted language: pao
Predicting random sentence 8: __label__pao      ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Predicted language: pao
Predicting random sentence 9: __label__sgaw_kayin       လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 10: __label__beik    ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Predicted language: beik

Processing with model: 7gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 7gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.396s
user    0m0.669s
sys     0m2.226s
Predicting random sentence 1: __label__sgaw_kayin       ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 2: __label__rakhine  မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Predicted language: rakhine
Predicting random sentence 3: __label__dawei    ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Predicted language: dawei
Predicting random sentence 4: __label__mon      ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Predicted language: mon
Predicting random sentence 5: __label__rakhine  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Predicted language: rakhine
Predicting random sentence 6: __label__pao      ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Predicted language: pao
Predicting random sentence 7: __label__rakhine  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Predicted language: rakhine
Predicting random sentence 8: __label__dawei    ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei
Predicting random sentence 9: __label__bamar_burmese    ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Predicted language: bamar
Predicting random sentence 10: __label__po_kayin        ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Predicted language: po_kayin

All processing completed.

real    0m20.781s
user    0m39.862s
sys     2m0.957s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

နောက်တစ်ခေါက် ထပ် experiment လုပ်ခဲ့တယ်။ ရလဒ်က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test_mixed_10random4exp.sh | tee test_mixed4_with_10_random.log
Processing with model: 3gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 3gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.378s
user    0m0.747s
sys     0m2.184s
Predicting random sentence 1: __label__bamar_burmese    ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Predicted language: bamar
Predicting random sentence 2: __label__rakhine  ငါ အ လုပ် မ ပြီး သိ ပါ ။
Predicted language: rakhine
Predicting random sentence 3: __label__rakhine  ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine
Predicting random sentence 4: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Predicted language: sgaw_kayin
Predicting random sentence 5: __label__dawei    ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Predicted language: dawei
Predicting random sentence 6: __label__rakhine  မင်း မိန်း စ ရာ မ လို ပါ ။
Predicted language: rakhine
Predicting random sentence 7: __label__po_kayin ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin
Predicting random sentence 8: __label__bamar_burmese    က လေး က အိမ် မှာ ပါ
Predicted language: bamar
Predicting random sentence 9: __label__rakhine  ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine
Predicting random sentence 10: __label__po_kayin        ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Predicted language: po_kayin

Processing with model: 4gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 4gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.356s
user    0m0.698s
sys     0m2.210s
Predicting random sentence 1: __label__rakhine  ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine
Predicting random sentence 2: __label__dawei    နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Predicted language: dawei
Predicting random sentence 3: __label__bamar_burmese    ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Predicted language: bamar
Predicting random sentence 4: __label__shan     ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Predicted language: mon
Predicting random sentence 5: __label__rakhine  ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Predicted language: rakhine
Predicting random sentence 6: __label__shan     တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Predicted language: mon
Predicting random sentence 7: __label__mon      ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Predicted language: mon
Predicting random sentence 8: __label__pao      ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Predicted language: pao
Predicting random sentence 9: __label__mon      ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Predicted language: mon
Predicting random sentence 10: __label__pao     ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Predicted language: pao

Processing with model: 5gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 5gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.376s
user    0m0.761s
sys     0m2.164s
Predicting random sentence 1: __label__rakhine  ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine
Predicting random sentence 2: __label__po_kayin ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Predicted language: po_kayin
Predicting random sentence 3: __label__sgaw_kayin       က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Predicted language: sgaw_kayin
Predicting random sentence 4: __label__pao      ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Predicted language: pao
Predicting random sentence 5: __label__po_kayin ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Predicted language: po_kayin
Predicting random sentence 6: __label__mon      သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon
Predicting random sentence 7: __label__dawei    ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Predicted language: dawei
Predicting random sentence 8: __label__shan     ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Predicted language: mon
Predicting random sentence 9: __label__mon      ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Predicted language: mon
Predicting random sentence 10: __label__rakhine မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Predicted language: rakhine

Processing with model: 6gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 6gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.392s
user    0m0.784s
sys     0m2.155s
Predicting random sentence 1: __label__mon      လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Predicted language: mon
Predicting random sentence 2: __label__mon      သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon
Predicting random sentence 3: __label__po_kayin ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Predicted language: po_kayin
Predicting random sentence 4: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 5: __label__rakhine  ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Predicted language: rakhine
Predicting random sentence 6: __label__rakhine  ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Predicted language: rakhine
Predicting random sentence 7: __label__shan     ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Predicted language: dawei
Predicting random sentence 8: __label__beik     ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Predicted language: beik
Predicting random sentence 9: __label__sgaw_kayin       ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 10: __label__beik    အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
Predicted language: beik

Processing with model: 7gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 7gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.386s
user    0m0.799s
sys     0m2.139s
Predicting random sentence 1: __label__sgaw_kayin       ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 2: __label__shan     တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Predicted language: mon
Predicting random sentence 3: __label__rakhine  ငါ အ လုပ် မ ပြီး သိ ပါ ။
Predicted language: rakhine
Predicting random sentence 4: __label__bamar_burmese    ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar
Predicting random sentence 5: __label__shan     ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Predicted language: mon
Predicting random sentence 6: __label__bamar_burmese    ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar
Predicting random sentence 7: __label__rakhine  ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Predicted language: rakhine
Predicting random sentence 8: __label__po_kayin ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin
Predicting random sentence 9: __label__shan     ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Predicted language: mon
Predicting random sentence 10: __label__dawei   ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Predicted language: dawei

All processing completed.

real    0m20.705s
user    0m40.384s
sys     2m0.410s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ။ ဒီတစ်ခေါက် experiment ရလဒ်မှာတော့ 7gram model မှာ အထူးသဖြင့် ရှမ်း နဲ့ မွန်ကို မှန်မှန်ကန်ကန် classification မလုပ်ပေးနိုင်တာကို တွေ့ရတယ်။ နားလည်လိုက်တာက input လုပ်တဲ့ စာကြောင်းပေါ်ကိုလည်း မူတည်ပြီး language detection လုပ်တဲ့အခါမှာ လွဲနိုင်တယ်။ သိတဲ့အတိုင်းပဲ စာကြောင်း တစ်ကြောင်းတည်းမှာ ရှိတဲ့ စာလုံးကိုတချို့ကိုပဲ အခြေခံပြီး classification လုပ်ရတာမို့လို့ မော်ဒယ်အနေနဲ့လည်း ခက်ခဲတယ်။  


၅ခေါက် ပြည့်သွားအောင် အထက်ပါလိုမျိုး experiment ကိုပဲ နောက်တစ်ခေါက် ထပ် run ပြီး လေ့လာခဲ့တယ်။ ရလဒ်ကတော့ အောက်ပါအတိုင်းပါပဲ။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$ time ./test_mixed_10random4exp.sh | tee test_mixed5_with_10_random.log
Processing with model: 3gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 3gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.365s
user    0m0.727s
sys     0m2.191s
Predicting random sentence 1: __label__po_kayin အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Predicted language: po_kayin
Predicting random sentence 2: __label__rakhine  ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Predicted language: rakhine
Predicting random sentence 3: __label__bamar_burmese    ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar
Predicting random sentence 4: __label__shan     တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Predicted language: mon
Predicting random sentence 5: __label__mon      သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon
Predicting random sentence 6: __label__pao      ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Predicted language: pao
Predicting random sentence 7: __label__beik     နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Predicted language: beik
Predicting random sentence 8: __label__dawei    အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Predicted language: dawei
Predicting random sentence 9: __label__sgaw_kayin       လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 10: __label__mon     သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Predicted language: mon

Processing with model: 4gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 4gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.354s
user    0m0.795s
sys     0m2.111s
Predicting random sentence 1: __label__sgaw_kayin       ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 2: __label__dawei    အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Predicted language: dawei
Predicting random sentence 3: __label__shan     ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Predicted language: mon
Predicting random sentence 4: __label__po_kayin ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin
Predicting random sentence 5: __label__po_kayin ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Predicted language: po_kayin
Predicting random sentence 6: __label__bamar_burmese    တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Predicted language: bamar
Predicting random sentence 7: __label__po_kayin ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Predicted language: po_kayin
Predicting random sentence 8: __label__po_kayin ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Predicted language: po_kayin
Predicting random sentence 9: __label__beik     သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Predicted language: beik
Predicting random sentence 10: __label__mon_tst က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon

Processing with model: 5gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 5gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.378s
user    0m0.769s
sys     0m2.162s
Predicting random sentence 1: __label__pao      ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Predicted language: pao
Predicting random sentence 2: __label__dawei    အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Predicted language: dawei
Predicting random sentence 3: __label__po_kayin ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Predicted language: po_kayin
Predicting random sentence 4: __label__rakhine  ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Predicted language: rakhine
Predicting random sentence 5: __label__shan     ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Predicted language: mon
Predicting random sentence 6: __label__mon_tst  က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon
Predicting random sentence 7: __label__po_kayin ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Predicted language: po_kayin
Predicting random sentence 8: __label__pao      က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Predicted language: pao
Predicting random sentence 9: __label__mon_tst  က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Predicted language: mon
Predicting random sentence 10: __label__po_kayin        နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin

Processing with model: 6gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 6gram.model.bin
Number of test examples: 80
Precision at 1: 0.900
Recall at 1: 0.900

real    0m0.385s
user    0m0.723s
sys     0m2.215s
Predicting random sentence 1: __label__shan     တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Predicted language: mon
Predicting random sentence 2: __label__dawei    အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Predicted language: dawei
Predicting random sentence 3: __label__sgaw_kayin       တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
Predicted language: sgaw_kayin
Predicting random sentence 4: __label__sgaw_kayin       ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Predicted language: sgaw_kayin
Predicting random sentence 5: __label__bamar_burmese    ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar
Predicting random sentence 6: __label__beik     ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Predicted language: beik
Predicting random sentence 7: __label__shan     မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan
Predicting random sentence 8: __label__shan     မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Predicted language: shan
Predicting random sentence 9: __label__pao      က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Predicted language: pao
Predicting random sentence 10: __label__bamar_burmese   ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Predicted language: bamar

Processing with model: 7gram.model.bin
Testing with file: all_test.fasttext.shuf and model: 7gram.model.bin
Number of test examples: 80
Precision at 1: 0.887
Recall at 1: 0.887

real    0m0.387s
user    0m0.679s
sys     0m2.260s
Predicting random sentence 1: __label__mon      ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Predicted language: mon
Predicting random sentence 2: __label__rakhine  သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Predicted language: rakhine
Predicting random sentence 3: __label__dawei    အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Predicted language: dawei
Predicting random sentence 4: __label__bamar_burmese    မင်္ဂ လာ ပါ ဆ ရာ မ
Predicted language: bamar
Predicting random sentence 5: __label__sgaw_kayin       ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Predicted language: sgaw_kayin
Predicting random sentence 6: __label__pao      ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Predicted language: pao
Predicting random sentence 7: __label__shan     ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Predicted language: mon
Predicting random sentence 8: __label__shan     တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Predicted language: mon
Predicting random sentence 9: __label__po_kayin နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Predicted language: po_kayin
Predicting random sentence 10: __label__mon     အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Predicted language: mon

All processing completed.

real    0m20.750s
user    0m39.720s
sys     2m1.126s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/fasttext$
```

## To Do

- ကယားလီ၊ ကချင်၊ ရဝမ်၊ မီဇိုချင်း ဘာသာတွေပါ ထည့်ပြီး experiment လုပ်ရန် 
(ဒေတာတွေက ရှိပြီးသားမို့လို့ အားလုံးစုံသွားအောင် ထည့်ပြီး စမ်းတာက စာတမ်းအတွက် ပိုကောင်းတာမို့လို့၊ သို့သော် အသစ်ထည့်မယ့် ဘာသာစကားတွေက လက်ရှိ စမ်းနေတဲ့ ဘာသာစကားတွေနဲ့ မတူပဲ alphabet ကို သုံးတာ၊ ကယားလီ ဆိုရင်လည်း သီးသန့် glyph မို့လို့ ကွဲကွဲပြားပြား ဖြစ်နေမှာမို့လို့ မော်ဒယ်အတွက် သက်ရောက်မှုက သိပ်မရှိနိုင်ဘူးလို့ ခန့်မှန်းထားတယ်)

- Rule-based ကို စဉ်းစားလို့ ရနိုင်မလား ?!
- Character frequency + Syllable frequency နှစ်မျိုးကို ပေါင်းပြီးမှ decision လုပ်ရင်ကော

## Character and Syllable Frequency Approach 

syllable segmented file, character segmented file ဆိုတာထက် segmentation ဘာမှ မလုပ်ထားတဲ့ ဖိုင်အနေနဲ့ သွားကြည့်မှာမို့လို့ python code တစ်ပုဒ်ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ cat ./rm_space.py
"""

A program to remove spaces from all files located in a specified input directory.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 23 Jan 2024

Usage:
python ./rm_space.py --input ./syl_seg --output ./raw

"""

import os
import argparse

def process_files(input_dir, output_dir):
    # Create output directory if it doesn't exist
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    for filename in os.listdir(input_dir):
        input_file_path = os.path.join(input_dir, filename)
        output_file_path = os.path.join(output_dir, f"{filename}.raw")

        # Read the content and remove spaces
        with open(input_file_path, 'r', encoding='utf-8') as file:
            content = file.read().replace(' ', '')

        # Write the content to the new file in the output directory
        with open(output_file_path, 'w', encoding='utf-8') as file:
            file.write(content)

        print(f"Processed: {input_file_path} -> {output_file_path}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Process files to remove spaces and save with .raw extension.")
    parser.add_argument('--input', type=str, required=True, help="Input directory path")
    parser.add_argument('--output', type=str, required=True, help="Output directory path")

    args = parser.parse_args()

    process_files(args.input, args.output)
```

raw ဖိုင်အဖြစ် အောက်ပါအတိုင်း ပြောင်းခဲ့တယ်။ 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ python ./rm_space.py --input ./syl_seg --output ./raw
Processed: ./syl_seg/mon.all.syl -> ./raw/mon.all.syl.raw
Processed: ./syl_seg/bamar.all.syl -> ./raw/bamar.all.syl.raw
Processed: ./syl_seg/po_kayin.all.syl -> ./raw/po_kayin.all.syl.raw
Processed: ./syl_seg/rakhine.all.syl -> ./raw/rakhine.all.syl.raw
Processed: ./syl_seg/shan.all.syl -> ./raw/shan.all.syl.raw
Processed: ./syl_seg/beik.all.syl -> ./raw/beik.all.syl.raw
Processed: ./syl_seg/sgaw_kayin.all.syl -> ./raw/sgaw_kayin.all.syl.raw
Processed: ./syl_seg/dawei.all.syl -> ./raw/dawei.all.syl.raw
Processed: ./syl_seg/pao.all.syl -> ./raw/pao.all.syl.raw
```

Checked the output raw files ... 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ ls ./syl_seg/
bamar.all.syl  dawei.all.syl  pao.all.syl       rakhine.all.syl     shan.all.syl
beik.all.syl   mon.all.syl    po_kayin.all.syl  sgaw_kayin.all.syl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ ls ./raw
bamar.all.syl.raw  mon.all.syl.raw       rakhine.all.syl.raw
beik.all.syl.raw   pao.all.syl.raw       sgaw_kayin.all.syl.raw
dawei.all.syl.raw  po_kayin.all.syl.raw  shan.all.syl.raw
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

Check the output content ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/raw$ head bamar.all.syl.raw
နေကမီးကျီးခဲလိုရဲရဲတောက်ပြီးတက်လာတယ်ပြီးတော့ငါတို့ရပ်နိုင်ရုံလောက်ပဲရှိပေမဲ့အခုဘယ်နည်းနဲ့မဆိုတိုက်ခိုက်ရတော့မယ်စစ်သည်ရဲမက်တွေမဟုတ်ဘူးတစ်ယောက်ချင်းတိုက်ခိုက်တာမဟုတ်ဘူးဒါကရန်ပွဲတစ်ပွဲ
တောမီးတွေနဲ့ရေကြီးမှုတွေရဲ့ဘေးဒဏ်ကိုခံခဲ့ရတဲ့အမေရိကန်ပြည်ထောင်စုတစ်ခွင်ကမိသားစုတွေအတွက်ကြက်ခြေနီအဖွဲ့ကထောက်ပံ့မှုတွေပေးနေတယ်
ဒီညနေကျွန်တော်တို့ရဲ့ပွဲကိုအစီအစဉ်မှူးအဖြစ်ဆောင်ရွက်ပေးသူကတော့ချစ်စရာကောင်းတဲ့ဖြစ်ပါတယ်
ဒါကဘာအတွက်လဲဆိုတာမှန်းကြည့်
မင်းရောငါရောမင်းရဲ့ခွေးလေးရောငါတို့ရဲ့သိမြင်နားလည်မှုစကြဝဠာနယ်ပယ်တစ်ခုထဲမှာပိတ်မိနေကြတယ်ငါတို့လွတ်မြောက်နိုင်ရင်အရာဝတ္ထုတွေကိုမြင်နိုင်တဲ့တခြားနည်းလမ်းတွေအများကြီးရှိလာမယ်
သူတို့အလုပ်ခွင်ရဲ့သနားစရာအခြေအနေဟာအရင်ကထက်ပိုပြီးအခက်အခဲတွေနဲ့ရင်ဆိုင်လာရတယ်
လုပ်ဖော်ကိုင်ဖက်အသစ်ဒီနေ့အပြင်မှာအရမ်းအေးတာတောင်မှပတ်ဝန်းကျင်ထိန်းသိမ်းရေးအတွက်ကြံ့ကြံ့ခံနေတုန်းပဲ
တန်နဲ့ချီတဲ့ပိုးကောင်တွေငါ့ရှေ့ကနေရာတိုင်းမှာငါသေတော့မယ်လို့ငါထင်တယ်
သို့ဟားဟားဟားမင်းငါ့ကိုလွမ်းနေမှာပဲအဲဒါကိုဝန်ခံလိုက်တာလုံးဝကောင်းပါတယ်
အပြင်ကစာရွက်အရွယ်အစားထက်ကျော်လွန်ပြီးလျှံထွက်နေတဲ့စာသားတွေနဲ့ဖွဲ့ပြီးသားစာမျက်နှာတွေကိုခေါက်လိုက်အဲဒါကိုလို့လည်းခေါ်တယ်
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/raw$ head shan.all.syl.raw
ယွင်ႈၵုင်ႇၵူၼ်းႁတ်းႁၢၼ်ႁႃႉ
ဢၼ်ၸႅတ်ႈတူၺ်းသူႁေႃႈၵႃးၼႆႉတွပ်ႇယဝ်ႉယဝ်ႉႁႃႉ
လွင်ႈၶူင်သၢင်ႈမႂ်းဢမ်ႇႁိုင်သင်တေဢွင်ႇမၢၼ်ယဝ်ႉ
ဢၼ်ၼၼ်ႉပဵၼ်လွင်ႈၵိတ်ႇၶွင်ႈသူ
တေၵိၼ်သေဢၼ်ဢၼ်ႁႃႉ
ဢွမ်မူင်းၵဝ်ႁႃဢမ်ႇႁၼ်
ပဵၼ်ၵူၼ်းဢၼ်လဵၼ်ႈၸိူင်းၶႅၼ်ႇႄတႉယဝ်ႈ
ၵုပ်ႉၵူႈသူၼႆႉတႄႇၽုၺ်ႇသႅင်ႇၵိၼ်ယမ်ႉၼႆႉမႃးတေႃႇမိူဝ်ႈလဵဝ်ဢၼ်ၽႅဝ်မႃးၼႆႉပဵၼ်႙႙႙ၵူႈယဝ်ႉ
ၼင်ႈႁွင်ႈတၢင်းၼႃႈဢဝ်ၼႄႈ
လႆႈႁႅင်းလီၵႃႈႁိုဝ်
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/raw$
```

ပြီးတော့ character-based + syllable-based frequency dictionary တွေကို language အားလုံးအတွက် ဆောက်ဖို့လည်း shell script ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ cat ./build_dict.sh
#!/bin/bash

# Define the base directory and the Python script
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/char_syl_freq"
PYTHON_SCRIPT="$BASE_DIR/char_syl_freq_lang_detect.py"
TEXT_DIR="$BASE_DIR/raw"  # Assuming you have raw text files for training
PROFILE_DIR="$BASE_DIR/profile"

# Create the profile directory if it doesn't exist
mkdir -p "$PROFILE_DIR"

# Loop through each text file in the text_files directory
for file in "$TEXT_DIR"/*.raw; do
    # Extract the language name from the filename
    filename=$(basename -- "$file")
    language=${filename%%.*}

    # Define the output profile filename
    output_profile="$PROFILE_DIR/${language}_combined_profile.json"

    # Run the Python script to create the profile
    if python3 "$PYTHON_SCRIPT" --mode train --input "$file" --output "$output_profile"; then
        echo "Created combined character and syllable language profile for $language."
    else
        echo "Error in creating profile for $language. Check the input file and script."
        exit 1
    fi
done

echo "All language profiles have been created."
```

Building combined freq dictionaries ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ time ./build_dict.sh
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/bamar_combined_profile.json
Created combined character and syllable language profile for bamar.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/beik_combined_profile.json
Created combined character and syllable language profile for beik.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/dawei_combined_profile.json
Created combined character and syllable language profile for dawei.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/mon_combined_profile.json
Created combined character and syllable language profile for mon.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/pao_combined_profile.json
Created combined character and syllable language profile for pao.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/po_kayin_combined_profile.json
Created combined character and syllable language profile for po_kayin.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/rakhine_combined_profile.json
Created combined character and syllable language profile for rakhine.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/sgaw_kayin_combined_profile.json
Created combined character and syllable language profile for sgaw_kayin.
Frequency profile saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_freq/profile/shan_combined_profile.json
Created combined character and syllable language profile for shan.
All language profiles have been created.

real    0m2.095s
user    0m1.837s
sys     0m0.257s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

output အဖြစ် ထွက်လာတဲ့ char+freq combined freq dictionary or profile ဖိုင်တွေက အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$ ls
bamar_combined_profile.json  po_kayin_combined_profile.json
beik_combined_profile.json   rakhine_combined_profile.json
dawei_combined_profile.json  sgaw_kayin_combined_profile.json
mon_combined_profile.json    shan_combined_profile.json
pao_combined_profile.json
```

json ဖိုင်တွေကို လေ့လာကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$ jq . ./bamar_combined_profile.json | head
{
  "char_freq": {
    "န": 0.03075064057623789,
    "ေ": 0.047584740646742264,
    "က": 0.050672723053937586,
    "မ": 0.033901227292895256,
    "ီ": 0.014187328987136802,
    "း": 0.05850670834987462,
    "ျ": 0.017534672104960597,
    "ခ": 0.015219306374062736,
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$ jq . ./bamar_combined_profile.json  | tail
    "ပေါ့်": 1.51462827992754e-06,
    "ဩတ္တပ္ပ": 6.05851311971016e-06,
    "ဩတ္တပ္တ": 1.51462827992754e-06,
    "နန္တ": 1.51462827992754e-06,
    "ဒေါ့်": 1.51462827992754e-06,
    "စွ": 1.51462827992754e-06,
    "ယွမ့်": 1.51462827992754e-06,
    "ဆစ့်": 1.51462827992754e-06
  }
}
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$
```

for Mon profile ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$ jq . ./mon_combined_profile.json | head
{
  "char_freq": {
    "၂": 8.005740412384583e-05,
    "၀": 0.0006226686987410232,
    "မ": 0.02315438032604119,
    "ိ": 0.027931138772097325,
    "ဏ": 0.007845625604136892,
    "ေ": 0.05183272153662775,
    "တ": 0.036488385746223956,
    "်": 0.12899026857776538,
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$ jq . ./mon_combined_profile.json | tail
    "သုင်လ္ဒေါဝ်တ္ၚဲၜိုတ်": 9.195148639577759e-06,
    "ရေင်အ္စာ": 1.8390297279155518e-05,
    "ယျေ": 9.195148639577759e-06,
    "။ ္အ္အ္အ္အ္အ္အ": 9.195148639577759e-06,
    "လဵု‌": 9.195148639577759e-06,
    "မၠောန်သ္ၚိ": 9.195148639577759e-06,
    "ဗၠာဲက္ဍုဟ်": 9.195148639577759e-06,
    "မျိုင်": 9.195148639577759e-06
  }
}
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/profile$
```

Make raw files for test-data:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ python ./rm_space.py --input ./eg_input/ --output ./eg_input_raw
Processed: ./eg_input/sgaw_kayin.txt -> ./eg_input_raw/sgaw_kayin.txt.raw
Processed: ./eg_input/po_kayin.txt -> ./eg_input_raw/po_kayin.txt.raw
Processed: ./eg_input/mon.txt -> ./eg_input_raw/mon.txt.raw
Processed: ./eg_input/pao.txt -> ./eg_input_raw/pao.txt.raw
Processed: ./eg_input/shan.txt -> ./eg_input_raw/shan.txt.raw
Processed: ./eg_input/mon_tst.txt -> ./eg_input_raw/mon_tst.txt.raw
Processed: ./eg_input/bamar_burmese.txt -> ./eg_input_raw/bamar_burmese.txt.raw
Processed: ./eg_input/rakhine.txt -> ./eg_input_raw/rakhine.txt.raw
Processed: ./eg_input/beik.txt -> ./eg_input_raw/beik.txt.raw
Processed: ./eg_input/dawei.txt -> ./eg_input_raw/dawei.txt.raw
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

Check the raw test-data files:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/eg_input_raw$ head -n 3 *.raw
==> bamar_burmese.txt.raw <==
နေကောင်းလား
ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
မင်္ဂလာပါဆရာမ

==> beik.txt.raw <==
ဖယ်သူလေကိုမေးရိလဲ။
သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
ဘဇာလောက်စိတ်လှုပ်ရှားရိ။

==> dawei.txt.raw <==
ဟှယ်လူလေဟှိုမေးကေ့နူး။
အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
ဟှယ်လော့စိလှုပ်ရှားဟှယ်။

==> mon_tst.txt.raw <==
လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
ကသပ်ပ္ဍဲဗှ်ေဂှ်

==> mon.txt.raw <==
ဗှ်ေဟယျတုဲမာန်ဟာ။
ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။

==> pao.txt.raw <==
နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
ဝွေꩻမူႏတတောင်ချာတဝ်းဒွုမ်ပါꩻမုဲင်ꩻမုဲင်ꩻ
နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ

==> po_kayin.txt.raw <==
ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.

==> rakhine.txt.raw <==
သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
ဆူပြီးရီကိုသောက်သင့်ရေ။

==> sgaw_kayin.txt.raw <==
တၢ်ဝဲန့ၣ်နတဘျးစဲဒီးအဂၤတခါဧဲၣ်.
ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.

==> shan.txt.raw <==
မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq/eg_input_raw$
```

### Shell script for testing with char_syl_freq approach

language detection experiment အတွက် shell script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define directories
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/char_syl_freq"
PYTHON_SCRIPT="$BASE_DIR/char_syl_freq_lang_detect.py"
INPUT_DIR="$BASE_DIR/eg_input_raw"
PROFILE_DIR="$BASE_DIR/profile"

# Number of random sentences to test
NUM_RANDOM_SENTENCES=10

# Loop through each input file in the directory
for input_file in "$INPUT_DIR"/*.raw; do
    echo "Processing file: $(basename "$input_file")"
    
    # Run detection on the entire file
    python "$PYTHON_SCRIPT" --input "$input_file" --mode detect --profiles "$PROFILE_DIR"
    
    # Extract and predict random sentences from the file
    for i in $(seq 1 $NUM_RANDOM_SENTENCES); do
        random_sentence=$(shuf -n 1 "$input_file")
        echo "Predicting random sentence $i: $random_sentence"
        python "$PYTHON_SCRIPT" --input "$random_sentence" --mode detect --profiles "$PROFILE_DIR"
    done

    echo ""
done

echo "All processing completed."

```

Language detection experiment no.1  with char_syl_freq approach ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ time ./test4exp.sh | tee test1.log
Processing file: bamar_burmese.txt.raw
Detected language: bamar_combined_profile.json
Predicting random sentence 1: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 2: ကျောင်းသားကျောင်းသွားပါ
Detected language: rakhine_combined_profile.json
Predicting random sentence 3: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 4: ပါပါသမီးကိုလွမ်းနေတယ်
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: ကလေးကအိမ်မှာပါ
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Detected language: bamar_combined_profile.json
Predicting random sentence 7: နေကောင်းလား
Detected language: beik_combined_profile.json
Predicting random sentence 8: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Detected language: beik_combined_profile.json
Predicting random sentence 9: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 10: ကလေးကအိမ်မှာပါ
Detected language: rakhine_combined_profile.json

Processing file: beik.txt.raw
Detected language: beik_combined_profile.json
Predicting random sentence 1: ဖယ်သူလေကိုမေးရိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 2: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 3: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 4: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Detected language: beik_combined_profile.json
Predicting random sentence 6: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Detected language: beik_combined_profile.json
Predicting random sentence 7: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Detected language: beik_combined_profile.json
Predicting random sentence 8: ဖယ်သူလေကိုမေးရိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 9: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 10: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json

Processing file: dawei.txt.raw
Detected language: dawei_combined_profile.json
Predicting random sentence 1: အဲဝယ်ဟှားဟှိုလက်ထပ်လိုက်ဇာလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 2: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 3: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 4: ခံဗျားခရီးထွပ်ဟှလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 5: နန်ငါ့ဟှိုရှင်းပြပါလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 6: အဲဝယ်ဟှားဟှိုလက်ထပ်လိုက်ဇာလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 7: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Detected language: dawei_combined_profile.json
Predicting random sentence 8: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 9: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Detected language: dawei_combined_profile.json
Predicting random sentence 10: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Detected language: dawei_combined_profile.json

Processing file: mon_tst.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 2: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 6: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 8: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 9: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 10: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json

Processing file: mon.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 2: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Detected language: mon_combined_profile.json
Predicting random sentence 3: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Detected language: mon_combined_profile.json
Predicting random sentence 4: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 5: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Detected language: mon_combined_profile.json
Predicting random sentence 6: ဗှ်ေဟယျတုဲမာန်ဟာ။
Detected language: mon_combined_profile.json
Predicting random sentence 7: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 8: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 9: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Detected language: mon_combined_profile.json
Predicting random sentence 10: ဗှ်ေဟယျတုဲမာန်ဟာ။
Detected language: mon_combined_profile.json

Processing file: pao.txt.raw
Detected language: pao_combined_profile.json
Predicting random sentence 1: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 2: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 3: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 4: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Detected language: pao_combined_profile.json
Predicting random sentence 5: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 6: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 7: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 8: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Detected language: pao_combined_profile.json
Predicting random sentence 9: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 10: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Detected language: pao_combined_profile.json

Processing file: po_kayin.txt.raw
Detected language: po_kayin_combined_profile.json
Predicting random sentence 1: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 2: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 3: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 4: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 5: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 6: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 7: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 8: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 9: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 10: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json

Processing file: rakhine.txt.raw
Detected language: rakhine_combined_profile.json
Predicting random sentence 1: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 2: ငါအလုပ်မပြီးသိပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 3: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 4: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: ငါအလုပ်မပြီးသိပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 7: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Detected language: rakhine_combined_profile.json
Predicting random sentence 8: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Detected language: rakhine_combined_profile.json
Predicting random sentence 9: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 10: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Detected language: rakhine_combined_profile.json

Processing file: sgaw_kayin.txt.raw
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 1: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 2: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 3: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 4: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 5: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 6: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 7: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 8: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 9: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 10: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json

Processing file: shan.txt.raw
Detected language: shan_combined_profile.json
Predicting random sentence 1: မိူဝ်ႈပူၼ်ႉမႃးဝၼ်းသုၵ်းၵၢင်ၼႂ်႑႑မွင်းၼၼ်ႉသူမီးယူႇတီႈလႂ်။
Detected language: shan_combined_profile.json
Predicting random sentence 2: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 3: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 4: မိူဝ်ႈပူၼ်ႉမႃးဝၼ်းသုၵ်းၵၢင်ၼႂ်႑႑မွင်းၼၼ်ႉသူမီးယူႇတီႈလႂ်။
Detected language: shan_combined_profile.json
Predicting random sentence 5: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 6: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 7: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 8: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 9: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 10: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Detected language: shan_combined_profile.json

All processing completed.

real    0m4.994s
user    0m4.278s
sys     0m0.715s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

Language detection experiment no.2  with char_syl_freq approach ... 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ time ./test4exp.sh | tee test2.log
Processing file: bamar_burmese.txt.raw
Detected language: bamar_combined_profile.json
Predicting random sentence 1: ကလေးကအိမ်မှာပါ
Detected language: rakhine_combined_profile.json
Predicting random sentence 2: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Detected language: beik_combined_profile.json
Predicting random sentence 3: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Detected language: bamar_combined_profile.json
Predicting random sentence 4: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 5: မင်္ဂလာပါဆရာမ
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: မင်္ဂလာပါဆရာမ
Detected language: rakhine_combined_profile.json
Predicting random sentence 7: ပါပါသမီးကိုလွမ်းနေတယ်
Detected language: rakhine_combined_profile.json
Predicting random sentence 8: မင်္ဂလာပါဆရာမ
Detected language: rakhine_combined_profile.json
Predicting random sentence 9: နေကောင်းလား
Detected language: beik_combined_profile.json
Predicting random sentence 10: မင်္ဂလာပါဆရာမ
Detected language: rakhine_combined_profile.json

Processing file: beik.txt.raw
Detected language: beik_combined_profile.json
Predicting random sentence 1: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Detected language: beik_combined_profile.json
Predicting random sentence 2: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Detected language: bamar_combined_profile.json
Predicting random sentence 3: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Detected language: beik_combined_profile.json
Predicting random sentence 4: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: အဲဒီကိုသောဖို့ငါမင်းကိုငါမတိုက်တွန်းရ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: ဖယ်သူလေကိုမေးရိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 7: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Detected language: bamar_combined_profile.json
Predicting random sentence 8: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Detected language: bamar_combined_profile.json
Predicting random sentence 9: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Detected language: beik_combined_profile.json
Predicting random sentence 10: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Detected language: bamar_combined_profile.json

Processing file: dawei.txt.raw
Detected language: dawei_combined_profile.json
Predicting random sentence 1: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 2: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 3: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 4: နန်ငါ့ဟှိုရှင်းပြပါလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 5: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Detected language: dawei_combined_profile.json
Predicting random sentence 6: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Detected language: dawei_combined_profile.json
Predicting random sentence 7: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 8: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 9: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 10: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Detected language: dawei_combined_profile.json

Processing file: mon_tst.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 2: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 6: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 8: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 9: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json

Processing file: mon.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 2: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Detected language: mon_combined_profile.json
Predicting random sentence 3: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 4: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 5: ဗှ်ေဟယျတုဲမာန်ဟာ။
Detected language: mon_combined_profile.json
Predicting random sentence 6: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 7: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 8: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 9: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Detected language: mon_combined_profile.json
Predicting random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json

Processing file: pao.txt.raw
Detected language: pao_combined_profile.json
Predicting random sentence 1: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 2: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 3: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 4: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Detected language: pao_combined_profile.json
Predicting random sentence 5: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Detected language: pao_combined_profile.json
Predicting random sentence 6: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Detected language: pao_combined_profile.json
Predicting random sentence 7: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Detected language: pao_combined_profile.json
Predicting random sentence 8: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 9: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Detected language: pao_combined_profile.json
Predicting random sentence 10: ဝွေꩻမူႏတတောင်ချာတဝ်းဒွုမ်ပါꩻမုဲင်ꩻမုဲင်ꩻ
Detected language: pao_combined_profile.json

Processing file: po_kayin.txt.raw
Detected language: po_kayin_combined_profile.json
Predicting random sentence 1: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 2: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 3: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 4: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 5: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 6: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 7: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 8: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 9: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 10: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Detected language: po_kayin_combined_profile.json

Processing file: rakhine.txt.raw
Detected language: rakhine_combined_profile.json
Predicting random sentence 1: မင်းမိန်းစရာမလိုပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 2: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 3: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 4: ကိုယ်မင်းကိုနားလည်ပါရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: ကိုယ်မင်းကိုနားလည်ပါရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: မင်းမိန်းစရာမလိုပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 7: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 8: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 9: ငါအလုပ်မပြီးသိပါ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 10: မင်းမိန်းစရာမလိုပါ။
Detected language: rakhine_combined_profile.json

Processing file: sgaw_kayin.txt.raw
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 1: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 2: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 3: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 4: တၢ်ဝဲန့ၣ်နတဘျးစဲဒီးအဂၤတခါဧဲၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 5: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 6: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 7: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 8: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 9: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 10: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Detected language: sgaw_kayin_combined_profile.json

Processing file: shan.txt.raw
Detected language: shan_combined_profile.json
Predicting random sentence 1: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 2: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 3: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Detected language: shan_combined_profile.json
Predicting random sentence 4: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 5: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 6: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 7: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 8: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 9: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 10: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Detected language: shan_combined_profile.json

All processing completed.

real    0m5.003s
user    0m4.275s
sys     0m0.730s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

Language detection experiment no.3  with char_syl_freq approach ... 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$ time ./test4exp.sh | tee test3.log
Processing file: bamar_burmese.txt.raw
Detected language: bamar_combined_profile.json
Predicting random sentence 1: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 2: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Detected language: bamar_combined_profile.json
Predicting random sentence 3: နေကောင်းလား
Detected language: beik_combined_profile.json
Predicting random sentence 4: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 5: ကလေးကအိမ်မှာပါ
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: ပါပါသမီးကိုလွမ်းနေတယ်
Detected language: rakhine_combined_profile.json
Predicting random sentence 7: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 8: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Detected language: beik_combined_profile.json
Predicting random sentence 9: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Detected language: bamar_combined_profile.json
Predicting random sentence 10: နေကောင်းလား
Detected language: beik_combined_profile.json

Processing file: beik.txt.raw
Detected language: beik_combined_profile.json
Predicting random sentence 1: ဖယ်သူလေကိုမေးရိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 2: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 3: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Detected language: beik_combined_profile.json
Predicting random sentence 4: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Detected language: beik_combined_profile.json
Predicting random sentence 5: နင်ခရီးမထွက်ခဲ့ရလား။
Detected language: beik_combined_profile.json
Predicting random sentence 6: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Detected language: beik_combined_profile.json
Predicting random sentence 7: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Detected language: beik_combined_profile.json
Predicting random sentence 8: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 9: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 10: နင်ခရီးမထွက်ခဲ့ရလား။
Detected language: beik_combined_profile.json

Processing file: dawei.txt.raw
Detected language: dawei_combined_profile.json
Predicting random sentence 1: နန်ငါ့ဟှိုရှင်းပြပါလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 2: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 3: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 4: နန်ငါ့ဟှိုရှင်းပြပါလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 5: နန်ငါ့ဟှိုရှင်းပြပါလား။
Detected language: dawei_combined_profile.json
Predicting random sentence 6: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 7: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Detected language: dawei_combined_profile.json
Predicting random sentence 8: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Detected language: dawei_combined_profile.json
Predicting random sentence 9: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Detected language: dawei_combined_profile.json
Predicting random sentence 10: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Detected language: dawei_combined_profile.json

Processing file: mon_tst.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 2: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 4: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Detected language: mon_combined_profile.json
Predicting random sentence 6: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 8: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 9: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json
Predicting random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json

Processing file: mon.txt.raw
Detected language: mon_combined_profile.json
Predicting random sentence 1: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 2: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 3: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 4: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Detected language: mon_combined_profile.json
Predicting random sentence 5: ဗှ်ေဟယျတုဲမာန်ဟာ။
Detected language: mon_combined_profile.json
Predicting random sentence 6: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 7: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Detected language: mon_combined_profile.json
Predicting random sentence 8: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Detected language: mon_combined_profile.json
Predicting random sentence 9: ဗှ်ေဟယျတုဲမာန်ဟာ။
Detected language: mon_combined_profile.json
Predicting random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Detected language: mon_combined_profile.json

Processing file: pao.txt.raw
Detected language: pao_combined_profile.json
Predicting random sentence 1: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Detected language: pao_combined_profile.json
Predicting random sentence 2: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Detected language: pao_combined_profile.json
Predicting random sentence 3: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 4: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Detected language: pao_combined_profile.json
Predicting random sentence 5: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Detected language: pao_combined_profile.json
Predicting random sentence 6: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Detected language: pao_combined_profile.json
Predicting random sentence 7: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Detected language: pao_combined_profile.json
Predicting random sentence 8: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Detected language: pao_combined_profile.json
Predicting random sentence 9: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Detected language: pao_combined_profile.json
Predicting random sentence 10: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Detected language: pao_combined_profile.json

Processing file: po_kayin.txt.raw
Detected language: po_kayin_combined_profile.json
Predicting random sentence 1: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 2: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 3: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 4: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 5: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 6: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 7: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 8: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 9: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Detected language: po_kayin_combined_profile.json
Predicting random sentence 10: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Detected language: po_kayin_combined_profile.json

Processing file: rakhine.txt.raw
Detected language: rakhine_combined_profile.json
Predicting random sentence 1: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 2: ဆူပြီးရီကိုသောက်သင့်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 3: ကိုယ်မင်းကိုနားလည်ပါရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 4: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 5: ဆူပြီးရီကိုသောက်သင့်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 6: မင်းတောင်တိကိုတက်နီကျလား။
Detected language: rakhine_combined_profile.json
Predicting random sentence 7: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 8: ဆူပြီးရီကိုသောက်သင့်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 9: ဆူပြီးရီကိုသောက်သင့်ရေ။
Detected language: rakhine_combined_profile.json
Predicting random sentence 10: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Detected language: rakhine_combined_profile.json

Processing file: sgaw_kayin.txt.raw
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 1: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 2: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 3: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 4: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 5: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 6: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 7: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 8: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 9: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Detected language: sgaw_kayin_combined_profile.json
Predicting random sentence 10: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Detected language: sgaw_kayin_combined_profile.json

Processing file: shan.txt.raw
Detected language: shan_combined_profile.json
Predicting random sentence 1: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 2: တႃႇမၼ်းၼၢင်းႁဝ်းတေထၢမ်ဢမ်ႇၸႂ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 3: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 4: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 5: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 6: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Detected language: shan_combined_profile.json
Predicting random sentence 7: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 8: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Detected language: shan_combined_profile.json
Predicting random sentence 9: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Detected language: shan_combined_profile.json
Predicting random sentence 10: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Detected language: shan_combined_profile.json

All processing completed.

real    0m4.951s
user    0m4.257s
sys     0m0.699s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_freq$
```

What I learned:  char_syl frequency dictionary based နဲ့လည်း မြန်မြန်ဆန်ဆန် language detection လုပ်လို့ ရတယ်။ ရလဒ်လည်း အကြမ်းဖျဉ်းအားဖြင့် ကြည့်ကြည့်ရင် Neural Network, FastText approach တွေနဲ့ comparable လုပ်လို့ ရတယ်လို့ နားလည်တယ်။ သို့သော် formal comparison တော့ လုပ်ရဦးမယ်။ အဲဒါပြီးမှ အတိအကျ သိရမယ်။ လက်ရှိ char_syl freq dictionary based approach မှာက ကောင်းကောင်း language detection မလုပ်ပေးနိုင်တာက dialect language pair တွေဖြစ်တဲ့ ဗမာ၊ ဘိတ်၊ ထားဝယ်၊ ရခိုင် ဒီ ဘာသာစကားလေးမျိုးအကြားပဲ။ တခုကောင်းတာက မွန်နဲ့ ရှမ်းကို ရောတာမျိုး မဖြစ်တာကတော့ ကောင်းတယ်။   

## Rethinking

လက်ရှိအချိန်ထိ စမ်းခဲ့တဲ့ approach တွေက အောက်ပါအတိုင်း ...  

1. Naive Based Language Detection with Syllable Ngram
2. Character Frequency Dictionary
3. Syllable Frequency Dictionary
4. Character+Syllable Frequency Dictionary
5. Embedding (both Word2Vec and FastText) and Cosine Similarity
6. FastText Lib based Classification
7. Neural Network based Classification

ထပ် လုပ်လို့ ရနိုင်တာက Language Model ကို KenLM တို့လို strong statistical LM ဆောက်ပြီး PPL, Naive နှစ်မျိုးပေါင်းပြီး classification လုပ်တာမျိုး။    
ပြီးတော့ language model ကိုလည်း character level, syllable level ဆောက်ပြီးမှ အဲဒီ LM နှစ်ခုနဲ့ PPL measure လုပ်ပြီးမှ language detection အတွက် decision လုပ်တာမျိုး။   

## To Do

- Embedding approach မှာလည်း လက်ရှိမှာက ဖိုင်တစ်ဖိုင်လုံး input လုပ်ပြီးပဲ testing or language detection လုပ်ထားတာမို့လို့ အဲဒီ Python code မှာလည်း both file input and string input လက်ခံနိုင်အောင် ပြင်ရန်
- ပြီးရင် Embedding approach နဲ့ experiment ကို string ပါ ထည့်ပြီး ထပ် run ရန်
- Ken LM library နဲ့ char, syl LM နှစ်ခုဆောက်ပြီးတော့ language detection လုပ်ကြည့်ရန်
- တကယ်က Naive Based Language Dection မှာလည်း လက်ရှိက Syllable unit နဲ့ပဲ လုပ်ထားတာမို့လို၊ character Unit ပါ ထပ်ဖြည့်ပြီး run တာမျိုးလည်း လုပ်ကြည်လို့ ရတယ်။

## Updating Embedding Approach  

လက်ရှိ ရလဒ်တွေက အောက်ပါအတိုင်းပဲ။ Word2Vec, FastText with Cosine Similarity နဲ့ language detection ရလဒ်တွေကတော့ မကောင်းဘူး။   

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ ./detect_languages.sh
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: beik.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: dawei.txt - Detected Language with Word2Vec: Detected language: pao_word2vec
File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: pao.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: rakhine.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
File: shan.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
File: beik.txt - Detected Language with FastText: Detected language: mon_fasttext
File: dawei.txt - Detected Language with FastText: Detected language: mon_fasttext
File: mon_tst.txt - Detected Language with FastText: Detected language: mon_fasttext
File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: rakhine.txt - Detected Language with FastText: Detected language: mon_fasttext
File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
File: shan.txt - Detected Language with FastText: Detected language: mon_fasttext
Language detection completed for all files.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

လောလောဆယ် input မှာ string ကိုလည်း လက်ခံနိုင်အောင် ပြင်ခဲ့တယ်။  

```python

elif args.mode == 'detect':
    if not args.input or not args.model_folder:
        print("For detection, both --input and --model_folder arguments are required.")
    else:
        models = {fname.split('.')[0]: load_model(os.path.join(args.model_folder, fname))
                  for fname in os.listdir(args.model_folder) if fname.endswith('.model')}

        # Check if the input is a file path or a string
        if os.path.isfile(args.input):
            with open(args.input, 'r', encoding='utf-8') as file:
                text = file.read()
        else:
            text = args.input

        detected_language = detect_language(text, models)
        print(f"Detected language: {detected_language}")

```

language detection လုပ်တဲ့အခါမှာ random string နဲ့လည်း test လုပ်ဖို့ ပြီးတော့ random ကို 10 time လုပ်ဖို့အတွက် bash shell script ကို အောက်ပါအတိုင်းပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define base directory, Python script, and input directory
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/embedding"
PYTHON_SCRIPT="$BASE_DIR/embed_lang_detect.py"  # Replace with the name of your Python script
INPUT_DIR="$BASE_DIR/eg_input"
WORD2VEC_DIR="$BASE_DIR/word2vec"
FASTTEXT_DIR="$BASE_DIR/fasttext"

# Function to run language detection
run_detection() {
    model_type=$1
    model_dir=$2
    echo "Running language detection using $model_type models..."
    for file in "$INPUT_DIR"/*; do
        filename=$(basename -- "$file")
        detected_language=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$file" --model_folder "$model_dir")
        echo "File: $filename - Detected Language with $model_type: $detected_language"

        # Run detection on random sentences from the file, 10 times
        for i in {1..10}; do
            random_sentence=$(shuf -n 1 "$file")
            echo "Attempt $i - Random sentence from $filename: $random_sentence"
            detected_language_sentence=$(python3 "$PYTHON_SCRIPT" --mode detect --input "$random_sentence" --model_folder "$model_dir")
            echo "Detected Language with $model_type: $detected_language_sentence"
        done
        echo ""
    done
}

# Run detection using Word2Vec models
run_detection "Word2Vec" "$WORD2VEC_DIR"

# Run detection using FastText models
run_detection "FastText" "$FASTTEXT_DIR"

echo "Language detection completed for all files."

```

Language Detection with Embedding (word2vec, fasttext and Cosine) approach Experiment-1:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./detect_languages_exp.sh | tee lang_detection_exp1.log
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: beik.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 8 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 10 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with Word2Vec: Detected language: beik_word2vec

File: dawei.txt - Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 1 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from dawei.txt: အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 9 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 2 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 3 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 8 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 10 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from mon.txt: လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: pao.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 1 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from pao.txt: ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 4 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 2 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 3 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 5 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 6 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: rakhine.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from rakhine.txt: ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from rakhine.txt: ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from rakhine.txt: ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from rakhine.txt: ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from sgaw_kayin.txt: ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from sgaw_kayin.txt: ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 4 - Random sentence from sgaw_kayin.txt: ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 6 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 10 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with Word2Vec: Detected language: pao_word2vec

File: shan.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 7 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from shan.txt: ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Detected Language with FastText: Detected language: pao_fasttext
Attempt 3 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with FastText: Detected language: pao_fasttext
Attempt 5 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with FastText: Detected language: pao_fasttext
Attempt 6 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Detected Language with FastText: Detected language: pao_fasttext
Attempt 10 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with FastText: Detected language: mon_fasttext

File: beik.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext

File: dawei.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext

File: mon_tst.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext

File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
Attempt 1 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon.txt: ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon.txt: ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Detected Language with FastText: Detected language: mon_fasttext

File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext
Attempt 3 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext
Attempt 8 - Random sentence from pao.txt: က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext

File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from po_kayin.txt: ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from po_kayin.txt: ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from po_kayin.txt: ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from po_kayin.txt: ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Detected Language with FastText: Detected language: mon_fasttext

File: rakhine.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 2 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from rakhine.txt: မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with FastText: Detected language: pao_fasttext

File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from sgaw_kayin.txt: ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from sgaw_kayin.txt: လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from sgaw_kayin.txt: ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext

File: shan.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 4 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 5 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 6 - Random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 7 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 8 - Random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 9 - Random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 10 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext

Language detection completed for all files.

real    4m30.923s
user    4m39.432s
sys     12m42.365s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

Experiment-2 Result with Embedding Approach (word2vec, fasttext, and cosine similarity measurement):  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./detect_languages_exp.sh | tee lang_detection_exp2.log
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 9 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

File: beik.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 5 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 9 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Detected Language with Word2Vec: Detected language: beik_word2vec

File: dawei.txt - Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 1 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from dawei.txt: အဲ ဝယ် ဟှား ဟှို လက် ထပ် လိုက် ဇာ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 7 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 9 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from dawei.txt: ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 6 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 8 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 10 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: pao.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 1 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 7 - Random sentence from pao.txt: က ထိန်ꩻ‌ နွောင်ꩻ ဝွေꩻ နဝ်ꩻ အဝ်ႏ ဒျာႏ နာꩻ လွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 8 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from pao.txt: ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec

File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 2 - Random sentence from po_kayin.txt: ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from po_kayin.txt: ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from po_kayin.txt: ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 10 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec

File: rakhine.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 9 - Random sentence from rakhine.txt: မင်း တောင် တိ ကို တက် နီ ကျ လား ။
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 10 - Random sentence from rakhine.txt: ဆူ ပြီး ရီ ကို သောက် သင့် ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 2 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 3 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 5 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 6 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from sgaw_kayin.txt: ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 10 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
Detected Language with Word2Vec: Detected language: pao_word2vec

File: shan.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 9 - Random sentence from shan.txt: ႁဝ်း မိူဝ်ႈၽုၵ်ႈ  ၵၢင်ၼႂ် တေဢွၵ်ႇ ပႆ တၢင်း  ဢိူဝ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from bamar_burmese.txt: ပါ ပါ သ မီး ကို လွမ်း နေ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သွား ပါ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with FastText: Detected language: mon_fasttext

File: beik.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Detected Language with FastText: Detected language: mon_fasttext

File: dawei.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext

File: mon_tst.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext

File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
Attempt 1 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon.txt: ပေါဲ ဂီ တ ဂှ် ဂိ တု ဂ တ မှ ကၠောန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with FastText: Detected language: mon_fasttext

File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext
Attempt 4 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext
Attempt 7 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with FastText: Detected language: mon_fasttext

File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from po_kayin.txt: ဆီၫ့ မီၪ့ ဆၧ ကဲၪ ခိၬ ယ ဆီၫ့ မီၪ့ ဘီၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from po_kayin.txt: ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext

File: rakhine.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from rakhine.txt: ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 8 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext

File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from sgaw_kayin.txt: ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from sgaw_kayin.txt: ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext

File: shan.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 3 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 6 - Random sentence from shan.txt: ဢမ်ႇ မူတ်း သႂ်  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 7 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 8 - Random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Detected Language with FastText: Detected language: po_kayin_fasttext
Attempt 9 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with FastText: Detected language: mon_fasttext

Language detection completed for all files.

real    4m27.828s
user    4m36.366s
sys     12m38.217s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

Experiment-3 Result for Embedding (Word2Vec, FastText, Cosine) Approach:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$ time ./detect_languages_exp.sh | tee lang_detection_exp3.log
Running language detection using Word2Vec models...
File: bamar_burmese.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from bamar_burmese.txt: မင်္ဂ လာ ပါ ဆ ရာ မ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 5 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from bamar_burmese.txt: က လေး က အိမ် မှာ ပါ
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: beik.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from beik.txt: အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from beik.txt: အဲ့ အ မ ကို လက် ထပ် လိုက် ရယ် လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from beik.txt: မင်း ငါ့ ကို ရှင်း ပြ နိုင် မ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from beik.txt: နင် ခ ရီး မ ထွက် ခဲ့ ရ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: dawei.txt - Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 1 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 3 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 4 - Random sentence from dawei.txt: သူး နို့ ဟှယ် လော့ သတ္တိ ရှိ ဟှယ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 6 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 8 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from dawei.txt: ဟှယ် လော့ စိ လှုပ် ရှား ဟှယ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from dawei.txt: အဲ ဟှို သွား ဟှို့ နန့် ဟှို ငါ တိုက် တွန်း ဟှ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: mon_tst.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 3 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 8 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 9 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec
Attempt 10 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: dawei_word2vec

File: mon.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from mon.txt: လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from mon.txt: ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from mon.txt: လၟုဟ် အဲ  ဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from mon.txt: အဲ ဟ ယျ ဗှ်ေ တိၚ် ဂီ တာ လေပ် မံၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from mon.txt: ဗှ်ေ ဟ ယျ တုဲ မာန် ဟာ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

File: pao.txt - Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 1 - Random sentence from pao.txt: ခွေ စ ဥ်ꩻ စာꩻ အ တွိုင်ꩻ စ ဥ်ꩻ စာꩻ ဟုဲင်း
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 3 - Random sentence from pao.txt: ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 4 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from pao.txt: ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 6 - Random sentence from pao.txt: ဆုဲင်ꩻ သွတ် တ လဲင်ႏ ရက် ဒျာႏ ဝွေꩻ နဝ်ꩻ တဲ့ ဒေါ့ꩻ ခွင်ꩻ တ လ တဝ်း ဒွုမ်
Detected Language with Word2Vec: Detected language: beik_word2vec
Attempt 7 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from pao.txt: ဒေါ့ꩻ ဝင်ꩻ မဉ်ꩻ နဝ်ꩻ လွ ထီႏ ငါႏ
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: po_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from po_kayin.txt: ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from po_kayin.txt: ယ မ့ၬ လဲၩ ချဲၩ့ၦ ဂူၫ ဂၩ အ လၩ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from po_kayin.txt: အ ဝ့ၫ ထီး န့ၦၡၩ ဘၪ နး ဂၩ လၧၩ့ အ့ၬ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 5 - Random sentence from po_kayin.txt: ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 6 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 7 - Random sentence from po_kayin.txt: ယ ဂဲၫ ထဲၩ့ လီၩ ပျၩ့ ထၬ ကဲၪ ခိၬ န လီၩ ထၬ ဆ့ လီၫ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 8 - Random sentence from po_kayin.txt: နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from po_kayin.txt: ၦ လၧ ဖီၪ့ ဂုး ထၬ အ ဝ့ၫ က န့ နီၪ မွဲ ဒၪ နၧၩ လီၫ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with Word2Vec: Detected language: pao_word2vec

File: rakhine.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from rakhine.txt: ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 5 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 6 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from rakhine.txt: သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 8 - Random sentence from rakhine.txt: ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 9 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: sgaw_kayin.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 2 - Random sentence from sgaw_kayin.txt: က ကွၢ် ထွဲ အီၤ အ ဂီၢ် က နၢၤ ဒၣ် နၤ လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 3 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 4 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 5 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 6 - Random sentence from sgaw_kayin.txt: ဒ် န တဲ တ့ၢ် အ သိး ယ တဲ နၢ် ပၢၢ် တ့ၢ် လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 7 - Random sentence from sgaw_kayin.txt: ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 8 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with Word2Vec: Detected language: pao_word2vec
Attempt 9 - Random sentence from sgaw_kayin.txt: ဒ် ယ ဆိ က မိၣ် အ သိး ဆိ က မိၣ် တ က့ၢ် .
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 10 - Random sentence from sgaw_kayin.txt: ဘၣ် တဲ ပှၤ အ ဂ့ၢ် န့ၣ် သး ဟ့ လီၤ .
Detected Language with Word2Vec: Detected language: rakhine_word2vec

File: shan.txt - Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 1 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 2 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 3 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with Word2Vec: Detected language: rakhine_word2vec
Attempt 4 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 5 - Random sentence from shan.txt: ဢမ်ႇ မီး  ၶပ်း မၢႆ တႃႇဢွၵ်ႇ ပၢႆႈ  ႁႃႉ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 6 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 7 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 8 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 9 - Random sentence from shan.txt: ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec
Attempt 10 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with Word2Vec: Detected language: po_kayin_word2vec

Running language detection using FastText models...
File: bamar_burmese.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from bamar_burmese.txt: ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from bamar_burmese.txt: နေ ကောင်း လား
Detected Language with FastText: Detected language: pao_fasttext
Attempt 5 - Random sentence from bamar_burmese.txt: ပုပ္ပါး တောင် ကို ထပ် တက် ချင် သေး တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from bamar_burmese.txt: ကျောင်း သား ကျောင်း သူ ကျောင်း မှာ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from bamar_burmese.txt: တက္က သိုလ် အ သွား အ ပြန် ကို သင်္ဘော စီး ပြီး သွား ရ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from bamar_burmese.txt: ပြော ပြ ပါ ဦး ဘာ တွေ ဖြစ် နေ တာ လဲ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from bamar_burmese.txt: ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from bamar_burmese.txt: ကျန်း မာ တယ် ဒါ ပေ မဲ့ အ လုပ် များ တယ်
Detected Language with FastText: Detected language: mon_fasttext

File: beik.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from beik.txt: ဖယ် သူ လေ ကို မေး ရိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from beik.txt: သူ တို့ ဘ ဇာ လောက် သတ္တိ ရှိ လဲ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from beik.txt: သူ ဒယ့် ဟာ ကို လို ချင် မ ဟုတ် ဝ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from beik.txt: ဘ ဇာ လောက် စိတ် လှုပ် ရှား ရိ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from beik.txt: အဲ ဒီ ကို သော ဖို့ ငါ မင်း ကို ငါ မ တိုက် တွန်း ရ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from beik.txt: ဒါ ထဲ မှာ အ ဝေး ပြော ဖုန်း ပြော တ အား များ ရယ် ။
Detected Language with FastText: Detected language: mon_fasttext

File: dawei.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 2 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from dawei.txt: နန် ငါ့ ဟှို ရှင်း ပြ ပါ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from dawei.txt: အဲ မို ထဲ မှာ ဝေး ကို ဖုန်း ပြော ဇာ ရ တိုင်း များ ဟှယ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from dawei.txt: အယ် ထဲ မှာ ဝီး ပြော ဖောင်း ပြော ဇာ ရ ရာ များ ဟှယ် ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 7 - Random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from dawei.txt: ခံ ဗျား ခ ရီး ထွပ် ဟှ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from dawei.txt: အယ် ဝယ် ဟှား အဲ့ မာ ဂို လို ရှင် ဟှယ် မှု ဝ လား ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from dawei.txt: ဟှယ် လူ လေ ဟှို မေး ကေ့ နူး ။
Detected Language with FastText: Detected language: mon_fasttext

File: mon_tst.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon_tst.txt: လၟုဟ် အဲဗ္တောန် တိၚ် မံၚ် ဂီ တာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon_tst.txt: က သပ်ပ္ဍဲ ဗှ်ေ ဂှ်
Detected Language with FastText: Detected language: mon_fasttext

File: mon.txt - Detected Language with FastText: Detected language: beik_fasttext
Attempt 1 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from mon.txt: ပ္ဍဲ ဗှ်ေ ဂှ် က သပ် တၟေၚ်ၚ် နွံ မံၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from mon.txt: သွက် အဲ ဂွံ အံၚ် ဇၞး ရာ ဒ နာ ကဵု ညိ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from mon.txt: ယဝ် ဗှ်ေ ဟွံ ပ ယှုက် အဲ ရ တှ်ေ တုဲ မာန် ဏောၚ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from mon.txt: ဂ လာန် ဗှ်ေ ပ တိုန် လဝ် နူ ဏေအ်ဗ္တံ ဂှ် ခိုဟ် ကွေံ ကွေံ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from mon.txt: ခိုဟ် ယျ ဆက် ဂ စာန် ညိ ပၠန် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from mon.txt: ၜိုတ် အဲ ကၠောန် မာန် အဲ ဂ စာန် လဝ် ရ ။
Detected Language with FastText: Detected language: mon_fasttext

File: pao.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နာꩻ တ အွဉ်ႏ ဖွို့ꩻ တဝ်း ဟောင်း တွမ်ႏ အ လင် တ ဗာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from pao.txt: ‌ နာꩻ က ဒေါ့ꩻ အ တွိုင်ꩻ ခွေ သျင်ꩻ ပျ ဗာႏ ဒျာႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ နီ အ တာႏ ယပ် ခုဲင်ႏ ငါႏ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with FastText: Detected language: pao_fasttext
Attempt 6 - Random sentence from pao.txt: တယ်ႏ နာ ဆာ ဒုံး ပျံ ထင်ႏ စ ခိန်ႏ နဝ်ꩻ ဝွေꩻ တဲမ်း ဗာႏ ဒျာႏ မတ် တန်ꩻ
Detected Language with FastText: Detected language: beik_fasttext
Attempt 7 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with FastText: Detected language: pao_fasttext
Attempt 9 - Random sentence from pao.txt: နဝ်ꩻ နဝ်ꩻ ခွေ ယမ်း မာႏ ဗာႏ ဟောင်း
Detected Language with FastText: Detected language: pao_fasttext
Attempt 10 - Random sentence from pao.txt: ဝွေꩻ မူႏ တ တောင် ချာ တဝ်း ဒွုမ် ပါꩻ မုဲင်ꩻ မုဲင်ꩻ
Detected Language with FastText: Detected language: mon_fasttext

File: po_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from po_kayin.txt: ယ အဲၪ အ ဝ့ၫ နီၪ လ ခဲၫ့ ထုၬ က ဘျၩ့ မၬ ယ လီၩ ဘၪၥ့ၪ လၧၩ့ ထၧၩ့ ယၫ အ့ၬ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ မွဲ ဆၧ အ ကၪ လၧ ပ ဂး လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from po_kayin.txt: ဆၧ အ နီၪ န ထိၬ ဘုၬ ထဲၩ့ လၧ ဆၧ အ ဂူၫ ဂၩ က မံၩ့ အ့ၬ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from po_kayin.txt: နၫ ဆၫ အ ဆၧ ယူၩ ဖျိၬ ထၪ့ ကၠၧၫ့ , အ ဝ့ၫ ကွ့ၭ နဲၫ့ ဆၧ ကၠၧၫ့ လ့ၬ လီၫ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from po_kayin.txt: ယ ယဲး ထဲး ဘၪ ဆၧ အ နီၪ ဧၪ .
Detected Language with FastText: Detected language: mon_fasttext

File: rakhine.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from rakhine.txt: မင်း မိန်း စ ရာ မ လို ပါ ။
Detected Language with FastText: Detected language: pao_fasttext
Attempt 3 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from rakhine.txt: ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from rakhine.txt: မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from rakhine.txt: ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from rakhine.txt: ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from rakhine.txt: ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from rakhine.txt: ငါ အ လုပ် မ ပြီး သိ ပါ ။
Detected Language with FastText: Detected language: mon_fasttext

File: sgaw_kayin.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် လၢ ပ ဂီၢ် ကီ ခဲ ဝဲ ဒၣ် လီၤ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န တ ဘျး စဲ ဒီး အ ဂၤ တ ခါ ဧဲၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 5 - Random sentence from sgaw_kayin.txt: ပျဲ တၢ် မၤ စၢၤ တ က့ၢ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 6 - Random sentence from sgaw_kayin.txt: ပိာ် မုၣ် န့ၣ် တ တိၢ် နီၣ် ပှၤ နီ တ ဂၤ လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from sgaw_kayin.txt: တၢ် ဝဲ န့ၣ် န့ၣ် မ့ၢ် ယ ထီၣ် ယီၢ် ဘၣ် ဧါ .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from sgaw_kayin.txt: လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext
Attempt 10 - Random sentence from sgaw_kayin.txt: လၢ ခံ က တၢၢ် တ ဘျီ က တဲ အီၤ လၢ ယ အဲၣ် အီၤ န့ၣ် အ ခွဲး တ န့ၢ် လၢၤ ဘၣ် .
Detected Language with FastText: Detected language: mon_fasttext

File: shan.txt - Detected Language with FastText: Detected language: mon_fasttext
Attempt 1 - Random sentence from shan.txt: ဢ ရ သႃႇ မၼ်း တႄႉ မိူၼ်ၼမ်ႉ လၢင်ႉ ဝၢၼ်ႇ ဝႆႉ ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 2 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 3 - Random sentence from shan.txt: တွင်း ပၢၼ်ႇၵဝ်  ဢမ်ႇ တွင်း ပၢၼ်ႇ  ၵဝ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 4 - Random sentence from shan.txt: မႂ်း လွင်ႈၼႆႉ လၢတ်ႈ မႃး  ႁိုဝ်  ဢမ်ႇ လၢတ်ႈ မႃး  ႁႃႉ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 5 - Random sentence from shan.txt: တႃႇ မၼ်းၼၢင်း  ႁဝ်း တေ ထၢမ်  ဢမ်ႇ  ၸႂ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 6 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 7 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 8 - Random sentence from shan.txt: တႃႇ လုၵ်ႈႁဵၼ်းၶဝ် တေ လႆႈ  ဢဝ် ပပ်ႉ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext
Attempt 9 - Random sentence from shan.txt: ဢၼ်ၼႆႉ တႃႇ မၼ်း ယၢပ်ႇ  ဢိူဝ်ႈ ။
Detected Language with FastText: Detected language: rakhine_fasttext
Attempt 10 - Random sentence from shan.txt: မိူဝ်ႈ ပူၼ်ႉ မႃး ဝၼ်း သုၵ်း  ၵၢင်ၼႂ်  ႑႑ မွင်း  ၼၼ်ႉ သူ မီး ယူႇ တီႈ လႂ် ။
Detected Language with FastText: Detected language: mon_fasttext

Language detection completed for all files.

real    4m27.666s
user    4m38.407s
sys     12m37.057s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/embedding$
```

compare လုပ်လို့ရအောင် string input ကိုလည်း ဖြည့်ထားလိုက်ပြီ။ ဒါပေမဲ့ အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ word2vec, fasttext with cosine similarity က ရလဒ် မကောင်းဘူး။  
အထက်ပါ To Do မှာ ကျန်တာက ken-lm နဲ့ စမ်းကြည့်ဖို့ ကိစ္စ ...  

- Ken LM library နဲ့ char, syl LM နှစ်ခုဆောက်ပြီးတော့ language detection လုပ်ကြည့်ရန်

## char+syl LM Approach  

python code အရင် ရေးခဲ့တယ်။ ပြီးတော့ အဲဒီ python code နဲ့ run ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define base directory and script paths
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/char_syl_LM"
PYTHON_SCRIPT="$BASE_DIR/char_syl_lm_lang_detect.py"
RAW_DIR="$BASE_DIR/raw"
LM_DIR="$BASE_DIR/lm"

# Loop through each raw file
for raw_file in "$RAW_DIR"/*; do
    # Extract the language name (first part of the filename)
    lang_name=$(basename -- "$raw_file" | cut -d '.' -f 1)

    # Train models for character level and syllable level for 3, 4, and 5-grams
    for level in char syl; do
        for n in 3 4 5; do
            output_file="$LM_DIR/${lang_name}.${level}.${n}gram.lm.pkl"
            echo "Training $level level $n-gram model for $lang_name language."
            python "$PYTHON_SCRIPT" --mode train --level "$level" --n "$n" --input "$raw_file" --output "$output_file"
            echo "Language model saved to $output_file"
        done
    done
done

echo "Language model training completed."

```

Run shell script as follows:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ time ./build_lm.sh
Training char level 3-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.3gram.lm.pkl
Training char level 4-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.4gram.lm.pkl
Training char level 5-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.char.5gram.lm.pkl
Training syl level 3-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.3gram.lm.pkl
Training syl level 4-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.4gram.lm.pkl
Training syl level 5-gram model for bamar language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/bamar.syl.5gram.lm.pkl
Training char level 3-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.3gram.lm.pkl
Training char level 4-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.4gram.lm.pkl
Training char level 5-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.char.5gram.lm.pkl
Training syl level 3-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.3gram.lm.pkl
Training syl level 4-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.4gram.lm.pkl
Training syl level 5-gram model for beik language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/beik.syl.5gram.lm.pkl
Training char level 3-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.3gram.lm.pkl
Training char level 4-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.4gram.lm.pkl
Training char level 5-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.char.5gram.lm.pkl
Training syl level 3-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.3gram.lm.pkl
Training syl level 4-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.4gram.lm.pkl
Training syl level 5-gram model for dawei language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/dawei.syl.5gram.lm.pkl
Training char level 3-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.3gram.lm.pkl
Training char level 4-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.4gram.lm.pkl
Training char level 5-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.char.5gram.lm.pkl
Training syl level 3-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.3gram.lm.pkl
Training syl level 4-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.4gram.lm.pkl
Training syl level 5-gram model for mon language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/mon.syl.5gram.lm.pkl
Training char level 3-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.3gram.lm.pkl
Training char level 4-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.4gram.lm.pkl
Training char level 5-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.char.5gram.lm.pkl
Training syl level 3-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.3gram.lm.pkl
Training syl level 4-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.4gram.lm.pkl
Training syl level 5-gram model for pao language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/pao.syl.5gram.lm.pkl
Training char level 3-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.3gram.lm.pkl
Training char level 4-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.4gram.lm.pkl
Training char level 5-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.char.5gram.lm.pkl
Training syl level 3-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.3gram.lm.pkl
Training syl level 4-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.4gram.lm.pkl
Training syl level 5-gram model for po_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/po_kayin.syl.5gram.lm.pkl
Training char level 3-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.3gram.lm.pkl
Training char level 4-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.4gram.lm.pkl
Training char level 5-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.char.5gram.lm.pkl
Training syl level 3-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.3gram.lm.pkl
Training syl level 4-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.4gram.lm.pkl
Training syl level 5-gram model for rakhine language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/rakhine.syl.5gram.lm.pkl
Training char level 3-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.3gram.lm.pkl
Training char level 4-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.4gram.lm.pkl
Training char level 5-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.char.5gram.lm.pkl
Training syl level 3-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.3gram.lm.pkl
Training syl level 4-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.4gram.lm.pkl
Training syl level 5-gram model for sgaw_kayin language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/sgaw_kayin.syl.5gram.lm.pkl
Training char level 3-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.3gram.lm.pkl
Training char level 4-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.4gram.lm.pkl
Training char level 5-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.char.5gram.lm.pkl
Training syl level 3-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.3gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.3gram.lm.pkl
Training syl level 4-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.4gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.4gram.lm.pkl
Training syl level 5-gram model for shan language.
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.5gram.lm.pkl
Language model saved to /home/ye/exp/sylbreak4all/lang_detection/char_syl_LM/lm/shan.syl.5gram.lm.pkl
Language model training completed.

real    5m57.618s
user    6m47.999s
sys     2m56.116s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

After running above shell script, I got char, syl LMs as follows:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ ls ./lm/*char*pkl
./lm/bamar.char.3gram.lm.pkl  ./lm/pao.char.5gram.lm.pkl
./lm/bamar.char.4gram.lm.pkl  ./lm/po_kayin.char.3gram.lm.pkl
./lm/bamar.char.5gram.lm.pkl  ./lm/po_kayin.char.4gram.lm.pkl
./lm/beik.char.3gram.lm.pkl   ./lm/po_kayin.char.5gram.lm.pkl
./lm/beik.char.4gram.lm.pkl   ./lm/rakhine.char.3gram.lm.pkl
./lm/beik.char.5gram.lm.pkl   ./lm/rakhine.char.4gram.lm.pkl
./lm/dawei.char.3gram.lm.pkl  ./lm/rakhine.char.5gram.lm.pkl
./lm/dawei.char.4gram.lm.pkl  ./lm/sgaw_kayin.char.3gram.lm.pkl
./lm/dawei.char.5gram.lm.pkl  ./lm/sgaw_kayin.char.4gram.lm.pkl
./lm/mon.char.3gram.lm.pkl    ./lm/sgaw_kayin.char.5gram.lm.pkl
./lm/mon.char.4gram.lm.pkl    ./lm/shan.char.3gram.lm.pkl
./lm/mon.char.5gram.lm.pkl    ./lm/shan.char.4gram.lm.pkl
./lm/pao.char.3gram.lm.pkl    ./lm/shan.char.5gram.lm.pkl
./lm/pao.char.4gram.lm.pkl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ ls ./lm/*syl*pkl
./lm/bamar.syl.3gram.lm.pkl  ./lm/pao.syl.5gram.lm.pkl
./lm/bamar.syl.4gram.lm.pkl  ./lm/po_kayin.syl.3gram.lm.pkl
./lm/bamar.syl.5gram.lm.pkl  ./lm/po_kayin.syl.4gram.lm.pkl
./lm/beik.syl.3gram.lm.pkl   ./lm/po_kayin.syl.5gram.lm.pkl
./lm/beik.syl.4gram.lm.pkl   ./lm/rakhine.syl.3gram.lm.pkl
./lm/beik.syl.5gram.lm.pkl   ./lm/rakhine.syl.4gram.lm.pkl
./lm/dawei.syl.3gram.lm.pkl  ./lm/rakhine.syl.5gram.lm.pkl
./lm/dawei.syl.4gram.lm.pkl  ./lm/sgaw_kayin.syl.3gram.lm.pkl
./lm/dawei.syl.5gram.lm.pkl  ./lm/sgaw_kayin.syl.4gram.lm.pkl
./lm/mon.syl.3gram.lm.pkl    ./lm/sgaw_kayin.syl.5gram.lm.pkl
./lm/mon.syl.4gram.lm.pkl    ./lm/shan.syl.3gram.lm.pkl
./lm/mon.syl.5gram.lm.pkl    ./lm/shan.syl.4gram.lm.pkl
./lm/pao.syl.3gram.lm.pkl    ./lm/shan.syl.5gram.lm.pkl
./lm/pao.syl.4gram.lm.pkl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

filesize info for character LMs:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ ls ./lm/*char*pkl -lh
-rw-rw-r-- 1 ye ye 229K ม.ค.  23 16:47 ./lm/bamar.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.4M ม.ค.  23 16:48 ./lm/bamar.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 5.6M ม.ค.  23 16:48 ./lm/bamar.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 101K ม.ค.  23 16:49 ./lm/beik.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 481K ม.ค.  23 16:49 ./lm/beik.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.5M ม.ค.  23 16:49 ./lm/beik.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 108K ม.ค.  23 16:49 ./lm/dawei.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 518K ม.ค.  23 16:49 ./lm/dawei.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.6M ม.ค.  23 16:49 ./lm/dawei.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 153K ม.ค.  23 16:49 ./lm/mon.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 709K ม.ค.  23 16:49 ./lm/mon.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.2M ม.ค.  23 16:49 ./lm/mon.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 153K ม.ค.  23 16:49 ./lm/pao.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 802K ม.ค.  23 16:49 ./lm/pao.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.8M ม.ค.  23 16:50 ./lm/pao.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 137K ม.ค.  23 16:50 ./lm/po_kayin.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 784K ม.ค.  23 16:50 ./lm/po_kayin.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.9M ม.ค.  23 16:50 ./lm/po_kayin.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 152K ม.ค.  23 16:50 ./lm/rakhine.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 809K ม.ค.  23 16:51 ./lm/rakhine.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.8M ม.ค.  23 16:51 ./lm/rakhine.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 165K ม.ค.  23 16:51 ./lm/sgaw_kayin.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.1M ม.ค.  23 16:52 ./lm/sgaw_kayin.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 4.2M ม.ค.  23 16:52 ./lm/sgaw_kayin.char.5gram.lm.pkl
-rw-rw-r-- 1 ye ye  99K ม.ค.  23 16:53 ./lm/shan.char.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 490K ม.ค.  23 16:53 ./lm/shan.char.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.8M ม.ค.  23 16:53 ./lm/shan.char.5gram.lm.pkl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

filesize information for syllable LMs:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ ls ./lm/*syl*pkl -lh
-rw-rw-r-- 1 ye ye 6.9M ม.ค.  23 16:48 ./lm/bamar.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye  20M ม.ค.  23 16:48 ./lm/bamar.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  39M ม.ค.  23 16:49 ./lm/bamar.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 961K ม.ค.  23 16:49 ./lm/beik.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.2M ม.ค.  23 16:49 ./lm/beik.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 3.9M ม.ค.  23 16:49 ./lm/beik.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.2M ม.ค.  23 16:49 ./lm/dawei.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.5M ม.ค.  23 16:49 ./lm/dawei.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 4.4M ม.ค.  23 16:49 ./lm/dawei.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 1.8M ม.ค.  23 16:49 ./lm/mon.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 4.0M ม.ค.  23 16:49 ./lm/mon.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye 7.1M ม.ค.  23 16:49 ./lm/mon.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 3.0M ม.ค.  23 16:50 ./lm/pao.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 7.1M ม.ค.  23 16:50 ./lm/pao.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  13M ม.ค.  23 16:50 ./lm/pao.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.3M ม.ค.  23 16:50 ./lm/po_kayin.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 5.9M ม.ค.  23 16:50 ./lm/po_kayin.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  12M ม.ค.  23 16:50 ./lm/po_kayin.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 2.3M ม.ค.  23 16:51 ./lm/rakhine.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 5.9M ม.ค.  23 16:51 ./lm/rakhine.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  12M ม.ค.  23 16:51 ./lm/rakhine.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 4.1M ม.ค.  23 16:52 ./lm/sgaw_kayin.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye  13M ม.ค.  23 16:52 ./lm/sgaw_kayin.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  29M ม.ค.  23 16:53 ./lm/sgaw_kayin.syl.5gram.lm.pkl
-rw-rw-r-- 1 ye ye 4.5M ม.ค.  23 16:53 ./lm/shan.syl.3gram.lm.pkl
-rw-rw-r-- 1 ye ye 7.4M ม.ค.  23 16:53 ./lm/shan.syl.4gram.lm.pkl
-rw-rw-r-- 1 ye ye  12M ม.ค.  23 16:53 ./lm/shan.syl.5gram.lm.pkl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

### Confirmation on pkl Files

သိတဲ့အတိုင်းပဲ ထွက်လာတဲ့ pkl ဖိုင်တွေကို မျက်စိနဲ့ confirm လုပ်ဖို့ လိုအပ်တယ်။ အဲဒါကြောင့် pkl lm တွေကို text ဖိုင်အဖြစ် ပြောင်းဖို့ လိုအပ်တယ်။ အဲဒီအတွက် python code ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```python
"""
For converting pkl file to text file.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 23 Jan 2024

Usage:
    python ./pkl2txt_lm.py --input ./lm --output ./txt_lm
"""

import argparse
import os
import pickle
import sys

def load_language_model(model_path):
    with open(model_path, 'rb') as file:
        return pickle.load(file)

def model_to_text(model):
    model_text = ""
    for n in range(1, model.order + 1):
        model_text += f"=== {n}-grams ===\n"
        for ngram in model.counts[n]:
            # Construct the n-gram as a string
            ngram_str = ' '.join(ngram)
            count = model.counts[n][ngram]
            model_text += f"{ngram_str}: {count}\n"
    return model_text

def save_text_model(text_model, output_path):
    with open(output_path, 'w', encoding='utf-8') as file:
        file.write(text_model)

def convert_models(input_dir, output_dir):
    for model_file in os.listdir(input_dir):
        if model_file.endswith('.pkl'):
            model_path = os.path.join(input_dir, model_file)
            model = load_language_model(model_path)
            model_text = model_to_text(model)

            # Creating output filename by replacing .pkl with .txt
            output_filename = model_file.replace('.pkl', '.txt')
            output_path = os.path.join(output_dir, output_filename)
            save_text_model(model_text, output_path)
            print(f"Converted {model_file} to {output_filename}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Convert .pkl language models to text format.')
    parser.add_argument('--input', type=str, required=True, help='Input folder path containing .pkl language models.')
    parser.add_argument('--output', type=str, required=True, help='Output folder path to save text-based language models.')

    args = parser.parse_args()

    if not os.path.exists(args.input):
        print(f"Input directory {args.input} does not exist.")
        sys.exit(1)

    if not os.path.exists(args.output):
        os.makedirs(args.output)

    convert_models(args.input, args.output)

```

Converting ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ time python ./pkl2txt_lm.py --input ./lm --output ./txt_lm
Converted beik.syl.4gram.lm.pkl to beik.syl.4gram.lm.txt
Converted pao.syl.4gram.lm.pkl to pao.syl.4gram.lm.txt
Converted dawei.char.4gram.lm.pkl to dawei.char.4gram.lm.txt
Converted sgaw_kayin.char.4gram.lm.pkl to sgaw_kayin.char.4gram.lm.txt
Converted bamar.syl.4gram.lm.pkl to bamar.syl.4gram.lm.txt
Converted mon.char.3gram.lm.pkl to mon.char.3gram.lm.txt
Converted sgaw_kayin.char.3gram.lm.pkl to sgaw_kayin.char.3gram.lm.txt
Converted beik.char.3gram.lm.pkl to beik.char.3gram.lm.txt
Converted sgaw_kayin.char.5gram.lm.pkl to sgaw_kayin.char.5gram.lm.txt
Converted rakhine.syl.4gram.lm.pkl to rakhine.syl.4gram.lm.txt
Converted pao.syl.5gram.lm.pkl to pao.syl.5gram.lm.txt
Converted po_kayin.char.5gram.lm.pkl to po_kayin.char.5gram.lm.txt
Converted sgaw_kayin.syl.5gram.lm.pkl to sgaw_kayin.syl.5gram.lm.txt
Converted dawei.syl.3gram.lm.pkl to dawei.syl.3gram.lm.txt
Converted mon.syl.5gram.lm.pkl to mon.syl.5gram.lm.txt
Converted beik.char.4gram.lm.pkl to beik.char.4gram.lm.txt
Converted shan.char.5gram.lm.pkl to shan.char.5gram.lm.txt
Converted po_kayin.char.4gram.lm.pkl to po_kayin.char.4gram.lm.txt
Converted beik.syl.5gram.lm.pkl to beik.syl.5gram.lm.txt
Converted mon.syl.3gram.lm.pkl to mon.syl.3gram.lm.txt
Converted po_kayin.char.3gram.lm.pkl to po_kayin.char.3gram.lm.txt
Converted bamar.char.5gram.lm.pkl to bamar.char.5gram.lm.txt
Converted bamar.char.3gram.lm.pkl to bamar.char.3gram.lm.txt
Converted bamar.char.4gram.lm.pkl to bamar.char.4gram.lm.txt
Converted bamar.syl.3gram.lm.pkl to bamar.syl.3gram.lm.txt
Converted rakhine.syl.3gram.lm.pkl to rakhine.syl.3gram.lm.txt
Converted pao.syl.3gram.lm.pkl to pao.syl.3gram.lm.txt
Converted po_kayin.syl.4gram.lm.pkl to po_kayin.syl.4gram.lm.txt
Converted rakhine.char.4gram.lm.pkl to rakhine.char.4gram.lm.txt
Converted po_kayin.syl.5gram.lm.pkl to po_kayin.syl.5gram.lm.txt
Converted dawei.syl.4gram.lm.pkl to dawei.syl.4gram.lm.txt
Converted pao.char.5gram.lm.pkl to pao.char.5gram.lm.txt
Converted beik.char.5gram.lm.pkl to beik.char.5gram.lm.txt
Converted shan.char.4gram.lm.pkl to shan.char.4gram.lm.txt
Converted dawei.char.5gram.lm.pkl to dawei.char.5gram.lm.txt
Converted pao.char.4gram.lm.pkl to pao.char.4gram.lm.txt
Converted shan.syl.4gram.lm.pkl to shan.syl.4gram.lm.txt
Converted shan.syl.5gram.lm.pkl to shan.syl.5gram.lm.txt
Converted rakhine.char.3gram.lm.pkl to rakhine.char.3gram.lm.txt
Converted sgaw_kayin.syl.3gram.lm.pkl to sgaw_kayin.syl.3gram.lm.txt
Converted mon.char.4gram.lm.pkl to mon.char.4gram.lm.txt
Converted bamar.syl.5gram.lm.pkl to bamar.syl.5gram.lm.txt
Converted pao.char.3gram.lm.pkl to pao.char.3gram.lm.txt
Converted mon.char.5gram.lm.pkl to mon.char.5gram.lm.txt
Converted shan.syl.3gram.lm.pkl to shan.syl.3gram.lm.txt
Converted dawei.syl.5gram.lm.pkl to dawei.syl.5gram.lm.txt
Converted rakhine.char.5gram.lm.pkl to rakhine.char.5gram.lm.txt
Converted rakhine.syl.5gram.lm.pkl to rakhine.syl.5gram.lm.txt
Converted shan.char.3gram.lm.pkl to shan.char.3gram.lm.txt
Converted dawei.char.3gram.lm.pkl to dawei.char.3gram.lm.txt
Converted mon.syl.4gram.lm.pkl to mon.syl.4gram.lm.txt
Converted sgaw_kayin.syl.4gram.lm.pkl to sgaw_kayin.syl.4gram.lm.txt
Converted beik.syl.3gram.lm.pkl to beik.syl.3gram.lm.txt
Converted po_kayin.syl.3gram.lm.pkl to po_kayin.syl.3gram.lm.txt

real    0m18.177s
user    0m18.080s
sys     0m3.966s
```

Check the converted text files:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$ ls
bamar.char.3gram.lm.txt  mon.char.3gram.lm.txt       rakhine.char.3gram.lm.txt
bamar.char.4gram.lm.txt  mon.char.4gram.lm.txt       rakhine.char.4gram.lm.txt
bamar.char.5gram.lm.txt  mon.char.5gram.lm.txt       rakhine.char.5gram.lm.txt
bamar.syl.3gram.lm.txt   mon.syl.3gram.lm.txt        rakhine.syl.3gram.lm.txt
bamar.syl.4gram.lm.txt   mon.syl.4gram.lm.txt        rakhine.syl.4gram.lm.txt
bamar.syl.5gram.lm.txt   mon.syl.5gram.lm.txt        rakhine.syl.5gram.lm.txt
beik.char.3gram.lm.txt   pao.char.3gram.lm.txt       sgaw_kayin.char.3gram.lm.txt
beik.char.4gram.lm.txt   pao.char.4gram.lm.txt       sgaw_kayin.char.4gram.lm.txt
beik.char.5gram.lm.txt   pao.char.5gram.lm.txt       sgaw_kayin.char.5gram.lm.txt
beik.syl.3gram.lm.txt    pao.syl.3gram.lm.txt        sgaw_kayin.syl.3gram.lm.txt
beik.syl.4gram.lm.txt    pao.syl.4gram.lm.txt        sgaw_kayin.syl.4gram.lm.txt
beik.syl.5gram.lm.txt    pao.syl.5gram.lm.txt        sgaw_kayin.syl.5gram.lm.txt
dawei.char.3gram.lm.txt  po_kayin.char.3gram.lm.txt  shan.char.3gram.lm.txt
dawei.char.4gram.lm.txt  po_kayin.char.4gram.lm.txt  shan.char.4gram.lm.txt
dawei.char.5gram.lm.txt  po_kayin.char.5gram.lm.txt  shan.char.5gram.lm.txt
dawei.syl.3gram.lm.txt   po_kayin.syl.3gram.lm.txt   shan.syl.3gram.lm.txt
dawei.syl.4gram.lm.txt   po_kayin.syl.4gram.lm.txt   shan.syl.4gram.lm.txt
dawei.syl.5gram.lm.txt   po_kayin.syl.5gram.lm.txt   shan.syl.5gram.lm.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$ head bamar.char.3gram.lm.txt
=== 1-grams ===
်: 227563
< s >: 143652
< / s >: 143652
ာ: 124614
း: 117753
တ: 102502
က: 101986
ေ: 95771
ု: 93325
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$ head bamar.syl.3gram.lm.txt
=== 1-grams ===
< s >: 71826
< / s >: 71826
အ: 28883
တ ယ ်: 17672
ပ ါ: 14580
က ိ ု: 14194
မ: 13426
က: 13016
မ ှ ာ: 9821
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$ head shan.cha
r.3gram.lm.txt
=== 1-grams ===
်: 94222
< s >: 66220
< / s >: 66220
ၼ: 39516
း: 35352
ႈ: 35298
မ: 23417
ဝ: 23035
ႉ: 22497
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM/txt_lm$ head shan.syl.3gram.lm.txt
=== 1-grams ===
< s >: 33110
< / s >: 33110
တ ေ: 2080
ယ ူ ႇ: 1849
လ ႆ ႈ: 1789
ယ ဝ ် ႉ: 1428
သ ူ: 1328
မ ၼ ် း: 1157
သ င ်: 897
```

အထက်ပါ အတိုင်းပဲ syllable language model တွေကိုလည်း character level အတိုင်းပဲ ဆောက်ထားတယ် ဆိုတာကို သွားတွေ့ရတယ်။  

char_syl_lm_lang_detect.py python code မှာလည်း --text_lm option ကို ထည့်ပြီး pkl နဲ့ မသိမ်းပဲ၊ text file LM အဖြစ် သိမ်းအောင် update လုပ်ခဲ့တယ်။  
ပြီးတော့ အဲဒီကနေလည်း syllable LM က ဘယ်လိုဖြစ်နေလဲ၊ syllable segmentation လုပ်တာ လွဲနေသလား ဆိုတာကို လေ့လာကြည့်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level char --n 3 --input ./raw/shan.all.syl.raw --output ./shan.char.3gram.lm.txt --text_lm
Language model saved to ./shan.char.3gram.lm.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level syl --n 3 --input ./raw/shan.all.syl.raw --output ./s
han.syl.3gram.lm.txt --text_lm
Language model saved to ./shan.syl.3gram.lm.txt
```

Check the character level LM:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ head ./shan.char.3gram.lm.txt
 ်: 94222
< s >: 66220
< / s >: 66220
 ၼ: 39516
 း: 35352
 ႈ: 35298
 မ: 23417
 ဝ: 23035
 ႉ: 22497
 ႃ: 21942
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ tail ./shan.char.3gram.lm.txt
တ ယ: <FreqDist with 1 samples and 1 outcomes>
ႂ 8: <FreqDist with 1 samples and 1 outcomes>
ႉ 6: <FreqDist with 1 samples and 1 outcomes>
း ႗: <FreqDist with 1 samples and 1 outcomes>
႗ ဝ: <FreqDist with 1 samples and 1 outcomes>
့ ၵ: <FreqDist with 1 samples and 1 outcomes>
့ ၶ: <FreqDist with 1 samples and 1 outcomes>
4 1: <FreqDist with 1 samples and 1 outcomes>
ႈ ​: <FreqDist with 1 samples and 1 outcomes>
​ ႄ: <FreqDist with 1 samples and 1 outcomes>
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

Check the syllable level LM:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ head ./shan.syl.3gra
m.lm.txt
< s >: 33110
< / s >: 33110
တ ေ: 2080
ယ ူ ႇ: 1849
လ ႆ ႈ: 1789
ယ ဝ ် ႉ: 1428
သ ူ: 1328
မ ၼ ် း: 1157
သ င ်: 897
တ ီ ႈ: 855
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ tail ./shan.syl.3gra
m.lm.txt
ၼမ်ႉ တႃၶႃႈ: <FreqDist with 1 samples and 1 outcomes>
တႃၶႃႈ လႆႈ: <FreqDist with 1 samples and 1 outcomes>
လႆႈ တူၵ်းႁႃႉ: <FreqDist with 1 samples and 1 outcomes>
မိူဝ်ႈၶမ်ႈ ဝႃးၶီႇ: <FreqDist with 1 samples and 1 outcomes>
ဝႃးၶီႇ မေႃႇၼမ်ႉၵမ်းၼိုင်ႈ: <FreqDist with 1 samples and 1 outcomes>
မေႃႇၼမ်ႉၵမ်းၼိုင်ႈ ပဵၼ်ႁိုဝ်: <FreqDist with 1 samples and 1 outcomes>
ပဵၼ်ႁိုဝ် လၢတ်ႈ​ႄၼေႁဝ်း: <FreqDist with 1 samples and 1 outcomes>
လၢတ်ႈ​ႄၼေႁဝ်း တူၺ်း: <FreqDist with 1 samples and 1 outcomes>
<s> သူဢမ်ႇႁဵတ်း: <FreqDist with 1 samples and 1 outcomes>
သူဢမ်ႇႁဵတ်း သင်ႁႃႉ: <FreqDist with 1 samples and 1 outcomes>
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$

```

ဗမာစာဖိုင်နဲ့လည်း confirm လုပ်ခဲ့ ... 

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level char --n 3 --input ./raw/bamar.all.syl.raw --output .
/bamar.char.3gram.lm.txt --text_lm
Language model saved to ./bamar.char.3gram.lm.txt
```

Check char level LM of Bamar language:  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ head ./bamar.char.3gram.lm.txt
 ်: 227563
< s >: 143652
< / s >: 143652
 ာ: 124614
 း: 117753
 တ: 102502
 က: 101986
 ေ: 95771
 ု: 93325
 ိ: 80112
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ tail ./bamar.char.3gram.lm.txt
ဪ ဘ: <FreqDist with 1 samples and 1 outcomes>
ဂ ဃ: <FreqDist with 1 samples and 1 outcomes>
ဃ န: <FreqDist with 1 samples and 1 outcomes>
န ဏ: <FreqDist with 1 samples and 1 outcomes>
ဲ ဪ: <FreqDist with 1 samples and 1 outcomes>
ဟ ံ: <FreqDist with 1 samples and 1 outcomes>
၁ ဥ: <FreqDist with 1 samples and 1 outcomes>
၂ ဥ: <FreqDist with 1 samples and 1 outcomes>
ိ ဩ: <FreqDist with 1 samples and 5 outcomes>
ဖ သ: <FreqDist with 1 samples and 1 outcomes>
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

For the syllable level ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level syl --n 3 --input ./raw/bamar.all.syl.raw --output ./bamar.syl.3gram.lm.txt --text_lm
Traceback (most recent call last):
  File "./char_syl_lm_lang_detect.py", line 150, in <module>
    save_language_model(model, args.output, text_output=args.text_lm)
  File "./char_syl_lm_lang_detect.py", line 59, in save_language_model
    token = ngram[-1]
IndexError: string index out of range
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level syl --n 3 --input ./raw/bamar.all.syl.raw --output ./bamar.syl.3gram.lm.pkl
Language model saved to ./bamar.syl.3gram.lm.pkl
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ .txt format နဲ့ LM ဆောက်တဲ့အခါမှာ error ပေးတယ်။ .pkl အတွက်ကျ error မပေးဘူး။  

ဒီ LM model approach အတွက် တနေကုန် code ထိုင်ရေး debug ရှာလုပ်နေခဲ့ရတယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level syl --n 3 --input ./raw/bamar.all.syl.raw --output ./bamar.syl.3gram.lm.txt --text_lm
...
...
...
Skipping invalid ngram: ('ကျွမ်း', 'ပြီး')
Skipping invalid ngram: ('တော်', 'လိမ္မော်')
Skipping invalid ngram: ('သာ', 'မြည်း')
Skipping invalid ngram: ('ခွဲ', 'သုံး')
Skipping invalid ngram: ('ကျပ်', 'တ')
Skipping invalid ngram: ('ဟာ', 'ဝယ်')
Skipping invalid ngram: ('တော်', 'ဆွယ်')
Skipping invalid ngram: ('ဆို', 'လူ')
Skipping invalid ngram: ('ဟို', 'အင်္ကျီ')
Skipping invalid ngram: ('ဗျား', 'ဟို')
Skipping invalid ngram: ('ထည်', 'စမ်း')
Skipping invalid ngram: ('ဘူး', 'သေး')
Skipping invalid ngram: ('သေး', 'လည်း')
Skipping invalid ngram: ('ဦး', 'နံ')
Skipping invalid ngram: ('က', 'ရွှယ်')
Skipping invalid ngram: ('ရွှယ်', 'ယွမ့်')
Skipping invalid ngram: ('ယွမ့်', 'လမ်း')
Skipping invalid ngram: ('ကျန်း', 'လိ')
Skipping invalid ngram: ('လိ', 'ရင်း')
Skipping invalid ngram: ('ဘူး', 'ဝမ်')
Skipping invalid ngram: ('ဝမ်', 'လန်')
Skipping invalid ngram: ('လန်', 'သိ')
Skipping invalid ngram: ('လန်', 'ကျန်း')
Skipping invalid ngram: ('<s>', 'သုန်')
Skipping invalid ngram: ('သုန်', 'ဆစ့်')
Skipping invalid ngram: ('ဆစ့်', 'လမ်း')
Skipping invalid ngram: ('ကြီး', 'နံ')
Skipping invalid ngram: ('၇', 'ပါ')
Skipping invalid ngram: ('ကျွမ်း', 'ဘူး')
Skipping invalid ngram: ('ဏ', 'စုံ')
Skipping invalid ngram: ('ဘဏ်', 'တစ်')
Skipping invalid ngram: ('လွန်', 'နီး')
Skipping invalid ngram: ('သိုလ်', 'နား')
Skipping invalid ngram: ('ပေါ့', 'တက္က')
Skipping invalid ngram: ('ရံ', 'ထ')
Skipping invalid ngram: ('လည်း', 'နွား')
Skipping invalid ngram: ('ည', 'လည်း')
Skipping invalid ngram: ('ဗျား', 'နွား')
Skipping invalid ngram: ('ချိုး', 'မယ်')
Skipping invalid ngram: ('ချိန်', 'ထ')
Skipping invalid ngram: ('မယ်', 'ထ')
Skipping invalid ngram: ('နင့်', 'အစ်')
Skipping invalid ngram: ('ယာ', 'လား')
Skipping invalid ngram: ('ယား', 'သွား')
Skipping invalid ngram: ('ဗျား', 'ယိုး')
Skipping invalid ngram: ('ယား', 'ရောက်')
Skipping invalid ngram: ('ပန်', 'သွား')
Skipping invalid ngram: ('များ', 'ဂျ')
Skipping invalid ngram: ('ယာန်', 'ခင်')
Skipping invalid ngram: ('ယာန်', 'ပဲ')
Skipping invalid ngram: ('ညီ', 'ရဲ့')
Skipping invalid ngram: ('ဗျား', 'ဗိုက်')
Skipping invalid ngram: ('လည်း', 'မော')
Skipping invalid ngram: ('မော', 'ရေ')
Skipping invalid ngram: ('လည်း', 'ဆာ')
Skipping invalid ngram: ('ဘူး', 'သား')
Skipping invalid ngram: ('ဘူး', 'ချောင်း')
Skipping invalid ngram: ('ခြုံ', 'ဘူး')
Skipping invalid ngram: ('မြန်', 'သင့်')
Skipping invalid ngram: ('မြန်', 'ရင်')
Skipping invalid ngram: ('ဆ', 'တိုက်')
Skipping invalid ngram: ('ဗျား', 'လုံ')
Skipping invalid ngram: ('ခေတ်', 'ကမ္ဘာ')
Skipping invalid ngram: ('ကား', 'ဒု')
Skipping invalid ngram: ('ကား', 'တက်')
Skipping invalid ngram: ('တက်', 'လား')
Skipping invalid ngram: ('ကား', 'ခက်')
Skipping invalid ngram: ('မင်း', 'ဖြည်း')
Skipping invalid ngram: ('သွား', 'ဘယ်')
Skipping invalid ngram: ('တော်', 'ဘောင်း')
Skipping invalid ngram: ('နဲ့', 'အင်္ကျီ')
Skipping invalid ngram: ('ရှည်', 'နှစ်')
Skipping invalid ngram: ('ကုန်', 'စိတ်')
Skipping invalid ngram: ('ရှည်', 'ကြ')
Skipping invalid ngram: ('အင်္ကျီ', 'ပြ')
Skipping invalid ngram: ('ရှစ်', 'ထောင်')
Skipping invalid ngram: ('ထောင်', 'ငါး')
Skipping invalid ngram: ('မျိုး', 'တံ')
Skipping invalid ngram: ('ကြယ်', 'ကိုး')
Skipping invalid ngram: ('ကိုး', 'လုံး')
Skipping invalid ngram: ('လုံး', 'တံ')
Skipping invalid ngram: ('ဆိပ်', 'စိန်')
Skipping invalid ngram: ('စိန်', 'တံ')
Skipping invalid ngram: ('များ', 'စိန်')
Skipping invalid ngram: ('ဇိုင်း', 'ရှိ')
Skipping invalid ngram: ('ဇိုင်း', 'ကြိုက်')
Skipping invalid ngram: ('ဝါ', 'မီး')
Skipping invalid ngram: ('ခိုး', 'ရှိ')
Skipping invalid ngram: ('ခြား', 'ဒီ')
Skipping invalid ngram: ('ရောင်', 'ဘေး')
Skipping invalid ngram: ('ပြာ', 'မိုး')
Skipping invalid ngram: ('ဆိုဒ်', 'လတ်')
Skipping invalid ngram: ('နင်', 'ကြည့်')
Skipping invalid ngram: ('ဘူး', 'ဆိုဒ်')
Skipping invalid ngram: ('သေး', 'ဝတ်')
Skipping invalid ngram: ('ဝတ်', 'လည်း')
Skipping invalid ngram: ('ကို', 'ဆိုဒ်')
Skipping invalid ngram: ('ချ', 'ဝယ်')
Skipping invalid ngram: ('<s>', 'လိ')
Skipping invalid ngram: ('လွန်', 'ချို')
Skipping invalid ngram: ('ရီ', 'စား')
Skipping invalid ngram: ('ရီ', 'ကြိုက်')
Language model saved to ./bamar.syl.3gram.lm.txt
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

```

```

```

```

```

```

```

```

```

