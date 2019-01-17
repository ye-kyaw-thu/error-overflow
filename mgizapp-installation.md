# mgizapp Installation Note

Message for my students and someone who are not familiar with Linux environment:  
```
Please note, I am running as a root in this case.  
For your case, you need to use sudo command (if your account is in the sudoers list) or you have to contact to your server admin.  
Of course, if you are running on your own notebook, you are the administrator!  
```

First download mgiza:

```bash
git clone https://github.com/moses-smt/mgiza
```

Change your path for installation process:

```bash
cd mgiza/mgizapp/
```

As usual, check INSTALL file:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# vi INSTALL 
```

Run cmake .:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# cmake .
-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- You have not set the install dir, default to './inst', if
    you want to set it, use cmake -DCMAKE_INSTALL_PREFIX to do so
-- Performing Test TR1_SHARED_PTR_USE_TR1_MEMORY
-- Performing Test TR1_SHARED_PTR_USE_TR1_MEMORY - Success
-- Performing Test TR1_SHARED_PTR_USE_MEMORY
-- Performing Test TR1_SHARED_PTR_USE_MEMORY - Failed
-- Performing Test TR1_UNORDERED_MAP_USE_TR1_UNORDERED_MAP
-- Performing Test TR1_UNORDERED_MAP_USE_TR1_UNORDERED_MAP - Success
-- Performing Test TR1_UNORDERED_MAP_USE_UNORDERED_MAP
-- Performing Test TR1_UNORDERED_MAP_USE_UNORDERED_MAP - Failed
CMake Warning at /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:577 (message):
  Imported targets and dependency information not available for Boost version
  (all versions older than 1.33)
Call Stack (most recent call first):
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:959 (_Boost_COMPONENT_DEPENDENCIES)
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:1618 (_Boost_MISSING_DEPENDENCIES)
  CMakeLists.txt:57 (FIND_PACKAGE)


CMake Warning at /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:577 (message):
  Imported targets and dependency information not available for Boost version
  (all versions older than 1.33)
Call Stack (most recent call first):
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:959 (_Boost_COMPONENT_DEPENDENCIES)
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:1618 (_Boost_MISSING_DEPENDENCIES)
  CMakeLists.txt:57 (FIND_PACKAGE)


-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Could NOT find Boost
CMake Warning at /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:577 (message):
  Imported targets and dependency information not available for Boost version
  (all versions older than 1.33)
Call Stack (most recent call first):
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:959 (_Boost_COMPONENT_DEPENDENCIES)
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:1618 (_Boost_MISSING_DEPENDENCIES)
  CMakeLists.txt:70 (FIND_PACKAGE)


CMake Warning at /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:577 (message):
  Imported targets and dependency information not available for Boost version
  (all versions older than 1.33)
Call Stack (most recent call first):
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:959 (_Boost_COMPONENT_DEPENDENCIES)
  /usr/local/share/cmake-3.12/Modules/FindBoost.cmake:1618 (_Boost_MISSING_DEPENDENCIES)
  CMakeLists.txt:70 (FIND_PACKAGE)


-- Could NOT find Boost
CMake Error at CMakeLists.txt:79 (MESSAGE):
  Boost not found, please set the BOOST_ROOT and BOOST_LIBRARYDIR environment
  variables


-- Configuring incomplete, errors occurred!
See also "/home/yekyawthu/tool/mgiza/mgizapp/CMakeFiles/CMakeOutput.log".
See also "/home/yekyawthu/tool/mgiza/mgizapp/CMakeFiles/CMakeError.log".
```

