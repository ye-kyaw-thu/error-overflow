# OpenNMT Installation, Training, Testing Log

Date: 9 Jan 2024

## Create New Anaconda Envrionment

```
(base) yekyaw.thu@gpu:~$ conda create --name opennmt python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2023.12.12 |       h06a4308_0         126 KB
    openssl-3.0.12             |       h7f8727e_0         5.2 MB
    pip-23.3.1                 |   py38h06a4308_0         2.6 MB
    setuptools-68.2.2          |   py38h06a4308_0         948 KB
    xz-5.4.5                   |       h5eee18b_0         646 KB
    ------------------------------------------------------------
                                           Total:         9.5 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.12.12-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.12-h7f8727e_0
  pip                pkgs/main/linux-64::pip-23.3.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.18-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.2.2-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.5-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
setuptools-68.2.2    | 948 KB    | ############################################### | 100%
ca-certificates-2023 | 126 KB    | ############################################### | 100%
xz-5.4.5             | 646 KB    | ############################################### | 100%
pip-23.3.1           | 2.6 MB    | ############################################### | 100%
openssl-3.0.12       | 5.2 MB    | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate opennmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~$
```

Activate opennmt env:  

```
(base) yekyaw.thu@gpu:~$ conda activate opennmt
(opennmt) yekyaw.thu@gpu:~$
```

## PyTorch Installation 

Check nvcc version:  

```
(opennmt) yekyaw.thu@gpu:~$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Sun_Jul_28_19:07:16_PDT_2019
Cuda compilation tools, release 10.1, V10.1.243
(opennmt) yekyaw.thu@gpu:~$
```

