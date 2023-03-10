
## PySFedit and PSFEditor Testing

## git clone for PySFedit

```
(base) ye@ykt-pro:~/tool/scalable-font$ git clone https://gitlab.com/kalehmann/pysfedit.git
Cloning into 'pysfedit'...
remote: Enumerating objects: 1026, done.
remote: Counting objects: 100% (1026/1026), done.
remote: Compressing objects: 100% (369/369), done.
remote: Total 1026 (delta 634), reused 1011 (delta 630), pack-reused 0
Receiving objects: 100% (1026/1026), 302.87 KiB | 1.58 MiB/s, done.
Resolving deltas: 100% (634/634), done.
(base) ye@ykt-pro:~/tool/scalable-font$ 
```

## Installation

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ python3 ./setup.py install
Traceback (most recent call last):
  File "./setup.py", line 26, in <module>
    'pysfedit=pysfedit:main'
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/__init__.py", line 145, in setup
    return distutils.core.setup(**attrs)
  File "/home/ye/tool/anaconda3/lib/python3.7/distutils/core.py", line 121, in setup
    dist.parse_config_files()
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/dist.py", line 701, in parse_config_files
    ignore_option_errors=ignore_option_errors)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 121, in parse_configuration
    meta.parse()
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 426, in parse
    section_parser_method(section_options)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 399, in parse_section
    self[name] = value
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 184, in __setitem__
    value = parser(value)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 514, in _parse_version
    version = self._parse_attr(value, self.package_dir)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/setuptools/config.py", line 349, in _parse_attr
    module = import_module(module_name)
  File "/home/ye/tool/anaconda3/lib/python3.7/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1006, in _gcd_import
  File "<frozen importlib._bootstrap>", line 983, in _find_and_load
  File "<frozen importlib._bootstrap>", line 967, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 677, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 728, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "/home/ye/tool/scalable-font/pysfedit/pysfedit/__init__.py", line 27, in <module>
    import gi
ModuleNotFoundError: No module named 'gi'
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ 
```

pip နဲ့ install လုပ်ကြည့်တာက အဆင်မပြေလို့ os package ကိုပဲ apt နဲ့ install လုပ်ခဲ့ ...  

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ sudo apt install python3-gi
Reading package lists... Done
Building dependency tree       
Reading state information... Done
python3-gi is already the newest version (3.26.1-2ubuntu1).
python3-gi set to manually installed.
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122 linux-hwe-5.4-headers-5.4.0-124
  linux-hwe-5.4-headers-5.4.0-125 linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132 linux-hwe-5.4-headers-5.4.0-135
  linux-hwe-5.4-headers-5.4.0-136 linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 146 not upgraded.
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$
```

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ which -a python3
/home/ye/tool/anaconda3/bin/python3
/usr/bin/python3
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ 
```

for running:  

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit/bin$ /usr/bin/python3 ./pysfedit
```

