# compare-mt running log

POS tag label တွေပါ သုံးပြီး evaluation လုပ်ခိုင်းတော့ error တက်ပြီး ရှင်းလို့မရဆိုလို့ ကိုယ်တိုင် error ရှင်းခဲ့စဉ်က မှတ်ထားတဲ့ log ဖိုင်ပါ။  
ငါကိုယ်တိုင်လည်း bootstrap function ကို သုံးဖို့ စမ်းကြည့်တော့ error ပေးနေတယ်။ error နှစ်ခုက မတူပေမဲ့ python environment နဲ့ ဆိုင်တယ် သို့မဟုတ် library ကြောင့်လို့ ယူဆထားခဲ့...  
ငါ့စက်ထဲမှာ ပေးတဲ့ error က အောက်ပါအတိုင်း...  

**(Solution က setup.py ကနေ installation လုပ်တာမျိုးမဟုတ်ပဲ pip install နဲ့ သွားတာ...။ နောက်ဆုံးနားက "Section: Installation of compare-mt Success" ကို ကျော်ပြီးတော့ ကြည့်ပါ။)**  

```
(base) ye@ykt-pro:/media/ye/project1/exp/rk-bk-my-word-pivot/final-compare$ ./mk-compare-html-bootstrap.sh | tee run-all-bootstrap.log
...
...
...

Transfer-Pivot-Triangulation-Pivot=-65.1983, Transfer-Pivot=34.8017, Triangulation-Pivot=100.0000
Ref:  သူ က သူ့ ကို ချစ် ဟုတ်ဝ ။
Transfer-Pivot: သူဝ ဒယ်ကောင်မငယ် ဝို ချစ် ဟုတ်ဝ ။
Triangulation-Pivot: သူ က သူ့ ကို ချစ် ဟုတ်ဝ ။

Traceback (most recent call last):
  File "/home/ye/tool/anaconda3/bin/compare-mt", line 11, in <module>
    load_entry_point('compare-mt==0.2.4', 'console_scripts', 'compare-mt')()
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/compare_mt_main.py", line 595, in main
    reporters.generate_html_report(reports, args.output_directory, args.report_title)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/reporters.py", line 652, in generate_html_report
    content.append(r.html_content(output_directory))
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/reporters.py", line 216, in html_content
    self.plot(output_directory, self.output_fig_file, ext)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/reporters.py", line 208, in plot
    xticklabels=xticklabels)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/reporters.py", line 79, in make_bar_chart
    bars.append(ax.bar(ind+i*width, data, width, color=bar_colors[i], bottom=0, yerr=err))
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/matplotlib/__init__.py", line 1601, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/matplotlib/axes/_axes.py", line 2456, in bar
    fmt='none', **error_kw)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/matplotlib/__init__.py", line 1601, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/matplotlib/axes/_axes.py", line 3424, in errorbar
    lower, upper = extract_err(yerr, y)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/matplotlib/axes/_axes.py", line 3357, in extract_err
    "err must be a scalar or a 1D or (2, n) array-like")
ValueError: err must be a scalar or a 1D or (2, n) array-like
####################
(base) ye@ykt-pro:/media/ye/project1/exp/rk-bk-my-word-pivot/final-compare$
```

ဇာဇာလှိုင်ရဲ့ စက်ထဲမှာလည်း အဲဒီလိုပဲ error ပေးနေတယ် ဆိုတော့ ဖြစ်ဖို့များတာက library version, python environment etc. တွေကြောင့်လားလို့....  
python version နိမ့်တာက စက်ထဲမှာ ရှိနေလို့ အဲဒီ env ထဲဝင်ပြီး အရင်ဆုံး setup run ဖို့ ကြိုးစားကြည့်ခဲ့  

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install -r requirements.txt 
Collecting nltk>=3.2
  Downloading nltk-3.6.7-py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 1.6 MB/s 
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from -r requirements.txt (line 2)) (1.18.1)
Requirement already satisfied: matplotlib in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from -r requirements.txt (line 3)) (3.1.3)
Collecting absl-py
  Downloading absl_py-1.0.0-py3-none-any.whl (126 kB)
     |████████████████████████████████| 126 kB 6.6 MB/s 
Collecting sacrebleu
  Downloading sacrebleu-2.0.0-py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 4.9 MB/s 
Collecting langid
  Using cached langid-1.1.6.tar.gz (1.9 MB)
ERROR: Could not find a version that satisfies the requirement wtl (from -r requirements.txt (line 7)) (from versions: none)
ERROR: No matching distribution found for wtl (from -r requirements.txt (line 7))
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ gedit requirements.txt 
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda deactivate

အထက်ပါအတိုင်း wtl ကို installation မှာ error ပေးတယ်။

wtl က original compare-mt ရဲ့ requirements.txt မှာ မပါဘူး။
ငါ ပထမတစ်ခေါက် installation လုပ်ထားတုန်းက လိုအပ်လို့ ဖြည့်ထားခဲ့တာလို့ ထင်တယ်။
အဲဒါကို comment ပိတ်ပြီး installation ကို ဆက်လုပ်ကြည့်ခဲ့တယ်... 

(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install -r requirements.txt 
Collecting nltk>=3.2
  Using cached nltk-3.6.7-py3-none-any.whl (1.5 MB)
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from -r requirements.txt (line 2)) (1.18.1)
Requirement already satisfied: matplotlib in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from -r requirements.txt (line 3)) (3.1.3)
Collecting absl-py
  Using cached absl_py-1.0.0-py3-none-any.whl (126 kB)
Collecting sacrebleu
  Using cached sacrebleu-2.0.0-py3-none-any.whl (90 kB)
Collecting langid
  Using cached langid-1.1.6.tar.gz (1.9 MB)
Collecting regex>=2021.8.3
  Downloading regex-2021.11.10-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (748 kB)
     |████████████████████████████████| 748 kB 1.7 MB/s 
Collecting click
  Downloading click-8.0.3-py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 2.6 MB/s 
Requirement already satisfied: joblib in /home/ye/.local/lib/python3.6/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (0.15.1)
Requirement already satisfied: tqdm in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/tqdm-4.46.0-py3.6.egg (from nltk>=3.2->-r requirements.txt (line 1)) (4.46.0)
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (2.8.1)
Requirement already satisfied: cycler>=0.10 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (0.10.0)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (2.4.7)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (1.2.0)
Requirement already satisfied: six in /home/ye/.local/lib/python3.6/site-packages (from absl-py->-r requirements.txt (line 4)) (1.15.0)
Collecting colorama
  Downloading colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting portalocker
  Downloading portalocker-2.3.2-py2.py3-none-any.whl (15 kB)
Collecting tabulate>=0.8.9
  Downloading tabulate-0.8.9-py3-none-any.whl (25 kB)
Requirement already satisfied: importlib-metadata; python_version < "3.8" in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from click->nltk>=3.2->-r requirements.txt (line 1)) (1.5.0)
Requirement already satisfied: zipp>=0.5 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from importlib-metadata; python_version < "3.8"->click->nltk>=3.2->-r requirements.txt (line 1)) (3.1.0)
Building wheels for collected packages: langid
  Building wheel for langid (setup.py) ... done
  Created wheel for langid: filename=langid-1.1.6-py3-none-any.whl size=1941188 sha256=59fc753162e7e701f991dffb6b37b5f309834f3d112bc893045cc7e83e6a9b58
  Stored in directory: /home/ye/.cache/pip/wheels/b4/77/b4/b38806c8087e0860cfeabab1f96b60c48346d8db59a9254787
Successfully built langid
Installing collected packages: regex, click, nltk, absl-py, colorama, portalocker, tabulate, sacrebleu, langid
Successfully installed absl-py-1.0.0 click-8.0.3 colorama-0.4.4 langid-1.1.6 nltk-3.6.7 portalocker-2.3.2 regex-2021.11.10 sacrebleu-2.0.0 tabulate-0.8.9
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

setup ကို အောက်ပါအတိုင်း လုပ်ခဲ့...  

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ python setup.py install
...
...
...
e 195, in setup_context
    yield
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/setuptools/sandbox.py", line 250, in run_setup
    _execfile(setup_script, ns)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/setuptools/sandbox.py", line 45, in _execfile
    exec(code, globals, locals)
  File "/tmp/easy_install-bovbpurr/pyfasttext-0.4.6/setup.py", line 3, in <module>
    import codecs
ModuleNotFoundError: No module named 'Cython'

Cython မရှိဘူးဆိုပြီးတော့ error ပေးနေလို့ Cython ကို အောက်ပါအတိုင်း installation လုပ်ခဲ့တယ်။

(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install Cython
Collecting Cython
  Downloading Cython-0.29.26-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
     |████████████████████████████████| 1.9 MB 1.7 MB/s 
ERROR: whatthelang 1.0.1 requires cysignals, which is not installed.
ERROR: whatthelang 1.0.1 requires pyfasttext, which is not installed.
Installing collected packages: Cython
Successfully installed Cython-0.29.26

အထက်မှာ whatthelang ဆိုတာက မရှိဘူး ပြောနေလို့ အောက်ပါအတိုင်း whatthelang ကို install လုပ်ခဲ့တယ်။  

(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install whatthelang
Requirement already satisfied: whatthelang in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/whatthelang-1.0.1-py3.6.egg (1.0.1)
Requirement already satisfied: Cython in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from whatthelang) (0.29.26)
Collecting cysignals
  Downloading cysignals-1.11.2-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (867 kB)
     |████████████████████████████████| 867 kB 1.6 MB/s 
Collecting pyfasttext
  Using cached pyfasttext-0.4.6.tar.gz (244 kB)
Processing /home/ye/.cache/pip/wheels/6e/9c/ed/4499c9865ac1002697793e0ae05ba6be33553d098f3347fb94/future-0.18.2-py3-none-any.whl
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from pyfasttext->whatthelang) (1.18.1)
Building wheels for collected packages: pyfasttext
  Building wheel for pyfasttext (setup.py) ... done
  Created wheel for pyfasttext: filename=pyfasttext-0.4.6-cp36-cp36m-linux_x86_64.whl size=2147583 sha256=d2eed50faf382c64a2f4c33cee72eb6d9aa19c151e066a879e568dbb50de8ab6
  Stored in directory: /home/ye/.cache/pip/wheels/81/98/74/cdaf00a160739381e20d22ade32a0914c06db2846425eb8db5
Successfully built pyfasttext
Installing collected packages: cysignals, future, pyfasttext
Successfully installed cysignals-1.11.2 future-0.18.2 pyfasttext-0.4.6
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$

setup ကို ပြန် run ပေးခဲ့တယ်။   

