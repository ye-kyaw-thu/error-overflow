# XNMT Installation and Test Running

XNMT က default setting က DyNet နဲ့ ချိတ်ပြီးသုံးတာကြောင့် အနည်းဆုံး DyNet python library ကို installation လုပ် ရပါတယ်။  
အဲဒီနေရာမှာ အခန့်မသင့်ရင် installation မှာတင် တစ်နေတတ်ပါတယ်။  
အထူးသဖြင့်တော့ Eigen ကို installation လုပ်တဲ့အခါ version မတူလို့ ERROR ပေးတာမျိုး၊ pip နဲ့ install လုပ်တာဆိုရင် DyNet အတွက် wheel ဆောက်တဲ့ နေရာမှာ ပြဿနာပေးတာမျိုး၊ GPU library ဖြစ်တဲ့ CUDA ကိစ္စတို့က နည်းနည်း ခက်ပါတယ်။  

ဒီ log ကတော့ Backend ကို DyNet မသုံးပဲနဲ့ PyTorch ကိုသုံးပြီး GPU ကို အခြေခံတဲ့ training/testing ကို စမ်းပြထားတာပါ။  

y@LST Lab,  
1 May 2022

## clone xnmt

```
(base) ye@ye-System-Product-Name:~/tool$ git clone https://github.com/neulab/xnmt
Cloning into 'xnmt'...
remote: Enumerating objects: 10946, done.
remote: Counting objects: 100% (165/165), done.
remote: Compressing objects: 100% (137/137), done.
remote: Total 10946 (delta 26), reused 110 (delta 25), pack-reused 10781
Receiving objects: 100% (10946/10946), 17.66 MiB | 14.87 MiB/s, done.
Resolving deltas: 100% (8339/8339), done.
(base) ye@ye-System-Product-Name:~/tool$ 
```

## create new env

```
(base) ye@ye-System-Product-Name:~/tool/xnmt$ conda create -n "xnmt" python
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/xnmt

  added / updated specs:
    - python


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libstdcxx-ng-9.3.0         |      hd4cf53a_17         3.1 MB
    libuuid-1.0.3              |       h7f8727e_2          17 KB
    pip-21.2.4                 |  py310h06a4308_0         1.8 MB
    python-3.10.4              |       h12debd9_0        24.2 MB
    setuptools-61.2.0          |  py310h06a4308_0        1019 KB
    tzdata-2022a               |       hda174b7_0         109 KB
    ------------------------------------------------------------
                                           Total:        30.2 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h7b6447c_0
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.3.29-h06a4308_1
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  libuuid            pkgs/main/linux-64::libuuid-1.0.3-h7f8727e_2
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1n-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.4-py310h06a4308_0
  python             pkgs/main/linux-64::python-3.10.4-h12debd9_0
  readline           pkgs/main/linux-64::readline-8.1.2-h7f8727e_1
  setuptools         pkgs/main/linux-64::setuptools-61.2.0-py310h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.38.2-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  tzdata             pkgs/main/noarch::tzdata-2022a-hda174b7_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.12-h7f8727e_2


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.10.4        | 24.2 MB   | ################################################################################### | 100% 
libstdcxx-ng-9.3.0   | 3.1 MB    | ################################################################################### | 100% 
libuuid-1.0.3        | 17 KB     | ################################################################################### | 100% 
pip-21.2.4           | 1.8 MB    | ################################################################################### | 100% 
tzdata-2022a         | 109 KB    | ################################################################################### | 100% 
setuptools-61.2.0    | 1019 KB   | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate xnmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(base) ye@ye-System-Product-Name:~/tool/xnmt$ conda activate xnmt
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

## installation of requirements

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ cat requirements.txt 
PyYAML
scipy>=0.19.0    
lxml    
dynet    
matplotlib    
cython   
h5py
asteval
numpy
Unidecode>=1.0.22
beautifulsoup4
nltk
pylru
tensorboardX==1.6
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ 
```

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ pip install -r requirements.txt
Collecting PyYAML
  Downloading PyYAML-6.0-cp310-cp310-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (682 kB)
     |████████████████████████████████| 682 kB 1.7 MB/s 
Collecting scipy>=0.19.0
  Downloading scipy-1.8.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (42.3 MB)
     |████████████████████████████████| 42.3 MB 133 kB/s 
Collecting lxml
  Downloading lxml-4.8.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (7.0 MB)
     |████████████████████████████████| 7.0 MB 33.3 MB/s 
Collecting dynet
  Downloading dyNET-2.1.2.tar.gz (509 kB)
     |████████████████████████████████| 509 kB 100.4 MB/s 
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
    Preparing wheel metadata ... done
Collecting matplotlib
  Downloading matplotlib-3.5.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.9 MB)
     |████████████████████████████████| 11.9 MB 94.7 MB/s 
Collecting cython
  Using cached Cython-0.29.28-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
Collecting h5py
  Downloading h5py-3.6.0-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
     |████████████████████████████████| 4.5 MB 21.3 MB/s 
Collecting asteval
  Using cached asteval-0.9.26.tar.gz (40 kB)
Collecting numpy
  Downloading numpy-1.22.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.8 MB)
     |████████████████████████████████| 16.8 MB 87.8 MB/s 
Collecting Unidecode>=1.0.22
  Using cached Unidecode-1.3.4-py3-none-any.whl (235 kB)
Requirement already satisfied: beautifulsoup4 in /home/ye/.local/lib/python3.10/site-packages (from -r requirements.txt (line 11)) (4.11.1)
Collecting nltk
  Downloading nltk-3.7-py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 97.4 MB/s 
Collecting pylru
  Using cached pylru-1.2.1-py3-none-any.whl (16 kB)
Collecting tensorboardX==1.6
  Using cached tensorboardX-1.6-py2.py3-none-any.whl (129 kB)
Collecting protobuf>=3.2.0
  Downloading protobuf-3.20.1-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 111.0 MB/s 
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting fonttools>=4.22.0
  Downloading fonttools-4.33.3-py3-none-any.whl (930 kB)
     |████████████████████████████████| 930 kB 94.6 MB/s 
Requirement already satisfied: packaging>=20.0 in /home/ye/.local/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 5)) (21.3)
Collecting pyparsing>=2.2.1
  Using cached pyparsing-3.0.8-py3-none-any.whl (98 kB)
Collecting pillow>=6.2.0
  Downloading Pillow-9.1.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.3 MB)
     |████████████████████████████████| 4.3 MB 29.9 MB/s 
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/.local/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 5)) (2.8.2)
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.2-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.6 MB)
     |████████████████████████████████| 1.6 MB 106.1 MB/s 
Requirement already satisfied: soupsieve>1.2 in /home/ye/.local/lib/python3.10/site-packages (from beautifulsoup4->-r requirements.txt (line 11)) (2.3.2.post1)
Collecting tqdm
  Using cached tqdm-4.64.0-py2.py3-none-any.whl (78 kB)
Collecting regex>=2021.8.3
  Downloading regex-2022.4.24-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (763 kB)
     |████████████████████████████████| 763 kB 104.0 MB/s 
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting click
  Downloading click-8.1.3-py3-none-any.whl (96 kB)
     |████████████████████████████████| 96 kB 1.0 MB/s 
Building wheels for collected packages: dynet, asteval
  Building wheel for dynet (PEP 517) ... error
  ERROR: Command errored out with exit status 1:
   command: /home/ye/anaconda3/envs/xnmt/bin/python /home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/pip/_vendor/pep517/in_process/_in_process.py build_wheel /tmp/tmpw3_u_94n
       cwd: /tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539
  Complete output (31 lines):
  /tmp/pip-build-env-pi88zdg7/overlay/lib/python3.10/site-packages/setuptools/dist.py:516: UserWarning: Normalizing 'v2.1.2' to '2.1.2'
    warnings.warn(tmpl.format(**locals()))
  /tmp/pip-build-env-pi88zdg7/overlay/lib/python3.10/site-packages/setuptools/dist.py:757: UserWarning: Usage of dash-separated 'description-file' will not be supported in future versions. Please use the underscore name 'description_file' instead
    warnings.warn(
  running bdist_wheel
  running build
  INFO:root:CMAKE_PATH='/usr/bin/cmake'
  INFO:root:MAKE_PATH='/usr/bin/make'
  INFO:root:MAKE_FLAGS='-j 12'
  INFO:root:EIGEN3_INCLUDE_DIR='/tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539/build/py3.10-64bit/eigen'
  INFO:root:EIGEN3_DOWNLOAD_URL='https://github.com/clab/dynet/releases/download/2.1/eigen-b2e267dc99d4.zip'
  INFO:root:CC_PATH='/usr/bin/gcc'
  INFO:root:CXX_PATH='/usr/bin/g++'
  INFO:root:SCRIPT_DIR='/tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539'
  INFO:root:BUILD_DIR='/tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539/build/py3.10-64bit'
  INFO:root:INSTALL_PREFIX='/home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/../../..'
  INFO:root:PYTHON='/home/ye/anaconda3/envs/xnmt/bin/python'
  /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /usr/bin/cmake)
  /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
  g++ (Ubuntu 11.2.0-19ubuntu1) 11.2.0
  Copyright (C) 2021 Free Software Foundation, Inc.
  This is free software; see the source for copying conditions.  There is NO
  warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
  
  INFO:root:Creating build directory /tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539/build/py3.10-64bit
  INFO:root:Fetching Eigen...
  INFO:root:Unpacking Eigen...
  INFO:root:Configuring...
  /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /usr/bin/cmake)
  /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
  error: /usr/bin/cmake /tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539 -DCMAKE_INSTALL_PREFIX='/home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/../../..' -DEIGEN3_INCLUDE_DIR='/tmp/pip-install-exprtx0c/dynet_3ea4b332d3a24a66aa3af88593c68539/build/py3.10-64bit/eigen' -DPYTHON='/home/ye/anaconda3/envs/xnmt/bin/python' -DCUDNN_ROOT='/usr/local/cuda-11.6/'
  ----------------------------------------
  ERROR: Failed building wheel for dynet
  Building wheel for asteval (setup.py) ... done
  Created wheel for asteval: filename=asteval-0.9.26-py3-none-any.whl size=17648 sha256=e527c432be5d271de67d8927790b07e8cca479c3be1ee3ed2635244647426bd0
  Stored in directory: /home/ye/.cache/pip/wheels/1e/df/9a/6d529691f3fd6838c6ad007a8519716b8fd12cb18818fd5531
Successfully built asteval
Failed to build dynet
ERROR: Could not build wheels for dynet which use PEP 517 and cannot be installed directly
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

နောက်ဆုံးပိုင်းမှာ ERROR ပေးတယ်။  

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ pip install --upgrade pip setuptools wheel
Requirement already satisfied: pip in /home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages (21.2.4)
Collecting pip
  Downloading pip-22.0.4-py3-none-any.whl (2.1 MB)
     |████████████████████████████████| 2.1 MB 1.7 MB/s 
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages (61.2.0)
Collecting setuptools
  Using cached setuptools-62.1.0-py3-none-any.whl (1.1 MB)
Requirement already satisfied: wheel in /home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages (0.37.1)
Installing collected packages: setuptools, pip
  Attempting uninstall: setuptools
    Found existing installation: setuptools 61.2.0
    Uninstalling setuptools-61.2.0:
      Successfully uninstalled setuptools-61.2.0
  Attempting uninstall: pip
    Found existing installation: pip 21.2.4
    Uninstalling pip-21.2.4:
      Successfully uninstalled pip-21.2.4
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
ipython 8.3.0 requires pexpect>4.3; sys_platform != "win32", which is not installed.
Successfully installed pip-22.0.4 setuptools-62.1.0
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

ထပ် try ကြည့်တော့...  

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ pip install -r requirements.txt
Collecting PyYAML
  Using cached PyYAML-6.0-cp310-cp310-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (682 kB)
Collecting scipy>=0.19.0
  Using cached scipy-1.8.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (42.3 MB)
Collecting lxml
  Using cached lxml-4.8.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (7.0 MB)
Collecting dynet
  Using cached dyNET-2.1.2.tar.gz (509 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting matplotlib
  Using cached matplotlib-3.5.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.9 MB)
Collecting cython
  Using cached Cython-0.29.28-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
Collecting h5py
  Using cached h5py-3.6.0-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
Collecting asteval
  Using cached asteval-0.9.26-py3-none-any.whl
Collecting numpy
  Using cached numpy-1.22.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.8 MB)
Collecting Unidecode>=1.0.22
  Using cached Unidecode-1.3.4-py3-none-any.whl (235 kB)
Requirement already satisfied: beautifulsoup4 in /home/ye/.local/lib/python3.10/site-packages (from -r requirements.txt (line 11)) (4.11.1)
Collecting nltk
  Using cached nltk-3.7-py3-none-any.whl (1.5 MB)
Collecting pylru
  Using cached pylru-1.2.1-py3-none-any.whl (16 kB)
Collecting tensorboardX==1.6
  Using cached tensorboardX-1.6-py2.py3-none-any.whl (129 kB)
Collecting protobuf>=3.2.0
  Using cached protobuf-3.20.1-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.1 MB)
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting pyparsing>=2.2.1
  Using cached pyparsing-3.0.8-py3-none-any.whl (98 kB)
Collecting fonttools>=4.22.0
  Using cached fonttools-4.33.3-py3-none-any.whl (930 kB)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/.local/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 5)) (2.8.2)
Collecting pillow>=6.2.0
  Using cached Pillow-9.1.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.3 MB)
Requirement already satisfied: packaging>=20.0 in /home/ye/.local/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 5)) (21.3)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.4.2-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.6 MB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Requirement already satisfied: soupsieve>1.2 in /home/ye/.local/lib/python3.10/site-packages (from beautifulsoup4->-r requirements.txt (line 11)) (2.3.2.post1)
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting click
  Using cached click-8.1.3-py3-none-any.whl (96 kB)
Collecting tqdm
  Using cached tqdm-4.64.0-py2.py3-none-any.whl (78 kB)
Collecting regex>=2021.8.3
  Using cached regex-2022.4.24-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (763 kB)
