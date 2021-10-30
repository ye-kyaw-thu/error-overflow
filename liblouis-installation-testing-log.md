# liblouis Installation and Testing Log

## git clone

```
(base) ye@:/media/ye/project1/exp$ git clone https://github.com/liblouis/liblouis
Cloning into 'liblouis'...
remote: Enumerating objects: 31979, done.
remote: Counting objects: 100% (1228/1228), done.
remote: Compressing objects: 100% (444/444), done.
remote: Total 31979 (delta 816), reused 1112 (delta 757), pack-reused 30751
Receiving objects: 100% (31979/31979), 78.70 MiB | 13.96 MiB/s, done.
Resolving deltas: 100% (23479/23479), done.
(base) ye@:/media/ye/project1/exp$ cd liblouis/
(base) ye@:/media/ye/project1/exp/liblouis$ ls
ANNOUNCEMENT  ChangeLog     COPYING.LESSER    Dockerfile.win64  HACKING              License.md   NEWS       README.windows  tools
AUTHORS       configure.ac  doc               Doxyfile          liblouis             m4           python     tables          windows
autogen.sh    contrib       Dockerfile        extra             liblouis.pc.in       Makefile.am  README     tests
build-aux     COPYING       Dockerfile.win32  gnulib            libyaml_mingw.patch  man          README.md  TODO
(base) ye@:/media/ye/project1/exp/liblouis$
```

## run ./configure and got error

./configure ကို run တော့ configure ဖိုင် မရှိသေးဘူးဆိုတဲ့ ERROR ကို အောက်ပါအတိုင်း ပေးတယ်။  

```
(base) ye@:/media/ye/project1/exp/liblouis$ ./configure --enable-ucs4
bash: ./configure: No such file or directory
(base) ye@:/media/ye/project1/exp/liblouis$
```

## run autoreconf

အဲဒါကြောင့် autoreconf နဲ့ ./configure ဖိုင်ကို ထုတ်ခဲ့တယ်...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ autoreconf --verbose --install --force
autoreconf: Entering directory `.'
autoreconf: configure.ac: not using Gettext
autoreconf: running: aclocal --force -I m4 -I gnulib/m4 -I tools/gnulib/m4
autoreconf: configure.ac: tracing
autoreconf: running: libtoolize --copy --force
libtoolize: putting auxiliary files in AC_CONFIG_AUX_DIR, 'build-aux'.
libtoolize: copying file 'build-aux/ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
autoreconf: running: /usr/bin/autoconf --force
autoreconf: running: /usr/bin/autoheader --force
autoreconf: running: automake --add-missing --copy --force-missing
configure.ac:17: installing 'build-aux/ar-lib'
configure.ac:14: installing 'build-aux/compile'
configure.ac:21: installing 'build-aux/config.guess'
configure.ac:21: installing 'build-aux/config.sub'
configure.ac:10: installing 'build-aux/install-sh'
configure.ac:10: installing 'build-aux/missing'
Makefile.am: installing './INSTALL'
doc/Makefile.am:11: installing 'build-aux/mdate-sh'
doc/Makefile.am:11: installing 'build-aux/texinfo.tex'
gnulib/Makefile.am: installing 'build-aux/depcomp'
parallel-tests: installing 'build-aux/test-driver'
autoreconf: Leaving directory `.'
(base) ye@:/media/ye/project1/exp/liblouis$
```

configure ဖိုင် ထွက်လာပြီ...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ ls configure*
configure  configure.ac
```

## run ./configure

./configure ကို --enable-ucs4 ဆိုတဲ့ option ပါဖြည့်ပြီး run ခဲ့တယ်။  
README ဖိုင်ကို refer လုပ်ပါ  

