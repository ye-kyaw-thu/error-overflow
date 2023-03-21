# Marian Version 1.12.0 Installation Log

sudo right ရှိတဲ့ အကောင့်နဲ့ installation လုပ်ခဲ့တာမို့ အရမ်းတော့ အခက်အခဲ မရှိခဲ့ပေမဲ့ GCC version error က ထုံးစံအတိုင်း တက်တာမို့ solution ကို ကျောင်းသားများ လေ့လာနိုင်ဖို့အတွက် log မှတ်ပေးခဲ့ ...  

## make error

```
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
[ 48%] Built target faiss
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/sendrecv.dep] Error 1
make[5]: *** Waiting for unfinished jobs....
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/all_reduce.dep] Error 1
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/all_gather.dep] Error 1
make[4]: *** [Makefile:50: /home/rnd/marian/build/local/obj/collectives/device/colldevice.a] Error 2
make[4]: *** Waiting for unfinished jobs....
make[3]: *** [/home/rnd/marian/src/3rd_party/nccl/Makefile:25: src.build] Error 2
make[2]: *** [src/3rd_party/CMakeFiles/nccl_install.dir/build.make:112: src/3rd_party/nccl_install-prefix/src/nccl_install-stamp/nccl_install-build] Error 2
make[1]: *** [CMakeFiles/Makefile2:697: src/3rd_party/CMakeFiles/nccl_install.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
[ 48%] Built target libyaml-cpp
[ 48%] Linking CXX static library libsentencepiece.a
[ 48%] Built target sentencepiece-static
[ 49%] Linking CXX static library libsentencepiece_train.a
[ 49%] Built target sentencepiece_train-static
[ 49%] Built target SQLiteCpp
make: *** [Makefile:152: all] Error 2
(base) rnd@gpu:~/marian/build$ 
```

## Check GCC Version

```
(base) rnd@gpu:~/marian/build$ gcc --version
gcc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

(base) rnd@gpu:~/marian/build$ 
```

အထက်ပါအတိုင်း 9.4.0 ဖြစ်နေတာကို တွေ့ရ ...  

## Check Installed GCC

```
(base) rnd@gpu:~/marian/build$ ls /usr/bin/gcc*
/usr/bin/gcc    /usr/bin/gcc-9   /usr/bin/gcc-ar-8  /usr/bin/gcc-nm    /usr/bin/gcc-nm-9    /usr/bin/gcc-ranlib-8
/usr/bin/gcc-8  /usr/bin/gcc-ar  /usr/bin/gcc-ar-9  /usr/bin/gcc-nm-8  /usr/bin/gcc-ranlib  /usr/bin/gcc-ranlib-9
(base) rnd@gpu:~/marian/build$ 
```

## Rerun cmake with parameter

အရင်ဆုံး build folder ကို ဖျက်ခဲ့တယ်။  

```
(base) rnd@gpu:~/marian$ rm -rf build
```

ပြီးတော့ folder အသစ် ပြန်ဆောက်ခဲ့ ...  

```
(base) rnd@gpu:~/marian$ mkdir build
(base) rnd@gpu:~/marian$ cd build
(base) rnd@gpu:~/marian/build$
```

gcc version ကို 8 ပဲ ထားပြီး cmake command ကို ပြန် run ခဲ့ ...  

```
(base) rnd@gpu:~/marian/build$ cmake .. -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_C_COMPILER=/usr/bin/gcc-8
-- The CXX compiler identification is GNU 9.4.0
-- The C compiler identification is GNU 8.4.0
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Check for working C compiler: /usr/bin/gcc-8
-- Check for working C compiler: /usr/bin/gcc-8 -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Project name: marian
-- Project version: v1.12.0+65bf82ff
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
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Found MKL: -Wl,--start-group;/opt/intel/mkl/lib/intel64/libmkl_intel_ilp64.a;/opt/intel/mkl/lib/intel64/libmkl_sequential.a;/opt/intel/mkl/lib/intel64/libmkl_core.a;-Wl,--end-group  
-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Configuring done
-- Generating done
-- Build files have been written to: /home/rnd/marian/build
(base) rnd@gpu:~/marian/build$
```

## Run make Again

