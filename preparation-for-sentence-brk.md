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

