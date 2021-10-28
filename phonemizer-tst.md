
## git clone

```
(base) ye@:/media/ye/project1/exp$ git clone https://github.com/bootphon/phonemizer
Cloning into 'phonemizer'...
remote: Enumerating objects: 1754, done.
remote: Counting objects: 100% (634/634), done.
remote: Compressing objects: 100% (377/377), done.
remote: Total 1754 (delta 438), reused 429 (delta 252), pack-reused 1120
Receiving objects: 100% (1754/1754), 528.08 KiB | 4.63 MiB/s, done.
Resolving deltas: 100% (1206/1206), done.
(base) ye@:/media/ye/project1/exp$
```

## run setup.py

```
(base) ye@:/media/ye/project1/exp$ cd phonemizer/
(base) ye@:/media/ye/project1/exp/phonemizer$ sudo python setup.py install
[sudo] password for ye: 
Partial import of phonemizer during the build process.
running install
running bdist_egg
running egg_info
creating phonemizer.egg-info
writing phonemizer.egg-info/PKG-INFO
writing dependency_links to phonemizer.egg-info/dependency_links.txt
writing entry points to phonemizer.egg-info/entry_points.txt
writing requirements to phonemizer.egg-info/requires.txt
writing top-level names to phonemizer.egg-info/top_level.txt
writing manifest file 'phonemizer.egg-info/SOURCES.txt'
reading manifest file 'phonemizer.egg-info/SOURCES.txt'
writing manifest file 'phonemizer.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/phonemizer
copying phonemizer/__init__.py -> build/lib/phonemizer
copying phonemizer/logger.py -> build/lib/phonemizer
copying phonemizer/main.py -> build/lib/phonemizer
copying phonemizer/phonemize.py -> build/lib/phonemizer
copying phonemizer/punctuation.py -> build/lib/phonemizer
copying phonemizer/separator.py -> build/lib/phonemizer
copying phonemizer/utils.py -> build/lib/phonemizer
copying phonemizer/version.py -> build/lib/phonemizer
creating build/lib/test
copying test/__init__.py -> build/lib/test
copying test/test_espeak.py -> build/lib/test
copying test/test_espeak_lang_switch.py -> build/lib/test
copying test/test_espeak_word_mismatch.py -> build/lib/test
copying test/test_espeak_wrapper.py -> build/lib/test
copying test/test_festival.py -> build/lib/test
copying test/test_import.py -> build/lib/test
copying test/test_main.py -> build/lib/test
copying test/test_mbrola.py -> build/lib/test
copying test/test_phonemize.py -> build/lib/test
copying test/test_punctuation.py -> build/lib/test
copying test/test_segments.py -> build/lib/test
copying test/test_separator.py -> build/lib/test
copying test/test_utils.py -> build/lib/test
creating build/lib/phonemizer/backend
copying phonemizer/backend/__init__.py -> build/lib/phonemizer/backend
copying phonemizer/backend/base.py -> build/lib/phonemizer/backend
copying phonemizer/backend/segments.py -> build/lib/phonemizer/backend
creating build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/__init__.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/api.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/base.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/espeak.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/language_switch.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/mbrola.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/voice.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/words_mismatch.py -> build/lib/phonemizer/backend/espeak
copying phonemizer/backend/espeak/wrapper.py -> build/lib/phonemizer/backend/espeak
creating build/lib/phonemizer/backend/festival
copying phonemizer/backend/festival/__init__.py -> build/lib/phonemizer/backend/festival
copying phonemizer/backend/festival/festival.py -> build/lib/phonemizer/backend/festival
copying phonemizer/backend/festival/lispy.py -> build/lib/phonemizer/backend/festival
creating build/lib/phonemizer/share
creating build/lib/phonemizer/share/festival
copying phonemizer/share/festival/phonemize.scm -> build/lib/phonemizer/share/festival
creating build/lib/phonemizer/share/segments
copying phonemizer/share/segments/chintang.g2p -> build/lib/phonemizer/share/segments
copying phonemizer/share/segments/cree.g2p -> build/lib/phonemizer/share/segments
copying phonemizer/share/segments/inuktitut.g2p -> build/lib/phonemizer/share/segments
copying phonemizer/share/segments/japanese.g2p -> build/lib/phonemizer/share/segments
copying phonemizer/share/segments/sesotho.g2p -> build/lib/phonemizer/share/segments
copying phonemizer/share/segments/yucatec.g2p -> build/lib/phonemizer/share/segments
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/logger.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/main.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/phonemize.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/punctuation.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/separator.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/utils.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/version.py -> build/bdist.linux-x86_64/egg/phonemizer
creating build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/base.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/segments.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
creating build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/api.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/base.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/espeak.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/language_switch.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/mbrola.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/voice.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/words_mismatch.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/wrapper.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
creating build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/festival.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/lispy.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
creating build/bdist.linux-x86_64/egg/phonemizer/share
creating build/bdist.linux-x86_64/egg/phonemizer/share/festival
copying build/lib/phonemizer/share/festival/phonemize.scm -> build/bdist.linux-x86_64/egg/phonemizer/share/festival
creating build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/chintang.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/cree.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/inuktitut.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/japanese.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/sesotho.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/yucatec.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
creating build/bdist.linux-x86_64/egg/test
copying build/lib/test/__init__.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_lang_switch.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_word_mismatch.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_wrapper.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_festival.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_import.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_main.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_mbrola.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_phonemize.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_punctuation.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_segments.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_separator.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_utils.py -> build/bdist.linux-x86_64/egg/test
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/logger.py to logger.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/main.py to main.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/phonemize.py to phonemize.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/punctuation.py to punctuation.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/separator.py to separator.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/utils.py to utils.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/version.py to version.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/base.py to base.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/segments.py to segments.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/api.py to api.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/base.py to base.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/espeak.py to espeak.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/language_switch.py to language_switch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/mbrola.py to mbrola.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/voice.py to voice.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/words_mismatch.py to words_mismatch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/wrapper.py to wrapper.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/festival.py to festival.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/lispy.py to lispy.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak.py to test_espeak.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_lang_switch.py to test_espeak_lang_switch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_word_mismatch.py to test_espeak_word_mismatch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_wrapper.py to test_espeak_wrapper.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_festival.py to test_festival.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_import.py to test_import.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_main.py to test_main.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_mbrola.py to test_mbrola.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_phonemize.py to test_phonemize.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_punctuation.py to test_punctuation.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_segments.py to test_segments.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_separator.py to test_separator.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_utils.py to test_utils.cpython-38.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
creating dist
creating 'dist/phonemizer-3.0-py3.8.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing phonemizer-3.0-py3.8.egg
Copying phonemizer-3.0-py3.8.egg to /usr/local/lib/python3.8/dist-packages
Adding phonemizer 3.0 to easy-install.pth file
Installing phonemize script to /usr/local/bin

Installed /usr/local/lib/python3.8/dist-packages/phonemizer-3.0-py3.8.egg
Processing dependencies for phonemizer==3.0
Searching for segments
Reading https://pypi.org/simple/segments/
Downloading https://files.pythonhosted.org/packages/1e/ae/02d31d73cfc3fa1dc74b7b7f14820fadc287e74406583d7af7b80fcaac41/segments-2.2.0-py2.py3-none-any.whl#sha256=1175ca7210e443045c0b0642d735cb7cad7cd5e09d6914a8f04cfc7c4be9af1a
Best match: segments 2.2.0
Processing segments-2.2.0-py2.py3-none-any.whl
Installing segments-2.2.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding segments 2.2.0 to easy-install.pth file
Installing segments script to /usr/local/bin

Installed /usr/local/lib/python3.8/dist-packages/segments-2.2.0-py3.8.egg
Searching for joblib
Reading https://pypi.org/simple/joblib/
Downloading https://files.pythonhosted.org/packages/3e/d5/0163eb0cfa0b673aa4fe1cd3ea9d8a81ea0f32e50807b0c295871e4aab2e/joblib-1.1.0-py2.py3-none-any.whl#sha256=f21f109b3c7ff9d95f8387f752d0d9c34a02aa2f7060c2135f465da0e5160ff6
Best match: joblib 1.1.0
Processing joblib-1.1.0-py2.py3-none-any.whl
Installing joblib-1.1.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding joblib 1.1.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/joblib-1.1.0-py3.8.egg
Searching for dlinfo
Reading https://pypi.org/simple/dlinfo/
Downloading https://files.pythonhosted.org/packages/a7/f9/e014eb5740dfc6ebe6105f4c38890f361e5b0e1537a9f04bb4f34432efb9/dlinfo-1.2.1-py3-none-any.whl#sha256=a97d7cc66d997b4ac491f0e8068eb324790994834951a9beb5a4619835b361d9
Best match: dlinfo 1.2.1
Processing dlinfo-1.2.1-py3-none-any.whl
Installing dlinfo-1.2.1-py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding dlinfo 1.2.1 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/dlinfo-1.2.1-py3.8.egg
Searching for attrs>=18.1
Reading https://pypi.org/simple/attrs/
Downloading https://files.pythonhosted.org/packages/20/a9/ba6f1cd1a1517ff022b35acd6a7e4246371dfab08b8e42b829b6d07913cc/attrs-21.2.0-py2.py3-none-any.whl#sha256=149e90d6d8ac20db7a955ad60cf0e6881a3f20d37096140088356da6c716b0b1
Best match: attrs 21.2.0
Processing attrs-21.2.0-py2.py3-none-any.whl
Installing attrs-21.2.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding attrs 21.2.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/attrs-21.2.0-py3.8.egg
Searching for regex
Reading https://pypi.org/simple/regex/
Downloading https://files.pythonhosted.org/packages/bc/53/13796a617c5cf34648c7bec837f2d5d1132168adfd7d16038a20fa1e361a/regex-2021.10.23-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl#sha256=13ec99df95003f56edcd307db44f06fbeb708c4ccdcf940478067dd62353181e
Best match: regex 2021.10.23
Processing regex-2021.10.23-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
Installing regex-2021.10.23-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl to /usr/local/lib/python3.8/dist-packages
Adding regex 2021.10.23 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/regex-2021.10.23-py3.8-linux-x86_64.egg
Searching for csvw>=1.5.6
Reading https://pypi.org/simple/csvw/
Downloading https://files.pythonhosted.org/packages/55/ae/afb43a6b88c4202d29e4ec7aca76633d8c530140f4f5a32ee762d07c4607/csvw-1.11.0-py2.py3-none-any.whl#sha256=243825391308f2568593415364868dda5e50f608fc2bb307fbd79d534af52fd5
Best match: csvw 1.11.0
Processing csvw-1.11.0-py2.py3-none-any.whl
Installing csvw-1.11.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding csvw 1.11.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/csvw-1.11.0-py3.8.egg
Searching for clldutils>=1.7.3
Reading https://pypi.org/simple/clldutils/
Downloading https://files.pythonhosted.org/packages/21/41/4641a3bd20ec2a025ae7c2d912095afb57b55a0da574f6549f6a16f3ac10/clldutils-3.10.0-py2.py3-none-any.whl#sha256=4c6b36e50416c6c4d2a7aec62e1ed4ac9a5ebd03bc550279ed05fdfe807d7244
Best match: clldutils 3.10.0
Processing clldutils-3.10.0-py2.py3-none-any.whl
Installing clldutils-3.10.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding clldutils 3.10.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/clldutils-3.10.0-py3.8.egg
Searching for uritemplate>=3.0.0
Reading https://pypi.org/simple/uritemplate/
Downloading https://files.pythonhosted.org/packages/81/c0/7461b49cd25aeece13766f02ee576d1db528f1c37ce69aee300e075b485b/uritemplate-4.1.1-py2.py3-none-any.whl#sha256=830c08b8d99bdd312ea4ead05994a38e8936266f84b9a7878232db50b044e02e
Best match: uritemplate 4.1.1
Processing uritemplate-4.1.1-py2.py3-none-any.whl
Installing uritemplate-4.1.1-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding uritemplate 4.1.1 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/uritemplate-4.1.1-py3.8.egg
Searching for rfc3986
Reading https://pypi.org/simple/rfc3986/
Downloading https://files.pythonhosted.org/packages/c4/e5/63ca2c4edf4e00657584608bee1001302bbf8c5f569340b78304f2f446cb/rfc3986-1.5.0-py2.py3-none-any.whl#sha256=a86d6e1f5b1dc238b218b012df0aa79409667bb209e58da56d0b94704e712a97
Best match: rfc3986 1.5.0
Processing rfc3986-1.5.0-py2.py3-none-any.whl
Installing rfc3986-1.5.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding rfc3986 1.5.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/rfc3986-1.5.0-py3.8.egg
Searching for isodate
Reading https://pypi.org/simple/isodate/
Downloading https://files.pythonhosted.org/packages/9b/9f/b36f7774ff5ea8e428fdcfc4bb332c39ee5b9362ddd3d40d9516a55221b2/isodate-0.6.0-py2.py3-none-any.whl#sha256=aa4d33c06640f5352aca96e4b81afd8ab3b47337cc12089822d6f322ac772c81
Best match: isodate 0.6.0
Processing isodate-0.6.0-py2.py3-none-any.whl
Installing isodate-0.6.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding isodate 0.6.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/isodate-0.6.0-py3.8.egg
Searching for tabulate>=0.7.7
Reading https://pypi.org/simple/tabulate/
Downloading https://files.pythonhosted.org/packages/ca/80/7c0cad11bd99985cfe7c09427ee0b4f9bd6b048bd13d4ffb32c6db237dfb/tabulate-0.8.9-py3-none-any.whl#sha256=d7c013fe7abbc5e491394e10fa845f8f32fe54f8dc60c6622c6cf482d25d47e4
Best match: tabulate 0.8.9
Processing tabulate-0.8.9-py3-none-any.whl
Installing tabulate-0.8.9-py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding tabulate 0.8.9 to easy-install.pth file
Installing tabulate script to /usr/local/bin

Installed /usr/local/lib/python3.8/dist-packages/tabulate-0.8.9-py3.8.egg
Searching for colorlog
Reading https://pypi.org/simple/colorlog/
Downloading https://files.pythonhosted.org/packages/19/11/6daf005ecf7e00ec431f369b79029cd4a7bf47121a891f8a72be8f2b4bcb/colorlog-6.5.0-py2.py3-none-any.whl#sha256=d334b1b8dae5989b786232f05586a7a0111feb24ff9cfc8310c3347a91388717
Best match: colorlog 6.5.0
Processing colorlog-6.5.0-py2.py3-none-any.whl
Installing colorlog-6.5.0-py2.py3-none-any.whl to /usr/local/lib/python3.8/dist-packages
Adding colorlog 6.5.0 to easy-install.pth file

Installed /usr/local/lib/python3.8/dist-packages/colorlog-6.5.0-py3.8.egg
Searching for python-dateutil==2.8.1
Best match: python-dateutil 2.8.1
Adding python-dateutil 2.8.1 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Finished processing dependencies for phonemizer==3.0
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

## run pytest and got error

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pytest
================================================================= test session starts ==================================================================
platform linux -- Python 3.7.6, pytest-5.3.5, py-1.8.1, pluggy-0.13.1
rootdir: /media/ye/project1/exp/phonemizer, inifile: setup.cfg, testpaths: test
plugins: remotedata-0.3.2, openfiles-0.4.0, astropy-header-0.1.2, doctestplus-0.5.0, arraydiff-0.3, hydra-core-1.0.5, hypothesis-5.5.4
collected 14 items / 10 errors / 4 selected                                                                                                            

======================================================================== ERRORS ========================================================================
_________________________________________________________ ERROR collecting test/test_espeak.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_espeak.py:24: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
___________________________________________________ ERROR collecting test/test_espeak_lang_switch.py ___________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_lang_switch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_espeak_lang_switch.py:22: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________ ERROR collecting test/test_espeak_word_mismatch.py __________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_word_mismatch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_espeak_word_mismatch.py:9: in <module>
    from phonemizer import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_____________________________________________________ ERROR collecting test/test_espeak_wrapper.py _____________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_wrapper.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_espeak_wrapper.py:27: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_festival.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_festival.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_festival.py:27: in <module>
    from phonemizer.backend import FestivalBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________________ ERROR collecting test/test_main.py __________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_main.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_main.py:27: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_________________________________________________________ ERROR collecting test/test_mbrola.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_mbrola.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_mbrola.py:22: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_______________________________________________________ ERROR collecting test/test_phonemize.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_phonemize.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_phonemize.py:22: in <module>
    from phonemizer.phonemize import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
______________________________________________________ ERROR collecting test/test_punctuation.py _______________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_punctuation.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_punctuation.py:21: in <module>
    from phonemizer.backend import EspeakBackend, FestivalBackend, SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_segments.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_segments.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
test/test_segments.py:24: in <module>
    from phonemizer.backend import SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 10 errors during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
================================================================== 10 errors in 0.30s ==================================================================
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

## error fixing

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pip uninstall pytest
Found existing installation: pytest 5.3.5
Uninstalling pytest-5.3.5:
  Would remove:
    /home/ye/anaconda3/bin/py.test
    /home/ye/anaconda3/bin/pytest
    /home/ye/anaconda3/lib/python3.7/site-packages/_pytest
    /home/ye/anaconda3/lib/python3.7/site-packages/pytest
    /home/ye/anaconda3/lib/python3.7/site-packages/pytest-5.3.5-py3.7.egg-info
Proceed (Y/n)? Y
  Successfully uninstalled pytest-5.3.5
(base) ye@:/media/ye/project1/exp/phonemizer$ pip install pytest
Collecting pytest
  Downloading pytest-6.2.5-py3-none-any.whl (280 kB)
     |████████████████████████████████| 280 kB 1.7 MB/s            
Collecting iniconfig
  Downloading iniconfig-1.1.1-py2.py3-none-any.whl (5.0 kB)
Requirement already satisfied: packaging in /home/ye/anaconda3/lib/python3.7/site-packages (from pytest) (21.0)
Requirement already satisfied: toml in /home/ye/anaconda3/lib/python3.7/site-packages (from pytest) (0.10.2)
Requirement already satisfied: attrs>=19.2.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from pytest) (19.3.0)
Requirement already satisfied: importlib-metadata>=0.12 in /home/ye/anaconda3/lib/python3.7/site-packages (from pytest) (1.5.0)
Requirement already satisfied: pluggy<2.0,>=0.12 in /home/ye/anaconda3/lib/python3.7/site-packages (from pytest) (0.13.1)
Collecting py>=1.8.2
  Downloading py-1.10.0-py2.py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 6.4 MB/s             
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from importlib-metadata>=0.12->pytest) (2.2.0)
Requirement already satisfied: pyparsing>=2.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from packaging->pytest) (2.4.6)
Installing collected packages: py, iniconfig, pytest
  Attempting uninstall: py
    Found existing installation: py 1.8.1
    Uninstalling py-1.8.1:
      Successfully uninstalled py-1.8.1
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
pytest-astropy 0.8.0 requires pytest-cov>=2.0, which is not installed.
pytest-astropy 0.8.0 requires pytest-filter-subpackage>=0.1, which is not installed.
Successfully installed iniconfig-1.1.1 py-1.10.0 pytest-6.2.5
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

Try again...  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pytest
================================================================= test session starts ==================================================================
platform linux -- Python 3.7.6, pytest-6.2.5, py-1.10.0, pluggy-0.13.1
rootdir: /media/ye/project1/exp/phonemizer, configfile: setup.cfg, testpaths: test
plugins: remotedata-0.3.2, openfiles-0.4.0, astropy-header-0.1.2, doctestplus-0.5.0, arraydiff-0.3, hydra-core-1.0.5, hypothesis-5.5.4
collected 14 items / 10 errors / 4 selected                                                                                                            

======================================================================== ERRORS ========================================================================
_________________________________________________________ ERROR collecting test/test_espeak.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak.py:24: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
___________________________________________________ ERROR collecting test/test_espeak_lang_switch.py ___________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_lang_switch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_lang_switch.py:22: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________ ERROR collecting test/test_espeak_word_mismatch.py __________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_word_mismatch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_word_mismatch.py:9: in <module>
    from phonemizer import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_____________________________________________________ ERROR collecting test/test_espeak_wrapper.py _____________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_wrapper.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_wrapper.py:27: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_festival.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_festival.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_festival.py:27: in <module>
    from phonemizer.backend import FestivalBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________________ ERROR collecting test/test_main.py __________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_main.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_main.py:27: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_________________________________________________________ ERROR collecting test/test_mbrola.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_mbrola.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_mbrola.py:22: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_______________________________________________________ ERROR collecting test/test_phonemize.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_phonemize.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_phonemize.py:22: in <module>
    from phonemizer.phonemize import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
______________________________________________________ ERROR collecting test/test_punctuation.py _______________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_punctuation.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_punctuation.py:21: in <module>
    from phonemizer.backend import EspeakBackend, FestivalBackend, SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_segments.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_segments.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_segments.py:24: in <module>
    from phonemizer.backend import SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
=============================================================== short test summary info ================================================================
ERROR test/test_espeak.py
ERROR test/test_espeak_lang_switch.py
ERROR test/test_espeak_word_mismatch.py
ERROR test/test_espeak_wrapper.py
ERROR test/test_festival.py
ERROR test/test_main.py
ERROR test/test_mbrola.py
ERROR test/test_phonemize.py
ERROR test/test_punctuation.py
ERROR test/test_segments.py
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 10 errors during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
================================================================== 10 errors in 0.31s ==================================================================
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

Refer to Issue 11:  
[https://github.com/bootphon/phonemizer/issues/11](https://github.com/bootphon/phonemizer/issues/11)  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ sudo apt-get install python-setuptools
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  apturl-common gir1.2-goa-1.0 ibverbs-providers libboost-atomic-dev libboost-atomic1.71-dev libboost-atomic1.71.0 libboost-chrono-dev
  libboost-chrono1.71-dev libboost-chrono1.71.0 libboost-container-dev libboost-container1.71-dev libboost-container1.71.0 libboost-context-dev
  libboost-context1.71-dev libboost-context1.71.0 libboost-coroutine-dev libboost-coroutine1.71-dev libboost-coroutine1.71.0 libboost-date-time-dev
  libboost-date-time1.71-dev libboost-dev libboost-exception-dev libboost-exception1.71-dev libboost-fiber-dev libboost-fiber1.71-dev
  libboost-fiber1.71.0 libboost-filesystem-dev libboost-filesystem1.71-dev libboost-graph-parallel-dev libboost-graph-parallel1.71-dev
  libboost-graph-parallel1.71.0 libboost-graph1.71.0 libboost-locale-dev libboost-locale1.71-dev libboost-log1.71.0 libboost-math-dev
  libboost-math1.71-dev libboost-math1.71.0 libboost-mpi-dev libboost-mpi-python-dev libboost-mpi-python1.71-dev libboost-mpi-python1.71.0
  libboost-mpi1.71-dev libboost-mpi1.71.0 libboost-numpy-dev libboost-numpy1.71-dev libboost-numpy1.71.0 libboost-program-options-dev
  libboost-program-options1.71-dev libboost-program-options1.71.0 libboost-python-dev libboost-python1.71-dev libboost-python1.71.0
  libboost-random-dev libboost-random1.71-dev libboost-random1.71.0 libboost-regex1.71.0 libboost-serialization-dev libboost-serialization1.71-dev
  libboost-serialization1.71.0 libboost-stacktrace-dev libboost-stacktrace1.71-dev libboost-stacktrace1.71.0 libboost-system-dev
  libboost-system1.71-dev libboost-system1.71.0 libboost-test-dev libboost-test1.71-dev libboost-test1.71.0 libboost-thread-dev
  libboost-thread1.71-dev libboost-timer-dev libboost-timer1.71-dev libboost-timer1.71.0 libboost-tools-dev libboost-type-erasure-dev
  libboost-type-erasure1.71-dev libboost-type-erasure1.71.0 libboost-wave-dev libboost-wave1.71-dev libboost-wave1.71.0 libboost1.71-dev
  libboost1.71-tools-dev libcaf-openmpi-3 libcoarrays-openmpi-dev libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7
  libevent-pthreads-2.1-7 libfabric1 libhwloc-dev libhwloc-plugins libhwloc15 libibverbs-dev libibverbs1 libnl-3-dev libnl-route-3-dev libnuma-dev
  libopenmpi-dev libopenmpi3 libpmix2 libpsm-infinipath1 libpsm2-2 librdmacm1 mpi-default-bin mpi-default-dev openmpi-bin openmpi-common python3-click
  python3-colorama python3-dateutil python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  python-pkg-resources
Suggested packages:
  python-setuptools-doc
The following NEW packages will be installed:
  python-pkg-resources python-setuptools
0 upgraded, 2 newly installed, 0 to remove and 21 not upgraded.
Need to get 453 kB of archives.
After this operation, 2,023 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python-pkg-resources all 44.1.1-1 [127 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python-setuptools all 44.1.1-1 [326 kB]
Fetched 453 kB in 2s (191 kB/s)            
Selecting previously unselected package python-pkg-resources.
(Reading database ... 657143 files and directories currently installed.)
Preparing to unpack .../python-pkg-resources_44.1.1-1_all.deb ...
Unpacking python-pkg-resources (44.1.1-1) ...
Selecting previously unselected package python-setuptools.
Preparing to unpack .../python-setuptools_44.1.1-1_all.deb ...
Unpacking python-setuptools (44.1.1-1) ...
Setting up python-pkg-resources (44.1.1-1) ...
Setting up python-setuptools (44.1.1-1) ...
(base) ye@:/media/ye/project1/exp/phonemizer$
```

