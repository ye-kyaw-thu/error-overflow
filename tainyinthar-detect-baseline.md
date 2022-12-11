# Baseline

## FastText to CSV Format Conversion

I defined labels as follows:  

```
__label__bk = 1
__label__dw = 2
__label__my = 3
__label__rk = 4
```

I used following sed command:  

```bash
sed -e 's/__label__bk /1\t/' -e 's/__label__dw /2\t/' -e 's/__label__my /3\t/' -e 's/__label__rk /4\t/' ./test.shuf.all > test.shuf.csv
```

Run for test file:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ sed -e 's/__label__bk /1\t/' -e 's/__label__dw /2\t/' -e 's/__label__my /3\t/' -e 's/__label__rk /4\t/' ./test.shuf.all > test.shuf.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ head test.shuf.csv
4	 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။
3	 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။
4	 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။
2	ကျွန် တော် မွန်း လန်း ဇာ စား နေ တူး ဟှ သူ ဖောင်း ပြော နေ ဟှယ် ။
1	အ မှား လုပ် ဝယ့် ကျောင်း သား ဒေ ဝို ဆ ရာ ဂ ရိုက် ရယ် ။
3	 ခင် ဗျား မှာ ကျွန် တော့် နံ ပါတ် ရှိ တယ် လေ ။
4	 ဒေ က လိန့် မေ စွာ စိတ် ရှုပ် လား ဗျာယ် ။
3	 သူ တို့ က ဝံ ပု လွေ ကြီး ထွက် ပြေး အောင် ပန်း သီး တွေ နဲ့ ဗုံး ကြဲ သ လို ပစ် ပေါက် ကြ တယ် ။
4	 ဒေ မာ ငါး မျှား စွာ ကို ခွ င့် မ ပြု ပါ ။
1	အယ့် ဒါ ဘ ဇာ လောက် ထင် ရှား ရိ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$
```

Run for training data as follows:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ sed -e 's/__label__bk /1\t/' -e 's/__label__dw /2\t/' -e 's/__label__my /3\t/' -e 's/__label__rk /4\t/' ./train.shuf.all > train.shuf.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ head train.shuf.csv
2	နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။
3	 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။
3	 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။
3	 ဒါ ဘယ် သူ့ သွား တိုက် ဆေး လဲ ။
3	 ဘယ် အ ချိန် ငွေ လာ ပေး ရ မ လဲ ဆို တာ ကျွန် တော် စဉ်း စား နေ တယ် ။
4	 ယင်း ချင့် ဇာ လောက် တန် ဖိုး ဟိ လေး ။
3	 ငါ အိပ် ချင် တယ် ဒါ ပေ မ ယ့် မ အိပ် နိုင် ဘူး ။
4	 ဂီ တ ဟာ မြူး ကြွ စီ ရေ အ ထိ အ ရှိန် မြ င့် ခ ရေ ။
3	 ကျွန် တော် တို့ အဲ ဒါ ကို တောင်း ဆို ထား လား ။
2	တ ပည့် ဂန်း များ ရ စာ ရေး တတ် ဝို့ နဲ့ ဖတ် တက် ဝို့ သန် ယူ နေ ရယ် ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ 
```

Confirmation of filesize:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ wc train.*
   45026   586952  5647995 train.shuf.all
   45026   586952  5197735 train.shuf.csv
   90052  1173904 10845730 total
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ wc test.*
   4964   65253  628176 test.shuf.all
   4964   65253  578536 test.shuf.csv
   9928  130506 1206712 total
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ 
```

## Swap Two Columns

for training data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ cut -f1 ./train.shuf.csv > f1.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ cut -f2 ./train.shuf.csv > f2.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ wc {f1,f2}.csv
  45026   45026   90052 f1.csv
  45026  541926 5107683 f2.csv
  90052  586952 5197735 total
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ paste -d "," f2.csv f1.(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ paste -d "," f2.csv f1.csv > train.final.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ head -n 3 ./train.final.csv 
နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။,2
 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။,3
 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။,3
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$
```

swap two columns for test data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ cut -f1 ./test.shuf.csv > f1.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ cut -f2 ./test.shuf.csv > f2.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ paste -d "," f2.csv f1.csv > test.final.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$ head -n 3 ./test.final.csv 
 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။,4
 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။,3
 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။,4
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv$
```

## Prepared Another CSV version

လူအနေနဲ့ ကြည့်ရတာက 1,2,3,4 ထက် bk,dw,my,rk က ပိုအဆင်ပြေလို့ နောက်ထပ် format version တစ်ခုလည်း ပြင်ဆင်ထားခဲ့တယ်။  

for test file:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ sed -e 's/__label__bk /bk\t/' -e 's/__label__dw /dw\t/' -e 's/__label__my /my\t/' -e 's/__label__rk /rk\t/' ./test.shuf.all > test.shuf-txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n 3 ./test.shuf-txt.csv 
rk	 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။
my	 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။
rk	 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ 
```

