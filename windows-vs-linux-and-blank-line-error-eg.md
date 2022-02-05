# File Format Between Windows and Linux and Blank Line Error Example

Machine Translation လုပ်ဖို့အတွက် parallel data ကို ပြင်ဆင်ရတဲ့အခါမှာ အတွေ့အကြုံမရှိတဲ့ ကျောင်းသားတွေအတွက်က သင်ပြရတဲ့ preprocessing ကိစ္စတွေက အများကြီးပါပဲ။  
အခု ဒီ error ကတော့ ဘာနဲ့ ဆိုင်သလဲ ဆိုရင် Windows နဲ့ Linux ရဲ့ OS နှစ်ခုအကြားမှာ newline ကို သိမ်းတဲ့ ပုံစံက မတူတာကို မပြောင်းထားတာ (file format conversion) နဲ့ text ဖိုင်ထဲမှာ blank line တွေ ပါနေလို့ source နဲ့ target အကြားမှာ လိုင်းအရေအတွက် မတူတဲ့ ကိစ္စပါ။   

တကယ်က training, validation နဲ့ test ဒေတာ ခွဲထားတာကလည်း shuffle မလုပ်ပဲ ခွဲထားလို့ အဲဒါကလည်း Machine Learning မှာ Machine Translation မှာ ပြဿနာပါပဲ။   

အခု တင်ပေးထားတာက ကျောင်းသူ တစ်ယောက်ဆီကနေ ပို့ပေးတဲ့ ဒေတာကို ဆရာက ဘယ်လို စစ်ကြည့်ခဲ့တယ်၊ file conversion ကို ဘယ်လို လုပ်ခဲ့တယ် ဆိုတာနဲ့ နောက်ဆုံး blank line ရှိနေတာကို ရှာတွေ့သွားတဲ့အထိ ရိုက်ခဲ့တဲ့ command တွေကို log လုပ်ပေးထားတာပါ။  

တကယ်က ဒီပြဿနာ သေးသေးလေးတွေက အစ NLP အလုပ်မှာ အရေးကြီးပါတယ်။ အကြိမ်ကြိမ်အခါခါ မေ့ကြ၊ မှားကြတယ် ဆိုတာကိုလည်း R&D လုပ်ရင်း တွေ့ရတာမို့ လေ့လာချင်သူတွေ လေ့လာလို့ ရအောင် error-overflow မှာ တင်ပေးထားလိုက်တာပါ။  

y  
5 Feb 2022  

## Check the Files

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ wc *
   1000   13676   68916 test.en
   1000   15133  245910 test.my
    999    2427  157014 test.th
  13598  172683  868531 train.en
  13599  198596 3065224 train.my
  12578   28600 1999397 train.th
   1000   14105   69368 valid.en
   1000   15457  247618 valid.my
    999    2197  159704 valid.th
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ file *
test.en:  UTF-8 Unicode text
test.my:  UTF-8 Unicode text
test.th:  UTF-8 Unicode text, with CRLF line terminators
train.en: UTF-8 Unicode text, with very long lines, with CRLF, LF line terminators
train.my: UTF-8 Unicode text, with very long lines, with CRLF line terminators
train.th: UTF-8 Unicode text, with CRLF line terminators
valid.en: UTF-8 Unicode text
valid.my: UTF-8 Unicode text, with very long lines
valid.th: UTF-8 Unicode text, with CRLF line terminators
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ gedit *.th
```

## Conversion with Perl

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ perl -p -e 's/\r$//' < ./train.th > ./train.utf8.th
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ perl -p -e 's/\r$//' < ./test.th > ./test.utf8.th
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ perl -p -e 's/\r$//' < ./valid.th > ./valid.utf8.th
```

