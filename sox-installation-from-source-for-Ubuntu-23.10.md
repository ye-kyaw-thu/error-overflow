# Sox Installation From Source 

I installed Sox on Ubuntu 23.10.  
ဒီ sox tool က အရမ်းအသုံးဝင်တဲ့ tool ဖြစ်လို့ ခဏခဏ စက်ပေါင်းများစွာပေါ်မှာ installation လုပ်ပြီး သုံးဖြစ်နေပါတယ်။  
အရင်တင်ထားတာလည်း ရှိချင်ရှိမယ်။ လက်ရှိ သုံးနေတဲ့ Linux, Ubuntu 23.10 မှာလုပ်ဖြစ်တာကို log အနေနဲ့ တင်ပေးထားတာပါ။  

I downloaded from the following link:  
[https://sourceforge.net/projects/sox/](https://sourceforge.net/projects/sox/)  

After that, moved from Downloads/ folder to tool/ folder.  

```
(base) ye@lst-hpc3090:~/Downloads$ mv sox-14.4.2.tar.bz2 ../tool/
(base) ye@lst-hpc3090:~/Downloads$ cd ../tool
```

tar.gz2 file extraction with tar command.  

```
(base) ye@lst-hpc3090:~/tool$ tar -xvjf ./sox-14.4.2.tar.bz2 
sox-14.4.2/
sox-14.4.2/config.sub
sox-14.4.2/aclocal.m4
sox-14.4.2/COPYING
sox-14.4.2/cygbuild
sox-14.4.2/src/
sox-14.4.2/src/gsrt.c
sox-14.4.2/src/tx16w.c
sox-14.4.2/src/tremolo.c
sox-14.4.2/src/vox-fmt.c
sox-14.4.2/src/compandt.c
sox-14.4.2/src/downsample.c
sox-14.4.2/src/swap.c
sox-14.4.2/src/compand.c
sox-14.4.2/src/mat4.c
sox-14.4.2/src/cvsdfilt.h
sox-14.4.2/src/voc.c
sox-14.4.2/src/g711.h
sox-14.4.2/src/getopt.c
sox-14.4.2/src/vorbis.c
sox-14.4.2/src/8svx.c
sox-14.4.2/src/rate_poly_fir.h
sox-14.4.2/src/example5.c
sox-14.4.2/src/optional-fmts.am
sox-14.4.2/src/win32-glob.c
sox-14.4.2/src/stretch.c
sox-14.4.2/src/formats.c
sox-14.4.2/src/pulseaudio.c
sox-14.4.2/src/test-comments
sox-14.4.2/src/example0.c
sox-14.4.2/src/sndio.c
sox-14.4.2/src/compandt.h
sox-14.4.2/src/speed.c
sox-14.4.2/src/chorus.c
sox-14.4.2/src/paf.c
sox-14.4.2/src/biquad.h
sox-14.4.2/src/dft_filter.c
sox-14.4.2/src/adpcms.c
sox-14.4.2/src/f4-fmt.c
sox-14.4.2/src/alsa.c
sox-14.4.2/src/avr.c
sox-14.4.2/src/rate.c
sox-14.4.2/src/wavpack.c
sox-14.4.2/src/hilbert.c
sox-14.4.2/src/caf.c
sox-14.4.2/src/vol.c
sox-14.4.2/src/formats_i.c
sox-14.4.2/src/example6.c
sox-14.4.2/src/dft_filter.h
sox-14.4.2/src/xi.c
sox-14.4.2/src/cvsd.c
sox-14.4.2/src/win32-ltdl.c
sox-14.4.2/src/dither.h
sox-14.4.2/src/contrast.c
sox-14.4.2/src/util.h
sox-14.4.2/src/fir.c
sox-14.4.2/src/pvf.c
sox-14.4.2/src/ladspa.c
sox-14.4.2/src/fifo.h
sox-14.4.2/src/noisered.c
sox-14.4.2/src/output.c
sox-14.4.2/src/mat5.c
sox-14.4.2/src/input.c
sox-14.4.2/src/coreaudio.c
sox-14.4.2/src/stat.c
sox-14.4.2/src/amr-nb.c
sox-14.4.2/src/sox_i.h
sox-14.4.2/src/la-fmt.c
sox-14.4.2/src/libsox_i.c
sox-14.4.2/src/stats.c
sox-14.4.2/src/ima_rw.h
sox-14.4.2/src/libsox.c
sox-14.4.2/src/g723_40.c
sox-14.4.2/src/effects_i.c
sox-14.4.2/src/g711.c
sox-14.4.2/src/skeleff.c
sox-14.4.2/src/wve.c
sox-14.4.2/src/dcshift.c
sox-14.4.2/src/echos.c
sox-14.4.2/src/effects_i_dsp.c
sox-14.4.2/src/mp3-util.h
sox-14.4.2/src/sox_sample_test.c
sox-14.4.2/src/rate_half_fir.h
sox-14.4.2/src/fft4g.c
sox-14.4.2/src/phaser.c
sox-14.4.2/src/xa.c
sox-14.4.2/src/ima-fmt.c
sox-14.4.2/src/formats.h
sox-14.4.2/src/rate_poly_fir0.h
sox-14.4.2/src/noiseprof.c
sox-14.4.2/src/gain.c
sox-14.4.2/src/bend.c
sox-14.4.2/src/sf.c
sox-14.4.2/src/testall.sh
sox-14.4.2/src/ignore-warning.h
sox-14.4.2/src/biquad.c
sox-14.4.2/src/cvsd-fmt.c
sox-14.4.2/src/sphere.c
sox-14.4.2/src/reverb.c
sox-14.4.2/src/example4.c
sox-14.4.2/src/sox-fmt.c
sox-14.4.2/src/u4-fmt.c
sox-14.4.2/src/dvms-fmt.c
sox-14.4.2/src/dat.c
sox-14.4.2/src/vox.c
sox-14.4.2/src/xmalloc.h
sox-14.4.2/src/al-fmt.c
sox-14.4.2/src/win32-ltdl.h
sox-14.4.2/src/htk.c
sox-14.4.2/src/maud.c
sox-14.4.2/src/sox.c
sox-14.4.2/src/g721.c
sox-14.4.2/src/loudness.c
sox-14.4.2/src/ul-fmt.c
sox-14.4.2/src/win32-glob.h
sox-14.4.2/src/au.c
sox-14.4.2/src/aifc-fmt.c
sox-14.4.2/src/reverse.c
sox-14.4.2/src/cvsd.h
sox-14.4.2/src/remix.c
sox-14.4.2/src/Makefile.am
sox-14.4.2/src/util.c
sox-14.4.2/src/u2-fmt.c
sox-14.4.2/src/xmalloc.c
sox-14.4.2/src/soxconfig.h.in
sox-14.4.2/src/gsm.c
sox-14.4.2/src/testall.bat
sox-14.4.2/src/spectrogram.c
sox-14.4.2/src/example1.c
sox-14.4.2/src/monkey.wav
sox-14.4.2/src/aiff-fmt.c
sox-14.4.2/src/skelform.c
...
...
...
sox-14.4.2/lpc10/dyptrk.c
sox-14.4.2/lpc10/lpcini.c
sox-14.4.2/lpc10/lpfilt.c
sox-14.4.2/lpc10/difmag.c
sox-14.4.2/lpc10/voicin.c
sox-14.4.2/lpc10/ham84.c
sox-14.4.2/lpc10/placea.c
sox-14.4.2/lpc10/CMakeLists.txt
sox-14.4.2/LICENSE.GPL
sox-14.4.2/CMakeLists.txt
sox-14.4.2/sox.txt
(base) ye@lst-hpc3090:~/tool$
```

## Check

check extracted source folder ...  

```
(base) ye@lst-hpc3090:~/tool$ cd sox-14.4.2/
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ ls
aclocal.m4      config.sub    FEATURES.in  LICENSE.GPL   Makefile.in  README.osx    soxformat.txt
AUTHORS         configure     INSTALL      LICENSE.LGPL  missing      README.sh     soxi.1
ChangeLog       configure.ac  install-sh   lpc10         msvc10       README.win32  soxi.txt
CMakeLists.txt  COPYING       libgsm       ltmain.sh     msvc9        scripts       sox.pc.in
compile         cygbuild      libsox.3     m4            NEWS         sox.1         sox.txt
config.guess    depcomp       libsox.txt   Makefile.am   README       soxformat.7   src
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ 
```

## configure

```
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking target system type... x86_64-unknown-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether make supports nested variables... (cached) yes
checking for gcc... gcc
checking whether the C compiler works... yes
...
...
...
gsm........................yes (in-tree)
lpc10......................yes (in-tree)
mp2/mp3....................no
 id3tag....................no
 lame......................no
 mad.......................no
 twolame...................no
oggvorbis..................no
opus.......................no
sndfile....................no
wavpack....................no

OTHER OPTIONS
ladspa effects.............no
magic support..............no
png support................no
OpenMP support.............yes, -fopenmp

Configure finished.  Do 'make -s && make install' to compile and install SoX.

(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ 
```

## make

-S option used.  

```
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ make -S
Making all in lpc10
make[1]: Entering directory '/home/ye/tool/sox-14.4.2/lpc10'
  CC       analys.lo
  CC       bsynz.lo
  CC       chanwr.lo
  CC       dcbias.lo
  CC       decode.lo
  CC       deemp.lo
  CC       difmag.lo
  CC       dyptrk.lo
  CC       encode.lo
  CC       energy.lo
  CC       f2clib.lo
  CC       ham84.lo
  CC       hp100.lo
  CC       invert.lo
  CC       irc2pc.lo
...
...
...
  118 |   assert(in = sox_open_read(argv[1], NULL, NULL, NULL));
      |          ^~
example1.c:123:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
  123 |   assert(out = sox_open_write(argv[2], &in->signal, NULL, NULL, NULL, NULL));
      |          ^~~
  CCLD     example1
  CC       example2.o
In file included from example2.c:28:
example2.c: In function ‘main’:
example2.c:53:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   53 |   assert(in = sox_open_read(*argv, NULL, NULL, NULL));
      |          ^~
example2.c:78:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   78 |   assert(buf = malloc(sizeof(sox_sample_t) * block_size));
      |          ^~~
  CCLD     example2
  CC       example3.o
In file included from example3.c:27:
example3.c: In function ‘main’:
example3.c:68:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   68 |   assert(in = sox_open_read(argv[1], NULL, NULL, NULL));
      |          ^~
example3.c:70:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   70 |   assert(out= sox_open_write("default", &in->signal, NULL, "alsa", NULL, NULL));
      |          ^~~
  CCLD     example3
  CC       example4.o
  CCLD     example4
  CC       example5.o
In file included from example5.c:27:
example5.c: In function ‘main’:
example5.c:60:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   60 |   assert(in = sox_open_read(argv[1], NULL, NULL, NULL));
      |          ^~
example5.c:64:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   64 |   assert(out = sox_open_memstream_write(&buffer, &buffer_size, &in->signal, NULL, "sox", NULL));
      |          ^~~
example5.c:71:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   71 |   assert(in = sox_open_mem_read(buffer, buffer_size, NULL, NULL, NULL));
      |          ^~
example5.c:72:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   72 |   assert(out = sox_open_write(argv[2], &in->signal, NULL, NULL, NULL, NULL));
      |          ^~~
  CCLD     example5
  CC       example6.o
In file included from example6.c:27:
example6.c: In function ‘main’:
example6.c:89:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   89 |   assert(in = sox_open_read(argv[1], NULL, NULL, NULL));
      |          ^~
example6.c:90:10: warning: suggest parentheses around assignment used as truth value [-Wparentheses]
   90 |   assert(out = sox_open_write(argv[2], &out_signal, &out_encoding, NULL, NULL, NULL));
      |          ^~~
  CCLD     example6
make  all-am
make[2]: Entering directory '/home/ye/tool/sox-14.4.2/src'
make[2]: Leaving directory '/home/ye/tool/sox-14.4.2/src'
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2/src'
make[1]: Entering directory '/home/ye/tool/sox-14.4.2'
make[1]: Nothing to be done for 'all-am'.
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2'
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ 
```

## make install

Final step ...  
Here, I run with sudo.  

```
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ sudo make install
[sudo] password for ye: 
Making install in lpc10
make[1]: Entering directory '/home/ye/tool/sox-14.4.2/lpc10'
make[2]: Entering directory '/home/ye/tool/sox-14.4.2/lpc10'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/sox-14.4.2/lpc10'
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2/lpc10'
Making install in libgsm
make[1]: Entering directory '/home/ye/tool/sox-14.4.2/libgsm'
make[2]: Entering directory '/home/ye/tool/sox-14.4.2/libgsm'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/ye/tool/sox-14.4.2/libgsm'
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2/libgsm'
Making install in src
make[1]: Entering directory '/home/ye/tool/sox-14.4.2/src'
make[2]: Entering directory '/home/ye/tool/sox-14.4.2/src'
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool --silent  --silent --mode=install /usr/bin/install -c   libsox.la '/usr/local/lib'
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool --silent  --silent --mode=install /usr/bin/install -c sox '/usr/local/bin'
make  install-exec-hook
make[3]: Entering directory '/home/ye/tool/sox-14.4.2/src'
if test "yes" = "yes"; then	\
	cd /usr/local/bin; rm -f  play rec; ln -s sox play; ln -s sox rec; \
fi
if test "yes" = "yes"; then	\
	cd /usr/local/bin; rm -f  soxi; ln -s sox soxi; \
fi
make[3]: Leaving directory '/home/ye/tool/sox-14.4.2/src'
 /usr/bin/mkdir -p '/usr/local/include'
 /usr/bin/install -c -m 644 sox.h '/usr/local/include'
make[2]: Leaving directory '/home/ye/tool/sox-14.4.2/src'
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2/src'
make[1]: Entering directory '/home/ye/tool/sox-14.4.2'
make[2]: Entering directory '/home/ye/tool/sox-14.4.2'
make[2]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/usr/local/share/man/man1'
 /usr/bin/install -c -m 644 sox.1 soxi.1 '/usr/local/share/man/man1'
 /usr/bin/mkdir -p '/usr/local/share/man/man3'
 /usr/bin/install -c -m 644 libsox.3 '/usr/local/share/man/man3'
 /usr/bin/mkdir -p '/usr/local/share/man/man7'
 /usr/bin/install -c -m 644 soxformat.7 '/usr/local/share/man/man7'
 /usr/bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 sox.pc '/usr/local/lib/pkgconfig'
make  install-data-hook
make[3]: Entering directory '/home/ye/tool/sox-14.4.2'
cd /usr/local/share/man/man1 && rm -f play.1 && ln -s sox.1 play.1
cd /usr/local/share/man/man1 && rm -f rec.1 && ln -s sox.1 rec.1
cd /usr/local/share/man/man7 && rm -f soxeffect.7 && ln -s ../man1/sox.1 soxeffect.7
make[3]: Leaving directory '/home/ye/tool/sox-14.4.2'
make[2]: Leaving directory '/home/ye/tool/sox-14.4.2'
make[1]: Leaving directory '/home/ye/tool/sox-14.4.2'
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ 
```

## Call --help

```
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ sox --help
sox:      SoX v14.4.2

Usage summary: [gopts] [[fopts] infile]... [fopts] outfile [effect [effopt]]...

SPECIAL FILENAMES (infile, outfile):
-                        Pipe/redirect input/output (stdin/stdout); may need -t
-d, --default-device     Use the default audio device (where available)
-n, --null               Use the `null' file handler; e.g. with synth effect
-p, --sox-pipe           Alias for `-t sox -'

SPECIAL FILENAMES (infile only):
"|program [options] ..." Pipe input from external program (where supported)
http://server/file       Use the given URL as input file (where supported)

GLOBAL OPTIONS (gopts) (can be specified at any point before the first effect):
--buffer BYTES           Set the size of all processing buffers (default 8192)
--clobber                Don't prompt to overwrite output file (default)
--combine concatenate    Concatenate all input files (default for sox, rec)
--combine sequence       Sequence all input files (default for play)
-D, --no-dither          Don't dither automatically
--dft-min NUM            Minimum size (log2) for DFT processing (default 10)
--effects-file FILENAME  File containing effects and options
-G, --guard              Use temporary files to guard against clipping
-h, --help               Display version number and usage information
--help-effect NAME       Show usage of effect NAME, or NAME=all for all
--help-format NAME       Show info on format NAME, or NAME=all for all
--i, --info              Behave as soxi(1)
--input-buffer BYTES     Override the input buffer size (default: as --buffer)
--no-clobber             Prompt to overwrite output file
-m, --combine mix        Mix multiple input files (instead of concatenating)
--combine mix-power      Mix to equal power (instead of concatenating)
-M, --combine merge      Merge multiple input files (instead of concatenating)
--multi-threaded         Enable parallel effects channels processing
--norm                   Guard (see --guard) & normalise
--play-rate-arg ARG      Default `rate' argument for auto-resample with `play'
--plot gnuplot|octave    Generate script to plot response of filter effect
-q, --no-show-progress   Run in quiet mode; opposite of -S
--replay-gain track|album|off  Default: off (sox, rec), track (play)
-R                       Use default random numbers (same on each run of SoX)
-S, --show-progress      Display progress while processing audio data
--single-threaded        Disable parallel effects channels processing
--temp DIRECTORY         Specify the directory to use for temporary files
-T, --combine multiply   Multiply samples of corresponding channels from all
                         input files (instead of concatenating)
--version                Display version number of SoX and exit
-V[LEVEL]                Increment or set verbosity level (default 2); levels:
                           1: failure messages
                           2: warnings
                           3: details of processing
                           4-6: increasing levels of debug messages
FORMAT OPTIONS (fopts):
Input file format options need only be supplied for files that are headerless.
Output files will have the same format as the input file where possible and not
overridden by any of various means including providing output format options.

-v|--volume FACTOR       Input file volume adjustment factor (real number)
--ignore-length          Ignore input file length given in header; read to EOF
-t|--type FILETYPE       File type of audio
-e|--encoding ENCODING   Set encoding (ENCODING may be one of signed-integer,
                         unsigned-integer, floating-point, mu-law, a-law,
                         ima-adpcm, ms-adpcm, gsm-full-rate)
-b|--bits BITS           Encoded sample size in bits
-N|--reverse-nibbles     Encoded nibble-order
-X|--reverse-bits        Encoded bit-order
--endian little|big|swap Encoded byte-order; swap means opposite to default
-L/-B/-x                 Short options for the above
-c|--channels CHANNELS   Number of channels of audio data; e.g. 2 = stereo
-r|--rate RATE           Sample rate of audio
-C|--compression FACTOR  Compression factor for output format
--add-comment TEXT       Append output file comment
--comment TEXT           Specify comment text for the output file
--comment-file FILENAME  File containing comment text for the output file
--no-glob                Don't `glob' wildcard match the following filename

AUDIO FILE FORMATS: 8svx aif aifc aiff aiffc al amb au avr cdda cdr cvs cvsd cvu dat dvms f32 f4 f64 f8 fssd gsm gsrt hcom htk ima ircam la lpc lpc10 lu maud nist prc raw s1 s16 s2 s24 s3 s32 s4 s8 sb sf sl sln smp snd sndr sndt sou sox sph sw txw u1 u16 u2 u24 u3 u32 u4 u8 ub ul uw vms voc vox wav wavpcm wve xa
PLAYLIST FORMATS: m3u pls
AUDIO DEVICE DRIVERS: oss ossdsp

EFFECTS: allpass band bandpass bandreject bass bend biquad chorus channels compand contrast dcshift deemph delay dither divide+ downsample earwax echo echos equalizer fade fir firfit+ flanger gain highpass hilbert input# loudness lowpass mcompand noiseprof noisered norm oops output# overdrive pad phaser pitch rate remix repeat reverb reverse riaa silence sinc speed splice stat stats stretch swap synth tempo treble tremolo trim upsample vad vol
  * Deprecated effect    + Experimental effect    # LibSoX-only effect
EFFECT OPTIONS (effopts): effect dependent; see --help-effect
(base) ye@lst-hpc3090:~/tool/sox-14.4.2$ 
```

:) :) :)  


