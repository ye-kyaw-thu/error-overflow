# Khmer Spelling Checking Experiment-1

## Original Data Info

```
ye@lst-gpu-3090:~/exp/kh-spell/data/original$ ls
dataall.txt  km_KH.dic.txt  newdiction-kh.word.txt  SBBICkm_KH.txt
ye@lst-gpu-3090:~/exp/kh-spell/data/original$ wc *
   8118   33251 3378199 dataall.txt
  75101   75119 2009584 km_KH.dic.txt
    645     646    8853 newdiction-kh.word.txt
  75038   75063 2139159 SBBICkm_KH.txt
 158902  184079 7535795 total
ye@lst-gpu-3090:~/exp/kh-spell/data/original$
```

File content/format:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/original$ head -n 5 *
==> dataall.txt <==
<អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||(អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្ដាច់សង្គ្រាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>|||សម័យផ្ដាច់សង្គ្រាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
<សំរាប់>ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក<អី>ក៏ថាទៅ|||(សម្រាប់/cphotyp)ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក(អ្វី/typo)ក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed <នឹង>ស៊ែមួយផងបង|||បាតនឹងហើយបងជួយfollowed (និង/vow)ស៊ែមួយផងបង

==> km_KH.dic.txt <==
៛
០/a/P
១/a/P
២/a/P
៣/a/P

==> newdiction-kh.word.txt <==
បាន
ការ
មាន
ជា
នៅ

==> SBBICkm_KH.txt <==
ក
កក
កកកុញ
កកកុះ
កកឈាម
ye@lst-gpu-3090:~/exp/kh-spell/data/original$
```

## To Do

- Extraction of wrong and correct word pairs from the manually collected real spelling error data
- Write a spelling error simulation program based on edit-distance

## Testing with Code from Sokheang

```
ye@lst-gpu-3090:~/exp/kh-spell/data/code$ python3 ./simulat.py ./input.txt > out
```

Check the out file:  

```
how
[('', 'how'), ('h', 'ow'), ('ho', 'w'), ('how', '')]
['ow', 'hw', 'ho']
['ohw', 'hwo']
{'ឆ', 'ង', 'ស', 'ឋ', 'អ', 'យ', 'ហ', 'ព', 'ខ', 'ផ', 'ឃ', 'ឡ', 'ជ', 'ញ', 'ន', 'ឈ', 'ធ', 'ច', 'ថ', 'រ', 'ឌ', 'ប', 'ទ', 'ល', 'ភ', 'ក', 'ម', 'វ', 'ត', 'ឍ', 'ណ', 'គ', 'ដ'}
['ឆow', 'ងow', 'សow', 'ឋow', 'អow', 'យow', 'ហow', 'ពow', 'ខow', 'ផow', 'ឃow', 'ឡow', 'ជow', 'ញow', 'នow', 'ឈow', 'ធow', 'ចow', 'ថow', 'រow', 'ឌow', 'បow', 'ទow', 'លow', 'ភow', 'កow', 'មow', 'វow', 'តow', 'ឍow', 'ណow', 'គow', 'ដow', 'hឆw', 'hងw', 'hសw', 'hឋw', 'hអw', 'hយw', 'hហw', 'hពw', 'hខw', 'hផw', 'hឃw', 'hឡw', 'hជw', 'hញw', 'hនw', 'hឈw', 'hធw', 'hចw', 'hថw', 'hរw', 'hឌw', 'hបw', 'hទw', 'hលw', 'hភw', 'hកw', 'hមw', 'hវw', 'hតw', 'hឍw', 'hណw', 'hគw', 'hដw', 'hoឆ', 'hoង', 'hoស', 'hoឋ', 'hoអ', 'hoយ', 'hoហ', 'hoព', 'hoខ', 'hoផ', 'hoឃ', 'hoឡ', 'hoជ', 'hoញ', 'hoន', 'hoឈ', 'hoធ', 'hoច', 'hoថ', 'hoរ', 'hoឌ', 'hoប', 'hoទ', 'hoល', 'hoភ', 'hoក', 'hoម', 'hoវ', 'hoត', 'hoឍ', 'hoណ', 'hoគ', 'hoដ']
['ឆhow', 'ងhow',
```

I found that not ready to use and I need to rewrite the simulation code.  

## Writing Edit Distance Simulation Code

```python

```

## Compiling Marian on Server

```
      |  ^~~~~
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/sendrecv.dep] Error 1
make[5]: *** Waiting for unfinished jobs....
In file included from /usr/include/cuda_runtime.h:83,
                 from <command-line>:
/usr/include/crt/host_config.h:138:2: error: #error -- unsupported GNU version! gcc versions later than 8 are not supported!
  138 | #error -- unsupported GNU version! gcc versions later than 8 are not supported!
      |  ^~~~~
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/all_reduce.dep] Error 1
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/all_gather.dep] Error 1
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/broadcast.dep] Error 1
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/reduce_scatter.dep] Error 1
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/reduce.dep] Error 1
make[5]: *** [Makefile:53: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/functions.dep] Error 1
make[4]: *** [Makefile:50: /home/yekyaw.thu/tool/marian/build/local/obj/collectives/device/colldevice.a] Error 2
make[4]: *** Waiting for unfinished jobs....
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
(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$
```

## Searching GCC Package Under Conda

```
(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ conda search gcc_linux-64
Loading channels: done
# Name                       Version           Build  Channel
gcc_linux-64                   5.4.0     h98af8de_24  pkgs/main
gcc_linux-64                   7.2.0              19  pkgs/main
gcc_linux-64                   7.2.0              24  pkgs/main
gcc_linux-64                   7.2.0              25  pkgs/main
gcc_linux-64                   7.2.0              26  pkgs/main
gcc_linux-64                   7.2.0     h196ecd4_10  pkgs/main
gcc_linux-64                   7.2.0     h217957b_13  pkgs/main
gcc_linux-64                   7.2.0      h22f992b_7  pkgs/main
gcc_linux-64                   7.2.0      h29fd5c9_3  pkgs/main
gcc_linux-64                   7.2.0     h4118e58_11  pkgs/main
gcc_linux-64                   7.2.0     h550dcbe_27  pkgs/main
gcc_linux-64                   7.2.0      h60973fd_9  pkgs/main
gcc_linux-64                   7.2.0      h6f34251_8  pkgs/main
gcc_linux-64                   7.2.0     haf1f6fa_15  pkgs/main
gcc_linux-64                   7.2.0      hc7b1ceb_1  pkgs/main
gcc_linux-64                   7.2.0     hd763dfe_12  pkgs/main
gcc_linux-64                   7.2.0      hecb3f9c_2  pkgs/main
gcc_linux-64                   7.2.0     hf1c97a4_14  pkgs/main
gcc_linux-64                   7.3.0      h553295d_1  pkgs/main
gcc_linux-64                   7.3.0     h553295d_15  pkgs/main
gcc_linux-64                   7.3.0      h553295d_2  pkgs/main
gcc_linux-64                   7.3.0      h553295d_3  pkgs/main
gcc_linux-64                   7.3.0      h553295d_6  pkgs/main
gcc_linux-64                   7.3.0      h553295d_7  pkgs/main
gcc_linux-64                   7.3.0      h553295d_8  pkgs/main
gcc_linux-64                   7.3.0      h553295d_9  pkgs/main
gcc_linux-64                   7.5.0     h8f34230_30  pkgs/main
gcc_linux-64                   8.2.0      h218040c_2  pkgs/main
gcc_linux-64                   8.2.0      h218040c_3  pkgs/main
gcc_linux-64                   8.4.0     he201b7d_30  pkgs/main
gcc_linux-64                   9.3.0     h1ee779e_30  pkgs/main
gcc_linux-64                  11.2.0      h5c386dc_0  pkgs/main
(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$
```

## Install GCC Version < 8

```
(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ conda install gcc_linux-64==7.5.0
...
...
...
`$ /opt/anaconda/anaconda3/bin/conda install gcc_linux-64==7.5.0`

  environment variables:
                 CIO_TEST=<not set>
        CONDA_DEFAULT_ENV=py3.10.6
                CONDA_EXE=/opt/anaconda/anaconda3/bin/conda
             CONDA_PREFIX=/home/yekyaw.thu/.conda/envs/py3.10.6
    CONDA_PROMPT_MODIFIER=(py3.10.6)
         CONDA_PYTHON_EXE=/opt/anaconda/anaconda3/bin/python
               CONDA_ROOT=/opt/anaconda/anaconda3
              CONDA_SHLVL=1
                     PATH=/opt/anaconda/anaconda3/bin:/home/yekyaw.thu/.conda/envs/py3.10.6/bin:
                          /opt/anaconda/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/s
                          bin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
       REQUESTS_CA_BUNDLE=<not set>
            SSL_CERT_FILE=<not set>

     active environment : py3.10.6
    active env location : /home/yekyaw.thu/.conda/envs/py3.10.6
            shell level : 1
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
             user-agent : conda/4.8.2 requests/2.25.1 CPython/3.7.6 Linux/5.4.0-131-generic ubuntu/20.04.3 glibc/2.31
                UID:GID : 804601154:804600513
             netrc file : None
           offline mode : False


An unexpected error has occurred. Conda has prepared the above report.

If submitted, this report will be used by core maintainers to improve
future releases of conda.
Would you like conda to send this report to the core maintainers?

[y/N]:
Timeout reached. No report sent.

(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$
```

Try with removed one equal sign as follows:  

```
If submitted, this report will be used by core maintainers to improve
future releases of conda.
Would you like conda to send this report to the core maintainers?

[y/N]:
Timeout reached. No report sent.

(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ conda install gcc_linux-64=7.5.0
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: -
Found conflicts! Looking for incompatible packages.
This can take several minutes.  Press CTRL-C to abort.
failed

UnsatisfiableError: The following specifications were found to be incompatible with each other:

Output in format: Requested package -> Available versions

Package libstdcxx-ng conflicts for:
gcc_linux-64=7.5.0 -> gcc_impl_linux-64=7.5.0 -> libstdcxx-ng[version='>=4.9|>=7.5.0']
python=3.10.6 -> libffi[version='>=3.3,<3.4.0a0'] -> libstdcxx-ng[version='>=7.3.0']The following specifications were found to be incompatible with your CUDA driver:

  - feature:/linux-64::__cuda==11.4=0

Your installed CUDA driver is: 11.4


(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ conda install gcc_linux-64=7.5.0

Check the current gcc version:  

(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ gcc --version
gcc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$
```

```
(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$ which gcc && gcc --version
/usr/bin/gcc
gcc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

(py3.10.6) yekyaw.thu@gpu:~/tool/marian/build$
```

## Cmake with NO GPU

```
-- Detecting C compile features - done
-- Project name: marian
-- Project version: v1.11.0+f00d0621
CMake Warning at CMakeLists.txt:79 (message):
  CMAKE_BUILD_TYPE not set; setting to Release


-- Building with -march=native and intrinsics will be chosen automatically by the compiler to match the current machine.
-- Checking support for CPU intrinsics
-- Could not find hardware support for AVX512 on this machine.
CMake Warning at CMakeLists.txt:463 (message):
  COMPILE_CUDA=off : Building only CPU version


-- Not Found Tcmalloc
CMake Warning at CMakeLists.txt:500 (message):
  Cannot find TCMalloc library.  Continuing.


-- Found MKL: -Wl,--start-group;/opt/intel/mkl/lib/intel64/libmkl_intel_ilp64.a;/opt/intel/mkl/lib/intel64/libmkl_sequential.a;/opt/intel/mkl/lib/intel64/libmkl_core.a;-Wl,--end-group
-- VERSION: 0.1.94
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Not Found TCMalloc: TCMALLOC_LIB-NOTFOUND
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE)
-- Configuring done
-- Generating done
-- Build files have been written to: /home/yekyaw.thu/tool/marian/build
(py35) yekyaw.thu@gpu:~/tool/marian/build$ cmake .. -DCOMPILE_CUDA=off
```

Run make command:  

```
(py35) yekyaw.thu@gpu:~/tool/marian/build$ make -j24
...
...
...
[ 90%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group.cpp.o
[ 91%] Building CXX object src/CMakeFiles/marian.dir/training/graph_group_singleton.cpp.o
[ 91%] Building CXX object src/CMakeFiles/marian.dir/training/validator.cpp.o
[ 92%] Building CXX object src/CMakeFiles/marian.dir/training/communicator.cpp.o
[ 92%] Building CXX object src/CMakeFiles/marian.dir/microsoft/quicksand.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/microsoft/sentencepiece.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/microsoft/cosmos.cpp.o
[ 93%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/Converter.cpp.o
[ 94%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/StringUtils.cpp.o
[ 94%] Building CXX object src/CMakeFiles/marian.dir/microsoft/shortlist/utils/ParameterTree.cpp.o
[ 95%] Linking CXX static library ../libmarian.a
[ 95%] Built target marian
Scanning dependencies of target marian_conv
Scanning dependencies of target marian_decoder
Scanning dependencies of target marian_scorer
Scanning dependencies of target marian_vocab
Scanning dependencies of target marian_train
[ 95%] Building CXX object src/CMakeFiles/marian_decoder.dir/command/marian_decoder.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian_conv.dir/command/marian_conv.cpp.o
[ 95%] Building CXX object src/CMakeFiles/marian_vocab.dir/command/marian_vocab.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_scorer.dir/command/marian_scorer.cpp.o
[ 96%] Building CXX object src/CMakeFiles/marian_train.dir/command/marian_main.cpp.o
[ 97%] Linking CXX executable ../marian-vocab
[ 97%] Built target marian_vocab
[ 97%] Linking CXX executable ../marian-decoder
[ 98%] Linking CXX executable ../marian-conv
[ 98%] Linking CXX executable ../marian-scorer
[ 98%] Built target marian_conv
[ 98%] Built target marian_decoder
[ 98%] Built target marian_scorer
[100%] Linking CXX executable ../marian
[100%] Built target marian_train
```

Installation without GPU success!  
Note: Installation was done on one of the CADT server.  

## Called --help

```
(py35) yekyaw.thu@gpu:~/tool/marian/build$ ./marian --help
...
...
...
base-prenorm, transformer-big-prenorm


Validation set options:
  --valid-sets VECTOR ...               Paths to validation corpora: source target
  --valid-freq TEXT=10000u              Validate model every arg updates (append 't' for every arg target labels)
  --valid-metrics VECTOR=cross-entropy ...
                                        Metric to use during validation: cross-entropy, ce-mean-words, perplexity, valid-script, translation, bleu, bleu-detok (deprecated, same as bleu), bleu-segmented, chrf. Multiple metrics can be specified
  --valid-reset-stalled                 Reset all stalled validation metrics when the training is restarted
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
```

## Data Preparation and Preprocessings

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ ls
dataall.txt  khnormal2.py  km_KH.dic.txt  newdiction-kh.word.txt  SBBICkm_KH.txt
```

Create a small file for testing normalization program ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ shuf ./km_KH.dic.txt | head > 10lines.txt
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cat 10lines.txt
សហការី
រួមដៃ
លោកតា
ក្លងស្ពាន់
សាកភ័ក្ខ
នាដកថា
ថ្លៃផ្ដាច់មុខ
សម្ពាធគ្រឹះ
ព្រែកព្នៅ
គូសព្រាង
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Testing normalization program ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ python3 ./khnormal2.py 10lines.txt output.txt
```

Confirmation ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ diff 10lines.txt output.txt
7c7
< ថ្លៃផ្ដាច់មុខ
---
> ថ្លៃផ្តាច់មុខ
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cat output.txt
សហការី
រួមដៃ
លោកតា
ក្លងស្ពាន់
សាកភ័ក្ខ
នាដកថា
ថ្លៃផ្តាច់មុខ
សម្ពាធគ្រឹះ
ព្រែកព្នៅ
គូសព្រាង
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Running for km_KH.dict.txt file ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 ./khnormal2.py km_KH.dic.txt km_KH.dic.normal

real    0m3.680s
user    0m3.668s
sys     0m0.012s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ diff -y --suppress-common-lines km_KH.dic.txt km_KH.dic.normal | wc -l
3994
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Running for SBBICkm_KH.txt file ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 ./khnormal2.py SBBICkm_KH.txt SBBICkm_KH.normal

real    0m3.753s
user    0m3.744s
sys     0m0.009s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ diff -y --suppress-common-lines SBBICkm_KH.txt SBBICkm_KH.normal | wc -l
75039
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Running for newdiction-kh.word.txt ...   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 ./khnormal2.py newdiction-kh.word.txt newdiction-kh.word.normal

real    0m0.037s
user    0m0.033s
sys     0m0.004s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ diff -y --suppress-common-lines newdiction-kh.word.txt newdiction-kh.word.normal | wc -l
9
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Finally, normalization for our manually collected spelling error data ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 ./khnormal2.py ./dataall.txt ./dataall.normal

real    0m6.068s
user    0m6.063s
sys     0m0.005s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ diff -y --suppress-common-lines ./dataall.txt ./dataall.normal | wc
 -l
2070
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Combining some files ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ ls *.normal
dataall.normal  km_KH.dic.normal  newdiction-kh.word.normal  SBBICkm_KH.normal
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cat km_KH.dic.normal SBBICkm_KH.normal newdiction-kh.word.normal > dict.all.normal
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Sorting and make unique ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time sort ./dict.all.normal | uniq > dict.all.normal.uniq

real    0m0.868s
user    0m1.520s
sys     0m0.015s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.all.normal
 150787  150828 4075711 ./dict.all.normal
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.all.normal.uniq
  75910   75936 2070678 ./dict.all.normal.uniq
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

## Make Error Simulation and Parallel Data on Dictionary

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 ./make-edit-error.py ./dict.all.normal.uniq r > ./dict.all.normal.uniq.parallel
Traceback (most recent call last):
  File "/home/ye/exp/kh-spell/data/preprocessing/./make-edit-error.py", line 64, in <module>
    edit1_word = random.choice(edit1(input_word))
  File "/usr/lib/python3.10/random.py", line 378, in choice
    return seq[self._randbelow(len(seq))]
IndexError: list index out of range

real    0m0.045s
user    0m0.033s
sys     0m0.012s
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

To solve above error, I have to delete followings words:  

```
១/a/P
២០
២/a/P
៣០
៣/a/P
```

And I need to remove 1 character words inside the dictionary ...   

## Remove 1 Character Words from the Dictionary

I wrote a perl script:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cat ./remove-one-char-lines.pl
use strict;
use warnings;
use utf8;

# Written by Prof. Ye Kyaw Thu, IDRI, CADT, Cambodia
# Removing one character lines from the dictionary
# Last updated: 21 Oct 2022
# How to run:
# perl ./remove-one-char-lines <input-file>

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

while (!eof($inputFILE)) {

    my $line = <$inputFILE>;
    if ($line !~  /^\s*$/) {
        chomp($line);

        # print lines that length >1
        if (length($line) > 1) {
           print "$line\n";
         }
    }

}

close ($inputFILE);
```

Removing one character words:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ perl ./remove-one-char-lines.pl ./dict.all.normal.uniq.clean1 > ./dict.all.normal.uniq.clean1.word
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.all.normal.uniq.clean1
  75909   75936 2070637 ./dict.all.normal.uniq.clean1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.all.normal.uniq.clean1.word
  75849   75875 2070394 ./dict.all.normal.uniq.clean1.word
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$  
```

Check the top lines ...   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head ./dict.all.normal.uniq.clean1.word
១០
១៦
១៧
២០
៣០
ក៏
កក
កក់
កកកុះ
កកកុញ
```

Check with the tail command:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ tail ./dict.all.normal.uniq.clean1.word
ឲ្យអំណាច
ឲ្យអនុមតិ
ឲ្យអស់
ឲ្យអស់ចំណង់
ឲ្យអស់ចិត្ត
ឲ្យអស់ដៃ
ឲ្យអស់អាចម៍អស់នោម
ឲ្យអស់អាថ៌សេចក្តី
ឲ្យឩបាយ
ឳទក
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

## Make Spelling Error Simulation and Parallel Data on Dictionary

Run again ...   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 make-edit-error.py ./dict.all.normal.uniq.clean1.word
r > dict.parallel
Traceback (most recent call last):
  File "/home/ye/exp/kh-spell/data/preprocessing/make-edit-error.py", line 67, in <module>
    edit2_word = random.choice(edit2(input_word))
  File "/usr/lib/python3.10/random.py", line 378, in choice
    return seq[self._randbelow(len(seq))]
IndexError: list index out of range

real    0m0.044s
user    0m0.040s
sys     0m0.004s
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

I still got above Error!!!

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cat ./dict.parallel
១០       ១
១៦       ៦
១៧
២០       ០
៣០       ០
```

I found one problem is that edit-distance 2 for 2 character words might cause error!!!  
As shown in above ...   

One more error in the code is around here:  

```python
 70       if (random_edit == 1):
 71          edit1_word = random.choice(edit1(input_word))
 72          print(input_word, '\t', edit1_word)
 73       elif (random_edit ==2):
 74          edit2_word = random.choice(edit2(input_word))
 75          print(input_word, '\t', edit2_word)
 ```
I assume that random.choice give the error   
because of the number of element return back from the edit1 or edit2 functions  

Updated the Python Code:  

```python

      if (random_edit == 1):
         #edit1_word = random.choice(edit1(input_word))
         edit1_list = edit1(input_word)
         if edit1_list:
            edit1_word = random.choice(edit1_list)
            print(input_word, '\t', edit1_word)
      elif (random_edit ==2):
         #edit2_word = random.choice(edit2(input_word))
         edit2_list = edit2(input_word)
         if edit2_list:
            edit2_word = random.choice(edit2_list)
            print(input_word, '\t', edit2_word)
```

```
Now running is OK. However, some strange spaces are found between two words.  
When I cleaned with khnormal2.py, the delimeter TAB removed ...  
I think I should use clean space perl script ...   

When I checked with cut commands, it looks OK ...   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cut -f1 ./dict.parallel | wc
  75788   75814 2145644
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cut -f2 ./dict.parallel | wc
  75788   78344 2140590
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

I updated the Python code and finally can run ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 make-edit-error.py ./dict.all.normal.uniq.clean1.word 1 > dict.parallel.edit1

real    0m0.349s
user    0m0.345s
sys     0m0.004s
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time python3 make-edit-error.py ./dict.all.normal.uniq.clean1.word 2 > dict.parallel.edit2

real    0m2.991s
user    0m2.983s
sys     0m0.009s
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Check the edit-distance 1 dictionary size:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.all.normal.uniq.clean1.word
  75849   75875 2070394 ./dict.all.normal.uniq.clean1.word
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.parallel.edit1
  75784  153156 4286609 ./dict.parallel.edit1
```

Check the edit-distance 2 dictionary size:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dict.parallel.edit2
  75737  155021 4286809 ./dict.parallel.edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

## Check the Dictionary Parallel Data

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ shuf ./dict.parallel.edit1 | head -n 15
ភេទបព្វជិត       េទបព្វជិត
ឧបហាស    ឧបហាឧស
ព្រះទ័យ          ពរះទ័យ
សែងព្រះអាទិត្យ   សងែព្រះអាទិត្យ
ទ័ពបម្រុង        ព័ពបម្រុង
អាណាប្រជាជន      អាណាប្រជាជ
កន្លៀតគន្លោង     កន្ល្តគន្លោង
មន្ទីរដូរប្រាក់          មន្ទីរូរប្រាក់
ពុំដែលមានហ្មង    ពុដំែលមានហ្មង
ដោយអស់សង្ឃឹមខ្លលាំង      ដោយអស់សម្ឃឹមខ្លលាំង
រាជគំនាល់        រគជគំនាល់
បណ្តឹងជំនួស      បណ្តឹងជំនួ
វដ្តៈ    វដ្ៈ
ជរាមច្ចុ         ជរាុច្ចុ
ហ៊ឺៈ!    ហឺ៊ៈ!
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ shuf ./dict.parallel.edit2 | head -n 15
ស្លឹកគ្រៃត្រែ    ស្លឹក្គរៃ្ត្រែ
អត់ឲ្យ   អត់្យឲ
ណូឌ      ឌឌូ
ខាប់ដាក់ទឹក      ាាប់ដកា់ទឹក
រសាយជំនឿ         រសាយជសនឿឿ
នឹកម៉ៃ   ឹនកកម៉ៃ
ត្រាចក្រហម       ត្ាាចក្រហមរ
ផ្កុល    ផកល
ស្ទើរនឹង         ្សសទើរនឹង
ពង្រឹងគុណភាព     ពង្ឹរគុណភាព
គឺថា     គថា
ដំបារ    ំដបរា
ល្ហូត    លល្ហតូ
ឈឺខ្ទោកៗ         ្ឺខ្កទោកៗ
នំដង្កូវ         ំនងដ្កូវ
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

## Start Working With Manually Collected Data

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc dataall.normal
   8118   33251 3372117 dataall.normal
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

When I run I got following errors:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ time perl ./mk-spelling-dict.pl ./dataall.normal text > dataall.normal.parallel

Use of uninitialized value $correction in pattern match (m//) at ./mk-spelling-dict.pl line 43, <$inputFILE> line 510.
Use of uninitialized value $correction in pattern match (m//) at ./mk-spelling-dict.pl line 43, <$inputFILE> line 7801.

real    0m0.045s
user    0m0.045s
sys     0m0.000s
```

Check the line number 510 and 7801 sentences.  
I found as follows:    

```
 510 ជូនពរឲ្យបងប្អូនខ្មែរកម្ពុជាក្រោមរួចផុតពីគ្រោះនេះផងចុះ។
     ញ(ឲ្យ/dia)ទទួលកម្មពៀរដែលវាបានសាងមកលើខ្មែរយ៉ាងធ្ងន់ធ្ងរមួយ(សង/typo)មួយ(ម៉ឺន/seq)យ<ម៉ឺន>|||ជូនពរឲ្យបងប្អូនខ្មែរកម្ព
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ sed -n '510p' ./dataall.normal
ជូនពរឲ្យបងប្អូនខ្មែរកម្ពុជាក្រោមរួចផុតពីគ្រោះនេះផងចុះ។
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ sed -n '7801p' ./dataall.normal

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Found blank lines at the end of the dataall.normal file:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ tail ./dataall.normal










ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dataall.normal
   8117   33250 3372116 ./dataall.normal
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ perl ./clean-space.pl ./dataall.normal > ./dataall.normal.clean
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dataall.normal.clean
   7734   33250 3369917 ./dataall.normal.clean
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ perl ./mk-spelling-dict.pl ./dataall.normal.clean text > ./dataall.parallel
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dataall.parallel
 19054  38142 538014 ./dataall.parallel
 ```
 
 ```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head ./dataall.parallel
អញ្ចឹង  អ៊ីចឹង
នឹង     និង
បារាំ   បារាំង
ស្ទួច   ស្ទូច
សំរាប់  សម្រាប់
អី      អ្វី
នឹង     និង
សរសើ    សរសើរ
មើប្បី  ដើម្បី
គាត     គាត់
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ tail ./dataall.parallel
បីដារ   បិតា
កា      ការ
ឯកសណ្ថាន        ឯកសណ្ឋាន
បែ      បែរ
បុក្គល  បុគ្គល
យូ      យូរ
រាន     រៀន
ឈ្ងល់   ឆ្ងល់
បុរស់   បុរស
តំរាប់  តម្រាប់
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

## Splitting Training/Validation/Testing Data

Important!!!  
We have following dataset in total and final data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc dict.parallel.edit1
  75784  153156 4286609 dict.parallel.edit1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc dict.parallel.edit2
  75737  155021 4286809 dict.parallel.edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc dataall.parallel
 19054  38142 538014 dataall.parallel
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Check again the content:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head dict.parallel.edit1
១០       ១១
១៦       ១ ៦
១៧        ១៧
២០       ២២
៣០       ៣
កក់      កកក់
កកកុះ    កកុះ
កកកុញ    កកកុញក
កក់ក្តៅ          កក់ក្ៅត
កក់ក្បាល         កក់កាបាល
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head dict.parallel.edit2
១០       ១
១៦       ១៦៦
១៧       ១១
២០
៣០       ៣០
ក៏       ៏កក៏
កក       ក
កក់      ក ់
កកកុះ    កកកកុុ
កកកុញ    ញកកកកុញ
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head dict.parallel.edit2
១០       ១
១៦       ១៦៦
១៧       ១១
២០
៣០       ៣០
ក៏       ៏កក៏
កក       ក
កក់      ក ់
កកកុះ    កកកកុុ
កកកុញ    ញកកកកុញ
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$
```

Make backup:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ mkdir final-data
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cp dataall.parallel ./final-data/
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cp dict.parallel.edit1 ./final-data/
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cp dict.parallel.edit2 ./final-data/

Shuffling:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ shuf ./dataall.parallel > dataall.parallel.shuf
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ shuf ./dict.parallel.edit1 > dict.parallel.edit1.shuf
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ shuf ./dict.parallel.edit2 > dict.parallel.edit2.shuf
```

Prepare three test data set.  
They are real word error test-set, edit-1 test-set and edit-2 test-set.  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ tail -n 1500 ./dataall.parallel.shuf > test.manual
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ tail -n 1000 dict.parallel.edit1.shuf > test.edit1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ tail -n 1000 dict.parallel.edit2.shuf > test.edit2
```

Preparing three training data:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ head -n 17554 ./dataall.parallel.shuf > train.manual
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ head -n 74784 ./dict.parallel.edit1.shuf > train.edit1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ head -n 74737 ./dict.parallel.edit2.shuf > train.edit2
```

Important!!!  
Actually, column1 vs column2 are different between simulated data and manually collected data.  
For simulated data: col1: correnct-word, col2: wrong-word.  
For manually collected data: col1: wrong-word, col2: correct-word.  
And thus, I have to swap dictionary data-sets.  

Swapping Col1 and Col2 for dictionary data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ ls test*
test.edit1  test.edit2  test.manual
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f1 test.edit1 > c1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f2 test.edit1 > c2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ paste c2 c1 > test.edit1.swap
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f1 test.edit2 > c1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f2 test.edit2 > c2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ paste c2 c1 > test.edit2.swap
```

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ ls train*
train.edit1  train.edit2  train.manual
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f1 train.edit1 > c1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f2 train.edit1 > c2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ paste c2 c1 > train.edit1.swap
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f1 train.edit2 > c1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cut -f2 train.edit2 > c2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ paste c2 c1 > train.edit2.swap


Combining all training data and split as training and valid:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ mkdir final-data
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cat train.manual train.edit1.swap train.edit2.swap > ./final-data/train.pair

backup:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cp test.edit1.swap ./final-data/
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cp test.edit2.swap ./final-data/
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set$ cp test.manual ./final-data/

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ wc *
   1000    2027   56998 test.edit1.swap
   1000    2047   57596 test.edit2.swap
   1500    3008   42104 test.manual
 167075  339237 8954734 train.pair
 170575  346319 9111432 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ tail -n 16000 ./train.pair > valid.final
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ head -n 151075 ./train.pair > train.final

The following are the training/validation/test data-set for NMT modeling:

## Final Data Preprocessings

Here, we will split parallel data into source and target pairs.  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ head -n 3 *
==> 4nmt <==
head: error reading '4nmt': Is a directory

==> test.edit1.swap <==
 កករសារ ក្រសារ
 វតត    វិត
 ក្ របែល        ក្របែល

==> test.edit2.swap <==
 បនញហ្ាផ្ទៃក្នុង        បញ្ហាផ្ទៃក្នុង
 ចរ្ុងមិនឡើងិ   ច្រុងមិនឡើង
 ផលិផតផលចេញពីលទឹកដោះគោ  ផលិតផលចេញពីទឹកដោះគោ

==> test.manual <==
រុស្ស៊ី រុស្ស៊ី
ប៉ុនហ្នឹង       ប៉ុណ្នឹង
ផស់     របស់

==> train.final <==
ក្រោយយ  ក្រោយ
កំបត់   កំបុត
ចឹង     អ៊ីចឹង

==> train.pair <==
ក្រោយយ  ក្រោយ
កំបត់   កំបុត
ចឹង     អ៊ីចឹង

==> valid.final <==
 ក្ហហមឆ្ិន      ក្រហមឆ្អិន
 គន្ថនចនរា      គន្ថចរនា
 ាសសិនិកជន      សាសនិកជន
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$


For training data:  
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f1 train.final > ./4nmt/train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f2 train.final > ./4nmt/train.cr

For valid data:  
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f1 valid.final > ./4nmt/valid.er
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f2 valid.final > ./4nmt/valid.cr

For manual test data:

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f1 test.manual > ./4nmt/test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f2 test.manual > ./4nmt/test.cr

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ mkdir edit1
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ mkdir edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ cd ..

For edit1 test data:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f1 ./test.edit1.swap > ./4nmt/edit1/test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f2 ./test.edit1.swap > ./4nmt/edit1/test
.cr

For edit2 test data:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f1 ./test.edit2.swap > ./4nmt/edit2/test
.er
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ cut -f2 ./test.edit2.swap > ./4nmt/edit2/test
.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$

Folder Structure is as follows:  

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$ tree ./4nmt/
./4nmt/
├── edit1
│   ├── test.cr
│   └── test.er
├── edit2
│   ├── test.cr
│   └── test.er
├── test.cr
├── test.er
├── train.cr
├── train.er
├── valid.cr
└── valid.er

2 directories, 10 files
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data$

## Check Final Train/Valid/Test Data Size

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ wc train.{er,cr}
 151075  155355 4008672 train.er
 151075  151121 4039905 train.cr
 302150  306476 8048577 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ wc valid.{er,cr}
 16000  16756 452932 valid.er
 16000  16005 453225 valid.cr
 32000  32761 906157 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ wc test.{er,cr}
 1500  1508 19902 test.er
 1500  1500 22202 test.cr
 3000  3008 42104 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$

ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt/edit1$ wc *
 1000  1001 28552 test.cr
 1000  1026 28446 test.er
 2000  2027 56998 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt/edit1$ cd ../edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt/edit2$ wc *
 1000  1000 28890 test.cr
 1000  1047 28706 test.er
 2000  2047 57596 total
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt/edit2$

## Building vocab 

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# mkdir vocab
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# cat ./train.er valid.er ./test.er ./edit1/test.er ./edit2/test.er > ./vocab/vocab.er.yml
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# cat ./train.cr valid.cr ./test.cr ./edit1/test.cr ./edit2/te
st.cr > ./vocab/vocab.cr.yml
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt#

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head vocab.er.yml
ក្រោយយ
កំបត់
ចឹង
ទទ៊ទ៊៊៊ៅ
សំរាប់
ម៉េស
ស្មើេ
ក៍
 ចិយ
ក
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head vocab.cr.yml
ក្រោយ
កំបុត
អអ៊ីចឹង
ទៅ
សម្រាប់
ម្ល៉េះ
ស្មើ
ក៏
 ចុយ
ក៏
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab#
 
## Data Folder Path 

Original Data Path:  
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt$ pwd
/home/ye/exp/kh-spell/data/preprocessing/split-3set/final-data/4nmt

Data Folder Path for your reference:  

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# tree
.
|-- edit1
|   |-- test.cr
|   `-- test.er
|-- edit2
|   |-- test.cr
|   `-- test.er
|-- test.cr
|-- test.er
|-- train.cr
|-- train.er
|-- valid.cr
|-- valid.er
`-- vocab
    |-- vocab.cr.yml
    `-- vocab.er.yml

3 directories, 12 files
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt#

## Preparing Shell Script for NMT Running

/home/ye/exp/kh-spell/transformer/4nmt  

#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Khmer Spelling Correction with NMT model
## Last updated: 21 Oct 2022

mkdir model.transformer.dict1;

marian \
    --model model.transformer.dict1/model.npz --type transformer \
    --train-sets 4nmt/train.er 4nmt/train.cr \
    --max-length 100 \
    --vocabs 4nmt/vocab/vocab.er.yml 4nmt/vocab/vocab.cr.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets 4nmt/valid.er 4nmt/valid.cr \
    --valid-translation-output model.transformer.dict1/valid.er-cr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.dict1/train.log --valid-log model.transformer.dict1/valid.log \
    --enc-depth 2 --dec-depth 2 \
	--transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.dict1/config.yml

time marian -c model.transformer.dict1/config.yml  2>&1 | tee transformer.dict1.log


## Training Kh-Spelling Checking NMT Model

[0x7fa3816822f7]                                                       + 0xae2f7
[0x7fa381682558]                                                       + 0xae558
[0x55f9124d8291]                                                       + 0x318291
[0x55f912bc89a5]    YAML::Scanner::  EnsureTokensInQueue  ()           + 0x35
[0x55f912bc8b1d]    YAML::Scanner::  empty  ()                         + 0xd
[0x55f912bbd68a]    YAML::Parser::  ParseDirectives  ()                + 0x1a
[0x55f912bbd7bd]    YAML::Parser::  HandleNextDocument  (YAML::EventHandler&) + 0x2d
[0x55f912bb9da9]    YAML::  Load  (std::istream&)                      + 0x49
[0x55f91271203d]    marian::DefaultVocab::  load  (std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>> const&,  unsigned long) + 0x86d
[0x55f91270182e]    marian::Vocab::  loadOrCreate  (std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>> const&,  std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>> const&,  unsigned long) + 0x4ae
[0x55f91274e874]    marian::data::CorpusBase::  CorpusBase  (std::shared_ptr<marian::Options>,  bool,  unsigned long) + 0x1ac4
[0x55f9127624fe]    marian::data::Corpus::  Corpus  (std::shared_ptr<marian::Options>,  bool,  unsigned long) + 0x6e
[0x55f912638f55]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x2d5
[0x55f912568347]    mainTrainer  (int,  char**)                        + 0x147
[0x7fa3812eed90]                                                       + 0x29d90
[0x7fa3812eee40]    __libc_start_main                                  + 0x80
[0x55f912561995]    _start                                             + 0x25


real    0m3.439s
user    0m0.016s
sys     0m0.038s
root@2328f1decde9:/home/ye/exp/kh-spell/transformer# ./transformer.dict1.sh

Got above error!!!

I think following is the reason:  

[2022-10-21 16:37:45] [data] Loading vocabulary from JSON/Yaml file 4nmt/vocab/vocab.er.yml
[2022-10-21 16:37:45] Error: Unhandled exception of type 'N4YAML15ParserExceptionE': yaml-cpp: error at line 1726, column 13: illegal map value
[2022-10-21 16:37:45] Error: Aborted from void unhandledException() in /temp/marian/src/common/logging.cpp:113

Ha Haa Haa!!!
I haven't build vocab file. I am tired ... :)
Yes, I also have to make segmentation!!!

## Character Segmentation

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh test.cr > ../test.cr
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh test.er > ../test.er
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh train.er > ../train.e
r
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh train.cr > ../train.c
r
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh valid.cr > ../valid.c
r
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# bash ./char-segmentation.sh valid.er > ../valid.e
r
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment#

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1# ls
test.cr  test.er
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1# bash ../char-segmentation.sh ./test.cr > ../../edit1/test.cr
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1# bash ../char-segmentation.sh ./test.er > ..
/../edit1/test.er
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1# cd ../edit2/
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2#
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2# bash ../char-segmentation.sh ./test.cr > ../../edit2/test.cr
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2# bash ../char-segmentation.sh ./test.er > ..
/../edit2/test.er
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2#

## Building Vocab with Character Segmentation

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# mkdir vocab
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# cat train.er valid.er test.er ./edit1/test.er ./edit1/test.er > ./vocab/all.er
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt# cat train.cr valid.cr test.cr ./edit1/test.cr ./edit1/test.c
r > ./vocab/all.cr
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt#

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# marian-vocab < ./all.cr > cr.vocab.yml
[2022-10-21 16:58:01] Creating vocabulary...
[2022-10-21 16:58:01] [data] Creating vocabulary stdout from stdin
[2022-10-21 16:58:02] Finished
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# marian-vocab < ./all.er > er.vocab.yml
[2022-10-21 16:58:14] Creating vocabulary...
[2022-10-21 16:58:14] [data] Creating vocabulary stdout from stdin
[2022-10-21 16:58:14] Finished
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab#

Check the vocab file content:  

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head ./er.vocab.yml
</s>: 0
<unk>: 1
�: 2
�: 3
�: 4
�: 5
�: 6
�: 7
�: 8
�: 9
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head ./cr.vocab.yml
</s>: 0
<unk>: 1
�: 2
�: 3
�: 4
�: 5
�: 6
�: 7
�: 8
�: 9
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/4nmt/vocab#

## Training Khmer Spelling Checking Model with Transformer Archi

ye@lst-gpu-3090:~$ nvidia-smi
Sat Oct 22 00:01:38 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.07    Driver Version: 515.65.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
| 40%   70C    P2   382W / 480W |   2164MiB / 24564MiB |     91%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1700      G   /usr/lib/xorg/Xorg                 58MiB |
|    0   N/A  N/A      2469      G   /usr/bin/gnome-shell               58MiB |
|    0   N/A  N/A     25414      C   marian                           2043MiB |
+-----------------------------------------------------------------------------+

It looks OK ...   
I should enjoy my late dinner ... now 0:02 in Phnom Penh.  


[2022-10-21 17:34:33] Ep. 62 : Up. 94500 : Sen. 128,014 : Cost 0.78355324 * 1,280,045 @ 2,532 after 241,120,740 : Time 8.47s : 151075.54 words/s : gNorm 0.2031 : L.r. 1.2344e-04
[2022-10-21 17:34:37] Seen 151,011 samples
[2022-10-21 17:34:37] Starting data epoch 63 in logical epoch 63
[2022-10-21 17:34:37] [data] Shuffling data
[2022-10-21 17:34:37] [data] Done reading 151,075 sentences
[2022-10-21 17:34:37] [data] Done shuffling 151,075 sentences to temp files
[2022-10-21 17:34:41] Ep. 63 : Up. 95000 : Sen. 26,342 : Cost 0.78252792 * 1,272,658 @ 1,739 after 242,393,398 : Time 8.78s : 145005.98 words/s : gNorm 0.2171 : L.r. 1.2312e-04
[2022-10-21 17:34:41] Saving model weights and runtime parameters to model.transformer.dict1/model.iter95000.npz
[2022-10-21 17:34:41] Saving model weights and runtime parameters to model.transformer.dict1/model.npz
[2022-10-21 17:34:42] Saving Adam parameters
[2022-10-21 17:34:42] [training] Saving training checkpoint to model.transformer.dict1/model.npz and model.transformer.dict1/model.npz.optimizer.npz
[2022-10-21 17:34:46] [valid] Ep. 63 : Up. 95000 : cross-entropy : 5.29923 : stalled 10 times (last best: 4.95204)
[2022-10-21 17:34:47] [valid] Ep. 63 : Up. 95000 : perplexity : 1.214 : stalled 10 times (last best: 1.19868)
[2022-10-21 17:35:05] [valid] Ep. 63 : Up. 95000 : bleu : 91.0272 : stalled 1 times (last best: 91.0274)
[2022-10-21 17:35:05] Training finished
[2022-10-21 17:35:05] Saving model weights and runtime parameters to model.transformer.dict1/model.npz
[2022-10-21 17:35:06] Saving Adam parameters
[2022-10-21 17:35:06] [training] Saving training checkpoint to model.transformer.dict1/model.npz and model.transformer.dict1/model.npz.optimizer.npz

real    34m39.034s
user    35m4.287s
sys     0m44.154s
root@2328f1decde9:/home/ye/exp/kh-spell/transformer# ./transformer.dict1.sh

## Preparing Testing Script

#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for training
## Last updated: 20 Oct 2022

data_path="/home/ye/exp/kh-spell/transformer/4nmt";
src="er"; tgt="cr";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 >
echo "Evaluation with hyp.best.manual.${tgt}, Transformer dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 >
echo "Evaluation with hyp.best.edit1.${tgt}, Transformer dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit1/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 >
echo "Evaluation with hyp.best.edit2.${tgt}, Transformer dictionary model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit2/test.${tgt} < ./hyp.best.edit2.${tgt} >> eval-best-result.txt;

## Testing 

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/model.transformer.dict1# time bash ./test-eval-best.sh
...
...
...
[2022-10-21 18:01:21] Best translation 984 : � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 985 : � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 986 : � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 987 : � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 988 : � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 989 : � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 990 : � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 991 : � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 992 : � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 993 : � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 994 : � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 995 : � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 996 : � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 997 : � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 998 : � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
[2022-10-21 18:01:21] Best translation 999 : � � � � � � � � � � � �
[2022-10-21 18:01:21] Total time: 23.15535s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m8.993s
user    1m6.708s
sys     0m3.060s


## Test Results

root@2328f1decde9:/home/ye/exp/kh-spell/transformer/model.transformer.dict1# cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Transformer dictionary model:
BLEU = 92.89, 96.3/94.6/92.7/90.7 (BP=0.993, ratio=0.993, hyp_len=20556, ref_len=20700)
==========
Evaluation with hyp.best.edit1.cr, Transformer dictionary model:
BLEU = 95.34, 97.9/97.0/95.8/94.1 (BP=0.991, ratio=0.991, hyp_len=26314, ref_len=26551)
==========
Evaluation with hyp.best.edit2.cr, Transformer dictionary model:
BLEU = 90.18, 96.6/94.8/92.1/88.4 (BP=0.971, ratio=0.971, hyp_len=26111, ref_len=26890)
root@2328f1decde9:/home/ye/exp/kh-spell/transformer/model.transformer.dict1#


## Reference

https://stackoverflow.com/questions/27236891/diff-command-to-get-number-of-different-lines-only
https://stackoverflow.com/questions/41076865/python-error-with-random-choice