```
(base) ye@:/media/ye/project1/exp/liblouis$ ./configure --enable-ucs4
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
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
checking for gcc option to accept ISO C99... none needed
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
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
checking minix/config.h usability... no
checking minix/config.h presence... no
checking for minix/config.h... no
checking whether it is safe to define __EXTENSIONS__... yes
checking whether _XOPEN_SOURCE should be defined... no
checking for Minix Amsterdam compiler... no
checking for ar... ar
checking the archiver (ar) interface... ar
checking for ar... (cached) ar
checking for ranlib... ranlib
checking for gcc option to accept ISO C99... (cached) none needed
checking for gcc option to accept ISO Standard C... (cached) none needed
checking for size_t... yes
checking for working alloca.h... yes
checking for alloca... yes
checking whether the preprocessor supports include_next... yes
checking whether system header files limit the line length... no
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for dirent.h... yes
checking for unistd.h... (cached) yes
checking for limits.h... yes
checking for wchar.h... yes
checking for stdint.h... (cached) yes
checking for getopt.h... yes
checking for sys/cdefs.h... yes
checking for sys/socket.h... yes
checking if environ is properly declared... yes
checking whether limits.h has LLONG_MAX, WORD_BIT, ULLONG_WIDTH etc.... yes
checking whether malloc, realloc, calloc are POSIX compliant... yes
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... yes
checking for unsigned long long int... yes
checking for long long int... yes
checking whether setenv is declared... yes
checking for setenv... yes
checking for strndup... yes
checking for getprogname... no
checking for getexecname... no
checking for _set_invalid_parameter_handler... no
checking search.h usability... yes
checking search.h presence... yes
checking for search.h... yes
checking for tsearch... yes
checking for wchar_t... yes
checking for wint_t... yes
checking whether wint_t is too small... no
checking whether stdint.h conforms to C99... yes
checking whether stdint.h predates C++11... no
checking whether stdint.h has UINTMAX_WIDTH etc.... yes
checking for C/C++ restrict keyword... __restrict
checking whether strndup is declared... yes
checking whether strnlen is declared... yes
checking for pid_t... yes
checking for mode_t... yes
checking for alloca as a compiler built-in... yes
checking if gcc/ld supports -Wl,--output-def... no
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... (cached) yes
checking for stdlib.h... (cached) yes
checking for GNU libc compatible realloc... yes
checking whether setenv validates arguments... yes
checking for ssize_t... yes
checking for good max_align_t... yes
checking whether NULL can be used in arbitrary expressions... yes
checking for working strndup... yes
checking for working strnlen... yes
checking whether // is distinct from /... no
checking for complete errno.h... yes
checking whether strerror_r is declared... yes
checking for strerror_r... yes
checking whether strerror_r returns char *... yes
checking for getopt.h... (cached) yes
checking for getopt_long_only... yes
checking whether getopt is POSIX compatible... yes
checking for working GNU getopt function... yes
checking for working GNU getopt_long function... yes
checking for inline... inline
checking for stdbool.h that conforms to C99... yes
checking for _Bool... yes
checking whether strerror(0) succeeds... yes
checking whether // is distinct from /... (cached) no
checking for error_at_line... yes
checking whether program_invocation_name is declared... yes
checking whether program_invocation_short_name is declared... yes
checking whether __argv is declared... no
checking whether the compiler generally respects inline... yes
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... (cached) yes
checking whether program_invocation_name is declared... (cached) yes
checking whether program_invocation_short_name is declared... (cached) yes
checking for stdlib.h... (cached) yes
checking for GNU libc compatible realloc... (cached) yes
checking for ssize_t... (cached) yes
checking for va_copy... yes
checking for good max_align_t... (cached) yes
checking whether NULL can be used in arbitrary expressions... (cached) yes
checking which flavor of printf attribute matches inttypes macros... system
checking for working strerror function... yes
checking for working strndup... (cached) yes
checking for working strnlen... (cached) yes
checking whether ln -s works... no, using cp -pR
checking whether make sets $(MAKE)... (cached) yes
checking the archiver (ar) interface... (cached) ar
checking for yaml_parser_initialize in -lyaml... no
configure: WARNING: libyaml was not found. YAML tests will be skipped
checking for ANSI C header files... (cached) yes
checking stddef.h usability... yes
checking stddef.h presence... yes
checking for stddef.h... yes
checking for stdlib.h... (cached) yes
checking for string.h... (cached) yes
checking for an ANSI C-conforming const... yes
checking for working memcmp... yes
checking for vprintf... yes
checking for _doprnt... no
checking for memset... yes
checking for library containing strerror... none required
checking for ANSI C header files... (cached) yes
checking how to print strings... printf
checking for a sed that does not truncate output... /usr/bin/sed
checking for fgrep... /usr/bin/grep -F
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
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... (cached) ranlib
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
checking whether -Wno-missing-field-initializers is supported... yes
checking whether -Wno-missing-field-initializers is needed... no
checking whether -Wuninitialized is supported... yes
checking max safe object size... 9223372036854775807
checking whether C compiler handles -Werror -Wunknown-warning-option... no
checking whether C compiler handles -fno-common... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -W... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wabsolute-value... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Waddress... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Waddress-of-packed-member... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Waggressive-loop-optimizations... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wall... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wattribute-warning... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wattributes... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wbad-function-cast... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wbool-compare... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wbool-operation... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wbuiltin-declaration-mismatch... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wbuiltin-macro-redefined... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcannot-profile... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcast-align... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcast-align=strict... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcast-function-type... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wchar-subscripts... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wclobbered... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcomment... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcomments... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcoverage-mismatch... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wcpp... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdangling-else... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdate-time... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdeprecated... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdeprecated-declarations... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdesignated-init... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdisabled-optimization... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdiscarded-array-qualifiers... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdiscarded-qualifiers... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdiv-by-zero... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wdouble-promotion... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wduplicated-branches... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wduplicated-cond... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wduplicate-decl-specifier... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wempty-body... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wendif-labels... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wenum-compare... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wexpansion-to-defined... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wextra... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-contains-nul... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-extra-args... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-nonliteral... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-security... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-signedness... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-y2k... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-zero-length... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wframe-address... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wfree-nonheap-object... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Whsa... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wif-not-aligned... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wignored-attributes... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wignored-qualifiers... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wimplicit... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wimplicit-function-declaration... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wimplicit-int... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wincompatible-pointer-types... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Winit-self... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Winline... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wint-conversion... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wint-in-bool-context... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wint-to-pointer-cast... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Winvalid-memory-model... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Winvalid-pch... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wlogical-not-parentheses... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wlogical-op... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmain... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmaybe-uninitialized... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmemset-elt-size... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmemset-transposed-args... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmisleading-indentation... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-attributes... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-braces... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-declarations... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-field-initializers... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-include-dirs... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-parameter-type... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-profile... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmissing-prototypes... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmultichar... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wmultistatement-macros... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnarrowing... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnested-externs... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnonnull... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnonnull-compare... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnull-dereference... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wodr... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wold-style-declaration... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wold-style-definition... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wopenmp-simd... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Woverflow... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Woverlength-strings... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Woverride-init... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpacked... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpacked-bitfield-compat... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpacked-not-aligned... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wparentheses... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpointer-arith... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpointer-compare... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpointer-sign... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpointer-to-int-cast... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpragmas... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wpsabi... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wrestrict... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wreturn-local-addr... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wreturn-type... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wscalar-storage-order... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsequence-point... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wshadow... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wshift-count-negative... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wshift-count-overflow... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wshift-negative-value... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsizeof-array-argument... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsizeof-pointer-div... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsizeof-pointer-memaccess... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstack-protector... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstrict-aliasing... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstrict-overflow... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstrict-prototypes... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstringop-truncation... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsuggest-attribute=cold... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsuggest-attribute=malloc... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsuggest-final-methods... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsuggest-final-types... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wswitch... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wswitch-bool... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wswitch-unreachable... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wsync-nand... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wtautological-compare... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wtrampolines... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wtrigraphs... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wtype-limits... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wuninitialized... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunknown-pragmas... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunsafe-loop-optimizations... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-but-set-parameter... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-but-set-variable... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-function... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-label... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-local-typedefs... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-macros... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-parameter... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-result... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-value... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-variable... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvarargs... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvariadic-macros... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvector-operation-performance... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvla... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvolatile-register-var... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wwrite-strings... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Walloc-size-larger-than=9223372036854775807... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Warray-bounds=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wattribute-alias=2... no
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-overflow=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wformat-truncation=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wimplicit-fallthrough=5... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wnormalized=nfc... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wshift-overflow=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wstringop-overflow=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wunused-const-variable=2... yes
checking whether C compiler handles -Werror -Wunknown-warning-option... (cached) no
checking whether C compiler handles -Wvla-larger-than=4031... yes
checking for clang-format-7... no
checking for clang-format... no
checking for help2man... no
checking for a sed that does not truncate output... (cached) /usr/bin/sed
checking for makeinfo... yes
checking for makeinfo version >= 5... yes
checking whether 4 byte-wide characters should be supported... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating doc/Makefile
config.status: creating man/Makefile
config.status: creating liblouis/Makefile
config.status: creating liblouis/liblouis.h
config.status: creating windows/Makefile
config.status: creating windows/include/Makefile
config.status: creating windows/utils/Makefile
config.status: creating tables/Makefile
config.status: creating liblouis.pc
config.status: creating tests/Makefile
config.status: creating tests/braille-specs/Makefile
config.status: creating tests/resolve_table.h
config.status: creating tests/tables/Makefile
config.status: creating tests/tables/emphclass/Makefile
config.status: creating tests/tables/attribute/Makefile
config.status: creating tests/tables/moreTables/Makefile
config.status: creating tests/tables/resolve_table/Makefile
config.status: creating tests/tables/resolve_table/dir_1/Makefile
config.status: creating tests/tables/resolve_table/dir_1/dir_1.1/Makefile
config.status: creating tests/tables/resolve_table/dir_2/Makefile
config.status: creating tests/tablesWithMetadata/Makefile
config.status: creating tests/ueb_test_data/Makefile
config.status: creating tests/yaml/Makefile
config.status: creating python/Makefile
config.status: creating python/setup.py
config.status: creating python/louis/Makefile
config.status: creating tools/Makefile
config.status: creating tools/gnulib/Makefile
config.status: creating tools/lou_maketable.d/Makefile
config.status: creating tools/lou_maketable.d/lou_maketable
config.status: creating gnulib/Makefile
config.status: creating liblouis/config.h
config.status: executing depfiles commands
config.status: executing libtool commands
(base) ye@:/media/ye/project1/exp/liblouis$
```

