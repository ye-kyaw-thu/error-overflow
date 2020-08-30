# HTK Make Error

HTK toolkit က (Automatic Speech Recognition) ASR field မှာ acoustic model ဆောက်ဖို့အတွက် တွင်တွင်ကျယ်ကျယ်သုံးခဲ့ကြတဲ့ traditional tool တစ်ခုဖြစ်ပါတယ်။  
လက်ရှိအချိန်အထိလည်း ASR လောကထဲကို ဝင်ကြမယ်ဆိုရင် မသိမဖြစ်တဲ့ modeling technique ပါပဲ။  
Internship ကျောင်းသားတစ်ချို့ကို လက်တွေ့လုပ်ပြဖို့ installation လုပ်တဲ့အခါမှာ make all အဆင့်မှာ အောက်ပါ error ကို တွေ့လို့ ဖြေရှင်းပုံဖြေရှင်းနည်းကို reference အဖြစ်အသုံးဝင်အောင် မှတ်သားထားတာပါ။  


(base) ye@ykt-pro:~/tool/htk$ ./configure --prefix=/usr/local မှာ ဘာပြဿနာမှ မရှိပဲ make all လုပ်တဲ့အခါမှာ အောက်ပါအတိုင်း Error ပေးတယ် ဆိုပါစို့...  

```
(base) ye@ykt-pro:~/tool/htk$ make all
(cd HTKTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HTKTools'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/ye/tool/htk/HTKTools'
(cd HLMTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HLMTools'
Makefile:77: *** missing separator (did you mean TAB instead of 8 spaces?).  Stop.
make[1]: Leaving directory '/home/ye/tool/htk/HLMTools'
Makefile:111: recipe for target 'hlmtools' failed
make: *** [hlmtools] Error 1
```

# Solution

HLMTools အောက်မှာရှိတဲ့ Makefile ကို အောက်ပါအတိုင်း ဝင်ပြင်ပေးလိုက်ပါ  

```
(base) ye@ykt-pro:~/tool/htk/HLMTools$ gedit Makefile

```

လိုင်းနံပါတ် 77 ရဲ့ ရှေ့ဆုံးမှာ space ဖြစ်နေတဲ့ နေရာကို <TAB> နဲ့ အစားထိုးပေးပါ။  

```
76 mkinstalldir:
77	if [ ! -d $(bindir) -a X_ = X_yes ] ; then mkdir -p $(bindir) ; fi

```

အထက်ပါအတိုင်း Makefile ကို ပြင်လိုက်ပြီးပြီဆိုရင်တော့ make all ကို run ရင် error မပေးတော့ပါဘူး :)  