## installation of dependencies

```
(base) ye@:/media/ye/project1/exp/phonemizer$ sudo apt-get install festival espeak-ng mbrola
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  apturl-common gir1.2-goa-1.0 ibverbs-providers libboost-atomic-dev libboost-atomic1.71-dev libboost-atomic1.71.0 libboost-chrono-dev
  libboost-chrono1.71-dev libboost-chrono1.71.0 libboost-container-dev libboost-container1.71-dev libboost-container1.71.0 libboost-context-dev
  libboost-context1.71-dev libboost-context1.71.0 libboost-coroutine-dev libboost-coroutine1.71-dev libboost-coroutine1.71.0 libboost-date-time-dev
  libboost-date-time1.71-dev libboost-dev libboost-exception-dev libboost-exception1.71-dev libboost-fiber-dev libboost-fiber1.71-dev
  libboost-fiber1.71.0 libboost-filesystem-dev libboost-filesystem1.71-dev libboost-graph-parallel-dev libboost-graph-parallel1.71-dev
  libboost-graph-parallel1.71.0 libboost-graph1.71.0 libboost-locale-dev libboost-locale1.71-dev libboost-log1.71.0 libboost-math-dev
  libboost-math1.71-dev libboost-math1.71.0 libboost-mpi-dev libboost-mpi-python-dev libboost-mpi-python1.71-dev libboost-mpi-python1.71.0
  libboost-mpi1.71-dev libboost-mpi1.71.0 libboost-numpy-dev libboost-numpy1.71-dev libboost-numpy1.71.0 libboost-program-options-dev
  libboost-program-options1.71-dev libboost-program-options1.71.0 libboost-python-dev libboost-python1.71-dev libboost-python1.71.0
  libboost-random-dev libboost-random1.71-dev libboost-random1.71.0 libboost-regex1.71.0 libboost-serialization-dev libboost-serialization1.71-dev
  libboost-serialization1.71.0 libboost-stacktrace-dev libboost-stacktrace1.71-dev libboost-stacktrace1.71.0 libboost-system-dev
  libboost-system1.71-dev libboost-system1.71.0 libboost-test-dev libboost-test1.71-dev libboost-test1.71.0 libboost-thread-dev
  libboost-thread1.71-dev libboost-timer-dev libboost-timer1.71-dev libboost-timer1.71.0 libboost-tools-dev libboost-type-erasure-dev
  libboost-type-erasure1.71-dev libboost-type-erasure1.71.0 libboost-wave-dev libboost-wave1.71-dev libboost-wave1.71.0 libboost1.71-dev
  libboost1.71-tools-dev libcaf-openmpi-3 libcoarrays-openmpi-dev libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7
  libevent-pthreads-2.1-7 libfabric1 libhwloc-dev libhwloc-plugins libhwloc15 libibverbs-dev libibverbs1 libnl-3-dev libnl-route-3-dev libnuma-dev
  libopenmpi-dev libopenmpi3 libpmix2 libpsm-infinipath1 libpsm2-2 librdmacm1 mpi-default-bin mpi-default-dev openmpi-bin openmpi-common python3-click
  python3-colorama python3-dateutil python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  festlex-cmu festlex-poslex festvox-kallpc16k libestools2.5
Suggested packages:
  pidgin-festival festival-freebsoft-utils mbrola-voice cicero
The following NEW packages will be installed:
  espeak-ng festival festlex-cmu festlex-poslex festvox-kallpc16k libestools2.5 mbrola
0 upgraded, 7 newly installed, 0 to remove and 21 not upgraded.
Need to get 6,888 kB of archives.
After this operation, 23.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 espeak-ng amd64 1.50+dfsg-7 [322 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libestools2.5 amd64 1:2.5.0-9 [901 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 festival amd64 1:2.5.0-4build1 [805 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 festlex-cmu all 2.4-2 [895 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 festlex-poslex all 2.4-1 [186 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/multiverse amd64 mbrola amd64 3.3+dfsg-2 [165 kB]
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 festvox-kallpc16k all 2.4-1 [3,614 kB]
Fetched 6,888 kB in 2s (2,819 kB/s)          
Selecting previously unselected package espeak-ng.
(Reading database ... 657272 files and directories currently installed.)
Preparing to unpack .../0-espeak-ng_1.50+dfsg-7_amd64.deb ...
Unpacking espeak-ng (1.50+dfsg-7) ...
Selecting previously unselected package libestools2.5:amd64.
Preparing to unpack .../1-libestools2.5_1%3a2.5.0-9_amd64.deb ...
Unpacking libestools2.5:amd64 (1:2.5.0-9) ...
Selecting previously unselected package festival.
Preparing to unpack .../2-festival_1%3a2.5.0-4build1_amd64.deb ...
Unpacking festival (1:2.5.0-4build1) ...
Selecting previously unselected package festlex-cmu.
Preparing to unpack .../3-festlex-cmu_2.4-2_all.deb ...
Unpacking festlex-cmu (2.4-2) ...
Selecting previously unselected package festlex-poslex.
Preparing to unpack .../4-festlex-poslex_2.4-1_all.deb ...
Unpacking festlex-poslex (2.4-1) ...
Selecting previously unselected package mbrola.
Preparing to unpack .../5-mbrola_3.3+dfsg-2_amd64.deb ...
Unpacking mbrola (3.3+dfsg-2) ...
Selecting previously unselected package festvox-kallpc16k.
Preparing to unpack .../6-festvox-kallpc16k_2.4-1_all.deb ...
Unpacking festvox-kallpc16k (2.4-1) ...
Setting up mbrola (3.3+dfsg-2) ...
Setting up libestools2.5:amd64 (1:2.5.0-9) ...
Setting up festival (1:2.5.0-4build1) ...
Setting up espeak-ng (1.50+dfsg-7) ...
Processing triggers for sgml-base (1.30) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
install-info: warning: no info dir entry in `/usr/share/info/automake-history.info.gz'
Processing triggers for libc-bin (2.32-0ubuntu3) ...
/sbin/ldconfig.real: /usr/local/lib/liblouis.so.20 is not a symbolic link

