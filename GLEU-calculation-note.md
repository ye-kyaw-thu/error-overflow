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
"RuntimeWarning: invalid value encountered in multiply lower_bound = self.a * scale + loc" နဲ့ "RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc" ဆိုတဲ့ runtime warning ပေးနေလို့ -n တန်ဖိုးကို အမျိုးမျိုး လျှော့တာ၊ တိုးတာ လုပ်ခဲ့ပေမဲ့ warning က တက်နေတုန်းပဲ...  

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
စာကြောင်းက အရမ်းတိုနေတာနဲ့ ဆိုင်မယ်လို့ ယူဆတယ်။ စာတမ်းကို ဖတ်ရန်...   

## Debugging

Iteration ကို အပြောင်းအလဲ လုပ်ကြည့်ခဲ့...  
ရလဒ်ကတော့ အောက်ပါအတိုင်း မပြောင်းလဲပါဘူး...  

```
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4 --iter 1
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.672853

real	0m0.208s
user	0m0.367s
sys	0m0.721s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc
pho-typo.open.chk 0.672853

real	0m0.203s
user	0m0.372s
sys	0m0.705s
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$
```

ဖြစ်နိုင်တာက sentence length (i.e. number of words) မညီလို့ ပေးတဲ့ Warning လည်း ဖြစ်နိုင်တယ်။  
error message နဲ့ Googling လုပ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

