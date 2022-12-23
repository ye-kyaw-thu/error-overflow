# Seq2Seq Model Experiments

## Experimental Setting

For this time, I will build Seq2Seq NMT model for Khmer spelling checking...  

Note: I need to build 3 models and they are as follows:  

1. Seq2Seq Model with Dictionary or Word level 
2. Seq2Seq Model with Sentence-Edit1 
3. Seq2Seq Model with Sentence-Edit2

For the Evaluation, I used three test-sets as follows:  

1. normal data
2. edit distance-1 data
3. edit distance-2 data

In details:  

for Dictionary (i.e. word level model) ...  
1. dictionary test-data
2. edit distance-1 word data
3. edit distance-2 word data

for Sentencce ...  
1. manually collected sentence level spelling error data
2. edit distance-1 sentence data
3. edit distance-3 sentence data 


## Revist the Experimental Setting of the Previous 

```
I will train two models. One is training with edit-distance 1 errors and another is edit-distance 2 errors.  
For the testing, I will use three test-sets. They are as follows:  

edit-1 test-set (test set of Khmer word segmented data with edit-1)  
edit-2 test-set (test set of Khmer word segmented data with edit-2)  
manual test-set (the whole data that manually prepared)  
```

## Preprocessing

create a new folder for Seq2Seq experiment:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell# mkdir seq2seq
root@7a2ffa404585:/home/ye/exp/kh-spell# cd seq2seq/
```

I copied char-final/ folder ...  
data and vocab file info are as follows:   

```
char-final/
|-- edit1
|   |-- original-err
|   |   |-- test.er
|   |   `-- train.er
|   |-- test.cr
|   |-- test.er
|   |-- train-valid
|   |   |-- train.cr
|   |   `-- train.er
|   |-- train.cr
|   |-- train.er
|   |-- valid.cr
|   |-- valid.er
|   `-- vocab
|       |-- all.cr
|       |-- all.er
|       |-- vocab.cr.yml
|       `-- vocab.er.yml
|-- edit2
|   |-- original-err
|   |   |-- test.er
|   |   `-- train.er
|   |-- test.cr
|   |-- test.er
|   |-- train-valid
|   |   |-- train.cr
|   |   `-- train.er
|   |-- train.cr
|   |-- train.er
|   |-- valid.cr
|   |-- valid.er
|   `-- vocab
|       |-- all.cr
|       |-- all.er
|       |-- vocab.cr.yml
|       `-- vocab.er.yml
|-- folder-struct.txt
`-- manual
    |-- test.cr
    `-- test.er

9 directories, 31 files
```

check the manual/ ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual# ls
test.cr  test.er
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual# head -n 5 test.er
ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម អ ក ្ ស រ
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ
ខ ្ ញ ុ ំ វ ិ ញ ស ុ ំ ឆ ្ ល ើ យ ថ ា ទ េ ហ ើ យ អ ្ ន ក ណ ា ថ ា ប ្ រ ុ ស ក ំ ស ា ក ក ៏ ថ ា ទ ៅ
ប ា ត ន ឹ ង ហ ើ យ ប ង ជ ួ យ f o l l o w e d ស ៊ ែ ម ួ យ ផ ង ប ង
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual# head -n 5 test.cr
អ ៊ ី ច ឹ ង ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម ន ិ ង អ ក ្ ស រ ប ា រ ា ំ ង
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ស ្ ទ ូ ច ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ
ស ម ្ រ ា ប ់ ខ ្ ញ ុ ំ វ ិ ញ ស ុ ំ ឆ ្ ល ើ យ ថ ា ទ េ ហ ើ យ អ ្ ន ក ណ ា ថ ា ប ្ រ ុ ស ក ំ ស ា ក អ ្ វ ី ក ៏ ថ ា ទ ៅ
ប ា ត ន ឹ ង ហ ើ យ ប ង ជ ួ យ f o l l o w e d ន ិ ង ស ៊ ែ ម ួ យ ផ ង ប ង
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual#
```

Check the manual data filesize:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual# wc *
   7734    3204 2127990 test.cr
   7734    3135 1768641 test.er
  15468    6339 3896631 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/manual#
```

When I checked edit1 data filesize ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1# wc *.er
    4997     3416  2447409 test.er
   80000    54660 39293638 train.er
    9981     6911  5024735 valid.er
   94978    64987 46765782 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1# wc *.cr
    4997     3416  2447409 test.cr
   80000    54660 39293638 train.cr
    9981     6911  5024735 valid.cr
   94978    64987 46765782 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1#
```

check the file content of edit1 data:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1# head -n 3 *.er
==> test.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក អ ា ច ប ិ ទ ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ្ អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ រ ំ

==> valid.er <==
ក ញ ្ ញ ា ផ េ ង វ ួ ច ន ា ក ្ ញ ា ផ េ ង វ ួ ច ន ា
ខ ្ ញ ុ ំ ខ ្ ល ា ច យ ើ ង ច េ ញ ព ី ត ែ ម ន ៅ ព េ ល ន េ ះ ផ ង ខ ្ ញ ុ ំ ខ ្ ល ា ច យ ើ ង ច េ ញ ព ី ត ែ ម ន ៅ ព េ ល ន េ ះ ផ ង
ម ៉ ែ ប ើ ក ូ ន ជ ា ប ់ គ ុ ក ទ ៅ ម ៉ ែ ន ិ ង ប ្ អ ូ ន ន ឹ ង ទ ៅ ជ ា យ ៉ ា ង ណ ា ? ម ៉ ែ ប ើ ក ូ ន ជ ា ប ់ គ ុ ក ទ ៅ ម ៉ ែ  ិ ង ប ្ អ ូ ន ន ឹ ង ទ ៅ ជ ា យ ៉ ា ជ ណ ា ?
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1#
```

check the file content of edit1 data, *.cr:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1# head -n 3 *.cr
==> test.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក អ ា ច ប ិ ទ ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ្ អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ រ ំ

==> valid.cr <==
ក ញ ្ ញ ា ផ េ ង វ ួ ច ន ា ក ្ ញ ា ផ េ ង វ ួ ច ន ា
ខ ្ ញ ុ ំ ខ ្ ល ា ច យ ើ ង ច េ ញ ព ី ត ែ ម ន ៅ ព េ ល ន េ ះ ផ ង ខ ្ ញ ុ ំ ខ ្ ល ា ច យ ើ ង ច េ ញ ព ី ត ែ ម ន ៅ ព េ ល ន េ ះ ផ ង
ម ៉ ែ ប ើ ក ូ ន ជ ា ប ់ គ ុ ក ទ ៅ ម ៉ ែ ន ិ ង ប ្ អ ូ ន ន ឹ ង ទ ៅ ជ ា យ ៉ ា ង ណ ា ? ម ៉ ែ ប ើ ក ូ ន ជ ា ប ់ គ ុ ក ទ ៅ ម ៉ ែ  ិ ង ប ្ អ ូ ន ន ឹ ង ទ ៅ ជ ា យ ៉ ា ជ ណ ា ?
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1#
```

Check the filesize of edit2 data ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2# wc *.er
    4998     3424  2447429 test.er
   80000    54677 39289177 train.er
    9978     6907  5023517 valid.er
   94976    65008 46760123 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2# wc *.cr
    4998     3424  2447429 test.cr
   80000    54677 39289177 train.cr
    9978     6907  5023517 valid.cr
   94976    65008 46760123 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2#
```

Check the file content of edit2 data ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2# head -n 3 *.er
==> test.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក ប អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ រ ី ឈ ន ន អ ៊ ញ ី
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន ប ះ ជ ា ប ន ្ ទ ប ់ ជ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក អ ា ច ប ិ ទ ក ត ា
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ក អ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ស ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> valid.er <==
ប ៉ ុ ន ្ ត ែ គ េ ព ិ ន ិ ត ្ យ ឃ ើ ញ ថ ា ប ្ រ ព ័ ន ្ ធ ដ ា ំ ដ ុ ះ ដ ំ ណ ា ំ ស ្ រ ូ វ ត ែ ម ួ យ ម ុ ខ ប ា ន ផ ្ ត ល ់ ម ក ន ូ វ ច ំ ណ ូ ល ទ ុ ន ម ា ន ក ម ្ រ ិ ត ហ េ ត ុ ដ ូ ច ន េ ះ ក ា រ ផ ្ ល ា ស ់ ប ្ ត ូ រ ផ ្ ទ ៃ ដ ី ដ ា ំ ដ ុ ះ ស ្ រ ូ វ ឬ  ្ រ ូ វ ជ ំ ន ួ ស វ ិ ញ ដ ោ យ ដ ំ ណ ា ំ ដ ែ ល ផ ្ ត ល ់ ន ូ វ ប ្ រ ា ក ់ ច ំ ណ េ ញ ខ ្ ព ស ់ ត ា ម រ យ ៈ ក ា រ ធ ្ វ ើ ព ិ ព ិ ធ ក ម ្ ម ដ ំ ណ ា ំ គ ឺ ជ ា ដ ំ ណ ោ ះ ស ្ រ ា យ ម ួ យ គ ួ រ ព ិ ច ា រ ណ ា ប ៉ ុ ន ្ ត ែ គ េ ព ិ ន ិ ត ្ យ ឃ ើ ញ ថ ា ប ្ រ ព ័ ន ្ ធ ដ ា ំ ដ ុ ះ ដ ំ ណ ា ំ ស ្ រ ូ វ ត ែ ម ួ យ ម ុ ខ ប ា ន ផ ្ ត ល ់ ម ក ន ូ វ ច                                            ំ                                                                                                                             ំ ណ ូ ល ទ ុ ន ម ា ន ក ម ្ រ ិ ត ហ េ ត ុ ដ ូ ច ន េ ះ ក ា រ ផ ្ ល ា ស ់ ប ្ ត ូ រ ្ ផ ទ ៃ ដ ី ដ ា ំ ដ ុ ះ ស ្ រ ូ វ រ ឬ ត ្ រ ូ វ ជ ំ ន ួ ស វ ិ ញ ដ ោ យ ដ ំ ណ ា ំ ដ ែ ល ផ ្ ត ល ់ ន ូ វ ប ្ រ ា ក ់ ច ំ ណ េ ញ ខ ្ ព ស ់ ត ា ម រ យ ៈ ក ា រ ធ ្ វ ើ ព ិ ព ិ ធ ក ម ្ ម ដ ំ ណ ា ំ គ ឺ ជ ា ដ ំ ណ ោ ះ ស ្ រ ា យ ម ួ យ គ ួ រ ព ិ ច ា រ ណ ា
ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច
ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ? ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ?
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2#
```

