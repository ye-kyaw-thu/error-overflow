# Brat Testing Log

Brat က ဆရာ Tsujii တို့အဖွဲ့က develop လုပ်ထားတဲ့ annotation tool ပါ။  
အဲဒီ tool ကို ဒီတစ်ခါတော့ မြန်မာစာ annotation အတွက် သုံးဖို့လိုအပ်လာလို့ စမ်းကြည့်ထားတုန်းက note အဖြစ် ရေးထားတဲ့ log ပါ။  

## git clone

git clone နဲ့ ကိုယ့်local စက်ထဲကို download လုပ်ယူပါမယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/nlplab/brat
Cloning into 'brat'...
remote: Enumerating objects: 17063, done.
remote: Counting objects: 100% (34/34), done.
remote: Compressing objects: 100% (25/25), done.
remote: Total 17063 (delta 11), reused 23 (delta 9), pack-reused 17029
Receiving objects: 100% (17063/17063), 84.47 MiB | 17.21 MiB/s, done.
Resolving deltas: 100% (10305/10305), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd brat
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat$ ls
ajax.cgi         apache-user.sh      configurations   diff.xhtml    favicon.ico  install.sh     lighttpd_fcgi.conf  res            static         tutorial.cgi
ajax.fcgi        client              CONTRIBUTING.md  example-data  index.html   LICENSE.md     offline.xhtml       server         testserver.py
apache-group.sh  config_template.py  CONTRIBUTORS.md  external      index.xhtml  lighttpd.conf  README.md           standalone.py  tools
```

## Standalone Installation

တစ်ယောက်ထက်မကတဲ့ annotator တွေ web-server မှာ အလုပ်အတူတူ လုပ်လို့ရအောင်လည်း Brat က support လုပ်ပါတယ်။ Facility တွေအများကြီးပါ။ ဒါပေမဲ့ ဒီ testing ကတော့ ကိုယ့်စက်ထဲမှာပဲ data ပြင်ဆင်တဲ့သူ တစ်ယောက်တည်း အတွက်ပဲ စမ်းခဲ့ပါတယ်။ Standalone installation (-u option) ပါ။  
user name နဲ့ password ကို သတ်မှတ်ပေးရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat$ ./install.sh -u
Please enter the user name that you want to use when logging into brat:
ye
Please enter a brat password (this shows on screen):
abc123
Please enter the administrator contact email:
abc123
Data and work directories data/ and work/ exist, skipping setup.
The installation has finished, you are almost done.

1.) If you are installing brat on a webserver, make sure you have 
    followed the steps described in the brat manual to enable CGI:

    http://brat.nlplab.org/installation.html

2.) Please verify that brat is running by accessing your installation
    using a web browser.

You can automatically diagnose some common installation issues using:

    tools/troubleshooting.sh URL_TO_BRAT_INSTALLATION

If there are issues not detected by the above script, please contact the
brat developers and/or file a bug to the brat bug tracker:

    https://github.com/nlplab/brat/issues'

3.) Once brat is running, put your data in the data directory. Or use
    the example data placed there by the installation:

    /home/ye/tool/brat/data

4.) You can find configuration files to place in your data directory in
    the configurations directory, see the manual for further details:

    /home/ye/tool/brat/configurations

5.) Then, you (and your team?) are ready to start annotating!
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat$ 

## Run Brat as Standalone Server
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat$ python standalone.py
Serving brat at http://0.0.0.0:8001
```

## Screenshot

