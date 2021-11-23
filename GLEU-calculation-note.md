# GLEU (General Language Evaluation Understanding) Calculation Note

## git clone

```
(base) ye@:/media/ye/project2/tool$ git clone https://github.com/cnap/gec-ranking
Cloning into 'gec-ranking'...
remote: Enumerating objects: 125, done.
remote: Total 125 (delta 0), reused 0 (delta 0), pack-reused 125
Receiving objects: 100% (125/125), 449.56 KiB | 3.30 MiB/s, done.
Resolving deltas: 100% (57/57), done.
(base) ye@:/media/ye/project2/tool$
```

## Preparing Data

phonetic-typo error type ကို automatic extracted RE rule နဲ့ spelling suggestion လုပ်ထားတဲ့ ရလဒ်ကို အခြေခံပြီးတွက်မှာမို့ အဲဒီ open-test ဒေတာရဲ့ reference-hyp အတွဲဖိုင်ကို အရင် head လုပ်ကြည့်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github/pecs$ head pho-typo.open.sug-chk 
ရွာ နေ ပြီ	ရွာ နေ ပြီ
ဖြစ် လို့ လဲ	ဖြစ် လို့ လဲ
ဗြောင် စား တွေ လုပ် မ	ဗြောင် စား တွေ လုပ် မ
လောက် နေ ပြီ	လောက် နေ ပြီ
ကား များ ပြီး လို့ ရှိ	ကား များ ပြီး လို့ ရှိ
သ ခံ တွေ ဆေး ရုံ	သ ခံ တွေ ဆေး ရုံ
စောက် ရမ်း တွေ လွမ်း တယ်	စောက် ရမ်း တွေ လွမ်း တယ်
တယ် ဘာ ဖြစ် ဖြစ်	တယ် ပါ ဖြစ် ဖြစ်
စာ သင် ပြီး ဝမ်း	စာ သင် ပြီး ၀
ရှာ ပြီး ပြန် သင်	ရှာ ပြီး ပြန် သင်
(base) ye@:/media/ye/project2/exp/errant/my-data/4github/pecs$
```

GLEU တွက်ဖို့အတွက်က input file သို့မဟုတ် source ဖိုင်လည်း လိုအပ်တယ်။ spelling correction လုပ်တဲ့ case မှာ ဆိုရင်တော့ input ဖိုင် ဆိုတာက spelling အမှားပါနေတဲ့ ဖိုင်ပေါ့...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ head /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/pho-typo.err.syl 
ရွာ နေ ပီ
ဖစ် လို့ လဲ
ဗြောင် စား တေ လုပ် မ
လောက် နေ ပီ
ကား များ ပီး လို့ ရှိ
သ ခံ တေ ဆေး ရုံ
စောက် ရမ်း တေ လွမ်း တယ်
တယ် ဘာ ဖစ် ဖစ်
စာ သင် ပီး ၀
ရှာ ပီး ပြန် သင်
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

အထက်ပါ နှစ်ဖိုင်လုံးကို GLEU စမ်းတွက်ဖို့အတွက် folder အသစ်တစ်ခုဆောက်ပြီး အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  
GLEU ကို installation လုပ်ခဲ့တဲ့ folder အောက်မှာပဲ ပြင်ဆင်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/tool/gec-ranking$ mkdir rule-spellchk
(base) ye@:/media/ye/project2/tool/gec-ranking$ cd rule-spellchk/
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk$ mkdir open
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk$ cd open/
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open$ mkdir pecs
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open$ cd pecs/
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ pwd
/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs
```