for training file:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ sed -e 's/__label__bk /bk\t/' -e 's/__label__dw /dw\t/' -e 's/__label__my /my\t/' -e 's/__label__rk /rk\t/' ./train.shuf.all > train.shuf-txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head train.shuf-txt.csv 
dw	နန့် ကီး မွန်း တည့် နူး ဟှ ကျန် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။
my	 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။
my	 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။
my	 ဒါ ဘယ် သူ့ သွား တိုက် ဆေး လဲ ။
my	 ဘယ် အ ချိန် ငွေ လာ ပေး ရ မ လဲ ဆို တာ ကျွန် တော် စဉ်း စား နေ တယ် ။
rk	 ယင်း ချင့် ဇာ လောက် တန် ဖိုး ဟိ လေး ။
my	 ငါ အိပ် ချင် တယ် ဒါ ပေ မ ယ့် မ အိပ် နိုင် ဘူး ။
rk	 ဂီ တ ဟာ မြူး ကြွ စီ ရေ အ ထိ အ ရှိန် မြ င့် ခ ရေ ။
my	 ကျွန် တော် တို့ အဲ ဒါ ကို တောင်း ဆို ထား လား ။
dw	တ ပည့် ဂန်း များ ရ စာ ရေး တတ် ဝို့ နဲ့ ဖတ် တက် ဝို့ သန် ယူ နေ ရယ် ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

swap two columns for training data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ ls
test.shuf.all  test.shuf-txt.csv  train.shuf.all  train.shuf-txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f1 ./train.shuf-txt.csv > f1
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f2 ./train.shuf-txt.csv > f2
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ paste -d "," f2 f1 > train.txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n 3 ./train.txt.csv 
နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။,dw
 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။,my
 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။,my
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ 
```

swap two columns for test data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f1 ./test.shuf-txt.csv > f1
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f2 ./test.shuf-txt.csv > f2
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ paste -d "," f2 f1 > test.txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n 3 ./test.txt.csv 
 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။,rk
 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။,my
 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။,rk
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

Moved to the Python scripts running folder:  

```
(base) yekyaw.thu@gpu:~/exp/dialect-detection/data/txt-csv$ ls *.csv
test.shuf-txt.csv  test.txt.csv  train.shuf-txt.csv  train.txt.csv
(base) yekyaw.thu@gpu:~/exp/dialect-detection/data/txt-csv$ cp {test,train}.txt.csv ../../scripts/csv/
```

change filename according to the python code:  

```
(base) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ ls
test.txt.csv  train.txt.csv
(base) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv train.txt.csv train.csv
(base) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv test.txt.csv test.csv
```

## KNN Result

1st time running got error message as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ time python ./knn.py 
Traceback (most recent call last):
  File "./knn.py", line 19, in <module>
    polar_train = pd.read_csv('csv/train.csv')
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/pandas/util/_decorators.py", line 311, in wrapper
    return func(*args, **kwargs)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/pandas/io/parsers/readers.py", line 586, in read_csv
    return _read(filepath_or_buffer, kwds)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/pandas/io/parsers/readers.py", line 488, in _read
    return parser.read(nrows)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/pandas/io/parsers/readers.py", line 1047, in read
    index, columns, col_dict = self._engine.read(nrows)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/pandas/io/parsers/c_parser_wrapper.py", line 224, in read
    chunks = self._reader.read_low_memory(nrows)
  File "pandas/_libs/parsers.pyx", line 801, in pandas._libs.parsers.TextReader.read_low_memory
  File "pandas/_libs/parsers.pyx", line 857, in pandas._libs.parsers.TextReader._read_rows
  File "pandas/_libs/parsers.pyx", line 843, in pandas._libs.parsers.TextReader._tokenize_rows
  File "pandas/_libs/parsers.pyx", line 1925, in pandas._libs.parsers.raise_parser_error
pandas.errors.ParserError: Error tokenizing data. C error: Expected 2 fields in line 819, saw 3


real	0m0.320s
user	0m0.360s
sys	0m0.492s
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ 
```

The reason is containing comman in the text or feature part at line no. 819 ...  

