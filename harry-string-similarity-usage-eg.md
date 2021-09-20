
# git clone

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/rieck/harry
Cloning into 'harry'...
remote: Enumerating objects: 3775, done.
remote: Total 3775 (delta 0), reused 0 (delta 0), pack-reused 3775
Receiving objects: 100% (3775/3775), 4.14 MiB | 13.20 MiB/s, done.
Resolving deltas: 100% (2917/2917), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd harry/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ ls
bootstrap  build  configure.ac  COPYING  doc  examples  git2changes.py  harry.png  m4  Makefile.am  pedantic  python  README.md  src  tests
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

#  run bootstrap


```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ ./bootstrap 
libtoolize: putting auxiliary files in '.'.
libtoolize: linking file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: linking file 'm4/libtool.m4'
libtoolize: linking file 'm4/ltoptions.m4'
libtoolize: linking file 'm4/ltsugar.m4'
libtoolize: linking file 'm4/ltversion.m4'
libtoolize: linking file 'm4/lt~obsolete.m4'
configure.ac:17: installing './compile'
configure.ac:18: installing './config.guess'
configure.ac:18: installing './config.sub'
configure.ac:13: installing './install-sh'
configure.ac:13: installing './missing'
python/Makefile.am:16: installing './py-compile'
src/Makefile.am: installing './depcomp'
parallel-tests: installing './test-driver'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

# Insallation

Linux/Unix OS မှာ installation လုပ်နေကြထုံးစံအတိုင်း, 
./configure, make, make install နဲ့ သွားမယ်။   

ပထမဦးဆုံး  
run ./configure  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ ./configure

  Harry - A Tool for Measuring String Similarity
  Copyright (c) 2013-2016 Konrad Rieck (konrad@mlsec.org)

checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
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
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for fgrep... /usr/bin/grep -F
checking how to print strings... printf
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
checking for python... /home/ye/anaconda3/bin/python
checking for python version... 3.7
checking for python platform... linux
checking for python script directory... ${prefix}/lib/python3.7/site-packages
checking for python extension module directory... ${exec_prefix}/lib/python3.7/site-packages
checking zlib.h usability... yes
checking zlib.h presence... yes
checking for zlib.h... yes
checking for gzopen in -lz... yes
checking archive.h usability... no
checking archive.h presence... no
checking for archive.h... no
checking for archive_read_new in -larchive... no
checking libconfig.h usability... no
checking libconfig.h presence... no
checking for libconfig.h... no
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for PKGCONFIG... configure: error: Package requirements (libconfig >= 1.3.2) were not met:

No package 'libconfig' found

Consider adjusting the PKG_CONFIG_PATH environment variable if you
installed software in a non-standard prefix.

Alternatively, you may set the environment variables PKGCONFIG_CFLAGS
and PKGCONFIG_LIBS to avoid the need to call pkg-config.
See the pkg-config man page for more details.

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

ပေးနေတဲ့ error က libconfig ဆိုတဲ့ pkg မရှိဘူးတဲ့ ...  

## Got libconfig not found error

libconfig-dev ကို အောက်ပါအတိုင်း installation လုပ်ခဲ့ ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ sudo apt-get install -y libconfig-dev
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
  python3-colorama python3-dateutil python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libconfig-doc libconfig9
The following NEW packages will be installed:
  libconfig-dev libconfig-doc libconfig9
0 upgraded, 3 newly installed, 0 to remove and 63 not upgraded.
Need to get 380 kB of archives.
After this operation, 527 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libconfig9 amd64 1.5-0.4build1 [22.3 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libconfig-dev amd64 1.5-0.4build1 [51.7 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libconfig-doc all 1.5-0.4build1 [306 kB]
Fetched 380 kB in 2s (209 kB/s)        
Selecting previously unselected package libconfig9:amd64.
(Reading database ... 656796 files and directories currently installed.)
Preparing to unpack .../libconfig9_1.5-0.4build1_amd64.deb ...
Unpacking libconfig9:amd64 (1.5-0.4build1) ...
Selecting previously unselected package libconfig-dev:amd64.
Preparing to unpack .../libconfig-dev_1.5-0.4build1_amd64.deb ...
Unpacking libconfig-dev:amd64 (1.5-0.4build1) ...
Selecting previously unselected package libconfig-doc.
Preparing to unpack .../libconfig-doc_1.5-0.4build1_all.deb ...
Unpacking libconfig-doc (1.5-0.4build1) ...
Setting up libconfig9:amd64 (1.5-0.4build1) ...
Setting up libconfig-doc (1.5-0.4build1) ...
Setting up libconfig-dev:amd64 (1.5-0.4build1) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
install-info: warning: no info dir entry in `/usr/share/info/automake-history.info.gz'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

