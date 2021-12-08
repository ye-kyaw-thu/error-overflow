# Word Level Lexicon Building Log with NATools

NATools ကို အရင် install လုပ်ထားရလိမ့်မယ်...  
Installation လုပ်ပုံလုပ်နည်းက အောက်ပါ link ကို ကြည့်ပါ။  
[https://github.com/ye-kyaw-thu/error-overflow/blob/master/NATools-installation-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/NATools-installation-log.md)  

## Alignment with NATools

အရင်ဆုံး parallel corpus ကို ပြင်ဆင်ထားရလိမ့်မယ်။  
အရင် word-to-word lexicon ကို ဆောက်တုန်းကလိုပဲ folder တွေကို အောက်ပါအတိုင်း ခွဲထားခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x$ ls
my-bk  my-ch  my-kc  my-ky  my-mo  my-pk  my-po  my-rk  my-rw  my-sh  my-sk  rk-bk  rw-kc
```

nat-create ဆိုတဲ့ command ရဲ့ help screen ကို ခေါ်ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ nat-create --help
nat-create: creates a NATools corpus, and extracts its PTD.

	nat-create [-q] [-langs=L1..L2] [-tokenize] [-ngrams]
	           [-csize=70000]
	           [-noEM] [-ipfp[=5]] [-samplea[=10]] [-sampleb[=10]]
	           [-id=ID] [-i] <corpusL1> <corpusL2>

	nat-create [-q] [-langs=L1..L2] [-tokenize] [-ngrams]
	           [-csize=70000]
	           [-noEM] [-ipfp[=5]] [-samplea[=10]] [-sampleb[=10]]
	           [-id=ID] [-i] -tmx <tmx>

For more help, please run 'perldoc nat-create'
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$
```

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ mkdir phrase
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ cp train* ./phrase/
cp: -r not specified; omitting directory 'train'
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ ls ./phrase/
train.bk  train.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$
```

word-level alignment လုပ်ခိုင်းကြည့်တော့ အောက်ပါအတိုင်း ERROR ပေးတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ time nat-create -langs=my..bk ./train.my ./train.bk
Name for the corpus directory: 
my-bk-phrase
 Source wordlist does not exist. Creating a new one
 Target wordlist does not exist. Creating a new one

 Sentences	Words cp1	Words cp2
 
** WARNING: sentence too big: max(3766,4278)>500
        1	    3766	    4278

**ERROR** No sentences found

ERROR: 512

real	0m6.170s
user	0m0.111s
sys	0m0.020s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ cd my-bk-phrase/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase$ ls
nat.cnf  source.001  target.001
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase$ head -3 *
==> nat.cnf <==
[nat]
noLanguageIdentification=1
source-language=my

==> source.001 <==
တွင်း မ တူး ဘူးလား ။
အမျိုးသား သန့်စင်ခန်း ဘယ် မှာလဲ ။
သူမ ဘေးမှာ ရှိ တဲ့ စာအုပ် ။

==> target.001 <==
တွင်း မ တူး ရလား ။
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။
```

folder, file preparation နဲ့ run တဲ့ ပုံစံကို မသိသေးလို့ ERROR ပေးတာလို့ ယူဆ...  
documentation တွေ ကို ပြန်ဖတ်ကြည့်ခဲ့...  

File format ကြောင့် ပေးတဲ့ ERROR ဆိုတာကို သိခဲ့ရတယ်။  
[https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/view/README](https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/view/README) မှာ ရှင်းပြထားတဲ့အတိုင်းပဲ translation unit တွေ တစ်ခုနဲ့တစ်ခုအကြားမှာ $ ခြားပေးရမယ်။ translation unit တစ်ခုက တစ်လိုင်းထက်မကပိုလည်း ရတယ် ဆိုတဲ့ format.  
ရှင်းပြထားတဲ့ အင်္ဂလိပ်စာ-ပေါ်တူဂီ language pair ဥပမာက အောက်ပါအတိုင်း...  

```
I saw a cat .
$
The cat was 
fat .
$
            
 
        
 
Eu vi um
gato .
$
O gato era gordo .
$
```

အဲဒါကြောင့် အရင်ဆုံး corpus ရဲ့ format ကို အောက်ပါအတိုင်း awk command ကို သုံးပြီးတော့ ပြောင်းခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ awk '{print $0,"\n$"}' ./train.my > corpus.MY
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ awk '{print $0,"\n$"}' ./train.bk > corpus.BK
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ head ./corpus.MY 
တွင်း မ တူး ဘူးလား ။ 
$
အမျိုးသား သန့်စင်ခန်း ဘယ် မှာလဲ ။ 
$
သူမ ဘေးမှာ ရှိ တဲ့ စာအုပ် ။ 
$
သူမ ဘယ်သူ့ ကို နှိပ်စက် ခဲ့သလဲ ။ 
$
သူ မင်းကို ဘာဖြစ်လို့ လက်ထပ်ခဲ့ သလဲ ဆိုတာ မင်း နားလည် လား ၊ နားမလည် ဘူးလား ။ 
$
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ head ./corpus.BK 
တွင်း မ တူး ရလား ။ 
$
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။ 
$
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။ 
$
ဒီမိန်းမ ဖယ်သူ့ ကို နှိပ်စက် ပီးပီလဲ  ။ 
$
သူ မင်း ကို ဘာဖြစ် လက်ထပ် တယ်ဆို နင် နားလည် တယ် မဟုတ်  ။ 
$
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$
```

alignment ပြန်လုပ်ခိုင်းကြည့်တော့ ဒီတစ်ခါတော့ အဆင်ပြေသွားပုံ ရတယ်...  
Note: run တဲ့အခါမှာ folder name ကို ပေးပေးရတယ်။ ကြိုက်တဲ့နာမည်ပေးပါ သို့သော် အဓိပ္ပါယ်ရှိတဲ့ နာမည် ဖြစ်ပြီး space တွေ မပါပါစေနဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ time nat-create -langs=MY..BK ./corpus.MY ./corpus.BK 
Name for the corpus directory: 
my-bk-phrase-lex
 Source wordlist does not exist. Creating a new one
 Target wordlist does not exist. Creating a new one

 Sentences	Words cp1	Words cp2
    10615	   69290	   69784

 Creating index.
 Saving.....
 Creating index.
 Saving.....

Allocating the sparse matrix (9447 x 9608): done 
Memory used:    3534.9 kb

Loading Corpus file 1
Loading Corpus file 2
Loading matrix. This can take a while
EM-algorithm, model A, Iterative Proportional Fitting

Initial matrix total: 65342.51
Initial memory used:    3534.9 kb

Step 1 of the EM-algorithm: done 
Matrix mean difference: 0.294409
Matrix total: 69550.48
Memory used:    3906.5 kb

Step 2 of the EM-algorithm: done 
Matrix mean difference: 0.175125
Matrix total: 69477.53
Memory used:    3906.9 kb

Step 3 of the EM-algorithm: done 
Matrix mean difference: 0.047180
Matrix total: 69424.19
Memory used:    3906.9 kb

Step 4 of the EM-algorithm: done 
Matrix mean difference: 0.018433
Matrix total: 69406.27
Memory used:    3906.9 kb

Step 5 of the EM-algorithm: done 
Matrix mean difference: 0.010511
Matrix total: 69398.00
Memory used:    3906.9 kb


Converting matrix to dictionary: done 


Loading /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/dict.001...
Loading /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/source.001.crp.partials...
Loading /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/target.001.crp.partials...
Loading /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/source.lex...
Loading /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/target.lex...
Writing dictionaries /media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/source-target.001.bin,/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/target-source.001.bin...

Freeing data structures

real	0m16.254s
user	0m0.976s
sys	0m0.129s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ 
```

output ရလာတဲ့ file တွေကို list လုပ်ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ cd my-bk-phrase-lex/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ ls
nat.cnf               source.001.crp.invidx    source-target.001.bin  target.001.crp           target.invidx          target-source.dmp
source.001            source.001.crp.partials  source-target.bin      target.001.crp.index     target.lex
source.001.crp        source.invidx            source-target.dmp      target.001.crp.invidx    target-source.001.bin
source.001.crp.index  source.lex               target.001             target.001.crp.partials  target-source.bin
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

nat.cnf ဖိုင်ကတော့ human readable ဖိုင်ပါ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ cat nat.cnf 
[nat]
csize=70000
nr-chunks=1
target-tokens-count=69784
source-language=MY
source-forms=9447
source-tokens-count=69290
homedir=/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex
target-forms=9608
target-language=BK
name=my-bk-phrase-lex
nr-tus=10622
noLanguageIdentification=1
cfg=/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex/nat.cnf
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

source.001 နဲ့ target.001 ဖိုင်က input ပေးလိုက်တဲ့ parallel corpus ဖိုင်တွေပါပဲ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ head {source,target}.001
==> source.001 <==
တွင်း မ တူး ဘူးလား ။ 
$
အမျိုးသား သန့်စင်ခန်း ဘယ် မှာလဲ ။ 
$
သူမ ဘေးမှာ ရှိ တဲ့ စာအုပ် ။ 
$
သူမ ဘယ်သူ့ ကို နှိပ်စက် ခဲ့သလဲ ။ 
$
သူ မင်းကို ဘာဖြစ်လို့ လက်ထပ်ခဲ့ သလဲ ဆိုတာ မင်း နားလည် လား ၊ နားမလည် ဘူးလား ။ 
$

==> target.001 <==
တွင်း မ တူး ရလား ။ 
$
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။ 
$
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။ 
$
ဒီမိန်းမ ဖယ်သူ့ ကို နှိပ်စက် ပီးပီလဲ  ။ 
$
သူ မင်း ကို ဘာဖြစ် လက်ထပ် တယ်ဆို နင် နားလည် တယ် မဟုတ်  ။ 
$
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

ကျန်တဲ့ ဖိုင်တွေက binary ဖိုင်တွေ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ file *
nat.cnf:                 ASCII text
source.001:              UTF-8 Unicode text
source.001.crp:          data
source.001.crp.index:    data
source.001.crp.invidx:   DOS 2.0 backup id file, sequence 36
source.001.crp.partials: data
source.invidx:           DOS 2.0 backup id file, sequence 36
source.lex:              data
source-target.001.bin:   gzip compressed data, from Unix, original size modulo 2^32 642468
source-target.bin:       gzip compressed data, from Unix, original size modulo 2^32 642468
source-target.dmp:       UTF-8 Unicode text
target.001:              UTF-8 Unicode text
target.001.crp:          data
target.001.crp.index:    data
target.001.crp.invidx:   DOS 2.0 backup id file, sequence 37
target.001.crp.partials: data
target.invidx:           DOS 2.0 backup id file, sequence 37
target.lex:              data
target-source.001.bin:   gzip compressed data, from Unix, original size modulo 2^32 653416
target-source.bin:       gzip compressed data, from Unix, original size modulo 2^32 653416
target-source.dmp:       UTF-8 Unicode text
```

## Building a Dictionary

homepage မှာ ရှင်းပြထားတဲ့ command ကို corpus folder ထဲဝင်ပြီး အောက်ပါအတိုင်း run ပေမဲ့ error ပေးတယ်...  
nat-dumpDicts source.lex source-target.bin target.lex target-source.bin > dict.txt  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ nat-dumpDicts source.lex source-target.bin target.lex target-source.bin > dict.txt
source.lex is not a directory at /usr/local/bin/nat-dumpDicts line 31.
```

command ကို update လုပ်ထားတဲ့ ပုံရှိတယ်။  
အောက်ပါလိုမျိုး "-full" option ဖြည့်ပေးမှ dict.txt ဖိုင်ကို output အဖြစ်ရတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ nat-dumpDicts -full ./source.lex ./source-target.bin ./target.lex ./target-source.bin > dict.txt
```

dictionary ဖိုင်ရဲ့ format က perl မှာသုံးတဲ့ Data::Dumper ဖိုင် format ဖြစ်တာကို တွေ့ရတယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ head -n 30 ./dict.txt 
use utf8;
$DIC1 = {
"(none)" => {
  count => 0,
  trans => {
              "ကို" => 0.11020068,
                "မ" => 0.08753784,
              "ရယ်" => 0.06719629,
                "က" => 0.05875995,
              "ဝို" => 0.04434199,
             "ပြော" => 0.01867740,
              "မှာ" => 0.01786756,
             "လုပ်" => 0.01722777,
    },
},
"တွင်း" => {
  count => 3,
  trans => {
        "ကျရင်လန်း" => 0.43550017,
            "တွင်း" => 0.33681375,
           "စနေနေ့" => 0.22768611,
    },
},
"မ" => {
  count => 1807,
  trans => {
                "မ" => 0.85693467,
           "(none)" => 0.12533303,
    },
},
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

## Testing lex2perl Conversion

ဆောက်ထားတဲ့ lexicon ကနေ perl hash format ကိုပြောင်းတဲ့ ပရိုဂရမ် ဖြစ်တဲ့ nat-lex2perl ကို စမ်းကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ nat-lex2perl ./source.lex > source.lex.lex2perl
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ head -n 30 ./source.lex.lex2perl 
use utf8;
{
	"\(none\)" => 32736,
	"တွင်း" => 3,
	"မ" => 1807,
	"တူး" => 4,
	"ဘူးလား" => 397,
	"။" => 10586,
	"အမျိုးသား" => 7,
	"သန့်စင်ခန်း" => 2,
	"ဘယ်" => 93,
	"မှာလဲ" => 144,
	"သူမ" => 1026,
	"ဘေးမှာ" => 5,
	"ရှိ" => 293,
	"တဲ့" => 282,
	"စာအုပ်" => 95,
	"ဘယ်သူ့" => 351,
	"ကို" => 2249,
	"နှိပ်စက်" => 7,
	"ခဲ့သလဲ" => 64,
	"သူ" => 871,
	"မင်းကို" => 139,
	"ဘာဖြစ်လို့" => 63,
	"လက်ထပ်ခဲ့" => 1,
	"သလဲ" => 362,
	"ဆိုတာ" => 111,
	"မင်း" => 1844,
	"နားလည်" => 28,
	"လား" => 179,
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

ဖိုင်ရဲ့နောက်ဆုံးပိုင်းကို tail နဲ့လည်း ကြည့်ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ tail -n 30  ./source.lex.lex2perl 
	"ခရီးသည်" => 1,
	"လုပ်ခဲ့မိတာ" => 1,
	"နီမလေးဟာ" => 1,
	"ကစားစရာ" => 1,
	"ပိုးကောင်တွေကို" => 1,
	"ထွက်သွားပြီ" => 1,
	"မိတ္တူကူးစက်ထဲ" => 1,
	"ထည့်ဖို့" => 1,
	"ပိုက်ဆံအကြွေ" => 1,
	"၇နာရီခွဲလေ" => 1,
	"အခုကို" => 1,
	"သွားမှ" => 1,
	"ရတော့မှာ" => 1,
	"ကြောင်လေးတွေ" => 1,
	"ဟောပြော" => 1,
	"ဖက်မထား" => 1,
	"ငိုနေတဲ့" => 1,
	"ဆူညံသံကို" => 1,
	"နုတ်စ်" => 1,
	"ကိုတောင်" => 1,
	"ဆိုနိုင်ပါ့မလား" => 1,
	"အစာစား" => 1,
	"ကျွေး" => 1,
	"ဇွန်းတွေကို" => 1,
	"ဆေးပါ" => 1,
	"ယောက်ခမ" => 1,
	"သူနာပြုတွေ" => 1,
	"ဖြတ်ဖြတ်" => 2,
	"ဇာတ်လမ်းတွဲတွေကို" => 1,
}
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$
```

## Testing nat-pair2tmx Command

ဒီ nat-pair2tmx command က NATools file format corpus နှစ်ဖိုင်ကို သုံးပြီးတော့ TMX file format အဖြစ် ပြောင်းပေးတဲ့ command ပါ။  
အသုံးဝင်တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ nat-pair2tmx ./corpus.MY MY ./corpus.BK BK  >  corpus-my-bk.tmx
```

```$ head -30 ./corpus-my-bk.tmx``` နဲ့ ကြည့်ရင် TMX format output ဖိုင်ကို အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  

```xml

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE tmx SYSTEM "http://www.lisa.org/tmx/tmx14.dtd">
<tmx>
 <header creationtool="nat-pair2tmx" datatype="plaintext" srclang="MY" creationtoolversion="0.7.12" o-tmf="natcorpus" segtype="paragraph" adminlang="EN">
 </header>
 <body>
  <tu>
   <tuv xml:lang="MY">
    <seg>တွင်း မ တူး ဘူးလား ။ </seg>
   </tuv>
   <tuv xml:lang="BK">
    <seg>တွင်း မ တူး ရလား ။ </seg>
   </tuv>
  </tu>
  <tu>
   <tuv xml:lang="MY">
    <seg>အမျိုးသား သန့်စင်ခန်း ဘယ် မှာလဲ ။ </seg>
   </tuv>
   <tuv xml:lang="BK">
    <seg>အမျိုးသား သန့်စင်ခန်း ဘာမှာ ။ </seg>
   </tuv>
  </tu>
  <tu>
   <tuv xml:lang="MY">
    <seg>သူမ ဘေးမှာ ရှိ တဲ့ စာအုပ် ။ </seg>
   </tuv>
   <tuv xml:lang="BK">
    <seg>နင့် ဘေး မှာ ရှိတဲ့ စာအုပ် ။ </seg>
   </tuv>
  </tu>
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$
```

## Testing nat-shell

nat-shell command ကို လေ့လာကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ nat-shell 
Welcome to NATools shell tool
(nat)usage
Gets help for a command. Use:
	usage <command>
You can get a list of available commands using
	commands

(nat)commands
 Commands available:
   align
   codify
   commands
   encode
   grep
   help
   index
   init
   mkdict
   open
   usage

(nat)usage align
Aligns all chunks or a specific one. Use:
	align [<chunk_nr>|all]

(nat)usage codify
Codifies a parallel corpus. Use:
	codify <corpus-1> <corpus-2>

(nat)usage encode
Codifies a parallel corpus. Use:
	codify <corpus-1> <corpus-2>

(nat)usage index
Join all invertion indexes
(nat)usage init
Initializes a directory for a NATools corpus. Use:
	init <dir> <name>

(nat)usage mkdict

(nat)usage open
Open a NATools corpus. Use:
	open <dir>

(nat)

```

## perldoc for All NATools Commands

NATools က support လုပ်ထားတဲ့ command တွေက တော်တော်များများရှိလို့ သုံးပုံသုံးနည်း ကို perldoc နဲ့ ကြည့်ဖို့ အောက်ပါအတိုင်း command ပေးခဲ့...  
(perldoc ဆိုတာက perl program တွေရဲ့ help screen documentation ကို print လုပ်ပေးတဲ့ command ပါ)  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ compgen -c nat- | xargs -I{} perldoc {} | sed '/Copyright (C)/a ==========' > perldoc-out.txt
```

အောက်ပါ command တွေအတွက်တော့ perldoc ပြင်ဆင်ထားတာ မရှိဘူး...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ compgen -c nat- | xargs -I{} perldoc {} | sed '/Copyright (C)/a ==========' > perldoc-out.txt
No documentation found for "nat-mergeidx".
No documentation found for "nat-server".
No documentation found for "nat-css".
No documentation found for "nat-samplea".
No documentation found for "nat-pre".
No documentation found for "nat-sentalign".
No documentation found for "nat-mat2dic".
No documentation found for "nat-grep".
No documentation found for "nat-words2id".
No documentation found for "nat-postbin".
No documentation found for "nat-ngrams".
No documentation found for "nat-ntd-add".
No documentation found for "nat-sampleb".
No documentation found for "nat-ipfp".
No documentation found for "nat-mkntd".
No documentation found for "nat-initmat".
No documentation found for "nat-ntd-dump".
```

perldoc-out.txt ဖိုင်ထဲမှာ အောက်ပါအတိုင်း help screen output တွေကို offline ဖတ်လို့ ရလိမ့်မယ်...  
(command တစ်ခုစီရဲ့ help screen အပြီးမှာ ====== နဲ့ ခြားထားတယ်)  

```
NAME
    nat-rank - classifies each parallel corpus aligned sentence

SYNOPSIS
      nat-rank <ParallelCorpus>

DESCRIPTION
    This tool reads the "ParallelCorpus" configuration file and computes a
    translation quality value for each aligned sentence. This quality value
    is computed using the terminology dictionary obtained by the word
    alignment process.

SEE ALSO
    NATools documentation;

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-lex2perl - dumps a lexicon file as Perl hash.

SYNOPSIS
       nat-lex2perl <file.lex>

DESCRIPTION
    This tool is used mainly for debug of lexicon files ("file.lex" files).
    Pass one as parameter and it will output a Data::Dumper file with the
    lexicon information.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-examplesExtractor: extracts translation examples and terminology
    from a NATools corpus.

SYNOPSIS
       nat-examplesExtractor <offset> <length> <file1> <file2>
       nat-examplesExtractor -local=cp -rules=f.rul 0 100 cp/source.001 cp/target.001

DESCRIPTION
    This command is the example and terminology extractor. In fact it still
    needs a lot of work and for now I really suggest you to contact me for
    more details.

Options
     -rules=file
     -local=directory

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-pair2tmx - join two files in NATools input format into a TMX file.

SYNOPSIS
       nat-pair2tmx <file1> <lang1> <file2> <lang2>

DESCRIPTION
    This script is used to convert a pair of files in NATools input format
    (translation units separated by a dollar sign) into a TMX file.

    To use it supply two NATools input files (with same number of
    translation units) and two language descriptors. For instance,

      nat-pair2tmx corpus.pt pt corpus.en en  >  corpus-pt-en.tmx

    Note that the TMX will be output to STDTOU.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-tmx2pair - splits a TMX file into several files, one for each
    language

SYNOPSIS
     nat-tmx2pair f.tmx

DESCRIPTION
    This script takes a TMX file and outputs n different files, one for each
    language with translation units separated by dollar signs (NATools
    standard input format).

    The files creates are based on the tmx filename, with the language tag
    appended in the end.

SEE ALSO
    NATools documentation, perl(1).

AUTHOR
    Alberto Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-compareDicts - used to compare two PTDs in Perl dumper format.

SYNOPSIS
      print "\tnat-compareDicts [-stats] [-html] [-full] <dic1.dmp> <dic2.dmp>\n\n";

DESCRIPTION
    This program compares two Probabilistic Translation Dictionaries in Perl
    Dumper format. It can be used in four different ways:

    *   With no switches, a shell will be loaded. In this shell the user can
        entry words, and those words entries in the dictionary willl be
        shown.

    *   With the "-html" switch, an HTML table will be printed to STDOUT.
        This table tries to show entries will less or more differences
        between the two dictionaries.

    *   The "-full" switch prints to STDOUT all entries from the
        dictionaries together with some comparison values.

SEE ALSO
    perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-codify - Command line tool to codify corpora

SYNOPSIS
       nat-codify <file1.nat> <file2.nat>

       nat-codify -tmx <file.tmx>

DESCRIPTION
    The "-tokenize" flag can be used to force NATools to tokenize the texts.
    Note that at the moment a Portuguese tokenizer is used for all
    languages. This might change in the future.

    The "-id=name" flag can be used to force NATools Corpora name. By
    default the name is read interactively.

    The "-q" flag can be used to force quite mode. In thic case, the name is
    extracted from the file-names.

    The "-lang=PT..EN" flag can be used to force languages.

SEE ALSO
    NATools documentation, perl(1), nat-create

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2002-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-shell - A shell interface to NATools corpora alignment

SYNOPSIS
      nat-shell

DESCRIPTION
    This is intended to be a shell for NATools main command. At the moment
    is just supports the creation of parallel corpora. Details on the shell
    commands usage are available inside the shell. Just issue a "usage"
    command at the prompt.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-create - Command line tool to create NATools Corpora Objects

SYNOPSIS
       nat-create <file1.nat> <file2.nat>

       nat-create -tmx <file.tmx>

DESCRIPTION
    This is the basic command used to create a NATools Corpora Object from
    the command line.

    A NATools Corpora Object is a ditectory with:

    *   the configuration file ("nat.cnf" - metadata information)

    *   the corpus

    *   the corpus indexes

    *   the probabilistic translation dictionaries ("source-target.dmp",
        "target-source.dmp")

    *   the (bi,tri,tetra)grams databases ("source.ngrams", "target.ngrams")

  Known Switches
    tokenize
        The "-tokenize" flag can be used to force NATools to tokenize the
        texts. Note that at the moment a Portuguese tokenizer is used for
        all languages. This might change in the future.

    id  The "-id=name" flag can be used to force NATools Corpora name. By
        default the name is read interactively.

    q   The "-q" flag can be used to force quiet mode. In thic case, the
        name is extracted from the file-names.

    lang
        The "-lang=PT..EN" flag can be used to force languages.

    ngrams
        The "-ngrams" flag can be set to force NATools to create ngrams
        indexes.

    noEM
        The "-noEM" flag is used to bypass the EM-Algorithm (useful for
        debug purposes, mainly).

    ipfp
        The "-ipfp" flag is mutually exclusive with "-noEM", "-samplea" and
        "-sampleb". It defines that the EM-Algorithm to be used is the IPFP
        one. Optional numeric argument is the number of iterations. Defaults
        to 5.

    samplea
        The "-samplea" flag is mutually exclusive with "-noEM", "-ipfp" and
        "-sampleb". It defines that the EM-Algorithm to be used is the
        Sample A one. Optional numeric argument is the number of iterations.
        Defaults to 10.

    sampleb
        The "-sampleb" flag is mutually exclusive with "-noEM", "-ipfp" and
        "-samplea". It defines that the EM-Algorithm to be used is the
        Sample B one. Optional numeric argument is the number of iterations.
        Defaults to 10.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2011 by Alberto Manuel Brandão Simões
==========

NAME
    nat-ngramsIdx - Indexes a ngrams SQLite file

SYNOPSIS
       nat-ngramsIdx source.2.ngrams

DESCRIPTION
    This is an utility tool to create indexes in ngrams SQLite files.
    Normally you do not need to use it directly.

SEE ALSO
    NATools documentation

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2007-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-dumpDicts - Command line tool to dump NATools PTDs

SYNOPSIS
       nat-dumpDicts <natools-dir>

       nat-dumpDicts -self <natools-dir>

DESCRIPTION
    This command is used to dump NATools Probabilistic Translation
    Dictionaries in different formats. By default a Perl Data::Dumper format
    is used, but other formats are also available, like SQLite database.

  Data::Dumper
    To dump a PTD in Perl can be performed in three different ways:

    *   Use it directly with a NATools corpus directory path, and it will
        create two files in the current directory with the dictionaries.
        They will be named "source-target.dmp" and "target-source.dmp".

        Note: this process will overwrite any files with those names.

    *   Use it with the "-self" flag and a NATools corpus directory path.
        The dictionaries will be created inside the NATools corpus directory
        and will be named "source-target.dmp" and "target-source.dmp".

        Note: this process will overwrite any files with those names.

    *   Used mainly for debug purposes, you can also supply four arguments
        to "nat-dumpDicts" (together with the "-full" flag). These arguments
        are the source lexicon file, the source-target binary dictionary
        file, the target lexicon file and finally the target-source binary
        dictionary file. If this all seems strange to you, just do not use
        it.

           nat-dumpDicts -full <src.lex> <src-tgt.bin> <tgt.lex> <tgt-src.bin>

  SQLite database
    When running this command you can supply a "-sqlite=databasename"
    option. In this case, instead of dumping in Perl Data::Dumper format, a
    sqlite database will be created. You can use this option with or without
    the "-full" flag, but there isn't a "-self" option as the output
    filename is supplied in the command line.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-mkMakefile - generates a pmakefile to be used by Makefile::Parallel

SYNOPSIS
      nat-mkMakefile -id=<ID> <sourceCrp> <targetCrp>   >   pmakefile
      nat-mkMakefile -id=<ID> <tmxfile>                 >   pmakefile

DESCRIPTION
    This script generates a parallel makefile to be used by
    Makefile::Parallel to align and extract examples using a PBS based
    cluster.

    The "-id" switch is required and should contain the identifier of the
    corpus to be created.

OPTIONS
    "-full"
        Creates the full makefile, including n-grams and terminology
        extraction.

    "-ngrams"
        Creates the makefile including n-grams computation.

    "-terminology"
        Creates the makefile including terminology extraction.

SEE ALSO
    NATools documentation, Makefile::Parallel, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-StarDict - Creates a StarDict from a NATools corpus.

SYNOPSIS
      nat-StarDict <NatCorpus>

DESCRIPTION
    This tool creates a StarDict (http://stardict.sourceforge.net)
    dictionary with the probabilistic translation dictionary (source-target)
    and translation examples for the translations with higher translation
    probabilities.

    Note that this script is *NOT* fully functional. It outputs a perl
    structure that needs to be converted to StarDict format.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-ptd - concentrates a set of PTD commands in a common interface

SYNOPSIS
      nat-ptd [-v] <command> [command-args]

DESCRIPTION
    "nat-ptd" supports the following commands. Most places where a PTD needs
    to be specified, you can use a bziped2 PTD as far as the filename ends
    in bz2.

  help
    The method can be invoked without arguments, and a list of available
    commands will be printed.

    If an optional parameter with the name of a command is supplied, it
    prints detailed help for it (from this man-page).

        nat-ptd help [command-name]

  intersect
    Intersects domains from supplied PTDs. Keep lowerer counts and
    translation probabilities.

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  toSQLite
    This option can be used to convert a PTD to the SQLite format. First
    argument is the PTD filename. Second, optional, argument can be
    specified as the output filename.

  toDmp
    This option can be used to convert a PTD to the Dumper format. First
    argument is the PTD filename. Second, optional, argument can be
    specified as the output filename.

  toDmpBz
    This option can be used to convert a PTD to a Bzipped Dumper format.
    First argument is the PTD filename. Second, optional, argument can be
    specified as the output filename.

  toDmpXz
    This option can be used to convert a PTD to a XZipped Dumper format.
    First argument is the PTD filename. Second, optional, argument can be
    specified as the output filename.

  toTSV
    This option can be used to export a PTD to a plain text file using a Tab
    Separated Format. The first column represent each term, the second
    column the possible translation, and the third column the probability of
    this possible translation. This file can be directly used as a glossary
    in OmegaT.

    Usage:

      ptd-nat toTSV [-m=<p>] <ptd-filename> <dst-filename>

    The following options can be used:

    "-m=p"
        Minimum probabilty for translation to be exported. "p" must be a
        probability in the interval [0,1] (default: 0.5).

  toStarDict
    FIXME

    Usage:

      ptd-nat toStarDict [-m=<p>] [-d=<directory>] <ptd-filename> <dst-dict-name>

    The following options can be used:

    "-m=p"
        Minimum probabilty for translation to be exported. "p" must be a
        probability in the interval [0,1] (default: 0.4).

    "-d=directory"
        Destination directory for the created dictinary (default: .).

  stats
    Prints some basic statistics about a PTD.

  compare
    Given two PTD, print some basic statistics comparing their size,
    domains, etc.

  query
    This command allows you to query interactively a PTD.

  grep
    Greps entries matching a specific pattern from a PTD. Supply a pattern
    and a PTD file. By default it dumps a subset PTD with entries that
    match. With the "-compact" option it will print a small table with the
    entry's best translation.

        nat-ptd grep [-compact] [-o=outfile] <pattern> <ptd-file>

  compose
    This method receives a two or more dictionaries.

    When receiving a pair of dictionaries (first dictionary target language
    should be the same as the second dictionary source language), composes
    them, resulting a PTD from first dictionary source language to second
    dictionary target language.

    This method can be used with more than two dictionaries for a full
    transitive dictionary computation.

    You can specify the output filename with the "-o" switch.

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  filter
    This method filters a dictionary (or dictionary pair) accordingly with
    some default values (that can be adjusted).

    If the supplied name is a directory, it is supposed to be of a NATools
    object (a NATools alignment folder). In this case, files
    "source-target.dmp" and "target-source.dmp" are searched inside it.

    If the supplied name is not a directory, it is suppoed to be a name of a
    PTD dump file. This command will check if it is alone (just a direction)
    or if a second filename was supplied. If two were supplied, they are
    considered bidirectional (source-target and target-source).

    Therefore, three possible usages:

        nat-ptd filter <natools-obj-dir>
        nat-ptd filter <file.dmp>
        nat-ptd filter <file-s-t.dmp> <file-t-s.dmp>

    The following switchs can be used:

    "-numbers"
        By default the filtering will remove terms (entries and
        translations) with numbers (only numbers, with possible digit
        separators: space, comma, point, colon). Use this switch to force
        them to be preserved.

    "-symbols"
        Any other term type that is not a standard word (with possible dash
        or apostrophe) or a number (as described above), is considered to
        include strange symbols, and will be ignored. Use this switch to
        force them to be preserved.

    "-none"
        By default, the 'no translation', also known as 'none', is removed.
        You can force it to be preserved with this switch.

    "-occs=n"
        Defines the minimum occurrence count for entries to be preserved. By
        default the used value is 2 (that is, entries with 1 occurrence are
        discarded). Use 0 to not discard any entry by occurrence count.

    "-prob=p"
        Defines the minimum probability for translations to be preserved. By
        default the value is 1% (0.01). Define the value as 0 to preserve
        all translations.

    "-bidir"
        Defines if the filtering should check for bidirectional
        translations, that is, preserve only terms which translations'
        translations' include that term. Mathematically, preserve t if

            t   in   Translations ( Translations ( t ) )

        Note that this is only available for NATool objects or dictionary
        pairs. By default this switch is ON. Turn it OFF assigning a 0 to
        the switch: "-bidir=0"

    Also, the "-o" switch can be used to define an output filename. When
    using a pair of dictionaries, specify the output filenames separated by
    a comma: "-o=outputfile1,outputfile2".

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  lowercase
    This method recompute the probabilities for a dictionary, lowercasing
    all terms, and summing up occurrences, and recomputing probabilities.

        nat-ptd lowercase [-o=outputfile] <ptd-filename>

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  reprob
    This method recompute the probabilities from a dictionary. It sums up
    all possible translations probabilities, consider that total to be 100%
    (1), and recomputes each probability accordingly.

    It takes a required argument, the name of the PTD dump file. Optionally,
    you can supply an output file with the "-o" switch.

        nat-ptd reprob [-o=outputfile] <ptd-filename>

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  add
    Adds two or more PTD files into a single PTD file. They should have the
    same source and target language. You can use the "-o" switch to specify
    an output filename.

    As of recent NATools versions, you can supply an option "-type" to
    specify the type of output file ("dmp" or "sqlite" are supported, and
    "dmp" is the default).

  ucts
    Create unambiguous-concept traslation sets.

      ptd-nat ucts [-m=<number>] [-M=<number>] [-p=<probabilty>] [-P=<probability>] <ptd-filename> <ptd-filename>

    The following options can be used:

    "-m=n"
        Mininum number of occurences of each token. "n" must be an integer
        (default: 10).

    "-M=n"
        Manixum number of occurences of each token. "n" must be an integer
        (default: 100).

    "-p=p"
        Minimum probabilty for translation. "p" must be a probability in the
        interval [0,1] (default: 0.2).

    "-P=p"
        Minimum probabilty for the inverse translations. "p" must be a
        probability in the interval [0,1] (default: 0.8).

    "-r=0|1"
        Print rank (default: 0).

  bws
    Create bi-words sets.

      ptd-nat bws [-m=<number>] [-p=<probabilty>] <ptd-filename> <ptd-filename>

    The following options are available:

    "-m=n"
        Mininum number of occurences of each token. "n" must be an integer
        (default: 10).

    "-p=p"
        Minimum probabilty for translation. "p" must be a probability in the
        interval [0,1] (default: 0.4).

    "-r=0|1"
        Print rank (default: 0).

SEE ALSO
    NATools, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

    Nuno Alexandre Carvalho, <smash@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2010-2014 by Natura Project
==========

NAME
    nat-mkRealDict - used to create a dictionary similar to a PTD based on a
    word aligned corpus.

SYNOPSIS
      nat-mkRealDict <aligned-corpus>

DESCRIPTION
    While not fully functional, this scripts reads from the supplied file an
    word aligned corpus (two columns separated by a tab character). The
    result printed to STDOUT is a dictionary similar to a PTD in structure)
    with the real alignments used in the corpus.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-addDict: adds a dictionary in Perl Dumper format into a NATools
    corpus.

SYNOPSIS
      nat-addDict <natDir> <dumperFile>

      nat-addDict <natDir> <source-target.dmp> <target-source.dmp>

DESCRIPTION
    This command is used to add an external dictionary (in Perl Dumper
    format) to a NATools corpus.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-dict - interface for binary PTDs operations.

SYNOPSIS
            nat-dict add <dic1.bin> <dic2.bin>

DESCRIPTION
    This tool is indented to be an interfce for binary PTDs algebra. At the
    moment is just supports the following commands:

    "add"
        Used to add two binary PTDs. In fact, it accumulates the second
        dictionary in the first one, so be careful using if in case you want
        to preserve the original dictionaries.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2012 by Alberto Manuel Brandão Simões
==========

NAME
    nat-makeCWB - Dumps a NATools corpus in a format suitable to be imported
    in CWB

SYNOPSIS
      nat-makeCWB [-encode=<CWBName> -d=<CWBCrpDir> [-r=<CWBRegistry>]] <NatCrpDir>

DESCRIPTION
    This small scripts exports a NATools corpus directory to a pair of files
    that can be easily imported in Corpus WorkBench (CWB).

    By default nat-makeCWB processes a NATools corpora dir an creates a pair
    of files, source.cqp and target.cqp that can be later imported into CWB
    using cwb-align-import.

    Flags:

    -encode
        If this option is used then nat-makeCWB will try to use cwb tools to
        create the aligned corpus. This option should be follows by the
        corpora name. The corpora creates will nem named "name_source" and
        "name_target" respectively.

        This option should be used in conjunction with option "-d".

        The CWB registry directory will be guessed using "cwb-config" or
        "CORPUS_REGISTRY" environment variable. To use other path, please
        specify it with -r.

    -d  This option is required when using "-encode". It specifies CWB
        corpus directory (without the corpus name).

    -r  Use this option to force a registry path other than the system
        default.

    -debug
        Use this option if you need to debug the temporary files. If this
        option is supplied they will not be deleted.

SEE ALSO
    NATools, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2010 by Alberto Manuel Brandão Simões
==========

NAME
    nat-sentenec-align - simple interface for Vanilla aligner.

SYNOPSIS
      nat-sentence-align [-tmx] [-single] [-d=.EOS] [-D=.EOP] <f1> <f2>

DESCRIPTION
    This command is a frontend for the Vanilla aligner supplied with
    NATools. To use it you must supply two parallel files with soft and hard
    delimiters for sincronization.

    By default these delimiters are '.EOS' and '.EOP'. You can change them
    using the "-d" and "-D" switches.

    At the end it creates a pair of sentence-aligned files. You can supply a
    "-tmx" option to force the creation of a TMX, or the "-single" option to
    force the creation of a single file with the two languages (mainly used
    for debugging).

SEE ALSO
    NATools Documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

NAME
    nat-substDict: substitutes a dictionary in a NATools corpus by a Perl
    Dumper format PTD.

SYNOPSIS
      nat-substDict <natDir> <dumperFile>
      nat-substDict <natDir> <source-target.dmp> <target-source.dmp>

DESCRIPTION
    This tool is used to substitute a dictionary on a NATools corpus. Unless
    you know what you are doing, this can be a bad option making the corpus
    unusable.

    To use it just pass as first parameter a NATools corpus directory and as
    second argument a Perl Data::Dumper file with the two dictionaries (or a
    pair of Data::Dumper files, one with each dictionary).

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões
==========

```

## Reading NATools Perl Scripts

Script or Command တစ်ခုချင်းစီရဲ့ source code တွေကို လေ့လာချင်ရင်တော့ အောက်ပါ link ကနေ သွားပြီး coding ဖတ်တာ လုပ်ပါ။  

[https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/source/scripts](https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/source/scripts)  

ဥပမာ nat-sentence-align  ဆိုတဲ့ command ကို perl script ဘယ်လိုရေးထားသလဲ ဆိုတာကို သိချင်ရင်၊ nat-sentence-align ဆိုတာကို click လုပ်ရင် အောက်ပါ link ကို jump လုပ်သွားပြီးတော့  

[https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/source/scripts/nat-sentence-align](https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/source/scripts/nat-sentence-align)  

browser မှာ source code ကို ဖတ်လို့ ရပါလိမ့်မယ်။  

```perl
#!/usr/bin/perl -s
 
use Lingua::PT::PLNbase;
use Lingua::NATools::ConfigData;
use warnings;
use strict;
 
our ($h);
our ($tmx,$single,$raw, $d, $D, $utf8);
 
sub usage {
    print "nat-sentence-align: simple interface for Vanilla aligner\n\n";
    print "\tnat-sentence-align [-tmx] [-single] [-d=.EOS] [-D=.EOP] <f1> <f2>\n\n";
    print "For more help, please run 'perldoc nat-sentence-align'\n";
    exit;
}
 
usage() if ($h);
 
my $BINPREFIX = Lingua::NATools::ConfigData->config('bindir');
my $command = "";
 
my $file1 = shift or die "I need two files to align\n";
my $file2 = shift or die "I need two files to align\n";
 
if ($tmx && $single) { undef $single }
 
unless ($raw) {
  $/ = "\n\n";
  for my $file ($file1, $file2) {
    open I, $utf8?"<:utf8":"<", $file or die "Cannot open file '$file': $!\n";
    open O, $utf8?">:utf8":">", "$file.tok" or die "Cannot open file '$file.tok': $!\n";
 
    while (<I>) {
      next if m!^(\s\n)*$!;
      s/\n/ /g;
      s/\ +/ /g;
 
      my @sentences = sentences($_);
      for my $s (@sentences) {
        my @atomos = atomiza($s);
        print O join("\n",@atomos),"\n.EOS\n";
      }
 
      print O ".EOP\n";
    }
    close O;
    close I;
  }
  $command .= " -d .EOS -D .EOP $file1.tok $file2.tok";
} else {
  die "Using 'raw', you must supply -d and -D" if ($raw && (!$d || !$D));
  $command .= " -d $d -D $D $file1 $file2";
}
 
 
$command = " -s$command" if ($single);
 
 
$command = "$BINPREFIX/nat-sentalign$command";
system($command);
die $@ if ($@);
#print $command;
 
if ($tmx) {
  # files are $file1.tok.al e $file2.tok.al
  # langs...
  local $/ = "\n";
  my ($lang1, $lang2);
  print STDOUT "Please enter language code for '$file1': ";
  chomp($lang1 = <STDIN>);
 
  print STDOUT "Please enter language code for '$file2': ";
  chomp($lang2 = <STDIN>);
 
  print STDOUT "Producing TMX '$lang1-$lang2.tmx'...\n";
  `nat-pair2tmx $file1.tok.al $lang1 $file2.tok.al $lang2 > $file1-$file2.tmx`;
}
```

## Note for Me/Students

NATools counts the co-occurrences of words in all aligned sentence pairs and builds a sparse matrix of word-to-word probabilities using an iterative expectation maximization algorithm. Then, the two probabilistic bilingual dictionaries are composed by the elements with the highest probability values in the matrix.  

Reference:  

- A. M. Sim˜oes and J. J. Almeida. NATools – A statistical word aligner workbench. Processamiento del Lenguaje Natural, 31:217–224, 2003.   
- Caseli, H.M., Gomes, F.T., Pardo, T.A.S. & Nunes, M.G.V. (2008), "VisualLIHLA: the visual online tool for lexical alignment", In Proceedings of the VI Workshop em Tecnologia da Informação e da Linguagem Humana (TIL). Vila Velha, ES. October 2008., pp. 1-3.  
- Santos, Diana & Simões, Alberto. (2008). Portuguese-English Word Alignment: some Experiments. 

## Relating to StarDict Building

**experiment နဲ့ တိုက်ရိုက် မဆိုင်ပါ** 

StarDict, QStarDict GUI Dictionary application တွေနဲ့ ကိုယ်ဆောက်ထားတဲ့ dictionary ကို တွဲသုံးလို့ ရမယ့် ပုံရှိတယ်။  
အချိန်ရတဲ့အခါမှာ ဆက်လုပ်ရန်...  

StarDict dictionary format ဆောက်ချင်ရင် အောက်ပါ command နဲ့ ဆောက်လို့ရ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ nat-StarDict ./my-bk-phrase-lex/ > my-bk-stardict.dict
```

stardict or QStarDict ရဲ့ format က tar.bz2 မို့လို့... tar.bz2 format အဖြစ် ပြောင်းတဲ့ command က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ tar -cvjSf ./my-bk-stardict.tar.bz2 ./my-bk-stardict.dict 
./my-bk-stardict.dict
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$
```

stardict တွေကို ဖတ်တဲ့ folder က homefolder ရဲ့ အောက်မှာ hidden အနေနဲ့ ထားရတာမို့ အဲဒီ folder က ပုံမှန်ဆိုရင် မရှိသေးလို့ ဆောက်ရတယ်။ အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ mkdir -p ~/.stardict/dic
```

online ကနေ download လုပ်ထားတဲ့ stardict Basic Thai Dictionary ဆိုတဲ့ဟာကို qstardict နဲ့ သုံးလို့ ရချင်ရင်အောက်ပါအတိုင်း လုပ်လို့ ရတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ cp ~/Downloads/stardict-comn_sdict_axm05_BASIC_Thai_Lang-2.4.2.tar.bz2 .
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ tar xjvf ./stardict-comn_sdict_axm05_BASIC_Thai_Lang-2.4.2.tar.bz2 -C ~/.stardict/dic/
stardict-BASIC_Thai_Lang-2.4.2/
stardict-BASIC_Thai_Lang-2.4.2/BASIC_Thai_Lang.idx
stardict-BASIC_Thai_Lang-2.4.2/BASIC_Thai_Lang.ifo
stardict-BASIC_Thai_Lang-2.4.2/BASIC_Thai_Lang.dict.dz
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w$ qstardict 
```

လောလောဆယ် အခု ရလာတဲ့ NATools ရဲ့ dictionary ကို ဘယ်လို qstardict or stardict က သုံးလို့ရအောင် လုပ်ရမလဲ မသိသေး...  

(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/my-x/my-bk/w2w/my-bk-phrase-lex$ perldoc nat-StarDict

```
NAME
    nat-StarDict - Creates a StarDict from a NATools corpus.

SYNOPSIS
      nat-StarDict <NatCorpus>

DESCRIPTION
    This tool creates a StarDict (http://stardict.sourceforge.net)
    dictionary with the probabilistic translation dictionary (source-target)
    and translation examples for the translations with higher translation
    probabilities.

    Note that this script is *NOT* fully functional. It outputs a perl
    structure that needs to be converted to StarDict format.

SEE ALSO
    NATools documentation, perl(1)

AUTHOR
    Alberto Manuel Brandão Simões, <ambs@cpan.org>

COPYRIGHT AND LICENSE
    Copyright (C) 2006-2009 by Alberto Manuel Brandão Simões

```

perl structure အဘိဓာန်ပဲ ရသေးတယ်။  
အဲဒီကနေ stardict က သိအောင် ပြောင်းပေးရမယ်။  


## Reference

- [https://en.wikipedia.org/wiki/Translation_Memory_eXchange](https://en.wikipedia.org/wiki/Translation_Memory_eXchange)  
- [StarDict Dictionary Format](https://en.wikipedia.org/wiki/StarDict)  
- [Adding a New Dictionary to QStarDict](https://github.com/a-rodin/qstardict/wiki/Dictionaries-Installation)  
- [StarDict Dictionaries](https://sites.google.com/site/gtonguedict/home/stardict-dictionaries)  
- [NATools – A Statistical Word Aligner Workbench](https://rua.ua.es/dspace/bitstream/10045/1550/1/PLN_31_26.pdf)  
- [LIHLA: A lexical aligner based on language-independent heuristics](http://www.nilc.icmc.usp.br/nilc/download/CaNuFoENIA05.pdf)  
- [PANACEA Project, Platform for Automatic, Normalized Annotation and Cost-Effective Acquisition of Language Resources for Human Language Technologies](https://cordis.europa.eu/docs/projects/cnect/4/248064/080/deliverables/001-PANACEAD51.pdf)  
- [VisualLIHLA - Lexical alignment visualization](http://www.nilc.icmc.usp.br/nilc/tools/visuallihla/lihla.htm)  
- [Portuguese-English word alignment: some experiments](http://www.lrec-conf.org/proceedings/lrec2008/pdf/760_paper.pdf)  
- [Tools and Resources of Interinstitutional Center for Computational Linguistics](http://www.nilc.icmc.usp.br/nilc/index.php/tools-and-resources)  
- [Presentation Slide of Original Developer Dr. Alberto Simões, mostly in Portuguese](https://ambs.zbr.pt/en/pres.html)  


