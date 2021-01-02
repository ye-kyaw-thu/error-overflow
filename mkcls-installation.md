# mkcls Installation and Running Notes

## Introduction to Franz Och's ```mkcls```

mkcls က စာလုံးတွေကို word cluster ဆောက်ဖို့အတွက် သုံးတဲ့ tool တစ်ခုပါ။ အော်ရဂျင်နယ် code က [Franz Och](https://en.wikipedia.org/wiki/Franz_Josef_Och) က ၁၉၉၀လောက်မှာ ရေးခဲ့ပြီးတော့ NLP လောကမှာ မသိတဲ့သူမရှိလောက်အောင်ကို နာမည်ကြီးတဲ့ tool တစ်ခု ဖြစ်ပါတယ်။ Bigram contextual similarity ကို အခြေခံထားပြီး လက်ရှိ ဗားရှင်းက အခုနောက်ပိုင်းသုံးတဲ့ C++ compiler နဲ့ run လို့ရအောင် ပြင်ထားတဲ့ ဗားရှင်းဖြစ်ပါတယ်။ Algorithm နဲ့ ပတ်သက်ပြီးအသေးစိတ် လေ့လာချင်တဲ့ သူတွေက [The StatMT Blog](http://statmt.blogspot.com/2014/07/understanding-mkcls.html), [paper](https://www.aclweb.org/anthology/E99-1010/) တို့ကို ဖတ်ရှုလေ့လာပါ။   

## git clone

```
(base) ye@ykt-pro:~/tool$ git clone https://github.com/clab/mkcls
Cloning into 'mkcls'...
remote: Enumerating objects: 88, done.
remote: Counting objects: 100% (88/88), done.
remote: Compressing objects: 100% (53/53), done.
remote: Total 88 (delta 33), reused 88 (delta 33), pack-reused 0
Unpacking objects: 100% (88/88), done.
(base) ye@ykt-pro:~/tool$ cd mkcls/
(base) ye@ykt-pro:~/tool/mkcls$ ls
corpus-stats.pl  LICENSE  Makefile  README.md  run-mkcls.pl  src
```

## make

```
(base) ye@ykt-pro:~/tool/mkcls$ make
make -C src
make[1]: Entering directory '/home/ye/tool/mkcls/src'
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c GDAOptimization.cc -o GDAOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c HCOptimization.cc -o HCOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c Problem.cc -o Problem.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c IterOptimization.cc -o IterOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c ProblemTest.cc -o ProblemTest.o
ProblemTest.cc: In function ‘void multiSolveProblem(Problem&, int, int)’:
ProblemTest.cc:203:7: warning: variable ‘maxLaeufe’ set but not used [-Wunused-but-set-variable]
  203 |   int maxLaeufe;
      |       ^~~~~~~~~
ProblemTest.cc:225:13: warning: array subscript 6 is above array bounds of ‘StatVar [5]’ [-Warray-bounds]
  225 |   end[MY_OPT].title =   "  MY";
      |   ~~~~~~~~~~^
ProblemTest.cc:205:11: note: while referencing ‘end’
  205 |   StatVar end[MAX_OPT_NR],auswertungen[MAX_OPT_NR],start[MAX_OPT_NR];
      |           ^~~
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c RRTOptimization.cc -o RRTOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c MYOptimization.cc -o MYOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c SAOptimization.cc -o SAOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c TAOptimization.cc -o TAOptimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c Optimization.cc -o Optimization.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemTest.cc -o KategProblemTest.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemKBC.cc -o KategProblemKBC.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemWBC.cc -o KategProblemWBC.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblem.cc -o KategProblem.o
KategProblem.cc: In member function ‘virtual int KategProblem::_change(ProblemChange**)’:
KategProblem.cc:484:10: warning: this statement may fall through [-Wimplicit-fallthrough=]
  484 |       kat=randomInt(katFreq.nKats-2)+2;
      |       ~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~
KategProblem.cc:486:5: note: here
  486 |     case K_DET:
      |     ^~~~
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c StatVar.cc -o StatVar.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c general.cc -o general.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -c mkcls.cc -o mkcls.o
/usr/local/bin/ccache-gxx -std=c++11 -Wall -W -DNDEBUG -O3 -funroll-loops -o mkcls GDAOptimization.o HCOptimization.o Problem.o IterOptimization.o ProblemTest.o RRTOptimization.o MYOptimization.o SAOptimization.o TAOptimization.o Optimization.o KategProblemTest.o KategProblemKBC.o KategProblemWBC.o KategProblem.o StatVar.o general.o mkcls.o 
make[1]: Leaving directory '/home/ye/tool/mkcls/src'
(base) ye@ykt-pro:~/tool/mkcls$
```

## check --help

```
(base) ye@ykt-pro:~/tool/mkcls$ perl ./run-mkcls.pl --help
Usage: ./run-mkcls.pl --text file.txt [--c NUM_CLASSES] [--alg {TA,OPT,ISR}] [--n N] > output.txt

 * If --c is unspecified sqrt(|V|) will be used.

 * --alg determines the algorithm. OPT is default.
   ISR is the best, but slow, OPT is second best, TA is fastest.

 * OPT and ISR run depend on --n to control the number of restarts.
   n=2 is default, larger n get much slower

(base) ye@ykt-pro:~/tool/mkcls$ 
```

## Prepare data

```
(base) ye@ykt-pro:~/tool/mkcls$ mkdir y-test
(base) ye@ykt-pro:~/tool/mkcls$ cd y-test/

(base) ye@ykt-pro:~/tool/mkcls/y-test$ cp /media/ye/project1/exp/wfst-mt/exp/word/wfst-mt/my-rk/all.my .
(base) ye@ykt-pro:~/tool/mkcls/y-test$ cp /media/ye/project1/exp/wfst-mt/exp/word/wfst-mt/my-rk/all.rk .

(base) ye@ykt-pro:~/tool/mkcls/y-test$ wc all.{my,rk}
  395916  1377429 24142452 all.my
  395916  1358773 23724976 all.rk
  791832  2736202 47867428 total
(base) ye@ykt-pro:~/tool/mkcls/y-test$ 
```

တကယ်က ဒီ all.my, all.rk ဖိုင်က စာကြောင်းဆိုတာထက် alignment လုပ်ထားတဲ့ output တွေဖြစ်တာကြောင့် ပုံမှန် စာကြောင်းနဲ့တော့ ကွက်တိတူတာမဟုတ်ဘူး။

## Make class for all.my

```
(base) ye@ykt-pro:~/tool/mkcls$ time perl ./run-mkcls.pl --text ./y-test/all.my > all.my.class
Reading corpus from ./y-test/all.my ...
|V| = 14168
sqrt(|V|) = 120
c = 120
Running: /home/ye/tool/mkcls/src/mkcls -c120 -n2 -p./y-test/all.my -VtempxfbwZ.txt OPT

***** 2 runs. (algorithm:TA)*****
;KategProblem:cats: 120   words: 14169

start-costs: MEAN: 2.48518e+07 (2.48407e+07-2.48629e+07)  SIGMA:11092.6   
  end-costs: MEAN: 2.33268e+07 (2.33188e+07-2.33349e+07)  SIGMA:8063.91   
   start-pp: MEAN: 286.9 (285.105-288.694)  SIGMA:1.79458   
     end-pp: MEAN: 121.412 (120.86-121.965)  SIGMA:0.552094   
 iterations: MEAN: 348683 (333506-363860)  SIGMA:15177   
       time: MEAN: 20.0251 (19.1209-20.9293)  SIGMA:0.904203   

mkcls succeeded.
Cluster C1 has 55 type(s)
Cluster C2 has 72 type(s)
Cluster C3 has 53 type(s)
Cluster C4 has 175 type(s)
Cluster C5 has 286 type(s)
Cluster C6 has 81 type(s)
Cluster C7 has 74 type(s)
Cluster C8 has 246 type(s)
Cluster C9 has 129 type(s)
Cluster C10 has 69 type(s)
Cluster C11 has 120 type(s)
Cluster C12 has 83 type(s)
Cluster C13 has 116 type(s)
Cluster C14 has 543 type(s)
Cluster C15 has 71 type(s)
Cluster C16 has 153 type(s)
Cluster C17 has 80 type(s)
Cluster C18 has 143 type(s)
Cluster C19 has 127 type(s)
Cluster C20 has 209 type(s)
Cluster C21 has 84 type(s)
Cluster C22 has 77 type(s)
Cluster C23 has 117 type(s)
Cluster C24 has 127 type(s)
Cluster C25 has 124 type(s)
Cluster C26 has 185 type(s)
Cluster C27 has 121 type(s)
Cluster C28 has 278 type(s)
Cluster C29 has 295 type(s)
Cluster C30 has 102 type(s)
Cluster C31 has 235 type(s)
Cluster C32 has 54 type(s)
Cluster C33 has 131 type(s)
Cluster C34 has 164 type(s)
Cluster C35 has 116 type(s)
Cluster C36 has 112 type(s)
Cluster C37 has 165 type(s)
Cluster C38 has 237 type(s)
Cluster C39 has 121 type(s)
Cluster C40 has 88 type(s)
Cluster C41 has 153 type(s)
Cluster C42 has 123 type(s)
Cluster C43 has 99 type(s)
Cluster C44 has 133 type(s)
Cluster C45 has 101 type(s)
Cluster C46 has 70 type(s)
Cluster C47 has 76 type(s)
Cluster C48 has 52 type(s)
Cluster C49 has 105 type(s)
Cluster C50 has 75 type(s)
Cluster C51 has 31 type(s)
Cluster C52 has 123 type(s)
Cluster C53 has 76 type(s)
Cluster C54 has 97 type(s)
Cluster C55 has 122 type(s)
Cluster C56 has 42 type(s)
Cluster C57 has 104 type(s)
Cluster C58 has 51 type(s)
Cluster C59 has 232 type(s)
Cluster C60 has 97 type(s)
Cluster C61 has 75 type(s)
Cluster C62 has 59 type(s)
Cluster C63 has 302 type(s)
Cluster C64 has 140 type(s)
Cluster C65 has 10 type(s)
Cluster C66 has 60 type(s)
Cluster C67 has 118 type(s)
Cluster C68 has 87 type(s)
Cluster C69 has 110 type(s)
Cluster C70 has 159 type(s)
Cluster C71 has 121 type(s)
Cluster C72 has 81 type(s)
Cluster C73 has 84 type(s)
Cluster C74 has 76 type(s)
Cluster C75 has 101 type(s)
Cluster C76 has 119 type(s)
Cluster C77 has 43 type(s)
Cluster C78 has 105 type(s)
Cluster C79 has 89 type(s)
Cluster C80 has 95 type(s)
Cluster C81 has 166 type(s)
Cluster C82 has 119 type(s)
Cluster C83 has 55 type(s)
Cluster C84 has 64 type(s)
Cluster C85 has 175 type(s)
Cluster C86 has 119 type(s)
Cluster C87 has 138 type(s)
Cluster C88 has 111 type(s)
Cluster C89 has 101 type(s)
Cluster C90 has 100 type(s)
Cluster C91 has 97 type(s)
Cluster C92 has 159 type(s)
Cluster C93 has 218 type(s)
Cluster C94 has 62 type(s)
Cluster C95 has 91 type(s)
Cluster C96 has 46 type(s)
Cluster C97 has 126 type(s)
Cluster C98 has 101 type(s)
Cluster C99 has 137 type(s)
Cluster C100 has 48 type(s)
Cluster C101 has 58 type(s)
Cluster C102 has 54 type(s)
Cluster C103 has 178 type(s)
Cluster C104 has 104 type(s)
Cluster C105 has 100 type(s)
Cluster C106 has 81 type(s)
Cluster C107 has 113 type(s)
Cluster C108 has 69 type(s)
Cluster C109 has 59 type(s)
Cluster C110 has 161 type(s)
Cluster C111 has 153 type(s)
Cluster C112 has 123 type(s)
Cluster C113 has 144 type(s)
Cluster C114 has 132 type(s)
Cluster C115 has 32 type(s)
Cluster C116 has 149 type(s)
Cluster C117 has 107 type(s)
Cluster C118 has 79 type(s)
Cluster C119 has 123 type(s)
Cluster C120 has 102 type(s)
Done.

real	0m42.880s
user	0m42.673s
sys	0m0.157s
(base) ye@ykt-pro:~/tool/mkcls$ 

(base) ye@ykt-pro:~/tool/mkcls$ head all.my.class 
C1	နိုင်	1590
C1	သေး	1518
C1	ခဲ့	879
C1	စေချင်	223
C1	မိ	173
C1	နေမှာ	127
C1	သာ	123
C1	ဖူး	121
C1	နိုင်မယ့်	114
C1	ပေါက်	103

(base) ye@ykt-pro:~/tool/mkcls$ shuf ./all.my.class | head
C78	စကားစု	1
C86	အဖွဲ့ဝင်	50
C95	အသုံးပြု	80
C113	အသက်ရှင်	16
C81	အမှတ်တမဲ့ကြား	27
C57	တွက်ထား	51
C47	ပြေးနေ	2
C49	လုပ်စရာတွေ	57
C40	ဒေါပွနေတဲ့	10
C38	ဦးထုပ်	60

(base) ye@ykt-pro:~/tool/mkcls$ tail ./all.my.class | head
C120	ပြန်ယူလာ	1
C120	အနေနဲ့တော့	1
C120	ဖြတ်သန်းစီးဆင်းနေတာက	1
C120	ပြသခွင့်	1
C120	လွှင့်ပစ်လိုက်	1
C120	ဗျက်ကြီး	1
C120	အကြွေးဆပ်	1
C120	မိသားစုကော	1
C120	ပျံ့	1
C120	အကြံရ	1
(base) ye@ykt-pro:~/tool/mkcls$ 
```

## Preparing for normal sentences

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/data4pbsmt/word/my-rk$ cat train.my dev.my test.my > /home/ye/tool/mkcls/y-test/train-dev-test.my

(base) ye@ykt-pro:~/tool/mkcls/y-test$ wc ./train-dev-test.my 
  18372  127570 2083963 ./train-dev-test.my
(base) ye@ykt-pro:~/tool/mkcls/y-test$ head train-dev-test.my 
မင်း အဲ့ဒါ ကို အခြား တစ်ခုနဲ့ မ ချိတ် ဘူးလား ။
သူမ ဘယ်သူ့ကိုမှ မ မှတ်မိတော့ဘူး ။
အဲ့ဒါ ကျွန်တော် တို့ အတွက် ခက်ခဲ တယ် ။
ခင်ဗျား ပြောခဲ့ သလို ကျွန်တော် ရှင်းပြ ခဲ့တယ် ။
သူ့ကို ထိန်းဖို့ မင်း ပဲ တတ်နိုင်တယ် ။
အဲ့ဒါ ကို ကိုယ် တက်နင်း မိသွား လား ။
ငါ စဉ်းစား သလို စဉ်းစားပါ ။
အတင်းပြော ရတာ မုန်း တယ် ။
နောက်ဆုံး တစ် ကြိမ် သူ့ကို ချစ်ပါတယ် လို့ ပြောခွင့်တောင် မ ရ တော့ဘူး ။
နာဆာ မှ ဒုံးပျံ စတက်တာ နဲ့ သူ မှတ်တမ်း ရေး ခဲ့တယ် ။
(base) ye@ykt-pro:~/tool/mkcls/y-test$ 
```

## make word class with normal Myanmar sentences

```
(base) ye@ykt-pro:~/tool/mkcls$ time perl ./run-mkcls.pl --text ./y-test/train-dev-test.my > ./y-test/train-dev-test.my.class
Reading corpus from ./y-test/train-dev-test.my ...
|V| = 16017
sqrt(|V|) = 127
c = 127
Running: /home/ye/tool/mkcls/src/mkcls -c127 -n2 -p./y-test/train-dev-test.my -Vtempqwv_b.txt OPT

***** 2 runs. (algorithm:TA)*****
;KategProblem:cats: 127   words: 16018

start-costs: MEAN: 1.63762e+06 (1.63515e+06-1.64009e+06)  SIGMA:2474.55   
  end-costs: MEAN: 1.47664e+06 (1.47618e+06-1.4771e+06)  SIGMA:459.887   
   start-pp: MEAN: 243.133 (239.011-247.255)  SIGMA:4.12211   
     end-pp: MEAN: 80.6733 (80.4191-80.9275)  SIGMA:0.254214   
 iterations: MEAN: 398244 (373656-422833)  SIGMA:24588.5   
       time: MEAN: 11.7243 (11.1028-12.3458)  SIGMA:0.621486   

mkcls succeeded.
Cluster C1 has 216 type(s)
Cluster C2 has 126 type(s)
Cluster C3 has 83 type(s)
Cluster C4 has 84 type(s)
Cluster C5 has 172 type(s)
Cluster C6 has 96 type(s)
Cluster C7 has 99 type(s)
Cluster C8 has 181 type(s)
Cluster C9 has 104 type(s)
Cluster C10 has 42 type(s)
Cluster C11 has 69 type(s)
Cluster C12 has 164 type(s)
Cluster C13 has 163 type(s)
Cluster C14 has 41 type(s)
Cluster C15 has 147 type(s)
Cluster C16 has 142 type(s)
Cluster C17 has 76 type(s)
Cluster C18 has 89 type(s)
Cluster C19 has 107 type(s)
Cluster C20 has 188 type(s)
Cluster C21 has 115 type(s)
Cluster C22 has 148 type(s)
Cluster C23 has 87 type(s)
Cluster C24 has 194 type(s)
Cluster C25 has 139 type(s)
Cluster C26 has 110 type(s)
Cluster C27 has 48 type(s)
Cluster C28 has 100 type(s)
Cluster C29 has 64 type(s)
Cluster C30 has 100 type(s)
Cluster C31 has 208 type(s)
Cluster C32 has 99 type(s)
Cluster C33 has 80 type(s)
Cluster C34 has 112 type(s)
Cluster C35 has 198 type(s)
Cluster C36 has 65 type(s)
Cluster C37 has 133 type(s)
Cluster C38 has 163 type(s)
Cluster C39 has 82 type(s)
Cluster C40 has 96 type(s)
Cluster C41 has 165 type(s)
Cluster C42 has 142 type(s)
Cluster C43 has 125 type(s)
Cluster C44 has 92 type(s)
Cluster C45 has 124 type(s)
Cluster C46 has 92 type(s)
Cluster C47 has 188 type(s)
Cluster C48 has 74 type(s)
Cluster C49 has 142 type(s)
Cluster C50 has 121 type(s)
Cluster C51 has 146 type(s)
Cluster C52 has 132 type(s)
Cluster C53 has 136 type(s)
Cluster C54 has 253 type(s)
Cluster C55 has 77 type(s)
Cluster C56 has 42 type(s)
Cluster C57 has 62 type(s)
Cluster C58 has 142 type(s)
Cluster C59 has 137 type(s)
Cluster C60 has 75 type(s)
Cluster C61 has 129 type(s)
Cluster C62 has 109 type(s)
Cluster C63 has 154 type(s)
Cluster C64 has 141 type(s)
Cluster C65 has 155 type(s)
Cluster C66 has 77 type(s)
Cluster C67 has 103 type(s)
Cluster C68 has 95 type(s)
Cluster C69 has 74 type(s)
Cluster C70 has 98 type(s)
Cluster C71 has 335 type(s)
Cluster C72 has 99 type(s)
Cluster C73 has 38 type(s)
Cluster C74 has 171 type(s)
Cluster C75 has 110 type(s)
Cluster C76 has 143 type(s)
Cluster C77 has 178 type(s)
Cluster C78 has 109 type(s)
Cluster C79 has 158 type(s)
Cluster C80 has 84 type(s)
Cluster C81 has 125 type(s)
Cluster C82 has 159 type(s)
Cluster C83 has 216 type(s)
Cluster C84 has 72 type(s)
Cluster C85 has 44 type(s)
Cluster C86 has 147 type(s)
Cluster C87 has 157 type(s)
Cluster C88 has 228 type(s)
Cluster C89 has 93 type(s)
Cluster C90 has 385 type(s)
Cluster C91 has 51 type(s)
Cluster C92 has 224 type(s)
Cluster C93 has 140 type(s)
Cluster C94 has 90 type(s)
Cluster C95 has 99 type(s)
Cluster C96 has 99 type(s)
Cluster C97 has 138 type(s)
Cluster C98 has 100 type(s)
Cluster C99 has 67 type(s)
Cluster C100 has 142 type(s)
Cluster C101 has 92 type(s)
Cluster C102 has 137 type(s)
Cluster C103 has 108 type(s)
Cluster C104 has 117 type(s)
Cluster C105 has 129 type(s)
Cluster C106 has 116 type(s)
Cluster C107 has 146 type(s)
Cluster C108 has 50 type(s)
Cluster C109 has 12 type(s)
Cluster C110 has 206 type(s)
Cluster C111 has 110 type(s)
Cluster C112 has 123 type(s)
Cluster C113 has 144 type(s)
Cluster C114 has 154 type(s)
Cluster C115 has 61 type(s)
Cluster C116 has 43 type(s)
Cluster C117 has 145 type(s)
Cluster C118 has 194 type(s)
Cluster C119 has 46 type(s)
Cluster C120 has 144 type(s)
Cluster C121 has 182 type(s)
Cluster C122 has 259 type(s)
Cluster C123 has 77 type(s)
Cluster C124 has 173 type(s)
Cluster C125 has 101 type(s)
Cluster C126 has 315 type(s)
Cluster C127 has 100 type(s)
Done.

real	0m24.006s
user	0m23.979s
sys	0m0.024s
(base) ye@ykt-pro:~/tool/mkcls$ 

(base) ye@ykt-pro:~/tool/mkcls/y-test$ head ./train-dev-test.my.class 
C1	မေးခွန်း	30
C1	မိဘ	29
C1	သင်ခန်းစာ	29
C1	အဝတ်အစား	25
C1	လုပ်စရာ	14
C1	ပန်းကန်	12
C1	ခြေထောက်	11
C1	ကြက်ဥ	10
C1	မြင်း	10
C1	တံဆိပ်ခေါင်း	7
(base) ye@ykt-pro:~/tool/mkcls/y-test$ shuf ./train-dev-test.my.class | head
C81	အမြတ်	3
C40	မျက်ကပ်	2
C86	ပိုကြာခဲ့	1
C64	ရမှာပေါ့။	1
C58	ရောက်ပြီး	1
C107	ပေးနိုင်ပါတယ်	1
C1	သက်ကြီးရွယ်အို	1
C42	အားနာပါ	1
C73	ကောင်လေး	14
C6	အိုက်စကရင်	1
(base) ye@ykt-pro:~/tool/mkcls/y-test$ tail ./train-dev-test.my.class 
C127	လာရောက်	1
C127	ရပ်ဆိုင်း	1
C127	ရောက်လေ့ရှိ	1
C127	၁၉၁၇	1
C127	အကျွမ်းဝင်	1
C127	တပ်ဆင်ထား	1
C127	စိုက်ထား	1
C127	တီးပြ	1
C127	လွမ်းရ	1
C127	မဖြစ်မနေသွား	1
(base) ye@ykt-pro:~/tool/mkcls/y-test$
```