```
(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio cudatoolkit=10.1 -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: \
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  added / updated specs:
    - cudatoolkit=10.1
    - pytorch
    - torchaudio
    - torchvision


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    brotli-python-1.0.9        |   py38h6a678d5_7         329 KB
    certifi-2023.11.17         |   py38h06a4308_0         158 KB
    cffi-1.16.0                |   py38h5eee18b_0         252 KB
    cryptography-41.0.7        |   py38hdda0065_0         2.0 MB
    cudatoolkit-10.1.243       |       h6bb024c_0       347.4 MB
    ffmpeg-4.3                 |       hf484d3e_0         9.9 MB  pytorch
    filelock-3.13.1            |   py38h06a4308_0          21 KB
    gmp-6.2.1                  |       h295c915_3         544 KB
    gmpy2-2.1.2                |   py38heeb90bb_0         191 KB
    gnutls-3.6.15              |       he1e5248_0         1.0 MB
    intel-openmp-2023.1.0      |   hdb19cb5_46306        17.2 MB
    lame-3.100                 |       h7b6447c_0         323 KB
    lcms2-2.12                 |       h3be6417_0         312 KB
    libiconv-1.16              |       h7f8727e_2         736 KB
    libidn2-2.3.4              |       h5eee18b_0         146 KB
    libjpeg-turbo-2.0.0        |       h9bf148f_0         950 KB  pytorch
    libtasn1-4.19.0            |       h5eee18b_0          63 KB
    libunistring-0.9.10        |       h27cfd23_0         536 KB
    llvm-openmp-14.0.6         |       h9e868ea_0         4.4 MB
    markupsafe-2.1.3           |   py38h5eee18b_0          22 KB
    mkl-2023.1.0               |   h213fc3f_46344       171.5 MB
    mkl-service-2.4.0          |   py38h5eee18b_1          54 KB
    mkl_fft-1.3.8              |   py38h5eee18b_0         221 KB
    mkl_random-1.2.4           |   py38hdb19cb5_0         327 KB
    mpfr-4.0.2                 |       hb69a4c5_1         487 KB
    mpmath-1.3.0               |   py38h06a4308_0         832 KB
    nettle-3.7.3               |       hbbd107a_1         809 KB
    networkx-3.1               |   py38h06a4308_0         2.7 MB
    numpy-1.24.3               |   py38hf6e8229_1          10 KB
    numpy-base-1.24.3          |   py38h060ed82_1         6.2 MB
    openh264-2.1.1             |       h4ff587b_0         711 KB
    openjpeg-2.4.0             |       h3ad879b_0         331 KB
    pillow-10.0.1              |   py38ha6cbd5a_0         742 KB
    pytorch-2.1.2              |      py3.8_cpu_0        77.2 MB  pytorch
    pytorch-mutex-1.0          |              cpu           3 KB  pytorch
    pyyaml-6.0.1               |   py38h5eee18b_0         192 KB
    sympy-1.12                 |   py38h06a4308_0        10.5 MB
    tbb-2021.8.0               |       hdb19cb5_0         1.6 MB
    torchaudio-2.1.2           |         py38_cpu         4.8 MB  pytorch
    torchvision-0.16.2         |         py38_cpu        11.2 MB  pytorch
    urllib3-1.26.18            |   py38h06a4308_0         196 KB
    ------------------------------------------------------------
                                           Total:       677.1 MB

The following NEW packages will be INSTALLED:

  blas               pkgs/main/linux-64::blas-1.0-mkl
  brotli-python      pkgs/main/linux-64::brotli-python-1.0.9-py38h6a678d5_7
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h7b6447c_0
  certifi            pkgs/main/linux-64::certifi-2023.11.17-py38h06a4308_0
  cffi               pkgs/main/linux-64::cffi-1.16.0-py38h5eee18b_0
  charset-normalizer pkgs/main/noarch::charset-normalizer-2.0.4-pyhd3eb1b0_0
  cryptography       pkgs/main/linux-64::cryptography-41.0.7-py38hdda0065_0
  cudatoolkit        pkgs/main/linux-64::cudatoolkit-10.1.243-h6bb024c_0
  ffmpeg             pytorch/linux-64::ffmpeg-4.3-hf484d3e_0
  filelock           pkgs/main/linux-64::filelock-3.13.1-py38h06a4308_0
  freetype           pkgs/main/linux-64::freetype-2.12.1-h4a9f257_0
  giflib             pkgs/main/linux-64::giflib-5.2.1-h5eee18b_3
  gmp                pkgs/main/linux-64::gmp-6.2.1-h295c915_3
  gmpy2              pkgs/main/linux-64::gmpy2-2.1.2-py38heeb90bb_0
  gnutls             pkgs/main/linux-64::gnutls-3.6.15-he1e5248_0
  idna               pkgs/main/linux-64::idna-3.4-py38h06a4308_0
  intel-openmp       pkgs/main/linux-64::intel-openmp-2023.1.0-hdb19cb5_46306
  jinja2             pkgs/main/linux-64::jinja2-3.1.2-py38h06a4308_0
  jpeg               pkgs/main/linux-64::jpeg-9e-h5eee18b_1
  lame               pkgs/main/linux-64::lame-3.100-h7b6447c_0
  lcms2              pkgs/main/linux-64::lcms2-2.12-h3be6417_0
  lerc               pkgs/main/linux-64::lerc-3.0-h295c915_0
  libdeflate         pkgs/main/linux-64::libdeflate-1.17-h5eee18b_1
  libiconv           pkgs/main/linux-64::libiconv-1.16-h7f8727e_2
  libidn2            pkgs/main/linux-64::libidn2-2.3.4-h5eee18b_0
  libjpeg-turbo      pytorch/linux-64::libjpeg-turbo-2.0.0-h9bf148f_0
  libpng             pkgs/main/linux-64::libpng-1.6.39-h5eee18b_0
  libtasn1           pkgs/main/linux-64::libtasn1-4.19.0-h5eee18b_0
  libtiff            pkgs/main/linux-64::libtiff-4.5.1-h6a678d5_0
  libunistring       pkgs/main/linux-64::libunistring-0.9.10-h27cfd23_0
  libwebp            pkgs/main/linux-64::libwebp-1.3.2-h11a3e52_0
  libwebp-base       pkgs/main/linux-64::libwebp-base-1.3.2-h5eee18b_0
  llvm-openmp        pkgs/main/linux-64::llvm-openmp-14.0.6-h9e868ea_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.4-h6a678d5_0
  markupsafe         pkgs/main/linux-64::markupsafe-2.1.3-py38h5eee18b_0
  mkl                pkgs/main/linux-64::mkl-2023.1.0-h213fc3f_46344
  mkl-service        pkgs/main/linux-64::mkl-service-2.4.0-py38h5eee18b_1
  mkl_fft            pkgs/main/linux-64::mkl_fft-1.3.8-py38h5eee18b_0
  mkl_random         pkgs/main/linux-64::mkl_random-1.2.4-py38hdb19cb5_0
  mpc                pkgs/main/linux-64::mpc-1.1.0-h10f8cd9_1
  mpfr               pkgs/main/linux-64::mpfr-4.0.2-hb69a4c5_1
  mpmath             pkgs/main/linux-64::mpmath-1.3.0-py38h06a4308_0
  nettle             pkgs/main/linux-64::nettle-3.7.3-hbbd107a_1
  networkx           pkgs/main/linux-64::networkx-3.1-py38h06a4308_0
  numpy              pkgs/main/linux-64::numpy-1.24.3-py38hf6e8229_1
  numpy-base         pkgs/main/linux-64::numpy-base-1.24.3-py38h060ed82_1
  openh264           pkgs/main/linux-64::openh264-2.1.1-h4ff587b_0
  openjpeg           pkgs/main/linux-64::openjpeg-2.4.0-h3ad879b_0
  pillow             pkgs/main/linux-64::pillow-10.0.1-py38ha6cbd5a_0
  pycparser          pkgs/main/noarch::pycparser-2.21-pyhd3eb1b0_0
  pyopenssl          pkgs/main/linux-64::pyopenssl-23.2.0-py38h06a4308_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38h06a4308_0
  pytorch            pytorch/linux-64::pytorch-2.1.2-py3.8_cpu_0
  pytorch-mutex      pytorch/noarch::pytorch-mutex-1.0-cpu
  pyyaml             pkgs/main/linux-64::pyyaml-6.0.1-py38h5eee18b_0
  requests           pkgs/main/linux-64::requests-2.31.0-py38h06a4308_0
  sympy              pkgs/main/linux-64::sympy-1.12-py38h06a4308_0
  tbb                pkgs/main/linux-64::tbb-2021.8.0-hdb19cb5_0
  torchaudio         pytorch/linux-64::torchaudio-2.1.2-py38_cpu
  torchvision        pytorch/linux-64::torchvision-0.16.2-py38_cpu
  typing_extensions  pkgs/main/linux-64::typing_extensions-4.7.1-py38h06a4308_0
  urllib3            pkgs/main/linux-64::urllib3-1.26.18-py38h06a4308_0
  yaml               pkgs/main/linux-64::yaml-0.2.5-h7b6447c_0
  zstd               pkgs/main/linux-64::zstd-1.5.5-hc292b87_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libjpeg-turbo-2.0.0  | 950 KB    | ############################################### | 100%
gnutls-3.6.15        | 1.0 MB    | ############################################### | 100%
pillow-10.0.1        | 742 KB    | ############################################### | 100%
mpmath-1.3.0         | 832 KB    | ############################################### | 100%
mkl_random-1.2.4     | 327 KB    | ############################################### | 100%
nettle-3.7.3         | 809 KB    | ############################################### | 100%
intel-openmp-2023.1. | 17.2 MB   | ############################################### | 100%
openh264-2.1.1       | 711 KB    | ############################################### | 100%
libunistring-0.9.10  | 536 KB    | ############################################### | 100%
sympy-1.12           | 10.5 MB   | ############################################### | 100%
gmp-6.2.1            | 544 KB    | ############################################### | 100%
pytorch-2.1.2        | 77.2 MB   | ############################################### | 100%
lame-3.100           | 323 KB    | ############################################### | 100%
cryptography-41.0.7  | 2.0 MB    | ############################################### | 100%
libidn2-2.3.4        | 146 KB    | ############################################### | 100%
numpy-1.24.3         | 10 KB     | ############################################### | 100%
mkl_fft-1.3.8        | 221 KB    | ############################################### | 100%
brotli-python-1.0.9  | 329 KB    | ############################################### | 100%
certifi-2023.11.17   | 158 KB    | ############################################### | 100%
cffi-1.16.0          | 252 KB    | ############################################### | 100%
markupsafe-2.1.3     | 22 KB     | ############################################### | 100%
libtasn1-4.19.0      | 63 KB     | ############################################### | 100%
cudatoolkit-10.1.243 | 347.4 MB  | ############################################### | 100%
numpy-base-1.24.3    | 6.2 MB    | ############################################### | 100%
mpfr-4.0.2           | 487 KB    | ############################################### | 100%
filelock-3.13.1      | 21 KB     | ############################################### | 100%
urllib3-1.26.18      | 196 KB    | ############################################### | 100%
ffmpeg-4.3           | 9.9 MB    | ############################################### | 100%
libiconv-1.16        | 736 KB    | ############################################### | 100%
pyyaml-6.0.1         | 192 KB    | ############################################### | 100%
pytorch-mutex-1.0    | 3 KB      | ############################################### | 100%
torchvision-0.16.2   | 11.2 MB   | ############################################### | 100%
llvm-openmp-14.0.6   | 4.4 MB    | ############################################### | 100%
mkl-2023.1.0         | 171.5 MB  | ############################################### | 100%
lcms2-2.12           | 312 KB    | ############################################### | 100%
gmpy2-2.1.2          | 191 KB    | ############################################### | 100%
networkx-3.1         | 2.7 MB    | ############################################### | 100%
mkl-service-2.4.0    | 54 KB     | ############################################### | 100%
torchaudio-2.1.2     | 4.8 MB    | ############################################### | 100%
tbb-2021.8.0         | 1.6 MB    | ############################################### | 100%
openjpeg-2.4.0       | 331 KB    | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$
```

