# Sentencepiece Installation and Testing Log

Neural Network ကို သုံးပြီးတော့ machine translation, text generation စတဲ့ မော်ဒယ်တွေကို ဆောက်ကြမယ်ဆိုရင် မြန်မာစာ စာကြောင်းတွေကို ဘယ်လိုပုံစံနဲ့ word segmentation လုပ်ကြမှာလဲ ဆိုတာကို စဉ်းစားဖို့ လိုအပ်ပါတယ်။ ဘာကြောင့်လဲ ဆိုတော့ အဲဒီ ဖြတ်ထားတဲ့ segmentation unit တွေအပေါ်ကို မူတည်ပြီး model ရဲ့ learning လုပ်ရတာ၊ learn လုပ်ပြီး ရလာတဲ့ model ရဲ့ performance တွေက ကွာခြားသွားတဲ့ ကိစ္စတွေရှိလို့ ဖြစ်ပါတယ်။ အဲဒါကြောင့် sub-word unit ကို သုံးပြီး training လုပ်တာက option တစ်ခုဖြစ်လာပါတယ်။   

Senencepiece tool က အဲဒီလို စာကြောင်းတွေကို unigram, bpe, char, word တွေ ဖြတ်ဖို့အတွက် သုံးတဲ့ tool တစ်ခုပါ။  
ဒီနေရာမှာ အဲဒီ tool ကို installation လုပ်တဲ့ အဆင့်ကနေ မော်ဒယ်ဆောက်တာ၊ ပြီးတော့ ဆောက်ထားတဲ့ မော်ဒယ်တွေကို သုံးပြီးတော့ segmentation လုပ်တာတွေကို လုပ်ပြထားတဲ့ draft tutorial တစ်ခု ဖြစ်ပါတယ်။ မြန်မာကျောင်းသားတွေအတွက် ရည်ရွယ်တာမို့ မြန်မာစာ ကို သုံးပြီး လုပ်ပြထားတာပါ။  

ဒီ tutorial ကို ဖတ်မဲ့ သူက Linux OS, command တွေနဲ့ ရင်းနှီးပြီးသားလို့ ယူဆထားပါတယ်။  

## Git clone

```
(base) ye@ykt-pro:/media/ye/project1/tool$ git clone https://github.com/google/sentencepiece
Cloning into 'sentencepiece'...
remote: Enumerating objects: 260, done.
remote: Counting objects: 100% (260/260), done.
remote: Compressing objects: 100% (209/209), done.
remote: Total 3235 (delta 104), reused 123 (delta 46), pack-reused 2975
Receiving objects: 100% (3235/3235), 27.30 MiB | 406.00 KiB/s, done.
Resolving deltas: 100% (2159/2159), done.
```

## Installation

```
(base) ye@ykt-pro:/media/ye/project1/tool$ cd sentencepiece/
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece$ ls
appveyor.yml    config.h.in      data  LICENSE  README.md            src         test.bat  third_party
CMakeLists.txt  CONTRIBUTING.md  doc   python   sentencepiece.pc.in  tensorflow  test.sh   VERSION
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece$ mkdir build
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece$ cd build
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ cmake ..
-- VERSION: 0.1.93
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/local/bin/ccache-gcc
-- Check for working C compiler: /usr/local/bin/ccache-gcc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/local/bin/ccache-gxx
-- Check for working CXX compiler: /usr/local/bin/ccache-gxx -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found TCMalloc: /usr/lib/x86_64-linux-gnu/libtcmalloc_minimal.so
-- Configuring done
-- Generating done
-- Build files have been written to: /media/ye/project1/tool/sentencepiece/build
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ 
```

## Error with make command

```
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ make -j $(nproc)
Scanning dependencies of target sentencepiece
Scanning dependencies of target sentencepiece_train-static
Scanning dependencies of target sentencepiece-static
[  1%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
[  2%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/builder.cc.o
[  2%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arena.cc.o
[  3%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arena.cc.o
[  4%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  5%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  6%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/bytestream.cc.o
[  7%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/bytestream.cc.o
[  8%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[  9%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[ 10%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/common.cc.o
[ 11%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/common.cc.o
[ 11%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
[ 12%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 13%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 14%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[ 15%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 15%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 16%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[ 17%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 18%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 19%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 20%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/int128.cc.o
[ 21%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 22%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 23%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/int128.cc.o
[ 25%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/status.cc.o
[ 26%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 27%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 28%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 28%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 29%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 30%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 31%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[ 32%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 33%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 34%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
[ 35%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/status.cc.o
[ 36%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 37%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 38%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/time.cc.o
[ 39%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 40%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
[ 41%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 42%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 42%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 43%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
[ 44%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 45%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/time.cc.o
[ 46%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 47%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 48%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece.pb.cc.o
[ 49%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 50%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 51%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 52%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 53%] Linking CXX static library libsentencepiece_train.a
[ 54%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece.pb.cc.o
[ 54%] Built target sentencepiece_train-static
[ 55%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 56%] Building CXX object src/CMakeFiles/sentencepiece.dir/bpe_model.cc.o
[ 57%] Building CXX object src/CMakeFiles/sentencepiece.dir/char_model.cc.o
[ 57%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/bpe_model.cc.o
[ 58%] Building CXX object src/CMakeFiles/sentencepiece.dir/error.cc.o
[ 59%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/char_model.cc.o
[ 59%] Building CXX object src/CMakeFiles/sentencepiece.dir/filesystem.cc.o
[ 60%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/error.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/filesystem.cc.o
[ 62%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/init.cc.o
[ 63%] Building CXX object src/CMakeFiles/sentencepiece.dir/init.cc.o
[ 64%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_factory.cc.o
[ 65%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_factory.cc.o
[ 66%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_interface.cc.o
[ 67%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_interface.cc.o
[ 68%] Building CXX object src/CMakeFiles/sentencepiece.dir/normalizer.cc.o
[ 69%] Building CXX object src/CMakeFiles/sentencepiece.dir/sentencepiece_processor.cc.o
[ 70%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/normalizer.cc.o
[ 71%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/sentencepiece_processor.cc.o
[ 72%] Building CXX object src/CMakeFiles/sentencepiece.dir/unigram_model.cc.o
[ 72%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/unigram_model.cc.o
[ 73%] Building CXX object src/CMakeFiles/sentencepiece.dir/util.cc.o
[ 74%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/util.cc.o
[ 75%] Building CXX object src/CMakeFiles/sentencepiece.dir/word_model.cc.o
[ 76%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 76%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/strings/string_view.cc.o
[ 77%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 78%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/flags/flag.cc.o
[ 79%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
[ 80%] Linking CXX shared library libsentencepiece.so
CMake Error: cmake_symlink_library: System Error: Function not implemented
CMake Error: cmake_symlink_library: System Error: Function not implemented
src/CMakeFiles/sentencepiece.dir/build.make:1083: recipe for target 'src/libsentencepiece.so.0.0.0' failed
make[2]: *** [src/libsentencepiece.so.0.0.0] Error 1
make[2]: *** Deleting file 'src/libsentencepiece.so.0.0.0'
CMakeFiles/Makefile2:212: recipe for target 'src/CMakeFiles/sentencepiece.dir/all' failed
make[1]: *** [src/CMakeFiles/sentencepiece.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
[ 81%] Linking CXX static library libsentencepiece.a
[ 81%] Built target sentencepiece-static
Makefile:151: recipe for target 'all' failed
make: *** [all] Error 2
```

## Check HDD Information

lsblk command နဲ့ HDD mount point တွေနဲ့ file system ကို check လုပ်လို့ ရပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ lsblk -f
NAME   FSTYPE   LABEL     UUID                                 MOUNTPOINT
loop0  squashfs                                                /snap/gnome-characters/550
loop1  squashfs                                                /snap/vlc/1700
loop2  squashfs                                                /snap/gnome-3-34-1804/36
loop3  squashfs                                                /snap/gnome-characters/539
loop4  squashfs                                                /snap/core18/1885
loop5  squashfs                                                /snap/pdftk/9
loop6  squashfs                                                /snap/gnome-calculator/730
loop7  squashfs                                                /snap/gnome-system-monitor/145
loop8  squashfs                                                /snap/gnome-logs/93
loop9  squashfs                                                /snap/core/9993
loop10 squashfs                                                /snap/gtk-common-themes/1474
loop11 squashfs                                                /snap/core/9804
loop12 squashfs                                                /snap/gnome-3-34-1804/33
loop13 squashfs                                                /snap/gnome-3-28-1804/116
loop14 squashfs                                                /snap/gnome-system-monitor/148
loop15 squashfs                                                /snap/gtk-common-themes/1506
loop16 squashfs                                                /snap/gnome-calculator/748
loop17 squashfs                                                /snap/gnome-3-28-1804/128
loop18 squashfs                                                /snap/gnome-logs/100
loop19 squashfs                                                /snap/core18/1880
sda                                                            
├─sda1 vfat               4187-603C                            /boot/efi
└─sda2 ext4               0f1521bd-7b70-4f65-ae42-2a99bee59bcc /
sdb                                                            
└─sdb1 ntfs     Transcend 9C2EF43B2EF4104E                     /media/ye/Transcend
sdc                                                            
├─sdc1 vfat     EFI       5F66-17ED                            
└─sdc2 exfat    project1  5E5F-7ACF                            /media/ye/project1
```

mount command နဲ့ grep command ကို တွဲပြီးတော့လည်း check လုပ်နိုင်ပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ mount | grep "^/dev"
/dev/sda2 on / type ext4 (rw,relatime,errors=remount-ro)
/dev/sda1 on /boot/efi type vfat (rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
/dev/sdc2 on /media/ye/project1 type fuseblk (rw,nosuid,nodev,relatime,user_id=0,group_id=0,default_permissions,allow_other,blksize=4096,uhelper=udisks2)
/dev/sdb1 on /media/ye/Transcend type fuseblk (rw,nosuid,nodev,relatime,user_id=0,group_id=0,default_permissions,allow_other,blksize=4096,uhelper=udisks2)
```

file command နဲ့လည်း check လုပ်လို့ ရပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ sudo file -sL /dev/sdc2
/dev/sdc2: DOS/MBR boot sector
(base) ye@ykt-pro:/media/ye/project1/tool/sentencepiece/build$ sudo file -sL /dev/sdb1
/dev/sdb1: DOS/MBR boot sector, code offset 0x52+2, OEM-ID "NTFS    ", sectors/cluster 8, Media descriptor 0xf8, sectors/track 63, heads 255, hidden sectors 2048, dos < 4.0 BootSector (0x80), FAT (1Y bit by descriptor); NTFS, sectors/track 63, sectors 1953519615, $MFT start cluster 786432, $MFTMirror start cluster 2, bytes/RecordSegment 2^(-1*246), clusters/index block 1, serial number 09c2ef43b2ef4104e
```

အထက်ပါ Error က symbolic link လုပ်လို့ မရတဲ့ error ပါ။  
လက်ရှိ ဆရာ သုံးထားတာက 3TB HDD အကြီးကြီးဖြစ်ပြီး အဲဒီအပေါ်မှာ installation လုပ်ဖို့ ကြိုးစားရင်း symbolic link ကို create လုပ်လို့ မရတဲ့ error လို့ နားလည်ပါတယ်။ အဲဒါကြောင့် git clone လုပ်ထားတဲ့ folder ကို notebook ရဲ့ builtin HDD အောက်က tool/ အောက်ကို move လုပ်ပြီး installation ကို ဆက်လုပ်ကြည့်ခဲ့ပါတယ်။  

## move to ~/tool

```
(base) ye@ykt-pro:/media/ye/project1/tool$ mv ./sentencepiece/ ~/tool/
(base) ye@ykt-pro:/media/ye/project1/tool$ cd ~/tool/
(base) ye@ykt-pro:~/tool$ cd sentencepiece/
(base) ye@ykt-pro:~/tool/sentencepiece$ ls
appveyor.yml  CMakeLists.txt  CONTRIBUTING.md  doc      python     sentencepiece.pc.in  tensorflow  test.sh      VERSION
build         config.h.in     data             LICENSE  README.md  src                  test.bat    third_party
```

## Installation

ရှိနေပြီးသား build ဖိုလ်ဒါကို ဖျက်ပြီး အသစ်ပြန် create လုပ်ပါတယ်။ ပြီးမှ installation ရဲ့ command တစ်ခုဖြစ်တဲ့ cmake .. ကို run လုပ်တာ အဆင်ပြေပြေနဲ့ ပြီးသွားတာကို အောက်ပါအတိုင်း တွေ့ရပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece$ rm -r build
(base) ye@ykt-pro:~/tool/sentencepiece$ mkdir build
(base) ye@ykt-pro:~/tool/sentencepiece$ cd build
(base) ye@ykt-pro:~/tool/sentencepiece/build$ 
(base) ye@ykt-pro:~/tool/sentencepiece/build$ cmake ..
-- VERSION: 0.1.93
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/local/bin/ccache-gcc
-- Check for working C compiler: /usr/local/bin/ccache-gcc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/local/bin/ccache-gxx
-- Check for working CXX compiler: /usr/local/bin/ccache-gxx -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found TCMalloc: /usr/lib/x86_64-linux-gnu/libtcmalloc_minimal.so
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ye/tool/sentencepiece/build
(base) ye@ykt-pro:~/tool/sentencepiece/build$ 
```

## run make

