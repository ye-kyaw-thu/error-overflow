# How to install SWATH Thai Word Segmenter

Note: Before you install SWATH, you should install the dependency library named "Double-Array Trie".  
Link for downloading libdatrie-0.2.11:   
https://linux.thai.net/~thep/datrie/datrie.html

Installation note of datrie:  
[https://github.com/ye-kyaw-thu/error-overflow/blob/master/lib-install-libdtrie.0.2.11.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/lib-install-libdtrie.0.2.11.md)  

## clone the source code from github

```
(base) ye@ykt-pro:~/tool$ git clone https://github.com/tlwg/swath
Cloning into 'swath'...
remote: Enumerating objects: 2182, done.
remote: Total 2182 (delta 0), reused 0 (delta 0), pack-reused 2182
Receiving objects: 100% (2182/2182), 1.39 MiB | 399.00 KiB/s, done.
Resolving deltas: 100% (1612/1612), done.
(base) ye@ykt-pro:~/tool$ cd swath
(base) ye@ykt-pro:~/tool/swath$ ls
AUTHORS  autogen.sh  build-aux  ChangeLog  configure.ac  conv  COPYING  data  INSTALL  Makefile.am  NEWS  README  src  tests
```

## run autogen.sh

```
(base) ye@ykt-pro:~/tool/swath$ ./autogen.sh 
+ DIE=0
+ libtoolize --version
+ LIBTOOLIZE=libtoolize
+ [ 0 -eq 1 ]
+ libtoolize --force
libtoolize: putting auxiliary files in '.'.
libtoolize: linking file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: linking file 'm4/libtool.m4'
libtoolize: linking file 'm4/ltoptions.m4'
libtoolize: linking file 'm4/ltsugar.m4'
libtoolize: linking file 'm4/ltversion.m4'
libtoolize: linking file 'm4/lt~obsolete.m4'
+ aclocal
+ automake --add-missing
configure.ac:18: installing './compile'
configure.ac:11: installing './missing'
conv/Makefile.am: installing './depcomp'
+ autoconf -f
(base) ye@ykt-pro:~/tool/swath$ ls
aclocal.m4  autom4te.cache  compile       config.sub    conv     depcomp     ltmain.sh    Makefile.in  README       tests
AUTHORS     build-aux       config.guess  configure     COPYING  INSTALL     m4           missing      src
autogen.sh  ChangeLog       config.log    configure.ac  data     install-sh  Makefile.am  NEWS         test-driver
```

## run autoreconf -i
```
(base) ye@ykt-pro:~/tool/swath$ autoreconf -i
(base) ye@ykt-pro:~/tool/swath$ ls
aclocal.m4  autom4te.cache  compile       config.sub    conv     depcomp     ltmain.sh    Makefile.in  README       tests
AUTHORS     build-aux       config.guess  configure     COPYING  INSTALL     m4           missing      src
autogen.sh  ChangeLog       config.log    configure.ac  data     install-sh  Makefile.am  NEWS         test-driver
(base) ye@ykt-pro:~/tool/swath$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking for g++... g++
checking whether the C++ compiler works... yes
checking for C++ compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking for style of include used by make... GNU
checking dependency style of g++... gcc3
checking whether ln -s works... yes
checking whether make sets $(MAKE)... (cached) yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking how to print strings... printf
checking for gcc... gcc
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking for a sed that does not truncate output... /bin/sed
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for fgrep... /bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for ar... ar
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
checking for sysroot... no
checking for a working dd... /bin/dd
checking how to truncate binary pipes... /bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking how to run the C preprocessor... gcc -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking for dlfcn.h... yes
checking for objdir... .libs
checking if gcc supports -fno-rtti -fno-exceptions... no
checking for gcc option to produce PIC... -fPIC -DPIC
checking if gcc PIC flag -fPIC -DPIC works... yes
checking if gcc static flag -static works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.o... (cached) yes
checking whether the gcc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... yes
checking how to run the C++ preprocessor... g++ -E
checking for ld used by g++... /usr/bin/ld -m elf_x86_64
checking if the linker (/usr/bin/ld -m elf_x86_64) is GNU ld... yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking for g++ option to produce PIC... -fPIC -DPIC
checking if g++ PIC flag -fPIC -DPIC works... yes
checking if g++ static flag -static works... yes
checking if g++ supports -c -o file.o... yes
checking if g++ supports -c -o file.o... (cached) yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking dynamic linker characteristics... (cached) GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for DATRIE... yes
checking for ANSI C header files... (cached) yes
checking limits.h usability... yes
checking limits.h presence... yes
checking for limits.h... yes
checking for an ANSI C-conforming const... yes
checking for size_t... yes
checking for trietool-0.2... trietool-0.2
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating conv/Makefile
config.status: creating src/Makefile
config.status: creating data/Makefile
config.status: creating tests/Makefile
config.status: executing depfiles commands
config.status: executing libtool commands
```

## Check files 

```
(base) ye@ykt-pro:~/tool/swath$ ls
aclocal.m4      build-aux     config.log     configure.ac  depcomp     ltmain.sh    Makefile.in  src
AUTHORS         ChangeLog     config.status  conv          INSTALL     m4           missing      test-driver
autogen.sh      compile       config.sub     COPYING       install-sh  Makefile     NEWS         tests
autom4te.cache  config.guess  configure      data          libtool     Makefile.am  README
(base) ye@ykt-pro:~/tool/swath$ 
```

**If you got Makefile ... It looks OK ...

## run make

```
(base) ye@ykt-pro:~/tool/swath$ make
Making all in conv
make[1]: Entering directory '/home/ye/tool/swath/conv'
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" -DPACKAGE_STRING=\"swath\ 0.6.1-6-g4061d86\" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I.   -DNDEBUG  -g -O2 -MT conv.lo -MD -MP -MF .deps/conv.Tpo -c -o conv.lo conv.cxx
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT conv.lo -MD -MP -MF .deps/conv.Tpo -c conv.cxx  -fPIC -DPIC -o .libs/conv.o
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT conv.lo -MD -MP -MF .deps/conv.Tpo -c conv.cxx -o conv.o >/dev/null 2>&1
mv -f .deps/conv.Tpo .deps/conv.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" -DPACKAGE_STRING=\"swath\ 0.6.1-6-g4061d86\" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I.   -DNDEBUG  -g -O2 -MT convfact.lo -MD -MP -MF .deps/convfact.Tpo -c -o convfact.lo convfact.cxx
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT convfact.lo -MD -MP -MF .deps/convfact.Tpo -c convfact.cxx  -fPIC -DPIC -o .libs/convfact.o
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT convfact.lo -MD -MP -MF .deps/convfact.Tpo -c convfact.cxx -o convfact.o >/dev/null 2>&1
mv -f .deps/convfact.Tpo .deps/convfact.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" -DPACKAGE_STRING=\"swath\ 0.6.1-6-g4061d86\" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I.   -DNDEBUG  -g -O2 -MT tis620.lo -MD -MP -MF .deps/tis620.Tpo -c -o tis620.lo tis620.cxx
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT tis620.lo -MD -MP -MF .deps/tis620.Tpo -c tis620.cxx  -fPIC -DPIC -o .libs/tis620.o
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT tis620.lo -MD -MP -MF .deps/tis620.Tpo -c tis620.cxx -o tis620.o >/dev/null 2>&1
mv -f .deps/tis620.Tpo .deps/tis620.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" -DPACKAGE_STRING=\"swath\ 0.6.1-6-g4061d86\" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I.   -DNDEBUG  -g -O2 -MT utf8.lo -MD -MP -MF .deps/utf8.Tpo -c -o utf8.lo utf8.cxx
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT utf8.lo -MD -MP -MF .deps/utf8.Tpo -c utf8.cxx  -fPIC -DPIC -o .libs/utf8.o
libtool: compile:  g++ -DPACKAGE_NAME=\"swath\" -DPACKAGE_TARNAME=\"swath\" -DPACKAGE_VERSION=\"0.6.1-6-g4061d86\" "-DPACKAGE_STRING=\"swath 0.6.1-6-g4061d86\"" -DPACKAGE_BUGREPORT=\"https://github.com/tlwg/swath/issues\" -DPACKAGE_URL=\"\" -DPACKAGE=\"swath\" -DVERSION=\"0.6.1-6-g4061d86\" -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DHAVE_DLFCN_H=1 -DLT_OBJDIR=\".libs/\" -DSTDC_HEADERS=1 -DHAVE_LIMITS_H=1 -I. -DNDEBUG -g -O2 -MT utf8.lo -MD -MP -MF .deps/utf8.Tpo -c utf8.cxx -o utf8.o >/dev/null 2>&1
mv -f .deps/utf8.Tpo .deps/utf8.Plo
/bin/bash ../libtool  --tag=CXX   --mode=link g++  -g -O2   -o libconv.la  conv.lo convfact.lo tis620.lo utf8.lo  
libtool: link: ar cru .libs/libconv.a .libs/conv.o .libs/convfact.o .libs/tis620.o .libs/utf8.o 
ar: `u' modifier ignored since `D' is the default (see `U')
libtool: link: ranlib .libs/libconv.a
libtool: link: ( cd ".libs" && rm -f "libconv.la" && ln -s "../libconv.la" "libconv.la" )
make[1]: Leaving directory '/home/ye/tool/swath/conv'
Making all in src
make[1]: Entering directory '/home/ye/tool/swath/src'
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT dict.o -MD -MP -MF .deps/dict.Tpo -c -o dict.o dict.cpp
mv -f .deps/dict.Tpo .deps/dict.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT abswordseg.o -MD -MP -MF .deps/abswordseg.Tpo -c -o abswordseg.o abswordseg.cpp
mv -f .deps/abswordseg.Tpo .deps/abswordseg.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT convutil.o -MD -MP -MF .deps/convutil.Tpo -c -o convutil.o convutil.cpp
mv -f .deps/convutil.Tpo .deps/convutil.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT filefilter.o -MD -MP -MF .deps/filefilter.Tpo -c -o filefilter.o filefilter.cpp
mv -f .deps/filefilter.Tpo .deps/filefilter.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT filterhtml.o -MD -MP -MF .deps/filterhtml.Tpo -c -o filterhtml.o filterhtml.cpp
mv -f .deps/filterhtml.Tpo .deps/filterhtml.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT filterlatex.o -MD -MP -MF .deps/filterlatex.Tpo -c -o filterlatex.o filterlatex.cpp
mv -f .deps/filterlatex.Tpo .deps/filterlatex.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT filterrtf.o -MD -MP -MF .deps/filterrtf.Tpo -c -o filterrtf.o filterrtf.cpp
mv -f .deps/filterrtf.Tpo .deps/filterrtf.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT longwordseg.o -MD -MP -MF .deps/longwordseg.Tpo -c -o longwordseg.o longwordseg.cpp
mv -f .deps/longwordseg.Tpo .deps/longwordseg.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT maxwordseg.o -MD -MP -MF .deps/maxwordseg.Tpo -c -o maxwordseg.o maxwordseg.cpp
mv -f .deps/maxwordseg.Tpo .deps/maxwordseg.Po
g++ -DWORDSEGDATA_DIR=\"/usr/local/share/swath\" -DVERSION=\"0.6.1-6-g4061d86\" -I.  -I.. -I/usr/local/include -DNDEBUG  -g -O2 -MT wordseg.o -MD -MP -MF .deps/wordseg.Tpo -c -o wordseg.o wordseg.cpp
mv -f .deps/wordseg.Tpo .deps/wordseg.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++  -g -O2   -o swath dict.o abswordseg.o convutil.o filefilter.o filterhtml.o filterlatex.o filterrtf.o longwordseg.o maxwordseg.o wordseg.o ../conv/libconv.la -L/usr/local/lib -ldatrie 
libtool: link: g++ -g -O2 -o swath dict.o abswordseg.o convutil.o filefilter.o filterhtml.o filterlatex.o filterrtf.o longwordseg.o maxwordseg.o wordseg.o   ../conv/.libs/libconv.a -L/usr/local/lib /usr/local/lib/libdatrie.so
make[1]: Leaving directory '/home/ye/tool/swath/src'
Making all in data
make[1]: Entering directory '/home/ye/tool/swath/data'
cat tdict-city.txt tdict-collection.txt tdict-common.txt tdict-country.txt tdict-district.txt tdict-geo.txt tdict-history.txt tdict-ict.txt tdict-lang-ethnic.txt tdict-proper.txt tdict-science.txt tdict-slang.txt tdict-spell.txt tdict-std-compound.txt tdict-std.txt | LC_ALL=C sort -u > swathdic.lst
if test ! -e swathdic.abm; then \
  ln -s ./swathdic.abm . ; \
fi
rm -f swathdic.tri
trietool-0.2 swathdic add-list -e utf-8 swathdic.lst
make[1]: Leaving directory '/home/ye/tool/swath/data'
Making all in tests
make[1]: Entering directory '/home/ye/tool/swath/tests'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/ye/tool/swath/tests'
make[1]: Entering directory '/home/ye/tool/swath'
make[1]: Nothing to be done for 'all-am'.
make[1]: Leaving directory '/home/ye/tool/swath'
(base) ye@ykt-pro:~/tool/swath$ 

```

## run make install

```
(base) ye@ykt-pro:~/tool/swath$ sudo make install
Making install in conv
make[1]: Entering directory '/home/ye/tool/swath/conv'
make[2]: Entering directory '/home/ye/tool/swath/conv'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/swath/conv'
make[1]: Leaving directory '/home/ye/tool/swath/conv'
Making install in src
make[1]: Entering directory '/home/ye/tool/swath/src'
make[2]: Entering directory '/home/ye/tool/swath/src'
 /bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c swath '/usr/local/bin'
libtool: install: /usr/bin/install -c swath /usr/local/bin/swath
 /bin/mkdir -p '/usr/local/share/man/man1'
 /usr/bin/install -c -m 644 swath.1 '/usr/local/share/man/man1'
make[2]: Leaving directory '/home/ye/tool/swath/src'
make[1]: Leaving directory '/home/ye/tool/swath/src'
Making install in data
make[1]: Entering directory '/home/ye/tool/swath/data'
make[2]: Entering directory '/home/ye/tool/swath/data'
make[2]: Nothing to be done for 'install-exec-am'.
 /bin/mkdir -p '/usr/local/share/swath'
 /usr/bin/install -c -m 644 swathdic.tri '/usr/local/share/swath'
make[2]: Leaving directory '/home/ye/tool/swath/data'
make[1]: Leaving directory '/home/ye/tool/swath/data'
Making install in tests
make[1]: Entering directory '/home/ye/tool/swath/tests'
make[2]: Entering directory '/home/ye/tool/swath/tests'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/swath/tests'
make[1]: Leaving directory '/home/ye/tool/swath/tests'
make[1]: Entering directory '/home/ye/tool/swath'
make[2]: Entering directory '/home/ye/tool/swath'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/swath'
make[1]: Leaving directory '/home/ye/tool/swath'
(base) ye@ykt-pro:~/tool/swath$
```

## Testing SWATH Thai word segmentation

Traditionally, we did --help  

```
(base) ye@ykt-pro:~/tool/swath$ swath --help
Usage: swath [mule] [-v|--verbose] [-b "delimiter"] [-d dict-dir]
       [-f html|rtf|latex|lambda] [-m long|max] [-u {u|t},{u|t}] [-h|[-]-help]
Options:
	mule : for use with mule
	-v   : verbose mode
	-b   : define a word delimiter string for the output
	-d   : specify dictionary path
	-f   : specify format of the input
		html     : HTML file
		rtf      : RTF file
		latex    : LaTeX file
		lambda   : The input and output are same as latex, except that
		           the word delimiter is ^^^^200b
	-m   : choose word matching scheme when analyzing
		long     : longest matching scheme
		max      : maximal matching scheme
	-u   : specify encodings of input and output in 'i,o' form,
	       for input and output respectively, where 'i', 'o' is one of:
		u        : The input/output is in UTF-8
		t        : The input/output is in TIS-620
	-help: display this help message
(base) ye@ykt-pro:~/tool/swath$ 

```

***Finished swath installation!!! :)  
Reference: [http://www.cs.cmu.edu/~paisarn/papers/swathmanual.pdf](http://www.cs.cmu.edu/~paisarn/papers/swathmanual.pdf)  

## Word Segmentation with SWATH  

I copied one long thai sentence from the web.  

```
(base) ye@ykt-pro:~/tool/swath$ cat thai-input.nospace.txt 
Vaseline(วาสลีน)แบรนด์ที่มุ่งมั่นพัฒนาสังคมยืนเคียงข้างส่งต่อความห่วงใยพร้อมดูแลสุขภาพผิวของคนไทยมายาวนานในช่วงเวลาแห่งความหวั่นวิตกที่ประเทศไทยและทั่วโลกกำลังเผชิญสถานการณ์การแพร่ระบาดของไวรัสโควิด-19นี้วาสลีนจึงขอเป็นกระบอกเสียงผ่านวิดีโอ"ดูแลมือตัวเองให้ดีที่สุด"นำโดย"หมอเจี๊ยบ-ลลนาก้องธรนินทร์"ด้วยความตั้งใจที่จะบอกกับทุกคนว่าการดูแลสุขภาพร่างกายตัวเองให้แข็งแรงและดูแลมือตัวเองให้สะอาดด้วยการล้างมืออย่างถูกต้องใช้เจลแอลกอฮอล์70%และทาครีมบำรุงมืออย่างสม่ำเสมอจะเป็นการป้องกันจำนวนของผู้ติดเชื้อไม่ให้กลับมาเพิ่มสูงอีกและช่วยผ่อนภาระของบุคลากรทางการแพทย์ได้เป็นอย่างดีซึ่งนับเป็นคำขอบคุณและกำลังใจที่ดีที่สุดที่เราทุกคนสามารถทำได้เพื่อบุคลากรทางการแพทย์ผู้เสียสละและทุ่มเทปฏิบัติหน้าที่อย่างไม่เคยย่อท้อ
```

Example 1, word delimeter with pipe symbol.  
input, output encoding = utf-8, utf-8  

```
(base) ye@ykt-pro:~/tool/swath$ swath -b '|' -u 'u,u'  < ./thai-input.nospace.txt 
Vaseline(วา|ส|ลี|น)แบรนด์|ที่|มุ่งมั่น|พัฒนา|สังคม|ยืน|เคียง|ข้าง|ส่ง|ต่อ|ความ|ห่วงใย|พร้อม|ดูแล|สุขภาพ|ผิว|ของ|คน|ไทย|มา|ยาว|นาน|ใน|ช่วง|เวลา|แห่ง|ความ|หวั่นวิตก|ที่|ประเทศ|ไทย|และ|ทั่ว|โลก|กำลัง|เผชิญ|สถานการณ์|การ|แพร่|ระบาด|ของ|ไวรัส|โค|วิด-19นี้|วา|ส|ลี|น|จึง|ขอ|เป็น|กระบอก|เสียง|ผ่าน|วิดีโอ"ดูแล|มือ|ตัวเอง|ให้|ดี|ที่สุด"นำ|โดย"หมอ|เจี๊ยบ-ลลนา|ก้อง|ธร|นิ|นทร์"ด้วย|ความ|ตั้งใจ|ที่|จะ|บอก|กับ|ทุก|คน|ว่า|การ|ดูแล|สุขภาพ|ร่างกาย|ตัวเอง|ให้|แข็งแรง|และ|ดูแล|มือ|ตัวเอง|ให้|สะอาด|ด้วย|การ|ล้าง|มือ|อย่าง|ถูกต้อง|ใช้|เจล|แอลกอฮอล์70%และ|ทา|ครีม|บำรุง|มือ|อย่าง|สม่ำเสมอ|จะ|เป็น|การ|ป้องกัน|จำนวน|ของ|ผู้|ติด|เชื้อ|ไม่|ให้|กลับ|มา|เพิ่ม|สูง|อีก|และ|ช่วย|ผ่อน|ภาระ|ของ|บุคลากร|ทางการ|แพทย์|ได้|เป็น|อย่าง|ดี|ซึ่ง|นับ|เป็น|คำ|ขอบคุณ|และ|กำลังใจ|ที่|ดี|ที่สุด|ที่|เรา|ทุก|คน|สามารถ|ทำ|ได้|เพื่อ|บุคลากร|ทางการ|แพทย์|ผู้|เสียสละ|และ|ทุ่มเท|ปฏิบัติ|หน้าที่|อย่าง|ไม่|เคย|ย่อท้อ
```

If you don't give encoding parameter "-u", it is not working as follows:  

```
(base) ye@ykt-pro:~/tool/swath$ swath -b '|'  < ./thai-input.nospace.txt 
Vaseline(วาสลี฀)เ฀ร฀฀เ฀ีเมุเ฀มัเ฀฀ั฀฀าสั฀฀มยื฀เ฀ีย฀฀เา฀สเ฀฀เอ฀วามหเว฀เย฀รเอม฀ูเลสุ฀฀า฀฀ิว฀อ฀฀฀เ฀ยมายาว฀า฀เ฀฀เว฀เวลาเหเ฀฀วามหวัเ฀วิ฀฀฀ีเ฀ระเ฀ศเ฀ยเละ฀ัเวเล฀฀ำลั฀เ฀฀ิ฀ส฀า฀฀าร฀เ฀ารเ฀รเระ฀า฀฀อ฀เวรัสเ฀วิ฀-19฀ีเวาสลี฀฀ึ฀฀อเ฀เ฀฀ระ฀อ฀เสีย฀฀เา฀วิ฀ีเอ"฀ูเลมือ฀ัวเอ฀เหเ฀ี฀ีเสุ฀"฀ำเ฀ย"หมอเ฀ีเย฀-ลล฀า฀เอ฀฀ร฀ิ฀฀รเ"฀เวย฀วาม฀ัเ฀เ฀฀ีเ฀ะ฀อ฀฀ั฀฀ุ฀฀฀วเา฀าร฀ูเลสุ฀฀า฀รเา฀฀าย฀ัวเอ฀เหเเ฀เ฀เร฀เละ฀ูเลมือ฀ัวเอ฀เหเสะอา฀฀เวย฀ารลเา฀มืออยเา฀฀ู฀฀เอ฀เ฀เเ฀ลเอล฀อฮอลเ70%เละ฀า฀รีม฀ำรุ฀มืออยเา฀สมเำเสมอ฀ะเ฀เ฀฀าร฀เอ฀฀ั฀฀ำ฀ว฀฀อ฀฀ูเ฀ิ฀เ฀ืเอเมเเหเ฀ลั฀มาเ฀ิเมสู฀อี฀เละ฀เวย฀เอ฀฀าระ฀อ฀฀ุ฀ลา฀ร฀า฀฀ารเ฀฀ยเเ฀เเ฀เ฀อยเา฀฀ี฀ึเ฀฀ั฀เ฀เ฀฀ำ฀อ฀฀ุ฀เละ฀ำลั฀เ฀฀ีเ฀ี฀ีเสุ฀฀ีเเรา฀ุ฀฀฀สามาร฀฀ำเ฀เเ฀ืเอ฀ุ฀ลา฀ร฀า฀฀ารเ฀฀ยเ฀ูเเสียสละเละ฀ุเมเ฀฀฀ิ฀ั฀ิห฀เา฀ีเอยเา฀เมเเ฀ยยเอ฀เอ
```
