# gtn (Gaph Transformer Network) Installation Log 

## Got Error

```
-- The CXX compiler identification is GNU 8.4.0
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for C++ include pthread.h
-- Looking for C++ include pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Check for working CUDA compiler: /usr/bin/nvcc
-- Check for working CUDA compiler: /usr/bin/nvcc -- works
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
CMake Error at gtn/cuda/CMakeLists.txt:1 (cmake_minimum_required):
  CMake 3.17 or higher is required.  You are running version 3.16.3
Call Stack (most recent call first):
  CMakeLists.txt:50 (include)


-- Configuring incomplete, errors occurred!
See also "/home/rnd/tool/gtn/build/CMakeFiles/CMakeOutput.log".
See also "/home/rnd/tool/gtn/build/CMakeFiles/CMakeError.log".
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Download cmake Higher Version

```
(gtn) rnd@gpu:~/tool$ wget https://github.com/Kitware/CMake/releases/download/v3.26.0/cmake-3.26.0.tar.gz
--2023-03-21 21:09:10--  https://github.com/Kitware/CMake/releases/download/v3.26.0/cmake-3.26.0.tar.gz
Resolving github.com (github.com)... 20.205.243.166
Connecting to github.com (github.com)|20.205.243.166|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/537699/0a2859c7-2ca1-4f93-abd9-90a229fe17df?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230321%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230321T140912Z&X-Amz-Expires=300&X-Amz-Signature=977c2c60906d33929311118768f1f7a0918b1b3ac0e9e657522c65be5e0e9162&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=537699&response-content-disposition=attachment%3B%20filename%3Dcmake-3.26.0.tar.gz&response-content-type=application%2Foctet-stream [following]
--2023-03-21 21:09:12--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/537699/0a2859c7-2ca1-4f93-abd9-90a229fe17df?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230321%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230321T140912Z&X-Amz-Expires=300&X-Amz-Signature=977c2c60906d33929311118768f1f7a0918b1b3ac0e9e657522c65be5e0e9162&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=537699&response-content-disposition=attachment%3B%20filename%3Dcmake-3.26.0.tar.gz&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10667656 (10M) [application/octet-stream]
Saving to: ‘cmake-3.26.0.tar.gz’

cmake-3.26.0.tar.gz             100%[=====================================================>]  10.17M  25.8MB/s    in 0.4s    

2023-03-21 21:09:13 (25.8 MB/s) - ‘cmake-3.26.0.tar.gz’ saved [10667656/10667656]
```

```
(gtn) rnd@gpu:~/tool$ ls
cmake-3.26.0.tar.gz  gtn
(gtn) rnd@gpu:~/tool$
```

## Unzip and Installation of cmake 3.26.0

```
(gtn) rnd@gpu:~/tool$ tar -xzvf ./cmake-3.26.0.tar.gz 
...
...
...
cmake-3.26.0/Utilities/std/cmext/
cmake-3.26.0/Utilities/std/cmext/algorithm
cmake-3.26.0/Utilities/std/cmext/enum_set
cmake-3.26.0/Utilities/std/cmext/iterator
cmake-3.26.0/Utilities/std/cmext/memory
cmake-3.26.0/Utilities/std/cmext/string_view
cmake-3.26.0/Utilities/std/cmext/type_traits
cmake-3.26.0/bootstrap
cmake-3.26.0/cmake_uninstall.cmake.in
cmake-3.26.0/configure
cmake-3.26.0/doxygen.config
```

Check the folder content:  

```
(gtn) rnd@gpu:~/tool$ cd cmake-3.26.0/
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ ls
Auxiliary                   CMakeLogo.gif         Copyright.txt     Packaging   Utilities
CMakeCPack.cmake            CONTRIBUTING.rst      DartConfig.cmake  README.rst  bootstrap
CMakeCPackOptions.cmake.in  CTestConfig.cmake     Help              Source      cmake_uninstall.cmake.in
CMakeGraphVizOptions.cmake  CTestCustom.cmake.in  Licenses          Templates   configure
CMakeLists.txt              CompileFlags.cmake    Modules           Tests       doxygen.config
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

Run ./bootstrap and got following error:  

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ ./bootstrap
...
...
...
-- Checking whether CXX compiler has getloadavg
-- Checking whether CXX compiler has getloadavg - yes
-- Checking whether <ext/stdio_filebuf.h> is available
-- Checking whether <ext/stdio_filebuf.h> is available - yes
-- Performing Test HAVE_SOCKADDR_IN6_SIN6_ADDR
-- Performing Test HAVE_SOCKADDR_IN6_SIN6_ADDR - Success
-- Performing Test HAVE_SOCKADDR_IN6_SIN6_SCOPE_ID
-- Performing Test HAVE_SOCKADDR_IN6_SIN6_SCOPE_ID - Success
-- Looking for connect in socket;
-- Looking for connect in socket; - not found
-- Looking for gethostname
-- Looking for gethostname - found
-- Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_ROOT_DIR (missing: OPENSSL_CRYPTO_LIBRARY OPENSSL_INCLUDE_DIR) 
CMake Error at Utilities/cmcurl/CMakeLists.txt:608 (message):
  Could not find OpenSSL.  Install an OpenSSL development package or
  configure CMake with -DCMAKE_USE_OPENSSL=OFF to build without OpenSSL.


-- Configuring incomplete, errors occurred!
---------------------------------------------
Error when bootstrapping CMake:
Problem while running initial CMake
---------------------------------------------
(gtn) rnd@gpu:~/tool/cmake-3.26.0$
```

Running with sudo right:  

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ sudo ./bootstrap
[sudo] password for rnd: 
---------------------------------------------
CMake 3.26.0, Copyright 2000-2023 Kitware, Inc. and Contributors
Found GNU toolchain
C compiler on this system is: gcc   
C++ compiler on this system is: g++    
Makefile processor on this system is: make
g++ has setenv
g++ has unsetenv
g++ does not have environ in stdlib.h
g++ has stl wstring
g++ has <ext/stdio_filebuf.h>
---------------------------------------------
make: 'cmake' is up to date.
loading initial cache file /home/rnd/tool/cmake-3.26.0/Bootstrap.cmk/InitialCacheFlags.cmake
-- Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_ROOT_DIR (missing: OPENSSL_CRYPTO_LIBRARY OPENSSL_INCLUDE_DIR) 
CMake Error at Utilities/cmcurl/CMakeLists.txt:608 (message):
  Could not find OpenSSL.  Install an OpenSSL development package or
  configure CMake with -DCMAKE_USE_OPENSSL=OFF to build without OpenSSL.


-- Configuring incomplete, errors occurred!
---------------------------------------------
Error when bootstrapping CMake:
Problem while running initial CMake
---------------------------------------------
(gtn) rnd@gpu:~/tool/cmake-3.26.0$
```

အထက်ပါအတိုင်း same error ကို ပေးတယ်။  

## Installation of libssl-dev

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ sudo apt-get install libssl-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  libssl-doc
The following NEW packages will be installed:
  libssl-dev
0 upgraded, 1 newly installed, 0 to remove and 167 not upgraded.
Need to get 1585 kB of archives.
After this operation, 8016 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libssl-dev amd64 1.1.1f-1ubuntu2.17 [1585 kB]
Fetched 1585 kB in 8s (203 kB/s)     
Selecting previously unselected package libssl-dev:amd64.
(Reading database ... 229941 files and directories currently installed.)
Preparing to unpack .../libssl-dev_1.1.1f-1ubuntu2.17_amd64.deb ...
Unpacking libssl-dev:amd64 (1.1.1f-1ubuntu2.17) ...
Setting up libssl-dev:amd64 (1.1.1f-1ubuntu2.17) ...
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

## Retry ./bootstrap

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ ./bootstrap
...
...
...
-- Checking support for ARCHIVE_CRYPTO_SHA1_LIBSYSTEM
-- Checking support for ARCHIVE_CRYPTO_SHA1_LIBSYSTEM -- not found
-- Checking support for ARCHIVE_CRYPTO_SHA256_LIBSYSTEM
-- Checking support for ARCHIVE_CRYPTO_SHA256_LIBSYSTEM -- not found
-- Checking support for ARCHIVE_CRYPTO_SHA384_LIBSYSTEM
-- Checking support for ARCHIVE_CRYPTO_SHA384_LIBSYSTEM -- not found
-- Checking support for ARCHIVE_CRYPTO_SHA512_LIBSYSTEM
-- Checking support for ARCHIVE_CRYPTO_SHA512_LIBSYSTEM -- not found
-- Checking support for ARCHIVE_CRYPTO_MD5_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_MD5_OPENSSL -- found
-- Checking support for ARCHIVE_CRYPTO_RMD160_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_RMD160_OPENSSL -- found
-- Checking support for ARCHIVE_CRYPTO_SHA1_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_SHA1_OPENSSL -- found
-- Checking support for ARCHIVE_CRYPTO_SHA256_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_SHA256_OPENSSL -- found
-- Checking support for ARCHIVE_CRYPTO_SHA384_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_SHA384_OPENSSL -- found
-- Checking support for ARCHIVE_CRYPTO_SHA512_OPENSSL
-- Checking support for ARCHIVE_CRYPTO_SHA512_OPENSSL -- found
-- Checking for curses support
-- Checking for curses support - Failed
-- Looking for a Fortran compiler
-- Looking for a Fortran compiler - /usr/bin/f95
-- Performing Test run_pic_test
-- Performing Test run_pic_test - Success
-- Performing Test run_inlines_hidden_test
-- Performing Test run_inlines_hidden_test - Success
-- Configuring done (34.3s)
-- Generating done (0.5s)
-- Build files have been written to: /home/rnd/tool/cmake-3.26.0
---------------------------------------------
CMake has bootstrapped.  Now run make.
```

ဒီတစ်ခါတော့ ./bootstrap ကို run တာ OK.  

## run make

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ make
...
...
...
[ 97%] Linking CXX executable ../../bin/ctresalloc
[ 97%] Built target ctresalloc
[ 97%] Building C object Tests/RunCMake/CMakeFiles/pseudo_llvm-rc.dir/pseudo_llvm-rc.c.o
[ 97%] Linking C executable pseudo_llvm-rc
[ 97%] Built target pseudo_llvm-rc
[ 98%] Building C object Tests/RunCMake/CMakeFiles/print_stdin.dir/print_stdin.c.o
[ 98%] Linking C executable print_stdin
[ 98%] Built target print_stdin
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_emulator.dir/pseudo_emulator.c.o
[ 99%] Linking C executable pseudo_emulator
[ 99%] Built target pseudo_emulator
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_emulator_custom_command.dir/pseudo_emulator_custom_command.c.o
[ 99%] Linking C executable pseudo_emulator_custom_command
[ 99%] Built target pseudo_emulator_custom_command
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_emulator_custom_command_arg.dir/pseudo_emulator_custom_command_arg.c.o
[ 99%] Linking C executable pseudo_emulator_custom_command_arg
[ 99%] Built target pseudo_emulator_custom_command_arg
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_tidy.dir/pseudo_tidy.c.o
[ 99%] Linking C executable pseudo_tidy
[ 99%] Built target pseudo_tidy
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_iwyu.dir/pseudo_iwyu.c.o
[ 99%] Linking C executable pseudo_iwyu
[ 99%] Built target pseudo_iwyu
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_cpplint.dir/pseudo_cpplint.c.o
[ 99%] Linking C executable pseudo_cpplint
[ 99%] Built target pseudo_cpplint
[ 99%] Building C object Tests/RunCMake/CMakeFiles/pseudo_cppcheck.dir/pseudo_cppcheck.c.o
[ 99%] Linking C executable pseudo_cppcheck
[ 99%] Built target pseudo_cppcheck
[ 99%] Building CXX object Tests/FindPackageModeMakefileTest/CMakeFiles/foo.dir/foo.cpp.o
[100%] Linking CXX static library libfoo.a
[100%] Built target foo
```

