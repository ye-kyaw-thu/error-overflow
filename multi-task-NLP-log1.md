# multi-task Experiment log

```
$ git clone https://github.com/hellohaptik/multi-task-NLP.git
$ cd multi-task-NLP
```
လုပ်ပြီးသွားတဲ့အခါမှာ...  
အရင်ဆုံး python environment အသစ်ကို create လုပ်ခဲ့  

```
(base) ye@:~/exp/multi-task/multi-task-NLP$ conda create -n multiTask python=3.7.3
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/multiTask

  added / updated specs:
    - python=3.7.3


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2021.5.30          |   py37h06a4308_0         139 KB
    libedit-3.1.20210714       |       h7f8727e_0         165 KB
    pip-21.2.2                 |   py37h06a4308_0         1.8 MB
    python-3.7.3               |       h0371630_0        32.1 MB
    setuptools-58.0.4          |   py37h06a4308_0         775 KB
    ------------------------------------------------------------
                                           Total:        35.0 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.7.5-h06a4308_1
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py37h06a4308_0
  libedit            pkgs/main/linux-64::libedit-3.1.20210714-h7f8727e_0
  libffi             pkgs/main/linux-64::libffi-3.2.1-hf484d3e_1007
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py37h06a4308_0
  python             pkgs/main/linux-64::python-3.7.3-h0371630_0
  readline           pkgs/main/linux-64::readline-7.0-h7b6447c_5
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py37h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.33.0-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2021.5.30    | 139 KB    | ############################################################################################################# | 100% 
python-3.7.3         | 32.1 MB   | ############################################################################################################# | 100% 
setuptools-58.0.4    | 775 KB    | ############################################################################################################# | 100% 
pip-21.2.2           | 1.8 MB    | ############################################################################################################# | 100% 
libedit-3.1.20210714 | 165 KB    | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate multiTask
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@:~/exp/multi-task/multi-task-NLP$ conda activate multiTask
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$
```

## Install Requirements

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ pip install -r requirements.txt
Collecting seqeval==0.0.12
  Using cached seqeval-0.0.12.tar.gz (21 kB)
Collecting tqdm==4.30.0
  Using cached tqdm-4.30.0-py2.py3-none-any.whl (47 kB)
Collecting ipywidgets==7.4.2
  Using cached ipywidgets-7.4.2-py2.py3-none-any.whl (111 kB)
Collecting Keras==2.3.1
  Using cached Keras-2.3.1-py2.py3-none-any.whl (377 kB)
Collecting transformers==2.8.0
  Using cached transformers-2.8.0-py3-none-any.whl (563 kB)
Collecting joblib==0.13.2
  Using cached joblib-0.13.2-py2.py3-none-any.whl (278 kB)
Collecting torch==1.2.0
  Downloading torch-1.2.0-cp37-cp37m-manylinux1_x86_64.whl (748.9 MB)
     |████████████████████████████████| 748.9 MB 2.7 kB/s 
Collecting tensorflow==1.15.2
  Downloading tensorflow-1.15.2-cp37-cp37m-manylinux2010_x86_64.whl (110.5 MB)
     |████████████████████████████████| 110.5 MB 27.9 MB/s 
Collecting numpy==1.18.1
  Downloading numpy-1.18.1-cp37-cp37m-manylinux1_x86_64.whl (20.1 MB)
     |████████████████████████████████| 20.1 MB 94.2 MB/s 
Collecting sphinx_rtd_theme==0.4.3
  Downloading sphinx_rtd_theme-0.4.3-py2.py3-none-any.whl (6.4 MB)
     |████████████████████████████████| 6.4 MB 27.1 MB/s 
Collecting pandas==1.0.1
  Downloading pandas-1.0.1-cp37-cp37m-manylinux1_x86_64.whl (10.1 MB)
     |████████████████████████████████| 10.1 MB 68.3 MB/s 
Collecting scikit_learn==0.23.1
  Downloading scikit_learn-0.23.1-cp37-cp37m-manylinux1_x86_64.whl (6.8 MB)
     |████████████████████████████████| 6.8 MB 30.0 MB/s 
Collecting PyYAML==5.3.1
  Using cached PyYAML-5.3.1-cp37-cp37m-linux_x86_64.whl
Collecting ipykernel>=4.5.1
  Downloading ipykernel-6.4.1-py3-none-any.whl (124 kB)
     |████████████████████████████████| 124 kB 30.8 MB/s 
Collecting traitlets>=4.3.1
  Downloading traitlets-5.1.0-py3-none-any.whl (101 kB)
     |████████████████████████████████| 101 kB 15.0 MB/s 
Collecting widgetsnbextension~=3.4.0
  Downloading widgetsnbextension-3.4.2-py2.py3-none-any.whl (2.2 MB)
     |████████████████████████████████| 2.2 MB 122.7 MB/s 
Collecting nbformat>=4.2.0
  Using cached nbformat-5.1.3-py3-none-any.whl (178 kB)
Collecting ipython>=4.0.0
  Downloading ipython-7.28.0-py3-none-any.whl (788 kB)
     |████████████████████████████████| 788 kB 114.3 MB/s 
Collecting keras-applications>=1.0.6
  Using cached Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
Collecting h5py
  Downloading h5py-3.4.0-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.1 MB)
     |████████████████████████████████| 4.1 MB 30.8 MB/s 
Collecting scipy>=0.14
  Downloading scipy-1.7.1-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (28.5 MB)
     |████████████████████████████████| 28.5 MB 93.1 MB/s 
Collecting six>=1.9.0
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting keras-preprocessing>=1.0.5
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting tokenizers==0.5.2
  Downloading tokenizers-0.5.2-cp37-cp37m-manylinux1_x86_64.whl (5.6 MB)
     |████████████████████████████████| 5.6 MB 25.3 MB/s 
Collecting sacremoses
  Downloading sacremoses-0.0.46-py3-none-any.whl (895 kB)
     |████████████████████████████████| 895 kB 100.2 MB/s 
Collecting filelock
  Downloading filelock-3.3.0-py3-none-any.whl (9.7 kB)
Collecting sentencepiece
  Downloading sentencepiece-0.1.96-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.2 MB)
     |████████████████████████████████| 1.2 MB 59.3 MB/s 
Collecting requests
  Using cached requests-2.26.0-py2.py3-none-any.whl (62 kB)
Collecting boto3
  Downloading boto3-1.18.54-py3-none-any.whl (131 kB)
     |████████████████████████████████| 131 kB 85.4 MB/s 
Collecting regex!=2019.12.17
  Downloading regex-2021.9.30-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (747 kB)
     |████████████████████████████████| 747 kB 131.9 MB/s 
Collecting absl-py>=0.7.0
  Downloading absl_py-0.14.1-py3-none-any.whl (131 kB)
     |████████████████████████████████| 131 kB 75.4 MB/s 
Collecting wrapt>=1.11.1
  Downloading wrapt-1.13.1-cp37-cp37m-manylinux2010_x86_64.whl (79 kB)
     |████████████████████████████████| 79 kB 14.5 MB/s 
Collecting tensorflow-estimator==1.15.1
  Using cached tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
Collecting protobuf>=3.6.1
  Downloading protobuf-3.18.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 86.0 MB/s 
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting grpcio>=1.8.6
  Downloading grpcio-1.41.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.9 MB)
     |████████████████████████████████| 3.9 MB 72.6 MB/s 
Collecting tensorboard<1.16.0,>=1.15.0
  Using cached tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting termcolor>=1.1.0
  Using cached termcolor-1.1.0.tar.gz (3.9 kB)
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages (from tensorflow==1.15.2->-r requirements.txt (line 8)) (0.37.0)
Collecting gast==0.2.2
  Using cached gast-0.2.2.tar.gz (10 kB)
Collecting sphinx
  Downloading Sphinx-4.2.0-py3-none-any.whl (3.1 MB)
     |████████████████████████████████| 3.1 MB 79.8 MB/s 
Collecting python-dateutil>=2.6.1
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pytz>=2017.2
  Downloading pytz-2021.3-py2.py3-none-any.whl (503 kB)
     |████████████████████████████████| 503 kB 82.2 MB/s 
Collecting threadpoolctl>=2.0.0
  Downloading threadpoolctl-3.0.0-py3-none-any.whl (14 kB)
