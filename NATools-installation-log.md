# NATools Installation Log 

ဒီ tool က ငါသိတာကြာပြီ။ ဒါပေမဲ့ မသုံးဖြစ်သေးဘူး။ သူ့မှာက C programming coding ရော Perl ရော ပါတယ်။  
perl နဲ့ပဲ သုံးကြည့်တာက မြန်မာစာ၊ တိုင်းရင်းသားစာတွေအတွက် ပိုအဆင်ပြေလိမ့်မယ်လို့ ယူဆ...  

**ဒီ log ဖိုင်ကို ဖတ်ပြီး လိုက်လုပ်ကြည့်ကြမယ့် သူများအတွက် ကြိုတင် သတိပေးထားချင်တယ်**

အောက်က Download/Unzip NATools က source ကနေ install လုပ်ဖို့ ကြိုးစားကြည့်ထားတော့ version က နိမ့်နေတာနဲ့ error တက်တာကို log အနေနဲ့ မှတ်သားထားတာပါ။ တကယ်က perl module ကို တန်း install လုပ်တာက မပင်ပန်းပဲ အဆင်ပြေပါလိမ့်မယ်။  
အဲဒါကြောင့် "Try NATools Updated Version of Perl Module" ဆိုတဲ့ အဆင့်ကို ကျော်ကြည့်ပါ။  

## Download/Unzip NATools