Reference: [https://stackoverflow.com/questions/34955158/what-might-be-the-cause-of-invalid-value-encountered-in-less-equal-in-numpy/34955622](https://stackoverflow.com/questions/34955158/what-might-be-the-cause-of-invalid-value-encountered-in-less-equal-in-numpy/34955622)  

```
That's most likely happening because of a np.nan somewhere in the inputs involved.
```

--debug option ထည့်ပြီး run ခဲ့တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/scripts$ time python2.7 ./compute_gleu -s /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.err.syl -r /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.sug -o /media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs/pho-typo.open.chk -n 4 --debug | tee debug.log
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1920: RuntimeWarning: invalid value encountered in multiply
  lower_bound = self.a * scale + loc
/home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages/scipy/stats/_distn_infrastructure.py:1921: RuntimeWarning: invalid value encountered in multiply
  upper_bound = self.b * scale + loc

===== Sentence-level scores =====
SID Mean Stdev 95%CI GLEU
0 1.000000 0.000000 (nan,nan)
1 1.000000 0.000000 (nan,nan)
2 1.000000 0.000000 (nan,nan)
3 1.000000 0.000000 (nan,nan)
4 1.000000 0.000000 (nan,nan)
5 1.000000 0.000000 (nan,nan)
6 1.000000 0.000000 (nan,nan)
7 0.594604 0.000000 (nan,nan)
8 0.638943 0.000000 (nan,nan)
9 1.000000 0.000000 (nan,nan)
10 1.000000 0.000000 (nan,nan)
11 0.510029 0.000000 (nan,nan)
12 0.594604 0.000000 (nan,nan)
13 1.000000 0.000000 (nan,nan)
14 1.000000 0.000000 (nan,nan)
15 1.000000 0.000000 (nan,nan)
16 1.000000 0.000000 (nan,nan)
...
...
...
...
244 1.000000 0.000000 (nan,nan)
245 1.000000 0.000000 (nan,nan)
246 1.000000 0.000000 (nan,nan)
247 1.000000 0.000000 (nan,nan)
248 1.000000 0.000000 (nan,nan)
249 1.000000 0.000000 (nan,nan)
250 1.000000 0.000000 (nan,nan)
251 1.000000 0.000000 (nan,nan)
252 1.000000 0.000000 (nan,nan)
253 1.000000 0.000000 (nan,nan)
254 1.000000 0.000000 (nan,nan)
255 1.000000 0.000000 (nan,nan)
256 1.000000 0.000000 (nan,nan)
257 1.000000 0.000000 (nan,nan)
258 1.000000 0.000000 (nan,nan)
259 1.000000 0.000000 (nan,nan)
260 1.000000 0.000000 (nan,nan)
261 1.000000 0.000000 (nan,nan)
262 1.000000 0.000000 (nan,nan)
263 1.000000 0.000000 (nan,nan)
264 1.000000 0.000000 (nan,nan)
265 1.000000 0.000000 (nan,nan)
266 0.397635 0.000000 (nan,nan)
267 0.397635 0.000000 (nan,nan)
268 0.273012 0.000000 (nan,nan)
269 0.638943 0.000000 (nan,nan)

==== Overall score =====
Mean Stdev 95%CI GLEU
0.672853 0.000000 (nan,nan)

real	0m0.251s
user	0m0.426s
sys	0m0.719s
```

test, reference နဲ့ hyp ဖိုင်သုံးဖိုင်ကို paste လုပ်ပြီး မျက်လုံးနဲ့ စစ်ခဲ့...   

```
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ paste ./pho-typo.err.syl ./pho-typo.open.sug ./pho-typo.open.chk > source-ref-hyp.txt
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ head ./source-ref-hyp.txt 
ရွာ နေ ပီ	ရွာ နေ ပြီ	ရွာ နေ ပြီ
ဖစ် လို့ လဲ	ဖြစ် လို့ လဲ	ဖြစ် လို့ လဲ
ဗြောင် စား တေ လုပ် မ	ဗြောင် စား တွေ လုပ် မ	ဗြောင် စား တွေ လုပ် မ
လောက် နေ ပီ	လောက် နေ ပြီ	လောက် နေ ပြီ
ကား များ ပီး လို့ ရှိ	ကား များ ပြီး လို့ ရှိ	ကား များ ပြီး လို့ ရှိ
သ ခံ တေ ဆေး ရုံ	သ ခံ တွေ ဆေး ရုံ	သ ခံ တွေ ဆေး ရုံ
စောက် ရမ်း တေ လွမ်း တယ်	စောက် ရမ်း တွေ လွမ်း တယ်	စောက် ရမ်း တွေ လွမ်း တယ်
တယ် ဘာ ဖစ် ဖစ်	တယ် ဘာ ဖြစ် ဖြစ်	တယ် ပါ ဖြစ် ဖြစ်
စာ သင် ပီး ၀	စာ သင် ပြီး ဝမ်း	စာ သင် ပြီး ၀
ရှာ ပီး ပြန် သင်	ရှာ ပြီး ပြန် သင်	ရှာ ပြီး ပြန် သင်
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ tail ./source-ref-hyp.txt 
တီ ကြီး တေ က ဂ	တီ ကြီး တွေ က ဂ	တီ ကြီး တွေ က ဂ
လုပ် ပီး လို့ နား	လုပ် ပြီး လို့ နား	လုပ် ပြီး လို့ နား
ပီး ရင် လာ	ပြီး ရင် လာ	ပြီး ရင် လာ
ပီ	ပြီ	ပြီ
ချင် နေ ပီ	ချင် နေ ပြီ	ချင် နေ ပြီ
တာ တေ	တာ တွေ	တာ တွေ
တစ် ယောက် ထဲ လုပ် နေ	တစ် ယောက် တည်း လုပ် နေ	တစ် ယောက် ထဲ လုပ် နေ
ပြီး ရု ရှ တွေ ကို	ပြီး ရု ရှား တွေ ကို	ပြီး ရု ရှ တွေ ကို
တတ် ဖြစ် မ ယိ့ ရည် ရွယ်	တတ် ဖြစ် မဲ့ ရည် ရွယ်	တတ် ဖြစ် မ ယိ့ ရည် ရွယ်
နံ မည် ပျက်	နာ မည် ပျက်	နံ မည် ပျက်
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$ shuf ./source-ref-hyp.txt | head
၃ ချက် ငြိမ့် ပေး လိုက်	၃ ချက် ညိတ် ပေး လိုက်	၃ ချက် ငြိမ့် ပေး လိုက်
စေ ဆို ပီး ပေး တာ	စေ ဆို ပြီး ပေး တာ	စေ ဆို ပြီး ပေး တာ
နာ ရ ပီ လေ ကိုယ်	နာ ရ ပြီ လေ ကိုယ်	နာ ရ ပြီ လေ ကိုယ်
စပ် ထား ပီး ဘာ မှ	စပ် ထား ပြီး ဘာ မှ	စပ် ထား ပြီး ပါ မှ
လား ဆို ပီး တ ခြား	လား ဆို ပြီး တ ခြား	လား ဆို ပြီး တ ခြား
ပြန် ပို့ ပီး တတ် နိုင်	ပြန် ပို့ ပြီး တတ် နိုင်	ပြန် ပို့ ပြီး တတ် နိုင်
လိုက် လေး တေ လှီး ထား	လိုက် လေး တွေ လှီး ထား	လိုက် လေး တွေ လှီး ထား
များ ပို ပီ ပြင်	များ ပို ပြီး ပြင်	များ ပို ပြီ ပြင်
တိုင်း လာ ပီး လူ မ	တိုင်း လာ ပြီး လူ မ	တိုင်း လာ ပြီး လူ မ
ရော ဆ ကိ ပေါင်း စပ်	ရော စပ် ပေါင်း စပ်	ရော ဆ ကိ ပေါင်း စပ်
(py2.7env) ye@:/media/ye/project2/tool/gec-ranking/rule-spellchk/open/pecs$
```



## To Do
- Running Warning ကိစ္စကို လေ့လာရန်
- စာတမ်း ဖတ်ရန်

## Reference

- https://github.com/cnap/gec-ranking
- Paper relating to "GLEU matric"  
```
@InProceedings{napoles-EtAl:2015:ACL-IJCNLP,
  author    = {Napoles, Courtney  and  Sakaguchi, Keisuke  and  Post, Matt  and  Tetreault, Joel},
  title     = {Ground Truth for Grammatical Error Correction Metrics},
  booktitle = {Proceedings of the 53rd Annual Meeting of the Association for Computational Linguistics and the 7th International Joint Conference on Natural Language Processing (Volume 2: Short Papers)},
  month     = {July},
  year      = {2015},
  address   = {Beijing, China},
  publisher = {Association for Computational Linguistics},
  pages     = {588--593},
  url       = {http://www.aclweb.org/anthology/P15-2097}
}
```
- Paper relating to "GLEU update"  
```
@Article{napoles2016gleu,
  author    = {Napoles, Courtney  and  Sakaguchi, Keisuke  and  Post, Matt  and  Tetreault, Joel},
  title     = {{GLEU} Without Tuning},
  journal   = {eprint arXiv:1605.02592 [cs.CL]},
  year      = {2016},
  url       = {http://arxiv.org/abs/1605.02592}
}
```
