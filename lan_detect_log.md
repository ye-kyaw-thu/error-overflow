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

Debugging ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$ python ./char_syl_lm_lang_detect.py --mode train --level syl --n 3 --input ./raw/bamar.all.syl.raw --output ./bamar.syl.3gram.lm.txt --text_lm
...
...
...
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘယ်', 'သွား', 'မ', 'လို့', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'စာ', 'အုပ်', 'သွား', 'ဝယ်', 'မ', 'လို့', 'ခင်', 'ဗျား']
Syllables for sample text: ['ကျွန်', 'တော်', 'ကျောင်း', 'သွား', 'မ', 'လို့']
Syllables for sample text: ['ခင်', 'ဗျား', 'ညီ', 'မ', 'လေး', 'ကို', 'ခင်', 'ဗျား', 'သွား', 'မ']
Syllables for sample text: ['သွား', 'မ', 'ကြို', 'ဘူး', 'သူ့', 'ဘာ', 'သာ', 'သူ', 'ပြန်', 'လာ']
Syllables for sample text: ['မ', 'နက်', 'ဖြန်', 'ခင်', 'ဗျား', 'ကျွန်', 'တော့်', 'အ', 'ဆောင်', 'လာ']
Syllables for sample text: ['မ', 'နက်', 'ဖြန်', 'ကျွန်', 'တော်', 'ဘဏ်', 'သွား', 'မ', 'လို့', 'ကျွန်']
Syllables for sample text: ['မ', 'နက်', 'ဖြန်', 'ကျွန်', 'တော်', 'လည်း', 'ဘဏ်', 'သွား', 'မ', 'လို့']
Syllables for sample text: ['ကောင်း', 'ပါ', 'ပြီ', 'ခင်', 'ဗျား', 'ကျွန်', 'တော့်', 'ကို', 'လာ', 'ခေါ်']
Syllables for sample text: ['ကောင်း', 'ပါ', 'ပြီ', 'မ', 'နက်', 'ဖြန်', 'မ', 'နက်', 'ဆယ်', 'နာ']
Syllables for sample text: ['မင်္ဂ', 'လာ', 'ပါ', 'ခင်', 'ဗျား', 'ကျွန်', 'တော့်', 'ကို', 'စောင့်', 'တာ']
Syllables for sample text: ['မ', 'ကြာ', 'သေး', 'ဘူး', '၁', '၀', 'မိ', 'နစ်', 'ရှိ', 'ပြီ']
Syllables for sample text: ['ဆော', 'ရီး', 'ကျွန်', 'တော်', 'နည်း', 'နည်း', 'နောက်', 'ကျ', 'သွား', 'တယ်']
Syllables for sample text: ['ကျွန်', 'တော်', 'ခင်', 'ဗျား', 'ကို', 'မိတ်', 'ဆက်', 'ပေး', 'မယ်', 'ဒါ']
Syllables for sample text: ['သိ', 'ကျွမ်း', 'ရ', 'တာ', 'ဝမ်း', 'သာ', 'ပါ', 'တယ်', 'ကျွန်', 'တော့်']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', 'ဝမ်း', 'သာ', 'ပါ', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'တို့', 'နှစ်', 'ယောက်', 'သိ', 'ကျွမ်း', 'ပြီး', 'ပြီ', 'လား']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'သိ', 'ပြီး', 'ပြီ']
Syllables for sample text: ['ကြာ', 'ပြီ', 'လား', 'ဘယ်', 'လောက်', 'ကြာ', 'ပြီ', 'လဲ']
Syllables for sample text: ['မ', 'ကြာ', 'သေး', 'ဘူး', '၂', 'လ', '၃', 'လ', 'ရှိ', 'ပြီ']
Syllables for sample text: ['ဟုတ်', 'လား', 'ဘယ်', 'မှာ', 'သိ', 'တာ', 'လဲ']
Syllables for sample text: ['သင်', 'တန်း', 'တစ်', 'ခု', 'မှာ']
Syllables for sample text: ['ခင်', 'ဗျား', 'အ', 'သက်', 'ဘယ်', 'လောက်', 'ရှိ', 'ပြီ', 'လဲ']
Syllables for sample text: ['ခင်', 'ဗျား', 'အ', 'သက်', 'ဘယ်', 'လောက်', 'ရှိ', 'ပြီ', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', '၂', '၈', 'နှစ်', 'ပါ', 'ခင်', 'ဗျား', 'ရော']
Syllables for sample text: ['ကျွန်', 'တော့်', 'အ', 'သက်', 'ပို', 'ကြီး', 'တယ်', 'ကျွန်', 'တော်', 'က']
Syllables for sample text: ['၃', '၀', 'နှစ်', 'ကျွန်', 'တော်', 'က', 'ကျွန်', 'တော်', 'နဲ့', 'အ']
Syllables for sample text: ['ဟုတ်', 'လား']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'ဒါ', 'ဆို', 'ကျွန်', 'တော်', 'ခင်', 'ဗျား', 'ကို', 'အစ်']
Syllables for sample text: ['ကောင်း', 'တာ', 'ပေါ့', 'ရ', 'ပါ', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'ယူ', 'မ', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'ပန်း', 'သီး', 'လို', 'ချင်', 'ပါ', 'တယ်', 'တစ်', 'ကီ']
Syllables for sample text: ['နှစ်', 'ရာ', 'ကျပ်', 'ပါ']
Syllables for sample text: ['ဟို', 'လို', 'မျိုး', 'က', 'ရော']
Syllables for sample text: ['တစ်', 'ရာ', 'သုံး', 'ဆယ်']
Syllables for sample text: ['ဒီ', 'ဟာ', 'ပဲ', 'ယူ', 'မယ်']
Syllables for sample text: ['ဘယ်', 'လောက်', 'ယူ', 'မ', 'လဲ']
Syllables for sample text: ['နှစ်', 'ကီ', 'လို', 'ယူ', 'မယ်']
Syllables for sample text: ['တ', 'ခြား', 'ဟာ', 'ယူ', 'ဦး', 'မ', 'လား']
Syllables for sample text: ['မ', 'ယူ', 'တော့', 'ဘူး']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'ဝယ်', 'မ', 'လို့', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'လိမ္မော်', 'သီး', 'ဝယ်', 'မ', 'လို့', 'တစ်', 'ကီ', 'လို']
Syllables for sample text: ['နှစ်', 'ရာ', 'ကျပ်', 'ပါ']
Syllables for sample text: ['ဈေး', 'ကြီး', 'လိုက်', 'တာ']
Syllables for sample text: ['ဟို', 'လို', 'မျိုး', 'က', 'ဈေး', 'သက်', 'သာ', 'တယ်']
Syllables for sample text: ['ဟို', 'လို', 'မျိုး', 'က', 'ကောင်း', 'လား']
Syllables for sample text: ['ခင်', 'ဗျား', 'အ', 'ရ', 'သာ', 'မြည်း', 'ကြည့်', 'ကြည့်', 'ပါ']
Syllables for sample text: ['ကောင်း', 'တယ်', 'ကျွန်', 'တော်', 'လေး', 'လုံး', 'ယူ', 'မယ်']
Syllables for sample text: ['ဒါ', 'က', 'တစ်', 'ကီ', 'လို', 'ခွဲ', 'သုံး', 'ရာ', 'ကျပ်', 'တ']
Syllables for sample text: ['မ', 'ယူ', 'တော့', 'ဘူး']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'သောက်', 'မှာ', 'လဲ']
Syllables for sample text: ['အ', 'ချို', 'ရည်', 'ရှိ', 'လား']
Syllables for sample text: ['ရှိ', 'တယ်']
Syllables for sample text: ['နှစ်', 'ပု', 'လင်း', 'ယူ', 'မယ်']
Syllables for sample text: ['ရာ', 'သီ', 'ဥ', 'တု', 'က', 'အေး', 'လာ', 'ပြီ', 'ကျွန်', 'တော်']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', 'ပစ္စည်း', 'ဝယ်', 'မ', 'လို့', 'ကျွန်', 'တော်', 'တို့']
Syllables for sample text: ['တ', 'နင်္ဂ', 'နွေ', 'နေ့', 'သွား', 'မယ်', 'ဘယ်', 'လို', 'လဲ']
Syllables for sample text: ['တ', 'နင်္ဂ', 'နွေ', 'နေ့', 'ဆို', 'လူ', 'အ', 'ရမ်း', 'များ', 'တယ်']
Syllables for sample text: ['ဒါ', 'ဆို', 'မ', 'နက်', 'ဖြန်', 'ည', 'နေ', 'သွား', 'ရ', 'အောင်']
Syllables for sample text: ['အစ်', 'မ', 'ကျွန်', 'တော်', 'ဟို', 'အင်္ကျီ', 'ကြည့်', 'ကြည့်', 'မယ်']
Syllables for sample text: ['ကောင်း', 'ပါ', 'ပြီ', 'ကြည့်', 'ပါ']
Syllables for sample text: ['ကျွန်', 'တော်', 'စမ်း', 'ဝတ်', 'ကြည့်', 'လို့', 'ရ', 'မ', 'လား']
Syllables for sample text: ['ခင်', 'ဗျား', 'ခ', 'ဏ', 'စမ်း', 'ဝတ်', 'ကြည့်', 'ပါ']
Syllables for sample text: ['ဒီ', 'တစ်', 'ထည်', 'က', 'အ', 'ရမ်း', 'တို', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဟို', 'တစ်', 'ထည်', 'စမ်း', 'ဝတ်', 'ကြည့်', 'ပါ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ကျွန်', 'တော်', 'နောက်', 'တစ်', 'ခေါက်', 'ခ', 'ဏ', 'စမ်း']
Syllables for sample text: ['ဒီ', 'တစ်', 'ထည်', 'က', 'ကြီး', 'လည်း', 'မ', 'ကြီး', 'ဘူး', 'သေး']
Syllables for sample text: ['အ', 'ဆင်', 'ပြေ', 'လိုက်', 'တာ', 'ကျွန်', 'တော်', 'ဒီ', 'တစ်', 'ထည်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘယ်', 'မှာ', 'လဲ']
Syllables for sample text: ['နိုင်', 'ငံ', 'ခြား', 'ပ', 'ညာ', 'တော်', 'သင်', 'ကျောင်း', 'သား', 'အ']
Syllables for sample text: ['အ', 'ဆောက်', 'အ', 'ဦး', 'နံ', 'ပါတ်', 'က', 'ဘယ်', 'လောက်', 'လဲ']
Syllables for sample text: ['အ', 'ဆောက်', 'အ', 'ဦး', 'နံ', 'ပါတ်', '၉', 'ပါ']
Syllables for sample text: ['အ', 'ခန်း', 'နံ', 'ပါတ်', 'က', 'ဘယ်', 'လောက်', 'လဲ']
Syllables for sample text: ['အ', 'ခန်း', 'နံ', 'ပါတ်', '၃', '၀', '၈', 'ပါ', 'ခင်', 'ဗျား']
Syllables for sample text: ['ကျွန်', 'တော့်', 'အိမ်', 'က', 'ရွှယ်', 'ယွမ့်', 'လမ်း', 'နံ', 'ပါတ်', '၂']
Syllables for sample text: ['ကျေး', 'ဇူး', 'တင်', 'ပါ', 'တယ်']
Syllables for sample text: ['ကျန်း', 'လိ', 'ရင်း', 'ရဲ့', 'အိမ်', 'က', 'ဘယ်', 'နေ', 'ရာ', 'မှာ']
Syllables for sample text: ['ကျွန်', 'တော်', 'မ', 'သိ', 'ဘူး', 'ဝမ်', 'လန်', 'သိ', 'တယ်', 'သူ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ကျွန်', 'တော်', 'သူ့', 'ကို', 'သွား', 'မေး', 'လိုက်', 'မယ်']
Syllables for sample text: ['ဝမ်', 'လန်', 'ကျန်း', 'လိ', 'ရင်း', 'အိမ်', 'က', 'ဘယ်', 'နေ', 'ရာ']
Syllables for sample text: ['သုန်', 'ဆစ့်', 'လမ်း', 'မ', 'ကြီး', 'နံ', 'ပါတ်', '၉', '၇', 'ပါ']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'မ', 'နက်', 'ဖြန်', 'ကျွန်', 'တော်', 'သူ့', 'အိမ်', 'သွား']
Syllables for sample text: ['ခင်', 'ဗျား', 'လမ်း', 'မ', 'ကျွမ်း', 'ဘူး', 'ကျွန်', 'တော်', 'တို့', 'အ']
Syllables for sample text: ['ဒါ', 'ဆို', 'ရင်', 'သိပ်', 'ကောင်း', 'တာ', 'ပေါ့']
Syllables for sample text: ['ခင်', 'ဗျား', 'က', 'ဒီ', 'မြို့', 'က', 'လူ', 'လား']
Syllables for sample text: ['မ', 'ဟုတ်', 'ဘူး', 'ကျွန်', 'တော့်', 'အိမ်', 'က', 'တ', 'ခြား', 'မြို့']
Syllables for sample text: ['ဟုတ်', 'လား', 'ကျွန်', 'တော့်', 'အိမ်', 'က', 'ရွာ', 'မှာ']
Syllables for sample text: ['ကျေး', 'ဇူး', 'ပြု', 'ပြီး', 'ခ', 'ဏ', 'စုံ', 'စမ်း', 'ပါ', 'ရ']
Syllables for sample text: ['အ', 'ရှေ့', 'ဘက်', 'မှာ', 'ဘဏ်', 'တစ်', 'ခု', 'ရှိ', 'တယ်', 'စာ']
Syllables for sample text: ['ဘဏ်', 'ရဲ့', 'ဘေး', 'မှာ', 'ဘာ', 'ရှိ', 'လဲ']
Syllables for sample text: ['ဘဏ်', 'ရဲ့', 'ဘေး', 'မှာ', 'ဈေး', 'တစ်', 'ခု', 'ရှိ', 'တယ်']
Syllables for sample text: ['ဒီ', 'က', 'နေ', 'တက္က', 'သိုလ်', 'ကို', 'ဝေး', 'လား']
Syllables for sample text: ['မ', 'ဝေး', 'ပါ', 'ဘူး', 'အ', 'လွန်', 'နီး', 'ပါ', 'တယ်', 'ဒီ']
Syllables for sample text: ['တက္က', 'သိုလ်', 'နား', 'မှာ', 'စ', 'တိုး', 'ဆိုင်', 'ရှိ', 'လား']
Syllables for sample text: ['ရှိ', 'တာ', 'ပေါ့', 'တက္က', 'သိုလ်', 'ဘေး', 'မှာ', 'စ', 'တိုး', 'ဆိုင်']
Syllables for sample text: ['ခင်', 'ဗျား', 'မ', 'နက်', 'တိုင်း', 'ဘာ', 'စား', 'သောက်', 'သ', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'နွား', 'နို့', 'တစ်', 'ခွက်', 'အ', 'မြဲ', 'သောက်', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'က', 'မ', 'နက်', 'လည်း', 'နွား', 'နို့', 'သောက်', 'တယ်']
Syllables for sample text: ['ဟုတ်', 'တာ', 'ပေါ့', 'ကျွန်', 'တော်', 'က', 'နွား', 'နို့', 'သောက်', 'ရ']
Syllables for sample text: ['ဒီ', 'နေ့', 'ခင်', 'ဗျား', 'ဘယ်', 'အ', 'ချိန်', 'အိပ်', 'ရာ', 'ထ']
Syllables for sample text: ['ဒီ', 'နေ့', 'ကျွန်', 'တော်', '၆', 'နာ', 'ရီ', 'အိပ်', 'ရာ', 'ထ']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', '၆', 'နာ', 'ရီ', 'ထ', 'တာ', 'မ', 'နေ့']
Syllables for sample text: ['ည', '၁', '၁', 'နာ', 'ရီ', 'က', 'အိပ်', 'တာ', 'မ', 'နေ့']
Syllables for sample text: ['ဒီ', 'နေ့', 'ခင်', 'ဗျား', 'ရေ', 'ချိုး', 'မှာ', 'လား']
Syllables for sample text: ['ရေ', 'ချိုး', 'မယ်', 'ရေ', 'ချိုး', 'ပြီး', 'ရင်', 'အ', 'ဝတ်', 'လျှော်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘယ်', 'အ', 'ချိန်', 'ထ', 'မင်း', 'ချက်', 'မှာ', 'လဲ']
Syllables for sample text: ['ခ', 'ဏ', 'နေ', 'ရင်', 'ထ', 'မင်း', 'ချက်', 'မယ်', 'ထ', 'မင်း']
Syllables for sample text: ['နင့်', 'အစ်', 'ကို', 'က', 'ဘယ်', 'သွား', 'လဲ']
Syllables for sample text: ['စင်္ကာ', 'ပူ', 'သွား', 'တယ်']
Syllables for sample text: ['သူ', 'က', 'အင်', 'ဂျင်', 'နီ', 'ယာ', 'လား']
Syllables for sample text: ['မ', 'ဟုတ်', 'ဘူး', 'သူ', 'က', 'ကွန်', 'ပျူ', 'တာ', 'ပ', 'ညာ']
Syllables for sample text: ['သူ', 'ဘယ်', 'အ', 'ချိန်', 'က', 'သွား', 'တာ', 'လဲ', 'ဘယ်', 'နှ']
Syllables for sample text: ['သူ', 'က', '၂', '၀', '၁', '၃', 'ခု', 'နှစ်', 'က', 'သွား']
Syllables for sample text: ['ဘယ်', 'လို', 'လဲ', 'သူ့', 'အ', 'လုပ်', 'က', 'ကောင်း', 'လား']
Syllables for sample text: ['သူ', 'က', 'ပြော', 'တယ်', 'မ', 'ဆိုး', 'ဘူး', 'တဲ့', 'ဘယ်', 'လို']
Syllables for sample text: ['သွား', 'ချင်', 'တယ်', 'ကျွန်', 'တော်', 'က', 'ကို', 'ရီး', 'ယား', 'သွား']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', 'တ', 'ရုတ်', 'နိုင်', 'ငံ', 'ကို', 'သွား', 'ချင်']
Syllables for sample text: ['ခင်', 'ဗျား', 'တ', 'ရုတ်', 'နိုင်', 'ငံ', 'ကို', 'ရောက်', 'ဖူး', 'လား']
Syllables for sample text: ['မ', 'ရောက်', 'ဖူး', 'ဘူး', 'ခင်', 'ဗျား', 'ရော', 'ရောက်', 'ဖူး', 'လား']
Syllables for sample text: ['ကျွန်', 'တော်', 'တ', 'ရုတ်', 'နိုင်', 'ငံ', 'ကို', 'နှစ်', 'ကြိမ်', 'ရောက်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ယိုး', 'ဒ', 'ယား', 'ရောက်', 'ဖူး', 'လား']
Syllables for sample text: ['မ', 'ရောက်', 'ဖူး', 'ဘူး', 'ခင်', 'ဗျား', 'ယိုး', 'ဒ', 'ယား', 'သွား']
Syllables for sample text: ['မ', 'သွား', 'ချင်', 'ဘူး', 'ကျွန်', 'တော်', 'က', 'ဂျ', 'ပန်', 'သွား']
Syllables for sample text: ['အ', 'ခု', 'လူ', 'တော်', 'တော်', 'များ', 'များ', 'ဂျ', 'ပန်', 'သွား']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'စင်္ကာ', 'ပူ', 'သွား', 'တဲ့', 'လူ', 'တွေ', 'လဲ', 'အ']
Syllables for sample text: ['ခင်', 'ဗျား', 'က', 'ဘာ', 'လူ', 'မျိုး', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', 'က', 'ပြား', 'ပါ']
Syllables for sample text: ['ခင်', 'ဗျား', 'အ', 'ဖေ', 'အ', 'မေ', 'က', 'ဘာ', 'လူ', 'မျိုး']
Syllables for sample text: ['ကျွန်', 'တော့်', 'အ', 'ဖေ', 'က', 'ရှမ်း', 'လူ', 'မျိုး', 'ကျွန်', 'တော့်']
Syllables for sample text: ['ခင်', 'ဗျား', 'အစ်', 'မ', 'ကြီး', 'ရဲ့', 'အ', 'မျိုး', 'သား', 'က']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'ခင်', 'ဗျား', 'တို့', 'ရဲ့', 'ဆ', 'ရာ', 'က', 'ဘာ']
Syllables for sample text: ['ကျွန်', 'တော်', 'တို့', 'ရဲ့', 'ဆ', 'ရာ', 'က', 'ဂျ', 'ပန်', 'လူ']
Syllables for sample text: ['ခင်', 'ဗျား', 'က', 'ဗုဒ္ဓ', 'ဘာ', 'သာ', 'လား']
Syllables for sample text: ['မ', 'ဟုတ်', 'ဘူး', 'ကျွန်', 'တော်', 'က', 'ခ', 'ရစ်', 'ယာန်', 'ခင်']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', 'ခ', 'ရစ်', 'ယာန်', 'ပဲ']
Syllables for sample text: ['ကျွန်', 'တော့်', 'ညီ', 'ရဲ့', 'အ', 'မျိုး', 'သ', 'မီး', 'က', 'ဗုဒ္ဓ']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဗိုက်', 'ဆာ', 'လား']
Syllables for sample text: ['မ', 'ဆာ', 'ဘူး', 'ကျွန်', 'တော်', 'မော', 'လိုက်', 'တာ', 'နောက်', 'ပြီး']
Syllables for sample text: ['ဒီ', 'နေ့', 'အ', 'လုပ်', 'များ', 'တယ်', 'ကျွန်', 'တော်', 'လည်း', 'မော']
Syllables for sample text: ['ကျွန်', 'တော်', 'တို့', 'ကော်', 'ဖီ', 'ဆိုင်', 'သွား', 'ပြီး', 'တစ်', 'ခု']
Syllables for sample text: ['ရ', 'တယ်', 'ကျွန်', 'တော်', 'သ', 'ဘော', 'တူ', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'စား', 'ချင်', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', 'ထ', 'မင်း', 'စား', 'ချင်', 'တယ်']
Syllables for sample text: ['ကျွန်', 'တော်', 'ထ', 'မင်း', 'မ', 'စား', 'ချင်', 'ဘူး', 'သား', 'ရေ']
Syllables for sample text: ['ရ', 'ပါ', 'တယ်', 'ကျွန်', 'တော်', 'ဘာ', 'စား', 'စား', 'ရ', 'ပါ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ဒါ', 'ဆို', 'သွား', 'ကြ', 'တာ', 'ပေါ့']
Syllables for sample text: ['အစ်', 'ကို', 'ခင်', 'ဗျား', 'ဘာ', 'ဖြစ်', 'တာ', 'လဲ']
Syllables for sample text: ['ဘာ', 'မှ', 'မ', 'ဖြစ်', 'ဘူး', 'ချောင်း', 'နည်း', 'နည်း', 'ဆိုး', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဆေး', 'လိပ်', 'မ', 'သောက်', 'နဲ့', 'တော့']
Syllables for sample text: ['ကျွန်', 'တော်', 'နေ့', 'တိုင်း', 'သောက်', 'တာ', 'မ', 'များ', 'ဘူး']
Syllables for sample text: ['အဲ', 'ဒါ', 'က', 'ကျန်း', 'မာ', 'ရေး', 'အ', 'တွက်', 'လည်း', 'မ']
Syllables for sample text: ['ကျွန်', 'တော်', 'မ', 'သောက်', 'ချင်', 'ဘူး', 'ဒါ', 'ပေ', 'မဲ့', 'နေ']
Syllables for sample text: ['အ', 'ချိန်', 'ကြာ', 'လာ', 'ရင်', 'အ', 'ကျင့်', 'ဖြစ်', 'သွား', 'မှာ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ကျွန်', 'တော်', 'စမ်း', 'ကြည့်', 'မယ်', 'ဒီ', 'နေ့', 'ဆေး']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဆေး', 'ရုံ', 'သွား', 'ကြည့်', 'ပါ', 'လား']
Syllables for sample text: ['ခင်', 'ဗျား', 'စက်', 'ဘီး', 'စီး', 'တာ', 'အ', 'ရမ်း', 'မြန်', 'တယ်']
Syllables for sample text: ['ကျွန်', 'တော်', 'ကိစ္စ', 'ရှိ', 'လို့', 'မြန်', 'မြန်', 'သွား', 'ရ', 'မယ်']
Syllables for sample text: ['အဲ', 'ဒါ', 'ဆို', 'လည်း', 'အဲ', 'ဒီ', 'လောက်', 'မ', 'မြန်', 'သင့်']
Syllables for sample text: ['ကိစ္စ', 'မ', 'ရှိ', 'ပါ', 'ဘူး', 'ကျွန်', 'တော်', 'စက်', 'ဘီး', 'စီး']
Syllables for sample text: ['စီး', 'တာ', 'မြန်', 'ရင်', 'မ', 'တော်', 'တ', 'ဆ', 'တိုက်', 'ခိုက်']
Syllables for sample text: ['မ', 'နေ့', 'က', 'တက္က', 'သိုလ်', 'ရဲ့', 'ရှေ့', 'မှာ', 'လမ်း', 'ပန်း']
Syllables for sample text: ['တ', 'ကယ်', 'လား']
Syllables for sample text: ['ခင်', 'ဗျား', 'လုံ', 'ခြုံ', 'မှု', 'ကို', 'ဂ', 'ရု', 'စိုက်', 'ရ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ကျွန်', 'တော်', 'နောက်', 'ဆို', 'ရင်', 'မြန်', 'မြန်', 'မ']
Syllables for sample text: ['ယ', 'ခု', 'ခေတ်', 'ကမ္ဘာ', 'ပေါ်', 'မှာ', 'ဘယ်', 'ဘာ', 'သာ', 'စ']
Syllables for sample text: ['ပ', 'ထ', 'မ', 'တစ်', 'ခု', 'က', 'အင်္ဂ', 'လိပ်', 'စ', 'ကား']
Syllables for sample text: ['ခင်', 'ဗျား', 'အင်္ဂ', 'လိပ်', 'စ', 'ကား', 'တတ်', 'လား']
Syllables for sample text: ['တက်', 'တယ်', 'ခင်', 'ဗျား', 'ရော']
Syllables for sample text: ['နည်း', 'နည်း', 'တက်', 'တယ်']
Syllables for sample text: ['ခင်', 'ဗျား', 'တ', 'ရုတ်', 'စ', 'ကား', 'တက်', 'လား']
Syllables for sample text: ['နည်း', 'နည်း', 'မှ', 'မ', 'တက်', 'ဘူး', 'ကျွန်', 'တော်', 'သင်', 'ယူ']
Syllables for sample text: ['ကျွန်', 'တော်', 'တ', 'ရုတ်', 'စ', 'ကား', 'နည်း', 'နည်း', 'တတ်', 'တယ်']
Syllables for sample text: ['တ', 'ရုတ်', 'စ', 'ကား', 'ခက်', 'လား']
Syllables for sample text: ['တ', 'ရုတ်', 'စ', 'ကား', 'မ', 'ခက်', 'ဘူး', 'တ', 'ရုတ်', 'စာ']
Syllables for sample text: ['တ', 'ရုတ်', 'စာ', 'လုံး', 'က', 'အ', 'များ', 'ကြီး', 'ရှိ', 'တယ်']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'ဒါ', 'ပေ', 'မဲ့', 'မင်း', 'ဖြည်း', 'ဖြည်း', 'သင်', 'ယူ']
Syllables for sample text: ['ငါ', 'တို့', 'တ', 'ရုတ်', 'စ', 'ကား', 'သင်', 'သင့်', 'တယ်', 'အင်္ဂ']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'ဒါ', 'ကြောင့်', 'အ', 'ချိန်', 'ပေး', 'ပြီး', 'ကောင်း', 'ကောင်း']
Syllables for sample text: ['မ', 'နေ့', 'က', 'ခင်', 'ဗျား', 'ဘာ', 'ဝယ်', 'လာ', 'တာ', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'ဘောင်း', 'ဘီ', 'တစ်', 'ထည်', 'နဲ့', 'အင်္ကျီ', 'နှစ်', 'ထည်']
Syllables for sample text: ['ဘောင်း', 'ဘီ', 'က', 'အ', 'တို', 'လား', 'အ', 'ရှည်', 'လား']
Syllables for sample text: ['ဘောင်း', 'ဘီ', 'အ', 'ရှည်', 'တစ်', 'ထည်', 'နဲ့', 'အင်္ကျီ', 'လက်', 'ရှည်']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', 'တစ်', 'ကိုယ်', 'ကောင်း', 'ဆန်', 'တဲ့', 'လူ', 'မ']
Syllables for sample text: ['ကျွန်', 'တော်', 'တို့', 'ကျောင်း', 'က', 'ဆ', 'ရာ', 'မ', 'တွေ', 'က']
Syllables for sample text: ['တောင်း', 'ပန်', 'ပါ', 'တယ်', 'ခင်', 'ဗျား', 'ကို', 'အ', 'နှောင့်', 'အ']
Syllables for sample text: ['မ', 'ရှက်', 'ပါ', 'နဲ့']
Syllables for sample text: ['ကျွန်', 'တော်', 'သူ', 'တို့', 'ကို', 'အ', 'လွန်', 'စိတ်', 'ပူ', 'တယ်']
Syllables for sample text: ['မေ့', 'သွား', 'ပြီ']
Syllables for sample text: ['ကျွန်', 'တော်', 'မ', 'မေ့', 'ပါ', 'ဘူး', 'ခင်', 'ဗျား', 'စိတ်', 'ချ']
Syllables for sample text: ['မင်္ဂ', 'လာ', 'ပါ', 'ခင်', 'ဗျား', 'ဘာ', 'ကြည့်', 'မ', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော့်', 'ကို', 'ဟို', 'အင်္ကျီ', 'ပြ', 'ပါ']
Syllables for sample text: ['ဒီ', 'အင်္ကျီ', 'လား']
Syllables for sample text: ['ဟုတ်', 'တယ်', 'ဒီ', 'အင်္ကျီ', 'က', 'ဘယ်', 'လောက်', 'လဲ']
Syllables for sample text: ['ရှစ်', 'ထောင်']
Syllables for sample text: ['နည်း', 'နည်း', 'လျှော့', 'ပါ', 'ဦး']
Syllables for sample text: ['နင့်', 'ကို', '၃', '၀', '၀', 'လျှော့', 'ပေး', 'မယ်']
Syllables for sample text: ['နည်း', 'နည်း', 'ထပ်', 'လျှော့', 'ဦး', '၇', '၀', '၀', '၀', 'ပဲ']
Syllables for sample text: ['ဆော', 'ရီး', 'ခင်', 'ဗျား', 'ပြော', 'တဲ့', 'ဈေး', 'နှုန်း', 'ကို', 'ကျွန်']
Syllables for sample text: ['အ', 'နိမ့်', 'ဆုံး', 'ဈေး', 'ဘယ်', 'လောက်', 'လဲ']
Syllables for sample text: ['အ', 'နိမ့်', 'ဆုံး', 'ခု', 'နှစ်', 'ထောင်', 'ငါး', 'ရာ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ကျွန်', 'တော့်', 'ကို', 'ဟို', 'တစ်', 'ထည်', 'ပေး', 'ပါ']
Syllables for sample text: ['မေး', 'ပါ', 'ရ', 'စေ', 'ဒီ', 'လို', 'မျိုး', 'တံ', 'ဆိပ်', 'ရှိ']
Syllables for sample text: ['ကျွန်', 'တော်', 'တို့', 'ဆိုင်', 'မှာ', 'ဒါ', 'မျိုး', 'တံ', 'ဆိပ်', 'မ']
Syllables for sample text: ['ဘာ', 'တံ', 'ဆိပ်', 'ရှိ', 'လဲ', 'ကျွန်', 'တော်', 'ကြည့်', 'ကြည့်', 'မယ်']
Syllables for sample text: ['ကြယ်', 'ကိုး', 'လုံး', 'တံ', 'ဆိပ်', 'စိန်', 'တံ', 'ဆိပ်', 'ရှိ', 'တယ်']
Syllables for sample text: ['စိန်', 'တံ', 'ဆိပ်', 'က', 'ဝတ်', 'လို့', 'ကောင်း', 'လား']
Syllables for sample text: ['မ', 'ဆိုး', 'ဘူး', 'လူ', 'တော်', 'တော်', 'များ', 'များ', 'စိန်', 'တံ']
Syllables for sample text: ['ကြွ', 'ရောက်', 'လာ', 'တာ', 'ကို', 'ကြို', 'ဆို', 'ပါ', 'တယ်', 'ခင်']
Syllables for sample text: ['ကျွန်', 'တော်', 'အ', 'ဖြူ', 'ရောင်', 'အင်္ကျီ', 'ကြည့်', 'မယ်']
Syllables for sample text: ['အင်္ကျီ', 'အ', 'ဖြူ', 'က', 'ဒီ', 'လို', 'ဒီ', 'ဇိုင်း', 'ရှိ', 'တယ်']
Syllables for sample text: ['မ', 'ကြိုက်', 'ဘူး']
Syllables for sample text: ['ကျွန်', 'တော်', 'ဟို', 'လို', 'ဒီ', 'ဇိုင်း', 'ကြိုက်', 'တယ်', 'ဟို', 'လို']
Syllables for sample text: ['ဟုတ်', 'ကဲ့', 'ဒီ', 'လို', 'ဒီ', 'ဇိုင်း', 'က', 'အ', 'မဲ', 'အ']
Syllables for sample text: ['တ', 'ခြား', 'အ', 'ရောင်', 'မ', 'ရှိ', 'ဘူး', 'လား', 'ကျွန်', 'တော်']
Syllables for sample text: ['ဒါ', 'ဆို', 'ခင်', 'ဗျား', 'တ', 'ခြား', 'ဒီ', 'ဇိုင်း', 'တွေ', 'ကြည့်']
Syllables for sample text: ['အ', 'စိမ်း', 'ရောင်', 'ဘေး', 'က', 'ဟို', 'ဒီ', 'ဇိုင်း', 'က', 'ဘယ်']
Syllables for sample text: ['အ', 'နီ', 'ရောင်', 'ရှိ', 'တယ်', 'အ', 'ပြာ', 'မိုး', 'ပြာ', 'ရောင်']
Syllables for sample text: ['မိုး', 'ပြာ', 'ရောင်', 'က', 'ဆိုဒ်', 'လတ်', 'ရှိ', 'လား']
Syllables for sample text: ['ရှိ', 'တယ်', 'ဒါ', 'ပေ', 'မဲ့', 'နင်', 'ကြည့်', 'ရ', 'တာ', 'မ']
Syllables for sample text: ['ကောင်း', 'ပြီ', 'ငါ့', 'ကို', 'ဆိုဒ်', 'သေး', 'ပေး', 'ပါ']
Syllables for sample text: ['ကျေး', 'ဇူး', 'ပဲ', 'နောက်', 'လည်း', 'လာ', 'ဝယ်', 'ပါ', 'နော်']
Syllables for sample text: ['ခင်', 'ဗျား', 'တို့', 'ဆိုင်', 'က', 'ဈေး', 'မ', 'ကြီး', 'ရင်', 'ကျွန်']
Syllables for sample text: ['စိတ်', 'ချ', 'ဝယ်', 'ပါ', 'ကျွန်', 'တော်', 'တို့', 'ဆိုင်', 'က', 'ဈေး']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'အ', 'ရောင်', 'ကြိုက်', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', 'အ', 'ဖြူ', 'ရောင်', 'ပန်း', 'ရောင်', 'မိုး', 'ပြာ']
Syllables for sample text: ['မ', 'ဟုတ်', 'ဘူး', 'ကျွန်', 'တော်', 'သိ', 'ချင်', 'တာ', 'က', 'ခင်']
Syllables for sample text: ['ကျွန်', 'တော်', 'အ', 'ကြိုက်', 'ဆုံး', 'က', 'ပန်း', 'ရောင်']
Syllables for sample text: ['ဒါ', 'ဆို', 'ခင်', 'ဗျား', 'မှာ', 'ပန်း', 'ရောင်', 'အင်္ကျီ', 'ရှိ', 'လား']
Syllables for sample text: ['ရှိ', 'တာ', 'ပေါ့', 'ကျွန်', 'တော့်', 'မှာ', 'ပန်း', 'ရောင်', 'အင်္ကျီ', 'အ']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဒီ', 'နေ့', 'ဝတ်', 'တဲ့', 'ဘောင်း', 'ဘီ', 'မ', 'ဆိုး']
Syllables for sample text: ['လိ', 'လိ', 'အ', 'ထည်', 'ဆိုင်', 'က', 'ဝယ်', 'တာ']
Syllables for sample text: ['ဘာ', 'တံ', 'ဆိပ်', 'လဲ', 'ဈေး', 'ကြီး', 'လား']
Syllables for sample text: ['ဈေး', 'မ', 'ကြီး', 'ဘူး']
Syllables for sample text: ['ဝတ်', 'လို့', 'ကောင်း', 'လား']
Syllables for sample text: ['ဝတ်', 'လို့', 'အ', 'ရမ်း', 'ကောင်း', 'တယ်']
Syllables for sample text: ['ပန်း', 'သီး', 'တစ်', 'လုံး', 'ဘယ်', 'လောက်', 'လဲ']
Syllables for sample text: ['တစ်', 'လုံး', 'ခြောက်', 'ရာ']
Syllables for sample text: ['ချို', 'လား']
Syllables for sample text: ['အ', 'လွန်', 'ချို', 'တယ်', 'ဒါ', 'က', 'တ', 'ရုတ်', 'ပြည်', 'က']
Syllables for sample text: ['ခင်', 'ဗျား', 'ဘာ', 'အ', 'သီး', 'စား', 'ရ', 'တာ', 'ကြိုက်', 'လဲ']
Syllables for sample text: ['ကျွန်', 'တော်', 'က', 'စ', 'တော်', 'ဘယ်', 'ရီ', 'စား', 'ရ', 'တာ']
Syllables for sample text: ['ကျွန်', 'တော်', 'လည်း', 'စ', 'တော်', 'ဘယ်', 'ရီ', 'ကြိုက်', 'တယ်']
Syllables for sample text: ['ကျွန်', 'တော်', 'တို့', 'နှစ်', 'ယောက်', 'အ', 'တူ', 'တူ', 'ပဲ']
Sample data for model training: [['နေ', 'က', 'မီး', 'ကျီး', 'ခဲ', 'လို', 'ရဲ', 'ရဲ', 'တောက်', 'ပြီး', 'တက်', 'လာ', 'တယ်', 'ပြီး', 'တော့', 'ငါ', 'တို့', 'ရပ်', 'နိုင်', 'ရုံ', 'လောက်', 'ပဲ', 'ရှိ', 'ပေ', 'မဲ့', 'အ', 'ခု', 'ဘယ်', 'နည်း', 'နဲ့', 'မ', 'ဆို', 'တိုက်', 'ခိုက်', 'ရ', 'တော့', 'မယ်', 'စစ်', 'သည်', 'ရဲ', 'မက်', 'တွေ', 'မ', 'ဟုတ်', 'ဘူး', 'တစ်', 'ယောက်', 'ချင်း', 'တိုက်', 'ခိုက်', 'တာ', 'မ', 'ဟုတ်', 'ဘူး', 'ဒါ', 'က', 'ရန်', 'ပွဲ', 'တစ်', 'ပွဲ'], ['တော', 'မီး', 'တွေ', 'နဲ့', 'ရေ', 'ကြီး', 'မှု', 'တွေ', 'ရဲ့', 'ဘေး', 'ဒဏ်', 'ကို', 'ခံ', 'ခဲ့', 'ရ', 'တဲ့', 'အ', 'မေ', 'ရိ', 'ကန်', 'ပြည်', 'ထောင်', 'စု', 'တစ်', 'ခွင်', 'က', 'မိ', 'သား', 'စု', 'တွေ', 'အ', 'တွက်', 'ကြက်', 'ခြေ', 'နီ', 'အ', 'ဖွဲ့', 'က', 'ထောက်', 'ပံ့', 'မှု', 'တွေ', 'ပေး', 'နေ', 'တယ်'], ['ဒီ', 'ည', 'နေ', 'ကျွန်', 'တော်', 'တို့', 'ရဲ့', 'ပွဲ', 'ကို', 'အ', 'စီ', 'အ', 'စဉ်', 'မှူး', 'အ', 'ဖြစ်', 'ဆောင်', 'ရွက်', 'ပေး', 'သူ', 'က', 'တော့', 'ချစ်', 'စ', 'ရာ', 'ကောင်း', 'တဲ့', 'ဖြစ်', 'ပါ', 'တယ်'], ['ဒါ', 'က', 'ဘာ', 'အ', 'တွက်', 'လဲ', 'ဆို', 'တာ', 'မှန်း', 'ကြည့်'], ['မင်း', 'ရော', 'ငါ', 'ရော', 'မင်း', 'ရဲ့', 'ခွေး', 'လေး', 'ရော', 'ငါ', 'တို့', 'ရဲ့', 'သိ', 'မြင်', 'နား', 'လည်', 'မှု', 'စ', 'ကြ', 'ဝ', 'ဠာ', 'နယ်', 'ပယ်', 'တစ်', 'ခု', 'ထဲ', 'မှာ', 'ပိတ်', 'မိ', 'နေ', 'ကြ', 'တယ်', 'ငါ', 'တို့', 'လွတ်', 'မြောက်', 'နိုင်', 'ရင်', 'အ', 'ရာ', 'ဝတ္ထု', 'တွေ', 'ကို', 'မြင်', 'နိုင်', 'တဲ့', 'တ', 'ခြား', 'နည်း', 'လမ်း', 'တွေ', 'အ', 'များ', 'ကြီး', 'ရှိ', 'လာ', 'မယ်'], ['သူ', 'တို့', 'အ', 'လုပ်', 'ခွင်', 'ရဲ့', 'သ', 'နား', 'စ', 'ရာ', 'အ', 'ခြေ', 'အ', 'နေ', 'ဟာ', 'အ', 'ရင်', 'က', 'ထက်', 'ပို', 'ပြီး', 'အ', 'ခက်', 'အ', 'ခဲ', 'တွေ', 'နဲ့', 'ရင်', 'ဆိုင်', 'လာ', 'ရ', 'တယ်'], ['လုပ်', 'ဖော်', 'ကိုင်', 'ဖက်', 'အ', 'သစ်', 'ဒီ', 'နေ့', 'အ', 'ပြင်', 'မှာ', 'အ', 'ရမ်း', 'အေး', 'တာ', 'တောင်', 'မှ', 'ပတ်', 'ဝန်း', 'ကျင်', 'ထိန်း', 'သိမ်း', 'ရေး', 'အ', 'တွက်', 'ကြံ့', 'ကြံ့', 'ခံ', 'နေ', 'တုန်း', 'ပဲ'], ['တန်', 'နဲ့', 'ချီ', 'တဲ့', 'ပိုး', 'ကောင်', 'တွေ', 'ငါ့', 'ရှေ့', 'က', 'နေ', 'ရာ', 'တိုင်း', 'မှာ', 'ငါ', 'သေ', 'တော့', 'မယ်', 'လို့', 'ငါ', 'ထင်', 'တယ်'], ['သို့', 'ဟား', 'ဟား', 'ဟား', 'မင်း', 'ငါ့', 'ကို', 'လွမ်း', 'နေ', 'မှာ', 'ပဲ', 'အဲ', 'ဒါ', 'ကို', 'ဝန်', 'ခံ', 'လိုက်', 'တာ', 'လုံး', 'ဝ', 'ကောင်း', 'ပါ', 'တယ်'], ['အ', 'ပြင်', 'က', 'စာ', 'ရွက်', 'အ', 'ရွယ်', 'အ', 'စား', 'ထက်', 'ကျော်', 'လွန်', 'ပြီး', 'လျှံ', 'ထွက်', 'နေ', 'တဲ့', 'စာ', 'သား', 'တွေ', 'နဲ့', 'ဖွဲ့', 'ပြီး', 'သား', 'စာ', 'မျက်', 'နှာ', 'တွေ', 'ကို', 'ခေါက်', 'လိုက်', 'အဲ', 'ဒါ', 'ကို', 'လို့', 'လည်း', 'ခေါ်', 'တယ်']]
Sample n-grams: [<generator object everygrams at 0x7f48cef7ad60>, <generator object everygrams at 0x7f48cef7ac80>, <generator object everygrams at 0x7f48cef7add0>, <generator object everygrams at 0x7f48cef7ae40>, <generator object everygrams at 0x7f48cef7aeb0>, <generator object everygrams at 0x7f48cef7af20>, <generator object everygrams at 0x7f48cef7af90>, <generator object everygrams at 0x7f48cb014040>, <generator object everygrams at 0x7f48cb0140b0>, <generator object everygrams at 0x7f48cb014120>]
Language model saved to ./bamar.syl.3gram.lm.txt
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_LM$
```

Syllable segmentation ဖြတ်တာ မှန်ပါတယ်။  

## Note for Me

Date: 23 Jan 2024  

မနေ့က language model ကို NLTK library ကိုသုံးပြီး ဆောက် ပြီးတော့ detect လုပ်ဖို့ ကြိုးစားပေမဲ့ အချိန်တော်တော်ကြာ debug လုပ်ပြီး ပင်ပန်းသွားတယ်။   
အဲဒါနဲ့ အိပ်လိုက်တယ်။  

ဒီနေ့တော့ ပထမဆုံး ရေးခဲ့တဲ့ ngram, naive bayes approach ကိုပဲ syllable unit တစ်မျိုးတည်း မဟုတ်ပဲ character ngram ကိုပါ ဖြည့်ပြီး language detection လုပ်ဖို့ အိုက်ဒီယာ ရခဲ့တယ်။  
ဆိုလိုတာက char only, syl only, char+syl combination သုံးမျိုးသုံးပြီး language detection decision ကို လုပ်ဖို့ပါ။  

## Developing Char, Syl, Char+Syl Ngrams with Bayes Approach

Date: 24 Jan 2024  

python code --help screen ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ python ./char_syl_ngram.py --help
usage: char_syl_ngram.py [-h] --mode {build,detect} -i INPUT [-o OUTPUT]
                         [-p PROFILE_FOLDER] [-n NGRAM] [-v]

Naive Bayes based language detection and profile creation.

optional arguments:
  -h, --help            show this help message and exit
  --mode {build,detect}
                        Mode of operation: build or detect
  -i INPUT, --input INPUT
                        Input file path.
  -o OUTPUT, --output OUTPUT
                        Output file path (only for profile creation).
  -p PROFILE_FOLDER, --profile_folder PROFILE_FOLDER
                        Folder path containing language profiles (only for detection).
  -n NGRAM, --ngram NGRAM
                        Maximum n-gram value (default: 3).
  -v, --verbose         Display warning messages.
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

အဓိက update လုပ်ခဲ့တာက filename တစ်ခုတည်း မဟုတ်ပဲ --input option က string input ကိုလည်း လက်ခံဖို့။ ပြီးတော့ profile ကိုလည်း character ngram ရော syllable ngram ရော နှစ်ခုစလုံး ဆောက်ထားဖို့။ ပြီးတော့ original code မှာတုန်းကလို --profile_build, --detect တစ်ခုစီခွဲပြီး မထားတော့ပဲနဲ့ နှစ်ခုစလုံးကို --mode ဆိုတဲ့ option နဲ့ပဲ control လုပ်ဖို့ (အဲဒါကတော့ တခြားကုဒ်တွေနဲ့ တူအောင် ညှိတဲ့ အပိုင်းပါ) နောက်ပိုင်း library အနေနဲ့သုံးဖို့ ပြောင်းတဲ့အခါမှာ အဆင်ပြေအောင်လို့ပါ။  

Bash shell script for building for all TainYinThar languages ...  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ cat ./build_ngram_profiles.sh
#!/bin/bash

# Define the base directory and the Python script
BASE_DIR="$HOME/exp/sylbreak4all/lang_detection/char_syl_ngram"
PYTHON_SCRIPT="$BASE_DIR/char_syl_ngram.py"
TEXT_DIR="$BASE_DIR/raw"  # Assuming you have raw text files for training
OUTPUT_BASE_DIR="$BASE_DIR"  # Base directory for output profiles

# Define the n-gram values to iterate through
NGRAM_VALUES=(3 4 5)

# Loop through each n-gram value
for ngram_value in "${NGRAM_VALUES[@]}"; do
    # Create the output directory for this n-gram value
    OUTPUT_DIR="$OUTPUT_BASE_DIR/${ngram_value}gram_profile"
    mkdir -p "$OUTPUT_DIR"

    # Loop through each text file in the text_files directory
    for file in "$TEXT_DIR"/*.raw; do
        # Extract the language name from the filename
        filename=$(basename -- "$file")
        language=${filename%%.*}

        # Define the output profile filename based on n-gram value
        output_profile="$OUTPUT_DIR/${language}.${ngram_value}gram"

        # Run the Python script to create the profile
        if python3 "$PYTHON_SCRIPT" --mode build --ngram "$ngram_value" --input "$file" --output "$output_profile"; then
            echo "Created ${ngram_value}-gram language profile for $language."
        else
            echo "Error in creating ${ngram_value}-gram profile for $language. Check the input file and script."
            exit 1
        fi
    done
done

echo "All language profiles have been created."
```

Building profiles for 3gram to 5gram ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ time ./build_ngram_profiles.sh
Created 3-gram language profile for bamar.
Created 3-gram language profile for beik.
Created 3-gram language profile for dawei.
Created 3-gram language profile for mon.
Created 3-gram language profile for pao.
Created 3-gram language profile for po_kayin.
Created 3-gram language profile for rakhine.
Created 3-gram language profile for sgaw_kayin.
Created 3-gram language profile for shan.
Created 4-gram language profile for bamar.
Created 4-gram language profile for beik.
Created 4-gram language profile for dawei.
Created 4-gram language profile for mon.
Created 4-gram language profile for pao.
Created 4-gram language profile for po_kayin.
Created 4-gram language profile for rakhine.
Created 4-gram language profile for sgaw_kayin.
Created 4-gram language profile for shan.
Created 5-gram language profile for bamar.
Created 5-gram language profile for beik.
Created 5-gram language profile for dawei.
Created 5-gram language profile for mon.
Created 5-gram language profile for pao.
Created 5-gram language profile for po_kayin.
Created 5-gram language profile for rakhine.
Created 5-gram language profile for sgaw_kayin.
Created 5-gram language profile for shan.
All language profiles have been created.

real    0m12.952s
user    0m11.756s
sys     0m1.191s
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

Check the 3gram language profiles ...  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ tree ./3gram_profile/
./3gram_profile/
├── bamar.3gram
├── beik.3gram
├── dawei.3gram
├── mon.3gram
├── pao.3gram
├── po_kayin.3gram
├── rakhine.3gram
├── sgaw_kayin.3gram
└── shan.3gram

0 directories, 9 files
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

အစပိုင်းမှာ character unit နဲ့ 3gram ဆောက်ပြီး နောက်ပိုင်းမှာတော့ syllable unit နဲ့ ဆောက်သွားတာကို အောက်ပါအတိုင်း မြင်ရတယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/3gram_profile$ head bamar.3gram
နေက     0.0002653000215549747
ေကမ     4.2730388670518105e-05
ကမီ     8.450690748581713e-06
မီး     0.00039596031943134097
ီးက     0.0005618939296621635
းကျ     0.0006905669986734899
ကျီ     9.78759896753723e-05
ျီး     6.111225567213618e-05
ီးခ     0.00023052351641677835
းခဲ     0.00025536387722977573
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/3gram_profile$ tail ./bamar.3gram
ပြည် က ခင်      1.5227715866140115e-06
အ သီး စား       1.5227715866140115e-06
သီး စား ရ       1.5227715866140115e-06
က စ တော်        1.5227715866140115e-06
ဘယ် ရီ စား      1.5227715866140115e-06
ရီ စား ရ        1.5227715866140115e-06
တော် လည်း စ     1.5227715866140115e-06
လည်း စ တော်     1.5227715866140115e-06
ဘယ် ရီ ကြိုက်   1.5227715866140115e-06
ရီ ကြိုက် တယ်   1.5227715866140115e-06
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/3gram_profile$
```

4gram language profile တွေကိုလည်း လေ့လာခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ tree ./4gram_profile/
./4gram_profile/
├── bamar.4gram
├── beik.4gram
├── dawei.4gram
├── mon.4gram
├── pao.4gram
├── po_kayin.4gram
├── rakhine.4gram
├── sgaw_kayin.4gram
└── shan.4gram

0 directories, 9 files
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/4gram_profile$ head ./sgaw_kayin.4gram
နဘၣ်    0.00020427661610139886
ဘၣ်သ    0.0006640011383928484
ၣ်သံ    8.799863634213576e-05
်သံက    0.0001746459340005828
သံကွ    0.0004148340389087131
ံကွၢ    0.00041214034053591167
ကွၢ်    0.0014487652643356743
ွၢ်တ    0.0002761085727094378
ၢ်တၢ    0.0011883744216315331
်တၢ်    0.004368734300452459
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/4gram_profile$ tail ./sgaw_kayin.4gram
မူး န့ၣ် မၤ သးဒ်        1.1926234186935242e-06
မၤ သးဒ် လဲၣ် ပိာ်       1.1926234186935242e-06
ဖိ လၢ အ အဲၣ်    1.1926234186935242e-06
အဲၣ် ယၤ န့ၣ် န  1.1926234186935242e-06
မိၣ်ဒ် လဲၣ် တၢ် ကူ      1.1926234186935242e-06
ကၤ တ ဖၣ် နာ်    1.1926234186935242e-06
နာ် က့ အ လီၤ    1.1926234186935242e-06
က့ အ လီၤ အဲၣ်   1.1926234186935242e-06
အ လီၤ အဲၣ် ဖိ   1.1926234186935242e-06
လီၤ အဲၣ် ဖိ သ့ၣ်        1.1926234186935242e-06
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/4gram_profile$
```

5gram language profile တွေကိုလည်း ဝင်စစ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ tree ./5gram_profile/
./5gram_profile/
├── bamar.5gram
├── beik.5gram
├── dawei.5gram
├── mon.5gram
├── pao.5gram
├── po_kayin.5gram
├── rakhine.5gram
├── sgaw_kayin.5gram
└── shan.5gram

0 directories, 9 files
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

ဖိုင်တွေရဲ့ အထဲကိုဝင် ဝင်စစ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/5gram_profile$ head -n 30 ./pao.5gram
လိုမူ   0.00010200778097201457
ိုမူႏ   0.00013748360684258913
ုမူႏပ   3.844692628723517e-05
မူႏပေ   0.00015226520095532853
ူႏပေႏ   0.00016409047624552003
ႏပေႏမ   2.971100416660618e-06
ပေႏမာ   7.405578650482437e-06
ေႏမာꩻ   1.1840056884304255e-05
ႏမာꩻတ   4.288140452105699e-05
မာꩻတမ   0.00012270201272984973
ာꩻတမု   0.00015374336036660247
ꩻတမုဲ   0.0004212902138071855
တမုဲင   0.0011248940935735807
မုဲင်   0.005219395662802394
ုဲင်ꩻ   0.005568241283863043
ဲင်ꩻဟ   0.001633380931051816
င်ꩻဟေ   0.0017072889016155129
်ꩻဟော   0.0019304909727178778
ꩻဟောင   0.0027227844171607094
ဟောင်   0.007967294008360647
ောင်း   0.008718198989287808
ာင်း
        0.007526802503801013
င်း
ဝ       0.001287491628813714
်း
ဝွ      0.0017427647274860874
း
ဝွေ     0.001924578335072782

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/5gram_profile$
```

tail command နဲ့လည်း check လုပ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/5gram_profile$ tail -n 30 ./pao.5gram
အဂ် လိပ် ငဝ်း အွိုး အ   5.381683084618761e-06
လိပ် ငဝ်း အွိုး အ မွူး  5.381683084618761e-06
ငဝ်း အွိုး အ မွူး လောင်း        5.381683084618761e-06
အွိုး အ မွူး လောင်း သူꩻ 5.381683084618761e-06
အ မွူး လောင်း သူꩻ အ     5.381683084618761e-06
မွူး လောင်း သူꩻ အ ရာႏ   5.381683084618761e-06
လောင်း သူꩻ အ ရာႏ တ      5.381683084618761e-06
သူꩻ အ ရာႏ တ ဖြုံႏ       5.381683084618761e-06
အ ရာႏ တ ဖြုံႏ ငါꩻ       5.381683084618761e-06
ရာႏ တ ဖြုံႏ ငါꩻ တဲ့     5.381683084618761e-06
တ အဝ်ႏ တဝ်း နာꩻ ထူႏ     5.381683084618761e-06
အဝ်ႏ တဝ်း နာꩻ ထူႏ က     5.381683084618761e-06
တဝ်း နာꩻ ထူႏ က ဟန်      5.381683084618761e-06
နာꩻ ထူႏ က ဟန် အို       5.381683084618761e-06
ထူႏ က ဟန် အို ထ 5.381683084618761e-06
က ဟန် အို ထ ပေႏ 5.381683084618761e-06
ပေႏ ဆေ့ ဆေ့ ဟောင်း ဟန်  5.381683084618761e-06
ဆေ့ ဆေ့ ဟောင်း ဟန် နေင်ႏ        5.381683084618761e-06
ဆေ့ ဟောင်း ဟန် နေင်ႏ လို့       5.381683084618761e-06
ဟောင်း ဟန် နေင်ႏ လို့ ထိုꩻ      5.381683084618761e-06
ဟန် နေင်ႏ လို့ ထိုꩻ နောဝ်ႏ      5.381683084618761e-06
နေင်ႏ လို့ ထိုꩻ နောဝ်ႏ မွိုင်   5.381683084618761e-06
လို့ ထိုꩻ နောဝ်ႏ မွိုင် မွေး    5.381683084618761e-06
ထိုꩻ နောဝ်ႏ မွိုင် မွေး ငါႏ     5.381683084618761e-06
နောဝ်ႏ မွိုင် မွေး ငါႏ နောႏ     5.381683084618761e-06
မွိုင် မွေး ငါႏ နောႏ ထွ 5.381683084618761e-06
မွေး ငါႏ နောႏ ထွ မုဲင်ꩻ 5.381683084618761e-06
ငါႏ နောႏ ထွ မုဲင်ꩻ မွော့        5.381683084618761e-06
နောႏ ထွ မုဲင်ꩻ မွော့ အွဉ်ႏ      5.381683084618761e-06
ထွ မုဲင်ꩻ မွော့ အွဉ်ႏ ဖေင်ꩻ     5.381683084618761e-06
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram/5gram_profile$
```

Test or Experiment လုပ်တဲ့အခါမှာ file တစ်ဖိုင်လုံး input လုပ်ပြီးလည်း evaluate လုပ်ချင်တယ်။ တခြား အထက်က expeirment တွေမှာ လုပ်ခဲ့တဲ့အတိုင်းပဲ random sentence ၁၀ကြောင်းနဲ့လည်း စမ်းချင်တယ်။  
ပြီးတော့ ngram ကိုလည်း 3gram, 4gram, 5gram အားလုံးနဲ့ စမ်းချင်တယ်။  
Testing လုပ်ဖို့အတွက် shell script ကိုအောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$ cat test4exp.sh
#!/bin/bash

# Define base directory and script location
BASE_DIR="/home/ye/exp/sylbreak4all/lang_detection/char_syl_ngram"
PYTHON_SCRIPT="$BASE_DIR/char_syl_ngram.py"
INPUT_DIR="$BASE_DIR/eg_input_raw"

# Number of ngrams and random sentences
NGRAMS=(3 4 5)
NUM_RANDOM_SENTENCES=10

# Loop through each input file
for input_file in "$INPUT_DIR"/*.raw; do
    echo "Processing file: $(basename "$input_file")"

    # Loop through each ngram
    for ngram in "${NGRAMS[@]}"; do
        PROFILE_DIR="$BASE_DIR/${ngram}gram_profile"

        # Run the first command
        echo "Running with ngram=$ngram on full file"
        python "$PYTHON_SCRIPT" --mode detect --input "$input_file" --profile_folder "$PROFILE_DIR" --ngram $ngram

        # Extract and run the second command on random sentences
        for i in $(seq 1 $NUM_RANDOM_SENTENCES); do
            random_sentence=$(shuf -n 1 "$input_file")
            echo "Running with ngram=$ngram on random sentence $i: $random_sentence"
            python "$PYTHON_SCRIPT" --mode detect --input "$random_sentence" --profile_folder "$PROFILE_DIR" --ngram $ngram
        done
    done

    echo ""
done

echo "All processing completed."

(base) ye@lst-gpu-3090:~/exp/sylbreak4all/lang_detection/char_syl_ngram$
```

Experiment-1 (with char, syl, char+syl Ngram, Naive Bayes) ရဲ့ ရလဒ်က အောက်ပါအတိုင်း ...  

```
Processing file: bamar_burmese.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.00%
Running with ngram=3 on random sentence 1: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 59.70%
mon: 0.00%
shan: 0.00%
pao: 0.20%
rakhine: 0.02%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 40.07%

Combined Character and Syllable-based Detection:
beik: 29.85%
mon: 0.00%
shan: 0.00%
pao: 0.10%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 70.03%
Running with ngram=3 on random sentence 2: မင်္ဂလာပါဆရာမ
Character-based Detection:
beik: 0.06%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.21%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 99.73%

Syllable-based Detection:
beik: 13.75%
mon: 0.24%
shan: 0.02%
pao: 0.35%
rakhine: 0.52%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 23.06%
bamar: 62.04%

Combined Character and Syllable-based Detection:
beik: 6.90%
mon: 0.12%
shan: 0.01%
pao: 0.17%
rakhine: 0.36%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 11.53%
bamar: 80.89%
Running with ngram=3 on random sentence 3: ပါပါသမီးကိုလွမ်းနေတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.47%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.52%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.74%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.26%
bamar: 50.00%
Running with ngram=3 on random sentence 4: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
beik: 1.96%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 23.45%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 74.59%

Syllable-based Detection:
beik: 53.34%
mon: 0.06%
shan: 0.35%
pao: 0.01%
rakhine: 0.21%
po_kayin: 0.01%
sgaw_kayin: 0.02%
dawei: 44.79%
bamar: 1.21%

Combined Character and Syllable-based Detection:
beik: 27.65%
mon: 0.03%
shan: 0.18%
pao: 0.00%
rakhine: 11.83%
po_kayin: 0.00%
sgaw_kayin: 0.01%
dawei: 22.40%
bamar: 37.90%
Running with ngram=3 on random sentence 5: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.66%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.34%

Combined Character and Syllable-based Detection:
beik: 49.83%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.17%
Running with ngram=3 on random sentence 6: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.00%
Running with ngram=3 on random sentence 7: နေကောင်းလား
Character-based Detection:
beik: 44.89%
mon: 0.00%
shan: 0.00%
pao: 0.07%
rakhine: 35.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 6.83%
bamar: 12.41%

Syllable-based Detection:
beik: 1.01%
mon: 0.48%
shan: 0.48%
pao: 1.58%
rakhine: 47.41%
po_kayin: 0.48%
sgaw_kayin: 0.48%
dawei: 47.01%
bamar: 1.09%

Combined Character and Syllable-based Detection:
beik: 22.95%
mon: 0.24%
shan: 0.24%
pao: 0.82%
rakhine: 41.60%
po_kayin: 0.24%
sgaw_kayin: 0.24%
dawei: 26.92%
bamar: 6.75%
Running with ngram=3 on random sentence 8: နေကောင်းလား
Character-based Detection:
beik: 44.89%
mon: 0.00%
shan: 0.00%
pao: 0.07%
rakhine: 35.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 6.83%
bamar: 12.41%

Syllable-based Detection:
beik: 1.01%
mon: 0.48%
shan: 0.48%
pao: 1.58%
rakhine: 47.41%
po_kayin: 0.48%
sgaw_kayin: 0.48%
dawei: 47.01%
bamar: 1.09%

Combined Character and Syllable-based Detection:
beik: 22.95%
mon: 0.24%
shan: 0.24%
pao: 0.82%
rakhine: 41.60%
po_kayin: 0.24%
sgaw_kayin: 0.24%
dawei: 26.92%
bamar: 6.75%
Running with ngram=3 on random sentence 9: နေကောင်းလား
Character-based Detection:
beik: 44.89%
mon: 0.00%
shan: 0.00%
pao: 0.07%
rakhine: 35.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 6.83%
bamar: 12.41%

Syllable-based Detection:
beik: 1.01%
mon: 0.48%
shan: 0.48%
pao: 1.58%
rakhine: 47.41%
po_kayin: 0.48%
sgaw_kayin: 0.48%
dawei: 47.01%
bamar: 1.09%

Combined Character and Syllable-based Detection:
beik: 22.95%
mon: 0.24%
shan: 0.24%
pao: 0.82%
rakhine: 41.60%
po_kayin: 0.24%
sgaw_kayin: 0.24%
dawei: 26.92%
bamar: 6.75%
Running with ngram=3 on random sentence 10: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.66%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.34%

Combined Character and Syllable-based Detection:
beik: 49.83%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.17%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 50.00%
beik: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 10.13%
mon: 0.00%
bamar: 2.61%
beik: 85.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.67%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 5.06%
mon: 0.00%
bamar: 51.30%
beik: 42.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.84%
shan: 0.00%
Running with ngram=4 on random sentence 2: ကလေးကအိမ်မှာပါ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 97.13%
beik: 2.86%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.01%
shan: 0.00%

Syllable-based Detection:
dawei: 1.76%
mon: 2.42%
bamar: 6.31%
beik: 55.83%
po_kayin: 1.23%
sgaw_kayin: 0.14%
pao: 0.37%
rakhine: 30.71%
shan: 1.23%

Combined Character and Syllable-based Detection:
dawei: 0.88%
mon: 1.21%
bamar: 51.72%
beik: 29.34%
po_kayin: 0.62%
sgaw_kayin: 0.07%
pao: 0.19%
rakhine: 15.36%
shan: 0.62%
Running with ngram=4 on random sentence 3: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.34%
mon: 0.01%
bamar: 0.09%
beik: 99.17%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.39%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.17%
mon: 0.00%
bamar: 50.05%
beik: 49.58%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.20%
shan: 0.00%
Running with ngram=4 on random sentence 4: ပါပါသမီးကိုလွမ်းနေတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 99.90%
beik: 0.10%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 35.42%
mon: 0.36%
bamar: 0.32%
beik: 29.50%
po_kayin: 0.27%
sgaw_kayin: 0.27%
pao: 0.12%
rakhine: 32.58%
shan: 1.16%

Combined Character and Syllable-based Detection:
dawei: 17.71%
mon: 0.18%
bamar: 50.11%
beik: 14.80%
po_kayin: 0.14%
sgaw_kayin: 0.14%
pao: 0.06%
rakhine: 16.29%
shan: 0.58%
Running with ngram=4 on random sentence 5: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 56.81%
beik: 0.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 42.39%
shan: 0.00%

Syllable-based Detection:
dawei: 0.86%
mon: 0.75%
bamar: 2.18%
beik: 93.40%
po_kayin: 1.08%
sgaw_kayin: 0.13%
pao: 0.29%
rakhine: 0.80%
shan: 0.50%

Combined Character and Syllable-based Detection:
dawei: 0.43%
mon: 0.38%
bamar: 29.50%
beik: 47.10%
po_kayin: 0.54%
sgaw_kayin: 0.06%
pao: 0.14%
rakhine: 21.60%
shan: 0.25%
Running with ngram=4 on random sentence 6: ကလေးကအိမ်မှာပါ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 97.13%
beik: 2.86%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.01%
shan: 0.00%

Syllable-based Detection:
dawei: 1.76%
mon: 2.42%
bamar: 6.31%
beik: 55.83%
po_kayin: 1.23%
sgaw_kayin: 0.14%
pao: 0.37%
rakhine: 30.71%
shan: 1.23%

Combined Character and Syllable-based Detection:
dawei: 0.88%
mon: 1.21%
bamar: 51.72%
beik: 29.34%
po_kayin: 0.62%
sgaw_kayin: 0.07%
pao: 0.19%
rakhine: 15.36%
shan: 0.62%
Running with ngram=4 on random sentence 7: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 91.62%
beik: 8.35%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.03%
shan: 0.00%

Syllable-based Detection:
dawei: 6.82%
mon: 2.79%
bamar: 6.06%
beik: 45.04%
po_kayin: 0.91%
sgaw_kayin: 0.91%
pao: 12.49%
rakhine: 24.05%
shan: 0.91%

Combined Character and Syllable-based Detection:
dawei: 3.41%
mon: 1.40%
bamar: 48.84%
beik: 26.70%
po_kayin: 0.46%
sgaw_kayin: 0.46%
pao: 6.25%
rakhine: 12.04%
shan: 0.46%
Running with ngram=4 on random sentence 8: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 91.62%
beik: 8.35%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.03%
shan: 0.00%

Syllable-based Detection:
dawei: 6.82%
mon: 2.79%
bamar: 6.06%
beik: 45.04%
po_kayin: 0.91%
sgaw_kayin: 0.91%
pao: 12.49%
rakhine: 24.05%
shan: 0.91%

Combined Character and Syllable-based Detection:
dawei: 3.41%
mon: 1.40%
bamar: 48.84%
beik: 26.70%
po_kayin: 0.46%
sgaw_kayin: 0.46%
pao: 6.25%
rakhine: 12.04%
shan: 0.46%
Running with ngram=4 on random sentence 9: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 99.82%
beik: 0.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 40.67%
mon: 1.54%
bamar: 4.22%
beik: 48.70%
po_kayin: 0.55%
sgaw_kayin: 0.06%
pao: 0.15%
rakhine: 3.57%
shan: 0.55%

Combined Character and Syllable-based Detection:
dawei: 20.34%
mon: 0.77%
bamar: 52.02%
beik: 24.44%
po_kayin: 0.27%
sgaw_kayin: 0.03%
pao: 0.07%
rakhine: 1.79%
shan: 0.27%
Running with ngram=4 on random sentence 10: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 56.81%
beik: 0.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 42.39%
shan: 0.00%

Syllable-based Detection:
dawei: 0.86%
mon: 0.75%
bamar: 2.18%
beik: 93.40%
po_kayin: 1.08%
sgaw_kayin: 0.13%
pao: 0.29%
rakhine: 0.80%
shan: 0.50%

Combined Character and Syllable-based Detection:
dawei: 0.43%
mon: 0.38%
bamar: 29.50%
beik: 47.10%
po_kayin: 0.54%
sgaw_kayin: 0.06%
pao: 0.14%
rakhine: 21.60%
shan: 0.25%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.79%
mon: 0.00%
shan: 0.00%
beik: 99.21%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.04%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.96%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.02%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.40%
mon: 0.00%
shan: 0.00%
beik: 99.58%
Running with ngram=5 on random sentence 1: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 71.58%
mon: 0.00%
shan: 0.00%
beik: 28.42%

Syllable-based Detection:
sgaw_kayin: 4.55%
rakhine: 0.64%
dawei: 3.27%
pao: 0.20%
po_kayin: 34.26%
bamar: 0.00%
mon: 11.72%
shan: 38.81%
beik: 6.54%

Combined Character and Syllable-based Detection:
sgaw_kayin: 2.27%
rakhine: 0.32%
dawei: 1.64%
pao: 0.10%
po_kayin: 17.13%
bamar: 35.79%
mon: 5.86%
shan: 19.41%
beik: 17.48%
Running with ngram=5 on random sentence 2: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.99%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 2.62%
rakhine: 6.08%
dawei: 13.66%
pao: 5.99%
po_kayin: 22.39%
bamar: 2.81%
mon: 9.70%
shan: 22.39%
beik: 14.35%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.31%
rakhine: 3.04%
dawei: 6.83%
pao: 3.00%
po_kayin: 11.20%
bamar: 51.40%
mon: 4.85%
shan: 11.20%
beik: 7.18%
Running with ngram=5 on random sentence 3: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.93%
mon: 0.00%
shan: 0.00%
beik: 0.07%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 4.14%
dawei: 22.34%
pao: 0.03%
po_kayin: 0.24%
bamar: 0.00%
mon: 0.23%
shan: 0.83%
beik: 72.15%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 2.07%
dawei: 11.17%
pao: 0.01%
po_kayin: 0.12%
bamar: 49.96%
mon: 0.12%
shan: 0.41%
beik: 36.11%
Running with ngram=5 on random sentence 4: မင်္ဂလာပါဆရာမ
Character-based Detection:
sgaw_kayin: 0.02%
rakhine: 0.00%
dawei: 0.17%
pao: 0.26%
po_kayin: 0.02%
bamar: 97.85%
mon: 0.01%
shan: 0.02%
beik: 1.66%

Syllable-based Detection:
sgaw_kayin: 3.54%
rakhine: 3.60%
dawei: 11.26%
pao: 2.17%
po_kayin: 8.80%
bamar: 37.38%
mon: 12.10%
shan: 8.72%
beik: 12.42%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.78%
rakhine: 1.80%
dawei: 5.72%
pao: 1.21%
po_kayin: 4.41%
bamar: 67.61%
mon: 6.05%
shan: 4.37%
beik: 7.04%
Running with ngram=5 on random sentence 5: နေကောင်းလား
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 46.39%
dawei: 0.02%
pao: 0.00%
po_kayin: 0.00%
bamar: 20.07%
mon: 0.00%
shan: 0.00%
beik: 33.52%
Running with ngram=5 on random sentence 6: ကလေးကအိမ်မှာပါ
Character-based Detection:
sgaw_kayin: 0.04%
rakhine: 0.45%
dawei: 0.25%
pao: 0.01%
po_kayin: 0.04%
bamar: 32.00%
mon: 0.04%
shan: 0.04%
beik: 67.13%

Syllable-based Detection:
sgaw_kayin: 2.97%
rakhine: 5.69%
dawei: 9.44%
pao: 6.79%
po_kayin: 25.39%
bamar: 0.40%
mon: 7.67%
shan: 25.39%
beik: 16.26%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.51%
rakhine: 3.07%
dawei: 4.84%
pao: 3.40%
po_kayin: 12.71%
bamar: 16.20%
mon: 3.85%
shan: 12.71%
beik: 41.70%
Running with ngram=5 on random sentence 7: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 100.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.73%
rakhine: 1.53%
dawei: 33.38%
pao: 1.44%
po_kayin: 16.71%
bamar: 1.42%
mon: 7.51%
shan: 7.69%
beik: 23.58%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.36%
rakhine: 0.77%
dawei: 16.69%
pao: 0.72%
po_kayin: 8.35%
bamar: 50.71%
mon: 3.76%
shan: 3.85%
beik: 11.79%
Running with ngram=5 on random sentence 8: မင်္ဂလာပါဆရာမ
Character-based Detection:
sgaw_kayin: 0.02%
rakhine: 0.00%
dawei: 0.17%
pao: 0.26%
po_kayin: 0.02%
bamar: 97.85%
mon: 0.01%
shan: 0.02%
beik: 1.66%

Syllable-based Detection:
sgaw_kayin: 3.54%
rakhine: 3.60%
dawei: 11.26%
pao: 2.17%
po_kayin: 8.80%
bamar: 37.38%
mon: 12.10%
shan: 8.72%
beik: 12.42%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.78%
rakhine: 1.80%
dawei: 5.72%
pao: 1.21%
po_kayin: 4.41%
bamar: 67.61%
mon: 6.05%
shan: 4.37%
beik: 7.04%
Running with ngram=5 on random sentence 9: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 39.04%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 15.32%
mon: 0.00%
shan: 0.00%
beik: 45.64%

Syllable-based Detection:
sgaw_kayin: 16.47%
rakhine: 4.19%
dawei: 11.34%
pao: 9.31%
po_kayin: 16.47%
bamar: 0.01%
mon: 15.20%
shan: 16.47%
beik: 10.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 8.23%
rakhine: 21.61%
dawei: 5.67%
pao: 4.65%
po_kayin: 8.23%
bamar: 7.66%
mon: 7.60%
shan: 8.23%
beik: 28.10%
Running with ngram=5 on random sentence 10: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.93%
mon: 0.00%
shan: 0.00%
beik: 0.07%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 4.14%
dawei: 22.34%
pao: 0.03%
po_kayin: 0.24%
bamar: 0.00%
mon: 0.23%
shan: 0.83%
beik: 72.15%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 2.07%
dawei: 11.17%
pao: 0.01%
po_kayin: 0.12%
bamar: 49.96%
mon: 0.12%
shan: 0.41%
beik: 36.11%

Processing file: beik.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.78%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.22%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 99.89%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=3 on random sentence 1: အဲဒီကိုသောဖို့ငါမင်းကိုငါမတိုက်တွန်းရ။
Character-based Detection:
beik: 76.37%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.06%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 23.57%

Syllable-based Detection:
beik: 0.30%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 3.55%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 96.15%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 38.33%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 1.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 48.07%
bamar: 11.79%
Running with ngram=3 on random sentence 2: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.84%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 5.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 92.57%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.92%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 2.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 46.29%
bamar: 0.00%
Running with ngram=3 on random sentence 3: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 97.91%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 1.64%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.41%
bamar: 0.03%

Combined Character and Syllable-based Detection:
beik: 98.95%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.82%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.20%
bamar: 0.01%
Running with ngram=3 on random sentence 4: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 5: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.53%
mon: 0.01%
shan: 0.00%
pao: 0.03%
rakhine: 8.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 88.25%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 51.76%
mon: 0.01%
shan: 0.00%
pao: 0.01%
rakhine: 4.09%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 44.12%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 5.20%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.63%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 93.72%
bamar: 0.45%

Combined Character and Syllable-based Detection:
beik: 52.60%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.31%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 46.86%
bamar: 0.23%
Running with ngram=3 on random sentence 7: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 5.20%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.63%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 93.72%
bamar: 0.45%

Combined Character and Syllable-based Detection:
beik: 52.60%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.31%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 46.86%
bamar: 0.23%
Running with ngram=3 on random sentence 8: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.84%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 5.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 92.57%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.92%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 2.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 46.29%
bamar: 0.00%
Running with ngram=3 on random sentence 9: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 10: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.53%
mon: 0.01%
shan: 0.00%
pao: 0.03%
rakhine: 8.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 88.25%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 51.76%
mon: 0.01%
shan: 0.00%
pao: 0.01%
rakhine: 4.09%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 44.12%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.24%
mon: 0.05%
bamar: 0.00%
beik: 98.72%
po_kayin: 0.05%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.86%
shan: 0.05%

Combined Character and Syllable-based Detection:
dawei: 0.12%
mon: 0.03%
bamar: 0.00%
beik: 99.36%
po_kayin: 0.03%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.43%
shan: 0.03%
Running with ngram=4 on random sentence 2: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.81%
mon: 0.89%
bamar: 0.79%
beik: 86.65%
po_kayin: 0.18%
sgaw_kayin: 0.18%
pao: 0.07%
rakhine: 7.24%
shan: 0.18%

Combined Character and Syllable-based Detection:
dawei: 1.91%
mon: 0.44%
bamar: 0.40%
beik: 93.32%
po_kayin: 0.09%
sgaw_kayin: 0.09%
pao: 0.04%
rakhine: 3.62%
shan: 0.09%
Running with ngram=4 on random sentence 3: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.24%
mon: 0.05%
bamar: 0.00%
beik: 98.72%
po_kayin: 0.05%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.86%
shan: 0.05%

Combined Character and Syllable-based Detection:
dawei: 0.12%
mon: 0.03%
bamar: 0.00%
beik: 99.36%
po_kayin: 0.03%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.43%
shan: 0.03%
Running with ngram=4 on random sentence 4: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 86.82%
mon: 0.00%
bamar: 3.96%
beik: 9.14%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.07%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 43.41%
mon: 0.00%
bamar: 1.98%
beik: 54.57%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.04%
shan: 0.00%
Running with ngram=4 on random sentence 5: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 48.04%
mon: 1.91%
bamar: 2.21%
beik: 29.66%
po_kayin: 1.99%
sgaw_kayin: 0.91%
pao: 0.57%
rakhine: 12.50%
shan: 2.22%

Combined Character and Syllable-based Detection:
dawei: 24.02%
mon: 0.95%
bamar: 1.11%
beik: 64.83%
po_kayin: 0.99%
sgaw_kayin: 0.45%
pao: 0.28%
rakhine: 6.25%
shan: 1.11%
Running with ngram=4 on random sentence 6: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.03%
beik: 83.68%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 16.29%
shan: 0.00%

Syllable-based Detection:
dawei: 8.06%
mon: 1.76%
bamar: 0.05%
beik: 81.63%
po_kayin: 0.25%
sgaw_kayin: 0.04%
pao: 0.21%
rakhine: 7.17%
shan: 0.85%

Combined Character and Syllable-based Detection:
dawei: 4.03%
mon: 0.88%
bamar: 0.04%
beik: 82.66%
po_kayin: 0.12%
sgaw_kayin: 0.02%
pao: 0.11%
rakhine: 11.73%
shan: 0.42%
Running with ngram=4 on random sentence 7: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 86.82%
mon: 0.00%
bamar: 3.96%
beik: 9.14%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.07%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 43.41%
mon: 0.00%
bamar: 1.98%
beik: 54.57%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.04%
shan: 0.00%
Running with ngram=4 on random sentence 8: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.24%
mon: 0.05%
bamar: 0.00%
beik: 98.72%
po_kayin: 0.05%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.86%
shan: 0.05%

Combined Character and Syllable-based Detection:
dawei: 0.12%
mon: 0.03%
bamar: 0.00%
beik: 99.36%
po_kayin: 0.03%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.43%
shan: 0.03%
Running with ngram=4 on random sentence 9: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 86.82%
mon: 0.00%
bamar: 3.96%
beik: 9.14%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.07%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 43.41%
mon: 0.00%
bamar: 1.98%
beik: 54.57%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.04%
shan: 0.00%
Running with ngram=4 on random sentence 10: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.24%
mon: 0.05%
bamar: 0.00%
beik: 98.72%
po_kayin: 0.05%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.86%
shan: 0.05%

Combined Character and Syllable-based Detection:
dawei: 0.12%
mon: 0.03%
bamar: 0.00%
beik: 99.36%
po_kayin: 0.03%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.43%
shan: 0.03%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%
Running with ngram=5 on random sentence 1: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.01%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.99%

Syllable-based Detection:
sgaw_kayin: 3.86%
rakhine: 2.51%
dawei: 78.00%
pao: 1.03%
po_kayin: 1.12%
bamar: 0.38%
mon: 0.72%
shan: 1.11%
beik: 11.26%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.93%
rakhine: 1.26%
dawei: 39.00%
pao: 0.52%
po_kayin: 0.56%
bamar: 0.19%
mon: 0.36%
shan: 0.56%
beik: 55.63%
Running with ngram=5 on random sentence 2: အဲဒီကိုသောဖို့ငါမင်းကိုငါမတိုက်တွန်းရ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.03%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.01%
mon: 0.00%
shan: 0.00%
beik: 99.96%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 2.04%
dawei: 37.77%
pao: 0.01%
po_kayin: 0.13%
bamar: 0.00%
mon: 0.28%
shan: 0.08%
beik: 59.69%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 1.03%
dawei: 18.88%
pao: 0.00%
po_kayin: 0.07%
bamar: 0.01%
mon: 0.14%
shan: 0.04%
beik: 79.83%
Running with ngram=5 on random sentence 3: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 1.94%
rakhine: 7.53%
dawei: 10.08%
pao: 4.42%
po_kayin: 4.81%
bamar: 0.26%
mon: 3.10%
shan: 4.77%
beik: 63.10%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.97%
rakhine: 3.76%
dawei: 5.04%
pao: 2.21%
po_kayin: 2.40%
bamar: 0.13%
mon: 1.55%
shan: 2.38%
beik: 81.55%
Running with ngram=5 on random sentence 4: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.18%
rakhine: 33.27%
dawei: 36.31%
pao: 0.96%
po_kayin: 1.37%
bamar: 0.99%
mon: 0.47%
shan: 1.55%
beik: 24.89%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.09%
rakhine: 16.64%
dawei: 18.15%
pao: 0.48%
po_kayin: 0.69%
bamar: 0.50%
mon: 0.23%
shan: 0.78%
beik: 62.45%
Running with ngram=5 on random sentence 5: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 2.57%
rakhine: 1.62%
dawei: 17.41%
pao: 1.57%
po_kayin: 5.64%
bamar: 0.04%
mon: 4.12%
shan: 2.94%
beik: 64.10%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.29%
rakhine: 0.81%
dawei: 8.70%
pao: 0.79%
po_kayin: 2.82%
bamar: 0.02%
mon: 2.06%
shan: 1.47%
beik: 82.05%
Running with ngram=5 on random sentence 6: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 2.57%
rakhine: 1.62%
dawei: 17.41%
pao: 1.57%
po_kayin: 5.64%
bamar: 0.04%
mon: 4.12%
shan: 2.94%
beik: 64.10%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.29%
rakhine: 0.81%
dawei: 8.70%
pao: 0.79%
po_kayin: 2.82%
bamar: 0.02%
mon: 2.06%
shan: 1.47%
beik: 82.05%
Running with ngram=5 on random sentence 7: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%
Running with ngram=5 on random sentence 8: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.12%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.03%
mon: 0.00%
shan: 0.00%
beik: 99.86%

Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 33.10%
dawei: 33.42%
pao: 0.27%
po_kayin: 0.31%
bamar: 1.21%
mon: 0.30%
shan: 1.07%
beik: 30.25%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 16.61%
dawei: 16.71%
pao: 0.14%
po_kayin: 0.16%
bamar: 0.62%
mon: 0.15%
shan: 0.54%
beik: 65.06%
Running with ngram=5 on random sentence 9: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%
Running with ngram=5 on random sentence 10: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%

Processing file: dawei.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 4.55%
mon: 0.01%
shan: 0.00%
pao: 0.00%
rakhine: 93.53%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.86%
bamar: 0.05%

Combined Character and Syllable-based Detection:
beik: 2.28%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 46.77%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 50.93%
bamar: 0.02%
Running with ngram=3 on random sentence 2: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.82%
mon: 0.01%
shan: 0.01%
pao: 0.01%
rakhine: 0.47%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 98.57%
bamar: 0.10%

Combined Character and Syllable-based Detection:
beik: 0.41%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.24%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 99.28%
bamar: 0.05%
Running with ngram=3 on random sentence 3: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.42%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.45%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 98.80%
bamar: 0.32%

Combined Character and Syllable-based Detection:
beik: 0.21%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.22%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.40%
bamar: 0.16%
Running with ngram=3 on random sentence 4: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.08%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.79%
bamar: 0.11%

Combined Character and Syllable-based Detection:
beik: 0.04%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.90%
bamar: 0.05%
Running with ngram=3 on random sentence 5: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.42%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.45%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 98.80%
bamar: 0.32%

Combined Character and Syllable-based Detection:
beik: 0.21%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.22%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.40%
bamar: 0.16%
Running with ngram=3 on random sentence 6: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 13.04%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 86.87%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.03%
bamar: 0.06%

Combined Character and Syllable-based Detection:
beik: 6.52%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 43.43%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 50.01%
bamar: 0.03%
Running with ngram=3 on random sentence 7: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 13.04%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 86.87%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.03%
bamar: 0.06%

Combined Character and Syllable-based Detection:
beik: 6.52%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 43.43%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 50.01%
bamar: 0.03%
Running with ngram=3 on random sentence 8: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 4.55%
mon: 0.01%
shan: 0.00%
pao: 0.00%
rakhine: 93.53%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.86%
bamar: 0.05%

Combined Character and Syllable-based Detection:
beik: 2.28%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 46.77%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 50.93%
bamar: 0.02%
Running with ngram=3 on random sentence 9: ခံဗျားခရီးထွပ်ဟှလား။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 41.76%
mon: 0.00%
shan: 0.00%
pao: 0.02%
rakhine: 15.75%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 42.45%
bamar: 0.02%

Combined Character and Syllable-based Detection:
beik: 20.88%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 7.88%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 71.22%
bamar: 0.01%
Running with ngram=3 on random sentence 10: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.82%
mon: 0.01%
shan: 0.01%
pao: 0.01%
rakhine: 0.47%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 98.57%
bamar: 0.10%

Combined Character and Syllable-based Detection:
beik: 0.41%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.24%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 99.28%
bamar: 0.05%
Running with ngram=4 on full file
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 34.50%
mon: 0.39%
bamar: 0.11%
beik: 55.18%
po_kayin: 0.90%
sgaw_kayin: 0.11%
pao: 0.39%
rakhine: 7.52%
shan: 0.90%

Combined Character and Syllable-based Detection:
dawei: 67.25%
mon: 0.20%
bamar: 0.06%
beik: 27.59%
po_kayin: 0.45%
sgaw_kayin: 0.05%
pao: 0.19%
rakhine: 3.76%
shan: 0.45%
Running with ngram=4 on random sentence 2: ခံဗျားခရီးထွပ်ဟှလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 95.10%
mon: 0.29%
bamar: 0.22%
beik: 0.68%
po_kayin: 0.68%
sgaw_kayin: 0.08%
pao: 0.68%
rakhine: 1.60%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 97.55%
mon: 0.15%
bamar: 0.11%
beik: 0.34%
po_kayin: 0.34%
sgaw_kayin: 0.04%
pao: 0.34%
rakhine: 0.80%
shan: 0.34%
Running with ngram=4 on random sentence 3: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.02%
mon: 0.00%
bamar: 0.16%
beik: 55.90%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 43.92%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 50.01%
mon: 0.00%
bamar: 0.08%
beik: 27.95%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 21.96%
shan: 0.00%
Running with ngram=4 on random sentence 4: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 31.86%
mon: 1.03%
bamar: 0.00%
beik: 50.00%
po_kayin: 0.08%
sgaw_kayin: 0.00%
pao: 0.02%
rakhine: 16.75%
shan: 0.26%

Combined Character and Syllable-based Detection:
dawei: 65.93%
mon: 0.51%
bamar: 0.00%
beik: 25.00%
po_kayin: 0.04%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 8.38%
shan: 0.13%
Running with ngram=4 on random sentence 5: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.02%
mon: 0.00%
bamar: 0.16%
beik: 55.90%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 43.92%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 50.01%
mon: 0.00%
bamar: 0.08%
beik: 27.95%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 21.96%
shan: 0.00%
Running with ngram=4 on random sentence 6: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 34.50%
mon: 0.39%
bamar: 0.11%
beik: 55.18%
po_kayin: 0.90%
sgaw_kayin: 0.11%
pao: 0.39%
rakhine: 7.52%
shan: 0.90%

Combined Character and Syllable-based Detection:
dawei: 67.25%
mon: 0.20%
bamar: 0.06%
beik: 27.59%
po_kayin: 0.45%
sgaw_kayin: 0.05%
pao: 0.19%
rakhine: 3.76%
shan: 0.45%
Running with ngram=4 on random sentence 7: ခံဗျားခရီးထွပ်ဟှလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 95.10%
mon: 0.29%
bamar: 0.22%
beik: 0.68%
po_kayin: 0.68%
sgaw_kayin: 0.08%
pao: 0.68%
rakhine: 1.60%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 97.55%
mon: 0.15%
bamar: 0.11%
beik: 0.34%
po_kayin: 0.34%
sgaw_kayin: 0.04%
pao: 0.34%
rakhine: 0.80%
shan: 0.34%
Running with ngram=4 on random sentence 8: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 87.64%
mon: 0.39%
bamar: 4.90%
beik: 0.92%
po_kayin: 0.89%
sgaw_kayin: 0.89%
pao: 2.73%
rakhine: 0.74%
shan: 0.89%

Combined Character and Syllable-based Detection:
dawei: 93.82%
mon: 0.19%
bamar: 2.45%
beik: 0.46%
po_kayin: 0.45%
sgaw_kayin: 0.45%
pao: 1.37%
rakhine: 0.37%
shan: 0.45%
Running with ngram=4 on random sentence 9: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 87.64%
mon: 0.39%
bamar: 4.90%
beik: 0.92%
po_kayin: 0.89%
sgaw_kayin: 0.89%
pao: 2.73%
rakhine: 0.74%
shan: 0.89%

Combined Character and Syllable-based Detection:
dawei: 93.82%
mon: 0.19%
bamar: 2.45%
beik: 0.46%
po_kayin: 0.45%
sgaw_kayin: 0.45%
pao: 1.37%
rakhine: 0.37%
shan: 0.45%
Running with ngram=4 on random sentence 10: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 79.53%
mon: 1.56%
bamar: 2.04%
beik: 4.91%
po_kayin: 3.59%
sgaw_kayin: 3.59%
pao: 0.96%
rakhine: 0.27%
shan: 3.57%

Combined Character and Syllable-based Detection:
dawei: 89.76%
mon: 0.78%
bamar: 1.02%
beik: 2.45%
po_kayin: 1.80%
sgaw_kayin: 1.80%
pao: 0.48%
rakhine: 0.13%
shan: 1.78%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 1: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 10.55%
rakhine: 0.78%
dawei: 51.26%
pao: 2.82%
po_kayin: 10.55%
bamar: 0.17%
mon: 4.57%
shan: 4.90%
beik: 14.41%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.27%
rakhine: 0.39%
dawei: 75.63%
pao: 1.41%
po_kayin: 5.27%
bamar: 0.08%
mon: 2.28%
shan: 2.45%
beik: 7.20%
Running with ngram=5 on random sentence 2: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 10.55%
rakhine: 0.78%
dawei: 51.26%
pao: 2.82%
po_kayin: 10.55%
bamar: 0.17%
mon: 4.57%
shan: 4.90%
beik: 14.41%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.27%
rakhine: 0.39%
dawei: 75.63%
pao: 1.41%
po_kayin: 5.27%
bamar: 0.08%
mon: 2.28%
shan: 2.45%
beik: 7.20%
Running with ngram=5 on random sentence 3: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 1.05%
dawei: 88.35%
pao: 0.27%
po_kayin: 1.08%
bamar: 0.01%
mon: 0.30%
shan: 3.71%
beik: 5.18%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 0.52%
dawei: 94.18%
pao: 0.13%
po_kayin: 0.54%
bamar: 0.01%
mon: 0.15%
shan: 1.86%
beik: 2.59%
Running with ngram=5 on random sentence 4: ခံဗျားခရီးထွပ်ဟှလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.79%
rakhine: 6.63%
dawei: 77.62%
pao: 2.79%
po_kayin: 2.79%
bamar: 0.57%
mon: 1.21%
shan: 2.79%
beik: 2.79%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.40%
rakhine: 3.31%
dawei: 88.81%
pao: 1.40%
po_kayin: 1.40%
bamar: 0.28%
mon: 0.60%
shan: 1.40%
beik: 1.40%
Running with ngram=5 on random sentence 5: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.91%
rakhine: 0.09%
dawei: 92.65%
pao: 0.07%
po_kayin: 2.25%
bamar: 0.04%
mon: 0.93%
shan: 2.23%
beik: 0.83%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 0.04%
dawei: 96.33%
pao: 0.04%
po_kayin: 1.12%
bamar: 0.02%
mon: 0.47%
shan: 1.11%
beik: 0.42%
Running with ngram=5 on random sentence 6: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.83%
rakhine: 5.86%
dawei: 53.45%
pao: 7.00%
po_kayin: 6.83%
bamar: 1.54%
mon: 2.06%
shan: 6.83%
beik: 9.62%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.41%
rakhine: 2.93%
dawei: 76.72%
pao: 3.50%
po_kayin: 3.41%
bamar: 0.77%
mon: 1.03%
shan: 3.41%
beik: 4.81%
Running with ngram=5 on random sentence 7: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 0.07%
dawei: 88.96%
pao: 0.05%
po_kayin: 0.83%
bamar: 0.00%
mon: 0.09%
shan: 0.38%
beik: 9.57%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 0.04%
dawei: 94.48%
pao: 0.03%
po_kayin: 0.41%
bamar: 0.00%
mon: 0.05%
shan: 0.19%
beik: 4.78%
Running with ngram=5 on random sentence 8: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 0.07%
dawei: 88.96%
pao: 0.05%
po_kayin: 0.83%
bamar: 0.00%
mon: 0.09%
shan: 0.38%
beik: 9.57%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 0.04%
dawei: 94.48%
pao: 0.03%
po_kayin: 0.41%
bamar: 0.00%
mon: 0.05%
shan: 0.19%
beik: 4.78%
Running with ngram=5 on random sentence 9: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 9.76%
rakhine: 9.76%
dawei: 35.99%
pao: 9.76%
po_kayin: 9.76%
bamar: 1.23%
mon: 4.23%
shan: 9.76%
beik: 9.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 4.88%
rakhine: 4.88%
dawei: 68.00%
pao: 4.88%
po_kayin: 4.88%
bamar: 0.61%
mon: 2.11%
shan: 4.88%
beik: 4.88%
Running with ngram=5 on random sentence 10: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 9.76%
rakhine: 9.76%
dawei: 35.99%
pao: 9.76%
po_kayin: 9.76%
bamar: 1.23%
mon: 4.23%
shan: 9.76%
beik: 9.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 4.88%
rakhine: 4.88%
dawei: 68.00%
pao: 4.88%
po_kayin: 4.88%
bamar: 0.61%
mon: 2.11%
shan: 4.88%
beik: 4.88%

Processing file: mon_tst.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 38.04%
mon: 59.24%
shan: 0.83%
pao: 0.20%
rakhine: 0.12%
po_kayin: 1.03%
sgaw_kayin: 0.23%
dawei: 0.19%
bamar: 0.12%

Combined Character and Syllable-based Detection:
beik: 19.02%
mon: 79.62%
shan: 0.41%
pao: 0.10%
rakhine: 0.06%
po_kayin: 0.52%
sgaw_kayin: 0.12%
dawei: 0.09%
bamar: 0.06%
Running with ngram=3 on random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 2: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 4: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 6: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 8: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 9: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.28%
mon: 87.31%
bamar: 0.01%
beik: 3.17%
po_kayin: 1.02%
sgaw_kayin: 0.08%
pao: 0.65%
rakhine: 0.83%
shan: 5.64%

Combined Character and Syllable-based Detection:
dawei: 0.64%
mon: 93.65%
bamar: 0.01%
beik: 1.59%
po_kayin: 0.51%
sgaw_kayin: 0.04%
pao: 0.33%
rakhine: 0.42%
shan: 2.82%
Running with ngram=4 on random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 2: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 6: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 8: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 9: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 10: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.60%
dawei: 2.59%
pao: 0.82%
po_kayin: 0.97%
bamar: 0.02%
mon: 80.41%
shan: 11.43%
beik: 3.01%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.30%
dawei: 1.30%
pao: 0.41%
po_kayin: 0.48%
bamar: 0.01%
mon: 90.20%
shan: 5.72%
beik: 1.50%
Running with ngram=5 on random sentence 1: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 2: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 5: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 6: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 8: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 9: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%

Processing file: mon.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 5.10%
mon: 35.93%
shan: 5.81%
pao: 2.51%
rakhine: 3.15%
po_kayin: 24.94%
sgaw_kayin: 13.85%
dawei: 2.17%
bamar: 6.54%

Combined Character and Syllable-based Detection:
beik: 2.55%
mon: 67.96%
shan: 2.91%
pao: 1.25%
rakhine: 1.58%
po_kayin: 12.47%
sgaw_kayin: 6.93%
dawei: 1.08%
bamar: 3.27%
Running with ngram=3 on random sentence 2: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 9.30%
mon: 90.36%
shan: 0.05%
pao: 0.00%
rakhine: 0.06%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.23%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 4.65%
mon: 95.18%
shan: 0.02%
pao: 0.00%
rakhine: 0.03%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ဗှ်ေဟယျတုဲမာန်ဟာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.19%
mon: 82.34%
shan: 1.85%
pao: 1.50%
rakhine: 1.07%
po_kayin: 1.85%
sgaw_kayin: 1.85%
dawei: 1.85%
bamar: 6.49%

Combined Character and Syllable-based Detection:
beik: 0.59%
mon: 91.17%
shan: 0.93%
pao: 0.75%
rakhine: 0.54%
po_kayin: 0.93%
sgaw_kayin: 0.93%
dawei: 0.93%
bamar: 3.24%
Running with ngram=3 on random sentence 4: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 62.44%
mon: 20.08%
shan: 2.26%
pao: 0.46%
rakhine: 8.50%
po_kayin: 0.66%
sgaw_kayin: 0.08%
dawei: 4.68%
bamar: 0.85%

Combined Character and Syllable-based Detection:
beik: 31.22%
mon: 60.04%
shan: 1.13%
pao: 0.23%
rakhine: 4.25%
po_kayin: 0.33%
sgaw_kayin: 0.04%
dawei: 2.34%
bamar: 0.43%
Running with ngram=3 on random sentence 5: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 62.44%
mon: 20.08%
shan: 2.26%
pao: 0.46%
rakhine: 8.50%
po_kayin: 0.66%
sgaw_kayin: 0.08%
dawei: 4.68%
bamar: 0.85%

Combined Character and Syllable-based Detection:
beik: 31.22%
mon: 60.04%
shan: 1.13%
pao: 0.23%
rakhine: 4.25%
po_kayin: 0.33%
sgaw_kayin: 0.04%
dawei: 2.34%
bamar: 0.43%
Running with ngram=3 on random sentence 6: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.32%
mon: 99.33%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.28%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.16%
mon: 99.67%
shan: 0.03%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.14%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 76.25%
mon: 16.53%
shan: 2.06%
pao: 0.18%
rakhine: 0.36%
po_kayin: 1.00%
sgaw_kayin: 2.61%
dawei: 0.97%
bamar: 0.06%

Combined Character and Syllable-based Detection:
beik: 38.12%
mon: 58.26%
shan: 1.03%
pao: 0.09%
rakhine: 0.18%
po_kayin: 0.50%
sgaw_kayin: 1.30%
dawei: 0.49%
bamar: 0.03%
Running with ngram=3 on random sentence 8: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 9.30%
mon: 90.36%
shan: 0.05%
pao: 0.00%
rakhine: 0.06%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.23%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 4.65%
mon: 95.18%
shan: 0.02%
pao: 0.00%
rakhine: 0.03%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=3 on random sentence 9: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 5.10%
mon: 35.93%
shan: 5.81%
pao: 2.51%
rakhine: 3.15%
po_kayin: 24.94%
sgaw_kayin: 13.85%
dawei: 2.17%
bamar: 6.54%

Combined Character and Syllable-based Detection:
beik: 2.55%
mon: 67.96%
shan: 2.91%
pao: 1.25%
rakhine: 1.58%
po_kayin: 12.47%
sgaw_kayin: 6.93%
dawei: 1.08%
bamar: 3.27%
Running with ngram=3 on random sentence 10: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 76.25%
mon: 16.53%
shan: 2.06%
pao: 0.18%
rakhine: 0.36%
po_kayin: 1.00%
sgaw_kayin: 2.61%
dawei: 0.97%
bamar: 0.06%

Combined Character and Syllable-based Detection:
beik: 38.12%
mon: 58.26%
shan: 1.03%
pao: 0.09%
rakhine: 0.18%
po_kayin: 0.50%
sgaw_kayin: 1.30%
dawei: 0.49%
bamar: 0.03%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 24.19%
bamar: 0.00%
beik: 75.81%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 62.10%
bamar: 0.00%
beik: 37.90%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 33.85%
mon: 52.94%
bamar: 0.00%
beik: 8.69%
po_kayin: 1.68%
sgaw_kayin: 0.01%
pao: 0.99%
rakhine: 0.21%
shan: 1.65%

Combined Character and Syllable-based Detection:
dawei: 16.92%
mon: 76.47%
bamar: 0.00%
beik: 4.34%
po_kayin: 0.84%
sgaw_kayin: 0.00%
pao: 0.49%
rakhine: 0.10%
shan: 0.82%
Running with ngram=4 on random sentence 2: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 6.26%
mon: 79.23%
bamar: 0.35%
beik: 6.58%
po_kayin: 2.99%
sgaw_kayin: 0.14%
pao: 0.74%
rakhine: 0.76%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 3.13%
mon: 89.61%
bamar: 0.17%
beik: 3.29%
po_kayin: 1.49%
sgaw_kayin: 0.07%
pao: 0.37%
rakhine: 0.38%
shan: 1.48%
Running with ngram=4 on random sentence 3: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.03%
mon: 12.08%
bamar: 2.27%
beik: 11.58%
po_kayin: 2.47%
sgaw_kayin: 32.05%
pao: 7.79%
rakhine: 4.91%
shan: 15.81%

Combined Character and Syllable-based Detection:
dawei: 5.51%
mon: 56.04%
bamar: 1.14%
beik: 5.79%
po_kayin: 1.23%
sgaw_kayin: 16.02%
pao: 3.90%
rakhine: 2.46%
shan: 7.91%
Running with ngram=4 on random sentence 4: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.43%
mon: 14.16%
bamar: 0.36%
beik: 19.84%
po_kayin: 14.05%
sgaw_kayin: 2.65%
pao: 5.59%
rakhine: 12.28%
shan: 22.64%

Combined Character and Syllable-based Detection:
dawei: 4.22%
mon: 57.08%
bamar: 0.18%
beik: 9.92%
po_kayin: 7.02%
sgaw_kayin: 1.33%
pao: 2.79%
rakhine: 6.14%
shan: 11.32%
Running with ngram=4 on random sentence 5: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 33.85%
mon: 52.94%
bamar: 0.00%
beik: 8.69%
po_kayin: 1.68%
sgaw_kayin: 0.01%
pao: 0.99%
rakhine: 0.21%
shan: 1.65%

Combined Character and Syllable-based Detection:
dawei: 16.92%
mon: 76.47%
bamar: 0.00%
beik: 4.34%
po_kayin: 0.84%
sgaw_kayin: 0.00%
pao: 0.49%
rakhine: 0.10%
shan: 0.82%
Running with ngram=4 on random sentence 6: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 37.28%
mon: 21.19%
bamar: 0.01%
beik: 19.92%
po_kayin: 2.01%
sgaw_kayin: 0.02%
pao: 0.04%
rakhine: 12.61%
shan: 6.92%

Combined Character and Syllable-based Detection:
dawei: 18.64%
mon: 60.59%
bamar: 0.00%
beik: 9.96%
po_kayin: 1.01%
sgaw_kayin: 0.01%
pao: 0.02%
rakhine: 6.31%
shan: 3.46%
Running with ngram=4 on random sentence 7: ဗှ်ေဟယျတုဲမာန်ဟာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 13.75%
mon: 10.70%
bamar: 2.21%
beik: 8.97%
po_kayin: 13.98%
sgaw_kayin: 13.98%
pao: 13.98%
rakhine: 8.44%
shan: 13.98%

Combined Character and Syllable-based Detection:
dawei: 6.88%
mon: 55.35%
bamar: 1.10%
beik: 4.48%
po_kayin: 6.99%
sgaw_kayin: 6.99%
pao: 6.99%
rakhine: 4.22%
shan: 6.99%
Running with ngram=4 on random sentence 8: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 16.77%
mon: 19.65%
bamar: 0.43%
beik: 17.62%
po_kayin: 8.00%
sgaw_kayin: 0.61%
pao: 1.97%
rakhine: 7.47%
shan: 27.48%

Combined Character and Syllable-based Detection:
dawei: 8.39%
mon: 59.83%
bamar: 0.22%
beik: 8.81%
po_kayin: 4.00%
sgaw_kayin: 0.30%
pao: 0.98%
rakhine: 3.74%
shan: 13.74%
Running with ngram=4 on random sentence 9: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 37.28%
mon: 21.19%
bamar: 0.01%
beik: 19.92%
po_kayin: 2.01%
sgaw_kayin: 0.02%
pao: 0.04%
rakhine: 12.61%
shan: 6.92%

Combined Character and Syllable-based Detection:
dawei: 18.64%
mon: 60.59%
bamar: 0.00%
beik: 9.96%
po_kayin: 1.01%
sgaw_kayin: 0.01%
pao: 0.02%
rakhine: 6.31%
shan: 3.46%
Running with ngram=4 on random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 99.93%
shan: 0.06%
beik: 0.01%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 99.97%
shan: 0.03%
beik: 0.00%
Running with ngram=5 on random sentence 1: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.11%
rakhine: 1.32%
dawei: 9.29%
pao: 0.21%
po_kayin: 11.91%
bamar: 0.01%
mon: 25.45%
shan: 40.94%
beik: 10.77%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 0.66%
dawei: 4.64%
pao: 0.10%
po_kayin: 5.95%
bamar: 0.01%
mon: 62.73%
shan: 20.47%
beik: 5.38%
Running with ngram=5 on random sentence 2: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 3: ဗှ်ေဟယျတုဲမာန်ဟာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 99.97%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 15.28%
rakhine: 1.13%
dawei: 15.28%
pao: 15.28%
po_kayin: 15.28%
bamar: 0.24%
mon: 12.46%
shan: 15.28%
beik: 9.79%

Combined Character and Syllable-based Detection:
sgaw_kayin: 7.64%
rakhine: 0.57%
dawei: 7.64%
pao: 7.64%
po_kayin: 7.64%
bamar: 0.12%
mon: 56.22%
shan: 7.64%
beik: 4.90%
Running with ngram=5 on random sentence 4: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.19%
rakhine: 1.08%
dawei: 20.06%
pao: 3.86%
po_kayin: 4.56%
bamar: 0.23%
mon: 31.33%
shan: 15.55%
beik: 22.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.60%
rakhine: 0.54%
dawei: 10.03%
pao: 1.93%
po_kayin: 2.28%
bamar: 0.11%
mon: 65.67%
shan: 7.77%
beik: 11.07%
Running with ngram=5 on random sentence 5: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.10%
dawei: 9.58%
pao: 2.14%
po_kayin: 5.86%
bamar: 0.00%
mon: 64.86%
shan: 5.76%
beik: 11.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.05%
dawei: 4.79%
pao: 1.07%
po_kayin: 2.93%
bamar: 0.00%
mon: 82.43%
shan: 2.88%
beik: 5.84%
Running with ngram=5 on random sentence 6: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.11%
rakhine: 1.32%
dawei: 9.29%
pao: 0.21%
po_kayin: 11.91%
bamar: 0.01%
mon: 25.45%
shan: 40.94%
beik: 10.77%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 0.66%
dawei: 4.64%
pao: 0.10%
po_kayin: 5.95%
bamar: 0.01%
mon: 62.73%
shan: 20.47%
beik: 5.38%
Running with ngram=5 on random sentence 7: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.06%
rakhine: 0.44%
dawei: 5.00%
pao: 0.42%
po_kayin: 0.54%
bamar: 0.09%
mon: 81.30%
shan: 6.35%
beik: 5.80%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 0.22%
dawei: 2.50%
pao: 0.21%
po_kayin: 0.27%
bamar: 0.05%
mon: 90.65%
shan: 3.18%
beik: 2.90%
Running with ngram=5 on random sentence 8: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.20%
rakhine: 5.10%
dawei: 18.78%
pao: 5.03%
po_kayin: 18.78%
bamar: 2.36%
mon: 10.20%
shan: 18.78%
beik: 18.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.10%
rakhine: 2.55%
dawei: 9.39%
pao: 2.51%
po_kayin: 9.39%
bamar: 1.18%
mon: 55.10%
shan: 9.39%
beik: 9.39%
Running with ngram=5 on random sentence 9: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.19%
rakhine: 1.08%
dawei: 20.06%
pao: 3.86%
po_kayin: 4.56%
bamar: 0.23%
mon: 31.33%
shan: 15.55%
beik: 22.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.60%
rakhine: 0.54%
dawei: 10.03%
pao: 1.93%
po_kayin: 2.28%
bamar: 0.11%
mon: 65.67%
shan: 7.77%
beik: 11.07%
Running with ngram=5 on random sentence 10: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Character-based Detection:
sgaw_kayin: 0.12%
rakhine: 0.12%
dawei: 0.12%
pao: 0.12%
po_kayin: 0.12%
bamar: 0.12%
mon: 99.05%
shan: 0.12%
beik: 0.12%

Syllable-based Detection:
sgaw_kayin: 2.97%
rakhine: 15.76%
dawei: 15.76%
pao: 4.22%
po_kayin: 15.76%
bamar: 1.98%
mon: 12.01%
shan: 15.76%
beik: 15.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.55%
rakhine: 7.94%
dawei: 7.94%
pao: 2.17%
po_kayin: 7.94%
bamar: 1.05%
mon: 55.53%
shan: 7.94%
beik: 7.94%

Processing file: pao.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 94.31%
mon: 0.71%
shan: 0.13%
pao: 3.73%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 1.08%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 47.16%
mon: 0.35%
shan: 0.07%
pao: 51.86%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.54%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 94.31%
mon: 0.71%
shan: 0.13%
pao: 3.73%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 1.08%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 47.16%
mon: 0.35%
shan: 0.07%
pao: 51.86%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.54%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 2.10%
mon: 2.10%
shan: 2.10%
pao: 83.23%
rakhine: 2.10%
po_kayin: 2.10%
sgaw_kayin: 2.10%
dawei: 2.10%
bamar: 2.10%

Combined Character and Syllable-based Detection:
beik: 1.05%
mon: 1.05%
shan: 1.05%
pao: 91.61%
rakhine: 1.05%
po_kayin: 1.05%
sgaw_kayin: 1.05%
dawei: 1.05%
bamar: 1.05%
Running with ngram=3 on random sentence 4: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.68%
mon: 0.00%
shan: 0.00%
pao: 0.32%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.84%
mon: 0.00%
shan: 0.00%
pao: 50.16%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 5: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.06%
mon: 1.28%
shan: 26.95%
pao: 4.06%
rakhine: 6.15%
po_kayin: 0.86%
sgaw_kayin: 44.95%
dawei: 6.22%
bamar: 6.45%

Combined Character and Syllable-based Detection:
beik: 1.53%
mon: 0.64%
shan: 13.48%
pao: 52.03%
rakhine: 3.08%
po_kayin: 0.43%
sgaw_kayin: 22.48%
dawei: 3.11%
bamar: 3.23%
Running with ngram=3 on random sentence 6: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.68%
mon: 0.00%
shan: 0.00%
pao: 0.32%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.84%
mon: 0.00%
shan: 0.00%
pao: 50.16%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 7: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.77%
mon: 0.00%
shan: 0.00%
pao: 0.06%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.17%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.88%
mon: 0.00%
shan: 0.00%
pao: 50.03%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.09%
bamar: 0.00%
Running with ngram=3 on random sentence 8: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 94.31%
mon: 0.71%
shan: 0.13%
pao: 3.73%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 1.08%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 47.16%
mon: 0.35%
shan: 0.07%
pao: 51.86%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.54%
bamar: 0.00%
Running with ngram=3 on random sentence 9: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.39%
mon: 0.01%
shan: 0.01%
pao: 99.57%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.20%
mon: 0.00%
shan: 0.01%
pao: 99.79%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 10: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.77%
mon: 0.00%
shan: 0.00%
pao: 0.06%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.17%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.88%
mon: 0.00%
shan: 0.00%
pao: 50.03%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.09%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 49.43%
mon: 6.81%
bamar: 0.19%
beik: 22.08%
po_kayin: 2.07%
sgaw_kayin: 0.13%
pao: 11.60%
rakhine: 0.74%
shan: 6.97%

Combined Character and Syllable-based Detection:
dawei: 24.71%
mon: 3.41%
bamar: 0.09%
beik: 11.04%
po_kayin: 1.03%
sgaw_kayin: 0.07%
pao: 55.80%
rakhine: 0.37%
shan: 3.48%
Running with ngram=4 on random sentence 2: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 9.10%
mon: 4.53%
bamar: 0.35%
beik: 56.77%
po_kayin: 0.89%
sgaw_kayin: 0.14%
pao: 19.47%
rakhine: 5.73%
shan: 3.02%

Combined Character and Syllable-based Detection:
dawei: 4.55%
mon: 2.26%
bamar: 0.18%
beik: 28.39%
po_kayin: 0.44%
sgaw_kayin: 0.07%
pao: 59.73%
rakhine: 2.87%
shan: 1.51%
Running with ngram=4 on random sentence 3: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 49.43%
mon: 6.81%
bamar: 0.19%
beik: 22.08%
po_kayin: 2.07%
sgaw_kayin: 0.13%
pao: 11.60%
rakhine: 0.74%
shan: 6.97%

Combined Character and Syllable-based Detection:
dawei: 24.71%
mon: 3.41%
bamar: 0.09%
beik: 11.04%
po_kayin: 1.03%
sgaw_kayin: 0.07%
pao: 55.80%
rakhine: 0.37%
shan: 3.48%
Running with ngram=4 on random sentence 4: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 18.89%
mon: 5.91%
bamar: 2.75%
beik: 20.85%
po_kayin: 2.67%
sgaw_kayin: 0.43%
pao: 1.92%
rakhine: 15.10%
shan: 31.48%

Combined Character and Syllable-based Detection:
dawei: 9.45%
mon: 2.95%
bamar: 1.38%
beik: 10.43%
po_kayin: 1.33%
sgaw_kayin: 0.22%
pao: 50.96%
rakhine: 7.55%
shan: 15.74%
Running with ngram=4 on random sentence 5: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.91%
mon: 0.60%
bamar: 0.16%
beik: 2.18%
po_kayin: 0.93%
sgaw_kayin: 0.15%
pao: 92.65%
rakhine: 0.51%
shan: 0.92%

Combined Character and Syllable-based Detection:
dawei: 0.96%
mon: 0.30%
bamar: 0.08%
beik: 1.09%
po_kayin: 0.46%
sgaw_kayin: 0.08%
pao: 96.32%
rakhine: 0.26%
shan: 0.46%
Running with ngram=4 on random sentence 6: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 13.13%
mon: 13.13%
bamar: 7.52%
beik: 13.13%
po_kayin: 13.13%
sgaw_kayin: 13.13%
pao: 3.81%
rakhine: 5.75%
shan: 17.26%

Combined Character and Syllable-based Detection:
dawei: 6.57%
mon: 6.57%
bamar: 3.76%
beik: 6.57%
po_kayin: 6.57%
sgaw_kayin: 6.57%
pao: 51.90%
rakhine: 2.88%
shan: 8.63%
Running with ngram=4 on random sentence 7: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 22.07%
mon: 4.55%
bamar: 1.32%
beik: 10.85%
po_kayin: 3.06%
sgaw_kayin: 31.38%
pao: 1.89%
rakhine: 21.84%
shan: 3.03%

Combined Character and Syllable-based Detection:
dawei: 11.04%
mon: 2.28%
bamar: 0.66%
beik: 5.43%
po_kayin: 1.53%
sgaw_kayin: 15.69%
pao: 50.95%
rakhine: 10.92%
shan: 1.51%
Running with ngram=4 on random sentence 8: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 49.43%
mon: 6.81%
bamar: 0.19%
beik: 22.08%
po_kayin: 2.07%
sgaw_kayin: 0.13%
pao: 11.60%
rakhine: 0.74%
shan: 6.97%

Combined Character and Syllable-based Detection:
dawei: 24.71%
mon: 3.41%
bamar: 0.09%
beik: 11.04%
po_kayin: 1.03%
sgaw_kayin: 0.07%
pao: 55.80%
rakhine: 0.37%
shan: 3.48%
Running with ngram=4 on random sentence 9: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 18.89%
mon: 5.91%
bamar: 2.75%
beik: 20.85%
po_kayin: 2.67%
sgaw_kayin: 0.43%
pao: 1.92%
rakhine: 15.10%
shan: 31.48%

Combined Character and Syllable-based Detection:
dawei: 9.45%
mon: 2.95%
bamar: 1.38%
beik: 10.43%
po_kayin: 1.33%
sgaw_kayin: 0.22%
pao: 50.96%
rakhine: 7.55%
shan: 15.74%
Running with ngram=4 on random sentence 10: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 99.77%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 99.89%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.11%
Running with ngram=5 on random sentence 1: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.16%
dawei: 0.16%
pao: 98.75%
po_kayin: 0.16%
bamar: 0.16%
mon: 0.16%
shan: 0.16%
beik: 0.16%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.08%
dawei: 0.08%
pao: 99.37%
po_kayin: 0.08%
bamar: 0.08%
mon: 0.08%
shan: 0.08%
beik: 0.08%
Running with ngram=5 on random sentence 2: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.16%
dawei: 0.16%
pao: 98.75%
po_kayin: 0.16%
bamar: 0.16%
mon: 0.16%
shan: 0.16%
beik: 0.16%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.08%
dawei: 0.08%
pao: 99.37%
po_kayin: 0.08%
bamar: 0.08%
mon: 0.08%
shan: 0.08%
beik: 0.08%
Running with ngram=5 on random sentence 3: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.63%
rakhine: 3.39%
dawei: 17.08%
pao: 0.88%
po_kayin: 3.89%
bamar: 0.72%
mon: 8.61%
shan: 45.93%
beik: 18.86%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.32%
rakhine: 1.70%
dawei: 8.54%
pao: 50.44%
po_kayin: 1.94%
bamar: 0.36%
mon: 4.31%
shan: 22.97%
beik: 9.43%
Running with ngram=5 on random sentence 4: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.19%
rakhine: 6.66%
dawei: 19.66%
pao: 5.97%
po_kayin: 7.33%
bamar: 0.17%
mon: 16.25%
shan: 7.20%
beik: 35.58%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.59%
rakhine: 3.33%
dawei: 9.83%
pao: 52.98%
po_kayin: 3.67%
bamar: 0.09%
mon: 8.12%
shan: 3.60%
beik: 17.79%
Running with ngram=5 on random sentence 5: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 11.46%
rakhine: 11.46%
dawei: 11.46%
pao: 18.36%
po_kayin: 11.46%
bamar: 1.44%
mon: 11.46%
shan: 11.46%
beik: 11.46%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.73%
rakhine: 5.73%
dawei: 5.73%
pao: 59.18%
po_kayin: 5.73%
bamar: 0.72%
mon: 5.73%
shan: 5.73%
beik: 5.73%
Running with ngram=5 on random sentence 6: နဝ်ꩻနဝ်ꩻနာꩻတအွဉ်ႏဖွို့ꩻတဝ်းဟောင်းတွမ်ႏအလင်တဗာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.92%
rakhine: 2.17%
dawei: 24.98%
pao: 6.59%
po_kayin: 5.68%
bamar: 0.13%
mon: 12.59%
shan: 19.36%
beik: 27.57%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 1.09%
dawei: 12.49%
pao: 53.29%
po_kayin: 2.84%
bamar: 0.07%
mon: 6.30%
shan: 9.68%
beik: 13.79%
Running with ngram=5 on random sentence 7: ဝွေꩻမူႏတတောင်ချာတဝ်းဒွုမ်ပါꩻမုဲင်ꩻမုဲင်ꩻ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 13.84%
rakhine: 13.84%
dawei: 13.84%
pao: 1.42%
po_kayin: 13.84%
bamar: 1.74%
mon: 13.84%
shan: 13.84%
beik: 13.84%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.92%
rakhine: 6.92%
dawei: 6.92%
pao: 50.71%
po_kayin: 6.92%
bamar: 0.87%
mon: 6.92%
shan: 6.92%
beik: 6.92%
Running with ngram=5 on random sentence 8: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.16%
dawei: 0.16%
pao: 98.75%
po_kayin: 0.16%
bamar: 0.16%
mon: 0.16%
shan: 0.16%
beik: 0.16%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.08%
dawei: 0.08%
pao: 99.37%
po_kayin: 0.08%
bamar: 0.08%
mon: 0.08%
shan: 0.08%
beik: 0.08%
Running with ngram=5 on random sentence 9: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 11.46%
rakhine: 11.46%
dawei: 11.46%
pao: 18.36%
po_kayin: 11.46%
bamar: 1.44%
mon: 11.46%
shan: 11.46%
beik: 11.46%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.73%
rakhine: 5.73%
dawei: 5.73%
pao: 59.18%
po_kayin: 5.73%
bamar: 0.72%
mon: 5.73%
shan: 5.73%
beik: 5.73%
Running with ngram=5 on random sentence 10: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.28%
rakhine: 5.26%
dawei: 21.48%
pao: 2.78%
po_kayin: 16.80%
bamar: 0.44%
mon: 10.83%
shan: 16.65%
beik: 24.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.64%
rakhine: 2.63%
dawei: 10.74%
pao: 51.39%
po_kayin: 8.40%
bamar: 0.22%
mon: 5.41%
shan: 8.32%
beik: 12.24%

Processing file: po_kayin.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.12%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 99.87%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.06%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 99.94%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 3: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.87%
mon: 0.01%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.05%
sgaw_kayin: 0.00%
dawei: 0.02%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.93%
mon: 0.00%
shan: 0.02%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.03%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 4: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.07%
mon: 0.01%
shan: 0.02%
pao: 0.00%
rakhine: 0.01%
po_kayin: 98.86%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.54%
mon: 0.01%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 99.43%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 5: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.87%
mon: 0.01%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.05%
sgaw_kayin: 0.00%
dawei: 0.02%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.93%
mon: 0.00%
shan: 0.02%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.03%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 89.88%
mon: 0.87%
shan: 2.00%
pao: 0.14%
rakhine: 0.54%
po_kayin: 4.85%
sgaw_kayin: 0.23%
dawei: 1.22%
bamar: 0.25%

Combined Character and Syllable-based Detection:
beik: 44.94%
mon: 0.43%
shan: 1.00%
pao: 0.07%
rakhine: 0.27%
po_kayin: 52.43%
sgaw_kayin: 0.12%
dawei: 0.61%
bamar: 0.13%
Running with ngram=3 on random sentence 8: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 68.11%
mon: 0.57%
shan: 0.82%
pao: 0.06%
rakhine: 11.57%
po_kayin: 15.89%
sgaw_kayin: 2.13%
dawei: 0.50%
bamar: 0.35%

Combined Character and Syllable-based Detection:
beik: 34.05%
mon: 0.29%
shan: 0.41%
pao: 0.03%
rakhine: 5.78%
po_kayin: 57.94%
sgaw_kayin: 1.06%
dawei: 0.25%
bamar: 0.18%
Running with ngram=3 on random sentence 9: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 68.11%
mon: 0.57%
shan: 0.82%
pao: 0.06%
rakhine: 11.57%
po_kayin: 15.89%
sgaw_kayin: 2.13%
dawei: 0.50%
bamar: 0.35%

Combined Character and Syllable-based Detection:
beik: 34.05%
mon: 0.29%
shan: 0.41%
pao: 0.03%
rakhine: 5.78%
po_kayin: 57.94%
sgaw_kayin: 1.06%
dawei: 0.25%
bamar: 0.18%
Running with ngram=3 on random sentence 10: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 12.12%
mon: 0.57%
bamar: 0.00%
beik: 37.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 49.61%

Combined Character and Syllable-based Detection:
dawei: 6.06%
mon: 0.28%
bamar: 0.00%
beik: 18.85%
po_kayin: 50.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 24.81%
Running with ngram=4 on random sentence 1: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 19.17%
mon: 13.61%
bamar: 3.95%
beik: 20.14%
po_kayin: 0.48%
sgaw_kayin: 0.43%
pao: 2.25%
rakhine: 8.54%
shan: 31.42%

Combined Character and Syllable-based Detection:
dawei: 9.59%
mon: 6.81%
bamar: 1.97%
beik: 10.07%
po_kayin: 50.24%
sgaw_kayin: 0.22%
pao: 1.13%
rakhine: 4.27%
shan: 15.71%
Running with ngram=4 on random sentence 2: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 30.68%
mon: 17.68%
bamar: 0.27%
beik: 35.58%
po_kayin: 0.52%
sgaw_kayin: 0.22%
pao: 1.12%
rakhine: 2.71%
shan: 11.23%

Combined Character and Syllable-based Detection:
dawei: 15.34%
mon: 8.84%
bamar: 0.13%
beik: 17.79%
po_kayin: 50.26%
sgaw_kayin: 0.11%
pao: 0.56%
rakhine: 1.36%
shan: 5.61%
Running with ngram=4 on random sentence 3: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.67%
mon: 2.61%
bamar: 1.97%
beik: 3.86%
po_kayin: 79.11%
sgaw_kayin: 0.70%
pao: 0.43%
rakhine: 1.64%
shan: 6.02%

Combined Character and Syllable-based Detection:
dawei: 1.84%
mon: 1.30%
bamar: 0.98%
beik: 1.93%
po_kayin: 89.55%
sgaw_kayin: 0.35%
pao: 0.22%
rakhine: 0.82%
shan: 3.01%
Running with ngram=4 on random sentence 4: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 30.68%
mon: 17.68%
bamar: 0.27%
beik: 35.58%
po_kayin: 0.52%
sgaw_kayin: 0.22%
pao: 1.12%
rakhine: 2.71%
shan: 11.23%

Combined Character and Syllable-based Detection:
dawei: 15.34%
mon: 8.84%
bamar: 0.13%
beik: 17.79%
po_kayin: 50.26%
sgaw_kayin: 0.11%
pao: 0.56%
rakhine: 1.36%
shan: 5.61%
Running with ngram=4 on random sentence 5: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 23.58%
mon: 16.74%
bamar: 4.85%
beik: 24.77%
po_kayin: 1.13%
sgaw_kayin: 4.53%
pao: 2.77%
rakhine: 10.50%
shan: 11.14%

Combined Character and Syllable-based Detection:
dawei: 11.79%
mon: 8.37%
bamar: 2.43%
beik: 12.38%
po_kayin: 50.56%
sgaw_kayin: 2.26%
pao: 1.38%
rakhine: 5.25%
shan: 5.57%
Running with ngram=4 on random sentence 6: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 30.68%
mon: 17.68%
bamar: 0.27%
beik: 35.58%
po_kayin: 0.52%
sgaw_kayin: 0.22%
pao: 1.12%
rakhine: 2.71%
shan: 11.23%

Combined Character and Syllable-based Detection:
dawei: 15.34%
mon: 8.84%
bamar: 0.13%
beik: 17.79%
po_kayin: 50.26%
sgaw_kayin: 0.11%
pao: 0.56%
rakhine: 1.36%
shan: 5.61%
Running with ngram=4 on random sentence 7: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.34%
mon: 12.31%
bamar: 9.29%
beik: 18.22%
po_kayin: 1.34%
sgaw_kayin: 3.33%
pao: 2.04%
rakhine: 7.72%
shan: 28.42%

Combined Character and Syllable-based Detection:
dawei: 8.67%
mon: 6.16%
bamar: 4.64%
beik: 9.11%
po_kayin: 50.67%
sgaw_kayin: 1.66%
pao: 1.02%
rakhine: 3.86%
shan: 14.21%
Running with ngram=4 on random sentence 8: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.34%
mon: 12.31%
bamar: 9.29%
beik: 18.22%
po_kayin: 1.34%
sgaw_kayin: 3.33%
pao: 2.04%
rakhine: 7.72%
shan: 28.42%

Combined Character and Syllable-based Detection:
dawei: 8.67%
mon: 6.16%
bamar: 4.64%
beik: 9.11%
po_kayin: 50.67%
sgaw_kayin: 1.66%
pao: 1.02%
rakhine: 3.86%
shan: 14.21%
Running with ngram=4 on random sentence 9: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 9.81%
mon: 3.51%
bamar: 0.22%
beik: 11.37%
po_kayin: 30.66%
sgaw_kayin: 0.07%
pao: 0.36%
rakhine: 0.87%
shan: 43.14%

Combined Character and Syllable-based Detection:
dawei: 4.90%
mon: 1.75%
bamar: 0.11%
beik: 5.69%
po_kayin: 65.33%
sgaw_kayin: 0.03%
pao: 0.18%
rakhine: 0.43%
shan: 21.57%
Running with ngram=4 on random sentence 10: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.67%
mon: 2.61%
bamar: 1.97%
beik: 3.86%
po_kayin: 79.11%
sgaw_kayin: 0.70%
pao: 0.43%
rakhine: 1.64%
shan: 6.02%

Combined Character and Syllable-based Detection:
dawei: 1.84%
mon: 1.30%
bamar: 0.98%
beik: 1.93%
po_kayin: 89.55%
sgaw_kayin: 0.35%
pao: 0.22%
rakhine: 0.82%
shan: 3.01%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 15.38%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.18%
shan: 38.91%
beik: 45.53%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 7.69%
pao: 0.00%
po_kayin: 50.00%
bamar: 0.00%
mon: 0.09%
shan: 19.45%
beik: 22.77%
Running with ngram=5 on random sentence 1: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.62%
rakhine: 8.63%
dawei: 16.71%
pao: 0.86%
po_kayin: 0.66%
bamar: 0.71%
mon: 8.42%
shan: 44.94%
beik: 18.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.31%
rakhine: 4.31%
dawei: 8.36%
pao: 0.43%
po_kayin: 50.33%
bamar: 0.35%
mon: 4.21%
shan: 22.47%
beik: 9.22%
Running with ngram=5 on random sentence 2: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.62%
rakhine: 8.63%
dawei: 16.71%
pao: 0.86%
po_kayin: 0.66%
bamar: 0.71%
mon: 8.42%
shan: 44.94%
beik: 18.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.31%
rakhine: 4.31%
dawei: 8.36%
pao: 0.43%
po_kayin: 50.33%
bamar: 0.35%
mon: 4.21%
shan: 22.47%
beik: 9.22%
Running with ngram=5 on random sentence 3: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 4.49%
rakhine: 10.41%
dawei: 23.37%
pao: 2.74%
po_kayin: 2.00%
bamar: 4.81%
mon: 16.59%
shan: 11.04%
beik: 24.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 2.24%
rakhine: 5.20%
dawei: 11.68%
pao: 1.37%
po_kayin: 51.00%
bamar: 2.41%
mon: 8.29%
shan: 5.52%
beik: 12.27%
Running with ngram=5 on random sentence 4: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.23%
rakhine: 7.48%
dawei: 16.80%
pao: 1.97%
po_kayin: 9.95%
bamar: 3.46%
mon: 11.92%
shan: 27.54%
beik: 17.65%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.61%
rakhine: 3.74%
dawei: 8.40%
pao: 0.99%
po_kayin: 54.97%
bamar: 1.73%
mon: 5.96%
shan: 13.77%
beik: 8.82%
Running with ngram=5 on random sentence 5: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 5.73%
dawei: 11.11%
pao: 0.57%
po_kayin: 0.17%
bamar: 0.06%
mon: 40.16%
shan: 29.86%
beik: 12.26%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 2.87%
dawei: 5.55%
pao: 0.29%
po_kayin: 50.09%
bamar: 0.03%
mon: 20.08%
shan: 14.93%
beik: 6.13%
Running with ngram=5 on random sentence 6: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.58%
rakhine: 8.31%
dawei: 18.65%
pao: 2.19%
po_kayin: 0.01%
bamar: 3.84%
mon: 13.24%
shan: 30.58%
beik: 19.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.79%
rakhine: 4.15%
dawei: 9.33%
pao: 1.09%
po_kayin: 50.01%
bamar: 1.92%
mon: 6.62%
shan: 15.29%
beik: 9.80%
Running with ngram=5 on random sentence 7: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.57%
rakhine: 5.24%
dawei: 26.39%
pao: 1.36%
po_kayin: 8.99%
bamar: 1.12%
mon: 5.76%
shan: 20.45%
beik: 29.12%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.78%
rakhine: 2.62%
dawei: 13.19%
pao: 0.68%
po_kayin: 54.50%
bamar: 0.56%
mon: 2.88%
shan: 10.23%
beik: 14.56%
Running with ngram=5 on random sentence 8: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Character-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.01%
dawei: 0.01%
pao: 0.01%
po_kayin: 99.95%
bamar: 0.01%
mon: 0.01%
shan: 0.01%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 1.83%
rakhine: 15.62%
dawei: 15.62%
pao: 4.18%
po_kayin: 0.25%
bamar: 15.62%
mon: 15.62%
shan: 15.62%
beik: 15.62%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.92%
rakhine: 7.81%
dawei: 7.81%
pao: 2.09%
po_kayin: 50.10%
bamar: 7.81%
mon: 7.81%
shan: 7.81%
beik: 7.81%
Running with ngram=5 on random sentence 9: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 5.73%
dawei: 11.11%
pao: 0.57%
po_kayin: 0.17%
bamar: 0.06%
mon: 40.16%
shan: 29.86%
beik: 12.26%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 2.87%
dawei: 5.55%
pao: 0.29%
po_kayin: 50.09%
bamar: 0.03%
mon: 20.08%
shan: 14.93%
beik: 6.13%
Running with ngram=5 on random sentence 10: ဆီၫ့မီၪ့ဆၧကဲၪခိၬယဆီၫ့မီၪ့ဘီၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 4.49%
rakhine: 10.41%
dawei: 23.37%
pao: 2.74%
po_kayin: 2.00%
bamar: 4.81%
mon: 16.59%
shan: 11.04%
beik: 24.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 2.24%
rakhine: 5.20%
dawei: 11.68%
pao: 1.37%
po_kayin: 51.00%
bamar: 2.41%
mon: 8.29%
shan: 5.52%
beik: 12.27%

Processing file: rakhine.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.52%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 26.84%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 72.63%
bamar: 0.01%

Combined Character and Syllable-based Detection:
beik: 0.26%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 63.42%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 36.32%
bamar: 0.00%
Running with ngram=3 on random sentence 2: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
beik: 0.48%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.41%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.12%

Syllable-based Detection:
beik: 2.16%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 97.40%
bamar: 0.44%

Combined Character and Syllable-based Detection:
beik: 1.32%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 49.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 48.70%
bamar: 0.28%
Running with ngram=3 on random sentence 3: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.99%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 92.34%
mon: 0.12%
shan: 0.11%
pao: 1.36%
rakhine: 0.23%
po_kayin: 0.03%
sgaw_kayin: 0.11%
dawei: 5.48%
bamar: 0.22%

Combined Character and Syllable-based Detection:
beik: 46.17%
mon: 0.06%
shan: 0.05%
pao: 0.68%
rakhine: 50.11%
po_kayin: 0.02%
sgaw_kayin: 0.05%
dawei: 2.74%
bamar: 0.11%
Running with ngram=3 on random sentence 4: မင်းမိန်းစရာမလိုပါ။
Character-based Detection:
beik: 0.13%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.63%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.24%

Syllable-based Detection:
beik: 67.31%
mon: 12.08%
shan: 0.15%
pao: 2.53%
rakhine: 10.47%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 6.45%
bamar: 1.01%

Combined Character and Syllable-based Detection:
beik: 33.72%
mon: 6.04%
shan: 0.08%
pao: 1.26%
rakhine: 55.05%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 3.23%
bamar: 0.62%
Running with ngram=3 on random sentence 5: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
beik: 0.48%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.41%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.12%

Syllable-based Detection:
beik: 2.16%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 97.40%
bamar: 0.44%

Combined Character and Syllable-based Detection:
beik: 1.32%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 49.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 48.70%
bamar: 0.28%
Running with ngram=3 on random sentence 6: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.52%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 26.84%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 72.63%
bamar: 0.01%

Combined Character and Syllable-based Detection:
beik: 0.26%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 63.42%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 36.32%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ဆူပြီးရီကိုသောက်သင့်ရေ။
Character-based Detection:
beik: 10.03%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 79.62%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 10.35%

Syllable-based Detection:
beik: 60.86%
mon: 0.13%
shan: 0.06%
pao: 6.41%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.01%
dawei: 18.22%
bamar: 14.27%

Combined Character and Syllable-based Detection:
beik: 35.45%
mon: 0.07%
shan: 0.03%
pao: 3.21%
rakhine: 39.82%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 9.11%
bamar: 12.31%
Running with ngram=3 on random sentence 8: ဆူပြီးရီကိုသောက်သင့်ရေ။
Character-based Detection:
beik: 10.03%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 79.62%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 10.35%

Syllable-based Detection:
beik: 60.86%
mon: 0.13%
shan: 0.06%
pao: 6.41%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.01%
dawei: 18.22%
bamar: 14.27%

Combined Character and Syllable-based Detection:
beik: 35.45%
mon: 0.07%
shan: 0.03%
pao: 3.21%
rakhine: 39.82%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 9.11%
bamar: 12.31%
Running with ngram=3 on random sentence 9: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.99%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 92.34%
mon: 0.12%
shan: 0.11%
pao: 1.36%
rakhine: 0.23%
po_kayin: 0.03%
sgaw_kayin: 0.11%
dawei: 5.48%
bamar: 0.22%

Combined Character and Syllable-based Detection:
beik: 46.17%
mon: 0.06%
shan: 0.05%
pao: 0.68%
rakhine: 50.11%
po_kayin: 0.02%
sgaw_kayin: 0.05%
dawei: 2.74%
bamar: 0.11%
Running with ngram=3 on random sentence 10: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
beik: 1.93%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 97.13%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.94%

Syllable-based Detection:
beik: 32.60%
mon: 0.02%
shan: 0.01%
pao: 0.04%
rakhine: 66.63%
po_kayin: 0.01%
sgaw_kayin: 0.04%
dawei: 0.07%
bamar: 0.57%

Combined Character and Syllable-based Detection:
beik: 17.26%
mon: 0.01%
shan: 0.01%
pao: 0.02%
rakhine: 81.88%
po_kayin: 0.01%
sgaw_kayin: 0.02%
dawei: 0.04%
bamar: 0.76%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 50.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=4 on random sentence 2: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 4.40%
mon: 0.11%
bamar: 1.84%
beik: 93.52%
po_kayin: 0.03%
sgaw_kayin: 0.03%
pao: 0.03%
rakhine: 0.03%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 2.20%
mon: 0.06%
bamar: 0.92%
beik: 46.76%
po_kayin: 0.01%
sgaw_kayin: 0.01%
pao: 0.02%
rakhine: 50.01%
shan: 0.00%
Running with ngram=4 on random sentence 3: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.57%
mon: 0.20%
bamar: 0.01%
beik: 97.77%
po_kayin: 0.05%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.03%
shan: 0.34%

Combined Character and Syllable-based Detection:
dawei: 0.79%
mon: 0.10%
bamar: 0.00%
beik: 48.88%
po_kayin: 0.02%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 50.02%
shan: 0.17%
Running with ngram=4 on random sentence 4: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.13%
mon: 0.00%
bamar: 0.01%
beik: 99.86%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.06%
mon: 0.00%
bamar: 0.00%
beik: 49.93%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 50.00%
shan: 0.00%
Running with ngram=4 on random sentence 5: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 5.41%
mon: 2.51%
bamar: 0.08%
beik: 77.46%
po_kayin: 2.96%
sgaw_kayin: 0.35%
pao: 0.54%
rakhine: 7.74%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 2.70%
mon: 1.26%
bamar: 0.04%
beik: 38.73%
po_kayin: 1.48%
sgaw_kayin: 0.17%
pao: 0.27%
rakhine: 53.87%
shan: 1.48%
Running with ngram=4 on random sentence 6: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=4 on random sentence 7: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.02%
beik: 23.37%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 76.61%
shan: 0.00%

Syllable-based Detection:
dawei: 6.60%
mon: 2.83%
bamar: 0.01%
beik: 89.51%
po_kayin: 0.20%
sgaw_kayin: 0.00%
pao: 0.02%
rakhine: 0.15%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 3.30%
mon: 1.41%
bamar: 0.02%
beik: 56.44%
po_kayin: 0.10%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 38.38%
shan: 0.34%
Running with ngram=4 on random sentence 8: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 4.40%
mon: 0.11%
bamar: 1.84%
beik: 93.52%
po_kayin: 0.03%
sgaw_kayin: 0.03%
pao: 0.03%
rakhine: 0.03%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 2.20%
mon: 0.06%
bamar: 0.92%
beik: 46.76%
po_kayin: 0.01%
sgaw_kayin: 0.01%
pao: 0.02%
rakhine: 50.01%
shan: 0.00%
Running with ngram=4 on random sentence 9: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.57%
mon: 0.20%
bamar: 0.01%
beik: 97.77%
po_kayin: 0.05%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.03%
shan: 0.34%

Combined Character and Syllable-based Detection:
dawei: 0.79%
mon: 0.10%
bamar: 0.00%
beik: 48.88%
po_kayin: 0.02%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 50.02%
shan: 0.17%
Running with ngram=4 on random sentence 10: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 50.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 50.00%
Running with ngram=5 on random sentence 1: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 1.36%
dawei: 30.88%
pao: 0.02%
po_kayin: 9.29%
bamar: 0.00%
mon: 1.73%
shan: 14.57%
beik: 42.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 50.68%
dawei: 15.44%
pao: 0.01%
po_kayin: 4.64%
bamar: 0.00%
mon: 0.87%
shan: 7.28%
beik: 21.07%
Running with ngram=5 on random sentence 2: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.82%
rakhine: 9.71%
dawei: 7.40%
pao: 2.34%
po_kayin: 32.64%
bamar: 0.20%
mon: 2.65%
shan: 32.64%
beik: 8.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.91%
rakhine: 54.86%
dawei: 3.70%
pao: 1.17%
po_kayin: 16.32%
bamar: 0.10%
mon: 1.32%
shan: 16.32%
beik: 4.29%
Running with ngram=5 on random sentence 3: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.82%
rakhine: 9.71%
dawei: 7.40%
pao: 2.34%
po_kayin: 32.64%
bamar: 0.20%
mon: 2.65%
shan: 32.64%
beik: 8.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.91%
rakhine: 54.86%
dawei: 3.70%
pao: 1.17%
po_kayin: 16.32%
bamar: 0.10%
mon: 1.32%
shan: 16.32%
beik: 4.29%
Running with ngram=5 on random sentence 4: ဆူပြီးရီကိုသောက်သင့်ရေ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 4.27%
mon: 0.00%
shan: 0.00%
beik: 95.73%

Syllable-based Detection:
sgaw_kayin: 9.22%
rakhine: 3.64%
dawei: 3.43%
pao: 1.06%
po_kayin: 9.22%
bamar: 8.00%
mon: 1.73%
shan: 9.22%
beik: 54.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 4.61%
rakhine: 1.82%
dawei: 1.71%
pao: 0.53%
po_kayin: 4.61%
bamar: 6.14%
mon: 0.86%
shan: 4.61%
beik: 75.10%
Running with ngram=5 on random sentence 5: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.89%
rakhine: 2.22%
dawei: 15.05%
pao: 2.90%
po_kayin: 5.52%
bamar: 0.02%
mon: 7.00%
shan: 40.47%
beik: 25.93%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 51.11%
dawei: 7.53%
pao: 1.45%
po_kayin: 2.76%
bamar: 0.01%
mon: 3.50%
shan: 20.23%
beik: 12.97%
Running with ngram=5 on random sentence 6: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.82%
rakhine: 9.71%
dawei: 7.40%
pao: 2.34%
po_kayin: 32.64%
bamar: 0.20%
mon: 2.65%
shan: 32.64%
beik: 8.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.91%
rakhine: 54.86%
dawei: 3.70%
pao: 1.17%
po_kayin: 16.32%
bamar: 0.10%
mon: 1.32%
shan: 16.32%
beik: 4.29%
Running with ngram=5 on random sentence 7: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 1.36%
dawei: 30.88%
pao: 0.02%
po_kayin: 9.29%
bamar: 0.00%
mon: 1.73%
shan: 14.57%
beik: 42.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 50.68%
dawei: 15.44%
pao: 0.01%
po_kayin: 4.64%
bamar: 0.00%
mon: 0.87%
shan: 7.28%
beik: 21.07%
Running with ngram=5 on random sentence 8: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 40.75%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 59.25%

Syllable-based Detection:
sgaw_kayin: 0.57%
rakhine: 4.04%
dawei: 9.34%
pao: 2.95%
po_kayin: 41.19%
bamar: 2.54%
mon: 5.39%
shan: 11.87%
beik: 22.11%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.28%
rakhine: 22.39%
dawei: 4.67%
pao: 1.48%
po_kayin: 20.60%
bamar: 1.27%
mon: 2.69%
shan: 5.94%
beik: 40.68%
Running with ngram=5 on random sentence 9: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 1.36%
dawei: 30.88%
pao: 0.02%
po_kayin: 9.29%
bamar: 0.00%
mon: 1.73%
shan: 14.57%
beik: 42.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 50.68%
dawei: 15.44%
pao: 0.01%
po_kayin: 4.64%
bamar: 0.00%
mon: 0.87%
shan: 7.28%
beik: 21.07%
Running with ngram=5 on random sentence 10: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.89%
rakhine: 2.22%
dawei: 15.05%
pao: 2.90%
po_kayin: 5.52%
bamar: 0.02%
mon: 7.00%
shan: 40.47%
beik: 25.93%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 51.11%
dawei: 7.53%
pao: 1.45%
po_kayin: 2.76%
bamar: 0.01%
mon: 3.50%
shan: 20.23%
beik: 12.97%

Processing file: sgaw_kayin.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.46%
mon: 0.90%
shan: 2.08%
pao: 0.15%
rakhine: 0.57%
po_kayin: 0.28%
sgaw_kayin: 1.01%
dawei: 1.27%
bamar: 0.26%

Combined Character and Syllable-based Detection:
beik: 46.73%
mon: 0.45%
shan: 1.04%
pao: 0.07%
rakhine: 0.28%
po_kayin: 0.14%
sgaw_kayin: 50.51%
dawei: 0.64%
bamar: 0.13%
Running with ngram=3 on random sentence 3: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.61%
mon: 0.03%
shan: 0.11%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 98.69%
dawei: 0.54%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.31%
mon: 0.02%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 99.35%
dawei: 0.27%
bamar: 0.00%
Running with ngram=3 on random sentence 4: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.46%
mon: 0.90%
shan: 2.08%
pao: 0.15%
rakhine: 0.57%
po_kayin: 0.28%
sgaw_kayin: 1.01%
dawei: 1.27%
bamar: 0.26%

Combined Character and Syllable-based Detection:
beik: 46.73%
mon: 0.45%
shan: 1.04%
pao: 0.07%
rakhine: 0.28%
po_kayin: 0.14%
sgaw_kayin: 50.51%
dawei: 0.64%
bamar: 0.13%
Running with ngram=3 on random sentence 5: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 52.79%
mon: 0.36%
shan: 0.05%
pao: 0.02%
rakhine: 0.02%
po_kayin: 0.01%
sgaw_kayin: 46.28%
dawei: 0.46%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 26.39%
mon: 0.18%
shan: 0.03%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 73.14%
dawei: 0.23%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.97%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.03%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.01%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 7: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 22.19%
mon: 31.84%
shan: 1.00%
pao: 0.25%
rakhine: 1.52%
po_kayin: 1.01%
sgaw_kayin: 27.43%
dawei: 14.34%
bamar: 0.43%

Combined Character and Syllable-based Detection:
beik: 11.10%
mon: 15.92%
shan: 0.50%
pao: 0.12%
rakhine: 0.76%
po_kayin: 0.50%
sgaw_kayin: 63.71%
dawei: 7.17%
bamar: 0.22%
Running with ngram=3 on random sentence 8: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 82.28%
mon: 0.04%
shan: 0.05%
pao: 0.28%
rakhine: 0.11%
po_kayin: 0.10%
sgaw_kayin: 0.36%
dawei: 16.78%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 41.14%
mon: 0.02%
shan: 0.02%
pao: 0.14%
rakhine: 0.05%
po_kayin: 0.05%
sgaw_kayin: 50.18%
dawei: 8.39%
bamar: 0.00%
Running with ngram=3 on random sentence 9: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 22.19%
mon: 31.84%
shan: 1.00%
pao: 0.25%
rakhine: 1.52%
po_kayin: 1.01%
sgaw_kayin: 27.43%
dawei: 14.34%
bamar: 0.43%

Combined Character and Syllable-based Detection:
beik: 11.10%
mon: 15.92%
shan: 0.50%
pao: 0.12%
rakhine: 0.76%
po_kayin: 0.50%
sgaw_kayin: 63.71%
dawei: 7.17%
bamar: 0.22%
Running with ngram=3 on random sentence 10: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 82.28%
mon: 0.04%
shan: 0.05%
pao: 0.28%
rakhine: 0.11%
po_kayin: 0.10%
sgaw_kayin: 0.36%
dawei: 16.78%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 41.14%
mon: 0.02%
shan: 0.02%
pao: 0.14%
rakhine: 0.05%
po_kayin: 0.05%
sgaw_kayin: 50.18%
dawei: 8.39%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 99.73%
mon: 0.00%
bamar: 0.00%
beik: 0.27%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 49.87%
mon: 0.00%
bamar: 0.00%
beik: 0.13%
po_kayin: 0.00%
sgaw_kayin: 50.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.74%
mon: 12.59%
bamar: 9.50%
beik: 18.64%
po_kayin: 2.46%
sgaw_kayin: 0.02%
pao: 2.08%
rakhine: 7.90%
shan: 29.06%

Combined Character and Syllable-based Detection:
dawei: 8.87%
mon: 6.30%
bamar: 4.75%
beik: 9.32%
po_kayin: 1.23%
sgaw_kayin: 50.01%
pao: 1.04%
rakhine: 3.95%
shan: 14.53%
Running with ngram=4 on random sentence 2: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 62.28%
mon: 3.02%
bamar: 0.02%
beik: 30.70%
po_kayin: 0.28%
sgaw_kayin: 0.00%
pao: 1.32%
rakhine: 0.42%
shan: 1.96%

Combined Character and Syllable-based Detection:
dawei: 31.14%
mon: 1.51%
bamar: 0.01%
beik: 15.35%
po_kayin: 0.14%
sgaw_kayin: 50.00%
pao: 0.66%
rakhine: 0.21%
shan: 0.98%
Running with ngram=4 on random sentence 3: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 24.89%
mon: 2.12%
bamar: 0.00%
beik: 19.77%
po_kayin: 0.13%
sgaw_kayin: 35.09%
pao: 0.09%
rakhine: 0.58%
shan: 17.34%

Combined Character and Syllable-based Detection:
dawei: 12.44%
mon: 1.06%
bamar: 0.00%
beik: 9.88%
po_kayin: 0.06%
sgaw_kayin: 67.54%
pao: 0.05%
rakhine: 0.29%
shan: 8.67%
Running with ngram=4 on random sentence 4: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.59%
mon: 12.16%
bamar: 3.53%
beik: 17.99%
po_kayin: 8.17%
sgaw_kayin: 11.61%
pao: 3.24%
rakhine: 7.63%
shan: 8.09%

Combined Character and Syllable-based Detection:
dawei: 13.80%
mon: 6.08%
bamar: 1.76%
beik: 9.00%
po_kayin: 4.08%
sgaw_kayin: 55.80%
pao: 1.62%
rakhine: 3.81%
shan: 4.05%
Running with ngram=4 on random sentence 5: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.74%
mon: 12.59%
bamar: 9.50%
beik: 18.64%
po_kayin: 2.46%
sgaw_kayin: 0.02%
pao: 2.08%
rakhine: 7.90%
shan: 29.06%

Combined Character and Syllable-based Detection:
dawei: 8.87%
mon: 6.30%
bamar: 4.75%
beik: 9.32%
po_kayin: 1.23%
sgaw_kayin: 50.01%
pao: 1.04%
rakhine: 3.95%
shan: 14.53%
Running with ngram=4 on random sentence 6: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.59%
mon: 12.16%
bamar: 3.53%
beik: 17.99%
po_kayin: 8.17%
sgaw_kayin: 11.61%
pao: 3.24%
rakhine: 7.63%
shan: 8.09%

Combined Character and Syllable-based Detection:
dawei: 13.80%
mon: 6.08%
bamar: 1.76%
beik: 9.00%
po_kayin: 4.08%
sgaw_kayin: 55.80%
pao: 1.62%
rakhine: 3.81%
shan: 4.05%
Running with ngram=4 on random sentence 7: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 62.28%
mon: 3.02%
bamar: 0.02%
beik: 30.70%
po_kayin: 0.28%
sgaw_kayin: 0.00%
pao: 1.32%
rakhine: 0.42%
shan: 1.96%

Combined Character and Syllable-based Detection:
dawei: 31.14%
mon: 1.51%
bamar: 0.01%
beik: 15.35%
po_kayin: 0.14%
sgaw_kayin: 50.00%
pao: 0.66%
rakhine: 0.21%
shan: 0.98%
Running with ngram=4 on random sentence 8: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 50.32%
mon: 9.93%
bamar: 0.10%
beik: 21.76%
po_kayin: 2.10%
sgaw_kayin: 0.04%
pao: 0.71%
rakhine: 10.64%
shan: 4.40%

Combined Character and Syllable-based Detection:
dawei: 25.16%
mon: 4.97%
bamar: 0.05%
beik: 10.88%
po_kayin: 1.05%
sgaw_kayin: 50.02%
pao: 0.35%
rakhine: 5.32%
shan: 2.20%
Running with ngram=4 on random sentence 9: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.59%
mon: 12.16%
bamar: 3.53%
beik: 17.99%
po_kayin: 8.17%
sgaw_kayin: 11.61%
pao: 3.24%
rakhine: 7.63%
shan: 8.09%

Combined Character and Syllable-based Detection:
dawei: 13.80%
mon: 6.08%
bamar: 1.76%
beik: 9.00%
po_kayin: 4.08%
sgaw_kayin: 55.80%
pao: 1.62%
rakhine: 3.81%
shan: 4.05%
Running with ngram=4 on random sentence 10: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 22.31%
mon: 15.84%
bamar: 4.59%
beik: 23.44%
po_kayin: 10.64%
sgaw_kayin: 0.06%
pao: 2.62%
rakhine: 9.94%
shan: 10.54%

Combined Character and Syllable-based Detection:
dawei: 11.16%
mon: 7.92%
bamar: 2.30%
beik: 11.72%
po_kayin: 5.32%
sgaw_kayin: 50.03%
pao: 1.31%
rakhine: 4.97%
shan: 5.27%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.96%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.04%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 0.00%
dawei: 0.48%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 49.52%
Running with ngram=5 on random sentence 1: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 9.95%
dawei: 22.32%
pao: 2.62%
po_kayin: 10.65%
bamar: 4.60%
mon: 15.85%
shan: 10.55%
beik: 23.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 4.97%
dawei: 11.16%
pao: 1.31%
po_kayin: 5.32%
bamar: 2.30%
mon: 7.92%
shan: 5.28%
beik: 11.73%
Running with ngram=5 on random sentence 2: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 15.24%
dawei: 15.24%
pao: 4.08%
po_kayin: 4.43%
bamar: 15.24%
mon: 15.24%
shan: 15.24%
beik: 15.24%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.01%
rakhine: 7.62%
dawei: 7.62%
pao: 2.04%
po_kayin: 2.22%
bamar: 7.62%
mon: 7.62%
shan: 7.62%
beik: 7.62%
Running with ngram=5 on random sentence 3: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%
Running with ngram=5 on random sentence 4: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 9.95%
dawei: 22.32%
pao: 2.62%
po_kayin: 10.65%
bamar: 4.60%
mon: 15.85%
shan: 10.55%
beik: 23.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 4.97%
dawei: 11.16%
pao: 1.31%
po_kayin: 5.32%
bamar: 2.30%
mon: 7.92%
shan: 5.28%
beik: 11.73%
Running with ngram=5 on random sentence 5: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 1.79%
dawei: 39.26%
pao: 0.07%
po_kayin: 0.45%
bamar: 0.01%
mon: 4.94%
shan: 3.21%
beik: 50.25%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 0.90%
dawei: 19.63%
pao: 0.04%
po_kayin: 0.23%
bamar: 0.01%
mon: 2.47%
shan: 1.61%
beik: 25.12%
Running with ngram=5 on random sentence 6: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.99%
rakhine: 9.65%
dawei: 21.66%
pao: 2.54%
po_kayin: 10.33%
bamar: 4.46%
mon: 15.38%
shan: 10.24%
beik: 22.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 51.50%
rakhine: 4.82%
dawei: 10.83%
pao: 1.27%
po_kayin: 5.16%
bamar: 2.23%
mon: 7.69%
shan: 5.12%
beik: 11.38%
Running with ngram=5 on random sentence 7: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%
Running with ngram=5 on random sentence 8: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.99%
rakhine: 9.65%
dawei: 21.66%
pao: 2.54%
po_kayin: 10.33%
bamar: 4.46%
mon: 15.38%
shan: 10.24%
beik: 22.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 51.50%
rakhine: 4.82%
dawei: 10.83%
pao: 1.27%
po_kayin: 5.16%
bamar: 2.23%
mon: 7.69%
shan: 5.12%
beik: 11.38%
Running with ngram=5 on random sentence 9: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Character-based Detection:
sgaw_kayin: 99.97%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 8.42%
dawei: 16.30%
pao: 0.84%
po_kayin: 3.71%
bamar: 0.69%
mon: 8.22%
shan: 43.83%
beik: 17.99%

Combined Character and Syllable-based Detection:
sgaw_kayin: 49.99%
rakhine: 4.21%
dawei: 8.15%
pao: 0.42%
po_kayin: 1.86%
bamar: 0.35%
mon: 4.11%
shan: 21.92%
beik: 9.00%
Running with ngram=5 on random sentence 10: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%

Processing file: shan.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.46%
mon: 0.32%
shan: 93.67%
pao: 0.78%
rakhine: 0.77%
po_kayin: 0.31%
sgaw_kayin: 0.31%
dawei: 1.11%
bamar: 1.27%

Combined Character and Syllable-based Detection:
beik: 0.73%
mon: 0.16%
shan: 96.84%
pao: 0.39%
rakhine: 0.39%
po_kayin: 0.15%
sgaw_kayin: 0.15%
dawei: 0.55%
bamar: 0.63%
Running with ngram=3 on random sentence 2: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.46%
mon: 0.32%
shan: 93.67%
pao: 0.78%
rakhine: 0.77%
po_kayin: 0.31%
sgaw_kayin: 0.31%
dawei: 1.11%
bamar: 1.27%

Combined Character and Syllable-based Detection:
beik: 0.73%
mon: 0.16%
shan: 96.84%
pao: 0.39%
rakhine: 0.39%
po_kayin: 0.15%
sgaw_kayin: 0.15%
dawei: 0.55%
bamar: 0.63%
Running with ngram=3 on random sentence 3: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.18%
mon: 0.08%
shan: 98.69%
pao: 0.18%
rakhine: 0.18%
po_kayin: 0.18%
sgaw_kayin: 0.18%
dawei: 0.18%
bamar: 0.18%

Combined Character and Syllable-based Detection:
beik: 0.09%
mon: 0.04%
shan: 99.34%
pao: 0.09%
rakhine: 0.09%
po_kayin: 0.09%
sgaw_kayin: 0.09%
dawei: 0.09%
bamar: 0.09%
Running with ngram=3 on random sentence 4: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.60%
mon: 0.80%
shan: 84.36%
pao: 1.94%
rakhine: 1.91%
po_kayin: 0.76%
sgaw_kayin: 0.76%
dawei: 2.73%
bamar: 3.13%

Combined Character and Syllable-based Detection:
beik: 1.80%
mon: 0.40%
shan: 92.18%
pao: 0.97%
rakhine: 0.96%
po_kayin: 0.38%
sgaw_kayin: 0.38%
dawei: 1.37%
bamar: 1.57%
Running with ngram=3 on random sentence 5: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 6.23%
mon: 2.70%
shan: 53.72%
pao: 6.23%
rakhine: 6.23%
po_kayin: 6.23%
sgaw_kayin: 6.23%
dawei: 6.23%
bamar: 6.23%

Combined Character and Syllable-based Detection:
beik: 3.11%
mon: 1.35%
shan: 76.86%
pao: 3.11%
rakhine: 3.11%
po_kayin: 3.11%
sgaw_kayin: 3.11%
dawei: 3.11%
bamar: 3.11%
Running with ngram=3 on random sentence 6: တႃႇမၼ်းၼၢင်းႁဝ်းတေထၢမ်ဢမ်ႇၸႂ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 8.58%
mon: 1.90%
shan: 62.71%
pao: 4.62%
rakhine: 4.57%
po_kayin: 1.82%
sgaw_kayin: 1.82%
dawei: 6.52%
bamar: 7.47%

Combined Character and Syllable-based Detection:
beik: 4.29%
mon: 0.95%
shan: 81.35%
pao: 2.31%
rakhine: 2.28%
po_kayin: 0.91%
sgaw_kayin: 0.91%
dawei: 3.26%
bamar: 3.74%
Running with ngram=3 on random sentence 7: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.01%
mon: 0.00%
shan: 99.95%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 0.01%
bamar: 0.01%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 99.97%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 8: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 9: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.01%
mon: 0.00%
shan: 99.95%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 0.01%
bamar: 0.01%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 99.97%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 10: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%
Running with ngram=4 on random sentence 1: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.02%
mon: 5.21%
bamar: 12.02%
beik: 12.02%
po_kayin: 12.02%
sgaw_kayin: 12.02%
pao: 12.02%
rakhine: 12.02%
shan: 10.68%

Combined Character and Syllable-based Detection:
dawei: 6.01%
mon: 2.60%
bamar: 6.01%
beik: 6.01%
po_kayin: 6.01%
sgaw_kayin: 6.01%
pao: 6.01%
rakhine: 6.01%
shan: 55.34%
Running with ngram=4 on random sentence 2: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 1.70%
mon: 0.74%
bamar: 1.70%
beik: 1.70%
po_kayin: 1.70%
sgaw_kayin: 1.70%
pao: 1.70%
rakhine: 1.70%
shan: 87.37%

Combined Character and Syllable-based Detection:
dawei: 0.85%
mon: 0.37%
bamar: 0.85%
beik: 0.85%
po_kayin: 0.85%
sgaw_kayin: 0.85%
pao: 0.85%
rakhine: 0.85%
shan: 93.69%
Running with ngram=4 on random sentence 3: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 7.23%
mon: 3.13%
bamar: 7.23%
beik: 7.23%
po_kayin: 7.23%
sgaw_kayin: 7.23%
pao: 7.23%
rakhine: 7.23%
shan: 46.27%

Combined Character and Syllable-based Detection:
dawei: 3.61%
mon: 1.57%
bamar: 3.61%
beik: 3.61%
po_kayin: 3.61%
sgaw_kayin: 3.61%
pao: 3.61%
rakhine: 3.61%
shan: 73.13%
Running with ngram=4 on random sentence 4: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.95%
mon: 5.61%
bamar: 12.95%
beik: 12.95%
po_kayin: 12.95%
sgaw_kayin: 12.95%
pao: 12.95%
rakhine: 12.95%
shan: 3.74%

Combined Character and Syllable-based Detection:
dawei: 6.48%
mon: 2.81%
bamar: 6.48%
beik: 6.48%
po_kayin: 6.48%
sgaw_kayin: 6.48%
pao: 6.48%
rakhine: 6.48%
shan: 51.87%
Running with ngram=4 on random sentence 5: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.03%
mon: 0.01%
bamar: 0.03%
beik: 0.03%
po_kayin: 0.03%
sgaw_kayin: 0.03%
pao: 0.03%
rakhine: 0.03%
shan: 99.77%

Combined Character and Syllable-based Detection:
dawei: 0.02%
mon: 0.01%
bamar: 0.02%
beik: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.02%
shan: 99.89%
Running with ngram=4 on random sentence 6: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.02%
mon: 5.21%
bamar: 12.02%
beik: 12.02%
po_kayin: 12.02%
sgaw_kayin: 12.02%
pao: 12.02%
rakhine: 12.02%
shan: 10.68%

Combined Character and Syllable-based Detection:
dawei: 6.01%
mon: 2.60%
bamar: 6.01%
beik: 6.01%
po_kayin: 6.01%
sgaw_kayin: 6.01%
pao: 6.01%
rakhine: 6.01%
shan: 55.34%
Running with ngram=4 on random sentence 7: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.02%
mon: 5.21%
bamar: 12.02%
beik: 12.02%
po_kayin: 12.02%
sgaw_kayin: 12.02%
pao: 12.02%
rakhine: 12.02%
shan: 10.68%

Combined Character and Syllable-based Detection:
dawei: 6.01%
mon: 2.60%
bamar: 6.01%
beik: 6.01%
po_kayin: 6.01%
sgaw_kayin: 6.01%
pao: 6.01%
rakhine: 6.01%
shan: 55.34%
Running with ngram=4 on random sentence 8: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 11.77%
mon: 3.42%
bamar: 0.41%
beik: 15.49%
po_kayin: 3.28%
sgaw_kayin: 3.28%
pao: 0.88%
rakhine: 8.25%
shan: 53.22%

Combined Character and Syllable-based Detection:
dawei: 5.88%
mon: 1.71%
bamar: 0.21%
beik: 7.75%
po_kayin: 1.64%
sgaw_kayin: 1.64%
pao: 0.44%
rakhine: 4.12%
shan: 76.61%
Running with ngram=4 on random sentence 9: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 24.47%
mon: 7.12%
bamar: 0.86%
beik: 32.21%
po_kayin: 6.82%
sgaw_kayin: 6.82%
pao: 1.83%
rakhine: 17.14%
shan: 2.74%

Combined Character and Syllable-based Detection:
dawei: 12.23%
mon: 3.56%
bamar: 0.43%
beik: 16.10%
po_kayin: 3.41%
sgaw_kayin: 3.41%
pao: 0.91%
rakhine: 8.57%
shan: 51.37%
Running with ngram=4 on random sentence 10: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 11.77%
mon: 3.42%
bamar: 0.41%
beik: 15.49%
po_kayin: 3.28%
sgaw_kayin: 3.28%
pao: 0.88%
rakhine: 8.25%
shan: 53.22%

Combined Character and Syllable-based Detection:
dawei: 5.88%
mon: 1.71%
bamar: 0.21%
beik: 7.75%
po_kayin: 1.64%
sgaw_kayin: 1.64%
pao: 0.44%
rakhine: 4.12%
shan: 76.61%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%
Running with ngram=5 on random sentence 1: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.50%
rakhine: 1.24%
dawei: 0.91%
pao: 0.40%
po_kayin: 1.50%
bamar: 0.19%
mon: 0.28%
shan: 92.44%
beik: 1.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.75%
rakhine: 0.62%
dawei: 0.46%
pao: 0.20%
po_kayin: 0.75%
bamar: 0.09%
mon: 0.14%
shan: 96.22%
beik: 0.77%
Running with ngram=5 on random sentence 2: မိူဝ်ႈပူၼ်ႉမႃးဝၼ်းသုၵ်းၵၢင်ၼႂ်႑႑မွင်းၼၼ်ႉသူမီးယူႇတီႈလႂ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.73%
rakhine: 9.52%
dawei: 37.32%
pao: 3.95%
po_kayin: 14.78%
bamar: 0.50%
mon: 6.40%
shan: 0.32%
beik: 25.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.87%
rakhine: 4.76%
dawei: 18.66%
pao: 1.98%
po_kayin: 7.39%
bamar: 0.25%
mon: 3.20%
shan: 50.16%
beik: 12.74%
Running with ngram=5 on random sentence 3: တႃႇမၼ်းၼၢင်းႁဝ်းတေထၢမ်ဢမ်ႇၸႂ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.76%
rakhine: 5.58%
dawei: 4.13%
pao: 1.81%
po_kayin: 6.76%
bamar: 0.85%
mon: 1.27%
shan: 65.86%
beik: 6.98%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.38%
rakhine: 2.79%
dawei: 2.06%
pao: 0.91%
po_kayin: 3.38%
bamar: 0.42%
mon: 0.63%
shan: 82.93%
beik: 3.49%
Running with ngram=5 on random sentence 4: မိူဝ်ႈပူၼ်ႉမႃးဝၼ်းသုၵ်းၵၢင်ၼႂ်႑႑မွင်းၼၼ်ႉသူမီးယူႇတီႈလႂ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.73%
rakhine: 9.52%
dawei: 37.32%
pao: 3.95%
po_kayin: 14.78%
bamar: 0.50%
mon: 6.40%
shan: 0.32%
beik: 25.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.87%
rakhine: 4.76%
dawei: 18.66%
pao: 1.98%
po_kayin: 7.39%
bamar: 0.25%
mon: 3.20%
shan: 50.16%
beik: 12.74%
Running with ngram=5 on random sentence 5: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.36%
rakhine: 0.36%
dawei: 0.36%
pao: 0.36%
po_kayin: 0.36%
bamar: 0.36%
mon: 0.16%
shan: 97.31%
beik: 0.36%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.18%
rakhine: 0.18%
dawei: 0.18%
pao: 0.18%
po_kayin: 0.18%
bamar: 0.18%
mon: 0.08%
shan: 98.66%
beik: 0.18%
Running with ngram=5 on random sentence 6: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 11.21%
rakhine: 11.21%
dawei: 11.21%
pao: 11.21%
po_kayin: 11.21%
bamar: 11.21%
mon: 4.86%
shan: 16.65%
beik: 11.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.61%
rakhine: 5.61%
dawei: 5.61%
pao: 5.61%
po_kayin: 5.61%
bamar: 5.61%
mon: 2.43%
shan: 58.32%
beik: 5.61%
Running with ngram=5 on random sentence 7: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 11.21%
rakhine: 11.21%
dawei: 11.21%
pao: 11.21%
po_kayin: 11.21%
bamar: 11.21%
mon: 4.86%
shan: 16.65%
beik: 11.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.61%
rakhine: 5.61%
dawei: 5.61%
pao: 5.61%
po_kayin: 5.61%
bamar: 5.61%
mon: 2.43%
shan: 58.32%
beik: 5.61%
Running with ngram=5 on random sentence 8: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 12.23%
rakhine: 12.23%
dawei: 12.23%
pao: 12.23%
po_kayin: 12.23%
bamar: 12.23%
mon: 5.30%
shan: 9.08%
beik: 12.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.12%
rakhine: 6.12%
dawei: 6.12%
pao: 6.12%
po_kayin: 6.12%
bamar: 6.12%
mon: 2.65%
shan: 54.54%
beik: 6.12%
Running with ngram=5 on random sentence 9: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.50%
rakhine: 1.24%
dawei: 0.91%
pao: 0.40%
po_kayin: 1.50%
bamar: 0.19%
mon: 0.28%
shan: 92.44%
beik: 1.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.75%
rakhine: 0.62%
dawei: 0.46%
pao: 0.20%
po_kayin: 0.75%
bamar: 0.09%
mon: 0.14%
shan: 96.22%
beik: 0.77%
Running with ngram=5 on random sentence 10: မိူဝ်ႈပူၼ်ႉမႃးဝၼ်းသုၵ်းၵၢင်ၼႂ်႑႑မွင်းၼၼ်ႉသူမီးယူႇတီႈလႂ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.73%
rakhine: 9.52%
dawei: 37.32%
pao: 3.95%
po_kayin: 14.78%
bamar: 0.50%
mon: 6.40%
shan: 0.32%
beik: 25.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.87%
rakhine: 4.76%
dawei: 18.66%
pao: 1.98%
po_kayin: 7.39%
bamar: 0.25%
mon: 3.20%
shan: 50.16%
beik: 12.74%

All processing completed.

real    12m27.260s
user    11m14.308s
sys     1m12.785s
```

Experiment-2 (with char, syl, char+syl Ngram, Naive Bayes) ရဲ့ ရလဒ်က အောက်ပါအတိုင်း ...  

```
Processing file: bamar_burmese.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.00%
Running with ngram=3 on random sentence 1: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
beik: 1.96%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 23.45%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 74.59%

Syllable-based Detection:
beik: 53.34%
mon: 0.06%
shan: 0.35%
pao: 0.01%
rakhine: 0.21%
po_kayin: 0.01%
sgaw_kayin: 0.02%
dawei: 44.79%
bamar: 1.21%

Combined Character and Syllable-based Detection:
beik: 27.65%
mon: 0.03%
shan: 0.18%
pao: 0.00%
rakhine: 11.83%
po_kayin: 0.00%
sgaw_kayin: 0.01%
dawei: 22.40%
bamar: 37.90%
Running with ngram=3 on random sentence 2: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
beik: 0.38%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.11%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 99.50%

Syllable-based Detection:
beik: 11.24%
mon: 10.81%
shan: 3.84%
pao: 50.03%
rakhine: 6.41%
po_kayin: 3.84%
sgaw_kayin: 2.92%
dawei: 8.99%
bamar: 1.91%

Combined Character and Syllable-based Detection:
beik: 5.81%
mon: 5.41%
shan: 1.92%
pao: 25.01%
rakhine: 3.26%
po_kayin: 1.92%
sgaw_kayin: 1.46%
dawei: 4.50%
bamar: 50.71%
Running with ngram=3 on random sentence 3: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.66%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.34%

Combined Character and Syllable-based Detection:
beik: 49.83%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.17%
Running with ngram=3 on random sentence 4: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 59.70%
mon: 0.00%
shan: 0.00%
pao: 0.20%
rakhine: 0.02%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 40.07%

Combined Character and Syllable-based Detection:
beik: 29.85%
mon: 0.00%
shan: 0.00%
pao: 0.10%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 70.03%
Running with ngram=3 on random sentence 5: ကလေးကအိမ်မှာပါ
Character-based Detection:
beik: 0.69%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.32%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 98.99%

Syllable-based Detection:
beik: 66.89%
mon: 4.24%
shan: 0.33%
pao: 1.72%
rakhine: 0.19%
po_kayin: 0.10%
sgaw_kayin: 0.03%
dawei: 26.37%
bamar: 0.12%

Combined Character and Syllable-based Detection:
beik: 33.79%
mon: 2.12%
shan: 0.17%
pao: 0.86%
rakhine: 0.25%
po_kayin: 0.05%
sgaw_kayin: 0.01%
dawei: 13.18%
bamar: 49.56%
Running with ngram=3 on random sentence 6: နေကောင်းလား
Character-based Detection:
beik: 44.89%
mon: 0.00%
shan: 0.00%
pao: 0.07%
rakhine: 35.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 6.83%
bamar: 12.41%

Syllable-based Detection:
beik: 1.01%
mon: 0.48%
shan: 0.48%
pao: 1.58%
rakhine: 47.41%
po_kayin: 0.48%
sgaw_kayin: 0.48%
dawei: 47.01%
bamar: 1.09%

Combined Character and Syllable-based Detection:
beik: 22.95%
mon: 0.24%
shan: 0.24%
pao: 0.82%
rakhine: 41.60%
po_kayin: 0.24%
sgaw_kayin: 0.24%
dawei: 26.92%
bamar: 6.75%
Running with ngram=3 on random sentence 7: ကလေးကအိမ်မှာပါ
Character-based Detection:
beik: 0.69%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.32%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 98.99%

Syllable-based Detection:
beik: 66.89%
mon: 4.24%
shan: 0.33%
pao: 1.72%
rakhine: 0.19%
po_kayin: 0.10%
sgaw_kayin: 0.03%
dawei: 26.37%
bamar: 0.12%

Combined Character and Syllable-based Detection:
beik: 33.79%
mon: 2.12%
shan: 0.17%
pao: 0.86%
rakhine: 0.25%
po_kayin: 0.05%
sgaw_kayin: 0.01%
dawei: 13.18%
bamar: 49.56%
Running with ngram=3 on random sentence 8: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.00%
Running with ngram=3 on random sentence 9: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 100.00%

Syllable-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 50.00%
Running with ngram=3 on random sentence 10: နေကောင်းလား
Character-based Detection:
beik: 44.89%
mon: 0.00%
shan: 0.00%
pao: 0.07%
rakhine: 35.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 6.83%
bamar: 12.41%

Syllable-based Detection:
beik: 1.01%
mon: 0.48%
shan: 0.48%
pao: 1.58%
rakhine: 47.41%
po_kayin: 0.48%
sgaw_kayin: 0.48%
dawei: 47.01%
bamar: 1.09%

Combined Character and Syllable-based Detection:
beik: 22.95%
mon: 0.24%
shan: 0.24%
pao: 0.82%
rakhine: 41.60%
po_kayin: 0.24%
sgaw_kayin: 0.24%
dawei: 26.92%
bamar: 6.75%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 50.00%
beik: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 10.13%
mon: 0.00%
bamar: 2.61%
beik: 85.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.67%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 5.06%
mon: 0.00%
bamar: 51.30%
beik: 42.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.84%
shan: 0.00%
Running with ngram=4 on random sentence 2: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 98.77%
beik: 1.23%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.71%
mon: 0.01%
bamar: 0.04%
beik: 97.50%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.73%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 0.35%
mon: 0.00%
bamar: 49.40%
beik: 49.37%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.86%
shan: 0.01%
Running with ngram=4 on random sentence 3: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 10.13%
mon: 0.00%
bamar: 2.61%
beik: 85.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.67%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 5.06%
mon: 0.00%
bamar: 51.30%
beik: 42.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.84%
shan: 0.00%
Running with ngram=4 on random sentence 4: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 99.82%
beik: 0.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 40.67%
mon: 1.54%
bamar: 4.22%
beik: 48.70%
po_kayin: 0.55%
sgaw_kayin: 0.06%
pao: 0.15%
rakhine: 3.57%
shan: 0.55%

Combined Character and Syllable-based Detection:
dawei: 20.34%
mon: 0.77%
bamar: 52.02%
beik: 24.44%
po_kayin: 0.27%
sgaw_kayin: 0.03%
pao: 0.07%
rakhine: 1.79%
shan: 0.27%
Running with ngram=4 on random sentence 5: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 56.81%
beik: 0.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 42.39%
shan: 0.00%

Syllable-based Detection:
dawei: 0.86%
mon: 0.75%
bamar: 2.18%
beik: 93.40%
po_kayin: 1.08%
sgaw_kayin: 0.13%
pao: 0.29%
rakhine: 0.80%
shan: 0.50%

Combined Character and Syllable-based Detection:
dawei: 0.43%
mon: 0.38%
bamar: 29.50%
beik: 47.10%
po_kayin: 0.54%
sgaw_kayin: 0.06%
pao: 0.14%
rakhine: 21.60%
shan: 0.25%
Running with ngram=4 on random sentence 6: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 98.77%
beik: 1.23%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.71%
mon: 0.01%
bamar: 0.04%
beik: 97.50%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.73%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 0.35%
mon: 0.00%
bamar: 49.40%
beik: 49.37%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.86%
shan: 0.01%
Running with ngram=4 on random sentence 7: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 56.81%
beik: 0.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 42.39%
shan: 0.00%

Syllable-based Detection:
dawei: 0.86%
mon: 0.75%
bamar: 2.18%
beik: 93.40%
po_kayin: 1.08%
sgaw_kayin: 0.13%
pao: 0.29%
rakhine: 0.80%
shan: 0.50%

Combined Character and Syllable-based Detection:
dawei: 0.43%
mon: 0.38%
bamar: 29.50%
beik: 47.10%
po_kayin: 0.54%
sgaw_kayin: 0.06%
pao: 0.14%
rakhine: 21.60%
shan: 0.25%
Running with ngram=4 on random sentence 8: ကလေးကအိမ်မှာပါ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 97.13%
beik: 2.86%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.01%
shan: 0.00%

Syllable-based Detection:
dawei: 1.76%
mon: 2.42%
bamar: 6.31%
beik: 55.83%
po_kayin: 1.23%
sgaw_kayin: 0.14%
pao: 0.37%
rakhine: 30.71%
shan: 1.23%

Combined Character and Syllable-based Detection:
dawei: 0.88%
mon: 1.21%
bamar: 51.72%
beik: 29.34%
po_kayin: 0.62%
sgaw_kayin: 0.07%
pao: 0.19%
rakhine: 15.36%
shan: 0.62%
Running with ngram=4 on random sentence 9: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 100.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 10.13%
mon: 0.00%
bamar: 2.61%
beik: 85.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.67%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 5.06%
mon: 0.00%
bamar: 51.30%
beik: 42.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.84%
shan: 0.00%
Running with ngram=4 on random sentence 10: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 98.77%
beik: 1.23%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.71%
mon: 0.01%
bamar: 0.04%
beik: 97.50%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 1.73%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 0.35%
mon: 0.00%
bamar: 49.40%
beik: 49.37%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.86%
shan: 0.01%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.79%
mon: 0.00%
shan: 0.00%
beik: 99.21%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.04%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.96%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.02%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.40%
mon: 0.00%
shan: 0.00%
beik: 99.58%
Running with ngram=5 on random sentence 1: တက္ကသိုလ်အသွားအပြန်ကိုသင်္ဘောစီးပြီးသွားရတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.93%
mon: 0.00%
shan: 0.00%
beik: 0.07%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 4.14%
dawei: 22.34%
pao: 0.03%
po_kayin: 0.24%
bamar: 0.00%
mon: 0.23%
shan: 0.83%
beik: 72.15%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 2.07%
dawei: 11.17%
pao: 0.01%
po_kayin: 0.12%
bamar: 49.96%
mon: 0.12%
shan: 0.41%
beik: 36.11%
Running with ngram=5 on random sentence 2: နေကောင်းလား
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 46.39%
dawei: 0.02%
pao: 0.00%
po_kayin: 0.00%
bamar: 20.07%
mon: 0.00%
shan: 0.00%
beik: 33.52%
Running with ngram=5 on random sentence 3: ပြောပြပါဦးဘာတွေဖြစ်နေတာလဲ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 71.58%
mon: 0.00%
shan: 0.00%
beik: 28.42%

Syllable-based Detection:
sgaw_kayin: 4.55%
rakhine: 0.64%
dawei: 3.27%
pao: 0.20%
po_kayin: 34.26%
bamar: 0.00%
mon: 11.72%
shan: 38.81%
beik: 6.54%

Combined Character and Syllable-based Detection:
sgaw_kayin: 2.27%
rakhine: 0.32%
dawei: 1.64%
pao: 0.10%
po_kayin: 17.13%
bamar: 35.79%
mon: 5.86%
shan: 19.41%
beik: 17.48%
Running with ngram=5 on random sentence 4: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.99%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 2.62%
rakhine: 6.08%
dawei: 13.66%
pao: 5.99%
po_kayin: 22.39%
bamar: 2.81%
mon: 9.70%
shan: 22.39%
beik: 14.35%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.31%
rakhine: 3.04%
dawei: 6.83%
pao: 3.00%
po_kayin: 11.20%
bamar: 51.40%
mon: 4.85%
shan: 11.20%
beik: 7.18%
Running with ngram=5 on random sentence 5: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 15.49%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 84.33%
mon: 0.00%
shan: 0.00%
beik: 0.17%

Syllable-based Detection:
sgaw_kayin: 13.78%
rakhine: 11.36%
dawei: 8.40%
pao: 13.78%
po_kayin: 13.78%
bamar: 1.73%
mon: 9.61%
shan: 13.78%
beik: 13.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.89%
rakhine: 13.43%
dawei: 4.20%
pao: 6.89%
po_kayin: 6.89%
bamar: 43.03%
mon: 4.81%
shan: 6.89%
beik: 6.98%
Running with ngram=5 on random sentence 6: ကျန်းမာတယ်ဒါပေမဲ့အလုပ်များတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 100.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.73%
rakhine: 1.53%
dawei: 33.38%
pao: 1.44%
po_kayin: 16.71%
bamar: 1.42%
mon: 7.51%
shan: 7.69%
beik: 23.58%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.36%
rakhine: 0.77%
dawei: 16.69%
pao: 0.72%
po_kayin: 8.35%
bamar: 50.71%
mon: 3.76%
shan: 3.85%
beik: 11.79%
Running with ngram=5 on random sentence 7: ကျောင်းသားကျောင်းသွားပါ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 99.99%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 2.62%
rakhine: 6.08%
dawei: 13.66%
pao: 5.99%
po_kayin: 22.39%
bamar: 2.81%
mon: 9.70%
shan: 22.39%
beik: 14.35%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.31%
rakhine: 3.04%
dawei: 6.83%
pao: 3.00%
po_kayin: 11.20%
bamar: 51.40%
mon: 4.85%
shan: 11.20%
beik: 7.18%
Running with ngram=5 on random sentence 8: ကျောင်းသားကျောင်းသူကျောင်းမှာ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 15.49%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 84.33%
mon: 0.00%
shan: 0.00%
beik: 0.17%

Syllable-based Detection:
sgaw_kayin: 13.78%
rakhine: 11.36%
dawei: 8.40%
pao: 13.78%
po_kayin: 13.78%
bamar: 1.73%
mon: 9.61%
shan: 13.78%
beik: 13.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.89%
rakhine: 13.43%
dawei: 4.20%
pao: 6.89%
po_kayin: 6.89%
bamar: 43.03%
mon: 4.81%
shan: 6.89%
beik: 6.98%
Running with ngram=5 on random sentence 9: ပုပ္ပါးတောင်ကိုထပ်တက်ချင်သေးတယ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 39.04%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 15.32%
mon: 0.00%
shan: 0.00%
beik: 45.64%

Syllable-based Detection:
sgaw_kayin: 16.47%
rakhine: 4.19%
dawei: 11.34%
pao: 9.31%
po_kayin: 16.47%
bamar: 0.01%
mon: 15.20%
shan: 16.47%
beik: 10.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 8.23%
rakhine: 21.61%
dawei: 5.67%
pao: 4.65%
po_kayin: 8.23%
bamar: 7.66%
mon: 7.60%
shan: 8.23%
beik: 28.10%
Running with ngram=5 on random sentence 10: နေကောင်းလား
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 46.39%
dawei: 0.02%
pao: 0.00%
po_kayin: 0.00%
bamar: 20.07%
mon: 0.00%
shan: 0.00%
beik: 33.52%

Processing file: beik.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.78%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.22%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 99.89%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=3 on random sentence 1: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Character-based Detection:
beik: 62.50%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 37.44%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.06%

Syllable-based Detection:
beik: 0.78%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.02%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.20%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 31.64%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 18.73%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 49.60%
bamar: 0.03%
Running with ngram=3 on random sentence 2: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 3: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.12%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.88%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.06%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 49.94%
bamar: 0.00%
Running with ngram=3 on random sentence 4: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 5: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 6: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.53%
mon: 0.01%
shan: 0.00%
pao: 0.03%
rakhine: 8.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 88.25%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 51.76%
mon: 0.01%
shan: 0.00%
pao: 0.01%
rakhine: 4.09%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 44.12%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.69%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.05%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 0.01%
bamar: 0.21%

Combined Character and Syllable-based Detection:
beik: 99.84%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.03%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 0.01%
bamar: 0.10%
Running with ngram=3 on random sentence 8: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 11.92%
mon: 0.09%
shan: 0.03%
pao: 0.98%
rakhine: 24.13%
po_kayin: 0.07%
sgaw_kayin: 0.03%
dawei: 1.31%
bamar: 61.44%

Combined Character and Syllable-based Detection:
beik: 55.96%
mon: 0.05%
shan: 0.02%
pao: 0.49%
rakhine: 12.06%
po_kayin: 0.04%
sgaw_kayin: 0.01%
dawei: 0.66%
bamar: 30.72%
Running with ngram=3 on random sentence 9: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.84%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 5.59%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 92.57%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.92%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 2.80%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 46.29%
bamar: 0.00%
Running with ngram=3 on random sentence 10: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.12%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.88%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.06%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 49.94%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.54%
mon: 0.39%
bamar: 0.03%
beik: 97.38%
po_kayin: 0.60%
sgaw_kayin: 0.08%
pao: 0.05%
rakhine: 0.25%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 0.27%
mon: 0.19%
bamar: 0.01%
beik: 98.69%
po_kayin: 0.30%
sgaw_kayin: 0.04%
pao: 0.02%
rakhine: 0.12%
shan: 0.34%
Running with ngram=4 on random sentence 2: သူတို့ဘဇာလောက်သတ္တိရှိလဲ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.54%
mon: 0.39%
bamar: 0.03%
beik: 97.38%
po_kayin: 0.60%
sgaw_kayin: 0.08%
pao: 0.05%
rakhine: 0.25%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 0.27%
mon: 0.19%
bamar: 0.01%
beik: 98.69%
po_kayin: 0.30%
sgaw_kayin: 0.04%
pao: 0.02%
rakhine: 0.12%
shan: 0.34%
Running with ngram=4 on random sentence 3: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 74.83%
mon: 0.32%
bamar: 10.94%
beik: 10.99%
po_kayin: 0.05%
sgaw_kayin: 0.58%
pao: 0.06%
rakhine: 2.06%
shan: 0.17%

Combined Character and Syllable-based Detection:
dawei: 37.41%
mon: 0.16%
bamar: 5.47%
beik: 55.50%
po_kayin: 0.02%
sgaw_kayin: 0.29%
pao: 0.03%
rakhine: 1.03%
shan: 0.08%
Running with ngram=4 on random sentence 4: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.81%
mon: 0.89%
bamar: 0.79%
beik: 86.65%
po_kayin: 0.18%
sgaw_kayin: 0.18%
pao: 0.07%
rakhine: 7.24%
shan: 0.18%

Combined Character and Syllable-based Detection:
dawei: 1.91%
mon: 0.44%
bamar: 0.40%
beik: 93.32%
po_kayin: 0.09%
sgaw_kayin: 0.09%
pao: 0.04%
rakhine: 3.62%
shan: 0.09%
Running with ngram=4 on random sentence 5: အဲဒီကိုသောဖို့ငါမင်းကိုငါမတိုက်တွန်းရ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.43%
beik: 99.51%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.06%
shan: 0.00%

Syllable-based Detection:
dawei: 0.05%
mon: 0.00%
bamar: 0.03%
beik: 3.04%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 96.88%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.03%
mon: 0.00%
bamar: 0.23%
beik: 51.27%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 48.47%
shan: 0.00%
Running with ngram=4 on random sentence 6: အဲဒီကိုသောဖို့ငါမင်းကိုငါမတိုက်တွန်းရ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.43%
beik: 99.51%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.06%
shan: 0.00%

Syllable-based Detection:
dawei: 0.05%
mon: 0.00%
bamar: 0.03%
beik: 3.04%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 96.88%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.03%
mon: 0.00%
bamar: 0.23%
beik: 51.27%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 48.47%
shan: 0.00%
Running with ngram=4 on random sentence 7: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 74.83%
mon: 0.32%
bamar: 10.94%
beik: 10.99%
po_kayin: 0.05%
sgaw_kayin: 0.58%
pao: 0.06%
rakhine: 2.06%
shan: 0.17%

Combined Character and Syllable-based Detection:
dawei: 37.41%
mon: 0.16%
bamar: 5.47%
beik: 55.50%
po_kayin: 0.02%
sgaw_kayin: 0.29%
pao: 0.03%
rakhine: 1.03%
shan: 0.08%
Running with ngram=4 on random sentence 8: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.24%
mon: 0.05%
bamar: 0.00%
beik: 98.72%
po_kayin: 0.05%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.86%
shan: 0.05%

Combined Character and Syllable-based Detection:
dawei: 0.12%
mon: 0.03%
bamar: 0.00%
beik: 99.36%
po_kayin: 0.03%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 0.43%
shan: 0.03%
Running with ngram=4 on random sentence 9: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 74.83%
mon: 0.32%
bamar: 10.94%
beik: 10.99%
po_kayin: 0.05%
sgaw_kayin: 0.58%
pao: 0.06%
rakhine: 2.06%
shan: 0.17%

Combined Character and Syllable-based Detection:
dawei: 37.41%
mon: 0.16%
bamar: 5.47%
beik: 55.50%
po_kayin: 0.02%
sgaw_kayin: 0.29%
pao: 0.03%
rakhine: 1.03%
shan: 0.08%
Running with ngram=4 on random sentence 10: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 2.14%
mon: 0.01%
bamar: 0.12%
beik: 6.32%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.23%
rakhine: 91.17%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 1.07%
mon: 0.00%
bamar: 0.06%
beik: 53.16%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.12%
rakhine: 45.59%
shan: 0.00%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%
Running with ngram=5 on random sentence 1: သူဒယ့်ဟာကိုလိုချင်မဟုတ်ဝ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.19%
rakhine: 9.05%
dawei: 17.82%
pao: 0.19%
po_kayin: 1.18%
bamar: 0.17%
mon: 1.05%
shan: 0.54%
beik: 69.80%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.10%
rakhine: 4.53%
dawei: 8.91%
pao: 0.09%
po_kayin: 0.59%
bamar: 0.09%
mon: 0.52%
shan: 0.27%
beik: 84.90%
Running with ngram=5 on random sentence 2: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%
Running with ngram=5 on random sentence 3: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.36%
rakhine: 64.31%
dawei: 31.33%
pao: 0.02%
po_kayin: 0.36%
bamar: 0.01%
mon: 1.47%
shan: 0.36%
beik: 1.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.18%
rakhine: 32.15%
dawei: 15.67%
pao: 0.01%
po_kayin: 0.18%
bamar: 0.00%
mon: 0.73%
shan: 0.18%
beik: 50.89%
Running with ngram=5 on random sentence 4: ဘဇာလောက်စိတ်လှုပ်ရှားရိ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.01%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.99%

Syllable-based Detection:
sgaw_kayin: 3.86%
rakhine: 2.51%
dawei: 78.00%
pao: 1.03%
po_kayin: 1.12%
bamar: 0.38%
mon: 0.72%
shan: 1.11%
beik: 11.26%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.93%
rakhine: 1.26%
dawei: 39.00%
pao: 0.52%
po_kayin: 0.56%
bamar: 0.19%
mon: 0.36%
shan: 0.56%
beik: 55.63%
Running with ngram=5 on random sentence 5: နင်ခရီးမထွက်ခဲ့ရလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 1.94%
rakhine: 7.53%
dawei: 10.08%
pao: 4.42%
po_kayin: 4.81%
bamar: 0.26%
mon: 3.10%
shan: 4.77%
beik: 63.10%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.97%
rakhine: 3.76%
dawei: 5.04%
pao: 2.21%
po_kayin: 2.40%
bamar: 0.13%
mon: 1.55%
shan: 2.38%
beik: 81.55%
Running with ngram=5 on random sentence 6: မင်းငါ့ကိုရှင်းပြနိုင်မလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.12%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.03%
mon: 0.00%
shan: 0.00%
beik: 99.86%

Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 33.10%
dawei: 33.42%
pao: 0.27%
po_kayin: 0.31%
bamar: 1.21%
mon: 0.30%
shan: 1.07%
beik: 30.25%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 16.61%
dawei: 16.71%
pao: 0.14%
po_kayin: 0.16%
bamar: 0.62%
mon: 0.15%
shan: 0.54%
beik: 65.06%
Running with ngram=5 on random sentence 7: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%
Running with ngram=5 on random sentence 8: ဖယ်သူလေကိုမေးရိလဲ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 2.57%
rakhine: 1.62%
dawei: 17.41%
pao: 1.57%
po_kayin: 5.64%
bamar: 0.04%
mon: 4.12%
shan: 2.94%
beik: 64.10%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.29%
rakhine: 0.81%
dawei: 8.70%
pao: 0.79%
po_kayin: 2.82%
bamar: 0.02%
mon: 2.06%
shan: 1.47%
beik: 82.05%
Running with ngram=5 on random sentence 9: အဲ့အမကိုလက်ထပ်လိုက်ရယ်လား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.36%
rakhine: 64.31%
dawei: 31.33%
pao: 0.02%
po_kayin: 0.36%
bamar: 0.01%
mon: 1.47%
shan: 0.36%
beik: 1.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.18%
rakhine: 32.15%
dawei: 15.67%
pao: 0.01%
po_kayin: 0.18%
bamar: 0.00%
mon: 0.73%
shan: 0.18%
beik: 50.89%
Running with ngram=5 on random sentence 10: ဒါထဲမှာအဝေးပြောဖုန်းပြောတအားများရယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.04%
dawei: 0.30%
pao: 0.00%
po_kayin: 0.04%
bamar: 0.00%
mon: 0.02%
shan: 0.04%
beik: 99.55%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 0.02%
dawei: 0.15%
pao: 0.00%
po_kayin: 0.02%
bamar: 0.00%
mon: 0.01%
shan: 0.02%
beik: 99.77%

Processing file: dawei.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.82%
mon: 0.01%
shan: 0.01%
pao: 0.01%
rakhine: 0.47%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 98.57%
bamar: 0.10%

Combined Character and Syllable-based Detection:
beik: 0.41%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.24%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 99.28%
bamar: 0.05%
Running with ngram=3 on random sentence 2: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 4.55%
mon: 0.01%
shan: 0.00%
pao: 0.00%
rakhine: 93.53%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.86%
bamar: 0.05%

Combined Character and Syllable-based Detection:
beik: 2.28%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 46.77%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 50.93%
bamar: 0.02%
Running with ngram=3 on random sentence 3: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.38%
mon: 0.01%
shan: 0.00%
pao: 0.25%
rakhine: 1.93%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 96.38%
bamar: 0.05%

Combined Character and Syllable-based Detection:
beik: 0.69%
mon: 0.01%
shan: 0.00%
pao: 0.13%
rakhine: 0.96%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 98.19%
bamar: 0.02%
Running with ngram=3 on random sentence 4: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.08%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.79%
bamar: 0.11%

Combined Character and Syllable-based Detection:
beik: 0.04%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.90%
bamar: 0.05%
Running with ngram=3 on random sentence 5: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.24%
mon: 0.69%
shan: 0.35%
pao: 0.32%
rakhine: 1.17%
po_kayin: 0.10%
sgaw_kayin: 0.16%
dawei: 94.57%
bamar: 1.40%

Combined Character and Syllable-based Detection:
beik: 0.62%
mon: 0.34%
shan: 0.17%
pao: 0.16%
rakhine: 0.59%
po_kayin: 0.05%
sgaw_kayin: 0.08%
dawei: 97.29%
bamar: 0.70%
Running with ngram=3 on random sentence 6: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.08%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.79%
bamar: 0.11%

Combined Character and Syllable-based Detection:
beik: 0.04%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 99.90%
bamar: 0.05%
Running with ngram=3 on random sentence 7: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.82%
mon: 0.01%
shan: 0.01%
pao: 0.01%
rakhine: 0.47%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 98.57%
bamar: 0.10%

Combined Character and Syllable-based Detection:
beik: 0.41%
mon: 0.00%
shan: 0.01%
pao: 0.00%
rakhine: 0.24%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 99.28%
bamar: 0.05%
Running with ngram=3 on random sentence 8: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.24%
mon: 0.69%
shan: 0.35%
pao: 0.32%
rakhine: 1.17%
po_kayin: 0.10%
sgaw_kayin: 0.16%
dawei: 94.57%
bamar: 1.40%

Combined Character and Syllable-based Detection:
beik: 0.62%
mon: 0.34%
shan: 0.17%
pao: 0.16%
rakhine: 0.59%
po_kayin: 0.05%
sgaw_kayin: 0.08%
dawei: 97.29%
bamar: 0.70%
Running with ngram=3 on random sentence 9: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.38%
mon: 0.01%
shan: 0.00%
pao: 0.25%
rakhine: 1.93%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 96.38%
bamar: 0.05%

Combined Character and Syllable-based Detection:
beik: 0.69%
mon: 0.01%
shan: 0.00%
pao: 0.13%
rakhine: 0.96%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 98.19%
bamar: 0.02%
Running with ngram=3 on random sentence 10: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 100.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.24%
mon: 0.69%
shan: 0.35%
pao: 0.32%
rakhine: 1.17%
po_kayin: 0.10%
sgaw_kayin: 0.16%
dawei: 94.57%
bamar: 1.40%

Combined Character and Syllable-based Detection:
beik: 0.62%
mon: 0.34%
shan: 0.17%
pao: 0.16%
rakhine: 0.59%
po_kayin: 0.05%
sgaw_kayin: 0.08%
dawei: 97.29%
bamar: 0.70%
Running with ngram=4 on full file
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.58%
mon: 1.52%
bamar: 28.63%
beik: 14.61%
po_kayin: 3.51%
sgaw_kayin: 3.51%
pao: 0.94%
rakhine: 16.19%
shan: 3.51%

Combined Character and Syllable-based Detection:
dawei: 63.79%
mon: 0.76%
bamar: 14.32%
beik: 7.31%
po_kayin: 1.75%
sgaw_kayin: 1.75%
pao: 0.47%
rakhine: 8.09%
shan: 1.75%
Running with ngram=4 on random sentence 2: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 87.64%
mon: 0.39%
bamar: 4.90%
beik: 0.92%
po_kayin: 0.89%
sgaw_kayin: 0.89%
pao: 2.73%
rakhine: 0.74%
shan: 0.89%

Combined Character and Syllable-based Detection:
dawei: 93.82%
mon: 0.19%
bamar: 2.45%
beik: 0.46%
po_kayin: 0.45%
sgaw_kayin: 0.45%
pao: 1.37%
rakhine: 0.37%
shan: 0.45%
Running with ngram=4 on random sentence 3: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 79.53%
mon: 1.56%
bamar: 2.04%
beik: 4.91%
po_kayin: 3.59%
sgaw_kayin: 3.59%
pao: 0.96%
rakhine: 0.27%
shan: 3.57%

Combined Character and Syllable-based Detection:
dawei: 89.76%
mon: 0.78%
bamar: 1.02%
beik: 2.45%
po_kayin: 1.80%
sgaw_kayin: 1.80%
pao: 0.48%
rakhine: 0.13%
shan: 1.78%
Running with ngram=4 on random sentence 4: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 87.64%
mon: 0.39%
bamar: 4.90%
beik: 0.92%
po_kayin: 0.89%
sgaw_kayin: 0.89%
pao: 2.73%
rakhine: 0.74%
shan: 0.89%

Combined Character and Syllable-based Detection:
dawei: 93.82%
mon: 0.19%
bamar: 2.45%
beik: 0.46%
po_kayin: 0.45%
sgaw_kayin: 0.45%
pao: 1.37%
rakhine: 0.37%
shan: 0.45%
Running with ngram=4 on random sentence 5: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.44%
mon: 0.00%
bamar: 1.04%
beik: 77.46%
po_kayin: 0.01%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 21.03%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 50.22%
mon: 0.00%
bamar: 0.52%
beik: 38.73%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 10.51%
shan: 0.00%
Running with ngram=4 on random sentence 6: ဟှယ်လူလေဟှိုမေးကေ့နူး။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 79.53%
mon: 1.56%
bamar: 2.04%
beik: 4.91%
po_kayin: 3.59%
sgaw_kayin: 3.59%
pao: 0.96%
rakhine: 0.27%
shan: 3.57%

Combined Character and Syllable-based Detection:
dawei: 89.76%
mon: 0.78%
bamar: 1.02%
beik: 2.45%
po_kayin: 1.80%
sgaw_kayin: 1.80%
pao: 0.48%
rakhine: 0.13%
shan: 1.78%
Running with ngram=4 on random sentence 7: အဲဝယ်ဟှားဟှိုလက်ထပ်လိုက်ဇာလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 80.26%
mon: 3.08%
bamar: 0.09%
beik: 10.04%
po_kayin: 0.64%
sgaw_kayin: 0.64%
pao: 0.24%
rakhine: 4.37%
shan: 0.64%

Combined Character and Syllable-based Detection:
dawei: 90.13%
mon: 1.54%
bamar: 0.05%
beik: 5.02%
po_kayin: 0.32%
sgaw_kayin: 0.32%
pao: 0.12%
rakhine: 2.19%
shan: 0.32%
Running with ngram=4 on random sentence 8: အဲမိုထဲမှာဝေးကိုဖုန်းပြောဇာရတိုင်းများဟှယ်။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.44%
mon: 0.00%
bamar: 1.04%
beik: 77.46%
po_kayin: 0.01%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 21.03%
shan: 0.01%

Combined Character and Syllable-based Detection:
dawei: 50.22%
mon: 0.00%
bamar: 0.52%
beik: 38.73%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 10.51%
shan: 0.00%
Running with ngram=4 on random sentence 9: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 81.95%
mon: 0.02%
bamar: 0.01%
beik: 17.88%
po_kayin: 0.02%
sgaw_kayin: 0.00%
pao: 0.07%
rakhine: 0.02%
shan: 0.04%

Combined Character and Syllable-based Detection:
dawei: 90.97%
mon: 0.01%
bamar: 0.00%
beik: 8.94%
po_kayin: 0.01%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 0.01%
shan: 0.02%
Running with ngram=4 on random sentence 10: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
dawei: 100.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 31.86%
mon: 1.03%
bamar: 0.00%
beik: 50.00%
po_kayin: 0.08%
sgaw_kayin: 0.00%
pao: 0.02%
rakhine: 16.75%
shan: 0.26%

Combined Character and Syllable-based Detection:
dawei: 65.93%
mon: 0.51%
bamar: 0.00%
beik: 25.00%
po_kayin: 0.04%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 8.38%
shan: 0.13%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 1: အဲဟှိုသွားဟှို့နန့်ဟှိုငါတိုက်တွန်းဟှ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.27%
rakhine: 9.89%
dawei: 25.23%
pao: 0.42%
po_kayin: 2.27%
bamar: 9.41%
mon: 4.97%
shan: 2.27%
beik: 45.27%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.13%
rakhine: 4.95%
dawei: 62.62%
pao: 0.21%
po_kayin: 1.13%
bamar: 4.71%
mon: 2.48%
shan: 1.13%
beik: 22.64%
Running with ngram=5 on random sentence 2: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 1.05%
dawei: 88.35%
pao: 0.27%
po_kayin: 1.08%
bamar: 0.01%
mon: 0.30%
shan: 3.71%
beik: 5.18%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 0.52%
dawei: 94.18%
pao: 0.13%
po_kayin: 0.54%
bamar: 0.01%
mon: 0.15%
shan: 1.86%
beik: 2.59%
Running with ngram=5 on random sentence 3: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.83%
rakhine: 5.86%
dawei: 53.45%
pao: 7.00%
po_kayin: 6.83%
bamar: 1.54%
mon: 2.06%
shan: 6.83%
beik: 9.62%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.41%
rakhine: 2.93%
dawei: 76.72%
pao: 3.50%
po_kayin: 3.41%
bamar: 0.77%
mon: 1.03%
shan: 3.41%
beik: 4.81%
Running with ngram=5 on random sentence 4: အယ်ထဲမှာဝီးပြောဖောင်းပြောဇာရရာများဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.91%
rakhine: 0.09%
dawei: 92.65%
pao: 0.07%
po_kayin: 2.25%
bamar: 0.04%
mon: 0.93%
shan: 2.23%
beik: 0.83%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 0.04%
dawei: 96.33%
pao: 0.04%
po_kayin: 1.12%
bamar: 0.02%
mon: 0.47%
shan: 1.11%
beik: 0.42%
Running with ngram=5 on random sentence 5: သူးနို့ဟှယ်လော့သတ္တိရှိဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 6.83%
rakhine: 5.86%
dawei: 53.45%
pao: 7.00%
po_kayin: 6.83%
bamar: 1.54%
mon: 2.06%
shan: 6.83%
beik: 9.62%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.41%
rakhine: 2.93%
dawei: 76.72%
pao: 3.50%
po_kayin: 3.41%
bamar: 0.77%
mon: 1.03%
shan: 3.41%
beik: 4.81%
Running with ngram=5 on random sentence 6: ခံဗျားခရီးထွပ်ဟှလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.79%
rakhine: 6.63%
dawei: 77.62%
pao: 2.79%
po_kayin: 2.79%
bamar: 0.57%
mon: 1.21%
shan: 2.79%
beik: 2.79%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.40%
rakhine: 3.31%
dawei: 88.81%
pao: 1.40%
po_kayin: 1.40%
bamar: 0.28%
mon: 0.60%
shan: 1.40%
beik: 1.40%
Running with ngram=5 on random sentence 7: အဲဝယ်ဟှားဟှိုလက်ထပ်လိုက်ဇာလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.33%
rakhine: 36.54%
dawei: 1.72%
pao: 0.02%
po_kayin: 0.33%
bamar: 0.01%
mon: 0.94%
shan: 0.33%
beik: 59.79%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 18.27%
dawei: 50.86%
pao: 0.01%
po_kayin: 0.16%
bamar: 0.00%
mon: 0.47%
shan: 0.16%
beik: 29.90%
Running with ngram=5 on random sentence 8: နန်ငါ့ဟှိုရှင်းပြပါလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 1.05%
dawei: 88.35%
pao: 0.27%
po_kayin: 1.08%
bamar: 0.01%
mon: 0.30%
shan: 3.71%
beik: 5.18%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 0.52%
dawei: 94.18%
pao: 0.13%
po_kayin: 0.54%
bamar: 0.01%
mon: 0.15%
shan: 1.86%
beik: 2.59%
Running with ngram=5 on random sentence 9: ဟှယ်လော့စိလှုပ်ရှားဟှယ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 9.76%
rakhine: 9.76%
dawei: 35.99%
pao: 9.76%
po_kayin: 9.76%
bamar: 1.23%
mon: 4.23%
shan: 9.76%
beik: 9.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 4.88%
rakhine: 4.88%
dawei: 68.00%
pao: 4.88%
po_kayin: 4.88%
bamar: 0.61%
mon: 2.11%
shan: 4.88%
beik: 4.88%
Running with ngram=5 on random sentence 10: အယ်ဝယ်ဟှားအဲ့မာဂိုလိုရှင်ဟှယ်မှုဝလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 100.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.04%
rakhine: 0.07%
dawei: 88.96%
pao: 0.05%
po_kayin: 0.83%
bamar: 0.00%
mon: 0.09%
shan: 0.38%
beik: 9.57%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 0.04%
dawei: 94.48%
pao: 0.03%
po_kayin: 0.41%
bamar: 0.00%
mon: 0.05%
shan: 0.19%
beik: 4.78%

Processing file: mon_tst.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 38.04%
mon: 59.24%
shan: 0.83%
pao: 0.20%
rakhine: 0.12%
po_kayin: 1.03%
sgaw_kayin: 0.23%
dawei: 0.19%
bamar: 0.12%

Combined Character and Syllable-based Detection:
beik: 19.02%
mon: 79.62%
shan: 0.41%
pao: 0.10%
rakhine: 0.06%
po_kayin: 0.52%
sgaw_kayin: 0.12%
dawei: 0.09%
bamar: 0.06%
Running with ngram=3 on random sentence 1: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 2: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 3: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 5: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 6: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 7.47%
mon: 6.13%
shan: 8.51%
pao: 3.67%
rakhine: 4.62%
po_kayin: 36.54%
sgaw_kayin: 20.30%
dawei: 3.17%
bamar: 9.58%

Combined Character and Syllable-based Detection:
beik: 3.73%
mon: 53.07%
shan: 4.26%
pao: 1.84%
rakhine: 2.31%
po_kayin: 18.27%
sgaw_kayin: 10.15%
dawei: 1.59%
bamar: 4.79%
Running with ngram=3 on random sentence 8: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 9: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=3 on random sentence 10: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.66%
mon: 94.68%
shan: 0.66%
pao: 0.66%
rakhine: 0.66%
po_kayin: 0.66%
sgaw_kayin: 0.66%
dawei: 0.66%
bamar: 0.66%

Combined Character and Syllable-based Detection:
beik: 0.33%
mon: 97.34%
shan: 0.33%
pao: 0.33%
rakhine: 0.33%
po_kayin: 0.33%
sgaw_kayin: 0.33%
dawei: 0.33%
bamar: 0.33%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.28%
mon: 87.31%
bamar: 0.01%
beik: 3.17%
po_kayin: 1.02%
sgaw_kayin: 0.08%
pao: 0.65%
rakhine: 0.83%
shan: 5.64%

Combined Character and Syllable-based Detection:
dawei: 0.64%
mon: 93.65%
bamar: 0.01%
beik: 1.59%
po_kayin: 0.51%
sgaw_kayin: 0.04%
pao: 0.33%
rakhine: 0.42%
shan: 2.82%
Running with ngram=4 on random sentence 1: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 2: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 5: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 6: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 8: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.11%
mon: 11.11%
bamar: 11.11%
beik: 11.11%
po_kayin: 11.11%
sgaw_kayin: 11.11%
pao: 11.11%
rakhine: 11.11%
shan: 11.11%

Combined Character and Syllable-based Detection:
dawei: 5.56%
mon: 55.56%
bamar: 5.56%
beik: 5.56%
po_kayin: 5.56%
sgaw_kayin: 5.56%
pao: 5.56%
rakhine: 5.56%
shan: 5.56%
Running with ngram=4 on random sentence 9: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 10: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.60%
dawei: 2.59%
pao: 0.82%
po_kayin: 0.97%
bamar: 0.02%
mon: 80.41%
shan: 11.43%
beik: 3.01%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.30%
dawei: 1.30%
pao: 0.41%
po_kayin: 0.48%
bamar: 0.01%
mon: 90.20%
shan: 5.72%
beik: 1.50%
Running with ngram=5 on random sentence 1: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 2: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 3: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 4: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 5: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 6: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 8: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 9: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%
Running with ngram=5 on random sentence 10: ကသပ်ပ္ဍဲဗှ်ေဂှ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Processing file: mon.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 87.38%
mon: 5.07%
shan: 0.01%
pao: 0.00%
rakhine: 0.11%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 7.42%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 43.69%
mon: 52.53%
shan: 0.00%
pao: 0.00%
rakhine: 0.05%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 3.71%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ဗှ်ေဟယျတုဲမာန်ဟာ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.19%
mon: 82.34%
shan: 1.85%
pao: 1.50%
rakhine: 1.07%
po_kayin: 1.85%
sgaw_kayin: 1.85%
dawei: 1.85%
bamar: 6.49%

Combined Character and Syllable-based Detection:
beik: 0.59%
mon: 91.17%
shan: 0.93%
pao: 0.75%
rakhine: 0.54%
po_kayin: 0.93%
sgaw_kayin: 0.93%
dawei: 0.93%
bamar: 3.24%
Running with ngram=3 on random sentence 3: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 5.10%
mon: 35.93%
shan: 5.81%
pao: 2.51%
rakhine: 3.15%
po_kayin: 24.94%
sgaw_kayin: 13.85%
dawei: 2.17%
bamar: 6.54%

Combined Character and Syllable-based Detection:
beik: 2.55%
mon: 67.96%
shan: 2.91%
pao: 1.25%
rakhine: 1.58%
po_kayin: 12.47%
sgaw_kayin: 6.93%
dawei: 1.08%
bamar: 3.27%
Running with ngram=3 on random sentence 4: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 9.30%
mon: 90.36%
shan: 0.05%
pao: 0.00%
rakhine: 0.06%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.23%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 4.65%
mon: 95.18%
shan: 0.02%
pao: 0.00%
rakhine: 0.03%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=3 on random sentence 5: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 84.52%
mon: 3.82%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 11.62%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 42.26%
mon: 51.91%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 5.81%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.32%
mon: 99.33%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.28%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.16%
mon: 99.67%
shan: 0.03%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.14%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 84.52%
mon: 3.82%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 11.62%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 42.26%
mon: 51.91%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 5.81%
bamar: 0.00%
Running with ngram=3 on random sentence 8: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 84.52%
mon: 3.82%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 11.62%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 42.26%
mon: 51.91%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 5.81%
bamar: 0.00%
Running with ngram=3 on random sentence 9: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 76.25%
mon: 16.53%
shan: 2.06%
pao: 0.18%
rakhine: 0.36%
po_kayin: 1.00%
sgaw_kayin: 2.61%
dawei: 0.97%
bamar: 0.06%

Combined Character and Syllable-based Detection:
beik: 38.12%
mon: 58.26%
shan: 1.03%
pao: 0.09%
rakhine: 0.18%
po_kayin: 0.50%
sgaw_kayin: 1.30%
dawei: 0.49%
bamar: 0.03%
Running with ngram=3 on random sentence 10: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
beik: 0.00%
mon: 100.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 9.30%
mon: 90.36%
shan: 0.05%
pao: 0.00%
rakhine: 0.06%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.23%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 4.65%
mon: 95.18%
shan: 0.02%
pao: 0.00%
rakhine: 0.03%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.11%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 24.19%
bamar: 0.00%
beik: 75.81%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 62.10%
bamar: 0.00%
beik: 37.90%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.43%
mon: 14.16%
bamar: 0.36%
beik: 19.84%
po_kayin: 14.05%
sgaw_kayin: 2.65%
pao: 5.59%
rakhine: 12.28%
shan: 22.64%

Combined Character and Syllable-based Detection:
dawei: 4.22%
mon: 57.08%
bamar: 0.18%
beik: 9.92%
po_kayin: 7.02%
sgaw_kayin: 1.33%
pao: 2.79%
rakhine: 6.14%
shan: 11.32%
Running with ngram=4 on random sentence 2: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.67%
mon: 6.59%
bamar: 0.08%
beik: 86.06%
po_kayin: 0.18%
sgaw_kayin: 0.02%
pao: 0.14%
rakhine: 4.63%
shan: 0.62%

Combined Character and Syllable-based Detection:
dawei: 0.84%
mon: 53.29%
bamar: 0.04%
beik: 43.03%
po_kayin: 0.09%
sgaw_kayin: 0.01%
pao: 0.07%
rakhine: 2.31%
shan: 0.31%
Running with ngram=4 on random sentence 3: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 4: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 6.26%
mon: 79.23%
bamar: 0.35%
beik: 6.58%
po_kayin: 2.99%
sgaw_kayin: 0.14%
pao: 0.74%
rakhine: 0.76%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 3.13%
mon: 89.61%
bamar: 0.17%
beik: 3.29%
po_kayin: 1.49%
sgaw_kayin: 0.07%
pao: 0.37%
rakhine: 0.38%
shan: 1.48%
Running with ngram=4 on random sentence 5: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.14%
mon: 16.71%
bamar: 0.34%
beik: 19.15%
po_kayin: 13.56%
sgaw_kayin: 2.56%
pao: 5.85%
rakhine: 11.85%
shan: 21.85%

Combined Character and Syllable-based Detection:
dawei: 4.07%
mon: 58.35%
bamar: 0.17%
beik: 9.57%
po_kayin: 6.78%
sgaw_kayin: 1.28%
pao: 2.92%
rakhine: 5.92%
shan: 10.92%
Running with ngram=4 on random sentence 6: ပေါဲဂီတဂှ်ဂိတုဂတမှကၠောန်ဏောၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 33.85%
mon: 52.94%
bamar: 0.00%
beik: 8.69%
po_kayin: 1.68%
sgaw_kayin: 0.01%
pao: 0.99%
rakhine: 0.21%
shan: 1.65%

Combined Character and Syllable-based Detection:
dawei: 16.92%
mon: 76.47%
bamar: 0.00%
beik: 4.34%
po_kayin: 0.84%
sgaw_kayin: 0.00%
pao: 0.49%
rakhine: 0.10%
shan: 0.82%
Running with ngram=4 on random sentence 7: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.03%
mon: 12.08%
bamar: 2.27%
beik: 11.58%
po_kayin: 2.47%
sgaw_kayin: 32.05%
pao: 7.79%
rakhine: 4.91%
shan: 15.81%

Combined Character and Syllable-based Detection:
dawei: 5.51%
mon: 56.04%
bamar: 1.14%
beik: 5.79%
po_kayin: 1.23%
sgaw_kayin: 16.02%
pao: 3.90%
rakhine: 2.46%
shan: 7.91%
Running with ngram=4 on random sentence 8: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 8.43%
mon: 14.16%
bamar: 0.36%
beik: 19.84%
po_kayin: 14.05%
sgaw_kayin: 2.65%
pao: 5.59%
rakhine: 12.28%
shan: 22.64%

Combined Character and Syllable-based Detection:
dawei: 4.22%
mon: 57.08%
bamar: 0.18%
beik: 9.92%
po_kayin: 7.02%
sgaw_kayin: 1.33%
pao: 2.79%
rakhine: 6.14%
shan: 11.32%
Running with ngram=4 on random sentence 9: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 6.26%
mon: 79.23%
bamar: 0.35%
beik: 6.58%
po_kayin: 2.99%
sgaw_kayin: 0.14%
pao: 0.74%
rakhine: 0.76%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 3.13%
mon: 89.61%
bamar: 0.17%
beik: 3.29%
po_kayin: 1.49%
sgaw_kayin: 0.07%
pao: 0.37%
rakhine: 0.38%
shan: 1.48%
Running with ngram=4 on random sentence 10: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
dawei: 0.00%
mon: 100.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 6.26%
mon: 79.23%
bamar: 0.35%
beik: 6.58%
po_kayin: 2.99%
sgaw_kayin: 0.14%
pao: 0.74%
rakhine: 0.76%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 3.13%
mon: 89.61%
bamar: 0.17%
beik: 3.29%
po_kayin: 1.49%
sgaw_kayin: 0.07%
pao: 0.37%
rakhine: 0.38%
shan: 1.48%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 99.93%
shan: 0.06%
beik: 0.01%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 99.97%
shan: 0.03%
beik: 0.00%
Running with ngram=5 on random sentence 1: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.84%
rakhine: 15.02%
dawei: 15.02%
pao: 15.02%
po_kayin: 4.37%
bamar: 15.02%
mon: 10.70%
shan: 6.98%
beik: 15.02%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.42%
rakhine: 7.51%
dawei: 7.51%
pao: 7.51%
po_kayin: 2.19%
bamar: 7.51%
mon: 55.35%
shan: 3.49%
beik: 7.51%
Running with ngram=5 on random sentence 2: ဂလာန်ဗှ်ေပတိုန်လဝ်နူဏေအ်ဗ္တံဂှ်ခိုဟ်ကွေံကွေံ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.20%
rakhine: 5.10%
dawei: 18.78%
pao: 5.03%
po_kayin: 18.78%
bamar: 2.36%
mon: 10.20%
shan: 18.78%
beik: 18.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.10%
rakhine: 2.55%
dawei: 9.39%
pao: 2.51%
po_kayin: 9.39%
bamar: 1.18%
mon: 55.10%
shan: 9.39%
beik: 9.39%
Running with ngram=5 on random sentence 3: ပ္ဍဲဗှ်ေဂှ်ကသပ်တၟေၚ်ၚ်နွံမံၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.84%
rakhine: 15.02%
dawei: 15.02%
pao: 15.02%
po_kayin: 4.37%
bamar: 15.02%
mon: 10.70%
shan: 6.98%
beik: 15.02%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.42%
rakhine: 7.51%
dawei: 7.51%
pao: 7.51%
po_kayin: 2.19%
bamar: 7.51%
mon: 55.35%
shan: 3.49%
beik: 7.51%
Running with ngram=5 on random sentence 4: အဲဟယျဗှ်ေတိၚ်ဂီတာလေပ်မံၚ်။
Character-based Detection:
sgaw_kayin: 0.37%
rakhine: 0.04%
dawei: 0.23%
pao: 0.37%
po_kayin: 0.37%
bamar: 0.01%
mon: 97.84%
shan: 0.37%
beik: 0.37%

Syllable-based Detection:
sgaw_kayin: 3.65%
rakhine: 2.30%
dawei: 11.58%
pao: 8.33%
po_kayin: 9.05%
bamar: 0.49%
mon: 20.71%
shan: 31.12%
beik: 12.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 2.01%
rakhine: 1.17%
dawei: 5.90%
pao: 4.35%
po_kayin: 4.71%
bamar: 0.25%
mon: 59.28%
shan: 15.75%
beik: 6.58%
Running with ngram=5 on random sentence 5: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.19%
rakhine: 1.08%
dawei: 20.06%
pao: 3.86%
po_kayin: 4.56%
bamar: 0.23%
mon: 31.33%
shan: 15.55%
beik: 22.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.60%
rakhine: 0.54%
dawei: 10.03%
pao: 1.93%
po_kayin: 2.28%
bamar: 0.11%
mon: 65.67%
shan: 7.77%
beik: 11.07%
Running with ngram=5 on random sentence 6: ခိုဟ်ယျဆက်ဂစာန်ညိပၠန်။
Character-based Detection:
sgaw_kayin: 0.12%
rakhine: 0.12%
dawei: 0.12%
pao: 0.12%
po_kayin: 0.12%
bamar: 0.12%
mon: 99.05%
shan: 0.12%
beik: 0.12%

Syllable-based Detection:
sgaw_kayin: 2.97%
rakhine: 15.76%
dawei: 15.76%
pao: 4.22%
po_kayin: 15.76%
bamar: 1.98%
mon: 12.01%
shan: 15.76%
beik: 15.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.55%
rakhine: 7.94%
dawei: 7.94%
pao: 2.17%
po_kayin: 7.94%
bamar: 1.05%
mon: 55.53%
shan: 7.94%
beik: 7.94%
Running with ngram=5 on random sentence 7: လၟုဟ်အဲဗ္တောန်တိၚ်မံၚ်ဂီတာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.48%
rakhine: 2.19%
dawei: 11.06%
pao: 7.96%
po_kayin: 8.65%
bamar: 0.47%
mon: 24.25%
shan: 29.73%
beik: 12.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.74%
rakhine: 1.10%
dawei: 5.53%
pao: 3.98%
po_kayin: 4.32%
bamar: 0.23%
mon: 62.13%
shan: 14.87%
beik: 6.10%
Running with ngram=5 on random sentence 8: ၜိုတ်အဲကၠောန်မာန်အဲဂစာန်လဝ်ရ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.06%
rakhine: 0.44%
dawei: 5.00%
pao: 0.42%
po_kayin: 0.54%
bamar: 0.09%
mon: 81.30%
shan: 6.35%
beik: 5.80%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.03%
rakhine: 0.22%
dawei: 2.50%
pao: 0.21%
po_kayin: 0.27%
bamar: 0.05%
mon: 90.65%
shan: 3.18%
beik: 2.90%
Running with ngram=5 on random sentence 9: သွက်အဲဂွံအံၚ်ဇၞးရာဒနာကဵုညိ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.11%
rakhine: 1.32%
dawei: 9.29%
pao: 0.21%
po_kayin: 11.91%
bamar: 0.01%
mon: 25.45%
shan: 40.94%
beik: 10.77%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.05%
rakhine: 0.66%
dawei: 4.64%
pao: 0.10%
po_kayin: 5.95%
bamar: 0.01%
mon: 62.73%
shan: 20.47%
beik: 5.38%
Running with ngram=5 on random sentence 10: ယဝ်ဗှ်ေဟွံပယှုက်အဲရတှ်ေတုဲမာန်ဏောၚ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 100.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.19%
rakhine: 1.08%
dawei: 20.06%
pao: 3.86%
po_kayin: 4.56%
bamar: 0.23%
mon: 31.33%
shan: 15.55%
beik: 22.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.60%
rakhine: 0.54%
dawei: 10.03%
pao: 1.93%
po_kayin: 2.28%
bamar: 0.11%
mon: 65.67%
shan: 7.77%
beik: 11.07%

Processing file: pao.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.46%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.53%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.73%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.26%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 94.31%
mon: 0.71%
shan: 0.13%
pao: 3.73%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 1.08%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 47.16%
mon: 0.35%
shan: 0.07%
pao: 51.86%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.54%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.46%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.53%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.73%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.26%
bamar: 0.00%
Running with ngram=3 on random sentence 4: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.39%
mon: 0.01%
shan: 0.01%
pao: 99.57%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.20%
mon: 0.00%
shan: 0.01%
pao: 99.79%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 5: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.39%
mon: 0.01%
shan: 0.01%
pao: 99.57%
rakhine: 0.01%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.20%
mon: 0.00%
shan: 0.01%
pao: 99.79%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 94.31%
mon: 0.71%
shan: 0.13%
pao: 3.73%
rakhine: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.00%
dawei: 1.08%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 47.16%
mon: 0.35%
shan: 0.07%
pao: 51.86%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.54%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.46%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.53%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.73%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.26%
bamar: 0.00%
Running with ngram=3 on random sentence 8: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 14.16%
mon: 6.25%
shan: 0.64%
pao: 70.71%
rakhine: 0.49%
po_kayin: 0.10%
sgaw_kayin: 0.42%
dawei: 6.74%
bamar: 0.50%

Combined Character and Syllable-based Detection:
beik: 7.08%
mon: 3.12%
shan: 0.32%
pao: 85.35%
rakhine: 0.24%
po_kayin: 0.05%
sgaw_kayin: 0.21%
dawei: 3.37%
bamar: 0.25%
Running with ngram=3 on random sentence 9: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 25.86%
mon: 3.38%
shan: 3.38%
pao: 32.17%
rakhine: 8.51%
po_kayin: 3.38%
sgaw_kayin: 3.38%
dawei: 5.38%
bamar: 14.55%

Combined Character and Syllable-based Detection:
beik: 12.93%
mon: 1.69%
shan: 1.69%
pao: 66.08%
rakhine: 4.26%
po_kayin: 1.69%
sgaw_kayin: 1.69%
dawei: 2.69%
bamar: 7.27%
Running with ngram=3 on random sentence 10: ဆုဲင်ꩻသွတ်တလဲင်ႏရက်ဒျာႏဝွေꩻနဝ်ꩻတဲ့ဒေါ့ꩻခွင်ꩻတလတဝ်းဒွုမ်
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 100.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.46%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.53%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.73%
mon: 0.00%
shan: 0.00%
pao: 50.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.26%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 18.89%
mon: 5.91%
bamar: 2.75%
beik: 20.85%
po_kayin: 2.67%
sgaw_kayin: 0.43%
pao: 1.92%
rakhine: 15.10%
shan: 31.48%

Combined Character and Syllable-based Detection:
dawei: 9.45%
mon: 2.95%
bamar: 1.38%
beik: 10.43%
po_kayin: 1.33%
sgaw_kayin: 0.22%
pao: 50.96%
rakhine: 7.55%
shan: 15.74%
Running with ngram=4 on random sentence 2: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 3: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 18.89%
mon: 5.91%
bamar: 2.75%
beik: 20.85%
po_kayin: 2.67%
sgaw_kayin: 0.43%
pao: 1.92%
rakhine: 15.10%
shan: 31.48%

Combined Character and Syllable-based Detection:
dawei: 9.45%
mon: 2.95%
bamar: 1.38%
beik: 10.43%
po_kayin: 1.33%
sgaw_kayin: 0.22%
pao: 50.96%
rakhine: 7.55%
shan: 15.74%
Running with ngram=4 on random sentence 4: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.91%
mon: 0.60%
bamar: 0.16%
beik: 2.18%
po_kayin: 0.93%
sgaw_kayin: 0.15%
pao: 92.65%
rakhine: 0.51%
shan: 0.92%

Combined Character and Syllable-based Detection:
dawei: 0.96%
mon: 0.30%
bamar: 0.08%
beik: 1.09%
po_kayin: 0.46%
sgaw_kayin: 0.08%
pao: 96.32%
rakhine: 0.26%
shan: 0.46%
Running with ngram=4 on random sentence 5: နဝ်ꩻနဝ်ꩻနီအတာႏယပ်ခုဲင်ႏငါႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 2.90%
mon: 2.06%
bamar: 0.19%
beik: 3.04%
po_kayin: 1.38%
sgaw_kayin: 0.56%
pao: 83.83%
rakhine: 1.29%
shan: 4.75%

Combined Character and Syllable-based Detection:
dawei: 1.45%
mon: 1.03%
bamar: 0.10%
beik: 1.52%
po_kayin: 0.69%
sgaw_kayin: 0.28%
pao: 91.92%
rakhine: 0.65%
shan: 2.37%
Running with ngram=4 on random sentence 6: နဝ်ꩻနဝ်ꩻခွေယမ်းမာႏဗာႏဟောင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 13.13%
mon: 13.13%
bamar: 7.52%
beik: 13.13%
po_kayin: 13.13%
sgaw_kayin: 13.13%
pao: 3.81%
rakhine: 5.75%
shan: 17.26%

Combined Character and Syllable-based Detection:
dawei: 6.57%
mon: 6.57%
bamar: 3.76%
beik: 6.57%
po_kayin: 6.57%
sgaw_kayin: 6.57%
pao: 51.90%
rakhine: 2.88%
shan: 8.63%
Running with ngram=4 on random sentence 7: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 9.10%
mon: 4.53%
bamar: 0.35%
beik: 56.77%
po_kayin: 0.89%
sgaw_kayin: 0.14%
pao: 19.47%
rakhine: 5.73%
shan: 3.02%

Combined Character and Syllable-based Detection:
dawei: 4.55%
mon: 2.26%
bamar: 0.18%
beik: 28.39%
po_kayin: 0.44%
sgaw_kayin: 0.07%
pao: 59.73%
rakhine: 2.87%
shan: 1.51%
Running with ngram=4 on random sentence 8: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.91%
mon: 0.60%
bamar: 0.16%
beik: 2.18%
po_kayin: 0.93%
sgaw_kayin: 0.15%
pao: 92.65%
rakhine: 0.51%
shan: 0.92%

Combined Character and Syllable-based Detection:
dawei: 0.96%
mon: 0.30%
bamar: 0.08%
beik: 1.09%
po_kayin: 0.46%
sgaw_kayin: 0.08%
pao: 96.32%
rakhine: 0.26%
shan: 0.46%
Running with ngram=4 on random sentence 9: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 22.07%
mon: 4.55%
bamar: 1.32%
beik: 10.85%
po_kayin: 3.06%
sgaw_kayin: 31.38%
pao: 1.89%
rakhine: 21.84%
shan: 3.03%

Combined Character and Syllable-based Detection:
dawei: 11.04%
mon: 2.28%
bamar: 0.66%
beik: 5.43%
po_kayin: 1.53%
sgaw_kayin: 15.69%
pao: 50.95%
rakhine: 10.92%
shan: 1.51%
Running with ngram=4 on random sentence 10: ခွေစဥ်ꩻစာꩻအတွိုင်ꩻစဥ်ꩻစာꩻဟုဲင်း
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 100.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 18.89%
mon: 5.91%
bamar: 2.75%
beik: 20.85%
po_kayin: 2.67%
sgaw_kayin: 0.43%
pao: 1.92%
rakhine: 15.10%
shan: 31.48%

Combined Character and Syllable-based Detection:
dawei: 9.45%
mon: 2.95%
bamar: 1.38%
beik: 10.43%
po_kayin: 1.33%
sgaw_kayin: 0.22%
pao: 50.96%
rakhine: 7.55%
shan: 15.74%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 99.77%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 99.89%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.11%
Running with ngram=5 on random sentence 1: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 2.31%
dawei: 7.60%
pao: 2.86%
po_kayin: 2.84%
bamar: 0.07%
mon: 14.51%
shan: 9.66%
beik: 59.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.23%
rakhine: 1.16%
dawei: 3.80%
pao: 51.43%
po_kayin: 1.42%
bamar: 0.03%
mon: 7.26%
shan: 4.83%
beik: 29.84%
Running with ngram=5 on random sentence 2: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 2.31%
dawei: 7.60%
pao: 2.86%
po_kayin: 2.84%
bamar: 0.07%
mon: 14.51%
shan: 9.66%
beik: 59.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.23%
rakhine: 1.16%
dawei: 3.80%
pao: 51.43%
po_kayin: 1.42%
bamar: 0.03%
mon: 7.26%
shan: 4.83%
beik: 29.84%
Running with ngram=5 on random sentence 3: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.57%
rakhine: 8.28%
dawei: 18.58%
pao: 3.45%
po_kayin: 8.86%
bamar: 3.83%
mon: 13.19%
shan: 8.78%
beik: 31.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.78%
rakhine: 4.14%
dawei: 9.29%
pao: 51.73%
po_kayin: 4.43%
bamar: 1.91%
mon: 6.60%
shan: 4.39%
beik: 15.73%
Running with ngram=5 on random sentence 4: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 2.31%
dawei: 7.60%
pao: 2.86%
po_kayin: 2.84%
bamar: 0.07%
mon: 14.51%
shan: 9.66%
beik: 59.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.23%
rakhine: 1.16%
dawei: 3.80%
pao: 51.43%
po_kayin: 1.42%
bamar: 0.03%
mon: 7.26%
shan: 4.83%
beik: 29.84%
Running with ngram=5 on random sentence 5: တယ်ႏနာဆာဒုံးပျံထင်ႏစခိန်ႏနဝ်ꩻဝွေꩻတဲမ်းဗာႏဒျာႏမတ်တန်ꩻ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 1.28%
rakhine: 5.26%
dawei: 21.48%
pao: 2.78%
po_kayin: 16.80%
bamar: 0.44%
mon: 10.83%
shan: 16.65%
beik: 24.48%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.64%
rakhine: 2.63%
dawei: 10.74%
pao: 51.39%
po_kayin: 8.40%
bamar: 0.22%
mon: 5.41%
shan: 8.32%
beik: 12.24%
Running with ngram=5 on random sentence 6: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 2.31%
dawei: 7.60%
pao: 2.86%
po_kayin: 2.84%
bamar: 0.07%
mon: 14.51%
shan: 9.66%
beik: 59.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.23%
rakhine: 1.16%
dawei: 3.80%
pao: 51.43%
po_kayin: 1.42%
bamar: 0.03%
mon: 7.26%
shan: 4.83%
beik: 29.84%
Running with ngram=5 on random sentence 7: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.16%
dawei: 0.16%
pao: 98.75%
po_kayin: 0.16%
bamar: 0.16%
mon: 0.16%
shan: 0.16%
beik: 0.16%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.08%
dawei: 0.08%
pao: 99.37%
po_kayin: 0.08%
bamar: 0.08%
mon: 0.08%
shan: 0.08%
beik: 0.08%
Running with ngram=5 on random sentence 8: ဒေါ့ꩻဝင်ꩻမဉ်ꩻနဝ်ꩻလွထီႏငါႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.57%
rakhine: 8.28%
dawei: 18.58%
pao: 3.45%
po_kayin: 8.86%
bamar: 3.83%
mon: 13.19%
shan: 8.78%
beik: 31.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.78%
rakhine: 4.14%
dawei: 9.29%
pao: 51.73%
po_kayin: 4.43%
bamar: 1.91%
mon: 6.60%
shan: 4.39%
beik: 15.73%
Running with ngram=5 on random sentence 9: ကထိန်ꩻ‌နွောင်ꩻဝွေꩻနဝ်ꩻအဝ်ႏဒျာႏနာꩻလွုမ်
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.16%
rakhine: 0.16%
dawei: 0.16%
pao: 98.75%
po_kayin: 0.16%
bamar: 0.16%
mon: 0.16%
shan: 0.16%
beik: 0.16%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.08%
rakhine: 0.08%
dawei: 0.08%
pao: 99.37%
po_kayin: 0.08%
bamar: 0.08%
mon: 0.08%
shan: 0.08%
beik: 0.08%
Running with ngram=5 on random sentence 10: ‌နာꩻကဒေါ့ꩻအတွိုင်ꩻခွေသျင်ꩻပျဗာႏဒျာႏ
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 100.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.46%
rakhine: 2.31%
dawei: 7.60%
pao: 2.86%
po_kayin: 2.84%
bamar: 0.07%
mon: 14.51%
shan: 9.66%
beik: 59.68%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.23%
rakhine: 1.16%
dawei: 3.80%
pao: 51.43%
po_kayin: 1.42%
bamar: 0.03%
mon: 7.26%
shan: 4.83%
beik: 29.84%

Processing file: po_kayin.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.01%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 12.56%
mon: 4.66%
shan: 8.73%
pao: 1.01%
rakhine: 11.39%
po_kayin: 32.86%
sgaw_kayin: 0.68%
dawei: 16.73%
bamar: 11.38%

Combined Character and Syllable-based Detection:
beik: 6.28%
mon: 2.33%
shan: 4.36%
pao: 0.51%
rakhine: 5.70%
po_kayin: 66.43%
sgaw_kayin: 0.34%
dawei: 8.36%
bamar: 5.69%
Running with ngram=3 on random sentence 2: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 1.07%
mon: 0.01%
shan: 0.02%
pao: 0.00%
rakhine: 0.01%
po_kayin: 98.86%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.54%
mon: 0.01%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 99.43%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 89.88%
mon: 0.87%
shan: 2.00%
pao: 0.14%
rakhine: 0.54%
po_kayin: 4.85%
sgaw_kayin: 0.23%
dawei: 1.22%
bamar: 0.25%

Combined Character and Syllable-based Detection:
beik: 44.94%
mon: 0.43%
shan: 1.00%
pao: 0.07%
rakhine: 0.27%
po_kayin: 52.43%
sgaw_kayin: 0.12%
dawei: 0.61%
bamar: 0.13%
Running with ngram=3 on random sentence 4: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 5: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 12.56%
mon: 4.66%
shan: 8.73%
pao: 1.01%
rakhine: 11.39%
po_kayin: 32.86%
sgaw_kayin: 0.68%
dawei: 16.73%
bamar: 11.38%

Combined Character and Syllable-based Detection:
beik: 6.28%
mon: 2.33%
shan: 4.36%
pao: 0.51%
rakhine: 5.70%
po_kayin: 66.43%
sgaw_kayin: 0.34%
dawei: 8.36%
bamar: 5.69%
Running with ngram=3 on random sentence 6: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 89.88%
mon: 0.87%
shan: 2.00%
pao: 0.14%
rakhine: 0.54%
po_kayin: 4.85%
sgaw_kayin: 0.23%
dawei: 1.22%
bamar: 0.25%

Combined Character and Syllable-based Detection:
beik: 44.94%
mon: 0.43%
shan: 1.00%
pao: 0.07%
rakhine: 0.27%
po_kayin: 52.43%
sgaw_kayin: 0.12%
dawei: 0.61%
bamar: 0.13%
Running with ngram=3 on random sentence 8: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.87%
mon: 0.01%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.05%
sgaw_kayin: 0.00%
dawei: 0.02%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.93%
mon: 0.00%
shan: 0.02%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.03%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 9: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.63%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.35%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.82%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 50.18%
sgaw_kayin: 0.00%
dawei: 0.01%
bamar: 0.00%
Running with ngram=3 on random sentence 10: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 15.64%
mon: 0.12%
shan: 0.01%
pao: 0.00%
rakhine: 0.00%
po_kayin: 84.24%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 7.82%
mon: 0.06%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 92.12%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 12.12%
mon: 0.57%
bamar: 0.00%
beik: 37.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 49.61%

Combined Character and Syllable-based Detection:
dawei: 6.06%
mon: 0.28%
bamar: 0.00%
beik: 18.85%
po_kayin: 50.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 24.81%
Running with ngram=4 on random sentence 1: ၦလၧဖီၪ့ဂုးထၬအဝ့ၫကန့နီၪမွဲဒၪနၧၩလီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 11.18%
mon: 40.45%
bamar: 0.15%
beik: 12.34%
po_kayin: 2.66%
sgaw_kayin: 0.05%
pao: 0.93%
rakhine: 2.22%
shan: 30.02%

Combined Character and Syllable-based Detection:
dawei: 5.59%
mon: 20.23%
bamar: 0.08%
beik: 6.17%
po_kayin: 51.33%
sgaw_kayin: 0.02%
pao: 0.46%
rakhine: 1.11%
shan: 15.01%
Running with ngram=4 on random sentence 2: အဝ့ၫထီးန့ၦၡၩဘၪနးဂၩလၧၩ့အ့ၬ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 15.86%
mon: 15.86%
bamar: 15.86%
beik: 15.86%
po_kayin: 0.37%
sgaw_kayin: 0.22%
pao: 4.25%
rakhine: 15.86%
shan: 15.86%

Combined Character and Syllable-based Detection:
dawei: 7.93%
mon: 7.93%
bamar: 7.93%
beik: 7.93%
po_kayin: 50.19%
sgaw_kayin: 0.11%
pao: 2.12%
rakhine: 7.93%
shan: 7.93%
Running with ngram=4 on random sentence 3: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.52%
mon: 2.82%
bamar: 0.02%
beik: 0.58%
po_kayin: 95.51%
sgaw_kayin: 0.02%
pao: 0.03%
rakhine: 0.10%
shan: 0.41%

Combined Character and Syllable-based Detection:
dawei: 0.26%
mon: 1.41%
bamar: 0.01%
beik: 0.29%
po_kayin: 97.75%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.05%
shan: 0.20%
Running with ngram=4 on random sentence 4: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.52%
mon: 2.82%
bamar: 0.02%
beik: 0.58%
po_kayin: 95.51%
sgaw_kayin: 0.02%
pao: 0.03%
rakhine: 0.10%
shan: 0.41%

Combined Character and Syllable-based Detection:
dawei: 0.26%
mon: 1.41%
bamar: 0.01%
beik: 0.29%
po_kayin: 97.75%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.05%
shan: 0.20%
Running with ngram=4 on random sentence 5: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.67%
mon: 2.61%
bamar: 1.97%
beik: 3.86%
po_kayin: 79.11%
sgaw_kayin: 0.70%
pao: 0.43%
rakhine: 1.64%
shan: 6.02%

Combined Character and Syllable-based Detection:
dawei: 1.84%
mon: 1.30%
bamar: 0.98%
beik: 1.93%
po_kayin: 89.55%
sgaw_kayin: 0.35%
pao: 0.22%
rakhine: 0.82%
shan: 3.01%
Running with ngram=4 on random sentence 6: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 19.17%
mon: 13.61%
bamar: 3.95%
beik: 20.14%
po_kayin: 0.48%
sgaw_kayin: 0.43%
pao: 2.25%
rakhine: 8.54%
shan: 31.42%

Combined Character and Syllable-based Detection:
dawei: 9.59%
mon: 6.81%
bamar: 1.97%
beik: 10.07%
po_kayin: 50.24%
sgaw_kayin: 0.22%
pao: 1.13%
rakhine: 4.27%
shan: 15.71%
Running with ngram=4 on random sentence 7: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.67%
mon: 2.61%
bamar: 1.97%
beik: 3.86%
po_kayin: 79.11%
sgaw_kayin: 0.70%
pao: 0.43%
rakhine: 1.64%
shan: 6.02%

Combined Character and Syllable-based Detection:
dawei: 1.84%
mon: 1.30%
bamar: 0.98%
beik: 1.93%
po_kayin: 89.55%
sgaw_kayin: 0.35%
pao: 0.22%
rakhine: 0.82%
shan: 3.01%
Running with ngram=4 on random sentence 8: ဆၧအနီၪမွဲဆၧအကၪလၧပဂးလီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.52%
mon: 2.82%
bamar: 0.02%
beik: 0.58%
po_kayin: 95.51%
sgaw_kayin: 0.02%
pao: 0.03%
rakhine: 0.10%
shan: 0.41%

Combined Character and Syllable-based Detection:
dawei: 0.26%
mon: 1.41%
bamar: 0.01%
beik: 0.29%
po_kayin: 97.75%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 0.05%
shan: 0.20%
Running with ngram=4 on random sentence 9: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.56%
mon: 12.46%
bamar: 9.40%
beik: 18.44%
po_kayin: 0.12%
sgaw_kayin: 3.37%
pao: 2.06%
rakhine: 7.82%
shan: 28.77%

Combined Character and Syllable-based Detection:
dawei: 8.78%
mon: 6.23%
bamar: 4.70%
beik: 9.22%
po_kayin: 50.06%
sgaw_kayin: 1.69%
pao: 1.03%
rakhine: 3.91%
shan: 14.38%
Running with ngram=4 on random sentence 10: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 100.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.67%
mon: 2.61%
bamar: 1.97%
beik: 3.86%
po_kayin: 79.11%
sgaw_kayin: 0.70%
pao: 0.43%
rakhine: 1.64%
shan: 6.02%

Combined Character and Syllable-based Detection:
dawei: 1.84%
mon: 1.30%
bamar: 0.98%
beik: 1.93%
po_kayin: 89.55%
sgaw_kayin: 0.35%
pao: 0.22%
rakhine: 0.82%
shan: 3.01%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 15.38%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.18%
shan: 38.91%
beik: 45.53%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 7.69%
pao: 0.00%
po_kayin: 50.00%
bamar: 0.00%
mon: 0.09%
shan: 19.45%
beik: 22.77%
Running with ngram=5 on random sentence 1: ယယဲးထဲးဘၪဆၧအနီၪဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.23%
rakhine: 7.48%
dawei: 16.80%
pao: 1.97%
po_kayin: 9.95%
bamar: 3.46%
mon: 11.92%
shan: 27.54%
beik: 17.65%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.61%
rakhine: 3.74%
dawei: 8.40%
pao: 0.99%
po_kayin: 54.97%
bamar: 1.73%
mon: 5.96%
shan: 13.77%
beik: 8.82%
Running with ngram=5 on random sentence 2: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.62%
rakhine: 8.63%
dawei: 16.71%
pao: 0.86%
po_kayin: 0.66%
bamar: 0.71%
mon: 8.42%
shan: 44.94%
beik: 18.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.31%
rakhine: 4.31%
dawei: 8.36%
pao: 0.43%
po_kayin: 50.33%
bamar: 0.35%
mon: 4.21%
shan: 22.47%
beik: 9.22%
Running with ngram=5 on random sentence 3: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.42%
rakhine: 8.36%
dawei: 18.76%
pao: 2.20%
po_kayin: 0.24%
bamar: 6.22%
mon: 13.32%
shan: 30.76%
beik: 19.71%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.21%
rakhine: 4.18%
dawei: 9.38%
pao: 1.10%
po_kayin: 50.12%
bamar: 3.11%
mon: 6.66%
shan: 15.38%
beik: 9.85%
Running with ngram=5 on random sentence 4: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.58%
rakhine: 8.31%
dawei: 18.65%
pao: 2.19%
po_kayin: 0.01%
bamar: 3.84%
mon: 13.24%
shan: 30.58%
beik: 19.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.79%
rakhine: 4.15%
dawei: 9.33%
pao: 1.09%
po_kayin: 50.01%
bamar: 1.92%
mon: 6.62%
shan: 15.29%
beik: 9.80%
Running with ngram=5 on random sentence 5: ယအဲၪအဝ့ၫနီၪလခဲၫ့ထုၬကဘျၩ့မၬယလီၩဘၪၥ့ၪလၧၩ့ထၧၩ့ယၫအ့ၬ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.22%
rakhine: 7.29%
dawei: 31.72%
pao: 0.72%
po_kayin: 0.02%
bamar: 0.28%
mon: 11.35%
shan: 11.62%
beik: 36.78%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.11%
rakhine: 3.65%
dawei: 15.86%
pao: 0.36%
po_kayin: 50.01%
bamar: 0.14%
mon: 5.67%
shan: 5.81%
beik: 18.39%
Running with ngram=5 on random sentence 6: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
sgaw_kayin: 4.10%
rakhine: 4.10%
dawei: 4.10%
pao: 4.10%
po_kayin: 67.23%
bamar: 4.10%
mon: 4.10%
shan: 4.10%
beik: 4.10%

Syllable-based Detection:
sgaw_kayin: 3.53%
rakhine: 8.18%
dawei: 18.36%
pao: 2.16%
po_kayin: 1.57%
bamar: 3.78%
mon: 13.03%
shan: 30.10%
beik: 19.29%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.81%
rakhine: 6.14%
dawei: 11.23%
pao: 3.13%
po_kayin: 34.40%
bamar: 3.94%
mon: 8.57%
shan: 17.10%
beik: 11.69%
Running with ngram=5 on random sentence 7: ယဂဲၫထဲၩ့လီၩပျၩ့ထၬကဲၪခိၬနလီၩထၬဆ့လီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.42%
rakhine: 8.36%
dawei: 18.76%
pao: 2.20%
po_kayin: 0.24%
bamar: 6.22%
mon: 13.32%
shan: 30.76%
beik: 19.71%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.21%
rakhine: 4.18%
dawei: 9.38%
pao: 1.10%
po_kayin: 50.12%
bamar: 3.11%
mon: 6.66%
shan: 15.38%
beik: 9.85%
Running with ngram=5 on random sentence 8: ယမ့ၬလဲၩချဲၩ့ၦဂူၫဂၩအလၩ.
Character-based Detection:
sgaw_kayin: 4.10%
rakhine: 4.10%
dawei: 4.10%
pao: 4.10%
po_kayin: 67.23%
bamar: 4.10%
mon: 4.10%
shan: 4.10%
beik: 4.10%

Syllable-based Detection:
sgaw_kayin: 3.53%
rakhine: 8.18%
dawei: 18.36%
pao: 2.16%
po_kayin: 1.57%
bamar: 3.78%
mon: 13.03%
shan: 30.10%
beik: 19.29%

Combined Character and Syllable-based Detection:
sgaw_kayin: 3.81%
rakhine: 6.14%
dawei: 11.23%
pao: 3.13%
po_kayin: 34.40%
bamar: 3.94%
mon: 8.57%
shan: 17.10%
beik: 11.69%
Running with ngram=5 on random sentence 9: နၫဆၫအဆၧယူၩဖျိၬထၪ့ကၠၧၫ့,အဝ့ၫကွ့ၭနဲၫ့ဆၧကၠၧၫ့လ့ၬလီၫ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 3.58%
rakhine: 8.31%
dawei: 18.65%
pao: 2.19%
po_kayin: 0.01%
bamar: 3.84%
mon: 13.24%
shan: 30.58%
beik: 19.59%

Combined Character and Syllable-based Detection:
sgaw_kayin: 1.79%
rakhine: 4.15%
dawei: 9.33%
pao: 1.09%
po_kayin: 50.01%
bamar: 1.92%
mon: 6.62%
shan: 15.29%
beik: 9.80%
Running with ngram=5 on random sentence 10: ဆၧအနီၪနထိၬဘုၬထဲၩ့လၧဆၧအဂူၫဂၩကမံၩ့အ့ၬဧၪ.
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 100.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.62%
rakhine: 8.63%
dawei: 16.71%
pao: 0.86%
po_kayin: 0.66%
bamar: 0.71%
mon: 8.42%
shan: 44.94%
beik: 18.45%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.31%
rakhine: 4.31%
dawei: 8.36%
pao: 0.43%
po_kayin: 50.33%
bamar: 0.35%
mon: 4.21%
shan: 22.47%
beik: 9.22%

Processing file: rakhine.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
beik: 0.48%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.41%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.12%

Syllable-based Detection:
beik: 2.16%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 97.40%
bamar: 0.44%

Combined Character and Syllable-based Detection:
beik: 1.32%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 49.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 48.70%
bamar: 0.28%
Running with ngram=3 on random sentence 2: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.11%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.84%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.04%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.55%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 50.42%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.02%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.18%
mon: 0.00%
shan: 0.00%
pao: 1.05%
rakhine: 2.53%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 3.20%
bamar: 0.04%

Combined Character and Syllable-based Detection:
beik: 46.59%
mon: 0.00%
shan: 0.00%
pao: 0.53%
rakhine: 51.26%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.60%
bamar: 0.02%
Running with ngram=3 on random sentence 4: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
beik: 0.48%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.41%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.12%

Syllable-based Detection:
beik: 2.16%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 97.40%
bamar: 0.44%

Combined Character and Syllable-based Detection:
beik: 1.32%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 49.70%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 48.70%
bamar: 0.28%
Running with ngram=3 on random sentence 5: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.99%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 92.34%
mon: 0.12%
shan: 0.11%
pao: 1.36%
rakhine: 0.23%
po_kayin: 0.03%
sgaw_kayin: 0.11%
dawei: 5.48%
bamar: 0.22%

Combined Character and Syllable-based Detection:
beik: 46.17%
mon: 0.06%
shan: 0.05%
pao: 0.68%
rakhine: 50.11%
po_kayin: 0.02%
sgaw_kayin: 0.05%
dawei: 2.74%
bamar: 0.11%
Running with ngram=3 on random sentence 6: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 92.20%
mon: 0.00%
shan: 0.00%
pao: 0.02%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 2.08%
bamar: 5.70%

Combined Character and Syllable-based Detection:
beik: 46.10%
mon: 0.00%
shan: 0.00%
pao: 0.01%
rakhine: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.04%
bamar: 2.85%
Running with ngram=3 on random sentence 7: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 81.81%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.29%
bamar: 16.72%

Combined Character and Syllable-based Detection:
beik: 40.90%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 50.09%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.64%
bamar: 8.36%
Running with ngram=3 on random sentence 8: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 81.81%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.18%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.29%
bamar: 16.72%

Combined Character and Syllable-based Detection:
beik: 40.90%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 50.09%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.64%
bamar: 8.36%
Running with ngram=3 on random sentence 9: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.18%
mon: 0.00%
shan: 0.00%
pao: 1.05%
rakhine: 2.53%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 3.20%
bamar: 0.04%

Combined Character and Syllable-based Detection:
beik: 46.59%
mon: 0.00%
shan: 0.00%
pao: 0.53%
rakhine: 51.26%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 1.60%
bamar: 0.02%
Running with ngram=3 on random sentence 10: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 99.99%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 92.34%
mon: 0.12%
shan: 0.11%
pao: 1.36%
rakhine: 0.23%
po_kayin: 0.03%
sgaw_kayin: 0.11%
dawei: 5.48%
bamar: 0.22%

Combined Character and Syllable-based Detection:
beik: 46.17%
mon: 0.06%
shan: 0.05%
pao: 0.68%
rakhine: 50.11%
po_kayin: 0.02%
sgaw_kayin: 0.05%
dawei: 2.74%
bamar: 0.11%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 100.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 50.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 50.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 3.44%
mon: 0.00%
bamar: 0.00%
beik: 96.50%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.05%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 1.72%
mon: 0.00%
bamar: 0.00%
beik: 48.25%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 50.03%
shan: 0.00%
Running with ngram=4 on random sentence 2: မင်းမိန်းစရာမလိုပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.70%
beik: 0.13%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 99.17%
shan: 0.00%

Syllable-based Detection:
dawei: 8.03%
mon: 1.00%
bamar: 0.55%
beik: 67.72%
po_kayin: 0.33%
sgaw_kayin: 0.02%
pao: 0.22%
rakhine: 21.65%
shan: 0.49%

Combined Character and Syllable-based Detection:
dawei: 4.01%
mon: 0.50%
bamar: 0.63%
beik: 33.93%
po_kayin: 0.16%
sgaw_kayin: 0.01%
pao: 0.11%
rakhine: 60.41%
shan: 0.25%
Running with ngram=4 on random sentence 3: မင်းမိန်းစရာမလိုပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.70%
beik: 0.13%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 99.17%
shan: 0.00%

Syllable-based Detection:
dawei: 8.03%
mon: 1.00%
bamar: 0.55%
beik: 67.72%
po_kayin: 0.33%
sgaw_kayin: 0.02%
pao: 0.22%
rakhine: 21.65%
shan: 0.49%

Combined Character and Syllable-based Detection:
dawei: 4.01%
mon: 0.50%
bamar: 0.63%
beik: 33.93%
po_kayin: 0.16%
sgaw_kayin: 0.01%
pao: 0.11%
rakhine: 60.41%
shan: 0.25%
Running with ngram=4 on random sentence 4: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.57%
mon: 0.20%
bamar: 0.01%
beik: 97.77%
po_kayin: 0.05%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.03%
shan: 0.34%

Combined Character and Syllable-based Detection:
dawei: 0.79%
mon: 0.10%
bamar: 0.00%
beik: 48.88%
po_kayin: 0.02%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 50.02%
shan: 0.17%
Running with ngram=4 on random sentence 5: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=4 on random sentence 6: သူအမှန်အတိုင်းမကျိန်ဆိုရဲပါလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.02%
beik: 23.37%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 76.61%
shan: 0.00%

Syllable-based Detection:
dawei: 6.60%
mon: 2.83%
bamar: 0.01%
beik: 89.51%
po_kayin: 0.20%
sgaw_kayin: 0.00%
pao: 0.02%
rakhine: 0.15%
shan: 0.68%

Combined Character and Syllable-based Detection:
dawei: 3.30%
mon: 1.41%
bamar: 0.02%
beik: 56.44%
po_kayin: 0.10%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 38.38%
shan: 0.34%
Running with ngram=4 on random sentence 7: ကိုယ်မင်းကိုနားလည်ပါရေ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 5.41%
mon: 2.51%
bamar: 0.08%
beik: 77.46%
po_kayin: 2.96%
sgaw_kayin: 0.35%
pao: 0.54%
rakhine: 7.74%
shan: 2.96%

Combined Character and Syllable-based Detection:
dawei: 2.70%
mon: 1.26%
bamar: 0.04%
beik: 38.73%
po_kayin: 1.48%
sgaw_kayin: 0.17%
pao: 0.27%
rakhine: 53.87%
shan: 1.48%
Running with ngram=4 on random sentence 8: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 100.00%
shan: 0.00%

Syllable-based Detection:
dawei: 1.57%
mon: 0.20%
bamar: 0.01%
beik: 97.77%
po_kayin: 0.05%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.03%
shan: 0.34%

Combined Character and Syllable-based Detection:
dawei: 0.79%
mon: 0.10%
bamar: 0.00%
beik: 48.88%
po_kayin: 0.02%
sgaw_kayin: 0.01%
pao: 0.01%
rakhine: 50.02%
shan: 0.17%
Running with ngram=4 on random sentence 9: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=4 on random sentence 10: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.11%
beik: 2.83%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 97.05%
shan: 0.00%

Syllable-based Detection:
dawei: 24.54%
mon: 0.48%
bamar: 0.18%
beik: 72.98%
po_kayin: 0.38%
sgaw_kayin: 0.00%
pao: 0.03%
rakhine: 1.30%
shan: 0.11%

Combined Character and Syllable-based Detection:
dawei: 12.27%
mon: 0.24%
bamar: 0.15%
beik: 37.91%
po_kayin: 0.19%
sgaw_kayin: 0.00%
pao: 0.01%
rakhine: 49.18%
shan: 0.05%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 100.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 50.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 50.00%
Running with ngram=5 on random sentence 1: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.89%
rakhine: 2.22%
dawei: 15.05%
pao: 2.90%
po_kayin: 5.52%
bamar: 0.02%
mon: 7.00%
shan: 40.47%
beik: 25.93%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 51.11%
dawei: 7.53%
pao: 1.45%
po_kayin: 2.76%
bamar: 0.01%
mon: 3.50%
shan: 20.23%
beik: 12.97%
Running with ngram=5 on random sentence 2: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.67%
rakhine: 0.40%
dawei: 53.76%
pao: 0.05%
po_kayin: 0.67%
bamar: 3.33%
mon: 0.33%
shan: 0.19%
beik: 40.60%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.34%
rakhine: 50.20%
dawei: 26.88%
pao: 0.02%
po_kayin: 0.34%
bamar: 1.66%
mon: 0.16%
shan: 0.10%
beik: 20.30%
Running with ngram=5 on random sentence 3: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.89%
rakhine: 2.22%
dawei: 15.05%
pao: 2.90%
po_kayin: 5.52%
bamar: 0.02%
mon: 7.00%
shan: 40.47%
beik: 25.93%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 51.11%
dawei: 7.53%
pao: 1.45%
po_kayin: 2.76%
bamar: 0.01%
mon: 3.50%
shan: 20.23%
beik: 12.97%
Running with ngram=5 on random sentence 4: ငါအလုပ်မပြီးသိပါ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 40.75%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 59.25%

Syllable-based Detection:
sgaw_kayin: 0.57%
rakhine: 4.04%
dawei: 9.34%
pao: 2.95%
po_kayin: 41.19%
bamar: 2.54%
mon: 5.39%
shan: 11.87%
beik: 22.11%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.28%
rakhine: 22.39%
dawei: 4.67%
pao: 1.48%
po_kayin: 20.60%
bamar: 1.27%
mon: 2.69%
shan: 5.94%
beik: 40.68%
Running with ngram=5 on random sentence 5: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 22.36%
dawei: 40.42%
pao: 0.22%
po_kayin: 3.94%
bamar: 0.00%
mon: 2.44%
shan: 13.31%
beik: 17.30%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 61.18%
dawei: 20.21%
pao: 0.11%
po_kayin: 1.97%
bamar: 0.00%
mon: 1.22%
shan: 6.66%
beik: 8.65%
Running with ngram=5 on random sentence 6: မင်းတောင်တိကိုတက်နီကျလား။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.89%
rakhine: 2.22%
dawei: 15.05%
pao: 2.90%
po_kayin: 5.52%
bamar: 0.02%
mon: 7.00%
shan: 40.47%
beik: 25.93%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.45%
rakhine: 51.11%
dawei: 7.53%
pao: 1.45%
po_kayin: 2.76%
bamar: 0.01%
mon: 3.50%
shan: 20.23%
beik: 12.97%
Running with ngram=5 on random sentence 7: ကျွန်တော်ဆိုကေပြန်ပီးလိုက်ဖို့။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.67%
rakhine: 0.40%
dawei: 53.76%
pao: 0.05%
po_kayin: 0.67%
bamar: 3.33%
mon: 0.33%
shan: 0.19%
beik: 40.60%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.34%
rakhine: 50.20%
dawei: 26.88%
pao: 0.02%
po_kayin: 0.34%
bamar: 1.66%
mon: 0.16%
shan: 0.10%
beik: 20.30%
Running with ngram=5 on random sentence 8: ထိုမချေကိုသူအမှန်မမြတ်နိုးခပါ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 22.36%
dawei: 40.42%
pao: 0.22%
po_kayin: 3.94%
bamar: 0.00%
mon: 2.44%
shan: 13.31%
beik: 17.30%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 61.18%
dawei: 20.21%
pao: 0.11%
po_kayin: 1.97%
bamar: 0.00%
mon: 1.22%
shan: 6.66%
beik: 8.65%
Running with ngram=5 on random sentence 9: ငါဘတ်စ်ကားစီးဖို့အတွက်အကြွီလိုချင်ရေ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 99.99%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.01%

Syllable-based Detection:
sgaw_kayin: 0.73%
rakhine: 0.28%
dawei: 41.10%
pao: 0.08%
po_kayin: 4.48%
bamar: 0.00%
mon: 1.72%
shan: 24.57%
beik: 27.05%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.36%
rakhine: 50.14%
dawei: 20.55%
pao: 0.04%
po_kayin: 2.24%
bamar: 0.00%
mon: 0.86%
shan: 12.28%
beik: 13.53%
Running with ngram=5 on random sentence 10: မိုးချက်ချင်းရွာရေအခါသူရို့ဇာတိလုပ်နီစွာ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 100.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 1.36%
dawei: 30.88%
pao: 0.02%
po_kayin: 9.29%
bamar: 0.00%
mon: 1.73%
shan: 14.57%
beik: 42.14%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 50.68%
dawei: 15.44%
pao: 0.01%
po_kayin: 4.64%
bamar: 0.00%
mon: 0.87%
shan: 7.28%
beik: 21.07%

Processing file: sgaw_kayin.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 100.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 50.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.61%
mon: 0.03%
shan: 0.11%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 98.69%
dawei: 0.54%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.31%
mon: 0.02%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 99.35%
dawei: 0.27%
bamar: 0.00%
Running with ngram=3 on random sentence 2: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 82.28%
mon: 0.04%
shan: 0.05%
pao: 0.28%
rakhine: 0.11%
po_kayin: 0.10%
sgaw_kayin: 0.36%
dawei: 16.78%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 41.14%
mon: 0.02%
shan: 0.02%
pao: 0.14%
rakhine: 0.05%
po_kayin: 0.05%
sgaw_kayin: 50.18%
dawei: 8.39%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.97%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.03%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.01%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 4: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 52.79%
mon: 0.36%
shan: 0.05%
pao: 0.02%
rakhine: 0.02%
po_kayin: 0.01%
sgaw_kayin: 46.28%
dawei: 0.46%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 26.39%
mon: 0.18%
shan: 0.03%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 73.14%
dawei: 0.23%
bamar: 0.00%
Running with ngram=3 on random sentence 5: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.61%
mon: 0.03%
shan: 0.11%
pao: 0.00%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 98.69%
dawei: 0.54%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.31%
mon: 0.02%
shan: 0.05%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 99.35%
dawei: 0.27%
bamar: 0.00%
Running with ngram=3 on random sentence 6: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 99.97%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.03%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 49.99%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 50.01%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 7: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.46%
mon: 0.90%
shan: 2.08%
pao: 0.15%
rakhine: 0.57%
po_kayin: 0.28%
sgaw_kayin: 1.01%
dawei: 1.27%
bamar: 0.26%

Combined Character and Syllable-based Detection:
beik: 46.73%
mon: 0.45%
shan: 1.04%
pao: 0.07%
rakhine: 0.28%
po_kayin: 0.14%
sgaw_kayin: 50.51%
dawei: 0.64%
bamar: 0.13%
Running with ngram=3 on random sentence 8: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 52.79%
mon: 0.36%
shan: 0.05%
pao: 0.02%
rakhine: 0.02%
po_kayin: 0.01%
sgaw_kayin: 46.28%
dawei: 0.46%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 26.39%
mon: 0.18%
shan: 0.03%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 73.14%
dawei: 0.23%
bamar: 0.00%
Running with ngram=3 on random sentence 9: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 54.32%
mon: 1.19%
shan: 1.28%
pao: 0.32%
rakhine: 1.20%
po_kayin: 2.75%
sgaw_kayin: 13.85%
dawei: 24.73%
bamar: 0.35%

Combined Character and Syllable-based Detection:
beik: 27.16%
mon: 0.60%
shan: 0.64%
pao: 0.16%
rakhine: 0.60%
po_kayin: 1.38%
sgaw_kayin: 56.93%
dawei: 12.37%
bamar: 0.17%
Running with ngram=3 on random sentence 10: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 0.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 93.46%
mon: 0.90%
shan: 2.08%
pao: 0.15%
rakhine: 0.57%
po_kayin: 0.28%
sgaw_kayin: 1.01%
dawei: 1.27%
bamar: 0.26%

Combined Character and Syllable-based Detection:
beik: 46.73%
mon: 0.45%
shan: 1.04%
pao: 0.07%
rakhine: 0.28%
po_kayin: 0.14%
sgaw_kayin: 50.51%
dawei: 0.64%
bamar: 0.13%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 99.73%
mon: 0.00%
bamar: 0.00%
beik: 0.27%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Combined Character and Syllable-based Detection:
dawei: 49.87%
mon: 0.00%
bamar: 0.00%
beik: 0.13%
po_kayin: 0.00%
sgaw_kayin: 50.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%
Running with ngram=4 on random sentence 1: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 17.74%
mon: 12.59%
bamar: 9.50%
beik: 18.64%
po_kayin: 2.46%
sgaw_kayin: 0.02%
pao: 2.08%
rakhine: 7.90%
shan: 29.06%

Combined Character and Syllable-based Detection:
dawei: 8.87%
mon: 6.30%
bamar: 4.75%
beik: 9.32%
po_kayin: 1.23%
sgaw_kayin: 50.01%
pao: 1.04%
rakhine: 3.95%
shan: 14.53%
Running with ngram=4 on random sentence 2: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 25.95%
mon: 9.13%
bamar: 2.86%
beik: 28.64%
po_kayin: 2.77%
sgaw_kayin: 5.06%
pao: 0.36%
rakhine: 5.15%
shan: 20.09%

Combined Character and Syllable-based Detection:
dawei: 12.97%
mon: 4.56%
bamar: 1.43%
beik: 14.32%
po_kayin: 1.38%
sgaw_kayin: 52.53%
pao: 0.18%
rakhine: 2.57%
shan: 10.05%
Running with ngram=4 on random sentence 3: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.59%
mon: 12.16%
bamar: 3.53%
beik: 17.99%
po_kayin: 8.17%
sgaw_kayin: 11.61%
pao: 3.24%
rakhine: 7.63%
shan: 8.09%

Combined Character and Syllable-based Detection:
dawei: 13.80%
mon: 6.08%
bamar: 1.76%
beik: 9.00%
po_kayin: 4.08%
sgaw_kayin: 55.80%
pao: 1.62%
rakhine: 3.81%
shan: 4.05%
Running with ngram=4 on random sentence 4: တၢ်ဝဲန့ၣ်န့ၣ်မ့ၢ်ယထီၣ်ယီၢ်ဘၣ်ဧါ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 22.31%
mon: 15.84%
bamar: 4.59%
beik: 23.44%
po_kayin: 10.64%
sgaw_kayin: 0.06%
pao: 2.62%
rakhine: 9.94%
shan: 10.54%

Combined Character and Syllable-based Detection:
dawei: 11.16%
mon: 7.92%
bamar: 2.30%
beik: 11.72%
po_kayin: 5.32%
sgaw_kayin: 50.03%
pao: 1.31%
rakhine: 4.97%
shan: 5.27%
Running with ngram=4 on random sentence 5: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 50.32%
mon: 9.93%
bamar: 0.10%
beik: 21.76%
po_kayin: 2.10%
sgaw_kayin: 0.04%
pao: 0.71%
rakhine: 10.64%
shan: 4.40%

Combined Character and Syllable-based Detection:
dawei: 25.16%
mon: 4.97%
bamar: 0.05%
beik: 10.88%
po_kayin: 1.05%
sgaw_kayin: 50.02%
pao: 0.35%
rakhine: 5.32%
shan: 2.20%
Running with ngram=4 on random sentence 6: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 24.89%
mon: 2.12%
bamar: 0.00%
beik: 19.77%
po_kayin: 0.13%
sgaw_kayin: 35.09%
pao: 0.09%
rakhine: 0.58%
shan: 17.34%

Combined Character and Syllable-based Detection:
dawei: 12.44%
mon: 1.06%
bamar: 0.00%
beik: 9.88%
po_kayin: 0.06%
sgaw_kayin: 67.54%
pao: 0.05%
rakhine: 0.29%
shan: 8.67%
Running with ngram=4 on random sentence 7: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 50.32%
mon: 9.93%
bamar: 0.10%
beik: 21.76%
po_kayin: 2.10%
sgaw_kayin: 0.04%
pao: 0.71%
rakhine: 10.64%
shan: 4.40%

Combined Character and Syllable-based Detection:
dawei: 25.16%
mon: 4.97%
bamar: 0.05%
beik: 10.88%
po_kayin: 1.05%
sgaw_kayin: 50.02%
pao: 0.35%
rakhine: 5.32%
shan: 2.20%
Running with ngram=4 on random sentence 8: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 25.95%
mon: 9.13%
bamar: 2.86%
beik: 28.64%
po_kayin: 2.77%
sgaw_kayin: 5.06%
pao: 0.36%
rakhine: 5.15%
shan: 20.09%

Combined Character and Syllable-based Detection:
dawei: 12.97%
mon: 4.56%
bamar: 1.43%
beik: 14.32%
po_kayin: 1.38%
sgaw_kayin: 52.53%
pao: 0.18%
rakhine: 2.57%
shan: 10.05%
Running with ngram=4 on random sentence 9: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 27.59%
mon: 12.16%
bamar: 3.53%
beik: 17.99%
po_kayin: 8.17%
sgaw_kayin: 11.61%
pao: 3.24%
rakhine: 7.63%
shan: 8.09%

Combined Character and Syllable-based Detection:
dawei: 13.80%
mon: 6.08%
bamar: 1.76%
beik: 9.00%
po_kayin: 4.08%
sgaw_kayin: 55.80%
pao: 1.62%
rakhine: 3.81%
shan: 4.05%
Running with ngram=4 on random sentence 10: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 100.00%
pao: 0.00%
rakhine: 0.00%
shan: 0.00%

Syllable-based Detection:
dawei: 62.28%
mon: 3.02%
bamar: 0.02%
beik: 30.70%
po_kayin: 0.28%
sgaw_kayin: 0.00%
pao: 1.32%
rakhine: 0.42%
shan: 1.96%

Combined Character and Syllable-based Detection:
dawei: 31.14%
mon: 1.51%
bamar: 0.01%
beik: 15.35%
po_kayin: 0.14%
sgaw_kayin: 50.00%
pao: 0.66%
rakhine: 0.21%
shan: 0.98%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.96%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 99.04%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 0.00%
dawei: 0.48%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 49.52%
Running with ngram=5 on random sentence 1: ပိာ်မုၣ်န့ၣ်တတိၢ်နီၣ်ပှၤနီတဂၤလၢၤဘၣ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 12.92%
dawei: 17.00%
pao: 0.88%
po_kayin: 6.23%
bamar: 0.72%
mon: 19.79%
shan: 13.18%
beik: 29.28%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 6.46%
dawei: 8.50%
pao: 0.44%
po_kayin: 3.12%
bamar: 0.36%
mon: 9.89%
shan: 6.59%
beik: 14.64%
Running with ngram=5 on random sentence 2: ဘၣ်တဲပှၤအဂ့ၢ်န့ၣ်သးဟ့လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.02%
rakhine: 15.24%
dawei: 15.24%
pao: 4.08%
po_kayin: 4.43%
bamar: 15.24%
mon: 15.24%
shan: 15.24%
beik: 15.24%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.01%
rakhine: 7.62%
dawei: 7.62%
pao: 2.04%
po_kayin: 2.22%
bamar: 7.62%
mon: 7.62%
shan: 7.62%
beik: 7.62%
Running with ngram=5 on random sentence 3: ပျဲတၢ်မၤစၢၤတက့ၢ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 2.99%
rakhine: 9.65%
dawei: 21.66%
pao: 2.54%
po_kayin: 10.33%
bamar: 4.46%
mon: 15.38%
shan: 10.24%
beik: 22.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 51.50%
rakhine: 4.82%
dawei: 10.83%
pao: 1.27%
po_kayin: 5.16%
bamar: 2.23%
mon: 7.69%
shan: 5.12%
beik: 11.38%
Running with ngram=5 on random sentence 4: ကကွၢ်ထွဲအီၤအဂီၢ်ကနၢၤဒၣ်နၤလီၤ.
Character-based Detection:
sgaw_kayin: 99.97%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 8.42%
dawei: 16.30%
pao: 0.84%
po_kayin: 3.71%
bamar: 0.69%
mon: 8.22%
shan: 43.83%
beik: 17.99%

Combined Character and Syllable-based Detection:
sgaw_kayin: 49.99%
rakhine: 4.21%
dawei: 8.15%
pao: 0.42%
po_kayin: 1.86%
bamar: 0.35%
mon: 4.11%
shan: 21.92%
beik: 9.00%
Running with ngram=5 on random sentence 5: ဒ်ယဆိကမိၣ်အသိးဆိကမိၣ်တက့ၢ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.06%
rakhine: 2.85%
dawei: 13.07%
pao: 0.13%
po_kayin: 0.68%
bamar: 0.02%
mon: 7.67%
shan: 27.23%
beik: 48.30%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.03%
rakhine: 1.43%
dawei: 6.53%
pao: 0.06%
po_kayin: 0.34%
bamar: 0.01%
mon: 3.83%
shan: 13.61%
beik: 24.15%
Running with ngram=5 on random sentence 6: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%
Running with ngram=5 on random sentence 7: ဒ်နတဲတ့ၢ်အသိးယတဲနၢ်ပၢၢ်တ့ၢ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.19%
rakhine: 5.52%
dawei: 27.79%
pao: 0.38%
po_kayin: 2.96%
bamar: 1.18%
mon: 9.77%
shan: 21.54%
beik: 30.67%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.09%
rakhine: 2.76%
dawei: 13.89%
pao: 0.19%
po_kayin: 1.48%
bamar: 0.59%
mon: 4.89%
shan: 10.77%
beik: 15.34%
Running with ngram=5 on random sentence 8: လၢခံကတၢၢ်တဘျီကတဲအီၤလၢယအဲၣ်အီၤန့ၣ်အခွဲးတန့ၢ်လၢၤဘၣ်.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 1.79%
dawei: 39.26%
pao: 0.07%
po_kayin: 0.45%
bamar: 0.01%
mon: 4.94%
shan: 3.21%
beik: 50.25%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 0.90%
dawei: 19.63%
pao: 0.04%
po_kayin: 0.23%
bamar: 0.01%
mon: 2.47%
shan: 1.61%
beik: 25.12%
Running with ngram=5 on random sentence 9: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%
Running with ngram=5 on random sentence 10: တၢ်ဝဲန့ၣ်လၢပဂီၢ်ကီခဲဝဲဒၣ်လီၤ.
Character-based Detection:
sgaw_kayin: 100.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 0.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.01%
rakhine: 7.31%
dawei: 28.32%
pao: 0.24%
po_kayin: 0.86%
bamar: 0.01%
mon: 20.11%
shan: 13.39%
beik: 29.75%

Combined Character and Syllable-based Detection:
sgaw_kayin: 50.00%
rakhine: 3.65%
dawei: 14.16%
pao: 0.12%
po_kayin: 0.43%
bamar: 0.01%
mon: 10.05%
shan: 6.69%
beik: 14.88%

Processing file: shan.txt.raw
Running with ngram=3 on full file
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 1: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.18%
mon: 0.08%
shan: 98.69%
pao: 0.18%
rakhine: 0.18%
po_kayin: 0.18%
sgaw_kayin: 0.18%
dawei: 0.18%
bamar: 0.18%

Combined Character and Syllable-based Detection:
beik: 0.09%
mon: 0.04%
shan: 99.34%
pao: 0.09%
rakhine: 0.09%
po_kayin: 0.09%
sgaw_kayin: 0.09%
dawei: 0.09%
bamar: 0.09%
Running with ngram=3 on random sentence 2: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.01%
mon: 0.00%
shan: 99.95%
pao: 0.01%
rakhine: 0.01%
po_kayin: 0.01%
sgaw_kayin: 0.01%
dawei: 0.01%
bamar: 0.01%

Combined Character and Syllable-based Detection:
beik: 0.00%
mon: 0.00%
shan: 99.97%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%
Running with ngram=3 on random sentence 3: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.18%
mon: 0.08%
shan: 98.69%
pao: 0.18%
rakhine: 0.18%
po_kayin: 0.18%
sgaw_kayin: 0.18%
dawei: 0.18%
bamar: 0.18%

Combined Character and Syllable-based Detection:
beik: 0.09%
mon: 0.04%
shan: 99.34%
pao: 0.09%
rakhine: 0.09%
po_kayin: 0.09%
sgaw_kayin: 0.09%
dawei: 0.09%
bamar: 0.09%
Running with ngram=3 on random sentence 4: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.51%
mon: 0.22%
shan: 96.21%
pao: 0.51%
rakhine: 0.51%
po_kayin: 0.51%
sgaw_kayin: 0.51%
dawei: 0.51%
bamar: 0.51%

Combined Character and Syllable-based Detection:
beik: 0.26%
mon: 0.11%
shan: 98.10%
pao: 0.26%
rakhine: 0.26%
po_kayin: 0.26%
sgaw_kayin: 0.26%
dawei: 0.26%
bamar: 0.26%
Running with ngram=3 on random sentence 5: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.51%
mon: 0.22%
shan: 96.21%
pao: 0.51%
rakhine: 0.51%
po_kayin: 0.51%
sgaw_kayin: 0.51%
dawei: 0.51%
bamar: 0.51%

Combined Character and Syllable-based Detection:
beik: 0.26%
mon: 0.11%
shan: 98.10%
pao: 0.26%
rakhine: 0.26%
po_kayin: 0.26%
sgaw_kayin: 0.26%
dawei: 0.26%
bamar: 0.26%
Running with ngram=3 on random sentence 6: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 6.23%
mon: 2.70%
shan: 53.72%
pao: 6.23%
rakhine: 6.23%
po_kayin: 6.23%
sgaw_kayin: 6.23%
dawei: 6.23%
bamar: 6.23%

Combined Character and Syllable-based Detection:
beik: 3.11%
mon: 1.35%
shan: 76.86%
pao: 3.11%
rakhine: 3.11%
po_kayin: 3.11%
sgaw_kayin: 3.11%
dawei: 3.11%
bamar: 3.11%
Running with ngram=3 on random sentence 7: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 3.60%
mon: 0.80%
shan: 84.36%
pao: 1.94%
rakhine: 1.91%
po_kayin: 0.76%
sgaw_kayin: 0.76%
dawei: 2.73%
bamar: 3.13%

Combined Character and Syllable-based Detection:
beik: 1.80%
mon: 0.40%
shan: 92.18%
pao: 0.97%
rakhine: 0.96%
po_kayin: 0.38%
sgaw_kayin: 0.38%
dawei: 1.37%
bamar: 1.57%
Running with ngram=3 on random sentence 8: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 6.23%
mon: 2.70%
shan: 53.72%
pao: 6.23%
rakhine: 6.23%
po_kayin: 6.23%
sgaw_kayin: 6.23%
dawei: 6.23%
bamar: 6.23%

Combined Character and Syllable-based Detection:
beik: 3.11%
mon: 1.35%
shan: 76.86%
pao: 3.11%
rakhine: 3.11%
po_kayin: 3.11%
sgaw_kayin: 3.11%
dawei: 3.11%
bamar: 3.11%
Running with ngram=3 on random sentence 9: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 0.18%
mon: 0.08%
shan: 98.69%
pao: 0.18%
rakhine: 0.18%
po_kayin: 0.18%
sgaw_kayin: 0.18%
dawei: 0.18%
bamar: 0.18%

Combined Character and Syllable-based Detection:
beik: 0.09%
mon: 0.04%
shan: 99.34%
pao: 0.09%
rakhine: 0.09%
po_kayin: 0.09%
sgaw_kayin: 0.09%
dawei: 0.09%
bamar: 0.09%
Running with ngram=3 on random sentence 10: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
beik: 0.00%
mon: 0.00%
shan: 100.00%
pao: 0.00%
rakhine: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
dawei: 0.00%
bamar: 0.00%

Syllable-based Detection:
beik: 6.23%
mon: 2.70%
shan: 53.72%
pao: 6.23%
rakhine: 6.23%
po_kayin: 6.23%
sgaw_kayin: 6.23%
dawei: 6.23%
bamar: 6.23%

Combined Character and Syllable-based Detection:
beik: 3.11%
mon: 1.35%
shan: 76.86%
pao: 3.11%
rakhine: 3.11%
po_kayin: 3.11%
sgaw_kayin: 3.11%
dawei: 3.11%
bamar: 3.11%
Running with ngram=4 on full file
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Combined Character and Syllable-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%
Running with ngram=4 on random sentence 1: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.27%
mon: 0.12%
bamar: 0.27%
beik: 0.27%
po_kayin: 0.27%
sgaw_kayin: 0.27%
pao: 0.27%
rakhine: 0.27%
shan: 98.02%

Combined Character and Syllable-based Detection:
dawei: 0.13%
mon: 0.06%
bamar: 0.13%
beik: 0.13%
po_kayin: 0.13%
sgaw_kayin: 0.13%
pao: 0.13%
rakhine: 0.13%
shan: 99.01%
Running with ngram=4 on random sentence 2: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 11.77%
mon: 3.42%
bamar: 0.41%
beik: 15.49%
po_kayin: 3.28%
sgaw_kayin: 3.28%
pao: 0.88%
rakhine: 8.25%
shan: 53.22%

Combined Character and Syllable-based Detection:
dawei: 5.88%
mon: 1.71%
bamar: 0.21%
beik: 7.75%
po_kayin: 1.64%
sgaw_kayin: 1.64%
pao: 0.44%
rakhine: 4.12%
shan: 76.61%
Running with ngram=4 on random sentence 3: ႁဝ်းမိူဝ်ႈၽုၵ်ႈၵၢင်ၼႂ်တေဢွၵ်ႇပႆတၢင်းဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 24.47%
mon: 7.12%
bamar: 0.86%
beik: 32.21%
po_kayin: 6.82%
sgaw_kayin: 6.82%
pao: 1.83%
rakhine: 17.14%
shan: 2.74%

Combined Character and Syllable-based Detection:
dawei: 12.23%
mon: 3.56%
bamar: 0.43%
beik: 16.10%
po_kayin: 3.41%
sgaw_kayin: 3.41%
pao: 0.91%
rakhine: 8.57%
shan: 51.37%
Running with ngram=4 on random sentence 4: တွင်းပၢၼ်ႇၵဝ်ဢမ်ႇတွင်းပၢၼ်ႇၵဝ်။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.03%
mon: 0.01%
bamar: 0.03%
beik: 0.03%
po_kayin: 0.03%
sgaw_kayin: 0.03%
pao: 0.03%
rakhine: 0.03%
shan: 99.77%

Combined Character and Syllable-based Detection:
dawei: 0.02%
mon: 0.01%
bamar: 0.02%
beik: 0.02%
po_kayin: 0.02%
sgaw_kayin: 0.02%
pao: 0.02%
rakhine: 0.02%
shan: 99.89%
Running with ngram=4 on random sentence 5: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.02%
mon: 5.21%
bamar: 12.02%
beik: 12.02%
po_kayin: 12.02%
sgaw_kayin: 12.02%
pao: 12.02%
rakhine: 12.02%
shan: 10.68%

Combined Character and Syllable-based Detection:
dawei: 6.01%
mon: 2.60%
bamar: 6.01%
beik: 6.01%
po_kayin: 6.01%
sgaw_kayin: 6.01%
pao: 6.01%
rakhine: 6.01%
shan: 55.34%
Running with ngram=4 on random sentence 6: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 12.02%
mon: 5.21%
bamar: 12.02%
beik: 12.02%
po_kayin: 12.02%
sgaw_kayin: 12.02%
pao: 12.02%
rakhine: 12.02%
shan: 10.68%

Combined Character and Syllable-based Detection:
dawei: 6.01%
mon: 2.60%
bamar: 6.01%
beik: 6.01%
po_kayin: 6.01%
sgaw_kayin: 6.01%
pao: 6.01%
rakhine: 6.01%
shan: 55.34%
Running with ngram=4 on random sentence 7: ဢရသႃႇမၼ်းတႄႉမိူၼ်ၼမ်ႉလၢင်ႉဝၢၼ်ႇဝႆႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 1.70%
mon: 0.74%
bamar: 1.70%
beik: 1.70%
po_kayin: 1.70%
sgaw_kayin: 1.70%
pao: 1.70%
rakhine: 1.70%
shan: 87.37%

Combined Character and Syllable-based Detection:
dawei: 0.85%
mon: 0.37%
bamar: 0.85%
beik: 0.85%
po_kayin: 0.85%
sgaw_kayin: 0.85%
pao: 0.85%
rakhine: 0.85%
shan: 93.69%
Running with ngram=4 on random sentence 8: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 7.23%
mon: 3.13%
bamar: 7.23%
beik: 7.23%
po_kayin: 7.23%
sgaw_kayin: 7.23%
pao: 7.23%
rakhine: 7.23%
shan: 46.27%

Combined Character and Syllable-based Detection:
dawei: 3.61%
mon: 1.57%
bamar: 3.61%
beik: 3.61%
po_kayin: 3.61%
sgaw_kayin: 3.61%
pao: 3.61%
rakhine: 3.61%
shan: 73.13%
Running with ngram=4 on random sentence 9: တႃႇမၼ်းၼၢင်းႁဝ်းတေထၢမ်ဢမ်ႇၸႂ်ႈ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 0.74%
mon: 0.22%
bamar: 0.03%
beik: 0.98%
po_kayin: 0.21%
sgaw_kayin: 0.21%
pao: 0.06%
rakhine: 0.52%
shan: 97.05%

Combined Character and Syllable-based Detection:
dawei: 0.37%
mon: 0.11%
bamar: 0.01%
beik: 0.49%
po_kayin: 0.10%
sgaw_kayin: 0.10%
pao: 0.03%
rakhine: 0.26%
shan: 98.53%
Running with ngram=4 on random sentence 10: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
dawei: 0.00%
mon: 0.00%
bamar: 0.00%
beik: 0.00%
po_kayin: 0.00%
sgaw_kayin: 0.00%
pao: 0.00%
rakhine: 0.00%
shan: 100.00%

Syllable-based Detection:
dawei: 7.23%
mon: 3.13%
bamar: 7.23%
beik: 7.23%
po_kayin: 7.23%
sgaw_kayin: 7.23%
pao: 7.23%
rakhine: 7.23%
shan: 46.27%

Combined Character and Syllable-based Detection:
dawei: 3.61%
mon: 1.57%
bamar: 3.61%
beik: 3.61%
po_kayin: 3.61%
sgaw_kayin: 3.61%
pao: 3.61%
rakhine: 3.61%
shan: 73.13%
Running with ngram=5 on full file
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%
Running with ngram=5 on random sentence 1: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 12.23%
rakhine: 12.23%
dawei: 12.23%
pao: 12.23%
po_kayin: 12.23%
bamar: 12.23%
mon: 5.30%
shan: 9.08%
beik: 12.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.12%
rakhine: 6.12%
dawei: 6.12%
pao: 6.12%
po_kayin: 6.12%
bamar: 6.12%
mon: 2.65%
shan: 54.54%
beik: 6.12%
Running with ngram=5 on random sentence 2: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 12.23%
rakhine: 12.23%
dawei: 12.23%
pao: 12.23%
po_kayin: 12.23%
bamar: 12.23%
mon: 5.30%
shan: 9.08%
beik: 12.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.12%
rakhine: 6.12%
dawei: 6.12%
pao: 6.12%
po_kayin: 6.12%
bamar: 6.12%
mon: 2.65%
shan: 54.54%
beik: 6.12%
Running with ngram=5 on random sentence 3: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 12.23%
rakhine: 12.23%
dawei: 12.23%
pao: 12.23%
po_kayin: 12.23%
bamar: 12.23%
mon: 5.30%
shan: 9.08%
beik: 12.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.12%
rakhine: 6.12%
dawei: 6.12%
pao: 6.12%
po_kayin: 6.12%
bamar: 6.12%
mon: 2.65%
shan: 54.54%
beik: 6.12%
Running with ngram=5 on random sentence 4: မႂ်းလွင်ႈၼႆႉလၢတ်ႈမႃးႁိုဝ်ဢမ်ႇလၢတ်ႈမႃးႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 0.36%
rakhine: 0.36%
dawei: 0.36%
pao: 0.36%
po_kayin: 0.36%
bamar: 0.36%
mon: 0.16%
shan: 97.31%
beik: 0.36%

Combined Character and Syllable-based Detection:
sgaw_kayin: 0.18%
rakhine: 0.18%
dawei: 0.18%
pao: 0.18%
po_kayin: 0.18%
bamar: 0.18%
mon: 0.08%
shan: 98.66%
beik: 0.18%
Running with ngram=5 on random sentence 5: တႃႇလုၵ်ႈႁဵၼ်းၶဝ်တေလႆႈဢဝ်ပပ်ႉလႂ်။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 18.17%
rakhine: 14.98%
dawei: 11.08%
pao: 4.86%
po_kayin: 18.17%
bamar: 2.28%
mon: 3.41%
shan: 8.30%
beik: 18.76%

Combined Character and Syllable-based Detection:
sgaw_kayin: 9.08%
rakhine: 7.49%
dawei: 5.54%
pao: 2.43%
po_kayin: 9.08%
bamar: 1.14%
mon: 1.70%
shan: 54.15%
beik: 9.38%
Running with ngram=5 on random sentence 6: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.09%
rakhine: 0.09%
dawei: 0.09%
pao: 0.09%
po_kayin: 0.09%
bamar: 0.09%
mon: 0.09%
shan: 99.24%
beik: 0.09%

Syllable-based Detection:
sgaw_kayin: 11.86%
rakhine: 11.86%
dawei: 11.86%
pao: 11.86%
po_kayin: 11.86%
bamar: 11.86%
mon: 5.13%
shan: 11.86%
beik: 11.86%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.98%
rakhine: 5.98%
dawei: 5.98%
pao: 5.98%
po_kayin: 5.98%
bamar: 5.98%
mon: 2.61%
shan: 55.55%
beik: 5.98%
Running with ngram=5 on random sentence 7: ဢမ်ႇမီးၶပ်းမၢႆတႃႇဢွၵ်ႇပၢႆႈႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 11.21%
rakhine: 11.21%
dawei: 11.21%
pao: 11.21%
po_kayin: 11.21%
bamar: 11.21%
mon: 4.86%
shan: 16.65%
beik: 11.21%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.61%
rakhine: 5.61%
dawei: 5.61%
pao: 5.61%
po_kayin: 5.61%
bamar: 5.61%
mon: 2.43%
shan: 58.32%
beik: 5.61%
Running with ngram=5 on random sentence 8: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.09%
rakhine: 0.09%
dawei: 0.09%
pao: 0.09%
po_kayin: 0.09%
bamar: 0.09%
mon: 0.09%
shan: 99.24%
beik: 0.09%

Syllable-based Detection:
sgaw_kayin: 11.86%
rakhine: 11.86%
dawei: 11.86%
pao: 11.86%
po_kayin: 11.86%
bamar: 11.86%
mon: 5.13%
shan: 11.86%
beik: 11.86%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.98%
rakhine: 5.98%
dawei: 5.98%
pao: 5.98%
po_kayin: 5.98%
bamar: 5.98%
mon: 2.61%
shan: 55.55%
beik: 5.98%
Running with ngram=5 on random sentence 9: ဢမ်ႇမူတ်းသႂ်ႁႃႉ။
Character-based Detection:
sgaw_kayin: 0.09%
rakhine: 0.09%
dawei: 0.09%
pao: 0.09%
po_kayin: 0.09%
bamar: 0.09%
mon: 0.09%
shan: 99.24%
beik: 0.09%

Syllable-based Detection:
sgaw_kayin: 11.86%
rakhine: 11.86%
dawei: 11.86%
pao: 11.86%
po_kayin: 11.86%
bamar: 11.86%
mon: 5.13%
shan: 11.86%
beik: 11.86%

Combined Character and Syllable-based Detection:
sgaw_kayin: 5.98%
rakhine: 5.98%
dawei: 5.98%
pao: 5.98%
po_kayin: 5.98%
bamar: 5.98%
mon: 2.61%
shan: 55.55%
beik: 5.98%
Running with ngram=5 on random sentence 10: ဢၼ်ၼႆႉတႃႇမၼ်းယၢပ်ႇဢိူဝ်ႈ။
Character-based Detection:
sgaw_kayin: 0.00%
rakhine: 0.00%
dawei: 0.00%
pao: 0.00%
po_kayin: 0.00%
bamar: 0.00%
mon: 0.00%
shan: 100.00%
beik: 0.00%

Syllable-based Detection:
sgaw_kayin: 12.23%
rakhine: 12.23%
dawei: 12.23%
pao: 12.23%
po_kayin: 12.23%
bamar: 12.23%
mon: 5.30%
shan: 9.08%
beik: 12.23%

Combined Character and Syllable-based Detection:
sgaw_kayin: 6.12%
rakhine: 6.12%
dawei: 6.12%
pao: 6.12%
po_kayin: 6.12%
bamar: 6.12%
mon: 2.65%
shan: 54.54%
beik: 6.12%

All processing completed.

real    12m29.376s
user    11m13.991s
sys     1m15.194s
```

Experiment-3 (with char, syl, char+syl Ngram, Naive Bayes) ရဲ့ ရလဒ်က အောက်ပါအတိုင်း ...  

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