Building wheels for collected packages: dynet
  Building wheel for dynet (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Building wheel for dynet (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [31 lines of output]
      /tmp/pip-build-env-ftuwmhm5/overlay/lib/python3.10/site-packages/setuptools/dist.py:516: UserWarning: Normalizing 'v2.1.2' to '2.1.2'
        warnings.warn(tmpl.format(**locals()))
      /tmp/pip-build-env-ftuwmhm5/overlay/lib/python3.10/site-packages/setuptools/dist.py:757: UserWarning: Usage of dash-separated 'description-file' will not be supported in future versions. Please use the underscore name 'description_file' instead
        warnings.warn(
      running bdist_wheel
      running build
      INFO:root:CMAKE_PATH='/usr/bin/cmake'
      INFO:root:MAKE_PATH='/usr/bin/make'
      INFO:root:MAKE_FLAGS='-j 12'
      INFO:root:EIGEN3_INCLUDE_DIR='/tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9/build/py3.10-64bit/eigen'
      INFO:root:EIGEN3_DOWNLOAD_URL='https://github.com/clab/dynet/releases/download/2.1/eigen-b2e267dc99d4.zip'
      INFO:root:CC_PATH='/usr/bin/gcc'
      INFO:root:CXX_PATH='/usr/bin/g++'
      INFO:root:SCRIPT_DIR='/tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9'
      INFO:root:BUILD_DIR='/tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9/build/py3.10-64bit'
      INFO:root:INSTALL_PREFIX='/home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/../../..'
      INFO:root:PYTHON='/home/ye/anaconda3/envs/xnmt/bin/python'
      /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /usr/bin/cmake)
      /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
      g++ (Ubuntu 11.2.0-19ubuntu1) 11.2.0
      Copyright (C) 2021 Free Software Foundation, Inc.
      This is free software; see the source for copying conditions.  There is NO
      warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
      
      INFO:root:Creating build directory /tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9/build/py3.10-64bit
      INFO:root:Fetching Eigen...
      INFO:root:Unpacking Eigen...
      INFO:root:Configuring...
      /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /usr/bin/cmake)
      /usr/bin/cmake: /home/ye/anaconda3/envs/xnmt/lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
      error: /usr/bin/cmake /tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9 -DCMAKE_INSTALL_PREFIX='/home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/../../..' -DEIGEN3_INCLUDE_DIR='/tmp/pip-install-h0y75ts8/dynet_fbec59feb3f343f98ef1a5981accceb9/build/py3.10-64bit/eigen' -DPYTHON='/home/ye/anaconda3/envs/xnmt/bin/python' -DCUDNN_ROOT='/usr/local/cuda-11.6/'
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for dynet
Failed to build dynet
ERROR: Could not build wheels for dynet, which is required to install pyproject.toml-based projects
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ sudo apt-get install gcc-4.9
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'gcc-4.9-arm-linux-gnueabi' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-s390x-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-sh4-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-hppa64' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-sparc64-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-aarch64-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-mips64-linux-gnuabi64' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-m68k-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-powerpc64-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-powerpc-linux-gnuspe' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-arm-linux-gnueabihf' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-mips-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-powerpc64le-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-hppa-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-powerpc-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-mipsel-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-sparc-linux-gnu' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-mips64el-linux-gnuabi64' for regex 'gcc-4.9'
Note, selecting 'gcc-4.9-alpha-linux-gnu' for regex 'gcc-4.9'
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.
```

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ sudo apt-get upgrade libstdc++6
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
libstdc++6 is already the newest version (12-20220319-1ubuntu1).
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic-hwe-22.04 linux-headers-generic-hwe-22.04 linux-image-generic-hwe-22.04
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.
```

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following NEW packages will be installed:
  linux-headers-5.15.0-27 linux-headers-5.15.0-27-generic linux-image-5.15.0-27-generic linux-modules-5.15.0-27-generic
  linux-modules-extra-5.15.0-27-generic
The following packages will be upgraded:
  linux-generic-hwe-22.04 linux-headers-generic-hwe-22.04 linux-image-generic-hwe-22.04
3 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.
3 standard security updates
Need to get 110 MB of archives.
After this operation, 558 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-modules-5.15.0-27-generic amd64 5.15.0-27.28 [22.0 MB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-5.15.0-27-generic amd64 5.15.0-27.28 [10.9 MB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-modules-extra-5.15.0-27-generic amd64 5.15.0-27.28 [61.8 MB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-generic-hwe-22.04 amd64 5.15.0.27.30 [1,670 B]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-generic-hwe-22.04 amd64 5.15.0.27.30 [2,506 B]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-5.15.0-27 all 5.15.0-27.28 [12.3 MB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-5.15.0-27-generic amd64 5.15.0-27.28 [2,793 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-generic-hwe-22.04 amd64 5.15.0.27.30 [2,388 B]
Fetched 110 MB in 2s (61.8 MB/s)
Selecting previously unselected package linux-modules-5.15.0-27-generic.
(Reading database ... 192024 files and directories currently installed.)
Preparing to unpack .../0-linux-modules-5.15.0-27-generic_5.15.0-27.28_amd64.deb ...
Unpacking linux-modules-5.15.0-27-generic (5.15.0-27.28) ...
Selecting previously unselected package linux-image-5.15.0-27-generic.
Preparing to unpack .../1-linux-image-5.15.0-27-generic_5.15.0-27.28_amd64.deb ...
Unpacking linux-image-5.15.0-27-generic (5.15.0-27.28) ...
Selecting previously unselected package linux-modules-extra-5.15.0-27-generic.
Preparing to unpack .../2-linux-modules-extra-5.15.0-27-generic_5.15.0-27.28_amd64.deb ...
Unpacking linux-modules-extra-5.15.0-27-generic (5.15.0-27.28) ...
Preparing to unpack .../3-linux-generic-hwe-22.04_5.15.0.27.30_amd64.deb ...
Unpacking linux-generic-hwe-22.04 (5.15.0.27.30) over (5.15.0.25.27) ...
Preparing to unpack .../4-linux-image-generic-hwe-22.04_5.15.0.27.30_amd64.deb ...
Unpacking linux-image-generic-hwe-22.04 (5.15.0.27.30) over (5.15.0.25.27) ...
Selecting previously unselected package linux-headers-5.15.0-27.
Preparing to unpack .../5-linux-headers-5.15.0-27_5.15.0-27.28_all.deb ...
Unpacking linux-headers-5.15.0-27 (5.15.0-27.28) ...
Selecting previously unselected package linux-headers-5.15.0-27-generic.
Preparing to unpack .../6-linux-headers-5.15.0-27-generic_5.15.0-27.28_amd64.deb ...
Unpacking linux-headers-5.15.0-27-generic (5.15.0-27.28) ...
Preparing to unpack .../7-linux-headers-generic-hwe-22.04_5.15.0.27.30_amd64.deb ...
Unpacking linux-headers-generic-hwe-22.04 (5.15.0.27.30) over (5.15.0.25.27) ...
Setting up linux-headers-5.15.0-27 (5.15.0-27.28) ...
Setting up linux-headers-5.15.0-27-generic (5.15.0-27.28) ...
Setting up linux-headers-generic-hwe-22.04 (5.15.0.27.30) ...
Setting up linux-image-5.15.0-27-generic (5.15.0-27.28) ...
I: /boot/vmlinuz.old is now a symlink to vmlinuz-5.15.0-25-generic
I: /boot/vmlinuz is now a symlink to vmlinuz-5.15.0-27-generic
I: /boot/initrd.img is now a symlink to initrd.img-5.15.0-27-generic
Setting up linux-modules-extra-5.15.0-27-generic (5.15.0-27.28) ...
Setting up linux-image-generic-hwe-22.04 (5.15.0.27.30) ...
Setting up linux-generic-hwe-22.04 (5.15.0.27.30) ...
Setting up linux-modules-5.15.0-27-generic (5.15.0-27.28) ...
Processing triggers for linux-image-5.15.0-27-generic (5.15.0-27.28) ...
/etc/kernel/postinst.d/initramfs-tools:
update-initramfs: Generating /boot/initrd.img-5.15.0-27-generic
/etc/kernel/postinst.d/zz-update-grub:
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.15.0-27-generic
Found initrd image: /boot/initrd.img-5.15.0-27-generic
Found linux image: /boot/vmlinuz-5.15.0-25-generic
Found initrd image: /boot/initrd.img-5.15.0-25-generic
Memtest86+ needs a 16-bit boot, that is not available on EFI, exiting
Warning: os-prober will not be executed to detect other bootable partitions.
Systems on them will not be added to the GRUB boot configuration.
Check GRUB_DISABLE_OS_PROBER documentation entry.
Adding boot menu entry for UEFI Firmware Settings ...
done
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_3.4.20
GLIBCXX_3.4.21
GLIBCXX_3.4.22
GLIBCXX_3.4.23
GLIBCXX_3.4.24
GLIBCXX_3.4.25
GLIBCXX_3.4.26
GLIBCXX_3.4.27
GLIBCXX_3.4.28
GLIBCXX_3.4.29
GLIBCXX_3.4.30
GLIBCXX_DEBUG_MESSAGE_LENGTH
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$
```

နောက်တစ်ခေါက် ထပ်ပြီး requirement ကို install လုပ်ကြည့်တော့ DyNet အတွက် အပိုင်းမှာ စောစောကလိုပဲ ERROR ပေးနေသေးတယ်။  

```
6_64-linux-gnu/libjsoncpp.so.25)
      error: /usr/bin/cmake /tmp/pip-install-2au4zfk9/dynet_84fb189d489e4e72898ca4f468f41afa -DCMAKE_INSTALL_PREFIX='/home/ye/anaconda3/envs/xnmt/lib/python3.10/site-packages/../../..' -DEIGEN3_INCLUDE_DIR='/tmp/pip-install-2au4zfk9/dynet_84fb189d489e4e72898ca4f468f41afa/build/py3.10-64bit/eigen' -DPYTHON='/home/ye/anaconda3/envs/xnmt/bin/python' -DCUDNN_ROOT='/usr/local/cuda-11.6/'
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for dynet
Failed to build dynet
ERROR: Could not build wheels for dynet, which is required to install pyproject.toml-based projects
(xnmt) ye@ye-System-Product-Name:~/tool/xnmt$ 
```

Python version ကို 3.6 အထိ ပြန်ချပြီး environment အသစ်တစ်ခု ပြန်ဆောက်ပြီး ထပ်စမ်းကြည့်မယ်  


```
(base) ye@ye-System-Product-Name:~/tool/xnmt$ conda create -n "xnmt-py3.6" python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/xnmt-py3.6

  added / updated specs:
    - python=3.6


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.3.29-h06a4308_1
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1n-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.13-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.1.2-h7f8727e_1
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.38.2-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.12-h7f8727e_2


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate xnmt-py3.6
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(base) ye@ye-System-Product-Name:~/tool/xnmt$ conda activate xnmt-py3.6
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ pip install -r requirements.txt
Collecting PyYAML
  Using cached PyYAML-6.0-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (603 kB)
Collecting scipy>=0.19.0
  Using cached scipy-1.5.4-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
Collecting lxml
  Using cached lxml-4.8.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (6.4 MB)
Collecting dynet
  Using cached dyNET-2.1.2-cp36-cp36m-manylinux1_x86_64.whl (4.4 MB)
Collecting matplotlib
  Using cached matplotlib-3.3.4-cp36-cp36m-manylinux1_x86_64.whl (11.5 MB)
Collecting cython
  Using cached Cython-0.29.28-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
Collecting h5py
  Using cached h5py-3.1.0-cp36-cp36m-manylinux1_x86_64.whl (4.0 MB)
Collecting asteval
  Using cached asteval-0.9.26-py3-none-any.whl
Collecting numpy
  Using cached numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
Collecting Unidecode>=1.0.22
  Using cached Unidecode-1.3.4-py3-none-any.whl (235 kB)
Collecting beautifulsoup4
  Using cached beautifulsoup4-4.11.1-py3-none-any.whl (128 kB)
Collecting nltk
  Using cached nltk-3.6.7-py3-none-any.whl (1.5 MB)
Collecting pylru
  Using cached pylru-1.2.1-py3-none-any.whl (16 kB)
Collecting tensorboardX==1.6
  Using cached tensorboardX-1.6-py2.py3-none-any.whl (129 kB)
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting protobuf>=3.2.0
  Using cached protobuf-3.19.4-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (1.1 MB)
Collecting pillow>=6.2.0
  Using cached Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3
  Using cached pyparsing-3.0.8-py3-none-any.whl (98 kB)
Collecting python-dateutil>=2.1
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting cached-property
  Using cached cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Collecting importlib-metadata
  Using cached importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Collecting soupsieve>1.2
  Using cached soupsieve-2.3.2.post1-py3-none-any.whl (37 kB)
Collecting tqdm
  Using cached tqdm-4.64.0-py2.py3-none-any.whl (78 kB)
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting click
  Using cached click-8.0.4-py3-none-any.whl (97 kB)
Collecting regex>=2021.8.3
  Using cached regex-2022.4.24-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (749 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting zipp>=0.5
  Using cached zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting importlib-resources
  Using cached importlib_resources-5.4.0-py3-none-any.whl (28 kB)
Installing collected packages: zipp, typing-extensions, six, importlib-resources, importlib-metadata, tqdm, soupsieve, regex, python-dateutil, pyparsing, protobuf, pillow, numpy, kiwisolver, joblib, cython, cycler, click, cached-property, Unidecode, tensorboardX, scipy, PyYAML, pylru, nltk, matplotlib, lxml, h5py, dynet, beautifulsoup4, asteval
Successfully installed PyYAML-6.0 Unidecode-1.3.4 asteval-0.9.26 beautifulsoup4-4.11.1 cached-property-1.5.2 click-8.0.4 cycler-0.11.0 cython-0.29.28 dynet-2.1.2 h5py-3.1.0 importlib-metadata-4.8.3 importlib-resources-5.4.0 joblib-1.1.0 kiwisolver-1.3.1 lxml-4.8.0 matplotlib-3.3.4 nltk-3.6.7 numpy-1.19.5 pillow-8.4.0 protobuf-3.19.4 pylru-1.2.1 pyparsing-3.0.8 python-dateutil-2.8.2 regex-2022.4.24 scipy-1.5.4 six-1.16.0 soupsieve-2.3.2.post1 tensorboardX-1.6 tqdm-4.64.0 typing-extensions-4.1.1 zipp-3.6.0
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

ဒီတစ်ခါတော့ requirement အားလုံးကို installation လုပ်ပေးတာ အဆင်ပြေသွားပြီလို့ ထင်တယ်...  

## Installation of requirements-extra

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ cd requirements-extra/
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ ls
audio-feature-extraction.txt  build-doc.txt  ensembling-scripts.txt  lattice.txt  README  sentencepiece.txt  tensorboard.txt
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat audio-feature-extraction.txt 
# needed for audio feature extraction via !MelFiltExtractor
librosa
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./audio-feature-extraction.txt 
Collecting librosa
  Using cached librosa-0.9.1-py3-none-any.whl (213 kB)
Collecting audioread>=2.1.5
  Using cached audioread-2.1.9-py3-none-any.whl
Requirement already satisfied: scipy>=1.2.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from librosa->-r ./audio-feature-extraction.txt (line 2)) (1.5.4)
Collecting pooch>=1.0
  Using cached pooch-1.6.0-py3-none-any.whl (56 kB)
Collecting packaging>=20.0
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting resampy>=0.2.2
  Using cached resampy-0.2.2-py3-none-any.whl
Collecting numba>=0.45.1
  Using cached numba-0.53.1-cp36-cp36m-manylinux2014_x86_64.whl (3.4 MB)
Requirement already satisfied: joblib>=0.14 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from librosa->-r ./audio-feature-extraction.txt (line 2)) (1.1.0)
Collecting scikit-learn>=0.19.1
  Using cached scikit_learn-0.24.2-cp36-cp36m-manylinux2010_x86_64.whl (22.2 MB)
Collecting soundfile>=0.10.2
  Using cached SoundFile-0.10.3.post1-py2.py3-none-any.whl (21 kB)
Collecting decorator>=4.0.10
  Using cached decorator-5.1.1-py3-none-any.whl (9.1 kB)
Requirement already satisfied: numpy>=1.17.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from librosa->-r ./audio-feature-extraction.txt (line 2)) (1.19.5)
Collecting llvmlite<0.37,>=0.36.0rc1
  Using cached llvmlite-0.36.0-cp36-cp36m-manylinux2010_x86_64.whl (25.3 MB)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from numba>=0.45.1->librosa->-r ./audio-feature-extraction.txt (line 2)) (58.0.4)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from packaging>=20.0->librosa->-r ./audio-feature-extraction.txt (line 2)) (3.0.8)
Collecting requests>=2.19.0
  Using cached requests-2.27.1-py2.py3-none-any.whl (63 kB)
Collecting appdirs>=1.3.0
  Using cached appdirs-1.4.4-py2.py3-none-any.whl (9.6 kB)
Collecting urllib3<1.27,>=1.21.1
  Using cached urllib3-1.26.9-py2.py3-none-any.whl (138 kB)
Collecting charset-normalizer~=2.0.0
  Using cached charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests>=2.19.0->pooch>=1.0->librosa->-r ./audio-feature-extraction.txt (line 2)) (2020.6.20)
Collecting idna<4,>=2.5
  Using cached idna-3.3-py3-none-any.whl (61 kB)
Requirement already satisfied: six>=1.3 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from resampy>=0.2.2->librosa->-r ./audio-feature-extraction.txt (line 2)) (1.16.0)
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting cffi>=1.0
  Using cached cffi-1.15.0-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (405 kB)
Collecting pycparser
  Using cached pycparser-2.21-py2.py3-none-any.whl (118 kB)
Installing collected packages: urllib3, pycparser, llvmlite, idna, charset-normalizer, threadpoolctl, requests, packaging, numba, cffi, appdirs, soundfile, scikit-learn, resampy, pooch, decorator, audioread, librosa
Successfully installed appdirs-1.4.4 audioread-2.1.9 cffi-1.15.0 charset-normalizer-2.0.12 decorator-5.1.1 idna-3.3 librosa-0.9.1 llvmlite-0.36.0 numba-0.53.1 packaging-21.3 pooch-1.6.0 pycparser-2.21 requests-2.27.1 resampy-0.2.2 scikit-learn-0.24.2 soundfile-0.10.3.post1 threadpoolctl-3.1.0 urllib3-1.26.9
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat build-doc.txt 
Sphinx
sphinxcontrib-napoleon
sphinx_autodoc_typehints
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./build-doc.txt 
Collecting Sphinx
  Using cached Sphinx-4.5.0-py3-none-any.whl (3.1 MB)
Collecting sphinxcontrib-napoleon
  Using cached sphinxcontrib_napoleon-0.7-py2.py3-none-any.whl (17 kB)
Collecting sphinx_autodoc_typehints
  Using cached sphinx_autodoc_typehints-1.12.0-py3-none-any.whl (9.4 kB)
Collecting sphinxcontrib-applehelp
  Using cached sphinxcontrib_applehelp-1.0.2-py2.py3-none-any.whl (121 kB)
Collecting sphinxcontrib-jsmath
  Using cached sphinxcontrib_jsmath-1.0.1-py2.py3-none-any.whl (5.1 kB)
Collecting sphinxcontrib-qthelp
  Using cached sphinxcontrib_qthelp-1.0.3-py2.py3-none-any.whl (90 kB)
Collecting Pygments>=2.0
  Using cached Pygments-2.12.0-py3-none-any.whl (1.1 MB)
Requirement already satisfied: importlib-metadata>=4.4 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from Sphinx->-r ./build-doc.txt (line 1)) (4.8.3)
Collecting babel>=1.3
  Using cached Babel-2.10.1-py3-none-any.whl (9.5 MB)
Collecting docutils<0.18,>=0.14
  Using cached docutils-0.17.1-py2.py3-none-any.whl (575 kB)
Requirement already satisfied: packaging in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from Sphinx->-r ./build-doc.txt (line 1)) (21.3)
Collecting sphinxcontrib-serializinghtml>=1.1.5
  Using cached sphinxcontrib_serializinghtml-1.1.5-py2.py3-none-any.whl (94 kB)
Collecting snowballstemmer>=1.1
  Using cached snowballstemmer-2.2.0-py2.py3-none-any.whl (93 kB)
Collecting alabaster<0.8,>=0.7
  Using cached alabaster-0.7.12-py2.py3-none-any.whl (14 kB)
Collecting sphinxcontrib-htmlhelp>=2.0.0
  Using cached sphinxcontrib_htmlhelp-2.0.0-py2.py3-none-any.whl (100 kB)
Collecting Jinja2>=2.3
  Using cached Jinja2-3.0.3-py3-none-any.whl (133 kB)
Requirement already satisfied: requests>=2.5.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from Sphinx->-r ./build-doc.txt (line 1)) (2.27.1)
Collecting imagesize
  Using cached imagesize-1.3.0-py2.py3-none-any.whl (5.2 kB)
Collecting sphinxcontrib-devhelp
  Using cached sphinxcontrib_devhelp-1.0.2-py2.py3-none-any.whl (84 kB)
Requirement already satisfied: six>=1.5.2 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from sphinxcontrib-napoleon->-r ./build-doc.txt (line 2)) (1.16.0)
Collecting pockets>=0.3
  Using cached pockets-0.9.1-py2.py3-none-any.whl (26 kB)
Collecting pytz>=2015.7
  Using cached pytz-2022.1-py2.py3-none-any.whl (503 kB)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from importlib-metadata>=4.4->Sphinx->-r ./build-doc.txt (line 1)) (3.6.0)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from importlib-metadata>=4.4->Sphinx->-r ./build-doc.txt (line 1)) (4.1.1)
Collecting MarkupSafe>=2.0
  Using cached MarkupSafe-2.0.1-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (30 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests>=2.5.0->Sphinx->-r ./build-doc.txt (line 1)) (2020.6.20)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests>=2.5.0->Sphinx->-r ./build-doc.txt (line 1)) (1.26.9)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests>=2.5.0->Sphinx->-r ./build-doc.txt (line 1)) (3.3)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests>=2.5.0->Sphinx->-r ./build-doc.txt (line 1)) (2.0.12)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from packaging->Sphinx->-r ./build-doc.txt (line 1)) (3.0.8)
Installing collected packages: pytz, MarkupSafe, sphinxcontrib-serializinghtml, sphinxcontrib-qthelp, sphinxcontrib-jsmath, sphinxcontrib-htmlhelp, sphinxcontrib-devhelp, sphinxcontrib-applehelp, snowballstemmer, Pygments, Jinja2, imagesize, docutils, babel, alabaster, Sphinx, pockets, sphinxcontrib-napoleon, sphinx-autodoc-typehints
Successfully installed Jinja2-3.0.3 MarkupSafe-2.0.1 Pygments-2.12.0 Sphinx-4.5.0 alabaster-0.7.12 babel-2.10.1 docutils-0.17.1 imagesize-1.3.0 pockets-0.9.1 pytz-2022.1 snowballstemmer-2.2.0 sphinx-autodoc-typehints-1.12.0 sphinxcontrib-applehelp-1.0.2 sphinxcontrib-devhelp-1.0.2 sphinxcontrib-htmlhelp-2.0.0 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-napoleon-0.7 sphinxcontrib-qthelp-1.0.3 sphinxcontrib-serializinghtml-1.1.5
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat ./ensembling-scripts.txt 
# needed for some scripts under 'script/code'
docopt
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./ensembling-scripts.txt 
Collecting docopt
  Using cached docopt-0.6.2-py2.py3-none-any.whl
Installing collected packages: docopt
Successfully installed docopt-0.6.2
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat lattice.txt 
graphviz
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./lattice.txt 
Collecting graphviz
  Using cached graphviz-0.19.1-py3-none-any.whl (46 kB)
Installing collected packages: graphviz
Successfully installed graphviz-0.19.1
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat sentencepiece.txt 
# Needed when using sentencepiece via !SentencepieceTokenizer or !SentencePieceTextReader
sentencepiece>=0.0.6
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./sentencepiece.txt 
Collecting sentencepiece>=0.0.6
  Using cached sentencepiece-0.1.96-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.2 MB)
Installing collected packages: sentencepiece
Successfully installed sentencepiece-0.1.96
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ cat ./tensorboard.txt 
# for tensorboard visualization; run via 'tensorboard --logdir <path/to/base/xnmt/log/dir>'
tensorflow
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ 
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$ pip install -r ./tensorboard.txt 
Collecting tensorflow
  Using cached tensorflow-2.6.2-cp36-cp36m-manylinux2010_x86_64.whl (458.3 MB)
Collecting google-pasta~=0.2
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Requirement already satisfied: h5py~=3.1.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorflow->-r ./tensorboard.txt (line 2)) (3.1.0)
Collecting opt-einsum~=3.3.0
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Requirement already satisfied: protobuf>=3.9.2 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorflow->-r ./tensorboard.txt (line 2)) (3.19.4)
Collecting six~=1.15.0
  Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting flatbuffers~=1.12.0
  Using cached flatbuffers-1.12-py2.py3-none-any.whl (15 kB)
Collecting keras<2.7,>=2.6.0
  Using cached keras-2.6.0-py2.py3-none-any.whl (1.3 MB)
Collecting clang~=5.0
  Using cached clang-5.0-py3-none-any.whl
Collecting astunparse~=1.6.3
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Requirement already satisfied: wheel~=0.35 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorflow->-r ./tensorboard.txt (line 2)) (0.37.1)
Requirement already satisfied: numpy~=1.19.2 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorflow->-r ./tensorboard.txt (line 2)) (1.19.5)
Collecting keras-preprocessing~=1.1.2
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting gast==0.4.0
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting tensorflow-estimator<2.7,>=2.6.0
  Using cached tensorflow_estimator-2.6.0-py2.py3-none-any.whl (462 kB)
Collecting absl-py~=0.10
  Using cached absl_py-0.15.0-py3-none-any.whl (132 kB)
Collecting grpcio<2.0,>=1.37.0
  Using cached grpcio-1.44.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.3 MB)
Collecting wrapt~=1.12.1
  Using cached wrapt-1.12.1-cp36-cp36m-linux_x86_64.whl
Collecting termcolor~=1.1.0
  Using cached termcolor-1.1.0-py3-none-any.whl
Collecting typing-extensions~=3.7.4
  Using cached typing_extensions-3.7.4.3-py3-none-any.whl (22 kB)
Collecting tensorboard<2.7,>=2.6.0
  Using cached tensorboard-2.6.0-py3-none-any.whl (5.6 MB)
