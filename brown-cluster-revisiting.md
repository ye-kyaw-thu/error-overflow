# Brown Cluster Revisiting

## git clone

```
(base) ye@lst-gpu-server-197:~/ye/exp$ git clone https://github.com/redpony/brown-cluster
Cloning into 'brown-cluster'...
remote: Enumerating objects: 98, done.
remote: Total 98 (delta 0), reused 0 (delta 0), pack-reused 98
Receiving objects: 100% (98/98), 50.55 KiB | 958.00 KiB/s, done.
Resolving deltas: 100% (28/28), done.
```

```
(base) ye@lst-gpu-server-197:~/ye/exp$ cd brown-cluster/
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ ls
basic  cluster-viewer  input.txt  Makefile  output.txt  README  wcluster.cc
```

## make

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ make
g++ -Wall -g -O3 -o basic/logging.o -c basic/logging.cc
g++ -Wall -g -O3 -o wcluster.o -c wcluster.cc
wcluster.cc: In function ‘void compute_cluster_distribs()’:
wcluster.cc:830:10: warning: variable ‘kl’ set but not used [-Wunused-but-set-variable]
  830 |     real kl;
      |          ^~
g++ -Wall -g -O3 -o basic/city.o -c basic/city.cc
g++ -Wall -g -O3 -o basic/indent.o -c basic/indent.cc
g++ -Wall -g -O3 -o basic/lisp.o -c basic/lisp.cc
g++ -Wall -g -O3 -o basic/mem-tracker.o -c basic/mem-tracker.cc
g++ -Wall -g -O3 -o basic/multi-ostream.o -c basic/multi-ostream.cc
g++ -Wall -g -O3 -o basic/opt.o -c basic/opt.cc
g++ -Wall -g -O3 -o basic/prob-utils.o -c basic/prob-utils.cc
g++ -Wall -g -O3 -o basic/stats.o -c basic/stats.cc
g++ -Wall -g -O3 -o basic/std.o -c basic/std.cc
g++ -Wall -g -O3 -o basic/stl-basic.o -c basic/stl-basic.cc
g++ -Wall -g -O3 -o basic/stl-utils.o -c basic/stl-utils.cc
g++ -Wall -g -O3 -o basic/str.o -c basic/str.cc
g++ -Wall -g -O3 -o basic/strdb.o -c basic/strdb.cc
g++ -Wall -g -O3 -o basic/str-str-db.o -c basic/str-str-db.cc
g++ -Wall -g -O3 -o basic/timer.o -c basic/timer.cc
g++ -Wall -g -O3 -o basic/union-set.o -c basic/union-set.cc
g++ -Wall -g -O3 -o wcluster basic/logging.o wcluster.o basic/city.o basic/indent.o basic/lisp.o basic/mem-tracker.o basic/multi-ostream.o basic/opt.o basic/prob-utils.o basic/stats.o basic/std.o basic/stl-basic.o basic/stl-utils.o basic/str.o basic/strdb.o basic/str-str-db.o basic/timer.o basic/union-set.o
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Check the program ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ ls
basic           input.txt  output.txt  wcluster     wcluster.o
cluster-viewer  Makefile   README      wcluster.cc
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

## --help

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ ./wcluster
usage: ./wcluster
  chk                 : Check data structures are valid (expensive). [false]
  stats               : Just print out stats. [false]
  paths2map           : Take the paths file and generate a map file. [false]
  ncollocs      <int> : Collocations with most mutual information (output). [500]
  c             <int> : Number of clusters. [1000]
  plen          <int> : Maximum length of a phrase to consider. [1]
  min-occur     <int> : Keep phrases that occur at least this many times. [1]
  rand          <int> : Number to call srand with. [-579121777]
  output_dir    <str> : Output everything to this directory. []
  text          <str> : Text file with corpora (input). []
  restrict      <str> : Only consider words that appear in this text (input). []
  paths         <str> : File containing root-to-node paths in the clustering tree (input/output). []
  map           <str> : File containing lots of good information about each phrase, more general than paths (output) []
  collocs       <str> : Collocations with most mutual information (output). []
  featvec       <str> : Feature vectors (output). []
  comment       <str> : Description of this run. []
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

## Test Run

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ time ./wcluster --text input.txt --c 50
Logging to input-c50-p1.out/log