Check the file content of *.cr (of edit2):  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2# head -n 3 *.cr
==> test.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក ប អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ រ ី ឈ ន ន អ ៊ ញ ី
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន ប ះ ជ ា ប ន ្ ទ ប ់ ជ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក អ ា ច ប ិ ទ ក ត ា
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ក អ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ស ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> valid.cr <==
ប ៉ ុ ន ្ ត ែ គ េ ព ិ ន ិ ត ្ យ ឃ ើ ញ ថ ា ប ្ រ ព ័ ន ្ ធ ដ ា ំ ដ ុ ះ ដ ំ ណ ា ំ ស ្ រ ូ វ ត ែ ម ួ យ ម ុ ខ ប ា ន ផ ្ ត ល ់ ម ក ន ូ វ ច ំ ណ ូ ល ទ ុ ន ម ា ន ក ម ្ រ ិ ត ហ េ ត ុ ដ ូ ច ន េ ះ ក ា រ ផ ្ ល ា ស ់ ប ្ ត ូ រ ផ ្ ទ ៃ ដ ី ដ ា ំ ដ ុ ះ ស ្ រ ូ វ ឬ  ្ រ ូ វ ជ ំ ន ួ ស វ ិ ញ ដ ោ យ ដ ំ ណ ា ំ ដ ែ ល ផ ្ ត ល ់ ន ូ វ ប ្ រ ា ក ់ ច ំ ណ េ ញ ខ ្ ព ស ់ ត ា ម រ យ ៈ ក ា រ ធ ្ វ ើ ព ិ ព ិ ធ ក ម ្ ម ដ ំ ណ ា ំ គ ឺ ជ ា ដ ំ ណ ោ ះ ស ្ រ ា យ ម ួ យ គ ួ រ ព ិ ច ា រ ណ ា ប ៉ ុ ន ្ ត ែ គ េ ព ិ ន ិ ត ្ យ ឃ ើ ញ ថ ា ប ្ រ ព ័ ន ្ ធ ដ ា ំ ដ ុ ះ ដ ំ ណ ា ំ ស ្ រ ូ វ ត ែ ម ួ យ ម ុ ខ ប ា ន ផ ្ ត ល ់ ម ក ន ូ វ ច                                            ំ                                                                                                                             ំ ណ ូ ល ទ ុ ន ម ា ន ក ម ្ រ ិ ត ហ េ ត ុ ដ ូ ច ន េ ះ ក ា រ ផ ្ ល ា ស ់ ប ្ ត ូ រ ្ ផ ទ ៃ ដ ី ដ ា ំ ដ ុ ះ ស ្ រ ូ វ រ ឬ ត ្ រ ូ វ ជ ំ ន ួ ស វ ិ ញ ដ ោ យ ដ ំ ណ ា ំ ដ ែ ល ផ ្ ត ល ់ ន ូ វ ប ្ រ ា ក ់ ច ំ ណ េ ញ ខ ្ ព ស ់ ត ា ម រ យ ៈ ក ា រ ធ ្ វ ើ ព ិ ព ិ ធ ក ម ្ ម ដ ំ ណ ា ំ គ ឺ ជ ា ដ ំ ណ ោ ះ ស ្ រ ា យ ម ួ យ គ ួ រ ព ិ ច ា រ ណ ា
ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច
ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ? ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ?
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2#
```

Check Vocab files for "edit1" ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1/vocab# ls
all.cr  all.er  vocab.cr.yml  vocab.er.yml
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1/vocab#
```

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1/vocab# head *.yml
==> vocab.cr.yml <==
</s>: 0
<unk>: 1                                                                                                                      ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9

==> vocab.er.yml <==
</s>: 0
<unk>: 1                                                                                                                      ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1/vocab# wc *.yml
 195  392 1522 vocab.cr.yml
 195  392 1522 vocab.er.yml
 390  784 3044 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit1/vocab#
```

check vocab file for "edit-2" ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2/vocab# ls
all.cr  all.er  vocab.cr.yml  vocab.er.yml
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2/vocab# head *.yml
==> vocab.cr.yml <==
</s>: 0
<unk>: 1                                                                                                                      ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9

==> vocab.er.yml <==
</s>: 0
<unk>: 1                                                                                                                      ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2/vocab#
```

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2/vocab# wc *.yml
 195  392 1522 vocab.cr.yml
 195  392 1522 vocab.er.yml
 390  784 3044 total
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/char-final/edit2/vocab#
```

## Prepare Shell Script

We need to prepare Seq2Seq shell script for training Seq2Seq NMT model and I prepared as follows:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training
## Last updated: 16 Dec 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.edit1";
mkdir ${model_folder};
data_path="/home/ye/exp/kh-spell/seq2seq/char-final/edit1/";
src="er"; tgt="cr";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 300 \
  --valid-sets ${data_path}/valid.${src} ${data_path}/valid.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log1
```

strat training ...  

```
...
...
...
[2022-12-16 12:57:03] [config] valid-script-path: ""
[2022-12-16 12:57:03] [config] valid-sets:
[2022-12-16 12:57:03] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit1//valid.er
[2022-12-16 12:57:03] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit1//valid.cr
[2022-12-16 12:57:03] [config] valid-translation-output: ""
[2022-12-16 12:57:03] [config] vocabs:
[2022-12-16 12:57:03] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit1//vocab/vocab.er.yml
[2022-12-16 12:57:03] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit1//vocab/vocab.cr.yml
[2022-12-16 12:57:03] [config] word-penalty: 0
[2022-12-16 12:57:03] [config] word-scores: false
[2022-12-16 12:57:03] [config] workspace: 4500
[2022-12-16 12:57:03] [config] Model is being created with Marian v1.11.0 f00d0621 2022-02-08 08:39:24 -0800
[2022-12-16 12:57:03] Using synchronous SGD
[2022-12-16 12:57:03] [comm] Compiled without MPI support. Running as a single process on 7a2ffa404585
[2022-12-16 12:57:03] Synced seed 1111
[2022-12-16 12:57:03] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/char-final/edit1//vocab/vocab.er.yml
[2022-12-16 12:57:03] [data] Setting vocabulary size for input 0 to 196
[2022-12-16 12:57:03] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/char-final/edit1//vocab/vocab.cr.yml
[2022-12-16 12:57:03] [data] Setting vocabulary size for input 1 to 196
[2022-12-16 12:57:03] [batching] Collecting statistics for batch fitting with step size 10
[2022-12-16 12:57:03] [memory] Extending reserved space to 4608 MB (device gpu0)
[2022-12-16 12:57:03] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-16 12:57:03] [comm] Using global sharding
[2022-12-16 12:57:03] [comm] NCCLCommunicators constructed successfully
[2022-12-16 12:57:03] [training] Using 1 GPUs
[2022-12-16 12:57:03] [logits] Applying loss function for 1 factor(s)
[2022-12-16 12:57:03] [memory] Reserving 704 MB, device gpu0
[2022-12-16 12:57:04] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-16 12:57:04] [memory] Reserving 704 MB, device gpu0
...
...
...
[2022-12-18 19:04:22] Best translation 40 : ត ើ ម ា ន ជ ើ ង យ ន ្ ត ហ ោ ះ ត ភ ្ ជ ា ប ់ ទ ៅ ហ ោ ស ស ្ ត ុ ន ដ ែ រ ឬ ទ េ ? ត ើ ម ា ន ជ ើ ង យ ន ្ ត ហ ោ ះ ត ភ ្ ជ ា ប ់ ទ ៅ ហ ោ ស ស ្ ត ុ ន ដ ែ រ ឬ ទ េ ?
[2022-12-18 19:04:22] Best translation 80 : ខ ្ ញ ុ ំ ស ុ ំ ម ើ ល ប ន ្ ត ិ ច ប ា ន ទ េ ? ខ ្ ញ ុ ំ ស ុ ំ ម ើ ប ន ្ ត ិ ច ប ា ន ទ េ ?
[2022-12-18 19:04:22] Best translation 160 : ក ុ ំ ព ្ យ ា យ ា ម ក ុ ំ ព យ យ ា យ ា ម
[2022-12-18 19:04:36] Best translation 320 : ក ា រ គ ិ ត ល ុ យ ស ម ្ រ ា ប ់ វ ី ស ៊ ី អ ា ក ា រ គ ិ ត រ ល ុ យ ស ម ្ រ ា ប ់ វ ី ស ៊ ី អ ា
[2022-12-18 19:04:46] Best translation 640 : អ ្ ន ក ន ៅ ទ េ ព េ ល វ ៉ ា ក ង ? ន ្ ន ក ន ៅ ទ េ ព េ ល វ ៉ ា ក ង ?
[2022-12-18 19:05:03] Best translation 1280 : ល ោ ក ប ញ ្ ជ ា ក ់ ថ ា ៖ « យ ើ ង ប ា ន ក ា ន ់ ទ ង ់ ប ង ្ រ ួ ប ប ង ្ រ ួ ម ជ ា ត ិ ហ ើ យ យ ើ ង ន ឹ ង ច ូ ល រ ួ ម ដ ោ យ ព េ ញ ច ិ ត ្ ត ព េ ញ ថ ្ ល ើ ម ឲ ្ យ ត ែ គ ោ រ ព ត ា ម រ ដ ្ ឋ ធ ម ្ ម ន ុ ញ ្ ញ ត ែ ច ល ន ា ណ ា ម ួ យ ដ ែ ល ប ៉ ះ ព ា ល ់ ដ ល ់ អ ធ ិ ប ត េ យ ្ យ ភ ា ព ប ្ រ ទ េ ស ដ ទ ៃ យ ើ ង ម ិ ន ម ា ន យ ោ ប ល ់ ទ េ » R ។ ល ោ ក ប ញ ្ ជ ា ក ់ ថ ា ៖ « យ ើ ង ប ា ន ក ា ន ់ ទ ង ់ ប ង ្ រ ួ ប ប ង ្ រ ួ ម ជ ា ត ិ ហ ើ យ យ ើ ង ន ឹ ង ច ូ ល រ ួ ម ដ ោ យ ព េ ញ ច ិ ត ្ ត ព េ ញ ថ ្ ល ើ ម ឲ ្ យ ត ែ គ ោ រ ព ត ា ម រ ដ ្ ឋ ធ ម ្ ម ន ុ ញ ្ ញ ត ែ ច ល ន ា ណ ា ម ួ យ ដ ែ ល ប ៉ ះ ព ា ល ់ ដ ល ់ អ ធ ិ ប ត េ យ ្ យ ភ ា ព ប ្ រ ទ េ ស ដ ទ ៃ យ ើ ង ម ិ ន ម ា ន យ ោ ប ល ់ ទ េ » R ។
[2022-12-18 19:05:56] Best translation 2560 : ត ើ អ ្ ន ក ត ្ រ ូ វ ក ា រ ក ក ់ ម ួ យ ទ េ ? ត ើ អ ្ ន ក ក ត ្ រ ូ វ ក ា រ ក  ់ ម ួ យ ទ េ ?
[2022-12-18 19:07:22] Best translation 5120 : ឯ ក ឧ ត ្ ត ម ស ា ម ិ ទ ្ ទ ិ ឯ ក ឧ ត ្ ត ម ស ា ម ិ ទ ្ ទ ិ
[2022-12-18 19:09:57] Total translation time: 347.87491s
[2022-12-18 19:09:57] [valid] Ep. 59 : Up. 170000 : bleu : 99.266 : new best
[2022-12-18 19:09:57] Training finished
[2022-12-18 19:09:57] Saving model weights and runtime parameters to model.seq2seq.edit1/model.npz
[2022-12-18 19:10:02] Saving Adam parameters
[2022-12-18 19:10:05] [training] Saving training checkpoint to model.seq2seq.edit1/model.npz and model.seq2seq.edit1/model.npz.optimizer.npz

real    3253m19.073s
user    3134m28.358s
sys     113m55.657s
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq#
```

check the model folder:  

```
root@79c22d75525d:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit1# ls
config.yml            model.iter135000.npz  model.iter20000.npz  model.iter60000.npz  model.npz.decoder.yml
model.iter10000.npz   model.iter140000.npz  model.iter25000.npz  model.iter65000.npz  model.npz.optimizer.npz
model.iter100000.npz  model.iter145000.npz  model.iter30000.npz  model.iter70000.npz  model.npz.progress.yml
model.iter105000.npz  model.iter15000.npz   model.iter35000.npz  model.iter75000.npz  model.npz.yml
model.iter110000.npz  model.iter150000.npz  model.iter40000.npz  model.iter80000.npz  s2s.er-cr.log1
model.iter115000.npz  model.iter155000.npz  model.iter45000.npz  model.iter85000.npz  train.log
model.iter120000.npz  model.iter160000.npz  model.iter5000.npz   model.iter90000.npz  valid.log
model.iter125000.npz  model.iter165000.npz  model.iter50000.npz  model.iter95000.npz
model.iter130000.npz  model.iter170000.npz  model.iter55000.npz  model.npz
root@79c22d75525d:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit1#
```

check the valid log file:  

