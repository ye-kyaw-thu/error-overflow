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


```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