## run ./configure again

ဒီတစ်ခါ ./configure ကတော့ အဆင်ပြေရမယ် ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ ./configure

  Harry - A Tool for Measuring String Similarity
  Copyright (c) 2013-2016 Konrad Rieck (konrad@mlsec.org)

checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
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
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for fgrep... /usr/bin/grep -F
checking how to print strings... printf
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
checking for python... /home/ye/anaconda3/bin/python
checking for python version... 3.7
checking for python platform... linux
checking for python script directory... ${prefix}/lib/python3.7/site-packages
checking for python extension module directory... ${exec_prefix}/lib/python3.7/site-packages
checking zlib.h usability... yes
checking zlib.h presence... yes
checking for zlib.h... yes
checking for gzopen in -lz... yes
checking archive.h usability... no
checking archive.h presence... no
checking for archive.h... no
checking for archive_read_new in -larchive... no
checking libconfig.h usability... yes
checking libconfig.h presence... yes
checking for libconfig.h... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for PKGCONFIG... yes
checking omp.h usability... yes
checking omp.h presence... yes
checking for omp.h... yes
checking for OpenMP flag of C compiler... -fopenmp
checking pthread.h usability... yes
checking pthread.h presence... yes
checking for pthread.h... yes
checking for pthread_rwlock_init in -lpthread... yes
checking getopt.h usability... yes
checking getopt.h presence... yes
checking for getopt.h... yes
checking for string.h... (cached) yes
checking for strings.h... (cached) yes
checking regex.h usability... yes
checking regex.h presence... yes
checking for regex.h... yes
checking uthash.h usability... no
checking uthash.h presence... no
checking for uthash.h... no
checking uthash/uthash.h usability... no
checking uthash/uthash.h presence... no
checking for uthash/uthash.h... no
checking for log2... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/measures/Makefile
config.status: creating src/input/Makefile
config.status: creating src/output/Makefile
config.status: creating python/Makefile
config.status: creating tests/Makefile
config.status: creating doc/Makefile
config.status: creating examples/Makefile
config.status: creating examples/alexa/Makefile
config.status: creating examples/reuters/Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands

 .Oo Optional packages:
     Support for reading archives (--with-libarchive):       no
     Support for multi-processing (--with-openmp):           yes
     Support for POSIX threads and locks (--with-pthreads):  yes
 .Oo Optional features:
     POSIX read-write lock (--enable-prwlock):               no
     MD5 as alternative hash (--enable-md5hash):             no

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

## run make


run make:   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ make
...
...
...
/usr/include/features.h:187:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
mv -f .deps/dist_kernel.Tpo .deps/dist_kernel.Po
/bin/bash ../libtool  --tag=CC   --mode=link gcc  -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC  -fopenmp    -o check_kernel dist_kernel.o ../src/libharry.la -lpthread -lz  -lm -lconfig
libtool: link: gcc -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC -fopenmp -o check_kernel dist_kernel.o   ../src/.libs/libharry.a -lpthread -lz -lm -lconfig -fopenmp
gcc -DHAVE_CONFIG_H -I. -I..  -I../src -I../src/measures   -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC  -fopenmp  -MT kern_spectrum.o -MD -MP -MF .deps/kern_spectrum.Tpo -c -o kern_spectrum.o kern_spectrum.c
In file included from /usr/include/x86_64-linux-gnu/sys/time.h:21,
                 from ../src/common.h:23,
                 from kern_spectrum.c:13:
