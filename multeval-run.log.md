## git clone

```
(base) ye@:~/tool$ git clone https://github.com/jhclark/multeval
Cloning into 'multeval'...
remote: Enumerating objects: 1136, done.
remote: Total 1136 (delta 0), reused 0 (delta 0), pack-reused 1136
Receiving objects: 100% (1136/1136), 4.66 MiB | 10.50 MiB/s, done.
Resolving deltas: 100% (647/647), done.
(base) ye@:~/tool$ cd multeval/
(base) ye@:~/tool/multeval$ ls
build.xml  CHANGELOG  constants  dist.sh  example  get_deps.sh  lib  LICENSE.txt  multeval.sh  README.md  reg-test  src  table.png
```

## 1st Time Running

1st time running လုပ်ကြည့်တော့ METEOR  မရှိလို့ဆိုပြီး download လုပ်တယ်။  
 
```
(base) ye@:~/tool/multeval$ ./multeval.sh eval --refs example/refs.test2010.lc.tok.en.* \
>                    --hyps-baseline example/hyps.lc.tok.en.baseline.opt* \
>                    --meteor.language en
Existing METEOR installation not found. Performing first-run setup: Downloading and installing METEOR 1.4...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  242M  100  242M    0     0   422k      0  0:09:47  0:09:47 --:--:--  429k
Error: Could not find or load main class multeval.MultEval
Caused by: java.lang.ClassNotFoundException: multeval.MultEval
```

HDD မှာ space သိပ်မရှိတော့လို့ portable HDD ဘက်ကို ရွှေ့ခဲ့တယ်။  
အောက်ပါအတိုင်း multeval ဖိုလ်ဒါကို ~/tool/ အောက် ကနေ /media/ye/project2/tool/ အောက်ကိုရွှေ့ခဲ့...  

```
(base) ye@:~/tool/multeval$ cd ..
(base) ye@:~/tool$ mv ./multeval/ /media/ye/project2/tool/
anymalign/                      gec-ranking/                    mteval-test-log.md              sqlite-autoconf-3370000.tar.gz
audio_exploration-test.txt      GLEU-calc.md                    NLPTools/                       stardict-3/
bitext-tokaligner/              label-studio-installation.log   signalgen/                      word-seg-tool/
ced_word_alignment/             mteval/                         sqlite-autoconf-3370000/        
(base) ye@:~/tool$ mv ./multeval/ /media/ye/project2/tool/
(base) ye@:~/tool$ cd /media/ye/project2/tool/
(base) ye@:/media/ye/project2/tool$ 
```

## Run Ant

Ref: https://github.com/jhclark/multeval/issues/24  
Ref: https://github.com/jhclark/multeval#building  

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs example/refs.test2010.lc.tok.en.* \
>                    --hyps-baseline example/hyps.lc.tok.en.baseline.opt* \
>                    --meteor.language en
Found existing METEOR installation at ./lib/meteor-1.4
Error: Could not find or load main class multeval.MultEval
Caused by: java.lang.ClassNotFoundException: multeval.MultEval
(base) ye@:/media/ye/project2/tool/multeval$ ant
Buildfile: /media/ye/project2/tool/multeval/build.xml

has_meteor:

not_has_meteor:

check_meteor:

compile:
    [mkdir] Created dir: /media/ye/project2/tool/multeval/bin
    [javac] Compiling 38 source files to /media/ye/project2/tool/multeval/bin

jar:
      [jar] Building jar: /media/ye/project2/tool/multeval/multeval-0.5.1.jar

BUILD SUCCESSFUL
Total time: 1 second
(base) ye@:/media/ye/project2/tool/multeval$
```

## 1st Time Running Success

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs example/refs.test2010.lc.tok.en.*                    --hyps-baseline example/hyps.lc.tok.en.baseline.opt*                    --meteor.language en
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.31 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt0
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt1
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt2
Reading non-laced references file /media/ye/project2/tool/multeval/example/refs.test2010.lc.tok.en.0
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 3.53 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 18.526808
RESULT: baseline: BLEU: MEDIAN: 18.538889
RESULT: baseline: BLEU: STDDEV: 0.057280
RESULT: baseline: BLEU: MIN: 18.464451
RESULT: baseline: BLEU: MAX: 18.577084
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.308651
RESULT: baseline: METEOR: MEDIAN: 29.330036
RESULT: baseline: METEOR: STDDEV: 0.046259
RESULT: baseline: METEOR: MIN: 29.255569
RESULT: baseline: METEOR: MAX: 29.340350
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 65.656694
RESULT: baseline: TER: MEDIAN: 65.560582
RESULT: baseline: TER: STDDEV: 0.203397
RESULT: baseline: TER: MIN: 65.519164
RESULT: baseline: TER: MAX: 65.890337
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 107.544525
RESULT: baseline: Length: MEDIAN: 107.482397
RESULT: baseline: Length: STDDEV: 0.121665
RESULT: baseline: Length: MIN: 107.466467
RESULT: baseline: Length: MAX: 107.684710
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [the x 1931, , x 1510, of x 916, in x 767, ' x 576, to x 483, a x 375, on x 325, - x 306, is x 267]
Top unmatched reference words accoring to METEOR: [, x 590, " x 520, to x 428, of x 340, 's x 339, a x 251, the x 229, for x 229, - x 201, in x 201]
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 1; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 1; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 1; opt run 3 of 3)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 18.526396
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 0.263162
RESULT: baseline: BLEU: RESAMPLED_MIN: 17.281689
RESULT: baseline: BLEU: RESAMPLED_MAX: 19.754815
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.308571
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.147872
RESULT: baseline: METEOR: RESAMPLED_MIN: 28.678957
RESULT: baseline: METEOR: RESAMPLED_MAX: 30.023805
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 65.656587
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 0.367371
RESULT: baseline: TER: RESAMPLED_MIN: 64.066615
RESULT: baseline: TER: RESAMPLED_MAX: 67.460203
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 107.545687
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.360997
RESULT: baseline: Length: RESAMPLED_MIN: 106.159558
RESULT: baseline: Length: RESAMPLED_MAX: 109.098979
Performed bootstrap resampling in 5.77 s
n=3            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       18.5 (0.3/0.1/-)       29.3 (0.1/0.0/-)       65.7 (0.4/0.2/-)       107.5 (0.4/0.1/-)      
(base) ye@:/media/ye/project2/tool/multeval$
```

