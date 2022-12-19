# Seq2Seq Model Experiments

For this time, I will build Seq2Seq NMT model for Khmer spelling checking...  

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

```

```

```

```

```

```

```

```

```