## Check the Converted Files

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ wc *.utf8.th
    999    2427  156015 test.utf8.th
  12578   28600 1986819 train.utf8.th
    999    2197  158705 valid.utf8.th
  14576   33224 2301539 total
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ file *.utf8.th
test.utf8.th:  UTF-8 Unicode text
train.utf8.th: UTF-8 Unicode text
valid.utf8.th: UTF-8 Unicode text
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$
```

## Install dos2unix program

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ sudo apt-get install dos2unix
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  apturl-common gir1.2-goa-1.0 ibverbs-providers libboost-atomic-dev libboost-atomic1.71-dev libboost-atomic1.71.0 libboost-chrono-dev
  libboost-chrono1.71-dev libboost-chrono1.71.0 libboost-container-dev libboost-container1.71-dev libboost-container1.71.0 libboost-context-dev
  libboost-context1.71-dev libboost-context1.71.0 libboost-coroutine-dev libboost-coroutine1.71-dev libboost-coroutine1.71.0 libboost-date-time-dev
  libboost-date-time1.71-dev libboost-dev libboost-exception-dev libboost-exception1.71-dev libboost-fiber-dev libboost-fiber1.71-dev
  libboost-fiber1.71.0 libboost-filesystem-dev libboost-filesystem1.71-dev libboost-graph-parallel-dev libboost-graph-parallel1.71-dev
  libboost-graph-parallel1.71.0 libboost-graph1.71.0 libboost-locale-dev libboost-locale1.71-dev libboost-log1.71.0 libboost-math-dev
  libboost-math1.71-dev libboost-math1.71.0 libboost-mpi-dev libboost-mpi-python-dev libboost-mpi-python1.71-dev libboost-mpi-python1.71.0
  libboost-mpi1.71-dev libboost-mpi1.71.0 libboost-numpy-dev libboost-numpy1.71-dev libboost-numpy1.71.0 libboost-program-options-dev
  libboost-program-options1.71-dev libboost-program-options1.71.0 libboost-python-dev libboost-python1.71-dev libboost-python1.71.0
  libboost-random-dev libboost-random1.71-dev libboost-random1.71.0 libboost-regex1.71.0 libboost-serialization-dev libboost-serialization1.71-dev
  libboost-serialization1.71.0 libboost-stacktrace-dev libboost-stacktrace1.71-dev libboost-stacktrace1.71.0 libboost-system-dev
  libboost-system1.71-dev libboost-system1.71.0 libboost-test-dev libboost-test1.71-dev libboost-test1.71.0 libboost-thread-dev
  libboost-thread1.71-dev libboost-timer-dev libboost-timer1.71-dev libboost-timer1.71.0 libboost-tools-dev libboost-type-erasure-dev
  libboost-type-erasure1.71-dev libboost-type-erasure1.71.0 libboost-wave-dev libboost-wave1.71-dev libboost-wave1.71.0 libboost1.71-dev
  libboost1.71-tools-dev libcaf-openmpi-3 libcoarrays-openmpi-dev libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7
  libevent-pthreads-2.1-7 libfabric1 libhwloc-dev libhwloc-plugins libhwloc15 libibverbs-dev libibverbs1 libnl-3-dev libnl-route-3-dev libnuma-dev
  libopenmpi-dev libopenmpi3 libpmix2 libpsm-infinipath1 libpsm2-2 librdmacm1 mpi-default-bin mpi-default-dev openmpi-bin openmpi-common python3-click
  python3-colorama python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  dos2unix
0 upgraded, 1 newly installed, 0 to remove and 23 not upgraded.
Need to get 374 kB of archives.
After this operation, 1,352 kB of additional disk space will be used.
WARNING: The following packages cannot be authenticated!
  dos2unix
Install these packages without verification? [y/N] y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 dos2unix amd64 7.4.1-1 [374 kB]
Fetched 374 kB in 2s (221 kB/s)                         
Selecting previously unselected package dos2unix.
(Reading database ... 665544 files and directories currently installed.)
Preparing to unpack .../dos2unix_7.4.1-1_amd64.deb ...
Unpacking dos2unix (7.4.1-1) ...
Setting up dos2unix (7.4.1-1) ...
Processing triggers for man-db (2.9.3-2) ...
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$
```

## Conversion

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ dos2unix valid.utf8.th 
dos2unix: converting file valid.utf8.th to Unix format...
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ dos2unix test.utf8.th 
dos2unix: converting file test.utf8.th to Unix format...
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ dos2unix train.utf8.th 
dos2unix: converting file train.utf8.th to Unix format...
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$
```

## Check Converted Files Again

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ file *.utf8.th
test.utf8.th:  UTF-8 Unicode text
train.utf8.th: UTF-8 Unicode text
valid.utf8.th: UTF-8 Unicode text
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$ wc *.utf8.th
    999    2427  156015 test.utf8.th
  12578   28600 1986819 train.utf8.th
    999    2197  158705 valid.utf8.th
  14576   33224 2301539 total
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/corpus_med_en-my$
```

မရဘူး တစ်ခုခုတော့ လွဲနေတယ်...  