## Comparing Several Systems

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs example/refs.test2010.lc.tok.en.* \
>                    --hyps-baseline example/hyps.lc.tok.en.baseline.opt* \
>                    --hyps-sys1 example/hyps.lc.tok.en.sys1.opt* \
>                    --hyps-sys2 example/hyps.lc.tok.en.sys2.opt* \
>                    --meteor.language en
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 4.95 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt0
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt1
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt2
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt0
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt1
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt2
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt0
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt1
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt2
Reading non-laced references file /media/ye/project2/tool/multeval/example/refs.test2010.lc.tok.en.0
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 5.49 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 18.526808
RESULT: baseline: BLEU: MEDIAN: 18.538889
RESULT: baseline: BLEU: STDDEV: 0.057280
RESULT: baseline: BLEU: MIN: 18.464451
RESULT: baseline: BLEU: MAX: 18.577084
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 1: BLEU: AVG: 18.813470
RESULT: system 1: BLEU: MEDIAN: 18.979487
RESULT: system 1: BLEU: STDDEV: 0.294001
RESULT: system 1: BLEU: MIN: 18.474014
RESULT: system 1: BLEU: MAX: 18.986909
RESULT: system 1: BLEU: MEDIAN_IDX: 2.000000
RESULT: system 2: BLEU: AVG: 18.526808
RESULT: system 2: BLEU: MEDIAN: 18.538889
RESULT: system 2: BLEU: STDDEV: 0.057280
RESULT: system 2: BLEU: MIN: 18.464451
RESULT: system 2: BLEU: MAX: 18.577084
RESULT: system 2: BLEU: MEDIAN_IDX: 0.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.308651
RESULT: baseline: METEOR: MEDIAN: 29.330036
RESULT: baseline: METEOR: STDDEV: 0.046259
RESULT: baseline: METEOR: MIN: 29.255569
RESULT: baseline: METEOR: MAX: 29.340350
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 30.290422
RESULT: system 1: METEOR: MEDIAN: 30.304878
RESULT: system 1: METEOR: STDDEV: 0.092845
RESULT: system 1: METEOR: MIN: 30.191196
RESULT: system 1: METEOR: MAX: 30.375191
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 2: METEOR: AVG: 29.308651
RESULT: system 2: METEOR: MEDIAN: 29.330036
RESULT: system 2: METEOR: STDDEV: 0.046259
RESULT: system 2: METEOR: MIN: 29.255569
RESULT: system 2: METEOR: MAX: 29.340350
RESULT: system 2: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 65.656694
RESULT: baseline: TER: MEDIAN: 65.560582
RESULT: baseline: TER: STDDEV: 0.203397
RESULT: baseline: TER: MIN: 65.519164
RESULT: baseline: TER: MAX: 65.890337
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
RESULT: system 1: TER: AVG: 64.816644
RESULT: system 1: TER: MEDIAN: 64.932934
RESULT: system 1: TER: STDDEV: 0.589323
RESULT: system 1: TER: MIN: 64.177844
RESULT: system 1: TER: MAX: 65.339153
RESULT: system 1: TER: MEDIAN_IDX: 2.000000
RESULT: system 2: TER: AVG: 65.656694
RESULT: system 2: TER: MEDIAN: 65.560582
RESULT: system 2: TER: STDDEV: 0.203397
RESULT: system 2: TER: MIN: 65.519164
RESULT: system 2: TER: MAX: 65.890337
RESULT: system 2: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 107.544525
RESULT: baseline: Length: MEDIAN: 107.482397
RESULT: baseline: Length: STDDEV: 0.121665
RESULT: baseline: Length: MIN: 107.466467
RESULT: baseline: Length: MAX: 107.684710
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
RESULT: system 1: Length: AVG: 107.700640
RESULT: system 1: Length: MEDIAN: 108.092522
RESULT: system 1: Length: STDDEV: 0.724763
RESULT: system 1: Length: MIN: 106.864307
RESULT: system 1: Length: MAX: 108.145092
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
RESULT: system 2: Length: AVG: 107.544525
RESULT: system 2: Length: MEDIAN: 107.482397
RESULT: system 2: Length: STDDEV: 0.121665
RESULT: system 2: Length: MIN: 107.466467
RESULT: system 2: Length: MAX: 107.684710
RESULT: system 2: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [the x 1931, , x 1510, of x 916, in x 767, ' x 576, to x 483, a x 375, on x 325, - x 306, is x 267]
Top unmatched reference words accoring to METEOR: [, x 590, " x 520, to x 428, of x 340, 's x 339, a x 251, the x 229, for x 229, - x 201, in x 201]
Top unmatched hypothesis words accoring to METEOR: [the x 1729, , x 1190, of x 823, in x 665, ' x 564, to x 442, a x 331, on x 301, - x 281, that x 250]
Top unmatched reference words accoring to METEOR: [, x 755, " x 515, to x 461, of x 348, 's x 332, the x 294, a x 270, for x 241, in x 209, - x 197]
Top unmatched hypothesis words accoring to METEOR: [the x 1931, , x 1510, of x 916, in x 767, ' x 576, to x 483, a x 375, on x 325, - x 306, is x 267]
Top unmatched reference words accoring to METEOR: [, x 590, " x 520, to x 428, of x 340, 's x 339, a x 251, the x 229, for x 229, - x 201, in x 201]
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 3)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 18.528480
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 0.261707
RESULT: baseline: BLEU: RESAMPLED_MIN: 17.428218
RESULT: baseline: BLEU: RESAMPLED_MAX: 19.551606
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.309785
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.148159
RESULT: baseline: METEOR: RESAMPLED_MIN: 28.661360
RESULT: baseline: METEOR: RESAMPLED_MAX: 29.863000
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 65.654634
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 0.365092
RESULT: baseline: TER: RESAMPLED_MIN: 64.132279
RESULT: baseline: TER: RESAMPLED_MAX: 67.158132
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 107.544498
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.358540
RESULT: baseline: Length: RESAMPLED_MIN: 105.946717
RESULT: baseline: Length: RESAMPLED_MAX: 109.017061
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 3)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 18.814439
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 0.262831
RESULT: system 1: BLEU: RESAMPLED_MIN: 17.455487
RESULT: system 1: BLEU: RESAMPLED_MAX: 19.926694
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 30.291488
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.144194
RESULT: system 1: METEOR: RESAMPLED_MIN: 29.644102
RESULT: system 1: METEOR: RESAMPLED_MAX: 30.973416
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 64.814568
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 0.365808
RESULT: system 1: TER: RESAMPLED_MIN: 62.800683
RESULT: system 1: TER: RESAMPLED_MAX: 66.592127
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 107.703041
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.346143
RESULT: system 1: Length: RESAMPLED_MIN: 105.365993
RESULT: system 1: Length: RESAMPLED_MAX: 109.797308
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 3)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 18.524246
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 0.264358
RESULT: system 2: BLEU: RESAMPLED_MIN: 17.438310
RESULT: system 2: BLEU: RESAMPLED_MAX: 19.640820
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 29.307265
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.149514
RESULT: system 2: METEOR: RESAMPLED_MIN: 28.671829
RESULT: system 2: METEOR: RESAMPLED_MAX: 30.026695
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 65.657786
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 0.368520
RESULT: system 2: TER: RESAMPLED_MIN: 64.100710
RESULT: system 2: TER: RESAMPLED_MAX: 67.263569
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 107.545073
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.362505
RESULT: system 2: Length: RESAMPLED_MIN: 106.001974
RESULT: system 2: Length: RESAMPLED_MAX: 109.051413
Performed bootstrap resampling in 17.1 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.000200
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.090391
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.000100
RESULT: system 2: METEOR: P_VALUE: 0.000100
RESULT: system 2: TER: P_VALUE: 0.000100
RESULT: system 2: Length: P_VALUE: 0.000100
Performed approximate randomization in 20.4 s
n=3            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       18.5 (0.3/0.1/-)       29.3 (0.1/0.0/-)       65.7 (0.4/0.2/-)       107.5 (0.4/0.1/-)      
system 1       18.8 (0.3/0.3/0.00)    30.3 (0.1/0.1/0.00)    64.8 (0.4/0.6/0.00)    107.7 (0.3/0.7/0.09)   
system 2       18.5 (0.3/0.1/0.00)    29.3 (0.1/0.0/0.00)    65.7 (0.4/0.2/0.00)    107.5 (0.4/0.1/0.00)   
(base) ye@:/media/ye/project2/tool/multeval$
```

## Option for Include Latex Table, Ranked and Sentence-Level Metric Score

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs example/refs.test2010.lc.tok.en.* \
>                    --hyps-baseline example/hyps.lc.tok.en.baseline.opt* \
>                    --hyps-sys1 example/hyps.lc.tok.en.sys1.opt* \
>                    --hyps-sys2 example/hyps.lc.tok.en.sys2.opt* \
>                    --meteor.language en \
>                    --latex table.tex \
>                    --rankDir rank \
>                    --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 4.95 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt0
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt1
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.baseline.opt2
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt0
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt1
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys1.opt2
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt0
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt1
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/tool/multeval/example/hyps.lc.tok.en.sys2.opt2
Reading non-laced references file /media/ye/project2/tool/multeval/example/refs.test2010.lc.tok.en.0
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 5.63 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 18.526808
RESULT: baseline: BLEU: MEDIAN: 18.538889
RESULT: baseline: BLEU: STDDEV: 0.057280
RESULT: baseline: BLEU: MIN: 18.464451
RESULT: baseline: BLEU: MAX: 18.577084
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 1: BLEU: AVG: 18.813470
RESULT: system 1: BLEU: MEDIAN: 18.979487
RESULT: system 1: BLEU: STDDEV: 0.294001
RESULT: system 1: BLEU: MIN: 18.474014
RESULT: system 1: BLEU: MAX: 18.986909
RESULT: system 1: BLEU: MEDIAN_IDX: 2.000000
RESULT: system 2: BLEU: AVG: 18.526808
RESULT: system 2: BLEU: MEDIAN: 18.538889
RESULT: system 2: BLEU: STDDEV: 0.057280
RESULT: system 2: BLEU: MIN: 18.464451
RESULT: system 2: BLEU: MAX: 18.577084
RESULT: system 2: BLEU: MEDIAN_IDX: 0.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.308651
RESULT: baseline: METEOR: MEDIAN: 29.330036
RESULT: baseline: METEOR: STDDEV: 0.046259
RESULT: baseline: METEOR: MIN: 29.255569
RESULT: baseline: METEOR: MAX: 29.340350
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 30.290422
RESULT: system 1: METEOR: MEDIAN: 30.304878
RESULT: system 1: METEOR: STDDEV: 0.092845
RESULT: system 1: METEOR: MIN: 30.191196
RESULT: system 1: METEOR: MAX: 30.375191
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 2: METEOR: AVG: 29.308651
RESULT: system 2: METEOR: MEDIAN: 29.330036
RESULT: system 2: METEOR: STDDEV: 0.046259
RESULT: system 2: METEOR: MIN: 29.255569
RESULT: system 2: METEOR: MAX: 29.340350
RESULT: system 2: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 65.656694
RESULT: baseline: TER: MEDIAN: 65.560582
RESULT: baseline: TER: STDDEV: 0.203397
RESULT: baseline: TER: MIN: 65.519164
RESULT: baseline: TER: MAX: 65.890337
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
RESULT: system 1: TER: AVG: 64.816644
RESULT: system 1: TER: MEDIAN: 64.932934
RESULT: system 1: TER: STDDEV: 0.589323
RESULT: system 1: TER: MIN: 64.177844
RESULT: system 1: TER: MAX: 65.339153
RESULT: system 1: TER: MEDIAN_IDX: 2.000000
RESULT: system 2: TER: AVG: 65.656694
RESULT: system 2: TER: MEDIAN: 65.560582
RESULT: system 2: TER: STDDEV: 0.203397
RESULT: system 2: TER: MIN: 65.519164
RESULT: system 2: TER: MAX: 65.890337
RESULT: system 2: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 107.544525
RESULT: baseline: Length: MEDIAN: 107.482397
RESULT: baseline: Length: STDDEV: 0.121665
RESULT: baseline: Length: MIN: 107.466467
RESULT: baseline: Length: MAX: 107.684710
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
RESULT: system 1: Length: AVG: 107.700640
RESULT: system 1: Length: MEDIAN: 108.092522
RESULT: system 1: Length: STDDEV: 0.724763
RESULT: system 1: Length: MIN: 106.864307
RESULT: system 1: Length: MAX: 108.145092
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
RESULT: system 2: Length: AVG: 107.544525
RESULT: system 2: Length: MEDIAN: 107.482397
RESULT: system 2: Length: STDDEV: 0.121665
RESULT: system 2: Length: MIN: 107.466467
RESULT: system 2: Length: MAX: 107.684710
RESULT: system 2: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [the x 1931, , x 1510, of x 916, in x 767, ' x 576, to x 483, a x 375, on x 325, - x 306, is x 267]
Top unmatched reference words accoring to METEOR: [, x 590, " x 520, to x 428, of x 340, 's x 339, a x 251, the x 229, for x 229, - x 201, in x 201]
Top unmatched hypothesis words accoring to METEOR: [the x 1729, , x 1190, of x 823, in x 665, ' x 564, to x 442, a x 331, on x 301, - x 281, that x 250]
Top unmatched reference words accoring to METEOR: [, x 755, " x 515, to x 461, of x 348, 's x 332, the x 294, a x 270, for x 241, in x 209, - x 197]
Top unmatched hypothesis words accoring to METEOR: [the x 1931, , x 1510, of x 916, in x 767, ' x 576, to x 483, a x 375, on x 325, - x 306, is x 267]
Top unmatched reference words accoring to METEOR: [, x 590, " x 520, to x 428, of x 340, 's x 339, a x 251, the x 229, for x 229, - x 201, in x 201]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 3)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 18.526850
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 0.262580
RESULT: baseline: BLEU: RESAMPLED_MIN: 17.396280
RESULT: baseline: BLEU: RESAMPLED_MAX: 19.635494
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.309410
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.149686
RESULT: baseline: METEOR: RESAMPLED_MIN: 28.644189
RESULT: baseline: METEOR: RESAMPLED_MAX: 29.922597
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 65.655327
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 0.368438
RESULT: baseline: TER: RESAMPLED_MIN: 64.132378
RESULT: baseline: TER: RESAMPLED_MAX: 67.428507
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 107.542772
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.360986
RESULT: baseline: Length: RESAMPLED_MIN: 105.949217
RESULT: baseline: Length: RESAMPLED_MAX: 109.116758
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 3)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 18.812016
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 0.262978
RESULT: system 1: BLEU: RESAMPLED_MIN: 17.512302
RESULT: system 1: BLEU: RESAMPLED_MAX: 20.048600
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 30.290100
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.143888
RESULT: system 1: METEOR: RESAMPLED_MIN: 29.596009
RESULT: system 1: METEOR: RESAMPLED_MAX: 30.919994
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 64.817451
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 0.365273
RESULT: system 1: TER: RESAMPLED_MIN: 62.858652
RESULT: system 1: TER: RESAMPLED_MAX: 66.727891
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 107.698938
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.346146
RESULT: system 1: Length: RESAMPLED_MIN: 105.296198
RESULT: system 1: Length: RESAMPLED_MAX: 109.517207
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 3)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 3)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 18.527854
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 0.262120
RESULT: system 2: BLEU: RESAMPLED_MIN: 17.466415
RESULT: system 2: BLEU: RESAMPLED_MAX: 19.607047
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 29.309215
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.148626
RESULT: system 2: METEOR: RESAMPLED_MIN: 28.693230
RESULT: system 2: METEOR: RESAMPLED_MAX: 29.996132
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 65.656725
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 0.365012
RESULT: system 2: TER: RESAMPLED_MIN: 64.141542
RESULT: system 2: TER: RESAMPLED_MAX: 67.345573
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 107.546102
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.360784
RESULT: system 2: Length: RESAMPLED_MIN: 105.846961
RESULT: system 2: Length: RESAMPLED_MAX: 109.084165
Performed bootstrap resampling in 17.8 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.000600
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.091491
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.000100
RESULT: system 2: METEOR: P_VALUE: 0.000100
RESULT: system 2: TER: P_VALUE: 0.000100
RESULT: system 2: Length: P_VALUE: 0.000100
Performed approximate randomization in 23.1 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=3            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       18.5 (0.3/0.1/-)       29.3 (0.1/0.0/-)       65.7 (0.4/0.2/-)       107.5 (0.4/0.1/-)      
system 1       18.8 (0.3/0.3/0.00)    30.3 (0.1/0.1/0.00)    64.8 (0.4/0.6/0.00)    107.7 (0.3/0.7/0.09)   
system 2       18.5 (0.3/0.1/0.00)    29.3 (0.1/0.0/0.00)    65.7 (0.4/0.2/0.00)    107.5 (0.4/0.1/0.00)   
```

Latex table ကိုလည်း တွေ့ရလိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/tool/multeval$ ls
bin        CHANGELOG  dist.sh  get_deps.sh  LICENSE.txt         multeval.sh  README.md  sentLevel  table.png
build.xml  constants  example  lib          multeval-0.5.1.jar  rank         reg-test   src        table.tex
(base) ye@:/media/ye/project2/tool/multeval$ 
```

table.tex ကို cat လုပ်ကြည့်ရင်...  
အောက်ပါအတိုင်း တွေ့ရလိမ့်မယ်။ စာတမ်းရေးတဲ့သူတွေအတွက် အသုံးဝယ်လိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/tool/multeval$ cat table.tex 
\begin{table}[htb]
\begin{center}
\begin{footnotesize}
\begin{tabular}{|l|l|l|l|l|l|}
\hline
\bf Metric & \bf System & \bf Avg & \bf $\overline{s}_{\text{sel}}$ & \bf $s_{\text{Test}}$ & \bf $p$-value \\
\hline
\multirow{3}{*}{BLEU $\uparrow$}
& baseline & 18.5 & 0.3 & 0.1 & - \\
& system 1 & 18.8 & 0.3 & 0.3 & 0.00 \\
& system 2 & 18.5 & 0.3 & 0.1 & 0.00 \\
\hline
\multirow{3}{*}{METEOR $\uparrow$}
& baseline & 29.3 & 0.1 & 0.0 & - \\
& system 1 & 30.3 & 0.1 & 0.1 & 0.00 \\
& system 2 & 29.3 & 0.1 & 0.0 & 0.00 \\
\hline
\multirow{3}{*}{TER $\downarrow$}
& baseline & 65.7 & 0.4 & 0.2 & - \\
& system 1 & 64.8 & 0.4 & 0.6 & 0.00 \\
& system 2 & 65.7 & 0.4 & 0.2 & 0.00 \\
\hline
\multirow{3}{*}{Length }
& baseline & 107.5 & 0.4 & 0.1 & - \\
& system 1 & 107.7 & 0.3 & 0.7 & 0.09 \\
& system 2 & 107.5 & 0.4 & 0.1 & 0.00 \\
\hline
\end{tabular}
\end{footnotesize}
\end{center}
\caption{\label{tab:scores} Metric scores for all systems: jBLEU V0.1.1 (an exact reimplementation of NIST's mteval-v13.pl without tokenization); Meteor V1.4 en on rank task with all default modules NOT ignoring punctuation; Translation Error Rate (TER) V0.8.0; Hypothesis length over reference length as a percent; . p-values are relative to baseline and indicate whether a difference of this magnitude (between the baseline and the system on that line) is likely to be generated again by some random process (a randomized optimizer). Metric scores are averages over multiple runs. $s_{sel}$ indicates the variance due to test set selection and has nothing to do with optimizer instability.}
\end{table}
(base) ye@:/media/ye/project2/tool/multeval$
```

## Call Help

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Usage: program <module_name> [options...]

=== METEOR ===
-w [--meteor.weights]             Specify module weights (overrides default)  [optional]
-a [--meteor.paraphraseFile]      If default is not desired  [optional]
-x [--meteor.beamSize]            Specify beam size (overrides default) 
-l [--meteor.language]            Two-letter language code of a supported METEOR language (e.g. 'en') 
-s [--meteor.synonymDirectory]    If default is not desired (NOTE: This option has a different short flag than stand-alone METEOR)  [optional]
-t [--meteor.task]                One of: rank adq hter tune (Rank is generally a good choice) 
-k [--meteor.keepPunctuation]     Consider punctuation when aligning sentences (if false, the meteor tokenizer will be run, after which punctuation will be removed) 
-p [--meteor.params]              Custom parameters of the form 'alpha beta gamma' (overrides default)  [optional]
-m [--meteor.modules]             Specify modules. (overrides default) Any of: exact stem synonym paraphrase  [optional]

=== TER ===
-I [--ter.insertCost]             Insert cost for TER 
-d [--ter.maxShiftDistance]       Maximum shift distance for TER 
-T [--ter.shiftCost]              Shift cost for TER 
-M [--ter.matchCost]              Match cost for TER 
-B [--ter.substituteCost]         Substitute cost for TER 
-b [--ter.beamWidth]              Beam width for TER 
-P [--ter.punctuation]            Use punctuation in TER? 
-D [--ter.deleteCost]             Delete cost for TER 

=== BLEU ===
-v [--bleu.verbosity]             Verbosity level (Integer: 0-1) 

=== MultEvalModule (for eval module) ===
-H [--hyps-sys]                   Space-delimited list of files containing tokenized, fullform hypotheses, one per line 
-F [--fullLatexDoc]               Output a fully compilable Latex document instead of just the table alone  [optional]
-D [--debug]                      Show debugging output?  [optional]
-S [--sentLevelDir]               Score the hypotheses of each system at the sentence-level and output to the specified directory for analysis  [optional]
-t [--threads]                    How many threads should we use? Thread-unsafe metrics will be run in a separate thread. (Zero means all available cores)  [optional]
-B [--hyps-baseline]              Space-delimited list of files containing tokenized, fullform hypotheses, one per line 
-L [--latex]                      Latex-formatted table including measures that are commonly (or should be commonly) reported  [optional]
-r [--rankDir]                    Rank hypotheses of median optimization run of each system with regard to improvement/decline over median baseline system and output to the specified directory for analysis  [optional]
-b [--boot-samples]               Number of bootstrap replicas to draw during bootstrap resampling to estimate standard deviation for each system 
-s [--ar-shuffles]                Number of shuffles to perform to estimate p-value during approximate randomization test system *PAIR* 
-R [--refs]                       Space-delimited list of files containing tokenized, fullform references, one per line 
-o [--metrics]                    Space-delimited list of metrics to use. Any of: bleu, meteor, ter, length 
-v [--verbosity]                  Verbosity level (Integer: 0-1) 

--help                        help message

Failed to specify required options: [refs, hyps-baseline]
(base) ye@:/media/ye/project2/tool/multeval$
```

## Running for bk-my-rk

baseline ကို ဖြုတ်ပြီး run ကြည့်ခဲ့...   
ပြီးတော့ meteor.language en ကိုလည်း ဖြုတ်ခဲ့တယ်။  

```
--hyps-baseline example/hyps.lc.tok.en.baseline.opt* \
--meteor.language en \
```

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/test.rk \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo-sentence.myrk.rk \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo.rk \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```                 

အောက်ပါ error ပေးပြီး help screen တက်လာတယ်။   

```
Failed to specify required options: [hyps-baseline]
```

အဲဒါကြောင်း hyp1, hyp2 နှစ်ခုတည်းကို နှိုင်းယှဉ်တာ လုပ်လို့ မရပဲနဲ့ baseline ကိုပါ ထည့်ပေးရမယ်ဆိုတဲ့ သဘော...  
အောက်ပါ command နဲ့ ထပ် run ခဲ့တယ်  

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/test.rk \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/baseline/baseline-bk-my-rk.test.cleaned.1 \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo-sentence.myrk.rk \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo.rk \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```   

အောက်ပါ error ပေးတယ် ဆိုတော့ language ကိုလည်း သတ်မှတ်ပေးရမယ်ဆိုတဲ့ ပုံစံ...  

```
Failed to specify required options: [meteor.language]
```

ရခိုင်စာအတွက်က ဘယ်လို သတ်မှတ်မှာလဲ?! မြန်မာစာ အတွက် ဗမာစာအတွက်ကော METEOR မှာက သတ်မှတ်ပြီးသားရှိလို့လား?! ?!  
Ref: https://www.cs.cmu.edu/~alavie/METEOR/README.html

```-l other``` ဆိုတဲ့ option ရှိတယ်။

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/test.rk \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/baseline/baseline-bk-my-rk.test.cleaned.1 \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo-sentence.myrk.rk \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo.rk \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```

အထက်ပါ command နဲ့ option တွေနဲ့ ဆိုရင် run လို့တော့ ရသွားပြီ။ သို့သော် အောက်ပါအတိုင်း optimizer ကို တစ်ခုထက်မက ပိုသုံးဖို့ message ပေးတယ်။  

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/test.rk \
> --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/baseline/baseline-bk-my-rk.test.cleaned.1 \
> --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo-sentence.myrk.rk \
> --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo.rk \
> --meteor.language en \
> --latex table.tex \
> --rankDir rank \
> --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.55 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/baseline/baseline-bk-my-rk.test.cleaned.1
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo-sentence.myrk.rk
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/hypo.rk
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot/bk-my-rk/test.rk
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 280 ms
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 35.326908
RESULT: baseline: BLEU: MEDIAN: 35.326908
RESULT: baseline: BLEU: STDDEV: NaN
RESULT: baseline: BLEU: MIN: 35.326908
RESULT: baseline: BLEU: MAX: 35.326908
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 1: BLEU: AVG: 35.489542
RESULT: system 1: BLEU: MEDIAN: 35.489542
RESULT: system 1: BLEU: STDDEV: NaN
RESULT: system 1: BLEU: MIN: 35.489542
RESULT: system 1: BLEU: MAX: 35.489542
RESULT: system 1: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 2: BLEU: AVG: 37.301253
RESULT: system 2: BLEU: MEDIAN: 37.301253
RESULT: system 2: BLEU: STDDEV: NaN
RESULT: system 2: BLEU: MIN: 37.301253
RESULT: system 2: BLEU: MAX: 37.301253
RESULT: system 2: BLEU: MEDIAN_IDX: 0.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 31.349773
RESULT: baseline: METEOR: MEDIAN: 31.349773
RESULT: baseline: METEOR: STDDEV: NaN
RESULT: baseline: METEOR: MIN: 31.349773
RESULT: baseline: METEOR: MAX: 31.349773
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 31.542302
RESULT: system 1: METEOR: MEDIAN: 31.542302
RESULT: system 1: METEOR: STDDEV: NaN
RESULT: system 1: METEOR: MIN: 31.542302
RESULT: system 1: METEOR: MAX: 31.542302
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 2: METEOR: AVG: 31.873140
RESULT: system 2: METEOR: MEDIAN: 31.873140
RESULT: system 2: METEOR: STDDEV: NaN
RESULT: system 2: METEOR: MIN: 31.873140
RESULT: system 2: METEOR: MAX: 31.873140
RESULT: system 2: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 46.429089
RESULT: baseline: TER: MEDIAN: 46.429089
RESULT: baseline: TER: STDDEV: NaN
RESULT: baseline: TER: MIN: 46.429089
RESULT: baseline: TER: MAX: 46.429089
RESULT: baseline: TER: MEDIAN_IDX: 0.000000
RESULT: system 1: TER: AVG: 45.907576
RESULT: system 1: TER: MEDIAN: 45.907576
RESULT: system 1: TER: STDDEV: NaN
RESULT: system 1: TER: MIN: 45.907576
RESULT: system 1: TER: MAX: 45.907576
RESULT: system 1: TER: MEDIAN_IDX: 0.000000
RESULT: system 2: TER: AVG: 44.531363
RESULT: system 2: TER: MEDIAN: 44.531363
RESULT: system 2: TER: STDDEV: NaN
RESULT: system 2: TER: MIN: 44.531363
RESULT: system 2: TER: MAX: 44.531363
RESULT: system 2: TER: MEDIAN_IDX: 0.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 102.071563
RESULT: baseline: Length: MEDIAN: 102.071563
RESULT: baseline: Length: STDDEV: NaN
RESULT: baseline: Length: MIN: 102.071563
RESULT: baseline: Length: MAX: 102.071563
RESULT: baseline: Length: MEDIAN_IDX: 0.000000
RESULT: system 1: Length: AVG: 101.694915
RESULT: system 1: Length: MEDIAN: 101.694915
RESULT: system 1: Length: STDDEV: NaN
RESULT: system 1: Length: MIN: 101.694915
RESULT: system 1: Length: MAX: 101.694915
RESULT: system 1: Length: MEDIAN_IDX: 0.000000
RESULT: system 2: Length: AVG: 100.724323
RESULT: system 2: Length: MEDIAN: 100.724323
RESULT: system 2: Length: STDDEV: NaN
RESULT: system 2: Length: MIN: 100.724323
RESULT: system 2: Length: MAX: 100.724323
RESULT: system 2: Length: MEDIAN_IDX: 0.000000
Top unmatched hypothesis words accoring to METEOR: [။ x 148, ကို x 94, ရေ x 87, ငါ x 41, ပါ x 39, က x 38, တိ x 36, မ x 31, လေး x 31, ဖို့ x 27]
Top unmatched reference words accoring to METEOR: [။ x 60, ကျွန်တော် x 45, ကို x 42, မ x 29, ပါလား x 27, ရေ x 26, မင်း x 26, က x 25, ရို့ x 24, စွာလေး x 23]
Top unmatched hypothesis words accoring to METEOR: [။ x 155, ကို x 87, ရေ x 86, ပါ x 45, က x 37, ငါ x 32, လေး x 32, တိ x 31, ကျွန်တော် x 31, မ x 29]
Top unmatched reference words accoring to METEOR: [ကို x 48, ကျွန်တော် x 42, ။ x 33, ရို့ x 32, မ x 30, ရေ x 29, က x 25, သူ x 25, မင်း x 24, ပါ x 22]
Top unmatched hypothesis words accoring to METEOR: [။ x 152, ရေ x 73, ကို x 69, က x 38, ပါ x 36, လေး x 32, တိ x 30, ငါ x 29, ထိုမချေ x 25, မ x 24]
Top unmatched reference words accoring to METEOR: [ကို x 47, ကျွန်တော် x 41, ။ x 37, ရို့ x 32, မ x 29, မင်း x 28, က x 26, ရေ x 25, သူ x 23, ပါလား x 22]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 1)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 35.325130
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.013256
RESULT: baseline: BLEU: RESAMPLED_MIN: 31.738101
RESULT: baseline: BLEU: RESAMPLED_MAX: 39.489174
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 31.347290
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.477155
RESULT: baseline: METEOR: RESAMPLED_MIN: 29.621471
RESULT: baseline: METEOR: RESAMPLED_MAX: 33.046635
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 46.434142
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 0.933237
RESULT: baseline: TER: RESAMPLED_MIN: 43.178808
RESULT: baseline: TER: RESAMPLED_MAX: 50.183742
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 102.071242
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.726010
RESULT: baseline: Length: RESAMPLED_MIN: 99.456288
RESULT: baseline: Length: RESAMPLED_MAX: 105.041770
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 1)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 35.488517
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.009612
RESULT: system 1: BLEU: RESAMPLED_MIN: 31.206507
RESULT: system 1: BLEU: RESAMPLED_MAX: 39.555181
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 31.541671
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.475638
RESULT: system 1: METEOR: RESAMPLED_MIN: 29.629976
RESULT: system 1: METEOR: RESAMPLED_MAX: 33.571721
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 45.909244
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 0.930804
RESULT: system 1: TER: RESAMPLED_MIN: 42.325718
RESULT: system 1: TER: RESAMPLED_MAX: 49.755325
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.691467
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.745362
RESULT: system 1: Length: RESAMPLED_MIN: 99.270595
RESULT: system 1: Length: RESAMPLED_MAX: 104.495038
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 1)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 37.271323
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 1.022579
RESULT: system 2: BLEU: RESAMPLED_MIN: 33.731130
RESULT: system 2: BLEU: RESAMPLED_MAX: 41.408085
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 31.868386
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.482387
RESULT: system 2: METEOR: RESAMPLED_MIN: 30.124959
RESULT: system 2: METEOR: RESAMPLED_MAX: 33.692022
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 44.544365
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 0.915057
RESULT: system 2: TER: RESAMPLED_MIN: 40.981220
RESULT: system 2: TER: RESAMPLED_MAX: 47.822300
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 100.723404
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.693006
RESULT: system 2: Length: RESAMPLED_MIN: 98.111600
RESULT: system 2: Length: RESAMPLED_MAX: 103.222945
Performed bootstrap resampling in 2.60 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.752725
RESULT: system 1: METEOR: P_VALUE: 0.411659
RESULT: system 1: TER: P_VALUE: 0.176082
RESULT: system 1: Length: P_VALUE: 0.138186
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.000400
RESULT: system 2: METEOR: P_VALUE: 0.028197
RESULT: system 2: TER: P_VALUE: 0.000100
RESULT: system 2: Length: P_VALUE: 0.000100
Performed approximate randomization in 1.39 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=1            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       35.3 (1.0/*/-)         31.3 (0.5/*/-)         46.4 (0.9/*/-)         102.1 (0.7/*/-)        
system 1       35.5 (1.0/*/**)        31.5 (0.5/*/**)        45.9 (0.9/*/**)        101.7 (0.7/*/**)       
system 2       37.3 (1.0/*/**)        31.9 (0.5/*/**)        44.5 (0.9/*/**)        100.7 (0.7/*/**)       
  *  Indicates no estimate of optimizer instability due to single optimizer run. Consider multiple optimizer runs.
  ** Indicates no p-value due to single optimizer run. Consider multiple optimizer runs.
(base) ye@:/media/ye/project2/tool/multeval$
```

အဲဒါကြောင့် 10-fold ခွဲ run ထားခဲ့တဲ့ ရလဒ်တွေ အကုန်မဟုတ်ရင်တောင်မှ example ထဲမှာ ပြထားသလို ၃စုံလောက် ပြင်ရလိမ့်မယ်။  

## Prepared Data for Running with Multiple Optimizer

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold$ tree -L 1
.
├── bk-my-dw
├── bk-my-rk
├── dw-my-bk
└── rk-my-bk

4 directories, 0 files
```

