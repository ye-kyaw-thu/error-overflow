# CRFSuite version 0.12 Installation Note

CRF-Suite ကို installation မလုပ်ခင်မှာ အရင်ဆုံး liblbfgs က ကိုယ့်စက်ထဲမှာ မရှိသေးရင်  
အဲဒါကို အရင်ဆုံး install လုပ်ပေးရတယ်။  

Download link: https://github.com/chokkan/liblbfgs  

## After download liblbfgs

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ mv ~/Downloads/liblbfgs-master.zip .
```

## Unzip

```
(base) ye@ykt-pro:~/tool$ unzip ./liblbfgs-master.zip 
Archive:  ./liblbfgs-master.zip
7fc787678e4a7f02eaef1c21b36b9bc3bcc0d39b
   creating: liblbfgs-master/
  inflating: liblbfgs-master/.gitignore  
  inflating: liblbfgs-master/AUTHORS  
  inflating: liblbfgs-master/CMakeLists.txt  
  inflating: liblbfgs-master/COPYING  
  inflating: liblbfgs-master/ChangeLog  
  inflating: liblbfgs-master/Makefile.am  
 extracting: liblbfgs-master/NEWS    
  inflating: liblbfgs-master/README  
  inflating: liblbfgs-master/autogen.sh  
   creating: liblbfgs-master/cmake/
  inflating: liblbfgs-master/cmake/Config.cmake.in  
  inflating: liblbfgs-master/cmake/Subproject.cmake  
  inflating: liblbfgs-master/configure.ac  
   creating: liblbfgs-master/doc/
  inflating: liblbfgs-master/doc/doxyfile  
  inflating: liblbfgs-master/doc/footer.html  
  inflating: liblbfgs-master/doc/header.html  
   creating: liblbfgs-master/include/
  inflating: liblbfgs-master/include/lbfgs.h  
  inflating: liblbfgs-master/lbfgs.sln  
   creating: liblbfgs-master/lib/
  inflating: liblbfgs-master/lib/Makefile.am  
  inflating: liblbfgs-master/lib/arithmetic_ansi.h  
  inflating: liblbfgs-master/lib/arithmetic_sse_double.h  
  inflating: liblbfgs-master/lib/arithmetic_sse_float.h  
  inflating: liblbfgs-master/lib/lbfgs.c  
  inflating: liblbfgs-master/lib/lib.vcxproj  
   creating: liblbfgs-master/sample/
  inflating: liblbfgs-master/sample/Makefile.am  
  inflating: liblbfgs-master/sample/sample.c  
  inflating: liblbfgs-master/sample/sample.cpp  
  inflating: liblbfgs-master/sample/sample.vcxproj  
```

## Change directory

```
(base) ye@ykt-pro:~/tool$ cd liblbfgs-master/
```

## Run ./autogen.sh and got error!!!

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ ./autogen.sh 
libtoolize:   error: One of these is required:
libtoolize:                 gm4 gnum4 m4
libtoolize:   error: Please install GNU M4, or 'export M4=/path/to/gnu/m4'.
./autogen.sh: 20: ./autogen.sh: aclocal: not found
aclocal failed!
```

## To solve error try to install libtool

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ sudo apt-get install libtool m4 automake
[sudo] password for ye: 
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?

(base) ye@ykt-pro:~/tool/liblbfgs-master$ sudo apt-get install libtool
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
```

## Check the process

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ ps aux | grep -i apt
root      5551  0.0  0.0   4624   772 ?        Ss   21:11   0:00 /bin/sh /usr/lib/apt/apt.systemd.daily install
root      5555  0.0  0.0   4624  1640 ?        S    21:11   0:00 /bin/sh /usr/lib/apt/apt.systemd.daily lock_is_held install
root     11404 32.0  1.2 177640 98056 ?        RN   21:14   0:00 /usr/bin/python3 /usr/lib/update-notifier/apt-check --human-readable
ye       11411  0.0  0.0  21824  1036 pts/0    S+   21:14   0:00 grep --color=auto -i apt
```

