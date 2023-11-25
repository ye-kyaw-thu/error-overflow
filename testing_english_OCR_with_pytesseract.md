# Testing English OCR with pytesseract

## Git Clone

```
(base) ye@lst-gpu-3090:~/tool$ git clone https://github.com/tesseract-ocr/tesseract
Cloning into 'tesseract'...
remote: Enumerating objects: 47193, done.
remote: Counting objects: 100% (580/580), done.
remote: Compressing objects: 100% (314/314), done.
remote: Total 47193 (delta 314), reused 415 (delta 259), pack-reused 46613
Receiving objects: 100% (47193/47193), 51.89 MiB | 12.02 MiB/s, done.
Resolving deltas: 100% (36830/36830), done.
```

## Run autogen.sh

```
(base) ye@lst-gpu-3090:~/tool$ cd tesseract/
(base) ye@lst-gpu-3090:~/tool/tesseract$ ./autogen.sh
Running aclocal
Running /usr/bin/libtoolize
libtoolize: putting auxiliary files in AC_CONFIG_AUX_DIR, 'config'.
libtoolize: copying file 'config/ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
Running aclocal
Running autoconf
Running autoheader
Running automake --add-missing --copy
configure.ac:425: installing 'config/compile'
configure.ac:89: installing 'config/config.guess'
configure.ac:89: installing 'config/config.sub'
configure.ac:27: installing 'config/install-sh'
configure.ac:27: installing 'config/missing'
Makefile.am: installing 'config/depcomp'
parallel-tests: installing 'config/test-driver'

All done.
To build the software now, do something like:

$ ./configure [--enable-debug] [...other options]
```

## Run ./configure

