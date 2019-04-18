

```
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool$ mkdir sndfile-waveform
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool$ cd sndfile-waveform/
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform$ sudo apt-get build-dep sndfile-tools
Reading package lists... Done
E: You must put some 'source' URIs in your sources.list
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform$ ls
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform$ sudo apt-get install octave-signal libsamplerate0-dev git
Reading package lists... Done
Building dependency tree       
Reading state information... Done
git is already the newest version (1:2.7.4-0ubuntu1.6).
The following additional packages will be installed:
  gnuplot-data gnuplot-tex gnuplot-x11 libarpack2 libcxsparse3.1.4 libfltk-gl1.3 libfltk1.3 libgl2ps0 libglpk36 libgraphicsmagick++-q16-12
  libgraphicsmagick-q16-3 liboctave3 libosmesa6 libplot2c2 libpstoedit0c2a libqhull7 libqrupdate1 libqscintilla2-12v5 libqscintilla2-l10n libslicot0
  octave octave-common octave-control pstoedit
Suggested packages:
  gnuplot-doc libiodbc2-dev graphicsmagick-dbg octave-info octave-doc octave-htmldoc xfig | ivtools-bin | tgif | transfig
The following NEW packages will be installed:
  gnuplot-data gnuplot-tex gnuplot-x11 libarpack2 libcxsparse3.1.4 libfltk-gl1.3 libfltk1.3 libgl2ps0 libglpk36 libgraphicsmagick++-q16-12
  libgraphicsmagick-q16-3 liboctave3 libosmesa6 libplot2c2 libpstoedit0c2a libqhull7 libqrupdate1 libqscintilla2-12v5 libqscintilla2-l10n
  libsamplerate0-dev libslicot0 octave octave-common octave-control octave-signal pstoedit
0 upgraded, 26 newly installed, 0 to remove and 215 not upgraded.
Need to get 19.5 MB of archives.
After this operation, 82.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libqrupdate1 amd64 1.1.2-1build1 [37.6 kB]
Get:2 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libslicot0 amd64 5.0+20101122-2 [1,002 kB]
Get:3 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 gnuplot-tex all 4.6.6-3 [10.1 kB]
Get:4 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 gnuplot-data all 4.6.6-3 [53.2 kB]
Get:5 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 gnuplot-x11 amd64 4.6.6-3 [794 kB]
Get:6 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libarpack2 amd64 3.3.0-1build2 [88.2 kB]
Get:7 http://jp.archive.ubuntu.com/ubuntu xenial/main amd64 libcxsparse3.1.4 amd64 1:4.4.6-1 [62.8 kB]
Get:8 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libfltk1.3 amd64 1.3.3-7 [501 kB]
Get:9 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libfltk-gl1.3 amd64 1.3.3-7 [39.5 kB]
Get:10 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libgl2ps0 amd64 1.3.8-1.2 [35.5 kB]
Get:11 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libglpk36 amd64 4.57-1build3 [386 kB]
Get:12 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 libgraphicsmagick-q16-3 amd64 1.3.23-1ubuntu0.1 [1,107 kB]
Get:13 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 libgraphicsmagick++-q16-12 amd64 1.3.23-1ubuntu0.1 [101 kB]
Get:14 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 liboctave3 amd64 4.0.0-3ubuntu9.2 [6,899 kB]
Get:15 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libplot2c2 amd64 2.6-3ubuntu1 [941 kB]                                               
Get:16 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libpstoedit0c2a amd64 3.70-1ubuntu2 [315 kB]                                         
Get:17 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libqhull7 amd64 2015.2-1 [152 kB]                                                    
Get:18 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libqscintilla2-l10n all 2.9.1+dfsg-4build1 [38.3 kB]                                 
Get:19 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 libqscintilla2-12v5 amd64 2.9.1+dfsg-4build1 [810 kB]                                
Get:20 http://jp.archive.ubuntu.com/ubuntu xenial/main amd64 libsamplerate0-dev amd64 0.1.8-8 [990 kB]                                                
Get:21 http://jp.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libosmesa6 amd64 18.0.5-0ubuntu0~16.04.1 [1,272 kB]                              
Get:22 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 octave-common all 4.0.0-3ubuntu9.2 [1,282 kB]                                
Get:23 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 octave amd64 4.0.0-3ubuntu9.2 [1,474 kB]                                     
Get:24 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 octave-control amd64 3.0.0-1 [819 kB]                                                
Get:25 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 octave-signal amd64 1.3.2-1 [199 kB]                                                 
Get:26 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 pstoedit amd64 3.70-1ubuntu2 [102 kB]                                                
Fetched 19.5 MB in 15s (1,285 kB/s)                                                                                                                   
Selecting previously unselected package libqrupdate1:amd64.
(Reading database ... 376466 files and directories currently installed.)
Preparing to unpack .../libqrupdate1_1.1.2-1build1_amd64.deb ...
Unpacking libqrupdate1:amd64 (1.1.2-1build1) ...
Selecting previously unselected package libslicot0:amd64.
Preparing to unpack .../libslicot0_5.0+20101122-2_amd64.deb ...
Unpacking libslicot0:amd64 (5.0+20101122-2) ...
Selecting previously unselected package gnuplot-tex.
Preparing to unpack .../gnuplot-tex_4.6.6-3_all.deb ...
Unpacking gnuplot-tex (4.6.6-3) ...
Selecting previously unselected package gnuplot-data.
Preparing to unpack .../gnuplot-data_4.6.6-3_all.deb ...
Unpacking gnuplot-data (4.6.6-3) ...
Selecting previously unselected package gnuplot-x11.
Preparing to unpack .../gnuplot-x11_4.6.6-3_amd64.deb ...
Unpacking gnuplot-x11 (4.6.6-3) ...
Selecting previously unselected package libarpack2.
Preparing to unpack .../libarpack2_3.3.0-1build2_amd64.deb ...
Unpacking libarpack2 (3.3.0-1build2) ...
Selecting previously unselected package libcxsparse3.1.4:amd64.
Preparing to unpack .../libcxsparse3.1.4_1%3a4.4.6-1_amd64.deb ...
Unpacking libcxsparse3.1.4:amd64 (1:4.4.6-1) ...
Selecting previously unselected package libfltk1.3:amd64.
Preparing to unpack .../libfltk1.3_1.3.3-7_amd64.deb ...
Unpacking libfltk1.3:amd64 (1.3.3-7) ...
Selecting previously unselected package libfltk-gl1.3:amd64.
Preparing to unpack .../libfltk-gl1.3_1.3.3-7_amd64.deb ...
Unpacking libfltk-gl1.3:amd64 (1.3.3-7) ...
Selecting previously unselected package libgl2ps0.
Preparing to unpack .../libgl2ps0_1.3.8-1.2_amd64.deb ...
Unpacking libgl2ps0 (1.3.8-1.2) ...
Selecting previously unselected package libglpk36:amd64.
Preparing to unpack .../libglpk36_4.57-1build3_amd64.deb ...
Unpacking libglpk36:amd64 (4.57-1build3) ...
Selecting previously unselected package libgraphicsmagick-q16-3.
Preparing to unpack .../libgraphicsmagick-q16-3_1.3.23-1ubuntu0.1_amd64.deb ...
Unpacking libgraphicsmagick-q16-3 (1.3.23-1ubuntu0.1) ...
Selecting previously unselected package libgraphicsmagick++-q16-12.
Preparing to unpack .../libgraphicsmagick++-q16-12_1.3.23-1ubuntu0.1_amd64.deb ...
Unpacking libgraphicsmagick++-q16-12 (1.3.23-1ubuntu0.1) ...
Selecting previously unselected package liboctave3:amd64.
Preparing to unpack .../liboctave3_4.0.0-3ubuntu9.2_amd64.deb ...
Unpacking liboctave3:amd64 (4.0.0-3ubuntu9.2) ...
Selecting previously unselected package libplot2c2.
Preparing to unpack .../libplot2c2_2.6-3ubuntu1_amd64.deb ...
Unpacking libplot2c2 (2.6-3ubuntu1) ...
Selecting previously unselected package libpstoedit0c2a.
Preparing to unpack .../libpstoedit0c2a_3.70-1ubuntu2_amd64.deb ...
Unpacking libpstoedit0c2a (3.70-1ubuntu2) ...
Selecting previously unselected package libqhull7:amd64.
Preparing to unpack .../libqhull7_2015.2-1_amd64.deb ...
Unpacking libqhull7:amd64 (2015.2-1) ...
Selecting previously unselected package libqscintilla2-l10n.
Preparing to unpack .../libqscintilla2-l10n_2.9.1+dfsg-4build1_all.deb ...
Unpacking libqscintilla2-l10n (2.9.1+dfsg-4build1) ...
Selecting previously unselected package libqscintilla2-12v5.
Preparing to unpack .../libqscintilla2-12v5_2.9.1+dfsg-4build1_amd64.deb ...
Unpacking libqscintilla2-12v5 (2.9.1+dfsg-4build1) ...
Selecting previously unselected package libsamplerate0-dev:amd64.
Preparing to unpack .../libsamplerate0-dev_0.1.8-8_amd64.deb ...
Unpacking libsamplerate0-dev:amd64 (0.1.8-8) ...
Selecting previously unselected package libosmesa6:amd64.
Preparing to unpack .../libosmesa6_18.0.5-0ubuntu0~16.04.1_amd64.deb ...
Unpacking libosmesa6:amd64 (18.0.5-0ubuntu0~16.04.1) ...
Selecting previously unselected package octave-common.
Preparing to unpack .../octave-common_4.0.0-3ubuntu9.2_all.deb ...
Unpacking octave-common (4.0.0-3ubuntu9.2) ...
Selecting previously unselected package octave.
Preparing to unpack .../octave_4.0.0-3ubuntu9.2_amd64.deb ...
Unpacking octave (4.0.0-3ubuntu9.2) ...
Selecting previously unselected package octave-control.
Preparing to unpack .../octave-control_3.0.0-1_amd64.deb ...
Unpacking octave-control (3.0.0-1) ...
Selecting previously unselected package octave-signal.
Preparing to unpack .../octave-signal_1.3.2-1_amd64.deb ...
Unpacking octave-signal (1.3.2-1) ...
Selecting previously unselected package pstoedit.
Preparing to unpack .../pstoedit_3.70-1ubuntu2_amd64.deb ...
Unpacking pstoedit (3.70-1ubuntu2) ...
Processing triggers for tex-common (6.04) ...
Running mktexlsr. This may take some time... done.
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for doc-base (0.10.7) ...
Processing 3 added doc-base files...
Processing triggers for bamfdaemon (0.5.3~bzr0+16.04.20180209-0ubuntu1) ...
Rebuilding /usr/share/applications/bamf-2.index...
Processing triggers for desktop-file-utils (0.22-1ubuntu5.1) ...
Processing triggers for gnome-menus (3.13.3-6ubuntu3.1) ...
Processing triggers for mime-support (3.59ubuntu1) ...
Setting up libqrupdate1:amd64 (1.1.2-1build1) ...
Setting up libslicot0:amd64 (5.0+20101122-2) ...
Setting up gnuplot-tex (4.6.6-3) ...
Setting up gnuplot-data (4.6.6-3) ...
Setting up gnuplot-x11 (4.6.6-3) ...
update-alternatives: using /usr/bin/gnuplot4-x11 to provide /usr/bin/gnuplot (gnuplot) in auto mode
update-alternatives: using /usr/bin/gnuplot4-x11 to provide /usr/bin/gnuplot4 (gnuplot4) in auto mode
Setting up libarpack2 (3.3.0-1build2) ...
Setting up libcxsparse3.1.4:amd64 (1:4.4.6-1) ...
Setting up libfltk1.3:amd64 (1.3.3-7) ...
Setting up libfltk-gl1.3:amd64 (1.3.3-7) ...
Setting up libgl2ps0 (1.3.8-1.2) ...
Setting up libglpk36:amd64 (4.57-1build3) ...
Setting up libgraphicsmagick-q16-3 (1.3.23-1ubuntu0.1) ...
Setting up libgraphicsmagick++-q16-12 (1.3.23-1ubuntu0.1) ...
Setting up liboctave3:amd64 (4.0.0-3ubuntu9.2) ...
Setting up libplot2c2 (2.6-3ubuntu1) ...
Setting up libpstoedit0c2a (3.70-1ubuntu2) ...
Setting up libqhull7:amd64 (2015.2-1) ...
Setting up libqscintilla2-l10n (2.9.1+dfsg-4build1) ...
Setting up libqscintilla2-12v5 (2.9.1+dfsg-4build1) ...
Setting up libsamplerate0-dev:amd64 (0.1.8-8) ...
Setting up libosmesa6:amd64 (18.0.5-0ubuntu0~16.04.1) ...
Setting up octave-common (4.0.0-3ubuntu9.2) ...
Setting up octave (4.0.0-3ubuntu9.2) ...
Setting up octave-control (3.0.0-1) ...
Setting up octave-signal (1.3.2-1) ...
Setting up pstoedit (3.70-1ubuntu2) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform$ git clone https://github.com/erikd/sndfile-tools.git
Cloning into 'sndfile-tools'...
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1225 (delta 0), reused 0 (delta 0), pack-reused 1224
Receiving objects: 100% (1225/1225), 690.46 KiB | 112.00 KiB/s, done.
Resolving deltas: 100% (778/778), done.
Checking connectivity... done.
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform$ cd sndfile-tools/
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ ./autogen.sh 
checking for autoconf... yes
checking for automake... yes
checking for libtool... libtoolize
checking for pkg-config ... yes
Creating 'build-aux' directory.
Generating configuration files for sndfile-tools, please wait ... 
  aclocal 
  libtoolize --automake --force
  autoheader
  automake --add-missing 
configure.ac:35: installing 'build-aux/compile'
configure.ac:25: installing 'build-aux/config.guess'
configure.ac:25: installing 'build-aux/config.sub'
configure.ac:30: installing 'build-aux/install-sh'
configure.ac:30: installing 'build-aux/missing'
Makefile.am: installing 'build-aux/depcomp'
parallel-tests: installing 'build-aux/test-driver'
  autoconf
Installing git pre-commit hook for this project.

(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ ./configure
checking whether configure should try to set CFLAGS/CPPFLAGS/LDFLAGS... yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether make supports nested variables... (cached) yes
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
checking for gcc option to accept ISO C99... none needed
checking for C compiler vendor... gnu
checking for a sed that does not truncate output... /bin/sed
checking for C compiler version... 7.3.0
checking whether make sets $(MAKE)... (cached) yes
checking whether ln -s works... yes
checking how to print strings... printf
checking for a sed that does not truncate output... (cached) /bin/sed
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
checking for library containing floor... -lm
checking for floor... yes
checking for ceil... yes
checking for fmod... yes
checking for lrint... yes
checking for lrintf... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for SNDFILE... yes
checking for SAMPLERATE... yes
checking for FFTW3... yes
checking for CAIRO... yes
checking for JACK... yes
checking whether gcc is Clang... no
checking whether pthreads work with -pthread... yes
checking for joinable pthread attribute... PTHREAD_CREATE_JOINABLE
checking whether more special flags are required for pthreads... no
checking for PTHREAD_PRIO_INHERIT... yes
checking whether C compiler accepts -O2... yes
checking whether C compiler accepts -pipe... yes
checking whether the linker accepts -Wl,-O1... yes
checking whether the linker accepts -Wl,--as-needed... yes
checking whether the linker accepts -Wl,--no-undefined... yes
checking whether the linker accepts -Wl,--gc-sections... yes
checking whether C compiler accepts -Wall... yes
checking whether C compiler accepts -Wextra... yes
checking whether C compiler accepts -Wstrict-prototypes... yes
checking whether C compiler accepts -Wmissing-prototypes... yes
checking whether C compiler accepts -Waggregate-return... yes
checking whether C compiler accepts -Wcast-align... yes
checking whether C compiler accepts -Wcast-qual... yes
checking whether C compiler accepts -Wnested-externs... yes
checking whether C compiler accepts -Wshadow... yes
checking whether C compiler accepts -Wpointer-arith... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/config.h
config.status: executing depfiles commands
config.status: executing libtool commands

-=-=-=-=-=-=-=-=-=-= Configuration Complete =-=-=-=-=-=-=-=-=-=-=-

  Configuration summary :

    sndfile-tools version : ............... 1.04

    Host CPU : ............................ x86_64
    Host Vendor : ......................... pc
    Host OS : ............................. linux-gnu

    CFLAGS : ..............................  -O2 -pipe -Wall -Wextra -Wstrict-prototypes -Wmissing-prototypes -Waggregate-return -Wcast-align -Wcast-qual -Wnested-externs -Wshadow -Wpointer-arith
    CPPFLAGS : ............................ 
    LDFLAGS : .............................  -Wl,-O1 -Wl,--as-needed -Wl,--no-undefined -Wl,--gc-sections

  Tools :

    C Compiler Vendor is : ................ gnu (7.3.0)

  Extra tools required for testing and examples :

    Found libjack ......................... yes

  Installation directories :

    Program directory : ................... /usr/local/bin


(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ make
  CC       src/bin_sndfile_generate_chirp-generate-chirp.o
  CC       src/bin_sndfile_generate_chirp-common.o
  CCLD     bin/sndfile-generate-chirp
libtool: Version mismatch error.  This is libtool 2.4.2, but the
libtool: definition of this LT_INIT comes from libtool 2.4.6.
libtool: You should recreate aclocal.m4 with macros from libtool 2.4.2
libtool: and run autoconf again.
Makefile:814: recipe for target 'bin/sndfile-generate-chirp' failed
make: *** [bin/sndfile-generate-chirp] Error 63

(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ vi Makefile
```

