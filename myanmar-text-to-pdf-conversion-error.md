# Error of conversion Myanmar language text file into pdf file

ဒီ ပြဿနာက မြန်မာစာဖိုင်တွေကို ကိုင်တွယ်ပြီး လုပ်တဲ့ အခါမှာ ကြုံတွေ့ရတဲ့ ပြဿနာတွေ အထဲက တစ်ခုပါ။  
မြန်မာစာ ပါနေတဲ့ text ဖိုင်ကို pdf ဖိုင်ကို ပြောင်းတဲ့အခါမှာ မြန်မာစာလုံးတွေက pdf ဖိုင်မှာ မှန်မှန်ကန်ကန် ပြမပေးတာမျိုးကို  
ကြုံတွေတဲ့အခါမှာ အသုံးဝင်ပါလိမ့်မယ်။

pandoc က font တွေ printing ကိစ္စတွေအတွက် အရမ်းကို powerful ဖြစ်တဲ့ tool ဖြစ်ပါတယ်။
အခု ပြဿနာကိုလည်း pandoc နဲ့ ဖြေရှင်းလို့ရပါတယ်။  
သို့သော် option အနေနဲ့ --variable mainfont="Myanmar3" --latex-engine=xelatex ဆိုပြီး၊ ကိုယ်သုံးချင်တဲ့ ဖောင့်နာမည်နဲ့ xelatex engine ကို ပေးမှသာ အလုပ်လုပ်ပေးပါလိမ့်မယ်။  

ကျွန်တော်ကိုယ်တိုင် ပထမဆုံးအကြိမ် မြန်မာစာ စာကြောင်းတွေပါတဲ့ text ဖိုင်ကို pdf အဖြစ် ပြောင်းတဲ့ အခါမှာ ကြုံရတုန်းက ရေးထားခဲ့တဲ့ old log ဖိုင်ကို အခြေခံပြီးတော့ ပြန် run ပြထားတာဖြစ်လို့ pandoc အပြင် တခြား text to pdf ပြောင်းပေးနိုင်တဲ့ ပရိုဂရမ်တွေကိုလည်း မိတ်ဆက်ပြီးသားဖြစ်သွားပါလိမ့်မယ်။ တခြား ပရိုဂရမ်တွေရဲ့ option တွေကိုတော့ ကျွန်တော် အသေးစိတ် ပြန်စမ်းထားတာ မဟုတ်လို့ အချိန်ရတဲ့သူက စမ်းကြည့်ချင်တဲ့သူက သက်ဆိုင်ရာ ပရိုဂရမ်တွေရဲ့ option တွေကိုလေ့လာပြီး ကြိုးစားကြည့်ချင်လည်း ကြိုးစားကြည့်ပါ။  

# cat reply.txt

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ cat reply.txt
> Main difficulty is could not get enough language resources
> in Myanmar language. As I have to deal with unstructured social media data,
> it is challenging to apply with existing resources.
မြန်မာစာ သုတေသနအတွက် က လုပ်စရာတွေအများကြီးကျန်သေးတယ်။
မြန်မာတစ်နိုင်ငံလုံးမှာ တကယ်တမ်း မြန်မာစာ NLP အတွက်အချိန်ပေးပြီး လုပ်နိုင်တဲ့သူ၊
စနစ်တကျ လုပ်တဲ့ researcher အရေအတွက်က အရမ်းနည်းနေပါသေးတယ်။
```

# txt to pdf conversion with enscript and ps2pf

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ enscript ./reply.txt -p reply.ps
[ 1 page * 1 copy ] left in reply.ps
3 lines were wrapped
14 non-printable characters
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ ps2pdf ./reply.ps ./reply-conv-with-enscript.pdf
```

# confirm converted pdf file with evince:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ evince ./reply-conv-with-enscript.pdf 
```
[see reply-conv-with-enscript.pdf file](https://github.com/ye-kyaw-thu/error-overflow/blob/master/my-text2pdf-output/reply-conv-with-enscript.pdf)

# convert txt to pdf with pandoc
# Got error as follows:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ pandoc ./reply.txt -o ./reply-conv-with-pandoc.pdf
! Package inputenc Error: Unicode char မ (U+1019)
(inputenc)                not set up for use with LaTeX.

See the inputenc package documentation for explanation.
Type  H <return>  for immediate help.
 ...                                              
                                                  
l.56 ...ging to apply with existing resources. မ

Try running pandoc with --latex-engine=xelatex.
pandoc: Error producing PDF
```

