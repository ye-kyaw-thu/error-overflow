# Experiment Log for Mu Haung Braille Translation

မျက်မမြင်စာ မူဟောင်း ဒေတာက ပြင်ဆင်တာ ပြီးသွားလို့ NMT လုပ်ကြည့်ခဲ့တဲ့ Experiment log ပါ။  

## Information of Mu Haung Data

NMT အတွက် experiment မလုပ်ခင်မှာ သီတာစန်းနဲ့ ဇွန်လှိုင်မိုး (Ph.D. Candidates at UTYCC) တို့က SMT ကို 10-fold cross validation run ထားခဲ့ကြတာမို့ အဲဒီ ၁၀ပိုင်း ပိုင်းထားတဲ့ ဒေတာတွေနဲ့ ပတ်သက်ပြီး အရင် ကြည့်ခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/10fold-SMT-WER-result$ for i in {0..9};do cd $i; wc train$i dev$i test$i; cd ..; echo "====="; done;
  16415  440314 5098799 train0
   2897   78288  908019 dev0
   2167   57606  667895 test0
  21479  576208 6674713 total
=====
  16416  440406 5099357 train1
   2897   78288  908019 dev1
   2166   57514  667337 test1
  21479  576208 6674713 total
=====
  16456  439998 5096459 train2
   2905   78688  911013 dev2
   2118   57522  667241 test2
  21479  576208 6674713 total
=====
  16389  440066 5100164 train3
   2893   78196  907133 dev3
   2197   57946  667416 test3
  21479  576208 6674713 total
=====
  16436  439890 5098371 train4
   2901   78352  908620 dev4
   2142   57966  667722 test4
  21479  576208 6674713 total
=====
  16438  440668 5098722 train5
   2901   78352  908620 dev5
   2140   57188  667371 test5
  21479  576208 6674713 total
=====
  16477  440222 5095299 train6
   2908   78602  911458 dev6
   2094   57384  667956 test6
  21479  576208 6674713 total
=====
  16391  440088 5100558 train7
   2893   78196  907133 dev7
   2195   57924  667022 test7
  21479  576208 6674713 total
=====
  16449  440118 5097032 train8
   2903   78418  909412 dev8
   2127   57672  668269 test8
  21479  576208 6674713 total
=====
  16444  439710 5092929 train9
   2902   79012  915300 dev9
   2133   57486  666484 test9
  21479  576208 6674713 total
=====
(base) ye@:/media/ye/project2/exp/braille-nmt/data/10fold-SMT-WER-result$
```

## Preparation for NMT Running

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/10fold-SMT-WER-result/0$ head test0
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။	⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။	⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။	⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
၂ ။ ဒေါက်တို က ညီနောင် လေး ဦး ကို ဘယ်လို ပြော သလဲ ။	⠼⠃ ⠲ ⠙⠴⠞⠕ ⠅⠣ ⠷⠪⠝⠶ ⠇⠱⠆ ⠥⠆ ⠅ ⠃⠮⠇⠕ ⠿⠻⠆ ⠹⠸ ⠲
ထို့ပြင် ကျောက်စာ ကူးသူ ၊ စာပုံနှိပ်တိုက် စာရေး ၊ သတင်းစာတိုက် စာရေး စသည် ဖြင့် လည်း ဘဝ မျိုးစုံ ကျင်လည် ဖူး သည် ။	⠼⠂⠿⠔ ⠟⠴⠎⠁ ⠅⠥⠆⠹⠥ ⠒ ⠎⠁⠏⠉⠠⠣⠱⠅⠞⠬ ⠎⠁⠗⠱⠆ ⠒ ⠹⠣⠞⠔⠆⠎⠁⠞⠬ ⠎⠁⠗⠱⠆ ⠎⠣⠹ ⠿⠓ ⠇⠆ ⠃⠣⠺⠣ ⠾⠕⠆⠎⠉ ⠟⠔⠇⠮ ⠘⠥⠆ ⠹ ⠲
ဤသို့ဖြင့် မီးရထား သည် ဘူတာရုံ အနီး ကို ချဉ်းကပ် လာ လေ သည် ။	⠪⠙⠿⠓ ⠍⠪⠆⠗⠣⠞⠓⠁⠆ ⠹ ⠃⠥⠞⠁⠗⠉ ⠣⠝⠪⠆ ⠅ ⠡⠔⠆⠅⠣⠞ ⠇⠁ ⠃ ⠹ ⠲
ပြိုက် ရှိုက် ။	⠿⠬ ⠩⠬ ⠲
၁ ၄ ။ ကျီစား = ကစား သည် ။ ပြက်ရယ် ပြု သည် ။	⠼⠁ ⠙ ⠲ ⠟⠪⠎⠁⠆ ⠰⠶ ⠅⠣⠎⠁⠆ ⠹ ⠲ ⠿⠑⠗⠮ ⠿⠥⠂ ⠹ ⠲
၁ ။ ချိုင့်ဝှမ်း = မြေ မြင့် နှစ် ခု အကြား ရှိ နက်ရှိုင်း သော အရပ် ။	⠼⠁ ⠲ ⠡⠖⠂⠜⠋⠆ ⠰⠶ ⠾⠱ ⠾⠔⠂ ⠠⠣⠭ ⠨⠥⠂ ⠣⠟⠁⠆ ⠩ ⠝⠑⠩⠖⠆ ⠹⠻⠆ ⠣⠗⠣⠞ ⠲
အောက်ပါ စကားလုံးများ ၏ စာလုံးပေါင်း သတ်ပုံ ကို လေ့ကျင့် ပါ ။	⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠊ ⠎⠁⠇⠉⠆⠏⠶⠆ ⠹⠣⠞⠏⠉ ⠅ ⠇⠱⠂⠟⠔⠂ ⠏ ⠲
(base) ye@:/media/ye/project2/exp/braille-nmt/data/10fold-SMT-WER-result/0$
```