```
(base) ye@lst-gpu-3090:~/tool/tesseract$ ./configure --prefix=$HOME/local/
checking for g++... g++
checking whether the C++ compiler works... yes
checking for C++ compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether the compiler supports GNU C++... yes
checking whether g++ accepts -g... yes
checking for g++ option to enable C++11 features... none needed
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a race-free mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports the include directive... yes (GNU style)
checking whether make supports nested variables... yes
checking dependency style of g++... gcc3
checking for a sed that does not truncate output... /usr/bin/sed
checking Major version... 5
checking Minor version... 3
checking Point version... 3-30-gea0b
checking whether make supports nested variables... (cached) yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking whether C++ compiler accepts -Werror=unused-command-line-argument... no
checking whether C++ compiler accepts -mavx... yes
checking whether C++ compiler accepts -mavx2... yes
checking whether C++ compiler accepts -mavx512f... yes
checking whether C++ compiler accepts -mfma... yes
checking whether C++ compiler accepts -msse4.1... yes
checking for feenableexcept... yes
checking whether C++ compiler accepts -fopenmp-simd... yes
checking --enable-float32 argument...
checking --enable-graphics argument...
checking --enable-legacy argument...
checking for g++ option to support OpenMP... -fopenmp
checking for stdio.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for strings.h... yes
checking for sys/stat.h... yes
checking for sys/types.h... yes
checking for unistd.h... yes
checking for tiffio.h... no
checking --enable-opencl argument...
checking for tensorflow/core/framework/graph.pb.h... no
checking --enable-visibility argument...
checking whether to use tessdata-prefix... yes
checking if compiling with clang... no
checking whether to enable debugging...
checking how to print strings... printf
checking for gcc... gcc
checking whether the compiler supports GNU C... yes
checking whether gcc accepts -g... yes
checking for gcc option to enable C11 features... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking for a sed that does not truncate output... (cached) /usr/bin/sed
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
checking whether C++ compiler accepts -std=c++17... yes
checking whether C++ compiler accepts -std=c++20... yes
checking for library containing pthread_create... none required
checking for brew... false
checking for asciidoc... false
checking for xsltproc... true
checking for wchar_t... yes
checking for long long int... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for libcurl... no
checking for lept >= 1.74... no
configure: error: Leptonica 1.74 or higher is required. Try to install libleptonica-dev package.
(base) ye@lst-gpu-3090:~/tool/tesseract$ sudo apt-get install libleptonica-dev
[sudo] password for ye:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  liblept5
The following NEW packages will be installed:
  liblept5 libleptonica-dev
0 upgraded, 2 newly installed, 0 to remove and 14 not upgraded.
Need to get 2,668 kB of archives.
After this operation, 9,204 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 liblept5 amd64 1.82.0-3build1 [1,107 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libleptonica-dev amd64 1.82.0-3build1 [1,562 kB]
Fetched 2,668 kB in 1s (3,317 kB/s)
Selecting previously unselected package liblept5:amd64.
(Reading database ... 395266 files and directories currently installed.)
Preparing to unpack .../liblept5_1.82.0-3build1_amd64.deb ...
Unpacking liblept5:amd64 (1.82.0-3build1) ...
Selecting previously unselected package libleptonica-dev.
Preparing to unpack .../libleptonica-dev_1.82.0-3build1_amd64.deb ...
Unpacking libleptonica-dev (1.82.0-3build1) ...
Setting up liblept5:amd64 (1.82.0-3build1) ...
Setting up libleptonica-dev (1.82.0-3build1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.4) ...
(base) ye@lst-gpu-3090:~/tool/tesseract$ ./configure --prefix=$HOME/local/
checking for g++... g++
checking whether the C++ compiler works... yes
checking for C++ compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether the compiler supports GNU C++... yes
checking whether g++ accepts -g... yes
checking for g++ option to enable C++11 features... none needed
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a race-free mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports the include directive... yes (GNU style)
checking whether make supports nested variables... yes
checking dependency style of g++... gcc3
checking for a sed that does not truncate output... /usr/bin/sed
checking Major version... 5
checking Minor version... 3
checking Point version... 3-30-gea0b
checking whether make supports nested variables... (cached) yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking whether C++ compiler accepts -Werror=unused-command-line-argument... no
checking whether C++ compiler accepts -mavx... yes
checking whether C++ compiler accepts -mavx2... yes
checking whether C++ compiler accepts -mavx512f... yes
checking whether C++ compiler accepts -mfma... yes
checking whether C++ compiler accepts -msse4.1... yes
checking for feenableexcept... yes
checking whether C++ compiler accepts -fopenmp-simd... yes
checking --enable-float32 argument...
checking --enable-graphics argument...
checking --enable-legacy argument...
checking for g++ option to support OpenMP... -fopenmp
checking for stdio.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for strings.h... yes
checking for sys/stat.h... yes
checking for sys/types.h... yes
checking for unistd.h... yes
checking for tiffio.h... no
checking --enable-opencl argument...
checking for tensorflow/core/framework/graph.pb.h... no
checking --enable-visibility argument...
checking whether to use tessdata-prefix... yes
checking if compiling with clang... no
checking whether to enable debugging...
checking how to print strings... printf
checking for gcc... gcc
checking whether the compiler supports GNU C... yes
checking whether gcc accepts -g... yes
checking for gcc option to enable C11 features... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking for a sed that does not truncate output... (cached) /usr/bin/sed
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
checking whether C++ compiler accepts -std=c++17... yes
checking whether C++ compiler accepts -std=c++20... yes
checking for library containing pthread_create... none required
checking for brew... false
checking for asciidoc... false
checking for xsltproc... true
checking for wchar_t... yes
checking for long long int... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for libcurl... no
checking for lept >= 1.74... yes
checking for libarchive... no
checking for icu-uc >= 52.1... yes
checking for icu-i18n >= 52.1... yes
checking for pango >= 1.38.0... no
configure: WARNING: pango 1.38.0 or higher is required, but was not found.
configure: WARNING: Training tools WILL NOT be built.
configure: WARNING: Try to install libpango1.0-dev package.
checking for cairo... no
configure: WARNING: Training tools WILL NOT be built because of missing cairo library.
configure: WARNING: Try to install libcairo-dev?? package.
checking for pangocairo... no
checking for pangoft2... no
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating include/tesseract/version.h
config.status: creating Makefile
config.status: creating tesseract.pc
config.status: creating tessdata/Makefile
config.status: creating tessdata/configs/Makefile
config.status: creating tessdata/tessconfigs/Makefile
config.status: creating java/Makefile
config.status: creating java/com/Makefile
config.status: creating java/com/google/Makefile
config.status: creating java/com/google/scrollview/Makefile
config.status: creating java/com/google/scrollview/events/Makefile
config.status: creating java/com/google/scrollview/ui/Makefile
config.status: creating include/config_auto.h
config.status: executing depfiles commands
config.status: executing libtool commands

Configuration is done.
You can now build and install tesseract by running:

$ make
$ sudo make install
$ sudo ldconfig

Documentation will not be built because asciidoc or xsltproc is missing.

You cannot build training tools because of missing dependency.
Check configure output for details.

(base) ye@lst-gpu-3090:~/tool/tesseract$
```