Requirement already satisfied: cached-property in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from h5py~=3.1.0->tensorflow->-r ./tensorboard.txt (line 2)) (1.5.2)
Collecting google-auth<2,>=1.6.3
  Using cached google_auth-1.35.0-py2.py3-none-any.whl (152 kB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.3.6-py3-none-any.whl (97 kB)
Collecting werkzeug>=0.11.15
  Using cached Werkzeug-2.0.3-py3-none-any.whl (289 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Requirement already satisfied: requests<3,>=2.21.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (2.27.1)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (58.0.4)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting rsa<5,>=3.1.4
  Using cached rsa-4.8-py3-none-any.whl (39 kB)
Collecting pyasn1-modules>=0.2.1
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting cachetools<5.0,>=2.0.0
  Using cached cachetools-4.2.4-py3-none-any.whl (10 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Requirement already satisfied: importlib-metadata>=4.4 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from markdown>=2.6.8->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (4.8.3)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (3.6.0)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests<3,>=2.21.0->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (2.0.12)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests<3,>=2.21.0->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (3.3)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests<3,>=2.21.0->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (1.26.9)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages (from requests<3,>=2.21.0->tensorboard<2.7,>=2.6.0->tensorflow->-r ./tensorboard.txt (line 2)) (2020.6.20)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.2.0-py3-none-any.whl (151 kB)
Collecting dataclasses
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Installing collected packages: pyasn1, typing-extensions, six, rsa, pyasn1-modules, oauthlib, cachetools, requests-oauthlib, google-auth, dataclasses, werkzeug, tensorboard-plugin-wit, tensorboard-data-server, markdown, grpcio, google-auth-oauthlib, absl-py, wrapt, termcolor, tensorflow-estimator, tensorboard, opt-einsum, keras-preprocessing, keras, google-pasta, gast, flatbuffers, clang, astunparse, tensorflow
  Attempting uninstall: typing-extensions
    Found existing installation: typing-extensions 4.1.1
    Uninstalling typing-extensions-4.1.1:
      Successfully uninstalled typing-extensions-4.1.1
  Attempting uninstall: six
    Found existing installation: six 1.16.0
    Uninstalling six-1.16.0:
      Successfully uninstalled six-1.16.0
Successfully installed absl-py-0.15.0 astunparse-1.6.3 cachetools-4.2.4 clang-5.0 dataclasses-0.8 flatbuffers-1.12 gast-0.4.0 google-auth-1.35.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.44.0 keras-2.6.0 keras-preprocessing-1.1.2 markdown-3.3.6 oauthlib-3.2.0 opt-einsum-3.3.0 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-oauthlib-1.3.1 rsa-4.8 six-1.15.0 tensorboard-2.6.0 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.6.2 tensorflow-estimator-2.6.0 termcolor-1.1.0 typing-extensions-3.7.4.3 werkzeug-2.0.3 wrapt-1.12.1
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/requirements-extra$
```

## Installation of xnmt

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ python setup.py install
checking git revision in setup.py
running install
running bdist_egg
running egg_info
creating xnmt.egg-info
writing xnmt.egg-info/PKG-INFO
writing dependency_links to xnmt.egg-info/dependency_links.txt
writing entry points to xnmt.egg-info/entry_points.txt
writing requirements to xnmt.egg-info/requires.txt
writing top-level names to xnmt.egg-info/top_level.txt
writing manifest file 'xnmt.egg-info/SOURCES.txt'
reading manifest file 'xnmt.egg-info/SOURCES.txt'
adding license file 'COPYING'
writing manifest file 'xnmt.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/xnmt
copying xnmt/experiments.py -> build/lib/xnmt
copying xnmt/norms.py -> build/lib/xnmt
copying xnmt/xnmt_evaluate.py -> build/lib/xnmt
copying xnmt/reports.py -> build/lib/xnmt
copying xnmt/tee.py -> build/lib/xnmt
copying xnmt/graph.py -> build/lib/xnmt
copying xnmt/search_strategies.py -> build/lib/xnmt
copying xnmt/sentence_stats.py -> build/lib/xnmt
copying xnmt/preproc.py -> build/lib/xnmt
copying xnmt/input_readers.py -> build/lib/xnmt
copying xnmt/optimizers.py -> build/lib/xnmt
copying xnmt/tensor_tools.py -> build/lib/xnmt
copying xnmt/sent.py -> build/lib/xnmt
copying xnmt/transformer.py -> build/lib/xnmt
copying xnmt/levenshtein.py -> build/lib/xnmt
copying xnmt/length_norm.py -> build/lib/xnmt
copying xnmt/output.py -> build/lib/xnmt
copying xnmt/xnmt_decode.py -> build/lib/xnmt
copying xnmt/vocabs.py -> build/lib/xnmt
copying xnmt/losses.py -> build/lib/xnmt
copying xnmt/loss_calculators.py -> build/lib/xnmt
copying xnmt/param_collections.py -> build/lib/xnmt
copying xnmt/param_initializers.py -> build/lib/xnmt
copying xnmt/hyper_params.py -> build/lib/xnmt
copying xnmt/batchers.py -> build/lib/xnmt
copying xnmt/events.py -> build/lib/xnmt
copying xnmt/event_trigger.py -> build/lib/xnmt
copying xnmt/expression_seqs.py -> build/lib/xnmt
copying xnmt/git_rev.py -> build/lib/xnmt
copying xnmt/loss_trackers.py -> build/lib/xnmt
copying xnmt/utils.py -> build/lib/xnmt
copying xnmt/plotting.py -> build/lib/xnmt
copying xnmt/trace.py -> build/lib/xnmt
copying xnmt/persistence.py -> build/lib/xnmt
copying xnmt/__init__.py -> build/lib/xnmt
copying xnmt/inferences.py -> build/lib/xnmt
copying xnmt/settings.py -> build/lib/xnmt
copying xnmt/xnmt_run_experiments.py -> build/lib/xnmt
creating build/lib/xnmt/rl
copying xnmt/rl/policy_gradient.py -> build/lib/xnmt/rl
copying xnmt/rl/eps_greedy.py -> build/lib/xnmt/rl
copying xnmt/rl/confidence_penalty.py -> build/lib/xnmt/rl
copying xnmt/rl/__init__.py -> build/lib/xnmt/rl
creating build/lib/xnmt/specialized_encoders
copying xnmt/specialized_encoders/self_attentional_am.py -> build/lib/xnmt/specialized_encoders
copying xnmt/specialized_encoders/tilburg_harwath.py -> build/lib/xnmt/specialized_encoders
copying xnmt/specialized_encoders/__init__.py -> build/lib/xnmt/specialized_encoders
creating build/lib/xnmt/eval
copying xnmt/eval/metrics.py -> build/lib/xnmt/eval
copying xnmt/eval/tasks.py -> build/lib/xnmt/eval
copying xnmt/eval/__init__.py -> build/lib/xnmt/eval
creating build/lib/xnmt/simultaneous
copying xnmt/simultaneous/simult_search_strategies.py -> build/lib/xnmt/simultaneous
copying xnmt/simultaneous/simult_rewards.py -> build/lib/xnmt/simultaneous
copying xnmt/simultaneous/simult_translators.py -> build/lib/xnmt/simultaneous
copying xnmt/simultaneous/__init__.py -> build/lib/xnmt/simultaneous
copying xnmt/simultaneous/simult_state.py -> build/lib/xnmt/simultaneous
creating build/lib/xnmt/modelparts
copying xnmt/modelparts/embedders.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/decoders.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/bridges.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/scorers.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/attenders.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/transforms.py -> build/lib/xnmt/modelparts
copying xnmt/modelparts/__init__.py -> build/lib/xnmt/modelparts
creating build/lib/xnmt/models
copying xnmt/models/language_models.py -> build/lib/xnmt/models
copying xnmt/models/retrievers.py -> build/lib/xnmt/models
copying xnmt/models/base.py -> build/lib/xnmt/models
copying xnmt/models/classifiers.py -> build/lib/xnmt/models
copying xnmt/models/sequence_labelers.py -> build/lib/xnmt/models
copying xnmt/models/__init__.py -> build/lib/xnmt/models
creating build/lib/xnmt/train
copying xnmt/train/tasks.py -> build/lib/xnmt/train
copying xnmt/train/__init__.py -> build/lib/xnmt/train
copying xnmt/train/regimens.py -> build/lib/xnmt/train
creating build/lib/xnmt/thirdparty
copying xnmt/thirdparty/__init__.py -> build/lib/xnmt/thirdparty
creating build/lib/xnmt/transducers
copying xnmt/transducers/recurrent.py -> build/lib/xnmt/transducers
copying xnmt/transducers/pyramidal.py -> build/lib/xnmt/transducers
copying xnmt/transducers/self_attention.py -> build/lib/xnmt/transducers
copying xnmt/transducers/convolution.py -> build/lib/xnmt/transducers
copying xnmt/transducers/fixed_size_att.py -> build/lib/xnmt/transducers
copying xnmt/transducers/base.py -> build/lib/xnmt/transducers
copying xnmt/transducers/network_in_network.py -> build/lib/xnmt/transducers
copying xnmt/transducers/positional.py -> build/lib/xnmt/transducers
copying xnmt/transducers/residual.py -> build/lib/xnmt/transducers
copying xnmt/transducers/__init__.py -> build/lib/xnmt/transducers
copying xnmt/transducers/lattice.py -> build/lib/xnmt/transducers
creating build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/length_prior.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/priors.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/segmenting_composer.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/segmenting_encoder.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/reporter.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
copying xnmt/specialized_encoders/segmenting_encoder/__init__.py -> build/lib/xnmt/specialized_encoders/segmenting_encoder
creating build/lib/xnmt/models/translators
copying xnmt/models/translators/transformer.py -> build/lib/xnmt/models/translators
copying xnmt/models/translators/auto_regressive.py -> build/lib/xnmt/models/translators
copying xnmt/models/translators/ensemble.py -> build/lib/xnmt/models/translators
copying xnmt/models/translators/default.py -> build/lib/xnmt/models/translators
copying xnmt/models/translators/__init__.py -> build/lib/xnmt/models/translators
creating build/lib/xnmt/thirdparty/charcut
copying xnmt/thirdparty/charcut/charcut.py -> build/lib/xnmt/thirdparty/charcut
copying xnmt/thirdparty/charcut/__init__.py -> build/lib/xnmt/thirdparty/charcut
creating build/lib/xnmt/thirdparty/speech_features
copying xnmt/thirdparty/speech_features/sigproc.py -> build/lib/xnmt/thirdparty/speech_features
copying xnmt/thirdparty/speech_features/base.py -> build/lib/xnmt/thirdparty/speech_features
copying xnmt/thirdparty/speech_features/__init__.py -> build/lib/xnmt/thirdparty/speech_features
creating build/lib/xnmt/thirdparty/comparemt
copying xnmt/thirdparty/comparemt/compare_mt.py -> build/lib/xnmt/thirdparty/comparemt
copying xnmt/thirdparty/comparemt/__init__.py -> build/lib/xnmt/thirdparty/comparemt
creating build/lib/xnmt/thirdparty/dl4mt_simul_trans
copying xnmt/thirdparty/dl4mt_simul_trans/reward.py -> build/lib/xnmt/thirdparty/dl4mt_simul_trans
copying xnmt/thirdparty/dl4mt_simul_trans/bleu.py -> build/lib/xnmt/thirdparty/dl4mt_simul_trans
copying xnmt/thirdparty/dl4mt_simul_trans/__init__.py -> build/lib/xnmt/thirdparty/dl4mt_simul_trans
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/experiments.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/norms.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/rl
copying build/lib/xnmt/rl/policy_gradient.py -> build/bdist.linux-x86_64/egg/xnmt/rl
copying build/lib/xnmt/rl/eps_greedy.py -> build/bdist.linux-x86_64/egg/xnmt/rl
copying build/lib/xnmt/rl/confidence_penalty.py -> build/bdist.linux-x86_64/egg/xnmt/rl
copying build/lib/xnmt/rl/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/rl
copying build/lib/xnmt/xnmt_evaluate.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/reports.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/specialized_encoders
copying build/lib/xnmt/specialized_encoders/self_attentional_am.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders
creating build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/length_prior.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/priors.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/segmenting_composer.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/segmenting_encoder.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/reporter.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/segmenting_encoder/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder
copying build/lib/xnmt/specialized_encoders/tilburg_harwath.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders
copying build/lib/xnmt/specialized_encoders/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/specialized_encoders
copying build/lib/xnmt/tee.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/eval
copying build/lib/xnmt/eval/metrics.py -> build/bdist.linux-x86_64/egg/xnmt/eval
copying build/lib/xnmt/eval/tasks.py -> build/bdist.linux-x86_64/egg/xnmt/eval
copying build/lib/xnmt/eval/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/eval
copying build/lib/xnmt/graph.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/search_strategies.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/sentence_stats.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/preproc.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/input_readers.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/optimizers.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/tensor_tools.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/sent.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/transformer.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/levenshtein.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/length_norm.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/output.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/xnmt_decode.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/vocabs.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/losses.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/loss_calculators.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/simultaneous
copying build/lib/xnmt/simultaneous/simult_search_strategies.py -> build/bdist.linux-x86_64/egg/xnmt/simultaneous
copying build/lib/xnmt/simultaneous/simult_rewards.py -> build/bdist.linux-x86_64/egg/xnmt/simultaneous
copying build/lib/xnmt/simultaneous/simult_translators.py -> build/bdist.linux-x86_64/egg/xnmt/simultaneous
copying build/lib/xnmt/simultaneous/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/simultaneous
copying build/lib/xnmt/simultaneous/simult_state.py -> build/bdist.linux-x86_64/egg/xnmt/simultaneous
creating build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/embedders.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/decoders.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/bridges.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/scorers.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/attenders.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/transforms.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/modelparts/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/modelparts
copying build/lib/xnmt/param_collections.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/param_initializers.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/hyper_params.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/batchers.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/events.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/event_trigger.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/models/language_models.py -> build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/models/retrievers.py -> build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/models/base.py -> build/bdist.linux-x86_64/egg/xnmt/models
creating build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/translators/transformer.py -> build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/translators/auto_regressive.py -> build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/translators/ensemble.py -> build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/translators/default.py -> build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/translators/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/models/translators
copying build/lib/xnmt/models/classifiers.py -> build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/models/sequence_labelers.py -> build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/models/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/models
copying build/lib/xnmt/expression_seqs.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/git_rev.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/loss_trackers.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/utils.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/train
copying build/lib/xnmt/train/tasks.py -> build/bdist.linux-x86_64/egg/xnmt/train
copying build/lib/xnmt/train/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/train
copying build/lib/xnmt/train/regimens.py -> build/bdist.linux-x86_64/egg/xnmt/train
copying build/lib/xnmt/plotting.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/trace.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/persistence.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/__init__.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/thirdparty
creating build/bdist.linux-x86_64/egg/xnmt/thirdparty/charcut
copying build/lib/xnmt/thirdparty/charcut/charcut.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/charcut
copying build/lib/xnmt/thirdparty/charcut/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/charcut
creating build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features
copying build/lib/xnmt/thirdparty/speech_features/sigproc.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features
copying build/lib/xnmt/thirdparty/speech_features/base.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features
copying build/lib/xnmt/thirdparty/speech_features/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features
creating build/bdist.linux-x86_64/egg/xnmt/thirdparty/comparemt
copying build/lib/xnmt/thirdparty/comparemt/compare_mt.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/comparemt
copying build/lib/xnmt/thirdparty/comparemt/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/comparemt
creating build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans
copying build/lib/xnmt/thirdparty/dl4mt_simul_trans/reward.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans
copying build/lib/xnmt/thirdparty/dl4mt_simul_trans/bleu.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans
copying build/lib/xnmt/thirdparty/dl4mt_simul_trans/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans
copying build/lib/xnmt/thirdparty/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/thirdparty
copying build/lib/xnmt/inferences.py -> build/bdist.linux-x86_64/egg/xnmt
creating build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/recurrent.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/pyramidal.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/self_attention.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/convolution.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/fixed_size_att.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/base.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/network_in_network.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/positional.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/residual.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/__init__.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/transducers/lattice.py -> build/bdist.linux-x86_64/egg/xnmt/transducers
copying build/lib/xnmt/settings.py -> build/bdist.linux-x86_64/egg/xnmt
copying build/lib/xnmt/xnmt_run_experiments.py -> build/bdist.linux-x86_64/egg/xnmt
byte-compiling build/bdist.linux-x86_64/egg/xnmt/experiments.py to experiments.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/norms.py to norms.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/rl/policy_gradient.py to policy_gradient.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/rl/eps_greedy.py to eps_greedy.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/rl/confidence_penalty.py to confidence_penalty.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/rl/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/xnmt_evaluate.py to xnmt_evaluate.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/reports.py to reports.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/self_attentional_am.py to self_attentional_am.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/length_prior.py to length_prior.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/priors.py to priors.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/segmenting_composer.py to segmenting_composer.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/segmenting_encoder.py to segmenting_encoder.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/reporter.py to reporter.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/segmenting_encoder/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/tilburg_harwath.py to tilburg_harwath.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/specialized_encoders/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/tee.py to tee.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/eval/metrics.py to metrics.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/eval/tasks.py to tasks.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/eval/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/graph.py to graph.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/search_strategies.py to search_strategies.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/sentence_stats.py to sentence_stats.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/preproc.py to preproc.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/input_readers.py to input_readers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/optimizers.py to optimizers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/tensor_tools.py to tensor_tools.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/sent.py to sent.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transformer.py to transformer.cpython-36.pyc
build/bdist.linux-x86_64/egg/xnmt/transformer.py:127: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_Q.dim() == (n_units // h, n_querys), batch * h)
build/bdist.linux-x86_64/egg/xnmt/transformer.py:128: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_K.dim() == (n_units // h, n_keys), batch * h)
build/bdist.linux-x86_64/egg/xnmt/transformer.py:129: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_V.dim() == (n_units // h, n_keys), batch * h)
byte-compiling build/bdist.linux-x86_64/egg/xnmt/levenshtein.py to levenshtein.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/length_norm.py to length_norm.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/output.py to output.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/xnmt_decode.py to xnmt_decode.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/vocabs.py to vocabs.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/losses.py to losses.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/loss_calculators.py to loss_calculators.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/simultaneous/simult_search_strategies.py to simult_search_strategies.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/simultaneous/simult_rewards.py to simult_rewards.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/simultaneous/simult_translators.py to simult_translators.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/simultaneous/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/simultaneous/simult_state.py to simult_state.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/embedders.py to embedders.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/decoders.py to decoders.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/bridges.py to bridges.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/scorers.py to scorers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/attenders.py to attenders.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/transforms.py to transforms.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/modelparts/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/param_collections.py to param_collections.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/param_initializers.py to param_initializers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/hyper_params.py to hyper_params.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/batchers.py to batchers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/events.py to events.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/event_trigger.py to event_trigger.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/language_models.py to language_models.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/retrievers.py to retrievers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/base.py to base.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/translators/transformer.py to transformer.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/translators/auto_regressive.py to auto_regressive.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/translators/ensemble.py to ensemble.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/translators/default.py to default.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/translators/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/classifiers.py to classifiers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/sequence_labelers.py to sequence_labelers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/models/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/expression_seqs.py to expression_seqs.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/git_rev.py to git_rev.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/loss_trackers.py to loss_trackers.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/utils.py to utils.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/train/tasks.py to tasks.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/train/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/train/regimens.py to regimens.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/plotting.py to plotting.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/trace.py to trace.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/persistence.py to persistence.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/charcut/charcut.py to charcut.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/charcut/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features/sigproc.py to sigproc.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features/base.py to base.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/speech_features/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/comparemt/compare_mt.py to compare_mt.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/comparemt/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans/reward.py to reward.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans/bleu.py to bleu.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/dl4mt_simul_trans/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/thirdparty/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/inferences.py to inferences.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/recurrent.py to recurrent.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/pyramidal.py to pyramidal.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/self_attention.py to self_attention.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/convolution.py to convolution.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/fixed_size_att.py to fixed_size_att.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/base.py to base.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/network_in_network.py to network_in_network.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/positional.py to positional.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/residual.py to residual.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/transducers/lattice.py to lattice.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/settings.py to settings.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/xnmt/xnmt_run_experiments.py to xnmt_run_experiments.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying xnmt.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
xnmt.__pycache__.__init__.cpython-36: module references __file__
xnmt.__pycache__.tee.cpython-36: module references __file__
xnmt.__pycache__.xnmt_decode.cpython-36: module references __file__
creating dist
creating 'dist/xnmt-0.0.1-py3.6.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing xnmt-0.0.1-py3.6.egg
creating /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg
Extracting xnmt-0.0.1-py3.6.egg to /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/transformer.py:127: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_Q.dim() == (n_units // h, n_querys), batch * h)
/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/transformer.py:128: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_K.dim() == (n_units // h, n_keys), batch * h)
/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/transformer.py:129: SyntaxWarning: assertion is always true, perhaps remove parentheses?
  assert(batch_V.dim() == (n_units // h, n_keys), batch * h)
Adding xnmt 0.0.1 to easy-install.pth file
Installing xnmt script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing xnmt_decode script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing xnmt_evaluate script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Installed /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg
Processing dependencies for xnmt==0.0.1
Searching for tensorboardX==1.6
Best match: tensorboardX 1.6
Adding tensorboardX 1.6 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for pylru==1.2.1
Best match: pylru 1.2.1
Adding pylru 1.2.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for nltk==3.6.7
Best match: nltk 3.6.7
Adding nltk 3.6.7 to easy-install.pth file
Installing nltk script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for beautifulsoup4==4.11.1
Best match: beautifulsoup4 4.11.1
Adding beautifulsoup4 4.11.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for Unidecode==1.3.4
Best match: Unidecode 1.3.4
Adding Unidecode 1.3.4 to easy-install.pth file
Installing unidecode script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for numpy==1.19.5
Best match: numpy 1.19.5
Adding numpy 1.19.5 to easy-install.pth file
Installing f2py script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing f2py3 script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing f2py3.6 script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for asteval==0.9.26
Best match: asteval 0.9.26
Adding asteval 0.9.26 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for h5py==3.1.0
Best match: h5py 3.1.0
Adding h5py 3.1.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for Cython==0.29.28
Best match: Cython 0.29.28
Adding Cython 0.29.28 to easy-install.pth file
Installing cygdb script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing cython script to /home/ye/anaconda3/envs/xnmt-py3.6/bin
Installing cythonize script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for matplotlib==3.3.4
Best match: matplotlib 3.3.4
Adding matplotlib 3.3.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for dyNET==2.1.2
Best match: dyNET 2.1.2
Adding dyNET 2.1.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for lxml==4.8.0
Best match: lxml 4.8.0
Adding lxml 4.8.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for scipy==1.5.4
Best match: scipy 1.5.4
Adding scipy 1.5.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for PyYAML==6.0
Best match: PyYAML 6.0
Adding PyYAML 6.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for protobuf==3.19.4
Best match: protobuf 3.19.4
Adding protobuf 3.19.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for joblib==1.1.0
Best match: joblib 1.1.0
Adding joblib 1.1.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for click==8.0.4
Best match: click 8.0.4
Adding click 8.0.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for tqdm==4.64.0
Best match: tqdm 4.64.0
Adding tqdm 4.64.0 to easy-install.pth file
Installing tqdm script to /home/ye/anaconda3/envs/xnmt-py3.6/bin

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for regex==2022.4.24
Best match: regex 2022.4.24
Adding regex 2022.4.24 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for soupsieve==2.3.2.post1
Best match: soupsieve 2.3.2.post1
Adding soupsieve 2.3.2.post1 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for importlib-metadata==4.8.3
Best match: importlib-metadata 4.8.3
Adding importlib-metadata 4.8.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for cached-property==1.5.2
Best match: cached-property 1.5.2
Adding cached-property 1.5.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for kiwisolver==1.3.1
Best match: kiwisolver 1.3.1
Adding kiwisolver 1.3.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for Pillow==8.4.0
Best match: Pillow 8.4.0
Adding Pillow 8.4.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for pyparsing==3.0.8
Best match: pyparsing 3.0.8
Adding pyparsing 3.0.8 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for cycler==0.11.0
Best match: cycler 0.11.0
Adding cycler 0.11.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for python-dateutil==2.8.2
Best match: python-dateutil 2.8.2
Adding python-dateutil 2.8.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for importlib-resources==5.4.0
Best match: importlib-resources 5.4.0
Adding importlib-resources 5.4.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for typing-extensions==3.7.4.3
Best match: typing-extensions 3.7.4.3
Adding typing-extensions 3.7.4.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Searching for zipp==3.6.0
Best match: zipp 3.6.0
Adding zipp 3.6.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages
Finished processing dependencies for xnmt==0.0.1
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

ပထမတစ်ခေါက်တုန်းကလည်း ဒီအဆင့်အထိက အဆင်ပြေခဲ့တယ်လို့ ထင်တယ်။ ပြီးမှ xnmt ကို training လုပ်ကြည့်တော့မှ DyNet GPU support လုပ်အောင် installation လုပ်မထားဘူး ဆိုတဲ့ error ပေးခဲ့တာ...  

## Call --help

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ xnmt
xnmt           xnmt_decode    xnmt_evaluate  
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ xnmt --help
usage: xnmt [-h] [--backend BACKEND] [--gpu]

optional arguments:
  -h, --help         show this help message and exit
  --backend BACKEND
  --gpu
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ xnmt_decode --help
usage: xnmt_decode [-h] [--backend BACKEND] [--gpu]

optional arguments:
  -h, --help         show this help message and exit
  --backend BACKEND
  --gpu
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ xnmt_evaluate --help
usage: xnmt_evaluate [-h] [--backend BACKEND] [--gpu]

optional arguments:
  -h, --help         show this help message and exit
  --backend BACKEND
  --gpu
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

## Check configuration Files

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ ls ./examples/
01_standard.yaml       04_settings.yaml        09_programmatic.py         14_report.yaml       19_subword_sample.yaml  data
02_minimal.yaml        05_preproc.yaml         10_programmatic_load.py    15_score.yaml        20_self_attention.yaml  README
03a_multiple_exp.yaml  06_early_stopping.yaml  11_component_sharing.yaml  16_ensembling.yaml   21_char_segment.yaml
03b_multiple_exp.yaml  07_load_finetune.yaml   12_multi_task.yaml         17_minrisk.yaml      22_switchout.yaml
03c_multiple_exp.yaml  08_load_eval_beam.yaml  13_speech.yaml             18_lexiconbias.yaml  23_autobatch.yaml
```

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ cat ./examples/01_standard.yaml 
# A standard setup, specifying model architecture, training parameters, 
# and evaluation of the trained model
!Experiment # 'standard' is the name given to the experiment
  name: standard # every experiment needs a name
  # global parameters shared throughout the experiment
  exp_global: !ExpGlobal
    # {EXP_DIR} is a placeholder for the directory in which the config file lies.
    # {EXP} is a placeholder for the experiment name (here: 'standard')
    model_file: '{EXP_DIR}/models/{EXP}.mod'
    log_file: '{EXP_DIR}/logs/{EXP}.log'
    default_layer_dim: 512
    dropout: 0.3
  # model architecture
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: examples/data/head.ja.vocab}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: examples/data/head.en.vocab}
    src_embedder: !SimpleWordEmbedder
      emb_dim: 512
    encoder: !BiLSTMSeqTransducer
      layers: 1
    attender: !MlpAttender
      hidden_dim: 512
      state_dim: 512
      input_dim: 512
    decoder: !AutoRegressiveDecoder
      embedder: !SimpleWordEmbedder
        emb_dim: 512
      rnn: !UniLSTMSeqTransducer
        layers: 1
      transform: !AuxNonLinear
        output_dim: 512
        activation: 'tanh'
      bridge: !CopyBridge {}
      scorer: !Softmax {}
  # training parameters
  train: !SimpleTrainingRegimen
    batcher: !SrcBatcher
      batch_size: 32
    trainer: !AdamTrainer
      alpha: 0.001
    run_for_epochs: 2
    src_file: examples/data/head.ja
    trg_file: examples/data/head.en
    dev_tasks:
      - !LossEvalTask
        src_file: examples/data/head.ja
        ref_file: examples/data/head.en
  # final evaluation
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu
      src_file: examples/data/head.ja
      ref_file: examples/data/head.en
      hyp_file: examples/output/{EXP}.test_hyp
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

## Training with 01 config

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ time xnmt --dynet-gpu ./examples/01_standard.yaml 
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 33, in <module>
    sys.exit(load_entry_point('xnmt==0.0.1', 'console_scripts', 'xnmt')())
  File "/home/ye/anaconda3/envs/xnmt-py3.6/bin/xnmt", line 25, in importlib_load_entry_point
    return next(matches).load()
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/importlib_metadata/__init__.py", line 194, in load
    module = import_module(match.group('module'))
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/importlib/__init__.py", line 126, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 994, in _gcd_import
  File "<frozen importlib._bootstrap>", line 971, in _find_and_load
  File "<frozen importlib._bootstrap>", line 941, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "<frozen importlib._bootstrap>", line 994, in _gcd_import
  File "<frozen importlib._bootstrap>", line 971, in _find_and_load
  File "<frozen importlib._bootstrap>", line 955, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 665, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 678, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/__init__.py", line 74, in <module>
    import xnmt.batchers
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py", line 14, in <module>
    from xnmt import tensor_tools as tt
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/tensor_tools.py", line 18, in <module>
    from xnmt import param_collections, trace
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/param_collections.py", line 14, in <module>
    import dynet as dy
  File "/home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/dynet.py", line 25, in <module>
    raise RuntimeError(ERRMSG)
RuntimeError: DyNet was not installed with GPU support. Please see the installation instructions for how to make it possible to use GPUs.

real	0m0.198s
user	0m0.604s
sys	0m0.516s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

ERROR ပေးတယ်။  

## Installation of pytorch

Backend ကို dynet မထားပဲနဲ့ pytorch ကိုလည်း သုံးလို့ ရတာမို့ pytorch နဲ့လည်း စမ်းကြည့်ဖို့ ဆုံးဖြတ်ပြီး pytorch ကို installation လုပ်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt$ conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=11.3 -c pytorch -c conda-forge
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/xnmt-py3.6

  added / updated specs:
    - cudatoolkit=11.3
    - pytorch==1.10.1
    - torchaudio==0.10.1
    - torchvision==0.11.2


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    bzip2-1.0.8                |       h7f98852_4         484 KB  conda-forge
    ca-certificates-2021.10.8  |       ha878542_0         139 KB  conda-forge
    certifi-2016.9.26          |           py36_0         217 KB  conda-forge
    dataclasses-0.8            |     pyh787bdff_2          22 KB  conda-forge
    ffmpeg-4.3                 |       hf484d3e_0         9.9 MB  pytorch
    freetype-2.10.4            |       h0708190_1         890 KB  conda-forge
    gmp-6.2.1                  |       h58526e2_0         806 KB  conda-forge
    gnutls-3.6.13              |       h85f3911_1         2.0 MB  conda-forge
    intel-openmp-2022.0.1      |    h06a4308_3633         4.2 MB
    jpeg-9e                    |       h7f8727e_0         240 KB
    lame-3.100                 |    h7f98852_1001         496 KB  conda-forge
    libblas-3.9.0              |   14_linux64_mkl          13 KB  conda-forge
    libcblas-3.9.0             |   14_linux64_mkl          12 KB  conda-forge
    libiconv-1.16              |       h516909a_0         1.4 MB  conda-forge
    liblapack-3.9.0            |   14_linux64_mkl          12 KB  conda-forge
    libpng-1.6.37              |       h21135ba_2         306 KB  conda-forge
    libtiff-4.0.10             |    hc3755c2_1005         602 KB  conda-forge
    libuv-1.40.0               |       h7b6447c_0         736 KB
    lz4-c-1.9.3                |       h9c3ff4c_1         179 KB  conda-forge
    mkl-2022.0.1               |     h06a4308_117       127.7 MB
    nettle-3.6                 |       he412f7d_0         6.5 MB  conda-forge
    numpy-1.19.5               |   py36hfc0c790_2         5.3 MB  conda-forge
    olefile-0.46               |     pyh9f0ad1d_1          32 KB  conda-forge
    openh264-2.1.1             |       h780b84a_0         1.5 MB  conda-forge
    pillow-6.2.1               |   py36h6b7be26_0         639 KB  conda-forge
    python_abi-3.6             |          2_cp36m           4 KB  conda-forge
    pytorch-1.10.1             |py3.6_cuda11.3_cudnn8.2.0_0        1.21 GB  pytorch
    pytorch-mutex-1.0          |             cuda           3 KB  pytorch
    torchaudio-0.10.1          |       py36_cu113         4.5 MB  pytorch
    torchvision-0.11.2         |       py36_cu113        30.4 MB  pytorch
    typing_extensions-3.10.0.2 |     pyha770c72_0          28 KB  conda-forge
    zstd-1.4.9                 |       ha95c52a_0         431 KB  conda-forge
    ------------------------------------------------------------
                                           Total:        1.40 GB

The following NEW packages will be INSTALLED:

  blas               pkgs/main/linux-64::blas-1.0-mkl
  bzip2              conda-forge/linux-64::bzip2-1.0.8-h7f98852_4
  cudatoolkit        pkgs/main/linux-64::cudatoolkit-11.3.1-h2bc3f7f_2
  dataclasses        conda-forge/noarch::dataclasses-0.8-pyh787bdff_2
  ffmpeg             pytorch/linux-64::ffmpeg-4.3-hf484d3e_0
  freetype           conda-forge/linux-64::freetype-2.10.4-h0708190_1
  gmp                conda-forge/linux-64::gmp-6.2.1-h58526e2_0
  gnutls             conda-forge/linux-64::gnutls-3.6.13-h85f3911_1
  intel-openmp       pkgs/main/linux-64::intel-openmp-2022.0.1-h06a4308_3633
  jpeg               pkgs/main/linux-64::jpeg-9e-h7f8727e_0
  lame               conda-forge/linux-64::lame-3.100-h7f98852_1001
  libblas            conda-forge/linux-64::libblas-3.9.0-14_linux64_mkl
  libcblas           conda-forge/linux-64::libcblas-3.9.0-14_linux64_mkl
  libiconv           conda-forge/linux-64::libiconv-1.16-h516909a_0
  liblapack          conda-forge/linux-64::liblapack-3.9.0-14_linux64_mkl
  libpng             conda-forge/linux-64::libpng-1.6.37-h21135ba_2
  libtiff            conda-forge/linux-64::libtiff-4.0.10-hc3755c2_1005
  libuv              pkgs/main/linux-64::libuv-1.40.0-h7b6447c_0
  lz4-c              conda-forge/linux-64::lz4-c-1.9.3-h9c3ff4c_1
  mkl                pkgs/main/linux-64::mkl-2022.0.1-h06a4308_117
  nettle             conda-forge/linux-64::nettle-3.6-he412f7d_0
  numpy              conda-forge/linux-64::numpy-1.19.5-py36hfc0c790_2
  olefile            conda-forge/noarch::olefile-0.46-pyh9f0ad1d_1
  openh264           conda-forge/linux-64::openh264-2.1.1-h780b84a_0
  pillow             conda-forge/linux-64::pillow-6.2.1-py36h6b7be26_0
  python_abi         conda-forge/linux-64::python_abi-3.6-2_cp36m
  pytorch            pytorch/linux-64::pytorch-1.10.1-py3.6_cuda11.3_cudnn8.2.0_0
  pytorch-mutex      pytorch/noarch::pytorch-mutex-1.0-cuda
  torchaudio         pytorch/linux-64::torchaudio-0.10.1-py36_cu113
  torchvision        pytorch/linux-64::torchvision-0.11.2-py36_cu113
  typing_extensions  conda-forge/noarch::typing_extensions-3.10.0.2-pyha770c72_0
  zstd               conda-forge/linux-64::zstd-1.4.9-ha95c52a_0

The following packages will be SUPERSEDED by a higher-priority channel:

  ca-certificates    pkgs/main::ca-certificates-2022.3.29-~ --> conda-forge::ca-certificates-2021.10.8-ha878542_0
  certifi            pkgs/main/noarch::certifi-2020.6.20-p~ --> conda-forge/linux-64::certifi-2016.9.26-py36_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
ca-certificates-2021 | 139 KB    | ################################################################################### | 100% 
freetype-2.10.4      | 890 KB    | ################################################################################### | 100% 
gnutls-3.6.13        | 2.0 MB    | ################################################################################### | 100% 
zstd-1.4.9           | 431 KB    | ################################################################################### | 100% 
gmp-6.2.1            | 806 KB    | ################################################################################### | 100% 
openh264-2.1.1       | 1.5 MB    | ################################################################################### | 100% 
mkl-2022.0.1         | 127.7 MB  | ################################################################################### | 100% 
olefile-0.46         | 32 KB     | ################################################################################### | 100% 
dataclasses-0.8      | 22 KB     | ################################################################################### | 100% 
lame-3.100           | 496 KB    | ################################################################################### | 100% 
ffmpeg-4.3           | 9.9 MB    | ################################################################################### | 100% 
intel-openmp-2022.0. | 4.2 MB    | ################################################################################### | 100% 
libpng-1.6.37        | 306 KB    | ################################################################################### | 100% 
bzip2-1.0.8          | 484 KB    | ################################################################################### | 100% 
certifi-2016.9.26    | 217 KB    | ################################################################################### | 100% 
libcblas-3.9.0       | 12 KB     | ################################################################################### | 100% 
pillow-6.2.1         | 639 KB    | ################################################################################### | 100% 
liblapack-3.9.0      | 12 KB     | ################################################################################### | 100% 
lz4-c-1.9.3          | 179 KB    | ################################################################################### | 100% 
numpy-1.19.5         | 5.3 MB    | ################################################################################### | 100% 
torchaudio-0.10.1    | 4.5 MB    | ################################################################################### | 100% 
pytorch-1.10.1       | 1.21 GB   | ################################################################################### | 100% 
python_abi-3.6       | 4 KB      | ################################################################################### | 100% 
typing_extensions-3. | 28 KB     | ################################################################################### | 100% 
pytorch-mutex-1.0    | 3 KB      | ################################################################################### | 100% 
torchvision-0.11.2   | 30.4 MB   | ################################################################################### | 100% 
libiconv-1.16        | 1.4 MB    | ################################################################################### | 100% 
libtiff-4.0.10       | 602 KB    | ################################################################################### | 100% 
nettle-3.6           | 6.5 MB    | ################################################################################### | 100% 
libblas-3.9.0        | 13 KB     | ################################################################################### | 100% 
jpeg-9e              | 240 KB    | ################################################################################### | 100% 
libuv-1.40.0         | 736 KB    | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: \ By downloading and using the CUDA Toolkit conda packages, you accept the terms and conditions of the CUDA End User License Agreement (EULA): https://docs.nvidia.com/cuda/eula/index.html

done
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt$
```

import စမ်းလုပ်ကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.__version__)
1.10.1
>>> exit()
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/xnmt$
```

## checking command line arguments

တကယ်က --help နဲ့က အထက်မှာ ကြည့်ခဲ့တဲ့အတိုင်းပဲ ဘာမှ သိပ်မပြောထားဘူး။ source code (xnmt_run_experiments.py) ထဲကို ဝင်ကြည့်မှပဲ ပိုသိရတယ်။  

```python
def main(overwrite_args: Optional[Sequence[str]] = None) -> None:

  with tee.Tee(), tee.Tee(error=True):
    argparser = argparse.ArgumentParser()
    utils.add_backend_argparse(argparser)
    argparser.add_argument("--settings", type=str, default="standard", help="settings (standard, debug, or unittest)"
                                                                            "must be given in '=' syntax, e.g."
                                                                            " --settings=standard")
    argparser.add_argument("--resume", action='store_true', help="whether a saved experiment is being resumed, and"
                                                                 "locations of output files should be re-used.")
    argparser.add_argument("--backend", type=str, default="dynet", help="backend (dynet or torch)")
    argparser.add_argument("experiments_file")
    argparser.add_argument("experiment_name", nargs='*', help="Run only the specified experiments")
    argparser.set_defaults(generate_doc=False)
    args = argparser.parse_args(overwrite_args)
```


## Test Training with pytorch Backend

အချိန်က သိပ်မရလို့ အဆင်ပြေပြေနဲ့ run လို့ ရဖို့ မျှော်လင့်တယ်...  


```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ time xnmt --backend torch --gpu ./examples/01_standard.yaml 
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-01 13:29:55
=> Running standard
> use randomly initialized neural network parameters for all components
  neural network param count: 5884997
> Training
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
[standard] Epoch 1.0000: train_loss/word=4.693482 (steps=1, words/sec=175.42, time=0-00:00:00)
> Checkpoint [standard]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[standard] Epoch 1.0000 dev Loss: 4.592 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
[standard] Epoch 2.0000: train_loss/word=4.593520 (steps=2, words/sec=2369.35, time=0-00:00:00)
> Checkpoint [standard]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[standard] Epoch 2.0000 dev Loss: 4.460 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on examples/data/head.ja and examples/data/head.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
standard                      | BLEU4: 0.0, 0.470588/0.000000/0.000000/0.000000 (BP = 0.012869, ratio=0.19, hyp_len=17, ref_len=91)

real	0m4.799s
user	0m3.937s
sys	0m1.431s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

## Test Run with KFTT Data

README ဖိုင်ကို ဝင်ဖတ်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ cat README.md 
This trains a neural machine translation model on the [KFTT](http://www.phontron.com/kftt/) en-ja data.

How to run

    # Download data
    ./download.sh
    # Train model
    xnmt --dynet-gpu ./config.kftt.en-ja.yaml

On a GTX 1080 Ti this trains at ~2700-2800 words/sec and achieves a BLEU score of 23.14 after 12 epochs of training.

Reference output after the final evaluation, for random seed `3301906583`:

    Experiment                    | Final Scores
    -----------------------------------------------------------------------
    kftt.en-ja                    | BLEU4: 0.20526004248457844, 0.574099/0.306461/0.179848/0.114350 (BP = 0.836909, ratio=0.85, hyp_len=22787, ref_len=26844)
                                  | BLEU4: 0.23145703986424254, 0.593274/0.333834/0.205808/0.136245 (BP = 0.847868, ratio=0.86, hyp_len=24444, ref_len=28478)
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$
```

အရင်ဆုံး corpus ကို download လုပ်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ ls
config.kftt.en-ja.yaml  download.sh  README.md
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ ./download.sh 
/bin/bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by /bin/bash)
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-01 13:40:51--  http://www.phontron.com/kftt/download/kftt-data-1.0.tar.gz
Resolving www.phontron.com (www.phontron.com)... 208.113.196.149
Connecting to www.phontron.com (www.phontron.com)|208.113.196.149|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 99246893 (95M) [application/gzip]
Saving to: ‘kftt-data-1.0.tar.gz’

