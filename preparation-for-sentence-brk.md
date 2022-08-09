sentence breaking experiment လုပ်ဖို့အတွက် ပြင်ဆင်ရာမှာ ဒီတစ်ခါ GPU server က sudo command သုံးလို့မရတဲ့ environment ဖြစ်ပြီးတော့ ပေးထားတဲ့ docker env အောက်မှာပဲ run ရလို့ လက်ဝင်တယ်။ တချို့ marian framework ကို run လို့ရဖို့ လုပ်ခဲ့တုန်းက log ပါ။  

## git clone


```
root@2b3cc0b49af6:/home/tool# git clone https://github.com/marian-nmt/marian
Cloning into 'marian'...
remote: Enumerating objects: 59913, done.
remote: Counting objects: 100% (1834/1834), done.
remote: Compressing objects: 100% (639/639), done.
remote: Total 59913 (delta 1268), reused 1550 (delta 1156), pack-reused 58079
Receiving objects: 100% (59913/59913), 40.26 MiB | 2.10 MiB/s, done.
Resolving deltas: 100% (46069/46069), done.
root@2b3cc0b49af6:/home/tool#
```

## check

```
root@2b3cc0b49af6:/home/tool# cd marian
root@2b3cc0b49af6:/home/tool/marian# ls
CHANGELOG.md    CMakeSettings.json  Doxyfile.in  README.md  azure-pipelines.yml  contrib  examples          scripts  vs
CMakeLists.txt  CONTRIBUTING.md     LICENSE.md   VERSION    build                doc      regression-tests  src
root@2b3cc0b49af6:/home/tool/marian#
```

## no cmake error

```
root@2b3cc0b49af6:/home/tool/marian# mkdir build
root@2b3cc0b49af6:/home/tool/marian# cd build
root@2b3cc0b49af6:/home/tool/marian/build# cmake .. | tee ../../marian-installation.log
bash: cmake: command not found
root@2b3cc0b49af6:/home/tool/marian/build#
```

## cmake installation

```
root@2b3cc0b49af6:/home/tool/marian# apt-get install build-essential libssl-dev
...
...
...
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
build-essential set to manually installed.
Suggested packages:
  libssl-doc
The following NEW packages will be installed:
  libssl-dev
The following packages will be upgraded:
  libssl3
1 upgraded, 1 newly installed, 0 to remove and 81 not upgraded.
Need to get 4270 kB of archives.
After this operation, 12.4 MB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libssl3 amd64 3.0.2-0ubuntu1.6 [1900 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libssl-dev amd64 3.0.2-0ubuntu1.6 [2370 kB]
Fetched 4270 kB in 3s (1586 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
(Reading database ... 30655 files and directories currently installed.)
Preparing to unpack .../libssl3_3.0.2-0ubuntu1.6_amd64.deb ...
Unpacking libssl3:amd64 (3.0.2-0ubuntu1.6) over (3.0.2-0ubuntu1.2) ...
Setting up libssl3:amd64 (3.0.2-0ubuntu1.6) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
Selecting previously unselected package libssl-dev:amd64.
(Reading database ... 30655 files and directories currently installed.)
Preparing to unpack .../libssl-dev_3.0.2-0ubuntu1.6_amd64.deb ...
Unpacking libssl-dev:amd64 (3.0.2-0ubuntu1.6) ...
Setting up libssl-dev:amd64 (3.0.2-0ubuntu1.6) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
```

Check Linux:


```
root@2b3cc0b49af6:/home/tool/marian# uname -a
Linux 2b3cc0b49af6 5.15.0-43-generic #46-Ubuntu SMP Tue Jul 12 10:30:17 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
root@2b3cc0b49af6:/home/tool/marian#
```

Install cmake with apt-get:

```
Preparing to unpack .../0-libuv1_1.43.0-1_amd64.deb ...
Unpacking libuv1:amd64 (1.43.0-1) ...
Selecting previously unselected package libarchive13:amd64.
Preparing to unpack .../1-libarchive13_3.6.0-1ubuntu1_amd64.deb ...
Unpacking libarchive13:amd64 (3.6.0-1ubuntu1) ...
Selecting previously unselected package libjsoncpp25:amd64.
Preparing to unpack .../2-libjsoncpp25_1.9.5-3_amd64.deb ...
Unpacking libjsoncpp25:amd64 (1.9.5-3) ...
Selecting previously unselected package librhash0:amd64.
Preparing to unpack .../3-librhash0_1.4.2-1ubuntu1_amd64.deb ...
Unpacking librhash0:amd64 (1.4.2-1ubuntu1) ...
Selecting previously unselected package dh-elpa-helper.
Preparing to unpack .../4-dh-elpa-helper_2.0.9ubuntu1_all.deb ...
Unpacking dh-elpa-helper (2.0.9ubuntu1) ...
Selecting previously unselected package emacsen-common.
Preparing to unpack .../5-emacsen-common_3.0.4_all.deb ...
Unpacking emacsen-common (3.0.4) ...
Selecting previously unselected package cmake-data.
Preparing to unpack .../6-cmake-data_3.22.1-1ubuntu1_all.deb ...
Unpacking cmake-data (3.22.1-1ubuntu1) ...
Selecting previously unselected package cmake.
Preparing to unpack .../7-cmake_3.22.1-1ubuntu1_amd64.deb ...
Unpacking cmake (3.22.1-1ubuntu1) ...
Setting up libarchive13:amd64 (3.6.0-1ubuntu1) ...
Setting up libuv1:amd64 (1.43.0-1) ...
Setting up emacsen-common (3.0.4) ...
Setting up dh-elpa-helper (2.0.9ubuntu1) ...
Setting up libjsoncpp25:amd64 (1.9.5-3) ...
Setting up librhash0:amd64 (1.4.2-1ubuntu1) ...
Setting up cmake-data (3.22.1-1ubuntu1) ...
Setting up cmake (3.22.1-1ubuntu1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
root@2b3cc0b49af6:/home/tool/marian# apt-get -y install cmake
```