အထက်မှာ မြင်ရတဲ့အတိုင်း apt.systemd.daily* နဲ့ ဆိုင်တဲ့ process တွေက run နေတာကို  
တွေ့ရတယ်။  
ဆရာက System setting မှာ application, installed software package တွေကို အော်တို update လုပ်ခိုင်းထားလို့ ...  
ဆရာ က ဒီ ကွန်ပျူတာကို ပိတ်ထားတာ ၂ပတ်လောက် ရှိနေလို့ Ubuntu OS က auto update လုပ်နေလို့ ...   

အဲဒီလို ကိစ္စဆိုရင်တော့ စောင့် ယုံပဲ ရှိတယ်။  
ခဏစောင့်တယ်။  
Reference: https://itsfoss.com/could-not-get-lock-error/  

## After waiting, try to install again

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ sudo apt-get install libtool m4 automake
Reading package lists... Done
Building dependency tree       
Reading state information... Done
libtool is already the newest version (2.4.6-2).
libtool set to manually installed.
The following packages were automatically installed and are no longer required:
  linux-headers-5.3.0-40 linux-headers-5.3.0-40-generic
  linux-image-5.3.0-40-generic linux-modules-5.3.0-40-generic
  linux-modules-extra-5.3.0-40-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  autoconf libsigsegv2
Suggested packages:
  autoconf-archive gnu-standards autoconf-doc m4-doc
The following NEW packages will be installed:
  autoconf automake libsigsegv2 m4
0 upgraded, 4 newly installed, 0 to remove and 64 not upgraded.
Need to get 1,043 kB of archives.
After this operation, 3,833 kB of additional disk space will be used.
Do you want to continue? [Y/n] 
...
....
...

