# WER Calculation for 10-fold Experimental Result

WER တွက်တာကို NLP class မှာ workshop တွေမှာ သင်ကြားပေးခဲ့ပေမဲ့ လက်တွေ့ experiment တွေမှာတော့ 10-fold run ထားတာမျိုးလည်း ရှိလို့ အဲဒီလို 10-fold run ပြီးထွက်လာတဲ့ hyp ဖိုင်တွေအားလုံးကို ပေါင်းပြီးတော့ WER ဘယ်လိုတွက်သလဲ ဆိုတာကို လေ့လာနိုင်အောင် တင်ပေးထားတာပါ။  

Experiment ကတော့ သဇင်မြင့်ဦးနဲ့ လုပ်ခဲ့တဲ့ ဗမာစာကို ကြားခံထားပြီးတော့ ထားဝယ်စာ ကနေ ဘိတ်စာကို ဘာသာပြန်တာ၊ ဘိတ်စာ ကနေ ထားဝယ်စာ ကို ဘာသာပြန်တာ၊   
ထိုနည်းလည်းကောင်း ဘိတ်စာ ကနေ ရခိုင် စာကို၊ ရခိုင်စာ ကနေ ဘိတ်စာကို ဘာသာပြန်ထားတဲ့ ရလဒ်တွေကို သုံးပြီး run ပြထားပါတယ်။  

y@Lab  
26 Jan 2022  

## File Preparation

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ./mk-one-big-file.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ls *.all
baseline.all  ref.all  transfer.all  triangulation.all
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ wc *.all
   6622   40916  629492 baseline.all
   6622   39659  637258 ref.all
   6622   41085  623866 transfer.all
   6622   40087  615364 triangulation.all
  26488  161747 2505980 total
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head *.all
==> baseline.all <==
သူ ခံဗျား ဟှို အဲဇာ ပေး ဟှို့မှုဝ ။ 
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး ဇာနူး ။ 
နည်း ပြေ တာပေါ့ ။ 
နန် ဟှဲဇာ ရေး နူး ။ 
ဆရာ လာ နေဟှယ် ။ 
ဆရာ လာ နေဟှယ် ။ 
သူ အင်္ဂလိပ် ဂါး ပြော နိုင်ဘဲ့လား ။ 
နန် ဆေးလိ လျှော့ သော့-က့့့််် နေနူး ။ 
သူးနို့ ငွေ စု ဟှ ၊ စု လား ။ 
ဝယ်ယား ဟှ သူ့ ဟှို သိ ထားဇာ ။ 

==> ref.all <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
နန် ဟှဲဇာ ရေး နေဟှယ် ။ 
ဆရာ လာပီ ။
ဆရာ လာ ပီ ။
သူ အန်းဂလီ ဂါး  ပြော နိုင်ဟှီးလား ။
ခံဗျား ဆေးလိ လျှော့ သော့-က့့်် လိုက်မား ။
သူးနို့ ငွေ စု ကေ့ဟှ ငွေ စု ကေ့လား ။
ဝယ်ယား ဟှ သူ့ ဝို သိ ဟှားဇာ ။

==> transfer.all <==
သူ ခံဗျား ဟှို အဲ့မာ ပေး မှာ မှုဝ ။ 
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး နူး ။ 
ရတိုင်း ပြေ သွားမယ် ။ 
နန် ဟှဲဇာ ရေး နူး ။ 
ဆရာ လာ နေဟှယ် ။ 
ဆရာ လာ နေဟှယ် ။ 
သူ အမ်းဂလိ ဂါး ပြော နိုင်လား ။ 
ခံဗျား ဆေးလိ လျှော့ သော့-က့့့််် နေနူး ။ 
သူးနို့ ငွေ စု ဟှ စု လား ။ 
သူ ဟှ သူ့ ဟှို သိ ဟှားဇာ ။ 

==> triangulation.all <==
သူ ခံဗျား ဟှို အဲ့မာ ပေး မှုဝ ။ 
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး ခဲ့နူး ။ 
ရတိုင်း ပြေ တာပေါ့ ။ 
နန် ဟှဲဇာ ရေး နေဟှယ် ။ 
ဆရာ လာ နေဟှယ် ။ 
ဆရာ လာ နေဟှယ် ။ 
သူ အင်္ဂလိပ် ဂါး ပြော နိုင်လား ။ 
နန် ဆေးလိ လျှော့ သော့-က့့်် ခဲ့ဟှယ် ။ 
သူးနို့ ငွေ စု ဟှ စု လား ။ 
သူ ဟှ သူ့ ဟှို သိ ထားဇာ ။ 
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ tail *.all
==> baseline.all <==
သိပ် ကော ရုံလောက် ဝဲ့ ၊ ခံဗျား ကော နေကော ပဲ့လား ။ 
သူးနို့ ကျွနနွန့် ငယ်ချင်း ဒွေ ဝို သိ ရယ် ။ 
ဟှယ်ဒူ့ ပေတံ ဟှယ် ။ 
ငါ ဗြော် ဖူးမျှခြား လူ ဒွေ ထက် နန် ပို စိဝမ်ဇားစာ ကွန်း ဟှယ် ။ 
အဲဇာ ဟှို တိုင်း ဟှလား ။ 
သူ အယ်မျိုး လူ န မင်္ဂလာဆောင် ဟှို့ပဲ့လား ။ 
သူ့ ဟှို သိပ်ပြီး ရတိုင်း ပြော နဲ့လန်း ။ 
ကျွန်တော်ဝို့ သူ့ ဝို သိ ရယ် ။ 
နန် ဟှယ်စာ ဝယ် နေနူး ။ 
ကျွန်တော် မှား လုပ် ခဲ့ကြောက်လား ။ 

==> ref.all <==
ကော ရောငမျှပဲ့ ၊ ခံဗျား မား နေကော ပဲ့လား ။
သူးနို့ ကျွန်တော့် ငယ်ချင်း ဒွေ ဝို သိ ရယ် ။
ဟှယ်ဒူ့ ပေတံ နူး ။
ငါ ဗြော် ဖူးမျှထဲမှာ ခြား လူ ဒွေ ထက် နန်ရ ပို စိဝမ်စား ဝို့ ကွန်း ရယ် ။
အဲ့ဇာဝို မ တိုင်း ဟှလား ။
သူ အရ်မာလူ န လပ်ထပ် ဟှို့လား ။
အဲဟှို ရတိုင်းညင် ဝေဖန်  ကေ့န ။
ကျွန်တော် သူးနို့ ဝို သိ ဟှယ် ။
နန် ဟှယ်ရာ ဝယ် နူး ။
ကျွန်တော့ မှား လောက် မိလား ။

==> transfer.all <==
ရတိုင်း ကော ရုံလောက် ပဲ ၊ ခံဗျား ကော နေကော လား ။ 
သူးနို့ ကျွန်တော့ ငယ်ချင်း ဒွေ ဝို သိ ရယ် ။ 
ဟှယ်ဒူ့ ပေတံ ဟှယ် ။ 
ငါ ဗြော် ဖူးမျှခြား လူ ဒွေ ထက် နန် ပို စိဝမ်ဇားစာ ကွန်း ဟှယ် ။ 
အဲ့မာ ဟှို တိုင်း ဟှလား ။ 
သူ အယ်မျိုး လူ န မင်္ဂလာဆွန် မယ်ပဲ့လား ။ 
သူ ဟှို သိပ်ပြီး ရတိုင်း ပြော နဲ့လန်း ။ 
ကျွန်တော် ဝယ်ယား ဝို သိ ဟှယ် ။ 
နန် ဟှယ်ရာ ဝယ် နူး ။ 
ကျွန်တော် မှား လောက် လိုက်ဟှိလား ။ 

