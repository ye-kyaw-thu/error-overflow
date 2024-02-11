# Ngram LM Evaluation Tool Development Log

## Create a New Conda Env

```
(base) rnd@gpu:~/tool$ conda create --name LM python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/rnd/anaconda3/envs/LM

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2023.12.12 |       h06a4308_0         126 KB
    openssl-3.0.13             |       h7f8727e_0         5.2 MB
    pip-23.3.1                 |   py38h06a4308_0         2.6 MB
    python-3.8.18              |       h955ad1f_0        25.3 MB
    setuptools-68.2.2          |   py38h06a4308_0         948 KB
    wheel-0.41.2               |   py38h06a4308_0         108 KB
    xz-5.4.5                   |       h5eee18b_0         646 KB
    ------------------------------------------------------------
                                           Total:        34.9 MB

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
  openssl            pkgs/main/linux-64::openssl-3.0.13-h7f8727e_0
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
python-3.8.18        | 25.3 MB   | ############################################### | 100%
pip-23.3.1           | 2.6 MB    | ############################################### | 100%
openssl-3.0.13       | 5.2 MB    | ############################################### | 100%
xz-5.4.5             | 646 KB    | ############################################### | 100%
setuptools-68.2.2    | 948 KB    | ############################################### | 100%
wheel-0.41.2         | 108 KB    | ############################################### | 100%
ca-certificates-2023 | 126 KB    | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate LM
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) rnd@gpu:~/tool$
```

## Conda Activate LM

```
(base) rnd@gpu:~/tool$ conda activate LM
(LM) rnd@gpu:~/tool$
```

## Git Clone KenLM

```
(LM) rnd@gpu:~/tool$ git clone https://github.com/kpu/kenlm
Cloning into 'kenlm'...
remote: Enumerating objects: 14161, done.
remote: Counting objects: 100% (474/474), done.
remote: Compressing objects: 100% (328/328), done.
remote: Total 14161 (delta 162), reused 406 (delta 132), pack-reused 13687
Receiving objects: 100% (14161/14161), 5.91 MiB | 3.22 MiB/s, done.
Resolving deltas: 100% (8042/8042), done.
(LM) rnd@gpu:~/tool$ cd kenlm
(LM) rnd@gpu:~/tool/kenlm$ ls
BUILDING             compile_query_only.sh  Doxyfile     pyproject.toml  util
clean_query_only.sh  COPYING                LICENSE      python
cmake                COPYING.3              lm           README.md
CMakeLists.txt       COPYING.LESSER.3       MANIFEST.in  setup.py
(LM) rnd@gpu:~/tool/kenlm$
```

## Installation of KenLM

Facing error:  

```
(LM) rnd@gpu:~/tool/kenlm$ mkdir -p build
(LM) rnd@gpu:~/tool/kenlm$ cd build
(LM) rnd@gpu:~/tool/kenlm/build$ cmake ..
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is unknown
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
CMake Error at CMakeLists.txt:14 (project):
  No CMAKE_CXX_COMPILER could be found.

  Tell CMake where to find the compiler by setting either the environment
  variable "CXX" or the CMake cache entry CMAKE_CXX_COMPILER to the full path
  to the compiler, or to the compiler name if it is in the PATH.


-- Configuring incomplete, errors occurred!
(LM) rnd@gpu:~/tool/kenlm/build$
```

## Reinstall g++

```
(LM) rnd@gpu:~/tool/kenlm/build$ which g++
(LM) rnd@gpu:~/tool/kenlm/build$
(LM) rnd@gpu:~/tool/kenlm/build$ sudo apt install --reinstall g++
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no longer required:
  screen-resolution-extra
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 1 reinstalled, 0 to remove and 162 not upgraded.
Need to get 1,604 B of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 g++ amd64 4:9.3.0-1ubuntu2 [1,604 B]
Fetched 1,604 B in 1s (1,289 B/s)
(Reading database ... 197785 files and directories currently installed.)
Preparing to unpack .../g++_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking g++ (4:9.3.0-1ubuntu2) over (4:9.3.0-1ubuntu2) ...
Setting up g++ (4:9.3.0-1ubuntu2) ...
Processing triggers for man-db (2.9.1-1) ...
(LM) rnd@gpu:~/tool/kenlm/build$
(LM) rnd@gpu:~/tool/kenlm/build$ g++ --version
g++ (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

(LM) rnd@gpu:~/tool/kenlm/build$
```

## Try KenLM Installation Again

```
(LM) rnd@gpu:~/tool/kenlm$ rm -r build
(LM) rnd@gpu:~/tool/kenlm$
(LM) rnd@gpu:~/tool/kenlm$ mkdir -p build
(LM) rnd@gpu:~/tool/kenlm$ cd build
(LM) rnd@gpu:~/tool/kenlm/build$ cmake ..
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Boost: /usr/lib/x86_64-linux-gnu/cmake/Boost-1.71.0/BoostConfig.cmake (found suitable version "1.71.0", minimum required is "1.41.0") found components: program_options system thread unit_test_framework
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- Found Threads: TRUE
-- Found ZLIB: /usr/lib/x86_64-linux-gnu/libz.so (found version "1.2.11")
-- Found BZip2: /usr/lib/x86_64-linux-gnu/libbz2.so (found version "1.0.8")
-- Looking for BZ2_bzCompressInit
-- Looking for BZ2_bzCompressInit - found
-- Looking for lzma_auto_decoder in /usr/lib/x86_64-linux-gnu/liblzma.so
-- Looking for lzma_auto_decoder in /usr/lib/x86_64-linux-gnu/liblzma.so - found
-- Looking for lzma_easy_encoder in /usr/lib/x86_64-linux-gnu/liblzma.so
-- Looking for lzma_easy_encoder in /usr/lib/x86_64-linux-gnu/liblzma.so - found
-- Looking for lzma_lzma_preset in /usr/lib/x86_64-linux-gnu/liblzma.so
-- Looking for lzma_lzma_preset in /usr/lib/x86_64-linux-gnu/liblzma.so - found
-- Found LibLZMA: /usr/lib/x86_64-linux-gnu/liblzma.so (found version "5.2.4")
-- Looking for clock_gettime in rt
-- Looking for clock_gettime in rt - found
-- Found OpenMP_C: -fopenmp (found version "4.5")
-- Found OpenMP_CXX: -fopenmp (found version "4.5")
-- Found OpenMP: TRUE (found version "4.5")
-- Configuring done (2.8s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rnd/tool/kenlm/build
(LM) rnd@gpu:~/tool/kenlm/build$
```

```
(LM) rnd@gpu:~/tool/kenlm/build$ make -j 20
[  1%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/bignum-dtoa.cc.o
[  2%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/fast-dtoa.cc.o
[  3%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/cached-powers.cc.o
[  4%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/fixed-dtoa.cc.o
[  5%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/bignum.cc.o
[  6%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/string-to-double.cc.o
[  8%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/double-to-string.cc.o
[  9%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/io.cc.o
[  9%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/line_input.cc.o
[ 10%] Building CXX object util/CMakeFiles/kenlm_util.dir/double-conversion/strtod.cc.o
[ 11%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/chain.cc.o
[ 12%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/multi_progress.cc.o
[ 13%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/count_records.cc.o
[ 15%] Building CXX object util/CMakeFiles/kenlm_util.dir/ersatz_progress.cc.o
[ 15%] Building CXX object util/CMakeFiles/kenlm_util.dir/stream/rewindable_stream.cc.o
[ 16%] Building CXX object util/CMakeFiles/kenlm_util.dir/bit_packing.cc.o
[ 18%] Building CXX object util/CMakeFiles/kenlm_util.dir/exception.cc.o
[ 18%] Building CXX object util/CMakeFiles/kenlm_util.dir/file.cc.o
[ 19%] Building CXX object util/CMakeFiles/kenlm_util.dir/file_piece.cc.o
[ 20%] Building CXX object util/CMakeFiles/kenlm_util.dir/float_to_string.cc.o
[ 21%] Building CXX object util/CMakeFiles/kenlm_util.dir/integer_to_string.cc.o
[ 22%] Building CXX object util/CMakeFiles/kenlm_util.dir/mmap.cc.o
[ 23%] Building CXX object util/CMakeFiles/kenlm_util.dir/murmur_hash.cc.o
[ 25%] Building CXX object util/CMakeFiles/kenlm_util.dir/parallel_read.cc.o
[ 26%] Building CXX object util/CMakeFiles/kenlm_util.dir/pool.cc.o
[ 27%] Building CXX object util/CMakeFiles/kenlm_util.dir/read_compressed.cc.o
[ 28%] Building CXX object util/CMakeFiles/kenlm_util.dir/scoped.cc.o
[ 29%] Building CXX object util/CMakeFiles/kenlm_util.dir/spaces.cc.o
[ 30%] Building CXX object util/CMakeFiles/kenlm_util.dir/string_piece.cc.o
[ 31%] Building CXX object util/CMakeFiles/kenlm_util.dir/usage.cc.o
[ 32%] Linking CXX static library ../lib/libkenlm_util.a
[ 32%] Built target kenlm_util
[ 33%] Building CXX object util/CMakeFiles/probing_hash_table_benchmark.dir/probing_hash_table_benchmark_main.cc.o
[ 34%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/arpa_io.cc.o
[ 36%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/phrase.cc.o
[ 36%] Building CXX object lm/CMakeFiles/kenlm.dir/bhiksha.cc.o
[ 37%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/vocab.cc.o
[ 38%] Building CXX object lm/CMakeFiles/kenlm.dir/binary_format.cc.o
[ 39%] Building CXX object lm/CMakeFiles/kenlm.dir/config.cc.o
[ 40%] Building CXX object lm/CMakeFiles/kenlm.dir/model.cc.o
[ 41%] Building CXX object lm/CMakeFiles/kenlm.dir/lm_exception.cc.o
[ 42%] Building CXX object lm/CMakeFiles/kenlm.dir/quantize.cc.o
[ 43%] Building CXX object lm/CMakeFiles/kenlm.dir/search_hashed.cc.o
[ 44%] Building CXX object lm/CMakeFiles/kenlm.dir/read_arpa.cc.o
[ 45%] Building CXX object lm/CMakeFiles/kenlm.dir/virtual_interface.cc.o
[ 46%] Building CXX object lm/CMakeFiles/kenlm.dir/search_trie.cc.o
[ 47%] Building CXX object lm/CMakeFiles/kenlm.dir/trie.cc.o
[ 48%] Building CXX object lm/CMakeFiles/kenlm.dir/trie_sort.cc.o
[ 50%] Building CXX object lm/CMakeFiles/kenlm.dir/value_build.cc.o
[ 51%] Building CXX object lm/CMakeFiles/kenlm.dir/sizes.cc.o
[ 52%] Building CXX object lm/CMakeFiles/kenlm.dir/vocab.cc.o
[ 53%] Building CXX object lm/CMakeFiles/kenlm.dir/common/model_buffer.cc.o
[ 54%] Building CXX object lm/CMakeFiles/kenlm.dir/common/print.cc.o
[ 55%] Building CXX object lm/CMakeFiles/kenlm.dir/common/renumber.cc.o
[ 56%] Building CXX object lm/CMakeFiles/kenlm.dir/common/size_option.cc.o
[ 57%] Linking CXX static library ../../lib/libkenlm_filter.a
[ 57%] Built target kenlm_filter
[ 58%] Linking CXX static library ../lib/libkenlm.a
[ 58%] Built target kenlm
[ 59%] Building CXX object lm/CMakeFiles/fragment.dir/fragment_main.cc.o
[ 60%] Building CXX object lm/CMakeFiles/query.dir/query_main.cc.o
[ 61%] Building CXX object lm/filter/CMakeFiles/filter.dir/filter_main.cc.o
[ 62%] Building CXX object lm/CMakeFiles/kenlm_benchmark.dir/kenlm_benchmark_main.cc.o
[ 64%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/backoff_reunification.cc.o
[ 64%] Building CXX object lm/filter/CMakeFiles/phrase_table_vocab.dir/phrase_table_vocab_main.cc.o
[ 65%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/corpus_count.cc.o
[ 67%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/adjust_counts.cc.o
[ 67%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/bounded_sequence_encoding.cc.o
[ 68%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/initial_probabilities.cc.o
[ 70%] Building CXX object lm/CMakeFiles/build_binary.dir/build_binary_main.cc.o
[ 70%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/pipeline.cc.o
[ 71%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/merge_vocab.cc.o
[ 72%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/output.cc.o
[ 73%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/merge_probabilities.cc.o
[ 76%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/normalize.cc.o
[ 76%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/pipeline.cc.o
[ 77%] Building CXX object lm/builder/CMakeFiles/kenlm_builder.dir/interpolate.cc.o
[ 78%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/split_worker.cc.o
[ 79%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/tune_derivatives.cc.o
[ 80%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/tune_instances.cc.o
[ 81%] Linking CXX executable ../bin/fragment
[ 81%] Built target fragment
[ 82%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/tune_weights.cc.o
[ 83%] Linking CXX executable ../bin/build_binary
[ 83%] Built target build_binary
[ 84%] Building CXX object lm/interpolate/CMakeFiles/kenlm_interpolate.dir/universal_vocab.cc.o
[ 85%] Linking CXX executable ../bin/query
[ 86%] Linking CXX executable ../../bin/phrase_table_vocab
[ 86%] Built target query
[ 86%] Built target phrase_table_vocab
[ 87%] Linking CXX executable ../bin/probing_hash_table_benchmark
[ 87%] Built target probing_hash_table_benchmark
[ 88%] Linking CXX static library ../../lib/libkenlm_interpolate.a
[ 88%] Built target kenlm_interpolate
[ 89%] Building CXX object lm/interpolate/CMakeFiles/interpolate.dir/interpolate_main.cc.o
[ 90%] Building CXX object lm/interpolate/CMakeFiles/streaming_example.dir/streaming_example_main.cc.o
[ 91%] Linking CXX static library ../../lib/libkenlm_builder.a
[ 91%] Built target kenlm_builder
[ 92%] Building CXX object lm/builder/CMakeFiles/lmplz.dir/lmplz_main.cc.o
[ 93%] Building CXX object lm/builder/CMakeFiles/count_ngrams.dir/count_ngrams_main.cc.o
[ 94%] Linking CXX executable ../../bin/filter
[ 94%] Built target filter
[ 95%] Linking CXX executable ../bin/kenlm_benchmark
[ 95%] Built target kenlm_benchmark
[ 96%] Linking CXX executable ../../bin/interpolate
[ 97%] Linking CXX executable ../../bin/lmplz
[ 97%] Built target interpolate
[ 97%] Built target lmplz
[ 98%] Linking CXX executable ../../bin/streaming_example
[ 98%] Built target streaming_example
[100%] Linking CXX executable ../../bin/count_ngrams
[100%] Built target count_ngrams
(LM) rnd@gpu:~/tool/kenlm/build$
```

## Check lmplz Command

```
(LM) rnd@gpu:~/tool/kenlm/build$ tree ./bin
./bin
├── build_binary
├── count_ngrams
├── filter
├── fragment
├── interpolate
├── kenlm_benchmark
├── lmplz
├── phrase_table_vocab
├── probing_hash_table_benchmark
├── query
└── streaming_example

0 directories, 11 files
(LM) rnd@gpu:~/tool/kenlm/build$
```

## Add Path to .bashrc

(LM) rnd@gpu:~/tool/kenlm/build/bin$ nano ../../../../.bashrc  

```
# for KenLM

export PATH=$PATH:/home/rnd/tool/kenlm/build/bin;
```

Run lmplz command ...  