real    0m0.027s
user    0m0.007s
sys     0m0.001s
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ ls ./input-c50-p1.out/
collocs  log  map  paths
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$ cat ./collocs
0.304599        chased  the
0.203066        the     cat
0.203066        the     mouse
0.203066        the     dog
0.101533        cat     chased
0.101533        mouse   chased
0.101533        dog     chased
0.0301046       cat     the
0.0301046       mouse   the
0       the     the
0       the     chased
0       cat     cat
0       cat     mouse
0       cat     dog
0       chased  cat
0       chased  chased
0       chased  mouse
0       chased  dog
0       mouse   cat
0       mouse   mouse
0       mouse   dog
0       dog     the
0       dog     cat
0       dog     mouse
0       dog     dog
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$
```

Check the log file:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$ cat log
main: ./wcluster --text input.txt --c 50 {
  Sun Apr 14 00:56:50 2024 on lst-gpu-server-197 (1200MHz)
  read_text() {
    read_text(): input.txt {
      Reading from input.txt [0s, cumulative 0s]
      StrDB::write(): input.txt.strdb [0s, cumulative 0s]
    } [0s, cumulative 0s]
    Counting phrases {
      5 distinct phrases of length 1, keeping 5 which occur at least 1 times
    } [0s, cumulative 0s]
    Finding left/right phrases [0s, cumulative 0s]
    Text length: 15, 5 phrases, 5 words
  } [0s, cumulative 0.02s]
  create_initial_clusters() {
    Sorting 5 phrases by frequency
    Selecting top 5 phrases to be initial clusters
  } [0s, cumulative 0.02s]
  Writing to input-c50-p1.out/collocs
  do_clustering() {
    compute_L2() {
      Computing L2 [0s, cumulative 0s]
    } [0s, cumulative 0s]
    Stage 1 {
      report_mem_usage() [0s, cumulative 0s]
    } [0s, cumulative 0s]
    compute_cluster_distribs() [0s, cumulative 0s]
    Stage 2 {
      report_mem_usage() [0s, cumulative 0s]
      Clustering: 0/4 [0s, cumulative 0s]
      Clustering: 1/4 [0s, cumulative 0s]
      Clustering: 2/4 [0s, cumulative 0s]
      Clustering: 3/4 [0s, cumulative 0s]
    } [0s, cumulative 0s]
    Done: 1 cluster left: mutual info = 4.996e-16
    report_mem_usage() {
      DoubleVecVec p2: 560 (0.211401)
      DoubleVecVec q2: 560 (0.211401)
      DoubleVecVec L2: 560 (0.211401)
      IntMat left_phrases: 176 (0.0664402)
      IntMat right_phrases: 176 (0.0664402)
      IntIntPairMap cluster_tree: 132 (0.0498301)
      StrDB db: 69 (0.0260476)
      IntIntMap rep2cluster: 68 (0.0256701)
      IntIntMap cluster2rep: 68 (0.0256701)
      IntIntMap cluster2slot: 68 (0.0256701)
      IntMat phrases: 68 (0.0256701)
      DoubleVec p1: 56 (0.0211401)
      IntVec slot2cluster: 28 (0.01057)
      IntVec phrase_freqs: 20 (0.00755002)
      IntVec freq_order_phrases: 20 (0.00755002)
      UnionSet phrase2rep: 20 (0.00755002)
      Total: 2K
    } [0s, cumulative 0s]
  } [0s, cumulative 0.02s]
  Writing cluster paths to input-c50-p1.out/paths
  Writing cluster map to input-c50-p1.out/map
} [0.02s]
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$
```

Check the map file:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$ cat map
the     0-L 0.788457    0-R 0.606136    0-freq 6
chased  10-L 0.693147   10-R 0.693147   10-freq 3
dog     110-L 0.405465  110-R 1.09861   110-freq 2
mouse   1110-L 0.693147 1110-R 0.693147 1110-freq 2
cat     1111-L 0.693147 1111-R 0.693147 1111-freq 2
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$
```

Check the path file:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$ cat paths
0       the     6
10      chased  3
110     dog     2
1110    mouse   2
1111    cat     2
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/input-c50-p1.out$
```

## Testing with Myanmar Corpus  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ wc ./myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned
  358046  6931666 93483055 ./myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ head myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned
ကြိုးစား နေ ပါ တယ်
အားလုံး ညှစ် တယ်
လယ်ယာ လုပ်ငန်း ကို အဓိက လုပ်ကိုင် ပြီး မြန်မာ့ ဓလေ့ ဝါးဓနိ အိမ် များ အများစု စုဖွဲ့ တည်ရှိ နေ သည့် အေး ကျေးရွာ ၏ အဓိက ရေ အရင်းအမြစ် အဖြစ် စပါး ရေသွင်း စိုက်ပျိုး ရန် အတွက် နိုင်ငံတော် အစိုးရ က တူးမြောင်း တစ် ခု ဆောက်လုပ် ကာ ဧရာဝတီ မြစ် မှ ရေ ကို သွယ်ယူ ပေး ထား ပြီး ကျေးရွာလူထု သောက်သုံး ရန် ချက်ပြုတ် ရာ တွင် အသုံးပြု ရန် အတွက် မူ အဝီစိရေ သွယ်ယူ သည့် ပိုက် တစ် ခု သာ လျှင် ရှိ ပါ သည်
သူ ဟာ ဘေးဘျမ်း ကင်းကင်း နဲ့ ပြန်ရောက် လာ ခဲ့ တယ် လေ
အခု ချိန် မှာ ထိုင်ဝမ် က နေ ဗြိတိန် ကို တိုက်ရိုက် လေယာဉ် မ ရှိ ဘူး ခင်ဗျား ဟောင်ကောင် က နေ တဆင့် သွား ရ မယ်
သူ့ ဘာသာ သူ ပြော ချင် ရာ ပြော ပြီး သူ့ ဘက် အဖော် လှည့် ညှိ သေး ၏
အန်ကယ် မနက် စောစော ထ ပြီး ပုံမှန် လမ်းလျှောက် ပေး ပါ လား
ဒီလို လေး ပဲ အမြဲ ထာဝရ မြင် ချင် ပါ တယ် ခန့်စည်သူ ကို မ တွေ့ မိ ပါ လား နိုင်ငံတော် ကို ဖား အဲ လေ နိုင်ငံတော် အကျိုးပြု ဇာတ်ကား တွေ ရိုက် နေ ကျ အနုပညာရှင် တွေ က ရှေ့ ဆုံး တန်း မှာ ကွ
ကျွန်တော့် ကို ပိုက်ဆံ နည်းနည်း ချေး မလား
သူ က လူရင်း ပါ
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Running ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ time ./wcluster --text ./myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned --c 100 --min-occur 3 --output_dir
 my_c100_min3
Logging to my_c100_min3/log

