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

Syllable Breaking ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./train.my -s " " > train.syl
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./dev.my -s " " > dev.syl
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./sylbreak.pl -i ./test.my -s " " > test.syl
```

confirmed with wc command ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ wc *.syl
   1031   13394  141200 dev.syl
   1000   13473  141923 test.syl
  19994  263503 2790412 train.syl
  22025  290370 3073535 total
```

no. of words should be bigger than word segmented files ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ wc *.my
   1031    9573  119279 dev.my
   1000    9579  119884 test.my
  19994  187544 2359638 train.my
  22025  206696 2598801 total
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

check the file content ... it looks OK ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 5 *.syl
==> dev.syl <==
 ဒိုင် ဗင်   ထိုး   တဲ့   စင်   ၊   ဒိုင် ဗင် ဘုတ်   နဲ့   လမ်း   တွေ   မ   ရှိ   ဘူး   ။
 ၅ ၀   ဘတ်   ကို   အ ကြွေ   လဲ   ပေး   မ လား   ။
 အ မျိုး သား ပြ တိုက်   ကို   ဘယ် လို   သွား   ရ   မ လဲ   ။
 ဒီ   နေ ရာ   က   ပြိုင် ဘက် ကင်း   ပဲ   ။
 တ ခြား   အ ခန်း   တွေ‌   ရော   ရ   နိုင်   မ လား   ။

==> test.syl <==
 ကျ သင့် ငွေ   ဘယ် လောက်   လဲ   ။
 ကျွန် တော်   လက် ဆောင်   အ နေ   နဲ့   ပေး   လို့   ရ   တဲ့   ပစ္စည်း   မျိုး   ကြည့်   ချင်   လို့   ။
 ရ ထား   က   ကြာ   နေ   တာ   လား   ။
 တံ ခါး   နောက်   မှာ   ရပ်   ပါ   ။
 ခ ဏ   လောက်   ။

==> train.syl <==
 ဟုတ် ကဲ့   ၊   ကျွန် တော်   ထိုင်း   စစ် တု ရင်   က စား   ရ   တာ   ကြိုက်   တယ်   ။
 က လေး များ   အ တွက်   တစ်   ခု   ခု   အ ကြံ ပြု   ပေး   နိုင်   မ လား   ။
 အဲ ဒီ   ကို   ဘယ် လို   ရောက်   နိုင်   မ လဲ   ။
 တစ် ကိုယ် လုံး   ကိုက် ခဲ   နေ   လို့   ။
 ကျွန် တော်   တို့   အ တွက်   လုပ်   ပေး   ခဲ့   တာ   တွေ   ကျေး ဇူး တင်   ပါ   တယ်   ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

## Cleaning Spaces

Current sylbreak program is just showing the concept of syllable breaking with regular expression and you need to make space cleaning ...    

changed file names of word segmented training, dev and test files:  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv train.my train.word
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv dev.my dev.word
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ mv test.my test.word
```

run space cleaning perl script ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./train.syl > train.my
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./dev.syl > dev.my
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ perl ./clean-space.pl ./test.syl > test.my
```

Check the cleaned files...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ head -n 5 {train,dev,test}.my
==> train.my <==
ဟုတ် ကဲ့ ၊ ကျွန် တော် ထိုင်း စစ် တု ရင် က စား ရ တာ ကြိုက် တယ် ။
က လေး များ အ တွက် တစ် ခု ခု အ ကြံ ပြု ပေး နိုင် မ လား ။
အဲ ဒီ ကို ဘယ် လို ရောက် နိုင် မ လဲ ။
တစ် ကိုယ် လုံး ကိုက် ခဲ နေ လို့ ။
ကျွန် တော် တို့ အ တွက် လုပ် ပေး ခဲ့ တာ တွေ ကျေး ဇူး တင် ပါ တယ် ။

==> dev.my <==
ဒိုင် ဗင် ထိုး တဲ့ စင် ၊ ဒိုင် ဗင် ဘုတ် နဲ့ လမ်း တွေ မ ရှိ ဘူး ။
၅ ၀ ဘတ် ကို အ ကြွေ လဲ ပေး မ လား ။
အ မျိုး သား ပြ တိုက် ကို ဘယ် လို သွား ရ မ လဲ ။
ဒီ နေ ရာ က ပြိုင် ဘက် ကင်း ပဲ ။
တ ခြား အ ခန်း တွေ‌ ရော ရ နိုင် မ လား ။

==> test.my <==
ကျ သင့် ငွေ ဘယ် လောက် လဲ ။
ကျွန် တော် လက် ဆောင် အ နေ နဲ့ ပေး လို့ ရ တဲ့ ပစ္စည်း မျိုး ကြည့် ချင် လို့ ။
ရ ထား က ကြာ နေ တာ လား ။
တံ ခါး နောက် မှာ ရပ် ပါ ။
ခ ဏ လောက် ။
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$
```

copied syllable breaked Myanmar files to the path data/  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ cp *.my ../
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data/mk-syl$ cd ..
```

make confirmation ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$ wc *.my
   1031   13394  123100 dev.my
   1000   13473  123778 test.my
  19994  263503 2435597 train.my
  22025  290370 2682475 total
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$
```

confirmation the no. of sentences with Thai corpus also ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl/data$ wc *.th
   1031    6809   98543 dev.th
   1000    7169   99326 test.th
  19994  139767 1951021 train.th
  22025  153745 2148890 total
```

## Prepare Configuration Files for Syllable Unit Experiments 

Generally same configuration files with word unit experiments, I just added "syl" to the name of the experiments ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$ head -3 config.*
==> config.baseline.my-th-syl.yaml <==
# standard settings
asean.baseline.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.nodropout.my-th-syl.yaml <==
# standard settings
asean.baseline.nodropout.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.nodropout.th-my-syl.yaml <==
# standard settings
asean.baseline.nodropout.syl.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.baseline.th-my-syl.yaml <==
# standard settings
asean.baseline.syl.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.my-th-syl.yaml <==
# standard settings
switchout.asean.syl.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.nodropout.my-th-syl.yaml <==
# standard settings
switchout.nodropout.syl.asean.my-th: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.nodropout.th-my-syl.yaml <==
# standard settings
switchout.nodropout.syl.asean.th-my: !Experiment
  exp_global: !ExpGlobal

==> config.switchout.th-my-syl.yaml <==
# standard settings
switchout.asean.syl.th-my: !Experiment
  exp_global: !ExpGlobal
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-myth-syl$
```

## Training Baseline, Syllable with Dropout  

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

