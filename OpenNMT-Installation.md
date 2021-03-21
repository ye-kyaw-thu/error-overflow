# OpenNMT Installation and Demo Running with English-Myanmar Parallel Corpus

Neural Machine Translation framework တွေက လက်ရှိမှာ အများကြီးရှိပါတယ်။ အဲဒီထဲက OpenNMT framework ကို installation လုပ်တဲ့အဆင့်ကနေ ကိုယ့်ဒေတာနဲ့ကိုယ် run တာကို ဒီမိုလုပ်ပြထားပါတယ်။  

## Installing OpenNMT

OpenNMT Python version source code ကို GitHub ကနေ အရင်ဆုံး download လုပ်ပါ။ လုပ်ပြီးရင် အောက်ပါအတိုင်း installation လုပ်ပါ။  
Anaconda ကိုသုံးပြီးတော့ Python 3.6 version environment ကို ကြိုပြင်ဆင်ထားသင့်ပါတယ်။ အဲဒီအဆင့်တွေကိုတော့ ဒီနေရာမှာ skip လုပ်ပြီးသွားပါမယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpenNMT-py$ pip install -e .
Obtaining file:///home/ye/tool/OpenNMT-py
Requirement already satisfied: tqdm<5,>=4.51 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from OpenNMT-py==2.0.0) (4.55.1)
Collecting flask==1.1.2
  Using cached Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting pyyaml==5.3.1
  Using cached PyYAML-5.3.1.tar.gz (269 kB)
Collecting torch==1.6.0
  Downloading torch-1.6.0-cp36-cp36m-manylinux1_x86_64.whl (748.8 MB)
     |████████████████████████████████| 748.8 MB 26 kB/s 
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from torch==1.6.0->OpenNMT-py==2.0.0) (1.19.4)
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', ConnectionResetError(104, 'Connection reset by peer'))': /simple/future/
Collecting torchtext==0.5.0
  Using cached torchtext-0.5.0-py3-none-any.whl (73 kB)
Requirement already satisfied: six in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from torchtext==0.5.0->OpenNMT-py==2.0.0) (1.15.0)
Collecting waitress==1.4.4
  Using cached waitress-1.4.4-py2.py3-none-any.whl (58 kB)
Collecting click>=5.1
  Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting configargparse<2,>=1.2.3
  Downloading ConfigArgParse-1.4.tar.gz (45 kB)
     |████████████████████████████████| 45 kB 880 kB/s 
Collecting itsdangerous>=0.24
  Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.3-py2.py3-none-any.whl (125 kB)
     |████████████████████████████████| 125 kB 863 kB/s 
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp36-cp36m-manylinux2010_x86_64.whl (32 kB)
Collecting pyonmttok<2,>=1.23
  Downloading pyonmttok-1.25.0-cp36-cp36m-manylinux1_x86_64.whl (2.6 MB)
     |████████████████████████████████| 2.6 MB 510 kB/s 
Collecting tensorboard<3,>=2.3
  Using cached tensorboard-2.4.1-py3-none-any.whl (10.6 MB)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from tensorboard<3,>=2.3->OpenNMT-py==2.0.0) (51.0.0.post20201207)
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from tensorboard<3,>=2.3->OpenNMT-py==2.0.0) (0.36.2)
Collecting absl-py>=0.4
  Using cached absl_py-0.12.0-py3-none-any.whl (129 kB)
Collecting google-auth<2,>=1.6.3
  Downloading google_auth-1.28.0-py2.py3-none-any.whl (136 kB)
     |████████████████████████████████| 136 kB 637 kB/s 
Collecting cachetools<5.0,>=2.0.0
  Using cached cachetools-4.2.1-py3-none-any.whl (12 kB)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.3-py2.py3-none-any.whl (18 kB)
Collecting grpcio>=1.24.3
  Downloading grpcio-1.36.1-cp36-cp36m-manylinux2014_x86_64.whl (4.1 MB)
     |████████████████████████████████| 4.1 MB 774 kB/s 
Collecting markdown>=2.6.8
  Using cached Markdown-3.3.4-py3-none-any.whl (97 kB)
Collecting protobuf>=3.6.0
  Downloading protobuf-3.15.6-cp36-cp36m-manylinux1_x86_64.whl (1.0 MB)
     |████████████████████████████████| 1.0 MB 1.0 MB/s 
Collecting pyasn1-modules>=0.2.1
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Collecting requests
  Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests->torchtext==0.5.0->OpenNMT-py==2.0.0) (2020.12.5)
Collecting chardet<5,>=3.0.2
  Using cached chardet-4.0.0-py2.py3-none-any.whl (178 kB)
Collecting idna<3,>=2.5
  Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.0-py2.py3-none-any.whl (23 kB)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.1.0-py2.py3-none-any.whl (147 kB)
Collecting rsa<5,>=3.1.4
  Using cached rsa-4.7.2-py3-none-any.whl (34 kB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.0-py3-none-any.whl (781 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.4-py2.py3-none-any.whl (153 kB)
     |████████████████████████████████| 153 kB 1.0 MB/s 
Collecting Werkzeug>=0.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting future
  Downloading future-0.18.2.tar.gz (829 kB)
     |████████████████████████████████| 829 kB 1.0 MB/s 
Collecting importlib-metadata
  Downloading importlib_metadata-3.7.3-py3-none-any.whl (12 kB)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from importlib-metadata->markdown>=2.6.8->tensorboard<3,>=2.3->OpenNMT-py==2.0.0) (3.7.4.3)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from importlib-metadata->markdown>=2.6.8->tensorboard<3,>=2.3->OpenNMT-py==2.0.0) (3.4.1)
Collecting sentencepiece
  Downloading sentencepiece-0.1.95-cp36-cp36m-manylinux2014_x86_64.whl (1.2 MB)
     |████████████████████████████████| 1.2 MB 1.1 MB/s 
Building wheels for collected packages: pyyaml, configargparse, future
  Building wheel for pyyaml (setup.py) ... done
  Created wheel for pyyaml: filename=PyYAML-5.3.1-cp36-cp36m-linux_x86_64.whl size=44621 sha256=427f50aed45ca2d6db472290b295b7782e02c3ebd2938b5269db27872934456c
  Stored in directory: /home/ye/.cache/pip/wheels/e5/9d/ad/2ee53cf262cba1ffd8afe1487eef788ea3f260b7e6232a80fc
  Building wheel for configargparse (setup.py) ... done
  Created wheel for configargparse: filename=ConfigArgParse-1.4-py3-none-any.whl size=19639 sha256=8bf34e7fd9ec7ed7d13444b3c47810ae27d4ef285c14c0947b0410e64ab31c70
  Stored in directory: /home/ye/.cache/pip/wheels/d7/58/75/55e0ab6ba4dccaa280df70550a38a98db42a9e66555b056c09
  Building wheel for future (setup.py) ... done
  Created wheel for future: filename=future-0.18.2-py3-none-any.whl size=491059 sha256=83885b18281ba41594addf334092a6001ec1a808e37c3d829526d9f99097f777
  Stored in directory: /home/ye/.cache/pip/wheels/6e/9c/ed/4499c9865ac1002697793e0ae05ba6be33553d098f3347fb94
Successfully built pyyaml configargparse future
Installing collected packages: urllib3, pyasn1, idna, chardet, rsa, requests, pyasn1-modules, oauthlib, cachetools, requests-oauthlib, MarkupSafe, importlib-metadata, google-auth, future, Werkzeug, torch, tensorboard-plugin-wit, sentencepiece, protobuf, markdown, Jinja2, itsdangerous, grpcio, google-auth-oauthlib, click, absl-py, waitress, torchtext, tensorboard, pyyaml, pyonmttok, flask, configargparse, OpenNMT-py
  Attempting uninstall: torch
    Found existing installation: torch 1.7.1
    Uninstalling torch-1.7.1:
      Successfully uninstalled torch-1.7.1
  Attempting uninstall: pyyaml
    Found existing installation: PyYAML 5.4.1
    Uninstalling PyYAML-5.4.1:
      Successfully uninstalled PyYAML-5.4.1
  Running setup.py develop for OpenNMT-py
Successfully installed Jinja2-2.11.3 MarkupSafe-1.1.1 OpenNMT-py Werkzeug-1.0.1 absl-py-0.12.0 cachetools-4.2.1 chardet-4.0.0 click-7.1.2 configargparse-1.4 flask-1.1.2 future-0.18.2 google-auth-1.28.0 google-auth-oauthlib-0.4.3 grpcio-1.36.1 idna-2.10 importlib-metadata-3.7.3 itsdangerous-1.1.0 markdown-3.3.4 oauthlib-3.1.0 protobuf-3.15.6 pyasn1-0.4.8 pyasn1-modules-0.2.8 pyonmttok-1.25.0 pyyaml-5.3.1 requests-2.25.1 requests-oauthlib-1.3.0 rsa-4.7.2 sentencepiece-0.1.95 tensorboard-2.4.1 tensorboard-plugin-wit-1.8.0 torch-1.6.0 torchtext-0.5.0 urllib3-1.26.4 waitress-1.4.4
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpenNMT-py$
```

## Installing Requirements

တခြား လိုအပ်တဲ့ library, tool တွေကို installation လုပ်ပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpenNMT-py$ pip install -r requirements.opt.txt
Collecting git+git://github.com/NVIDIA/apex.git@700d6825e205732c1d6be511306ca4e595297070 (from -r requirements.opt.txt (line 6))
  Cloning git://github.com/NVIDIA/apex.git (to revision 700d6825e205732c1d6be511306ca4e595297070) to /tmp/pip-req-build-jlao6024
Collecting cffi==1.14.3
  Downloading cffi-1.14.3-cp36-cp36m-manylinux1_x86_64.whl (400 kB)
     |████████████████████████████████| 400 kB 1.7 MB/s 
Requirement already satisfied: pycparser in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from cffi==1.14.3->-r requirements.opt.txt (line 1)) (2.20)
Collecting joblib==0.17.0
  Using cached joblib-0.17.0-py3-none-any.whl (301 kB)
Collecting llvmlite==0.32.1
  Downloading llvmlite-0.32.1-cp36-cp36m-manylinux1_x86_64.whl (20.2 MB)
     |████████████████████████████████| 20.2 MB 703 kB/s 
Collecting numba==0.43.0
  Downloading numba-0.43.0-cp36-cp36m-manylinux1_x86_64.whl (3.3 MB)
     |████████████████████████████████| 3.3 MB 576 kB/s 
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from numba==0.43.0->-r requirements.opt.txt (line 3)) (1.19.4)
Collecting pyrouge==0.1.3
  Using cached pyrouge-0.1.3.tar.gz (60 kB)
Collecting sentencepiece==0.1.94
  Downloading sentencepiece-0.1.94-cp36-cp36m-manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 611 kB/s 
Collecting subword-nmt==0.3.7
  Using cached subword_nmt-0.3.7-py2.py3-none-any.whl (26 kB)
Building wheels for collected packages: apex, pyrouge
  Building wheel for apex (setup.py) ... done
  Created wheel for apex: filename=apex-0.1-py3-none-any.whl size=192739 sha256=5230d2cbd6cdadb6eed288e82e060bde0368a9d8426c4606b722629bb3be2db8
  Stored in directory: /home/ye/.cache/pip/wheels/8d/f8/65/1a008861e573ad6c957b50e46f7fc63ce4cbce157fad9d8a38
  Building wheel for pyrouge (setup.py) ... done
  Created wheel for pyrouge: filename=pyrouge-0.1.3-py3-none-any.whl size=191613 sha256=c394230932b542c14af92999ec82fd20a801b8ef6697502332234abca82fc719
  Stored in directory: /home/ye/.cache/pip/wheels/a4/5b/9a/2886f984445146fa94b3629de3ad6e5c1d4b931285716461bb
Successfully built apex pyrouge
Installing collected packages: llvmlite, subword-nmt, sentencepiece, pyrouge, numba, joblib, cffi, apex
  Attempting uninstall: llvmlite
    Found existing installation: llvmlite 0.35.0
    Uninstalling llvmlite-0.35.0:
      Successfully uninstalled llvmlite-0.35.0
  Attempting uninstall: sentencepiece
    Found existing installation: sentencepiece 0.1.95
    Uninstalling sentencepiece-0.1.95:
      Successfully uninstalled sentencepiece-0.1.95
  Attempting uninstall: numba
    Found existing installation: numba 0.52.0
    Uninstalling numba-0.52.0:
      Successfully uninstalled numba-0.52.0
  Attempting uninstall: joblib
    Found existing installation: joblib 1.0.0
    Uninstalling joblib-1.0.0:
      Successfully uninstalled joblib-1.0.0
  Attempting uninstall: cffi
    Found existing installation: cffi 1.14.5
    Uninstalling cffi-1.14.5:
      Successfully uninstalled cffi-1.14.5
Successfully installed apex-0.1 cffi-1.14.3 joblib-0.17.0 llvmlite-0.32.1 numba-0.43.0 pyrouge-0.1.3 sentencepiece-0.1.94 subword-nmt-0.3.7
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpenNMT-py$
```

