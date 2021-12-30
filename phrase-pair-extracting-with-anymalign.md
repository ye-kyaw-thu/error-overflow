# Phrase Pair Extracting with Anymalign

Parallel corpus ကနေ alignment လုပ်ပြီး phrase pair တွေကို ဆွဲထုတ်တာကို ဗမာစာနဲ့ တိုင်းရင်းသားဘာသာ စကားတွေအကြားကို လုပ်ကြည့်ခဲ့တဲ့ experiment log ပါ။  
ဒေါက်တာတန်း ကျောင်းသူ မေမြတ်မြတ်ခိုင်အတွက် ရည်ရွယ်ပြီး ပြင်ဆင်ခဲ့...  

## git clone

```
(base) ye@:/media/ye/project2/tool$ git clone https://github.com/alexhzhai/anymalign
Cloning into 'anymalign'...
remote: Enumerating objects: 24, done.
remote: Total 24 (delta 0), reused 0 (delta 0), pack-reused 24
Unpacking objects: 100% (24/24), 31.29 KiB | 471.00 KiB/s, done.
```

## Check Files and Folder of Anymalign Tool

```
(base) ye@:/media/ye/project2/tool$ cd anymalign/
(base) ye@:/media/ye/project2/tool/anymalign$ ls
anymalign.py  de.txt  en.txt  fr.txt  license.txt  output.txt  README.md  README_orig.txt
(base) ye@:/media/ye/project2/tool/anymalign$
```

## Call Help  

ဒီ alignment tool က propose လုပ်ထားတာ နည်းနည်းကြာနေပြီး သို့သော် multilingual alignment လုပ်လို့ ရတာနဲ့ alignment output ကလည်း human readable ဖြစ်လို့  
Pharaoh format ဖြစ်တဲ့ ဂဏန်းတွေကနေ ပြန် conversion လုပ်စရာ မလိုလို့ ကြိုက်တယ်။  
Python program ဖြစ်လို့ installation ဘာညာကလည်း မလိုပဲနဲ့ Alignment training speed ကလည်း မြန်ပါတယ်။  
ပြီးတော့ ဒီ tool ကို develop လုပ်ခဲ့ကြတဲ့ ဆရာဖြစ်တဲ့ Prof. Yves Lepage (Waseda University) နဲ့ကလည်း ရင်းနှီးလို့ တစ်ခုခုဆို Anymalign ကို သွားသွားသတိရတာနဲ့ သုံးဖြစ်နေတာ...  

run တဲ့အခါမှာ python2.7 နဲ့ run ဖို့ မမေ့ပါနဲ့...  
ပထမဆုံး parameter ကို သိဖို့အတွက် help ခေါ်ကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/tool/anymalign$ python2.7 ./anymalign.py  --help
Usage: (basic usage)
    python anymalign.py corpus.source corpus.target >translationTable.txt

For more control:
    python anymalign.py [INPUT_FILE[.gz|.bz2] [...]] >ALIGNMENT_FILE
    python anymalign.py -m [ALIGNMENT_FILES[.gz|.bz2] [...]] >ALIGNMENT_FILE

INPUT_FILE is a tab separated list of aligned sentences (1/line):
<sentenceNlanguage1> [<TAB> <sentenceNlanguage2> [...]]

A generated ALIGNMENT_FILE has the same format as INPUT_FILE (same
fields), plus three extra fields at the end of each line:
1) a space-separated list of lexical weights (1/language);
2) a space-separated list of translation probabilities (1/language);
3) an absolute frequency:
<phraseNlanguage1> [...] <TAB> <lexWeights> <TAB> <probas> <TAB> <frequency>

ALIGNMENT_FILES is the concatenation of several ALIGNMENT_FILE's.