```
(base) rnd@gpu:~/marian/build$ make -j24
...
...
...
Compiling  debug.cc                            > /home/rnd/marian/build/local/obj/debug.o
[ 44%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 45%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 45%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
Compiling  proxy.cc                            > /home/rnd/marian/build/local/obj/proxy.o
Compiling  misc/nvmlwrap.cc                    > /home/rnd/marian/build/local/obj/misc/nvmlwrap.o
Compiling  misc/ibvwrap.cc                     > /home/rnd/marian/build/local/obj/misc/ibvwrap.o
Compiling  misc/utils.cc                       > /home/rnd/marian/build/local/obj/misc/utils.o
Compiling  misc/argcheck.cc                    > /home/rnd/marian/build/local/obj/misc/argcheck.o
Compiling  transport/p2p.cc                    > /home/rnd/marian/build/local/obj/transport/p2p.o
Compiling  transport/shm.cc                    > /home/rnd/marian/build/local/obj/transport/shm.o
Compiling  transport/net.cc                    > /home/rnd/marian/build/local/obj/transport/net.o
Compiling  transport/net_socket.cc             > /home/rnd/marian/build/local/obj/transport/net_socket.o
Compiling  transport/net_ib.cc                 > /home/rnd/marian/build/local/obj/transport/net_ib.o
Compiling  transport/coll_net.cc               > /home/rnd/marian/build/local/obj/transport/coll_net.o
Compiling  collectives/sendrecv.cc             > /home/rnd/marian/build/local/obj/collectives/sendrecv.o
Compiling  collectives/all_reduce.cc           > /home/rnd/marian/build/local/obj/collectives/all_reduce.o
Compiling  collectives/all_gather.cc           > /home/rnd/marian/build/local/obj/collectives/all_gather.o
Compiling  collectives/broadcast.cc            > /home/rnd/marian/build/local/obj/collectives/broadcast.o
Compiling  collectives/reduce.cc               > /home/rnd/marian/build/local/obj/collectives/reduce.o
Compiling  collectives/reduce_scatter.cc       > /home/rnd/marian/build/local/obj/collectives/reduce_scatter.o
Compiling  graph/topo.cc                       > /home/rnd/marian/build/local/obj/graph/topo.o
Compiling  graph/paths.cc                      > /home/rnd/marian/build/local/obj/graph/paths.o
Compiling  graph/search.cc                     > /home/rnd/marian/build/local/obj/graph/search.o
Compiling  graph/connect.cc                    > /home/rnd/marian/build/local/obj/graph/connect.o
Compiling  graph/rings.cc                      > /home/rnd/marian/build/local/obj/graph/rings.o
Compiling  graph/trees.cc                      > /home/rnd/marian/build/local/obj/graph/trees.o
Compiling  graph/tuning.cc                     > /home/rnd/marian/build/local/obj/graph/tuning.o
Compiling  graph/xml.cc                        > /home/rnd/marian/build/local/obj/graph/xml.o
[ 45%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
Generating rules                               > /home/rnd/marian/build/local/obj/collectives/device/Makefile.rules
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/sendrecv.dep] Error 1
make[5]: *** Waiting for unfinished jobs....
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[ 46%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[ 47%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[ 47%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
[ 47%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/all_reduce.dep] Error 1
[ 48%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
make[5]: *** [Makefile:53: /home/rnd/marian/build/local/obj/collectives/device/all_gather.dep] Error 1
make[4]: *** [Makefile:50: /home/rnd/marian/build/local/obj/collectives/device/colldevice.a] Error 2
make[4]: *** Waiting for unfinished jobs....
[ 48%] Building CXX object src/3rd_party/sentencepiece/src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 48%] Built target libyaml-cpp
[ 48%] Built target faiss
make[3]: *** [/home/rnd/marian/src/3rd_party/nccl/Makefile:25: src.build] Error 2
make[2]: *** [src/3rd_party/CMakeFiles/nccl_install.dir/build.make:112: src/3rd_party/nccl_install-prefix/src/nccl_install-stamp/nccl_install-build] Error 2
make[1]: *** [CMakeFiles/Makefile2:697: src/3rd_party/CMakeFiles/nccl_install.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
[ 48%] Linking CXX static library libsentencepiece.a
[ 48%] Built target sentencepiece-static
[ 49%] Linking CXX static library libsentencepiece_train.a
[ 49%] Built target sentencepiece_train-static
[ 49%] Built target SQLiteCpp
make: *** [Makefile:152: all] Error 2
(base) rnd@gpu:~/marian/build$
```

## Trying with update-alternative

```
(base) rnd@gpu:~/marian/build$ which update-alternatives
/usr/bin/update-alternatives
(base) rnd@gpu:~/marian/build$ 
```

Check existing gcc versions:  

```
(base) rnd@gpu:~/marian/build$ ls /usr/bin/gcc-
gcc-8         gcc-ar        gcc-ar-9      gcc-nm-8      gcc-ranlib    gcc-ranlib-9  
gcc-9         gcc-ar-8      gcc-nm        gcc-nm-9      gcc-ranlib-8  
(base) rnd@gpu:~/marian/build$
```