Processing triggers for man-db (2.9.3-2) ...
Setting up festlex-poslex (2.4-1) ...
Setting up festlex-cmu (2.4-2) ...
Setting up festvox-kallpc16k (2.4-1) ...
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ sudo python ./setup.py install
Partial import of phonemizer during the build process.
running install
running bdist_egg
running egg_info
writing phonemizer.egg-info/PKG-INFO
writing dependency_links to phonemizer.egg-info/dependency_links.txt
writing entry points to phonemizer.egg-info/entry_points.txt
writing requirements to phonemizer.egg-info/requires.txt
writing top-level names to phonemizer.egg-info/top_level.txt
reading manifest file 'phonemizer.egg-info/SOURCES.txt'
writing manifest file 'phonemizer.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/logger.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/main.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/phonemize.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/punctuation.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/separator.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/utils.py -> build/bdist.linux-x86_64/egg/phonemizer
copying build/lib/phonemizer/version.py -> build/bdist.linux-x86_64/egg/phonemizer
creating build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/base.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
copying build/lib/phonemizer/backend/segments.py -> build/bdist.linux-x86_64/egg/phonemizer/backend
creating build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/api.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/base.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/espeak.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/language_switch.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/mbrola.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/voice.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/words_mismatch.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
copying build/lib/phonemizer/backend/espeak/wrapper.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/espeak
creating build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/__init__.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/festival.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
copying build/lib/phonemizer/backend/festival/lispy.py -> build/bdist.linux-x86_64/egg/phonemizer/backend/festival
creating build/bdist.linux-x86_64/egg/phonemizer/share
creating build/bdist.linux-x86_64/egg/phonemizer/share/festival
copying build/lib/phonemizer/share/festival/phonemize.scm -> build/bdist.linux-x86_64/egg/phonemizer/share/festival
creating build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/chintang.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/cree.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/inuktitut.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/japanese.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/sesotho.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
copying build/lib/phonemizer/share/segments/yucatec.g2p -> build/bdist.linux-x86_64/egg/phonemizer/share/segments
creating build/bdist.linux-x86_64/egg/test
copying build/lib/test/__init__.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_lang_switch.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_word_mismatch.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_espeak_wrapper.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_festival.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_import.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_main.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_mbrola.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_phonemize.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_punctuation.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_segments.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_separator.py -> build/bdist.linux-x86_64/egg/test
copying build/lib/test/test_utils.py -> build/bdist.linux-x86_64/egg/test
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/logger.py to logger.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/main.py to main.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/phonemize.py to phonemize.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/punctuation.py to punctuation.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/separator.py to separator.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/utils.py to utils.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/version.py to version.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/base.py to base.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/segments.py to segments.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/api.py to api.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/base.py to base.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/espeak.py to espeak.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/language_switch.py to language_switch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/mbrola.py to mbrola.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/voice.py to voice.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/words_mismatch.py to words_mismatch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/espeak/wrapper.py to wrapper.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/festival.py to festival.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/phonemizer/backend/festival/lispy.py to lispy.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak.py to test_espeak.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_lang_switch.py to test_espeak_lang_switch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_word_mismatch.py to test_espeak_word_mismatch.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_espeak_wrapper.py to test_espeak_wrapper.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_festival.py to test_festival.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_import.py to test_import.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_main.py to test_main.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_mbrola.py to test_mbrola.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_phonemize.py to test_phonemize.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_punctuation.py to test_punctuation.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_segments.py to test_segments.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_separator.py to test_separator.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/test/test_utils.py to test_utils.cpython-38.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying phonemizer.egg-info/zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
creating 'dist/phonemizer-3.0-py3.8.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing phonemizer-3.0-py3.8.egg
Removing /usr/local/lib/python3.8/dist-packages/phonemizer-3.0-py3.8.egg
Copying phonemizer-3.0-py3.8.egg to /usr/local/lib/python3.8/dist-packages
phonemizer 3.0 is already the active version in easy-install.pth
Installing phonemize script to /usr/local/bin