Collecting debugpy<2.0,>=1.0.0
  Downloading debugpy-1.5.0-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.9 MB)
     |████████████████████████████████| 1.9 MB 77.6 MB/s 
Collecting argcomplete>=1.12.3
  Downloading argcomplete-1.12.3-py2.py3-none-any.whl (38 kB)
Collecting matplotlib-inline<0.2.0,>=0.1.0
  Downloading matplotlib_inline-0.1.3-py3-none-any.whl (8.2 kB)
Collecting jupyter-client<8.0
  Downloading jupyter_client-7.0.5-py3-none-any.whl (124 kB)
     |████████████████████████████████| 124 kB 100.7 MB/s 
Collecting tornado<7.0,>=4.2
  Downloading tornado-6.1-cp37-cp37m-manylinux2010_x86_64.whl (428 kB)
     |████████████████████████████████| 428 kB 72.6 MB/s 
Collecting ipython-genutils
  Using cached ipython_genutils-0.2.0-py2.py3-none-any.whl (26 kB)
Collecting importlib-metadata<5
  Using cached importlib_metadata-4.8.1-py3-none-any.whl (17 kB)
Collecting zipp>=0.5
  Downloading zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-3.10.0.2-py3-none-any.whl (26 kB)
Collecting backcall
  Using cached backcall-0.2.0-py2.py3-none-any.whl (11 kB)
Collecting prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0
  Downloading prompt_toolkit-3.0.20-py3-none-any.whl (370 kB)
     |████████████████████████████████| 370 kB 74.7 MB/s 
Collecting pickleshare
  Using cached pickleshare-0.7.5-py2.py3-none-any.whl (6.9 kB)
Collecting pexpect>4.3
  Using cached pexpect-4.8.0-py2.py3-none-any.whl (59 kB)
Requirement already satisfied: setuptools>=18.5 in /home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages (from ipython>=4.0.0->ipywidgets==7.4.2->-r requirements.txt (line 3)) (58.0.4)
Collecting decorator
  Downloading decorator-5.1.0-py3-none-any.whl (9.1 kB)
Collecting jedi>=0.16
  Using cached jedi-0.18.0-py2.py3-none-any.whl (1.4 MB)
Collecting pygments
  Downloading Pygments-2.10.0-py3-none-any.whl (1.0 MB)
     |████████████████████████████████| 1.0 MB 94.0 MB/s 
Collecting parso<0.9.0,>=0.8.0
  Using cached parso-0.8.2-py2.py3-none-any.whl (94 kB)
Collecting jupyter-core>=4.6.0
  Downloading jupyter_core-4.8.1-py3-none-any.whl (86 kB)
     |████████████████████████████████| 86 kB 4.1 MB/s 
Collecting nest-asyncio>=1.5
  Using cached nest_asyncio-1.5.1-py3-none-any.whl (5.0 kB)
Collecting pyzmq>=13
  Downloading pyzmq-22.3.0-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 91.4 MB/s 
Collecting entrypoints
  Using cached entrypoints-0.3-py2.py3-none-any.whl (11 kB)
Collecting jsonschema!=2.5.0,>=2.4
  Downloading jsonschema-4.0.1-py3-none-any.whl (69 kB)
     |████████████████████████████████| 69 kB 10.5 MB/s 
Collecting pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0
  Downloading pyrsistent-0.18.0-cp37-cp37m-manylinux1_x86_64.whl (119 kB)
     |████████████████████████████████| 119 kB 74.1 MB/s 
Collecting attrs>=17.4.0
  Using cached attrs-21.2.0-py2.py3-none-any.whl (53 kB)
Collecting ptyprocess>=0.5
  Using cached ptyprocess-0.7.0-py2.py3-none-any.whl (13 kB)
