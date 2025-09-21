# Small OCR Experiment

NICT မှာ အလုပ်လုပ်စဉ်က မြန်မာစာ OCR ကို train/test လုပ်ခဲ့တယ်။  
ပြီးတော့ Vichet နဲ့အတူ Tesseract ကို ခမာစာအတွက်လည်း စမ်းဖြစ်ခဲ့ကြသေးတယ်။  
2014/2015 တုန်းက၊ အဲဒီနာက်ပိုင်း ကိုယ်တိုင်မစမ်းဖြစ်ခဲ့တော့ဘူး။  

ဒီနေ့တော့ OCR အခြေအနေကို သိချင်တာနဲ့ coding/testing တချို့ လုပ်ဖြစ်ခဲ့။  
မြန်မာစာအပြင် multilingual OCR အခြေအနေကို လေ့လာဖြစ်။  

21 Sept 2025
y

## Library Installation

```
ye@lst-hpc3090:~/exp/ocr$ pip install pytesseract --break-system-packages
Defaulting to user installation because normal site-packages is not writeable
DEPRECATION: Loading egg at /home/ye/.local/lib/python3.12/site-packages/mmh3-5.2.0-py3.12-linux-x86_64.egg is deprecated. pip 24.3 will enforce this behaviour change. A possible replacement is to use pip for package installation.. Discussion can be found at https://github.com/pypa/pip/issues/12330
Collecting pytesseract
  Downloading pytesseract-0.3.13-py3-none-any.whl.metadata (11 kB)
Requirement already satisfied: packaging>=21.3 in /usr/lib/python3/dist-packages (from pytesseract) (24.0)
Requirement already satisfied: Pillow>=8.0.0 in /usr/lib/python3/dist-packages (from pytesseract) (10.2.0)
Downloading pytesseract-0.3.13-py3-none-any.whl (14 kB)
Installing collected packages: pytesseract
Successfully installed pytesseract-0.3.13
ye@lst-hpc3090:~/exp/ocr$
```

## Call Help

```
ye@lst-hpc3090:~/exp/ocr$ python ./ocr_tesseract.py --help
usage: ocr_tesseract.py [-h] [-i INPUT] [-o OUTPUT] [-l LANG] [--list-langs]

OCR tool using Tesseract locally

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input file (PNG, JPG, JPEG, TIFF, BMP, GIF, PDF)
  -o OUTPUT, --output OUTPUT
                        Output text file
  -l LANG, --lang LANG  Language code (check available codes with --list-langs)
  --list-langs          List all supported Tesseract languages and exit
ye@lst-hpc3090:~/exp/ocr$
```

## Testing without Installing Binary

```
ye@lst-hpc3090:~/exp/ocr$ time python ./ocr_tesseract.py --input ./img/th_pro_en_my.png  --lang mya --output ./th_pro_en_my.tx
t
Error running OCR: tesseract is not installed or it's not in your PATH. See README file for more information.

real    0m0.333s
user    0m2.813s
sys     0m0.045s
ye@lst-hpc3090:~/exp/ocr$
```

## Tesseract Installation

```
ye@lst-hpc3090:~/exp/ocr$ sudo apt install tesseract-ocr-all
...
...
...
Setting up tesseract-ocr-script-viet (1:4.1.0-2) ...
Setting up tesseract-ocr-kan (1:4.1.0-2) ...
Setting up tesseract-ocr-script-hans-vert (1:4.1.0-2) ...
Setting up tesseract-ocr-script-ethi (1:4.1.0-2) ...
Setting up tesseract-ocr-tir (1:4.1.0-2) ...
Setting up tesseract-ocr-sqi (1:4.1.0-2) ...
Setting up tesseract-ocr-osd (1:4.1.0-2) ...
Setting up tesseract-ocr-khm (1:4.1.0-2) ...
Setting up tesseract-ocr-eus (1:4.1.0-2) ...
Setting up tesseract-ocr-kor-vert (1:4.1.0-2) ...
Setting up tesseract-ocr-script-jpan-vert (1:4.1.0-2) ...
Setting up tesseract-ocr-hin (1:4.1.0-2) ...
Setting up tesseract-ocr-script-taml (1:4.1.0-2) ...
Setting up tesseract-ocr-mkd (1:4.1.0-2) ...
Setting up tesseract-ocr-rus (1:4.1.0-2) ...
Setting up tesseract-ocr-tgk (1:4.1.0-2) ...
Setting up tesseract-ocr-tel (1:4.1.0-2) ...
Setting up tesseract-ocr-script-telu (1:4.1.0-2) ...
Setting up tesseract-ocr-pus (1:4.1.0-2) ...
Setting up tesseract-ocr-script-hang-vert (1:4.1.0-2) ...
Setting up tesseract-ocr-frk (1:4.1.0-2) ...
Setting up tesseract-ocr-dzo (1:4.1.0-2) ...
Setting up tesseract-ocr-script-cher (1:4.1.0-2) ...
Setting up tesseract-ocr-srp-latn (1:4.1.0-2) ...
Setting up tesseract-ocr-aze (1:4.1.0-2) ...
Setting up tesseract-ocr (5.3.4-1build5) ...
Setting up tesseract-ocr-all (5.3.4-1build5) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libc-bin (2.39-0ubuntu8.5) ...
ye@lst-hpc3090:~/exp/ocr$
```

support လုပ်တဲ့ language အားလုံးကို install လုပ်ခဲ့တယ်။  
Japanese vertical OCR ပါ အပါအဝင်။  
 
```
ye@lst-hpc3090:~/exp/ocr$ time python ./ocr_tesseract.py --input ./img/th_pro_en_my.png  --lang mya --output ./th_pro_en_my.txt
[✓] OCR complete. Output saved to ./th_pro_en_my.txt

real    0m2.483s
user    0m5.284s
sys     0m1.817s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./th_pro_en_my.txt
  38  245 2683 ./th_pro_en_my.txt
ye@lst-hpc3090:~/exp/ocr$
```

## Check OCR Output

တကယ်က input လုပ်လိုက်တဲ့ image မှာက ထိုင်းစာ၊ ထိုင်းအသံထွက်နဲ့ အင်္ဂလိပ်စာနဲ့ မြန်မာစာ စာကြောင်းတွေ ပါဝင်တယ်။   
စုစုပေါင်း ၁၀ကြောင်းပါ။  

```
ร้านนี้มีการบริการที่เป็นกันเอง	raan ni mii gaan buri gaan tee bpen gan eng	This shop has friendly service.	ဒီဆိုင်မှာ ကိုယ်တိုင် ဝန်ဆောင်မှုရှိတယ်။
ร้านนี้มีการบริการลูกค้าดี	raan ni mii gaan buri gaan luuk khaa dee	This shop has good customer service.	ဒီဆိုင်မှာက ဖောရွေတဲ့ ဝန်ဆောင်မှုရှိတယ်။
ร้านนี้มีการส่งเสริมการขาย	raan ni mii gaan sǒng serm gaan kaai	This shop promotes sales.	ဒီဆိုင်က အရောင်းမြှင့်တင်ရေးလုပ်တယ်။
ร้านนี้มีการเสนอสินค้าพิเศษ	raan ni mii gaan sa nuua sin khaa phi sàet	This shop offers special products.	ဒီဆိုင်က အထူးထုတ်ကုန်တွေ ရောင်းပါတယ်။
ร้านนี้มีการเสนอสินค้าลดราคา	raan ni mii gaan sa nuua sin khaa loht raa kaa	This shop offers discounted products.	ဤဆိုင်သည် လျှော့စျေးဖြင့် ကုန်ပစ္စည်းများကို ပေးသည်။
ร้านนี้มีการเสนอสินค้าส่งเสริมการขาย	raan ni mii gaan sa nuua sin khaa sǒng serm gaan kaai	This shop offers sales promotions.	ဒီဆိုင်မှာ အရောင်းမြှင့်တင်ရေး အစီအစဉ်တွေရှိတယ်။
ร้านนี้มีการเสนอสินค้าใหม่	raan ni mii gaan sa nuua sin khaa mai	This shop offers new products.	ဒီဆိုင်က ထုတ်ကုန်သစ်တွေ တင်ပေးတယ်။
ร้านนี้มีบริการจัดส่ง	raan ni mii buri gaan jat song	This shop provides delivery service.	ဒီဆိုင်က ပို့ဆောင်ရေး ဝန်ဆောင်မှုပေးတယ်။
ร้านนี้มีโปรโมชั่นดี	raan ni mii promochn dee	This shop has good promotions.	ဒီဆိုင်မှာ ပရိုမိုးရှင်းကောင်းတွေရှိတယ်။
ร้านนี้มีโปรโมชั่นที่ดี	raan ni mii promochn tee dee	This shop has good promotions.	ဒီဆိုင်မှာ ကောင်းတဲ့ ပရိုမိုးရှင်းတွေ လုပ်နေတယ်။
```

ရေးထားတဲ့ ပိုင်သွန်ကုဒ်ရဲ့ OCR output က အောက်ပါအတိုင်းပါ။   

```
၂၇၂၅၀ ၅ ဒဒ ၉၈ - ၁111 - ဒဿ ~ ငေ . [၈၉ ၉၉၈၇ ၀ ၂44 . ၅၉ ၅ ၅ ၁၅ င ၂.
ဆိုင်မှာ - ကိုယ်တိုင် ဝန်ဆောင်မူရှိတယ်;

ကြး ၂၇ ၂၅၂၅ ၉ ၂၂၈၅၂ ၅၂၅ ၂၂၂၅၅၂ ၅၁၅ ၂၂၂၂၂ ၅၅၄ ၄၁၁ ၅၉ < ၉၉ ~ ၅၉၉၉ ၇၁၅

ဒဒေဗၢငင ငြ > ဒီဆိုင်မှာက င ဖောရွှေတဲ့ င ၀န်ဆောင်မူုရှိတယ်;

ကြ ၂ ၅ ၂ ၇ ၅ ၈၀ ၅၇ ၉၅ < ၈ ၁၈၅၅ ၂၂. ၁ တး
အရောင်းမြှင့်တင်ရေးလုပ်တယ်;

ခံစ ၄ရၤ႔႔႔ဂ7ၤမ|“ ၅၅၀၅1) ၅1 ဤ11 ဌာ ဒဝ 114 ၁17 ]ာ ရရ 1၀1 ဒဲ 15 ဒါဝၤာ ၀55၀ အဝင -
[၀1၀၀1 = . ဒီဆိုင်က : အထူးထုတ်ကုန်တွေ : ရောင်းပါတယ်;

ခစ ၄ရၤ႔႔~ရ~၅၈+၅၇ 11 ၅1 ဤ1 1 - ဝရ 5၈ 114၅ ၁17] ၈၀ ၀ အဝ ]ရရ ဤ) 1 ဒဝၤာ ၀55၀ 13၀၀7 း
[၀1၀၀1 = . > ဤဆိုင်သည် း လျှော့စျေးဖြင့် င် ကုန်ပစ္စည်းများကို - ပေးသည်;

ကြး ၂ ပာ ၇ ၅၂၅ ၂၈၅ ၂၂၈ ၅၄၂၅ ၁ ၂၂၉၂၉ ၂၇ ၅၅၁ ၁၉၇၅၉ ၁၁၅၂ ၅၉၂၂ ၂၃၄၈ ၂၂၁ ၂၅၉၂၅
၉ ၁ ၁ ၅၉၅၀၂၂ "ဒီဆိုင်မှာ : အရောင်းမြှင့်တင်ရေး : အစီအစဉ်တွေရှိတယ်;

၂ 1 ၂၂ ၂၂၅ ၂၅ ၈၅၂ ၅၅ ၁ ၂၂၂ ၂၂ ၂၂၉၅5 ၂၈၂ ၂၅၂ ၂၅၉၉ ၅ ၁ ၂ ၂၅၅၉ |
ဒီဆိုင်က င ထုတ်ကုန်သစ်တွေ င တင်ပေးတယ်!

ယ ၅ ၅၂၂ ၂ ၂၂၈ ၂ ၂၅ ၅ ၅ ၁၅၀၅၅ ၇ ပ ၂ ၂၅၂ ၂
ဆောင်ရေး င ၀န်ဆောင်မူပေးတယ်#

ခနခ ဒရ ၅1 1 1 ၀၅၀၅၀၀ ဝမ အဒ 5 55၈၀ ၈ ၄၀၀၀ [၅၈၀၈၀1 ၀ = . `” ဒီဆိုင်မှာ - ပရိုမိုးရှင်းကောင်းတွေရှိတယ်1
ခနခ ရဝ) ၅1 1 1 ၀၅၀၅၀၀ ဝ ဝဝ 1 5 51၀ 1၇၅5 ၀၀၀ ၂၀၅၈၀၅၅၀*1 ဝ . ဒီဆိုင်မှာ - ကောင်းတဲ့ -