## Preparing the Data

Machine translation မလုပ်ခင်မှာ အမြဲတမ်း လုပ်ရတာကတော့ data preparation ပါ။  
ဒီနေရာမှာတော့ အဆင်သင့်ရှိပြီးသားဖြစ်တဲ့ English-Germany parallel corpus ကို download လုပ်ပြီးသုံးပါမယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT$ mkdir tutorial
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT$ cd tutorial
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ wget https://s3.amazonaws.com/opennmt-trainingdata/toy-ende.tar.gz
--2021-03-20 23:55:16--  https://s3.amazonaws.com/opennmt-trainingdata/toy-ende.tar.gz
Resolving s3.amazonaws.com (s3.amazonaws.com)... 54.231.98.123
Connecting to s3.amazonaws.com (s3.amazonaws.com)|54.231.98.123|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1662081 (1.6M) [application/x-gzip]
Saving to: ‘toy-ende.tar.gz’

toy-ende.tar.gz                       100%[=========================================================================>]   1.58M   469KB/s    in 3.5s    

2021-03-20 23:55:20 (469 KB/s) - ‘toy-ende.tar.gz’ saved [1662081/1662081]

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$
```

## Extract .tar.gz

tar.gz ဖိုင်ကို အောက်ပါအတိုင်း ဖြေပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ tar xf toy-ende.tar.gz
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ cd toy-ende/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ ls
src-test.txt  src-train.txt  src-val.txt  tgt-test.txt  tgt-train.txt  tgt-val.txt
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ 
```

## Check the Data

Training ဒေတာက စာကြောင်းရေ တစ်သောင်းပဲရှိတဲ့ parallel corpus အသေးလေးပါ။ validation data က စာကြောင်းရေ သုံးထောင်ဖြစ်ပြီးတော့၊ test data ကတော့ နှစ်ထောင့်ခုနှစ်ရာကျော်ရှိပါတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ wc *
   2737   61376  344699 src-test.txt
  10000  225069 1253552 src-train.txt
   3000   72088  399012 src-val.txt
   2737   57659  375812 tgt-test.txt
  10000  213992 1414977 tgt-train.txt
   3000   71666  463304 tgt-val.txt
  31474  701850 4251356 total
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ head *
==> src-test.txt <==
Orlando Bloom and Miranda Kerr still love each other
Actors Orlando Bloom and Model Miranda Kerr want to go their separate ways .
However , in an interview , Bloom has said that he and Kerr still love each other .
Miranda Kerr and Orlando Bloom are parents to two-year-old Flynn .
Actor Orlando Bloom announced his separation from his wife , supermodel Miranda Kerr .
In an interview with US journalist Katie Couric , which is to be broadcast on Friday (local time), Bloom said , &quot; sometimes life doesn &apos;t go exactly as we plan or hope for &quot; .
He and Kerr still love each other , emphasised the 36-year-old .
&quot; We &apos;re going to support one another and love each other as parents to Flynn &quot; .
Kerr and Bloom have been married since 2010 . Their son Flynn was born in 2011 .
Jet makers feud over seat width with big orders at stake

==> src-train.txt <==
It is not acceptable that , with the help of the national bureaucracies , Parliament &apos;s legislative prerogative should be made null and void by means of implementing provisions whose content , purpose and extent are not laid down in advance .
Federal Master Trainer and Senior Instructor of the Italian Federation of Aerobic Fitness , Group Fitness , Postural Gym , Stretching and Pilates; from 2004 , he has been collaborating with Antiche Terme as personal Trainer and Instructor of Stretching , Pilates and Postural Gym .
&quot; Two soldiers came up to me and told me that if I refuse to sleep with them , they will kill me . They beat me and ripped my clothes .
Yes , we also say that the European budget is not about the duplication of national budgets , but about delivering common goals beyond the capacity of nation states where European funds can realise economies of scale or create synergies .
The name of this site , and program name Title purchased will not be displayed .
They would be abiding by the principle of the UN , which precludes military action except in self-defence , which does not apply here .
rapporteur . - (FR) Mr President , representatives of the Council and the Commission , ladies and gentlemen , I should like to begin by thanking my colleagues , who entrusted me with this report , and the shadow rapporteur for their respective contributions .
Shortly thereafter , Mårthen Cedergran , who had been responsible for vocals , left Bombshell Rocks to establish himself as a tattoo artist .
The next item should be the presentation by the Commission of the preliminary draft budget for 2001 .
This is about as much as we can hope for within the confines of the common fisheries policy .

==> src-val.txt <==
Parliament Does Not Support Amendment Freeing Tymoshenko
Today , the Ukraine parliament dismissed , within the Code of Criminal Procedure amendment , the motion to revoke an article based on which the opposition leader , Yulia Tymoshenko , was sentenced .
The amendment that would lead to freeing the imprisoned former Prime Minister was revoked during second reading of the proposal for mitigation of sentences for economic offences .
In October , Tymoshenko was sentenced to seven years in prison for entering into what was reported to be a disadvantageous gas deal with Russia .
The verdict is not yet final; the court will hear Tymoshenko &apos;s appeal in December .
Tymoshenko claims the verdict is a political revenge of the regime; in the West , the trial has also evoked suspicion of being biased .
The proposal to remove Article 365 from the Code of Criminal Procedure , upon which the former Prime Minister was sentenced , was supported by 147 members of parliament .
Its ratification would require 226 votes .
Libya &apos;s Victory
The story of Libya &apos;s liberation , or rebellion , already has its defeated .

==> tgt-test.txt <==
Orlando Bloom und Miranda Kerr lieben sich noch immer
Schauspieler Orlando Bloom und Model Miranda Kerr wollen künftig getrennte Wege gehen .
In einem Interview sagte Bloom jedoch , dass er und Kerr sich noch immer lieben .
Miranda Kerr und Orlando Bloom sind Eltern des zweijährigen Flynn .
Schauspieler Orlando Bloom hat sich zur Trennung von seiner Frau , Topmodel Miranda Kerr , geäußert .
In einem Interview mit US-Journalistin Katie Couric , das am Freitag (Ortszeit) ausgestrahlt werden sollte , sagte Bloom , &quot; das Leben verläuft manchmal nicht genau so , wie wir es planen oder erhoffen &quot; .
Kerr und er selbst liebten sich noch immer , betonte der 36-Jährige .
&quot; Wir werden uns gegenseitig unterstützen und lieben als Eltern von Flynn &quot; .
Kerr und Bloom sind seit 2010 verheiratet , im Jahr 2011 wurde ihr Söhnchen Flynn geboren .
Jumbo-Hersteller streiten im Angesicht großer Bestellungen über Sitzbreite

==> tgt-train.txt <==
Es geht nicht an , dass über Ausführungsbestimmungen , deren Inhalt , Zweck und Ausmaß vorher nicht bestimmt ist , zusammen mit den nationalen Bürokratien das Gesetzgebungsrecht des Europäischen Parlaments ausgehebelt wird .
Meistertrainer und leitender Dozent des italienischen Fitnessverbands für Aerobic , Gruppenfitness , Haltungsgymnastik , Stretching und Pilates; arbeitet seit 2004 bei Antiche Terme als Personal Trainer und Lehrer für Stretching , Pilates und Rückengymnastik .
Also kam ich nach Südafrika " , erzählte eine Frau namens Grace dem Human Rights Watch-Mitarbeiter Gerry Simpson , der die Probleme der zimbabwischen Flüchtlinge in Südafrika untersucht .
Ja , wir sagen auch , dass es beim europäischen Haushalt nicht um die Vervielfältigung der nationalen Haushalte geht , sondern um das Erreichen gemeinsamer Ziele , die über die Kapazität von Nationalstaaten hinausgehen , wo die europäischen Finanzmittel Rationalisierungseffekte oder Synergieeffekte erzeugen .
Der Name dieser Seite , Namen und Programm-Titel erworben werden nicht angezeigt .
Sie würden an dem Prinzip der UNO festhalten , nach dem militärische Aktionen außer im Falle der Selbstverteidigung , der beim Irak nicht zutrifft , ausgeschlossen sind .
Berichterstatter . - (FR) Herr Präsident , sehr geehrte Vertreter des Rates und der Kommission , meine Damen und Herren ! Ich möchte gleich eingangs meinen Kollegen , die mich mit diesem Bericht betraut haben , sowie dem Schattenberichterstatter für ihre jeweiligen Beiträge danken .
Kurze Zeit später verlässt der bis dato für den Gesang verantwortliche Mårthen Cedergran die Bombshell Rocks , um sich als Tätowierer selbständig zu machen .
Nach der Tagesordnung sollte die Kommission den Vorentwurf des Gesamthaushaltsplans für das Jahr 2001 vorlegen .
Das ist etwa soviel , wie wir innerhalb der Grenzen der Gemeinsamen Fischereipolitik erwarten können .

==> tgt-val.txt <==
Keine befreiende Novelle für Tymoshenko durch das Parlament
Das ukrainische Parlament verweigerte heute den Antrag , im Rahmen einer Novelle des Strafgesetzbuches denjenigen Paragrafen abzuschaffen , auf dessen Grundlage die Oppositionsführerin Yulia Timoshenko verurteilt worden war .
Die Neuregelung , die den Weg zur Befreiung der inhaftierten Expremierministerin hätte ebnen können , lehnten die Abgeordneten bei der zweiten Lesung des Antrags auf Milderung der Strafen für wirtschaftliche Delikte ab .
Timoshenko war im Oktober wegen des Abschlusses eines angeblich nachteiligen Vertrags mit Russland über den Einkauf von Erdgas zu sieben Jahren Haft verurteilt worden .
Das Urteil ist noch nicht rechtskräftig , im Dezember soll die Berufung der Verurteilten vor Gericht verhandelt werden .
Timoshenko selbst bezeichnet das Urteil als politische Rache des Regimes und auch im Westen ließ der Prozess den Verdacht der Voreingenommenheit des Gerichts aufkommen .
Der Antrag , Paragraf 365 , auf dessen Grundlage die Expremierministerin verurteilt wurde , aus dem Strafgesetzbuch zu entfernen , wurde von 147 Abgeordneten unterstützt .
226 Stimmen wären zu seiner Annahme erforderlich gewesen .
Libyscher Sieg
Die Geschichte des libyschen Befreiungskampfes oder libyschen Rebellion kennt schon ihre Verlierer .
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ 
```

## Preparing config file

Toy config ဖိုင်ကို လေ့လာကြည့်ပါ။  

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ cat ./toy_en_de.yaml 

```
# toy_en_de.yaml

## Where the samples will be written
save_data: toy-ende/run/example
## Where the vocab(s) will be written
src_vocab: toy-ende/run/example.vocab.src
tgt_vocab: toy-ende/run/example.vocab.tgt
# Prevent overwriting existing files in the folder
overwrite: False

# Corpus opts:
data:
    corpus_1:
        path_src: toy-ende/src-train.txt
        path_tgt: toy-ende/tgt-train.txt
    valid:
        path_src: toy-ende/src-val.txt
        path_tgt: toy-ende/tgt-val.txt
        
# Vocabulary files that were just created
src_vocab: toy-ende/run/example.vocab.src
tgt_vocab: toy-ende/run/example.vocab.tgt

# Train on a single GPU
world_size: 1
gpu_ranks: [0]

# Where to save the checkpoints
save_model: toy-ende/run/model
save_checkpoint_steps: 500
train_steps: 1000
valid_steps: 500
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$
```

## Building Vocabs

NMT အတွက်က vocab dictionary အရင်ဆောက်ဖို့ လိုအပ်ပါတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ time onmt_build_vocab -config toy_en_de.yaml -n_sample 10000
Corpus corpus_1's weight should be given. We default it to 1 for you.
[2021-03-21 00:19:12,363 INFO] Counter vocab from 10000 samples.
[2021-03-21 00:19:12,363 INFO] Build vocab on 10000 transformed examples/corpus.
[2021-03-21 00:19:12,368 INFO] corpus_1's transforms: TransformPipe()
[2021-03-21 00:19:12,368 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:19:12,570 INFO] Counters src:24995
[2021-03-21 00:19:12,570 INFO] Counters tgt:35816

real	0m0.708s
user	0m0.602s
sys	0m0.060s
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ 
```