/usr/include/features.h:187:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
mv -f .deps/kern_spectrum.Tpo .deps/kern_spectrum.Po
/bin/bash ../libtool  --tag=CC   --mode=link gcc  -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC  -fopenmp    -o check_spectrum kern_spectrum.o ../src/libharry.la -lpthread -lz  -lm -lconfig
libtool: link: gcc -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC -fopenmp -o check_spectrum kern_spectrum.o   ../src/.libs/libharry.a -lpthread -lz -lm -lconfig -fopenmp
gcc -DHAVE_CONFIG_H -I. -I..  -I../src -I../src/measures   -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC  -fopenmp  -MT dist_osa.o -MD -MP -MF .deps/dist_osa.Tpo -c -o dist_osa.o dist_osa.c
In file included from /usr/include/x86_64-linux-gnu/sys/time.h:21,
                 from ../src/common.h:23,
                 from dist_osa.c:13:
/usr/include/features.h:187:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
mv -f .deps/dist_osa.Tpo .deps/dist_osa.Po
/bin/bash ../libtool  --tag=CC   --mode=link gcc  -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC  -fopenmp    -o check_osa dist_osa.o ../src/libharry.la -lpthread -lz  -lm -lconfig
libtool: link: gcc -g -O2 -DNDEBUG -std=c99 -fgnu89-inline -Wall -fPIC -fopenmp -o check_osa dist_osa.o   ../src/.libs/libharry.a -lpthread -lz -lm -lconfig -fopenmp
make[2]: Leaving directory '/home/ye/tool/harry/tests'
make[1]: Leaving directory '/home/ye/tool/harry'
```

## make check

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ make check
Making check in src
make[1]: Entering directory '/home/ye/tool/harry/src'
Making check in measures
make[2]: Entering directory '/home/ye/tool/harry/src/measures'
make[2]: Nothing to be done for 'check'.
make[2]: Leaving directory '/home/ye/tool/harry/src/measures'
Making check in input
make[2]: Entering directory '/home/ye/tool/harry/src/input'
make[2]: Nothing to be done for 'check'.
make[2]: Leaving directory '/home/ye/tool/harry/src/input'
Making check in output
make[2]: Entering directory '/home/ye/tool/harry/src/output'
make[2]: Nothing to be done for 'check'.
make[2]: Leaving directory '/home/ye/tool/harry/src/output'
make[2]: Entering directory '/home/ye/tool/harry/src'
make[2]: Nothing to be done for 'check-am'.
make[2]: Leaving directory '/home/ye/tool/harry/src'
make[1]: Leaving directory '/home/ye/tool/harry/src'
Making check in doc
make[1]: Entering directory '/home/ye/tool/harry/doc'
make[1]: Nothing to be done for 'check'.
make[1]: Leaving directory '/home/ye/tool/harry/doc'
Making check in examples
make[1]: Entering directory '/home/ye/tool/harry/examples'
Making check in alexa
make[2]: Entering directory '/home/ye/tool/harry/examples/alexa'
make[2]: Nothing to be done for 'check'.
make[2]: Leaving directory '/home/ye/tool/harry/examples/alexa'
Making check in reuters
make[2]: Entering directory '/home/ye/tool/harry/examples/reuters'
make[2]: Nothing to be done for 'check'.
make[2]: Leaving directory '/home/ye/tool/harry/examples/reuters'
Making check in .
make[2]: Entering directory '/home/ye/tool/harry/examples'
make[2]: Nothing to be done for 'check-am'.
make[2]: Leaving directory '/home/ye/tool/harry/examples'
make[1]: Leaving directory '/home/ye/tool/harry/examples'
Making check in python
make[1]: Entering directory '/home/ye/tool/harry/python'
make  check-local
make[2]: Entering directory '/home/ye/tool/harry/python'
make[2]: Nothing to be done for 'check-local'.
make[2]: Leaving directory '/home/ye/tool/harry/python'
make[1]: Leaving directory '/home/ye/tool/harry/python'
Making check in .
make[1]: Entering directory '/home/ye/tool/harry'
make[1]: Nothing to be done for 'check-am'.
make[1]: Leaving directory '/home/ye/tool/harry'
Making check in tests
make[1]: Entering directory '/home/ye/tool/harry/tests'
make  check_vcache check_levenshtein check_hamming check_jarowinkler check_lee check_damerau check_compression check_wdegree check_subsequence check_bag check_coefficient check_distance check_kernel check_spectrum check_osa
make[2]: Entering directory '/home/ye/tool/harry/tests'
make[2]: 'check_vcache' is up to date.
make[2]: 'check_levenshtein' is up to date.
make[2]: 'check_hamming' is up to date.
make[2]: 'check_jarowinkler' is up to date.
make[2]: 'check_lee' is up to date.
make[2]: 'check_damerau' is up to date.
make[2]: 'check_compression' is up to date.
make[2]: 'check_wdegree' is up to date.
make[2]: 'check_subsequence' is up to date.
make[2]: 'check_bag' is up to date.
make[2]: 'check_coefficient' is up to date.
make[2]: 'check_distance' is up to date.
make[2]: 'check_kernel' is up to date.
make[2]: 'check_spectrum' is up to date.
make[2]: 'check_osa' is up to date.
make[2]: Leaving directory '/home/ye/tool/harry/tests'
make  check-TESTS
make[2]: Entering directory '/home/ye/tool/harry/tests'
make[3]: Entering directory '/home/ye/tool/harry/tests'
PASS: check_vcache
PASS: check_levenshtein
PASS: check_hamming
PASS: check_jarowinkler
PASS: check_lee
PASS: check_damerau
PASS: check_compression
PASS: check_wdegree
PASS: check_subsequence
PASS: check_bag
PASS: check_coefficient
PASS: check_distance
PASS: check_kernel
PASS: check_spectrum
PASS: check_osa
PASS: check_measures.sh
PASS: check_options.sh
PASS: check_configs.sh
PASS: check_inputs.sh
SKIP: check_python.py
SKIP: check_pylev.py
============================================================================
Testsuite summary for harry 0.4.3
============================================================================
# TOTAL: 21
# PASS:  19
# SKIP:  2
# XFAIL: 0
# FAIL:  0
# XPASS: 0
# ERROR: 0
============================================================================
make[3]: Leaving directory '/home/ye/tool/harry/tests'
make[2]: Leaving directory '/home/ye/tool/harry/tests'
make[1]: Leaving directory '/home/ye/tool/harry/tests'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 

```