ဌး

ယစ

မြး

. ဝ

ဝ္ဝ င့ ၃ င
ပရုမှုးရုငးတွေ လှုပနေတယၢ1

```

## Preparing Myanmar Text Only Image  

```
ဒီဆိုင်မှာ ကိုယ်တိုင် ဝန်ဆောင်မှုရှိတယ်။
ဒီဆိုင်မှာက ဖောရွေတဲ့ ဝန်ဆောင်မှုရှိတယ်။
ဒီဆိုင်က အရောင်းမြှင့်တင်ရေးလုပ်တယ်။
ဒီဆိုင်က အထူးထုတ်ကုန်တွေ ရောင်းပါတယ်။
ဤဆိုင်သည် လျှော့စျေးဖြင့် ကုန်ပစ္စည်းများကို ပေးသည်။
ဒီဆိုင်မှာ အရောင်းမြှင့်တင်ရေး အစီအစဉ်တွေရှိတယ်။
ဒီဆိုင်က ထုတ်ကုန်သစ်တွေ တင်ပေးတယ်။
ဒီဆိုင်က ပို့ဆောင်ရေး ဝန်ဆောင်မှုပေးတယ်။
ဒီဆိုင်မှာ ပရိုမိုးရှင်းကောင်းတွေရှိတယ်။
ဒီဆိုင်မှာ ကောင်းတဲ့ ပရိုမိုးရှင်းတွေ လုပ်နေတယ်။
```

အထက်ပါ စာကြောင်းတွေကို image အဖြစ်ပြောင်းပြီး စမ်းမယ်။  

```
ye@lst-hpc3090:~/exp/ocr$ ls img/
my_only.png  th_pro_en_my.png
ye@lst-hpc3090:~/exp/ocr$
```

## Testing with Myanmar Text Only

```
ye@lst-hpc3090:~/exp/ocr$ time python ./ocr_tesseract.py --input ./img/my_only.png  --lang mya --output ./my_only.txt
[✓] OCR complete. Output saved to ./my_only.txt