update-alternatives tool ကို သုံးပြီးတော့ multiple GCC, G++ compiler list ကို အောက်ပါအတိုင်း create လုပ်ခဲ့ ...  

```
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
update-alternatives: using /usr/bin/gcc-8 to provide /usr/bin/gcc (gcc) in auto mode
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
update-alternatives: using /usr/bin/g++-8 to provide /usr/bin/g++ (g++) in auto mode
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
update-alternatives: using /usr/bin/gcc-9 to provide /usr/bin/gcc (gcc) in auto mode
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
update-alternatives: using /usr/bin/g++-9 to provide /usr/bin/g++ (g++) in auto mode
```

အောက်ပါအတိုင်း gcc version ကို 8 အဖြစ် ရွေးထားခဲ့ ...  

```
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --config gcc
There are 2 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path            Priority   Status
------------------------------------------------------------
* 0            /usr/bin/gcc-9   9         auto mode
  1            /usr/bin/gcc-8   8         manual mode
  2            /usr/bin/gcc-9   9         manual mode

Press <enter> to keep the current choice[*], or type selection number: 1
update-alternatives: using /usr/bin/gcc-8 to provide /usr/bin/gcc (gcc) in manual mode
```

အောက်ပါအတိုင်း g++ (C++ compiler) ကိုလည်း version 8 အဖြစ် manual ရွေးထားခဲ့ ...  

```
(base) rnd@gpu:~/marian/build$ sudo update-alternatives --config g++
There are 2 choices for the alternative g++ (providing /usr/bin/g++).

  Selection    Path            Priority   Status
------------------------------------------------------------
* 0            /usr/bin/g++-9   9         auto mode
  1            /usr/bin/g++-8   8         manual mode
  2            /usr/bin/g++-9   9         manual mode

Press <enter> to keep the current choice[*], or type selection number: 1
update-alternatives: using /usr/bin/g++-8 to provide /usr/bin/g++ (g++) in manual mode
(base) rnd@gpu:~/marian/build$ 
```

## Make Confirmation

```
(base) rnd@gpu:~/marian/build$ gcc --version
gcc (Ubuntu 8.4.0-3ubuntu2) 8.4.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

```
(base) rnd@gpu:~/marian/build$ g++ --version
g++ (Ubuntu 8.4.0-3ubuntu2) 8.4.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

(base) rnd@gpu:~/marian/build$ 
```

## Run cmake, make Again 

marain compilation ကို ထပ် ကြိုးစားကြည့်ခဲ့ ...  

```
(base) rnd@gpu:~/marian/build$ cd ..
(base) rnd@gpu:~/marian$ rm -rf ./build
(base) rnd@gpu:~/marian$ mkdir build
(base) rnd@gpu:~/marian$ cd build
```

Run cmake as follows:  

```
(base) rnd@gpu:~/marian/build$ cmake ..
-- The CXX compiler identification is GNU 8.4.0
-- The C compiler identification is GNU 8.4.0
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
-- Project version: v1.12.0+65bf82ff
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
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Found MKL: -Wl,--start-group;/opt/intel/mkl/lib/intel64/libmkl_intel_ilp64.a;/opt/intel/mkl/lib/intel64/libmkl_sequential.a;/opt/intel/mkl/lib/intel64/libmkl_core.a;-Wl,--end-group  
-- VERSION: 0.1.94
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Configuring done
-- Generating done
-- Build files have been written to: /home/rnd/marian/build
(base) rnd@gpu:~/marian/build$ 
```

Run make again as follows ...  

```
(base) rnd@gpu:~/marian/build$ make -j24
...
...
...
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
Scanning dependencies of target marian_conv
Scanning dependencies of target marian_scorer
Scanning dependencies of target marian_decoder
Scanning dependencies of target marian_train
Scanning dependencies of target marian_vocab
[ 96%] Building CXX object src/CMakeFiles/marian_conv.dir/command/marian_conv.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_vocab.dir/command/marian_vocab.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_decoder.dir/command/marian_decoder.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_scorer.dir/command/marian_scorer.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_train.dir/command/marian_main.cpp.o
[ 97%] Linking CXX executable ../marian-vocab
[ 97%] Built target marian_vocab
[ 98%] Linking CXX executable ../marian-decoder
[ 98%] Linking CXX executable ../marian-conv
[ 99%] Linking CXX executable ../marian-scorer
[ 99%] Built target marian_decoder
[ 99%] Built target marian_conv
[ 99%] Built target marian_scorer
[100%] Linking CXX executable ../marian
[100%] Built target marian_train
(base) rnd@gpu:~/marian/build$
```

## Check the build/ Folder

```
(base) rnd@gpu:~/marian/build$ ls
CMakeCache.txt     CPackSourceConfig.cmake  libmarian.a  marian-conv     marian-vocab  spm_export_vocab  src
CMakeFiles         Makefile                 local        marian-decoder  spm_decode    spm_normalize
CPackConfig.cmake  cmake_install.cmake      marian       marian-scorer   spm_encode    spm_train
(base) rnd@gpu:~/marian/build$ 
```

## Update $PATH

.bashrc ဖိုင်မှာ ဝင်ဖြည့်ခဲ့ ...  

```
export PATH=$PATH:/home/rnd/marian/build
```

## Check marian commands

logout လုပ်ပြီး login ပြန်ဝင်ပြီး marian command တချို့ကို စမ်းကြည့်ခဲ့ ...  

```
(base) rnd@gpu:~$ marian --version
v1.12.0 65bf82ff 2023-02-21 09:56:29 -0800
(base) rnd@gpu:~$ 
```

```
(base) rnd@gpu:~$ marian --help
Marian: Fast Neural Machine Translation in C++
Usage: marian [OPTIONS]

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
(base) rnd@gpu:~$
```

vocab ဆောက်တဲ့ command ကိုလည်း confirm လုပ်ကြည့်ခဲ့ ...  

```
(base) rnd@gpu:~$ marian-vocab --help
Create a vocabulary from text corpora given on STDIN
Usage: marian-vocab [OPTIONS]