## make install

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ sudo make install
Making install in src
make[1]: Entering directory '/home/ye/tool/harry/src'
Making install in measures
make[2]: Entering directory '/home/ye/tool/harry/src/measures'
make[3]: Entering directory '/home/ye/tool/harry/src/measures'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/home/ye/tool/harry/src/measures'
make[2]: Leaving directory '/home/ye/tool/harry/src/measures'
Making install in input
make[2]: Entering directory '/home/ye/tool/harry/src/input'
make[3]: Entering directory '/home/ye/tool/harry/src/input'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/home/ye/tool/harry/src/input'
make[2]: Leaving directory '/home/ye/tool/harry/src/input'
Making install in output
make[2]: Entering directory '/home/ye/tool/harry/src/output'
make[3]: Entering directory '/home/ye/tool/harry/src/output'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/home/ye/tool/harry/src/output'
make[2]: Leaving directory '/home/ye/tool/harry/src/output'
make[2]: Entering directory '/home/ye/tool/harry/src'
make[3]: Entering directory '/home/ye/tool/harry/src'
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c harry '/usr/local/bin'
libtool: install: /usr/bin/install -c harry /usr/local/bin/harry
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/home/ye/tool/harry/src'
make[2]: Leaving directory '/home/ye/tool/harry/src'
make[1]: Leaving directory '/home/ye/tool/harry/src'
Making install in doc
make[1]: Entering directory '/home/ye/tool/harry/doc'
make[2]: Entering directory '/home/ye/tool/harry/doc'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/doc/harry'
 /usr/bin/install -c -m 644 example.cfg '/usr/local/share/doc/harry'
 /usr/bin/mkdir -p '/usr/local/share/man/man1'
 /usr/bin/install -c -m 644 'harry.man' '/usr/local/share/man/man1/harry.1'