(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ python setup.py install
running install
running bdist_egg
running egg_info
writing compare_mt.egg-info/PKG-INFO
writing dependency_links to compare_mt.egg-info/dependency_links.txt
writing entry points to compare_mt.egg-info/entry_points.txt
writing requirements to compare_mt.egg-info/requires.txt
writing top-level names to compare_mt.egg-info/top_level.txt
reading manifest file 'compare_mt.egg-info/SOURCES.txt'
writing manifest file 'compare_mt.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_scorers.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_repetition_utils.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/__init__.py -> build/bdist.linux-x86_64/egg/tests
creating build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/stat_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/sign_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/scorers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/reporters.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/repetition_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/print_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/ngram_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/formatting.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/corpus_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_mt_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_ll_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/bucketers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/arg_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/align_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt
creating build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/tokenizer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/scoring.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge_scorer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/io.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
byte-compiling build/bdist.linux-x86_64/egg/tests/test_scorers.py to test_scorers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/test_repetition_utils.py to test_repetition_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/stat_utils.py to stat_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/sign_utils.py to sign_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/scorers.py to scorers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/reporters.py to reporters.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/repetition_utils.py to repetition_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/print_utils.py to print_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/ngram_utils.py to ngram_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/formatting.py to formatting.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/corpus_utils.py to corpus_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_mt_main.py to compare_mt_main.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_ll_main.py to compare_ll_main.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/bucketers.py to bucketers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/arg_utils.py to arg_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/align_utils.py to align_utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/tokenizer.py to tokenizer.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/scoring.py to scoring.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge_scorer.py to rouge_scorer.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge.py to rouge.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/io.py to io.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/__init__.py to __init__.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
tests.__pycache__.test_repetition_utils.cpython-36: module references __file__
tests.__pycache__.test_scorers.cpython-36: module references __file__
creating 'dist/compare_mt-0.2.4-py3.6.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing compare_mt-0.2.4-py3.6.egg
removing '/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg' (and everything under it)
creating /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg
Extracting compare_mt-0.2.4-py3.6.egg to /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
compare-mt 0.2.4 is already the active version in easy-install.pth
Installing compare-ll script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing compare-mt script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Installed /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg
Processing dependencies for compare-mt==0.2.4
Searching for whatthelang==1.0.1
Best match: whatthelang 1.0.1
Processing whatthelang-1.0.1-py3.6.egg
whatthelang 1.0.1 is already the active version in easy-install.pth

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/whatthelang-1.0.1-py3.6.egg
Searching for langid==1.1.6
Best match: langid 1.1.6
Adding langid 1.1.6 to easy-install.pth file
Installing langid script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for sacrebleu==2.0.0
Best match: sacrebleu 2.0.0
Adding sacrebleu 2.0.0 to easy-install.pth file
Installing sacrebleu script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for absl-py==1.0.0
Best match: absl-py 1.0.0
Adding absl-py 1.0.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for matplotlib==3.1.3
Best match: matplotlib 3.1.3
Adding matplotlib 3.1.3 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for numpy==1.18.1
Best match: numpy 1.18.1
Adding numpy 1.18.1 to easy-install.pth file
Installing f2py script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing f2py3 script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing f2py3.6 script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for nltk==3.6.7
Best match: nltk 3.6.7
Adding nltk 3.6.7 to easy-install.pth file
Installing nltk script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for pyfasttext==0.4.6
Best match: pyfasttext 0.4.6
Adding pyfasttext 0.4.6 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for cysignals==1.11.2
Best match: cysignals 1.11.2
Adding cysignals 1.11.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for Cython==0.29.26
Best match: Cython 0.29.26
Adding Cython 0.29.26 to easy-install.pth file
Installing cygdb script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing cython script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing cythonize script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for portalocker==2.3.2
Best match: portalocker 2.3.2
Adding portalocker 2.3.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for tabulate==0.8.9
Best match: tabulate 0.8.9
Adding tabulate 0.8.9 to easy-install.pth file
Installing tabulate script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for colorama==0.4.4
Best match: colorama 0.4.4
Adding colorama 0.4.4 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for regex==2021.11.10
Best match: regex 2021.11.10
Adding regex 2021.11.10 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /home/ye/.local/lib/python3.6/site-packages
Searching for python-dateutil==2.8.1
Best match: python-dateutil 2.8.1
Adding python-dateutil 2.8.1 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for kiwisolver==1.2.0
Best match: kiwisolver 1.2.0
Adding kiwisolver 1.2.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for cycler==0.10.0
Best match: cycler 0.10.0
Adding cycler 0.10.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for pyparsing==2.4.7
Best match: pyparsing 2.4.7
Adding pyparsing 2.4.7 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for tqdm==4.46.0
Best match: tqdm 4.46.0
Processing tqdm-4.46.0-py3.6.egg
tqdm 4.46.0 is already the active version in easy-install.pth
Installing tqdm script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/tqdm-4.46.0-py3.6.egg
Searching for click==8.0.3
Best match: click 8.0.3
Adding click 8.0.3 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for joblib==0.15.1
Best match: joblib 0.15.1
Adding joblib 0.15.1 to easy-install.pth file

Using /home/ye/.local/lib/python3.6/site-packages
Searching for future==0.18.2
Best match: future 0.18.2
Adding future 0.18.2 to easy-install.pth file
Installing futurize script to /home/ye/tool/anaconda3/envs/conda3.6/bin
Installing pasteurize script to /home/ye/tool/anaconda3/envs/conda3.6/bin

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for importlib-metadata==1.5.0
Best match: importlib-metadata 1.5.0
Adding importlib-metadata 1.5.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Searching for zipp==3.1.0
Best match: zipp 3.1.0
Adding zipp 3.1.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages
Finished processing dependencies for compare-mt==0.2.4
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

## Call --help

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt --help
usage: compare-mt [-h] [--sys_names SYS_NAMES [SYS_NAMES ...]]
                  [--src_file SRC_FILE] [--fig_size FIG_SIZE]
                  [--compare_scores [COMPARE_SCORES [COMPARE_SCORES ...]]]
                  [--compare_word_accuracies [COMPARE_WORD_ACCURACIES [COMPARE_WORD_ACCURACIES ...]]]
                  [--compare_src_word_accuracies [COMPARE_SRC_WORD_ACCURACIES [COMPARE_SRC_WORD_ACCURACIES ...]]]
                  [--compare_sentence_buckets [COMPARE_SENTENCE_BUCKETS [COMPARE_SENTENCE_BUCKETS ...]]]
                  [--compare_ngrams [COMPARE_NGRAMS [COMPARE_NGRAMS ...]]]
                  [--compare_sentence_examples [COMPARE_SENTENCE_EXAMPLES [COMPARE_SENTENCE_EXAMPLES ...]]]
                  [--compare_repetitions [COMPARE_REPETITIONS [COMPARE_REPETITIONS ...]]]
                  [--compare_repetition_examples [COMPARE_REPETITION_EXAMPLES [COMPARE_REPETITION_EXAMPLES ...]]]
                  [--output_directory OUTPUT_DIRECTORY]
                  [--report_title REPORT_TITLE] [--decimals DECIMALS]
                  [--scorer_scale {1,100}] [--lang_id [LANG_ID [LANG_ID ...]]]
                  ref_file out_files [out_files ...]

Program to compare MT results

positional arguments:
  ref_file              A path to a correct reference file
  out_files             Paths to system outputs

optional arguments:
  -h, --help            show this help message and exit
  --sys_names SYS_NAMES [SYS_NAMES ...]
                        Names for each system, must be same number as output
                        files
  --src_file SRC_FILE   A path to the source file
  --fig_size FIG_SIZE   The size of figures, in "width x height" format.
  --compare_scores [COMPARE_SCORES [COMPARE_SCORES ...]]
                        Compare scores. Can specify arguments in
                        'arg1=val1,arg2=val2,...' format. See documentation
                        for 'generate_score_report' to see which arguments are
                        available.
  --compare_word_accuracies [COMPARE_WORD_ACCURACIES [COMPARE_WORD_ACCURACIES ...]]
                        Compare word accuracies by buckets. Can specify
                        arguments in 'arg1=val1,arg2=val2,...' format. See
                        documentation for 'generate_word_accuracy_report' to
                        see which arguments are available.
  --compare_src_word_accuracies [COMPARE_SRC_WORD_ACCURACIES [COMPARE_SRC_WORD_ACCURACIES ...]]
                        Source analysis. Can specify arguments in
                        'arg1=val1,arg2=val2,...' format. See documentation
                        for 'generate_src_word_accuracy_report' to see which
                        arguments are available.
  --compare_sentence_buckets [COMPARE_SENTENCE_BUCKETS [COMPARE_SENTENCE_BUCKETS ...]]
                        Compare sentence counts by buckets. Can specify
                        arguments in 'arg1=val1,arg2=val2,...' format. See
                        documentation for 'generate_sentence_buckets_report'
                        to see which arguments are available.
  --compare_ngrams [COMPARE_NGRAMS [COMPARE_NGRAMS ...]]
                        Compare ngrams. Can specify arguments in
                        'arg1=val1,arg2=val2,...' format. See documentation
                        for 'generate_ngram_report' to see which arguments are
                        available.
  --compare_sentence_examples [COMPARE_SENTENCE_EXAMPLES [COMPARE_SENTENCE_EXAMPLES ...]]
                        Compare sentences. Can specify arguments in
                        'arg1=val1,arg2=val2,...' format. See documentation
                        for 'generate_sentence_examples' to see which
                        arguments are available.
  --compare_repetitions [COMPARE_REPETITIONS [COMPARE_REPETITIONS ...]]
                        Compare repetition statistics. Can specify arguments
                        in 'arg1=val1,arg2=val2,...' format. See documentation
                        for 'generate_repetitions_report' to see which
                        arguments are available.
  --compare_repetition_examples [COMPARE_REPETITION_EXAMPLES [COMPARE_REPETITION_EXAMPLES ...]]
                        Compare sentences that contain repetitions. Can
                        specify arguments in 'arg1=val1,arg2=val2,...' format.
                        See documentation for 'generate_repetition_examples'
                        to see which arguments are available.
  --output_directory OUTPUT_DIRECTORY
                        A path to a directory where a graphical report will be
                        saved. Open index.html in the directory to read the
                        report.
  --report_title REPORT_TITLE
                        The name of the HTML report.
  --decimals DECIMALS   Number of decimals to print for floating point numbers
  --scorer_scale {1,100}
                        Set the scale of BLEU, METEOR, WER and chrF to 0-1 or
                        0-100 (default 0-100)
  --lang_id [LANG_ID [LANG_ID ...]]
                        Use language identification on output. Can specify
                        arguments in 'arg1=val1,arg2=val2,...' format.
                        Arguments: model=[wtl,langid], min_length=int,
                        print_lines=[True,False],
                        print_line_numbers=[True,False] Set minimum length for
                        segments to be analyzed with language identification
                        (the shorter the segment, the more unreliable the
                        analysis), default=5.
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

Help screen ကတော့ အထက်ပါအတိုင်း တက်လာတယ်။   

## run example command

အောက်ပါအတိုင်း error ပေးတယ်...  

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt example/ted.ref.eng example/ted.sys1.eng example/ted.sys2.eng --compare_scores score_type=bleu,bootstrap=1000 score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000 --compare_word_accuracies bucket_type=freq,freq_corpus_file=example/ted.train.eng bucket_type=label,ref_labels=example/ted.ref.eng.tag,out_labels=\
> "example/ted.sys1.eng.tag;example/ted.sys2.eng.tag",\
> label_set=CC+DT+IN+JJ+NN+NNP+NNS+PRP+RB+TO+VB+VBP+VBZ --output_directory outputs --sys_names PBMT NMT
********************** Aggregate Scores ************************
BLEU:
	PBMT	NMT	Win?
BLEU	22.4309	24.0322	s2>s1
	[21.6638,23.2117]	[23.2452,24.7964]	p=0.0000

********************** Aggregate Scores ************************
RIBES:
	PBMT	NMT	Win?
RIBES	80.0020	79.9978	-
	[79.3705,80.5776]	[79.3388,80.6832]	p=0.4910

********************** Aggregate Scores ************************
length ratio:
	PBMT	NMT	Win?
length ratio	0.9479 (ref=48183, out=45672)	0.9382 (ref=48183, out=45207)	s1>s2
	[0.9407,0.9546]	[0.9299,0.9465]	p=0.0050

Reading frequency from "example/ted.train.eng"
********************** Word Accuracy Analysis ************************
--- word fmeas by frequency bucket
<1	0.1005	0.0493
1	0.2226	0.0850
2	0.3430	0.1735
3	0.3644	0.2408
4	0.4364	0.1667
[5,10)	0.3664	0.2012
[10,100)	0.4843	0.3880
[100,1000)	0.5482	0.5160
>=1000	0.6377	0.6485

********************** Word Accuracy Analysis ************************
--- word fmeas by labels bucket
CC	0.7877	0.8043
DT	0.5252	0.5634
IN	0.5360	0.5441
JJ	0.4991	0.4620
NN	0.5485	0.4828
NNP	0.6297	0.4930
NNS	0.5591	0.4992
PRP	0.6274	0.6584
RB	0.4861	0.4662
TO	0.6246	0.6360
VB	0.4720	0.4366
VBP	0.4339	0.4533
VBZ	0.4814	0.5031
other	0.6716	0.6661

********************** Sentence Bucket Analysis ************************
--- bucket type: length, statistic type: BLEU
<10	22.3102	25.3150
[10,20)	20.9790	24.6741
[20,30)	23.1616	23.7933
[30,40)	21.7460	23.1794
[40,50)	22.1873	21.8982
[50,60)	23.3107	25.5426
>=60	27.2580	24.7044

********************** Sentence Bucket Analysis ************************
--- bucket type: len(output)-len(reference), statistic type: count
<-20	0	9
[-20,-10)	39	51
[-10,-5)	194	182
-5	107	93
-4	127	153
-3	219	194
-2	296	275
-1	330	344
0	394	423
1	263	256
2	173	187
3	115	97
4	73	58
5	41	44
[6,11)	66	67
[11,21)	8	12
>=21	0	0

********************** Sentence Bucket Analysis ************************
--- bucket type: sentence-level BLEU, statistic type: count
<10.0	141	136
[10.0,20.0)	857	817
[20.0,30.0)	628	581
[30.0,40.0)	379	391
[40.0,50.0)	193	206
[50.0,60.0)	101	127
[60.0,70.0)	53	64
[70.0,80.0)	31	43
[80.0,90.0)	31	36
>=90.0	31	44

********************** N-gram Difference Analysis ************************
--- min_ngram_length=1, max_ngram_length=4
    report_length=50, alpha=1.0, compare_type=match
--- 50 n-grams where PBMT>NMT in match
phantom	0.9459 (sys1=34, sys2=1)
Amy	0.9091 (sys1=9, sys2=0)
, who	0.9000 (sys1=8, sys2=0)
my mother	0.8889 (sys1=7, sys2=0)
And so	0.8571 (sys1=5, sys2=0)
something else happened	0.8571 (sys1=5, sys2=0)
my mother .	0.8571 (sys1=5, sys2=0)
Avelile	0.8571 (sys1=5, sys2=0)
else happened	0.8571 (sys1=5, sys2=0)
rightness	0.8333 (sys1=4, sys2=0)
file	0.8333 (sys1=4, sys2=0)
the fusiform	0.8333 (sys1=4, sys2=0)
my mother . "	0.8333 (sys1=4, sys2=0)
mother . "	0.8333 (sys1=4, sys2=0)
and so on	0.8333 (sys1=4, sys2=0)
fusiform	0.8333 (sys1=4, sys2=0)
Center	0.8333 (sys1=4, sys2=0)
centers	0.8333 (sys1=4, sys2=0)
mother . " "	0.8333 (sys1=4, sys2=0)
so on	0.8333 (sys1=4, sys2=0)
Oz	0.8333 (sys1=4, sys2=0)
fine	0.8333 (sys1=4, sys2=0)
the phantom	0.8333 (sys1=4, sys2=0)
viewer	0.8333 (sys1=4, sys2=0)
instead	0.8182 (sys1=8, sys2=1)
exchange	0.8125 (sys1=12, sys2=2)
stroke	0.8000 (sys1=3, sys2=0)
creativity can	0.8000 (sys1=3, sys2=0)
46664	0.8000 (sys1=3, sys2=0)
response	0.8000 (sys1=3, sys2=0)
the Bible	0.8000 (sys1=3, sys2=0)
WikiLeaks	0.8000 (sys1=3, sys2=0)
billion pixels	0.8000 (sys1=3, sys2=0)
. The	0.8000 (sys1=3, sys2=0)
of women	0.8000 (sys1=3, sys2=0)
exactly like	0.8000 (sys1=3, sys2=0)
gyrus	0.8000 (sys1=3, sys2=0)
Israel	0.8000 (sys1=3, sys2=0)
and so on .	0.8000 (sys1=3, sys2=0)
amygdala	0.8000 (sys1=3, sys2=0)
. And	0.8000 (sys1=3, sys2=0)
fusiform gyrus	0.8000 (sys1=3, sys2=0)
found that	0.8000 (sys1=3, sys2=0)
Limpopo	0.8000 (sys1=3, sys2=0)
pixels	0.8000 (sys1=3, sys2=0)
Bible	0.8000 (sys1=3, sys2=0)
Baghdad	0.8000 (sys1=3, sys2=0)
like my mother	0.8000 (sys1=3, sys2=0)
Beth	0.8000 (sys1=3, sys2=0)
excited	0.8000 (sys1=3, sys2=0)

--- 50 n-grams where NMT>PBMT in match
going to show you	0.1250 (sys1=0, sys2=6)
going to show	0.1250 (sys1=0, sys2=6)
, because the	0.1429 (sys1=0, sys2=5)
't even	0.1429 (sys1=0, sys2=5)
Is it	0.1429 (sys1=0, sys2=5)
hemisphere	0.1429 (sys1=0, sys2=5)
'm going to show	0.1429 (sys1=0, sys2=5)
Is	0.1429 (sys1=0, sys2=5)
: Okay	0.1667 (sys1=0, sys2=4)
the presence of	0.1667 (sys1=0, sys2=4)
years old	0.1667 (sys1=0, sys2=4)
the light	0.1667 (sys1=0, sys2=4)
the camera	0.1667 (sys1=0, sys2=4)
the process	0.1667 (sys1=0, sys2=4)
presence of	0.1667 (sys1=0, sys2=4)
left hemisphere	0.1667 (sys1=0, sys2=4)
the present	0.1667 (sys1=0, sys2=4)
: Okay ,	0.1667 (sys1=0, sys2=4)
process of	0.1667 (sys1=0, sys2=4)
yet	0.1667 (sys1=0, sys2=4)
with a	0.1818 (sys1=1, sys2=8)
how do	0.1818 (sys1=1, sys2=8)
babies are	0.2000 (sys1=0, sys2=3)
told	0.2000 (sys1=0, sys2=3)
little bit	0.2000 (sys1=0, sys2=3)
the kids	0.2000 (sys1=0, sys2=3)
what 's going	0.2000 (sys1=0, sys2=3)
, there 's a	0.2000 (sys1=0, sys2=3)
, as if	0.2000 (sys1=0, sys2=3)
a little bit	0.2000 (sys1=0, sys2=3)
Everything	0.2000 (sys1=0, sys2=3)
how do you	0.2000 (sys1=0, sys2=3)
to show	0.2000 (sys1=1, sys2=7)
core of	0.2000 (sys1=0, sys2=3)
, he	0.2000 (sys1=0, sys2=3)
it doesn	0.2000 (sys1=0, sys2=3)
don 't even	0.2000 (sys1=0, sys2=3)
the surgeon	0.2000 (sys1=0, sys2=3)
if they	0.2000 (sys1=0, sys2=3)
the puzzle	0.2000 (sys1=0, sys2=3)
leave	0.2000 (sys1=0, sys2=3)
a computer mouse	0.2000 (sys1=0, sys2=3)
a short	0.2000 (sys1=0, sys2=3)
AG : Okay ,	0.2000 (sys1=0, sys2=3)
I was a	0.2000 (sys1=0, sys2=3)
he was	0.2000 (sys1=0, sys2=3)
it doesn 't	0.2000 (sys1=0, sys2=3)
that .	0.2000 (sys1=0, sys2=3)
a computer	0.2000 (sys1=0, sys2=3)
the panels	0.2000 (sys1=0, sys2=3)

********************** Sentence Examples Analysis ************************
--- 10 sentences where PBMT>NMT at sentence-level BLEU
PBMT-NMT=83.8501, PBMT=100.0000, NMT=16.1499
Ref:  That 's exciting in itself .
PBMT: That 's exciting in itself .
NMT: This is a thrill of self .

PBMT-NMT=80.3593, PBMT=100.0000, NMT=19.6407
Ref:  And they lived together happily ever after .
PBMT: And they lived together happily ever after .
NMT: And he lived with happily to death .

PBMT-NMT=60.2365, PBMT=100.0000, NMT=39.7635
Ref:  Beth Israel 's in Boston .
PBMT: Beth Israel 's in Boston .
NMT: Beat Isaill is in Boston .

PBMT-NMT=58.0890, PBMT=100.0000, NMT=41.9110
Ref:  ( Applause ) Last question , Julian .
PBMT: ( Applause ) Last question , Julian .
NMT: ( Applause ) The last question , Julian . Julan .

PBMT-NMT=55.9402, PBMT=73.6064, NMT=17.6662
Ref:  We realized that even rich kids from the suburbs really want DryBath . ( Laughter ) At least once a week .
PBMT: And we found that even rich kids a suburbs really want DryBath . ( Laughter ) At least once a week .
NMT: We 've learned that the rich kids have actually wanted DryBothth , ( Laughter ) at the time for a week .

PBMT-NMT=52.5045, PBMT=100.0000, NMT=47.4955
Ref:  JA : I 'm not sure about the incident .
PBMT: JA : I 'm not sure about the incident .
NMT: J : I 'm not sure of you .

PBMT-NMT=50.9120, PBMT=62.4209, NMT=11.5088
Ref:  This was described beautifully in a book in 2006 by Michael Porter and Elizabeth Teisberg .
PBMT: This was described beautifully in 2006 in a book that wrote Michael Porter and Elizabeth Teisberg .
NMT: This was originally gorgeous in 2006 in 2006 in 2006 , and they wrote Michael Porrter and Edzabet Tode .

PBMT-NMT=50.0000, PBMT=100.0000, NMT=50.0000
Ref:  Why is that ?
PBMT: Why is that ?
NMT: Why is this ?

PBMT-NMT=47.5859, PBMT=72.7245, NMT=25.1386
Ref:  I don 't literally mean 24 hours , seven days a week .
PBMT: I don 't mean literally 24 hours , seven days a week .
NMT: I don 't mean literally 24 hours in the week .

PBMT-NMT=46.8170, PBMT=100.0000, NMT=53.1830
Ref:  The differences were dramatic .
PBMT: The differences were dramatic .
NMT: The variations were dramatic .

--- 10 sentences where NMT>PBMT at sentence-level BLEU
PBMT-NMT=-57.1510, PBMT=15.3697, NMT=72.5207
Ref:  Tiny tweaks can lead to big changes .
PBMT: Now , this idea of marginal raisestas can lead to a big change to happen .
NMT: Facferences can lead to big changes .

PBMT-NMT=-59.3851, PBMT=40.6149, NMT=100.0000
Ref:  So here 's a video .
PBMT: So here 's the video . "
NMT: So here 's a video .

PBMT-NMT=-59.3851, PBMT=40.6149, NMT=100.0000
Ref:  It 's not the numbers .
PBMT: It 's not about those numbers .
NMT: It 's not the numbers .

PBMT-NMT=-60.3335, PBMT=14.9794, NMT=75.3129
Ref:  So here I 'm going to show you two tandem clips .
PBMT: Here you 're going to two footage .
NMT: So here I 'm going to show you two footage .

PBMT-NMT=-62.2036, PBMT=37.7964, NMT=100.0000
Ref:  ( Applause ) That 's true .
PBMT: ( Applause ) It 's so .
NMT: ( Applause ) That 's true .

PBMT-NMT=-62.3940, PBMT=37.6060, NMT=100.0000
Ref:  What is this ?
PBMT: " What is that ?
NMT: What is this ?

PBMT-NMT=-65.2492, PBMT=34.7508, NMT=100.0000
Ref:  And what I 'm talking about is this .
PBMT: And that 's what I 'm saying is this .
NMT: And what I 'm talking about is this .

PBMT-NMT=-66.0191, PBMT=33.9809, NMT=100.0000
Ref:  Light is good .
PBMT: The light 's good .
NMT: Light is good .

PBMT-NMT=-69.3835, PBMT=30.6165, NMT=100.0000
Ref:  They 're just learning how to count .
PBMT: Meanwhile just teach to count .
NMT: They 're just learning how to count .

PBMT-NMT=-69.6735, PBMT=30.3265, NMT=100.0000
Ref:  Boy : That 's why .
PBMT: Boy : So .
NMT: Boy : That 's why .

Traceback (most recent call last):
  File "/home/ye/tool/anaconda3/envs/conda3.6/bin/compare-mt", line 11, in <module>
    load_entry_point('compare-mt==0.2.4', 'console_scripts', 'compare-mt')()
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg/compare_mt/compare_mt_main.py", line 595, in main
    reporters.generate_html_report(reports, args.output_directory, args.report_title)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg/compare_mt/reporters.py", line 652, in generate_html_report
    content.append(r.html_content(output_directory))
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg/compare_mt/reporters.py", line 216, in html_content
    self.plot(output_directory, self.output_fig_file, ext)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg/compare_mt/reporters.py", line 208, in plot
    xticklabels=xticklabels)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/compare_mt-0.2.4-py3.6.egg/compare_mt/reporters.py", line 79, in make_bar_chart
    bars.append(ax.bar(ind+i*width, data, width, color=bar_colors[i], bottom=0, yerr=err))
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/__init__.py", line 1599, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 2455, in bar
    fmt='none', **error_kw)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/__init__.py", line 1599, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3423, in errorbar
    lower, upper = extract_err(yerr, y)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3356, in extract_err
    "err must be a scalar or a 1D or (2, n) array-like")
ValueError: err must be a scalar or a 1D or (2, n) array-like
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ 
```

Googling လုပ်ကြည့်တော့ matplotlib ကြောင့်လားလို့ မသင်္ကာလို့ matplotlib ကို uninstall လုပ်ပြီးတော့ ပြန် အသစ် install လုပ်ခဲ့တယ်။  

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip uninstall matplotlib
Found existing installation: matplotlib 3.1.3
Uninstalling matplotlib-3.1.3:
  Would remove:
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib-3.1.3-py3.6-nspkg.pth
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib-3.1.3.dist-info/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axes_grid/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axes_grid1/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axisartist/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/mplot3d/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/pylab.py
Proceed (y/n)? y
  Successfully uninstalled matplotlib-3.1.3
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install matplotlib
Collecting matplotlib
  Downloading matplotlib-3.3.4-cp36-cp36m-manylinux1_x86_64.whl (11.5 MB)
     |████████████████████████████████| 11.5 MB 1.6 MB/s 
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib) (2.4.7)
Requirement already satisfied: pillow>=6.2.0 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib) (7.1.2)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib) (1.2.0)
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib) (2.8.1)
Requirement already satisfied: cycler>=0.10 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib) (0.10.0)
Requirement already satisfied: numpy>=1.15 in /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages (from matplotlib) (1.18.1)
Requirement already satisfied: six>=1.5 in /home/ye/.local/lib/python3.6/site-packages (from python-dateutil>=2.1->matplotlib) (1.15.0)
Installing collected packages: matplotlib
Successfully installed matplotlib-3.3.4
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ 
```

