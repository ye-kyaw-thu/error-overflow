## Kytea Installation Make Error Note

KyTea ကို ဂျပန်အစိုးရသုတေသနဌာန NICT, Kyoto မှာ researcher အဖြစ် ၄နှစ်ကြာ အလုပ်လုပ်ခဲ့စဉ်က ဂျပန်စာအတွက်ကော၊ မြန်မစာအတွက်ကော၊ ကမ္ဘောဒီးယားစာအတွက်ကော tagging model တွေဆောက်ဖို့အတွက် အကြိမ်ကြိမ်အခါခါ သုံးခဲ့ပါတယ်။ အခုနောက်ပိုင်း Linux distribution မှာ Kytea ကို အဆင်ပြေပြေနဲ့ installation လုပ်လို့ မရတဲ့ ပြဿနာတက်နေတယ်။ အဲဒီအတွက် မှတ်ထားတဲ့ installation note ပါ။ ဒီနေ့အထိတော့ နောက်ပိုင်း စက်တွေမှာ installation လုပ်တဲ့ အခါမှာ make မှာ ရပ်နေတဲ့ အခြေအနေပါ။ ရှင်းရအုံးမယ် ...
```
(base) ye@ykt-pro:~/tool$ git clone https://github.com/neubig/kytea
Cloning into 'kytea'...
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1240 (delta 0), reused 0 (delta 0), pack-reused 1239
Receiving objects: 100% (1240/1240), 38.56 MiB | 494.00 KiB/s, done.
Resolving deltas: 100% (746/746), done.
```

