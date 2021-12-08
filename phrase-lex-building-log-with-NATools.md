# Phrase Level Lexicon Building Log with NATools

NATools ကို အရင် install လုပ်ထားရလိမ့်မယ်...  
Installation လုပ်ပုံလုပ်နည်းက အောက်ပါ link ကို ကြည့်ပါ။  
[https://github.com/ye-kyaw-thu/error-overflow/blob/master/NATools-installation-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/NATools-installation-log.md)  

## Alignment with NATools

အရင်ဆုံး parallel corpus ကို ပြင်ဆင်ထားရလိမ့်မယ်။  
word-to-word lexicon ဆောက်တုန်းကလိုပဲ folder တွေကို အောက်ပါအတိုင်း ခွဲထားခဲ့တယ်...  

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

alignment လုပ်ခိုင်းကြည့်တော့ အောက်ပါအတိုင်း ERROR ပေးတယ်။  

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

## Relating to StarDict Building

StarDict, QStarDict application တွေနဲ့ ကိုယ်ဆောက်ထားတဲ့ dictionary ကို တွဲသုံးလို့ ရမယ့် ပုံရှိတယ်။  
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