make[2]: Leaving directory '/home/ye/tool/harry/doc'
make[1]: Leaving directory '/home/ye/tool/harry/doc'
Making install in examples
make[1]: Entering directory '/home/ye/tool/harry/examples'
Making install in alexa
make[2]: Entering directory '/home/ye/tool/harry/examples/alexa'
make[3]: Entering directory '/home/ye/tool/harry/examples/alexa'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/doc/harry/alexa'
 /usr/bin/install -c -m 644 alexa1000.txt figure_1.png figure_2.png run_example.sh README.md most_similar.py '/usr/local/share/doc/harry/alexa'
make[3]: Leaving directory '/home/ye/tool/harry/examples/alexa'
make[2]: Leaving directory '/home/ye/tool/harry/examples/alexa'
Making install in reuters
make[2]: Entering directory '/home/ye/tool/harry/examples/reuters'
make[3]: Entering directory '/home/ye/tool/harry/examples/reuters'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/doc/harry/reuters'
 /usr/bin/install -c -m 644 README.md harry.cfg reuters.zip run_example.sh '/usr/local/share/doc/harry/reuters'
make[3]: Leaving directory '/home/ye/tool/harry/examples/reuters'
make[2]: Leaving directory '/home/ye/tool/harry/examples/reuters'
Making install in .
make[2]: Entering directory '/home/ye/tool/harry/examples'
make[3]: Entering directory '/home/ye/tool/harry/examples'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/doc/harry'
 /usr/bin/install -c -m 644 README.md TUTORIAL.md data.txt '/usr/local/share/doc/harry'
make[3]: Leaving directory '/home/ye/tool/harry/examples'
make[2]: Leaving directory '/home/ye/tool/harry/examples'
make[1]: Leaving directory '/home/ye/tool/harry/examples'
Making install in python
make[1]: Entering directory '/home/ye/tool/harry/python'
make[2]: Entering directory '/home/ye/tool/harry/python'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/lib/python3.7/site-packages'
 /usr/bin/install -c -m 644 harry.py '/usr/local/lib/python3.7/site-packages'
Byte-compiling python modules...
harry.py
Byte-compiling python modules (optimized versions) ...
harry.py
make[2]: Leaving directory '/home/ye/tool/harry/python'
make[1]: Leaving directory '/home/ye/tool/harry/python'
Making install in .
make[1]: Entering directory '/home/ye/tool/harry'
make[2]: Entering directory '/home/ye/tool/harry'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/harry'
make[1]: Leaving directory '/home/ye/tool/harry'
Making install in tests
make[1]: Entering directory '/home/ye/tool/harry/tests'
make[2]: Entering directory '/home/ye/tool/harry/tests'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/harry/tests'
make[1]: Leaving directory '/home/ye/tool/harry/tests'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ 
```

## Check the -D option

harry က input, measure နဲ့ output အလုပ်တွေအတွက် configuration setting file နဲ့ အပြောင်းအလဲ လုပ်တာကို support လုပ်ပါတယ်။  
လက်ရှိ setting ကို ကြည့်ချင်ရင် "-D" option နဲ့ ကြည့်လို့ ရတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ harry -D
# Harry 0.4.3 - Default configuration
input = {
       input_format	= "lines";
       chunk_size	= 256;
       decode_str	= false;
       fasta_regex	= " (\+|-)?[0-9]+";
       lines_regex	= "^(\+|-)?[0-9]+";
       reverse_str	= false;
       stoptoken_file	= "";
       soundex	= false;
};

measures = {
       measure	= "dist_levenshtein";
       granularity	= "bytes";
       token_delim	= " %0a%0d";
       num_threads	= 0;
       cache_size	= 256;
       global_cache	= false;
       col_range	= "";
       row_range	= "";
       split	= "";
       dist_hamming = {
              norm	= "none";
       };

       dist_levenshtein = {
              norm	= "none";
              cost_ins	= 1.00000;
              cost_del	= 1.00000;
              cost_sub	= 1.00000;
       };

       dist_damerau = {
              norm	= "none";
              cost_ins	= 1.00000;
              cost_del	= 1.00000;
              cost_sub	= 1.00000;
              cost_tra	= 1.00000;
       };

       dist_osa = {
              norm	= "none";
              cost_ins	= 1.00000;
              cost_del	= 1.00000;
              cost_sub	= 1.00000;
              cost_tra	= 1.00000;
       };

       dist_jarowinkler = {
              scaling	= 0.10000;
       };

       dist_lee = {
              min_sym	= 0;
              max_sym	= 255;
       };

       dist_compression = {
              level	= 9;
       };

       dist_bag = {
              norm	= "none";
       };

       dist_kernel = {
              kern	= "kern_wdegree";
              norm	= "none";
              squared	= true;
       };

       kern_wdegree = {
              degree	= 3;
              shift	= 0;
              norm	= "none";
       };

       kern_distance = {
              dist	= "dist_bag";
              type	= "linear";
              gamma	= 1.00000;
              degree	= 1.00000;
              norm	= "none";
       };

       kern_subsequence = {
              length	= 3;
              lambda	= 0.10000;
              norm	= "none";
       };

       kern_spectrum = {
              length	= 3;
              norm	= "none";
       };

       sim_coefficient = {
              matching	= "bin";
       };

};

output = {
       output_format	= "text";
       precision	= 0;
       separator	= ",";
       save_indices	= false;
       save_labels	= false;
       save_sources	= false;
       compress	= false;
};

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$
```

