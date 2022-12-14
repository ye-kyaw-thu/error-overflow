# Testing Sentence Tokenization for Burmese with Updated Data

Thura Aung updated/cleaned the corpus and thus, we need to run all the experiments again with the updated data.  

## Move the Old Data

```
root@48e31407fc14:/home/ye/exp/mysent# mv data-{sent,para} ./old-exp1-data/
root@48e31407fc14:/home/ye/exp/mysent# tree ./old-exp1-data/
./old-exp1-data/
|-- data-para
|   |-- combind-process
|   |   |-- test.my-tg
|   |   |-- test.my-tg.shuf
|   |   |-- test.my.combi
|   |   |-- test.my.final
|   |   |-- test.tg.combi
|   |   |-- test.tg.final
|   |   |-- train.my-tg
|   |   |-- train.my-tg.shuf
|   |   |-- train.my.combi
|   |   |-- train.my.final
|   |   |-- train.tg.combi
|   |   |-- train.tg.final
|   |   |-- valid.my-tg
|   |   |-- valid.my-tg.shuf
|   |   |-- valid.my.combi
|   |   |-- valid.my.final
|   |   |-- valid.tg.combi
|   |   `-- valid.tg.final
|   |-- paragraph.txt
|   |-- paragraph.txt.error
|   |-- preprocessing
|   |   |-- mk-wordtag2.pl
|   |   |-- para.tag
|   |   |-- para.word
|   |   |-- paragraph.txt
|   |   |-- paragraph.txt.shuf
|   |   |-- test.my
|   |   |-- test.tg
|   |   |-- train.my
|   |   |-- train.tg
|   |   |-- valid.my
|   |   `-- valid.tg
|   |-- test.my
|   |-- test.tg
|   |-- train.my
|   |-- train.tg
|   |-- valid.my
|   |-- valid.tg
|   `-- vocab
|       |-- all.my
|       |-- all.tg
|       |-- vocab.my.yml
|       `-- vocab.tg.yml
`-- data-sent
    |-- test.my
    |-- test.tg
    |-- train.my
    |-- train.tg
    |-- valid.my
    |-- valid.tg
    `-- vocab
        |-- all.my
        |-- all.tg
        |-- vocab.my.yml
        `-- vocab.tg.yml

6 directories, 51 files
root@48e31407fc14:/home/ye/exp/mysent#
```

## Prepare New Dataset

Copy data to the GPU machine:  

```
C:\Users\801680>scp [12Dec]mySentence_data_results.zip ye@10.222.xx.xx:/home/ye/
ye@10.222.xx.xx's password:
[12Dec]mySentence_data_results.zip                                                          100%   10MB   2.7MB/s   00:03

C:\Users\801680>
```

Check on server side:  

```
root@48e31407fc14:/home/ye/exp/mysent/tmp# mv /home/ye/\[12Dec\]mySentence_data_results.zip .
root@48e31407fc14:/home/ye/exp/mysent/tmp# ls
'[12Dec]mySentence_data_results.zip'
root@48e31407fc14:/home/ye/exp/mysent/tmp# unzip \[12Dec\]mySentence_data_results.zip
Archive:  [12Dec]mySentence_data_results.zip
  inflating: [12Dec]Results_mySentence.pdf
  inflating: clean-data-rdy2train.zip
root@48e31407fc14:/home/ye/exp/mysent/tmp# ls
'[12Dec]Results_mySentence.pdf'  '[12Dec]mySentence_data_results.zip'   clean-data-rdy2train.zip
root@48e31407fc14:/home/ye/exp/mysent/tmp# unzip ./clean-data-rdy2train.zip
Archive:  ./clean-data-rdy2train.zip
   creating: clean-data-rdy2train/
   creating: clean-data-rdy2train/data-sent/
  inflating: clean-data-rdy2train/data-sent/test.my~
  inflating: clean-data-rdy2train/data-sent/train.txt~
   creating: clean-data-rdy2train/data-sent/sent_tagged/
  inflating: clean-data-rdy2train/data-sent/sent_tagged/test.tagged
  inflating: clean-data-rdy2train/data-sent/sent_tagged/train.tagged
  inflating: clean-data-rdy2train/data-sent/sent_tagged/valid.tagged
   creating: clean-data-rdy2train/data-sent/sent_parallel/
  inflating: clean-data-rdy2train/data-sent/sent_parallel/train.my
  inflating: clean-data-rdy2train/data-sent/sent_parallel/test.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/valid.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/valid.my
  inflating: clean-data-rdy2train/data-sent/sent_parallel/train.tg
  inflating: clean-data-rdy2train/data-sent/sent_parallel/test.my
   creating: clean-data-rdy2train/data-sent+para/
   creating: clean-data-rdy2train/data-sent+para/sent+para_tagged/
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/valid.tagged
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/train.tagged
  inflating: clean-data-rdy2train/data-sent+para/sent+para_tagged/test.tagged
   creating: clean-data-rdy2train/data-sent+para/sent+para_parallel/
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/valid.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/valid.my
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/train.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/train.my
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/test.tg
  inflating: clean-data-rdy2train/data-sent+para/sent+para_parallel/test.my
root@48e31407fc14:/home/ye/exp/mysent/tmp#
```

copied sentence and parallel data to the folder called by the NMT framework marian:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-sent# cp ../tmp/clean-data-rdy2train/data-sent/sent_parallel/* .
root@48e31407fc14:/home/ye/exp/mysent/data-sent# ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
root@48e31407fc14:/home/ye/exp/mysent/data-sent# wc *
    4712      448   919423 test.my
    4712    63622   127244 test.tg
   40000     3688  7868628 train.my
   40000   543541  1087082 train.tg
    2414      257   466536 valid.my
    2414    32315    64630 valid.tg
   94252   643871 10533543 total
root@48e31407fc14:/home/ye/exp/mysent/data-sent#
```

for sent+para data:  

```
root@48e31407fc14:/home/ye/exp/mysent/data-para# cp ../tmp/clean-data-rdy2train/data-sent+para/sent+para_parallel/* .
root@48e31407fc14:/home/ye/exp/mysent/data-para# wc *
    5512      758  1380183 test.my
    5512    96632   193264 test.tg
   47002     6031 11944271 train.my
   47002   834243  1668486 train.tg
    3079      518   877576 valid.my
    3079    61782   123564 valid.tg
  111186   999964 16187344 total
root@48e31407fc14:/home/ye/exp/mysent/data-para#
```

## make Vocab

for sent only dataset:  

```

```

for sent+paragraph dataset:  

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

```

```

```

```