kftt-data-1.0.tar.gz            100%[=====================================================>]  94.65M  11.2MB/s    in 10s     

2022-05-01 13:41:02 (9.28 MB/s) - ‘kftt-data-1.0.tar.gz’ saved [99246893/99246893]

kftt-data-1.0/data/tok/
kftt-data-1.0/data/tok/kyoto-tune.en
kftt-data-1.0/data/tok/kyoto-dev.ja
kftt-data-1.0/data/tok/kyoto-train.cln.en
kftt-data-1.0/data/tok/kyoto-dev.en
kftt-data-1.0/data/tok/kyoto-train.en
kftt-data-1.0/data/tok/kyoto-tune.ja
kftt-data-1.0/data/tok/kyoto-train.cln.ja
kftt-data-1.0/data/tok/kyoto-train.ja
kftt-data-1.0/data/tok/kyoto-test.ja
kftt-data-1.0/data/tok/kyoto-test.en
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$
```

config ဖိုင်က အောက်ပါအတိုင်း...  

```yaml
# standard settings
kftt.en-ja: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.en'
      - '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.ja'
      out_files:
      - '{EXP_DIR}/vocab.en'
      - '{EXP_DIR}/vocab.ja'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 40000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
    trg_reader: !PlainTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.ja'}
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 20  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.en'
    trg_file: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.ja'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu
        src_file: &dev_src '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.en'
        ref_file: &dev_trg '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.ja'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.ja'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.ja'
    - !AccuracyEvalTask
      eval_metrics: bleu
      src_file: &test_src '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-test.en'
      ref_file: &test_trg '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-test.ja'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.ja'