```
(LM) rnd@gpu:~/tool/kenlm/build/bin$ source ../../../../.bashrc
(base) rnd@gpu:~/tool/kenlm/build/bin$ lmplz --help
Builds unpruned language models with modified Kneser-Ney smoothing.

Please cite:
@inproceedings{Heafield-estimate,
  author = {Kenneth Heafield and Ivan Pouzyrevsky and Jonathan H. Clark and Philipp Koehn},
  title = {Scalable Modified {Kneser-Ney} Language Model Estimation},
  year = {2013},
  month = {8},
  booktitle = {Proceedings of the 51st Annual Meeting of the Association for Computational Linguistics},
  address = {Sofia, Bulgaria},
  url = {http://kheafield.com/professional/edinburgh/estimate\_paper.pdf},
}

Provide the corpus on stdin.  The ARPA file will be written to stdout.  Order of
the model (-o) is the only mandatory option.  As this is an on-disk program,
setting the temporary file location (-T) and sorting memory (-S) is recommended.

Memory sizes are specified like GNU sort: a number followed by a unit character.
Valid units are % for percentage of memory (supported platforms only) and (in
increasing powers of 1024): b, K, M, G, T, P, E, Z, Y.  Default is K (*1024).
This machine has 67349291008 bytes of memory.

Language model building options:
  -h [ --help ]                         Show this help message
  -o [ --order ] arg                    Order of the model
  --interpolate_unigrams [=arg(=1)] (=1)
                                        Interpolate the unigrams (default) as
                                        opposed to giving lots of mass to <unk>
                                        like SRI.  If you want SRI's behavior
                                        with a large <unk> and the old lmplz
                                        default, use --interpolate_unigrams 0.
  --skip_symbols                        Treat <s>, </s>, and <unk> as
                                        whitespace instead of throwing an
                                        exception
  -T [ --temp_prefix ] arg (=/tmp/)     Temporary file prefix
  -S [ --memory ] arg (=80%)            Sorting memory
  --minimum_block arg (=8K)             Minimum block size to allow
  --sort_block arg (=64M)               Size of IO operations for sort
                                        (determines arity)
  --block_count arg (=2)                Block count (per order)
  --vocab_estimate arg (=1000000)       Assume this vocabulary size for
                                        purposes of calculating memory in step
                                        1 (corpus count) and pre-sizing the
                                        hash table
  --vocab_pad arg (=0)                  If the vocabulary is smaller than this
                                        value, pad with <unk> to reach this
                                        size. Requires --interpolate_unigrams
  --verbose_header                      Add a verbose header to the ARPA file
                                        that includes information such as token
                                        count, smoothing type, etc.
  --text arg                            Read text from a file instead of stdin
  --arpa arg                            Write ARPA to a file instead of stdout
  --intermediate arg                    Write ngrams to intermediate files.
                                        Turns off ARPA output (which can be
                                        reactivated by --arpa file).  Forces
                                        --renumber on.
  --renumber                            Renumber the vocabulary identifiers so
                                        that they are monotone with the hash of
                                        each string.  This is consistent with
                                        the ordering used by the trie data
                                        structure.
  --collapse_values                     Collapse probability and backoff into a
                                        single value, q that yields the same
                                        sentence-level probabilities.  See
                                        http://kheafield.com/professional/edinb
                                        urgh/rest_paper.pdf for more details,
                                        including a proof.
  --prune arg                           Prune n-grams with count less than or
                                        equal to the given threshold.  Specify
                                        one value for each order i.e. 0 0 1 to
                                        prune singleton trigrams and above.
                                        The sequence of values must be
                                        non-decreasing and the last value
                                        applies to any remaining orders.
                                        Default is to not prune, which is
                                        equivalent to --prune 0.
  --limit_vocab_file arg                Read allowed vocabulary separated by
                                        whitespace. N-grams that contain
                                        vocabulary items not in this list will
                                        be pruned. Can be combined with --prune
                                        arg
  --discount_fallback [=arg(=0.5 1 1.5)]
                                        The closed-form estimate for Kneser-Ney
                                        discounts does not work without
                                        singletons or doubletons.  It can also
                                        fail if these values are out of range.
                                        This option falls back to
                                        user-specified discounts when the
                                        closed-form estimate fails.  Note that
                                        this option is generally a bad idea:
                                        you should deduplicate your corpus
                                        instead.  However, class-based models
                                        need custom discounts because they lack
                                        singleton unigrams.  Provide up to
                                        three discounts (for adjusted counts 1,
                                        2, and 3+), which will be applied to
                                        all orders where the closed-form
                                        estimates fail.

(base) rnd@gpu:~/tool/kenlm/build/bin$
```

## Preprocessing

admin account ကနေ user account ကို ပြန်ပြောင်း။ အထက်ပါလိုမျိုးပဲ .bashrc မှာ kenlm path ကို ဖြည့်ပြီး lmplz ကို run လို့ရအောင်ပြင်ခဲ့။  

cleaning file ကို download လုပ် ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/python/clean_non_burmese.py
--2024-02-11 10:46:03--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/python/clean_non_burmese.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.111.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5747 (5.6K) [text/plain]
Saving to: ‘clean_non_burmese.py’

clean_non_burmese.py   100%[==========================>]   5.61K  --.-KB/s    in 0s

2024-02-11 10:46:04 (52.2 MB/s) - ‘clean_non_burmese.py’ saved [5747/5747]