## Check Files of 2nd Time Sending From My Student

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ ls
test.en  test.my  test.th  train.en  train.my  train.th  valid.en  valid.my  valid.th
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ file *
test.en:  UTF-8 Unicode text
test.my:  UTF-8 Unicode text
test.th:  UTF-8 Unicode text
train.en: UTF-8 Unicode text, with very long lines, with CRLF, LF line terminators
train.my: UTF-8 Unicode text, with very long lines, with CRLF line terminators
train.th: UTF-8 Unicode text
valid.en: UTF-8 Unicode text
valid.my: UTF-8 Unicode text, with very long lines
valid.th: UTF-8 Unicode text
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ wc *
   1000   13676   68916 test.en
   1000   15133  245910 test.my
   1000    2427  156016 test.th
  13598  172683  868531 train.en
  13599  198596 3065224 train.my
  12578   28600 1986819 train.th
   1000   14105   69368 valid.en
   1000   15457  247618 valid.my
   1000    2197  158706 valid.th
  45775  462874 6867108 total
  ```
  
 ```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ dos2unix --help
Usage: dos2unix [options] [file ...] [-n infile outfile ...]
 --allow-chown         allow file ownership change
 -ascii                convert only line breaks (default)
 -iso                  conversion between DOS and ISO-8859-1 character set
   -1252               use Windows code page 1252 (Western European)
   -437                use DOS code page 437 (US) (default)
   -850                use DOS code page 850 (Western European)
   -860                use DOS code page 860 (Portuguese)
   -863                use DOS code page 863 (French Canadian)
   -865                use DOS code page 865 (Nordic)
 -7                    convert 8 bit characters to 7 bit space
 -b, --keep-bom        keep Byte Order Mark
 -c, --convmode        conversion mode
   convmode            ascii, 7bit, iso, mac, default to ascii
 -f, --force           force conversion of binary files
 -h, --help            display this help text
 -i, --info[=FLAGS]    display file information
   file ...            files to analyze
 -k, --keepdate        keep output file date
 -L, --license         display software license
 -l, --newline         add additional newline
 -m, --add-bom         add Byte Order Mark (default UTF-8)
 -n, --newfile         write to new file
   infile              original file in new-file mode
   outfile             output file in new-file mode
 --no-allow-chown      don't allow file ownership change (default)
 -o, --oldfile         write to old file (default)
   file ...            files to convert in old-file mode
 -q, --quiet           quiet mode, suppress all warnings
 -r, --remove-bom      remove Byte Order Mark (default)
 -s, --safe            skip binary files (default)
 -u,  --keep-utf16     keep UTF-16 encoding
 -ul, --assume-utf16le assume that the input format is UTF-16LE
 -ub, --assume-utf16be assume that the input format is UTF-16BE
 -v,  --verbose        verbose operation
 -F, --follow-symlink  follow symbolic links and convert the targets
 -R, --replace-symlink replace symbolic links with converted files
                         (original target files remain unchanged)
 -S, --skip-symlink    keep symbolic links and targets unchanged (default)
 -V, --version         display version number
 ```
 
 ```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ dos2unix -b ./train.en
dos2unix: converting file ./train.en to Unix format...
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ dos2unix -b ./train.my 
dos2unix: converting file ./train.my to Unix format...
```

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ wc *
   1000   13676   68916 test.en
   1000   15133  245910 test.my
   1000    2427  156016 test.th
  13598  172683  867510 train.en
  13599  198596 3051625 train.my
  12578   28600 1986819 train.th
   1000   14105   69368 valid.en
   1000   15457  247618 valid.my
   1000    2197  158706 valid.th
  45775  462874 6852488 total
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ file *
test.en:  UTF-8 Unicode text
test.my:  UTF-8 Unicode text
test.th:  UTF-8 Unicode text
train.en: UTF-8 Unicode text, with very long lines
train.my: UTF-8 Unicode text, with very long lines
train.th: UTF-8 Unicode text
valid.en: UTF-8 Unicode text
valid.my: UTF-8 Unicode text, with very long lines
valid.th: UTF-8 Unicode text
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ 
```

## I Found the Problem

နောက်ဆုံးမှာတော့ အောက်ပါအတိုင်း manual translation လုပ်ရင်းနဲ့ training ဖိုင်တွေမှာ enter တွေ ဆက်တိုက် ခေါက်ထားတာကို သွားတွေ့ရပါတယ်။  

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ tail train.*
==> train.en <==











==> train.my <==