Installation က အဆင်ပြေပြေနဲ့ ပြီးသွားပြီဆိုရင်တော့ standalone mode နဲ့ run ကြည့်ကြရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat$ python standalone.py
Serving brat at http://0.0.0.0:8001
```

Web page တစ်ခုအနေနဲ့ အောက်ပါ UI လိုမျိုးကို မြင်ရပါလိမ့်မယ်။  
ကိုယ် annotation လုပ်မယ့် project ဖိုလ်ဒါအောက်ကိုဝင်ပြီး အလုပ်လုပ်သွားယုံပါပဲ။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/brat-running-standalone-mode.png" alt="drawing" width="800"/>  
</p>  
<div align="center">
  Fig. Open project folder dialogue screen of Brat Annotation Tool  
</div>   
<br />

အသုံးပြုပုံ ဘာညာနဲ့ ပတ်သက်တဲ့ Tutorial လည်း ရှိပါတယ်။  
လေ့လာကြည့်ကြပါ။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/brat-tutorial-screen.png" alt="drawing" width="800"/>  
</p>  
<div align="center">
  Fig. Tutorial Screen of Brat Annotation Tool  
</div>   
<br />

## Check Files

Example tagged လုပ်ပြထားတဲ့ folder တွေကို ဝင်လေ့လာခဲ့တယ်။  
အောက်ပါ ဖိုင်စာရင်းက ပေါ်တူဂီဘာသာစကား conll ဒေတာနဲ့ ပတ်သက်တယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$ ls
annotation.conf                            portuguese_bosque_train.conll-doc-284.ann  portuguese_bosque_train.conll-doc-531.txt  portuguese_bosque_train.conll-doc-747.ann
portuguese_bosque_train.conll-doc-120.ann  portuguese_bosque_train.conll-doc-284.txt  portuguese_bosque_train.conll-doc-590.ann  portuguese_bosque_train.conll-doc-747.txt
portuguese_bosque_train.conll-doc-120.txt  portuguese_bosque_train.conll-doc-322.ann  portuguese_bosque_train.conll-doc-590.txt  portuguese_bosque_train.conll-doc-754.ann
portuguese_bosque_train.conll-doc-12.ann   portuguese_bosque_train.conll-doc-322.txt  portuguese_bosque_train.conll-doc-616.ann  portuguese_bosque_train.conll-doc-754.txt
portuguese_bosque_train.conll-doc-12.txt   portuguese_bosque_train.conll-doc-401.ann  portuguese_bosque_train.conll-doc-616.txt  portuguese_bosque_train.conll-doc-785.ann
portuguese_bosque_train.conll-doc-227.ann  portuguese_bosque_train.conll-doc-401.txt  portuguese_bosque_train.conll-doc-668.ann  portuguese_bosque_train.conll-doc-785.txt
portuguese_bosque_train.conll-doc-227.txt  portuguese_bosque_train.conll-doc-48.ann   portuguese_bosque_train.conll-doc-668.txt  portuguese_bosque_train.conll-doc-87.ann
portuguese_bosque_train.conll-doc-241.ann  portuguese_bosque_train.conll-doc-48.txt   portuguese_bosque_train.conll-doc-710.ann  portuguese_bosque_train.conll-doc-87.txt
portuguese_bosque_train.conll-doc-241.txt  portuguese_bosque_train.conll-doc-504.ann  portuguese_bosque_train.conll-doc-710.txt  README
portuguese_bosque_train.conll-doc-261.ann  portuguese_bosque_train.conll-doc-504.txt  portuguese_bosque_train.conll-doc-73.ann   tools.conf
portuguese_bosque_train.conll-doc-261.txt  portuguese_bosque_train.conll-doc-531.ann  portuguese_bosque_train.conll-doc-73.txt   visual.conf
```

