# Installation of libdatrie-0.2.11 (Double-Array Trie)

This library is useful and it is also required when you need SWATH Thai word segmenter.  
First download Double-Array Trie Library from the following link:  
[https://linux.thai.net/~thep/datrie/datrie.html](https://linux.thai.net/~thep/datrie/datrie.html)

## Untar

```bash
(base) ye@ykt-pro:~/tool$ tar -xf ./libdatrie-0.2.11.tar.xz 
(base) ye@ykt-pro:~/tool$ cd libdatrie-0.2.11/
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ ls
aclocal.m4  ChangeLog    configure.ac  datrie-0.2.pc.in  m4           man     README.migration  VERSION
AUTHORS     config.h.in  COPYING       doc               Makefile.am  NEWS    tests
build-aux   configure    datrie        INSTALL           Makefile.in  README  tools
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ 

(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
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
checking for style of include used by make... GNU
checking dependency style of gcc... gcc3
checking whether ln -s works... yes
checking whether make sets $(MAKE)... (cached) yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking how to print strings... printf
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
checking for dlltool... dlltool
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
checking whether linker supports -version-script... yes
checking for iconv_open... yes
checking for locale_charset in -liconv... no
checking for nl_langinfo (CODESET)... yes
checking for ANSI C header files... (cached) yes
checking limits.h usability... yes
checking limits.h presence... yes
checking for limits.h... yes
checking for stdlib.h... (cached) yes
checking stdio.h usability... yes
checking stdio.h presence... yes
checking for stdio.h... yes
checking for string.h... (cached) yes
checking for an ANSI C-conforming const... yes
checking for size_t... yes
checking for doxygen... no
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating datrie-0.2.pc
config.status: creating datrie/Makefile
config.status: creating tools/Makefile
config.status: creating man/Makefile
config.status: creating doc/Makefile
config.status: creating doc/Doxyfile
config.status: creating tests/Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
```bash

list the files:

```bash
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ ls
aclocal.m4  ChangeLog    config.log     configure.ac  datrie-0.2.pc     INSTALL  Makefile     man     README.migration  tools
AUTHORS     config.h     config.status  COPYING       datrie-0.2.pc.in  libtool  Makefile.am  NEWS    stamp-h1          VERSION
build-aux   config.h.in  configure      datrie        doc               m4       Makefile.in  README  tests
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ 
```

## run make

```bash
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ make
make  all-recursive
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11'
Making all in datrie
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/datrie'
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT dstring.lo -MD -MP -MF .deps/dstring.Tpo -c -o dstring.lo dstring.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT dstring.lo -MD -MP -MF .deps/dstring.Tpo -c dstring.c  -fPIC -DPIC -o .libs/dstring.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT dstring.lo -MD -MP -MF .deps/dstring.Tpo -c dstring.c -o dstring.o >/dev/null 2>&1
mv -f .deps/dstring.Tpo .deps/dstring.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT trie-string.lo -MD -MP -MF .deps/trie-string.Tpo -c -o trie-string.lo trie-string.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT trie-string.lo -MD -MP -MF .deps/trie-string.Tpo -c trie-string.c  -fPIC -DPIC -o .libs/trie-string.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT trie-string.lo -MD -MP -MF .deps/trie-string.Tpo -c trie-string.c -o trie-string.o >/dev/null 2>&1
mv -f .deps/trie-string.Tpo .deps/trie-string.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT fileutils.lo -MD -MP -MF .deps/fileutils.Tpo -c -o fileutils.lo fileutils.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT fileutils.lo -MD -MP -MF .deps/fileutils.Tpo -c fileutils.c  -fPIC -DPIC -o .libs/fileutils.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT fileutils.lo -MD -MP -MF .deps/fileutils.Tpo -c fileutils.c -o fileutils.o >/dev/null 2>&1
mv -f .deps/fileutils.Tpo .deps/fileutils.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT darray.lo -MD -MP -MF .deps/darray.Tpo -c -o darray.lo darray.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT darray.lo -MD -MP -MF .deps/darray.Tpo -c darray.c  -fPIC -DPIC -o .libs/darray.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT darray.lo -MD -MP -MF .deps/darray.Tpo -c darray.c -o darray.o >/dev/null 2>&1
mv -f .deps/darray.Tpo .deps/darray.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT tail.lo -MD -MP -MF .deps/tail.Tpo -c -o tail.lo tail.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT tail.lo -MD -MP -MF .deps/tail.Tpo -c tail.c  -fPIC -DPIC -o .libs/tail.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT tail.lo -MD -MP -MF .deps/tail.Tpo -c tail.c -o tail.o >/dev/null 2>&1
mv -f .deps/tail.Tpo .deps/tail.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT trie.lo -MD -MP -MF .deps/trie.Tpo -c -o trie.lo trie.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT trie.lo -MD -MP -MF .deps/trie.Tpo -c trie.c  -fPIC -DPIC -o .libs/trie.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT trie.lo -MD -MP -MF .deps/trie.Tpo -c trie.c -o trie.o >/dev/null 2>&1
mv -f .deps/trie.Tpo .deps/trie.Plo
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT alpha-map.lo -MD -MP -MF .deps/alpha-map.Tpo -c -o alpha-map.lo alpha-map.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT alpha-map.lo -MD -MP -MF .deps/alpha-map.Tpo -c alpha-map.c  -fPIC -DPIC -o .libs/alpha-map.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -g -O2 -MT alpha-map.lo -MD -MP -MF .deps/alpha-map.Tpo -c alpha-map.c -o alpha-map.o >/dev/null 2>&1
mv -f .deps/alpha-map.Tpo .deps/alpha-map.Plo
/bin/bash ../libtool  --tag=CC   --mode=link gcc  -g -O2 -no-undefined -version-info 4:4:3 -Wl,-version-script -Wl,./libdatrie.map  -o libdatrie.la -rpath /usr/local/lib dstring.lo trie-string.lo fileutils.lo darray.lo tail.lo trie.lo alpha-map.lo  
libtool: link: gcc -shared  -fPIC -DPIC  .libs/dstring.o .libs/trie-string.o .libs/fileutils.o .libs/darray.o .libs/tail.o .libs/trie.o .libs/alpha-map.o    -g -O2 -Wl,-version-script -Wl,./libdatrie.map   -Wl,-soname -Wl,libdatrie.so.1 -o .libs/libdatrie.so.1.3.4
libtool: link: (cd ".libs" && rm -f "libdatrie.so.1" && ln -s "libdatrie.so.1.3.4" "libdatrie.so.1")
libtool: link: (cd ".libs" && rm -f "libdatrie.so" && ln -s "libdatrie.so.1.3.4" "libdatrie.so")
libtool: link: ar cru .libs/libdatrie.a  dstring.o trie-string.o fileutils.o darray.o tail.o trie.o alpha-map.o
ar: `u' modifier ignored since `D' is the default (see `U')
libtool: link: ranlib .libs/libdatrie.a
libtool: link: ( cd ".libs" && rm -f "libdatrie.la" && ln -s "../libdatrie.la" "libdatrie.la" )
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/datrie'
Making all in tools
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tools'
gcc -DHAVE_CONFIG_H -I. -I..  -I..   -g -O2 -MT trietool.o -MD -MP -MF .deps/trietool.Tpo -c -o trietool.o trietool.c
mv -f .deps/trietool.Tpo .deps/trietool.Po
/bin/bash ../libtool  --tag=CC   --mode=link gcc  -g -O2   -o trietool trietool.o ../datrie/libdatrie.la  
libtool: link: gcc -g -O2 -o .libs/trietool trietool.o  ../datrie/.libs/libdatrie.so
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tools'
Making all in man
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/man'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/man'
Making all in doc
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/doc'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/doc'
Making all in tests
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11'
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11'
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ 
```

## run make install

```bash
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ sudo make install
[sudo] password for ye: 
Making install in datrie
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11/datrie'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/datrie'
 /bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   libdatrie.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/libdatrie.so.1.3.4 /usr/local/lib/libdatrie.so.1.3.4
libtool: install: (cd /usr/local/lib && { ln -s -f libdatrie.so.1.3.4 libdatrie.so.1 || { rm -f libdatrie.so.1 && ln -s libdatrie.so.1.3.4 libdatrie.so.1; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f libdatrie.so.1.3.4 libdatrie.so || { rm -f libdatrie.so && ln -s libdatrie.so.1.3.4 libdatrie.so; }; })
libtool: install: /usr/bin/install -c .libs/libdatrie.lai /usr/local/lib/libdatrie.la
libtool: install: /usr/bin/install -c .libs/libdatrie.a /usr/local/lib/libdatrie.a
libtool: install: chmod 644 /usr/local/lib/libdatrie.a
libtool: install: ranlib /usr/local/lib/libdatrie.a
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
 /bin/mkdir -p '/usr/local/include/datrie'
 /usr/bin/install -c -m 644 typedefs.h triedefs.h alpha-map.h trie.h '/usr/local/include/datrie'
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/datrie'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/datrie'
Making install in tools
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tools'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tools'
 /bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c trietool '/usr/local/bin'
libtool: install: /usr/bin/install -c .libs/trietool /usr/local/bin/trietool
make  install-data-hook
make[3]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tools'
rm -f /usr/local/bin/trietool-0.2
ln -s trietool /usr/local/bin/trietool-0.2
make[3]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tools'
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tools'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tools'
Making install in man
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11/man'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/man'
make[2]: Nothing to be done for 'install-exec-am'.
 /bin/mkdir -p '/usr/local/share/man/man1'
 /usr/bin/install -c -m 644 trietool.1 '/usr/local/share/man/man1'
make  install-data-hook
make[3]: Entering directory '/home/ye/tool/libdatrie-0.2.11/man'
rm -f /usr/local/share/man/man1/trietool-0.2.1
ln -s trietool.1 /usr/local/share/man/man1/trietool-0.2.1
make[3]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/man'
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/man'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/man'
Making install in doc
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11/doc'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/doc'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/doc'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/doc'
Making install in tests
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11/tests'
make[1]: Entering directory '/home/ye/tool/libdatrie-0.2.11'
make[2]: Entering directory '/home/ye/tool/libdatrie-0.2.11'
make[2]: Nothing to be done for 'install-exec-am'.
 /bin/mkdir -p '/usr/local/share/doc/libdatrie'
 /usr/bin/install -c -m 644 README.migration '/usr/local/share/doc/libdatrie'
 /bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 datrie-0.2.pc '/usr/local/lib/pkgconfig'
make[2]: Leaving directory '/home/ye/tool/libdatrie-0.2.11'
make[1]: Leaving directory '/home/ye/tool/libdatrie-0.2.11'
(base) ye@ykt-pro:~/tool/libdatrie-0.2.11$ 
```

**Fin library installation!