```
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ rm -f aclocal.m4
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ aclocal && libtoolize --force && autoreconf

libtoolize: putting auxiliary files in AC_CONFIG_AUX_DIR, `build-aux'.
libtoolize: linking file `build-aux/ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIR, `m4'.
libtoolize: linking file `m4/libtool.m4'
libtoolize: linking file `m4/ltoptions.m4'
libtoolize: linking file `m4/ltsugar.m4'
libtoolize: linking file `m4/ltversion.m4'
libtoolize: linking file `m4/lt~obsolete.m4'
libtoolize: Consider adding `-I m4' to ACLOCAL_AMFLAGS in Makefile.am.
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ 
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ ./configure
checking whether configure should try to set CFLAGS/CPPFLAGS/LDFLAGS... yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether make supports nested variables... (cached) yes
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
checking for gcc option to accept ISO C99... none needed
checking for C compiler vendor... gnu
checking for a sed that does not truncate output... /bin/sed
checking for C compiler version... 7.3.0
checking whether make sets $(MAKE)... (cached) yes
checking whether ln -s works... yes
checking how to print strings... printf
checking for a sed that does not truncate output... (cached) /bin/sed
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for fgrep... /bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking the maximum length of command line arguments... 1572864
checking whether the shell understands some XSI constructs... yes
checking whether the shell understands "+="... yes
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
checking for library containing floor... -lm
checking for floor... yes
checking for ceil... yes
checking for fmod... yes
checking for lrint... yes
checking for lrintf... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for SNDFILE... yes
checking for SAMPLERATE... yes
checking for FFTW3... yes
checking for CAIRO... yes
checking for JACK... yes
checking whether gcc is Clang... no
checking whether pthreads work with -pthread... yes
checking for joinable pthread attribute... PTHREAD_CREATE_JOINABLE
checking whether more special flags are required for pthreads... no
checking for PTHREAD_PRIO_INHERIT... yes
checking whether C compiler accepts -O2... yes
checking whether C compiler accepts -pipe... yes
checking whether the linker accepts -Wl,-O1... yes
checking whether the linker accepts -Wl,--as-needed... yes
checking whether the linker accepts -Wl,--no-undefined... yes
checking whether the linker accepts -Wl,--gc-sections... yes
checking whether C compiler accepts -Wall... yes
checking whether C compiler accepts -Wextra... yes
checking whether C compiler accepts -Wstrict-prototypes... yes
checking whether C compiler accepts -Wmissing-prototypes... yes
checking whether C compiler accepts -Waggregate-return... yes
checking whether C compiler accepts -Wcast-align... yes
checking whether C compiler accepts -Wcast-qual... yes
checking whether C compiler accepts -Wnested-externs... yes
checking whether C compiler accepts -Wshadow... yes
checking whether C compiler accepts -Wpointer-arith... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/config.h
config.status: executing depfiles commands
config.status: executing libtool commands