## Training

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ time onmt_train -config toy_en_de.yaml
[2021-03-21 00:28:48,357 INFO] Missing transforms field for corpus_1 data, set to default: [].
[2021-03-21 00:28:48,357 WARNING] Corpus corpus_1's weight should be given. We default it to 1 for you.
[2021-03-21 00:28:48,357 INFO] Missing transforms field for valid data, set to default: [].
[2021-03-21 00:28:48,357 INFO] Parsed 2 corpora from -data.
[2021-03-21 00:28:48,357 INFO] Get special vocabs from Transforms: {'src': set(), 'tgt': set()}.
[2021-03-21 00:28:48,358 INFO] Loading vocab from text file...
[2021-03-21 00:28:48,358 INFO] Loading src vocabulary from toy-ende/run/example.vocab.src
[2021-03-21 00:28:48,392 INFO] Loaded src vocab has 24995 tokens.
[2021-03-21 00:28:48,399 INFO] Loading tgt vocabulary from toy-ende/run/example.vocab.tgt
[2021-03-21 00:28:48,467 INFO] Loaded tgt vocab has 35816 tokens.
[2021-03-21 00:28:48,477 INFO] Building fields with vocab in counters...
[2021-03-21 00:28:48,512 INFO]  * tgt vocab size: 35820.
[2021-03-21 00:28:48,537 INFO]  * src vocab size: 24997.
[2021-03-21 00:28:48,539 INFO]  * src vocab size = 24997
[2021-03-21 00:28:48,539 INFO]  * tgt vocab size = 35820
[2021-03-21 00:28:48,541 INFO] Building model...
[2021-03-21 00:28:51,293 INFO] NMTModel(
  (encoder): RNNEncoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(24997, 500, padding_idx=1)
        )
      )
    )
    (rnn): LSTM(500, 500, num_layers=2, dropout=0.3)
  )
  (decoder): InputFeedRNNDecoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(35820, 500, padding_idx=1)
        )
      )
    )
    (dropout): Dropout(p=0.3, inplace=False)
    (rnn): StackedLSTM(
      (dropout): Dropout(p=0.3, inplace=False)
      (layers): ModuleList(
        (0): LSTMCell(1000, 500)
        (1): LSTMCell(500, 500)
      )
    )
    (attn): GlobalAttention(
      (linear_in): Linear(in_features=500, out_features=500, bias=False)
      (linear_out): Linear(in_features=1000, out_features=500, bias=False)
    )
  )
  (generator): Sequential(
    (0): Linear(in_features=500, out_features=35820, bias=True)
    (1): Cast()
    (2): LogSoftmax(dim=-1)
  )
)
[2021-03-21 00:28:51,293 INFO] encoder: 16506500
[2021-03-21 00:28:51,293 INFO] decoder: 41613820
[2021-03-21 00:28:51,293 INFO] * number of parameters: 58120320
[2021-03-21 00:28:51,294 INFO] Starting training on GPU: [0]
[2021-03-21 00:28:51,294 INFO] Start training loop and validate every 500 steps...
[2021-03-21 00:28:51,294 INFO] corpus_1's transforms: TransformPipe()
[2021-03-21 00:28:51,294 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:29:15,279 INFO] Step 50/ 1000; acc:   3.91; ppl: 147677.56; xent: 11.90; lr: 1.00000; 2954/2927 tok/s;     24 sec
[2021-03-21 00:29:41,072 INFO] Step 100/ 1000; acc:   4.28; ppl: 21049.63; xent: 9.95; lr: 1.00000; 2906/2886 tok/s;     50 sec
[2021-03-21 00:29:55,000 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:30:06,571 INFO] Step 150/ 1000; acc:   7.72; ppl: 6473.50; xent: 8.78; lr: 1.00000; 2801/2801 tok/s;     75 sec
[2021-03-21 00:30:33,136 INFO] Step 200/ 1000; acc:   8.12; ppl: 2778.93; xent: 7.93; lr: 1.00000; 2728/2705 tok/s;    102 sec
[2021-03-21 00:31:00,180 INFO] Step 250/ 1000; acc:   9.11; ppl: 2196.77; xent: 7.69; lr: 1.00000; 2618/2604 tok/s;    129 sec
[2021-03-21 00:31:20,640 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:31:27,649 INFO] Step 300/ 1000; acc:   8.51; ppl: 1950.40; xent: 7.58; lr: 1.00000; 2648/2656 tok/s;    156 sec
[2021-03-21 00:31:54,726 INFO] Step 350/ 1000; acc:   9.74; ppl: 1610.59; xent: 7.38; lr: 1.00000; 2654/2636 tok/s;    183 sec
[2021-03-21 00:32:21,583 INFO] Step 400/ 1000; acc:   9.68; ppl: 1502.00; xent: 7.31; lr: 1.00000; 2668/2633 tok/s;    210 sec
[2021-03-21 00:32:47,674 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:32:48,790 INFO] Step 450/ 1000; acc:  10.23; ppl: 1276.15; xent: 7.15; lr: 1.00000; 2640/2654 tok/s;    237 sec
[2021-03-21 00:33:15,247 INFO] Step 500/ 1000; acc:  11.40; ppl: 1131.68; xent: 7.03; lr: 1.00000; 2717/2701 tok/s;    264 sec
[2021-03-21 00:33:15,248 INFO] valid's transforms: TransformPipe()
[2021-03-21 00:33:15,248 INFO] Loading ParallelCorpus(toy-ende/src-val.txt, toy-ende/tgt-val.txt, align=None)...
[2021-03-21 00:33:29,272 INFO] Validation perplexity: 1604.68
[2021-03-21 00:33:29,272 INFO] Validation accuracy: 6.57595
[2021-03-21 00:33:29,428 INFO] Saving checkpoint toy-ende/run/model_step_500.pt
[2021-03-21 00:33:57,207 INFO] Step 550/ 1000; acc:  11.68; ppl: 1035.14; xent: 6.94; lr: 1.00000; 1725/1703 tok/s;    306 sec
[2021-03-21 00:34:23,567 INFO] Step 600/ 1000; acc:  12.27; ppl: 909.96; xent: 6.81; lr: 1.00000; 2703/2708 tok/s;    332 sec
[2021-03-21 00:34:27,965 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:34:49,969 INFO] Step 650/ 1000; acc:  12.82; ppl: 836.26; xent: 6.73; lr: 1.00000; 2772/2753 tok/s;    359 sec
[2021-03-21 00:35:16,797 INFO] Step 700/ 1000; acc:  13.62; ppl: 769.12; xent: 6.65; lr: 1.00000; 2698/2671 tok/s;    386 sec
[2021-03-21 00:35:43,239 INFO] Step 750/ 1000; acc:  13.78; ppl: 732.43; xent: 6.60; lr: 1.00000; 2714/2715 tok/s;    412 sec
[2021-03-21 00:35:52,202 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:36:09,068 INFO] Step 800/ 1000; acc:  14.26; ppl: 654.65; xent: 6.48; lr: 1.00000; 2755/2755 tok/s;    438 sec
[2021-03-21 00:36:35,706 INFO] Step 850/ 1000; acc:  15.18; ppl: 613.27; xent: 6.42; lr: 1.00000; 2670/2639 tok/s;    464 sec
[2021-03-21 00:37:03,539 INFO] Step 900/ 1000; acc:  15.05; ppl: 571.68; xent: 6.35; lr: 1.00000; 2663/2660 tok/s;    492 sec
[2021-03-21 00:37:18,324 INFO] Loading ParallelCorpus(toy-ende/src-train.txt, toy-ende/tgt-train.txt, align=None)...
[2021-03-21 00:37:30,486 INFO] Step 950/ 1000; acc:  15.79; ppl: 525.61; xent: 6.26; lr: 1.00000; 2663/2662 tok/s;    519 sec
[2021-03-21 00:37:56,977 INFO] Step 1000/ 1000; acc:  15.78; ppl: 502.18; xent: 6.22; lr: 1.00000; 2749/2705 tok/s;    546 sec
[2021-03-21 00:37:56,977 INFO] Loading ParallelCorpus(toy-ende/src-val.txt, toy-ende/tgt-val.txt, align=None)...
[2021-03-21 00:38:11,280 INFO] Validation perplexity: 1008.72
[2021-03-21 00:38:11,280 INFO] Validation accuracy: 14.1818
[2021-03-21 00:38:11,455 INFO] Saving checkpoint toy-ende/run/model_step_1000.pt

real	9m24.291s
user	8m38.686s
sys	0m44.289s
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$
```

Check the folder...

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ cd toy-ende/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ ls
run  src-test.txt  src-train.txt  src-val.txt  tgt-test.txt  tgt-train.txt  tgt-val.txt
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ cd run/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende/run$ ls
example.vocab.src  example.vocab.tgt  model_step_1000.pt  model_step_500.pt
```

## Translate

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ time onmt_translate -model toy-ende/run/model_step_1000.pt -src toy-ende/src-test.txt -output toy-ende/pred_1000.txt -gpu 0 -verbose | tee translate.log
...
...
...
[2021-03-21 00:50:24,516 INFO] 
SENT 2732: ['FAA', 'advisory', 'committee', 'members', 'expressed', 'mixed', 'feelings', 'about', 'whether', 'use', 'of', 'the', 'devices', 'presents', 'any', 'risk', '.']
PRED 2732: Sie haben nicht , dass , dass es nicht , dass , dass es nicht , dass es in den Mitgliedstaaten , dass es nicht , dass es in den Mitgliedstaaten , dass es nicht , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es nicht , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es nicht , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es nicht , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den
PRED SCORE: -223.4119

[2021-03-21 00:50:24,516 INFO] 
SENT 2733: ['Douglas', 'Kidd', 'of', 'the', 'National', 'Association', 'of', 'Airline', 'Passengers', 'said', 'he', 'believes', 'interference', 'from', 'the', 'devices', 'is', 'genuine', 'even', 'if', 'the', 'risk', 'is', 'minimal', '.']
PRED 2733: Sie haben nicht , dass , dass es nicht , dass , dass es in den Mitgliedstaaten , dass es nicht , dass es nicht , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es in den Mitgliedstaaten , dass es
PRED SCORE: -223.7879

[2021-03-21 00:50:24,517 INFO] 
SENT 2734: ['Other', 'committee', 'members', 'said', 'there', 'are', 'only', 'anecdotal', 'reports', 'from', 'pilots', 'to', 'support', 'that', 'the', 'devices', 'can', 'interfere', 'with', 'aircraft', 'systems', ',', 'and', 'most', 'of', 'those', 'reports', 'are', 'very', 'old', '.']
PRED 2734: Die Kommission ist nicht , dass , dass es nicht , dass , dass es nicht , dass , dass es , dass , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es nicht , dass es in den
PRED SCORE: -215.4642

[2021-03-21 00:50:24,517 INFO] 
SENT 2735: ['However', ',', 'the', 'committee', 'recommended', 'the', 'FAA', 'allow', 'pilots', 'to', 'order', 'passengers', 'to', 'shut', 'off', 'devices', 'during', 'instrument', 'landings', 'in', 'low', 'visibility', '.']
PRED 2735: Es ist nicht , dass , dass wir nicht , dass , dass wir nicht , dass , dass wir nicht , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass es , dass , dass
PRED SCORE: -179.9455

[2021-03-21 00:50:24,517 INFO] 
SENT 2736: ['A', 'travel', 'industry', 'group', 'welcomed', 'the', 'changes', ',', 'calling', 'them', 'common-sense', 'accommodations', 'for', 'a', 'traveling', 'public', 'now', 'bristling', 'with', 'technology', '.']
PRED 2736: Es ist nicht , dass , dass Sie nicht , dass , dass es nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht , dass Sie nicht ,
PRED SCORE: -220.1446

[2021-03-21 00:50:24,517 INFO] 
SENT 2737: ['&quot;', 'We', '&apos;re', 'pleased', 'the', 'FAA', 'recognizes', 'that', 'an', 'enjoyable', 'passenger', 'experience', 'is', 'not', 'incompatible', 'with', 'safety', 'and', 'security', ',', '&quot;', 'said', 'Roger', 'Dow', ',', 'CEO', 'of', 'the', 'U.S.', 'Travel', 'Association', '.']
PRED 2737: Wir haben nicht , dass wir uns , dass wir uns , dass wir nicht , dass wir nicht , dass wir nicht , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den Mitgliedstaaten , dass wir in den
PRED SCORE: -193.0609

[2021-03-21 00:50:24,517 INFO] PRED AVG SCORE: -2.0628, PRED PPL: 7.8682

real	3m1.507s
user	3m2.472s
sys	0m0.648s
```

## Release

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ onmt_release_model --model toy-ende/run/model_step_1000.pt --output toy-ende/run/model_step_1000_release.pt
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ ls ./toy-ende/run/
example.vocab.src  example.vocab.tgt  model_step_1000.pt  model_step_1000_release.pt  model_step_500.pt
```

---

အထက်မှာလုပ်ပြခဲ့တာက OpenNMT ရဲ့ Github မှာလည်း ဥပမာအနေနဲ့ OpenNMT ကို ဘယ်လိုသုံးရမလဲ ဆိုတဲ့ tutorial ကိုအခြေခံပြီး ကိုယ့်စက်ထဲမှာ run ကြည့်တဲ့ပုံစံပါ။  
အခု ဆက်လုပ်သွားမှာက MT share task အတွက် ပြင်ဆင်နေတဲ့ အင်္ဂလိပ်စာ-မြန်မာစာ corpus ကို သုံးပြီး neural machine translation လုပ်တာကိုပါ။ မြန်မာစာ NLP R&D ကို စိတ်ဝင်စားတဲ့ ကျောင်းသား/သူ တွေ လေ့လာနိုင်အောင် လုပ်ပြထားတာဖြစ်ပါတယ်။  

