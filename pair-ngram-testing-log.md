# Pair ngram testing log

## Env Preparation

```
(base) rnd@gpu:~/tool/pair_ngram$ ls
AUTHORS  CONTRIBUTING  README.md  environment.yml  error.py  predict.py  predict_lexicon.py  run.sh  split.py  train.py
(base) rnd@gpu:~/tool/pair_ngram$ conda env create -f environment.yml
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.3.1

Please update conda by running

    $ conda update -n base -c defaults conda



Downloading and Extracting Packages
libpng-1.6.39        | 276 KB    | ################################################################################### | 100% 
python_abi-3.9       | 6 KB      | ################################################################################### | 100% 
xorg-kbproto-1.0.7   | 27 KB     | ################################################################################### | 100% 
setuptools-67.6.1    | 567 KB    | ################################################################################### | 100% 
libffi-3.3           | 51 KB     | ################################################################################### | 100% 
libsqlite-3.40.0     | 791 KB    | ################################################################################### | 100% 
openfst-1.8.2        | 7.4 MB    | ################################################################################### | 100% 
libtool-2.4.7        | 402 KB    | ################################################################################### | 100% 
zlib-1.2.13          | 92 KB     | ################################################################################### | 100% 
libglib-2.68.4       | 3.0 MB    | ################################################################################### | 100% 
libtiff-4.4.0        | 473 KB    | ################################################################################### | 100% 
ld_impl_linux-64-2.4 | 688 KB    | ################################################################################### | 100% 
gts-0.7.6            | 411 KB    | ################################################################################### | 100% 
fribidi-1.0.10       | 112 KB    | ################################################################################### | 100% 
libexpat-2.5.0       | 76 KB     | ################################################################################### | 100% 
gtk2-2.24.33         | 7.3 MB    | ################################################################################### | 100% 
gettext-0.21.1       | 4.1 MB    | ################################################################################### | 100% 
librsvg-2.52.2       | 5.2 MB    | ################################################################################### | 100% 
xorg-xproto-7.0.31   | 73 KB     | ################################################################################### | 100% 
libwebp-1.2.4        | 87 KB     | ################################################################################### | 100% 
_openmp_mutex-4.5    | 23 KB     | ################################################################################### | 100% 
font-ttf-ubuntu-0.83 | 1.9 MB    | ################################################################################### | 100% 
xorg-libice-1.0.10   | 58 KB     | ################################################################################### | 100% 
harfbuzz-3.0.0       | 2.0 MB    | ################################################################################### | 100% 
libblas-3.9.0        | 13 KB     | ################################################################################### | 100% 
font-ttf-source-code | 684 KB    | ################################################################################### | 100% 
libstdcxx-ng-12.2.0  | 4.3 MB    | ################################################################################### | 100% 
libzlib-1.2.13       | 64 KB     | ################################################################################### | 100% 
gdk-pixbuf-2.42.6    | 609 KB    | ################################################################################### | 100% 
ngram-1.3.14         | 3.4 MB    | ################################################################################### | 100% 
libiconv-1.17        | 1.4 MB    | ################################################################################### | 100% 
font-ttf-dejavu-sans | 388 KB    | ################################################################################### | 100% 
freetype-2.12.1      | 611 KB    | ################################################################################### | 100% 
zstd-1.5.2           | 410 KB    | ################################################################################### | 100% 
libgcc-ng-12.2.0     | 931 KB    | ################################################################################### | 100% 
libgd-2.3.3          | 279 KB    | ################################################################################### | 100% 
libwebp-base-1.2.4   | 404 KB    | ################################################################################### | 100% 
libopenblas-0.3.21   | 10.1 MB   | ################################################################################### | 100% 
libxml2-2.9.12       | 772 KB    | ################################################################################### | 100% 
cairo-1.16.0         | 1.5 MB    | ################################################################################### | 100% 
libcblas-3.9.0       | 13 KB     | ################################################################################### | 100% 
xz-5.2.6             | 409 KB    | ################################################################################### | 100% 
tzdata-2023c         | 115 KB    | ################################################################################### | 100% 
xorg-xextproto-7.3.0 | 30 KB     | ################################################################################### | 100% 
font-ttf-inconsolata | 94 KB     | ################################################################################### | 100% 
numpy-1.21.2         | 6.2 MB    | ################################################################################### | 100% 
pthread-stubs-0.4    | 5 KB      | ################################################################################### | 100% 
liblapack-3.9.0      | 13 KB     | ################################################################################### | 100% 
tk-8.6.12            | 3.3 MB    | ################################################################################### | 100% 
libxcb-1.13          | 391 KB    | ################################################################################### | 100% 
readline-8.2         | 275 KB    | ################################################################################### | 100% 
xorg-libsm-1.2.3     | 26 KB     | ################################################################################### | 100% 
libgomp-12.2.0       | 455 KB    | ################################################################################### | 100% 
giflib-5.2.1         | 76 KB     | ################################################################################### | 100% 
fonts-conda-forge-1  | 4 KB      | ################################################################################### | 100% 
libdeflate-1.14      | 81 KB     | ################################################################################### | 100% 
python-3.9.5         | 27.4 MB   | ################################################################################### | 100% 
xorg-libxau-1.0.9    | 13 KB     | ################################################################################### | 100% 
icu-68.2             | 13.1 MB   | ################################################################################### | 100% 
atk-1.0-2.36.0       | 560 KB    | ################################################################################### | 100% 
expat-2.5.0          | 134 KB    | ################################################################################### | 100% 
xorg-libxext-1.3.4   | 49 KB     | ################################################################################### | 100% 
jpeg-9e              | 235 KB    | ################################################################################### | 100% 
xorg-libxdmcp-1.1.3  | 19 KB     | ################################################################################### | 100% 
pip-23.0.1           | 1.3 MB    | ################################################################################### | 100% 
pynini-2.1.5         | 1.9 MB    | ################################################################################### | 100% 
lerc-4.0.0           | 275 KB    | ################################################################################### | 100% 
graphviz-2.49.1      | 3.9 MB    | ################################################################################### | 100% 
baumwelch-0.3.7      | 362 KB    | ################################################################################### | 100% 
_libgcc_mutex-0.1    | 3 KB      | ################################################################################### | 100% 
pango-1.48.10        | 403 KB    | ################################################################################### | 100% 
xorg-libx11-1.8.4    | 810 KB    | ################################################################################### | 100% 
libuuid-2.38.1       | 33 KB     | ################################################################################### | 100% 
xorg-libxrender-0.9. | 32 KB     | ################################################################################### | 100% 
ncurses-6.3          | 1002 KB   | ################################################################################### | 100% 
graphite2-1.3.13     | 102 KB    | ################################################################################### | 100% 
pixman-0.40.0        | 627 KB    | ################################################################################### | 100% 
sqlite-3.40.0        | 801 KB    | ################################################################################### | 100% 
openssl-1.1.1t       | 1.9 MB    | ################################################################################### | 100% 
xorg-renderproto-0.1 | 9 KB      | ################################################################################### | 100% 
fontconfig-2.14.2    | 266 KB    | ################################################################################### | 100% 
pcre-8.45            | 253 KB    | ################################################################################### | 100% 
fonts-conda-ecosyste | 4 KB      | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: - b''
- b''
done
#
# To activate this environment, use
#
#     $ conda activate pair_ngram
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) rnd@gpu:~/tool/pair_ngram$ 
```