check cmake:

```
Preparing to unpack .../0-libuv1_1.43.0-1_amd64.deb ...
Unpacking libuv1:amd64 (1.43.0-1) ...
Selecting previously unselected package libarchive13:amd64.
Preparing to unpack .../1-libarchive13_3.6.0-1ubuntu1_amd64.deb ...
Unpacking libarchive13:amd64 (3.6.0-1ubuntu1) ...
Selecting previously unselected package libjsoncpp25:amd64.
Preparing to unpack .../2-libjsoncpp25_1.9.5-3_amd64.deb ...
Unpacking libjsoncpp25:amd64 (1.9.5-3) ...
Selecting previously unselected package librhash0:amd64.
Preparing to unpack .../3-librhash0_1.4.2-1ubuntu1_amd64.deb ...
Unpacking librhash0:amd64 (1.4.2-1ubuntu1) ...
Selecting previously unselected package dh-elpa-helper.
Preparing to unpack .../4-dh-elpa-helper_2.0.9ubuntu1_all.deb ...
Unpacking dh-elpa-helper (2.0.9ubuntu1) ...
Selecting previously unselected package emacsen-common.
Preparing to unpack .../5-emacsen-common_3.0.4_all.deb ...
Unpacking emacsen-common (3.0.4) ...
Selecting previously unselected package cmake-data.
Preparing to unpack .../6-cmake-data_3.22.1-1ubuntu1_all.deb ...
Unpacking cmake-data (3.22.1-1ubuntu1) ...
Selecting previously unselected package cmake.
Preparing to unpack .../7-cmake_3.22.1-1ubuntu1_amd64.deb ...
Unpacking cmake (3.22.1-1ubuntu1) ...
Setting up libarchive13:amd64 (3.6.0-1ubuntu1) ...
Setting up libuv1:amd64 (1.43.0-1) ...
Setting up emacsen-common (3.0.4) ...
Setting up dh-elpa-helper (2.0.9ubuntu1) ...
Setting up libjsoncpp25:amd64 (1.9.5-3) ...
Setting up librhash0:amd64 (1.4.2-1ubuntu1) ...
Setting up cmake-data (3.22.1-1ubuntu1) ...
Setting up cmake (3.22.1-1ubuntu1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
root@2b3cc0b49af6:/home/tool/marian# apt-get -y install cmake
```

build for marian:

```
root@2b3cc0b49af6:/home/tool/marian# mkdir build
root@2b3cc0b49af6:/home/tool/marian# cd build
root@2b3cc0b49af6:/home/tool/marian/build# cmake ..
...
...
CMake Warning at CMakeLists.txt:523 (find_package):
  By not providing "FindMKL.cmake" in CMAKE_MODULE_PATH this project has
  asked CMake to find a package configuration file provided by "MKL", but
  CMake did not find one.

  Could not find a package configuration file provided by "MKL" with any of
  the following names:

    MKLConfig.cmake
    mkl-config.cmake

  Add the installation prefix of "MKL" to CMAKE_PREFIX_PATH or set "MKL_DIR"
  to a directory containing one of the above files.  If "MKL" provides a
  separate development package or SDK, be sure it has been installed.


-- Looking for sgemm_
-- Looking for sgemm_ - not found
-- Could NOT find BLAS (missing: BLAS_LIBRARIES)
CMake Error at CMakeLists.txt:634 (include):
  include could not find requested file:

    GetCacheVariables


-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE)
-- Configuring incomplete, errors occurred!
See also "/home/tool/marian/build/CMakeFiles/CMakeOutput.log".
See also "/home/tool/marian/build/CMakeFiles/CMakeError.log".
root@2b3cc0b49af6:/home/tool/marian/build#
```


```
root@2b3cc0b49af6:/home/tool/marian/build# vi CMakeCache.txt
# This is the CMakeCache file.
# For build in directory: /home/tool/marian/build
# It was generated by CMake: /usr/bin/cmake
# You can edit this file to change values found and used by cmake.
# If you do not want to change any of the values, simply exit the editor.
# If you do want to change a value, simply edit, save, and exit the editor.
# The syntax for the file is as follows:
# KEY:TYPE=VALUE
# KEY is the name of a variable in the cache.
# TYPE is a hint to GUIs for the type of VALUE, DO NOT EDIT TYPE!.
# VALUE is the current value for the KEY.

########################
# EXTERNAL cache entries
########################

//Path to a library.
BLAS_Accelerate_LIBRARY:FILEPATH=BLAS_Accelerate_LIBRARY-NOTFOUND

//Path to a library.
BLAS_acml_LIBRARY:FILEPATH=BLAS_acml_LIBRARY-NOTFOUND

//Path to a library.
BLAS_acml_mp_LIBRARY:FILEPATH=BLAS_acml_mp_LIBRARY-NOTFOUND

//Path to a library.
BLAS_armpl_lp64_LIBRARY:FILEPATH=BLAS_armpl_lp64_LIBRARY-NOTFOUND

//Path to a library.
BLAS_blas_LIBRARY:FILEPATH=BLAS_blas_LIBRARY-NOTFOUND
```

because of above error, install lib of openblas as follows:  