==> triangulation.all <==
ရတိုင်း ကော ရုံလောက် ပဲ ၊ ခံဗျား ကော နေကော လား ။ 
သူးနို့ ကျွန်တော့ ငယ်ချင်း ဒွေ ဝို သိ ရယ် ။ 
ဟှယ်ဒူ့ ပေတံ ဟှယ် ။ 
ငါ ဗြော် ဖူးမျှခြား လူ ဒွေ ထက် နန် ပို စိတ်ဝင်စားဖို့ ကော ဟှယ် ။ 
အဲမှုဇာ ဟှို တိုင်း ဟှလား ။ 
သူ အယ်မျိုး လူ န မင်္ဂလာဆောင် ဟှို့ပဲ့လား ။ 
သူ့ဟှို သိပ်ပြီး ရတိုင်း ပြော နဲ့လန်း ။ 
ကျွန်တော် သူ့ဟှို သိ ဟှယ် ။ 
နန် ဟှယ်ရာ ဟှယ် နေဟှယ် ။ 
ကျွန်တော် မှား လုပ် ခဲ့ကြောက်လား ။ 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## WER Calculation with wer++.py

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ python2.7 /media/ye/project2/tool/WERpp/wer++.py ./transfer.all ./ref.all
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
[WW] Blank line in reference
WER: 59.37 (Ins: 2476 Dels: 3902 Subs: 17168 Ref: 39659 )
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

run with ignore option:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ python2.7 /media/ye/project2/tool/WERpp/wer++.py ./transfer.all ./ref.all -c -i
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
WER: 59.18 (Ins: 2476 Dels: 3827 Subs: 17168 Ref: 39659 )
```

Calculate CER (character error rate):  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ python2.7 /media/ye/project2/tool/WERpp/wer++.py ./transfer.all ./ref.all -c -i --cer
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
CER: 40.28 (Ins: 29066 Dels: 28870 Subs: 35862 Ref: 232852 )
```

Calcultate the number of keys need to correct erroneous words:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ python2.7 /media/ye/project2/tool/WERpp/wer++.py ./transfer.all ./ref.all -c -i -K
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
[WW] Blank line in reference, ignoring it
WER: 59.18 (Ins: 2476 Dels: 3827 Subs: 17168 Ref: 39659 )
Number of pressed keys: 171828
```

## Finding Blank Lines

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ./find-blank-lines.sh ./ref.all 
./ref.all:1143:
./ref.all:1369:
./ref.all:1459:
./ref.all:1654:
./ref.all:1692:
./ref.all:2619:
./ref.all:2668:
./ref.all:3043:
./ref.all:4008:
./ref.all:5109:
./ref.all:5180:
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ 
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ./find-blank-lines.sh ./baseline.all
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ./find-blank-lines.sh ./triangulation.all 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ./find-blank-lines.sh ./transfer.all 
```

## Check the Blank Line

```
1142 သူ အဲဟှို သွားလည် ဟှ သွားလည် လား ။	သူ အာမိုဇာ ဟှို သွား ဖူးရမော် ၊ သွား ကေ့လား ။ 
1143	အယ် ကွန်ဝါးယော့ ဝက်သက် ဘောပွတ် နေဟှယ် ။ 
1144 သူ ငါ  ပြောဇာဟှို ခိုး နားထွန် ခဲ့လား ။	သူ ကျွန်တော် ပြော ဇာဟှို ခိုး နားထွန် ခဲ့လား ။
```

```
1368 ငါ ဟှဲဇာ နားလည် ခဲ့ဟှ ။	ငါ ဟှဲဇာ နားလည် နေနူး ။ 
1369	ခြေနေ ဘယ်နှယ့်မျိုး ။ 
1370 ဈေးရောင်းမားဟှ ဟှယ်ဓာလေ ရောင်း နေနူး ။	အရောင်းဈေးသည် ဟှဲဇာ ရော နေဟှယ် ။ 
```

```
1458 အယ်ဝယ်ဟှား နန့်နားဟှို ဖောင်းဆစ် ဟှို့မှုဝလား ။	သူ နင့်နား ဖုန်းဆစ် မုဟှလား ။ 
1459	ဒီနေ့ ဒီခေတ်မှာလေ ခေတ်မီကိရိယာတွေနဲ့တိုင်းတာကြည့်တဲ့ခါ ကမ္ဘာကြီးကတိတိကျကျကို လုံးဝိုင်းနေတာ မဟုတ်ဘူးဆိုတာ ပြောပြနိုင်ပီ ။ 
1460 သူ နန့်ဝို မ ကြောက် ရ ။	သူ ဟှ နန့် ဟှို မ ကြောက်် ဟှ ။
```

```
1653 သူးလို့ စစ်တပ်ထဲ ဝင် ရဟှိ ပျော် နေကေဟှယ် ။	သူးနို့ စစ်တပ် ထဲ ဝမ် ရဟှိ ကြည်နူး နေကေဟှယ် ။ 
1654	ကျွနနွန်လေ ဝမ့် သန့်ရှင်း ငွေထည် ဟှို ဝပ် ပွတ်တိုက် ဟှယ် ။ 
1655 သူးနို့ ဆွေးနွီး ဇာကို ငါ ကြား ရှင်ဟှယ် ။	သူးနို့ ဆွေးနွေး စာ ငါ ကြား ရှင်ဟှယ် ။
```

```
1691 နန် သင်တန်း တတ် ဟှို့လား ။	နန် သင်တန်း တက် ဟှို့ မှုဟှလား ။ 
1692	ပင်လယ်ဟာ ယာ ငြိမ်သက် နေ လီ့မယ် ။ 
1693 ကျွန်တော် အယ်မျိုး မ လောက် ဟှ ။	ကျွန်တော် အယ်မျိုး မ လုပ် ဟှ ။ 
```

```
2618 တစ်ခါတစ်ခါ အယ်မိုဇာဟှ ပို ပျော်ဟှို့ ကောန် ဟှယ်  ။	ခါလေခါအား ပျော် ဟှို့ ကော ။ 
2619	သူ ဘယ်သူဖြစ်ဖြစ် ငါမတွေ့ချင်ဟ ။ 
2620 နန် ခု အိ ဟှမယ်လား ။	နန် ခု အိ တော့မယ်လား ။ 
```

```
2667 နန် ဟှဲဇာ  ပြော သင့်ဟှယ် ။	နန် ဟှဲဇာ ပြော သင့်နူး ။ 
2668 	နို့လေ မထွက်ခင် စာလောင်း တစ် လုံး န လုံး လော့ လက်နှိပ်စက် ရိုက် ပေးရဟှို့လား ။ 
2669 နန် ဟှယ်လူ့ဟှိုလဲ  ပြောဝ ဆိုပီး ကတိ ပေးထားဟှယ် ။	နန် ဖယ်သူ့ကိုမှ မ ပြောဘူး လေ ကတိ ပေးထားရယ် ။ 
```

```
3042 ကျွန်မ ဟှယ်သူ န  ပြောလို့ ရနိုင်မလဲ ။	ကျွန်မ နို့ ဘာသူ န ပြော လို့ရနိုင်ပါ့လဲ ။ 
3043	ကျေးဇူး အယ်ဇာဂို စာတိုက် သို့ ပို့ပေး ။ 
3044 နန် ဟှယ်လူ့ ဟှို   ပြစ်တန်ရစ် ဇာနူး ။	နန် ဟှယ်လူ့ ဟှို ပြစ်ပေး ခဲ့ဟှယ် ပြော ရစ်ဇာနူး ။
```

```
4007 အာမိုဇာ ဟှယ်လော့ ရွန်(လ်)လှ ဟှယ် ။	အာမိုဇာ ဟှယ်လော့ အရောင်လှ ဟှယ် ။ 
4008 	ပါဠိ ကို နန် ရတဲ့ အချက် ဟှို ငါ သိ ဟှ ။ 
4009 ရေဒီယို ဖွမ့် ဟှာ စိဆိုး ဟှို့လား ။	ရေဒီယို ဖွမ့် ဟှာ စိဆိုး ဟှို့လား ။
```