-=-=-=-=-=-=-=-=-=-= Configuration Complete =-=-=-=-=-=-=-=-=-=-=-

  Configuration summary :

    sndfile-tools version : ............... 1.04

    Host CPU : ............................ x86_64
    Host Vendor : ......................... pc
    Host OS : ............................. linux-gnu

    CFLAGS : ..............................  -O2 -pipe -Wall -Wextra -Wstrict-prototypes -Wmissing-prototypes -Waggregate-return -Wcast-align -Wcast-qual -Wnested-externs -Wshadow -Wpointer-arith
    CPPFLAGS : ............................ 
    LDFLAGS : .............................  -Wl,-O1 -Wl,--as-needed -Wl,--no-undefined -Wl,--gc-sections

  Tools :

    C Compiler Vendor is : ................ gnu (7.3.0)

  Extra tools required for testing and examples :

    Found libjack ......................... yes

  Installation directories :

    Program directory : ................... /usr/local/bin
```

```
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$ make
  CC       src/bin_sndfile_generate_chirp-common.o
  CCLD     bin/sndfile-generate-chirp
  CC       src/bin_sndfile_spectrogram-spectrogram.o
  CC       src/bin_sndfile_spectrogram-window.o
  CC       src/bin_sndfile_spectrogram-common.o
  CC       src/bin_sndfile_spectrogram-spectrum.o
  CCLD     bin/sndfile-spectrogram
  CC       src/bin_sndfile_mix_to_mono-mix-to-mono.o
  CC       src/bin_sndfile_mix_to_mono-common.o
  CCLD     bin/sndfile-mix-to-mono
  CC       src/bin_sndfile_resample-resample.o
  CC       src/bin_sndfile_resample-common.o
  CCLD     bin/sndfile-resample
  CC       src/bin_sndfile_waveform-waveform.o
  CC       src/bin_sndfile_waveform-common.o
  CCLD     bin/sndfile-waveform
  CC       src/bin_sndfile_jackplay-jackplay.o
  CCLD     bin/sndfile-jackplay
(py3.6.5) lar@lar-air:/media/lar/Transcend/tool/sndfile-waveform/sndfile-tools$
```
