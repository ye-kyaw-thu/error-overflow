# WER and OOV Calculation by Using WER++.py

OOV dictionary ကို ပြင်ဆင်ပြီးတော့ WER နဲ့ OOV တွက်တာကို [WER++.py](https://github.com/nsmartinez/WERpp/blob/master/wer%2B%2B.py) ကို သုံးပြီးလုပ်ပြထားတာပါ။  
ဒီနေရာမှာတော့ pivot machine translation experiment ရဲ့ hypothesis, တိုက်စစ်ဖို့အတွက် ပြင်ထားတဲ့ test data (i.e. reference), training data ထဲက စာလုံးတွေနဲ့ ဆောက်ထားတဲ့ dictionary ကို သုံးပြီး တွက်ပြထားတာပါ။  
NLP/MT evaluation အလုပ်တွေအတွက် အသုံးဝင်ပါလိမ့်မယ်။  

y  
7 Feb 2022  

## Shell Script for 10-fold 

ငါတို့မှာက 10-fold ခွဲပြီးတော့ run ထားတာမို့လို့ experiment တစ်မျိုးစီအတွက် ၁၀ ခါ တွက်ဖို့ လိုအပ်တယ်။  
experiment က baseline, transfer နဲ့ triangulation ဆိုပြီး သုံးမျိုး ရှိတာမို့လို့ အခါ ၃၀ တွက်ဖို့ လိုအပ်တယ်။  
အဲဒါမျိုးကို language pair တစ်ခုစီအတွက် တွက်ရမှာ။ အဲဒါကြောင့် shell script ရေးလိုက်တာက ပိုအဆင်ပြေလိမ့်မယ်။  

အမြန်ရေးတာမို့လို့ rotation ဖြစ်နေတဲ့ ကိစ္စကို မစဉ်းစားတော့ပဲနဲ့ 1 to 10 ကိစ္စ ကို manual ပဲ ချရေးလိုက်ရင်တော့ အောက်ပါအတိုင်း shell script ရလိမ့်မယ်။  
အောက်က shell script က rk-my-bk အတွက် ပါ ...

```bash
#!/bin/bash

# 1
echo "for #1";
cat ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt1;
cd tmp;
cat ./dict4opt1 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt1.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt1.dict ./baseline.opt1 ./rk-my-bk.ref1
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt1.dict ./transfer.opt1 ./rk-my-bk.ref1
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt1.dict ./triangulation.opt1 ./rk-my-bk.ref1


# 2
echo "for #2";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt2;
cd tmp;
cat ./dict4opt2 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt2.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt2.dict ./baseline.opt2 ./rk-my-bk.ref2
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt2.dict ./transfer.opt2 ./rk-my-bk.ref2
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt2.dict ./triangulation.opt2 ./rk-my-bk.ref2

# 3
echo "for #3";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt3;
cd tmp;
cat ./dict4opt3 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt3.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt3.dict ./baseline.opt3 ./rk-my-bk.ref3
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt3.dict ./transfer.opt3 ./rk-my-bk.ref3
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt3.dict ./triangulation.opt3 ./rk-my-bk.ref3

# 4
echo "for #4";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt4;
cd tmp;
cat ./dict4opt4 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt4.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt4.dict ./baseline.opt4 ./rk-my-bk.ref4
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt4.dict ./transfer.opt4 ./rk-my-bk.ref4
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt4.dict ./triangulation.opt4 ./rk-my-bk.ref4

# 5
echo "for #5";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt5;
cd tmp;
cat ./dict4opt5 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt5.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt5.dict ./baseline.opt5 ./rk-my-bk.ref5
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt5.dict ./transfer.opt5 ./rk-my-bk.ref5
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt5.dict ./triangulation.opt5 ./rk-my-bk.ref5

# 6
echo "for #6";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt6;
cd tmp;
cat ./dict4opt6 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt6.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt6.dict ./baseline.opt6 ./rk-my-bk.ref6
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt6.dict ./transfer.opt6 ./rk-my-bk.ref6
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt6.dict ./triangulation.opt6 ./rk-my-bk.ref6

# 7
echo "for #7";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref8 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt7;
cd tmp;
cat ./dict4opt7 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt7.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt7.dict ./baseline.opt7 ./rk-my-bk.ref7
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt7.dict ./transfer.opt7 ./rk-my-bk.ref7
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt7.dict ./triangulation.opt7 ./rk-my-bk.ref7

# 8
echo "for #8";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref9 ./rk-my-bk.ref10 > ./tmp/dict4opt8;
cd tmp;
cat ./dict4opt8 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt8.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt8.dict ./baseline.opt8 ./rk-my-bk.ref8
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt8.dict ./transfer.opt8 ./rk-my-bk.ref8
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt8.dict ./triangulation.opt8 ./rk-my-bk.ref8

# 9
echo "for #9";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref10 > ./tmp/dict4opt9;
cd tmp;
cat ./dict4opt9 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt9.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt9.dict ./baseline.opt9 ./rk-my-bk.ref9
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt9.dict ./transfer.opt9 ./rk-my-bk.ref9
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt9.dict ./triangulation.opt9 ./rk-my-bk.ref9

# 10
echo "for #10";
cat ./rk-my-bk.ref1 ./rk-my-bk.ref2 ./rk-my-bk.ref3 ./rk-my-bk.ref4 ./rk-my-bk.ref5 ./rk-my-bk.ref6 ./rk-my-bk.ref7 ./rk-my-bk.ref8 ./rk-my-bk.ref9 > ./tmp/dict4opt10;
cd tmp;
cat ./dict4opt10 | sed "s/\t/ /g" | sed "s/ /\n/g" | sort | uniq > ./dict4opt10.dict;

cd ..;
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt10.dict ./baseline.opt10 ./rk-my-bk.ref10
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt10.dict ./transfer.opt10 ./rk-my-bk.ref10
python2.7 /media/ye/project2/tool/WERpp/wer++.py --ignore-blank -O ./tmp/dict4opt10.dict ./triangulation.opt10 ./rk-my-bk.ref10


```

## WER Calculation with OOV for bk-my-dw

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/bk-my-dw$ ./oov-calc-bk-my-dw.sh 
for #1
WER: 59.66 (Ins: 242 Dels: 395 Subs: 1757 Ref: 4013 ) OOVs: 13.51% OOVsSubs: 29.25% OOVsIns: 11.57%
WER: 59.01 (Ins: 227 Dels: 411 Subs: 1730 Ref: 4013 ) OOVs: 13.46% OOVsSubs: 29.42% OOVsIns: 13.66%
WER: 58.61 (Ins: 297 Dels: 328 Subs: 1727 Ref: 4013 ) OOVs: 13.36% OOVsSubs: 29.24% OOVsIns: 10.44%
for #2
WER: 58.29 (Ins: 244 Dels: 358 Subs: 1747 Ref: 4030 ) OOVs: 13.62% OOVsSubs: 29.54% OOVsIns: 13.52%
WER: 58.51 (Ins: 230 Dels: 396 Subs: 1732 Ref: 4030 ) OOVs: 13.72% OOVsSubs: 29.91% OOVsIns: 15.22%
WER: 57.10 (Ins: 281 Dels: 299 Subs: 1721 Ref: 4030 ) OOVs: 13.60% OOVsSubs: 29.87% OOVsIns: 12.10%
for #3
WER: 60.88 (Ins: 241 Dels: 419 Subs: 1774 Ref: 3998 ) OOVs: 14.76% OOVsSubs: 31.45% OOVsIns: 13.28%
WER: 61.78 (Ins: 250 Dels: 404 Subs: 1816 Ref: 3998 ) OOVs: 14.88% OOVsSubs: 30.84% OOVsIns: 14.00%
WER: 59.95 (Ins: 297 Dels: 320 Subs: 1780 Ref: 3998 ) OOVs: 14.76% OOVsSubs: 31.12% OOVsIns: 12.12%
for #4
WER: 59.17 (Ins: 313 Dels: 329 Subs: 1732 Ref: 4012 ) OOVs: 14.36% OOVsSubs: 29.97% OOVsIns: 18.21%
WER: 60.59 (Ins: 294 Dels: 395 Subs: 1742 Ref: 4012 ) OOVs: 14.48% OOVsSubs: 30.31% OOVsIns: 18.03%
WER: 59.15 (Ins: 283 Dels: 375 Subs: 1715 Ref: 4012 ) OOVs: 14.38% OOVsSubs: 30.73% OOVsIns: 17.67%
for #5
WER: 58.02 (Ins: 254 Dels: 351 Subs: 1722 Ref: 4011 ) OOVs: 13.69% OOVsSubs: 29.50% OOVsIns: 16.14%
WER: 57.39 (Ins: 242 Dels: 361 Subs: 1699 Ref: 4011 ) OOVs: 13.71% OOVsSubs: 30.19% OOVsIns: 15.29%
WER: 56.42 (Ins: 255 Dels: 315 Subs: 1693 Ref: 4011 ) OOVs: 13.61% OOVsSubs: 29.65% OOVsIns: 17.25%
for #6
WER: 56.51 (Ins: 247 Dels: 326 Subs: 1711 Ref: 4042 ) OOVs: 13.68% OOVsSubs: 29.87% OOVsIns: 17.00%
WER: 57.35 (Ins: 251 Dels: 355 Subs: 1712 Ref: 4042 ) OOVs: 13.68% OOVsSubs: 29.85% OOVsIns: 16.73%
WER: 56.48 (Ins: 286 Dels: 303 Subs: 1694 Ref: 4042 ) OOVs: 13.66% OOVsSubs: 30.05% OOVsIns: 15.03%
for #7
WER: 61.44 (Ins: 269 Dels: 420 Subs: 1784 Ref: 4025 ) OOVs: 13.19% OOVsSubs: 27.58% OOVsIns: 14.50%
WER: 60.20 (Ins: 275 Dels: 397 Subs: 1751 Ref: 4025 ) OOVs: 13.29% OOVsSubs: 28.10% OOVsIns: 15.64%
WER: 58.53 (Ins: 308 Dels: 334 Subs: 1714 Ref: 4025 ) OOVs: 13.22% OOVsSubs: 28.35% OOVsIns: 14.94%
for #8
WER: 59.63 (Ins: 238 Dels: 363 Subs: 1780 Ref: 3993 ) OOVs: 14.78% OOVsSubs: 30.73% OOVsIns: 18.07%
WER: 59.68 (Ins: 231 Dels: 385 Subs: 1767 Ref: 3993 ) OOVs: 14.93% OOVsSubs: 31.69% OOVsIns: 15.58%
WER: 58.63 (Ins: 283 Dels: 295 Subs: 1763 Ref: 3993 ) OOVs: 14.73% OOVsSubs: 30.74% OOVsIns: 16.25%
for #9
WER: 60.03 (Ins: 284 Dels: 405 Subs: 1703 Ref: 3985 ) OOVs: 14.33% OOVsSubs: 31.12% OOVsIns: 14.44%
WER: 59.37 (Ins: 253 Dels: 399 Subs: 1714 Ref: 3985 ) OOVs: 14.53% OOVsSubs: 31.62% OOVsIns: 14.62%
WER: 59.72 (Ins: 299 Dels: 344 Subs: 1737 Ref: 3985 ) OOVs: 14.48% OOVsSubs: 30.92% OOVsIns: 13.38%
for #10
WER: 59.07 (Ins: 209 Dels: 356 Subs: 1532 Ref: 3550 ) OOVs: 13.86% OOVsSubs: 30.81% OOVsIns: 9.57%
WER: 57.80 (Ins: 223 Dels: 324 Subs: 1505 Ref: 3550 ) OOVs: 13.89% OOVsSubs: 31.10% OOVsIns: 11.21%
WER: 57.49 (Ins: 251 Dels: 280 Subs: 1510 Ref: 3550 ) OOVs: 13.94% OOVsSubs: 30.93% OOVsIns: 11.16%
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/bk-my-dw$
```

## WER Calculation with OOV for dw-my-bk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/dw-my-bk$ ./oov-calc-dw-my-bk.sh
for #1
WER: 56.43 (Ins: 403 Dels: 298 Subs: 1707 Ref: 4267 ) OOVs: 9.66% OOVsSubs: 21.50% OOVsIns: 11.17%
WER: 56.41 (Ins: 427 Dels: 255 Subs: 1725 Ref: 4267 ) OOVs: 9.75% OOVsSubs: 21.22% OOVsIns: 11.71%
WER: 55.64 (Ins: 397 Dels: 252 Subs: 1725 Ref: 4267 ) OOVs: 9.68% OOVsSubs: 21.10% OOVsIns: 12.34%
for #2
WER: 54.95 (Ins: 386 Dels: 285 Subs: 1689 Ref: 4295 ) OOVs: 9.29% OOVsSubs: 21.26% OOVsIns: 10.36%
WER: 55.23 (Ins: 382 Dels: 259 Subs: 1731 Ref: 4295 ) OOVs: 9.20% OOVsSubs: 20.28% OOVsIns: 11.52%
WER: 54.41 (Ins: 347 Dels: 271 Subs: 1719 Ref: 4295 ) OOVs: 9.22% OOVsSubs: 20.83% OOVsIns: 10.95%
for #3
WER: 56.96 (Ins: 422 Dels: 285 Subs: 1733 Ref: 4284 ) OOVs: 9.97% OOVsSubs: 21.70% OOVsIns: 12.09%
WER: 58.05 (Ins: 443 Dels: 277 Subs: 1767 Ref: 4284 ) OOVs: 10.01% OOVsSubs: 21.39% OOVsIns: 11.51%
WER: 56.68 (Ins: 430 Dels: 263 Subs: 1735 Ref: 4284 ) OOVs: 9.92% OOVsSubs: 21.50% OOVsIns: 12.09%
for #4
WER: 58.09 (Ins: 350 Dels: 347 Subs: 1706 Ref: 4137 ) OOVs: 10.97% OOVsSubs: 23.45% OOVsIns: 15.43%
WER: 58.30 (Ins: 423 Dels: 305 Subs: 1684 Ref: 4137 ) OOVs: 11.02% OOVsSubs: 23.52% OOVsIns: 14.18%
WER: 57.96 (Ins: 354 Dels: 326 Subs: 1718 Ref: 4137 ) OOVs: 10.95% OOVsSubs: 23.40% OOVsIns: 14.41%
for #5
WER: 55.52 (Ins: 324 Dels: 301 Subs: 1700 Ref: 4188 ) OOVs: 10.91% OOVsSubs: 24.47% OOVsIns: 12.65%
WER: 56.11 (Ins: 325 Dels: 280 Subs: 1745 Ref: 4188 ) OOVs: 10.94% OOVsSubs: 23.72% OOVsIns: 13.54%
WER: 55.68 (Ins: 323 Dels: 276 Subs: 1733 Ref: 4188 ) OOVs: 10.91% OOVsSubs: 23.83% OOVsIns: 13.62%
for #6
WER: 54.79 (Ins: 361 Dels: 256 Subs: 1726 Ref: 4276 ) OOVs: 9.38% OOVsSubs: 21.09% OOVsIns: 10.25%
WER: 54.82 (Ins: 386 Dels: 235 Subs: 1723 Ref: 4276 ) OOVs: 9.35% OOVsSubs: 21.01% OOVsIns: 9.84%
WER: 54.75 (Ins: 360 Dels: 244 Subs: 1737 Ref: 4276 ) OOVs: 9.33% OOVsSubs: 20.84% OOVsIns: 10.28%
for #7
WER: 57.49 (Ins: 385 Dels: 316 Subs: 1759 Ref: 4279 ) OOVs: 9.70% OOVsSubs: 21.38% OOVsIns: 10.13%
WER: 56.88 (Ins: 462 Dels: 268 Subs: 1704 Ref: 4279 ) OOVs: 9.75% OOVsSubs: 21.65% OOVsIns: 10.39%
WER: 56.46 (Ins: 385 Dels: 292 Subs: 1739 Ref: 4279 ) OOVs: 9.70% OOVsSubs: 21.68% OOVsIns: 9.87%
for #8
WER: 56.77 (Ins: 366 Dels: 286 Subs: 1752 Ref: 4235 ) OOVs: 10.39% OOVsSubs: 22.55% OOVsIns: 12.30%
WER: 56.74 (Ins: 405 Dels: 251 Subs: 1747 Ref: 4235 ) OOVs: 10.32% OOVsSubs: 22.55% OOVsIns: 10.62%
WER: 56.88 (Ins: 351 Dels: 284 Subs: 1774 Ref: 4235 ) OOVs: 10.34% OOVsSubs: 22.44% OOVsIns: 11.40%
for #9
WER: 56.75 (Ins: 415 Dels: 305 Subs: 1689 Ref: 4245 ) OOVs: 10.15% OOVsSubs: 22.26% OOVsIns: 13.25%
WER: 56.63 (Ins: 411 Dels: 259 Subs: 1734 Ref: 4245 ) OOVs: 10.37% OOVsSubs: 22.49% OOVsIns: 12.17%
WER: 55.38 (Ins: 390 Dels: 278 Subs: 1683 Ref: 4245 ) OOVs: 10.32% OOVsSubs: 22.70% OOVsIns: 14.36%
for #10
WER: 56.98 (Ins: 356 Dels: 250 Subs: 1529 Ref: 3747 ) OOVs: 11.00% OOVsSubs: 23.48% OOVsIns: 14.89%
WER: 58.10 (Ins: 356 Dels: 268 Subs: 1553 Ref: 3747 ) OOVs: 11.13% OOVsSubs: 23.50% OOVsIns: 14.61%
WER: 56.63 (Ins: 342 Dels: 236 Subs: 1544 Ref: 3747 ) OOVs: 11.02% OOVsSubs: 23.38% OOVsIns: 15.20%
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/dw-my-bk$
```

## WER Calculation with OOV for bk-my-rk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/bk-my-rk$ ./oov-calc-bk-my-rk.sh 
for #1
WER: 44.83 (Ins: 448 Dels: 568 Subs: 2005 Ref: 6739 ) OOVs: 8.03% OOVsSubs: 24.84% OOVsIns: 9.60%
WER: 44.00 (Ins: 467 Dels: 542 Subs: 1956 Ref: 6739 ) OOVs: 8.06% OOVsSubs: 25.51% OOVsIns: 9.42%
WER: 42.74 (Ins: 436 Dels: 515 Subs: 1929 Ref: 6739 ) OOVs: 7.89% OOVsSubs: 25.45% OOVsIns: 9.40%
for #2
WER: 44.10 (Ins: 489 Dels: 556 Subs: 2044 Ref: 7004 ) OOVs: 7.42% OOVsSubs: 23.58% OOVsIns: 7.77%
WER: 44.35 (Ins: 526 Dels: 525 Subs: 2055 Ref: 7004 ) OOVs: 7.44% OOVsSubs: 23.55% OOVsIns: 7.03%
WER: 43.20 (Ins: 502 Dels: 499 Subs: 2025 Ref: 7004 ) OOVs: 7.37% OOVsSubs: 23.56% OOVsIns: 7.77%
for #3
WER: 45.21 (Ins: 508 Dels: 577 Subs: 2088 Ref: 7019 ) OOVs: 8.02% OOVsSubs: 24.95% OOVsIns: 8.27%
WER: 44.85 (Ins: 544 Dels: 536 Subs: 2068 Ref: 7019 ) OOVs: 8.09% OOVsSubs: 25.29% OOVsIns: 8.27%
WER: 44.22 (Ins: 571 Dels: 479 Subs: 2054 Ref: 7019 ) OOVs: 7.98% OOVsSubs: 25.12% OOVsIns: 7.71%
for #4
WER: 45.95 (Ins: 510 Dels: 573 Subs: 2040 Ref: 6796 ) OOVs: 7.98% OOVsSubs: 24.22% OOVsIns: 9.41%
WER: 45.50 (Ins: 525 Dels: 544 Subs: 2023 Ref: 6796 ) OOVs: 7.93% OOVsSubs: 24.07% OOVsIns: 9.90%
WER: 44.11 (Ins: 509 Dels: 509 Subs: 1980 Ref: 6796 ) OOVs: 7.84% OOVsSubs: 24.19% OOVsIns: 10.61%
for #5
WER: 44.10 (Ins: 435 Dels: 564 Subs: 2022 Ref: 6851 ) OOVs: 7.58% OOVsSubs: 23.74% OOVsIns: 8.97%
WER: 43.45 (Ins: 484 Dels: 504 Subs: 1989 Ref: 6851 ) OOVs: 7.60% OOVsSubs: 23.93% OOVsIns: 9.30%
WER: 42.81 (Ins: 442 Dels: 520 Subs: 1971 Ref: 6851 ) OOVs: 7.49% OOVsSubs: 23.90% OOVsIns: 9.50%
for #6
WER: 45.85 (Ins: 471 Dels: 570 Subs: 2076 Ref: 6798 ) OOVs: 8.72% OOVsSubs: 25.92% OOVsIns: 11.68%
WER: 45.56 (Ins: 490 Dels: 545 Subs: 2062 Ref: 6798 ) OOVs: 8.72% OOVsSubs: 25.99% OOVsIns: 11.63%
WER: 45.34 (Ins: 507 Dels: 514 Subs: 2061 Ref: 6798 ) OOVs: 8.63% OOVsSubs: 25.47% OOVsIns: 12.23%
for #7
WER: 44.35 (Ins: 525 Dels: 562 Subs: 2027 Ref: 7021 ) OOVs: 7.79% OOVsSubs: 24.91% OOVsIns: 8.00%
WER: 45.25 (Ins: 576 Dels: 533 Subs: 2068 Ref: 7021 ) OOVs: 7.83% OOVsSubs: 24.42% OOVsIns: 7.81%
WER: 43.61 (Ins: 499 Dels: 546 Subs: 2017 Ref: 7021 ) OOVs: 7.71% OOVsSubs: 24.84% OOVsIns: 8.02%
for #8
WER: 44.48 (Ins: 519 Dels: 549 Subs: 2052 Ref: 7014 ) OOVs: 7.96% OOVsSubs: 24.32% OOVsIns: 11.37%
WER: 44.27 (Ins: 511 Dels: 533 Subs: 2061 Ref: 7014 ) OOVs: 7.94% OOVsSubs: 24.21% OOVsIns: 11.35%
WER: 42.80 (Ins: 469 Dels: 534 Subs: 1999 Ref: 7014 ) OOVs: 7.83% OOVsSubs: 24.36% OOVsIns: 13.22%
for #9
WER: 43.75 (Ins: 517 Dels: 536 Subs: 1935 Ref: 6830 ) OOVs: 7.69% OOVsSubs: 24.29% OOVsIns: 10.64%
WER: 43.67 (Ins: 566 Dels: 495 Subs: 1922 Ref: 6830 ) OOVs: 7.69% OOVsSubs: 24.56% OOVsIns: 9.36%
WER: 42.18 (Ins: 541 Dels: 457 Subs: 1883 Ref: 6830 ) OOVs: 7.60% OOVsSubs: 24.48% OOVsIns: 10.72%
for #10
WER: 46.53 (Ins: 516 Dels: 659 Subs: 2037 Ref: 6903 ) OOVs: 7.76% OOVsSubs: 23.47% OOVsIns: 11.24%
WER: 45.97 (Ins: 523 Dels: 640 Subs: 2010 Ref: 6903 ) OOVs: 7.79% OOVsSubs: 23.93% OOVsIns: 10.90%
WER: 44.60 (Ins: 512 Dels: 562 Subs: 2005 Ref: 6903 ) OOVs: 7.69% OOVsSubs: 23.54% OOVsIns: 11.52%
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/bk-my-rk$
```

## WER Calculation with OOV for rk-my-bk

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver2/mteval-running/data4eval-pivot-10fold/rk-my-bk$ ./oov-calc-rk-my-bk.sh 
for #1
WER: 47.14 (Ins: 463 Dels: 435 Subs: 2381 Ref: 6956 ) OOVs: 7.12% OOVsSubs: 19.61% OOVsIns: 6.05%
WER: 46.42 (Ins: 476 Dels: 402 Subs: 2351 Ref: 6956 ) OOVs: 7.16% OOVsSubs: 19.69% OOVsIns: 7.35%
WER: 45.95 (Ins: 432 Dels: 419 Subs: 2345 Ref: 6956 ) OOVs: 7.12% OOVsSubs: 19.87% OOVsIns: 6.71%
for #2
WER: 46.50 (Ins: 400 Dels: 459 Subs: 2462 Ref: 7142 ) OOVs: 6.85% OOVsSubs: 18.56% OOVsIns: 8.00%
WER: 46.51 (Ins: 438 Dels: 442 Subs: 2442 Ref: 7142 ) OOVs: 6.82% OOVsSubs: 18.59% OOVsIns: 7.53%
WER: 46.19 (Ins: 395 Dels: 479 Subs: 2425 Ref: 7142 ) OOVs: 6.82% OOVsSubs: 18.64% OOVsIns: 8.86%
for #3
WER: 48.57 (Ins: 446 Dels: 506 Subs: 2522 Ref: 7152 ) OOVs: 7.07% OOVsSubs: 18.79% OOVsIns: 7.17%
WER: 47.69 (Ins: 412 Dels: 495 Subs: 2504 Ref: 7152 ) OOVs: 7.10% OOVsSubs: 18.81% OOVsIns: 8.98%
WER: 47.92 (Ins: 403 Dels: 516 Subs: 2508 Ref: 7152 ) OOVs: 7.09% OOVsSubs: 18.98% OOVsIns: 7.69%
for #4
WER: 48.10 (Ins: 426 Dels: 500 Subs: 2395 Ref: 6905 ) OOVs: 6.68% OOVsSubs: 18.16% OOVsIns: 6.10%
WER: 47.79 (Ins: 425 Dels: 490 Subs: 2385 Ref: 6905 ) OOVs: 6.68% OOVsSubs: 18.11% OOVsIns: 6.82%
WER: 47.81 (Ins: 400 Dels: 509 Subs: 2392 Ref: 6905 ) OOVs: 6.71% OOVsSubs: 18.23% OOVsIns: 6.75%
for #5
WER: 47.44 (Ins: 438 Dels: 430 Subs: 2456 Ref: 7007 ) OOVs: 6.66% OOVsSubs: 17.87% OOVsIns: 6.39%
WER: 46.91 (Ins: 413 Dels: 469 Subs: 2405 Ref: 7007 ) OOVs: 6.74% OOVsSubs: 18.50% OOVsIns: 6.54%
WER: 46.88 (Ins: 419 Dels: 433 Subs: 2433 Ref: 7007 ) OOVs: 6.72% OOVsSubs: 18.25% OOVsIns: 6.44%
for #6
WER: 48.44 (Ins: 454 Dels: 462 Subs: 2466 Ref: 6982 ) OOVs: 7.61% OOVsSubs: 19.79% OOVsIns: 9.47%
WER: 47.94 (Ins: 446 Dels: 451 Subs: 2450 Ref: 6982 ) OOVs: 7.61% OOVsSubs: 19.92% OOVsIns: 9.64%
WER: 48.61 (Ins: 418 Dels: 492 Subs: 2484 Ref: 6982 ) OOVs: 7.59% OOVsSubs: 19.69% OOVsIns: 9.81%
for #7
WER: 47.87 (Ins: 419 Dels: 511 Subs: 2489 Ref: 7142 ) OOVs: 6.79% OOVsSubs: 18.48% OOVsIns: 5.97%
WER: 46.42 (Ins: 439 Dels: 468 Subs: 2408 Ref: 7142 ) OOVs: 6.78% OOVsSubs: 18.98% OOVsIns: 6.15%
WER: 47.27 (Ins: 419 Dels: 499 Subs: 2458 Ref: 7142 ) OOVs: 6.76% OOVsSubs: 18.76% OOVsIns: 5.25%
for #8
WER: 46.87 (Ins: 413 Dels: 511 Subs: 2427 Ref: 7149 ) OOVs: 6.95% OOVsSubs: 19.65% OOVsIns: 4.84%
WER: 46.24 (Ins: 397 Dels: 483 Subs: 2426 Ref: 7149 ) OOVs: 6.91% OOVsSubs: 19.41% OOVsIns: 5.79%
WER: 46.41 (Ins: 426 Dels: 473 Subs: 2419 Ref: 7149 ) OOVs: 6.88% OOVsSubs: 19.47% OOVsIns: 4.93%
for #9
WER: 46.30 (Ins: 369 Dels: 481 Subs: 2353 Ref: 6918 ) OOVs: 7.05% OOVsSubs: 19.51% OOVsIns: 7.86%
WER: 46.65 (Ins: 394 Dels: 473 Subs: 2360 Ref: 6918 ) OOVs: 7.08% OOVsSubs: 19.58% OOVsIns: 7.11%
WER: 47.01 (Ins: 360 Dels: 516 Subs: 2376 Ref: 6918 ) OOVs: 7.05% OOVsSubs: 19.36% OOVsIns: 7.78%
for #10
WER: 48.43 (Ins: 586 Dels: 432 Subs: 2411 Ref: 7081 ) OOVs: 7.16% OOVsSubs: 18.79% OOVsIns: 9.22%
WER: 47.72 (Ins: 516 Dels: 444 Subs: 2419 Ref: 7081 ) OOVs: 7.13% OOVsSubs: 18.89% OOVsIns: 9.30%
WER: 48.57 (Ins: 527 Dels: 448 Subs: 2464 Ref: 7081 ) OOVs: 7.13% OOVsSubs: 18.59% OOVsIns: 8.92%
```

## Note

wer++.py ကို run တဲ့အခါမှာ reference ဖိုင်မှာ hyp ဖိုင်တွေမှာ blank line တွေရှိနေရင် "--ignore-blank" option ပေးပြီး run ရင်လည်း တွေ့တိုင်းမှာ အောက်ပါလိုမျိုး message တွေက အကြောင်းတိုင်း အတွက် ပေးမှာ ဖြစ်ပါတယ်။  

```
[WW] Blank line in reference, ignoring it
```

## Reference

[https://github.com/nsmartinez/WERpp](https://github.com/nsmartinez/WERpp)  
