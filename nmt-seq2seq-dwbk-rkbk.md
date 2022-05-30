# Seq2Seq Archi for NMT Baseline

## Data Information

10-folds data for dw-bk language pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$ for i in {1..10}; do echo "path: $i/"; wc ./$i/*.{dw,bk}; done;
path: 1/
    500    3032   48817 ./1/dev.dw
    670    4013   64228 ./1/test.dw
   5452   32614  524213 ./1/train.dw
    500    3213   46186 ./1/dev.bk
    670    4267   60615 ./1/test.bk
   5452   34473  494687 ./1/train.bk
  13244   81612 1238746 total
path: 2/
    500    3032   48817 ./2/dev.dw
    670    4030   65195 ./2/test.dw
   5452   32597  523246 ./2/train.dw
    500    3213   46186 ./2/dev.bk
    670    4295   61799 ./2/test.bk
   5452   34445  493503 ./2/train.bk
  13244   81612 1238746 total
path: 3/
    500    3032   48817 ./3/dev.dw
    670    3998   65039 ./3/test.dw
   5452   32629  523402 ./3/train.dw
    500    3213   46186 ./3/dev.bk
    670    4284   61312 ./3/test.bk
   5452   34456  493990 ./3/train.bk
  13244   81612 1238746 total
path: 4/
    500    3032   48817 ./4/dev.dw
    670    4012   64983 ./4/test.dw
   5452   32615  523458 ./4/train.dw
    500    3213   46186 ./4/dev.bk
    670    4137   60685 ./4/test.bk
   5452   34603  494617 ./4/train.bk
  13244   81612 1238746 total
path: 5/
    500    3032   48817 ./5/dev.dw
    670    4011   63713 ./5/test.dw
   5452   32616  524728 ./5/train.dw
    500    3213   46186 ./5/dev.bk
    670    4188   61079 ./5/test.bk
   5452   34552  494223 ./5/train.bk
  13244   81612 1238746 total
path: 6/
    500    3032   48817 ./6/dev.dw
    670    4042   64120 ./6/test.dw
   5452   32585  524321 ./6/train.dw
    500    3213   46186 ./6/dev.bk
    670    4276   60268 ./6/test.bk
   5452   34464  495034 ./6/train.bk
  13244   81612 1238746 total
path: 7/
    500    3032   48817 ./7/dev.dw
    670    4025   63846 ./7/test.dw
   5452   32602  524595 ./7/train.dw
    500    3213   46186 ./7/dev.bk
    670    4279   60287 ./7/test.bk
   5452   34461  495015 ./7/train.bk
  13244   81612 1238746 total
path: 8/
    500    3032   48817 ./8/dev.dw
    670    3993   65355 ./8/test.dw
   5452   32634  523086 ./8/train.dw
    500    3213   46186 ./8/dev.bk
    670    4235   60716 ./8/test.bk
   5452   34505  494586 ./8/train.bk
  13244   81612 1238746 total
path: 9/
    500    3032   48817 ./9/dev.dw
    670    3985   63827 ./9/test.dw
   5452   32642  524614 ./9/train.dw
    500    3213   46186 ./9/dev.bk
    670    4245   60518 ./9/test.bk
   5452   34495  494784 ./9/train.bk
  13244   81612 1238746 total
 path: 10/
    500    2946   47560 ./10/dev.dw
    592    3550   56952 ./10/test.dw
   5530   33163  532746 ./10/train.dw
    500    3164   45302 ./10/dev.bk
    592    3747   54209 ./10/test.bk
   5530   35042  501977 ./10/train.bk
  13244   81612 1238746 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$
```

```

```

```

```

```

```

```

```

```

```