multiple matplotlib ကို ကိုယ့် environment ထဲမှာ installation လုပ်ထားမိတဲ့ ပြဿနာ ဆိုပြီးတော့ တချို့ site တွေကလည်းပြောနေလို့.... အဲဒီမှာ အကြံပေးထားတဲ့အတိုင်း ...   

matplotlib ကို  pip နဲ့ လည်း uninstall လုပ်ခဲ့  
ပြီးတော့ conda uninstall လုပ်ခဲ့  

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip uninstall matplotlib
Found existing installation: matplotlib 3.3.4
Uninstalling matplotlib-3.3.4:
  Would remove:
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib-3.3.4-py3.6-nspkg.pth
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib-3.3.4.dist-info/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axes_grid/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axes_grid1/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/axisartist/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/mplot3d/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/mpl_toolkits/tests/*
    /home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/pylab.py
Proceed (y/n)? y
  Successfully uninstalled matplotlib-3.3.4
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda uninstall matplotlib
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/conda3.6

  removed specs:
    - matplotlib


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    _openmp_mutex-4.5          |            1_gnu          22 KB
    argon2-cffi-20.1.0         |   py36h27cfd23_1          46 KB
    async_generator-1.10       |   py36h28b3542_0          39 KB
    attrs-21.2.0               |     pyhd3eb1b0_0          46 KB
    backcall-0.2.0             |     pyhd3eb1b0_0          13 KB
    bleach-4.0.0               |     pyhd3eb1b0_0         113 KB
    ca-certificates-2021.10.26 |       h06a4308_2         115 KB
    certifi-2021.5.30          |   py36h06a4308_0         139 KB
    cffi-1.14.0                |   py36h2e261b9_0         223 KB
    cycler-0.11.0              |     pyhd3eb1b0_0          12 KB
    decorator-5.1.0            |     pyhd3eb1b0_0          14 KB
    defusedxml-0.7.1           |     pyhd3eb1b0_0          23 KB
    expat-2.4.1                |       h2531618_2         168 KB
    fontconfig-2.13.1          |       h6c09931_0         250 KB
    freeglut-3.0.0             |       hf484d3e_5         176 KB
    freetype-2.11.0            |       h70c0345_0         618 KB
    graphite2-1.3.14           |       h23475e2_0          99 KB
    hdf5-1.10.2                |       hba1933b_1         3.8 MB
    importlib-metadata-4.8.1   |   py36h06a4308_0          38 KB
    importlib_metadata-4.8.1   |       hd3eb1b0_0          11 KB
    intel-openmp-2021.4.0      |    h06a4308_3561         4.2 MB
    ipykernel-5.3.4            |   py36h5ca1d4c_0         181 KB
    ipython-7.16.1             |   py36h5ca1d4c_0         999 KB
    ipywidgets-7.6.5           |     pyhd3eb1b0_1         105 KB
    jasper-2.0.14              |       hd8c5072_2         736 KB
    jinja2-3.0.2               |     pyhd3eb1b0_0         110 KB
    joblib-1.0.1               |     pyhd3eb1b0_0         208 KB
    jpeg-9d                    |       h7f8727e_0         232 KB
    jsonschema-3.2.0           |     pyhd3eb1b0_2          47 KB
    jupyter_client-7.1.0       |     pyhd3eb1b0_0         100 KB
    jupyter_console-6.4.0      |     pyhd3eb1b0_0          23 KB
    jupyter_core-4.8.1         |   py36h06a4308_0          74 KB
    jupyterlab_widgets-1.0.0   |     pyhd3eb1b0_1         109 KB
    kiwisolver-1.3.1           |   py36h2531618_0          80 KB
    lcms2-2.12                 |       h3be6417_0         312 KB
    ld_impl_linux-64-2.35.1    |       h7274673_9         586 KB
    libgcc-ng-9.3.0            |      h5101ec6_17         4.8 MB
    libgfortran-ng-7.5.0       |      ha8ba4b0_17          22 KB
    libgfortran4-7.5.0         |      ha8ba4b0_17         995 KB
    libglu-9.0.0               |       hf484d3e_1         271 KB
    libgomp-9.3.0              |      h5101ec6_17         311 KB
    libstdcxx-ng-9.3.0         |      hd4cf53a_17         3.1 MB
    libtiff-4.2.0              |       h85742a9_0         502 KB
    libuuid-1.0.3              |       h7f8727e_2          17 KB
    libwebp-base-1.2.0         |       h27cfd23_0         437 KB
    libxml2-2.9.12             |       h03d6c58_0         1.2 MB
    lz4-c-1.9.3                |       h295c915_1         185 KB
    markupsafe-2.0.1           |   py36h27cfd23_0          21 KB
    matplotlib-base-3.3.4      |   py36h62a2d02_0         5.1 MB
    mkl-service-2.3.0          |   py36he8ac12f_0          52 KB
    mkl_fft-1.3.0              |   py36h54f3939_0         170 KB
    nbclient-0.5.3             |     pyhd3eb1b0_0          62 KB
    nbconvert-6.0.7            |           py36_0         480 KB
    nbformat-5.1.3             |     pyhd3eb1b0_0          44 KB
    ncurses-6.3                |       h7f8727e_2         782 KB
    nest-asyncio-1.5.1         |     pyhd3eb1b0_0          10 KB
    ninja-1.10.2               |       h5e70eb0_2         1.5 MB
    notebook-6.4.3             |   py36h06a4308_0         4.2 MB
    openjpeg-2.4.0             |       h3ad879b_0         331 KB
    openssl-1.1.1l             |       h7f8727e_0         2.5 MB
    packaging-21.3             |     pyhd3eb1b0_0          36 KB
    pandoc-2.12                |       h06a4308_0         9.5 MB
    pandocfilters-1.4.3        |   py36h06a4308_1          14 KB
    parso-0.8.2                |     pyhd3eb1b0_0          69 KB
    patsy-0.5.1                |           py36_0         274 KB
    pcre-8.45                  |       h295c915_0         207 KB
    pillow-8.3.1               |   py36h2c7a002_0         637 KB
    pip-21.2.2                 |   py36h06a4308_0         1.8 MB
    pixman-0.40.0              |       h7f8727e_1         373 KB
    prometheus_client-0.12.0   |     pyhd3eb1b0_0          47 KB
    prompt-toolkit-3.0.20      |     pyhd3eb1b0_0         259 KB
    prompt_toolkit-3.0.20      |       hd3eb1b0_0          12 KB
    ptyprocess-0.7.0           |     pyhd3eb1b0_2          17 KB
    pycparser-2.21             |     pyhd3eb1b0_0          94 KB
    pygments-2.10.0            |     pyhd3eb1b0_0         725 KB
    pyparsing-3.0.4            |     pyhd3eb1b0_0          81 KB
    pyrsistent-0.17.3          |   py36h7b6447c_0          89 KB
    python-dateutil-2.8.2      |     pyhd3eb1b0_0         233 KB
    pytz-2021.3                |     pyhd3eb1b0_0         171 KB
    pyzmq-22.2.1               |   py36h295c915_1         454 KB
    qtconsole-5.1.1            |     pyhd3eb1b0_0          98 KB
    qtpy-1.10.0                |     pyhd3eb1b0_0          35 KB
    readline-8.1               |       h27cfd23_0         362 KB
    scipy-1.5.2                |   py36h0b6359f_0        14.4 MB
    send2trash-1.8.0           |     pyhd3eb1b0_1          19 KB
    setuptools-58.0.4          |   py36h06a4308_0         788 KB
    six-1.16.0                 |     pyhd3eb1b0_0          18 KB
    sqlite-3.37.0              |       hc218d9a_0         999 KB
    statsmodels-0.12.2         |   py36h27cfd23_0         8.6 MB
    terminado-0.9.4            |   py36h06a4308_0          25 KB
    testpath-0.5.0             |     pyhd3eb1b0_0          81 KB
    tk-8.6.11                  |       h1ccaba5_0         3.0 MB
    tornado-6.1                |   py36h27cfd23_0         581 KB
    traitlets-4.3.3            |   py36h06a4308_0         138 KB
    typing_extensions-3.10.0.2 |     pyh06a4308_0          31 KB
    wcwidth-0.2.5              |     pyhd3eb1b0_0          26 KB
    wheel-0.37.0               |     pyhd3eb1b0_1          33 KB
    zeromq-4.3.4               |       h2531618_0         331 KB
    zipp-3.6.0                 |     pyhd3eb1b0_0          17 KB
    zlib-1.2.11                |       h7f8727e_4         108 KB
    zstd-1.4.9                 |       haebb681_0         480 KB
    ------------------------------------------------------------
                                           Total:        85.9 MB

The following NEW packages will be INSTALLED:

  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  argon2-cffi        pkgs/main/linux-64::argon2-cffi-20.1.0-py36h27cfd23_1
  async_generator    pkgs/main/linux-64::async_generator-1.10-py36h28b3542_0
  cffi               pkgs/main/linux-64::cffi-1.14.0-py36h2e261b9_0
  importlib-metadata pkgs/main/linux-64::importlib-metadata-4.8.1-py36h06a4308_0
  jupyterlab_pygmen~ pkgs/main/noarch::jupyterlab_pygments-0.1.2-py_0
  jupyterlab_widgets pkgs/main/noarch::jupyterlab_widgets-1.0.0-pyhd3eb1b0_1
  lcms2              pkgs/main/linux-64::lcms2-2.12-h3be6417_0
  libgfortran4       pkgs/main/linux-64::libgfortran4-7.5.0-ha8ba4b0_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libwebp-base       pkgs/main/linux-64::libwebp-base-1.2.0-h27cfd23_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.3-h295c915_1
  nbclient           pkgs/main/noarch::nbclient-0.5.3-pyhd3eb1b0_0
  nest-asyncio       pkgs/main/noarch::nest-asyncio-1.5.1-pyhd3eb1b0_0
  openjpeg           pkgs/main/linux-64::openjpeg-2.4.0-h3ad879b_0
  packaging          pkgs/main/noarch::packaging-21.3-pyhd3eb1b0_0
  pycparser          pkgs/main/noarch::pycparser-2.21-pyhd3eb1b0_0
  typing_extensions  pkgs/main/noarch::typing_extensions-3.10.0.2-pyh06a4308_0

The following packages will be REMOVED:

  gmp-6.1.2-h6c8ec71_1
  libedit-3.1.20181209-hc058e9b_0
  libgfortran-3.0.0-1
  matplotlib-3.1.3-py36_0
  python_abi-3.6-1_cp36m
  xorg-fixesproto-5.0-h14c3975_1002
  xorg-inputproto-2.3.2-h14c3975_1002
  xorg-kbproto-1.0.7-h14c3975_1002
  xorg-libx11-1.6.9-h516909a_0
  xorg-libxau-1.0.9-h14c3975_0
  xorg-libxext-1.3.4-h516909a_0
  xorg-libxfixes-5.0.3-h516909a_1004
  xorg-libxi-1.7.10-h516909a_0
  xorg-xextproto-7.3.0-h14c3975_1002
  xorg-xproto-7.0.31-h14c3975_1007

The following packages will be UPDATED:

  attrs                                         19.3.0-py_0 --> 21.2.0-pyhd3eb1b0_0
  backcall           pkgs/main/linux-64::backcall-0.1.0-py~ --> pkgs/main/noarch::backcall-0.2.0-pyhd3eb1b0_0
  bleach                                         3.1.4-py_0 --> 4.0.0-pyhd3eb1b0_0
  ca-certificates                               2020.7.22-0 --> 2021.10.26-h06a4308_2
  certifi                                  2020.6.20-py36_0 --> 2021.5.30-py36h06a4308_0
  cycler                    conda-forge::cycler-0.10.0-py_2 --> pkgs/main::cycler-0.11.0-pyhd3eb1b0_0
  dbus                                   1.13.14-hb2f20db_0 --> 1.13.18-hb2f20db_0
  decorator                                      4.4.2-py_0 --> 5.1.0-pyhd3eb1b0_0
  defusedxml                                     0.6.0-py_0 --> 0.7.1-pyhd3eb1b0_0
  expat                                    2.2.6-he6710b0_0 --> 2.4.1-h2531618_2
  fontconfig                              2.13.0-h9420a91_0 --> 2.13.1-h6c09931_0
  freetype                                 2.9.1-h8a8886c_1 --> 2.11.0-h70c0345_0
  graphite2          conda-forge::graphite2-1.3.13-he1b5a4~ --> pkgs/main::graphite2-1.3.14-h23475e2_0
  importlib_metadata pkgs/main/linux-64::importlib_metadat~ --> pkgs/main/noarch::importlib_metadata-4.8.1-hd3eb1b0_0
  intel-openmp                                   2020.1-217 --> 2021.4.0-h06a4308_3561
  ipykernel                            5.1.4-py36h39e3cac_0 --> 5.3.4-py36h5ca1d4c_0
  ipython                             7.13.0-py36h5ca1d4c_0 --> 7.16.1-py36h5ca1d4c_0
  ipython_genutils   pkgs/main/linux-64::ipython_genutils-~ --> pkgs/main/noarch::ipython_genutils-0.2.0-pyhd3eb1b0_1
  ipywidgets                                     7.5.1-py_0 --> 7.6.5-pyhd3eb1b0_1
  jasper                                  2.0.14-h07fcdf6_1 --> 2.0.14-hd8c5072_2
  jinja2                                        2.11.2-py_0 --> 3.0.2-pyhd3eb1b0_0
  joblib                                        0.14.1-py_0 --> 1.0.1-pyhd3eb1b0_0
  jpeg                                        9b-h024ee3a_2 --> 9d-h7f8727e_0
  jsonschema         pkgs/main/linux-64::jsonschema-3.2.0-~ --> pkgs/main/noarch::jsonschema-3.2.0-pyhd3eb1b0_2
  jupyter_client                                 6.1.3-py_0 --> 7.1.0-pyhd3eb1b0_0
  jupyter_console                                6.1.0-py_0 --> 6.4.0-pyhd3eb1b0_0
  jupyter_core                                 4.6.3-py36_0 --> 4.8.1-py36h06a4308_0
  kiwisolver         conda-forge::kiwisolver-1.2.0-py36hdb~ --> pkgs/main::kiwisolver-1.3.1-py36h2531618_0
  ld_impl_linux-64                        2.33.1-h53a641e_7 --> 2.35.1-h7274673_9
  libffi                                   3.2.1-hd88cf55_4 --> 3.2.1-hf484d3e_1007
  libgcc-ng                                9.1.0-hdf63c60_0 --> 9.3.0-h5101ec6_17
  libgfortran-ng                           7.3.0-hdf63c60_0 --> 7.5.0-ha8ba4b0_17
  libsodium                               1.0.16-h1bed415_0 --> 1.0.18-h7b6447c_0
  libstdcxx-ng                             9.1.0-hdf63c60_0 --> 9.3.0-hd4cf53a_17
  libtiff                                  4.1.0-h2733197_0 --> 4.2.0-h85742a9_0
  libxcb                                    1.13-h1bed415_1 --> 1.14-h7b6447c_0
  libxml2                                  2.9.9-hea5a465_1 --> 2.9.12-h03d6c58_0
  markupsafe                           1.1.1-py36h7b6447c_0 --> 2.0.1-py36h27cfd23_0
  matplotlib-base                      3.1.3-py36hef1b27d_0 --> 3.3.4-py36h62a2d02_0
  mkl                                            2020.1-217 --> 2020.2-256
  mkl_fft                             1.0.15-py36ha843d7b_0 --> 1.3.0-py36h54f3939_0
  mkl_random                           1.1.0-py36hd6b4f25_0 --> 1.1.1-py36h0573a6f_0
  nbconvert                                    5.6.1-py36_0 --> 6.0.7-py36_0
  nbformat                                       5.0.6-py_0 --> 5.1.3-pyhd3eb1b0_0
  ncurses                                    6.2-he6710b0_1 --> 6.3-h7f8727e_2
  ninja                                1.9.0-py36hfd86e86_0 --> 1.10.2-h5e70eb0_2
  notebook                                     6.0.3-py36_0 --> 6.4.3-py36h06a4308_0
  openssl                                 1.1.1h-h7b6447c_0 --> 1.1.1l-h7f8727e_0
  pandoc                                          2.2.3.2-0 --> 2.12-h06a4308_0
  pandocfilters                                1.4.2-py36_1 --> 1.4.3-py36h06a4308_1
  parso                                          0.7.0-py_0 --> 0.8.2-pyhd3eb1b0_0
  pcre                                      8.43-he6710b0_0 --> 8.45-h295c915_0
  pexpect            pkgs/main/linux-64::pexpect-4.8.0-py3~ --> pkgs/main/noarch::pexpect-4.8.0-pyhd3eb1b0_3
  pickleshare        pkgs/main/linux-64::pickleshare-0.7.5~ --> pkgs/main/noarch::pickleshare-0.7.5-pyhd3eb1b0_1003
  pillow                               7.1.2-py36hb39fc2d_0 --> 8.3.1-py36h2c7a002_0
  pip                                         20.0.2-py36_3 --> 21.2.2-py36h06a4308_0
  pixman             conda-forge::pixman-0.38.0-h516909a_1~ --> pkgs/main::pixman-0.40.0-h7f8727e_1
  prometheus_client                              0.7.1-py_0 --> 0.12.0-pyhd3eb1b0_0
  prompt-toolkit                                 3.0.4-py_0 --> 3.0.20-pyhd3eb1b0_0
  prompt_toolkit                                    3.0.4-0 --> 3.0.20-hd3eb1b0_0
  ptyprocess         pkgs/main/linux-64::ptyprocess-0.6.0-~ --> pkgs/main/noarch::ptyprocess-0.7.0-pyhd3eb1b0_2
  pygments                                       2.6.1-py_0 --> 2.10.0-pyhd3eb1b0_0
  pyparsing          conda-forge::pyparsing-2.4.7-pyh9f0ad~ --> pkgs/main::pyparsing-3.0.4-pyhd3eb1b0_0
  pyrsistent                          0.16.0-py36h7b6447c_0 --> 0.17.3-py36h7b6447c_0
  python-dateutil                                2.8.1-py_0 --> 2.8.2-pyhd3eb1b0_0
  pytz                                          2020.1-py_0 --> 2021.3-pyhd3eb1b0_0
  pyzmq                               18.1.1-py36he6710b0_0 --> 22.2.1-py36h295c915_1
  qtconsole                                      4.7.4-py_0 --> 5.1.1-pyhd3eb1b0_0
  qtpy                                           1.9.0-py_0 --> 1.10.0-pyhd3eb1b0_0
  readline                                   8.0-h7b6447c_0 --> 8.1-h27cfd23_0
  scipy                                1.4.1-py36h0b6359f_0 --> 1.5.2-py36h0b6359f_0
  send2trash         pkgs/main/linux-64::send2trash-1.5.0-~ --> pkgs/main/noarch::send2trash-1.8.0-pyhd3eb1b0_1
  setuptools                                  46.4.0-py36_0 --> 58.0.4-py36h06a4308_0
  six                 pkgs/main/linux-64::six-1.14.0-py36_0 --> pkgs/main/noarch::six-1.16.0-pyhd3eb1b0_0
  sqlite                                  3.31.1-h62c20be_1 --> 3.37.0-hc218d9a_0
  statsmodels        conda-forge::statsmodels-0.11.1-py36h~ --> pkgs/main::statsmodels-0.12.2-py36h27cfd23_0
  terminado                                    0.8.3-py36_0 --> 0.9.4-py36h06a4308_0
  testpath                                       0.4.4-py_0 --> 0.5.0-pyhd3eb1b0_0
  tk                                       8.6.8-hbc83047_0 --> 8.6.11-h1ccaba5_0
  tornado                              6.0.4-py36h7b6447c_1 --> 6.1-py36h27cfd23_0
  wcwidth                                        0.1.9-py_0 --> 0.2.5-pyhd3eb1b0_0
  wheel              pkgs/main/linux-64::wheel-0.34.2-py36~ --> pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  zeromq                                   4.3.1-he6710b0_3 --> 4.3.4-h2531618_0
  zipp                                           3.1.0-py_0 --> 3.6.0-pyhd3eb1b0_0
  zlib                                    1.2.11-h7b6447c_3 --> 1.2.11-h7f8727e_4
  zstd                                     1.3.7-h0b5b093_0 --> 1.4.9-haebb681_0

The following packages will be SUPERSEDED by a higher-priority channel:

  bzip2                 conda-forge::bzip2-1.0.8-h516909a_2 --> pkgs/main::bzip2-1.0.8-h7b6447c_0
  freeglut           conda-forge::freeglut-3.0.0-hf484d3e_~ --> pkgs/main::freeglut-3.0.0-hf484d3e_5
  hdf5                  conda-forge::hdf5-1.10.2-hc401514_3 --> pkgs/main::hdf5-1.10.2-hba1933b_1
  libglu             conda-forge::libglu-9.0.0-he1b5a44_10~ --> pkgs/main::libglu-9.0.0-hf484d3e_1
  patsy                conda-forge/noarch::patsy-0.5.1-py_0 --> pkgs/main/linux-64::patsy-0.5.1-py36_0

The following packages will be DOWNGRADED:

  libuuid                                  1.0.3-h1bed415_2 --> 1.0.3-h7f8727e_2
  mkl-service                          2.3.0-py36he904b0f_0 --> 2.3.0-py36he8ac12f_0
  traitlets                                    4.3.3-py36_0 --> 4.3.3-py36h06a4308_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libstdcxx-ng-9.3.0   | 3.1 MB    | ########################################################## | 100% 
nbconvert-6.0.7      | 480 KB    | ########################################################## | 100% 
prompt_toolkit-3.0.2 | 12 KB     | ########################################################## | 100% 
libgomp-9.3.0        | 311 KB    | ########################################################## | 100% 
argon2-cffi-20.1.0   | 46 KB     | ########################################################## | 100% 
patsy-0.5.1          | 274 KB    | ########################################################## | 100% 
statsmodels-0.12.2   | 8.6 MB    | ########################################################## | 100% 
certifi-2021.5.30    | 139 KB    | ########################################################## | 100% 
jupyter_console-6.4. | 23 KB     | ########################################################## | 100% 
defusedxml-0.7.1     | 23 KB     | ########################################################## | 100% 
libtiff-4.2.0        | 502 KB    | ########################################################## | 100% 
pixman-0.40.0        | 373 KB    | ########################################################## | 100% 
ipython-7.16.1       | 999 KB    | ########################################################## | 100% 
pyparsing-3.0.4      | 81 KB     | ########################################################## | 100% 
backcall-0.2.0       | 13 KB     | ########################################################## | 100% 
jpeg-9d              | 232 KB    | ########################################################## | 100% 
_openmp_mutex-4.5    | 22 KB     | ########################################################## | 100% 
joblib-1.0.1         | 208 KB    | ########################################################## | 100% 
libxml2-2.9.12       | 1.2 MB    | ########################################################## | 100% 
ptyprocess-0.7.0     | 17 KB     | ########################################################## | 100% 
jsonschema-3.2.0     | 47 KB     | ########################################################## | 100% 
importlib_metadata-4 | 11 KB     | ########################################################## | 100% 
freetype-2.11.0      | 618 KB    | ########################################################## | 100% 
prometheus_client-0. | 47 KB     | ########################################################## | 100% 
expat-2.4.1          | 168 KB    | ########################################################## | 100% 
tornado-6.1          | 581 KB    | ########################################################## | 100% 
six-1.16.0           | 18 KB     | ########################################################## | 100% 
zeromq-4.3.4         | 331 KB    | ########################################################## | 100% 
pillow-8.3.1         | 637 KB    | ########################################################## | 100% 
jupyter_client-7.1.0 | 100 KB    | ########################################################## | 100% 
nbformat-5.1.3       | 44 KB     | ########################################################## | 100% 
python-dateutil-2.8. | 233 KB    | ########################################################## | 100% 
lcms2-2.12           | 312 KB    | ########################################################## | 100% 
send2trash-1.8.0     | 19 KB     | ########################################################## | 100% 
setuptools-58.0.4    | 788 KB    | ########################################################## | 100% 
zlib-1.2.11          | 108 KB    | ########################################################## | 100% 
scipy-1.5.2          | 14.4 MB   | ########################################################## | 100% 
hdf5-1.10.2          | 3.8 MB    | ########################################################## | 100% 
wheel-0.37.0         | 33 KB     | ########################################################## | 100% 
ninja-1.10.2         | 1.5 MB    | ########################################################## | 100% 
jasper-2.0.14        | 736 KB    | ########################################################## | 100% 
libuuid-1.0.3        | 17 KB     | ########################################################## | 100% 
openssl-1.1.1l       | 2.5 MB    | ########################################################## | 100% 
fontconfig-2.13.1    | 250 KB    | ########################################################## | 100% 
openjpeg-2.4.0       | 331 KB    | ########################################################## | 100% 
libgcc-ng-9.3.0      | 4.8 MB    | ########################################################## | 100% 
ld_impl_linux-64-2.3 | 586 KB    | ########################################################## | 100% 
jupyter_core-4.8.1   | 74 KB     | ########################################################## | 100% 
pygments-2.10.0      | 725 KB    | ########################################################## | 100% 
qtpy-1.10.0          | 35 KB     | ########################################################## | 100% 
intel-openmp-2021.4. | 4.2 MB    | ########################################################## | 100% 
lz4-c-1.9.3          | 185 KB    | ########################################################## | 100% 
markupsafe-2.0.1     | 21 KB     | ########################################################## | 100% 
sqlite-3.37.0        | 999 KB    | ########################################################## | 100% 
zstd-1.4.9           | 480 KB    | ########################################################## | 100% 
pip-21.2.2           | 1.8 MB    | ########################################################## | 100% 
pytz-2021.3          | 171 KB    | ########################################################## | 100% 
matplotlib-base-3.3. | 5.1 MB    | ########################################################## | 100% 
graphite2-1.3.14     | 99 KB     | ########################################################## | 100% 
nbclient-0.5.3       | 62 KB     | ########################################################## | 100% 
mkl_fft-1.3.0        | 170 KB    | ########################################################## | 100% 
typing_extensions-3. | 31 KB     | ########################################################## | 100% 
importlib-metadata-4 | 38 KB     | ########################################################## | 100% 
decorator-5.1.0      | 14 KB     | ########################################################## | 100% 
pandocfilters-1.4.3  | 14 KB     | ########################################################## | 100% 
parso-0.8.2          | 69 KB     | ########################################################## | 100% 
libglu-9.0.0         | 271 KB    | ########################################################## | 100% 
readline-8.1         | 362 KB    | ########################################################## | 100% 
terminado-0.9.4      | 25 KB     | ########################################################## | 100% 
jupyterlab_widgets-1 | 109 KB    | ########################################################## | 100% 
notebook-6.4.3       | 4.2 MB    | ########################################################## | 100% 
ncurses-6.3          | 782 KB    | ########################################################## | 100% 
pandoc-2.12          | 9.5 MB    | ########################################################## | 100% 
nest-asyncio-1.5.1   | 10 KB     | ########################################################## | 100% 
zipp-3.6.0           | 17 KB     | ########################################################## | 100% 
jinja2-3.0.2         | 110 KB    | ########################################################## | 100% 
packaging-21.3       | 36 KB     | ########################################################## | 100% 
tk-8.6.11            | 3.0 MB    | ########################################################## | 100% 
pcre-8.45            | 207 KB    | ########################################################## | 100% 
libgfortran-ng-7.5.0 | 22 KB     | ########################################################## | 100% 
pyrsistent-0.17.3    | 89 KB     | ########################################################## | 100% 
qtconsole-5.1.1      | 98 KB     | ########################################################## | 100% 
mkl-service-2.3.0    | 52 KB     | ########################################################## | 100% 
prompt-toolkit-3.0.2 | 259 KB    | ########################################################## | 100% 
pyzmq-22.2.1         | 454 KB    | ########################################################## | 100% 
testpath-0.5.0       | 81 KB     | ########################################################## | 100% 
libwebp-base-1.2.0   | 437 KB    | ########################################################## | 100% 
wcwidth-0.2.5        | 26 KB     | ########################################################## | 100% 
attrs-21.2.0         | 46 KB     | ########################################################## | 100% 
freeglut-3.0.0       | 176 KB    | ########################################################## | 100% 
cffi-1.14.0          | 223 KB    | ########################################################## | 100% 
bleach-4.0.0         | 113 KB    | ########################################################## | 100% 
kiwisolver-1.3.1     | 80 KB     | ########################################################## | 100% 
traitlets-4.3.3      | 138 KB    | ########################################################## | 100% 
ipykernel-5.3.4      | 181 KB    | ########################################################## | 100% 
libgfortran4-7.5.0   | 995 KB    | ########################################################## | 100% 
ca-certificates-2021 | 115 KB    | ########################################################## | 100% 
pycparser-2.21       | 94 KB     | ########################################################## | 100% 
cycler-0.11.0        | 12 KB     | ########################################################## | 100% 
ipywidgets-7.6.5     | 105 KB    | ########################################################## | 100% 
async_generator-1.10 | 39 KB     | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

ပြီးမှ conda နဲ့ matplotlib ကို ပြန် clean install လုပ်ခဲ့...   

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda install matplotlib
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: \ 
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::patsy==0.5.1=py36_0
  - defaults/linux-64::qt==5.9.7=h5867ecd_1
  - defaults/noarch::pytz==2021.3=pyhd3eb1b0_0
  - defaults/linux-64::harfbuzz==1.8.8=hffaf4a1_0
  - defaults/linux-64::libglu==9.0.0=hf484d3e_1
  - defaults/linux-64::readline==8.1=h27cfd23_0
  - defaults/linux-64::terminado==0.9.4=py36h06a4308_0
  - defaults/noarch::cycler==0.11.0=pyhd3eb1b0_0
  - defaults/linux-64::openssl==1.1.1l=h7f8727e_0
  - defaults/linux-64::pandocfilters==1.4.3=py36h06a4308_1
  - defaults/linux-64::scikit-learn==0.22.1=py36hd81dba3_0
  - defaults/linux-64::ipykernel==5.3.4=py36h5ca1d4c_0
  - defaults/linux-64::libvpx==1.7.0=h439df22_0
  - defaults/linux-64::freeglut==3.0.0=hf484d3e_5
  - defaults/noarch::nbclient==0.5.3=pyhd3eb1b0_0
  - defaults/linux-64::zstd==1.4.9=haebb681_0
  - pytorch/linux-64::torchvision==0.6.0=py36_cu102
  - defaults/linux-64::kiwisolver==1.3.1=py36h2531618_0
  - defaults/noarch::zipp==3.6.0=pyhd3eb1b0_0
  - defaults/noarch::jupyterlab_widgets==1.0.0=pyhd3eb1b0_1
  - defaults/noarch::jupyterlab_pygments==0.1.2=py_0
  - defaults/noarch::importlib_metadata==4.8.1=hd3eb1b0_0
  - defaults/linux-64::libgcc-ng==9.3.0=h5101ec6_17
  - defaults/linux-64::pyrsistent==0.17.3=py36h7b6447c_0
  - defaults/linux-64::lz4-c==1.9.3=h295c915_1
  - defaults/noarch::qtpy==1.10.0=pyhd3eb1b0_0
  - defaults/linux-64::certifi==2021.5.30=py36h06a4308_0
  - defaults/linux-64::expat==2.4.1=h2531618_2
  - defaults/noarch::pygments==2.10.0=pyhd3eb1b0_0
  - defaults/noarch::six==1.16.0=pyhd3eb1b0_0
  - defaults/noarch::bleach==4.0.0=pyhd3eb1b0_0
  - defaults/linux-64::dbus==1.13.18=hb2f20db_0
  - defaults/linux-64::argon2-cffi==20.1.0=py36h27cfd23_1
  - defaults/linux-64::jasper==2.0.14=hd8c5072_2
  - defaults/linux-64::hdf5==1.10.2=hba1933b_1
  - defaults/linux-64::webencodings==0.5.1=py36_1
  - defaults/linux-64::retrying==1.3.3=py36_2
  - defaults/linux-64::libxml2==2.9.12=h03d6c58_0
  - defaults/linux-64::olefile==0.46=py36_0
  - defaults/noarch::ipython_genutils==0.2.0=pyhd3eb1b0_1
  - defaults/linux-64::pyqt==5.9.2=py36h05f1152_2
  - defaults/linux-64::libuuid==1.0.3=h7f8727e_2
  - defaults/linux-64::jupyter==1.0.0=py36_7
  - defaults/linux-64::opencv==3.4.2=py36h6fd60c2_1
  - defaults/linux-64::pcre==8.45=h295c915_0
  - defaults/noarch::defusedxml==0.7.1=pyhd3eb1b0_0
  - defaults/linux-64::libopencv==3.4.2=hb342d67_1
  - defaults/linux-64::libgfortran-ng==7.5.0=ha8ba4b0_17
  - defaults/linux-64::libffi==3.2.1=hf484d3e_1007
  - defaults/linux-64::numpy==1.18.1=py36h4f9e942_0
  - defaults/linux-64::jupyter_core==4.8.1=py36h06a4308_0
  - defaults/noarch::jinja2==3.0.2=pyhd3eb1b0_0
  - defaults/linux-64::entrypoints==0.3=py36_0
  - defaults/linux-64::mkl-service==2.3.0=py36he8ac12f_0
  - defaults/noarch::ipywidgets==7.6.5=pyhd3eb1b0_1
  - defaults/linux-64::cffi==1.14.0=py36h2e261b9_0
  - defaults/linux-64::gst-plugins-base==1.14.0=hbbd80ab_1
  - defaults/linux-64::jpeg==9d=h7f8727e_0
  - defaults/linux-64::zlib==1.2.11=h7f8727e_4
  - defaults/linux-64::nbconvert==6.0.7=py36_0
  - defaults/noarch::pyparsing==3.0.4=pyhd3eb1b0_0
  - defaults/linux-64::libopus==1.3.1=h7b6447c_0
  - defaults/linux-64::py-opencv==3.4.2=py36hb342d67_1
  - defaults/linux-64::libpng==1.6.37=hbc83047_0
  - defaults/linux-64::sqlite==3.37.0=hc218d9a_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::markupsafe==2.0.1=py36h27cfd23_0
  - menpo/linux-64::opencv3==3.1.0=py36_0
  - defaults/noarch::ptyprocess==0.7.0=pyhd3eb1b0_2
  - defaults/linux-64::pillow==8.3.1=py36h2c7a002_0
  - defaults/linux-64::fontconfig==2.13.1=h6c09931_0
  - defaults/linux-64::ipython==7.16.1=py36h5ca1d4c_0
  - defaults/linux-64::icu==58.2=he6710b0_3
  - defaults/noarch::packaging==21.3=pyhd3eb1b0_0
  - defaults/linux-64::pip==21.2.2=py36h06a4308_0
  - defaults/noarch::testpath==0.5.0=pyhd3eb1b0_0
  - defaults/linux-64::sip==4.19.8=py36hf484d3e_0
  - defaults/linux-64::libxcb==1.14=h7b6447c_0
  - defaults/linux-64::numpy-base==1.18.1=py36hde5b4d6_1
  - defaults/linux-64::mistune==0.8.4=py36h7b6447c_0
  - defaults/linux-64::libstdcxx-ng==9.3.0=hd4cf53a_17
  - defaults/linux-64::setuptools==58.0.4=py36h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/noarch::wheel==0.37.0=pyhd3eb1b0_1
  - defaults/noarch::typing_extensions==3.10.0.2=pyh06a4308_0
  - defaults/noarch::jsonschema==3.2.0=pyhd3eb1b0_2
  - defaults/noarch::send2trash==1.8.0=pyhd3eb1b0_1
  - defaults/noarch::attrs==21.2.0=pyhd3eb1b0_0
  - defaults/noarch::plotly==4.6.0=py_0
  - defaults/linux-64::mkl_fft==1.3.0=py36h54f3939_0
  - defaults/noarch::joblib==1.0.1=pyhd3eb1b0_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::python==3.6.10=hcf32534_1
  - defaults/linux-64::pixman==0.40.0=h7f8727e_1
  - defaults/linux-64::mkl_random==1.1.1=py36h0573a6f_0
  - defaults/linux-64::libtiff==4.2.0=h85742a9_0
  - defaults/linux-64::traitlets==4.3.3=py36h06a4308_0
  - defaults/noarch::prometheus_client==0.12.0=pyhd3eb1b0_0
  - defaults/noarch::backcall==0.2.0=pyhd3eb1b0_0
  - defaults/linux-64::gstreamer==1.14.0=hb453b48_1
  - defaults/linux-64::libsodium==1.0.18=h7b6447c_0
  - defaults/noarch::prompt-toolkit==3.0.20=pyhd3eb1b0_0
  - defaults/noarch::decorator==5.1.0=pyhd3eb1b0_0
  - defaults/linux-64::tk==8.6.11=h1ccaba5_0
  - defaults/linux-64::async_generator==1.10=py36h28b3542_0
  - defaults/noarch::pexpect==4.8.0=pyhd3eb1b0_3
  - defaults/linux-64::notebook==6.4.3=py36h06a4308_0
  - defaults/linux-64::statsmodels==0.12.2=py36h27cfd23_0
  - defaults/linux-64::matplotlib-base==3.3.4=py36h62a2d02_0
  - defaults/noarch::wcwidth==0.2.5=pyhd3eb1b0_0
  - defaults/linux-64::cairo==1.14.12=h8948797_3
  - defaults/noarch::python-dateutil==2.8.2=pyhd3eb1b0_0
  - defaults/noarch::nbformat==5.1.3=pyhd3eb1b0_0
  - defaults/linux-64::ninja==1.10.2=h5e70eb0_2
  - defaults/noarch::pickleshare==0.7.5=pyhd3eb1b0_1003
  - defaults/linux-64::glib==2.63.1=h5a9c865_0
  - defaults/linux-64::jedi==0.17.0=py36_0
  - defaults/linux-64::freetype==2.11.0=h70c0345_0
  - defaults/noarch::prompt_toolkit==3.0.20=hd3eb1b0_0
  - defaults/linux-64::pyzmq==22.2.1=py36h295c915_1
  - defaults/linux-64::ncurses==6.3=h7f8727e_2
  - defaults/noarch::parso==0.8.2=pyhd3eb1b0_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - pytorch/linux-64::pytorch==1.5.0=py3.6_cuda10.2.89_cudnn7.6.5_0
  - defaults/linux-64::cudatoolkit==10.2.89=hfd86e86_1
  - defaults/noarch::nest-asyncio==1.5.1=pyhd3eb1b0_0
  - defaults/linux-64::tornado==6.1=py36h27cfd23_0
  - defaults/noarch::jupyter_client==7.1.0=pyhd3eb1b0_0
  - defaults/linux-64::widgetsnbextension==3.5.1=py36_0
  - defaults/linux-64::pandas==1.0.3=py36h0573a6f_0
  - defaults/linux-64::libwebp-base==1.2.0=h27cfd23_0
  - defaults/linux-64::ffmpeg==4.0=hcdf2ecd_0
  - defaults/noarch::qtconsole==5.1.1=pyhd3eb1b0_0
  - defaults/linux-64::zeromq==4.3.4=h2531618_0
  - defaults/linux-64::importlib-metadata==4.8.1=py36h06a4308_0
  - conda-forge/noarch::seaborn==0.10.1=py_0
  - defaults/linux-64::xz==5.2.5=h7b6447c_0
  - defaults/noarch::jupyter_console==6.4.0=pyhd3eb1b0_0
  - defaults/linux-64::graphite2==1.3.14=h23475e2_0
  - defaults/linux-64::scipy==1.5.2=py36h0b6359f_0
done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/conda3.6

  added / updated specs:
    - matplotlib


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    matplotlib-3.3.4           |   py36h06a4308_0          26 KB
    ------------------------------------------------------------
                                           Total:          26 KB

The following NEW packages will be INSTALLED:

  matplotlib         pkgs/main/linux-64::matplotlib-3.3.4-py36h06a4308_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
matplotlib-3.3.4     | 26 KB     | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

package inconsistance error တော့ ပေးနေတယ်....  
compare-mt ကို run လို့ ရမရ ပြန်ကြည့်ကြည့်မယ်....   

```
(conda3.6) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt example/ted.ref.eng example/ted.sys1.eng example/ted.sys2.eng --compare_scores score_type=bleu,bootstrap=1000 score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000 --compare_word_accuracies bucket_type=freq,freq_corpus_file=example/ted.train.eng bucket_type=label,ref_labels=example/ted.ref.eng.tag,out_labels="example/ted.sys1.eng.tag;example/ted.sys2.eng.tag",label_set=CC+DT+IN+JJ+NN+NNP+NNS+PRP+RB+TO+VB+VBP+VBZ --output_directory outputs --sys_names PBMT NMT
...
...
...
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 2512, in bar
    fmt='none', **error_kw)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/__init__.py", line 1447, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3453, in errorbar
    lower, upper = extract_err('y', yerr, y, lolims, uplims)
  File "/home/ye/tool/anaconda3/envs/conda3.6/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3404, in extract_err
    f"{name}err must be a scalar or a 1D or (2, n) array-like")
ValueError: yerr must be a scalar or a 1D or (2, n) array-like
```

same error ပဲ ပေးနေတယ်....   
အဲဒါနဲ့ conda uninstall matplotlib လုပ်ပြီး၊ pip install matplotlib လုပ်ကြည့်ခဲ့ပြီး compare-mt ကို ထပ် run ကြည့်ခဲ့လည်း same error ပဲ ပေးနေတယ်...  :(  

အဲဒါနဲ့ ကိုယ့်စက်ထဲမှာ environment အသစ် တစ်ခုဆောက်ပြီးတော့ setup run ဖို့ ဆုံးဖြတ်ခဲ့..  

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda create -n "compare-mt" python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/compare-mt

  added / updated specs:
    - python=3.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2021.10.8          |   py37h06a4308_0         151 KB
    pip-21.2.2                 |   py37h06a4308_0         1.8 MB
    python-3.7.11              |       h12debd9_0        45.3 MB
    setuptools-58.0.4          |   py37h06a4308_0         775 KB
    ------------------------------------------------------------
                                           Total:        48.0 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.10.26-h06a4308_2
  certifi            pkgs/main/linux-64::certifi-2021.10.8-py37h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py37h06a4308_0
  python             pkgs/main/linux-64::python-3.7.11-h12debd9_0
  readline           pkgs/main/linux-64::readline-8.1-h27cfd23_0
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py37h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.37.0-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7f8727e_4


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2021.10.8    | 151 KB    | ########################################################## | 100% 
setuptools-58.0.4    | 775 KB    | ########################################################## | 100% 
pip-21.2.2           | 1.8 MB    | ########################################################## | 100% 
python-3.7.11        | 45.3 MB   | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate compare-mt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda activate compare-mt
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

install required libaries ...   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install -r requirements.txt 
Requirement already satisfied: nltk>=3.2 in /home/ye/.local/lib/python3.7/site-packages (from -r requirements.txt (line 1)) (3.5)
Collecting numpy
  Downloading numpy-1.21.5-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (15.7 MB)
     |████████████████████████████████| 15.7 MB 16.4 MB/s 
Collecting matplotlib
  Downloading matplotlib-3.5.1-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (11.2 MB)
     |████████████████████████████████| 11.2 MB 17.9 MB/s 
Collecting absl-py
  Using cached absl_py-1.0.0-py3-none-any.whl (126 kB)
Collecting sacrebleu
  Using cached sacrebleu-2.0.0-py3-none-any.whl (90 kB)
Collecting langid
  Using cached langid-1.1.6.tar.gz (1.9 MB)
Collecting click
  Using cached click-8.0.3-py3-none-any.whl (97 kB)
Collecting joblib
  Downloading joblib-1.1.0-py2.py3-none-any.whl (306 kB)
     |████████████████████████████████| 306 kB 13.1 MB/s 
Collecting tqdm
  Downloading tqdm-4.62.3-py2.py3-none-any.whl (76 kB)
     |████████████████████████████████| 76 kB 3.0 MB/s 
Requirement already satisfied: regex in /home/ye/.local/lib/python3.7/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (2020.5.14)
Collecting cycler>=0.10
  Downloading cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pillow>=6.2.0
  Downloading Pillow-8.4.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
     |████████████████████████████████| 3.1 MB 10.0 MB/s 
Collecting fonttools>=4.22.0
  Downloading fonttools-4.28.5-py3-none-any.whl (890 kB)
     |████████████████████████████████| 890 kB 26.1 MB/s 
Collecting packaging>=20.0
  Downloading packaging-21.3-py3-none-any.whl (40 kB)
     |████████████████████████████████| 40 kB 4.2 MB/s 
Collecting python-dateutil>=2.7
  Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
     |████████████████████████████████| 247 kB 8.5 MB/s 
Collecting pyparsing>=2.2.1
  Downloading pyparsing-3.0.6-py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 4.7 MB/s 
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.3.2-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 13.0 MB/s 
Collecting six
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting tabulate>=0.8.9
  Using cached tabulate-0.8.9-py3-none-any.whl (25 kB)
Collecting colorama
  Using cached colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting portalocker
  Using cached portalocker-2.3.2-py2.py3-none-any.whl (15 kB)
Collecting importlib-metadata
  Downloading importlib_metadata-4.10.0-py3-none-any.whl (17 kB)
Collecting typing-extensions>=3.6.4
  Downloading typing_extensions-4.0.1-py3-none-any.whl (22 kB)
Collecting zipp>=0.5
  Downloading zipp-3.7.0-py3-none-any.whl (5.3 kB)
Building wheels for collected packages: langid
  Building wheel for langid (setup.py) ... done
  Created wheel for langid: filename=langid-1.1.6-py3-none-any.whl size=1941187 sha256=20f4122eccec190822b2a82872594b0b58e4b33ef80a93303bdfe6e949197d56
  Stored in directory: /home/ye/.cache/pip/wheels/2b/bb/7f/11e4db39477278161e882eadc46fb558949a28b13470fc74b8
Successfully built langid
Installing collected packages: zipp, typing-extensions, six, pyparsing, importlib-metadata, tqdm, tabulate, python-dateutil, portalocker, pillow, packaging, numpy, kiwisolver, joblib, fonttools, cycler, colorama, click, sacrebleu, matplotlib, langid, absl-py
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
mchmm 0.4.1 requires graphviz, which is not installed.
mchmm 0.4.1 requires scipy, which is not installed.
Successfully installed absl-py-1.0.0 click-8.0.3 colorama-0.4.4 cycler-0.11.0 fonttools-4.28.5 importlib-metadata-4.10.0 joblib-1.1.0 kiwisolver-1.3.2 langid-1.1.6 matplotlib-3.5.1 numpy-1.21.5 packaging-21.3 pillow-8.4.0 portalocker-2.3.2 pyparsing-3.0.6 python-dateutil-2.8.2 sacrebleu-2.0.0 six-1.16.0 tabulate-0.8.9 tqdm-4.62.3 typing-extensions-4.0.1 zipp-3.7.0
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install graphviz
Collecting graphviz
  Downloading graphviz-0.19.1-py3-none-any.whl (46 kB)
     |████████████████████████████████| 46 kB 268 kB/s 
Installing collected packages: graphviz
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
mchmm 0.4.1 requires scipy, which is not installed.
Successfully installed graphviz-0.19.1
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install scipy
Collecting scipy
  Downloading scipy-1.7.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (38.1 MB)
     |████████████████████████████████| 38.1 MB 8.5 MB/s 
Requirement already satisfied: numpy<1.23.0,>=1.16.5 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from scipy) (1.21.5)
Installing collected packages: scipy
Successfully installed scipy-1.7.3
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install -r requirements.txt 
Requirement already satisfied: nltk>=3.2 in /home/ye/.local/lib/python3.7/site-packages (from -r requirements.txt (line 1)) (3.5)
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from -r requirements.txt (line 2)) (1.21.5)
Requirement already satisfied: matplotlib in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from -r requirements.txt (line 3)) (3.5.1)
Requirement already satisfied: absl-py in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from -r requirements.txt (line 4)) (1.0.0)
Requirement already satisfied: sacrebleu in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from -r requirements.txt (line 5)) (2.0.0)
Requirement already satisfied: langid in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from -r requirements.txt (line 6)) (1.1.6)
Requirement already satisfied: click in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (8.0.3)
Requirement already satisfied: tqdm in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (4.62.3)
Requirement already satisfied: regex in /home/ye/.local/lib/python3.7/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (2020.5.14)
Requirement already satisfied: joblib in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (1.1.0)
Requirement already satisfied: fonttools>=4.22.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (4.28.5)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (1.3.2)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (2.8.2)
Requirement already satisfied: pillow>=6.2.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (8.4.0)
Requirement already satisfied: cycler>=0.10 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (0.11.0)
Requirement already satisfied: packaging>=20.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (21.3)
Requirement already satisfied: pyparsing>=2.2.1 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->-r requirements.txt (line 3)) (3.0.6)
Requirement already satisfied: six in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from absl-py->-r requirements.txt (line 4)) (1.16.0)
Requirement already satisfied: portalocker in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->-r requirements.txt (line 5)) (2.3.2)
Requirement already satisfied: colorama in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->-r requirements.txt (line 5)) (0.4.4)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->-r requirements.txt (line 5)) (0.8.9)
Requirement already satisfied: importlib-metadata in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from click->nltk>=3.2->-r requirements.txt (line 1)) (4.10.0)
Requirement already satisfied: zipp>=0.5 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from importlib-metadata->click->nltk>=3.2->-r requirements.txt (line 1)) (3.7.0)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from importlib-metadata->click->nltk>=3.2->-r requirements.txt (line 1)) (4.0.1)
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

run setup.py ...   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ python setup.py install
running install
running bdist_egg
running egg_info
writing compare_mt.egg-info/PKG-INFO
writing dependency_links to compare_mt.egg-info/dependency_links.txt
writing entry points to compare_mt.egg-info/entry_points.txt
writing requirements to compare_mt.egg-info/requires.txt
writing top-level names to compare_mt.egg-info/top_level.txt
reading manifest file 'compare_mt.egg-info/SOURCES.txt'
adding license file 'LICENSE'
writing manifest file 'compare_mt.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_scorers.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_repetition_utils.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/__init__.py -> build/bdist.linux-x86_64/egg/tests
creating build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/stat_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/sign_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/scorers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/reporters.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/repetition_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/print_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/ngram_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/formatting.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/corpus_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_mt_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_ll_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/bucketers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/arg_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/align_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt
creating build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/tokenizer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/scoring.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge_scorer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/io.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
byte-compiling build/bdist.linux-x86_64/egg/tests/test_scorers.py to test_scorers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/test_repetition_utils.py to test_repetition_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/stat_utils.py to stat_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/sign_utils.py to sign_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/scorers.py to scorers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/reporters.py to reporters.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/repetition_utils.py to repetition_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/print_utils.py to print_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/ngram_utils.py to ngram_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/formatting.py to formatting.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/corpus_utils.py to corpus_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_mt_main.py to compare_mt_main.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_ll_main.py to compare_ll_main.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/bucketers.py to bucketers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/arg_utils.py to arg_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/align_utils.py to align_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/tokenizer.py to tokenizer.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/scoring.py to scoring.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge_scorer.py to rouge_scorer.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge.py to rouge.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/io.py to io.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/__init__.py to __init__.cpython-37.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
tests.__pycache__.test_repetition_utils.cpython-37: module references __file__
tests.__pycache__.test_scorers.cpython-37: module references __file__
creating 'dist/compare_mt-0.2.4-py3.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing compare_mt-0.2.4-py3.7.egg
creating /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg
Extracting compare_mt-0.2.4-py3.7.egg to /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Adding compare-mt 0.2.4 to easy-install.pth file
Installing compare-ll script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing compare-mt script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Installed /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg
Processing dependencies for compare-mt==0.2.4
Searching for whatthelang
Reading https://pypi.org/simple/whatthelang/
Downloading https://files.pythonhosted.org/packages/8a/28/2abb6e71271e91eaf67fc2279f1abbae3a0200122c71fb1db518717909ae/whatthelang-1.0.1.tar.gz#sha256=75d8be322d8916c197e5f3761d15812e0601974fcbc1c80eb93af297d4ebdfd4
Best match: whatthelang 1.0.1
Processing whatthelang-1.0.1.tar.gz
Writing /tmp/easy_install-fk2s4lag/whatthelang-1.0.1/setup.cfg
Running whatthelang-1.0.1/setup.py -q bdist_egg --dist-dir /tmp/easy_install-fk2s4lag/whatthelang-1.0.1/egg-dist-tmp-dany9agt
zip_safe flag not set; analyzing archive contents...
whatthelang.__pycache__.predict_lang.cpython-37: module references __file__
whatthelang.__pycache__.test_predict_lang.cpython-37: module references __file__
creating /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/whatthelang-1.0.1-py3.7.egg
Extracting whatthelang-1.0.1-py3.7.egg to /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Adding whatthelang 1.0.1 to easy-install.pth file

Installed /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/whatthelang-1.0.1-py3.7.egg
Searching for pyfasttext
Reading https://pypi.org/simple/pyfasttext/
Downloading https://files.pythonhosted.org/packages/f5/ef/90606442481d1e4ab10eba8c2b2c449ceaa70c60e9b8d5898bb7504e3634/pyfasttext-0.4.6.tar.gz#sha256=aeb56569b5b47e958e5eeca3576047d666a495a5cc23010b0a503001d68b3390
Best match: pyfasttext 0.4.6
Processing pyfasttext-0.4.6.tar.gz
Writing /tmp/easy_install-3j7wy7o4/pyfasttext-0.4.6/setup.cfg
Running pyfasttext-0.4.6/setup.py -q bdist_egg --dist-dir /tmp/easy_install-3j7wy7o4/pyfasttext-0.4.6/egg-dist-tmp-opyufdnn
Traceback (most recent call last):
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 156, in save_modules
    yield saved
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 198, in setup_context
    yield
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 259, in run_setup
    _execfile(setup_script, ns)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 46, in _execfile
    exec(code, globals, locals)
  File "/tmp/easy_install-3j7wy7o4/pyfasttext-0.4.6/setup.py", line 3, in <module>
    import codecs
ModuleNotFoundError: No module named 'Cython'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "setup.py", line 60, in <module>
    include_package_data=True,
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/__init__.py", line 153, in setup
    return distutils.core.setup(**attrs)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/distutils/core.py", line 148, in setup
    dist.run_commands()
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/distutils/dist.py", line 966, in run_commands
    self.run_command(cmd)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/distutils/dist.py", line 985, in run_command
    cmd_obj.run()
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/install.py", line 67, in run
    self.do_egg_install()
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/install.py", line 117, in do_egg_install
    cmd.run(show_deprecation=False)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 408, in run
    self.easy_install(spec, not self.no_deps)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 650, in easy_install
    return self.install_item(None, spec, tmpdir, deps, True)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 697, in install_item
    self.process_distribution(spec, dist, deps)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 745, in process_distribution
    [requirement], self.local_index, self.easy_install
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/pkg_resources/__init__.py", line 768, in resolve
    replace_conflicting=replace_conflicting
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/pkg_resources/__init__.py", line 1051, in best_match
    return self.obtain(req, installer)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/pkg_resources/__init__.py", line 1063, in obtain
    return installer(requirement)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 669, in easy_install
    return self.install_item(spec, dist.location, tmpdir, deps)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 695, in install_item
    dists = self.install_eggs(spec, download, tmpdir)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 890, in install_eggs
    return self.build_and_install(setup_script, setup_base)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 1162, in build_and_install
    self.run_setup(setup_script, setup_base, args)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/command/easy_install.py", line 1146, in run_setup
    run_setup(setup_script, args)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 262, in run_setup
    raise
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/contextlib.py", line 130, in __exit__
    self.gen.throw(type, value, traceback)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 198, in setup_context
    yield
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/contextlib.py", line 130, in __exit__
    self.gen.throw(type, value, traceback)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 169, in save_modules
    saved_exc.resume()
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 143, in resume
    raise exc.with_traceback(self._tb)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 156, in save_modules
    yield saved
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 198, in setup_context
    yield
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 259, in run_setup
    _execfile(setup_script, ns)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/setuptools/sandbox.py", line 46, in _execfile
    exec(code, globals, locals)
  File "/tmp/easy_install-3j7wy7o4/pyfasttext-0.4.6/setup.py", line 3, in <module>
    import codecs
ModuleNotFoundError: No module named 'Cython'
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install Cython
Collecting Cython
  Downloading Cython-0.29.26-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
     |████████████████████████████████| 1.9 MB 1.8 MB/s 
Installing collected packages: Cython
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
whatthelang 1.0.1 requires cysignals, which is not installed.
whatthelang 1.0.1 requires pyfasttext, which is not installed.
Successfully installed Cython-0.29.26
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install cysignals
Collecting cysignals
  Downloading cysignals-1.11.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (871 kB)
     |████████████████████████████████| 871 kB 1.3 MB/s 
Requirement already satisfied: Cython>=0.28 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from cysignals) (0.29.26)
Installing collected packages: cysignals
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
whatthelang 1.0.1 requires pyfasttext, which is not installed.
Successfully installed cysignals-1.11.2
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install pyfasttext
Collecting pyfasttext
  Using cached pyfasttext-0.4.6.tar.gz (244 kB)
Collecting future
  Using cached future-0.18.2-py3-none-any.whl
Requirement already satisfied: cysignals in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from pyfasttext) (1.11.2)
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from pyfasttext) (1.21.5)
Requirement already satisfied: Cython>=0.28 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from cysignals->pyfasttext) (0.29.26)
Building wheels for collected packages: pyfasttext
  Building wheel for pyfasttext (setup.py) ... done
  Created wheel for pyfasttext: filename=pyfasttext-0.4.6-cp37-cp37m-linux_x86_64.whl size=2142288 sha256=427738143bd8b747665e97ad29d3efae5f5a4cadb9fdefb3868ff1401098363b
  Stored in directory: /home/ye/.cache/pip/wheels/e6/e7/60/c4506ea3173416f3774e221bd741d06bfc2127ec23ceff6619
Successfully built pyfasttext
Installing collected packages: future, pyfasttext
Successfully installed future-0.18.2 pyfasttext-0.4.6
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install Cython
Requirement already satisfied: Cython in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (0.29.26)
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ 
```

setup.py ကို ပြန် run ခဲ့...   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ python setup.py install
running install
running bdist_egg
running egg_info
writing compare_mt.egg-info/PKG-INFO
writing dependency_links to compare_mt.egg-info/dependency_links.txt
writing entry points to compare_mt.egg-info/entry_points.txt
writing requirements to compare_mt.egg-info/requires.txt
writing top-level names to compare_mt.egg-info/top_level.txt
reading manifest file 'compare_mt.egg-info/SOURCES.txt'
adding license file 'LICENSE'
writing manifest file 'compare_mt.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_scorers.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/test_repetition_utils.py -> build/bdist.linux-x86_64/egg/tests
copying build/lib/tests/__init__.py -> build/bdist.linux-x86_64/egg/tests
creating build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/stat_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/sign_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/scorers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/reporters.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/repetition_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/print_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/ngram_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/formatting.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/corpus_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_mt_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/compare_ll_main.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/bucketers.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/arg_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/align_utils.py -> build/bdist.linux-x86_64/egg/compare_mt
copying build/lib/compare_mt/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt
creating build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/tokenizer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/scoring.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge_scorer.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/rouge.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/io.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
copying build/lib/compare_mt/rouge/__init__.py -> build/bdist.linux-x86_64/egg/compare_mt/rouge
byte-compiling build/bdist.linux-x86_64/egg/tests/test_scorers.py to test_scorers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/test_repetition_utils.py to test_repetition_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/tests/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/stat_utils.py to stat_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/sign_utils.py to sign_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/scorers.py to scorers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/reporters.py to reporters.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/repetition_utils.py to repetition_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/print_utils.py to print_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/ngram_utils.py to ngram_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/formatting.py to formatting.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/corpus_utils.py to corpus_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_mt_main.py to compare_mt_main.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/compare_ll_main.py to compare_ll_main.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/bucketers.py to bucketers.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/arg_utils.py to arg_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/align_utils.py to align_utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/tokenizer.py to tokenizer.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/scoring.py to scoring.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge_scorer.py to rouge_scorer.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/rouge.py to rouge.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/io.py to io.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/compare_mt/rouge/__init__.py to __init__.cpython-37.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying compare_mt.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
tests.__pycache__.test_repetition_utils.cpython-37: module references __file__
tests.__pycache__.test_scorers.cpython-37: module references __file__
creating 'dist/compare_mt-0.2.4-py3.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing compare_mt-0.2.4-py3.7.egg
removing '/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg' (and everything under it)
creating /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg
Extracting compare_mt-0.2.4-py3.7.egg to /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
compare-mt 0.2.4 is already the active version in easy-install.pth
Installing compare-ll script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing compare-mt script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Installed /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg
Processing dependencies for compare-mt==0.2.4
Searching for whatthelang==1.0.1
Best match: whatthelang 1.0.1
Processing whatthelang-1.0.1-py3.7.egg
whatthelang 1.0.1 is already the active version in easy-install.pth

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/whatthelang-1.0.1-py3.7.egg
Searching for langid==1.1.6
Best match: langid 1.1.6
Adding langid 1.1.6 to easy-install.pth file
Installing langid script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for sacrebleu==2.0.0
Best match: sacrebleu 2.0.0
Adding sacrebleu 2.0.0 to easy-install.pth file
Installing sacrebleu script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for absl-py==1.0.0
Best match: absl-py 1.0.0
Adding absl-py 1.0.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for matplotlib==3.5.1
Best match: matplotlib 3.5.1
Adding matplotlib 3.5.1 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for numpy==1.21.5
Best match: numpy 1.21.5
Adding numpy 1.21.5 to easy-install.pth file
Installing f2py script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing f2py3 script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing f2py3.7 script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for nltk==3.5
Best match: nltk 3.5
Adding nltk 3.5 to easy-install.pth file
Installing nltk script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/.local/lib/python3.7/site-packages
Searching for pyfasttext==0.4.6
Best match: pyfasttext 0.4.6
Adding pyfasttext 0.4.6 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for cysignals==1.11.2
Best match: cysignals 1.11.2
Adding cysignals 1.11.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for Cython==0.29.26
Best match: Cython 0.29.26
Adding Cython 0.29.26 to easy-install.pth file
Installing cygdb script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing cython script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing cythonize script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for colorama==0.4.4
Best match: colorama 0.4.4
Adding colorama 0.4.4 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for portalocker==2.3.2
Best match: portalocker 2.3.2
Adding portalocker 2.3.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for tabulate==0.8.9
Best match: tabulate 0.8.9
Adding tabulate 0.8.9 to easy-install.pth file
Installing tabulate script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for regex==2020.5.14
Best match: regex 2020.5.14
Adding regex 2020.5.14 to easy-install.pth file

Using /home/ye/.local/lib/python3.7/site-packages
Searching for six==1.16.0
Best match: six 1.16.0
Adding six 1.16.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for pyparsing==3.0.6
Best match: pyparsing 3.0.6
Adding pyparsing 3.0.6 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for kiwisolver==1.3.2
Best match: kiwisolver 1.3.2
Adding kiwisolver 1.3.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for python-dateutil==2.8.2
Best match: python-dateutil 2.8.2
Adding python-dateutil 2.8.2 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for Pillow==8.4.0
Best match: Pillow 8.4.0
Adding Pillow 8.4.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for packaging==21.3
Best match: packaging 21.3
Adding packaging 21.3 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for fonttools==4.28.5
Best match: fonttools 4.28.5
Adding fonttools 4.28.5 to easy-install.pth file
Installing fonttools script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing pyftmerge script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing pyftsubset script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing ttx script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for cycler==0.11.0
Best match: cycler 0.11.0
Adding cycler 0.11.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for joblib==1.1.0
Best match: joblib 1.1.0
Adding joblib 1.1.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for tqdm==4.62.3
Best match: tqdm 4.62.3
Adding tqdm 4.62.3 to easy-install.pth file
Installing tqdm script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for click==8.0.3
Best match: click 8.0.3
Adding click 8.0.3 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for future==0.18.2
Best match: future 0.18.2
Adding future 0.18.2 to easy-install.pth file
Installing futurize script to /home/ye/tool/anaconda3/envs/compare-mt/bin
Installing pasteurize script to /home/ye/tool/anaconda3/envs/compare-mt/bin

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for importlib-metadata==4.10.0
Best match: importlib-metadata 4.10.0
Adding importlib-metadata 4.10.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for zipp==3.7.0
Best match: zipp 3.7.0
Adding zipp 3.7.0 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Searching for typing-extensions==4.0.1
Best match: typing-extensions 4.0.1
Adding typing-extensions 4.0.1 to easy-install.pth file

Using /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages
Finished processing dependencies for compare-mt==0.2.4
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ 

```

compare-mt ကို ထပ် run ခဲ့...  error ပေးနေဆဲ...   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt example/ted.ref.eng example/ted.sys1.eng example/ted.sys2.eng --compare_scores score_type=bleu,bootstrap=1000 score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000 --compare_word_accuracies bucket_type=freq,freq_corpus_file=example/ted.train.eng bucket_type=label,ref_labels=example/ted.ref.eng.tag,out_labels="example/ted.sys1.eng.tag;example/ted.sys2.eng.tag",label_set=CC+DT+IN+JJ+NN+NNP+NNS+PRP+RB+TO+VB+VBP+VBZ --output_directory outputs --sys_names PBMT NMT
...
...
...
g/compare_mt/reporters.py", line 208, in plot
    xticklabels=xticklabels)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt-0.2.4-py3.7.egg/compare_mt/reporters.py", line 79, in make_bar_chart
    bars.append(ax.bar(ind+i*width, data, width, color=bar_colors[i], bottom=0, yerr=err))
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/matplotlib/__init__.py", line 1412, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/matplotlib/axes/_axes.py", line 2427, in bar
    fmt='none', **error_kw)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/matplotlib/__init__.py", line 1412, in inner
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/matplotlib/axes/_axes.py", line 3460, in errorbar
    f"'{dep_axis}' (shape: {np.shape(dep)})") from None
ValueError: 'yerr' (shape: (1, 2)) must be a scalar or a 1D or (2, n) array-like whose shape matches 'y' (shape: (1,))
```

အဆင်မပြေဘူး...  
compare-mt ကို released လုပ်ခဲ့တာက 2018 လောက်က ဆိုတော့ အဲဒီတုန်းက ရှိတဲ့ python version ကိုပဲအခြေခံပြီး environment ပြင်ကြည့်ဖို့ စဉ်းစားခဲ့.... 
အရင်ဆုံး လက်ရှိ compare-mt Python env ကို remove လုပ်ခဲ့တယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda env remove --name compare-mt

Remove all packages in environment /home/ye/tool/anaconda3/envs/compare-mt:

(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

compare-mt environment အသစ်ကို အောက်ပါအတိုင်း ဆောက်ခဲ့...  

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda create --name compare-mt python=3.6.8
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/compare-mt

  added / updated specs:
    - python=3.6.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libedit-3.1.20210910       |       h7f8727e_0         166 KB
    python-3.6.8               |       h0371630_0        30.1 MB
    ------------------------------------------------------------
                                           Total:        30.3 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.10.26-h06a4308_2
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py36h06a4308_0
  libedit            pkgs/main/linux-64::libedit-3.1.20210910-h7f8727e_0
  libffi             pkgs/main/linux-64::libffi-3.2.1-hf484d3e_1007
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.8-h0371630_0
  readline           pkgs/main/linux-64::readline-7.0-h7b6447c_5
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.33.0-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7f8727e_4


Proceed ([y]/n)? y


Downloading and Extracting Packages
libedit-3.1.20210910 | 166 KB    | ########################################################## | 100% 
python-3.6.8         | 30.1 MB   | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate compare-mt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda activate compare-mt
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

install requirements.txt   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install -r requirements.txt 
Collecting nltk>=3.2
  Using cached nltk-3.6.7-py3-none-any.whl (1.5 MB)
Collecting numpy
  Downloading numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
     |████████████████████████████████| 14.8 MB 11.2 MB/s 
Collecting matplotlib
  Using cached matplotlib-3.3.4-cp36-cp36m-manylinux1_x86_64.whl (11.5 MB)
Collecting absl-py
  Using cached absl_py-1.0.0-py3-none-any.whl (126 kB)
Collecting sacrebleu
  Using cached sacrebleu-2.0.0-py3-none-any.whl (90 kB)
Collecting langid
  Using cached langid-1.1.6-py3-none-any.whl
Collecting click
  Using cached click-8.0.3-py3-none-any.whl (97 kB)
Collecting tqdm
  Using cached tqdm-4.62.3-py2.py3-none-any.whl (76 kB)
Collecting regex>=2021.8.3
  Using cached regex-2021.11.10-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (748 kB)
Requirement already satisfied: joblib in /home/ye/.local/lib/python3.6/site-packages (from nltk>=3.2->-r requirements.txt (line 1)) (0.15.1)
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (2.8.1)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib->-r requirements.txt (line 3)) (2.4.7)
Collecting pillow>=6.2.0
  Downloading Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
     |████████████████████████████████| 3.1 MB 10.4 MB/s 
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (1.1 MB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Requirement already satisfied: six in /home/ye/.local/lib/python3.6/site-packages (from absl-py->-r requirements.txt (line 4)) (1.15.0)
Collecting tabulate>=0.8.9
  Using cached tabulate-0.8.9-py3-none-any.whl (25 kB)
Collecting portalocker
  Using cached portalocker-2.3.2-py2.py3-none-any.whl (15 kB)
Collecting colorama
  Using cached colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting importlib-metadata
  Downloading importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Collecting zipp>=0.5
  Downloading zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-4.0.1-py3-none-any.whl (22 kB)
Installing collected packages: zipp, typing-extensions, importlib-metadata, tqdm, tabulate, regex, portalocker, pillow, numpy, kiwisolver, cycler, colorama, click, sacrebleu, nltk, matplotlib, langid, absl-py
Successfully installed absl-py-1.0.0 click-8.0.3 colorama-0.4.4 cycler-0.11.0 importlib-metadata-4.8.3 kiwisolver-1.3.1 langid-1.1.6 matplotlib-3.3.4 nltk-3.6.7 numpy-1.19.5 pillow-8.4.0 portalocker-2.3.2 regex-2021.11.10 sacrebleu-2.0.0 tabulate-0.8.9 tqdm-4.62.3 typing-extensions-4.0.1 zipp-3.6.0
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$
```

python setup.py install   
pip install Cython  
pip install cysignals  
pip install pyfasttext  

python setup.py install  

လုပ်ခဲ့ပြီး compare-mt example command ကို run ကြည့်ခဲ့ပေမဲ့ error ပေးနေဆဲ...   

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt example/ted.ref.eng example/ted.sys1.eng example/ted.sys2.eng --compare_scores score_type=bleu,bootstrap=1000 score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000 --compare_word_accuracies bucket_type=freq,freq_corpus_file=example/ted.train.eng bucket_type=label,ref_labels=example/ted.ref.eng.tag,out_labels="example/ted.sys1.eng.tag;example/ted.sys2.eng.tag",label_set=CC+DT+IN+JJ+NN+NNP+NNS+PRP+RB+TO+VB+VBP+VBZ --output_directory outputs --sys_names PBMT NMT
...
...
...
    return func(ax, *map(sanitize_sequence, args), **kwargs)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3453, in errorbar
    lower, upper = extract_err('y', yerr, y, lolims, uplims)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.6/site-packages/matplotlib/axes/_axes.py", line 3404, in extract_err
    f"{name}err must be a scalar or a 1D or (2, n) array-like")
ValueError: yerr must be a scalar or a 1D or (2, n) array-like
```

ဘာလဲကွာ?! ...  

## Installation of compare-mt Success

environment အသစ်ကို python version 3.7 နဲ့ဆောက်ခဲ့...  
setup.py ကို run တာမဟုတ်ပဲနဲ့ လက်ရှိ ရှိပြီးသား python env အပေါ်မှာပဲ pip install compare-mt ကိုသုံးပြီးလုပ်တဲ့ option လည်း ရှိလို့ ဒီတစ်ခေါက်တော့ အဲဒါနဲ့ သွားကြည့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda create --name compare-mt python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/compare-mt

  added / updated specs:
    - python=3.7


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.10.26-h06a4308_2
  certifi            pkgs/main/linux-64::certifi-2021.10.8-py37h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py37h06a4308_0
  python             pkgs/main/linux-64::python-3.7.11-h12debd9_0
  readline           pkgs/main/linux-64::readline-8.1-h27cfd23_0
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py37h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.37.0-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7f8727e_4


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate compare-mt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ conda activate compare-mt
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install compare-mt 
Collecting compare-mt
  Downloading compare_mt-0.2.8.tar.gz (43 kB)
     |████████████████████████████████| 43 kB 474 kB/s 
    ERROR: Command errored out with exit status 1:
     command: /home/ye/tool/anaconda3/envs/compare-mt/bin/python -c 'import io, os, sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/setup.py'"'"'; __file__='"'"'/tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/setup.py'"'"';f = getattr(tokenize, '"'"'open'"'"', open)(__file__) if os.path.exists(__file__) else io.StringIO('"'"'from setuptools import setup; setup()'"'"');code = f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base /tmp/pip-pip-egg-info-esq1owkc
         cwd: /tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/
    Complete output (9 lines):
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/setup.py", line 4, in <module>
        import compare_mt
      File "/tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/compare_mt/__init__.py", line 4, in <module>
        import compare_mt.sign_utils
      File "/tmp/pip-install-2gf8m6k6/compare-mt_55697a6d8c044cfa86b13aa29bbefb2d/compare_mt/sign_utils.py", line 13, in <module>
        import numpy as np
    ModuleNotFoundError: No module named 'numpy'
    ----------------------------------------
WARNING: Discarding https://files.pythonhosted.org/packages/e9/4c/e18ea230d656e273a1dd8a0fcea74154ebb343ea471dce7e95a6cd74ed7d/compare_mt-0.2.8.tar.gz#sha256=5aca950d5fe44f351fe81d10737dd7b58fd957a7e938e322e120aed3f3c696ca (from https://pypi.org/simple/compare-mt/). Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.
  Downloading compare_mt-0.2.7.tar.gz (41 kB)
     |████████████████████████████████| 41 kB 104 kB/s 
Requirement already satisfied: nltk>=3.2 in /home/ye/.local/lib/python3.7/site-packages (from compare-mt) (3.5)
Collecting numpy
  Using cached numpy-1.21.5-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (15.7 MB)
Collecting matplotlib
  Using cached matplotlib-3.5.1-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (11.2 MB)
Collecting absl-py
  Using cached absl_py-1.0.0-py3-none-any.whl (126 kB)
Collecting sacrebleu
  Using cached sacrebleu-2.0.0-py3-none-any.whl (90 kB)
Requirement already satisfied: regex in /home/ye/.local/lib/python3.7/site-packages (from nltk>=3.2->compare-mt) (2020.5.14)
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting click
  Using cached click-8.0.3-py3-none-any.whl (97 kB)
Collecting tqdm
  Using cached tqdm-4.62.3-py2.py3-none-any.whl (76 kB)
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting importlib-metadata
  Using cached importlib_metadata-4.10.0-py3-none-any.whl (17 kB)
Collecting zipp>=0.5
  Using cached zipp-3.7.0-py3-none-any.whl (5.3 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-4.0.1-py3-none-any.whl (22 kB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pillow>=6.2.0
  Using cached Pillow-8.4.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.3.2-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
Collecting fonttools>=4.22.0
  Using cached fonttools-4.28.5-py3-none-any.whl (890 kB)
Collecting python-dateutil>=2.7
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pyparsing>=2.2.1
  Using cached pyparsing-3.0.6-py3-none-any.whl (97 kB)
Collecting packaging>=20.0
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting colorama
  Using cached colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting tabulate>=0.8.9
  Using cached tabulate-0.8.9-py3-none-any.whl (25 kB)
Collecting portalocker
  Using cached portalocker-2.3.2-py2.py3-none-any.whl (15 kB)
Building wheels for collected packages: compare-mt
  Building wheel for compare-mt (setup.py) ... done
  Created wheel for compare-mt: filename=compare_mt-0.2.7-py3-none-any.whl size=50090 sha256=81693e620ed82004b540b22b0c859aa46fa5df4a2c20dbe8ec2f6314aa7faeee
  Stored in directory: /home/ye/.cache/pip/wheels/d4/ac/7b/2022bf2c5c733c2fe8250d4cbc3306a4c2aae4bfc86782896d
Successfully built compare-mt
Installing collected packages: zipp, typing-extensions, six, pyparsing, importlib-metadata, tqdm, tabulate, python-dateutil, portalocker, pillow, packaging, numpy, kiwisolver, joblib, fonttools, cycler, colorama, click, sacrebleu, matplotlib, absl-py, compare-mt
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
mchmm 0.4.1 requires graphviz, which is not installed.
mchmm 0.4.1 requires scipy, which is not installed.
Successfully installed absl-py-1.0.0 click-8.0.3 colorama-0.4.4 compare-mt-0.2.7 cycler-0.11.0 fonttools-4.28.5 importlib-metadata-4.10.0 joblib-1.1.0 kiwisolver-1.3.2 matplotlib-3.5.1 numpy-1.21.5 packaging-21.3 pillow-8.4.0 portalocker-2.3.2 pyparsing-3.0.6 python-dateutil-2.8.2 sacrebleu-2.0.0 six-1.16.0 tabulate-0.8.9 tqdm-4.62.3 typing-extensions-4.0.1 zipp-3.7.0
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ 
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install numpy
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (1.21.5)
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install graphviz
Collecting graphviz
  Using cached graphviz-0.19.1-py3-none-any.whl (46 kB)
Installing collected packages: graphviz
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
mchmm 0.4.1 requires scipy, which is not installed.
Successfully installed graphviz-0.19.1
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install scipy
Collecting scipy
  Using cached scipy-1.7.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (38.1 MB)
Requirement already satisfied: numpy<1.23.0,>=1.16.5 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from scipy) (1.21.5)
Installing collected packages: scipy
Successfully installed scipy-1.7.3
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ pip install compare-mt 
Requirement already satisfied: compare-mt in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (0.2.7)
Requirement already satisfied: absl-py in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from compare-mt) (1.0.0)
Requirement already satisfied: sacrebleu in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from compare-mt) (2.0.0)
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from compare-mt) (1.21.5)
Requirement already satisfied: matplotlib in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from compare-mt) (3.5.1)
Requirement already satisfied: nltk>=3.2 in /home/ye/.local/lib/python3.7/site-packages (from compare-mt) (3.5)
Requirement already satisfied: tqdm in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->compare-mt) (4.62.3)
Requirement already satisfied: click in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->compare-mt) (8.0.3)
Requirement already satisfied: regex in /home/ye/.local/lib/python3.7/site-packages (from nltk>=3.2->compare-mt) (2020.5.14)
Requirement already satisfied: joblib in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from nltk>=3.2->compare-mt) (1.1.0)
Requirement already satisfied: six in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from absl-py->compare-mt) (1.16.0)
Requirement already satisfied: importlib-metadata in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from click->nltk>=3.2->compare-mt) (4.10.0)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from importlib-metadata->click->nltk>=3.2->compare-mt) (4.0.1)
Requirement already satisfied: zipp>=0.5 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from importlib-metadata->click->nltk>=3.2->compare-mt) (3.7.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (1.3.2)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (2.8.2)
Requirement already satisfied: fonttools>=4.22.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (4.28.5)
Requirement already satisfied: pillow>=6.2.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (8.4.0)
Requirement already satisfied: packaging>=20.0 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (21.3)
Requirement already satisfied: pyparsing>=2.2.1 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (3.0.6)
Requirement already satisfied: cycler>=0.10 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from matplotlib->compare-mt) (0.11.0)
Requirement already satisfied: colorama in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->compare-mt) (0.4.4)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->compare-mt) (0.8.9)
Requirement already satisfied: portalocker in /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages (from sacrebleu->compare-mt) (2.3.2)
```

compare-mt ကို example command နဲ့ run ကြည့်ခဲ့...  

```
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ compare-mt example/ted.ref.eng \
example/ted.sys1.eng example/ted.sys2.eng --compare_scores score_type=bleu,bootstrap=1000 \
score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000\
--compare_word_accuracies bucket_type=freq,freq_corpus_file=example/ted.train.eng\
bucket_type=label,ref_labels=example/ted.ref.eng.tag,out_labels="example/ted.sys1.eng.tag;example/ted.sys2.eng.tag",\
label_set=CC+DT+IN+JJ+NN+NNP+NNS+PRP+RB+TO+VB+VBP+VBZ \
--output_directory outputs --sys_names PBMT NMT
********************** Aggregate Scores ************************
BLEU:
	PBMT	NMT	Win?
BLEU	22.4309	24.0322	s2>s1
	[21.5177,23.5150]	[23.0692,25.1154]	p=0.0000

********************** Aggregate Scores ************************
RIBES:
	PBMT	NMT	Win?
RIBES	80.0020	79.9978	-
	[79.1258,80.8138]	[78.9881,80.9409]	p=0.5000

********************** Aggregate Scores ************************
length ratio:
	PBMT	NMT	Win?
length ratio	0.9479 (ref=48183, out=45672)	0.9382 (ref=48183, out=45207)	s1>s2
	[0.9384,0.9581]	[0.9265,0.9515]	p=0.0320

Reading frequency from "example/ted.train.eng"
********************** Word Accuracy Analysis ************************
--- word fmeas by frequency bucket
frequency	PBMT	NMT
<1	0.1005	0.0493
1	0.2226	0.0850
2	0.3430	0.1735
3	0.3644	0.2408
4	0.4364	0.1667
[5,10)	0.3664	0.2012
[10,100)	0.4843	0.3880
[100,1000)	0.5482	0.5160
>=1000	0.6377	0.6485

********************** Word Accuracy Analysis ************************
--- word fmeas by labels bucket
labels	PBMT	NMT
CC	0.7877	0.8043
DT	0.5252	0.5634
IN	0.5360	0.5441
JJ	0.4991	0.4620
NN	0.5485	0.4828
NNP	0.6297	0.4930
NNS	0.5591	0.4992
PRP	0.6274	0.6584
RB	0.4861	0.4662
TO	0.6246	0.6360
VB	0.4720	0.4366
VBP	0.4339	0.4533
VBZ	0.4814	0.5031
other	0.6716	0.6661

********************** Sentence Bucket Analysis ************************
--- bucket type: length, statistic type: BLEU
length	PBMT	NMT
<10	23.3613	26.3236
[10,20)	22.0618	24.8458
[20,30)	22.4301	24.0137
[30,40)	20.4857	22.0523
[40,50)	21.3550	22.2325
[50,60)	22.4186	22.8380
>=60	25.9409	24.1902

********************** Sentence Bucket Analysis ************************
--- bucket type: len(output)-len(reference), statistic type: count
lengthdiff	PBMT	NMT
<-20	0	9
[-20,-10)	39	51
[-10,-5)	194	182
-5	107	93
-4	127	153
-3	219	194
-2	296	275
-1	330	344
0	394	423
1	263	256
2	173	187
3	115	97
4	73	58
5	41	44
[6,11)	66	67
[11,21)	8	12
>=21	0	0

********************** Sentence Bucket Analysis ************************
--- bucket type: sentence-level BLEU, statistic type: count
sentbleu	PBMT	NMT
<10.0	128	116
[10.0,20.0)	832	798
[20.0,30.0)	651	604
[30.0,40.0)	391	396
[40.0,50.0)	191	212
[50.0,60.0)	106	129
[60.0,70.0)	52	63
[70.0,80.0)	32	47
[80.0,90.0)	31	36
>=90.0	31	44

********************** N-gram Difference Analysis ************************
--- min_ngram_length=1, max_ngram_length=4
    report_length=50, alpha=1.0, compare_type=match
--- 50 n-grams where PBMT>NMT in match
phantom	0.9459 (sys1=34, sys2=1)
Amy	0.9091 (sys1=9, sys2=0)
, who	0.9000 (sys1=8, sys2=0)
my mother	0.8889 (sys1=7, sys2=0)
my mother .	0.8571 (sys1=5, sys2=0)
else happened	0.8571 (sys1=5, sys2=0)
And so	0.8571 (sys1=5, sys2=0)
something else happened	0.8571 (sys1=5, sys2=0)
Avelile	0.8571 (sys1=5, sys2=0)
viewer	0.8333 (sys1=4, sys2=0)
mother . " "	0.8333 (sys1=4, sys2=0)
Center	0.8333 (sys1=4, sys2=0)
Oz	0.8333 (sys1=4, sys2=0)
the fusiform	0.8333 (sys1=4, sys2=0)
file	0.8333 (sys1=4, sys2=0)
the phantom	0.8333 (sys1=4, sys2=0)
fusiform	0.8333 (sys1=4, sys2=0)
centers	0.8333 (sys1=4, sys2=0)
my mother . "	0.8333 (sys1=4, sys2=0)
and so on	0.8333 (sys1=4, sys2=0)
so on	0.8333 (sys1=4, sys2=0)
fine	0.8333 (sys1=4, sys2=0)
mother . "	0.8333 (sys1=4, sys2=0)
rightness	0.8333 (sys1=4, sys2=0)
instead	0.8182 (sys1=8, sys2=1)
exchange	0.8125 (sys1=12, sys2=2)
fishermen	0.8000 (sys1=3, sys2=0)
abuse of women	0.8000 (sys1=3, sys2=0)
response	0.8000 (sys1=3, sys2=0)
lose the ability to	0.8000 (sys1=3, sys2=0)
. And	0.8000 (sys1=3, sys2=0)
stroke	0.8000 (sys1=3, sys2=0)
Limpopo	0.8000 (sys1=3, sys2=0)
so on .	0.8000 (sys1=3, sys2=0)
Bible	0.8000 (sys1=3, sys2=0)
creativity can	0.8000 (sys1=3, sys2=0)
Beth	0.8000 (sys1=3, sys2=0)
address	0.8000 (sys1=3, sys2=0)
found that	0.8000 (sys1=3, sys2=0)
the fusiform gyrus	0.8000 (sys1=3, sys2=0)
Carter Center	0.8000 (sys1=3, sys2=0)
fun	0.8000 (sys1=3, sys2=0)
Yeah	0.8000 (sys1=7, sys2=1)
exactly like	0.8000 (sys1=3, sys2=0)
the Bible	0.8000 (sys1=3, sys2=0)
command	0.8000 (sys1=3, sys2=0)
Israel	0.8000 (sys1=3, sys2=0)
Baghdad	0.8000 (sys1=3, sys2=0)
like my mother	0.8000 (sys1=3, sys2=0)
of women	0.8000 (sys1=3, sys2=0)

--- 50 n-grams where NMT>PBMT in match
going to show	0.1250 (sys1=0, sys2=6)
going to show you	0.1250 (sys1=0, sys2=6)
Is it	0.1429 (sys1=0, sys2=5)
Is	0.1429 (sys1=0, sys2=5)
'm going to show	0.1429 (sys1=0, sys2=5)
't even	0.1429 (sys1=0, sys2=5)
, because the	0.1429 (sys1=0, sys2=5)
hemisphere	0.1429 (sys1=0, sys2=5)
years old	0.1667 (sys1=0, sys2=4)
presence of	0.1667 (sys1=0, sys2=4)
yet	0.1667 (sys1=0, sys2=4)
: Okay	0.1667 (sys1=0, sys2=4)
left hemisphere	0.1667 (sys1=0, sys2=4)
the process	0.1667 (sys1=0, sys2=4)
the light	0.1667 (sys1=0, sys2=4)
process of	0.1667 (sys1=0, sys2=4)
the camera	0.1667 (sys1=0, sys2=4)
the present	0.1667 (sys1=0, sys2=4)
: Okay ,	0.1667 (sys1=0, sys2=4)
the presence of	0.1667 (sys1=0, sys2=4)
with a	0.1818 (sys1=1, sys2=8)
how do	0.1818 (sys1=1, sys2=8)
act	0.2000 (sys1=0, sys2=3)
AG : Okay	0.2000 (sys1=0, sys2=3)
little bit	0.2000 (sys1=0, sys2=3)
how do you	0.2000 (sys1=0, sys2=3)
a very early	0.2000 (sys1=0, sys2=3)
it doesn	0.2000 (sys1=0, sys2=3)
it doesn 't	0.2000 (sys1=0, sys2=3)
the surgeon	0.2000 (sys1=0, sys2=3)
, he	0.2000 (sys1=0, sys2=3)
going to be	0.2000 (sys1=0, sys2=3)
her the	0.2000 (sys1=0, sys2=3)
the youngest	0.2000 (sys1=0, sys2=3)
to show	0.2000 (sys1=1, sys2=7)
penalty	0.2000 (sys1=0, sys2=3)
he was	0.2000 (sys1=0, sys2=3)
not a	0.2000 (sys1=0, sys2=3)
the puzzle	0.2000 (sys1=0, sys2=3)
told	0.2000 (sys1=0, sys2=3)
a computer mouse	0.2000 (sys1=0, sys2=3)
to show you	0.2000 (sys1=1, sys2=7)
that .	0.2000 (sys1=0, sys2=3)
core of the	0.2000 (sys1=0, sys2=3)
don 't have to	0.2000 (sys1=0, sys2=3)
if they	0.2000 (sys1=0, sys2=3)
core of	0.2000 (sys1=0, sys2=3)
yeah	0.2000 (sys1=0, sys2=3)
, there 's a	0.2000 (sys1=0, sys2=3)
size of	0.2000 (sys1=0, sys2=3)

********************** Sentence Examples Analysis ************************
--- 10 sentences where PBMT>NMT at sentence-level BLEU
PBMT-NMT=81.4249, PBMT=100.0000, NMT=18.5751
Ref:  That 's exciting in itself .
PBMT: That 's exciting in itself .
NMT: This is a thrill of self .

PBMT-NMT=79.8351, PBMT=100.0000, NMT=20.1649
Ref:  And they lived together happily ever after .
PBMT: And they lived together happily ever after .
NMT: And he lived with happily to death .

PBMT-NMT=58.8866, PBMT=100.0000, NMT=41.1134
Ref:  Beth Israel 's in Boston .
PBMT: Beth Israel 's in Boston .
NMT: Beat Isaill is in Boston .

PBMT-NMT=57.5987, PBMT=100.0000, NMT=42.4013
Ref:  ( Applause ) Last question , Julian .
PBMT: ( Applause ) Last question , Julian .
NMT: ( Applause ) The last question , Julian . Julan .

PBMT-NMT=55.9284, PBMT=73.7835, NMT=17.8551
Ref:  We realized that even rich kids from the suburbs really want DryBath . ( Laughter ) At least once a week .
PBMT: And we found that even rich kids a suburbs really want DryBath . ( Laughter ) At least once a week .
NMT: We 've learned that the rich kids have actually wanted DryBothth , ( Laughter ) at the time for a week .

PBMT-NMT=51.9216, PBMT=100.0000, NMT=48.0784
Ref:  JA : I 'm not sure about the incident .
PBMT: JA : I 'm not sure about the incident .
NMT: J : I 'm not sure of you .

PBMT-NMT=50.8271, PBMT=62.5361, NMT=11.7091
Ref:  This was described beautifully in a book in 2006 by Michael Porter and Elizabeth Teisberg .
PBMT: This was described beautifully in 2006 in a book that wrote Michael Porter and Elizabeth Teisberg .
NMT: This was originally gorgeous in 2006 in 2006 in 2006 , and they wrote Michael Porrter and Edzabet Tode .

PBMT-NMT=49.1867, PBMT=100.0000, NMT=50.8133
Ref:  Why is that ?
PBMT: Why is that ?
NMT: Why is this ?

PBMT-NMT=47.4704, PBMT=72.7245, NMT=25.2542
Ref:  I don 't literally mean 24 hours , seven days a week .
PBMT: I don 't mean literally 24 hours , seven days a week .
NMT: I don 't mean literally 24 hours in the week .

PBMT-NMT=46.2715, PBMT=100.0000, NMT=53.7285
Ref:  The differences were dramatic .
PBMT: The differences were dramatic .
NMT: The variations were dramatic .

--- 10 sentences where NMT>PBMT at sentence-level BLEU
PBMT-NMT=-57.0510, PBMT=15.8445, NMT=72.8955
Ref:  Tiny tweaks can lead to big changes .
PBMT: Now , this idea of marginal raisestas can lead to a big change to happen .
NMT: Facferences can lead to big changes .

PBMT-NMT=-58.8866, PBMT=41.1134, NMT=100.0000
Ref:  So here 's a video .
PBMT: So here 's the video . "
NMT: So here 's a video .

PBMT-NMT=-58.8866, PBMT=41.1134, NMT=100.0000
Ref:  It 's not the numbers .
PBMT: It 's not about those numbers .
NMT: It 's not the numbers .

PBMT-NMT=-60.2462, PBMT=15.2231, NMT=75.4693
Ref:  So here I 'm going to show you two tandem clips .
PBMT: Here you 're going to two footage .
NMT: So here I 'm going to show you two footage .

PBMT-NMT=-61.3903, PBMT=38.6097, NMT=100.0000
Ref:  What is this ?
PBMT: " What is that ?
NMT: What is this ?

PBMT-NMT=-61.7397, PBMT=38.2603, NMT=100.0000
Ref:  ( Applause ) That 's true .
PBMT: ( Applause ) It 's so .
NMT: ( Applause ) That 's true .

PBMT-NMT=-64.0696, PBMT=35.9304, NMT=100.0000
Ref:  Light is good .
PBMT: The light 's good .
NMT: Light is good .

PBMT-NMT=-64.9156, PBMT=35.0844, NMT=100.0000
Ref:  And what I 'm talking about is this .
PBMT: And that 's what I 'm saying is this .
NMT: And what I 'm talking about is this .

PBMT-NMT=-68.8509, PBMT=31.1491, NMT=100.0000
Ref:  They 're just learning how to count .
PBMT: Meanwhile just teach to count .
NMT: They 're just learning how to count .

PBMT-NMT=-69.1802, PBMT=30.8198, NMT=100.0000
Ref:  Boy : That 's why .
PBMT: Boy : So .
NMT: Boy : That 's why .

(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt$ cd outputs/
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt/outputs$ google-chrome ./index.html 
Opening in existing browser session.
(compare-mt) ye@ykt-pro:/media/ye/project1/tool/compare-mt/outputs$ 
```

ဒီတစ်ခါတော့ html report ထွက်တယ်။  
Easy Peasy Lemon Squeezy!!!  :P   

## Study on Required Files for Running with Example Command

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ted.ref.eng
By the end of this year , there 'll be nearly a billion people on this planet that actively use social networking sites .
The one thing that all of them have in common is that they 're going to die .
While that might be a somewhat morbid thought , I think it has some really profound implications that are worth exploring .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ted.sys1.eng
By the end of this year will be on this planet about billion people to use active aspects of social networks .
The only thing that they have in common is that all die .
Even when it can be a bit of a morbidn thought , I think that there 's seriously impacts that it 's explore .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ted.sys2.eng
The end of this year is going to be about billions of people actively use sites of social media .
The only thing that everybody 's common is that they die .
Even though it might be a little bit of a clamina thought , I think it 's a serious impact that tries to explore .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ted.train.eng
But what I find really fascinating is what happens when architects and planners leave and these places become appropriated by people , like here in Chandigarh , India , the city which has been completely designed by the architect Le Corbusier .
Now 60 years later , the city has been taken over by people in very different ways from whatever perhaps intended for , like here , where you have the people sitting in the windows of the assembly hall .
But over the course of several years , I 've been documenting Rem Koolhaas 's CCTV building in Beijing and the olympic stadium in the same city by the architects Herzog and de Meuron .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ted.ref.eng.tag
IN DT NN IN DT NN , EX MD VB RB DT CD NNS IN DT NN WDT RB VBP JJ NN NNS .
DT CD NN IN DT IN PRP VBP IN JJ VBZ IN PRP VBP VBG TO VB .
IN DT MD VB DT RB JJ NN , PRP VBP PRP VBZ DT RB JJ NNS WDT VBP JJ VBG .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ./ted.sys1.eng.tag 
IN DT NN IN DT NN MD VB IN DT NN IN CD NNS TO VB JJ NNS IN JJ NNS .
DT JJ NN IN PRP VBP IN JJ VBZ IN DT NN .
RB WRB PRP MD VB DT NN IN DT NN NN , PRP VBP IN EX VBZ RB VBZ IN PRP VBZ RB .
```

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ head -3 ./ted.sys2.eng.tag 
DT NN IN DT NN VBZ VBG TO VB IN NNS IN NNS RB VBP NNS IN JJ NNS .
DT JJ NN IN NN POS JJ VBZ IN PRP VBP .
RB IN PRP MD VB DT JJ NN IN DT NN NN , PRP VBP PRP VBZ DT JJ NN WDT VBZ TO VB .
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ 
```

## Current Error That I Have to Solve

လက်ရှိ ဇာဇာလှိုင်က run လို့ မရဖြစ်နေတာက အောက်ပါ command...   
(label တွေပါသုံးပြီး evaluation လုပ်ချင်တာ... )  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ compare-mt 8_compare-mt-with-label/1_ref.my 8_compare-mt-with-label/2_trans.my 8_compare-mt-with-label/3_multiTrans.my 8_compare-mt-with-label/4_s-multiTrans.my --compare_scores score_type=bleu,bootstrap=1000 score_type=ribes,bootstrap=1000 score_type=length,bootstrap=1000 --compare_word_accuracies bucket_type=freq,freq_corpus_file=8_compare-mt-with-label/train.my bucket_type=label,ref_labels=8_compare-mt-with-label/1_ref.my.word.upos.tag,out_labels="8_compare-mt-with-label/2_trans.my.upos.tag;8_compare-mt-with-label/3_multiTrans.my.upos.tag;8_compare-mt-with-label/4_s-multiTrans.my.upos.tag",label_set=VERB+NOUN+PRON+ADJ+ADV+ADP+CONJ+DET+NUM+PRT+X --output_directory outputs-for-cmt-label --sys_names Trans MulTrans SMulTrans
********************** Aggregate Scores ************************
BLEU:
Trans MulTrans SMulTrans
BLEU 22.7889 24.8936 25.2540

v s1 / s2 -> MulTrans SMulTrans
Trans s2>s1 (p=0.0030) s2>s1 (p=0.0000)
MulTrans - (p=0.2870)

********************** Aggregate Scores ************************
RIBES:
Trans MulTrans SMulTrans
RIBES 72.2036 73.6971 72.0465

v s1 / s2 -> MulTrans SMulTrans
Trans - (p=0.0940) - (p=0.4230)
MulTrans s1>s2 (p=0.0490)

********************** Aggregate Scores ************************
length ratio:
Trans MulTrans SMulTrans
length ratio 0.7705 (ref=13470, out=10379) 0.7970 (ref=13470, out=10735) 0.8142 (ref=13470, out=10967)

v s1 / s2 -> MulTrans SMulTrans
Trans s2>s1 (p=0.0080) s2>s1 (p=0.0000)
MulTrans s2>s1 (p=0.0360)

Reading frequency from "8_compare-mt-with-label/train.my"
********************** Word Accuracy Analysis ************************
--- word fmeas by frequency bucket
frequency Trans MulTrans SMulTrans
<1 0.0000 0.0000 0.0000
1 0.1000 0.3333 0.0000
2 0.0952 0.0870 0.1000
3 0.1429 0.1667 0.1429
4 0.0000 0.0000 0.0000
[5,10) 0.1905 0.2885 0.2991
[10,100) 0.3062 0.3585 0.3492
[100,1000) 0.3894 0.4354 0.4321
>=1000 0.5898 0.6033 0.5974

Traceback (most recent call last):
  File "/home/ye/tool/anaconda3/envs/compare-mt/bin/compare-mt", line 8, in <module>
    sys.exit(main())
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 643, in main
    reports.append( (name, [func(ref, outs, **arg_utils.parse_profile(x)) for x in arg]) )
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 643, in <listcomp>
    reports.append( (name, [func(ref, outs, **arg_utils.parse_profile(x)) for x in arg]) )
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 145, in generate_word_accuracy_report
    statistics, my_ref_total_list, my_out_totals_list, my_out_matches_list = bucketer.calc_statistics(ref, outs, ref_labels=ref_labels, out_labels=out_labels)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 185, in calc_statistics
    [x[rsi] for x in out_labels] if out_labels else None)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 74, in _calc_trg_buckets_and_matches
    ref_buckets = [self.calc_bucket(w, label=l) for (w,l) in itertools.zip_longest(ref_sent, ref_label)]
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 74, in <listcomp>
    ref_buckets = [self.calc_bucket(w, label=l) for (w,l) in itertools.zip_longest(ref_sent, ref_label)]
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 520, in calc_bucket
    raise ValueError('When calculating buckets by label, label must be non-zero')
ValueError: When calculating buckets by label, label must be non-zero
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ 
```

"label must be non-zero" ဆိုတဲ့ error ကို ပေးနေတယ်...  

အရင်ဆုံး reference ဖိုင်တွေ၊ output ဖိုင်တွေနဲ့ label ဖိုင်တွေရဲ့ content ကို အကြမ်းမျဉ်း print ထုတ်ပြီး confirmation လုပ်ခဲ့...  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/1_ref.my
 ကျ သင့် ငွေ ဘယ် လောက် လဲ ။
 ကျွန် တော် လက် ဆောင် အ နေ နဲ့ ပေး လို့ ရ တဲ့ ပစ္စည်း မျိုး ကြည့် ချင် လို့ ။
 ရ ထား က ကြာ နေ တာ လား ။
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/2_trans.my
 ယာဉ် စီး ခ ဘယ် လောက် လဲ ။
 ကျွန် တော် အ သံ သွင်း ဆိုင် ရှာ နေ တာ ပါ ။
 ရ ထား က အ ချိန် မှန် လား ။
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/3_multiTrans.my
 ယာဉ် စီး ခ ဘယ် လောက် လဲ ။
 ကျွန် တော် လက် ဆောင် ရှာ နေ တာ ။
 ရ ထား က အ ချိန် မှန် လား ။
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/4_s-multiTrans.my
 ယာဉ် စီး ခ ဘယ် လောက် လဲ ။
 ကျွန် တော် လက် ဆောင် ရှာ နေ တာ ။
 ရ ထား က အ ချိန် မှန် လား ။
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/train.my
 ဟုတ် ကဲ့ ၊ ကျွန် တော် ထိုင်း စစ် တု ရင် က စား ရ တာ ကြိုက် တယ် ။
 က လေး များ အ တွက် တစ် ခု ခု အ ကြံ ပြု ပေး နိုင် မ လား ။
 အဲ ဒီ ကို ဘယ် လို ရောက် နိုင် မ လဲ ။
```

tag ဖိုင်တွေက အောက်ပါအတိုင်း အဆင်ပြေသလို မြင်ရ...  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/1_ref.my.word.upos.tag
NOUN ADJ PRT .
PRON NOUN NOUN ADP VERB PRT VERB PRT NOUN NOUN VERB PRT PRT .
NOUN ADP VERB PRT PRT PRT .
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/2_trans.my.upos.tag
NOUN ADJ PRT .
PRON VERB NOUN VERB PRT PRT PRT .
NOUN ADP ADJ PRT .
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
NOUN ADJ PRT .
PRON NOUN VERB PRT PRT .
NOUN ADP ADJ PRT .
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ head -3 ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag NOUN ADJ PRT .
PRON NOUN VERB PRT PRT .
NOUN ADP ADJ PRT .
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$
```

check file size:  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/1_ref.my
  1000  13470 124765 ./8_compare-mt-with-label/1_ref.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/2_trans.my
 1000 10379 96006 ./8_compare-mt-with-label/2_trans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/3_multiTrans.my
  1000  10735 100147 ./8_compare-mt-with-label/3_multiTrans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/4_s-multiTrans.my
  1000  10967 103806 ./8_compare-mt-with-label/4_s-multiTrans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/train.my
  20000  263499 2455740 ./8_compare-mt-with-label/train.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/1_ref.my.word.upos.tag
 1000  9579 39774 ./8_compare-mt-with-label/1_ref.my.word.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/2_trans.my.upos.tag
 1000  7673 31606 ./8_compare-mt-with-label/2_trans.my.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
 1000  7836 32185 ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag
 1000  7913 32720 ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$
```

blank line တွေများ ရှိနေသလား ဆိုတာကိုလည်း ရှာဖွကြည့်ခဲ့...  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/1_ref.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/2_trans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/3_multiTrans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/4_s-multiTrans.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/train.my
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/1_ref.my.word.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/2_trans.my.upos.tag (compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ sed -n '/^$/=' ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$
```

Error ပေးနေတဲ့ python code ဖိုင်နာမည် ```bucketers.py``` ထဲကို ဝင်ကြည့်ခဲ့...  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ gedit /home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py
```

Line 520: မှာ ရှိတဲ့ function က ...  

```python
  def calc_bucket(self, word, label=None):
    if not label:
      raise ValueError('When calculating buckets by label, label must be non-zero')
    return self.bucket_map[label]
```

အထက်ပါ function ကနေ error ပေးတာ...   
line no. 73 ခေါ်သုံးရာကနေ error တက်တာလို့ နားလည်တယ်

Line 73:  

```python
    # Process the reference, getting the bucket
    ref_buckets = [self.calc_bucket(w, label=l) for (w,l) in itertools.zip_longest(ref_sent, ref_label)]
```


Check the POS-tag labels  

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label/8_compare-mt-with-label$ cat ./1_ref.my.word.upos.tag | sed "s/ /\n/g;" | sort | uniq -c
   1127 .
    285 ADJ
   1377 ADP
    204 ADV
    165 CONJ
   1669 NOUN
    201 NUM
    660 PRON
   2433 PRT
   1378 VERB
     80 X
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label/8_compare-mt-with-label$ cat ./2_trans.my.upos.tag | sed "s/ /\n/g;" | sort | uniq -c
   1029 .
    241 ADJ
    990 ADP
    147 ADV
    104 CONJ
      5 n
   1260 NOUN
    126 NUM
    501 PRON
   2045 PRT
   1189 VERB
     36 X
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label/8_compare-mt-with-label$ cat ./3_multiTrans.my.upos.tag | sed "s/ /\n/g;" | sort | uniq -c
   1042 .
    236 ADJ
   1146 ADP
    248 ADV
     84 CONJ
      5 n
   1265 NOUN
    139 NUM
    529 PRON
   1956 PRT
   1143 VERB
     43 X
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label/8_compare-mt-with-label$ cat ./4_s-multiTrans.my.upos.tag | sed "s/ /\n/g;" | sort | uniq -c
    947 .
    259 ADJ
   1176 ADP
    249 ADV
     91 CONJ
      5 n
   1405 NOUN
    248 NUM
    551 PRON
   1973 PRT
    981 VERB
     28 X
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label/8_compare-mt-with-label$ 
```

DET မရှိပဲနဲ့ DET tag ကို command မှာ ပေးထားတာတွေ့ရ....  

code မှာ print တစ်ကြောင်း ရိုက်ထည့်ပြီး debug လုပ်ခဲ့...  

```python
  def calc_bucket(self, word, label=None):
    if not label:
      print("word: ", word)
      raise ValueError('When calculating buckets by label, label must be non-zero')
    return self.bucket_map[label]
```

run ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
word:  လောက်
Traceback (most recent call last):
  File "/home/ye/tool/anaconda3/envs/compare-mt/bin/compare-mt", line 8, in <module>
    sys.exit(main())
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 643, in main
    reports.append( (name, [func(ref, outs, **arg_utils.parse_profile(x)) for x in arg]) )
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 643, in <listcomp>
    reports.append( (name, [func(ref, outs, **arg_utils.parse_profile(x)) for x in arg]) )
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/compare_mt_main.py", line 145, in generate_word_accuracy_report
    statistics, my_ref_total_list, my_out_totals_list, my_out_matches_list = bucketer.calc_statistics(ref, outs, ref_labels=ref_labels, out_labels=out_labels)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 185, in calc_statistics
    [x[rsi] for x in out_labels] if out_labels else None)
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 74, in _calc_trg_buckets_and_matches
    ref_buckets = [self.calc_bucket(w, label=l) for (w,l) in itertools.zip_longest(ref_sent, ref_label)]
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 74, in <listcomp>
    ref_buckets = [self.calc_bucket(w, label=l) for (w,l) in itertools.zip_longest(ref_sent, ref_label)]
  File "/home/ye/tool/anaconda3/envs/compare-mt/lib/python3.7/site-packages/compare_mt/bucketers.py", line 522, in calc_bucket
    raise ValueError('When calculating buckets by label, label must be non-zero')
ValueError: When calculating buckets by label, label must be non-zero
```

## I Found the Reason

အထက်ပါအတိုင်း တောက်လျှောက် Error ကို trace လိုက်လာရင်း တစ်ခုသွားသတိရတာက စာကြောင်း တစ်ကြောင်းမှာ ရှိတဲ့ စာလုံးအရေအတွက် (no. of words in a sentence) နဲ့ POS tagging လုပ်ထားတဲ့ အရေအတွက် (no. of POS tags) က တူညီနေမှ ဖြစ်မယ်ဆိုတဲ့ အချက်ကို....  
သေချာအောင် compare-mt Github original ပါလာတဲ့ example folder ထဲက word file နဲ့ POS-tag file တွေရဲ့ စာလုံးရေအရေအတွက်ကို wc command ကို သုံးပြီးတော့ confirmation လုပ်ခဲ့တော့ reference မှာ အနည်းငယ်လွဲနေပေမဲ့ evaluation လုပ်တဲ့ system-1 နဲ့ system-2 ရဲ့ output file တွေမှာက no. of words = no. of POS-tags ဖြစ်နေတာကို အောက်ပါအတိုင်း တွေ့ရတယ်။  
(reference မှာ မတူတာက space ပိုရိုက်ထားတာမျိုး ဖြစ်နိုင်တယ်။ အဲဒါမျိုးဆိုရင်တော့ ပြဿနာ မဟုတ်ဘူးလေ...)  

```
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ wc ted.ref.eng ted.ref.eng.tag
  2445  48181 231365 ted.ref.eng
  2445  48183 154104 ted.ref.eng.tag
  4890  96364 385469 total
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ wc ted.sys1.eng ted.sys1.eng.tag
  2445  45672 217289 ted.sys1.eng
  2445  45672 146376 ted.sys1.eng.tag
  4890  91344 363665 total
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$ wc ted.sys2.eng ted.sys2.eng.tag
  2445  45207 212717 ted.sys2.eng
  2445  45207 145629 ted.sys2.eng.tag
  4890  90414 358346 total
(base) ye@ykt-pro:/media/ye/project1/tool/compare-mt/example$
```

ဇာဇာလှိုင်က ငါ့ဆီကို ပို့ထားတဲ့ reference file တွေ word file တွေနဲ့ POS-tag ဖိုင်တွေအားလုံးကို wc command နဲ့ confirm လုပ်ကြည့်တော့ အောက်ပါအတိုင်း လွဲနေတာကို တွေ့ရတယ်။   
ERROR ဖြစ်ရဲ့ အကြောင်းအရင်းကိုတော့ ရှာတွေ့သွားပြီ။ ဘာကြောင့်မတူရတာလဲ၊ ဖိုင် attach လုပ်တာမှာ လွဲသွားတာလား?! သို့မဟုတ် NMT model ကနေ output ထွက်တဲ့အခါမှာ လွဲတာလား (သိပ်တော့ မဖြစ်နိုင်၊ မော်ဒယ်က OOV ဖြစ်သည့်တိုင်အောင် POS-tag တစ်ခုတော့ tag လုပ်ပေးလိုက်မယ်လို့ ယူဆ) ...   

```
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/1_ref.my ./8_compare-mt-with-label/1_ref.my.word.upos.tag
  1000  13470 124765 ./8_compare-mt-with-label/1_ref.my
  1000   9579  39771 ./8_compare-mt-with-label/1_ref.my.word.upos.tag
  2000  23049 164536 total
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/2_trans.my ./8_compare-mt-with-label/2_trans.my.upos.tag
  1000  10379  96006 ./8_compare-mt-with-label/2_trans.my
  1000   7673  31606 ./8_compare-mt-with-label/2_trans.my.upos.tag
  2000  18052 127612 total
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/3_multiTrans.my ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
  1000  10735 100147 ./8_compare-mt-with-label/3_multiTrans.my
  1000   7836  32185 ./8_compare-mt-with-label/3_multiTrans.my.upos.tag
  2000  18571 132332 total
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$ wc ./8_compare-mt-with-label/4_s-multiTrans.my ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag
  1000  10967 103806 ./8_compare-mt-with-label/4_s-multiTrans.my
  1000   7913  32720 ./8_compare-mt-with-label/4_s-multiTrans.my.upos.tag
  2000  18880 136526 total
(compare-mt) ye@ykt-pro:~/Downloads/Report-for-compare-mt-label$
```

## To Do  

- ဘာကြောင့် hyp ဖိုင်တွေရဲ့ no. of words နဲ့ POS-tag အရေအတွက်က မတူရတာလဲ ဆိုတာကို ဇာဇာလှိုင်ကို ပြန် confim လုပ်ရန်
- compare-mt ရဲ့ တခြား option တွေကို combine လုပ်ကြည့်တာ၊ လိုတဲ့ report တစ်ခုတည်းကိုပဲ သီးခြားထုတ်တာမျိုး လုပ်ကြည့်ရန်

## Reference

https://stackoverflow.com/questions/47571689/unable-to-use-matplotlib-functions-in-my-program
https://stackoverflow.com/questions/59819158/pyplot-errorbars-with-different-x-and-y-error