## Checking Support Measures

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ harry -M
    dist_bag             Bag distance
    dist_compression     Normalized compression distance (NCD)
    dist_damerau         Damerau-Levenshtein distance
    dist_hamming         Hamming distance
    dist_jaro            Jaro distance
    dist_jarowinkler     Jaro-Winkler distance
    dist_kernel          Kernel substitution distance
    dist_lee             Lee distance
    dist_levenshtein     Levenshtein distance
    dist_osa             Optimal string alignment (OSA) distance
    kern_distance        Distance substitution kernel (DSK)
    kern_spectrum        Spectrum kernel
    kern_subsequence     Subsequence kernel (SSK)
    kern_wdegree         Weighted-degree kernel (WDK)
    sim_braun            Braun-Blanquet coefficient
    sim_dice             Soerensen-Dice coefficient
    sim_jaccard          Jaccard coefficient
    sim_kulczynski       second Kulczynski coefficient
    sim_otsuka           Otsuka coefficient
    sim_simpson          Simpson coefficient
    sim_sokal            Sokal-Sneath coefficient
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$
```

## Testing

Testing လုပ်ဖို့အတွက်က ဒီ link ကို မှီငြမ်းခဲ့ ```https://github.com/rieck/harry/blob/master/examples/TUTORIAL.md```  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ cat ./2lines.txt 
အားပေး နေ မယ် ။
စောင့်မျှော် နေ မယ် နော် ။
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ harry ./2lines.txt -
# Harry 0.4.3 - Output module for stdout format
0,35
35,0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$
```


## Testing Harry Python Module

Harry ကို python module အနေနဲ့လည်း ခေါ်သုံးလို့ ရပါတယ်။   
ခေါ်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import harry
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'harry'
>>> exit()
```
အထက်ပါအတိုင်း error ပေးပါတယ်။  
PYTHONPATH မှာ harry.py ပရိုဂရမ်ရှိတဲ့ path ကို assign လုပ်ထားမှ ရမယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/python$ export PYTHONPATH=/home/ye/tool/harry/python
```

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import harry
>>> print(help(harry))

Enter ခေါက်လိုက်ရင် အောက်ပါ harry ရဲ့ help screen ကို မြင်ရလိမ့်မယ် ...  

```
Help on module harry:

NAME
    harry

DESCRIPTION
    Harry is a small tool for measuring the similarity of strings.  The
    module supports common distance and kernel functions for strings as
    well as some exotic similarity measures.
    
    The Python module of Harry uses largely the same parameters as the
    command-line tool. See manual page harry(1) for more information.
    Copyright (C) 2013-2015 Konrad Rieck (konrad@mlsec.org)