Installed /usr/local/lib/python3.8/dist-packages/phonemizer-3.0-py3.8.egg
Processing dependencies for phonemizer==3.0
Searching for segments==2.2.0
Best match: segments 2.2.0
Processing segments-2.2.0-py3.8.egg
segments 2.2.0 is already the active version in easy-install.pth
Installing segments script to /usr/local/bin

Using /usr/local/lib/python3.8/dist-packages/segments-2.2.0-py3.8.egg
Searching for joblib==1.1.0
Best match: joblib 1.1.0
Processing joblib-1.1.0-py3.8.egg
joblib 1.1.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/joblib-1.1.0-py3.8.egg
Searching for dlinfo==1.2.1
Best match: dlinfo 1.2.1
Processing dlinfo-1.2.1-py3.8.egg
dlinfo 1.2.1 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/dlinfo-1.2.1-py3.8.egg
Searching for attrs==21.2.0
Best match: attrs 21.2.0
Processing attrs-21.2.0-py3.8.egg
attrs 21.2.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/attrs-21.2.0-py3.8.egg
Searching for regex==2021.10.23
Best match: regex 2021.10.23
Processing regex-2021.10.23-py3.8-linux-x86_64.egg
regex 2021.10.23 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/regex-2021.10.23-py3.8-linux-x86_64.egg
Searching for csvw==1.11.0
Best match: csvw 1.11.0
Processing csvw-1.11.0-py3.8.egg
csvw 1.11.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/csvw-1.11.0-py3.8.egg
Searching for clldutils==3.10.0
Best match: clldutils 3.10.0
Processing clldutils-3.10.0-py3.8.egg
clldutils 3.10.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/clldutils-3.10.0-py3.8.egg
Searching for uritemplate==4.1.1
Best match: uritemplate 4.1.1
Processing uritemplate-4.1.1-py3.8.egg
uritemplate 4.1.1 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/uritemplate-4.1.1-py3.8.egg
Searching for rfc3986==1.5.0
Best match: rfc3986 1.5.0
Processing rfc3986-1.5.0-py3.8.egg
rfc3986 1.5.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/rfc3986-1.5.0-py3.8.egg
Searching for python-dateutil==2.8.1
Best match: python-dateutil 2.8.1
Adding python-dateutil 2.8.1 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Searching for isodate==0.6.0
Best match: isodate 0.6.0
Processing isodate-0.6.0-py3.8.egg
isodate 0.6.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/isodate-0.6.0-py3.8.egg
Searching for tabulate==0.8.9
Best match: tabulate 0.8.9
Processing tabulate-0.8.9-py3.8.egg
tabulate 0.8.9 is already the active version in easy-install.pth
Installing tabulate script to /usr/local/bin

