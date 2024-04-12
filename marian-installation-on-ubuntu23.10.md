# Installation of Marian on New OS Installed GPU Machine

Date: 12 Apr 2024  

## Error with cmake ..

```
ye@lst-hpc3090:~/tool/marian/build$ cmake ..
-- Project name: marian
-- Project version: v1.12.0+65bf82ff
CMake Warning at CMakeLists.txt:79 (message):
  CMAKE_BUILD_TYPE not set; setting to Release


-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
-- Could not find hardware support for AVX512 on this machine.
CMake Warning (dev) at CMakeLists.txt:308 (find_package):
  Policy CMP0146 is not set: The FindCUDA module is removed.  Run "cmake
  --help-policy CMP0146" for policy details.  Use the cmake_policy command to
  set the policy and suppress this warning.

This warning is for project developers.  Use -Wno-dev to suppress it.

-- Compiling code for Pascal GPUs
-- Compiling code for Volta GPUs
-- Compiling code for Turing GPUs
-- Compiling code for Ampere GPUs
-- Compiling code for Ampere RTX GPUs
CMake Error at CMakeLists.txt:415 (message):
  cuBLASLt library not found


-- Configuring incomplete, errors occurred!
ye@lst-hpc3090:~/tool/marian/build$
```

## Solution

I updated the CMakeLists.txt file (Check around line no. 413) as follows:  

```
    if ((CUDA_VERSION VERSION_EQUAL "11.0" OR CUDA_VERSION VERSION_GREATER "11.0"))
      #find_library(CUDA_cublasLt_LIBRARY NAMES cublasLt PATHS ${CUDA_TOOLKIT_ROOT_DIR}/lib64 ${CUDA_TOOLKIT_ROOT_DIR}/lib/x64 NO_DEFAULT_PATH)
      find_library(CUDA_cublasLt_LIBRARY NAMES libcublasLt.so PATHS /usr/lib/x86_64-linux-gnu/ NO_DEFAULT_PATH)
```

## cmake Again

```
ye@lst-hpc3090:~/tool/marian/build$ cmake ..
-- Project name: marian
-- Project version: v1.12.0+65bf82ff
CMake Warning at CMakeLists.txt:79 (message):
  CMAKE_BUILD_TYPE not set; setting to Release


-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
-- Could not find hardware support for AVX512 on this machine.
CMake Warning (dev) at CMakeLists.txt:308 (find_package):
  Policy CMP0146 is not set: The FindCUDA module is removed.  Run "cmake
  --help-policy CMP0146" for policy details.  Use the cmake_policy command to
  set the policy and suppress this warning.

This warning is for project developers.  Use -Wno-dev to suppress it.

-- Compiling code for Pascal GPUs
-- Compiling code for Volta GPUs
-- Compiling code for Turing GPUs
-- Compiling code for Ampere GPUs
-- Compiling code for Ampere RTX GPUs
-- Found CUDA libraries: /usr/lib/x86_64-linux-gnu/libcurand.so;/usr/lib/x86_64-linux-gnu/libcusparse.so;/usr/lib/x86_64-linux-gnu/libcublas.so;/usr/lib/x86_64-linux-gnu/libcublasLt.so
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find MKL (missing: MKL_LIBRARIES MKL_INCLUDE_DIRS MKL_INTERFACE_LIBRARY MKL_SEQUENTIAL_LAYER_LIBRARY MKL_CORE_LIBRARY) 
-- Looking for sgemm_
-- Looking for sgemm_ - not found
-- Could NOT find BLAS (missing: BLAS_LIBRARIES) 
CMake Deprecation Warning at src/3rd_party/sentencepiece/CMakeLists.txt:15 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Configuring done (0.9s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ye/tool/marian/build
ye@lst-hpc3090:~/tool/marian/build$ 
```

## sudo make Error

```
Generating rules                               > /home/ye/tool/marian/build/local/obj/collectives/device/Makefile.rules
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:132:2: error: #error -- unsupported GNU version! gcc versions later than 12 are not supported! The nvcc flag '-allow-unsupported-compiler' can be used to override this version check; however, using an unsupported host compiler may cause compilation failure or incorrect run time execution. Use at your own risk.
  132 | #error -- unsupported GNU version! gcc versions later than 12 are not supported! The nvcc flag '-allow-unsupported-compiler' can be used to override this version check; however, using an unsupported host compiler may cause compilation failure or incorrect run time execution. Use at your own risk.
      |  ^~~~~
make[5]: *** [Makefile:53: /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv.dep] Error 1
make[4]: *** [Makefile:50: /home/ye/tool/marian/build/local/obj/collectives/device/colldevice.a] Error 2
make[4]: *** Waiting for unfinished jobs....
[ 44%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/regex_yaml.cpp.o
[ 45%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanner.cpp.o
[ 45%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanscalar.cpp.o
[ 45%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantag.cpp.o
[ 46%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantoken.cpp.o
[ 46%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/simplekey.cpp.o
[ 47%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/singledocparser.cpp.o
[ 47%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/stream.cpp.o
[ 47%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/tag.cpp.o
[ 48%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/yaml-node.cpp.o
make[3]: *** [/home/ye/tool/marian/src/3rd_party/nccl/Makefile:25: src.build] Error 2
make[2]: *** [src/3rd_party/CMakeFiles/nccl_install.dir/build.make:86: src/3rd_party/nccl_install-prefix/src/nccl_install-stamp/nccl_install-build] Error 2
make[1]: *** [CMakeFiles/Makefile2:633: src/3rd_party/CMakeFiles/nccl_install.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
[ 48%] Linking CXX static library libsentencepiece.a
[ 48%] Built target sentencepiece-static
[ 48%] Built target libyaml-cpp
[ 48%] Built target faiss
/home/ye/tool/marian/src/3rd_party/SQLiteCpp/sqlite3/sqlite3.c: In function ‘sqlite3SelectNew’:
/home/ye/tool/marian/src/3rd_party/SQLiteCpp/sqlite3/sqlite3.c:117589:10: warning: function may return address of local variable [-Wreturn-local-addr]
117589 |   return pNew;
       |          ^~~~
/home/ye/tool/marian/src/3rd_party/SQLiteCpp/sqlite3/sqlite3.c:117550:10: note: declared here
117550 |   Select standin;
       |          ^~~~~~~
/home/ye/tool/marian/src/3rd_party/SQLiteCpp/sqlite3/sqlite3.c:117550:10: note: declared here
[ 49%] Linking CXX static library libsentencepiece_train.a
[ 49%] Built target sentencepiece_train-static
[ 49%] Built target SQLiteCpp
make: *** [Makefile:156: all] Error 2
ye@lst-hpc3090:~/tool/marian/build$ 
```

## Install Different Versions of GCC

```
ye@lst-hpc3090:~/tool/marian/build$ sudo apt install gcc-9 g++-9 gcc-12 g++-12
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
gcc-12 is already the newest version (12.3.0-9ubuntu2).
gcc-12 set to manually installed.
g++-12 is already the newest version (12.3.0-9ubuntu2).
g++-12 set to manually installed.
The following additional packages will be installed:
  cpp-9 gcc-11-base gcc-9-base libasan5 libgcc-9-dev libstdc++-9-dev libtsan0
Suggested packages:
  gcc-9-locales g++-9-multilib gcc-9-doc gcc-9-multilib libstdc++-9-doc
The following NEW packages will be installed:
  cpp-9 g++-9 gcc-11-base gcc-9 gcc-9-base libasan5 libgcc-9-dev libstdc++-9-dev libtsan0
0 upgraded, 9 newly installed, 0 to remove and 12 not upgraded.
Need to get 43.2 MB of archives.
After this operation, 145 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 gcc-9-base amd64 9.5.0-4ubuntu2 [30.9 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 cpp-9 amd64 9.5.0-4ubuntu2 [10.5 MB]
Get:3 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 libasan5 amd64 9.5.0-4ubuntu2 [3,106 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu mantic/main amd64 gcc-11-base amd64 11.4.0-4ubuntu1 [42.8 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu mantic/main amd64 libtsan0 amd64 11.4.0-4ubuntu1 [2,268 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 libgcc-9-dev amd64 9.5.0-4ubuntu2 [2,479 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 gcc-9 amd64 9.5.0-4ubuntu2 [11.2 MB]
Get:8 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 libstdc++-9-dev amd64 9.5.0-4ubuntu2 [1,809 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu mantic/universe amd64 g++-9 amd64 9.5.0-4ubuntu2 [11.8 MB]
Fetched 43.2 MB in 4s (10.2 MB/s)
Selecting previously unselected package gcc-9-base:amd64.
(Reading database ... 230933 files and directories currently installed.)
Preparing to unpack .../0-gcc-9-base_9.5.0-4ubuntu2_amd64.deb ...
Unpacking gcc-9-base:amd64 (9.5.0-4ubuntu2) ...
Selecting previously unselected package cpp-9.
Preparing to unpack .../1-cpp-9_9.5.0-4ubuntu2_amd64.deb ...
Unpacking cpp-9 (9.5.0-4ubuntu2) ...
Selecting previously unselected package libasan5:amd64.
Preparing to unpack .../2-libasan5_9.5.0-4ubuntu2_amd64.deb ...
Unpacking libasan5:amd64 (9.5.0-4ubuntu2) ...
Selecting previously unselected package gcc-11-base:amd64.
Preparing to unpack .../3-gcc-11-base_11.4.0-4ubuntu1_amd64.deb ...
Unpacking gcc-11-base:amd64 (11.4.0-4ubuntu1) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../4-libtsan0_11.4.0-4ubuntu1_amd64.deb ...
Unpacking libtsan0:amd64 (11.4.0-4ubuntu1) ...
Selecting previously unselected package libgcc-9-dev:amd64.
Preparing to unpack .../5-libgcc-9-dev_9.5.0-4ubuntu2_amd64.deb ...
Unpacking libgcc-9-dev:amd64 (9.5.0-4ubuntu2) ...
Selecting previously unselected package gcc-9.
Preparing to unpack .../6-gcc-9_9.5.0-4ubuntu2_amd64.deb ...
Unpacking gcc-9 (9.5.0-4ubuntu2) ...
Selecting previously unselected package libstdc++-9-dev:amd64.
Preparing to unpack .../7-libstdc++-9-dev_9.5.0-4ubuntu2_amd64.deb ...
Unpacking libstdc++-9-dev:amd64 (9.5.0-4ubuntu2) ...
Selecting previously unselected package g++-9.
Preparing to unpack .../8-g++-9_9.5.0-4ubuntu2_amd64.deb ...
Unpacking g++-9 (9.5.0-4ubuntu2) ...
Setting up gcc-11-base:amd64 (11.4.0-4ubuntu1) ...
Setting up gcc-9-base:amd64 (9.5.0-4ubuntu2) ...
Setting up libtsan0:amd64 (11.4.0-4ubuntu1) ...
Setting up libasan5:amd64 (9.5.0-4ubuntu2) ...
Setting up cpp-9 (9.5.0-4ubuntu2) ...
Setting up libgcc-9-dev:amd64 (9.5.0-4ubuntu2) ...
Setting up gcc-9 (9.5.0-4ubuntu2) ...
Setting up libstdc++-9-dev:amd64 (9.5.0-4ubuntu2) ...
Setting up g++-9 (9.5.0-4ubuntu2) ...
Processing triggers for man-db (2.11.2-3) ...
Processing triggers for libc-bin (2.38-1ubuntu6.1) ...
ye@lst-hpc3090:~/tool/marian/build$ 
```

## Setup Alternatives

```
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 90
update-alternatives: using /usr/bin/gcc-9 to provide /usr/bin/gcc (gcc) in auto mode
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 90
update-alternatives: using /usr/bin/g++-9 to provide /usr/bin/g++ (g++) in auto mode
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 120
update-alternatives: using /usr/bin/gcc-12 to provide /usr/bin/gcc (gcc) in auto mode
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 120
update-alternatives: using /usr/bin/g++-12 to provide /usr/bin/g++ (g++) in auto mode
ye@lst-hpc3090:~/tool/marian/build$ 
```

## Select the Default GCC Version

```
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --config gcc
There are 2 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/gcc-12   120       auto mode
  1            /usr/bin/gcc-12   120       manual mode
  2            /usr/bin/gcc-9    90        manual mode

Press <enter> to keep the current choice[*], or type selection number: 0
ye@lst-hpc3090:~/tool/marian/build$ 
```

## make Again 

