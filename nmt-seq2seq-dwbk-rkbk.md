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

data info for rk-bk language pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$ for i in {1..10}; do echo "path: $i/"; wc ./$i/*.{rk,bk}; done;
path: 1/
    800    5175   85367 ./1/dev.rk
   1072    6739  110724 ./1/test.rk
   8850   57071  927947 ./1/train.rk
    800    5306   79716 ./1/dev.bk
   1072    6956  103337 ./1/test.bk
   8850   58185  864939 ./1/train.bk
  21444  139432 2172030 total
path: 2/
    800    5175   85367 ./2/dev.rk
   1072    7004  115305 ./2/test.rk
   8850   56806  923366 ./2/train.rk
    800    5306   79716 ./2/dev.bk
   1072    7142  107707 ./2/test.bk
   8850   57999  860569 ./2/train.bk
  21444  139432 2172030 total
path: 3/
    800    5175   85367 ./3/dev.rk
   1072    7019  114329 ./3/test.rk
   8850   56791  924342 ./3/train.rk
    800    5306   79716 ./3/dev.bk
   1072    7152  106704 ./3/test.bk
   8850   57989  861572 ./3/train.bk
  21444  139432 2172030 total
path: 4/
    800    5175   85367 ./4/dev.rk
   1072    6796  109356 ./4/test.rk
   8850   57014  929315 ./4/train.rk
    800    5306   79716 ./4/dev.bk
   1072    6905  101225 ./4/test.bk
   8850   58236  867051 ./4/train.bk
  21444  139432 2172030 total
path: 5/
    800    5175   85367 ./5/dev.rk
   1072    6851  109765 ./5/test.rk
   8850   56959  928906 ./5/train.rk
    800    5306   79716 ./5/dev.bk
   1072    7007  102834 ./5/test.bk
   8850   58134  865442 ./5/train.bk
  21444  139432 2172030 total
path: 6/
    800    5175   85367 ./6/dev.rk
   1072    6798  112415 ./6/test.rk
   8850   57012  926256 ./6/train.rk
    800    5306   79716 ./6/dev.bk
   1072    6982  104609 ./6/test.bk
   8850   58159  863667 ./6/train.bk
  21444  139432 2172030 total
path: 7/
    800    5175   85367 ./7/dev.rk
   1072    7021  112493 ./7/test.rk
   8850   56789  926178 ./7/train.rk
    800    5306   79716 ./7/dev.bk
   1072    7142  105254 ./7/test.bk
   8850   57999  863022 ./7/train.bk
  21444  139432 2172030 total
path: 8/
    800    5175   85367 ./8/dev.rk
   1072    7014  114156 ./8/test.rk
   8850   56796  924515 ./8/train.rk
    800    5306   79716 ./8/dev.bk
   1072    7149  106394 ./8/test.bk
   8850   57992  861882 ./8/train.bk
  21444  139432 2172030 total
path: 9/
    800    5175   85367 ./9/dev.rk
   1072    6830  110901 ./9/test.rk
   8850   56980  927770 ./9/train.rk
    800    5306   79716 ./9/dev.bk
   1072    6918  103287 ./9/test.bk
   8850   58223  864989 ./9/train.bk
  21444  139432 2172030 total
path: 10/
    800    5128   83237 ./10/dev.rk
   1072    6898  114428 ./10/test.rk
   8850   56959  926373 ./10/train.rk
    800    5173   77217 ./10/dev.bk
   1072    7081  106504 ./10/test.bk
   8850   58193  864271 ./10/train.bk
  21444  139432 2172030 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$
```


```

```

```

```

```

```

```

```