Preparing to unpack .../autoconf_2.69-11_all.deb ...
Unpacking autoconf (2.69-11) ...
Selecting previously unselected package automake.
Preparing to unpack .../automake_1%3a1.15.1-3ubuntu2_all.deb ...
Unpacking automake (1:1.15.1-3ubuntu2) ...
Setting up libsigsegv2:amd64 (2.12-1) ...
Setting up m4 (1.4.18-1) ...
Setting up autoconf (2.69-11) ...
Setting up automake (1:1.15.1-3ubuntu2) ...
update-alternatives: using /usr/bin/automake-1.15 to provide /usr/bin/automake (automake) in auto mode
Processing triggers for install-info (6.5.0.dfsg.1-2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:~/tool/liblbfgs-master$ 
```

## Installation of liblbfgs

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ ./autogen.sh 
libtoolize: putting auxiliary files in '.'.
libtoolize: copying file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
configure.ac:30: installing './compile'
configure.ac:30: installing './config.guess'
configure.ac:30: installing './config.sub'
configure.ac:22: installing './install-sh'
configure.ac:22: installing './missing'
configure.ac:102: warning: 'INCLUDES' is the old name for 'AM_CPPFLAGS' (or '*_CPPFLAGS')
Makefile.am: installing './INSTALL'
lib/Makefile.am:24: warning: 'INCLUDES' is the old name for 'AM_CPPFLAGS' (or '*_CPPFLAGS')
lib/Makefile.am: installing './depcomp'
sample/Makefile.am:15: warning: 'INCLUDES' is the old name for 'AM_CPPFLAGS' (or '*_CPPFLAGS')
```

## ./configure

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
...
...
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating lib/Makefile
config.status: creating sample/Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
(base) ye@ykt-pro:~/tool/liblbfgs-master$ 
```

## make

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ make
make  all-recursive
make[1]: Entering directory '/home/ye/tool/liblbfgs-master'
Making all in lib
make[2]: Entering directory '/home/ye/tool/liblbfgs-master/lib'
/bin/bash ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I.. -I.. -I../include   -O3 -ffast-math  -Wall -O3 -ffast-math  -Wall -MT lbfgs.lo -MD -MP -MF .deps/lbfgs.Tpo -c -o lbfgs.lo lbfgs.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I.. -I.. -I../include -O3 -ffast-math -Wall -O3 -ffast-math -Wall -MT lbfgs.lo -MD -MP -MF .deps/lbfgs.Tpo -c lbfgs.c  -fPIC -DPIC -o .libs/lbfgs.o
...
...
libtool: link: gcc -O3 -ffast-math -Wall -O3 -ffast-math -Wall -o .libs/sample sample.o   ../lib/.libs/liblbfgs.so -lm
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master/sample'
make[2]: Entering directory '/home/ye/tool/liblbfgs-master'
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master'
make[1]: Leaving directory '/home/ye/tool/liblbfgs-master'
(base) ye@ykt-pro:~/tool/liblbfgs-master$ 
```

## make install

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ make install
Making install in lib
make[1]: Entering directory '/home/ye/tool/liblbfgs-master/lib'
make[2]: Entering directory '/home/ye/tool/liblbfgs-master/lib'
 /bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   liblbfgs.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/liblbfgs-1.10.so /usr/local/lib/liblbfgs-1.10.so
/usr/bin/install: cannot create regular file '/usr/local/lib/liblbfgs-1.10.so': Permission denied
Makefile:384: recipe for target 'install-libLTLIBRARIES' failed
make[2]: *** [install-libLTLIBRARIES] Error 1
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master/lib'
Makefile:572: recipe for target 'install-am' failed
make[1]: *** [install-am] Error 2
make[1]: Leaving directory '/home/ye/tool/liblbfgs-master/lib'
Makefile:455: recipe for target 'install-recursive' failed
make: *** [install-recursive] Error 1
(base) ye@ykt-pro:~/tool/liblbfgs-master$ 
```

*** Note make install ကို run ဖို့ sudo ခံပေးရမယ်။  

```
(base) ye@ykt-pro:~/tool/liblbfgs-master$ sudo make install
Making install in lib
make[1]: Entering directory '/home/ye/tool/liblbfgs-master/lib'
make[2]: Entering directory '/home/ye/tool/liblbfgs-master/lib'
 /bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   liblbfgs.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/liblbfgs-1.10.so /usr/local/lib/liblbfgs-1.10.so
libtool: install: (cd /usr/local/lib && { ln -s -f liblbfgs-1.10.so liblbfgs.so || { rm -f liblbfgs.so && ln -s liblbfgs-1.10.so liblbfgs.so; }; })
libtool: install: /usr/bin/install -c .libs/liblbfgs.lai /usr/local/lib/liblbfgs.la
libtool: install: /usr/bin/install -c .libs/liblbfgs.a /usr/local/lib/liblbfgs.a
libtool: install: chmod 644 /usr/local/lib/liblbfgs.a
libtool: install: ranlib /usr/local/lib/liblbfgs.a
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
 /bin/mkdir -p '/usr/local/include'
 /usr/bin/install -c -m 644 ../include/lbfgs.h '/usr/local/include'
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master/lib'
make[1]: Leaving directory '/home/ye/tool/liblbfgs-master/lib'
Making install in sample
make[1]: Entering directory '/home/ye/tool/liblbfgs-master/sample'
make[2]: Entering directory '/home/ye/tool/liblbfgs-master/sample'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master/sample'
make[1]: Leaving directory '/home/ye/tool/liblbfgs-master/sample'
make[1]: Entering directory '/home/ye/tool/liblbfgs-master'
make[2]: Entering directory '/home/ye/tool/liblbfgs-master'
make[2]: Nothing to be done for 'install-exec-am'.
 /bin/mkdir -p '/usr/local/share/doc/liblbfgs'
 /usr/bin/install -c -m 644 README INSTALL COPYING AUTHORS ChangeLog NEWS '/usr/local/share/doc/liblbfgs'
make[2]: Leaving directory '/home/ye/tool/liblbfgs-master'
make[1]: Leaving directory '/home/ye/tool/liblbfgs-master'
(base) ye@ykt-pro:~/tool/liblbfgs-master$ 
```

# CRFsuite Installation 

Download link: http://www.chokkan.org/software/crfsuite/  

After you download ...  
move to that tar.gz file to your installation folder  

```
(base) ye@ykt-pro:~/tool$ tar -xzvf ./crfsuite-0.12.tar.gz 
crfsuite-0.12/
crfsuite-0.12/lib/
crfsuite-0.12/lib/crf/
crfsuite-0.12/lib/crf/Makefile.am
crfsuite-0.12/lib/crf/crf.vcxproj
crfsuite-0.12/lib/crf/src/
crfsuite-0.12/lib/crf/src/dataset.c
...
...
```

## Change folder

```
(base) ye@ykt-pro:~/tool$ cd crfsuite-0.12/
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ ls
aclocal.m4  config.guess  COPYING       genbinary.sh.in  ltmain.sh    swig
AUTHORS     config.h.in   crfsuite.sln  include          Makefile.am  win32
autogen.sh  config.sub    depcomp       INSTALL          Makefile.in
ChangeLog   configure     example       install-sh       missing
compile     configure.in  frontend      lib              README
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ 
```

## Installation

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ ./autogen.sh 
libtoolize: putting auxiliary files in '.'.
libtoolize: copying file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
aclocal: warning: autoconf input should be named 'configure.ac', not 'configure.in'
configure.in:33: error: automatic de-ANSI-fication support has been removed
/usr/share/aclocal-1.15/obsolete.m4:26: AM_C_PROTOTYPES is expanded from...
configure.in:33: the top level
autom4te: /usr/bin/m4 failed with exit status: 1
aclocal: error: echo failed with exit status: 1
aclocal failed!
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ 
```

*** Got Error!  

### Error message မှာ ပြောထားတဲ့ အတိုင်း ဖိုင်နာမည်ပြောင်းကြည့် ...

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ ls configure
configure     configure.in  
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ mv configure.in configure.ac
```

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ ./autogen.sh 
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: You should add the contents of 'm4/libtool.m4' to 'aclocal.m4'.
libtoolize: You should add the contents of 'm4/ltoptions.m4' to 'aclocal.m4'.
libtoolize: You should add the contents of 'm4/ltversion.m4' to 'aclocal.m4'.
libtoolize: You should add the contents of 'm4/lt~obsolete.m4' to 'aclocal.m4'.
configure.ac:33: error: automatic de-ANSI-fication support has been removed
/usr/share/aclocal-1.15/obsolete.m4:26: AM_C_PROTOTYPES is expanded from...
configure.ac:33: the top level
autom4te: /usr/bin/m4 failed with exit status: 1
aclocal: error: echo failed with exit status: 1
aclocal failed!
```

## Skip running ./autogen.sh and Install

./autogen.sh အဆင့်ကို မလုပ်တော့ပဲ ပုံမှန်အတိုင်းပဲ အောက်ပါအတိုင်း  
installation လုပ်တော့ အဆင်ပြေသွားတယ်  

## ./configure

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
...
...
checking for lbfgs in -llbfgs... yes
configure: creating ./config.status
config.status: creating Makefile
config.status: creating genbinary.sh
config.status: creating include/Makefile
config.status: creating lib/cqdb/Makefile
config.status: creating lib/crf/Makefile
config.status: creating frontend/Makefile
config.status: creating swig/Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
```

## Run make

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ make
make  all-recursive
make[1]: Entering directory '/home/ye/tool/crfsuite-0.12'
Making all in include
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12/include'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12/include'
Making all in lib/cqdb
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12/lib/cqdb'
/bin/bash ../../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I../.. -I../.. -I../../include -I.   -I./include -mfpmath=sse -msse2 -DUSE_SSE -O3 -fomit-frame-pointer -ffast-math -Winline -std=c99  -MT libcqdb_la-lookup3.lo -MD -MP -MF .deps/libcqdb_la-lookup3.Tpo -c -o libcqdb_la-lookup3.lo `test -f 'src/lookup3.c' || echo './'`src/lookup3.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I../.. -I../.. -I../../include -I. -I./include -mfpmath=sse -msse2 -DUSE_SSE -O3 -fomit-frame-pointer -ffast-math -Winline -std=c99 -MT libcqdb_la-lookup3.lo -MD -MP -MF .deps/libcqdb_la-lookup3.Tpo -c src/lookup3.c  -fPIC -DPIC -o .libs/libcqdb_la-lookup3.o
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I../.. -I../.. -I../../include -I. -I./include -mfpmath=sse -msse2 -DUSE_SSE -O3 -fomit-frame-pointer -ffast-math -Winline -std=c99 -MT libcqdb_la-lookup3.lo -MD -MP -MF .deps/libcqdb_la-lookup3.Tpo -c src/lookup3.c -o libcqdb_la-lookup3.o >/dev/null 2>&1
mv -f .deps/libcqdb_la-lookup3.Tpo .deps/libcqdb_la-lookup3.Plo
...
...
mv -f .deps/crfsuite-main.Tpo .deps/crfsuite-main.Po
/bin/bash ../libtool --tag=CC   --mode=link gcc -I../include -mfpmath=sse -msse2 -DUSE_SSE -O3 -fomit-frame-pointer -ffast-math -Winline -std=c99    -o crfsuite crfsuite-iwa.o crfsuite-option.o crfsuite-reader.o crfsuite-learn.o crfsuite-tag.o crfsuite-dump.o crfsuite-main.o ../lib/crf/libcrfsuite.la -llbfgs -lm 
libtool: link: gcc -I../include -mfpmath=sse -msse2 -DUSE_SSE -O3 -fomit-frame-pointer -ffast-math -Winline -std=c99 -o .libs/crfsuite crfsuite-iwa.o crfsuite-option.o crfsuite-reader.o crfsuite-learn.o crfsuite-tag.o crfsuite-dump.o crfsuite-main.o  ../lib/crf/.libs/libcrfsuite.so /usr/local/lib/liblbfgs.so -lm
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12/frontend'
Making all in swig
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12/swig'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12/swig'
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12'
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12'
make[1]: Leaving directory '/home/ye/tool/crfsuite-0.12'
```

## sudo make install

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ sudo make install
[sudo] password for ye: 
Making install in include
make[1]: Entering directory '/home/ye/tool/crfsuite-0.12/include'
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12/include'
make[2]: Nothing to be done for 'install-exec-am'.
test -z "/usr/local/include" || /bin/mkdir -p "/usr/local/include"
 /usr/bin/install -c -m 644 crfsuite.h crfsuite_api.hpp crfsuite.hpp '/usr/local/include'
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12/include'
make[1]: Leaving directory '/home/ye/tool/crfsuite-0.12/include'
Making install in lib/cqdb
make[1]: Entering directory '/home/ye/tool/crfsuite-0.12/lib/cqdb'
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12/lib/cqdb'
test -z "/usr/local/lib" || /bin/mkdir -p "/usr/local/lib"
 /bin/bash ../../libtool   --mode=install /usr/bin/install -c   libcqdb.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/libcqdb-0.12.so /usr/local/lib/libcqdb-0.12.so
libtool: install: (cd /usr/local/lib && { ln -s -f libcqdb-0.12.so libcqdb.so || { rm -f libcqdb.so && ln -s libcqdb-0.12.so libcqdb.so; }; })
libtool: install: /usr/bin/install -c .libs/libcqdb.lai /usr/local/lib/libcqdb.la
libtool: install: /usr/bin/install -c .libs/libcqdb.a /usr/local/lib/libcqdb.a
libtool: install: chmod 644 /usr/local/lib/libcqdb.a
libtool: install: ranlib /usr/local/lib/libcqdb.a
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /usr/local/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /usr/local/lib
...
...
...
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12/swig'
make[1]: Leaving directory '/home/ye/tool/crfsuite-0.12/swig'
make[1]: Entering directory '/home/ye/tool/crfsuite-0.12'
make[2]: Entering directory '/home/ye/tool/crfsuite-0.12'
make[2]: Nothing to be done for 'install-exec-am'.
test -z "/usr/local/share/doc/crfsuite" || /bin/mkdir -p "/usr/local/share/doc/crfsuite"
 /usr/bin/install -c -m 644 README INSTALL COPYING AUTHORS ChangeLog '/usr/local/share/doc/crfsuite'
make[2]: Leaving directory '/home/ye/tool/crfsuite-0.12'
make[1]: Leaving directory '/home/ye/tool/crfsuite-0.12'
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ 
```

# Check crfsuite command

```
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ crfsuite --help
CRFSuite 0.12  Copyright (c) 2007-2011 Naoaki Okazaki

USAGE: crfsuite <COMMAND> [OPTIONS]
    COMMAND     Command name to specify the processing
    OPTIONS     Arguments for the command (optional; command-specific)

COMMAND:
    learn       Obtain a model from a training set of instances
    tag         Assign suitable labels to given instances by using a model
    dump        Output a model in a plain-text format

For the usage of each command, specify -h option in the command argument.
(base) ye@ykt-pro:~/tool/crfsuite-0.12$ 
```

### Installation Success!!! Yeah~!!! :)  