```
 ကောင် လေး က သူ့ ကို မော့ ကြ ည့် ပြီး ပြော တယ် ၊ ကဲ ကျွန် တော် တို့ ဝေး ဝေး ပြေး ကြ စို့ , လာ လာ ။,my
```

## Cleaning

Cleaning extra spaces ...  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ ls
test.shuf.all  test.shuf-txt.csv  test.txt.csv  train.shuf.all  train.shuf-txt.csv  train.txt.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f1 ./train.shuf-txt.csv > f1
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f2 ./train.shuf-txt.csv > f2
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ vi clean-space.pl
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ perl ./clean-space.pl ./f2 > f2.clean
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

### cleaning of commas

1st grep commas ...  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ grep -n "," ./f2.clean 
819:ကောင် လေး က သူ့ ကို မော့ ကြ ည့် ပြီး ပြော တယ် ၊ ကဲ ကျွန် တော် တို့ ဝေး ဝေး ပြေး ကြ စို့ , လာ လာ ။
3412:မင်း ယင်း ချင့်် ကို ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ နဲ့ ဇာ ပိုင် ရ ခ လေ ။
6507:မြို့ စား ကြီး က လယ် သ မား ကြီး ကို ဒေါ် လာ ၄ ၀ , ၀ ၀ ၀ ပေး လိ မ့် မယ် ။
7156:ခြံ ရဲ့ တန် ဘိုး အ မှန် က ဒေါ် လာ ၄ ၀ , ၀ ၀ ၀ လား ။
7492:မင်း အ ခန်း က နောက် တစ် ပတ် မှာ အ သ င့် ဖြစ် ဖို့ ၊ ယ ကေ လည်း ,င်း အ ချိန် ထိ ကျွန် တော် ရို့ နဲ့ နိန် နိုင် ပါ ယေ ။
8533:ခြံ ရဲ့ ဈေး ဟာ ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ လား ။
12854:မင်း ဒါ ကို ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ နဲ့ ဘယ် လို ရ ခဲ့ သ လဲ ။
14034:မြိုး စား ကြီး က ဒေါ် လာ ၁ ၀ , ၀ ၀ ၀ ပို့ လိုက် တေ ။
14410:​ ကျွန် တော် အဲ ဒါ ကို ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ နဲ့ ရ ခဲ့ ပါ တယ် ။
14509:ငါ ယင်း ချင့် ကို ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ နန့် ရ ခ ရေ ။
21574:လျော့ ဈီး က ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ လား ။
24255:အင်္ဂ လိပ် အ ပြင် , ကို ရီး ယား ကို လည်း သူ ရို့ ကျွမ်း ကျွမ်း ကျင် ကျင် ပြော နိုင် တယ် ။
26744:မြို့ စား ကြီး က ဒေါ် လာ ၁ ၀ , ၀ ၀ ၀ ပို့ လိုက် တယ် ။
28156:အေ ခြံ ဈီး စွာ ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ လား ။
30173:အင်္ဂ လိပ် အ ပြင် , ကို ရီး ယား ကို လည်း သူ ရို့ ကျွမ်း ကျွမ်း ကျင် ကျင် ပြော နိုင် ရေ ။
30299:အ ကျိုး ဆောင် က ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ ပီး ခ ရေ ။
32414:အ ကျိုး ဆောင် က ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ ပေး ခဲ့ တယ် ။
32906:ခြံ တန် ဖိုး အ မှန် ဂ ပေါင် ၄ ၀ , ၀ ၀ ၀ ပါ ။
34567:ခြံ ရဲ့ အ မှန် တ ကယ် တန် ဘိုး က ပေါင် ၄ ၀ , ၀ ၀ ၀ ပါ ။
35936:လျှော့ ဈေး က ဒေါ် လာ ၃ ၀ , ၀ ၀ ၀ လား ။
39243:အေ ခြံ တန် ဖိုး အ မှန် ဂ ဒေါ် လာ ၄ ၀ , ၀ ၀ ၀ လား ။
39790:မြိုး စား ကြီး က လယ် သ မား ကြီး ကို ဒေါ် လာ ၄ ၀ , ၀ ၀ ၀ ပီး လိ မ့် မေ ။
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