## run make

make ကို run တယ်...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ make
...
...
...
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/emphclass'
Making all in attribute
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[3]: Nothing to be done for 'all'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables'
make[3]: Nothing to be done for 'all-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables'
Making all in tablesWithMetadata
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
Making all in yaml
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/yaml'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/yaml'
Making all in braille-specs
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
Making all in ueb_test_data
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests'
make[2]: Nothing to be done for 'all-am'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/tests'
Making all in python
make[1]: Entering directory '/media/ye/project1/exp/liblouis/python'
Making all in louis
make[2]: Entering directory '/media/ye/project1/exp/liblouis/python/louis'
source ../../liblouis/liblouis.la ; \
sed "s/###LIBLOUIS_SONAME###/$dlname/" \
	< ./__init__.py.in \
	> __init__.py
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/python/louis'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/python'
make[2]: Nothing to be done for 'all-am'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/python'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/python'
Making all in windows
make[1]: Entering directory '/media/ye/project1/exp/liblouis/windows'
Making all in include
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows/include'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows/include'
Making all in utils
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows/utils'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows/utils'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows'
make[2]: Nothing to be done for 'all-am'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/windows'
Making all in doc
make[1]: Entering directory '/media/ye/project1/exp/liblouis/doc'
Updating ./version.texi
restore=: && backupdir=".am$$" && \
am__cwd=`pwd` && CDPATH="${ZSH_VERSION+.}:" && cd . && \
rm -rf $backupdir && mkdir $backupdir && \
if (/bin/bash /media/ye/project1/exp/liblouis/build-aux/missing makeinfo --version) >/dev/null 2>&1; then \
  for f in liblouis.info liblouis.info-[0-9] liblouis.info-[0-9][0-9] liblouis.i[0-9] liblouis.i[0-9][0-9]; do \
    if test -f $f; then mv $f $backupdir; restore=mv; else :; fi; \
  done; \
else :; fi && \
cd "$am__cwd"; \
if /bin/bash /media/ye/project1/exp/liblouis/build-aux/missing makeinfo   -I . \
 -o liblouis.info liblouis.texi; \
then \
  rc=0; \
  CDPATH="${ZSH_VERSION+.}:" && cd .; \
