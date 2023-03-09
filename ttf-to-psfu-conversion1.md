# TTF Font to PSF Font Conversion

https://www.seasip.info/Unix/PSF/#download

အထက်ပါ link ကနေ download လုပ်ပြီး tar.gz ဖိုင်ကို unzip လုပ်ဖို့ ကြိုးစားတာ အဆင်မပြေခဲ့ဘူး။
အဲဒါကြောင့် ... တခြား link ကနေ ရှာ ပြီးအောက်ပါအတိုင်း download လုပ်ကြည့်ခဲ့ .... 

## git clone

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ git clone https://codeberg.org/gnarz/psftools.git
Cloning into 'psftools'...
remote: Enumerating objects: 90, done.
remote: Total 90 (delta 0), reused 0 (delta 0), pack-reused 90
Unpacking objects: 100% (90/90), done.
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

## make

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/psftools$ make
gcc -Wall -Wextra -g -o psfc.o -c psfc.c
gcc -Wall -Wextra -g -o psf.o -c psf.c
gcc -g -o psfc psfc.o psf.o 
gcc -Wall -Wextra -g -o psfd.o -c psfd.c
gcc -g -o psfd psfd.o psf.o 
gcc -Wall -Wextra -g -o psfid.o -c psfid.c
psfid.c: In function ‘main’:
psfid.c:83:9: warning: this statement may fall through [-Wimplicit-fallthrough=]
   83 |      if (opt[2] == '\0' && strchr(options, opt[1]) == 0) {
      |         ^
psfid.c:88:5: note: here
   88 |     default:
      |     ^~~~~~~
gcc -g -o psfid psfid.o psf.o 
gcc -Wall -Wextra -g -o psft.o -c psft.c
gcc -g -o psft psft.o psf.o 
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/psftools$ 
```

## make install

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/psftools$ sudo make install
[sudo] password for ye: 
cp psfc psfd psfid psft /usr/local/bin
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/psftools$ 
```

## check

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/psftools$ psf
psfaddtable    psfc           psfd           psfgettable    psfid          psfstriptable  psft           psfxtable
```

## Check the demo file

```
@psf2
Width: 6
Height: 8
Pixel: #
@0: U+0000
......
......
......
......
......
......
......
......
@1: U+263a
..###.
.#...#
.##.##
.#...#
.##.##
.#.#.#
.#...#
..###.
@2: U+263b
..###.
.#####
.#.#.#
.#####
.#.#.#
.##.##
.#####
..###.
@3: U+2665
..#.#.
.#####
```

## good reference

https://nafe.sourceforge.net/  

I already downloaded:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ mv /media/ye/project1/tmp-download/nafe-0.1.tar.gz .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ tar -xzvf ./nafe-0.1.tar.gz 
nafe-0.1/
nafe-0.1/ChangeLog
nafe-0.1/COPYING
nafe-0.1/Makefile
nafe-0.1/demo6x6.psfu
nafe-0.1/demo8x6.psfu
nafe-0.1/demofont.map
nafe-0.1/demofont.txt
nafe-0.1/psf2txt.c
nafe-0.1/readme.txt
nafe-0.1/txt2psf.c
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

## console font folder

```
/usr/share/consolefonts
```

## check Thai psf font

```
(base) ye@ykt-pro:/usr/share/consolefonts$ cp Thai-Fixed16.psf.gz /media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font/
(base) ye@ykt-pro:/usr/share/consolefonts$ 
```

after copied to the local folder, run gunzip  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ gunzip ./Thai-Fixed16.psf.gz 
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ ls
Thai-Fixed16.psf
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ 

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ psfd ./Thai-Fixed16.psf ./Thai-Fixed16.psf.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ 
```

## Checked the converted text file

```
   1 @psf1
   2 Width: 8
   3 Height: 16
   4 Pixel: #
   5 @0: U+0e0c
   6 ........
   7 ........
   8 ........
   9 ........
  10 ........
  11 ........
  12 ..###..#
  13 .#...#.#
  14 ..#..#.#
  15 .#...#.#
  16 .#...#.#
  17 .#...#.#
  18 .##.####
  19 .##.##.#
  20 ........
  21 ........
  22 @1: U+0e12
  23 ........
  24 ........
  25 ........
  26 ........
  27 ........
  28 ........
  29 ..#.#..#
  30 .#.#.#.#
  31 .#...#.#
  32 .###.#.#
  33 .###.#.#
  34 .#.#.#.#
```

## Check the number of lines

```
4323 @254: U+25a0 U+25ae
4324 ........
4325 ........
4326 ........
4327 ........
4328 ........
4329 ........
4330 .#######
4331 .#######
4332 .#######
4333 .#######
4334 .#######
4335 .#######
4336 .#######
4337 ........
4338 ........
4339 ........
4340 @255: U+00da
4341 ....##..
4342 ..##....
4343 ........
4344 ........
4345 .#....#.
4346 .#....#.
4347 .#....#.
4348 .#....#.
4349 .#....#.
4350 .#....#.
4351 .#....#.
4352 .#....#.
4353 .#....#.
4354 ..####..
4355 ........
4356 ........
```

## Testing psfid command

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ psfid ./Thai-Fixed16.psf
 v:1 w:8 h:16 n:256 u:1

    psfid [-v] [-w] [-h] [-n] [-u] font.psf

print information about a psf font:

  * -v psf version
  * -w font width
  * -h font height
  * -n number of chars in font
  * -u presence of unicode translation table in font (1 for yes, 0 for no)
  * -l list table of encoded chars
```

-l option ကို သုံးပြီး encoded character တွေကို list လုပ်ကြည့်လို့ ရ။ ထိုင်းအတွက်က အောက်ပါအတိုင်း  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ psfid -l ./Thai-Fixed16.psf
467 chars encoded:
U+00020
U+00021
U+00022
U+00023
U+00024
U+00025
U+00026
U+00027
U+00028
U+00029
U+0002a
U+0002b
U+0002c
U+0002d
U+0002e
U+0002f
```

total char ကို wc နဲ့ confirm လုပ်ကြည့်ခဲ့တော့ အောက်ပါအတိုင်း ရ  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ psfid -l ./Thai-Fixed16.psf | wc
    468     470    3755
```

-n option နဲ့ ကြည့်ရင် မြင်ရတဲ့ character အရေအတွက်နဲ့တော့ကွာတယ်။ လေ့လာရလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/check-thai-font$ psfid -n ./Thai-Fixed16.psf
 n:256
```

## Installation of bdf2psf

```
sudo apt-get install bdf2psf
```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ sudo apt-get install bdf2psf
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122 linux-hwe-5.4-headers-5.4.0-124
  linux-hwe-5.4-headers-5.4.0-125 linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132 linux-hwe-5.4-headers-5.4.0-135
  linux-hwe-5.4-headers-5.4.0-136 linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  bdf2psf
0 upgraded, 1 newly installed, 0 to remove and 146 not upgraded.
Need to get 24.4 kB of archives.
After this operation, 228 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 bdf2psf all 1.178ubuntu2.9 [24.4 kB]
Fetched 24.4 kB in 1s (21.9 kB/s)                        
Selecting previously unselected package bdf2psf.
(Reading database ... 665341 files and directories currently installed.)
Preparing to unpack .../bdf2psf_1.178ubuntu2.9_all.deb ...
Unpacking bdf2psf (1.178ubuntu2.9) ...
Setting up bdf2psf (1.178ubuntu2.9) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

Check the command:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ bdf2psf --help
Usage:
bdf2psf [--fb|--raw][--log LOG] BDF{+BDF} EQUIV{+EQUIV} SYMB{+[:]SYMB} SIZE PSF [SFM]

--fb           Create font for framebuffer.
--raw          Create a raw font (SIZE*8 bytes)
--log          A log file for warnings.
BDF{+BDF}      A list of BDF fonts.  The fonts listed first take precedence
               when several fonts define glyphs for same unicode.
EQUIV{+EQUIV}  A list of equivalents files.  Each non-empty line in these files
               contains a list of unicodes to be considered equal (for all of
               them only one position number in the PSF will be reserved).
SYMB{+SYMB}    Files containing lists of symbols to include in the PSF font.
               Unicodes listed first take precedence.  When a file name is
               preceeded by a colon, no warnings about missing symbols in
               the BDF fonts will be issued.
SIZE           Create PSF font with how many character positions
               (usually 256 or 512).
PSF            The new font.  If a file with this name already exists,
               it will be overwritten
SFM            The SFM table of the PSF font.  If a file with this name already
               exists, it will be overwritten.  Optional.
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

## Installation of otf2bdf

```
sudo apt-get install -y otf2bdf
```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ sudo apt-get install -y otf2bdf
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122 linux-hwe-5.4-headers-5.4.0-124
  linux-hwe-5.4-headers-5.4.0-125 linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132 linux-hwe-5.4-headers-5.4.0-135
  linux-hwe-5.4-headers-5.4.0-136 linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  otf2bdf
0 upgraded, 1 newly installed, 0 to remove and 146 not upgraded.
Need to get 26.4 kB of archives.
After this operation, 106 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 otf2bdf amd64 3.1-4 [26.4 kB]
Fetched 26.4 kB in 1s (22.4 kB/s)  
Selecting previously unselected package otf2bdf.
(Reading database ... 665374 files and directories currently installed.)
Preparing to unpack .../otf2bdf_3.1-4_amd64.deb ...
Unpacking otf2bdf (3.1-4) ...
Setting up otf2bdf (3.1-4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```
Check the installed command:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ otf2bdf --help
Usage: otf2bdf [options below] font.ttf
-h		This message.
-v		Print warning messages during conversion.
-l "subset"	Specify a subset of glyphs to generate.
-m mapfile	Glyph reencoding file.
-n		Turn off glyph hinting.
-et		Display the encoding tables available in the font.
-c c		Set the character spacing (default: from font).
-f name		Set the foundry name (default: freetype).
-t name		Set the typeface name (default: from font).
-w name		Set the weight name (default: Medium).
-s name		Set the slant name (default: R).
-k name		Set the width name (default: Normal).
-d name		Set the additional style name (default: empty).
-u char		Set the character to replace '-' in names (default: space).
-pid id		Set the platform ID for encoding (default: 3).
-eid id		Set the encoding ID for encoding (default: 1).
-p n		Set the point size (default: 12pt).
-r n		Set the horizontal and vertical resolution (default: 100dpi).
-rh n		Set the horizontal resolution (default: 100dpi)
-rv n		Set the vertical resolution (default: 100dpi)
-o outfile	Set the output filename (default: stdout).
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ 
```

## Try again

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make all
sh conv.sh
/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf => dejavusansmono: 8conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 12conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 15conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 19conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 
/usr/share/fonts/truetype/freefont/FreeMono.ttf => freemono: 8conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 12conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 15conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 19conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 
/usr/share/fonts/truetype/liberation2/LiberationMono-Regular.ttf => liberationmono-regular: 8conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 12conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 15conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 19conv.sh: line 43: psf2txt: command not found
conv.sh: line 44: psf2txt: command not found
:x 
touch .done
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ 
```

psf2txt command မတွေ့ဘူးလို့ အထက်ပါအတိုင်း error message ပေးတယ်။  
အဲဒါကြောင် psf2txt ကို install လုပ်ကြည့်မယ်။  

## Installation of psf2txt, txt2psf Through NAFE

NAFE မှာ psf2txt.c, txt2psf.c ဆိုတဲ့ source code တွေ ပါတာတွေ့လို့ ...  
NAFE ကို install လုပ်ကြည့်ခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ make all
/usr/local/bin/ccache-gcc     txt2psf.c   -o txt2psf
txt2psf.c: In function ‘error’:
txt2psf.c:12:4: warning: implicit declaration of function ‘exit’ [-Wimplicit-function-declaration]
   12 |    exit(1);
      |    ^~~~
txt2psf.c:12:4: warning: incompatible implicit declaration of built-in function ‘exit’
txt2psf.c:9:1: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
    8 | #include <stdio.h>
  +++ |+#include <stdlib.h>
    9 | 
txt2psf.c: In function ‘main’:
txt2psf.c:42:4: warning: incompatible implicit declaration of built-in function ‘exit’
   42 |    exit(1);
      |    ^~~~
txt2psf.c:42:4: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
/usr/local/bin/ccache-gcc     psf2txt.c   -o psf2txt
psf2txt.c: In function ‘error’:
psf2txt.c:12:4: warning: implicit declaration of function ‘exit’ [-Wimplicit-function-declaration]
   12 |    exit(1);
      |    ^~~~
psf2txt.c:12:4: warning: incompatible implicit declaration of built-in function ‘exit’
psf2txt.c:9:1: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
    8 | #include <stdio.h>
  +++ |+#include <stdlib.h>
    9 | 
psf2txt.c: In function ‘main’:
psf2txt.c:43:4: warning: incompatible implicit declaration of built-in function ‘exit’
   43 |    exit(1);
      |    ^~~~
psf2txt.c:43:4: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
```

Installation ပြီးသွားတဲ့အခါမှာ ls ခေါ်ကြည့်တော့ အောက်ပါအတိုင်း ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ ls
ChangeLog  demo6x6.psfu  demofont.map  Makefile  psf2txt.c   txt2psf
COPYING    demo8x6.psfu  demofont.txt  psf2txt   readme.txt  txt2psf.c
```

Check psf2txt command:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ ./psf2txt --help
NAFE v 0.1 -- not another font editor!
Copyleft 2004 by Corvus Corax
Distributed under GPL -- NO WARRANTY!
Usage: ./psf2txt <fontfile.psf> <outfile.txt>
```

Check txt2psf command:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ ./txt2psf --help
NAFE v 0.1 -- not another font editor!
Copyleft 2004 by Corvus Corax
Distributed under GPL -- NO WARRANTY!
Usage: ./txt2psf <fontfile.txt> <outfile.psf>
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ 
```

local folder မှာတော့ အလုပ်လုပ်တယ်။  

## copied two files

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ sudo cp psf2txt /usr/bin/
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/nafe-0.1$ sudo cp txt2psf /usr/bin/
```

## Try again 

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make clean
rm -f *.psfu *.psfu.gz *.log *.bdf .done
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make all
sh conv.sh
/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf => dejavusansmono: 8:x 12:x 15:x 19:x 
/usr/share/fonts/truetype/freefont/FreeMono.ttf => freemono: 8:x 12:x 15:x 19:x 
/usr/share/fonts/truetype/liberation2/LiberationMono-Regular.ttf => liberationmono-regular: 8:x 12:x 15:x 19:x 
touch .done
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ 
```

အထက်ပါအတိုင်း ဒီတစ်ခါတော့ make က error မပေးတော့ဘူး။  

## Learn Makefile

```bash
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ cat Makefile 
PROJECT=ttf-console-fonts
PSFDIR=/usr/share/kbd/consolefonts

.PHONY: all clean install push tarball

all: .done

.done: conv.sh fonts ttf2psfu.sh
	sh conv.sh
	touch .done

clean:
	rm -f *.psfu *.psfu.gz *.log *.bdf .done

install: all
	mkdir -p $(DESTDIR)$(PSFDIR)
	install -m0644 *.psfu.gz $(DESTDIR)$(PSFDIR)

push: clean
	git push

tarball: push
	sh mktarball.sh $(PROJECT)
```

## Learn the conv.sh

```bash
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ cat conv.sh
#!/bin/bash

# 20170403 bkw:

# convert TTF (or OTF) fonts to *.psfu.gz fonts that can be used
# on the Linux console.

# conversion isn't done directly. instead, the TTF is rendered as a
# BDF (via otf2bdf), then converted to a psfu via bdf2psf.

# these are supposedly in points. yeah, right.
SIZES=${SIZES:-8 12 15 19}

warn() {
	echo "$@" 1>&2
}

die() {
	warn "$@"
	exit 1
}

convfont() {
	font="$1"
	file="$( fc-list "$font" | head -n1 | cut -d: -f1 )"

	psfname="$( basename "$( echo $file | cut -d. -f1 | tr A-Z a-z | tr -d " " )" )"
	echo -n "$file => $psfname: "

	if [ ! -e "$file" ]; then
		warn "Font '$font' not found, skipping"
		return 1
	fi

	for size in $SIZES; do
		echo -n "$size"
		sh ./ttf2psfu.sh -p $size "$file" &> $psfname.$size.log

		# bug in file? if the width is double-digit, file prints HxW, but if
		# width is single-digit it prints WxH, WTF?
		#pxsize=$( file test.psfu | sed 's|.*, \(.*\)x\(.*\)$|\2x\1|' )

		w="$( psf2txt test.psfu | sed -n '/^Width/s,.* ,,p' )"
		h="$( psf2txt test.psfu | sed -n '/^Height/s,.* ,,p' )"
		pxsize=${w}x${h}
		gzip -9c < test.psfu > $psfname-$pxsize.psfu.gz
		rm -f test.psfu
		echo -n ":$pxsize "
	done
	echo
}

cat fonts | while read font; do
	convfont "$font"
done
```

## Update the Makefile path and run again

path ကို အောက်ပါအတိုင်း ပြင်ကြည့်ခဲ့  

```
PROJECT=ttf-console-fonts
#PSFDIR=/usr/share/kbd/consolefonts
PSFDIR=/usr/share/consolefonts
```

ပြီး make clean လုပ်ပြီး make ထပ် run ခဲ့တော့ အောက်ပါအတိုင်း  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make clean
rm -f *.psfu *.psfu.gz *.log *.bdf .done
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make
sh conv.sh
/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf => dejavusansmono: 8:x 12:x 15:x 19:x 
/usr/share/fonts/truetype/freefont/FreeMono.ttf => freemono: 8:x 12:x 15:x 19:x 
/usr/share/fonts/truetype/liberation2/LiberationMono-Regular.ttf => liberationmono-regular: 8:x 12:x 15:x 19:x 
touch .done
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ lsconv.sh                dejavusansmono-x.psfu.gz  freemono.8.log                 liberationmono-regular.8.log      tmp.bdf
dejavusansmono.12.log  fonts                     freemono-x.psfu.gz             liberationmono-regular-x.psfu.gz  ttf2psfu.sh
dejavusansmono.15.log  freemono.12.log           liberationmono-regular.12.log  Makefile
dejavusansmono.19.log  freemono.15.log           liberationmono-regular.15.log  mktarball.sh
dejavusansmono.8.log   freemono.19.log           liberationmono-regular.19.log  README
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$
```

မထူးခြားဘူး ...  
အောက်ပါ font သုံးဖိုင်အတွက်တော့ လုပ်ပေးသွားတယ် ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ ls *.gz
dejavusansmono-x.psfu.gz  freemono-x.psfu.gz  liberationmono-regular-x.psfu.gz
```

## Check the filename fonts

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ cat fonts
DejaVu Sans Mono:style=Book
FreeMono:style=Regular
Liberation Mono:style=Regular
```

ဒီ fonts ဆိုတဲ့ ဖိုင်ထဲမှာ ပေးထားတဲ့ ဖိုင်နာမည်တွေကိုပဲ ဖတ်ပြီး ttf to psfu ဖိုင်အဖြစ် ပြောင်းပေးသွားပုံရတယ်။  

## Updating the "fonts" file

အရင်ဆုံး မြန်မာဖောင့်တွေကို စစ်ကြည့်ခဲ့ ....   

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ fc-list | grep "Myanmar"
/usr/share/fonts/truetype/noto/NotoSansMyanmar-Bold.ttf: Noto Sans Myanmar:style=Bold
/home/ye/.local/share/fonts/mm_Finger.ttf: Myanmar Finger Spelling (ver 2.0):style=Regular
/home/ye/.local/share/fonts/myanmar3.ttf: Myanmar3:style=Regular
/usr/share/fonts/truetype/noto/NotoSerifMyanmar-Bold.ttf: Noto Serif Myanmar:style=Bold
/usr/share/fonts/truetype/noto/NotoSansMyanmarUI-Regular.ttf: Noto Sans Myanmar UI:style=Regular
/usr/share/fonts/truetype/noto/NotoSansMyanmar-Regular.ttf: Noto Sans Myanmar:style=Regular
/usr/share/fonts/truetype/noto/NotoSansMyanmarUI-Bold.ttf: Noto Sans Myanmar UI:style=Bold
/usr/share/fonts/truetype/noto/NotoSerifMyanmar-Regular.ttf: Noto Serif Myanmar:style=Regular
```

ပြီးတော့ fonts ဖိုင်ကို fonts.original အဖြစ် နာမည်ပြောင်းသိမ်းခဲ့ ...   

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ mv fonts fonts.original
```

ပြီးမှ fonts ဖိုင်အသစ်ကို ဖန်တီးခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ cat ./fonts
Myanmar3:style=Regular
```

make လုပ်ကြည့်တော့ Myanmar3 ဖောင့် ttf ဖိုင်ကို ပြောင်းပေးတာကို တွေ့ခဲ့ရ ... :)  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ make
sh conv.sh
/home/ye/.local/share/fonts/myanmar3.ttf => ye: 8:x 12:x 15:x 19:x 
touch .done
```

## Check the Converted File

backup အရင်ကူး  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ cp ye-x.psfu.gz ./bk/
```

gunzip ကို run  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ gunzip ./ye-x.psfu.gz 
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ ls ./ye-x.psfu 
./ye-x.psfu
```

file command နဲ့ check လုပ်ကြည့်ခဲ့ ...   

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ file ./ye-x.psfu 
./ye-x.psfu: Linux/i386 PC Screen Font v2 data, 512 characters, Unicode directory, 32x16
```

## Convert Myanmar3 psfu File into Text File

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ psfd ./ye-x.psfu ./ye-x.psfu.txt
```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/ttf-console-fonts-20170403_abc5771$ psfid ./ye-x.psfu
 v:2 w:16 h:32 n:512 u:1(base)
```

## Check the Converted Text File

လိုင်းက ထိုင်းဖိုင်ထက် အများကြီး ပိုတာကို တွေ့ရတယ်။   
ပြီးတော့ မြန်မာစာ စာလုံးတွေကို ထင်ထင်ရှားရှား မတွေ့ရဘူး။  
x, y လည်း အများကြီး ပိုယူထားသလားလို့ ....   

```
16867 ##.##...###.##.#
16868 @511
16869 #.#.###.##.##.#.
16870 #.##.#.#.##.....
16871 ###...####.#.###
16872 ##..##..####.#..
16873 ##...###....#..#
16874 #....##...#.#.##
16875 .#....#.###...##
16876 #.#.......#.####
16877 ##.##..##.#..#.#
16878 ..#.#.##.#######
16879 ####.#####...#..
16880 .#...#...#...#..
16881 #.##...#.#.#....
16882 .#...#.#.####.#.
16883 #.#...##...#.###
16884 ##.#.####.#..###
16885 ###....##..###.#
16886 #...#..##.#..##.
16887 .#.####.########
16888 ##.##.....#..##.
16889 #.##.#.#.....#..
16890 .###.#.#.#...#..
16891 ..#....#.#.##.#.
16892 #....###.......#
16893 .....#..##.##.##
16894 ###.#..##..#.#.#
16895 #..#.###...#####
16896 #.##.#..##.##.##
16897 .##.#..#..###.#.
16898 .###..#..#..#..#
16899 ##..#####.#...##
16900 ...##........#.#
```

ဒါပေမဲ အင်္ဂလိပ်စာလုံး တချို့ကိုတော့ သေသေချာချာ တွေ့ရတယ်။ အောက်ပါအတိုင်း    

```
 1 @psf2
    2 Width: 16
    3 Height: 32
    4 Pixel: #
    5 @0: U+00d7
    6 ................
    7 ................
    8 ................
    9 ................
   10 ................
   11 ................
   12 ................
   13 ................
   14 ................
   15 ................
   16 ................
   17 ..#.......#.....
   18 .###.....##.....
   19 ..###...##......
   20 ...###.##.......
   21 ....####........
   22 .....###........
   23 ....#####.......
   24 ...###.###......
   25 ..###....##.....
   26 ..##......#.....
   27 ................
   28 ................
   29 ................
   30 ................
   31 ................
   32 ................
   33 ................
   34 ................
```

```
1191 ................
 1192 ................
 1193 @36: U+0024
 1194 ................
 1195 ......##........
 1196 ......##........
 1197 ......##........
 1198 ......##........
 1199 ....#####.......
 1200 ...########.....
 1201 ..##########....
 1202 ..##..##.###....
 1203 ..##..##.###....
 1204 ..##..##.##.....
 1205 ..###.##........
 1206 ..######........
 1207 ...######.......
 1208 .....######.....
 1209 ......######....
 1210 ..##..##..###...
 1211 ..###.##...##...
 1212 .####.##...##...
 1213 .####.##..###...
 1214 ..###.##.####...
 1215 ...#########....
 1216 ....#######.....
 1217 ......##........
 1218 ......##........
```

```
1626 ................
 1627 ......###.......
 1628 .....####.......
 1629 ....#####.......
 1630 ...######.......
 1631 ..####.##.......
 1632 .###...##.......
 1633 ###....##.......
 1634 .......##.......
 1635 .......##.......
 1636 .......##.......
 1637 .......##.......
 1638 .......##.......
 1639 .......##.......
 1640 .......##.......
 1641 .......##.......
 1642 .......##.......
 1643 .......##.......
 1644 ..###########...
 1645 ..###########...
 1646 ................
 1647 ................
 1648 ................
```

```
2579 @78: U+004e U+039d U+24c3
 2580 ................
 2581 ................
 2582 ................
 2583 ................
 2584 ................
 2585 ####.....######.
 2586 ####.....######.
 2587 ..###......##...
 2588 ..###......##...
 2589 ..####.....##...
 2590 ..#####....##...
 2591 ..##.##....##...
 2592 ..##.###...##...
 2593 ..##..###..##...
 2594 ..##...##..##...
 2595 ..##...###.##...
 2596 ..##....##.##...
 2597 ..##....#####...
 2598 ..##.....####...
 2599 ..##......###...
 2600 ..##......###...
 2601 ######.....####.
 2602 ######.....####.
 2603 ................
 2604 ................
 2605 ................
```

## Reference

- https://codeberg.org/gnarz/psftools/src/branch/master
- https://www.seasip.info/Unix/PSF/