```

start training ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ time xnmt --backend torch --gpu ./config.kftt.en-ja.yaml | tee training.log
...
...
...
[kftt.en-ja] Epoch 8.7505: train_loss/word=2.915795 (steps=60455, words/sec=6502.15, time=0-02:58:28)
[kftt.en-ja] Epoch 8.7536: train_loss/word=2.917960 (steps=60471, words/sec=7091.32, time=0-02:58:30)
[kftt.en-ja] Epoch 8.7567: train_loss/word=2.822938 (steps=60490, words/sec=6841.46, time=0-02:58:33)
[kftt.en-ja] Epoch 8.7598: train_loss/word=2.849215 (steps=60514, words/sec=6749.49, time=0-02:58:37)
[kftt.en-ja] Epoch 8.7629: train_loss/word=2.861567 (steps=60538, words/sec=6386.54, time=0-02:58:41)
[kftt.en-ja] Epoch 8.7660: train_loss/word=2.855167 (steps=60558, words/sec=6537.59, time=0-02:58:44)
[kftt.en-ja] Epoch 8.7691: train_loss/word=2.850161 (steps=60581, words/sec=6390.28, time=0-02:58:47)
[kftt.en-ja] Epoch 8.7724: train_loss/word=2.861889 (steps=60602, words/sec=6651.37, time=0-02:58:51)
[kftt.en-ja] Epoch 8.7755: train_loss/word=2.885655 (steps=60624, words/sec=6597.26, time=0-02:58:54)
[kftt.en-ja] Epoch 8.7786: train_loss/word=2.931132 (steps=60646, words/sec=6600.03, time=0-02:58:58)
[kftt.en-ja] Epoch 8.7816: train_loss/word=2.871369 (steps=60665, words/sec=6944.43, time=0-02:59:00)
[kftt.en-ja] Epoch 8.7847: train_loss/word=2.884183 (steps=60686, words/sec=6790.38, time=0-02:59:04)
[kftt.en-ja] Epoch 8.7878: train_loss/word=2.898026 (steps=60709, words/sec=6921.74, time=0-02:59:07)
[kftt.en-ja] Epoch 8.7909: train_loss/word=2.928635 (steps=60727, words/sec=6530.05, time=0-02:59:10)
[kftt.en-ja] Epoch 8.7941: train_loss/word=2.873140 (steps=60750, words/sec=6689.45, time=0-02:59:14)
[kftt.en-ja] Epoch 8.7972: train_loss/word=2.907810 (steps=60776, words/sec=6428.97, time=0-02:59:18)
[kftt.en-ja] Epoch 8.8003: train_loss/word=2.874352 (steps=60799, words/sec=6709.17, time=0-02:59:22)
[kftt.en-ja] Epoch 8.8035: train_loss/word=2.863333 (steps=60820, words/sec=6688.48, time=0-02:59:25)
[kftt.en-ja] Epoch 8.8065: train_loss/word=2.939122 (steps=60840, words/sec=6714.99, time=0-02:59:28)
[kftt.en-ja] Epoch 8.8096: train_loss/word=2.865530 (steps=60861, words/sec=6616.61, time=0-02:59:31)
[kftt.en-ja] Epoch 8.8127: train_loss/word=2.902620 (steps=60885, words/sec=6716.94, time=0-02:59:35)
[kftt.en-ja] Epoch 8.8158: train_loss/word=2.852586 (steps=60907, words/sec=6542.71, time=0-02:59:39)
[kftt.en-ja] Epoch 8.8189: train_loss/word=2.907211 (steps=60932, words/sec=6519.93, time=0-02:59:43)
[kftt.en-ja] Epoch 8.8220: train_loss/word=2.883810 (steps=60952, words/sec=6734.73, time=0-02:59:46)
[kftt.en-ja] Epoch 8.8251: train_loss/word=2.909509 (steps=60975, words/sec=6574.14, time=0-02:59:50)
[kftt.en-ja] Epoch 8.8281: train_loss/word=2.910170 (steps=60995, words/sec=6618.24, time=0-02:59:53)
[kftt.en-ja] Epoch 8.8312: train_loss/word=2.848548 (steps=61017, words/sec=6811.18, time=0-02:59:56)
[kftt.en-ja] Epoch 8.8342: train_loss/word=2.834950 (steps=61037, words/sec=6414.55, time=0-02:59:59)
[kftt.en-ja] Epoch 8.8373: train_loss/word=2.917147 (steps=61059, words/sec=6566.38, time=0-03:00:03)
[kftt.en-ja] Epoch 8.8404: train_loss/word=2.875751 (steps=61079, words/sec=6293.85, time=0-03:00:06)
[kftt.en-ja] Epoch 8.8436: train_loss/word=2.755098 (steps=61098, words/sec=6932.04, time=0-03:00:09)
[kftt.en-ja] Epoch 8.8467: train_loss/word=2.888348 (steps=61121, words/sec=6529.16, time=0-03:00:13)
[kftt.en-ja] Epoch 8.8497: train_loss/word=2.895965 (steps=61143, words/sec=6618.55, time=0-03:00:16)
[kftt.en-ja] Epoch 8.8528: train_loss/word=2.852120 (steps=61162, words/sec=6999.24, time=0-03:00:19)
[kftt.en-ja] Epoch 8.8561: train_loss/word=2.896539 (steps=61180, words/sec=6343.89, time=0-03:00:22)
[kftt.en-ja] Epoch 8.8592: train_loss/word=2.893600 (steps=61203, words/sec=6371.41, time=0-03:00:25)
[kftt.en-ja] Epoch 8.8623: train_loss/word=2.809745 (steps=61226, words/sec=6613.14, time=0-03:00:29)
[kftt.en-ja] Epoch 8.8654: train_loss/word=2.872592 (steps=61249, words/sec=6722.56, time=0-03:00:33)
[kftt.en-ja] Epoch 8.8685: train_loss/word=2.913196 (steps=61272, words/sec=6473.46, time=0-03:00:36)
[kftt.en-ja] Epoch 8.8716: train_loss/word=2.915566 (steps=61297, words/sec=6384.33, time=0-03:00:40)
[kftt.en-ja] Epoch 8.8747: train_loss/word=2.953619 (steps=61317, words/sec=6550.15, time=0-03:00:44)
[kftt.en-ja] Epoch 8.8780: train_loss/word=2.898203 (steps=61339, words/sec=6333.13, time=0-03:00:47)
[kftt.en-ja] Epoch 8.8811: train_loss/word=2.877447 (steps=61363, words/sec=6482.40, time=0-03:00:51)
[kftt.en-ja] Epoch 8.8842: train_loss/word=2.892599 (steps=61379, words/sec=6767.39, time=0-03:00:53)
[kftt.en-ja] Epoch 8.8873: train_loss/word=2.849660 (steps=61401, words/sec=6559.84, time=0-03:00:57)
[kftt.en-ja] Epoch 8.8906: train_loss/word=2.882688 (steps=61419, words/sec=6598.61, time=0-03:00:59)
[kftt.en-ja] Epoch 8.8937: train_loss/word=2.890680 (steps=61442, words/sec=6595.54, time=0-03:01:03)
[kftt.en-ja] Epoch 8.8968: train_loss/word=2.918781 (steps=61464, words/sec=6721.37, time=0-03:01:07)
[kftt.en-ja] Epoch 8.8999: train_loss/word=2.893818 (steps=61486, words/sec=6929.66, time=0-03:01:10)
[kftt.en-ja] Epoch 8.9030: train_loss/word=2.894360 (steps=61506, words/sec=6274.98, time=0-03:01:13)
[kftt.en-ja] Epoch 8.9063: train_loss/word=2.861494 (steps=61526, words/sec=6718.67, time=0-03:01:16)
[kftt.en-ja] Epoch 8.9094: train_loss/word=2.980662 (steps=61548, words/sec=6568.39, time=0-03:01:20)
[kftt.en-ja] Epoch 8.9125: train_loss/word=2.879728 (steps=61569, words/sec=6568.41, time=0-03:01:23)
[kftt.en-ja] Epoch 8.9156: train_loss/word=2.948145 (steps=61589, words/sec=6683.77, time=0-03:01:26)
[kftt.en-ja] Epoch 8.9187: train_loss/word=2.888122 (steps=61610, words/sec=6624.32, time=0-03:01:29)
[kftt.en-ja] Epoch 8.9218: train_loss/word=2.874523 (steps=61632, words/sec=6796.12, time=0-03:01:33)
[kftt.en-ja] Epoch 8.9248: train_loss/word=2.917676 (steps=61654, words/sec=6635.87, time=0-03:01:36)
[kftt.en-ja] Epoch 8.9280: train_loss/word=2.876245 (steps=61672, words/sec=6501.66, time=0-03:01:39)
[kftt.en-ja] Epoch 8.9311: train_loss/word=2.891432 (steps=61694, words/sec=6565.00, time=0-03:01:43)
[kftt.en-ja] Epoch 8.9342: train_loss/word=2.915230 (steps=61717, words/sec=6460.58, time=0-03:01:46)
[kftt.en-ja] Epoch 8.9373: train_loss/word=2.908713 (steps=61738, words/sec=6402.54, time=0-03:01:50)
[kftt.en-ja] Epoch 8.9405: train_loss/word=2.885417 (steps=61759, words/sec=6827.84, time=0-03:01:53)
[kftt.en-ja] Epoch 8.9436: train_loss/word=2.862373 (steps=61782, words/sec=6556.13, time=0-03:01:57)
[kftt.en-ja] Epoch 8.9467: train_loss/word=2.922826 (steps=61805, words/sec=6672.55, time=0-03:02:00)
[kftt.en-ja] Epoch 8.9502: train_loss/word=2.925391 (steps=61827, words/sec=6566.17, time=0-03:02:04)
[kftt.en-ja] Epoch 8.9533: train_loss/word=2.947029 (steps=61851, words/sec=6338.91, time=0-03:02:08)
[kftt.en-ja] Epoch 8.9564: train_loss/word=2.895966 (steps=61870, words/sec=6704.95, time=0-03:02:10)
[kftt.en-ja] Epoch 8.9595: train_loss/word=2.843767 (steps=61888, words/sec=6862.96, time=0-03:02:13)
[kftt.en-ja] Epoch 8.9628: train_loss/word=2.875996 (steps=61907, words/sec=6792.77, time=0-03:02:16)
[kftt.en-ja] Epoch 8.9659: train_loss/word=2.886320 (steps=61925, words/sec=7097.61, time=0-03:02:19)
[kftt.en-ja] Epoch 8.9692: train_loss/word=2.885894 (steps=61948, words/sec=6600.42, time=0-03:02:22)
[kftt.en-ja] Epoch 8.9722: train_loss/word=2.869250 (steps=61966, words/sec=6766.76, time=0-03:02:25)
[kftt.en-ja] Epoch 8.9753: train_loss/word=2.933958 (steps=61990, words/sec=6426.17, time=0-03:02:29)
[kftt.en-ja] Epoch 8.9784: train_loss/word=2.894378 (steps=62014, words/sec=6665.81, time=0-03:02:33)
[kftt.en-ja] Epoch 8.9815: train_loss/word=3.041609 (steps=62028, words/sec=7064.53, time=0-03:02:35)
[kftt.en-ja] Epoch 8.9846: train_loss/word=2.912091 (steps=62052, words/sec=6569.95, time=0-03:02:39)
[kftt.en-ja] Epoch 8.9878: train_loss/word=2.858972 (steps=62074, words/sec=6434.14, time=0-03:02:42)
[kftt.en-ja] Epoch 8.9909: train_loss/word=2.946891 (steps=62099, words/sec=6255.13, time=0-03:02:46)
[kftt.en-ja] Epoch 8.9940: train_loss/word=2.858897 (steps=62118, words/sec=6671.72, time=0-03:02:49)
[kftt.en-ja] Epoch 8.9971: train_loss/word=2.872681 (steps=62138, words/sec=6685.92, time=0-03:02:52)
[kftt.en-ja] Epoch 9.0000: train_loss/word=2.891032 (steps=62156, words/sec=6920.78, time=0-03:02:55)
> Checkpoint [kftt.en-ja]
Performing inference on ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja
Starting to read ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja
Done reading ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja. Packing into batches.
Done packing batches.
[kftt.en-ja] Epoch 9.0000 dev BLEU4: 0.20898957356200792, 0.561566/0.300049/0.177164/0.110552 (BP = 0.871949, ratio=0.88, hyp_len=23609, ref_len=26844) (time=0-03:05:01)
[kftt.en-ja]              dev auxiliary Loss: 3.864 (ref_len=26844)
             checkpoint took 0-00:02:06
  new learning rate: 0.25
[kftt.en-ja] Epoch 9.0002: train_loss/word=2.807816 (steps=62157, words/sec=6176.49, time=0-03:05:05)
[kftt.en-ja] Epoch 9.0032: train_loss/word=2.760526 (steps=62182, words/sec=6417.60, time=0-03:05:09)
[kftt.en-ja] Epoch 9.0063: train_loss/word=2.744496 (steps=62201, words/sec=6845.55, time=0-03:05:12)
[kftt.en-ja] Epoch 9.0097: train_loss/word=2.743906 (steps=62225, words/sec=6529.12, time=0-03:05:16)
[kftt.en-ja] Epoch 9.0128: train_loss/word=2.747468 (steps=62250, words/sec=6671.21, time=0-03:05:20)
[kftt.en-ja] Epoch 9.0159: train_loss/word=2.766608 (steps=62275, words/sec=6483.28, time=0-03:05:24)
[kftt.en-ja] Epoch 9.0192: train_loss/word=2.694235 (steps=62297, words/sec=6644.00, time=0-03:05:27)
[kftt.en-ja] Epoch 9.0224: train_loss/word=2.760913 (steps=62320, words/sec=6607.56, time=0-03:05:31)
[kftt.en-ja] Epoch 9.0255: train_loss/word=2.768547 (steps=62341, words/sec=6574.13, time=0-03:05:34)
[kftt.en-ja] Epoch 9.0285: train_loss/word=2.690202 (steps=62360, words/sec=6715.73, time=0-03:05:37)
[kftt.en-ja] Epoch 9.0316: train_loss/word=2.819312 (steps=62378, words/sec=6759.40, time=0-03:05:40)
[kftt.en-ja] Epoch 9.0347: train_loss/word=2.758544 (steps=62397, words/sec=6727.17, time=0-03:05:43)
[kftt.en-ja] Epoch 9.0381: train_loss/word=2.759388 (steps=62417, words/sec=6870.77, time=0-03:05:46)
[kftt.en-ja] Epoch 9.0412: train_loss/word=2.747292 (steps=62442, words/sec=6646.69, time=0-03:05:50)
[kftt.en-ja] Epoch 9.0443: train_loss/word=2.778123 (steps=62462, words/sec=6688.97, time=0-03:05:53)
[kftt.en-ja] Epoch 9.0474: train_loss/word=2.729932 (steps=62479, words/sec=7040.99, time=0-03:05:56)
[kftt.en-ja] Epoch 9.0505: train_loss/word=2.782323 (steps=62504, words/sec=6511.44, time=0-03:06:00)
[kftt.en-ja] Epoch 9.0535: train_loss/word=2.736515 (steps=62524, words/sec=6423.25, time=0-03:06:03)
[kftt.en-ja] Epoch 9.0566: train_loss/word=2.705564 (steps=62545, words/sec=6948.64, time=0-03:06:06)
[kftt.en-ja] Epoch 9.0598: train_loss/word=2.712554 (steps=62564, words/sec=7017.71, time=0-03:06:09)
[kftt.en-ja] Epoch 9.0629: train_loss/word=2.745018 (steps=62584, words/sec=6560.51, time=0-03:06:12)
[kftt.en-ja] Epoch 9.0661: train_loss/word=2.672419 (steps=62599, words/sec=6695.30, time=0-03:06:14)
[kftt.en-ja] Epoch 9.0692: train_loss/word=2.790723 (steps=62622, words/sec=6510.10, time=0-03:06:18)
[kftt.en-ja] Epoch 9.0723: train_loss/word=2.710032 (steps=62644, words/sec=6949.36, time=0-03:06:21)
[kftt.en-ja] Epoch 9.0755: train_loss/word=2.697599 (steps=62663, words/sec=7030.13, time=0-03:06:24)
[kftt.en-ja] Epoch 9.0786: train_loss/word=2.679081 (steps=62681, words/sec=7028.58, time=0-03:06:27)
[kftt.en-ja] Epoch 9.0817: train_loss/word=2.784401 (steps=62702, words/sec=6732.28, time=0-03:06:30)
[kftt.en-ja] Epoch 9.0848: train_loss/word=2.772938 (steps=62725, words/sec=6215.49, time=0-03:06:34)
[kftt.en-ja] Epoch 9.0879: train_loss/word=2.676546 (steps=62745, words/sec=6569.17, time=0-03:06:37)
[kftt.en-ja] Epoch 9.0910: train_loss/word=2.738241 (steps=62764, words/sec=6836.57, time=0-03:06:40)
[kftt.en-ja] Epoch 9.0943: train_loss/word=2.782007 (steps=62787, words/sec=6326.36, time=0-03:06:44)
[kftt.en-ja] Epoch 9.0974: train_loss/word=2.768546 (steps=62813, words/sec=6570.46, time=0-03:06:48)
[kftt.en-ja] Epoch 9.1005: train_loss/word=2.750275 (steps=62835, words/sec=6534.86, time=0-03:06:51)
[kftt.en-ja] Epoch 9.1036: train_loss/word=2.760303 (steps=62857, words/sec=6702.28, time=0-03:06:55)
[kftt.en-ja] Epoch 9.1068: train_loss/word=2.770721 (steps=62877, words/sec=6690.53, time=0-03:06:58)
[kftt.en-ja] Epoch 9.1099: train_loss/word=2.721660 (steps=62901, words/sec=6593.39, time=0-03:07:02)
[kftt.en-ja] Epoch 9.1130: train_loss/word=2.778080 (steps=62921, words/sec=6716.96, time=0-03:07:05)
[kftt.en-ja] Epoch 9.1161: train_loss/word=2.779645 (steps=62939, words/sec=6832.11, time=0-03:07:08)
[kftt.en-ja] Epoch 9.1192: train_loss/word=2.773700 (steps=62964, words/sec=6657.24, time=0-03:07:12)
[kftt.en-ja] Epoch 9.1223: train_loss/word=2.743079 (steps=62986, words/sec=6505.33, time=0-03:07:15)
[kftt.en-ja] Epoch 9.1255: train_loss/word=2.706781 (steps=63009, words/sec=6599.77, time=0-03:07:19)
[kftt.en-ja] Epoch 9.1286: train_loss/word=2.754132 (steps=63031, words/sec=6707.52, time=0-03:07:22)
[kftt.en-ja] Epoch 9.1317: train_loss/word=2.734767 (steps=63051, words/sec=6626.84, time=0-03:07:26)
[kftt.en-ja] Epoch 9.1348: train_loss/word=2.711875 (steps=63071, words/sec=6714.44, time=0-03:07:29)
[kftt.en-ja] Epoch 9.1379: train_loss/word=2.719928 (steps=63091, words/sec=6544.30, time=0-03:07:32)
[kftt.en-ja] Epoch 9.1410: train_loss/word=2.754093 (steps=63114, words/sec=6560.77, time=0-03:07:35)
[kftt.en-ja] Epoch 9.1441: train_loss/word=2.782186 (steps=63134, words/sec=6515.43, time=0-03:07:38)
[kftt.en-ja] Epoch 9.1472: train_loss/word=2.759159 (steps=63157, words/sec=6743.53, time=0-03:07:42)
[kftt.en-ja] Epoch 9.1504: train_loss/word=2.733376 (steps=63179, words/sec=6401.05, time=0-03:07:46)
[kftt.en-ja] Epoch 9.1535: train_loss/word=2.758792 (steps=63201, words/sec=6433.15, time=0-03:07:49)
[kftt.en-ja] Epoch 9.1565: train_loss/word=2.741607 (steps=63226, words/sec=6375.86, time=0-03:07:53)
[kftt.en-ja] Epoch 9.1596: train_loss/word=2.761790 (steps=63250, words/sec=6524.93, time=0-03:07:57)
[kftt.en-ja] Epoch 9.1627: train_loss/word=2.731743 (steps=63274, words/sec=6460.34, time=0-03:08:01)
[kftt.en-ja] Epoch 9.1661: train_loss/word=2.685067 (steps=63294, words/sec=6826.91, time=0-03:08:04)
[kftt.en-ja] Epoch 9.1692: train_loss/word=2.723829 (steps=63316, words/sec=6593.36, time=0-03:08:08)
[kftt.en-ja] Epoch 9.1724: train_loss/word=2.737088 (steps=63339, words/sec=6652.72, time=0-03:08:11)
[kftt.en-ja] Epoch 9.1754: train_loss/word=2.757834 (steps=63358, words/sec=6807.36, time=0-03:08:14)
[kftt.en-ja] Epoch 9.1786: train_loss/word=2.749907 (steps=63382, words/sec=6856.45, time=0-03:08:18)
[kftt.en-ja] Epoch 9.1817: train_loss/word=2.708247 (steps=63401, words/sec=6842.37, time=0-03:08:21)
[kftt.en-ja] Epoch 9.1848: train_loss/word=2.738201 (steps=63423, words/sec=6476.14, time=0-03:08:24)
[kftt.en-ja] Epoch 9.1880: train_loss/word=2.743067 (steps=63444, words/sec=6620.56, time=0-03:08:28)
[kftt.en-ja] Epoch 9.1911: train_loss/word=2.733803 (steps=63466, words/sec=6679.09, time=0-03:08:31)
[kftt.en-ja] Epoch 9.1942: train_loss/word=2.702050 (steps=63489, words/sec=6610.29, time=0-03:08:35)
[kftt.en-ja] Epoch 9.1974: train_loss/word=2.741140 (steps=63511, words/sec=6527.75, time=0-03:08:38)
[kftt.en-ja] Epoch 9.2004: train_loss/word=2.775308 (steps=63529, words/sec=6495.47, time=0-03:08:41)
[kftt.en-ja] Epoch 9.2037: train_loss/word=2.748577 (steps=63556, words/sec=6426.35, time=0-03:08:45)
[kftt.en-ja] Epoch 9.2067: train_loss/word=2.717736 (steps=63579, words/sec=6365.21, time=0-03:08:49)
[kftt.en-ja] Epoch 9.2098: train_loss/word=2.797101 (steps=63602, words/sec=6499.38, time=0-03:08:53)
[kftt.en-ja] Epoch 9.2129: train_loss/word=2.778195 (steps=63622, words/sec=6472.84, time=0-03:08:56)
[kftt.en-ja] Epoch 9.2160: train_loss/word=2.707656 (steps=63644, words/sec=6359.53, time=0-03:09:00)
[kftt.en-ja] Epoch 9.2191: train_loss/word=2.683033 (steps=63666, words/sec=6273.09, time=0-03:09:03)
[kftt.en-ja] Epoch 9.2222: train_loss/word=2.786427 (steps=63691, words/sec=6340.65, time=0-03:09:08)
[kftt.en-ja] Epoch 9.2254: train_loss/word=2.791105 (steps=63713, words/sec=6480.29, time=0-03:09:11)
[kftt.en-ja] Epoch 9.2285: train_loss/word=2.711165 (steps=63735, words/sec=6692.83, time=0-03:09:15)
[kftt.en-ja] Epoch 9.2316: train_loss/word=2.657412 (steps=63756, words/sec=6634.64, time=0-03:09:18)
[kftt.en-ja] Epoch 9.2348: train_loss/word=2.726953 (steps=63777, words/sec=6590.79, time=0-03:09:21)
[kftt.en-ja] Epoch 9.2379: train_loss/word=2.766774 (steps=63799, words/sec=6438.12, time=0-03:09:25)
[kftt.en-ja] Epoch 9.2409: train_loss/word=2.687117 (steps=63819, words/sec=6824.80, time=0-03:09:28)
[kftt.en-ja] Epoch 9.2441: train_loss/word=2.781344 (steps=63843, words/sec=6319.65, time=0-03:09:32)
[kftt.en-ja] Epoch 9.2472: train_loss/word=2.800348 (steps=63859, words/sec=6753.37, time=0-03:09:34)
[kftt.en-ja] Epoch 9.2503: train_loss/word=2.782275 (steps=63880, words/sec=6483.06, time=0-03:09:37)
[kftt.en-ja] Epoch 9.2534: train_loss/word=2.752297 (steps=63901, words/sec=6545.37, time=0-03:09:41)
[kftt.en-ja] Epoch 9.2566: train_loss/word=2.742174 (steps=63921, words/sec=6706.24, time=0-03:09:44)
[kftt.en-ja] Epoch 9.2596: train_loss/word=2.777953 (steps=63938, words/sec=6609.54, time=0-03:09:46)
[kftt.en-ja] Epoch 9.2627: train_loss/word=2.801299 (steps=63958, words/sec=6551.73, time=0-03:09:49)
[kftt.en-ja] Epoch 9.2658: train_loss/word=2.761505 (steps=63980, words/sec=6676.71, time=0-03:09:53)
[kftt.en-ja] Epoch 9.2689: train_loss/word=2.734110 (steps=64000, words/sec=6562.19, time=0-03:09:56)
[kftt.en-ja] Epoch 9.2721: train_loss/word=2.734316 (steps=64020, words/sec=6570.65, time=0-03:09:59)
[kftt.en-ja] Epoch 9.2752: train_loss/word=2.703056 (steps=64039, words/sec=6716.08, time=0-03:10:02)
[kftt.en-ja] Epoch 9.2783: train_loss/word=2.831567 (steps=64060, words/sec=6924.04, time=0-03:10:05)
[kftt.en-ja] Epoch 9.2815: train_loss/word=2.698374 (steps=64083, words/sec=6937.53, time=0-03:10:09)
[kftt.en-ja] Epoch 9.2846: train_loss/word=2.738388 (steps=64104, words/sec=6640.26, time=0-03:10:12)
[kftt.en-ja] Epoch 9.2876: train_loss/word=2.773207 (steps=64125, words/sec=6826.75, time=0-03:10:16)
[kftt.en-ja] Epoch 9.2908: train_loss/word=2.771343 (steps=64149, words/sec=6672.77, time=0-03:10:19)
[kftt.en-ja] Epoch 9.2938: train_loss/word=2.695168 (steps=64170, words/sec=6602.13, time=0-03:10:23)
[kftt.en-ja] Epoch 9.2969: train_loss/word=2.748330 (steps=64186, words/sec=7448.64, time=0-03:10:25)
[kftt.en-ja] Epoch 9.3001: train_loss/word=2.780581 (steps=64202, words/sec=6783.93, time=0-03:10:27)
[kftt.en-ja] Epoch 9.3032: train_loss/word=2.731724 (steps=64221, words/sec=6782.76, time=0-03:10:30)
[kftt.en-ja] Epoch 9.3063: train_loss/word=2.745201 (steps=64241, words/sec=6308.28, time=0-03:10:33)
[kftt.en-ja] Epoch 9.3095: train_loss/word=2.774157 (steps=64266, words/sec=6524.09, time=0-03:10:37)
[kftt.en-ja] Epoch 9.3127: train_loss/word=2.695520 (steps=64289, words/sec=6393.27, time=0-03:10:41)
[kftt.en-ja] Epoch 9.3161: train_loss/word=2.776366 (steps=64311, words/sec=6564.78, time=0-03:10:45)
[kftt.en-ja] Epoch 9.3192: train_loss/word=2.783591 (steps=64335, words/sec=6516.77, time=0-03:10:49)
[kftt.en-ja] Epoch 9.3222: train_loss/word=2.781741 (steps=64357, words/sec=6390.64, time=0-03:10:52)
[kftt.en-ja] Epoch 9.3253: train_loss/word=2.759210 (steps=64379, words/sec=6279.13, time=0-03:10:56)
[kftt.en-ja] Epoch 9.3285: train_loss/word=2.760501 (steps=64404, words/sec=6499.66, time=0-03:11:00)
[kftt.en-ja] Epoch 9.3317: train_loss/word=2.729051 (steps=64427, words/sec=6353.91, time=0-03:11:04)
[kftt.en-ja] Epoch 9.3348: train_loss/word=2.760711 (steps=64449, words/sec=6352.35, time=0-03:11:07)
[kftt.en-ja] Epoch 9.3379: train_loss/word=2.793856 (steps=64472, words/sec=6338.76, time=0-03:11:11)
[kftt.en-ja] Epoch 9.3410: train_loss/word=2.711589 (steps=64495, words/sec=6632.29, time=0-03:11:15)
[kftt.en-ja] Epoch 9.3440: train_loss/word=2.776050 (steps=64518, words/sec=6716.84, time=0-03:11:18)
[kftt.en-ja] Epoch 9.3473: train_loss/word=2.765984 (steps=64542, words/sec=6532.66, time=0-03:11:22)
[kftt.en-ja] Epoch 9.3503: train_loss/word=2.804812 (steps=64562, words/sec=6871.35, time=0-03:11:25)
[kftt.en-ja] Epoch 9.3534: train_loss/word=2.759752 (steps=64588, words/sec=6488.43, time=0-03:11:30)
[kftt.en-ja] Epoch 9.3564: train_loss/word=2.774302 (steps=64612, words/sec=6595.85, time=0-03:11:34)
[kftt.en-ja] Epoch 9.3596: train_loss/word=2.768695 (steps=64634, words/sec=6647.14, time=0-03:11:37)
[kftt.en-ja] Epoch 9.3627: train_loss/word=2.784934 (steps=64660, words/sec=6576.26, time=0-03:11:42)
[kftt.en-ja] Epoch 9.3657: train_loss/word=2.739412 (steps=64680, words/sec=6841.46, time=0-03:11:45)
[kftt.en-ja] Epoch 9.3688: train_loss/word=2.726746 (steps=64703, words/sec=6682.54, time=0-03:11:48)
[kftt.en-ja] Epoch 9.3720: train_loss/word=2.801617 (steps=64722, words/sec=6702.74, time=0-03:11:51)
[kftt.en-ja] Epoch 9.3751: train_loss/word=2.724856 (steps=64742, words/sec=6804.51, time=0-03:11:54)
[kftt.en-ja] Epoch 9.3781: train_loss/word=2.769030 (steps=64765, words/sec=6282.61, time=0-03:11:58)
[kftt.en-ja] Epoch 9.3812: train_loss/word=2.723162 (steps=64787, words/sec=6460.13, time=0-03:12:02)
[kftt.en-ja] Epoch 9.3842: train_loss/word=2.762905 (steps=64807, words/sec=6534.17, time=0-03:12:05)
[kftt.en-ja] Epoch 9.3874: train_loss/word=2.730017 (steps=64829, words/sec=6654.39, time=0-03:12:08)
[kftt.en-ja] Epoch 9.3905: train_loss/word=2.790941 (steps=64853, words/sec=6414.18, time=0-03:12:12)
[kftt.en-ja] Epoch 9.3937: train_loss/word=2.660407 (steps=64873, words/sec=6360.10, time=0-03:12:15)
[kftt.en-ja] Epoch 9.3968: train_loss/word=2.738219 (steps=64895, words/sec=6487.92, time=0-03:12:19)
[kftt.en-ja] Epoch 9.3998: train_loss/word=2.761760 (steps=64919, words/sec=6426.06, time=0-03:12:23)
[kftt.en-ja] Epoch 9.4030: train_loss/word=2.796515 (steps=64941, words/sec=6383.70, time=0-03:12:26)
[kftt.en-ja] Epoch 9.4060: train_loss/word=2.790799 (steps=64965, words/sec=6318.76, time=0-03:12:30)
[kftt.en-ja] Epoch 9.4091: train_loss/word=2.778885 (steps=64984, words/sec=6598.22, time=0-03:12:33)
[kftt.en-ja] Epoch 9.4122: train_loss/word=2.809260 (steps=65007, words/sec=6407.05, time=0-03:12:37)
[kftt.en-ja] Epoch 9.4153: train_loss/word=2.753890 (steps=65030, words/sec=6466.27, time=0-03:12:41)
[kftt.en-ja] Epoch 9.4184: train_loss/word=2.748124 (steps=65052, words/sec=6424.52, time=0-03:12:44)
[kftt.en-ja] Epoch 9.4215: train_loss/word=2.743308 (steps=65073, words/sec=6654.05, time=0-03:12:48)
[kftt.en-ja] Epoch 9.4246: train_loss/word=2.733227 (steps=65094, words/sec=6416.25, time=0-03:12:51)
[kftt.en-ja] Epoch 9.4276: train_loss/word=2.737237 (steps=65117, words/sec=6498.38, time=0-03:12:55)
[kftt.en-ja] Epoch 9.4311: train_loss/word=2.766489 (steps=65138, words/sec=6753.70, time=0-03:12:58)
[kftt.en-ja] Epoch 9.4341: train_loss/word=2.780008 (steps=65160, words/sec=6416.53, time=0-03:13:02)
[kftt.en-ja] Epoch 9.4373: train_loss/word=2.762560 (steps=65184, words/sec=6595.94, time=0-03:13:05)
[kftt.en-ja] Epoch 9.4404: train_loss/word=2.738606 (steps=65205, words/sec=6777.45, time=0-03:13:09)
[kftt.en-ja] Epoch 9.4435: train_loss/word=2.720755 (steps=65226, words/sec=6621.43, time=0-03:13:12)
[kftt.en-ja] Epoch 9.4465: train_loss/word=2.759479 (steps=65248, words/sec=6699.58, time=0-03:13:15)
[kftt.en-ja] Epoch 9.4497: train_loss/word=2.711243 (steps=65269, words/sec=6453.73, time=0-03:13:19)
[kftt.en-ja] Epoch 9.4529: train_loss/word=2.772245 (steps=65289, words/sec=6569.12, time=0-03:13:22)
[kftt.en-ja] Epoch 9.4563: train_loss/word=2.777266 (steps=65310, words/sec=6230.43, time=0-03:13:25)
[kftt.en-ja] Epoch 9.4594: train_loss/word=2.802437 (steps=65332, words/sec=6413.56, time=0-03:13:29)
[kftt.en-ja] Epoch 9.4625: train_loss/word=2.749416 (steps=65353, words/sec=6460.45, time=0-03:13:32)
[kftt.en-ja] Epoch 9.4656: train_loss/word=2.731556 (steps=65372, words/sec=6630.62, time=0-03:13:35)
[kftt.en-ja] Epoch 9.4687: train_loss/word=2.708048 (steps=65391, words/sec=6833.53, time=0-03:13:38)
[kftt.en-ja] Epoch 9.4717: train_loss/word=2.751325 (steps=65413, words/sec=6560.56, time=0-03:13:41)
[kftt.en-ja] Epoch 9.4748: train_loss/word=2.755931 (steps=65433, words/sec=6345.11, time=0-03:13:44)
[kftt.en-ja] Epoch 9.4779: train_loss/word=2.792278 (steps=65457, words/sec=6637.76, time=0-03:13:48)
[kftt.en-ja] Epoch 9.4810: train_loss/word=2.784004 (steps=65476, words/sec=6479.93, time=0-03:13:51)
[kftt.en-ja] Epoch 9.4842: train_loss/word=2.707911 (steps=65498, words/sec=6523.55, time=0-03:13:55)
[kftt.en-ja] Epoch 9.4872: train_loss/word=2.733226 (steps=65518, words/sec=6425.59, time=0-03:13:58)
[kftt.en-ja] Epoch 9.4904: train_loss/word=2.725941 (steps=65541, words/sec=6459.22, time=0-03:14:02)
[kftt.en-ja] Epoch 9.4935: train_loss/word=2.750370 (steps=65562, words/sec=6591.10, time=0-03:14:05)
[kftt.en-ja] Epoch 9.4966: train_loss/word=2.729028 (steps=65581, words/sec=6735.59, time=0-03:14:08)
[kftt.en-ja] Epoch 9.4997: train_loss/word=2.769715 (steps=65606, words/sec=6297.09, time=0-03:14:12)
[kftt.en-ja] Epoch 9.5027: train_loss/word=2.814581 (steps=65627, words/sec=6614.58, time=0-03:14:15)
[kftt.en-ja] Epoch 9.5063: train_loss/word=2.784460 (steps=65646, words/sec=6580.54, time=0-03:14:18)
[kftt.en-ja] Epoch 9.5094: train_loss/word=2.800551 (steps=65670, words/sec=6367.94, time=0-03:14:22)
[kftt.en-ja] Epoch 9.5125: train_loss/word=2.838108 (steps=65688, words/sec=6516.57, time=0-03:14:25)
[kftt.en-ja] Epoch 9.5156: train_loss/word=2.735338 (steps=65710, words/sec=6726.09, time=0-03:14:28)
[kftt.en-ja] Epoch 9.5187: train_loss/word=2.691001 (steps=65727, words/sec=6788.78, time=0-03:14:31)
[kftt.en-ja] Epoch 9.5218: train_loss/word=2.780180 (steps=65746, words/sec=6715.75, time=0-03:14:34)
[kftt.en-ja] Epoch 9.5250: train_loss/word=2.748890 (steps=65768, words/sec=6485.98, time=0-03:14:37)
[kftt.en-ja] Epoch 9.5281: train_loss/word=2.731640 (steps=65792, words/sec=6317.52, time=0-03:14:41)
[kftt.en-ja] Epoch 9.5313: train_loss/word=2.724897 (steps=65812, words/sec=6887.31, time=0-03:14:44)
[kftt.en-ja] Epoch 9.5344: train_loss/word=2.766300 (steps=65836, words/sec=6572.13, time=0-03:14:48)
[kftt.en-ja] Epoch 9.5375: train_loss/word=2.746457 (steps=65858, words/sec=6677.77, time=0-03:14:51)
[kftt.en-ja] Epoch 9.5406: train_loss/word=2.758414 (steps=65882, words/sec=6484.00, time=0-03:14:55)
[kftt.en-ja] Epoch 9.5437: train_loss/word=2.706631 (steps=65898, words/sec=6958.85, time=0-03:14:58)
[kftt.en-ja] Epoch 9.5469: train_loss/word=2.765777 (steps=65921, words/sec=6550.07, time=0-03:15:01)
[kftt.en-ja] Epoch 9.5499: train_loss/word=2.731632 (steps=65937, words/sec=6705.00, time=0-03:15:04)
[kftt.en-ja] Epoch 9.5531: train_loss/word=2.701108 (steps=65957, words/sec=6845.94, time=0-03:15:07)
[kftt.en-ja] Epoch 9.5562: train_loss/word=2.819564 (steps=65983, words/sec=6370.85, time=0-03:15:11)
[kftt.en-ja] Epoch 9.5593: train_loss/word=2.794873 (steps=66006, words/sec=6642.46, time=0-03:15:15)
[kftt.en-ja] Epoch 9.5624: train_loss/word=2.671140 (steps=66026, words/sec=6846.52, time=0-03:15:18)
[kftt.en-ja] Epoch 9.5655: train_loss/word=2.760952 (steps=66045, words/sec=6670.56, time=0-03:15:21)
[kftt.en-ja] Epoch 9.5687: train_loss/word=2.734807 (steps=66064, words/sec=6826.90, time=0-03:15:24)
[kftt.en-ja] Epoch 9.5717: train_loss/word=2.751447 (steps=66086, words/sec=6658.06, time=0-03:15:27)
[kftt.en-ja] Epoch 9.5748: train_loss/word=2.730490 (steps=66105, words/sec=6778.42, time=0-03:15:30)
[kftt.en-ja] Epoch 9.5781: train_loss/word=2.773275 (steps=66129, words/sec=6449.18, time=0-03:15:34)
[kftt.en-ja] Epoch 9.5812: train_loss/word=2.752310 (steps=66153, words/sec=6568.98, time=0-03:15:38)
[kftt.en-ja] Epoch 9.5844: train_loss/word=2.753338 (steps=66177, words/sec=6718.05, time=0-03:15:42)
[kftt.en-ja] Epoch 9.5877: train_loss/word=2.750399 (steps=66197, words/sec=6519.30, time=0-03:15:45)
[kftt.en-ja] Epoch 9.5908: train_loss/word=2.821394 (steps=66220, words/sec=6353.43, time=0-03:15:48)
[kftt.en-ja] Epoch 9.5940: train_loss/word=2.747917 (steps=66235, words/sec=6763.11, time=0-03:15:51)
[kftt.en-ja] Epoch 9.5972: train_loss/word=2.795287 (steps=66253, words/sec=6711.62, time=0-03:15:53)
[kftt.en-ja] Epoch 9.6003: train_loss/word=2.773651 (steps=66278, words/sec=6602.73, time=0-03:15:57)
[kftt.en-ja] Epoch 9.6033: train_loss/word=2.744516 (steps=66299, words/sec=6784.37, time=0-03:16:01)
[kftt.en-ja] Epoch 9.6065: train_loss/word=2.763205 (steps=66325, words/sec=6345.26, time=0-03:16:05)
[kftt.en-ja] Epoch 9.6095: train_loss/word=2.785365 (steps=66350, words/sec=6316.19, time=0-03:16:09)
[kftt.en-ja] Epoch 9.6126: train_loss/word=2.757824 (steps=66372, words/sec=6632.05, time=0-03:16:13)
[kftt.en-ja] Epoch 9.6158: train_loss/word=2.785830 (steps=66399, words/sec=6447.38, time=0-03:16:17)
[kftt.en-ja] Epoch 9.6188: train_loss/word=2.791561 (steps=66424, words/sec=6437.19, time=0-03:16:21)
[kftt.en-ja] Epoch 9.6219: train_loss/word=2.752905 (steps=66447, words/sec=6701.34, time=0-03:16:25)
[kftt.en-ja] Epoch 9.6249: train_loss/word=2.766218 (steps=66468, words/sec=6529.35, time=0-03:16:28)
[kftt.en-ja] Epoch 9.6280: train_loss/word=2.803765 (steps=66492, words/sec=6414.17, time=0-03:16:32)
[kftt.en-ja] Epoch 9.6312: train_loss/word=2.807906 (steps=66518, words/sec=6306.33, time=0-03:16:37)
[kftt.en-ja] Epoch 9.6342: train_loss/word=2.778564 (steps=66538, words/sec=6583.81, time=0-03:16:40)
[kftt.en-ja] Epoch 9.6379: train_loss/word=2.802812 (steps=66562, words/sec=6687.86, time=0-03:16:44)
[kftt.en-ja] Epoch 9.6411: train_loss/word=2.804927 (steps=66585, words/sec=6468.35, time=0-03:16:48)
[kftt.en-ja] Epoch 9.6441: train_loss/word=2.757077 (steps=66602, words/sec=6964.11, time=0-03:16:50)
[kftt.en-ja] Epoch 9.6472: train_loss/word=2.749073 (steps=66624, words/sec=6564.82, time=0-03:16:54)
[kftt.en-ja] Epoch 9.6503: train_loss/word=2.801257 (steps=66644, words/sec=6679.47, time=0-03:16:57)
[kftt.en-ja] Epoch 9.6534: train_loss/word=2.742632 (steps=66668, words/sec=6481.52, time=0-03:17:01)
[kftt.en-ja] Epoch 9.6565: train_loss/word=2.731504 (steps=66692, words/sec=6544.56, time=0-03:17:04)
[kftt.en-ja] Epoch 9.6597: train_loss/word=2.765915 (steps=66715, words/sec=6481.96, time=0-03:17:08)
[kftt.en-ja] Epoch 9.6628: train_loss/word=2.776360 (steps=66736, words/sec=6659.15, time=0-03:17:11)
[kftt.en-ja] Epoch 9.6659: train_loss/word=2.747509 (steps=66759, words/sec=6369.20, time=0-03:17:15)
[kftt.en-ja] Epoch 9.6691: train_loss/word=2.686977 (steps=66777, words/sec=6982.58, time=0-03:17:18)
[kftt.en-ja] Epoch 9.6721: train_loss/word=2.728634 (steps=66799, words/sec=6516.67, time=0-03:17:21)
[kftt.en-ja] Epoch 9.6752: train_loss/word=2.781672 (steps=66821, words/sec=6767.76, time=0-03:17:25)
[kftt.en-ja] Epoch 9.6782: train_loss/word=2.761141 (steps=66845, words/sec=6476.53, time=0-03:17:29)
[kftt.en-ja] Epoch 9.6814: train_loss/word=2.622740 (steps=66863, words/sec=6859.32, time=0-03:17:31)
[kftt.en-ja] Epoch 9.6846: train_loss/word=2.760580 (steps=66884, words/sec=6789.86, time=0-03:17:34)
[kftt.en-ja] Epoch 9.6877: train_loss/word=2.832786 (steps=66902, words/sec=6804.49, time=0-03:17:37)
[kftt.en-ja] Epoch 9.6908: train_loss/word=2.758335 (steps=66926, words/sec=6502.00, time=0-03:17:41)
[kftt.en-ja] Epoch 9.6938: train_loss/word=2.820810 (steps=66946, words/sec=6601.24, time=0-03:17:44)
[kftt.en-ja] Epoch 9.6969: train_loss/word=2.789336 (steps=66965, words/sec=6463.25, time=0-03:17:47)
[kftt.en-ja] Epoch 9.7000: train_loss/word=2.744581 (steps=66989, words/sec=6550.45, time=0-03:17:51)
[kftt.en-ja] Epoch 9.7030: train_loss/word=2.835230 (steps=67014, words/sec=6407.00, time=0-03:17:55)
[kftt.en-ja] Epoch 9.7062: train_loss/word=2.752686 (steps=67038, words/sec=6509.86, time=0-03:17:59)
[kftt.en-ja] Epoch 9.7093: train_loss/word=2.741064 (steps=67060, words/sec=6468.68, time=0-03:18:03)
[kftt.en-ja] Epoch 9.7125: train_loss/word=2.770665 (steps=67080, words/sec=6589.55, time=0-03:18:06)
[kftt.en-ja] Epoch 9.7155: train_loss/word=2.803441 (steps=67104, words/sec=6547.59, time=0-03:18:10)
[kftt.en-ja] Epoch 9.7187: train_loss/word=2.752675 (steps=67128, words/sec=6593.80, time=0-03:18:13)
[kftt.en-ja] Epoch 9.7218: train_loss/word=2.728476 (steps=67148, words/sec=6666.08, time=0-03:18:17)
[kftt.en-ja] Epoch 9.7249: train_loss/word=2.745394 (steps=67174, words/sec=6541.53, time=0-03:18:21)
[kftt.en-ja] Epoch 9.7282: train_loss/word=2.808136 (steps=67193, words/sec=6823.82, time=0-03:18:24)
[kftt.en-ja] Epoch 9.7313: train_loss/word=2.787531 (steps=67213, words/sec=6593.68, time=0-03:18:27)
[kftt.en-ja] Epoch 9.7346: train_loss/word=2.739683 (steps=67237, words/sec=6561.03, time=0-03:18:31)
[kftt.en-ja] Epoch 9.7377: train_loss/word=2.774287 (steps=67262, words/sec=6410.16, time=0-03:18:35)
[kftt.en-ja] Epoch 9.7408: train_loss/word=2.732180 (steps=67282, words/sec=6729.33, time=0-03:18:38)
[kftt.en-ja] Epoch 9.7439: train_loss/word=2.781989 (steps=67303, words/sec=6408.50, time=0-03:18:41)
[kftt.en-ja] Epoch 9.7469: train_loss/word=2.820710 (steps=67323, words/sec=6345.75, time=0-03:18:44)
[kftt.en-ja] Epoch 9.7500: train_loss/word=2.722644 (steps=67346, words/sec=6561.52, time=0-03:18:48)
[kftt.en-ja] Epoch 9.7532: train_loss/word=2.764452 (steps=67366, words/sec=6617.66, time=0-03:18:51)
[kftt.en-ja] Epoch 9.7565: train_loss/word=2.812356 (steps=67385, words/sec=6679.87, time=0-03:18:54)
[kftt.en-ja] Epoch 9.7596: train_loss/word=2.800676 (steps=67406, words/sec=6366.87, time=0-03:18:57)
[kftt.en-ja] Epoch 9.7627: train_loss/word=2.791382 (steps=67431, words/sec=6322.00, time=0-03:19:02)
[kftt.en-ja] Epoch 9.7659: train_loss/word=2.755338 (steps=67449, words/sec=6803.63, time=0-03:19:04)
[kftt.en-ja] Epoch 9.7691: train_loss/word=2.794416 (steps=67470, words/sec=6463.85, time=0-03:19:08)
[kftt.en-ja] Epoch 9.7723: train_loss/word=2.764144 (steps=67493, words/sec=6515.39, time=0-03:19:11)
[kftt.en-ja] Epoch 9.7754: train_loss/word=2.743790 (steps=67515, words/sec=6527.95, time=0-03:19:15)
[kftt.en-ja] Epoch 9.7786: train_loss/word=2.792361 (steps=67536, words/sec=6622.26, time=0-03:19:18)
[kftt.en-ja] Epoch 9.7816: train_loss/word=2.757331 (steps=67555, words/sec=6725.21, time=0-03:19:21)
[kftt.en-ja] Epoch 9.7847: train_loss/word=2.722901 (steps=67574, words/sec=6816.06, time=0-03:19:24)
[kftt.en-ja] Epoch 9.7878: train_loss/word=2.785472 (steps=67598, words/sec=6437.42, time=0-03:19:28)
[kftt.en-ja] Epoch 9.7908: train_loss/word=2.852131 (steps=67621, words/sec=6541.57, time=0-03:19:31)
[kftt.en-ja] Epoch 9.7939: train_loss/word=2.784420 (steps=67646, words/sec=6365.67, time=0-03:19:36)
[kftt.en-ja] Epoch 9.7969: train_loss/word=2.739223 (steps=67667, words/sec=6684.26, time=0-03:19:39)
[kftt.en-ja] Epoch 9.8000: train_loss/word=2.772309 (steps=67689, words/sec=6570.31, time=0-03:19:42)
[kftt.en-ja] Epoch 9.8031: train_loss/word=2.728653 (steps=67709, words/sec=6729.66, time=0-03:19:45)
[kftt.en-ja] Epoch 9.8062: train_loss/word=2.772584 (steps=67732, words/sec=6604.02, time=0-03:19:49)
[kftt.en-ja] Epoch 9.8093: train_loss/word=2.825411 (steps=67755, words/sec=6508.32, time=0-03:19:53)
[kftt.en-ja] Epoch 9.8124: train_loss/word=2.699628 (steps=67777, words/sec=6605.63, time=0-03:19:57)
[kftt.en-ja] Epoch 9.8156: train_loss/word=2.798103 (steps=67801, words/sec=6716.58, time=0-03:20:00)
[kftt.en-ja] Epoch 9.8188: train_loss/word=2.740291 (steps=67822, words/sec=6824.06, time=0-03:20:04)
[kftt.en-ja] Epoch 9.8220: train_loss/word=2.729131 (steps=67844, words/sec=6791.06, time=0-03:20:07)
[kftt.en-ja] Epoch 9.8250: train_loss/word=2.749048 (steps=67868, words/sec=6463.48, time=0-03:20:11)
[kftt.en-ja] Epoch 9.8281: train_loss/word=2.793230 (steps=67891, words/sec=6787.64, time=0-03:20:15)
[kftt.en-ja] Epoch 9.8312: train_loss/word=2.762647 (steps=67914, words/sec=6557.42, time=0-03:20:18)
[kftt.en-ja] Epoch 9.8343: train_loss/word=2.825238 (steps=67936, words/sec=6507.31, time=0-03:20:22)
[kftt.en-ja] Epoch 9.8374: train_loss/word=2.781372 (steps=67956, words/sec=6798.22, time=0-03:20:25)
[kftt.en-ja] Epoch 9.8406: train_loss/word=2.755678 (steps=67979, words/sec=6680.90, time=0-03:20:29)
[kftt.en-ja] Epoch 9.8437: train_loss/word=2.795257 (steps=68003, words/sec=6491.21, time=0-03:20:33)
[kftt.en-ja] Epoch 9.8467: train_loss/word=2.695406 (steps=68024, words/sec=6928.50, time=0-03:20:36)
[kftt.en-ja] Epoch 9.8501: train_loss/word=2.822585 (steps=68042, words/sec=6886.95, time=0-03:20:39)
[kftt.en-ja] Epoch 9.8531: train_loss/word=2.773858 (steps=68065, words/sec=6823.32, time=0-03:20:42)
[kftt.en-ja] Epoch 9.8563: train_loss/word=2.753120 (steps=68086, words/sec=6720.57, time=0-03:20:46)
[kftt.en-ja] Epoch 9.8594: train_loss/word=2.781702 (steps=68111, words/sec=6504.77, time=0-03:20:50)
[kftt.en-ja] Epoch 9.8625: train_loss/word=2.772309 (steps=68130, words/sec=6791.55, time=0-03:20:53)
[kftt.en-ja] Epoch 9.8656: train_loss/word=2.726567 (steps=68152, words/sec=6730.61, time=0-03:20:56)
[kftt.en-ja] Epoch 9.8687: train_loss/word=2.778198 (steps=68175, words/sec=6810.70, time=0-03:21:00)
[kftt.en-ja] Epoch 9.8718: train_loss/word=2.746900 (steps=68199, words/sec=6764.64, time=0-03:21:04)
[kftt.en-ja] Epoch 9.8748: train_loss/word=2.771287 (steps=68222, words/sec=6733.65, time=0-03:21:07)
[kftt.en-ja] Epoch 9.8780: train_loss/word=2.720405 (steps=68242, words/sec=6881.20, time=0-03:21:10)
[kftt.en-ja] Epoch 9.8810: train_loss/word=2.835888 (steps=68261, words/sec=6650.92, time=0-03:21:13)
[kftt.en-ja] Epoch 9.8841: train_loss/word=2.793611 (steps=68277, words/sec=6791.05, time=0-03:21:16)
[kftt.en-ja] Epoch 9.8872: train_loss/word=2.755423 (steps=68298, words/sec=6781.04, time=0-03:21:19)
[kftt.en-ja] Epoch 9.8904: train_loss/word=2.763471 (steps=68320, words/sec=6778.64, time=0-03:21:22)
[kftt.en-ja] Epoch 9.8935: train_loss/word=2.791587 (steps=68344, words/sec=6538.66, time=0-03:21:26)
[kftt.en-ja] Epoch 9.8965: train_loss/word=2.772682 (steps=68366, words/sec=6876.28, time=0-03:21:30)
[kftt.en-ja] Epoch 9.8997: train_loss/word=2.715620 (steps=68389, words/sec=6717.22, time=0-03:21:33)
[kftt.en-ja] Epoch 9.9027: train_loss/word=2.821078 (steps=68409, words/sec=6585.16, time=0-03:21:36)
[kftt.en-ja] Epoch 9.9058: train_loss/word=2.719626 (steps=68427, words/sec=7061.79, time=0-03:21:39)
[kftt.en-ja] Epoch 9.9089: train_loss/word=2.734602 (steps=68448, words/sec=6866.73, time=0-03:21:42)
[kftt.en-ja] Epoch 9.9120: train_loss/word=2.771043 (steps=68470, words/sec=6890.48, time=0-03:21:46)
[kftt.en-ja] Epoch 9.9151: train_loss/word=2.796050 (steps=68489, words/sec=6675.16, time=0-03:21:49)
[kftt.en-ja] Epoch 9.9182: train_loss/word=2.776901 (steps=68509, words/sec=6723.08, time=0-03:21:52)
[kftt.en-ja] Epoch 9.9213: train_loss/word=2.742764 (steps=68530, words/sec=6716.17, time=0-03:21:55)
[kftt.en-ja] Epoch 9.9244: train_loss/word=2.770930 (steps=68550, words/sec=6672.88, time=0-03:21:58)
[kftt.en-ja] Epoch 9.9276: train_loss/word=2.729756 (steps=68568, words/sec=6658.99, time=0-03:22:01)
[kftt.en-ja] Epoch 9.9312: train_loss/word=2.752195 (steps=68589, words/sec=6694.87, time=0-03:22:04)
[kftt.en-ja] Epoch 9.9345: train_loss/word=2.768579 (steps=68610, words/sec=6672.93, time=0-03:22:07)
[kftt.en-ja] Epoch 9.9376: train_loss/word=2.728319 (steps=68632, words/sec=6603.62, time=0-03:22:10)
[kftt.en-ja] Epoch 9.9407: train_loss/word=2.789969 (steps=68651, words/sec=6477.69, time=0-03:22:13)
[kftt.en-ja] Epoch 9.9438: train_loss/word=2.814544 (steps=68672, words/sec=6626.84, time=0-03:22:17)
[kftt.en-ja] Epoch 9.9469: train_loss/word=2.762091 (steps=68693, words/sec=6620.15, time=0-03:22:20)
[kftt.en-ja] Epoch 9.9500: train_loss/word=2.864625 (steps=68713, words/sec=6396.93, time=0-03:22:23)
[kftt.en-ja] Epoch 9.9532: train_loss/word=2.757559 (steps=68736, words/sec=6570.41, time=0-03:22:27)
[kftt.en-ja] Epoch 9.9563: train_loss/word=2.816792 (steps=68761, words/sec=6496.23, time=0-03:22:31)
[kftt.en-ja] Epoch 9.9594: train_loss/word=2.741811 (steps=68785, words/sec=6750.62, time=0-03:22:35)
[kftt.en-ja] Epoch 9.9625: train_loss/word=2.811772 (steps=68810, words/sec=6474.31, time=0-03:22:39)
[kftt.en-ja] Epoch 9.9655: train_loss/word=2.770039 (steps=68830, words/sec=6315.32, time=0-03:22:42)
[kftt.en-ja] Epoch 9.9687: train_loss/word=2.807421 (steps=68851, words/sec=6757.73, time=0-03:22:46)
[kftt.en-ja] Epoch 9.9718: train_loss/word=2.765241 (steps=68871, words/sec=6820.72, time=0-03:22:49)
[kftt.en-ja] Epoch 9.9750: train_loss/word=2.741100 (steps=68892, words/sec=6913.81, time=0-03:22:52)
[kftt.en-ja] Epoch 9.9782: train_loss/word=2.806860 (steps=68913, words/sec=6517.50, time=0-03:22:55)
[kftt.en-ja] Epoch 9.9812: train_loss/word=2.747080 (steps=68933, words/sec=5813.60, time=0-03:22:59)
[kftt.en-ja] Epoch 9.9844: train_loss/word=2.802435 (steps=68958, words/sec=6435.97, time=0-03:23:03)
[kftt.en-ja] Epoch 9.9874: train_loss/word=2.771759 (steps=68980, words/sec=6453.00, time=0-03:23:06)
[kftt.en-ja] Epoch 9.9905: train_loss/word=2.730278 (steps=69002, words/sec=6604.13, time=0-03:23:10)
[kftt.en-ja] Epoch 9.9937: train_loss/word=2.835580 (steps=69023, words/sec=6534.83, time=0-03:23:13)
[kftt.en-ja] Epoch 9.9968: train_loss/word=2.774051 (steps=69046, words/sec=6864.50, time=0-03:23:17)
[kftt.en-ja] Epoch 9.9998: train_loss/word=2.809498 (steps=69063, words/sec=6419.20, time=0-03:23:19)
[kftt.en-ja] Epoch 10.0000: train_loss/word=2.704749 (steps=69064, words/sec=7623.10, time=0-03:23:19)
> Checkpoint [kftt.en-ja]
Performing inference on ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja
Starting to read ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja
Done reading ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja. Packing into batches.
Done packing batches.
[kftt.en-ja] Epoch 10.0000 dev BLEU4: 0.20848327451379126, 0.552713/0.292985/0.170452/0.104554 (BP = 0.899496, ratio=0.90, hyp_len=24273, ref_len=26844) (time=0-03:25:27)
[kftt.en-ja]              dev auxiliary Loss: 3.876 (ref_len=26844)
             checkpoint took 0-00:02:07
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./kftt-data-1.0/data/tok/kyoto-dev.en and ./kftt-data-1.0/data/tok/kyoto-dev.ja
Performing inference on ./kftt-data-1.0/data/tok/kyoto-test.en and ./kftt-data-1.0/data/tok/kyoto-test.ja
Experiment                    | Final Scores
-----------------------------------------------------------------------
kftt.en-ja                    | BLEU4: 0.20977575129707296, 0.560763/0.301096/0.177240/0.109862 (BP = 0.876057, ratio=0.88, hyp_len=23707, ref_len=26844)
                              | BLEU4: 0.23446049110262004, 0.580502/0.324791/0.202485/0.136095 (BP = 0.873291, ratio=0.88, hyp_len=25080, ref_len=28478)

real	210m27.913s
user	194m34.178s
sys	15m57.014s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$
```