```
root@2b3cc0b49af6:/home/tool/marian/build# apt-get -y install libopenblas-dev
...
...
...
Fetched 11.5 MB in 13s (878 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libopenblas0-pthread:amd64.
(Reading database ... 35424 files and directories currently installed.)
Preparing to unpack .../libopenblas0-pthread_0.3.20+ds-1_amd64.deb ...
Unpacking libopenblas0-pthread:amd64 (0.3.20+ds-1) ...
Selecting previously unselected package libopenblas0:amd64.
Preparing to unpack .../libopenblas0_0.3.20+ds-1_amd64.deb ...
Unpacking libopenblas0:amd64 (0.3.20+ds-1) ...
Selecting previously unselected package libopenblas-pthread-dev:amd64.
Preparing to unpack .../libopenblas-pthread-dev_0.3.20+ds-1_amd64.deb ...
Unpacking libopenblas-pthread-dev:amd64 (0.3.20+ds-1) ...
Selecting previously unselected package libopenblas-dev:amd64.
Preparing to unpack .../libopenblas-dev_0.3.20+ds-1_amd64.deb ...
Unpacking libopenblas-dev:amd64 (0.3.20+ds-1) ...
Setting up libopenblas0-pthread:amd64 (0.3.20+ds-1) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so.3 to provide /usr/lib/x86_64-linux-gnu/libblas.so.3 (libblas.so.3-x86_64-linux-gnu) in auto mode
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/liblapack.so.3 to provide /usr/lib/x86_64-linux-gnu/liblapack.so.3 (liblapack.so.3-x86_64-linux-gnu) in auto mode
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/libopenblas.so.0 to provide /usr/lib/x86_64-linux-gnu/libopenblas.so.0 (libopenblas.so.0-x86_64-linux-gnu) in auto mode
Setting up libopenblas0:amd64 (0.3.20+ds-1) ...
Setting up libopenblas-pthread-dev:amd64 (0.3.20+ds-1) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so to provide /usr/lib/x86_64-linux-gnu/libblas.so (libblas.so-x86_64-linux-gnu) in auto mode
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/liblapack.so to provide /usr/lib/x86_64-linux-gnu/liblapack.so (liblapack.so-x86_64-linux-gnu) in auto mode
update-alternatives: using /usr/lib/x86_64-linux-gnu/openblas-pthread/libopenblas.so to provide /usr/lib/x86_64-linux-gnu/libopenblas.so (libopenblas.so-x86_64-linux-gnu) in auto mode
Setting up libopenblas-dev:amd64 (0.3.20+ds-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
```

Also install root@2b3cc0b49af6:/home/tool/marian/build# apt-get install doxygen as follows:  


```
Need to get 48.2 MB of archives.
After this operation, 219 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu jammy/main amd64 libllvm14 amd64 1:14.0.0-1ubuntu1 [24.0 MB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libclang-cpp14 amd64 1:14.0.0-1ubuntu1 [12.1 MB]
Get:3 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libclang1-14 amd64 1:14.0.0-1ubuntu1 [6796 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy/universe amd64 libxapian30 amd64 1.4.18-4 [701 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy/universe amd64 doxygen amd64 1.9.1-2ubuntu2 [4620 kB]
Fetched 48.2 MB in 32s (1485 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libllvm14:amd64.
(Reading database ... 35468 files and directories currently installed.)
Preparing to unpack .../libllvm14_1%3a14.0.0-1ubuntu1_amd64.deb ...
Unpacking libllvm14:amd64 (1:14.0.0-1ubuntu1) ...
Selecting previously unselected package libclang-cpp14.
Preparing to unpack .../libclang-cpp14_1%3a14.0.0-1ubuntu1_amd64.deb ...
Unpacking libclang-cpp14 (1:14.0.0-1ubuntu1) ...
Selecting previously unselected package libclang1-14.
Preparing to unpack .../libclang1-14_1%3a14.0.0-1ubuntu1_amd64.deb ...
Unpacking libclang1-14 (1:14.0.0-1ubuntu1) ...
Selecting previously unselected package libxapian30:amd64.
Preparing to unpack .../libxapian30_1.4.18-4_amd64.deb ...
Unpacking libxapian30:amd64 (1.4.18-4) ...
Selecting previously unselected package doxygen.
Preparing to unpack .../doxygen_1.9.1-2ubuntu2_amd64.deb ...
Unpacking doxygen (1.9.1-2ubuntu2) ...
Setting up libxapian30:amd64 (1.4.18-4) ...
Setting up libllvm14:amd64 (1:14.0.0-1ubuntu1) ...
Setting up libclang1-14 (1:14.0.0-1ubuntu1) ...
Setting up libclang-cpp14 (1:14.0.0-1ubuntu1) ...
Setting up doxygen (1.9.1-2ubuntu2) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
```

install graphviz also:  


