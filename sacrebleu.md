# sacreBLEU

## Installation

```
ye@lst-hpc3090:~/exp/eval_power$ pip install sacrebleu --break-system-packages
Defaulting to user installation because normal site-packages is not writeable
Collecting sacrebleu
  Downloading sacrebleu-2.5.1-py3-none-any.whl.metadata (51 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 51.8/51.8 kB 1.1 MB/s eta 0:00:00
Collecting portalocker (from sacrebleu)
  Downloading portalocker-3.2.0-py3-none-any.whl.metadata (8.7 kB)
Requirement already satisfied: regex in /home/ye/.local/lib/python3.12/site-packages (from sacrebleu) (2024.11.6)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/.local/lib/python3.12/site-packages (from sacrebleu) (0.9.0)
Requirement already satisfied: numpy>=1.17 in /home/ye/.local/lib/python3.12/site-packages (from sacrebleu) (2.1.3)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from sacrebleu) (0.4.6)
Requirement already satisfied: lxml in /usr/lib/python3/dist-packages (from sacrebleu) (5.2.1)
Downloading sacrebleu-2.5.1-py3-none-any.whl (104 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 104.1/104.1 kB 5.0 MB/s eta 0:00:00
Downloading portalocker-3.2.0-py3-none-any.whl (22 kB)
Installing collected packages: portalocker, sacrebleu
Successfully installed portalocker-3.2.0 sacrebleu-2.5.1
ye@lst-hpc3090:~/exp/eval_power$
```

## --help  