အထက်ပါအတိုင်း corpus ထဲမှာက comma တွေ တော်တော်ပါနေတာနဲ့ ပြီးတော့ "," ကို delimeter အဖြစ် သုံးရတာက ပြဿနာ ပေးတာများတာမို့လို့ .... comma အစား TAB ကိုပဲ သုံးဖို့ ဆုံးဖြတ်ခဲ့တယ်။  
I decided to use TAB ...  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ paste f2 f1 > train.tab.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n ./train.tab.csv 
head: invalid number of lines: ‘./train.tab.csv’
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n 5 ./train.tab.csv 
နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။	dw
 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။	my
 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။	my
 ဒါ ဘယ် သူ့ သွား တိုက် ဆေး လဲ ။	my
 ဘယ် အ ချိန် ငွေ လာ ပေး ရ မ လဲ ဆို တာ ကျွန် တော် စဉ်း စား နေ တယ် ။	my
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

cleaning spaces and prepare TAB separated file for test data:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f1 ./test.shuf-txt.csv > f1
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ cut -f2 ./test.shuf-txt.csv > f2
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ perl ./clean-space.pl ./f2 > f2.clean 
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ paste f2 f1 > test.tab.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$ head -n 5 ./test.tab.csv 
 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။	rk
 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။	my
 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။	rk
ကျွန် တော် မွန်း လန်း ဇာ စား နေ တူး ဟှ သူ ဖောင်း ပြော နေ ဟှယ် ။	dw
အ မှား လုပ် ဝယ့် ကျောင်း သား ဒေ ဝို ဆ ရာ ဂ ရိုက် ရယ် ။	bk
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/txt-csv$
```

Copied zip file to server and prepared on server as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/data/txt-csv$ cp {test,train}.tab.csv ../../scripts/csv/
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/data/txt-csv$ cd ../../scripts/csv/
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ ls
test.tab.csv  train.tab.csv
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ wc *
   4964   65253  583500 test.tab.csv
  45026  586952 5242761 train.tab.csv
  49990  652205 5826261 total
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$
```

Change filename according to the Python code:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv test.tab.csv test.csv
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv train.tab.csv train.csv
```

## Update KNN and Other Scripts 

added "sep" parameter ...  

```python
polar_train = pd.read_csv('csv/train.csv', sep="\t")
polar_test = pd.read_csv('csv/test.csv', sep="\t")
```

## Train KNN Again

Train with TAB file and got following error:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ time python ./knn.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
Traceback (most recent call last):
  File "./knn.py", line 35, in <module>
    unigram_vectorizer.fit(polar_train['text'].values)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1283, in fit
    self.fit_transform(raw_documents)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1330, in fit_transform
    vocabulary, X = self._count_vocab(raw_documents, self.fixed_vocabulary_)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1201, in _count_vocab
    for feature in analyze(doc):
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 108, in _analyze
    doc = decoder(doc)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 227, in decode
    "np.nan is an invalid document, expected byte or unicode string."
ValueError: np.nan is an invalid document, expected byte or unicode string.

real	0m0.755s
user	0m0.767s
sys	0m0.720s
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ 
```

When I refered following link:  
https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0

I found that using number label ...  

## Preparing Number Label

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ sed -e 's/bk/1/' -e 's/dw/2/' -e 's/my/3/' -e 's/rk/4/' ./train.tab.csv > train.no.csv
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ gedit train.no.csv 
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ sed -e 's/bk/1/' -e 's/dw/2/' -e 's/my/3/' -e 's/rk/4/' ./test.tab.csv > test.no.csv
```

Check the converted file:  

```
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ head -n 5 ./train.no.csv 
နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။	2
 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။	3
 သူ မ က သူ့ ကို သတ် ခဲ့ တာ လား ။	3
 ဒါ ဘယ် သူ့ သွား တိုက် ဆေး လဲ ။	3
 ဘယ် အ ချိန် ငွေ လာ ပေး ရ မ လဲ ဆို တာ ကျွန် တော် စဉ်း စား နေ တယ် ။	3
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ head -n 5 ./test.no.csv 
 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။	4
 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။	3
 ယင်း ချင့် ကို မင်း အာ မ မ ခံ ခ ပါ ။	4
ကျွန် တော် မွန်း လန်း ဇာ စား နေ တူး ဟှ သူ ဖောင်း ပြော နေ ဟှယ် ။	2
အ မှား လုပ် ဝယ့် ကျောင်း သား ဒေ ဝို ဆ ရာ ဂ ရိုက် ရယ် ။	1
(base) ye@ykt-pro:~/data/ethnic-parallel-data/4dialect-detect/preprocess/csv/number-csv$ 
```

## Replace train.csv, test.csv Files on Server

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/data/number-csv$ cp train.no.csv ../../scripts/csv/
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/data/number-csv$ cp test.no.csv ../../scripts/csv/
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/data/number-csv$ cd ../../scripts/csv/
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ ls
test.csv  test.no.csv  train.csv  train.no.csv	without-header
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ rm train.csv
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ rm test.csv
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ ls
test.no.csv  train.no.csv  without-header
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv train.no.csv train.csv
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ mv test.no.csv test.csv
```