```
Selecting previously unselected package libpathplan4:amd64.
Preparing to unpack .../06-libpathplan4_2.42.2-6_amd64.deb ...
Unpacking libpathplan4:amd64 (2.42.2-6) ...
Selecting previously unselected package libgvc6.
Preparing to unpack .../07-libgvc6_2.42.2-6_amd64.deb ...
Unpacking libgvc6 (2.42.2-6) ...
Selecting previously unselected package libgvpr2:amd64.
Preparing to unpack .../08-libgvpr2_2.42.2-6_amd64.deb ...
Unpacking libgvpr2:amd64 (2.42.2-6) ...
Selecting previously unselected package liblab-gamut1:amd64.
Preparing to unpack .../09-liblab-gamut1_2.42.2-6_amd64.deb ...
Unpacking liblab-gamut1:amd64 (2.42.2-6) ...
Selecting previously unselected package graphviz.
Preparing to unpack .../10-graphviz_2.42.2-6_amd64.deb ...
Unpacking graphviz (2.42.2-6) ...
Selecting previously unselected package libgts-bin.
Preparing to unpack .../11-libgts-bin_0.7.6+darcs121130-5_amd64.deb ...
Unpacking libgts-bin (0.7.6+darcs121130-5) ...
Setting up liblab-gamut1:amd64 (2.42.2-6) ...
Setting up libgts-0.7-5:amd64 (0.7.6+darcs121130-5) ...
Setting up libpathplan4:amd64 (2.42.2-6) ...
Setting up libann0 (1.1.2+doc-7build1) ...
Setting up libgd3:amd64 (2.3.0-2ubuntu2) ...
Setting up fonts-liberation (1:1.07.4-11) ...
Setting up libcdt5:amd64 (2.42.2-6) ...
Setting up libcgraph6:amd64 (2.42.2-6) ...
Setting up libgts-bin (0.7.6+darcs121130-5) ...
Setting up libgvc6 (2.42.2-6) ...
Setting up libgvpr2:amd64 (2.42.2-6) ...
Setting up graphviz (2.42.2-6) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for fontconfig (2.13.1-4.2ubuntu5) ...
root@2b3cc0b49af6:/home/tool/marian/build# apt-get install graphviz
```

run cmake again and errors are as follows:  
inside CMakeError.log  

```
Determining if the function sgemm_ exists failed with the following output:  
Change Dir: /home/tool/marian/build/CMakeFiles/CMakeTmp

Run Build Command(s):/usr/bin/gmake -f Makefile cmTC_f3efd/fast && /usr/bin/gmake  -f CMakeFiles/cmTC_f3efd.dir/build.make CMakeFiles/cmTC_f3efd.dir/build
gmake[1]: Entering directory '/home/tool/marian/build/CMakeFiles/CMakeTmp'
Building C object CMakeFiles/cmTC_f3efd.dir/CheckFunctionExists.c.o
/usr/bin/cc   -pthread -Wl,--no-as-needed -fPIC -Wno-unused-result  -march=native  -DCHECK_FUNCTION_EXISTS=sgemm_ -o CMakeFiles/cmTC_f3efd.dir/CheckFunctionExists.c.o -c /usr/share/cmake-3.22/Modules/CheckFunctionExists.c
Linking C executable cmTC_f3efd
/usr/bin/cmake -E cmake_link_script CMakeFiles/cmTC_f3efd.dir/link.txt --verbose=1
/usr/bin/cc -pthread -Wl,--no-as-needed -fPIC -Wno-unused-result  -march=native  -DCHECK_FUNCTION_EXISTS=sgemm_ CMakeFiles/cmTC_f3efd.dir/CheckFunctionExists.c.o -o cmTC_f3efd
/usr/bin/ld: CMakeFiles/cmTC_f3efd.dir/CheckFunctionExists.c.o: in function `main':
CheckFunctionExists.c:(.text+0x14): undefined reference to `sgemm_'
collect2: error: ld returned 1 exit status
gmake[1]: *** [CMakeFiles/cmTC_f3efd.dir/build.make:99: cmTC_f3efd] Error 1
gmake[1]: Leaving directory '/home/tool/marian/build/CMakeFiles/CMakeTmp'
gmake: *** [Makefile:127: cmTC_f3efd/fast] Error 2
```

I think I have to solve this ERROR: "Determining if the function sgemm_ exists failed".  
Actually, that error is relating to BLAS...  

When I log the running output with tee command, I noticed following errors:  


```
1)
-- Detecting C compile features - done
CMake Error at CMakeLists.txt:68 (include):
  include could not find requested file:

    GetVersionFromFile

2)
-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
CMake Error at CMakeLists.txt:152 (include):
  include could not find requested file:

    FindSSE

3)
-- Found BLAS: /usr/lib/x86_64-linux-gnu/libopenblas.so
CMake Error at CMakeLists.txt:534 (include):
  include could not find requested file:

    FindCBLAS


CMake Error at CMakeLists.txt:634 (include):
  include could not find requested file:

    GetCacheVariables

```

## Pulling Docker Image of Marian Framework


```
ye@lst-gpu-server-197:~/docker-image$ docker pull intel/nmt_marian_framework_demo
Using default tag: latest
latest: Pulling from intel/nmt_marian_framework_demo
e703a715e88d: Pull complete
23691a51b8ef: Pull complete
3b0b30fd7bda: Pull complete
4d729a10ad9b: Pull complete
4709d7bf584a: Pull complete
64cdf3c6fc15: Pull complete
118c4c11cc70: Pull complete
e49f1fdbefad: Pull complete
f3590a1a996d: Pull complete
f856d69186c0: Pull complete
bfbe6c5a596d: Pull complete
0b7ab3529f01: Pull complete
c33617f8aca5: Pull complete
190cca65d218: Pull complete
fd5f80da1c3f: Pull complete
Digest: sha256:0f538f8d468a068e2290b1d61c2936c9758f06c36cabc86ab212141ead143028
Status: Downloaded newer image for intel/nmt_marian_framework_demo:latest
docker.io/intel/nmt_marian_framework_demo:latest
ye@lst-gpu-server-197:~/docker-image$
```

## Check the downloaded images

