## cloning

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/espeak-ng/espeak-ng/
Cloning into 'espeak-ng'...
remote: Enumerating objects: 159, done.
remote: Counting objects: 100% (159/159), done.
remote: Compressing objects: 100% (110/110), done.
remote: Total 42488 (delta 71), reused 103 (delta 47), pack-reused 42329
Receiving objects: 100% (42488/42488), 49.71 MiB | 722.00 KiB/s, done.
Resolving deltas: 100% (29289/29289), done.
```

## checking

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd espeak-ng/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ ls
android       configure.ac    COPYING.BSD2  data        emscripten       fastlane  Makefile.am  src    vim
autogen.sh    COPYING         COPYING.IEEE  dictsource  espeak-ng-data   _layouts  phsource     tests
CHANGELOG.md  COPYING.APACHE  COPYING.UCD   docs        espeak-ng.pc.in  m4        README.md    tools
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ find /usr/lib | grep libespeak-ng
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1.1.49
```

espeak ကို install လုပ်ထားတာရှိလို့ အထက်ပါအတိုင်း library တွေကို မြင်နေရတာ...

## autogen

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ ./autogen.sh 
libtoolize: putting auxiliary files in '.'.
libtoolize: copying file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
configure.ac:4: installing './compile'
configure.ac:4: installing './config.guess'
configure.ac:4: installing './config.sub'
configure.ac:3: installing './install-sh'
configure.ac:3: installing './missing'
Makefile.am:469: warning: '%'-style pattern rules are a GNU make extension
Makefile.am:480: warning: '%'-style pattern rules are a GNU make extension
Makefile.am:483: warning: '%'-style pattern rules are a GNU make extension
Makefile.am:1005: warning: '%'-style pattern rules are a GNU make extension
Makefile.am: installing './INSTALL'
Makefile.am: installing './depcomp'
```

## configure

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking how to print strings... printf
checking whether make supports the include directive... yes (GNU style)
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
checking dependency style of gcc... gcc3
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
checking whether make supports nested variables... (cached) yes
checking whether make supports nested variables... (cached) yes
checking for gcc... (cached) gcc
checking whether we are using the GNU C compiler... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking for gcc option to accept ISO C89... (cached) none needed
checking whether gcc understands -c and -o together... (cached) yes
checking dependency style of gcc... (cached) gcc3
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking dependency style of g++... gcc3
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
checking whether make sets $(MAKE)... (cached) yes
checking whether ln -s works... yes
checking for ndk-build... no
checking for gradle... no
./configure: line 12526: 0: command not found
checking if gcc supports C99 without any flags... yes
checking if gcc supports C99 with the -std=c99 flag... yes
checking if gcc supports C99... -std=c99
checking if targeting FreeBSD... no
checking endian.h usability... yes
checking endian.h presence... yes
checking for endian.h... yes
checking fcntl.h usability... yes
checking fcntl.h presence... yes
checking for fcntl.h... yes
checking getopt.h usability... yes
checking getopt.h presence... yes
checking for getopt.h... yes
checking locale.h usability... yes
checking locale.h presence... yes
checking for locale.h... yes
checking stddef.h usability... yes
checking stddef.h presence... yes
checking for stddef.h... yes
checking stdbool.h usability... yes
checking stdbool.h presence... yes
checking for stdbool.h... yes
checking sys/endian.h usability... no
checking sys/endian.h presence... no
checking for sys/endian.h... no
checking sys/time.h usability... yes
checking sys/time.h presence... yes
checking for sys/time.h... yes
checking wchar.h usability... yes
checking wchar.h presence... yes
checking for wchar.h... yes
checking wctype.h usability... yes
checking wctype.h presence... yes
checking for wctype.h... yes
checking for size_t... yes
checking for ssize_t... yes
checking for uint16_t... yes
checking for uint32_t... yes
checking for uint64_t... yes
checking for pid_t... yes
checking vfork.h usability... no
checking vfork.h presence... no
checking for vfork.h... no
checking for fork... yes
checking for vfork... yes
checking for working fork... yes
checking for working vfork... (cached) yes
checking for working strcoll... yes
checking for error_at_line... yes
checking for dup2... yes
checking for getopt_long... yes
checking for gettimeofday... yes
checking for malloc... yes
checking for memchr... yes
checking for memmove... yes
checking for memset... yes
checking for mkdir... yes
checking for mkstemp... yes
checking for pow... no
checking for realloc... yes
checking for setlocale... yes
checking for sqrt... no
checking for strchr... yes
checking for strdup... yes
checking for strerror... yes
checking for strrchr... yes
checking for strstr... yes
checking pcaudiolib/audio.h usability... no
checking pcaudiolib/audio.h presence... no
checking for pcaudiolib/audio.h... no
checking sonic.h usability... no
checking sonic.h presence... no
checking for sonic.h... no
checking for ronn... no
checking for kramdown... no
checking whether C compiler accepts -Wimplicit... yes
checking whether C compiler accepts -Wmissing-prototypes... yes
checking whether C compiler accepts -Wreturn-type... yes
checking whether C compiler accepts -Wuninitialized... yes
checking whether C compiler accepts -Wunused... yes
checking whether C compiler accepts -Wunused-parameter... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating espeak-ng.pc
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
configure:

    Configuration for eSpeak NG complete.

        Source code location:          .

        C99 Compiler:                  gcc
        C99 Compiler flags:            -Wunused-parameter -Wunused -Wuninitialized -Wreturn-type -Wmissing-prototypes -Wimplicit -g -O2 -std=c99

        Sonic:                         no
        PCAudioLib:                    no

        gradle (Android):              gradle
        ndk-build (Android):           

        Klatt:                         yes
        speechPlayer:                  yes
        MBROLA:                        yes
        Async:                         yes

        Extended Dictionaries:
            Russian:                   no
            Chinese (Mandarin):        no
            Chinese (Cantonese):       no
	    
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$
```

