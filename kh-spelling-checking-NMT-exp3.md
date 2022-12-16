# Seq2Seq Model Experiments

For this time, I will build Seq2Seq NMT model for Khmer spelling checking...  

## Preprocessing

create a new folder for Seq2Seq experiment:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell# mkdir seq2seq
root@7a2ffa404585:/home/ye/exp/kh-spell# cd seq2seq/
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq# cp -r ../transformer/4nmt/ .
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq# cd 4nmt
```

data and vocab file info are as follows:  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt# ls
edit1  edit2  no-segment  test.cr  test.er  train.cr  train.er  valid.cr  valid.er  vocab
```

check no-segment data ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt# cd no-segment/
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment# ls
char-segmentation.sh  edit1  edit2  test.cr  test.er  train.cr  train.er  valid.cr  valid.er  vocab
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment# head test.er
រុស្សស៊ី
បប៉ុនហ្នឹង
ផស់
ឆ្គួត
អី
 សាម៉ាញ
អី
 ខ្ទើយ
ឧបត្ថម
និសិត
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment# cd edit1
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment/edit1# ls
test.cr  test.er
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment/edit1# head test.cr
ក្រសារ
វិត
ក្របែល
រាងបួនជ្រុង
អមិត
បង្កាត់ភ្លើង
ស្រែក្រសាំង
អ្នករកសស៊ីលក់ដូរដីធ្លីផ្ទះសំបែង
ពង្វិល
គណៈមហានិកាយ
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/no-segment/edit1#
```

When I checked edit1 data ...  

```
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt# cd edit1
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/edit1# ls
test.cr  test.er
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/edit1# head test.cr
� � � � � � � � � � � � � � � � � �
� � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
root@7a2ffa404585:/home/ye/exp/kh-spell/seq2seq/4nmt/edit1#
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