filename တွေက အောက်ပါလိုပုံစံနဲ့ ပေးထားတယ်။ folder တစ်ခုအောက်မှာ reference ရော၊ baseline ရော၊ transfer model ရဲ့ hyp ရော ပြီးတော့ triangulation model ရဲ့ hyp ရော သိမ်းထားတယ်။ 10-fold အတွက် အားလုံးကို စုထားခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw$ ls
baseline.opt1   baseline.opt5  bk-my-dw.ref1   bk-my-dw.ref5  transfer.opt1   transfer.opt5  triangulation.opt1   triangulation.opt5
baseline.opt10  baseline.opt6  bk-my-dw.ref10  bk-my-dw.ref6  transfer.opt10  transfer.opt6  triangulation.opt10  triangulation.opt6
baseline.opt2   baseline.opt7  bk-my-dw.ref2   bk-my-dw.ref7  transfer.opt2   transfer.opt7  triangulation.opt2   triangulation.opt7
baseline.opt3   baseline.opt8  bk-my-dw.ref3   bk-my-dw.ref8  transfer.opt3   transfer.opt8  triangulation.opt3   triangulation.opt8
baseline.opt4   baseline.opt9  bk-my-dw.ref4   bk-my-dw.ref9  transfer.opt4   transfer.opt9  triangulation.opt4   triangulation.opt9
```

## Evaluation for bk-my-dw

bk-my-dw အတွက် run လို့ရအောင် "--refs", "--hyps-baseline", "--hyps-sys1", "--hyps-sys2" option တို့ကို အောက်ပါအတိုင်း ပြင်ခဲ့...  

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```

Run ကြည့်တော့...  အောက်ပါအတိုင်း non-parallel ဆိုတဲ့ error ပေးတယ်... 

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* \
> --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt* \
> --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* \
> --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* \
> --meteor.language en \
> --latex table.tex \
> --rankDir rank \
> --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.13 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt10
Exception in thread "main" java.lang.RuntimeException: Non-parallel inputs detected. Expected 670 hypotheses, but got 592
	at multeval.HypothesisManager.loadHyps(HypothesisManager.java:101)
	at multeval.HypothesisManager.loadData(HypothesisManager.java:44)
	at multeval.MultEvalModule.run(MultEvalModule.java:109)
	at multeval.MultEval.main(MultEval.java:115)

real	0m5.693s
user	0m7.881s
sys	0m0.280s
(base) ye@:/media/ye/project2/tool/multeval$
```

check with "wc" command ...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold$ wc ./bk-my-dw/*
    670    4166   63859 ./bk-my-dw/baseline.opt1
    592    3697   56141 ./bk-my-dw/baseline.opt10
    670    4150   64443 ./bk-my-dw/baseline.opt2
    670    4202   64569 ./bk-my-dw/baseline.opt3
    670    4044   62927 ./bk-my-dw/baseline.opt4
    670    4114   63678 ./bk-my-dw/baseline.opt5
    670    4131   62869 ./bk-my-dw/baseline.opt6
    670    4176   63595 ./bk-my-dw/baseline.opt7
    670    4130   63498 ./bk-my-dw/baseline.opt8
    670    4106   63913 ./bk-my-dw/baseline.opt9
    670    4013   64228 ./bk-my-dw/bk-my-dw.ref1
    592    3550   56952 ./bk-my-dw/bk-my-dw.ref10
    670    4030   65195 ./bk-my-dw/bk-my-dw.ref2
    670    3998   65039 ./bk-my-dw/bk-my-dw.ref3
    670    4012   64983 ./bk-my-dw/bk-my-dw.ref4
    670    4011   63713 ./bk-my-dw/bk-my-dw.ref5
    670    4042   64120 ./bk-my-dw/bk-my-dw.ref6
    670    4025   63846 ./bk-my-dw/bk-my-dw.ref7
    670    3993   65355 ./bk-my-dw/bk-my-dw.ref8
    670    3985   63827 ./bk-my-dw/bk-my-dw.ref9
    670    4197   63590 ./bk-my-dw/transfer.opt1
    592    3651   55139 ./bk-my-dw/transfer.opt10
    670    4202   63889 ./bk-my-dw/transfer.opt2
    670    4178   63697 ./bk-my-dw/transfer.opt3
    670    4128   63768 ./bk-my-dw/transfer.opt4
    670    4136   63036 ./bk-my-dw/transfer.opt5
    670    4157   61671 ./bk-my-dw/transfer.opt6
    670    4147   62101 ./bk-my-dw/transfer.opt7
    670    4158   63664 ./bk-my-dw/transfer.opt8
    670    4131   63311 ./bk-my-dw/transfer.opt9
    670    4044   62473 ./bk-my-dw/triangulation.opt1
    592    3579   54913 ./bk-my-dw/triangulation.opt10
    670    4054   63131 ./bk-my-dw/triangulation.opt2
    670    4047   63170 ./bk-my-dw/triangulation.opt3
    670    4119   62756 ./bk-my-dw/triangulation.opt4
    670    4077   62083 ./bk-my-dw/triangulation.opt5
    670    4069   61259 ./bk-my-dw/triangulation.opt6
    670    4051   61233 ./bk-my-dw/triangulation.opt7
    670    4017   62423 ./bk-my-dw/triangulation.opt8
    670    4030   61923 ./bk-my-dw/triangulation.opt9
  26488  161747 2505980 total
```

အထက်ပါအတိုင်း opt10 မှာက စာကြောင်းရေက 592 ပဲ ရှိလို့ ပေးနေတဲ့ error ...
အဲဒါကြောင့် 1 to 9 နဲ့ပဲ စမ်းဖို့ ဆုံးဖြတ်ခဲ့... အဲဒါနဲ့လည်း သီအိုရီအရဆိုရင် significant ဖြစ်မဖြစ်က measure လုပ်လို့ အိုကေတယ်။  

folder အသစ်ဆောက်ပြီး အဲဒီ ဖိုလ်ဒါအောက်ကို 10/ ရဲ့ ဒေတာကို ခဏရွှေ့ထားခဲ့...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw$ mv *10 ./for-10/
mv: cannot move 'for-10' to a subdirectory of itself, './for-10/for-10'
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw$ ls ./for-10/
baseline.opt10  bk-my-dw.ref10  transfer.opt10  triangulation.opt10
```

ထပ် run ကြည့်ခဲ့တော့ run လို့တော့ ရသွားပြီ...  

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt* --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* --meteor.language en --latex table.tex --rankDir rank --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.01 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt9
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt1
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt2
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt3
Reading Hypotheses for system 2 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt4
Reading Hypotheses for system 2 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt5
Reading Hypotheses for system 2 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt6
Reading Hypotheses for system 2 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt7
Reading Hypotheses for system 2 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt8
Reading Hypotheses for system 2 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.05 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 19.040364
RESULT: baseline: BLEU: MEDIAN: 19.074694
RESULT: baseline: BLEU: STDDEV: 0.891339
RESULT: baseline: BLEU: MIN: 17.573734
RESULT: baseline: BLEU: MAX: 20.229331
RESULT: baseline: BLEU: MEDIAN_IDX: 1.000000
RESULT: system 1: BLEU: AVG: 19.042434
RESULT: system 1: BLEU: MEDIAN: 19.102299
RESULT: system 1: BLEU: STDDEV: 1.048039
RESULT: system 1: BLEU: MIN: 17.244120
RESULT: system 1: BLEU: MAX: 20.292390
RESULT: system 1: BLEU: MEDIAN_IDX: 7.000000
RESULT: system 2: BLEU: AVG: 19.043974
RESULT: system 2: BLEU: MEDIAN: 18.886349
RESULT: system 2: BLEU: STDDEV: 0.905266
RESULT: system 2: BLEU: MIN: 17.737365
RESULT: system 2: BLEU: MAX: 20.552394
RESULT: system 2: BLEU: MEDIAN_IDX: 8.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 24.540353
RESULT: baseline: METEOR: MEDIAN: 24.492708
RESULT: baseline: METEOR: STDDEV: 0.455889
RESULT: baseline: METEOR: MIN: 23.745844
RESULT: baseline: METEOR: MAX: 25.412564
RESULT: baseline: METEOR: MEDIAN_IDX: 1.000000
RESULT: system 1: METEOR: AVG: 24.671590
RESULT: system 1: METEOR: MEDIAN: 24.777206
RESULT: system 1: METEOR: STDDEV: 0.437853
RESULT: system 1: METEOR: MIN: 23.899297
RESULT: system 1: METEOR: MAX: 25.182453
RESULT: system 1: METEOR: MEDIAN_IDX: 1.000000
RESULT: system 2: METEOR: AVG: 24.406830
RESULT: system 2: METEOR: MEDIAN: 24.303646
RESULT: system 2: METEOR: STDDEV: 0.406750
RESULT: system 2: METEOR: MIN: 23.818734
RESULT: system 2: METEOR: MAX: 25.041214
RESULT: system 2: METEOR: MEDIAN_IDX: 8.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 60.879318
RESULT: baseline: TER: MEDIAN: 60.592194
RESULT: baseline: TER: STDDEV: 1.344548
RESULT: baseline: TER: MIN: 58.950202
RESULT: baseline: TER: MAX: 63.176312
RESULT: baseline: TER: MEDIAN_IDX: 1.000000
RESULT: system 1: TER: AVG: 60.912218
RESULT: system 1: TER: MEDIAN: 60.915209
RESULT: system 1: TER: STDDEV: 1.159928
RESULT: system 1: TER: MIN: 59.057873
RESULT: system 1: TER: MAX: 63.230148
RESULT: system 1: TER: MEDIAN_IDX: 1.000000
RESULT: system 2: TER: AVG: 59.632122
RESULT: system 2: TER: MEDIAN: 59.730821
RESULT: system 2: TER: STDDEV: 0.740120
RESULT: system 2: TER: MIN: 58.250336
RESULT: system 2: TER: MAX: 60.699865
RESULT: system 2: TER: MEDIAN_IDX: 3.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 102.670294
RESULT: baseline: Length: MEDIAN: 102.593516
RESULT: baseline: Length: STDDEV: 0.480755
RESULT: baseline: Length: MIN: 102.116142
RESULT: baseline: Length: MAX: 103.599606
RESULT: baseline: Length: MEDIAN_IDX: 4.000000
RESULT: system 1: Length: AVG: 102.571126
RESULT: system 1: Length: MEDIAN: 102.521632
RESULT: system 1: Length: STDDEV: 0.369614
RESULT: system 1: Length: MIN: 102.188716
RESULT: system 1: Length: MAX: 103.390250
RESULT: system 1: Length: MEDIAN_IDX: 6.000000
RESULT: system 2: Length: AVG: 102.151654
RESULT: system 2: Length: MEDIAN: 102.154848
RESULT: system 2: Length: STDDEV: 0.393246
RESULT: system 2: Length: MIN: 101.633576
RESULT: system 2: Length: MAX: 102.794006
RESULT: system 2: Length: MEDIAN_IDX: 4.000000
Top unmatched hypothesis words accoring to METEOR: [ဟှို x 70, ဟှယ် x 37, သူ x 36, ဟှ x 34, နန် x 33, ဟှို့ x 30, နန့် x 28, မ x 24, နေဟှယ် x 23, ၊ x 20]
Top unmatched reference words accoring to METEOR: [ဟှို x 30, ဟှယ် x 28, ကျွန်တော် x 27, နန် x 26, သူ x 24, ဟှ x 21, ငါ x 19, နူး x 17, ခံဗျား x 17, ဝို x 16]
Top unmatched hypothesis words accoring to METEOR: [ဟှို x 82, ဟှယ် x 43, သူ x 42, နန် x 38, ဟှ x 34, ကျွန်တော် x 34, ဟှို့ x 32, မ x 28, လား x 27, နူး x 22]
Top unmatched reference words accoring to METEOR: [ဟှို x 25, ဟှယ် x 23, နန် x 22, ဟှ x 20, ကျွန်တော် x 20, ငါ x 19, ခံဗျား x 19, ဝို x 16, သူ x 16, နူး x 15]
Top unmatched hypothesis words accoring to METEOR: [ကျွန်တော် x 48, ဟှ x 47, ဟှို x 38, ဟှယ် x 34, သူ x 33, နန် x 26, လောက် x 20, မ x 19, သူးနို့ x 19, ငါ့ x 18]
Top unmatched reference words accoring to METEOR: [ဟှို x 52, ဟှယ် x 29, ဟှ x 25, နန် x 23, မ x 22, နူး x 21, ငါ x 20, ဟှို့ x 16, ကျွန်တော် x 16, လေ x 14]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 19.029902
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.118274
RESULT: baseline: BLEU: RESAMPLED_MIN: 13.385342
RESULT: baseline: BLEU: RESAMPLED_MAX: 25.077283
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 24.544210
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.476549
RESULT: baseline: METEOR: RESAMPLED_MIN: 22.052001
RESULT: baseline: METEOR: RESAMPLED_MAX: 27.285640
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 60.875756
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.392294
RESULT: baseline: TER: RESAMPLED_MIN: 53.753027
RESULT: baseline: TER: RESAMPLED_MAX: 68.509485
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 102.671077
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.378951
RESULT: baseline: Length: RESAMPLED_MIN: 100.465344
RESULT: baseline: Length: RESAMPLED_MAX: 105.429754
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 19.033880
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.101957
RESULT: system 1: BLEU: RESAMPLED_MIN: 13.886790
RESULT: system 1: BLEU: RESAMPLED_MAX: 24.584479
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 24.674425
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.467260
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.129983
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.191291
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 60.916235
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.382213
RESULT: system 1: TER: RESAMPLED_MIN: 54.084659
RESULT: system 1: TER: RESAMPLED_MAX: 68.847185
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 102.572929
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.375621
RESULT: system 1: Length: RESAMPLED_MIN: 100.750000
RESULT: system 1: Length: RESAMPLED_MAX: 104.893565
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 9 of 9)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 19.029728
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 1.112067
RESULT: system 2: BLEU: RESAMPLED_MIN: 13.922609
RESULT: system 2: BLEU: RESAMPLED_MAX: 25.197962
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 24.408358
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.467121
RESULT: system 2: METEOR: RESAMPLED_MIN: 22.000593
RESULT: system 2: METEOR: RESAMPLED_MAX: 26.985549
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 59.631164
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 1.340061
RESULT: system 2: TER: RESAMPLED_MIN: 53.138412
RESULT: system 2: TER: RESAMPLED_MAX: 65.827241
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 102.151257
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.359029
RESULT: system 2: Length: RESAMPLED_MIN: 100.309757
RESULT: system 2: Length: RESAMPLED_MAX: 104.464973
Performed bootstrap resampling in 14.8 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.975702
RESULT: system 1: METEOR: P_VALUE: 0.072793
RESULT: system 1: TER: P_VALUE: 0.837516
RESULT: system 1: Length: P_VALUE: 0.141586
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.957904
RESULT: system 2: METEOR: P_VALUE: 0.057394
RESULT: system 2: TER: P_VALUE: 0.000100
RESULT: system 2: Length: P_VALUE: 0.000100
Performed approximate randomization in 10.7 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       19.0 (1.1/0.9/-)       24.5 (0.5/0.5/-)       60.9 (1.4/1.3/-)       102.7 (0.4/0.5/-)      
system 1       19.0 (1.1/1.0/0.98)    24.7 (0.5/0.4/0.07)    60.9 (1.4/1.2/0.84)    102.6 (0.4/0.4/0.14)   
system 2       19.0 (1.1/0.9/0.96)    24.4 (0.5/0.4/0.06)    59.6 (1.3/0.7/0.00)    102.2 (0.4/0.4/0.00)   

real	0m33.290s
user	3m40.726s
sys	0m0.590s
(base) ye@:/media/ye/project2/tool/multeval$
```

## Evaluation for dw-my-bk

အရင်ဆုံး 10/ အတွက် ရထားတဲ့ အဖြေတွေနဲ့ ref ကို folder အသစ်ဆောက်ပြီး ရွှေ့ထားခဲ့...  

```
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk$ mkdir for-10
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk$ mv *10 ./for-10/
mv: cannot move 'for-10' to a subdirectory of itself, './for-10/for-10'
(base) ye@:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk$ ls ./for-10/
baseline.opt10  dw-my-bk.ref10  transfer.opt10  triangulation.opt10
```

