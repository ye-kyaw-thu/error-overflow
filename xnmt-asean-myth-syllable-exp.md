# ASEAN-MT Domain My-Th, Th-My, SwitchOut Experiment with Syllable Unit

## Syllable Breaking

I already downloaded sylbreak.pl and clean-space.pl tools ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ ls
clean-space.pl  dev.my  print-blank-lines.pl  sylbreak.pl  test.my  train.my
```

Currently, word segmented Myanmar data:  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 3 *.my
==> dev.my <==
ဒိုင်ဗင် ထိုး တဲ့ စင် ၊ ဒိုင်ဗင်ဘုတ် နဲ့ လမ်း တွေ မ ရှိ ဘူး ။
၅၀ ဘတ် ကို အကြွေ လဲ ပေး မလား ။
အမျိုးသားပြတိုက် ကို ဘယ်လို သွား ရ မလဲ ။

==> test.my <==
ကျသင့်ငွေ ဘယ်လောက် လဲ ။
ကျွန်တော် လက်ဆောင် အနေ နဲ့ ပေး လို့ ရ တဲ့ ပစ္စည်း မျိုး ကြည့် ချင် လို့ ။
ရထား က ကြာ နေ တာ လား ။

==> train.my <==
ဟုတ်ကဲ့ ၊ ကျွန်တော် ထိုင်း စစ်တုရင် ကစား ရ တာ ကြိုက် တယ် ။
ကလေးများ အတွက် တစ် ခု ခု အကြံပြု ပေး နိုင် မလား ။
အဲဒီ ကို ဘယ်လို ရောက် နိုင် မလဲ ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