```
ye@lst-hpc3090:~/tool/marian/build$ sudo make -j20
[  0%] Performing build step for 'nccl_install'
[  0%] Built target marian_version
[  6%] Built target zlib
[  8%] Built target SQLiteCpp
[ 11%] Built target pathie-cpp
[ 12%] Built target intgemm
[ 14%] Built target faiss
[ 19%] Built target sentencepiece_train-static
[ 31%] Built target libyaml-cpp
[ 47%] Built target sentencepiece-static
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_encode.dir/spm_encode_main.cc.o
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_train.dir/spm_train_main.cc.o
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_normalize.dir/spm_normalize_main.cc.o
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_decode.dir/spm_decode_main.cc.o
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_export_vocab.dir/spm_export_vocab_main.cc.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u64.o
[ 49%] Linking CXX executable ../../../../spm_export_vocab
[ 49%] Built target spm_export_vocab
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f16.o
[ 50%] Linking CXX executable ../../../../spm_normalize
[ 51%] Linking CXX executable ../../../../spm_train
[ 51%] Built target spm_normalize
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f64.o
[ 51%] Linking CXX executable ../../../../spm_decode
[ 51%] Built target spm_train
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i8.o
[ 51%] Built target spm_decode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u64.o
[ 51%] Linking CXX executable ../../../../spm_encode
[ 51%] Built target spm_encode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f64.o
Compiling  functions.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/functions.o
Archiving  objects                             > /home/ye/tool/marian/build/local/obj/collectives/device/colldevice.a
Linking    libnccl.so.2.8.3                    > /home/ye/tool/marian/build/local/lib/libnccl.so.2.8.3
Archiving  libnccl_static.a                    > /home/ye/tool/marian/build/local/lib/libnccl_static.a
/home/ye/tool/marian/src/3rd_party/nccl/src
[ 51%] No install step for 'nccl_install'
[ 52%] Completed 'nccl_install'
[ 54%] Built target nccl_install
[ 54%] Built target 3rd_party_installs
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_add.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_add_all.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/translator/marian_cuda_generated_nth_element.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_algorithm.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_cudnn_wrappers.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_device.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_element.cu.o
[ 57%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_hash.cu.o
[ 57%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_prod.cu.o
[ 58%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_topk.cu.o
[ 59%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/translator/marian_cuda_generated_helpers.cu.o
[ 58%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_tensor_operators.cu.o
[ 60%] Building CXX object src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod.cpp.o
[ 60%] Building CXX object src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod_sparse.cpp.o
In file included from /home/ye/tool/marian/src/common/definitions.h:5,
                 from /home/ye/tool/marian/src/tensors/tensor.h:3,
                 from /home/ye/tool/marian/src/tensors/gpu/prod.h:3,
                 from /home/ye/tool/marian/src/tensors/gpu/prod.cpp:9:
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = float; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:550:1:
/home/ye/tool/marian/src/common/intrusive_ptr.h:24:23: error: pointer used after ‘void operator delete(void*, std::size_t)’ [-Werror=use-after-free]
   24 |     if(x != 0 && --x->references_ == 0) {    \
      |                    ~~~^~~~~~~~~~~
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = float; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:549:18:
/home/ye/tool/marian/src/common/intrusive_ptr.h:25:14: note: call to ‘void operator delete(void*, std::size_t)’ here
   25 |       delete x;                              \
      |              ^
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = __half; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:550:1:
/home/ye/tool/marian/src/common/intrusive_ptr.h:24:23: error: pointer used after ‘void operator delete(void*, std::size_t)’ [-Werror=use-after-free]
   24 |     if(x != 0 && --x->references_ == 0) {    \
      |                    ~~~^~~~~~~~~~~
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = __half; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:549:18:
/home/ye/tool/marian/src/common/intrusive_ptr.h:25:14: note: call to ‘void operator delete(void*, std::size_t)’ here
   25 |       delete x;                              \
      |              ^
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
cc1plus: all warnings being treated as errors
make[2]: *** [src/CMakeFiles/marian_cuda.dir/build.make:160: src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:365: src/CMakeFiles/marian_cuda.dir/all] Error 2
make: *** [Makefile:156: all] Error 2
ye@lst-hpc3090:~/tool/marian/build$ 
```

## Change GCC to ver.9

```
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --config gcc
There are 2 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/gcc-12   120       auto mode
  1            /usr/bin/gcc-12   120       manual mode
  2            /usr/bin/gcc-9    90        manual mode

Press <enter> to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/bin/gcc-9 to provide /usr/bin/gcc (gcc) in manual mode
ye@lst-hpc3090:~/tool/marian/build$
```

## make Again

```
[ 54%] Built target spm_export_vocab
[ 54%] Built target spm_normalize
[ 54%] Built target spm_encode
In file included from /home/ye/tool/marian/src/common/definitions.h:5,
                 from /home/ye/tool/marian/src/tensors/tensor.h:3,
                 from /home/ye/tool/marian/src/tensors/gpu/prod.h:3,
                 from /home/ye/tool/marian/src/tensors/gpu/prod.cpp:9:
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = float; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:550:1:
/home/ye/tool/marian/src/common/intrusive_ptr.h:24:23: error: pointer used after ‘void operator delete(void*, std::size_t)’ [-Werror=use-after-free]
   24 |     if(x != 0 && --x->references_ == 0) {    \
      |                    ~~~^~~~~~~~~~~
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = float; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:549:18:
/home/ye/tool/marian/src/common/intrusive_ptr.h:25:14: note: call to ‘void operator delete(void*, std::size_t)’ here
   25 |       delete x;                              \
      |              ^
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = __half; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:550:1:
/home/ye/tool/marian/src/common/intrusive_ptr.h:24:23: error: pointer used after ‘void operator delete(void*, std::size_t)’ [-Werror=use-after-free]
   24 |     if(x != 0 && --x->references_ == 0) {    \
      |                    ~~~^~~~~~~~~~~
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
In function ‘void marian::intrusivePtrRelease(MemoryPiece*)’,
    inlined from ‘IntrusivePtr<T>::~IntrusivePtr() [with T = marian::MemoryPiece]’ at /home/ye/tool/marian/src/common/intrusive_ptr.h:66:26,
    inlined from ‘void marian::gpu::ProdBatchedTypedLegacy(marian::Tensor, marian::Ptr<marian::Allocator>, marian::Tensor, marian::Tensor, bool, bool, ComputeType, ComputeType) [with ElementType = __half; ComputeType = float]’ at /home/ye/tool/marian/src/tensors/gpu/prod.cpp:549:18:
/home/ye/tool/marian/src/common/intrusive_ptr.h:25:14: note: call to ‘void operator delete(void*, std::size_t)’ here
   25 |       delete x;                              \
      |              ^
/home/ye/tool/marian/src/tensors/memory_piece.h:14:3: note: in expansion of macro ‘ENABLE_INTRUSIVE_PTR’
   14 |   ENABLE_INTRUSIVE_PTR(MemoryPiece)
      |   ^~~~~~~~~~~~~~~~~~~~
cc1plus: all warnings being treated as errors
make[2]: *** [src/CMakeFiles/marian_cuda.dir/build.make:5839: src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:365: src/CMakeFiles/marian_cuda.dir/all] Error 2
make: *** [Makefile:156: all] Error 2
ye@lst-hpc3090:~/tool/marian/build$ 
```

## Check Current Installed Compilers

```
ye@lst-hpc3090:~/tool/marian/build$ dpkg --list | grep compiler
ii  g++                                           4:13.2.0-1ubuntu1                       amd64        GNU C++ compiler
ii  g++-12                                        12.3.0-9ubuntu2                         amd64        GNU C++ compiler
ii  g++-13                                        13.2.0-4ubuntu3                         amd64        GNU C++ compiler
ii  g++-9                                         9.5.0-4ubuntu2                          amd64        GNU C++ compiler
ii  gcc                                           4:13.2.0-1ubuntu1                       amd64        GNU C compiler
ii  gcc-12                                        12.3.0-9ubuntu2                         amd64        GNU C compiler
ii  gcc-13                                        13.2.0-4ubuntu3                         amd64        GNU C compiler
ii  gcc-9                                         9.5.0-4ubuntu2                          amd64        GNU C compiler
ii  libllvm15:amd64                               1:15.0.7-10                             amd64        Modular compiler and toolchain technologies, runtime library
ii  libllvm15:i386                                1:15.0.7-10                             i386         Modular compiler and toolchain technologies, runtime library
ii  libxkbcommon0:amd64                           1.5.0-1                                 amd64        library interface to the XKB compiler - shared library
ii  rpcsvc-proto                                  1.4.2-0ubuntu6                          amd64        RPC protocol compiler and definitions
ye@lst-hpc3090:~/tool/marian/build$
```

## Install gcc 13

```
ye@lst-hpc3090:~/tool/marian/build$ sudo apt install g++-13 gcc-13
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
g++-13 is already the newest version (13.2.0-4ubuntu3).
g++-13 set to manually installed.
gcc-13 is already the newest version (13.2.0-4ubuntu3).
gcc-13 set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 35 not upgraded.
```

```
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-13 13
ye@lst-hpc3090:~/tool/marian/build$ 
```

```
ye@lst-hpc3090:~/tool/marian/build$ sudo update-alternatives --config gcc
There are 3 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path             Priority   Status
------------------------------------------------------------
  0            /usr/bin/gcc-12   120       auto mode
  1            /usr/bin/gcc-12   120       manual mode
  2            /usr/bin/gcc-13   13        manual mode
* 3            /usr/bin/gcc-9    90        manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```

## Install gcc 7.3 from Source

[http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/](http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/)  

[http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.3.0/](http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.3.0/)  