real    0m0.904s
user    0m3.519s
sys     0m0.552s
ye@lst-hpc3090:~/exp/ocr$
```

Let's check the OCR output:  

```
(ချူး ၂၃ ၂ ချြ ချ
င ကုယတုင င ဝနဆောငမူရုတယ,

ဂု

ဂို

င လူ င ငု င
က ဖောရွေတ့ ` ဝနဆောငမှုရုတယၢ#

ဂု

င င်းမြှင့် ဖျ
အရောငးမှုင္ဝငရေးလုပတယၢ

ဦး |
ဂ် ဂ် ဂ် ဂဲ
33၆5

မျ ်းပါ ချ
င အထူးထုတကုနတွေ င ရောငးပ | တယ
နဏ 1 င

ချြ င င္ည င္လ ဝ င္လ

ငသည င လျှော့စျေးဖြင့် င ကုနပစ္စညးများကု င ပေးသညၢ#
လျာ ဓ င္လ ဝ ချ

င အရောင်းမြှင့်တင်ရေး င အစအစဉဥတွေရုတယၢ,း

)၃ ဖစ
~
-ိ၀

ဖြူ

မျမျူ၂ျ င ချ

င ထုတကုနသစတွေ တငပေးတယၢ1]
ဝ င င္ည င ချ
င ပုဆောငရေး င ၀ဝနဆောငမူပေးတယၢ

၂၉၃ င ဖျား.
ပရုမှုးရူငးကောငးတွေရုတယၢ

ဂဂ ဂဂ ဒ္မာ ဂဂ ဂဂ

ယစ ယစ ယစ ယစ ယစ
-ဂီ၀-ီ၀-ပိ၀-ဂ၀-င၀
ဖြူ

ချြ ဝ္ဝ ငု ချ
- ကောငးတံ့ : ပရုမှးရူငးတွေ င လုပနေတယၢ

```

ရလဒ်က မကောင်းဘူး။  

## Make Claning Input

အထက်ပါ my_only.png ဖိုင်က Notepad++ မှာ ဖွင့်ထားတဲ့ မြန်မာစာကြောင်းတွေကို screenshot လုပ်ခဲ့တာ။ ဆိုတော့ space တွေကို dot တွေနဲ့ ပြနေတဲ့အပိုင်းတော့ ပါနေတယ်။
အဲဒါကို ဖျောက်ပြီး ထပ်စမ်းကြည့်မယ်။  

```
ye@lst-hpc3090:~/exp/ocr$ ls ./img/
my_only_clean.png  my_only.png  th_pro_en_my.png
ye@lst-hpc3090:~/exp/ocr$
```

my_only_clean.png ကတော့ Windows OS ရဲ့ default notepad program ပေါ်ကနေ screenshot လုပ်ထားတဲ့ပုံ။  

## OCR Testing with Clean Myanmar Only PNG File  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./ocr_tesseract.py --input ./img/my_only_clean.png  --lang mya --output ./my_only_clean.txt
[✓] OCR complete. Output saved to ./my_only_clean.txt

real    0m0.852s
user    0m3.440s
sys     0m0.466s
ye@lst-hpc3090:~/exp/ocr$
```

```
သည်

ဃျ

ဒိ

ဖ
ဒ ၇.
ွ တွံ ဇြ ဒ်ာ
ဝိ ်၁ ကီ
ဝာ ဝိ ပ မ
အ ၀၁ ၁
ဗပ ပာ ဟ
(၆ ဖဲ ဏ
ဂို ဇာ ဇြ ငိ
ဆိ ပပ် ဖဲ ဗပစ
ဝႆ ဠဌဏ္ဍက္မ္ခာ
မ ၂: ၅ ဓ္ဖာ
ဝဏ
ဇွီမ္ဂီ ဂိ ဂြံ
ဖိ ဇ္ဇ ဂိ

ပး
၉ ဂ ဂ္ဂိါ
ဒာ ဂိ ငိ ဝပ
ဗပ ဗပ ဗပ ၀၀
ဝဂ္ဂံ- ဝဂ္ဂဲ- ဝဂ္ဂဲ- ၂
ဖက ဇက ဝက င်ျ

၂

ဗျ

မျ
တယ

ဉ်

မျ
ဧီတယ1|

အစီအစဉ်တွေရှိတယ်1
မျ
မျ

ဓူဝပေ

၂

မျ
ငရေး
နသစတွေ တငဝဝေ
ဝန်ဆောင်

ငဲ့တ
နျ

လျ

ဓိ

မြှ
ရ

င္လ

ဓိ

လျ
လျ

မှာ အရောင

ခ

`

ဂ
က ပူ့ဆောငေ

၉၉၀ ထှတ်က့

နီလျ
ဆုင

တွေရှိတယ်!

ဓိ

လျ

းရှင်းကောင်

ဝ္ဝ
ဓု
ခ

မှာ ပရု

နတယ်

လျ
ခိတ္စေ လုပခေ

းရှင်

ဝ္ဝ
ပရိုမို

စ

လူ
ာ ကောငးတံ့

င်မှ

င
ဆု
ထ

ဓ္ဆ
၀

```

Oh! ပိုတောင်ဆိုးသွားသလိုပဲ။  အဆင်မပြေဘူး။  

## Check Suppoted Language List  

```
ye@lst-hpc3090:~/exp/ocr$ python ./ocr_tesseract.py --list-langs > lang_list.txt
```

```
Installed Tesseract languages:
  - afr
  - amh
  - ara
  - asm
  - aze
  - aze_cyrl
  - bel
  - ben
  - bod
  - bos
  - bre
  - bul
  - cat
  - ceb
  - ces
  - chi_sim
  - chi_sim_vert
  - chi_tra
  - chi_tra_vert
  - chr
  - cos
  - cym
  - dan
  - deu
  - div
  - dzo
  - ell
  - eng
  - enm
  - epo
  - est
  - eus
  - fao
  - fas
  - fil
  - fin
  - fra
  - frk
  - frm
  - fry
  - gla
  - gle
  - glg
  - grc
  - guj
  - hat
  - heb
  - hin
  - hrv
  - hun
  - hye
  - iku
  - ind
  - isl
  - ita
  - ita_old
  - jav
  - jpn
  - jpn_vert
  - kan
  - kat
  - kat_old
  - kaz
  - khm
  - kir
  - kmr
  - kor
  - kor_vert
  - lao
  - lat
  - lav
  - lit
  - ltz
  - mal
  - mar
  - mkd
  - mlt
  - mon
  - mri
  - msa
  - mya
  - nep
  - nld
  - nor
  - oci
  - ori
  - osd
  - pan
  - pol
  - por
  - pus
  - que
  - ron
  - rus
  - san
  - sin
  - slk
  - slv
  - snd
  - spa
  - spa_old
  - sqi
  - srp
  - srp_latn
  - sun
  - swa
  - swe
  - syr
  - tam
  - tat
  - tel
  - tgk
  - tha
  - tir
  - ton
  - tur
  - uig
  - ukr
  - urd
  - uzb
  - uzb_cyrl
  - vie
  - yid
  - yor

```

```
ye@lst-hpc3090:~/exp/ocr$ python ./ocr_tesseract.py --list-langs | wc
    125     251    1086
ye@lst-hpc3090:~/exp/ocr$
```

## Installing Google Cloud Vision Library

ကျောင်းသားတွေကလည်း Google Cloud Vision က ပိုကောင်းတယ်လို့ပြောကြလို့ စမ်းကြည့်ခဲ့...  

```
ye@lst-hpc3090:~/exp/ocr$ pip install google-cloud-vision --break-system-packages
...
...
...
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 160.8/160.8 kB 21.4 MB/s eta 0:00:00
Downloading google_auth-2.40.3-py2.py3-none-any.whl (216 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 216.1/216.1 kB 31.0 MB/s eta 0:00:00
Downloading proto_plus-1.26.1-py3-none-any.whl (50 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 50.2/50.2 kB 7.5 MB/s eta 0:00:00
Downloading cachetools-5.5.2-py3-none-any.whl (10 kB)
Downloading googleapis_common_protos-1.70.0-py3-none-any.whl (294 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 294.5/294.5 kB 20.5 MB/s eta 0:00:00
Downloading grpcio_status-1.75.0-py3-none-any.whl (14 kB)
Downloading protobuf-6.32.1-cp39-abi3-manylinux2014_x86_64.whl (322 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 322.0/322.0 kB 51.1 MB/s eta 0:00:00
Downloading grpcio-1.75.0-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (6.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.4/6.4 MB 55.4 MB/s eta 0:00:00
Downloading pyasn1_modules-0.4.2-py3-none-any.whl (181 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.3/181.3 kB 27.1 MB/s eta 0:00:00
Downloading rsa-4.9.1-py3-none-any.whl (34 kB)
Downloading pyasn1-0.6.1-py3-none-any.whl (83 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 83.1/83.1 kB 12.0 MB/s eta 0:00:00
Installing collected packages: pyasn1, protobuf, grpcio, cachetools, rsa, pyasn1-modules, proto-plus, googleapis-common-protos, grpcio-status, google-auth, google-api-core, google-cloud-vision
  Attempting uninstall: protobuf
    Found existing installation: protobuf 5.29.5
    Uninstalling protobuf-5.29.5:
      Successfully uninstalled protobuf-5.29.5
  Attempting uninstall: grpcio
    Found existing installation: grpcio 1.74.0
    Uninstalling grpcio-1.74.0:
      Successfully uninstalled grpcio-1.74.0
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow 2.19.0 requires protobuf!=4.21.0,!=4.21.1,!=4.21.2,!=4.21.3,!=4.21.4,!=4.21.5,<6.0.0dev,>=3.20.3, but you have protobuf 6.32.1 which is incompatible.
Successfully installed cachetools-5.5.2 google-api-core-2.25.1 google-auth-2.40.3 google-cloud-vision-3.10.2 googleapis-common-protos-1.70.0 grpcio-1.75.0 grpcio-status-1.75.0 proto-plus-1.26.1 protobuf-6.32.1 pyasn1-0.6.1 pyasn1-modules-0.4.2 rsa-4.9.1
ye@lst-hpc3090:~/exp/ocr$
```

## Call --help  

```
ye@lst-hpc3090:~/exp/ocr$ python ./ocr_tool.py --help
usage: ocr_tool.py [-h] -i INPUT -o OUTPUT [-l LANG [LANG ...]] -c CREDENTIALS

OCR tool using Google Cloud Vision API

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Path to input image or PDF file
  -o OUTPUT, --output OUTPUT
                        Path to save extracted text (.txt)
  -l LANG [LANG ...], --lang LANG [LANG ...]
                        Language hints (e.g. th km my vi lo)
  -c CREDENTIALS, --credentials CREDENTIALS
                        Path to Google Cloud service account JSON key
ye@lst-hpc3090:~/exp/ocr$
```

Account က card နဲ့ confirm လုပ်ရတာမို့ မြန်မာယူဇာတိုင်းအတွက်တော့ အဆင်မပြေနိုင်ဘူး။  
အဲဒါကြောင့် တခြား option ကို အရင်ဆုံး ထပ်ကြိုးစားကြည့်မယ်။

## Adding EasyOCR and PaddleOCR

EasyOCR နဲ့ PaddleOCR က free ရတာမို့လို့ အဲဒီနှစ်မျိုးနဲ့လည်း စမ်းကြည့်မယ်။  
အောက်ပါ library တွေတော့ လိုအပ်လိမ့်မယ်။  

```
# system packages
sudo apt update
sudo apt install -y poppler-utils tesseract-ocr

# python packages (in a venv)
python -m pip install --upgrade pip
pip install pillow pdf2image pytesseract easyocr
# paddlepaddle (CPU) + paddleocr:
python -m pip install paddlepaddle -i https://www.paddlepaddle.org.cn/packages/stable/cpu/
pip install paddleocr
```

ကိုယ့်စက်မှာက တချို့ ရှိပြီးသား...   

```
ye@lst-hpc3090:~/exp/ocr$ sudo apt install -y poppler-utils
[sudo] password for ye:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
poppler-utils is already the newest version (24.02.0-1ubuntu9.6).
poppler-utils set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 160 not upgraded.
ye@lst-hpc3090:~/exp/ocr$
```

pip ကိုလည်း update လုပ်။  

```
ye@lst-hpc3090:~/exp/ocr$ python -m pip install --upgrade pip --break-system-packages
Defaulting to user installation because normal site-packages is not writeable
DEPRECATION: Loading egg at /home/ye/.local/lib/python3.12/site-packages/mmh3-5.2.0-py3.12-linux-x86_64.egg is deprecated. pip 24.3 will enforce this behaviour change. A possible replacement is to use pip for package installation.. Discussion can be found at https://github.com/pypa/pip/issues/12330
Requirement already satisfied: pip in /usr/lib/python3/dist-packages (24.0)
Collecting pip
  Downloading pip-25.2-py3-none-any.whl.metadata (4.7 kB)
Downloading pip-25.2-py3-none-any.whl (1.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.8/1.8 MB 13.5 MB/s eta 0:00:00
Installing collected packages: pip
Successfully installed pip-25.2
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ pip install pillow easyocr --break-system-packages
...
...
...
      Successfully uninstalled nvidia-cuda-cupti-cu12-12.6.80
  Attempting uninstall: nvidia-cublas-cu12
    Found existing installation: nvidia-cublas-cu12 12.6.4.1
    Uninstalling nvidia-cublas-cu12-12.6.4.1:
      Successfully uninstalled nvidia-cublas-cu12-12.6.4.1
  Attempting uninstall: nvidia-cusparse-cu12
    Found existing installation: nvidia-cusparse-cu12 12.5.4.2
    Uninstalling nvidia-cusparse-cu12-12.5.4.2:
      Successfully uninstalled nvidia-cusparse-cu12-12.5.4.2
  Attempting uninstall: nvidia-cufft-cu12
    Found existing installation: nvidia-cufft-cu12 11.3.0.4
    Uninstalling nvidia-cufft-cu12-11.3.0.4:
      Successfully uninstalled nvidia-cufft-cu12-11.3.0.4
  Attempting uninstall: nvidia-cudnn-cu12
    Found existing installation: nvidia-cudnn-cu12 9.5.1.17
    Uninstalling nvidia-cudnn-cu12-9.5.1.17:
      Successfully uninstalled nvidia-cudnn-cu12-9.5.1.17
  Attempting uninstall: nvidia-cusolver-cu12
    Found existing installation: nvidia-cusolver-cu12 11.7.1.2
    Uninstalling nvidia-cusolver-cu12-11.7.1.2:
      Successfully uninstalled nvidia-cusolver-cu12-11.7.1.2
  Attempting uninstall: torch
    Found existing installation: torch 2.7.1
    Uninstalling torch-2.7.1:
      Successfully uninstalled torch-2.7.1
Successfully installed Shapely-2.1.1 easyocr-1.7.2 imageio-2.37.0 lazy-loader-0.4 ninja-1.13.0 nvidia-cublas-cu12-12.8.4.1 nvidia-cuda-cupti-cu12-12.8.90 nvidia-cuda-nvrtc-cu12-12.8.93 nvidia-cuda-runtime-cu12-12.8.90 nvidia-cudnn-cu12-9.10.2.21 nvidia-cufft-cu12-11.3.3.83 nvidia-cufile-cu12-1.13.1.3 nvidia-curand-cu12-10.3.9.90 nvidia-cusolver-cu12-11.7.3.90 nvidia-cusparse-cu12-12.5.8.93 nvidia-cusparselt-cu12-0.7.1 nvidia-nccl-cu12-2.27.3 nvidia-nvjitlink-cu12-12.8.93 nvidia-nvtx-cu12-12.8.90 opencv-python-headless-4.12.0.88 pyclipper-1.3.0.post6 python-bidi-0.6.6 scikit-image-0.25.2 tifffile-2025.9.20 torch-2.8.0 torchvision-0.23.0 triton-3.4.0
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python -m pip install paddlepaddle -i https://www.paddlepaddle.org.cn/packages/stable/cpu/ --break-system-packages
...
...
...
Collecting opt_einsum==3.3.0 (from paddlepaddle)
  Downloading https://paddle-whl.bj.bcebos.com/stable/cpu/opt-einsum/opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Requirement already satisfied: networkx in /home/ye/.local/lib/python3.12/site-packages (from paddlepaddle) (3.5)
Requirement already satisfied: typing_extensions in /home/ye/.local/lib/python3.12/site-packages (from paddlepaddle) (4.14.1)
Collecting safetensors>=0.6.0 (from paddlepaddle)
  Downloading https://paddle-whl.bj.bcebos.com/stable/cpu/safetensors/safetensors-0.6.2-cp38-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (485 kB)
Requirement already satisfied: anyio in /home/ye/.local/lib/python3.12/site-packages (from httpx->paddlepaddle) (4.9.0)
Requirement already satisfied: certifi in /usr/lib/python3/dist-packages (from httpx->paddlepaddle) (2023.11.17)
Requirement already satisfied: httpcore==1.* in /home/ye/.local/lib/python3.12/site-packages (from httpx->paddlepaddle) (1.0.9)
Requirement already satisfied: idna in /usr/lib/python3/dist-packages (from httpx->paddlepaddle) (3.6)
Requirement already satisfied: h11>=0.16 in /home/ye/.local/lib/python3.12/site-packages (from httpcore==1.*->httpx->paddlepaddle) (0.16.0)
Requirement already satisfied: sniffio>=1.1 in /home/ye/.local/lib/python3.12/site-packages (from anyio->httpx->paddlepaddle) (1.3.1)
Installing collected packages: safetensors, opt_einsum, paddlepaddle
  Attempting uninstall: safetensors
    Found existing installation: safetensors 0.5.3
    Uninstalling safetensors-0.5.3:
      Successfully uninstalled safetensors-0.5.3
  Attempting uninstall: opt_einsum
    Found existing installation: opt_einsum 3.4.0
    Uninstalling opt_einsum-3.4.0:
      Successfully uninstalled opt_einsum-3.4.0
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow 2.19.0 requires protobuf!=4.21.0,!=4.21.1,!=4.21.2,!=4.21.3,!=4.21.4,!=4.21.5,<6.0.0dev,>=3.20.3, but you have protobuf 6.32.1 which is incompatible.
Successfully installed opt_einsum-3.3.0 paddlepaddle-3.2.0 safetensors-0.6.2
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ pip install paddleocr --break-system-packages
...
...
...
Downloading opencv_contrib_python-4.10.0.84-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (68.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 68.7/68.7 MB 61.2 MB/s  0:00:01
Downloading aistudio_sdk-0.3.8-py3-none-any.whl (62 kB)
Downloading modelscope-1.30.0-py3-none-any.whl (5.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.9/5.9 MB 51.7 MB/s  0:00:00
Downloading pydantic-2.11.9-py3-none-any.whl (444 kB)
Downloading pydantic_core-2.33.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 50.1 MB/s  0:00:00
Downloading annotated_types-0.7.0-py3-none-any.whl (13 kB)
Downloading pypdfium2-4.30.0-py3-none-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.8/2.8 MB 58.9 MB/s  0:00:00
Downloading typing_inspection-0.4.1-py3-none-any.whl (14 kB)
Downloading bce_python_sdk-0.9.46-py3-none-any.whl (352 kB)
Downloading future-1.0.0-py3-none-any.whl (491 kB)
Downloading pycryptodome-3.23.0-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 55.6 MB/s  0:00:00
Downloading colorlog-6.9.0-py3-none-any.whl (11 kB)
Downloading imagesize-1.4.1-py2.py3-none-any.whl (8.8 kB)
Downloading prettytable-3.16.0-py3-none-any.whl (33 kB)
Downloading py_cpuinfo-9.0.0-py3-none-any.whl (22 kB)
Downloading ruamel.yaml-0.18.15-py3-none-any.whl (119 kB)
Downloading ruamel.yaml.clib-0.2.12-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (754 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 754.1/754.1 kB 59.3 MB/s  0:00:00
Downloading ujson-5.11.0-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (57 kB)
Installing collected packages: py-cpuinfo, ujson, typing-inspection, ruamel.yaml.clib, PyYAML, pypdfium2, pydantic-core, pycryptodome, prettytable, opencv-contrib-python, modelscope, imagesize, future, colorlog, annotated-types, ruamel.yaml, pydantic, bce-python-sdk, aistudio_sdk, paddlex, paddleocr
Successfully installed PyYAML-6.0.2 aistudio_sdk-0.3.8 annotated-types-0.7.0 bce-python-sdk-0.9.46 colorlog-6.9.0 future-1.0.0 imagesize-1.4.1 modelscope-1.30.0 opencv-contrib-python-4.10.0.84 paddleocr-3.2.0 paddlex-3.2.1 prettytable-3.16.0 py-cpuinfo-9.0.0 pycryptodome-3.23.0 pydantic-2.11.9 pydantic-core-2.33.2 pypdfium2-4.30.0 ruamel.yaml-0.18.15 ruamel.yaml.clib-0.2.12 typing-inspection-0.4.1 ujson-5.11.0
ye@lst-hpc3090:~/exp/ocr$
```

## Call --help for free_ocr_tool.py  

```
ye@lst-hpc3090:~/exp/ocr$ python ./free_ocr_tool.py --help
usage: free_ocr_tool.py [-h] [-i INPUT] [-o OUTPUT] [-e {tesseract,easyocr,paddleocr}] [-l LANG [LANG ...]] [-g] [--dpi DPI]
                        [--poppler-path POPPLER_PATH] [--list-langs]

Unified OCR tool: tesseract | easyocr | paddleocr (image + PDF support)

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input image or PDF file (png/jpg/tiff/pdf)
  -o OUTPUT, --output OUTPUT
                        Output text file (.txt)
  -e {tesseract,easyocr,paddleocr}, --engine {tesseract,easyocr,paddleocr}
                        OCR engine: tesseract | easyocr | paddleocr
  -l LANG [LANG ...], --lang LANG [LANG ...]
                        Language code(s). Examples: Tesseract: 'eng' 'tha' or 'eng+tha' via multiple values (we combine
                        them) EasyOCR: 'th' 'en' 'vi' (list). See EasyOCR list (jaided.ai) PaddleOCR: one code like 'en'
                        'th' 'vietnam' (see Paddle docs). Paddle typically requires one language/model per run.
  -g, --gpu             Enable GPU for EasyOCR/PaddleOCR (if supported & installed).
  --dpi DPI             DPI when converting PDF pages to images (default: 300).
  --poppler-path POPPLER_PATH
                        (Windows) path to poppler bin folder for pdf2image.
  --list-langs          List supported/installed languages (best-effort). Optionally add -e ENGINE to limit.
ye@lst-hpc3090:~/exp/ocr$
```

## Testing

```
ye@lst-hpc3090:~/exp/ocr$ time python ./free_ocr_tool.py --input ./img/my_only.png --engine tesseract --lang mya --output ./my_only.txt
[i] Processing page 1/1 with engine 'tesseract' ...
[✓] OCR complete — saved to ./my_only.txt

real    0m5.269s
user    0m8.254s
sys     0m0.724s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./free_ocr_tool.py --engine easyocr --list-langs

EasyOCR: installed (python package present). Supported language codes are listed at the EasyOCR demo/docs page.
Reference (official list): https://www.jaided.ai/easyocr/
ye@lst-hpc3090:~/exp/ocr$
```

```
Supported Languages

Language	Code Name
Abaza	abq
Adyghe	ady
Afrikaans	af
Angika	ang
Arabic	ar
Assamese	as
Avar	ava
Azerbaijani	az
Belarusian	be
Bulgarian	bg
Bihari	bh
Bhojpuri	bho
Bengali	bn
Bosnian	bs
Simplified Chinese	ch_sim
Traditional Chinese	ch_tra
Chechen	che
Czech	cs
Welsh	cy
Danish	da
Dargwa	dar
German	de
English	en
Spanish	es
Estonian	et
Persian (Farsi)	fa
French	fr
Irish	ga
Goan Konkani	gom
Hindi	hi
Croatian	hr
Hungarian	hu
Indonesian	id
Ingush	inh
Icelandic	is
Italian	it
Japanese	ja
Kabardian	kbd
Kannada	kn
Korean	ko
Kurdish	ku
Latin	la
Lak	lbe
Lezghian	lez
Lithuanian	lt
Latvian	lv
Magahi	mah
Maithili	mai
Maori	mi
Mongolian	mn
Marathi	mr
Malay	ms
Maltese	mt
Nepali	ne
Newari	new
Dutch	nl
Norwegian	no
Occitan	oc
Pali	pi
Polish	pl
Portuguese	pt
Romanian	ro
Russian	ru
Serbian (cyrillic)	rs_cyrillic
Serbian (latin)	rs_latin
Nagpuri	sck
Slovak	sk
Slovenian	sl
Albanian	sq
Swedish	sv
Swahili	sw
Tamil	ta
Tabassaran	tab
Telugu	te
Thai	th
Tajik	tjk
Tagalog	tl
Turkish	tr
Uyghur	ug
Ukranian	uk
Urdu	ur
Uzbek	uz
Vietnamese	vi
```

EasyOCR က မြန်မာစာကိုတော့ support မလုပ်ဘူး။  
30 free OCR operation ရတယ်။ အဲဒီထက် ပိုရင် ပိုက်ဆံပေးရမယ်။  

PaddleOCR support လုပ်တဲ့ ဘာသာစကားတွေက အောက်ပါအတိုင်း...  

```
ye@lst-hpc3090:~/exp/ocr$ python ./free_ocr_tool.py --engine paddleocr  --list-langs

PaddleOCR installed (python package present). PaddleOCR provides many language models (80+).
Note: PaddleOCR typically handles one language/model at a time (run per language).
See PaddleOCR multilingual docs for full list: https://paddlepaddle.github.io/PaddleOCR/
ye@lst-hpc3090:~/exp/ocr$
```

Multilingual OCR support  လုပ်တယ်။  
Paper:  

```
https://arxiv.org/abs/2507.05595  
```


GitHub:  

```
https://github.com/PaddlePaddle/PaddleOCR
```

အကြမ်း လေ့လာကြည့်သလောက် အောက်ပါ ဘာသာစကားတွေပဲ support လုပ်သလားလို့။ ကိုယ့်ဖာသာကိုယ် training လုပ်ဖို့ လိုအပ်လိမ့်မယ်။  

```
Single model supports five text types (Simplified Chinese, Traditional Chinese, English, Japanese, and Pinyin)  
```

Testing EasyOCR ... 

```
ye@lst-hpc3090:~/exp/ocr$ time python ./free_ocr_tool.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine easyocr --la
ng ch_sim --output ./zh_easyocr.txt
[i] Processing page 1/1 with engine 'easyocr' ...
Using CPU. Note: This module is much faster with a GPU.
Downloading recognition model, please wait. This may take several minutes depending upon your network connection.
Progress: |██████████████████████████████████████████████████| 100.0% Complete[✓] OCR complete — saved to ./zh_easyocr.txt

real    0m11.771s
user    0m20.086s
sys     0m2.968s
```

GPU သုံးပြီး run ကြည့်တော့ တဝက်လောက် ပိုမြန်တာတွေ့ရတယ်။  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./free_ocr_tool.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine easyocr --lang ch_sim --output ./zh_easyocr_gpu.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' ...
[✓] OCR complete — saved to ./zh_easyocr_gpu.txt

real    0m6.032s
user    0m8.785s
sys     0m0.571s
ye@lst-hpc3090:~/exp/ocr$
```

Check OCR result:  

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_easyocr.txt
--- PAGE 1 ---
街舞入戏;跨界融合创新爆点;  薪火新生;青年传承掀新热潮;  古今交融
数字赋能助新发展:近年来,
一股洋溢着青春气息的创新之风正吹拂着古老的梨园=
传统戏曲正以前所未有的开放姿态,拥抱新潮元素;探索
青春表达。
探索传统戏曲新叙事
(川剧高腔亮一嗓孑,
硬是幺不倒台;  古戏台上跳街舞;更是幺不倒台.
今年8月,重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》
将川剧的造型身段与街舞的动感节奏融合; 并注入地道的重庆方言说唱,
上演
了一场别开生面的川剧街舞。
'幺不倒台'
是川渝地区方言,在戏班里面是说角色演得好,观众不让你下台, 这是对演员的高度认
可。
重庆市川剧院院长沈铁梅说。
街舞-川剧真的很棒 !
"希望看到更多传统文化结合新元素;
迸发出新的生命力" .对此,
不少网友
给出了正面反馈=
4我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品。通过这些跨界作
品,
使观众有一个了解传统文化的新窗口。
重庆市川剧院青年演员万珉含说。
ye@lst-hpc3090:~/exp/ocr$
```

GPU နဲ့ run ထားတဲ့ output ကိုလည်း confirm လုပ်ခဲ့...  

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_easyocr_gpu.txt
--- PAGE 1 ---
街舞入戏;跨界融合创新爆点;  薪火新生;青年传承掀新热潮;  古今交融
数字赋能助新发展:近年来,
一股洋溢着青春气息的创新之风正吹拂着古老的梨园=
传统戏曲正以前所未有的开放姿态,拥抱新潮元素;探索
青春表达。
探索传统戏曲新叙事
川剧高腔亮一嗓子,
硬是幺不倒台;  古戏台上跳街舞;更是幺不倒台.
今年8月,重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》
将川剧的造型身段与街舞的动感节奏融合; 并注入地道的重庆方言说唱,
上演
了一场别开生面的川剧街舞。
'幺不倒台'
是川渝地区方言,在戏班里面是说角色演得好。观众不让你下台, 这是对演员的高度认
可。
重庆市川剧院院长沈铁梅说。
街舞-川剧真的很棒 !
"希望看到更多传统文化结合新元素;
迸发出新的生命力" .对此,
不少网友
给出了正面反馈=
《我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品。通过这些跨界作
品,
使观众有一个了解传统文化的新窗口。
重庆市川剧院青年演员万珉含说。
ye@lst-hpc3090:~/exp/ocr$
```

Original news က ဒီလင့်ကနေ ယူထားတာ။  

```
http://www.chinatoday.com.cn/zw2018/ly_4982/202509/t20250919_800415685.html
```

## Updated the Code

Tesseract ကို ဖြုတ်ပြီး EasyOCR နဲ့ PaddleOCR နှစ်ခုကိုပဲ ပေါင်းရေးမယ်။  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m30.523s
user    4m10.316s
sys     0m2.858s
ye@lst-hpc3090:~/exp/ocr$
```

blank OCR error. Debug the code and run again:  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
/home/ye/exp/ocr/./easy_paddle_ocr.py:57: DeprecationWarning: Please use `predict` instead.
  result = ocr.ocr(arr)
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m31.442s
user    4m10.252s
sys     0m2.868s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

Error ဆက်ရှိ။  
Debug လုပ် ထပ် run ...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
/home/ye/exp/ocr/./easy_paddle_ocr.py:55: DeprecationWarning: Please use `predict` instead.
  result = ocr.ocr(arr)   # or .predict(arr), both should work
[DEBUG] Could not save debug JSON: Object of type Font is not JSON serializable
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m33.946s
user    4m15.059s
sys     0m3.031s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
0 0 0 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

ရပြီ...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[DEBUG] Result type: <class 'list'>
[DEBUG] Result length: 1
[DEBUG] First element type: <class 'paddlex.inference.pipelines.ocr.result.OCRResult'>
[DEBUG] Extracted 15 text lines
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m32.009s
user    4m13.506s
sys     0m2.800s
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
 14  15 209 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

OCR output ကို စစ်ကြည်တော့...  

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_paddleocr.txt
input_path
page_index
doc_preprocessor_res
dt_polys
model_settings
text_det_params
text_type
text_rec_score_thresh
return_word_box
rec_texts
rec_scores
rec_polys
vis_fonts
textline_orientation_angles
rec_boxesye@lst-hpc3090:~/exp/ocr$
```

debug ပြန်လုပ် ထပ် test လုပ်ခဲ့...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[DEBUG] Result type: <class 'list'>
[DEBUG] Result length: 1
[DEBUG] First element type: <class 'paddlex.inference.pipelines.ocr.result.OCRResult'>
[DEBUG] Inspecting OCRResult attributes:
Connecting to https://paddle-model-ecology.bj.bcebos.com/paddlex/PaddleX3.0/fonts/simfang.ttf ...
Downloading simfang.ttf ...
[==================================================] 100.00%
Connecting to https://paddle-model-ecology.bj.bcebos.com/paddlex/PaddleX3.0/fonts/PingFang-SC-Regular.ttf ...
Downloading PingFang-SC-Regular.ttf ...
[==================================================] 100.00%
[DEBUG] Extracted 271 text lines
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m35.807s
user    4m14.850s
sys     0m2.864s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
 270  271 2447 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```
line က များတယ်။  

```
input
path
None
page
index
None
doc
preprocessor
res
input
path
None
page
index
None
input
img
array
dtype
uint
model
settings
use
doc
orientation
classify
True
use
doc
unwarping
True
angle
rot
img
array
dtype
uint
output
img
array
dtype
uint
polys
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
model
settings
use
doc
preprocessor
True
use
textline
orientation
False
text
det
params
limit
side
len
limit
type
min
thresh
max
side
limit
box
thresh
unclip
ratio
text
type
general
text
rec
score
thresh
return
word
box
False
rec
texts
街舞入戏
跨界融合创新爆点
薪火新生
青年传承掀新热潮
古今交融
数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园
传统戏曲正以前所未有的开放姿态
拥抱新潮元素
探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子
硬是幺不倒台
古戏台上跳街舞
更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品
幺不倒台
将川剧的造型身段与街舞的动感节奏融合
并注入地道的重庆方言说唱
上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言
在戏班里面是说角色演得好
观众不让你下台
这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素
进发出新的生命力
对此
不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品
通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说
rec
scores
rec
polys
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
array
dtype
int
vis
fonts
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
paddlex
utils
fonts
Font
object
textline
orientation
angles
rec
boxes
array
dtype
int
```

Debug ပြန်လုပ်...   

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[DEBUG] Extracted 288 text lines
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m31.343s
user    4m11.997s
sys     0m2.985s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
 287  288 2559 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
 287  288 2559 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
input
None
page
None
doc
input
None
page
None
input
255
255
255
255
255
255
255
255
uint8
model
use
True
use
True
rot
255
255
255
255
255
255
255
255
uint8
output
255
255
255
255
255
255
255
255
uint8
dt
34
34
32
int16
44
78
int16
87
119
int16
43
156
43
184
int16
53
221
53
250
int16
263
289
int16
303
330
int16
52
364
52
394
int16
408
435
int16
58
471
58
498
int16
510
537
int16
549
573
int16
model
use
True
use
False
text
limit
64
limit
max
4000
box
unclip
text
text
return
False
rec
街舞入戏
跨界融合创新爆点
薪火新生
青年传承掀新热潮
古今交融
数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园
传统戏曲正以前所未有的开放姿态
拥抱新潮元素
探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子
硬是幺不倒台
古戏台上跳街舞
更是幺不倒台
今年8月
重庆市川剧院与不齐
舞团合作推出作品
幺不倒台
将川剧的造型身段与街舞的动感节奏融合
并注入地道的重庆方言说唱
上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言
在戏班里面是说角色演得好
观众不让你下台
这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素
进发出新的生命力
对此
不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品
通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说
rec
9956104755401611
9957005977630615
9985746145248413
999476969242096
997307300567627
9979105591773987
9996168613433838
9938819408416748
9988461136817932
9856690168380737
999143123626709
9984830617904663
rec
34
34
32
int16
44
78
int16
87
119
int16
43
156
43
184
int16
53
221
53
250
int16
263
289
int16
303
330
int16
52
364
52
394
int16
408
435
int16
58
471
58
498
int16
510
537
int16
549
573
int16
vis
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
paddlex
utils
Font
object
at
0x745dd1569520
textline
rec
34
49
573
int16
```

Meta data ကို filter လုပ်တာထက် rec_texts ကို ယူလိုက်ရင် ရလိမ့်မယ်။  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[DEBUG] OCRResult attributes:
[DEBUG] Trying legacy API approach...
/home/ye/exp/ocr/./easy_paddle_ocr.py:127: DeprecationWarning: Please use `predict` instead.
  legacy_result = ocr.ocr(arr)
[DEBUG] Extracted 0 text lines
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m55.349s
user    8m6.810s
sys     0m4.857s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
 0  3 16 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
ye@lst-hpc3090:~/exp/ocr$ cat zh_paddleocr.txt
No text detectedye@lst-hpc3090:~/exp/ocr$
```

Debug and run again ...  

```
l_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[DEBUG] Result type: <class 'list'>
[DEBUG] Result length: 1
[DEBUG] Item 0 type: <class 'paddlex.inference.pipelines.ocr.result.OCRResult'>
[DEBUG] Item 0 attributes: ['_save_funcs', '_json_writer', '_rand_fn', '_img_writer']
[DEBUG] Item 0 string preview: {'input_path': None, 'page_index': None, 'doc_preprocessor_res': {'input_path': None, 'page_index': None, 'input_img': array([[[255, ..., 255],
        ...,
        [255, ..., 255]],

       ...,

   ...
[DEBUG] Found Chinese text in string: ['街舞入戏', '跨界融合创新爆点', '薪火新生']
[DEBUG] Extracted 42 text lines
[DEBUG] First 5 lines:
  1. 街舞入戏
  2. 跨界融合创新爆点
  3. 薪火新生
  4. 青年传承掀新热潮
  5. 古今交融
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m31.210s
user    4m9.758s
sys     0m2.885s
ye@lst-hpc3090:~/exp/ocr$
```

zh_paddleocr.txt file:  

```
街舞入戏
跨界融合创新爆点
薪火新生
青年传承掀新热潮
古今交融
数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园
传统戏曲正以前所未有的开放姿态
拥抱新潮元素
探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子
硬是幺不倒台
古戏台上跳街舞
更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品
幺不倒台
将川剧的造型身段与街舞的动感节奏融合
并注入地道的重庆方言说唱
上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言
在戏班里面是说角色演得好
观众不让你下台
这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素
进发出新的生命力
对此
不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品
通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说
```

## Testing with Updated Code  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt
[i] Processing page 1/1 with engine 'paddleocr' ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m35.416s
user    4m11.946s
sys     0m2.852s
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./zh_paddleocr.txt
  20   21 1154 ./zh_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

OCR ရလဒ်ကို ပြန်စစ်...  

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_paddleocr.txt
街舞入戏，跨界融合创新爆点；薪火新生，青年传承掀新热潮；古今交融，数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园。传统戏曲正以前所未有的开放姿态，拥抱新潮元素，探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子，硬是幺不倒台；古戏台上跳街舞，更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》，将川剧的造型身段与街舞的动感节奏融合，并注入地道的重庆方言说唱，上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言，在戏班里面是说角色演得好，观众不让你下台，这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素，进发出新的生命力
对此，不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品，通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说ye@lst-hpc3090:~/exp/ocr$
```

Testing with EasyOCR ...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine easyocr --
lang ch_sim --output ./zh_easyocr.txt
[i] Processing page 1/1 with engine 'easyocr' ...
Using CPU. Note: This module is much faster with a GPU.
[✓] OCR complete. Saved to ./zh_easyocr.txt

real    0m7.599s
user    0m19.760s
sys     0m2.770s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc zh_easyocr.txt
  25   33 1172 zh_easyocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_easyocr.txt
街舞入戏;跨界融合创新爆点;  薪火新生;青年传承掀新热潮;  古今交融
数字赋能助新发展:近年来,
一股洋溢着青春气息的创新之风正吹拂着古老的梨园=
传统戏曲正以前所未有的开放姿态,拥抱新潮元素;探索
青春表达。
探索传统戏曲新叙事
(川剧高腔亮一嗓孑,
硬是幺不倒台;  古戏台上跳街舞;更是幺不倒台.
今年8月,重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》
将川剧的造型身段与街舞的动感节奏融合; 并注入地道的重庆方言说唱,
上演
了一场别开生面的川剧街舞。
'幺不倒台'
是川渝地区方言,在戏班里面是说角色演得好,观众不让你下台, 这是对演员的高度认
可。
重庆市川剧院院长沈铁梅说。
街舞-川剧真的很棒 !
"希望看到更多传统文化结合新元素;
迸发出新的生命力" .对此,
不少网友
给出了正面反馈=
4我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品。通过这些跨界作
品,
使观众有一个了解传统文化的新窗口。
重庆市川剧院青年演员万珉含说。ye@lst-hpc3090:~/exp/ocr$
```

## Added --GPU Again

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --help
usage: easy_paddle_ocr.py [-h] [-i INPUT] [-o OUTPUT] [-e {easyocr,paddleocr}] [-l LANG [LANG ...]] [--gpu] [--list-langs]
                          [--engine-langs {easyocr,paddleocr}]

Free OCR tool using EasyOCR or PaddleOCR

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input image file (PNG, JPG, JPEG, TIFF, BMP, GIF)
  -o OUTPUT, --output OUTPUT
                        Output text file
  -e {easyocr,paddleocr}, --engine {easyocr,paddleocr}
                        OCR engine to use (easyocr or paddleocr)
  -l LANG [LANG ...], --lang LANG [LANG ...]
                        Language codes (EasyOCR: multiple codes, PaddleOCR: single code like 'ch')
  --gpu                 Use GPU for acceleration (if available)
  --list-langs          List supported languages for an engine
  --engine-langs {easyocr,paddleocr}
                        Specify engine for --list-langs
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --engine easyocr --lang ja --outp
ut ./ja_easyocr.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' (GPU: True) ...
Downloading recognition model, please wait. This may take several minutes depending upon your network connection.
Progress: |██████████████████████████████████████████████████| 100.0% Complete[✓] OCR complete. Saved to ./ja_easyocr.txt

real    0m9.490s
user    0m8.908s
sys     0m0.608s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ja_easyocr.txt
  18   32 1226 ja_easyocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ja_easyocr.txt
福島で女性がクマに糞われ大けが 山形では
目撃相次ぎ駆除も
2025年9月21日 15時02分
クマ被害
2日夕方 福島県喜多方市の墓地の 近くで除草作業をしていたフ0代の女性がクマに韓われ一
左腕や 左手首の骨を折る六けがをしました。
クマはそのまま逃げたとみられ一
警察が注意を呼びかけています。
また
山形県鶴岡市では:鶴岡駅近くにクマが現れ 獅友会に駆除されました。
警察によりますと2日午俊斗時半ごろ 福島県喜多方市山都町で「女性がクマに韓われ頭と腕
にけがをした」と消防を通じて通報がありました。
近くに住む70代の 女性が左腕や 左手首の骨を折る大けがをしていて 』送される際に意識は
あり 命に別状はないとみられるということです。
女性は夫とともに墓地に向かう道の除草作業をしていましたが 当時は夫と離れた場所で1人
で作業をしていたということです_
現場は山林に囲まれ住宅や農地がある地域で クマはそのまま逃げたとみられ一
警察が近く
住民に注意を呼びかけています。ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m30.908s
user    4m9.701s
sys     0m2.804s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_paddleocr.txt
街舞入戏，跨界融合创新爆点；薪火新生，青年传承掀新热潮；古今交融，数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园。传统戏曲正以前所未有的开放姿态，拥抱新潮元素，探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子，硬是幺不倒台；古戏台上跳街舞，更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》，将川剧的造型身段与街舞的动感节奏融合，并注入地道的重庆方言说唱，上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言，在戏班里面是说角色演得好，观众不让你下台，这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素，进发出新的生命力
对此，不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品，通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说ye@lst-hpc3090:~/exp/ocr$
```

paddleocr အင်ဂျင်နဲ့ပဲ ဂျပန်စာအတွက် စမ်းကြည့်...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --engine paddleocr --lang japan -
-output ./ja_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./ja_paddleocr.txt

real    0m31.237s
user    4m10.065s
sys     0m2.764s
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ./ja_paddleocr.txt
 0  3 16 ./ja_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
ye@lst-hpc3090:~/exp/ocr$ cat ja_paddleocr.txt
No text detectedye@lst-hpc3090:~/exp/ocr$
```

PaddleOCR က မော်ဒယ်တွေ ကို ညှိပေးဖို့ လိုအပ်တယ်။  
သူ့မှာ multilingual OCR model လည်း ရှိတယ်။  

## Code Updating  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --engine paddleocr --lang japan --output ./ja_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
[i] Using multilingual model for language: japan
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./ja_paddleocr.txt

real    0m32.793s
user    4m8.826s
sys     0m2.526s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc ja_paddleocr.txt
  22   23 1102 ja_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ja_paddleocr.txt
福島で女性がクマに襲われ大けが山形では
目撃相次駆除も
クマ被害
日夕方、福島県喜多方市の墓地の近
で除草作業していた
代の女性がマに襲われ
左腕や左手首の骨折る大けがしました
クマはそのまま逃げたとみられ、警察が注意を呼びかけています
山形県鶴岡市では
鶴岡駅近
にマが現れ、猟友会に駆除されました
警察こよますと
日午後
時半ごろ、福島喜多方市山都町
女性がマに襲われ頭と腕
こけがをしたと消防通じて通報がありました
に住む
代の女性が左腕や左手首の骨折る大けがをしいて、搬送され際に意識
あり、命にこ別状はないとみられるということです
女性は夫とともに墓地にこ向かう道の除草作業していましが、当時は夫と離れた場所
で作業をしていたということです
現場は山林にこ囲まれ住宅や農地がある地域で、クマはそのまま逃げたとみられ、警察が近
の住民に注意呼びかけていますye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --engine paddleocr --lang ch --output ./zh_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./zh_paddleocr.txt

real    0m31.216s
user    4m12.535s
sys     0m2.753s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_paddleocr.txt
街舞入戏，跨界融合创新爆点；薪火新生，青年传承掀新热潮；古今交融，数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园。传统戏曲正以前所未有的开放姿态，拥抱新潮元素，探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子，硬是幺不倒台；古戏台上跳街舞，更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》，将川剧的造型身段与街舞的动感节奏融合，并注入地道的重庆方言说唱，上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言，在戏班里面是说角色演得好，观众不让你下台，这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素，进发出新的生命力
对此，不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品，通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说ye@lst-hpc3090:~/exp/ocr$
```

Japan ကိုပဲ EasyOCR နဲ့ ထပ်စမ်း။  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --engine easyocr --lang ja --output ./ja_easyocr.txt
[i] Processing page 1/1 with engine 'easyocr' (GPU: False) ...
Using CPU. Note: This module is much faster with a GPU.
[✓] OCR complete. Saved to ./ja_easyocr.txt

real    0m7.564s
user    0m20.405s
sys     0m2.662s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./ja_easyocr.txt
福島で女性がクマに糞われ大けが 山形では
目撃相次ぎ駆除も
2025年9月21日 15時02分
クマ被害
2日夕方 福島県喜多方市の墓地の 近くで除草作業をしていたフ0代の女性がクマに韓われ一
左腕や 左手首の骨を折る六けがをしました。
クマはそのまま逃げたとみられ一
警察が注意を呼びかけています。
また
山形県鶴岡市では:鶴岡駅近くにクマが現れ 獅友会に駆除されました。
警察によりますと2日午俊斗時半ごろ 福島県喜多方市山都町で「女性がクマに韓われ頭と腕
にけがをした」と消防を通じて通報がありました。
近くに住む7代の 女性が左腕や 左手首の骨を折る大けがをしていて 投送される際に意識は
あり 命に別状はないとみられるということです。
女性は夫とともに墓地に向かう道の除草作業をしていましたが 当時は夫と離れた場所で1人
で作業をしていたということです_
現場は山林に囲まれ住宅や農地がある地域で クマはそのまま逃げたとみられ一
警察が近く
住民に注意を呼びかけています。ye@lst-hpc3090:~/exp/ocr$
```

## Preparing Multilingual Data

```

20日夕方、福島県喜多方市の墓地の近くで除草作業をしていた70代の女性がクマに襲われ、左腕や左手首の骨を折る大けがをしました。
Can NATO innovate fast enough to counter Russia’s growing drone threat?
义务教育阶段的孩子更让人牵挂。2025年4月，我发起“华阳星火助学计划”，通过社会募集资金改善村内优秀学生的学习条件。截至目前，已筹集超12万元，平均每月有1万元助学金定向帮扶优秀学生。
クマはそのまま逃げたとみられ、警察が注意を呼びかけています。
Days after the wail of air-raid sirens and the roar of NATO fighter jets punctuated a peaceful late-summer night in eastern Poland, the key question in Europe is not only whether Moscow deliberately sent nearly two dozen drones into NATO airspace, but what the military response reveals about the alliance’s long-term ability to deal with this growing threat.
ကျန်းမာအောင် နေပါ။ အိပ်ရေးဝအောင် အိပ်ပါ။
また、山形県鶴岡市ではJR鶴岡駅近くにクマが現れ、猟友会に駆除されました。
2024年元旦过后，我响应党组织号召，主动请缨，成为中国延安干部学院派驻四川省凉山彝族自治州越西县华阳村的第一书记。从繁华大都市到偏远小山村，从企业家之子到脱贫村第一书记，这样的身份转变，让不少人满心疑惑：这年轻人，是来做什么的？
GST काउंसिल की 56वीं मीटिंग में इस पर फैसला लिया गया था। वित्त मंत्री निर्मला सीतारमण ने 3 सितंबर को इसकी जानकारी दी। इस बदलाव से जुड़ी हर जरूरी जानकारी को 9 सवालों के जवाब में बता रहे हैं...

```

## Testing Multilingual with PaddleOCR  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine paddleocr --lang ml --
output ./multi_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
[i] Using multilingual model for language: ml
Traceback (most recent call last):
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 246, in <module>
    main()
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 242, in main
    process_file(args.input, args.output, args.engine, langs, args.gpu)
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 177, in process_file
    text = ocr_with_paddleocr_image(img, lang, use_gpu)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 83, in ocr_with_paddleocr_image
    ocr = PaddleOCR(**init_kwargs)
          ^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/.local/lib/python3.12/site-packages/paddleocr/_pipelines/ocr.py", line 107, in __init__
    raise ValueError(
ValueError: No models are available for the language 'ml' and OCR version None.

real    0m5.154s
user    0m7.575s
sys     0m0.237s
ye@lst-hpc3090:~/exp/ocr$
```

--lang option ဘာမှမပေး...  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine paddleocr --output ./m
ulti_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./multi_paddleocr.txt

real    0m40.079s
user    5m39.888s
sys     0m3.415s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ wc multi_paddleocr.txt
 21  22 707 multi_paddleocr.txt
ye@lst-hpc3090:~/exp/ocr$
```

ဘာမှမပေးရင် တရုတ်က default ...  

```
ye@lst-hpc3090:~/exp/ocr$ cat multi_paddleocr.txt
日夕方
福島県喜多方市
墓地
除草作業
女性
左腕
左手首
义务教育阶段的孩子更让人牵挂
我发起"华阳星火助学计划"，通过社会募集资金改善村内优秀学生的学习条件。截至
目前，已筹集超
万元，平均每月有
万元助学金定向帮扶优秀学生
警察
注意
山形県鶴岡市
鶴岡駅近
猟友会
駆除
年元旦过后，我响应党组织号召，主动请缨，成为中国延安干部学院派驻四川省凉山彝族自治州越西县华阳村的第一书记。从繁
华大都市到偏远小山村，从企业家之子到脱贫村第一书记，这样的身份转变
让不少人满心疑惑
这年轻人，是来做什么的ye@lst-hpc3090:~/exp/ocr$
```

## Updated  

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --list-langs paddleocr
PaddleOCR common language codes:
  ch
  en
  japan
  korean
  french
  german
  latin
  arabic
  cyrillic

Note: For Japanese, use 'japan', 'japanese', 'jp', or 'ja'
For multilingual documents, PaddleOCR automatically detects scripts
For full 80+ language support, see:
 https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.6/doc/doc_en/multi_languages_en.md
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --list-langs easyocr
Traceback (most recent call last):
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 181, in <module>
    main()
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 171, in main
    list_languages(args.list_langs)
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 131, in list_languages
    langs = easyocr.Reader.available_languages()
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AttributeError: type object 'Reader' has no attribute 'available_languages'
ye@lst-hpc3090:~/exp/ocr$
```

## Updated Code  

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --help
usage: easy_paddle_ocr.py [-h] [-i INPUT] [-o OUTPUT] [-e {easyocr,paddleocr}] [-l LANG [LANG ...]] [--gpu]
                          [--list-langs ENGINE]

Free OCR tool using EasyOCR or PaddleOCR

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input image file (PNG, JPG, JPEG, TIFF, BMP, GIF)
  -o OUTPUT, --output OUTPUT
                        Output text file
  -e {easyocr,paddleocr}, --engine {easyocr,paddleocr}
                        OCR engine to use (easyocr or paddleocr)
  -l LANG [LANG ...], --lang LANG [LANG ...]
                        Language codes (EasyOCR: multiple codes, PaddleOCR: single code like 'ch')
  --gpu                 Use GPU for acceleration (if available)
  --list-langs ENGINE   List supported languages for an engine (easyocr or paddleocr)
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python easy_paddle_ocr.py --list-langs paddleocr
PaddleOCR common language codes:
  ch
  en
  japan
  korean
  french
  german
  latin
  arabic
  cyrillic

Note: For Japanese, use 'japan', 'japanese', 'jp', or 'ja'
For multilingual documents, PaddleOCR automatically detects scripts
For full 80+ language support, see:
 https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.6/doc/doc_en/multi_languages_en.md
ye@lst-hpc3090:~/exp/ocr$
```

```
EasyOCR supported languages:
  abq
  ad
  af
  ang
  ar
  as
  ava
  az
  be
  bg
  bh
  bho
  bn
  bs
  ch_sim
  ch_tra
  che
  cs
  cy
  da
  dar
  de
  en
  es
  et
  fa
  fr
  ga
  gom
  hi
  hr
  hu
  id
  inh
  is
  it
  ja
  kbd
  kn
  ko
  ku
  la
  lbe
  lez
  lt
  lv
  mah
  mai
  mi
  mn
  mr
  ms
  mt
  ne
  new
  nl
  no
  oc
  pi
  pl
  pt
  ro
  rs_cyrillic
  rs_latin
  ru
  sck
  sk
  sl
  sq
  sv
  sw
  ta
  tab
  te
  th
  tjk
  tl
  tr
  ug
  uk
  ur
  uz
  vi

Example: -l en ch_sim ja (for multiple languages)

```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine paddleocr --lang ml --
output ./multi_paddleocr.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
[i] Using multilingual model for mixed language document
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./multi_paddleocr.txt

real    0m40.275s
user    5m41.133s
sys     0m3.590s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --lang ja --engine paddleocr --output ja.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ja.txt

real    0m31.827s
user    4m8.460s
sys     0m2.640s
ye@lst-hpc3090:~/exp/ocr$
```

## Error Fixing  

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --lang ja --engine paddleocr --output ja.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ja.txt

real    0m31.183s
user    4m9.163s
sys     0m2.769s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./ja.txt
福島で女性がクマに襲われ大けが山形では
目撃相次駆除も
クマ被害
日夕方、福島県喜多方市の墓地の近
で除草作業していた
代の女性がマに襲われ
左腕や左手首の骨折る大けがしました
クマはそのまま逃げたとみられ、警察が注意を呼びかけています
山形県鶴岡市では
鶴岡駅近
にマが現れ、猟友会に駆除されました
警察こよますと
日午後
時半ごろ、福島喜多方市山都町
女性がマに襲われ頭と腕
こけがをしたと消防通じて通報がありました
に住む
代の女性が左腕や左手首の骨折る大けがをしいて、搬送され際に意識
あり、命にこ別状はないとみられるということです
女性は夫とともに墓地にこ向かう道の除草作業していましが、当時は夫と離れた場所
で作業をしていたということです
現場は山林にこ囲まれ住宅や農地がある地域で、クマはそのまま逃げたとみられ、警察が近
の住民に注意呼びかけていますye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --lang zh --engine
paddleocr --output ./zh.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./zh.txt

real    0m31.158s
user    4m11.738s
sys     0m2.943s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat ./zh.txt
街舞入戏，跨界融合创新爆点；薪火新生，青年传承掀新热潮；古今交融，数字赋能助新发展
近年来
一股洋溢着青春气息的创新之风正吹拂着古老的梨园。传统戏曲正以前所未有的开放姿态，拥抱新潮元素，探索
青春表达
探索传统戏曲新叙事
川剧高腔亮一嗓子，硬是幺不倒台；古戏台上跳街舞，更是幺不倒台
今年
重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》，将川剧的造型身段与街舞的动感节奏融合，并注入地道的重庆方言说唱，上演
了一场别开生面的川剧街舞
幺不倒台
是川渝地区方言，在戏班里面是说角色演得好，观众不让你下台，这是对演员的高度认
重庆市川剧院院长沈铁梅说
街舞
川剧真的很棒
希望看到更多传统文化结合新元素，进发出新的生命力
对此，不少网友
给出了正面反馈
我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品，通过这些跨界作
使观众有一个了解传统文化的新窗口
重庆市川剧院青年演员万玥含说ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/zh_from_ChinaToday_21Sept2025.png --lang ch_sim --eng
ine easyocr --output ./zh_easy.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' (GPU: True) ...
[✓] OCR complete. Saved to ./zh_easy.txt

real    0m6.368s
user    0m8.954s
sys     0m0.525s
ye@lst-hpc3090:~/exp/ocr$
ye@lst-hpc3090:~/exp/ocr$ cat ./zh_easy.txt
街舞入戏;跨界融合创新爆点;  薪火新生;青年传承掀新热潮;  古今交融
数字赋能助新发展:近年来,
一股洋溢着青春气息的创新之风正吹拂着古老的梨园=
传统戏曲正以前所未有的开放姿态,拥抱新潮元素;探索
青春表达。
探索传统戏曲新叙事
川剧高腔亮一嗓子,
硬是幺不倒台;  古戏台上跳街舞;更是幺不倒台.
今年8月,重庆市川剧院与不齐
舞团合作推出作品《幺不倒台》
将川剧的造型身段与街舞的动感节奏融合; 并注入地道的重庆方言说唱,
上演
了一场别开生面的川剧街舞。
'幺不倒台'
是川渝地区方言,在戏班里面是说角色演得好。观众不让你下台, 这是对演员的高度认
可。
重庆市川剧院院长沈铁梅说。
街舞-川剧真的很棒 !
"希望看到更多传统文化结合新元素;
迸发出新的生命力" .对此,
不少网友
给出了正面反馈=
《我希望我们以后能够更多地创造出一些传统文化和潮流文化相结合的作品。通过这些跨界作
品,
使观众有一个了解传统文化的新窗口。
重庆市川剧院青年演员万珉含说。ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/nhk_21Sept_2025.png --lang ja --engine easyocr --outp
ut ./ja_easy.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' (GPU: True) ...
[✓] OCR complete. Saved to ./ja_easy.txt

real    0m6.154s
user    0m8.791s
sys     0m0.531s
ye@lst-hpc3090:~/exp/ocr$
ye@lst-hpc3090:~/exp/ocr$ cat ja_easy.txt
福島で女性がクマに糞われ大けが 山形では
目撃相次ぎ駆除も
2025年9月21日 15時02分
クマ被害
2日夕方 福島県喜多方市の墓地の 近くで除草作業をしていたフ0代の女性がクマに韓われ一
左腕や 左手首の骨を折る六けがをしました。
クマはそのまま逃げたとみられ一
警察が注意を呼びかけています。
また
山形県鶴岡市では:鶴岡駅近くにクマが現れ 獅友会に駆除されました。
警察によりますと2日午俊斗時半ごろ 福島県喜多方市山都町で「女性がクマに韓われ頭と腕
にけがをした」と消防を通じて通報がありました。
近くに住む70代の 女性が左腕や 左手首の骨を折る大けがをしていて 』送される際に意識は
あり 命に別状はないとみられるということです。
女性は夫とともに墓地に向かう道の除草作業をしていましたが 当時は夫と離れた場所で1人
で作業をしていたということです_
現場は山林に囲まれ住宅や農地がある地域で クマはそのまま逃げたとみられ一
警察が近く
住民に注意を呼びかけています。ye@lst-hpc3090:~/exp/ocr$
```

## Testing for Multilingual   

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --lang ml --engine paddleocr --
output ./mutilingual.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
Traceback (most recent call last):
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 231, in <module>
    main()
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 227, in main
    process_file(args.input, args.output, args.engine, langs, args.gpu)
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 151, in process_file
    text = ocr_with_paddleocr_image(img, lang, use_gpu)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 67, in ocr_with_paddleocr_image
    ocr = PaddleOCR(**init_kwargs)
          ^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/.local/lib/python3.12/site-packages/paddleocr/_pipelines/ocr.py", line 107, in __init__
    raise ValueError(
ValueError: No models are available for the language 'ml' and OCR version None.

real    0m4.861s
user    0m7.569s
sys     0m0.257s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ time python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine paddleocr --output ./m
utilingual.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./mutilingual.txt

real    0m40.221s
user    5m40.837s
sys     0m3.421s
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --help
usage: easy_paddle_ocr.py [-h] [-i INPUT] [-o OUTPUT] [-e {easyocr,paddleocr}] [-l LANG [LANG ...]] [--gpu]
                          [--list-langs ENGINE]

Free OCR tool using EasyOCR or PaddleOCR

options:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input image file (PNG, JPG, JPEG, TIFF, BMP, GIF)
  -o OUTPUT, --output OUTPUT
                        Output text file
  -e {easyocr,paddleocr}, --engine {easyocr,paddleocr}
                        OCR engine to use (easyocr or paddleocr)
  -l LANG [LANG ...], --lang LANG [LANG ...]
                        Language codes (EasyOCR: multiple codes, PaddleOCR: single code like 'ch')
  --gpu                 Use GPU for acceleration (if available)
  --list-langs ENGINE   List supported languages for an engine (easyocr or paddleocr)
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --list-langs paddleocr
PaddleOCR common language codes:
  ch
  en
  japan
  korean
  french
  german
  latin
  arabic
  cyrillic

Note: For Japanese, use 'japan', 'japanese', 'jp', or 'ja'
For multilingual documents, PaddleOCR automatically detects scripts
For full 80+ language support, see:
 https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.6/doc/doc_en/multi_languages_en.md
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --list-langs easyocr
...
...
...
  new
  nl
  no
  oc
  pi
  pl
  pt
  ro
  rs_cyrillic
  rs_latin
  ru
  sck
  sk
  sl
  sq
  sv
  sw
  ta
  tab
  te
  th
  tjk
  tl
  tr
  ug
  uk
  ur
  uz
  vi

Example: -l en ch_sim ja (for multiple languages)
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine paddleocr --lang ml --output ./multilingual_paddle.txt --gpu
[i] Processing page 1/1 with engine 'paddleocr' (GPU: True) ...
[i] Using multilingual mode (Chinese base model)
/home/ye/.local/lib/python3.12/site-packages/paddle/utils/cpp_extension/extension_utils.py:718: UserWarning: No ccache found. Please be aware that recompiling all source files may be required. You can download and install ccache from: https://github.com/ccache/ccache/blob/master/doc/INSTALL.md
  warnings.warn(warning_message)
Creating model: ('PP-LCNet_x1_0_doc_ori', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-LCNet_x1_0_doc_ori`.
Creating model: ('UVDoc', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/UVDoc`.
Creating model: ('PP-OCRv5_server_det', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_det`.
Creating model: ('PP-OCRv5_server_rec', None)
Model files already exist. Using cached files. To redownload, please delete the directory manually: `/home/ye/.paddlex/official_models/PP-OCRv5_server_rec`.
[✓] OCR complete. Saved to ./multilingual_paddle.txt
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ cat multilingual_paddle.txt
日夕方、福島県喜多方市の墓地の近くで除草作業をしていた
代の女性がクマに襲われ、左腕や左手首の骨を折る大けがをしました
义务教育阶段的孩子更让人牵挂
我发起
华阳星火助学计划
通过社会募集资金改善村内优秀学生的学习条件。截至
目前，已筹集超
万元，平均每月有
万元助学金定向帮扶优秀学生
マはそのまま逃げたとみられ、警察が注意を呼びかけています
in eastern
key question in
Europe is
山形県鶴岡市ではJR鶴岡駅近くにマが現れ、猟友会に駆除されました
年元旦过后，我响应党组织号召，主动请缨，成为中国延安干部学院派驻四川省凉山彝族自治州越西县华阳村的第一书记。从繁
华大都市到偏远小山村，从企业家之子到脱贫村第一书记，这样的身份转变
让不少人满心疑惑
这年轻人，是来做什么的ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine easyocr --lang ch_sim ja en
 --output ./multilingual_paddle.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' (GPU: True) ...
Traceback (most recent call last):
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 231, in <module>
    main()
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 227, in main
    process_file(args.input, args.output, args.engine, langs, args.gpu)
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 148, in process_file
    text = ocr_with_easyocr_image(img, langs, use_gpu)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/exp/ocr/./easy_paddle_ocr.py", line 32, in ocr_with_easyocr_image
    reader = easyocr.Reader(langs, gpu=use_gpu)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/ye/.local/lib/python3.12/site-packages/easyocr/easyocr.py", line 124, in __init__
    self.setModelLanguage('chinese_sim', lang_list, ['ch_sim','en'], '["ch_sim","en"]')
  File "/home/ye/.local/lib/python3.12/site-packages/easyocr/easyocr.py", line 286, in setModelLanguage
    raise ValueError(language.capitalize() + ' is only compatible with English, try lang_list=' + list_lang_string)
ValueError: Chinese_sim is only compatible with English, try lang_list=["ch_sim","en"]
ye@lst-hpc3090:~/exp/ocr$
```

```
ye@lst-hpc3090:~/exp/ocr$ python ./easy_paddle_ocr.py --input ./img/multilingual_test.png --engine easyocr --lang ch_sim en --
output ./multilingual_paddle.txt --gpu
[i] Processing page 1/1 with engine 'easyocr' (GPU: True) ...
[✓] OCR complete. Saved to ./multilingual_paddle.txt
ye@lst-hpc3090:~/exp/ocr$
```

easyOCR နဲ့ဆိုရင်တော့ တရုတ်စာနဲ့ အင်္ဂလိပ်စာကို တွဲသိတယ်။  

```
208夕方。福息鼎喜多方市0墓地0近<C除草作祟{匕乙 !70代0女性加2312羹力九。左腕加左手首0骨左折召大(+加"l击龙。
Can
NAT0
innovate
fast
enough
to
counter Russia' s  growing
Qrone
threat?
义务教育阶段的孩子更让人牵挂
2025年4月,我发起"华阳星火助学计划" ,通过社会募集资金改善村内优秀学生的学习条件。截至
目前。己筹集超12万元;平均每月有1万元助学金定向帮扶优秀学生。
Fl己0击击逃(f龙匕35九。警察加注意{呼Z{+击寸。
Days
after
the
Wail
Or
air-raid
Sirens
and
the
rOar
Or
NATO
fighter
jets  punctuated
a
peaceful
late-summer night
i
eastern
Poland
the
question
in Europe
15
not
Only
Whether
MoSCOW
deliberately
Sent
nearly
tWO
Qozen
Qrones
into
NATO airspace,
bu1t
what
the
military
response
reveals
about
the
a1liance' 5
long-term  abbility
tO
Qeal
With
this
growing
thceat 
031$8663O8
38569806338 . 38801
击尤 山形鼎:`市CJ:阀近<1夕又加琨九狒友会1躯除芒九击匕龙。
2024年元旦过后。我响应党组织号召,主动请缨;成为中国延安干部学院派驻四川省凉山彝族自治州越西县华阳村的第一书记。从繁
华大都市到偏远小山村,从企业家之子到脱贫村第-书记;这样的身份转娈。让不少人满心疑惑:这年轻人,是来做什么的?
GST
FTJ耐564 #eT并3氽~{7% @IASRTA3 u[:耐v耐〈币升d-4#n忑丽廿刃两丹耐9骊N市
可呵:并^ >
key
6SOlII
```

```
#!/usr/bin/env python3
import argparse
import sys
import os
import numpy as np
from PIL import Image

# --- EasyOCR import ---
try:
    import easyocr
    _HAVE_EASYOCR = True
except ImportError:
    _HAVE_EASYOCR = False

# --- PaddleOCR import ---
try:
    from paddleocr import PaddleOCR
    import inspect
    _HAVE_PADDLEOCR = True
except ImportError:
    _HAVE_PADDLEOCR = False


# =========================
# OCR ENGINE WRAPPERS
# =========================

def ocr_with_easyocr_image(img: Image.Image, langs: list[str], use_gpu: bool) -> str:
    if not _HAVE_EASYOCR:
        raise RuntimeError("easyocr not installed. Install with: pip install easyocr")
    arr = np.array(img.convert("RGB"))
    reader = easyocr.Reader(langs, gpu=use_gpu)
    results = reader.readtext(arr, detail=0)
    return "\n".join(results)



def ocr_with_paddleocr_image(img: Image.Image, lang: str, use_gpu: bool) -> str:
    if not _HAVE_PADDLEOCR:
        raise RuntimeError("paddleocr not installed. Install with: pip install paddleocr")

    arr = np.array(img.convert("RGB"))
    sig = inspect.signature(PaddleOCR)

    # Map language codes to PaddleOCR supported languages
    lang_mapping = {
        'ch': 'ch', 'chinese': 'ch', 'zh': 'ch', 'cn': 'ch',
        'en': 'en', 'english': 'en',
        'japan': 'japan', 'japanese': 'japan', 'jp': 'japan', 'ja': 'japan',
        'korean': 'korean', 'ko': 'korean', 'kr': 'korean',
        'french': 'french', 'fr': 'french',
        'german': 'german', 'de': 'german',
        'multilingual': 'ml', 'multi': 'ml', 'ml': 'ml',
    }
    
    # Get the mapped language code or use the original
    mapped_lang = lang_mapping.get(lang.lower(), lang.lower())
    
    # For multilingual documents, use Chinese model which handles multiple scripts well
    if mapped_lang in ['ml', 'multi', 'multilingual']:
        print("[i] Using multilingual mode (Chinese base model)")
        mapped_lang = 'ch'
    
    init_kwargs = {"lang": mapped_lang}
    if "device" in sig.parameters:
        init_kwargs["device"] = "gpu" if use_gpu else "cpu"
    if "use_textline_orientation" in sig.parameters:
        init_kwargs["use_textline_orientation"] = False
    elif "use_angle_cls" in sig.parameters:
        init_kwargs["use_angle_cls"] = False

    ocr = PaddleOCR(**init_kwargs)

    try:
        result = ocr.predict(arr)
    except Exception as e:
        raise RuntimeError(f"PaddleOCR inference error: {e}")

    lines = []
    
    if isinstance(result, list) and len(result) > 0:
        # Extract text from string representation
        result_str = str(result)
        
        import re
        
        # Combined pattern for multiple scripts (Chinese, Japanese, Korean, Latin, Cyrillic, etc.)
        combined_pattern = r'[\u4e00-\u9fff\u3400-\u4dbf\uf900-\ufaff\u3040-\u309F\u30A0-\u30FF\uAC00-\uD7AFa-zA-Z\u00C0-\u02FF\u0400-\u04FF\u0500-\u052F]{2,}(?:[\u4e00-\u9fff\u3400-\u4dbf\uf900-\ufaff\u3040-\u309F\u30A0-\u30FF\uAC00-\uD7AFa-zA-Z\u00C0-\u02FF\u0400-\u04FF\u0500-\u052F\s\u3000-\u303F\uFF00-\uFFEF\u2000-\u206F]{1,30}[\u4e00-\u9fff\u3400-\u4dbf\uf900-\ufaff\u3040-\u309F\u30A0-\u30FF\uAC00-\uD7AFa-zA-Z\u00C0-\u02FF\u0400-\u04FF\u0500-\u052F]{1,})*'
        
        matches = re.findall(combined_pattern, result_str)
        lines.extend(matches)
        
        # Comprehensive metadata filtering
        metadata_words = {
            'None', 'array', 'dtype', 'True', 'angle', 'False', 'min', 'thresh', 
            'general', 'paddlex', 'utils', 'fonts', 'Font', 'object', 'input', 
            'path', 'page', 'index', 'doc', 'preprocessor', 'res', 'img', 'model', 
            'settings', 'use', 'orientation', 'classify', 'unwarping', 'rot', 
            'output', 'polys', 'text', 'det', 'params', 'limit', 'side', 'len', 
            'type', 'max', 'box', 'unclip', 'ratio', 'rec', 'scores', 'vis', 
            'textline', 'angles', 'boxes', 'at', 'bf', '0x'
        }
        
        filtered_lines = []
        for line in lines:
            # Skip metadata, short lines, numbers, memory addresses, etc.
            line_clean = line.strip()
            if (line_clean and 
                len(line_clean) > 1 and
                not any(meta_word in line_clean for meta_word in metadata_words) and
                not line_clean.isdigit() and
                not re.match(r'^[a-zA-Z_]+$', line_clean) and
                not re.match(r'^0x[0-9a-fA-F]+$', line_clean) and
                not re.match(r'^\d+$', line_clean) and
                not re.match(r'^[_\W]+$', line_clean)):
                filtered_lines.append(line_clean)
        
        lines = filtered_lines
        
        # Remove duplicates while preserving order
        seen = set()
        unique_lines = []
        for line in lines:
            if line not in seen:
                seen.add(line)
                unique_lines.append(line)
        lines = unique_lines

    return "\n".join(lines) if lines else "No text detected"

# =========================
# MAIN OCR PIPELINE
# =========================

def process_file(input_file: str, output_file: str, engine: str, langs: list[str], use_gpu: bool):
    ext = os.path.splitext(input_file)[1].lower()

    # Load single image (you can extend to PDF if needed)
    try:
        img = Image.open(input_file)
    except Exception as e:
        sys.stderr.write(f"[ERROR] Failed to open {input_file}: {e}\n")
        sys.exit(1)

    print(f"[i] Processing page 1/1 with engine '{engine}' (GPU: {use_gpu}) ...")

    if engine == "easyocr":
        text = ocr_with_easyocr_image(img, langs, use_gpu)
    elif engine == "paddleocr":
        lang = langs[0] if langs else "ch"
        text = ocr_with_paddleocr_image(img, lang, use_gpu)
    else:
        sys.stderr.write(f"[ERROR] Unknown engine: {engine}\n")
        sys.exit(1)

    with open(output_file, "w", encoding="utf-8") as f:
        f.write(text)
    print(f"[✓] OCR complete. Saved to {output_file}")


def list_languages(engine: str):
    if engine == "easyocr":
        if not _HAVE_EASYOCR:
            print("EasyOCR not installed.")
            return
        
        # EasyOCR language list - manually maintained since available_languages() doesn't exist
        langs = [
            'abq', 'ad', 'af', 'ang', 'ar', 'as', 'ava', 'az', 'be', 'bg', 
            'bh', 'bho', 'bn', 'bs', 'ch_sim', 'ch_tra', 'che', 'cs', 'cy', 
            'da', 'dar', 'de', 'en', 'es', 'et', 'fa', 'fr', 'ga', 'gom', 
            'hi', 'hr', 'hu', 'id', 'inh', 'is', 'it', 'ja', 'kbd', 'kn', 
            'ko', 'ku', 'la', 'lbe', 'lez', 'lt', 'lv', 'mah', 'mai', 'mi', 
            'mn', 'mr', 'ms', 'mt', 'ne', 'new', 'nl', 'no', 'oc', 'pi', 
            'pl', 'pt', 'ro', 'ru', 'rs_cyrillic', 'rs_latin', 'sck', 'sk', 
            'sl', 'sq', 'sv', 'sw', 'ta', 'tab', 'te', 'th', 'tjk', 'tl', 
            'tr', 'ug', 'uk', 'ur', 'uz', 'vi'
        ]
        print("EasyOCR supported languages:")
        for l in sorted(langs):
            print(f"  {l}")
        print("\nExample: -l en ch_sim ja (for multiple languages)")
        
    elif engine == "paddleocr":
        if not _HAVE_PADDLEOCR:
            print("PaddleOCR not installed.")
            return
        # Updated list with more language codes
        langs = ["ch", "en", "japan", "korean", "french", "german", "latin", "arabic", "cyrillic"]
        print("PaddleOCR common language codes:")
        for l in langs:
            print(f"  {l}")
        print("\nNote: For Japanese, use 'japan', 'japanese', 'jp', or 'ja'")
        print("For multilingual documents, PaddleOCR automatically detects scripts")
        print("For full 80+ language support, see:")
        print(" https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.6/doc/doc_en/multi_languages_en.md")
    else:
        print(f"Unknown engine: {engine}")


# =========================
# CLI ENTRY POINT
# =========================

def main():
    parser = argparse.ArgumentParser(description="Free OCR tool using EasyOCR or PaddleOCR")
    parser.add_argument("-i", "--input", help="Input image file (PNG, JPG, JPEG, TIFF, BMP, GIF)")
    parser.add_argument("-o", "--output", help="Output text file")
    parser.add_argument("-e", "--engine", choices=["easyocr", "paddleocr"], required=False,
                        help="OCR engine to use (easyocr or paddleocr)")
    parser.add_argument("-l", "--lang", nargs="+",
                        help="Language codes (EasyOCR: multiple codes, PaddleOCR: single code like 'ch')")
    parser.add_argument("--gpu", action="store_true", help="Use GPU for acceleration (if available)")
    parser.add_argument("--list-langs", metavar="ENGINE", choices=["easyocr", "paddleocr"],
                        help="List supported languages for an engine (easyocr or paddleocr)")

    args = parser.parse_args()

    if args.list_langs:
        list_languages(args.list_langs)
        sys.exit(0)

    if not args.input or not args.output or not args.engine:
        parser.error("the following arguments are required: -i/--input, -o/--output, -e/--engine")

    langs = args.lang if args.lang else []
    process_file(args.input, args.output, args.engine, langs, args.gpu)


if __name__ == "__main__":
    main()


```


## Conclusion

- Chinese, English, Japanese OCR အတွက်ကတော့ EasyOCR နဲ့ PaddleOCR ကို offline သုံးလို့ ရလိမ့်မယ်။
- စာမျက်နှာ ဘယ်လောက် အများကြီးထဲ ပေးလုပ်သလဲ ဆိုတာကတော့ မစမ်းရသေး
- multilingual OCR ကို စမ်းကြည့်တာ အရမ်းကြီး အဆင်မပြေဘူး။ သို့သော် အင်္ဂလိပ်၊ တရုတ် အတွဲလိုမျိုးကတော့ ရနိုင်တယ်
- မြန်မာစာအတွက်ကတော့ internship ကျောင်းသားတွေလုပ်ခဲ့တဲ့ google-cloud-vision က အကောင်းဆုံး ဖြစ်နိုင်တယ်။
- အချိန်ရတဲ့အခါ google-cloud-vision ကိုပဲ study လုပ်ရန်