command ရဲ့ option တွေကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```

run ကြည့်ခဲ့တော့ အောက်ပါအတိုင်း ရလဒ်ရရှိ...  

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref* \
> --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt* \
> --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt* \
> --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt* \
> --meteor.language en \
> --latex table.tex \
> --rankDir rank \
> --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.00 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt9
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt1
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt2
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt3
Reading Hypotheses for system 2 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt4
Reading Hypotheses for system 2 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt5
Reading Hypotheses for system 2 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt6
Reading Hypotheses for system 2 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt7
Reading Hypotheses for system 2 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt8
Reading Hypotheses for system 2 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.13 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 22.013168
RESULT: baseline: BLEU: MEDIAN: 22.177208
RESULT: baseline: BLEU: STDDEV: 1.254035
RESULT: baseline: BLEU: MIN: 20.289742
RESULT: baseline: BLEU: MAX: 23.886464
RESULT: baseline: BLEU: MEDIAN_IDX: 7.000000
RESULT: system 1: BLEU: AVG: 21.497999
RESULT: system 1: BLEU: MEDIAN: 21.541367
RESULT: system 1: BLEU: STDDEV: 1.372429
RESULT: system 1: BLEU: MIN: 19.399643
RESULT: system 1: BLEU: MAX: 23.412333
RESULT: system 1: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 2: BLEU: AVG: 22.045627
RESULT: system 2: BLEU: MEDIAN: 22.301236
RESULT: system 2: BLEU: STDDEV: 1.273386
RESULT: system 2: BLEU: MIN: 20.035715
RESULT: system 2: BLEU: MAX: 23.748817
RESULT: system 2: BLEU: MEDIAN_IDX: 4.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 25.121856
RESULT: baseline: METEOR: MEDIAN: 25.073858
RESULT: baseline: METEOR: STDDEV: 0.440194
RESULT: baseline: METEOR: MIN: 24.635723
RESULT: baseline: METEOR: MAX: 25.728305
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 24.623296
RESULT: system 1: METEOR: MEDIAN: 24.589827
RESULT: system 1: METEOR: STDDEV: 0.489732
RESULT: system 1: METEOR: MIN: 24.020333
RESULT: system 1: METEOR: MAX: 25.380568
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 2: METEOR: AVG: 25.056533
RESULT: system 2: METEOR: MEDIAN: 25.227676
RESULT: system 2: METEOR: STDDEV: 0.447235
RESULT: system 2: METEOR: MIN: 24.440269
RESULT: system 2: METEOR: MAX: 25.569590
RESULT: system 2: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 56.523207
RESULT: baseline: TER: MEDIAN: 56.405063
RESULT: baseline: TER: STDDEV: 0.843650
RESULT: baseline: TER: MIN: 55.265823
RESULT: baseline: TER: MAX: 57.772152
RESULT: baseline: TER: MEDIAN_IDX: 8.000000
RESULT: system 1: TER: AVG: 56.534459
RESULT: system 1: TER: MEDIAN: 56.481013
RESULT: system 1: TER: STDDEV: 0.813920
RESULT: system 1: TER: MIN: 55.291139
RESULT: system 1: TER: MAX: 58.278481
RESULT: system 1: TER: MEDIAN_IDX: 3.000000
RESULT: system 2: TER: AVG: 56.140647
RESULT: system 2: TER: MEDIAN: 55.873418
RESULT: system 2: TER: STDDEV: 0.830163
RESULT: system 2: TER: MIN: 55.316456
RESULT: system 2: TER: MAX: 57.417722
RESULT: system 2: TER: MEDIAN_IDX: 1.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.709710
RESULT: baseline: Length: MEDIAN: 101.733822
RESULT: baseline: Length: STDDEV: 0.178932
RESULT: baseline: Length: MIN: 101.414979
RESULT: baseline: Length: MAX: 102.022694
RESULT: baseline: Length: MEDIAN_IDX: 4.000000
RESULT: system 1: Length: AVG: 101.383627
RESULT: system 1: Length: MEDIAN: 101.377275
RESULT: system 1: Length: STDDEV: 0.236002
RESULT: system 1: Length: MIN: 101.013848
RESULT: system 1: Length: MAX: 101.725838
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
RESULT: system 2: Length: AVG: 101.644897
RESULT: system 2: Length: MEDIAN: 101.577520
RESULT: system 2: Length: STDDEV: 0.265569
RESULT: system 2: Length: MIN: 101.344861
RESULT: system 2: Length: MAX: 102.212829
RESULT: system 2: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [မ x 54, ကို x 53, နင် x 48, ငါ x 37, ရိ x 36, ဝို x 27, ရယ် x 22, သူ x 20, မှာ x 20, ပြော x 18]
Top unmatched reference words accoring to METEOR: [မ x 41, မင်း x 33, ကို x 31, ဝို x 25, က x 24, ငါ x 19, ရယ် x 17, ဝ x 16, သူ x 15, လေ x 14]
Top unmatched hypothesis words accoring to METEOR: [နင် x 63, ကို x 58, ငါ x 41, ရိ x 29, ရယ် x 24, မှာ x 23, ရ x 22, သူ x 22, ဒယ်ကောင်မငယ် x 19, က x 18]
Top unmatched reference words accoring to METEOR: [မ x 43, ကို x 40, မင်း x 38, ဝို x 30, ငါ x 21, ဝ x 19, ကျွန်တော် x 19, သူ x 17, နေရယ် x 17, က x 16]
Top unmatched hypothesis words accoring to METEOR: [နင် x 55, ကို x 52, ငါ x 48, မ x 29, ရိ x 28, သူ x 24, ရ x 22, ရယ် x 22, မှာ x 21, နေရယ် x 21]
Top unmatched reference words accoring to METEOR: [မ x 38, ကို x 30, ဝို x 29, မင်း x 29, ရယ် x 19, ငါ x 18, ဝ x 17, သူ x 17, ကျွန်တော် x 17, က x 16]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 21.999995
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.167998
RESULT: baseline: BLEU: RESAMPLED_MIN: 15.880132
RESULT: baseline: BLEU: RESAMPLED_MAX: 29.401509
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 25.123748
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.490217
RESULT: baseline: METEOR: RESAMPLED_MIN: 22.790465
RESULT: baseline: METEOR: RESAMPLED_MAX: 27.809935
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 56.518616
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.281565
RESULT: baseline: TER: RESAMPLED_MIN: 49.911817
RESULT: baseline: TER: RESAMPLED_MAX: 62.569691
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.709899
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.370567
RESULT: baseline: Length: RESAMPLED_MIN: 100.073314
RESULT: baseline: Length: RESAMPLED_MAX: 103.775913
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 21.490212
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.179290
RESULT: system 1: BLEU: RESAMPLED_MIN: 15.227744
RESULT: system 1: BLEU: RESAMPLED_MAX: 28.053330
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 24.625923
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.481534
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.335233
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.300142
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 56.529098
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.252689
RESULT: system 1: TER: RESAMPLED_MIN: 50.595691
RESULT: system 1: TER: RESAMPLED_MAX: 63.261694
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.382938
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.355359
RESULT: system 1: Length: RESAMPLED_MIN: 99.899900
RESULT: system 1: Length: RESAMPLED_MAX: 103.745802
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 9 of 9)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 22.032345
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 1.164110
RESULT: system 2: BLEU: RESAMPLED_MIN: 15.610536
RESULT: system 2: BLEU: RESAMPLED_MAX: 28.381823
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 25.057503
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.482104
RESULT: system 2: METEOR: RESAMPLED_MIN: 22.686921
RESULT: system 2: METEOR: RESAMPLED_MAX: 27.589533
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 56.140714
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 1.247249
RESULT: system 2: TER: RESAMPLED_MIN: 51.018356
RESULT: system 2: TER: RESAMPLED_MAX: 62.340967
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 101.642434
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.361284
RESULT: system 2: Length: RESAMPLED_MIN: 99.927589
RESULT: system 2: Length: RESAMPLED_MAX: 104.130224
Performed bootstrap resampling in 15.4 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.006899
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.946405
RESULT: system 1: Length: P_VALUE: 0.000100
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.859114
RESULT: system 2: METEOR: P_VALUE: 0.370963
RESULT: system 2: TER: P_VALUE: 0.005499
RESULT: system 2: Length: P_VALUE: 0.238676
Performed approximate randomization in 11.0 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       22.0 (1.2/1.3/-)       25.1 (0.5/0.4/-)       56.5 (1.3/0.8/-)       101.7 (0.4/0.2/-)      
system 1       21.5 (1.2/1.4/0.01)    24.6 (0.5/0.5/0.00)    56.5 (1.3/0.8/0.95)    101.4 (0.4/0.2/0.00)   
system 2       22.0 (1.2/1.3/0.86)    25.1 (0.5/0.4/0.37)    56.1 (1.2/0.8/0.01)    101.6 (0.4/0.3/0.24)   

real	0m34.287s
user	3m48.578s
sys	0m0.665s
(base) ye@:/media/ye/project2/tool/multeval$
```

## Evaluation for bk-my-rk

```
294 မင်း ယင်း မာ နီ မာလား ။
295 
296 ရဟန်းဝတ်စွာ ပိုကောင်း ပါရေ ။
```

စာကြောင်းကို ရိုက်ဖြည့်ခဲ့...  

```
294 မင်း ယင်း မာ နီ မာလား ။
295 မင်း သဘောကျတာ ဝမ်းသာ ရေ ။
296 ရဟန်းဝတ်စွာ ပိုကောင်း ပါရေ ။
```

command option ကို run လို့ ရအောင် ပြင်ဆင်ခဲ့...  

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```

evaulation result က အောက်ပါအတိုင်း.... 

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref* \
> --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt* \
> --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt* \
> --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt* \
> --meteor.language en \
> --latex table.tex \
> --rankDir rank \
> --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.03 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt9
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt1
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt10
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt2
Reading Hypotheses for system 2 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt3
Reading Hypotheses for system 2 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt4
Reading Hypotheses for system 2 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt5
Reading Hypotheses for system 2 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt6
Reading Hypotheses for system 2 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt7
Reading Hypotheses for system 2 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt8
Reading Hypotheses for system 2 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 3.37 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 38.107317
RESULT: baseline: BLEU: MEDIAN: 38.101657
RESULT: baseline: BLEU: STDDEV: 1.096922
RESULT: baseline: BLEU: MIN: 36.523549
RESULT: baseline: BLEU: MAX: 39.562671
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 1: BLEU: AVG: 38.065692
RESULT: system 1: BLEU: MEDIAN: 38.678206
RESULT: system 1: BLEU: STDDEV: 1.083216
RESULT: system 1: BLEU: MIN: 36.531621
RESULT: system 1: BLEU: MAX: 39.524288
RESULT: system 1: BLEU: MEDIAN_IDX: 8.000000
RESULT: system 2: BLEU: AVG: 39.108122
RESULT: system 2: BLEU: MEDIAN: 39.553497
RESULT: system 2: BLEU: STDDEV: 1.141870
RESULT: system 2: BLEU: MIN: 36.648374
RESULT: system 2: BLEU: MAX: 40.495678
RESULT: system 2: BLEU: MEDIAN_IDX: 5.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 32.392887
RESULT: baseline: METEOR: MEDIAN: 32.597018
RESULT: baseline: METEOR: STDDEV: 0.422477
RESULT: baseline: METEOR: MIN: 31.781338
RESULT: baseline: METEOR: MAX: 32.914025
RESULT: baseline: METEOR: MEDIAN_IDX: 8.000000
RESULT: system 1: METEOR: AVG: 32.293924
RESULT: system 1: METEOR: MEDIAN: 32.415859
RESULT: system 1: METEOR: STDDEV: 0.363030
RESULT: system 1: METEOR: MIN: 31.826429
RESULT: system 1: METEOR: MAX: 32.763816
RESULT: system 1: METEOR: MEDIAN_IDX: 2.000000
RESULT: system 2: METEOR: AVG: 32.812989
RESULT: system 2: METEOR: MEDIAN: 33.076160
RESULT: system 2: METEOR: STDDEV: 0.542853
RESULT: system 2: METEOR: MIN: 31.736482
RESULT: system 2: METEOR: MAX: 33.362702
RESULT: system 2: METEOR: MEDIAN_IDX: 2.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 45.984142
RESULT: baseline: TER: MEDIAN: 46.190920
RESULT: baseline: TER: STDDEV: 1.074351
RESULT: baseline: TER: MIN: 43.827736
RESULT: baseline: TER: MAX: 47.496891
RESULT: baseline: TER: MEDIAN_IDX: 8.000000
RESULT: system 1: TER: AVG: 45.693408
RESULT: system 1: TER: MEDIAN: 46.019900
RESULT: system 1: TER: STDDEV: 1.101920
RESULT: system 1: TER: MIN: 43.952114
RESULT: system 1: TER: MAX: 47.030473
RESULT: system 1: TER: MEDIAN_IDX: 8.000000
RESULT: system 2: TER: AVG: 44.483831
RESULT: system 2: TER: MEDIAN: 44.542910
RESULT: system 2: TER: STDDEV: 1.189155
RESULT: system 2: TER: MIN: 42.335199
RESULT: system 2: TER: MAX: 46.128731
RESULT: system 2: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.770679
RESULT: baseline: Length: MEDIAN: 101.853203
RESULT: baseline: Length: STDDEV: 0.277564
RESULT: baseline: Length: MIN: 101.277084
RESULT: baseline: Length: MAX: 102.175174
RESULT: baseline: Length: MEDIAN_IDX: 5.000000
RESULT: system 1: Length: AVG: 101.705263
RESULT: system 1: Length: MEDIAN: 101.611949
RESULT: system 1: Length: STDDEV: 0.260411
RESULT: system 1: Length: MIN: 101.456019
RESULT: system 1: Length: MAX: 102.097693
RESULT: system 1: Length: MEDIAN_IDX: 5.000000
RESULT: system 2: Length: AVG: 101.546450
RESULT: system 2: Length: MEDIAN: 101.507902
RESULT: system 2: Length: STDDEV: 0.206090
RESULT: system 2: Length: MIN: 101.264128
RESULT: system 2: Length: MAX: 101.943780
RESULT: system 2: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [။ x 105, ကို x 72, ရေ x 62, ပါ x 41, ဖို့ x 39, သူ x 33, မင်း x 32, က x 31, တိ x 29, မ x 26]
Top unmatched reference words accoring to METEOR: [။ x 52, ကို x 47, လား x 35, ပါ x 30, မင်း x 30, ကျွန်တော် x 26, လေး x 26, က x 24, မ x 23, ထိုမချေ x 23]
Top unmatched hypothesis words accoring to METEOR: [။ x 123, ကို x 64, ရေ x 56, ပါ x 52, သူ x 32, တိ x 29, မ x 28, နီရေ x 27, ငါ x 26, ကျွန်တော် x 26]
Top unmatched reference words accoring to METEOR: [ကို x 59, ။ x 47, ရေ x 37, မင်း x 31, ကျွန်တော် x 30, ရို့ x 28, ထိုမချေ x 27, ယင်းချင့် x 26, သူ x 25, ငါ x 24]
Top unmatched hypothesis words accoring to METEOR: [။ x 113, ကို x 65, ပါ x 52, ရေ x 49, သူ x 32, ပါလား x 28, တိ x 28, မ x 26, ငါ x 26, မင်း x 26]
Top unmatched reference words accoring to METEOR: [ကို x 54, ။ x 34, ရေ x 34, မင်း x 32, သူ x 27, က x 24, ပါ x 24, ပါရေ x 24, လေး x 24, ငါ x 23]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 38.103567
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.071303
RESULT: baseline: BLEU: RESAMPLED_MIN: 32.201271
RESULT: baseline: BLEU: RESAMPLED_MAX: 43.677738
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 32.395886
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.465969
RESULT: baseline: METEOR: RESAMPLED_MIN: 30.025558
RESULT: baseline: METEOR: RESAMPLED_MAX: 34.613193
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 45.986119
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.062983
RESULT: baseline: TER: RESAMPLED_MIN: 40.419865
RESULT: baseline: TER: RESAMPLED_MAX: 52.254353
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.773048
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.288701
RESULT: baseline: Length: RESAMPLED_MIN: 100.159559
RESULT: baseline: Length: RESAMPLED_MAX: 103.476483
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 38.061631
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.069623
RESULT: system 1: BLEU: RESAMPLED_MIN: 32.634000
RESULT: system 1: BLEU: RESAMPLED_MAX: 43.710118
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 32.294867
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.461668
RESULT: system 1: METEOR: RESAMPLED_MIN: 29.933738
RESULT: system 1: METEOR: RESAMPLED_MAX: 34.573143
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 45.698411
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.054095
RESULT: system 1: TER: RESAMPLED_MIN: 40.576565
RESULT: system 1: TER: RESAMPLED_MAX: 51.840920
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.706830
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.287805
RESULT: system 1: Length: RESAMPLED_MIN: 100.213311
RESULT: system 1: Length: RESAMPLED_MAX: 103.408925
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 10 of 10)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 39.101832
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 1.083604
RESULT: system 2: BLEU: RESAMPLED_MIN: 32.477376
RESULT: system 2: BLEU: RESAMPLED_MAX: 45.150634
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 32.813365
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.468791
RESULT: system 2: METEOR: RESAMPLED_MIN: 29.961902
RESULT: system 2: METEOR: RESAMPLED_MAX: 35.373830
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 44.483981
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 1.040249
RESULT: system 2: TER: RESAMPLED_MIN: 38.571651
RESULT: system 2: TER: RESAMPLED_MAX: 50.637240
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 101.546026
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.278362
RESULT: system 2: Length: RESAMPLED_MIN: 99.984992
RESULT: system 2: Length: RESAMPLED_MAX: 102.967273
Performed bootstrap resampling in 24.8 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.695430
RESULT: system 1: METEOR: P_VALUE: 0.077892
RESULT: system 1: TER: P_VALUE: 0.003800
RESULT: system 1: Length: P_VALUE: 0.099890
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.000100
RESULT: system 2: METEOR: P_VALUE: 0.000100
RESULT: system 2: TER: P_VALUE: 0.000100
RESULT: system 2: Length: P_VALUE: 0.000100
Performed approximate randomization in 26.1 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       38.1 (1.1/1.1/-)       32.4 (0.5/0.4/-)       46.0 (1.1/1.1/-)       101.8 (0.3/0.3/-)      
system 1       38.1 (1.1/1.1/0.70)    32.3 (0.5/0.4/0.08)    45.7 (1.1/1.1/0.00)    101.7 (0.3/0.3/0.10)   
system 2       39.1 (1.1/1.1/0.00)    32.8 (0.5/0.5/0.00)    44.5 (1.0/1.2/0.00)    101.5 (0.3/0.2/0.00)   
(base) ye@:/media/ye/project2/tool/multeval$
```

## Evaluation for rk-my-bk

command option ကို run လို့ ရအောင် ပြင်ဆင်ခဲ့...  

```
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel
```