## make with jx option

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make -j8 src/espeak-ng src/speak-ng
Makefile:2783: warning: ignoring prerequisites on suffix rule definition
  CC       src/espeak-ng.o
  CC       src/speak-ng.o
  CC       src/ucd-tools/src/libespeak_ng_la-case.lo
  CC       src/ucd-tools/src/libespeak_ng_la-categories.lo
  CC       src/ucd-tools/src/libespeak_ng_la-ctype.lo
  CC       src/ucd-tools/src/libespeak_ng_la-scripts.lo
  CC       src/ucd-tools/src/libespeak_ng_la-tostring.lo
  CC       src/ucd-tools/src/libespeak_ng_la-proplist.lo
src/espeak-ng.c: In function ‘main’:
src/espeak-ng.c:744:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  744 |   fread(p_text, 1, filesize, f_text);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from src/speak-ng.c:23:
src/espeak-ng.c: In function ‘main’:
src/espeak-ng.c:744:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  744 |   fread(p_text, 1, filesize, f_text);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-compiledata.lo
  CC       src/libespeak-ng/la-compiledict.lo
  CC       src/libespeak-ng/la-compilembrola.lo
  CC       src/libespeak-ng/la-dictionary.lo
  CC       src/libespeak-ng/la-encoding.lo
  CC       src/libespeak-ng/la-error.lo
  CC       src/libespeak-ng/la-espeak_api.lo
src/libespeak-ng/compilembrola.c: In function ‘espeak_ng_CompileMbrolaVoice’:
src/libespeak-ng/compilembrola.c:127:29: warning: ‘%s’ directive writing up to 39 bytes into a region of size between 20 and 179 [-Wformat-overflow=]
  127 |  sprintf(buf, "%s/mbrola_ph/%s_phtrans", path_home, mbrola_voice);
      |                             ^~                      ~~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compilembrola.c:24:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 20 and 218 bytes into a destination of size 190
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c: In function ‘LoadDataFile.part.0.isra’:
src/libespeak-ng/compiledata.c:1033:40: warning: ‘%s’ directive output may be truncated writing up to 199 bytes into a region of size 180 [-Wformat-truncation=]
 1033 |  snprintf(filename, sizeof(filename), "%s/%s", phsrc, path);
      |                                        ^~      ~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:70:10: note: ‘__builtin___snprintf_chk’ output 2 or more bytes (assuming 201) into a destination of size 180
   70 |   return __builtin___snprintf_chk (__s, __n, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   71 |        __bos (__s), __fmt, __va_arg_pack ());
      |        ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-ieee80.lo
  CC       src/libespeak-ng/la-intonation.lo
  CC       src/libespeak-ng/la-mnemonics.lo
  CC       src/libespeak-ng/la-numbers.lo
  CC       src/libespeak-ng/la-readclause.lo
src/libespeak-ng/compiledata.c: In function ‘CompilePhoneme.isra’:
src/libespeak-ng/compiledata.c:2002:29: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 2002 |   sprintf(number_buf, "%.3dP", n_procs);
      |                             ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 13 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledict.c: In function ‘espeak_ng_CompileDictionary’:
src/libespeak-ng/compiledict.c:1550:23: warning: ‘rules.txt’ directive writing 9 bytes into a region of size between 6 and 205 [-Wformat-overflow=]
 1550 |  sprintf(fname_in, "%srules.txt", path);
      |                       ^~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledict.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 10 and 209 bytes into a destination of size 205
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledict.c:1557:26: warning: ‘%s’ directive writing up to 39 bytes into a region of size between 15 and 174 [-Wformat-overflow=]
 1557 |  sprintf(fname_out, "%s%c%s_dict", path_home, PATHSEP, dict_name);
      |                          ^~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledict.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 7 and 205 bytes into a destination of size 175
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-phoneme.lo
src/libespeak-ng/compiledata.c: In function ‘espeak_ng_CompilePhonemeDataPath’:
src/libespeak-ng/compiledata.c:2558:20: warning: ‘/phonemes’ directive writing 9 bytes into a region of size between 1 and 200 [-Wformat-overflow=]
 2558 |  sprintf(fname, "%s/phonemes", phsrc);
      |                    ^~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 10 and 209 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2564:21: warning: ‘%s’ directive writing 14 bytes into a region of size between 0 and 199 [-Wformat-overflow=]
 2564 |  sprintf(fname, "%s/%s", phsrc, "compile_report");
      |                     ^~          ~~~~~~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 16 and 215 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2572:21: warning: ‘%s’ directive writing 17 bytes into a region of size between 0 and 199 [-Wformat-overflow=]
 2572 |  sprintf(fname, "%s/%s", phdst, "phondata-manifest");
      |                     ^~          ~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 19 and 218 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2590:21: warning: ‘%s’ directive writing 8 bytes into a region of size between 0 and 199 [-Wformat-overflow=]
 2590 |  sprintf(fname, "%s/%s", phdst, "phondata");
      |                     ^~          ~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 10 and 209 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2600:21: warning: ‘%s’ directive writing 9 bytes into a region of size between 0 and 199 [-Wformat-overflow=]
 2600 |  sprintf(fname, "%s/%s", phdst, "phonindex");
      |                     ^~          ~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 11 and 210 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2611:21: warning: ‘%s’ directive writing 7 bytes into a region of size between 0 and 199 [-Wformat-overflow=]
 2611 |  sprintf(fname, "%s/%s", phdst, "phontab");
      |                     ^~          ~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 9 and 208 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2623:20: warning: ‘/compile_prog_log’ directive writing 17 bytes into a region of size between 1 and 200 [-Wformat-overflow=]
 2623 |  sprintf(fname, "%s/compile_prog_log", phsrc);
      |                    ^~~~~~~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 18 and 217 bytes into a destination of size 200
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/compiledata.c:2469:21: warning: ‘%s’ directive writing up to 255 bytes into a region of size between 80 and 279 [-Wformat-overflow=]
 2469 |    sprintf(buf, "%s/%s", phsrc, item_string);
      |                     ^~          ~~~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/compiledata.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 2 and 456 bytes into a destination of size 280
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c: In function ‘LookupThousands’:
src/libespeak-ng/numbers.c:1200:26: warning: ‘%d’ directive writing between 1 and 11 bytes into a region of size between 0 and 9 [-Wformat-overflow=]
 1200 |     sprintf(string, "_%dM%do", value, thousandplex);
      |                          ^~
