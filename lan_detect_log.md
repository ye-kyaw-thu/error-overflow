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


