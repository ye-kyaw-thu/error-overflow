# SwitchOut Experiment with ASEAN-MT Domain

## Data Preparation

ဒီဒေတာက ဇာဇာလှိုင် (KMITL) နဲ့ အတူလုပ်ခဲ့တဲ့ သူ့ပထမဂျာနယ် experiment အတွက် သုံးခဲ့ဒေတာထဲက (i.e. /home/ye/data/zzh/plan-to-use-for-switchout/1_TH-to-EN_Models_Reports/1_Transformer_Models_Reports/) ကနေ ယူထားတာ။  
ဆိုလိုတာက အဲဒီတုန်းက ခွဲထားခဲ့တဲ့ train, valid, test ပမာဏအတိုင်းပဲ ယူသုံးထားတာ။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ wc *
   1000    7176   37600 test.en
   1000    7169   99326 test.th
  20000  141098  737287 train.en
  20000  139767 1951027 train.th
   1031    7245   37663 valid.en
   1031    6809   98543 valid.th
  44062  309264 2961446 total

```

လက်ရှိ xnmt အတွက် သုံးထားတဲ့ config ဖိုင်တွေမှာ dev လို့ သုံးခဲ့တာကြောင့် ပြန်ပြင်ရမှာကို ပျင်းလို့၊ ပြင်ရင်းနဲ့ အမှားမဖြစ်အောင်လို့ valid ကိုပဲ dev အဖြစ် နာမည်ပြောင်းသိမ်းခဲ့တယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mv valid.en dev.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt/data$ mv valid.th dev.th
```