Add headers ...  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ head -n 3 train.csv 
text	label
နန့် ကီး မွန်း တည့် နူး ဟှ ကျန်် နော် တီ ဗီ ကေ့ နေ ဟှယ် ။	2
 လတ် ဆတ် တဲ့ အ သီး များ နှ င့် ဟင်း သီး ဟင်း ရွက် များ က မင်း အ တွက် ကောင်း တယ် ။	3
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ head -n 3 test.csv 
text	label
 ဖြစ် နိုင် ကေ နောက် ကြာ သ ပ တေး နိ ။	4
 ပြော ရ မှာ တော့ အား နာ ပါ ရဲ့ ကျွန် တော် ကွန် ပျူ တာ သိပ္ပံ နဲ့ ပတ် သက် လို့ များ များ စား စား မ သိ ဘူး ။	3
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ 
```

## KNN Train Again

Training KNN ...  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ time python ./knn.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
Traceback (most recent call last):
  File "./knn.py", line 35, in <module>
    unigram_vectorizer.fit(polar_train['text'].values)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1283, in fit
    self.fit_transform(raw_documents)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1330, in fit_transform
    vocabulary, X = self._count_vocab(raw_documents, self.fixed_vocabulary_)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 1201, in _count_vocab
    for feature in analyze(doc):
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 108, in _analyze
    doc = decoder(doc)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/feature_extraction/text.py", line 227, in decode
    "np.nan is an invalid document, expected byte or unicode string."
ValueError: np.nan is an invalid document, expected byte or unicode string.

real	0m0.726s
user	0m0.771s
sys	0m0.515s
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$
```

Found blank lines ...  

```
(sentiment) ye@ykt-pro:~/exp/dialect-detect/csv$ grep -n "^$" ./f1
3715:
4933:
8634:
8739:
9764:
11574:
11743:
18184:
23604:
24292:
25407:
26392:
35382:
37034:
43843:
(sentiment) ye@ykt-pro:~/exp/dialect-detect/csv$
```

Blank line တွေကို ရှင်ပြီးတော့ KNN ကို training လုပ်တာ ရပြီ ဒါပေမဲ့ အောက်ပါအတိုင်း error အသစ် ထပ်ရတယ်။  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ time python knn.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
KNN, Unigram Counts
Train score: 0.65 ; Validation score: 0.62

Traceback (most recent call last):
  File "knn.py", line 121, in <module>
    train_and_show_scores_KNN(X_train_unigram, y_train, 'KNN, Unigram Counts', 'knn_unigram_count.joblib')
  File "knn.py", line 117, in train_and_show_scores_KNN
    dump(clf, 'classifiers/' + model)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/joblib/numpy_pickle.py", line 552, in dump
    with open(filename, 'wb') as f:
FileNotFoundError: [Errno 2] No such file or directory: 'classifiers/knn_unigram_count.joblib'

real	0m25.647s
user	0m19.971s
sys	0m5.579s
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$
```

classifier folder မရှိလို့ ပေးတဲ့ error ပါ။ အဲဒါကြောင့် folder ဆောက်ပေးလိုက်တဲ့အခါမှာ အဆင်ပြေသွားပါတယ်။  

Blank lines in test file also:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ grep -n "^$" f1
1051:
4792:
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts/csv$ 
```

## KNN Results 

```
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ time python knn.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
KNN, Unigram Counts
Train score: 0.67 ; Validation score: 0.65

KNN, Unigram Tf-Idf
Train score: 0.66 ; Validation score: 0.63

KNN, Bigram Counts
Train score: 0.64 ; Validation score: 0.62

KNN, Bigram Tf-Idf
Train score: 0.66 ; Validation score: 0.62

KNN Test Result, Unigram Counts:  0.579403466344216
Error Rate: 0.42
KNN Test Result, Unigram Tf-Idf:  0.6297863764611044
Error Rate: 0.37
KNN Test Result, Bigram Count:  0.5257960499798469
Error Rate: 0.47
KNN Test Result, Bigram Tf-Idf:  0.6299879081015719
Error Rate: 0.37

real	1m49.006s
user	1m24.834s
sys	0m24.650s
(tabpfn) yekyaw.thu@gpu:~/exp/dialect-detection/scripts$ 
```

## SVM Results

```

```

## Decision Tree Results

```

```

## Random Forest Results  

```

```

## SGD Results  

```

```

## Summary  

```

```

```

```