## Activate

```
(base) rnd@gpu:~/tool/pair_ngram$ conda activate pair_ngram
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Create Temp Directory

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ readonly TEMPDATA="$(mktemp --directory)"
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ echo $TEMPDATA 
/tmp/tmp.Msn7f6i7pz
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Prepare a Shell Script for Downloading Data

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cat ./download-data.sh 
#!/bin/bash

curl \
--output "${TEMPDATA}/pairs.tsv" \
"https://gist.githubusercontent.com/kylebgorman/01adff5799edb0edf3bcce20187c833a/raw/fb0e66d31e021fca7adec4c2104ffea0e879f2e4/pairs.tsv"

curl \
--output "${TEMPDATA}/lexicon.txt" \
"http://cvsweb.netbsd.org/bsdweb.cgi/src/share/dict/web2?rev=1.54"
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Run the Script

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ sudo ./download-data.sh 
[sudo] password for rnd: 
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  807k  100  807k    0     0  2905k      0 --:--:-- --:--:-- --:--:-- 2894k
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2435k    0 2435k    0     0   146k      0 --:--:--  0:00:16 --:--:--  138k
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Backup The Data and Check

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ ./backup-data.sh 
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  807k  100  807k    0     0  1409k      0 --:--:-- --:--:-- --:--:-- 1409k
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2435k    0 2435k    0     0   160k      0 --:--:--  0:00:15 --:--:--  148k
```

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ ls ./data-bk/
lexicon.txt  pairs.tsv
```

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cd data-bk/
(pair_ngram) rnd@gpu:~/tool/pair_ngram/data-bk$ wc *
 235974  235974 2493871 lexicon.txt
  26381   65954  827013 pairs.tsv
 262355  301928 3320884 total
```

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram/data-bk$ head lexicon.txt 
A
a
aa
aal
aalii
aam
Aani
aardvark
aardwolf
Aaron
```

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram/data-bk$ head pairs.tsv 
フルーツサラダ	fruits salad
クリッパーチップ	clipper chip
ライフサイクル	life cycle
ボイストレーニング	voice training
オップアート	op art
ノーズコーン	nose cone
インカムタックス	income tax
エグゼクティブフロア	executive floor
ウェブフォーム	web form
ハムサンド	ham sand
```

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram/data-bk$ tail pairs.tsv 
ブルマーズ	bloomers
スパーテル	spatula
ドルフィン	dolphin
リットル	liter
ロケート	locate
スカイラーク	skylark
ウオッカ	vodka
ラゲッジ	luggage
コレスポンデント	correspondent
メード	maid
(pair_ngram) rnd@gpu:~/tool/pair_ngram/data-bk$
```

## Data Splitting

temp ဖိုလ်ဒါအောက်မှာ အလုပ်လုပ်ရတာ အရမ်းအဆင်ပြေကြီး မဟုတ်လို့ backup ဆိုပြီး ကူးထားတဲ့ data path ကိုပဲ ပြောင်းသုံးခဲ့ ...  
```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ python -m split --seed 10037 --input ./data-bk/pairs.tsv --train ./data-bk/train.tsv --dev ./data-bk/dev.tsv --test ./data-bk/test.tsv
INFO:	Total set:	26,381 lines
INFO:	Train set:	21,104 lines
INFO:	Dev set:	2,638 lines
INFO:	Test set:	2,639 lines
(pair_ngram) rnd@gpu:~/tool/pair_ngram$
```

## Training 

Original README ဖိုင်မှာ က --batch-size, --max-iters ဆိုပြီး လုပ်ထားလို့ Error ပေးတာကိုလည်း ပြင်ဆင်ခဲ့။  
Prepared a shell script as follows:  

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cat ./run-train.sh 
#!/bin/bash

python -m train \
--seed 10037 \
--batch_size 128 \
--max_iters 10 \
--order 6 \
--size 100000 \
--tsv ./data-bk/train.tsv \
--fst ./data-bk/plm.fst


(pair_ngram) rnd@gpu:~/tool/pair_ngram$
```