## Run make

```
...
...
  CXX      src/ccutil/libtesseract_ccutil_la-unicharcompress.lo
  CXX      src/ccutil/libtesseract_ccutil_la-unicharmap.lo
  CXX      src/ccutil/libtesseract_ccutil_la-unicharset.lo
  CXX      src/ccutil/libtesseract_ccutil_la-params.lo
  CXX      src/ccutil/libtesseract_ccutil_la-ambigs.lo
  CXX      src/ccutil/libtesseract_ccutil_la-bitvector.lo
  CXX      src/ccutil/libtesseract_ccutil_la-indexmapbidi.lo
  CXXLD    libtesseract_ccutil.la
  CXX      src/lstm/libtesseract_lstm_la-convolve.lo
  CXX      src/lstm/libtesseract_lstm_la-fullyconnected.lo
  CXX      src/lstm/libtesseract_lstm_la-functions.lo
  CXX      src/lstm/libtesseract_lstm_la-input.lo
  CXX      src/lstm/libtesseract_lstm_la-lstm.lo
  CXX      src/lstm/libtesseract_lstm_la-lstmrecognizer.lo
  CXX      src/lstm/libtesseract_lstm_la-maxpool.lo
  CXX      src/lstm/libtesseract_lstm_la-network.lo
  CXX      src/lstm/libtesseract_lstm_la-networkio.lo
  CXX      src/lstm/libtesseract_lstm_la-parallel.lo
  CXX      src/lstm/libtesseract_lstm_la-plumbing.lo
  CXX      src/lstm/libtesseract_lstm_la-recodebeam.lo
  CXX      src/lstm/libtesseract_lstm_la-reconfig.lo
  CXX      src/lstm/libtesseract_lstm_la-reversed.lo
  CXX      src/lstm/libtesseract_lstm_la-series.lo
  CXX      src/lstm/libtesseract_lstm_la-stridemap.lo
  CXX      src/lstm/libtesseract_lstm_la-tfnetwork.lo
  CXX      src/lstm/libtesseract_lstm_la-weightmatrix.lo
  CXXLD    libtesseract_lstm.la
  CXX      src/arch/libtesseract_native_la-dotproduct.lo
  CXXLD    libtesseract_native.la
  CXX      src/arch/libtesseract_avx_la-dotproductavx.lo
  CXXLD    libtesseract_avx.la
  CXX      src/arch/libtesseract_avx2_la-intsimdmatrixavx2.lo
  CXXLD    libtesseract_avx2.la
  CXX      src/arch/libtesseract_avx512_la-dotproductavx512.lo
  CXXLD    libtesseract_avx512.la
  CXX      src/arch/libtesseract_fma_la-dotproductfma.lo
  CXXLD    libtesseract_fma.la
  CXX      src/arch/libtesseract_sse_la-dotproductsse.lo
  CXX      src/arch/libtesseract_sse_la-intsimdmatrixsse.lo
  CXXLD    libtesseract_sse.la
  CXXLD    libtesseract.la
  CXXLD    tesseract
make[1]: Leaving directory '/home/ye/tool/tesseract'
Making all in tessdata
make[1]: Entering directory '/home/ye/tool/tesseract/tessdata'
Making all in configs
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata/configs'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata/configs'
Making all in tessconfigs
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata'
make[2]: Nothing to be done for 'all-am'.
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata'
make[1]: Leaving directory '/home/ye/tool/tesseract/tessdata'
```