```
[2022-12-16 14:24:14] [valid] Ep. 2 : Up. 5000 : cross-entropy : 22.1416 : new best
[2022-12-16 14:26:22] [valid] Ep. 2 : Up. 5000 : perplexity : 1.19078 : new best
[2022-12-16 14:26:57] [valid] First sentence's tokens as scored:
[2022-12-16 14:26:57] [valid] DefaultVocab keeps original segments for scoring
[2022-12-16 14:26:57] [valid]   Hyp:  ^~^`  ^=^r  ^~^s  ^~   ^~^d  ^~^`  ^~^z  ^~^n  ^~   ^~^j  ^=^b  ^~^{  ^~^x  ^~   ^~^s  >[2022-12-16 14:26:57] [valid]   Ref:  ^~^`  ^=^r  ^~^s  ^~   ^~^d  ^~^`  ^~^z  ^~^n  ^~   ^~^j  ^=^b  ^~^{  ^~^=  ^~^o  ^=^r >[2022-12-16 14:46:27] [valid] Ep. 2 : Up. 5000 : bleu : 21.4778 : new best
[2022-12-16 16:13:00] [valid] Ep. 4 : Up. 10000 : cross-entropy : 2.43137 : new best
[2022-12-16 16:15:08] [valid] Ep. 4 : Up. 10000 : perplexity : 1.01936 : new best
[2022-12-16 16:23:53] [valid] Ep. 4 : Up. 10000 : bleu : 82.7636 : new best
[2022-12-16 17:50:16] [valid] Ep. 6 : Up. 15000 : cross-entropy : 1.28409 : new best
[2022-12-16 17:52:24] [valid] Ep. 6 : Up. 15000 : perplexity : 1.01018 : new best
[2022-12-16 18:01:00] [valid] Ep. 6 : Up. 15000 : bleu : 92.5303 : new best
[2022-12-16 19:27:44] [valid] Ep. 7 : Up. 20000 : cross-entropy : 0.78219 : new best
[2022-12-16 19:29:52] [valid] Ep. 7 : Up. 20000 : perplexity : 1.00619 : new best
[2022-12-16 19:37:24] [valid] Ep. 7 : Up. 20000 : bleu : 95.0214 : new best
[2022-12-16 21:04:07] [valid] Ep. 9 : Up. 25000 : cross-entropy : 0.515372 : new best
[2022-12-16 21:06:15] [valid] Ep. 9 : Up. 25000 : perplexity : 1.00407 : new best
[2022-12-16 21:13:19] [valid] Ep. 9 : Up. 25000 : bleu : 96.1252 : new best
[2022-12-16 22:40:11] [valid] Ep. 11 : Up. 30000 : cross-entropy : 0.375392 : new best
[2022-12-16 22:42:18] [valid] Ep. 11 : Up. 30000 : perplexity : 1.00296 : new best
[2022-12-16 22:49:04] [valid] Ep. 11 : Up. 30000 : bleu : 96.7862 : new best
[2022-12-17 00:15:50] [valid] Ep. 13 : Up. 35000 : cross-entropy : 0.293978 : new best
[2022-12-17 00:17:58] [valid] Ep. 13 : Up. 35000 : perplexity : 1.00232 : new best
[2022-12-17 00:24:17] [valid] Ep. 13 : Up. 35000 : bleu : 96.6233 : stalled 1 times (last best: 96.7862)
[2022-12-17 01:51:06] [valid] Ep. 14 : Up. 40000 : cross-entropy : 0.244644 : new best
[2022-12-17 01:53:14] [valid] Ep. 14 : Up. 40000 : perplexity : 1.00193 : new best
[2022-12-17 01:59:28] [valid] Ep. 14 : Up. 40000 : bleu : 96.0846 : stalled 2 times (last best: 96.7862)
[2022-12-17 03:26:20] [valid] Ep. 16 : Up. 45000 : cross-entropy : 0.210326 : new best
[2022-12-17 03:28:29] [valid] Ep. 16 : Up. 45000 : perplexity : 1.00166 : new best
[2022-12-17 03:34:27] [valid] Ep. 16 : Up. 45000 : bleu : 96.3315 : stalled 3 times (last best: 96.7862)
[2022-12-17 05:01:35] [valid] Ep. 18 : Up. 50000 : cross-entropy : 0.174407 : new best
[2022-12-17 05:03:43] [valid] Ep. 18 : Up. 50000 : perplexity : 1.00138 : new best
[2022-12-17 05:09:35] [valid] Ep. 18 : Up. 50000 : bleu : 96.9138 : new best
[2022-12-17 06:36:20] [valid] Ep. 20 : Up. 55000 : cross-entropy : 0.136498 : new best
[2022-12-17 06:38:29] [valid] Ep. 20 : Up. 55000 : perplexity : 1.00108 : new best
[2022-12-17 06:44:24] [valid] Ep. 20 : Up. 55000 : bleu : 97.8289 : new best
[2022-12-17 08:11:38] [valid] Ep. 21 : Up. 60000 : cross-entropy : 0.121526 : new best
[2022-12-17 08:13:46] [valid] Ep. 21 : Up. 60000 : perplexity : 1.00096 : new best
[2022-12-17 08:19:40] [valid] Ep. 21 : Up. 60000 : bleu : 98.4312 : new best
[2022-12-17 09:46:37] [valid] Ep. 23 : Up. 65000 : cross-entropy : 0.11079 : new best
[2022-12-17 09:48:46] [valid] Ep. 23 : Up. 65000 : perplexity : 1.00087 : new best
[2022-12-17 09:54:39] [valid] Ep. 23 : Up. 65000 : bleu : 98.4936 : new best
[2022-12-17 11:21:47] [valid] Ep. 25 : Up. 70000 : cross-entropy : 0.105662 : new best
[2022-12-17 11:23:56] [valid] Ep. 25 : Up. 70000 : perplexity : 1.00083 : new best
[2022-12-17 11:29:47] [valid] Ep. 25 : Up. 70000 : bleu : 98.8019 : new best
[2022-12-17 12:56:42] [valid] Ep. 26 : Up. 75000 : cross-entropy : 0.107262 : stalled 1 times (last best: 0.105662)
[2022-12-17 12:58:50] [valid] Ep. 26 : Up. 75000 : perplexity : 1.00085 : stalled 1 times (last best: 1.00083)
[2022-12-17 13:04:39] [valid] Ep. 26 : Up. 75000 : bleu : 98.8604 : new best
[2022-12-17 14:31:49] [valid] Ep. 28 : Up. 80000 : cross-entropy : 0.109629 : stalled 2 times (last best: 0.105662)
[2022-12-17 14:33:57] [valid] Ep. 28 : Up. 80000 : perplexity : 1.00086 : stalled 2 times (last best: 1.00083)
[2022-12-17 14:39:46] [valid] Ep. 28 : Up. 80000 : bleu : 98.8898 : new best
[2022-12-17 16:06:46] [valid] Ep. 30 : Up. 85000 : cross-entropy : 0.115599 : stalled 3 times (last best: 0.105662)
[2022-12-17 16:08:54] [valid] Ep. 30 : Up. 85000 : perplexity : 1.00091 : stalled 3 times (last best: 1.00083)
[2022-12-17 16:14:37] [valid] Ep. 30 : Up. 85000 : bleu : 98.8323 : stalled 1 times (last best: 98.8898)
[2022-12-17 17:41:45] [valid] Ep. 32 : Up. 90000 : cross-entropy : 0.113816 : stalled 4 times (last best: 0.105662)
[2022-12-17 17:43:53] [valid] Ep. 32 : Up. 90000 : perplexity : 1.0009 : stalled 4 times (last best: 1.00083)
[2022-12-17 17:49:38] [valid] Ep. 32 : Up. 90000 : bleu : 98.849 : stalled 2 times (last best: 98.8898)
[2022-12-17 19:16:47] [valid] Ep. 33 : Up. 95000 : cross-entropy : 0.112386 : stalled 5 times (last best: 0.105662)
[2022-12-17 19:18:55] [valid] Ep. 33 : Up. 95000 : perplexity : 1.00089 : stalled 5 times (last best: 1.00083)
[2022-12-17 19:24:42] [valid] Ep. 33 : Up. 95000 : bleu : 98.8914 : new best
[2022-12-17 20:51:49] [valid] Ep. 35 : Up. 100000 : cross-entropy : 0.116195 : stalled 6 times (last best: 0.105662)
[2022-12-17 20:53:57] [valid] Ep. 35 : Up. 100000 : perplexity : 1.00092 : stalled 6 times (last best: 1.00083)
[2022-12-17 20:59:43] [valid] Ep. 35 : Up. 100000 : bleu : 98.9387 : new best
[2022-12-17 22:26:39] [valid] Ep. 37 : Up. 105000 : cross-entropy : 0.115279 : stalled 7 times (last best: 0.105662)
[2022-12-17 22:28:47] [valid] Ep. 37 : Up. 105000 : perplexity : 1.00091 : stalled 7 times (last best: 1.00083)
[2022-12-17 22:34:31] [valid] Ep. 37 : Up. 105000 : bleu : 99.0154 : new best
[2022-12-18 00:01:40] [valid] Ep. 39 : Up. 110000 : cross-entropy : 0.103347 : new best
[2022-12-18 00:03:48] [valid] Ep. 39 : Up. 110000 : perplexity : 1.00082 : new best
[2022-12-18 00:09:31] [valid] Ep. 39 : Up. 110000 : bleu : 99.0962 : new best
[2022-12-18 01:36:44] [valid] Ep. 40 : Up. 115000 : cross-entropy : 0.0971452 : new best
[2022-12-18 01:38:52] [valid] Ep. 40 : Up. 115000 : perplexity : 1.00077 : new best
[2022-12-18 01:44:36] [valid] Ep. 40 : Up. 115000 : bleu : 99.1454 : new best
[2022-12-18 03:11:30] [valid] Ep. 42 : Up. 120000 : cross-entropy : 0.0947782 : new best
[2022-12-18 03:13:38] [valid] Ep. 42 : Up. 120000 : perplexity : 1.00075 : new best
[2022-12-18 03:19:24] [valid] Ep. 42 : Up. 120000 : bleu : 99.1544 : new best
[2022-12-18 04:46:24] [valid] Ep. 44 : Up. 125000 : cross-entropy : 0.100008 : stalled 1 times (last best: 0.0947782)
[2022-12-18 04:48:32] [valid] Ep. 44 : Up. 125000 : perplexity : 1.00079 : stalled 1 times (last best: 1.00075)
[2022-12-18 04:54:16] [valid] Ep. 44 : Up. 125000 : bleu : 99.1728 : new best
[2022-12-18 06:21:21] [valid] Ep. 46 : Up. 130000 : cross-entropy : 0.113115 : stalled 2 times (last best: 0.0947782)
[2022-12-18 06:23:29] [valid] Ep. 46 : Up. 130000 : perplexity : 1.00089 : stalled 2 times (last best: 1.00075)
[2022-12-18 06:29:14] [valid] Ep. 46 : Up. 130000 : bleu : 99.0146 : stalled 1 times (last best: 99.1728)
[2022-12-18 07:56:15] [valid] Ep. 47 : Up. 135000 : cross-entropy : 0.112187 : stalled 3 times (last best: 0.0947782)
[2022-12-18 07:58:23] [valid] Ep. 47 : Up. 135000 : perplexity : 1.00089 : stalled 3 times (last best: 1.00075)
[2022-12-18 08:04:06] [valid] Ep. 47 : Up. 135000 : bleu : 99.0539 : stalled 2 times (last best: 99.1728)
[2022-12-18 09:31:26] [valid] Ep. 49 : Up. 140000 : cross-entropy : 0.116024 : stalled 4 times (last best: 0.0947782)
[2022-12-18 09:33:35] [valid] Ep. 49 : Up. 140000 : perplexity : 1.00092 : stalled 4 times (last best: 1.00075)
[2022-12-18 09:39:17] [valid] Ep. 49 : Up. 140000 : bleu : 99.0565 : stalled 3 times (last best: 99.1728)
[2022-12-18 11:06:39] [valid] Ep. 51 : Up. 145000 : cross-entropy : 0.118661 : stalled 5 times (last best: 0.0947782)
[2022-12-18 11:08:47] [valid] Ep. 51 : Up. 145000 : perplexity : 1.00094 : stalled 5 times (last best: 1.00075)
[2022-12-18 11:14:32] [valid] Ep. 51 : Up. 145000 : bleu : 99.0231 : stalled 4 times (last best: 99.1728)
[2022-12-18 12:41:50] [valid] Ep. 52 : Up. 150000 : cross-entropy : 0.115153 : stalled 6 times (last best: 0.0947782)
[2022-12-18 12:43:59] [valid] Ep. 52 : Up. 150000 : perplexity : 1.00091 : stalled 6 times (last best: 1.00075)
[2022-12-18 12:49:42] [valid] Ep. 52 : Up. 150000 : bleu : 99.0496 : stalled 5 times (last best: 99.1728)
[2022-12-18 14:17:06] [valid] Ep. 54 : Up. 155000 : cross-entropy : 0.108059 : stalled 7 times (last best: 0.0947782)
[2022-12-18 14:19:14] [valid] Ep. 54 : Up. 155000 : perplexity : 1.00085 : stalled 7 times (last best: 1.00075)
[2022-12-18 14:24:56] [valid] Ep. 54 : Up. 155000 : bleu : 99.1252 : stalled 6 times (last best: 99.1728)
[2022-12-18 15:51:58] [valid] Ep. 56 : Up. 160000 : cross-entropy : 0.107755 : stalled 8 times (last best: 0.0947782)
[2022-12-18 15:54:06] [valid] Ep. 56 : Up. 160000 : perplexity : 1.00085 : stalled 8 times (last best: 1.00075)
[2022-12-18 15:59:48] [valid] Ep. 56 : Up. 160000 : bleu : 99.1286 : stalled 7 times (last best: 99.1728)
[2022-12-18 17:27:02] [valid] Ep. 58 : Up. 165000 : cross-entropy : 0.108267 : stalled 9 times (last best: 0.0947782)
[2022-12-18 17:29:11] [valid] Ep. 58 : Up. 165000 : perplexity : 1.00085 : stalled 9 times (last best: 1.00075)
[2022-12-18 17:34:56] [valid] Ep. 58 : Up. 165000 : bleu : 99.1569 : stalled 8 times (last best: 99.1728)
[2022-12-18 19:02:01] [valid] Ep. 59 : Up. 170000 : cross-entropy : 0.099185 : stalled 10 times (last best: 0.0947782)
[2022-12-18 19:04:09] [valid] Ep. 59 : Up. 170000 : perplexity : 1.00078 : stalled 10 times (last best: 1.00075)
[2022-12-18 19:09:57] [valid] Ep. 59 : Up. 170000 : bleu : 99.266 : new best
```