evaluation result က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/tool/multeval$ ./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref* \
> --hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt* \
> --hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt* \
> --hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt* \
> --meteor.language en \
> --latex table.tex \
> --rankDir rank \
> --sentLevelDir sentLevel
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.07 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt9
Reading Hypotheses for system 2 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt1
Reading Hypotheses for system 2 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt10
Reading Hypotheses for system 2 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt2
Reading Hypotheses for system 2 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt3
Reading Hypotheses for system 2 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt4
Reading Hypotheses for system 2 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt5
Reading Hypotheses for system 2 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt6
Reading Hypotheses for system 2 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt7
Reading Hypotheses for system 2 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt8
Reading Hypotheses for system 2 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 4.02 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 31.480908
RESULT: baseline: BLEU: MEDIAN: 31.522166
RESULT: baseline: BLEU: STDDEV: 0.715522
RESULT: baseline: BLEU: MIN: 30.566390
RESULT: baseline: BLEU: MAX: 32.873347
RESULT: baseline: BLEU: MEDIAN_IDX: 4.000000
RESULT: system 1: BLEU: AVG: 32.513436
RESULT: system 1: BLEU: MEDIAN: 32.695810
RESULT: system 1: BLEU: STDDEV: 0.630776
RESULT: system 1: BLEU: MIN: 31.557934
RESULT: system 1: BLEU: MAX: 33.614592
RESULT: system 1: BLEU: MEDIAN_IDX: 9.000000
RESULT: system 2: BLEU: AVG: 32.005802
RESULT: system 2: BLEU: MEDIAN: 32.296170
RESULT: system 2: BLEU: STDDEV: 0.971518
RESULT: system 2: BLEU: MIN: 30.872371
RESULT: system 2: BLEU: MAX: 33.392403
RESULT: system 2: BLEU: MEDIAN_IDX: 7.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.312269
RESULT: baseline: METEOR: MEDIAN: 29.184757
RESULT: baseline: METEOR: STDDEV: 0.488781
RESULT: baseline: METEOR: MIN: 28.755664
RESULT: baseline: METEOR: MAX: 30.277635
RESULT: baseline: METEOR: MEDIAN_IDX: 4.000000
RESULT: system 1: METEOR: AVG: 29.671726
RESULT: system 1: METEOR: MEDIAN: 29.695654
RESULT: system 1: METEOR: STDDEV: 0.362983
RESULT: system 1: METEOR: MIN: 29.203431
RESULT: system 1: METEOR: MAX: 30.262589
RESULT: system 1: METEOR: MEDIAN_IDX: 2.000000
RESULT: system 2: METEOR: AVG: 29.590991
RESULT: system 2: METEOR: MEDIAN: 29.892847
RESULT: system 2: METEOR: STDDEV: 0.506059
RESULT: system 2: METEOR: MIN: 28.753944
RESULT: system 2: METEOR: MAX: 30.169151
RESULT: system 2: METEOR: MEDIAN_IDX: 7.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 49.452097
RESULT: baseline: TER: MEDIAN: 49.494949
RESULT: baseline: TER: STDDEV: 1.076815
RESULT: baseline: TER: MIN: 47.428834
RESULT: baseline: TER: MAX: 51.438629
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
RESULT: system 1: TER: AVG: 48.867463
RESULT: system 1: TER: MEDIAN: 48.943985
RESULT: system 1: TER: STDDEV: 0.927551
RESULT: system 1: TER: MIN: 47.183961
RESULT: system 1: TER: MAX: 50.520355
RESULT: system 1: TER: MEDIAN_IDX: 7.000000
RESULT: system 2: TER: AVG: 49.196511
RESULT: system 2: TER: MEDIAN: 49.035813
RESULT: system 2: TER: STDDEV: 1.047645
RESULT: system 2: TER: MIN: 47.199265
RESULT: system 2: TER: MAX: 50.811142
RESULT: system 2: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.974573
RESULT: baseline: Length: MEDIAN: 102.066233
RESULT: baseline: Length: STDDEV: 0.394486
RESULT: baseline: Length: MIN: 101.449485
RESULT: baseline: Length: MAX: 102.460059
RESULT: baseline: Length: MEDIAN_IDX: 3.000000
RESULT: system 1: Length: AVG: 101.917451
RESULT: system 1: Length: MEDIAN: 101.895173
RESULT: system 1: Length: STDDEV: 0.380179
RESULT: system 1: Length: MIN: 101.422351
RESULT: system 1: Length: MAX: 102.507793
RESULT: system 1: Length: MEDIAN_IDX: 0.000000
RESULT: system 2: Length: AVG: 101.979082
RESULT: system 2: Length: MEDIAN: 102.079528
RESULT: system 2: Length: STDDEV: 0.281791
RESULT: system 2: Length: MIN: 101.459538
RESULT: system 2: Length: MAX: 102.309109
RESULT: system 2: Length: MEDIAN_IDX: 3.000000
Top unmatched hypothesis words accoring to METEOR: [ကို x 75, နင် x 69, မ x 46, ကျွန်တော် x 38, ရ x 37, ရယ် x 37, ဝို့ x 37, က x 36, ဝို x 36, ဒယ်ကောင်မငယ် x 31]
Top unmatched reference words accoring to METEOR: [။ x 64, ကို x 58, ဝို x 41, မင်း x 40, ရယ် x 39, သူ x 28, က x 27, ငါ x 27, မ x 25, နင် x 24]
Top unmatched hypothesis words accoring to METEOR: [ကို x 66, ဝို x 54, နင် x 53, ဒယ်ကောင်မငယ် x 43, ရယ် x 40, က x 27, ငါ x 26, ရ x 25, ဝို့ x 25, မ x 23]
Top unmatched reference words accoring to METEOR: [ကို x 74, ဝို x 57, ။ x 43, မင်း x 40, မ x 33, သူ x 32, ငါ x 31, နေရယ် x 26, ရယ် x 24, နင့် x 23]
Top unmatched hypothesis words accoring to METEOR: [ကို x 109, နင် x 70, ရယ် x 44, ရ x 42, မ x 39, ဝို x 38, ဒယ်ကောင်မငယ် x 35, က x 31, ကျွန်တော် x 29, ရလား x 28]
Top unmatched reference words accoring to METEOR: [ဝို x 50, မင်း x 44, ကို x 43, ။ x 40, က x 33, ဝို့ x 31, သူ x 29, ငါ x 25, ရယ် x 22, နင် x 22]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/sentLevel
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/rank
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 3; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 31.477697
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.004130
RESULT: baseline: BLEU: RESAMPLED_MIN: 26.871343
RESULT: baseline: BLEU: RESAMPLED_MAX: 36.788321
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.315393
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.428642
RESULT: baseline: METEOR: RESAMPLED_MIN: 27.077609
RESULT: baseline: METEOR: RESAMPLED_MAX: 31.942461
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 49.452848
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.087591
RESULT: baseline: TER: RESAMPLED_MIN: 43.563603
RESULT: baseline: TER: RESAMPLED_MAX: 56.462271
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.974987
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.313708
RESULT: baseline: Length: RESAMPLED_MIN: 100.382691
RESULT: baseline: Length: RESAMPLED_MAX: 103.859085
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 3; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 32.514039
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.029285
RESULT: system 1: BLEU: RESAMPLED_MIN: 27.759558
RESULT: system 1: BLEU: RESAMPLED_MAX: 37.349550
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 29.673819
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.441507
RESULT: system 1: METEOR: RESAMPLED_MIN: 27.603290
RESULT: system 1: METEOR: RESAMPLED_MAX: 32.361738
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 48.864769
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.093576
RESULT: system 1: TER: RESAMPLED_MIN: 43.521493
RESULT: system 1: TER: RESAMPLED_MAX: 55.213415
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.915405
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.305996
RESULT: system 1: Length: RESAMPLED_MIN: 100.288309
RESULT: system 1: Length: RESAMPLED_MAX: 103.806570
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 3 of 3; opt run 10 of 10)
RESULT: system 2: BLEU: RESAMPLED_MEAN_AVG: 32.007198
RESULT: system 2: BLEU: RESAMPLED_STDDEV_AVG: 1.020131
RESULT: system 2: BLEU: RESAMPLED_MIN: 27.080131
RESULT: system 2: BLEU: RESAMPLED_MAX: 37.682092
RESULT: system 2: METEOR: RESAMPLED_MEAN_AVG: 29.595097
RESULT: system 2: METEOR: RESAMPLED_STDDEV_AVG: 0.437299
RESULT: system 2: METEOR: RESAMPLED_MIN: 27.125643
RESULT: system 2: METEOR: RESAMPLED_MAX: 31.979918
RESULT: system 2: TER: RESAMPLED_MEAN_AVG: 49.194789
RESULT: system 2: TER: RESAMPLED_STDDEV_AVG: 1.091911
RESULT: system 2: TER: RESAMPLED_MIN: 43.524189
RESULT: system 2: TER: RESAMPLED_MAX: 55.053069
RESULT: system 2: Length: RESAMPLED_MEAN_AVG: 101.978627
RESULT: system 2: Length: RESAMPLED_STDDEV_AVG: 0.304155
RESULT: system 2: Length: RESAMPLED_MIN: 100.247813
RESULT: system 2: Length: RESAMPLED_MAX: 103.756331
Performed bootstrap resampling in 25.1 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 3)
RESULT: system 1: BLEU: P_VALUE: 0.000100
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.153885
Performing approximate randomization to estimate p-value between baseline system and system 3 (of 3)
RESULT: system 2: BLEU: P_VALUE: 0.000100
RESULT: system 2: METEOR: P_VALUE: 0.000100
RESULT: system 2: TER: P_VALUE: 0.011699
RESULT: system 2: Length: P_VALUE: 0.911909
Performed approximate randomization in 32.1 s
Writing Latex table to /media/ye/project2/tool/multeval/table.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       31.5 (1.0/0.7/-)       29.3 (0.4/0.5/-)       49.5 (1.1/1.1/-)       102.0 (0.3/0.4/-)      
system 1       32.5 (1.0/0.6/0.00)    29.7 (0.4/0.4/0.00)    48.9 (1.1/0.9/0.00)    101.9 (0.3/0.4/0.15)   
system 2       32.0 (1.0/1.0/0.00)    29.6 (0.4/0.5/0.00)    49.2 (1.1/1.0/0.01)    102.0 (0.3/0.3/0.91)   
(base) ye@:/media/ye/project2/tool/multeval$
```

## Result Tables

တစ်ခေါက် run ပြီးတိုင်းမှာ table.tex ဖိုင်ကို ဖိုင်နာမည်ပြောင်းပြီး သိမ်းပေးဖို့ လိုအပ်တယ်။  
ဥပမာ အောက်ပါလိုမျိုး...  

```
(base) ye@:/media/ye/project2/tool/multeval$ mv table.tex bk-my-rk.table.tex
```

ရလဒ် ဇယားတွေကို လေ့လာကြည့်ရအောင်....  



## Check rank/

```
(base) ye@:/media/ye/project2/tool/multeval/rank$ ls
sys2.sortedby.bleu    sys2.sortedby.meteor  sys3.sortedby.bleu    sys3.sortedby.meteor
sys2.sortedby.length  sys2.sortedby.ter     sys3.sortedby.length  sys3.sortedby.ter
(base) ye@:/media/ye/project2/tool/multeval/rank$ head -30 ./sys2.sortedby.bleu 
SENT 85	bleu: 6.6 -> 100.0 = 93.4	meteor: 9.0 -> 100.0 = 91.0	ter: 120.0 -> 0.0 = -120.0	length: 100.0 -> 100.0 = 0.0
bleu-median-baseline: ဒါ ရစ်သတ္တပတ် ကူဆောန်းရစ်မာ ရာသီဥတု သာယာပီးနေသာမယ် ဆိုဟှီးကောဟှယ် ။
bleu-median-variant: နင်တို့ ဘယ်မှာ သောက် ဝို့ ။
ref1: နင်တို့ ဘယ်မှာ သောက် ဝို့ ။
ref2: ငါ စကားပြော နေရယ် ။
ref3: ငါ စန္ဒရား တီး နိုင်ရယ် ။
ref4: သူ ငါ့ ကို ခွင့်မလွှတ် ရ ။
ref5: ဖယ်သူတွေ ဂုဏ်ပြုခံ ရရိလဲ ။
ref6: အဲ့အမ ကို ဂုဏ်ပြု ရယ်လား ။
ref7: နင်ဝို့ ကြိုးစား မယ် မ ဟုတ် ဝလား ။
ref8: ဒါတပတ် ကုန်ခါနီးမှာ ရာသီဥတုသာယာပ ပြီး နေပူ မယ်တဲ့ ။
ref9: ဒယ်ဇာ ဟုတ်ဝယ် ပဲ့လား ။

SENT 3	bleu: 7.3 -> 100.0 = 92.7	meteor: 11.2 -> 100.0 = 88.8	ter: 100.0 -> 0.0 = -100.0	length: 100.0 -> 100.0 = 0.0
bleu-median-baseline: နေ့လောင်း ဇာတ်လမ်းတွဲလေဟှ လွဲဟှီး ရှားလည်း မ ရှိ ကြဟ ။
bleu-median-variant: နင် ဘာဇာတွေ ရေး နေရယ် ။
ref1: နင် ဘာဇာတွေ ရေး နေရယ် ။
ref2: ငယ်ငယ်တည်းက မင်းသား လုပ်ဝို့ ဝါသနာ ပါစ ။
ref3: သူ ဝ အမြဲတမ်း အကောင်းဘက် ပဲ့ ကြည့် ရယ် ။
ref4: နင့်မှာ ရုပ်မြင်သံကြားစက် တစ် လုံး ရှိ ရယ်ရ်လာ ။
ref5: သူ သူတို့ ဝို မ နှိုး ဝ ။
ref6: ငါ့ဝို အလုပ်ခန့် တဲ့ လူ ဝ အတွင်းရေးမှူး ပဲ့ ။
ref7: နင် ရှာ နေတဲ့ ဖြေ ။
ref8: တစ်နေ့လုံး အပိုင်းတွဲတွေ ခဲ လာ နေမှာ ။
ref9: ငါ စနေ နေ့ ကျရင် ဖုန်းဆက် မယ် ။

SENT 0	bleu: 7.8 -> 100.0 = 92.2	meteor: 13.0 -> 100.0 = 87.0	ter: 83.3 -> 0.0 = -83.3	length: 116.7 -> 100.0 = -16.7
bleu-median-baseline: ဟှိုဖော့သယ်ဟှ သူ့ မဲသားဟှို ပြန် ပို့ လား ။
bleu-median-variant: သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
ref1: သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
(base) ye@:/media/ye/project2/tool/multeval/rank$ 
```

## check sentLevel/

```
(base) ye@:/media/ye/project2/tool/multeval/sentLevel$ ls
sys1.opt1   sys1.opt3  sys1.opt6  sys1.opt9   sys2.opt2  sys2.opt5  sys2.opt8  sys3.opt10  sys3.opt4  sys3.opt7
sys1.opt10  sys1.opt4  sys1.opt7  sys2.opt1   sys2.opt3  sys2.opt6  sys2.opt9  sys3.opt2   sys3.opt5  sys3.opt8
sys1.opt2   sys1.opt5  sys1.opt8  sys2.opt10  sys2.opt4  sys2.opt7  sys3.opt1  sys3.opt3   sys3.opt6  sys3.opt9
(base) ye@:/media/ye/project2/tool/multeval/sentLevel$ head  sys1.opt1
0 ||| သူ ခင်ဗျား ကို ဒယ်ဇာ မ ပေး ဖို့ မ ဟုတ် ဝ ။ ||| bleu=36.13 meteor=47.99 ter=50.00 length=122.22 ||| bleu1p=0.95 bleu2p=0.80 bleu3p=0.61 bleu4p=0.36 brevity=1.00 prec=0.73 rec=1.00 frag=0.49
1 ||| နင် ဖယ်သူ့ ဝို ဒုက္ခပေး ခဲ့ရယ် ။ ||| bleu=37.99 meteor=31.84 ter=28.57 length=100.00 ||| bleu1p=0.96 bleu2p=0.84 bleu3p=0.59 bleu4p=0.38 brevity=1.00 prec=0.67 rec=0.67 frag=0.52
2 ||| သိပ် ပြေ တာပေါ့ ။ ||| bleu=100.00 meteor=100.00 ter=0.00 length=100.00 ||| bleu1p=1.00 bleu2p=1.00 bleu3p=1.00 bleu4p=1.00 brevity=1.00 prec=1.00 rec=1.00 frag=0.00
3 ||| နင် ဘာ ရေး နေရယ် ။ ||| bleu=42.73 meteor=38.21 ter=16.67 length=100.00 ||| bleu1p=0.95 bleu2p=0.80 bleu3p=0.60 bleu4p=0.43 brevity=1.00 prec=0.80 rec=0.80 frag=0.52
4 ||| ဆရာ လာ ပြီ ။ ||| bleu=35.36 meteor=33.51 ter=20.00 length=100.00 ||| bleu1p=0.93 bleu2p=0.71 bleu3p=0.50 bleu4p=0.35 brevity=1.00 prec=0.75 rec=0.75 frag=0.55
5 ||| ဆရာ လာ ပြီ ။ ||| bleu=35.36 meteor=33.51 ter=16.67 length=100.00 ||| bleu1p=0.93 bleu2p=0.71 bleu3p=0.50 bleu4p=0.35 brevity=1.00 prec=0.75 rec=0.75 frag=0.55
6 ||| သူ အန်းဂလီ စကား မ ပြော နိုင်ဟှီးလား ။ ||| bleu=9.82 meteor=26.02 ter=60.00 length=116.67 ||| bleu1p=0.92 bleu2p=0.49 bleu3p=0.23 bleu4p=0.10 brevity=1.00 prec=0.57 rec=0.67 frag=0.60
7 ||| ခင်ဗျား ဆေးလိပ် လျှော့ သောက် လိုက်မား ။ ||| bleu=53.73 meteor=41.71 ter=16.67 length=100.00 ||| bleu1p=0.96 bleu2p=0.84 bleu3p=0.71 bleu4p=0.54 brevity=1.00 prec=0.83 rec=0.83 frag=0.50
8 ||| သူဝို့ ငွေ မ စု ၊ ကြေးပြား မ စု ကြရယ်လား ။ ||| bleu=11.04 meteor=27.64 ter=83.33 length=100.00 ||| bleu1p=0.88 bleu2p=0.51 bleu3p=0.25 bleu4p=0.11 brevity=1.00 prec=0.60 rec=0.67 frag=0.58
9 ||| ဒယ်ကောင်မငယ် က သူ့ ကို မ သိ ဟားဇာ ။ ||| bleu=14.54 meteor=24.25 ter=57.14 length=114.29 ||| bleu1p=0.93 bleu2p=0.57 bleu3p=0.31 bleu4p=0.15 brevity=1.00 prec=0.50 rec=0.57 frag=0.57
(base) ye@:/media/ye/project2/tool/multeval/sentLevel$ head sys2.opt1
0 ||| သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။ ||| bleu=100.00 meteor=100.00 ter=0.00 length=100.00 ||| bleu1p=1.00 bleu2p=1.00 bleu3p=1.00 bleu4p=1.00 brevity=1.00 prec=1.00 rec=1.00 frag=0.00
1 ||| နင် ဖယ်သူ့ ဝို ဒုက္ခပေး ။ ||| bleu=42.73 meteor=32.66 ter=28.57 length=100.00 ||| bleu1p=0.95 bleu2p=0.80 bleu3p=0.60 bleu4p=0.43 brevity=1.00 prec=0.80 rec=0.67 frag=0.52
2 ||| တအား အဆင်ပြေ စို့ ။ ||| bleu=15.97 meteor=10.00 ter=50.00 length=100.00 ||| bleu1p=0.71 bleu2p=0.45 bleu3p=0.27 bleu4p=0.16 brevity=1.00 prec=0.25 rec=0.25 frag=0.60
3 ||| နင် ဘာဇာတွေ ရေး နေရယ် ။ ||| bleu=100.00 meteor=100.00 ter=0.00 length=100.00 ||| bleu1p=1.00 bleu2p=1.00 bleu3p=1.00 bleu4p=1.00 brevity=1.00 prec=1.00 rec=1.00 frag=0.00
4 ||| ဆရာ လာ ပြီ ။ ||| bleu=35.36 meteor=33.51 ter=20.00 length=100.00 ||| bleu1p=0.93 bleu2p=0.71 bleu3p=0.50 bleu4p=0.35 brevity=1.00 prec=0.75 rec=0.75 frag=0.55
5 ||| ဆရာ လာ ပြီ ။ ||| bleu=35.36 meteor=33.51 ter=16.67 length=100.00 ||| bleu1p=0.93 bleu2p=0.71 bleu3p=0.50 bleu4p=0.35 brevity=1.00 prec=0.75 rec=0.75 frag=0.55
6 ||| သူ အန်းဂလီ စကား ပြော နိုင်ဟှီးလား ။ ||| bleu=19.30 meteor=28.90 ter=40.00 length=100.00 ||| bleu1p=0.90 bleu2p=0.60 bleu3p=0.36 bleu4p=0.19 brevity=1.00 prec=0.67 rec=0.67 frag=0.57
7 ||| နင် ဆေးလိပ် လျှော့ သောက် လိုက်မား ။ ||| bleu=32.47 meteor=31.84 ter=33.33 length=100.00 ||| bleu1p=0.90 bleu2p=0.72 bleu3p=0.51 bleu4p=0.32 brevity=1.00 prec=0.67 rec=0.67 frag=0.52
8 ||| သူလို့ ကြေးပြား မ စု ခဲ့ရ ငွေ မ စု ကြရယ်လား ။ ||| bleu=9.98 meteor=18.95 ter=100.00 length=100.00 ||| bleu1p=0.80 bleu2p=0.46 bleu3p=0.23 bleu4p=0.10 brevity=1.00 prec=0.40 rec=0.44 frag=0.57
9 ||| သူက သူ့ ကို သိထား ဇာ ။ ||| bleu=17.97 meteor=19.57 ter=57.14 length=100.00 ||| bleu1p=0.84 bleu2p=0.56 bleu3p=0.33 bleu4p=0.18 brevity=1.00 prec=0.50 rec=0.43 frag=0.55
(base) ye@:/media/ye/project2/tool/multeval/sentLevel$
```

## Prepare as Shell Script

```bash
#!/bin/bash

# run on 18 Jan 2022

# for bk-my-dw
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel

# for dw-my-bk
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel

# for bk-my-rk
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel

# for rk-my-bk
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/baseline.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt* \
--hyps-sys2 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt* \
--meteor.language en \
--latex table.tex \
--rankDir rank \
--sentLevelDir sentLevel

```

## Calculation between Sys1 vs Sys2

ဒီတစ်ခါတော့ System 1 နဲ့ System 2 အကြား နှိုင်းယှဉ်ကြည့်ချင်လို့ အထက်က ပထမဆုံး run ခဲ့တဲ့ shell script ကို အောက်ပါအတိုင်း ပြင်လိုက်တယ်။

```bash
#!/bin/bash

# run on 19 Jan 2022
# ဒီတစ်ခါတော့ transfer ကို baseline အဖြစ်ထားပြီးတော့ Triangulation ကို sys1 အနေနဲ့ထား run ကြည့်ခဲ့တယ်

# for bk-my-dw
echo "Evaluation for bk-my-dw ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* \
--meteor.language en \
--latex bk-my-dw.tran-vs-tri.tex \
--rankDir run2/rank/bk-my-dw \
--sentLevelDir run2/sentLevel/bk-my-dw
echo "==========";

# for dw-my-bk
echo "Evaluation for dw-my-bk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt* \
--meteor.language en \
--latex dw-my-bk.tran-vs-tri.tex \
--rankDir run2/rank/dw-my-bk \
--sentLevelDir run2/sentLevel/dw-my-bk
echo "==========";

# for bk-my-rk
echo "Evaluation for bk-my-rk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt* \
--meteor.language en \
--latex bk-my-rk.tran-vs-tri.tex \
--rankDir run2/rank/bk-my-rk \
--sentLevelDir run2/sentLevel/bk-my-rk
echo "==========";

# for rk-my-bk
echo "Evaluation for rk-my-bk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt* \
--meteor.language en \
--latex rk-my-bk.tran-vs-tri.tex \
--rankDir run2/rank/rk-my-bk \
--sentLevelDir run2/sentLevel/rk-my-bk
echo "==========";

```

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./run2.sh | tee run2.log
```