We got above ERROR MESSAGE!  
We need to install Boost:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# apt-get install libboost-all-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  icu-devtools libboost-atomic-dev libboost-atomic1.58-dev libboost-atomic1.58.0 libboost-chrono-dev libboost-chrono1.58-dev libboost-chrono1.58.0
  libboost-context-dev libboost-context1.58-dev libboost-context1.58.0 libboost-coroutine-dev libboost-coroutine1.58-dev libboost-coroutine1.58.0
  libboost-date-time-dev libboost-date-time1.58-dev libboost-date-time1.58.0 libboost-dev libboost-exception-dev libboost-exception1.58-dev
  libboost-filesystem-dev libboost-filesystem1.58-dev libboost-filesystem1.58.0 libboost-graph-dev libboost-graph-parallel-dev
  libboost-graph-parallel1.58-dev libboost-graph-parallel1.58.0 libboost-graph1.58-dev libboost-graph1.58.0 libboost-iostreams-dev
  libboost-iostreams1.58-dev libboost-iostreams1.58.0 libboost-locale-dev libboost-locale1.58-dev libboost-locale1.58.0 libboost-log-dev
  libboost-log1.58-dev libboost-log1.58.0 libboost-math-dev libboost-math1.58-dev libboost-math1.58.0 libboost-mpi-dev libboost-mpi-python-dev
  libboost-mpi-python1.58-dev libboost-mpi-python1.58.0 libboost-mpi1.58-dev libboost-mpi1.58.0 libboost-program-options-dev
  libboost-program-options1.58-dev libboost-program-options1.58.0 libboost-python-dev libboost-python1.58-dev libboost-python1.58.0
  libboost-random-dev libboost-random1.58-dev libboost-random1.58.0 libboost-regex-dev libboost-regex1.58-dev libboost-regex1.58.0
  libboost-serialization-dev libboost-serialization1.58-dev libboost-serialization1.58.0 libboost-signals-dev libboost-signals1.58-dev
  libboost-signals1.58.0 libboost-system-dev libboost-system1.58-dev libboost-system1.58.0 libboost-test-dev libboost-test1.58-dev
  libboost-test1.58.0 libboost-thread-dev libboost-thread1.58-dev libboost-thread1.58.0 libboost-timer-dev libboost-timer1.58-dev
  libboost-timer1.58.0 libboost-tools-dev libboost-wave-dev libboost-wave1.58-dev libboost-wave1.58.0 libboost1.58-dev libboost1.58-tools-dev
  libhwloc-dev libhwloc-plugins libhwloc5 libibverbs-dev libibverbs1 libicu-dev libicu55 libnuma-dev libnuma1 libopenmpi-dev libopenmpi1.10 libxml2
  mpi-default-bin mpi-default-dev ocl-icd-libopencl1 openmpi-bin openmpi-common sgml-base xml-core
Suggested packages:
  libboost-doc graphviz libboost1.58-doc gccxml libmpfrc++-dev libntl-dev xsltproc doxygen docbook-xml docbook-xsl default-jdk fop
  libhwloc-contrib-plugins icu-doc opennmpi-doc opencl-icd gfortran openmpi-checkpoint sgml-base-doc debhelper
The following NEW packages will be installed:
  icu-devtools libboost-all-dev libboost-atomic-dev libboost-atomic1.58-dev libboost-atomic1.58.0 libboost-chrono-dev libboost-chrono1.58-dev
  libboost-chrono1.58.0 libboost-context-dev libboost-context1.58-dev libboost-context1.58.0 libboost-coroutine-dev libboost-coroutine1.58-dev
  libboost-coroutine1.58.0 libboost-date-time-dev libboost-date-time1.58-dev libboost-date-time1.58.0 libboost-dev libboost-exception-dev
  libboost-exception1.58-dev libboost-filesystem-dev libboost-filesystem1.58-dev libboost-filesystem1.58.0 libboost-graph-dev
  libboost-graph-parallel-dev libboost-graph-parallel1.58-dev libboost-graph-parallel1.58.0 libboost-graph1.58-dev libboost-graph1.58.0
  libboost-iostreams-dev libboost-iostreams1.58-dev libboost-iostreams1.58.0 libboost-locale-dev libboost-locale1.58-dev libboost-locale1.58.0
  libboost-log-dev libboost-log1.58-dev libboost-log1.58.0 libboost-math-dev libboost-math1.58-dev libboost-math1.58.0 libboost-mpi-dev
  libboost-mpi-python-dev libboost-mpi-python1.58-dev libboost-mpi-python1.58.0 libboost-mpi1.58-dev libboost-mpi1.58.0 libboost-program-options-dev
  libboost-program-options1.58-dev libboost-program-options1.58.0 libboost-python-dev libboost-python1.58-dev libboost-python1.58.0
  libboost-random-dev libboost-random1.58-dev libboost-random1.58.0 libboost-regex-dev libboost-regex1.58-dev libboost-regex1.58.0
  libboost-serialization-dev libboost-serialization1.58-dev libboost-serialization1.58.0 libboost-signals-dev libboost-signals1.58-dev
  libboost-signals1.58.0 libboost-system-dev libboost-system1.58-dev libboost-system1.58.0 libboost-test-dev libboost-test1.58-dev
  libboost-test1.58.0 libboost-thread-dev libboost-thread1.58-dev libboost-thread1.58.0 libboost-timer-dev libboost-timer1.58-dev
  libboost-timer1.58.0 libboost-tools-dev libboost-wave-dev libboost-wave1.58-dev libboost-wave1.58.0 libboost1.58-dev libboost1.58-tools-dev
  libhwloc-dev libhwloc-plugins libhwloc5 libibverbs-dev libibverbs1 libicu-dev libicu55 libnuma-dev libnuma1 libopenmpi-dev libopenmpi1.10 libxml2
  mpi-default-bin mpi-default-dev ocl-icd-libopencl1 openmpi-bin openmpi-common sgml-base xml-core