အရင်ဆုံး original ဒေတာကို folder အသစ် ဆောက်ပြီး ကော်ပီကူးခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/0/*0 ./0/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 1
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/1/*1 ./1/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 2
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/2/*2 ./2/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 3
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/3/*3 ./3/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 4
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/4/*4 ./4/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 5
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/5/*5 ./5/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 6
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/6/*6 ./6/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 7
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/7/*7 ./7/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 8
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/8/*8 ./8/
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ mkdir 9
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cp ../10fold-SMT-WER-result/9/*9 ./9/
```

source, target တစ်စုံစီ ဖြစ်အောင် ခွဲ...  
shell script တစ်ပုဒ် ရေးခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cat ./split-src-trg.sh 
#!/bin/bash

for i in {0..9};
do
  cd $i;
  pwd;
  cut -f1 train$i > train.my;
  cut -f2 train$i > train.br;
  
  cut -f1 dev$i > dev.my;
  cut -f2 dev$i > dev.br;

  cut -f1 test$i > test.my;
  cut -f2 test$i > test.br;
  
  head -n 3 *.my;
  head -n 3 *.br;
  echo "==========";
  
  cd ..;
done
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$
```

shell ကို run ခဲ့...  
```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ ./split-src-trg.sh 
/media/ye/project2/exp/braille-nmt/data/for-nmt/0
==> dev.my <==
၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
( ခ ) ယုန် နှင့် လိပ် ။
ဂျပန် နိုင်ငံ ပညာ ( Kyoiku ) ထုတ်ဝေရေး ။

==> test.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။

==> train.my <==
၄ ။ အောက်ပါ မေးခွန်းများ ကို ဖြေဆို ပါ ။
အဲဒီ မှာ ကိုရွှေ ဗျည်း တို့ မသရ တို့ ရှိ ကြ တယ် လေ ။
စစ် မှာ ယွန်းမ ။
==> dev.br <==
⠼⠊ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
⠶ ⠨⠣ ⠶ ⠽⠉ ⠗ ⠇⠱⠅ ⠲
⠚⠣⠏⠋ ⠝⠌ ⠏⠔⠷⠁ ⠶ ⠠⠅⠽⠕⠊⠅⠥ ⠶ ⠁⠦⠺⠱⠗⠱⠆ ⠲

==> test.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲

==> train.br <==
⠼⠙ ⠲ ⠴⠏ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠅ ⠿⠓⠱⠈⠕ ⠏ ⠲
⠮⠆⠙⠪ ⠰⠣⠁ ⠅⠕⠩⠺⠱ ⠃⠽⠪⠆ ⠚ ⠍⠣⠹⠣⠗⠣ ⠚ ⠩ ⠟ ⠞⠮ ⠇⠱ ⠲
⠎⠭ ⠰⠣⠁ ⠽⠥⠝⠆⠍⠣ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/1
==> dev.my <==
၉ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
( ခ ) ယုန် နှင့် လိပ် ။
ဂျပန် နိုင်ငံ ပညာ ( Kyoiku ) ထုတ်ဝေရေး ။

==> test.my <==
အနော်ရထာမင်းမြတ် သည် ရှင်အရဟံ ၏ ဩဝါဒ ဖြင့် ဗုဒ္ဓသာသနာ ထွန်းကား အောင် စွမ်းဆောင် ခဲ့ ပါ သည် ။
အားလုံး သော ညီနောင် တို့ ကလည်း သဘောတူ ကြ လေ ၏ ။
မျက်စိ ---- လာပြီ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠼⠊ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
⠶ ⠨⠣ ⠶ ⠽⠉ ⠗ ⠇⠱⠅ ⠲
⠚⠣⠏⠋ ⠝⠌ ⠏⠔⠷⠁ ⠶ ⠠⠅⠽⠕⠊⠅⠥ ⠶ ⠁⠦⠺⠱⠗⠱⠆ ⠲

==> test.br <==
⠣⠝⠻⠗⠣⠞⠓⠁⠍⠌⠄⠆⠾⠣⠞ ⠹ ⠩⠔⠣⠗⠣⠓⠋ ⠊ ⠻⠆⠺⠁⠙⠣ ⠿⠓ ⠃⠦⠙⠣⠹⠁⠹⠣⠝⠁ ⠁⠥⠝⠆⠅⠁⠆ ⠶ ⠎⠺⠋⠆⠈⠶ ⠨⠮⠂ ⠏ ⠹ ⠲
⠁⠆⠇⠉⠆ ⠹⠻⠆ ⠷⠪⠝⠶ ⠚ ⠅⠣⠇⠆ ⠹⠣⠃⠻⠆⠞⠥ ⠟ ⠃ ⠊ ⠲
⠾⠑⠎⠊ ⠤⠤⠤⠤ ⠇⠁⠿⠪ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/2
==> dev.my <==
ဣန္ဒြေ ကြီး နှင့် ။
အမည်ရင်း မှာ ဦးဝန် ဖြစ် သည် ။
၁ ၁ ။ အဝီစိ = ငရဲကြီး ရှစ် ထပ် တွင် အောက်ဆုံး ထပ် ငရဲ ။

==> test.my <==
ရေသည် အရပ်သား တင် ။
နောက်ဆုံး တွင် အိမ်ရှေ့ မင်း အရာ ပေး ရာ အိမ်ရှေ့ မင်း အရာ လည်း လက်ခံ မည် ။
တံငါသည် လည်း အရှင် မင်းကြီး ကျွန်တော် မျိုး သည် ဤ ငါး ဖိုး အဖြစ် ရွှေ ငွေ ဥစ္စာ ကျေးရွာ တို့ ကို မ လို ပါ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠢⠙⠣⠗⠱ ⠟⠪⠆ ⠗ ⠲
⠣⠾⠪⠗⠔⠆ ⠰⠣⠁ ⠥⠆⠺⠥⠝ ⠭ ⠹ ⠲
⠼⠁ ⠁ ⠲ ⠣⠺⠪⠎⠊ ⠰⠶ ⠌⠣⠗⠮⠆⠟⠪⠆ ⠩⠭ ⠁⠣⠞ ⠞⠺ ⠴⠈⠉⠆ ⠁⠣⠞ ⠌⠣⠗⠮⠆ ⠲

==> test.br <==
⠗⠱⠹⠮ ⠣⠗⠣⠞⠹⠁⠆ ⠞⠔ ⠲
⠝⠴⠈⠉⠆ ⠞⠺ ⠱⠝⠩⠱⠂ ⠍⠔⠆ ⠣⠽ ⠏⠱⠆ ⠗⠁ ⠱⠝⠩⠱⠂ ⠍⠔⠆ ⠣⠽ ⠇⠆ ⠇⠑⠨⠋ ⠍ ⠲
⠞⠋⠌⠁⠹⠮ ⠇⠆ ⠣⠩ ⠍⠔⠆⠟⠪⠆ ⠟⠞ ⠾⠕⠆ ⠹ ⠪ ⠌⠁⠆ ⠘⠕⠆ ⠣⠭ ⠩⠺⠱ ⠌⠺⠱ ⠦⠎⠁ ⠟⠱⠆⠗⠺⠁ ⠚ ⠅ ⠋ ⠇⠕ ⠏ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/3
==> dev.my <==
ဒါပေမယ့် အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
( ခ ) စိတ် ခံစားချက် စကားလုံး တွေ ကို ရေး ကြည့် ကြ ရအောင် ။

==> test.my <==
၄ ။ အောက်ပါ မေးခွန်းများ ကို ဖြေဆို ပါ ။
အဲဒီ မှာ ကိုရွှေ ဗျည်း တို့ မသရ တို့ ရှိ ကြ တယ် လေ ။
စစ် မှာ ယွန်းမ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠙⠁⠏⠱⠍⠮⠂ ⠔⠛⠣⠇⠱⠅ ⠭⠭ ⠒ ⠚⠣⠏⠋ ⠭⠭ ⠒ ⠃⠮ ⠝⠌⠡⠹⠁⠆ ⠏⠮⠆ ⠭⠭ ⠟⠞⠚ ⠞⠖⠆⠿⠪ ⠅ ⠹⠨ ⠇⠦ ⠿⠪⠆ ⠇⠁ ⠕⠅⠡⠦ ⠱ ⠞⠁ ⠅ ⠞⠻⠂ ⠣⠇⠕ ⠋ ⠩ ⠃⠥⠆ ⠇⠕⠂ ⠽⠔⠽⠔⠟⠱⠆⠟⠱⠆ ⠿⠋ ⠿⠻⠆ ⠇⠬ ⠹⠣ ⠞⠮⠂ ⠲
⠇⠱⠿⠔⠆⠍⠉⠞⠖⠆ ⠒ ⠹⠉⠆⠈⠶ ⠒ ⠡⠪⠆⠍⠺⠋⠆ ⠒ ⠱⠆⠾⠣ ⠒ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠲
⠶ ⠨⠣ ⠶ ⠎⠱⠅ ⠨⠋⠎⠁⠆⠡⠑ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠞⠺⠱ ⠅ ⠗⠱⠆ ⠟⠪⠂ ⠟ ⠗⠣⠶ ⠲

==> test.br <==
⠼⠙ ⠲ ⠴⠏ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠅ ⠿⠓⠱⠈⠕ ⠏ ⠲
⠮⠆⠙⠪ ⠰⠣⠁ ⠅⠕⠩⠺⠱ ⠃⠽⠪⠆ ⠚ ⠍⠣⠹⠣⠗⠣ ⠚ ⠩ ⠟ ⠞⠮ ⠇⠱ ⠲
⠎⠭ ⠰⠣⠁ ⠽⠥⠝⠆⠍⠣ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/4
==> dev.my <==
ပါနီ လည်း လာ တယ် ရှိ တယ် ။
၂ ။ ဆက်စပ် = တစ် ခု နှင့် တစ် ခု ပူးပေါင်း သည် ။ ဆက်နွယ် သည် ။
ဂျင် ပဲ့ ချင်း ပေါက် ကြစို့ ။

==> test.my <==
မောင်ဖြူး ။
ယခုခေတ် သမယ တိုးတက် သော နည်း တို့ဖြင့် ပစ္စည်းများ ကို လုပ်ကိုင် ရောင်းချသူများ သည် အချိန် ကို မလစ်ဟင်း စေ ရအောင် အမြန်ဆုံး သော နည်းများ ကို အသုံးပြု ကြ ရ ၏ ။
ရန်ကုန် ကောလိပ် တွင် ပညာ သင်ယူ နေ ဆဲ ပထမ ကျောင်းသား သပိတ် အရေးတော်ပုံ ကြီး ပေါ်ပေါက် လာ ရာ ၁ ၉ ၂ ၃ ခုနှစ် အထိ အမျိုးသား ကျောင်းဆရာ အဖြစ် တာဝန် ထမ်းခဲ့ သည် ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠏⠁⠝⠪ ⠇⠆ ⠇⠁ ⠞⠮ ⠩ ⠞⠮ ⠲
⠼⠃ ⠲ ⠈⠑⠎⠣⠞ ⠰⠶ ⠞⠭ ⠨⠥⠂ ⠗ ⠞⠭ ⠨⠥⠂ ⠏⠥⠆⠏⠶⠆ ⠹ ⠲ ⠈⠑⠝⠺⠮ ⠹ ⠲
⠚⠔ ⠏⠮⠂ ⠡⠔⠆ ⠏⠴ ⠟⠣⠎⠕⠂ ⠲

==> test.br <==
⠍⠶⠿⠓⠥⠆ ⠲
⠽⠨⠨⠭ ⠹⠣⠍⠣⠽⠣ ⠞⠕⠆⠞⠑ ⠹⠻⠆ ⠝⠪⠆ ⠚⠿⠓ ⠏⠭⠎⠪⠆⠾ ⠅ ⠇⠦⠅⠖ ⠗⠶⠆⠡⠣⠹⠥⠾ ⠹ ⠣⠡⠢ ⠅ ⠍⠣⠇⠭⠓⠔⠆ ⠎ ⠗⠣⠶ ⠣⠾⠋⠈⠉⠆ ⠹⠻⠆ ⠝⠪⠆⠾ ⠅ ⠣⠹⠉⠆⠿⠥⠂ ⠟⠣ ⠗⠣ ⠊ ⠲
⠗⠋⠅⠉ ⠅⠻⠆⠇⠱⠅ ⠞⠺ ⠏⠔⠷⠁ ⠹⠔⠽⠥ ⠝⠱ ⠈⠮⠆ ⠏⠣⠁⠣⠍⠣ ⠟⠶⠆⠹⠁⠆ ⠹⠣⠏⠱⠅ ⠣⠗⠱⠆⠞⠏⠉ ⠟⠪⠆ ⠏⠻⠏⠴ ⠇⠁ ⠗⠁ ⠼⠁ ⠊ ⠃ ⠉ ⠨⠥⠂⠠⠣⠭ ⠣⠁⠊ ⠣⠾⠕⠆⠹⠁⠆ ⠟⠶⠆⠈⠣⠗⠁ ⠣⠭ ⠞⠁⠺⠥⠝ ⠁⠋⠆⠨⠮⠂ ⠹ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/5
==> dev.my <==
ပါနီ လည်း လာ တယ် ရှိ တယ် ။
၂ ။ ဆက်စပ် = တစ် ခု နှင့် တစ် ခု ပူးပေါင်း သည် ။ ဆက်နွယ် သည် ။
ဂျင် ပဲ့ ချင်း ပေါက် ကြစို့ ။

==> test.my <==
၃ ၅ ။ စည်းပုံ = အမျိုးသမီးများ ဦးခေါင်း ၌ ဝတ်ဆင် ရသော အဆင်တန်ဆာ ။
နေရပ် ချောင် က ၊ လူမည် မောင်ဝ ဟု ကလောင် အမည်ခံ လိုက် ရာ က စ၍ မောင်ဝ အမည် တွင် ခဲ့ သည် ။
၂ ။ ဓာတ်သိ = အခြေအနေ ၊ စိတ်သဘော ကို သိ ပြီး သူ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠏⠁⠝⠪ ⠇⠆ ⠇⠁ ⠞⠮ ⠩ ⠞⠮ ⠲
⠼⠃ ⠲ ⠈⠑⠎⠣⠞ ⠰⠶ ⠞⠭ ⠨⠥⠂ ⠗ ⠞⠭ ⠨⠥⠂ ⠏⠥⠆⠏⠶⠆ ⠹ ⠲ ⠈⠑⠝⠺⠮ ⠹ ⠲
⠚⠔ ⠏⠮⠂ ⠡⠔⠆ ⠏⠴ ⠟⠣⠎⠕⠂ ⠲

==> test.br <==
⠼⠉ ⠑ ⠲ ⠎⠪⠆⠏⠉ ⠰⠶ ⠣⠾⠕⠆⠹⠣⠍⠪⠆⠾ ⠥⠆⠨⠶⠆ ⠫ ⠺⠥⠞⠈⠔ ⠗⠣⠹⠻⠆ ⠣⠈⠔⠞⠋⠎⠓⠁ ⠲
⠝⠱⠗⠣⠞ ⠡⠶ ⠅⠣ ⠒ ⠇⠥⠍ ⠍⠶⠺⠣ ⠓ ⠅⠣⠇⠶ ⠣⠍⠨⠋ ⠇⠬ ⠗⠁ ⠅⠣ ⠎⠣⠯ ⠍⠶⠺⠣ ⠣⠍ ⠞⠺ ⠨⠮⠂ ⠹ ⠲
⠼⠃ ⠲ ⠙⠣⠞⠹⠊ ⠰⠶ ⠣⠡⠱⠣⠝⠱ ⠒ ⠎⠱⠅⠹⠣⠃⠻⠆ ⠅ ⠹⠊ ⠿⠪⠆ ⠹⠥ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/6
==> dev.my <==
၁ ။ အောက်ပါ အချက်များ ပေါ် မူတည် ပြီး ဇယား တွင် ဖြည့် ပါ ။
တစ်နေ့ တွင် မင်းကြီး က အမောင် လုလင် ၊ ဤ အတတ်ပညာ ကို အဘယ် ဆရာ့ ထံ တွင် လေ့လာ ဆည်းပူး ခဲ့ သနည်း ။
ဦးဖိုးကျား သည် ဒုတိယ ကမ္ဘာစစ် အတွင်း စစ်ပြေး ရင်း မြန်မာ နှစ် ၁ ၃ ၀ ၃ ခု ( ခရစ် နှစ် ၁ ၉ ၄ ၂ ) တွင် ထန်းတပင် မြို့ ၌ ကွယ်လွန် သည် ။

==> test.my <==
သင်္ကြန် ကျ ရင် သိကြားမင်းကြီး လဲ လူ့ပြည် ဆင်း လာ သ တဲ့ ။
ဤသို့ ဦးရာကျော် သမီး ဇနီး တို့ သည် သား အတွက် နှင့် အားတက် သူ က တစ်ဖုံ ၊ ဝတ်လုံ ကြောင့် ငွေ ကုန်၍ ညည်းသူ က တစ်မျိုး ၊ အကျိုး နှင့် အကြောင်း အကောင်း နှင့် အဆိုး သည် နှစ်မျိုး တွင် ဆိုး မည် ကောင်း မည် ကြံစည် စိတ်ကူး၍ ပြောဆို ကြ ပြီးနောက် အိပ်ခန်း သို့ ဝင် ကြ လေ ၏ ။
ဖြည်းညင်း သာသာ ကျ လေ ပြီ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠼⠁ ⠲ ⠴⠏⠁ ⠣⠡⠑⠾ ⠏⠻ ⠍⠥⠞⠮ ⠿⠪⠆ ⠵⠣⠽⠁⠆ ⠞⠺ ⠿⠓⠱⠂ ⠏ ⠲
⠞⠭⠝⠱⠂ ⠞⠺ ⠍⠔⠆⠟⠪⠆ ⠅⠣ ⠣⠍⠶ ⠇⠥⠂⠇⠔ ⠒ ⠪ ⠣⠞⠣⠞⠏⠔⠷⠁ ⠅ ⠣⠃⠮ ⠈⠣⠗⠁⠂ ⠁⠋ ⠞⠺ ⠇⠱⠂⠇⠁ ⠈⠪⠆⠏⠥⠆ ⠨⠮⠂ ⠹⠝ ⠲
⠥⠆⠘⠕⠆⠟⠁⠆ ⠹ ⠙⠥⠂⠞⠊⠽⠣ ⠅⠋⠃⠁⠎⠭ ⠣⠞⠺⠔⠆ ⠎⠭⠿⠱⠆ ⠗⠔⠆ ⠾⠋⠍⠁ ⠠⠣⠭ ⠼⠁ ⠉ ⠚ ⠉ ⠨⠥⠂ ⠶ ⠅⠗ ⠠⠣⠭ ⠼⠁ ⠊ ⠙ ⠃ ⠶ ⠞⠺ ⠁⠋⠆⠞⠣⠏⠔ ⠾⠕⠂ ⠫ ⠅⠺⠮⠇⠥⠝ ⠹ ⠲

==> test.br <==
⠹⠔⠟⠋ ⠟⠣ ⠗⠔ ⠹⠊⠟⠁⠆⠍⠔⠆⠟⠪⠆ ⠇⠮⠆ ⠇⠥⠂⠿⠪ ⠈⠔⠆ ⠇⠁ ⠹⠣ ⠞⠮⠂ ⠲
⠪⠙ ⠥⠆⠗⠁⠟⠻ ⠹⠣⠍⠪⠆ ⠵⠣⠝⠪⠆ ⠚ ⠹ ⠹⠁⠆ ⠣⠞⠺⠑ ⠗ ⠁⠆⠞⠑ ⠹⠥ ⠅⠣ ⠞⠭⠘⠉ ⠒ ⠺⠥⠞⠇⠉ ⠳ ⠌⠺⠱ ⠅⠉⠯ ⠷⠪⠆⠹⠥ ⠅⠣ ⠞⠭⠾⠕⠆ ⠒ ⠣⠟⠕⠆ ⠗ ⠣⠟ ⠣⠅⠶⠆ ⠗ ⠣⠈⠕⠆ ⠹ ⠠⠣⠭⠾⠕⠆ ⠞⠺ ⠈⠕⠆ ⠍ ⠅⠶⠆ ⠍ ⠟⠋⠎⠪ ⠎⠱⠅⠅⠥⠆⠯ ⠿⠻⠆⠈⠕ ⠟⠣ ⠿⠪⠆⠝⠴ ⠱⠅⠨⠋⠆ ⠙ ⠺⠔ ⠟ ⠃ ⠊ ⠲
⠿⠓⠱⠆⠷⠔⠆ ⠹⠁⠹⠁ ⠟⠣ ⠃ ⠛ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/7
==> dev.my <==
ဒါပေမယ့် အင်္ဂလိပ် ဖြစ်ဖြစ် ၊ ဂျပန် ဖြစ်ဖြစ် ၊ ဘယ် နိုင်ငံခြားသား ပဲ ဖြစ်ဖြစ် ကျွန်တော်တို့ တိုင်းပြည် ကို သခင် လုပ် ပြီး လာ အုပ်ချုပ် နေ တာ ကို တော့ အလို မ ရှိ ဘူး လို့ ယဉ်ယဉ်ကျေးကျေး ပြန် ပြော လိုက် သ တဲ့ ။
လေပြင်းမုန်တိုင်း ၊ သုံးဆောင် ၊ ချီးမွမ်း ၊ အေးမြ ၊ နူးညံ့ သိမ်မွေ့ ။
( ခ ) စိတ် ခံစားချက် စကားလုံး တွေ ကို ရေး ကြည့် ကြ ရအောင် ။

==> test.my <==
၅ ။ အရုပ် ဆိုင် မှ မခွာ နိုင် အောင် အဘယ်ကြောင့် ဖြစ် နေ ရ ပါ သနည်း ။
၄ ။ လုလင် သည် သူ၏ ဆရာ မှာ ဗျိုင်း ဖြစ် ကြောင်း အဘယ်ကြောင့် မပြော လို သနည်း ။
အားကစား ပြိုင်ပွဲ ကျင်းပ သည် ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠙⠁⠏⠱⠍⠮⠂ ⠔⠛⠣⠇⠱⠅ ⠭⠭ ⠒ ⠚⠣⠏⠋ ⠭⠭ ⠒ ⠃⠮ ⠝⠌⠡⠹⠁⠆ ⠏⠮⠆ ⠭⠭ ⠟⠞⠚ ⠞⠖⠆⠿⠪ ⠅ ⠹⠨ ⠇⠦ ⠿⠪⠆ ⠇⠁ ⠕⠅⠡⠦ ⠱ ⠞⠁ ⠅ ⠞⠻⠂ ⠣⠇⠕ ⠋ ⠩ ⠃⠥⠆ ⠇⠕⠂ ⠽⠔⠽⠔⠟⠱⠆⠟⠱⠆ ⠿⠋ ⠿⠻⠆ ⠇⠬ ⠹⠣ ⠞⠮⠂ ⠲
⠇⠱⠿⠔⠆⠍⠉⠞⠖⠆ ⠒ ⠹⠉⠆⠈⠶ ⠒ ⠡⠪⠆⠍⠺⠋⠆ ⠒ ⠱⠆⠾⠣ ⠒ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠲
⠶ ⠨⠣ ⠶ ⠎⠱⠅ ⠨⠋⠎⠁⠆⠡⠑ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠞⠺⠱ ⠅ ⠗⠱⠆ ⠟⠪⠂ ⠟ ⠗⠣⠶ ⠲

==> test.br <==
⠼⠑ ⠲ ⠣⠗⠦ ⠈⠖ ⠰⠣⠣ ⠋⠨⠺⠁ ⠝ ⠶ ⠣⠃⠮⠳ ⠭ ⠱ ⠗⠣ ⠏ ⠹⠝ ⠲
⠼⠙ ⠲ ⠇⠥⠂⠇⠔ ⠹ ⠹⠥⠊ ⠈⠣⠗⠁ ⠰⠣⠁ ⠃⠽⠖⠆ ⠭ ⠟⠶⠆ ⠣⠃⠮⠳ ⠋⠿⠻⠆ ⠇⠕ ⠹⠝ ⠲
⠁⠆⠅⠣⠎⠁⠆ ⠿⠖⠏⠺⠮⠆ ⠟⠔⠆⠏⠣ ⠹ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/8
==> dev.my <==
အိပ်ရာ မှ ထ၍ မကြာမီ မှာ ပင် အနီးအနား ရှိ ဘုန်းကြီးကျောင်း မှ ကလတက်သံ ကို ကြား ရ လေ သည် ။
အမဲသား ငါးများ မ ပုပ် မ သိုး ဘဲ တာရှည်ခံ အောင် ဆား ဖြင့် ပြုပြင် ထား နိုင် သည် ။
ပါနီ လည်း လာ တယ် ရှိ တယ် ။

==> test.my <==
ဇာလီ ပျော် တဲ့ ကျောင်း သင်္ခမ်း ( အမ်း ကာရန် အချ သံ ) ချ သံ အလှည့် ။
၄ ။ သင် တို့ နေထိုင် ရာ အရပ်ဒေသ အလိုက် ထင်ရှား သော ပန်း အမည်များ ကို ဖော်ပြ ပါ ။
ကု ကူ ကူး ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠱⠅⠗⠁ ⠰⠣⠣ ⠁⠣⠯ ⠍⠣⠟⠁⠍⠪ ⠰⠣⠁ ⠏⠔ ⠣⠝⠪⠆⠣⠝⠁⠆ ⠩ ⠃⠉⠆⠟⠪⠆⠟⠶⠆ ⠰⠣⠣ ⠅⠣⠇⠣⠞⠑⠹⠋ ⠅ ⠟⠁⠆ ⠗⠣ ⠃ ⠹ ⠲
⠣⠍⠮⠆⠹⠁⠆ ⠌⠁⠆⠾ ⠋ ⠏⠦ ⠋ ⠹⠕⠆ ⠃⠮⠆ ⠞⠁⠩⠱⠨⠋ ⠶ ⠎⠓⠁⠆ ⠿⠓ ⠿⠥⠂⠿⠔ ⠞⠓⠁⠆ ⠝ ⠹ ⠲
⠏⠁⠝⠪ ⠇⠆ ⠇⠁ ⠞⠮ ⠩ ⠞⠮ ⠲

==> test.br <==
⠵⠁⠇⠪ ⠿⠻ ⠞⠮⠂ ⠟⠶⠆ ⠹⠔⠨⠋⠆ ⠶ ⠋⠆ ⠅⠁⠗⠋ ⠣⠡⠣ ⠹⠋ ⠶ ⠡⠣ ⠹⠋ ⠣⠸⠣⠮⠂ ⠲
⠼⠙ ⠲ ⠹⠔ ⠚ ⠝⠱⠁⠖ ⠗⠁ ⠣⠗⠣⠞⠙⠱⠹⠣ ⠣⠇⠬ ⠁⠔⠩⠁⠆ ⠹⠻⠆ ⠏⠋⠆ ⠣⠍⠾ ⠅ ⠘⠻⠿⠣ ⠏ ⠲
⠅⠥⠂ ⠅⠥ ⠅⠥⠆ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/9
==> dev.my <==
ထိုအခါ အဘိုးအို က ထင်းစည်း ကို ဖြေစေ၍ တစ် ယောက် တစ် ချောင်း စီ ချိုး စေ ပြန် ၏ ။
အောက်ပါ မေးခွန်းများ ကို စဉ်းစား ဖြေဆို ပါ ။
မင်းခမ်းမင်းနား အဆောင်အယောင်များ ကြောင့် မြန်မာ ဇာတ်သဘင် သည် ပိုမို ခမ်းနား လာ သည် ။

==> test.my <==
မြေ လည်း မာ ၏ ။
ရ ပါ တယ် ဆရာ ။
ကြီး ကား ကြီးပွား လို ၏ ။

==> train.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ရေခံတက်ပင် ၏ ခွကြား ၌ နား၍ စား ပြီးသော် အရိုး တို့ ကို ခံတက် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
==> dev.br <==
⠼⠣⠨⠁ ⠣⠃⠕⠆⠕ ⠅⠣ ⠁⠔⠆⠎⠪⠆ ⠅ ⠿⠓⠱⠎⠱⠯ ⠞⠭ ⠽⠴ ⠞⠭ ⠡⠶⠆ ⠎⠪ ⠡⠕⠆ ⠎ ⠿⠋ ⠊ ⠲
⠴⠏⠁ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠅ ⠎⠔⠆⠎⠁⠆ ⠿⠓⠱⠈⠕ ⠏ ⠲
⠍⠔⠆⠨⠋⠆⠍⠔⠆⠝⠁⠆ ⠣⠈⠶⠣⠽⠶⠾ ⠳ ⠾⠋⠍⠁ ⠵⠣⠞⠹⠣⠃⠔ ⠹ ⠏⠕⠍⠕ ⠨⠋⠆⠝⠁⠆ ⠇⠁ ⠹ ⠲

==> test.br <==
⠾⠱ ⠇⠆ ⠍⠁ ⠊ ⠲
⠗⠣ ⠏ ⠞⠮ ⠈⠣⠗⠁ ⠲
⠟⠪⠆ ⠅⠁⠆ ⠟⠪⠆⠏⠺⠁⠆ ⠇⠕ ⠊ ⠲

==> train.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠗⠱⠨⠋⠞⠑⠏⠔ ⠊ ⠨⠺⠣⠟⠁⠆ ⠫ ⠝⠁⠆⠯ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠨⠋⠞⠑ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
==========
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$
```

## Bulding Vocab Files

shell script တစ်ပုဒ် ရေးခဲ့တယ်...  

```bash
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cat ./build-vocab.sh 
#!/bin/bash

for i in {0..9};
do
   cd $i;
   pwd;
   mkdir vocab;
   cat ./train.my ./dev.my > ./vocab/train-dev.my
   cat ./train.br ./dev.br > ./vocab/train-dev.br
   
   #rm ./vocab/vocab*.yml;
   time marian-vocab < ./vocab/train-dev.my > ./vocab/vocab.my.yml
   time marian-vocab < ./vocab/train-dev.br > ./vocab/vocab.br.yml   
   ls -lh ./vocab/*     
   echo "==========";
  
  cd ..;
done
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$
```

run ခဲ့သည်...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ ./build-vocab.sh 
/media/ye/project2/exp/braille-nmt/data/for-nmt/0
[2022-02-19 01:08:36] Creating vocabulary...
[2022-02-19 01:08:36] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:36] Finished

real	0m0.216s
user	0m0.204s
sys	0m0.012s
[2022-02-19 01:08:36] Creating vocabulary...
[2022-02-19 01:08:36] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:36] Finished

real	0m0.185s
user	0m0.176s
sys	0m0.008s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 443K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 557K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/1
[2022-02-19 01:08:36] Creating vocabulary...
[2022-02-19 01:08:36] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:37] Finished

real	0m0.209s
user	0m0.196s
sys	0m0.012s
[2022-02-19 01:08:37] Creating vocabulary...
[2022-02-19 01:08:37] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:37] Finished

real	0m0.181s
user	0m0.172s
sys	0m0.008s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 557K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/2
[2022-02-19 01:08:37] Creating vocabulary...
[2022-02-19 01:08:37] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:37] Finished

real	0m0.216s
user	0m0.203s
sys	0m0.012s
[2022-02-19 01:08:37] Creating vocabulary...
[2022-02-19 01:08:37] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:37] Finished

real	0m0.179s
user	0m0.167s
sys	0m0.012s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 557K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/3
[2022-02-19 01:08:37] Creating vocabulary...
[2022-02-19 01:08:37] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:37] Finished

real	0m0.209s
user	0m0.200s
sys	0m0.008s
[2022-02-19 01:08:37] Creating vocabulary...
[2022-02-19 01:08:37] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:38] Finished

real	0m0.179s
user	0m0.171s
sys	0m0.008s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 558K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/4
[2022-02-19 01:08:38] Creating vocabulary...
[2022-02-19 01:08:38] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:38] Finished

real	0m0.210s
user	0m0.201s
sys	0m0.008s
[2022-02-19 01:08:38] Creating vocabulary...
[2022-02-19 01:08:38] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:38] Finished

real	0m0.179s
user	0m0.162s
sys	0m0.016s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 558K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/5
[2022-02-19 01:08:38] Creating vocabulary...
[2022-02-19 01:08:38] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:38] Finished

real	0m0.209s
user	0m0.205s
sys	0m0.004s
[2022-02-19 01:08:38] Creating vocabulary...
[2022-02-19 01:08:38] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:38] Finished

real	0m0.181s
user	0m0.176s
sys	0m0.004s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 557K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/6
[2022-02-19 01:08:38] Creating vocabulary...
[2022-02-19 01:08:38] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:39] Finished

real	0m0.208s
user	0m0.195s
sys	0m0.012s
[2022-02-19 01:08:39] Creating vocabulary...
[2022-02-19 01:08:39] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:39] Finished

real	0m0.180s
user	0m0.175s
sys	0m0.004s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 443K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 556K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/7
[2022-02-19 01:08:39] Creating vocabulary...
[2022-02-19 01:08:39] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:39] Finished

real	0m0.208s
user	0m0.204s
sys	0m0.004s
[2022-02-19 01:08:39] Creating vocabulary...
[2022-02-19 01:08:39] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:39] Finished

real	0m0.186s
user	0m0.175s
sys	0m0.012s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 558K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/8
[2022-02-19 01:08:39] Creating vocabulary...
[2022-02-19 01:08:39] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:39] Finished

real	0m0.213s
user	0m0.209s
sys	0m0.004s
[2022-02-19 01:08:39] Creating vocabulary...
[2022-02-19 01:08:39] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:40] Finished

real	0m0.184s
user	0m0.176s
sys	0m0.008s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 558K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
/media/ye/project2/exp/braille-nmt/data/for-nmt/9
[2022-02-19 01:08:40] Creating vocabulary...
[2022-02-19 01:08:40] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:40] Finished

real	0m0.208s
user	0m0.200s
sys	0m0.008s
[2022-02-19 01:08:40] Creating vocabulary...
[2022-02-19 01:08:40] [data] Creating vocabulary stdout from stdin
[2022-02-19 01:08:40] Finished

real	0m0.184s
user	0m0.173s
sys	0m0.012s
-rwxr-xr-x 1 ye ye 2.5M ဖေ   19 01:08 ./vocab/train-dev.br
-rwxr-xr-x 1 ye ye 3.3M ဖေ   19 01:08 ./vocab/train-dev.my
-rwxr-xr-x 1 ye ye 444K ဖေ   19 01:08 ./vocab/vocab.br.yml
-rwxr-xr-x 1 ye ye 557K ဖေ   19 01:08 ./vocab/vocab.my.yml
==========
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$ cat ./build-vocab.sh 
#!/bin/bash

for i in {0..9};
do
   cd $i;
   pwd;
   mkdir vocab;
   cat ./train.my ./dev.my > ./vocab/train-dev.my
   cat ./train.br ./dev.br > ./vocab/train-dev.br
   
   #rm ./vocab/vocab*.yml;
   time marian-vocab < ./vocab/train-dev.my > ./vocab/vocab.my.yml
   time marian-vocab < ./vocab/train-dev.br > ./vocab/vocab.br.yml   
   ls -lh ./vocab/*     
   echo "==========";
  
  cd ..;
done
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt$
```

## Get the script

```
https://raw.githubusercontent.com/ye-kyaw-thu/MTRSS/master/WAT2021/scripts/nmt/YCC-MT2/transformer.sh
```

check the reference script:  
(ဒီ script က WAT 2021 အတွက် သုံးခဲ့တဲ့ script ပါ)  


(base) ye@:/media/ye/project2/exp/braille-nmt$ cat ./transformer.sh   

```bash  
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for WAT2021 en-my, my-en share tasks

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \ 
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer;

marian \
    --model model.transformer/model.npz --type transformer \
    --train-sets data/train.en data/train.my \
    --max-length 200 \
    --vocabs data/vocab/vocab.en.yml data/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data/valid.en data/valid.my \
    --valid-translation-output data/valid.en-my.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer/train.log --valid-log model.transformer/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer/config.yml
    
time marian -c model.transformer/config.yml  2>&1 | tee transformer-enmy.log

```

## Editing the Script

Myanmar-to-Braille ကို training လုပ်ဖို့အတွက် အရင် WAT2021 အတွက် သုံးခဲ့တဲ့ shell script ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Myanmar-Braille, Braille-Myanmar NMT Translation
## 19 Feb 2022

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \ 
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz --type transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my-br.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer/train.log --valid-log /media/ye/project2/exp/braille-nmt/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer/config0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer/config0.yml  2>&1 | tee transformer-mybr0.log

```

## Running or Training Transformer for Myanmar-to-Braille (for 0/)

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./transformer.sh 
mkdir: cannot create directory ‘model.transformer’: File exists
[2022-02-19 01:11:11] [marian] Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-02-19 01:11:11] [marian] Running on administrator-HP-Z2-Tower-G4-Workstation as process 573846 with command line:
[2022-02-19 01:11:11] [marian] marian -c /media/ye/project2/exp/braille-nmt/model.transformer/config0.yml
[2022-02-19 01:11:11] [config] after: 0e
[2022-02-19 01:11:11] [config] after-batches: 0
[2022-02-19 01:11:11] [config] after-epochs: 0
[2022-02-19 01:11:11] [config] all-caps-every: 0
[2022-02-19 01:11:11] [config] allow-unk: false
[2022-02-19 01:11:11] [config] authors: false
[2022-02-19 01:11:11] [config] beam-size: 6
[2022-02-19 01:11:11] [config] bert-class-symbol: "[CLS]"
[2022-02-19 01:11:11] [config] bert-mask-symbol: "[MASK]"
[2022-02-19 01:11:11] [config] bert-masking-fraction: 0.15
[2022-02-19 01:11:11] [config] bert-sep-symbol: "[SEP]"
[2022-02-19 01:11:11] [config] bert-train-type-embeddings: true
[2022-02-19 01:11:11] [config] bert-type-vocab-size: 2
[2022-02-19 01:11:11] [config] build-info: ""
[2022-02-19 01:11:11] [config] cite: false
[2022-02-19 01:11:11] [config] clip-norm: 5
[2022-02-19 01:11:11] [config] cost-scaling:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] cost-type: ce-sum
[2022-02-19 01:11:11] [config] cpu-threads: 0
[2022-02-19 01:11:11] [config] data-weighting: ""
[2022-02-19 01:11:11] [config] data-weighting-type: sentence
[2022-02-19 01:11:11] [config] dec-cell: gru
[2022-02-19 01:11:11] [config] dec-cell-base-depth: 2
[2022-02-19 01:11:11] [config] dec-cell-high-depth: 1
[2022-02-19 01:11:11] [config] dec-depth: 2
[2022-02-19 01:11:11] [config] devices:
[2022-02-19 01:11:11] [config]   - 0
[2022-02-19 01:11:11] [config]   - 1
[2022-02-19 01:11:11] [config] dim-emb: 512
[2022-02-19 01:11:11] [config] dim-rnn: 1024
[2022-02-19 01:11:11] [config] dim-vocabs:
[2022-02-19 01:11:11] [config]   - 0
[2022-02-19 01:11:11] [config]   - 0
[2022-02-19 01:11:11] [config] disp-first: 0
[2022-02-19 01:11:11] [config] disp-freq: 500
[2022-02-19 01:11:11] [config] disp-label-counts: true
[2022-02-19 01:11:11] [config] dropout-rnn: 0
[2022-02-19 01:11:11] [config] dropout-src: 0
[2022-02-19 01:11:11] [config] dropout-trg: 0
[2022-02-19 01:11:11] [config] dump-config: ""
[2022-02-19 01:11:11] [config] early-stopping: 10
[2022-02-19 01:11:11] [config] embedding-fix-src: false
[2022-02-19 01:11:11] [config] embedding-fix-trg: false
[2022-02-19 01:11:11] [config] embedding-normalization: false
[2022-02-19 01:11:11] [config] embedding-vectors:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] enc-cell: gru
[2022-02-19 01:11:11] [config] enc-cell-depth: 1
[2022-02-19 01:11:11] [config] enc-depth: 2
[2022-02-19 01:11:11] [config] enc-type: bidirectional
[2022-02-19 01:11:11] [config] english-title-case-every: 0
[2022-02-19 01:11:11] [config] exponential-smoothing: 0.0001
[2022-02-19 01:11:11] [config] factor-weight: 1
[2022-02-19 01:11:11] [config] grad-dropping-momentum: 0
[2022-02-19 01:11:11] [config] grad-dropping-rate: 0
[2022-02-19 01:11:11] [config] grad-dropping-warmup: 100
[2022-02-19 01:11:11] [config] gradient-checkpointing: false
[2022-02-19 01:11:11] [config] guided-alignment: none
[2022-02-19 01:11:11] [config] guided-alignment-cost: mse
[2022-02-19 01:11:11] [config] guided-alignment-weight: 0.1
[2022-02-19 01:11:11] [config] ignore-model-config: false
[2022-02-19 01:11:11] [config] input-types:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] interpolate-env-vars: false
[2022-02-19 01:11:11] [config] keep-best: false
[2022-02-19 01:11:11] [config] label-smoothing: 0.1
[2022-02-19 01:11:11] [config] layer-normalization: false
[2022-02-19 01:11:11] [config] learn-rate: 0.0003
[2022-02-19 01:11:11] [config] lemma-dim-emb: 0
[2022-02-19 01:11:11] [config] log: model.transformer/train.log
[2022-02-19 01:11:11] [config] log-level: info
[2022-02-19 01:11:11] [config] log-time-zone: ""
[2022-02-19 01:11:11] [config] logical-epoch:
[2022-02-19 01:11:11] [config]   - 1e
[2022-02-19 01:11:11] [config]   - 0
[2022-02-19 01:11:11] [config] lr-decay: 0
[2022-02-19 01:11:11] [config] lr-decay-freq: 50000
[2022-02-19 01:11:11] [config] lr-decay-inv-sqrt:
[2022-02-19 01:11:11] [config]   - 16000
[2022-02-19 01:11:11] [config] lr-decay-repeat-warmup: false
[2022-02-19 01:11:11] [config] lr-decay-reset-optimizer: false
[2022-02-19 01:11:11] [config] lr-decay-start:
[2022-02-19 01:11:11] [config]   - 10
[2022-02-19 01:11:11] [config]   - 1
[2022-02-19 01:11:11] [config] lr-decay-strategy: epoch+stalled
[2022-02-19 01:11:11] [config] lr-report: true
[2022-02-19 01:11:11] [config] lr-warmup: 0
[2022-02-19 01:11:11] [config] lr-warmup-at-reload: false
[2022-02-19 01:11:11] [config] lr-warmup-cycle: false
[2022-02-19 01:11:11] [config] lr-warmup-start-rate: 0
[2022-02-19 01:11:11] [config] max-length: 200
[2022-02-19 01:11:11] [config] max-length-crop: false
[2022-02-19 01:11:11] [config] max-length-factor: 3
[2022-02-19 01:11:11] [config] maxi-batch: 100
[2022-02-19 01:11:11] [config] maxi-batch-sort: trg
[2022-02-19 01:11:11] [config] mini-batch: 64
[2022-02-19 01:11:11] [config] mini-batch-fit: true
[2022-02-19 01:11:11] [config] mini-batch-fit-step: 10
[2022-02-19 01:11:11] [config] mini-batch-track-lr: false
[2022-02-19 01:11:11] [config] mini-batch-warmup: 0
[2022-02-19 01:11:11] [config] mini-batch-words: 0
[2022-02-19 01:11:11] [config] mini-batch-words-ref: 0
[2022-02-19 01:11:11] [config] model: /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz
[2022-02-19 01:11:11] [config] multi-loss-type: sum
[2022-02-19 01:11:11] [config] multi-node: false
[2022-02-19 01:11:11] [config] multi-node-overlap: true
[2022-02-19 01:11:11] [config] n-best: false
[2022-02-19 01:11:11] [config] no-nccl: false
[2022-02-19 01:11:11] [config] no-reload: false
[2022-02-19 01:11:11] [config] no-restore-corpus: false
[2022-02-19 01:11:11] [config] normalize: 0.6
[2022-02-19 01:11:11] [config] normalize-gradient: false
[2022-02-19 01:11:11] [config] num-devices: 0
[2022-02-19 01:11:11] [config] optimizer: adam
[2022-02-19 01:11:11] [config] optimizer-delay: 1
[2022-02-19 01:11:11] [config] optimizer-params:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] output-omit-bias: false
[2022-02-19 01:11:11] [config] overwrite: false
[2022-02-19 01:11:11] [config] precision:
[2022-02-19 01:11:11] [config]   - float32
[2022-02-19 01:11:11] [config]   - float32
[2022-02-19 01:11:11] [config]   - float32
[2022-02-19 01:11:11] [config] pretrained-model: ""
[2022-02-19 01:11:11] [config] quantize-biases: false
[2022-02-19 01:11:11] [config] quantize-bits: 0
[2022-02-19 01:11:11] [config] quantize-log-based: false
[2022-02-19 01:11:11] [config] quantize-optimization-steps: 0
[2022-02-19 01:11:11] [config] quiet: false
[2022-02-19 01:11:11] [config] quiet-translation: true
[2022-02-19 01:11:11] [config] relative-paths: false
[2022-02-19 01:11:11] [config] right-left: false
[2022-02-19 01:11:11] [config] save-freq: 5000
[2022-02-19 01:11:11] [config] seed: 1111
[2022-02-19 01:11:11] [config] sentencepiece-alphas:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] sentencepiece-max-lines: 2000000
[2022-02-19 01:11:11] [config] sentencepiece-options: ""
[2022-02-19 01:11:11] [config] shuffle: data
[2022-02-19 01:11:11] [config] shuffle-in-ram: false
[2022-02-19 01:11:11] [config] sigterm: save-and-exit
[2022-02-19 01:11:11] [config] skip: false
[2022-02-19 01:11:11] [config] sqlite: ""
[2022-02-19 01:11:11] [config] sqlite-drop: false
[2022-02-19 01:11:11] [config] sync-sgd: true
[2022-02-19 01:11:11] [config] tempdir: /tmp
[2022-02-19 01:11:11] [config] tied-embeddings: true
[2022-02-19 01:11:11] [config] tied-embeddings-all: false
[2022-02-19 01:11:11] [config] tied-embeddings-src: false
[2022-02-19 01:11:11] [config] train-embedder-rank:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] train-sets:
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br
[2022-02-19 01:11:11] [config] transformer-aan-activation: swish
[2022-02-19 01:11:11] [config] transformer-aan-depth: 2
[2022-02-19 01:11:11] [config] transformer-aan-nogate: false
[2022-02-19 01:11:11] [config] transformer-decoder-autoreg: self-attention
[2022-02-19 01:11:11] [config] transformer-depth-scaling: false
[2022-02-19 01:11:11] [config] transformer-dim-aan: 2048
[2022-02-19 01:11:11] [config] transformer-dim-ffn: 2048
[2022-02-19 01:11:11] [config] transformer-dropout: 0.3
[2022-02-19 01:11:11] [config] transformer-dropout-attention: 0
[2022-02-19 01:11:11] [config] transformer-dropout-ffn: 0
[2022-02-19 01:11:11] [config] transformer-ffn-activation: swish
[2022-02-19 01:11:11] [config] transformer-ffn-depth: 2
[2022-02-19 01:11:11] [config] transformer-guided-alignment-layer: last
[2022-02-19 01:11:11] [config] transformer-heads: 8
[2022-02-19 01:11:11] [config] transformer-no-projection: false
[2022-02-19 01:11:11] [config] transformer-pool: false
[2022-02-19 01:11:11] [config] transformer-postprocess: dan
[2022-02-19 01:11:11] [config] transformer-postprocess-emb: d
[2022-02-19 01:11:11] [config] transformer-postprocess-top: ""
[2022-02-19 01:11:11] [config] transformer-preprocess: ""
[2022-02-19 01:11:11] [config] transformer-tied-layers:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] transformer-train-position-embeddings: false
[2022-02-19 01:11:11] [config] tsv: false
[2022-02-19 01:11:11] [config] tsv-fields: 0
[2022-02-19 01:11:11] [config] type: transformer
[2022-02-19 01:11:11] [config] ulr: false
[2022-02-19 01:11:11] [config] ulr-dim-emb: 0
[2022-02-19 01:11:11] [config] ulr-dropout: 0
[2022-02-19 01:11:11] [config] ulr-keys-vectors: ""
[2022-02-19 01:11:11] [config] ulr-query-vectors: ""
[2022-02-19 01:11:11] [config] ulr-softmax-temperature: 1
[2022-02-19 01:11:11] [config] ulr-trainable-transformation: false
[2022-02-19 01:11:11] [config] unlikelihood-loss: false
[2022-02-19 01:11:11] [config] valid-freq: 5000
[2022-02-19 01:11:11] [config] valid-log: /media/ye/project2/exp/braille-nmt/valid.log
[2022-02-19 01:11:11] [config] valid-max-length: 1000
[2022-02-19 01:11:11] [config] valid-metrics:
[2022-02-19 01:11:11] [config]   - cross-entropy
[2022-02-19 01:11:11] [config]   - perplexity
[2022-02-19 01:11:11] [config]   - bleu
[2022-02-19 01:11:11] [config] valid-mini-batch: 64
[2022-02-19 01:11:11] [config] valid-reset-stalled: false
[2022-02-19 01:11:11] [config] valid-script-args:
[2022-02-19 01:11:11] [config]   []
[2022-02-19 01:11:11] [config] valid-script-path: ""
[2022-02-19 01:11:11] [config] valid-sets:
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br
[2022-02-19 01:11:11] [config] valid-translation-output: /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my-br.output
[2022-02-19 01:11:11] [config] vocabs:
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-02-19 01:11:11] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-02-19 01:11:11] [config] word-penalty: 0
[2022-02-19 01:11:11] [config] word-scores: false
[2022-02-19 01:11:11] [config] workspace: 1000
[2022-02-19 01:11:11] [config] Model is being created with Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-02-19 01:11:11] Using synchronous SGD
[2022-02-19 01:11:11] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-02-19 01:11:11] [data] Setting vocabulary size for input 0 to 18,602
[2022-02-19 01:11:11] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-02-19 01:11:11] [data] Setting vocabulary size for input 1 to 18,364
[2022-02-19 01:11:11] [comm] Compiled without MPI support. Running as a single process on administrator-HP-Z2-Tower-G4-Workstation
[2022-02-19 01:11:11] [batching] Collecting statistics for batch fitting with step size 10
[2022-02-19 01:11:11] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-02-19 01:11:12] [memory] Extending reserved space to 1024 MB (device gpu1)
[2022-02-19 01:11:12] [comm] Using NCCL 2.8.3 for GPU communication
[2022-02-19 01:11:12] [comm] NCCLCommunicator constructed successfully
[2022-02-19 01:11:12] [training] Using 2 GPUs
[2022-02-19 01:11:12] [logits] Applying loss function for 1 factor(s)
[2022-02-19 01:11:12] [memory] Reserving 128 MB, device gpu0
[2022-02-19 01:11:12] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-02-19 01:11:12] [memory] Reserving 128 MB, device gpu0
[2022-02-19 01:11:37] [batching] Done. Typical MB size is 4,134 target words
[2022-02-19 01:11:37] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-02-19 01:11:38] [memory] Extending reserved space to 1024 MB (device gpu1)
[2022-02-19 01:11:38] [comm] Using NCCL 2.8.3 for GPU communication
[2022-02-19 01:11:38] [comm] NCCLCommunicator constructed successfully
[2022-02-19 01:11:38] [training] Using 2 GPUs
[2022-02-19 01:11:38] Training started
[2022-02-19 01:11:38] [data] Shuffling data
[2022-02-19 01:11:38] [data] Done reading 16,415 sentences
[2022-02-19 01:11:38] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:11:38] [training] Batches are processed as 1 process(es) x 2 devices/process
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu1
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu0
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu0
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu1
[2022-02-19 01:11:38] [memory] Reserving 64 MB, device gpu0
[2022-02-19 01:11:38] [memory] Reserving 64 MB, device gpu1
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu1
[2022-02-19 01:11:38] [memory] Reserving 128 MB, device gpu0
[2022-02-19 01:12:07] Seen 16415 samples
[2022-02-19 01:12:07] Starting data epoch 2 in logical epoch 2
[2022-02-19 01:12:07] [data] Shuffling data
[2022-02-19 01:12:08] [data] Done reading 16,415 sentences
[2022-02-19 01:12:08] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:12:36] Seen 16415 samples
[2022-02-19 01:12:36] Starting data epoch 3 in logical epoch 3
[2022-02-19 01:12:36] [data] Shuffling data
[2022-02-19 01:12:36] [data] Done reading 16,415 sentences
[2022-02-19 01:12:36] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:13:05] Seen 16415 samples
[2022-02-19 01:13:05] Starting data epoch 4 in logical epoch 4
[2022-02-19 01:13:05] [data] Shuffling data
[2022-02-19 01:13:05] [data] Done reading 16,415 sentences
[2022-02-19 01:13:05] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:13:33] Seen 16415 samples
[2022-02-19 01:13:33] Starting data epoch 5 in logical epoch 5
[2022-02-19 01:13:33] [data] Shuffling data
[2022-02-19 01:13:33] [data] Done reading 16,415 sentences
[2022-02-19 01:13:33] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:14:03] Seen 16415 samples
[2022-02-19 01:14:03] Starting data epoch 6 in logical epoch 6
[2022-02-19 01:14:03] [data] Shuffling data
[2022-02-19 01:14:03] [data] Done reading 16,415 sentences
[2022-02-19 01:14:03] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:14:33] Seen 16415 samples
[2022-02-19 01:14:33] Starting data epoch 7 in logical epoch 7
[2022-02-19 01:14:33] [data] Shuffling data
[2022-02-19 01:14:33] [data] Done reading 16,415 sentences
[2022-02-19 01:14:33] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:14:57] Ep. 7 : Up. 500 : Sen. 13,097 : Cost 5.29971933 * 1,606,009 @ 2,847 after 1,606,009 : Time 199.15s : 8064.22 words/s : L.r. 3.0000e-04
[2022-02-19 01:15:03] Seen 16415 samples
[2022-02-19 01:15:03] Starting data epoch 8 in logical epoch 8
[2022-02-19 01:15:03] [data] Shuffling data
[2022-02-19 01:15:03] [data] Done reading 16,415 sentences
[2022-02-19 01:15:03] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:15:34] Seen 16415 samples
[2022-02-19 01:15:34] Starting data epoch 9 in logical epoch 9
[2022-02-19 01:15:34] [data] Shuffling data
[2022-02-19 01:15:34] [data] Done reading 16,415 sentences
[2022-02-19 01:15:34] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:16:04] Seen 16415 samples
[2022-02-19 01:16:04] Starting data epoch 10 in logical epoch 10
[2022-02-19 01:16:04] [data] Shuffling data
[2022-02-19 01:16:04] [data] Done reading 16,415 sentences
[2022-02-19 01:16:04] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:16:34] Seen 16415 samples
[2022-02-19 01:16:34] Starting data epoch 11 in logical epoch 11
[2022-02-19 01:16:34] [data] Shuffling data
[2022-02-19 01:16:34] [data] Done reading 16,415 sentences
[2022-02-19 01:16:34] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:17:04] Seen 16415 samples
[2022-02-19 01:17:04] Starting data epoch 12 in logical epoch 12
[2022-02-19 01:17:04] [data] Shuffling data
[2022-02-19 01:17:04] [data] Done reading 16,415 sentences
[2022-02-19 01:17:04] [data] Done shuffling 16,415 sentences to temp files
...
...
...
[2022-02-19 01:37:21] Seen 16415 samples
[2022-02-19 01:37:21] Starting data epoch 53 in logical epoch 53
[2022-02-19 01:37:21] [data] Shuffling data
[2022-02-19 01:37:21] [data] Done reading 16,415 sentences
[2022-02-19 01:37:21] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:37:51] Seen 16415 samples
[2022-02-19 01:37:51] Starting data epoch 54 in logical epoch 54
[2022-02-19 01:37:51] [data] Shuffling data
[2022-02-19 01:37:51] [data] Done reading 16,415 sentences
[2022-02-19 01:37:51] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:38:21] Seen 16415 samples
[2022-02-19 01:38:21] Starting data epoch 55 in logical epoch 55
[2022-02-19 01:38:21] [data] Shuffling data
[2022-02-19 01:38:21] [data] Done reading 16,415 sentences
[2022-02-19 01:38:21] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:38:34] Ep. 55 : Up. 4000 : Sen. 7,128 : Cost 1.44619870 * 1,610,751 @ 2,523 after 12,876,642 : Time 205.39s : 7842.56 words/s : L.r. 3.0000e-04
[2022-02-19 01:38:51] Seen 16415 samples
[2022-02-19 01:38:51] Starting data epoch 56 in logical epoch 56
[2022-02-19 01:38:51] [data] Shuffling data
[2022-02-19 01:38:51] [data] Done reading 16,415 sentences
[2022-02-19 01:38:51] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:39:23] Seen 16415 samples
[2022-02-19 01:39:23] Starting data epoch 57 in logical epoch 57
[2022-02-19 01:39:23] [data] Shuffling data
[2022-02-19 01:39:23] [data] Done reading 16,415 sentences
[2022-02-19 01:39:23] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:39:53] Seen 16415 samples
[2022-02-19 01:39:53] Starting data epoch 58 in logical epoch 58
[2022-02-19 01:39:53] [data] Shuffling data
[2022-02-19 01:39:53] [data] Done reading 16,415 sentences
[2022-02-19 01:39:53] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:40:23] Seen 16415 samples
[2022-02-19 01:40:23] Starting data epoch 59 in logical epoch 59
[2022-02-19 01:40:23] [data] Shuffling data
[2022-02-19 01:40:23] [data] Done reading 16,415 sentences
[2022-02-19 01:40:23] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:40:53] Seen 16415 samples
[2022-02-19 01:40:53] Starting data epoch 60 in logical epoch 60
[2022-02-19 01:40:53] [data] Shuffling data
[2022-02-19 01:40:53] [data] Done reading 16,415 sentences
[2022-02-19 01:40:53] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:41:24] Seen 16415 samples
[2022-02-19 01:41:24] Starting data epoch 61 in logical epoch 61
[2022-02-19 01:41:24] [data] Shuffling data
[2022-02-19 01:41:24] [data] Done reading 16,415 sentences
[2022-02-19 01:41:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:41:54] Seen 16415 samples
[2022-02-19 01:41:54] Starting data epoch 62 in logical epoch 62
[2022-02-19 01:41:54] [data] Shuffling data
[2022-02-19 01:41:54] [data] Done reading 16,415 sentences
[2022-02-19 01:41:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:42:00] Ep. 62 : Up. 4500 : Sen. 2,904 : Cost 1.42916024 * 1,602,719 @ 3,492 after 14,479,361 : Time 206.35s : 7766.98 words/s : L.r. 3.0000e-04
[2022-02-19 01:42:24] Seen 16415 samples
[2022-02-19 01:42:24] Starting data epoch 63 in logical epoch 63
[2022-02-19 01:42:24] [data] Shuffling data
[2022-02-19 01:42:24] [data] Done reading 16,415 sentences
[2022-02-19 01:42:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:42:54] Seen 16415 samples
[2022-02-19 01:42:54] Starting data epoch 64 in logical epoch 64
[2022-02-19 01:42:54] [data] Shuffling data
[2022-02-19 01:42:54] [data] Done reading 16,415 sentences
[2022-02-19 01:42:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:43:24] Seen 16415 samples
[2022-02-19 01:43:24] Starting data epoch 65 in logical epoch 65
[2022-02-19 01:43:24] [data] Shuffling data
[2022-02-19 01:43:24] [data] Done reading 16,415 sentences
[2022-02-19 01:43:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:43:54] Seen 16415 samples
[2022-02-19 01:43:54] Starting data epoch 66 in logical epoch 66
[2022-02-19 01:43:54] [data] Shuffling data
[2022-02-19 01:43:54] [data] Done reading 16,415 sentences
[2022-02-19 01:43:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:44:24] Seen 16415 samples
[2022-02-19 01:44:24] Starting data epoch 67 in logical epoch 67
[2022-02-19 01:44:24] [data] Shuffling data
[2022-02-19 01:44:24] [data] Done reading 16,415 sentences
[2022-02-19 01:44:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:44:54] Seen 16415 samples
[2022-02-19 01:44:54] Starting data epoch 68 in logical epoch 68
[2022-02-19 01:44:54] [data] Shuffling data
[2022-02-19 01:44:54] [data] Done reading 16,415 sentences
[2022-02-19 01:44:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 01:45:23] Ep. 68 : Up. 5000 : Sen. 16,183 : Cost 1.41602731 * 1,605,007 @ 3,108 after 16,084,368 : Time 202.97s : 7907.63 words/s : L.r. 3.0000e-04
[2022-02-19 01:45:23] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.orig.npz
[2022-02-19 01:45:24] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.iter5000.npz
[2022-02-19 01:45:24] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz
[2022-02-19 01:45:25] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.optimizer.npz
tcmalloc: large alloc 1073741824 bytes == 0x559ebaf94000 @ 
tcmalloc: large alloc 1207959552 bytes == 0x559ebaf94000 @ 
tcmalloc: large alloc 1476395008 bytes == 0x559ebaf94000 @ 
tcmalloc: large alloc 1610612736 bytes == 0x559ebaf94000 @ 
[2022-02-19 01:45:33] [valid] Ep. 68 : Up. 5000 : cross-entropy : 8.1241 : new best
[2022-02-19 01:45:37] Error: CUDA error 2 'out of memory' - /home/ye/tool/marian/src/tensors/gpu/device.cu:32: cudaMalloc(&data_, size)
[2022-02-19 01:45:37] Error: Aborted from virtual void marian::gpu::Device::reserve(size_t) in /home/ye/tool/marian/src/tensors/gpu/device.cu:32

[CALL STACK]
[0x559e91d97880]    marian::gpu::Device::  reserve  (unsigned long)    + 0xf80
[0x559e916c77df]    marian::TensorAllocator::  allocate  (IntrusivePtr<marian::TensorBase>&,  marian::Shape,  marian::Type) + 0x4ef
[0x559e918d3b00]    marian::Node::  allocate  ()                       + 0x1e0
[0x559e918ca2ce]    marian::ExpressionGraph::  forward  (std::__cxx11::list<IntrusivePtr<marian::Chainable<IntrusivePtr<marian::TensorBase>>>,std::allocator<IntrusivePtr<marian::Chainable<IntrusivePtr<marian::TensorBase>>>>>&,  bool) + 0x8e
[0x559e918cbcae]    marian::ExpressionGraph::  forwardNext  ()         + 0x24e
[0x559e91a9ce64]                                                       + 0x77de64
[0x559e91a9d694]                                                       + 0x77e694
[0x559e9167115d]    std::__future_base::_State_baseV2::  _M_do_set  (std::function<std::unique_ptr<std::__future_base::_Result_base,std::__future_base::_Result_base::_Deleter> ()>*,  bool*) + 0x2d
[0x7f6b06ff7c0f]                                                       + 0x11c0f
[0x559e91a9418a]                                                       + 0x77518a
[0x559e9167389a]    std::thread::_State_impl<std::thread::_Invoker<std::tuple<marian::ThreadPool::reserve(unsigned long)::{lambda()#1}>>>::  _M_run  () + 0x13a
[0x7f6b06edade4]                                                       + 0xd6de4
[0x7f6b06fef590]                                                       + 0x9590
[0x7f6b06bc9223]    clone                                              + 0x43


real	34m26.806s
user	56m37.654s
sys	0m5.917s
(base) ye@:/media/ye/project2/exp/braille-nmt$ 
```

Run လုပ်နေရင်းနဲ့ အထက်ပါအတိုင်း crush ဖြစ်သွားလို့ စက်ကို restart လုပ်ပြီးမှ ပြန် run ခဲ့တယ်။  

## Checking GPU Usage

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ nvidia-smi 
Sat Feb 19 01:15:40 2022       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.119.03   Driver Version: 450.119.03   CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro P1000        Off  | 00000000:01:00.0  On |                  N/A |
| 80%   81C    P0    N/A /  N/A |   3631MiB /  4036MiB |     99%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  Quadro P1000        Off  | 00000000:03:00.0 Off |                  N/A |
| 78%   81C    P0    N/A /  N/A |   1754MiB /  4040MiB |     99%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      2105      G   /usr/lib/xorg/Xorg                458MiB |
|    0   N/A  N/A      2242      G   /usr/bin/gnome-shell              380MiB |
|    0   N/A  N/A    439424      G   ...AAAAAAAAA= --shared-files     1041MiB |
|    0   N/A  N/A    573846      C   marian                           1745MiB |
|    1   N/A  N/A      2105      G   /usr/lib/xorg/Xorg                  4MiB |
|    1   N/A  N/A    573846      C   marian                           1745MiB |
+-----------------------------------------------------------------------------+
(base) ye@:/media/ye/project2/exp/braille-nmt$ 
```

## Retraining

Restart လုပ်ပြီး ပြန် train ကြည့်ခဲ့...  
ဒီတစ်ခါတော့ error မပေးတော့ဘူး...  

```

...
...
...
[2022-02-19 12:40:55] Starting data epoch 1360 in logical epoch 1360
[2022-02-19 12:40:55] [data] Shuffling data
[2022-02-19 12:40:55] [data] Done reading 16,415 sentences
[2022-02-19 12:40:55] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 12:41:24] Seen 16415 samples
[2022-02-19 12:41:24] Starting data epoch 1361 in logical epoch 1361
[2022-02-19 12:41:24] [data] Shuffling data
[2022-02-19 12:41:24] [data] Done reading 16,415 sentences
[2022-02-19 12:41:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 12:41:54] Seen 16415 samples
[2022-02-19 12:41:54] Starting data epoch 1362 in logical epoch 1362
[2022-02-19 12:41:54] [data] Shuffling data
[2022-02-19 12:41:54] [data] Done reading 16,415 sentences
[2022-02-19 12:41:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 12:42:24] Seen 16415 samples
[2022-02-19 12:42:24] Starting data epoch 1363 in logical epoch 1363
[2022-02-19 12:42:24] [data] Shuffling data
[2022-02-19 12:42:24] [data] Done reading 16,415 sentences
[2022-02-19 12:42:24] [data] Done shuffling 16,415 sentences to temp files
[2022-02-19 12:42:25] Ep. 1363 : Up. 100000 : Sen. 536 : Cost 1.32002175 * 1,615,204 @ 3,858 after 322,221,966 : Time 203.72s : 7928.66 words/s : L.r. 1.2000e-04
[2022-02-19 12:42:25] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.orig.npz
[2022-02-19 12:42:26] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.iter100000.npz
[2022-02-19 12:42:26] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz
[2022-02-19 12:42:27] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.optimizer.npz
[2022-02-19 12:42:30] [valid] Ep. 1363 : Up. 100000 : cross-entropy : 7.78329 : stalled 10 times (last best: 7.65078)
[2022-02-19 12:42:32] [valid] Ep. 1363 : Up. 100000 : perplexity : 1.70973 : stalled 10 times (last best: 1.69419)
[2022-02-19 12:42:46] [valid] Ep. 1363 : Up. 100000 : bleu : 87.2733 : stalled 8 times (last best: 87.288)
[2022-02-19 12:42:46] Training finished
[2022-02-19 12:42:47] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.orig.npz
[2022-02-19 12:42:47] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz
[2022-02-19 12:42:48] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer/model0-mybr.npz.optimizer.npz

real	642m50.866s
user	1070m43.506s
sys	1m18.182s
(base) ye@:/media/ye/project2/exp/braille-nmt$ 
```

## Prepare Shell Script for Braille to Myanmar (for 0)

(base) ye@:/media/ye/project2/exp/braille-nmt$ cat ./transformer-brmy.sh  

```bash 
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Myanmar-Braille, Braille-Myanmar NMT Translation
## 19 Feb 2022

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \ 
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer-brmy;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz --type transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br-my.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer-brmy/train0.log --valid-log /media/ye/project2/exp/braille-nmt/valid0.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-brmy/config0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-brmy/config0.yml  2>&1 | tee transformer-brmy0.log

```

## Training Transformer Model for Braille to Myanmar (for 0)

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./transformer-brmy.sh 
...
...
...
[2022-02-20 18:38:51] Starting data epoch 1077 in logical epoch 1077
[2022-02-20 18:38:51] [data] Shuffling data
[2022-02-20 18:38:51] [data] Done reading 16,415 sentences
[2022-02-20 18:38:51] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:39:22] Seen 16415 samples
[2022-02-20 18:39:22] Starting data epoch 1078 in logical epoch 1078
[2022-02-20 18:39:22] [data] Shuffling data
[2022-02-20 18:39:22] [data] Done reading 16,415 sentences
[2022-02-20 18:39:23] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:39:54] Seen 16415 samples
[2022-02-20 18:39:54] Starting data epoch 1079 in logical epoch 1079
[2022-02-20 18:39:54] [data] Shuffling data
[2022-02-20 18:39:54] [data] Done reading 16,415 sentences
[2022-02-20 18:39:54] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:40:26] Seen 16415 samples
[2022-02-20 18:40:26] Starting data epoch 1080 in logical epoch 1080
[2022-02-20 18:40:26] [data] Shuffling data
[2022-02-20 18:40:26] [data] Done reading 16,415 sentences
[2022-02-20 18:40:26] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:40:58] Seen 16415 samples
[2022-02-20 18:40:58] Starting data epoch 1081 in logical epoch 1081
[2022-02-20 18:40:58] [data] Shuffling data
[2022-02-20 18:40:58] [data] Done reading 16,415 sentences
[2022-02-20 18:40:58] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:41:30] Seen 16415 samples
[2022-02-20 18:41:30] Starting data epoch 1082 in logical epoch 1082
[2022-02-20 18:41:30] [data] Shuffling data
[2022-02-20 18:41:30] [data] Done reading 16,415 sentences
[2022-02-20 18:41:30] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:42:01] Seen 16415 samples
[2022-02-20 18:42:01] Starting data epoch 1083 in logical epoch 1083
[2022-02-20 18:42:01] [data] Shuffling data
[2022-02-20 18:42:02] [data] Done reading 16,415 sentences
[2022-02-20 18:42:02] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:42:05] Ep. 1083 : Up. 79500 : Sen. 1,482 : Cost 1.32252479 * 1,612,487 @ 3,582 after 255,993,855 : Time 216.88s : 7434.77 words/s : L.r. 1.3459e-04
[2022-02-20 18:42:34] Seen 16415 samples
[2022-02-20 18:42:34] Starting data epoch 1084 in logical epoch 1084
[2022-02-20 18:42:34] [data] Shuffling data
[2022-02-20 18:42:34] [data] Done reading 16,415 sentences
[2022-02-20 18:42:34] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:43:05] Seen 16415 samples
[2022-02-20 18:43:05] Starting data epoch 1085 in logical epoch 1085
[2022-02-20 18:43:05] [data] Shuffling data
[2022-02-20 18:43:05] [data] Done reading 16,415 sentences
[2022-02-20 18:43:05] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:43:37] Seen 16415 samples
[2022-02-20 18:43:37] Starting data epoch 1086 in logical epoch 1086
[2022-02-20 18:43:37] [data] Shuffling data
[2022-02-20 18:43:37] [data] Done reading 16,415 sentences
[2022-02-20 18:43:37] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:44:09] Seen 16415 samples
[2022-02-20 18:44:09] Starting data epoch 1087 in logical epoch 1087
[2022-02-20 18:44:09] [data] Shuffling data
[2022-02-20 18:44:09] [data] Done reading 16,415 sentences
[2022-02-20 18:44:09] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:44:41] Seen 16415 samples
[2022-02-20 18:44:41] Starting data epoch 1088 in logical epoch 1088
[2022-02-20 18:44:41] [data] Shuffling data
[2022-02-20 18:44:41] [data] Done reading 16,415 sentences
[2022-02-20 18:44:41] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:45:13] Seen 16415 samples
[2022-02-20 18:45:13] Starting data epoch 1089 in logical epoch 1089
[2022-02-20 18:45:13] [data] Shuffling data
[2022-02-20 18:45:13] [data] Done reading 16,415 sentences
[2022-02-20 18:45:13] [data] Done shuffling 16,415 sentences to temp files
[2022-02-20 18:45:42] Ep. 1089 : Up. 80000 : Sen. 15,450 : Cost 1.32245231 * 1,612,075 @ 3,784 after 257,605,930 : Time 217.00s : 7429.01 words/s : L.r. 1.3416e-04
[2022-02-20 18:45:42] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz.orig.npz
[2022-02-20 18:45:42] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.iter80000.npz
[2022-02-20 18:45:42] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz
[2022-02-20 18:45:43] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz.optimizer.npz
[2022-02-20 18:45:46] [valid] Ep. 1089 : Up. 80000 : cross-entropy : 7.92556 : stalled 10 times (last best: 7.7043)
[2022-02-20 18:45:48] [valid] Ep. 1089 : Up. 80000 : perplexity : 1.72658 : stalled 10 times (last best: 1.70045)
[2022-02-20 18:46:04] [valid] Ep. 1089 : Up. 80000 : bleu : 87.7214 : stalled 8 times (last best: 87.8391)
[2022-02-20 18:46:05] Training finished
[2022-02-20 18:46:05] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz.orig.npz
[2022-02-20 18:46:06] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz
[2022-02-20 18:46:06] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-brmy/model0-brmy.npz.optimizer.npz

real	582m26.619s
user	950m28.466s
sys	1m10.190s
```

## Checking Output Models Folder

checking for Myanmar-Braille models ...  
translation လုပ်ဖို့အတွက် train လုပ်ခဲ့တဲ့ model တွေကို sorting လုပ်ပြီး iteration အစဉ်အလိုက် ကြည့်ရင် အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  
iteration အစီအစဉ်တွေကို looping ပတ်ဖို့အတွက် သိချင်တာမို့ sort လုပ်တဲ့အခါမှာ -V option ကို သုံးထားတယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ ls model0-mybr.*.npz | sort -V
model0-mybr.iter5000.npz
model0-mybr.iter10000.npz
model0-mybr.iter15000.npz
model0-mybr.iter20000.npz
model0-mybr.iter25000.npz
model0-mybr.iter30000.npz
model0-mybr.iter35000.npz
model0-mybr.iter40000.npz
model0-mybr.iter45000.npz
model0-mybr.iter50000.npz
model0-mybr.iter55000.npz
model0-mybr.iter60000.npz
model0-mybr.iter65000.npz
model0-mybr.iter70000.npz
model0-mybr.iter75000.npz
model0-mybr.iter80000.npz
model0-mybr.iter85000.npz
model0-mybr.iter90000.npz
model0-mybr.iter95000.npz
model0-mybr.iter100000.npz
model0-mybr.npz.optimizer.npz
model0-mybr.npz.orig.npz
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$
```

## Prepared tran-eval Shell Script for Myanmar-to-Braille

(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ cat ./tran-eval-mybr.sh  

```bash 
#!/bin/bash

## Preparation for Myanmar-MuHaung, MuHaung-Myanmar
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer Model
## 21 Feb 2022

for i in {5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,55000,60000,65000,70000,75000,80000,85000,90000,95000,100000}
do
   marian-decoder -m ./model0-mybr.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter$i.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my
   echo "Evaluation with hyp.iter$i.br, Transformer Model:" >> test0-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./hyp.iter$i.br  >> test0-results.txt
done

```

## Translation with Test Data (for 0/, my-br)

test ဒေတာကို training လုပ်ခဲ့တဲ့ မော်ဒယ် တစ်ခုချင်းစီကို pass လုပ်ပြီး translation output တွေကို hyp ဖိုင်တွေအနေနဲ့ သိမ်းထားခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ ./tran-eval-mybr.sh
...
...
...
[2022-02-21 10:19:44] Best translation 2038 : ⠞⠋⠌⠁ ⠝⠁⠆ ⠝⠪⠆ ⠞⠋⠌⠁ ⠍⠥⠂⠈⠕⠆ ⠝⠁⠆ ⠝⠪⠆ ⠍⠥⠂⠈⠕⠆ ⠲
[2022-02-21 10:19:44] Best translation 2039 : ⠍⠔⠆⠟⠪⠆ ⠈⠕ ⠲
[2022-02-21 10:19:44] Best translation 2040 : ⠣⠎⠪⠆⠣⠗⠉⠆ ⠘⠺⠮⠂ ⠅⠁ ⠁⠶ ⠞⠮ ⠈⠶⠗⠺⠑ ⠏ ⠍⠮ ⠲
[2022-02-21 10:19:44] Best translation 2041 : ⠼⠃ ⠲ ⠹⠑⠃⠣⠹⠁⠓⠁⠗⠣⠅⠣ ⠰⠶ ⠝⠋⠂⠹⠁ ⠏⠶⠆ ⠲
[2022-02-21 10:19:44] Best translation 2042 : ⠼⠁ ⠲ ⠈⠮⠂⠠⠣⠭ ⠇⠣ ⠗⠁⠹⠪ ⠃⠺⠮⠂ ⠅⠣⠃⠽⠁ ⠏ ⠗⠁⠹⠪ ⠣⠇⠬ ⠏⠺⠔⠂ ⠹⠻⠆ ⠏⠋⠆ ⠣⠍⠾ ⠅ ⠘⠻⠿⠣ ⠏ ⠲
[2022-02-21 10:19:44] Best translation 2043 : ⠕⠆⠎⠪ ⠃⠉ ⠍⠶⠆ ⠹⠋ ⠗⠣⠞⠥ ⠟⠁⠆ ⠗⠣ ⠞⠣⠞ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2044 : ⠎⠁⠏⠱ ⠗ ⠎⠁⠝⠮⠵⠔⠆ ⠣⠘⠺⠮⠂ ⠦⠅⠣⠞⠁⠣ ⠎⠣⠹⠂ ⠎⠁⠏⠱ ⠣⠘⠺⠮⠂⠣⠎⠪⠆ ⠞⠁⠺⠥⠝⠾ ⠅ ⠇⠆ ⠁⠋⠆⠈⠶ ⠨⠮⠂ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2045 : ⠍⠣⠾⠣⠗⠔ ⠹ ⠣⠷⠢⠂ ⠅⠣ ⠨⠁⠝⠪⠆ ⠫ ⠗⠣⠞⠣⠝⠁ ⠹⠉⠆⠏⠁⠆ ⠅ ⠅⠋⠞⠻⠂ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2046 : ⠼⠋ ⠲ ⠛⠋⠙⠣⠞⠃⠣ ⠰⠶ ⠁⠣⠞⠞⠣⠇⠆⠇⠆ ⠒ ⠨⠣⠞ ⠺⠥⠞⠞⠣⠽⠁⠆ ⠣⠝⠱⠣⠞⠓⠁⠆ ⠲
[2022-02-21 10:19:44] Best translation 2047 : ⠶ ⠶⠂ ⠶⠆ ⠲
[2022-02-21 10:19:44] Best translation 2048 : ⠣⠨⠥⠂ ⠽⠥ ⠞⠮⠂ ⠌⠺⠱ ⠠⠣⠭ ⠈⠮⠂ ⠩⠭ ⠟⠣⠞ ⠎⠣⠏⠁⠆ ⠏⠻ ⠡⠢ ⠰⠣⠁ ⠎⠣⠏⠁⠆ ⠨⠥⠂⠝⠭ ⠈⠮ ⠏⠱⠆ ⠗⠣ ⠍⠮ ⠲
[2022-02-21 10:19:44] Best translation 2049 : ⠣⠇⠦⠹⠣⠍⠁⠆⠾ ⠊ ⠹⠺⠱⠆ ⠾⠱ ⠙ ⠟⠣ ⠨⠮⠂ ⠗⠣ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2050 : ⠣⠃⠕⠆ ⠲
[2022-02-21 10:19:44] Best translation 2051 : ⠩⠱⠆ ⠹⠻⠆⠣⠨⠁ ⠖ ⠟⠪⠆ ⠞⠭ ⠨⠥⠂ ⠊ ⠣⠗⠣⠞ ⠇⠱⠆ ⠾⠑⠠⠣⠁ ⠫ ⠎⠥⠝⠘⠕ ⠒ ⠎⠥⠝⠍⠣ ⠒ ⠡⠔⠹⠱⠂ ⠒ ⠺⠥⠝⠇⠕⠓⠌⠣⠞ ⠇⠱⠆ ⠥⠆ ⠚ ⠹ ⠇⠅ ⠒ ⠖ ⠊ ⠣⠇⠮ ⠾⠔⠂ ⠗⠁ ⠣⠗⠣⠞ ⠫ ⠇⠱⠅ ⠹ ⠇⠅ ⠣⠹⠪⠆⠹⠪⠆ ⠝⠱ ⠟⠣ ⠅⠉ ⠊ ⠲
[2022-02-21 10:19:44] Best translation 2052 : ⠍⠪⠆⠱⠝ ⠅⠣⠇⠱⠆ ⠅ ⠹⠔⠍⠣⠞⠉⠆ ⠏ ⠲
[2022-02-21 10:19:44] Best translation 2053 : ⠺⠔⠆⠘⠋⠂ ⠙⠻⠨⠔ ⠊ ⠃⠥⠆⠹⠪⠆⠟⠻ ⠰⠣⠁ ⠞⠣⠿⠓⠱⠆⠿⠓⠱⠆ ⠡⠑⠎⠓⠁⠆ ⠇⠁⠯ ⠟⠻ ⠝ ⠹⠣⠓⠾⠣ ⠅⠉ ⠹⠻⠆ ⠓⠥ ⠊ ⠲
[2022-02-21 10:19:44] Best translation 2054 : ⠍⠣⠓⠻⠹⠣⠙⠁ ⠹⠥⠂⠨⠣⠍⠢ ⠹ ⠼ ⠹⠥⠚ ⠎⠣⠅⠁⠆ ⠅ ⠟⠁⠆ ⠿⠪⠆ ⠧ ⠹⠔⠚ ⠌ ⠊ ⠣⠈⠉⠆⠣⠿⠓⠣⠞ ⠫ ⠞⠪ ⠟⠣ ⠍ ⠇⠻⠆ ⠓ ⠍⠱⠆ ⠊ ⠲
[2022-02-21 10:19:44] Best translation 2055 : ⠼⠙ ⠲ ⠛⠋⠙⠣⠞⠃⠣ ⠰⠶ ⠾⠕⠆⠗⠕⠆ ⠵⠁⠞⠊ ⠣⠇⠦⠣⠅⠖ ⠎⠣⠹ ⠙⠣⠇⠑ ⠲
[2022-02-21 10:19:44] Best translation 2056 : ⠺⠊⠙⠱⠓⠣⠗⠭ ⠍⠔⠆⠟⠪⠆ ⠇⠆ ⠪ ⠿⠑⠹⠣⠝⠁ ⠅ ⠣⠃⠮⠹⠥ ⠿⠓⠱ ⠎⠪⠗⠔ ⠹⠝ ⠓ ⠍⠱⠆ ⠊ ⠲
[2022-02-21 10:19:44] Best translation 2057 : ⠟⠞⠚ ⠗⠴ ⠝⠱ ⠎⠔ ⠅⠋⠏⠶ ⠗ ⠗⠱ ⠗ ⠅⠋ ⠏⠪⠏⠪ ⠾⠔ ⠗⠣ ⠏⠱ ⠹⠱⠆ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2058 : ⠹⠁⠙⠣⠅⠣ ⠲ ⠲ ⠇⠥⠅⠶⠆ ⠰⠶ ⠇⠥⠅⠶⠆ ⠲
[2022-02-21 10:19:44] Best translation 2059 : ⠡⠔ ⠝ ⠈⠱⠆ ⠿⠓⠋⠆ ⠏ ⠲
[2022-02-21 10:19:44] Best translation 2060 : ⠺⠔⠆⠘⠋⠂ ⠹ ⠅⠋⠆⠗⠕⠆⠞⠋⠆ ⠅⠣⠎⠁⠆ ⠗⠣⠹⠻⠆ ⠅⠣⠎⠁⠆⠝⠪⠆ ⠭ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2061 : ⠹⠣⠝⠣⠞ ⠓ ⠗⠱⠆ ⠰⠣⠣ ⠣⠹⠪⠆ ⠎⠣⠹ ⠚ ⠅ ⠈⠪ ⠒ ⠌⠁⠆⠾⠭⠡⠔⠆ ⠒ ⠌⠣⠗⠦⠹⠪⠆ ⠎⠣⠹ ⠚ ⠗ ⠗⠻⠆ ⠞⠓⠁⠆ ⠹⠻⠆ ⠎⠁⠆⠘⠺⠮ ⠞⠭ ⠾⠕⠆ ⠓ ⠣⠙⠱⠅⠏⠮ ⠗⠣ ⠇⠍ ⠲
[2022-02-21 10:19:44] Best translation 2062 : ⠼⠁ ⠲ ⠇⠥⠂⠇⠔ ⠰⠶ ⠿⠕⠗⠺⠮ ⠹⠻⠆ ⠽⠴⠟⠁⠆ ⠲
[2022-02-21 10:19:44] Best translation 2063 : ⠥⠂⠏⠣⠍⠁ ⠝⠱⠅⠃⠋⠗⠺⠁ ⠫ ⠡⠪ ⠅⠣⠇⠱⠆ ⠞⠭ ⠓⠾⠔ ⠅ ⠨⠣⠞ ⠘⠕⠂ ⠗⠋ ⠎⠪⠆⠞ ⠺⠔⠇⠥⠂⠈⠮⠆ ⠓ ⠇⠑ ⠅⠣⠇⠆ ⠇⠱⠆ ⠌⠁⠆ ⠡⠑ ⠇⠴ ⠋⠎⠕⠂ ⠗⠣ ⠊ ⠲
[2022-02-21 10:19:44] Best translation 2064 : ⠍⠊⠨⠔ ⠰⠣⠁ ⠹⠣⠃⠔ ⠏⠔⠷⠁⠹⠮ ⠾⠕⠆⠗⠕⠆ ⠭ ⠹ ⠲
[2022-02-21 10:19:44] Best translation 2065 : ⠹⠣⠞⠏⠉ ⠹⠋⠏⠴ ⠅⠣⠃⠽⠁ ⠅ ⠈⠕ ⠟ ⠗⠣⠶ ⠲
[2022-02-21 10:19:44] Best translation 2066 : ⠾⠑ ⠞⠭ ⠨⠣⠞ ⠒ ⠣⠇⠶⠆⠃⠥⠂⠗⠁⠆ ⠅⠮ ⠞⠭ ⠃⠪⠵⠣⠝⠁ ⠓⠾⠣ ⠲
[2022-02-21 10:19:44] Best translation 2067 : ⠺⠥⠞⠁⠥⠂ ⠅⠁⠍⠣⠛⠉ ⠒ ⠌⠺⠱⠎⠣ ⠗ ⠟⠉ ⠹⠻⠆⠣⠨⠁ ⠒ ⠁⠗⠉ ⠅ ⠿⠓⠣⠞ ⠝ ⠨⠮⠂ ⠸⠣⠣ ⠏ ⠹ ⠩⠺⠱⠝⠋⠆⠩⠔ ⠿ ⠲
[2022-02-21 10:19:44] Best translation 2068 : ⠣⠃⠕⠆⠟⠪⠆ ⠗⠻⠆ ⠅⠶⠍⠣⠇⠱⠆ ⠗⠻⠆ ⠹⠣⠞⠃⠔⠷⠥⠂ ⠿ ⠚ ⠒ ⠁⠝⠋⠙⠁ ⠿ ⠚ ⠒ ⠥⠆⠃⠣⠷⠶ ⠶ ⠅⠋⠞⠻⠂⠏⠣⠇⠔ ⠶ ⠚ ⠸⠽⠴ ⠘⠥⠆ ⠗⠣⠶ ⠝⠱⠂⠇⠮ ⠅⠣⠞⠮⠆ ⠅⠣ ⠸⠣⠮⠆ ⠝⠮⠂ ⠁⠺⠑ ⠟ ⠞⠮ ⠲
[2022-02-21 10:19:44] Best translation 2069 : ⠓⠋ ⠣⠍⠥⠣⠽ ⠝⠮⠂ ⠈⠕ ⠝ ⠟⠣ ⠗⠮⠂⠇⠁⠆ ⠲
[2022-02-21 10:19:44] Best translation 2070 : ⠗⠺⠁ ⠁⠮⠆ ⠰⠣⠁ ⠣⠷⠢⠂ ⠏⠺⠮⠆ ⠩ ⠹⠇ ⠲
[2022-02-21 10:19:44] Best translation 2071 : ⠅⠺⠁ ⠵⠋⠃⠥⠙⠪⠏⠁ ⠰⠣⠁ ⠾⠋⠍⠁ ⠅ ⠝ ⠍⠂ ⠇⠥ ⠋ ⠏⠻ ⠹⠱⠆ ⠏⠁ ⠃⠥⠆ ⠓ ⠅⠥⠆⠞⠕⠂ ⠞ ⠍⠥ ⠊ ⠲
[2022-02-21 10:19:45] Best translation 2072 : ⠼⠉ ⠲ ⠛⠋⠙⠣⠞⠃⠣ ⠹⠥ ⠅ ⠹⠣⠞⠰⠣⠣⠞ ⠞⠓⠁⠆ ⠞⠮⠂ ⠍⠱⠆⠨⠥⠝⠆ ⠞⠺⠱ ⠍⠱⠆ ⠿⠪⠆ ⠿⠻⠆⠞⠁ ⠞⠺⠱ ⠋ ⠍⠱⠂ ⠗⠣⠶ ⠰⠣⠣⠞⠎⠥⠂ ⠰⠣⠁ ⠗⠱⠆⠰⠣⠣⠞ ⠇⠁ ⠟⠣ ⠗⠣ ⠍⠮⠝⠻ ⠲
[2022-02-21 10:19:45] Best translation 2073 : ⠼⠋ ⠲ ⠣⠟⠱ ⠰⠶ ⠾⠋⠍⠁ ⠿⠪ ⠭⠞⠮ ⠙⠱⠹⠣ ⠲
[2022-02-21 10:19:45] Best translation 2074 : ⠅⠮⠂⠗⠮⠂ ⠒ ⠡⠪⠆⠍⠥⠝⠆ ⠒ ⠎⠁⠗⠔⠆ ⠒ ⠹⠑⠹⠱ ⠒ ⠣⠟⠔⠂ ⠒ ⠦⠎⠁ ⠲
[2022-02-21 10:19:45] Best translation 2075 : ⠩⠱⠆ ⠹⠻⠆⠣⠨⠁ ⠃⠁⠗⠁⠝⠣⠹⠪ ⠍⠔⠆ ⠞⠭⠏⠁⠆ ⠊ ⠹⠁⠆⠞⠻ ⠹ ⠞⠑⠅⠣⠹⠕ ⠿⠪ ⠫ ⠏⠔⠷⠁ ⠹⠔⠟⠁⠆ ⠝⠱⠎⠔ ⠞⠭ ⠝⠱⠂ ⠫ ⠣⠍⠮⠕ ⠞⠭ ⠽⠴ ⠸⠣⠋⠆ ⠞⠓⠁⠆ ⠹⠻⠆ ⠠⠣⠋⠆ ⠅ ⠎⠁⠆ ⠇⠕ ⠹ ⠗ ⠞⠭ ⠈⠦ ⠽⠥⠯ ⠎⠁⠆ ⠊ ⠲
[2022-02-21 10:19:45] Best translation 2076 : ⠎⠢⠂ ⠟⠪⠆ ⠾⠖ ⠟⠪⠆ ⠒ ⠗⠱⠅ ⠟⠪⠆ ⠞⠻⠆ ⠞⠶ ⠲
[2022-02-21 10:19:45] Best translation 2077 : ⠏⠁⠇⠊ ⠎⠁⠏⠱ ⠟⠋⠆⠛⠋⠾ ⠅⠣⠃⠽⠁ ⠇⠔⠅⠁⠾ ⠅ ⠇⠮⠞⠪ ⠈⠣⠗⠁⠞ ⠁⠋ ⠞⠺ ⠈⠑⠇⠑ ⠈⠪⠆⠏⠥⠆ ⠿⠪⠆ ⠹⠑⠅⠣⠞⠣ ⠎⠁⠏⠱⠾ ⠅ ⠿⠪⠆⠎⠯ ⠈⠣⠗⠁⠞ ⠁⠋ ⠞⠺ ⠈⠑⠇⠑ ⠈⠪⠆⠏⠥⠆ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2078 : ⠼⠉ ⠲ ⠦ ⠞⠋⠞⠖⠆ ⠅⠁⠗⠋ ⠹⠻⠆ ⠡⠋ ⠟⠮ ⠟⠪⠆⠾ ⠞⠺ ⠞⠓⠁⠆⠩ ⠹⠂ ⠞⠊⠗⠭⠈⠋⠾ ⠊ ⠣⠍ ⠅ ⠘⠻⠿⠣ ⠏ ⠲ ⠣⠃⠮⠳ ⠁⠕⠙ ⠞⠓⠁⠆ ⠗⠣ ⠹⠝ ⠲
[2022-02-21 10:19:45] Best translation 2079 : ⠪ ⠅⠣⠃⠽⠁ ⠅ ⠗⠱⠆⠹⠥ ⠥⠆⠟⠔⠥⠂ ⠹ ⠾⠋⠍⠁ ⠠⠣⠭ ⠼⠁ ⠁ ⠉ ⠑ ⠤ ⠼⠁ ⠃ ⠚ ⠚ ⠶ ⠅⠗ ⠠⠣⠭ ⠼⠁ ⠛ ⠛ ⠤ ⠼⠁ ⠁ ⠓ ⠉ ⠓ ⠶ ⠣⠞⠺⠑ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠁⠈⠕ ⠭ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2080 : ⠼⠉ ⠁ ⠲ ⠴⠍⠱⠂ ⠰⠶ ⠈⠔⠡⠔ ⠎⠔⠆⠎⠁⠆ ⠹ ⠲ ⠠⠣⠣⠇⠉⠆⠹⠺⠔⠆ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2081 : ⠼⠁ ⠲ ⠣⠞⠁⠅⠥⠆ ⠡ ⠈⠕⠹ ⠰⠣⠁ ⠣⠃⠮ ⠝⠪⠆ ⠲
[2022-02-21 10:19:45] Best translation 2082 : ⠪ ⠹⠥ ⠊ ⠝⠺⠁⠆⠾ ⠋⠓⠦ ⠏ ⠲
[2022-02-21 10:19:45] Best translation 2083 : ⠼⠉ ⠲ ⠴⠏⠁ ⠣⠇⠔⠅⠁ ⠚ ⠹ ⠍⠙ ⠹⠻⠆ ⠣⠟ ⠗ ⠈⠑⠎⠣⠞ ⠹⠉⠆ ⠞⠓⠁⠆ ⠿⠪⠆ ⠣⠃⠮⠳ ⠼ ⠣⠇⠔⠅⠁ ⠾⠴ ⠟⠶⠆ ⠩⠔⠆⠿⠣ ⠏ ⠲
[2022-02-21 10:19:45] Best translation 2084 : ⠾⠕⠂ ⠞⠶ ⠾⠑⠠⠣⠁ ⠅⠣ ⠗⠱ ⠗⠶⠆ ⠍⠢⠆⠍⠣ ⠁⠺⠑ ⠈⠕ ⠗⠋ ⠎⠣⠅⠁⠆ ⠰⠣⠁ ⠲
[2022-02-21 10:19:45] Best translation 2085 : ⠎⠁ ⠣⠗⠱⠆⠣⠹⠁⠆ ⠣⠇⠱⠆⠞⠓⠁⠆ ⠏ ⠲
[2022-02-21 10:19:45] Best translation 2086 : ⠟⠬⠁⠪⠆⠗⠕⠆ ⠎⠱⠞⠪⠞ ⠹ ⠾⠣⠞⠎⠺⠁⠿ ⠊ ⠈⠋⠞⠩⠔ ⠅ ⠞⠓⠁⠏⠣⠝⠁⠯ ⠞⠮ ⠞⠓⠁⠆ ⠵ ⠞⠋⠨⠕⠆ ⠟⠪⠆ ⠹ ⠓ ⠽⠉⠟⠪ ⠅⠕⠆⠅⠺⠮ ⠟ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2087 : ⠅⠺⠮⠇⠥⠝ ⠹⠂ ⠣⠡⠢ ⠣⠁⠊ ⠣⠈⠑⠍⠣⠿⠣⠞ ⠎⠁ ⠗⠱⠆ ⠨⠮⠂ ⠹⠥ ⠭ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2088 : ⠼⠃ ⠚ ⠁ ⠚ ⠤ ⠼⠃ ⠚ ⠁ ⠁ ⠏⠔⠷⠁⠹⠔ ⠠⠣⠭ ⠲
[2022-02-21 10:19:45] Best translation 2089 : ⠎⠣ ⠲
[2022-02-21 10:19:45] Best translation 2090 : ⠼⠛ ⠲ ⠹⠪⠞⠔⠆⠟⠥⠞ ⠞⠺ ⠒ ⠏⠣⠇⠔ ⠈⠱⠆ ⠍⠕⠆ ⠒ ⠗⠺⠁⠹⠥⠝⠆⠿⠓⠕⠆ ⠲
[2022-02-21 10:19:45] Best translation 2091 : ⠼⠉ ⠊ ⠲ ⠽⠣⠞⠍⠁⠆ ⠰⠶ ⠝⠋⠆⠞⠺⠔⠆ ⠹⠉⠆ ⠣⠗⠕⠆ ⠩⠱ ⠽⠣⠞ ⠟⠪⠆ ⠲
[2022-02-21 10:19:45] Best translation 2092 : ⠙⠦⠨⠣ ⠏ ⠏⠮⠆ ⠹⠥⠌⠮⠡⠔⠆ ⠗⠱ ⠨⠮⠆⠞⠋ ⠓⠌⠁⠆ ⠏ ⠕⠝⠆ ⠇⠕⠂ ⠿⠻⠆ ⠿⠪⠆ ⠣⠅⠥⠣⠷⠪ ⠞⠶⠆ ⠗⠣ ⠞⠮ ⠲
[2022-02-21 10:19:45] Best translation 2093 : ⠙⠗⠁ ⠞⠺ ⠼ ⠿⠪ ⠅⠣⠇⠱⠆ ⠅⠣ ⠎⠭ ⠋ ⠞⠬ ⠃⠮⠆ ⠟⠞⠚ ⠃⠥⠂⠗⠔ ⠅ ⠘⠋⠆ ⠹⠺⠁⠆ ⠏ ⠲
[2022-02-21 10:19:45] Best translation 2094 : ⠅⠣⠇⠣⠞⠑⠹⠋ ⠗⠣⠞⠥ ⠏⠯ ⠇⠁ ⠹⠻⠆ ⠣⠙⠱⠅⠏⠮ ⠞⠭ ⠾⠕⠆ ⠇⠆ ⠩ ⠹⠱⠆ ⠊ ⠲
[2022-02-21 10:19:45] Best translation 2095 : ⠣⠩ ⠍⠔⠆⠟⠪⠆ ⠒ ⠟⠥ ⠊ ⠣⠍ ⠅⠁⠆ ⠹⠥⠂⠺⠥⠝⠝⠣⠹⠁⠍⠣ ⠞⠪⠆ ⠲
[2022-02-21 10:19:45] Best translation 2096 : ⠋⠞⠻⠇⠻⠆⠃⠣ ⠇⠥⠿⠕⠟⠪⠆ ⠎⠥⠝ ⠡⠔ ⠩⠁ ⠵ ⠟⠻⠷⠁ ⠅⠋⠆ ⠟⠻⠷⠁ ⠅⠋⠆ ⠞⠓⠁⠆ ⠓⠋ ⠞⠥ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2097 : ⠾⠴⠃⠑ ⠈⠪ ⠙ ⠨⠣⠗⠪⠆ ⠠⠣⠔ ⠞⠺⠱⠂ ⠇⠢⠂ ⠝⠮ ⠅⠣⠡⠔ ⠏⠣⠇⠺⠱ ⠹⠋⠇⠺⠔ ⠕⠆⠎⠪ ⠠⠣⠻⠆ ⠁⠶⠅⠁ ⠝⠮⠂ ⠍⠣⠝⠻⠆ ⠲
[2022-02-21 10:19:45] Best translation 2098 : ⠾⠋⠍⠁ ⠃⠥⠂⠗⠔ ⠚ ⠅⠕⠂ ⠁⠪⠆ ⠅⠕⠂ ⠝⠋⠆ ⠣⠭ ⠝⠴⠈⠉⠆ ⠞⠪⠁⠶ ⠎⠋⠾⠋⠆ ⠨⠮⠂ ⠟⠣ ⠹⠂ ⠝⠋⠆⠞⠻ ⠟⠪⠆ ⠇⠆ ⠭ ⠹ ⠲
[2022-02-21 10:19:45] Best translation 2099 : ⠻⠆ ⠻⠂ ⠻ ⠲
[2022-02-21 10:19:45] Best translation 2100 : ⠼⠉ ⠲ ⠅⠋⠙⠣ ⠰⠶ ⠣⠏⠖⠆ ⠒ ⠣⠨⠋⠆ ⠲
[2022-02-21 10:19:45] Best translation 2101 : ⠞⠔ ⠏ ⠹ ⠿ ⠲
[2022-02-21 10:19:46] Best translation 2102 : ⠏⠋⠆⠅⠣⠇⠱⠆⠾ ⠏⠺⠔⠂ ⠞⠻⠂ ⠍ ⠘⠥⠆⠞⠋ ⠭⠞⠮ ⠡⠪ ⠒ ⠝⠱⠡⠪ ⠰⠣⠁ ⠩⠺⠱⠗⠪ ⠇⠶⠆ ⠌⠁ ⠚ ⠎⠁⠹⠔⠟⠶⠆ ⠲
[2022-02-21 10:19:46] Best translation 2103 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠲
[2022-02-21 10:19:46] Best translation 2104 : ⠼⠋ ⠲ ⠾⠋⠍⠁⠂ ⠗⠕⠆⠗⠁ ⠡ ⠅⠣⠎⠁⠆ ⠝⠪⠆ ⠹ ⠾⠋⠍⠁ ⠚ ⠣⠞⠺⠑ ⠛⠉⠽⠥ ⠘⠺⠮⠗⠁ ⠭ ⠏ ⠹⠇ ⠲
[2022-02-21 10:19:46] Best translation 2105 : ⠣⠗⠱⠆ ⠋⠓⠦ ⠓ ⠸⠽⠴ ⠹ ⠅ ⠟⠬ ⠞ ⠋ ⠍⠥ ⠲
[2022-02-21 10:19:46] Best translation 2106 : ⠟⠋⠆⠍⠁ ⠿⠻⠩⠺⠔⠯ ⠒ ⠅⠦⠅⠥⠂⠞⠻⠆ ⠇⠱⠆⠎⠁⠆ ⠣⠞⠏⠱ ⠒ ⠚⠍⠱⠍⠱ ⠲
[2022-02-21 10:19:46] Best translation 2107 : ⠈⠱⠆⠟⠻⠆ ⠲
[2022-02-21 10:19:46] Best translation 2108 : ⠼ ⠹⠥⠂ ⠝⠺⠁⠆ ⠋⠓⠦ ⠓ ⠈⠕ ⠊ ⠲
[2022-02-21 10:19:46] Best translation 2109 : ⠹⠥ ⠊ ⠏⠁⠆ ⠅⠣⠇⠱⠆⠾ ⠒ ⠡⠱ ⠿⠓⠁⠆ ⠇⠑ ⠿⠓⠁⠆ ⠅⠣⠇⠱⠆⠾ ⠒ ⠝⠁⠆⠗⠺⠑ ⠅⠣⠇⠱⠆⠾ ⠰⠣⠁ ⠺⠁⠯ ⠇⠁ ⠟ ⠃ ⠹ ⠲
[2022-02-21 10:19:46] Best translation 2110 : ⠶ ⠎⠣ ⠶ ⠣⠍⠊ ⠣⠘⠣ ⠚ ⠅ ⠇⠦⠟⠺⠱⠆ ⠡ ⠿⠓ ⠍⠙ ⠹⠻⠆ ⠣⠟⠕⠆⠟⠵ ⠚ ⠅ ⠗⠣⠩⠊ ⠝ ⠹⠝ ⠲
[2022-02-21 10:19:46] Best translation 2111 : ⠺⠔⠆⠘⠋⠂ ⠲ ⠲ ⠇⠣⠿⠱⠂ ⠟⠻ ⠼⠋ ⠗⠑ ⠏ ⠘⠱⠘⠱ ⠲
[2022-02-21 10:19:46] Best translation 2112 : ⠡⠖ ⠡⠖⠂ ⠡⠖⠆ ⠲
[2022-02-21 10:19:46] Best translation 2113 : ⠹⠥ ⠹ ⠝⠍ ⠗ ⠇⠬ ⠶ ⠿⠓⠥ ⠹ ⠒ ⠡⠻⠆ ⠹ ⠒ ⠸⠣⠣ ⠹ ⠒ ⠡⠻⠆ ⠹ ⠸⠣⠣ ⠹ ⠗ ⠣⠓⠾⠣ ⠥⠆⠹⠁⠕⠆ ⠇⠔ ⠌⠮ ⠱ ⠞⠣⠞ ⠹⠥ ⠲
[2022-02-21 10:19:46] Best translation 2114 : ⠼⠃ ⠲ ⠇⠱⠆ ⠍⠶⠂ ⠎⠋⠟⠶⠆ ⠞⠺ ⠣⠏⠽⠄ ⠾⠕⠆ ⠚ ⠹ ⠍⠙ ⠹⠻⠆ ⠝⠱⠗⠁ ⠣⠹⠪⠆⠹⠪⠆ ⠫ ⠏⠴ ⠝⠱ ⠞⠋⠎⠓⠁⠈⠔ ⠱ ⠟ ⠹⠝ ⠲
[2022-02-21 10:19:46] Best translation 2115 : ⠣⠾⠕⠆ ⠨⠥⠂⠝⠭ ⠈⠑ ⠞⠖⠶ ⠋ ⠿⠑ ⠹⠻⠆ ⠡⠭ ⠡ ⠹ ⠭ ⠃ ⠹⠞ ⠲
[2022-02-21 10:19:46] Best translation 2116 : ⠋⠞⠻⠇⠻⠆⠃⠣ ⠹⠔⠟⠋ ⠲
[2022-02-21 10:19:46] Best translation 2117 : ⠼⠣⠨⠁ ⠏⠥⠂⠎⠥⠝ ⠅⠣ ⠣⠈⠺⠱ ⠃⠽⠖⠆ ⠣⠃⠮⠳ ⠣⠟⠥ ⠅ ⠖ ⠫ ⠋ ⠸⠣⠥⠞ ⠃⠮⠆ ⠪ ⠨⠋⠞⠑⠏⠔ ⠙ ⠈⠶⠽⠥ ⠨⠮⠂ ⠹⠝ ⠓ ⠍⠱⠆ ⠃ ⠊ ⠲
[2022-02-21 10:19:46] Best translation 2118 : ⠣⠍ ⠙⠣⠁⠺⠱⠆ ⠲
[2022-02-21 10:19:46] Best translation 2119 : ⠍⠋⠞⠣⠇⠱⠆ ⠞⠑⠅⠣⠹⠕ ⠰⠣⠣ ⠇⠱⠂⠇⠁ ⠗⠱⠆ ⠣⠘⠺⠮⠂ ⠲
[2022-02-21 10:19:46] Best translation 2120 : ⠓⠦⠅⠮⠂ ⠒ ⠇⠱⠆ ⠈⠮ ⠇⠴ ⠈⠕ ⠏ ⠞⠻⠂ ⠲
[2022-02-21 10:19:46] Best translation 2121 : ⠹⠥ ⠸ ⠌⠁⠆ ⠘⠋⠆ ⠁⠺⠑ ⠹⠣⠞⠣⠞ ⠶ ⠹⠣ ⠞⠮⠂ ⠶ ⠲
[2022-02-21 10:19:46] Best translation 2122 : ⠪ ⠇⠆ ⠿⠇⠶⠆ ⠁⠆ ⠅⠶⠆⠡⠪⠆ ⠍⠔⠛⠣⠇⠁ ⠞⠭ ⠟⠢ ⠭ ⠹⠞ ⠲
[2022-02-21 10:19:46] Best translation 2123 : ⠥⠂⠏⠮ ⠒ ⠕⠆⠎⠁⠆⠘⠑ ⠒ ⠽⠥⠝⠆⠍⠣ ⠒ ⠣⠏⠁ ⠡⠣ ⠒ ⠾⠔⠆ ⠰⠣⠁ ⠉⠆⠨⠥⠝ ⠒ ⠙⠁⠆ ⠰⠣⠁ ⠍⠕⠆⠟⠕⠆ ⠲
[2022-02-21 10:19:46] Best translation 2124 : ⠗⠣⠺⠱ ⠒ ⠃⠪⠵⠣⠝⠁ ⠒ ⠃⠽⠁⠈⠉ ⠒ ⠇⠱⠅⠿⠁ ⠱⠆ ⠒ ⠗⠣⠞⠥⠂ ⠲
[2022-02-21 10:19:46] Best translation 2125 : ⠅⠣⠞⠞⠪⠏⠁ ⠗ ⠲
[2022-02-21 10:19:46] Best translation 2126 : ⠾⠋⠍⠁ ⠃⠥⠂⠗⠔ ⠏⠁ ⠞⠍ ⠹⠻⠆⠣⠨⠁ ⠞⠺ ⠇⠆ ⠩⠺⠱ ⠈⠪⠆⠿⠓⠥ ⠹⠣⠃⠻⠆ ⠙ ⠒ ⠗⠱⠓⠷⠊ ⠗ ⠸⠣⠢⠂ ⠹⠣⠇⠕ ⠓⠥⠯ ⠰⠣⠣⠞⠞⠋⠆⠞⠔ ⠨⠮⠂ ⠹ ⠲
[2022-02-21 10:19:46] Best translation 2127 : ⠨⠺⠱ ⠝⠱⠅⠃⠋⠗⠺⠁ ⠨⠺⠱⠆ ⠲
[2022-02-21 10:19:46] Best translation 2128 : ⠥⠆⠊ ⠹ ⠣⠍⠣⠗⠣⠏⠥⠗⠣ ⠾⠕⠂ ⠾⠴⠯ ⠰⠣⠣ ⠏⠕⠆ ⠁⠮ ⠒ ⠡⠪ ⠁⠮ ⠚ ⠅ ⠣⠗⠶⠆⠣⠺⠮ ⠿⠥⠂ ⠹⠻⠆ ⠏⠕⠆ ⠾⠔⠆⠹⠁⠆⠯ ⠭⠗⠁ ⠏⠭⠎⠪⠆ ⠦⠎⠁ ⠟⠺⠮⠺⠣ ⠡⠋⠆⠹⠁ ⠹ ⠲
[2022-02-21 10:19:46] Best translation 2129 : ⠨⠑⠈⠭ ⠣⠘⠺⠔⠂ ⠲
[2022-02-21 10:19:46] Best translation 2130 : ⠼⠉ ⠲ ⠘⠺⠁ ⠗⠣ ⠗⠁ ⠰⠶ ⠎⠥⠂⠎⠪⠆ ⠡ ⠋ ⠩ ⠒ ⠅⠺⠮⠆ ⠿⠓⠁ ⠁⠺⠑ ⠑ ⠲
[2022-02-21 10:19:46] Best translation 2131 : ⠍⠊⠍⠊ ⠅⠕⠞⠖ ⠣⠹⠋⠝⠱⠣⠹⠋⠞⠓⠁⠆ ⠿⠓ ⠗⠥⠞⠈⠕ ⠇⠱⠂⠟⠔⠂ ⠏ ⠲
[2022-02-21 10:19:46] Best translation 2132 : ⠶ ⠨⠣ ⠶ ⠞⠭⠥⠂⠞⠥⠂ ⠸ ⠤⠤⠤⠤⠤⠤ ⠎⠪ ⠟⠁⠾⠔⠂ ⠏ ⠹ ⠲
[2022-02-21 10:19:46] Best translation 2133 : ⠷⠶⠏⠔⠹⠁⠗⠺⠁ ⠿⠓⠥⠆ ⠾⠕⠂⠝⠮ ⠼⠁ ⠉ ⠙ ⠑ ⠨⠥⠂ ⠒ ⠞⠋⠨⠥⠆ ⠇⠣⠈⠋⠆ ⠼⠁ ⠗⠑ ⠹⠥⠌⠮⠡⠔⠆ ⠗⠪⠞⠥ ⠹⠥⠌⠮⠡⠔⠆ ⠁⠋⠙ ⠎⠱⠆⠠⠣⠮⠆ ⠎⠁⠗⠱⠆⠇⠬ ⠏ ⠹ ⠲
[2022-02-21 10:19:46] Best translation 2134 : ⠼⠓ ⠲ ⠁⠆⠹⠋ ⠰⠶ ⠋ ⠗⠣ ⠋ ⠝⠱ ⠋ ⠭ ⠋ ⠝⠱ ⠁⠆⠁⠦ ⠟⠕⠆⠏⠋⠆ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2135 : ⠿⠁⠆⠗⠪ ⠹⠁ ⠈⠶⠽⠥ ⠟⠣ ⠡⠱ ⠓ ⠈⠕⠯ ⠿⠁⠆⠗⠪ ⠅ ⠈⠶⠽⠥ ⠎ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠫ ⠣⠏⠴⠺⠣ ⠠⠣⠭ ⠘⠑ ⠅ ⠇⠢⠆⠹⠦ ⠿⠪⠆ ⠰⠣⠣ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠸⠣⠣⠎ ⠹⠻⠆ ⠅⠋⠃⠣⠇⠁ ⠡⠪ ⠟⠕⠆ ⠅ ⠟⠭ ⠿⠪⠆⠸ ⠼ ⠅⠋⠃⠣⠇⠁ ⠟⠕⠆ ⠎⠣ ⠫ ⠿⠁⠆⠗⠪ ⠿⠓ ⠝⠮⠸⠣⠮⠂ ⠟⠕⠆ ⠎⠣ ⠅ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠏⠴ ⠺⠣ ⠟⠕⠆ ⠓⠶⠆ ⠎⠣ ⠞⠭⠘⠑ ⠗ ⠞⠱⠂ ⠿⠪⠆ ⠎⠔⠆⠌⠮ ⠿⠪⠆ ⠹⠺⠔⠆⠯ ⠞⠓⠁⠆ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠺⠣ ⠅⠣ ⠏⠥⠂⠗⠺⠑ ⠅⠣ ⠒ ⠏⠕⠆⠗⠺⠣ ⠒ ⠶⠕⠅ ⠅ ⠎⠁⠆⠹⠴ ⠎ ⠡ ⠓⠌⠁ ⠒ ⠏⠥⠂⠗⠺⠑ ⠒ ⠟⠔⠝⠪ ⠒ ⠞⠉⠏⠉ ⠚ ⠅ ⠞⠱⠂ ⠝⠱⠗⠁ ⠫ ⠞⠱⠂ ⠝⠱⠗⠁ ⠫ ⠞⠱⠂ ⠡⠪ ⠑ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠊ ⠲
[2022-02-21 10:19:47] Best translation 2136 : ⠟⠞⠚ ⠗ ⠗⠔⠆⠠⠣⠪⠆ ⠹⠻⠆ ⠣⠟⠣⠽ ⠏⠔ ⠭ ⠇⠔⠂ ⠅⠣⠎⠁⠆ ⠒ ⠟⠞⠚ ⠞⠖⠆⠈⠣ ⠰⠣⠣ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠞⠚ ⠟⠪⠂⠾⠔ ⠨⠋⠎⠁⠆ ⠹⠣⠇⠕ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠶⠆ ⠿⠁⠞⠁ ⠟⠪⠆ ⠊ ⠇⠑⠈⠭ ⠰⠣⠣ ⠗⠱⠆ ⠗⠣ ⠍ ⠲
[2022-02-21 10:19:47] Best translation 2137 : ⠎⠣⠅⠁⠆⠇⠉⠆ ⠅⠣⠇⠱⠆ ⠞⠺⠱ ⠎⠪ ⠅⠁ ⠗⠮ ⠗⠥⠞⠈⠕ ⠗⠱⠆ ⠟⠪⠂ ⠍⠮ ⠲
[2022-02-21 10:19:47] Best translation 2138 : ⠍⠣⠾⠣⠗⠔ ⠚ ⠣⠷⠢⠂ ⠅⠣ ⠹⠂ ⠨⠱⠞⠄ ⠅⠣ ⠣⠏⠽⠄ ⠋ ⠏⠻ ⠹⠱⠆ ⠏ ⠣⠷⠢⠂ ⠍⠔⠆⠹⠣⠍⠪⠆⠾ ⠹ ⠏⠺⠮⠆⠨⠔⠆ ⠅ ⠏⠴ ⠶ ⠍⠊⠍⠊ ⠊ ⠏⠔⠅ ⠣⠹⠋ ⠗ ⠟⠕⠆⠎⠁⠆⠯ ⠈⠕ ⠟ ⠗⠣ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2139 : ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠒ ⠃⠁⠹⠁⠿⠋ ⠺⠥⠞⠁⠥⠂⠾ ⠭⠞⠮ ⠗⠁ ⠎⠱⠅⠁⠮⠆ ⠒ ⠌⠁⠆⠾⠭⠡⠔⠆ ⠒ ⠥⠆⠃⠣⠷⠶ ⠒ ⠱⠝⠩⠔⠍⠣ ⠒ ⠣⠺⠥⠞⠸⠽⠻ ⠒ ⠝⠁⠆⠇⠪ ⠒ ⠗⠮⠆⠗⠮⠆⠺⠔⠝⠂⠺⠔⠂ ⠎⠣⠹ ⠚ ⠰⠣⠁ ⠁⠔⠩⠁⠆ ⠹⠻⠆ ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠭ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2140 : ⠩⠱⠆⠨⠭ ⠎⠭⠹⠪ ⠞⠭ ⠥⠆ ⠊ ⠃⠣⠺⠣ ⠞⠭ ⠎⠱⠅ ⠞⠭ ⠏⠖⠆ ⠅ ⠁⠔⠓⠣⠞ ⠹⠻⠆ ⠖⠆⠡⠔⠆ ⠭ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠓⠌⠑⠾ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-02-21 10:19:47] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-02-21 10:19:47] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠏⠋⠆⠈⠕⠆⠞⠋⠆ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-02-21 10:19:47] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠡⠓⠌⠁ ⠇⠑⠝⠁⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠣⠇⠶⠆⠞ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-02-21 10:19:47] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-02-21 10:19:47] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏⠁ ⠇⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠎⠪⠆⠞ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-02-21 10:19:48] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠙⠶⠆⠏⠶ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-02-21 10:19:48] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-02-21 10:19:48] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠍⠥⠞⠮ ⠣⠾⠣⠟⠕⠆⠓⠌⠁ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-02-21 10:19:48] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠞⠁⠏ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-02-21 10:19:48] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-02-21 10:19:48] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-02-21 10:19:48] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-02-21 10:19:48] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-02-21 10:19:48] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏⠁ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-02-21 10:19:48] Best translation 2160 : ⠺⠔⠆⠘⠋⠂ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-02-21 10:19:48] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-02-21 10:19:48] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-02-21 10:19:48] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-02-21 10:19:48] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-02-21 10:19:48] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-02-21 10:19:48] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠍⠣⠹⠴⠹⠉⠆ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-02-21 10:19:48] Total time: 68.72124s wall
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$

```

## Check the Results

BLEU Score တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ cat test0-results.txt 
Evaluation with hyp.iter5000.br, Transformer Model:
BLEU = 82.76, 95.5/90.8/86.2/81.9 (BP=0.936, ratio=0.938, hyp_len=27007, ref_len=28803)
Evaluation with hyp.iter10000.br, Transformer Model:
BLEU = 83.44, 95.6/91.0/86.7/82.6 (BP=0.939, ratio=0.941, hyp_len=27102, ref_len=28803)
Evaluation with hyp.iter15000.br, Transformer Model:
BLEU = 84.25, 95.5/90.9/86.5/82.4 (BP=0.950, ratio=0.951, hyp_len=27398, ref_len=28803)
Evaluation with hyp.iter20000.br, Transformer Model:
BLEU = 84.68, 95.5/90.8/86.4/82.2 (BP=0.956, ratio=0.957, hyp_len=27553, ref_len=28803)
Evaluation with hyp.iter25000.br, Transformer Model:
BLEU = 84.88, 95.5/90.8/86.4/82.3 (BP=0.958, ratio=0.959, hyp_len=27611, ref_len=28803)
Evaluation with hyp.iter30000.br, Transformer Model:
BLEU = 85.32, 95.4/90.6/86.2/82.0 (BP=0.965, ratio=0.966, hyp_len=27811, ref_len=28803)
Evaluation with hyp.iter35000.br, Transformer Model:
BLEU = 85.60, 95.3/90.4/85.9/81.6 (BP=0.971, ratio=0.972, hyp_len=27989, ref_len=28803)
Evaluation with hyp.iter40000.br, Transformer Model:
BLEU = 85.68, 95.3/90.4/85.8/81.6 (BP=0.972, ratio=0.973, hyp_len=28017, ref_len=28803)
Evaluation with hyp.iter45000.br, Transformer Model:
BLEU = 85.70, 95.3/90.4/86.0/81.7 (BP=0.972, ratio=0.972, hyp_len=27995, ref_len=28803)
Evaluation with hyp.iter50000.br, Transformer Model:
BLEU = 86.03, 95.2/90.3/85.8/81.5 (BP=0.977, ratio=0.977, hyp_len=28139, ref_len=28803)
Evaluation with hyp.iter55000.br, Transformer Model:
BLEU = 85.94, 95.2/90.2/85.6/81.3 (BP=0.978, ratio=0.978, hyp_len=28164, ref_len=28803)
Evaluation with hyp.iter60000.br, Transformer Model:
BLEU = 86.23, 95.2/90.2/85.5/81.1 (BP=0.982, ratio=0.982, hyp_len=28284, ref_len=28803)
Evaluation with hyp.iter65000.br, Transformer Model:
BLEU = 86.37, 95.1/90.2/85.5/81.1 (BP=0.983, ratio=0.983, hyp_len=28326, ref_len=28803)
Evaluation with hyp.iter70000.br, Transformer Model:
BLEU = 86.46, 95.1/90.0/85.3/80.9 (BP=0.986, ratio=0.986, hyp_len=28408, ref_len=28803)
Evaluation with hyp.iter75000.br, Transformer Model:
BLEU = 86.38, 95.1/90.1/85.4/81.0 (BP=0.984, ratio=0.985, hyp_len=28359, ref_len=28803)
Evaluation with hyp.iter80000.br, Transformer Model:
BLEU = 86.40, 95.1/90.1/85.4/81.0 (BP=0.985, ratio=0.985, hyp_len=28366, ref_len=28803)
Evaluation with hyp.iter85000.br, Transformer Model:
BLEU = 86.66, 95.1/90.0/85.3/80.8 (BP=0.989, ratio=0.989, hyp_len=28490, ref_len=28803)
Evaluation with hyp.iter90000.br, Transformer Model:
BLEU = 86.67, 95.0/89.9/85.2/80.8 (BP=0.990, ratio=0.990, hyp_len=28506, ref_len=28803)
Evaluation with hyp.iter95000.br, Transformer Model:
BLEU = 86.73, 95.1/89.9/85.2/80.7 (BP=0.990, ratio=0.990, hyp_len=28527, ref_len=28803)
Evaluation with hyp.iter100000.br, Transformer Model:
BLEU = 86.64, 95.1/90.0/85.4/80.9 (BP=0.988, ratio=0.988, hyp_len=28458, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$
```

## Checking for Braille to Myanmar ...  

Braille ကနေ မြန်မာစာဘက်ကို translation လုပ်ဖို့အတွက် train လုပ်ခဲ့တဲ့ model တွေကို sorting လုပ်ပြီး iteration အစဉ်အလိုက် ကြည့်ရင် အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ ls model0-brmy.iter*.npz | sort -V
model0-brmy.iter5000.npz
model0-brmy.iter10000.npz
model0-brmy.iter15000.npz
model0-brmy.iter20000.npz
model0-brmy.iter25000.npz
model0-brmy.iter30000.npz
model0-brmy.iter35000.npz
model0-brmy.iter40000.npz
model0-brmy.iter45000.npz
model0-brmy.iter50000.npz
model0-brmy.iter55000.npz
model0-brmy.iter60000.npz
model0-brmy.iter65000.npz
model0-brmy.iter70000.npz
model0-brmy.iter75000.npz
model0-brmy.iter80000.npz
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$
```

## Prepared tran-eval Shell Script for Braille-to-Myanmar


(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ cat ./tran-eval-brmy.sh 

```bash
 #!/bin/bash

## Preparation for Myanmar-MuHaung, MuHaung-Myanmar
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer Model
## 21 Feb 2022

for i in {5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,55000,60000,65000,70000,75000,80000}
do
   marian-decoder -m ./model0-brmy.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter$i.my < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br
   echo "Evaluation with hyp.iter$i.my, Transformer Model:" >> test0-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./hyp.iter$i.my  >> test0-results.txt
done
```

##  Translation with Test Data (for 0/, br-my)

Braille (မူဟောင်း) ကနေ မြန်မာစာ ဘက်ကို translation လုပ်ပြီး ထွက်လာတဲ့ output hyp ဖိုင်တွေကို evaluation လုပ်ဖို့အတွက် အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ time ./tran-eval-brmy.sh 
...
...
...
[2022-02-21 16:35:36] Best translation 2052 : မီးအိမ် ကလေး ကို ကရုစိုက် ပါ ။
[2022-02-21 16:35:36] Best translation 2053 : ဂြောင် ဒေါ်ခင် ၏ ဘူးသီးကြော် မှာ တဖြည်းဖြည်း ပေါက်များ လာ၍ ကျော် နိုင် သမျှ ကုန် သော ဟူ ၏ ။
[2022-02-21 16:35:37] Best translation 2054 : မဟော်သဓာ သုခမိန် သည် ထို သူတို့ စကား ကို ကြား ပြီး သော် သင်တို့ ငါ ၏ အဆုံးအဖြတ် ၌ တည် ကြ မည် လော ဟု မေး ၏ ။
[2022-02-21 16:35:37] Best translation 2055 : ၄ ။ သင်သာ = မျိုးရိုး ဇာတိ အလုပ်အကိုင် စသည် ထူးခြားတာ ။
[2022-02-21 16:35:37] Best translation 2056 : ဝိဒေဟရာဇ် မင်းကြီး လည်း ဤ ပြဿနာ ကို အဘယ်သူ ဖြေ စီရင် သနည်း ဟု မေး ၏ ။
[2022-02-21 16:35:37] Best translation 2057 : ကျွန်တော်တို့ ရောက် နေ စဉ် ကန်ပေါင် နှင့် ရေ နှင့် ကန် ပီပီ မြင် ရ ပေ သေး သည် ။
[2022-02-21 16:35:37] Best translation 2058 : သာဓက ။ ။ လူကောင်း = လူကောင်း ။
[2022-02-21 16:35:37] Best translation 2059 : ခြင် နိုင် ဆေး ဖျန်း ပါ ။
[2022-02-21 16:35:37] Best translation 2060 : ဂြောင် သည် ဆင်ခြေလျှော ကစား ရသော ကစားနည်း ဖြစ် သည် ။
[2022-02-21 16:35:37] Best translation 2061 : သနပ် ဟု ရေး မှ အသီး စသည် တို့ ကို ဆီ ၊ လိမ်လိမ်မာမာ ၊ ငရုတ်သီး စသည် တို့ နှင့် ရော ထား သော စားဖွယ် တစ် မျိုး ဟု အဓိပ္ပာယ် ရ လိမ့်မည် ။
[2022-02-21 16:35:37] Best translation 2062 : ၁ ။ လုလင် = ပျိုရွယ် သော ယောက်ျား ။
[2022-02-21 16:35:37] Best translation 2063 : ဥပမာ လာစဉ် ၌ ချည် ကလေး တစ် မျှင် ကို ခပ် ဖို့ ရန် အပြား လာပါဦးကွာ ဟု လက် ကလည်း လေး ငါး ချက် လောက် ကြမ်းကြမ်းတမ်းတမ်း ရ ၏ ။
[2022-02-21 16:35:37] Best translation 2064 : မိခင် မှာ သဘင် ပညာသည် မျိုးရိုး ဖြစ် သည် ။
[2022-02-21 16:35:37] Best translation 2065 : သတ်ပုံ သံပေါက် ကဗျာ ကို ဆို ကြ ရအောင် ။
[2022-02-21 16:35:37] Best translation 2066 : မြက် တစ် ခတ် ၊ တူးရွင်း ကယ် တစ် ဗီဇနာ မျှ ။
[2022-02-21 16:35:37] Best translation 2067 : ဝတ္ထု ကာမဂုဏ် ၊ ငွေစ နှင့် ကြုံ သောအခါ ၊ အာရုံ ကို ဖြတ် နိုင် ခဲ့ လှ ပါ သည် ရွှေနန်းရှင် ဘုရား ။
[2022-02-21 16:35:37] Best translation 2068 : အဘိုးကြီး ရော ကောင်မလေး ရော သဗ္ဗညု ဘုရား တို့ ၊ အာနန္ဒာ ဘုရား တို့ ၊ တျော ( ကန်တော့ပလ္လင် ) တို့ လျှောက် ဖူး ရအောင် နေ့လယ် ကတဲ က လှည်း နဲ့ ထွက် ကြ တယ် ။
[2022-02-21 16:35:37] Best translation 2069 : ဟန် အမူအရာ နဲ့ ဆို နိုင် ကြ ရဲ့လား ။
[2022-02-21 16:35:37] Best translation 2070 : ရွာ ထဲ မှာ အငြိမ့် ပွဲ ရှိ သလား ။
[2022-02-21 16:35:37] Best translation 2071 : ကွာ ဇမ္ဗူဒီပါ မှာ မြန်မာ ကို နိုင် မည့် လူ မ ပေါ် သေး ပါ ဘူး ဟု ကျုံးဝါး တော် မူ ၏ ။
[2022-02-21 16:35:37] Best translation 2072 : ၃ ။ အလုတ် သူ ကို သတ်မှတ် ထား တဲ့ မေးခွန်း တွေ မေး ပြီး ပြောတာ တွေ မ မေ့ ရအောင် မှတ်စု မှာ ရေးမှတ် လာ ကြ ရ မယ်နော် ။
[2022-02-21 16:35:37] Best translation 2073 : ၆ ။ အကြေ = မြန်မာ ပြည် ဗြဟ္မဒတ် ဒေသ ။
[2022-02-21 16:35:37] Best translation 2074 : ကဲ့ရဲ့ ၊ ချီးမွမ်း ၊ စာရင်း ၊ သက်သေ ၊ အကျင့် ၊ ဥစ္စာ ။
[2022-02-21 16:35:37] Best translation 2075 : ရှေး သောအခါ ဗာရာဏသီ မင်း တစ်ပါး ၏ သားတော် သည် တက္ကသိုလ် ပြည် ၌ ပညာ သင်ကြား နေစဉ် တစ် နေ့ ၌ အမယ်အို တစ် ယောက် လှမ်း ထား သော နှမ်း ကို စား လို သည် နှင့် တစ် ဆုတ် ယူ၍ စား ၏ ။
[2022-02-21 16:35:37] Best translation 2076 : စိမ့် ကြီး မြိုင် ကြီး ၊ ရိပ် ကြီး တော တောင် ။
[2022-02-21 16:35:37] Best translation 2077 : ပါဠိ စာပေ ကျမ်းဂန်များ ကဗျာ လင်္ကာများ ကို လယ်တီ ဆရာတော် ထံ တွင် ဆက်လက် ဆည်းပူး ပြီး သက္ကတ စာပေများ ကို ဝိသုဒ္ဓါရုံ ဆရာတော် ထံ တွင် ဆက်လက် ဆည်းပူး သည် ။
[2022-02-21 16:35:37] Best translation 2078 : ၃ ။ အုတ် တံတိုင်း ကာရံ သော ခြံ ကျယ် ကြီးများ တွင် ထားရှိ သည့် တိရစ္ဆာန်များ ၏ အမည် ကို ဖော်ပြ ပါ ။ အဘယ်ကြောင့် ထိုသို့ ထား ရ သနည်း ။
[2022-02-21 16:35:38] Best translation 2079 : ဤ ကဗျာ ကို ရေးသူ ဦးကြင်ဥ သည် မြန်မာ နှစ် ၁ ၁ ၃ ၅ - ၁ ၂ ၀ ၀ ( ခရစ် နှစ် ၁ ၇ ၇ ၃ - ၁ ၈ ၃ ၈ ) အတွက် ပေါ်ပေါက် ခဲ့ သော စာဆို ဖြစ် သည် ။
[2022-02-21 16:35:38] Best translation 2080 : ၃ ၁ ။ အောက်မေ့ = ဆင်ခြင် စဉ်းစား သည် ။ နှလုံးသွင်း သည် ။
[2022-02-21 16:35:38] Best translation 2081 : ၁ ။ အတာကူး ခြင်း ဆိုသည် မှာ အဘယ် နည်း ။
[2022-02-21 16:35:38] Best translation 2082 : ဤ သူ ၏ နွားများ မဟုတ် ပါ ။
[2022-02-21 16:35:38] Best translation 2083 : ၃ ။ အောက်ပါ အလင်္ကာ တို့ သည် မည်သို့ သော အကြောင်း နှင့် ဆက်စပ် သုံး ထား ပြီး အဘယ်ကြောင့် ထို အလင်္ကာ မြောက် ကြောင်း ရှင်းပြ ပါ ။
[2022-02-21 16:35:38] Best translation 2084 : မြို့ တောင် မျက်နှာ က ရေ ရောင်း မိန်းမ ထွက် ဆို ရန် စကား မှာ ။
[2022-02-21 16:35:38] Best translation 2085 : စာ အရေးအသား အလေးထား ပါ ။
[2022-02-21 16:35:38] Best translation 2086 : ကျိုက်ထီးရိုး စေတီတော် သည် မြတ်စွာဘုရား ၏ ဆံတော်ရှင် ကို ဌာပနာ၍ တည် ထား သောကြောင့် တန်ခိုး ကြီး သည် ဟု ယုံကြည် ကိုးကွယ် ကြ သည် ။
[2022-02-21 16:35:38] Best translation 2087 : ကွယ်လွန် သည့် အချိန် အထိ အဆက်မပြတ် စာ ရေး ခဲ့ သူ ဖြစ် သည် ။
[2022-02-21 16:35:38] Best translation 2088 : ၂ ၀ ၁ ၀ - ၂ ၀ ၁ ၁ ပညာသင် နှစ် ။
[2022-02-21 16:35:38] Best translation 2089 : စ ။
[2022-02-21 16:35:38] Best translation 2090 : ၇ ။ သီတင်းကျွတ် တွင် ၊ ပလ္လင် ဆေး မိုး ၊ ရွာသွန်းဖြိုး ။
[2022-02-21 16:35:38] Best translation 2091 : ၃ ၉ ။ ယပ်မား = နန်းတွင်း သုံး အရိုး ရှည် ယပ် ကြီး ။
[2022-02-21 16:35:38] Best translation 2092 : ဒုက္ခ ပါ ပဲ သူငယ်ချင်း ရေ ခဲတံ ငှား ပါ အုံး လို့ ပြော ပြီး အကူအညီ တောင်း ရ တယ် ။
[2022-02-21 16:35:38] Best translation 2093 : သို့ရာ တွင် ထို ပြည် ကလေး က စစ် မ တိုက် ဘဲ ကျွန်တော်တို့ ဘုရင် ကို ဖမ်း သွား ပါ ။
[2022-02-21 16:35:38] Best translation 2094 : ကလတက်သံ နှင့်အတူ ပါ၍ လာ သော အဓိပ္ပာယ် တစ် မျိုး လည်း ရှိ သေး ၏ ။
[2022-02-21 16:35:38] Best translation 2095 : အရှင် မင်းကြီး ၊ ကျွန်ုပ် ၏ အမည် ကား သုဝဏ္ဏသာမ တည်း ။
[2022-02-21 16:35:38] Best translation 2096 : ဂြောင် ကုသိုလ်ရှင် လူပျိုကြီး စွန် ချင် ရှာ သောကြောင့် ကြော်ငြာ ကမ်း ထား ဟန် တူ သည် ။
[2022-02-21 16:35:38] Best translation 2097 : မြောက်ဘက် ဆီ သို့ ခရီး နှင် တွေ့ လိမ့် နယ် ကချင် ပလွေ သံလွင် အိုးစည် နှော ထောင်ကာ နဲ့ မနော ။
[2022-02-21 16:35:38] Best translation 2098 : မြန်မာ ဘုရင် တို့ ကိုယ့် ထီး ကိုယ့် နန်း အဖြစ် နောက်ဆုံး တည်ထောင် စံမြန်း ခဲ့ ကြ သည့် နန်းတော် ကြီး လည်း ဖြစ် သည် ။
[2022-02-21 16:35:38] Best translation 2099 : အော အော့ အော် ။
[2022-02-21 16:35:38] Best translation 2100 : ၃ ။ ကဏ္ဍ = အပိုင်း ၊ အခန်း ။
[2022-02-21 16:35:38] Best translation 2101 : တင် ပါ သည် ဘုရား ။
[2022-02-21 16:35:38] Best translation 2102 : ပန်းကလေးများ ပွင့် တော့ မည် ဖူးတံ အော့်ဖ် ချီ ၊ နေခြည် မှာ ရွှေရည် လောင်း ငါ တို့ စာသင်ကျောင်း ။
[2022-02-21 16:35:38] Best translation 2103 : လေ့ကျင့်ခန်း ။
[2022-02-21 16:35:38] Best translation 2104 : ၆ ။ မြန်မာ့ ရိုးရာ ခြင်း ကစား နည်း သည် မြန်မာ တို့ အတွက် ဂုဏ်ယူ ဖွယ်ရာ ဖြစ် ပါ သလား ။
[2022-02-21 16:35:38] Best translation 2105 : အရေး မဟုတ် ဟု လျှောက် သည် ကို ကြိုက် တော် မ မူ ။
[2022-02-21 16:35:38] Best translation 2106 : ကျန်းမာ မရွေး ၊ တူးရွင်း လေးစား အပ်ပေ ၊ တို့မေမေ ။
[2022-02-21 16:35:38] Best translation 2107 : ဆေးကြော ။
[2022-02-21 16:35:38] Best translation 2108 : ထို သူ့ နွား မဟုတ် ဟု ဆို ၏ ။
[2022-02-21 16:35:38] Best translation 2109 : သူ ၏ ပါး ကလေးများ ၊ ခြေ ဖျား လက် ဖျား ကလေးများ ၊ နားရွက် ကလေးများ မှာ ဝါ၍ လာ ကြ လေ သည် ။
[2022-02-21 16:35:38] Best translation 2110 : ( စ ) အမိ အဖ တို့ ကို လုပ်ကျွေး ခြင်း ဖြင့် မည်သို့ သော အကျိုးကျေးဇူး တို့ ကို ရရှိ နိုင် သနည်း ။
[2022-02-21 16:35:38] Best translation 2111 : ဂြောင် ။ ။ လပြည့် ကျော် ၆ ရက် ပါ ဖေဖေ ။
[2022-02-21 16:35:38] Best translation 2112 : ချိုင် ချိုင့် ချိုင်း ။
[2022-02-21 16:35:38] Best translation 2113 : သူ သည် နာမည် နှင့် လိုက် အောင် ဖြူ သည် ၊ ချော သည် ၊ လှ သည် ၊ ချော သည် လှ သည် နှင့် အမျှ ထွက်လာသော လင် ငယ် နေ တတ် သူ ။
[2022-02-21 16:35:39] Best translation 2114 : ၂ ။ လေး မောင့် စံကျောင်း တွင် မြစ်ဖျား မျိုး တို့ သည် မည်သို့ သော နေရာ အသီးသီး ၌ ပေါက် နေ တန်ဆာဆင် နေ ကြ သနည်း ။
[2022-02-21 16:35:39] Best translation 2115 : အမျိုး ခုနစ် ဆက် တိုင်အောင် မ ပျက် သော ချစ် ခြင်း သည် ဖြစ် လေ သတည်း ။
[2022-02-21 16:35:39] Best translation 2116 : ဂြောင် သင်္ကြန် ။
[2022-02-21 16:35:39] Best translation 2117 : ထိုအခါ ပုစွန် က အဆွေ ဗျိုင်း အဘယ်ကြောင့် အကျွန်ုပ် ကို အိုင် ၌ မ လွှတ် ဘဲ ဤ ခံတက်ပင် သို့ ဆောင်ယူ ခဲ့ သနည်း ဟု မေး လေ ၏ ။
[2022-02-21 16:35:39] Best translation 2118 : အမည် ဒထွေး ။
[2022-02-21 16:35:39] Best translation 2119 : မန္တလေး တက္ကသိုလ် မှ လေ့လာ ရေး အဖွဲ့ ။
[2022-02-21 16:35:39] Best translation 2120 : ဟုတ်ကဲ့ ၊ လေး ဆယ် လောက် ဆို ပါ တော့ ။
[2022-02-21 16:35:39] Best translation 2121 : သူ လျှင် ငါး ဖမ်း ထွက် သတတ် ( သ တဲ့ ) ။
[2022-02-21 16:35:39] Best translation 2122 : ဤ လည်း ဘုရားလောင်း အား ကောင်းချီး မင်္ဂလာ တစ် ကြိမ် ဖြစ် သတည်း ။
[2022-02-21 16:35:39] Best translation 2123 : ဥပါယ် ၊ အိုးစားဖက် ၊ ယွန်းမ ၊ အပါ ချ ၊ မြင်း မှာ အုန်းခွံ ၊ ဓား မှာ မိုးကြိုး ။
[2022-02-21 16:35:39] Best translation 2124 : ရဝေ ၊ ဗီဇနာ ၊ ဗျာဆုံ ၊ လိပ်ပြာ အေး ၊ ရတု ။
[2022-02-21 16:35:39] Best translation 2125 : ကတ္တီပါ နှင့် ။
[2022-02-21 16:35:39] Best translation 2126 : မြန်မာ ဘုရင် ပါ တော်မူ သောအခါ တွင် လည်း ရွှေ ဆီးဖြူ သဘော သို့ ၊ သိမ်ဖွဲ့သေးနုပ် နှင့် လှိမ့် သလို ဟူ၍ မှတ်တမ်းတင် ခဲ့ သည် ။
[2022-02-21 16:35:39] Best translation 2127 : ခွေ ဋ် ခွေး ။
[2022-02-21 16:35:39] Best translation 2128 : ဦးအိ သည် အမရပူရ မြို့ ဖြင်း မှ ပိုး ထည် ၊ ချည် ထည် တို့ ကို အရောင်းအဝယ် ပြု သော ပိုး ကင်ခ်ျ့ ဖြစ်ရာ ပစ္စည်း ဥစ္စာ ကြွယ်ဝ ချမ်းသာ သည် ။
[2022-02-21 16:35:39] Best translation 2129 : ခက်ဆစ် အဖွင့် ။
[2022-02-21 16:35:39] Best translation 2130 : ၃ ။ ဖွာ ရ ရာ = စုစည်း ခြင်း မ ရှိ ၊ ကွဲ ဖျာ ထွက် လျက် ။
[2022-02-21 16:35:39] Best translation 2131 : မိမိ ကိုယ်တိုင် အသံနေအသံထား ဖြင့် ရွတ်ဆို လေ့ကျင့် ပါ ။
[2022-02-21 16:35:39] Best translation 2132 : ( ခ ) တစ်ဥတု လျှင် ------ စီ ကြာမြင့် ပါ သည် ။
[2022-02-21 16:35:39] Best translation 2133 : ညောင်ပင်သာရွာ ဖြူး မြို့နယ် ၁ ၃ ၄ ၅ ခု ၊ တန်ခူး လဆန်း ၁ ရက် သူငယ်ချင်း ဦးဘဇော် သူငယ်ချင်း ထံသို့ ကင်ခ်ျ့ ပါ သည် ။
[2022-02-21 16:35:39] Best translation 2134 : ၈ ။ အားသန် = မ ရ မ နေ မ ဖြစ် မ နေ အားထုတ် ကြိုးပမ်း သည် ။
[2022-02-21 16:35:39] Best translation 2135 : ပျားရည် သာ ဆောင်ယူ ကြ ချေ ဟု ဆို၍ ပျားရည် ကို ဆောင်ယူ စေ ပြီး သော် ပတ္တမြား ၌ အပေါက်ဝ နှစ် ဖက် ကို လိမ်းသုတ် ပြီး မှ နူးညံ့ သိမ်မွေ့ လှစွာ သော ကမ္ဗလာ ချည် ကြိုး ကို ကျစ် ပြီးလျှင် ထို ကမ္ဗလာ ကြိုး စ ၌ ပျားရည် ဖြင့် ပျားပိတုန်း ကမ္ဗလာ ကြိုး စ ကို ပတ္တမြား ပေါက် ဝ ကြိုး ဟောင်း စ တစ်ဖက် နှင့် တေ့ ပြီး စဉ်းငယ် ထား ပြီး သော် ပတ္တမြား ဝ ပတ္တမြား ဝ က ပုရွက် ၊ ပိုးရွ ၊ အောင်အုပ် ကို ပုရွက် စားသောက် စေ ခြင်း ၊ ၊ မူးမူး ၊ နေရာ တို့ ၌ ၊ နေရာ တို့ ကို ပတ္တမြား ထား ၏ ။
[2022-02-21 16:35:39] Best translation 2136 : ကျွန်တော်တို့ နှင့် ရင်းနှီး သော အကြောင်းအရာ ပင် ဖြစ် လင့် ကစား ၊ ကျွန်တော်တို့ ခေါက်ထည်ကြမ်း မှ မ ရေး ရ ၊ ကျွန်တော်တို့ ကြည့်မြင် ခံစား သလို မ ရေး ရ ၊ ကျောင်း ပြာတာ ကြီး ၏ လက်ဆစ် မှ ရေး ရ မည် ။
[2022-02-21 16:35:39] Best translation 2137 : စကားလုံး ကလေး တွေ စီ ကာ ရယ် ရွတ်ဆို ရေး ကြည့် မယ် ။
[2022-02-21 16:35:40] Best translation 2138 : မမြရင် တို့ အငြိမ့် က သည့် ခေတ် က အုန်းမောင်း မ ပေါ် သေး ပါ အငြိမ့် မင်းသမီးများ သည် ပွဲခင်း ကို ပေါက် အောင် မိမိ ၏ ပင်ကို အသံ နှင့် ကြိုးစား၍ ဆို ကြ ရ သည် ။
[2022-02-21 16:35:40] Best translation 2139 : မှီငြမ်းပြု ဝတ္ထုများ ၊ ဘာသာပြန် ဝတ္ထုများ ဖေဖေါ်ဝါရီ ရာ ပျိုးနုတ်၍ ၊ ဦးစော ၊ ဘူးသီးခြောက် ၊ ရွှေရင်ကြား ၊ ဦးဘဉာဏ် ၊ ဦးငွေကိုင် ၊ သင်ချေ စသည် တို့ မှာ ထင်ရှား သော မှီငြမ်းပြု သော ဝတ္ထုများ ဖြစ် သည် ။
[2022-02-21 16:35:40] Best translation 2140 : ရှေးခေတ် စစ်သည် တစ် ဦး ၏ ဘဝ တစ် စိတ် တစ် ပိုင်း ကို ထင်ဟပ် သော အိုင်းချင်း ဖြစ် သည် ။
[2022-02-21 16:35:40] Best translation 2141 : လိပ်ပြာ တွင် လည်း အခြား သော ဥပေါသထ ကဲ့သို့ ဦးခေါင်း ပိုင်း ၊ ရင် ပိုင်း ၊ ဝမ်းဗိုက် ပိုင်း ဟူ၍ ရှိ သည် ။
[2022-02-21 16:35:40] Best translation 2142 : ကာတွန်း ဆရာကြီး ဦးဘဂျမ်း ။
[2022-02-21 16:35:40] Best translation 2143 : ဈမျဉ်းဆွဲ ။
[2022-02-21 16:35:40] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် ခင်မ မောင်း လေ့ ရှိ သည် ။
[2022-02-21 16:35:40] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-02-21 16:35:40] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အသားရောင် သည် အရေး တွင် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ ချောင်းဦး ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-02-21 16:35:40] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-02-21 16:35:40] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-02-21 16:35:40] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-02-21 16:35:40] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ ငယ်ထိပ် က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-02-21 16:35:40] Best translation 2151 : နေ့တိုင်း မှာ ကား ပုတ်သင်ညို သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-02-21 16:35:40] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-02-21 16:35:40] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ပုတ်သင်ညို မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-02-21 16:35:40] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ ကုပ်ကုပ် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-02-21 16:35:40] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-02-21 16:35:40] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-02-21 16:35:40] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-02-21 16:35:40] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-02-21 16:35:40] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-02-21 16:35:40] Best translation 2160 : ဂြောင် လည်း မ ထိုင် ရ ။
[2022-02-21 16:35:40] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-02-21 16:35:40] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-02-21 16:35:40] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-02-21 16:35:40] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-02-21 16:35:40] Best translation 2165 : ဒူးရင်းသီး ။
[2022-02-21 16:35:41] Best translation 2166 : မိမိ တည် သော ဘုရား ကလအုတ် ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-02-21 16:35:41] Total time: 70.15524s wall

real	19m20.520s
user	36m27.111s
sys	0m47.298s
```

## Check the Results

Braille to Myanmar Translation Results are as follows...  
မူဟောင်းကနေ မြန်မာကို test ဒေတာ သုံးပြီး ဘာသာပြန်ထားတဲ့ ရလဒ်တွေကအောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ cat test0-results.txt 
Evaluation with hyp.iter5000.my, Transformer Model:
BLEU = 83.76, 95.6/91.0/86.8/82.9 (BP=0.942, ratio=0.943, hyp_len=27171, ref_len=28803)
Evaluation with hyp.iter10000.my, Transformer Model:
BLEU = 84.17, 95.6/91.2/87.2/83.3 (BP=0.943, ratio=0.945, hyp_len=27217, ref_len=28803)
Evaluation with hyp.iter15000.my, Transformer Model:
BLEU = 84.74, 95.6/91.1/87.0/83.1 (BP=0.952, ratio=0.953, hyp_len=27440, ref_len=28803)
Evaluation with hyp.iter20000.my, Transformer Model:
BLEU = 84.82, 95.6/91.3/87.3/83.5 (BP=0.949, ratio=0.951, hyp_len=27382, ref_len=28803)
Evaluation with hyp.iter25000.my, Transformer Model:
BLEU = 85.28, 95.5/90.9/86.8/82.9 (BP=0.959, ratio=0.960, hyp_len=27655, ref_len=28803)
Evaluation with hyp.iter30000.my, Transformer Model:
BLEU = 85.46, 95.5/90.8/86.7/82.7 (BP=0.962, ratio=0.963, hyp_len=27741, ref_len=28803)
Evaluation with hyp.iter35000.my, Transformer Model:
BLEU = 86.05, 95.4/90.7/86.6/82.6 (BP=0.970, ratio=0.971, hyp_len=27954, ref_len=28803)
Evaluation with hyp.iter40000.my, Transformer Model:
BLEU = 86.00, 95.3/90.6/86.3/82.3 (BP=0.972, ratio=0.972, hyp_len=28002, ref_len=28803)
Evaluation with hyp.iter45000.my, Transformer Model:
BLEU = 86.29, 95.4/90.6/86.4/82.4 (BP=0.974, ratio=0.975, hyp_len=28075, ref_len=28803)
Evaluation with hyp.iter50000.my, Transformer Model:
BLEU = 86.55, 95.3/90.5/86.2/82.2 (BP=0.979, ratio=0.979, hyp_len=28196, ref_len=28803)
Evaluation with hyp.iter55000.my, Transformer Model:
BLEU = 86.33, 95.3/90.5/86.3/82.2 (BP=0.976, ratio=0.976, hyp_len=28121, ref_len=28803)
Evaluation with hyp.iter60000.my, Transformer Model:
BLEU = 86.99, 95.3/90.4/86.1/82.1 (BP=0.985, ratio=0.985, hyp_len=28365, ref_len=28803)
Evaluation with hyp.iter65000.my, Transformer Model:
BLEU = 87.24, 95.1/90.3/85.9/81.8 (BP=0.990, ratio=0.990, hyp_len=28514, ref_len=28803)
Evaluation with hyp.iter70000.my, Transformer Model:
BLEU = 87.40, 95.1/90.3/85.9/81.8 (BP=0.992, ratio=0.992, hyp_len=28564, ref_len=28803)
Evaluation with hyp.iter75000.my, Transformer Model:
BLEU = 87.40, 95.1/90.2/85.8/81.6 (BP=0.993, ratio=0.993, hyp_len=28592, ref_len=28803)
Evaluation with hyp.iter80000.my, Transformer Model:
BLEU = 87.54, 95.1/90.3/85.9/81.7 (BP=0.994, ratio=0.994, hyp_len=28618, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$
```

## To Do

- Error Analysis
- to increase the translation performance