## Copying configuration file for Transformer architecture

OpenNMT က transformer architecture NMT အတွက် ဥပမာအနေနဲ့ ပြင်ဆင်ပေးထားတဲ့ configuration ဖိုင်ကို အရင်ဆုံးကော်ပီကူးယူခဲ့တယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/OpenNMT-py/config$ cp config-transformer-base-1GPU.yml /home/ye/exp/nmt/openNMT/wat2021/exp-syl4/
```

## Check the Data

Corpus information (training, developing, testing files) ကတော့ အောက်ပါအတိုင်းပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data$ wc *.{en,my}
    1018    27929   151447 test.en
  238014  3357260 17186660 train.en
    1000    27318   147768 valid.en
    1018    58895   561443 test.my
  238014  6285996 60847350 train.my
    1000    57709   550454 valid.my
  480064  9815107 79445122 total
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data$ head -n 3 *.my
==> test.my <==
ဆစ် ဒ နီ က ရ န့် ဝစ်ခ် မြင်း ပြိုင် ကွင်း မှ မျိုး သ န့် ပြိုင် မြင်း ရှစ် ကောင် ဟာ မြင်း တုတ် ကွေး ရော ဂါ ကူး စက် ခံ ခဲ့ ရ တယ် ဆို တာ အ တည် ပြု ခဲ့ ပါ တယ် ။
ရ န့် ဝစ်ခ် ကို ပိတ် ထား ခဲ့ ပြီး ၂ လ အ ထိ ကြာ ကြာ ဆက် လက် ထိန်း သိမ်း ထား ရန် မျှော် လ င့် ပါ တယ် ။
အ လွန် ပြင်း ထန် သော တုတ် ကွေး ဟာ ရ န့် ဝစ်ခ် မှာ အ မြဲ ထား သော မြင်း ၇၀၀ ထဲ က အ များ စု ကို ကူး စက် လိ မ့် မည် လို့ ခ န့် မှန်း ထား ပါ တယ် ။

==> train.my <==
ကြိမ် ချောင်း ရဲ စ ခန်း တွင် လူ သတ် မှု ဖြ င့် အ မှု ဖွ င့် ထား ပြီး ပြီ ။
ရဲ များ က စုံ စမ်း လျက် ရှိ သည် ။
တပ် မ တော် တပ် ဖွဲ့ သည် ရှမ်း ပြည် နယ် မြောက် ပိုင်း တာ မိုး ညဲ မြို့ ၌ မ နေ့ က ရှောင် တ ခင် စစ် ဆေး မှု တစ် ခု ပြု လုပ် စဉ် အ တွင်း ယာဉ် တစ် စီး မှ လက် နက် များ နှ င့် တ ရား မ ဝင် သစ် များ ကို ဖမ်း ဆီး ရ မိ ခဲ့ သည် ။

==> valid.my <==
&quot; သူ ၏ ဆုံး ပါး ခြင်း အ တွက် ကျွန် တော် တို့ ဝမ်း နည်း သော် လည်း ၊ လူ မျိုး ရေး နှ င့် ဘာ သာ ရေး ရန် စွယ် ကို နှိုး ဆွ ပေး သော အ မွေ အ နှစ် တစ် ခု ကို သူ ချန် ထား ခဲ့ သည် ။ &quot;
ပါ ကစ္စ တန် နိုင် ငံ ၏ ဝတ် ဇီ ရီ စ တန် မြောက် ပိုင်း ရှိ ၊ လူ က ထိန်း ရန် မ လို သော စစ် လေ ယာဉ် မှ ပစ် ခတ် ခြင်း အ နေ ဖြ င့် ယ ခု သတ် မှတ် ထား သော ၊ အ မေ ရိ ကန် ပြည် ထောင် စု ဒုံး ကျည် ဖြ င့် ၊ သူ့ ကို ထိ ခိုက် စေ ခဲ့ သည် ဟု ထင် ကြေး ပေး ခဲ့ ပြီး နောက် နောက် ထပ် အ လွန် များ ပြား သော စစ် သွေး ကြွ များ လည်း သေ ဆုံး ကြောင်း သ တင်း ပို့ ခဲ့ သည် ။
&quot; လူ က ထိန်း ရန် မ လို သော လေ ယာဉ် မှ ပစ် ခတ် ရန် ဒုံး ကျည် ပေါ် ပေါက် ခဲ့ သည် ၊ &quot; ဟု ပါ ကစ္စ တန် သ တင်း ထောက် လှမ်း ရေး အ ရာ ရှိ တစ် ယောက် က ပြော ခဲ့ သည် ။
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data$ head -n 3 *.en
==> test.en <==
It has been confirmed that eight thoroughbred race horses at Randwick Racecourse in Sydney have been infected with equine influenza .
Randwick has been locked down , and is expected to remain so for up to two months .
It is expected that the virulent flu will affect the majority of the 700 horses stabled at Randwick .

==> train.en <==
A murder case has been opened at the Kyeikgyaung police station .
Police are investigating .
Tatmadaw troops seized arms and illegal timber from a vehicle during a surprise check in Tarmoenyae in northern Shan state yesterday .

==> valid.en <==
&amp; quot ; Though we are sad for his loss , he left a legacy that will inflame the enemy nation and religion . &amp; quot ;
It is speculated that he was hit by a United States missile , which is now identified as being fired from a Predator drone , in the North Waziristan of Pakistan , and a dozen more militants were also reported dead .
&amp; quot ; The missile appeared to have been fired by a drone , &amp; quot ; said a Pakistani intelligence official .
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data$
```

## Editing config file

for running transformer model with WAT2021 data, I have to edit the config file ...  
configuration ဖိုင်မှာအဓိက update လုပ်ရတာကတော့ ကိုယ်သုံးမယ့် corpus (i.e. training/validation) ဖိုင်နာမည်တွေကိုပါ။  
update လုပ်ထားတဲ့ configuration ဖိုင်ကတော့ အောက်ပါအတိုင်းပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$ cat ./config-transformer-wat2021.yml 
## Based on the config-transformer-base-1GPU.yml, I updated for WAT2021 NMT esperiment
## Updated by Ye Kyaw Thu, LST, NECTEC, Thailand
## 21 Mar2021
## 

## Where the samples will be written
save_data: data/run/transformer
## Where the vocab(s) will be written
src_vocab: data/run/transformer.vocab.src
tgt_vocab: data/run/transformer.vocab.tgt
# Prevent overwriting existing files in the folder
overwrite: False

# Corpus opts:
data:
    corpus_1:
        path_src: data/train.en
        path_tgt: data/train.my
    valid:
        path_src: data/valid.en
        path_tgt: data/valid.my
        
# Vocabulary files that were just created
src_vocab: data/run/transformer.vocab.src
tgt_vocab: data/run/transformer.vocab.tgt

save_model: exp/transformer1.en-my
save_checkpoint_steps: 10000
keep_checkpoint: 10
seed: 3435
train_steps: 500000
valid_steps: 10000
warmup_steps: 8000
report_every: 100

decoder_type: transformer
encoder_type: transformer
word_vec_size: 512
rnn_size: 512
layers: 6
transformer_ff: 2048
heads: 8

accum_count: 8
optim: adam
adam_beta1: 0.9
adam_beta2: 0.998
decay_method: noam
learning_rate: 2.0
max_grad_norm: 0.0

#batch_size: 4096
batch_size: 64
batch_type: tokens
normalization: tokens
dropout: 0.1
label_smoothing: 0.1

max_generator_batches: 2

param_init: 0.0
param_init_glorot: 'true'
position_encoding: 'true'

world_size: 1
## Run with GPU no. zero
gpu_ranks: [0]

```

## Building Vocabs

onmt_build_vocab နဲ့ source, target language-pair အတွက် vocab building လုပ်မယ်။  
-config option နဲ့ စောစောက update လုပ်ထားခဲ့တဲ့ configuration ဖိုင်ကိုတော့ argument passing လုပ်ပေးရလိမ့်မယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$ time onmt_build_vocab -config ./config-transformer-wat2021.yml -n_sample 10000
Corpus corpus_1's weight should be given. We default it to 1 for you.
[2021-03-21 02:29:27,542 INFO] Counter vocab from 10000 samples.
[2021-03-21 02:29:27,542 INFO] Build vocab on 10000 transformed examples/corpus.
[2021-03-21 02:29:27,547 INFO] corpus_1's transforms: TransformPipe()
[2021-03-21 02:29:27,547 INFO] Loading ParallelCorpus(data/train.en, data/train.my, align=None)...
[2021-03-21 02:29:27,849 INFO] Counters src:11588
[2021-03-21 02:29:27,849 INFO] Counters tgt:2538

real	0m0.747s
user	0m0.588s
sys	0m0.053s
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$
```

Vocab ဖိုင်ကို head command နဲ့ ကြည့်ကြည့်ရင် အောက်ပါအတိုင်း မြင်ရလိမ့်မယ်။  
Check the Vocabs...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data/run$ head *
==> transformer.vocab.src <==
the	17622
.	9630
of	9142
,	8102
and	7332
to	5909
in	4058
The	2447
for	2275
a	2174

==> transformer.vocab.tgt <==
အ	26656
င့်	11634
သည်	10256
များ	10223
။	10002
ရေး	6817
သ	6671
ကို	6440
ပါ	6216
ရ	6164

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/data/run$ wc *
 11588  23176 122798 transformer.vocab.src
  2538   5076  37987 transformer.vocab.tgt
 14126  28252 160785 total
```

## Start Training and Got ERROR

Transofmer architecture နဲ့ training လုပ်ကြည့်တဲ့အခါမှာ အောက်ပါအတိုင်း error ပေးတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$ time onmt_train -config ./config-transformer-wat2021.yml 
[2021-03-21 02:40:55,268 INFO] Missing transforms field for corpus_1 data, set to default: [].
[2021-03-21 02:40:55,268 WARNING] Corpus corpus_1's weight should be given. We default it to 1 for you.
[2021-03-21 02:40:55,268 INFO] Missing transforms field for valid data, set to default: [].
[2021-03-21 02:40:55,268 INFO] Parsed 2 corpora from -data.
[2021-03-21 02:40:55,268 INFO] Get special vocabs from Transforms: {'src': set(), 'tgt': set()}.
[2021-03-21 02:40:55,268 INFO] Loading vocab from text file...
[2021-03-21 02:40:55,268 INFO] Loading src vocabulary from data/run/transformer.vocab.src
[2021-03-21 02:40:55,285 INFO] Loaded src vocab has 11588 tokens.
[2021-03-21 02:40:55,288 INFO] Loading tgt vocabulary from data/run/transformer.vocab.tgt
[2021-03-21 02:40:55,292 INFO] Loaded tgt vocab has 2538 tokens.
[2021-03-21 02:40:55,293 INFO] Building fields with vocab in counters...
[2021-03-21 02:40:55,295 INFO]  * tgt vocab size: 2542.
[2021-03-21 02:40:55,306 INFO]  * src vocab size: 11590.
[2021-03-21 02:40:55,306 INFO]  * src vocab size = 11590
[2021-03-21 02:40:55,306 INFO]  * tgt vocab size = 2542
[2021-03-21 02:40:55,308 INFO] Building model...
[2021-03-21 02:40:57,258 INFO] NMTModel(
  (encoder): TransformerEncoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(11590, 512, padding_idx=1)
        )
        (pe): PositionalEncoding(
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (transformer): ModuleList(
      (0): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (1): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (2): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (3): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (4): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (5): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
    )
    (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
  )
  (decoder): TransformerDecoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(2542, 512, padding_idx=1)
        )
        (pe): PositionalEncoding(
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
    (transformer_layers): ModuleList(
      (0): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (1): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (2): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (3): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (4): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (5): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
    )
  )
  (generator): Sequential(
    (0): Linear(in_features=512, out_features=2542, bias=True)
    (1): Cast()
    (2): LogSoftmax(dim=-1)
  )
)
[2021-03-21 02:40:57,260 INFO] encoder: 24849408
[2021-03-21 02:40:57,260 INFO] decoder: 27830766
[2021-03-21 02:40:57,260 INFO] * number of parameters: 52680174
[2021-03-21 02:40:57,262 INFO] Starting training on GPU: [0]
[2021-03-21 02:40:57,262 INFO] Start training loop and validate every 10000 steps...
[2021-03-21 02:40:57,262 INFO] corpus_1's transforms: TransformPipe()
[2021-03-21 02:40:57,262 INFO] Loading ParallelCorpus(data/train.en, data/train.my, align=None)...
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/py3.6env/bin/onmt_train", line 33, in <module>
    sys.exit(load_entry_point('OpenNMT-py', 'console_scripts', 'onmt_train')())
  File "/home/ye/tool/OpenNMT-py/onmt/bin/train.py", line 169, in main
    train(opt)
  File "/home/ye/tool/OpenNMT-py/onmt/bin/train.py", line 154, in train
    train_process(opt, device_id=0)
  File "/home/ye/tool/OpenNMT-py/onmt/train_single.py", line 112, in main
    valid_steps=opt.valid_steps)
  File "/home/ye/tool/OpenNMT-py/onmt/trainer.py", line 244, in train
    report_stats)
  File "/home/ye/tool/OpenNMT-py/onmt/trainer.py", line 368, in _gradient_accumulation
    with_align=self.with_align)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 722, in _call_impl
    result = self.forward(*input, **kwargs)
  File "/home/ye/tool/OpenNMT-py/onmt/models/model.py", line 69, in forward
    with_align=with_align)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 722, in _call_impl
    result = self.forward(*input, **kwargs)
  File "/home/ye/tool/OpenNMT-py/onmt/decoders/transformer.py", line 473, in forward
    with_align=with_align,
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 722, in _call_impl
    result = self.forward(*input, **kwargs)
  File "/home/ye/tool/OpenNMT-py/onmt/decoders/transformer.py", line 98, in forward
    output, attns = self._forward(*args, **kwargs)
  File "/home/ye/tool/OpenNMT-py/onmt/decoders/transformer.py", line 263, in _forward
    inputs_norm, dec_mask, layer_cache, step
  File "/home/ye/tool/OpenNMT-py/onmt/decoders/transformer.py", line 150, in _forward_self_attn
    attn_type="self",
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 722, in _call_impl
    result = self.forward(*input, **kwargs)
  File "/home/ye/tool/OpenNMT-py/onmt/modules/multi_headed_attn.py", line 205, in forward
    context_original = torch.matmul(drop_attn, value)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 2.56 GiB already allocated; 50.81 MiB free; 2.62 GiB reserved in total by PyTorch)

real	0m9.933s
user	0m10.725s
sys	0m0.589s
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$
```