annotation.conf ဖိုင်ကို ဝင်လေ့လာခဲ့။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$ vi annotation.conf 
```

ဒီ annotation tool ကို သုံးမယ်ဆိုရင် စာကြောင်း အကြောင်း ၁၀၀လောက် ၁၅၀လောက်ကို text ဖိုင် တစ်ဖိုင်စီသွား လုပ်တာက သင့်တော်တယ်။  
myPOS corpus (version 3.0) တစ်ခုလုံး ဆိုရင် စာကြောင်းရေ လေးသောင်းကျော်ရှိတာမို့ သူ့ကို loading လုပ်ကြည့်တဲ့အခါမှာ အချိန်အရမ်းကြာပြီးတော့ load လုပ်မပေးနိုင်တာကို တွေ့ရတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$ head portuguese_bosque_train.conll-doc-120.txt 
ROOT Um quarteto formado por Bob_Mover ( sax alto e voz ) , Carlo_Morena ( piano ) , Pedro_Gonçalves ( contrabaixo ) e João_Silvestre ( bateria ) actua a_partir_de as 23h , em a catedral lisboeta de o jazz : em o Hot_Clube de Portugal .
ROOT Uma « autêntica » big_band , constituída por 16 músicos , com alguns de os temas mais conhecidos de o reportório « standard » liderada por o trombonista Claus_Nymark e com a voz de Ana_Paula_Oliveira : em o Speakeasy ( Cais_da_Rocha Conde_d'Óbidos -- Armazém 115 ) , a as 23h e 01h.
ROOT CONTRA O GOVERNO --
ROOT Alguns milhares de trabalhadores afectos a a CGTP desfilaram ontem por a baixa de Lisboa em protesto contra a política económica e social de o Governo .
ROOT Um boneco cabeçudo baptizado de « Santo_Cavaco » foi a estrela de a manifestação , que partiu de os Restauradores e foi até a a Praça_da_Ribeira , depois de interromper o trânsito de as Ruas de o Ouro e de a Prata .
ROOT O mote de os protestos variou entre « Emprego seguro , garantia de futuro ! » , « Melhores salários , melhores horários ! » , « Mais emprego , mais salário , Portugal mais solidário ! » ou « Despedir , desmantelar , é Cavaco a governar ! »
ROOT Em o fim , Manuel_Carvalho_da_Silva , coordenador de a CGTP , também ajudou :
ROOT « Não podemos permitir que a contratação colectiva continue bloqueada , que o desemprego continue a aumentar , que a segurança social , a saúde e a educação continuem a degradar- se » .
ROOT « Somos obrigados a tornar os nossos programas o mais interessantes possível , em um ambiente onde existem múltiplas escolhas » , refere Victor_Neufeld , o produtor executivo de o programa 20/20 , de a ABC , citado por a Associated_Press .
ROOT « Cada_vez fazemos mais pesquisa para encontrar histórias novas e cada_vez vamos mais fundo para as investigar . »
```