Collecting wcwidth
  Using cached wcwidth-0.2.5-py2.py3-none-any.whl (30 kB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.3.4-py3-none-any.whl (97 kB)
Collecting werkzeug>=0.11.15
  Using cached Werkzeug-2.0.1-py3-none-any.whl (288 kB)
Collecting notebook>=4.4.1
  Downloading notebook-6.4.4-py3-none-any.whl (9.9 MB)
     |████████████████████████████████| 9.9 MB 55.1 MB/s 
Collecting argon2-cffi
  Downloading argon2_cffi-21.1.0-cp35-abi3-manylinux_2_5_x86_64.manylinux1_x86_64.whl (96 kB)
     |████████████████████████████████| 96 kB 7.1 MB/s 
Collecting nbconvert
  Downloading nbconvert-6.2.0-py3-none-any.whl (553 kB)
     |████████████████████████████████| 553 kB 83.0 MB/s 
Collecting terminado>=0.8.3
  Downloading terminado-0.12.1-py3-none-any.whl (15 kB)
Collecting prometheus-client
  Using cached prometheus_client-0.11.0-py2.py3-none-any.whl (56 kB)
Collecting Send2Trash>=1.5.0
  Downloading Send2Trash-1.8.0-py3-none-any.whl (18 kB)
Collecting jinja2
  Downloading Jinja2-3.0.2-py3-none-any.whl (133 kB)
     |████████████████████████████████| 133 kB 72.4 MB/s 
Collecting cffi>=1.0.0
  Downloading cffi-1.14.6-cp37-cp37m-manylinux1_x86_64.whl (402 kB)
     |████████████████████████████████| 402 kB 75.0 MB/s 
Collecting pycparser
  Using cached pycparser-2.20-py2.py3-none-any.whl (112 kB)
Collecting botocore<1.22.0,>=1.21.54
  Downloading botocore-1.21.54-py3-none-any.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 61.0 MB/s 
Collecting s3transfer<0.6.0,>=0.5.0
  Downloading s3transfer-0.5.0-py3-none-any.whl (79 kB)
     |████████████████████████████████| 79 kB 10.1 MB/s 
Collecting jmespath<1.0.0,>=0.7.1
  Using cached jmespath-0.10.0-py2.py3-none-any.whl (24 kB)
Collecting urllib3<1.27,>=1.25.4
  Downloading urllib3-1.26.7-py2.py3-none-any.whl (138 kB)
     |████████████████████████████████| 138 kB 86.2 MB/s 
Collecting cached-property
  Using cached cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Collecting MarkupSafe>=2.0
  Downloading MarkupSafe-2.0.1-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (31 kB)
Collecting bleach
  Downloading bleach-4.1.0-py2.py3-none-any.whl (157 kB)
     |████████████████████████████████| 157 kB 76.8 MB/s 
Collecting jupyterlab-pygments
  Using cached jupyterlab_pygments-0.1.2-py2.py3-none-any.whl (4.6 kB)
Collecting defusedxml
  Using cached defusedxml-0.7.1-py2.py3-none-any.whl (25 kB)
Collecting mistune<2,>=0.8.1
  Using cached mistune-0.8.4-py2.py3-none-any.whl (16 kB)
Collecting pandocfilters>=1.4.1
  Downloading pandocfilters-1.5.0-py2.py3-none-any.whl (8.7 kB)
Collecting nbclient<0.6.0,>=0.5.0
  Downloading nbclient-0.5.4-py3-none-any.whl (66 kB)
     |████████████████████████████████| 66 kB 5.1 MB/s 
Collecting testpath
  Using cached testpath-0.5.0-py3-none-any.whl (84 kB)
Collecting packaging
  Using cached packaging-21.0-py3-none-any.whl (40 kB)
Collecting webencodings
  Using cached webencodings-0.5.1-py2.py3-none-any.whl (11 kB)
Collecting pyparsing>=2.0.2
  Using cached pyparsing-2.4.7-py2.py3-none-any.whl (67 kB)
Collecting charset-normalizer~=2.0.0
  Downloading charset_normalizer-2.0.6-py3-none-any.whl (37 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages (from requests->transformers==2.8.0->-r requirements.txt (line 5)) (2021.5.30)
Collecting idna<4,>=2.5
  Using cached idna-3.2-py3-none-any.whl (59 kB)
Collecting click
  Using cached click-8.0.1-py3-none-any.whl (97 kB)
Collecting sphinxcontrib-applehelp
  Downloading sphinxcontrib_applehelp-1.0.2-py2.py3-none-any.whl (121 kB)
     |████████████████████████████████| 121 kB 31.5 MB/s 
Collecting docutils<0.18,>=0.14
  Downloading docutils-0.17.1-py2.py3-none-any.whl (575 kB)
     |████████████████████████████████| 575 kB 75.9 MB/s 
Collecting babel>=1.3
  Downloading Babel-2.9.1-py2.py3-none-any.whl (8.8 MB)
     |████████████████████████████████| 8.8 MB 30.0 MB/s 
Collecting sphinxcontrib-devhelp
  Downloading sphinxcontrib_devhelp-1.0.2-py2.py3-none-any.whl (84 kB)
     |████████████████████████████████| 84 kB 3.0 MB/s 
Collecting imagesize
  Downloading imagesize-1.2.0-py2.py3-none-any.whl (4.8 kB)
Collecting sphinxcontrib-serializinghtml>=1.1.5
  Downloading sphinxcontrib_serializinghtml-1.1.5-py2.py3-none-any.whl (94 kB)
     |████████████████████████████████| 94 kB 2.8 MB/s 
Collecting sphinxcontrib-qthelp
  Downloading sphinxcontrib_qthelp-1.0.3-py2.py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 11.9 MB/s 
Collecting alabaster<0.8,>=0.7
  Downloading alabaster-0.7.12-py2.py3-none-any.whl (14 kB)
Collecting snowballstemmer>=1.1
  Downloading snowballstemmer-2.1.0-py2.py3-none-any.whl (93 kB)
     |████████████████████████████████| 93 kB 2.0 MB/s 
Collecting sphinxcontrib-jsmath
  Downloading sphinxcontrib_jsmath-1.0.1-py2.py3-none-any.whl (5.1 kB)
Collecting sphinxcontrib-htmlhelp>=2.0.0
  Downloading sphinxcontrib_htmlhelp-2.0.0-py2.py3-none-any.whl (100 kB)
     |████████████████████████████████| 100 kB 10.9 MB/s 
Building wheels for collected packages: seqeval, gast, termcolor
  Building wheel for seqeval (setup.py) ... done
  Created wheel for seqeval: filename=seqeval-0.0.12-py3-none-any.whl size=7434 sha256=9e60977325f67d9b0cb92eb1c5796261a3bb46599be5310ec93ccc386d136b42
  Stored in directory: /home/ye/.cache/pip/wheels/dc/cc/62/a3b81f92d35a80e39eb9b2a9d8b31abac54c02b21b2d466edc
  Building wheel for gast (setup.py) ... done
  Created wheel for gast: filename=gast-0.2.2-py3-none-any.whl size=7554 sha256=e1d9aaf31113ab8f79d041174fd45a179bdc2b5e7d38dd53edb208c7fd3a650c
  Stored in directory: /home/ye/.cache/pip/wheels/21/7f/02/420f32a803f7d0967b48dd823da3f558c5166991bfd204eef3
  Building wheel for termcolor (setup.py) ... done
  Created wheel for termcolor: filename=termcolor-1.1.0-py3-none-any.whl size=4847 sha256=3896fb453334a54d801441a752d3fe6d871215c6235b03151f99999bf5a2cc88
  Stored in directory: /home/ye/.cache/pip/wheels/3f/e3/ec/8a8336ff196023622fbcb36de0c5a5c218cbb24111d1d4c7f2
Successfully built seqeval gast termcolor
Installing collected packages: zipp, typing-extensions, traitlets, six, pyrsistent, importlib-metadata, attrs, wcwidth, tornado, pyzmq, python-dateutil, pyparsing, ptyprocess, parso, nest-asyncio, jupyter-core, jsonschema, ipython-genutils, entrypoints, webencodings, pygments, pycparser, prompt-toolkit, pickleshare, pexpect, packaging, nbformat, matplotlib-inline, MarkupSafe, jupyter-client, jedi, decorator, backcall, urllib3, testpath, pandocfilters, numpy, nbclient, mistune, jupyterlab-pygments, jmespath, jinja2, ipython, defusedxml, debugpy, cffi, cached-property, bleach, argcomplete, terminado, Send2Trash, pytz, prometheus-client, nbconvert, ipykernel, idna, h5py, charset-normalizer, botocore, argon2-cffi, werkzeug, tqdm, sphinxcontrib-serializinghtml, sphinxcontrib-qthelp, sphinxcontrib-jsmath, sphinxcontrib-htmlhelp, sphinxcontrib-devhelp, sphinxcontrib-applehelp, snowballstemmer, scipy, s3transfer, requests, regex, PyYAML, protobuf, notebook, markdown, keras-preprocessing, keras-applications, joblib, imagesize, grpcio, docutils, click, babel, alabaster, absl-py, wrapt, widgetsnbextension, tokenizers, threadpoolctl, termcolor, tensorflow-estimator, tensorboard, sphinx, sentencepiece, sacremoses, opt-einsum, Keras, google-pasta, gast, filelock, boto3, astor, transformers, torch, tensorflow, sphinx-rtd-theme, seqeval, scikit-learn, pandas, ipywidgets
Successfully installed Keras-2.3.1 MarkupSafe-2.0.1 PyYAML-5.3.1 Send2Trash-1.8.0 absl-py-0.14.1 alabaster-0.7.12 argcomplete-1.12.3 argon2-cffi-21.1.0 astor-0.8.1 attrs-21.2.0 babel-2.9.1 backcall-0.2.0 bleach-4.1.0 boto3-1.18.54 botocore-1.21.54 cached-property-1.5.2 cffi-1.14.6 charset-normalizer-2.0.6 click-8.0.1 debugpy-1.5.0 decorator-5.1.0 defusedxml-0.7.1 docutils-0.17.1 entrypoints-0.3 filelock-3.3.0 gast-0.2.2 google-pasta-0.2.0 grpcio-1.41.0 h5py-3.4.0 idna-3.2 imagesize-1.2.0 importlib-metadata-4.8.1 ipykernel-6.4.1 ipython-7.28.0 ipython-genutils-0.2.0 ipywidgets-7.4.2 jedi-0.18.0 jinja2-3.0.2 jmespath-0.10.0 joblib-0.13.2 jsonschema-4.0.1 jupyter-client-7.0.5 jupyter-core-4.8.1 jupyterlab-pygments-0.1.2 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.3.4 matplotlib-inline-0.1.3 mistune-0.8.4 nbclient-0.5.4 nbconvert-6.2.0 nbformat-5.1.3 nest-asyncio-1.5.1 notebook-6.4.4 numpy-1.18.1 opt-einsum-3.3.0 packaging-21.0 pandas-1.0.1 pandocfilters-1.5.0 parso-0.8.2 pexpect-4.8.0 pickleshare-0.7.5 prometheus-client-0.11.0 prompt-toolkit-3.0.20 protobuf-3.18.0 ptyprocess-0.7.0 pycparser-2.20 pygments-2.10.0 pyparsing-2.4.7 pyrsistent-0.18.0 python-dateutil-2.8.2 pytz-2021.3 pyzmq-22.3.0 regex-2021.9.30 requests-2.26.0 s3transfer-0.5.0 sacremoses-0.0.46 scikit-learn-0.23.1 scipy-1.7.1 sentencepiece-0.1.96 seqeval-0.0.12 six-1.16.0 snowballstemmer-2.1.0 sphinx-4.2.0 sphinx-rtd-theme-0.4.3 sphinxcontrib-applehelp-1.0.2 sphinxcontrib-devhelp-1.0.2 sphinxcontrib-htmlhelp-2.0.0 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.3 sphinxcontrib-serializinghtml-1.1.5 tensorboard-1.15.0 tensorflow-1.15.2 tensorflow-estimator-1.15.1 termcolor-1.1.0 terminado-0.12.1 testpath-0.5.0 threadpoolctl-3.0.0 tokenizers-0.5.2 torch-1.2.0 tornado-6.1 tqdm-4.30.0 traitlets-5.1.0 transformers-2.8.0 typing-extensions-3.10.0.2 urllib3-1.26.7 wcwidth-0.2.5 webencodings-0.5.1 werkzeug-2.0.1 widgetsnbextension-3.4.2 wrapt-1.13.1 zipp-3.6.0
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ 
```

## Test Run coNLL NER-POS Tasks

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/coNLL_data$ ls
coNLL_testa.txt  coNLL_testb.txt  coNLL_train.txt
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/coNLL_data$ wc *
  55045  206312  827012 coNLL_testa.txt
  50351  186664  748096 coNLL_testb.txt
 219554  818268 3281528 coNLL_train.txt
 324950 1211244 4856636 total
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/coNLL_data$ head *
==> coNLL_testa.txt <==
-DOCSTART- -X- O O

CRICKET NNP I-NP O
- : O O
LEICESTERSHIRE NNP I-NP I-ORG
TAKE NNP I-NP O
OVER IN I-PP O
AT NNP I-NP O
TOP NNP I-NP O
AFTER NNP I-NP O

==> coNLL_testb.txt <==
-DOCSTART- -X- -X- O

SOCCER NN I-NP O
- : O O
JAPAN NNP I-NP I-LOC
GET VB I-VP O
LUCKY NNP I-NP O
WIN NNP I-NP O
, , O O
CHINA NNP I-NP I-PER

==> coNLL_train.txt <==
-DOCSTART- -X- O O

EU NNP I-NP I-ORG
rejects VBZ I-VP O
German JJ I-NP I-MISC
call NN I-NP O
to TO I-VP O
boycott VB I-VP O
British JJ I-NP I-MISC
lamb NN I-NP O
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/coNLL_data
```

Got Error! as follows:  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ time python ./data_preparation.py --task_file /home/ye/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/tasks_file_conll.yml --data_dir /home/ye/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/coNLL_data/ --max_seq_len 50
Using TensorFlow backend.
Traceback (most recent call last):
  File "./data_preparation.py", line 314, in <module>
    main()
  File "./data_preparation.py", line 284, in main
    tasks = TasksParam(args.task_file)
  File "/home/ye/exp/multi-task/multi-task-NLP/utils/task_utils.py", line 76, in __init__
    labelMap[taskName] = joblib.load(taskVals["label_map_or_file"])
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/joblib/numpy_pickle.py", line 590, in load
    with open(filename, 'rb') as f:
FileNotFoundError: [Errno 2] No such file or directory: '../../data/ner_coNLL_train_label_map.joblib'

real	0m1.494s
user	0m1.555s
sys	0m1.153s
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$
```

## Data Transformation

I need to transform the data format, at first ...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../data_transformations.py --transform_file ./transform_file_conll.yml 
Making data from file coNLL_train.txt ...
Processing 0 rows...
Processing 5000 rows...
Processing 10000 rows...
Processing 15000 rows...
Processing 20000 rows...
Processing 25000 rows...
Processing 30000 rows...
Processing 35000 rows...
Processing 40000 rows...
Processing 45000 rows...
Processing 50000 rows...
Processing 55000 rows...
Processing 60000 rows...
Processing 65000 rows...
Processing 70000 rows...
Processing 75000 rows...
Processing 80000 rows...
Processing 85000 rows...
Processing 90000 rows...
Processing 95000 rows...
Processing 100000 rows...
Processing 105000 rows...
Processing 110000 rows...
Processing 115000 rows...
Processing 120000 rows...
Processing 125000 rows...
Processing 130000 rows...
Processing 135000 rows...
Processing 140000 rows...
Processing 145000 rows...
Processing 150000 rows...
Processing 155000 rows...
Processing 160000 rows...
Processing 165000 rows...
Processing 170000 rows...
Processing 175000 rows...
Processing 180000 rows...
Processing 185000 rows...
Processing 190000 rows...
Processing 195000 rows...
Processing 200000 rows...
Processing 205000 rows...
Processing 210000 rows...
Processing 215000 rows...
NER File Written at ../../data
POS File Written at ../../data
Created NER label map from train file coNLL_train.txt
{'I-ORG': 0, 'O': 1, 'I-MISC': 2, 'I-PER': 3, 'I-LOC': 4, 'B-LOC': 5, 'B-MISC': 6, 'B-ORG': 7}
label Map NER written at ../../data/ner_coNLL_train_label_map.joblib
Created POS label map from train file coNLL_train.txt
{'I-NP': 0, 'I-VP': 1, 'O': 2, 'I-PP': 3, 'B-NP': 4, 'I-SBAR': 5, 'I-ADJP': 6, 'I-ADVP': 7, 'I-PRT': 8, 'B-VP': 9, 'B-PP': 10, 'I-CONJP': 11, 'I-INTJ': 12, 'I-LST': 13, 'B-ADVP': 14, 'B-SBAR': 15, 'B-ADJP': 16}
label Map POS written at ../../data/pos_coNLL_train_label_map.joblib
Max len of sentence:  113
Mean len of sentences:  14.501887329962253
Median len of sentences:  10
Making data from file coNLL_testa.txt ...
Processing 0 rows...
Processing 5000 rows...
Processing 10000 rows...
Processing 15000 rows...
Processing 20000 rows...
Processing 25000 rows...
Processing 30000 rows...
Processing 35000 rows...
Processing 40000 rows...
Processing 45000 rows...
Processing 50000 rows...
Processing 55000 rows...
NER File Written at ../../data
POS File Written at ../../data
Max len of sentence:  109
Mean len of sentences:  15.803692307692307
Median len of sentences:  11.0
Making data from file coNLL_testb.txt ...
Processing 0 rows...
Processing 5000 rows...
Processing 10000 rows...
Processing 15000 rows...
Processing 20000 rows...
Processing 25000 rows...
Processing 30000 rows...
Processing 35000 rows...
Processing 40000 rows...
Processing 45000 rows...
Processing 50000 rows...
NER File Written at ../../data
POS File Written at ../../data
Max len of sentence:  124
Mean len of sentences:  13.447726614538082
Median len of sentences:  9

real	0m1.853s
user	0m1.953s
sys	0m0.790s
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ 
```

## Data Preparation

python ../../data_preparation.py --task_file 'tasks_file_conll.yml'  --data_dir '../../data' --max_seq_len 50

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../data_preparation.py --task_file 'tasks_file_conll.yml'  --data_dir '../../data' --max_seq_len 50
Using TensorFlow backend.
task object created from task file...
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 232k/232k [00:01<00:00, 218kB/s]
bert model tokenizer loaded for config bert-base-uncased
Loading raw data for task conllner from ../../data/ner_coNLL_train.tsv
Processing Started...
Data Size:  14041
number of threads:  7
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1774.97it/s]
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 2000.40it/sData Processing done for conllner. File saved at ../../data/bert-base-uncased_prepared_data/ner_conll_train.json███| 2005/2005 [00:00<00:00, 2144.09it/s]
Loading raw data for task conllner from ../../data/ner_coNLL_testa.tsv████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1799.38it/s]
Processing Started...██████████████████████████████████████████████████████████████████████████████████▋          | 1816/2005 [00:01<00:00, 1562.13it/s]
Data Size:  3250██████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1694.24it/s]
number of threads:  7█████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1645.31it/s]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 2143.47it/s]
 78%|██████████████████████████████████████████████████████████████████████████████████████▌                        | 362/464 [00:00<00:00, 1864.56it/sData Processing done for conllner. File saved at ../../data/bert-base-uncased_prepared_data/ner_conll_testa.json█████| 464/464 [00:00<00:00, 1646.63it/s]
Loading raw data for task conllner from ../../data/ner_coNLL_testb.tsv██████████████████████████████████████████████| 464/464 [00:00<00:00, 1336.75it/s]
Processing Started...███████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 1583.06it/s]
Data Size:  3453████████████████████████████████████▊                                                               | 200/464 [00:00<00:00, 1989.04it/s]
number of threads:  7███████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 1651.06it/s]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 2106.58it/s]
 91%|████████████████████████████████████████████████████████████████████████████████████████████████████▊          | 448/493 [00:00<00:00, 2257.11it/sData Processing done for conllner. File saved at ../../data/bert-base-uncased_prepared_data/ner_conll_testb.json█████| 493/493 [00:00<00:00, 2018.51it/s]
Loading raw data for task conllpos from ../../data/pos_coNLL_train.tsv██████████████████████████████████████████████| 493/493 [00:00<00:00, 1423.96it/s]
Processing Started...███████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 1540.37it/s]
Data Size:  14041███████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 1532.40it/s]
number of threads:  7███████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 2679.90it/s]
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1743.92it/s]
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1950.53it/sData Processing done for conllpos. File saved at ../../data/bert-base-uncased_prepared_data/pos_conll_train.json███| 2005/2005 [00:00<00:00, 2092.23it/s]
Loading raw data for task conllpos from ../../data/pos_coNLL_testa.tsv████████████████████████████████████▏       | 1861/2005 [00:01<00:00, 1610.05it/s]
Processing Started...█████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1763.08it/s]
Data Size:  3250██████████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1685.94it/s]
number of threads:  7█████████████████████████████████████████████████████████████████████████████████████████████| 2005/2005 [00:01<00:00, 1635.52it/s]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 2087.33it/s]
 77%|█████████████████████████████████████████████████████████████████████████████████████▋                         | 358/464 [00:00<00:00, 1843.83it/sData Processing done for conllpos. File saved at ../../data/bert-base-uncased_prepared_data/pos_conll_testa.json█████| 464/464 [00:00<00:00, 1614.95it/s]
Loading raw data for task conllpos from ../../data/pos_coNLL_testb.tsv██████████████████████████████████████████████| 464/464 [00:00<00:00, 1313.53it/s]
Processing Started...███████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 1553.61it/s]
Data Size:  3453████████████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 2411.00it/s]
number of threads:  7███████████████████████████████████████████████████████████████████████████████████████████████| 464/464 [00:00<00:00, 1610.17it/s]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 2062.73it/s]
 91%|████████████████████████████████████████████████████████████████████████████████████████████████████▊          | 448/493 [00:00<00:00, 2258.14it/sData Processing done for conllpos. File saved at ../../data/bert-base-uncased_prepared_data/pos_conll_testb.json█████| 493/493 [00:00<00:00, 2017.60it/s]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 1437.57it/s]