config ဖိုင်မှာ task အနေနဲ့ testing ကို ထည့်ထားရင် testing လည်း လုပ်ပေးတယ်။  

## Check the model and outputs

model folder အောက်မှာက...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ tree ./models/
./models/
├── kftt.en-ja.mod
└── kftt.en-ja.mod.data
    ├── AuxNonLinear-5436935f
    ├── DenseWordEmbedder-35e672da
    ├── Linear-da953d1c
    ├── MlpAttender-fb815d33
    ├── SimpleWordEmbedder-56af3728
    ├── UniLSTMSeqTransducer-4dd4e810
    ├── UniLSTMSeqTransducer-5dec2edd
    ├── UniLSTMSeqTransducer-7f83663d
    ├── UniLSTMSeqTransducer-82ff1a73
    └── UniLSTMSeqTransducer-85c06e6e

1 directory, 11 files
```

model ရဲ့ size က ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/models$ ls -lh kftt.en-ja.mod
-rw-rw-r-- 1 ye ye 1.6M May  1 17:16 kftt.en-ja.mod
```

log folder အောက်မှာက...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ tree ./logs/
./logs/
├── kftt.en-ja.log
└── kftt.en-ja.log.yaml

0 directories, 2 files
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$
```

## Check Model File

တစ်ခု ကောင်းတာက မော်ဒယ်ဖိုင်ကိုလည်း text format မို့လို့ လေ့လာဖို့ လွယ်ကူတယ်။  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/models$ head -n 500 ./kftt.en-ja.mod
!Experiment
evaluate:
- !AccuracyEvalTask
  desc: null
  eval_metrics: bleu
  hyp_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/hyp/{EXP}.dev.ja'
    value: ./hyp/kftt.en-ja.dev.ja
  inference: null
  model: !Ref
    default: 1928437192847
    name: null
    path: model
  perform_inference: true
  ref_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.ja'
    value: ./kftt-data-1.0/data/tok/kyoto-dev.ja
  src_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.en'
    value: ./kftt-data-1.0/data/tok/kyoto-dev.en
- !AccuracyEvalTask
  desc: null
  eval_metrics: bleu
  hyp_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/hyp/{EXP}.test.ja'
    value: ./hyp/kftt.en-ja.test.ja
  inference: null
  model: !Ref
    default: 1928437192847
    name: null
    path: model
  perform_inference: true
  ref_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-test.ja'
    value: ./kftt-data-1.0/data/tok/kyoto-test.ja
  src_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-test.en'
    value: ./kftt-data-1.0/data/tok/kyoto-test.en
exp_global: !ExpGlobal
  bias_init: !ZeroInitializer {}
  commandline_args:
    backend: torch
    experiment_name: []
    experiments_file: ./config.kftt.en-ja.yaml
    generate_doc: false
    gpu: true
    resume: false
    seed: null
    settings: standard
  default_layer_dim: 512
  dropout: 0.3
  log_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/logs/{EXP}.log'
    value: ./logs/kftt.en-ja.log
  loss_comb_method: sum
  model_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/models/{EXP}.mod'
    value: ./models/kftt.en-ja.mod
  param_init: !GlorotInitializer
    gain: 1.0
  placeholders: {}
  save_num_checkpoints: 1
  weight_noise: 0.0
model: !DefaultTranslator
  attender: !MlpAttender
    bias_init: !Ref
      default: 1928437192847
      name: null
      path: exp_global.bias_init
    hidden_dim: 512
    input_dim: 512
    param_init: !Ref
      default: 1928437192847
      name: null
      path: exp_global.param_init
    state_dim: 512
    xnmt_subcol_name: MlpAttender-fb815d33
  decoder: !AutoRegressiveDecoder
    bridge: !LinearBridge
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      dec_dim: 512
      dec_layers: 2
      enc_dim: 512
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      projector: !Linear
        bias: true
        bias_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.bias_init
        input_dim: 512
        output_dim: 512
        param_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.param_init
        xnmt_subcol_name: Linear-da953d1c
    embedder: !DenseWordEmbedder
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      emb_dim: 512
      fix_norm: null
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      src_reader: !Ref
        default: 1928437192847
        name: null
        path: model.src_reader
      trg_reader: !Ref
        default: 1928437192847
        name: null
        path: model.trg_reader
      vocab: null
      vocab_size: 40003
      weight_noise: 0.0
      word_dropout: 0.0
      xnmt_subcol_name: DenseWordEmbedder-35e672da
    input_dim: 512
    input_feeding: true
    rnn: !UniLSTMSeqTransducer
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      decoder_input_dim: 512
      decoder_input_feeding: true
      hidden_dim: 512
      input_dim: 512
      layers: 2
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      var_dropout: 0.3
      weightnoise_std: 0.0
      xnmt_subcol_name: UniLSTMSeqTransducer-85c06e6e
    scorer: !Softmax
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      input_dim: 512
      label_smoothing: 0.1
      output_projector: !Ref
        default: 1928437192847
        name: null
        path: model.decoder.embedder
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      trg_reader: !Ref
        default: 1928437192847
        name: null
        path: model.trg_reader
      vocab: null
      vocab_size: null
    transform: !AuxNonLinear
      activation: relu
      aux_input_dim: 512
      bias: true
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      input_dim: 512
      output_dim: 512
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      xnmt_subcol_name: AuxNonLinear-5436935f
  encoder: !ResidualSeqTransducer
    child: !BiLSTMSeqTransducer
      backward_layers:
      - !UniLSTMSeqTransducer
        bias_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.bias_init
        decoder_input_dim: null
        decoder_input_feeding: true
        hidden_dim: 256
        input_dim: 512
        layers: 1
        param_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.param_init
        var_dropout: 0.3
        weightnoise_std: 0.0
        xnmt_subcol_name: UniLSTMSeqTransducer-7f83663d
      - !UniLSTMSeqTransducer
        bias_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.bias_init
        decoder_input_dim: null
        decoder_input_feeding: true
        hidden_dim: 256
        input_dim: 512
        layers: 1
        param_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.param_init
        var_dropout: 0.3
        weightnoise_std: 0.0
        xnmt_subcol_name: UniLSTMSeqTransducer-5dec2edd
      bias_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.bias_init
      forward_layers:
      - !UniLSTMSeqTransducer
        bias_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.bias_init
        decoder_input_dim: null
        decoder_input_feeding: true
        hidden_dim: 256
        input_dim: 512
        layers: 1
        param_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.param_init
        var_dropout: 0.3
        weightnoise_std: 0.0
        xnmt_subcol_name: UniLSTMSeqTransducer-82ff1a73
      - !UniLSTMSeqTransducer
        bias_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.bias_init
        decoder_input_dim: null
        decoder_input_feeding: true
        hidden_dim: 256
        input_dim: 512
        layers: 1
        param_init: !Ref
          default: 1928437192847
          name: null
          path: exp_global.param_init
        var_dropout: 0.3
        weightnoise_std: 0.0
        xnmt_subcol_name: UniLSTMSeqTransducer-4dd4e810
      hidden_dim: 512
      input_dim: 512
      layers: 2
      param_init: !Ref
        default: 1928437192847
        name: null
        path: exp_global.param_init
      var_dropout: 0.3
    dropout: 0.3
    input_dim: 512
    layer_norm: false
    layer_norm_component: null
  inference: !AutoRegressiveInference
    batcher: !InOrderBatcher
      batch_size: 1
      pad_src_to_multiple: 1
    max_num_sents: null
    max_src_len: null
    mode: onebest
    post_process: []
    ref_file: null
    reporter: null
    search_strategy: !BeamSearch
      beam_size: 5
      len_norm: !PolynomialNormalization
        apply_during_search: true
        m: 0.8
      max_len: 100
      one_best: true
      scores_proc: null
    src_file: null
    trg_file: null
  src_embedder: !SimpleWordEmbedder
    emb_dim: 512
    fix_norm: null
    param_init: !Ref
      default: 1928437192847
      name: null
      path: exp_global.param_init
    src_reader: !Ref
      default: 1928437192847
      name: null
      path: model.src_reader
    trg_reader: !Ref
      default: 1928437192847
      name: null
      path: model.trg_reader
    vocab: null
    vocab_size: 40003
    weight_noise: 0.0
    word_dropout: 0.0
    xnmt_subcol_name: SimpleWordEmbedder-56af3728
  src_reader: !PlainTextReader
    output_proc: []
    read_sent_len: false
    vocab: !Vocab
      i2w:
      - <s>
      - </s>
      - the
      - ','
      - .
      - of
      - and
      - (
      - )
      - in
      - to
      - was
      - a
      - is
      - ''''
      - as
      - '"'
      - The
      - 'no'
      - by
      - that
      - he
      - for
      - 'on'
      - with
      - his
      - ':'
      - In
      - from
      - He
      - '''s'
      - at
      - were
      - it
      - are
      - It
      - Kyoto
      - an
      - which
      - who
      - also
      - period
      - or
      - family
      - be
      - this
      - Temple
      - City
      - Emperor
      - called
      - name
      - became
      - Japan
      - clan
      - not
      - had
      - Province
      - His
      - Japanese
      - Prefecture
      - but
      - one
      - used
      - Imperial
      - '-'
      - after
      - Station
      - been
      - have
      - son
      - This
      - time
      - has
      - there
      - first
      - However
      - into
      - when
      - 'On'
      - such
      - made
      - during
      - said
      - year
      - they
      - other
      - their
      - its
      - A
      - Edo
      - Shrine
      - died
      - Prince
      - people
      - After
      - government
      - Rank
      - same
      - school
      - between
      - later
      - head
      - years
      - ;
      - father
      - There
      - old
      - under
      - many
      - about
      - two
      - her
      - so
      - only
      - temple
      - daughter
      - Castle
      - Buddhist
      - FUJIWARA
      - because
      - system
      - established
      - death
      - known
      - some
      - located
      - age
      - Line
      - second
      - As
      - up
      - rank
      - Junior
      - appointed
      - position
      - him
      - them
      - out
      - area
      - written
      - court
      - can
      - over
      - Domain
      - served
      - held
      - Nara
      - Ward
      - she
      - /
      - part
      - '1'
      - army
      - station
      - three
      - where
      - than
      - all
      - line
      - around
      - then
      - mother
      - style
      - rice
      - Kamakura
      - following
      - born
      - came
      - April
      - well
      - wife
      - School
      - Tokyo
      - given
      - being
      - MINAMOTO
      - March
      - priest
      - side
      - When
      - took
      - lord
      - Osaka
      - post
      - Meiji

```