(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

--help ခေါ်ကြည့်...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ python ./clean_non_burmese.py --help
usage: clean_non_burmese.py [-h] [--input INPUT] [--output OUTPUT] [--verbose]
                            [--space_cleaning]

Remove unwanted characters from text while preserving the overall structure

optional arguments:
  -h, --help            show this help message and exit
  --input INPUT         Input file path
  --output OUTPUT       Output file path
  --verbose             Print counts of removed characters
  --space_cleaning, -s  Clean up space characters (remove leading/trailing
                        spaces, multiple spaces)
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

cleaning လုပ် ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./clean_non_burmese.py --input ../corpus
/myWord_myPOS_myPara_myNovelv1_wordseg.shuf --output ./corpus/myWord_myPOS_myPara_myNovel1
v1_wordseg.shuf.cleaned --verbose --space_cleaning
Removed 923091 unwanted characters

real    0m3.917s
user    0m3.272s
sys     0m0.432s
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## Building ngram LM Model with KenLM  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ time lmplz -o 5 < ./corpus/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned > 5gram.arpa
=== 1/5 Counting and sorting n-grams ===
Reading /home/yekyaw.thu/exp/lm/kenlm/corpus/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Unigram tokens 6931666 types 103089
=== 2/5 Calculating and sorting adjusted counts ===
Chain sizes: 1:1237068 2:5256409088 3:9855767552 4:15769227264 5:22996791296
Statistics:
1 103089 D1=0.682236 D2=1.03897 D3+=1.30468
2 1155572 D1=0.735122 D2=1.06525 D3+=1.36774
3 3263668 D1=0.830523 D2=1.18537 D3+=1.39379
4 4672136 D1=0.908363 D2=1.30372 D3+=1.45238
5 5134544 D1=0.817936 D2=1.74513 D3+=1.59389
Memory estimate for binary LM:
type     MB
probing 298 assuming -p 1.5
probing 351 assuming -r models -p 1.5
trie    143 without quantization
trie     78 assuming -q 8 -b 8 quantization
trie    126 assuming -a 22 array pointer compression
trie     61 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:1237068 2:18489152 3:65273360 4:112131264 5:143767232
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
------------------------------------------------------------------------------------------++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++******************************************************************************************####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:1237068 2:18489152 3:65273360 4:112131264 5:143767232
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
------------------------------------------------------------------------------------------++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++******************************************************************************************####################################################################################################
=== 5/5 Writing ARPA model ===
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
------------------------------------------------------------------------------------------++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++****************************************************************************************************
Name:lmplz      VmPeak:52789084 kB      VmRSS:27768 kB  RSSMax:9460956 kB       user:9.655sys:5.12208     CPU:14.7771     real:11.4181

real    0m11.423s
user    0m9.656s
sys     0m5.123s
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## Check ARPA LM File

အရင်ဆုံး သပ်သပ်ရပ်ရပ်ဖြစ်အောင် model/ folder အောက်မှာ ပြောင်းသိမ်းခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ mkdir model
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ mv 5gram.arpa ./model/
```

Check the LM file ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ head -n 50 ./model/5gram.arpa
\data\
ngram 1=103089
ngram 2=1155572
ngram 3=3263668
ngram 4=4672136
ngram 5=5134544

\1-grams:
-6.100141       <unk>   0
0       <s>     -1.1136011
-2.0540004      </s>    0
-3.4277027      ကြိုးစား        -0.7406527
-2.2756474      နေ      -1.1480055
-2.2833006      ပါ      -0.7934854
-2.604671       တယ်     -0.6414488
-3.1418326      အားလုံး -0.5147764
-4.2948036      ညှစ်    -0.36235598
-4.213913       လယ်ယာ   -0.48633564
-3.391057       လုပ်ငန်း        -0.59556603
-2.0045376      ကို     -0.7854268
-3.8257236      အဓိက    -0.36103
-3.6672733      လုပ်ကိုင်       -0.77430165
-2.4600196      ပြီး    -0.61884594
-3.6177957      မြန်မာ့ -0.49834687
-4.232767       ဓလေ့    -0.38696668
-5.971  ဝါးဓနိ  -0.13364083
-3.0633998      အိမ်    -0.84310097
-2.2266874      များ    -0.8185917
-3.8410883      အများစု -0.58294964
-5.2424035      စုဖွဲ့  -0.20037098
-3.8763692      တည်ရှိ  -0.7152147
-3.137169       သည့်    -0.40706497
-3.4997754      အေး     -0.54355377
-3.372058       ကျေးရွာ -0.67367
-2.4780574      ၏       -0.52887875
-2.8332143      ရေ      -0.585245
-4.5235586      အရင်းအမြစ်      -0.36342874
-2.9719703      အဖြစ်   -0.5106326
-3.7736254      စပါး    -0.42303085
-5.504938       ရေသွင်း -0.4660563
-3.6869268      စိုက်ပျိုး      -0.70568806
-2.9553792      ရန်     -0.5211003
-2.854191       အတွက်   -0.48012853
-3.672546       နိုင်ငံတော်     -0.6230423
-3.3581207      အစိုးရ  -0.6330904
-2.0195286      က       -0.74369365
-4.8169656      တူးမြောင်း      -0.21687807
-2.3460748      တစ်     -1.2043443
-3.22168        ခု      -0.5341255
-3.9086382      ဆောက်လုပ်       -0.66838413
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Check with tail command ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ tail -n 50 ./model/5gram.arpa
-0.6649076      <s> အင်္ဂလိပ် အရေး ပိုင် မစ္စတာဘရောင်း
-0.8592887      ရွာ လယ် ညောင်ပင် အောက် ပြေးပြေးလွှားလွှား
-0.6396752      ဘေး က ပက်လက်ကုလားထိုင် ပေါ် မှာခြေပစ်လက်ပစ်ထိုင်
-0.65780675     ဤ မြင်း ကြီး မှာ ဗယ်
-0.57897574     ထွက် လာ သည် ပါ းစုန့်
-0.5606526      လဲ ဗလ ဝါ မ ုက္ခ
-0.66792935     သံ တ ဂျောင်း ဂျောင်း ခြူသံတချွင်ချွင်
-0.65565056     စိမ်း ကွမ်းတောင်ကိုင် တော့ မည့် ဒင်္ဂ
-0.5867255      တာ များ ယော က ျ်ားဘ
-0.5398557      ကြီး ပီဂျီဝုဒ် ဟော က ်စ်ဂျိဗ်စ်
-0.41680175     မှာ ထိုင် လျှင် တင် ပျှဉ်
-0.41686422     သူ တို့ နှာခေါင်း ရ ှုံ
-1.718125       ဘာ လဲ သိ လား ဆွေ့
-0.8680346      ကောင်း ဘူး လှေ တွေ အနောက်ဘက်ကမ်း
-0.7268616      ချောင်း ရှိ တဲ့ က တ္တူးကတ္တ
-0.55592275     လောလောဆယ် အား ဖြင့် လုပ် ခတလဝဝိ
-1.0075617      သူ တို့ က သိပ် ဋ္ဌေး
-0.55594134     ကြ မည် ကြမ်းပြင် များ ဂျွမ်းခနဲဂျွမ်း
-0.58700573     က လေး တော် က ီမန်း
-0.41684306     ပုံ နှမ ကား ရာ းခွ
-0.4168356      မှ ဤ အရပ် ကား ပဋိရူပ
-0.5629921      ကို ကို့ ကို စေ့စေ့ ငှငှ
-0.39488256     လို ပါ မောင် စေ့စေ့ ငှငှ
-0.6001961      သည် မြင်းခြံ မြောက် လက် ဆီမီးခုံ
-1.0117141      နှစ် က တုန်း က ယစ်မျိုး
-0.58976126     တဲ့ အခါ နိုင်ငံ ရေး လုပ်ဖော်ကိုင်ဘက်
-0.71721303     လိုက် မင်း သား ကို အဝှာ
-0.6112564      ချယ် က အကြီးဆုံး သား သြရဿ
-0.5873692      သား သြရဿ သား ကြီး သြရဿ
-0.41681442     ဘက် သ ကတ် ဘက် သချာ
-0.58317256     ဆင် နင်း ပ စေ ဥရု
-0.3942994      ရောင် ကြောင် ကား သိဒ္ဓိ မဏိ
-0.65791094     ကြောက်ရွံ့ လွယ် ခြင်း သည် ကြက်ပျောက်ငှက်ပျောက်
-0.5839636      ကြိုတင် ကြံစည် ထား သမျှ ကြက်ပျောက်ငှက်ပျောက်
-0.41637003     မ မီ ချင် ထို့ကြောင့် ဖောဋ္ဌဗ္ဗ
-0.4167947      တွေး ကာ ဆွေး လ ျလျဟဟလေးတွတွ
-1.8327162      မ ရှိ တာ က ်ု
-0.589644       ကော့ ဖ် က က ်ဖ်ကာမိုရေဗီး
-0.41686422     သည် မှာ အင်္ဂလိပ် ရ ှ်ကျူးန်
-0.656572       အသရေ မဲ့ သော က ာဠကဏ္ဏီ
-0.63017225     ခေါ် ပါ ဦး ကွယ့် ဧည်သည်
-0.6533201      လေး ရဲ့ ခေါင်း မှာ ဖဲပြားချည်
-0.65199643     ရှိ သေး ၏ ဆရာ ဝန့်
-0.5877174      မြှောက် ပြ သည် ဆရာ ဝန့်
-0.57509375     ဆို သော်လည်း တစ် ပါ းယောကျ်ား
-0.5897417      တ ကျိပ် တို့ လည်း ဝိပ္ပဋိ
-0.4145626      သူ တို့ ရဲ့ ယုတ် ္တိ
-0.5490875      တ ရက်နေ့ သည် အမ ြိတ္တ

\end\
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Normalization မလုပ်ထားလို့ တချို့ ပြဿနာတွေရှိသေးတယ်။  
spelling ပြဿနာလည်း ရှိဦးမှာ ...  

## Build Binary LM File  

Check the command ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ build_binary --help
Usage: build_binary [-u log10_unknown_probability] [-s] [-i] [-v] [-w mmap|after] [-p probing_multiplier] [-T trie_temporary] [-S trie_building_mem] [-q bits] [-b bits] [-a bits] [type] input.arpa [output.mmap]

-u sets the log10 probability for <unk> if the ARPA file does not have one.
   Default is -100.  The ARPA file will always take precedence.
-s allows models to be built even if they do not have <s> and </s>.
-i allows buggy models from IRSTLM by mapping positive log probability to 0.
-v disables inclusion of the vocabulary in the binary file.
-w mmap|after determines how writing is done.
   mmap maps the binary file and writes to it.  Default for trie.
   after allocates anonymous memory, builds, and writes.  Default for probing.
-r "order1.arpa order2 order3 order4" adds lower-order rest costs from these
   model files.  order1.arpa must be an ARPA file.  All others may be ARPA or
   the same data structure as being built.  All files must have the same
   vocabulary.  For probing, the unigrams must be in the same order.

type is either probing or trie.  Default is probing.

probing uses a probing hash table.  It is the fastest but uses the most memory.
-p sets the space multiplier and must be >1.0.  The default is 1.5.

trie is a straightforward trie with bit-level packing.  It uses the least
memory and is still faster than SRI or IRST.  Building the trie format uses an
on-disk sort to save memory.
-T is the temporary directory prefix.  Default is the output file name.
-S determines memory use for sorting.  Default is 80%.  This is compatible
   with GNU sort.  The number is followed by a unit: % for percent of physical
   memory, b for bytes, K for Kilobytes, M for megabytes, then G,T,P,E,Z,Y.
   Default unit is K for Kilobytes.
-q turns quantization on and sets the number of bits (e.g. -q 8).
-b sets backoff quantization bits.  Requires -q and defaults to that value.
-a compresses pointers using an array of offsets.  The parameter is the
   maximum number of bits encoded by the array.  Memory is minimized subject
   to the maximum, so pick 255 to minimize memory.

-h print this help message.

Get a memory estimate by passing an ARPA file without an output file name.
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Build binary file based on .arpa file:  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ time build_binary trie ./model/5gram.arpa ./model/5gram.bin
Reading ./model/5gram.arpa
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Identifying n-grams omitted by SRI
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Writing trie
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
SUCCESS

real    0m12.756s
user    0m9.962s
sys     0m0.601s
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Check the output file ...  

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$ ls -lh ./model/
total 1.2G
-rw-r--r-- 1 yekyaw.thu domain users 1013M Feb 11 10:51 5gram.arpa
-rw-r--r-- 1 yekyaw.thu domain users  147M Feb 11 10:59 5gram.bin
(base) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## Vocab File Preparation

တကယ်က KenLM ကို ဆောက်တဲ့အခါမှာ vocab ဖိုင်ကိုလည်း ပေးပြီး အဲဒီ vocab ထဲမှာရှိတဲ့ စာလုံးတွေကိုပဲ limit လုပ်ပြီးဆောက်ခိုင်းတာမျိုးလုပ်လို့ ရတယ်။ ပြီးတော့ LM ကို evaluation လုပ်တဲ့အခါမှာလည်း အဲဒီ vocab ဖိုင်ကို သုံးတာမျိုးလည်း လုပ်လို့ ရတယ်။  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./mk_vocab.py --input ./corpus/myWord_myPO
S_myPara_myNovel1v1_wordseg.shuf.cleaned --output ./corpus/vocab.txt
Vocabulary written to './corpus/vocab.txt'

real    0m1.043s
user    0m0.981s
sys     0m0.040s
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Check the output vocab file:  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ ls -lh ./corpus/vocab.txt
-rw-r--r-- 1 yekyaw.thu domain users 2.8M Feb 11 11:31 ./corpus/vocab.txt
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Let's check the content of the vocab file ...  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ head ./corpus/vocab.txt
က
ကက
ကကက
ကကကကက
ကကကျွတ်
ကကကျွတ်ကကကျွတ်
ကကစ်လေး
ကကတစ်
ကကတစ်ကို
ကကန
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ tail ./corpus/vocab.txt
၍ကြ
၎
၎င်း
၎င်းက
၎င်းကို
၎င်းထဲမှာ
၎အေးမြတ်သူ
၏
၏စိုင်း
၏န
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

လက်တွေ့ ပြဿနာတွေကိုလည်း မြင်ရလိမ့်မယ် ...  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ shuf ./corpus/vocab.txt | head -n 30
မြင်းကွင်း
ဆည်ယူ
သုံးသိန်းနှစ်သောင်း
အသုံးမခံ
ကျေးကျေး
စက်တင်ဘာလ
တောက်တိုမယ်ရ
ဒေါ်ခင်မိုးဝေ
ဘစု
မျက်နှာပြင်
ကျိုက်ကဆော့
အတော်ကလေး
ခြေတံရှည်အိမ်
ခြားတယ်
မောင်ရိုဟန်
ကကြား
ကနားလေး
ကွေကာစီတီ
ပြားကပ်
သင်ကြား
တောင်ကုတ်
ရီးရယ်
လမင်းကြီး
အရိုင်းဆန်ဆန်
ဥပေါသထ
ပြောလို့ရ
ကြမ်းပေါက်
သေသူ
မိုက်ကြေး
စောင်းငန်း
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Python code is as follows:  
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ cat mk_vocab.py  

```python
"""

for make vocab file from the corpus
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 11 Feb 2024

Usage:
    time python ./mk_vocab.py --input ./corpus/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned --output ./corpus/vocab.txt

"""

import argparse

def create_vocab(input_file, output_file=None):
    unique_words = set()

    # Read the word-segmented text corpus file
    with open(input_file, 'r', encoding='utf-8') as f:
        for line in f:
            words = line.strip().split()
            unique_words.update(words)

    # Write the vocabulary list to the output file or print to stdout
    if output_file:
        with open(output_file, 'w', encoding='utf-8') as f:
            for word in sorted(unique_words):
                f.write(word + '\n')
        print(f"Vocabulary written to '{output_file}'")
    else:
        for word in sorted(unique_words):
            print(word)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Create a vocabulary list from a word-segmented text corpus file.")
    parser.add_argument("-i", "--input", required=True, help="Input word-segmented text corpus file")
    parser.add_argument("-o", "--output", help="Output file to save the vocabulary list (optional)")
    args = parser.parse_args()

    create_vocab(args.input, args.output)

```

## Closed Test Data Preparation

corpus ထဲကပဲ ကျပန်း ၁၀ကြောင်းဆွဲယူထားတာပါ။  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ cp ../corpus/test1.txt ./corpus/
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ head ./corpus/test1.txt
ကြိုးစား နေ ပါ တယ်
အားလုံး ညှစ် တယ်
လယ်ယာ လုပ်ငန်း ကို အဓိက လုပ်ကိုင် ပြီး မြန်မာ့ ဓလေ့ ဝါးဓနိ အိမ် များ အများစု စုဖွဲ့ တည်ရှိ နေ သည့် အေး ကျေးရွာ ၏ အဓိက ရေ အရင်းအမြစ် အဖြစ် စပါး ရေသွင်း စိုက်ပျိုး ရန် အတွက် နိုင်ငံတော် အစိုးရ က တူးမြောင်း တစ် ခု ဆောက်လုပ် ကာ ဧရာဝတီ မြစ် မှ ရေ ကို သွယ်ယူ ပေး ထား ပြီး ကျေးရွာလူထု သောက်သုံး ရန် ၊ ချက်ပြုတ် ရာ တွင် အသုံးပြု ရန် အတွက် မူ အဝီစိရေ သွယ်ယူ သည့် ပိုက် တစ် ခု သာ လျှင် ရှိ ပါ သည် ။
သူ ဟာ ဘေးဘျမ်း ကင်းကင်း နဲ့ ပြန်ရောက် လာ ခဲ့ တယ် လေ ။
အခု ချိန် မှာ ထိုင်ဝမ် က နေ ဗြိတိန် ကို တိုက်ရိုက် လေယာဉ် မ ရှိ ဘူး ။ ခင်ဗျား ဟောင်ကောင် က နေ တဆင့် သွား ရ မယ် ။
သူ့ ဘာသာ သူ ပြော ချင် ရာ ပြော ပြီး သူ့ ဘက် အဖော် လှည့် ညှိ သေး ၏ ။
အန်ကယ် မနက် စောစော ထ ပြီး ပုံမှန် လမ်းလျှောက် ပေး ပါ လား ။
ဒီလို လေး ပဲ အမြဲ ထာဝရ မြင် ချင် ပါ တယ် ခန့်စည်သူ ကို မ တွေ့ မိ ပါ လား နိုင်ငံတော် ကို ဖား ( အဲ လေ ) နိုင်ငံတော် အကျိုးပြု ဇာတ်ကား တွေ ရိုက် နေ ကျ အနုပညာရှင် တွေ က ရှေ့ ဆုံး တန်း မှာ ကွ ။
ကျွန်တော့် ကို ပိုက်ဆံ နည်းနည်း ချေး မလား ။
သူ က လူရင်း ပါ ။
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## Write Python Code for LM Evaluation

(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ cat evaluate_lm.py  

```python
"""

Evaluation on ngram LM with test file.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 11 Feb 2024

Usage:
time python ./evaluate_lm.py --language_model ./model/5gram.arpa \
--vocab_file ./corpus/vocab.txt --test_data ./corpus/test1.txt --perplexity

time python ./evaluate_lm.py --language_model ./model/5gram.arpa \
--vocab_file ./corpus/vocab.txt --test_data ./corpus/test1.txt --perplexity

"""

import argparse
import kenlm

def load_vocab(vocab_file):
    vocab = set()
    with open(vocab_file, 'r', encoding='utf-8') as f:
        for line in f:
            word = line.strip()
            vocab.add(word)

    # Check if <s> and </s> are not present in the vocabulary, then add them
    if '<s>' not in vocab:
        vocab.add('<s>')
    if '</s>' not in vocab:
        vocab.add('</s>')

    return vocab

def evaluate_language_model(lm_path, vocab_path, test_data_path, calculate_perplexity):
    model = kenlm.LanguageModel(lm_path)
    vocab = load_vocab(vocab_path)

    num_sentences = 0
    num_words = 0
    total_logprob = 0
    total_oov = 0

    with open(test_data_path, 'r', encoding='utf-8') as f:
        for line in f:
            sentence = line.strip()

            # Prepend <s> and append </s> to the sentence
            sentence = '<s> ' + sentence + ' </s>'

            num_sentences += 1

            # Get OOV words in the sentence
            oov_words = [word for word in sentence.split() if word not in vocab]
            oov_count = len(oov_words)
            total_oov += oov_count

            num_words += len(sentence.split())

            logprob = model.score(sentence)
            total_logprob += logprob

            print(f'Sentence: {sentence}')
            print(f'Log Probability Score: {logprob}')
            print(f'OOV Words: {", ".join(oov_words)}')
            print(f'Number of OOV words: {oov_count}')

            # Generate suggestions for the next word
            if not calculate_perplexity:
                words = sentence.split()
                prefix = ' '.join(words[:-1])
                suggestions = [(model.score(prefix + ' ' + next_word), next_word) for next_word in vocab]
                suggestions.sort(reverse=True)

                print("Next word suggestions:")
                for score, word in suggestions[:5]:
                    print(f'\t{word}\tScore: {score}')

                print()

    if calculate_perplexity:
        print(f"\n{num_sentences} sentences, {num_words} words")
        print(f"logprob= {total_logprob}")

    print(f"Total number of OOV words: {total_oov}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Evaluate a language model.")
    parser.add_argument("-l", "--language_model", required=True, help="Path to the KenLM language model file")
    parser.add_argument("-v", "--vocab_file", required=True, help="Path to the vocabulary file")
    parser.add_argument("-t", "--test_data", required=True, help="Path to the test data file")
    parser.add_argument("-p", "--perplexity", action="store_true", help="Calculate perplexity")
    args = parser.parse_args()

    evaluate_language_model(args.language_model, args.vocab_file, args.test_data, args.perplexity)

```

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ python ./evaluate_lm.py --help
usage: evaluate_lm.py [-h] -l LANGUAGE_MODEL -v VOCAB_FILE -t TEST_DATA [-p]

Evaluate a language model.

optional arguments:
  -h, --help            show this help message and exit
  -l LANGUAGE_MODEL, --language_model LANGUAGE_MODEL
                        Path to the KenLM language model file
  -v VOCAB_FILE, --vocab_file VOCAB_FILE
                        Path to the vocabulary file
  -t TEST_DATA, --test_data TEST_DATA
                        Path to the test data file
  -p, --perplexity      Calculate perplexity
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## Confirmation of "\<s\>" and "\<\/s\>" Tags

```
(base) yekyaw.thu@gpu:~/exp/lm/kenlm/model$ grep -E "\<s\>|\<\/s\>" ./5gram.arpa | head -n 30
0       <s>     -1.1136011
-2.0540004      </s>    0
-2.598232       <s> </s>        0
-1.9679106      ကြိုးစား </s>   0
-2.514302       နေ </s> 0
-1.2094808      ပါ </s> 0
-1.1553888      တယ် </s>        0
-2.1345441      အားလုံး </s>    0
-1.8800373      ညှစ် </s>       0
-2.327113       လယ်ယာ </s>      0
-1.8913853      လုပ်ငန်း </s>   0
-2.4015002      ကို </s>        0
-2.101151       အဓိက </s>       0
-2.2684805      ပြီး </s>       0
-2.5052533      မြန်မာ့ </s>    0
-1.9871839      ဓလေ့ </s>       0
-2.3923814      အိမ် </s>       0
-2.0189044      များ </s>       0
-2.5034368      အများစု </s>    0
-2.3004208      သည့် </s>       0
-1.8819267      အေး </s>        0
-2.2012866      ကျေးရွာ </s>    0
-1.3313514      ၏ </s>  0
-1.4686385      ရေ </s> 0
-2.3824224      အဖြစ် </s>      0
-2.032643       စပါး </s>       0
-2.0160484      ရန် </s>        0
-2.1435182      အတွက် </s>      0
-2.498015       နိုင်ငံတော် </s>        0
-1.9355946      အစိုးရ </s>     0
(base) yekyaw.thu@gpu:~/exp/lm/kenlm/model$
```

## Evaluation 5gram LM with 10 Lines of Test File

Evaluation with --perplexity command line argument:  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./evaluate_lm.py --language_model ./model/5gram.arpa --vocab_file ./corpus/vocab.txt --test_data ./corpus/test1.txt --perplexity
Loading the LM will be faster if you build a binary file.
Reading /home/yekyaw.thu/exp/lm/kenlm/model/5gram.arpa
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Sentence: <s> ကြိုးစား နေ ပါ တယ် </s>
Log Probability Score: -8.356277465820312
OOV Words:
Number of OOV words: 0
Sentence: <s> အားလုံး ညှစ် တယ် </s>
Log Probability Score: -9.53565788269043
OOV Words:
Number of OOV words: 0
Sentence: <s> လယ်ယာ လုပ်ငန်း ကို အဓိက လုပ်ကိုင် ပြီး မြန်မာ့ ဓလေ့ ဝါးဓနိ အိမ် များ အများစု စုဖွဲ့ တည်ရှိ နေ သည့် အေး ကျေးရွာ ၏ အဓိက ရေ အရင်းအမြစ် အဖြစ် စပါး ရေသွင်း စိုက်ပျိုး ရန် အတွက် နိုင်ငံတော် အစိုးရ က တူးမြောင်း တစ် ခု ဆောက်လုပ် ကာ ဧရာဝတီ မြစ် မှ ရေ ကို သွယ်ယူ ပေး ထား ပြီး ကျေးရွာလူထု သောက်သုံး ရန် ၊ ချက်ပြုတ် ရာ တွင် အသုံးပြု ရန် အတွက် မူ အဝီစိရေ သွယ်ယူ သည့် ပိုက် တစ် ခု သာ လျှင် ရှိ ပါ သည် ။ </s>
Log Probability Score: -65.08269500732422
OOV Words: ၊, ။
Number of OOV words: 2
Sentence: <s> သူ ဟာ ဘေးဘျမ်း ကင်းကင်း နဲ့ ပြန်ရောက် လာ ခဲ့ တယ် လေ ။ </s>
Log Probability Score: -20.666202545166016
OOV Words: ။
Number of OOV words: 1
Sentence: <s> အခု ချိန် မှာ ထိုင်ဝမ် က နေ ဗြိတိန် ကို တိုက်ရိုက် လေယာဉ် မ ရှိ ဘူး ။ ခင်ဗျား ဟောင်ကောင် က နေ တဆင့် သွား ရ မယ် ။ </s>
Log Probability Score: -41.217063903808594
OOV Words: ။, ။
Number of OOV words: 2
Sentence: <s> သူ့ ဘာသာ သူ ပြော ချင် ရာ ပြော ပြီး သူ့ ဘက် အဖော် လှည့် ညှိ သေး ၏ ။ </s>
Log Probability Score: -25.022071838378906
OOV Words: ။
Number of OOV words: 1
Sentence: <s> အန်ကယ် မနက် စောစော ထ ပြီး ပုံမှန် လမ်းလျှောက် ပေး ပါ လား ။ </s>
Log Probability Score: -23.394229888916016
OOV Words: ။
Number of OOV words: 1
Sentence: <s> ဒီလို လေး ပဲ အမြဲ ထာဝရ မြင် ချင် ပါ တယ် ခန့်စည်သူ ကို မ တွေ့ မိ ပါ လား နိုင်ငံတော် ကို ဖား ( အဲ လေ ) နိုင်ငံတော် အကျိုးပြု ဇာတ်ကား တွေ ရိုက် နေ ကျ အနုပညာရှင် တွေ က ရှေ့ ဆုံး တန်း မှာ ကွ ။ </s>
Log Probability Score: -62.0733528137207
OOV Words: (, ), ။
Number of OOV words: 3
Sentence: <s> ကျွန်တော့် ကို ပိုက်ဆံ နည်းနည်း ချေး မလား ။ </s>
Log Probability Score: -19.40286636352539
OOV Words: ။
Number of OOV words: 1
Sentence: <s> သူ က လူရင်း ပါ ။ </s>
Log Probability Score: -19.079509735107422
OOV Words: ။
Number of OOV words: 1

10 sentences, 207 words
logprob= -293.829927444458
Total number of OOV words: 12

real    0m6.527s
user    0m6.270s
sys     0m0.252s
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

Evaluation without --perplexity command line argument:  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./evaluate_lm.py --language_model ./model/5gram.arpa --vocab_file ./corpus/vocab.txt --test_data ./corpus/test1.txt
Loading the LM will be faster if you build a binary file.
Reading /home/yekyaw.thu/exp/lm/kenlm/model/5gram.arpa
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Sentence: <s> ကြိုးစား နေ ပါ တယ် </s>
Log Probability Score: -8.356277465820312
OOV Words:
Number of OOV words: 0
Next word suggestions:
        ခင်ဗျာ  Score: -7.6588358879089355
        ရှင်    Score: -7.86376953125
        </s>    Score: -8.356277465820312
        ဘုရား   Score: -8.382424354553223
        ရှင့်   Score: -8.456396102905273

Sentence: <s> အားလုံး ညှစ် တယ် </s>
Log Probability Score: -9.53565788269043
OOV Words:
Number of OOV words: 0
Next word suggestions:
        </s>    Score: -9.53565788269043
        တဲ့     Score: -10.213935852050781
        လေ      Score: -10.232338905334473
        နော်    Score: -10.288532257080078
        ပေါ့    Score: -10.30185317993164

Sentence: <s> လယ်ယာ လုပ်ငန်း ကို အဓိက လုပ်ကိုင် ပြီး မြန်မာ့ ဓလေ့ ဝါးဓနိ အိမ် များ အများစု စုဖွဲ့ တည်ရှိ နေ သည့် အေး ကျေးရွာ ၏ အဓိက ရေ အရင်းအမြစ် အဖြစ် စပါး ရေသွင်း စိုက်ပျိုး ရန် အတွက် နိုင်ငံတော် အစိုးရ က တူးမြောင်း တစ် ခု ဆောက်လုပ် ကာ ဧရာဝတီ မြစ် မှ ရေ ကို သွယ်ယူ ပေး ထား ပြီး ကျေးရွာလူထု သောက်သုံး ရန် ၊ ချက်ပြုတ် ရာ တွင် အသုံးပြု ရန် အတွက် မူ အဝီစိရေ သွယ်ယူ သည့် ပိုက် တစ် ခု သာ လျှင် ရှိ ပါ သည် ။ </s>
Log Probability Score: -65.08269500732422
OOV Words: ၊, ။
Number of OOV words: 2
Next word suggestions:
        <s>     Score: -63.57292938232422
        သည်     Score: -64.43460845947266
        ပါ      Score: -64.46748352050781
        တယ်     Score: -64.73475646972656
        ၏       Score: -64.78410339355469

Sentence: <s> သူ ဟာ ဘေးဘျမ်း ကင်းကင်း နဲ့ ပြန်ရောက် လာ ခဲ့ တယ် လေ ။ </s>
Log Probability Score: -20.666202545166016
OOV Words: ။
Number of OOV words: 1
Next word suggestions:
        <s>     Score: -19.15643310546875
        သည်     Score: -20.018110275268555
        ပါ      Score: -20.050981521606445
        တယ်     Score: -20.318260192871094
        ၏       Score: -20.367610931396484

Sentence: <s> အခု ချိန် မှာ ထိုင်ဝမ် က နေ ဗြိတိန် ကို တိုက်ရိုက် လေယာဉ် မ ရှိ ဘူး ။ ခင်ဗျား ဟောင်ကောင် က နေ တဆင့် သွား ရ မယ် ။ </s>
Log Probability Score: -41.217063903808594
OOV Words: ။, ။
Number of OOV words: 2
Next word suggestions:
        <s>     Score: -39.70729446411133
        သည်     Score: -40.568973541259766
        ပါ      Score: -40.601844787597656
        တယ်     Score: -40.86912155151367
        ၏       Score: -40.91847229003906

Sentence: <s> သူ့ ဘာသာ သူ ပြော ချင် ရာ ပြော ပြီး သူ့ ဘက် အဖော် လှည့် ညှိ သေး ၏ ။ </s>
Log Probability Score: -25.022071838378906
OOV Words: ။
Number of OOV words: 1
Next word suggestions:
        <s>     Score: -23.51230239868164
        သည်     Score: -24.373979568481445
        ပါ      Score: -24.406850814819336
        တယ်     Score: -24.674129486083984
        ၏       Score: -24.723480224609375

Sentence: <s> အန်ကယ် မနက် စောစော ထ ပြီး ပုံမှန် လမ်းလျှောက် ပေး ပါ လား ။ </s>
Log Probability Score: -23.394229888916016
OOV Words: ။
Number of OOV words: 1
Next word suggestions:
        <s>     Score: -21.88446044921875
        သည်     Score: -22.746137619018555
        ပါ      Score: -22.779008865356445
        တယ်     Score: -23.046287536621094
        ၏       Score: -23.095638275146484

Sentence: <s> ဒီလို လေး ပဲ အမြဲ ထာဝရ မြင် ချင် ပါ တယ် ခန့်စည်သူ ကို မ တွေ့ မိ ပါ လား နိုင်ငံတော် ကို ဖား ( အဲ လေ ) နိုင်ငံတော် အကျိုးပြု ဇာတ်ကား တွေ ရိုက် နေ ကျ အနုပညာရှင် တွေ က ရှေ့ ဆုံး တန်း မှာ ကွ ။ </s>
Log Probability Score: -62.0733528137207
OOV Words: (, ), ။
Number of OOV words: 3
Next word suggestions:
        <s>     Score: -60.56358337402344
        သည်     Score: -61.425262451171875
        ပါ      Score: -61.458133697509766
        တယ်     Score: -61.72541046142578
        ၏       Score: -61.77476119995117

Sentence: <s> ကျွန်တော့် ကို ပိုက်ဆံ နည်းနည်း ချေး မလား ။ </s>
Log Probability Score: -19.40286636352539
OOV Words: ။
Number of OOV words: 1
Next word suggestions:
        <s>     Score: -17.893096923828125
        သည်     Score: -18.75477409362793
        ပါ      Score: -18.78764533996582
        တယ်     Score: -19.05492401123047
        ၏       Score: -19.10427474975586

Sentence: <s> သူ က လူရင်း ပါ ။ </s>
Log Probability Score: -19.079509735107422
OOV Words: ။
Number of OOV words: 1
Next word suggestions:
        <s>     Score: -17.569740295410156
        သည်     Score: -18.43141746520996
        ပါ      Score: -18.46428871154785
        တယ်     Score: -18.7315673828125
        ၏       Score: -18.78091812133789

Total number of OOV words: 12

real    0m9.885s
user    0m9.642s
sys     0m0.236s
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

## ## Evaluation 5gram LM with BBC Article

Note: ဒီ test ဖိုင်က word segmentation မလုပ်ထားပဲ BBC article ကို ဒီအတိုင်းပဲ ယူထားတာ ဖြစ်လို့ PPL တန်ဖိုးက အထက်က test1.txt ဖိုင်နဲ့ ယှဉ်လိုက်ရင် ကြီးကို ကြီးရမယ်။  
ပြီးတော့ OOV value ကလည်း များကို များရမယ်။ ရေးထားတဲ့ python code မှာ အမှားမပါအောင် confirmation လုပ်တာလည်း ပါပါတယ်။  

ပြီးတော့ တခုမြင်စေချင်တာက blank line တွေမရှင်းထားရင်၊ ပြီးတော့ data cleaning မလုပ်ထားရင် အဲဒါတွေကလည်း evaluaiton မှာပါ သက်ရောက်တာကိုပါ။  
<s> </s> လိုင်းကိစ္စတွေ၊ ZWNJ စတာတွေကိုလည်း evaluation output မှာပါလာတာတွေကိုလေ့လာပါ။  

running with --perplexity option result:  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./evaluate_lm.py --language_model ./model/5gram.arpa --vocab_file ./corpus/vocab.txt --test_data ./corpus/bbc_article1.txt --perplex
ity
Loading the LM will be faster if you build a binary file.
Reading /home/yekyaw.thu/exp/lm/kenlm/model/5gram.arpa
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Sentence: <s> ရောဂါ X တကမ္ဘာလုံး ပြန့်လာရင် ဘယ်လို လုပ်ကြမလဲ </s>
Log Probability Score: -37.36429977416992
OOV Words: X, ပြန့်လာရင်, လုပ်ကြမလဲ
Number of OOV words: 3
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ၂၃ ဇန်နဝါရီ ၂၀၂၄ </s>
Log Probability Score: -23.485849380493164
OOV Words: ၂၃, ၂၀၂၄
Number of OOV words: 2
Sentence: <s> အသစ်တင်ချိန် ၂၇ ဇန်နဝါရီ ၂၀၂၄ </s>
Log Probability Score: -29.58599090576172
OOV Words: အသစ်တင်ချိန်, ၂၇, ၂၀၂၄
Number of OOV words: 3
Sentence: <s> ဆွစ်ဇာလန်နိုင်ငံ ဒါးဗို့စ်က ကမ္ဘာ့စီးပွားရေး ဖိုရမ်မှာ ကျန်းမာရေး ကဏ္ဍဆိုင်ရာ ခေါင်းဆောင်တွေဟာ နောက်ထပ် တကမ္ဘာလုံး ပျံ့နှံ့ဖြစ်ပွားနိုင်တဲ့ ရောဂါတခု ဖြစ်လာရင် လုပ်ရမှာ တွေကို ကြိုတင်ပြင်ဆင် စီစဉ်ထားဖို့ က အရေးကြီးကြောင်း ဆွေးနွေးခဲ့ကြပါတယ်။ ပညာရှင်တွေကတော့ ဒီမသိသေးတဲ့ ရောဂါကို “ရောဂါ အိတ်စ်” (Disease X) လို့ နာမည်ပေးထားပါတယ်။ </s>
Log Probability Score: -165.9970703125
OOV Words: ဆွစ်ဇာလန်နိုင်ငံ, ဒါးဗို့စ်က, ကမ္ဘာ့စီးပွားရေး, ဖိုရမ်မှာ, ကဏ္ဍဆိုင်ရာ, ခေါင်းဆောင်တွေဟာ, ပျံ့နှံ့ဖြစ်ပွားနိုင်တဲ့, ရောဂါတခု, ဖြစ်လာရင်, ကြိုတင်ပြင်ဆင်, စီစဉ်ထားဖို့, အရေးကြီးကြောင်း, ဆွေးနွေးခဲ့ကြပါတယ်။, ပညာရှင်တွေကတော့, ဒီမသိသေးတဲ့, ရောဂါကို, “ရောဂါ, အိတ်စ်”, (Disease, X), နာမည်ပေးထားပါတယ်။
Number of OOV words: 21
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကိုဗစ်-၁၉ တကမ္ဘာလုံးကို ပျံ့နှံ့ခဲ့တဲ့အချိန်တုန်းကလို ကျန်းမာရေး စနစ်တွေက မထိန်းချုပ် နိုင်ခဲ့တာ၊ စီးပွားရေးပိုင်းမှာ ဒေါ်လာ ထရီလျံနဲ့ချီပြီး ရှုံးခဲ့ကြတာ စတာတွေ အပါအဝင် အားလုံးမြင်လိုက်ရတဲ့ အဆုံးအရှုံးတွေ လျှော့ချနိုင်အောင် ကြိုတင် ပြင်ဆင်ထားဖို့က အရေးကြီးကြောင်း ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ (WHO) က အရင်ကာလတွေကတည်းက သတိပေးထားပါတယ်။ </s>
Log Probability Score: -142.34747314453125
OOV Words: ကိုဗစ်-၁၉, တကမ္ဘာလုံးကို, ပျံ့နှံ့ခဲ့တဲ့အချိန်တုန်းကလို, စနစ်တွေက, မထိန်းချုပ်, နိုင်ခဲ့တာ၊, စီးပွားရေးပိုင်းမှာ, ထရီလျံနဲ့ချီပြီး, ရှုံးခဲ့ကြတာ, အားလုံးမြင်လိုက်ရတဲ့, အဆုံးအရှုံးတွေ, လျှော့ချနိုင်အောင်, ပြင်ဆင်ထားဖို့က, အရေးကြီးကြောင်း, ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, (WHO), အရင်ကာလတွေကတည်းက, သတိပေးထားပါတယ်။
Number of OOV words: 18
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ရောဂါ အိတ်စ် (Disease X) ဆိုတာ ဘာလဲ </s>
Log Probability Score: -35.69732666015625
OOV Words: အိတ်စ်, (Disease, X)
Number of OOV words: 3
Sentence: <s> ဒါက တကယ့်ရောဂါ မဟုတ်သေးသလို ဒီနာမည်နဲ့ ရောဂါဆိုတာလည်းမရှိသေးပါဘူး။ </s>
Log Probability Score: -34.029563903808594
OOV Words: တကယ့်ရောဂါ, မဟုတ်သေးသလို, ဒီနာမည်နဲ့, ရောဂါဆိုတာလည်းမရှိသေးပါဘူး။
Number of OOV words: 4
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ဒါက အခုလက်ရှိထိ မပေါ်ပေါက်သေးပေမဲ့ ကူးစက်ပျံ့နှံ့နိုင်တဲ့ ဒါမှမဟုတ် နိုင်ငံတွေ၊ တိုက်ကြီးတွေကို ပျံ့နှံ့သွားပြီး ကမ္ဘာ့ကပ်ရောဂါအထိ ဖြစ်သွားနိုင်တဲ့ ကူးစက်ရောဂါတခုကို ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ က သတ်မှတ်ခေါ်ဝေါ်တဲ့ အသုံးအနှုန်း တခုပါ။ </s>
Log Probability Score: -94.48975372314453
OOV Words: အခုလက်ရှိထိ, မပေါ်ပေါက်သေးပေမဲ့, ကူးစက်ပျံ့နှံ့နိုင်တဲ့, နိုင်ငံတွေ၊, တိုက်ကြီးတွေကို, ပျံ့နှံ့သွားပြီး, ကမ္ဘာ့ကပ်ရောဂါအထိ, ဖြစ်သွားနိုင်တဲ့, ကူးစက်ရောဂါတခုကို, ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, သတ်မှတ်ခေါ်ဝေါ်တဲ့, တခုပါ။
Number of OOV words: 12
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကိုဗစ်-၁၉ ကမ္ဘာ့ရောဂါကပ်မတိုင်မီကတည်းက ဒီအသုံးအနှုန်းက ရှိခဲ့ပါတယ်။ ၂၀၁၈ ခုနှစ် ဖေဖော်ဝါရီမှာ WHO က ထုတ်ပြန်တဲ့ ဦးစားပေးစောင့်ကြည့်ရမယ့် ရောဂါစာရင်းထဲမှာ ရောဂါ အိတ်စ် လည်း ပါဝင်ပါတယ်။ </s>
Log Probability Score: -93.749755859375
OOV Words: ကိုဗစ်-၁၉, ကမ္ဘာ့ရောဂါကပ်မတိုင်မီကတည်းက, ဒီအသုံးအနှုန်းက, ရှိခဲ့ပါတယ်။, ၂၀၁၈, ဖေဖော်ဝါရီမှာ, WHO, ထုတ်ပြန်တဲ့, ဦးစားပေးစောင့်ကြည့်ရမယ့်, ရောဂါစာရင်းထဲမှာ, အိတ်စ်, ပါဝင်ပါတယ်။
Number of OOV words: 12
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ က ကမကထပြုမှုနဲ့ ကျွမ်းကျင်သူတွေ စုပေါင်းကာ ရေးဆွဲ ထားတဲ့ စီမံချက်ဟာ ကမ္ဘာလုံးဆိုင်ရာ ဗျူဟာဖြစ်ပြီး အဲဒီထဲမှာ ကပ်ရောဂါ ပျံ့နှံ့ လာချိန်အတွင်း သုတေသနနဲ့ ထုတ်လုပ်မှု လုပ်ငန်းတွေ မြန်မြန်ဆန်ဆန် လုပ်ဆောင်နိုင်‌အောင် ပြင်ဆင်ထားတဲ့ အစီအစဉ်တွေ ပါဝင်ပါတယ်။ </s>
Log Probability Score: -131.4842071533203
OOV Words: ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, ကမကထပြုမှုနဲ့, ကျွမ်းကျင်သူတွေ, စုပေါင်းကာ, စီမံချက်ဟာ, ကမ္ဘာလုံးဆိုင်ရာ, ဗျူဟာဖြစ်ပြီး, အဲဒီထဲမှာ, လာချိန်အတွင်း, သုတေသနနဲ့, ထုတ်လုပ်မှု, လုပ်ငန်းတွေ, လုပ်ဆောင်နိုင်‌အောင်, ပါဝင်ပါတယ်။
Number of OOV words: 14
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ဒီအစီအစဉ်တွေဟာ ရောဂါပိုးရှိမရှိ သိဖို့လုပ်တဲ့ ဆေးစစ်မှုတွေ၊ ကာကွယ်ဆေးတွေ၊ ကုသမှုဆေးဝါးတွေကို စွမ်းဆောင်ရည်ရှိရှိနဲ့ ခပ်မြန်မြန်လုပ်ဆောင်နိုင်ပြီး လူတွေရဲ့ အသက်ကို ကယ်နိုင်ဖို့၊ အကျပ်အတည်း အကြီးအမားဆိုက်မှာကို ရှောင်ရှားနိုင်ဖို့ စတာ တွေ အတွက် ရည်ရွယ်တာပါ။ </s>
Log Probability Score: -104.09574127197266
OOV Words: ဒီအစီအစဉ်တွေဟာ, ရောဂါပိုးရှိမရှိ, သိဖို့လုပ်တဲ့, ဆေးစစ်မှုတွေ၊, ကာကွယ်ဆေးတွေ၊, ကုသမှုဆေးဝါးတွေကို, စွမ်းဆောင်ရည်ရှိရှိနဲ့, ခပ်မြန်မြန်လုပ်ဆောင်နိုင်ပြီး, လူတွေရဲ့, ကယ်နိုင်ဖို့၊, အကြီးအမားဆိုက်မှာကို, ရှောင်ရှားနိုင်ဖို့, ရည်ရွယ်တာပါ။
Number of OOV words: 13
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ပြီးခဲ့တဲ့နှစ်ပိုင်းတွေအတွင်း ဥပမာ - ဆားစ် ရောဂါ (Sars - Severe Acute Respiratory Syndrome)၊ ဝက်တုပ်ကွေး (Swine flu) ၊ မားစ် (Mers - Middle East Respiratory Syndrome), အီဘိုလာ ရောဂါ (Ebola)၊ ကိုဗစ်-၁၉ စတဲ့ရောဂါတွေ ကမ္ဘာမှာ ပျံ့နှံ့ ကူးစက်ခဲ့ပါတယ်။ </s>
Log Probability Score: -181.41049194335938
OOV Words: ပြီးခဲ့တဲ့နှစ်ပိုင်းတွေအတွင်း, -, ဆားစ်, (Sars, -, Severe, Acute, Respiratory, Syndrome)၊, ဝက်တုပ်ကွေး, (Swine, flu), ၊, (Mers, -, Middle, East, Respiratory, Syndrome),, (Ebola)၊, ကိုဗစ်-၁၉, စတဲ့ရောဂါတွေ, ကမ္ဘာမှာ, ကူးစက်ခဲ့ပါတယ်။
Number of OOV words: 24
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> နောက်ထပ် ကမ္ဘာကပ်တခု ရောက်လာနိုင်တာ နဲ့ အဲဒီရောဂါဟာ ကိုဗစ်-၁၉ ကို ဖြစ်စေတဲ့ ကိုရိုနာဗိုင်းရပ်စ်ထက် ဆိုးဝါးနိုင်တယ်ဆိုတာကို ကျန်းမာရေး ပညာရှင်တွေက စိုးရိမ် ထိတ်လန့်နေပါတယ်။ </s>
Log Probability Score: -78.83583068847656
OOV Words: ကမ္ဘာကပ်တခု, ရောက်လာနိုင်တာ, အဲဒီရောဂါဟာ, ကိုဗစ်-၁၉, ဖြစ်စေတဲ့, ကိုရိုနာဗိုင်းရပ်စ်ထက်, ဆိုးဝါးနိုင်တယ်ဆိုတာကို, ပညာရှင်တွေက, ထိတ်လန့်နေပါတယ်။
Number of OOV words: 9
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ရောဂါ အိတ်စ် က ကမ္ဘာ့ကပ်တခု ဖြစ်လာမလား </s>
Log Probability Score: -30.80592918395996
OOV Words: အိတ်စ်, ကမ္ဘာ့ကပ်တခု, ဖြစ်လာမလား
Number of OOV words: 3
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ရောဂါ အိတ်စ်က လောလောဆယ်မှာ မပေါ်ထွန်းသေးပေမယ့် သုတေသီတွေ၊ သိပ္ပံပညာရှင်တွေ၊ ကျွမ်းကျင်သူတွေက ဒီလို ဗိုင်းရပ်စ် မျိုးပေါ်လာရင် တုံ့ပြန် ဆောင်ရွက်နိုင်ဖို့ အစီအစဉ် နဲ့ အဲဒီ ကမ္ဘာ့ကပ်ကို ရင်ဆိုင်နိုင်ဖို့အရေး ကျန်းမာရေးစနစ်ကို ဘယ်လို စီစဉ်ထားရမလဲဆိုတာတွေကို ကြိုကြိုတင်တင် လုပ်ဆောင်ထားနိုင်ဖို့ မျှော်လင့် နေပါတယ်။ </s>
Log Probability Score: -131.12477111816406
OOV Words: အိတ်စ်က, လောလောဆယ်မှာ, မပေါ်ထွန်းသေးပေမယ့်, သုတေသီတွေ၊, သိပ္ပံပညာရှင်တွေ၊, ကျွမ်းကျင်သူတွေက, မျိုးပေါ်လာရင်, ဆောင်ရွက်နိုင်ဖို့, ကမ္ဘာ့ကပ်ကို, ရင်ဆိုင်နိုင်ဖို့အရေး, ကျန်းမာရေးစနစ်ကို, စီစဉ်ထားရမလဲဆိုတာတွေကို, လုပ်ဆောင်ထားနိုင်ဖို့, နေပါတယ်။
Number of OOV words: 14
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ပြီးခဲ့တဲ့ သီတင်းပတ်အတွင်းက ကမ္ဘာ့ စီးပွားရေးဖိုရမ်မှာ WHO အကြီးအကဲ ဒေါက်တာ တက်ဒရို့စ် ဆန်ဒါနွန် ဂက်ဘရီရီးဆပ်စ် ဦးဆောင်ခဲ့ပြီး “ရောဂါ အိတ်စ် အတွက် ပြင်ဆင်ခြင်း” လို့အမည်ရတဲ့ ကြားဖြတ်ဆွေးနွေးပွဲတခုကို ပြုလုပ်ခဲ့ကြကာ “ရှေ့မှာ ဖြစ်လာမယ့် စိန်ခေါ်မှု အများအပြားအတွက် ကျန်းမာရေး စနစ်တွေကို ပြင်ဆင်ဖို့ရာမှာ လိုအပ်တဲ့ အားထုတ်ဆောင်ရွက်မှု” တွေကို ဆွေးနွေးခဲ့ကြပါတယ်။ </s>
Log Probability Score: -172.65003967285156
OOV Words: ပြီးခဲ့တဲ့, သီတင်းပတ်အတွင်းက, စီးပွားရေးဖိုရမ်မှာ, WHO, တက်ဒရို့စ်, ဆန်ဒါနွန်, ဂက်ဘရီရီးဆပ်စ်, ဦးဆောင်ခဲ့ပြီး, “ရောဂါ, အိတ်စ်, ပြင်ဆင်ခြင်း”, လို့အမည်ရတဲ့, ကြားဖြတ်ဆွေးနွေးပွဲတခုကို, ပြုလုပ်ခဲ့ကြကာ, “ရှေ့မှာ, ဖြစ်လာမယ့်, စိန်ခေါ်မှု, အများအပြားအတွက်, စနစ်တွေကို, ပြင်ဆင်ဖို့ရာမှာ, အားထုတ်ဆောင်ရွက်မှု”, ဆွေးနွေးခဲ့ကြပါတယ်။
Number of OOV words: 22
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> “ဒါက ကြောက်ရွံ့မှုတွေကို ဖြစ်သွားစေမယ်လို့ တချို့လူတွေက ပြောတာပေါ့” လို့ ဒေါက်တာ တက်ဒရို့စ်က ဆို ပါတယ်။ </s>
Log Probability Score: -58.95525360107422
OOV Words: “ဒါက, ကြောက်ရွံ့မှုတွေကို, ဖြစ်သွားစေမယ်လို့, တချို့လူတွေက, ပြောတာပေါ့”, တက်ဒရို့စ်က, ပါတယ်။
Number of OOV words: 7
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> “ဒီလို ကပ်မျိုးတွေ ဖြစ်လာမှာကို ကြိုတင်မှန်းထားတာက ပိုကောင်းတယ်၊ ဘာ့ကြောင့် လဲဆိုတော့ ကျွန်တော်တို့ သမိုင်းမှာ အကြိမ်များစွာ ဖြစ်ခဲ့ပြီးပြီလေ၊ ဒီတော့ အဲဒီအတွက် ကြိုတင်ပြင်ဆင်ထားဖို့လိုတယ်။” </s>
Log Probability Score: -90.61121368408203
OOV Words: “ဒီလို, ကပ်မျိုးတွေ, ဖြစ်လာမှာကို, ကြိုတင်မှန်းထားတာက, ပိုကောင်းတယ်၊, လဲဆိုတော့, ကျွန်တော်တို့, သမိုင်းမှာ, အကြိမ်များစွာ, ဖြစ်ခဲ့ပြီးပြီလေ၊, အဲဒီအတွက်, ကြိုတင်ပြင်ဆင်ထားဖို့လိုတယ်။”
Number of OOV words: 12
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကမ္ဘာက၊ လူအတော်များများက ကိုဗစ်-၁၉ ကပ်ကို အတော် အံ့အားသင့်ခဲ့ကြပါတယ်၊ ၂၀၂၁ မှာ BBC Future ဌာနက “ကမ္ဘာတလွှားကို ပျံ့နှံ့မယ့် ကပ်ဘေးတခုအတွက် ကျန်ုပ်တို့ ပြင်ဆင်ထားကြဖို့ ကူးစက်ရောဂါပျံ့နှံမှုနဲ့ ကာကွယ်ရေးဆိုင်ရာ ကျန်းမာရေးပညာရှင်တွေ၊ တခြားကျွမ်းကျင်သူတွေက သတိပေးနေတာ နှစ်အတော် ကြာကြာကတည်းကပါ” လို့ ရေးဖူးပါတယ်။ </s>
Log Probability Score: -150.66319274902344
OOV Words: ကမ္ဘာက၊, လူအတော်များများက, ကိုဗစ်-၁၉, ကပ်ကို, အံ့အားသင့်ခဲ့ကြပါတယ်၊, ၂၀၂၁, BBC, Future, ဌာနက, “ကမ္ဘာတလွှားကို, ပျံ့နှံ့မယ့်, ကပ်ဘေးတခုအတွက်, ကျန်ုပ်တို့, ပြင်ဆင်ထားကြဖို့, ကူးစက်ရောဂါပျံ့နှံမှုနဲ့, ကာကွယ်ရေးဆိုင်ရာ, ကျန်းမာရေးပညာရှင်တွေ၊, တခြားကျွမ်းကျင်သူတွေက, သတိပေးနေတာ, နှစ်အတော်, ကြာကြာကတည်းကပါ”, ရေးဖူးပါတယ်။
Number of OOV words: 22
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> အဲဒီကျွမ်းကျင်သူအများစုက တိရိစ္ဆာန်တွေဆီကနေ ကပ်ရောဂါ စတင်နိုင်တယ် ဆိုတာကို စိုးရိမ်ခဲ့ကြပါတယ်။ </s>
Log Probability Score: -41.254173278808594
OOV Words: အဲဒီကျွမ်းကျင်သူအများစုက, တိရိစ္ဆာန်တွေဆီကနေ, စတင်နိုင်တယ်, စိုးရိမ်ခဲ့ကြပါတယ်။
Number of OOV words: 4
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> တကယ်တော့ အသစ်ပေါ်လာတဲ့ ရောဂါတွေထဲက ၇၅% ဟာ ဇူးနော်တစ် (zoonotic) လို့ ခေါ်ကြတဲ့ တိရိစ္ဆာန်ကနေ လူတွေဆီကို ကူးစက်ပျံ့နှံ့လာတဲ့ ရောဂါတွေပါ။ </s>
Log Probability Score: -77.30233764648438
OOV Words: အသစ်ပေါ်လာတဲ့, ရောဂါတွေထဲက, ၇၅%, ဇူးနော်တစ်, (zoonotic), ခေါ်ကြတဲ့, တိရိစ္ဆာန်ကနေ, လူတွေဆီကို, ကူးစက်ပျံ့နှံ့လာတဲ့, ရောဂါတွေပါ။
Number of OOV words: 10
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> တရုတ်နိုင်ငံတွင်း တိရိစ္ဆာန်အရှင်တွေရောင်းတဲ့ စျေးတခုက လင်းနို့တွေဆီကနေ အစပြုလာတာလို့ ယူဆရတဲ့ ကိုဗစ်-၁၉ ရောဂါဟာလည်း ဒီလို ရောဂါမျိုးထဲက တခုပါ။ ဒါပေမဲ့ ကိုဗစ်-၁၉ လို ဇူးနော်တစ် ရောဂါဟာ လူတွေရဲ့ လုပ်ဆောင်မှုတွေကြောင့် ပိုပြီး အန္တရာယ်များသွားတယ်လို့ မှတ်ယူနိုင်ပါတယ်။ </s>
Log Probability Score: -126.19227600097656
OOV Words: တရုတ်နိုင်ငံတွင်း, တိရိစ္ဆာန်အရှင်တွေရောင်းတဲ့, စျေးတခုက, လင်းနို့တွေဆီကနေ, အစပြုလာတာလို့, ယူဆရတဲ့, ကိုဗစ်-၁၉, ရောဂါဟာလည်း, ရောဂါမျိုးထဲက, တခုပါ။, ကိုဗစ်-၁၉, ဇူးနော်တစ်, ရောဂါဟာ, လူတွေရဲ့, လုပ်ဆောင်မှုတွေကြောင့်, အန္တရာယ်များသွားတယ်လို့, မှတ်ယူနိုင်ပါတယ်။
Number of OOV words: 17
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ရာသီဥတုအပေါ် လူသားတွေရဲ့ သက်ရောက်မှုတွေ၊ သဘာဝတောရိုင်းနေရာတွေကို လူသားတွေက ဝင်ယူလာတာတွေ၊ ကမ္ဘာအနှံ့ကို လူတွေ ခရီးသွားကြတာတွေ၊ စတာတွေက တိရိစ္ဆာန်ကြောင့် စဖြစ်လာတဲ့ ရောဂါကို ပိုပျံ့နှံ့စေပါတယ်။ </s>
Log Probability Score: -90.70189666748047
OOV Words: ရာသီဥတုအပေါ်, လူသားတွေရဲ့, သက်ရောက်မှုတွေ၊, သဘာဝတောရိုင်းနေရာတွေကို, လူသားတွေက, ဝင်ယူလာတာတွေ၊, ကမ္ဘာအနှံ့ကို, ခရီးသွားကြတာတွေ၊, စတာတွေက, တိရိစ္ဆာန်ကြောင့်, စဖြစ်လာတဲ့, ရောဂါကို, ပိုပျံ့နှံ့စေပါတယ်။
Number of OOV words: 13
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> နောင်လာမယ့် ကမ္ဘာ့ကပ်အတွက် ကမ္ဘာက ဘယ်လို ပြင်ဆင်ထားနေလဲ </s>
Log Probability Score: -34.48929977416992
OOV Words: နောင်လာမယ့်, ကမ္ဘာ့ကပ်အတွက်, ကမ္ဘာက, ပြင်ဆင်ထားနေလဲ
Number of OOV words: 4
Sentence: <s> နောက်ထပ် ကမ္ဘာ့ကပ်အတွက် ရည်ရွယ်ပြင်ဆင်ထားတဲ့ လုပ်ဆောင်မှုတွေကို WHO အနေနဲ့ စပြီး အကောင်အထည်ဖော် လုပ်ဆောင်နေပြီလို့ ကမ္ဘာ့စီးပွားရေး ဖိုရမ်က ကြားဖြတ် ဆွေးနွေးပွဲမှာ ဒေါက်တာ တက်ဒရို့စ်က ပြောပါတယ်။ </s>
Log Probability Score: -92.91385650634766
OOV Words: ကမ္ဘာ့ကပ်အတွက်, ရည်ရွယ်ပြင်ဆင်ထားတဲ့, လုပ်ဆောင်မှုတွေကို, WHO, လုပ်ဆောင်နေပြီလို့, ကမ္ဘာ့စီးပွားရေး, ဖိုရမ်က, ဆွေးနွေးပွဲမှာ, တက်ဒရို့စ်က, ပြောပါတယ်။
Number of OOV words: 10
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> အဲဒီလုပ်ဆောင်မှုတွေထဲမှာ ကမ္ဘာ့ကပ် ရန်ပုံငွေတခုနဲ့ တောင်အာဖရိကမှာ “နည်းပညာ လွှဲပြောင်းပေးတဲ့ ဆုံရပ်ဌာန” တခုတို့ ပါဝင်ပြီး အဲဒါတွေက ကာကွယ်ဆေးတွေ ဒေသတွင်းမှာ ထုတ်လုပ်နိုင်မှာ ဖြစ်သလို ဝင်ငွေမြင့်တဲ့ နိုင်ငံတွေနဲ့ ဝင်ငွေနည်းတဲ့ နိုင်ငံတွေအကြား ကာကွယ်ဆေး လက်လှမ်းမီနိုင်မှု ကွာဟချက်တွေကို ကျော်လွှား နိုင်ရေးမှာ အထောက်အကူ ဖြစ်လာမှာပါ။ </s>
Log Probability Score: -156.616943359375
OOV Words: အဲဒီလုပ်ဆောင်မှုတွေထဲမှာ, ကမ္ဘာ့ကပ်, ရန်ပုံငွေတခုနဲ့, တောင်အာဖရိကမှာ, “နည်းပညာ, လွှဲပြောင်းပေးတဲ့, ဆုံရပ်ဌာန”, တခုတို့, ပါဝင်ပြီး, အဲဒါတွေက, ကာကွယ်ဆေးတွေ, ဒေသတွင်းမှာ, ထုတ်လုပ်နိုင်မှာ, ဝင်ငွေမြင့်တဲ့, နိုင်ငံတွေနဲ့, ဝင်ငွေနည်းတဲ့, နိုင်ငံတွေအကြား, လက်လှမ်းမီနိုင်မှု, ကွာဟချက်တွေကို, နိုင်ရေးမှာ, ဖြစ်လာမှာပါ။
Number of OOV words: 21
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကပ်ရောဂါတခုအတွက် နောက်ထပ် စနစ်အသစ်တွေ လုပ်ဆောင်မယ့်အစား ရှိပြီးသား စနစ်တွေကို ပိုအားကောင်းအောင်လုပ်ကြဖို့ ရောဂါထိန်းချုပ်ရေးနဲ့ ကာကွယ်ရေးဆိုင်ရာ ဥ‌ရောပစင်တာ က ၂၀၂၂ ခုနှစ်အတွင်း ထုတ်တဲ့ အစီရင်ခံစာတခုထဲမှာ အကြံပြုထားပါတယ်။ </s>
Log Probability Score: -98.53652954101562
OOV Words: ကပ်ရောဂါတခုအတွက်, စနစ်အသစ်တွေ, လုပ်ဆောင်မယ့်အစား, ရှိပြီးသား, စနစ်တွေကို, ပိုအားကောင်းအောင်လုပ်ကြဖို့, ရောဂါထိန်းချုပ်ရေးနဲ့, ကာကွယ်ရေးဆိုင်ရာ, ဥ‌ရောပစင်တာ, ၂၀၂၂, ခုနှစ်အတွင်း, ထုတ်တဲ့, အစီရင်ခံစာတခုထဲမှာ, အကြံပြုထားပါတယ်။
Number of OOV words: 14
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကပ်ရောဂါအသစ်တခု မရောက်ခင် စနစ်အသစ်တွေကို စမ်းသပ်ကြည့်ထားကြဖို့ အတွက်လည်း သူတို့က အားပေးပါတယ်။ </s>
Log Probability Score: -47.92193603515625
OOV Words: ကပ်ရောဂါအသစ်တခု, စနစ်အသစ်တွေကို, စမ်းသပ်ကြည့်ထားကြဖို့, အားပေးပါတယ်။
Number of OOV words: 4
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကျန်းမာရေးဆိုင်ရာ ဒေတာ အချက်အလက်တွေနဲ့ ပတ်သက်ပြီး စုဆောင်းတာ၊ ဆန်းစစ်တာ၊ အဓိပ္ပာယ်ပြန်တာတွေကို ဆက်တိုက်နဲ့ စနစ်တကျလုပ်ဆောင်‌ရေးကို ပိုတိုးမြှင့်ဖို့ အားပေးတဲ့ အကြံပြုမှုပေါင်း ၁၀ ခုကို WHO က ၂၀၂၂ ဇွန်လမှာ ထုတ်ပြန်ခဲ့ ပါတယ်။ </s>
Log Probability Score: -123.28478240966797
OOV Words: ကျန်းမာရေးဆိုင်ရာ, အချက်အလက်တွေနဲ့, စုဆောင်းတာ၊, ဆန်းစစ်တာ၊, အဓိပ္ပာယ်ပြန်တာတွေကို, ဆက်တိုက်နဲ့, စနစ်တကျလုပ်ဆောင်‌ရေးကို, ပိုတိုးမြှင့်ဖို့, အားပေးတဲ့, အကြံပြုမှုပေါင်း, ၁၀, WHO, ၂၀၂၂, ဇွန်လမှာ, ထုတ်ပြန်ခဲ့, ပါတယ်။
Number of OOV words: 16
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> “ရောဂါတခု မပျံ့နှံ့မီ၊ အသက်တွေ မဆုံးရှုံးမီ၊ ထိန်းသိမ်းရခက်ခဲတဲ့ အခြေအနေ မရောက်မီ၊ ရောဂါဖြစ်ပြီဆိုတာကို ဆောလျင်စွာ သိရှိနိုင်ရေးအတွက် စွမ်းဆောင်ရည် မြင့်တဲ့ ကူးစက်ရောဂါ စောင့်ကြည့်ရေး စနစ်တခု မရှိမဖြစ်လိုအပ်ကြောင်း” အဲဒီ အကြံ ပြုချက်တွေက ထောက်ပြထားပါတယ်။ </s>
Log Probability Score: -119.08399963378906
OOV Words: “ရောဂါတခု, မပျံ့နှံ့မီ၊, အသက်တွေ, မဆုံးရှုံးမီ၊, ထိန်းသိမ်းရခက်ခဲတဲ့, မရောက်မီ၊, ရောဂါဖြစ်ပြီဆိုတာကို, သိရှိနိုင်ရေးအတွက်, မြင့်တဲ့, စောင့်ကြည့်ရေး, စနစ်တခု, မရှိမဖြစ်လိုအပ်ကြောင်း”, ပြုချက်တွေက, ထောက်ပြထားပါတယ်။
Number of OOV words: 14
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ရောဂါတခု ရုတ်တရက်ဖြစ်ပွားလာတာရင် ကိုယ်သိရှိသတ်မှတ်ပြီးသား အကြောင်းရင်းတခုကြောင့် ဖြစ်တာလို့ မတွက်ဆနိုင်ကြောင်း WHO က လက်ခံထားပြီး “လောလောဆယ် မသိထားကြသေးတဲ့ ရောဂါပိုး တခုကနေ လူတွေ ရောဂါရလာနိုင်တယ်” ဆိုတာကို အသိအမှတ်ပြုထားပါတယ်။ </s>
Log Probability Score: -103.57569122314453
OOV Words: ရောဂါတခု, ရုတ်တရက်ဖြစ်ပွားလာတာရင်, ကိုယ်သိရှိသတ်မှတ်ပြီးသား, အကြောင်းရင်းတခုကြောင့်, ဖြစ်တာလို့, မတွက်ဆနိုင်ကြောင်း, WHO, လက်ခံထားပြီး, “လောလောဆယ်, မသိထားကြသေးတဲ့, တခုကနေ, ရောဂါရလာနိုင်တယ်”, အသိအမှတ်ပြုထားပါတယ်။
Number of OOV words: 13
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကာကွယ်ဆေးဆိုင်ရာ နည်းပညာပိုင်းတွေမှာလည်း နောက်ထပ် တိုးတက်မှုတွေ မြင်ရမယ်လို့ လူအများစုက မှန်းဆမျှော်လင့်ထားကြပါတယ်။ </s>
Log Probability Score: -46.97667694091797
OOV Words: ကာကွယ်ဆေးဆိုင်ရာ, နည်းပညာပိုင်းတွေမှာလည်း, မြင်ရမယ်လို့, လူအများစုက, မှန်းဆမျှော်လင့်ထားကြပါတယ်။
Number of OOV words: 5
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> ကိုဗစ်ရောဂါ စတင်ဖြစ်ပွားပြီး တနှစ်အတွင်း ကမ္ဘာတလွှားမှာ အမျိုးမျိုးသော ကိုဗစ်-၁၉ ကာကွယ်ဆေးတွေ ရရှိလာနိုင်တာဟာ ကာကွယ်ဆေးထုတ်လုပ်မှုနဲ့ ပတ်သက်ပြီး ထင်ရှားတဲ့ အောင်မြင်မှု တခုပါ။ </s>
Log Probability Score: -84.02906799316406
OOV Words: စတင်ဖြစ်ပွားပြီး, တနှစ်အတွင်း, ကမ္ဘာတလွှားမှာ, ကိုဗစ်-၁၉, ကာကွယ်ဆေးတွေ, ရရှိလာနိုင်တာဟာ, ကာကွယ်ဆေးထုတ်လုပ်မှုနဲ့, ထင်ရှားတဲ့, တခုပါ။
Number of OOV words: 9
Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Sentence: <s> အနာဂတ်မှာတော့ လူတွေကို အကာအကွယ်ပေးဖို့အတွက် ကာကွယ်ဆေး အသစ်တွေ ဖော်တဲ့နေရာမှာ သိပ္ပံပညာရှင်တွေအနေနဲ့ ရှိနှင့်ပြီးသား “ကာကွယ်ဆေးတွေ” ကို ဖြစ်လာတဲ့ရောဂါနဲ့ အညီ မြန်မြန်ဆန်ဆန် အဆင့်မြှင့်ပြောင်းလဲ နိုင်လိမ့်မယ်လို့ မျှော်လင့်ရပါတယ်။ </s>
Log Probability Score: -97.12353515625
OOV Words: အနာဂတ်မှာတော့, အကာအကွယ်ပေးဖို့အတွက်, ဖော်တဲ့နေရာမှာ, သိပ္ပံပညာရှင်တွေအနေနဲ့, ရှိနှင့်ပြီးသား, “ကာကွယ်ဆေးတွေ”, ဖြစ်လာတဲ့ရောဂါနဲ့, အဆင့်မြှင့်ပြောင်းလဲ, နိုင်လိမ့်မယ်လို့, မျှော်လင့်ရပါတယ်။
Number of OOV words: 10

63 sentences, 641 words
logprob= -3294.5959248542786
Total number of OOV words: 382

real    0m6.493s
user    0m6.212s
sys     0m0.228s
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

running without --perplexity option result:  

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ time python ./evaluate_lm.py --language_model ./model/5gram.arpa --vocab_file ./corpus/vocab.txt --test_data ./corpus/bbc_article1.txt
Loading the LM will be faster if you build a binary file.
Reading /home/yekyaw.thu/exp/lm/kenlm/model/5gram.arpa
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Sentence: <s> ရောဂါ X တကမ္ဘာလုံး ပြန့်လာရင် ဘယ်လို လုပ်ကြမလဲ </s>
Log Probability Score: -37.36429977416992
OOV Words: X, ပြန့်လာရင်, လုပ်ကြမလဲ
Number of OOV words: 3
Next word suggestions:
        <s>     Score: -35.854530334472656
        သည်     Score: -36.716209411621094
        ပါ      Score: -36.749080657958984
        တယ်     Score: -37.016357421875
        ၏       Score: -37.06570816040039

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ၂၃ ဇန်နဝါရီ ၂၀၂၄ </s>
Log Probability Score: -23.485849380493164
OOV Words: ၂၃, ၂၀၂၄
Number of OOV words: 2
Next word suggestions:
        <s>     Score: -21.9760799407959
        သည်     Score: -22.837757110595703
        ပါ      Score: -22.870628356933594
        တယ်     Score: -23.137908935546875
        ၏       Score: -23.187257766723633

Sentence: <s> အသစ်တင်ချိန် ၂၇ ဇန်နဝါရီ ၂၀၂၄ </s>
Log Probability Score: -29.58599090576172
OOV Words: အသစ်တင်ချိန်, ၂၇, ၂၀၂၄
Number of OOV words: 3
Next word suggestions:
        <s>     Score: -28.076221466064453
        သည်     Score: -28.937898635864258
        ပါ      Score: -28.97076988220215
        တယ်     Score: -29.238048553466797
        ၏       Score: -29.287399291992188

Sentence: <s> ဆွစ်ဇာလန်နိုင်ငံ ဒါးဗို့စ်က ကမ္ဘာ့စီးပွားရေး ဖိုရမ်မှာ ကျန်းမာရေး ကဏ္ဍဆိုင်ရာ ခေါင်းဆောင်တွေဟာ နောက်ထပ် တကမ္ဘာလုံး ပျံ့နှံ့ဖြစ်ပွားနိုင်တဲ့ ရောဂါတခု ဖြစ်လာရင် လုပ်ရမှာ တွေကို ကြိုတင်ပြင်ဆင် စီစဉ်ထားဖို့ က အရေးကြီးကြောင်း ဆွေးနွေးခဲ့ကြပါတယ်။ ပညာရှင်တွေကတော့ ဒီမသိသေးတဲ့ ရောဂါကို “ရောဂါ အိတ်စ်” (Disease X) လို့ နာမည်ပေးထားပါတယ်။ </s>
Log Probability Score: -165.9970703125
OOV Words: ဆွစ်ဇာလန်နိုင်ငံ, ဒါးဗို့စ်က, ကမ္ဘာ့စီးပွားရေး, ဖိုရမ်မှာ, ကဏ္ဍဆိုင်ရာ, ခေါင်းဆောင်တွေဟာ, ပျံ့နှံ့ဖြစ်ပွားနိုင်တဲ့, ရောဂါတခု, ဖြစ်လာရင်, ကြိုတင်ပြင်ဆင်, စီစဉ်ထားဖို့, အရေးကြီးကြောင်း, ဆွေးနွေးခဲ့ကြပါတယ်။, ပညာရှင်တွေကတော့, ဒီမသိသေးတဲ့, ရောဂါကို, “ရောဂါ, အိတ်စ်”, (Disease, X), နာမည်ပေးထားပါတယ်။
Number of OOV words: 21
Next word suggestions:
        <s>     Score: -164.4873046875
        သည်     Score: -165.34898376464844
        ပါ      Score: -165.38185119628906
        တယ်     Score: -165.64913940429688
        ၏       Score: -165.69847106933594

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကိုဗစ်-၁၉ တကမ္ဘာလုံးကို ပျံ့နှံ့ခဲ့တဲ့အချိန်တုန်းကလို ကျန်းမာရေး စနစ်တွေက မထိန်းချုပ် နိုင်ခဲ့တာ၊ စီးပွားရေးပိုင်းမှာ ဒေါ်လာ ထရီလျံနဲ့ချီပြီး ရှုံးခဲ့ကြတာ စတာတွေ အပါအဝင် အားလုံးမြင်လိုက်ရတဲ့ အဆုံးအရှုံးတွေ လျှော့ချနိုင်အောင် ကြိုတင် ပြင်ဆင်ထားဖို့က အရေးကြီးကြောင်း ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ (WHO) က အရင်ကာလတွေကတည်းက သတိပေးထားပါတယ်။ </s>
Log Probability Score: -142.34747314453125
OOV Words: ကိုဗစ်-၁၉, တကမ္ဘာလုံးကို, ပျံ့နှံ့ခဲ့တဲ့အချိန်တုန်းကလို, စနစ်တွေက, မထိန်းချုပ်, နိုင်ခဲ့တာ၊, စီးပွားရေးပိုင်းမှာ, ထရီလျံနဲ့ချီပြီး, ရှုံးခဲ့ကြတာ, အားလုံးမြင်လိုက်ရတဲ့, အဆုံးအရှုံးတွေ, လျှော့ချနိုင်အောင်, ပြင်ဆင်ထားဖို့က, အရေးကြီးကြောင်း, ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, (WHO), အရင်ကာလတွေကတည်းက, သတိပေးထားပါတယ်။
Number of OOV words: 18
Next word suggestions:
        <s>     Score: -140.83770751953125
        သည်     Score: -141.6993865966797
        ပါ      Score: -141.7322540283203
        တယ်     Score: -141.99954223632812
        ၏       Score: -142.0488739013672

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ရောဂါ အိတ်စ် (Disease X) ဆိုတာ ဘာလဲ </s>
Log Probability Score: -35.69732666015625
OOV Words: အိတ်စ်, (Disease, X)
Number of OOV words: 3
Next word suggestions:
        ကျေးဇူးပြုပါ    Score: -35.56293487548828
        ဆိုတာ   Score: -35.566078186035156
        </s>    Score: -35.69732666015625
        မသိ     Score: -35.88474655151367
        <s>     Score: -36.3519287109375

Sentence: <s> ဒါက တကယ့်ရောဂါ မဟုတ်သေးသလို ဒီနာမည်နဲ့ ရောဂါဆိုတာလည်းမရှိသေးပါဘူး။ </s>
Log Probability Score: -34.029563903808594
OOV Words: တကယ့်ရောဂါ, မဟုတ်သေးသလို, ဒီနာမည်နဲ့, ရောဂါဆိုတာလည်းမရှိသေးပါဘူး။
Number of OOV words: 4
Next word suggestions:
        <s>     Score: -32.51979446411133
        သည်     Score: -33.381473541259766
        ပါ      Score: -33.414344787597656
        တယ်     Score: -33.68162155151367
        ၏       Score: -33.73097229003906

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ဒါက အခုလက်ရှိထိ မပေါ်ပေါက်သေးပေမဲ့ ကူးစက်ပျံ့နှံ့နိုင်တဲ့ ဒါမှမဟုတ် နိုင်ငံတွေ၊ တိုက်ကြီးတွေကို ပျံ့နှံ့သွားပြီး ကမ္ဘာ့ကပ်ရောဂါအထိ ဖြစ်သွားနိုင်တဲ့ ကူးစက်ရောဂါတခုကို ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ က သတ်မှတ်ခေါ်ဝေါ်တဲ့ အသုံးအနှုန်း တခုပါ။ </s>
Log Probability Score: -94.48975372314453
OOV Words: အခုလက်ရှိထိ, မပေါ်ပေါက်သေးပေမဲ့, ကူးစက်ပျံ့နှံ့နိုင်တဲ့, နိုင်ငံတွေ၊, တိုက်ကြီးတွေကို, ပျံ့နှံ့သွားပြီး, ကမ္ဘာ့ကပ်ရောဂါအထိ, ဖြစ်သွားနိုင်တဲ့, ကူးစက်ရောဂါတခုကို, ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, သတ်မှတ်ခေါ်ဝေါ်တဲ့, တခုပါ။
Number of OOV words: 12
Next word suggestions:
        <s>     Score: -92.97998046875
        သည်     Score: -93.84166717529297
        ပါ      Score: -93.8745346069336
        တယ်     Score: -94.14180755615234
        ၏       Score: -94.191162109375

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကိုဗစ်-၁၉ ကမ္ဘာ့ရောဂါကပ်မတိုင်မီကတည်းက ဒီအသုံးအနှုန်းက ရှိခဲ့ပါတယ်။ ၂၀၁၈ ခုနှစ် ဖေဖော်ဝါရီမှာ WHO က ထုတ်ပြန်တဲ့ ဦးစားပေးစောင့်ကြည့်ရမယ့် ရောဂါစာရင်းထဲမှာ ရောဂါ အိတ်စ် လည်း ပါဝင်ပါတယ်။ </s>
Log Probability Score: -93.749755859375
OOV Words: ကိုဗစ်-၁၉, ကမ္ဘာ့ရောဂါကပ်မတိုင်မီကတည်းက, ဒီအသုံးအနှုန်းက, ရှိခဲ့ပါတယ်။, ၂၀၁၈, ဖေဖော်ဝါရီမှာ, WHO, ထုတ်ပြန်တဲ့, ဦးစားပေးစောင့်ကြည့်ရမယ့်, ရောဂါစာရင်းထဲမှာ, အိတ်စ်, ပါဝင်ပါတယ်။
Number of OOV words: 12
Next word suggestions:
        <s>     Score: -92.23998260498047
        သည်     Score: -93.10166931152344
        ပါ      Score: -93.13453674316406
        တယ်     Score: -93.40180969238281
        ၏       Score: -93.45116424560547

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့ က ကမကထပြုမှုနဲ့ ကျွမ်းကျင်သူတွေ စုပေါင်းကာ ရေးဆွဲ ထားတဲ့ စီမံချက်ဟာ ကမ္ဘာလုံးဆိုင်ရာ ဗျူဟာဖြစ်ပြီး အဲဒီထဲမှာ ကပ်ရောဂါ ပျံ့နှံ့ လာချိန်အတွင်း သုတေသနနဲ့ ထုတ်လုပ်မှု လုပ်ငန်းတွေ မြန်မြန်ဆန်ဆန် လုပ်ဆောင်နိုင်‌အောင် ပြင်ဆင်ထားတဲ့ အစီအစဉ်တွေ ပါဝင်ပါတယ်။ </s>
Log Probability Score: -131.4842071533203
OOV Words: ကမ္ဘာ့ကျန်းမာရေးအဖွဲ့, ကမကထပြုမှုနဲ့, ကျွမ်းကျင်သူတွေ, စုပေါင်းကာ, စီမံချက်ဟာ, ကမ္ဘာလုံးဆိုင်ရာ, ဗျူဟာဖြစ်ပြီး, အဲဒီထဲမှာ, လာချိန်အတွင်း, သုတေသနနဲ့, ထုတ်လုပ်မှု, လုပ်ငန်းတွေ, လုပ်ဆောင်နိုင်‌အောင်, ပါဝင်ပါတယ်။
Number of OOV words: 14
Next word suggestions:
        <s>     Score: -129.9744415283203
        သည်     Score: -130.83612060546875
        ပါ      Score: -130.86898803710938
        တယ်     Score: -131.1362762451172
        ၏       Score: -131.18560791015625

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ဒီအစီအစဉ်တွေဟာ ရောဂါပိုးရှိမရှိ သိဖို့လုပ်တဲ့ ဆေးစစ်မှုတွေ၊ ကာကွယ်ဆေးတွေ၊ ကုသမှုဆေးဝါးတွေကို စွမ်းဆောင်ရည်ရှိရှိနဲ့ ခပ်မြန်မြန်လုပ်ဆောင်နိုင်ပြီး လူတွေရဲ့ အသက်ကို ကယ်နိုင်ဖို့၊ အကျပ်အတည်း အကြီးအမားဆိုက်မှာကို ရှောင်ရှားနိုင်ဖို့ စတာ တွေ အတွက် ရည်ရွယ်တာပါ။ </s>
Log Probability Score: -104.09574127197266
OOV Words: ဒီအစီအစဉ်တွေဟာ, ရောဂါပိုးရှိမရှိ, သိဖို့လုပ်တဲ့, ဆေးစစ်မှုတွေ၊, ကာကွယ်ဆေးတွေ၊, ကုသမှုဆေးဝါးတွေကို, စွမ်းဆောင်ရည်ရှိရှိနဲ့, ခပ်မြန်မြန်လုပ်ဆောင်နိုင်ပြီး, လူတွေရဲ့, ကယ်နိုင်ဖို့၊, အကြီးအမားဆိုက်မှာကို, ရှောင်ရှားနိုင်ဖို့, ရည်ရွယ်တာပါ။
Number of OOV words: 13
Next word suggestions:
        <s>     Score: -102.58596801757812
        သည်     Score: -103.4476547241211
        ပါ      Score: -103.48052215576172
        တယ်     Score: -103.74779510498047
        ၏       Score: -103.79714965820312

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ပြီးခဲ့တဲ့နှစ်ပိုင်းတွေအတွင်း ဥပမာ - ဆားစ် ရောဂါ (Sars - Severe Acute Respiratory Syndrome)၊ ဝက်တုပ်ကွေး (Swine flu) ၊ မားစ် (Mers - Middle East Respiratory Syndrome), အီဘိုလာ ရောဂါ (Ebola)၊ ကိုဗစ်-၁၉ စတဲ့ရောဂါတွေ ကမ္ဘာမှာ ပျံ့နှံ့ ကူးစက်ခဲ့ပါတယ်။ </s>
Log Probability Score: -181.41049194335938
OOV Words: ပြီးခဲ့တဲ့နှစ်ပိုင်းတွေအတွင်း, -, ဆားစ်, (Sars, -, Severe, Acute, Respiratory, Syndrome)၊, ဝက်တုပ်ကွေး, (Swine, flu), ၊, (Mers, -, Middle, East, Respiratory, Syndrome),, (Ebola)၊, ကိုဗစ်-၁၉, စတဲ့ရောဂါတွေ, ကမ္ဘာမှာ, ကူးစက်ခဲ့ပါတယ်။
Number of OOV words: 24
Next word suggestions:
        <s>     Score: -179.90072631835938
        သည်     Score: -180.7624053955078
        ပါ      Score: -180.79527282714844
        တယ်     Score: -181.06256103515625
        ၏       Score: -181.1118927001953

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> နောက်ထပ် ကမ္ဘာကပ်တခု ရောက်လာနိုင်တာ နဲ့ အဲဒီရောဂါဟာ ကိုဗစ်-၁၉ ကို ဖြစ်စေတဲ့ ကိုရိုနာဗိုင်းရပ်စ်ထက် ဆိုးဝါးနိုင်တယ်ဆိုတာကို ကျန်းမာရေး ပညာရှင်တွေက စိုးရိမ် ထိတ်လန့်နေပါတယ်။ </s>
Log Probability Score: -78.83583068847656
OOV Words: ကမ္ဘာကပ်တခု, ရောက်လာနိုင်တာ, အဲဒီရောဂါဟာ, ကိုဗစ်-၁၉, ဖြစ်စေတဲ့, ကိုရိုနာဗိုင်းရပ်စ်ထက်, ဆိုးဝါးနိုင်တယ်ဆိုတာကို, ပညာရှင်တွေက, ထိတ်လန့်နေပါတယ်။
Number of OOV words: 9
Next word suggestions:
        <s>     Score: -77.32605743408203
        သည်     Score: -78.187744140625
        ပါ      Score: -78.22061157226562
        တယ်     Score: -78.48788452148438
        ၏       Score: -78.53723907470703

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ရောဂါ အိတ်စ် က ကမ္ဘာ့ကပ်တခု ဖြစ်လာမလား </s>
Log Probability Score: -30.80592918395996
OOV Words: အိတ်စ်, ကမ္ဘာ့ကပ်တခု, ဖြစ်လာမလား
Number of OOV words: 3
Next word suggestions:
        <s>     Score: -29.296159744262695
        သည်     Score: -30.1578369140625
        ပါ      Score: -30.19070816040039
        တယ်     Score: -30.457988739013672
        ၏       Score: -30.50733757019043

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ရောဂါ အိတ်စ်က လောလောဆယ်မှာ မပေါ်ထွန်းသေးပေမယ့် သုတေသီတွေ၊ သိပ္ပံပညာရှင်တွေ၊ ကျွမ်းကျင်သူတွေက ဒီလို ဗိုင်းရပ်စ် မျိုးပေါ်လာရင် တုံ့ပြန် ဆောင်ရွက်နိုင်ဖို့ အစီအစဉ် နဲ့ အဲဒီ ကမ္ဘာ့ကပ်ကို ရင်ဆိုင်နိုင်ဖို့အရေး ကျန်းမာရေးစနစ်ကို ဘယ်လို စီစဉ်ထားရမလဲဆိုတာတွေကို ကြိုကြိုတင်တင် လုပ်ဆောင်ထားနိုင်ဖို့ မျှော်လင့် နေပါတယ်။ </s>
Log Probability Score: -131.12477111816406
OOV Words: အိတ်စ်က, လောလောဆယ်မှာ, မပေါ်ထွန်းသေးပေမယ့်, သုတေသီတွေ၊, သိပ္ပံပညာရှင်တွေ၊, ကျွမ်းကျင်သူတွေက, မျိုးပေါ်လာရင်, ဆောင်ရွက်နိုင်ဖို့, ကမ္ဘာ့ကပ်ကို, ရင်ဆိုင်နိုင်ဖို့အရေး, ကျန်းမာရေးစနစ်ကို, စီစဉ်ထားရမလဲဆိုတာတွေကို, လုပ်ဆောင်ထားနိုင်ဖို့, နေပါတယ်။
Number of OOV words: 14
Next word suggestions:
        <s>     Score: -129.61500549316406
        သည်     Score: -130.4766845703125
        ပါ      Score: -130.50955200195312
        တယ်     Score: -130.77684020996094
        ၏       Score: -130.826171875

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ပြီးခဲ့တဲ့ သီတင်းပတ်အတွင်းက ကမ္ဘာ့ စီးပွားရေးဖိုရမ်မှာ WHO အကြီးအကဲ ဒေါက်တာ တက်ဒရို့စ် ဆန်ဒါနွန် ဂက်ဘရီရီးဆပ်စ် ဦးဆောင်ခဲ့ပြီး “ရောဂါ အိတ်စ် အတွက် ပြင်ဆင်ခြင်း” လို့အမည်ရတဲ့ ကြားဖြတ်ဆွေးနွေးပွဲတခုကို ပြုလုပ်ခဲ့ကြကာ “ရှေ့မှာ ဖြစ်လာမယ့် စိန်ခေါ်မှု အများအပြားအတွက် ကျန်းမာရေး စနစ်တွေကို ပြင်ဆင်ဖို့ရာမှာ လိုအပ်တဲ့ အားထုတ်ဆောင်ရွက်မှု” တွေကို ဆွေးနွေးခဲ့ကြပါတယ်။ </s>
Log Probability Score: -172.65003967285156
OOV Words: ပြီးခဲ့တဲ့, သီတင်းပတ်အတွင်းက, စီးပွားရေးဖိုရမ်မှာ, WHO, တက်ဒရို့စ်, ဆန်ဒါနွန်, ဂက်ဘရီရီးဆပ်စ်, ဦးဆောင်ခဲ့ပြီး, “ရောဂါ, အိတ်စ်, ပြင်ဆင်ခြင်း”, လို့အမည်ရတဲ့, ကြားဖြတ်ဆွေးနွေးပွဲတခုကို, ပြုလုပ်ခဲ့ကြကာ, “ရှေ့မှာ, ဖြစ်လာမယ့်, စိန်ခေါ်မှု, အများအပြားအတွက်, စနစ်တွေကို, ပြင်ဆင်ဖို့ရာမှာ, အားထုတ်ဆောင်ရွက်မှု”, ဆွေးနွေးခဲ့ကြပါတယ်။
Number of OOV words: 22
Next word suggestions:
        <s>     Score: -171.14027404785156
        သည်     Score: -172.001953125
        ပါ      Score: -172.03482055664062
        တယ်     Score: -172.30210876464844
        ၏       Score: -172.3514404296875

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> “ဒါက ကြောက်ရွံ့မှုတွေကို ဖြစ်သွားစေမယ်လို့ တချို့လူတွေက ပြောတာပေါ့” လို့ ဒေါက်တာ တက်ဒရို့စ်က ဆို ပါတယ်။ </s>
Log Probability Score: -58.95525360107422
OOV Words: “ဒါက, ကြောက်ရွံ့မှုတွေကို, ဖြစ်သွားစေမယ်လို့, တချို့လူတွေက, ပြောတာပေါ့”, တက်ဒရို့စ်က, ပါတယ်။
Number of OOV words: 7
Next word suggestions:
        <s>     Score: -57.44548416137695
        သည်     Score: -58.30716323852539
        ပါ      Score: -58.34003448486328
        တယ်     Score: -58.6073112487793
        ၏       Score: -58.65666198730469

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> “ဒီလို ကပ်မျိုးတွေ ဖြစ်လာမှာကို ကြိုတင်မှန်းထားတာက ပိုကောင်းတယ်၊ ဘာ့ကြောင့် လဲဆိုတော့ ကျွန်တော်တို့ သမိုင်းမှာ အကြိမ်များစွာ ဖြစ်ခဲ့ပြီးပြီလေ၊ ဒီတော့ အဲဒီအတွက် ကြိုတင်ပြင်ဆင်ထားဖို့လိုတယ်။” </s>
Log Probability Score: -90.61121368408203
OOV Words: “ဒီလို, ကပ်မျိုးတွေ, ဖြစ်လာမှာကို, ကြိုတင်မှန်းထားတာက, ပိုကောင်းတယ်၊, လဲဆိုတော့, ကျွန်တော်တို့, သမိုင်းမှာ, အကြိမ်များစွာ, ဖြစ်ခဲ့ပြီးပြီလေ၊, အဲဒီအတွက်, ကြိုတင်ပြင်ဆင်ထားဖို့လိုတယ်။”
Number of OOV words: 12
Next word suggestions:
        <s>     Score: -89.1014404296875
        သည်     Score: -89.96312713623047
        ပါ      Score: -89.9959945678711
        တယ်     Score: -90.26326751708984
        ၏       Score: -90.3126220703125

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကမ္ဘာက၊ လူအတော်များများက ကိုဗစ်-၁၉ ကပ်ကို အတော် အံ့အားသင့်ခဲ့ကြပါတယ်၊ ၂၀၂၁ မှာ BBC Future ဌာနက “ကမ္ဘာတလွှားကို ပျံ့နှံ့မယ့် ကပ်ဘေးတခုအတွက် ကျန်ုပ်တို့ ပြင်ဆင်ထားကြဖို့ ကူးစက်ရောဂါပျံ့နှံမှုနဲ့ ကာကွယ်ရေးဆိုင်ရာ ကျန်းမာရေးပညာရှင်တွေ၊ တခြားကျွမ်းကျင်သူတွေက သတိပေးနေတာ နှစ်အတော် ကြာကြာကတည်းကပါ” လို့ ရေးဖူးပါတယ်။ </s>
Log Probability Score: -150.66319274902344
OOV Words: ကမ္ဘာက၊, လူအတော်များများက, ကိုဗစ်-၁၉, ကပ်ကို, အံ့အားသင့်ခဲ့ကြပါတယ်၊, ၂၀၂၁, BBC, Future, ဌာနက, “ကမ္ဘာတလွှားကို, ပျံ့နှံ့မယ့်, ကပ်ဘေးတခုအတွက်, ကျန်ုပ်တို့, ပြင်ဆင်ထားကြဖို့, ကူးစက်ရောဂါပျံ့နှံမှုနဲ့, ကာကွယ်ရေးဆိုင်ရာ, ကျန်းမာရေးပညာရှင်တွေ၊, တခြားကျွမ်းကျင်သူတွေက, သတိပေးနေတာ, နှစ်အတော်, ကြာကြာကတည်းကပါ”, ရေးဖူးပါတယ်။
Number of OOV words: 22
Next word suggestions:
        <s>     Score: -149.15342712402344
        သည်     Score: -150.01510620117188
        ပါ      Score: -150.0479736328125
        တယ်     Score: -150.3152618408203
        ၏       Score: -150.36459350585938

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> အဲဒီကျွမ်းကျင်သူအများစုက တိရိစ္ဆာန်တွေဆီကနေ ကပ်ရောဂါ စတင်နိုင်တယ် ဆိုတာကို စိုးရိမ်ခဲ့ကြပါတယ်။ </s>
Log Probability Score: -41.254173278808594
OOV Words: အဲဒီကျွမ်းကျင်သူအများစုက, တိရိစ္ဆာန်တွေဆီကနေ, စတင်နိုင်တယ်, စိုးရိမ်ခဲ့ကြပါတယ်။
Number of OOV words: 4
Next word suggestions:
        <s>     Score: -39.74440383911133
        သည်     Score: -40.606082916259766
        ပါ      Score: -40.638954162597656
        တယ်     Score: -40.90623092651367
        ၏       Score: -40.95558166503906

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> တကယ်တော့ အသစ်ပေါ်လာတဲ့ ရောဂါတွေထဲက ၇၅% ဟာ ဇူးနော်တစ် (zoonotic) လို့ ခေါ်ကြတဲ့ တိရိစ္ဆာန်ကနေ လူတွေဆီကို ကူးစက်ပျံ့နှံ့လာတဲ့ ရောဂါတွေပါ။ </s>
Log Probability Score: -77.30233764648438
OOV Words: အသစ်ပေါ်လာတဲ့, ရောဂါတွေထဲက, ၇၅%, ဇူးနော်တစ်, (zoonotic), ခေါ်ကြတဲ့, တိရိစ္ဆာန်ကနေ, လူတွေဆီကို, ကူးစက်ပျံ့နှံ့လာတဲ့, ရောဂါတွေပါ။
Number of OOV words: 10
Next word suggestions:
        <s>     Score: -75.79256439208984
        သည်     Score: -76.65425109863281
        ပါ      Score: -76.68711853027344
        တယ်     Score: -76.95439147949219
        ၏       Score: -77.00374603271484

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> တရုတ်နိုင်ငံတွင်း တိရိစ္ဆာန်အရှင်တွေရောင်းတဲ့ စျေးတခုက လင်းနို့တွေဆီကနေ အစပြုလာတာလို့ ယူဆရတဲ့ ကိုဗစ်-၁၉ ရောဂါဟာလည်း ဒီလို ရောဂါမျိုးထဲက တခုပါ။ ဒါပေမဲ့ ကိုဗစ်-၁၉ လို ဇူးနော်တစ် ရောဂါဟာ လူတွေရဲ့ လုပ်ဆောင်မှုတွေကြောင့် ပိုပြီး အန္တရာယ်များသွားတယ်လို့ မှတ်ယူနိုင်ပါတယ်။ </s>
Log Probability Score: -126.19227600097656
OOV Words: တရုတ်နိုင်ငံတွင်း, တိရိစ္ဆာန်အရှင်တွေရောင်းတဲ့, စျေးတခုက, လင်းနို့တွေဆီကနေ, အစပြုလာတာလို့, ယူဆရတဲ့, ကိုဗစ်-၁၉, ရောဂါဟာလည်း, ရောဂါမျိုးထဲက, တခုပါ။, ကိုဗစ်-၁၉, ဇူးနော်တစ်, ရောဂါဟာ, လူတွေရဲ့, လုပ်ဆောင်မှုတွေကြောင့်, အန္တရာယ်များသွားတယ်လို့, မှတ်ယူနိုင်ပါတယ်။
Number of OOV words: 17
Next word suggestions:
        <s>     Score: -124.68250274658203
        သည်     Score: -125.544189453125
        ပါ      Score: -125.57705688476562
        တယ်     Score: -125.84432983398438
        ၏       Score: -125.89368438720703

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ရာသီဥတုအပေါ် လူသားတွေရဲ့ သက်ရောက်မှုတွေ၊ သဘာဝတောရိုင်းနေရာတွေကို လူသားတွေက ဝင်ယူလာတာတွေ၊ ကမ္ဘာအနှံ့ကို လူတွေ ခရီးသွားကြတာတွေ၊ စတာတွေက တိရိစ္ဆာန်ကြောင့် စဖြစ်လာတဲ့ ရောဂါကို ပိုပျံ့နှံ့စေပါတယ်။ </s>
Log Probability Score: -90.70189666748047
OOV Words: ရာသီဥတုအပေါ်, လူသားတွေရဲ့, သက်ရောက်မှုတွေ၊, သဘာဝတောရိုင်းနေရာတွေကို, လူသားတွေက, ဝင်ယူလာတာတွေ၊, ကမ္ဘာအနှံ့ကို, ခရီးသွားကြတာတွေ၊, စတာတွေက, တိရိစ္ဆာန်ကြောင့်, စဖြစ်လာတဲ့, ရောဂါကို, ပိုပျံ့နှံ့စေပါတယ်။
Number of OOV words: 13
Next word suggestions:
        <s>     Score: -89.19212341308594
        သည်     Score: -90.0538101196289
        ပါ      Score: -90.08667755126953
        တယ်     Score: -90.35395050048828
        ၏       Score: -90.40330505371094

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> နောင်လာမယ့် ကမ္ဘာ့ကပ်အတွက် ကမ္ဘာက ဘယ်လို ပြင်ဆင်ထားနေလဲ </s>
Log Probability Score: -34.48929977416992
OOV Words: နောင်လာမယ့်, ကမ္ဘာ့ကပ်အတွက်, ကမ္ဘာက, ပြင်ဆင်ထားနေလဲ
Number of OOV words: 4
Next word suggestions:
        <s>     Score: -32.979530334472656
        သည်     Score: -33.841209411621094
        ပါ      Score: -33.874080657958984
        တယ်     Score: -34.141357421875
        ၏       Score: -34.19070816040039

Sentence: <s> နောက်ထပ် ကမ္ဘာ့ကပ်အတွက် ရည်ရွယ်ပြင်ဆင်ထားတဲ့ လုပ်ဆောင်မှုတွေကို WHO အနေနဲ့ စပြီး အကောင်အထည်ဖော် လုပ်ဆောင်နေပြီလို့ ကမ္ဘာ့စီးပွားရေး ဖိုရမ်က ကြားဖြတ် ဆွေးနွေးပွဲမှာ ဒေါက်တာ တက်ဒရို့စ်က ပြောပါတယ်။ </s>
Log Probability Score: -92.91385650634766
OOV Words: ကမ္ဘာ့ကပ်အတွက်, ရည်ရွယ်ပြင်ဆင်ထားတဲ့, လုပ်ဆောင်မှုတွေကို, WHO, လုပ်ဆောင်နေပြီလို့, ကမ္ဘာ့စီးပွားရေး, ဖိုရမ်က, ဆွေးနွေးပွဲမှာ, တက်ဒရို့စ်က, ပြောပါတယ်။
Number of OOV words: 10
Next word suggestions:
        <s>     Score: -91.40408325195312
        သည်     Score: -92.2657699584961
        ပါ      Score: -92.29863739013672
        တယ်     Score: -92.56591033935547
        ၏       Score: -92.61526489257812

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> အဲဒီလုပ်ဆောင်မှုတွေထဲမှာ ကမ္ဘာ့ကပ် ရန်ပုံငွေတခုနဲ့ တောင်အာဖရိကမှာ “နည်းပညာ လွှဲပြောင်းပေးတဲ့ ဆုံရပ်ဌာန” တခုတို့ ပါဝင်ပြီး အဲဒါတွေက ကာကွယ်ဆေးတွေ ဒေသတွင်းမှာ ထုတ်လုပ်နိုင်မှာ ဖြစ်သလို ဝင်ငွေမြင့်တဲ့ နိုင်ငံတွေနဲ့ ဝင်ငွေနည်းတဲ့ နိုင်ငံတွေအကြား ကာကွယ်ဆေး လက်လှမ်းမီနိုင်မှု ကွာဟချက်တွေကို ကျော်လွှား နိုင်ရေးမှာ အထောက်အကူ ဖြစ်လာမှာပါ။ </s>
Log Probability Score: -156.616943359375
OOV Words: အဲဒီလုပ်ဆောင်မှုတွေထဲမှာ, ကမ္ဘာ့ကပ်, ရန်ပုံငွေတခုနဲ့, တောင်အာဖရိကမှာ, “နည်းပညာ, လွှဲပြောင်းပေးတဲ့, ဆုံရပ်ဌာန”, တခုတို့, ပါဝင်ပြီး, အဲဒါတွေက, ကာကွယ်ဆေးတွေ, ဒေသတွင်းမှာ, ထုတ်လုပ်နိုင်မှာ, ဝင်ငွေမြင့်တဲ့, နိုင်ငံတွေနဲ့, ဝင်ငွေနည်းတဲ့, နိုင်ငံတွေအကြား, လက်လှမ်းမီနိုင်မှု, ကွာဟချက်တွေကို, နိုင်ရေးမှာ, ဖြစ်လာမှာပါ။
Number of OOV words: 21
Next word suggestions:
        <s>     Score: -155.107177734375
        သည်     Score: -155.96885681152344
        ပါ      Score: -156.00172424316406
        တယ်     Score: -156.26901245117188
        ၏       Score: -156.31834411621094

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကပ်ရောဂါတခုအတွက် နောက်ထပ် စနစ်အသစ်တွေ လုပ်ဆောင်မယ့်အစား ရှိပြီးသား စနစ်တွေကို ပိုအားကောင်းအောင်လုပ်ကြဖို့ ရောဂါထိန်းချုပ်ရေးနဲ့ ကာကွယ်ရေးဆိုင်ရာ ဥ‌ရောပစင်တာ က ၂၀၂၂ ခုနှစ်အတွင်း ထုတ်တဲ့ အစီရင်ခံစာတခုထဲမှာ အကြံပြုထားပါတယ်။ </s>
Log Probability Score: -98.53652954101562
OOV Words: ကပ်ရောဂါတခုအတွက်, စနစ်အသစ်တွေ, လုပ်ဆောင်မယ့်အစား, ရှိပြီးသား, စနစ်တွေကို, ပိုအားကောင်းအောင်လုပ်ကြဖို့, ရောဂါထိန်းချုပ်ရေးနဲ့, ကာကွယ်ရေးဆိုင်ရာ, ဥ‌ရောပစင်တာ, ၂၀၂၂, ခုနှစ်အတွင်း, ထုတ်တဲ့, အစီရင်ခံစာတခုထဲမှာ, အကြံပြုထားပါတယ်။
Number of OOV words: 14
Next word suggestions:
        <s>     Score: -97.0267562866211
        သည်     Score: -97.88844299316406
        ပါ      Score: -97.92131042480469
        တယ်     Score: -98.18858337402344
        ၏       Score: -98.2379379272461

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကပ်ရောဂါအသစ်တခု မရောက်ခင် စနစ်အသစ်တွေကို စမ်းသပ်ကြည့်ထားကြဖို့ အတွက်လည်း သူတို့က အားပေးပါတယ်။ </s>
Log Probability Score: -47.92193603515625
OOV Words: ကပ်ရောဂါအသစ်တခု, စနစ်အသစ်တွေကို, စမ်းသပ်ကြည့်ထားကြဖို့, အားပေးပါတယ်။
Number of OOV words: 4
Next word suggestions:
        <s>     Score: -46.412166595458984
        သည်     Score: -47.27384567260742
        ပါ      Score: -47.30671691894531
        တယ်     Score: -47.57399368286133
        ၏       Score: -47.62334442138672

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကျန်းမာရေးဆိုင်ရာ ဒေတာ အချက်အလက်တွေနဲ့ ပတ်သက်ပြီး စုဆောင်းတာ၊ ဆန်းစစ်တာ၊ အဓိပ္ပာယ်ပြန်တာတွေကို ဆက်တိုက်နဲ့ စနစ်တကျလုပ်ဆောင်‌ရေးကို ပိုတိုးမြှင့်ဖို့ အားပေးတဲ့ အကြံပြုမှုပေါင်း ၁၀ ခုကို WHO က ၂၀၂၂ ဇွန်လမှာ ထုတ်ပြန်ခဲ့ ပါတယ်။ </s>
Log Probability Score: -123.28478240966797
OOV Words: ကျန်းမာရေးဆိုင်ရာ, အချက်အလက်တွေနဲ့, စုဆောင်းတာ၊, ဆန်းစစ်တာ၊, အဓိပ္ပာယ်ပြန်တာတွေကို, ဆက်တိုက်နဲ့, စနစ်တကျလုပ်ဆောင်‌ရေးကို, ပိုတိုးမြှင့်ဖို့, အားပေးတဲ့, အကြံပြုမှုပေါင်း, ၁၀, WHO, ၂၀၂၂, ဇွန်လမှာ, ထုတ်ပြန်ခဲ့, ပါတယ်။
Number of OOV words: 16
Next word suggestions:
        <s>     Score: -121.77500915527344
        သည်     Score: -122.6366958618164
        ပါ      Score: -122.66956329345703
        တယ်     Score: -122.93683624267578
        ၏       Score: -122.98619079589844

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> “ရောဂါတခု မပျံ့နှံ့မီ၊ အသက်တွေ မဆုံးရှုံးမီ၊ ထိန်းသိမ်းရခက်ခဲတဲ့ အခြေအနေ မရောက်မီ၊ ရောဂါဖြစ်ပြီဆိုတာကို ဆောလျင်စွာ သိရှိနိုင်ရေးအတွက် စွမ်းဆောင်ရည် မြင့်တဲ့ ကူးစက်ရောဂါ စောင့်ကြည့်ရေး စနစ်တခု မရှိမဖြစ်လိုအပ်ကြောင်း” အဲဒီ အကြံ ပြုချက်တွေက ထောက်ပြထားပါတယ်။ </s>
Log Probability Score: -119.08399963378906
OOV Words: “ရောဂါတခု, မပျံ့နှံ့မီ၊, အသက်တွေ, မဆုံးရှုံးမီ၊, ထိန်းသိမ်းရခက်ခဲတဲ့, မရောက်မီ၊, ရောဂါဖြစ်ပြီဆိုတာကို, သိရှိနိုင်ရေးအတွက်, မြင့်တဲ့, စောင့်ကြည့်ရေး, စနစ်တခု, မရှိမဖြစ်လိုအပ်ကြောင်း”, ပြုချက်တွေက, ထောက်ပြထားပါတယ်။
Number of OOV words: 14
Next word suggestions:
        <s>     Score: -117.57422637939453
        သည်     Score: -118.4359130859375
        ပါ      Score: -118.46878051757812
        တယ်     Score: -118.73605346679688
        ၏       Score: -118.78540802001953

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ရောဂါတခု ရုတ်တရက်ဖြစ်ပွားလာတာရင် ကိုယ်သိရှိသတ်မှတ်ပြီးသား အကြောင်းရင်းတခုကြောင့် ဖြစ်တာလို့ မတွက်ဆနိုင်ကြောင်း WHO က လက်ခံထားပြီး “လောလောဆယ် မသိထားကြသေးတဲ့ ရောဂါပိုး တခုကနေ လူတွေ ရောဂါရလာနိုင်တယ်” ဆိုတာကို အသိအမှတ်ပြုထားပါတယ်။ </s>
Log Probability Score: -103.57569122314453
OOV Words: ရောဂါတခု, ရုတ်တရက်ဖြစ်ပွားလာတာရင်, ကိုယ်သိရှိသတ်မှတ်ပြီးသား, အကြောင်းရင်းတခုကြောင့်, ဖြစ်တာလို့, မတွက်ဆနိုင်ကြောင်း, WHO, လက်ခံထားပြီး, “လောလောဆယ်, မသိထားကြသေးတဲ့, တခုကနေ, ရောဂါရလာနိုင်တယ်”, အသိအမှတ်ပြုထားပါတယ်။
Number of OOV words: 13
Next word suggestions:
        <s>     Score: -102.06591796875
        သည်     Score: -102.92760467529297
        ပါ      Score: -102.9604721069336
        တယ်     Score: -103.22774505615234
        ၏       Score: -103.277099609375

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကာကွယ်ဆေးဆိုင်ရာ နည်းပညာပိုင်းတွေမှာလည်း နောက်ထပ် တိုးတက်မှုတွေ မြင်ရမယ်လို့ လူအများစုက မှန်းဆမျှော်လင့်ထားကြပါတယ်။ </s>
Log Probability Score: -46.97667694091797
OOV Words: ကာကွယ်ဆေးဆိုင်ရာ, နည်းပညာပိုင်းတွေမှာလည်း, မြင်ရမယ်လို့, လူအများစုက, မှန်းဆမျှော်လင့်ထားကြပါတယ်။
Number of OOV words: 5
Next word suggestions:
        <s>     Score: -45.4669075012207
        သည်     Score: -46.32858657836914
        ပါ      Score: -46.36145782470703
        တယ်     Score: -46.62873458862305
        ၏       Score: -46.67808532714844

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> ကိုဗစ်ရောဂါ စတင်ဖြစ်ပွားပြီး တနှစ်အတွင်း ကမ္ဘာတလွှားမှာ အမျိုးမျိုးသော ကိုဗစ်-၁၉ ကာကွယ်ဆေးတွေ ရရှိလာနိုင်တာဟာ ကာကွယ်ဆေးထုတ်လုပ်မှုနဲ့ ပတ်သက်ပြီး ထင်ရှားတဲ့ အောင်မြင်မှု တခုပါ။ </s>
Log Probability Score: -84.02906799316406
OOV Words: စတင်ဖြစ်ပွားပြီး, တနှစ်အတွင်း, ကမ္ဘာတလွှားမှာ, ကိုဗစ်-၁၉, ကာကွယ်ဆေးတွေ, ရရှိလာနိုင်တာဟာ, ကာကွယ်ဆေးထုတ်လုပ်မှုနဲ့, ထင်ရှားတဲ့, တခုပါ။
Number of OOV words: 9
Next word suggestions:
        <s>     Score: -82.51929473876953
        သည်     Score: -83.3809814453125
        ပါ      Score: -83.41384887695312
        တယ်     Score: -83.68112182617188
        ၏       Score: -83.73047637939453

Sentence: <s>  </s>
Log Probability Score: -5.765833377838135
OOV Words:
Number of OOV words: 0
Next word suggestions:
        အခန်း   Score: -4.539181709289551
        လေ့ကျင့်ခန်း    Score: -4.562793731689453
        ဖုန်း   Score: -4.581358432769775
        ဟုတ်ကဲ့ Score: -4.669960021972656
        သတင်းစဉ်        Score: -4.694637775421143

Sentence: <s> အနာဂတ်မှာတော့ လူတွေကို အကာအကွယ်ပေးဖို့အတွက် ကာကွယ်ဆေး အသစ်တွေ ဖော်တဲ့နေရာမှာ သိပ္ပံပညာရှင်တွေအနေနဲ့ ရှိနှင့်ပြီးသား “ကာကွယ်ဆေးတွေ” ကို ဖြစ်လာတဲ့ရောဂါနဲ့ အညီ မြန်မြန်ဆန်ဆန် အဆင့်မြှင့်ပြောင်းလဲ နိုင်လိမ့်မယ်လို့ မျှော်လင့်ရပါတယ်။ </s>
Log Probability Score: -97.12353515625
OOV Words: အနာဂတ်မှာတော့, အကာအကွယ်ပေးဖို့အတွက်, ဖော်တဲ့နေရာမှာ, သိပ္ပံပညာရှင်တွေအနေနဲ့, ရှိနှင့်ပြီးသား, “ကာကွယ်ဆေးတွေ”, ဖြစ်လာတဲ့ရောဂါနဲ့, အဆင့်မြှင့်ပြောင်းလဲ, နိုင်လိမ့်မယ်လို့, မျှော်လင့်ရပါတယ်။
Number of OOV words: 10
Next word suggestions:
        <s>     Score: -95.61376190185547
        သည်     Score: -96.47544860839844
        ပါ      Score: -96.50831604003906
        တယ်     Score: -96.77558898925781
        ၏       Score: -96.82494354248047

Total number of OOV words: 382

real    0m22.931s
user    0m22.699s
sys     0m0.216s
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