psf font copying ...  

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit/bin/font$ cp /media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv/Thai-Fixed16.psf .
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit/bin/font$ 
```

```
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$ sudo /usr/bin/python3 ./setup.py install
running install
running bdist_egg
running egg_info
creating PySFedit.egg-info
writing PySFedit.egg-info/PKG-INFO
writing dependency_links to PySFedit.egg-info/dependency_links.txt
writing entry points to PySFedit.egg-info/entry_points.txt
writing requirements to PySFedit.egg-info/requires.txt
writing top-level names to PySFedit.egg-info/top_level.txt
writing manifest file 'PySFedit.egg-info/SOURCES.txt'
reading manifest file 'PySFedit.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
writing manifest file 'PySFedit.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/pysfedit
copying pysfedit/__init__.py -> build/lib/pysfedit
copying pysfedit/edit_description_dialog.py -> build/lib/pysfedit
copying pysfedit/font_editor.py -> build/lib/pysfedit
copying pysfedit/constants.py -> build/lib/pysfedit
copying pysfedit/preferences_window.py -> build/lib/pysfedit
copying pysfedit/glyph_editor.py -> build/lib/pysfedit
creating build/lib/pysfedit/psflib
copying pysfedit/psflib/__init__.py -> build/lib/pysfedit/psflib
copying pysfedit/psflib/byteutils.py -> build/lib/pysfedit/psflib
copying pysfedit/psflib/asmutils.py -> build/lib/pysfedit/psflib
creating build/lib/pysfedit/res
creating build/lib/pysfedit/res/img
copying pysfedit/res/img/icon.png -> build/lib/pysfedit/res/img
creating build/lib/pysfedit/res/locale
creating build/lib/pysfedit/res/locale/de_DE
creating build/lib/pysfedit/res/locale/de_DE/LC_MESSAGES
copying pysfedit/res/locale/de_DE/LC_MESSAGES/pysfedit.mo -> build/lib/pysfedit/res/locale/de_DE/LC_MESSAGES
copying pysfedit/res/locale/de_DE/LC_MESSAGES/pysfedit.po -> build/lib/pysfedit/res/locale/de_DE/LC_MESSAGES
creating build/lib/pysfedit/res/txt
copying pysfedit/res/txt/gpl-3.0.txt -> build/lib/pysfedit/res/txt
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/pysfedit
copying build/lib/pysfedit/__init__.py -> build/bdist.linux-x86_64/egg/pysfedit
copying build/lib/pysfedit/edit_description_dialog.py -> build/bdist.linux-x86_64/egg/pysfedit
creating build/bdist.linux-x86_64/egg/pysfedit/res
creating build/bdist.linux-x86_64/egg/pysfedit/res/txt
copying build/lib/pysfedit/res/txt/gpl-3.0.txt -> build/bdist.linux-x86_64/egg/pysfedit/res/txt
creating build/bdist.linux-x86_64/egg/pysfedit/res/locale
creating build/bdist.linux-x86_64/egg/pysfedit/res/locale/de_DE
creating build/bdist.linux-x86_64/egg/pysfedit/res/locale/de_DE/LC_MESSAGES
copying build/lib/pysfedit/res/locale/de_DE/LC_MESSAGES/pysfedit.po -> build/bdist.linux-x86_64/egg/pysfedit/res/locale/de_DE/LC_MESSAGES
copying build/lib/pysfedit/res/locale/de_DE/LC_MESSAGES/pysfedit.mo -> build/bdist.linux-x86_64/egg/pysfedit/res/locale/de_DE/LC_MESSAGES
creating build/bdist.linux-x86_64/egg/pysfedit/res/img
copying build/lib/pysfedit/res/img/icon.png -> build/bdist.linux-x86_64/egg/pysfedit/res/img
copying build/lib/pysfedit/font_editor.py -> build/bdist.linux-x86_64/egg/pysfedit
copying build/lib/pysfedit/constants.py -> build/bdist.linux-x86_64/egg/pysfedit
creating build/bdist.linux-x86_64/egg/pysfedit/psflib
copying build/lib/pysfedit/psflib/__init__.py -> build/bdist.linux-x86_64/egg/pysfedit/psflib
copying build/lib/pysfedit/psflib/byteutils.py -> build/bdist.linux-x86_64/egg/pysfedit/psflib
copying build/lib/pysfedit/psflib/asmutils.py -> build/bdist.linux-x86_64/egg/pysfedit/psflib
copying build/lib/pysfedit/preferences_window.py -> build/bdist.linux-x86_64/egg/pysfedit
copying build/lib/pysfedit/glyph_editor.py -> build/bdist.linux-x86_64/egg/pysfedit
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/edit_description_dialog.py to edit_description_dialog.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/font_editor.py to font_editor.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/constants.py to constants.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/psflib/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/psflib/byteutils.py to byteutils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/psflib/asmutils.py to asmutils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/preferences_window.py to preferences_window.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/pysfedit/glyph_editor.py to glyph_editor.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying PySFedit.egg-info/zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
creating dist
creating 'dist/PySFedit-1.0.0-py3.6.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing PySFedit-1.0.0-py3.6.egg
Copying PySFedit-1.0.0-py3.6.egg to /usr/local/lib/python3.6/dist-packages
Adding PySFedit 1.0.0 to easy-install.pth file
Installing pysfedit script to /usr/local/bin