## OpenNMT Installation

```
(opennmt) yekyaw.thu@gpu:~$ pip install OpenNMT-py
Collecting OpenNMT-py
  Downloading OpenNMT_py-3.4.3-py3-none-any.whl.metadata (7.4 kB)
Requirement already satisfied: torch<2.2,>=2.0.1 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-py) (2.1.2)
Collecting configargparse (from OpenNMT-py)
  Downloading ConfigArgParse-1.7-py3-none-any.whl.metadata (23 kB)
Collecting ctranslate2<4,>=3.17 (from OpenNMT-py)
  Downloading ctranslate2-3.23.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (10 kB)
Requirement already satisfied: tensorboard>=2.3 in ./.local/lib/python3.8/site-packages (from OpenNMT-py) (2.11.2)
Collecting flask (from OpenNMT-py)
  Downloading flask-3.0.0-py3-none-any.whl.metadata (3.6 kB)
Collecting waitress (from OpenNMT-py)
  Downloading waitress-2.1.2-py3-none-any.whl (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.7/57.7 kB 99.9 kB/s eta 0:00:00
Collecting pyonmttok<2,>=1.35 (from OpenNMT-py)
  Downloading pyonmttok-1.37.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.0/17.0 MB 71.7 kB/s eta 0:00:00
Requirement already satisfied: pyyaml in ./.conda/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-py) (6.0.1)
Collecting sacrebleu (from OpenNMT-py)
  Downloading sacrebleu-2.4.0-py3-none-any.whl.metadata (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.4/57.4 kB 89.9 kB/s eta 0:00:00
Collecting rapidfuzz (from OpenNMT-py)
  Downloading rapidfuzz-3.6.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)
Collecting pyahocorasick (from OpenNMT-py)
  Downloading pyahocorasick-2.0.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (104 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 104.5/104.5 kB 61.3 kB/s eta 0:00:00
Collecting fasttext-wheel (from OpenNMT-py)
  Downloading fasttext_wheel-0.9.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.4/4.4 MB 73.4 kB/s eta 0:00:00
Collecting spacy (from OpenNMT-py)
  Downloading spacy-3.7.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (25 kB)
Collecting six (from OpenNMT-py)
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Requirement already satisfied: setuptools in ./.conda/envs/opennmt/lib/python3.8/site-packages (from ctranslate2<4,>=3.17->OpenNMT-py) (68.2.2)
Requirement already satisfied: numpy in ./.local/lib/python3.8/site-packages (from ctranslate2<4,>=3.17->OpenNMT-py) (1.24.1)
Requirement already satisfied: absl-py>=0.4 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (1.4.0)
Requirement already satisfied: grpcio>=1.24.3 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (1.51.1)
Requirement already satisfied: google-auth<3,>=1.6.3 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (2.16.0)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (0.4.6)
Requirement already satisfied: markdown>=2.6.8 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (3.4.1)
Requirement already satisfied: protobuf<4,>=3.9.2 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (3.19.6)
Requirement already satisfied: requests<3,>=2.21.0 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (2.31.0)
Requirement already satisfied: tensorboard-data-server<0.7.0,>=0.6.0 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (0.6.1)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (1.8.1)
Requirement already satisfied: werkzeug>=1.0.1 in ./.local/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (2.2.2)
Requirement already satisfied: wheel>=0.26 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from tensorboard>=2.3->OpenNMT-py) (0.41.2)
Requirement already satisfied: filelock in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch<2.2,>=2.0.1->OpenNMT-py) (3.13.1)
Requirement already satisfied: typing-extensions in ./.local/lib/python3.8/site-packages (from torch<2.2,>=2.0.1->OpenNMT-py) (4.4.0)
Requirement already satisfied: sympy in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch<2.2,>=2.0.1->OpenNMT-py) (1.12)
Requirement already satisfied: networkx in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch<2.2,>=2.0.1->OpenNMT-py) (3.1)
Requirement already satisfied: jinja2 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch<2.2,>=2.0.1->OpenNMT-py) (3.1.2)
Collecting fsspec (from torch<2.2,>=2.0.1->OpenNMT-py)
  Downloading fsspec-2023.12.2-py3-none-any.whl.metadata (6.8 kB)
Collecting pybind11>=2.2 (from fasttext-wheel->OpenNMT-py)
  Downloading pybind11-2.11.1-py3-none-any.whl.metadata (9.5 kB)
Collecting werkzeug>=1.0.1 (from tensorboard>=2.3->OpenNMT-py)
  Downloading werkzeug-3.0.1-py3-none-any.whl.metadata (4.1 kB)
Collecting itsdangerous>=2.1.2 (from flask->OpenNMT-py)
  Downloading itsdangerous-2.1.2-py3-none-any.whl (15 kB)
Collecting click>=8.1.3 (from flask->OpenNMT-py)
  Using cached click-8.1.7-py3-none-any.whl.metadata (3.0 kB)
Collecting blinker>=1.6.2 (from flask->OpenNMT-py)
  Downloading blinker-1.7.0-py3-none-any.whl.metadata (1.9 kB)
Requirement already satisfied: importlib-metadata>=3.6.0 in ./.local/lib/python3.8/site-packages (from flask->OpenNMT-py) (6.0.0)
Collecting portalocker (from sacrebleu->OpenNMT-py)
  Downloading portalocker-2.8.2-py3-none-any.whl.metadata (8.5 kB)
Collecting regex (from sacrebleu->OpenNMT-py)
  Downloading regex-2023.12.25-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.9/40.9 kB 95.2 kB/s eta 0:00:00
Collecting tabulate>=0.8.9 (from sacrebleu->OpenNMT-py)
  Downloading tabulate-0.9.0-py3-none-any.whl (35 kB)
Collecting colorama (from sacrebleu->OpenNMT-py)
  Downloading colorama-0.4.6-py2.py3-none-any.whl (25 kB)
Collecting lxml (from sacrebleu->OpenNMT-py)
  Downloading lxml-5.1.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.5 kB)
Collecting spacy-legacy<3.1.0,>=3.0.11 (from spacy->OpenNMT-py)
  Downloading spacy_legacy-3.0.12-py2.py3-none-any.whl (29 kB)
Collecting spacy-loggers<2.0.0,>=1.0.0 (from spacy->OpenNMT-py)
  Downloading spacy_loggers-1.0.5-py3-none-any.whl.metadata (23 kB)
Collecting murmurhash<1.1.0,>=0.28.0 (from spacy->OpenNMT-py)
  Downloading murmurhash-1.0.10-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.0 kB)
Collecting cymem<2.1.0,>=2.0.2 (from spacy->OpenNMT-py)
  Downloading cymem-2.0.8-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (8.4 kB)
Collecting preshed<3.1.0,>=3.0.2 (from spacy->OpenNMT-py)
  Downloading preshed-3.0.9-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.2 kB)
Collecting thinc<8.3.0,>=8.1.8 (from spacy->OpenNMT-py)
  Downloading thinc-8.2.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (15 kB)
Collecting wasabi<1.2.0,>=0.9.1 (from spacy->OpenNMT-py)
  Downloading wasabi-1.1.2-py3-none-any.whl.metadata (28 kB)
Collecting srsly<3.0.0,>=2.4.3 (from spacy->OpenNMT-py)
  Downloading srsly-2.4.8-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (20 kB)
Collecting catalogue<2.1.0,>=2.0.6 (from spacy->OpenNMT-py)
  Downloading catalogue-2.0.10-py3-none-any.whl.metadata (14 kB)
Collecting weasel<0.4.0,>=0.1.0 (from spacy->OpenNMT-py)
  Downloading weasel-0.3.4-py3-none-any.whl.metadata (4.7 kB)
Collecting typer<0.10.0,>=0.3.0 (from spacy->OpenNMT-py)
  Downloading typer-0.9.0-py3-none-any.whl (45 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.9/45.9 kB 98.0 kB/s eta 0:00:00
Collecting smart-open<7.0.0,>=5.2.1 (from spacy->OpenNMT-py)
  Downloading smart_open-6.4.0-py3-none-any.whl.metadata (21 kB)
Collecting tqdm<5.0.0,>=4.38.0 (from spacy->OpenNMT-py)
  Using cached tqdm-4.66.1-py3-none-any.whl.metadata (57 kB)
Collecting pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4 (from spacy->OpenNMT-py)
  Downloading pydantic-2.5.3-py3-none-any.whl.metadata (65 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 65.6/65.6 kB 62.8 kB/s eta 0:00:00
Requirement already satisfied: packaging>=20.0 in ./.local/lib/python3.8/site-packages (from spacy->OpenNMT-py) (23.0)
Collecting langcodes<4.0.0,>=3.2.0 (from spacy->OpenNMT-py)
  Downloading langcodes-3.3.0-py3-none-any.whl (181 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.6/181.6 kB 50.9 kB/s eta 0:00:00
Requirement already satisfied: cachetools<6.0,>=2.0.0 in ./.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard>=2.3->OpenNMT-py) (5.2.1)
Collecting pyasn1-modules>=0.2.1 (from google-auth<3,>=1.6.3->tensorboard>=2.3->OpenNMT-py)
  Downloading pyasn1_modules-0.3.0-py2.py3-none-any.whl (181 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.3/181.3 kB 52.5 kB/s eta 0:00:00
Requirement already satisfied: rsa<5,>=3.1.4 in ./.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard>=2.3->OpenNMT-py) (4.9)
Requirement already satisfied: requests-oauthlib>=0.7.0 in ./.local/lib/python3.8/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=2.3->OpenNMT-py) (1.3.1)
Collecting zipp>=0.5 (from importlib-metadata>=3.6.0->flask->OpenNMT-py)
  Downloading zipp-3.17.0-py3-none-any.whl.metadata (3.7 kB)
Requirement already satisfied: MarkupSafe>=2.0 in ./.local/lib/python3.8/site-packages (from jinja2->torch<2.2,>=2.0.1->OpenNMT-py) (2.1.1)
Collecting annotated-types>=0.4.0 (from pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4->spacy->OpenNMT-py)
  Downloading annotated_types-0.6.0-py3-none-any.whl.metadata (12 kB)
Collecting pydantic-core==2.14.6 (from pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4->spacy->OpenNMT-py)
  Downloading pydantic_core-2.14.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.5 kB)
Collecting typing-extensions (from torch<2.2,>=2.0.1->OpenNMT-py)
  Downloading typing_extensions-4.9.0-py3-none-any.whl.metadata (3.0 kB)
Requirement already satisfied: charset-normalizer<4,>=2 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard>=2.3->OpenNMT-py) (2.0.4)
Requirement already satisfied: idna<4,>=2.5 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard>=2.3->OpenNMT-py) (3.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard>=2.3->OpenNMT-py) (1.26.18)
Requirement already satisfied: certifi>=2017.4.17 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard>=2.3->OpenNMT-py) (2023.11.17)
Collecting blis<0.8.0,>=0.7.8 (from thinc<8.3.0,>=8.1.8->spacy->OpenNMT-py)
  Downloading blis-0.7.11-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.4 kB)
Collecting confection<1.0.0,>=0.0.1 (from thinc<8.3.0,>=8.1.8->spacy->OpenNMT-py)
  Downloading confection-0.1.4-py3-none-any.whl.metadata (19 kB)
Collecting cloudpathlib<0.17.0,>=0.7.0 (from weasel<0.4.0,>=0.1.0->spacy->OpenNMT-py)
  Downloading cloudpathlib-0.16.0-py3-none-any.whl.metadata (14 kB)
Requirement already satisfied: mpmath>=0.19 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from sympy->torch<2.2,>=2.0.1->OpenNMT-py) (1.3.0)
Collecting pyasn1<0.6.0,>=0.4.6 (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard>=2.3->OpenNMT-py)
  Downloading pyasn1-0.5.1-py2.py3-none-any.whl.metadata (8.6 kB)
Collecting oauthlib>=3.0.0 (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=2.3->OpenNMT-py)
  Downloading oauthlib-3.2.2-py3-none-any.whl (151 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 151.7/151.7 kB 51.4 kB/s eta 0:00:00
Downloading OpenNMT_py-3.4.3-py3-none-any.whl (257 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 257.3/257.3 kB 65.4 kB/s eta 0:00:00
Downloading ctranslate2-3.23.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (36.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 36.8/36.8 MB 90.7 kB/s eta 0:00:00
Downloading ConfigArgParse-1.7-py3-none-any.whl (25 kB)
Downloading flask-3.0.0-py3-none-any.whl (99 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 99.7/99.7 kB 77.8 kB/s eta 0:00:00
Downloading rapidfuzz-3.6.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.4/3.4 MB 119.7 kB/s eta 0:00:00
Downloading sacrebleu-2.4.0-py3-none-any.whl (106 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 106.3/106.3 kB 90.2 kB/s eta 0:00:00
Downloading spacy-3.7.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (6.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.7/6.7 MB 125.2 kB/s eta 0:00:00
Downloading blinker-1.7.0-py3-none-any.whl (13 kB)
Downloading catalogue-2.0.10-py3-none-any.whl (17 kB)
Using cached click-8.1.7-py3-none-any.whl (97 kB)
Downloading cymem-2.0.8-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (46 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 46.4/46.4 kB 253.4 kB/s eta 0:00:00
Downloading murmurhash-1.0.10-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (29 kB)
Downloading preshed-3.0.9-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (154 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 154.2/154.2 kB 225.0 kB/s eta 0:00:00
Downloading pybind11-2.11.1-py3-none-any.whl (227 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 227.7/227.7 kB 190.7 kB/s eta 0:00:00
Downloading pydantic-2.5.3-py3-none-any.whl (381 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 381.9/381.9 kB 72.1 kB/s eta 0:00:00
Downloading pydantic_core-2.14.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 89.0 kB/s eta 0:00:00
Downloading smart_open-6.4.0-py3-none-any.whl (57 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.0/57.0 kB 152.6 kB/s eta 0:00:00
Downloading spacy_loggers-1.0.5-py3-none-any.whl (22 kB)
Downloading srsly-2.4.8-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (494 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 494.3/494.3 kB 95.6 kB/s eta 0:00:00
Downloading thinc-8.2.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (934 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 934.3/934.3 kB 297.7 kB/s eta 0:00:00
Using cached tqdm-4.66.1-py3-none-any.whl (78 kB)
Downloading typing_extensions-4.9.0-py3-none-any.whl (32 kB)
Downloading wasabi-1.1.2-py3-none-any.whl (27 kB)
Downloading weasel-0.3.4-py3-none-any.whl (50 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 50.1/50.1 kB 180.1 kB/s eta 0:00:00
Downloading werkzeug-3.0.1-py3-none-any.whl (226 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 226.7/226.7 kB 134.9 kB/s eta 0:00:00
Downloading fsspec-2023.12.2-py3-none-any.whl (168 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 169.0/169.0 kB 70.2 kB/s eta 0:00:00
Downloading lxml-5.1.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (8.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.0/8.0 MB 158.4 kB/s eta 0:00:00
Downloading portalocker-2.8.2-py3-none-any.whl (17 kB)
Downloading regex-2023.12.25-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (777 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 777.0/777.0 kB 138.1 kB/s eta 0:00:00
Downloading annotated_types-0.6.0-py3-none-any.whl (12 kB)
Downloading blis-0.7.11-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (10.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 10.2/10.2 MB 150.7 kB/s eta 0:00:00
Downloading cloudpathlib-0.16.0-py3-none-any.whl (45 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.0/45.0 kB 86.5 kB/s eta 0:00:00
Downloading confection-0.1.4-py3-none-any.whl (35 kB)
Downloading zipp-3.17.0-py3-none-any.whl (7.4 kB)
Downloading pyasn1-0.5.1-py2.py3-none-any.whl (84 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 84.9/84.9 kB 91.7 kB/s eta 0:00:00
Installing collected packages: cymem, zipp, werkzeug, wasabi, waitress, typing-extensions, tqdm, tabulate, spacy-loggers, spacy-legacy, smart-open, six, regex, rapidfuzz, pyonmttok, pybind11, pyasn1, pyahocorasick, portalocker, oauthlib, murmurhash, lxml, langcodes, itsdangerous, fsspec, ctranslate2, configargparse, colorama, click, catalogue, blis, blinker, typer, srsly, sacrebleu, pydantic-core, pyasn1-modules, preshed, fasttext-wheel, cloudpathlib, annotated-types, pydantic, flask, confection, weasel, thinc, spacy, OpenNMT-py
  Attempting uninstall: werkzeug
    Found existing installation: Werkzeug 2.2.2
    Uninstalling Werkzeug-2.2.2:
      Successfully uninstalled Werkzeug-2.2.2
  Attempting uninstall: typing-extensions
    Found existing installation: typing_extensions 4.4.0
    Uninstalling typing_extensions-4.4.0:
      Successfully uninstalled typing_extensions-4.4.0
Successfully installed OpenNMT-py-3.4.3 annotated-types-0.6.0 blinker-1.7.0 blis-0.7.11 catalogue-2.0.10 click-8.1.7 cloudpathlib-0.16.0 colorama-0.4.6 confection-0.1.4 configargparse-1.7 ctranslate2-3.23.0 cymem-2.0.8 fasttext-wheel-0.9.2 flask-3.0.0 fsspec-2023.12.2 itsdangerous-2.1.2 langcodes-3.3.0 lxml-5.1.0 murmurhash-1.0.10 oauthlib-3.2.2 portalocker-2.8.2 preshed-3.0.9 pyahocorasick-2.0.0 pyasn1-0.5.1 pyasn1-modules-0.3.0 pybind11-2.11.1 pydantic-2.5.3 pydantic-core-2.14.6 pyonmttok-1.37.1 rapidfuzz-3.6.1 regex-2023.12.25 sacrebleu-2.4.0 six-1.16.0 smart-open-6.4.0 spacy-3.7.2 spacy-legacy-3.0.12 spacy-loggers-1.0.5 srsly-2.4.8 tabulate-0.9.0 thinc-8.2.2 tqdm-4.66.1 typer-0.9.0 typing-extensions-4.7.1 waitress-2.1.2 wasabi-1.1.2 weasel-0.3.4 werkzeug-3.0.1 zipp-3.17.0
(opennmt) yekyaw.thu@gpu:~$
```