src/libespeak-ng/numbers.c:1200:21: note: directive argument in the range [-2147483647, 2147483647]
 1200 |     sprintf(string, "_%dM%do", value, thousandplex);
      |                     ^~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 6 and 25 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1205:26: warning: ‘%d’ directive writing between 1 and 11 bytes into a region of size between 0 and 9 [-Wformat-overflow=]
 1205 |     sprintf(string, "_%dM%de", value, thousandplex);
      |                          ^~
src/libespeak-ng/numbers.c:1205:21: note: directive argument in the range [-2147483647, 2147483647]
 1205 |     sprintf(string, "_%dM%de", value, thousandplex);
      |                     ^~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 6 and 25 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1210:26: warning: ‘%d’ directive writing between 1 and 11 bytes into a region of size between 0 and 9 [-Wformat-overflow=]
 1210 |     sprintf(string, "_%dM%dx", value, thousandplex);
      |                          ^~
src/libespeak-ng/numbers.c:1210:21: note: directive argument in the range [-2147483647, 2147483647]
 1210 |     sprintf(string, "_%dM%dx", value, thousandplex);
      |                     ^~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 6 and 25 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1215:25: warning: ‘%d’ directive writing between 1 and 11 bytes into a region of size between 0 and 9 [-Wformat-overflow=]
 1215 |    sprintf(string, "_%dM%d", value, thousandplex);
      |                         ^~
src/libespeak-ng/numbers.c:1215:20: note: directive argument in the range [-2147483647, 2147483647]
 1215 |    sprintf(string, "_%dM%d", value, thousandplex);
      |                    ^~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 24 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1228:27: warning: ‘o’ directive writing 1 byte into a region of size between 0 and 10 [-Wformat-overflow=]
 1228 |     sprintf(string, "_%s%do", M_Variant(value), thousandplex);
      |                           ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output 4 or more bytes (assuming 14) into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1233:27: warning: ‘e’ directive writing 1 byte into a region of size between 0 and 10 [-Wformat-overflow=]
 1233 |     sprintf(string, "_%s%de", M_Variant(value), thousandplex);
      |                           ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output 4 or more bytes (assuming 14) into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1238:27: warning: ‘x’ directive writing 1 byte into a region of size between 0 and 10 [-Wformat-overflow=]
 1238 |     sprintf(string, "_%s%dx", M_Variant(value), thousandplex);
      |                           ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output 4 or more bytes (assuming 14) into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1243:26: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 1243 |    sprintf(string, "_%s%d", M_Variant(value), thousandplex);
      |                          ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output 3 or more bytes (assuming 13) into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1247:26: warning: ‘%d’ directive writing between 1 and 10 bytes into a region of size 9 [-Wformat-overflow=]
 1247 |      sprintf(string, "_0M%d", thousandplex-1);
      |                          ^~
src/libespeak-ng/numbers.c:1247:22: note: directive argument in the range [3, 2147483646]
 1247 |      sprintf(string, "_0M%d", thousandplex-1);
      |                      ^~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 14 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c: In function ‘LookupNum2’:
src/libespeak-ng/numbers.c:1381:27: warning: ‘%c’ directive writing 1 byte into a region of size between 0 and 9 [-Wformat-overflow=]
 1381 |      sprintf(string, "_%dX%c", tens, ord_type);
      |                           ^~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 14 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1381:27: warning: ‘%c’ directive writing 1 byte into a region of size between 0 and 9 [-Wformat-overflow=]
 1381 |      sprintf(string, "_%dX%c", tens, ord_type);
      |                           ^~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 14 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1395:28: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 1395 |       sprintf(string, "_%dX", tens);
      |                            ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 4 and 13 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1393:27: warning: ‘Xf’ directive writing 2 bytes into a region of size between 1 and 10 [-Wformat-overflow=]
 1393 |       sprintf(string, "_%dXf", tens);
      |                           ^~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 14 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/readclause.c: In function ‘LookupCharName’:
src/libespeak-ng/readclause.c:274:29: warning: ‘%s’ directive writing up to 59 bytes into a region of size 52 [-Wformat-overflow=]
  274 |    sprintf(buf, "[\002_^_%s %s _^_%s]]", "en", phonemes2, WordToString2(tr->translator_name));
      |                             ^~                 ~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/readclause.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 15 and 78 bytes into a destination of size 60
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/readclause.c:279:23: warning: ‘%s’ directive writing up to 59 bytes into a region of size 58 [-Wformat-overflow=]
  279 |    sprintf(buf, "[\002%s]] ", phonemes2);
      |                       ^~      ~~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/readclause.c:27:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 6 and 65 bytes into a destination of size 60
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c: In function ‘LookupNum3.isra’:
src/libespeak-ng/numbers.c:1616:27: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 1616 |     sprintf(string, "_%dCo", hundreds);
      |                           ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 13 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1616:27: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 1616 |     sprintf(string, "_%dCo", hundreds);
      |                           ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 13 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/numbers.c:1634:29: warning: ‘__builtin___sprintf_chk’ may write a terminating nul past the end of the destination [-Wformat-overflow=]
 1634 |       sprintf(string, "_%dC0", hundreds);
      |                             ^
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/numbers.c:25:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 5 and 13 bytes into a destination of size 12
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-phonemelist.lo
  CC       src/libespeak-ng/la-setlengths.lo
  CC       src/libespeak-ng/la-spect.lo
  CC       src/libespeak-ng/la-speech.lo