```
ye@lst-gpu-server-197:~/docker-image$ docker ps
CONTAINER ID   IMAGE                                  COMMAND       CREATED        STATUS       PORTS     NAMES
2b3cc0b49af6   nvidia/cuda:11.7.0-devel-ubuntu22.04   "/bin/bash"   44 hours ago   Up 6 hours             ylst
ye@lst-gpu-server-197:~/docker-image$ docker images
REPOSITORY                        TAG                          IMAGE ID       CREATED         SIZE
nvidia/cuda                       11.7.0-devel-ubuntu22.04     dbfe75619692   2 months ago    4.54GB
nvidia/cuda                       11.7.0-runtime-ubuntu22.04   ac9074e02625   2 months ago    1.88GB
nvidia/cuda                       11.7.0-base-ubuntu22.04      d7f6a127140e   2 months ago    214MB
intel/nmt_marian_framework_demo   latest                       827326ffd56a   10 months ago   1.82GB
nvidia/cuda                       10.0-base                    97cca2bac989   13 months ago   109MB
nvidia/cuda                       10.2-base                    55c80b56bbcd   13 months ago   107MB
nvidia/cuda                       11.1-base                    287475453634   20 months ago   124MB
nvidia/cuda                       11.0-base                    2ec708416bb8   23 months ago   122MB
ye@lst-gpu-server-197:~/docker-image$
```

## Testing Pulled Image

```
ye@lst-gpu-server-197:~$ docker run 827326ffd56a
Please review the following licenses & disclaimers:
Helper scripts: /nmt/license.txt
Marian license: /nmt/marian/license.txt
Pre-trained model discalimer: /nmt/discalimer.txt
Pre-trained model license: /nmt/model/licesne.txt

Starting latency test...
Traceback (most recent call last):
  File "/nmt/runme.py", line 183, in <module>
    subprocess.check_output([PPREFIX+MARIAN_BIN, '-i', PPREFIX+INPUT_DATA, '-o', PPREFIX+WORKDIR+'/translated.out'] + flagsLatency.split())
  File "/usr/lib/python3.9/subprocess.py", line 424, in check_output
    return run(*popenargs, stdout=PIPE, timeout=timeout, check=True,
  File "/usr/lib/python3.9/subprocess.py", line 528, in run
    raise CalledProcessError(retcode, process.args,
subprocess.CalledProcessError: Command '['/nmt/marian/marian-decoder', '-i', '/nmt/data/input_en.txt', '-o', '/tmp/marian/translated.out', '-m', '/nmt/model/model-finetune.intgemm.alphas.2021.bin', '--gemm-type', 'intgemm8', '--beam-size=1', '--mini-batch=1', '--maxi-batch=1', '--maxi-batch-sort', 'src', '-w', '512', '--skip-cost', '--cpu-threads', '2', '--quiet', '--quiet-translation', '-v', '/nmt/model/vocab.spm', '/nmt/model/vocab.spm', '--shortlist', '/nmt/model/lex.s2t.50.bin', 'false', '--log-level', 'off', '--intgemm-options', 'shifted', 'all-shifted', 'precomputed-alpha']' died with <Signals.SIGILL: 4>.
ye@lst-gpu-server-197:~$
```

## Try to Install on Another GPU Server

```
yekyaw.thu@gpu:~$ mkdir tool
yekyaw.thu@gpu:~$ cd tool
yekyaw.thu@gpu:~/tool$ apt-get install git cmake build-essential
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
yekyaw.thu@gpu:~/tool$ sudo apt-get install git cmake build-essential
[sudo] password for yekyaw.thu: 
Sorry, try again.
[sudo] password for yekyaw.thu: 
sudo: 1 incorrect password attempt
```

```
yekyaw.thu@gpu:~/tool$ git clone https://github.com/marian-nmt/marian
Cloning into 'marian'...
remote: Enumerating objects: 59913, done.
remote: Counting objects: 100% (1834/1834), done.
remote: Compressing objects: 100% (639/639), done.
remote: Total 59913 (delta 1268), reused 1550 (delta 1156), pack-reused 58079
Receiving objects: 100% (59913/59913), 40.26 MiB | 16.73 MiB/s, done.
Resolving deltas: 100% (46069/46069), done.
```

```
yekyaw.thu@gpu:~/tool$ cd marian/
yekyaw.thu@gpu:~/tool/marian$ ls
CHANGELOG.md	CMakeSettings.json  Doxyfile.in  README.md  azure-pipelines.yml  contrib  examples	    scripts  vs
CMakeLists.txt	CONTRIBUTING.md     LICENSE.md	 VERSION    cmake		 doc	  regression-tests  src
```

```
yekyaw.thu@gpu:~/tool/marian$ mkdir build
yekyaw.thu@gpu:~/tool/marian$ cd build
```