tail -n 150 နဲ့ မော်ဒယ်ဖိုင်ရဲ့ နောက်ဆုံးပိုင်းကိုလည်း လေ့လာကြည့်ခဲ့...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/models$ tail -n 150 ./kftt.en-ja.mod
      - "\u30DF\u30FC"
      - "\u3059\u308B\u3081"
      - "\u5BC4\u305B\u934B"
      - "\u51B7\u9EA6"
      - "\u4E38\u68D2"
      - "\u8FFD\u3044\u629C"
      - "\u5730\u6D88"
      - "\u6765\u8CD3"
      - "\u30A4\u30E8\u30FC"
      - "\u6FE1\u308C\u8863"
      - "\u57FA\u5C64"
      - "\u5C0F\u7AE5"
      - "\u3084\u3063\u3064\u3051"
      - "\u624B\u53E3"
      - "\u3068\u304D\u308F"
      - "\u3059\u3093"
      - "\u6642\u4FA1"
      - "\u3042\u3044\u305F"
      - "\u868A\u5C4B"
      - "\u7DF4\u308A\u8FBC"
      - "\u85AC\u5264"
      - "\u30B8\u30E3\u30DD"
      - "\u30BA\u30EA\u30FC"
      - "\u30D5\u30A1\u30F3\u30BF\u30F3"
      - "\u30E9\u30C8\u30A5\u30FC\u30EB"
      - "\u5F15\u51FA\u3057"
      - "\u70AD\u6AC3"
      - "\u3068\u3042"
      - "\u30B9\u30C8\u30FC\u30D6"
      - "\u8B1D\u610F"
      - "\u5FA1\u970A\u524D"
      - "\u30A2\u30FC\u30E2\u30F3\u30C9"
      - <unk>
      sentencepiece_vocab: false
      vocab_file: null
