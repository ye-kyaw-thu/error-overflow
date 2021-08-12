# Brat Testing Log

Brat က ဆရာ Tsujii တို့အဖွဲ့က develop လုပ်ထားတဲ့ annotation tool ပါ။  
အဲဒီ tool ကို ဒီတစ်ခါတော့ မြန်မာစာ annotation အတွက် သုံးဖို့လိုအပ်လာလို့ စမ်းကြည့်ထားတုန်းက note အဖြစ် ရေးထားတဲ့ log ပါ။  

## Standalone Installation

တစ်ယောက်ထက်မကတဲ့ annotator တွေ web-server မှာ အလုပ်အတူတူ လုပ်လို့ရအောင်လည်း Brat က support လုပ်ပါတယ်။ Facility တွေအများကြီးပါ။ ဒါပေမဲ့ ဒီ testing ကတော့ ကိုယ့်စက်ထဲမှာပဲ data ပြင်ဆင်တဲ့သူ တစ်ယောက်တည်း အတွက်ပဲ စမ်းခဲ့ပါတယ်။ Standalone installation ပါ။  

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


## Check Files

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

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/examples/CoNLL-ST_2006$ vi annotation.conf 
```

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

** to add figure
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
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/brat/data/mypos$ 
```

## Testing Skip Line Problem

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