running output screen က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./run2.sh | tee run2.log
Evaluation for bk-my-dw ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.15 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 1.98 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 19.042434
RESULT: baseline: BLEU: MEDIAN: 19.102299
RESULT: baseline: BLEU: STDDEV: 1.048039
RESULT: baseline: BLEU: MIN: 17.244120
RESULT: baseline: BLEU: MAX: 20.292390
RESULT: baseline: BLEU: MEDIAN_IDX: 7.000000
RESULT: system 1: BLEU: AVG: 19.043974
RESULT: system 1: BLEU: MEDIAN: 18.886349
RESULT: system 1: BLEU: STDDEV: 0.905266
RESULT: system 1: BLEU: MIN: 17.737365
RESULT: system 1: BLEU: MAX: 20.552394
RESULT: system 1: BLEU: MEDIAN_IDX: 8.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 24.671590
RESULT: baseline: METEOR: MEDIAN: 24.777206
RESULT: baseline: METEOR: STDDEV: 0.437853
RESULT: baseline: METEOR: MIN: 23.899297
RESULT: baseline: METEOR: MAX: 25.182453
RESULT: baseline: METEOR: MEDIAN_IDX: 1.000000
RESULT: system 1: METEOR: AVG: 24.406830
RESULT: system 1: METEOR: MEDIAN: 24.303646
RESULT: system 1: METEOR: STDDEV: 0.406750
RESULT: system 1: METEOR: MIN: 23.818734
RESULT: system 1: METEOR: MAX: 25.041214
RESULT: system 1: METEOR: MEDIAN_IDX: 8.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 60.912218
RESULT: baseline: TER: MEDIAN: 60.915209
RESULT: baseline: TER: STDDEV: 1.159928
RESULT: baseline: TER: MIN: 59.057873
RESULT: baseline: TER: MAX: 63.230148
RESULT: baseline: TER: MEDIAN_IDX: 1.000000
RESULT: system 1: TER: AVG: 59.632122
RESULT: system 1: TER: MEDIAN: 59.730821
RESULT: system 1: TER: STDDEV: 0.740120
RESULT: system 1: TER: MIN: 58.250336
RESULT: system 1: TER: MAX: 60.699865
RESULT: system 1: TER: MEDIAN_IDX: 3.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 102.571126
RESULT: baseline: Length: MEDIAN: 102.521632
RESULT: baseline: Length: STDDEV: 0.369614
RESULT: baseline: Length: MIN: 102.188716
RESULT: baseline: Length: MAX: 103.390250
RESULT: baseline: Length: MEDIAN_IDX: 6.000000
RESULT: system 1: Length: AVG: 102.151654
RESULT: system 1: Length: MEDIAN: 102.154848
RESULT: system 1: Length: STDDEV: 0.393246
RESULT: system 1: Length: MIN: 101.633576
RESULT: system 1: Length: MAX: 102.794006
RESULT: system 1: Length: MEDIAN_IDX: 4.000000
Top unmatched hypothesis words accoring to METEOR: [ဟှို x 82, ဟှယ် x 43, သူ x 42, နန် x 38, ဟှ x 34, ကျွန်တော် x 34, ဟှို့ x 32, မ x 28, လား x 27, နူး x 22]
Top unmatched reference words accoring to METEOR: [ဟှို x 25, ဟှယ် x 23, နန် x 22, ဟှ x 20, ကျွန်တော် x 20, ငါ x 19, ခံဗျား x 19, ဝို x 16, သူ x 16, နူး x 15]
Top unmatched hypothesis words accoring to METEOR: [ကျွန်တော် x 48, ဟှ x 47, ဟှို x 38, ဟှယ် x 34, သူ x 33, နန် x 26, လောက် x 20, မ x 19, သူးနို့ x 19, ငါ့ x 18]
Top unmatched reference words accoring to METEOR: [ဟှို x 52, ဟှယ် x 29, ဟှ x 25, နန် x 23, မ x 22, နူး x 21, ငါ x 20, ဟှို့ x 16, ကျွန်တော် x 16, လေ x 14]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run2/sentLevel/bk-my-dw
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run2/rank/bk-my-dw
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 19.038922
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.102558
RESULT: baseline: BLEU: RESAMPLED_MIN: 13.505434
RESULT: baseline: BLEU: RESAMPLED_MAX: 25.371634
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 24.677270
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.469093
RESULT: baseline: METEOR: RESAMPLED_MIN: 22.276197
RESULT: baseline: METEOR: RESAMPLED_MAX: 27.198418
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 60.900450
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.379832
RESULT: baseline: TER: RESAMPLED_MIN: 53.340517
RESULT: baseline: TER: RESAMPLED_MAX: 69.483315
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 102.570317
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.376929
RESULT: baseline: Length: RESAMPLED_MIN: 100.760736
RESULT: baseline: Length: RESAMPLED_MAX: 105.319931
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 19.036849
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.104339
RESULT: system 1: BLEU: RESAMPLED_MIN: 13.481504
RESULT: system 1: BLEU: RESAMPLED_MAX: 25.768900
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 24.409291
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.466035
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.111565
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.296148
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 59.634016
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.340991
RESULT: system 1: TER: RESAMPLED_MIN: 52.618856
RESULT: system 1: TER: RESAMPLED_MAX: 66.477426
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 102.151671
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.361770
RESULT: system 1: Length: RESAMPLED_MIN: 100.403633
RESULT: system 1: Length: RESAMPLED_MAX: 104.506110
Performed bootstrap resampling in 9.95 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.983802
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.000100
Performed approximate randomization in 5.21 s
Writing Latex table to /media/ye/project2/tool/multeval/bk-my-dw.tran-vs-tri.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       19.0 (1.1/1.0/-)       24.7 (0.5/0.4/-)       60.9 (1.4/1.2/-)       102.6 (0.4/0.4/-)      
system 1       19.0 (1.1/0.9/0.98)    24.4 (0.5/0.4/0.00)    59.6 (1.3/0.7/0.00)    102.2 (0.4/0.4/0.00)   
==========
Evaluation for dw-my-bk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 4.89 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.22 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 21.497999
RESULT: baseline: BLEU: MEDIAN: 21.541367
RESULT: baseline: BLEU: STDDEV: 1.372429
RESULT: baseline: BLEU: MIN: 19.399643
RESULT: baseline: BLEU: MAX: 23.412333
RESULT: baseline: BLEU: MEDIAN_IDX: 0.000000
RESULT: system 1: BLEU: AVG: 22.045627
RESULT: system 1: BLEU: MEDIAN: 22.301236
RESULT: system 1: BLEU: STDDEV: 1.273386
RESULT: system 1: BLEU: MIN: 20.035715
RESULT: system 1: BLEU: MAX: 23.748817
RESULT: system 1: BLEU: MEDIAN_IDX: 4.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 24.623296
RESULT: baseline: METEOR: MEDIAN: 24.589827
RESULT: baseline: METEOR: STDDEV: 0.489732
RESULT: baseline: METEOR: MIN: 24.020333
RESULT: baseline: METEOR: MAX: 25.380568
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 25.056533
RESULT: system 1: METEOR: MEDIAN: 25.227676
RESULT: system 1: METEOR: STDDEV: 0.447235
RESULT: system 1: METEOR: MIN: 24.440269
RESULT: system 1: METEOR: MAX: 25.569590
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 56.534459
RESULT: baseline: TER: MEDIAN: 56.481013
RESULT: baseline: TER: STDDEV: 0.813920
RESULT: baseline: TER: MIN: 55.291139
RESULT: baseline: TER: MAX: 58.278481
RESULT: baseline: TER: MEDIAN_IDX: 3.000000
RESULT: system 1: TER: AVG: 56.140647
RESULT: system 1: TER: MEDIAN: 55.873418
RESULT: system 1: TER: STDDEV: 0.830163
RESULT: system 1: TER: MIN: 55.316456
RESULT: system 1: TER: MAX: 57.417722
RESULT: system 1: TER: MEDIAN_IDX: 1.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.383627
RESULT: baseline: Length: MEDIAN: 101.377275
RESULT: baseline: Length: STDDEV: 0.236002
RESULT: baseline: Length: MIN: 101.013848
RESULT: baseline: Length: MAX: 101.725838
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
RESULT: system 1: Length: AVG: 101.644897
RESULT: system 1: Length: MEDIAN: 101.577520
RESULT: system 1: Length: STDDEV: 0.265569
RESULT: system 1: Length: MIN: 101.344861
RESULT: system 1: Length: MAX: 102.212829
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [နင် x 63, ကို x 58, ငါ x 41, ရိ x 29, ရယ် x 24, မှာ x 23, ရ x 22, သူ x 22, ဒယ်ကောင်မငယ် x 19, က x 18]
Top unmatched reference words accoring to METEOR: [မ x 43, ကို x 40, မင်း x 38, ဝို x 30, ငါ x 21, ဝ x 19, ကျွန်တော် x 19, သူ x 17, နေရယ် x 17, က x 16]
Top unmatched hypothesis words accoring to METEOR: [နင် x 55, ကို x 52, ငါ x 48, မ x 29, ရိ x 28, သူ x 24, ရ x 22, ရယ် x 22, မှာ x 21, နေရယ် x 21]
Top unmatched reference words accoring to METEOR: [မ x 38, ကို x 30, ဝို x 29, မင်း x 29, ရယ် x 19, ငါ x 18, ဝ x 17, သူ x 17, ကျွန်တော် x 17, က x 16]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run2/sentLevel/dw-my-bk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run2/rank/dw-my-bk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 21.488727
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.179550
RESULT: baseline: BLEU: RESAMPLED_MIN: 13.371982
RESULT: baseline: BLEU: RESAMPLED_MAX: 28.478725
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 24.627387
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.481954
RESULT: baseline: METEOR: RESAMPLED_MIN: 22.201820
RESULT: baseline: METEOR: RESAMPLED_MAX: 27.623659
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 56.530460
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.252772
RESULT: baseline: TER: RESAMPLED_MIN: 50.178026
RESULT: baseline: TER: RESAMPLED_MAX: 62.611125
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.382969
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.354912
RESULT: baseline: Length: RESAMPLED_MIN: 99.851227
RESULT: baseline: Length: RESAMPLED_MAX: 103.747433
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 22.028967
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.156599
RESULT: system 1: BLEU: RESAMPLED_MIN: 15.515673
RESULT: system 1: BLEU: RESAMPLED_MAX: 28.985580
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 25.056071
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.479646
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.804183
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.566731
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 56.145605
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.245138
RESULT: system 1: TER: RESAMPLED_MIN: 50.305033
RESULT: system 1: TER: RESAMPLED_MAX: 63.199390
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.643186
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.358638
RESULT: system 1: Length: RESAMPLED_MIN: 100.000000
RESULT: system 1: Length: RESAMPLED_MAX: 104.208167
Performed bootstrap resampling in 10.4 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.001400
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.001200
RESULT: system 1: Length: P_VALUE: 0.000200
Performed approximate randomization in 5.54 s
Writing Latex table to /media/ye/project2/tool/multeval/dw-my-bk.tran-vs-tri.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       21.5 (1.2/1.4/-)       24.6 (0.5/0.5/-)       56.5 (1.3/0.8/-)       101.4 (0.4/0.2/-)      
system 1       22.0 (1.2/1.3/0.00)    25.1 (0.5/0.4/0.00)    56.1 (1.2/0.8/0.00)    101.6 (0.4/0.3/0.00)   
==========
Evaluation for bk-my-rk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.03 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.64 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 38.067441
RESULT: baseline: BLEU: MEDIAN: 38.678206
RESULT: baseline: BLEU: STDDEV: 1.081014
RESULT: baseline: BLEU: MIN: 36.531621
RESULT: baseline: BLEU: MAX: 39.524288
RESULT: baseline: BLEU: MEDIAN_IDX: 8.000000
RESULT: system 1: BLEU: AVG: 39.109911
RESULT: system 1: BLEU: MEDIAN: 39.553497
RESULT: system 1: BLEU: STDDEV: 1.140862
RESULT: system 1: BLEU: MIN: 36.648374
RESULT: system 1: BLEU: MAX: 40.495678
RESULT: system 1: BLEU: MEDIAN_IDX: 5.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 32.296889
RESULT: baseline: METEOR: MEDIAN: 32.415859
RESULT: baseline: METEOR: STDDEV: 0.362787
RESULT: baseline: METEOR: MIN: 31.826429
RESULT: baseline: METEOR: MAX: 32.763816
RESULT: baseline: METEOR: MEDIAN_IDX: 2.000000
RESULT: system 1: METEOR: AVG: 32.815977
RESULT: system 1: METEOR: MEDIAN: 33.076160
RESULT: system 1: METEOR: STDDEV: 0.541591
RESULT: system 1: METEOR: MIN: 31.736482
RESULT: system 1: METEOR: MAX: 33.362702
RESULT: system 1: METEOR: MEDIAN_IDX: 2.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 45.688744
RESULT: baseline: TER: MEDIAN: 46.019900
RESULT: baseline: TER: STDDEV: 1.097256
RESULT: baseline: TER: MIN: 43.952114
RESULT: baseline: TER: MAX: 47.030473
RESULT: baseline: TER: MEDIAN_IDX: 8.000000
RESULT: system 1: TER: AVG: 44.479167
RESULT: system 1: TER: MEDIAN: 44.542910
RESULT: system 1: TER: STDDEV: 1.185460
RESULT: system 1: TER: MIN: 42.335199
RESULT: system 1: TER: MAX: 46.128731
RESULT: system 1: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.705263
RESULT: baseline: Length: MEDIAN: 101.611949
RESULT: baseline: Length: STDDEV: 0.260411
RESULT: baseline: Length: MIN: 101.456019
RESULT: baseline: Length: MAX: 102.097693
RESULT: baseline: Length: MEDIAN_IDX: 5.000000
RESULT: system 1: Length: AVG: 101.546450
RESULT: system 1: Length: MEDIAN: 101.507902
RESULT: system 1: Length: STDDEV: 0.206090
RESULT: system 1: Length: MIN: 101.264128
RESULT: system 1: Length: MAX: 101.943780
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [။ x 123, ကို x 64, ရေ x 56, ပါ x 52, သူ x 32, တိ x 29, မ x 28, နီရေ x 27, ငါ x 26, ကျွန်တော် x 26]
Top unmatched reference words accoring to METEOR: [ကို x 59, ။ x 47, ရေ x 37, မင်း x 31, ကျွန်တော် x 30, ရို့ x 28, ထိုမချေ x 27, ယင်းချင့် x 26, သူ x 25, ငါ x 24]
Top unmatched hypothesis words accoring to METEOR: [။ x 113, ကို x 65, ပါ x 52, ရေ x 49, သူ x 32, ပါလား x 28, တိ x 28, မ x 26, ငါ x 26, မင်း x 26]
Top unmatched reference words accoring to METEOR: [ကို x 54, ။ x 34, ရေ x 34, မင်း x 32, သူ x 27, က x 24, ပါ x 24, ပါရေ x 24, လေး x 24, ငါ x 23]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run2/sentLevel/bk-my-rk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run2/rank/bk-my-rk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 38.064114
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.070282
RESULT: baseline: BLEU: RESAMPLED_MIN: 32.588083
RESULT: baseline: BLEU: RESAMPLED_MAX: 43.789705
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 32.297989
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.461322
RESULT: baseline: METEOR: RESAMPLED_MIN: 29.985765
RESULT: baseline: METEOR: RESAMPLED_MAX: 34.470978
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 45.688635
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.048588
RESULT: baseline: TER: RESAMPLED_MIN: 40.523691
RESULT: baseline: TER: RESAMPLED_MAX: 51.714464
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.704691
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.286861
RESULT: baseline: Length: RESAMPLED_MIN: 100.075643
RESULT: baseline: Length: RESAMPLED_MAX: 103.273104
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 39.113282
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.080863
RESULT: system 1: BLEU: RESAMPLED_MIN: 32.496218
RESULT: system 1: BLEU: RESAMPLED_MAX: 45.324115
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 32.821394
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.466954
RESULT: system 1: METEOR: RESAMPLED_MIN: 29.962566
RESULT: system 1: METEOR: RESAMPLED_MAX: 35.313919
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 44.470025
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.043688
RESULT: system 1: TER: RESAMPLED_MIN: 38.920852
RESULT: system 1: TER: RESAMPLED_MAX: 51.091363
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.546546
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.278539
RESULT: system 1: Length: RESAMPLED_MIN: 99.913954
RESULT: system 1: Length: RESAMPLED_MAX: 102.982404
Performed bootstrap resampling in 18.1 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.000100
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.000100
Performed approximate randomization in 13.0 s
Writing Latex table to /media/ye/project2/tool/multeval/bk-my-rk.tran-vs-tri.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       38.1 (1.1/1.1/-)       32.3 (0.5/0.4/-)       45.7 (1.0/1.1/-)       101.7 (0.3/0.3/-)      
system 1       39.1 (1.1/1.1/0.00)    32.8 (0.5/0.5/0.00)    44.5 (1.0/1.2/0.00)    101.5 (0.3/0.2/0.00)   
==========
Evaluation for rk-my-bk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.00 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.58 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 32.513436
RESULT: baseline: BLEU: MEDIAN: 32.695810
RESULT: baseline: BLEU: STDDEV: 0.630776
RESULT: baseline: BLEU: MIN: 31.557934
RESULT: baseline: BLEU: MAX: 33.614592
RESULT: baseline: BLEU: MEDIAN_IDX: 9.000000
RESULT: system 1: BLEU: AVG: 32.005802
RESULT: system 1: BLEU: MEDIAN: 32.296170
RESULT: system 1: BLEU: STDDEV: 0.971518
RESULT: system 1: BLEU: MIN: 30.872371
RESULT: system 1: BLEU: MAX: 33.392403
RESULT: system 1: BLEU: MEDIAN_IDX: 7.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.671726
RESULT: baseline: METEOR: MEDIAN: 29.695654
RESULT: baseline: METEOR: STDDEV: 0.362983
RESULT: baseline: METEOR: MIN: 29.203431
RESULT: baseline: METEOR: MAX: 30.262589
RESULT: baseline: METEOR: MEDIAN_IDX: 2.000000
RESULT: system 1: METEOR: AVG: 29.590991
RESULT: system 1: METEOR: MEDIAN: 29.892847
RESULT: system 1: METEOR: STDDEV: 0.506059
RESULT: system 1: METEOR: MIN: 28.753944
RESULT: system 1: METEOR: MAX: 30.169151
RESULT: system 1: METEOR: MEDIAN_IDX: 7.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 48.867463
RESULT: baseline: TER: MEDIAN: 48.943985
RESULT: baseline: TER: STDDEV: 0.927551
RESULT: baseline: TER: MIN: 47.183961
RESULT: baseline: TER: MAX: 50.520355
RESULT: baseline: TER: MEDIAN_IDX: 7.000000
RESULT: system 1: TER: AVG: 49.196511
RESULT: system 1: TER: MEDIAN: 49.035813
RESULT: system 1: TER: STDDEV: 1.047645
RESULT: system 1: TER: MIN: 47.199265
RESULT: system 1: TER: MAX: 50.811142
RESULT: system 1: TER: MEDIAN_IDX: 2.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.917451
RESULT: baseline: Length: MEDIAN: 101.895173
RESULT: baseline: Length: STDDEV: 0.380179
RESULT: baseline: Length: MIN: 101.422351
RESULT: baseline: Length: MAX: 102.507793
RESULT: baseline: Length: MEDIAN_IDX: 0.000000
RESULT: system 1: Length: AVG: 101.979082
RESULT: system 1: Length: MEDIAN: 102.079528
RESULT: system 1: Length: STDDEV: 0.281791
RESULT: system 1: Length: MIN: 101.459538
RESULT: system 1: Length: MAX: 102.309109
RESULT: system 1: Length: MEDIAN_IDX: 3.000000
Top unmatched hypothesis words accoring to METEOR: [ကို x 66, ဝို x 54, နင် x 53, ဒယ်ကောင်မငယ် x 43, ရယ် x 40, က x 27, ငါ x 26, ရ x 25, ဝို့ x 25, မ x 23]
Top unmatched reference words accoring to METEOR: [ကို x 74, ဝို x 57, ။ x 43, မင်း x 40, မ x 33, သူ x 32, ငါ x 31, နေရယ် x 26, ရယ် x 24, နင့် x 23]
Top unmatched hypothesis words accoring to METEOR: [ကို x 109, နင် x 70, ရယ် x 44, ရ x 42, မ x 39, ဝို x 38, ဒယ်ကောင်မငယ် x 35, က x 31, ကျွန်တော် x 29, ရလား x 28]
Top unmatched reference words accoring to METEOR: [ဝို x 50, မင်း x 44, ကို x 43, ။ x 40, က x 33, ဝို့ x 31, သူ x 29, ငါ x 25, ရယ် x 22, နင် x 22]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run2/sentLevel/rk-my-bk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run2/rank/rk-my-bk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 32.508503
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.027855
RESULT: baseline: BLEU: RESAMPLED_MIN: 27.587630
RESULT: baseline: BLEU: RESAMPLED_MAX: 37.421846
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.672468
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.440281
RESULT: baseline: METEOR: RESAMPLED_MIN: 27.636765
RESULT: baseline: METEOR: RESAMPLED_MAX: 31.998524
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 48.870893
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.097468
RESULT: baseline: TER: RESAMPLED_MIN: 43.538767
RESULT: baseline: TER: RESAMPLED_MAX: 54.750230
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.917883
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.307841
RESULT: baseline: Length: RESAMPLED_MIN: 100.323815
RESULT: baseline: Length: RESAMPLED_MAX: 103.899761
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 32.002202
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.023913
RESULT: system 1: BLEU: RESAMPLED_MIN: 27.058701
RESULT: system 1: BLEU: RESAMPLED_MAX: 37.838852
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 29.592994
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.437133
RESULT: system 1: METEOR: RESAMPLED_MIN: 27.188774
RESULT: system 1: METEOR: RESAMPLED_MAX: 32.009709
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 49.194655
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.093117
RESULT: system 1: TER: RESAMPLED_MIN: 43.499541
RESULT: system 1: TER: RESAMPLED_MAX: 56.429559
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.978704
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.305317
RESULT: system 1: Length: RESAMPLED_MIN: 100.473662
RESULT: system 1: Length: RESAMPLED_MAX: 103.774385
Performed bootstrap resampling in 18.3 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.000200
RESULT: system 1: METEOR: P_VALUE: 0.120388
RESULT: system 1: TER: P_VALUE: 0.000700
RESULT: system 1: Length: P_VALUE: 0.077992
Performed approximate randomization in 13.3 s
Writing Latex table to /media/ye/project2/tool/multeval/rk-my-bk.tran-vs-tri.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       32.5 (1.0/0.6/-)       29.7 (0.4/0.4/-)       48.9 (1.1/0.9/-)       101.9 (0.3/0.4/-)      
system 1       32.0 (1.0/1.0/0.00)    29.6 (0.4/0.5/0.12)    49.2 (1.1/1.0/0.00)    102.0 (0.3/0.3/0.08)   
==========

