
## git clone

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/irstlm-team/irstlm
Cloning into 'irstlm'...
remote: Enumerating objects: 1781, done.
remote: Total 1781 (delta 0), reused 0 (delta 0), pack-reused 1781
Receiving objects: 100% (1781/1781), 3.54 MiB | 674.00 KiB/s, done.
Resolving deltas: 100% (1187/1187), done.
```

## check files

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd irstlm/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ ls
CMakeLists.txt  configure.ac  Copyright  doc  LICENSE  Makefile.am  NOTE  README.md  regenerate-makefiles.sh  scripts  src
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## Regnerate Makefile

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ sh regenerate-makefiles.sh --force
Calling /usr/bin/autoreconf
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: error: required file './ar-lib' not found
configure.ac:10:   'automake --add-missing' can install 'ar-lib'
configure.ac:3: error: required file './compile' not found
configure.ac:3:   'automake --add-missing' can install 'compile'
configure.ac:5: error: required file './config.guess' not found
configure.ac:5:   'automake --add-missing' can install 'config.guess'
configure.ac:5: error: required file './config.sub' not found
configure.ac:5:   'automake --add-missing' can install 'config.sub'
configure.ac:2: error: required file './install-sh' not found
configure.ac:2:   'automake --add-missing' can install 'install-sh'
configure.ac:5: error: required file './ltmain.sh' not found
configure.ac:2: error: required file './missing' not found
configure.ac:2:   'automake --add-missing' can install 'missing'
src/Makefile.am: error: required file './depcomp' not found
src/Makefile.am:   'automake --add-missing' can install 'depcomp'
autoreconf: automake failed with exit status: 1
autoreconf FAILED
trying '/home/ye/anaconda3/bin/libtoolize --force; /usr/bin/automake --add-missing ; /usr/bin/autoreconf'
libtoolize: putting auxiliary files in '.'.
libtoolize: linking file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: linking file 'm4/libtool.m4'
libtoolize: linking file 'm4/ltoptions.m4'
libtoolize: linking file 'm4/ltsugar.m4'
libtoolize: linking file 'm4/ltversion.m4'
libtoolize: linking file 'm4/lt~obsolete.m4'
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:9124: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: installing './ar-lib'
configure.ac:3: installing './compile'
configure.ac:5: installing './config.guess'
configure.ac:5: installing './config.sub'
configure.ac:2: installing './install-sh'
configure.ac:2: installing './missing'
src/Makefile.am: installing './depcomp'
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
/usr/share/aclocal-1.16/ar-lib.m4:13: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## ./configure

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking whether make supports the include directive... yes (GNU style)
checking dependency style of gcc... gcc3
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking dependency style of g++... gcc3
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking how to print strings... printf
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... yes
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
checking for a working dd... /usr/bin/dd
checking how to truncate binary pipes... /usr/bin/dd bs=4096 count=1
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
checking the archiver (ar) interface... ar
configure: documentation will not be created (default); get it through the website 
configure: trace enabled (default); trace level is overwritten to default value 1
configure: assert enabled (default)
configure: generation of debugging symbols disabled (default), compilation without "-g", only "-O2"
configure: profiling disabled (default)
configure: caching disabled (default)
configure: caching disabled (default)
configure: interpolated search disabled (default)
configure: optimization disabled (default)
configure: c++x0 dialect is enabled (default), compilation with "-DHAVE_CXX0 -std=c++0x "
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating scripts/Makefile
config.status: creating doc/Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
configure: The software will be installed into /usr/local
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## Check

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ echo | g++ -E -x c++ -std=c++0x -dM - >& /dev/null ; echo $?
0
```

It looks OK!  