src/libespeak-ng/spect.c: In function ‘LoadSpectSeq’:
src/libespeak-ng/spect.c:301:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  301 |  fread(&id1, sizeof(uint32_t), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:303:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  303 |  fread(&id2, sizeof(uint32_t), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:318:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  318 |  fread(&name_len, sizeof(uint32_t), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:325:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  325 |   fread(spect->name, sizeof(char), name_len, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:329:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  329 |  fread(&n, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:330:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  330 |  fread(&spect->amplitude, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:331:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  331 |  fread(&spect->max_y, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:332:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  332 |  fread(&temp, sizeof(short), 1, stream); // unused
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c: In function ‘LoadFrame’:
src/libespeak-ng/spect.c:144:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  144 |  fread(&frame->nx, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:145:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  145 |  fread(&frame->markers, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:146:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  146 |  fread(&frame->amp_adjust, sizeof(short), 1, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:152:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  152 |   fread(&ix, sizeof(short), 1, stream); // spare
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:153:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  153 |   fread(&ix, sizeof(short), 1, stream); // spare
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:157:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  157 |   fread(&frame->formants[ix].freq, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:158:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  158 |   fread(&frame->formants[ix].bandw, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:159:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  159 |   fread(&frame->peaks[ix].pkfreq, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:160:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  160 |   fread(&frame->peaks[ix].pkheight, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:161:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  161 |   fread(&frame->peaks[ix].pkwidth, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:162:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  162 |   fread(&frame->peaks[ix].pkright, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:173:4: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  173 |    fread(&frame->peaks[ix].klt_bw, sizeof(short), 1, stream);
      |    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:174:4: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  174 |    fread(&frame->peaks[ix].klt_ap, sizeof(short), 1, stream);
      |    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:175:4: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  175 |    fread(&frame->peaks[ix].klt_bp, sizeof(short), 1, stream);
      |    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:185:4: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  185 |    fread(frame->klatt_param + ix, sizeof(short), 1, stream);
      |    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c:197:3: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
  197 |   fread(&x, sizeof(short), 1, stream);
      |   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/spect.c: In function ‘read_double’:
src/libespeak-ng/spect.c:51:2: warning: ignoring return value of ‘fread’ declared with attribute ‘warn_unused_result’ [-Wunused-result]
   51 |  fread(bytes, sizeof(char), 10, stream);
      |  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
src/libespeak-ng/speech.c: In function ‘espeak_ng_InitializeOutput’:
src/libespeak-ng/speech.c:267:125: warning: unused parameter ‘device’ [-Wunused-parameter]
  267 | ESPEAK_NG_API espeak_ng_STATUS espeak_ng_InitializeOutput(espeak_ng_OUTPUT_MODE output_mode, int buffer_length, const char *device)
      |                                                                                                                 ~~~~~~~~~~~~^~~~~~
  CC       src/libespeak-ng/la-ssml.lo
  CC       src/libespeak-ng/la-synthdata.lo
src/libespeak-ng/ssml.c: In function ‘ParseSsmlReference’:
src/libespeak-ng/ssml.c:972:29: warning: format ‘%x’ expects argument of type ‘unsigned int *’, but argument 3 has type ‘int *’ [-Wformat=]
  972 |    return sscanf(&ref[2], "%x", c1);
      |                            ~^   ~~
      |                             |   |
      |                             |   int *
      |                             unsigned int *
      |                            %x
  CC       src/libespeak-ng/la-synthesize.lo
  CC       src/libespeak-ng/la-synth_mbrola.lo
  CC       src/libespeak-ng/la-translate.lo
src/libespeak-ng/synthesize.c: In function ‘DoPhonemeAlignment’:
src/libespeak-ng/synthesize.c:141:23: warning: assignment to ‘intptr_t’ {aka ‘long int’} from ‘char *’ makes integer from pointer without a cast [-Wint-conversion]
  141 |  wcmdq[wcmdq_tail][1] = pho;
      |                       ^
  CC       src/libespeak-ng/la-tr_languages.lo
  CC       src/libespeak-ng/la-voices.lo
src/libespeak-ng/voices.c: In function ‘SetVoiceScores’:
src/libespeak-ng/voices.c:1167:27: warning: ‘%s’ directive writing up to 79 bytes into a region of size between 73 and 232 [-Wformat-overflow=]
 1167 |   sprintf(buf, "%s/voices/%s", path_home, language);
      |                           ^~              ~~~~~~~~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/voices.c:26:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:38:10: note: ‘__builtin___sprintf_chk’ output between 9 and 247 bytes into a destination of size 240
   38 |   return __builtin___sprintf_chk (__s, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   39 |       __bos (__s), __fmt, __va_arg_pack ());
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-wavegen.lo
  CC       src/libespeak-ng/la-klatt.lo
  CC       src/libespeak-ng/la-sPlayer.lo
src/libespeak-ng/wavegen.c: In function ‘WavegenFill’:
src/libespeak-ng/wavegen.c:1404:17: warning: variable ‘p_start’ set but not used [-Wunused-but-set-variable]
 1404 |  unsigned char *p_start;
      |                 ^~~~~~~
src/libespeak-ng/wavegen.c: In function ‘espeak_ng_SetConstF0’:
src/libespeak-ng/wavegen.c:1439:1: warning: control reaches end of non-void function [-Wreturn-type]
 1439 | }
      | ^
src/libespeak-ng/sPlayer.c:97:6: warning: no previous prototype for ‘KlattInitSP’ [-Wmissing-prototypes]
   97 | void KlattInitSP() {
      |      ^~~~~~~~~~~
src/libespeak-ng/sPlayer.c:101:6: warning: no previous prototype for ‘KlattResetSP’ [-Wmissing-prototypes]
  101 | void KlattResetSP() {
      |      ^~~~~~~~~~~~
src/libespeak-ng/sPlayer.c:11:12: warning: ‘MAX’ defined but not used [-Wunused-function]
   11 | static int MAX(int a, int b) { return((a) > (b) ? a : b); }
      |            ^~~
  CXX      src/speechPlayer/src/frame.lo
  CXX      src/speechPlayer/src/speechPlayer.lo
  CXX      src/speechPlayer/src/speechWaveGenerator.lo
  CC       src/libespeak-ng/la-mbrowrap.lo
  CC       src/libespeak-ng/la-espeak_command.lo
src/libespeak-ng/mbrowrap.c: In function ‘mbrola_has_errors’:
src/libespeak-ng/mbrowrap.c:359:15: warning: ‘%s’ directive output may be truncated writing up to 255 bytes into a region of size 160 [-Wformat-truncation=]
  359 |              "%s", buf_ptr);
      |               ^~
In file included from /usr/include/stdio.h:866,
                 from src/include/compat/stdio.h:30,
                 from src/libespeak-ng/mbrowrap.c:78:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:70:10: note: ‘__builtin_snprintf’ output between 1 and 256 bytes into a destination of size 160
   70 |   return __builtin___snprintf_chk (__s, __n, __USE_FORTIFY_LEVEL - 1,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   71 |        __bos (__s), __fmt, __va_arg_pack ());
      |        ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  CC       src/libespeak-ng/la-event.lo
  CC       src/libespeak-ng/la-fifo.lo
  CXXLD    src/libespeak-ng.la
  CCLD     src/espeak-ng
  CXXLD    src/speak-ng
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$

## make docs

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make docs
Makefile:2783: warning: ignoring prerequisites on suffix rule definition
  MD        docs/add_language.html
/bin/bash: line 1: no: command not found
make: *** [Makefile:2784: docs/add_language.html] Error 127
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ which bash
/usr/bin/bash
```

## Update Makefile

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ gedit Makefile

#SHELL = /bin/bash
SHELL = /usr/bin/bash
```

## try again make docs

Error က အောက်ပါ လိုင်းနဲ့ ဆိုင်တာကို တွေ့ရ

```
2784   .md.html: _layouts/webpage.html
2785   	@echo "  MD        $@"
2786   	@cat $< | sed -e 's/\.md)/.html)/g' -e 's/\.ronn/.html/g' | \
2787   		$(KRAMDOWN) --template _layouts/webpage.html > $@
```

လိုင်း 618 မှာ အောက်ပါ setting ကို တွေ့ရ...

```
KRAMDOWN = no
```

no ဆိုတဲ့ setting ကြောင့်လို့ ယူဆ။

## Installation of Kramdown

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ sudo gem install kramdown
Fetching kramdown-2.3.0.gem
Successfully installed kramdown-2.3.0
Parsing documentation for kramdown-2.3.0
Installing ri documentation for kramdown-2.3.0
Done installing documentation for kramdown after 0 seconds
1 gem installed
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ which kramdown 
/usr/local/bin/kramdown
```

## Edit Makefile and Retry

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ which kramdown 
/usr/local/bin/kramdown
```

gedit Makefile
```
618    KRAMDOWN = yes
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ sudo make docs
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
  MD        docs/guide.html
yes: unrecognized option '--template'
Try 'yes --help' for more information.
make: *** [Makefile:2785: docs/guide.html] Error 1
```

I skip make docs ...

## check languages

https://github.com/espeak-ng/espeak-ng/blob/master/docs/languages.md#:~:text=Development%20version%20of%20eSpeak%20NG,are%20listed%20in%20table%20below.

## compile for Myanmar languages

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make my
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
ESPEAK_DATA_PATH=/home/ye/tool/espeak-ng src/espeak-ng --compile-intonations && \
	ESPEAK_DATA_PATH=/home/ye/tool/espeak-ng src/espeak-ng --compile-phonemes && \
	touch phsource/phonemes.stamp
Compiled 30 intonation tunes: 0 errors.
Unknown phoneme table: 'en'
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/en_dict'
Compiling phoneme data: /home/ye/tool/espeak-ng/espeak-ng-data/../phsource/phonemes

Refs 4279,  Reused 3309
Compiled phonemes: 0 errors.
touch dictsource/my_extra
  DICT      espeak-ng-data/my_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/my_dict'
Using phonemetable: 'my'
Compiling: 'my_list'
	11 entries
Compiling: 'my_emoji'
	1644 entries
Compiling: 'my_extra'
	0 entries
Compiling: 'my_rules'
	78 rules, 64 groups (0)

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$
```

## make for Burmese language

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ find /usr/lib | grep libespeak-ng
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1.1.49
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ 
```

## make for all support languages

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
make  all-am
make[1]: Entering directory '/home/ye/tool/espeak-ng'
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
touch dictsource/af_extra
  DICT      espeak-ng-data/af_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/af_dict'
Using phonemetable: 'af'
Compiling: 'af_list'
	1584 entries
Compiling: 'af_emoji'
	1639 entries
Compiling: 'af_extra'
	0 entries
Compiling: 'af_rules'
	5202 rules, 60 groups (0)

touch dictsource/am_extra
  DICT      espeak-ng-data/am_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/am_dict'
Using phonemetable: 'am'
Compiling: 'am_list'
	31 entries
Compiling: 'am_emoji'
	1639 entries
Compiling: 'am_extra'
	0 entries
Compiling: 'am_rules'
	345 rules, 7 groups (0)

touch dictsource/an_extra
  DICT      espeak-ng-data/an_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/an_dict'
Using phonemetable: 'an'
Compiling: 'an_list'
	484 entries
Compiling: 'an_extra'
	0 entries
Compiling: 'an_rules'
	184 rules, 29 groups (0)

touch dictsource/ar_extra
  DICT      espeak-ng-data/ar_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/ar_dict'
Using phonemetable: 'ar'
Compiling: 'ar_listx'
	30089 entries
Compiling: 'ar_list'
	251 entries
Compiling: 'ar_emoji'
	1639 entries
Compiling: 'ar_extra'
	0 entries
Compiling: 'ar_rules'
	383 rules, 39 groups (37)

touch dictsource/as_extra
  DICT      espeak-ng-data/as_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/as_dict'
Using phonemetable: 'as'
Compiling: 'as_list'
	209 entries
Compiling: 'as_extra'
	0 entries
Compiling: 'as_rules'
	146 rules, 66 groups (66)

touch dictsource/az_extra
  DICT      espeak-ng-data/az_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/az_dict'
Using phonemetable: 'az'
Compiling: 'az_list'
	84 entries
Compiling: 'az_emoji'
	1639 entries
Compiling: 'az_extra'
	0 entries
Compiling: 'az_rules'
	58 rules, 34 groups (0)

  DICT      espeak-ng-data/ba_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/ba_dict'
Using phonemetable: 'ba'
Compiling: 'ba_list'
	79 entries
Compiling: 'ba_rules'
	52 rules, 44 groups (0)

touch dictsource/bg_extra
  DICT      espeak-ng-data/bg_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/bg_dict'
Using phonemetable: 'bg'
Compiling: 'bg_listx'
	2790 entries
Compiling: 'bg_list'
	231 entries
Compiling: 'bg_emoji'
	1639 entries
Compiling: 'bg_extra'
	0 entries
Compiling: 'bg_rules'
	118 rules, 31 groups (30)

touch dictsource/bn_extra
  DICT      espeak-ng-data/bn_dict
Can't read dictionary file: '/home/ye/tool/espeak-ng/espeak-ng-data/bn_dict'
Using phonemetable: 'bn'
Compiling: 'bn_list'
	380 entries
Compiling: 'bn_emoji'
	1639 entries
Compiling: 'bn_extra'
	0 entries
Compiling: 'bn_rules'
	168 rules, 68 groups (67)

...
...
...
...
```

## make check

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make check
...
...
...
s;E2m t'ys;VtS;_! p;,It;s'ot d;E2v;Itn'AttsVt; p@-rats'Ent dv'A (en)s'i:(ru) ojd;'in t'otS;ka tS;It'yr;E2sta v'os;E2md;E2s;atv'os;E2m t'ys;VtS;_! p;,It;s'ot d;E2v;Itn'AttsVt; p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I ojd;'in p@-rats'Ent dv;'es;t;I t'otS;ka vOs;Ims'ot p;Vd;d;Is;'jats;'ejm t'ys;VtS;
---
> (en)s'i:(ru) n'ojl t'otS;ka# v'os;E2md;E2s;ats;'ejm m;,IlI;'onof_! p;,It;s'ot SE2z;d;d;Is;'jatd;'evI3t; t'ys;VtS;_! dv;'es;t;I p;Vd;d;Is;'jattR;'i p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I ojd;'in p@-rats'Ent dv;'es;t;I t'otS;ka# t@-r;'ittsat;S'Es;t; t'ys;VtS;_! vOs;Ims'ot s;Imn'AttsVt; p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# dv;'e t'ys;VdZ; d;E2v;Itn'AttsVt; p@-rats'Ent dv;'es;t;I ojd;'in t'otS;ka# n'ojl tR;'iv'os;E#m_!s;'ejm d;'evI3t;S'Es;t;_!tR;'i p@-rats'Ent dv'A (en)s'i:(ru) ojd;'in t'otS;ka# n'ojl tR;'iv'os;E#m_!s;'ejm d;'evI3t;S'Es;t;_!tR;'i p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I ojd;'in p@-rats'Ent dv;'es;t;I t'otS;ka# tS;It'yr;E2sta# d;E2v;Itn'AttsVt; t'ys;VtS;_! S,E#s;t;s'ot t@-r;'ittsat;s;'ejm p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# n'ojldv'A_! tR;'is;'ejm_!p;'jat; p@-rats'Ent dv'AttsVt; (en)s'i:(ru) p@-rats'Ent dv;'es;t;I t'otS;ka# t@-r;'ittsVt; t'ys;VtS;_! v'os;E2md;E2s;ats;'ejm p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# n'ojltS;It'yR;I_! p;'jat;Vjd;'in_!tS;It'yR;I p@-rats'Ent dv;'es;t;I t'otS;ka# p;,It;s'ot v'os;E2md;E2s;atdv;'e t'ys;VtS;_! s;,Ims'ot t@-r;'ittsat;d;'evI3t; p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# dv;'es;t;I SE#stn'AttsVt; t'ys;VtS;_! dev;ats'ot s'o@-*Okdv'A p@-rats'Ent dv;'es;t;I t'otS;ka# s;,Ims'ot p;Vd;d;Is;'jat t'ys;VtS;_! p;,It;s'ot d;E2v;In'ostOtR;'i p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# tS;It'yr;E2sta# s;'emd;E2s;Vt t'ys;VtS;_! t@-r;'ista# v'os;E2m p@-rats'Ent dv;'es;t;I t'otS;ka# n'ojld;'evI3t;_! p;'jat;n'ojl_!dv'A p@-rats'Ent dv'A (en)s'i:(ru) n'ojl t'otS;ka# st'o s'o@-*Okdv;'e t'ys;VtS;_! p;,It;s'ot s;Imn'AttsVt; p@-rats'Ent
> dv'A (en)s'i:(ru) v'os;E2m t'otS;ka# vOs;Ims'ot dv'Attsat;d;'evI3t; t'ys;VtS;_! s;,Ims'ot SE2z;d;d;Is;'jatv'os;E2m p@-rats'Ent dv'AttsVt; (en)s'i:(ru) p@-rats'Ent dv;'es;t;I p@-rats'Ent dv'A (en)s'i:(ru) p;'jat; t'otS;ka# S,E#s;t;s'ot SE2z;d;d;Is;'jatd;'evI3t; t'ys;VtS;_! s'o@-*Okojd;'in p@-rats'Ent dv'AttsVt; tS;It'yR;I t'otS;ka# p;Vd;d;Is;'jatd;'evI3t; t'ys;VtS;_! S,E#s;t;s'ot d;E2v;In'ostOd;'evI3t; p@-rats'Ent dv'A (en)s'i:(ru) d;'es;It; t'otS;ka# dv'A m;,IlI;'onof_! S,E#s;t;s'ot p;Vd;d;Is;'jatdv;'e t'ys;VtS;_! t@-r;'ista# d;E2v;In'ostOojd;'in p@-rats'Ent dv'AttsVt; d;'es;It; t'otS;ka# dv;'es;t;I SE2z;d;d;Is;'jatp;'jat; t'ys;VtS;_! dv;'es;t;I t@-r;'ittsat;v'os;E2m p@-rats'Ent dv'A (en)s'i:(ru) d;'es;It; t'otS;ka# dv'A m;,IlI;'onof_! S,E#s;t;s'ot p;Vd;d;Is;'jatdv;'e t'ys;VtS;_! t@-r;'ista# d;E2v;In'ostOojd;'in p@-rats'Ent dv'AttsVt; (en)z'Ed(ru) p@-rats'Ent dv'AttsVt; (en)'Em(ru) p@-rats'Ent dv;'e t'ys;VdZ; d;'es;It; t'otS;ka# n'ojltR;'i_!s;'ejm v'os;E#mS'Es;t;_!p;'jat; p@-rats'Ent dv'A (en)s'i:(ru) d;E2v;Itn'AttsVt; t'otS;ka# s;,Ims'ot d;E2v;In'ostOv'os;E2m t'ys;VtS;_! p;,It;s'ot t@-r;'ittsat;s;'ejm p@-rats'Ent dv'AttsVt; (en)v'i:(ru) p@-rats'Ent dv;'es;t;I ojd;'in t'otS;ka# st'o s;'emd;E2s;VttS;It'yR;I t'ys;VtS;_! st'o v'os;E2md;E2s;atv'os;E2m p@-rats'Ent dv'AttsVt; (en)'eI(ru) p@-rats'Ent dv;'es;t;I ojd;'in t'otS;ka# tS;It'yr;E2sta# v'os;E2md;E2s;atv'os;E2m t'ys;VtS;_! p;,It;s'ot d;E2v;Itn'AttsVt; p@-rats'Ent dv'A (en)s'i:(ru) ojd;'in t'otS;ka# tS;It'yr;E2sta# v'os;E2md;E2s;atv'os;E2m t'ys;VtS;_! p;,It;s'ot d;E2v;Itn'AttsVt; p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I p@-rats'Ent dv;'es;t;I ojd;'in p@-rats'Ent dv;'es;t;I t'otS;ka# vOs;Ims'ot p;Vd;d;Is;'jats;'ejm t'ys;VtS;
make: *** [Makefile:2809: tests/translate.check] Error 1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ make check
```

## make library

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ sudo make LIBDIR=/usr/lib/x86_64-linux-gnu install
[sudo] password for ye: 
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
make[1]: Entering directory '/home/ye/tool/espeak-ng'
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
 /usr/bin/mkdir -p '/usr/local/lib'
 /usr/bin/bash ./libtool   --mode=install /usr/bin/install -c   src/libespeak-ng.la '/usr/local/lib'
libtool: install: /usr/bin/install -c src/.libs/libespeak-ng.so.1.1.51 /usr/local/lib/libespeak-ng.so.1.1.51
libtool: install: (cd /usr/local/lib && { ln -s -f libespeak-ng.so.1.1.51 libespeak-ng.so.1 || { rm -f libespeak-ng.so.1 && ln -s libespeak-ng.so.1.1.51 libespeak-ng.so.1; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f libespeak-ng.so.1.1.51 libespeak-ng.so || { rm -f libespeak-ng.so && ln -s libespeak-ng.so.1.1.51 libespeak-ng.so; }; })
libtool: install: /usr/bin/install -c src/.libs/libespeak-ng.lai /usr/local/lib/libespeak-ng.la
libtool: install: /usr/bin/install -c src/.libs/libespeak-ng.a /usr/local/lib/libespeak-ng.a
libtool: install: chmod 644 /usr/local/lib/libespeak-ng.a
libtool: install: ranlib /usr/local/lib/libespeak-ng.a
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
  /usr/bin/bash ./libtool   --mode=install /usr/bin/install -c src/speak-ng src/espeak-ng '/usr/local/bin'
libtool: install: /usr/bin/install -c src/speak-ng /usr/local/bin/speak-ng
libtool: install: /usr/bin/install -c src/.libs/espeak-ng /usr/local/bin/espeak-ng
make  install-exec-hook
make[2]: Entering directory '/home/ye/tool/espeak-ng'
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
cd /usr/local/bin && rm -f espeak && ln -s espeak-ng espeak
cd /usr/local/bin && rm -f speak  && ln -s speak-ng speak
cd /usr/lib/x86_64-linux-gnu && rm -f libespeak.la && ln -s libespeak-ng.la libespeak.la
make[2]: Leaving directory '/home/ye/tool/espeak-ng'
 /usr/bin/mkdir -p '/usr/local/include/espeak'
 /usr/bin/install -c -m 644 src/include/espeak/speak_lib.h '/usr/local/include/espeak'
 /usr/bin/mkdir -p '/usr/local/include/espeak-ng'
 /usr/bin/install -c -m 644 src/include/espeak-ng/encoding.h src/include/espeak-ng/espeak_ng.h src/include/espeak-ng/speak_lib.h '/usr/local/include/espeak-ng'
 /usr/bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 espeak-ng.pc '/usr/local/lib/pkgconfig'
 /usr/bin/mkdir -p '/usr/local/share/vim/addons/ftdetect'
 /usr/bin/install -c -m 644 ./vim/ftdetect/espeakfiletype.vim '/usr/local/share/vim/addons/ftdetect'
 /usr/bin/mkdir -p '/usr/local/share/vim/addons/syntax'
 /usr/bin/install -c -m 644 ./vim/syntax/espeaklist.vim ./vim/syntax/espeakrules.vim '/usr/local/share/vim/addons/syntax'
 /usr/bin/mkdir -p '/usr/local/share/vim/registry'
 /usr/bin/install -c -m 644 ./vim/registry/espeak.yaml '/usr/local/share/vim/registry'
make  install-data-hook
make[2]: Entering directory '/home/ye/tool/espeak-ng'
Makefile:2784: warning: ignoring prerequisites on suffix rule definition
rm -rf /usr/local/share/espeak-ng-data
mkdir -p /usr/local/share/espeak-ng-data
cp -prf espeak-ng-data/* /usr/local/share/espeak-ng-data
make[2]: Leaving directory '/home/ye/tool/espeak-ng'
make[1]: Leaving directory '/home/ye/tool/espeak-ng'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ find /usr/lib | grep libespeak-ng
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1
/usr/lib/x86_64-linux-gnu/libespeak-ng.so.1.1.49
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$
```

## checkin with TAB

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak
espeak     espeak-ng 
```

## checking with --help

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak-ng --help

eSpeak NG text-to-speech: 1.50  Data at: /usr/lib/x86_64-linux-gnu/espeak-ng-data

espeak-ng [options] ["<words>"]

-f <text file>   Text file to speak
--stdin    Read text input from stdin at once till to the end of a stream.

If neither -f nor --stdin are provided, then <words> from arguments are spoken,
or text is spoken from stdin, read separately one line by line at a time.

-a <integer>
	   Amplitude, 0 to 200, default is 100
-d <device>
	   Use the specified device to speak the audio on. If not specified, the
	   default audio device is used.
-g <integer>
	   Word gap. Pause between words, units of 10mS at the default speed
-k <integer>
	   Indicate capital letters with: 1=sound, 2=the word "capitals",
	   higher values indicate a pitch increase (try -k20).
-l <integer>
	   Line length. If not zero (which is the default), consider
	   lines less than this length as end-of-clause
-p <integer>
	   Pitch adjustment, 0 to 99, default is 50
-s <integer>
	   Speed in approximate words per minute. The default is 175
-v <voice name>
	   Use voice file of this name from espeak-ng-data/voices
-w <wave file name>
	   Write speech to this WAV file, rather than speaking it directly
-b	   Input text encoding, 1=UTF8, 2=8 bit, 4=16 bit 
-m	   Interpret SSML markup, and ignore other < > tags
-q	   Quiet, don't produce any speech (may be useful with -x)
-x	   Write phoneme mnemonics to stdout
-X	   Write phonemes mnemonics and translation trace to stdout
-z	   No final sentence pause at the end of the text
--compile=<voice name>
	   Compile pronunciation rules and dictionary from the current
	   directory. <voice name> specifies the language
--compile-debug=<voice name>
	   Compile pronunciation rules and dictionary from the current
	   directory, including line numbers for use with -X.
	   <voice name> specifies the language
--compile-mbrola=<voice name>
	   Compile an MBROLA voice
--compile-intonations
	   Compile the intonation data
--compile-phonemes=<phsource-dir>
	   Compile the phoneme data using <phsource-dir> or the default phsource directory
--ipa      Write phonemes to stdout using International Phonetic Alphabet
--path="<path>"
	   Specifies the directory containing the espeak-ng-data directory
--pho      Write mbrola phoneme data (.pho) to stdout or to the file in --phonout
--phonout="<filename>"
	   Write phoneme output from -x -X --ipa and --pho to this file
--punct="<characters>"
	   Speak the names of punctuation characters during speaking.  If
	   =<characters> is omitted, all punctuation is spoken.
--sep=<character>
	   Separate phonemes (from -x --ipa) with <character>.
	   Default is space, z means ZWJN character.
--split=<minutes>
	   Starts a new WAV file every <minutes>.  Used with -w
--stdout   Write speech output to stdout
--tie=<character>
	   Use a tie character within multi-letter phoneme names.
	   Default is U+361, z means ZWJ character.
--version  Shows version number and date, and location of espeak-ng-data
--voices=<language>
	   List the available voices for the specified language.
	   If <language> is omitted, then list all voices.
--load     Load voice from a file in current directory by name.
-h, --help Show this help.
```

## Check for Myanmar language

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak-ng --voices=my
Pty Language       Age/Gender VoiceName          File                 Other Languages
 5  my              --/M      Myanmar_(Burmese)  sit/my               
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$
```

## Testing

--ipa option ပေးပြီး IPA symbol ကို print ထုတ်ကြည့်ခဲ့...

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak-ng -v my --ipa
ရဲကျော်သူ
jˌateˈau2  ðˈu1
နေကောင်းလား
neɜkˈau2ŋ  lts
မင်းအသံက ဘယ်လိုအသံလဲကွာ
mŋ  ə2ðˈak bj  lˌoəðalˈakwats
နားကိုမလည်ဘူး
ntskˈo2mlŋ  bˈu2
မဟုတ်သေးပါဘူး
mhˈuɜt  ðe2pˈebu2
```

ဗမာအသံထွက်လည်း အဆင်မပြေ၊ IPA symbol ကလည်း အဆင်မပြေသေးတာကို တွေ့ရ...

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak-ng -v en --ipa
who are you
hˈuː ɑː juː
are you ok?
ɑː juː ˌəʊkˈeɪ
I have a computer
aɪ hav ɐ kəmpjˈuːtə
I am a researcher
aɪɐm ɐ ɹɪsˈɜːtʃə
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/espeak-ng$ espeak-ng -v zh --ipa
中新网2月15日电 综合报道，英国哈里王子和妻子梅根正准备迎接他们的第二个孩子。
ts.ˈonɡ5 ɕˈi5n wˈɑ2ŋ ˈər5 ˈyɛ5 ji5wˈu2 ʐˈi.5 tˈiɛ5n tsˈonɡ5 xˈo-ɜ pˈɑu5 tˈɑu5
jˈi5ŋ kˈuoɜ xˈɑ5 lˈi2 wˈɑɜŋ tsi̪ɜ xˈo-ɜ tɕhˈi5 tsi̪2 mˈeiɜ kˈə5n ts.ˈə5ŋ ts.ˈuə2n pˈei5 jˈiɜŋ tɕˈiɛ5 thˈɑ5 mə2n tə1 tˈi5 ˈər5 ko-1 xˈaiɜ tsi̪ɜ
哈里夫妇的发言人14日证实，39岁的梅根已怀有身孕。
xˈɑ5 lˈi2 fu4 fˈu5 tə1 fˈɑ5 jˈiɛɜn ʐˈəɜn ji5sˈi̪5 ʐˈi.5 ts.ˈə5ŋ s.ˈi.ɜ
sa5ntɕˈiou2 sˈuei5 tə1 mˈeiɜ kˈə5n jˈi2 xˈuaiɜ jˈiou2 s.ˈə5n ʲˈyə5n
```
