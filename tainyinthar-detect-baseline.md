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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