Start training ...  

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ time ./run-train.sh 
INFO:   Compiling FARs
INFO:   Compiling covering grammar
INFO:   Training aligner
INFO:   Aligning data
INFO:   Encoding alignments
INFO:   Compiling pair n-gram model

real    2m47.816s
user    43m21.813s
sys     0m3.468s
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Prediction

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cat run-predict.sh 
#!/bin/bash

python -m predict \
--rule ./data-bk/plm.fst \
--input <(cut -f1 ./data-bk/dev.tsv) \
--output ./data-bk/hypo.txt
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ time ./run-predict.sh 

real    0m39.231s
user    7m16.964s
sys     0m1.493s
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ 
```

## Evaluation

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cat ./run-score.sh 
#!/bin/bash

python -m error \
--gold <(cut -f2 ./data-bk/dev.tsv) \
--hypo ./data-bk/hypo.txt
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ ./run-score.sh 
Error rate:     40.14
(pair_ngram) rnd@gpu:~/tool/pair_ngram$
```

Eror rate က များတယ်။  

## Prediction with Lexicon Constraint

Preparing a new script:  

```
(pair_ngram) rnd@gpu:~/tool/pair_ngram$ cat ./predict-score-with-lexicon-constraint.sh 
#!/bin/bash

## running with lexicon constraint

python -m predict_lexicon \
--rule ./data-bk/plm.fst \
--lexicon ./data-bk/lexicon.txt \
--input <(cut -f1 ./data-bk/dev.tsv) \
--output ./data-bk/hypo-lexicon.txt
  
python -m error \
--gold <(cut -f2 ./data-bk/dev.tsv) \
--hypo ./data-bk/hypo-lexicon.txt
(pair_ngram) rnd@gpu:~/tool/pair_ngram$
```

predict and scoring or evaluation:  

```

```

```

```

```

```