Reference: [https://www.flamingbytes.com/blog/install-gcc-from-source/](https://www.flamingbytes.com/blog/install-gcc-from-source/)  

```
ye@lst-hpc3090:~/tool$ tar -xzvf ./gcc-7.3.0.tar.gz 
```

```
ye@lst-hpc3090:~/tool$ cd gcc-7.3.0/
ye@lst-hpc3090:~/tool/gcc-7.3.0$ ls
ABOUT-NLS           COPYING          intl          libgomp          libvtv              MD5SUMS
ChangeLog           COPYING3         LAST_UPDATED  libhsail-rt      ltgcc.m4            missing
ChangeLog.jit       COPYING3.LIB     libada        libiberty        ltmain.sh           mkdep
ChangeLog.tree-ssa  COPYING.LIB      libatomic     libitm           lt~obsolete.m4      mkinstalldirs
compile             COPYING.RUNTIME  libbacktrace  libmpx           lto-plugin          move-if-change
config              depcomp          libcc1        libobjc          ltoptions.m4        NEWS
config.guess        fixincludes      libcilkrts    liboffloadmic    ltsugar.m4          README
config-ml.in        gcc              libcpp        libquadmath      ltversion.m4        symlink-tree
config.rpath        gnattools        libdecnumber  libsanitizer     MAINTAINERS         ylwrap
config.sub          gotools          libffi        libssp           maintainer-scripts  zlib
configure           include          libgcc        libstdc++-v3     Makefile.def
configure.ac        INSTALL          libgfortran   libtool-ldflags  Makefile.in
contrib             install-sh       libgo         libtool.m4       Makefile.tpl
ye@lst-hpc3090:~/tool/gcc-7.3.0$ 
```

```
ye@lst-hpc3090:~/tool/gcc-7.3.0$ cd contrib
ye@lst-hpc3090:~/tool/gcc-7.3.0/contrib$ ls
analyze_brprob.py              config-list.mk          gimple.vim              reghunt
analyze_brprob_spec.py         dg-cmp-results.sh       gthr_supp_vxw_5x.c      regression
ChangeLog                      dg-extract-results.py   header-tools            repro_fail
ChangeLog.jit                  dg-extract-results.sh   index-prop              test_installed
ChangeLog.tree-ssa             dglib.pm                jit-coverage-report.py  test_recheck
check_GNU_style.sh             download_prerequisites  make-obstacks-texi.pl   testsuite-management
check_makefile_deps.sh         filter_gcc_for_doxygen  make_sunver.pl          test_summary
check_warning_flags.sh         filter_knr2ansi.pl      mark_spam.py            texi2pod.pl
clang-format                   filter_params.pl        mklog                   uninclude
compare-all-tests              gcc_build               paranoia.cc             update-copyright.py
compare-debug                  gcc.doxy                patch_tester.sh         vimrc
compareSumTests3               gcc_update              prepare_patch.sh        warn_summary
compare_tests                  gen_autofdo_event.py    prerequisites.md5
compare_two_ftime_report_sets  gennews                 prerequisites.sha512
ye@lst-hpc3090:~/tool/gcc-7.3.0/contrib$ 
```

Download dependent libraries ...  

```
ye@lst-hpc3090:~/tool/gcc-7.3.0$ time ./contrib/download_prerequisites 
2024-04-12 17:02:53 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/gmp-6.1.0.tar.bz2 [2383840] -> "./gmp-6.1.0.tar.bz2" [1]
2024-04-12 17:03:03 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/mpfr-3.1.4.tar.bz2 [1279284] -> "./mpfr-3.1.4.tar.bz2" [1]
2024-04-12 17:03:09 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/mpc-1.0.3.tar.gz [669925] -> "./mpc-1.0.3.tar.gz" [1]
2024-04-12 17:03:18 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-0.16.1.tar.bz2 [1626446] -> "./isl-0.16.1.tar.bz2" [1]
gmp-6.1.0.tar.bz2: OK
mpfr-3.1.4.tar.bz2: OK
mpc-1.0.3.tar.gz: OK
isl-0.16.1.tar.bz2: OK
All prerequisites downloaded successfully.

real	1m13.105s
user	0m0.572s
sys	0m0.091s
ye@lst-hpc3090:~/tool/gcc-7.3.0$
```

configure ...  

```
ye@lst-hpc3090:~/tool/gcc-7.3.0$ time ./configure --enable-languages=c,c++ --disable-multilib
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether ln works... yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... /usr/bin/sed
checking for gawk... no
checking for mawk... mawk
checking for libatomic support... yes
checking for libcilkrts support... yes
checking for libitm support... yes
checking for libsanitizer support... yes
checking for libvtv support... yes
checking for libmpx support... yes
checking for libhsail-rt support... yes
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... yes
checking whether we are cross compiling... no
checking for suffix of executables... 
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking whether g++ accepts -static-libstdc++ -static-libgcc... yes
checking for gnatbind... no
checking for gnatmake... no
checking whether compiler driver understands Ada... no
checking how to compare bootstrapped objects... cmp --ignore-initial=16 $$f1 $$f2
checking for objdir... .libs
configure: WARNING: using in-tree isl, disabling version check
*** This configuration is not supported in the following subdirectories:
     gnattools gotools target-libada target-libhsail-rt target-libgfortran target-libbacktrace target-libgo target-libffi target-libobjc target-liboffloadmic
    (Any other directories should still work fine.)
checking for default BUILD_CONFIG... bootstrap-debug
checking for --enable-vtable-verify... no
checking for bison... no
checking for byacc... no
checking for yacc... no
checking for bison... no
checking for gm4... no
checking for gnum4... no
checking for m4... no
checking for flex... no
checking for lex... no
checking for flex... no
checking for makeinfo... no
/home/ye/tool/gcc-7.3.0/missing: 81: makeinfo: not found
checking for expect... no
checking for runtest... no
checking for ar... ar
checking for as... as
checking for dlltool... no
checking for ld... ld
checking for lipo... no
checking for nm... nm
checking for ranlib... ranlib
checking for strip... strip
checking for windres... no
checking for windmc... no
checking for objcopy... objcopy
checking for objdump... objdump
checking for readelf... readelf
checking for cc... cc
checking for c++... c++
checking for gcc... gcc
checking for gfortran... no
checking for gccgo... no
checking for ar... no
checking for ar... ar
checking for as... no
checking for as... as
checking for dlltool... no
checking for dlltool... no
checking for ld... no
checking for ld... ld
checking for lipo... no
checking for lipo... no
checking for nm... no
checking for nm... nm
checking for objcopy... no
checking for objcopy... objcopy
checking for objdump... no
checking for objdump... objdump
checking for ranlib... no
checking for ranlib... ranlib
checking for readelf... no
checking for readelf... readelf
checking for strip... no
checking for strip... strip
checking for windres... no
checking for windres... no
checking for windmc... no
checking for windmc... no
checking where to find the target ar... host tool
checking where to find the target as... host tool
checking where to find the target cc... just compiled
checking where to find the target c++... just compiled
checking where to find the target c++ for libstdc++... just compiled
checking where to find the target dlltool... host tool
checking where to find the target gcc... just compiled
checking where to find the target gfortran... host tool
checking where to find the target gccgo... host tool
checking where to find the target ld... host tool
checking where to find the target lipo... host tool
checking where to find the target nm... host tool
checking where to find the target objcopy... host tool
checking where to find the target objdump... host tool
checking where to find the target ranlib... host tool
checking where to find the target readelf... host tool
checking where to find the target strip... host tool
checking where to find the target windres... host tool
checking where to find the target windmc... host tool
checking whether to enable maintainer-specific portions of Makefiles... no
configure: creating ./config.status
config.status: creating Makefile

real	0m0.706s
user	0m0.740s
sys	0m0.127s
ye@lst-hpc3090:~/tool/gcc-7.3.0$ 
```

compile ...  

```
ye@lst-hpc3090:~/tool/gcc-7.3.0$ time make -j20
...
...
...
j.lo tls.lo method-serial.lo method-gl.lo method-ml.lo  x86_sse.lo x86_avx.lo futex.lo  
libtool: link: /home/ye/tool/gcc-7.3.0/host-x86_64-pc-linux-gnu/gcc/xgcc -B/home/ye/tool/gcc-7.3.0/host-x86_64-pc-linux-gnu/gcc/ -B/usr/local/x86_64-pc-linux-gnu/bin/ -B/usr/local/x86_64-pc-linux-gnu/lib/ -isystem /usr/local/x86_64-pc-linux-gnu/include -isystem /usr/local/x86_64-pc-linux-gnu/sys-include    -shared  -fPIC -DPIC  .libs/aatree.o .libs/alloc.o .libs/alloc_c.o .libs/alloc_cpp.o .libs/barrier.o .libs/beginend.o .libs/clone.o .libs/eh_cpp.o .libs/local.o .libs/query.o .libs/retry.o .libs/rwlock.o .libs/useraction.o .libs/util.o .libs/sjlj.o .libs/tls.o .libs/method-serial.o .libs/method-gl.o .libs/method-ml.o .libs/x86_sse.o .libs/x86_avx.o .libs/futex.o    -mrtm -pthread -Wl,-O1 -Wl,--version-script -Wl,../.././libitm/libitm.map   -Wl,-soname -Wl,libitm.so.1 -o .libs/libitm.so.1.0.0
libtool: link: (cd ".libs" && rm -f "libitm.so.1" && ln -s "libitm.so.1.0.0" "libitm.so.1")
libtool: link: (cd ".libs" && rm -f "libitm.so" && ln -s "libitm.so.1.0.0" "libitm.so")
libtool: link: ar rc .libs/libitm.a  aatree.o alloc.o alloc_c.o alloc_cpp.o barrier.o beginend.o clone.o eh_cpp.o local.o query.o retry.o rwlock.o useraction.o util.o sjlj.o tls.o method-serial.o method-gl.o method-ml.o x86_sse.o x86_avx.o futex.o
libtool: link: ranlib .libs/libitm.a
libtool: link: ( cd ".libs" && rm -f "libitm.la" && ln -s "../libitm.la" "libitm.la" )
make[4]: Leaving directory '/home/ye/tool/gcc-7.3.0/x86_64-pc-linux-gnu/libitm'
make[3]: Leaving directory '/home/ye/tool/gcc-7.3.0/x86_64-pc-linux-gnu/libitm'
make[2]: Leaving directory '/home/ye/tool/gcc-7.3.0/x86_64-pc-linux-gnu/libitm'
make[1]: Leaving directory '/home/ye/tool/gcc-7.3.0'
make: *** [Makefile:944: all] Error 2

real	10m9.188s
user	112m42.039s
sys	4m56.812s
```

Installation ...  

```
time sudo make install
...
...
...
izer_common/sanitizer_platform_limits_posix.cc  -fPIC -DPIC -o .libs/sanitizer_platform_limits_posix.o
../../.././libsanitizer/sanitizer_common/sanitizer_platform_limits_posix.cc:157:10: fatal error: sys/ustat.h: No such file or directory
 #include <sys/ustat.h>
          ^~~~~~~~~~~~~
compilation terminated.
make[3]: *** [Makefile:523: sanitizer_platform_limits_posix.lo] Error 1
make[3]: Leaving directory '/home/ye/tool/gcc-7.3.0/x86_64-pc-linux-gnu/libsanitizer/sanitizer_common'
make[2]: *** [Makefile:467: install-recursive] Error 1
make[2]: Leaving directory '/home/ye/tool/gcc-7.3.0/x86_64-pc-linux-gnu/libsanitizer'
make[1]: *** [Makefile:19241: install-target-libsanitizer] Error 2
make[1]: Leaving directory '/home/ye/tool/gcc-7.3.0'
make: *** [Makefile:2338: install] Error 2

real	0m6.392s
user	0m0.016s
sys	0m0.024s
ye@lst-hpc3090:~/tool/gcc-7.3.0$
```

Got Error and thus cannot get the 7.3 as follows (confirmation with tab key):  

```
ye@lst-hpc3090:~/tool/gcc-7.3.0$ ls /usr/bin/gcc-
gcc-12         gcc-ar         gcc-ar-9       gcc-nm-13      gcc-ranlib-12  
gcc-13         gcc-ar-12      gcc-nm         gcc-nm-9       gcc-ranlib-13  
gcc-9          gcc-ar-13      gcc-nm-12      gcc-ranlib     gcc-ranlib-9   
ye@lst-hpc3090:~/tool/gcc-7.3.0$
```

## Installation of gcc-7.5 from Source

Download link:  
[http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.5.0/](http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.5.0/)  

```
ye@lst-hpc3090:~/tool$ cd gcc-7.5.0/
ye@lst-hpc3090:~/tool/gcc-7.5.0$ ls
ABOUT-NLS           COPYING          intl          libgomp          libvtv              MD5SUMS
ChangeLog           COPYING3         LAST_UPDATED  libhsail-rt      ltgcc.m4            missing
ChangeLog.jit       COPYING3.LIB     libada        libiberty        ltmain.sh           mkdep
ChangeLog.tree-ssa  COPYING.LIB      libatomic     libitm           lt~obsolete.m4      mkinstalldirs
compile             COPYING.RUNTIME  libbacktrace  libmpx           lto-plugin          move-if-change
config              depcomp          libcc1        libobjc          ltoptions.m4        NEWS
config.guess        fixincludes      libcilkrts    liboffloadmic    ltsugar.m4          README
config-ml.in        gcc              libcpp        libquadmath      ltversion.m4        symlink-tree
config.rpath        gnattools        libdecnumber  libsanitizer     MAINTAINERS         ylwrap
config.sub          gotools          libffi        libssp           maintainer-scripts  zlib
configure           include          libgcc        libstdc++-v3     Makefile.def
configure.ac        INSTALL          libgfortran   libtool-ldflags  Makefile.in
contrib             install-sh       libgo         libtool.m4       Makefile.tpl
ye@lst-hpc3090:~/tool/gcc-7.5.0$ 
```

```
ye@lst-hpc3090:~/tool/gcc-7.5.0$ time ./contrib/download_prerequisites 
2024-04-12 17:40:06 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/gmp-6.1.0.tar.bz2 [2383840] -> "./gmp-6.1.0.tar.bz2" [1]
2024-04-12 17:40:13 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/mpfr-3.1.4.tar.bz2 [1279284] -> "./mpfr-3.1.4.tar.bz2" [1]
2024-04-12 17:40:19 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/mpc-1.0.3.tar.gz [669925] -> "./mpc-1.0.3.tar.gz" [1]
2024-04-12 17:40:26 URL: ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-0.16.1.tar.bz2 [1626446] -> "./isl-0.16.1.tar.bz2" [1]
gmp-6.1.0.tar.bz2: OK
mpfr-3.1.4.tar.bz2: OK
mpc-1.0.3.tar.gz: OK
isl-0.16.1.tar.bz2: OK
All prerequisites downloaded successfully.

real	0m36.916s
user	0m0.515s
sys	0m0.087s
ye@lst-hpc3090:~/tool/gcc-7.5.0$ 
```

configure ...  

```
ye@lst-hpc3090:~/tool/gcc-7.5.0$ time ./configure --enable-languages=c,c++ --disable-multilib
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether ln works... yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... /usr/bin/sed
checking for gawk... no
checking for mawk... mawk
checking for libatomic support... yes
checking for libcilkrts support... yes
checking for libitm support... yes
checking for libsanitizer support... yes
checking for libvtv support... yes
checking for libmpx support... yes
checking for libhsail-rt support... yes
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... yes
checking whether we are cross compiling... no
checking for suffix of executables... 
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking whether g++ accepts -static-libstdc++ -static-libgcc... yes
checking for gnatbind... no
checking for gnatmake... no
checking whether compiler driver understands Ada... no
checking how to compare bootstrapped objects... cmp --ignore-initial=16 $$f1 $$f2
checking for objdir... .libs
configure: WARNING: using in-tree isl, disabling version check
*** This configuration is not supported in the following subdirectories:
     gnattools gotools target-libada target-libhsail-rt target-libgfortran target-libbacktrace target-libgo target-libffi target-libobjc target-liboffloadmic
    (Any other directories should still work fine.)
checking for default BUILD_CONFIG... bootstrap-debug
checking for --enable-vtable-verify... no
checking for bison... no
checking for byacc... no
checking for yacc... no
checking for bison... no
checking for gm4... no
checking for gnum4... no
checking for m4... no
checking for flex... no
checking for lex... no
checking for flex... no
checking for makeinfo... no
/home/ye/tool/gcc-7.5.0/missing: 81: makeinfo: not found
checking for expect... no
checking for runtest... no
checking for ar... ar
checking for as... as
checking for dlltool... no
checking for ld... ld
checking for lipo... no
checking for nm... nm
checking for ranlib... ranlib
checking for strip... strip
checking for windres... no
checking for windmc... no
checking for objcopy... objcopy
checking for objdump... objdump
checking for readelf... readelf
checking for cc... cc
checking for c++... c++
checking for gcc... gcc
checking for gfortran... no
checking for gccgo... no
checking for ar... no
checking for ar... ar
checking for as... no
checking for as... as
checking for dlltool... no
checking for dlltool... no
checking for ld... no
checking for ld... ld
checking for lipo... no
checking for lipo... no
checking for nm... no
checking for nm... nm
checking for objcopy... no
checking for objcopy... objcopy
checking for objdump... no
checking for objdump... objdump
checking for ranlib... no
checking for ranlib... ranlib
checking for readelf... no
checking for readelf... readelf
checking for strip... no
checking for strip... strip
checking for windres... no
checking for windres... no
checking for windmc... no
checking for windmc... no
checking where to find the target ar... host tool
checking where to find the target as... host tool
checking where to find the target cc... just compiled
checking where to find the target c++... just compiled
checking where to find the target c++ for libstdc++... just compiled
checking where to find the target dlltool... host tool
checking where to find the target gcc... just compiled
checking where to find the target gfortran... host tool
checking where to find the target gccgo... host tool
checking where to find the target ld... host tool
checking where to find the target lipo... host tool
checking where to find the target nm... host tool
checking where to find the target objcopy... host tool
checking where to find the target objdump... host tool
checking where to find the target ranlib... host tool
checking where to find the target readelf... host tool
checking where to find the target strip... host tool
checking where to find the target windres... host tool
checking where to find the target windmc... host tool
checking whether to enable maintainer-specific portions of Makefiles... no
configure: creating ./config.status
config.status: creating Makefile

real	0m0.720s
user	0m0.740s
sys	0m0.153s
ye@lst-hpc3090:~/tool/gcc-7.5.0$ 
```

```
ye@lst-hpc3090:~/tool/gcc-7.5.0$ time make -j20
...
...
...
j.lo tls.lo method-serial.lo method-gl.lo method-ml.lo  x86_sse.lo x86_avx.lo futex.lo  
libtool: link: /home/ye/tool/gcc-7.5.0/host-x86_64-pc-linux-gnu/gcc/xgcc -B/home/ye/tool/gcc-7.5.0/host-x86_64-pc-linux-gnu/gcc/ -B/usr/local/x86_64-pc-linux-gnu/bin/ -B/usr/local/x86_64-pc-linux-gnu/lib/ -isystem /usr/local/x86_64-pc-linux-gnu/include -isystem /usr/local/x86_64-pc-linux-gnu/sys-include    -shared  -fPIC -DPIC  .libs/aatree.o .libs/alloc.o .libs/alloc_c.o .libs/alloc_cpp.o .libs/barrier.o .libs/beginend.o .libs/clone.o .libs/eh_cpp.o .libs/local.o .libs/query.o .libs/retry.o .libs/rwlock.o .libs/useraction.o .libs/util.o .libs/sjlj.o .libs/tls.o .libs/method-serial.o .libs/method-gl.o .libs/method-ml.o .libs/x86_sse.o .libs/x86_avx.o .libs/futex.o    -mrtm -pthread -Wl,-O1 -Wl,--version-script -Wl,../.././libitm/libitm.map   -Wl,-soname -Wl,libitm.so.1 -o .libs/libitm.so.1.0.0
libtool: link: (cd ".libs" && rm -f "libitm.so.1" && ln -s "libitm.so.1.0.0" "libitm.so.1")
libtool: link: (cd ".libs" && rm -f "libitm.so" && ln -s "libitm.so.1.0.0" "libitm.so")
libtool: link: ar rc .libs/libitm.a  aatree.o alloc.o alloc_c.o alloc_cpp.o barrier.o beginend.o clone.o eh_cpp.o local.o query.o retry.o rwlock.o useraction.o util.o sjlj.o tls.o method-serial.o method-gl.o method-ml.o x86_sse.o x86_avx.o futex.o
libtool: link: ranlib .libs/libitm.a
libtool: link: ( cd ".libs" && rm -f "libitm.la" && ln -s "../libitm.la" "libitm.la" )
make[4]: Leaving directory '/home/ye/tool/gcc-7.5.0/x86_64-pc-linux-gnu/libitm'
make[3]: Leaving directory '/home/ye/tool/gcc-7.5.0/x86_64-pc-linux-gnu/libitm'
make[2]: Leaving directory '/home/ye/tool/gcc-7.5.0/x86_64-pc-linux-gnu/libitm'
make[1]: Leaving directory '/home/ye/tool/gcc-7.5.0'
make: *** [Makefile:944: all] Error 2

real	9m52.457s
user	108m31.374s
sys	5m3.100s
```

For this time, I removed "--disable-multilib" ... 

```
ye@lst-hpc3090:~/tool/gcc-7.5.0$ time ./configure --enable-languages=c,c++
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether ln works... yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... /usr/bin/sed
checking for gawk... no
checking for mawk... mawk
checking for libatomic support... yes
checking for libcilkrts support... yes
checking for libitm support... yes
checking for libsanitizer support... yes
checking for libvtv support... yes
checking for libmpx support... yes
checking for libhsail-rt support... yes
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... yes
checking whether we are cross compiling... no
checking for suffix of executables... 
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking whether g++ accepts -static-libstdc++ -static-libgcc... yes
checking for gnatbind... no
checking for gnatmake... no
checking whether compiler driver understands Ada... no
checking how to compare bootstrapped objects... cmp --ignore-initial=16 $$f1 $$f2
checking for objdir... .libs
configure: WARNING: using in-tree isl, disabling version check
*** This configuration is not supported in the following subdirectories:
     gnattools gotools target-libada target-libhsail-rt target-libgfortran target-libbacktrace target-libgo target-libffi target-libobjc target-liboffloadmic
    (Any other directories should still work fine.)
checking for default BUILD_CONFIG... bootstrap-debug
checking for --enable-vtable-verify... no
*** removing build-x86_64-pc-linux-gnu/libiberty/Makefile to force reconfigure
*** removing build-x86_64-pc-linux-gnu/libcpp/Makefile to force reconfigure
*** removing build-x86_64-pc-linux-gnu/fixincludes/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libgcc/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libgomp/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libcilkrts/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libatomic/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libitm/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libstdc++-v3/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libsanitizer/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libvtv/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libmpx/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libssp/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libquadmath/Makefile to force reconfigure
/usr/bin/ld: cannot find crt1.o: No such file or directory
/usr/bin/ld: cannot find crti.o: No such file or directory
/usr/bin/ld: skipping incompatible /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.3.0/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc: No such file or directory
/usr/bin/ld: cannot find -lgcc_s: No such file or directory
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.so when searching for -lc
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.a when searching for -lc
/usr/bin/ld: cannot find -lc: No such file or directory
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.so when searching for -lc
/usr/bin/ld: skipping incompatible /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.3.0/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc: No such file or directory
/usr/bin/ld: cannot find -lgcc_s: No such file or directory
/usr/bin/ld: cannot find crtn.o: No such file or directory
collect2: error: ld returned 1 exit status
configure: error: I suspect your system does not have 32-bit development libraries (libc and headers). If you have them, rerun configure with --enable-multilib. If you do not have them, and want to build a 64-bit-only compiler, rerun configure with --disable-multilib.

real	0m0.526s
user	0m0.476s
sys	0m0.109s
ye@lst-hpc3090:~/tool/gcc-7.5.0$ 
```

```
ye@lst-hpc3090:~/tool/gcc-7.5.0$ ./configure --prefix=$(pwd) --enable-languages=c,c++,fortran --disable-werror
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether ln works... yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... /usr/bin/sed
checking for gawk... no
checking for mawk... mawk
checking for libatomic support... yes
checking for libcilkrts support... yes
checking for libitm support... yes
checking for libsanitizer support... yes
checking for libvtv support... yes
checking for libmpx support... yes
checking for libhsail-rt support... yes
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... yes
checking whether we are cross compiling... no
checking for suffix of executables... 
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking whether g++ accepts -static-libstdc++ -static-libgcc... yes
checking for gnatbind... no
checking for gnatmake... no
checking whether compiler driver understands Ada... no
checking how to compare bootstrapped objects... cmp --ignore-initial=16 $$f1 $$f2
checking for objdir... .libs
configure: WARNING: using in-tree isl, disabling version check
*** This configuration is not supported in the following subdirectories:
     gnattools gotools target-libada target-libhsail-rt target-libgo target-libffi target-libobjc target-liboffloadmic
    (Any other directories should still work fine.)
checking for default BUILD_CONFIG... bootstrap-debug
checking for --enable-vtable-verify... no
*** removing build-x86_64-pc-linux-gnu/libiberty/Makefile to force reconfigure
*** removing build-x86_64-pc-linux-gnu/libcpp/Makefile to force reconfigure
*** removing build-x86_64-pc-linux-gnu/fixincludes/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libgcc/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libgomp/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libcilkrts/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libatomic/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libitm/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libstdc++-v3/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libsanitizer/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libvtv/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libmpx/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libssp/Makefile to force reconfigure
*** removing x86_64-pc-linux-gnu/libquadmath/Makefile to force reconfigure
/usr/bin/ld: cannot find crt1.o: No such file or directory
/usr/bin/ld: cannot find crti.o: No such file or directory
/usr/bin/ld: skipping incompatible /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc: No such file or directory
/usr/bin/ld: cannot find -lgcc_s: No such file or directory
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.so when searching for -lc
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.a when searching for -lc
/usr/bin/ld: cannot find -lc: No such file or directory
/usr/bin/ld: skipping incompatible /usr/lib/x86_64-linux-gnu/libc.so when searching for -lc
/usr/bin/ld: skipping incompatible /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc: No such file or directory
/usr/bin/ld: cannot find -lgcc_s: No such file or directory
/usr/bin/ld: cannot find crtn.o: No such file or directory
collect2: error: ld returned 1 exit status
configure: error: I suspect your system does not have 32-bit development libraries (libc and headers). If you have them, rerun configure with --enable-multilib. If you do not have them, and want to build a 64-bit-only compiler, rerun configure with --disable-multilib.
ye@lst-hpc3090:~/tool/gcc-7.5.0$ 
```

I should stop gcc old version compilation from source code ...  

## Reinstall Marian with -DUSE_STATIC_LIBS=on

```
ye@lst-hpc3090:~/tool/marian$ sudo rm -rf build
```

```
ye@lst-hpc3090:~/tool/marian$ mkdir build
```

```
ye@lst-hpc3090:~/tool/marian$ cd build
```

```
ye@lst-hpc3090:~/tool/marian/build$ cmake .. -DUSE_STATIC_LIBS=on
-- The CXX compiler identification is GNU 7.5.0
-- The C compiler identification is GNU 7.5.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/local/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/local/bin/gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Project name: marian
-- Project version: v1.12.0+65bf82ff
CMake Warning at CMakeLists.txt:79 (message):
  CMAKE_BUILD_TYPE not set; setting to Release


-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
-- Could not find hardware support for AVX512 on this machine.
CMake Warning (dev) at CMakeLists.txt:308 (find_package):
  Policy CMP0146 is not set: The FindCUDA module is removed.  Run "cmake
  --help-policy CMP0146" for policy details.  Use the cmake_policy command to
  set the policy and suppress this warning.

This warning is for project developers.  Use -Wno-dev to suppress it.

-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "12.0", minimum required is "9.0") 
-- Compiling code for Pascal GPUs
-- Compiling code for Volta GPUs
-- Compiling code for Turing GPUs
-- Compiling code for Ampere GPUs
-- Compiling code for Ampere RTX GPUs
-- Found CUDA libraries: /usr/lib/x86_64-linux-gnu/libcurand_static.a;/usr/lib/x86_64-linux-gnu/libcublas_static.a;/usr/lib/x86_64-linux-gnu/libcusparse_static.a;/usr/lib/x86_64-linux-gnu/libculibos.a;/usr/lib/x86_64-linux-gnu/libcublasLt_static.a
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find MKL (missing: MKL_LIBRARIES MKL_INCLUDE_DIRS MKL_INTERFACE_LIBRARY MKL_SEQUENTIAL_LAYER_LIBRARY MKL_CORE_LIBRARY) 
-- Looking for sgemm_
-- Looking for sgemm_ - not found
-- Could NOT find BLAS (missing: BLAS_LIBRARIES) 
CMake Warning at src/3rd_party/intgemm/CMakeLists.txt:58 (message):
  Your compiler is too old to support AVX512VNNI.  Multiplication will
  be slower on CPUs that support these instructions.  For details rerun cmake
  with --debug-trycompile then try to build in
  compile_tests/CMakeFiles/CMakeTmp.


CMake Deprecation Warning at src/3rd_party/sentencepiece/CMakeLists.txt:15 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Configuring done (0.8s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ye/tool/marian/build
ye@lst-hpc3090:~/tool/marian/build$
```

```
ye@lst-hpc3090:~/tool/marian/build$ make -j20
[  1%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/path.cpp.o
[  1%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[  2%] Creating directories for 'nccl_install'
[  3%] Built target marian_version
[  3%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/builder.cc.o
[  3%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Backup.cpp.o
[  4%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
[  4%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/entry_iterator.cpp.o
[  5%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/errors.cpp.o
[  5%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
[  5%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/adler32.c.o
[  5%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/contrib/graphbuilderadapter.cpp.o
[  6%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/contrib/graphbuilder.cpp.o
[  6%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/binary_renamed.cpp.o
[  7%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Database.cpp.o
[  7%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Column.cpp.o
[  7%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Exception.cpp.o
[  8%] Building CXX object src/3rd_party/intgemm/CMakeFiles/intgemm.dir/intgemm/intgemm.cc.o
[  9%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arena.cc.o
[ 10%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/VectorTransform.cpp.o
[ 10%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[ 11%] No download step for 'nccl_install'
[ 11%] No update step for 'nccl_install'
[ 11%] No patch step for 'nccl_install'
[ 11%] No configure step for 'nccl_install'
[ 11%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/compress.c.o
[ 11%] Performing build step for 'nccl_install'
[ 12%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/crc32.c.o
Generating nccl.h.in                           > /home/ye/tool/marian/build/local/include/nccl.h
Grabbing   include/nccl_net.h                  > /home/ye/tool/marian/build/local/include/nccl_net.h
Generating nccl.pc.in                          > /home/ye/tool/marian/build/local/lib/pkgconfig/nccl.pc
Compiling  init.cc                             > /home/ye/tool/marian/build/local/obj/init.o
[ 12%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/deflate.c.o
[ 13%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/convert.cpp.o
[ 13%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/directives.cpp.o
[ 13%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emit.cpp.o
[ 14%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[ 14%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Statement.cpp.o
[ 15%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzclose.c.o
[ 16%] Building CXX object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/src/Transaction.cpp.o
[ 16%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arenastring.cc.o
[ 17%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitfromevents.cpp.o
[ 17%] Building C object src/3rd_party/SQLiteCpp/CMakeFiles/SQLiteCpp.dir/sqlite3/sqlite3.c.o
[ 17%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/bytestream.cc.o
Compiling  channel.cc                          > /home/ye/tool/marian/build/local/obj/channel.o
[ 18%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[ 18%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitter.cpp.o
[ 18%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/common.cc.o
[ 19%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 19%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 19%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 19%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
[ 19%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzlib.c.o
[ 19%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzread.c.o
[ 20%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/gzwrite.c.o
[ 20%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/infback.c.o
[ 21%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 22%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inffast.c.o
[ 22%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inflate.c.o
[ 22%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/inftrees.c.o
[ 22%] Linking CXX static library libintgemm.a
[ 22%] Built target intgemm
[ 23%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/trees.c.o
[ 23%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
[ 23%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/uncompr.c.o
[ 24%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitterstate.cpp.o
[ 24%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/int128.cc.o
[ 25%] Building C object src/3rd_party/zlib/CMakeFiles/zlib.dir/zutil.c.o
[ 26%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 26%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 26%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie.cpp.o
[ 27%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
[ 27%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie_ifstream.cpp.o
[ 28%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/pathie_ofstream.cpp.o
[ 28%] Built target zlib
[ 28%] Building CXX object src/3rd_party/pathie-cpp/CMakeFiles/pathie-cpp.dir/src/temp.cpp.o
[ 28%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 29%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/status.cc.o
Compiling  bootstrap.cc                        > /home/ye/tool/marian/build/local/obj/bootstrap.o
[ 29%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 29%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/emitterutils.cpp.o
[ 29%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/exceptions.cpp.o
[ 30%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/exp.cpp.o
[ 30%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 30%] Built target pathie-cpp
[ 30%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/memory.cpp.o
[ 30%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 31%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 32%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/node_data.cpp.o
[ 32%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 33%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 33%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/time.cc.o
[ 33%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/nodebuilder.cpp.o
[ 33%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 34%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 34%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 35%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece.pb.cc.o
[ 35%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 35%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/bpe_model.cc.o
[ 36%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/char_model.cc.o
[ 36%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/error.cc.o
[ 36%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/nodeevents.cpp.o
[ 37%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/null.cpp.o
Compiling  transport.cc                        > /home/ye/tool/marian/build/local/obj/transport.o
Compiling  enqueue.cc                          > /home/ye/tool/marian/build/local/obj/enqueue.o
[ 38%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/filesystem.cc.o
[ 38%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/init.cc.o
[ 38%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/model_factory.cc.o
[ 39%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/model_interface.cc.o
In file included from include/core.h:54:0,
                 from include/transport.h:13,
                 from include/comm.h:10,
                 from include/enqueue.h:10,
                 from enqueue.cc:7:
enqueue.cc: In function ‘ncclResult_t ncclLaunchCooperativeKernelMultiDevice(cudaLaunchParams*, int*, int, int)’:
enqueue.cc:75:97: warning: ‘cudaError_t cudaLaunchCooperativeKernelMultiDevice(cudaLaunchParams*, unsigned int, unsigned int)’ is deprecated [-Wdeprecated-declarations]
             cudaCooperativeLaunchMultiDeviceNoPreSync|cudaCooperativeLaunchMultiDeviceNoPostSync));
                                                                                                 ^
include/checks.h:14:23: note: in definition of macro ‘CUDACHECK’
     cudaError_t err = cmd;                                  \
                       ^~~
In file included from /usr/include/channel_descriptor.h:61:0,
                 from /usr/include/cuda_runtime.h:95,
                 from /home/ye/tool/marian/build/local/include/nccl.h:10,
                 from include/devcomm.h:10,
                 from include/transport.h:10,
                 from include/comm.h:10,
                 from include/enqueue.h:10,
                 from enqueue.cc:7:
/usr/include/cuda_runtime_api.h:4360:57: note: declared here
 extern __CUDA_DEPRECATED __host__ cudaError_t CUDARTAPI cudaLaunchCooperativeKernelMultiDevice(struct cudaLaunchParams *launchParamsList, unsigned int numDevices, unsigned int flags  __dv(0));
                                                         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
enqueue.cc: In function ‘ncclResult_t ncclCpuBarrierOut(ncclComm*)’:
enqueue.cc:178:49: warning: ‘int pthread_yield()’ is deprecated: pthread_yield is deprecated, use sched_yield instead [-Wdeprecated-declarations]
   while (*ptr < comm->intraRanks) pthread_yield();
                                                 ^
In file included from /usr/include/features.h:502:0,
                 from /usr/include/x86_64-linux-gnu/bits/libc-header-start.h:33,
                 from /usr/include/limits.h:26,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/limits.h:194,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/syslimits.h:7,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/limits.h:34,
                 from /usr/include/driver_types.h:81,
                 from /usr/include/builtin_types.h:59,
                 from /usr/include/cuda_runtime.h:91,
                 from /home/ye/tool/marian/build/local/include/nccl.h:10,
                 from include/devcomm.h:10,
                 from include/transport.h:10,
                 from include/comm.h:10,
                 from include/enqueue.h:10,
                 from enqueue.cc:7:
/usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/pthread.h:488:12: note: declared here
 extern int __REDIRECT_NTH (pthread_yield, (void), sched_yield)
            ^
[ 39%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/ostream_wrapper.cpp.o
[ 39%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/normalizer.cc.o
[ 39%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/parse.cpp.o
Compiling  group.cc                            > /home/ye/tool/marian/build/local/obj/group.o
[ 40%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/parser.cpp.o
[ 41%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/case_encoder.cc.o
[ 41%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/sentencepiece_processor.cc.o
[ 41%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/unigram_model.cc.o
[ 41%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/regex_yaml.cpp.o
[ 41%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/Heap.cpp.o
[ 42%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/util.cc.o
[ 42%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 43%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 44%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanner.cpp.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
[ 44%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scanscalar.cpp.o
[ 44%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/hamming.cpp.o
[ 44%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantag.cpp.o
[ 45%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/scantoken.cpp.o
[ 45%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/simplekey.cpp.o
[ 46%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/singledocparser.cpp.o
[ 46%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/stream.cpp.o
[ 46%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/tag.cpp.o
Compiling  debug.cc                            > /home/ye/tool/marian/build/local/obj/debug.o
Compiling  proxy.cc                            > /home/ye/tool/marian/build/local/obj/proxy.o
[ 47%] Building CXX object src/3rd_party/yaml-cpp/CMakeFiles/libyaml-cpp.dir/yaml-node.cpp.o
Compiling  misc/nvmlwrap.cc                    > /home/ye/tool/marian/build/local/obj/misc/nvmlwrap.o
[ 48%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/misc.cpp.o
Compiling  misc/ibvwrap.cc                     > /home/ye/tool/marian/build/local/obj/misc/ibvwrap.o
misc/nvmlwrap.cc: In function ‘ncclResult_t wrapNvmlSymbols()’:
misc/nvmlwrap.cc:37:57: warning: ‘int pthread_yield()’ is deprecated: pthread_yield is deprecated, use sched_yield instead [-Wdeprecated-declarations]
     while (nvmlState == nvmlInitializing) pthread_yield();
                                                         ^
In file included from /usr/include/features.h:502:0,
                 from /usr/include/x86_64-linux-gnu/bits/libc-header-start.h:33,
                 from /usr/include/limits.h:26,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/limits.h:194,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/syslimits.h:7,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/limits.h:34,
                 from /usr/include/driver_types.h:81,
                 from /usr/include/builtin_types.h:59,
                 from /usr/include/cuda_runtime.h:91,
                 from /home/ye/tool/marian/build/local/include/nccl.h:10,
                 from include/nvmlwrap.h:10,
                 from misc/nvmlwrap.cc:7:
/usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/pthread.h:488:12: note: declared here
 extern int __REDIRECT_NTH (pthread_yield, (void), sched_yield)
            ^
Compiling  misc/utils.cc                       > /home/ye/tool/marian/build/local/obj/misc/utils.o
[ 48%] Building CXX object src/3rd_party/faiss/CMakeFiles/faiss.dir/utils/random.cpp.o
Compiling  misc/argcheck.cc                    > /home/ye/tool/marian/build/local/obj/misc/argcheck.o
misc/ibvwrap.cc: In function ‘ncclResult_t wrap_ibv_symbols()’:
misc/ibvwrap.cc:51:55: warning: ‘int pthread_yield()’ is deprecated: pthread_yield is deprecated, use sched_yield instead [-Wdeprecated-declarations]
     while (ibvState == ibvInitializing) pthread_yield();
                                                       ^
In file included from /usr/include/features.h:502:0,
                 from /usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/pthread.h:30,
                 from include/core.h:10,
                 from include/ibvwrap.h:15,
                 from misc/ibvwrap.cc:7:
/usr/local/lib/gcc/x86_64-pc-linux-gnu/7.5.0/include-fixed/pthread.h:488:12: note: declared here
 extern int __REDIRECT_NTH (pthread_yield, (void), sched_yield)
            ^
Compiling  transport/p2p.cc                    > /home/ye/tool/marian/build/local/obj/transport/p2p.o
Compiling  transport/shm.cc                    > /home/ye/tool/marian/build/local/obj/transport/shm.o
Compiling  transport/net.cc                    > /home/ye/tool/marian/build/local/obj/transport/net.o
Compiling  transport/net_socket.cc             > /home/ye/tool/marian/build/local/obj/transport/net_socket.o
Compiling  transport/net_ib.cc                 > /home/ye/tool/marian/build/local/obj/transport/net_ib.o
Compiling  transport/coll_net.cc               > /home/ye/tool/marian/build/local/obj/transport/coll_net.o
Compiling  collectives/sendrecv.cc             > /home/ye/tool/marian/build/local/obj/collectives/sendrecv.o
Compiling  collectives/all_reduce.cc           > /home/ye/tool/marian/build/local/obj/collectives/all_reduce.o
Compiling  collectives/all_gather.cc           > /home/ye/tool/marian/build/local/obj/collectives/all_gather.o
Compiling  collectives/broadcast.cc            > /home/ye/tool/marian/build/local/obj/collectives/broadcast.o
Compiling  collectives/reduce.cc               > /home/ye/tool/marian/build/local/obj/collectives/reduce.o
Compiling  collectives/reduce_scatter.cc       > /home/ye/tool/marian/build/local/obj/collectives/reduce_scatter.o
[ 48%] Built target libyaml-cpp
Compiling  graph/topo.cc                       > /home/ye/tool/marian/build/local/obj/graph/topo.o
Compiling  graph/paths.cc                      > /home/ye/tool/marian/build/local/obj/graph/paths.o
Compiling  graph/search.cc                     > /home/ye/tool/marian/build/local/obj/graph/search.o
Compiling  graph/connect.cc                    > /home/ye/tool/marian/build/local/obj/graph/connect.o
Compiling  graph/rings.cc                      > /home/ye/tool/marian/build/local/obj/graph/rings.o
Compiling  graph/trees.cc                      > /home/ye/tool/marian/build/local/obj/graph/trees.o
Compiling  graph/tuning.cc                     > /home/ye/tool/marian/build/local/obj/graph/tuning.o
Compiling  graph/xml.cc                        > /home/ye/tool/marian/build/local/obj/graph/xml.o
Generating rules                               > /home/ye/tool/marian/build/local/obj/collectives/device/Makefile.rules
[ 48%] Linking CXX static library libsentencepiece.a
[ 48%] Built target sentencepiece-static
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i8.o
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_encode.dir/spm_encode_main.cc.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_u64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f16.o
[ 49%] Built target faiss
[ 49%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_decode.dir/spm_decode_main.cc.o
[ 50%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_export_vocab.dir/spm_export_vocab_main.cc.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_sum_f64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u32.o
[ 50%] Linking CXX executable ../../../../spm_export_vocab
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_u64.o
[ 50%] Built target spm_export_vocab
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_prod_f64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i8.o
[ 50%] Linking CXX executable ../../../../spm_encode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u8.o
[ 50%] Linking CXX executable ../../../../spm_decode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i32.o
[ 50%] Built target spm_encode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u32.o
[ 50%] Built target spm_decode
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_u64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_min_f64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u8.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_i64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_u64.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f16.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f32.o
Compiling  sendrecv.cu                         > /home/ye/tool/marian/build/local/obj/collectives/device/sendrecv_max_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_sum_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_prod_f64.o
[ 50%] Built target SQLiteCpp
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_min_f64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u8.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_i64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_u64.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f16.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f32.o
Compiling  all_reduce.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_reduce_max_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_sum_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_prod_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_min_f64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u8.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u32.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_i64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_u64.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f16.o
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f32.o
[ 51%] Linking CXX static library libsentencepiece_train.a
Compiling  all_gather.cu                       > /home/ye/tool/marian/build/local/obj/collectives/device/all_gather_max_f64.o
[ 51%] Built target sentencepiece_train-static
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_sum_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i32.o
[ 51%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_normalize.dir/spm_normalize_main.cc.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_i64.o
[ 51%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/spm_train.dir/spm_train_main.cc.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_prod_f64.o
[ 52%] Linking CXX executable ../../../../spm_normalize
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u8.o
[ 52%] Built target spm_normalize
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f32.o
[ 53%] Linking CXX executable ../../../../spm_train
[ 53%] Built target spm_train
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_min_f64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u8.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_i64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_u64.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f16.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f32.o
Compiling  broadcast.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/broadcast_max_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_sum_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_prod_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_min_f64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u8.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_i64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_u64.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f16.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f32.o
Compiling  reduce.cu                           > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_max_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_sum_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_prod_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_min_f64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u8.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_i64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_u64.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f16.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f32.o
Compiling  reduce_scatter.cu                   > /home/ye/tool/marian/build/local/obj/collectives/device/reduce_scatter_max_f64.o
Compiling  functions.cu                        > /home/ye/tool/marian/build/local/obj/collectives/device/functions.o
Archiving  objects                             > /home/ye/tool/marian/build/local/obj/collectives/device/colldevice.a
Linking    libnccl.so.2.8.3                    > /home/ye/tool/marian/build/local/lib/libnccl.so.2.8.3
Archiving  libnccl_static.a                    > /home/ye/tool/marian/build/local/lib/libnccl_static.a
/home/ye/tool/marian/src/3rd_party/nccl/src
[ 53%] No install step for 'nccl_install'
[ 54%] Completed 'nccl_install'
[ 54%] Built target nccl_install
[ 54%] Built target 3rd_party_installs
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_cudnn_wrappers.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_add_all.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/translator/marian_cuda_generated_nth_element.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_algorithm.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_add.cu.o
[ 55%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_element.cu.o
[ 56%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_hash.cu.o
[ 57%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_device.cu.o
[ 57%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_prod.cu.o
[ 58%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_tensor_operators.cu.o
[ 58%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/tensors/gpu/marian_cuda_generated_topk.cu.o
[ 59%] Building NVCC (Device) object src/CMakeFiles/marian_cuda.dir/translator/marian_cuda_generated_helpers.cu.o
[ 60%] Building CXX object src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod_sparse.cpp.o
[ 60%] Building CXX object src/CMakeFiles/marian_cuda.dir/tensors/gpu/prod.cpp.o
[ 60%] Linking CXX static library libmarian_cuda.a
[ 60%] Built target marian_cuda
[ 60%] Building CXX object src/CMakeFiles/marian.dir/common/version.cpp.o
[ 62%] Building CXX object src/CMakeFiles/marian.dir/common/cli_wrapper.cpp.o
[ 62%] Building CXX object src/CMakeFiles/marian.dir/common/fastopt.cpp.o
[ 62%] Building CXX object src/CMakeFiles/marian.dir/common/aliases.cpp.o
[ 63%] Building CXX object src/CMakeFiles/marian.dir/common/logging.cpp.o
[ 63%] Building CXX object src/CMakeFiles/marian.dir/common/utils.cpp.o
[ 63%] Building CXX object src/CMakeFiles/marian.dir/common/cli_helper.cpp.o
[ 64%] Building CXX object src/CMakeFiles/marian.dir/common/build_info.cpp.o
[ 64%] Building CXX object src/CMakeFiles/marian.dir/common/config_parser.cpp.o
[ 64%] Building CXX object src/CMakeFiles/marian.dir/common/config.cpp.o
[ 64%] Building CXX object src/CMakeFiles/marian.dir/common/io.cpp.o
[ 64%] Building CXX object src/CMakeFiles/marian.dir/common/config_validator.cpp.o
[ 65%] Building CXX object src/CMakeFiles/marian.dir/common/filesystem.cpp.o
[ 65%] Building CXX object src/CMakeFiles/marian.dir/common/file_stream.cpp.o
[ 66%] Building CXX object src/CMakeFiles/marian.dir/common/options.cpp.o
[ 66%] Building CXX object src/CMakeFiles/marian.dir/common/file_utils.cpp.o
[ 67%] Building CXX object src/CMakeFiles/marian.dir/common/binary.cpp.o
[ 68%] Building CXX object src/CMakeFiles/marian.dir/common/signal_handling.cpp.o
[ 68%] Building CXX object src/CMakeFiles/marian.dir/common/types.cpp.o
[ 68%] Building CXX object src/CMakeFiles/marian.dir/data/alignment.cpp.o
[ 68%] Building CXX object src/CMakeFiles/marian.dir/data/vocab.cpp.o
[ 68%] Building CXX object src/CMakeFiles/marian.dir/data/default_vocab.cpp.o
[ 69%] Building CXX object src/CMakeFiles/marian.dir/data/sentencepiece_vocab.cpp.o
[ 69%] Building CXX object src/CMakeFiles/marian.dir/data/factored_vocab.cpp.o
[ 70%] Building CXX object src/CMakeFiles/marian.dir/data/corpus_base.cpp.o
[ 70%] Building CXX object src/CMakeFiles/marian.dir/data/corpus.cpp.o
[ 70%] Building CXX object src/CMakeFiles/marian.dir/data/corpus_sqlite.cpp.o
[ 71%] Building CXX object src/CMakeFiles/marian.dir/data/corpus_nbest.cpp.o
[ 71%] Building CXX object src/CMakeFiles/marian.dir/data/text_input.cpp.o
[ 72%] Building CXX object src/CMakeFiles/marian.dir/data/shortlist.cpp.o
[ 72%] Building CXX object src/CMakeFiles/marian.dir/3rd_party/cnpy/cnpy.cpp.o
[ 72%] Building CXX object src/CMakeFiles/marian.dir/3rd_party/ExceptionWithCallStack.cpp.o
[ 73%] Building CXX object src/CMakeFiles/marian.dir/3rd_party/onnx/protobuf/onnx-ml.pb-wrapper.cpp.o
[ 73%] Building CXX object src/CMakeFiles/marian.dir/3rd_party/phf/phf.cc.o
[ 74%] Building CXX object src/CMakeFiles/marian.dir/tensors/backend.cpp.o
[ 74%] Building CXX object src/CMakeFiles/marian.dir/tensors/rand.cpp.o
[ 74%] Building CXX object src/CMakeFiles/marian.dir/tensors/tensor.cpp.o
[ 75%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/device.cpp.o
[ 75%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/prod.cpp.o
[ 76%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/topk.cpp.o
[ 76%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/tensor_operators.cpp.o
[ 76%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/integer_common.cpp.o
[ 77%] Building CXX object src/CMakeFiles/marian.dir/tensors/cpu/fbgemm/packed_gemm.cpp.o
[ 77%] Building CXX object src/CMakeFiles/marian.dir/graph/expression_graph.cpp.o
[ 78%] Building CXX object src/CMakeFiles/marian.dir/graph/expression_operators.cpp.o
[ 78%] Building CXX object src/CMakeFiles/marian.dir/graph/node.cpp.o
[ 78%] Building CXX object src/CMakeFiles/marian.dir/graph/node_operators.cpp.o
[ 79%] Building CXX object src/CMakeFiles/marian.dir/graph/node_initializers.cpp.o
[ 79%] Building CXX object src/CMakeFiles/marian.dir/onnx/expression_graph_onnx_exporter.cpp.o
[ 80%] Building CXX object src/CMakeFiles/marian.dir/onnx/expression_graph_onnx_serialization.cpp.o
[ 80%] Building CXX object src/CMakeFiles/marian.dir/layers/convolution.cpp.o
[ 80%] Building CXX object src/CMakeFiles/marian.dir/layers/generic.cpp.o
[ 81%] Building CXX object src/CMakeFiles/marian.dir/layers/loss.cpp.o
[ 81%] Building CXX object src/CMakeFiles/marian.dir/layers/weight.cpp.o
[ 81%] Building CXX object src/CMakeFiles/marian.dir/layers/embedding.cpp.o
[ 82%] Building CXX object src/CMakeFiles/marian.dir/layers/output.cpp.o
[ 82%] Building CXX object src/CMakeFiles/marian.dir/layers/logits.cpp.o
[ 83%] Building CXX object src/CMakeFiles/marian.dir/layers/lsh.cpp.o
[ 83%] Building CXX object src/CMakeFiles/marian.dir/rnn/cells.cpp.o
[ 83%] Building CXX object src/CMakeFiles/marian.dir/rnn/attention.cpp.o
[ 84%] Building CXX object src/CMakeFiles/marian.dir/optimizers/quantizer.cpp.o
[ 84%] Building CXX object src/CMakeFiles/marian.dir/optimizers/clippers.cpp.o
[ 85%] Building CXX object src/CMakeFiles/marian.dir/optimizers/optimizers.cpp.o
[ 85%] Building CXX object src/CMakeFiles/marian.dir/optimizers/exponential_smoothing.cpp.o
[ 85%] Building CXX object src/CMakeFiles/marian.dir/models/model_factory.cpp.o
[ 86%] Building CXX object src/CMakeFiles/marian.dir/models/encoder_decoder.cpp.o
[ 86%] Building CXX object src/CMakeFiles/marian.dir/models/transformer_stub.cpp.o
[ 87%] Building CXX object src/CMakeFiles/marian.dir/models/costs.cpp.o
[ 87%] Building CXX object src/CMakeFiles/marian.dir/rescorer/score_collector.cpp.o
[ 87%] Building CXX object src/CMakeFiles/marian.dir/embedder/vector_collector.cpp.o
[ 88%] Building CXX object src/CMakeFiles/marian.dir/translator/beam_search.cpp.o
[ 88%] Building CXX object src/CMakeFiles/marian.dir/translator/history.cpp.o
[ 89%] Building CXX object src/CMakeFiles/marian.dir/translator/output_collector.cpp.o
[ 89%] Building CXX object src/CMakeFiles/marian.dir/translator/output_printer.cpp.o
[ 89%] Building CXX object src/CMakeFiles/marian.dir/translator/nth_element.cpp.o
[ 90%] Building CXX object src/CMakeFiles/marian.dir/translator/helpers.cpp.o
[ 90%] Building CXX object src/CMakeFiles/marian.dir/translator/scorers.cpp.o
[ 91%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group_async.cpp.o
[ 91%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group_sync.cpp.o
[ 91%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group.cpp.o
[ 92%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group_singleton.cpp.o
[ 92%] Building CXX object src/CMakeFiles/marian.dir/training/validator.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/training/communicator.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/microsoft/quicksand.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/microsoft/sentencepiece.cpp.o
[ 94%] Building CXX object src/CMakeFiles/marian.dir/microsoft/cosmos.cpp.o
[ 94%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/Converter.cpp.o
[ 94%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/StringUtils.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/ParameterTree.cpp.o
[ 95%] Linking CXX static library ../libmarian.a
[ 95%] Built target marian
[ 95%] Building CXX object src/CMakeFiles/marian_train.dir/command/marian_main.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian_decoder.dir/command/marian_decoder.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian_scorer.dir/command/marian_scorer.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian_vocab.dir/command/marian_vocab.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_conv.dir/command/marian_conv.cpp.o
[ 97%] Linking CXX executable ../marian-vocab
[ 97%] Built target marian_vocab
[ 98%] Linking CXX executable ../marian-decoder
[ 98%] Linking CXX executable ../marian-conv
[ 99%] Linking CXX executable ../marian-scorer
[ 99%] Built target marian_conv
[ 99%] Built target marian_decoder
[ 99%] Built target marian_scorer
[100%] Linking CXX executable ../marian
[100%] Built target marian_train
ye@lst-hpc3090:~/tool/marian/build$ 
```

I used gcc 9.5:  

```
ye@lst-hpc3090:~/tool/marian/build$ gcc --version
gcc (Ubuntu 9.5.0-4ubuntu2) 9.5.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

ye@lst-hpc3090:~/tool/marian/build$
```

## Confirmed with --help  

```
ye@lst-hpc3090:~/tool/marian/build$ ./marian --help
Marian: Fast Neural Machine Translation in C++
Usage: ./marian [OPTIONS]

General options:
  -h,--help                             Print this help message and exit
  --version                             Print the version number and exit
  --authors                             Print list of authors and exit
  --cite                                Print citation and exit
  --build-info TEXT                     Print CMake build options and exit. Set to 'all' to print advanced options
  -c,--config VECTOR ...                Configuration file(s). If multiple, later overrides earlier
  -w,--workspace INT=2048               Preallocate arg MB of work space. Negative `--workspace -N` value allocates workspace as total available GPU memory minus N megabytes.
  --log TEXT                            Log training process information to file given by arg
  --log-level TEXT=info                 Set verbosity level of logging: trace, debug, info, warn, err(or), critical, off
  --log-time-zone TEXT                  Set time zone for the date shown on logging
  --quiet                               Suppress all logging to stderr. Logging to files still works
  --quiet-translation                   Suppress logging for translation
  --seed UINT                           Seed for all random number generators. 0 means initialize randomly
  --check-nan                           Check for NaNs or Infs in forward and backward pass. Will abort when found. This is a diagnostic option that will slow down computation significantly
  --interpolate-env-vars                allow the use of environment variables in paths, of the form ${VAR_NAME}
  --relative-paths                      All paths are relative to the config file location
  --dump-config TEXT                    Dump current (modified) configuration to stdout and exit. Possible values: full, minimal, expand
  --sigterm TEXT=save-and-exit          What to do with SIGTERM: save-and-exit or exit-immediately.


Model options:
  -m,--model TEXT=model.npz             Path prefix for model to be saved/resumed. Supported file extensions: .npz, .bin
  --pretrained-model TEXT               Path prefix for pre-trained model to initialize model weights
  --ignore-model-config                 Ignore the model configuration saved in npz file
  --type TEXT=amun                      Model type: amun, nematus, s2s, multi-s2s, transformer
  --dim-vocabs VECTOR=0,0 ...           Maximum items in vocabulary ordered by rank, 0 uses all items in the provided/created vocabulary file
  --dim-emb INT=512                     Size of embedding vector
  --factors-dim-emb INT                 Embedding dimension of the factors. Only used if concat is selected as factors combining form
  --factors-combine TEXT=sum            How to combine the factors and lemma embeddings. Options available: sum, concat
  --lemma-dependency TEXT               Lemma dependency method to use when predicting target factors. Options: soft-transformer-layer, hard-transformer-layer, lemma-dependent-bias, re-embedding
  --lemma-dim-emb INT=0                 Re-embedding dimension of lemma in factors
  --dim-rnn INT=1024                    Size of rnn hidden state
  --enc-type TEXT=bidirectional         Type of encoder RNN : bidirectional, bi-unidirectional, alternating (s2s)
  --enc-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --enc-cell-depth INT=1                Number of transitional cells in encoder layers (s2s)
  --enc-depth INT=1                     Number of encoder layers (s2s)
  --dec-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --dec-cell-base-depth INT=2           Number of transitional cells in first decoder layer (s2s)
  --dec-cell-high-depth INT=1           Number of transitional cells in next decoder layers (s2s)
  --dec-depth INT=1                     Number of decoder layers (s2s)
  --skip                                Use skip connections (s2s)
  --layer-normalization                 Enable layer normalization
  --right-left                          Train right-to-left model
  --input-types VECTOR ...              Provide type of input data if different than 'sequence'. Possible values: sequence, class, alignment, weight. You need to provide one type per input file (if --train-sets) or per TSV field (if --tsv).
  --best-deep                           Use Edinburgh deep RNN configuration (s2s)
  --tied-embeddings                     Tie target embeddings and output embeddings in output layer
  --tied-embeddings-src                 Tie source and target embeddings
  --tied-embeddings-all                 Tie all embedding layers and output layer
  --output-omit-bias                    Do not use a bias vector in decoder output layer
  --transformer-heads INT=8             Number of heads in multi-head attention (transformer)
  --transformer-no-projection           Omit linear projection after multi-head attention (transformer)
  --transformer-rnn-projection          Add linear projection after rnn layer (transformer)
  --transformer-pool                    Pool encoder states instead of using cross attention (selects first encoder state, best used with special token)
  --transformer-dim-ffn INT=2048        Size of position-wise feed-forward network (transformer)
  --transformer-decoder-dim-ffn INT=0   Size of position-wise feed-forward network in decoder (transformer). Uses --transformer-dim-ffn if 0.
  --transformer-ffn-depth INT=2         Depth of filters (transformer)
  --transformer-decoder-ffn-depth INT=0 Depth of filters in decoder (transformer). Uses --transformer-ffn-depth if 0
  --transformer-ffn-activation TEXT=swish
                                        Activation between filters: swish or relu (transformer)
  --transformer-dim-aan INT=2048        Size of position-wise feed-forward network in AAN (transformer)
  --transformer-aan-depth INT=2         Depth of filter for AAN (transformer)
  --transformer-aan-activation TEXT=swish
                                        Activation between filters in AAN: swish or relu (transformer)
  --transformer-aan-nogate              Omit gate in AAN (transformer)
  --transformer-decoder-autoreg TEXT=self-attention
                                        Type of autoregressive layer in transformer decoder: self-attention, average-attention (transformer)
  --transformer-tied-layers VECTOR ...  List of tied decoder layers (transformer)
  --transformer-guided-alignment-layer TEXT=last
                                        Last or number of layer to use for guided alignment training in transformer
  --transformer-preprocess TEXT         Operation before each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-emb TEXT=d  Operation after transformer embedding layer: d = dropout, a = add, n = normalize
  --transformer-postprocess TEXT=dan    Operation after each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-top TEXT    Final operation after a full transformer stack: d = dropout, a = add, n = normalize. The optional skip connection with 'a' by-passes the entire stack.
  --transformer-train-position-embeddings
                                        Train positional embeddings instead of using static sinusoidal embeddings
  --transformer-depth-scaling           Scale down weight initialization in transformer layers by 1 / sqrt(depth)
  --bert-mask-symbol TEXT=[MASK]        Masking symbol for BERT masked-LM training
  --bert-sep-symbol TEXT=[SEP]          Sentence separator symbol for BERT next sentence prediction training
  --bert-class-symbol TEXT=[CLS]        Class symbol BERT classifier training
  --bert-masking-fraction FLOAT=0.15    Fraction of masked out tokens during training
  --bert-train-type-embeddings=true     Train bert type embeddings, set to false to use static sinusoidal embeddings
  --bert-type-vocab-size INT=2          Size of BERT type vocab (sentence A and B)
  --dropout-rnn FLOAT                   Scaling dropout along rnn layers and time (0 = no dropout)
  --dropout-src FLOAT                   Dropout source words (0 = no dropout)
  --dropout-trg FLOAT                   Dropout target words (0 = no dropout)
  --transformer-dropout FLOAT           Dropout between transformer layers (0 = no dropout)
  --transformer-dropout-attention FLOAT Dropout for transformer attention (0 = no dropout)
  --transformer-dropout-ffn FLOAT       Dropout for transformer filter (0 = no dropout)


Training options:
  --cost-type TEXT=ce-sum               Optimization criterion: ce-mean, ce-mean-words, ce-sum, perplexity
  --multi-loss-type TEXT=sum            How to accumulate multi-objective losses: sum, scaled, mean
  --unlikelihood-loss                   Use word-level weights as indicators for sequence-level unlikelihood training
  --overwrite                           Do not create model checkpoints, only overwrite main model file with last checkpoint. Reduces disk usage
  --no-reload                           Do not load existing model specified in --model arg
  -t,--train-sets VECTOR ...            Paths to training corpora: source target
  -v,--vocabs VECTOR ...                Paths to vocabulary files have to correspond to --train-sets. If this parameter is not supplied we look for vocabulary files source.{yml,json} and target.{yml,json}. If these files do not exist they are created
  --sentencepiece-alphas VECTOR ...     Sampling factors for SentencePiece vocabulary; i-th factor corresponds to i-th vocabulary
  --sentencepiece-options TEXT          Pass-through command-line options to SentencePiece trainer
  --sentencepiece-max-lines UINT=2000000
                                        Maximum lines to train SentencePiece vocabulary, selected with sampling from all data. When set to 0 all lines are going to be used.
  -e,--after-epochs UINT                Finish after this many epochs, 0 is infinity (deprecated, '--after-epochs N' corresponds to '--after Ne')
  --after-batches UINT                  Finish after this many batch updates, 0 is infinity (deprecated, '--after-batches N' corresponds to '--after Nu')
  -a,--after TEXT=0e                    Finish after this many chosen training units, 0 is infinity (e.g. 100e = 100 epochs, 10Gt = 10 billion target labels, 100Ku = 100,000 updates
  --disp-freq TEXT=1000u                Display information every arg updates (append 't' for every arg target labels)
  --disp-first UINT                     Display information for the first arg updates
  --disp-label-counts=true              Display label counts when logging loss progress
  --save-freq TEXT=10000u               Save model file every arg updates (append 't' for every arg target labels)
  --logical-epoch VECTOR=1e,0 ...       Redefine logical epoch counter as multiple of data epochs (e.g. 1e), updates (e.g. 100Ku) or labels (e.g. 1Gt). Second parameter defines width of fractional display, 0 by default.
  --max-length UINT=50                  Maximum length of a sentence in a training sentence pair
  --max-length-crop                     Crop a sentence to max-length instead of omitting it if longer than max-length
  --tsv                                 Tab-separated input
  --tsv-fields UINT                     Number of fields in the TSV input. By default, it is guessed based on the model type
  --shuffle TEXT=data                   How to shuffle input data (data: shuffles data and sorted batches; batches: data is read in order into batches, but batches are shuffled; none: no shuffling). Use with '--maxi-batch-sort none' in order to achieve exact reading order
  --no-shuffle                          Shortcut for backwards compatiblity, equivalent to --shuffle none (deprecated)
  --no-restore-corpus                   Skip restoring corpus state after training is restarted
  -T,--tempdir TEXT=/tmp                Directory for temporary (shuffled) files and database
  --sqlite TEXT                         Use disk-based sqlite3 database for training corpus storage, default is temporary with path creates persistent storage
  --sqlite-drop                         Drop existing tables in sqlite3 database
  -d,--devices VECTOR=0 ...             Specifies GPU ID(s) to use for training. Defaults to 0..num-devices-1
  --num-devices UINT                    Number of GPUs to use for this process. Defaults to length(devices) or 1
  --no-nccl                             Disable inter-GPU communication via NCCL
  --sharding TEXT=global                When using NCCL and MPI for multi-process training use 'global' (default, less memory usage) or 'local' (more memory usage but faster) sharding
  --sync-freq TEXT=200u                 When sharding is local sync all shards across processes once every n steps (possible units u=updates, t=target labels, e=epochs)
  --cpu-threads UINT=0                  Use CPU-based computation with this many independent threads, 0 means GPU-based computation
  --mini-batch INT=64                   Size of mini-batch used during update
  --mini-batch-words INT                Set mini-batch size based on words instead of sentences
  --mini-batch-fit                      Determine mini-batch size automatically based on sentence-length to fit reserved memory
  --mini-batch-fit-step UINT=10         Step size for mini-batch-fit statistics
  --gradient-checkpointing              Enable gradient-checkpointing to minimize memory usage
  --maxi-batch INT=100                  Number of batches to preload for length-based sorting
  --maxi-batch-sort TEXT=trg            Sorting strategy for maxi-batch: none, src, trg (not available for decoder)
  --shuffle-in-ram                      Keep shuffled corpus in RAM, do not write to temp file
  --data-threads UINT=8                 Number of concurrent threads to use during data reading and processing
  --all-caps-every UINT                 When forming minibatches, preprocess every Nth line on the fly to all-caps. Assumes UTF-8
  --english-title-case-every UINT       When forming minibatches, preprocess every Nth line on the fly to title-case. Assumes English (ASCII only)
  --mini-batch-words-ref UINT           If given, the following hyper parameters are adjusted as-if we had this mini-batch size: --learn-rate, --optimizer-params, --exponential-smoothing, --mini-batch-warmup
  --mini-batch-warmup TEXT=0            Linear ramp-up of MB size, up to this #updates (append 't' for up to this #target labels). Auto-adjusted to --mini-batch-words-ref if given
  --mini-batch-track-lr                 Dynamically track mini-batch size inverse to actual learning rate (not considering lr-warmup)
  --mini-batch-round-up=true            Round up batch size to next power of 2 for more efficient training, but this can make batch size less stable. Disable with --mini-batch-round-up=false
  -o,--optimizer TEXT=adam              Optimization algorithm: sgd, adagrad, adam
  --optimizer-params VECTOR ...         Parameters for optimization algorithm, e.g. betas for Adam. Auto-adjusted to --mini-batch-words-ref if given
  --optimizer-delay FLOAT=1             SGD update delay (#batches between updates). 1 = no delay. Can be fractional, e.g. 0.1 to use only 10% of each batch
  --sync-sgd                            Use synchronous SGD instead of asynchronous for multi-gpu training
  -l,--learn-rate FLOAT=0.0001          Learning rate. Auto-adjusted to --mini-batch-words-ref if given
  --lr-report                           Report learning rate for each update
  --lr-decay FLOAT                      Per-update decay factor for learning rate: lr <- lr * arg (0 to disable)
  --lr-decay-strategy TEXT=epoch+stalled
                                        Strategy for learning rate decaying: epoch, batches, stalled, epoch+batches, epoch+stalled
  --lr-decay-start VECTOR=10,1 ...      The first number of (epoch, batches, stalled) validations to start learning rate decaying (tuple)
  --lr-decay-freq UINT=50000            Learning rate decaying frequency for batches, requires --lr-decay-strategy to be batches
  --lr-decay-reset-optimizer            Reset running statistics of optimizer whenever learning rate decays
  --lr-decay-repeat-warmup              Repeat learning rate warmup when learning rate is decayed
  --lr-decay-inv-sqrt VECTOR=0 ...      Decrease learning rate at arg / sqrt(no. batches) starting at arg (append 't' or 'e' for sqrt(target labels or epochs)). Add second argument to define the starting point (default: same as first value)
  --lr-warmup TEXT=0                    Increase learning rate linearly for arg first batches (append 't' for arg first target labels)
  --lr-warmup-start-rate FLOAT          Start value for learning rate warmup
  --lr-warmup-cycle                     Apply cyclic warmup
  --lr-warmup-at-reload                 Repeat warmup after interrupted training
  --label-smoothing FLOAT               Epsilon for label smoothing (0 to disable)
  --factor-weight FLOAT=1               Weight for loss function for factors (factored vocab only) (1 to disable)
  --clip-norm FLOAT=1                   Clip gradient norm to arg (0 to disable)
  --exponential-smoothing FLOAT=0       Maintain smoothed version of parameters for validation and saving with smoothing factor. 0 to disable. Auto-adjusted to --mini-batch-words-ref if given.
  --guided-alignment TEXT=none          Path to a file with word alignments. Use guided alignment to guide attention or 'none'. If --tsv it specifies the index of a TSV field that contains the alignments (0-based)
  --guided-alignment-cost TEXT=ce       Cost type for guided alignment: ce (cross-entropy), mse (mean square error), mult (multiplication)
  --guided-alignment-weight FLOAT=0.1   Weight for guided alignment cost
  --data-weighting TEXT                 Path to a file with sentence or word weights. If --tsv it specifies the index of a TSV field that contains the weights (0-based)
  --data-weighting-type TEXT=sentence   Processing level for data weighting: sentence, word
  --embedding-vectors VECTOR ...        Paths to files with custom source and target embedding vectors
  --embedding-normalization             Normalize values from custom embedding vectors to [-1, 1]
  --embedding-fix-src                   Fix source embeddings. Affects all encoders
  --embedding-fix-trg                   Fix target embeddings. Affects all decoders
  --fp16                                Shortcut for mixed precision training with float16 and cost-scaling, corresponds to: --precision float16 float32 --cost-scaling 8.f 10000 1.f 8.f
  --precision VECTOR=float32,float32 ...
                                        Mixed precision training for forward/backward pass and optimizaton. Defines types for: forward/backward pass, optimization.
  --cost-scaling VECTOR ...             Dynamic cost scaling for mixed precision training: scaling factor, frequency, multiplier, minimum factor
  --gradient-norm-average-window UINT=100
                                        Window size over which the exponential average of the gradient norm is recorded (for logging and scaling). After this many updates about 90% of the mass of the exponential average comes from these updates
  --dynamic-gradient-scaling VECTOR ... Re-scale gradient to have average gradient norm if (log) gradient norm diverges from average by arg1 sigmas. If arg2 = "log" the statistics are recorded for the log of the gradient norm else use plain norm
  --check-gradient-nan                  Skip parameter update in case of NaNs in gradient
  --normalize-gradient                  Normalize gradient by multiplying with no. devices / total labels (not recommended and to be removed in the future)
  --train-embedder-rank VECTOR ...      Override model configuration and train a embedding similarity ranker with the model encoder, parameters encode margin and an optional normalization factor
  --quantize-bits UINT=0                Number of bits to compress model to. Set to 0 to disable
  --quantize-optimization-steps UINT=0  Adjust quantization scaling factor for N steps
  --quantize-log-based                  Uses log-based quantization
  --quantize-biases                     Apply quantization to biases
  --ulr                                 Enable ULR (Universal Language Representation)
  --ulr-query-vectors TEXT              Path to file with universal sources embeddings from projection into universal space
  --ulr-keys-vectors TEXT               Path to file with universal sources embeddings of target keys from projection into universal space
  --ulr-trainable-transformation        Make Query Transformation Matrix A trainable
  --ulr-dim-emb INT                     ULR monolingual embeddings dimension
  --ulr-dropout FLOAT=0                 ULR dropout on embeddings attentions. Default is no dropout
  --ulr-softmax-temperature FLOAT=1     ULR softmax temperature to control randomness of predictions. Deafult is 1.0: no temperature
  --task VECTOR ...                     Use predefined set of options. Possible values: transformer-base, transformer-big, transformer-base-prenorm, transformer-big-prenorm


Validation set options:
  --valid-sets VECTOR ...               Paths to validation corpora: source target
  --valid-freq TEXT=10000u              Validate model every arg updates (append 't' for every arg target labels)
  --valid-metrics VECTOR=cross-entropy ...
                                        Metric to use during validation: cross-entropy, ce-mean-words, perplexity, valid-script, translation, bleu, bleu-detok (deprecated, same as bleu), bleu-segmented, chrf. Multiple metrics can be specified
  --valid-reset-stalled                 Reset stalled validation metrics when the training is restarted
  --valid-reset-all                     Reset all validation metrics when the training is restarted
  --early-stopping UINT=10              Stop if the first validation metric does not improve for arg consecutive validation steps
  --early-stopping-on TEXT=first        Decide if early stopping should take into account first, all, or any validation metricsPossible values: first, all, any
  -b,--beam-size UINT=12                Beam size used during search with validating translator
  -n,--normalize FLOAT=0                Divide translation score by pow(translation length, arg)
  --max-length-factor FLOAT=3           Maximum target length as source length times factor
  --word-penalty FLOAT                  Subtract (arg * translation length) from translation score
  --allow-unk                           Allow unknown words to appear in output
  --n-best                              Generate n-best list
  --word-scores                         Print word-level scores. One score per subword unit, not normalized even if --normalize
  --valid-mini-batch INT=32             Size of mini-batch used during validation
  --valid-max-length UINT=1000          Maximum length of a sentence in a validating sentence pair. Sentences longer than valid-max-length are cropped to valid-max-length
  --valid-script-path TEXT              Path to external validation script. It should print a single score to stdout. If the option is used with validating translation, the output translation file will be passed as a first argument
  --valid-script-args VECTOR ...        Additional args passed to --valid-script-path. These are inserted between the script path and the output translation-file path
  --valid-translation-output TEXT       (Template for) path to store the translation. E.g., validation-output-after-{U}-updates-{T}-tokens.txt. Template parameters: {E} for epoch; {B} for No. of batches within epoch; {U} for total No. of updates; {T} for total No. of tokens seen.
  --keep-best                           Keep best model for each validation metric
  --valid-log TEXT                      Log validation scores to file given by arg
ye@lst-hpc3090:~/tool/marian/build$
```

vocab building command ...  

```
ye@lst-hpc3090:~/tool/marian/build$ ./marian-vocab --help
Create a vocabulary from text corpora given on STDIN
Usage: ./marian-vocab [OPTIONS]

Allowed options:
  -h,--help                             Print this help message and exit
  --version                             Print the version number and exit
  -m,--max-size UINT=0                  Generate only UINT most common vocabulary items

Examples:
  ./marian-vocab < text.src > vocab.yml
  cat text.src text.trg | ./marian-vocab > vocab.yml
ye@lst-hpc3090:~/tool/marian/build$ 
```

decoding command ...  

```
ye@lst-hpc3090:~/tool/marian/build$ ./marian-decoder --help
Marian: Fast Neural Machine Translation in C++
Usage: ./marian-decoder [OPTIONS]

General options:
  -h,--help                             Print this help message and exit
  --version                             Print the version number and exit
  --authors                             Print list of authors and exit
  --cite                                Print citation and exit
  --build-info TEXT                     Print CMake build options and exit. Set to 'all' to print advanced options
  -c,--config VECTOR ...                Configuration file(s). If multiple, later overrides earlier
  -w,--workspace INT=512                Preallocate arg MB of work space. Negative `--workspace -N` value allocates workspace as total available GPU memory minus N megabytes.
  --log TEXT                            Log training process information to file given by arg
  --log-level TEXT=info                 Set verbosity level of logging: trace, debug, info, warn, err(or), critical, off
  --log-time-zone TEXT                  Set time zone for the date shown on logging
  --quiet                               Suppress all logging to stderr. Logging to files still works
  --quiet-translation                   Suppress logging for translation
  --seed UINT                           Seed for all random number generators. 0 means initialize randomly
  --check-nan                           Check for NaNs or Infs in forward and backward pass. Will abort when found. This is a diagnostic option that will slow down computation significantly
  --interpolate-env-vars                allow the use of environment variables in paths, of the form ${VAR_NAME}
  --relative-paths                      All paths are relative to the config file location
  --dump-config TEXT                    Dump current (modified) configuration to stdout and exit. Possible values: full, minimal, expand


Model options:
  -m,--models VECTOR ...                Paths to model(s) to be loaded. Supported file extensions: .npz, .bin
  --model-mmap                          Use memory-mapping when loading model (CPU only)
  --ignore-model-config                 Ignore the model configuration saved in npz file
  --type TEXT=amun                      Model type: amun, nematus, s2s, multi-s2s, transformer
  --dim-vocabs VECTOR=0,0 ...           Maximum items in vocabulary ordered by rank, 0 uses all items in the provided/created vocabulary file
  --dim-emb INT=512                     Size of embedding vector
  --factors-dim-emb INT                 Embedding dimension of the factors. Only used if concat is selected as factors combining form
  --factors-combine TEXT=sum            How to combine the factors and lemma embeddings. Options available: sum, concat
  --lemma-dependency TEXT               Lemma dependency method to use when predicting target factors. Options: soft-transformer-layer, hard-transformer-layer, lemma-dependent-bias, re-embedding
  --lemma-dim-emb INT=0                 Re-embedding dimension of lemma in factors
  --dim-rnn INT=1024                    Size of rnn hidden state
  --enc-type TEXT=bidirectional         Type of encoder RNN : bidirectional, bi-unidirectional, alternating (s2s)
  --enc-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --enc-cell-depth INT=1                Number of transitional cells in encoder layers (s2s)
  --enc-depth INT=1                     Number of encoder layers (s2s)
  --dec-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --dec-cell-base-depth INT=2           Number of transitional cells in first decoder layer (s2s)
  --dec-cell-high-depth INT=1           Number of transitional cells in next decoder layers (s2s)
  --dec-depth INT=1                     Number of decoder layers (s2s)
  --skip                                Use skip connections (s2s)
  --layer-normalization                 Enable layer normalization
  --right-left                          Train right-to-left model
  --input-types VECTOR ...              Provide type of input data if different than 'sequence'. Possible values: sequence, class, alignment, weight. You need to provide one type per input file (if --train-sets) or per TSV field (if --tsv).
  --best-deep                           Use Edinburgh deep RNN configuration (s2s)
  --tied-embeddings                     Tie target embeddings and output embeddings in output layer
  --tied-embeddings-src                 Tie source and target embeddings
  --tied-embeddings-all                 Tie all embedding layers and output layer
  --output-omit-bias                    Do not use a bias vector in decoder output layer
  --transformer-heads INT=8             Number of heads in multi-head attention (transformer)
  --transformer-no-projection           Omit linear projection after multi-head attention (transformer)
  --transformer-rnn-projection          Add linear projection after rnn layer (transformer)
  --transformer-pool                    Pool encoder states instead of using cross attention (selects first encoder state, best used with special token)
  --transformer-dim-ffn INT=2048        Size of position-wise feed-forward network (transformer)
  --transformer-decoder-dim-ffn INT=0   Size of position-wise feed-forward network in decoder (transformer). Uses --transformer-dim-ffn if 0.
  --transformer-ffn-depth INT=2         Depth of filters (transformer)
  --transformer-decoder-ffn-depth INT=0 Depth of filters in decoder (transformer). Uses --transformer-ffn-depth if 0
  --transformer-ffn-activation TEXT=swish
                                        Activation between filters: swish or relu (transformer)
  --transformer-dim-aan INT=2048        Size of position-wise feed-forward network in AAN (transformer)
  --transformer-aan-depth INT=2         Depth of filter for AAN (transformer)
  --transformer-aan-activation TEXT=swish
                                        Activation between filters in AAN: swish or relu (transformer)
  --transformer-aan-nogate              Omit gate in AAN (transformer)
  --transformer-decoder-autoreg TEXT=self-attention
                                        Type of autoregressive layer in transformer decoder: self-attention, average-attention (transformer)
  --transformer-tied-layers VECTOR ...  List of tied decoder layers (transformer)
  --transformer-guided-alignment-layer TEXT=last
                                        Last or number of layer to use for guided alignment training in transformer
  --transformer-preprocess TEXT         Operation before each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-emb TEXT=d  Operation after transformer embedding layer: d = dropout, a = add, n = normalize
  --transformer-postprocess TEXT=dan    Operation after each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-top TEXT    Final operation after a full transformer stack: d = dropout, a = add, n = normalize. The optional skip connection with 'a' by-passes the entire stack.
  --transformer-train-position-embeddings
                                        Train positional embeddings instead of using static sinusoidal embeddings
  --transformer-depth-scaling           Scale down weight initialization in transformer layers by 1 / sqrt(depth)
  --bert-mask-symbol TEXT=[MASK]        Masking symbol for BERT masked-LM training
  --bert-sep-symbol TEXT=[SEP]          Sentence separator symbol for BERT next sentence prediction training
  --bert-class-symbol TEXT=[CLS]        Class symbol BERT classifier training
  --bert-masking-fraction FLOAT=0.15    Fraction of masked out tokens during training
  --bert-train-type-embeddings=true     Train bert type embeddings, set to false to use static sinusoidal embeddings
  --bert-type-vocab-size INT=2          Size of BERT type vocab (sentence A and B)


Translator options:
  -i,--input VECTOR=stdin ...           Paths to input file(s), stdin by default
  -o,--output TEXT=stdout               Path to output file, stdout by default
  -v,--vocabs VECTOR ...                Paths to vocabulary files have to correspond to --input
  -b,--beam-size UINT=12                Beam size used during search with validating translator
  -n,--normalize FLOAT=0                Divide translation score by pow(translation length, arg)
  --max-length-factor FLOAT=3           Maximum target length as source length times factor
  --word-penalty FLOAT                  Subtract (arg * translation length) from translation score
  --allow-unk                           Allow unknown words to appear in output
  --allow-special                       Allow special symbols to appear in output, e.g. for SentencePiece with byte-fallback do not suppress the newline symbol
  --n-best                              Generate n-best list
  --alignment TEXT                      Return word alignment. Possible values: 0.0-1.0, hard, soft
  --force-decode                        Use force-decoding of given prefixes. Forces decoding to follow vocab IDs from last stream in the batch (or the first stream, if there is only one). Use either as `./marian-decoder --force-decode --input source.txt prefixes.txt [...]` where inputs and prefixes align on line-level or as `paste source.txt prefixes.txt | ./marian-decoder --force-decode --tsv --tsv-fields 2 [...]` when reading from stdin.
  --word-scores                         Print word-level scores. One score per subword unit, not normalized even if --normalize
  --stat-freq TEXT=0                    Display speed information every arg mini-batches. Disabled by default with 0, set to value larger than 0 to activate
  --no-spm-decode                       Keep the output segmented into SentencePiece subwords
  --max-length UINT=1000                Maximum length of a sentence in a training sentence pair
  --max-length-crop                     Crop a sentence to max-length instead of omitting it if longer than max-length
  --tsv                                 Tab-separated input
  --tsv-fields UINT                     Number of fields in the TSV input. By default, it is guessed based on the model type
  -d,--devices VECTOR=0 ...             Specifies GPU ID(s) to use for training. Defaults to 0..num-devices-1
  --num-devices UINT                    Number of GPUs to use for this process. Defaults to length(devices) or 1
  --cpu-threads UINT=0                  Use CPU-based computation with this many independent threads, 0 means GPU-based computation
  --mini-batch INT=1                    Size of mini-batch used during batched translation
  --mini-batch-words INT                Set mini-batch size based on words instead of sentences
  --maxi-batch INT=1                    Number of batches to preload for length-based sorting
  --maxi-batch-sort TEXT=none           Sorting strategy for maxi-batch: none, src, trg (not available for decoder)
  --data-threads UINT=8                 Number of concurrent threads to use during data reading and processing
  --fp16                                Shortcut for mixed precision inference with float16, corresponds to: --precision float16
  --precision VECTOR=float32 ...        Mixed precision for inference, set parameter type in expression graph
  --skip-cost                           Ignore model cost during translation, not recommended for beam-size > 1
  --shortlist VECTOR ...                Use softmax shortlist: path first best prune
  --weights VECTOR ...                  Scorer weights
  --output-sampling VECTOR ...          Noise output layer with gumbel noise. Implicit default is 'full 1.0' for sampling from full distribution with softmax temperature 1.0. Also accepts 'topk num temp' (e.g. topk 100 0.1) for top-100 sampling with temperature 0.1
  --output-approx-knn VECTOR ...        Use approximate knn search in output layer (currently only in transformer)
  --optimize=false                      Optimize the graph on-the-fly
  -g,--gemm-type TEXT=float32           GEMM Type to be used for on-line quantization/packing: float32, packed16, packed8
  --quantize-range FLOAT=0              Range for the on-line quantiziation of weight matrix in multiple of this range and standard deviation, 0.0 means min/max quantization
ye@lst-hpc3090:~/tool/marian/build$ 
```

Installation on a new OS successful!  

## Reference

1. [https://medium.com/@darrenjs/building-gcc-from-source-dcc368a3bb70](https://medium.com/@darrenjs/building-gcc-from-source-dcc368a3bb70)  
2. [https://gibsonic.org/tools/2019/08/08/gcc_building.html](https://gibsonic.org/tools/2019/08/08/gcc_building.html)  
3. [http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.5.0/](http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-7.5.0/)  