real	2m7.098s
user	13m44.394s
sys	0m2.134s
(base) ye@:/media/ye/project2/tool/multeval$
```

run2.log ကို ကြည့်ကြည့်တော့ ရလဒ်တွေက အောက်ပါအတိုင်း...  

```
Evaluation for bk-my-dw ...
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       19.0 (1.1/1.0/-)       24.7 (0.5/0.4/-)       60.9 (1.4/1.2/-)       102.6 (0.4/0.4/-)      
system 1       19.0 (1.1/0.9/0.98)    24.4 (0.5/0.4/0.00)    59.6 (1.3/0.7/0.00)    102.2 (0.4/0.4/0.00)   
==========
Evaluation for dw-my-bk ...
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       21.5 (1.2/1.4/-)       24.6 (0.5/0.5/-)       56.5 (1.3/0.8/-)       101.4 (0.4/0.2/-)      
system 1       22.0 (1.2/1.3/0.00)    25.1 (0.5/0.4/0.00)    56.1 (1.2/0.8/0.00)    101.6 (0.4/0.3/0.00)   
==========
Evaluation for bk-my-rk ...
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       38.1 (1.1/1.1/-)       32.3 (0.5/0.4/-)       45.7 (1.0/1.1/-)       101.7 (0.3/0.3/-)      
system 1       39.1 (1.1/1.1/0.00)    32.8 (0.5/0.5/0.00)    44.5 (1.0/1.2/0.00)    101.5 (0.3/0.2/0.00)   
==========
Evaluation for rk-my-bk ...
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       32.5 (1.0/0.6/-)       29.7 (0.4/0.4/-)       48.9 (1.1/0.9/-)       101.9 (0.3/0.4/-)      
system 1       32.0 (1.0/1.0/0.00)    29.6 (0.4/0.5/0.12)    49.2 (1.1/1.0/0.00)    102.0 (0.3/0.3/0.08)   
==========
```

## Comparing Sys2 vs Sys1

ဒီတစ်ခါတော့ Triangulation ကို baseline မှာထားပြီးတော့ Transfer ကို System-1 အနေနဲ့ ထားပြီး run ဖို့ ပြင်ဆင်ခဲ့။ updated shell script က အောက်ပါအတိုင်း   

```
#!/bin/bash

# run on 19 Jan 2022
# ဒီတစ်ခါတော့ Triangulation ကို baseline အဖြစ်ထားပြီးတော့ Transfer ကို sys1 အနေနဲ့ထား run ကြည့်ခဲ့တယ်

# for bk-my-dw
echo "Evaluation for bk-my-dw ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt* \
--meteor.language en \
--latex run3/latex/bk-my-dw.tran-vs-tri.tex \
--rankDir run3/rank/bk-my-dw \
--sentLevelDir run3/sentLevel/bk-my-dw
echo "==========";

# for dw-my-bk
echo "Evaluation for dw-my-bk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt* \
--meteor.language en \
--latex run3/latex/dw-my-bk.tran-vs-tri.tex \
--rankDir run3/rank/dw-my-bk \
--sentLevelDir run3/sentLevel/dw-my-bk
echo "==========";

# for bk-my-rk
echo "Evaluation for bk-my-rk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt* \
--meteor.language en \
--latex run3/latex/bk-my-rk.tran-vs-tri.tex \
--rankDir run3/rank/bk-my-rk \
--sentLevelDir run3/sentLevel/bk-my-rk
echo "==========";

# for rk-my-bk
echo "Evaluation for rk-my-bk ...";
./multeval.sh eval --refs /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref* \
--hyps-sys1 /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt* \
--hyps-baseline /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt* \
--meteor.language en \
--latex run3/latex/rk-my-bk.tran-vs-tri.tex \
--rankDir run3/rank/rk-my-bk \
--sentLevelDir run3/sentLevel/rk-my-bk
echo "==========";

```

running output က အောက်ပါအတိုင်း

```
(base) ye@:/media/ye/project2/tool/multeval$ time ./run3.sh | tee run3.log
Evaluation for bk-my-dw ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.05 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/triangulation.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/transfer.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-dw/bk-my-dw.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.03 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 19.043974
RESULT: baseline: BLEU: MEDIAN: 18.886349
RESULT: baseline: BLEU: STDDEV: 0.905266
RESULT: baseline: BLEU: MIN: 17.737365
RESULT: baseline: BLEU: MAX: 20.552394
RESULT: baseline: BLEU: MEDIAN_IDX: 8.000000
RESULT: system 1: BLEU: AVG: 19.042434
RESULT: system 1: BLEU: MEDIAN: 19.102299
RESULT: system 1: BLEU: STDDEV: 1.048039
RESULT: system 1: BLEU: MIN: 17.244120
RESULT: system 1: BLEU: MAX: 20.292390
RESULT: system 1: BLEU: MEDIAN_IDX: 7.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 24.406830
RESULT: baseline: METEOR: MEDIAN: 24.303646
RESULT: baseline: METEOR: STDDEV: 0.406750
RESULT: baseline: METEOR: MIN: 23.818734
RESULT: baseline: METEOR: MAX: 25.041214
RESULT: baseline: METEOR: MEDIAN_IDX: 8.000000
RESULT: system 1: METEOR: AVG: 24.671590
RESULT: system 1: METEOR: MEDIAN: 24.777206
RESULT: system 1: METEOR: STDDEV: 0.437853
RESULT: system 1: METEOR: MIN: 23.899297
RESULT: system 1: METEOR: MAX: 25.182453
RESULT: system 1: METEOR: MEDIAN_IDX: 1.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 59.632122
RESULT: baseline: TER: MEDIAN: 59.730821
RESULT: baseline: TER: STDDEV: 0.740120
RESULT: baseline: TER: MIN: 58.250336
RESULT: baseline: TER: MAX: 60.699865
RESULT: baseline: TER: MEDIAN_IDX: 3.000000
RESULT: system 1: TER: AVG: 60.912218
RESULT: system 1: TER: MEDIAN: 60.915209
RESULT: system 1: TER: STDDEV: 1.159928
RESULT: system 1: TER: MIN: 59.057873
RESULT: system 1: TER: MAX: 63.230148
RESULT: system 1: TER: MEDIAN_IDX: 1.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 102.151654
RESULT: baseline: Length: MEDIAN: 102.154848
RESULT: baseline: Length: STDDEV: 0.393246
RESULT: baseline: Length: MIN: 101.633576
RESULT: baseline: Length: MAX: 102.794006
RESULT: baseline: Length: MEDIAN_IDX: 4.000000
RESULT: system 1: Length: AVG: 102.571126
RESULT: system 1: Length: MEDIAN: 102.521632
RESULT: system 1: Length: STDDEV: 0.369614
RESULT: system 1: Length: MIN: 102.188716
RESULT: system 1: Length: MAX: 103.390250
RESULT: system 1: Length: MEDIAN_IDX: 6.000000
Top unmatched hypothesis words accoring to METEOR: [ကျွန်တော် x 48, ဟှ x 47, ဟှို x 38, ဟှယ် x 34, သူ x 33, နန် x 26, လောက် x 20, မ x 19, သူးနို့ x 19, ငါ့ x 18]
Top unmatched reference words accoring to METEOR: [ဟှို x 52, ဟှယ် x 29, ဟှ x 25, နန် x 23, မ x 22, နူး x 21, ငါ x 20, ဟှို့ x 16, ကျွန်တော် x 16, လေ x 14]
Top unmatched hypothesis words accoring to METEOR: [ဟှို x 82, ဟှယ် x 43, သူ x 42, နန် x 38, ဟှ x 34, ကျွန်တော် x 34, ဟှို့ x 32, မ x 28, လား x 27, နူး x 22]
Top unmatched reference words accoring to METEOR: [ဟှို x 25, ဟှယ် x 23, နန် x 22, ဟှ x 20, ကျွန်တော် x 20, ငါ x 19, ခံဗျား x 19, ဝို x 16, သူ x 16, နူး x 15]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run3/sentLevel/bk-my-dw
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run3/rank/bk-my-dw
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 19.029961
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.105978
RESULT: baseline: BLEU: RESAMPLED_MIN: 14.004157
RESULT: baseline: BLEU: RESAMPLED_MAX: 25.132465
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 24.407412
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.466936
RESULT: baseline: METEOR: RESAMPLED_MIN: 21.941675
RESULT: baseline: METEOR: RESAMPLED_MAX: 26.687788
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 59.634237
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.333503
RESULT: baseline: TER: RESAMPLED_MIN: 53.578180
RESULT: baseline: TER: RESAMPLED_MAX: 66.147233
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 102.151475
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.358959
RESULT: baseline: Length: RESAMPLED_MIN: 100.300375
RESULT: baseline: Length: RESAMPLED_MAX: 104.388164
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 19.025413
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.100964
RESULT: system 1: BLEU: RESAMPLED_MIN: 13.462324
RESULT: system 1: BLEU: RESAMPLED_MAX: 24.875040
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 24.672374
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.466260
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.323792
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.172323
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 60.912399
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.382142
RESULT: system 1: TER: RESAMPLED_MIN: 53.653949
RESULT: system 1: TER: RESAMPLED_MAX: 68.534483
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 102.570424
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.375756
RESULT: system 1: Length: RESAMPLED_MIN: 100.830189
RESULT: system 1: Length: RESAMPLED_MAX: 105.502988
Performed bootstrap resampling in 9.97 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.983202
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.000100
Performed approximate randomization in 5.20 s
Writing Latex table to /media/ye/project2/tool/multeval/run3/latex/bk-my-dw.tran-vs-tri.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       19.0 (1.1/0.9/-)       24.4 (0.5/0.4/-)       59.6 (1.3/0.7/-)       102.2 (0.4/0.4/-)      
system 1       19.0 (1.1/1.0/0.98)    24.7 (0.5/0.4/0.00)    60.9 (1.4/1.2/0.00)    102.6 (0.4/0.4/0.00)   
==========
Evaluation for dw-my-bk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.06 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt2
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt3
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt4
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt5
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt6
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt7
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt8
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/triangulation.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt2
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt3
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt4
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt5
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt6
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt7
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt8
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/transfer.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/dw-my-bk/dw-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 1.84 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 22.045627
RESULT: baseline: BLEU: MEDIAN: 22.301236
RESULT: baseline: BLEU: STDDEV: 1.273386
RESULT: baseline: BLEU: MIN: 20.035715
RESULT: baseline: BLEU: MAX: 23.748817
RESULT: baseline: BLEU: MEDIAN_IDX: 4.000000
RESULT: system 1: BLEU: AVG: 21.497999
RESULT: system 1: BLEU: MEDIAN: 21.541367
RESULT: system 1: BLEU: STDDEV: 1.372429
RESULT: system 1: BLEU: MIN: 19.399643
RESULT: system 1: BLEU: MAX: 23.412333
RESULT: system 1: BLEU: MEDIAN_IDX: 0.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 25.056533
RESULT: baseline: METEOR: MEDIAN: 25.227676
RESULT: baseline: METEOR: STDDEV: 0.447235
RESULT: baseline: METEOR: MIN: 24.440269
RESULT: baseline: METEOR: MAX: 25.569590
RESULT: baseline: METEOR: MEDIAN_IDX: 0.000000
RESULT: system 1: METEOR: AVG: 24.623296
RESULT: system 1: METEOR: MEDIAN: 24.589827
RESULT: system 1: METEOR: STDDEV: 0.489732
RESULT: system 1: METEOR: MIN: 24.020333
RESULT: system 1: METEOR: MAX: 25.380568
RESULT: system 1: METEOR: MEDIAN_IDX: 0.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 56.140647
RESULT: baseline: TER: MEDIAN: 55.873418
RESULT: baseline: TER: STDDEV: 0.830163
RESULT: baseline: TER: MIN: 55.316456
RESULT: baseline: TER: MAX: 57.417722
RESULT: baseline: TER: MEDIAN_IDX: 1.000000
RESULT: system 1: TER: AVG: 56.534459
RESULT: system 1: TER: MEDIAN: 56.481013
RESULT: system 1: TER: STDDEV: 0.813920
RESULT: system 1: TER: MIN: 55.291139
RESULT: system 1: TER: MAX: 58.278481
RESULT: system 1: TER: MEDIAN_IDX: 3.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.644897
RESULT: baseline: Length: MEDIAN: 101.577520
RESULT: baseline: Length: STDDEV: 0.265569
RESULT: baseline: Length: MIN: 101.344861
RESULT: baseline: Length: MAX: 102.212829
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
RESULT: system 1: Length: AVG: 101.383627
RESULT: system 1: Length: MEDIAN: 101.377275
RESULT: system 1: Length: STDDEV: 0.236002
RESULT: system 1: Length: MIN: 101.013848
RESULT: system 1: Length: MAX: 101.725838
RESULT: system 1: Length: MEDIAN_IDX: 2.000000
Top unmatched hypothesis words accoring to METEOR: [နင် x 55, ကို x 52, ငါ x 48, မ x 29, ရိ x 28, သူ x 24, ရ x 22, ရယ် x 22, မှာ x 21, နေရယ် x 21]
Top unmatched reference words accoring to METEOR: [မ x 38, ကို x 30, ဝို x 29, မင်း x 29, ရယ် x 19, ငါ x 18, ဝ x 17, သူ x 17, ကျွန်တော် x 17, က x 16]
Top unmatched hypothesis words accoring to METEOR: [နင် x 63, ကို x 58, ငါ x 41, ရိ x 29, ရယ် x 24, မှာ x 23, ရ x 22, သူ x 22, ဒယ်ကောင်မငယ် x 19, က x 18]
Top unmatched reference words accoring to METEOR: [မ x 43, ကို x 40, မင်း x 38, ဝို x 30, ငါ x 21, ဝ x 19, ကျွန်တော် x 19, သူ x 17, နေရယ် x 17, က x 16]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run3/sentLevel/dw-my-bk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run3/rank/dw-my-bk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 9)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 22.031130
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.158419
RESULT: baseline: BLEU: RESAMPLED_MIN: 16.138143
RESULT: baseline: BLEU: RESAMPLED_MAX: 28.236582
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 25.057005
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.479910
RESULT: baseline: METEOR: RESAMPLED_MIN: 22.659716
RESULT: baseline: METEOR: RESAMPLED_MAX: 27.679065
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 56.142353
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.250124
RESULT: baseline: TER: RESAMPLED_MIN: 50.556680
RESULT: baseline: TER: RESAMPLED_MAX: 62.468193
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.645760
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.359274
RESULT: baseline: Length: RESAMPLED_MIN: 100.072957
RESULT: baseline: Length: RESAMPLED_MAX: 104.530982
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 9)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 9)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 21.489016
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.176787
RESULT: system 1: BLEU: RESAMPLED_MIN: 14.794733
RESULT: system 1: BLEU: RESAMPLED_MAX: 28.954009
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 24.627025
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.480500
RESULT: system 1: METEOR: RESAMPLED_MIN: 22.224929
RESULT: system 1: METEOR: RESAMPLED_MAX: 27.757920
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 56.532538
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.253370
RESULT: system 1: TER: RESAMPLED_MIN: 50.100806
RESULT: system 1: TER: RESAMPLED_MAX: 62.653374
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.382132
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.355090
RESULT: system 1: Length: RESAMPLED_MIN: 99.774040
RESULT: system 1: Length: RESAMPLED_MAX: 103.698075
Performed bootstrap resampling in 10.1 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.002100
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.001100
RESULT: system 1: Length: P_VALUE: 0.000100
Performed approximate randomization in 6.03 s
Writing Latex table to /media/ye/project2/tool/multeval/run3/latex/dw-my-bk.tran-vs-tri.tex
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       22.0 (1.2/1.3/-)       25.1 (0.5/0.4/-)       56.1 (1.3/0.8/-)       101.6 (0.4/0.3/-)      
system 1       21.5 (1.2/1.4/0.00)    24.6 (0.5/0.5/0.00)    56.5 (1.3/0.8/0.00)    101.4 (0.4/0.2/0.00)   
==========
Evaluation for bk-my-rk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.10 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/triangulation.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/transfer.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/bk-my-rk/bk-my-rk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.79 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 39.109911
RESULT: baseline: BLEU: MEDIAN: 39.553497
RESULT: baseline: BLEU: STDDEV: 1.140862
RESULT: baseline: BLEU: MIN: 36.648374
RESULT: baseline: BLEU: MAX: 40.495678
RESULT: baseline: BLEU: MEDIAN_IDX: 5.000000
RESULT: system 1: BLEU: AVG: 38.067441
RESULT: system 1: BLEU: MEDIAN: 38.678206
RESULT: system 1: BLEU: STDDEV: 1.081014
RESULT: system 1: BLEU: MIN: 36.531621
RESULT: system 1: BLEU: MAX: 39.524288
RESULT: system 1: BLEU: MEDIAN_IDX: 8.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 32.815977
RESULT: baseline: METEOR: MEDIAN: 33.076160
RESULT: baseline: METEOR: STDDEV: 0.541591
RESULT: baseline: METEOR: MIN: 31.736482
RESULT: baseline: METEOR: MAX: 33.362702
RESULT: baseline: METEOR: MEDIAN_IDX: 2.000000
RESULT: system 1: METEOR: AVG: 32.296889
RESULT: system 1: METEOR: MEDIAN: 32.415859
RESULT: system 1: METEOR: STDDEV: 0.362787
RESULT: system 1: METEOR: MIN: 31.826429
RESULT: system 1: METEOR: MAX: 32.763816
RESULT: system 1: METEOR: MEDIAN_IDX: 2.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 44.479167
RESULT: baseline: TER: MEDIAN: 44.542910
RESULT: baseline: TER: STDDEV: 1.185460
RESULT: baseline: TER: MIN: 42.335199
RESULT: baseline: TER: MAX: 46.128731
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
RESULT: system 1: TER: AVG: 45.688744
RESULT: system 1: TER: MEDIAN: 46.019900
RESULT: system 1: TER: STDDEV: 1.097256
RESULT: system 1: TER: MIN: 43.952114
RESULT: system 1: TER: MAX: 47.030473
RESULT: system 1: TER: MEDIAN_IDX: 8.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.546450
RESULT: baseline: Length: MEDIAN: 101.507902
RESULT: baseline: Length: STDDEV: 0.206090
RESULT: baseline: Length: MIN: 101.264128
RESULT: baseline: Length: MAX: 101.943780
RESULT: baseline: Length: MEDIAN_IDX: 2.000000
RESULT: system 1: Length: AVG: 101.705263
RESULT: system 1: Length: MEDIAN: 101.611949
RESULT: system 1: Length: STDDEV: 0.260411
RESULT: system 1: Length: MIN: 101.456019
RESULT: system 1: Length: MAX: 102.097693
RESULT: system 1: Length: MEDIAN_IDX: 5.000000
Top unmatched hypothesis words accoring to METEOR: [။ x 113, ကို x 65, ပါ x 52, ရေ x 49, သူ x 32, ပါလား x 28, တိ x 28, မ x 26, ငါ x 26, မင်း x 26]
Top unmatched reference words accoring to METEOR: [ကို x 54, ။ x 34, ရေ x 34, မင်း x 32, သူ x 27, က x 24, ပါ x 24, ပါရေ x 24, လေး x 24, ငါ x 23]
Top unmatched hypothesis words accoring to METEOR: [။ x 123, ကို x 64, ရေ x 56, ပါ x 52, သူ x 32, တိ x 29, မ x 28, နီရေ x 27, ငါ x 26, ကျွန်တော် x 26]
Top unmatched reference words accoring to METEOR: [ကို x 59, ။ x 47, ရေ x 37, မင်း x 31, ကျွန်တော် x 30, ရို့ x 28, ထိုမချေ x 27, ယင်းချင့် x 26, သူ x 25, ငါ x 24]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run3/sentLevel/bk-my-rk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run3/rank/bk-my-rk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 39.107429
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.084857
RESULT: baseline: BLEU: RESAMPLED_MIN: 32.711923
RESULT: baseline: BLEU: RESAMPLED_MAX: 44.510515
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 32.817435
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.467933
RESULT: baseline: METEOR: RESAMPLED_MIN: 29.853352
RESULT: baseline: METEOR: RESAMPLED_MAX: 35.215738
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 44.481909
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.043382
RESULT: baseline: TER: RESAMPLED_MIN: 38.630731
RESULT: baseline: TER: RESAMPLED_MAX: 50.480025
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.546985
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.279449
RESULT: baseline: Length: RESAMPLED_MIN: 100.104853
RESULT: baseline: Length: RESAMPLED_MAX: 103.362465
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 38.060601
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.069335
RESULT: system 1: BLEU: RESAMPLED_MIN: 32.273679
RESULT: system 1: BLEU: RESAMPLED_MAX: 43.927808
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 32.297501
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.462359
RESULT: system 1: METEOR: RESAMPLED_MIN: 30.058516
RESULT: system 1: METEOR: RESAMPLED_MAX: 34.628238
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 45.692977
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.051750
RESULT: system 1: TER: RESAMPLED_MIN: 40.100094
RESULT: system 1: TER: RESAMPLED_MAX: 51.257373
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.704917
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.287516
RESULT: system 1: Length: RESAMPLED_MIN: 100.373804
RESULT: system 1: Length: RESAMPLED_MAX: 103.319188
Performed bootstrap resampling in 18.2 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.000100
RESULT: system 1: METEOR: P_VALUE: 0.000100
RESULT: system 1: TER: P_VALUE: 0.000100
RESULT: system 1: Length: P_VALUE: 0.000100
Performed approximate randomization in 13.5 s
Writing Latex table to /media/ye/project2/tool/multeval/run3/latex/bk-my-rk.tran-vs-tri.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       39.1 (1.1/1.1/-)       32.8 (0.5/0.5/-)       44.5 (1.0/1.2/-)       101.5 (0.3/0.2/-)      
system 1       38.1 (1.1/1.1/0.00)    32.3 (0.5/0.4/0.00)    45.7 (1.1/1.1/0.00)    101.7 (0.3/0.3/0.00)   
==========
Evaluation for rk-my-bk ...
Found existing METEOR installation at ./lib/meteor-1.4
MultEval V0.5.1
By Jonathan Clark
Using Libraries: METEOR (Michael Denkowski) and TER (Matthew Snover)