Using /usr/local/lib/python3.8/dist-packages/tabulate-0.8.9-py3.8.egg
Searching for colorlog==6.5.0
Best match: colorlog 6.5.0
Processing colorlog-6.5.0-py3.8.egg
colorlog 6.5.0 is already the active version in easy-install.pth

Using /usr/local/lib/python3.8/dist-packages/colorlog-6.5.0-py3.8.egg
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Finished processing dependencies for phonemizer==3.0
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pytest
================================================================= test session starts ==================================================================
platform linux -- Python 3.7.6, pytest-6.2.5, py-1.10.0, pluggy-0.13.1
rootdir: /media/ye/project1/exp/phonemizer, configfile: setup.cfg, testpaths: test
plugins: remotedata-0.3.2, openfiles-0.4.0, astropy-header-0.1.2, doctestplus-0.5.0, arraydiff-0.3, hydra-core-1.0.5, hypothesis-5.5.4
collected 14 items / 10 errors / 4 selected                                                                                                            

======================================================================== ERRORS ========================================================================
_________________________________________________________ ERROR collecting test/test_espeak.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak.py:24: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
___________________________________________________ ERROR collecting test/test_espeak_lang_switch.py ___________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_lang_switch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_lang_switch.py:22: in <module>
    from phonemizer.backend import EspeakBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________ ERROR collecting test/test_espeak_word_mismatch.py __________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_word_mismatch.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_word_mismatch.py:9: in <module>
    from phonemizer import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_____________________________________________________ ERROR collecting test/test_espeak_wrapper.py _____________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_espeak_wrapper.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_espeak_wrapper.py:27: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_festival.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_festival.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_festival.py:27: in <module>
    from phonemizer.backend import FestivalBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
__________________________________________________________ ERROR collecting test/test_main.py __________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_main.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_main.py:27: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_________________________________________________________ ERROR collecting test/test_mbrola.py _________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_mbrola.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_mbrola.py:22: in <module>
    from phonemizer.backend import EspeakMbrolaBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
_______________________________________________________ ERROR collecting test/test_phonemize.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_phonemize.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_phonemize.py:22: in <module>
    from phonemizer.phonemize import phonemize
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
______________________________________________________ ERROR collecting test/test_punctuation.py _______________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_punctuation.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_punctuation.py:21: in <module>
    from phonemizer.backend import EspeakBackend, FestivalBackend, SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
________________________________________________________ ERROR collecting test/test_segments.py ________________________________________________________
ImportError while importing test module '/media/ye/project1/exp/phonemizer/test/test_segments.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
/home/ye/anaconda3/lib/python3.7/importlib/__init__.py:127: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
test/test_segments.py:24: in <module>
    from phonemizer.backend import SegmentsBackend
phonemizer/__init__.py:37: in <module>
    from .phonemize import phonemize
phonemizer/phonemize.py:26: in <module>
    from phonemizer.backend import BACKENDS
phonemizer/backend/__init__.py:19: in <module>
    from .espeak.espeak import EspeakBackend
phonemizer/backend/espeak/espeak.py:20: in <module>
    from phonemizer.backend.espeak.base import BaseEspeakBackend
phonemizer/backend/espeak/base.py:20: in <module>
    from phonemizer.backend.espeak.wrapper import EspeakWrapper
phonemizer/backend/espeak/wrapper.py:26: in <module>
    from phonemizer.backend.espeak.api import EspeakAPI
phonemizer/backend/espeak/api.py:29: in <module>
    import dlinfo
E   ModuleNotFoundError: No module named 'dlinfo'
=============================================================== short test summary info ================================================================
ERROR test/test_espeak.py
ERROR test/test_espeak_lang_switch.py
ERROR test/test_espeak_word_mismatch.py
ERROR test/test_espeak_wrapper.py
ERROR test/test_festival.py
ERROR test/test_main.py
ERROR test/test_mbrola.py
ERROR test/test_phonemize.py
ERROR test/test_punctuation.py
ERROR test/test_segments.py
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 10 errors during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
================================================================== 10 errors in 0.25s ==================================================================
(base) ye@:/media/ye/project1/exp/phonemizer$
```

Refer following:  
[https://stackoverflow.com/questions/41748464/pytest-cannot-import-module-while-python-can](https://stackoverflow.com/questions/41748464/pytest-cannot-import-module-while-python-can)  


python3 -m pytest ဆိုတဲ့ command နဲ့ run လည်း same error ပေးတယ်။  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ python3 -m pytest
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ sudo pip install ./ --upgrade
```

upgrade လုပ်လည်း မရဘူး...  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pytest --import-mode=append
```

အဆင်မပြေဘူး...  

pip install နဲ့ပဲ လုပ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pip install phonemizer
Collecting phonemizer
  Downloading phonemizer-3.0-py3-none-any.whl (87 kB)
     |████████████████████████████████| 87 kB 1.9 MB/s             
Requirement already satisfied: attrs>=18.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from phonemizer) (19.3.0)
Requirement already satisfied: joblib in /home/ye/anaconda3/lib/python3.7/site-packages (from phonemizer) (0.17.0)
Collecting segments
  Downloading segments-2.2.0-py2.py3-none-any.whl (15 kB)
Collecting dlinfo
  Downloading dlinfo-1.2.1-py3-none-any.whl (3.6 kB)
Requirement already satisfied: regex in /home/ye/anaconda3/lib/python3.7/site-packages (from segments->phonemizer) (2020.11.13)
Collecting csvw>=1.5.6
  Downloading csvw-1.11.0-py2.py3-none-any.whl (35 kB)
Collecting clldutils>=1.7.3
  Downloading clldutils-3.10.0-py2.py3-none-any.whl (195 kB)
     |████████████████████████████████| 195 kB 6.6 MB/s            
Requirement already satisfied: python-dateutil in /home/ye/anaconda3/lib/python3.7/site-packages (from clldutils>=1.7.3->segments->phonemizer) (2.8.1)
Requirement already satisfied: tabulate>=0.7.7 in /home/ye/anaconda3/lib/python3.7/site-packages (from clldutils>=1.7.3->segments->phonemizer) (0.8.7)
Collecting colorlog
  Downloading colorlog-6.5.0-py2.py3-none-any.whl (11 kB)
Collecting uritemplate>=3.0.0
  Downloading uritemplate-4.1.1-py2.py3-none-any.whl (10 kB)
Requirement already satisfied: rfc3986 in /home/ye/anaconda3/lib/python3.7/site-packages (from csvw>=1.5.6->segments->phonemizer) (1.4.0)
Collecting isodate
  Downloading isodate-0.6.0-py2.py3-none-any.whl (45 kB)
     |████████████████████████████████| 45 kB 5.6 MB/s             
Requirement already satisfied: six in /home/ye/anaconda3/lib/python3.7/site-packages (from isodate->csvw>=1.5.6->segments->phonemizer) (1.14.0)
Installing collected packages: uritemplate, isodate, csvw, colorlog, clldutils, segments, dlinfo, phonemizer
Successfully installed clldutils-3.10.0 colorlog-6.5.0 csvw-1.11.0 dlinfo-1.2.1 isodate-0.6.0 phonemizer-3.0 segments-2.2.0 uritemplate-4.1.1
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

pip နဲ့ install လုပ်ပြီး run တော့ module ပြဿနာတော့ အဆင်ပြေသွားပြီ ဒါပေမဲ့ အောက်ပါ error ရတယ်...  

```
test/test_punctuation.py:197: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/phonemize.py:238: in phonemize
    return _phonemize(phonemizer, text, separator, strip, njobs, prepend_text)
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/phonemize.py:84: in _phonemize
    text, separator=separator, strip=strip, njobs=njobs)
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/backend/base.py:166: in phonemize
    phonemized = self._phonemize_aux(text, 0, separator, strip)
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/backend/festival/festival.py:198: in _phonemize_aux
    text = self._process(text)
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/backend/festival/festival.py:248: in _process
    data.close()
/home/ye/anaconda3/lib/python3.7/tempfile.py:507: in close
    self._closer.close()
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

self = <tempfile._TemporaryFileCloser object at 0x7ff1d5dc8990>, unlink = <built-in function unlink>

    def close(self, unlink=_os.unlink):
        if not self.close_called and self.file is not None:
            self.close_called = True
            try:
>               self.file.close()
E               OSError: [Errno 28] No space left on device

