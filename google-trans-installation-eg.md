# Google trans command line tool installation

Google machine translation ကို ကိုယ့်စက်ထဲမှာ command line ကနေ run ဖို့အတွက် installation လုပ်တဲ့အခါမှာ gawk မရှိလို့ error ပေးတတ်ပါတယ်။ ကျွန်တော့် ကျောင်းသားတွေအတွက် installation reference အဖြစ်နဲ့ ရေးပေးထားတာပါ။  

## git clone

```
git clone https://github.com/soimort/translate-shell
cd translate-shell/
```

## Running make and got error

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ make
make: gawk: Command not found
Makefile:17: recipe for target 'build' failed
make: *** [build] Error 127
```

## Install gawk if you don't have

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ sudo apt-get install gawk
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  gawk-doc
The following NEW packages will be installed:
  gawk
0 upgraded, 1 newly installed, 0 to remove and 107 not upgraded.
Need to get 401 kB of archives.
After this operation, 1,552 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 gawk amd64 1:4.1.4+dfsg-1build1 [401 kB]
Fetched 401 kB in 3s (137 kB/s)                         
Selecting previously unselected package gawk.
(Reading database ... 298593 files and directories currently installed.)
Preparing to unpack .../gawk_1%3a4.1.4+dfsg-1build1_amd64.deb ...
Unpacking gawk (1:4.1.4+dfsg-1build1) ...
Setting up gawk (1:4.1.4+dfsg-1build1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$
```

## run make again

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ make
[OK] Task build completed.
```

## run sudo make install

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ sudo make install
[OK] Task build completed.
[OK] translate-shell installed.
```

Installation finished!

## run trans --help

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ trans --help
Usage:  trans [OPTIONS] [SOURCE]:[TARGETS] [TEXT]...

Information options:
    -V, -version
        Print version and exit.
    -H, -help
        Print help message and exit.
    -M, -man
        Show man page and exit.
    -T, -reference
        Print reference table of languages and exit.
    -R, -reference-english
        Print reference table of languages (in English names) and exit.
    -L CODES, -list CODES
        Print details of languages and exit.
    -S, -list-engines
        List available translation engines and exit.
    -U, -upgrade
        Check for upgrade of this program.

Translator options:
    -e ENGINE, -engine ENGINE
        Specify the translation engine to use.

Display options:
    -verbose
        Verbose mode. (default)
    -b, -brief
        Brief mode.
    -d, -dictionary
        Dictionary mode.
    -identify
        Language identification.
    -show-original Y/n
        Show original text or not.
    -show-original-phonetics Y/n
        Show phonetic notation of original text or not.
    -show-translation Y/n
        Show translation or not.
    -show-translation-phonetics Y/n
        Show phonetic notation of translation or not.
    -show-prompt-message Y/n
        Show prompt message or not.
    -show-languages Y/n
        Show source and target languages or not.
    -show-original-dictionary y/N
        Show dictionary entry of original text or not.
    -show-dictionary Y/n
        Show dictionary entry of translation or not.
    -show-alternatives Y/n
        Show alternative translations or not.
    -w NUM, -width NUM
        Specify the screen width for padding.
    -indent NUM
        Specify the size of indent (number of spaces).
    -theme FILENAME
        Specify the theme to use.
    -no-theme
        Do not use any other theme than default.
    -no-ansi
        Do not use ANSI escape codes.
    -no-autocorrect
        Do not autocorrect. (if defaulted by the translation engine)
    -no-bidi
        Do not convert bidirectional texts.
    -no-warn
        Do not write warning messages to stderr.
    -dump
        Print raw API response instead.

Audio options:
    -p, -play
        Listen to the translation.
    -speak
        Listen to the original text.
    -n VOICE, -narrator VOICE
        Specify the narrator, and listen to the translation.
    -player PROGRAM
        Specify the audio player to use, and listen to the translation.
    -no-play
        Do not listen to the translation.
    -no-translate
        Do not translate anything when using -speak.
    -download-audio
        Download the audio to the current directory.
    -download-audio-as FILENAME
        Download the audio to the specified file.

Terminal paging and browsing options:
    -v, -view
        View the translation in a terminal pager.
    -pager PROGRAM
        Specify the terminal pager to use, and view the translation.
    -no-view
        Do not view the translation in a terminal pager.
    -browser PROGRAM
        Specify the web browser to use.

Networking options:
    -x HOST:PORT, -proxy HOST:PORT
        Use HTTP proxy on given port.
    -u STRING, -user-agent STRING
        Specify the User-Agent to identify as.

Interactive shell options:
    -I, -interactive, -shell
        Start an interactive shell.
    -E, -emacs
        Start the GNU Emacs front-end for an interactive shell.
    -no-rlwrap
        Do not invoke rlwrap when starting an interactive shell.

I/O options:
    -i FILENAME, -input FILENAME
        Specify the input file.
    -o FILENAME, -output FILENAME
        Specify the output file.

Language preference options:
    -l CODE, -hl CODE, -lang CODE
        Specify your home language.
    -s CODE, -sl CODE, -source CODE, -from CODE
        Specify the source language.
    -t CODES, -tl CODE, -target CODES, -to CODES
        Specify the target language(s), joined by '+'.

Other options:
    -no-init
        Do not load any initialization script.

See the man page trans(1) for more information.
```

If you see above help screen, now you can use google translatation from your command line! :)

## Start using Google Translation Service from your command prompt

ကိုယ့် စက်ရဲ့ locale setting ပေါ်မူတည်ပြီး default ဘာသာပြန်ပေးမဲ့ language က တူမှာ မဟုတ်ဘူး

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ trans "translate me"
translate me

私を翻訳して
(Watashi o hon'yaku shite)

「translate me」の翻訳
[ English -> 日本語 ]

translate me
    私を翻訳して, 私を翻訳
```

## Test Google Translatation Service with other options

source language, target langaugage ကို သတ်မှတ်ပေးလို့ ရတယ်။
ဥပမာ အောက်ပါအတိုင်း

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ trans -brief -no-autocorrect -s en -t my
hello
ဟယ်လို
how are you?
နေကောင်းလား?
i wanna go to Pyin Oo Lwin
ပြင် ဦး လွင်ကိုသွားချင်တယ်
```

## For Your Reference


locale list ကို ကြည့်ချင်ရင်

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ cat /etc/locale.gen | less 
```

ဥပမာ local ကို မြန်မာဘာသာ အဖြစ် ပြောင်းချင်ရင်

```
(base) ye@ykt-pro:/media/ye/Transcend/experiment/gMT/source/translate-shell$ export LANG="my_MM UTF-8"
```