## Verify the Installation

```
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
False
(opennmt) yekyaw.thu@gpu:~$
```

PyTorch က GPU ကို recognition မဖြစ်လို့ False လို့ ပေါ်နေတာ ...  
Error ဖြစ်နိုင်ချေက အမျိုးမျိုးပဲ CUDA နဲ့ PyTorch ဗားရှင်းက မကိုက်တာ။ Anaconda environment ပြဿနာ ...  

အရင်ဆုံး nvidia-smi command ကို လက်ရှိ environment မှာ run လို့ ရမရ ပြန်စစ်ကြည့်တော့ အောက်ပါအတိုင်း အဆင်ပြေတာကို တွေ့ခဲ့ရတယ်။  

```
(opennmt) yekyaw.thu@gpu:~$ nvidia-smi
Tue Jan  9 13:41:50 2024
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.223.02   Driver Version: 470.223.02   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 30%   41C    P0    57W / 300W |      0MiB / 11019MiB |      1%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 60%   69C    P0    73W / 257W |      0MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 18%   64C    P0    71W / 250W |      0MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
(opennmt) yekyaw.thu@gpu:~$
```

အဲဒါကြောင့် cudatoolkit=10.1 နဲ့ အဆင်မပြေဘူးလို့ ယူဆတယ်။   

