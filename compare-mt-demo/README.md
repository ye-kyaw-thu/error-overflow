# compare-mt Running Demo

compare-mt ကို သုံးပြီးတော့ machine translation system နှစ်ခုအကြား significantly difference ဖြစ်မဖြစ်ကို တိုင်းတာပြထားတာပါ။ 
ဗမာစာ အပါအဝင် တိုင်းရင်းသား ဘာသာစကားတွေအကြား ကွန်ပျူတာကိုသုံးပြီး အော်တိုဘာသာပြန်နိုင်အောင် Statistical Machine Translation, Neural Machine Translation စတဲ့ experiment တွေကို အများကြီး လုပ်ခဲ့ပါတယ်။ Researcher အနေနဲ့ ဒီနေရာမှာ အရေးကြီးတဲ့မေးခွန်းတစ်ခုက system နှစ်ခုအကြားမှာ ဘယ် machine translation system or approach က ပိုသာတာလဲ၊ ပိုကောင်းတာလဲ ဆိုတဲ့ မေးခွန်းပါ။  

လက်တွေ့မှာက parallel corpus ဒေတာကလည်း အထူးသဖြင့် ဗမာစာနဲ့ တိုင်းရင်းသား ဘာသာစကားတွေအတွက်ဆိုရင် ဒေတာက မရှိလို့ ကိုယ်ဖာသာကိုယ်ဆောက်ရတာနဲ့ Test-set တစ်ခုကိုပဲသုံးပြီး evaluation လုပ်ကြရပါတယ်။  

အဲဒါကြောင့် ဘယ် approach က သာတယ်ဆိုတာကို prove လုပ်ဖို့ ဆိုရင် လုပ်လို့ ရတဲ့ နည်းလမ်းတစ်ခုက statistical test လုပ်တာ တနည်းအားဖြင့် bootstrap resampling method လုပ်တာပါ။ 
အဲဒီလို လုပ်ရင် test-data က နည်းရင်တောင် system နှစ်ခုအကြားမှာ ဘယ် system က ပိုသာတယ်ဆိုတာကို confidence ရှိရှိနဲ့ evaluation လုပ်လို့ ရပါတယ်။ 
အဲဒီလို လုပ်ဖို့အတွက် ဆိုရင် moses (SMT tool) မှာဆိုရင် bootstrap-hypothesis-difference-significance.pl ဆိုတဲ့ perl program ရှိပါတယ်။ 
ဒီနေရာမှာတော့ ပိုပြီးတော့ visualize လုပ်ပေးတဲ့ compare-mt ကို သုံးပြီး လုပ်ပြထားပါတယ်။ ယူသုံးထားတဲ့ experiment က ဒေါက်တာတန်း ကျောင်းသူ သဇင်မြင့်ဦး နဲ့အတူလေ့လာနေတဲ့ Pivot Machine Translation ကပါ။
အဓိက အသစ်လုပ်ကြည့်ခဲ့တဲ့ approach က နှစ်မျိုးပါ Transfer Pivot နဲ့ Triangulation Pivot ပါ။ 
Run ထားတာတွေ အများကြီးထဲကနေ Beik-Burmese-Rakhine (baseline vs triangulation) နဲ့ Beik-Burmese-Rakhine (Transfer vs Triangulation) အတွက် compare-mt ကို run ထားတဲ့ ရလဒ်တွေကို folder အလိုက် တင်ပေးထားပါတယ်။ 
ဂျာနယ်စာတမ်း publish လုပ်ပြီးသွားရင် ဒီနေရာမှာလည်း အဲဒီ စာတမ်းရဲ့ link ကို ဖြည့်ပေးထားပါမယ်။  

1 Jan 2022  
y@Lab  


## Bootstrap Resampling Results with compare-mt

[compare-mt-demo/](https://github.com/ye-kyaw-thu/error-overflow/tree/master/compare-mt-demo) ဖိုလ်ဒါအောက်မှာ html report နှစ်ခုရဲ့ ဖိုလ်ဒါတွေကို upload လုပ်ပေးထားပါတယ်။ ပထမ ဖိုလ်ဒါက ဘိတ်ကနေ ရခိုင်ဘာသာကို SMT လုပ်တာကို pivot language အနေနဲ့ ဗမာစာကို ထားထားပြီး လုပ်ခဲ့တဲ့ Triangulation-Pivot experiment ပါ။ ဒီနေရာမှာ baseline (i.e. normal PBSMT translation) ထက် Triangulation-Pivot experiment ရဲ့ ရလဒ်တွေက statistically significance (p <= 0.05) ဖြစ်တယ်ဆိုတာကို လေ့လာနိုင်ပါတယ်။   

1. [Bootstrap Resampling for Baseline-vs-Triangulation, Beik-Myanmar-Rakhine](https://htmlpreview.github.io/?https://github.com/ye-kyaw-thu/error-overflow/blob/master/compare-mt-demo/bk-my-rk-baseline-vs-triangulation/index.html)  

Transfer-Pivot နဲ့ Triangulation-Pivot နည်းလမ်းနှစ်ခုအကြား bootstrap resampling လုပ်ထားတာကိုလည်း အောက်ပါ လင့်ကနေလေ့လာနိုင်ပါတယ်။ ဒီနေရာမှာ Triangulation-Pivot က Transfer-Pivot က statistically significance ဖြစ်တယ်ဆိုတာကို တွေ့ကြရပါလိမ့်မယ်။  

2. [Beik-Burmese-Rakhine (Transfer vs Triangulation)](https://htmlpreview.github.io/?https://github.com/ye-kyaw-thu/error-overflow/blob/master/compare-mt-demo/bk-my-rk-transfer-vs-triangulation/index.html)  

## Reference

1. [https://en.wikipedia.org/wiki/P-value](https://en.wikipedia.org/wiki/P-value)
2. [https://en.wikipedia.org/wiki/Statistical_significance](https://en.wikipedia.org/wiki/Statistical_significance)
3. Koehn, Philipp. “Statistical Significance Tests for Machine Translation Evaluation.” EMNLP (2004). [Paper](https://aclanthology.org/W04-3250.pdf) 