real    1m15.046s
user    1m14.530s
sys     0m0.493s
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Check the output folder:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ wc ./my_c100_min3/*
    500    1500   16111 ./my_c100_min3/collocs
  36700  256565 3513105 ./my_c100_min3/log
  36648  256536 2808773 ./my_c100_min3/map
  36648  109944 1321436 ./my_c100_min3/paths
 110496  624545 7659425 total
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Check the collocs file:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$ head -n 50 ./collocs
0.0289299       ပါ      တယ်
0.00947498      မ       ဟုတ်
0.00799242      တစ်     ခု
0.00748023      က       ကျွန်တော်
0.00744308      တစ်     ယောက်
0.00697772      မ       ရှိ
0.0065595       သူ      တို့
0.00569782      ဆို     တာ
0.0056859       နေ      တာ
0.00567081      ကျွန်တော်       တို့
0.00547053      အားပေး  နေ
0.00524878      လိုက်   တာ
0.00476417      ပါ      ဘူး
0.00456984      တွေ     ကို
0.00436566      ဆို     ရင်
0.00416269      မ       သိ
0.00383724      များ    ကို
0.00368334      က       တော့
0.00359578      ထဲ      မှာ
0.00344965      ပေး     ပါ
0.00339323      ရ       တာ
0.00328943      တာ      လဲ
0.00310866      ဟုတ်    ဘူး
0.00307491      နေ      ကြ
0.00306911      နှစ်    ယောက်
0.00305758      တာ      ပဲ
0.00295125      လေ      သည်
0.00294785      တွေ     က
0.00293699      ခဲ့     သည်
0.00291504      မြန်မာ  နိုင်ငံ
0.00285382      ဖြစ်    သည်
0.00284852      မ       အိမ်
0.00281149      က       လည်း
0.00273864      နေ      တယ်
0.00273847      ဘူး     လား
0.00266265      ကြ      သည်
0.00254687      မှ      မ
0.00249274      တယ်     နော်
0.00229208      ချစ်    စရာ
0.00227625      တာ      ပေါ့
0.00217967      နေ      ပြီ
0.00214917      ဖြစ်    ပါ
0.00214613      အရမ်း   ချစ်
0.00211095      လာ      ခဲ့
0.00210947      ကြ      ပါ
0.00205294      ရ       ပါ
0.00202553      လူ      တွေ
0.00201797      ချစ်    တယ်
0.00199815      ဘာ      မှ
0.00198328      ရ       မယ်
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$
```

ဖိုင်ရဲ့ နောက်ဆုံးပိုင်းကိုလည်း ကြည့်ဖြစ်ခဲ့ ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$ tail -n 50 ./col
locs
0.000261415     လည်း    ဖြစ်
0.000259945     ခု      လို
0.000256836     မင်း    ဘာ
0.000256081     တွေ     ထဲ
0.000255756     လုပ်    ဖို့
0.000255333     မှု     ရှိ
0.00025401      လာ      တော့
0.000252792     ကြီး    ကို
0.000252476     ခု      မှ
0.000252187     အားပေး  မယ်
0.000252081     နေ      တတ်
0.000251006     ယောက်   က
0.000250848     လုပ်    ခဲ့
0.000250203     မ       လှ
0.000248064     ပါ      သေး
0.000246863     များ    အတွက်
0.000246377     ပေး     ကြ
0.000245794     ချင်    တဲ့
0.00024483      တတ်     သော
0.000244487     မ       လာ
0.000243032     တွေ     လုပ်
0.000241988     နေ      လေ
0.00024083      ယောက်   ကို
0.000240443     ပြော    လေ
0.000239951     နိုင်   သေး
0.000238761     ပြော    ကြ
0.000238253     ကို     အားပေး
0.000237999     ကြ      ၏
0.000237178     ရ       လေ
0.000236505     မ       ကြည့်
0.000235879     ခြင်း   ကို
0.000234539     အိမ်    က
0.000233577     လိုက်   ပြီး
0.000233521     နော်    အားပေး
0.000232344     နိုင်   တော့
0.000231563     လာ      ရင်
0.000229885     ထဲ      ရောက်
0.000229823     လာ      လေ
0.000229798     တို့    မြန်မာ
0.000229757     နိုင်   တယ်
0.000229034     ကြီး    က
0.000228911     ရှိ     လား
0.00022775      လှ      လိုက်
0.000227108     စေ      ဖို့
0.000226804     မ       ရောက်
0.000224836     ပြော    ခဲ့
0.000224646     ထား     ခြင်း
0.000223784     ကောင်း  သော
0.00022351      ဘူး     လေ
0.000223294     မည်     ဆို
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$
```

log ဖိုင်ကိုလည်း ဝင်လေ့လာခဲ့...  

```
      Merging phrase: 36272/36648: 25309(ကန်ထုတ်) [0.001s, cumulative 1m7.561s]
      Merging phrase: 36273/36648: 25311(အလုပ်ကြီးအကိုင်ကြီး) [0.002s, cumulative 1m7.563s]
      Merging phrase: 36274/36648: 25645(ထျန်အန်မင်း) [0.002s, cumulative 1m7.565s]
      Merging phrase: 36275/36648: 25574(မီယာမီ) [0.002s, cumulative 1m7.567s]
      Merging phrase: 36276/36648: 25585(ဦးသိန်းဟန်) [0.002s, cumulative 1m7.569s]
      Merging phrase: 36277/36648: 25593(ဝထ္ထု) [0.001s, cumulative 1m7.57s]
      Merging phrase: 36278/36648: 25596(ချင်မနီ) [0.002s, cumulative 1m7.572s]
      Merging phrase: 36279/36648: 25603(အနင်းခံ) [0.002s, cumulative 1m7.574s]
      Merging phrase: 36280/36648: 25605(ဟုတ်ပ) [0.002s, cumulative 1m7.576s]
      Merging phrase: 36281/36648: 25607(ရံပုံငွေ) [0.001s, cumulative 1m7.577s]
      Merging phrase: 36282/36648: 25608(ရုပ်လုံးဖော်) [0.002s, cumulative 1m7.579s]
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$ head map
ဟောက်ရှင်းကျင်  0000-L 3.30906  0000-R 3.30035  0000-freq 3
အောင်နိုင်ဝင်း  0000-L 4.38827  0000-R 3.10925  0000-freq 3
ဟောင်ဟောင်      0000-L 3.62539  0000-R 2.47724  0000-freq 3
အဟေဟေး  0000-L 3.76027  0000-R 3.99303  0000-freq 3
သမိတိံဝနံ       0000-L 2.99383  0000-R 3.45398  0000-freq 3
ကကျွတ်ကကျွတ်ကကျွတ်      0000-L 3.6311   0000-R 3.4652   0000-freq 3
မောင်ဝိတ်       0000-L 2.14675  0000-R 2.74189  0000-freq 3
အေးပေါ့ 0000-L 3.26062  0000-R 3.37363  0000-freq 3
ဂွတ်ည   0000-L 2.76033  0000-R 4.42842  0000-freq 3
ကိုတူး  0000-L 4.20287  0000-R 3.35362  0000-freq 3
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$ head paths
0000    ဟောက်ရှင်းကျင်  3
0000    အောင်နိုင်ဝင်း  3
0000    ဟောင်ဟောင်      3
0000    အဟေဟေး  3
0000    သမိတိံဝနံ       3
0000    ကကျွတ်ကကျွတ်ကကျွတ်      3
0000    မောင်ဝိတ်       3
0000    အေးပေါ့ 3
0000    ဂွတ်ည   3
0000    ကိုတူး  3
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$ tail paths
111111  ကံကောင်း        1144
111111  ပြေ     1242
111111  ချမ်းသာ 1537
111111  မြန်    1936
111111  ရှည်    1977
111111  တိုးတက် 2041
111111  ပျော်ရွှင်      2838
111111  ကျန်းမာ 4293
111111  အောင်မြင်       5201
111111  ကြိုးစား        5100
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster/my_c100_min3$
```

## Making HTML File

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ time ./cluster-viewer/build-viewer.sh ./my_c100_min3/paths
Creating output in clusters ...
  File "./cluster-viewer/code/make_html.py", line 14
    wordcounts.sort(key=lambda (w,c): -c)
                               ^
SyntaxError: invalid syntax

real    0m0.037s
user    0m0.026s
sys     0m0.013s
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Debugging as follows:

```python
def get_cluster_rows():
    for path, rows in itertools.groupby(get_word_rows(), key=lambda x: x[0]):
        wordcounts = [(w,c) for _,w,c in rows]
        #wordcounts.sort(key=lambda (w,c): -c)
        wordcounts.sort(key=lambda wc: -wc[1])
```

## Try Again

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ time ./cluster-viewer/build-viewer.sh ./my_c100_min3/paths my_c100_min3_clusters
Creating output in my_c100_min3_clusters ...
  File "./cluster-viewer/code/make_html.py", line 46
    print """
    <tr>
    <td class=path>^<a target=_blank href="paths/{path}.html">{path}</a> <span class=count>({nwords})</span>
    <td class=words>{wc}
    """.format(path=path, nwords=nwords, wc=wc1)
          ^
SyntaxError: invalid syntax

real    0m0.038s
user    0m0.035s
sys     0m0.005s
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

Updated the code as follows:  

```
    #print """
    #<tr>
    #<td class=path>^<a target=_blank href="paths/{path}.html">{path}</a> <span c>    #<td class=words>{wc}
    #""".format(path=path, nwords=nwords, wc=wc1)

    print("""
    <tr>
    <td class=path>^<a target=_blank href="paths/{path}.html">{path}</a> <span cl>    <td class=words>{wc}
    """.format(path=path, nwords=nwords, wc=wc1))

    print "</tr>"
```

## Try Again  

Got error relating to old print format using and thus ...  
updated into python3 format:  

```
with open(f"{sys.argv[2]}/paths/{path}.html", 'w') as f:
    f.write(f"""<style>{style}</style>\n""")
    f.write("""<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">\n""")
    f.write("""<a href="../cluster_viewer.html">back to cluster viewer</a>\n""")
    f.write(f"""<h1>cluster path {path}</h1>\n""")

    f.write(f"{nwords:,} words, {sum(c for w,c in allwc):,} tokens\n")
    f.write("""<a href='#freq'>freq</a> <a href='#alpha'>alpha</a> <a href='#suffix'>suffix</a>\n""")

    f.write("""<a name=freq><h2>Words in frequency order</h2></a>\n""")
    allwc.sort(key=lambda x: (-x[1], x[0]))
    f.write(wc_table(allwc))

    f.write("""<a name=alpha><h2>Words in alphabetical order</h2></a>\n""")
    allwc.sort(key=lambda x: (x[0], -x[1]))
    f.write(wc_table(allwc))

    f.write("""<a name=suffix><h2>Words in suffix order</h2></a>\n""")
    allwc.sort(key=lambda x: (list(reversed(x[0])), -x[1]))
    f.write(wc_table(allwc, tdword='suffixsort'))
```

## Try Again

```
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$ time ./cluster-viewer/build-viewer.sh ./my_c100_min3/paths my_c100_min3_clusters
Creating output in my_c100_min3_clusters ...
Done. View clusters in my_c100_min3_clusters/cluster_viewer.html

real    0m0.418s
user    0m0.379s
sys     0m0.042s
(base) ye@lst-gpu-server-197:~/ye/exp/brown-cluster$
```

## Learn Brown Word Clusters



## Reference

[https://aclanthology.org/J92-4003.pdf](https://aclanthology.org/J92-4003.pdf)  
