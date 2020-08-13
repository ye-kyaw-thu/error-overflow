# pdftk ကို installation လုပ်ထားပေမဲ့ run လိုက်တဲ့အခါမှာ တက်တဲ့ error  

## Installation of Java lib for pdftk:

ကျွန်တော်ရဲ့ Github, tool/ repository ရဲ့ bash shell script တစ်ပုဒ်ဖြစ်တဲ့ split-even-odd.pdf ကို ကျောင်းသားတွေကို run ပြဖို့အတွက် pdftk ကို installation လုပ်ထားပေမဲ့ run တဲ့အခါမှာ အောက်ပါအတိုင်း error တက်ပါတယ်။   

```
(base) ye@ykt-pro:/media/ye/Transcend/yLab/intern-2/text-gen$ bash ./split-even-odd.pdf ./myanmarconstitution2008mm.pdf 
Total pages in your PDF file: 424
Error: Unexpected Exception in open_reader()
java.io.FileNotFoundException: ./myanmarconstitution2008mm.pdf (Permission denied)
   at gnu.java.nio.channels.FileChannelImpl.open(libgcj.so.16)
   at gnu.java.nio.channels.FileChannelImpl.<init>(libgcj.so.16)
   at gnu.java.nio.channels.FileChannelImpl.create(libgcj.so.16)
   at java.io.RandomAccessFile.<init>(libgcj.so.16)
   at pdftk.com.lowagie.text.pdf.RandomAccessFileOrArray.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PRTokeniser.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PdfReader.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PdfReader.<init>(pdftk)
Error: Failed to open PDF file: 
   ./myanmarconstitution2008mm.pdf
Errors encountered.  No output created.
Done.  Input errors, so no output created.
I/O Error: Couldn't open file 'odd.pdf': No such file or directory.
No. of pages of odd.pdf: 
Error: Unexpected Exception in open_reader()
java.io.FileNotFoundException: ./myanmarconstitution2008mm.pdf (Permission denied)
   at gnu.java.nio.channels.FileChannelImpl.open(libgcj.so.16)
   at gnu.java.nio.channels.FileChannelImpl.<init>(libgcj.so.16)
   at gnu.java.nio.channels.FileChannelImpl.create(libgcj.so.16)
   at java.io.RandomAccessFile.<init>(libgcj.so.16)
   at pdftk.com.lowagie.text.pdf.RandomAccessFileOrArray.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PRTokeniser.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PdfReader.<init>(pdftk)
   at pdftk.com.lowagie.text.pdf.PdfReader.<init>(pdftk)
Error: Failed to open PDF file: 
   ./myanmarconstitution2008mm.pdf
Errors encountered.  No output created.
Done.  Input errors, so no output created.
I/O Error: Couldn't open file 'even.pdf': No such file or directory.
No. of pages of even.pdf: 
```

## Solution

soft link ချိတ်ပေးလိုက်ရင် အဆင်ပြေသွားပါတယ်။ PDF ဖိုင်ထဲက စုံဂဏန်း စာမျက်နှာတွေကိုပါ print ထုပ်ပြီး သပ်သပ် PDF ဖိုင်အနေနဲ့သိမ်းပေးပါလိမ့်မယ်။ ထိုနည်းလည်းကောင်း မဂဏန်း စာမျက်နှာတွေကိုလည်း PDF ဖိုင်အနေနဲ့ သပ်သပ် သိမ်းပေးပါလိမ့မယ်။  

```
(base) ye@ykt-pro:/media/ye/Transcend/yLab/intern-2/text-gen$ sudo ln -s /snap/pdftk/current/usr/bin/pdftk /usr/bin/pdftk
```

## Reference

https://askubuntu.com/questions/1028522/how-can-i-install-pdftk-in-ubuntu-18-04-and-later
Ref link: https://stackoverflow.com/questions/50883270/unexpected-exception-in-open-reader