Installed /usr/local/lib/python3.6/dist-packages/PySFedit-1.0.0-py3.6.egg
Processing dependencies for PySFedit==1.0.0
Searching for pygobject==3.26.1
Best match: pygobject 3.26.1
Adding pygobject 3.26.1 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Searching for pycairo==1.16.2
Best match: pycairo 1.16.2
Adding pycairo 1.16.2 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Searching for Pillow==5.1.0
Best match: Pillow 5.1.0
Adding Pillow 5.1.0 to easy-install.pth file

Using /usr/lib/python3/dist-packages
Finished processing dependencies for PySFedit==1.0.0
(base) ye@ykt-pro:~/tool/scalable-font/pysfedit$
```

ထိုင်းဖောင့်နဲ့ စမ်းဖွင့်ကြည့်တော့ အောက်ပါအတိုင်း UI ကို တွေ့ရ ...  

![UI of PySFedit](https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/psf2bmp/pysfedit-screen1.png "PySFedit Editor UI")

## PSFEditor

နောက်ထပ် psf font editor ကိုလည်း စမ်းခဲ့ ...  

```
(base) ye@ykt-pro:~/tool$ git clone https://github.com/ideras/PSFEditor
Cloning into 'PSFEditor'...
remote: Enumerating objects: 79, done.
remote: Total 79 (delta 0), reused 0 (delta 0), pack-reused 79
Unpacking objects: 100% (79/79), done.
(base) ye@ykt-pro:~/tool$ cd PSFEditor/
(base) ye@ykt-pro:~/tool/PSFEditor$ 
```

အရင်ဆုံး qmake ကို run ပြီးမှ make ကို run ...  

```
../anaconda3/include/qt/QtWidgets/qstyleoption.h:510:5: note: because ‘QStyleOptionComplex’ has user-provided ‘QStyleOptionComplex::QStyleOptionComplex(const QStyleOptionComplex&)’
  510 |     QStyleOptionComplex(const QStyleOptionComplex &other) : QStyleOption(Version, Type) { *this = other; }
      |     ^~~~~~~~~~~~~~~~~~~
../anaconda3/include/qt/QtWidgets/qstyleoption.h: In copy constructor ‘QStyleOptionSizeGrip::QStyleOptionSizeGrip(const QStyleOptionSizeGrip&)’:
../anaconda3/include/qt/QtWidgets/qstyleoption.h:654:108: note: synthesized method ‘QStyleOptionSizeGrip& QStyleOptionSizeGrip::operator=(const QStyleOptionSizeGrip&)’ first required here
  654 |     QStyleOptionSizeGrip(const QStyleOptionSizeGrip &other) : QStyleOptionComplex(Version, Type) { *this = other; }
      |                                                                                                            ^~~~~
../anaconda3/include/qt/QtWidgets/qstyleoption.h: In copy constructor ‘QStyleOptionGraphicsItem::QStyleOptionGraphicsItem(const QStyleOptionGraphicsItem&)’:
../anaconda3/include/qt/QtWidgets/qstyleoption.h:670:109: warning: implicitly-declared ‘QStyleOptionGraphicsItem& QStyleOptionGraphicsItem::operator=(const QStyleOptionGraphicsItem&)’ is deprecated [-Wdeprecated-copy]
  670 |     QStyleOptionGraphicsItem(const QStyleOptionGraphicsItem &other) : QStyleOption(Version, Type) { *this = other; }
      |                                                                                                             ^~~~~
../anaconda3/include/qt/QtWidgets/qstyleoption.h:670:5: note: because ‘QStyleOptionGraphicsItem’ has user-provided ‘QStyleOptionGraphicsItem::QStyleOptionGraphicsItem(const QStyleOptionGraphicsItem&)’
  670 |     QStyleOptionGraphicsItem(const QStyleOptionGraphicsItem &other) : QStyleOption(Version, Type) { *this = other; }
      |     ^~~~~~~~~~~~~~~~~~~~~~~~
