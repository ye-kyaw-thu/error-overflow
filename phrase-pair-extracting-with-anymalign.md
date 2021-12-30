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

## for Myanmar-Beik


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