## Check Current cmake Version

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ which cmake
/usr/bin/cmake
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ cmake --version
cmake version 3.16.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

## Run make install

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ sudo make install
...
...
...
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v141_CL.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_CSharp.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v11_RC.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_CudaHost.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v12_CL.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v12_LIB.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v12_Link.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v12_MASM.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v11_MASM.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_RC.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v12_CSharp.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_NASM.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v14_MASM.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_Cuda.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v140_Link.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v143_Link.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v11_CSharp.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v10_MARMASM.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v11_Link.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/FlagTables/v140_CSharp.json
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/nasm.props.in
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/CustomBuildDepFile.targets
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/nasm.xml
-- Installing: /usr/local/share/cmake-3.26/Templates/MSBuild/nasm.targets
-- Installing: /usr/local/share/vim/vimfiles/indent
-- Installing: /usr/local/share/vim/vimfiles/indent/cmake.vim
-- Installing: /usr/local/share/vim/vimfiles/syntax
-- Installing: /usr/local/share/vim/vimfiles/syntax/cmake.vim
-- Installing: /usr/local/share/emacs/site-lisp/cmake-mode.el
-- Installing: /usr/local/share/aclocal/cmake.m4
-- Installing: /usr/local/share/bash-completion/completions/cmake
-- Installing: /usr/local/share/bash-completion/completions/cpack
-- Installing: /usr/local/share/bash-completion/completions/ctest
```

## Check

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ cmake --version
CMake Error: Could not find CMAKE_ROOT !!!
CMake has most likely not been installed correctly.
Modules directory not found in
/usr/local/share/cmake-3.16
cmake version 3.16.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

## Run Source and then Check Version Again

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ . ~/.bashrc
```

```
(base) rnd@gpu:~/tool/cmake-3.26.0$ cmake --version
cmake version 3.26.0

CMake suite maintained and supported by Kitware (kitware.com/cmake).
(base) rnd@gpu:~/tool/cmake-3.26.0$ source activate gtn
```

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ cmake --version
cmake version 3.26.0
CMake suite maintained and supported by Kitware (kitware.com/cmake).
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

```
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ which cmake
/usr/local/bin/cmake
(gtn) rnd@gpu:~/tool/cmake-3.26.0$ 
```

## Run cmake .. for GTN