FUNCTIONS
    compare(x, y=None, **kwargs)
        Compare strings using a similarity measure
        
        Parameters
        ----------
        x (list)                  List of strings to compare
        y (list)                  List of strings to compare [optional]
        
        Parameters (Measure options)
        ----------
        measure (str)             Set similarity measure.
        granularity (str)         Set granularity: bytes, bits, tokens.
        token_delim (str)         Set delimiters for tokens.
        num_threads (int)         Set number of threads.
        cache_size (int)          Set size of cache in megabytes.
        global_cache (bool)       Enable global cache.
        col_range (str)           Set the column range (x) of strings.
        row_range (str)           Set the row range (y) of strings.
        split (str)               Split matrix into blocks and compute one.
        
        Parameters (Generic options)
:

```

နောက်စာမျက်နှာကို သွားချင်ရင် Space ကီးနှိပ်ပါ...  
ဒီ လက်ရှိ help screen က ထွက်ချင်ရင် q ကို နှိပ်ပါ...  

## Testing with myPara

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ shuf ./train.txt | head
သူ ပြော ၍ ဝ သောအခါ ပြန် လှည့် သွား သည် ။	သူ ပြော ၍ ကျေနပ် သောအခါ ပြန် လှည့် သွား သည် ။	1
မင်း ဘယ် သူ့ ကို ရွေးချယ် သင့် သလဲ ။	သူ့ ပျား တွေ နဲ့ အတူ ရှိ နေ တယ် ။	0
ရှေး ဘုရင် များ တွင် မိဖုရား များ တစ် ယောက် မ က ရှိ ကြ သည် ။	ထို ဘုရင် ကြီး သည် မိဖုရားခေါင်ကြီး တစ် ဦး သာ ထား ခဲ့ သည် ။	0
ဘယ် နေ့ လာ ရ မယ် ဆို တာ မင်း ကို ပြော ဖို့ ငါ မေ့ သွား ခဲ့ တယ် ။	ဘယ် နေ့ လာ ရ မယ် ဆို တာ မင်း ကို ပြော ဖို့ ငါ မ မေ့ ပါ ဘူး ။	0
ရှိ ခိုး ပူဇော် ပါ တယ်	ရှိ ခိုး ဦး တိုက် ပါ တယ်	1
နားလည် ပြီ ။	နားမလည် ဘူး လား ။	0
ကြား ရ တာ စိတ် မ ကောင်း ပါ ဘူး	ကြား ရ တာ စိတ် မ ကောင်း လိုက် တာ	1
ငကြောင် ပါ ကွာ	င ကြောက် တွေ ပဲ နော်	0
ဆရာတော် ကျန်းမာ ချမ်းသာ ပါ စေ သက်တော် ရာ ကျော် ရှည် ပါ စေ	ဆရာတော် ကြီး များ အသက် ရာ ကျော် ရှည် ပါ စေ	1
ကိုယ် အဲ့ဒါ ကို စုံစမ်း လေ့လာ လိုက် မယ် ။	ကိုယ် တို့ အဲ့ဒါ ကို ထပ် မ စုံစမ်း တော့ ဘူး ။	0
```

အထက်ပါ shuffle လုပ်ပြီးထွက်လာတဲ့ စာကြောင်း 10 ကြောင်းကိုတည်ပြီး စမ်းခဲ့...  

## write a shell script

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ cat mk-distance-csv.sh 
#!/bin/bash

# for getting all distances of "harry string similarity tool"
# written by Ye, LST, NECTEC, Thailand
# 20 Sept 2021

cut -f3 $1 > label.txt

cut -f1,2 $1 | sed -e 'y/\t/\n/' > ./para.tmp

count=($(wc ./para.tmp));

# clean previous calculated files
rm {dist_,sim_,kern}*.txt;

for distance in {dist_bag,dist_compression,dist_damerau,dist_hamming,dist_jaro,\
dist_jarowinkler,dist_kernel,dist_lee,dist_levenshtein,dist_osa,\
kern_distance,kern_spectrum,kern_subsequence,kern_wdegree,sim_braun,\
sim_dice,sim_jaccard,sim_kulczynski,sim_otsuka,sim_simpson,sim_sokal}
do
    # bash ပုံမှန် တွန့်ကွင်းနဲ့ looping ပတ်တဲ့အခါမှာ eval တို့ seq တို့ကို သုံးရတာမို့ C style နဲ့ပဲ သုံးခဲ့
    for (( i = 0; i < $count-1; i+=2 )) 
    do 
        # harry -x 0:1 -y 1:2
        #echo "$i:$(( $i+1 )) -y $(( $i+1 )):$(( $i+2 )):";
        harry -q -m $distance -x $i:$(( $i+1 )) -y $(( $i+1 )):$(( $i+2 )) ./para.tmp - | grep -v "#" >> $distance.txt
    done