### Testing for Sentence, Edit-1 Model

copied testing shell scripts ...  

```
root@1be262fcefc6:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit1# cp test-eval-best.sh ../../seq2seq/model.seq
2seq.edit1/
```

check/update the test shell scripts ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, CADT, Cambodia
## for NMT Experiments for Khmer Spelling Checking with NMT Models
## preparing to testing with "sentence, edit-distance-1 model"
## used Marian NMT Framework for training
## Last updated: 22 Dec 2022

data_path="/home/ye/exp/kh-spell/seq2seq/char-final/edit1";
#Note: test-data are same for both Transformer and Seq2Seq models,
#and thus I am not updating the paths of the input test data and reference data.

src="er"; tgt="cr";

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.manual.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/manual/test.${src};
echo "Evaluation with hyp.best.manual.${tgt}, Seq2Seq sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/manual/test.${tgt} \
< ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit1.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.edit1.${tgt}, Seq2Seq sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit2.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/edit2/test.${src};
echo "Evaluation with hyp.best.edit2.${tgt}, Seq2Seq sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/edit2/test.${tgt} \
< ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

start testing ...  

```
root@36ae92f960d5:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit1# ./test-eval-best.sh | tee test1.log
...
...
...
 វ ដ ំ ណ េ ក ហ ើ យ ច ា ប ់ ផ ្ ត ើ ម ដ ុ ះ ផ ្ ទ ុ យ ដ ក វ ិ ញ ក ា រ ទ ុ ក ដ ា ដ ់ គ ្ រ ា ប ់ ព ូ ជ ក ្ ន ុ ង ក ន ្ ល ែ ង ដ ែ ល ម ា ន ក ម ្ ត ៅ ប រ ិ យ ា ក ា ស ព ី ៤ ០ ៥ ០ អ ង ្ ស ា ស េ គ ឺ ធ ្ វ ើ ឱ ្ យ គ ្ រ ា ប ់ ប ញ ្ ឈ ប ់ ន ូ វ ដ ំ ណ េ ក ហ ើ យ ច ា ប ់ ផ ្ ត ើ ម ដ ុ ះ
[2022-12-22 02:29:30] Best translation 4918 : អ ្ វ ី ដ ែ ល ជ ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ? អ វ ្ ី ដ ែ ល ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ?
[2022-12-22 02:29:30] Best translation 4919 : ខ ្ ញ ុ ំ ច ង ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់ ថ ្ ង ៃ  ្ អ ែ ក ខ ្ ញ ុ                                                                                                                ំ                                                                                                                             ំ ច ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់ ្ ង ៃ ស ្ អ ែ ក
[2022-12-22 02:29:30] Best translation 4920 : ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ ទ េ ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ េ េ
[2022-12-22 02:29:30] Best translation 4921 : ក ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។ ក ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ម ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។
[2022-12-22 02:29:30] Best translation 4922 : ត ើ ន ៅ ហ ា វ ៉ ៃ ម ៉ ោ ង ជ ា ថ ្ ង ៃ អ ្ វ ី ? ត ើ ន ៅ ហ ៉ វ ៉ ៃ ម ៉ ោ ង ជ ា  ្ ង ៃ អ ្ វ ី ? ្
[2022-12-22 02:29:30] Best translation 4923 : ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ ស ុ វ ណ ្ ណ ី ស ូ ម ្ ប ី ម ួ យ ម ៉ ា ត ់ ន                                                                                                                 ិ                                                                                                                             ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ា ំ ង ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ ស ុ វ ណ ្ ណ ី ស ម ្ ប ូ ី ម ួ យ ម ៉ ា ត                                                                                                           ់                                                                                                                             ់ ន ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ី ា ង
[2022-12-22 02:29:30] Total time: 1162.79029s wall

real    19m24.607s
user    17m51.990s
sys     1m33.154s
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.
```

check the results ...  

```
root@36ae92f960d5:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit1# cat ./eval-best-result.txt
Evaluation with hyp.best.manual.cr, Seq2Seq sent, edit1 model:
BLEU = 76.06, 86.5/80.6/76.8/73.6 (BP=0.960, ratio=0.961, hyp_len=510108, ref_len=531058)
==========
Evaluation with hyp.best.edit1.cr, Seq2Seq sent, edit1 model:
BLEU = 99.51, 100.0/100.0/100.0/100.0 (BP=0.995, ratio=0.995, hyp_len=598807, ref_len=601627)
==========
Evaluation with hyp.best.edit2.cr, Seq2Seq sent, edit1 model:
BLEU = 99.52, 100.0/100.0/99.9/99.9 (BP=0.996, ratio=0.996, hyp_len=599063, ref_len=601640)
root@36ae92f960d5:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit1#
```

## Seq2Seq Edit-2 Model

prepare a shell script for training Seq2Seq model ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq# cp seq2seq.edit1.sh seq2seq.edit2.sh
```

the updated shell script is as follows:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training for edit-2 data
## Last updated: 19 Dec 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.edit2";
mkdir ${model_folder};
data_path="/home/ye/exp/kh-spell/seq2seq/char-final/edit2/";
src="er"; tgt="cr";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 300 \
  --valid-sets ${data_path}/valid.${src} ${data_path}/valid.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.edit2.log1
```

check GPU status:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq# nvidia-smi
Failed to initialize NVML: Unknown Error
```

logout container accout, logout server etc. and then check again.  

```
ye@lst-gpu-3090:~$ nvidia-smi
Mon Dec 19 07:57:28 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.86.01    Driver Version: 515.86.01    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
|  0%   45C    P8    36W / 480W |     63MiB / 24564MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      3639      G   /usr/lib/xorg/Xorg                 46MiB |
|    0   N/A  N/A      3771      G   /usr/bin/gnome-shell               15MiB |
+-----------------------------------------------------------------------------+
```

re-login to container env:  

```
ye@lst-gpu-3090:~$ ./start-ye_conda.sh
[sudo] password for ye:
ye_conda
root@79c22d75525d:/# cd temp/build
root@79c22d75525d:/temp/build# ls
CMakeCache.txt     CPackSourceConfig.cmake  libmarian.a  marian-conv     marian-vocab  spm_export_vocab  src
CMakeFiles         Makefile                 local        marian-decoder  spm_decode    spm_normalize
CPackConfig.cmake  cmake_install.cmake      marian       marian-scorer   spm_encode    spm_train
root@79c22d75525d:/temp/build# cp marian* /usr/bin/
```

start training edit-2 model ...  

```
root@1be262fcefc6:/home/ye/exp/kh-spell/seq2seq# ./seq2seq.edit2.sh
...
...
...
[2022-12-19 01:04:50] [config] valid-script-path: ""
[2022-12-19 01:04:50] [config] valid-sets:
[2022-12-19 01:04:50] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit2//valid.er
[2022-12-19 01:04:50] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit2//valid.cr
[2022-12-19 01:04:50] [config] valid-translation-output: ""
[2022-12-19 01:04:50] [config] vocabs:
[2022-12-19 01:04:50] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit2//vocab/vocab.er.yml
[2022-12-19 01:04:50] [config]   - /home/ye/exp/kh-spell/seq2seq/char-final/edit2//vocab/vocab.cr.yml
[2022-12-19 01:04:50] [config] word-penalty: 0
[2022-12-19 01:04:50] [config] word-scores: false
[2022-12-19 01:04:50] [config] workspace: 4500
[2022-12-19 01:04:50] [config] Model is being created with Marian v1.11.0 f00d0621 2022-02-08 08:39:24 -0800
[2022-12-19 01:04:50] Using synchronous SGD
[2022-12-19 01:04:50] [comm] Compiled without MPI support. Running as a single process on 1be262fcefc6
[2022-12-19 01:04:50] Synced seed 1111
[2022-12-19 01:04:50] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/char-final/edit2//vocab/vocab.er.yml
[2022-12-19 01:04:50] [data] Setting vocabulary size for input 0 to 196
[2022-12-19 01:04:50] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/char-final/edit2//vocab/vocab.cr.yml
[2022-12-19 01:04:50] [data] Setting vocabulary size for input 1 to 196
[2022-12-19 01:04:50] [batching] Collecting statistics for batch fitting with step size 10
[2022-12-19 01:04:50] [memory] Extending reserved space to 4608 MB (device gpu0)
[2022-12-19 01:04:50] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-19 01:04:50] [comm] Using global sharding
[2022-12-19 01:04:50] [comm] NCCLCommunicators constructed successfully
[2022-12-19 01:04:50] [training] Using 1 GPUs
[2022-12-19 01:04:50] [logits] Applying loss function for 1 factor(s)
[2022-12-19 01:04:50] [memory] Reserving 704 MB, device gpu0
[2022-12-19 01:04:51] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-19 01:04:51] [memory] Reserving 704 MB, device gpu0
...
...
...
 ព េ ល ន េ ះ ត ើ ន រ ណ ា ព ិ ត ប ្ រ ា ក ដ ដ ែ ល ម                                                                            ិ                                                                                                                             ិ ន ស ្ គ ា ល ់ ទ ំ ហ ំ ផ ្ ទ ៃ ម េ ឃ ? ត ើ ស ត ្ វ ក ង ្ ក ែ ប ជ ា ស ត ្ វ ខ ើ ច ស ម ត ្ ថ ភ ា ព ម ិ ន ស ្ គ ា ល ់ ទ ំ ហ ំ ម េ ឃ ឬ ក ៏ ម ន ុ ស ្ ស ដ ែ ល ន ា ំ គ ្ ន ា ត ្ ម ះ ត ិ ះ ដ ៀ ល ក ង ្ ក ែ ប ប ា ត អ ណ ្ ត ូ ង ជ