## Run make install

```
(base) ye@lst-gpu-3090:~/tool/tesseract$ make install
Making install in .
make[1]: Entering directory '/home/ye/tool/tesseract'
make[2]: Entering directory '/home/ye/tool/tesseract'
 /usr/bin/mkdir -p '/home/ye/local/lib'
 /bin/bash ./libtool   --mode=install /usr/bin/install -c   libtesseract.la '/home/ye/local/lib'
libtool: install: /usr/bin/install -c .libs/libtesseract.so.5.0.3 /home/ye/local/lib/libtesseract.so.5.0.3
libtool: install: (cd /home/ye/local/lib && { ln -s -f libtesseract.so.5.0.3 libtesseract.so.5 || { rm -f libtesseract.so.5 && ln -s libtesseract.so.5.0.3 libtesseract.so.5; }; })
libtool: install: (cd /home/ye/local/lib && { ln -s -f libtesseract.so.5.0.3 libtesseract.so || { rm -f libtesseract.so && ln -s libtesseract.so.5.0.3 libtesseract.so; }; })
libtool: install: /usr/bin/install -c .libs/libtesseract.lai /home/ye/local/lib/libtesseract.la
libtool: install: /usr/bin/install -c .libs/libtesseract.a /home/ye/local/lib/libtesseract.a
libtool: install: chmod 644 /home/ye/local/lib/libtesseract.a
libtool: install: ranlib /home/ye/local/lib/libtesseract.a
libtool: finish: PATH="/home/ye/.local/bin:/home/ye/anaconda3/bin:/home/ye/anaconda3/condabin:/home/ye/tool/SCTK/bin:/usr/local/cuda-11.8/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/ye/tool/julia-1.8.1/bin:/home/ye/tool/kenlm/build/bin:/sbin" ldconfig -n /home/ye/local/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /home/ye/local/lib

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
 /usr/bin/mkdir -p '/home/ye/local/bin'
  /bin/bash ./libtool   --mode=install /usr/bin/install -c tesseract '/home/ye/local/bin'
libtool: install: /usr/bin/install -c .libs/tesseract /home/ye/local/bin/tesseract
 /usr/bin/mkdir -p '/home/ye/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 tesseract.pc '/home/ye/local/lib/pkgconfig'
 /usr/bin/mkdir -p '/home/ye/local/include/tesseract'
 /usr/bin/install -c -m 644 ./include/tesseract/version.h include/tesseract/baseapi.h include/tesseract/capi.h include/tesseract/export.h include/tesseract/ltrresultiterator.h include/tesseract/ocrclass.h include/tesseract/osdetect.h include/tesseract/pageiterator.h include/tesseract/publictypes.h include/tesseract/renderer.h include/tesseract/resultiterator.h include/tesseract/unichar.h '/home/ye/local/include/tesseract'
make[2]: Leaving directory '/home/ye/tool/tesseract'
make[1]: Leaving directory '/home/ye/tool/tesseract'
Making install in tessdata
make[1]: Entering directory '/home/ye/tool/tesseract/tessdata'
Making install in configs
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata/configs'
make[3]: Entering directory '/home/ye/tool/tesseract/tessdata/configs'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/home/ye/local/share/tessdata/configs'
 /usr/bin/install -c -m 644 inter makebox box.train unlv ambigs.train lstm.train lstmdebug api_config kannada box.train.stderr quiet logfile digits get.images lstmbox wordstrbox alto hocr pdf tsv txt linebox rebox strokewidth bigram '/home/ye/local/share/tessdata/configs'
make[3]: Leaving directory '/home/ye/tool/tesseract/tessdata/configs'
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata/configs'
Making install in tessconfigs
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[3]: Entering directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/home/ye/local/share/tessdata/tessconfigs'
 /usr/bin/install -c -m 644 batch batch.nochop nobatch matdemo segdemo msdemo '/home/ye/local/share/tessdata/tessconfigs'
make[3]: Leaving directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata/tessconfigs'
make[2]: Entering directory '/home/ye/tool/tesseract/tessdata'
make[3]: Entering directory '/home/ye/tool/tesseract/tessdata'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/home/ye/local/share/tessdata'
 /usr/bin/install -c -m 644 pdf.ttf '/home/ye/local/share/tessdata'
make[3]: Leaving directory '/home/ye/tool/tesseract/tessdata'
make[2]: Leaving directory '/home/ye/tool/tesseract/tessdata'
make[1]: Leaving directory '/home/ye/tool/tesseract/tessdata'
(base) ye@lst-gpu-3090:~/tool/tesseract$
```