done

paste {dist_bag,dist_compression,dist_damerau,dist_hamming,dist_jaro,\
dist_jarowinkler,dist_kernel,dist_lee,dist_levenshtein,dist_osa,\
kern_distance,kern_spectrum,kern_subsequence,kern_wdegree,sim_braun,\
sim_dice,sim_jaccard,sim_kulczynski,sim_otsuka,sim_simpson,sim_sokal}.txt ./label.txt -d "," > all_distance.txt

echo "wc all_distance.txt:"
wc all_distance.txt

echo "head all_distance.txt:"
head all_distance.txt

rm ./label.txt;
rm ./para.tmp;
```

## make features CSV file

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ bash ./mk-distance-csv.sh ./mypara-10lines.txt 
wc all_distance.txt:
  10   10 1455 all_distance.txt
head all_distance.txt:
16,0.146341,16,89,0.166014,0.0996083,164.333,6000,16,16,11918.5,243,0.000263601,26.6667,0.956522,0.956522,0.916667,0.956522,0.956522,0.956522,0.846154,1
23,0.506944,38,61,0.289805,0.231844,129.667,3508,38,38,7598,98,0.000111681,23,0.73913,0.755556,0.607143,0.755929,0.755742,0.772727,0.435897,0
17,0.463918,43,115,0.216625,0.1733,255,7241,43,43,23726,387,0.000447501,26.3333,0.777778,0.807692,0.677419,0.808889,0.80829,0.84,0.512195,0
17,0.188119,20,41,0.0711534,0.0426921,71.3333,3053,20,20,23607.5,509,0.000551857,117.667,0.892857,0.925926,0.862069,0.927198,0.926562,0.961538,0.757576,0
9,0.288136,9,31,0.14945,0.0896699,62,2047,9,9,3563.5,77,8.4394e-05,28.3333,0.777778,0.848485,0.736842,0.855556,0.852013,0.933333,0.583333,1
16,0.393617,16,26,0.218734,0.13124,44.3333,1799,16,16,1396.5,30,3.23094e-05,15.6667,0.785714,0.785714,0.647059,0.785714,0.785714,0.785714,0.478261,0
11,0.230769,12,17,0.0807298,0.0484379,30.3333,1206,12,12,6189.5,157,0.000178442,63.1667,0.777778,0.823529,0.7,0.826389,0.824958,0.875,0.538462,1
16,0.4375,18,46,0.240478,0.168335,80.3333,3365,18,18,1946,50,5.94379e-05,4.16667,0.769231,0.833333,0.714286,0.839161,0.836242,0.909091,0.555556,0
44,0.346591,46,114,0.21214,0.127284,194.333,8106,46,46,16482.5,361,0.000420554,32.6667,0.857143,0.878049,0.782609,0.878571,0.87831,0.9,0.642857,1
13,0.358824,37,81,0.161302,0.0967811,166,5205,37,37,12700.5,218,0.000258249,29.3333,0.8,0.869565,0.769231,0.87619,0.872872,0.952381,0.625,0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$
```

တကယ် run ဖို့အတွက်ကတော့ myPara corpus တစ်ခုလုံးနဲ့ ဆောက်ဖို့ လိုအပ်တယ်။

## Paper of Harry Tool

Paper title: Harry: A Tool for Measuring String Similarity:  
Authors: Konrad Rieck, Christian Wressnegger  
https://jmlr.org/papers/volume17/rieck16a/rieck16a.pdf  

Documentation: https://github.com/rieck/harry/tree/master/doc  
Harry Version 0.4.3, User Manual: https://github.com/rieck/harry/blob/master/doc/harry.pdf  