[2022-12-19 02:34:53] Best translation 0 : ប ៉ ុ ន ្ ត ែ គ េ ព ិ ន ិ ត ្ យ ឃ ើ ញ ថ ា ប ្ រ ព ័ ន ្ ធ ដ ា ំ ដ ុ ះ ដ ំ ណ ា ំ ដ ែ ល ផ ្ ត ល ់ ម ក ន ូ វ ច ំ ណ ូ ល ទ ុ ន ម ា ន ក ម ្ រ ិ ត ហ េ ត ុ ដ ូ ច ន េ ះ ក ា រ ផ ្ ល ា ស ់ ប ្ ត ូ រ ផ ្ ទ ៃ ដ ី ដ ា ំ ដ ុ ះ ស ្ រ ា យ ម ួ យ គ ួ រ ព ិ ច ា រ ណ ា
[2022-12-19 02:35:03] Best translation 1 : ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច ខ ្ ញ ុ ំ ម ិ ន អ ា ច ជ ឿ ថ ា វ ា ខ ូ ច
[2022-12-19 02:35:03] Best translation 2 : ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ? ខ ្ ញ ុ ំ អ ា ច ទ ទ ួ ល ល ុ យ ត ្ រ ឡ ប ់ ម ក វ ិ ញ ទ េ ?
[2022-12-19 02:35:03] Best translation 3 : ខ ្ ញ ុ ំ ច ង ់ ប ា ន ម ៉ ូ ត ស ក ់ ថ ្ ម ី ប ំ ផ ុ ត ដ ែ ល អ ្ ន ក គ ិ ត ថ ា ស ម ន ឹ ង ខ ្ ញ ុ ំ ច ង ់ ប ា ន ម ៉ ូ ត ស ក ់ ថ ្ ម ី ប ំ ផ ុ ត ដ ែ ល អ ្ ន ក គ ិ ត ថ ា ស ម ន ឹ ង ខ ្ ញ ុ ំ
[2022-12-19 02:35:03] Best translation 4 : ល ោ ក ស ្ រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ ា ល ោ ក ្ ស រ ី វ ណ ្ ណ ដ
[2022-12-19 02:35:03] Best translation 5 : ស ី ត ុ ណ ្ ហ ភ ា ព ត ុ ល ្ យ ភ ា ព ទ ឹ ក ន ិ ង ស ម ្ ព ា ធ ឈ ា ម ល ើ ស ព ី ន េ ះ ម ា ន ន ា ទ ី យ ៉ ា ង ស ំ ខ ា ន ់ ប ង ្ ក ើ ត ឬ ភ ្ ញ ោ ច ក ា រ ប ញ ្ ច េ ញ អ រ ម ៉ ូ ន រ ប ស ់ ក ្ រ ព េ ញ អ ៊ ី ប ៉ ូ ភ ី ស ។
[2022-12-19 02:35:03] Best translation 10 : ហ ើ យ ខ ្ ញ ុ ំ ច ង ់ អ ោ យ អ ្ ន ក ម ិ ន ប ្ រ ក រ ន ់
[2022-12-19 02:35:03] Best translation 20 : គ ា ត ់ ឈ ្ ម ោ ះ វ ី ដ ា វ ័ ន ្ ត គ ា ត ់ ឈ ្ ម ោ ះ វ ី ដ ា វ ័ ន ្ ត
[2022-12-19 02:35:03] Best translation 40 : ត ា ម រ យ ៈ ស ម ី ក ា រ ន េ ះ អ ា ច ប ញ ្ ជ ា ក ់ ថ ា ច ម ្ ល ើ យ ត ប ន ៃ ដ ំ ណ  ំ ន ឹ ង ធ ្ ល ា ក ់ ច ុ ះ ន ៅ ព េ ល ដ ែ ល ក ម ្ រ ិ ត ន ៃ ក ា រ ប ្ រ ើ ជ ី ក ើ ន ឡ ើ ង
[2022-12-19 02:35:03] Best translation 80 : វ ា ថ ្ ល ៃ វ ា ថ ្ ល ៃ
[2022-12-19 02:35:03] Best translation 160 : ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ក ់ ស ្ ល ុ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។
[2022-12-19 02:35:35] Best translation 320 : ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន
[2022-12-19 02:36:14] Best translation 640 : អ ្ ន ក ន ា ង ហ ុ ន ស ុ ម ា ន
[2022-12-19 02:37:31] Best translation 1280 : ក ្ រ ព ះ រ ខ ្ ញ ុ ំ ព ឺ
[2022-12-19 02:40:16] Best translation 2560 : ត ើ ន េ ះ គ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ? ត ើ ន េ ះ គ ឺ  ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ?
[2022-12-19 02:44:46] Best translation 5120 : អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ
...
...
...
[2022-12-19 15:32:02] Best translation 640 : អ ្ ន ក ន ា ង ហ ុ ន ស ុ ម ា ន អ ្ ន ក ន ា ង ម ហ ុ ស ុ ម ា ន
[2022-12-19 15:32:26] Best translation 1280 : ក ្ រ ព ះ ខ ្ ញ ុ ំ ឈ ឺ ក ្ រ ព ះ រ ខ ្ ញ ុ ំ ព ឺ
[2022-12-19 15:33:13] Best translation 2560 : ត ើ ន េ ះ គ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ? ត ើ ន េ ះ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ស ត ូ អ ៊ ី ម ែ ន ទ េ ?
[2022-12-19 15:34:43] Best translation 5120 : អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ា ត ុ ណ ា ស ់ ព េ ល េ ះ
[2022-12-19 15:37:19] Total translation time: 350.18331s
[2022-12-19 15:37:19] [valid] Ep. 16 : Up. 45000 : bleu : 96.0812 : new best
[2022-12-19 15:45:46] Ep. 16 : Up. 45500 : Sen. 53,671 : Cost 0.09405990 * 1,116,862 @ 2,271 after 101,667,796 : Time 1150.61s : 970.67 words/s : gNorm 0.2638
[2022-12-19 15:54:07] Ep. 16 : Up. 46000 : Sen. 66,220 : Cost 0.09300728 * 1,117,609 @ 1,831 after 102,785,405 : Time 500.66s : 2232.29 words/s : gNorm 0.2310
[2022-12-19 15:57:46] Seen 72,097 samples
[2022-12-19 15:57:46] Starting data epoch 17 in logical epoch 17
[2022-12-19 15:57:46] [data] Shuffling data
[2022-12-19 15:57:46] [data] Done reading 80,000 sentences
[2022-12-19 15:57:46] [data] Done shuffling 80,000 sentences to temp files
[2022-12-19 16:02:19] Ep. 17 : Up. 46500 : Sen. 6,932 : Cost 0.09449922 * 1,113,735 @ 2,314 after 103,899,140 : Time 492.54s : 2261.22 words/s : gNorm 0.2297
[2022-12-19 16:10:49] Ep. 17 : Up. 47000 : Sen. 19,308 : Cost 0.09098923 * 1,116,107 @ 2,301 after 105,015,247 : Time 509.11s : 2192.26 words/s : gNorm 0.2446
[2022-12-19 16:19:07] Ep. 17 : Up. 47500 : Sen. 31,882 : Cost 0.09060568 * 1,117,499 @ 2,286 after 106,132,746 : Time 498.24s : 2242.87 words/s : gNorm 0.2337
[2022-12-19 16:27:41] Ep. 17 : Up. 48000 : Sen. 44,024 : Cost 0.09161432 * 1,115,831 @ 2,334 after 107,248,577 : Time 513.90s : 2171.28 words/s : gNorm 0.2184
[2022-12-19 16:35:52] Ep. 17 : Up. 48500 : Sen. 56,812 : Cost 0.08904881 * 1,114,961 @ 2,332 after 108,363,538 : Time 491.40s : 2268.93 words/s : gNorm 0.2154
...
...
...
[2022-12-20 07:16:39] Best translation 20 : គ ា ត ់ ឈ ្ ម ោ ះ វ ី ដ ា វ ័ ន ្ ត គ ា ត ់ ឈ ្ ម ោ ះ វ ដ ត ា វ ័ ន ្ ត
[2022-12-20 07:16:39] Best translation 40 : ត ា ម រ យ ៈ ស ម ី ក ា រ ន េ ះ អ ា ច ប ញ ្ ជ ា ក ់ ថ ា ច ម ្ ល ើ យ ត ប ន ៃ ដ ំ ណ ា ំ ន ឹ ង ធ ្ ល ា ក ់ ច ុ ះ ន ៅ ព េ ល ដ ែ ល ក ម ្ រ ិ ត ន ៃ ក ា រ ប ្ រ ើ ជ ី ក ើ ន ឡ ើ ង ត ា ម រ យ ៈ ស ម ី ក ា រ ន េ ះ អ ា ច ា ប ញ ្ ជ ា ក ់ ថ ា ច ម ្ ល ើ យ ត ប ន ៃ ដ ំ ណ ា ំ ន ឹ ង ធ ្ ល ា ក ់ ច ុ ះ ន ៅ ព េ ល ដ ែ ល ក ម ្ រ ិ ត ន ៃ ក ា រ ប ្ រ ើ ជ ឡ ក ើ ន ឡ ើ ង
[2022-12-20 07:16:39] Best translation 80 : វ ា ថ ្ ល ៃ វ ា ា ល ្ ៃ
[2022-12-20 07:16:39] Best translation 160 : ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ក ់ ស ្ ល ុ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។ ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ស ្ ល ុ ់ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។
[2022-12-20 07:16:46] Best translation 320 : ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព ត ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី គ ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព ត ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន
[2022-12-20 07:17:00] Best translation 640 : អ ្ ន ក ន ា ង ហ ុ ន ស ុ ម ា ន អ ្ ន ក ន ា ង ម ហ ុ ស ុ ម ា ន
[2022-12-20 07:17:23] Best translation 1280 : ក ្ រ ព ះ ខ ្ ញ ុ ំ ឈ ឺ ក ្ រ ព ះ រ ខ ្ ញ ុ ំ ព ឺ
[2022-12-20 07:18:13] Best translation 2560 : ត ើ ន េ ះ គ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ? ត ើ ន េ ះ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ស ត ូ អ ៊ ី ម ែ ន ទ េ ?
[2022-12-20 07:19:39] Best translation 5120 : អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ា ត ុ ណ ា ស ់ ព េ ល េ ះ
[2022-12-20 07:22:09] Total translation time: 341.83692s
[2022-12-20 07:22:09] [valid] Ep. 33 : Up. 95000 : bleu : 98.9888 : stalled 1 times (last best: 99.0195)
[2022-12-20 07:27:58] Seen 72,097 samples
[2022-12-20 07:27:58] Starting data epoch 34 in logical epoch 34
[2022-12-20 07:27:58] [data] Shuffling data
[2022-12-20 07:27:59] [data] Done reading 80,000 sentences
[2022-12-20 07:27:59] [data] Done shuffling 80,000 sentences to temp files
[2022-12-20 07:30:30] Ep. 34 : Up. 95500 : Sen. 3,769 : Cost 0.06934321 * 1,114,261 @ 2,258 after 213,367,431 : Time 1136.22s : 980.68 words/s : gNorm 0.1763
...
...
...
[2022-12-20 19:52:44] Best translation 160 : ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ក ់ ស ្ ល ុ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។ ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ស ្ ល ុ ់ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។
[2022-12-20 19:52:51] Best translation 320 : ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព ត ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី គ ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម                                                                ួ                                                                                                                             ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព  ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក                                                                                        ់                                                                                                                             ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន
[2022-12-20 19:53:05] Best translation 640 : អ ្ ន ក ន ា ង ហ ុ ន ស ុ ម ា ន អ ្ ន ក ន ា ង ម ហ ុ ស ុ ម ា ន
[2022-12-20 19:53:28] Best translation 1280 : ក ្ រ ព ះ ខ ្ ញ ុ ំ ឈ ឺ ក ្ រ ព ះ រ ខ ្ ញ ុ ំ ព ឺ
[2022-12-20 19:54:15] Best translation 2560 : ត ើ ន េ ះ គ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ? ត ើ ន េ ះ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ស ត ូ អ ៊ ី ម ែ ន ទ េ ?
[2022-12-20 19:55:41] Best translation 5120 : អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ា ត ុ ណ ា ស ់ ព េ ល េ ះ
[2022-12-20 19:58:11] Total translation time: 338.99281s
[2022-12-20 19:58:11] [valid] Ep. 47 : Up. 135000 : bleu : 99.0416 : stalled 3 times (last best: 99.2182)
[2022-12-20 20:06:42] Ep. 47 : Up. 135500 : Sen. 64,599 : Cost 0.05341753 * 1,117,150 @ 2,264 after 302,743,070 : Time 1139.28s : 980.57 words/s : gNorm 0.1520
[2022-12-20 20:11:39] Seen 72,097 samples
[2022-12-20 20:11:39] Starting data epoch 48 in logical epoch 48
[2022-12-20 20:11:39] [data] Shuffling data
[2022-12-20 20:11:39] [data] Done reading 80,000 sentences
[2022-12-20 20:11:39] [data] Done shuffling 80,000 sentences to temp files
[2022-12-20 20:15:09] Ep. 48 : Up. 136000 : Sen. 5,031 : Cost 0.05394067 * 1,116,472 @ 2,358 after 303,859,542 : Time 506.83s : 2202.85 words/s : gNorm 0.1460
...
...
...
[2022-12-21 00:36:37] Best translation 160 : ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ក ់ ស ្ ល ុ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។ ហ ្ វ ូ ង ម ្ រ ឹ គ ដ ឹ ង ថ ា ព ្ រ ះ ព ោ ធ ិ ស ត ្ វ ត ្ រ ូ វ គ េ ប ា ញ ់ ក ៏ ត ស ្ ល ុ ់ ត ភ ្ ញ ា ក ់ ផ ្ អ ើ ល រ ត ់ អ ស ់ ។
[2022-12-21 00:36:44] Best translation 320 : ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព ត ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី គ ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន ទ ្ វ ា រ ប ន ្ ទ ប ់ រ ៀ ន រ ប ើ ក ឡ ើ ង ជ ា ម                                                                ួ                                                                                                                             ួ យ រ ូ ប រ ា ង ត ូ ច ច ្ រ ឡ ឹ ង រ ប ស ់ ក ្ ម េ ង ស ្ រ ី ដ ៏ គ ួ រ ឱ ្ យ ស ្ រ ល ា ញ ់ ម ្ ន ា ក ់ ដ ែ ល ស ្ ល ៀ ក ស ំ ព  ់ ភ ្ ល ី ស េ ខ ្ ល ី ត ្ រ ឹ ម ជ ង ្ គ ង ់ ទ ី ន ុ យ ជ ា ម ួ យ អ ា វ ដ ៃ ខ ្ ល ី ន ិ ង ស ្ ប ែ ក ជ ើ ង ប ៉ ា ត ា ព ណ ៌ ផ ្ ទ ៃ ម េ ឃ ស ៊ ី ្ ន ា ដ ោ យ ច ង ល ើ ក ស ក                                                                                        ់                                                                                                                             ់ ទ ា ំ ង អ ស ់ ឡ ើ ង ទ ុ ក ត ែ ដ ឺ ម ី ខ ា ង ម ុ ខ ជ ា ឯ ក ស ណ ្ ឋ ា ន រ ប ស ់ ន ិ ស ្ ស ិ ត ស ា ក ល វ ិ ទ ្ យ ា ល ័ យ ន ័ រ ត ុ ន
[2022-12-21 00:36:58] Best translation 640 : អ ្ ន ក ន ា ង ហ ុ ន ស ុ ម ា ន អ ្ ន ក ន ា ង ម ហ ុ ស ុ ម ា ន
[2022-12-21 00:37:22] Best translation 1280 : ក ្ រ ព ះ ខ ្ ញ ុ ំ ឈ ឺ ក ្ រ ព ះ រ ខ ្ ញ ុ ំ ព ឺ
[2022-12-21 00:38:08] Best translation 2560 : ត ើ ន េ ះ គ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ត ស ូ អ ៊ ី ម ែ ន ទ េ ? ត ើ ន េ ះ ឺ ទ ី ល ំ ន ៅ រ ប ស ់ ម ៉ ា ស ត ូ អ ៊ ី ម ែ ន ទ េ ?
[2022-12-21 00:39:34] Best translation 5120 : អ ា ក ា ស ធ ា ត ុ ណ ា ស ់ ព េ ល ន េ ះ អ ា ក ា ស ា ត ុ ណ ា ស ់ ព េ ល េ ះ
[2022-12-21 00:42:03] Total translation time: 338.24392s
[2022-12-21 00:42:03] [valid] Ep. 52 : Up. 150000 : bleu : 98.9482 : stalled 6 times (last best: 99.2182)
[2022-12-21 00:42:03] Training finished
[2022-12-21 00:42:03] Saving model weights and runtime parameters to model.seq2seq.edit2/model.npz
[2022-12-21 00:42:08] Saving Adam parameters
[2022-12-21 00:42:11] [training] Saving training checkpoint to model.seq2seq.edit2/model.npz and model.seq2seq.edit2/model.npz.optimizer.npz