Allowed options:
  -h,--help                             Print this help message and exit
  --version                             Print the version number and exit
  -m,--max-size UINT=0                  Generate only UINT most common vocabulary items

Examples:
  ./marian-vocab < text.src > vocab.yml
  cat text.src text.trg | ./marian-vocab > vocab.yml
(base) rnd@gpu:~$
```

sentencepiece train command ကိုလည်း checking ...  

```
(base) rnd@gpu:~$ spm_train --help
sentencepiece

Usage: spm_train [options] files

   --input (comma separated list of input sentences)  type: std::string default: ""
   --input_format (Input format. Supported format is `text` or `tsv`.)  type: std::string default: ""
   --model_prefix (output model prefix)  type: std::string default: ""
   --model_type (model algorithm: unigram, bpe, word or char)  type: std::string default: "unigram"
   --vocab_size (vocabulary size)  type: int32 default: 8000
   --accept_language (comma-separated list of languages this model can accept)  type: std::string default: ""
   --self_test_sample_size (the size of self test samples)  type: int32 default: 0
   --character_coverage (character coverage to determine the minimum symbols)  type: double default: 0.9995
   --input_sentence_size (maximum size of sentences the trainer loads)  type: int32 default: 0
   --shuffle_input_sentence (Randomly sample input sentences in advance. Valid when --input_sentence_size > 0)  type: bool default: true
   --seed_sentencepiece_size (the size of seed sentencepieces)  type: int32 default: 1000000
   --shrinking_factor (Keeps top shrinking_factor pieces with respect to the loss)  type: double default: 0.75
   --num_threads (number of threads for training)  type: int32 default: 16
   --num_sub_iterations (number of EM sub-iterations)  type: int32 default: 2
   --max_sentencepiece_length (maximum length of sentence piece)  type: int32 default: 16
   --max_sentence_length (maximum length of sentence in byte)  type: int32 default: 4192
   --split_by_unicode_script (use Unicode script to split sentence pieces)  type: bool default: true
   --split_by_number (split tokens by numbers (0-9))  type: bool default: true
   --split_by_whitespace (use a white space to split sentence pieces)  type: bool default: true
   --split_digits (split all digits (0-9) into separate pieces)  type: bool default: false
   --treat_whitespace_as_suffix (treat whitespace marker as suffix instead of prefix.)  type: bool default: false
   --control_symbols (comma separated list of control symbols)  type: std::string default: ""
   --control_symbols_file (load control_symbols from file.)  type: std::string default: ""
   --user_defined_symbols (comma separated list of user defined symbols)  type: std::string default: ""
   --user_defined_symbols_file (load user_defined_symbols from file.)  type: std::string default: ""
   --required_chars (UTF8 characters in this flag are always used in the character set regardless of --character_coverage)  type: std::string default: ""
   --required_chars_file (load required_chars from file.)  type: std::string default: ""
   --byte_fallback (decompose unknown pieces into UTF-8 byte pieces)  type: bool default: false
   --vocabulary_output_piece_score (Define score in vocab file)  type: bool default: true
   --normalization_rule_name (Normalization rule name. Choose from nfkc or identity)  type: std::string default: "nmt_nfkc"
   --normalization_rule_tsv (Normalization rule TSV file. )  type: std::string default: ""
   --denormalization_rule_tsv (Denormalization rule TSV file.)  type: std::string default: ""
   --add_dummy_prefix (Add dummy whitespace at the beginning of text)  type: bool default: true
   --remove_extra_whitespaces (Removes leading, trailing, and duplicate internal whitespace)  type: bool default: true
   --encode_unicode_case (Handles unicode case)  type: bool default: false
   --hard_vocab_limit (If set to false, --vocab_size is considered as a soft limit.)  type: bool default: true
   --use_all_vocab (If set to true, use all tokens as vocab. Valid for word/char models.)  type: bool default: false
   --unk_id (Override UNK (<unk>) id.)  type: int32 default: 0
   --bos_id (Override BOS (<s>) id. Set -1 to disable BOS.)  type: int32 default: 1
   --eos_id (Override EOS (</s>) id. Set -1 to disable EOS.)  type: int32 default: 2
   --pad_id (Override PAD (<pad>) id. Set -1 to disable PAD.)  type: int32 default: -1
   --unk_piece (Override UNK (<unk>) piece.)  type: std::string default: "<unk>"
   --bos_piece (Override BOS (<s>) piece.)  type: std::string default: "<s>"
   --eos_piece (Override EOS (</s>) piece.)  type: std::string default: "</s>"
   --pad_piece (Override PAD (<pad>) piece.)  type: std::string default: "<pad>"
   --unk_surface (Dummy surface string for <unk>. In decoding <unk> is decoded to `unk_surface`.)  type: std::string default: " ⁇ "
   --train_extremely_large_corpus (Increase bit depth for unigram tokenization.)  type: bool default: false
   --random_seed (Seed value for random generator.)  type: int32 default: -1
   --help (show help)  type: bool default: false
   --version (show version)  type: bool default: false
   --minloglevel (Messages logged at a lower level than this don't actually get logged anywhere)  type: int default: 0


(base) rnd@gpu:~$
```

spm_encode နဲ့ spm_decode command တွေကိုလည်း --help ခေါ်ကြည့်ခဲ့ ...  

```
(base) rnd@gpu:~$ spm_encode --help
sentencepiece

Usage: spm_encode [options] files

   --model (model file name)  type: std::string default: ""
   --output_format (choose from piece, id, proto, nbest_piece, nbest_id, nbest_proto, sample_piece, sample_id or sample_proto.)  type: std::string default: "piece"
   --input (input filename)  type: std::string default: ""
   --output (output filename)  type: std::string default: ""
   --extra_options (':' separated encoder extra options, e.g., "reverse:bos:eos")  type: std::string default: ""
   --nbest_size (NBest size)  type: int32 default: 10
   --alpha (Smoothing parameter for sampling mode.)  type: double default: 0.5
   --random_seed (Seed value for random generator.)  type: int32 default: -1
   --vocabulary (Restrict the vocabulary. The encoder only emits the tokens in "vocabulary" file)  type: std::string default: ""
   --vocabulary_threshold (Words with frequency < threshold will be treated as OOV)  type: int32 default: 0
   --generate_vocabulary (Generates vocabulary file instead of segmentation)  type: bool default: false
   --help (show help)  type: bool default: false
   --version (show version)  type: bool default: false
   --minloglevel (Messages logged at a lower level than this don't actually get logged anywhere)  type: int default: 0
```

```
(base) rnd@gpu:~$ spm_decode --help
sentencepiece

Usage: spm_decode [options] files

   --model (model file name)  type: std::string default: ""
   --input (input filename)  type: std::string default: ""
   --output (output filename)  type: std::string default: ""
   --input_format (choose from piece or id)  type: std::string default: "piece"
   --output_format (choose from string or proto)  type: std::string default: "string"
   --extra_options (':' separated encoder extra options, e.g., "reverse:bos:eos")  type: std::string default: ""
   --help (show help)  type: bool default: false
   --version (show version)  type: bool default: false
   --minloglevel (Messages logged at a lower level than this don't actually get logged anywhere)  type: int default: 0


(base) rnd@gpu:~$
```

## Reference

- https://marian-nmt.github.io/quickstart/
- https://stackoverflow.com/questions/65605972/cmake-unsupported-gnu-version-gcc-versions-later-than-8-are-not-supported
- https://stackoverflow.com/questions/39854114/set-gcc-version-for-make-in-shell
- https://linuxconfig.org/how-to-switch-between-multiple-gcc-and-g-compiler-versions-on-ubuntu-20-04-lts-focal-fossa



