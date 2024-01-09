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
