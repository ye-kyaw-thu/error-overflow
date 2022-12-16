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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