```
5108 အဲ့ဟှို ကျွန်တော် မ သွား ဟှ ။	အဲဟှို ကျွန်တော် မ သွား ဟှ ။ 
5109 	သူဝ ဝယ်ယား ဝို ရှစ် နေလား ။ 
5110 ဂုဏ် ပြု ခံရဝို လူ လေ ။	ဆုရ ရဟှို လူ လေ ။ 
```

```
5179 လေကျင့်ခန်းလုပ်ဟှို့ သင့်ဖစ် သေးရလော် ။	လေ့ကျင့်ခန်း လုပ် ဟှို့ သစ်ဖစ် သေးရလား ။ 
5180 	ကျွန်တော် ထင်မြင်ချင် ပေး ဟှိ ရဘဲ့လော် ။ 
5181 နန် ငါ့ ဂါး ဒေ ဟှို ယောင် ဟှို့မှုဟှ ။	နန် ငါ့ ဂါး လေ ဟှို ယုံ ဝို့ဟုတ်ဝ ။ 
```

## Adding Speaker-ID for Using with SCLITE Toolkit

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/add-spu_id.pl
--2022-01-26 16:33:13--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/add-spu_id.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.111.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 299 [text/plain]
Saving to: ‘add-spu_id.pl’

add-spu_id.pl                         100%[=========================================================================>]     299  --.-KB/s    in 0s      

2022-01-26 16:33:14 (8.78 MB/s) - ‘add-spu_id.pl’ saved [299/299]
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ cat add-spu_id.pl 
#!/usr/bin/perl
#use strict;

# last updated 19 Nov 2017
# ye@OPU
# for taging speaker ID