copy ကူးခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cp ./pecs/pho-typo.open.sug-chk /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$ cp /media/ye/project1/paper/ONA2021/ei-phyu-mon/report/Finaldata/bigramSyllablePair/test-data/error/pho-typo.err.syl /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/
(base) ye@:/media/ye/project2/exp/errant/my-data/4github$
```

".sug-chk" ဖိုင်ကနေ sug (i.e. reference) နဲ့ chk (i.e. hyp) ဖိုင်နှစ်ဖိုင်အဖြစ် အောက်ပါအတိုင်း သပ်သပ်စီ ခွဲသိမ်းခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ cut -f1 ./pho-typo.open.sug-chk > ./pho-typo.open.sug
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ cut -f2 ./pho-typo.open.sug-chk > ./pho-typo.open.chk
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ head ./pho-typo.open.sug
ရွာ နေ ပြီ
ဖြစ် လို့ လဲ
ဗြောင် စား တွေ လုပ် မ
လောက် နေ ပြီ
ကား များ ပြီး လို့ ရှိ
သ ခံ တွေ ဆေး ရုံ
စောက် ရမ်း တွေ လွမ်း တယ်
တယ် ဘာ ဖြစ် ဖြစ်
စာ သင် ပြီး ဝမ်း
ရှာ ပြီး ပြန် သင်
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ head ./pho-typo.open.chk 
ရွာ နေ ပြီ
ဖြစ် လို့ လဲ
ဗြောင် စား တွေ လုပ် မ
လောက် နေ ပြီ
ကား များ ပြီး လို့ ရှိ
သ ခံ တွေ ဆေး ရုံ
စောက် ရမ်း တွေ လွမ်း တယ်
တယ် ပါ ဖြစ် ဖြစ်
စာ သင် ပြီး ၀
ရှာ ပြီး ပြန် သင်
(base) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$
```

## Calculate GLEU

GLEU score ကို အောက်ပါအတိုင် တွက်ကြည့်ခဲ့တယ်။  
ပထမဆုံး GLEU score ကို လက်ရှိ ကွန်ပျူတာမှာ တွက်တာမို့ scipy.stats module က မရှိလို့ အောက်ပါအတိုင်း error ပေးတယ်။  

```
(base) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4 -l 0.0
Traceback (most recent call last):
  File "./compute_gleu", line 26, in <module>
    import scipy.stats
ImportError: No module named scipy.stats

real	0m0.015s
user	0m0.007s
sys	0m0.007s
(base) ye@:/media/ye/project2/tool/gec-ranking/scripts$
```

GLEU တွက်တဲ့ python script က python2.7 နဲ့ ရေးထားတာမို့ စက်ထဲမှာလည်း py2.7 environment ပြင်ထားတာ ရှိတာမို့ အဲဒီ environment အောက်မှာတော့ scipy ကို install လုပ်ထားသလားလို့ ... အဲဒါနဲ့ py2.7env conda environment အောက်ကို ဝင်ပြီးမှ GLEU ထပ်တွက်ကြည့်ခဲ့တယ်။  
အောက်ပါအတိုင်း parameter or option က မှားနေကြောင်း error ပေးတယ်။ ကြည့်ရတာ Github မှာ example အနေနဲ့ run ပြထားတာက update မဖြစ်တော့ဘူးလို့ ထင်တယ်။  

```
(base) ye@:/media/ye/project2/tool/gec-ranking/scripts$ conda activate py2.7env
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4 -l 0.0
usage: compute_gleu [-h] -r [REFERENCE [REFERENCE ...]] -s SOURCE -o
                    [HYPOTHESIS [HYPOTHESIS ...]] [-n N] [-d] [--iter ITER]
compute_gleu: error: unrecognized arguments: -l 0.0

real	0m0.362s
user	0m0.380s
sys	0m1.036s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ 
```

default parameter နဲ့ပဲ သွားကြည့်တယ်။ "-l" option ကို မပေးပဲ အောက်ပါအတိုင်း run ကြည့်ခဲ့တယ်။  

```
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.672853

real	0m0.955s
user	0m0.530s
sys	0m0.965s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$
```
"RuntimeWarning: invalid value encountered in multiply" ဆိုတဲ့ error ပေးနေလို့ -n တန်ဖိုးကို အမျိုးမျိုး လျှော့တာ၊ တိုးတာ လုပ်ခဲ့ပေမဲ့ warning က တက်နေတုန်းပဲ...  

```
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.672853

real	0m0.955s
user	0m0.530s
sys	0m0.965s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 1
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.949313

real	0m0.221s
user	0m0.398s
sys	0m0.696s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 2
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.862073

real	0m0.215s
user	0m0.383s
sys	0m0.782s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 3
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.767264

real	0m0.212s
user	0m0.414s
sys	0m0.681s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$
```

အထက်ပါအတိုင်း GLEU score တော့ ထွက်တယ်။ -n value ပေါ်မူတည်ပြီး ရလဒ်အပြောင်းအလဲ ရှိတာကို တွေ့ရတယ်။  
Runtime Warning နဲ့ ပတ်သက်ပြီး လေ့လာရန်...  
စာကြောင်းက အရမ်းတိုနေတာနဲ့ ဆိုင်မယ်လို့ ယူဆတယ်။  