# conversion looks OK if I used --latex-engine=xelatex

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ pandoc ./reply.txt -o ./reply-conv-with-pandoc.pdf --latex-engine=xelatex
```

# confirm converted pdf with evince:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ evince ./reply-conv-with-pandoc.pdf 
```
[See reply-conv-with-pandoc.pdf file](https://github.com/ye-kyaw-thu/error-overflow/blob/master/my-text2pdf-output/reply-conv-with-pandoc.pdf)

# convert txt to pdf with libreoffice

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ libreoffice --convert-to "pdf" ./reply.txt 

(soffice:28658): Gdk-WARNING **: gdk_window_set_icon_list: icons too large

(soffice:28658): Gdk-WARNING **: gdk_window_set_icon_list: icons too large
convert /home/lar/tool/perl/preparing/pdf2mytxt/github/reply.txt -> /home/lar/tool/perl/preparing/pdf2mytxt/github/reply.pdf using filter : writer_pdf_Export
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ ls
reply-conv-with-enscript.pdf  reply-conv-with-pandoc.pdf  reply.pdf  reply.ps  reply.txt
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ mv reply.pdf ./reply-conv-with-libreoffice.pdf
```

# confirm converted pdf file with evince:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ evince ./reply-conv-with-libreoffice.pdf 
```

# installation of cups-pdf

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/comment$ sudo apt-get install cups-pdf
[sudo] password for lar: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  printer-driver-cups-pdf
The following NEW packages will be installed:
  cups-pdf printer-driver-cups-pdf
0 upgraded, 2 newly installed, 0 to remove and 235 not upgraded.
Need to get 35.4 kB of archives.
After this operation, 160 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 printer-driver-cups-pdf amd64 2.6.1-21 [34.3 kB]
Get:2 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 cups-pdf amd64 2.6.1-21 [1,106 B]
Fetched 35.4 kB in 3s (10.2 kB/s)    
Selecting previously unselected package printer-driver-cups-pdf.
(Reading database ... 361754 files and directories currently installed.)
Preparing to unpack .../printer-driver-cups-pdf_2.6.1-21_amd64.deb ...
Unpacking printer-driver-cups-pdf (2.6.1-21) ...
Selecting previously unselected package cups-pdf.
Preparing to unpack .../cups-pdf_2.6.1-21_amd64.deb ...
Unpacking cups-pdf (2.6.1-21) ...
Processing triggers for cups (2.1.3-4ubuntu0.6) ...
Updating PPD files for cups-pdf ...
Setting up printer-driver-cups-pdf (2.6.1-21) ...
Setting up cups-pdf (2.6.1-21) ...
```

# conv txt to pdf with cupsfilter:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ cupsfilter ./reply.txt > ./reply-conv-with-cupsfilter.pdf
DEBUG: argv[0]="cupsfilter"
DEBUG: argv[1]="1"
DEBUG: argv[2]="lar"
DEBUG: argv[3]="reply.txt"
DEBUG: argv[4]="1"
DEBUG: argv[5]=""
DEBUG: argv[6]="./reply.txt"
DEBUG: envp[0]="<CFProcessPath>"
DEBUG: envp[1]="CONTENT_TYPE=text/plain"
DEBUG: envp[2]="CUPS_DATADIR=/usr/share/cups"
DEBUG: envp[3]="CUPS_FONTPATH=/usr/share/cups/fonts"
DEBUG: envp[4]="CUPS_SERVERBIN=/usr/lib/cups"
DEBUG: envp[5]="CUPS_SERVERROOT=/etc/cups"
DEBUG: envp[6]="LANG=en_US.UTF8"
DEBUG: envp[7]="PATH=/usr/lib/cups/filter:/usr/bin:/usr/sbin:/bin:/usr/bin"
DEBUG: envp[8]="PPD=/usr/share/cups/model/laserjet.ppd"
DEBUG: envp[9]="PRINTER_INFO=cupsfilter"
DEBUG: envp[10]="PRINTER_LOCATION=Unknown"
DEBUG: envp[11]="PRINTER=cupsfilter"
DEBUG: envp[12]="RIP_MAX_CACHE=128m"
DEBUG: envp[13]="USER=lar"
DEBUG: envp[14]="CHARSET=utf-8"
DEBUG: envp[15]="FINAL_CONTENT_TYPE=application/pdf"
INFO: texttopdf (PID 28981) started.
INFO: texttopdf (PID 28981) exited with no errors.
```

# No comment
Oh! NO ~!!!! my Myanmar language ...

# Trying with wkhtmltopdf:
# Installation of wkhtmltopdf:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/comment$ sudo apt-get install xvfb
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  xserver-common
The following NEW packages will be installed:
  xvfb
The following packages will be upgraded:
  xserver-common
1 upgraded, 1 newly installed, 0 to remove and 234 not upgraded.
Need to get 805 kB of archives.
After this operation, 2,249 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://jp.archive.ubuntu.com/ubuntu xenial-updates/main amd64 xserver-common all 2:1.18.4-0ubuntu0.8 [27.7 kB]
Get:2 http://jp.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 xvfb amd64 2:1.18.4-0ubuntu0.8 [777 kB]
Fetched 805 kB in 2s (317 kB/s)
(Reading database ... 361788 files and directories currently installed.)
Preparing to unpack .../xserver-common_2%3a1.18.4-0ubuntu0.8_all.deb ...
Unpacking xserver-common (2:1.18.4-0ubuntu0.8) over (2:1.18.4-0ubuntu0.7) ...
Selecting previously unselected package xvfb.
Preparing to unpack .../xvfb_2%3a1.18.4-0ubuntu0.8_amd64.deb ...
Unpacking xvfb (2:1.18.4-0ubuntu0.8) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up xserver-common (2:1.18.4-0ubuntu0.8) ...
Setting up xvfb (2:1.18.4-0ubuntu0.8) ...
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/comment$ sudo apt-get install wkhtmltopdf
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  wkhtmltopdf
0 upgraded, 1 newly installed, 0 to remove and 234 not upgraded.
Need to get 187 kB of archives.
After this operation, 1,001 kB of additional disk space will be used.
Get:1 http://jp.archive.ubuntu.com/ubuntu xenial/universe amd64 wkhtmltopdf amd64 0.12.2.4-1 [187 kB]
Fetched 187 kB in 0s (243 kB/s)     
Selecting previously unselected package wkhtmltopdf.
(Reading database ... 361795 files and directories currently installed.)
Preparing to unpack .../wkhtmltopdf_0.12.2.4-1_amd64.deb ...
Unpacking wkhtmltopdf (0.12.2.4-1) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up wkhtmltopdf (0.12.2.4-1) ...
lar@lar-air:~/tool/perl/preparing/pdf2myt
```

# conv txt to pdf with wkhtmltopdf

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ wkhtmltopdf ./reply.txt ./reply-conv-with-wkhtmltopdf.pdf
Loading page (1/2)
Printing pages (2/2)                                               
Done         
```

# confirm converted pdf file with evince:

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ evince ./reply-conv-with-wkhtmltopdf.pdf 
```

# convert txt to pdf with pandoc again
# *** for this time, I used --variable mainfont="Myanmar3" option

```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ pandoc --variable mainfont="Myanmar3" --latex-engine=xelatex ./reply.txt -o reply-conv-with-pandoc2.pdf
```

# confirm converted pdf file with evince:
```
lar@lar-air:~/tool/perl/preparing/pdf2mytxt/github$ evince ./reply-conv-with-pandoc2.pdf 
```

## YAEH!!!!   
I got PDF file with correct Myanmar sentences !!! :)

# Reference:

[https://stackoverflow.com/questions/18178084/pandoc-and-foreign-characters](https://stackoverflow.com/questions/18178084/pandoc-and-foreign-characters)  