```
ye@lst-hpc3090:~/exp/eval_power$ sacrebleu --help  
usage: sacrebleu [-h] [--citation] [--list] [--test-set TEST_SET]
                 [--language-pair LANGPAIR] [--origlang ORIGLANG]
                 [--subset SUBSET] [--download DOWNLOAD]
                 [--echo ECHO [ECHO ...]] [--input [INPUT ...]]
                 [--num-refs NUM_REFS] [--encoding ENCODING]
                 [--metrics {bleu,chrf,ter} [{bleu,chrf,ter} ...]]
                 [--sentence-level] [--smooth-method {none,floor,add-k,exp}]
                 [--smooth-value BLEU_SMOOTH_VALUE]
                 [--tokenize {none,zh,13a,intl,char,ja-mecab,ko-mecab,spm,flores101,flores200}]
                 [--lowercase] [--force] [--chrf-char-order CHRF_CHAR_ORDER]
                 [--chrf-word-order CHRF_WORD_ORDER] [--chrf-beta CHRF_BETA]
                 [--chrf-whitespace] [--chrf-lowercase] [--chrf-eps-smoothing]
                 [--ter-case-sensitive] [--ter-asian-support] [--ter-no-punct]
                 [--ter-normalized] [--confidence]
                 [--confidence-n CONFIDENCE_N] [--paired-ar | --paired-bs]
                 [--paired-ar-n PAIRED_AR_N] [--paired-bs-n PAIRED_BS_N]
                 [--paired-jobs PAIRED_JOBS] [--quiet] [--short]
                 [--score-only] [--width WIDTH] [--detail] [--no-color]
                 [--format {json,text,latex}] [--version]
                 [refs ...]

sacreBLEU: Hassle-free computation of shareable BLEU scores.
Quick usage: score your detokenized output against WMT'14 EN-DE:
    cat output.detok.de | sacrebleu -t wmt14 -l en-de

positional arguments:
  refs                  Optional list of references. If given, it should
                        preceed the -i/--input argument.

options:
  -h, --help            show this help message and exit
  --citation, --cite    Dump the bibtex citation and quit.
  --list                Print a list of all available test sets.
  --test-set TEST_SET, -t TEST_SET
                        The test set to use (see also --list) or a comma-
                        separated list of test sets to be concatenated.
  --language-pair LANGPAIR, -l LANGPAIR
                        Source-target language pair (2-char ISO639-1 codes).
  --origlang ORIGLANG, -ol ORIGLANG
                        Use a subset of sentences with a given original
                        language (2-char ISO639-1 codes), "non-" prefix means
                        negation.
  --subset SUBSET       Use a subset of sentences whose document annotation
                        matches a given regex (see SUBSETS in the source
                        code).
  --download DOWNLOAD   Download a test set and quit.
  --echo ECHO [ECHO ...]
                        Output the source (src), reference (ref), or other
                        available field (docid, ref:A, ref:1 for example) to
                        STDOUT and quit. You can get available fields with
                        options `--list` and `-t`For example: `sacrebleu -t
                        wmt21 --list`. If multiple fields are given, they are
                        outputted with tsv format in the order they are
                        given.You can also use `--echo all` to output all
                        available fields.
  --input [INPUT ...], -i [INPUT ...]
                        Read input from file(s) instead of STDIN.
  --num-refs NUM_REFS, -nr NUM_REFS
                        Split the reference stream on tabs, and expect this
                        many references. (Default: 1)
  --encoding ENCODING, -e ENCODING
                        Open text files with specified encoding (Default:
                        utf-8)
  --metrics {bleu,chrf,ter} [{bleu,chrf,ter} ...], -m {bleu,chrf,ter} [{bleu,chrf,ter} ...]
                        Space-delimited list of metrics to compute (Default:
                        bleu)
  --sentence-level, -sl
                        Compute metric for each sentence.
  --version, -V         show program's version number and exit

BLEU related arguments:
  --smooth-method {none,floor,add-k,exp}, -s {none,floor,add-k,exp}
                        Smoothing method: exponential decay, floor (increment
                        zero counts), add-k (increment num/denom by k for
                        n>1), or none. (Default: exp)
  --smooth-value BLEU_SMOOTH_VALUE, -sv BLEU_SMOOTH_VALUE
                        The smoothing value. Only valid for floor and add-k.
                        (Defaults: floor: 0.1, add-k: 1)
  --tokenize {none,zh,13a,intl,char,ja-mecab,ko-mecab,spm,flores101,flores200}, -tok {none,zh,13a,intl,char,ja-mecab,ko-mecab,spm,flores101,flores200}
                        Tokenization method to use for BLEU. If not provided,
                        defaults to `zh` for Chinese, `ja-mecab` for Japanese,
                        `ko-mecab` for Korean and `13a` (mteval) otherwise.
  --lowercase, -lc      If True, enables case-insensitivity. (Default: False)
  --force               Insist that your tokenized input is actually
                        detokenized.

chrF related arguments:
  --chrf-char-order CHRF_CHAR_ORDER, -cc CHRF_CHAR_ORDER
                        Character n-gram order. (Default: 6)
  --chrf-word-order CHRF_WORD_ORDER, -cw CHRF_WORD_ORDER
                        Word n-gram order (Default: 0). If equals to 2, the
                        metric is referred to as chrF++.
  --chrf-beta CHRF_BETA
                        Determine the importance of recall w.r.t precision.
                        (Default: 2)
  --chrf-whitespace     Include whitespaces when extracting character n-grams.
                        (Default: False)
  --chrf-lowercase      Enable case-insensitivity. (Default: False)
  --chrf-eps-smoothing  Enables epsilon smoothing similar to chrF++.py, NLTK
                        and Moses; instead of effective order smoothing.
                        (Default: False)

TER related arguments (The defaults replicate TERCOM's behavior):
  --ter-case-sensitive  Enables case sensitivity. (Default: False)
  --ter-asian-support   Enables special treatment of Asian characters.
                        (Default: False)
  --ter-no-punct        Removes punctuation. (Default: False)
  --ter-normalized      Applies basic normalization and tokenization.
                        (Default: False)

Confidence interval (CI) estimation for single-system evaluation:
  --confidence, -ci     Report confidence interval using bootstrap resampling.
  --confidence-n CONFIDENCE_N, -cin CONFIDENCE_N
                        Set the number of bootstrap resamples for CI
                        estimation (Default: 1000).

Paired significance testing for multi-system evaluation:
  --paired-ar, -par     Perform paired test using approximate randomization
                        (AR). This option is mutually exclusive with --paired-
                        bs (Default: False).
  --paired-bs, -pbs     Perform paired test using bootstrap resampling. This
                        option is mutually exclusive with --paired-ar
                        (Default: False).
  --paired-ar-n PAIRED_AR_N, -parn PAIRED_AR_N
                        Number of trials for approximate randomization test
                        (Default: 10000).
  --paired-bs-n PAIRED_BS_N, -pbsn PAIRED_BS_N
                        Number of bootstrap resamples for paired bootstrap
                        resampling test (Default: 1000).
  --paired-jobs PAIRED_JOBS, -j PAIRED_JOBS
                        If 0, launches as many workers as the number of
                        systems. If > 0, sets the number of workers manually.
                        This feature is currently not supported on Windows.

Reporting related arguments:
  --quiet, -q           Suppress verbose messages.
  --short, -sh          Produce a shorter (less human readable) signature.
  --score-only, -b      Print only the computed score.
  --width WIDTH, -w WIDTH
                        Floating point width (Default: 1).
  --detail, -d          Print detailed information (split test sets based on
                        origlang).
  --no-color, -nc       Disable the occasional use of terminal colors.
  --format {json,text,latex}, -f {json,text,latex}
                        Set the output format. `latex` is only valid for
                        multi-system mode whereas `json` and `text` apply to
                        single-system mode only. This flag is overridden if
                        the SACREBLEU_FORMAT environment variable is set to
                        one of the valid choices (Default: json).

```

## Example Usage


အလွယ်ဆုံး အသုံးပြုပုံက အောက်ပါအတိုင်း...  

```
sacrebleu reference.txt -i hypothesis.txt -m bleu -b -w 4
```

- `reference.txt`: File with reference translations (one per line)
- `hypothesis.txt`: File with system translations (one per line)
- `-m bleu`: Compute BLEU score (default)
- `-b`: Print only the BLEU score (no verbose output)
- `-w 4`: Use 4 decimal places for the score

အချိန်ရတဲ့အခါမှာ MT experiment တချို့က ရလဒ်တွေနဲ့ အသုံးပြုပုံကို ရှင်းပြမယ်။  

```

```

```

```

```

```

```

```

```

```

```

```

```


```