make command ကို run တဲ့အခါမှာတော့ CPU က ကိုယ့်စက်ထဲမှာ ရှိတဲ့ အရေအတွက်ကို nproc command နဲ့ ရှာကြည့်ပြီး make ကို pass လုပ်ပေးတော့ installation process က ပိုမြန်ဆန်ပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/build$ make -j $(nproc)
Scanning dependencies of target sentencepiece_train-static
Scanning dependencies of target sentencepiece-static
Scanning dependencies of target sentencepiece
[  1%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arena.cc.o
[  1%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  2%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arena.cc.o
[  3%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/builder.cc.o
[  4%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/bytestream.cc.o
[  5%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[  6%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  8%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/common.cc.o
[  8%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/bytestream.cc.o
[  9%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 10%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[ 11%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 12%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/common.cc.o
[ 13%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 14%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
[ 15%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 16%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 16%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/int128.cc.o
[ 17%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 18%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 19%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 19%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 20%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/status.cc.o
[ 21%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 22%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 23%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 25%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/time.cc.o
[ 26%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 27%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 28%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 29%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 30%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece.pb.cc.o
[ 31%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 32%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 33%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/int128.cc.o
[ 34%] Building CXX object src/CMakeFiles/sentencepiece.dir/bpe_model.cc.o
[ 35%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 36%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 36%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
[ 37%] Building CXX object src/CMakeFiles/sentencepiece.dir/char_model.cc.o
[ 38%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 39%] Building CXX object src/CMakeFiles/sentencepiece.dir/error.cc.o
[ 40%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/status.cc.o
[ 41%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[ 41%] Building CXX object src/CMakeFiles/sentencepiece.dir/filesystem.cc.o
[ 42%] Building CXX object src/CMakeFiles/sentencepiece.dir/init.cc.o
[ 43%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 44%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_factory.cc.o
[ 45%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 46%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_interface.cc.o
[ 46%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 47%] Building CXX object src/CMakeFiles/sentencepiece.dir/normalizer.cc.o
[ 48%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 49%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 50%] Building CXX object src/CMakeFiles/sentencepiece.dir/sentencepiece_processor.cc.o
[ 51%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[ 52%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/time.cc.o
[ 53%] Building CXX object src/CMakeFiles/sentencepiece.dir/unigram_model.cc.o
[ 54%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 55%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 56%] Building CXX object src/CMakeFiles/sentencepiece.dir/util.cc.o
[ 57%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 58%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece.pb.cc.o
[ 59%] Building CXX object src/CMakeFiles/sentencepiece.dir/word_model.cc.o
[ 59%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/strings/string_view.cc.o
[ 60%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/flags/flag.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/bpe_model.cc.o
[ 62%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[ 63%] Linking CXX shared library libsentencepiece.so
[ 63%] Built target sentencepiece
Scanning dependencies of target spm_decode
[ 63%] Building CXX object src/CMakeFiles/spm_decode.dir/spm_decode_main.cc.o
[ 64%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/char_model.cc.o
[ 65%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/error.cc.o
[ 66%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
[ 67%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/filesystem.cc.o
[ 68%] Linking CXX executable spm_decode
[ 68%] Built target spm_decode
Scanning dependencies of target sentencepiece_train
[ 69%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/builder.cc.o
[ 70%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/init.cc.o
[ 71%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_factory.cc.o
[ 72%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/unicode_script.cc.o
[ 73%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
[ 74%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_interface.cc.o
[ 75%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
[ 76%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/normalizer.cc.o
[ 77%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/trainer_factory.cc.o
[ 78%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/trainer_interface.cc.o
[ 79%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/sentencepiece_processor.cc.o
[ 80%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 81%] Linking CXX static library libsentencepiece_train.a
[ 81%] Built target sentencepiece_train-static
Scanning dependencies of target spm_export_vocab
[ 82%] Building CXX object src/CMakeFiles/spm_export_vocab.dir/spm_export_vocab_main.cc.o
[ 83%] Linking CXX executable spm_export_vocab
[ 83%] Built target spm_export_vocab
Scanning dependencies of target spm_encode
[ 83%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/unigram_model_trainer.cc.o
[ 84%] Building CXX object src/CMakeFiles/spm_encode.dir/spm_encode_main.cc.o
[ 85%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/word_model_trainer.cc.o
[ 85%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/unigram_model.cc.o
[ 86%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/char_model_trainer.cc.o
[ 87%] Linking CXX executable spm_encode
[ 87%] Built target spm_encode
[ 88%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/bpe_model_trainer.cc.o
[ 89%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/util.cc.o
[ 90%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/sentencepiece_trainer.cc.o
[ 91%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 92%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/pretokenizer_for_training.cc.o
[ 93%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 94%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
[ 95%] Linking CXX shared library libsentencepiece_train.so
[ 95%] Built target sentencepiece_train
Scanning dependencies of target spm_train
Scanning dependencies of target spm_normalize
[ 96%] Building CXX object src/CMakeFiles/spm_train.dir/spm_train_main.cc.o
[ 97%] Building CXX object src/CMakeFiles/spm_normalize.dir/spm_normalize_main.cc.o
[ 98%] Linking CXX static library libsentencepiece.a
[ 98%] Built target sentencepiece-static
[ 99%] Linking CXX executable spm_train
[100%] Linking CXX executable spm_normalize
[100%] Built target spm_train
[100%] Built target spm_normalize
(base) ye@ykt-pro:~/tool/sentencepiece/build$ 
```

## run sudo make install

နောက်ဆုံး installation command ဖြစ်တဲ့ make install ကို run တာပါ။ သူကတော့ super user right ရှိမှ run လို့ရမှာ ဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/build$ sudo make install
[ 10%] Built target sentencepiece_train-static
[ 46%] Built target sentencepiece-static
[ 81%] Built target sentencepiece
[ 82%] Built target spm_decode
[ 92%] Built target sentencepiece_train
[ 94%] Built target spm_normalize
[ 96%] Built target spm_train
[ 98%] Built target spm_export_vocab
[100%] Built target spm_encode
Install the project...
-- Install configuration: ""
-- Installing: /usr/local/lib/pkgconfig/sentencepiece.pc
-- Installing: /usr/local/lib/libsentencepiece.so.0.0.0
-- Installing: /usr/local/lib/libsentencepiece.so.0
-- Installing: /usr/local/lib/libsentencepiece.so
-- Installing: /usr/local/lib/libsentencepiece_train.so.0.0.0
-- Installing: /usr/local/lib/libsentencepiece_train.so.0
-- Installing: /usr/local/lib/libsentencepiece_train.so
-- Set runtime path of "/usr/local/lib/libsentencepiece_train.so.0.0.0" to ""
-- Installing: /usr/local/lib/libsentencepiece.a
-- Installing: /usr/local/lib/libsentencepiece_train.a
-- Installing: /usr/local/bin/spm_encode
-- Set runtime path of "/usr/local/bin/spm_encode" to ""
-- Installing: /usr/local/bin/spm_decode
-- Set runtime path of "/usr/local/bin/spm_decode" to ""
-- Installing: /usr/local/bin/spm_normalize
-- Set runtime path of "/usr/local/bin/spm_normalize" to ""
-- Installing: /usr/local/bin/spm_train
-- Set runtime path of "/usr/local/bin/spm_train" to ""
-- Installing: /usr/local/bin/spm_export_vocab
-- Set runtime path of "/usr/local/bin/spm_export_vocab" to ""
-- Installing: /usr/local/include/sentencepiece_trainer.h
-- Installing: /usr/local/include/sentencepiece_processor.h
```

## sudo ldconfig -v

ldconfig command ကတော့ library configuration ဖိုင်ကို update လုပ်တဲ့ command ပါ။ -v (verbose) နဲ့ run တာမို့ screen မှာ ထွက်လာမယ့် output တွေက အများကြီးမို့လို့ အိုက်ဒီယာရအောင် တချို့ကိုပဲ ပြထားပါတယ်။ မဟုတ်ရင် လိုင်းက ထောင်ချီပြီးတော့ ရှိမှာမို့ပါ။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/build$ sudo ldconfig -v
/sbin/ldconfig.real: Can't stat /usr/local/lib/i386-linux-gnu: No such file or directory
/sbin/ldconfig.real: Can't stat /usr/local/lib/i686-linux-gnu: No such file or directory
/sbin/ldconfig.real: Can't stat /lib/i686-linux-gnu: No such file or directory
/sbin/ldconfig.real: Can't stat /usr/lib/i686-linux-gnu: No such file or directory
/sbin/ldconfig.real: Path `/lib/x86_64-linux-gnu' given more than once
/sbin/ldconfig.real: Path `/usr/lib/x86_64-linux-gnu' given more than once
/usr/lib/x86_64-linux-gnu/libfakeroot:
	libfakeroot-0.so -> libfakeroot-tcp.so
/lib/i386-linux-gnu:
	libgcc_s.so.1 -> libgcc_s.so.1
	libSegFault.so -> libSegFault.so
	libpcprofile.so -> libpcprofile.so
	libpthread.so.0 -> libpthread-2.27.so
	libBrokenLocale.so.1 -> libBrokenLocale-2.27.so
/sbin/ldconfig.real: /lib/i386-linux-gnu/ld-2.27.so is the dynamic linker, ignoring

	ld-linux.so.2 -> ld-2.27.so
	libm.so.6 -> libm-2.27.so
	libnss_hesiod.so.2 -> libnss_hesiod-2.27.so
	libnss_nis.so.2 -> libnss_nis-2.27.so
	libnsl.so.1 -> libnsl-2.27.so
	libanl.so.1 -> libanl-2.27.so
	libnss_dns.so.2 -> libnss_dns-2.27.so
	libcrypt.so.1 -> libcrypt-2.27.so
	libbsd.so.0 -> libbsd.so.0.8.7
	libutil.so.1 -> libutil-2.27.so
	libcidn.so.1 -> libcidn-2.27.so
	libnss_compat.so.2 -> libnss_compat-2.27.so
	librt.so.1 -> librt-2.27.so
	libc.so.6 -> libc-2.27.so
	libdl.so.2 -> libdl-2.27.so
	libnss_files.so.2 -> libnss_files-2.27.so
	libmemusage.so -> libmemusage.so
	libresolv.so.2 -> libresolv-2.27.so
	libnss_nisplus.so.2 -> libnss_nisplus-2.27.so
	libthread_db.so.1 -> libthread_db-1.0.so
/usr/lib/i386-linux-gnu:
	libxcb.so.1 -> libxcb.so.1.1.0
	libXdmcp.so.6 -> libXdmcp.so.6.0.0
	libXau.so.6 -> libXau.so.6.0.0
	libX11.so.6 -> libX11.so.6.3.0
...
...
...
/usr/libx32:
	libgcc_s.so.1 -> libgcc_s.so.1
	libitm.so.1 -> libitm.so.1.0.0
	libatomic.so.1 -> libatomic.so.1.2.0
	libubsan.so.0 -> libubsan.so.0.0.0
	libcilkrts.so.5 -> libcilkrts.so.5.0.0
	libasan.so.4 -> libasan.so.4.0.0
	libquadmath.so.0 -> libquadmath.so.0.0.0
	libgomp.so.1 -> libgomp.so.1.0.0
	libstdc++.so.6 -> libstdc++.so.6.0.25
/lib:
/usr/lib:
	libgjs.so.0 -> libgjs.so.0.0.0
	libMonoSupportW.so -> libMonoSupportW.so
	libmono-profiler-iomap.so.0 -> libmono-profiler-iomap.so.0.0.0
	libtidy.so.5 -> libtidy.so.5.2.0
	libhardsid-builder.so.0 -> libhardsid-builder.so.0.0.1
	libmono-profiler-log.so.0 -> libmono-profiler-log.so.0.0.0
	libsidplay2.so.1 -> libsidplay2.so.1.0.1
	libresid-builder.so.0 -> libresid-builder.so.0.0.1
	libgoffice-0.10.so.10 -> libgoffice-0.10.so.10.0.39
	libMonoPosixHelper.so -> libMonoPosixHelper.so
	libmonosgen-2.0.so.1 -> libmonosgen-2.0.so.1.0.0
	libnatpmp.so.1 -> libnatpmp.so.1
	libnetpbm.so.10 -> libnetpbm.so.10.0
	liblilv-0.so.0 -> liblilv-0.so.0.24.2
	libgdiplus.so.0 -> libgdiplus.so.0.0.0
	libminisat.so.2 -> libminisat.so.2.1.0
	libmono-profiler-aot.so.0 -> libmono-profiler-aot.so.0.0.0
	libmonoboehm-2.0.so.1 -> libmonoboehm-2.0.so.1.0.0
	libann.so.0 -> libann.so.0.0.0
(base) ye@ykt-pro:~/tool/sentencepiece/build$ 
```

## Call --help

ထုံးစံအတိုင်းပါ installation က အဆင်ပြေပြေနဲ့ ကိုယ့်စက်ထဲမှာ ပြီးစီးသွားမယ်ဆိုရင် အောက်ပါအတိုင်း help ခေါ်ကြည့်လို့ ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/build$ spm_train --help
sentencepiece

Usage: spm_train [options] files

   --help (show help)  type: bool default: false
   --version (show version)  type: bool default: false
   --minloglevel (Messages logged at a lower level than this don't actually get logged anywhere)  type: int default: 0
   --input (comma separated list of input sentences)  type: std::string default: ""
   --input_format (Input format. Supported format is `text` or `tsv`.)  type: std::string default: ""
   --model_prefix (output model prefix)  type: std::string default: ""
   --model_type (model algorithm: unigram, bpe, word or char)  type: std::string default: "unigram"
   --vocab_size (vocabulary size)  type: int32 default: 8000
   --accept_language (comma-separated list of languages this model can accept)  type: std::string default: ""
   --self_test_sample_size (the size of self test samples)  type: int32 default: 0
   --character_coverage (character coverage to determine the minimum symbols)  type: double default: 0.9995
   --input_sentence_size (maximum size of sentences the trainer loads)  type: int32 default: 0
   --shuffle_input_sentence (Randomly sample input sentences in advance. Valid when --input_sentence_size > 0)  type: bool default: true
   --seed_sentencepiece_size (the size of seed sentencepieces)  type: int32 default: 1000000
   --shrinking_factor (Keeps top shrinking_factor pieces with respect to the loss)  type: double default: 0.75
   --num_threads (number of threads for training)  type: int32 default: 16
   --num_sub_iterations (number of EM sub-iterations)  type: int32 default: 2
   --max_sentencepiece_length (maximum length of sentence piece)  type: int32 default: 16
   --max_sentence_length (maximum length of sentence in byte)  type: int32 default: 4192
   --split_by_unicode_script (use Unicode script to split sentence pieces)  type: bool default: true
   --split_by_number (split tokens by numbers (0-9))  type: bool default: true
   --split_by_whitespace (use a white space to split sentence pieces)  type: bool default: true
   --split_digits (split all digits (0-9) into separate pieces)  type: bool default: false
   --treat_whitespace_as_suffix (treat whitespace marker as suffix instead of prefix.)  type: bool default: false
   --control_symbols (comma separated list of control symbols)  type: std::string default: ""
   --user_defined_symbols (comma separated list of user defined symbols)  type: std::string default: ""
   --required_chars (UTF8 characters in this flag are always used in the character set regardless of --character_coverage)  type: std::string default: ""
   --byte_fallback (decompose unknown pieces into UTF-8 byte pieces)  type: bool default: false
   --vocabulary_output_piece_score (Define score in vocab file)  type: bool default: true
   --normalization_rule_name (Normalization rule name. Choose from nfkc or identity)  type: std::string default: "nmt_nfkc"
   --normalization_rule_tsv (Normalization rule TSV file. )  type: std::string default: ""
   --denormalization_rule_tsv (Denormalization rule TSV file.)  type: std::string default: ""
   --add_dummy_prefix (Add dummy whitespace at the beginning of text)  type: bool default: true
   --remove_extra_whitespaces (Removes leading, trailing, and duplicate internal whitespace)  type: bool default: true
   --hard_vocab_limit (If set to false, --vocab_size is considered as a soft limit.)  type: bool default: true
   --use_all_vocab (If set to true, use all tokens as vocab. Valid for word/char models.)  type: bool default: false
   --unk_id (Override UNK (<unk>) id.)  type: int32 default: 0
   --bos_id (Override BOS (<s>) id. Set -1 to disable BOS.)  type: int32 default: 1
   --eos_id (Override EOS (</s>) id. Set -1 to disable EOS.)  type: int32 default: 2
   --pad_id (Override PAD (<pad>) id. Set -1 to disable PAD.)  type: int32 default: -1
   --unk_piece (Override UNK (<unk>) piece.)  type: std::string default: "<unk>"
   --bos_piece (Override BOS (<s>) piece.)  type: std::string default: "<s>"
   --eos_piece (Override EOS (</s>) piece.)  type: std::string default: "</s>"
   --pad_piece (Override PAD (<pad>) piece.)  type: std::string default: "<pad>"
   --unk_surface (Dummy surface string for <unk>. In decoding <unk> is decoded to `unk_surface`.)  type: std::string default: " ⁇ "
   --train_extremely_large_corpus (Increase bit depth for unigram tokenization.)  type: bool default: false
```

## Preparing Training and Test Data

Training data နှစ်ဖိုင် သုံးပါမယ်။ တစ်ဖိုင်က big-lm2.my ဖိုင်ပါ။ သူကတော့ manual word segmentation လုပ်ထားတဲ့ ဖိုင်ပါ။ နောက်တစ်ဖိုင်ရဲ့ နာမည်ကတော့ big-lm2.my.syl.clean ဖိုင်ပါ။ အဲဒီဖိုင်ကတော့ စောစောက big-lm2.my ဖိုင်ကိုပဲ syllable breaking လုပ်ထားပြီးတော့ ပိုနေတဲ့ space တွေကို ရှင်းထားတဲ့ ဖိုင်ဖြစ်ပါတယ်။  

### Training Data

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ head -n 3 ./big-lm2.my
မင်း အဲ့ဒါ ကို အခြား တစ်ခုနဲ့ မ ချိတ် ဘူးလား ။
သူမ ဘယ်သူ့ကိုမှ မ မှတ်မိတော့ဘူး ။
အဲ့ဒါ ကျွန်တော် တို့ အတွက် ခက်ခဲ တယ် ။
```

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ head -n 3 ./big-lm2.my.syl.clean 
မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
သူ မ ဘယ် သူ့ ကို မှ မ မှတ် မိ တော့ ဘူး ။
အဲ့ ဒါ ကျွန် တော် တို့ အ တွက် ခက် ခဲ တယ် ။
```

ဖိုင်ရဲ့ size ကတော့ အောက်ပါအတိုင်းပါ။ စုစုပေါင်း စာကြောင်းရေအရေအတွက်ကတော့ 92,458 ရှိပါတယ်။ ကိုးသောင်းကျော်ရှိပါတယ်။ BPE ဆောက်တဲ့အခါမှာ တကယ်က ဒေတာကို များနိုင်သမျှ များအောင် ပြင်ထားတဲ့ monolingual ဖိုင်နဲ့ ဆောက်ကြမှသာ သင့်တော်ပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ wc ./big-lm2.my
   92458   940841 12500002 ./big-lm2.my
```

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ wc ./big-lm2.my.syl.clean 
   92458  1407301 12929896 ./big-lm2.my.syl.clean
```

### Test Data

test ဖိုင် နှစ်ဖိုင်ပြင်ထားပါတယ်။ အဲဒီ ဖိုင်အထဲမှာ ပါတဲ့ ဒေတာက အောက်ပါအတိုင်းပါ။ စာကြောင်းရေက အများကြီး မထည့်ထားပါဘူး  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ cat ./test1.txt 
မင်း ကို ငါ ဘယ်လို ခေါ် ရ မ လဲ
စာ တော် တဲ့ ကျောင်း သူ တစ် ယောက် ပါ
အ ရမ်း ဆော့ တဲ့ ကလေး က ကျန်း မာ တယ်
အခု တော့ ပါ နက် ဆ ရာ ဟာ စက် တင် ဘာ လ ၁၉ ရက် နေ့ မှာ ဆန္ဒ ပြ ပွဲ ကျင်း ပ ဖို့ အ တွက် ပြင် ဆင် နေ ပါ တယ် ။
ဘတ်စ် ကား စီး ပြီး ရုံး တက် တဲ့ ဘိလပ် ပြန် ညွှန် ကြား ရေး မှူး ချုပ်
```

အောက်ပါဖိုင်ကတော့ BBC Burmese ရဲ့ article တစ်ခုတည်းကနေ ယူထားတဲ့ စာကြောင်းတွေ ဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ cat test2.raw
နိုင်ငံတခု ထူထောင်တဲ့အခါမှာ စစ်တပ်၊ စီးပွားရေးလုပ်ငန်းတွေနဲ့ တရားရုံးစတဲ့ ပင်မအဖွဲ့အစည်းတွေသာမက စာပေ ယဉ်ကျေးမှု စိတ်ဓာတ်ပိုင်းကလည်း နိုင်ငံသိစိတ် ချစ်စိတ်တွေ ပေါ်လာအောင် ဆော်ဩ ပေးရပါတယ်။ ဒါကိုသိတဲ့ လူကြီးပိုင်းက မြန်မာပြည်အတွက် ပြတိုက် စာကြည့်တိုက်နဲ့ အနုပညာတိုက်တွေ ရှိဖို့လိုတဲ့အကြောင်း ကိုလိုနီခေတ်ကစပြီး တိုက်တွန်းခဲ့ကြသလို ဒီယဉ်ကျေးမှု အဆောက်အဦတွေကို ကွပ်ကဲဖို့ အတွက် ပညာရှင်တွေ ပေါ်ထွက်ဖို့လည်း ကမ္ဘာစစ် မဖြစ်ခင်ကတည်းက စိုင်းပြင်းခဲ့ကြပါတယ်။ ဒါကြောင့် ဦးခင်ဇော်နဲ့ ဦးသိန်းဟန်ကို ပိဋကတ်တိုက်ပညာလို့ ခေါ်တဲ့ စာကြည့်တိုက်လုပ်ငန်းအတွက် ဗြိတိန်ကို စေလွှတ်ခဲ့ သလို ပန်းချီပညာသင်အဖြစ် ဦးဘဉာဏ်နဲ့ ဦးဘဇော်ကိုလည်း ဒီ့အရင်ကတည်းက လန်ဒန်ကို ပို့ခဲ့ပါတယ်။

ဒါပေမဲ့ ကိုလိုနီခေတ်မြန်မာနိုင်ငံမှာ အဲဒီအချိန်ထိ အမျိုးသားစာကြည့်တိုက်နဲ့ ပြတိုက်၊ အနုပညာပြခန်းတွေ မရှိသေးဘဲ ရန်ကုန် တက္ကသိုလ် ပိဋကတ်တိုက်နဲ့ ရန်ကုန်မြို့ထဲက ဗားနတ်ပိဋကတ်တိုက်နဲ့ ပြတိုက်အပြင် ပြည်နားက မှော်ဇာ၊ ရခိုင်က မြောက်ဦးနဲ့ အညာက ပုဂံ၊ ရွှေဘိုနဲ့ မန္တလေးမှာ ကမ္ပည်းကျောက်စာဌာန ပြတိုက်ကလေးတွေပဲ ရှိခဲ့ပါတယ်။
```

## Training Unigram

အရင်ဆုံး unigram unit model ကို ဆောက်ကြည့်ရအောင်  

```
command ရဲ့ syntax က အောက်ပါအတိုင်း   
spm_train --input=<input> --model_prefix=<model_name> --vocab_size=8000 --character_coverage=1.0 --model_type=<type>
```

### Build Unigram

ဒီနေရာမှာတော့ vocab_size ကို 8000 ထားကြည့်ထားပါတယ်။ 
မော်ဒယ်ဖိုင်နာမည်ရဲ့ prefix ကိုတော့ --model_prefix ဆိုတဲ့ option နဲ့ သတ်မှတ်လို့ရတာမို့ word-unigram ဆိုပြီး မော်ဒယ်ရဲ့ ဖိုင်နာမည်ကိုကြည့်တာနဲ့ word segmentation လုပ်ထားတဲ့ training ဒေတာနဲ့ ဆောက်ခဲ့တယ်၊ မော်ဒယ်ကတော့ unigram အမျိုးအစားဆိုတာကို ကွဲကွဲပြားပြားသိအောင် ပေးခဲ့ပါတယ်။  
နောက်ထပ် အရေးကြီးတဲ့ အချက်တချက်က Sentencepiece ရဲ့ GitHub မှာလည်း ဖော်ပြထားသလို --character_coverage နဲ့ ပတ်သက်ပြီး ပေးတဲ့အခါမှာ မြန်မာစာလို ဘာသာစကားအတွက်က 1.0 ထားသင့်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my --model_prefix=word-unigram --vocab_size=8000 --character_coverage=1.0 --model_type=unigram
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my
  input_format: 
  model_prefix: big-lm2
  model_type: UNIGRAM
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=4810538
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
unigram_model_trainer.cc(134) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(138) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(189) LOG(INFO) Initialized 87599 seed sentencepieces
trainer_interface.cc(518) LOG(INFO) Tokenizing input sentences with whitespace: 92458
trainer_interface.cc(528) LOG(INFO) Done! 40528
unigram_model_trainer.cc(484) LOG(INFO) Using 40528 sentences for EM training
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=27584 obj=9.01387 num_tokens=81848 num_tokens/piece=2.96723
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=21685 obj=7.1652 num_tokens=81887 num_tokens/piece=3.7762
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=16245 obj=7.13295 num_tokens=85630 num_tokens/piece=5.27116
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=16190 obj=7.11736 num_tokens=85651 num_tokens/piece=5.29036
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=12135 obj=7.16975 num_tokens=91969 num_tokens/piece=7.57882
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=12130 obj=7.15643 num_tokens=91978 num_tokens/piece=7.58269
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=9096 obj=7.2401 num_tokens=99581 num_tokens/piece=10.9478
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=9094 obj=7.22277 num_tokens=99581 num_tokens/piece=10.9502
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=8800 obj=7.23231 num_tokens=100381 num_tokens/piece=11.4069
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=8800 obj=7.23036 num_tokens=100381 num_tokens/piece=11.4069
trainer_interface.cc(606) LOG(INFO) Saving model: big-lm2.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: big-lm2.vocab

real	0m4.920s
user	0m9.525s
sys	0m0.108s

```

အထက်ပါအတိုင်း မော်ဒယ်ကို အောင်အောင်မြင်မြင်နဲ့ဆောက်လို့ရတာကို တွေ့ရပါတယ်။  

### Build Syllable Unigram Got Error

သို့သော် syllable ဖြတ်ထားတဲ့ training ဒေတာဖိုင်ကို သုံးပြီး ဆောက်ကြည့်တဲ့အခါမှာတော့ vocab_size ကို 8000 ထားရင် အောက်ပါအတိုင်း error ပေးတာကို တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-unigram --vocab_size=8000 --character_coverage=1.0 --model_type=unigram
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-unigram
  model_type: UNIGRAM
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
unigram_model_trainer.cc(134) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(138) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(189) LOG(INFO) Initialized 2964 seed sentencepieces
trainer_interface.cc(518) LOG(INFO) Tokenizing input sentences with whitespace: 92458
trainer_interface.cc(528) LOG(INFO) Done! 3259
unigram_model_trainer.cc(484) LOG(INFO) Using 3259 sentences for EM training
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=2466 obj=7.49826 num_tokens=6076 num_tokens/piece=2.46391
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=1834 obj=6.46334 num_tokens=5990 num_tokens/piece=3.26609
trainer_interface.cc(606) LOG(INFO) Saving model: syl-unigram.model
spm_train_main.cc(214) [_status.ok()] Internal: /home/ye/tool/sentencepiece/src/trainer_interface.cc(581) [(trainer_spec_.vocab_size()) == (model_proto->pieces_size())] Vocabulary size too high (8000). Please set it to a value <= 1869.
Program terminated with an unrecoverable error.

real	0m2.610s
user	0m2.935s
sys	0m0.084s
```

### Build Syllable Unigram with <=1869

vocab_size ကို 1000 ထားပြီး training လုပ်တော့မှ မော်ဒယ်ဖိုင် ထွက်လာပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-unigram --vocab_size=1000 --character_coverage=1.0 --model_type=unigram
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-unigram
  model_type: UNIGRAM
  vocab_size: 1000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
unigram_model_trainer.cc(134) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(138) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(189) LOG(INFO) Initialized 2964 seed sentencepieces
trainer_interface.cc(518) LOG(INFO) Tokenizing input sentences with whitespace: 92458
trainer_interface.cc(528) LOG(INFO) Done! 3259
unigram_model_trainer.cc(484) LOG(INFO) Using 3259 sentences for EM training
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=2466 obj=7.49826 num_tokens=6076 num_tokens/piece=2.46391
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=1834 obj=6.46334 num_tokens=5990 num_tokens/piece=3.26609
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=1293 obj=6.37312 num_tokens=5991 num_tokens/piece=4.63341
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=1291 obj=6.35346 num_tokens=6000 num_tokens/piece=4.64756
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=0 size=1100 obj=6.3648 num_tokens=6305 num_tokens/piece=5.73182
unigram_model_trainer.cc(500) LOG(INFO) EM sub_iter=1 size=1100 obj=6.36053 num_tokens=6308 num_tokens/piece=5.73455
trainer_interface.cc(606) LOG(INFO) Saving model: syl-unigram.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: syl-unigram.vocab

real	0m2.687s
user	0m3.076s
sys	0m0.073s
```

output ထွက်လာတဲ့ ဖိုင်တွေကတော့ ကိုယ်ပေးခဲ့တဲ့ prefix အပေါ်မှာလည်း မူတည်ပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ls *.model
syl-unigram.model  word-unigram.model
```

## Build BPE

BPE unit နဲ့ မော်ဒယ်ဆောက်ကြည့်ရအောင်...  

### Word BPE

Word segmentation လုပ်ထားတဲ့ training ဖိုင် big-lm2.my ကို သုံးမယ်။ ဖိုင်နာမည်ရဲ့ prefix ကိုတော့ word-bpe နဲ့ စပေးဖို့ option ပေးထားခဲ့ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my --model_prefix=word-bpe --vocab_size=8000 --character_coverage=1.0 --model_type=bpe
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my
  input_format: 
  model_prefix: word-bpe
  model_type: BPE
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=4810538
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(518) LOG(INFO) Tokenizing input sentences with whitespace: 92458
trainer_interface.cc(528) LOG(INFO) Done! 40528
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=103736 min_freq=72
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=35356 size=20 all=4705 active=1917 piece=စ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19140 size=40 all=5577 active=2789 piece=▁ကျွန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12280 size=60 all=6291 active=3503 piece=ောင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=8851 size=80 all=7384 active=4596 piece=ုတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=6553 size=100 all=7992 active=5204 piece=▁သွား
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=6401 min_freq=312
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=4677 size=120 all=8979 active=1964 piece=့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=3913 size=140 all=10081 active=3066 piece=▁ကောင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=3088 size=160 all=10886 active=3871 piece=▁မျ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=2649 size=180 all=11712 active=4697 piece=▁ယောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=2315 size=200 all=12676 active=5661 piece=ဘူး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=2312 min_freq=265
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1960 size=220 all=13858 active=2090 piece=▁သိ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1753 size=240 all=14814 active=3046 piece=▁ပြန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1564 size=260 all=15451 active=3683 piece=နည်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1423 size=280 all=16406 active=4638 piece=▁ဘယ်လို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1333 size=300 all=17299 active=5531 piece=▁တက
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=1330 min_freq=224
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1221 size=320 all=18098 active=1792 piece=ဆောင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1131 size=340 all=18936 active=2630 piece=▁နေရာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1044 size=360 all=19667 active=3361 piece=▁ဆေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=955 size=380 all=20542 active=4236 piece=ရီး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=893 size=400 all=21352 active=5046 piece=စု
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=891 min_freq=182
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=847 size=420 all=21989 active=1644 piece=▁ရော
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=781 size=440 all=22737 active=2392 piece=▁တောင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=745 size=460 all=23287 active=2942 piece=မား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=702 size=480 all=24094 active=3749 piece=ိမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=661 size=500 all=24656 active=4311 piece=▁-
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=656 min_freq=140
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=629 size=520 all=25406 active=1981 piece=ဝန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=598 size=540 all=26115 active=2690 piece=သည်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=575 size=560 all=26773 active=3348 piece=▁ကုလားထိုင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=557 size=580 all=27498 active=4073 piece=▁S
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=537 size=600 all=28222 active=4797 piece=ခမ်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=537 min_freq=111
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=524 size=620 all=28915 active=2089 piece=ကာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=512 size=640 all=29861 active=3035 piece=▁အမြဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=494 size=660 all=30444 active=3618 piece=▁ရိုက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=476 size=680 all=30873 active=4047 piece=ကလေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=455 size=700 all=31512 active=4686 piece=▁ကျွန်တော်တို့
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=454 min_freq=91
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=445 size=720 all=32100 active=2161 piece=▁ရာသီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=427 size=740 all=32499 active=2560 piece=အိတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=411 size=760 all=33204 active=3265 piece=▁အင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=390 size=780 all=33765 active=3826 piece=ပန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=379 size=800 all=34247 active=4308 piece=ရေ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=379 min_freq=77
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=369 size=820 all=34764 active=2118 piece=▁ကျန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=356 size=840 all=35202 active=2556 piece=စိ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=346 size=860 all=35509 active=2863 piece=▁ဘာသာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=332 size=880 all=35946 active=3300 piece=▁မျက်စိ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=323 size=900 all=36453 active=3807 piece=▁သေချာ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=322 min_freq=67
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=310 size=920 all=36873 active=2236 piece=▁ကော
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=301 size=940 all=37297 active=2660 piece=▁အဖြစ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=293 size=960 all=37708 active=3071 piece=ငန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=285 size=980 all=38146 active=3509 piece=ဆင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=278 size=1000 all=38754 active=4117 piece=▁နောက်ကျ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=278 min_freq=59
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=269 size=1020 all=39100 active=2272 piece=ပ္
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=261 size=1040 all=39389 active=2561 piece=▁လိမ့်မယ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=255 size=1060 all=39678 active=2850 piece=▁ပြဿနာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=250 size=1080 all=40133 active=3305 piece=▁အောင်မြင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=243 size=1100 all=40682 active=3854 piece=en
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=243 min_freq=52
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=236 size=1120 all=41290 active=2581 piece=▁အဝတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=230 size=1140 all=41702 active=2993 piece=▁A
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=226 size=1160 all=42076 active=3367 piece=▁ဆုံးဖြတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=221 size=1180 all=42448 active=3739 piece=▁တာဝန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=215 size=1200 all=42863 active=4154 piece=▁အနား
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=214 min_freq=48
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=208 size=1220 all=43120 active=2391 piece=▁ဖုန်းဆက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=203 size=1240 all=43409 active=2680 piece=ခိုက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=199 size=1260 all=43615 active=2886 piece=▁P
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=195 size=1280 all=43991 active=3262 piece=တ္တာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=191 size=1300 all=44181 active=3452 piece=စော
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=191 min_freq=44
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=187 size=1320 all=44553 active=2564 piece=▁ခဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=183 size=1340 all=45035 active=3046 piece=ကွယ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=180 size=1360 all=45321 active=3332 piece=▁ဒုက္ခ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=176 size=1380 all=45743 active=3754 piece=▁စီစဉ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=173 size=1400 all=46140 active=4151 piece=▁ကုန်ပစ္စည်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=172 min_freq=40
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=169 size=1420 all=46371 active=2538 piece=ရုပ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=165 size=1440 all=46745 active=2912 piece=▁နေတာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=160 size=1460 all=47210 active=3377 piece=တွဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=158 size=1480 all=47720 active=3887 piece=▁တကယ့်ကို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=155 size=1500 all=47944 active=4111 piece=ဘီး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=155 min_freq=37
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=151 size=1520 all=48309 active=2751 piece=ထက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=148 size=1540 all=48625 active=3067 piece=▁အနားယူ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=145 size=1560 all=48856 active=3298 piece=▁မှတ်မိ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=142 size=1580 all=49134 active=3576 piece=▁စေတီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=138 size=1600 all=49477 active=3919 piece=သိမ်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=138 min_freq=34
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=136 size=1620 all=49795 active=2757 piece=▁ဆောင်ရွက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=133 size=1640 all=49950 active=2912 piece=မြတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=132 size=1660 all=50147 active=3109 piece=▁စာသင်ခန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=128 size=1680 all=50496 active=3458 piece=▁အသား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=126 size=1700 all=50798 active=3760 piece=▁တန်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=126 min_freq=32
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=123 size=1720 all=51230 active=2965 piece=▁မမ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=121 size=1740 all=51500 active=3235 piece=▁သဘာဝ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=119 size=1760 all=51730 active=3465 piece=▁အထုပ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=118 size=1780 all=51924 active=3659 piece=▁တည်ဆောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=116 size=1800 all=52266 active=4001 piece=▁ဖြေရှင်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=116 min_freq=29
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=114 size=1820 all=52567 active=2904 piece=▁ကျွေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=112 size=1840 all=52763 active=3100 piece=ုံ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=110 size=1860 all=53055 active=3392 piece=▁နယ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=109 size=1880 all=53240 active=3577 piece=▁တယ်လီဖုန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=107 size=1900 all=53336 active=3673 piece=▁နှလုံး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=107 min_freq=28
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=106 size=1920 all=53535 active=2862 piece=များများ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=104 size=1940 all=53680 active=3007 piece=▁ဗုဒ္ဓ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=102 size=1960 all=53887 active=3214 piece=နေတဲ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=101 size=1980 all=54192 active=3519 piece=▁အစိုးရ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=99 size=2000 all=54442 active=3769 piece=▁ပေးပါ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=99 min_freq=26
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=98 size=2020 all=54651 active=2925 piece=▁နေ့လယ်စာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=96 size=2040 all=54864 active=3138 piece=▁ထိခိုက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=95 size=2060 all=55053 active=3327 piece=▁အိပ်ရာထ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=93 size=2080 all=55259 active=3533 piece=▁ညီလေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=91 size=2100 all=55417 active=3691 piece=▁ကနေ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=91 min_freq=25
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=90 size=2120 all=55613 active=2965 piece=▁အင်တာနက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=88 size=2140 all=55749 active=3101 piece=ပြေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=87 size=2160 all=55919 active=3271 piece=▁မုန့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=86 size=2180 all=56068 active=3420 piece=▁စုံစမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=85 size=2200 all=56175 active=3527 piece=▁တိုက်ခိုက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=84 min_freq=24
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=84 size=2220 all=56542 active=3171 piece=▁လှည့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=83 size=2240 all=56820 active=3449 piece=▁ရိုးရိုး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=82 size=2260 all=57006 active=3635 piece=▁ဘယ်နှစ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=80 size=2280 all=57123 active=3752 piece=ခို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=79 size=2300 all=57294 active=3923 piece=▁ကြာကြာ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=79 min_freq=23
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=78 size=2320 all=57524 active=3092 piece=▁ခဲ့သလဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=77 size=2340 all=57679 active=3247 piece=▁မဂ္ဂဇင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=76 size=2360 all=57891 active=3459 piece=▁တစ်ပတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=75 size=2380 all=58123 active=3691 piece=လှမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=74 size=2400 all=58322 active=3890 piece=▁အည
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=74 min_freq=22
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=74 size=2420 all=58464 active=3051 piece=▁စိတ်ဆိုး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=73 size=2440 all=58651 active=3238 piece=▁နည်းပညာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=71 size=2460 all=58828 active=3415 piece=▁လျော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=70 size=2480 all=58943 active=3530 piece=▁စာတိုက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=69 size=2500 all=59051 active=3638 piece=▁သင်္ကြန်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=69 min_freq=21
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=68 size=2520 all=59241 active=3141 piece=▁ဘုရင်မ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=67 size=2540 all=59385 active=3285 piece=တွန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=66 size=2560 all=59578 active=3478 piece=▁ဗီဇာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=65 size=2580 all=59675 active=3575 piece=ဌေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=65 size=2600 all=59880 active=3780 piece=▁တက္ကစီ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=65 min_freq=20
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=64 size=2620 all=60016 active=3130 piece=▁ခံစားချက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=63 size=2640 all=60229 active=3343 piece=သေချာချာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=62 size=2660 all=60453 active=3567 piece=▁ဥပဒေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=61 size=2680 all=60499 active=3613 piece=ကေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=61 size=2700 all=60723 active=3837 piece=▁ကုန်သွယ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=61 min_freq=19
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=60 size=2720 all=60799 active=3109 piece=▁ယူနန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=59 size=2740 all=61039 active=3349 piece=အလှန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=58 size=2760 all=61225 active=3535 piece=တာလား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=58 size=2780 all=61318 active=3628 piece=▁အနက်ရောင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=57 size=2800 all=61518 active=3828 piece=စ်ပို့
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=57 min_freq=18
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=56 size=2820 all=61620 active=3176 piece=▁နံရံ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=56 size=2840 all=61672 active=3228 piece=▁ပြည်တွင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=55 size=2860 all=61836 active=3392 piece=▁ပြောဆို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=54 size=2880 all=61957 active=3513 piece=▁ပါဆယ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=53 size=2900 all=62054 active=3610 piece=▁နွေး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=53 min_freq=18
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=52 size=2920 all=62138 active=3186 piece=ဘတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=52 size=2940 all=62329 active=3377 piece=▁ရှင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=51 size=2960 all=62375 active=3423 piece=ne
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=51 size=2980 all=62539 active=3587 piece=▁တာဝန်ယူ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=50 size=3000 all=62664 active=3712 piece=▁ကန့်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=50 min_freq=17
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=50 size=3020 all=62744 active=3211 piece=▁အများစု
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=49 size=3040 all=62859 active=3326 piece=ဆည်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=49 size=3060 all=63034 active=3501 piece=▁အရုပ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=48 size=3080 all=63123 active=3590 piece=▁b
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=48 size=3100 all=63367 active=3834 piece=▁အတတ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=48 min_freq=16
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=48 size=3120 all=63465 active=3263 piece=▁ရုပ်ရှင်ရုံ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=47 size=3140 all=63621 active=3419 piece=▁ကင်ဆာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=46 size=3160 all=63736 active=3534 piece=ဗာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=46 size=3180 all=63934 active=3732 piece=▁အိန္ဒ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=46 size=3200 all=63982 active=3780 piece=▁နိုင်ငံတော်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=46 min_freq=16
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=45 size=3220 all=64172 active=3386 piece=▁သမား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=45 size=3240 all=64257 active=3471 piece=▁မိဖုရား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=44 size=3260 all=64320 active=3534 piece=▁Re
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=44 size=3280 all=64440 active=3654 piece=▁တီထွင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=43 size=3300 all=64486 active=3700 piece=ဇင်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=43 min_freq=15
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=43 size=3320 all=64630 active=3362 piece=▁မွှေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=43 size=3340 all=64658 active=3390 piece=▁အကြောင်းအရာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=42 size=3360 all=64830 active=3562 piece=နေပြီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=42 size=3380 all=64911 active=3643 piece=▁ကိုကျော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=41 size=3400 all=64984 active=3716 piece=မူး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=41 min_freq=15
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=41 size=3420 all=65171 active=3426 piece=▁ပေါင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=41 size=3440 all=65239 active=3494 piece=▁အဆောက်အအုံ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=40 size=3460 all=65498 active=3753 piece=ဆော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=40 size=3480 all=65646 active=3901 piece=▁မတော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=40 size=3500 all=65687 active=3942 piece=မြှုပ်နှံ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=40 min_freq=14
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=39 size=3520 all=65856 active=3449 piece=▁ဓလေ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=39 size=3540 all=65926 active=3519 piece=ဖော်ကိုင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=38 size=3560 all=65984 active=3577 piece=▁#
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=38 size=3580 all=66189 active=3782 piece=▁စွပ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=38 size=3600 all=66281 active=3874 piece=▁တက်ကြွ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=38 min_freq=14
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=38 size=3620 all=66317 active=3347 piece=▁အတော်လေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=37 size=3640 all=66410 active=3440 piece=နင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=37 size=3660 all=66560 active=3590 piece=▁ရှိုး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=37 size=3680 all=66656 active=3686 piece=ကောင်းတဲ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=36 size=3700 all=66699 active=3729 piece=ေဒ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=36 min_freq=13
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=36 size=3720 all=66887 active=3518 piece=▁လက်ခ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=36 size=3740 all=66933 active=3564 piece=▁အခုတလော
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=35 size=3760 all=67031 active=3662 piece=▁၃၅
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=35 size=3780 all=67157 active=3788 piece=▁သို့သ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=35 size=3800 all=67208 active=3839 piece=▁တိုင်ပင်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=35 min_freq=13
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=34 size=3820 all=67297 active=3446 piece=နု
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=34 size=3840 all=67556 active=3705 piece=နှင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=34 size=3860 all=67655 active=3804 piece=▁နာကျင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=34 size=3880 all=67669 active=3818 piece=▁လည်ချောင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=33 size=3900 all=67856 active=4005 piece=ေးလျ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=33 min_freq=13
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=33 size=3920 all=67995 active=3528 piece=▁စခန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=33 size=3940 all=68032 active=3565 piece=▁နောက်မကျ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=32 size=3960 all=68143 active=3676 piece=ညမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=32 size=3980 all=68254 active=3787 piece=▁ငြိမ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=32 size=4000 all=68299 active=3832 piece=▁အသံထွက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=32 min_freq=12
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=31 size=4020 all=68337 active=3452 piece=ဗေဒ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=31 size=4040 all=68504 active=3619 piece=အချက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=31 size=4060 all=68603 active=3718 piece=▁ရေးသား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=31 size=4080 all=68637 active=3752 piece=▁သို့သော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=30 size=4100 all=68680 active=3795 piece=ox
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=30 min_freq=12
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=30 size=4120 all=68822 active=3558 piece=▁ဗဟို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=30 size=4140 all=68882 active=3618 piece=▁သစ်သား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=30 size=4160 all=68912 active=3648 piece=▁မေးမြန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=30 size=4180 all=68924 active=3660 piece=▁အွန်လိုင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=29 size=4200 all=69100 active=3836 piece=▁စူ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=29 min_freq=12
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=29 size=4220 all=69221 active=3571 piece=မောက္ခ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=29 size=4240 all=69277 active=3627 piece=▁ကာတွန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=29 size=4260 all=69300 active=3650 piece=▁မွေးဖွား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=29 size=4280 all=69319 active=3669 piece=▁အရေးကြီးဆုံး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=28 size=4300 all=69527 active=3877 piece=ပုံး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=28 min_freq=11
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=28 size=4320 all=69608 active=3549 piece=▁မူမူ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=28 size=4340 all=69694 active=3635 piece=▁တပ်ဆင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=28 size=4360 all=69727 active=3668 piece=▁ဟင့်အင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=28 size=4380 all=69730 active=3671 piece=▁သန့်ရှင်းရေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=27 size=4400 all=69845 active=3786 piece=ဂျစ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=27 min_freq=11
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=27 size=4420 all=69971 active=3611 piece=▁စွန့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=27 size=4440 all=69996 active=3636 piece=▁တိုကျို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=27 size=4460 all=70022 active=3662 piece=▁လိုင်စင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4480 all=70016 active=3656 piece=TV
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4500 all=70216 active=3856 piece=ဝှေ့
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=26 min_freq=11
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4520 all=70358 active=3643 piece=မှုန့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4540 all=70435 active=3720 piece=▁မူရင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4560 all=70446 active=3731 piece=▁နင်တို့က
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=26 size=4580 all=70452 active=3737 piece=▁အဆင့်မြင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4600 all=70584 active=3869 piece=ညှိ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=25 min_freq=10
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4620 all=70729 active=3658 piece=မှုတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4640 all=70819 active=3748 piece=▁ဦးမယ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4660 all=70880 active=3809 piece=▁တကယ်ကို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4680 all=70898 active=3827 piece=▁ပြန်အမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=25 size=4700 all=70901 active=3830 piece=▁ဝမ်းမြောက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=25 min_freq=10
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4720 all=71041 active=3684 piece=▁ရီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4740 all=71144 active=3787 piece=▁နေပါ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4760 all=71187 active=3830 piece=▁လှုံ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4780 all=71223 active=3866 piece=▁လိုတယ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4800 all=71246 active=3889 piece=▁ညီအစ်ကို
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=24 min_freq=10
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=24 size=4820 all=71255 active=3570 piece=▁ပြီးပြီလား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4840 all=71401 active=3716 piece=ဏ္ဍာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4860 all=71509 active=3824 piece=▁ဂရမ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4880 all=71585 active=3900 piece=▁အာဟာရ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4900 all=71640 active=3955 piece=▁အနိမ့်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=23 min_freq=10
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4920 all=71657 active=3599 piece=▁နိုဝင်ဘာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=23 size=4940 all=71680 active=3622 piece=▁ကောင်းကျိုး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=4960 all=71831 active=3773 piece=ပက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=4980 all=71969 active=3911 piece=▁ကနေ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=5000 all=72089 active=4031 piece=▁ငလျင်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=22 min_freq=9
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=5020 all=72156 active=3669 piece=▁မျောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=5040 all=72203 active=3716 piece=▁အတော်ပဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22 size=5060 all=72228 active=3741 piece=▁စားသုံးသူ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5080 all=72261 active=3774 piece=arn
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5100 all=72428 active=3941 piece=▁၃၂
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=21 min_freq=9
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5120 all=72530 active=3721 piece=▁စျေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5140 all=72576 active=3767 piece=▁ရုန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5160 all=72608 active=3799 piece=ရင်းနှီး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5180 all=72622 active=3813 piece=▁လမ်းပန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5200 all=72639 active=3830 piece=▁နေထိုင်မှု
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=21 min_freq=9
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=21 size=5220 all=72638 active=3631 piece=▁မြောက်မြားစွာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5240 all=72813 active=3806 piece=▁Ad
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5260 all=72960 active=3953 piece=▁Mic
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5280 all=73063 active=4056 piece=▁ဆယ့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5300 all=73117 active=4110 piece=▁ခုလို
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=20 min_freq=9
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5320 all=73149 active=3687 piece=▁ဆေးရည်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5340 all=73180 active=3718 piece=▁မြေကြီး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5360 all=73207 active=3745 piece=▁သိမ်းထား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5380 all=73216 active=3754 piece=▁အိပ်ရာဝင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=20 size=5400 all=73210 active=3748 piece=▁သဘောတူညီချက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=20 min_freq=9
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5420 all=73326 active=3777 piece=ဇာတ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5440 all=73416 active=3867 piece=စိုး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5460 all=73522 active=3973 piece=အိုင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5480 all=73575 active=4026 piece=ဖွယ်ရာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5500 all=73620 active=4071 piece=▁ထူးထူး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=19 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5520 all=73634 active=3693 piece=▁နေပါပြီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5540 all=73642 active=3701 piece=▁ဖြစ်သွား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=19 size=5560 all=73658 active=3717 piece=▁ရက်သတ္တပတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5580 all=73671 active=3730 piece=ရု
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5600 all=73834 active=3893 piece=▁ယိ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=18 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5620 all=73936 active=3791 piece=▁တာ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5640 all=74030 active=3885 piece=▁နန်န
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5660 all=74065 active=3920 piece=▁ညီမျှ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5680 all=74102 active=3957 piece=▁ခဲ့လား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5700 all=74125 active=3980 piece=▁ငယ်ရွယ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=18 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5720 all=74141 active=3717 piece=▁ကိုယ်ဝန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5740 all=74150 active=3726 piece=▁လိမ်းဆေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5760 all=74148 active=3724 piece=▁ရွှေရောင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=18 size=5780 all=74153 active=3729 piece=▁ပြောင်းပြန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5800 all=74212 active=3788 piece=▁Z
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=17 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5820 all=74334 active=3822 piece=ဆယ့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5840 all=74447 active=3935 piece=▁ကြွေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5860 all=74503 active=3991 piece=▁ချို့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5880 all=74563 active=4051 piece=အားလုံး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5900 all=74571 active=4059 piece=▁အရောက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=17 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5920 all=74590 active=3745 piece=▁ဘာသာရပ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5940 all=74597 active=3752 piece=▁မလေးရှား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5960 all=74591 active=3746 piece=▁အားသာချက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=17 size=5980 all=74582 active=3737 piece=▁လျှပ်စစ်မီး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6000 all=74645 active=3800 piece=၄၈
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=16 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6020 all=74785 active=3867 piece=ဆို့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6040 all=74889 active=3971 piece=ကွန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6060 all=74967 active=4049 piece=▁ဟဲဟဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6080 all=75048 active=4130 piece=▁ဂရိတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6100 all=75079 active=4161 piece=▁စုံစုံ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=16 min_freq=8
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6120 all=75092 active=3765 piece=နိုင်မှု
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6140 all=75114 active=3787 piece=▁အထွေထွေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6160 all=75118 active=3791 piece=▁အကုန်အကျ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6180 all=75117 active=3790 piece=▁အမြန်ချော
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6200 all=75106 active=3779 piece=▁လက်နှိပ်စက်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=16 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=16 size=6220 all=75092 active=3741 piece=▁တောင်ကိုရီးယား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6240 all=75242 active=3891 piece=ကြဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6260 all=75367 active=4016 piece=စတန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6280 all=75449 active=4098 piece=ညှင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6300 all=75517 active=4166 piece=▁လောဘ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=15 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6320 all=75541 active=3798 piece=▁မကျက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6340 all=75558 active=3815 piece=▁ကြာပြီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6360 all=75571 active=3828 piece=▁SWINGIN
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6380 all=75584 active=3841 piece=▁လက်ငင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6400 all=75611 active=3868 piece=▁ပြန်သွား
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=15 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6420 all=75605 active=3775 piece=▁စစ်ကိုင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6440 all=75604 active=3774 piece=▁တိုးမြှင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=15 size=6460 all=75603 active=3773 piece=▁ဖြစ်နိုင်ခြေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6480 all=75700 active=3870 piece=ငန်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6500 all=75777 active=3947 piece=ညင်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=14 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6520 all=75896 active=3896 piece=▁ဇီဝ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6540 all=75934 active=3934 piece=▁ထိတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6560 all=75962 active=3962 piece=တောင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6580 all=76015 active=4015 piece=▁လာခဲ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6600 all=76041 active=4041 piece=▁ဆိုးလ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=14 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6620 all=76050 active=3812 piece=▁အကျော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6640 all=76078 active=3840 piece=▁ထိုင်ပါ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6660 all=76091 active=3853 piece=▁ကန်ပေါင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6680 all=76097 active=3859 piece=▁လှော်ကား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6700 all=76099 active=3861 piece=▁လေ့ရှိတယ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=14 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6720 all=76102 active=3808 piece=▁အသင့်မဖြစ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=14 size=6740 all=76089 active=3795 piece=▁မိမိကိုယ်ကို
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6760 all=76135 active=3841 piece=ys
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6780 all=76264 active=3970 piece=အဆာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6800 all=76351 active=4057 piece=ဆုန်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=13 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6820 all=76423 active=3886 piece=ကျဉ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6840 all=76476 active=3939 piece=▁လူစု
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6860 all=76545 active=4008 piece=▁ကျရင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6880 all=76560 active=4023 piece=မယ်လို့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6900 all=76581 active=4044 piece=▁ပြောသံ
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=13 min_freq=7
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6920 all=76590 active=3838 piece=▁အသုံးအ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6940 all=76628 active=3876 piece=▁စွဲလမ်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6960 all=76633 active=3881 piece=▁အိပ်ရေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=6980 all=76643 active=3891 piece=▁လှည့်လည်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=7000 all=76654 active=3902 piece=▁တောရိုင်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=13 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=7020 all=76653 active=3831 piece=▁မနက်တိုင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13 size=7040 all=76651 active=3829 piece=▁သွားတိုက်ဆေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7060 all=76753 active=3931 piece=ltr
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7080 all=76843 active=4021 piece=hite
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7100 all=76945 active=4123 piece=▁ဒစ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=12 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7120 all=76997 active=3897 piece=နှင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7140 all=77071 active=3971 piece=▁ဂျာမ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7160 all=77088 active=3988 piece=စမ်းပါ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7180 all=77138 active=4038 piece=▁ပုံသေ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7200 all=77155 active=4055 piece=ပင်ပန်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=12 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7220 all=77170 active=3868 piece=▁ပေါ်လာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7240 all=77191 active=3889 piece=▁Broadus
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7260 all=77194 active=3892 piece=▁ရုံးခွဲ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7280 all=77199 active=3897 piece=▁ခွက်များ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7300 all=77204 active=3902 piece=▁လန်းဆန်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=12 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7320 all=77210 active=3865 piece=▁ကျွန်မရဲ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7340 all=77206 active=3861 piece=▁အကန့်အသတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7360 all=77205 active=3860 piece=▁မြို့တွင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7380 all=77205 active=3860 piece=▁နေရောင်ခြည်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=12 size=7400 all=77190 active=3845 piece=▁အသိုင်းအဝိုင်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=12 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7420 all=77307 active=3977 piece=der
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7440 all=77430 active=4100 piece=▁No
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7460 all=77536 active=4206 piece=လက်စ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7480 all=77594 active=4264 piece=ဗွီဒီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7500 all=77635 active=4305 piece=▁မအေး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=11 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7520 all=77687 active=3932 piece=▁ကြိတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7540 all=77692 active=3937 piece=▁ရဟန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7560 all=77723 active=3968 piece=တစ်ဆင့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7580 all=77753 active=3998 piece=▁တစ်ရက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7600 all=77761 active=4006 piece=▁အပြင်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=11 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7620 all=77786 active=3910 piece=▁ကူညီပေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7640 all=77775 active=3899 piece=▁နဲ့အမျှ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7660 all=77783 active=3907 piece=▁အလျောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7680 all=77794 active=3918 piece=▁ပြည့်စုံ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7700 all=77791 active=3915 piece=▁အရူးအမူး
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=11 min_freq=6
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7720 all=77799 active=3898 piece=▁ဖျောင်းဖျ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=11 size=7740 all=77795 active=3894 piece=▁ချစ်စရာလေး
trainer_interface.cc(606) LOG(INFO) Saving model: word-bpe.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: word-bpe.vocab

real	0m2.632s
user	0m2.929s
sys	0m0.052s
```

လက်ရှိ ဆိုရင် စုစုပေါင်း မော်ဒယ် သုံးဖိုင် ရှိနေပါပြီ။ model ရဲ့ file zie ကိုလည်း ကြည့်ကြည့်ပါ။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll *.model -h
-rw-r--r-- 1 ye ye 251K စက်   20 18:13 syl-unigram.model
-rw-r--r-- 1 ye ye 445K စက်   20 18:17 word-bpe.model
-rw-r--r-- 1 ye ye 447K စက်   20 18:07 word-unigram.model
```

### Syllable BPE

```
Syllable BPE မှာလည်း error ထွက်တယ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-bpe --vocab_size=8000 --character_coverage=1.0 --model_type=bpe
...
...
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=0 min_freq=0
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=0 size=5320 all=283 active=41 piece=▁ဟင်္သ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=0 size=5340 all=263 active=21 piece=▁ဓိပ္ပာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=0 size=5360 all=243 active=1 piece=တ္ထုပ္ပတ္တိ
bpe_model_trainer.cc(242) LOG(WARNING) No valid symbol found
trainer_interface.cc(606) LOG(INFO) Saving model: syl-bpe.model
spm_train_main.cc(214) [_status.ok()] Internal: /home/ye/tool/sentencepiece/src/trainer_interface.cc(581) [(trainer_spec_.vocab_size()) == (model_proto->pieces_size())] Vocabulary size too high (8000). Please set it to a value <= 5605.
Program terminated with an unrecoverable error.

real	0m0.852s
user	0m1.189s
sys	0m0.041s
```


### Build Again with Smaller Vocab Size

vocab size ကို 1000 ထားပြီး ဆောက်ကြည့်တော့ OK တယ် ...  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-bpe --vocab_size=1000 --character_coverage=1.0 --model_type=bpe
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-bpe
  model_type: BPE
  vocab_size: 1000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(518) LOG(INFO) Tokenizing input sentences with whitespace: 92458
trainer_interface.cc(528) LOG(INFO) Done! 3259
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=157203 min_freq=1
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=37720 size=20 all=1809 active=1512 piece=င်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=22529 size=40 all=2247 active=1950 piece=▁ထ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=13696 size=60 all=2541 active=2244 piece=မ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=9570 size=80 all=2838 active=2541 piece=▁ငါ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=7447 size=100 all=2988 active=2691 piece=▁တော့
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=7330 min_freq=48
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=5051 size=120 all=3156 active=1166 piece=▁ဘာ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=3942 size=140 all=3198 active=1208 piece=ည့်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=3147 size=160 all=3337 active=1347 piece=▁ယောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=2572 size=180 all=3406 active=1416 piece=ုန်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=2217 size=200 all=3513 active=1523 piece=▁အိမ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=2213 min_freq=54
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1918 size=220 all=3543 active=1030 piece=▁ချက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1681 size=240 all=3561 active=1048 piece=▁မှတ်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1486 size=260 all=3579 active=1066 piece=▁ခါ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1355 size=280 all=3584 active=1071 piece=▁ကောင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1269 size=300 all=3596 active=1083 piece=ွန်း
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=1264 min_freq=44
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1126 size=320 all=3613 active=999 piece=▁ကြား
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=1003 size=340 all=3634 active=1020 piece=▁မေး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=920 size=360 all=3648 active=1034 piece=▁လေ့
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=854 size=380 all=3666 active=1052 piece=▁-
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=799 size=400 all=3691 active=1077 piece=▁အိတ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=798 min_freq=35
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=751 size=420 all=3749 active=1058 piece=▁ပူ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=687 size=440 all=3774 active=1083 piece=▁ကိစ္စ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=627 size=460 all=3799 active=1108 piece=▁ထောက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=593 size=480 all=3796 active=1105 piece=▁ကမ္ဘ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=553 size=500 all=3835 active=1144 piece=▁၆
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=553 min_freq=28
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=518 size=520 all=3821 active=986 piece=▁အော်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=482 size=540 all=3828 active=993 piece=▁ဏီ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=447 size=560 all=3842 active=1007 piece=▁ပြိုင်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=414 size=580 all=3844 active=1009 piece=▁စိုက်
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=386 size=600 all=3864 active=1029 piece=▁ကွယ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=383 min_freq=21
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=361 size=620 all=3853 active=989 piece=▁တီး
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=342 size=640 all=3849 active=985 piece=▁သင်း
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=324 size=660 all=3861 active=997 piece=▁f
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=304 size=680 all=3867 active=1003 piece=▁တက္က
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=290 size=700 all=3856 active=992 piece=▁ကျပ်
bpe_model_trainer.cc(167) LOG(INFO) Updating active symbols. max_freq=290 min_freq=15
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=275 size=720 all=3871 active=1016 piece=▁လုံ
bpe_model_trainer.cc(258) LOG(INFO) Added: freq=261 size=740 all=3882 active=1027 piece=▁ဆန်
trainer_interface.cc(606) LOG(INFO) Saving model: syl-bpe.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: syl-bpe.vocab

real	0m0.714s
user	0m1.056s
sys	0m0.028s
```

Check the output model ...   

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ls *.model
syl-bpe.model  syl-unigram.model  word-bpe.model  word-unigram.model
```

## Build Char

### Build Word Char

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my --model_prefix=word-char --vocab_size=8000 --character_coverage=1.0 --model_type=char
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my
  input_format: 
  model_prefix: word-char
  model_type: CHAR
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=4810538
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(606) LOG(INFO) Saving model: word-char.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: word-char.vocab

real	0m0.524s
user	0m0.855s
sys	0m0.016s
```

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ls *.model
syl-bpe.model  syl-unigram.model  word-bpe.model  word-char.model  word-unigram.model
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll -h *.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:22 syl-bpe.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:13 syl-unigram.model
-rw-r--r-- 1 ye ye 445K စက်   20 18:17 word-bpe.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:25 word-char.model
-rw-r--r-- 1 ye ye 447K စက်   20 18:07 word-unigram.model
```

char model အတွက်က vocab size ကို ပြောင်းကြည့်လဲ အတူတူပဲဆိုတာကို တွေ့ရတယ်

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my --model_prefix=word-char --vocab_size=1000 --character_coverage=1.0 --model_type=char
```

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll -h *.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:22 syl-bpe.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:13 syl-unigram.model
-rw-r--r-- 1 ye ye 445K စက်   20 18:17 word-bpe.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:28 word-char.model
-rw-r--r-- 1 ye ye 447K စက်   20 18:07 word-unigram.model
```

### Build char Model with Syllable Segmented Training Data

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-char --vocab_size=1000 --character_coverage=1.0 --model_type=char
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-char
  model_type: CHAR
  vocab_size: 1000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(606) LOG(INFO) Saving model: syl-char.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: syl-char.vocab

real	0m0.554s
user	0m0.918s
sys	0m0.020s
```

char model မှာက word နဲ့ပဲ ဆောက်ဆောက် syllable ဖြတ်ပြီးတော့ပဲ ဆောက်ဆောက် ထွက်လာတဲ့ output model မှာ size က အတူတူပဲ ဆိုတာကို confirmation လုပ်ခဲ့တယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll -h {syl-char,word-char}.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:31 syl-char.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:28 word-char.model
```

## Build word Model with Word Segmented Training Data

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my --model_prefix=word-word --vocab_size=8000 --character_coverage=1.0 --model_type=word
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my
  input_format: 
  model_prefix: word-word
  model_type: WORD
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=4810538
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(606) LOG(INFO) Saving model: word-word.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: word-word.vocab

real	0m0.686s
user	0m1.016s
sys	0m0.012s

(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll -h *.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:22 syl-bpe.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:31 syl-char.model
-rw-r--r-- 1 ye ye 251K စက်   20 18:13 syl-unigram.model
-rw-r--r-- 1 ye ye 445K စက်   20 18:17 word-bpe.model
-rw-r--r-- 1 ye ye 235K စက်   20 18:28 word-char.model
-rw-r--r-- 1 ye ye 447K စက်   20 18:07 word-unigram.model
-rw-r--r-- 1 ye ye 499K စက်   20 18:34 word-word.model
```

### Build word Model with Syllable Segmented Training Data

အောက်ပါအတိုင်း error ပေးတယ်

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-word --vocab_size=8000 --character_coverage=1.0 --model_type=word
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-word
  model_type: WORD
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(606) LOG(INFO) Saving model: syl-word.model
spm_train_main.cc(214) [_status.ok()] Internal: /home/ye/tool/sentencepiece/src/trainer_interface.cc(581) [(trainer_spec_.vocab_size()) == (model_proto->pieces_size())] Vocabulary size too high (8000). Please set it to a value <= 3262.
Program terminated with an unrecoverable error.

real	0m0.678s
user	0m1.021s
sys	0m0.028s
```

### Change vocab size

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ time spm_train --input=./big-lm2.my.syl.clean --model_prefix=syl-word --vocab_size=1000 --character_coverage=1.0 --model_type=word
sentencepiece_trainer.cc(79) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./big-lm2.my.syl.clean
  input_format: 
  model_prefix: syl-word
  model_type: WORD
  vocab_size: 1000
  self_test_sample_size: 0
  character_coverage: 1
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(321) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(176) LOG(INFO) Loading corpus: ./big-lm2.my.syl.clean
trainer_interface.cc(377) LOG(INFO) Loaded all 92458 sentences
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(392) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(397) LOG(INFO) Normalizing sentences...
trainer_interface.cc(458) LOG(INFO) all chars count=5276647
trainer_interface.cc(479) LOG(INFO) Alphabet size=242
trainer_interface.cc(480) LOG(INFO) Final character coverage=1
trainer_interface.cc(512) LOG(INFO) Done! preprocessed 92458 sentences.
trainer_interface.cc(606) LOG(INFO) Saving model: syl-word.model
trainer_interface.cc(617) LOG(INFO) Saving vocabs: syl-word.vocab

real	0m0.693s
user	0m1.036s
sys	0m0.028s
```

ထင်ထားတဲ့အတိုင်းပါပဲ word မော်ဒယ်အတွက်က syllable ဖြတ်ပြီး ဆောက်တာနဲ့ word segmentation လုပ်ပြီး ဆောက်တာရဲ့ output မော်ဒယ်တွေက မတူပါဘူး။ အောက်ပါအတိုင်းပါပဲ  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ ll -h {word-word,syl-word}.model
-rw-r--r-- 1 ye ye 254K စက်   20 18:36 syl-word.model
-rw-r--r-- 1 ye ye 499K စက်   20 18:34 word-word.model
```

# Applying

command line syntax က အောက်ပါအတိုင်း  
spm_encode --model=<model_file> --output_format=piece < input > output  
spm_encode --model=<model_file> --output_format=id < input > output

## Segmentation on test1.txt

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-unigram.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ် လ ိ ု ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျ ောင်း ▁သူ ▁တ စ် ▁ယောက် ▁ပါ
▁အ ▁ရမ်း ▁ဆော့ ▁တဲ့ ▁က လ ေး ▁က ▁ကျန် း ▁မာ ▁တယ်
▁အ ခ ု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စ က် ▁တင် ▁ဘာ ▁လ ▁ ၁ ၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆ န္ဒ ▁ပြ ▁ပွဲ ▁ကျင် း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ် စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံ း ▁တက် ▁တဲ့ ▁ဘိ လ ပ် ▁ပြန် ▁ညွှန် ▁ကြာ း ▁ရေး ▁မှ ူး ▁ချုပ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-unigram.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ
▁အ ▁ရ မ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ်
▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁က ျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိလပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁ မှူး ▁ချုပ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-bpe.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ် လ ို ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ
▁အ ▁ရမ်း ▁ဆ ော့ ▁တဲ့ ▁က လ ေး ▁က ▁ကျန်း ▁မာ ▁တယ်
▁အ ခ ု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁ ၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆ န္ ဒ ▁ပြ ▁ပွဲ ▁ကျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘ ိ လ ပ် ▁ပြန် ▁ည ွှ န် ▁ကြား ▁ရေး ▁မှ ူး ▁ချုပ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-bpe.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ
▁အ ▁ရ မ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ်
▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁ကျ င်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိ လပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁မှ ူး ▁ချုပ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-char.model --output_format=piece < ./test1.txt
▁ မ င ် း ▁ က ိ ု ▁ င ါ ▁ ဘ ယ ် လ ိ ု ▁ ခ ေ ါ ် ▁ ရ ▁ မ ▁ လ ဲ
▁ စ ာ ▁ တ ေ ာ ် ▁ တ ဲ ့ ▁ က ျ ေ ာ င ် း ▁ သ ူ ▁ တ စ ် ▁ ယ ေ ာ က ် ▁ ပ ါ
▁ အ ▁ ရ မ ် း ▁ ဆ ေ ာ ့ ▁ တ ဲ ့ ▁ က လ ေ း ▁ က ▁ က ျ န ် း ▁ မ ာ ▁ တ ယ ်
▁ အ ခ ု ▁ တ ေ ာ ့ ▁ ပ ါ ▁ န က ် ▁ ဆ ▁ ရ ာ ▁ ဟ ာ ▁ စ က ် ▁ တ င ် ▁ ဘ ာ ▁ လ ▁ ၁ ၉ ▁ ရ က ် ▁ န ေ ့ ▁ မ ှ ာ ▁ ဆ န ္ ဒ ▁ ပ ြ ▁ ပ ွ ဲ ▁ က ျ င ် း ▁ ပ ▁ ဖ ိ ု ့ ▁ အ ▁ တ ွ က ် ▁ ပ ြ င ် ▁ ဆ င ် ▁ န ေ ▁ ပ ါ ▁ တ ယ ် ▁ ။
▁ ဘ တ ် စ ် ▁ က ာ း ▁ စ ီ း ▁ ပ ြ ီ း ▁ ရ ု ံ း ▁ တ က ် ▁ တ ဲ ့ ▁ ဘ ိ လ ပ ် ▁ ပ ြ န ် ▁ ည ွ ှ န ် ▁ က ြ ာ း ▁ ရ ေ း ▁ မ ှ ူ း ▁ ခ ျ ု ပ ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-char.model --output_format=piece < ./test1.txt
▁ မ င ် း ▁ က ိ ု ▁ င ါ ▁ ဘ ယ ် လ ိ ု ▁ ခ ေ ါ ် ▁ ရ ▁ မ ▁ လ ဲ
▁ စ ာ ▁ တ ေ ာ ် ▁ တ ဲ ့ ▁ က ျ ေ ာ င ် း ▁ သ ူ ▁ တ စ ် ▁ ယ ေ ာ က ် ▁ ပ ါ
▁ အ ▁ ရ မ ် း ▁ ဆ ေ ာ ့ ▁ တ ဲ ့ ▁ က လ ေ း ▁ က ▁ က ျ န ် း ▁ မ ာ ▁ တ ယ ်
▁ အ ခ ု ▁ တ ေ ာ ့ ▁ ပ ါ ▁ န က ် ▁ ဆ ▁ ရ ာ ▁ ဟ ာ ▁ စ က ် ▁ တ င ် ▁ ဘ ာ ▁ လ ▁ ၁ ၉ ▁ ရ က ် ▁ န ေ ့ ▁ မ ှ ာ ▁ ဆ န ္ ဒ ▁ ပ ြ ▁ ပ ွ ဲ ▁ က ျ င ် း ▁ ပ ▁ ဖ ိ ု ့ ▁ အ ▁ တ ွ က ် ▁ ပ ြ င ် ▁ ဆ င ် ▁ န ေ ▁ ပ ါ ▁ တ ယ ် ▁ ။
▁ ဘ တ ် စ ် ▁ က ာ း ▁ စ ီ း ▁ ပ ြ ီ း ▁ ရ ု ံ း ▁ တ က ် ▁ တ ဲ ့ ▁ ဘ ိ လ ပ ် ▁ ပ ြ န ် ▁ ည ွ ှ န ် ▁ က ြ ာ း ▁ ရ ေ း ▁ မ ှ ူ း ▁ ခ ျ ု ပ ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-word.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ
▁အ ▁ရမ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ်
▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁ကျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိလပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁မှူး ▁ချုပ်
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-word.model --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ
▁အ ▁ရမ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ်
▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁ကျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိလပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁မှူး ▁ချုပ်
```

## Segmentation on test2.raw

ဒီ test2.raw ကတော့ BBC မြန်မာ ကနေ ယူထားတဲ့ စာကြောင်းပါ။ Segmentation မလုပ်ထားပါဘူး။   
အောက်ပါ command ကို run ပါမယ်။  

```
spm_encode --model=syl-unigram.model --output_format=piece < ./test2.raw  
spm_encode --model=word-unigram.model --output_format=piece < ./test2.raw  
spm_encode --model=syl-bpe.model --output_format=piece < ./test2.raw  
spm_encode --model=word-bpe.model --output_format=piece < ./test2.raw  
spm_encode --model=syl-char.model --output_format=piece < ./test2.raw  
spm_encode --model=word-char.model --output_format=piece < ./test2.raw  
spm_encode --model=syl-word.model --output_format=piece < ./test2.raw  
spm_encode --model=word-word.model --output_format=piece < ./test2.raw  
```

moel တစ်ခုချင်းစီရဲ့ ထွက်လာတဲ့ output တွေကို လေ့လာကြည့်ကြရအောင်   

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-unigram.model --output_format=piece < ./test2.raw
▁နိုင် င ံ တ ခ ု ▁ထူ ထ ောင် တ ဲ့ အ ခ ါ မ ှ ာ ▁စစ် တ ပ် ၊ ▁စီး ပ ွ ား ရ ေး လ ုပ် င န်း တ ွ ေ န ဲ့ ▁တ ရ ား ရ ုံး စ တ ဲ့ ▁ပင် မ အ ဖ ွဲ ့ အ စ ည်း တ ွ ေ သ ာ မ က ▁စာ ပ ေ ▁ယဉ် က ျ ေး မ ှ ု ▁စ ိတ် ဓ ာ တ် ပ ိုင်း က လ ည်း ▁နိုင် င ံ သ ိ စ ိတ် ▁ချစ် စ ိတ် တ ွ ေ ▁ပေါ် လာ အ ောင် ▁ဆ ော် ဩ ▁ပေး ရ ပ ါ တ ယ် ။ ▁ဒါ က ိ ု သ ိ တ ဲ့ ▁လူ က ြ ီး ပ ိုင်း က ▁မြန် မ ာ ပ ြ ည ် အ တ ွက် ▁ပြ တ ိုက် ▁စာ က ြ ည ့ ် တ ိုက် န ဲ့ ▁အ န ု ပ ည ာ တ ိုက် တ ွ ေ ▁ရှိ ဖ ိ ု ့ လ ိ ု တ ဲ့ အ က ြ ောင်း ▁ကို လ ိ ု န ီ ခ ေ တ် က စ ပ ြ ီး ▁တိုက် တ ွ န်း ခ ဲ့ က ြ သ လ ိ ု ▁ဒီ ယ ဉ် က ျ ေး မ ှ ု ▁အ ဆ ောက် အ ဦ တ ွ ေ က ိ ု ▁ကွ ပ် က ဲ ဖ ိ ု ့ ▁အ တ ွက် ▁ပ ည ာ ရ ှ င် တ ွ ေ ▁ပေါ် ထ ွက် ဖ ိ ု ့ လ ည်း ▁ကမ္ဘာ စ စ် ▁မ ဖ ြ စ် ခ င် က တ ည်း က ▁စ ိုင်း ပ ြ င်း ခ ဲ့ က ြ ပ ါ တ ယ် ။ ▁ဒါ က ြ ေ ာ င ့ ် ▁ဦး ခ င် ဇ ော် န ဲ့ ▁ဦး သ ိန်း ဟ န် က ိ ု ▁ပိ ဋ က တ် တ ိုက် ပ ည ာ လ ိ ု ့ ▁ခေါ် တ ဲ့ ▁စာ က ြ ည ့ ် တ ိုက် လ ုပ် င န်း အ တ ွက် ▁ဗ ြိ တ ိန် က ိ ု ▁စေ လ ွ ှ တ် ခ ဲ့ ▁သ လ ိ ု ▁ပန် း ခ ျ ီ ပ ည ာ သ င် အ ဖ ြ စ် ▁ဦး ဘ ဉ ာ ဏ် န ဲ့ ▁ဦး ဘ ဇ ော် က ိ ု လ ည်း ▁ဒီ ့ အ ရ င် က တ ည်း က ▁လန် ဒ န် က ိ ု ▁ပို့ ခ ဲ့ ပ ါ တ ယ် ။

▁ဒါ ပ ေ မ ဲ့ ▁ကို လ ိ ု န ီ ခ ေ တ် မ ြန် မ ာ န ိုင် င ံ မ ှ ာ ▁အဲ ဒ ီ အ ခ ျ ိန် ထ ိ ▁အ မ ျ ိုး သ ား စ ာ က ြ ည ့ ် တ ိုက် န ဲ့ ▁ပြ တ ိုက် ၊ ▁အ န ု ပ ည ာ ပ ြ ခ န်း တ ွ ေ ▁မ ရ ှ ိ သ ေး ဘ ဲ ▁ရန် က ုန် ▁တ က္က သ ိုလ် ▁ပိ ဋ က တ် တ ိုက် န ဲ့ ▁ရန် က ုန် မ ြိ ု ့ ထ ဲ က ▁ဗာ း န တ် ပ ိ ဋ က တ် တ ိုက် န ဲ့ ▁ပြ တ ိုက် အ ပ ြ င် ▁ပြည် န ား က ▁မှ ော် ဇ ာ ၊ ▁ရ ခ ိုင် က ▁မြ ောက် ဦ း န ဲ့ ▁အ ည ာ က ▁ပု ဂ ံ ၊ ▁ရွှေ ဘ ိ ု န ဲ့ ▁မ န္တ လ ေး မ ှ ာ ▁က မ ္ပ ည်း က ျ ောက် စ ာ ဌ ာ န ▁ပြ တ ိုက် က လ ေး တ ွ ေ ပ ဲ ▁ရှိ ခ ဲ့ ပ ါ တ ယ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-unigram.model --output_format=piece < ./test2.raw
▁နိုင်ငံ တ ခု ▁ထူထောင် တဲ့ အခါ မှာ ▁စစ်တပ် ၊ ▁စီးပွားရေး လုပ်ငန်း တွေ နဲ့ ▁တရားရုံး စ တဲ့ ▁ပင်မ အဖွဲ့ အစည်း တွေ သာမက ▁စာပေ ▁ယဉ်ကျေးမှု ▁စိတ်ဓာတ် ပိုင်း က လည်း ▁နိုင်ငံ သိ စိတ် ▁ချစ် စိတ် တွေ ▁ပေါ်လာ အောင် ▁ဆ ော် ဩ ▁ပေး ရ ပါတယ် ။ ▁ဒါ ကို သိ တဲ့ ▁လူကြီး ပိုင်း က ▁မြန်မာပြည် အတွက် ▁ပြတိုက် ▁စာကြည့် တိုက် နဲ့ ▁အနုပညာ တိုက် တွေ ▁ရှိ ဖို့ လို တဲ့ အကြောင်း ▁ကိုလိုနီ ခေတ် က စ ပြီး ▁တိုက်တွန်း ခဲ့ ကြ သလို ▁ဒီ ယဉ်ကျေးမှု ▁အဆ ောက် အ ဦ တွေကို ▁က ွပ် ကဲ ဖို့ ▁အတွက် ▁ ပညာရှင် တွေ ▁ပေါ် ထွက် ဖို့ လည်း ▁ကမ္ဘာ စစ် ▁မဖြစ် ခင် က တည်း က ▁စ ိုင်း ပြင်း ခဲ့ ကြ ပါတယ် ။ ▁ဒါ ကြောင့် ▁ဦး ခင် ဇော် နဲ့ ▁ဦး သိန်း ဟန် ကို ▁ပိ ဋ ကတ် တိုက် ပညာ လို့ ▁ခေါ် တဲ့ ▁စာကြည့် တိုက် လုပ်ငန်း အတွက် ▁ဗြိတိန် ကို ▁စေ လွှတ် ခဲ့ ▁သလို ▁ပန်းချီ ပညာ သင် အ ဖြစ် ▁ဦး ဘ ဉာဏ် နဲ့ ▁ဦး ဘ ဇော် ကို လည်း ▁ဒီ ့ အ ရင် က တည်း က ▁လန်ဒန် ကို ▁ပို့ ခဲ့ပါတယ် ။

▁ဒါပေမဲ့ ▁ကိုလိုနီ ခေတ် မြန် မာ နိုင်ငံ မှာ ▁အဲဒီ အချိန် ထိ ▁အမျိုးသား စာ ကြည့် တိုက် နဲ့ ▁ပြတိုက် ၊ ▁အနုပညာ ပြ ခန်း တွေ ▁မရှိ သေး ဘဲ ▁ရန်ကုန် ▁တက္ကသိုလ် ▁ပိ ဋ ကတ် တိုက် နဲ့ ▁ရန်ကုန် မြို့ ထဲက ▁ဗာ း နတ် ပ ိ ဋ ကတ် တိုက် နဲ့ ▁ပြတိုက် အပြင် ▁ပြည် နား က ▁မှ ော် ဇာ ၊ ▁ရခိုင် က ▁မြောက် ဦး နဲ့ ▁အညာ က ▁ပုဂံ ၊ ▁ရွှေ ဘို နဲ့ ▁မန္တလေး မှာ ▁က မ ္ ပ ည်း ကျောက် စာ ဌာန ▁ပြတိုက် ကလေး တွေ ပဲ ▁ရှိ ခဲ့ပါတယ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-bpe.model --output_format=piece < ./test2.raw
▁နိုင် င ံ တ ခ ု ▁ထ ူ ထ ောင် တ ဲ့ အ ခ ါ မ ှ ာ ▁စစ် တ ပ် ၊ ▁စီး ပ ွ ား ရ ေး လ ုပ် င န်း တ ွေ န ဲ့ ▁တ ရ ား ရ ုံး စ တ ဲ့ ▁ပင် မ အ ဖ ွ ဲ့ အ စ ည်း တ ွေ သ ာ မ က ▁စာ ပ ေ ▁ယ ဉ် က ျ ေး မ ှ ု ▁စိတ် ဓ ာတ် ပ ိုင်း က လ ည်း ▁နိုင် င ံ သ ိ စ ိတ် ▁ချစ် စ ိတ် တ ွေ ▁ပေါ် လ ာ အ ောင် ▁ဆ ော် ဩ ▁ပေး ရ ပ ါ တ ယ် ။ ▁ဒါ က ို သ ိ တ ဲ့ ▁လူ က ြ ီး ပ ိုင်း က ▁မြန် မ ာ ပ ြ ည် အ တ ွက် ▁ပြ တ ိုက် ▁စာ က ြ ည ့် တ ိုက် န ဲ့ ▁အ န ု ပ ည ာ တ ိုက် တ ွေ ▁ရှိ ဖ ို့ လ ို တ ဲ့ အ က ြ ောင်း ▁ကို လ ို န ီ ခ ေ တ် က စ ပ ြ ီး ▁တိုက် တ ွန်း ခ ဲ့ က ြ သ လ ို ▁ဒီ ယ ဉ် က ျ ေး မ ှ ု ▁အ ဆ ောက် အ ဦ တ ွေ က ို ▁ကွ ပ် က ဲ ဖ ို့ ▁အ တ ွက် ▁ပ ည ာ ရ ှ င် တ ွေ ▁ပေါ် ထ ွက် ဖ ို့ လ ည်း ▁ကမ္ဘာ စ စ် ▁မ ဖ ြ စ် ခ င် က တ ည်း က ▁စ ိုင်း ပ ြ င်း ခ ဲ့ က ြ ပ ါ တ ယ် ။ ▁ဒါ က ြ ော င ့် ▁ဦး ခ င် ဇ ော် န ဲ့ ▁ဦး သ ိ န်း ဟ န် က ို ▁ပ ိ ဋ က တ် တ ိုက် ပ ည ာ လ ို့ ▁ခေါ် တ ဲ့ ▁စာ က ြ ည ့် တ ိုက် လ ုပ် င န်း အ တ ွက် ▁ဗ ြ ိ တ ိန် က ို ▁စေ လ ွှ တ် ခ ဲ့ ▁သ လ ို ▁ပန်း ခ ျီ ပ ည ာ သ င် အ ဖ ြ စ် ▁ဦး ဘ ဉ ာ ဏ် န ဲ့ ▁ဦး ဘ ဇ ော် က ို လ ည်း ▁ဒီ ့ အ ရ င် က တ ည်း က ▁လ န် ဒ န် က ို ▁ပို့ ခ ဲ့ ပ ါ တ ယ် ။

▁ဒါ ပ ေ မ ဲ့ ▁ကို လ ို န ီ ခ ေ တ် မ ြ န် မ ာ န ိုင် င ံ မ ှ ာ ▁အဲ ဒ ီ အ ခ ျ ိန် ထ ိ ▁အ မ ျ ိုး သ ား စ ာ က ြ ည ့် တ ိုက် န ဲ့ ▁ပြ တ ိုက် ၊ ▁အ န ု ပ ည ာ ပ ြ ခ န်း တ ွေ ▁မ ရ ှ ိ သ ေး ဘ ဲ ▁ရန် က ု န် ▁တက္က သ ိုလ် ▁ပ ိ ဋ က တ် တ ိုက် န ဲ့ ▁ရန် က ု န် မ ြ ို့ ထ ဲ က ▁ဗ ား န တ် ပ ိ ဋ က တ် တ ိုက် န ဲ့ ▁ပြ တ ိုက် အ ပ ြ င် ▁ပြည် န ား က ▁မှ ော် ဇ ာ ၊ ▁ရ ခ ိုင် က ▁မြောက် ဦ း န ဲ့ ▁အ ည ာ က ▁ပု ဂ ံ ၊ ▁ရွှေ ဘ ို န ဲ့ ▁မ န္တ လ ေး မ ှ ာ ▁က မ္ပ ည်း က ျ ောက် စ ာ ဌ ာ န ▁ပြ တ ိုက် က လ ေး တ ွေ ပ ဲ ▁ရှိ ခ ဲ့ ပ ါ တ ယ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-bpe.model --output_format=piece < ./test2.raw
▁နိုင်ငံ တ ခု ▁ထူထောင် တဲ့ အခါ မှာ ▁စစ်တပ် ၊ ▁စီးပွားရေး လုပ်ငန်း တွေ နဲ့ ▁တရားရုံး စ တဲ့ ▁ပင်မ အဖွဲ့ အစည်း တွေ သာ မက ▁စာပေ ▁ယဉ်ကျေးမှု ▁စိတ်ဓာတ် ပိုင်း က လည်း ▁နိုင်ငံ သိ စိတ် ▁ချစ် စိတ် တွေ ▁ပေါ်လာ အောင် ▁ဆ ော် ဩ ▁ပေးရ ပါတယ် ။ ▁ဒါကို သိ တဲ့ ▁လူကြီး ပိုင်း က ▁မြန်မာပြည် အတွက် ▁ပြတိုက် ▁စာကြည့်တိုက် နဲ့ ▁အနုပညာ တိုက် တွေ ▁ရှိ ဖို့ လို တဲ့ အ ကြောင်း ▁ကိုလိုနီ ခေတ် က စ ပြီး ▁တိုက်တွန်း ခဲ့ ကြ သလို ▁ဒီ ယ ဉ်ကျေး မှု ▁အဆောက်အ ဦ တွေကို ▁က ွပ် ကဲ ဖို့ ▁အတွက် ▁ပညာရှင် တွေ ▁ပေါ် ထွက် ဖို့ လည်း ▁ကမ္ဘာ စစ် ▁မဖြစ် ခင် က တည်းက ▁စ ိုင်း ပြင်း ခဲ့ ကြ ပါတယ် ။ ▁ဒါကြောင့် ▁ဦး ခင် ဇော် နဲ့ ▁ဦး သိန်း ဟန် ကို ▁ပိ ဋ ကတ် တိုက် ပညာ လို့ ▁ခေါ် တဲ့ ▁စာကြည့်တိုက် လုပ်ငန်း အတွက် ▁ဗြိတိန် ကို ▁စေ လွှတ် ခဲ့ ▁သလို ▁ပန်းချီ ပညာ သင် အ ဖြစ် ▁ဦး ဘ ဉာဏ် နဲ့ ▁ဦး ဘ ဇော် ကို လည်း ▁ဒီ ့ အ ရင် က တည်းက ▁လန်ဒန် ကို ▁ပို့ ခဲ့ ပါတယ် ။

▁ဒါပေမဲ့ ▁ကိုလိုနီ ခေတ် မြန် မာ နိုင်ငံ မှာ ▁အဲဒီ အချိန် ထိ ▁အမျိုးသား စာ ကြည့် တိုက် နဲ့ ▁ပြတိုက် ၊ ▁အနုပညာ ပြခန်း တွေ ▁မရှိ သေး ဘဲ ▁ရန်ကုန် ▁တက္ကသိုလ် ▁ပိ ဋ ကတ် တိုက် နဲ့ ▁ရန်ကုန် မြို့ ထဲက ▁ဗ ား နတ် ပိ ဋ ကတ် တိုက် နဲ့ ▁ပြတိုက် အပြင် ▁ပြည် နား က ▁မှ ော် ဇာ ၊ ▁ရခိုင် က ▁မြောက် ဦး နဲ့ ▁အညာ က ▁ပုဂံ ၊ ▁ရွှေ ဘို နဲ့ ▁မန္တလေး မှာ ▁က မ္ ပ ည်း ကျောက် စာ ဌာန ▁ပြတိုက် ကလေး တွေ ပဲ ▁ရှိ ခဲ့ ပါတယ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-char.model --output_format=piece < ./test2.raw
▁ န ိ ု င ် င ံ တ ခ ု ▁ ထ ူ ထ ေ ာ င ် တ ဲ ့ အ ခ ါ မ ှ ာ ▁ စ စ ် တ ပ ် ၊ ▁ စ ီ း ပ ွ ာ း ရ ေ း လ ု ပ ် င န ် း တ ွ ေ န ဲ ့ ▁ တ ရ ာ း ရ ု ံ း စ တ ဲ ့ ▁ ပ င ် မ အ ဖ ွ ဲ ့ အ စ ည ် း တ ွ ေ သ ာ မ က ▁ စ ာ ပ ေ ▁ ယ ဉ ် က ျ ေ း မ ှ ု ▁ စ ိ တ ် ဓ ာ တ ် ပ ိ ု င ် း က လ ည ် း ▁ န ိ ု င ် င ံ သ ိ စ ိ တ ် ▁ ခ ျ စ ် စ ိ တ ် တ ွ ေ ▁ ပ ေ ါ ် လ ာ အ ေ ာ င ် ▁ ဆ ေ ာ ် ဩ ▁ ပ ေ း ရ ပ ါ တ ယ ် ။ ▁ ဒ ါ က ိ ု သ ိ တ ဲ ့ ▁ လ ူ က ြ ီ း ပ ိ ု င ် း က ▁ မ ြ န ် မ ာ ပ ြ ည ် အ တ ွ က ် ▁ ပ ြ တ ိ ု က ် ▁ စ ာ က ြ ည ့ ် တ ိ ု က ် န ဲ ့ ▁ အ န ု ပ ည ာ တ ိ ု က ် တ ွ ေ ▁ ရ ှ ိ ဖ ိ ု ့ လ ိ ု တ ဲ ့ အ က ြ ေ ာ င ် း ▁ က ိ ု လ ိ ု န ီ ခ ေ တ ် က စ ပ ြ ီ း ▁ တ ိ ု က ် တ ွ န ် း ခ ဲ ့ က ြ သ လ ိ ု ▁ ဒ ီ ယ ဉ ် က ျ ေ း မ ှ ု ▁ အ ဆ ေ ာ က ် အ ဦ တ ွ ေ က ိ ု ▁ က ွ ပ ် က ဲ ဖ ိ ု ့ ▁ အ တ ွ က ် ▁ ပ ည ာ ရ ှ င ် တ ွ ေ ▁ ပ ေ ါ ် ထ ွ က ် ဖ ိ ု ့ လ ည ် း ▁ က မ ္ ဘ ာ စ စ ် ▁ မ ဖ ြ စ ် ခ င ် က တ ည ် း က ▁ စ ိ ု င ် း ပ ြ င ် း ခ ဲ ့ က ြ ပ ါ တ ယ ် ။ ▁ ဒ ါ က ြ ေ ာ င ့ ် ▁ ဦ း ခ င ် ဇ ေ ာ ် န ဲ ့ ▁ ဦ း သ ိ န ် း ဟ န ် က ိ ု ▁ ပ ိ ဋ က တ ် တ ိ ု က ် ပ ည ာ လ ိ ု ့ ▁ ခ ေ ါ ် တ ဲ ့ ▁ စ ာ က ြ ည ့ ် တ ိ ု က ် လ ု ပ ် င န ် း အ တ ွ က ် ▁ ဗ ြ ိ တ ိ န ် က ိ ု ▁ စ ေ လ ွ ှ တ ် ခ ဲ ့ ▁ သ လ ိ ု ▁ ပ န ် း ခ ျ ီ ပ ည ာ သ င ် အ ဖ ြ စ ် ▁ ဦ း ဘ ဉ ာ ဏ ် န ဲ ့ ▁ ဦ း ဘ ဇ ေ ာ ် က ိ ု လ ည ် း ▁ ဒ ီ ့ အ ရ င ် က တ ည ် း က ▁ လ န ် ဒ န ် က ိ ု ▁ ပ ိ ု ့ ခ ဲ ့ ပ ါ တ ယ ် ။

▁ ဒ ါ ပ ေ မ ဲ ့ ▁ က ိ ု လ ိ ု န ီ ခ ေ တ ် မ ြ န ် မ ာ န ိ ု င ် င ံ မ ှ ာ ▁ အ ဲ ဒ ီ အ ခ ျ ိ န ် ထ ိ ▁ အ မ ျ ိ ု း သ ာ း စ ာ က ြ ည ့ ် တ ိ ု က ် န ဲ ့ ▁ ပ ြ တ ိ ု က ် ၊ ▁ အ န ု ပ ည ာ ပ ြ ခ န ် း တ ွ ေ ▁ မ ရ ှ ိ သ ေ း ဘ ဲ ▁ ရ န ် က ု န ် ▁ တ က ္ က သ ိ ု လ ် ▁ ပ ိ ဋ က တ ် တ ိ ု က ် န ဲ ့ ▁ ရ န ် က ု န ် မ ြ ိ ု ့ ထ ဲ က ▁ ဗ ာ း န တ ် ပ ိ ဋ က တ ် တ ိ ု က ် န ဲ ့ ▁ ပ ြ တ ိ ု က ် အ ပ ြ င ် ▁ ပ ြ ည ် န ာ း က ▁ မ ှ ေ ာ ် ဇ ာ ၊ ▁ ရ ခ ိ ု င ် က ▁ မ ြ ေ ာ က ် ဦ း န ဲ ့ ▁ အ ည ာ က ▁ ပ ု ဂ ံ ၊ ▁ ရ ွ ှ ေ ဘ ိ ု န ဲ ့ ▁ မ န ္ တ လ ေ း မ ှ ာ ▁ က မ ္ ပ ည ် း က ျ ေ ာ က ် စ ာ ဌ ာ န ▁ ပ ြ တ ိ ု က ် က လ ေ း တ ွ ေ ပ ဲ ▁ ရ ှ ိ ခ ဲ ့ ပ ါ တ ယ ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-char.model --output_format=piece < ./test2.raw
▁ န ိ ု င ် င ံ တ ခ ု ▁ ထ ူ ထ ေ ာ င ် တ ဲ ့ အ ခ ါ မ ှ ာ ▁ စ စ ် တ ပ ် ၊ ▁ စ ီ း ပ ွ ာ း ရ ေ း လ ု ပ ် င န ် း တ ွ ေ န ဲ ့ ▁ တ ရ ာ း ရ ု ံ း စ တ ဲ ့ ▁ ပ င ် မ အ ဖ ွ ဲ ့ အ စ ည ် း တ ွ ေ သ ာ မ က ▁ စ ာ ပ ေ ▁ ယ ဉ ် က ျ ေ း မ ှ ု ▁ စ ိ တ ် ဓ ာ တ ် ပ ိ ု င ် း က လ ည ် း ▁ န ိ ု င ် င ံ သ ိ စ ိ တ ် ▁ ခ ျ စ ် စ ိ တ ် တ ွ ေ ▁ ပ ေ ါ ် လ ာ အ ေ ာ င ် ▁ ဆ ေ ာ ် ဩ ▁ ပ ေ း ရ ပ ါ တ ယ ် ။ ▁ ဒ ါ က ိ ု သ ိ တ ဲ ့ ▁ လ ူ က ြ ီ း ပ ိ ု င ် း က ▁ မ ြ န ် မ ာ ပ ြ ည ် အ တ ွ က ် ▁ ပ ြ တ ိ ု က ် ▁ စ ာ က ြ ည ့ ် တ ိ ု က ် န ဲ ့ ▁ အ န ု ပ ည ာ တ ိ ု က ် တ ွ ေ ▁ ရ ှ ိ ဖ ိ ု ့ လ ိ ု တ ဲ ့ အ က ြ ေ ာ င ် း ▁ က ိ ု လ ိ ု န ီ ခ ေ တ ် က စ ပ ြ ီ း ▁ တ ိ ု က ် တ ွ န ် း ခ ဲ ့ က ြ သ လ ိ ု ▁ ဒ ီ ယ ဉ ် က ျ ေ း မ ှ ု ▁ အ ဆ ေ ာ က ် အ ဦ တ ွ ေ က ိ ု ▁ က ွ ပ ် က ဲ ဖ ိ ု ့ ▁ အ တ ွ က ် ▁ ပ ည ာ ရ ှ င ် တ ွ ေ ▁ ပ ေ ါ ် ထ ွ က ် ဖ ိ ု ့ လ ည ် း ▁ က မ ္ ဘ ာ စ စ ် ▁ မ ဖ ြ စ ် ခ င ် က တ ည ် း က ▁ စ ိ ု င ် း ပ ြ င ် း ခ ဲ ့ က ြ ပ ါ တ ယ ် ။ ▁ ဒ ါ က ြ ေ ာ င ့ ် ▁ ဦ း ခ င ် ဇ ေ ာ ် န ဲ ့ ▁ ဦ း သ ိ န ် း ဟ န ် က ိ ု ▁ ပ ိ ဋ က တ ် တ ိ ု က ် ပ ည ာ လ ိ ု ့ ▁ ခ ေ ါ ် တ ဲ ့ ▁ စ ာ က ြ ည ့ ် တ ိ ု က ် လ ု ပ ် င န ် း အ တ ွ က ် ▁ ဗ ြ ိ တ ိ န ် က ိ ု ▁ စ ေ လ ွ ှ တ ် ခ ဲ ့ ▁ သ လ ိ ု ▁ ပ န ် း ခ ျ ီ ပ ည ာ သ င ် အ ဖ ြ စ ် ▁ ဦ း ဘ ဉ ာ ဏ ် န ဲ ့ ▁ ဦ း ဘ ဇ ေ ာ ် က ိ ု လ ည ် း ▁ ဒ ီ ့ အ ရ င ် က တ ည ် း က ▁ လ န ် ဒ န ် က ိ ု ▁ ပ ိ ု ့ ခ ဲ ့ ပ ါ တ ယ ် ။

▁ ဒ ါ ပ ေ မ ဲ ့ ▁ က ိ ု လ ိ ု န ီ ခ ေ တ ် မ ြ န ် မ ာ န ိ ု င ် င ံ မ ှ ာ ▁ အ ဲ ဒ ီ အ ခ ျ ိ န ် ထ ိ ▁ အ မ ျ ိ ု း သ ာ း စ ာ က ြ ည ့ ် တ ိ ု က ် န ဲ ့ ▁ ပ ြ တ ိ ု က ် ၊ ▁ အ န ု ပ ည ာ ပ ြ ခ န ် း တ ွ ေ ▁ မ ရ ှ ိ သ ေ း ဘ ဲ ▁ ရ န ် က ု န ် ▁ တ က ္ က သ ိ ု လ ် ▁ ပ ိ ဋ က တ ် တ ိ ု က ် န ဲ ့ ▁ ရ န ် က ု န ် မ ြ ိ ု ့ ထ ဲ က ▁ ဗ ာ း န တ ် ပ ိ ဋ က တ ် တ ိ ု က ် န ဲ ့ ▁ ပ ြ တ ိ ု က ် အ ပ ြ င ် ▁ ပ ြ ည ် န ာ း က ▁ မ ှ ေ ာ ် ဇ ာ ၊ ▁ ရ ခ ိ ု င ် က ▁ မ ြ ေ ာ က ် ဦ း န ဲ ့ ▁ အ ည ာ က ▁ ပ ု ဂ ံ ၊ ▁ ရ ွ ှ ေ ဘ ိ ု န ဲ ့ ▁ မ န ္ တ လ ေ း မ ှ ာ ▁ က မ ္ ပ ည ် း က ျ ေ ာ က ် စ ာ ဌ ာ န ▁ ပ ြ တ ိ ု က ် က လ ေ း တ ွ ေ ပ ဲ ▁ ရ ှ ိ ခ ဲ ့ ပ ါ တ ယ ် ။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=syl-word.model --output_format=piece < ./test2.raw
▁နိုင်ငံတခု▁ထူထောင်တဲ့အခါမှာ▁စစ်တပ်၊▁စီးပွားရေးလုပ်ငန်းတွေနဲ့▁တရားရုံးစတဲ့▁ပင်မအဖွဲ့အစည်းတွေသာမက▁စာပေ▁ယဉ်ကျေးမှု▁စိတ်ဓာတ်ပိုင်းကလည်း▁နိုင်ငံသိစိတ်▁ချစ်စိတ်တွေ▁ပေါ်လာအောင်▁ဆော်ဩ▁ပေးရပါတယ်။▁ဒါကိုသိတဲ့▁လူကြီးပိုင်းက▁မြန်မာပြည်အတွက်▁ပြတိုက်▁စာကြည့်တိုက်နဲ့▁အနုပညာတိုက်တွေ▁ရှိဖို့လိုတဲ့အကြောင်း▁ကိုလိုနီခေတ်ကစပြီး▁တိုက်တွန်းခဲ့ကြသလို▁ဒီယဉ်ကျေးမှု▁အဆောက်အဦတွေကို▁ကွပ်ကဲဖို့▁အတွက်▁ပညာရှင်တွေ▁ပေါ်ထွက်ဖို့လည်း▁ကမ္ဘာစစ်▁မဖြစ်ခင်ကတည်းက▁စိုင်းပြင်းခဲ့ကြပါတယ်။▁ဒါကြောင့်▁ဦးခင်ဇော်နဲ့▁ဦးသိန်းဟန်ကို▁ပိဋကတ်တိုက်ပညာလို့▁ခေါ်တဲ့▁စာကြည့်တိုက်လုပ်ငန်းအတွက်▁ဗြိတိန်ကို▁စေလွှတ်ခဲ့▁သလို▁ပန်းချီပညာသင်အဖြစ်▁ဦးဘဉာဏ်နဲ့▁ဦးဘဇော်ကိုလည်း▁ဒီ့အရင်ကတည်းက▁လန်ဒန်ကို▁ပို့ခဲ့ပါတယ်။

▁ဒါပေမဲ့▁ကိုလိုနီခေတ်မြန်မာနိုင်ငံမှာ▁အဲဒီအချိန်ထိ▁အမျိုးသားစာကြည့်တိုက်နဲ့▁ပြတိုက်၊▁အနုပညာပြခန်းတွေ▁မရှိသေးဘဲ▁ရန်ကုန်▁တက္ကသိုလ်▁ပိဋကတ်တိုက်နဲ့▁ရန်ကုန်မြို့ထဲက▁ဗားနတ်ပိဋကတ်တိုက်နဲ့▁ပြတိုက်အပြင်▁ပြည်နားက▁မှော်ဇာ၊▁ရခိုင်က▁မြောက်ဦးနဲ့▁အညာက▁ပုဂံ၊▁ရွှေဘိုနဲ့▁မန္တလေးမှာ▁ကမ္ပည်းကျောက်စာဌာန▁ပြတိုက်ကလေးတွေပဲ▁ရှိခဲ့ပါတယ်။
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-word.model --output_format=piece < ./test2.raw
▁နိုင်ငံတခု▁ထူထောင်တဲ့အခါမှာ▁စစ်တပ်၊▁စီးပွားရေးလုပ်ငန်းတွေနဲ့▁တရားရုံးစတဲ့▁ပင်မအဖွဲ့အစည်းတွေသာမက ▁စာပေ ▁ယဉ်ကျေးမှု ▁စိတ်ဓာတ်ပိုင်းကလည်း▁နိုင်ငံသိစိတ်▁ချစ်စိတ်တွေ▁ပေါ်လာအောင်▁ဆော်ဩ▁ပေးရပါတယ်။▁ဒါကိုသိတဲ့▁လူကြီးပိုင်းက▁မြန်မာပြည်အတွက် ▁ပြတိုက် ▁စာကြည့်တိုက်နဲ့▁အနုပညာတိုက်တွေ▁ရှိဖို့လိုတဲ့အကြောင်း▁ကိုလိုနီခေတ်ကစပြီး▁တိုက်တွန်းခဲ့ကြသလို▁ဒီယဉ်ကျေးမှု▁အဆောက်အဦတွေကို▁ကွပ်ကဲဖို့ ▁အတွက် ▁ပညာရှင်တွေ▁ပေါ်ထွက်ဖို့လည်း▁ကမ္ဘာစစ်▁မဖြစ်ခင်ကတည်းက▁စိုင်းပြင်းခဲ့ကြပါတယ်။ ▁ဒါကြောင့် ▁ဦးခင်ဇော်နဲ့▁ဦးသိန်းဟန်ကို▁ပိဋကတ်တိုက်ပညာလို့▁ခေါ်တဲ့▁စာကြည့်တိုက်လုပ်ငန်းအတွက်▁ဗြိတိန်ကို▁စေလွှတ်ခဲ့ ▁သလို ▁ပန်းချီပညာသင်အဖြစ်▁ဦးဘဉာဏ်နဲ့▁ဦးဘဇော်ကိုလည်း▁ဒီ့အရင်ကတည်းက▁လန်ဒန်ကို▁ပို့ခဲ့ပါတယ်။

▁ဒါပေမဲ့ ▁ကိုလိုနီခေတ်မြန်မာနိုင်ငံမှာ▁အဲဒီအချိန်ထိ▁အမျိုးသားစာကြည့်တိုက်နဲ့▁ပြတိုက်၊▁အနုပညာပြခန်းတွေ▁မရှိသေးဘဲ ▁ရန်ကုန် ▁တက္ကသိုလ် ▁ပိဋကတ်တိုက်နဲ့▁ရန်ကုန်မြို့ထဲက▁ဗားနတ်ပိဋကတ်တိုက်နဲ့▁ပြတိုက်အပြင်▁ပြည်နားက▁မှော်ဇာ၊▁ရခိုင်က▁မြောက်ဦးနဲ့▁အညာက▁ပုဂံ၊▁ရွှေဘိုနဲ့▁မန္တလေးမှာ▁ကမ္ပည်းကျောက်စာဌာန▁ပြတိုက်ကလေးတွေပဲ▁ရှိခဲ့ပါတယ်။
```

## Testing --extra_options

--extra_options=eos နဲ့ spm_encode ကို run ရင် sentence အဆုံး သင်္ကေတကို စာကြောင်းအဆုံးမှာ ဖြည့်ပေးပါမှာ ဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-word.model --extra_options=eos --output_format=piece < ./test1.txt
▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ </s>
▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ </s>
▁အ ▁ရမ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ် </s>
▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁ကျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။ </s>
▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိလပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁မှူး ▁ချုပ် </s>
```

--extra_options=bos:eos နဲ့ run ရင်တော့ စာကြောင်းအစ၊ စာကြောင်းအဆုံး သင်္ကေတာ ၂ခုစလုံ။ကို စာကြောင်းတိုင်းမှာ ရိုက်ပေးမှာ ဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-word.model --extra_options=bos:eos --output_format=piece < ./test1.txt
<s> ▁မင်း ▁ကို ▁ငါ ▁ဘယ်လို ▁ခေါ် ▁ရ ▁မ ▁လဲ </s>
<s> ▁စာ ▁တော် ▁တဲ့ ▁ကျောင်း ▁သူ ▁တစ် ▁ယောက် ▁ပါ </s>
<s> ▁အ ▁ရမ်း ▁ဆော့ ▁တဲ့ ▁ကလေး ▁က ▁ကျန်း ▁မာ ▁တယ် </s>
<s> ▁အခု ▁တော့ ▁ပါ ▁နက် ▁ဆ ▁ရာ ▁ဟာ ▁စက် ▁တင် ▁ဘာ ▁လ ▁၁၉ ▁ရက် ▁နေ့ ▁မှာ ▁ဆန္ဒ ▁ပြ ▁ပွဲ ▁ကျင်း ▁ပ ▁ဖို့ ▁အ ▁တွက် ▁ပြင် ▁ဆင် ▁နေ ▁ပါ ▁တယ် ▁။ </s>
<s> ▁ဘတ်စ် ▁ကား ▁စီး ▁ပြီး ▁ရုံး ▁တက် ▁တဲ့ ▁ဘိလပ် ▁ပြန် ▁ညွှန် ▁ကြား ▁ရေး ▁မှူး ▁ချုပ် </s>
```

--extra_options=reverse:bos:eos နဲ့ run ရင်တော့ အောက်ပါအတိုင်း စာကြောင်းကို ပြောင်းပြန် ရိုက်ထုတ်ပေးမှာ ဖြစ်ပါတယ်။  
ပြောင်းပြန်က လူတွေအတွက် ဖတ်ရပြုရတာ အဆင်မပြေပေမဲ့ Neural Network မော်ဒယ်အတွက်က စာကြောင်းကို ပြန်ပြန်လုပ်ပြီး မော်ဒယ်ဆောက်တာက performance ကောင်းချင်လည်း ကောင်းတတ်လို့ပါ။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_encode --model=word-word.model --extra_options=reverse:bos:eos --output_format=piece < ./test1.txt
<s> ▁လဲ ▁မ ▁ရ ▁ခေါ် ▁ဘယ်လို ▁ငါ ▁ကို ▁မင်း </s>
<s> ▁ပါ ▁ယောက် ▁တစ် ▁သူ ▁ကျောင်း ▁တဲ့ ▁တော် ▁စာ </s>
<s> ▁တယ် ▁မာ ▁ကျန်း ▁က ▁ကလေး ▁တဲ့ ▁ဆော့ ▁ရမ်း ▁အ </s>
<s> ▁။ ▁တယ် ▁ပါ ▁နေ ▁ဆင် ▁ပြင် ▁တွက် ▁အ ▁ဖို့ ▁ပ ▁ကျင်း ▁ပွဲ ▁ပြ ▁ဆန္ဒ ▁မှာ ▁နေ့ ▁ရက် ▁၁၉ ▁လ ▁ဘာ ▁တင် ▁စက် ▁ဟာ ▁ရာ ▁ဆ ▁နက် ▁ပါ ▁တော့ ▁အခု </s>
<s> ▁ချုပ် ▁မှူး ▁ရေး ▁ကြား ▁ညွှန် ▁ပြန် ▁ဘိလပ် ▁တဲ့ ▁တက် ▁ရုံး ▁ပြီး ▁စီး ▁ကား ▁ဘတ်စ် </s>
```

## Extracting Vocab List

ဆောက်ထားတဲ့ မော်ဒယ်ကနေ vocab list ကိုလည်း ဆွဲထုပ်လို့ ရပါတယ်။  
command option ရဲ့ syntax ကတော့ အောက်ပါအတိုင်းပါ။  

spm_export_vocab --model=<model_file> --output=<output file>  

### Extracting Vocab List from syl-word.model
ပထမဆုံး syl-word.model ဖိုင်ထဲကနေ vocab list ကို ဆွဲထုတ်ကြည့်ကြရအောင် ...   

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_export_vocab --model=syl-word.model --output=syl-word.vocab
```

မော်ဒယ်ဆောကစဉ်မှာ ပေးခဲ့တဲ့ vocab size အတိုင်း စာလုံးရေအရေအတွက်က ရှိမှာ ဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ wc ./syl-word.vocab 
 1000  2000 23089 ./syl-word.vocab
```

vocab ဖိုင်ရဲ့ ထိပ်ပိုင်းကို head command နဲ့ ခေါ်ကြည့်ရင် အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ head ./syl-word.vocab 
<unk>	0
<s>	0
</s>	0
▁။	-2.646
▁အ	-3.38824
▁တယ်	-3.65992
▁ပါ	-3.7384
▁မ	-3.79826
▁က	-3.9237
▁ကို	-3.98853
```

tail နဲ့ syl-word.vocab ဖိုင်ရဲ့ နောက်ဆုံး ၁၀ကြောင်းကို ကြည့်ကြည့်ရအောင်  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ tail ./syl-word.vocab 
▁ဂတ်	-9.92285
▁တိမ်	-9.92285
▁ဓါး	-9.92285
▁သင်္ကြန်	-9.92285
▁2	-9.93745
▁လူး	-9.93745
▁ခေါင်	-9.95227
▁မြက်	-9.95227
▁ရှိုး	-9.95227
▁ရှူး	-9.95227

```

### Extracting Vocab List from syl-char.model

character segmentation နဲ့ ဆောက်ထားတဲ့ မော်ဒယ်ကနေလည်း vocab list ကို ဆွဲကြည့်ရအောင်   

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_export_vocab --model=syl-char.model --output=char-word.vocab
```

character မော်ဒယ်ရဲ့ vocab ဖိုင်မှာတော့ အရေအတွက်က နည်းမှာ ဖြစ်ပါတယ်။ စုစုပေါင်း 245 လုံးပဲ ရှိတာကို တွေ့ရပါတယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ wc ./char-word.vocab 
 245  490 2957 ./char-word.vocab
```

head လုပ်ကြည့်ရအောင်   

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ head ./char-word.vocab 
<unk>	0
<s>	0
</s>	0
▁	-1.32184
	-2.49005
ာ	-3.09707
း	-3.17944
က	-3.29593
တ	-3.35336
ေ	-3.39885
```

ကိုယ်သုံးထားတဲ့ training ဖိုင်အပေါ်ကို မူတည်ပြီး မြန်မာစာလုံး မဟုတ်တဲ့ စာလုံးတွေလည်း vocab ဖိုင်ထဲမှာ ရှိနေနိုင်တယ်ဆိုတာကို သဘောပေါက်ပါ။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ tail ./char-word.vocab 
说	-15.4788
道	-15.4788
配	-15.4788
随	-15.4788
音	-15.4788
频	-15.4788
餐	-15.4788
麦	-15.4788
龙	-15.4788
😉	-15.4788

```

### Extracting Vocab List from word-word.model


ဒီတစ်ခါတော့ word-word.model ကထဲကနေ spm_export_vocab command နဲ့ vocab list ကို ဆွဲထုတ်ကြည့်မယ်။  

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ spm_export_vocab --model=word-word.model --output=word-word.vocab
```

မော်ဒယ်ဆောက်စဉ်မှာ ပေးခဲ့တဲ့ setting အတိုင်း vocab ကတော့ စုစုပေါင်း 8000 ရှိပါလိမ့်မယ်။
```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ wc ./word-word.vocab 
  8000  16000 280232 ./word-word.vocab
```
  
vocab ဖိုင်ကို shuffle လုပ်ပြီး စာလုံး ၃၀ ကို list လုပ်ကြည့်ကြရအောင်    

```
(base) ye@ykt-pro:~/tool/sentencepiece/y-test$ shuf ./word-word.vocab | head -30
▁တစ်ဦးတည်းသော	-12.3683
▁ညီမဟာ	-12.1451
▁မီးခိုး	-11.5573
▁ကိုယ့်ကိုယ်ကို	-12.3683
▁။”	-11.9628
▁စာရွက်စာတမ်း	-10.982
▁ပွင့်ပွင့်လင်းလင်း	-11.8087
▁စတင်မှု	-12.1451
▁တော့ပါဘူး	-11.2697
▁ဖခင်	-10.171
▁အရင်းအနှီး	-11.3567
▁ပဉ္စမ	-11.5573
▁ငါ့	-5.72807
▁ခွဲစိတ်ခန်း	-12.1451
▁ကြည့်ခဲ့တယ်	-12.1451
▁အကြောင်းအရင်း	-11.6751
▁အိတ်	-7.98001
▁ကော်လံ	-12.1451
▁ဘဲဥ	-11.9628
▁ပုံပဲ	-11.8087
▁စိန်	-10.9214
▁ဘယ့်နှယ်	-12.1451
▁လူသတ်မှု	-12.1451
▁ပြုပြင်ပြောင်းလဲရေး	-12.1451
▁ရောက်ပြီး	-12.1451
▁ဂရုစိုက်	-8.96707
▁အရေးတကြီး	-11.9628
▁မိမိ	-9.58018
▁ဆန္ဒရှိ	-10.6191
▁လူတန်းစား	-10.8642
```

## Suggestion for You

unigram, bpe, char, word စတဲ့ မော်ဒယ် ၄ခုထဲကမှ ဘယ်မော်ဒယ်က အကောင်းဆုံး ရလဒ်ကို ကိုယ့်ဆောက်ထားတဲ့ မော်ဒယ်က ပေးမှာလဲ ဆိုတဲ့ အချက်ကတော့ အတိအကျပြောဖို့ ခက်ပါတယ်။ ဘာကြောင့်လဲ ဆိုတော့ ဘယ်လို ဒိုမိန်း၊ ဘယ်လိုဒေတာကို သုံးမှာလဲ၊ ပြီးတော့ ဘယ်လောက် ပမာဏ (data size) ကို သုံးမှာလဲ၊ ဘယ်လို Neural network architecture ကို သုံးမှာလဲ ... ပြီးတော့ ဘယ်လို application မျိုးအတွက် ရည်ရွယ်တဲ့ မော်ဒယ်ကို ဆောက်မှာလဲ ဆိုတဲ့ အချက်တွေ အများကြီးအပေါ်မှာတော့ မူတည်ပါလိမ့်မယ်။ ကျွန်တော်တို့မြန်မာစာလို under-resourced langauge တွေအတွက်ကတော့ အကြံပေးရရင်၊ မော်ဒယ်ဆောက်ကြည့် evaluation လုပ်ကြည့်ပြီး confirmation လုပ်တဲ့နည်းကတော့ အသင့်တော်ဆုံးလို့ပဲ ပြောရမှာပါပဲ။ သီအိုရီလို့ ပြောရမလား လက်ရှိအချိန်အထိတော့ ကျွန်တော်လုပ်ခဲ့တဲ့ experiment တွေကနေပြောနိုင်တာကတော့ မြန်မာစာလို ဒေတာနည်းတဲ့ machine translation အတွက်ကတော့ sub-word unit တွေက ရလဒ်ကောင်းကောင်းပေးတာကို တွေ့ရပါတယ်။ syllable unit, bpe unit တို့ပါ။ မမေ့ပါနဲ့နော် မတူတဲ့ segmentation unit တွေနဲ့ ဆောက်ထားတဲ့ မော်ဒယ်တွေကို နှိုင်းယှဉ်တဲ့ အခါမှာ evaluation မလုပ်ခင်မှာ reference/hypothessis ဒေတာတွေကိုတော့ segmentation unite တစ်ခုပေါ်မှာ ညှိပြီးတော့ လုပ်မှသာ equal comparison ဖြစ်လိမ့်မယ် ဆိုတဲ့ အချက်ကို။  


# Reference Papers

Subword Regularization: Improving Neural Network Translation Models with Multiple Subword Candidates:  
[https://arxiv.org/pdf/1804.10959.pdf](https://arxiv.org/pdf/1804.10959.pdf)  

Neural Machine Translation of Rare Words with Subword Units:  
[https://www.aclweb.org/anthology/P16-1162.pdf](https://www.aclweb.org/anthology/P16-1162.pdf)  

# Github Source

Sentencepiece ရဲ့ source code ရှိတဲ့ GitHub Link:  
[https://github.com/google/sentencepiece](https://github.com/google/sentencepiece)  