Loading metric: bleu
Loading metric: meteor
Loading metric: ter
Loading metric: length
Found library jBLEU at file:/media/ye/project2/tool/multeval/multeval-0.5.1.jar
Found library METEOR at file:/media/ye/project2/tool/multeval/lib/meteor-1.4/meteor-1.4.jar
Using METEOR Version 1.4
Loading METEOR paraphrase table...
Loaded METEOR in 5.00 s
Found library TER at file:/media/ye/project2/tool/multeval/lib/tercom-0.8.0.jar
Using 8 threads
Reading Hypotheses for system baseline opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt1
Reading Hypotheses for system baseline opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt10
Reading Hypotheses for system baseline opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt2
Reading Hypotheses for system baseline opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt3
Reading Hypotheses for system baseline opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt4
Reading Hypotheses for system baseline opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt5
Reading Hypotheses for system baseline opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt6
Reading Hypotheses for system baseline opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt7
Reading Hypotheses for system baseline opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt8
Reading Hypotheses for system baseline opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/triangulation.opt9
Reading Hypotheses for system 1 opt run 1 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt1
Reading Hypotheses for system 1 opt run 2 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt10
Reading Hypotheses for system 1 opt run 3 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt2
Reading Hypotheses for system 1 opt run 4 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt3
Reading Hypotheses for system 1 opt run 5 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt4
Reading Hypotheses for system 1 opt run 6 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt5
Reading Hypotheses for system 1 opt run 7 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt6
Reading Hypotheses for system 1 opt run 8 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt7
Reading Hypotheses for system 1 opt run 9 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt8
Reading Hypotheses for system 1 opt run 10 file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/transfer.opt9
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref1
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref10
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref2
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref3
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref4
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref5
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref6
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref7
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref8
Reading non-laced references file /media/ye/project2/thazin-journal/pivot-journal/18Oct2021/mdpi-latex/draft-ver1/mteval-running/data4eval-pivot-10fold/rk-my-bk/rk-my-bk.ref9
Collecting sufficient statistics for metric: BLEU
Finished collecting sufficient statistics for metric: BLEU
Collecting sufficient statistics for metric: METEOR
Finished collecting sufficient statistics for metric: METEOR
Collecting sufficient statistics for metric: TER
Finished collecting sufficient statistics for metric: TER
Collecting sufficient statistics for metric: Length
Finished collecting sufficient statistics for metric: Length
Collected suff stats in 2.93 s
Scoring with metric: BLEU
RESULT: baseline: BLEU: AVG: 32.005802
RESULT: baseline: BLEU: MEDIAN: 32.296170
RESULT: baseline: BLEU: STDDEV: 0.971518
RESULT: baseline: BLEU: MIN: 30.872371
RESULT: baseline: BLEU: MAX: 33.392403
RESULT: baseline: BLEU: MEDIAN_IDX: 7.000000
RESULT: system 1: BLEU: AVG: 32.513436
RESULT: system 1: BLEU: MEDIAN: 32.695810
RESULT: system 1: BLEU: STDDEV: 0.630776
RESULT: system 1: BLEU: MIN: 31.557934
RESULT: system 1: BLEU: MAX: 33.614592
RESULT: system 1: BLEU: MEDIAN_IDX: 9.000000
Scoring with metric: METEOR
RESULT: baseline: METEOR: AVG: 29.590991
RESULT: baseline: METEOR: MEDIAN: 29.892847
RESULT: baseline: METEOR: STDDEV: 0.506059
RESULT: baseline: METEOR: MIN: 28.753944
RESULT: baseline: METEOR: MAX: 30.169151
RESULT: baseline: METEOR: MEDIAN_IDX: 7.000000
RESULT: system 1: METEOR: AVG: 29.671726
RESULT: system 1: METEOR: MEDIAN: 29.695654
RESULT: system 1: METEOR: STDDEV: 0.362983
RESULT: system 1: METEOR: MIN: 29.203431
RESULT: system 1: METEOR: MAX: 30.262589
RESULT: system 1: METEOR: MEDIAN_IDX: 2.000000
Scoring with metric: TER
RESULT: baseline: TER: AVG: 49.196511
RESULT: baseline: TER: MEDIAN: 49.035813
RESULT: baseline: TER: STDDEV: 1.047645
RESULT: baseline: TER: MIN: 47.199265
RESULT: baseline: TER: MAX: 50.811142
RESULT: baseline: TER: MEDIAN_IDX: 2.000000
RESULT: system 1: TER: AVG: 48.867463
RESULT: system 1: TER: MEDIAN: 48.943985
RESULT: system 1: TER: STDDEV: 0.927551
RESULT: system 1: TER: MIN: 47.183961
RESULT: system 1: TER: MAX: 50.520355
RESULT: system 1: TER: MEDIAN_IDX: 7.000000
Scoring with metric: Length
RESULT: baseline: Length: AVG: 101.979082
RESULT: baseline: Length: MEDIAN: 102.079528
RESULT: baseline: Length: STDDEV: 0.281791
RESULT: baseline: Length: MIN: 101.459538
RESULT: baseline: Length: MAX: 102.309109
RESULT: baseline: Length: MEDIAN_IDX: 3.000000
RESULT: system 1: Length: AVG: 101.917451
RESULT: system 1: Length: MEDIAN: 101.895173
RESULT: system 1: Length: STDDEV: 0.380179
RESULT: system 1: Length: MIN: 101.422351
RESULT: system 1: Length: MAX: 102.507793
RESULT: system 1: Length: MEDIAN_IDX: 0.000000
Top unmatched hypothesis words accoring to METEOR: [ကို x 109, နင် x 70, ရယ် x 44, ရ x 42, မ x 39, ဝို x 38, ဒယ်ကောင်မငယ် x 35, က x 31, ကျွန်တော် x 29, ရလား x 28]
Top unmatched reference words accoring to METEOR: [ဝို x 50, မင်း x 44, ကို x 43, ။ x 40, က x 33, ဝို့ x 31, သူ x 29, ငါ x 25, ရယ် x 22, နင် x 22]
Top unmatched hypothesis words accoring to METEOR: [ကို x 66, ဝို x 54, နင် x 53, ဒယ်ကောင်မငယ် x 43, ရယ် x 40, က x 27, ငါ x 26, ရ x 25, ဝို့ x 25, မ x 23]
Top unmatched reference words accoring to METEOR: [ကို x 74, ဝို x 57, ။ x 43, မင်း x 40, မ x 33, သူ x 32, ငါ x 31, နေရယ် x 26, ရယ် x 24, နင့် x 23]
Outputting sentence level scores to: /media/ye/project2/tool/multeval/run3/sentLevel/rk-my-bk
Outputting ranked hypotheses to: /media/ye/project2/tool/multeval/run3/rank/rk-my-bk
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 1 of 2; opt run 10 of 10)
RESULT: baseline: BLEU: RESAMPLED_MEAN_AVG: 32.000662
RESULT: baseline: BLEU: RESAMPLED_STDDEV_AVG: 1.019533
RESULT: baseline: BLEU: RESAMPLED_MIN: 26.832653
RESULT: baseline: BLEU: RESAMPLED_MAX: 37.832481
RESULT: baseline: METEOR: RESAMPLED_MEAN_AVG: 29.591921
RESULT: baseline: METEOR: RESAMPLED_STDDEV_AVG: 0.435724
RESULT: baseline: METEOR: RESAMPLED_MIN: 27.064067
RESULT: baseline: METEOR: RESAMPLED_MAX: 32.017960
RESULT: baseline: TER: RESAMPLED_MEAN_AVG: 49.200728
RESULT: baseline: TER: RESAMPLED_STDDEV_AVG: 1.090261
RESULT: baseline: TER: RESAMPLED_MIN: 43.145410
RESULT: baseline: TER: RESAMPLED_MAX: 55.122856
RESULT: baseline: Length: RESAMPLED_MEAN_AVG: 101.979021
RESULT: baseline: Length: RESAMPLED_STDDEV_AVG: 0.305957
RESULT: baseline: Length: RESAMPLED_MIN: 100.454739
RESULT: baseline: Length: RESAMPLED_MAX: 103.702122
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 1 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 2 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 3 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 4 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 5 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 6 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 7 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 8 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 9 of 10)
Performing bootstrap resampling to estimate stddev for test set selection (System 2 of 2; opt run 10 of 10)
RESULT: system 1: BLEU: RESAMPLED_MEAN_AVG: 32.512602
RESULT: system 1: BLEU: RESAMPLED_STDDEV_AVG: 1.029000
RESULT: system 1: BLEU: RESAMPLED_MIN: 27.598235
RESULT: system 1: BLEU: RESAMPLED_MAX: 37.954142
RESULT: system 1: METEOR: RESAMPLED_MEAN_AVG: 29.674028
RESULT: system 1: METEOR: RESAMPLED_STDDEV_AVG: 0.441267
RESULT: system 1: METEOR: RESAMPLED_MIN: 27.620360
RESULT: system 1: METEOR: RESAMPLED_MAX: 31.971864
RESULT: system 1: TER: RESAMPLED_MEAN_AVG: 48.862217
RESULT: system 1: TER: RESAMPLED_STDDEV_AVG: 1.095751
RESULT: system 1: TER: RESAMPLED_MIN: 43.020247
RESULT: system 1: TER: RESAMPLED_MAX: 55.441761
RESULT: system 1: Length: RESAMPLED_MEAN_AVG: 101.915412
RESULT: system 1: Length: RESAMPLED_STDDEV_AVG: 0.305975
RESULT: system 1: Length: RESAMPLED_MIN: 100.416786
RESULT: system 1: Length: RESAMPLED_MAX: 103.927918
Performed bootstrap resampling in 18.2 s
Performing approximate randomization to estimate p-value between baseline system and system 2 (of 2)
RESULT: system 1: BLEU: P_VALUE: 0.000100
RESULT: system 1: METEOR: P_VALUE: 0.120188
RESULT: system 1: TER: P_VALUE: 0.000500
RESULT: system 1: Length: P_VALUE: 0.076392
Performed approximate randomization in 13.0 s
Writing Latex table to /media/ye/project2/tool/multeval/run3/latex/rk-my-bk.tran-vs-tri.tex
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       32.0 (1.0/1.0/-)       29.6 (0.4/0.5/-)       49.2 (1.1/1.0/-)       102.0 (0.3/0.3/-)      
system 1       32.5 (1.0/0.6/0.00)    29.7 (0.4/0.4/0.12)    48.9 (1.1/0.9/0.00)    101.9 (0.3/0.4/0.08)   
==========

real	2m7.525s
user	13m45.661s
sys	0m2.273s
(base) ye@:/media/ye/project2/tool/multeval$
```

run3.log ဖိုင်ကို cat လုပ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/tool/multeval$ cat run3.log 
Evaluation for bk-my-dw ...
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       19.0 (1.1/0.9/-)       24.4 (0.5/0.4/-)       59.6 (1.3/0.7/-)       102.2 (0.4/0.4/-)      
system 1       19.0 (1.1/1.0/0.98)    24.7 (0.5/0.4/0.00)    60.9 (1.4/1.2/0.00)    102.6 (0.4/0.4/0.00)   
==========
Evaluation for dw-my-bk ...
n=9            BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       22.0 (1.2/1.3/-)       25.1 (0.5/0.4/-)       56.1 (1.3/0.8/-)       101.6 (0.4/0.3/-)      
system 1       21.5 (1.2/1.4/0.00)    24.6 (0.5/0.5/0.00)    56.5 (1.3/0.8/0.00)    101.4 (0.4/0.2/0.00)   
==========
Evaluation for bk-my-rk ...
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       39.1 (1.1/1.1/-)       32.8 (0.5/0.5/-)       44.5 (1.0/1.2/-)       101.5 (0.3/0.2/-)      
system 1       38.1 (1.1/1.1/0.00)    32.3 (0.5/0.4/0.00)    45.7 (1.1/1.1/0.00)    101.7 (0.3/0.3/0.00)   
==========
Evaluation for rk-my-bk ...
n=10           BLEU (s_sel/s_opt/p)   METEOR (s_sel/s_opt/p) TER (s_sel/s_opt/p)    Length (s_sel/s_opt/p) 
baseline       32.0 (1.0/1.0/-)       29.6 (0.4/0.5/-)       49.2 (1.1/1.0/-)       102.0 (0.3/0.3/-)      
system 1       32.5 (1.0/0.6/0.00)    29.7 (0.4/0.4/0.12)    48.9 (1.1/0.9/0.00)    101.9 (0.3/0.4/0.08)   
==========
(base) ye@:/media/ye/project2/tool/multeval$
```

folder နဲ့ file တွေကို tree command နဲ့ စစ်ဆေးကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/tool/multeval$ tree ./run3
./run3
├── latex
│   ├── bk-my-dw.tran-vs-tri.tex
│   ├── bk-my-rk.tran-vs-tri.tex
│   ├── dw-my-bk.tran-vs-tri.tex
│   └── rk-my-bk.tran-vs-tri.tex
├── rank
│   ├── bk-my-dw
│   │   ├── sys2.sortedby.bleu
│   │   ├── sys2.sortedby.length
│   │   ├── sys2.sortedby.meteor
│   │   └── sys2.sortedby.ter
│   ├── bk-my-rk
│   │   ├── sys2.sortedby.bleu
│   │   ├── sys2.sortedby.length
│   │   ├── sys2.sortedby.meteor
│   │   └── sys2.sortedby.ter
│   ├── dw-my-bk
│   │   ├── sys2.sortedby.bleu
│   │   ├── sys2.sortedby.length
│   │   ├── sys2.sortedby.meteor
│   │   └── sys2.sortedby.ter
│   └── rk-my-bk
│       ├── sys2.sortedby.bleu
│       ├── sys2.sortedby.length
│       ├── sys2.sortedby.meteor
│       └── sys2.sortedby.ter
└── sentLevel
    ├── bk-my-dw
    │   ├── sys1.opt1
    │   ├── sys1.opt2
    │   ├── sys1.opt3
    │   ├── sys1.opt4
    │   ├── sys1.opt5
    │   ├── sys1.opt6
    │   ├── sys1.opt7
    │   ├── sys1.opt8
    │   ├── sys1.opt9
    │   ├── sys2.opt1
    │   ├── sys2.opt2
    │   ├── sys2.opt3
    │   ├── sys2.opt4
    │   ├── sys2.opt5
    │   ├── sys2.opt6
    │   ├── sys2.opt7
    │   ├── sys2.opt8
    │   └── sys2.opt9
    ├── bk-my-rk
    │   ├── sys1.opt1
    │   ├── sys1.opt10
    │   ├── sys1.opt2
    │   ├── sys1.opt3
    │   ├── sys1.opt4
    │   ├── sys1.opt5
    │   ├── sys1.opt6
    │   ├── sys1.opt7
    │   ├── sys1.opt8
    │   ├── sys1.opt9
    │   ├── sys2.opt1
    │   ├── sys2.opt10
    │   ├── sys2.opt2
    │   ├── sys2.opt3
    │   ├── sys2.opt4
    │   ├── sys2.opt5
    │   ├── sys2.opt6
    │   ├── sys2.opt7
    │   ├── sys2.opt8
    │   └── sys2.opt9
    ├── dw-my-bk
    │   ├── sys1.opt1
    │   ├── sys1.opt2
    │   ├── sys1.opt3
    │   ├── sys1.opt4
    │   ├── sys1.opt5
    │   ├── sys1.opt6
    │   ├── sys1.opt7
    │   ├── sys1.opt8
    │   ├── sys1.opt9
    │   ├── sys2.opt1
    │   ├── sys2.opt2
    │   ├── sys2.opt3
    │   ├── sys2.opt4
    │   ├── sys2.opt5
    │   ├── sys2.opt6
    │   ├── sys2.opt7
    │   ├── sys2.opt8
    │   └── sys2.opt9
    └── rk-my-bk
        ├── sys1.opt1
        ├── sys1.opt10
        ├── sys1.opt2
        ├── sys1.opt3
        ├── sys1.opt4
        ├── sys1.opt5
        ├── sys1.opt6
        ├── sys1.opt7
        ├── sys1.opt8
        ├── sys1.opt9
        ├── sys2.opt1
        ├── sys2.opt10
        ├── sys2.opt2
        ├── sys2.opt3
        ├── sys2.opt4
        ├── sys2.opt5
        ├── sys2.opt6
        ├── sys2.opt7
        ├── sys2.opt8
        └── sys2.opt9

11 directories, 96 files
(base) ye@:/media/ye/project2/tool/multeval$
```

## Meteor-1.5-Dbnary version

http://kaiko.getalp.org/about-dbnary/meteor-with-dbnary/  
http://kaiko.getalp.org/about-dbnary/dataset/  


