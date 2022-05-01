
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

```


## Reference

- https://github.com/clab/dynet/issues/1570conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=11.3 -c pytorch -c conda-forge
- https://github.com/pydata/bottleneck/issues/281
- https://stackoverflow.com/questions/65349875/where-can-i-find-glibcxx-3-4-29
- https://pytorch.org/get-started/previous-versions/