real    2857m37.526s
user    2751m21.755s
sys     101m33.343s
root@1be262fcefc6:/home/ye/exp/kh-spell/seq2seq#
```

### Testing Seq2Seq Sentence, Edit-2 Model

```
root@1be262fcefc6:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit1# cd ../model.transformer.sent.edit2/
root@1be262fcefc6:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit2# cp test-eval-best.sh ../../seq2seq/model.seq2seq.edit2/
root@1be262fcefc6:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit2#
```

bash shell script for testing with Seq2Seq, sentence level, edit-2 model ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, CADT, Cambodia
## for NMT Experiments for Khmer Spelling Checking with NMT Models
## preparing for testing with "sentence level, edit-distance 2 model"
## used Marian NMT Framework for training
## Last updated: 22 Dec 2022

data_path="/home/ye/exp/kh-spell/seq2seq/char-final/edit2";
#Note: test-data are same for both Transformer and Seq2Seq models,
#and thus I am not updating the paths of the input test data and reference data.
src="er"; tgt="cr";

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.manual.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/manual/test.${src};
echo "Evaluation with hyp.best.manual.${tgt}, Seq2Seq sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/manual/test.${tgt} \
< ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit1.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/edit1/test.${src};
echo "Evaluation with hyp.best.edit1.${tgt}, Seq2Seq sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/edit1/test.${tgt} < ./hyp.best.edit1.${tgt} >>

echo "=" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit2.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.edit2.${tgt}, Seq2Seq sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

start testing ...  

```
test-eval-best.sh | tee test1.log
...
...
...
 វ ដ ំ ណ េ ក ហ ើ យ ច ា ប ់ ផ ្ ត ើ ម ដ ុ ះ ផ ្ ទ ុ យ ដ ក វ ិ ញ ក ា រ ទ ុ ក ដ ា ដ ់ គ ្ រ ា ប ់ ព ូ ជ ក ្ ន ុ ង ក ន ្ ល ែ ង ដ ែ ល ម ា ន ក ម ្ ត ៅ ប រ ិ យ ា ក ា ស ព ី ៤ ០ ៥ ០ អ ង ្ ស ា ស េ គ ឺ ធ ្ វ ើ ឱ ្ យ គ ្ រ ា ប ់ ប ញ ្ ឈ ប ់ ន ូ វ ដ ំ ណ េ ក ហ ើ យ ច ា ប ់ ផ ្ ត ើ ម ដ ុ ះ
[2022-12-22 04:02:22] Best translation 4918 : អ ្ វ ី ដ ែ ល ជ ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ? អ វ ្ ី ដ ែ ល ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ?
[2022-12-22 04:02:23] Best translation 4919 : ខ ្ ញ ុ ំ ច ង ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់ ថ ្ ង ៃ  ្ អ ែ ក ខ ្ ញ ុ                                                                                                                ំ                                                                                                                             ំ ច ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់ ្ ង ៃ ស ្ អ ែ ក
[2022-12-22 04:02:23] Best translation 4920 : ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ ទ េ ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ េ េ
[2022-12-22 04:02:23] Best translation 4921 : ក ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។ ក ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ម ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។
[2022-12-22 04:02:23] Best translation 4922 : ត ើ ន ៅ ហ ា វ ៉ ៃ ម ៉ ោ ង ជ ា ថ ្ ង ៃ អ ្ វ ី ? ត ើ ន ៅ ហ ៉ វ ៉ ៃ ម ៉ ោ ង ជ ា  ្ ង ៃ អ ្ វ ី ? ្
[2022-12-22 04:02:23] Best translation 4923 : ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ ស ុ វ ណ ្ ណ ី ស ូ ម ្ ប ី ម ួ យ ម ៉ ា ត ់ ន                                                                                                                 ិ                                                                                                                             ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ា ំ ង ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ ស ុ វ ណ ្ ណ ី ស ម ្ ប ូ ី ម ួ យ ម ៉ ា ត                                                                                                           ់                                                                                                                             ់ ន ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ី ា ង
[2022-12-22 04:02:23] Total time: 1157.84237s wall

real    19m19.630s
user    17m47.521s
sys     1m32.631s
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.
root@36ae92f960d5:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit2#
```

evaluation results for edit-2 model is as follows:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit2# cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Seq2Seq sent, edit2 model:
BLEU = 77.19, 99.5/96.3/93.0/89.7 (BP=0.816, ratio=0.831, hyp_len=441423, ref_len=531058)
==========
Evaluation with hyp.best.edit1.cr, Seq2Seq sent, edit2 model:
BLEU = 99.33, 100.0/100.0/100.0/100.0 (BP=0.994, ratio=0.994, hyp_len=597803, ref_len=601627)
==========
Evaluation with hyp.best.edit2.cr, Seq2Seq sent, edit2 model:
BLEU = 99.31, 100.0/100.0/100.0/100.0 (BP=0.993, ratio=0.993, hyp_len=597672, ref_len=601640)
root@41bd19a2fd56:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.edit2#
```

## Seq2Seq Model with Word Level

Now, already finished for sentence level two models (edit-1 and edit-2) as shown in above.  
for this time, I will use 4nmt/ data ...  

copied word level or dictionary data:  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq# cp ../transformer/4nmt/ . -r
```

copied seq2seq based shell script that I prepared for edit1 ...  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq# cp seq2seq.edit1.sh seq2seq.dict.sh
```

I updated the copied shell script.  
training shell script of Seq2Seq, dictionary is as follows:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## used for NMT Experiments for Khmer spelling correction
## used Marian NMT Framework for seq2seq training
## Last updated: 22 Dec 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.dict";
mkdir ${model_folder};
data_path="/home/ye/exp/kh-spell/seq2seq/4nmt/char-segment/";
src="er"; tgt="cr";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 300 \
  --valid-sets ${data_path}/valid.${src} ${data_path}/valid.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log1