## Installation of cudatoolkit=11.4

အရင်ဆုံး လက်ရှိ install လုပ်ထားတဲ့ cuda ကို uninstall လုပ်ခဲ့တယ်။  

```
(opennmt) yekyaw.thu@gpu:~$ conda uninstall pytorch torchvision torchaudio
Collecting package metadata (repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  removed specs:
    - pytorch
    - torchaudio
    - torchvision


The following packages will be REMOVED:

  pytorch-2.1.2-py3.8_cpu_0
  torchaudio-2.1.2-py38_cpu
  torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

# >>>>>>>>>>>>>>>>>>>>>> ERROR REPORT <<<<<<<<<<<<<<<<<<<<<<

    Traceback (most recent call last):
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/exceptions.py", line 1079, in __call__
        return func(*args, **kwargs)
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/main.py", line 84, in _main
        exit_code = do_call(args, p)
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/conda_argparse.py", line 82, in do_call
        return getattr(module, func_name)(args, parser)
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/main_remove.py", line 87, in execute
        handle_txn(txn, prefix, args, False, True)
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/install.py", line 334, in handle_txn
        common.confirm_yn()
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/common.py", line 59, in confirm_yn
        choice = confirm(message=message, choices=('yes', 'no'), default=default)
      File "/opt/anaconda/anaconda3/lib/python3.7/site-packages/conda/cli/common.py", line 42, in confirm
        user_choice = sys.stdin.readline().strip().lower()
      File "/opt/anaconda/anaconda3/lib/python3.7/codecs.py", line 322, in decode
        (result, consumed) = self._buffer_decode(data, self.errors, final)
    UnicodeDecodeError: 'utf-8' codec can't decode bytes in position 0-1: invalid continuation byte

`$ /opt/anaconda/anaconda3/bin/conda uninstall pytorch torchvision torchaudio`

  environment variables:
                 CIO_TEST=<not set>
        CONDA_DEFAULT_ENV=opennmt
                CONDA_EXE=/opt/anaconda/anaconda3/bin/conda
             CONDA_PREFIX=/home/yekyaw.thu/.conda/envs/opennmt
           CONDA_PREFIX_1=/opt/anaconda/anaconda3
    CONDA_PROMPT_MODIFIER=(opennmt)
         CONDA_PYTHON_EXE=/opt/anaconda/anaconda3/bin/python
               CONDA_ROOT=/opt/anaconda/anaconda3
              CONDA_SHLVL=2
                     PATH=/opt/anaconda/anaconda3/bin:/home/yekyaw.thu/.conda/envs/opennmt/bin:/
                          opt/anaconda/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sb
                          in:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
       REQUESTS_CA_BUNDLE=<not set>
            SSL_CERT_FILE=<not set>

     active environment : opennmt
    active env location : /home/yekyaw.thu/.conda/envs/opennmt
            shell level : 2
       user config file : /home/yekyaw.thu/.condarc
 populated config files :
          conda version : 4.8.2
    conda-build version : 3.18.11
         python version : 3.7.6.final.0
       virtual packages : __cuda=11.4
                          __glibc=2.31
       base environment : /opt/anaconda/anaconda3  (read only)
           channel URLs : https://repo.anaconda.com/pkgs/main/linux-64
                          https://repo.anaconda.com/pkgs/main/noarch
                          https://repo.anaconda.com/pkgs/r/linux-64
                          https://repo.anaconda.com/pkgs/r/noarch
          package cache : /opt/anaconda/anaconda3/pkgs
                          /home/yekyaw.thu/.conda/pkgs
       envs directories : /home/yekyaw.thu/.conda/envs
                          /opt/anaconda/anaconda3/envs
               platform : linux-64
             user-agent : conda/4.8.2 requests/2.25.1 CPython/3.7.6 Linux/5.4.0-166-generic ubuntu/20.04.3 glibc/2.31
                UID:GID : 804601154:804600513
             netrc file : None
           offline mode : False


An unexpected error has occurred. Conda has prepared the above report.

If submitted, this report will be used by core maintainers to improve
future releases of conda.
Would you like conda to send this report to the core maintainers?

[y/N]: N

No report sent. To permanently opt-out, use

    $ conda config --set report_errors false


(opennmt) yekyaw.thu@gpu:~$
```