/home/ye/anaconda3/lib/python3.7/tempfile.py:441: OSError
=============================================================== short test summary info ================================================================
FAILED test/test_festival.py::test_path_bad - Failed: DID NOT RAISE <class 'RuntimeError'>
FAILED test/test_festival.py::test_path_venv - OSError: [Errno 8] Exec format error: PosixPath('/media/ye/project1/exp/phonemizer/test/test_festival....
FAILED test/test_import.py::test_absolute - OSError: [Errno 28] No space left on device
FAILED test/test_main.py::test_help - OSError: [Errno 28] No space left on device
FAILED test/test_main.py::test_version - OSError: [Errno 28] No space left on device
FAILED test/test_main.py::test_list_languages - OSError: [Errno 28] No space left on device
FAILED test/test_main.py::test_readme - OSError: [Errno 28] No space left on device: '/tmp/tmpdq_fb8c4'
FAILED test/test_main.py::test_readme_festival_syll - OSError: [Errno 28] No space left on device: '/tmp/tmp1_vqwamh'
FAILED test/test_main.py::test_njobs[1] - OSError: [Errno 28] No space left on device: '/tmp/tmpp_zknpft'
FAILED test/test_main.py::test_njobs[6] - OSError: [Errno 28] No space left on device: '/tmp/tmplafixk4a'
FAILED test/test_main.py::test_unicode - OSError: [Errno 28] No space left on device: '/tmp/tmpq4destq4'
FAILED test/test_main.py::test_espeak_path - OSError: [Errno 28] No space left on device: '/tmp/tmplmjmfp8_'
FAILED test/test_main.py::test_festival_path - OSError: [Errno 28] No space left on device: '/tmp/tmp__mtzsy2'
FAILED test/test_phonemize.py::test_bad_language - OSError: [Errno 28] No space left on device: '/tmp/tmpddwkgg1c'
FAILED test/test_phonemize.py::test_text_type - OSError: [Errno 28] No space left on device
FAILED test/test_phonemize.py::test_lang_switch - OSError: [Errno 28] No space left on device: '/tmp/tmpfem71knp'
FAILED test/test_phonemize.py::test_espeak[2] - OSError: [Errno 28] No space left on device: '/tmp/tmplrt4k59n'
FAILED test/test_phonemize.py::test_espeak[4] - OSError: [Errno 28] No space left on device: '/tmp/tmpwqybfuzv'
FAILED test/test_punctuation.py::test_espeak - OSError: [Errno 28] No space left on device
FAILED test/test_punctuation.py::test_festival - OSError: [Errno 28] No space left on device
FAILED test/test_punctuation.py::test_issue_54[!'] - OSError: [Errno 28] No space left on device: '/tmp/tmptyvcp218'
FAILED test/test_punctuation.py::test_issue_54['!] - OSError: [Errno 28] No space left on device
FAILED test/test_punctuation.py::test_issue_54[!'!] - OSError: [Errno 28] No space left on device: '/tmp/tmpsyk64116'
FAILED test/test_punctuation.py::test_issue_54['!'] - OSError: [Errno 28] No space left on device: '/tmp/tmpsrum27fz'
FAILED test/test_punctuation.py::test_issue55[espeak-default-text0-expected0] - OSError: [Errno 28] No space left on device: '/tmp/tmpbukeo09b'
FAILED test/test_punctuation.py::test_issue55[espeak-.!;:,?-text1-expected1] - OSError: [Errno 28] No space left on device: '/tmp/tmpxy5m6agc'
FAILED test/test_punctuation.py::test_issue55[espeak-default-text2-expected2] - OSError: [Errno 28] No space left on device: '/tmp/tmple89a_w7'
FAILED test/test_punctuation.py::test_issue55[espeak-!-text3-expected3] - OSError: [Errno 28] No space left on device
FAILED test/test_punctuation.py::test_issue55[festival-default-text6-expected6] - OSError: [Errno 28] No space left on device
FAILED test/test_punctuation.py::test_issue55[festival-!-text7-expected7] - OSError: [Errno 28] No space left on device
ERROR test/test_segments.py::test_language - OSError: [Errno 28] No space left on device: '/tmp/pytest-of-ye'
================================================= 30 failed, 97 passed, 42 skipped, 1 error in 10.49s ==================================================
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

main HDD မှာ space မကျန်တော့ပေးတဲ့ error ပါ။  
HDD ရဲ့ space တချို့ထွက်လာအောင် ဖိုင်တွေကို ရွှေ့တာလုပ်ပြီး ပြန် run ခဲ့...  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ pytest
================================================================= test session starts ==================================================================
platform linux -- Python 3.7.6, pytest-6.2.5, py-1.10.0, pluggy-0.13.1
rootdir: /media/ye/project1/exp/phonemizer, configfile: setup.cfg, testpaths: test
plugins: remotedata-0.3.2, openfiles-0.4.0, astropy-header-0.1.2, doctestplus-0.5.0, arraydiff-0.3, hydra-core-1.0.5, hypothesis-5.5.4
collected 170 items                                                                                                                                    

test/test_espeak.py ...............                                                                                                              [  8%]
test/test_espeak_lang_switch.py ...........                                                                                                      [ 15%]
test/test_espeak_word_mismatch.py .....                                                                                                          [ 18%]
test/test_espeak_wrapper.py ....s..                                                                                                              [ 22%]
test/test_festival.py ...........FF                                                                                                              [ 30%]
test/test_import.py ..                                                                                                                           [ 31%]
test/test_main.py .........s..                                                                                                                   [ 38%]
test/test_mbrola.py ssssssssssssssssssssssssssssssssssssss.                                                                                      [ 61%]
test/test_phonemize.py ......ss.....                                                                                                             [ 68%]
test/test_punctuation.py .................................                                                                                       [ 88%]
test/test_segments.py ........                                                                                                                   [ 92%]
test/test_separator.py ........                                                                                                                  [ 97%]
test/test_utils.py ....                                                                                                                          [100%]

======================================================================= FAILURES =======================================================================
____________________________________________________________________ test_path_bad _____________________________________________________________________

    @pytest.mark.skipif(
        'PHONEMIZER_FESTIVAL_EXECUTABLE' in os.environ,
        reason='environment variable precedence')
    def test_path_bad():
        try:
            # corrupt the default espeak path, try to use python executable instead
            binary = shutil.which('python')
            FestivalBackend.set_executable(binary)
    
            with pytest.raises(RuntimeError):
                FestivalBackend('en-us').phonemize(['hello'])
            with pytest.raises(RuntimeError):
                FestivalBackend.version()
    
            with pytest.raises(RuntimeError):
>               FestivalBackend.set_executable(__file__)
E               Failed: DID NOT RAISE <class 'RuntimeError'>

test/test_festival.py:93: Failed
____________________________________________________________________ test_path_venv ____________________________________________________________________

    @pytest.mark.skipif(
        'PHONEMIZER_FESTIVAL_EXECUTABLE' in os.environ,
        reason='cannot modify environment')
    def test_path_venv():
        try:
            os.environ['PHONEMIZER_FESTIVAL_EXECUTABLE'] = shutil.which('python')
            with pytest.raises(RuntimeError):
                FestivalBackend('en-us').phonemize(['hello'])
            with pytest.raises(RuntimeError):
                FestivalBackend.version()
    
            os.environ['PHONEMIZER_FESTIVAL_EXECUTABLE'] = __file__
            with pytest.raises(RuntimeError):
>               FestivalBackend.version()

test/test_festival.py:113: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/backend/festival/festival.py:156: in version
    [festival, '--version']).decode('latin1').strip()
/home/ye/anaconda3/lib/python3.7/subprocess.py:411: in check_output
    **kwargs).stdout
/home/ye/anaconda3/lib/python3.7/subprocess.py:488: in run
    with Popen(*popenargs, **kwargs) as process:
/home/ye/anaconda3/lib/python3.7/subprocess.py:800: in __init__
    restore_signals, start_new_session)
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

self = <subprocess.Popen object at 0x7fc7784e8f10>, args = [PosixPath('/media/ye/project1/exp/phonemizer/test/test_festival.py'), '--version']
executable = b'/media/ye/project1/exp/phonemizer/test/test_festival.py', preexec_fn = None, close_fds = True, pass_fds = (), cwd = None, env = None
startupinfo = None, creationflags = 0, shell = False, p2cread = -1, p2cwrite = -1, c2pread = 22, c2pwrite = 23, errread = -1, errwrite = -1
restore_signals = True, start_new_session = False

    def _execute_child(self, args, executable, preexec_fn, close_fds,
                       pass_fds, cwd, env,
                       startupinfo, creationflags, shell,
                       p2cread, p2cwrite,
                       c2pread, c2pwrite,
                       errread, errwrite,
                       restore_signals, start_new_session):
        """Execute program (POSIX version)"""
    
        if isinstance(args, (str, bytes)):
            args = [args]
        else:
            args = list(args)
    
        if shell:
            # On Android the default shell is at '/system/bin/sh'.
            unix_shell = ('/system/bin/sh' if
                      hasattr(sys, 'getandroidapilevel') else '/bin/sh')
            args = [unix_shell, "-c"] + args
            if executable:
                args[0] = executable
    
        if executable is None:
            executable = args[0]
        orig_executable = executable
    
        # For transferring possible exec failure from child to parent.
        # Data format: "exception name:hex errno:description"
        # Pickle is not used; it is complex and involves memory allocation.
        errpipe_read, errpipe_write = os.pipe()
        # errpipe_write must not be in the standard io 0, 1, or 2 fd range.
        low_fds_to_close = []
        while errpipe_write < 3:
            low_fds_to_close.append(errpipe_write)
            errpipe_write = os.dup(errpipe_write)
        for low_fd in low_fds_to_close:
            os.close(low_fd)
        try:
            try:
                # We must avoid complex work that could involve
                # malloc or free in the child process to avoid
                # potential deadlocks, thus we do all this here.
                # and pass it to fork_exec()
    
                if env is not None:
                    env_list = []
                    for k, v in env.items():
                        k = os.fsencode(k)
                        if b'=' in k:
                            raise ValueError("illegal environment variable name")
                        env_list.append(k + b'=' + os.fsencode(v))
                else:
                    env_list = None  # Use execv instead of execve.
                executable = os.fsencode(executable)
                if os.path.dirname(executable):
                    executable_list = (executable,)
                else:
                    # This matches the behavior of os._execvpe().
                    executable_list = tuple(
                        os.path.join(os.fsencode(dir), executable)
                        for dir in os.get_exec_path(env))
                fds_to_keep = set(pass_fds)
                fds_to_keep.add(errpipe_write)
                self.pid = _posixsubprocess.fork_exec(
                        args, executable_list,
                        close_fds, tuple(sorted(map(int, fds_to_keep))),
                        cwd, env_list,
                        p2cread, p2cwrite, c2pread, c2pwrite,
                        errread, errwrite,
                        errpipe_read, errpipe_write,
                        restore_signals, start_new_session, preexec_fn)
                self._child_created = True
            finally:
                # be sure the FD is closed no matter what
                os.close(errpipe_write)
    
            # self._devnull is not always defined.
            devnull_fd = getattr(self, '_devnull', None)
            if p2cread != -1 and p2cwrite != -1 and p2cread != devnull_fd:
                os.close(p2cread)
            if c2pwrite != -1 and c2pread != -1 and c2pwrite != devnull_fd:
                os.close(c2pwrite)
            if errwrite != -1 and errread != -1 and errwrite != devnull_fd:
                os.close(errwrite)
            if devnull_fd is not None:
                os.close(devnull_fd)
            # Prevent a double close of these fds from __init__ on error.
            self._closed_child_pipe_fds = True
    
            # Wait for exec to fail or succeed; possibly raising an
            # exception (limited in size)
            errpipe_data = bytearray()
            while True:
                part = os.read(errpipe_read, 50000)
                errpipe_data += part
                if not part or len(errpipe_data) > 50000:
                    break
        finally:
            # be sure the FD is closed no matter what
            os.close(errpipe_read)
    
        if errpipe_data:
            try:
                pid, sts = os.waitpid(self.pid, 0)
                if pid == self.pid:
                    self._handle_exitstatus(sts)
                else:
                    self.returncode = sys.maxsize
            except ChildProcessError:
                pass
    
            try:
                exception_name, hex_errno, err_msg = (
                        errpipe_data.split(b':', 2))
                # The encoding here should match the encoding
                # written in by the subprocess implementations
                # like _posixsubprocess
                err_msg = err_msg.decode()
            except ValueError:
                exception_name = b'SubprocessError'
                hex_errno = b'0'
                err_msg = 'Bad exception data from child: {!r}'.format(
                              bytes(errpipe_data))
            child_exception_type = getattr(
                    builtins, exception_name.decode('ascii'),
                    SubprocessError)
            if issubclass(child_exception_type, OSError) and hex_errno:
                errno_num = int(hex_errno, 16)
                child_exec_never_called = (err_msg == "noexec")
                if child_exec_never_called:
                    err_msg = ""
                    # The error must be from chdir(cwd).
                    err_filename = cwd
                else:
                    err_filename = orig_executable
                if errno_num != 0:
                    err_msg = os.strerror(errno_num)
                    if errno_num == errno.ENOENT:
                        err_msg += ': ' + repr(err_filename)
>               raise child_exception_type(errno_num, err_msg, err_filename)
E               OSError: [Errno 8] Exec format error: PosixPath('/media/ye/project1/exp/phonemizer/test/test_festival.py')

/home/ye/anaconda3/lib/python3.7/subprocess.py:1551: OSError
=============================================================== short test summary info ================================================================
FAILED test/test_festival.py::test_path_bad - Failed: DID NOT RAISE <class 'RuntimeError'>
FAILED test/test_festival.py::test_path_venv - OSError: [Errno 8] Exec format error: PosixPath('/media/ye/project1/exp/phonemizer/test/test_festival....
====================================================== 2 failed, 126 passed, 42 skipped in 12.63s ======================================================
(base) ye@:/media/ye/project1/exp/phonemizer$
```

အထက်ပါအတိုင်း ERROR ပေးနေသေးတယ်...  
test အားလုံးက အဆင်မပြေလည်း အဓိက ကျတဲ့ အလုပ်တချို့လုပ်လို့ ရလား confirm လုပ်ချင်တယ်...  

```
base) ye@:/media/ye/project1/exp/phonemizer$ phonemize --help
usage: phonemize [-h] [-V] [-v | -q] [-j <int>] [-o <file>]
                 [--prepend-text [<str>]] [-b <str>] [-L] [-l <str|file>]
                 [-p <str>] [-w <str>] [-s <str>] [--strip]
                 [--espeak-library <library>] [--tie [<chr>]] [--with-stress]
                 [--language-switch {keep-flags,remove-flags,remove-utterance}]
                 [--words-mismatch {ignore,warn,remove}]
                 [--festival-executable <executable>] [--preserve-punctuation]
                 [--punctuation-marks <str>]
                 [<file>]

Multilingual text to phonemes converter

The 'phonemize' program allows simple phonemization of words and texts
in many language using four backends: espeak, espeak-mbrola, festival
and segments.

- espeak is a text-to-speech software supporting multiple languages
  and IPA (International Phonetic Alphabet) output. See
  http://espeak.sourceforge.net or
  https://github.com/espeak-ng/espeak-ng

- espeak-mbrola uses the SAMPA phonetic alphabet, it requires mbrola to be
  installed as well as additional mbrola voices. It does not support word or
  syllable tokenization. See
  https://github.com/espeak-ng/espeak-ng/blob/master/docs/mbrola.md

- festival is also a text-to-speech software. Currently only American
  English is supported and festival uses a custom phoneset
  (http://www.festvox.org/bsv/c4711.html), but festival is the only
  backend supporting tokenization at the syllable
  level. See http://www.cstr.ed.ac.uk/projects/festival

- segments is a Unicode tokenizer that build a phonemization from a
  grapheme to phoneme mapping provided as a file by the user. See
  https://github.com/cldf/segments.

See the '--list-languages' option below for details on the languages
supported by each backend.

optional arguments:
  -h, --help            show this help message and exit
  -V, --version         show version information and exit.
  -v, --verbose         write all log messages to stderr (displays only
                        warnings by default).
  -q, --quiet           do not display any log message, even warnings.
  -j <int>, --njobs <int>
                        number of parallel jobs, default is 1.

input/output:
  <file>                input text file to phonemize, if not specified read
                        from stdin.
  -o <file>, --output <file>
                        output text file to write, if not specified write to
                        stdout.
  --prepend-text [<str>]
                        prepend each line of the phonemized output text with
                        its matching input text. If a string is specified as
                        option value, use it as field separator, else use one
                        of "|", "||", "|||", "||||" by selecting the first one
                        that is not configured as a token separator (see
                        -p/-s/-w options).

backends:
  -b <str>, --backend <str>
                        the phonemization backend, must be 'espeak', 'espeak-
                        mbrola', 'festival' or 'segments'. Default is
                        'espeak'.
  -L, --list-languages  list available languages (and exit) for the specified
                        backend, or for all backends if none selected.

language:
  -l <str|file>, --language <str|file>
                        the language code of the input text, use '--list-
                        languages' for a list of supported languages. Default
                        is en-us.

token separators:
  -p <str>, --phone-separator <str>
                        phone separator, default is "".
  -w <str>, --word-separator <str>
                        word separator, not valid for espeak-mbrola backend,
                        default is " ".
  -s <str>, --syllable-separator <str>
                        syllable separator, only valid for festival backend,
                        this option has no effect if another backend is used.
                        Default is "".
  --strip               removes the end separators in phonemized tokens.

specific to espeak backend:
  --espeak-library <library>
                        the path to the espeak shared library to use (*.so on
                        Linux, *.dylib on Mac and *.dll on Windows, useful to
                        overload the default espeak version installed on the
                        system). Default to libespeak-ng.so.1. This path can
                        also be specified using the PHONEMIZER_ESPEAK_LIBRARY
                        environment variable.
  --tie [<chr>]         when the option is set, use a tie character within
                        multi-letter phoneme names, default to U+361 (as in
                        d͡ʒ), 'z' means ZWJ character, only compatible with
                        espeak>1.48 and incompatible with the -p/--phone-
                        separator option
  --with-stress         when the option is set, the stresses on phonemes are
                        present (stresses characters are ˈ'ˌ). By default
                        stresses are removed.
  --language-switch {keep-flags,remove-flags,remove-utterance}
                        espeak can pronounce some words in another language
                        (typically English) when phonemizing a text. This
                        option setups the policy to use when such a language
                        switch occurs. Three values are available: 'keep-
                        flags' (the default), 'remove-flags' or 'remove-
                        utterance'. The 'keep-flags' policy keeps the language
                        switching flags, for example (en) or (jp), in the
                        output. The 'remove-flags' policy removes them and the
                        'remove-utterance' policy removes the whole line of
                        text including a language switch.
  --words-mismatch {ignore,warn,remove}
                        espeak can join two consecutive words or drop some
                        words, yielding a word count mismatch between
                        orthographic and phonemized text. This option setups
                        the policy to use when such a words count mismatch
                        occurs. Three values are available: 'ignore' (the
                        default) which do nothing, 'warn' which issue a
                        warning for each mismatched line, and 'remove' which
                        remove the mismatched lines from the output.

specific to festival backend:
  --festival-executable <executable>
                        the path to the festival executable to use (useful to
                        overload the default festival installed on the
                        system). Default to /usr/bin/festival. This path can
                        also be specified using the
                        PHONEMIZER_FESTIVAL_EXCUTABLE environment variable.

punctuation processing:
  not available for espeak-mbrola backend

  --preserve-punctuation
                        preserve the punctuation marks in the phonemized
                        output, default is to remove them.
  --punctuation-marks <str>
                        the marks to consider during punctuation processing
                        (either for removal or preservation). Default is
                        ;:,.!?¡¿—…"«»“”.

Exemples:

* Phonemize a US English text with espeak

   $ echo 'hello world' | phonemize -l en-us -b espeak
   həloʊ wɜːld

* Phonemize a US English text with festival

   $ echo 'hello world' | phonemize -l en-us -b festival
   hhaxlow werld

* Phonemize a Japanese text with segments

  $ echo 'konnichiwa tsekai' | phonemize -l japanese -b segments
  konnitʃiwa t͡sekai

* Add a separator between phones

  $ echo 'hello world' | phonemize -l en-us -b festival -p '-' --strip
  hh-ax-l-ow w-er-l-d

* Phonemize some French text file using espeak

  $ phonemize -l fr-fr -b espeak text.txt -o phones.txt
```
 
 "--version" ကို ခေါ်ကြည့်ရအောင်..  
 
```
(base) ye@:/media/ye/project1/exp/phonemizer$ phonemize --version
phonemizer-3.0
available backends: espeak-ng-1.51, espeak-mbrola, festival-2.5.0, segments-2.2.0
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

testing...  

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize
həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize --prepend-text
hello world | həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize --prepend-text=';'
hello world ; həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" > hello.txt
(base) ye@:/media/ye/project1/exp/phonemizer$ phonemize hello.txt
həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ phonemize hello.txt -o hello.phon --strip
(base) ye@:/media/ye/project1/exp/phonemizer$ cat ./hello.phon
həloʊ wɜːld
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize
həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -l en-us -b espeak
həloʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo 'hello world' | phonemize -l en-us -b espeak --tie
həlo͡ʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```


```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -l en-us -b festival
hhaxlow werld 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "bonjour le monde" | phonemize -b espeak -l fr-fr -p ' ' -w '/w '
[WARNING] words count mismatch on 100.0% of the lines (1/1)
b ɔ̃ ʒ u ʁ /w l ə /w m ɔ̃ d /w 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "bonjour le monde" | phonemize -b espeak-mbrola -l mb-fr1 -p ' ' -w '/w '
fatal error: language "mb-fr1" is not supported by the espeak-mbrola backend
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo 'konnichiwa' | phonemize -b segments -l japanese
konnitʃiwa 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo 'konnichiwa' | phonemize -b segments -l ./phonemizer/share/japanese.g2p

fatal error: grapheme to phoneme file not found: ./phonemizer/share/japanese.g2p
(base) ye@:/media/ye/project1/exp/phonemizer$   konnitʃiwa
konnitʃiwa: command not found
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ phonemize --list-languages
supported languages for espeak are:
	af	->	Afrikaans
	am	->	Amharic
	an	->	Aragonese
	ar	->	Arabic
	as	->	Assamese
	az	->	Azerbaijani
	ba	->	Bashkir
	bg	->	Bulgarian
	bn	->	Bengali
	bpy	->	Bishnupriya Manipuri
	bs	->	Bosnian
	ca	->	Catalan
	chr-US-Qaaa-x-west	->	Cherokee 
	cmn	->	Chinese (Mandarin)
	cs	->	Czech
	cv	->	Chuvash
	cy	->	Welsh
	da	->	Danish
	de	->	German
	el	->	Greek
	en-029	->	English (Caribbean)
	en-gb	->	English (Great Britain)
	en-gb-scotland	->	English (Scotland)
	en-gb-x-gbclan	->	English (Lancaster)
	en-gb-x-gbcwmd	->	English (West Midlands)
	en-gb-x-rp	->	English (Received Pronunciation)
	en-us	->	English (America)
	eo	->	Esperanto
	es	->	Spanish (Spain)
	es-419	->	Spanish (Latin America)
	et	->	Estonian
	eu	->	Basque
	fa	->	Persian
	fa-latn	->	Persian (Pinglish)
	fi	->	Finnish
	fr-be	->	French (Belgium)
	fr-ch	->	French (Switzerland)
	fr-fr	->	French (France)
	ga	->	Gaelic (Irish)
	gd	->	Gaelic (Scottish)
	gn	->	Guarani
	grc	->	Greek (Ancient)
	gu	->	Gujarati
	hak	->	Hakka Chinese
	haw	->	Hawaiian
	he	->	Hebrew
	hi	->	Hindi
	hr	->	Croatian
	ht	->	Haitian Creole
	hu	->	Hungarian
	hy	->	Armenian (East Armenia)
	hyw	->	Armenian (West Armenia)
	ia	->	Interlingua
	id	->	Indonesian
	io	->	ido
	is	->	Icelandic
	it	->	Italian
	ja	->	Japanese
	jbo	->	Lojban
	ka	->	Georgian
	kk	->	Kazakh
	kl	->	Greenlandic
	kn	->	Kannada
	ko	->	Korean
	kok	->	Konkani
	ku	->	Kurdish
	ky	->	Kyrgyz
	la	->	Latin
	lfn	->	Lingua Franca Nova
	lt	->	Lithuanian
	ltg	->	Latgalian
	lv	->	Latvian
	mi	->	Māori
	mk	->	Macedonian
	ml	->	Malayalam
	mr	->	Marathi
	ms	->	Malay
	mt	->	Maltese
	my	->	Myanmar (Burmese)
	nb	->	Norwegian Bokmål
	nci	->	Nahuatl (Classical)
	ne	->	Nepali
	nl	->	Dutch
	nog	->	Nogai
	om	->	Oromo
	or	->	Oriya
	pa	->	Punjabi
	pap	->	Papiamento
	piqd	->	Klingon
	pl	->	Polish
	pt	->	Portuguese (Portugal)
	pt-br	->	Portuguese (Brazil)
	py	->	Pyash
	qdb	->	Lang Belta
	qu	->	Quechua
	quc	->	K'iche'
	ro	->	Romanian
	ru	->	Russian
	ru-lv	->	Russian (Latvia)
	sd	->	Sindhi
	shn	->	Shan (Tai Yai)
	si	->	Sinhala
	sk	->	Slovak
	sl	->	Slovenian
	sq	->	Albanian
	sr	->	Serbian
	sv	->	Swedish
	sw	->	Swahili
	ta	->	Tamil
	te	->	Telugu
	th	->	Thai
	tk	->	Turkmen
	tn	->	Setswana
	tr	->	Turkish
	tt	->	Tatar
	ug	->	Uyghur
	uk	->	Ukrainian
	ur	->	Urdu
	uz	->	Uzbek
	vi	->	Vietnamese (Northern)
	vi-vn-x-central	->	Vietnamese (Central)
	vi-vn-x-south	->	Vietnamese (Southern)
	yue	->	Chinese (Cantonese)
supported languages for festival are:
	en-us	->	english-us
supported languages for segments are:
	chintang	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/chintang.g2p
	cree	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/cree.g2p
	inuktitut	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/inuktitut.g2p
	japanese	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/japanese.g2p
	sesotho	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/sesotho.g2p
	yucatec	->	/home/ye/anaconda3/lib/python3.7/site-packages/phonemizer/share/segments/yucatec.g2p
supported languages for espeak-mbrola are:

None
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -w ' ' -p ''
hhaxlow werld 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -p ' ' -w ''
hh ax l ow w er l d 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -p '-' -s '|'
hh-ax-|l-ow-| w-er-l-d-| 
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -p '-' -s '|' --strip
hh-ax|l-ow w-er-l-d
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -p ' ' -s ';esyll ' -w ';eword '
hh ax ;esyll l ow ;esyll ;eword w er l d ;esyll ;eword 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -b festival -p ' ' -w ' '
fatal error: illegal separator with word=" ", syllable="" and phone=" ", must be all differents if not empty
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello, world!" | phonemize --strip
həloʊ wɜːld
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello, world!" | phonemize --preserve-punctuation --strip
həloʊ, wɜːld!
(base) ye@:/media/ye/project1/exp/phonemizer$ 
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -l en-us -b espeak --with-stress
həlˈoʊ wˈɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "hello world" | phonemize -l en-us -b espeak --tie
həlo͡ʊ wɜːld 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "j'aime le football" | phonemize -l fr-fr -b espeak --language-switch keep-flags
[WARNING] 1 utterances containing language switches on lines 1
[WARNING] extra phones may appear in the "fr-fr" phoneset
[WARNING] language switch flags have been kept (applying "keep-flags" policy)
ʒɛm lə (en)fʊtbɔːl(fr) 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "j'aime le football" | phonemize -l fr-fr -b espeak --language-switch remove-flags
[WARNING] 1 utterances containing language switches on lines 1
[WARNING] extra phones may appear in the "fr-fr" phoneset
[WARNING] language switch flags have been removed (applying "remove-flags" policy)
ʒɛm lə fʊtbɔːl 
(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "j'aime le football" | phonemize -l fr-fr -b espeak --language-switch remove-utterance
[WARNING] removed 1 utterances containing language switches (applying "remove-utterance" policy)
[WARNING] words count mismatch on 100.0% of the lines (1/1)

(base) ye@:/media/ye/project1/exp/phonemizer$
```

```
(base) ye@:/media/ye/project1/exp/phonemizer$ echo "that's it, words are merged" | phonemize -l en-us -b espeak
[WARNING] words count mismatch on 100.0% of the lines (1/1)
ðætsɪt wɜːdz ɑːɹ mɜːdʒd 
(base) ye@:/media/ye/project1/exp/phonemizer$
```