real|███0m11.813s███████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 1555.11it/s]
user|███0m27.849s███████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 1546.50it/s]
sys%|███0m1.798s████████████████████████████████████████████████████████████████████████████████████████████████████| 493/493 [00:00<00:00, 2572.56it/s]
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$
```

## Check Data (tsv data)

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ ls *.tsv
ner_coNLL_testa.tsv  ner_coNLL_testb.tsv  ner_coNLL_train.tsv  pos_coNLL_testa.tsv  pos_coNLL_testb.tsv  pos_coNLL_train.tsv
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ 
```

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ head -n 3 ./ner_coNLL_train.tsv 
0	['I-ORG', 'O', 'I-MISC', 'O', 'O', 'O', 'I-MISC', 'O', 'O']	['EU', 'rejects', 'German', 'call', 'to', 'boycott', 'British', 'lamb', '.']
1	['I-PER', 'I-PER']	['Peter', 'Blackburn']
2	['I-LOC', 'O']	['BRUSSELS', '1996-08-22']
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ head -n 3 ./ner_coNLL_testa.tsv 
0	['O', 'O', 'I-ORG', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O']	['CRICKET', '-', 'LEICESTERSHIRE', 'TAKE', 'OVER', 'AT', 'TOP', 'AFTER', 'INNINGS', 'VICTORY', '.']
1	['I-LOC', 'O']	['LONDON', '1996-08-30']
2	['I-MISC', 'I-MISC', 'O', 'I-PER', 'I-PER', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'I-ORG', 'O', 'I-ORG', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O']	['West', 'Indian', 'all-rounder', 'Phil', 'Simmons', 'took', 'four', 'for', '38', 'on', 'Friday', 'as', 'Leicestershire', 'beat', 'Somerset', 'by', 'an', 'innings', 'and', '39', 'runs', 'in', 'two', 'days', 'to', 'take', 'over', 'at', 'the', 'head', 'of', 'the', 'county', 'championship', '.']
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ 
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ head -n 3 ./pos_coNLL_train.tsv 
0	['I-NP', 'I-VP', 'I-NP', 'I-NP', 'I-VP', 'I-VP', 'I-NP', 'I-NP', 'O']	['EU', 'rejects', 'German', 'call', 'to', 'boycott', 'British', 'lamb', '.']
1	['I-NP', 'I-NP']	['Peter', 'Blackburn']
2	['I-NP', 'I-NP']	['BRUSSELS', '1996-08-22']
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ 
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ head -n 3 ./pos_coNLL_testb.tsv 
0	['I-NP', 'O', 'I-NP', 'I-VP', 'I-NP', 'I-NP', 'O', 'I-NP', 'I-PP', 'I-NP', 'I-NP', 'O']	['SOCCER', '-', 'JAPAN', 'GET', 'LUCKY', 'WIN', ',', 'CHINA', 'IN', 'SURPRISE', 'DEFEAT', '.']
1	['I-NP', 'I-NP']	['Nadim', 'Ladki']
2	['I-NP', 'O', 'I-NP', 'I-NP', 'I-NP', 'I-NP']	['AL-AIN', ',', 'United', 'Arab', 'Emirates', '1996-12-06']
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data$ 
```

## Check bert-base-uncased_prepared_data (json data)

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ ls
ner_conll_testa.json  ner_conll_testb.json  ner_conll_train.json  pos_conll_testa.json  pos_conll_testb.json  pos_conll_train.json
```

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ head -n 3 ./pos_conll_train.json
{"uid": "4010", "label": [17, 0, 3, 0, 0, 0, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 2765, 1997, 3803, 2034, 2407, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "4011", "label": [17, 0, 0, 1, 3, 0, 2, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 4715, 2674, 2209, 2006, 5095, 1024, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "4012", "label": [17, 0, 19, 19, 19, 19, 0, 19, 19, 19, 0, 0, 19, 19, 0, 19, 19, 19, 0, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 24665, 11057, 10343, 7507, 2361, 18629, 7629, 5403, 2213, 1017, 1054, 2243, 2278, 11333, 2389, 9148, 15992, 1016, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ head -n 3 ./pos_conll_testb.json 
{"uid": "2465", "label": [17, 0, 19, 0, 0, 19, 19, 2, 0, 2, 0, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 2184, 1027, 7701, 16137, 25389, 2050, 1006, 2605, 1007, 4868, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "2466", "label": [17, 0, 19, 0, 19, 19, 0, 2, 0, 19, 19, 19, 2, 0, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 2410, 1027, 27263, 7875, 2080, 2395, 1006, 1057, 1012, 1055, 1012, 1007, 2753, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "2467", "label": [17, 0, 19, 0, 19, 0, 2, 0, 2, 0, 18, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], "token_id": [101, 2410, 1027, 8852, 2666, 24253, 1006, 5118, 1007, 2753, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ head -n 3 ./ner_conll_train.json 
{"uid": "4010", "label": [8, 1, 1, 2, 1, 1, 9, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1], "token_id": [101, 2765, 1997, 3803, 2034, 2407, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "4011", "label": [8, 1, 1, 1, 1, 1, 1, 9, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1], "token_id": [101, 4715, 2674, 2209, 2006, 5095, 1024, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "4012", "label": [8, 0, 10, 10, 10, 10, 0, 10, 10, 10, 1, 0, 10, 10, 0, 10, 10, 10, 1, 9, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1], "token_id": [101, 24665, 11057, 10343, 7507, 2361, 18629, 7629, 5403, 2213, 1017, 1054, 2243, 2278, 11333, 2389, 9148, 15992, 1016, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ head -n 3 ./ner_conll_testa.json 
{"uid": "1856", "label": [8, 1, 4, 1, 3, 3, 10, 10, 10, 1, 1, 1, 1, 1, 1, 1, 3, 3, 10, 10, 1, 1, 1, 10, 10, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 10, 10, 10, 1, 10, 1, 0, 0, 0, 1, 10, 10, 1, 9], "token_id": [101, 1999, 9182, 1010, 4913, 10093, 5603, 14728, 2099, 7932, 2698, 4978, 2058, 2809, 7202, 1998, 2928, 11338, 2290, 20357, 2718, 2010, 2350, 1011, 2223, 2877, 24634, 11525, 1998, 5225, 1999, 2093, 3216, 2004, 1996, 2012, 27065, 10415, 2015, 8744, 2098, 1996, 3731, 2417, 9175, 1021, 1011, 1014, 1012, 102], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]}
{"uid": "1857", "label": [8, 3, 10, 10, 10, 1, 1, 10, 10, 1, 1, 1, 1, 1, 10, 10, 1, 1, 1, 9, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1], "token_id": [101, 10093, 5603, 14728, 2099, 1006, 1016, 1011, 1019, 1007, 5941, 1037, 3167, 2093, 1011, 2208, 3974, 9039, 1012, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
{"uid": "1858", "label": [8, 3, 3, 1, 1, 1, 1, 1, 1, 9, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1], "token_id": [101, 8937, 18087, 8219, 1037, 3819, 6619, 12994, 1012, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "type_id": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "mask": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/data/bert-base-uncased_prepared_data$ 
```

## Training

When I train, I got module not found error ...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../train.py \
>     --data_dir '../../data/bert-base-uncased_prepared_data' \
>     --task_file 'tasks_file_conll.yml' \
>     --out_dir 'conll_ner_pos_bert_base' \
>     --epochs 10 \
>     --train_batch_size 32 \
>     --eval_batch_size 32 \
>     --grad_accumulation_steps 1 \
>     --log_per_updates 50 \
>     --max_seq_len 50 \
>     --eval_while_train \
>     --test_while_train \
>     --silent 2>&1 | tee ./training.log
Traceback (most recent call last):
  File "../../train.py", line 14, in <module>
    from torch.utils.tensorboard import SummaryWriter
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/utils/tensorboard/__init__.py", line 6, in <module>
    from .writer import FileWriter, SummaryWriter  # noqa F401
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/utils/tensorboard/writer.py", line 18, in <module>
    from ._convert_np import make_np
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/utils/tensorboard/_convert_np.py", line 12, in <module>
    from caffe2.python import workspace
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/caffe2/python/workspace.py", line 15, in <module>
    from past.builtins import basestring
ModuleNotFoundError: No module named 'past'

real	0m0.431s
user	0m0.510s
sys	0m0.529s
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ 
```

Install module ...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ pip install future
Collecting future
  Using cached future-0.18.2.tar.gz (829 kB)
Building wheels for collected packages: future
  Building wheel for future (setup.py) ... done
  Created wheel for future: filename=future-0.18.2-py3-none-any.whl size=491070 sha256=5edb8c349cf57add7c99b3bfa15b151f6b2de86fff140db719a161803c3a306f
  Stored in directory: /home/ye/.cache/pip/wheels/56/b0/fe/4410d17b32f1f0c3cf54cdfb2bc04d7b4b8f4ae377e2229ba0
Successfully built future
Installing collected packages: future
Successfully installed future-0.18.2
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$
```

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../train.py     --data_dir '../../data/bert-base-uncased_prepared_data'     --task_file 'tasks_file_conll.yml'     --out_dir 'conll_ner_pos_bert_base'     --epochs 10     --train_batch_size 32     --eval_batch_size 32     --grad_accumulation_steps 1     --log_per_updates 50     --max_seq_len 50     --eval_while_train     --test_while_train     --silent 2>&1 | tee ./training.log
...
...
...
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/nn/modules/module.py", line 547, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/transformers/modeling_bert.py", line 368, in forward
    self_attention_outputs = self.attention(hidden_states, attention_mask, head_mask)
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/nn/modules/module.py", line 547, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/transformers/modeling_bert.py", line 314, in forward
    hidden_states, attention_mask, head_mask, encoder_hidden_states, encoder_attention_mask
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/nn/modules/module.py", line 547, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/transformers/modeling_bert.py", line 251, in forward
    context_layer = torch.matmul(attention_probs, value_layer)
RuntimeError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 3.94 GiB total capacity; 1.94 GiB already allocated; 38.06 MiB free; 116.65 MiB cached)


real	6m22.170s
user	0m26.413s
sys	0m6.477s
```

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../train.py     --data_dir '../../data/bert-base-uncased_prepared_data'     --task_file 'tasks_file_conll.yml'     --out_dir 'conll_ner_pos_bert_base'     --epochs 10     --train_batch_size 16     --eval_batch_size 16     --grad_accumulation_steps 1     --log_per_updates 50     --max_seq_len 50     --eval_while_train     --test_while_train     --silent 2>&1 | tee ./training.log
```

Batch size ကို 16 ထားလည်း CUDA out of memory error ပဲ ပေးနေတယ်...  
စက်ကို restart လုပ်ပြီး try ကြည့်ခဲ့...  

ဒီ တစ်ခေါက်တော့ run လို့ ရသွားခဲ့....  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$ time python ../../train.py     --data_dir '../../data/bert-base-uncased_prepared_data'     --task_file 'tasks_file_conll.yml'     --out_dir 'conll_ner_pos_bert_base'     --epochs 10     --train_batch_size 32     --eval_batch_size 32     --grad_accumulation_steps 1     --log_per_updates 50     --max_seq_len 50     --eval_while_train     --test_while_train     --silent 2>&1 | tee ./training.log
Epoch: 0: 100%|██████████| 878/878 [13:13<00:/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/nn/functional.py:1350: UserWarning: nn.functional.sigmoid is deprecated. Use torch.sigmoid instead.
  warnings.warn("nn.functional.sigmoid is deprecated. Use torch.sigmoid instead.")

Eval: 100%|██████████| 216/216 [01:05<00:00,  3.28it/s]
realh: 1153m15.256s██████| 878/878 [13:11<00:00,  1.12it/s]
userh: 2187m58.869s██████| 878/878 [13:07<00:00,  1.11it/s]
sysch: 33m14.025s████████| 878/878 [13:07<00:00,  1.12it/s]
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging$
```

multi_task_logs.log ထဲကို ဝင်ကြည့်ရင် dev အတွက် evaluation ရော test အတွက် evaluation ရလဒ်တွေရော ကြည့်လို့ ရလို့ အဆင်ပြေတယ်။  

```
INFO - logger created.
INFO - ARGS : {'data_dir': '../../data/bert-base-uncased_prepared_data', 'task_file': 'tasks_file_conll.yml', 'out_dir': 'conll_ner_pos_bert_base', 'epochs': 10, 'freeze_shared_model': False, 'train_batch_size': 32, 'eval_batch_size': 32, 'grad_accumulation_steps': 1, 'num_of_warmup_steps': 0, 'learning_rate': 2e-05, 'epsilon': 1e-08, 'grad_clip_value': 1.0, 'log_file': 'multi_task_logs.log', 'log_per_updates': 50, 'seed': 42, 'max_seq_len': 50, 'save_per_updates': 0, 'limit_save': 10, 'load_saved_model': None, 'eval_while_train': True, 'test_while_train': True, 'resume_train': False, 'finetune': False, 'debug_mode': False, 'silent': True}
INFO - Task params object created from task file...
INFO - task parameters:
 {'conllner': {'model_type': 'BERT', 'config_name': 'bert-base-uncased', 'dropout_prob': 0.2, 'label_map_or_file': '../../data/ner_coNLL_train_label_map.joblib', 'metrics': ['seqeval_f1_score', 'seqeval_precision', 'seqeval_recall'], 'loss_type': 'NERLoss', 'task_type': 'NER', 'file_names': ['ner_coNLL_train.tsv', 'ner_coNLL_testa.tsv', 'ner_coNLL_testb.tsv']}, 'conllpos': {'model_type': 'BERT', 'config_name': 'bert-base-uncased', 'dropout_prob': 0.2, 'label_map_or_file': '../../data/pos_coNLL_train_label_map.joblib', 'metrics': ['seqeval_f1_score', 'seqeval_precision', 'seqeval_recall'], 'loss_type': 'NERLoss', 'task_type': 'NER', 'file_names': ['pos_coNLL_train.tsv', 'pos_coNLL_testa.tsv', 'pos_coNLL_testb.tsv']}}
INFO - Tensorboard writing at 05_10-14_05/tb_logs
INFO - Creating data handlers for training...
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/ner_conll_train.json
INFO - Read Data for Task Id: 0 Task Name: conllner. Samples 14035
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/pos_conll_train.json
INFO - Read Data for Task Id: 1 Task Name: conllpos. Samples 14035
INFO - Creating data handlers for dev...
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/ner_conll_testa.json
INFO - Read Data for Task Id: 0 Task Name: conllner. Samples 3248
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/pos_conll_testa.json
INFO - Read Data for Task Id: 1 Task Name: conllpos. Samples 3248
INFO - Creating data handlers for test...
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/ner_conll_testb.json
INFO - Read Data for Task Id: 0 Task Name: conllner. Samples 3451
INFO - Reading data from file ../../data/bert-base-uncased_prepared_data/pos_conll_testb.json
INFO - Read Data for Task Id: 1 Task Name: conllpos. Samples 3451
INFO - NUM TRAIN STEPS: 8780
INFO - len of dataloader: 28070
INFO - Making multi-task model...
INFO - Using number of gpus: 2
INFO - Making shared model from given config name bert-base-uncased
INFO - 
####################### EPOCH 0 ###################

INFO - Steps: 50 Task: conllpos Avg.Loss: 1.7239872598648072 Task Loss: 1.414986252784729
INFO - Steps: 100 Task: conllpos Avg.Loss: 1.36918670296669 Task Loss: 0.6738380193710327
INFO - Steps: 150 Task: conllner Avg.Loss: 1.2072594718138376 Task Loss: 0.8379039168357849
INFO - Steps: 200 Task: conllner Avg.Loss: 1.0924078424274921 Task Loss: 0.8594430088996887
INFO - Steps: 250 Task: conllner Avg.Loss: 1.017382009267807 Task Loss: 0.7388234734535217
INFO - Steps: 300 Task: conllner Avg.Loss: 0.9604781742890676 Task Loss: 0.6197634935379028
INFO - Steps: 350 Task: conllner Avg.Loss: 0.9207684230804444 Task Loss: 0.6452434062957764
INFO - Steps: 400 Task: conllner Avg.Loss: 0.8841711015999317 Task Loss: 0.5846939086914062
INFO - Steps: 450 Task: conllpos Avg.Loss: 0.8501960169606738 Task Loss: 0.6187164187431335
INFO - Steps: 500 Task: conllner Avg.Loss: 0.8252821534276008 Task Loss: 0.5873832702636719
INFO - Steps: 550 Task: conllpos Avg.Loss: 0.7984397469325499 Task Loss: 0.5108623504638672
INFO - Steps: 600 Task: conllpos Avg.Loss: 0.7740134423101942 Task Loss: 0.575387179851532
INFO - Steps: 650 Task: conllner Avg.Loss: 0.7555600627912925 Task Loss: 0.4296213388442993
INFO - Steps: 700 Task: conllpos Avg.Loss: 0.7371033015102149 Task Loss: 0.2300920933485031
INFO - Steps: 750 Task: conllner Avg.Loss: 0.7206065048873425 Task Loss: 0.4758446514606476
INFO - Steps: 800 Task: conllpos Avg.Loss: 0.7057694440428167 Task Loss: 0.40741854906082153
INFO - Steps: 850 Task: conllpos Avg.Loss: 0.690859402900233 Task Loss: 0.43298253417015076
INFO - model saved in 878 global step at conll_ner_pos_bert_base/multi_task_model_0_878.pt
INFO - 
Running Evaluation on dev...
INFO - ********** conllner Evaluation************

INFO - seqeval_f1_score : 0.3494130751435181
INFO - seqeval_precision : 0.3484278879015721
INFO - seqeval_recall : 0.35040384945866987
INFO - ********** conllpos Evaluation************

INFO - seqeval_f1_score : 0.5878378378378378
INFO - seqeval_precision : 0.5509171628179096
INFO - seqeval_recall : 0.6300625811784154
INFO - 
Running Evaluation on test...
INFO - ********** conllner Evaluation************

INFO - seqeval_f1_score : 0.34997372569626906
INFO - seqeval_precision : 0.3391038696537678
INFO - seqeval_recall : 0.36156351791530944
INFO - ********** conllpos Evaluation************

INFO - seqeval_f1_score : 0.5681166804662122
INFO - seqeval_precision : 0.5281231497927767
INFO - seqeval_recall : 0.6146637265711136
INFO - Predictions File saved at conll_ner_pos_bert_base/conllner_test_predictions_0.tsv
INFO - Predictions File saved at conll_ner_pos_bert_base/conllpos_test_predictions_0.tsv
INFO - 
####################### EPOCH 1 ###################

INFO - Steps: 900 Task: conllpos Avg.Loss: 0.44733939387581567 Task Loss: 0.49750664830207825
INFO - Steps: 950 Task: conllpos Avg.Loss: 0.41471588984131813 Task Loss: 0.38029778003692627
INFO - Steps: 1000 Task: conllpos Avg.Loss: 0.4092011132323351 Task Loss: 0.2021685689687729
INFO - Steps: 1050 Task: conllner Avg.Loss: 0.40135617255298206 Task Loss: 0.3723362982273102
...
...
...
####################### EPOCH 9 ###################

INFO - Steps: 7950 Task: conllpos Avg.Loss: 0.1001631532611403 Task Loss: 0.020217880606651306
INFO - Steps: 8000 Task: conllpos Avg.Loss: 0.10772343432739834 Task Loss: 0.11353296786546707
INFO - Steps: 8050 Task: conllpos Avg.Loss: 0.11518600960954319 Task Loss: 0.11228577047586441
INFO - Steps: 8100 Task: conllner Avg.Loss: 0.11198339141162131 Task Loss: 0.06642302125692368
INFO - Steps: 8150 Task: conllner Avg.Loss: 0.10981700977783711 Task Loss: 0.0036876231897622347
INFO - Steps: 8200 Task: conllpos Avg.Loss: 0.11327582830172532 Task Loss: 0.11429984122514725
INFO - Steps: 8250 Task: conllpos Avg.Loss: 0.11441446969957338 Task Loss: 0.13093674182891846
INFO - Steps: 8300 Task: conllner Avg.Loss: 0.11446549561653922 Task Loss: 0.013396905735135078
INFO - Steps: 8350 Task: conllpos Avg.Loss: 0.1119606345133174 Task Loss: 0.16009871661663055
INFO - Steps: 8400 Task: conllner Avg.Loss: 0.11236278899013996 Task Loss: 0.0950835570693016
INFO - Steps: 8450 Task: conllner Avg.Loss: 0.11120766142118096 Task Loss: 0.11159289628267288
INFO - Steps: 8500 Task: conllpos Avg.Loss: 0.11085842446701283 Task Loss: 0.22129161655902863
INFO - Steps: 8550 Task: conllner Avg.Loss: 0.11140207761545079 Task Loss: 0.02758742682635784
INFO - Steps: 8600 Task: conllpos Avg.Loss: 0.11169017186017445 Task Loss: 0.2316276878118515
INFO - Steps: 8650 Task: conllpos Avg.Loss: 0.11209937039187506 Task Loss: 0.14967353641986847
INFO - Steps: 8700 Task: conllpos Avg.Loss: 0.11280078351682048 Task Loss: 0.043104056268930435
INFO - Steps: 8750 Task: conllner Avg.Loss: 0.11164643085465047 Task Loss: 0.055544812232255936
INFO - model saved in 8780 global step at conll_ner_pos_bert_base/multi_task_model_9_8780.pt
INFO - 
Running Evaluation on dev...
INFO - ********** conllner Evaluation************

INFO - seqeval_f1_score : 0.6554475784151063
INFO - seqeval_precision : 0.6066101199181048
INFO - seqeval_recall : 0.7128372572606977
INFO - ********** conllpos Evaluation************

INFO - seqeval_f1_score : 0.7957732799813527
INFO - seqeval_precision : 0.7855800575263663
INFO - seqeval_recall : 0.806234502302515
INFO - 
Running Evaluation on test...
INFO - ********** conllner Evaluation************

INFO - seqeval_f1_score : 0.5969553281756925
INFO - seqeval_precision : 0.5524249422632794
INFO - seqeval_recall : 0.6492942453854506
INFO - ********** conllpos Evaluation************

INFO - seqeval_f1_score : 0.7832221768522298
INFO - seqeval_precision : 0.7736398673478534
INFO - seqeval_recall : 0.7930448364571848
INFO - Predictions File saved at conll_ner_pos_bert_base/conllner_test_predictions_9.tsv
INFO - Predictions File saved at conll_ner_pos_bert_base/conllpos_test_predictions_9.tsv
```

## Check TensorBoard

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/05_10-14_05$ tensorboard --logdir ./tb_logs/
TensorBoard 1.15.0 at http://administrator-HP-Z2-Tower-G4-Workstation:6006/ (Press CTRL+C to quit)
```

## Check Models

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/conll_ner_pos_bert_base$ ls
conllner_test_predictions_0.tsv  conllner_test_predictions_6.tsv  conllpos_test_predictions_2.tsv  conllpos_test_predictions_8.tsv  multi_task_model_4_4390.pt
conllner_test_predictions_1.tsv  conllner_test_predictions_7.tsv  conllpos_test_predictions_3.tsv  conllpos_test_predictions_9.tsv  multi_task_model_5_5268.pt
conllner_test_predictions_2.tsv  conllner_test_predictions_8.tsv  conllpos_test_predictions_4.tsv  multi_task_model_0_878.pt        multi_task_model_6_6146.pt
conllner_test_predictions_3.tsv  conllner_test_predictions_9.tsv  conllpos_test_predictions_5.tsv  multi_task_model_1_1756.pt       multi_task_model_7_7024.pt
conllner_test_predictions_4.tsv  conllpos_test_predictions_0.tsv  conllpos_test_predictions_6.tsv  multi_task_model_2_2634.pt       multi_task_model_8_7902.pt
conllner_test_predictions_5.tsv  conllpos_test_predictions_1.tsv  conllpos_test_predictions_7.tsv  multi_task_model_3_3512.pt       multi_task_model_9_8780.pt
(multiTask) ye@:~/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/conll_ner_pos_bert_base$
```

## Test Inference

test program ကို အောက်ပါအတိုင်း ရေးခဲ့...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ cat infer.py
import sys
from infer_pipeline import inferPipeline

sys.path.insert(1, '../../')

pipe = inferPipeline(modelPath = '/home/ye/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/conll_ner_pos_bert_base/multi_task_model_9_8780.pt', maxSeqLen = 50)

#samples = [ ['sample_sentence_1'], ['sample_sentence_2'] ]
#tasks = ['TaskA', 'TaskB']
#pipe.infer(samples, tasks)

result=pipe.infer([['West', 'Indian', 'all-rounder', 'Phil', 'Simmons', 'took', 'four', 'for', '38', 'on', 'Friday', 'as', 'Leicestershire', 'beat', 'Somerset', 'by', 'an', 'innings', 'and', '39', 'runs', 'in', 'two', 'days', 'to', 'take', 'over', 'at', 'the', 'head', 'of', 'the', 'county', 'championship', '.'], ['my', 'name', 'is', 'ye', '.']], ['conllner', 'conllpos'])

print(result)
```

run ကြည့်တော့ အလုပ်လုပ်ပေးတယ်...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ time python ./infer.py
Using TensorFlow backend.
Eval:   0%|                                                                                                                       | 0/1 [00:00<?, ?it/s]/home/ye/anaconda3/envs/multiTask/lib/python3.7/site-packages/torch/nn/functional.py:1350: UserWarning: nn.functional.sigmoid is deprecated. Use torch.sigmoid instead.
  warnings.warn("nn.functional.sigmoid is deprecated. Use torch.sigmoid instead.")
Eval: 2it [00:01,  1.04it/s]                                                                                                                            
[{'Query': ['West', 'Indian', 'all-rounder', 'Phil', 'Simmons', 'took', 'four', 'for', '38', 'on', 'Friday', 'as', 'Leicestershire', 'beat', 'Somerset', 'by', 'an', 'innings', 'and', '39', 'runs', 'in', 'two', 'days', 'to', 'take', 'over', 'at', 'the', 'head', 'of', 'the', 'county', 'championship', '.'], 'conllner': [('LOC', 'West')], 'conllpos': [('NP', 'West')]}, {'Query': ['my', 'name', 'is', 'ye', '.'], 'conllner': [], 'conllpos': [('NP', 'my')]}]

real	0m10.479s
user	0m6.530s
sys	0m1.860s
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$
```

test ဖိုင် နဲ့ run မယ်ဆိုရင် ဖိုင်ကို ဖွင့်ဖတ်ပြီး load လုပ်ပြီး infer လုပ်တဲ့ ပုံစံရေးဖို့ ပြည့်ရလိမ့်မယ်။  
example အနေနဲ့ run ပြထားတဲ့ ပရိုဂရမ်ကိုတော့ ရှာမတွေ့လို့...  

## Prepare a testing.py

```
[{'Query': 'my', 'conllpos': [('NP', 'm')]}, {'Query': 'name', 'conllpos': [('VP', 'n')]}, {'Query': 'is', 'conllpos': [('NP', 'i')]}, {'Query': 'ye', 'conllpos': [('NP', 'y')]}, {'Query': '.', 'conllpos': []}]
```

```
[{'Query': "['CRICKET', '-', 'LEICESTERSHIRE', 'TAKE', 'OVER', 'AT', 'TOP', 'AFTER', 'INNINGS', 'VICTORY', '.']", 'conllner': []}, {'Query': "['LONDON', '1996-08-30']", 'conllner': []}, {'Query': "['West', 'Indian', 'all-rounder', 'Phil', 'Simmons', 'took', 'four', 'for', '38', 'on', 'Friday', 'as', 'Leicestershire', 'beat', 'Somerset', 'by', 'an', 'innings', 'and', '39', 'runs', 'in', 'two', 'days', 'to', 'take', 'over', 'at', 'the', 'head', 'of', 'the', 'county', 'championship', '.']", 'conllner': []}, ...
...
```


## Check  Inference File

run_inference.py ဆိုတဲ့ program  ကိုတော့ တွေ့လို့ အောက်ပါအတိုင်း စမ်းကြည့်ခဲ့...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ python ./run_inference.py 
Using TensorFlow backend.
usage: run_inference.py [-h] --pred_file_path PRED_FILE_PATH --out_dir OUT_DIR
                        [--has_labels HAS_LABELS] --task_name TASK_NAME
                        --saved_model_path SAVED_MODEL_PATH
                        [--eval_batch_size EVAL_BATCH_SIZE]
                        [--max_seq_len MAX_SEQ_LEN] [--seed SEED]
run_inference.py: error: the following arguments are required: --pred_file_path, --out_dir, --task_name, --saved_model_path
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ 
```

## Testing for TaskA (NER)

```
python ./run_inference.py --saved_model_path /home/ye/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/conll_ner_pos_bert_base/multi_task_model_9_8780.pt --task_name "conllner" --out_dir ./test-result --pred_file_path /home/ye/exp/multi-task/multi-task-NLP/data/ner_coNLL_testa.tsv
```
output folder က မရှိရင် auto ဆောက်ပေးတယ်...  

```
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$ time python ./run_inference.py --saved_model_path /home/ye/exp/multi-task/multi-task-NLP/examples/ner_pos_tagging/conll_ner_pos_bert_base/multi_task_model_9_8780.pt --task_name "conllner" --out_dir ./test-result --pred_file_path /home/ye/exp/multi-task/multi-task-NLP/data/ner_coNLL_testa.tsv
Using TensorFlow backend.
Processing Started...
Data Size:  3250
number of threads:  7
  0%|                                                                                                                           | 0/464 [00:00<?, ?it/s]
Process Process-2:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-3:                                                                                                               | 0/464 [00:00<?, ?it/s]
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-4:
Traceback (most recent call last):                                                                                              | 0/464 [00:00<?, ?it/s]
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-5:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap                    | 0/464 [00:00<?, ?it/s]
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-6:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()                                                                                                                  | 0/464 [00:00<?, ?it/s]
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-7:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run                            | 0/464 [00:00<?, ?it/s]
    self._target(*self._args, **self._kwargs)
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
                                                                                                                                                       Process Process-8:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 297, in _bootstrap
    self.run()
  File "/home/ye/anaconda3/envs/multiTask/lib/python3.7/multiprocessing/process.py", line 99, in run
    self._target(*self._args, **self._kwargs)                                                                                   | 0/464 [00:00<?, ?it/s]
  File "/home/ye/exp/multi-task/multi-task-NLP/data_preparation.py", line 203, in create_data_ner
    assert len(tempLabelsEnc) == len(tokenIds), "mismatch between processed tokens and labels"
AssertionError: mismatch between processed tokens and labels
Data Processing done for conllner. File saved at ./test-result/bert-base-uncased_prediction_data/ner_coNLL_testa.json
Eval: 0it [00:00, ?it/s]

real	0m12.222s
user	0m5.472s
sys	0m2.543s
(multiTask) ye@:~/exp/multi-task/multi-task-NLP$
```



## Reference

https://github.com/pbloem/former/issues/1