open (iFILE, $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!";

my $sentNo=1;

foreach $line(<iFILE>)
{

    chomp($line);
    print "$line (ye_$sentNo)\n";
    $sentNo = $sentNo+1;
}

close(iFILE);
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ 
```

Adding ID for baseline:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ perl ./add-spu_id.pl ./baseline.all > ./baseline.all.id
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head baseline.all.id 
သူ ခံဗျား ဟှို အဲဇာ ပေး ဟှို့မှုဝ ။  (ye_1)
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး ဇာနူး ။  (ye_2)
နည်း ပြေ တာပေါ့ ။  (ye_3)
နန် ဟှဲဇာ ရေး နူး ။  (ye_4)
ဆရာ လာ နေဟှယ် ။  (ye_5)
ဆရာ လာ နေဟှယ် ။  (ye_6)
သူ အင်္ဂလိပ် ဂါး ပြော နိုင်ဘဲ့လား ။  (ye_7)
နန် ဆေးလိ လျှော့ သော့-က့့့််် နေနူး ။  (ye_8)
သူးနို့ ငွေ စု ဟှ ၊ စု လား ။  (ye_9)
ဝယ်ယား ဟှ သူ့ ဟှို သိ ထားဇာ ။  (ye_10)
```

for reference:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ perl ./add-spu_id.pl ./ref.all > ref.all.id

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head ref.all.id 
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။ (ye_1)
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။ (ye_2)
သိပ်  ပြေ တာပေါ့ ။ (ye_3)
နန် ဟှဲဇာ ရေး နေဟှယ် ။  (ye_4)
ဆရာ လာပီ ။ (ye_5)
ဆရာ လာ ပီ ။ (ye_6)
သူ အန်းဂလီ ဂါး  ပြော နိုင်ဟှီးလား ။ (ye_7)
ခံဗျား ဆေးလိ လျှော့ သော့-က့့်် လိုက်မား ။ (ye_8)
သူးနို့ ငွေ စု ကေ့ဟှ ငွေ စု ကေ့လား ။ (ye_9)
ဝယ်ယား ဟှ သူ့ ဝို သိ ဟှားဇာ ။ (ye_10)
```

for transfer:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ perl ./add-spu_id.pl ./transfer.all > ./transfer.all.id
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head ./transfer.all.id 
သူ ခံဗျား ဟှို အဲ့မာ ပေး မှာ မှုဝ ။  (ye_1)
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး နူး ။  (ye_2)
ရတိုင်း ပြေ သွားမယ် ။  (ye_3)
နန် ဟှဲဇာ ရေး နူး ။  (ye_4)
ဆရာ လာ နေဟှယ် ။  (ye_5)
ဆရာ လာ နေဟှယ် ။  (ye_6)
သူ အမ်းဂလိ ဂါး ပြော နိုင်လား ။  (ye_7)
ခံဗျား ဆေးလိ လျှော့ သော့-က့့့််် နေနူး ။  (ye_8)
သူးနို့ ငွေ စု ဟှ စု လား ။  (ye_9)
သူ ဟှ သူ့ ဟှို သိ ဟှားဇာ ။  (ye_10)
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

for triangulation:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ perl ./add-spu_id.pl ./triangulation.all  > ./triangulation.all.id
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head ./triangulation.all.id 
သူ ခံဗျား ဟှို အဲ့မာ ပေး မှုဝ ။  (ye_1)
နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး ခဲ့နူး ။  (ye_2)
ရတိုင်း ပြေ တာပေါ့ ။  (ye_3)
နန် ဟှဲဇာ ရေး နေဟှယ် ။  (ye_4)
ဆရာ လာ နေဟှယ် ။  (ye_5)
ဆရာ လာ နေဟှယ် ။  (ye_6)
သူ အင်္ဂလိပ် ဂါး ပြော နိုင်လား ။  (ye_7)
နန် ဆေးလိ လျှော့ သော့-က့့်် ခဲ့ဟှယ် ။  (ye_8)
သူးနို့ ငွေ စု ဟှ စု လား ။  (ye_9)
သူ ဟှ သူ့ ဟှို သိ ထားဇာ ။  (ye_10)
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## Calculate WER for bk-my-dw

for baseline:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./baseline.all.id -i spu_id
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                         ./baseline.all.id                         |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   39659  | 50.2   43.3    6.5    9.7   59.5   93.9 |
     |===================================================================|
     | Sum/Avg|  6622   39659  | 50.2   43.3    6.5    9.7   59.5   93.9 |
     |===================================================================|
     |  Mean  |6622.0  39659.0 | 50.2   43.3    6.5    9.7   59.5   93.9 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  39659.0 | 50.2   43.3    6.5    9.7   59.5   93.9 |
     `-------------------------------------------------------------------'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./baseline.all.id -i spu_id -o pra
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'baseline.all.id.pra'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./baseline.all.id -i spu_id -o dtl
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'baseline.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

calcluation for Transfer:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./transfer.all.id -i spu_id
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                         ./transfer.all.id                         |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   39659  | 50.5   43.2    6.3    9.9   59.4   94.1 |
     |===================================================================|
     | Sum/Avg|  6622   39659  | 50.5   43.2    6.3    9.9   59.4   94.1 |
     |===================================================================|
     |  Mean  |6622.0  39659.0 | 50.5   43.2    6.3    9.9   59.4   94.1 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  39659.0 | 50.5   43.2    6.3    9.9   59.4   94.1 |
     `-------------------------------------------------------------------'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./transfer.all.id -i spu_id -o pra
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'transfer.all.id.pra'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./transfer.all.id -i spu_id -o dtl
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'transfer.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

calculation for Triangulation:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./triangulation.all.id -i spu_id
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                      ./triangulation.all.id                       |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   39659  | 49.9   42.9    7.2    8.3   58.4   94.0 |
     |===================================================================|
     | Sum/Avg|  6622   39659  | 49.9   42.9    7.2    8.3   58.4   94.0 |
     |===================================================================|
     |  Mean  |6622.0  39659.0 | 49.9   42.9    7.2    8.3   58.4   94.0 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  39659.0 | 49.9   42.9    7.2    8.3   58.4   94.0 |
     `-------------------------------------------------------------------'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./triangulation.all.id -i spu_id -o pra
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'triangulation.all.id.pra'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ sclite -r ./ref.all.id -h ./triangulation.all.id -i spu_id -o dtl
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'triangulation.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## Preparation for bk-my-rk

perl script ကို one upper folder မှာ ကော်ပီကူးထားခဲ့...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ cp ../bk-my-dw/add-spu_id.pl ../
```

run mk-one-big-file.sh  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ cp ../bk-my-dw/mk-one-big-file.sh .
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ gedit mk-one-big-file.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ ./mk-one-big-file.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ ls *.all
baseline.all  ref.all  transfer.all  triangulation.all
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ wc *.all
  10720   69755 1089184 baseline.all
  10720   68975 1123939 ref.all
  10720   69164 1101961 transfer.all
  10720   69126 1088996 triangulation.all
  42880  277020 4404080 total
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$
```

## WER Calculation for bk-my-rk

Prepare a shell script:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ cat ./wer-calc-all.sh 
#!/bin/bash

for method in {baseline,transfer,triangulation}
do
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o pra
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o dtl
done

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ 
```

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ ./wer-calc-all.sh 
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                         ./baseline.all.id                          |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    68975  | 63.4   29.4    7.2    8.3   44.9   85.5 |
     |====================================================================|
     | Sum/Avg| 10720    68975  | 63.4   29.4    7.2    8.3   44.9   85.5 |
     |====================================================================|
     |  Mean  |10720.0  68975.0 | 63.4   29.4    7.2    8.3   44.9   85.5 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  68975.0 | 63.4   29.4    7.2    8.3   44.9   85.5 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'baseline.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'baseline.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                         ./transfer.all.id                          |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    68975  | 63.2   29.2    7.6    7.9   44.7   85.7 |
     |====================================================================|
     | Sum/Avg| 10720    68975  | 63.2   29.2    7.6    7.9   44.7   85.7 |
     |====================================================================|
     |  Mean  |10720.0  68975.0 | 63.2   29.2    7.6    7.9   44.7   85.7 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  68975.0 | 63.2   29.2    7.6    7.9   44.7   85.7 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'transfer.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'transfer.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                       ./triangulation.all.id                       |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    68975  | 63.9   28.8    7.3    7.5   43.6   84.7 |
     |====================================================================|
     | Sum/Avg| 10720    68975  | 63.9   28.8    7.3    7.5   43.6   84.7 |
     |====================================================================|
     |  Mean  |10720.0  68975.0 | 63.9   28.8    7.3    7.5   43.6   84.7 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  68975.0 | 63.9   28.8    7.3    7.5   43.6   84.7 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'triangulation.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'triangulation.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$
```

## Preparation for dw-my-bk

prepare a shell script for combining all 10-fold running results into one big file:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ cat ./mk-one-big-file.sh 
#!/bin/bash

cat dw-my-bk.ref1 dw-my-bk.ref2 dw-my-bk.ref3 dw-my-bk.ref4 dw-my-bk.ref5 dw-my-bk.ref6 dw-my-bk.ref7 dw-my-bk.ref8 dw-my-bk.ref9 dw-my-bk.ref10 > ref.all
cat baseline.opt1 baseline.opt2 baseline.opt3 baseline.opt4 baseline.opt5 baseline.opt6 baseline.opt7 baseline.opt8 baseline.opt9 baseline.opt10 > baseline.all
cat transfer.opt1 transfer.opt2 transfer.opt3 transfer.opt4 transfer.opt5 transfer.opt6 transfer.opt7 transfer.opt8 transfer.opt9 transfer.opt10 > transfer.all
cat triangulation.opt1 triangulation.opt2 triangulation.opt3 triangulation.opt4 triangulation.opt5 triangulation.opt6 triangulation.opt7 triangulation.opt8 triangulation.opt9 triangulation.opt10 > triangulation.all

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

run above script ...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ ./mk-one-big-file.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ ls *.all
baseline.all  ref.all  transfer.all  triangulation.all
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

add ID:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ cp ../add-id-all.sh .
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ ./add-id-all.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ wc *.id
   6622   47736  675973 baseline.all.id
   6622   48575  666601 ref.all.id
   6622   47212  672855 transfer.all.id
   6622   47618  668609 triangulation.all.id
  26488  191141 2684038 total
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

Prepare for running SCLITE:  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ cp ../bk-my-rk/wer-calc-all.sh .
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ cat wer-calc-all.sh 
#!/bin/bash

for method in {baseline,transfer,triangulation}
do
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o pra
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o dtl
done

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

Calc WER ...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ ./wer-calc-all.sh 
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                         ./baseline.all.id                         |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   41953  | 50.6   40.3    9.1    7.1   56.5   94.2 |
     |===================================================================|
     | Sum/Avg|  6622   41953  | 50.6   40.3    9.1    7.1   56.5   94.2 |
     |===================================================================|
     |  Mean  |6622.0  41953.0 | 50.6   40.3    9.1    7.1   56.5   94.2 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  41953.0 | 50.6   40.3    9.1    7.1   56.5   94.2 |
     `-------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'baseline.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'baseline.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                         ./transfer.all.id                         |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   41953  | 49.7   40.6    9.7    6.4   56.7   94.5 |
     |===================================================================|
     | Sum/Avg|  6622   41953  | 49.7   40.6    9.7    6.4   56.7   94.5 |
     |===================================================================|
     |  Mean  |6622.0  41953.0 | 49.7   40.6    9.7    6.4   56.7   94.5 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  41953.0 | 49.7   40.6    9.7    6.4   56.7   94.5 |
     `-------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'transfer.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'transfer.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,-------------------------------------------------------------------.
     |                      ./triangulation.all.id                       |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | ye     |  6622   41953  | 50.5   40.6    8.8    6.6   56.0   94.7 |
     |===================================================================|
     | Sum/Avg|  6622   41953  | 50.5   40.6    8.8    6.6   56.0   94.7 |
     |===================================================================|
     |  Mean  |6622.0  41953.0 | 50.5   40.6    8.8    6.6   56.0   94.7 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |6622.0  41953.0 | 50.5   40.6    8.8    6.6   56.0   94.7 |
     `-------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          

    Writing string alignments to 'triangulation.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 6622 for speaker ye          

    Writing overall detailed scoring report 'triangulation.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

## Preparation for rk-my-bk

script ကို ပြင်ခဲ့...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ cat ./mk-one-big-file.sh 
#!/bin/bash

cat rk-my-bk.ref1 rk-my-bk.ref2 rk-my-bk.ref3 rk-my-bk.ref4 rk-my-bk.ref5 rk-my-bk.ref6 rk-my-bk.ref7 rk-my-bk.ref8 rk-my-bk.ref9 rk-my-bk.ref10 > ref.all
cat baseline.opt1 baseline.opt2 baseline.opt3 baseline.opt4 baseline.opt5 baseline.opt6 baseline.opt7 baseline.opt8 baseline.opt9 baseline.opt10 > baseline.all
cat transfer.opt1 transfer.opt2 transfer.opt3 transfer.opt4 transfer.opt5 transfer.opt6 transfer.opt7 transfer.opt8 transfer.opt9 transfer.opt10 > transfer.all
cat triangulation.opt1 triangulation.opt2 triangulation.opt3 triangulation.opt4 triangulation.opt5 triangulation.opt6 triangulation.opt7 triangulation.opt8 triangulation.opt9 triangulation.opt10 > triangulation.all

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```

10-fold ခွဲပြီး run ထားတာကို big-file ဖြစ်အောင် အထက်ပါ script ကို run ခဲ့တယ်...  
output အနေနဲ့ ".all" ဖိုင်တွေရလာလိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ ./mk-one-big-file.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ ls *.all
baseline.all  ref.all  transfer.all  triangulation.all
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```

အထက်က .all ဖိုင်အားလုံးကို ID တပ်ရမယ်။  
SCLITE tool ကို သုံးဖို့အတွက်က အဲဒီ ID တပ်ထားတဲ့ format ကို input လုပ်ပေးရမှာမို့...  

ရှေ့မှာလည်း သုံးပြခဲ့တဲ့အတိုင်းပါပဲ...  
add-id-all.sh က အောက်ပါအတိုင်းပါ...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ cat ../add-id-all.sh 
#!/bin/bash

perl ../add-spu_id.pl ./baseline.all > ./baseline.all.id
perl ../add-spu_id.pl ./ref.all > ./ref.all.id
perl ../add-spu_id.pl ./transfer.all > ./transfer.all.id
perl ../add-spu_id.pl ./triangulation.all > ./triangulation.all.id


(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ cp ../add-id-all.sh .
```

အောက်ပါအတိုင်း run လိုက်ရင် id တပ်ပြီးသား output ဖိုင်တွေ ရလာလိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ ./add-id-all.sh 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ ls *.id
baseline.all.id  ref.all.id  transfer.all.id  triangulation.all.id
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```

WER တွက်ဖို့အတွက် ရှေ့မှာ ပြင်ထားခဲ့တဲ့ shell script ကို လက်ရှိ path အောက်ကို copy ကူယူခဲ့...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ cp ../bk-my-rk/wer-calc-all.sh .
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ cat wer-calc-all.sh 
#!/bin/bash

for method in {baseline,transfer,triangulation}
do
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o pra
   sclite -r ./ref.all.id -h ./$method.all.id -i spu_id -o dtl
done

(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```

## WER Calculation for rk-my-bk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ ./wer-calc-all.sh 
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                         ./baseline.all.id                          |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    70434  | 59.2   34.5    6.3    6.8   47.6   90.0 |
     |====================================================================|
     | Sum/Avg| 10720    70434  | 59.2   34.5    6.3    6.8   47.6   90.0 |
     |====================================================================|
     |  Mean  |10720.0  70434.0 | 59.2   34.5    6.3    6.8   47.6   90.0 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  70434.0 | 59.2   34.5    6.3    6.8   47.6   90.0 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'baseline.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './baseline.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'baseline.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                         ./transfer.all.id                          |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    70434  | 59.6   34.2    6.3    6.6   47.0   88.7 |
     |====================================================================|
     | Sum/Avg| 10720    70434  | 59.6   34.2    6.3    6.6   47.0   88.7 |
     |====================================================================|
     |  Mean  |10720.0  70434.0 | 59.6   34.2    6.3    6.6   47.0   88.7 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  70434.0 | 59.6   34.2    6.3    6.6   47.0   88.7 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'transfer.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './transfer.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'transfer.all.id.dtl'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER                      

     ,--------------------------------------------------------------------.
     |                       ./triangulation.all.id                       |
     |--------------------------------------------------------------------|
     | SPKR   |  # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+-----------------+-----------------------------------------|
     | ye     | 10720    70434  | 59.6   34.4    6.0    6.9   47.3   89.3 |
     |====================================================================|
     | Sum/Avg| 10720    70434  | 59.6   34.4    6.0    6.9   47.3   89.3 |
     |====================================================================|
     |  Mean  |10720.0  70434.0 | 59.6   34.4    6.0    6.9   47.3   89.3 |
     |  S.D.  |   0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |10720.0  70434.0 | 59.6   34.4    6.0    6.9   47.3   89.3 |
     `--------------------------------------------------------------------'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          

    Writing string alignments to 'triangulation.all.id.pra'

Successful Completion
sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ref.all.id' and Hyp File: './triangulation.all.id'
    Alignment# 10720 for speaker ye          

    Writing overall detailed scoring report 'triangulation.all.id.dtl'

Successful Completion
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```

တွက်တာ အားလုံး ပြီးသွားပြီ။ ရလဒ်တွေကို အသေးစိတ်ကြည့်ရမယ်။  
အဲဒီအတွက်က ".dtl" နဲ့ ".pra" ဖိုင်တွေကို ဝင်ကြည့်ပါ။  

ဥပမာ bk-my-dw အတွက် ဆိုရင် အောက်ပါ ဖိုင်တွေကို ကြည့်ရပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ls *.dtl
baseline.all.id.dtl  transfer.all.id.dtl  triangulation.all.id.dtl
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ ls *.pra
baseline.all.id.pra  transfer.all.id.pra  triangulation.all.id.pra
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## Let's See ".dtl" File

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head -50 ./baseline.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./baseline.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             93.9%   (6220)

   with substitions                      92.6%   (6130)
   with deletions                        26.8%   (1772)
   with insertions                       37.0%   (2451)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   59.5%   (23582)

Percent Correct           =   50.2%   (19918)

Percent Substitution      =   43.3%   (17157)
Percent Deletions         =    6.5%   (2584)
Percent Insertions        =    9.7%   (3841)
Percent Word Accuracy     =   40.5%


Ref. words                =           (39659)
Hyp. words                =           (40916)
Aligned words             =           (43500)

CONFUSION PAIRS                  Total                 (13557)
                                 With >=  1 occurrences (13557)

   1:   91  ->  နူး ==> ဟှယ်
   2:   80  ->  ငါ ==> ကျွန်တော်
   3:   75  ->  ခံဗျား ==> နန်
   4:   70  ->  ဝို ==> ဟှို
   5:   39  ->  ကို ==> ဟှို
   6:   39  ->  ကျွန်တော် ==> ငါ
   7:   32  ->  ရယ် ==> ဟှယ်
   8:   32  ->  လုပ် ==> လောက်
   9:   32  ->  သူ့ဟှို ==> ဟှို
  10:   31  ->  ရ ==> ဟှ
  11:   31  ->  လောက် ==> လုပ်
  12:   29  ->  နူး ==> နေဟှယ်
  13:   29  ->  ရှိဟှယ် ==> ဟှယ်
  14:   27  ->  အဲဝယ်ဟှား ==> သူ
  15:   26  ->  နေနူး ==> နေဟှယ်
  16:   25  ->  အယ်ဝယ်ဟှား ==> သူ
  17:   24  ->  ဟှို ==> ဝို
  18:   23  ->  နန့် ==> နန်
  19:   20  ->  ခံဗျား ==> နန့်
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## Let's See ".pra" File

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head -50 ./baseline.all.id.pra


		DUMP OF SYSTEM ALIGNMENT STRUCTURE

System name:   ./baseline.all.id

Speakers: 
    0:  ye

Speaker sentences   0:  ye   #utts: 6622
id: (ye_1)
Scores: (#C #S #D #I) 5 2 1 0
REF:  အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ                ။ 
HYP:  သူ                      ခံဗျား ဟှို အဲဇာ ပေး *************** ဟှို့မှုဝ ။ 
Eval: S                                                                                  D               S                               

id: (ye_2)
Scores: (#C #S #D #I) 4 2 0 0
REF:  နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး       ရစ်ဇာနူး ။ 
HYP:  နန် ဟှယ်လူ့ ဟှို စိတ်ညစ်ပေး ဇာနူး          ။ 
Eval:                                              S                              S                            

id: (ye_3)
Scores: (#C #S #D #I) 3 1 0 0
REF:  သိပ် ပြေ တာပေါ့ ။ 
HYP:  နည်း ပြေ တာပေါ့ ။ 
Eval: S                                             

id: (ye_4)
Scores: (#C #S #D #I) 4 1 0 0
REF:  နန် ဟှဲဇာ ရေး နေဟှယ် ။ 
HYP:  နန် ဟှဲဇာ ရေး နူး          ။ 
Eval:                                     S                      

id: (ye_5)
Scores: (#C #S #D #I) 2 1 0 1
REF:  ဆရာ ****** လာပီ       ။ 
HYP:  ဆရာ လာ နေဟှယ် ။ 
Eval:           I      S                      

id: (ye_6)
Scores: (#C #S #D #I) 3 1 0 0
REF:  ဆရာ လာ ပီ             ။ 
HYP:  ဆရာ လာ နေဟှယ် ။ 
Eval:                  S                      

id: (ye_7)
Scores: (#C #S #D #I) 4 2 0 0
REF:  သူ အန်းဂလီ       ဂါး ပြော နိုင်ဟှီးလား ။ 
HYP:  သူ အင်္ဂလိပ် ဂါး ပြော နိုင်ဘဲ့လား    ။ 
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$
```

## Prepare Top 10 Confusion Pairs

ဒီတစ်ခေါက်က top 10 confusion pair ကို အဓိက စိတ်ဝင်စားတာမို့ ".dtl" ဖိုင်တွေကိုပဲ ကြည့်ပြီး top 10 တွေပဲ လေ့လာပါမယ်။  
နည်းနည်း အသေးစိတ် ပိုသိချင်လို့ လိုရမယ်ရ top 20 ထုတ်ထားမယ်။

### for Confusion Pairs for bk-my-dw

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head -51 ./baseline.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./baseline.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             93.9%   (6220)

   with substitions                      92.6%   (6130)
   with deletions                        26.8%   (1772)
   with insertions                       37.0%   (2451)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   59.5%   (23582)

Percent Correct           =   50.2%   (19918)

Percent Substitution      =   43.3%   (17157)
Percent Deletions         =    6.5%   (2584)
Percent Insertions        =    9.7%   (3841)
Percent Word Accuracy     =   40.5%


Ref. words                =           (39659)
Hyp. words                =           (40916)
Aligned words             =           (43500)

CONFUSION PAIRS                  Total                 (13557)
                                 With >=  1 occurrences (13557)

   1:   91  ->  နူး ==> ဟှယ်
   2:   80  ->  ငါ ==> ကျွန်တော်
   3:   75  ->  ခံဗျား ==> နန်
   4:   70  ->  ဝို ==> ဟှို
   5:   39  ->  ကို ==> ဟှို
   6:   39  ->  ကျွန်တော် ==> ငါ
   7:   32  ->  ရယ် ==> ဟှယ်
   8:   32  ->  လုပ် ==> လောက်
   9:   32  ->  သူ့ဟှို ==> ဟှို
  10:   31  ->  ရ ==> ဟှ
  11:   31  ->  လောက် ==> လုပ်
  12:   29  ->  နူး ==> နေဟှယ်
  13:   29  ->  ရှိဟှယ် ==> ဟှယ်
  14:   27  ->  အဲဝယ်ဟှား ==> သူ
  15:   26  ->  နေနူး ==> နေဟှယ်
  16:   25  ->  အယ်ဝယ်ဟှား ==> သူ
  17:   24  ->  ဟှို ==> ဝို
  18:   23  ->  နန့် ==> နန်
  19:   20  ->  ခံဗျား ==> နန့်
  20:   20  ->  ဟှယ် ==> နူး
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head -51 ./transfer.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./transfer.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             94.1%   (6233)

   with substitions                      92.6%   (6129)
   with deletions                        25.9%   (1717)
   with insertions                       37.7%   (2495)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   59.4%   (23549)

Percent Correct           =   50.5%   (20039)

Percent Substitution      =   43.2%   (17117)
Percent Deletions         =    6.3%   (2503)
Percent Insertions        =    9.9%   (3929)
Percent Word Accuracy     =   40.6%


Ref. words                =           (39659)
Hyp. words                =           (41085)
Aligned words             =           (43588)

CONFUSION PAIRS                  Total                 (13045)
                                 With >=  1 occurrences (13045)

   1:  103  ->  ငါ ==> ကျွန်တော်
   2:   89  ->  ဝို ==> ဟှို
   3:   87  ->  နူး ==> ဟှယ်
   4:   81  ->  ခံဗျား ==> နန်
   5:   56  ->  နန့် ==> နန်
   6:   50  ->  နေဟှယ် ==> နူး
   7:   48  ->  သူးလေ ==> သူးနို့
   8:   45  ->  လုပ် ==> လောက်
   9:   44  ->  အဲဝယ်ဟှား ==> သူ
  10:   42  ->  ရယ် ==> ဟှယ်
  11:   40  ->  ကို ==> ဟှို
  12:   38  ->  ရ ==> ဟှ
  13:   36  ->  လောက် ==> လုပ်
  14:   35  ->  သူ့ဟှို ==> ဟှို
  15:   34  ->  ဟှယ် ==> နူး
  16:   31  ->  ကျွန်တော် ==> ငါ
  17:   28  ->  အယ်ဝယ်ဟှား ==> သူ
  18:   27  ->  က ==> ဟှ
  19:   26  ->  နန့်ဟှို ==> ဟှို
  20:   23  ->  နေနူး ==> နူး
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ head -51 ./triangulation.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./triangulation.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             94.0%   (6227)

   with substitions                      92.5%   (6127)
   with deletions                        29.7%   (1970)
   with insertions                       32.3%   (2137)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   58.4%   (23163)

Percent Correct           =   49.9%   (19786)

Percent Substitution      =   42.9%   (17011)
Percent Deletions         =    7.2%   (2862)
Percent Insertions        =    8.3%   (3290)
Percent Word Accuracy     =   41.6%


Ref. words                =           (39659)
Hyp. words                =           (40087)
Aligned words             =           (42949)

CONFUSION PAIRS                  Total                 (13229)
                                 With >=  1 occurrences (13229)

   1:   93  ->  နူး ==> ဟှယ်
   2:   84  ->  ခံဗျား ==> နန်
   3:   77  ->  ငါ ==> ကျွန်တော်
   4:   58  ->  ဝို ==> ဟှို
   5:   41  ->  ရယ် ==> ဟှယ်
   6:   40  ->  ရ ==> ဟှ
   7:   37  ->  နန့် ==> နန်
   8:   37  ->  လုပ် ==> လောက်
   9:   37  ->  လောက် ==> လုပ်
  10:   37  ->  သူးလေ ==> သူးနို့
  11:   35  ->  နေနူး ==> နေဟှယ်
  12:   34  ->  အဲဝယ်ဟှား ==> သူ
  13:   33  ->  ကို ==> ဟှို
  14:   32  ->  ကျွန်တော် ==> ငါ
  15:   31  ->  နူး ==> နေဟှယ်
  16:   26  ->  က ==> ဟှ
  17:   26  ->  ဟှို ==> သူ့ဟှို
  18:   26  ->  အယ်ဝယ်ဟှား ==> သူ
  19:   24  ->  ရှိဟှယ် ==> ဟှယ်
  20:   23  ->  မှုဝ ==> မှုဟှ
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-dw$ 
```

### Confusion Pairs for bk-my-rk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ head -51 ./baseline.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./baseline.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             85.5%   (9161)

   with substitions                      84.3%   (9032)
   with deletions                        29.7%   (3188)
   with insertions                       36.2%   (3876)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   44.9%   (30983)

Percent Correct           =   63.4%   (43750)

Percent Substitution      =   29.4%   (20247)
Percent Deletions         =    7.2%   (4978)
Percent Insertions        =    8.3%   (5758)
Percent Word Accuracy     =   55.1%


Ref. words                =           (68975)
Hyp. words                =           (69755)
Aligned words             =           (74733)

CONFUSION PAIRS                  Total                 (14542)
                                 With >=  1 occurrences (14542)

   1:   97  ->  ကျွန်တော် ==> ငါ
   2:   90  ->  မင်းကို ==> ကို
   3:   86  ->  ထိုမချေ ==> သူ
   4:   83  ->  ပါလား။ ==> ။
   5:   80  ->  ငါ ==> ကျွန်တော်
   6:   80  ->  ရေ။ ==> ။
   7:   78  ->  ပါ။ ==> ။
   8:   62  ->  လေး။ ==> ။
   9:   57  ->  လား ==> ပါလား
  10:   54  ->  ပါရေ။ ==> ။
  11:   51  ->  ပါရေ ==> ရေ
  12:   49  ->  ရို့ ==> သူရို့
  13:   47  ->  ယင်း ==> ယင်းချင့်
  14:   47  ->  ယင်းချင့်ကို ==> ကို
  15:   47  ->  ။ ==> ရေ။
  16:   45  ->  ခပါ ==> ပါ
  17:   41  ->  ရို့ ==> ကျွန်တော်ရို့
  18:   39  ->  ကျွန်တော်ရို့ ==> ရို့
  19:   39  ->  နီရေ။ ==> ။
  20:   39  ->  မဟုတ်ပါ ==> ပါ
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ head -51 ./transfer.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./transfer.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             85.7%   (9185)

   with substitions                      84.2%   (9031)
   with deletions                        31.3%   (3354)
   with insertions                       34.8%   (3734)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   44.7%   (30830)

Percent Correct           =   63.2%   (43590)

Percent Substitution      =   29.2%   (20129)
Percent Deletions         =    7.6%   (5256)
Percent Insertions        =    7.9%   (5445)
Percent Word Accuracy     =   55.3%


Ref. words                =           (68975)
Hyp. words                =           (69164)
Aligned words             =           (74420)

CONFUSION PAIRS                  Total                 (14444)
                                 With >=  1 occurrences (14444)

   1:  104  ->  ပါလား။ ==> ။
   2:   95  ->  ငါ ==> ကျွန်တော်
   3:   89  ->  ရေ။ ==> ။
   4:   83  ->  ထိုမချေ ==> သူ
   5:   81  ->  ကျွန်တော် ==> ငါ
   6:   80  ->  ပါ။ ==> ။
   7:   70  ->  မင်းကို ==> ကို
   8:   67  ->  လေး။ ==> ။
   9:   62  ->  ပါရေ။ ==> ။
  10:   60  ->  ရို့ ==> သူရို့
  11:   55  ->  ကို ==> ယင်းချင့်ကို
  12:   54  ->  ရို့ ==> ကျွန်တော်ရို့
  13:   54  ->  လား ==> ပါလား
  14:   52  ->  ။ ==> ဖို့လေး။
  15:   49  ->  ကို ==> မင်းကို
  16:   48  ->  ပါရေ ==> ရေ
  17:   44  ->  ခပါ ==> ပါ
  18:   41  ->  ကို ==> သူ့ကို
  19:   41  ->  ယင်း ==> ယင်းချင့်
  20:   39  ->  နီရေ။ ==> ။
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$ head -51 ./triangulation.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./triangulation.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             84.7%   (9083)

   with substitions                      83.1%   (8908)
   with deletions                        30.5%   (3274)
   with insertions                       33.9%   (3635)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   43.6%   (30053)

Percent Correct           =   63.9%   (44097)

Percent Substitution      =   28.8%   (19854)
Percent Deletions         =    7.3%   (5024)
Percent Insertions        =    7.5%   (5175)
Percent Word Accuracy     =   56.4%


Ref. words                =           (68975)
Hyp. words                =           (69126)
Aligned words             =           (74150)

CONFUSION PAIRS                  Total                 (14373)
                                 With >=  1 occurrences (14373)

   1:   98  ->  ပါလား။ ==> ။
   2:   86  ->  ငါ ==> ကျွန်တော်
   3:   86  ->  ရေ။ ==> ။
   4:   80  ->  ပါ။ ==> ။
   5:   74  ->  မင်းကို ==> ကို
   6:   73  ->  ကျွန်တော် ==> ငါ
   7:   67  ->  ထိုမချေ ==> သူ
   8:   63  ->  လေး။ ==> ။
   9:   60  ->  ပါရေ။ ==> ။
  10:   56  ->  ရို့ ==> သူရို့
  11:   52  ->  ။ ==> ဖို့လေး။
  12:   51  ->  ရို့ ==> ကျွန်တော်ရို့
  13:   50  ->  လား ==> ပါလား
  14:   48  ->  ကို ==> ယင်းချင့်ကို
  15:   47  ->  ပါရေ ==> ရေ
  16:   45  ->  ယင်း ==> ယင်းချင့်
  17:   43  ->  ခပါ ==> ပါ
  18:   38  ->  ယင်းချင့်ကို ==> ကို
  19:   37  ->  ခပါလား။ ==> ။
  20:   37  ->  နီရေ။ ==> ။
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/bk-my-rk$
```

## Confusion Pairs for dw-my-bk 

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ head -51 ./baseline.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./baseline.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             94.2%   (6241)

   with substitions                      92.7%   (6140)
   with deletions                        36.5%   (2414)
   with insertions                       30.0%   (1984)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   56.5%   (23690)

Percent Correct           =   50.6%   (21232)

Percent Substitution      =   40.3%   (16913)
Percent Deletions         =    9.1%   (3808)
Percent Insertions        =    7.1%   (2969)
Percent Word Accuracy     =   43.5%


Ref. words                =           (41953)
Hyp. words                =           (41114)
Aligned words             =           (44922)

CONFUSION PAIRS                  Total                 (12902)
                                 With >=  1 occurrences (12902)

   1:  136  ->  မင်း ==> နင်
   2:  127  ->  ဝို ==> ကို
   3:   87  ->  ကျွန်တော် ==> ငါ
   4:   67  ->  ကို ==> ဝို
   5:   66  ->  ရယ် ==> ရိ
   6:   55  ->  ဒယ်ကောင်မငယ် ==> သူ
   7:   49  ->  ခင်ဗျား ==> နင်
   8:   49  ->  မ ==> ကို
   9:   44  ->  လဲ ==> ရိ
  10:   39  ->  ဝ ==> ရ
  11:   34  ->  နေရယ် ==> ရိ
  12:   32  ->  ကလား ==> ရလား
  13:   32  ->  မင်း ==> နင့်
  14:   28  ->  သော ==> သွား
  15:   27  ->  ရိ ==> ရယ်
  16:   24  ->  သူ ==> ဒယ်ကောင်မငယ်
  17:   23  ->  ဘယ်သူ့ ==> ဖယ်သူ့
  18:   23  ->  ရယ်လား ==> လား
  19:   22  ->  ဝယ် ==> ရယ်
  20:   21  ->  ငါ့ဝို ==> ကို
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ head -51 ./transfer.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./transfer.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             94.5%   (6256)

   with substitions                      92.9%   (6150)
   with deletions                        38.9%   (2577)
   with insertions                       27.1%   (1792)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   56.7%   (23794)

Percent Correct           =   49.7%   (20859)

Percent Substitution      =   40.6%   (17031)
Percent Deletions         =    9.7%   (4063)
Percent Insertions        =    6.4%   (2700)
Percent Word Accuracy     =   43.3%


Ref. words                =           (41953)
Hyp. words                =           (40590)
Aligned words             =           (44653)

CONFUSION PAIRS                  Total                 (12650)
                                 With >=  1 occurrences (12650)

   1:  156  ->  မင်း ==> နင်
   2:  117  ->  ဝို ==> ကို
   3:   93  ->  ကျွန်တော် ==> ငါ
   4:   89  ->  ကို ==> ဝို
   5:   69  ->  ရယ် ==> ရိ
   6:   55  ->  ဒယ်ကောင်မငယ် ==> သူ
   7:   51  ->  သူ ==> ဒယ်ကောင်မငယ်
   8:   48  ->  ခင်ဗျား ==> နင်
   9:   47  ->  မ ==> ကို
  10:   43  ->  လဲ ==> ရိ
  11:   37  ->  ဝ ==> ရ
  12:   35  ->  နေရယ် ==> ရိ
  13:   30  ->  ကလား ==> ရလား
  14:   29  ->  ကျနော် ==> ငါ
  15:   28  ->  နင့် ==> နင်
  16:   28  ->  ဝယ် ==> ရယ်
  17:   28  ->  သော ==> သွား
  18:   26  ->  ရိ ==> ရယ်
  19:   25  ->  မင့် ==> နင်
  20:   24  ->  နင့်ဝို ==> ကို
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$ head -51 ./triangulation.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./triangulation.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        6622
 with errors                             94.7%   (6272)

   with substitions                      93.4%   (6182)
   with deletions                        35.7%   (2367)
   with insertions                       28.1%   (1860)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   56.0%   (23510)

Percent Correct           =   50.5%   (21198)

Percent Substitution      =   40.6%   (17043)
Percent Deletions         =    8.8%   (3712)
Percent Insertions        =    6.6%   (2755)
Percent Word Accuracy     =   44.0%


Ref. words                =           (41953)
Hyp. words                =           (40996)
Aligned words             =           (44708)

CONFUSION PAIRS                  Total                 (12651)
                                 With >=  1 occurrences (12651)

   1:  149  ->  မင်း ==> နင်
   2:  147  ->  ဝို ==> ကို
   3:  104  ->  ကျွန်တော် ==> ငါ
   4:   84  ->  ကို ==> ဝို
   5:   65  ->  ဒယ်ကောင်မငယ် ==> သူ
   6:   59  ->  ရယ် ==> ရိ
   7:   55  ->  ခင်ဗျား ==> နင်
   8:   48  ->  ရိ ==> ရယ်
   9:   41  ->  မ ==> ကို
  10:   41  ->  လဲ ==> ရိ
  11:   36  ->  ဝ ==> ရ
  12:   35  ->  သူ ==> ဒယ်ကောင်မငယ်
  13:   34  ->  ဘာဇာတွေ ==> ဘာ
  14:   33  ->  သော ==> သွား
  15:   31  ->  ကလား ==> ရလား
  16:   30  ->  ကျနော် ==> ငါ
  17:   27  ->  နင့်ဝို ==> ကို
  18:   27  ->  နေရယ် ==> ရိ
  19:   26  ->  နင့် ==> နင်
  20:   26  ->  ဝယ် ==> ရယ်
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/dw-my-bk$
```

### Confusion Pairs for rk-my-bk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ head -51 ./baseline.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./baseline.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             90.0%   (9651)

   with substitions                      88.7%   (9505)
   with deletions                        28.0%   (3004)
   with insertions                       28.1%   (3017)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   47.6%   (33518)

Percent Correct           =   59.2%   (41692)

Percent Substitution      =   34.5%   (24291)
Percent Deletions         =    6.3%   (4451)
Percent Insertions        =    6.8%   (4776)
Percent Word Accuracy     =   52.4%


Ref. words                =           (70434)
Hyp. words                =           (70759)
Aligned words             =           (75210)

CONFUSION PAIRS                  Total                 (16476)
                                 With >=  1 occurrences (16476)

   1:  317  ->  ဝို ==> ကို
   2:  259  ->  မင်း ==> နင်
   3:  213  ->  ကို ==> ဝို
   4:  109  ->  ကျွန်တော် ==> ငါ
   5:  107  ->  ငါ ==> ကျွန်တော်
   6:  104  ->  မင့် ==> နင်
   7:  103  ->  ခင်ဗျား ==> နင်
   8:   71  ->  သူ ==> ဒယ်ကောင်မငယ်
   9:   63  ->  နင် ==> မင်း
  10:   62  ->  ဒယ်ကောင်မငယ် ==> သူ
  11:   60  ->  ဝယ် ==> ရယ်
  12:   59  ->  နင့် ==> မင်း
  13:   59  ->  ဘယ်သူ့ ==> ဖယ်သူ့
  14:   59  ->  အဲ့အမ ==> ဒယ်ကောင်မငယ်
  15:   56  ->  မင်း ==> နင့်
  16:   50  ->  ဖို့ ==> ဝို့
  17:   50  ->  လဲ ==> ရိ
  18:   49  ->  သော ==> သွား
  19:   45  ->  ဝို့ ==> ဖို့
  20:   44  ->  ငါလို့ ==> ကျွန်တော်ဝို့
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ head -51 ./transfer.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./transfer.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             88.7%   (9512)

   with substitions                      87.5%   (9376)
   with deletions                        28.0%   (2998)
   with insertions                       27.3%   (2931)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   47.0%   (33139)

Percent Correct           =   59.6%   (41971)

Percent Substitution      =   34.2%   (24058)
Percent Deletions         =    6.3%   (4405)
Percent Insertions        =    6.6%   (4676)
Percent Word Accuracy     =   53.0%


Ref. words                =           (70434)
Hyp. words                =           (70705)
Aligned words             =           (75110)

CONFUSION PAIRS                  Total                 (16183)
                                 With >=  1 occurrences (16183)

   1:  279  ->  ဝို ==> ကို
   2:  266  ->  ကို ==> ဝို
   3:  245  ->  မင်း ==> နင်
   4:  128  ->  ငါ ==> ကျွန်တော်
   5:  109  ->  သူ ==> ဒယ်ကောင်မငယ်
   6:  100  ->  မင့် ==> နင်
   7:   97  ->  ခင်ဗျား ==> နင်
   8:   90  ->  ကျွန်တော် ==> ငါ
   9:   82  ->  နင် ==> မင်း
  10:   59  ->  အဲ့အမ ==> ဒယ်ကောင်မငယ်
  11:   54  ->  ဝို့ ==> ဖို့
  12:   54  ->  သော ==> သွား
  13:   53  ->  ဘယ်သူ့ ==> ဖယ်သူ့
  14:   53  ->  လဲ ==> ရိ
  15:   53  ->  ဝယ် ==> ရယ်
  16:   52  ->  နင့် ==> မင်း
  17:   47  ->  ဒယ်ကောင်မငယ် ==> သူ
  18:   45  ->  ဖို့ ==> ဝို့
  19:   45  ->  မင်း ==> နင့်
  20:   43  ->  ခင်ဗျား ==> မင်း
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$ head -51 ./triangulation.all.id.dtl 
DETAILED OVERALL REPORT FOR THE SYSTEM: ./triangulation.all.id

SENTENCE RECOGNITION PERFORMANCE

 sentences                                        10720
 with errors                             89.3%   (9573)

   with substitions                      88.0%   (9430)
   with deletions                        26.9%   (2887)
   with insertions                       28.5%   (3058)


WORD RECOGNITION PERFORMANCE

Percent Total Error       =   47.3%   (33300)

Percent Correct           =   59.6%   (41964)

Percent Substitution      =   34.4%   (24236)
Percent Deletions         =    6.0%   (4234)
Percent Insertions        =    6.9%   (4830)
Percent Word Accuracy     =   52.7%


Ref. words                =           (70434)
Hyp. words                =           (71030)
Aligned words             =           (75264)

CONFUSION PAIRS                  Total                 (16334)
                                 With >=  1 occurrences (16334)

   1:  325  ->  ဝို ==> ကို
   2:  250  ->  မင်း ==> နင်
   3:  224  ->  ကို ==> ဝို
   4:  109  ->  ငါ ==> ကျွန်တော်
   5:  106  ->  ခင်ဗျား ==> နင်
   6:  104  ->  ကျွန်တော် ==> ငါ
   7:  103  ->  မင့် ==> နင်
   8:  100  ->  သူ ==> ဒယ်ကောင်မငယ်
   9:   68  ->  ဒယ်ကောင်မငယ် ==> သူ
  10:   66  ->  ဘယ်သူ့ ==> ဖယ်သူ့
  11:   61  ->  မင်း ==> နင့်
  12:   57  ->  အဲ့အမ ==> ဒယ်ကောင်မငယ်
  13:   55  ->  နင် ==> မင်း
  14:   52  ->  ဝယ် ==> ရယ်
  15:   50  ->  နင့် ==> မင်း
  16:   50  ->  လဲ ==> ရိ
  17:   50  ->  သော ==> သွား
  18:   49  ->  ဝို့ ==> ဖို့
  19:   46  ->  ဖို့ ==> ဝို့
  20:   42  ->  ဟုတ်ဝ ==> ဝ
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/wer-calc/data4eval-pivot-10fold/rk-my-bk$
```