```
yekyaw.thu@gpu:~/tool/marian/build$ cmake ..
-- The CXX compiler identification is GNU 9.4.0
-- The C compiler identification is GNU 9.4.0
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Project name: marian
-- Project version: v1.11.0+f00d0621
Submodule 'examples' (https://github.com/marian-nmt/marian-examples) registered for path 'examples'
Submodule 'regression-tests' (https://github.com/marian-nmt/marian-regression-tests) registered for path 'regression-tests'
Submodule 'src/3rd_party/fbgemm' (https://github.com/marian-nmt/FBGEMM) registered for path 'src/3rd_party/fbgemm'
Submodule 'src/3rd_party/intgemm' (https://github.com/marian-nmt/intgemm/) registered for path 'src/3rd_party/intgemm'
Submodule 'src/3rd_party/nccl' (https://github.com/marian-nmt/nccl) registered for path 'src/3rd_party/nccl'
Submodule 'src/3rd_party/sentencepiece' (https://github.com/marian-nmt/sentencepiece) registered for path 'src/3rd_party/sentencepiece'
Submodule 'src/3rd_party/simple-websocket-server' (https://github.com/marian-nmt/Simple-WebSocket-Server) registered for path 'src/3rd_party/simple-websocket-server'
Cloning into '/home/yekyaw.thu/tool/marian/examples'...
Cloning into '/home/yekyaw.thu/tool/marian/regression-tests'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/fbgemm'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/intgemm'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/nccl'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/sentencepiece'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/simple-websocket-server'...
Submodule path 'examples': checked out '6d5921cc7de91f4e915b59e9c52c9a76c4e99b00'
Submodule path 'regression-tests': checked out '0716f4e012d1e3f7543bffa8aecc97ce9c903e17'
Submodule path 'src/3rd_party/fbgemm': checked out '6f45243cb8ab7d7ab921af18d313ae97144618b8'
Submodule 'third_party/asmjit' (https://github.com/asmjit/asmjit.git) registered for path 'src/3rd_party/fbgemm/third_party/asmjit'
Submodule 'third_party/cpuinfo' (https://github.com/pytorch/cpuinfo) registered for path 'src/3rd_party/fbgemm/third_party/cpuinfo'
Submodule 'third_party/googletest' (https://github.com/google/googletest) registered for path 'src/3rd_party/fbgemm/third_party/googletest'
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/fbgemm/third_party/asmjit'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/fbgemm/third_party/cpuinfo'...
Cloning into '/home/yekyaw.thu/tool/marian/src/3rd_party/fbgemm/third_party/googletest'...
Submodule path 'src/3rd_party/fbgemm/third_party/asmjit': checked out '4da474ac9aa2689e88d5e40a2f37628f302d7e3c'
Submodule path 'src/3rd_party/fbgemm/third_party/cpuinfo': checked out 'd5e37adf1406cf899d7d9ec1d317c47506ccb970'
Submodule path 'src/3rd_party/fbgemm/third_party/googletest': checked out '0fc5466dbb9e623029b1ada539717d10bd45e99e'
Submodule path 'src/3rd_party/intgemm': checked out '8abde25b13c3ab210c0dec8e23f4944e3953812d'
Submodule path 'src/3rd_party/nccl': checked out '5dcf7751494f9d04057bfc6b4a2b64611bc12253'
Submodule path 'src/3rd_party/sentencepiece': checked out 'c307b874deb5ea896db8f93506e173353e66d4d3'
Submodule path 'src/3rd_party/simple-websocket-server': checked out '1d7e84aeb3f1ebdc78f6965d79ad3ca3003789fe'
CMake Warning at CMakeLists.txt:79 (message):
  CMAKE_BUILD_TYPE not set; setting to Release


-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
-- Could not find hardware support for AVX512 on this machine.
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Compiling code for Pascal GPUs
-- Compiling code for Volta GPUs
-- Compiling code for Turing GPUs
-- Found CUDA libraries: /usr/lib/x86_64-linux-gnu/libcurand.so;/usr/lib/x86_64-linux-gnu/libcusparse.so;/usr/lib/x86_64-linux-gnu/libcublas.so
-- Not Found Tcmalloc
CMake Warning at CMakeLists.txt:500 (message):
  Cannot find TCMalloc library.  Continuing.


-- Found MKL: -Wl,--start-group;/opt/intel/mkl/lib/intel64/libmkl_intel_ilp64.a;/opt/intel/mkl/lib/intel64/libmkl_sequential.a;/opt/intel/mkl/lib/intel64/libmkl_core.a;-Wl,--end-group  
-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Configuring done
-- Generating done
-- Build files have been written to: /home/yekyaw.thu/tool/marian/build
yekyaw.thu@gpu:~/tool/marian/build$
```

## Check CPU Info

```
yekyaw.thu@gpu:~/tool/marian/build$ cat /proc/cpuinfo
processor	: 0
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.103
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 0
cpu cores	: 12
apicid		: 0
initial apicid	: 0
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 1
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.212
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 1
cpu cores	: 12
apicid		: 2
initial apicid	: 2
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 2
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 4008.343
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 2
cpu cores	: 12
apicid		: 4
initial apicid	: 4
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 3
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.441
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 4
cpu cores	: 12
apicid		: 8
initial apicid	: 8
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 4
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.441
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 5
cpu cores	: 12
apicid		: 10
initial apicid	: 10
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 5
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.444
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 6
cpu cores	: 12
apicid		: 12
initial apicid	: 12
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 6
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.453
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 0
cpu cores	: 12
apicid		: 16
initial apicid	: 16
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 7
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.443
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 1
cpu cores	: 12
apicid		: 18
initial apicid	: 18
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 8
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.443
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 2
cpu cores	: 12
apicid		: 20
initial apicid	: 20
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 9
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.443
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 4
cpu cores	: 12
apicid		: 24
initial apicid	: 24
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 10
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.442
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 5
cpu cores	: 12
apicid		: 26
initial apicid	: 26
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 11
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.441
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 6
cpu cores	: 12
apicid		: 28
initial apicid	: 28
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 12
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.440
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 0
cpu cores	: 12
apicid		: 1
initial apicid	: 1
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 13
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.440
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 1
cpu cores	: 12
apicid		: 3
initial apicid	: 3
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 14
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.439
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 2
cpu cores	: 12
apicid		: 5
initial apicid	: 5
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 15
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3998.621
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 4
cpu cores	: 12
apicid		: 9
initial apicid	: 9
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 16
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3998.998
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 5
cpu cores	: 12
apicid		: 11
initial apicid	: 11
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 17
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.369
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 6
cpu cores	: 12
apicid		: 13
initial apicid	: 13
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 18
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.428
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 0
cpu cores	: 12
apicid		: 17
initial apicid	: 17
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 19
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.133
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 1
cpu cores	: 12
apicid		: 19
initial apicid	: 19
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 20
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.442
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 2
cpu cores	: 12
apicid		: 21
initial apicid	: 21
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 21
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.361
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 4
cpu cores	: 12
apicid		: 25
initial apicid	: 25
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 22
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 3999.441
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 5
cpu cores	: 12
apicid		: 27
initial apicid	: 27
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

processor	: 23
vendor_id	: AuthenticAMD
cpu family	: 23
model		: 8
model name	: AMD Ryzen Threadripper 2920X 12-Core Processor
stepping	: 2
microcode	: 0x800820d
cpu MHz		: 4054.602
cache size	: 512 KB
physical id	: 0
siblings	: 24
core id		: 6
cpu cores	: 12
apicid		: 29
initial apicid	: 29
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid amd_dcm aperfmperf pni pclmulqdq monitor ssse3 fma cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev ibpb vmmcall fsgsbase bmi1 avx2 smep bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
bugs		: sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips	: 6999.02
TLB size	: 2560 4K pages
clflush size	: 64
cache_alignment	: 64
address sizes	: 43 bits physical, 48 bits virtual
power management: ts ttp tm hwpstate cpb eff_freq_ro [13] [14]

yekyaw.thu@gpu:~/tool/marian/build$ 
```

