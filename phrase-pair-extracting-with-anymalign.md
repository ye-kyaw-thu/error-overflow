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

## Phrase Pair Extraction 