0 upgraded, 102 newly installed, 0 to remove and 85 not upgraded.
Need to get 34.1 MB of archives.
After this operation, 264 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y

...
...
...

update-alternatives: using /usr/bin/mpirun.openmpi to provide /usr/bin/mpirun (mpirun) in auto mode
Setting up mpi-default-bin (1.4) ...
Setting up libboost-mpi-python1.58.0 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-mpi-python1.58-dev (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-mpi-python-dev (1.58.0.1ubuntu1) ...
Setting up libboost-program-options1.58.0:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-program-options1.58-dev:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-program-options-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-python1.58-dev (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-python-dev (1.58.0.1ubuntu1) ...
Setting up libboost-random1.58.0:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-random1.58-dev:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-random-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-regex-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-serialization-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-signals1.58.0:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-signals1.58-dev:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-signals-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-system-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-test-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-thread-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-timer1.58.0:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-timer1.58-dev:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-timer-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-wave1.58.0:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-wave1.58-dev:amd64 (1.58.0+dfsg-5ubuntu3.1) ...
Setting up libboost-wave-dev:amd64 (1.58.0.1ubuntu1) ...
Setting up libboost-all-dev (1.58.0.1ubuntu1) ...
Setting up ocl-icd-libopencl1:amd64 (2.2.8-1) ...
Setting up libhwloc-plugins (1.11.2-3) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for sgml-base (1.26+nmu4ubuntu1) ...
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# 
```

Run again cmake .:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# cmake .
CMake Warning (dev) at cmake/CheckCXXSourceCompiles.cmake:16 (IF):
  Policy CMP0054 is not set: Only interpret if() arguments as variables or
  keywords when unquoted.  Run "cmake --help-policy CMP0054" for policy
  details.  Use the cmake_policy command to set the policy and suppress this
  warning.

  Quoted variables like "TR1_SHARED_PTR_USE_TR1_MEMORY" will no longer be
  dereferenced when the policy is set to NEW.  Since the policy is not set
  the OLD behavior will be used.
Call Stack (most recent call first):
  cmake/FindTR1.cmake:19 (check_cxx_source_compiles)
  CMakeLists.txt:42 (INCLUDE)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Boost version: 1.58.0
-- Found the following Boost libraries:
--   thread
--   system
--   chrono
--   date_time
--   atomic
Boost found
-- Boost_INCLUDE_DIR    : /usr/include
-- Configuring done
-- Generating done
-- Build files have been written to: /home/yekyawthu/tool/mgiza/mgizapp
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# 
```

It looks OK!

Let's make:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# make
Scanning dependencies of target snt2coocrmp
[  1%] Building CXX object src/CMakeFiles/snt2coocrmp.dir/snt2cooc-reduce-mem-preprocess.cpp.o
[  2%] Linking CXX executable ../bin/snt2coocrmp
[  2%] Built target snt2coocrmp
Scanning dependencies of target snt2plain
[  4%] Building CXX object src/CMakeFiles/snt2plain.dir/snt2plain.cpp.o
[  5%] Linking CXX executable ../bin/snt2plain
[  5%] Built target snt2plain
Scanning dependencies of target snt2cooc
[  7%] Building CXX object src/CMakeFiles/snt2cooc.dir/snt2cooc.cpp.o
[  8%] Linking CXX executable ../bin/snt2cooc
[  8%] Built target snt2cooc
Scanning dependencies of target mgiza_lib
[ 10%] Building CXX object src/CMakeFiles/mgiza_lib.dir/alignment.cpp.o
[ 11%] Building CXX object src/CMakeFiles/mgiza_lib.dir/AlignTables.cpp.o
[ 13%] Building CXX object src/CMakeFiles/mgiza_lib.dir/ATables.cpp.o
[ 14%] Building C object src/CMakeFiles/mgiza_lib.dir/cmd.c.o
[ 16%] Building CXX object src/CMakeFiles/mgiza_lib.dir/collCounts.cpp.o
[ 17%] Building CXX object src/CMakeFiles/mgiza_lib.dir/Dictionary.cpp.o
[ 19%] Building CXX object src/CMakeFiles/mgiza_lib.dir/ForwardBackward.cpp.o
[ 20%] Building CXX object src/CMakeFiles/mgiza_lib.dir/getSentence.cpp.o
[ 22%] Building CXX object src/CMakeFiles/mgiza_lib.dir/hmm.cpp.o
[ 23%] Building CXX object src/CMakeFiles/mgiza_lib.dir/HMMTables.cpp.o
[ 25%] Building CXX object src/CMakeFiles/mgiza_lib.dir/logprob.cpp.o
[ 26%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model1.cpp.o
[ 27%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model2.cpp.o
[ 29%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model2to3.cpp.o
[ 30%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model345-peg.cpp.o
[ 32%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model3.cpp.o
/home/yekyawthu/tool/mgiza/mgizapp/src/model3.cpp:735:0: warning: "TRAIN_ARGS" redefined
 #define TRAIN_ARGS perp,      trainViterbiPerp, sHandler1,    true, alignfile.c_str(),     true,  modelName,is_final
 ^
/home/yekyawthu/tool/mgiza/mgizapp/src/model3.cpp:481:0: note: this is the location of the previous definition
 #define TRAIN_ARGS perp,      trainViterbiPerp, sHandler1,    dump_files, alignfile.c_str(),     true,  modelName,is_final
 ^
[ 33%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model3_viterbi.cpp.o
[ 35%] Building CXX object src/CMakeFiles/mgiza_lib.dir/model3_viterbi_with_tricks.cpp.o
[ 36%] Building CXX object src/CMakeFiles/mgiza_lib.dir/MoveSwapMatrix.cpp.o
[ 38%] Building CXX object src/CMakeFiles/mgiza_lib.dir/myassert.cpp.o
[ 39%] Building CXX object src/CMakeFiles/mgiza_lib.dir/NTables.cpp.o
[ 41%] Building CXX object src/CMakeFiles/mgiza_lib.dir/Parameter.cpp.o
[ 42%] Building CXX object src/CMakeFiles/mgiza_lib.dir/parse.cpp.o
[ 44%] Building CXX object src/CMakeFiles/mgiza_lib.dir/Perplexity.cpp.o
[ 45%] Building CXX object src/CMakeFiles/mgiza_lib.dir/reports.cpp.o
[ 47%] Building CXX object src/CMakeFiles/mgiza_lib.dir/SetArray.cpp.o
[ 48%] Building CXX object src/CMakeFiles/mgiza_lib.dir/transpair_model3.cpp.o
[ 50%] Building CXX object src/CMakeFiles/mgiza_lib.dir/transpair_model4.cpp.o
[ 51%] Building CXX object src/CMakeFiles/mgiza_lib.dir/transpair_model5.cpp.o
[ 52%] Building CXX object src/CMakeFiles/mgiza_lib.dir/TTables.cpp.o
[ 54%] Building CXX object src/CMakeFiles/mgiza_lib.dir/utility.cpp.o
[ 55%] Building CXX object src/CMakeFiles/mgiza_lib.dir/vocab.cpp.o
[ 57%] Linking CXX static library ../lib/libmgiza.a
[ 57%] Built target mgiza_lib
Scanning dependencies of target mgiza
[ 58%] Building CXX object src/CMakeFiles/mgiza.dir/main.cpp.o
[ 60%] Linking CXX executable ../bin/mgiza
[ 60%] Built target mgiza
Scanning dependencies of target hmmnorm
[ 61%] Building CXX object src/CMakeFiles/hmmnorm.dir/hmmnorm.cxx.o
[ 63%] Linking CXX executable ../bin/hmmnorm
[ 63%] Built target hmmnorm
Scanning dependencies of target plain2snt
[ 64%] Building CXX object src/CMakeFiles/plain2snt.dir/plain2snt.cpp.o
[ 66%] Linking CXX executable ../bin/plain2snt
[ 66%] Built target plain2snt
Scanning dependencies of target symal
[ 67%] Building CXX object src/CMakeFiles/symal.dir/symal.cpp.o
[ 69%] Building C object src/CMakeFiles/symal.dir/cmd.c.o
[ 70%] Linking CXX executable ../bin/symal
[ 70%] Built target symal
Scanning dependencies of target d4norm
[ 72%] Building CXX object src/CMakeFiles/d4norm.dir/d4norm.cxx.o
[ 73%] Linking CXX executable ../bin/d4norm
[ 73%] Built target d4norm
Scanning dependencies of target mkcls
[ 75%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/GDAOptimization.cpp.o
[ 76%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/general.cpp.o
[ 77%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/HCOptimization.cpp.o
[ 79%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/IterOptimization.cpp.o
[ 80%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/KategProblem.cpp.o
[ 82%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/KategProblemKBC.cpp.o
[ 83%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/KategProblemTest.cpp.o
[ 85%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/KategProblemWBC.cpp.o
[ 86%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/mkcls.cpp.o
[ 88%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/MYOptimization.cpp.o
[ 89%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/Optimization.cpp.o
[ 91%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/Problem.cpp.o
[ 92%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/ProblemTest.cpp.o
[ 94%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/RRTOptimization.cpp.o
[ 95%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/SAOptimization.cpp.o
[ 97%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/StatVar.cpp.o
[ 98%] Building CXX object src/mkcls/CMakeFiles/mkcls.dir/TAOptimization.cpp.o
[100%] Linking CXX executable ../../bin/mkcls
[100%] Built target mkcls
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# 
```

Run make install:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# make install
[  2%] Built target snt2coocrmp
[  5%] Built target snt2plain
[  8%] Built target snt2cooc
[ 57%] Built target mgiza_lib
[ 60%] Built target mgiza
[ 63%] Built target hmmnorm
[ 66%] Built target plain2snt
[ 70%] Built target symal
[ 73%] Built target d4norm
[100%] Built target mkcls
Install the project...
-- Install configuration: ""
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/lib/libmgiza.a
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./mgiza
-- Set runtime path of "inst/./mgiza" to ""
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./snt2cooc
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./snt2plain
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./plain2snt
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./symal
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./hmmnorm
-- Set runtime path of "inst/./hmmnorm" to ""
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./d4norm
-- Set runtime path of "inst/./d4norm" to ""
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./snt2coocrmp
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./mkcls
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./force-align-moses.sh
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./giza2bal.pl
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./merge_alignment.py
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./plain2snt-hasvcb.py
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./sntpostproc.py
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./force-align-moses-old.sh
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./run.sh
-- Installing: /home/yekyawthu/tool/mgiza/mgizapp/inst/./snt2cooc.pl
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# 
```

cd ./bin:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp/bin# ./mkcls --help
Fehlerhafte Option: --help
mkcls - a program for making word classes: Usage: 
 mkcls [-nnum] [-ptrain] [-Vfile] opt
-V output classes (Default: no file)
-n number of optimization runs (Default: 1); larger number => better results
-p filename of training corpus (Default: 'train')
Example:
 mkcls -c80 -n10 -pin -Vout opt
 (generates 80 classes for the corpus 'in' and writes the classes in 'out')
Literature: 
 Franz Josef Och: �Maximum-Likelihood-Sch�tzung von Wortkategorien mit Verfahren
 der kombinatorischen Optimierung?Studienarbeit, Universit�t Erlangen-N�rnberg,
 Germany,1995. 
```

You need to update your .bashrc file for running mkcls from everywhere:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp/bin# pwd
/home/yekyawthu/tool/mgiza/mgizapp/bin
```

Update your .bashrc file:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp/bin# vi ~/.bashrc
```

Add following line:
export PATH="/home/yekyawthu/tool/mgiza/mgizapp/bin:$PATH"

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp/bin# cd ..
```

If you haven't run "source" command yet ...

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# mkcls --help
-su: mkcls: command not found
```

Run source command:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# source ~/.bashrc
```

Now You can run mkcls:

```bash
root@2223cfe7eb4a:/home/yekyawthu/tool/mgiza/mgizapp# mkcls --help
Fehlerhafte Option: --help
mkcls - a program for making word classes: Usage: 
 mkcls [-nnum] [-ptrain] [-Vfile] opt
-V output classes (Default: no file)
-n number of optimization runs (Default: 1); larger number => better results
-p filename of training corpus (Default: 'train')
Example:
 mkcls -c80 -n10 -pin -Vout opt
 (generates 80 classes for the corpus 'in' and writes the classes in 'out')
Literature: 
 Franz Josef Och: �Maximum-Likelihood-Sch�tzung von Wortkategorien mit Verfahren
 der kombinatorischen Optimierung?Studienarbeit, Universit�t Erlangen-N�rnberg,
 Germany,1995. 
```

============ FIN =============
