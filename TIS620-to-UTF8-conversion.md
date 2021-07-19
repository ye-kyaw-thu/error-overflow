# TIS-620 to UTF-8 Conversion

သုတေသနအလုပ်ကိစ္စ တစ်ခုနဲ့ [Thai-English electronic dictionary (LEXiTRON)](https://lexitron.nectec.or.th/2009_1/index.php?q=lookup/form/submit) corpus ကို Linux ပေါ်မှာ သုံးဖို့ ပြင်တဲ့အခါမှာ နဂိုဖိုင်က ထိုင်းစာလုံးတွေက ဖတ်လို့ မရခဲ့ပါဘူး။  
အတွေ့အကြုံအရ သေချာတယ် Windows ပေါ်မှာ ပြင်ဆင်ခဲ့ကြတာမို့ encoding ကို UTF-8 ပြောင်းပေးလိုက်ရင် ရတယ်ဆိုတာ သိလို့ အမြဲတမ်း သုံးနေကြ iconv နဲ့ conversion ကို အမျိုးမျိုး လုပ်ကြည့်ခဲ့ပေမဲ့ အဆင်မပြေခဲ့ပါဘူး။  
အဲဒါနဲ့ အမျိုးမျိုး စမ်းကြည့်ပြီး နောက်ဆုံး [thaiconv](http://www.lyndonhill.com/Projects/thaiconv.html) လို့ခေါ်တဲ့ tool နဲ့ကျမှပဲ conversion က အဆင်ပြေသွားလို့ error log အနေနဲ့ တင်ပေးထားလိုက်တာပါ။  

အသုံးဝင်ပါလိမ့်မယ်။  

## Original Lexitron Files

Colleague ဆီကနေ ရလာတဲ့ LEXiTRON corpus ထဲမှာ ပါလာတဲ့ ဖိုင်တွေနဲ့ သူတို့ရဲ့ encoding တွေက အောက်ပါအတိုင်းပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ file *
etlex:             ISO-8859 text
lexitron-data.zip: Zip archive data, at least v2.0 to extract
LICENSE-th.txt:    ISO-8859 text, with CRLF line terminators
LICENSE.txt:       ASCII text, with CRLF line terminators
telex:             Non-ISO extended-ASCII text, with LF, NEL line terminators
```

## Conversion

### for etlex

etlex က ဖိုင်နာမည်ကနေ နားလည်တာက English-Thai အတွဲလို့။ အဲဒီဖိုင်ကို iconv နဲ့ Windows မှာ အသုံးများတဲ့ ISO-8859 နဲ့ convertion လုပ်ကြည့်တော့ အောက်ပါအတိုင်း ပြောင်းမပေးနိုင်တာကို တွေ့ရ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ iconv -f ISO-8859 ./etlex -t UTF-8 -o ./etlex.utf8
iconv: failed to start conversion processing

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ iconv -f ISO-8859-14 ./etlex -t UTF-8 -o ./etlex.utf8
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ file ./etlex.utf8 
./etlex.utf8: UTF-8 Unicode text
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./etlex.utf8 
<Doc>
<esearch>a</esearch>
<eentry>a</eentry>
<tentry>ËṗÖè§ (ĊÓṗÓËṗéÒĊÓṗÒÁàẅṪèÍáÊṀ§ÇèÒĊÓṗÒÁṗÑéṗæ äÁèẂÕéà©ẅÒŴ)</tentry>
<ecat>DET</ecat>
<id>0</id>
</Doc>
<Doc>
<esearch>A</esearch>
<eentry>A</eentry>
```

### for telex

telex ကတော့ Thai-English direction ဖြစ်ပါလိမ့်မယ်။ အဲဒီ telex ဖိုင်ကိုလည်း ပြောင်းကြည့်ခဲ့တာ အောက်ပါအတိုင်း အဆင်မပြေခဲ့ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ iconv -f ISO-8859-14 ./telex -t UTF-8 -o ./telex.utf8
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ file ./telex.utf8 
./telex.utf8: UTF-8 Unicode text, with LF, NEL line terminators
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./telex.utf8 
<Doc>
<tsearch>ṀÑ§ḂÅèÒÇḃéÒ§ṁéṗ</tsearch>
<tentry>ṀÑ§ḂÅèÒÇḃéÒ§ṁéṗ</tentry>
<eentry>abovementioned</eentry>
<tcat>PRON</tcat>
<tsyn>ṀÑ§ḂÅèÒÇ</tsyn>
<tsample>ËṗèÇÂ§ÒṗḃÍ§àÃÒÊÒÁÒÃ¶ÃÑẃẃṖẃÒṖäṀéàṠçṗÍÂèÒ§ṀÕ ṁÒÁÊÀÒẅĊÇÒÁẅÃéÍÁṀéÒṗṁèÒ§æ ṀÑ§ḂÅèÒÇḃéÒ§ṁéṗ</tsample>
<id>0</id>
</Doc>
<Doc>
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ 
```

အဆင်မပြေဘူး...   

## Googling and Try Again

Stackoverflow မှာ သုံးခဲ့ဖူးတဲ့ shell script ကို download လုပ်ပြီး original ဖိုင်ကို overwrite မလုပ်သွားအောင် mv line နေရာကို နည်းနည်းဝင်ပြင်ရေးပြီး အဲဒီ script ကိုသုံးပြီးလည်း ပြောင်းဖို့ ကြိုးစားခဲ့...  

Reference link: https://stackoverflow.com/questions/11316986/how-to-convert-iso8859-15-to-utf8 

I updated output filename as follows:  

```bash
#!/bin/bash
TO="UTF-8"; FILE=$1
FROM=$(file -i $FILE | cut -d'=' -f2)
if [[ $FROM = "binary" ]]; then
 echo "Skipping binary $FILE..."
 exit 0
fi
iconv -f $FROM -t $TO -o $FILE.tmp $FILE; ERROR=$?
if [[ $ERROR -eq 0 ]]; then
  echo "Converting $FILE..."
  mv -f $FILE.tmp $FILE.utf8
else
  echo "Error on $FILE"
fi
```

Run လုပ်ကြည့်ခဲ့တယ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ vi to-utf8.sh
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ chmod +x ./to-utf8.sh 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ./to-utf8.sh ./etlex
Converting ./etlex...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ./to-utf8.sh ./telex
iconv: failed to start conversion processing
Error on ./telex
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./etlex.utf8 
<Doc>
<esearch>a</esearch>
<eentry>a</eentry>
<tentry>Ë¹Öè§ (¤Ó¹ÓË¹éÒ¤Ó¹ÒÁà¾×èÍáÊ´§ÇèÒ¤Ó¹ÒÁ¹Ñé¹æ äÁèªÕéà©¾ÒÐ)</tentry>
<ecat>DET</ecat>
<id>0</id>
</Doc>
<Doc>
<esearch>A</esearch>
<eentry>A</eentry>
```

အဆင်မပြေဘူး...  
