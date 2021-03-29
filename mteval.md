# mteval Installation and Usage

[mteval](https://github.com/odashi/mteval) က machine translation performance ကို တိုင်းတာတဲ့ automatic evaluation matrix တွေထဲက နာမည်ကြီး approach နှစ်ခုဖြစ်တဲ့ [BLEU](https://en.wikipedia.org/wiki/BLEU) နဲ့ [RIBES](https://github.com/nttcslab-nlp/RIBES) အပြင် edit distance based [WER](https://en.wikipedia.org/wiki/Word_error_rate) တွက်တာကိုပါ ပရိုဂရမ်တစ်ပုဒ်ထဲကနေ တပေါင်းထဲလုပ်ပေးနိုင်တဲ့ tool ပါ။ Machine Translation သုတေသန လုပ်နေကြတဲ့သူတွေအတွက် အသုံးဝင်ပါတယ်။    

## git clone

အရင်ဆုံး clone လုပ်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/odashi/mteval
Cloning into 'mteval'...
remote: Enumerating objects: 504, done.
remote: Total 504 (delta 0), reused 0 (delta 0), pack-reused 504
Receiving objects: 100% (504/504), 175.58 KiB | 1021.00 KiB/s, done.
Resolving deltas: 100% (290/290), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd mteval/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval$ mkdir build
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval$ cd build
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build$ cmake ..
-- The CXX compiler identification is GNU 8.4.0
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Boost: /usr/local/lib/cmake/Boost-1.75.0/BoostConfig.cmake (found suitable version "1.75.0", minimum required is "1.48.0") found components: program_options unit_test_framework 
-- Boost include directory: /usr/local/include
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ye/tool/mteval/build
```

## make

-j 8 က လက်ရှိ install လုပ်မယ့် စက်ထဲမှာ CPU ရှစ်လုံး ရှိလို့ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build$ make -j 8
make[1]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
Scanning dependencies of target mteval
make[2]: Leaving directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
[ 23%] Building CXX object mteval/CMakeFiles/mteval.dir/NISTEvaluator.cc.o
[ 23%] Building CXX object mteval/CMakeFiles/mteval.dir/RIBESEvaluator.cc.o
[ 23%] Building CXX object mteval/CMakeFiles/mteval.dir/Dictionary.cc.o
[ 23%] Building CXX object mteval/CMakeFiles/mteval.dir/BLEUEvaluator.cc.o
[ 29%] Building CXX object mteval/CMakeFiles/mteval.dir/Statistics.cc.o
[ 35%] Building CXX object mteval/CMakeFiles/mteval.dir/utils.cc.o
[ 41%] Building CXX object mteval/CMakeFiles/mteval.dir/EvaluatorFactory.cc.o
[ 47%] Building CXX object mteval/CMakeFiles/mteval.dir/WEREvaluator.cc.o
[ 52%] Linking CXX shared library libmteval.so
make[2]: Leaving directory '/home/ye/tool/mteval/build'
[ 52%] Built target mteval
make[2]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
Scanning dependencies of target mteval-pairwise
Scanning dependencies of target mteval-corpus
Scanning dependencies of target statistics_test
make[2]: Leaving directory '/home/ye/tool/mteval/build'
make[2]: Leaving directory '/home/ye/tool/mteval/build'
make[2]: Leaving directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
Scanning dependencies of target mteval-sentence
make[2]: Leaving directory '/home/ye/tool/mteval/build'
make[2]: Entering directory '/home/ye/tool/mteval/build'
[ 64%] Building CXX object test/CMakeFiles/statistics_test.dir/statistics_test.cc.o
[ 64%] Building CXX object bin/CMakeFiles/mteval-corpus.dir/mteval-corpus.cc.o
[ 70%] Building CXX object bin/CMakeFiles/mteval-pairwise.dir/mteval-pairwise.cc.o
[ 76%] Building CXX object bin/CMakeFiles/mteval-sentence.dir/mteval-sentence.cc.o
[ 82%] Linking CXX executable statistics_test
make[2]: Leaving directory '/home/ye/tool/mteval/build'
[ 82%] Built target statistics_test
[ 88%] Linking CXX executable mteval-sentence
[ 94%] Linking CXX executable mteval-corpus
make[2]: Leaving directory '/home/ye/tool/mteval/build'
[ 94%] Built target mteval-sentence
make[2]: Leaving directory '/home/ye/tool/mteval/build'
[ 94%] Built target mteval-corpus
[100%] Linking CXX executable mteval-pairwise
make[2]: Leaving directory '/home/ye/tool/mteval/build'
[100%] Built target mteval-pairwise
make[1]: Leaving directory '/home/ye/tool/mteval/build'
```

## make test

make လုပ်ခဲ့တာ အဆင်ပြေမပြေကို test လုပ်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build$ make test
Running tests...
Test project /home/ye/tool/mteval/build
    Start 1: statistics_test
1/1 Test #1: statistics_test ..................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
```

အထက်ပါ အတိုင်း test pass ဖြစ်တယ်။  

## Preparation 

y-test ဆိုတဲ့ ဖိုလ်ဒါအသစ် တစ်ခုဆောက်ပြီး၊ evaluation လုပ်လို့ရဖို့အတွက် reference ဖိုင်နဲ့ translated output ဖိုင်တွေကို ပြင်ဆင်ပါမယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build$ mkdir y-test
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build$ cd y-test/
```

ref.my က reference ဖိုင်ပါ။ hyp.iter10000.my, hyp.iter5000.my နဲ့ hyp.iter95000.my ဖိုင်တွေက English-Myanmar NMT system တစ်ခုကနေ ဘာသာပြန်ပြီး ထွက်လာတဲ့ translaed output ဖိုင် သုံးဖိုင်ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ls
hyp.iter10000.my  hyp.iter5000.my  hyp.iter95000.my  ref.my
```
mteval ကိုသုံးပြီးတော့ BLEU score, RIBES score နှစ်မျိုးစလုံးကို corpus level တွက်ခိုင်းကြည့်ရအောင်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus -e BLEU RIBES -r ./ref.my -h ./hyp.iter95000.my 
BLEU=0.134730	RIBES=0.621727
```

mteval ကိုသုံးပြီးတော့ BLEU score, RIBES score နှစ်မျိုးစလုံးကို sentence level တွက်ခိုင်းကြည့်ရအောင်။ Sentence level တွက်ခိုင်းရင် စာကြောင်းရေအရေအတွက်ရှိသလောက်ကို တစ်ကြောင်းချင်းတွက်ထုတ်ပေးမှာမို့ output ကို STDOUT ကို မပို့တော့ပဲ ```> ./eval.sentence.out``` ဆိုတဲ့ပုံစံနဲ့ redirection လုပ်ပြီး eval.sentence.out ဖိုင်ထဲမှာ သိမ်းခိုင်းခဲ့ပါတယ်။ ပြီးမှ ဖိုင်content ကို မြင်ရအောင်လို့ head command နဲ့ ၁၀ကြောင်းရိုက်ထုတ်ပြထားပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-sentence -e BLEU RIBES -r ./ref.my -h ./hyp.iter95000.my > ./eval.sentence.out
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ head ./eval.sentence.out 
BLEU=0.168792	RIBES=0.777937
BLEU=0.168662	RIBES=0.860962
BLEU=0.000000	RIBES=0.619974
BLEU=0.095984	RIBES=0.475614
BLEU=0.062082	RIBES=0.515194
BLEU=0.000000	RIBES=0.695593
BLEU=0.125828	RIBES=0.880277
BLEU=0.000000	RIBES=0.533335
BLEU=0.251149	RIBES=0.860091
BLEU=0.386280	RIBES=0.867717
```

ဒီတစ်ခါတော့ mteval-pairwise ဆိုတဲ့ command ကိုသုံးပြီး pairwise evaluation လုပ်ကြည့်ရအောင်။  
-i (iteration), -s (sampling) option တွေကိုလည်း ပေးဖို့လိုအပ်ပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-pairwise -i 1000 -s 100 -e BLEU RIBES -r ./ref.my -h ./hyp.iter{95000,10000}.my
BLEU: p=0.000000 (1000/1000)	RIBES: p=0.000000 (1000/1000)
```

အောက်ပါ usage example ကတော့ hyp.iter5000.my နဲ့ hyp.iter95000.my နှစ်ဖိုင်ကို pairwise evauation လုပ်ထားတဲ့ ရလဒ်ပါ။  
ဒီတစ်ခါတော့ p value က 1.0 အပြည့်ရတာကို တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-pairwise -i 1000 -s 100 -e BLEU RIBES -r ./ref.my -h ./hyp.iter{5000,95000}.my
BLEU: p=1.000000 (0/1000)	RIBES: p=1.000000 (0/1000)
```

အောက်ပါ ဥပမာကတော့ -s 500 ထားပြီး run ခဲ့တဲ့ output ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-pairwise -i 1000 -s 500 -e BLEU RIBES -r ./ref.my -h ./hyp.iter{5000,95000}.my
BLEU: p=1.000000 (0/1000)	RIBES: p=1.000000 (0/1000)
```

mteval command မှာ BLEU score, RIBES score တွက်တဲ့အခါမှာလည်း parameter တချို့ဖြည့်ပြီး အသေးစိတ်တွက်ခိုင်းလို့ ရပါတယ်။ အောက်ပါ ဥပမာနှစ်ခုကတော့ BLEU score တွက်တဲ့အခါမှာ ngram value နဲ့ smoothing value တွေကို parameter ပေးပြီး တွက်ပြထားတာ ဖြစ်ပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus -e BLEU:ngram=5:smooth=1 -r ./ref.my -h ./hyp.iter95000.my 
BLEU=0.102184
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus -e BLEU:ngram=2:smooth=1 -r ./ref.my -h ./hyp.iter95000.my 
BLEU=0.245931
```

နောက်ထပ်အသုံးဝင်တဲ့ option တစ်ခုက --output-stats ဆိုတဲ့ option ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus --output-stats -e BLEU  -r ./ref.my -h ./hyp.iter95000.my | tr '\t' '\n'
BLEU=0.134730
BLEU:len:hyp=45573
BLEU:len:ref=58895
BLEU:ngram:1:hyp=45573
BLEU:ngram:1:match=21230
BLEU:ngram:2:hyp=44555
BLEU:ngram:2:match=10379
BLEU:ngram:3:hyp=43539
BLEU:ngram:3:match=5614
BLEU:ngram:4:hyp=42523
BLEU:ngram:4:match=3224
BLEU:samples=1018
```

Linux command တွေကို မသုံးခင်မှာ command line option နဲ့ syntax တွေကို လေ့လာတဲ့ ပုံစံအတိုင်း --help နဲ့လည်း help screen ခေါ်ကြည့်လို့ ရပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus --help
Calculate corpus-wise evaluation metrics
Usage: mteval-corpus [options] -e EVAL1 EVAL2 ... -r REF -h HYP

Generic options:
  --help                   show this help and exit
  --output-stats           output statistics of evaluators with their scores

Input files:
  -r [ --reference ] arg   (required) reference file
  -h [ --hypothesis ] arg  (required) hypothesis file

Configurations:
  -e [ --evaluator ] arg   (required) evaluator specifications
```

အောက်ပါဥပမာကတော့ mteval-sentence command ကို --help နဲ့ help ခေါ်ကြည့်ရင် မြင်ရမယ့် output ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-sentence --help
Calculate sentence-wise evaluation metrics
Usage: mteval-sentence [options] -e EVAL1 EVAL2 ... -r REF -h HYP

Generic options:
  --help                   show this help and exit
  --output-stats           output statistics of evaluators with their scores

Input files:
  -r [ --reference ] arg   (required) reference file
  -h [ --hypothesis ] arg  (required) hypothesis file

Configurations:
  -e [ --evaluator ] arg   (required) evaluator specifications
```

mteval-pairwise command ရဲ့ help ကိုလည်း ကြည့်ကြည့်ရအောင်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-pairwise --help
Operate pairwise bootstrap resampling test
Usage: mteval-pairwise [options] -i INT -s INT -e EVAL1 EVAL2 ... -r REF -h HYP1 HYP2

Generic options:
  --help                   show this help and exit
  -v [ --verbose ]         show intermediate results

Input files:
  -r [ --reference ] arg   (required) reference file
  -h [ --hypothesis ] arg  (required) 2 hypothesis file

Configurations:
  -e [ --evaluator ] arg   (required) evaluator specifications
  -i [ --iteration ] arg   (required) number of virtual test sets to evaluate
  -s [ --sample ] arg      (required) number of sentences in a virtual test 
                           sets
```

အထူးသဖြင့် Automatic Speech Recognition မှာ အသုံးများတဲ့ WER (Word Error Rate) ကိုလည်း mteval command နဲ့ တွက်ခိုင်းလို့ ရပါတယ်။ Evaluation option ကို -e WER ဆိုပြီး ပေးလိုက်ယုံပါပဲ။  
```tr '\t' '\n'``` ကတော့ ထွက်လာတဲ့ output တွေကို ကြည့်ရတာ အဆင်ပြေအောင် tr command သုံးပြီး "TAB" နဲ့ ခြားထားတာတွေကို "ENTER" နဲ့ အစားထိုးထားတာ ဖြစ်ပါတယ်။  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus -e WER  -r ./ref.my -h ./hyp.iter95000.my | tr '\t' '\n'
WER=0.808147
```

```--output-stats``` option ကိုပါ ထည့်ပြီး သုံးပြထားတာပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mteval/build/y-test$ ../bin/mteval-corpus --output-stats -e WER  -r ./ref.my -h ./hyp.iter95000.my | tr '\t' '\n'
WER=0.808147
WER:distance=48420
WER:samples=1018
WER:score=822.693940
```
