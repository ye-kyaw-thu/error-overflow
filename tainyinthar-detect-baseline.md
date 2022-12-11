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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