conda install pytorch torchvision torchaudio cudatoolkit=11.4 -c pytorch  

```
(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio cudatoolkit=11.4 -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Collecting package metadata (repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.

PackagesNotFoundError: The following packages are not available from current channels:

  - cudatoolkit=11.4

Current channels:

  - https://conda.anaconda.org/pytorch/linux-64
  - https://conda.anaconda.org/pytorch/noarch
  - https://repo.anaconda.com/pkgs/main/linux-64
  - https://repo.anaconda.com/pkgs/main/noarch
  - https://repo.anaconda.com/pkgs/r/linux-64
  - https://repo.anaconda.com/pkgs/r/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page.


(opennmt) yekyaw.thu@gpu:~$
```

အထက်ပါအတိုင်း အဆင်မပြေလို့ version ကို ဘာမှ assign မလုပ်ပဲ install လုပ်ကြည့်ခဲ့ ...  


```
(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio -c pytorch
udio -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: |
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - pytorch/linux-64::torchaudio==2.1.2=py38_cpu
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - pytorch/linux-64::torchvision==0.16.2=py38_cpu
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - pytorch/linux-64::pytorch==2.1.2=py3.8_cpu_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



# All requested packages already installed.

(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: \
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - pytorch/linux-64::torchaudio==2.1.2=py38_cpu
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - pytorch/linux-64::torchvision==0.16.2=py38_cpu
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - pytorch/linux-64::pytorch==2.1.2=py3.8_cpu_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



# All requested packages already installed.

(opennmt) yekyaw.thu@gpu:~$
```

