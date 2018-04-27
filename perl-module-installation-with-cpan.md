# How to install a perl module with cpan

# in English:

LIke many programming languages, perl programming also use external libraries or modules.  
When you need to install a perl module, don't forget to use *cpan* command line tool.  
It will interact with [The Comprehensive Perl Archive Network (CPAN)](https://www.cpan.org/) from the command line.  

# in Myanmar language:

perl ပရိုဂရမ်မင်း မှာလည်း တခြား ပရိုဂရမ်မင်း ဘာသာစကားတွေလိုပဲ ပြင်ပ library (သို့မဟုတ်) module တွေကို ခေါ်ပြီး သုံးပါတယ်။  
ကိုယ်run ချင်တဲ့ ပရိုဂရမ်ကအတွက် လိုအပ်တဲ့ perl module တွေကို installation လုပ်ချင်တဲ့ အခါမှာ cpan ဆိုတဲ့ commandline tool ကို သုံးပါတယ်။  
cpan နဲ့ ပတ်သက်ပြီး သုံးပုံသုံးနည်းကို အလွယ် မိတ်ဆက်ပါမယ်။  

## help for cpan 
Linux ရဲ့ ထုံးစံအတိုင်း cpan command နဲ့ ပတ်သတ်တဲ့ help (သို့) option တွေကို အသေးစိတ်ကြည့်ချင်ရင်

```bash
man cpan
```

## Usage example  
ဆိုကြပါစို့ ကျွန်တော်တို့က Image::BMP ဆိုတဲ့ perl module က ကိုယ်ရဲ့ စက်ထဲမှာ မရှိလို့ installation လုပ်ချင်ရင်အောက်ပါ အဆင့်တွေအတိုင်း လုပ်ဆောင်ပါတယ်။  
ဗဟုသုတအတွက် Image::BMP class ကို installation လုပ်ရတဲ့ အခါမှာ မြင်ရမဲ့ output တွေအားလုံးကို ဖော်ပြပါမယ်။  

ဥပမာ ./readBMP ဆိုတဲ့ ပရိုဂရမ်က Image::BMP module ကို ယူသုံးထားပြီး၊ အဲဒီ perl module က စက်ထဲမှာ မရှိရင် အောက်ပါအတိုင်း error message ပေးပါလိမ့်မယ်။  

```bash
$./readBMP 
Can't locate Image/BMP.pm in @INC (you may need to install the Image::BMP module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.22.1 /usr/local/share/perl/5.22.1 /usr/lib/x86_64-linux-gnu/perl5/5.22 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.22 /usr/share/perl/5.22 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base .) at ./readBMP line 12.
BEGIN failed--compilation aborted at ./readBMP line 12.
```

Installation လုပ်ဖို့အတွက် cpan command ကို command prompt မှာ ရိုက်ထည့်ပါ။  

```bash
lar@lar-air:~/experiment/image2sound/ref-source/imageEncode/imageEncode-0.7$ cpan
Loading internal null logger. Install Log::Log4perl for logging messages
Terminal does not support AddHistory.

cpan shell -- CPAN exploration and modules installation (v2.11)
Enter 'h' for help.
cpan[1]>
```


```bash
cpan[1]> install Image::BMP
Reading '/home/lar/.local/share/.cpan/Metadata'
  Database was generated on Thu, 12 Oct 2017 10:29:02 GMT
Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/home/lar/.local/share/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/02packages.details.txt.gz
Reading '/home/lar/.local/share/.cpan/sources/modules/02packages.details.txt.gz'
  Database was generated on Fri, 27 Apr 2018 09:54:20 GMT
.............
  New CPAN.pm version (v2.16) available.
  [Currently running version is v2.11]
  You might want to try
    install CPAN
    reload cpan
  to both upgrade CPAN.pm and run the new version without leaving
  the current session.


...............................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/03modlist.data.gz
Reading '/home/lar/.local/share/.cpan/sources/modules/03modlist.data.gz'
DONE
Writing /home/lar/.local/share/.cpan/Metadata
Running install for module 'Image::BMP'
Fetching with LWP:
http://www.cpan.org/authors/id/D/DA/DAVEOLA/Image/Image-BMP-1.19.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/D/DA/DAVEOLA/Image/CHECKSUMS
Checksum for /home/lar/.local/share/.cpan/sources/authors/id/D/DA/DAVEOLA/Image/Image-BMP-1.19.tar.gz ok
Scanning cache /home/lar/.local/share/.cpan/build for sizes
..............................................................--------------DONE
DEL(1/35): /home/lar/.local/share/.cpan/build/Module-Build-0.4224-BJBO2x 
DEL(2/35): /home/lar/.local/share/.cpan/build/Module-Runtime-0.015-YH9MOP 
DEL(3/35): /home/lar/.local/share/.cpan/build/Try-Tiny-0.28-iE3apo 
DEL(4/35): /home/lar/.local/share/.cpan/build/Test-Fatal-0.014-oZeATr 
DEL(5/35): /home/lar/.local/share/.cpan/build/Dist-CheckConflicts-0.11-V1u74E 
DEL(6/35): /home/lar/.local/share/.cpan/build/Test-Requires-0.10-DFfe8L 
DEL(7/35): /home/lar/.local/share/.cpan/build/Package-Stash-XS-0.28-imTqtT 
DEL(8/35): /home/lar/.local/share/.cpan/build/Test-Deep-1.127-Wnpedc 
DEL(9/35): /home/lar/.local/share/.cpan/build/CPAN-Meta-Check-0.014-eGTXS1 
DEL(10/35): /home/lar/.local/share/.cpan/build/Test-Needs-0.002005-zkWspd 
DEL(11/35): /home/lar/.local/share/.cpan/build/Module-Implementation-0.09-fPghl1 
DEL(12/35): /home/lar/.local/share/.cpan/build/Package-Stash-0.37-vMlAiD 
DEL(13/35): /home/lar/.local/share/.cpan/build/Class-Load-0.24-VLNBbq 
DEL(14/35): /home/lar/.local/share/.cpan/build/Sub-Install-0.928-FqFRfs 
DEL(15/35): /home/lar/.local/share/.cpan/build/Params-Util-1.07-02yI98 
DEL(16/35): /home/lar/.local/share/.cpan/build/Data-OptList-0.110-n0DBTN 
DEL(17/35): /home/lar/.local/share/.cpan/build/Class-Load-XS-0.10-QTaXgH 
DEL(18/35): /home/lar/.local/share/.cpan/build/MRO-Compat-0.13-u6vC7M 
DEL(19/35): /home/lar/.local/share/.cpan/build/Sub-Name-0.21-CQGSWq 
DEL(20/35): /home/lar/.local/share/.cpan/build/Scalar-List-Utils-1.49-LtK98P 
DEL(21/35): /home/lar/.local/share/.cpan/build/Module-Runtime-Conflicts-0.003-Rx9HJU 
DEL(22/35): /home/lar/.local/share/.cpan/build/Variable-Magic-0.61-cQEkuU 
DEL(23/35): /home/lar/.local/share/.cpan/build/Sub-Exporter-Progressive-0.001013-lEGBBl 
DEL(24/35): /home/lar/.local/share/.cpan/build/B-Hooks-EndOfScope-0.21-fuRwul 
DEL(25/35): /home/lar/.local/share/.cpan/build/namespace-clean-0.27-y4eFmW 
DEL(26/35): /home/lar/.local/share/.cpan/build/Test-Warnings-0.026-nQbOBW 
DEL(27/35): /home/lar/.local/share/.cpan/build/Sub-Exporter-0.987-hlVUDi 
DEL(28/35): /home/lar/.local/share/.cpan/build/Sub-Identify-0.14-mFTDrv 
DEL(29/35): /home/lar/.local/share/.cpan/build/File-pushd-1.014-iqkwyQ 
DEL(30/35): /home/lar/.local/share/.cpan/build/Test-CleanNamespaces-0.22-v3GM4f 
DEL(31/35): /home/lar/.local/share/.cpan/build/Devel-OverloadInfo-0.004-PCwf9g 
DEL(32/35): /home/lar/.local/share/.cpan/build/Package-DeprecationManager-0.17-Qegyqv 
DEL(33/35): /home/lar/.local/share/.cpan/build/Devel-GlobalDestruction-0.14-nXp2JL 
DEL(34/35): /home/lar/.local/share/.cpan/build/Devel-StackTrace-2.02-qNZ7Er 
DEL(35/35): /home/lar/.local/share/.cpan/build/Eval-Closure-0.14-V2wbGC 
Configuring D/DA/DAVEOLA/Image/Image-BMP-1.19.tar.gz with Makefile.PL
Generating a Unix-style Makefile
Writing Makefile for Image::BMP
Writing MYMETA.yml and MYMETA.json
  DAVEOLA/Image/Image-BMP-1.19.tar.gz
  /usr/bin/perl Makefile.PL INSTALLDIRS=site -- OK
Running make for D/DA/DAVEOLA/Image/Image-BMP-1.19.tar.gz
cp lib/Image/BMP.pm blib/lib/Image/BMP.pm
Manifying 1 pod document
  DAVEOLA/Image/Image-BMP-1.19.tar.gz
  /usr/bin/make -- OK
Running make test
No tests defined for Image::BMP extension.
  DAVEOLA/Image/Image-BMP-1.19.tar.gz
  /usr/bin/make test -- OK
Running make install
Manifying 1 pod document
Installing /usr/local/share/perl/5.22.1/Image/BMP.pm
Installing /usr/local/man/man3/Image::BMP.3pm
Appending installation info to /usr/local/lib/x86_64-linux-gnu/perl/5.22.1/perllocal.pod
  DAVEOLA/Image/Image-BMP-1.19.tar.gz
  sudo /usr/bin/make install  -- OK

cpan[2]> exit
Terminal does not support GetHistory.
Lockfile removed.

```