## Training

Batch size ကို လျှော့ကြည့်ပြီး run တော့ အဆင်ပြေသွားခဲ့...  
Chage batch size as follows:  

```
#batch_size: 4096
batch_size: 64
```

Retrain again ...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4$ time onmt_train -config ./config-transformer-wat2021.yml 
[2021-03-21 02:45:29,005 INFO] Missing transforms field for corpus_1 data, set to default: [].
[2021-03-21 02:45:29,005 WARNING] Corpus corpus_1's weight should be given. We default it to 1 for you.
[2021-03-21 02:45:29,005 INFO] Missing transforms field for valid data, set to default: [].
[2021-03-21 02:45:29,005 INFO] Parsed 2 corpora from -data.
[2021-03-21 02:45:29,005 INFO] Get special vocabs from Transforms: {'src': set(), 'tgt': set()}.
[2021-03-21 02:45:29,005 INFO] Loading vocab from text file...
[2021-03-21 02:45:29,005 INFO] Loading src vocabulary from data/run/transformer.vocab.src
[2021-03-21 02:45:29,022 INFO] Loaded src vocab has 11588 tokens.
[2021-03-21 02:45:29,025 INFO] Loading tgt vocabulary from data/run/transformer.vocab.tgt
[2021-03-21 02:45:29,029 INFO] Loaded tgt vocab has 2538 tokens.
[2021-03-21 02:45:29,029 INFO] Building fields with vocab in counters...
[2021-03-21 02:45:29,031 INFO]  * tgt vocab size: 2542.
[2021-03-21 02:45:29,041 INFO]  * src vocab size: 11590.
[2021-03-21 02:45:29,041 INFO]  * src vocab size = 11590
[2021-03-21 02:45:29,041 INFO]  * tgt vocab size = 2542
[2021-03-21 02:45:29,043 INFO] Building model...
[2021-03-21 02:45:31,021 INFO] NMTModel(
  (encoder): TransformerEncoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(11590, 512, padding_idx=1)
        )
        (pe): PositionalEncoding(
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (transformer): ModuleList(
      (0): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (1): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (2): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (3): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (4): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
      (5): TransformerEncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
    )
    (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
  )
  (decoder): TransformerDecoder(
    (embeddings): Embeddings(
      (make_embedding): Sequential(
        (emb_luts): Elementwise(
          (0): Embedding(2542, 512, padding_idx=1)
        )
        (pe): PositionalEncoding(
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
    (transformer_layers): ModuleList(
      (0): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (1): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (2): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (3): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (4): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
      (5): TransformerDecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048, bias=True)
          (w_2): Linear(in_features=2048, out_features=512, bias=True)
          (layer_norm): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
          (dropout_1): Dropout(p=0.1, inplace=False)
          (dropout_2): Dropout(p=0.1, inplace=False)
        )
        (layer_norm_1): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
        (drop): Dropout(p=0.1, inplace=False)
        (context_attn): MultiHeadedAttention(
          (linear_keys): Linear(in_features=512, out_features=512, bias=True)
          (linear_values): Linear(in_features=512, out_features=512, bias=True)
          (linear_query): Linear(in_features=512, out_features=512, bias=True)
          (softmax): Softmax(dim=-1)
          (dropout): Dropout(p=0.1, inplace=False)
          (final_linear): Linear(in_features=512, out_features=512, bias=True)
        )
        (layer_norm_2): LayerNorm((512,), eps=1e-06, elementwise_affine=True)
      )
    )
  )
  (generator): Sequential(
    (0): Linear(in_features=512, out_features=2542, bias=True)
    (1): Cast()
    (2): LogSoftmax(dim=-1)
  )
)
[2021-03-21 02:45:31,022 INFO] encoder: 24849408
[2021-03-21 02:45:31,022 INFO] decoder: 27830766
[2021-03-21 02:45:31,022 INFO] * number of parameters: 52680174
[2021-03-21 02:45:31,024 INFO] Starting training on GPU: [0]
[2021-03-21 02:45:31,024 INFO] Start training loop and validate every 10000 steps...
[2021-03-21 02:45:31,024 INFO] corpus_1's transforms: TransformPipe()
[2021-03-21 02:45:31,024 INFO] Loading ParallelCorpus(data/train.en, data/train.my, align=None)...
[2021-03-21 02:46:26,207 INFO] Step 100/500000; acc:   3.92; ppl: 541.41; xent: 6.29; lr: 0.00001; 386/784 tok/s;     55 sec
[2021-03-21 02:47:21,730 INFO] Step 200/500000; acc:   6.98; ppl: 248.54; xent: 5.52; lr: 0.00002; 393/780 tok/s;    111 sec
[2021-03-21 02:48:16,789 INFO] Step 300/500000; acc:  12.59; ppl: 130.58; xent: 4.87; lr: 0.00004; 370/780 tok/s;    166 sec
[2021-03-21 02:49:11,782 INFO] Step 400/500000; acc:  18.14; ppl: 79.03; xent: 4.37; lr: 0.00005; 372/789 tok/s;    221 sec
[2021-03-21 02:50:07,942 INFO] Step 500/500000; acc:  25.05; ppl: 49.99; xent: 3.91; lr: 0.00006; 381/790 tok/s;    277 sec
[2021-03-21 02:51:04,942 INFO] Step 600/500000; acc:  31.47; ppl: 31.77; xent: 3.46; lr: 0.00007; 383/788 tok/s;    334 sec
[2021-03-21 02:52:04,021 INFO] Step 700/500000; acc:  30.62; ppl: 32.34; xent: 3.48; lr: 0.00009; 418/823 tok/s;    393 sec
[2021-03-21 02:53:04,561 INFO] Step 800/500000; acc:  32.75; ppl: 27.50; xent: 3.31; lr: 0.00010; 417/825 tok/s;    454 sec
[2021-03-21 02:54:08,207 INFO] Step 900/500000; acc:  30.34; ppl: 31.43; xent: 3.45; lr: 0.00011; 398/853 tok/s;    517 sec
[2021-03-21 02:55:11,845 INFO] Step 1000/500000; acc:  33.04; ppl: 25.46; xent: 3.24; lr: 0.00012; 404/862 tok/s;    581 sec
[2021-03-21 02:56:15,449 INFO] Step 1100/500000; acc:  32.92; ppl: 24.51; xent: 3.20; lr: 0.00014; 417/863 tok/s;    644 sec
[2021-03-21 02:57:17,359 INFO] Step 1200/500000; acc:  35.85; ppl: 18.94; xent: 2.94; lr: 0.00015; 420/853 tok/s;    706 sec
[2021-03-21 02:58:19,257 INFO] Step 1300/500000; acc:  36.20; ppl: 18.72; xent: 2.93; lr: 0.00016; 414/851 tok/s;    768 sec
[2021-03-21 02:59:17,734 INFO] Step 1400/500000; acc:  38.24; ppl: 16.63; xent: 2.81; lr: 0.00017; 359/810 tok/s;    827 sec
[2021-03-21 03:00:16,657 INFO] Step 1500/500000; acc:  41.80; ppl: 13.58; xent: 2.61; lr: 0.00019; 367/815 tok/s;    886 sec
[2021-03-21 03:01:15,161 INFO] Step 1600/500000; acc:  38.01; ppl: 17.50; xent: 2.86; lr: 0.00020; 337/809 tok/s;    944 sec
[2021-03-21 03:02:14,468 INFO] Step 1700/500000; acc:  40.31; ppl: 14.71; xent: 2.69; lr: 0.00021; 341/823 tok/s;   1003 sec
[2021-03-21 03:03:12,443 INFO] Step 1800/500000; acc:  39.32; ppl: 16.07; xent: 2.78; lr: 0.00022; 353/811 tok/s;   1061 sec

...
...
...