## Verify Again  

```
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
False
(opennmt) yekyaw.thu@gpu:~$
```

Oh! WTF!  

## Updating Conda

```
(opennmt) yekyaw.thu@gpu:~$ conda update --all
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - pytorch/linux-64::torchaudio==2.1.2=py38_cpu
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - pytorch/linux-64::torchvision==0.16.2=py38_cpu
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - pytorch/linux-64::pytorch==2.1.2=py3.8_cpu_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    cudatoolkit-11.8.0         |       h6a678d5_0       630.7 MB
    ------------------------------------------------------------
                                           Total:       630.7 MB

The following packages will be UPDATED:

  cudatoolkit                           10.1.243-h6bb024c_0 --> 11.8.0-h6a678d5_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
cudatoolkit-11.8.0   | 630.7 MB  | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: | b'By downloading and using the CUDA Toolkit conda packages, you accept the terms and conditions of the CUDA End User License Agreement (EULA): https://docs.nvidia.com/cuda/eula/index.html\n'
done
(opennmt) yekyaw.thu@gpu:~$
```

## Verify Again

```
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
False
(opennmt) yekyaw.thu@gpu:~$
```

## Uninstall and Install PyTorch

```
(opennmt) yekyaw.thu@gpu:~$ conda uninstall pytorch torchvision torchaudio
Collecting package metadata (repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::cudatoolkit==11.8.0=h6a678d5_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  removed specs:
    - pytorch
    - torchaudio
    - torchvision


The following packages will be REMOVED:

  pytorch-2.1.2-py3.8_cpu_0
  torchaudio-2.1.2-py38_cpu
  torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$
```

Install again ...  

```
(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: \
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cudatoolkit==11.8.0=h6a678d5_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  added / updated specs:
    - pytorch
    - torchaudio
    - torchvision


The following NEW packages will be INSTALLED:

  pytorch            pytorch/linux-64::pytorch-2.1.2-py3.8_cpu_0
  torchaudio         pytorch/linux-64::torchaudio-2.1.2-py38_cpu
  torchvision        pytorch/linux-64::torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$
```

## Verify Again  

```
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
False
(opennmt) yekyaw.thu@gpu:~$
```

Oh! No ...  

## Uninstall, Install, Try Again


```
(opennmt) yekyaw.thu@gpu:~$ conda uninstall pytorch torchvision torchaudio
Collecting package metadata (repodata.json): done
Solving environment: /
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::cudatoolkit==11.8.0=h6a678d5_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  removed specs:
    - pytorch
    - torchaudio
    - torchvision


The following packages will be REMOVED:

  pytorch-2.1.2-py3.8_cpu_0
  torchaudio-2.1.2-py38_cpu
  torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$
```

Installation and verify again ...  

```
(opennmt) yekyaw.thu@gpu:~$ conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Collecting package metadata (repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cudatoolkit==11.8.0=h6a678d5_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  added / updated specs:
    - cudatoolkit=10.2
    - pytorch
    - torchaudio
    - torchvision


The following NEW packages will be INSTALLED:

  pytorch            pytorch/linux-64::pytorch-2.1.2-py3.8_cpu_0
  torchaudio         pytorch/linux-64::torchaudio-2.1.2-py38_cpu
  torchvision        pytorch/linux-64::torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
False
```

## Uninstall, For this time Install with Pip

```
(opennmt) yekyaw.thu@gpu:~$ conda uninstall pytorch torchvision torchaudio
Collecting package metadata (repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::cudatoolkit==11.8.0=h6a678d5_0
  - defaults/linux-64::giflib==5.2.1=h5eee18b_3
  - defaults/linux-64::gmp==6.2.1=h295c915_3
  - defaults/linux-64::jpeg==9e=h5eee18b_1
  - defaults/linux-64::lame==3.100=h7b6447c_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::libdeflate==1.17=h5eee18b_1
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::libiconv==1.16=h7f8727e_2
  - pytorch/linux-64::libjpeg-turbo==2.0.0=h9bf148f_0
  - defaults/linux-64::libtasn1==4.19.0=h5eee18b_0
  - defaults/linux-64::libunistring==0.9.10=h27cfd23_0
  - defaults/linux-64::libwebp-base==1.3.2=h5eee18b_0
  - defaults/linux-64::lz4-c==1.9.4=h6a678d5_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::openh264==2.1.1=h4ff587b_0
  - defaults/linux-64::openssl==3.0.12=h7f8727e_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::yaml==0.2.5=h7b6447c_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::libidn2==2.3.4=h5eee18b_0
  - defaults/linux-64::libpng==1.6.39=h5eee18b_0
  - defaults/linux-64::llvm-openmp==14.0.6=h9e868ea_0
  - defaults/linux-64::mpfr==4.0.2=hb69a4c5_1
  - defaults/linux-64::nettle==3.7.3=hbbd107a_1
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::zstd==1.5.5=hc292b87_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::gnutls==3.6.15=he1e5248_0
  - defaults/linux-64::libtiff==4.5.1=h6a678d5_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::mpc==1.1.0=h10f8cd9_1
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - pytorch/linux-64::ffmpeg==4.3=hf484d3e_0
  - defaults/linux-64::lcms2==2.12=h3be6417_0
  - defaults/linux-64::libwebp==1.3.2=h11a3e52_0
  - defaults/linux-64::openjpeg==2.4.0=h3ad879b_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::certifi==2023.11.17=py38h06a4308_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::filelock==3.13.1=py38h06a4308_0
  - defaults/linux-64::gmpy2==2.1.2=py38heeb90bb_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::markupsafe==2.1.3=py38h5eee18b_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::mpmath==1.3.0=py38h06a4308_0
  - defaults/linux-64::networkx==3.1=py38h06a4308_0
  - defaults/linux-64::pillow==10.0.1=py38ha6cbd5a_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pyyaml==6.0.1=py38h5eee18b_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::typing_extensions==4.7.1=py38h06a4308_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::cffi==1.16.0=py38h5eee18b_0
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::sympy==1.12=py38h06a4308_0
  - defaults/linux-64::cryptography==41.0.7=py38hdda0065_0
  - defaults/linux-64::pyopenssl==23.2.0=py38h06a4308_0
  - defaults/linux-64::urllib3==1.26.18=py38h06a4308_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_0
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.11.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/opennmt

  removed specs:
    - pytorch
    - torchaudio
    - torchvision


The following packages will be REMOVED:

  pytorch-2.1.2-py3.8_cpu_0
  torchaudio-2.1.2-py38_cpu
  torchvision-0.16.2-py38_cpu


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(opennmt) yekyaw.thu@gpu:~$
```