Download NATools from the following link:  
[http://linguateca.di.uminho.pt/natools/](http://linguateca.di.uminho.pt/natools/)  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ mv ../NATools-0.5.10.tar.gz .
```

unzip "tar.gz" file  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ tar -xf ./NATools-0.5.10.tar.gz 
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ ls
NATools-0.5.10  NATools-0.5.10.tar.gz
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ tree ./NATools-0.5.10
./NATools-0.5.10
├── 3rdParty
│   ├── interface-freeling.pl
│   ├── interface-jspell.pl
│   ├── Makefile.am
│   └── Makefile.in
├── acinclude.m4
├── aclocal.m4
├── AUTHORS
├── ChangeLog
├── compile
├── config.guess
├── config.h.in
├── config.sub
├── configure
├── configure.ac
├── COPYING
├── data
│   ├── Makefile.am
│   ├── Makefile.in
│   └── rules.pt-en
├── depcomp
├── INSTALL
├── install-sh
├── ltmain.sh
├── Makefile.am
├── Makefile.in
├── missing
├── NAT
│   ├── cgis
│   │   ├── nat-about.cgi
│   │   ├── nat-dict.cgi
│   │   ├── nat-matrix.cgi
│   │   ├── nat-ngrams.cgi
│   │   ├── nat-ntd-browse.cgi
│   │   ├── nat-search.cgi
│   │   └── nat-translate.cgi
│   ├── examples
│   │   ├── ambs-2
│   │   ├── ambs-mk-compalinha-1
│   │   ├── ambs-mk-compalinha-2
│   │   ├── ambs-mk-compalinha-3
│   │   ├── ambs-test-rules
│   │   ├── jj-1
│   │   ├── jj-10-trigrams
│   │   ├── jj-11-tmxmetrics
│   │   ├── jj-12-term_extract
│   │   ├── jj-2
│   │   ├── jj-3
│   │   ├── jj-4
│   │   ├── jj-5
│   │   ├── jj-6
│   │   ├── jj-7
│   │   ├── jj-8
│   │   ├── jj-9
│   │   ├── markerHypothesis.pl
│   │   ├── Markers.EN
│   │   ├── Markers.PT
│   │   ├── nat-analyzePair
│   │   ├── nat-best
│   │   ├── nat-compareFiles
│   │   ├── nat-subtractDict
│   │   ├── nat-tmxfilter
│   │   └── nat-word-chunk
│   ├── Makefile.PL
│   ├── MANIFEST
│   ├── MANIFEST.SKIP
│   ├── META.yml
│   ├── NAT
│   │   ├── CGI.pm
│   │   ├── Client.pm
│   │   ├── Config.pm
│   │   ├── Corpus.pm
│   │   ├── Dict.pm
│   │   ├── Lexicon.pm
│   │   ├── Matrix.pm
│   │   ├── NATDict.pm
│   │   ├── PatternRules.yp
│   │   ├── PCorpus.pm
│   │   ├── PTD
│   │   │   ├── BzDmp.pm
│   │   │   ├── Dumper.pm
│   │   │   ├── SQLite.pm
│   │   │   └── XzDmp.pm
│   │   ├── PTD.pm
│   │   ├── Translator
│   │   │   ├── method1.pm
│   │   │   └── method2.pm
│   │   └── Translator.pm
│   ├── NAT.pm.in
│   ├── NAT.xs
│   ├── scripts
│   │   ├── nat-addDict
│   │   ├── nat-codify
│   │   ├── nat-compareDicts
│   │   ├── nat-create
│   │   ├── nat-dict
│   │   ├── nat-dumpDicts
│   │   ├── nat-examplesExtractor
│   │   ├── nat-lex2perl
│   │   ├── nat-makeCWB
│   │   ├── nat-mkMakefile
│   │   ├── nat-mkRealDict
│   │   ├── nat-ngramsIdx
│   │   ├── nat-pair2tmx
│   │   ├── nat-ptd
│   │   ├── nat-rank
│   │   ├── nat-sentence-align.in
│   │   ├── nat-shell
│   │   ├── nat-StarDict
│   │   ├── nat-substDict
│   │   ├── nat-tmx2pair
│   │   ├── nat-translate-shell
│   │   └── README
│   ├── t
│   │   ├── 00_basic.t
│   │   ├── 01_config.t
│   │   ├── 02_ptd.dmp
│   │   ├── 02_ptd.t
│   │   ├── 05_pairs.t
│   │   ├── 10_pcorpus.t
│   │   ├── 11_corpus.t
│   │   ├── 14_scripts.t
│   │   ├── 15_cgis.t
│   │   ├── 16_pods.t
│   │   ├── 17_pod_coverage.t
│   │   ├── 20_patterns.dic1
│   │   ├── 20_patterns.dic2
│   │   ├── 20_patterns.in
│   │   ├── 20_patterns.t
│   │   └── 99_sawAmpersand.t
│   └── typemap
├── NEWS
├── pods
│   ├── Makefile.am
│   ├── Makefile.in
│   ├── nat-css.pod
│   ├── nat-initmat.pod
│   ├── nat-ipfp.pod
│   ├── nat-mat2dic.pod
│   ├── nat-postbin.pod
│   ├── nat-pre.pod
│   ├── nat-samplea.pod
│   ├── nat-sampleb.pod
│   └── nat-sentalign.pod
├── README
├── src
│   ├── adddic.c
│   ├── bucket.c
│   ├── bucket.h
│   ├── corpus.c
│   ├── corpus.h
│   ├── corpusinfo.c
│   ├── corpusinfo.h
│   ├── dictionary.c
│   ├── dictionary.h
│   ├── grep.c
│   ├── initmat.c
│   ├── invindex.c
│   ├── invindex.h
│   ├── invindexjoin.c
│   ├── ipfp.c
│   ├── isolatin.c
│   ├── isolatin.h
│   ├── Makefile.am
│   ├── Makefile.in
│   ├── mat2dic.c
│   ├── matrix.c
│   ├── matrix.h
│   ├── mkdict.c
│   ├── natdict.c
│   ├── natdict.h
│   ├── natlexicon.c
│   ├── natlexicon.h
│   ├── ngramidx.c
│   ├── ngramidx.h
│   ├── ngrams_bdb.c
│   ├── ntdump.c
│   ├── parseini.c
│   ├── parseini.h
│   ├── partials.c
│   ├── partials.h
│   ├── postbin.c
│   ├── pre.c
│   ├── samplea.c
│   ├── sampleb.c
│   ├── search_sentence.c
│   ├── sent_align.c
│   ├── server
│   │   ├── Makefile.am
│   │   ├── Makefile.in
│   │   └── server.c
│   ├── srvshared.c
│   ├── srvshared.h
│   ├── standard.c
│   ├── standard.h
│   ├── tempdict.c
│   ├── tempdict.h
│   ├── words2id.c
│   ├── words.c
│   └── words.h
├── t
│   ├── corpus.input
│   ├── corpus.t
│   ├── corpus_t.c
│   ├── input
│   │   ├── EN-tok
│   │   ├── EN-tok.wc
│   │   ├── Makefile.am
│   │   ├── Makefile.in
│   │   ├── PT-tok
│   │   └── PT-tok.wc
│   ├── Makefile.am
│   ├── Makefile.in
│   ├── nat-pre.t
│   ├── nat-these.t
│   ├── words.input
│   ├── words.t
│   └── words_t.c
└── THANKS

15 directories, 204 files
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$
```

ငါတို့မှာက sentence level alignment လုပ်ထားပြီးသား parallel corpus က ရှိထားပြီးသား...  
အဲဒါကြောင့် sentence level alignment က လုပ်စရာ မလိုဘူး။  

## NATools Installation

Installation အတွက်က အောက်ပါ link ကို refer လုပ်ခဲ့တယ်။  
[http://linguateca.di.uminho.pt/natools/htdocs/install.html](http://linguateca.di.uminho.pt/natools/htdocs/install.html)  

cpan (Perl installation shell) က ကိုယ့်စက်ထဲမှာ ရှိတယ်ဆိုရင် command prompt မှာ "cpan" ဆိုပြီး ရိုက်လိုက်ပြီးတော့ ကိုယ် install လုပ်ချင်တဲ့ perl module တွေကို တစ်ခုပြီး တစ်ခု "install \<perl-module-name\>" ပေးပြီး ရိုက်သွားပါ။  
တချို့ လိုအပ်တဲ့နေရာတွေမှာ admin password ရိုက်ပေးဖို့တောင်းတာမျိုးလည်း ရှိပါတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ cpan
Terminal does not support AddHistory.

To fix that, maybe try>  install Term::ReadLine::Perl

cpan[1]> install Lingua::PT::PLNbase
Reading '/home/ye/.cpan/Metadata'
  Database was generated on Fri, 26 Mar 2021 11:17:03 GMT
Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/home/ye/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/02packages.details.txt.gz
Reading '/home/ye/.cpan/sources/modules/02packages.details.txt.gz'
  Database was generated on Wed, 08 Dec 2021 01:29:02 GMT
.............
  New CPAN.pm version (v2.29) available.
  [Currently running version is v2.28]
  You might want to try
    install CPAN
    reload cpan
  to both upgrade CPAN.pm and run the new version without leaving
  the current session.


...............................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/03modlist.data.gz
Reading '/home/ye/.cpan/sources/modules/03modlist.data.gz'
DONE
Writing /home/ye/.cpan/Metadata
Running install for module 'Lingua::PT::PLNbase'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/Lingua-PT-PLNbase-0.27.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-PT-PLNbase-0.27.tar.gz ok
Scanning cache /home/ye/.cpan/build for sizes
...............................---------------------------------------------DONE
DEL(1/3): /home/ye/.cpan/build/Test-Warn-0.36-0 
DEL(2/3): /home/ye/.cpan/build/CGI-4.51-0 
DEL(3/3): /home/ye/.cpan/build/Lingua-Sentence-1.100-0 
'YAML' not installed, will not store persistent state
Configuring A/AM/AMBS/Lingua-PT-PLNbase-0.27.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Warning: prerequisite File::Slurp 0 not found.
Warning: prerequisite Lingua::PT::Abbrev 0.05 not found.
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for Lingua::PT::PLNbase
Writing MYMETA.yml and MYMETA.json
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for A/AM/AMBS/Lingua-PT-PLNbase-0.27.tar.gz
---- Unsatisfied dependencies detected during ----
----    AMBS/Lingua-PT-PLNbase-0.27.tar.gz    ----
    File::Slurp [build_requires]
    Lingua::PT::Abbrev [requires]
Running install for module 'File::Slurp'
Fetching with LWP:
http://www.cpan.org/authors/id/C/CA/CAPOEIRAB/File-Slurp-9999.32.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/C/CA/CAPOEIRAB/File-Slurp-9999.32.tar.gz ok
Configuring C/CA/CAPOEIRAB/File-Slurp-9999.32.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for File::Slurp
Writing MYMETA.yml and MYMETA.json
  CAPOEIRAB/File-Slurp-9999.32.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for C/CA/CAPOEIRAB/File-Slurp-9999.32.tar.gz
cp lib/File/Slurp.pm blib/lib/File/Slurp.pm
Manifying 1 pod document
  CAPOEIRAB/File-Slurp-9999.32.tar.gz
  /usr/bin/make -- OK
Running make test for CAPOEIRAB/File-Slurp-9999.32.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00-report-prereqs.t ......... # 
# Versions for all modules listed in MYMETA.json (including optional ones):
# 
# === Configure Requires ===
# 
#     Module              Want Have
#     ------------------- ---- ----
#     ExtUtils::MakeMaker  any 7.58
# 
# === Build Requires ===
# 
#     Module              Want Have
#     ------------------- ---- ----
#     ExtUtils::MakeMaker  any 7.58
# 
# === Test Requires ===
# 
#     Module         Want     Have
#     -------------- ---- --------
#     Carp            any     1.50
#     Exporter       5.57     5.74
#     Fcntl           any     1.13
#     File::Basename  any     2.85
#     File::Spec     3.01     3.78
#     File::Temp      any   0.2311
#     IO::Handle      any     1.45
#     POSIX           any     1.88
#     Scalar::Util   1.00     1.55
#     Socket          any    2.031
#     Symbol          any     1.08
#     Test::More      any 1.302183
#     overload        any     1.30
#     strict          any     1.11
#     warnings        any     1.44
# 
# === Runtime Requires ===
# 
#     Module         Want   Have
#     -------------- ---- ------
#     B               any   1.76
#     Carp            any   1.50
#     Errno           any   1.30
#     Exporter       5.57   5.74
#     Fcntl           any   1.13
#     File::Basename  any   2.85
#     File::Spec     3.01   3.78
#     File::Temp      any 0.2311
#     IO::Handle      any   1.45
#     POSIX           any   1.88
#     strict          any   1.11
#     warnings        any   1.44
# 
t/00-report-prereqs.t ......... ok   
t/01-error_edit_file.t ........ ok     
t/01-error_edit_file_lines.t .. ok     
t/01-error_prepend_file.t ..... ok     
t/01-error_read_dir.t ......... ok     
t/01-error_read_file.t ........ ok     
t/01-error_write_file.t ....... ok       
t/append_null.t ............... ok   
t/binmode.t ................... ok   
t/data_glob.t ................. ok     
t/data_section.t .............. ok   
t/edit_file.t ................. ok     
t/error.t ..................... ok     
t/file_object.t ............... ok     
t/handle.t .................... ok   
t/inode.t ..................... ok   
t/large.t ..................... ok       
t/newline.t ................... ok   
t/no_clobber.t ................ ok   
t/original.t .................. ok   
t/paragraph.t ................. ok     
t/perms.t ..................... ok     
t/prepend_file.t .............. ok     
t/pseudo.t .................... ok   
t/read_dir.t .................. ok   
t/slurp.t ..................... ok   
t/stdin.t ..................... ok   
t/stringify.t ................. ok   
t/tainted.t ................... skipped: Taint was always terrible. Just stop it already.
t/write_file_win32.t .......... ok   
All tests successful.
Files=30, Tests=629,  2 wallclock secs ( 0.08 usr  0.01 sys +  1.41 cusr  0.18 csys =  1.68 CPU)
Result: PASS
Terminal does not support GetHistory.
Lockfile removed.
  CAPOEIRAB/File-Slurp-9999.32.tar.gz
  /usr/bin/make test -- OK
Running make install for CAPOEIRAB/File-Slurp-9999.32.tar.gz
[sudo] password for ye: 
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/File/Slurp.pm
Installing /usr/local/man/man3/File::Slurp.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  CAPOEIRAB/File-Slurp-9999.32.tar.gz
  sudo /usr/bin/make install  -- OK
Running install for module 'Lingua::PT::Abbrev'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/Lingua-PT-Abbrev-0.10.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-PT-Abbrev-0.10.tar.gz ok
Configuring A/AM/AMBS/Lingua-PT-Abbrev-0.10.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for Lingua::PT::Abbrev
Writing MYMETA.yml and MYMETA.json
  AMBS/Lingua-PT-Abbrev-0.10.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for A/AM/AMBS/Lingua-PT-Abbrev-0.10.tar.gz
cp lib/Lingua/PT/Abbrev.pm blib/lib/Lingua/PT/Abbrev.pm
perl ./data/cpdata.pl
Manifying 1 pod document
  AMBS/Lingua-PT-Abbrev-0.10.tar.gz
  /usr/bin/make -- OK
Running make test for AMBS/Lingua-PT-Abbrev-0.10.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00.load.t ....... ok   
t/04.regexp.t ..... ok   
t/pod-coverage.t .. ok   
t/pod.t ........... ok   
All tests successful.
Files=4, Tests=8,  0 wallclock secs ( 0.01 usr  0.01 sys +  0.13 cusr  0.03 csys =  0.18 CPU)
Result: PASS
  AMBS/Lingua-PT-Abbrev-0.10.tar.gz
  /usr/bin/make test -- OK
Running make install for AMBS/Lingua-PT-Abbrev-0.10.tar.gz
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/Lingua/PT/Abbrev.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PT/Abbrev/abbrev.dat
Installing /usr/local/man/man3/Lingua::PT::Abbrev.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  AMBS/Lingua-PT-Abbrev-0.10.tar.gz
  sudo /usr/bin/make install  -- OK
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-PT-PLNbase-0.27-0
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  Has already been prepared
Running make for A/AM/AMBS/Lingua-PT-PLNbase-0.27.tar.gz
cp lib/Lingua/PT/PLNbase.pm blib/lib/Lingua/PT/PLNbase.pm
cp scripts/sentences blib/script/sentences
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/sentences
Manifying 1 pod document
Manifying 1 pod document
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  /usr/bin/make -- OK
Running make test for AMBS/Lingua-PT-PLNbase-0.27.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00_segmenter1.t ... ok     
t/00_segmenter2.t ... ok     
t/01_tokenizer1.t ... ok     
t/01_tokenizer2.t ... ok     
t/01_tokenizer3.t ... ok   
t/02_accents.t ...... ok     
t/03_fsegmenter1.t .. ok   
t/pod-coverage.t .... ok   
t/pod.t ............. ok   
All tests successful.
Files=9, Tests=134,  1 wallclock secs ( 0.02 usr  0.02 sys +  0.36 cusr  0.08 csys =  0.48 CPU)
Result: PASS
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  /usr/bin/make test -- OK
Running make install for AMBS/Lingua-PT-PLNbase-0.27.tar.gz
Manifying 1 pod document
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/Lingua/PT/PLNbase.pm
Installing /usr/local/man/man1/sentences.1p
Installing /usr/local/man/man3/Lingua::PT::PLNbase.3pm
Installing /usr/local/bin/sentences
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  AMBS/Lingua-PT-PLNbase-0.27.tar.gz
  sudo /usr/bin/make install  -- OK

cpan[2]> 


```

install XML::TMX  
install XML::DT  
install Compress::Zlib  
install Storable  
install MLDBM  
install DB_File လုပ်တဲ့အခါမှာ အောက်ပါအတိုင်း error တက်တယ်...  

```
cpan[7]> install DB_File
Running install for module 'DB_File'
Fetching with LWP:
http://www.cpan.org/authors/id/P/PM/PMQS/DB_File-1.856.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/P/PM/PMQS/DB_File-1.856.tar.gz ok
Configuring P/PM/PMQS/DB_File-1.856.tar.gz with Makefile.PL
Parsing config.in...
Looks Good.
Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Warning (mostly harmless): No library found for -ldb
Generating a Unix-style Makefile
Writing Makefile for DB_File
Writing MYMETA.yml and MYMETA.json
  PMQS/DB_File-1.856.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for P/PM/PMQS/DB_File-1.856.tar.gz
cp DB_File.pm blib/lib/DB_File.pm
Running Mkbootstrap for DB_File ()
chmod 644 "DB_File.bs"
"/usr/bin/perl" -MExtUtils::Command::MM -e 'cp_nonempty' -- DB_File.bs blib/arch/auto/DB_File/DB_File.bs 644
x86_64-linux-gnu-gcc -c  -I/usr/local/BerkeleyDB/include -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g   -DVERSION=\"1.856\" -DXS_VERSION=\"1.856\" -fPIC "-I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE"  -D_NOT_CORE  -DmDB_Prefix_t=size_t -DmDB_Hash_t=u_int32_t   version.c
version.c:30:10: fatal error: db.h: No such file or directory
   30 | #include <db.h>
      |          ^~~~~~
compilation terminated.
make: *** [Makefile:355: version.o] Error 1
  PMQS/DB_File-1.856.tar.gz
  /usr/bin/make -- NOT OK
Failed during this command:
 PMQS/DB_File-1.856.tar.gz                    : make NO

cpan[8]> 

```

Error ကို ဖြေရှင်းဖို့အတွက် Googling လုပ်ကြည့်တော့  
[https://www.howtoforge.com/community/threads/cpan-install-db_file-make-error.1050/](https://www.howtoforge.com/community/threads/cpan-install-db_file-make-error.1050/)  
[https://www.howtoforge.com/community/threads/fc3-perfect-installation-make-errors.699/](https://www.howtoforge.com/community/threads/fc3-perfect-installation-make-errors.699/)  

apt-get နဲ့ install လုပ်ကြည့်တော့ အောက်ပါလိုမျိုး error ပေးတယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ apt-cache search DB_File
libcdb-file-perl - module to access cdb databases from Perl
libdb-file-lock-perl - wrapper adding locking for the DB_File module
libmldbm-perl - module for storing multidimensional hash structures in perl tied hashes
libtie-persistent-perl - tied interface to persistent file
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ apt-get install DB_File
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ sudo apt-get install DB_File
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package DB_File
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$
```

apt ကို update လုပ်ပြီး install လုပ်လည်း မရဘူး...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ sudo apt-get update
Hit:1 http://dl.google.com/linux/chrome/deb stable InRelease
Hit:2 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                                                   
Ign:3 http://ppa.launchpad.net/atareao/updf/ubuntu groovy InRelease                                                                                    
Hit:4 http://security.ubuntu.com/ubuntu groovy-security InRelease                                                                           
Hit:5 http://mm.archive.ubuntu.com/ubuntu groovy InRelease                   
Hit:6 http://ppa.launchpad.net/sylvain-pineau/kazam/ubuntu groovy InRelease
Hit:7 http://mm.archive.ubuntu.com/ubuntu groovy-updates InRelease       
Ign:8 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy InRelease
Hit:9 http://mm.archive.ubuntu.com/ubuntu groovy-backports InRelease     
Err:10 http://ppa.launchpad.net/atareao/updf/ubuntu groovy Release       
  404  Not Found [IP: 91.189.95.85 80]
Err:11 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release
  404  Not Found [IP: 91.189.95.85 80]
Reading package lists... Done
E: The repository 'http://ppa.launchpad.net/atareao/updf/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ sudo apt-get install DB_File
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package DB_File
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$
```

Googling ထပ်လုပ်ကြည့်တော့ အောက်ပါ link ကို တွေ့ခဲ့...  
[https://stackoverflow.com/questions/57697992/perl-cpanm-cannot-install-db-file](https://stackoverflow.com/questions/57697992/perl-cpanm-cannot-install-db-file)  

အထက်က link က ပြောထားတာက "libdb-dev" or "libdb-devel" လိုအပ်တယ်လို့...  
အဲဒါကြောင့် အောက်ပါ command နဲ့ libdb-dev ကို install လုပ်ခဲ့တယ်။  

```
$ sudo apt-get install libdb-dev
```

ပြီးမှ cpan installation shell ထဲကို ဝင်ပြီး DB_File ကို install လုပ်ဖို့ ကြိုးစားတာ ဒီတစ်ခါတော့ အဆင်ပြေပြေနဲ့ install လုပ်နိုင်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ cpan
Terminal does not support AddHistory.

To fix that, maybe try>  install Term::ReadLine::Perl

cpan[1]> install DB_File 
Reading '/home/ye/.cpan/Metadata'
  Database was generated on Wed, 08 Dec 2021 01:29:02 GMT
Running install for module 'DB_File'
Checksum for /home/ye/.cpan/sources/authors/id/P/PM/PMQS/DB_File-1.856.tar.gz ok
Scanning cache /home/ye/.cpan/build for sizes
............................................................................DONE
'YAML' not installed, will not store persistent state
Configuring P/PM/PMQS/DB_File-1.856.tar.gz with Makefile.PL
Parsing config.in...
Looks Good.
Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for DB_File
Writing MYMETA.yml and MYMETA.json
  PMQS/DB_File-1.856.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for P/PM/PMQS/DB_File-1.856.tar.gz
cp DB_File.pm blib/lib/DB_File.pm
Running Mkbootstrap for DB_File ()
chmod 644 "DB_File.bs"
"/usr/bin/perl" -MExtUtils::Command::MM -e 'cp_nonempty' -- DB_File.bs blib/arch/auto/DB_File/DB_File.bs 644
x86_64-linux-gnu-gcc -c  -I/usr/local/BerkeleyDB/include -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g   -DVERSION=\"1.856\" -DXS_VERSION=\"1.856\" -fPIC "-I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE"  -D_NOT_CORE  -DmDB_Prefix_t=size_t -DmDB_Hash_t=u_int32_t   version.c
"/usr/bin/perl" "/usr/share/perl/5.30/ExtUtils/xsubpp" -noprototypes -typemap '/usr/share/perl/5.30/ExtUtils/typemap' -typemap '/home/ye/.cpan/build/DB_File-1.856-2/typemap'  DB_File.xs > DB_File.xsc
mv DB_File.xsc DB_File.c
x86_64-linux-gnu-gcc -c  -I/usr/local/BerkeleyDB/include -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g   -DVERSION=\"1.856\" -DXS_VERSION=\"1.856\" -fPIC "-I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE"  -D_NOT_CORE  -DmDB_Prefix_t=size_t -DmDB_Hash_t=u_int32_t   DB_File.c
rm -f blib/arch/auto/DB_File/DB_File.so
LD_RUN_PATH="/lib/x86_64-linux-gnu" x86_64-linux-gnu-gcc  -shared -L/usr/local/lib -fstack-protector-strong  version.o DB_File.o  -o blib/arch/auto/DB_File/DB_File.so  \
   -ldb   \
  
chmod 755 blib/arch/auto/DB_File/DB_File.so
Manifying 1 pod document
  PMQS/DB_File-1.856.tar.gz
  /usr/bin/make -- OK
Running make test for PMQS/DB_File-1.856.tar.gz
"/usr/bin/perl" -MExtUtils::Command::MM -e 'cp_nonempty' -- DB_File.bs blib/arch/auto/DB_File/DB_File.bs 644
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/000prereq.t ... 1/2 # 
# 
# DB_File version            1.856
# DB_File::db_version        5.3
# DB_File::db_ver            5.003028
# 
t/000prereq.t ... ok   
t/db-btree.t .... ok       
t/db-hash.t ..... ok       
t/db-recno.t .... ok       
t/db-threads.t .. ok   
t/meta-json.t ... ok   
t/meta-yaml.t ... ok   
t/pod.t ......... ok   
All tests successful.
Files=8, Tests=581,  1 wallclock secs ( 0.06 usr  0.00 sys +  0.53 cusr  0.13 csys =  0.72 CPU)
Result: PASS
Terminal does not support GetHistory.
Lockfile removed.
  PMQS/DB_File-1.856.tar.gz
  /usr/bin/make test -- OK
Running make install for PMQS/DB_File-1.856.tar.gz
"/usr/bin/perl" -MExtUtils::Command::MM -e 'cp_nonempty' -- DB_File.bs blib/arch/auto/DB_File/DB_File.bs 644
Manifying 1 pod document
Files found in blib/arch: installing files in blib/lib into architecture dependent library tree
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/auto/DB_File/DB_File.so
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/DB_File.pm
Installing /usr/local/man/man3/DB_File.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  PMQS/DB_File-1.856.tar.gz
  sudo /usr/bin/make install  -- OK

cpan[2]> 

```

နောက် ကျန်နေသေးတဲ့ perl module တွေကို ဆက် install လုပ်ခဲ့တယ်...  

install Parse::Yapp
install DBI
install DBD::SQLite
install Time::HiRes
install Term::ReadLine
install URI::Escape
install Lingua::Identify
install Test::Pod
install Test::Pod::Coverage
install ExtUtils::MakeMaker
install Text::NSP
install IO::Compress::Bzip2
install IO::Compress::Xz
install List::MoreUtils

တချို့ ကိုယ့်စက်ထဲမှာ install လုပ်ထားပြီးသား module ကလည်း up to date ဖြစ်ထားပြီးသားဆိုရင်တော့ install ပဲ အောက်ပါလိုမျိုး message ပဲ ပြန်ပေးပါလိမ့်မယ်။  

```
cpan[9]> install Test::Pod
Test::Pod is up to date (1.52).
```

အထက်မှာ ပြောခဲ့တဲ့ perl module အကုန် install လုပ်ပြီးသွားပြီ။ ပြီးတော့ .tar.gz ဖိုင်ကိုလည်း ကိုယ့် path ထဲမှာ ဖြေထားပြီးသားဆိုတော့ configure လုပ်ဖို့ပဲ ကျန်တော့တယ်။  
အရင်ဆုံး unzip or ဖြေထားပြီးသား ဖိုလ်ဒါအောက်ထဲ ဝင်မယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools$ cd NATools-0.5.10/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$
```

ပြီးတော့ ./configure လုပ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$ ./configure

Checking basic configuration...

checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking for style of include used by make... GNU
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking dependency style of gcc... gcc3
checking for library containing strerror... none required
checking for gcc... (cached) gcc
checking whether we are using the GNU C compiler... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking for gcc option to accept ISO C89... (cached) none needed
checking dependency style of gcc... (cached) gcc3
checking whether gcc and cc understand -c and -o together... yes
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking how to print strings... printf
checking for a sed that does not truncate output... /usr/bin/sed
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... no, using cp -p
checking the maximum length of command line arguments... 1572864
checking whether the shell understands some XSI constructs... yes
checking whether the shell understands "+="... yes
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for ar... ar
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
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
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... yes

Checking for math functions...

checking for log10 in -lm... yes
checking for log in -lm... yes
checking for exp in -lm... yes
checking for sqrt in -lm... yes

Checking for zlib...

checking for gzopen in -lz... yes
checking for gzread in -lz... yes
checking for gzwrite in -lz... yes
checking for gzclose in -lz... yes

Checking for glib 2.0, SQLite and Berkeley DB...

checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for GLIB... yes
checking for SQLITE... no
configure: error: Package requirements (sqlite3 >= 3.5.0) were not met:

No package 'sqlite3' found

Consider adjusting the PKG_CONFIG_PATH environment variable if you
installed software in a non-standard prefix.

Alternatively, you may set the environment variables SQLITE_CFLAGS
and SQLITE_LIBS to avoid the need to call pkg-config.
See the pkg-config man page for more details.
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$
```

sqlite3 ကို မတွေ့ဘူးလို့ ပြောနေတယ်...  
ဒါပေမဲ့ ပြဿနာက sqlite က မရှိတာမဟုတ်ဘူး version မြင့်နေတဲ့ ပြဿနာလို့ ပြောနေတာမို့... backward compatibility ရှိရင်တော့ ပြဿနာ မရှိလောက်ဘူးလို့ ယူဆ...  

sqlite3 package တွေကို ဒေါင်းလုဒ်လုပ်ရတဲ့ site ရဲ့ address က အောက်ပါအတိုင်း...  
[https://www.sqlite.org/download.html](https://www.sqlite.org/download.html)  

sqlite3 version 337 ကို souce code ကနေ install လုပ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/tool$ mv ~/Downloads/sqlite-autoconf-3370000.tar.gz .
(base) ye@:/media/ye/project2/tool$ tar -xf ./sqlite-autoconf-3370000.tar.gz 
(base) ye@:/media/ye/project2/tool$ cd sqlite-autoconf-3370000/
(base) ye@:/media/ye/project2/tool/sqlite-autoconf-3370000$ ls
aclocal.m4    config.sub    depcomp     ltmain.sh          Makefile.in   README.txt  sqlite3.1     sqlite3.h      sqlite3rc.h
compile       configure     INSTALL     Makefile.am        Makefile.msc  Replace.cs  sqlite3.c     sqlite3.pc.in  tea
config.guess  configure.ac  install-sh  Makefile.fallback  missing       shell.c     sqlite3ext.h  sqlite3.rc
(base) ye@:/media/ye/project2/tool/sqlite-autoconf-3370000$
```

```
./configure
make
sudo make install
```

installation ကတော့ အဆင်ပြေတယ်။  

```
(base) ye@:/media/ye/project2/tool/sqlite-autoconf-3370000$ sqlite3 --version
3.31.1 2020-01-27 19:55:54 3bfa9cc97da10598521b342961df8f5f68c7388fa117345eeb516eaa837bb4d6
(base) ye@:/media/ye/project2/tool/sqlite-autoconf-3370000$ 
```

version လည်း 3.31.1 ဆိုတော့ အခု စမ်းချင်တဲ့ perl module တွေနဲ့ အဆင်ပြေမလားလို့...  
NATools ကို ဆက် install လုပ်ခဲ့...  
./configure ကို run တာ အောက်ပါအတိုင်း...  ဒီတစ်ခါတော့ OK သွားပြီ...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$ ./configure

Checking basic configuration...

checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking for style of include used by make... GNU
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking dependency style of gcc... gcc3
checking for library containing strerror... none required
checking for gcc... (cached) gcc
checking whether we are using the GNU C compiler... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking for gcc option to accept ISO C89... (cached) none needed
checking dependency style of gcc... (cached) gcc3
checking whether gcc and cc understand -c and -o together... yes
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking how to print strings... printf
checking for a sed that does not truncate output... /usr/bin/sed
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... no, using cp -p
checking the maximum length of command line arguments... 1572864
checking whether the shell understands some XSI constructs... yes
checking whether the shell understands "+="... yes
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for ar... ar
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
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
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... yes

Checking for math functions...

checking for log10 in -lm... yes
checking for log in -lm... yes
checking for exp in -lm... yes
checking for sqrt in -lm... yes

Checking for zlib...

checking for gzopen in -lz... yes
checking for gzread in -lz... yes
checking for gzwrite in -lz... yes
checking for gzclose in -lz... yes

Checking for glib 2.0, SQLite and Berkeley DB...

checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for GLIB... yes
checking for SQLITE... yes
checking for sqlite3... sqlite3
checking for Berkeley DB >= 4.3... yes
  - Berkeley BD header file: db.h
  - Berkeley BD library flags: -ldb
  - Berkeley BD installation prefix: /usr/local

Checking for Perl and modules...

checking for perl... perl
checking for pod2man... pod2man

Writing Perl specific files...

configure: creating ./config.status
config.status: creating NAT/scripts/nat-sentence-align
config.status: creating NAT/NAT.pm
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands

Checking required Perl modules versions...

checking Perl module Lingua::PT::PLNbase >= 0.17... ok (0.27)
checking Perl module IO::Socket >= 1.28... ok (1.45)
checking Perl module XML::TMX >= 0.16... ok (0.36)
checking Perl module XML::DT >= 0.44... ok (0.69)
checking Perl module Compress::Zlib >= 1.16... ok (2.102)
checking Perl module Test::Harness >= 2.26... ok (3.42)
checking Perl module Storable >= 2.04... ok (3.25)
checking Perl module MLDBM >= 2.00... ok (2.05)
checking Perl module Fcntl >= 1.03... ok (1.13)
checking Perl module POSIX >= 0... ok (1.88)
checking Perl module DB_File >= 1.804... ok (1.856)
checking Perl module Parse::Yapp::Driver >= 1.05... ok (1.21)
checking Perl module DBI >= 0... ok (1.643)
checking Perl module DBD::SQLite >= 1.30... ok (1.70)
checking Perl module File::Path >= 1.06... ok (2.18)
checking Perl module File::Spec >= 0.86... ok (3.78)
checking Perl module File::Copy >= 2.06... ok (2.34)
checking Perl module IPC::Open2 >= 1.01... ok (1.04)
checking Perl module Time::HiRes >= 1.2... ok (1.9764)
checking Perl module Term::ReadLine >= 1.01... ok (1.17)
checking Perl module URI::Escape >= 3.26... ok (5.10)
checking Perl module Lingua::Identify >= 0.17... ok (0.56)
checking Perl module Test::Pod >= 1.20... ok (1.52)
checking Perl module Test::Pod::Coverage >= 1.06... ok (1.10)
checking Perl module ExtUtils::Manifest >= 0... ok (1.73)
checking Perl module ExtUtils::MakeMaker >= 6.31... ok (7.62)
checking Perl module Memoize >= 0... ok (1.03_01)
checking Perl module Text::NSP >= 1.09... ok (1.31)
checking Perl module IO::Uncompress::Bunzip2 >= 2.027... ok (2.102)
checking Perl module IO::Compress::Bzip2 >= 2.027... ok (2.102)
checking Perl module IO::Uncompress::UnXz >= 2.030... ok (2.101)
checking Perl module IO::Compress::Xz >= 2.030... ok (2.101)
checking Perl module List::MoreUtils >= 0... ok (0.430)

Running Perl module Makefile.PL...

Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile.in
Writing Makefile.in for NAT
Writing MYMETA.yml and MYMETA.json

Writing makefiles...

configure: creating ./config.status
config.status: creating NAT/scripts/nat-sentence-align
config.status: creating NAT/NAT.pm
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/server/Makefile
config.status: creating pods/Makefile
config.status: creating data/Makefile
config.status: creating 3rdParty/Makefile
config.status: creating NAT/Makefile
config.status: creating t/Makefile
config.status: creating t/input/Makefile
config.status: creating config.h
config.status: config.h is unchanged
config.status: executing depfiles commands
config.status: executing libtool commands

-----------------------------------------------------------------------------
LIBS:  -lm -lz -lglib-2.0 -L/usr/local/lib -lsqlite3 -L/usr/local/lib// -ldb
CFLAGS: -g -O2 -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include -I/usr/local/include -I/usr/local/include
-----------------------------------------------------------------------------

Run 'make' to start compiling.

(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$ 
```

make command ကို run ခဲ့တယ်...  
C program တွေကို compile လုပ်ရတာခက်တဲ့ ထုံးစံအတိုင်း Error နှစ်ခုတွေ့တယ်လို့ အောက်ပါအတိုင်းပြောနေတယ်...  

```
$make
...
...
...
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-pair2tmx
cp scripts/nat-ptd blib/script/nat-ptd
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-ptd
cp scripts/nat-rank blib/script/nat-rank
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-rank
cp scripts/nat-sentence-align blib/script/nat-sentence-align
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-sentence-align
cp scripts/nat-shell blib/script/nat-shell
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-shell
cp scripts/nat-substDict blib/script/nat-substDict
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-substDict
cp scripts/nat-tmx2pair blib/script/nat-tmx2pair
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-tmx2pair
cp scripts/nat-translate-shell blib/script/nat-translate-shell
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-translate-shell
Manifying 21 pod documents
Manifying 16 pod documents
Can't write-open blib/man3/NAT::CGI.3pm: Invalid argument at /usr/local/share/perl/5.30.3/ExtUtils/Command/MM.pm line 153.
make[2]: *** [Makefile:584: manifypods] Error 22
make[2]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT'
make[1]: *** [Makefile:336: all-recursive] Error 1
make[1]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10'
make: *** [Makefile:259: all] Error 2
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$ make
```

Error နှစ်ခုကို ခဏမေ့ထားပြီး sudo make install လုပ်ခဲ့တော့ error ပေးတယ်...  

```
$sudo make install
...
...
...
Making install in t
make[1]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
Making install in input
make[2]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t/input'
make[3]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t/input'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t/input'
make[2]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t/input'
make[2]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
make[3]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
make[2]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
make[1]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/t'
Making install in NAT
make[1]: Entering directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT'
"/usr/bin/perl" -MExtUtils::Command::MM -e 'cp_nonempty' -- NAT.bs blib/arch/auto/NAT/NAT.bs 644
Manifying 21 pod documents
Manifying 16 pod documents
Can't write-open blib/man3/NAT::CGI.3pm: Invalid argument at /usr/local/share/perl/5.30.3/ExtUtils/Command/MM.pm line 153.
make[1]: *** [Makefile:584: manifypods] Error 22
make[1]: Leaving directory '/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT'
make: *** [Makefile:336: install-recursive] Error 1
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$
```

အဆင်မပြေဘူးကွာ...  

## Try NATools Updated Version of Perl Module

မထင်မှတ်ပဲနဲ့ perl module "Lingua::NATools" အနေနဲ့ updated version ကို ရှာလို့တွေ့တယ်။  
link က အောက်ပါအတိုင်း  
[https://metacpan.org/pod/Lingua::NATools](https://metacpan.org/pod/Lingua::NATools)  

**အဆင်ပြေရင်တော့ အထက်က အဆင်တွေကို ကျော်ပလိုက်လို့ ရတယ်**  
အောက်ပါအတိုင်း install လုပ်ခဲ့တယ်။ အဆင်ပြေပုံရတယ်!!!! :)  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10$ cpan
Terminal does not support AddHistory.

To fix that, maybe try>  install Term::ReadLine::Perl

cpan[1]> install Lingua::NATools                             
Reading '/home/ye/.cpan/Metadata'
  Database was generated on Wed, 08 Dec 2021 01:29:02 GMT
Running install for module 'Lingua::NATools'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz ok
Scanning cache /home/ye/.cpan/build for sizes
............................................................................DONE
'YAML' not installed, will not store persistent state
---- Unsatisfied dependencies detected during ----
----    AMBS/Lingua-NATools-v0.7.12.tar.gz    ----
    Config::AutoConf [build_requires]
    ExtUtils::LibBuilder [build_requires]
Running install for module 'Config::AutoConf'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/Config-AutoConf-0.320.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Config-AutoConf-0.320.tar.gz ok
Configuring A/AM/AMBS/Config-AutoConf-0.320.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for Config::AutoConf
Writing MYMETA.yml and MYMETA.json
  AMBS/Config-AutoConf-0.320.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for A/AM/AMBS/Config-AutoConf-0.320.tar.gz
cp lib/Config/AutoConf.pm blib/lib/Config/AutoConf.pm
Manifying 1 pod document
  AMBS/Config-AutoConf-0.320.tar.gz
  /usr/bin/make -- OK
Running make test for AMBS/Config-AutoConf-0.320.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t xt/*.t
t/00.load.t ....... ok   
t/01.checkprog.t .. 1/18 # Check for some progs to get an overview about world outside
# Found AWK as /usr/bin/gawk
# Found SED as /usr/bin/sed
# Found EGREP as /usr/bin/egrep
# Found PKG-CONFIG as /usr/bin/pkg-config
t/01.checkprog.t .. ok     
t/02.compile.t .... ok    
t/03.link.t ....... ok    
All tests successful.

Test Summary Report
-------------------
t/02.compile.t  (Wstat: 0 Tests: 31 Failed: 0)
  TODO passed:   28-30
t/03.link.t     (Wstat: 0 Tests: 18 Failed: 0)
  TODO passed:   11, 16, 18
Files=4, Tests=68, 19 wallclock secs ( 0.04 usr  0.00 sys + 16.52 cusr  3.20 csys = 19.76 CPU)
Result: PASS
Terminal does not support GetHistory.
Lockfile removed.
  AMBS/Config-AutoConf-0.320.tar.gz
  /usr/bin/make test -- OK
Running make install for AMBS/Config-AutoConf-0.320.tar.gz
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/Config/AutoConf.pm
Installing /usr/local/man/man3/Config::AutoConf.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  AMBS/Config-AutoConf-0.320.tar.gz
  sudo /usr/bin/make install  -- OK
Running install for module 'ExtUtils::LibBuilder'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/ExtUtils-LibBuilder-0.08.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/ExtUtils-LibBuilder-0.08.tar.gz ok
Configuring A/AM/AMBS/ExtUtils-LibBuilder-0.08.tar.gz with Build.PL
Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'ExtUtils-LibBuilder' version '0.08'
  AMBS/ExtUtils-LibBuilder-0.08.tar.gz
  /usr/bin/perl Build.PL -- OK
Running Build for A/AM/AMBS/ExtUtils-LibBuilder-0.08.tar.gz
Building ExtUtils-LibBuilder
  AMBS/ExtUtils-LibBuilder-0.08.tar.gz
  ./Build -- OK
Running Build test for AMBS/ExtUtils-LibBuilder-0.08.tar.gz
t/00-load.t ....... 1/1 # Testing ExtUtils::LibBuilder 0.08, Perl 5.030003, /usr/bin/perl
t/00-load.t ....... ok   
t/01-simple.t ..... ok   
t/pod-coverage.t .. ok   
t/pod.t ........... ok   
All tests successful.
Files=4, Tests=10,  1 wallclock secs ( 0.01 usr  0.00 sys +  0.26 cusr  0.08 csys =  0.35 CPU)
Result: PASS
  AMBS/ExtUtils-LibBuilder-0.08.tar.gz
  ./Build test -- OK
Running Build install for AMBS/ExtUtils-LibBuilder-0.08.tar.gz
Building ExtUtils-LibBuilder
Installing /usr/local/share/perl/5.30.3/ExtUtils/LibBuilder.pm
Installing /usr/local/man/man3/ExtUtils::LibBuilder.3pm
  AMBS/ExtUtils-LibBuilder-0.08.tar.gz
  sudo ./Build install  -- OK
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-NATools-v0.7.12-0
Configuring A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz with Build.PL
Checking prerequisites...
  requires:
    !  Lingua::PTD is not installed

ERRORS/WARNINGS FOUND IN PREREQUISITES.  You may wish to install the versions
of the modules indicated above before proceeding with this installation

Checking NATools version... 0.7.12
Checking for stdlib.h... Checking for cc... x86_64-linux-gnu-gcc
yes
Checking for stdarg.h... yes
Checking for string.h... yes
Checking for float.h... yes
Checking for assert.h... yes
Checking for ctype.h... yes
Checking for errno.h... yes
Checking for limits.h... yes
Checking for locale.h... yes
Checking for math.h... yes
Checking for setjmp.h... yes
Checking for signal.h... yes
Checking for stddef.h... yes
Checking for stdio.h... yes
Checking for time.h... yes
Checking for library containing log2... m
Checking for library containing pow... none required
Checking for library containing log10... none required
Checking for library containing log... none required
Checking for library containing exp... none required
Checking for library containing sqrt... none required
Checking for gzopen in -lz... yes
Checking for gzread in -lz... yes
Checking for gzwrite in -lz... yes
Checking for gzclose in -lz... yes
Checking for glib-2.0 >= 2.8... yes
Checking for sqlite3 >= 3.5.0... yes
Checking for sqlite3 binary... yes
Checking for Berkeley DB header >= 4.3.0... yes
Checking for Berkeley DB library >= 4.3.0... yes
configure: LIBS:  -lm -lz -lglib-2.0 -L/usr/local/lib -lsqlite3 -ldb
configure: CFLAGS:   -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include -I/usr/local/include
Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'Lingua-NATools' version 'v0.7.12'
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  /usr/bin/perl Build.PL -- OK
Running Build for A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz
---- Unsatisfied dependencies detected during ----
----    AMBS/Lingua-NATools-v0.7.12.tar.gz    ----
    Lingua::PTD [requires]
Running install for module 'Lingua::PTD'
Fetching with LWP:
http://www.cpan.org/authors/id/A/AM/AMBS/Lingua-PTD-1.16.tar.gz
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-PTD-1.16.tar.gz ok
Configuring A/AM/AMBS/Lingua-PTD-1.16.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Warning: prerequisite Term::ReadLine::Gnu 0 not found.
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for Lingua::PTD
Writing MYMETA.yml and MYMETA.json
  AMBS/Lingua-PTD-1.16.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for A/AM/AMBS/Lingua-PTD-1.16.tar.gz
---- Unsatisfied dependencies detected during ----
----        AMBS/Lingua-PTD-1.16.tar.gz       ----
    Term::ReadLine::Gnu [requires]
Running install for module 'Term::ReadLine::Gnu'
Fetching with LWP:
http://www.cpan.org/authors/id/H/HA/HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/H/HA/HAYASHI/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/H/HA/HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz ok
Configuring H/HA/HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz with Makefile.PL
Warning (mostly harmless): No library found for -ltermcap
rlver.c:3:10: fatal error: readline/readline.h: No such file or directory
    3 | #include <readline/readline.h>
      |          ^~~~~~~~~~~~~~~~~~~~~
compilation terminated.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Could not compile rlver.c.

system(): No such file or directory

If you have installed the GNU Readline Library (libreadline.{a,so} and
readline/readline.h, etc.) on directories for which your perl is not
configured to search (refer the value of `ccflags' and `libpath' in
the output of `perl -V'), specify the paths as follows;

        perl Makefile.PL --includedir=/yourdir/include --libdir=/yourdir/lib
or
        perl Makefile.PL --prefix=/yourdir

Note that the GNU Readline Library version 2.0 and earlier causes error
here.  Update it to version 2.1 and/or later.

Read INSTALL for more details.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Warning: No success on command[/usr/bin/perl Makefile.PL]
  HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz
  /usr/bin/perl Makefile.PL -- NOT OK
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-PTD-1.16-0
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been prepared
Running make for A/AM/AMBS/Lingua-PTD-1.16.tar.gz
Warning: Prerequisite 'Term::ReadLine::Gnu => 0' for 'AMBS/Lingua-PTD-1.16.tar.gz' failed when processing 'HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz' with 'writemakefile => NO '/usr/bin/perl Makefile.PL' returned status 256'. Continuing, but chances to succeed are limited.
cp lib/Lingua/PTD/SQLite.pm blib/lib/Lingua/PTD/SQLite.pm
cp lib/Lingua/PTD/XzDmp.pm blib/lib/Lingua/PTD/XzDmp.pm
cp lib/Lingua/PTD/TSV.pm blib/lib/Lingua/PTD/TSV.pm
cp lib/Lingua/PTD/StarDict.pm blib/lib/Lingua/PTD/StarDict.pm
cp lib/Lingua/PTD/Dumper.pm blib/lib/Lingua/PTD/Dumper.pm
cp lib/Lingua/PTD/BzDmp.pm blib/lib/Lingua/PTD/BzDmp.pm
cp lib/Lingua/PTD.pm blib/lib/Lingua/PTD.pm
cp bin/nat-ptd blib/script/nat-ptd
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-ptd
Manifying 1 pod document
Manifying 7 pod documents
  AMBS/Lingua-PTD-1.16.tar.gz
  /usr/bin/make -- OK
Running make test for AMBS/Lingua-PTD-1.16.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00-load.t .. 1/? # Testing Lingua::PTD 1.16, Perl 5.030003, /usr/bin/perl
t/00-load.t .. ok   
t/02_ptd.t ... ok       
All tests successful.
Files=2, Tests=183,  0 wallclock secs ( 0.02 usr  0.00 sys +  0.14 cusr  0.04 csys =  0.20 CPU)
Result: PASS
  AMBS/Lingua-PTD-1.16.tar.gz
Tests succeeded but one dependency not OK (Term::ReadLine::Gnu)
  AMBS/Lingua-PTD-1.16.tar.gz
  [dependencies] -- NA
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-NATools-v0.7.12-0
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  Has already been prepared
Running Build for A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz
Warning: Prerequisite 'Lingua::PTD => 1.00' for 'AMBS/Lingua-NATools-v0.7.12.tar.gz' failed when processing 'AMBS/Lingua-PTD-1.16.tar.gz' with 'make_test => NO one dependency not OK (Term::ReadLine::Gnu)'. Continuing, but chances to succeed are limited.
Building Lingua-NATools
  [pod2man] pods/nat-css.pod
  [pod2man] pods/nat-initmat.pod
  [pod2man] pods/nat-ipfp.pod
  [pod2man] pods/nat-mat2dic.pod
  [pod2man] pods/nat-postbin.pod
  [pod2man] pods/nat-pre.pod
  [pod2man] pods/nat-samplea.pod
  [pod2man] pods/nat-sampleb.pod
  [pod2man] pods/nat-sentalign.pod
  [cc] src/ngrams_bdb.c
  [cc] src/words.c
  [cc] src/server.c
  [cc] src/unicode.c
  [cc] src/ipfp.c
  [cc] src/sent_align.c
  [cc] src/standard.c
  [cc] src/grep.c
  [cc] src/parseini.c
  [cc] src/bucket.c
  [cc] src/ntdump.c
  [cc] src/natdict.c
  [cc] src/invindex.c
  [cc] src/tempdict.c
  [cc] src/ngramidx.c
  [cc] src/matrix.c
  [cc] src/search_sentence.c
  [cc] src/initmat.c
  [cc] src/dictionary.c
  [cc] src/words2id.c
  [cc] src/partials.c
  [cc] src/corpusinfo.c
  [cc] src/sampleb.c
  [cc] src/postbin.c
  [cc] src/srvshared.c
  [cc] src/corpus.c
  [cc] src/adddic.c
  [cc] src/mat2dic.c
  [cc] src/mkdict.c
  [cc] src/pre.c
  [cc] src/invindexjoin.c
  [cc] src/natlexicon.c
  [cc] src/samplea.c
  [ld] building libnatools.so
  [ld] nat-ntd-add
  [ld] nat-postbin
  [ld] nat-server
  [ld] nat-grep
  [ld] nat-mat2dic
  [ld] nat-mergeidx
  [ld] nat-ngrams
  [ld] nat-sentalign
  [ld] nat-css
  [ld] nat-pre
  [ld] nat-ntd-dump
  [ld] nat-mkntd
  [ld] nat-samplea
  [ld] nat-words2id
  [ld] nat-initmat
  [ld] nat-ipfp
  [ld] nat-sampleb
  [XS] natools.xs
  [CC] natools.c
  [LD] NATools.so
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  ./Build -- OK
Running Build test for AMBS/Lingua-NATools-v0.7.12.tar.gz
t/bin/corpus.t ............... ok   
t/bin/nat-pre.t .............. ok      
t/bin/nat-these.t ............ Warning: some of these tests can take about 1 minute on slow machines
t/bin/nat-these.t ............ ok      
t/bin/words.t ................ ok   
t/pm/00_basic.t .............. ok     
t/pm/01_config.t ............. ok     
t/pm/03.1_create_from_tmx.t .. 7/? # Let the server start...
t/pm/03.1_create_from_tmx.t .. ok     
t/pm/10_pcorpus.t ............ ok   
t/pm/11_corpus.t ............. ok   
t/pm/14_scripts.t ............ ok       
t/pm/15_cgis.t ............... ok   
t/pm/16_pods.t ............... skipped: export AUTHOR_TEST for author tests
t/pm/17_pod_coverage.t ....... skipped: export AUTHOR_TEST for author tests
t/pm/20_patterns.t ........... 1/26 Parsing rules file: [t/pm/20_patterns.in]
t/pm/20_patterns.t ........... ok     
All tests successful.
Files=14, Tests=8840, 10 wallclock secs ( 0.27 usr  0.04 sys +  5.80 cusr  0.68 csys =  6.79 CPU)
Result: PASS
  AMBS/Lingua-NATools-v0.7.12.tar.gz
Tests succeeded but one dependency not OK (Lingua::PTD)
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  [dependencies] -- NA
Failed during this command:
 HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz        : writemakefile NO '/usr/bin/perl Makefile.PL' returned status 256
 AMBS/Lingua-PTD-1.16.tar.gz                  : make_test NO one dependency not OK (Term::ReadLine::Gnu)
 AMBS/Lingua-NATools-v0.7.12.tar.gz           : make_test NO one dependency not OK (Lingua::PTD)

cpan[2]> 

```

အထက်ပါအတိုင်း module နှစ်ခုက install လုပ်ဖို့ လိုနေသေးကြောင်းပြောနေလို့ အဲဒီ ပြောနေတဲ့ module နှစ်ခုကို အရင် install လုပ်လိုက်တယ်။  
Term::ReadLine::Perl ကို အောက်ပါအတိုင်း install လုပ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$ cpan
Terminal does not support AddHistory.

To fix that, maybe try>  install Term::ReadLine::Perl

cpan[1]> install Lingua::PTD
Reading '/home/ye/.cpan/Metadata'
  Database was generated on Wed, 08 Dec 2021 01:29:02 GMT
Running install for module 'Lingua::PTD'
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-PTD-1.16.tar.gz ok
Scanning cache /home/ye/.cpan/build for sizes
............................................................................DONE
'YAML' not installed, will not store persistent state
Configuring A/AM/AMBS/Lingua-PTD-1.16.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Warning: prerequisite Term::ReadLine::Gnu 0 not found.
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for Lingua::PTD
Writing MYMETA.yml and MYMETA.json
  AMBS/Lingua-PTD-1.16.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for A/AM/AMBS/Lingua-PTD-1.16.tar.gz
---- Unsatisfied dependencies detected during ----
----        AMBS/Lingua-PTD-1.16.tar.gz       ----
    Term::ReadLine::Gnu [requires]
Running install for module 'Term::ReadLine::Gnu'
Checksum for /home/ye/.cpan/sources/authors/id/H/HA/HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz ok
Configuring H/HA/HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz with Makefile.PL
Warning (mostly harmless): No library found for -ltermcap
rlver.c:3:10: fatal error: readline/readline.h: No such file or directory
    3 | #include <readline/readline.h>
      |          ^~~~~~~~~~~~~~~~~~~~~
compilation terminated.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Could not compile rlver.c.

system(): No such file or directory

If you have installed the GNU Readline Library (libreadline.{a,so} and
readline/readline.h, etc.) on directories for which your perl is not
configured to search (refer the value of `ccflags' and `libpath' in
the output of `perl -V'), specify the paths as follows;

        perl Makefile.PL --includedir=/yourdir/include --libdir=/yourdir/lib
or
        perl Makefile.PL --prefix=/yourdir

Note that the GNU Readline Library version 2.0 and earlier causes error
here.  Update it to version 2.1 and/or later.

Read INSTALL for more details.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Warning: No success on command[/usr/bin/perl Makefile.PL]
  HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz
  /usr/bin/perl Makefile.PL -- NOT OK
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-PTD-1.16-1
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been prepared
Running make for A/AM/AMBS/Lingua-PTD-1.16.tar.gz
Warning: Prerequisite 'Term::ReadLine::Gnu => 0' for 'AMBS/Lingua-PTD-1.16.tar.gz' failed when processing 'HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz' with 'writemakefile => NO '/usr/bin/perl Makefile.PL' returned status 256'. Continuing, but chances to succeed are limited.
cp lib/Lingua/PTD/Dumper.pm blib/lib/Lingua/PTD/Dumper.pm
cp lib/Lingua/PTD/SQLite.pm blib/lib/Lingua/PTD/SQLite.pm
cp lib/Lingua/PTD/BzDmp.pm blib/lib/Lingua/PTD/BzDmp.pm
cp lib/Lingua/PTD/TSV.pm blib/lib/Lingua/PTD/TSV.pm
cp lib/Lingua/PTD/StarDict.pm blib/lib/Lingua/PTD/StarDict.pm
cp lib/Lingua/PTD.pm blib/lib/Lingua/PTD.pm
cp lib/Lingua/PTD/XzDmp.pm blib/lib/Lingua/PTD/XzDmp.pm
cp bin/nat-ptd blib/script/nat-ptd
"/usr/bin/perl" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/nat-ptd
Manifying 1 pod document
Manifying 7 pod documents
  AMBS/Lingua-PTD-1.16.tar.gz
  /usr/bin/make -- OK
Running make test for AMBS/Lingua-PTD-1.16.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00-load.t .. 1/? # Testing Lingua::PTD 1.16, Perl 5.030003, /usr/bin/perl
t/00-load.t .. ok   
t/02_ptd.t ... ok       
All tests successful.
Files=2, Tests=183,  1 wallclock secs ( 0.05 usr  0.01 sys +  0.22 cusr  0.06 csys =  0.34 CPU)
Result: PASS
Terminal does not support GetHistory.
Lockfile removed.
  AMBS/Lingua-PTD-1.16.tar.gz
Tests succeeded but one dependency not OK (Term::ReadLine::Gnu)
  AMBS/Lingua-PTD-1.16.tar.gz
  [dependencies] -- NA
Failed during this command:
 HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz        : writemakefile NO '/usr/bin/perl Makefile.PL' returned status 256
 AMBS/Lingua-PTD-1.16.tar.gz                  : make_test NO one dependency not OK (Term::ReadLine::Gnu)

```
Term::ReadLine::Gnu ကို install လုပ်တယ်..  

```
cpan[2]> install Term::ReadLine::Gnu
Running install for module 'Term::ReadLine::Gnu'
  HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Term-ReadLine-Gnu-1.42-1
  HAYASHI/Term-ReadLine-Gnu-1.42.tar.gz
  '/usr/bin/perl Makefile.PL' returned status 256, not re-running
```

ပြီးမှ Lingua::NATools ကို ဆက် install လုပ်တော့ အဆင်ပြေသွားတယ်။  

```
cpan[3]> install Lingua::NATools
Running install for module 'Lingua::NATools'
Checksum for /home/ye/.cpan/sources/authors/id/A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz ok
Configuring A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz with Build.PL
Checking prerequisites...
  requires:
    !  Lingua::PTD is not installed

ERRORS/WARNINGS FOUND IN PREREQUISITES.  You may wish to install the versions
of the modules indicated above before proceeding with this installation

Checking NATools version... 0.7.12
Checking for stdlib.h... Checking for cc... x86_64-linux-gnu-gcc
yes
Checking for stdarg.h... yes
Checking for string.h... yes
Checking for float.h... yes
Checking for assert.h... yes
Checking for ctype.h... yes
Checking for errno.h... yes
Checking for limits.h... yes
Checking for locale.h... yes
Checking for math.h... yes
Checking for setjmp.h... yes
Checking for signal.h... yes
Checking for stddef.h... yes
Checking for stdio.h... yes
Checking for time.h... yes
Checking for library containing log2... m
Checking for library containing pow... none required
Checking for library containing log10... none required
Checking for library containing log... none required
Checking for library containing exp... none required
Checking for library containing sqrt... none required
Checking for gzopen in -lz... yes
Checking for gzread in -lz... yes
Checking for gzwrite in -lz... yes
Checking for gzclose in -lz... yes
Checking for glib-2.0 >= 2.8... yes
Checking for sqlite3 >= 3.5.0... yes
Checking for sqlite3 binary... yes
Checking for Berkeley DB header >= 4.3.0... yes
Checking for Berkeley DB library >= 4.3.0... yes
configure: LIBS:  -lm -lz -lglib-2.0 -L/usr/local/lib -lsqlite3 -ldb
configure: CFLAGS:   -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include -I/usr/local/include
Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'Lingua-NATools' version 'v0.7.12'
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  /usr/bin/perl Build.PL -- OK
Running Build for A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz
---- Unsatisfied dependencies detected during ----
----    AMBS/Lingua-NATools-v0.7.12.tar.gz    ----
    Lingua::PTD [requires]
Running install for module 'Lingua::PTD'
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-PTD-1.16-1
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been prepared
  AMBS/Lingua-PTD-1.16.tar.gz
  Has already been made
Running make test for AMBS/Lingua-PTD-1.16.tar.gz
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00-load.t .. 1/? # Testing Lingua::PTD 1.16, Perl 5.030003, /usr/bin/perl
t/00-load.t .. ok   
t/02_ptd.t ... ok       
All tests successful.
Files=2, Tests=183,  0 wallclock secs ( 0.06 usr  0.01 sys +  0.24 cusr  0.05 csys =  0.36 CPU)
Result: PASS
  AMBS/Lingua-PTD-1.16.tar.gz
  /usr/bin/make test -- OK
Running make install for AMBS/Lingua-PTD-1.16.tar.gz
Manifying 1 pod document
Manifying 7 pod documents
Installing /usr/local/share/perl/5.30.3/Lingua/PTD.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/SQLite.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/Dumper.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/StarDict.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/XzDmp.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/TSV.pm
Installing /usr/local/share/perl/5.30.3/Lingua/PTD/BzDmp.pm
Installing /usr/local/man/man1/nat-ptd.1p
Installing /usr/local/man/man3/Lingua::PTD::StarDict.3pm
Installing /usr/local/man/man3/Lingua::PTD.3pm
Installing /usr/local/man/man3/Lingua::PTD::XzDmp.3pm
Installing /usr/local/man/man3/Lingua::PTD::BzDmp.3pm
Installing /usr/local/man/man3/Lingua::PTD::Dumper.3pm
Installing /usr/local/man/man3/Lingua::PTD::TSV.3pm
Installing /usr/local/man/man3/Lingua::PTD::SQLite.3pm
Installing /usr/local/bin/nat-ptd
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  AMBS/Lingua-PTD-1.16.tar.gz
  sudo /usr/bin/make install  -- OK
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/Lingua-NATools-v0.7.12-1
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  Has already been prepared
Running Build for A/AM/AMBS/Lingua-NATools-v0.7.12.tar.gz
Building Lingua-NATools
  [pod2man] pods/nat-css.pod
  [pod2man] pods/nat-initmat.pod
  [pod2man] pods/nat-ipfp.pod
  [pod2man] pods/nat-mat2dic.pod
  [pod2man] pods/nat-postbin.pod
  [pod2man] pods/nat-pre.pod
  [pod2man] pods/nat-samplea.pod
  [pod2man] pods/nat-sampleb.pod
  [pod2man] pods/nat-sentalign.pod
  [cc] src/invindexjoin.c
  [cc] src/unicode.c
  [cc] src/dictionary.c
  [cc] src/invindex.c
  [cc] src/corpusinfo.c
  [cc] src/ipfp.c
  [cc] src/sent_align.c
  [cc] src/matrix.c
  [cc] src/bucket.c
  [cc] src/grep.c
  [cc] src/mkdict.c
  [cc] src/sampleb.c
  [cc] src/ngramidx.c
  [cc] src/pre.c
  [cc] src/ngrams_bdb.c
  [cc] src/search_sentence.c
  [cc] src/natlexicon.c
  [cc] src/ntdump.c
  [cc] src/standard.c
  [cc] src/initmat.c
  [cc] src/corpus.c
  [cc] src/parseini.c
  [cc] src/partials.c
  [cc] src/words2id.c
  [cc] src/words.c
  [cc] src/natdict.c
  [cc] src/server.c
  [cc] src/mat2dic.c
  [cc] src/adddic.c
  [cc] src/samplea.c
  [cc] src/tempdict.c
  [cc] src/srvshared.c
  [cc] src/postbin.c
  [ld] building libnatools.so
  [ld] nat-grep
  [ld] nat-mat2dic
  [ld] nat-ipfp
  [ld] nat-css
  [ld] nat-samplea
  [ld] nat-ntd-add
  [ld] nat-postbin
  [ld] nat-mkntd
  [ld] nat-ntd-dump
  [ld] nat-ngrams
  [ld] nat-sampleb
  [ld] nat-initmat
  [ld] nat-server
  [ld] nat-sentalign
  [ld] nat-mergeidx
  [ld] nat-words2id
  [ld] nat-pre
  [XS] natools.xs
  [CC] natools.c
  [LD] NATools.so
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  ./Build -- OK
Running Build test for AMBS/Lingua-NATools-v0.7.12.tar.gz
t/bin/corpus.t ............... ok   
t/bin/nat-pre.t .............. ok      
t/bin/nat-these.t ............ Warning: some of these tests can take about 1 minute on slow machines
t/bin/nat-these.t ............ ok      
t/bin/words.t ................ ok   
t/pm/00_basic.t .............. ok     
t/pm/01_config.t ............. ok     
t/pm/03.1_create_from_tmx.t .. 33/? # Let the server start...
t/pm/03.1_create_from_tmx.t .. ok     
t/pm/10_pcorpus.t ............ ok   
t/pm/11_corpus.t ............. ok   
t/pm/14_scripts.t ............ ok       
t/pm/15_cgis.t ............... ok   
t/pm/16_pods.t ............... skipped: export AUTHOR_TEST for author tests
t/pm/17_pod_coverage.t ....... skipped: export AUTHOR_TEST for author tests
t/pm/20_patterns.t ........... 1/26 Parsing rules file: [t/pm/20_patterns.in]
t/pm/20_patterns.t ........... ok     
All tests successful.
Files=14, Tests=8840, 10 wallclock secs ( 0.31 usr  0.01 sys +  6.15 cusr  0.67 csys =  7.14 CPU)
Result: PASS
  AMBS/Lingua-NATools-v0.7.12.tar.gz
  ./Build test -- OK
Running Build install for AMBS/Lingua-NATools-v0.7.12.tar.gz
Building Lingua-NATools
Files found in blib/arch: installing files in blib/lib into architecture dependent library tree
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/auto/Lingua/NATools/NATools.bs
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/auto/Lingua/NATools/NATools.so
Installing /usr/local/man/man1/nat-pair2tmx.1p
Installing /usr/local/man/man1/nat-create.1p
Installing /usr/local/man/man1/nat-sentalign.1
Installing /usr/local/man/man1/nat-lex2perl.1p
Installing /usr/local/man/man1/nat-mkMakefile.1p
Installing /usr/local/man/man1/nat-mkRealDict.1p
Installing /usr/local/man/man1/nat-sampleb.1
Installing /usr/local/man/man1/nat-mat2dic.1
Installing /usr/local/man/man1/nat-postbin.1
Installing /usr/local/man/man1/nat-initmat.1
Installing /usr/local/man/man1/nat-samplea.1
Installing /usr/local/man/man1/nat-examplesExtractor.1p
Installing /usr/local/man/man1/nat-substDict.1p
Installing /usr/local/man/man1/nat-dict.1p
Installing /usr/local/man/man1/nat-compareDicts.1p
Installing /usr/local/man/man1/nat-rank.1p
Installing /usr/local/man/man1/nat-shell.1p
Installing /usr/local/man/man1/nat-makeCWB.1p
Installing /usr/local/man/man1/nat-codify.1p
Installing /usr/local/man/man1/nat-addDict.1p
Installing /usr/local/man/man1/nat-css.1
Installing /usr/local/man/man1/nat-dumpDicts.1p
Installing /usr/local/man/man1/nat-sentence-align.1p
Installing /usr/local/man/man1/nat-ipfp.1
Installing /usr/local/man/man1/nat-tmx2pair.1p
Installing /usr/local/man/man1/nat-pre.1
Installing /usr/local/man/man1/nat-ngramsIdx.1p
Installing /usr/local/man/man1/nat-StarDict.1p
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Dict.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Lexicon.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/NATDict.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/PatternRules.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/CGI.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Matrix.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/PCorpus.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Corpus.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Client.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/Config.pm
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools/ConfigData.pm
Installing /usr/local/man/man3/Lingua::NATools::Lexicon.3pm
Installing /usr/local/man/man3/Lingua::NATools::PCorpus.3pm
Installing /usr/local/man/man3/Lingua::NATools.3pm
Installing /usr/local/man/man3/Lingua::NATools::Config.3pm
Installing /usr/local/man/man3/Lingua::NATools::Client.3pm
Installing /usr/local/man/man3/Lingua::NATools::ConfigData.3pm
Installing /usr/local/man/man3/Lingua::NATools::NATDict.3pm
Installing /usr/local/man/man3/Lingua::NATools::Dict.3pm
Installing /usr/local/man/man3/Lingua::NATools::Matrix.3pm
Installing /usr/local/man/man3/Lingua::NATools::CGI.3pm
Installing /usr/local/man/man3/Lingua::NATools::Corpus.3pm
Installing /usr/local/bin/nat-rank
Installing /usr/local/bin/nat-mergeidx
Installing /usr/local/bin/nat-server
Installing /usr/local/bin/nat-css
Installing /usr/local/bin/nat-samplea
Installing /usr/local/bin/nat-lex2perl
Installing /usr/local/bin/nat-examplesExtractor
Installing /usr/local/bin/nat-pre
Installing /usr/local/bin/nat-sentalign
Installing /usr/local/bin/nat-mat2dic
Installing /usr/local/bin/nat-pair2tmx
Installing /usr/local/bin/nat-tmx2pair
Installing /usr/local/bin/nat-compareDicts
Installing /usr/local/bin/nat-codify
Installing /usr/local/bin/nat-grep
Installing /usr/local/bin/nat-shell
Installing /usr/local/bin/nat-words2id
Installing /usr/local/bin/nat-create
Installing /usr/local/bin/nat-postbin
Installing /usr/local/bin/nat-ngramsIdx
Installing /usr/local/bin/nat-dumpDicts
Installing /usr/local/bin/nat-mkMakefile
Installing /usr/local/bin/nat-ngrams
Installing /usr/local/bin/nat-StarDict
Installing /usr/local/bin/nat-ntd-add
Installing /usr/local/bin/nat-sampleb
Installing /usr/local/bin/nat-ipfp
Installing /usr/local/bin/nat-mkRealDict
Installing /usr/local/bin/nat-addDict
Installing /usr/local/bin/nat-dict
Installing /usr/local/bin/nat-makeCWB
Installing /usr/local/bin/nat-sentence-align
Installing /usr/local/bin/nat-mkntd
Installing /usr/local/bin/nat-substDict
Installing /usr/local/bin/nat-initmat
Installing /usr/local/bin/nat-ntd-dump
Installing /usr/local/lib/libnatools.so
/sbin/ldconfig.real: Path `/usr/lib/x86_64-linux-gnu' given more than once
(from /etc/ld.so.conf.d/x86_64-linux-gnu.conf:4 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/lib/x86_64-linux-gnu' given more than once
(from <builtin>:0 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/usr/lib/x86_64-linux-gnu' given more than once
(from <builtin>:0 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/usr/lib' given more than once
(from <builtin>:0 and <builtin>:0)
/sbin/ldconfig.real: /usr/local/lib/libnatools.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/liblouis.so.20 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libsqlite3.so.0 is not a symbolic link

/sbin/ldconfig.real: /lib/x86_64-linux-gnu/ld-2.32.so is the dynamic linker, ignoring

/sbin/ldconfig.real: /usr/local/lib/libnatools.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/liblouis.so.20 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libsqlite3.so.0 is not a symbolic link

  AMBS/Lingua-NATools-v0.7.12.tar.gz
  sudo ./Build install  -- OK

cpan[4]> 
```

## Finding Perl Module Path

perl-doc က ကိုယ့်စက်ထဲမှာ မရှိသေရင် အောက်ပါလိုမျိုး installation လုပ်ရလိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts$ sudo apt-get install perl-doc
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
  python3-colorama python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  perl-doc
0 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 7,492 kB of archives.
After this operation, 14.4 MB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 perl-doc all 5.30.3-4 [7,492 kB]
Fetched 7,492 kB in 3s (2,219 kB/s)   
Selecting previously unselected package perl-doc.
(Reading database ... 662613 files and directories currently installed.)
Preparing to unpack .../perl-doc_5.30.3-4_all.deb ...
Adding 'diversion of /usr/bin/perldoc to /usr/bin/perldoc.stub by perl-doc'
Unpacking perl-doc (5.30.3-4) ...
Setting up perl-doc (5.30.3-4) ...
Processing triggers for man-db (2.9.3-2) ...
```
ဥပမာ Data::Dumper နဲ့ ပတ်သက်တာကို ရှာကြည့်ရင်အောက်ပါအတိုင်း တွေ့ရလိမ့်မယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts$ perldoc -l Data::Dumper
/usr/lib/x86_64-linux-gnu/perl/5.30/Data/Dumper.pm
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts$
```

တကယ်လို့ Lingua::NATools ကို install မလုပ်ရသေးရင် (သို့မဟုတ်) install က failed ဖြစ်နေခဲ့ရင် အောက်ပါလိုမျိုး documentation ကို ရှာမတွေ့ဘူးလို့ ပြောလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts$ perldoc -l Lingua::NATools
No documentation found for "Lingua::NATools".
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts$
```

installed လုပ်ထားရင်တော့ အောက်ပါအတိုင်း perl module (pm file) ရှိတဲ့ path ကို ပြပေးလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$ perldoc -l Lingua::NATools
/usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Lingua/NATools.pm
```

perl -V နဲ့ လည်း ကြည့်လို့ရတယ်...  

## Test Alignment with NATools

အရင် ဗားရှင်းအဟောင်းရဲ့ NATools - Getting Started ဆိုတဲ့ link ကိုလည်း refer လုပ်ခဲ့တယ်။  
[http://linguateca.di.uminho.pt/natools/htdocs/getting-started.html](http://linguateca.di.uminho.pt/natools/htdocs/getting-started.html)  

installation က အဆင်ပြေပြေနဲ့ ပြီးခဲ့ရင် nat နဲ့ စတဲ့ command တွေကို အောက်ပါအတိုင်း တွေ့ရလိမ့်မယ်။  


```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$ nat-
nat-addDict            nat-examplesExtractor  nat-mergeidx           nat-ntd-dump           nat-sampleb            nat-tmx2pair
nat-codify             nat-grep               nat-mkMakefile         nat-pair2tmx           nat-sentalign          nat-words2id
nat-compareDicts       nat-initmat            nat-mkntd              nat-postbin            nat-sentence-align     
nat-create             nat-ipfp               nat-mkRealDict         nat-pre                nat-server             
nat-css                nat-lex2perl           nat-ngrams             nat-ptd                nat-shell              
nat-dict               nat-makeCWB            nat-ngramsIdx          nat-rank               nat-StarDict           
nat-dumpDicts          nat-mat2dic            nat-ntd-add            nat-samplea            nat-substDict          
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$
```

အသုံးပြုပုံနဲ့ ပတ်သက်ပြီးအောက်ပါ NATools perl module linek ကို refer လုပ်ပါ။  
[https://metacpan.org/pod/Lingua::NATools](https://metacpan.org/pod/Lingua::NATools)  
command တွေနဲ့ ပတ်သက်ပြီး အောက်ပါ link ကို ဖတ်ပါ။  
[https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12](https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12)  
ReadMe file:  
[https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/view/README](https://metacpan.org/release/AMBS/Lingua-NATools-v0.7.12/view/README)  

အောက်ပါ thesis ထဲမှာ NATools နဲ့ အရင်က လုပ်ခဲ့တဲ့ probabilistic alignment, dictionary extraction တွေနဲ့ ပတ်သက်ပြီး လေ့လာနိုင်...  
အသုံးဝင်တဲ့ perl script တချို့ကိုလည်း နမူနာအနေနဲ့ ရလိမ့်မယ်...  
[Parallel corpora word alignment and applications, Alberto Manuel Brand˜ao Sim˜oes](http://alfarrabio.di.uminho.pt/~albie/publications/msc.pdf)  

အောက်ပါ folder path အောက်မှာလည်း script တချို့ကို တွေ့နိုင်...  
[/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts](/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/NATools-0.5.10/NAT/scripts)  


let's check ```nat-create``` command  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$ nat-create --help
nat-create: creates a NATools corpus, and extracts its PTD.

	nat-create [-q] [-langs=L1..L2] [-tokenize] [-ngrams]
	           [-csize=70000]
	           [-noEM] [-ipfp[=5]] [-samplea[=10]] [-sampleb[=10]]
	           [-id=ID] [-i] <corpusL1> <corpusL2>

	nat-create [-q] [-langs=L1..L2] [-tokenize] [-ngrams]
	           [-csize=70000]
	           [-noEM] [-ipfp[=5]] [-samplea[=10]] [-sampleb[=10]]
	           [-id=ID] [-i] -tmx <tmx>

For more help, please run 'perldoc nat-create'
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/phrase/natools/Lingua-NATools-v0.7.12/scripts$
```

## Reference

- [https://metacpan.org/pod/Lingua::NATools](https://metacpan.org/pod/Lingua::NATools)  
[Parallel corpora word alignment and applications, Alberto Manuel Brand˜ao Sim˜oes](http://alfarrabio.di.uminho.pt/~albie/publications/msc.pdf)  

- [Paper: Parallel Corpora based Translation Resources Extraction, Alberto Sim˜oes, Jos´e Jo˜ao Almeida](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.149.5698&rep=rep1&type=pdf)  

- [https://stackoverflow.com/questions/1557959/how-can-i-find-out-where-a-perl-module-is-installed](https://stackoverflow.com/questions/1557959/how-can-i-find-out-where-a-perl-module-is-installed)  

- [https://www.cpan.org/modules/by-module/Lingua/AMBS/](https://www.cpan.org/modules/by-module/Lingua/AMBS/)  

