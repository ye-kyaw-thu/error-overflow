## Installing OpenNMT

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

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ tar xf toy-ende.tar.gz
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ cd toy-ende/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ ls
src-test.txt  src-train.txt  src-val.txt  tgt-test.txt  tgt-train.txt  tgt-val.txt
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial/toy-ende$ 
```

## Check the Data

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

Reference for the more complex configuration file:
https://github.com/OpenNMT/OpenNMT-py/tree/master/config

On my computer:
/home/ye/tool/OpenNMT-py/config


## Training

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

## Release

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ onmt_release_model --model toy-ende/run/model_step_1000.pt --output toy-ende/run/model_step_1000_release.pt
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/nmt/openNMT/tutorial$ ls ./toy-ende/run/
example.vocab.src  example.vocab.tgt  model_step_1000.pt  model_step_1000_release.pt  model_step_500.pt


## Reference

Paper: OpenNMT: Neural Machine Translation Toolkit
Link: https://www.aclweb.org/anthology/W18-1817.pdf

An open source neural machine translation system.
https://opennmt.net/



Screenshot png file path:
nvidia-smi-screenshot-onmt-tutorial-running-onGPU0.png