/home/ye/tool/anaconda3/bin/moc -DQT_DEPRECATED_WARNINGS -DQT_NO_STYLE_GTK -DQT_NO_DEBUG -DQT_WIDGETS_LIB -DQT_GUI_LIB -DQT_CORE_LIB --include ./moc_predefs.h -I/home/ye/tool/anaconda3/mkspecs/linux-g++ -I/home/ye/tool/PSFEditor -I/home/ye/tool/PSFEditor/include -I/home/ye/tool/anaconda3/include/qt -I/home/ye/tool/anaconda3/include/qt/QtWidgets -I/home/ye/tool/anaconda3/include/qt/QtGui -I/home/ye/tool/anaconda3/include/qt/QtCore -I/usr/include/c++/9 -I/usr/include/x86_64-linux-gnu/c++/9 -I/usr/include/c++/9/backward -I/usr/lib/gcc/x86_64-linux-gnu/9/include -I/usr/local/include -I/usr/include/x86_64-linux-gnu -I/usr/include include/dlgsymbinfo.h -o moc_dlgsymbinfo.cpp
g++ -c -pipe -O2 -Wall -W -D_REENTRANT -fPIC -DQT_DEPRECATED_WARNINGS -DQT_NO_STYLE_GTK -DQT_NO_DEBUG -DQT_WIDGETS_LIB -DQT_GUI_LIB -DQT_CORE_LIB -I. -Iinclude -I../anaconda3/include/qt -I../anaconda3/include/qt/QtWidgets -I../anaconda3/include/qt/QtGui -I../anaconda3/include/qt/QtCore -I. -I. -I../anaconda3/mkspecs/linux-g++ -o moc_dlgsymbinfo.o moc_dlgsymbinfo.cpp
g++ -Wl,-O1 -Wl,-rpath,/home/ye/tool/anaconda3/lib -o PSFEditor main.o mainwindow.o qfontglypheditor.o qglyphlistwidgetitemdelegate.o psfutil.o psf.o dlgsymbinfo.o qrc_psfeditor.o moc_mainwindow.o moc_qfontglypheditor.o moc_qglyphlistwidgetitemdelegate.o moc_dlgsymbinfo.o   -L/home/ye/tool/anaconda3/lib -lQt5Widgets -lQt5Gui -lQt5Core -lGL -lpthread 
(base) ye@ykt-pro:~/tool/PSFEditor$
```

အဆင်ပြေပြေနဲ့ compile လုပ်လို့ ရရင်တော့ အောက်ပါအတိုင်း PSFEditor program ကို တွေ့ရလိမ့်မယ်။  

```
(base) ye@ykt-pro:~/tool/PSFEditor$ ls
dlgsymbinfo.o        moc_mainwindow.o                      PSFEditor.pro                   README.md
include              moc_predefs.h                         psf.o                           src
main.o               moc_qfontglypheditor.cpp              psfutil.o                       ui
mainwindow.o         moc_qfontglypheditor.o                qfontglypheditor.o              ui_dlgsymbinfo.h
Makefile             moc_qglyphlistwidgetitemdelegate.cpp  qglyphlistwidgetitemdelegate.o  ui_mainwindow.h
moc_dlgsymbinfo.cpp  moc_qglyphlistwidgetitemdelegate.o    qrc_psfeditor.cpp
moc_dlgsymbinfo.o    PSFEditor                             qrc_psfeditor.o
moc_mainwindow.cpp   psfeditor.png                         rc
(base) ye@ykt-pro:~/tool/PSFEditor$ 
```

စမ်းဖို့အတွက် Thai psf font ဖိုင်ကို အသစ်ဆောက်ထားတဲ့ font/ folder အောက်ကို ကူးယူခဲ့ ...  

```
(base) ye@ykt-pro:~/tool/PSFEditor$ cp /media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv/Thai-Fixed16.psf ./font/
(base) ye@ykt-pro:~/tool/PSFEditor$ 
```

## Test Run

run ကြည့်ပြီး Thai psf font ဖိုင်ကို ဖွင့် ကြည့်ခဲ့ ...  



## Reference

- https://blog.kalehmann.de/blog/2018/12/28/pysfedit.html
- https://github.com/ideras/PSFEditor
- https://fontark.net/farkwp/