```

Start training for Seq2Seq Dictionary Model ...  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq# ./seq2seq.dict.sh
...
...
...
[2022-12-22 11:35:52] [config] valid-script-path: ""
[2022-12-22 11:35:52] [config] valid-sets:
[2022-12-22 11:35:52] [config]   - /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//valid.er
[2022-12-22 11:35:52] [config]   - /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//valid.cr
[2022-12-22 11:35:52] [config] valid-translation-output: ""
[2022-12-22 11:35:52] [config] vocabs:
[2022-12-22 11:35:52] [config]   - /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//vocab/vocab.er.yml
[2022-12-22 11:35:52] [config]   - /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//vocab/vocab.cr.yml
[2022-12-22 11:35:52] [config] word-penalty: 0
[2022-12-22 11:35:52] [config] word-scores: false
[2022-12-22 11:35:52] [config] workspace: 4500
[2022-12-22 11:35:52] [config] Model is being created with Marian v1.11.0 f00d0621 2022-02-08 08:39:24 -0800
[2022-12-22 11:35:52] Using synchronous SGD
[2022-12-22 11:35:52] [comm] Compiled without MPI support. Running as a single process on 0d441b235700
[2022-12-22 11:35:52] Synced seed 1111
[2022-12-22 11:35:52] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//vocab/vocab.er.yml
[2022-12-22 11:35:52] [data] Setting vocabulary size for input 0 to 114
[2022-12-22 11:35:52] [data] Loading vocabulary from JSON/Yaml file /home/ye/exp/kh-spell/seq2seq/4nmt/char-segment//vocab/vocab.cr.yml
[2022-12-22 11:35:52] [data] Setting vocabulary size for input 1 to 105
[2022-12-22 11:35:52] [batching] Collecting statistics for batch fitting with step size 10
[2022-12-22 11:35:52] [memory] Extending reserved space to 4608 MB (device gpu0)
[2022-12-22 11:35:52] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-22 11:35:52] [comm] Using global sharding
[2022-12-22 11:35:53] [comm] NCCLCommunicators constructed successfully
[2022-12-22 11:35:53] [training] Using 1 GPUs
[2022-12-22 11:35:53] [logits] Applying loss function for 1 factor(s)
[2022-12-22 11:35:53] [memory] Reserving 704 MB, device gpu0
[2022-12-22 11:35:53] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-22 11:35:53] [memory] Reserving 704 MB, device gpu0
...
...
...
[2022-12-22 13:09:36] Ep. 39 : Up. 35000 : Sen. 19,558 : Cost 0.38018847 * 768,592 @ 1,731 after 53,493,899 : Time 72.90s : 10543.49 words/s : gNorm 0.6194
[2022-12-22 13:09:36] Saving model weights and runtime parameters to model.seq2seq.dict/model.iter35000.npz
[2022-12-22 13:09:38] Saving model weights and runtime parameters to model.seq2seq.dict/model.npz
[2022-12-22 13:09:43] Saving Adam parameters
[2022-12-22 13:09:46] [training] Saving training checkpoint to model.seq2seq.dict/model.npz and model.seq2seq.dict/model.npz.optimizer.npz
[2022-12-22 13:10:17] [valid] Ep. 39 : Up. 35000 : cross-entropy : 2.21984 : new best
[2022-12-22 13:10:31] [valid] Ep. 39 : Up. 35000 : perplexity : 1.2549 : new best
[2022-12-22 13:10:31] Translating validation set...
[2022-12-22 13:10:31] Best translation 0 : ក ្ រ ហ ម ឆ ្ អ ិ ន
[2022-12-22 13:10:31] Best translation 1 : គ ន ្ ថ ច រ ន ា
[2022-12-22 13:10:31] Best translation 2 : ស ា ស ន ិ ក ជ ន
[2022-12-22 13:10:32] Best translation 3 : ក ោ ះ ឯ ក
[2022-12-22 13:10:32] Best translation 4 : ព ្ រ ូ ន ព ា ន
[2022-12-22 13:10:32] Best translation 5 : ឈ ូ ក ច ្ រ ា ល
[2022-12-22 13:10:32] Best translation 10 : ស ្ ង ួ ន ព ្ រ ល ឹ ង
[2022-12-22 13:10:32] Best translation 20 : ម ៉ ា ក ្ ម េ ក
[2022-12-22 13:10:32] Best translation 40 : ម ុ យ រ ា ស ី
[2022-12-22 13:10:32] Best translation 80 : អ ន ុ ព ័ ន ្ ធ ព ា ណ ិ ជ
[2022-12-22 13:10:32] Best translation 160 : ឥ ត ប ី ប ្ រ ៀ ប
[2022-12-22 13:10:32] Best translation 320 : ក ្ រ ង ជ រ
[2022-12-22 13:10:32] Best translation 640 : ព េ ល ព ្ រ េ ន
[2022-12-22 13:10:33] Best translation 1280 : ញ ា ក ់
[2022-12-22 13:10:35] Best translation 2560 : គ ហ ប ត ី
[2022-12-22 13:10:39] Best translation 5120 : ស ម ្ ប ុ ក
[2022-12-22 13:10:46] Best translation 10240 : ត ្ រ ោ ះ
[2022-12-22 13:10:54] Total translation time: 22.84298s
[2022-12-22 13:10:54] [valid] Ep. 39 : Up. 35000 : bleu : 85.3889 : new best
[2022-12-22 13:12:06] Ep. 39 : Up. 35500 : Sen. 102,400 : Cost 0.38027531 * 769,192 @ 1,904 after 54,263,091 : Time 149.83s : 5133.62 words/s : gNorm 0.6524
...
...
...
[2022-12-22 18:58:47] [valid] Ep. 180 : Up. 165000 : cross-entropy : 1.97484 : stalled 10 times (last best: 1.93207)
[2022-12-22 18:59:02] [valid] Ep. 180 : Up. 165000 : perplexity : 1.22385 : stalled 10 times (last best: 1.2185)
[2022-12-22 18:59:02] Translating validation set...
[2022-12-22 18:59:02] Best translation 0 : ក ្ រ ហ ម ឆ ្ អ ិ ន
[2022-12-22 18:59:02] Best translation 1 : គ ន ្ ថ ច រ ន ា
[2022-12-22 18:59:02] Best translation 2 : ទ ស ្ ស ន ិ ក ជ ន
[2022-12-22 18:59:02] Best translation 3 : ឯ ក ា ឯ ក ោ
[2022-12-22 18:59:02] Best translation 4 : ព ្ រ ូ ឡ ា ន
[2022-12-22 18:59:02] Best translation 5 : ឈ ូ ក ច ្ រ ា ល
[2022-12-22 18:59:02] Best translation 10 : ស ្ ង ួ ន ព ្ រ ល ឹ ង
[2022-12-22 18:59:02] Best translation 20 : ម ៉ ា ក ្ ម េ ក
[2022-12-22 18:59:02] Best translation 40 : ម ុ យ រ ា ម
[2022-12-22 18:59:02] Best translation 80 : អ ន ុ ព ័ ន ្ ធ ព ា ណ ិ ជ
[2022-12-22 18:59:02] Best translation 160 : ឥ ត ប ី ប ្ រ ៀ ប
[2022-12-22 18:59:02] Best translation 320 : ក ្ រ ង ជ រ
[2022-12-22 18:59:03] Best translation 640 : ព េ ល ព ្ រ េ ច
[2022-12-22 18:59:04] Best translation 1280 : ញ ា ត ក ា
[2022-12-22 18:59:06] Best translation 2560 : គ ហ ប ត ី
[2022-12-22 18:59:09] Best translation 5120 : ស ម ្ ប ុ ក
[2022-12-22 18:59:17] Best translation 10240 : ត ្ រ ោ ះ
[2022-12-22 18:59:24] Total translation time: 22.87907s
[2022-12-22 18:59:24] [valid] Ep. 180 : Up. 165000 : bleu : 88.963 : stalled 1 times (last best: 89.0247)
[2022-12-22 18:59:24] Training finished
[2022-12-22 18:59:24] Saving model weights and runtime parameters to model.seq2seq.dict/model.npz
[2022-12-22 18:59:30] Saving Adam parameters
[2022-12-22 18:59:33] [training] Saving training checkpoint to model.seq2seq.dict/model.npz and model.seq2seq.dict/model.npz.optimizer.npz

real    443m56.961s
user    433m58.504s
sys     5m34.948s
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq#
```