Check out http://users.info.unicaen.fr/~alardill/anymalign/ for more!

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -m, --merge           Do not align. Input files are pre-generated alignment
                        files (plain text format) to be merged into a single
                        alignment file.
  -T DIR, --temp-dir=DIR
                        (compatible with -m) Where to write temporary files.
                        Default is OS dependant.
  -q, --quiet           (compatible with -m) Do not show
                        progress information on standard error.

  Options to alter alignment behaviour:
    -a NB_AL, --new-alignments=NB_AL
                        Stop alignment when number of new alignments per
                        second is lower than NB_AL. Specify -1 to run
                        indefinitely. [default: -1]
    -i INDEX_N, --index-ngrams=INDEX_N
                        Consider n-grams up to n=INDEX_N as tokens. Increasing
                        this value increases the number of long n-grams
                        output, but slows the program down and requires more
                        memory [default: 1]
    -S NB_SENT, --max-sentences=NB_SENT
                        Maximum number of sentences (i.e. input lines) to be
                        loaded in memory at once. Specify 0 for all-in-memory.
                        [default: 0]
    -t NB_SEC, --timeout=NB_SEC
                        Stop alignment after NB_SEC seconds elapsed. Specify
                        -1 to run indefinitely. [default: -1]
    -w, --weight        Compute lexical weights (requires additional
                        computation time and memory).

  Filtering options:
    -D FIELDS, --discontiguous-fields=FIELDS
                        Allow discontiguous sequences (like "give up" in "give
                        it up") in languages at positions specified by FIELDS.
                        FIELDS is a comma-separated list of integers
                        (1-based), runs of fields can be specified by a dash
                        (e.g. "1,3-5").
    -l NB_LANG, --min-languages=NB_LANG
                        Keep only those alignments that contain words in at
                        least MIN_LANGUAGES languages (i.e. columns). Default
                        is to cover all languages.
    -n MIN_N, --min-ngram=MIN_N
                        Filter out any alignment that contains an N-gram with
                        N < MIN_N. [default: 1]
    -N MAX_N, --max-ngram=MAX_N
                        Filter out any alignment that contains an N-gram with
                        N > MAX_N (0 for no limit). [default: 7]

  Output formatting options:
    -d DELIM, --delimiter=DELIM
                        Delimiter for discontiguous sequences. This can be any
                        string. No delimiter is shown by default. Implies -D-
                        (allow discontinuities in all languages) if -D option
                        is not specified.
    -e ENCODING, --input-encoding=ENCODING
                        (compatible with -m) Input encoding. This is useful
                        only for HTML and TMX output formats (see -o option).
                        [default: utf-8]
    -L LANG, --languages=LANG
                        (compatible with -m) Input languages. LANG is a comma
                        separated list of language identifiers (e.g.
                        "en,fr,ar"). This is useful only for HTML (table
                        headers) and TMX (<xml:lang>) output formats (see -o
                        option).
    -o FORMAT, --output-format=FORMAT
                        (compatible with -m) Output format. Possible values
                        are "plain", "moses", "html", and "tmx". [default:
                        plain]
(base) ye@:/media/ye/project2/tool/anymalign$
```

## Testing timeout Command

anymalign က run ထားရင် တောက်လျှောက် alignment လုပ်နေမှာ သူ့ကို ရပ်ချင်ရင် Ctrl+C နဲ့ ရပ်ရတယ်။  
အဲဒီလို ရပ်လိုက်ရင် alignment လုပ်ထားတဲ့ output ကို screen ပေါ်မှာ သို့မဟုတ် terminal ပေါ်မှာပဲ ရိုက်ထုတ်ပေးတယ် အဲဒါကြောင့် command ရဲ့ နောက်ဆုံးမှာ " > outputfile" ဆိုတဲ့ ပုံစံနဲ့ run မှပဲ ဖိုင်အနေနဲ့ သိမ်းပေးလိမ့်မယ်။  

မလုပ်မဖြစ် မဟုတ်ပေမဲ့ language pair တစ်ခုချင်းစီကို သတ်မှတ်ထားတဲ့ အချိန်တစ်ခုအထိပဲ alignment training လုပ်ပြီး ရပ်လိုက်ချင်လို့ timeout command ကို အောက်ပါအတိုင်း သုံးကြည့်ခဲ့တယ်။ မိနစ် ၃၀ကြာရင် ရပ်ပါ ဆိုပြီးတော့ "30m" ဆိုတဲ့ setting နဲ့ timeout command ကို run ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ timeout 30m python2.7 /media/ye/project2/tool/anymalign/anymalign.py ../train.my ../train.bk > my-bk.align
Input corpus: 2 languages, 10622 lines
Aligning... (ctrl-c to interrupt)
(8806284 subcorpora, avg=12.82) 318672 alignments, 47 al/s(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ 
```

သို့သော် အထက်ပါလိုမျိုး command ပေးပြီး run ရင် output ဖိုင်ကို သိမ်းမပေးဘူး။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ wc my-bk.align 
0 0 0 my-bk.align
```

Control + C signal ကို anymalign ပရိုဂရမ်ကို ပို့ပေးချင်လို့ အောက်ပါအတိုင်း "--preserve-status" option ဖြည့်ပြီး run ကြည့်ခဲ့ပေမဲ့လည်း လိုချင်တဲ့ output ဖိုင်က ထွက်မလာဘူး...  

```
$ timeout --preserve-status 1m python2.7 /media/ye/project2/tool/anymalign/anymalign.py ../train.my ../train.bk > my-bk.align
```

timeout command --help 

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ timeout --help
Usage: timeout [OPTION] DURATION COMMAND [ARG]...
  or:  timeout [OPTION]
Start COMMAND, and kill it if still running after DURATION.

Mandatory arguments to long options are mandatory for short options too.
      --preserve-status
                 exit with the same status as COMMAND, even when the
                   command times out
      --foreground
                 when not running timeout directly from a shell prompt,
                   allow COMMAND to read from the TTY and get TTY signals;
                   in this mode, children of COMMAND will not be timed out
  -k, --kill-after=DURATION
                 also send a KILL signal if COMMAND is still running
                   this long after the initial signal was sent
  -s, --signal=SIGNAL
                 specify the signal to be sent on timeout;
                   SIGNAL may be a name like 'HUP' or a number;
                   see 'kill -l' for a list of signals
  -v, --verbose  diagnose to stderr any signal sent upon timeout
      --help     display this help and exit
      --version  output version information and exit

DURATION is a floating point number with an optional suffix:
's' for seconds (the default), 'm' for minutes, 'h' for hours or 'd' for days.
A duration of 0 disables the associated timeout.

If the command times out, and --preserve-status is not set, then exit with
status 124.  Otherwise, exit with the status of COMMAND.  If no signal
is specified, send the TERM signal upon timeout.  The TERM signal kills
any process that does not block or catch that signal.  It may be necessary
to use the KILL (9) signal, since this signal cannot be caught, in which
case the exit status is 128+9 rather than 124.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/timeout>
or available locally via: info '(coreutils) timeout invocation'
```

အထက်က ```--signal``` option မှာ ပြောထားတဲ့အတိုင်းပဲ ပေးလို့ရတဲ့ signal နာမည်တွေကို ```kill -l``` command နဲ့ ရှာကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX	
```

"Ctrl+C" ဆိုတာက "SIGINT" နဲ့ ညီတာမို့ timeout command ကို အောက်ပါအတိုင်း ```--signal=SIGINT``` option ပေးပြီး စမ်းrun ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ timeout --signal=SIGINT 1m python2.7 /media/ye/project2/tool/anymalign/anymalign.py ../train.my ../train.bk > my-bk.align
Input corpus: 2 languages, 10622 lines
Aligning... (ctrl-c to interrupt)
(303293 subcorpora, avg=12.36) Alignment interrupted! Proceeding...
129781 alignments
Sorting alignments
Computing conditional probabilities...
Outputting results...
```

ဖိုင်ရေးမရေးသိချင်လို့ wc command နဲ့ file size ကို စစ်ကြည့်တော့ ဖိုင်ရေးပေးသွားတယ် ဆိုတာကို confirmation ဖြစ်ပြီ။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ wc ./my-bk.align 
  129781  1317112 16773343 ./my-bk.align
```

file content ကို အောက်ပါအတိုင်း ဝင်စစ်ခဲ့...   

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$ head ./my-bk.align 
။	။	-	0.984014 0.986692	2570270
မ	မ	-	0.969712 0.932919	50553
သူ	သူ	-	0.974875 0.928916	23901
သိ	သိ	-	0.967190 0.969474	17245
။	ရယ် ။	-	0.005472 0.728134	14294
ကို	ကို	-	0.650083 0.791271	12165
မင်း	နင်	-	0.655438 0.842347	12102
သူမ	ဒယ်ကောင်မငယ်	-	0.752473 0.929304	8518
ကူညီ	ကူညီ	-	0.962621 0.975629	8447
ငါ	ငါ	-	0.952424 0.688787	8428
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-x/my-bk/w2w/anyma$
```

အိုကေ run လို့တော့ ရသွားပြီး အချိန်တစ်ခု သတ်မှတ်ပြီးတော့ parallel corpus တစ်ခုပြီးတစ်ခု alignment လုပ်သွားဖို့ပဲ ကျန်တော့တယ်။  

## Shell Script Writing

language pair က စုစုပေါင်း ၁၃ ခုရှိပြီးတော့ bi-directional alignment လုပ်ချင်တာကြောင့် အောက်ပါအတိုင်း shell script တစ်ပုဒ် ရေးခဲ့တယ်။  
ဒေတာပမာဏလည်း အများကြီး မဟုတ်တာကြောင့် ၁၅မိနစ် လောက်ဆိုရင် အတိုင်းအတာတစ်ခုအထိ phrase-pair တွေက ဆွဲထုတ်လို့ ရပြီလို့ ယူဆခဲ့ပြီး အရင်ဆုံး တစ်ခေါက် ပြီးအောင် run ကြည့်ဖို့ စိတ်ကူးခဲ့...  

```bash
#!/bin/bash

# phrase alignment for 13 language pairs with Anymalign Tool
# Last Updated: 30 Dec 2021
# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand

for fd in {my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc}
do
   src=${fd%-*}
   tgt=${fd##*-}
   mkdir -p $fd/w2w/anyma;
   cd $fd/w2w/anyma;
   echo "anymalign running for $src-$tgt...";
   timeout --signal=SIGINT 15m python2.7 /media/ye/project2/tool/anymalign/anymalign.py ../train.$src ../train.$tgt > $src-$tgt.align;
   head ./$src-$tgt.align;
   echo "==========";
   echo "anymalign running for $tgt-$src...";   
   timeout --signal=SIGINT 15m python2.7 /media/ye/project2/tool/anymalign/anymalign.py ../train.$tgt ../train.$src > $tgt-$src.align;
   head ./$tgt-$src.align;
   echo "==========";    echo "==========";
   cd ../../../;
done

```

## Phrase Pair Extraction 

Phrase pair extraction ကို "my-bk,my-ch,my-kc,my-ky,my-mo,my-pk,my-po,my-rk,my-rw,my-sh,my-sk,rk-bk,rw-kc" အတွက် လုပ်ခဲ့...  
ဒီနေရာမှာ သုံးထားတဲ့ ဘာသာစကားတစ်ခုချင်းစီရဲ့ သင်္ကတေအရှည်တွေက အောက်ပါအတိုင်း  

1. my = Myanmar
2. bk = Beik
3. ch = Mizo Chin
4. kc = Kachin (ဂျိန်းဖော)
5. ky = Kayah
6. mo = Mon
7. pk = Poh Kayin
8. po = Pa'O
9. rk = Rakhine
10. rw = Rawang
11. sh = Shan
12. sk = Sagaw Kayin

လက်ရှိမှာ run နေတုန်း ... ပြီးသလောက် log ကိုပဲ တင်ပေးထား...  

```
anymalign running for my-bk...
။	။	-	0.983761 0.986597	38180554
မ	မ	-	0.970767 0.931926	752729
သူ	သူ	-	0.974121 0.928685	351951
သိ	သိ	-	0.965710 0.970085	258000
။	ရယ် ။	-	0.005558 0.732639	215702
ကို	ကို	-	0.654232 0.799444	184084
မင်း	နင်	-	0.656136 0.838324	180005
ငါ	ငါ	-	0.954203 0.687019	125910
သူမ	ဒယ်ကောင်မငယ်	-	0.746889 0.927282	124661
ကူညီ	ကူညီ	-	0.960394 0.975704	124250
==========
anymalign running for bk-my...
။	။	-	0.986569 0.983817	38803872
မ	မ	-	0.931995 0.971002	764388
သူ	သူ	-	0.928052 0.974387	355210
သိ	သိ	-	0.970635 0.965926	260435
ရယ် ။	။	-	0.730127 0.005511	217364
ကို	ကို	-	0.799120 0.650722	184790
နင်	မင်း	-	0.838852 0.656342	181791
ငါ	ငါ	-	0.687902 0.953956	127460
ဒယ်ကောင်မငယ်	သူမ	-	0.924837 0.749586	126219
ကူညီ	ကူညီ	-	0.975406 0.960395	125249
==========
==========
anymalign running for my-ch...
။	.	-	0.550800 0.962547	4898081
။	a	-	0.073349 0.892812	652265
။	?	-	0.072672 0.888116	646250
မ	lo	-	0.710870 0.648172	317058
။	chu	-	0.026671 0.667900	237176
ကျွန်တော်	ka	-	0.655393 0.574250	205872
။	em ?	-	0.015765 0.864737	140192
မင်း	i	-	0.462554 0.391691	123821
။	nge ?	-	0.013911 0.739462	123709
။	i	-	0.013039 0.366792	115950
==========
anymalign running for ch-my...
.	။	-	0.962266 0.550989	4861713
a	။	-	0.891451 0.073066	644707
?	။	-	0.887856 0.072699	641467
lo	မ	-	0.645904 0.710082	313573
chu	။	-	0.670502 0.026631	234984
ka	ကျွန်တော်	-	0.575613 0.654233	205800
em ?	။	-	0.862325 0.015716	138674
i	မင်း	-	0.391248 0.460614	122731
nge ?	။	-	0.737955 0.013897	122620
i	။	-	0.367907 0.013080	115409
==========
==========
anymalign running for my-kc...
။	.	-	0.678513 0.926764	7100622
၊	,	-	0.978095 0.984578	1238437
။	ai	-	0.090114 0.681940	943039
။	ai .	-	0.081341 0.503383	851234
တစ်	langai	-	0.945418 0.902551	833063
လေ	le	-	0.973541 0.957634	814034
က	gaw	-	0.778737 0.842777	750771
နှုတ်ခမ်း	nten	-	0.998445 0.901410	521244
တယ် ။	ai .	-	0.764600 0.219810	371704
ဆံပင်	kara	-	0.997243 0.904475	331388
==========
anymalign running for kc-my...
.	။	-	0.927059 0.678136	7021784
,	၊	-	0.984625 0.978469	1226997
ai	။	-	0.682627 0.090448	936543
ai .	။	-	0.503552 0.081171	840492
langai	တစ်	-	0.902344 0.945150	821782
le	လေ	-	0.958069 0.974254	808783
gaw	က	-	0.840958 0.777645	738168
nten	နှုတ်ခမ်း	-	0.901671 0.998386	517861
ai .	တယ် ။	-	0.219959 0.766584	367140
kara	ဆံပင်	-	0.904086 0.997155	328420
==========
==========
anymalign running for my-ky...
။	꤯	-	0.887237 0.826904	7263664
တယ် ။	꤯	-	0.893036 0.041908	368130
ပါ ။	꤯	-	0.842750 0.034991	307367
ပါ တယ် ။	꤯	-	0.819678 0.032072	281730
။	?	-	0.029689 0.574869	243058
ကျေးဇူးတင်	ꤒꤟꤢꤧ꤬ꤙꤝꤤ	-	0.892745 0.802951	177783
မင်္ဂလာ	ꤒꤟꤢꤧ꤬ꤚꤛꤢꤙꤢꤧ꤬	-	0.933773 0.944617	119973
ကျွန်တော်	ꤠꤢ꤭	-	0.691810 0.543130	101454
ခင်ဗျား	ꤔꤟꤢꤧ꤬	-	0.657319 0.628934	92164
၊	.	-	0.410195 0.800333	83201
==========
anymalign running for ky-my...
==========
==========
anymalign running for my-mo...
။	။	-	0.959450 0.966333	26541786
၊	၊	-	0.991579 0.980987	346416
သူတို့	ဍေံတံ	-	0.954971 0.948727	317484
။	ဟာ ။	-	0.010591 0.722557	292971
ကျွန်တော်	အဲ	-	0.908313 0.733836	270095
။	ရ ။	-	0.008937 0.831193	247230
မ	ဟွံ	-	0.701916 0.811193	241097
သူမ	ဍေံ	-	0.853553 0.417596	185810
သူ	ဍေံ	-	0.889431 0.408525	181774
တယ် ။	။	-	0.845905 0.005537	152087
==========
anymalign running for mo-my...
။	။	-	0.966264 0.959389	26777026
၊	၊	-	0.980514 0.991639	348352
ဍေံတံ	သူတို့	-	0.948731 0.955547	319359
ဟာ ။	။	-	0.721593 0.010584	295398
အဲ	ကျွန်တော်	-	0.731417 0.906164	271840
ရ ။	။	-	0.831904 0.008964	250196
ဟွံ	မ	-	0.809750 0.700277	243125
ဍေံ	သူမ	-	0.420407 0.854268	189644
ဍေံ	သူ	-	0.408091 0.889675	184088
။	တယ် ။	-	0.005530 0.847787	153257
==========
==========
anymalign running for my-pk...
ကျွန်တော်	လီၫ	-	0.258474 0.095741	167350
ကို	လီၫ	-	0.258300 0.095684	167250
မင်း	န	-	0.270942 0.208413	158294
ကျွန်တော်	ယ	-	0.206492 0.242287	133694
မ	လီၫ	-	0.199223 0.069777	121967
မင်း	လီၫ	-	0.185687 0.062064	108485
မ	အ့ၬ	-	0.132485 0.252006	81109
ကို	နီၪ	-	0.121490 0.204357	78665
ခင်ဗျား	န	-	0.254855 0.101644	77201
တယ်	လီၫ	-	0.403118 0.039184	68491
==========
anymalign running for pk-my...
လီၫ	ကို	-	0.096434 0.259786	168649
လီၫ	ကျွန်တော်	-	0.095306 0.258297	166676
န	မင်း	-	0.208791 0.270995	158878
ယ	ကျွန်တော်	-	0.242847 0.207523	133912
လီၫ	မ	-	0.069186 0.198030	120996
လီၫ	မင်း	-	0.061823 0.184417	108119
အ့ၬ	မ	-	0.247872 0.130089	79484
နီၪ	ကို	-	0.204065 0.121078	78602
န	ခင်ဗျား	-	0.102394 0.256470	77916
လီၫ	တယ်	-	0.039007 0.401906	68218
==========
==========
anymalign running for my-po...
ငါ	ခွေ	-	0.940065 0.817239	3470848
မင်း	နာꩻ	-	0.927322 0.780573	2449266
သူမ	ဝွေꩻမူႏ	-	0.972148 0.871537	1560828
သူ	ဝွေꩻ	-	0.918356 0.648963	679938
သူတို့	ဝွေꩻသီး	-	0.939142 0.703413	590280
အဲဒါ	နဝ်ꩻနဝ်ꩻ	-	0.934063 0.571845	492421
ငါတို့	နီ	-	0.918040 0.653709	434532
ဘယ်လောက်	တခွိုင်းမုဲင်ꩻ	-	0.937411 0.989127	355138
အဲဒါ ကို	နဝ်ꩻနဝ်ꩻ	-	0.732895 0.161131	138751
လဲ	ဟောင်း	-	0.621889 0.242628	120073
==========
anymalign running for po-my...
ခွေ	ငါ	-	0.817655 0.940130	3554526
နာꩻ	မင်း	-	0.781191 0.927023	2509907
ဝွေꩻမူႏ	သူမ	-	0.871262 0.972353	1598933
ဝွေꩻ	သူ	-	0.650389 0.918461	698967
ဝွေꩻသီး	သူတို့	-	0.703990 0.938879	602709
နဝ်ꩻနဝ်ꩻ	အဲဒါ	-	0.571797 0.933537	501569
နီ	ငါတို့	-	0.654595 0.917763	444080
တခွိုင်းမုဲင်ꩻ	ဘယ်လောက်	-	0.988966 0.935008	360498
နဝ်ꩻနဝ်ꩻ	အဲဒါ ကို	-	0.161127 0.731709	141337
ဟောင်း	လဲ	-	0.243084 0.623686	123604
==========
==========
anymalign running for my-rk...
။	။	-	0.947494 0.979456	13939587
မ	မ	-	0.994976 0.992785	2134187
ကို	ကို	-	0.985632 0.955503	1330767
ကျွန်တော်	ကျွန်တော်	-	0.991009 0.989268	1205789
သူ	သူ	-	0.993121 0.985888	691986
သူမ	ထိုမချေ	-	0.978503 0.982116	452224
မင်း	မင်း	-	0.977474 0.668249	437359
ဘယ်သူ့	ဇာသူ့	-	0.997625 0.994163	404992
ပြော	ပြော	-	0.996008 0.990616	392188
က	က	-	0.990870 0.955710	364096
==========
anymalign running for rk-my...
။	။	-	0.979497 0.947564	14128610
မ	မ	-	0.992522 0.995109	2171746
ကို	ကို	-	0.955835 0.985726	1341057
ကျွန်တော်	ကျွန်တော်	-	0.989367 0.990776	1222079
သူ	သူ	-	0.986020 0.993086	702338
ထိုမချေ	သူမ	-	0.982397 0.978273	462871
မင်း	မင်း	-	0.667598 0.977195	440877
ဇာသူ့	ဘယ်သူ့	-	0.994642 0.997637	412834
ပြော	ပြော	-	0.990127 0.995747	397527
က	က	-	0.955194 0.990982	369789
==========
==========
anymalign running for my-rw...
။	.	-	0.905064 0.919042	15943633
၊	,	-	0.986045 0.985729	2038084
တစ်	TÌQ	-	0.928386 0.967337	1317023
ခင်ဗျား	NÀ	-	0.938745 0.912528	741053
တယ် ။	.	-	0.745392 0.035502	615888
ကို	KÀQ	-	0.891779 0.907811	507961
ကျွန်တော်	NGÀ	-	0.869770 0.700430	395600
လား	MÁ ?	-	0.718140 0.612402	352619
သူတို့	ÀNGMÀQ	-	0.999887 0.999465	274455
က	NØ̀	-	0.655005 0.492713	244176
==========
anymalign running for rw-my...
.	။	-	0.919001 0.905315	15988619
,	၊	-	0.985762 0.986086	2052609
TÌQ	တစ်	-	0.967306 0.927672	1318200
NÀ	ခင်ဗျား	-	0.912771 0.939113	739298
.	တယ် ။	-	0.035480 0.745115	617273
KÀQ	ကို	-	0.907378 0.890684	509011
NGÀ	ကျွန်တော်	-	0.699210 0.868815	396919
MÁ ?	လား	-	0.613041 0.717785	353215
ÀNGMÀQ	သူတို့	-	0.999369 0.999796	273842
NØ̀	က	-	0.489795 0.651908	243390
==========
==========
anymalign running for my-sh...
။	။	-	0.985369 0.976995	46154966
၊	၊	-	0.984670 0.979815	361874
သူမ	မၼ်းၼၢင်း	-	0.974736 0.953074	230299
တယ် ။	။	-	0.843193 0.003062	144659
။	ႁႃႉ ။	-	0.002862 0.764996	134035
။	ယဝ်ႉ ။	-	0.001632 0.825243	76453
။	ယူႇ ။	-	0.001581 0.727475	74070
မ	ဢမ်ႇ	-	0.720965 0.725711	62840
ကျွန်တော်	ၵဝ်ၶႃႈ	-	0.571491 0.802058	59718
ကျေးဇူးပြုပြီး	ၶႅၼ်းတေႃႈ	-	0.976965 0.978365	59377
==========
anymalign running for sh-my...
။	။	-	0.976843 0.985338	46553303
၊	၊	-	0.980295 0.984253	365013
မၼ်းၼၢင်း	သူမ	-	0.953325 0.974733	231311
။	တယ် ။	-	0.003043 0.842071	145029
ႁႃႉ ။	။	-	0.766158 0.002870	135610
ယဝ်ႉ ။	။	-	0.826290 0.001648	77858
ယူႇ ။	။	-	0.727021 0.001569	74122
ဢမ်ႇ	မ	-	0.722236 0.721595	63439
ၶႅၼ်းတေႃႈ	ကျေးဇူးပြုပြီး	-	0.977769 0.975447	60388
ၵဝ်ၶႃႈ	ကျွန်တော်	-	0.797225 0.573876	60102
==========
==========
anymalign running for my-sk...
မင်း	န	-	0.805203 0.577472	403954
သူတို့	အဝဲသ့ၣ်	-	0.946153 0.671863	401309
သူ	အဝဲ	-	0.876276 0.469965	342070
မ	တ	-	0.725453 0.727954	324181
ကျွန်တော်	ယ	-	0.737231 0.522187	322366
ခင်ဗျား	န	-	0.687929 0.164350	114966
သူမ	အဝဲ	-	0.499618 0.142692	103860
ငါ	ယ	-	0.762779 0.106120	65512
ကို	န့ၣ်	-	0.241173 0.281070	58648
တယ်	လီၤ	-	0.471682 0.221792	58632
==========
anymalign running for sk-my...
```