[2021-03-21 14:46:03,315 INFO] Step 79900/500000; acc:  67.29; ppl:  3.36; xent: 1.21; lr: 0.00031; 373/740 tok/s;  43232 sec
[2021-03-21 14:46:56,590 INFO] Step 80000/500000; acc:  57.67; ppl:  5.23; xent: 1.65; lr: 0.00031; 436/759 tok/s;  43286 sec
[2021-03-21 14:46:56,591 INFO] Loading ParallelCorpus(data/valid.en, data/valid.my, align=None)...
[2021-03-21 14:46:56,615 WARNING] The batch will be filled until we reach 1,its size may exceed 32 tokens
[2021-03-21 14:47:08,734 INFO] Validation perplexity: 25.2912
[2021-03-21 14:47:08,734 INFO] Validation accuracy: 38.575
[2021-03-21 14:47:08,839 INFO] Saving checkpoint exp/transformer1.en-my_step_80000.pt
[2021-03-21 14:47:58,186 INFO] Step 80100/500000; acc:  65.63; ppl:  3.69; xent: 1.31; lr: 0.00031; 403/685 tok/s;  43347 sec
[2021-03-21 14:48:48,349 INFO] Step 80200/500000; acc:  56.39; ppl:  5.27; xent: 1.66; lr: 0.00031; 555/822 tok/s;  43397 sec
[2021-03-21 14:49:38,869 INFO] Step 80300/500000; acc:  55.39; ppl:  5.62; xent: 1.73; lr: 0.00031; 504/790 tok/s;  43448 sec
[2021-03-21 14:50:28,513 INFO] Step 80400/500000; acc:  56.28; ppl:  5.25; xent: 1.66; lr: 0.00031; 521/829 tok/s;  43497 sec
[2021-03-21 14:51:20,722 INFO] Step 80500/500000; acc:  55.94; ppl:  5.51; xent: 1.71; lr: 0.00031; 470/758 tok/s;  43550 sec
[2021-03-21 14:52:10,390 INFO] Step 80600/500000; acc:  61.03; ppl:  4.32; xent: 1.46; lr: 0.00031; 565/821 tok/s;  43599 sec
[2021-03-21 14:52:59,565 INFO] Step 80700/500000; acc:  67.41; ppl:  3.45; xent: 1.24; lr: 0.00031; 517/870 tok/s;  43649 sec
[2021-03-21 14:53:47,486 INFO] Step 80800/500000; acc:  62.94; ppl:  4.24; xent: 1.44; lr: 0.00031; 560/881 tok/s;  43696 sec
[2021-03-21 14:54:34,821 INFO] Step 80900/500000; acc:  60.13; ppl:  4.73; xent: 1.55; lr: 0.00031; 520/920 tok/s;  43744 sec
[2021-03-21 14:55:23,468 INFO] Step 81000/500000; acc:  60.32; ppl:  4.55; xent: 1.52; lr: 0.00031; 497/877 tok/s;  43792 sec
[2021-03-21 14:56:15,543 INFO] Step 81100/500000; acc:  56.05; ppl:  5.36; xent: 1.68; lr: 0.00031; 428/779 tok/s;  43845 sec
[2021-03-21 14:57:07,021 INFO] Step 81200/500000; acc:  57.93; ppl:  4.89; xent: 1.59; lr: 0.00031; 444/797 tok/s;  43896 sec
[2021-03-21 14:57:57,048 INFO] Step 81300/500000; acc:  67.34; ppl:  3.28; xent: 1.19; lr: 0.00031; 496/841 tok/s;  43946 sec
[2021-03-21 14:58:46,730 INFO] Step 81400/500000; acc:  67.56; ppl:  3.28; xent: 1.19; lr: 0.00031; 490/833 tok/s;  43996 sec
[2021-03-21 14:59:35,307 INFO] Step 81500/500000; acc:  67.02; ppl:  3.40; xent: 1.22; lr: 0.00031; 550/866 tok/s;  44044 sec
[2021-03-21 15:00:24,930 INFO] Step 81600/500000; acc:  64.92; ppl:  3.71; xent: 1.31; lr: 0.00031; 584/831 tok/s;  44094 sec
[2021-03-21 15:01:16,559 INFO] Step 81700/500000; acc:  67.42; ppl:  3.40; xent: 1.22; lr: 0.00031; 544/819 tok/s;  44146 sec
[2021-03-21 15:02:08,398 INFO] Step 81800/500000; acc:  64.68; ppl:  3.76; xent: 1.33; lr: 0.00031; 553/791 tok/s;  44197 sec
[2021-03-21 15:02:59,469 INFO] Step 81900/500000; acc:  68.08; ppl:  3.19; xent: 1.16; lr: 0.00031; 567/819 tok/s;  44248 sec
[2021-03-21 15:03:54,084 INFO] Step 82000/500000; acc:  67.77; ppl:  3.20; xent: 1.16; lr: 0.00031; 510/760 tok/s;  44303 sec
[2021-03-21 15:04:52,709 INFO] Step 82100/500000; acc:  57.66; ppl:  5.29; xent: 1.67; lr: 0.00031; 442/730 tok/s;  44362 sec
[2021-03-21 15:05:50,140 INFO] Step 82200/500000; acc:  48.71; ppl:  7.93; xent: 2.07; lr: 0.00031; 397/728 tok/s;  44419 sec
[2021-03-21 15:06:47,210 INFO] Step 82300/500000; acc:  49.37; ppl:  7.65; xent: 2.04; lr: 0.00031; 412/725 tok/s;  44476 sec
[2021-03-21 15:07:48,459 INFO] Step 82400/500000; acc:  51.50; ppl:  6.99; xent: 1.95; lr: 0.00031; 386/746 tok/s;  44537 sec
[2021-03-21 15:08:47,443 INFO] Step 82500/500000; acc:  58.50; ppl:  5.10; xent: 1.63; lr: 0.00031; 411/787 tok/s;  44596 sec
[2021-03-21 15:09:42,958 INFO] Step 82600/500000; acc:  73.81; ppl:  2.63; xent: 0.97; lr: 0.00031; 477/847 tok/s;  44652 sec
[2021-03-21 15:10:39,379 INFO] Step 82700/500000; acc:  66.69; ppl:  3.50; xent: 1.25; lr: 0.00031; 427/832 tok/s;  44708 sec
[2021-03-21 15:11:30,528 INFO] Step 82800/500000; acc:  60.97; ppl:  4.40; xent: 1.48; lr: 0.00031; 450/804 tok/s;  44760 sec
[2021-03-21 15:12:21,483 INFO] Step 82900/500000; acc:  54.42; ppl:  5.98; xent: 1.79; lr: 0.00031; 478/803 tok/s;  44810 sec
[2021-03-21 15:13:11,135 INFO] Step 83000/500000; acc:  53.13; ppl:  6.70; xent: 1.90; lr: 0.00031; 490/855 tok/s;  44860 sec
[2021-03-21 15:13:59,445 INFO] Step 83100/500000; acc:  55.02; ppl:  6.35; xent: 1.85; lr: 0.00031; 495/907 tok/s;  44908 sec
[2021-03-21 15:14:47,282 INFO] Step 83200/500000; acc:  59.24; ppl:  5.13; xent: 1.64; lr: 0.00031; 511/917 tok/s;  44956 sec
[2021-03-21 15:15:35,554 INFO] Step 83300/500000; acc:  68.46; ppl:  3.21; xent: 1.17; lr: 0.00031; 579/885 tok/s;  45005 sec

```

လိုင်း တစ်လိုင်းစီရဲ့ ရှေ့ဆုံးမှာ အချိန်ကိုလည်း ဖော်ပြပေးထားတာကြောင့် Step တစ်ခုချင်းစီအတွက် ကြာချိန်ကိုလည်း ခန့်မှန်းလို့ ရပါလိမ့်မယ်။ GPU က တစ်လုံးပဲသုံးထားတဲ့ ကြာချိန်မို့လို့ GPU ကို တလုံးထက်မက ပိုသုံးမယ်ဆိုရင် လက်ရှိကြာချိန်ထက်တော့ မြန်လာပါလိမ့်မယ်။  

## Checking the Model

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/exp$ ls
transformer1.en-my_step_10000.pt  transformer1.en-my_step_40000.pt  transformer1.en-my_step_70000.pt
transformer1.en-my_step_20000.pt  transformer1.en-my_step_50000.pt  
transformer1.en-my_step_30000.pt  transformer1.en-my_step_60000.pt  
```

## Testing/Translation with GPU

GPU နှစ်လုံးစလုံးက သုံးထားတုန်း (GPU 0 က လက်ရှိ OpenNMT experiment နဲ့ GPU no. 1 က တခြား fairseq နဲ့ run ထားတဲ့ experiment) ကို လက်ရှိ ဆောက်ထားတဲ့ မော်ဒယ် 70K model နဲ့ translate လုပ်ဖို့ ကြိုးစားကြည့်တော့ memory က မနိုင်လို့ အောက်ပါအတိုင်း error ပေးတာကို တွေ့ရပါတယ်။

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/exp$ time onmt_translate -model ./transformer1.en-my_step_70000.pt -src ../data/test.en -output ../exp/hyp-70kmodel.txt -gpu 0 -verbose | tee ../exp/translate-70kmodel.log
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/py3.6env/bin/onmt_translate", line 33, in <module>
    sys.exit(load_entry_point('OpenNMT-py', 'console_scripts', 'onmt_translate')())
  File "/home/ye/tool/OpenNMT-py/onmt/bin/translate.py", line 44, in main
    translate(opt)
  File "/home/ye/tool/OpenNMT-py/onmt/bin/translate.py", line 15, in translate
    translator = build_translator(opt, logger=logger, report_score=True)
  File "/home/ye/tool/OpenNMT-py/onmt/translate/translator.py", line 32, in build_translator
    fields, model, model_opt = load_test_model(opt)
  File "/home/ye/tool/OpenNMT-py/onmt/model_builder.py", line 93, in load_test_model
    opt.gpu)
  File "/home/ye/tool/OpenNMT-py/onmt/model_builder.py", line 259, in build_base_model
    model.to(device)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 607, in to
    return self._apply(convert)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  [Previous line repeated 2 more times]
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 376, in _apply
    param_applied = fn(param)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 605, in convert
    return t.to(device, dtype if t.is_floating_point() else None, non_blocking)
RuntimeError: CUDA error: out of memory

real	0m4.360s
user	0m13.326s
sys	0m0.638s
```

GPU နံပါတ် 1 ကိုလည်း တခြား အလုပ်လုပ်ခိုင်းထားပေမဲ့ translate လုပ်တာလေးပဲဆိုတော့ လုပ်ပေးနိုင်မလားဆိုတာကို confirm လုပ်ကြည့်တာ... မရပါဘူး။    

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/exp$ time onmt_translate -model ./transformer1.en-my_step_70000.pt -src ../data/test.en -output ../exp/hyp-70kmodel.txt -gpu 1 -verbose | tee ../exp/translate-70kmodel.log
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/py3.6env/bin/onmt_translate", line 33, in <module>
    sys.exit(load_entry_point('OpenNMT-py', 'console_scripts', 'onmt_translate')())
  File "/home/ye/tool/OpenNMT-py/onmt/bin/translate.py", line 44, in main
    translate(opt)
  File "/home/ye/tool/OpenNMT-py/onmt/bin/translate.py", line 15, in translate
    translator = build_translator(opt, logger=logger, report_score=True)
  File "/home/ye/tool/OpenNMT-py/onmt/translate/translator.py", line 32, in build_translator
    fields, model, model_opt = load_test_model(opt)
  File "/home/ye/tool/OpenNMT-py/onmt/model_builder.py", line 93, in load_test_model
    opt.gpu)
  File "/home/ye/tool/OpenNMT-py/onmt/model_builder.py", line 259, in build_base_model
    model.to(device)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 607, in to
    return self._apply(convert)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 354, in _apply
    module._apply(fn)
  [Previous line repeated 2 more times]
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 376, in _apply
    param_applied = fn(param)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/nn/modules/module.py", line 605, in convert
    return t.to(device, dtype if t.is_floating_point() else None, non_blocking)
RuntimeError: CUDA error: out of memory

real	0m3.473s
user	0m12.334s
sys	0m0.381s
```

## Testing/Translation with CPU

လက်ရှိမှာ GPU နှစ်လုံးစလုံး မအားလို့ GPU ကို assign မလုပ်ပဲ လက်ရှိ ပြီးနေတဲ့ မော်ဒယ်နဲ့ပဲ ဘာသာပြန်ခိုင်းကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ။
Translation time ကတော့ အချိန်ကြာတယ်။ သို့သော် translated output တွေကတော့ ဗမာစာကြောင်းဆန်နေတာ၊ တော်တော်လေးကောင်းတာကို တွေ့ရပါလိမ့်မယ်... :)