## Install Python Module

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ pip install pytesseract
Collecting pytesseract
  Downloading pytesseract-0.3.10-py3-none-any.whl (14 kB)
Requirement already satisfied: packaging>=21.3 in /home/ye/anaconda3/lib/python3.9/site-packages (from pytesseract) (21.3)
Requirement already satisfied: Pillow>=8.0.0 in /home/ye/anaconda3/lib/python3.9/site-packages (from pytesseract) (9.0.1)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/lib/python3.9/site-packages (from packaging>=21.3->pytesseract) (3.0.4)
Installing collected packages: pytesseract
Successfully installed pytesseract-0.3.10
(base) ye@lst-gpu-3090:~/tool/tesseract/y$
```

## Add path

```
(base) ye@lst-gpu-3090:~/tool/tesseract$ sudo nano ~/.bashrc
```

```
#for Tesseract
export PATH="$PATH:/home/ye/tool/tesseract";
```

run source...  

```
(base) ye@lst-gpu-3090:~/tool/tesseract$ source ~/.bashrc
(base) ye@lst-gpu-3090:~/tool/tesseract$ which tesseract
/home/ye/tool/tesseract/tesseract
(base) ye@lst-gpu-3090:~/tool/tesseract$
```

## Coding for English

```python
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## for testing English OCR
## last updated: 25 Nov 2023

import argparse
import pytesseract
from PIL import Image

def perform_ocr(image_path):
    """
    Perform OCR on an image file and return the extracted text.

    :param image_path: Path to the image file.
    :return: Extracted text as a string.
    """
    try:
        # Load the image from the given path
        image = Image.open(image_path)

        # Perform OCR using Tesseract
        extracted_text = pytesseract.image_to_string(image, lang='eng')

        return extracted_text
    except Exception as e:
        return f"An error occurred: {str(e)}"

def main():
    # Create the parser
    parser = argparse.ArgumentParser(description='OCR Script to extract text from an image.')

    # Add the arguments
    parser.add_argument('image_path', type=str, help='Path to the image file.')
    parser.add_argument('-o', '--output', type=str, help='Output file to save the extracted text.')

    # Execute the parse_args() method
    args = parser.parse_args()

    extracted_text = perform_ocr(args.image_path)

    if args.output:
        # If output file is specified, write the text to the file
        with open(args.output, 'w') as file:
            file.write(extracted_text)
        print(f"Extracted text written to {args.output}")
    else:
        # Otherwise, print the text
        print("Extracted Text:\n", extracted_text)

if __name__ == "__main__":
    main()
```

## Called --help

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ python ./en_ocr.py --help
usage: en_ocr.py [-h] [-o OUTPUT] image_path

OCR Script to extract text from an image.

positional arguments:
  image_path            Path to the image file.

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Output file to save the extracted text.
```
					
## Testing

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ time python ./en_ocr.py
Extracted Text:
 An error occurred: (1, 'Error opening data file /home/ye/local/share/tessdata/eng.traineddata Please make sure the TESSDATA_PREFIX environment variable is set to your "tessdata" directory. Failed loading language \'eng\' Tesseract couldn\'t load any languages! Could not initialize tesseract.')