ဒီတခါတော့ pip နဲ့ installation လုပ်ကြည့်ခဲ့...  

```
(opennmt) yekyaw.thu@gpu:~$ pip install torch torchvision torchaudio
Collecting torch
  Downloading torch-2.1.2-cp38-cp38-manylinux1_x86_64.whl.metadata (25 kB)
Collecting torchvision
  Downloading torchvision-0.16.2-cp38-cp38-manylinux1_x86_64.whl.metadata (6.6 kB)
Collecting torchaudio
  Downloading torchaudio-2.1.2-cp38-cp38-manylinux1_x86_64.whl.metadata (6.4 kB)
Requirement already satisfied: filelock in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (3.13.1)
Requirement already satisfied: typing-extensions in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (4.7.1)
Requirement already satisfied: sympy in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (1.12)
Requirement already satisfied: networkx in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (3.1)
Requirement already satisfied: jinja2 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (3.1.2)
Requirement already satisfied: fsspec in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torch) (2023.12.2)
Collecting nvidia-cuda-nvrtc-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (23.7 MB)
Collecting nvidia-cuda-runtime-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (823 kB)
Collecting nvidia-cuda-cupti-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (14.1 MB)
Collecting nvidia-cudnn-cu12==8.9.2.26 (from torch)
  Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cublas-cu12==12.1.3.1 (from torch)
  Using cached nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl (410.6 MB)
Collecting nvidia-cufft-cu12==11.0.2.54 (from torch)
  Using cached nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl (121.6 MB)
Collecting nvidia-curand-cu12==10.3.2.106 (from torch)
  Using cached nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl (56.5 MB)
Collecting nvidia-cusolver-cu12==11.4.5.107 (from torch)
  Using cached nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl (124.2 MB)
Collecting nvidia-cusparse-cu12==12.1.0.106 (from torch)
  Using cached nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl (196.0 MB)
Collecting nvidia-nccl-cu12==2.18.1 (from torch)
  Using cached nvidia_nccl_cu12-2.18.1-py3-none-manylinux1_x86_64.whl (209.8 MB)
Collecting nvidia-nvtx-cu12==12.1.105 (from torch)
  Using cached nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (99 kB)
Collecting triton==2.1.0 (from torch)
  Using cached triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl.metadata (1.3 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cusolver-cu12==11.4.5.107->torch)
  Downloading nvidia_nvjitlink_cu12-12.3.101-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Requirement already satisfied: numpy in ./.local/lib/python3.8/site-packages (from torchvision) (1.24.1)
Requirement already satisfied: requests in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torchvision) (2.31.0)
Requirement already satisfied: pillow!=8.3.*,>=5.3.0 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from torchvision) (10.0.1)
Requirement already satisfied: MarkupSafe>=2.0 in ./.local/lib/python3.8/site-packages (from jinja2->torch) (2.1.1)
Requirement already satisfied: charset-normalizer<4,>=2 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests->torchvision) (2.0.4)
Requirement already satisfied: idna<4,>=2.5 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests->torchvision) (3.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests->torchvision) (1.26.18)
Requirement already satisfied: certifi>=2017.4.17 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from requests->torchvision) (2023.11.17)
Requirement already satisfied: mpmath>=0.19 in ./.conda/envs/opennmt/lib/python3.8/site-packages (from sympy->torch) (1.3.0)
Downloading torch-2.1.2-cp38-cp38-manylinux1_x86_64.whl (670.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 670.2/670.2 MB 1.6 MB/s eta 0:00:00
Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl (731.7 MB)
Using cached triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (89.2 MB)
Downloading torchvision-0.16.2-cp38-cp38-manylinux1_x86_64.whl (6.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.8/6.8 MB 5.6 MB/s eta 0:00:00
Downloading torchaudio-2.1.2-cp38-cp38-manylinux1_x86_64.whl (3.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.3/3.3 MB 5.7 MB/s eta 0:00:00
Downloading nvidia_nvjitlink_cu12-12.3.101-py3-none-manylinux1_x86_64.whl (20.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.5/20.5 MB 6.6 MB/s eta 0:00:00
Installing collected packages: triton, nvidia-nvtx-cu12, nvidia-nvjitlink-cu12, nvidia-nccl-cu12, nvidia-curand-cu12, nvidia-cufft-cu12, nvidia-cuda-runtime-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-cupti-cu12, nvidia-cublas-cu12, nvidia-cusparse-cu12, nvidia-cudnn-cu12, nvidia-cusolver-cu12, torch, torchvision, torchaudio
Successfully installed nvidia-cublas-cu12-12.1.3.1 nvidia-cuda-cupti-cu12-12.1.105 nvidia-cuda-nvrtc-cu12-12.1.105 nvidia-cuda-runtime-cu12-12.1.105 nvidia-cudnn-cu12-8.9.2.26 nvidia-cufft-cu12-11.0.2.54 nvidia-curand-cu12-10.3.2.106 nvidia-cusolver-cu12-11.4.5.107 nvidia-cusparse-cu12-12.1.0.106 nvidia-nccl-cu12-2.18.1 nvidia-nvjitlink-cu12-12.3.101 nvidia-nvtx-cu12-12.1.105 torch-2.1.2 torchaudio-2.1.2 torchvision-0.16.2 triton-2.1.0
(opennmt) yekyaw.thu@gpu:~$
```

## Verify Again

```
(opennmt) yekyaw.thu@gpu:~$ python -c "import torch; print(torch.cuda.is_available())"
/home/yekyaw.thu/.conda/envs/opennmt/lib/python3.8/site-packages/torch/cuda/__init__.py:138: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
False
(opennmt) yekyaw.thu@gpu:~$
```

## Try Again  

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