```
py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/wat2021/exp-syl4/exp$ time onmt_translate -model ./transformer1.en-my_step_70000.pt -src ../data/test.en -output ../exp/hyp-70kmodel.txt -verbose | tee ../exp/translate-70kmodel.log
[2021-03-21 13:57:32,459 INFO] Translating shard 0.
[2021-03-21 14:04:31,913 INFO] 
SENT 1: ['It', 'has', 'been', 'confirmed', 'that', 'eight', 'thoroughbred', 'race', 'horses', 'at', 'Randwick', 'Racecourse', 'in', 'Sydney', 'have', 'been', 'infected', 'with', 'equine', 'influenza', '.']
PRED 1: အ ဆို ပါ ပြိုင် ပွဲ တွင် ပါ ဝင် ယှဉ် ပြိုင် သူ ရှစ် ဦး နှ င့် အ တူ ယှဉ် တွဲ နေ ထိုင် သူ ရှစ် ဦး အား အ တည် ပြု ခဲ့ သည် ဟု အ တည် ပြု ခဲ့ သည် ။
PRED SCORE: -38.5376

[2021-03-21 14:04:31,913 INFO] 
SENT 2: ['Randwick', 'has', 'been', 'locked', 'down', ',', 'and', 'is', 'expected', 'to', 'remain', 'so', 'for', 'up', 'to', 'two', 'months', '.']
PRED 2: အ သက် ၁၈ နှစ် ပြ ည့် ပြီး မှ ဖြစ် မယ် လို့ မျှော် လ င့် ပါ တယ် ။
PRED SCORE: -17.2223

[2021-03-21 14:04:31,913 INFO] 
SENT 3: ['It', 'is', 'expected', 'that', 'the', 'virulent', 'flu', 'will', 'affect', 'the', 'majority', 'of', 'the', '700', 'horses', 'stabled', 'at', 'Randwick', '.']
PRED 3: အ များ အား ဖြ င့် ငွေ ကျပ် သိန်း ( ၅၀၀ ) ကို ထိ ခိုက် စေ မည် ဟု မျှော် လ င့် ပါ သည် ။
PRED SCORE: -22.3083

[2021-03-21 14:04:31,913 INFO] 
SENT 4: ['NSW', 'Minister', 'for', 'Primary', 'Industries', 'said', 'the', 'facility', 'would', 'be', 'quarantined', 'until', '30', 'days', 'after', 'the', 'last', 'sign', 'of', 'the', 'flu', '.']
PRED 4: ဝန် ကြီး ဌာ န သည် ရက် ပေါင်း ၃၀ အ တွင်း ဝန် ကြီး ဌာ န ကို အ သုံး ပြု ပြီး နောက် ဝန် ကြီး က ပြော သည် ။
PRED SCORE: -21.0435

[2021-03-21 14:04:31,913 INFO] 
SENT 5: ['The', 'cases', 'are', 'the', 'first', 'infections', 'of', 'race', 'horses', ',', 'despite', 'infecting', 'dozens', 'of', 'recreational', 'horses', 'across', 'NSW', 'and', 'Queensland', '.']
PRED 5: ပ ထ မ ဦး ဆုံး အ နေ ဖြ င့် အ ဝတ် အ စား များ နှ င့် အ ဝတ် အ ထည် များ ကို အ ဝတ် အ ထည် နှ င့် အ ဝတ် အ ထည် များ ကို ဝတ် ဆင် ထား သည် ။
PRED SCORE: -31.9870

[2021-03-21 14:04:31,914 INFO] 
SENT 6: ['The', 'flu', 'is', 'highly', 'contagious', 'but', 'cannot', 'be', 'transmitted', 'to', 'humans', '.']
PRED 6: အ မေ ရိ ကန် နိုင် ငံ က လူ သား များ အ တွက် ကူး စက် မှု မ ပြု နိုင် ပါ ။
PRED SCORE: -20.2262

[2021-03-21 14:04:31,914 INFO] 
SENT 7: ['The', 'national', 'racing', 'shutdown', 'was', 'costing', 'the', 'industry', 'tens', 'of', 'millions', 'of', 'dollars', 'every', 'day', '.']
PRED 7: အ မျိုး သား အ ဆ င့် စီး ပွား ရေး လုပ် ငန်း ရှင် များ အ နေ ဖြ င့် အ မေ ရိ ကန် ဒေါ် လာ ၁ ဒ သ မ ၅ သန်း ခ န့် ရှိ ပါ သည် ။
PRED SCORE: -23.1208

[2021-03-21 14:04:31,914 INFO] 
SENT 8: ['Chief', 'Executive', 'of', 'Racing', 'NSW', ',', 'Peter', 'V', '&amp;', 'apos', ';', 'Landys', 'said', 'while', 'racing', 'had', 'been', 'disrupted', 'since', 'a', 'ban', 'on', 'horse', 'movements', 'last', 'weekend', 'today', 'was', 'a', '&amp;', 'quot', ';', 'grim', ',', 'black', 'day', '&amp;', 'quot', ';', 'for', 'the', 'racing', 'industry', 'in', 'NSW', '.']
PRED 8: မြန် မာ နိုင် ငံ တွင် လွန် ခဲ့ သော ရက် သတ္တ ပတ် အ နည်း ငယ် က တည်း က ပင် လယ် ဓား ပြ တိုက် မှု ဖြစ် ပွား ခဲ့ သ ည့် စ နေ ၊ တ နင်္ဂ နွေ နေ့ က တည်း က ပင် ပီ တာ က ပြော သည် ။
PRED SCORE: -49.1662

[2021-03-21 14:04:31,914 INFO] 
SENT 9: ['Racing', 'is', 'expected', 'to', 'resume', 'in', 'all', 'Australian', 'states', 'except', 'NSW', 'and', 'Queensland', 'on', 'the', 'weekend', '.']
PRED 9: တိုင်း ဒေ သ ကြီး နှ င့် ပြည် နယ် များ အား လုံး တွင် စ နေ ၊ တ နင်္ဂ နွေ နေ့ နှ င့် တ နင်္ဂ နွေ နေ့ များ တွင် မည် သ ည့် အ ချိန် တွင် မ ဆို အာ မ ခံ ထား ရှိ ရ မည် ။
PRED SCORE: -32.8415

[2021-03-21 14:04:31,914 INFO] 
SENT 10: ['While', 'Sydney', '&amp;', 'apos', ';', 's', 'spring', 'racing', 'carnival', 'has', 'been', 'canceled', ',', 'Melbourne', '&amp;', 'apos', ';', 's', 'is', 'expected', 'to', 'kick', 'off', 'this', 'weekend', 'with', 'the', 'Caufield', 'Cup', '.']
PRED 10: နွေ ဦး ရာ သီ အား လပ် ရက် ခ ရီး စဉ် ပြီး ဆုံး သ ည့် အ ခါ အ မေ ရိ ကန် ပြည် ထောင် စု ၏ အ သံ ထွက် ပေါ် လာ ခြင်း ဖြစ် သည် ။
PRED SCORE: -35.7012

[2021-03-21 14:04:31,914 INFO] 
SENT 11: ['The', 'cup', 'will', 'be', 'ran', 'with', 'special', 'precautions', 'in', 'place', 'to', 'attempt', 'to', 'keep', 'the', 'state', 'free', 'of', 'the', 'virus', '.']
PRED 11: နိုင် ငံ တော် သည် နိုင် ငံ တော် ၏ အ ကျိုး စီး ပွား အ တွက် ကြို တင် ပြင် ဆင် မှု များ ပြု လုပ် ရန် ကြိုး ပမ်း ဆောင် ရွက် မည် ။
PRED SCORE: -21.8588

[2021-03-21 14:04:31,914 INFO] 
SENT 12: ['Contact', 'between', 'the', 'general', 'public', 'and', 'those', 'working', 'with', 'the', 'horses', 'will', 'be', 'banned', 'and', 'Sydney-based', 'jockeys', 'Darren', 'Beadman', 'and', 'Hugh', 'Bowman', 'and', 'a', 'number', 'of', 'interstate', 'trainers', 'including', 'Bart', 'Cummings', 'are', 'not', 'allowed', 'to', 'take', 'part', '.']
PRED 12: အ များ ပြည် သူ ဝန် ထမ်း များ နှ င့် အ တူ အ လုပ် လုပ် ကိုင် နေ သူ များ အ ကြား အ လုပ် လုပ် ကိုင် နေ သူ များ နှ င့် အ တူ အ လုပ် လုပ် ကိုင် ခွ င့် ပြု ထား သ ည့် သင် တန်း သား များ နှ င့် အ တူ အ လုပ် လုပ် ကိုင် ခွ င့် မ ပြု သ ည့် သင် တန်း သား များ အ ပါ အ ဝင် သင် တန်း သား များ နှ င့် အ တူ သင် တန်း တက် ခွ င့် မ ပြု ရ ။
PRED SCORE: -74.8321

[2021-03-21 14:04:31,914 INFO] 
SENT 13: ['Federal', 'Minister', 'for', 'Agriculture', ',', 'Peter', 'McGauran', 'said', 'the', 'spring', 'carnival', 'in', 'Melbourne', 'will', 'remain', '&amp;', 'quot', ';', 'largely', 'intact', '&amp;', 'quot', ';', 'despite', 'losing', 'some', 'of', 'the', 'biggest', 'names', 'in', 'Australian', 'racing', '.']
PRED 13: ဝန် ကြီး ဌာ န အ နေ ဖြ င့် မီ တာ ရှည် လျား သော ပင် လယ် ရေ မျက် နှာ ပြင် အ မြ င့် ဆုံး ရေ ချိုး ခန်း အ မည် တွင် ပါ ရှိ သ ည့် အ မည် များ အ နက် မှ ယ ခု ကဲ့ သို့ ပင် စင် ကာ ပူ သမ္မ တ နိုင် ငံ ဝန် ကြီး ချုပ် က ပြော ကြား သည် ။
PRED SCORE: -71.3782

[2021-03-21 14:04:31,914 INFO] 
SENT 14: ['At', 'least', '11', 'people', 'were', 'killed', 'Dec.', '26', 'and', '27', 'in', 'neighborhood', 'gang', 'turf', 'fights', 'between', 'drug', 'dealers', 'at', 'shantytown', '&amp;', 'quot', ';', 'morro', 'da', 'Mineira', '&amp;', 'quot', ';', '(', 'Miner', 'Hill', ')', 'in', 'the', 'Catumbi', 'neighborhood', 'of', 'Rio', 'de', 'Janeiro', ',', 'Brazil', '.']
PRED 14: အ နည်း ဆုံး ၁၁ - ၁၁ - ၁၁ - ၅ - ၅ - ၂၀၁၆ ရက် နေ့ တွင် တောင် ကြီး မြို့ နယ် တွင် မူး ယစ် ဆေး ဝါး တိုက် ဖျက် ရေး လုပ် ငန်း များ ဆောင် ရွက် နေ သ ည့် လူ ဦး ရေ ၆ ဦး သေ ဆုံး ခဲ့ သည် ။
PRED SCORE: -44.4893

[2021-03-21 14:04:31,914 INFO] 
SENT 15: ['The', 'region', 'is', 'controlled', 'by', 'rival', 'gang', 'Comando', 'Vermelho', '(', 'Red', 'Command', ')', ',', 'which', 'does', 'not', 'approve', 'of', 'other', 'gangs', 'selling', 'drugs', 'in', 'the', 'region', '.']
PRED 15: တိုင်း ဒေ သ ကြီး သည် မူး ယစ် ဆေး ဝါး ရောင်း ဝယ် ရေး လုပ် ငန်း များ ကို အ တည် ပြု ခြင်း မ ပြု ရ သေး သော ဒေ သ များ ကို အ တည် ပြု ခြင်း မ ပြု ရ ။
PRED SCORE: -33.4137

[2021-03-21 14:04:31,914 INFO] 
SENT 16: ['Comando', 'Vermelho', 'members', 'started', 'attacking', 'the', 'rival', 'members', 'of', 'ADA', 'to', 'protect', 'their', 'turf', '.']
PRED 16: အ ဖွဲ့ ဝင် များ သည် သူ တို့ ၏ ဦး စီး အ ဖွဲ့ ဝင် များ အား သူ တို့ ၏ ဦး ဆောင် မှု ဖြ င့် ကာ ကွယ် စော င့် ရှောက် ခဲ့ သည် ။
PRED SCORE: -28.2103

[2021-03-21 14:04:31,914 INFO] 
SENT 17: ['On', 'Friday', 'evening', ',', 'an', 'explosion', 'in', 'Chengdu', ',', 'China', 'caused', 'partial', 'shutdown', 'of', 'a', 'facility', 'operated', 'by', 'Foxconn', ',', 'one', 'of', 'the', 'world', '&amp;', 'apos', ';', 's', 'biggest', 'electronics', 'manufacturers', 'and', 'a', 'major', 'supplier', 'to', 'companies', 'like', 'Hewlett-Packard', ',', 'Dell', ',', 'Sony', ',', 'Apple', ',', 'Motorola', 'and', 'Nokia', '.']
PRED 17: သော ကြာ နေ့ ည နေ ပိုင်း တွင် တ ရုတ် ပြည် သူ့ သမ္မ တ နိုင် ငံ သည် ကမ္ဘာ လုံး ဆိုင် ရာ မ တော် တ ဆ ထိ ခိုက် မှု ဖြစ် ပွား မှု ကြော င့် ကမ္ဘာ လုံး ဆိုင် ရာ အ ကြီး ဆုံး ကုမ္ပ ဏီ တစ် ခု ဖြစ် သ ည့် အ တွက် အ ကြီး ဆုံး အ ဆ င့် မြ င့် ပ ရိ ဘော ဂ အ ရေ အ တွက် တစ် ခု နှ င့် တစ် ခု တို့ ဖြစ် သည် ။
PRED SCORE: -66.8427

[2021-03-21 14:04:31,914 INFO] 
SENT 18: ['Initial', 'investigations', 'now', 'suggest', 'the', 'explosion', 'was', 'caused', 'by', 'poor', 'ventilation', ',', 'which', 'lead', 'to', 'high', 'concentrations', 'of', 'combustible', 'dust', '.']
PRED 18: မ တော် တ ဆ ဖြစ် ပွား မှု ဖြစ် ပွား မှု ဖြစ် ပွား မှု ကြော င့် ဖြစ် ပွား ရ သ ည့် အ ကြောင်း အ ရာ များ မှာ မ တော် တ ဆ ဖြစ် ပွား မှု အ ဆ င့် မြ င့် မား လာ ခြင်း ဖြစ် သည် ။
PRED SCORE: -43.2014

[2021-03-21 14:04:31,914 INFO] 
SENT 19: ['The', 'blast', 'happened', 'at', '7', ':', '18PM', ',', 'around', 'the', 'time', 'workers', 'change', 'shifts', '.']
PRED 19: အ လုပ် သ မား ခု နစ် ဦး ခ န့် တွင် အ လုပ် သ မား ခု နစ် ဦး ခ န့် ဖြ င့် အ လုပ် သ မား ခု နစ် ဦး ခ န့် ရှိ ခဲ့ သည် ။
PRED SCORE: -21.6234

[2021-03-21 14:04:31,914 INFO] 
SENT 20: ['At', 'least', 'three', 'people', 'were', 'killed', ',', 'at', 'least', 'fifteen', 'injured', '.']
PRED 20: အ နည်း ဆုံး သုံး ဦး ဒဏ် ရာ ရ ရှိ ခဲ့ သည် ။
PRED SCORE: -6.2094

[2021-03-21 14:04:31,914 INFO] 
SENT 21: ['Foxconn', 'halted', 'production', 'to', 'investigate', ',', 'saying', '&amp;', 'quot', ';', 'All', 'operations', 'at', 'the', 'affected', 'workshop', 'remain', 'suspended', 'and', 'production', 'at', 'all', 'other', 'workshops', 'that', 'carry', 'out', 'similar', 'processing', 'functions', 'have', 'also', 'been', 'halted', 'pending', 'the', 'results', 'of', 'the', 'investigation', '.', '&amp;', 'quot', ';']
PRED 21: အ လုပ် ရုံ ဆွေး နွေး ပွဲ များ ပြု လုပ် ခြင်း နှ င့် အ ခြား အ လုပ် ရုံ ဆွေး နွေး ပွဲ များ ပြု လုပ် ခြင်း တို့ ကြော င့် အ လုပ် ရုံ ဆွေး နွေး ပွဲ များ ကျင်း ပ ခြင်း မ ပြု သေး မီ ကာ လ အ ပိုင်း အ ခြား ကာ လ အ ပိုင်း အ ခြား ကာ လ အ ပိုင်း အ ခြား အ လိုက် အ လုပ် ရုံ ဆွေး နွေး ပွဲ များ ပြု လုပ် ခဲ့ သည် ။
PRED SCORE: -60.8002

[2021-03-21 14:04:31,914 INFO] 
SENT 22: ['&amp;', 'quot', ';', 'All', 'other', 'production', 'operations', 'in', 'our', 'facilities', 'in', 'China', 'continue', 'operating', 'normally', '.', '&amp;', 'quot', ';']
PRED 22: ကျွန် တော် တို့ တ ရုတ် နိုင် ငံ က ထုတ် လုပ် သ ည့် လုပ် ငန်း များ အား လုံး ကို ဆက် လက် ဆောင် ရွက် နေ ပါ သည် ။
PRED SCORE: -22.5282

[2021-03-21 14:04:31,915 INFO] 
SENT 23: ['On', 'Monday', ',', 'city', 'officials', 'gave', 'the', 'cause', 'as', 'combustible', 'dust', 'in', 'the', 'air', 'at', 'a', 'polishing', 'workshop', '.']
PRED 23: တ နင်္လာ နေ့ တွင် မြို့ နယ် တာ ဝန် ရှိ သူ များ က လေ ကောင်း လေ သ န့် စင် ခန်း တွင် အ လုပ် ရုံ ဆွေး နွေး ပွဲ တစ် ခု ပြု လုပ် ခဲ့ သည် ။
PRED SCORE: -21.5170

[2021-03-21 14:04:31,915 INFO] 
SENT 24: ['Hong', 'Kong-based', 'labor', 'rights', 'group', 'Students', '&amp;', 'amp', ';', 'Scholars', 'Against', 'Corporate', 'Misbehavior', 'said', 'they', 'reported', 'aluminium', 'dust', 'problems', 'in', 'March', 'when', 'they', 'reviewed', 'working', 'conditions', 'at', 'Foxconn', '.']
PRED 24: ကျောင်း သား များ အ လုပ် သ မား များ ၏ အ ခွ င့် အ ရေး များ ဆိုင် ရာ ပြ ဿ နာ များ ကို ပြန် လည် သုံး သပ် သ ည့် အ ခါ အ လုပ် သ မား အင် အား စု များ က ပြန် လည် သုံး သပ် သ ည့် အ ခြေ အ နေ များ ကို ရှင်း လင်း ပြော ကြား ကြ သည် ။
PRED SCORE: -49.4947

[2021-03-21 14:04:31,915 INFO] 
SENT 25: ['After', 'the', 'explosion', ',', 'they', 'commented', 'that', 'workers', 'were', 'complaining', '&amp;', 'quot', ';', 'the', 'ventilation', 'of', 'the', 'department', 'is', 'poor', '.', '&amp;', 'quot', ';']
PRED 25: ဓာ တု ပစ္စည်း နှ င့် ဆက် စပ် ပစ္စည်း များ အ လုပ် သ မား များ အ လုပ် သ မား များ အ လုပ် သ မား များ က အန္တ ရာယ် ရှိ သ ည့် အ လုပ် သ မား များ ဖြစ် ကြောင်း ဖော် ပြ ခဲ့ သည် ။
PRED SCORE: -30.8029

[2021-03-21 14:04:31,915 INFO] 
SENT 26: ['&amp;', 'quot', ';', 'In', 'the', 'process', ',', 'there', 'is', 'lots', 'of', 'aluminum', '(', 'aluminium', ')', 'dust', 'floating', 'in', 'the', 'air', '.', '&amp;', 'quot', ';']
PRED 26: လုပ် ငန်း စဉ် တွင် လေ ကောင်း လေ သ န့် စင် ခန်း များ အ များ ကြီး ပါ ဝင် သည် ။
PRED SCORE: -14.8807

[2021-03-21 14:04:31,915 INFO] 
SENT 27: ['&amp;', 'quot', ';', 'Workers', 'always', 'breathe', 'in', 'aluminum', 'dust', 'even', 'though', 'they', 'put', 'on', 'masks', '.', '&amp;', 'quot', ';']
PRED 27: <unk> ကို အ မြဲ တမ်း အ သုံး ပြု နေ သော် လည်း သူ တို့ က အ ဝတ် အ ထည် ကို ဝတ် ဆင် ထား သည် ။
PRED SCORE: -26.6554

[2021-03-21 14:04:31,915 INFO] 
SENT 28: ['&amp;', 'quot', ';', 'When', 'workers', 'take', 'off', 'their', 'cotton', 'gloves', ',', 'their', 'hands', 'are', 'covered', 'with', 'aluminum', 'dust', '.', '&amp;', 'quot', ';']
PRED 28: အ လုပ် သ မား တွေ က သူ တို့ ရဲ့ လက် တွေ ကို ကိုင် ဆောင် ထား တဲ့ အ ခါ အ လုပ် သ မား တွေ က သူ တို့ ရဲ့ လက် ဆွဲ အိတ် တွေ ကို အ ပေါ် ဖုံး နဲ့ ချည် ထား တယ် ။
PRED SCORE: -36.9568

[2021-03-21 14:04:31,915 INFO] 
SENT 29: ['Foxconn', 'responded', 'by', 'saying', 'the', 'group', 'was', 'trying', 'to', '&amp;', 'quot', ';', 'capitalize', 'on', 'the', 'tragic', 'accident', '&amp;', 'quot', ';', 'and', 'misrepresented', '&amp;', 'quot', ';', 'Foxconn', '&amp;', 'apos', ';', 's', 'commitment', 'to', 'the', 'health', 'and', 'safety', 'of', 'our', 'employees', '.', '&amp;', 'quot', ';']
PRED 29: မ တော် တ ဆ ဖြစ် ပွား မှု နှ င့် ကျန်း မာ ရေး ဝန် ထမ်း များ ၏ လုံ ခြုံ ရေး အ ခြေ အ နေ များ ကို ပြော ကြား ရာ တွင် မ တော် တ ဆ ဖြစ် ပွား မှု နှ င့် ကျန်း မာ ရေး ဝန် ထမ်း များ ၏ အ သက် အန္တ ရာယ် ကင်း ရှင်း ရေး တို့ ကို အ လေး အ နက် ထား ဖော် ပြ ထား သည် ။
PRED SCORE: -54.4647

[2021-03-21 14:04:31,915 INFO] 
SENT 30: ['Research', 'group', 'IHS', 'iSuppli', 'said', 'the', 'explosion', 'may', 'cause', 'loss', 'of', 'production', 'of', '500,000', 'iPads', 'during', 'this', 'quarter', 'of', 'the', 'year', '.']
PRED 30: ဓာ တု ပစ္စည်း နှ င့် ဆက် စပ် ပစ္စည်း များ ၏ အ ဓိ က အ ကြောင်း အ ရာ များ ကို နှစ် စဉ် ထုတ် လွှ င့် ခြင်း ဖြ င့် ထုတ် လုပ် နိုင် သည် ။
PRED SCORE: -27.1393
...
...
...
[2021-03-21 17:05:16,866 INFO] 
SENT 236: ['&amp;', 'quot', ';', 'What', 'we', 'see', 'instead', 'is', ',', 'where', 'there', 'were', 'errors', 'made', 'they', 'were', 'based', 'on', 'poor', 'decision-making', 'process', 'or', 'using', 'wrong', 'information', ',', '&amp;', 'quot', ';', 'he', 'said', '.']
PRED 236: ကျွန် တော် တို့ တွေ့ ခဲ့ တဲ့ အ စား အ သောက် တွေ က ဆင်း ရဲ နွမ်း ပါး မှု လျှော့ ချ ရေး လုပ် ငန်း စဉ် တွေ မှာ အ ခြေ ခံ ကျ တဲ့ အ ချက် အ လက် တွေ အ ပေါ် မှာ အ ခြေ ခံ ပြီး ပြော တာ ပါ ။
PRED SCORE: -40.0995

[2021-03-21 17:05:16,866 INFO] 
SENT 237: ['The', 'Guardian', 'reported', 'that', '&amp;', 'quot', ';', 'the', 'report', 'is', 'narrowly', 'focused', 'on', 'the', 'final', 'days', 'before', 'the', 'explosion', 'rather', 'than', 'on', 'earlier', 'decisions', 'about', 'well', 'design', 'and', 'safety', 'procedures', '.', '&amp;', 'quot', ';']
PRED 237: အ ဆို ပါ အ စီ ရင် ခံ စာ တွင် ဖော် ပြ ထား သ ည့် ဓာတ် ခွဲ ခန်း ၏ လုံ ခြုံ ရေး ဆိုင် ရာ လုပ် ထုံး လုပ် နည်း များ သည် စော စော ပိုင်း အ စီ ရင် ခံ စာ တွင် ထ ည့် သွင်း ဖော် ပြ ထား သ ည့် အ ချက် အ လက် များ နှ င့် သက် ဆိုင် သ ည့် အ ချက် များ ကို ဖော် ပြ ထား သည် ။
PRED SCORE: -51.9576

[2021-03-21 17:05:16,866 INFO] 
SENT 238: ['&amp;', 'quot', ';', 'No', 'BP', 'officials', 'have', 'been', 'sacked', 'for', 'their', 'role', 'in', 'the', 'explosion', ',', 'and', 'Bly', 'said', 'there', 'was', 'no', 'indication', 'of', 'any', 'blame', 'beyond', 'the', 'well-site', 'managers', '.', '&amp;', 'quot', ';']
PRED 238: မ တော် တ ဆ ထိ ခိုက် မှု ဖြစ် ပွား မှု အ တွက် တာ ဝန် ရှိ သူ များ က အ ပြစ် မ ရှိ ကြောင်း ပြော ကြား ပြီး ဖြစ် ပါ သည် ။
PRED SCORE: -29.5328

[2021-03-21 17:05:16,866 INFO] 
SENT 239: ['The', 'Associated', 'Press', 'reported', 'that', 'Bly', '&amp;', 'quot', ';', 'said', 'at', 'a', 'briefing', 'in', 'Washington', 'that', 'the', 'internal', 'report', 'was', 'a', 'reconstruction', 'of', 'what', 'happened', 'on', 'the', 'rig', 'based', 'on', 'the', 'company', '&amp;', 'apos', ';', 's', 'data', 'and', 'interviews', 'with', 'mostly', 'BP', 'employees', 'and', 'was', 'not', 'meant', 'to', 'focus', 'on', 'assigning', 'blame', '.', '&amp;', 'quot', ';']
PRED 239: အ ဆို ပါ သ တင်း စာ ရှင်း လင်း ပွဲ တွင် ဖော် ပြ ထား သ ည့် အ ဆို ပါ သ တင်း အ ချက် အ လက် များ ကို ဖော် ပြ ထား သ ည့် အ ကြောင်း အ ရာ များ အ ပေါ် အ ခြေ ခံ ၍ ပြန် လည် ဖော် ပြ ထား သ ည့် အ ကြောင်း အ ရာ များ နှ င့် စပ် လျဉ်း ၍ အ ဆို ပါ အ စီ ရင် ခံ စာ တွင် ဖော် ပြ ထား သ ည့် အ ချက် အ လက် များ ကို ဖော် ပြ ထား ခြင်း မ ရှိ ပါ ဟု ဖော် ပြ ထား သည် ။
PRED SCORE: -65.5599

[2021-03-21 17:05:16,866 INFO] 
SENT 240: ['&amp;', 'quot', ';', 'The', 'six-person', 'investigating', 'panel', 'only', 'had', 'access', 'to', 'a', 'few', 'workers', 'from', 'other', 'companies', ',', 'and', 'samples', 'of', 'the', 'actual', 'cement', 'used', 'in', 'the', 'well', 'were', 'not', 'released', '.', '&amp;', 'quot', ';']
PRED 240: အ လုပ် သ မား အင် အား အ နည်း ငယ် သာ ပါ က အ လုပ် သ မား အင် အား အ နည်း ငယ် သာ ရှိ ပြီး အ လုပ် သ မား အင် အား အ သုံး ပြု သ ည့် အ လုပ် သ မား အင် အား အ သုံး ပြု သ ည့် အ လုပ် သ မား အင် အား အ နည်း ငယ် သာ သာ ရှိ ပါ သည် ။
PRED SCORE: -47.1950

```

Training လုပ်တုန်းက ဗမာစာဘက် အခြမ်းကို syllable breaking လုပ်ပြီးမှ train ထားတာမို့ translation/testing လုပ်တဲ့အခါမှာလည်း translated output က syllable ဖြတ်ပြီးသားအနေနဲ့ပဲ ရပါလိမ့်မယ်။  

## Reference

Reference for the more complex configuration file:  
https://github.com/OpenNMT/OpenNMT-py/tree/master/config  

Paper: OpenNMT: Neural Machine Translation Toolkit  
Link: https://www.aclweb.org/anthology/W18-1817.pdf

An open source neural machine translation system.  
https://opennmt.net/

Ref for the English-Myanmar Corpus:  
https://lotus.kuee.kyoto-u.ac.jp/WAT/WAT2021/index.html