```
(base) ye@ykt-pro:~/tool/kytea$ ls
appveyor.yml  build-win  configure.ac  data     kytea.pc.in  NEWS       src
AUTHORS       ChangeLog  COPYING       INSTALL  Makefile.am  README.md  tools
(base) ye@ykt-pro:~/tool/kytea$ make
make: *** No targets specified and no makefile found.  Stop.
(base) ye@ykt-pro:~/tool/kytea$ autoreconf -i
main::scan_file() called too early to check prototype at /usr/local/bin/aclocal line 618.
configure.ac:9: warning: macro `AM_PROG_AR' not found in library
configure.ac:9: error: possibly undefined macro: AM_PROG_AR
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
configure.ac:28: error: possibly undefined macro: AC_PROG_LIBTOOL
autoreconf: /usr/bin/autoconf failed with exit status: 1
```


## Try again

```
(base) ye@ykt-pro:~/tool/kytea$ autoreconf -i
main::scan_file() called too early to check prototype at /usr/local/bin/aclocal line 618.
configure.ac:29: error: possibly undefined macro: AC_PROG_LIBTOOL
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
autoreconf: /usr/bin/autoconf failed with exit status: 1
```

## Try again with several KyTea versions 

edit configure.ac  

```
(base) ye@ykt-pro:~/tool/kytea$ gedit configure.ac 
```

```
#AC_PROG_LIBTOOL
AC_PROG_LIBTOOL([m4])
```

./configure CFLAGS="-O3" CXXFLAGS="-O3"  
LANG=C make -j $(grep -c ^processor /proc/cpuinfo)  

make error on kytea-0.4.3  


```
mv -f .deps/run-kytea.Tpo .deps/run-kytea.Po
/bin/sh ../../libtool  --tag=CXX   --mode=link /usr/local/bin/ccache-gxx  -O3   -o kytea run-kytea.o  ../lib/libkytea.la 
mv -f .deps/train-kytea.Tpo .deps/train-kytea.Po
/bin/sh ../../libtool  --tag=CXX   --mode=link /usr/local/bin/ccache-gxx  -O3   -o train-kytea train-kytea.o  ../lib/libkytea.la 
libtool: link: /usr/local/bin/ccache-gxx -O3 -o .libs/kytea run-kytea.o  ../lib/.libs/libkytea.so
libtool: link: /usr/local/bin/ccache-gxx -O3 -o .libs/train-kytea train-kytea.o  ../lib/.libs/libkytea.so
..../lib//.liblibs//.libkytea.solibs:/ libkytea.soundefined:  referenceundefined  toreference  `tovoid  `kyteavoid: :kyteacheckValueVecEqual:<:intcheckValueVecEqual><(intstd>:(:stdvector:<:intvector,< std::allocator<int> > const&,int ,std::vector< intstd,: std::allocator<:allocator<int> > const&, std::vector<int, intstd:>: allocator>< intconst>& )>' 
const.&.)/'lib
/...libs//liblibkytea.so/:. libsundefined/ libkytea.soreference:  toundefined  `referencevoid  tokytea :`:voidcheckValueVecEqual <kyteaunsigned: :intcheckValueVecEqual><(unsignedstd :int:>vector(<stdunsigned: :intvector,< unsignedstd :int:,allocator <stdunsigned: :intallocator>< unsigned>  intconst>& ,>  stdconst:&:,vector <stdunsigned: :intvector,< unsignedstd :int:,allocator <stdunsigned: :intallocator>< unsigned>  intconst>& )>' 
const.&.)/'lib
/...libs//liblibkytea.so/:. libsundefined reference to/ `void kytea::libkytea.socheckValueVecEqual:< shortundefined> (referencestd :to: vector`<voidshort ,kytea :std::checkValueVecEqual:<allocatorshort<>short(>std :>: vectorconst<&short,,  stdstd::::vectorallocator<<shortshort,>  std>: :constallocator&<,short >std :>: vectorconst<&short),' 
std::allocator<short> > const&)'
collect2: error: ld returned 1 exit status
collect2: error: ld returned 1 exit status
Makefile:388: recipe for target 'train-kytea' failed
make[2]: *** [train-kytea] Error 1
make[2]: *** Waiting for unfinished jobs....
Makefile:384: recipe for target 'kytea' failed
make[2]: *** [kytea] Error 1eaString const&, int, kytea::KyteaString const*, int)'
test-kytea.cpp:(.text._ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv[_ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv]+0x1b8): undefined reference to `void kytea::Kytea::addTag<kytea::ModelTagEntry>(kytea::Dictionary<kytea::ModelTagEntry>::WordMap&, kytea::KyteaString const&, int, kytea::KyteaString const*, int)'
test-kytea.o:test-kytea.cpp:(.text._ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv[_ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv]+0x20e): more undefined references to `void kytea::Kytea::addTag<kytea::ModelTagEntry>(kytea::Dictionary<kytea::ModelTagEntry>::WordMap&, kytea::KyteaString const&, int, kytea::KyteaString const*, int)' follow
collect2: error: ld returned 1 exit status
Makefile:254: recipe for target 'test-kytea' failed
make[2]: *** [test-kytea] Error 1
make[2]: Leaving directory '/home/ye/tool/kytea-0.4.3/src/test'
Makefile:255: recipe for target 'all-recursive' failed
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory '/home/ye/tool/kytea-0.4.3/src'
Makefile:344: recipe for target 'all-recursive' failed
make: *** [all-recursive] Error 1
(base) ye@ykt-pro:~/tool/kytea-0.4.3$ 
```

make error on kytea-0.4.0  

```
test-kytea.o:test-kytea.cpp:(.text._ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv[_ZN5kytea9KyteaTest27testFeatureLookupDictionaryEv]+0x20e): more undefined references to `void kytea::Kytea::addTag<kytea::ModelTagEntry>(kytea::Dictionary<kytea::ModelTagEntry>::WordMap&, kytea::KyteaString const&, int, kytea::KyteaString const*, int)' follow
collect2: error: ld returned 1 exit status
Makefile:283: recipe for target 'test-kytea' failed
make[2]: *** [test-kytea] Error 1
make[2]: Leaving directory '/home/ye/tool/kytea-0.4.0/src/test'
Makefile:253: recipe for target 'all-recursive' failed
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory '/home/ye/tool/kytea-0.4.0/src'
Makefile:342: recipe for target 'all-recursive' failed
make: *** [all-recursive] Error 1
(base) ye@ykt-pro:~/tool/kytea-0.4.0$ 
```

make error on kytea-0.4.7  
```
make[2]: Leaving directory '/home/ye/tool/kytea-0.4.7/src/bin'
Makefile:341: recipe for target 'all-recursive' failed
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory '/home/ye/tool/kytea-0.4.7/src'
Makefile:442: recipe for target 'all-recursive' failed
make: *** [all-recursive] Error 1
(base) ye@ykt-pro:~/tool/kytea-0.4.7$
```

## Reference  
[https://qiita.com/SUZUKI_Masaya/items/bd03f39e20a1a8f7f4f6#%E5%BF%85%E8%A6%81%E3%81%AA%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB](https://qiita.com/SUZUKI_Masaya/items/bd03f39e20a1a8f7f4f6#%E5%BF%85%E8%A6%81%E3%81%AA%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)  
