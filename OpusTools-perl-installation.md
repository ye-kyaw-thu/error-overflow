# OpusTools-perl-installation

OpusTools-perl [https://github.com/Helsinki-NLP/Opus-MT](https://github.com/Helsinki-NLP/Opus-MT) က Helsinki-NLP က develop လုပ်ထားတဲ့ perl toolkit ပါ။ ဒီနေရာမှာတော့ installation လုပ်တဲ့ အဆင့်တွေနဲ့ tool တစ်ခုဖြစ်တဲ့ tmx ဖိုင် converter ကို သုံးတာကို လုပ်ပြထားပါတယ်။ TMX ဖိုင်ဆိုတာက [Translation Memory Exchange](https://en.wikipedia.org/wiki/Translation_Memory_eXchange) ဖိုင်ရဲ့ format ပါ။ တကယ့် professional ဘာသာပြန်သမားတွေက သုံးကြတဲ့ tool တွေမှာ သိမ်းတဲ့ format တစ်ခုပါ။ အတိုရှင်းပြရရင် XML file format ပါ။ အဲဒီ tmx format ကနေ ပုံမှန် text parallel corpus or moses parallel corpus format အဖြစ် ပြောင်းဖို့အတွက် OpusTools-perl package ရဲ့ tmx2moses (perl script) ကို သုံးပြထားပါတယ်။  

## git clone

git clone command နဲ့ GitHub repository ကို ကိုယ့်စက်ထဲကို download လုပ်ယူပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/Helsinki-NLP/OpusTools-perl
Cloning into 'OpusTools-perl'...
remote: Enumerating objects: 166, done.
remote: Counting objects: 100% (166/166), done.
remote: Compressing objects: 100% (115/115), done.
remote: Total 838 (delta 82), reused 116 (delta 48), pack-reused 672
Receiving objects: 100% (838/838), 600.63 KiB | 1.16 MiB/s, done.
Resolving deltas: 100% (478/478), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd OpusTools-perl/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ ls
CHANGES  inc  lib  LICENSE  Makefile.PL  README.md  scripts  t  TODO
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ cd scripts/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts$ ls
admin  alignments  convert  multilingwis  opus-cat  opus-index  opus-read  opus-udpipe
```

OpusTools-perl ဖိုလ်ဒါထဲဝင်ပြီး file list လုပ်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ ls
CHANGES  inc  lib  LICENSE  Makefile.PL  README.md  scripts  t  TODO
```
## perl Makefile.PL

perl Makefile.PL က perl package တွေကို install လုပ်တဲ့အခါမှာ ပေးရတဲ့ command တစ်ခုပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ perl Makefile.PL
*** Module::AutoInstall version 1.19
*** Checking for Perl dependencies...
[Core Features]
- Archive::Zip     ...loaded. (1.68)
- CGI              ...missing.
- Cwd              ...loaded. (3.78)
- DB_File          ...loaded. (1.843)
- HTML::Entities   ...loaded. (3.75)
- Lingua::Sentence ...missing.
- Test::More       ...loaded. (1.302183)
- Ufal::UDPipe     ...missing.
- XML::Parser      ...loaded. (2.46)
- XML::Writer      ...missing.
==> Auto-install the 4 mandatory module(s) from CPAN? [y] y
*** Dependencies will be installed the next time you type 'make'.
    (You may need to do that as the 'root' user.)
*** Module::AutoInstall configuration finished.
Warning: prerequisite CGI 0 not found.
Warning: prerequisite Lingua::Sentence 0 not found.
Warning: prerequisite Ufal::UDPipe 0 not found.
Warning: prerequisite XML::Writer 0 not found.
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Generating a Unix-style Makefile
Writing Makefile for OPUS::Tools
Writing MYMETA.yml and MYMETA.json
```

## make all

Error မရှိဘူး ဆိုရင်တော့ ```make all``` ကို run ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ make all
"/usr/bin/perl" "-Iinc" Makefile.PL --config= --installdeps=CGI,0,Lingua::Sentence,0,Ufal::UDPipe,0,XML::Writer,0
*** Installing dependencies...
*** Installing CGI...

CPAN.pm requires configuration, but most of it can be done automatically.
If you answer 'no' below, you will enter an interactive dialog for each
configuration option instead.

Would you like to configure as much as possible automatically? [yes] yes

 <install_help>

Warning: You do not have write permission for Perl library directories.

To install modules, you need to configure a local Perl library directory or
escalate your privileges.  CPAN can help you by bootstrapping the local::lib
module or by configuring itself to use 'sudo' (if available).  You may also
resolve this problem manually if you need to customize your setup.

What approach do you want?  (Choose 'local::lib', 'sudo' or 'manual')
 [local::lib] sudo


Autoconfiguration complete.

commit: wrote '/home/ye/.cpan/CPAN/MyConfig.pm'

You can re-run configuration any time with 'o conf init' in the CPAN shell
Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/home/ye/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/02packages.details.txt.gz
Reading '/home/ye/.cpan/sources/modules/02packages.details.txt.gz'
  Database was generated on Fri, 26 Mar 2021 11:17:03 GMT
............................................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/03modlist.data.gz
Reading '/home/ye/.cpan/sources/modules/03modlist.data.gz'
DONE
Writing /home/ye/.cpan/Metadata
Running install for module 'CGI'
Fetching with LWP:
http://www.cpan.org/authors/id/L/LE/LEEJO/CGI-4.51.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/L/LE/LEEJO/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/L/LE/LEEJO/CGI-4.51.tar.gz ok
'YAML' not installed, will not store persistent state
Configuring L/LE/LEEJO/CGI-4.51.tar.gz with Makefile.PL
Checking if your kit is complete...
Looks good
Warning: prerequisite Test::Warn 0.3 not found.
Have /usr/lib/x86_64-linux-gnu/perl-base
Want /usr/lib/x86_64-linux-gnu/perl/5.30
Your perl and your Config.pm seem to have different ideas about the
architecture they are running on.
Perl thinks: [perl-base]
Config says: [x86_64-linux-gnu-thread-multi]
This may or may not cause problems. Please check your installation of perl
if you have problems building this extension.
Warning: LINKTYPE set to '', no longer necessary
Generating a Unix-style Makefile
Writing Makefile for CGI
Writing MYMETA.yml and MYMETA.json
  LEEJO/CGI-4.51.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for L/LE/LEEJO/CGI-4.51.tar.gz
---- Unsatisfied dependencies detected during ----
----           LEEJO/CGI-4.51.tar.gz          ----
    Test::Warn [build_requires]
Running install for module 'Test::Warn'
Fetching with LWP:
http://www.cpan.org/authors/id/B/BI/BIGJ/Test-Warn-0.36.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/B/BI/BIGJ/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/B/BI/BIGJ/Test-Warn-0.36.tar.gz ok
Configuring B/BI/BIGJ/Test-Warn-0.36.tar.gz with Makefile.PL
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
Writing Makefile for Test::Warn
Writing MYMETA.yml and MYMETA.json
  BIGJ/Test-Warn-0.36.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for B/BI/BIGJ/Test-Warn-0.36.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/Test-Warn-0.36-0'
cp Warn.pm blib/lib/Test/Warn.pm
Manifying 1 pod document
make[1]: Leaving directory '/home/ye/.cpan/build/Test-Warn-0.36-0'
  BIGJ/Test-Warn-0.36.tar.gz
  /usr/bin/make -- OK
Running make test for BIGJ/Test-Warn-0.36.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/Test-Warn-0.36-0'
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/1.t ............... ok   
t/carped.t .......... ok   
t/warning_is.t ...... ok     
t/warning_like.t .... ok     
t/warnings_are.t .... ok       
t/warnings_exist.t .. ok    
t/warnings_like.t ... ok       
All tests successful.
Files=7, Tests=841,  1 wallclock secs ( 0.08 usr  0.01 sys +  1.07 cusr  0.03 csys =  1.19 CPU)
Result: PASS
make[1]: Leaving directory '/home/ye/.cpan/build/Test-Warn-0.36-0'
  BIGJ/Test-Warn-0.36.tar.gz
  /usr/bin/make test -- OK
Running make install for BIGJ/Test-Warn-0.36.tar.gz
[sudo] password for ye: 
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/Test/Warn.pm
Installing /usr/local/man/man3/Test::Warn.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  BIGJ/Test-Warn-0.36.tar.gz
  sudo /usr/bin/make install  -- OK
  LEEJO/CGI-4.51.tar.gz
  Has already been unwrapped into directory /home/ye/.cpan/build/CGI-4.51-0
  LEEJO/CGI-4.51.tar.gz
  Has already been prepared
Running make for L/LE/LEEJO/CGI-4.51.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/CGI-4.51-0'
cp lib/Fh.pm blib/lib/Fh.pm
cp lib/CGI/HTML/Functions.pm blib/lib/CGI/HTML/Functions.pm
cp lib/CGI/File/Temp.pm blib/lib/CGI/File/Temp.pm
cp lib/CGI/HTML/Functions.pod blib/lib/CGI/HTML/Functions.pod
cp lib/CGI/Util.pm blib/lib/CGI/Util.pm
cp lib/CGI/Cookie.pm blib/lib/CGI/Cookie.pm
cp lib/CGI/Carp.pm blib/lib/CGI/Carp.pm
cp lib/CGI/Pretty.pm blib/lib/CGI/Pretty.pm
cp lib/CGI/Push.pm blib/lib/CGI/Push.pm
cp lib/CGI.pm blib/lib/CGI.pm
cp lib/CGI.pod blib/lib/CGI.pod
Manifying 7 pod documents
make[1]: Leaving directory '/home/ye/.cpan/build/CGI-4.51-0'
  LEEJO/CGI-4.51.tar.gz
  /usr/bin/make -- OK
Running make test for LEEJO/CGI-4.51.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/CGI-4.51-0'
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t t/headers/*.t
t/append_query.t ............ ok     
t/arbitrary_handles.t ....... ok   
t/autoescape.t .............. ok     
t/can.t ..................... ok   
t/carp.t .................... 1/76 [Fri Mar 26 18:35:53 2021] carp.t: foo at /home/ye/.cpan/build/CGI-4.51-0/blib/lib/CGI/Carp.pm line 360.
t/carp.t .................... ok     
t/cgi.t ..................... 1/25 # cgi-lib.pl routines
private_tempfiles has been deprecated at /home/ye/.cpan/build/CGI-4.51-0/blib/lib/CGI.pm line 3236.
t/cgi.t ..................... ok     
t/changes.t ................. skipped: Test::CPAN::Changes required for this test
t/charset.t ................. ok   
t/checkbox_group.t .......... ok   
t/command_line.t ............ ok   
t/compiles_pod.t ............ ok    
t/cookie.t .................. ok     
t/delete.t .................. ok    
t/Dump.t .................... ok   
t/end_form.t ................ ok   
t/form.t .................... ok    
t/function.t ................ ok     
t/gh-155.t .................. ok    
t/headers.t ................. ok    
t/headers/attachment.t ...... ok   
t/headers/charset.t ......... ok   
t/headers/cookie.t .......... ok   
t/headers/default.t ......... ok   
t/headers/nph.t ............. ok   
t/headers/p3p.t ............. ok   
t/headers/target.t .......... ok   
t/headers/type.t ............ ok    
t/hidden.t .................. ok   
t/html.t .................... ok     
t/html_functions.t .......... ok     
t/http.t .................... ok   
t/init.t .................... ok   
t/multipart_globals.t ....... ok   
t/multipart_init.t .......... ok   
t/multipart_start.t ......... ok   
t/no_tabindex.t ............. ok     
t/param_fetch.t ............. ok   
t/param_list_context.t ...... ok   
t/popup_menu.t .............. ok   
t/postdata.t ................ ok     
t/pretty.t .................. CGI::Pretty is DEPRECATED and will be removed in a future release. Please see https://github.com/leejo/CGI.pm/issues/162 for more information at /home/ye/.cpan/build/CGI-4.51-0/blib/lib/CGI/Pretty.pm line 20.
t/pretty.t .................. ok   
t/push.t .................... ok     
t/query_string.t ............ ok   
t/redirect_query_string.t ... ok   
t/request.t ................. ok     
t/rt-31107.t ................ ok   
t/rt-52469.t ................ ok   
t/rt-57524.t ................ ok   
t/rt-75628.t ................ ok   
t/rt-84767.t ................ ok   
t/save_read_roundtrip.t ..... ok   
t/sorted.t .................. ok   
t/start_end_asterisk.t ...... ok     
t/start_end_end.t ........... ok     
t/start_end_start.t ......... ok     
t/unescapeHTML.t ............ ok   
t/upload.t .................. ok    
t/upload_quoted_unquoted.t .. ok   
t/uploadInfo.t .............. ok    
t/url.t ..................... ok   
t/user_agent.t .............. ok   
t/utf8.t .................... ok   
t/util-58.t ................. ok   
t/util.t .................... ok     
All tests successful.
Files=64, Tests=1580,  4 wallclock secs ( 0.10 usr  0.08 sys +  2.71 cusr  0.36 csys =  3.25 CPU)
Result: PASS
make[1]: Leaving directory '/home/ye/.cpan/build/CGI-4.51-0'
  LEEJO/CGI-4.51.tar.gz
  /usr/bin/make test -- OK
Running make install for LEEJO/CGI-4.51.tar.gz
Manifying 7 pod documents
Installing /usr/local/share/perl/5.30.3/Fh.pm
Installing /usr/local/share/perl/5.30.3/CGI.pm
Installing /usr/local/share/perl/5.30.3/CGI.pod
Installing /usr/local/share/perl/5.30.3/CGI/Cookie.pm
Installing /usr/local/share/perl/5.30.3/CGI/Push.pm
Installing /usr/local/share/perl/5.30.3/CGI/Util.pm
Installing /usr/local/share/perl/5.30.3/CGI/Pretty.pm
Installing /usr/local/share/perl/5.30.3/CGI/Carp.pm
Installing /usr/local/share/perl/5.30.3/CGI/HTML/Functions.pod
Installing /usr/local/share/perl/5.30.3/CGI/HTML/Functions.pm
Installing /usr/local/share/perl/5.30.3/CGI/File/Temp.pm
Installing /usr/local/man/man3/CGI.3pm
Installing /usr/local/man/man3/CGI::Cookie.3pm
Installing /usr/local/man/man3/CGI::Carp.3pm
Installing /usr/local/man/man3/CGI::Util.3pm
Installing /usr/local/man/man3/CGI::Pretty.3pm
Installing /usr/local/man/man3/CGI::HTML::Functions.3pm
Installing /usr/local/man/man3/CGI::Push.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  LEEJO/CGI-4.51.tar.gz
  sudo /usr/bin/make install  -- OK
*** CGI successfully installed.
*** Installing Lingua::Sentence...
Running install for module 'Lingua::Sentence'
Fetching with LWP:
http://www.cpan.org/authors/id/C/CA/CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/C/CA/CAPOEIRAB/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/C/CA/CAPOEIRAB/Lingua-Sentence-1.100.tar.gz ok
Configuring C/CA/CAPOEIRAB/Lingua-Sentence-1.100.tar.gz with Makefile.PL
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
Writing Makefile for Lingua::Sentence
Writing MYMETA.yml and MYMETA.json
  CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for C/CA/CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/Lingua-Sentence-1.100-0'
cp share/nonbreaking_prefix.sv blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sv
cp share/nonbreaking_prefix.it blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.it
cp share/nonbreaking_prefix.fr blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fr
cp share/nonbreaking_prefix.lt blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lt
cp share/nonbreaking_prefix.hu blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.hu
cp share/nonbreaking_prefix.ro blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ro
cp share/nonbreaking_prefix.es blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.es
cp share/nonbreaking_prefix.lv blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lv
cp share/nonbreaking_prefix.el blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.el
cp share/nonbreaking_prefix.da blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.da
cp share/nonbreaking_prefix.sl blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sl
cp share/nonbreaking_prefix.is blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.is
cp share/nonbreaking_prefix.pl blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pl
cp share/nonbreaking_prefix.ru blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ru
cp share/nonbreaking_prefix.ca blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ca
cp share/nonbreaking_prefix.pt blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pt
cp share/nonbreaking_prefix.cs blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.cs
cp share/nonbreaking_prefix.sk blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sk
cp share/nonbreaking_prefix.fi blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fi
cp share/nonbreaking_prefix.en blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.en
cp share/nonbreaking_prefix.nl blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.nl
cp share/nonbreaking_prefix.de blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.de
cp lib/Lingua/Sentence.pm blib/lib/Lingua/Sentence.pm
Manifying 1 pod document
make[1]: Leaving directory '/home/ye/.cpan/build/Lingua-Sentence-1.100-0'
  CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
  /usr/bin/make -- OK
Running make test for CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/Lingua-Sentence-1.100-0'
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sv (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pt (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.da (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.nl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.el (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.es (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lt (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sk (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.it (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.cs (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ru (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fi (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ro (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fr (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.is (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.hu (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ca (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lv (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.en (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.de (unchanged)
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/00-report-prereqs.t .. # 
# Versions for all modules listed in MYMETA.json (including optional ones):
# 
# === Configure Requires ===
# 
#     Module                  Want Have
#     ----------------------- ---- ----
#     ExtUtils::MakeMaker      any 7.58
#     File::ShareDir::Install 0.06 0.13
# 
# === Build Requires ===
# 
#     Module              Want Have
#     ------------------- ---- ----
#     ExtUtils::MakeMaker  any 7.58
# 
# === Test Requires ===
# 
#     Module              Want     Have
#     ------------------- ---- --------
#     ExtUtils::MakeMaker  any     7.58
#     File::Spec           any     3.78
#     Test::More           any 1.302183
# 
# === Test Recommends ===
# 
#     Module         Want     Have
#     ---------- -------- --------
#     CPAN::Meta 2.120900 2.150010
# 
# === Runtime Requires ===
# 
#     Module         Want  Have
#     -------------- ---- -----
#     Carp            any  1.50
#     File::ShareDir 1.02 1.118
#     File::Spec      any  3.78
#     Path::Tiny      any 0.116
#     strict          any  1.11
#     warnings        any  1.44
# 
t/00-report-prereqs.t .. ok   
t/Lingua-Sentence.t .... 1/32 WARNING: No known abbreviations for language 'xo', attempting fall-back to English version...
t/Lingua-Sentence.t .... ok     
All tests successful.
Files=2, Tests=33,  1 wallclock secs ( 0.01 usr  0.00 sys +  0.13 cusr  0.01 csys =  0.15 CPU)
Result: PASS
make[1]: Leaving directory '/home/ye/.cpan/build/Lingua-Sentence-1.100-0'
  CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
  /usr/bin/make test -- OK
Running make install for CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lv (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.da (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.it (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ro (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.en (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.cs (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pt (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.hu (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fi (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.de (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fr (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.is (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sk (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sv (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.nl (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ru (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ca (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lt (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.es (unchanged)
Skip blib/lib/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.el (unchanged)
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/Lingua/Sentence.pm
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pt
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.pl
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.de
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.it
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.en
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.is
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.nl
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.cs
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sk
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sv
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fr
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.es
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ru
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lv
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.sl
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.lt
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ro
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.ca
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.da
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.el
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.hu
Installing /usr/local/share/perl/5.30.3/auto/share/dist/Lingua-Sentence/nonbreaking_prefix.fi
Installing /usr/local/man/man3/Lingua::Sentence.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  CAPOEIRAB/Lingua-Sentence-1.100.tar.gz
  sudo /usr/bin/make install  -- OK
*** Lingua::Sentence successfully installed.
*** Installing Ufal::UDPipe...
Running install for module 'Ufal::UDPipe'
Fetching with LWP:
http://www.cpan.org/authors/id/S/ST/STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/S/ST/STRAKA/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/S/ST/STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz ok
Configuring S/ST/STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz with Build.PL
Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'Ufal-UDPipe' version 'v1.2.0.1'
  STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
  /usr/bin/perl Build.PL -- OK
Running Build for S/ST/STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
Building requires C++11 compiler, either g++ 4.7 or newer, or clang++ 3.2 or newer.
Building Ufal-UDPipe
x86_64-linux-gnu-gcc -Iudpipe -I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE -fPIC -x c++ -std=c++11 -fvisibility=hidden -w -Wno-reserved-user-defined-literal -c -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g -o udpipe/udpipe.o udpipe/udpipe.cpp
x86_64-linux-gnu-gcc -Iudpipe -I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE -fPIC -x c++ -std=c++11 -fvisibility=hidden -w -Wno-reserved-user-defined-literal -c -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g -o udpipe/udpipe_perl.o udpipe/udpipe_perl.cpp
x86_64-linux-gnu-gcc -Iudpipe -I/usr/lib/x86_64-linux-gnu/perl/5.30/CORE -DVERSION="v1.2.0.1" -DXS_VERSION="v1.2.0.1" -fPIC -x c++ -std=c++11 -fvisibility=hidden -w -Wno-reserved-user-defined-literal -c -D_REENTRANT -D_GNU_SOURCE -DDEBIAN -fwrapv -fno-strict-aliasing -pipe -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -O2 -g -o lib/Ufal/UDPipe.o lib/Ufal/UDPipe.c
ExtUtils::Mkbootstrap::Mkbootstrap('blib/arch/auto/Ufal/UDPipe/UDPipe.bs')
x86_64-linux-gnu-gcc -shared -L/usr/local/lib -fstack-protector-strong -o blib/arch/auto/Ufal/UDPipe/UDPipe.so lib/Ufal/UDPipe.o udpipe/udpipe.o udpipe/udpipe_perl.o -lstdc++
  STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
  ./Build -- OK
Running Build test for STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
t/import.t .. ok   
t/udpipe.t .. ok   
All tests successful.
Files=2, Tests=8,  0 wallclock secs ( 0.00 usr  0.01 sys +  0.10 cusr  0.01 csys =  0.12 CPU)
Result: PASS
  STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
  ./Build test -- OK
Running Build install for STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
Building requires C++11 compiler, either g++ 4.7 or newer, or clang++ 3.2 or newer.
Building Ufal-UDPipe
Files found in blib/arch: installing files in blib/lib into architecture dependent library tree
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/auto/Ufal/UDPipe/UDPipe.so
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/auto/Ufal/UDPipe/UDPipe.bs
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Ufal/UDPipe.pod
Installing /usr/local/lib/x86_64-linux-gnu/perl/5.30.3/Ufal/UDPipe.pm
Installing /usr/local/man/man3/Ufal::UDPipe.3pm
  STRAKA/Ufal-UDPipe-v1.2.0.1.tar.gz
  sudo ./Build install  -- OK
*** Ufal::UDPipe successfully installed.
*** Installing XML::Writer...
Running install for module 'XML::Writer'
Fetching with LWP:
http://www.cpan.org/authors/id/J/JO/JOSEPHW/XML-Writer-0.900.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/J/JO/JOSEPHW/CHECKSUMS
Checksum for /home/ye/.cpan/sources/authors/id/J/JO/JOSEPHW/XML-Writer-0.900.tar.gz ok
Configuring J/JO/JOSEPHW/XML-Writer-0.900.tar.gz with Makefile.PL
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
Writing Makefile for XML::Writer
Writing MYMETA.yml and MYMETA.json
  JOSEPHW/XML-Writer-0.900.tar.gz
  /usr/bin/perl Makefile.PL -- OK
Running make for J/JO/JOSEPHW/XML-Writer-0.900.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/XML-Writer-0.900-0'
cp Writer.pm blib/lib/XML/Writer.pm
Manifying 1 pod document
make[1]: Leaving directory '/home/ye/.cpan/build/XML-Writer-0.900-0'
  JOSEPHW/XML-Writer-0.900.tar.gz
  /usr/bin/make -- OK
Running make test for JOSEPHW/XML-Writer-0.900.tar.gz
make[1]: Entering directory '/home/ye/.cpan/build/XML-Writer-0.900-0'
PERL_DL_NONLAZY=1 "/usr/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/01_main.t ............... ok       
t/pod-coverage.t .......... ok   
t/pod.t ................... ok   
t/selfcontained_output.t .. ok     
All tests successful.
Files=4, Tests=274,  0 wallclock secs ( 0.02 usr  0.01 sys +  0.19 cusr  0.02 csys =  0.24 CPU)
Result: PASS
make[1]: Leaving directory '/home/ye/.cpan/build/XML-Writer-0.900-0'
  JOSEPHW/XML-Writer-0.900.tar.gz
  /usr/bin/make test -- OK
Running make install for JOSEPHW/XML-Writer-0.900.tar.gz
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/XML/Writer.pm
Installing /usr/local/man/man3/XML::Writer.3pm
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
  JOSEPHW/XML-Writer-0.900.tar.gz
  sudo /usr/bin/make install  -- OK
*** XML::Writer successfully installed.
*** Module::AutoInstall installation finished.
cp lib/OPUS/Tools.pm blib/lib/OPUS/Tools.pm
cp lib/OPUS/Tools/ISO639.pm blib/lib/OPUS/Tools/ISO639.pm
cp scripts/convert/bitext2tmx blib/script/bitext2tmx
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/bitext2tmx
cp scripts/convert/moses2opus blib/script/moses2opus
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/moses2opus
cp scripts/opus-cat blib/script/opus-cat
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-cat
cp scripts/opus-index blib/script/opus-index
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-index
cp scripts/convert/opus-iso639 blib/script/opus-iso639
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-iso639
cp scripts/admin/opus-make-website blib/script/opus-make-website
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-make-website
cp scripts/alignments/opus-merge-align blib/script/opus-merge-align
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-merge-align
cp scripts/alignments/opus-pivoting blib/script/opus-pivoting
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-pivoting
cp scripts/alignments/opus-pt2dic blib/script/opus-pt2dic
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-pt2dic
cp scripts/alignments/opus-pt2dice blib/script/opus-pt2dice
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-pt2dice
cp scripts/opus-read blib/script/opus-read
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-read
cp scripts/alignments/opus-split-align blib/script/opus-split-align
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-split-align
cp scripts/alignments/opus-swap-align blib/script/opus-swap-align
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-swap-align
cp scripts/opus-udpipe blib/script/opus-udpipe
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-udpipe
cp scripts/admin/opus-website blib/script/opus-website
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus-website
cp scripts/convert/opus2bitext blib/script/opus2bitext
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus2bitext
cp scripts/convert/opus2moses blib/script/opus2moses
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus2moses
cp scripts/convert/opus2multi blib/script/opus2multi
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus2multi
cp scripts/convert/opus2text blib/script/opus2text
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus2text
cp scripts/convert/opus2tmx blib/script/opus2tmx
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opus2tmx
cp scripts/admin/opusinfo-delete blib/script/opusinfo-delete
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opusinfo-delete
cp scripts/admin/opusinfo-refresh blib/script/opusinfo-refresh
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opusinfo-refresh
cp scripts/admin/opusinfo-set blib/script/opusinfo-set
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/opusinfo-set
cp scripts/convert/tmx2moses blib/script/tmx2moses
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/tmx2moses
cp scripts/convert/tmx2opus blib/script/tmx2opus
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/tmx2opus
cp scripts/convert/xml2opus blib/script/xml2opus
"/usr/bin/perl" "-Iinc" -MExtUtils::MY -e 'MY->fixin(shift)' -- blib/script/xml2opus
Manifying 14 pod documents
Manifying 1 pod document
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$
```

## make install

ပြီးရင်တော့ ```make install``` command ကို run ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ sudo make install
"/usr/bin/perl" "-Iinc" Makefile.PL --config= --installdeps=CGI,0,Lingua::Sentence,0,Ufal::UDPipe,0,XML::Writer,0
Manifying 14 pod documents
Manifying 1 pod document
Installing /usr/local/share/perl/5.30.3/OPUS/Tools.pm
Installing /usr/local/share/perl/5.30.3/OPUS/Tools/ISO639.pm
Installing /usr/local/man/man1/opus-udpipe.1p
Installing /usr/local/man/man1/tmx2moses.1p
Installing /usr/local/man/man1/opus2moses.1p
Installing /usr/local/man/man1/xml2opus.1p
Installing /usr/local/man/man1/opus2text.1p
Installing /usr/local/man/man1/bitext2tmx.1p
Installing /usr/local/man/man1/tmx2opus.1p
Installing /usr/local/man/man1/opus-index.1p
Installing /usr/local/man/man1/opus-read.1p
Installing /usr/local/man/man1/opus2multi.1p
Installing /usr/local/man/man1/opus2tmx.1p
Installing /usr/local/man/man1/opus-cat.1p
Installing /usr/local/man/man1/opus-swap-align.1p
Installing /usr/local/man/man1/moses2opus.1p
Installing /usr/local/man/man3/OPUS::Tools.3pm
Installing /usr/local/bin/opusinfo-delete
Installing /usr/local/bin/opus2bitext
Installing /usr/local/bin/opus-pt2dice
Installing /usr/local/bin/opus-split-align
Installing /usr/local/bin/opus2tmx
Installing /usr/local/bin/opus-index
Installing /usr/local/bin/xml2opus
Installing /usr/local/bin/opus-merge-align
Installing /usr/local/bin/tmx2moses
Installing /usr/local/bin/opusinfo-refresh
Installing /usr/local/bin/opus-cat
Installing /usr/local/bin/opus-pivoting
Installing /usr/local/bin/bitext2tmx
Installing /usr/local/bin/tmx2opus
Installing /usr/local/bin/opus-website
Installing /usr/local/bin/opus-read
Installing /usr/local/bin/opus-swap-align
Installing /usr/local/bin/opusinfo-set
Installing /usr/local/bin/opus-pt2dic
Installing /usr/local/bin/opus-iso639
Installing /usr/local/bin/opus-make-website
Installing /usr/local/bin/opus-udpipe
Installing /usr/local/bin/opus2multi
Installing /usr/local/bin/opus2moses
Installing /usr/local/bin/moses2opus
Installing /usr/local/bin/opus2text
Appending installation info to /usr/lib/x86_64-linux-gnu/perl/5.30/perllocal.pod
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$
```

## Check Scripts

tmx2moses ရှိတဲ့ ဖိုလ်ဒါအောက်ကို သွားရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ ls
blib  CHANGES  inc  lib  LICENSE  Makefile  Makefile.PL  MYMETA.json  MYMETA.yml  pm_to_blib  README.md  scripts  t  TODO
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl$ cd scripts/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts$ ls
admin  alignments  convert  multilingwis  opus-cat  opus-index  opus-read  opus-udpipe
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts$ cd convert/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ ls
bitext2tmx  moses2opus  opus2bitext  opus2moses  opus2multi  opus2text  opus2tmx  opus-iso639  text2utf8.pl  tmx2moses  tmx2opus  tmx2opus-new  xml2opus  xml2txt_simple.pl
```

tmx2moses: convert TMX files into aligned plain text files  
tmx2moses perl script နဲ့ convert လုပ်နိုင်တယ်လို့ ထင်တယ်။  
ကိုယ်ဖာ့သာကိုယ် script ရေးပြီး ပြောင်းလည်းရနိုင်ပေမဲ့... ရှိပြီးသား tool ကို သုံးတာကလည်း ကောင်းတဲ့အပိုင်းတွေအများကြီးရှိပါတယ်။  

## Converting tmx to moses

convert လုပ်ဖို့အတွက် example ဖိုင်တစ်ခုကိုဖန်တီးဖို့အတွက် [TMX wiki](https://en.wikipedia.org/wiki/Translation_Memory_eXchange) မှာပြထားတဲ့ example ကိုပဲ ယူလိုက်ပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ cat ./example.tmx
<tmx version="1.4">
  <header
    creationtool="XYZTool" creationtoolversion="1.01-023"
    datatype="PlainText" segtype="sentence"
    adminlang="en-us" srclang="en"
    o-tmf="ABCTransMem"/>
  <body>
    <tu>
      <tuv xml:lang="en">
        <seg>Hello world!</seg>
      </tuv>
      <tuv xml:lang="fr">
        <seg>Bonjour tout le monde!</seg>
      </tuv>
    </tu>
  </body>
</tmx>
```

convert လုပ်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ perl ./tmx2moses ./example.tmx 
```
convert လုပ်ပြီးသွားရင် အောက်ပါအတိုင်း example.tmx.en-fr.en ဖိုင်နဲ့ example.tmx.en-fr.fr ကို output လုပ်ပေးတာကို တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ ls
bitext2tmx   example.tmx.en-fr.en  moses2opus   opus2moses  opus2text  opus-iso639   tmx2moses  tmx2opus-new  xml2txt_simple.pl
example.tmx  example.tmx.en-fr.fr  opus2bitext  opus2multi  opus2tmx   text2utf8.pl  tmx2opus   xml2opus
```


```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ cat ./example.tmx.en-fr.en
Hello world!
```
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpusTools-perl/scripts/convert$ cat ./example.tmx.en-fr.fr
Bonjour tout le monde!
```

