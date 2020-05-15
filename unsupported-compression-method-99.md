# winzip နဲ့ zip လုပ်ထားတဲ့ ဖိုင်ကို Linux OS ပေါ်မှာ unzip command နဲ့ ဖြေရင်တွေ့ရတဲ့ error တစ်ခုကို ရှင်းနည်း

Repair.zip ဖိုင်က Windows OS မှာ winzip ဆိုတဲ့ အများသုံးကြတဲ့ zip လုပ်ပေးတဲ့ utility တစ်ခုပါ။  
ကြုံရတာက အဲဒီဖိုင်ကို Linux OS ပေါ်မှာ unzip command နဲ့ ဖြေတဲ့ အခါမှာ အောက်ပါအတိုင်း error ကို ပေးပါတယ်။  

```
$ unzip ./Repair.zip 
Archive:  ./Repair.zip
   skipping: Repair/error/detail-error-report.txt  unsupported compression method 99
   skipping: Repair/error/fixed-this-error.txt  unsupported compression method 99
   creating: Repair/
   creating: Repair/error/
```

ဖိုလ်ဒါအလိုက်ကို zip လုပ်ပြီး တဖက်က ပို့ပေးထားတာမို့ မဖြေပေးနိုင်ပေမဲ့ ဖိုလ်ဒါတော့ ဆောက်ပေးသွားပါတယ်။ အဲဒါကြောင့် ဖိုလ်ဒါ structure ကိုတော့ tree command နဲ့ ကြည့်ရင် အောက်ပါအတိုင်း မြင်ခဲ့ရပါတယ်။  

```
$ tree ./Repair
./Repair
└── error

1 directory, 0 files
```

အဲဒါနဲ့ တခြား unzip လုပ်တဲ့ ပရိုဂရမ်ဖြစ်တဲ့ 7z နဲ့ ဖြေလိုက်တဲ့ အခါမှာတော့ ဖြေပေးနိုင်ပါတယ်။  
-p ဆိုတဲ့ option က password နဲ့ zip လုပ်ထားလို့ password ထည့်ပေးရတဲ့ option ပါ။  
<password> နေရာမှာ ပေးထားတဲ့ စကားဝှက်ကို ရိုက်ထည့်ပေးရမှာ ဖြစ်ပါတယ်။  
အဲဒါဆိုရင်တော့ ဖြေပေး နိုင်တာကို အောက်ပါအတိုင်း တွေ့ရပါလိမ့်မယ်။  
   
```
$ 7z x -p<password> ./Repair.zip 

7-Zip [64] 9.20  Copyright (c) 1999-2010 Igor Pavlov  2010-11-18
p7zip Version 9.20 (locale=en_US.utf8,Utf16=on,HugeFiles=on,4 CPUs)

Processing archive: ./Repair.zip

Extracting  Repair
Extracting  Repair/error
Extracting  Repair/error/detail-error-report.txt
Extracting  Repair/error/fixed-this-error.txt

Everything is Ok

Folders: 2
Files: 2
Size:       171975
Compressed: 31534
```

Reference: [https://openwritings.net/pg/linux/unzip-error-unsupported-compression-method-99](https://openwritings.net/pg/linux/unzip-error-unsupported-compression-method-99)  