==> train.th <==
เพื่อนร่วมงานรุ่นน้องของคุณเห็นเธอและจากไปเป็นเวลาสองชั่วโมงแล้ว และเขาไม่กลับมาหาผู้ป่วยอีกเลย
เขาใส่ cannula ผิดและยังไม่ได้เริ่มการรักษาเลย
ผู้ป่วยไม่มีความสุข กรุณาพูดคุยกับผู้ป่วย
ผู้ป่วยควรนั่งบนเก้าอี้โดยให้ IV cannula อยู่ในแขนของเธอ
ผู้ป่วยรายนี้มีอาการเซลลูไลติสที่ขาขวาและมีสายสวนทางหลอดเลือดดำที่แขนซ้าย
หากพวกเขาเริ่มทำเช่นนั้น ผู้ทดสอบควรแจ้งให้อ่านงานอีกครั้ง
คุณนายบราวน์ ฉันเข้าใจว่าคุณไม่ค่อยพอใจกับวิธีที่เราจัดการกับสถานการณ์ของคุณ
ฉันไม่มีความสุขจริงๆ เพราะเพื่อนร่วมงานของคุณมาหาฉันเมื่อสองชั่วโมงที่แล้ว และเขาก็ทิ้งฉันไว้ตามลำพังตั้งแต่นั้นเป็นต้นมา
ฉันเสียใจจริงๆ คุณบราวน์ ที่เราจัดการกับสถานการณ์ของคุณไม่ถูกต้อง

(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$
```

## Shuffling is Important

ပြီးတော့ ဖိုင်တွေကို တစ်ဖိုင်ချင်း ဖွင့်စစ်တဲ့အခါမှာ text book ထဲကအစီအစဉ်အတိုင်း တန်းစီပြီး ရှိနေတာကို တွေ့ရတဲ့ အတွက် သေချာတယ်။ training/valid/test ဒေတာတွေ မခွဲခင်မှာ ကျောင်းသားက shuffle မလုပ်ထားရသေးဘူး ဆိုတာကိုလည်း ဂရုပြုမိခဲ့ပါတယ်။  

```
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$ head train.{en,my,th}
==> train.en <==
Hello
Are you Mr.Tun Tun ?
Nice to meet you .
My name is Dr.Aung .
I am one of the junior doctors in the department .
How would you like me to call you ?
You can call me &quot; Ko Tun &quot; .
From what you are telling me , most likely you have a condition called heart failure .
Heart failure is a condition in which your heart is not functioning ( pumping ) properly .
Have I made myself clear ?

==> train.my <==
မင်္ဂလာပါ ။
ခင်ဗျား က မစ္စတာ ထွန်းထွန်း ဖြစ် ပါ သလား ။
ခင်ဗျား ကို တွေ့ ရတာ ဝမ်းသာ ပါ တယ် ။
ကျွန်တော့် နာမည် ဒေါက်တာ အောင် ဖြစ် ပါ တယ် ။
ကျွန်တော် ဒီ ဌာန က ဆရာဝန် အငယ် တစ်ယောက် ဖြစ် ပါ တယ် ။
ခင်ဗျား ကို ဘယ်လို ခေါ် ရ မလဲ ။
ခင်ဗျား ကျွန်တော့် ကို " ကိုထွန်း " လို့ ခေါ် နိုင် ပါ တယ် ။
ခင်ဗျား ပြောပုံ အရ ဆိုရင် ခင်ဗျား ရဲ့ နှလုံး မှာ ပြဿနာ နည်းနည်း ရှိ နေတယ် ။
နှလုံး အားနည်း ခြင်း ဟာ ခင်ဗျား ရဲ့ နှလုံး က ကောင်းစွာ အလုပ် မ လုပ်ဆောင် တဲ့ အခြေအနေ တစ်ခု ဖြစ် တယ် ။
ကျွန်တော် ပြော တာ နားလည် ပါ သလား ။

==> train.th <==
สวัสดี
คุณคือนายตุน ตุน?
ยินดีที่ได้พบคุณ.
ฉันชื่อ หมออ๋อง
ฉันเป็นหนึ่งในแพทย์รุ่นน้องในแผนก
คุณต้องการให้ฉันโทรหาคุณอย่างไร
เรียกผมว่า "โก ตุน" ก็ได้
จากสิ่งที่คุณบอกฉัน เป็นไปได้มากว่าคุณมีอาการที่เรียกว่าภาวะหัวใจล้มเหลว
ภาวะหัวใจล้มเหลวเป็นภาวะที่หัวใจของคุณทำงาน (สูบฉีด) ไม่ถูกต้อง
ฉันได้ทำให้ตัวเองชัดเจน?
(base) ye@:/media/ye/project2/students/mya-ei-san/5Feb2022-translation/2nd-time/corpus_med_en-my$
```

အရေးကြီးပါတယ်။ Machine Learning မော်ဒယ်တွေအတွက် အခုကိစ္စမှာတော့ Machine Translation အတွက်ပေါ့လေ.... ဒေတာတွေကို training, validation, testing အဖြစ် မခွဲခင်မှာ shuffle လုပ်ကြရအောင်။  