```
(base) ye@ykt-pro:~/tool/htk$ make all
(cd HTKTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HTKTools'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/ye/tool/htk/HTKTools'
(cd HLMTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HLMTools'
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o Cluster -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  Cluster.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from Cluster.c:36:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
Cluster.c: In function ‘do_recovery’:
Cluster.c:870:4: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
    fgets(tmp, 256, file);
    ^~~~~~~~~~~~~~~~~~~~~
Cluster.c:874:4: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
    fgets(tmp, 256, file);
    ^~~~~~~~~~~~~~~~~~~~~
Cluster.c:887:4: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
    fgets(tmp, 256, file);
    ^~~~~~~~~~~~~~~~~~~~~
Cluster.c:896:4: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
    fgets(tmp, 256, file);
    ^~~~~~~~~~~~~~~~~~~~~
Cluster.c:906:4: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
    fgets(tmp, 256, file);
    ^~~~~~~~~~~~~~~~~~~~~
Cluster.c: In function ‘import_classmap’:
Cluster.c:1354:13: warning: ignoring return value of ‘fgets’, declared with attribute warn_unused_result [-Wunused-result]
             fgets(line, max_line_len, file);
             ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 Cluster /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o HLMCopy -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  HLMCopy.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from HLMCopy.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 HLMCopy /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LAdapt -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LAdapt.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LAdapt.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LAdapt /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LBuild -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LBuild.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LBuild.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LBuild /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LFoF -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LFoF.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LFoF.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LFoF /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LGCopy -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LGCopy.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LGCopy.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LGCopy /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LGList -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LGList.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LGList.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LGList /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LGPrep -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LGPrep.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LGPrep.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LGPrep /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LLink -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LLink.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LLink.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
LLink.c: In function ‘main’:
LLink.c:145:7: warning: ignoring return value of ‘fscanf’, declared with attribute warn_unused_result [-Wunused-result]
       fscanf(file, "Word|Class %20s", type);
       ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LLink.c:179:7: warning: ignoring return value of ‘fscanf’, declared with attribute warn_unused_result [-Wunused-result]
       fscanf(file, "Word|Class %20s\n", type);
       ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LLink /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LMerge -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LMerge.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from LMerge.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LMerge /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LNewMap -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LNewMap.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LNewMap.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LNewMap /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LNorm -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LNorm.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from LNorm.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LNorm /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LPlex -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LPlex.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from LPlex.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LPlex /usr/local/bin ; fi
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
/usr/local/bin/ccache-gcc -o LSubset -m32 -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="x86_64"' -g -O2 -I../HTKLib -I../HLMLib  LSubset.c ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -L/usr/X11R6/lib  ../HTKLib/HTKLib.a ../HLMLib/HLMLib.a -lm
In file included from /usr/include/bits/libc-header-start.h:33:0,
                 from /usr/include/stdio.h:27,
                 from ../HTKLib/HShell.h:40,
                 from LSubset.c:35:
/usr/include/features.h:184:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
 # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
   ^~~~~~~
if [ X_ = X_yes ] ; then /usr/bin/install -c -m 755 LSubset /usr/local/bin ; fi
make[1]: Leaving directory '/home/ye/tool/htk/HLMTools'
```

run make install  

```
(base) ye@ykt-pro:~/tool/htk$ sudo make install
(cd HTKTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HTKTools'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/ye/tool/htk/HTKTools'
(cd HTKTools && make install) \
|| case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HTKTools'
if [ ! -d /usr/local/bin ] ; then mkdir /usr/local/bin ; fi
for program in HSLab HBuild HCompV HCopy HDMan HERest HHEd HInit HLEd 	HList HLRescore HLStats HMMIRest HParse HQuant HRest HResults HSGen HSmooth HVite  ; do /usr/bin/install -c -m 755 ${program} /usr/local/bin ; done
make[1]: Leaving directory '/home/ye/tool/htk/HTKTools'
(cd HLMTools && make all) \
  || case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HLMTools'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/ye/tool/htk/HLMTools'
(cd HLMTools && make install) \
|| case "" in *k*) fail=yes;; *) exit 1;; esac;
make[1]: Entering directory '/home/ye/tool/htk/HLMTools'
if [ ! -d /usr/local/bin -a X_ = X_yes ] ; then mkdir -p /usr/local/bin ; fi
for program in Cluster HLMCopy LAdapt LBuild LFoF LGCopy LGList LGPrep LLink LMerge LNewMap LNorm LPlex LSubset  ; do /usr/bin/install -c -m 755 ${program} /usr/local/bin ; done
make[1]: Leaving directory '/home/ye/tool/htk/HLMTools'
(base) ye@ykt-pro:~/tool/htk$ ls
AUTHORS    config.guess  config.status  configure     env  HLMLib    HTK      HTKLib    HTKTools    LICENSE   Makefile.in
ChangeLog  config.log    config.sub     configure.ac  FAQ  HLMTools  HTKBook  HTKLVRec  install-sh  Makefile  README

```

### Reference:  

Ref:
http://www.voxforge.org/home/forums/message-boards/general-discussion/error-attempting-to-install-htk/8
gcc version error အတွက် က  
sudo apt-get install gcc-multilib g++-multilib