Reference: [https://github.com/irstlm-team/irstlm](https://github.com/irstlm-team/irstlm)  

## run make

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ make
(CDPATH="${ZSH_VERSION+.}:" && cd . && /bin/bash /home/ye/tool/irstlm/missing autoheader)
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
rm -f stamp-h1
touch config.h.in
cd . && /bin/bash ./config.status config.h
config.status: creating config.h
config.status: config.h is unchanged
make  all-recursive
make[1]: Entering directory '/home/ye/tool/irstlm'
Making all in src
make[2]: Entering directory '/home/ye/tool/irstlm/src'
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -isystem/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT dict.o -MD -MP -MF .deps/dict.Tpo -c -o dict.o dict.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from /usr/include/c++/10/ext/string_conversions.h:41,
                 from /usr/include/c++/10/bits/basic_string.h:6535,
                 from /usr/include/c++/10/string:55,
                 from /usr/include/c++/10/bits/locale_classes.h:40,
                 from /usr/include/c++/10/bits/ios_base.h:41,
                 from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from dict.cpp:23:
/usr/include/c++/10/cstdlib:75:15: fatal error: stdlib.h: No such file or directory
   75 | #include_next <stdlib.h>
      |               ^~~~~~~~~~
compilation terminated.
make[2]: *** [Makefile:753: dict.o] Error 1
make[2]: Leaving directory '/home/ye/tool/irstlm/src'
make[1]: *** [Makefile:407: all-recursive] Error 1
make[1]: Leaving directory '/home/ye/tool/irstlm'
make: *** [Makefile:339: all] Error 2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## Update Makefile.am

Reference: https://lintaka.wordpress.com/2018/12/13/irstlm-error/

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ gedit src/Makefile.am 

#AM_CXXFLAGS = -static -isystem/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES $(BOOST_CPPFLAGS) -DMYCODESIZE=3
AM_CXXFLAGS = -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES $(BOOST_CPPFLAGS) -DMYCODESIZE=3
```

## Rrun make again

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ make
make  all-recursive
make[1]: Entering directory '/home/ye/tool/irstlm'
Making all in src
make[2]: Entering directory '/home/ye/tool/irstlm/src'
 cd .. && /bin/bash /home/ye/tool/irstlm/missing automake-1.16 --foreign src/Makefile
configure.ac:10: warning: LT_INIT was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
configure.ac:10: warning: AC_PROG_LIBTOOL was called before AM_PROG_AR
aclocal.m4:70: AM_PROG_AR is expanded from...
configure.ac:10: the top level
 cd .. && /bin/bash ./config.status src/Makefile depfiles
config.status: creating src/Makefile
config.status: executing depfiles commands
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT dict.o -MD -MP -MF .deps/dict.Tpo -c -o dict.o dict.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dict.cpp:26:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from dict.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dict.cpp:26:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from dict.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dict.cpp:26:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from dict.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/dict.Tpo .deps/dict.Po
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x  -g -O2 -MT cmd.lo -MD -MP -MF .deps/cmd.Tpo -c -o cmd.lo cmd.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -g -O2 -MT cmd.lo -MD -MP -MF .deps/cmd.Tpo -c cmd.c  -fPIC -DPIC -o .libs/cmd.o
cc1: warning: command-line option ‘-std=c++11’ is valid for C++/ObjC++ but not for C
cmd.c: In function ‘SetParam’:
cmd.c:705:15: warning: comparison between pointer and zero character constant [-Wpointer-compare]
  705 |  if (!*s || (s=='\0' && cmd->Flag==0)){
      |               ^~
cmd.c:705:14: note: did you mean to dereference the pointer?
  705 |  if (!*s || (s=='\0' && cmd->Flag==0)){
      |              ^
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -g -O2 -MT cmd.lo -MD -MP -MF .deps/cmd.Tpo -c cmd.c -o cmd.o >/dev/null 2>&1
mv -f .deps/cmd.Tpo .deps/cmd.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x  -g -O2 -MT thpool.lo -MD -MP -MF .deps/thpool.Tpo -c -o thpool.lo thpool.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -g -O2 -MT thpool.lo -MD -MP -MF .deps/thpool.Tpo -c thpool.c  -fPIC -DPIC -o .libs/thpool.o
cc1: warning: command-line option ‘-std=c++11’ is valid for C++/ObjC++ but not for C
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -g -O2 -MT thpool.lo -MD -MP -MF .deps/thpool.Tpo -c thpool.c -o thpool.o >/dev/null 2>&1
mv -f .deps/thpool.Tpo .deps/thpool.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT dictionary.lo -MD -MP -MF .deps/dictionary.Tpo -c -o dictionary.lo dictionary.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT dictionary.lo -MD -MP -MF .deps/dictionary.Tpo -c dictionary.cpp -o dictionary.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from dictionary.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/iomanip:40,
                 from dictionary.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from dictionary.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/iomanip:40,
                 from dictionary.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from dictionary.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/iomanip:40,
                 from dictionary.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/dictionary.Tpo .deps/dictionary.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT htable.lo -MD -MP -MF .deps/htable.Tpo -c -o htable.lo htable.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT htable.lo -MD -MP -MF .deps/htable.Tpo -c htable.cpp -o htable.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
mv -f .deps/htable.Tpo .deps/htable.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT lmContainer.lo -MD -MP -MF .deps/lmContainer.Tpo -c -o lmContainer.lo lmContainer.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT lmContainer.lo -MD -MP -MF .deps/lmContainer.Tpo -c lmContainer.cpp -o lmContainer.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmContainer.cpp:30:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmContainer.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmContainer.cpp:30:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmContainer.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmContainer.cpp:30:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmContainer.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from lmContainer.cpp:32:
lmmacro.h: In member function ‘virtual bool irstlm::lmmacro::is_OOV(int)’:
lmmacro.h:101:16: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  101 |     field_ng = word_ng;
      |                ^~~~~~~
In file included from lmContainer.h:37,
                 from lmContainer.cpp:30:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mv -f .deps/lmContainer.Tpo .deps/lmContainer.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT lmclass.lo -MD -MP -MF .deps/lmclass.Tpo -c -o lmclass.lo lmclass.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT lmclass.lo -MD -MP -MF .deps/lmclass.Tpo -c lmclass.cpp -o lmclass.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmclass.cpp:32:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmclass.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmclass.cpp:32:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmclass.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmclass.cpp:32:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmclass.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/lmclass.Tpo .deps/lmclass.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT lmmacro.lo -MD -MP -MF .deps/lmmacro.Tpo -c -o lmmacro.lo lmmacro.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT lmmacro.lo -MD -MP -MF .deps/lmmacro.Tpo -c lmmacro.cpp -o lmmacro.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmmacro.cpp:32:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmmacro.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmmacro.cpp:32:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmmacro.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmmacro.cpp:32:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmmacro.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from lmmacro.cpp:35:
lmmacro.h: In member function ‘virtual bool irstlm::lmmacro::is_OOV(int)’:
lmmacro.h:101:16: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  101 |     field_ng = word_ng;
      |                ^~~~~~~
In file included from lmmacro.cpp:33:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
lmmacro.cpp: In member function ‘bool irstlm::lmmacro::transform(ngram&, ngram&)’:
lmmacro.cpp:367:15: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  367 |    field_ng = in;
      |               ^~
In file included from lmmacro.cpp:33:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
lmmacro.cpp:375:19: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  375 |    collapsed_ng = field_ng;
      |                   ^~~~~~~~
In file included from lmmacro.cpp:33:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mv -f .deps/lmmacro.Tpo .deps/lmmacro.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT lmtable.lo -MD -MP -MF .deps/lmtable.Tpo -c -o lmtable.lo lmtable.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT lmtable.lo -MD -MP -MF .deps/lmtable.Tpo -c lmtable.cpp -o lmtable.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmtable.cpp:36:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmtable.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.cpp:36:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmtable.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.cpp:36:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmtable.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::loadtxt_level(std::istream&, int)’:
lmtable.cpp:833:9: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  833 |      ng=ing;
      |         ^~~
In file included from lmtable.cpp:37:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
lmtable.cpp: In member function ‘double irstlm::lmtable::lprobx(ngram, double*, double*, int*)’:
lmtable.cpp:2711:14: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 2711 |   ctx = ng = ong;
      |              ^~~
In file included from lmtable.cpp:37:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
lmtable.cpp:2711:14: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 2711 |   ctx = ng = ong;
      |              ^~~
In file included from lmtable.cpp:37:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::loadtxt_mmap(std::istream&, const char*, const char*)’:
lmtable.cpp:622:15: warning: ignoring return value of ‘int ftruncate(int, __off64_t)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  622 |      ftruncate(fileno(fd),filesize);
      |      ~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~
lmtable.cpp:724:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  724 |   system(cmd);
      |   ~~~~~~^~~~~
lmtable.cpp:728:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  728 |   system(cmd);
      |   ~~~~~~^~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::expand_level_mmap(int, table_entry_pos_t, const char*)’:
lmtable.cpp:887:12: warning: ignoring return value of ‘int ftruncate(int, __off64_t)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  887 |   ftruncate(fileno(fd),filesize);
      |   ~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::concatenate_single_level(int, const char*, const char*)’:
lmtable.cpp:1785:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1785 |   system(cmd);
      |   ~~~~~~^~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::compact_single_level(int, const char*)’:
lmtable.cpp:1856:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1856 |   system(cmd);
      |   ~~~~~~^~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::resize_level_mmap(int, const char*)’:
lmtable.cpp:1889:12: warning: ignoring return value of ‘int ftruncate(int, __off64_t)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1889 |   ftruncate(fileno(fd),filesize);
      |   ~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::loadbin(std::istream&, const char*, const char*, int)’:
lmtable.cpp:1996:8: warning: ignoring return value of ‘ssize_t read(int, void*, size_t)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1996 |    read(diskid,miniheader,4);
      |    ~~~~^~~~~~~~~~~~~~~~~~~~~
lmtable.cpp: In member function ‘void irstlm::lmtable::loadtxt_mmap(std::istream&, const char*, const char*)’:
lmtable.cpp:722:20: warning: ‘%s’ directive writing up to 8191 bytes into a region of size 8188 [-Wformat-overflow=]
  722 |   sprintf(cmd,"cat %s >> %s", nameNgrams, nameHeader);
      |                    ^~         ~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from lmtable.cpp:23:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:34: note: ‘__builtin___sprintf_chk’ output between 9 and 16391 bytes into a destination of size 8192
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lmtable.cpp:722:20: warning: ‘%s’ directive writing up to 8191 bytes into a region of size 8188 [-Wformat-overflow=]
  722 |   sprintf(cmd,"cat %s >> %s", nameNgrams, nameHeader);
      |                    ^~         ~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from lmtable.cpp:23:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:34: note: ‘__builtin___sprintf_chk’ output between 9 and 16391 bytes into a destination of size 8192
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lmtable.cpp:726:19: warning: ‘%s’ directive writing up to 8191 bytes into a region of size 8189 [-Wformat-overflow=]
  726 |   sprintf(cmd,"mv %s %s", nameHeader, outfilename);
      |                   ^~      ~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from lmtable.cpp:23:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:34: note: ‘__builtin___sprintf_chk’ output 5 or more bytes (assuming 8196) into a destination of size 8192
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
mv -f .deps/lmtable.Tpo .deps/lmtable.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT lmInterpolation.lo -MD -MP -MF .deps/lmInterpolation.Tpo -c -o lmInterpolation.lo lmInterpolation.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT lmInterpolation.lo -MD -MP -MF .deps/lmInterpolation.Tpo -c lmInterpolation.cpp -o lmInterpolation.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmInterpolation.cpp:28:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmInterpolation.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmInterpolation.cpp:28:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmInterpolation.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from lmInterpolation.cpp:28:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from lmInterpolation.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/lmInterpolation.Tpo .deps/lmInterpolation.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT mempool.lo -MD -MP -MF .deps/mempool.Tpo -c -o mempool.lo mempool.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT mempool.lo -MD -MP -MF .deps/mempool.Tpo -c mempool.cpp -o mempool.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
mv -f .deps/mempool.Tpo .deps/mempool.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT mfstream.lo -MD -MP -MF .deps/mfstream.Tpo -c -o mfstream.lo mfstream.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT mfstream.lo -MD -MP -MF .deps/mfstream.Tpo -c mfstream.cpp -o mfstream.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from mfstream.cpp:28:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mfstream.cpp:28:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mfstream.cpp:28:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mfstream.cpp:92:67: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
   92 | mfstream& mfstream::iwritex(streampos loc,void *ptr,int size,int n)
      |                                                                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mfstream.cpp: In member function ‘mfstream& mfstream::iwritex(std::ios_base::streampos, void*, int, int)’:
mfstream.cpp:94:13: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
   94 |   streampos pos=tellp();
      |             ^~~
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mfstream.cpp: In member function ‘std::streampos mfstream::tellp()’:
mfstream.cpp:136:10: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  136 |  return (streampos) fstream::tellg();
      |          ^~~~~~~~~
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mfstream.cpp: At global scope:
mfstream.cpp:140:40: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  140 | mfstream& mfstream::seekp(streampos loc) {
      |                                        ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/mfstream.Tpo .deps/mfstream.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT n_gram.lo -MD -MP -MF .deps/n_gram.Tpo -c -o n_gram.lo n_gram.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT n_gram.lo -MD -MP -MF .deps/n_gram.Tpo -c n_gram.cpp -o n_gram.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.cpp:32:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/iomanip:40,
                 from n_gram.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.cpp:32:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/iomanip:40,
                 from n_gram.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.cpp:32:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/iomanip:40,
                 from n_gram.cpp:27:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from /usr/include/string.h:519,
                 from /usr/include/c++/10/cstring:42,
                 from htable.h:30,
                 from n_gram.cpp:31:
In function ‘void* memcpy(void*, const void*, size_t)’,
    inlined from ‘std::ifstream& operator>>(std::ifstream&, ngram&)’ at n_gram.cpp:142:9:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:34:33: warning: ‘void* __builtin_memcpy(void*, const void*, long unsigned int)’ accessing 76 bytes at offsets 0 and 4 overlaps 72 bytes at offset 4 [-Wrestrict]
   34 |   return __builtin___memcpy_chk (__dest, __src, __len, __bos0 (__dest));
      |          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
mv -f .deps/n_gram.Tpo .deps/n_gram.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT ngramcache.lo -MD -MP -MF .deps/ngramcache.Tpo -c -o ngramcache.lo ngramcache.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT ngramcache.lo -MD -MP -MF .deps/ngramcache.Tpo -c ngramcache.cpp -o ngramcache.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from ngramcache.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngramcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from ngramcache.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngramcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from ngramcache.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngramcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/ngramcache.Tpo .deps/ngramcache.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT ngramtable.lo -MD -MP -MF .deps/ngramtable.Tpo -c -o ngramtable.lo ngramtable.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT ngramtable.lo -MD -MP -MF .deps/ngramtable.Tpo -c ngramtable.cpp -o ngramtable.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from ngramtable.cpp:25:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from ngramtable.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from ngramtable.cpp:25:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from ngramtable.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from ngramtable.cpp:25:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from ngramtable.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
ngramtable.cpp: In constructor ‘ngramtable::ngramtable(char*, int, char*, dictionary*, char*, int, int, char*, int, TABLETYPE, int)’:
ngramtable.cpp:229:27: warning: ‘%d’ directive writing between 1 and 11 bytes into a region of size between 0 and 99 [-Wformat-overflow=]
  229 |         sprintf(info2,"%s %d %f",info,resolution,decay);
      |                           ^~
ngramtable.cpp:229:23: note: assuming directive output of 8 bytes
  229 |         sprintf(info2,"%s %d %f",info,resolution,decay);
      |                       ^~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from /usr/include/c++/10/cstdio:42,
                 from /usr/include/c++/10/ext/string_conversions.h:43,
                 from /usr/include/c++/10/bits/basic_string.h:6535,
                 from /usr/include/c++/10/string:55,
                 from /usr/include/c++/10/bits/locale_classes.h:40,
                 from /usr/include/c++/10/bits/ios_base.h:41,
                 from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from ngramtable.cpp:23:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:34: note: ‘__builtin___sprintf_chk’ output between 7 and 430 bytes into a destination of size 100
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
mv -f .deps/ngramtable.Tpo .deps/ngramtable.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT timer.lo -MD -MP -MF .deps/timer.Tpo -c -o timer.lo timer.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT timer.lo -MD -MP -MF .deps/timer.Tpo -c timer.cpp -o timer.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
mv -f .deps/timer.Tpo .deps/timer.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT util.lo -MD -MP -MF .deps/util.Tpo -c -o util.lo util.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT util.lo -MD -MP -MF .deps/util.Tpo -c util.cpp -o util.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from util.cpp:37:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.cpp:29:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from util.cpp:37:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.cpp:29:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from util.cpp:37:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.cpp:29:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/util.Tpo .deps/util.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT crc.lo -MD -MP -MF .deps/crc.Tpo -c -o crc.lo crc.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT crc.lo -MD -MP -MF .deps/crc.Tpo -c crc.cpp -o crc.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
mv -f .deps/crc.Tpo .deps/crc.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT interplm.lo -MD -MP -MF .deps/interplm.Tpo -c -o interplm.lo interplm.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT interplm.lo -MD -MP -MF .deps/interplm.Tpo -c interplm.cpp -o interplm.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from interplm.cpp:23:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from interplm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from interplm.cpp:23:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from interplm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from interplm.cpp:23:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from interplm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/interplm.Tpo .deps/interplm.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT linearlm.lo -MD -MP -MF .deps/linearlm.Tpo -c -o linearlm.lo linearlm.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT linearlm.lo -MD -MP -MF .deps/linearlm.Tpo -c linearlm.cpp -o linearlm.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from linearlm.cpp:25:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from linearlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from linearlm.cpp:25:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from linearlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from linearlm.cpp:25:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from linearlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/linearlm.Tpo .deps/linearlm.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT mdiadapt.lo -MD -MP -MF .deps/mdiadapt.Tpo -c -o mdiadapt.lo mdiadapt.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT mdiadapt.lo -MD -MP -MF .deps/mdiadapt.Tpo -c mdiadapt.cpp -o mdiadapt.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from mdiadapt.cpp:24:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from mdiadapt.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mdiadapt.cpp:24:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from mdiadapt.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mdiadapt.cpp:24:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from mdiadapt.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveBIN_per_word(char*, int, char*, int)’:
mdiadapt.cpp:1331:13: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 1331 |       locng=ng;      // make a local copy
      |             ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp:1394:12: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 1394 |      oldng=ng;
      |            ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveBIN_per_level(char*, int, char*, int)’:
mdiadapt.cpp:1640:11: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 1640 |       ng2=ng;
      |           ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveARPA_per_word(char*, int, char*)’:
mdiadapt.cpp:1823:12: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 1823 |      locng=ng;      // make a local copy
      |            ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp:1894:12: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 1894 |      oldng=ng;
      |            ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveARPA_per_level(char*, int, char*)’:
mdiadapt.cpp:2090:11: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
 2090 |       ng2=ng;
      |           ^~
In file included from mdiadapt.cpp:28:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveASR(char*, int, char*)’:
mdiadapt.cpp:758:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  758 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:915:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  915 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:1031:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1031 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveMT(char*, int, char*, int, double)’:
mdiadapt.cpp:1070:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1070 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveBIN_per_word(char*, int, char*, int)’:
mdiadapt.cpp:1175:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1175 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:1461:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1461 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveBIN_per_level(char*, int, char*, int)’:
mdiadapt.cpp:1471:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1471 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:1519:10: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1519 |    system("date");
      |    ~~~~~~^~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveARPA_per_word(char*, int, char*)’:
mdiadapt.cpp:1706:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1706 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:1926:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1926 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp: In member function ‘int irstlm::mdiadaptlm::saveARPA_per_level(char*, int, char*)’:
mdiadapt.cpp:1936:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1936 |   system("date");
      |   ~~~~~~^~~~~~~~
mdiadapt.cpp:2144:9: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 2144 |   system("date");
      |   ~~~~~~^~~~~~~~
mv -f .deps/mdiadapt.Tpo .deps/mdiadapt.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT mixture.lo -MD -MP -MF .deps/mixture.Tpo -c -o mixture.lo mixture.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT mixture.lo -MD -MP -MF .deps/mixture.Tpo -c mixture.cpp -o mixture.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from mixture.cpp:24:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from mixture.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mixture.cpp:24:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from mixture.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from mixture.cpp:24:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from mixture.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/mixture.Tpo .deps/mixture.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT normcache.lo -MD -MP -MF .deps/normcache.Tpo -c -o normcache.lo normcache.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT normcache.lo -MD -MP -MF .deps/normcache.Tpo -c normcache.cpp -o normcache.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from normcache.cpp:22:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from normcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from normcache.cpp:22:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from normcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from normcache.cpp:22:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from mfstream.h:26,
                 from normcache.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/normcache.Tpo .deps/normcache.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT shiftlm.lo -MD -MP -MF .deps/shiftlm.Tpo -c -o shiftlm.lo shiftlm.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT shiftlm.lo -MD -MP -MF .deps/shiftlm.Tpo -c shiftlm.cpp -o shiftlm.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from shiftlm.cpp:27:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from shiftlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from shiftlm.cpp:27:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from shiftlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from shiftlm.cpp:27:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from shiftlm.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/shiftlm.Tpo .deps/shiftlm.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT cplsa.lo -MD -MP -MF .deps/cplsa.Tpo -c -o cplsa.lo cplsa.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT cplsa.lo -MD -MP -MF .deps/cplsa.Tpo -c cplsa.cpp -o cplsa.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from cplsa.cpp:28:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cplsa.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cplsa.cpp:28:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cplsa.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cplsa.cpp:28:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cplsa.cpp:25:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
cplsa.cpp: In member function ‘int irstlm::plsa::initH()’:
cplsa.cpp:144:22: warning: ignoring return value of ‘int ftruncate(int, __off64_t)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  144 |             ftruncate(fileno(fd),len * sizeof(float));
      |             ~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cplsa.cpp: In member function ‘int irstlm::plsa::train(char*, char*, int, float, int)’:
cplsa.cpp:491:40: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  491 |         if (trset->numdoc()> 10) system("date");
      |                                  ~~~~~~^~~~~~~~
mv -f .deps/cplsa.Tpo .deps/cplsa.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT cswam.lo -MD -MP -MF .deps/cswam.Tpo -c -o cswam.lo cswam.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT cswam.lo -MD -MP -MF .deps/cswam.Tpo -c cswam.cpp -o cswam.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from cswam.cpp:30:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cswam.cpp:26:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cswam.cpp:30:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cswam.cpp:26:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cswam.cpp:30:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/sstream:38,
                 from cswam.cpp:26:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
cswam.cpp: In member function ‘void irstlm::cswam::loadword2vec(char*)’:
cswam.cpp:213:17: warning: this ‘for’ clause does not guard... [-Wmisleading-indentation]
  213 |                 for (int d=0;d<D;d++) cerr << " " << W2V[f][d]; cerr << "\n";}
      |                 ^~~
cswam.cpp:213:65: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘for’
  213 |                 for (int d=0;d<D;d++) cerr << " " << W2V[f][d]; cerr << "\n";}
      |                                                                 ^~~~
cswam.cpp: In member function ‘int irstlm::cswam::test(char*, char*, char*, char*, int)’:
cswam.cpp:1180:5: warning: this ‘for’ clause does not guard... [-Wmisleading-indentation]
 1180 |     for (int s=0;s<BUCKET;s++) delete [] alignments[s];delete [] alignments;
      |     ^~~
cswam.cpp:1180:56: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘for’
 1180 |     for (int s=0;s<BUCKET;s++) delete [] alignments[s];delete [] alignments;
      |                                                        ^~~~~~
cswam.cpp: In member function ‘int irstlm::cswam::train(char*, char*, char*, int, int)’:
cswam.cpp:1013:44: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
 1013 |         if (srcdata->numdoc()>10000) system("date");
      |                                      ~~~~~~^~~~~~~~
mv -f .deps/cswam.Tpo .deps/cswam.Plo
/bin/bash ../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT doc.lo -MD -MP -MF .deps/doc.Tpo -c -o doc.lo doc.cpp
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I.. -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -MT doc.lo -MD -MP -MF .deps/doc.Tpo -c doc.cpp -o doc.o
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from doc.cpp:22:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from doc.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from doc.cpp:22:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from doc.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from doc.cpp:22:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from doc.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/doc.Tpo .deps/doc.Plo
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o libirstlm.la -rpath /usr/local/lib cmd.lo thpool.lo dictionary.lo htable.lo lmContainer.lo lmclass.lo lmmacro.lo lmtable.lo lmInterpolation.lo mempool.lo mfstream.lo n_gram.lo ngramcache.lo ngramtable.lo timer.lo util.lo crc.lo interplm.lo linearlm.lo mdiadapt.lo mixture.lo normcache.lo shiftlm.lo cplsa.lo cswam.lo doc.lo   -lz
libtool: link: ar cru .libs/libirstlm.a  cmd.o thpool.o dictionary.o htable.o lmContainer.o lmclass.o lmmacro.o lmtable.o lmInterpolation.o mempool.o mfstream.o n_gram.o ngramcache.o ngramtable.o timer.o util.o crc.o interplm.o linearlm.o mdiadapt.o mixture.o normcache.o shiftlm.o cplsa.o cswam.o doc.o
ar: `u' modifier ignored since `D' is the default (see `U')
libtool: link: ranlib .libs/libirstlm.a
libtool: link: ( cd ".libs" && rm -f "libirstlm.la" && ln -s "../libirstlm.la" "libirstlm.la" )
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o dict dict.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o dict dict.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT ngt.o -MD -MP -MF .deps/ngt.Tpo -c -o ngt.o ngt.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from ngt.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngt.cpp:28:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from ngt.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngt.cpp:28:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from ngt.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from ngt.cpp:28:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
ngt.cpp: In function ‘int main(int, char**)’:
ngt.cpp:202:15: warning: implicitly-declared ‘ngram& ngram::operator=(const ngram&)’ is deprecated [-Wdeprecated-copy]
  202 |           ng2=ng;
      |               ^~
In file included from ngt.cpp:37:
n_gram.h:66:3: note: because ‘ngram’ has user-provided ‘ngram::ngram(const ngram&)’
   66 |   ngram(const ngram& ng);
      |   ^~~~~
mv -f .deps/ngt.Tpo .deps/ngt.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o ngt ngt.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o ngt ngt.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT dtsel.o -MD -MP -MF .deps/dtsel.Tpo -c -o dtsel.o dtsel.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dtsel.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from dtsel.cpp:31:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dtsel.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from dtsel.cpp:31:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dtsel.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from util.h:8,
                 from dtsel.cpp:31:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/dtsel.Tpo .deps/dtsel.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o dtsel dtsel.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o dtsel dtsel.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT compile-lm.o -MD -MP -MF .deps/compile-lm.Tpo -c -o compile-lm.o compile-lm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from compile-lm.cpp:32:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from compile-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from compile-lm.cpp:32:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from compile-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from compile-lm.cpp:32:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from compile-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/compile-lm.Tpo .deps/compile-lm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o compile-lm compile-lm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o compile-lm compile-lm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT interpolate-lm.o -MD -MP -MF .deps/interpolate-lm.Tpo -c -o interpolate-lm.o interpolate-lm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from interpolate-lm.cpp:31:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from interpolate-lm.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from interpolate-lm.cpp:31:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from interpolate-lm.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from n_gram.h:32,
                 from lmContainer.h:37,
                 from interpolate-lm.cpp:31:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from interpolate-lm.cpp:21:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/interpolate-lm.Tpo .deps/interpolate-lm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o interpolate-lm interpolate-lm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o interpolate-lm interpolate-lm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT prune-lm.o -MD -MP -MF .deps/prune-lm.Tpo -c -o prune-lm.o prune-lm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from prune-lm.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from prune-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from prune-lm.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from prune-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from prune-lm.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from prune-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/prune-lm.Tpo .deps/prune-lm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o prune-lm prune-lm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o prune-lm prune-lm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT quantize-lm.o -MD -MP -MF .deps/quantize-lm.Tpo -c -o quantize-lm.o quantize-lm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from quantize-lm.cpp:33:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from quantize-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from quantize-lm.cpp:33:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from quantize-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from quantize-lm.cpp:33:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from quantize-lm.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/quantize-lm.Tpo .deps/quantize-lm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o quantize-lm quantize-lm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o quantize-lm quantize-lm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT score-lm.o -MD -MP -MF .deps/score-lm.Tpo -c -o score-lm.o score-lm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from score-lm.cpp:29:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/fstream:38,
                 from score-lm.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from score-lm.cpp:29:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/fstream:38,
                 from score-lm.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from lmtable.h:39,
                 from score-lm.cpp:29:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/istream:38,
                 from /usr/include/c++/10/fstream:38,
                 from score-lm.cpp:23:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/score-lm.Tpo .deps/score-lm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o score-lm score-lm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o score-lm score-lm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT tlm.o -MD -MP -MF .deps/tlm.Tpo -c -o tlm.o tlm.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from tlm.cpp:26:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from tlm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from tlm.cpp:26:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from tlm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from tlm.cpp:26:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from tlm.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
tlm.cpp: In function ‘int main(int, char**)’:
tlm.cpp:317:12: warning: this statement may fall through [-Wimplicit-fallthrough=]
  317 |    cerr << "ModifiedShiftBeta (msb) is the old name for ImprovedKneserNey (ikn); this name is not supported anymore, but it is mapped into ImprovedKneserNey for back-compatibility";
      |            ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
tlm.cpp:318:3: note: here
  318 |   case IMPROVED_KNESER_NEY:
      |   ^~~~
tlm.cpp:529:12: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  529 |      system("echo > .tlmlock");
      |      ~~~~~~^~~~~~~~~~~~~~~~~~~
tlm.cpp:543:12: warning: ignoring return value of ‘int system(const char*)’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  543 |      system("rm .tlmlock");
      |      ~~~~~~^~~~~~~~~~~~~~~
mv -f .deps/tlm.Tpo .deps/tlm.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o tlm tlm.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o tlm tlm.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT plsa.o -MD -MP -MF .deps/plsa.Tpo -c -o plsa.o plsa.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from plsa.cpp:27:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from plsa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from plsa.cpp:27:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from plsa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from plsa.cpp:27:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from plsa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/plsa.Tpo .deps/plsa.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o plsa plsa.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o plsa plsa.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT verify-caching.o -MD -MP -MF .deps/verify-caching.Tpo -c -o verify-caching.o verify-caching.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from dictionary.h:26,
                 from normcache.h:24,
                 from mdiadapt.h:27,
                 from verify-caching.cpp:29:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from verify-caching.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from normcache.h:24,
                 from mdiadapt.h:27,
                 from verify-caching.cpp:29:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from verify-caching.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from dictionary.h:26,
                 from normcache.h:24,
                 from mdiadapt.h:27,
                 from verify-caching.cpp:29:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from verify-caching.cpp:24:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/verify-caching.Tpo .deps/verify-caching.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o verify-caching verify-caching.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o verify-caching verify-caching.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
g++ -DHAVE_CONFIG_H -I. -I..   -DTRACE_LEVEL=1 -DMY_ASSERT_FLAG -DHAVE_CXX0 -std=c++0x -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2 -MT cswa.o -MD -MP -MF .deps/cswa.Tpo -c -o cswa.o cswa.cpp
g++: warning: switch ‘-ffor-scope’ is no longer supported
In file included from cswa.cpp:27:
mfstream.h:193:61: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  193 |   mfstream& iwritex(streampos loc,void *ptr,int size,int n=1);
      |                                                             ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from cswa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cswa.cpp:27:
mfstream.h:196:19: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  196 |   streampos tellp();
      |                   ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from cswa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
In file included from cswa.cpp:27:
mfstream.h:199:32: warning: ‘std::ios_base::streampos’ is deprecated: use 'std::streampos' instead [-Wdeprecated-declarations]
  199 |   mfstream& seekp(streampos loc);
      |                                ^
In file included from /usr/include/c++/10/ios:42,
                 from /usr/include/c++/10/ostream:38,
                 from /usr/include/c++/10/iostream:39,
                 from cswa.cpp:22:
/usr/include/c++/10/bits/ios_base.h:481:28: note: declared here
  481 |     typedef std::streampos streampos
      |                            ^~~~~~~~~
mv -f .deps/cswa.Tpo .deps/cswa.Po
/bin/bash ../libtool  --tag=CXX   --mode=link g++ -static -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES  -DMYCODESIZE=3 -g -O2   -o cswa cswa.o -lirstlm -lpthread -lz
libtool: link: g++ -I/usr/include -W -Wall -ffor-scope -D_FILE_OFFSET_BITS=64 -D_LARGE_FILES -DMYCODESIZE=3 -g -O2 -o cswa cswa.o   /home/ye/tool/irstlm/src/.libs/libirstlm.a -lpthread -lz
g++: warning: switch '-ffor-scope' is no longer supported
make[2]: Leaving directory '/home/ye/tool/irstlm/src'
Making all in scripts
make[2]: Entering directory '/home/ye/tool/irstlm/scripts'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/irstlm/scripts'
Making all in doc
make[2]: Entering directory '/home/ye/tool/irstlm/doc'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/irstlm/doc'
make[2]: Entering directory '/home/ye/tool/irstlm'
make[2]: Leaving directory '/home/ye/tool/irstlm'
make[1]: Leaving directory '/home/ye/tool/irstlm'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## make install

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$ sudo make install
[sudo] password for ye: 
Making install in src
make[1]: Entering directory '/home/ye/tool/irstlm/src'
make[2]: Entering directory '/home/ye/tool/irstlm/src'
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   libirstlm.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/libirstlm.lai /usr/local/lib/libirstlm.la
libtool: install: /usr/bin/install -c .libs/libirstlm.a /usr/local/lib/libirstlm.a
libtool: install: chmod 644 /usr/local/lib/libirstlm.a
libtool: install: ranlib /usr/local/lib/libirstlm.a
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /usr/local/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /usr/local/lib

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the '-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the 'LD_RUN_PATH' environment variable
     during linking
   - use the '-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c dict ngt dtsel compile-lm interpolate-lm prune-lm quantize-lm prune-lm score-lm tlm plsa verify-caching cswa '/usr/local/bin'
libtool: install: /usr/bin/install -c dict /usr/local/bin/dict
libtool: install: /usr/bin/install -c ngt /usr/local/bin/ngt
libtool: install: /usr/bin/install -c dtsel /usr/local/bin/dtsel
libtool: install: /usr/bin/install -c compile-lm /usr/local/bin/compile-lm
libtool: install: /usr/bin/install -c interpolate-lm /usr/local/bin/interpolate-lm
libtool: install: /usr/bin/install -c prune-lm /usr/local/bin/prune-lm
libtool: install: /usr/bin/install -c quantize-lm /usr/local/bin/quantize-lm
libtool: install: /usr/bin/install -c prune-lm /usr/local/bin/prune-lm
libtool: install: /usr/bin/install -c score-lm /usr/local/bin/score-lm
libtool: install: /usr/bin/install -c tlm /usr/local/bin/tlm
libtool: install: /usr/bin/install -c plsa /usr/local/bin/plsa
libtool: install: /usr/bin/install -c verify-caching /usr/local/bin/verify-caching
libtool: install: /usr/bin/install -c cswa /usr/local/bin/cswa
 /usr/bin/mkdir -p '/usr/local/include'
 /usr/bin/install -c -m 644 cmd.h thpool.h dictionary.h gzfilebuf.h htable.h index.h lmContainer.h lmclass.h lmmacro.h lmtable.h lmInterpolation.h mempool.h mfstream.h n_gram.h ngramcache.h ngramtable.h timer.h util.h crc.h interplm.h linearlm.h mdiadapt.h mixture.h normcache.h shiftlm.h cplsa.h cswam.h doc.h '/usr/local/include'
make[2]: Leaving directory '/home/ye/tool/irstlm/src'
make[1]: Leaving directory '/home/ye/tool/irstlm/src'
Making install in scripts
make[1]: Entering directory '/home/ye/tool/irstlm/scripts'
make[2]: Entering directory '/home/ye/tool/irstlm/scripts'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/bin'
 /usr/bin/install -c add-start-end.sh build-lm-qsub.sh build-lm.sh rm-start-end.sh split-ngt.sh mdtsel.sh build-sublm.pl goograms2ngrams.pl lm-stat.pl merge-sublm.pl ngram-split.pl sort-lm.pl split-dict.pl plsa.sh '/usr/local/bin'
make[2]: Leaving directory '/home/ye/tool/irstlm/scripts'
make[1]: Leaving directory '/home/ye/tool/irstlm/scripts'
Making install in doc
make[1]: Entering directory '/home/ye/tool/irstlm/doc'
make[2]: Entering directory '/home/ye/tool/irstlm/doc'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Leaving directory '/home/ye/tool/irstlm/doc'
make[1]: Leaving directory '/home/ye/tool/irstlm/doc'
make[1]: Entering directory '/home/ye/tool/irstlm'
make[2]: Entering directory '/home/ye/tool/irstlm'
make  install-exec-hook
make[3]: Entering directory '/home/ye/tool/irstlm'
cd /usr/local/ && \
  ln -s -n -f lib lib64
make[3]: Leaving directory '/home/ye/tool/irstlm'
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/irstlm'
make[1]: Leaving directory '/home/ye/tool/irstlm'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm$
```

## How to build LM with IRSTLM

```
build-lm.sh -i TRAIN -n 3 -o iARPA_LM.gz -k 3 [-p]
```

Here, TRAIN is filename of the corpus.  

## Check these scripts

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/irstlm/scripts$ ls
add-start-end.sh  build-lm.sh     CMakeLists.txt      lm-stat.pl  Makefile.am  mdtsel.sh       ngram-split.pl  plsa.sh          sort-lm.pl     split-ngt.sh
build-lm-qsub.sh  build-sublm.pl  goograms2ngrams.pl  Makefile    Makefile.in  merge-sublm.pl  other           rm-start-end.sh  split-dict.pl  wrapper
```

## Reference

Paper:  
[https://www.researchgate.net/publication/221486318_IRSTLM_An_open_source_toolkit_for_handling_large_scale_language_models](https://www.researchgate.net/publication/221486318_IRSTLM_An_open_source_toolkit_for_handling_large_scale_language_models)  

A tutorial on the IRSTLM library:  
[https://pdfs.semanticscholar.org/12bc/c0548ed7f93e6675147e606b8bd98005ca5e.pdf](https://pdfs.semanticscholar.org/12bc/c0548ed7f93e6675147e606b8bd98005ca5e.pdf)  