name: kftt.en-ja
preproc: !PreprocRunner
  overwrite: false
  tasks:
  - !PreprocVocab
    in_files:
    - !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.en'
      value: ./kftt-data-1.0/data/tok/kyoto-train.cln.en
    - !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.ja'
      value: ./kftt-data-1.0/data/tok/kyoto-train.cln.ja
    out_files:
    - !SavedFormatString
      unformatted_value: '{EXP_DIR}/vocab.en'
      value: ./vocab.en
    - !SavedFormatString
      unformatted_value: '{EXP_DIR}/vocab.ja'
      value: ./vocab.ja
    specs:
    - filenum: all
      filters:
      - !VocabFiltererRank
        max_rank: 40000
random_search_report: null
status: done
train: !SimpleTrainingRegimen
  batcher: !WordSrcBatcher
    avg_batch_size: 64
    break_ties_randomly: true
    pad_src_to_multiple: 1
    words_per_batch: null
  dev_combinator: null
  dev_loss_tracker: !DevLossTracker
    eval_every: 0
    loss_comb_method: sum
  dev_tasks:
  - !AccuracyEvalTask
    desc: null
    eval_metrics: bleu
    hyp_file: !SavedFormatString
      unformatted_value: '{EXP_DIR}/hyp/{EXP}.dev.ja'
      value: ./hyp/kftt.en-ja.dev.ja
    inference: null
    model: !Ref
      default: 1928437192847
      name: null
      path: model
    perform_inference: true
    ref_file: !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.ja'
      value: ./kftt-data-1.0/data/tok/kyoto-dev.ja
    src_file: !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.en'
      value: ./kftt-data-1.0/data/tok/kyoto-dev.en
  - !LossEvalTask
    batcher: !Ref
      default: 1928437192847
      name: null
      path: train.batcher
    desc: null
    loss_calculator: !MLELoss {}
    max_num_sents: null
    max_src_len: null
    max_trg_len: null
    model: !Ref
      default: 1928437192847
      name: null
      path: model
    ref_file: !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.ja'
      value: ./kftt-data-1.0/data/tok/kyoto-dev.ja
    src_file: !SavedFormatString
      unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-dev.en'
      value: ./kftt-data-1.0/data/tok/kyoto-dev.en
  dev_zero: false
  initial_patience: 2
  loss_calculator: !MLELoss {}
  loss_comb_method: sum
  lr_decay: 0.5
  lr_decay_times: 2
  max_num_train_sents: null
  max_src_len: null
  max_trg_len: null
  model: !Ref
    default: 1928437192847
    name: null
    path: model
  name: !SavedFormatString
    unformatted_value: '{EXP}'
    value: kftt.en-ja
  patience: 1
  reload_command: null
  restart_trainer: false
  run_for_epochs: 20
  sample_train_sents: null
  src_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.en'
    value: ./kftt-data-1.0/data/tok/kyoto-train.cln.en
  train_loss_tracker: !TrainLossTracker
    accumulative: false
    aux_loss_per_token: true
  trainer: !AdamTrainer
    alpha: 0.001
    amsgrad: false
    beta_1: 0.9
    beta_2: 0.999
    eps: 1.0e-08
    rescale_grads: 5.0
    skip_noisy: false
    weight_decay: 0.0
  trg_file: !SavedFormatString
    unformatted_value: '{EXP_DIR}/kftt-data-1.0/data/tok/kyoto-train.cln.ja'
    value: ./kftt-data-1.0/data/tok/kyoto-train.cln.ja
  update_every: 1
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/models$
```

## Check the Hypothesis

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ tree ./hyp
./hyp
├── kftt.en-ja.dev.ja
└── kftt.en-ja.test.ja

0 directories, 2 files
```

dev ရော test ရော ကို file size အတူတူနည်းပါး ထားထားတာကို တွေ့ရ...   

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt$ cd hyp
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/hyp$ wc *
  1166  23707 117960 kftt.en-ja.dev.ja
  1160  25080 123136 kftt.en-ja.test.ja
  2326  48787 241096 total
```

development အတွက် hyp ဖိုင်နဲ့ testing အတွက် hyp ဖိုင်တွေကို head command နဲ့ print လုပ်ကြည့်ရအောင်...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/hyp$ head *
==> kftt.en-ja.dev.ja <==
臨済 禅 （ <unk> <unk> ） と は 、 中国 の 五 家 の 一 つ で 、 唐 の 禅 （ 臨済 ・ <unk> ・ <unk> ・ <unk> ） ・ 臨済 義 玄 （ 貞観 9 年 （ 867 年 ） ? - 貞観 9 年 （ 867 年 ） ） を 祖 と する 。
「 <unk> （ <unk> ） 」 、 『 <unk> <unk> 』 など と し て 知 ら れ 、 独特 の 禅 の 頂点 に まで 達 し た 。
公案 の 研究 に よ り 公案 を 自覚 し よ う と し た 禅 話 が 公案 を 意識 し て い る こと から 、 曹洞 宗 の 禅 禅 と は 異な る 。
中国 の 臨済 流
名前 の 通り 、 唐 の 廃仏 毀釈 後 の 廃仏 毀釈 後 に 臨済 義 玄 を 祖 と する 臨済 宗 を 祖 と する 。
<unk> は <unk> <unk> の 門人 と し て 河北 省 を 中心 と し た 宗教 運動 と し て 発展 し た が 、 唐 末期 の 混乱 が あ っ た こと に 対 し 、 <unk> は 分裂 し た 。
当時 の 中心 的 な 姿 は <unk> <unk> で あ っ た 。
<unk> <unk> の 下 に あ っ た 臨済 宗 の <unk> ・ <unk> ・ <unk> ・ <unk> ・ <unk> と とも に 、 臨済 宗 を 中心 に 各地 を 流 さ れ 、 中国 全土 を 席巻 し た 。
南宋 時代 に 入 る と 、 <unk> 派 に 属 する <unk> <unk> の 門人 ・ <unk> <unk> の 弟子 ・ <unk> <unk> が 、 臨済 宗 に お い て 主要 な 一派 と な っ た 。
日本 の 臨済 流

==> kftt.en-ja.test.ja <==
<unk>
道元 （ 道元 ） は 、 鎌倉 時代 前期 の 禅僧 。
曹洞 禅 の 祖 。
その 後 も 紀元 と も い う 。
また 、 <unk> で あ る 。
『 <unk> <unk> 』 、 <unk> 所 。
一般 に は 道元 禅師 と 呼 ば れ る 。
お 歯黒 を 洗 っ た の は 、 <unk> の <unk> ・ <unk> ・ <unk> ・ <unk> の よう に 広ま っ た と 伝え られ て い る 。
また 、 <unk> を 持参 し て 日本 に <unk> を もたら し た と い う 説 も あ る 。
道元 の 出自 に つ い て は 不明 で あ る が 、 右 大臣 土御門 通親 （ 源 通親 ・ 久我 通親 ） の 系統 で 生まれ た と い う 説 も あ る 。
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/recipes/kftt/hyp$
```

Note: multiple-GPU နဲ့ run တာကို XNMT က လက်ရှိထိ support မလုပ်သေးဘူးလို့ ထင်တယ်။  
Check: [https://github.com/neulab/xnmt/issues/415](https://github.com/neulab/xnmt/issues/415)  

## Reference

- https://github.com/clab/dynet/issues/1570conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=11.3 -c pytorch -c conda-forge
- https://github.com/pydata/bottleneck/issues/281
- https://stackoverflow.com/questions/65349875/where-can-i-find-glibcxx-3-4-29
- https://pytorch.org/get-started/previous-versions/
- https://github.com/neulab/xnmt/blob/transformer-optimizations/examples/16_transformer.yaml
- https://github.com/neulab/xnmt/issues/415