else \
  rc=$?; \
  CDPATH="${ZSH_VERSION+.}:" && cd . && \
  $restore $backupdir/* `echo "./liblouis.info" | sed 's|[^/]*$||'`; \
fi; \
rm -rf $backupdir; exit $rc
rm -rf liblouis.htp
if /bin/bash /media/ye/project1/exp/liblouis/build-aux/missing makeinfo --html --no-headers --no-split  -I . \
 -o liblouis.htp liblouis.texi; \
then \
  rm -rf liblouis.html && mv liblouis.htp liblouis.html; \
else \
  rm -rf liblouis.htp; exit 1; \
fi
/bin/bash /media/ye/project1/exp/liblouis/build-aux/missing makeinfo --plaintext liblouis.texi -o liblouis.txt
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/doc'
make[1]: Entering directory '/media/ye/project1/exp/liblouis'
make[1]: Nothing to be done for 'all-am'.
make[1]: Leaving directory '/media/ye/project1/exp/liblouis'
```

## run make install

make install ကို run တယ်...  
(sudo ခံပြီး run ခဲ့တယ်)  

```
(base) ye@:/media/ye/project1/exp/liblouis$ sudo make install
[sudo] password for ye: 
Making install in gnulib
make[1]: Entering directory '/media/ye/project1/exp/liblouis/gnulib'
make  install-recursive
make[2]: Entering directory '/media/ye/project1/exp/liblouis/gnulib'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/gnulib'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/gnulib'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/gnulib'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/gnulib'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/gnulib'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/gnulib'
Making install in liblouis
make[1]: Entering directory '/media/ye/project1/exp/liblouis/liblouis'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/liblouis'
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   liblouis.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/liblouis.so.20.0.7 /usr/local/lib/liblouis.so.20.0.7
libtool: install: (cd /usr/local/lib && { cp -pR -f liblouis.so.20.0.7 liblouis.so.20 || { rm -f liblouis.so.20 && cp -pR liblouis.so.20.0.7 liblouis.so.20; }; })
libtool: install: (cd /usr/local/lib && { cp -pR -f liblouis.so.20.0.7 liblouis.so || { rm -f liblouis.so && cp -pR liblouis.so.20.0.7 liblouis.so; }; })
libtool: install: /usr/bin/install -c .libs/liblouis.lai /usr/local/lib/liblouis.la
libtool: install: /usr/bin/install -c .libs/liblouis.a /usr/local/lib/liblouis.a
libtool: install: chmod 644 /usr/local/lib/liblouis.a
libtool: install: ranlib /usr/local/lib/liblouis.a
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /usr/local/lib
/sbin/ldconfig.real: /usr/local/lib/liblouis.so.20 is not a symbolic link

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
 /usr/bin/mkdir -p '/usr/local/include/liblouis'
 /usr/bin/install -c -m 644 liblouis.h '/usr/local/include/liblouis'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/liblouis'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/liblouis'
Making install in tools
make[1]: Entering directory '/media/ye/project1/exp/liblouis/tools'
Making install in gnulib
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make  install-recursive
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[5]: Entering directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[5]: Nothing to be done for 'install-exec-am'.
make[5]: Nothing to be done for 'install-data-am'.
make[5]: Leaving directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tools/gnulib'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tools/gnulib'
Making install in lou_maketable.d
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tools/lou_maketable.d'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tools/lou_maketable.d'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tools/lou_maketable.d'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tools/lou_maketable.d'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tools'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tools'
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c lou_allround lou_checkhyphens lou_checktable lou_debug lou_translate lou_trace lou_tableinfo '/usr/local/bin'
libtool: install: /usr/bin/install -c .libs/lou_allround /usr/local/bin/lou_allround
libtool: install: /usr/bin/install -c .libs/lou_checkhyphens /usr/local/bin/lou_checkhyphens
libtool: install: /usr/bin/install -c .libs/lou_checktable /usr/local/bin/lou_checktable
libtool: install: /usr/bin/install -c .libs/lou_debug /usr/local/bin/lou_debug
libtool: install: /usr/bin/install -c .libs/lou_translate /usr/local/bin/lou_translate
libtool: install: /usr/bin/install -c .libs/lou_trace /usr/local/bin/lou_trace
libtool: install: /usr/bin/install -c .libs/lou_tableinfo /usr/local/bin/lou_tableinfo
 /usr/bin/mkdir -p '/usr/local/bin'
 /usr/bin/install -c lou_maketable.d/lou_maketable '/usr/local/bin'
 /usr/bin/mkdir -p '/usr/local/bin'
 /usr/bin/mkdir -p '/usr/local/bin/lou_maketable.d/'
 /usr/bin/install -c lou_maketable.d/export_chunked_words.py lou_maketable.d/generate_alphabet.py lou_maketable.d/lou_maketable.mk lou_maketable.d/make_suggestions.py lou_maketable.d/submit_rows.py lou_maketable.d/submit_rows.sh lou_maketable.d/submit_rules.py lou_maketable.d/submit_rules.sh lou_maketable.d/substrings.pl lou_maketable.d/utils.py lou_maketable.d/wrap_patgen.sh '/usr/local/bin/lou_maketable.d/'
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tools'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tools'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/tools'
Making install in tables
make[1]: Entering directory '/media/ye/project1/exp/liblouis/tables'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tables'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 afr-za-g1.ctb afr-za-g2.ctb ar-ar-comp8.utb ar-ar-g1-core.uti ar-ar-g1.utb ar-ar-g2.ctb ar-ar-math.uti ar.tbl as-in-g1.utb as.tbl awa.tbl aw-in-g1.utb ba.utb be-in-g1.utb bel.utb bel-comp.utb bengali.cti bg.dis bg.ctb bg.tbl bg.utb bh.ctb bh.tbl bn.tbl bo.ctb bo.tbl boxes.ctb braille-patterns.cti bra.tbl br-in-g1.utb ca-chardefs.cti ca-g1.ctb ca.tbl chr-us-g1.ctb ckb-chardefs.cti ckb-g1.ctb ckb.tbl ckb-translation.cti compress.cti controlchars.cti '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 cop-eg-comp8.utb corrections.cti countries.cti cs-chardefs.cti cs-comp8.utb cs-g1.ctb cs-letterDef8Dots.uti cs.tbl cs-translation.cti cy-cy-g1.utb cy-cy-g2.ctb cy.tbl da-dk-6miscChars.cti da-dk-8miscChars.cti da-dk-g08.ctb da-dk-g16.ctb da-dk-g16-lit.ctb da-dk-g18.ctb da-dk-g26.ctb da-dk-g26l.ctb da-dk-g26-lit.ctb da-dk-g26l-lit.ctb da-dk-g28.ctb da-dk-g28l.ctb da-dk-octobraille.dis de-accents.cti de-accents-detailed.cti de-chardefs6.cti de-chardefs8.cti de-chess.ctb de-de-comp8.ctb de-de.dis de-eurobrl6.dis de-eurobrl6u.dis de-g0-core.uti de-g0.utb de-g0-bidi-core.uti de-g0-bidi.utb de-g1-core.cti de-g1-core-patterns.dic '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 de-g1.ctb de-g1-bidi.ctb de-g1-bidi-core.cti de-g2-core.cti de-g2-core-patterns.dic de-g2.ctb devanagari.cti digits6DotsPlusDot6.uti digits6Dots.uti digits8Dots.uti dra.ctb dra.tbl el.ctb en_CA.ctb en_CA.tbl en-chardefs.cti en-chess.ctb en-gb-comp8.ctb en-gb-g1.utb en-GB-g2.ctb en_GB.tbl en-in-g1.ctb en-nabcc.utb en-ueb-chardefs.uti en-ueb-g1.ctb en-ueb-g2.ctb en-ueb-math.ctb en-us-brf.dis en-us-comp6.ctb en-us-comp8.ctb en_US-comp8-ext.tbl en-us-comp8-ext.utb en-us-compbrl.uti en-us-emphasis.uti en-us-g1.ctb en-us-g2.ctb en-us-interline.ctb en-us-mathtext.ctb en_US.tbl eo-g1.ctb '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 eo-g1-x-system.ctb eo.tbl es-chardefs.cti Es-Es-G0.utb es-g1.ctb es-g2.ctb es-new.dis es-old.dis es.tbl et.ctb et-g0.utb ethio-g1.ctb et.tbl eurodefs.cti fa-ir-comp8.ctb fa-ir-g1.utb fi-fi-8dot.ctb fi.utb fr-bfu-comp68.cti fr-bfu-comp6.utb fr-bfu-comp8.utb fr-bfu-g2.ctb ga-g1.utb ga-g2.ctb gd.ctb gd.tbl gez.tbl gon.ctb gon.tbl grc-international-common.uti grc-international-composed.uti grc-international-decomposed.uti grc-international-en.utb gr-pl-comp8.uti gu-in-g1.utb gujarati.cti gurumuki.cti gu.tbl haw-us-g1.ctb he-IL.utb '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 he-IL-comp8.utb hi-in-g1.utb hi.tbl hr-chardefs.cti hr-comp8.tbl hr-comp8.utb hr-digits.uti hr-g1.ctb hr-g1.tbl hr-translation.cti hu-backtranslate-correction.dis hu-chardefs.cti hu-exceptionwords.cti hu-hu-comp8.ctb hu-hu-g1_braille_input.cti hu-hu-g1.ctb hu-hu-g2.ctb hu-hu-g2_exceptions.cti hu.tbl hy.ctb hyph_brl_da_dk.dic hyph_cs_CZ.dic hyph_da_DK.dic hyph_de_DE.dic hyph_en_US.dic hyph_eo.dic hyph_es_ES.dic hyph_fr_FR.dic hyph_hu_HU.dic hyph_it_IT.dic hyph_nb_NO.dic hyph_nl_NL.dic hyph_nn_NO.dic hyph_pl_PL.dic hyph_pt_PT.dic hyph_ru.dic hyph_sv_SE.dic hy.tbl IPA-unicode-range.uti IPA.utb '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 is-chardefs6.cti is-chardefs8.cti is.ctb is.tbl it-it-comp6.utb it-it-comp8.utb it.tbl iu-ca-g1.ctb ka-in-g1.utb kannada.cti kha.tbl kh-in-g1.utb kk.utb km-g1.utb kmr.tbl kn.tbl ko-2006.cti ko-2006-g1.ctb ko-2006-g2.ctb ko-chars.cti ko.cti ko-g1.ctb ko-g1-rules.cti ko-g2.ctb ko-g2-rules.cti kok.ctb kok.tbl kru.ctb kru.tbl ks-in-g1.utb latinLetterDef6Dots.uti latinLetterDef8Dots.uti litdigits6DotsPlusDot6.uti litdigits6Dots.uti loweredDigits6Dots.uti loweredDigits8Dots.uti lt-6dot.tbl lt-6dot.utb lt.ctb lt.tbl '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 Lv-Lv-g1.utb lv.tbl malayalam.cti mao-nz-g1.ctb marburg_single_cell_defs.cti marburg_unicode_defs.cti ml-in-g1.utb ml.tbl mn-in-g1.utb mni.tbl mn-MN-common.cti mn-MN-g1.utb mn-MN-g2.ctb mr-in-g1.utb mr.tbl ms-my-g2.ctb mt.ctb mt.tbl mun.ctb mun.tbl mwr.ctb mwr.tbl my-g1.utb my-g2.ctb ne.ctb nemethdefs.cti ne.tbl nl-BE.dis nl-BE-g0.utb nl_BE.tbl nl-chardefs.uti nl-comp8.utb nl-g0.uti nl-NL-g0.utb nl.tbl no-no-8dot-fallback-6dot-g0.utb no-no-8dot.utb no-no-braillo-047-01.dis no-no-chardefs6.uti no-no-comp8.ctb '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 no-no.dis no-no-g0.utb no-no-g1.ctb no-no-g2.ctb no-no-g3.ctb no-no-generic.ctb no-no-generic.dis no-no-latinLetterDef6Dots_diacritics.uti no.tbl np-in-g1.utb nso-za-g1.utb nso-za-g2.ctb or-in-g1.utb oriya.cti or.tbl pa.tbl pi.ctb pi.tbl pl-pl-comp8.ctb Pl-Pl-g1.utb pl.tbl printables.cti pt-pt-comp8.ctb pt-pt-g1.utb pt-pt-g2.ctb pt.tbl pu-in-g1.utb ro.ctb ro.tbl ru-chardefs.cti ru-compbrl.ctb ru.ctb ru-letters.dis ru-litbrl.ctb ru-litbrl-detailed.utb ru-ru.dis ru-ru-g1.ctb ru-unicode.dis sa-in-g1.utb sa.tbl '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 sah.utb sd.tbl se-se.ctb se-se.dis Se-Se-g1.utb si-in-g1.utb sin.cti sin.utb sk-chardefs.cti sk-g1.ctb sk-sk-g1.utb sk-sk.utb sk.tbl sk-translation.cti sl-si-comp8.ctb sl-si-g1.utb sl.tbl sot-za-g1.ctb sot-za-g2.ctb spaces.uti sr-chardefs.cti sr-g1.ctb sr.tbl sv-1989.ctb sv-1996.ctb sv.tbl ta.ctb tamil.cti ta-ta-g1.ctb ta.tbl te-in-g1.utb telugu.cti te.tbl text_nabcc.dis tr.ctb tr-g1.ctb tr-g2.ctb tr-g2.tbl tr.tbl tsn-za-g1.ctb '/usr/local/share/liblouis/tables'
 /usr/bin/install -c -m 644 tsn-za-g2.ctb tt.utb ukchardefs.cti ukmaths_single_cell_defs.cti ukmaths_unicode_defs.cti uk.utb uk-comp.utb unicode-braille.utb unicode.dis unicode-without-blank.dis uni-text.dis ur-pk-g1.utb ur-pk-g2.ctb us-table.dis uz-g1.utb ve-za-g1.utb ve-za-g2.ctb vi.ctb vi-charsdef.uti vi-lettersdef.uti vi-puncsdef.uti vi-saigon-g1.ctb vi-vn-g0.utb vi-vn-g1.ctb vi-vn-g2.ctb wiskunde-chardefs.cti wordcx.dis xh-za-g1.utb xh-za-g2.ctb zh-chn.ctb zh_CHN.tbl zhcn-g1.ctb zhcn-g2.ctb zh-hk.ctb zh_HK.tbl zh-tw.ctb zh_TW.tbl zu-za-g1.utb zu-za-g2.ctb '/usr/local/share/liblouis/tables'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tables'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/tables'
Making install in man
make[1]: Entering directory '/media/ye/project1/exp/liblouis/man'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/man'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/man'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/man'
Making install in tests
make[1]: Entering directory '/media/ye/project1/exp/liblouis/tests'
Making install in tables
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables'
Making install in moreTables
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/moreTables'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/moreTables'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/moreTables'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/moreTables'
Making install in resolve_table
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
Making install in dir_1
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
Making install in dir_1.1
make[5]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1/dir_1.1'
make[6]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1/dir_1.1'
make[6]: Nothing to be done for 'install-exec-am'.
make[6]: Nothing to be done for 'install-data-am'.
make[6]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1/dir_1.1'
make[5]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1/dir_1.1'
make[5]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
make[6]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
make[6]: Nothing to be done for 'install-exec-am'.
make[6]: Nothing to be done for 'install-data-am'.
make[6]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
make[5]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_1'
Making install in dir_2
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_2'
make[5]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_2'
make[5]: Nothing to be done for 'install-exec-am'.
make[5]: Nothing to be done for 'install-data-am'.
make[5]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_2'
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table/dir_2'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
make[5]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
make[5]: Nothing to be done for 'install-exec-am'.
make[5]: Nothing to be done for 'install-data-am'.
make[5]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/resolve_table'
Making install in emphclass
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/emphclass'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/emphclass'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/emphclass'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/emphclass'
Making install in attribute
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables/attribute'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables'
make[4]: Entering directory '/media/ye/project1/exp/liblouis/tests/tables'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables'
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tables'
Making install in tablesWithMetadata
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/tablesWithMetadata'
Making install in yaml
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/yaml'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/yaml'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/yaml'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/yaml'
Making install in braille-specs
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/braille-specs'
Making install in ueb_test_data
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests/ueb_test_data'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/tests'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/tests'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/tests'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/tests'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/tests'
Making install in python
make[1]: Entering directory '/media/ye/project1/exp/liblouis/python'
Making install in louis
make[2]: Entering directory '/media/ye/project1/exp/liblouis/python/louis'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/python/louis'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/python/louis'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/python/louis'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/python'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/python'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/python'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/python'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/python'
Making install in windows
make[1]: Entering directory '/media/ye/project1/exp/liblouis/windows'
Making install in include
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows/include'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/windows/include'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/windows/include'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows/include'
Making install in utils
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows/utils'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/windows/utils'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/windows/utils'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows/utils'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/windows'
make[3]: Entering directory '/media/ye/project1/exp/liblouis/windows'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project1/exp/liblouis/windows'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/windows'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/windows'
Making install in doc
make[1]: Entering directory '/media/ye/project1/exp/liblouis/doc'
make[2]: Entering directory '/media/ye/project1/exp/liblouis/doc'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/doc/liblouis'
 /usr/bin/install -c -m 644 liblouis.html liblouis.txt '/usr/local/share/doc/liblouis'
 /usr/bin/mkdir -p '/usr/local/share/info'
 /usr/bin/install -c -m 644 ./liblouis.info '/usr/local/share/info'
 install-info --info-dir='/usr/local/share/info' '/usr/local/share/info/liblouis.info'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis/doc'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis/doc'
make[1]: Entering directory '/media/ye/project1/exp/liblouis'
make[2]: Entering directory '/media/ye/project1/exp/liblouis'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 liblouis.pc '/usr/local/lib/pkgconfig'
make[2]: Leaving directory '/media/ye/project1/exp/liblouis'
make[1]: Leaving directory '/media/ye/project1/exp/liblouis'
(base) ye@:/media/ye/project1/exp/liblouis$
```

## check lou_" commands

lou_ command ဘာတွေရှိသလဲ ပြီးတော့ compile လုပ်ခဲ့တာ အဆင်ပြေရဲ့လား confirmation အတွက်...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ lou_
lou_allround      lou_checkhyphens  lou_checktable    lou_debug         lou_maketable     lou_tableinfo     lou_trace         lou_translate
(base) ye@:/media/ye/project1/exp/liblouis$
```

### lou_* --help

lou_* command တွေရဲ့ --help ခေါ်ကြည့်ခဲ့  

```
(base) ye@:/media/ye/project1/exp/liblouis$ lou_allround --help
Usage: lou_allround [OPTIONS]
This program tests every capability of the liblouis library. It is
completely interactive. 

  -h, --help          display this help and exit
  -v, --version       display version information and exit

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_checkhyphens --help
Usage: lou_checkhyphens [OPTIONS]
Check the accuracy of hyphenation in Braille translation for both
translated and untranslated words.

  -h, --help          display this help and exit
  -v, --version       display version information and exit

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_checktable --help
Usage: lou_checktable [OPTIONS] TABLE[,TABLE,...]
Test a Braille translation table. If the table contains errors,
appropriate messages are displayed. If there are no errors the
message "no errors found." is shown unless you specify the --quiet
option.
  -h, --help          display this help and exit
  -v, --version       display version information and exit
  -q, --quiet         do not write to standard error if there are no errors.

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_debug --help
Usage: lou_debug [OPTIONS] TABLE[,TABLE,...]
Examine and debug Braille translation tables. This program allows you
to inspect liblouis translation tables and gather information about
them, such as forward and backward rules, characters and dot patterns,
specific opcodes, the size of a table, whether a hyphenation
table is used, how many passes the translation takes and much
more.

  -h, --help          display this help and exit
  -v, --version       display version information and exit

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_maketable --help
ERROR: the Liblouis python bindings must be installed to run this program
(base) ye@:/media/ye/project1/exp/liblouis$ lou_tableinfo --help
Usage: lou_tableinfo [KEY] TABLE
Print all table metadata defined in TABLE, or a specific metadata field
if KEY is specified. Return 0 if the requested metadata could be found,
1 otherwise.

  -h, --help          display this help and exit
  -v, --version       display version information and exi

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_trace --help
Usage: lou_trace [OPTIONS] TABLE[,TABLE,...]
Examine and debug Braille translation tables. This program allows you
to inspect liblouis translation tables by printing out the list of
applied translation rules for a given input.

  -h, --help              display this help and exit
  -v, --version           display version information and exit
  -f, --forward           forward translation using the given table
  -b, --backward          backward translation using the given table
      --noContractions    Use no contractions
      --dotsIO            Display dot patterns
      --ucBrl             Use Unicode Braille patterns
      --noUndefined       Disable output of undefined dot numbers during back-translation
      --partialTrans      Use partial back-translation
                      If neither -f nor -b are specified forward translation
                      is assumed
Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ lou_translate --help
Usage: lou_translate [OPTIONS] TABLE[,TABLE,...]
Translate whatever is on standard input and print it on standard
output. It is intended for large-scale testing of the accuracy of
Braille translation and back-translation.

Options:
  -h, --help          display this help and exit
  -v, --version       display version information and exit
  -f, --forward       forward translation using the given table
  -b, --backward      backward translation using the given table
                      If neither -f nor -b are specified forward translation
                      is assumed
Examples:
  lou_translate --forward en-us-g2.ctb < input.txt
  
  Do a forward translation with table en-us-g2.ctb. The resulting braille is
  ASCII encoded.
  
  lou_translate unicode.dis,en-us-g2.ctb < input.txt
  
  Do a forward translation with table en-us-g2.ctb. The resulting braille is
  encoded as Unicode dot patterns.
  
  echo ",! qk br{n fox" | lou_translate --backward en-us-g2.ctb
  
  Do a backward translation with table en-us-g2.ctb.

Report bugs to liblouis-liblouisxml@freelists.org.
Liblouis home page: <http://www.liblouis.org>
(base) ye@:/media/ye/project1/exp/liblouis$ 
```

man page တော့ မရှိတာကို တွေ့ရ...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ man lou_allround
No manual entry for lou_allround
(base) ye@:/media/ye/project1/exp/liblouis$
```

man ကို install လုပ်ဖို့ man folder ကို ဝင်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/liblouis/man$ ls
Makefile  Makefile.am  Makefile.in
```

## install help2man

help2man is a tool for automatically generating simple manual pages from program output.  
help2man က စက်ထဲမှာ မရှိလို့ apt-get နဲ့ install လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ sudo apt-get install help2man
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
The following NEW packages will be installed:
  help2man
0 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 173 kB of archives.
After this operation, 510 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 help2man amd64 1.47.16 [173 kB]
Fetched 173 kB in 1s (122 kB/s)                         
Selecting previously unselected package help2man.
(Reading database ... 657071 files and directories currently installed.)
Preparing to unpack .../help2man_1.47.16_amd64.deb ...
Unpacking help2man (1.47.16) ...
Setting up help2man (1.47.16) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
install-info: warning: no info dir entry in `/usr/share/info/automake-history.info.gz'
(base) ye@:/media/ye/project1/exp/liblouis$
```

ပြန်ပြီး ./configure အဆင့်ကနေ မ run ခင်မှာ help2man က အလုပ်လုပ်တာ သေချာအောင်လို့ အောက်ပါအတိုင်း command တစ်ခုကို man page ဆောက်ပြီး confirm လုပ်ခဲ့  

```
(base) ye@:/media/ye/project1/exp/liblouis$ help2man lou_allround > lou_allround.man
(base) ye@:/media/ye/project1/exp/liblouis$ man ./lou_allround.man 
(base) ye@:/media/ye/project1/exp/liblouis$ cat ./lou_allround.man 
.\" DO NOT MODIFY THIS FILE!  It was generated by help2man 1.47.16.
.TH LOU_ALLROUND "1" "October 2021" "Liblouis 3.19.0" "User Commands"
.SH NAME
lou_allround \- manual page for lou_allround 3.19.0
.SH SYNOPSIS
.B lou_allround
[\fI\,OPTIONS\/\fR]
.SH DESCRIPTION
This program tests every capability of the liblouis library. It is
completely interactive.
.TP
\fB\-h\fR, \fB\-\-help\fR
display this help and exit
.TP
\fB\-v\fR, \fB\-\-version\fR
display version information and exit
.SH AUTHOR
Written by John J. Boyer.
.SH "REPORTING BUGS"
Report bugs to liblouis\-liblouisxml@freelists.org.
.br
Liblouis home page: <http://www.liblouis.org>
.SH COPYRIGHT
Copyright \(co 2019 ViewPlus Technologies, Inc. and JJB Software, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
.br
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
.SH "SEE ALSO"
The full documentation for
.B lou_allround
is maintained as a Texinfo manual.  If the
.B info
and
.B lou_allround
programs are properly installed at your site, the command
.IP
.B info lou_allround
.PP
should give you access to the complete manual.
(base) ye@:/media/ye/project1/exp/liblouis$
```

## Rerun "./configure", :make" and "make install"

```
$ ./configure --enable-ucs4
$ make
$ sudo make install
```

ဒီ တစ်ခါ run အပြီးမှာတော့ command တစ်ခုချင်းစီအတွက် man page တွေဆောက်ပြီးသား ဖြစ်နေတာကို အောက်ပါအတိုင်း confirm လုပ်ခဲ့...  
ပထမဆုံး "lou_allround" command အတွက် man page ကို ခေါ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ man lou_allround
```

အောက်ပါလိုမျိုး မြင်ရမယ်...  

```
OU_ALLROUND(1)                                                     User Commands                                                    LOU_ALLROUND(1)

NAME
       lou_allround - Test every capability of the liblouis library

SYNOPSIS
       lou_allround [OPTIONS]

DESCRIPTION
       This program tests every capability of the liblouis library. It is completely interactive.

       -h, --help
              display this help and exit

       -v, --version
              display version information and exit

AUTHOR
       Written by John J. Boyer.

REPORTING BUGS
       Report bugs to liblouis-liblouisxml@freelists.org.
       Liblouis home page: <http://www.liblouis.org>

COPYRIGHT
       Copyright  ©  2019  ViewPlus  Technologies,  Inc.  and  JJB  Software,  Inc.  License GPLv3+: GNU GPL version 3 or later <https://gnu.org/li‐
       censes/gpl.html>.
       This is free software: you are free to change and redistribute it.  There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       The full documentation for lou_allround is maintained as a Texinfo manual.  If the info and lou_allround programs are properly  installed  at
       your site, the command

              info liblouis

       should give you access to the complete manual.
 Manual page lou_allround(1) line 1 (press h for help or q to quit)
```

"lou_tableinfo" command ရဲ့ man page ကိုလည်း ခေါ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/liblouis$ man lou_tableinfo
```

အောက်ပါအတိုင်း မြင်ရလိမ့်မယ်...  

```
LOU_TABLEINFO(1)                                                    User Commands                                                   LOU_TABLEINFO(1)

NAME
       lou_tableinfo - A tool to query meta data from a liblouis Braille translation table

SYNOPSIS
       lou_tableinfo [KEY] TABLE

DESCRIPTION
       Print  all  table  metadata  defined  in TABLE, or a specific metadata field if KEY is specified. Return 0 if the requested metadata could be
       found, 1 otherwise.

       -h, --help
              display this help and exit

       -v, --version
              display version information and exi

AUTHOR
       Written by Bert Frees.

REPORTING BUGS
       Report bugs to liblouis-liblouisxml@freelists.org.
       Liblouis home page: <http://www.liblouis.org>

COPYRIGHT
       Copyright © 2019 Bert Frees License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free to change and redistribute it.  There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       The full documentation for lou_tableinfo is maintained as a Texinfo manual.  If the info and lou_tableinfo programs are properly installed at
       your site, the command

              info liblouis

       should give you access to the complete manual.
 Manual page lou_tableinfo(1) line 1 (press h for help or q to quit)
```

### Testing lou_translate

```
(base) ye@:/media/ye/project1/exp/liblouis$ echo ",! qk br{n fox" | lou_translate --backward en-us-g2.ctb
The quick brown fox
(base) ye@:/media/ye/project1/exp/liblouis$
```

### Check All Tables

```
(base) ye@:/media/ye/project1/exp/liblouis/tests$ time perl ./check_all_tables.pl 2>&1 | tee check-all-tables-output.txt
Use of uninitialized value $ENV{"LOUIS_TABLEPATH"} in concatenation (.) or string at ./check_all_tables.pl line 24.

real	0m0.009s
user	0m0.001s
sys	0m0.011s
(base) ye@:/media/ye/project1/exp/liblouis/tests$ 
```

```
(base) ye@:/media/ye/project1/exp/liblouis/tests$ export LOUIS_TABLEPATH=/media/ye/project1/exp/liblouis/
(base) ye@:/media/ye/project1/exp/liblouis/tests$ echo $LOUIS_TABLEPATH 
/media/ye/project1/exp/liblouis/
```

```
(base) ye@:/media/ye/project1/exp/liblouis/tests$ time perl ./check_all_tables.pl 2>&1 | tee check-all-tables-output.txt
/media/ye/project1/exp/liblouis//tables/bg.utb:245: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/bg.utb:246: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/bg.utb:247: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/bg.utb:248: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/bg.utb:249: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/bg.utb:250: warning: class is deprecated, use attribute instead
6 warnings issued
/media/ye/project1/exp/liblouis//tables/km-g1.utb:363: warning: class is deprecated, use attribute instead
1 warnings issued
/media/ye/project1/exp/liblouis//tables/my-g1.utb:625: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:626: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:627: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:628: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:629: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:653: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/my-g1.utb:654: warning: class is deprecated, use attribute instead
7 warnings issued
Duplicate emphasis class: italic
Duplicate emphasis class: underline
Duplicate emphasis class: bold
3 warnings issued
Duplicate emphasis class: italic
Duplicate emphasis class: underline
Duplicate emphasis class: bold
3 warnings issued
/media/ye/project1/exp/liblouis//tables/my-g1.utb:625: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:626: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:627: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:628: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:629: warning: \Xhhhh (with a capital 'X') is deprecated.
/media/ye/project1/exp/liblouis//tables/my-g1.utb:653: warning: class is deprecated, use attribute instead
/media/ye/project1/exp/liblouis//tables/my-g1.utb:654: warning: class is deprecated, use attribute instead
7 warnings issued

real	0m10.230s
user	0m5.531s
sys	0m3.437s
(base) ye@:/media/ye/project1/exp/liblouis/tests$
```

## Reference

http://www.idryman.org/blog/2016/03/10/autoconf-tutorial-1/
http://www.idryman.org/blog/2016/03/14/autoconf-tutorial-2/
http://www.idryman.org/blog/2016/03/15/autoconf-tutorial-part-3/
https://github.com/dryman/autoconf-tutorials