```
(gtn) rnd@gpu:~/tool/gtn/build$ cmake ..
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- The C compiler identification is GNU 8.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Configuring done (1.4s)
CMake Warning (dev) in CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "gtn".
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in benchmarks/CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "benchmark_parallel_cuda".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/build
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Run make Got Error

```
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  1%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[  3%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 13%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[ 13%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 16%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 16%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 22%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 23%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 25%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 27%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[ 28%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 30%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
nvcc fatal   : Value 'sm_80' is not defined for option 'gpu-architecture'
nvcc fatal   : Value 'sm_80' is not defined for option 'gpu-architecture'
make[2]: *** [CMakeFiles/gtn.dir/build.make:258: CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
make[2]: *** [CMakeFiles/gtn.dir/build.make:273: CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o] Error 1
nvcc fatal   : Value 'sm_80' is not defined for option 'gpu-architecture'
nvcc fatal   : Value 'sm_80' is not defined for option 'gpu-architecture'
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** [CMakeFiles/gtn.dir/build.make:317: CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Check nvcc Version

```
(gtn) rnd@gpu:~/tool/gtn/build$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Sun_Jul_28_19:07:16_PDT_2019
Cuda compilation tools, release 10.1, V10.1.243
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

```
(gtn) rnd@gpu:~/tool/gtn/build$ which nvcc
/usr/bin/nvcc
(gtn) rnd@gpu:~/tool/gtn/build$
```

nvcc --help ဆိုတဲ့ command ကနေ လေ့လာကြည့်ခဲ့ ...  

```
--gpu-architecture <arch>                  (-arch)                         
        Specify the name of the class of NVIDIA 'virtual' GPU architecture for which
        the CUDA input files must be compiled.
        With the exception as described for the shorthand below, the architecture
        specified with this option must be a 'virtual' architecture (such as compute_50).
        Normally, this option alone does not trigger assembly of the generated PTX
        for a 'real' architecture (that is the role of nvcc option '--gpu-code',
        see below); rather, its purpose is to control preprocessing and compilation
        of the input to PTX.
        For convenience, in case of simple nvcc compilations, the following shorthand
        is supported.  If no value for option '--gpu-code' is specified, then the
        value of this option defaults to the value of '--gpu-architecture'.  In this
        situation, as only exception to the description above, the value specified
        for '--gpu-architecture' may be a 'real' architecture (such as a sm_50),
        in which case nvcc uses the specified 'real' architecture and its closest
        'virtual' architecture as effective architecture values.  For example, 'nvcc
        --gpu-architecture=sm_50' is equivalent to 'nvcc --gpu-architecture=compute_50
        --gpu-code=sm_50,compute_50'.
        Allowed values for this option:  'compute_30','compute_32','compute_35',
        'compute_37','compute_50','compute_52','compute_53','compute_60','compute_61',
        'compute_62','compute_70','compute_72','compute_75','sm_30','sm_32','sm_35',
        'sm_37','sm_50','sm_52','sm_53','sm_60','sm_61','sm_62','sm_70','sm_72',
        'sm_75'.

--gpu-code <code>,...                      (-code)                         
        Specify the name of the NVIDIA GPU to assemble and optimize PTX for.
        nvcc embeds a compiled code image in the resulting executable for each specified
        <code> architecture, which is a true binary load image for each 'real' architecture
        (such as sm_50), and PTX code for the 'virtual' architecture (such as compute_50).
        During runtime, such embedded PTX code is dynamically compiled by the CUDA
        runtime system if no binary load image is found for the 'current' GPU.
        Architectures specified for options '--gpu-architecture' and '--gpu-code'
        may be 'virtual' as well as 'real', but the <code> architectures must be
        compatible with the <arch> architecture.  When the '--gpu-code' option is
        used, the value for the '--gpu-architecture' option must be a 'virtual' PTX
        architecture.
        For instance, '--gpu-architecture=compute_35' is not compatible with '--gpu-code=sm_30',
        because the earlier compilation stages will assume the availability of 'compute_35'
        features that are not present on 'sm_30'.
        Allowed values for this option:  'compute_30','compute_32','compute_35',
        'compute_37','compute_50','compute_52','compute_53','compute_60','compute_61',
        'compute_62','compute_70','compute_72','compute_75','sm_30','sm_32','sm_35',
        'sm_37','sm_50','sm_52','sm_53','sm_60','sm_61','sm_62','sm_70','sm_72',
        'sm_75'.
```

```
(gtn) rnd@gpu:~/tool/gtn/build$ ls /usr/local/
bin  cuda  cuda-11  cuda-11.4  doc  etc  games  go  include  lib  man  sbin  share  src
```

```
(gtn) rnd@gpu:~/tool/gtn/build$ sudo find / -name nvcc
[sudo] password for rnd: 
/opt/cuda-11.4/bin/nvcc
/home/nakanyseth.vuth/mycuda/cuda-11.4/bin/nvcc
/home/nakanyseth.vuth/mycuda/cuda/bin/nvcc
/home/sokhey.kim/.conda/pkgs/cuda-nvcc-11.8.89-0/bin/nvcc
/home.bak/sokhey.kim/.conda/pkgs/cuda-nvcc-11.8.89-0/bin/nvcc
/home.bak/nakanyseth.vuth/mycuda/cuda-11.4/bin/nvcc
/home.bak/nakanyseth.vuth/mycuda/cuda/bin/nvcc
/usr/lib/nvidia-cuda-toolkit/bin/nvcc
/usr/bin/nvcc
/usr/local/cuda-11.4/bin/nvcc
(gtn) rnd@gpu:~/tool/gtn/build$
```

```
(gtn) rnd@gpu:~/tool/gtn/build$ which nvcc
/usr/bin/nvcc
```

$PATH ကို ခေါ်ကြည့်တော့လည်း /usr/bin/ path က ပါပြီးသားမို့... ဘာပြဿနာလဲ ?!  

```
(gtn) rnd@gpu:~/tool/gtn/build$ echo $PATH
/home/rnd/anaconda3/envs/gtn/bin:/home/rnd/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/rnd/marian/build
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Run nvidia-smi Command

```
(gtn) rnd@gpu:~/tool/gtn/build$ nvidia-smi
Tue Mar 21 23:41:08 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 18%   49C    P8    21W / 300W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  5%   59C    P8    23W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 29%   41C    P8    28W / 250W |      3MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Check

ဒီ link: https://github.com/NVlabs/instant-ngp/issues/747 
မှာ ပြောထားသလိုပဲ ... 

```
You might have an old installation of nvidia-cuda-toolkit installed via apt-get (like me). To check, run:
apt-cache policy nvidia-cuda-toolkit

I suspect you have that package installed and the version is 10.1, so you'll want to remove it.

sudo apt remove nvidia-cuda-toolkit
```

check လုပ်ကြည့်တော့ version 10.1 ကို installation လုပ်ထားတာ တွေ့ရတယ် ...  

```
(gtn) rnd@gpu:~/tool/gtn/build$ apt-cache policy nvidia-cuda-toolkit
nvidia-cuda-toolkit:
  Installed: 10.1.243-3
  Candidate: 10.1.243-3
  Version table:
 *** 10.1.243-3 500
        500 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages
        100 /var/lib/dpkg/status
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

သို့သော် remove လုပ်ဖို့က အလွယ်တကူနဲ့ မလုပ်သင့် ....  

## Check build.make File

Error ပေးနေတဲ့ /home/rnd/tool/gtn/build/CMakeFiles/gtn.dir/ folder အောက်က build.make ဖိုင်ရဲ့ line no. 258 ကို ဝင်စစ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ ...  

```
258         /usr/bin/nvcc  $(CUDA_DEFINES) $(CUDA_INCLUDES) $(CUDA_FLAGS) -x cu -c /home/rnd/tool/gtn/gtn/cuda/creations.cu -o     CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
```

အောက်ပါ လင့်ကနေ

```
https://github.com/pytorch/vision/issues/2001
```

flags.make ဖိုင်ကို ဝင်ကြည့်ဖို့ အိုက်ဒီယာ ရခဲ့ ...  

## Check flags.make File

```
(gtn) rnd@gpu:~/tool/gtn/build/CMakeFiles/gtn.dir$ cat flags.make
# CMAKE generated file: DO NOT EDIT!
# Generated by "Unix Makefiles" Generator, CMake Version 3.26

# compile CUDA with /usr/bin/nvcc
# compile CXX with /usr/bin/c++
CUDA_DEFINES = -D_CUDA_

CUDA_INCLUDES = -I/home/rnd/tool/gtn

CUDA_FLAGS = -std=c++14 -Xcompiler=-fPIC -arch=sm_80 -default-stream=per-thread --extended-lambda

CXX_DEFINES = -D_CUDA_

CXX_INCLUDES = -I/home/rnd/tool/gtn

CXX_FLAGS = -std=gnu++14 -fPIC

(gtn) rnd@gpu:~/tool/gtn/build/CMakeFiles/gtn.dir$ 
```

အထက်ပါ မြင်ရတဲ့ -arch=sm_80 ကို ဝင်ပြင်ပြီး run ကြည့်ဖို့ ဆုံးဖြတ်ခဲ့ ...  

-arch=sm_75 အဖြစ် ပြောင်းပြီး file ကို update လုပ်ခဲ့ ...  

## Run make Again

```
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[  6%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[  6%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[  6%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[  6%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
nvcc fatal   : Unknown option '-extended-lambda'
nvcc fatal   : Unknown option '-extended-lambda'
make[2]: *** [CMakeFiles/gtn.dir/build.make:258: CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
make[2]: *** [CMakeFiles/gtn.dir/build.make:273: CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o] Error 1
nvcc fatal   : Unknown option '-extended-lambda'
nvcc fatal   : Unknown option '-extended-lambda'
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** [CMakeFiles/gtn.dir/build.make:317: CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

အထက်ပါအတိုင်း Error အသစ်နဲ့ ရပ်သွားခဲ့ ...  

## Updating CMakeLists.txt File

```
cmake ကိုပါ setting ပြောင်းပြီး အရင် run မှ ဖြစ်မယ်လို့ ယူဆလို့ ...  
/home/rnd/tool/gtn/ path အောက်က CMakeLists.txt ဖိုင်မှာ အောက်ပါအတိုင်း ရှိနေတဲ့အထဲကနေမှ ...  

 35 
 36 if (GTN_BUILD_CUDA)
 37   # TODO, better way to set these arch flags
 38   add_compile_options(
 39     $<$<COMPILE_LANGUAGE:CUDA>:-arch=sm_80>
 40     $<$<COMPILE_LANGUAGE:CUDA>:-default-stream=per-thread>
 41     $<$<COMPILE_LANGUAGE:CUDA>:--extended-lambda>)
 42 endif()
```

line no. 39 ရဲ့ sm_80 ကို လက်ရှိ nvcc က support လုပ်တဲ့ architecture တစ်ခု ဖြစ်တဲ့ sm_75 အနေနဲ့ ပြောင်းပြီး ဖိုင်ကို update လုပ်ခဲ့ ...  

## Run cmake .. Again

cmake .. ကို နောက်တစ်ခေါက် ပြန် run ခဲ့ ...  

```
(gtn) rnd@gpu:~/tool/gtn$ sudo rm -rf build
[sudo] password for rnd: 
(gtn) rnd@gpu:~/tool/gtn$ mkdir build
(gtn) rnd@gpu:~/tool/gtn$ cd build
(gtn) rnd@gpu:~/tool/gtn/build$ cmake ..
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- The C compiler identification is GNU 8.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Configuring done (1.8s)
CMake Warning (dev) in CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "gtn".
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in benchmarks/CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "benchmark_parallel_cuda".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/build
(gtn) rnd@gpu:~/tool/gtn/build$
```

## Run make Command Again

```
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 13%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 15%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 16%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 22%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 25%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 28%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
nvcc fatal   : Unknown option '-extended-lambda'
make[2]: *** [CMakeFiles/gtn.dir/build.make:258: CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
[ 30%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
nvcc fatal   : Unknown option '-extended-lambda'
nvcc fatal   : Unknown option '-extended-lambda'
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** [CMakeFiles/gtn.dir/build.make:273: CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o] Error 1
nvcc fatal   : Unknown option '-extended-lambda'
make[2]: *** [CMakeFiles/gtn.dir/build.make:317: CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

အထက်ပါအတိုင်း Error ပေးနေလို့ sm_80 တစ်ခုတည်း မကပဲ တစ်ခြား option တချို့ကိုပါ change ပေးရမလား တချို့ option တွေကို comment ပိတ်ပေးရမလား စဉ်းစားခဲ့ ...  

## Updating CMakeLists.txt

အောက်ပါ link ကနေ

```
https://github.com/NVIDIA/MinkowskiEngine/issues/207 
```

Dont use --extended-lambda but rather --expt-extended-lambda ဆိုတဲ့ အချက်ကို တွေ့ရ ....  
အဲဒါနဲ့ ဖိုင်ကို ဝင်ကြည့်တော့ ... 

```
 36 if (GTN_BUILD_CUDA)
 37   # TODO, better way to set these arch flags
 38   add_compile_options(
 39     $<$<COMPILE_LANGUAGE:CUDA>:-arch=sm_75>
 40     $<$<COMPILE_LANGUAGE:CUDA>:-default-stream=per-thread>
 41     $<$<COMPILE_LANGUAGE:CUDA>:--extended-lambda>)
 42 endif()
```

--extended-lambda အစား --expt-extended-lambda နဲ့ ပြောင်းခဲ့ ...  

## Rerun cmake and make Again

```
(gtn) rnd@gpu:~/tool/gtn$ sudo rm -rf ./build
(gtn) rnd@gpu:~/tool/gtn$ mkdir build
(gtn) rnd@gpu:~/tool/gtn$ cd build
(gtn) rnd@gpu:~/tool/gtn/build$ cmake ..
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- The C compiler identification is GNU 8.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Configuring done (1.8s)
CMake Warning (dev) in CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "gtn".
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in benchmarks/CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "benchmark_parallel_cuda".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/build
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

cmake run တာ ပြီးသွားလို့ make command ကို ဆက် run ခဲ့ ...  

```
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  1%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 13%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 16%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 22%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 25%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 25%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 28%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[ 30%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
/home/rnd/tool/gtn/gtn/cuda/cuda.cu(61): error: too few arguments in function call

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(94): error: identifier "cudaMallocAsync" is undefined

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(99): error: identifier "cudaFreeAsync" is undefined

3 errors detected in the compilation of "/tmp/tmpxft_0022b0c4_00000000-6_cuda.cpp1.ii".
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

အထက်ပါအတိုင်း Error Message အသစ်က ကြိုဆိုနေခဲ့ ... :)  

##  Trying with -DCMAKE_CUDA_ARCHITECTURES

```
(gtn) rnd@gpu:~/tool/gtn$ sudo rm -rf ./build
(gtn) rnd@gpu:~/tool/gtn$ nano CMakeLists.txt 
(gtn) rnd@gpu:~/tool/gtn$ mkdir build
(gtn) rnd@gpu:~/tool/gtn$ cd build
(gtn) rnd@gpu:~/tool/gtn/build$ cmake -DCMAKE_CUDA_ARCHITECTURES=75 ..
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- The C compiler identification is GNU 8.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Configuring done (1.8s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/build
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  3%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[  3%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 16%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 22%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 27%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 30%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
[ 30%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
/home/rnd/tool/gtn/gtn/cuda/cuda.cu(61): error: too few arguments in function call

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(94): error: identifier "cudaMallocAsync" is undefined

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(99): error: identifier "cudaFreeAsync" is undefined

3 errors detected in the compilation of "/tmp/tmpxft_0022c0f6_00000000-6_cuda.cpp1.ii".
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Removed --extended-lambda Option

--extended-lambda သို့မဟုတ် --expt-extended-lambda ရေးရတဲ့ line တစ်ခုလုံးကို comment ပိတ်ပြီး compile လုပ်ကြည့်တော့ အောက်ပါအတိုင်း error ပေးခဲ့ ...  

```
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  1%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  3%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[  5%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 13%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 18%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 23%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 25%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 28%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[ 30%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
/home/rnd/tool/gtn/gtn/cuda/cuda.cu(61): error: too few arguments in function call

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(74): error: __host__ or __device__ annotation on lambda requires --expt-extended-lambda nvcc flag

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(82): error: __host__ or __device__ annotation on lambda requires --expt-extended-lambda nvcc flag

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(94): error: identifier "cudaMallocAsync" is undefined

/home/rnd/tool/gtn/gtn/cuda/cuda.cu(99): error: identifier "cudaFreeAsync" is undefined

/home/rnd/tool/gtn/gtn/cuda/cuda.h(153): error: The closure type for a lambda ("lambda [](float, float)->float", defined at /home/rnd/tool/gtn/gtn/cuda/cuda.cu:74) cannot be used in the template argument type of a __global__ function template instantiation, unless the lambda is defined within a __device__ or __global__ function, or the lambda is an 'extended lambda' and the flag --expt-extended-lambda is specified
          detected during:
            instantiation of "gtn::cuda::detail::<unnamed>::transformKernel" based on template arguments <float, lambda [](float, float)->float> 
(153): here
            instantiation of "void gtn::cuda::detail::<unnamed>::transform(const T *, const T *, const T *, T *, F) [with T=float, F=lambda [](float, float)->float]" 
/home/rnd/tool/gtn/gtn/cuda/cuda.cu(72): here

/home/rnd/tool/gtn/gtn/cuda/cuda.h(153): error: The closure type for a lambda ("lambda [](float, float)->float", defined at /home/rnd/tool/gtn/gtn/cuda/cuda.cu:82) cannot be used in the template argument type of a __global__ function template instantiation, unless the lambda is defined within a __device__ or __global__ function, or the lambda is an 'extended lambda' and the flag --expt-extended-lambda is specified
          detected during:
            instantiation of "gtn::cuda::detail::<unnamed>::transformKernel" based on template arguments <float, lambda [](float, float)->float> 
(153): here
            instantiation of "void gtn::cuda::detail::<unnamed>::transform(const T *, const T *, const T *, T *, F) [with T=float, F=lambda [](float, float)->float]" 
/home/rnd/tool/gtn/gtn/cuda/cuda.cu(80): here

7 errors detected in the compilation of "/tmp/tmpxft_0022c7c4_00000000-6_cuda.cpp1.ii".
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
make[1]: *** [CMakeFiles/Makefile2:174: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:146: all] Error 2
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Solution

အမျိုးမျိုး parameter ကို ပြောင်းပြီး နောက်ပိတ်ဆုံး ပြေလည်သွားတာက -B build -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc ဆိုတဲ့ option နဲ့ ...  

အဲဒီတော့ nvcc path ကို assign လုပ်ပေးမှ ရတာနဲ့ architecture က 72 နဲ့ လက်ရှိ GPU စက်မှာ အဆင်ပြေတယ် ဆိုတဲ့ သဘောပေါ့။ running log က အောက်ပါအတိုင်းပါ ...  

```
(gtn) rnd@gpu:~/tool/gtn$ rm -rf build
(gtn) rnd@gpu:~/tool/gtn$ cmake -DCMAKE_CUDA_ARCHITECTURES=72 -B build -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc .
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 11.4.120
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/local/cuda-11.4/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- The C compiler identification is GNU 8.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Configuring done (1.7s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/build
(gtn) rnd@gpu:~/tool/gtn$ cd build
(gtn) rnd@gpu:~/tool/gtn/build$ make -j24
[  1%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 11%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 15%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 18%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 20%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 23%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 27%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 28%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
[ 30%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[ 32%] Linking CXX static library libgtn.a
[ 32%] Built target gtn
[ 33%] Building CXX object benchmarks/CMakeFiles/benchmark_ctc.dir/ctc.cpp.o
[ 35%] Building CXX object benchmarks/CMakeFiles/benchmark_parallel.dir/parallel.cpp.o
[ 37%] Building CXX object test/CMakeFiles/tests.dir/tests.cpp.o
[ 38%] Building CXX object benchmarks/CMakeFiles/benchmark_functions.dir/functions.cpp.o
[ 40%] Building CUDA object benchmarks/CMakeFiles/benchmark_parallel_cuda.dir/parallel_cuda.cu.o
[ 44%] Building CXX object test/CMakeFiles/tests.dir/creations_test.cpp.o
[ 44%] Building CXX object examples/CMakeFiles/ctc.dir/ctc.cpp.o
[ 45%] Building CXX object test/CMakeFiles/tests.dir/criterion_test.cpp.o
[ 47%] Building CXX object examples/CMakeFiles/priors.dir/priors.cpp.o
[ 50%] Building CXX object examples/CMakeFiles/asg.dir/asg.cpp.o
[ 50%] Building CXX object benchmarks/CMakeFiles/benchmark_graph.dir/graph.cpp.o
[ 54%] Building CXX object test/CMakeFiles/tests.dir/device_test.cpp.o
[ 54%] Building CXX object examples/CMakeFiles/edit_distance.dir/edit_distance.cpp.o
[ 55%] Building CXX object examples/CMakeFiles/count_ngrams.dir/count_ngrams.cpp.o
[ 59%] Building CXX object test/CMakeFiles/tests.dir/functions_test.cpp.o
[ 59%] Building CXX object test/CMakeFiles/tests.dir/autograd_test.cpp.o
[ 61%] Building CXX object test/CMakeFiles/tests.dir/graph_test.cpp.o
[ 62%] Building CXX object examples/CMakeFiles/tutorial.dir/tutorial.cpp.o
[ 64%] Building CXX object test/CMakeFiles/tests.dir/rand_test.cpp.o
[ 66%] Building CXX object examples/CMakeFiles/learned_decompositions.dir/learned_decompositions.cpp.o
[ 67%] Building CXX object test/CMakeFiles/tests.dir/cuda_test.cpp.o
[ 69%] Building CXX object test/CMakeFiles/tests.dir/parallel_test.cpp.o
[ 72%] Building CXX object test/CMakeFiles/tests.dir/hd_span_test.cpp.o
[ 72%] Building CXX object test/CMakeFiles/tests.dir/utils_test.cpp.o
[ 74%] Building CXX object test/CMakeFiles/tests.dir/cuda_creations_test.cpp.o
[ 76%] Building CXX object test/CMakeFiles/tests.dir/cuda_functions_test.cpp.o
[ 77%] Building CXX object test/CMakeFiles/tests.dir/cuda_utils_test.cpp.o
[ 79%] Linking CXX executable asg
[ 81%] Linking CXX executable edit_distance
[ 83%] Linking CXX executable ctc
[ 84%] Linking CXX executable count_ngrams
[ 86%] Linking CXX executable priors
[ 86%] Built target asg
[ 88%] Linking CXX executable learned_decompositions
[ 88%] Built target edit_distance
[ 89%] Linking CXX executable benchmark_graph
[ 91%] Linking CXX executable tutorial
[ 91%] Built target ctc
[ 93%] Linking CXX executable benchmark_functions
[ 93%] Built target count_ngrams
[ 93%] Built target priors
[ 93%] Built target benchmark_graph
[ 93%] Built target learned_decompositions
[ 93%] Built target tutorial
[ 93%] Built target benchmark_functions
[ 94%] Linking CXX executable benchmark_ctc
[ 96%] Linking CXX executable benchmark_parallel
[ 96%] Built target benchmark_ctc
[ 96%] Built target benchmark_parallel
[ 98%] Linking CXX executable benchmark_parallel_cuda
[ 98%] Built target benchmark_parallel_cuda
[100%] Linking CXX executable tests
[100%] Built target tests
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## make test

```
(gtn) rnd@gpu:~/tool/gtn/build$ make test
Running tests...
Test project /home/rnd/tool/gtn/build
    Start 1: tests
...
...
...
```

ကြာတယ် ...  

testing လုပ်နေတဲ့အချိန်မှာ nvidia-smi command ကို run ကြည့်တော့ အောက်ပါ condition ...  

```
(base) rnd@gpu:~/tool/gtn/build$ nvidia-smi
Wed Mar 22 02:12:33 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 48%   52C    P2    60W / 300W |    246MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 21%   60C    P8    24W / 257W |      3MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 30%   42C    P8    29W / 250W |    210MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2283342      C   ...tool/gtn/build/test/tests      243MiB |
|    2   N/A  N/A   2283342      C   ...tool/gtn/build/test/tests      207MiB |
+-----------------------------------------------------------------------------+
```

Ctrl+C နဲ့ ရပ်တော့လည်း မရ ဖြစ်နေတဲ့ condition ...  

ကြာလို့ logout လုပ်ခဲ့ ...  

## Run make install

```
(gtn) rnd@gpu:~/tool/gtn/build$ sudo make install
[sudo] password for rnd: 
[ 32%] Built target gtn
[ 59%] Built target tests
[ 62%] Built target benchmark_ctc
[ 66%] Built target benchmark_graph
[ 69%] Built target benchmark_functions
[ 72%] Built target benchmark_parallel
[ 76%] Built target benchmark_parallel_cuda
[ 79%] Built target asg
[ 83%] Built target ctc
[ 86%] Built target count_ngrams
[ 89%] Built target edit_distance
[ 93%] Built target priors
[ 96%] Built target tutorial
[100%] Built target learned_decompositions
Install the project...
-- Install configuration: ""
-- Installing: /usr/local/lib/libgtn.a
-- Installing: /usr/local/share/gtn/cmake/gtnTargets.cmake
-- Installing: /usr/local/share/gtn/cmake/gtnTargets-noconfig.cmake
-- Installing: /usr/local/include/gtn
-- Installing: /usr/local/include/gtn/creations.h
-- Installing: /usr/local/include/gtn/functions.h
-- Installing: /usr/local/include/gtn/cpu
-- Installing: /usr/local/include/gtn/cpu/creations.h
-- Installing: /usr/local/include/gtn/cpu/functions.h
-- Installing: /usr/local/include/gtn/cpu/shortest.h
-- Installing: /usr/local/include/gtn/cpu/compose.h
-- Installing: /usr/local/include/gtn/rand.h
-- Installing: /usr/local/include/gtn/gtn.h
-- Installing: /usr/local/include/gtn/autograd.h
-- Installing: /usr/local/include/gtn/criterions.h
-- Installing: /usr/local/include/gtn/hd_span.h
-- Installing: /usr/local/include/gtn/graph.h
-- Installing: /usr/local/include/gtn/device.h
-- Installing: /usr/local/include/gtn/utils.h
-- Installing: /usr/local/include/gtn/parallel.h
-- Installing: /usr/local/include/gtn/cuda
-- Installing: /usr/local/include/gtn/cuda/creations.h
-- Installing: /usr/local/include/gtn/cuda/functions.h
-- Installing: /usr/local/include/gtn/cuda/cuda.h
-- Installing: /usr/local/include/gtn/parallel
-- Installing: /usr/local/include/gtn/parallel/parallel_map.h
-- Installing: /usr/local/include/gtn/parallel/thread_pool.h
-- Installing: /usr/local/share/gtn/cmake/gtnConfig.cmake
(gtn) rnd@gpu:~/tool/gtn/build$ 
```

## Python Binding from Source

binding folder ရှိတဲ့ နေရာကို ဝင် ...  

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ ls
CMakeLists.txt  Manifest.in  README.md  benchmarks  examples  gtn  setup.py  src  test
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ 

(gtn) rnd@gpu:~/tool/gtn/bindings/python$ conda install setuptools
Collecting package metadata (current_repodata.json): done
Solving environment: | 
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::python==3.8.16=h7a1cb2a_3
  - defaults/linux-64::sqlite==3.41.1=h5eee18b_0
  - defaults/linux-64::pip==23.0.1=py38h06a4308_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::openssl==1.1.1t=h7f8727e_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::xz==5.2.10=h5eee18b_1
  - defaults/linux-64::setuptools==65.6.3=py38h06a4308_0
  - defaults/linux-64::certifi==2022.12.7=py38h06a4308_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::libffi==3.4.2=h6a678d5_6
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::wheel==0.38.4=py38h06a4308_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



# All requested packages already installed.

(gtn) rnd@gpu:~/tool/gtn/bindings/python$ 
```

setup run တော့ CMakeList.txt ကြောင့် error ပဲလို့ ထင်တယ်။ အောက်ပါအတိုင်း error ပေးပြီး ထွက်သွားတယ် ....  

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ python setup.py install
running install
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg
running egg_info
creating src/bindings/python/gtn.egg-info
writing src/bindings/python/gtn.egg-info/PKG-INFO
writing dependency_links to src/bindings/python/gtn.egg-info/dependency_links.txt
writing top-level names to src/bindings/python/gtn.egg-info/top_level.txt
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
reading manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib.linux-x86_64-cpython-38
creating build/lib.linux-x86_64-cpython-38/gtn
copying src/bindings/python/gtn/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn
creating build/lib.linux-x86_64-cpython-38/gtn/criterion
copying src/bindings/python/gtn/criterion/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn/criterion
running build_ext
-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is NVIDIA 10.1.243
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- Building Python bindings.
-- Found PythonInterp: /home/rnd/anaconda3/envs/gtn/bin/python (found version "3.8.16") 
-- Found PythonLibs: /home/rnd/anaconda3/envs/gtn/lib/libpython3.8.so
-- Performing Test HAS_FLTO
-- Performing Test HAS_FLTO - Success
-- LTO enabled
-- Configuring done (2.0s)
CMake Warning (dev) in CMakeLists.txt:
  Policy CMP0104 is not set: CMAKE_CUDA_ARCHITECTURES now detected for NVCC,
  empty CUDA_ARCHITECTURES not allowed.  Run "cmake --help-policy CMP0104"
  for policy details.  Use the cmake_policy command to set the policy and
  suppress this warning.

  CUDA_ARCHITECTURES is empty for target "gtn".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Creating directories for 'pybind11'
[  4%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  6%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[ 10%] Performing download step (git clone) for 'pybind11'
Cloning into 'pybind11'...
[ 12%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[ 14%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 17%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 19%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 21%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 25%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 27%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 29%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 31%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 34%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 36%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 38%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
/home/rnd/tool/gtn/bindings/python/src/gtn/cuda/cuda.cu(61): error: too few arguments in function call

/home/rnd/tool/gtn/bindings/python/src/gtn/cuda/cuda.cu(94): error: identifier "cudaMallocAsync" is undefined

/home/rnd/tool/gtn/bindings/python/src/gtn/cuda/cuda.cu(99): error: identifier "cudaFreeAsync" is undefined

[ 40%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
3 errors detected in the compilation of "/tmp/tmpxft_0022e851_00000000-6_cuda.cpp1.ii".
make[2]: *** [CMakeFiles/gtn.dir/build.make:288: CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o] Error 1
make[2]: *** Waiting for unfinished jobs....
HEAD is now at f7b49961 [skip ci] Tweaks in preparation for the 2.8.1 release. (#3421)
[ 42%] Performing update step for 'pybind11'
[ 44%] No patch step for 'pybind11'
[ 46%] No configure step for 'pybind11'
[ 48%] No build step for 'pybind11'
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 53%] Built target pybind11
make[1]: *** [CMakeFiles/Makefile2:138: CMakeFiles/gtn.dir/all] Error 2
make: *** [Makefile:136: all] Error 2
Traceback (most recent call last):
  File "setup.py", line 100, in <module>
    setup(
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/__init__.py", line 87, in setup
    return distutils.core.setup(**attrs)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 185, in setup
    return run_commands(dist)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
    dist.run_commands()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 969, in run_commands
    self.run_command(cmd)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py", line 74, in run
    self.do_egg_install()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py", line 123, in do_egg_install
    self.run_command('bdist_egg')
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/bdist_egg.py", line 165, in run
    cmd = self.call_command('install_lib', warn_dir=0)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/bdist_egg.py", line 151, in call_command
    self.run_command(cmdname)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install_lib.py", line 11, in run
    self.build()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/command/install_lib.py", line 112, in build
    self.run_command('build_ext')
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "setup.py", line 53, in run
    self.build_extension(ext)
  File "setup.py", line 95, in build_extension
    subprocess.check_call(
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/subprocess.py", line 364, in check_call
    raise CalledProcessError(retcode, cmd)
subprocess.CalledProcessError: Command '['cmake', '--build', '.', '--config', 'Release', '--', '-j4']' returned non-zero exit status 2.
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ 
```

## Python Installation With pip

အထက်ပါအတိုင်း source ကနေ setup ကို run တာမှာ error ပေးနေတာကြောင့် pip နဲ့ အဆင်ပြေမလား စမ်းကြည့်ခဲ့ ...  

```
(gtn) rnd@gpu:~/tool$ pip install gtn
Collecting gtn
  Using cached gtn-0.0.1.tar.gz (14 kB)
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: gtn
  Building wheel for gtn (setup.py) ... error
  error: subprocess-exited-with-error
  
  × python setup.py bdist_wheel did not run successfully.
  │ exit code: 1
  ╰─> [58 lines of output]
      running bdist_wheel
      running build
      running build_py
      creating build
      creating build/lib.linux-x86_64-cpython-38
      creating build/lib.linux-x86_64-cpython-38/gtn
      copying src/bindings/python/gtn/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn
      creating build/lib.linux-x86_64-cpython-38/gtn/criterion
      copying src/bindings/python/gtn/criterion/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn/criterion
      running build_ext
      CMake Warning:
        Ignoring extra path from command line:
      
         "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src"
      
      
      CMake Error: The source directory "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src" does not appear to contain CMakeLists.txt.
      Specify --help for usage, or press the help button on the CMake GUI.
      Traceback (most recent call last):
        File "<string>", line 2, in <module>
        File "<pip-setuptools-caller>", line 34, in <module>
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 100, in <module>
          setup(
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/__init__.py", line 87, in setup
          return distutils.core.setup(**attrs)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 185, in setup
          return run_commands(dist)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
          dist.run_commands()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 969, in run_commands
          self.run_command(cmd)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/wheel/bdist_wheel.py", line 325, in run
          self.run_command("build")
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/command/build.py", line 132, in run
          self.run_command(cmd_name)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 53, in run
          self.build_extension(ext)
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 92, in build_extension
          subprocess.check_call(
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/subprocess.py", line 364, in check_call
          raise CalledProcessError(retcode, cmd)
      subprocess.CalledProcessError: Command '['cmake', '/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src', '-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/build/lib.linux-x86_64-cpython-38/gtn/', '-DPYTHON_EXECUTABLE=/home/rnd/anaconda3/envs/gtn/bin/python', '-DPROJECT_SOURCE_DIR=/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src', '-DGTN_BUILD_PYTHON_BINDINGS=ON', '-DGTN_BUILD_EXAMPLES=OFF', '-DGTN_BUILD_BENCHMARKS=OFF', '-DGTN_BUILD_TESTS=OFF', '-DCMAKE_BUILD_TYPE=Release']' returned non-zero exit status 1.
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for gtn
  Running setup.py clean for gtn
Failed to build gtn
Installing collected packages: gtn
  Running setup.py install for gtn ... error
  error: subprocess-exited-with-error
  
  × Running setup.py install for gtn did not run successfully.
  │ exit code: 1
  ╰─> [62 lines of output]
      running install
      /home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
        warnings.warn(
      running build
      running build_py
      creating build
      creating build/lib.linux-x86_64-cpython-38
      creating build/lib.linux-x86_64-cpython-38/gtn
      copying src/bindings/python/gtn/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn
      creating build/lib.linux-x86_64-cpython-38/gtn/criterion
      copying src/bindings/python/gtn/criterion/__init__.py -> build/lib.linux-x86_64-cpython-38/gtn/criterion
      running build_ext
      CMake Warning:
        Ignoring extra path from command line:
      
         "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src"
      
      
      CMake Error: The source directory "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src" does not appear to contain CMakeLists.txt.
      Specify --help for usage, or press the help button on the CMake GUI.
      Traceback (most recent call last):
        File "<string>", line 2, in <module>
        File "<pip-setuptools-caller>", line 34, in <module>
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 100, in <module>
          setup(
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/__init__.py", line 87, in setup
          return distutils.core.setup(**attrs)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 185, in setup
          return run_commands(dist)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
          dist.run_commands()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 969, in run_commands
          self.run_command(cmd)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py", line 68, in run
          return orig.install.run(self)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/command/install.py", line 698, in run
          self.run_command('build')
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/command/build.py", line 132, in run
          self.run_command(cmd_name)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
          super().run_command(command)
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 53, in run
          self.build_extension(ext)
        File "/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/setup.py", line 92, in build_extension
          subprocess.check_call(
        File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/subprocess.py", line 364, in check_call
          raise CalledProcessError(retcode, cmd)
      subprocess.CalledProcessError: Command '['cmake', '/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src', '-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/build/lib.linux-x86_64-cpython-38/gtn/', '-DPYTHON_EXECUTABLE=/home/rnd/anaconda3/envs/gtn/bin/python', '-DPROJECT_SOURCE_DIR=/tmp/pip-install-4ph46qhz/gtn_69e45ca0995b4cfcaea4fe639ed107c2/src', '-DGTN_BUILD_PYTHON_BINDINGS=ON', '-DGTN_BUILD_EXAMPLES=OFF', '-DGTN_BUILD_BENCHMARKS=OFF', '-DGTN_BUILD_TESTS=OFF', '-DCMAKE_BUILD_TYPE=Release']' returned non-zero exit status 1.
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
error: legacy-install-failure

× Encountered error while trying to install package.
╰─> gtn

note: This is an issue with the package mentioned above, not pip.
hint: See above for output from the failure.
(gtn) rnd@gpu:~/tool$ 
```

အထက်ပါအတိုင်းပဲ ...  
pip နဲ့ install လုပ်ကြည့်တော့လည်း error ပေးတာကို တွေ့ရ ...  

## Debugging

ပြဿနာက cmake, make တို့ run ခဲ့တုန်းက ကြုံခဲ့ရတဲ့ ပြဿနာနဲ့ အတူတူပဲလို့ ထင်တယ်။  
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ vi setup.py ကို ကြည့်တော့ line no. 82, 83 မှာ cmake, build အတွက် argument pass လုပ်လို့ ရနိုင်တာကို ရှာဖွေတွေ့ရှိခဲ့ ...  

```
 75         if platform.system() == "Windows":
 76             # cmake_args += ['-DCMAKE_LIBRARY_OUTPUT_DIRECTORY_{}={}'.format(cfg.upper(), extdir)]
 77             # if sys.maxsize > 2 * *32:
 78             # cmake_args += ['-A', 'x64']
 79             # build_args += ['--', '/m']
 80             raise RuntimeError("gtn doesn't support building on Windows yet")
 81         else:
 82             cmake_args += ["-DCMAKE_BUILD_TYPE=" + cfg]
 83             build_args += ["--", "-j4"]
```

ငါ့အနေနဲ့ အထက်မှာ run ခဲ့တုန်းက parameter တွေက အောက်ပါအတိုင်းမို့ ...  

```
(gtn) rnd@gpu:~/tool/gtn$ cmake -DCMAKE_CUDA_ARCHITECTURES=72 -B build -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc .
```

အဲဒီ parameter နှစ်ခုကို ထပ်ဖြည့်ပေးလိုက်ရင် အဆင်ပြေနိုင်တယ်လို့ ယူဆခဲ့ ...  

```
 82             #cmake_args += ["-DCMAKE_BUILD_TYPE=" + cfg]
 83             cmake_args += ["-DCMAKE_CUDA_ARCHITECTURES=72 -B build -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc . "     + "-DCMAKE_BUILD_TYPE=" + cfg]
 84             #build_args += ["--", "-j4"]
 85             build_args += ["--", "-j24"]
```

## Run setup.py install Again

အထက်ပါအတိုင်း setup.py ကို update လုပ်ပြီး run ကြည့်တော့ အောက်ပါအတိုင်း error ပေးခဲ့ ...  

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ python setup.py install
running install
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg
running egg_info
writing src/bindings/python/gtn.egg-info/PKG-INFO
writing dependency_links to src/bindings/python/gtn.egg-info/dependency_links.txt
writing top-level names to src/bindings/python/gtn.egg-info/top_level.txt
reading manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
-- Building Python bindings.
-- Configuring done (0.2s)
CMake Error in CMakeLists.txt:
  Unknown CUDA architecture specifier "B build
  -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc .
  -DCMAKE_BUILD_TYPE=Release".


-- Generating done (0.0s)
CMake Generate step failed.  Build files cannot be regenerated correctly.
```

## Remove -B option and Run setup.py install again

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ python setup.py install
running install
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg
running egg_info
writing src/bindings/python/gtn.egg-info/PKG-INFO
writing dependency_links to src/bindings/python/gtn.egg-info/dependency_links.txt
writing top-level names to src/bindings/python/gtn.egg-info/top_level.txt
reading manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
CMake Warning:
  Ignoring extra path from command line:

   " -DCMAKE_CUDA_ARCHITECTURES=72 -DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc . -DCMAKE_BUILD_TYPE=Release"


-- Building Python bindings.
```

## Updating in Other Parts

ဒီတစ်ခါတော့ cmake_args ဆိုတဲ့ နေရာမှာ ဝင်ပြင်ခဲ့၊ အထက်က ပြင်ခဲ့တဲ့ line ကို comment ပိတ်ထားခဲ့။ ပြင်ခဲ့တာက အောက်ပါအတိုင်း ...  

```
 62         cmake_args = [
 63             "-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=" + extdir,
 64             "-DPYTHON_EXECUTABLE=" + sys.executable,
 65             "-DPROJECT_SOURCE_DIR=" + srcdir,
 66             "-DGTN_BUILD_PYTHON_BINDINGS=ON",
 67             "-DGTN_BUILD_EXAMPLES=OFF",
 68             "-DGTN_BUILD_BENCHMARKS=OFF",
 69             "-DGTN_BUILD_TESTS=OFF",
 70             "-DCMAKE_CUDA_ARCHITECTURES=72",
 71             "-DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc .",
 72         ]
```

## Run setup.py install Again

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ python setup.py install
running install
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg
running egg_info
writing src/bindings/python/gtn.egg-info/PKG-INFO
writing dependency_links to src/bindings/python/gtn.egg-info/dependency_links.txt
writing top-level names to src/bindings/python/gtn.egg-info/top_level.txt
reading manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
-- Building Python bindings.
-- Configuring done (0.2s)
You have changed variables that require your cache to be deleted.
Configure will be re-run and you may have to reset some variables.
The following variables have changed:
CMAKE_CUDA_COMPILER= /usr/local/cuda-11.4/bin/nvcc .

-- The CXX compiler identification is GNU 8.4.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr (found suitable version "10.1", minimum required is "9.0") 
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- The CUDA compiler identification is unknown
CMake Error at /usr/local/share/cmake-3.26/Modules/CMakeDetermineCUDACompiler.cmake:603 (message):
  Failed to detect a default CUDA architecture.



  Compiler output:

Call Stack (most recent call first):
  CMakeLists.txt:27 (enable_language)


-- Configuring incomplete, errors occurred!
Traceback (most recent call last):
  File "setup.py", line 104, in <module>
    setup(
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/__init__.py", line 87, in setup
    return distutils.core.setup(**attrs)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 185, in setup
    return run_commands(dist)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
    dist.run_commands()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 969, in run_commands
    self.run_command(cmd)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py", line 74, in run
    self.do_egg_install()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py", line 123, in do_egg_install
    self.run_command('bdist_egg')
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/bdist_egg.py", line 165, in run
    cmd = self.call_command('install_lib', warn_dir=0)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/bdist_egg.py", line 151, in call_command
    self.run_command(cmdname)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install_lib.py", line 11, in run
    self.build()
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/command/install_lib.py", line 112, in build
    self.run_command('build_ext')
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
    self.distribution.run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/dist.py", line 1208, in run_command
    super().run_command(command)
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
    cmd_obj.run()
  File "setup.py", line 53, in run
    self.build_extension(ext)
  File "setup.py", line 96, in build_extension
    subprocess.check_call(
  File "/home/rnd/anaconda3/envs/gtn/lib/python3.8/subprocess.py", line 364, in check_call
    raise CalledProcessError(retcode, cmd)
subprocess.CalledProcessError: Command '['cmake', '/home/rnd/tool/gtn/bindings/python/src', '-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=/home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/', '-DPYTHON_EXECUTABLE=/home/rnd/anaconda3/envs/gtn/bin/python', '-DPROJECT_SOURCE_DIR=/home/rnd/tool/gtn/bindings/python/src', '-DGTN_BUILD_PYTHON_BINDINGS=ON', '-DGTN_BUILD_EXAMPLES=OFF', '-DGTN_BUILD_BENCHMARKS=OFF', '-DGTN_BUILD_TESTS=OFF', '-DCMAKE_CUDA_ARCHITECTURES=72', '-DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc .', '-DCMAKE_BUILD_TYPE=Release']' returned non-zero exit status 1.
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ 
```

## Update and Run Again

အထက်က error ပေးနေတာက CMAKE_CUDER_COMPILER မှာ နောက်ဆုံး . (i.e. current path) ဆိုတာကြောင့်လို့ ခန့်မှန်းပြီး အဲဒီ path မှာ ပါနေတဲ့ . ကို အောက်ပါအတိုင်း ဖြုတ်ခဲ့ ...  

```
        cmake_args = [
            "-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=" + extdir,
            "-DPYTHON_EXECUTABLE=" + sys.executable,
            "-DPROJECT_SOURCE_DIR=" + srcdir,
            "-DGTN_BUILD_PYTHON_BINDINGS=ON",
            "-DGTN_BUILD_EXAMPLES=OFF",
            "-DGTN_BUILD_BENCHMARKS=OFF",
            "-DGTN_BUILD_TESTS=OFF",
            "-DCMAKE_CUDA_ARCHITECTURES=72",
            "-DCMAKE_CUDA_COMPILER=/usr/local/cuda-11.4/bin/nvcc",
        ]
```

ပြီးတော့ setup.py ကို နောက်တစ်ခေါက် ထပ် run ကြည့်ခဲ့တော့ ... အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ python binding လုပ်သွားတာကို တွေ့ရ ...  

```
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ python setup.py install
running install
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg
running egg_info
writing src/bindings/python/gtn.egg-info/PKG-INFO
writing dependency_links to src/bindings/python/gtn.egg-info/dependency_links.txt
writing top-level names to src/bindings/python/gtn.egg-info/top_level.txt
reading manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
writing manifest file 'src/bindings/python/gtn.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
-- The CUDA compiler identification is NVIDIA 11.4.120
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/local/cuda-11.4/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- Building Python bindings.
-- Found PythonInterp: /home/rnd/anaconda3/envs/gtn/bin/python (found version "3.8.16") 
-- Found PythonLibs: /home/rnd/anaconda3/envs/gtn/lib/libpython3.8.so
-- Performing Test HAS_FLTO
-- Performing Test HAS_FLTO - Success
-- LTO enabled
-- Configuring done (1.4s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] Building CXX object CMakeFiles/gtn.dir/gtn/autograd.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/functions.cpp.o
[  8%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/creations.cpp.o
[ 10%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/shortest.cpp.o
[ 12%] Building CXX object CMakeFiles/gtn.dir/gtn/cpu/compose.cpp.o
[ 14%] Building CXX object CMakeFiles/gtn.dir/gtn/rand.cpp.o
[ 21%] Building CXX object CMakeFiles/gtn.dir/gtn/device.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/parallel/parallel_map.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/criterions.cpp.o
[ 23%] Building CXX object CMakeFiles/gtn.dir/gtn/creations.cpp.o
[ 25%] Building CXX object CMakeFiles/gtn.dir/gtn/functions.cpp.o
[ 27%] Building CXX object CMakeFiles/gtn.dir/gtn/graph.cpp.o
[ 31%] Building CXX object CMakeFiles/gtn.dir/gtn/cuda/functions.cpp.o
[ 34%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/creations.cu.o
[ 34%] Building CXX object CMakeFiles/gtn.dir/gtn/utils.cpp.o
[ 36%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/compose.cu.o
[ 38%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/cuda.cu.o
[ 40%] Building CUDA object CMakeFiles/gtn.dir/gtn/cuda/shortest.cu.o
[ 42%] No patch step for 'pybind11'
[ 44%] No configure step for 'pybind11'
[ 46%] No build step for 'pybind11'
[ 48%] No install step for 'pybind11'
[ 51%] Completed 'pybind11'
[ 55%] Built target pybind11
[ 57%] Linking CXX static library libgtn.a
[ 57%] Built target gtn
[ 59%] Building CXX object bindings/python/CMakeFiles/graph.dir/gtn/graph.cpp.o
[ 61%] Building CXX object bindings/python/CMakeFiles/utils.dir/gtn/utils.cpp.o
[ 63%] Building CXX object bindings/python/CMakeFiles/cuda.dir/gtn/cuda.cpp.o
[ 65%] Building CXX object bindings/python/CMakeFiles/creations.dir/gtn/creations.cpp.o
[ 68%] Building CXX object bindings/python/CMakeFiles/functions.dir/gtn/functions.cpp.o
[ 70%] Building CXX object bindings/python/CMakeFiles/autograd.dir/gtn/autograd.cpp.o
[ 72%] Building CXX object bindings/python/CMakeFiles/rand.dir/gtn/rand.cpp.o
[ 74%] Building CXX object bindings/python/CMakeFiles/device.dir/gtn/device.cpp.o
[ 76%] Building CXX object bindings/python/CMakeFiles/parallel.dir/gtn/parallel.cpp.o
[ 78%] Building CXX object bindings/python/CMakeFiles/criterion.dir/gtn/criterion/criterion.cpp.o
[ 80%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/cuda.cpython-38-x86_64-linux-gnu.so
[ 82%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/rand.cpython-38-x86_64-linux-gnu.so
[ 85%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/criterion/criterion.cpython-38-x86_64-linux-gnu.so
[ 87%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/creations.cpython-38-x86_64-linux-gnu.so
[ 89%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/utils.cpython-38-x86_64-linux-gnu.so
[ 91%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/parallel.cpython-38-x86_64-linux-gnu.so
[ 93%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/device.cpython-38-x86_64-linux-gnu.so
[ 95%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/autograd.cpython-38-x86_64-linux-gnu.so
[ 97%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/graph.cpython-38-x86_64-linux-gnu.so
[ 97%] Built target cuda
[100%] Linking CXX shared module /home/rnd/tool/gtn/bindings/python/build/lib.linux-x86_64-cpython-38/gtn/functions.cpython-38-x86_64-linux-gnu.so
[100%] Built target rand
[100%] Built target criterion
[100%] Built target creations
[100%] Built target parallel
[100%] Built target utils
[100%] Built target device
[100%] Built target autograd
[100%] Built target graph
[100%] Built target functions
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[  8%] No build step for 'pybind11'
[ 48%] Built target gtn
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target graph
[ 65%] Built target creations
[ 70%] Built target device
[ 74%] Built target autograd
[ 78%] Built target functions
[ 82%] Built target criterion
[ 87%] Built target cuda
[ 91%] Built target rand
[ 95%] Built target utils
[100%] Built target parallel
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[ 46%] Built target gtn
[ 48%] No build step for 'pybind11'
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target graph
[ 65%] Built target autograd
[ 70%] Built target device
[ 78%] Built target criterion
[ 78%] Built target functions
[ 82%] Built target rand
[ 87%] Built target creations
[ 91%] Built target utils
[ 95%] Built target parallel
[100%] Built target cuda
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[ 38%] No build step for 'pybind11'
[ 48%] Built target gtn
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target graph
[ 65%] Built target autograd
[ 72%] Built target functions
[ 74%] Built target device
[ 78%] Built target criterion
[ 82%] Built target utils
[ 87%] Built target parallel
[ 95%] Built target rand
[ 95%] Built target creations
[100%] Built target cuda
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[  8%] No build step for 'pybind11'
[ 48%] Built target gtn
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target device
[ 65%] Built target rand
[ 70%] Built target utils
[ 74%] Built target creations
[ 82%] Built target graph
[ 82%] Built target functions
[ 87%] Built target autograd
[ 91%] Built target parallel
[ 95%] Built target criterion
[100%] Built target cuda
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[ 46%] Built target gtn
[ 48%] No build step for 'pybind11'
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target criterion
[ 65%] Built target autograd
[ 70%] Built target graph
[ 78%] Built target functions
[ 78%] Built target rand
[ 82%] Built target cuda
[ 91%] Built target utils
[ 91%] Built target device
[ 95%] Built target creations
[100%] Built target parallel
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[ 46%] Built target gtn
[ 48%] No build step for 'pybind11'
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target functions
[ 65%] Built target utils
[ 70%] Built target graph
[ 74%] Built target creations
[ 78%] Built target rand
[ 82%] Built target device
[ 87%] Built target autograd
[ 91%] Built target cuda
[ 95%] Built target criterion
[100%] Built target parallel
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[ 46%] Built target gtn
[ 48%] No build step for 'pybind11'
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target graph
[ 65%] Built target creations
[ 70%] Built target utils
[ 74%] Built target autograd
[ 78%] Built target parallel
[ 82%] Built target cuda
[ 87%] Built target device
[ 95%] Built target criterion
[ 95%] Built target rand
[100%] Built target functions
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[  8%] No build step for 'pybind11'
[ 48%] Built target gtn
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target functions
[ 65%] Built target graph
[ 70%] Built target cuda
[ 74%] Built target device
[ 78%] Built target creations
[ 82%] Built target parallel
[ 87%] Built target rand
[ 91%] Built target autograd
[ 95%] Built target utils
[100%] Built target criterion
-- Building Python bindings.
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/gtn/bindings/python/build/temp.linux-x86_64-cpython-38
[  2%] Performing update step for 'pybind11'
[  4%] No patch step for 'pybind11'
[  6%] No configure step for 'pybind11'
[  8%] No build step for 'pybind11'
[ 48%] Built target gtn
[ 51%] No install step for 'pybind11'
[ 53%] Completed 'pybind11'
[ 57%] Built target pybind11
[ 61%] Built target device
[ 65%] Built target graph
[ 70%] Built target rand
[ 76%] Built target functions
[ 80%] Built target autograd
[ 82%] Built target criterion
[ 87%] Built target cuda
[ 91%] Built target utils
[ 95%] Built target parallel
[100%] Built target creations
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/rand.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/graph.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/utils.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/autograd.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
creating build/bdist.linux-x86_64/egg/gtn/criterion
copying build/lib.linux-x86_64-cpython-38/gtn/criterion/__init__.py -> build/bdist.linux-x86_64/egg/gtn/criterion
copying build/lib.linux-x86_64-cpython-38/gtn/criterion/criterion.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn/criterion
copying build/lib.linux-x86_64-cpython-38/gtn/__init__.py -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/parallel.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/cuda.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/creations.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/functions.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
copying build/lib.linux-x86_64-cpython-38/gtn/device.cpython-38-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/gtn
byte-compiling build/bdist.linux-x86_64/egg/gtn/criterion/__init__.py to __init__.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/__init__.py to __init__.cpython-38.pyc
creating stub loader for gtn/graph.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/device.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/autograd.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/cuda.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/utils.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/rand.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/creations.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/functions.cpython-38-x86_64-linux-gnu.so
creating stub loader for gtn/parallel.cpython-38-x86_64-linux-gnu.so
byte-compiling build/bdist.linux-x86_64/egg/gtn/graph.py to graph.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/device.py to device.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/autograd.py to autograd.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/cuda.py to cuda.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/utils.py to utils.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/rand.py to rand.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/creations.py to creations.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/functions.py to functions.cpython-38.pyc
byte-compiling build/bdist.linux-x86_64/egg/gtn/parallel.py to parallel.cpython-38.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying src/bindings/python/gtn.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/bindings/python/gtn.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/bindings/python/gtn.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/bindings/python/gtn.egg-info/not-zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/bindings/python/gtn.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
creating dist
creating 'dist/gtn-0.0.1-py3.8-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing gtn-0.0.1-py3.8-linux-x86_64.egg
creating /home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/gtn-0.0.1-py3.8-linux-x86_64.egg
Extracting gtn-0.0.1-py3.8-linux-x86_64.egg to /home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages
Adding gtn 0.0.1 to easy-install.pth file

Installed /home/rnd/anaconda3/envs/gtn/lib/python3.8/site-packages/gtn-0.0.1-py3.8-linux-x86_64.egg
Processing dependencies for gtn==0.0.1
Finished processing dependencies for gtn==0.0.1
(gtn) rnd@gpu:~/tool/gtn/bindings/python$ 
```

## Install numpy Library

လက်ရှိ စက်မှာ account အသစ်နဲ့ ပြီးတော့ environment အသစ်နဲ့ စမ်းနေတာမို့ numpy Library က မရှိသေးဘူး။ testing လုပ်ကြည့်ဖို့အတွက် လိုအပ်တဲ့ numpy Library ကို အောက်ပါအတိုင်း install လုပ်ခဲ့ ...  

```
(gtn) rnd@gpu:~/tool/gtn$ pip install numpy
Collecting numpy
  Downloading numpy-1.24.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.3/17.3 MB 19.0 MB/s eta 0:00:00
Installing collected packages: numpy
Successfully installed numpy-1.24.2
(gtn) rnd@gpu:~/tool/gtn$ 
```

## Testing with Python

(gtn) rnd@gpu:~/tool/gtn$ time python -m unittest discover bindings/python/test
...F.............................Es....F...........
======================================================================
ERROR: test_graph_cuda (test_cuda.CudaTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/rnd/tool/gtn/bindings/python/test/test_cuda.py", line 39, in test_graph_cuda
    self.assertTrue(gtn.equal(g.cuda(gpu1).cpu(), g))
RuntimeError: [/home/rnd/tool/gtn/bindings/python/src/gtn/cuda/cuda.cu:88] CUDA error: invalid argument

======================================================================
FAIL: test_forward_score_grad (test_autograd.AutogradTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/rnd/tool/gtn/bindings/python/test/test_autograd.py", line 261, in test_forward_score_grad
    self.assertTrue(math.isnan(grad_weights[0]))
AssertionError: False is not true

======================================================================
FAIL: test_forward (test_functions.FunctionsTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/rnd/tool/gtn/bindings/python/test/test_functions.py", line 217, in test_forward
    self.assertRaises(ValueError, gtn.forward_score, g)
AssertionError: ValueError not raised by forward_score

----------------------------------------------------------------------
Ran 51 tests in 1.930s

FAILED (failures=2, errors=1, skipped=1)

real	0m2.169s
user	0m1.976s
sys	0m3.384s
(gtn) rnd@gpu:~/tool/gtn$ 

အထက်ပါအတိုင်း Error ပေးပြီး ရပ်သွားခဲ့ ...  

## Check the Code

Error ပေးနေတဲ့ ...  
/home/rnd/tool/gtn/bindings/python/test/test_cuda.py ပရိုဂရမ်ရဲ့ ...  
line 39 ဆိုတာကို ဝင်လေ့လာခဲ့ ...  

 37       if gtn.cuda.device_count() > 1:
 38         gpu1 = gtn.Device(gtn.CUDA, 1)
 39         self.assertTrue(gtn.equal(g.cuda(gpu1).cpu(), g))
 40         self.assertTrue(gtn.equal(gdev.cuda(gpu1).cpu(), g))


ပြီးတော့ ...  /home/rnd/tool/gtn/bindings/python/src/gtn/cuda/cuda.cu ပရိုဂရမ်ကိုလည်း ဝင်လေ့လာခဲ့ ...  
line 88 မှာ error ပေးနေတာတဲ့ ...  


 79 void subtract(const float* a, const float* b, float* out, size_t size) {
 80   transform(
 81     a, a + size, b, out,
 82     [] __device__ (const float lhs, const float rhs) {
 83       return lhs - rhs;
 84     });
 85 }
 86 
 87 void copy(void* dst, const void* src, size_t size) {
 88   CUDA_CHECK(cudaMemcpyAsync(dst, src, size, cudaMemcpyDefault));
 89 }
 90 


တကယ် testing လုပ်ခဲ့တာက 51 ခု၊ အဲဒီအထဲမှာမှ နှစ်မျိုးက failed ဖြစ်ပြီး 1 error, 1 skipped မို့လို့ ...  

Ran 51 tests in 1.930s

FAILED (failures=2, errors=1, skipped=1)

ခဏမေ့ထားပြီး တကယ် run ကြည့်ချင်တဲ့ example program တွေကို run ကြည့်ရင်ကော ....  
မိုးလင်းတော့မယ်။ Lab ကနေ မပြန်ရသေး ....  

## Installation for dot

Example program မှာက finite state ပုံတွေကို dot နဲ့ ဆွဲမှာမို့လို့ graphviz ကို install လုပ်ဖို့ လိုအပ်တယ်။   

(gtn) rnd@gpu:~/tool/gtn$ time sudo apt-get install graphviz
[sudo] password for rnd: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  fonts-liberation libann0 libcdt5 libcgraph6 libgts-0.7-5 libgts-bin libgvc6 libgvpr2 liblab-gamut1 libpathplan4
Suggested packages:
  graphviz-doc
The following NEW packages will be installed:
  fonts-liberation graphviz libann0 libcdt5 libcgraph6 libgts-0.7-5 libgts-bin libgvc6 libgvpr2 liblab-gamut1 libpathplan4
0 upgraded, 11 newly installed, 0 to remove and 167 not upgraded.
Need to get 2701 kB of archives.
After this operation, 11.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 fonts-liberation all 1:1.07.4-11 [822 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/universe amd64 libann0 amd64 1.1.2+doc-7build1 [26.0 kB]                        
Get:3 http://archive.ubuntu.com/ubuntu focal/universe amd64 libcdt5 amd64 2.42.2-3build2 [18.7 kB]                           
Get:4 http://archive.ubuntu.com/ubuntu focal/universe amd64 libcgraph6 amd64 2.42.2-3build2 [41.3 kB]                        
Get:5 http://archive.ubuntu.com/ubuntu focal/universe amd64 libgts-0.7-5 amd64 0.7.6+darcs121130-4 [150 kB]                  
Get:6 http://archive.ubuntu.com/ubuntu focal/universe amd64 libpathplan4 amd64 2.42.2-3build2 [21.9 kB]                      
Get:7 http://archive.ubuntu.com/ubuntu focal/universe amd64 libgvc6 amd64 2.42.2-3build2 [647 kB]                            
Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 libgvpr2 amd64 2.42.2-3build2 [167 kB]                           
Get:9 http://archive.ubuntu.com/ubuntu focal/universe amd64 liblab-gamut1 amd64 2.42.2-3build2 [177 kB]                      
Get:10 http://archive.ubuntu.com/ubuntu focal/universe amd64 graphviz amd64 2.42.2-3build2 [590 kB]                          
Get:11 http://archive.ubuntu.com/ubuntu focal/universe amd64 libgts-bin amd64 0.7.6+darcs121130-4 [41.3 kB]                  
Fetched 2701 kB in 8s (334 kB/s)                                                                                             
Selecting previously unselected package fonts-liberation.
(Reading database ... 230058 files and directories currently installed.)
Preparing to unpack .../00-fonts-liberation_1%3a1.07.4-11_all.deb ...
Unpacking fonts-liberation (1:1.07.4-11) ...
Selecting previously unselected package libann0.
Preparing to unpack .../01-libann0_1.1.2+doc-7build1_amd64.deb ...
Unpacking libann0 (1.1.2+doc-7build1) ...
Selecting previously unselected package libcdt5:amd64.
Preparing to unpack .../02-libcdt5_2.42.2-3build2_amd64.deb ...
Unpacking libcdt5:amd64 (2.42.2-3build2) ...
Selecting previously unselected package libcgraph6:amd64.
Preparing to unpack .../03-libcgraph6_2.42.2-3build2_amd64.deb ...
Unpacking libcgraph6:amd64 (2.42.2-3build2) ...
Selecting previously unselected package libgts-0.7-5:amd64.
Preparing to unpack .../04-libgts-0.7-5_0.7.6+darcs121130-4_amd64.deb ...
Unpacking libgts-0.7-5:amd64 (0.7.6+darcs121130-4) ...
Selecting previously unselected package libpathplan4:amd64.
Preparing to unpack .../05-libpathplan4_2.42.2-3build2_amd64.deb ...
Unpacking libpathplan4:amd64 (2.42.2-3build2) ...
Selecting previously unselected package libgvc6.
Preparing to unpack .../06-libgvc6_2.42.2-3build2_amd64.deb ...
Unpacking libgvc6 (2.42.2-3build2) ...
Selecting previously unselected package libgvpr2:amd64.
Preparing to unpack .../07-libgvpr2_2.42.2-3build2_amd64.deb ...
Unpacking libgvpr2:amd64 (2.42.2-3build2) ...
Selecting previously unselected package liblab-gamut1:amd64.
Preparing to unpack .../08-liblab-gamut1_2.42.2-3build2_amd64.deb ...
Unpacking liblab-gamut1:amd64 (2.42.2-3build2) ...
Selecting previously unselected package graphviz.
Preparing to unpack .../09-graphviz_2.42.2-3build2_amd64.deb ...
Unpacking graphviz (2.42.2-3build2) ...
Selecting previously unselected package libgts-bin.
Preparing to unpack .../10-libgts-bin_0.7.6+darcs121130-4_amd64.deb ...
Unpacking libgts-bin (0.7.6+darcs121130-4) ...
Setting up liblab-gamut1:amd64 (2.42.2-3build2) ...
Setting up libgts-0.7-5:amd64 (0.7.6+darcs121130-4) ...
Setting up libpathplan4:amd64 (2.42.2-3build2) ...
Setting up libann0 (1.1.2+doc-7build1) ...
Setting up fonts-liberation (1:1.07.4-11) ...
Setting up libcdt5:amd64 (2.42.2-3build2) ...
Setting up libcgraph6:amd64 (2.42.2-3build2) ...
Setting up libgts-bin (0.7.6+darcs121130-4) ...
Setting up libgvc6 (2.42.2-3build2) ...
Setting up libgvpr2:amd64 (2.42.2-3build2) ...
Setting up graphviz (2.42.2-3build2) ...
Processing triggers for libc-bin (2.31-0ubuntu9.7) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for fontconfig (2.13.1-2ubuntu3) ...

real	0m38.336s
user	0m8.255s
sys	0m2.362s
(gtn) rnd@gpu:~/tool/gtn$

## Check the dot Version

(gtn) rnd@gpu:~/tool/gtn$ dot -V
dot - graphviz version 2.43.0 (0)
(gtn) rnd@gpu:~/tool/gtn$ 

It looks OK! ...  

## Run Example Python Code

Testing လုပ်ကြည့်မယ့် python program က အောက်ပါအတိုင်း ...  

#!/usr/bin/env python3
"""
Copyright (c) Facebook, Inc. and its affiliates.

This source code is licensed under the MIT license found in the
LICENSE file in the root directory of this source tree.
"""

import gtn

# Recognizes "aba*"
g1 = gtn.Graph(False)
g1.add_node(True)
g1.add_node()
g1.add_node(False, True)
g1.add_arc(0, 1, 0)
g1.add_arc(1, 2, 1)
g1.add_arc(2, 2, 0)

# Recognizes "ba"
g2 = gtn.Graph(False)
g2.add_node(True)
g2.add_node()
g2.add_node(False, True)
g2.add_arc(0, 1, 1)
g2.add_arc(1, 2, 0)

# Recognizes "ac"
g3 = gtn.Graph(False)
g3.add_node(True)
g3.add_node()
g3.add_node(False, True)
g3.add_arc(0, 1, 0)
g3.add_arc(1, 2, 2)

symbols = {0: "a", 1: "b", 2: "c"}

gtn.draw(g1, "/tmp/union_g1.pdf", symbols, symbols)
gtn.draw(g2, "/tmp/union_g2.pdf", symbols, symbols)
gtn.draw(g3, "/tmp/union_g3.pdf", symbols, symbols)

graph = gtn.union([g1, g2, g3])

gtn.draw(graph, "/tmp/union_graph.pdf", symbols, symbols)

အဲဒါကြောင့် run ပြီးသွားရင် output pdf ဖိုင်တွေက /tmp/ အောက်မှာ ရှိလိမ့်မယ်။  

Let's run ...  

(gtn) rnd@gpu:~/tool/gtn$ time python bindings/python/examples/simple_graph.py 

real	0m0.261s
user	0m0.088s
sys	0m0.152s
(gtn) rnd@gpu:~/tool/gtn$ 

output PDF ဖိုင်တွေကို စစ်ကြည့်တော့ အောက်ပါအတိုင်း pdf ဖိုင်တွေကို တွေ့ရလို့ ပျော်တယ် ...  

(gtn) rnd@gpu:~/tool/gtn$ ls /tmp/*.pdf
/tmp/union_g1.pdf  /tmp/union_g2.pdf  /tmp/union_g3.pdf  /tmp/union_graph.pdf
(gtn) rnd@gpu:~/tool/gtn$

## Learning Output PDF Files

PDF  ဖိုင်တွေကို local machine ပေါ်ကို copy ကူးယူခဲ့ပြီး markdown မှာ ပြဖို့အတွက် jpg ဖိုင်အဖြစ် ပြောင်းခဲ့ပြီး fig/ ဖိုလ်ဒါအောက်မှာ သိမ်းထားခဲ့ ...  


https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/gtn-graphs/union_g1.jpg



## Reference

- https://github.com/NVlabs/instant-ngp/issues/747
- https://askubuntu.com/questions/1301714/nvcc-fatal-value-sm-86-is-not-defined-for-option-gpu-architecture
- https://github.com/NVIDIA/MinkowskiEngine/issues/207
- https://github.com/gtn-org/gtn/issues/32
- https://github.com/NVlabs/instant-ngp/issues/39
- https://stackoverflow.com/questions/42585210/extending-setuptools-extension-to-use-cmake-in-setup-py