check the output model folders:  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.dict# ls
config.yml            model.iter135000.npz  model.iter25000.npz  model.iter65000.npz    model.npz.optimizer.npz
model.iter10000.npz   model.iter140000.npz  model.iter30000.npz  model.iter70000.npz    model.npz.progress.yml
model.iter100000.npz  model.iter145000.npz  model.iter35000.npz  model.iter75000.npz    model.npz.yml
model.iter105000.npz  model.iter15000.npz   model.iter40000.npz  model.iter80000.npz    s2s.er-cr.log1
model.iter110000.npz  model.iter150000.npz  model.iter45000.npz  model.iter85000.npz    train.log
model.iter115000.npz  model.iter155000.npz  model.iter5000.npz   model.iter90000.npz    valid.log
model.iter120000.npz  model.iter160000.npz  model.iter50000.npz  model.iter95000.npz
model.iter125000.npz  model.iter165000.npz  model.iter55000.npz  model.npz
model.iter130000.npz  model.iter20000.npz   model.iter60000.npz  model.npz.decoder.yml
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.dict#
```

check the validation log file:  

```
[2022-12-22 11:50:06] [valid] Ep. 6 : Up. 5000 : cross-entropy : 5.20654 : new best
[2022-12-22 11:50:20] [valid] Ep. 6 : Up. 5000 : perplexity : 1.70328 : new best
[2022-12-22 11:50:20] [valid] First sentence's tokens as scored:
[2022-12-22 11:50:20] [valid] DefaultVocab keeps original segments for scoring
[2022-12-22 11:50:20] [valid]   Hyp:  ^~^`  ^~^t  ^=^r  ^~^o  ^~^z  ^~   ^~^t  ^~^o  ^=^r  ^~^o  ^~   ^~^`  ^~   ^~^z  ^~^t  >
[2022-12-22 11:50:20] [valid]   Ref:  ^~^t  ^=^r  ^~^z  ^~^o  ^~   ^~^t  ^~^o  ^=^r  ^~^o  ^~   ^~^`  ^~   ^~^z  ^~^t  ^=^d  >
[2022-12-22 11:50:43] [valid] Ep. 6 : Up. 5000 : bleu : 70.7407 : new best
[2022-12-22 12:03:26] [valid] Ep. 11 : Up. 10000 : cross-entropy : 3.47888 : new best
[2022-12-22 12:03:41] [valid] Ep. 11 : Up. 10000 : perplexity : 1.42738 : new best
[2022-12-22 12:04:03] [valid] Ep. 11 : Up. 10000 : bleu : 78.3459 : new best
[2022-12-22 12:16:47] [valid] Ep. 17 : Up. 15000 : cross-entropy : 2.9533 : new best
[2022-12-22 12:17:01] [valid] Ep. 17 : Up. 15000 : perplexity : 1.35267 : new best
[2022-12-22 12:17:24] [valid] Ep. 17 : Up. 15000 : bleu : 81.1392 : new best
[2022-12-22 12:30:08] [valid] Ep. 22 : Up. 20000 : cross-entropy : 2.65802 : new best
[2022-12-22 12:30:22] [valid] Ep. 22 : Up. 20000 : perplexity : 1.31243 : new best
[2022-12-22 12:30:45] [valid] Ep. 22 : Up. 20000 : bleu : 82.7804 : new best
[2022-12-22 12:43:30] [valid] Ep. 28 : Up. 25000 : cross-entropy : 2.45286 : new best
[2022-12-22 12:43:44] [valid] Ep. 28 : Up. 25000 : perplexity : 1.28517 : new best
[2022-12-22 12:44:07] [valid] Ep. 28 : Up. 25000 : bleu : 83.9255 : new best
[2022-12-22 12:56:54] [valid] Ep. 33 : Up. 30000 : cross-entropy : 2.31424 : new best
[2022-12-22 12:57:09] [valid] Ep. 33 : Up. 30000 : perplexity : 1.26708 : new best
[2022-12-22 12:57:31] [valid] Ep. 33 : Up. 30000 : bleu : 84.6845 : new best
[2022-12-22 13:10:17] [valid] Ep. 39 : Up. 35000 : cross-entropy : 2.21984 : new best
[2022-12-22 13:10:31] [valid] Ep. 39 : Up. 35000 : perplexity : 1.2549 : new best
[2022-12-22 13:10:54] [valid] Ep. 39 : Up. 35000 : bleu : 85.3889 : new best
[2022-12-22 13:23:43] [valid] Ep. 44 : Up. 40000 : cross-entropy : 2.14479 : new best
[2022-12-22 13:23:57] [valid] Ep. 44 : Up. 40000 : perplexity : 1.24531 : new best
[2022-12-22 13:24:20] [valid] Ep. 44 : Up. 40000 : bleu : 85.8426 : new best
[2022-12-22 13:37:10] [valid] Ep. 50 : Up. 45000 : cross-entropy : 2.0951 : new best
[2022-12-22 13:37:24] [valid] Ep. 50 : Up. 45000 : perplexity : 1.23899 : new best
[2022-12-22 13:37:47] [valid] Ep. 50 : Up. 45000 : bleu : 86.195 : new best
[2022-12-22 13:50:35] [valid] Ep. 55 : Up. 50000 : cross-entropy : 2.05609 : new best
[2022-12-22 13:50:49] [valid] Ep. 55 : Up. 50000 : perplexity : 1.23406 : new best
[2022-12-22 13:51:12] [valid] Ep. 55 : Up. 50000 : bleu : 86.6915 : new best
[2022-12-22 14:03:56] [valid] Ep. 60 : Up. 55000 : cross-entropy : 2.02559 : new best
[2022-12-22 14:04:11] [valid] Ep. 60 : Up. 55000 : perplexity : 1.23022 : new best
[2022-12-22 14:04:34] [valid] Ep. 60 : Up. 55000 : bleu : 86.9458 : new best
[2022-12-22 14:17:18] [valid] Ep. 66 : Up. 60000 : cross-entropy : 2.00121 : new best
[2022-12-22 14:17:32] [valid] Ep. 66 : Up. 60000 : perplexity : 1.22715 : new best
[2022-12-22 14:17:55] [valid] Ep. 66 : Up. 60000 : bleu : 87.1345 : new best
[2022-12-22 14:30:42] [valid] Ep. 71 : Up. 65000 : cross-entropy : 1.98565 : new best
[2022-12-22 14:30:56] [valid] Ep. 71 : Up. 65000 : perplexity : 1.2252 : new best
[2022-12-22 14:31:19] [valid] Ep. 71 : Up. 65000 : bleu : 87.2903 : new best
[2022-12-22 14:44:05] [valid] Ep. 77 : Up. 70000 : cross-entropy : 1.97691 : new best
[2022-12-22 14:44:20] [valid] Ep. 77 : Up. 70000 : perplexity : 1.2241 : new best
[2022-12-22 14:44:43] [valid] Ep. 77 : Up. 70000 : bleu : 87.3984 : new best
[2022-12-22 14:57:28] [valid] Ep. 82 : Up. 75000 : cross-entropy : 1.96783 : new best
[2022-12-22 14:57:42] [valid] Ep. 82 : Up. 75000 : perplexity : 1.22297 : new best
[2022-12-22 14:58:05] [valid] Ep. 82 : Up. 75000 : bleu : 87.6349 : new best
[2022-12-22 15:10:50] [valid] Ep. 88 : Up. 80000 : cross-entropy : 1.95954 : new best
[2022-12-22 15:11:05] [valid] Ep. 88 : Up. 80000 : perplexity : 1.22193 : new best
[2022-12-22 15:11:28] [valid] Ep. 88 : Up. 80000 : bleu : 87.7728 : new best
[2022-12-22 15:24:12] [valid] Ep. 93 : Up. 85000 : cross-entropy : 1.95082 : new best
[2022-12-22 15:24:27] [valid] Ep. 93 : Up. 85000 : perplexity : 1.22084 : new best
[2022-12-22 15:24:50] [valid] Ep. 93 : Up. 85000 : bleu : 87.9268 : new best
[2022-12-22 15:37:35] [valid] Ep. 99 : Up. 90000 : cross-entropy : 1.94329 : new best
[2022-12-22 15:37:49] [valid] Ep. 99 : Up. 90000 : perplexity : 1.2199 : new best
[2022-12-22 15:38:12] [valid] Ep. 99 : Up. 90000 : bleu : 88.0939 : new best
[2022-12-22 15:50:58] [valid] Ep. 104 : Up. 95000 : cross-entropy : 1.94034 : new best
[2022-12-22 15:51:12] [valid] Ep. 104 : Up. 95000 : perplexity : 1.21954 : new best
[2022-12-22 15:51:35] [valid] Ep. 104 : Up. 95000 : bleu : 88.1393 : new best
[2022-12-22 16:04:23] [valid] Ep. 109 : Up. 100000 : cross-entropy : 1.93781 : new best
[2022-12-22 16:04:37] [valid] Ep. 109 : Up. 100000 : perplexity : 1.21922 : new best
[2022-12-22 16:05:00] [valid] Ep. 109 : Up. 100000 : bleu : 88.2966 : new best
[2022-12-22 16:17:45] [valid] Ep. 115 : Up. 105000 : cross-entropy : 1.93377 : new best
[2022-12-22 16:18:00] [valid] Ep. 115 : Up. 105000 : perplexity : 1.21872 : new best
[2022-12-22 16:18:23] [valid] Ep. 115 : Up. 105000 : bleu : 88.3839 : new best
[2022-12-22 16:31:10] [valid] Ep. 120 : Up. 110000 : cross-entropy : 1.93213 : new best
[2022-12-22 16:31:24] [valid] Ep. 120 : Up. 110000 : perplexity : 1.21851 : new best
[2022-12-22 16:31:47] [valid] Ep. 120 : Up. 110000 : bleu : 88.5008 : new best
[2022-12-22 16:44:36] [valid] Ep. 126 : Up. 115000 : cross-entropy : 1.93207 : new best
[2022-12-22 16:44:51] [valid] Ep. 126 : Up. 115000 : perplexity : 1.2185 : new best
[2022-12-22 16:45:14] [valid] Ep. 126 : Up. 115000 : bleu : 88.6237 : new best
[2022-12-22 16:58:01] [valid] Ep. 131 : Up. 120000 : cross-entropy : 1.93627 : stalled 1 times (last best: 1.93207)
[2022-12-22 16:58:16] [valid] Ep. 131 : Up. 120000 : perplexity : 1.21903 : stalled 1 times (last best: 1.2185)
[2022-12-22 16:58:39] [valid] Ep. 131 : Up. 120000 : bleu : 88.6263 : new best
[2022-12-22 17:11:30] [valid] Ep. 137 : Up. 125000 : cross-entropy : 1.94097 : stalled 2 times (last best: 1.93207)
[2022-12-22 17:11:45] [valid] Ep. 137 : Up. 125000 : perplexity : 1.21961 : stalled 2 times (last best: 1.2185)
[2022-12-22 17:12:08] [valid] Ep. 137 : Up. 125000 : bleu : 88.731 : new best
[2022-12-22 17:24:53] [valid] Ep. 142 : Up. 130000 : cross-entropy : 1.94501 : stalled 3 times (last best: 1.93207)
[2022-12-22 17:25:07] [valid] Ep. 142 : Up. 130000 : perplexity : 1.22012 : stalled 3 times (last best: 1.2185)
[2022-12-22 17:25:30] [valid] Ep. 142 : Up. 130000 : bleu : 88.7013 : stalled 1 times (last best: 88.731)
[2022-12-22 17:38:16] [valid] Ep. 148 : Up. 135000 : cross-entropy : 1.95107 : stalled 4 times (last best: 1.93207)
[2022-12-22 17:38:31] [valid] Ep. 148 : Up. 135000 : perplexity : 1.22087 : stalled 4 times (last best: 1.2185)
[2022-12-22 17:38:54] [valid] Ep. 148 : Up. 135000 : bleu : 88.7047 : stalled 2 times (last best: 88.731)
[2022-12-22 17:51:41] [valid] Ep. 153 : Up. 140000 : cross-entropy : 1.94985 : stalled 5 times (last best: 1.93207)
[2022-12-22 17:51:55] [valid] Ep. 153 : Up. 140000 : perplexity : 1.22072 : stalled 5 times (last best: 1.2185)
[2022-12-22 17:52:18] [valid] Ep. 153 : Up. 140000 : bleu : 88.7429 : new best
[2022-12-22 18:05:06] [valid] Ep. 159 : Up. 145000 : cross-entropy : 1.95559 : stalled 6 times (last best: 1.93207)
[2022-12-22 18:05:20] [valid] Ep. 159 : Up. 145000 : perplexity : 1.22144 : stalled 6 times (last best: 1.2185)
[2022-12-22 18:05:43] [valid] Ep. 159 : Up. 145000 : bleu : 88.8451 : new best
[2022-12-22 18:18:31] [valid] Ep. 164 : Up. 150000 : cross-entropy : 1.96081 : stalled 7 times (last best: 1.93207)
[2022-12-22 18:18:45] [valid] Ep. 164 : Up. 150000 : perplexity : 1.22209 : stalled 7 times (last best: 1.2185)
[2022-12-22 18:19:08] [valid] Ep. 164 : Up. 150000 : bleu : 88.9434 : new best
[2022-12-22 18:31:57] [valid] Ep. 169 : Up. 155000 : cross-entropy : 1.96563 : stalled 8 times (last best: 1.93207)
[2022-12-22 18:32:11] [valid] Ep. 169 : Up. 155000 : perplexity : 1.22269 : stalled 8 times (last best: 1.2185)
[2022-12-22 18:32:34] [valid] Ep. 169 : Up. 155000 : bleu : 88.9658 : new best
[2022-12-22 18:45:22] [valid] Ep. 175 : Up. 160000 : cross-entropy : 1.96813 : stalled 9 times (last best: 1.93207)
[2022-12-22 18:45:36] [valid] Ep. 175 : Up. 160000 : perplexity : 1.22301 : stalled 9 times (last best: 1.2185)
[2022-12-22 18:45:59] [valid] Ep. 175 : Up. 160000 : bleu : 89.0247 : new best
[2022-12-22 18:58:47] [valid] Ep. 180 : Up. 165000 : cross-entropy : 1.97484 : stalled 10 times (last best: 1.93207)
[2022-12-22 18:59:02] [valid] Ep. 180 : Up. 165000 : perplexity : 1.22385 : stalled 10 times (last best: 1.2185)
[2022-12-22 18:59:24] [valid] Ep. 180 : Up. 165000 : bleu : 88.963 : stalled 1 times (last best: 89.0247)
```

## Testing/Evaluation for Seq2Seq Dictionary Model  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Khmer spelling correction
## used Marian NMT Framework for training
## Last updated: 23 December 2022

data_path="/home/ye/exp/kh-spell/seq2seq/4nmt/char-segment/";
src="er"; tgt="cr";

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output hyp.best.manual.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.manual.${tgt}, Seq2Seq dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "==========" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output hyp.best.edit1.${tgt} < ${data_path}/edit1/test.${src};
echo "Evaluation with hyp.best.edit1.${tgt}, Seq2Seq dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit1/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;

echo "==========" >> eval-best-result.txt;

time marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output hyp.best.edit2.${tgt} < ${data_path}/edit2/test.${src};
echo "Evaluation with hyp.best.edit2.${tgt}, Seq2Seq dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit2/test.${tgt} < ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

testing ...  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.dict# ./test-eval-best.sh | tee test.log
...
...
...
[2022-12-23 01:20:26] Best translation 978 : ច ង ្ អ ា ម
[2022-12-23 01:20:26] Best translation 979 : ផ ្ ល ូ វ ប ែ ក ជ ា ប ួ ន
[2022-12-23 01:20:26] Best translation 980 : ដ ា ក ់ ស ំ ញ ៉ ែ ង
[2022-12-23 01:20:26] Best translation 981 : ជ ា ក ្ ម េ ង
[2022-12-23 01:20:26] Best translation 982 : យ ុ ត ្ ត វ ា ទ ី
[2022-12-23 01:20:26] Best translation 983 : ដ ា ក ់ ថ ្ ន ា ំ ខ ្ ល ា ំ ង
[2022-12-23 01:20:26] Best translation 984 : ស ូ ម
[2022-12-23 01:20:26] Best translation 985 : ភ ្ ញ ច ់
[2022-12-23 01:20:26] Best translation 986 : ន ិ យ ា យ ប ៉ ប ៉ ា ច ់
[2022-12-23 01:20:26] Best translation 987 : ក ្ ត ឿ ង ខ ្ ញ ី
[2022-12-23 01:20:26] Best translation 988 : ទ ំ ហ ែ ង
[2022-12-23 01:20:26] Best translation 989 : ល ល ា ម
[2022-12-23 01:20:26] Best translation 990 : ប ច ្ ជ ិ ម យ ា ម
[2022-12-23 01:20:26] Best translation 991 : ល ្ ង ខ ្ ម ៅ
[2022-12-23 01:20:26] Best translation 992 : អ ា ហ ា រ ប ្ រ អ ប ់
[2022-12-23 01:20:26] Best translation 993 : រ ូ ប ព ្ រ ហ ្ ម
[2022-12-23 01:20:26] Best translation 994 : អ ហ ិ ត ក ៈ
[2022-12-23 01:20:26] Best translation 995 : ស ្ រ ម ក
[2022-12-23 01:20:26] Best translation 996 : ប ៉ ប ៉ ិ ក ប ៉ ប ា ក ់
[2022-12-23 01:20:26] Best translation 997 : ក ែ វ វ ៉ ែ ន ត ា
[2022-12-23 01:20:26] Best translation 998 : ឧ ប ្ ប ត ្ ត ិ ភ ូ ម ិ
[2022-12-23 01:20:26] Best translation 999 : ឡ េ ស ូ ត ូ
[2022-12-23 01:20:26] Total time: 20.93162s wall

real    0m22.714s
user    0m20.762s
sys     0m1.982s
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.
```

check the evaluation results with three test datasets:  

```
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.dict# cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Seq2Seq dictionary model:
BLEU = 87.97, 93.5/89.0/86.1/83.6 (BP=1.000, ratio=1.001, hyp_len=6910, ref_len=6900)
==========
Evaluation with hyp.best.edit1.cr, Seq2Seq dictionary model:
BLEU = 92.57, 96.5/93.0/91.0/89.9 (BP=1.000, ratio=1.004, hyp_len=8883, ref_len=8851)
==========
Evaluation with hyp.best.edit2.cr, Seq2Seq dictionary model:
BLEU = 88.30, 94.5/88.5/86.0/84.8 (BP=0.999, ratio=0.999, hyp_len=8954, ref_len=8964)
root@0d441b235700:/home/ye/exp/kh-spell/seq2seq/model.seq2seq.dict#
```

## Results Summary

To Do: When I have time, I wanna make a results summary ...  

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

