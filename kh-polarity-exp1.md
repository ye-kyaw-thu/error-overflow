# Khmer Polarity Classification Experiment-1

## Checking on Manually Created Polarity Corpus

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 1 > 805.col1.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 2 > 805.col2.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 3 > 805.col3.txt
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 168.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 168.
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 217.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 217.
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 222.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 222.
```

## Cleaned Data Information

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ ls700.txt  805.txt  8.5k.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ cat 8.5k.txt 700.txt 805.txt > ./kh-polar.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ wc ./kh-polar.txt 
  10015  101462 5705194 ./kh-polar.txt
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