annotation ကို ဘယ်လို data format နဲ့ သိမ်းပေးထားတာလဲ ဆိုတာကို example tagged လုပ်ပြထားတဲ့ ဖိုင်ကနေ လေ့လာခဲ့တယ်။  
အောက်ပါ format အတိုင်း သိမ်းပေးတာကို တွေ့ရတယ်။  
T1, T2 ဆိုတာက Tagged-1, Tagged-2 လားလို့....  
ဒုတိယ ကော်လံမှာ tag တွေကို သိမ်းထားတယ်။  
တတိယ ကော်လံနဲ့ စတုတ္ထကော်လံက tag လုပ်ထားတဲ့ စာလုံးက character ဘယ်နေရာကနေ ဘယ်နေရာအထိ ဆိုတာကို letter (or character) ရဲ့ position အလိုက် မှတ်ထားတဲ့ပုံစံ။  
နောက်ဆုံးကော်လံ ကတော့ tagged လုပ်ထားတဲ့ ပေါ်တူဂီစာကြောင်းထဲက စာလုံးတွေ ကို သိမ်းထားတာ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$ head portuguese_bosque_train.conll-doc-120.ann
T1	ROOT 0 4	ROOT
T2	art 5 7	Um
T3	n 8 16	quarteto
T4	v-pcp 17 24	formado
T5	prp 25 28	por
T6	prop 29 38	Bob_Mover
T7	punc 39 40	(
T8	n 41 44	sax
T9	adj 45 49	alto
T10	conj-c 50 51	e
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$
```

## Tagging on myPOS (version 3.0)

myPOS နဲ့ annotation tool ကို စမ်းဖို့အတွက် အရင်ဆုံး annotation.conf ဖိုင်မှာ setting ဝင်လုပ်ခဲ့တယ်။  
\[entities\] ဆိုတဲ့ အောက်မှာ myPOS မှာ သုံးထားတဲ့ POS tag-set ကို tag တစ်ခုစီကို စာကြောင်း တစ်ကြောင်းစီ ရေးတဲ့ပုံစံနဲ့ ဝင်ဖြည့်ခဲ့တယ်။  
ကျန်တဲ့ relations, events တို့ကိုတော့ မဆိုင်လို့ blank ထားထားခဲ့တယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ cat annotation.conf 
# Simple text-based definitions of entity types for the CoNLL 2002 Shared
# Task on Language-Independent Named Entity Recognition.


[entities]

abb
adj
adv
conj
fw
int
n
num
part
ppm
pron
punc
sb
tn
v

# (only entities defined, so the remaining sections are empty)

[relations]

[events]

[attributes]
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$
```

visual.conf ဖိုင်ကတော့ browser မှာ tag တစ်ခုချင်းစီကို ဘယ်လိုအရောင်နဲ့ ပေါ်စေချင်သလဲ စတဲ့ visual နဲ့ ဆိုင်တဲ့ setting ဖိုင်ပါ။  
ကိုယ်အဆင်ပြေသလို ထားလို့ အိုကေပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ cat visual.conf 
# Visual configuration options for the CoNLL 2002 Shared Task on
# Language-Independent Named Entity Recognition.

[drawing]

abb	bgColor:#ccadf6
adj	bgColor:#fffda8
adv	bgColor:#fffda8
conj	bgColor:white
fw	bgColor:#e3e3e3
int	bgColor:#ffe8be
n	bgColor:#a4bced
num	bgColor:#ccdaf6
part	bgColor:#ffe8be
ppm	bgColor:#ffe8be
pron	bgColor:#ccdaf6
punc	bgColor:#e3e3e3
sb	bgColor:#adf6a2
tn	bgColor:#ccadf6
v	bgColor:#adf6a2

SPAN_DEFAULT	fgColor:black, bgColor:lightgreen, borderColor:darken

# (no abbreviations, so empty "labels" section)

[labels]
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$

```

စာလုံး တစ်လုံးချင်းစီကို browser မှာ tagging လုပ်တဲ့အခါမှာ ကိုယ် tag လုပ်ချင်တဲ့ စာလုံးကို mouse နဲ့ selection မှတ်လိုက်တာနဲ့ အောက်ပါအတိုင်း myPOS မှာ သတ်မှတ်ထားတဲ့ POS tag တွေကိုရွေးဖို့အတွက် selection  box ကို မြင်ရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myPOS-tags-selection-box2.png" alt="drawing" width="500"/>  
</p>  
<div align="center">
  Fig. POS tags selection box
</div>   
<br />

မြန်မာစာ စာကြောင်းတချို့ကို manual tagging လုပ်ပြီးတဲ့အခါမှာ အောက်ပါလိုမျိုး လှလှပပ မြင်ရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/brat-myPOS-skip2.png" alt="drawing" width="800"/>  
</p>  
<div align="center">
  Fig. An examples of tagged Myanmar sentences
</div>   
<br />

အခု ဥပမာအနေနဲ့ manual tagging လုပ်နေတာက head.txt ဖိုင်မို့လို့ tagged လုပ်ထားတာကို သိမ်းပေးထားတဲ့ ဖိုင်နာမည်က head.ann ဖြစ်လာပြီးတော့ အဲဒီ ဖိုင်ထဲမှာတော့ tagging လုပ်ထားတာနဲ့ ပတ်သက်တာတွေကို အောက်ပါအတိုင်း မှတ်သားထားပေးထားတာကို တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ cat head.ann 
T1	adj 0 2	ဒီ
T2	n 3 5	ဆေ
T3	ppm 7 8	က
T4	num 9 12	၁၀၀
T5	n 13 25	ရာခိုင်နှုန်
T6	adj 27 36	ဆေးဘက်ဝင်
T7	n 37 41	အပင်
T8	part 42 45	မျာ
T9	ppm 47 49	မှ
T10	v 50 57	ဖော်စပ်
T11	part 58 61	ထား
T12	part 62 64	တာ
T13	v 65 69	ဖြစ်
T14	ppm 70 73	တယ်
T15	punc 74 75	။
T16	n 76 80	အသစ်
T17	v 81 84	ဝယ်
T18	part 85 88	ထား
T19	part 89 92	တဲ့
T20	n 93 99	ဆွယ်တာ
T21	ppm 100 101	က
T22	n 102 105	အသီ
T23	v 107 108	ထ
T24	part 109 111	နေ
T25	part 112 114	ပါ
T26	part 115 119	ပေါ့
T27	punc 120 121	။
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ 
```

## Testing Skip Line Problem

စာကြောင်းတွေကို manual tagging လုပ်တဲ့အခါမှာ လက်တွေ့မှာက ခက်တဲ့စာကြောင်းမို့လို့ လောလောဆယ် မလုပ်သေးဘူး ဆိုပြီးတော့ ကျော်သွားတာမျိုး လုပ်တတ်ကြပါတယ်။  
တခါတလေမှာ စာကြောင်း တစ်ကြောင်းလုံး ပြီးအောင် tag မလုပ်သေးပဲ ဘယ်လို tag ကို ရွေးရမလဲ မသေချာတာကြောင့် နောက်မှ ပြန်စစ်ပြီး ဆက်လုပ်မယ်ဆိုပြီးတော့ တပိုင်းတစနဲ့ ထားထားတာမျိုးလည်း ရှိတတာပါတယ်။  
အဲဒီ ကိစ္စအတွက် စမ်းကြည့်ခဲ့တော့ head.ann မှာက tag လုပ်ခဲ့တဲ့ အစီအစဉ်အတိုင်းပဲ save လုပ်ပေးသွားတာကို တွေ့ရပါတယ်။  
တကယ်တမ်းကတော့ ဒီကိစ္စက ann ဖိုင်တွေကနေ ကိုယ်လိုချင်တဲ့ tagged corpus အဖြစ် ပြန်ဆွဲထုတ်ယူတဲ့အခါမှာ corpus ထဲက စာကြောင်းအစီအစဉ်နဲ့ လွဲသွားနိုင်တယ်လို့ မြင်မိပါတယ်။  
တကယ်တမ်း ဒီ tool ကို သုံးပြီး manual tagging လုပ်တဲ့အခါမှာ ဒီကိစ္စကိုပါ စဉ်းစားပြီးတော့ စာကြောင်းတွေကို အစဉ်အလိုက်အတိုင်း အထက်အောက် တစ်ကြောင်းချင်းစီ တပ်သွားမှ ဖြစ်မယ်လို့ ထင်ပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ cat head.ann 
T1	adj 0 2	ဒီ
T2	n 3 5	ဆေ
T3	ppm 7 8	က
T4	num 9 12	၁၀၀
T5	n 13 25	ရာခိုင်နှုန်
T6	adj 27 36	ဆေးဘက်ဝင်
T7	n 37 41	အပင်
T8	part 42 45	မျာ
T9	ppm 47 49	မှ
T10	v 50 57	ဖော်စပ်
T11	part 58 61	ထား
T12	part 62 64	တာ
T13	v 65 69	ဖြစ်
T14	ppm 70 73	တယ်
T15	punc 74 75	။
T16	n 76 80	အသစ်
T17	v 81 84	ဝယ်
T18	part 85 88	ထား
T19	part 89 92	တဲ့
T20	n 93 99	ဆွယ်တာ
T21	ppm 100 101	က
T22	n 102 105	အသီ
T23	v 107 108	ထ
T24	part 109 111	နေ
T25	part 112 114	ပါ
T26	part 115 119	ပေါ့
T27	punc 120 121	။
T28	n 201 208	ပေဟိုင်
T29	n 209 215	ဥယျာဉ်
T30	punc 216 217	။
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ cat head.ann 
T1	adj 0 2	ဒီ
T2	n 3 5	ဆေ
T3	ppm 7 8	က
T4	num 9 12	၁၀၀
T5	n 13 25	ရာခိုင်နှုန်
T6	adj 27 36	ဆေးဘက်ဝင်
T7	n 37 41	အပင်
T8	part 42 45	မျာ
T9	ppm 47 49	မှ
T10	v 50 57	ဖော်စပ်
T11	part 58 61	ထား
T12	part 62 64	တာ
T13	v 65 69	ဖြစ်
T14	ppm 70 73	တယ်
T15	punc 74 75	။
T16	n 76 80	အသစ်
T17	v 81 84	ဝယ်
T18	part 85 88	ထား
T19	part 89 92	တဲ့
T20	n 93 99	ဆွယ်တာ
T21	ppm 100 101	က
T22	n 102 105	အသီ
T23	v 107 108	ထ
T24	part 109 111	နေ
T25	part 112 114	ပါ
T26	part 115 119	ပေါ့
T27	punc 120 121	။
T28	n 201 208	ပေဟိုင်
T29	n 209 215	ဥယျာဉ်
T30	punc 216 217	။
T31	part 122 123	မ
T32	v 124 131	ကျန်းမာ
T33	conj 132 137	လျှင်
T34	n 138 141	နတ်
T35	n 142 145	ဆရာ
T36	ppm 146 148	ထံ
T37	v 149 156	မေးမြန်
T38	conj 158 159	၍
T39	n 160 170	သက်ဆိုင်ရာ
T40	n 171 174	နတ်
T41	part 175 179	တို့
T42	ppm 180 183	အား
T43	v 184 192	ပူဇော်ပသ
T44	part 193 194	ရ
T45	ppm 195 198	သည်
T46	punc 199 200	။
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$
```

အထက်မှာ myPOS corpus (version 3.0) ကိုသုံးပြီး ဥပမာအနေနဲ့ manual POS tagging လုပ်ထားတာကို ဒီမိုလုပ်ပြခဲ့ပေမဲ့ [brat rapid annotation tool (brat)](https://github.com/nlplab/brat) က ကိုယ်လုပ်ချင်တဲ့ tagging scheme မျိုးစုံကို သတ်မှတ်ပြီး tagging လုပ်လို့ ရတဲ့ tool မို့လို့ တကယ်အသုံးဝင်ပါတယ်။ pure NLP တစ်ခုတည်းအတွက် မဟုတ်ပဲ BioNLP တို့လို ကိစ္စတွေအတွက်လည်း အသုံးဝင်ပါလိမ့်မယ်။ အောက်ပါ screenshot က [2006 CoNLL Shared Task](https://catalog.ldc.upenn.edu/LDC2015T11) ရဲ့ ပေါ်တူဂီ dependency tree ဒေတာဖိုင်ကို လေ့လာနိုင်အောင် ထည့်ပေးထားတာပါ။          

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/brat-CoNLL-ST_2006_portuguese-example.png" alt="drawing" width="1200"/>  
</p>  
<div align="center">
  Fig. An examples of dependency tree for Portuguese
</div>   
<br />

## Reference

Brat Homepage: http://brat.nlplab.org/index.html  
Manual: http://brat.nlplab.org/manual.html  
