
# Error for extracting .tar.gz file

.tar.gz ဖိုင်ကို ပုံမှန်အတိုင်း tar-xzvf command နဲ့ ဖြေတဲ့အခါမှာ မဖြေနိုင်ဘဲ error ရ  

```bash
$ tar -xzvf ./ngramtool-20040530.tar.gz 

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
```

# Check file type

ဖိုင်အမျိုးအစားကို file command နဲ့ စစ်ဆေးကြည့်တော့ gzip နဲ့ zip လုပ်ထားတာမဟုတ်ပဲ  
tar နဲ့ compress လုပ်ထားတဲ့ဖိုင်ဆိုတာကို အောက်ပါအတိုင်း တွေ့ရတယ်။  

```bash
$ file ./ngramtool-20040530.tar.gz 
./ngramtool-20040530.tar.gz: POSIX tar archive (GNU)
```

# Solution

အဲဒါကြောင့် "z" option ကို မထည့်ပဲ "tar -xvf" နဲ့ ဆိုရင် ဖြေလို့ရပါတယ်။  

```bash
$ tar -xvf ./ngramtool-20040530.tar.gz 
ngramtool-20040530/
ngramtool-20040530/src/
ngramtool-20040530/src/Jamfile
ngramtool-20040530/src/extractngram.cpp
ngramtool-20040530/src/extractngram.ggo
ngramtool-20040530/src/extractngram_cmdline.c
ngramtool-20040530/src/extractngram_cmdline.h
ngramtool-20040530/src/iconvert.cpp
...
...
...
```