real    0m0.216s
user    0m0.815s
sys     0m1.955s
(base) ye@lst-gpu-3090:~/tool/tesseract/y$
```

Error fixing ...  

```
export TESSDATA_PREFIX=/home/ye/tool/tesseract/tessdata;
```

```
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ (base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ source ~/.bashrc
```

Run again ...  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ time python ./en_ocr.py
Extracted Text:
 An error occurred: (1, 'Error opening data file /home/ye/tool/tesseract/tessdata/eng.traineddata Please make sure the TESSDATA_PREFIX environment variable is set to your "tessdata" directory. Failed loading language \'eng\' Tesseract couldn\'t load any languages! Could not initialize tesseract.')

real    0m0.234s
user    0m0.835s
sys     0m1.953s
```

Check the data folder:  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ ls
configs            eng.user-words  Makefile.am  pdf.ttf
eng.user-patterns  Makefile        Makefile.in  tessconfigs
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$
```

I need to download languge data file ...  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ wget https://github.com/tesseract-ocr/tessdata/raw/main/eng.traineddata -P /home/ye/tool/tesseract/tessdata/
--2023-11-25 16:02:55--  https://github.com/tesseract-ocr/tessdata/raw/main/eng.traineddata
Resolving github.com (github.com)... 20.205.243.166
Connecting to github.com (github.com)|20.205.243.166|:443... connected.
HTTP request sent, awaiting response...
302 Found
Location: https://raw.githubusercontent.com/tesseract-ocr/tessdata/main/eng.traineddata [following]
--2023-11-25 16:02:55--  https://raw.githubusercontent.com/tesseract-ocr/tessdata/main/eng.traineddata
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.108.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 23466654 (22M) [application/octet-stream]
Saving to: ‘/home/ye/tool/tesseract/tessdata/eng.traineddata’

eng.traineddata        100%[==========================>]  22.38M  31.4MB/s    in 0.7s

2023-11-25 16:02:58 (31.4 MB/s) - ‘/home/ye/tool/tesseract/tessdata/eng.traineddata’ saved [23466654/23466654]

(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$
```

check the folder again:  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ ls
configs          eng.user-patterns  Makefile     Makefile.in  tessconfigs
eng.traineddata  eng.user-words     Makefile.am  pdf.ttf
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$
```

Run again ... Now I can run it.   

## Results

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ python ./en_ocr.py ./ws_program.png
Extracted Text:
 WS2 : Development of Synthesized Speech with a Focus on The Issue of
Prosodic Elongation

Aphiwich Sangpet and Natthapol Kritsuthikul

WS3 : Myanmar Hate Speech Generation Using GPT-2: A Novel Technique for
Corpus Expansion

Nang Aeindray Kyaw, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha,
Manabu Okumura

WS4 : myNER9: Development, Manual Annotation, and Evaluation of a 9-Tag
Myanmar NER Corpus via XGBoost and Bi-LSTM

Kaung Lwin Thant, Ye Kyaw Thu, Thazin Myint Oo, Kwankamol Nongpong

WS5 : Myanmar Spelling Error Classification: An Empirical Study of Tsetlin
Machine Techniques

Ei Thandar Phyu, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha

```

output ဖိုင် ထုတ်ကြည့်မယ်။  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ python ./en_ocr.py ./ws_program.png -o output.txt
Extracted text written to output.txt
```

ထွက်လာတဲ့ဖိုင်ကို စစ်ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ cat output.txt
WS2 : Development of Synthesized Speech with a Focus on The Issue of
Prosodic Elongation

Aphiwich Sangpet and Natthapol Kritsuthikul

WS3 : Myanmar Hate Speech Generation Using GPT-2: A Novel Technique for
Corpus Expansion

Nang Aeindray Kyaw, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha,
Manabu Okumura

WS4 : myNER9: Development, Manual Annotation, and Evaluation of a 9-Tag
Myanmar NER Corpus via XGBoost and Bi-LSTM

Kaung Lwin Thant, Ye Kyaw Thu, Thazin Myint Oo, Kwankamol Nongpong

WS5 : Myanmar Spelling Error Classification: An Empirical Study of Tsetlin
Machine Techniques

Ei Thandar Phyu, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha

(base) ye@lst-gpu-3090:~/tool/tesseract/y$

```

