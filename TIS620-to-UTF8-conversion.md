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

## Using thaiconv Converter

Googling လုပ်ရင်း နောက်ဆုံး သွားတွေ့တာက [thaiconv](http://www.lyndonhill.com/Projects/thaiconv.html) ဆိုတဲ့ ထိုင်းဖောင့်ကို UTF8 ပြောင်းပေးတဲ့ tool တစ်ခုပါ။  

Downloads/ ဖိုလ်ဒါအောက်ကနေ working directory ဆီကို move လုပ် tar command နဲ့ unzip လုပ်ပြီး ထွက်လာတဲ့ executable file ကို ls လုပ်ကြည့်ခဲ့တယ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus$ mv ~/Downloads/thaiconv-1_8-linux.tar.bz2 .
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus$ tar -xf ./thaiconv-1_8-linux.tar.bz2 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus$ ls
lexitron-corpus  LST20_Corpus  LST20_Corpus.zip  ReadMe.txt  thaiconv  thaiconv-1_8-linux.tar.bz2
```

Help screen ခေါ်ကြည့်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ../thaiconv -h
thaiconv v1.8
Thai text transcoding tool. Lyndon Hill (c) 2017.
Usage: thaiconv [-h] [-s] [-sq] [-in X] [-out Y] [-noent] [-bom] -r input_filename [-w output_filename]
  Input/Output Formats: 0 = TIS-620, 1 = UTF-8 Thai, 2 = HTML, 3 = UTF-8 Latin 1 (cross coded Thai)
For extended information please see
<http://www.lyndonhill.com/Projects/thaiconv.html>

Reference: http://www.lyndonhill.com/Projects/thaiconv.html
```

Conversion လုပ်ကြည့်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ../thaiconv -r ./etlex -out 1 > ./etlex.utf8 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ../thaiconv -r ./telex -out 1 > ./telex.utf8 
```

file command နဲ့ UTF-8 encoding ကို ပြောင်းသွားပြီလား ဆိုတာကို စစ်ကြည့်တော့ ပြောင်းပေးသွားတာကို အောက်ပါအတိုင်း တွေ့ရ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ file {etlex,telex}.utf8
etlex.utf8: UTF-8 Unicode text
telex.utf8: UTF-8 Unicode text
```

file အတွင်းက စာသားတွေကိုလည်း မျက်လုံးနဲ့ကြည့်ချင်လို့ head command နဲ့ ထိပ်ဆုံး ၁၀ကြောင်းကို ရိုက်ထုတ်ခိုင်းပြီး ကြည့်ခဲ့တော့ အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ conversion လုပ်ပေးသွားတာကို တွေ့ရ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./etlex.utf8 
<Doc>
<esearch>a</esearch>
<eentry>a</eentry>
<tentry>หนึ่ง (คำนำหน้าคำนามเพื่อแสดงว่าคำนามนั้นๆ ไม่ชี้เฉพาะ)</tentry>
<ecat>DET</ecat>
<id>0</id>
</Doc>
<Doc>
<esearch>A</esearch>
<eentry>A</eentry>
```

telex.utf8 ဖိုင်ကိုလည်း head command နဲ့ ရိုက်ကြည့်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./telex.utf8 
<Doc>
<tsearch>ดังกล่าวข้างต้น</tsearch>
<tentry>ดังกล่าวข้างต้น</tentry>
<eentry>abovementioned</eentry>
<tcat>PRON</tcat>
<tsyn>ดังกล่าว</tsyn>
<tsample>หน่วยงานของเราสามารถรับบทบาทได้เป็นอย่างดี ตามสภาพความพร้อมด้านต่างๆ ดังกล่าวข้างต้น</tsample>
<id>0</id>
</Doc>
<Doc>
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ 
```

converted License file also...  
ထိုင်းလိုရေးထားတဲ့ လိုင်စင်ဖိုင်ကိုလည်း UTF-8 အဖြစ် conversion လုပ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ ../thaiconv -r ./LICENSE-th.txt -out 1 > ./LICENSE-th.txt.utf8
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus$ head ./LICENSE-th.txt.utf8 
สงวนลิขสิทธิ์ พ.ศ. 2546 โดยศูนย์เทคโนโลยีอิเล็กทรอนิกส์และคอมพิวเตอร์แห่งชาติ
ข้อตกลงการอนุญาตใช้สิทธิ์ (LICENSE AGREEMENT)

ข้อตกลงการอนุญาตใช้สิทธิ์ หมายถึง ข้อตกลงทางกฎหมายระหว่างผู้ใช้และศูนย์ฯ 
กรุณาอ่านรายละเอียดของข้อตกลงนี้ก่อนเป็น "ผู้ใช้" เพื่อใช้ประโยชน์จากซอฟต์แวร์
พจนานุกรมอิเล็กทรอนิกส์นี้ สาระสำคัญของข้อตกลงการอนุญาตใช้สิทธิ์ฉบับนี้ประกอบด้วย 
ข้อความสงวนลิขสิทธิ์ (Copyright Notice) คำนิยาม (Definitions) การยอมรับข้อ
ตกลงการอนุญาตใช้สิทธิ์ (Acceptance of License Agreement) เงื่อนไขการใช้ 
(Terms of Use) และข้อสงวนสิทธิ์การรับประกัน (Disclaimer of Warranty) 
```

## Testing -s option of thaiconv

thaiconv ရဲ့ -s option (Scan input file and report on type.) ကိုလည်း စမ်းကြည့်ခဲ့။  
ဒီ -s option နဲ့ input-file ထဲမှာ ပါတဲ့ စာလုံးတွေရဲ့ encoding information ကို အသေးစိတ် သိနိုင်။  
အသုံးဝင်တဲ့ option တစ်ခုပါပဲ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus/tmp$ ../../thaiconv -s -r ./etlex
thaiconv Scan Report
--------------------

11844562	plain ASCII characters.
367717	extended ASCII characters.
885	UTF-8 multibyte characters in Thai range.
68794	UTF-8 multibyte characters in Latin range.
667623	UTF-8 multibyte characters not in Thai range.
12949581	Total characters.

File is probably Thai TIS-620
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus/tmp$ ../../thaiconv -s -r ./telex 
thaiconv Scan Report
--------------------

7566164	plain ASCII characters.
740059	extended ASCII characters.
3166	UTF-8 multibyte characters in Thai range.
153266	UTF-8 multibyte characters in Latin range.
1374960	UTF-8 multibyte characters not in Thai range.
9837615	Total characters.

File is probably Thai TIS-620
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/data/LST-Thai-corpus/lexitron-corpus/tmp$
```