## make

```
yekyaw.thu@gpu:~/tool/marian/build$ make -j21
Scanning dependencies of target faiss
Scanning dependencies of target libyaml-cpp
Scanning dependencies of target marian_version
Scanning dependencies of target SQLiteCpp
Scanning dependencies of target zlib
Scanning dependencies of target sentencepiece-static
Scanning dependencies of target sentencepiece_train-static
Scanning dependencies of target pathie-cpp
Scanning dependencies of target intgemm
Scanning dependencies of target nccl_install
[  0%] Generating ../../src/common/git_revision.h
[  0%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/adler32.c.o
[  0%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/compress.c.o
[  0%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/Heap.cpp.o
[  0%] Creating directories for 'nccl_install'
[  1%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/crc32.c.o
[  1%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/deflate.c.o
[  2%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/VectorTransform.cpp.o
[  3%] Building CXX object src/3rd_party/intgemm/CMakeFiles/intgemm.dir/intgemm/intgemm.cc.o
[  3%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzlib.c.o
[  3%] Built target marian_version
[  3%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/hamming.cpp.o
[  4%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzclose.c.o
[  5%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/entry_iterator.cpp.o
[  6%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/misc.cpp.o
[  6%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/errors.cpp.o
[  7%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/contrib/graphbuilder.cpp.o
[  7%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/contrib/graphbuilderadapter.cpp.o
[  7%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/binary_renamed.cpp.o
[  8%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/path.cpp.o
[  9%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/builder.cc.o
[ 10%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arena.cc.o
[ 10%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Backup.cpp.o
[ 10%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arenastring.cc.o
[ 10%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzread.c.o
[ 11%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzwrite.c.o
[ 11%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/infback.c.o
[ 11%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
[ 12%] No download step for 'nccl_install'
[ 13%] No patch step for 'nccl_install'
[ 14%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inffast.c.o
[ 14%] No update step for 'nccl_install'
[ 14%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie.cpp.o
[ 14%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/random.cpp.o
[ 15%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
[ 16%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/convert.cpp.o
[ 16%] No configure step for 'nccl_install'
[ 16%] Performing build step for 'nccl_install'
[ 16%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inflate.c.o
[ 16%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Column.cpp.o
[ 16%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/directives.cpp.o
[ 16%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inftrees.c.o
[ 17%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/trees.c.o
[ 17%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/uncompr.c.o
[ 17%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/bytestream.cc.o
[ 17%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie_ifstream.cpp.o
Generating nccl.h.in                           > /home/yekyaw.thu/tool/marian/build/local/include/nccl.h
Grabbing   include/nccl_net.h                  > /home/yekyaw.thu/tool/marian/build/local/include/nccl_net.h
[ 18%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/zutil.c.o
[ 18%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emit.cpp.o
Generating nccl.pc.in                          > /home/yekyaw.thu/tool/marian/build/local/lib/pkgconfig/nccl.pc
Compiling  init.cc                             > /home/yekyaw.thu/tool/marian/build/local/obj/init.o
Compiling  channel.cc                          > /home/yekyaw.thu/tool/marian/build/local/obj/channel.o
[ 19%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie_ofstream.cpp.o
[ 20%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Database.cpp.o
[ 20%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/temp.cpp.o
[ 21%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitfromevents.cpp.o
[ 22%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/coded_stream.cc.o
Compiling  bootstrap.cc                        > /home/yekyaw.thu/tool/marian/build/local/obj/bootstrap.o
[ 22%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitter.cpp.o
[ 22%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Exception.cpp.o
[ 23%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitterstate.cpp.o
[ 23%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/common.cc.o
[ 23%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitterutils.cpp.o
[ 24%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 24%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/exceptions.cpp.o
[ 24%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Statement.cpp.o
[ 25%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/exp.cpp.o
[ 25%] Built target zlib
[ 25%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/memory.cpp.o
[ 25%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[ 26%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/node_data.cpp.o
[ 26%] Linking CXX static library libintgemm.a
Compiling  transport.cc                        > /home/yekyaw.thu/tool/marian/build/local/obj/transport.o
Compiling  enqueue.cc                          > /home/yekyaw.thu/tool/marian/build/local/obj/enqueue.o
[ 26%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/nodebuilder.cpp.o
[ 26%] Built target intgemm
Compiling  group.cc                            > /home/yekyaw.thu/tool/marian/build/local/obj/group.o
Compiling  debug.cc                            > /home/yekyaw.thu/tool/marian/build/local/obj/debug.o
[ 27%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Transaction.cpp.o
Compiling  proxy.cc                            > /home/yekyaw.thu/tool/marian/build/local/obj/proxy.o
[ 27%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/nodeevents.cpp.o
Compiling  misc/nvmlwrap.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/misc/nvmlwrap.o
[ 27%] Building C object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/sqlite3/sqlite3.c.o
[ 27%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 27%] Built target pathie-cpp
Compiling  misc/ibvwrap.cc                     > /home/yekyaw.thu/tool/marian/build/local/obj/misc/ibvwrap.o
Compiling  misc/utils.cc                       > /home/yekyaw.thu/tool/marian/build/local/obj/misc/utils.o
Compiling  misc/argcheck.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/misc/argcheck.o
Compiling  transport/p2p.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/transport/p2p.o
[ 28%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/null.cpp.o
Compiling  transport/shm.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/transport/shm.o
[ 28%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 28%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/ostream_wrapper.cpp.o
[ 28%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/parse.cpp.o
Compiling  transport/net.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/transport/net.o
[ 29%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/parser.cpp.o
Compiling  transport/net_socket.cc             > /home/yekyaw.thu/tool/marian/build/local/obj/transport/net_socket.o
Compiling  transport/net_ib.cc                 > /home/yekyaw.thu/tool/marian/build/local/obj/transport/net_ib.o
Compiling  transport/coll_net.cc               > /home/yekyaw.thu/tool/marian/build/local/obj/transport/coll_net.o
[ 29%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/regex_yaml.cpp.o
Compiling  collectives/sendrecv.cc             > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/sendrecv.o
Compiling  collectives/all_reduce.cc           > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/all_reduce.o
Compiling  collectives/all_gather.cc           > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/all_gather.o
[ 30%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanner.cpp.o
[ 30%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanscalar.cpp.o
[ 30%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantag.cpp.o
[ 31%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantoken.cpp.o
Compiling  collectives/broadcast.cc            > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/broadcast.o
[ 31%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/simplekey.cpp.o
Compiling  collectives/reduce.cc               > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/reduce.o
Compiling  collectives/reduce_scatter.cc       > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/reduce_scatter.o
[ 32%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 32%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/int128.cc.o
[ 33%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/singledocparser.cpp.o
[ 33%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[ 34%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 34%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 34%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 34%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/stream.cpp.o
[ 35%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/status.cc.o
[ 35%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/tag.cpp.o
[ 35%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 36%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/yaml-node.cpp.o
[ 36%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringpiece.cc.o
Compiling  graph/topo.cc                       > /home/yekyaw.thu/tool/marian/build/local/obj/graph/topo.o
[ 37%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[ 37%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
Compiling  graph/paths.cc                      > /home/yekyaw.thu/tool/marian/build/local/obj/graph/paths.o
Compiling  graph/search.cc                     > /home/yekyaw.thu/tool/marian/build/local/obj/graph/search.o
[ 38%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringprintf.cc.o
Compiling  graph/connect.cc                    > /home/yekyaw.thu/tool/marian/build/local/obj/graph/connect.o
[ 38%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 39%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 39%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
[ 39%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/time.cc.o
[ 40%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
Compiling  graph/rings.cc                      > /home/yekyaw.thu/tool/marian/build/local/obj/graph/rings.o
[ 40%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 41%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
Compiling  graph/trees.cc                      > /home/yekyaw.thu/tool/marian/build/local/obj/graph/trees.o
[ 41%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 42%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece.pb.cc.o
[ 42%] Built target faiss
[ 42%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 42%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/bpe_model.cc.o
Compiling  graph/tuning.cc                     > /home/yekyaw.thu/tool/marian/build/local/obj/graph/tuning.o
Compiling  graph/xml.cc                        > /home/yekyaw.thu/tool/marian/build/local/obj/graph/xml.o
[ 43%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/char_model.cc.o
[ 43%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/error.cc.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/filesystem.cc.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/init.cc.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/model_factory.cc.o
Generating rules                               > /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/Makefile.rules
[ 45%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/model_interface.cc.o
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
[ 45%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/normalizer.cc.o
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/case_encoder.cc.o
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/sendrecv.dep] Error 1
make[4]: *** [Makefile:50: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/colldevice.a] Error 2
make[4]: *** Waiting for unfinished jobs....
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/sentencepiece_processor.cc.o
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/unigram_model.cc.o
[ 47%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/util.cc.o
[ 47%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 47%] Built target libyaml-cpp
[ 48%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 48%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
make[3]: *** [/home/yekyaw.thu/tool/marian/src/3rd_party/nccl/Makefile:25: src.build] Error 2
make[2]: *** [src/3rd_party/CMakeFiles/nccl_install.dir/build.make:112: src/3rd_party/nccl_install-prefix/src/nccl_install-stamp/nccl_install-build] Error 2
make[1]: *** [CMakeFiles/Makefile2:697: src/3rd_party/CMakeFiles/nccl_install.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
[ 48%] Linking CXX static library libsentencepiece.a
[ 48%] Built target sentencepiece-static
[ 49%] Linking CXX static library libsentencepiece_train.a
[ 49%] Built target sentencepiece_train-static
[ 49%] Built target SQLiteCpp
make: *** [Makefile:152: all] Error 2
yekyaw.thu@gpu:~/tool/marian/build$ make -j21
```

ဒီစက်မှာလည်း အဆင်မပြေဘူး ....   
အဓိက ပြဿနာပေးတာက အောက်ပါအတိုင်းလို့ ယူဆခဲ့ ...  

```
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
```


