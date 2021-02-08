## git clone

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ git clone https://github.com/moses-smt/mosesdecoder.git

## Open README file

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ gedit README

And you must refer following link:
http://www.statmt.org/moses/?n=Development.GetStarted

## Check How Many CPU

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ lscpu
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   39 bits physical, 48 bits virtual
CPU(s):                          8
On-line CPU(s) list:             0-7
Thread(s) per core:              1
Core(s) per socket:              8
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       GenuineIntel
CPU family:                      6
Model:                           158
Model name:                      Intel(R) Core(TM) i7-9700 CPU @ 3.00GHz
Stepping:                        13
CPU MHz:                         800.252
CPU max MHz:                     4700.0000
CPU min MHz:                     800.0000
BogoMIPS:                        6000.00
Virtualization:                  VT-x
L1d cache:                       256 KiB
L1i cache:                       256 KiB
L2 cache:                        2 MiB
L3 cache:                        12 MiB
NUMA node0 CPU(s):               0-7
Vulnerability Itlb multihit:     KVM: Mitigation: VMX disabled
Vulnerability L1tf:              Not affected
Vulnerability Mds:               Not affected
Vulnerability Meltdown:          Not affected
Vulnerability Spec store bypass: Mitigation; Speculative Store Bypass disabled via prctl and seccomp
Vulnerability Spectre v1:        Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:        Mitigation; Enhanced IBRS, IBPB conditional, RSB filling
Vulnerability Srbds:             Mitigation; TSX disabled
Vulnerability Tsx async abort:   Mitigation; TSX disabled
Flags:                           fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch
                                 _perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_
                                 2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow 
                                 vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida a
                                 rat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d arch_capabilities
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

## Run bjam

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ ./bjam -j8
...
...
...
BaseManager.cpp:(.text._ZN5boost9iostreams6detail9close_allINS0_21basic_gzip_compressorISaIcEEENS1_16linked_streambufIcSt11char_traitsIcEEEEEvRT_RT0_[_ZN5boost9iostreams6detail9close_allINS0_21basic_gzip_compressorISaIcEEENS1_16linked_streambufIcSt11char_traitsIcEEEEEvRT_RT0_]+0x44): undefined reference to `boost::iostreams::detail::zlib_base::reset(bool, bool)'
/usr/bin/ld: moses/bin/gcc-10/release/link-static/threading-multi/libmoses.a(BaseManager.o): in function `long boost::iostreams::symmetric_filter<boost::iostreams::detail::zlib_compressor_impl<std::allocator<char> >, std::allocator<char> >::read<boost::iostreams::detail::linked_streambuf<char, std::char_traits<char> > >(boost::iostreams::detail::linked_streambuf<char, std::char_traits<char> >&, char*, long)':
BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0x9b): undefined reference to `boost::iostreams::detail::zlib_base::before(char const*&, char const*, char*&, char*)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0xa1): undefined reference to `boost::iostreams::zlib::no_flush'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0xb2): undefined reference to `boost::iostreams::detail::zlib_base::xdeflate(int)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0xc7): undefined reference to `boost::iostreams::detail::zlib_base::after(char const*&, char*&, bool)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0xce): undefined reference to `boost::iostreams::zlib_error::check(int)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0xdd): undefined reference to `boost::iostreams::zlib::stream_end'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0x17f): undefined reference to `boost::iostreams::detail::zlib_base::before(char const*&, char const*, char*&, char*)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl[_ZN5boost9iostreams16symmetric_filterINS0_6detail20zlib_compressor_implISaIcEEES4_E4readINS2_16linked_streambufIcSt11char_traitsIcEEEEElRT_Pcl]+0x185): undefined reference to `boost::iostreams::zlib::finish'
/usr/bin/ld: moses/bin/gcc-10/release/link-static/threading-multi/libmoses.a(BaseManager.o): in function `boost::iostreams::detail::bzip2_compressor_impl<std::allocator<char> >::close()':
BaseManager.cpp:(.text._ZN5boost9iostreams6detail21bzip2_compressor_implISaIcEE5closeEv[_ZN5boost9iostreams6detail21bzip2_compressor_implISaIcEE5closeEv]+0x13): undefined reference to `boost::iostreams::detail::bzip2_base::end(bool)'
/usr/bin/ld: moses/bin/gcc-10/release/link-static/threading-multi/libmoses.a(BaseManager.o): in function `void boost::iostreams::symmetric_filter<boost::iostreams::detail::bzip2_compressor_impl<std::allocator<char> >, std::allocator<char> >::close<boost::iostreams::non_blocking_adapter<boost::iostreams::detail::linked_streambuf<char, std::char_traits<char> > > >(boost::iostreams::non_blocking_adapter<boost::iostreams::detail::linked_streambuf<char, std::char_traits<char> > >&, std::_Ios_Openmode)':
BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x19f): undefined reference to `boost::iostreams::detail::bzip2_base::before(char const*&, char const*, char*&, char*)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1a5): undefined reference to `boost::iostreams::bzip2::finish'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1ad): undefined reference to `boost::iostreams::detail::bzip2_base::compress(int)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1bf): undefined reference to `boost::iostreams::detail::bzip2_base::after(char const*&, char*&)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1c6): undefined reference to `boost::iostreams::bzip2_error::check(int)'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1d0): undefined reference to `boost::iostreams::bzip2::stream_end'
/usr/bin/ld: BaseManager.cpp:(.text._ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode[_ZN5boost9iostreams16symmetric_filterINS0_6detail21bzip2_compressor_implISaIcEEES4_E5closeINS0_20non_blocking_adapterINS2_16linked_streambufIcSt11char_traitsIcEEEEEEEvRT_St13_Ios_Openmode]+0x1f8): undefined reference to `boost::iostreams::detail::bzip2_base::do_init(bool, void* (*)(void*, int, int), void (*)(void*, void*), void*)'
/usr/bin/ld: warning: creating DT_TEXTREL in a PIE
collect2: error: ld returned 1 exit status

    "g++"    -o "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/BackwardTest" -Wl,--start-group "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/BackwardTest.o" "util/bin/gcc-10/release/link-static/threading-multi/integer_to_string.o" "util/bin/gcc-10/release/link-static/threading-multi/pool.o" "util/bin/gcc-10/release/link-static/threading-multi/random.o" "util/bin/gcc-10/release/link-static/threading-multi/scoped.o" "util/bin/gcc-10/release/link-static/threading-multi/murmur_hash.o" "util/bin/gcc-10/release/link-static/threading-multi/usage.o" "util/bin/gcc-10/release/link-static/threading-multi/bit_packing.o" "util/bin/gcc-10/release/link-static/threading-multi/file_piece.o" "util/bin/gcc-10/release/link-static/threading-multi/string_piece.o" "util/bin/gcc-10/release/link-static/threading-multi/file.o" "util/bin/gcc-10/release/link-static/threading-multi/float_to_string.o" "lm/bin/gcc-10/release/link-static/threading-multi/config.o" "lm/bin/gcc-10/release/link-static/threading-multi/sizes.o" "lm/bin/gcc-10/release/link-static/threading-multi/lm_exception.o" "lm/bin/gcc-10/release/link-static/threading-multi/model.o" "lm/bin/gcc-10/release/link-static/threading-multi/vocab.o" "lm/bin/gcc-10/release/link-static/threading-multi/bhiksha.o" "lm/bin/gcc-10/release/link-static/threading-multi/value_build.o" "lm/bin/gcc-10/release/link-static/threading-multi/binary_format.o" "lm/bin/gcc-10/release/link-static/threading-multi/search_trie.o" "lm/bin/gcc-10/release/link-static/threading-multi/search_hashed.o" "lm/bin/gcc-10/release/link-static/threading-multi/virtual_interface.o" "lm/bin/gcc-10/release/link-static/threading-multi/quantize.o" "lm/bin/gcc-10/release/link-static/threading-multi/trie.o" "lm/bin/gcc-10/release/link-static/threading-multi/trie_sort.o" "lm/bin/gcc-10/release/link-static/threading-multi/read_arpa.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Backward.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/BackwardLMState.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Base.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/BilingualLM.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Implementation.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/InMemoryPerSentenceOnDemandLM.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Ken.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/MultiFactor.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Remote.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/SingleFactor.o" "moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/ExampleLM.o" "util/bin/gcc-10/release/link-static/threading-multi/read_compressed.o" "util/bin/gcc-10/release/link-static/threading-multi/parallel_read.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/double-conversion.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/fast-dtoa.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/bignum-dtoa.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/bignum.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/strtod.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/fixed-dtoa.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/cached-powers.o" "util/double-conversion/bin/gcc-10/release/link-static/threading-multi/diy-fp.o" "util/bin/gcc-10/release/link-static/threading-multi/mmap.o" "util/bin/gcc-10/release/link-static/threading-multi/ersatz_progress.o" "util/bin/gcc-10/release/link-static/threading-multi/exception.o" "moses/bin/gcc-10/release/link-static/threading-multi/libmoses.a" "probingpt/bin/gcc-10/release/link-static/threading-multi/libprobingpt.a"  -Wl,-Bstatic -lz -lboost_thread -lboost_system -lboost_unit_test_framework -lboost_serialization -lboost_program_options -lboost_filesystem -lboost_iostreams -lz -lboost_thread -lboost_system -Wl,-Bdynamic -lSegFault -lrt -Wl,--end-group -pthread 


...failed gcc.link moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/BackwardTest...
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest.run for lack of <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest...
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/OptimizerFactoryTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/TimerTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test.passed
Running 2 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/singleton_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/singleton_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/ngram_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/ngram_test.passed
Running 3 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/point_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/point_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/ReferenceTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test.passed
Running 2 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/timer_test
...on 1000th target...
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/timer_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/reference_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/reference_test.passed
Running 5 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/UtilTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/util_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/util_test.passed
Running 3 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/VocabularyTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test.passed
Running 2 test cases...

*** No errors detected
...failed updating 30 targets...
...skipped 32 targets...
...updated 976 targets...
The build failed.  If you need support, run:
  ./jam-files/bjam -j8 --debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
   1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
   2. Attach build.log.gz to your e-mail
   3. Say what is the EXACT command you executed when you got the error
ERROR
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

## Got Error

အပေါ်မှာ မြင်ရတဲ့အတိုင်း 

*** No errors detected
...failed updating 30 targets...
...skipped 32 targets...
...updated 976 targets...
The build failed. 

ပြီးတော့ 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/bin$ ls
1-1-Extraction  config.log        evaluator  fragment           hgdecode         lmplz        phrase-lookup                   pro            sentence-bleu        TMining
biconcor        CreateProbingPT2  extractor  gcc-10             kbmira           mert         phrase_table_vocab              query          sentence-bleu-nbest  train-expected-bleu
build_binary    dump_counts       filter     generateSequences  kenlm_benchmark  moses_chart  prepare-expected-bleu-training  queryOnDiskPt  symal

*** moses ဆိုတဲ့ binary ကို မတွေ့ဘူး။

## Install all required packages

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install subversion
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libapr1 libaprutil1 libserf-1-1 libsvn1 libutf8proc2
Suggested packages:
  db5.3-util libapache2-mod-svn subversion-tools
The following NEW packages will be installed:
  libapr1 libaprutil1 libserf-1-1 libsvn1 libutf8proc2 subversion
0 upgraded, 6 newly installed, 0 to remove and 93 not upgraded.
Need to get 2,382 kB of archives.
After this operation, 10.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libapr1 amd64 1.6.5-1ubuntu1 [91.4 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libaprutil1 amd64 1.6.1-4ubuntu2 [84.7 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libserf-1-1 amd64 1.3.9-8build1 [45.2 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libutf8proc2 amd64 2.5.0-1 [50.0 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libsvn1 amd64 1.14.0-2 [1,277 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 subversion amd64 1.14.0-2 [833 kB]
Fetched 2,382 kB in 4s (582 kB/s)   
Selecting previously unselected package libapr1:amd64.
(Reading database ... 269852 files and directories currently installed.)
Preparing to unpack .../0-libapr1_1.6.5-1ubuntu1_amd64.deb ...
Unpacking libapr1:amd64 (1.6.5-1ubuntu1) ...
Selecting previously unselected package libaprutil1:amd64.
Preparing to unpack .../1-libaprutil1_1.6.1-4ubuntu2_amd64.deb ...
Unpacking libaprutil1:amd64 (1.6.1-4ubuntu2) ...
Selecting previously unselected package libserf-1-1:amd64.
Preparing to unpack .../2-libserf-1-1_1.3.9-8build1_amd64.deb ...
Unpacking libserf-1-1:amd64 (1.3.9-8build1) ...
Selecting previously unselected package libutf8proc2:amd64.
Preparing to unpack .../3-libutf8proc2_2.5.0-1_amd64.deb ...
Unpacking libutf8proc2:amd64 (2.5.0-1) ...
Selecting previously unselected package libsvn1:amd64.
Preparing to unpack .../4-libsvn1_1.14.0-2_amd64.deb ...
Unpacking libsvn1:amd64 (1.14.0-2) ...
Selecting previously unselected package subversion.
Preparing to unpack .../5-subversion_1.14.0-2_amd64.deb ...
Unpacking subversion (1.14.0-2) ...
Setting up libutf8proc2:amd64 (2.5.0-1) ...
Setting up libapr1:amd64 (1.6.5-1ubuntu1) ...
Setting up libaprutil1:amd64 (1.6.1-4ubuntu2) ...
Setting up libserf-1-1:amd64 (1.3.9-8build1) ...
Setting up libsvn1:amd64 (1.14.0-2) ...
Setting up subversion (1.14.0-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
Processing triggers for man-db (2.9.3-2) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install zlib1g-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
zlib1g-dev is already the newest version (1:1.2.11.dfsg-2ubuntu4).
zlib1g-dev set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 93 not upgraded.

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install libicu-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  icu-devtools
Suggested packages:
  icu-doc
The following NEW packages will be installed:
  icu-devtools libicu-dev
0 upgraded, 2 newly installed, 0 to remove and 93 not upgraded.
Need to get 9,783 kB of archives.
After this operation, 46.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 icu-devtools amd64 67.1-4 [190 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libicu-dev amd64 67.1-4 [9,593 kB]
Fetched 9,783 kB in 14s (676 kB/s)                                                                                                                                                                        
Selecting previously unselected package icu-devtools.
(Reading database ... 269993 files and directories currently installed.)
Preparing to unpack .../icu-devtools_67.1-4_amd64.deb ...
Unpacking icu-devtools (67.1-4) ...
Selecting previously unselected package libicu-dev:amd64.
Preparing to unpack .../libicu-dev_67.1-4_amd64.deb ...
Unpacking libicu-dev:amd64 (67.1-4) ...
Setting up icu-devtools (67.1-4) ...
Setting up libicu-dev:amd64 (67.1-4) ...
Processing triggers for man-db (2.9.3-2) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install libboost-all-dev
...
...
...
Setting up libboost-coroutine1.71-dev:amd64 (1.71.0-6ubuntu9) ...
Setting up libboost-graph-parallel1.71.0 (1.71.0-6ubuntu9) ...
Setting up libboost-coroutine-dev:amd64 (1.71.0.0ubuntu4) ...
Setting up libboost-log-dev (1.71.0.0ubuntu4) ...
Setting up openmpi-bin (4.0.3-6ubuntu2) ...
update-alternatives: using /usr/bin/mpirun.openmpi to provide /usr/bin/mpirun (mpirun) in auto mode
update-alternatives: using /usr/bin/mpicc.openmpi to provide /usr/bin/mpicc (mpi) in auto mode
Setting up libboost-thread-dev:amd64 (1.71.0.0ubuntu4) ...
Setting up libboost-fiber-dev:amd64 (1.71.0.0ubuntu4) ...
Setting up libboost-locale1.71-dev:amd64 (1.71.0-6ubuntu9) ...
Setting up libcoarrays-dev:amd64 (2.9.0-2) ...
Setting up mpi-default-bin (1.13) ...
Setting up libboost-locale-dev:amd64 (1.71.0.0ubuntu4) ...
Setting up libcoarrays-openmpi-dev:amd64 (2.9.0-2) ...
Setting up libboost-type-erasure-dev:amd64 (1.71.0.0ubuntu4) ...
Setting up libboost-graph-parallel1.71-dev (1.71.0-6ubuntu9) ...
Setting up libopenmpi-dev:amd64 (4.0.3-6ubuntu2) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/openmpi/include to provide /usr/include/x86_64-linux-gnu/mpi (mpi-x86_64-linux-gnu) in auto mode
Setting up libboost-mpi-python1.71.0 (1.71.0-6ubuntu9) ...
Setting up libboost-graph-parallel-dev (1.71.0.0ubuntu4) ...
Setting up mpi-default-dev (1.13) ...
Setting up libboost-mpi1.71-dev (1.71.0-6ubuntu9) ...
Setting up libboost-mpi-python1.71-dev (1.71.0-6ubuntu9) ...
Setting up libboost-mpi-python-dev (1.71.0.0ubuntu4) ...
Setting up libboost-mpi-dev (1.71.0.0ubuntu4) ...
Setting up libboost-all-dev (1.71.0.0ubuntu4) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install libbz2-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  bzip2-doc
The following NEW packages will be installed:
  bzip2-doc libbz2-dev
0 upgraded, 2 newly installed, 0 to remove and 93 not upgraded.
Need to get 531 kB of archives.
After this operation, 719 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 bzip2-doc all 1.0.8-4ubuntu2 [500 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libbz2-dev amd64 1.0.8-4ubuntu2 [30.2 kB]
Fetched 531 kB in 2s (223 kB/s)       
Selecting previously unselected package bzip2-doc.
(Reading database ... 288786 files and directories currently installed.)
Preparing to unpack .../bzip2-doc_1.0.8-4ubuntu2_all.deb ...
Unpacking bzip2-doc (1.0.8-4ubuntu2) ...
Selecting previously unselected package libbz2-dev:amd64.
Preparing to unpack .../libbz2-dev_1.0.8-4ubuntu2_amd64.deb ...
Unpacking libbz2-dev:amd64 (1.0.8-4ubuntu2) ...
Setting up bzip2-doc (1.0.8-4ubuntu2) ...
Setting up libbz2-dev:amd64 (1.0.8-4ubuntu2) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
install-info: warning: no info dir entry in `/usr/share/info/automake-history.info.gz'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install liblzma-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  liblzma-doc
The following NEW packages will be installed:
  liblzma-dev
0 upgraded, 1 newly installed, 0 to remove and 93 not upgraded.
Need to get 147 kB of archives.
After this operation, 603 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 liblzma-dev amd64 5.2.4-1ubuntu1 [147 kB]
Fetched 147 kB in 2s (93.2 kB/s)      
Selecting previously unselected package liblzma-dev:amd64.
(Reading database ... 288799 files and directories currently installed.)
Preparing to unpack .../liblzma-dev_5.2.4-1ubuntu1_amd64.deb ...
Unpacking liblzma-dev:amd64 (5.2.4-1ubuntu1) ...
Setting up liblzma-dev:amd64 (5.2.4-1ubuntu1) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install python-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Note, selecting 'python-dev-is-python2' instead of 'python-dev'
The following additional packages will be installed:
  libpython2-dev libpython2-stdlib libpython2.7 libpython2.7-dev python-is-python2 python2 python2-dev python2-minimal python2.7-dev
Suggested packages:
  python2-doc python-tk
The following NEW packages will be installed:
  libpython2-dev libpython2-stdlib libpython2.7 libpython2.7-dev python-dev-is-python2 python-is-python2 python2 python2-dev python2-minimal python2.7-dev
0 upgraded, 10 newly installed, 0 to remove and 93 not upgraded.
Need to get 3,712 kB of archives.
After this operation, 17.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python2-minimal amd64 2.7.18-2 [13.5 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libpython2-stdlib amd64 2.7.18-2 [7,332 B]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python2 amd64 2.7.18-2 [9,068 B]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libpython2.7 amd64 2.7.18-1build2 [1,024 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libpython2.7-dev amd64 2.7.18-1build2 [2,358 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libpython2-dev amd64 2.7.18-2 [7,388 B]
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python-is-python2 all 2.7.17-4 [2,496 B]
Get:8 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python2.7-dev amd64 2.7.18-1build2 [287 kB]
Get:9 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python2-dev amd64 2.7.18-2 [1,264 B]
Get:10 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 python-dev-is-python2 all 2.7.17-4 [1,396 B]
Fetched 3,712 kB in 6s (657 kB/s)                  
Selecting previously unselected package python2-minimal.
(Reading database ... 288839 files and directories currently installed.)
Preparing to unpack .../python2-minimal_2.7.18-2_amd64.deb ...
Unpacking python2-minimal (2.7.18-2) ...
Selecting previously unselected package libpython2-stdlib:amd64.
Preparing to unpack .../libpython2-stdlib_2.7.18-2_amd64.deb ...
Unpacking libpython2-stdlib:amd64 (2.7.18-2) ...
Setting up python2-minimal (2.7.18-2) ...
Selecting previously unselected package python2.
(Reading database ... 288856 files and directories currently installed.)
Preparing to unpack .../0-python2_2.7.18-2_amd64.deb ...
Unpacking python2 (2.7.18-2) ...
Selecting previously unselected package libpython2.7:amd64.
Preparing to unpack .../1-libpython2.7_2.7.18-1build2_amd64.deb ...
Unpacking libpython2.7:amd64 (2.7.18-1build2) ...
Selecting previously unselected package libpython2.7-dev:amd64.
Preparing to unpack .../2-libpython2.7-dev_2.7.18-1build2_amd64.deb ...
Unpacking libpython2.7-dev:amd64 (2.7.18-1build2) ...
Selecting previously unselected package libpython2-dev:amd64.
Preparing to unpack .../3-libpython2-dev_2.7.18-2_amd64.deb ...
Unpacking libpython2-dev:amd64 (2.7.18-2) ...
Selecting previously unselected package python-is-python2.
Preparing to unpack .../4-python-is-python2_2.7.17-4_all.deb ...
Unpacking python-is-python2 (2.7.17-4) ...
Selecting previously unselected package python2.7-dev.
Preparing to unpack .../5-python2.7-dev_2.7.18-1build2_amd64.deb ...
Unpacking python2.7-dev (2.7.18-1build2) ...
Selecting previously unselected package python2-dev.
Preparing to unpack .../6-python2-dev_2.7.18-2_amd64.deb ...
Unpacking python2-dev (2.7.18-2) ...
Selecting previously unselected package python-dev-is-python2.
Preparing to unpack .../7-python-dev-is-python2_2.7.17-4_all.deb ...
Unpacking python-dev-is-python2 (2.7.17-4) ...
Setting up libpython2.7:amd64 (2.7.18-1build2) ...
Setting up libpython2.7-dev:amd64 (2.7.18-1build2) ...
Setting up libpython2-stdlib:amd64 (2.7.18-2) ...
Setting up python2 (2.7.18-2) ...
Setting up libpython2-dev:amd64 (2.7.18-2) ...
Setting up python-is-python2 (2.7.17-4) ...
Setting up python2.7-dev (2.7.18-1build2) ...
Setting up python2-dev (2.7.18-2) ...
Setting up python-dev-is-python2 (2.7.17-4) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install graphviz
Reading package lists... Done
Building dependency tree       
Reading state information... Done
graphviz is already the newest version (2.42.2-4).
0 upgraded, 0 newly installed, 0 to remove and 93 not upgraded.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install imagemagick
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  gsfonts imagemagick-6-common imagemagick-6.q16 libfftw3-double3 libilmbase25 liblqr-1-0 libmagickcore-6.q16-6 libmagickcore-6.q16-6-extra libmagickwand-6.q16-6 libnetpbm10 libopenexr25 netpbm
Suggested packages:
  imagemagick-doc autotrace enscript ffmpeg gimp gnuplot grads hp2xx html2ps libwmf-bin mplayer povray radiance transfig ufraw-batch libfftw3-bin libfftw3-dev inkscape libjxr-tools
The following NEW packages will be installed:
  gsfonts imagemagick imagemagick-6-common imagemagick-6.q16 libfftw3-double3 libilmbase25 liblqr-1-0 libmagickcore-6.q16-6 libmagickcore-6.q16-6-extra libmagickwand-6.q16-6 libnetpbm10 libopenexr25
  netpbm
0 upgraded, 13 newly installed, 0 to remove and 93 not upgraded.
Need to get 8,178 kB of archives.
After this operation, 25.7 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libfftw3-double3 amd64 3.3.8-2ubuntu6 [727 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 liblqr-1-0 amd64 0.4.2-2.1 [27.7 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 imagemagick-6-common all 8:6.9.10.23+dfsg-2.1ubuntu13.1 [60.8 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 libmagickcore-6.q16-6 amd64 8:6.9.10.23+dfsg-2.1ubuntu13.1 [1,649 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 libmagickwand-6.q16-6 amd64 8:6.9.10.23+dfsg-2.1ubuntu13.1 [300 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 gsfonts all 1:8.11+urwcyr1.0.7~pre44-4.4 [3,120 kB]
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 imagemagick-6.q16 amd64 8:6.9.10.23+dfsg-2.1ubuntu13.1 [427 kB]                                                                   
Get:8 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 imagemagick amd64 8:6.9.10.23+dfsg-2.1ubuntu13.1 [14.4 kB]                                                                        
Get:9 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libilmbase25 amd64 2.5.3-2 [118 kB]                                                                                                       
Get:10 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libopenexr25 amd64 2.5.3-2 [593 kB]                                                                                                      
Get:11 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 libmagickcore-6.q16-6-extra amd64 8:6.9.10.23+dfsg-2.1ubuntu13.1 [64.7 kB]                                                       
Get:12 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libnetpbm10 amd64 2:10.0-15.3build1 [58.0 kB]                                                                                            
Get:13 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 netpbm amd64 2:10.0-15.3build1 [1,017 kB]                                                                                                
Fetched 8,178 kB in 12s (685 kB/s)                                                                                                                                                                        
Selecting previously unselected package libfftw3-double3:amd64.
(Reading database ... 289019 files and directories currently installed.)
Preparing to unpack .../00-libfftw3-double3_3.3.8-2ubuntu6_amd64.deb ...
Unpacking libfftw3-double3:amd64 (3.3.8-2ubuntu6) ...
Selecting previously unselected package liblqr-1-0:amd64.
Preparing to unpack .../01-liblqr-1-0_0.4.2-2.1_amd64.deb ...
Unpacking liblqr-1-0:amd64 (0.4.2-2.1) ...
Selecting previously unselected package imagemagick-6-common.
Preparing to unpack .../02-imagemagick-6-common_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_all.deb ...
Unpacking imagemagick-6-common (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package libmagickcore-6.q16-6:amd64.
Preparing to unpack .../03-libmagickcore-6.q16-6_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_amd64.deb ...
Unpacking libmagickcore-6.q16-6:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package libmagickwand-6.q16-6:amd64.
Preparing to unpack .../04-libmagickwand-6.q16-6_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_amd64.deb ...
Unpacking libmagickwand-6.q16-6:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package gsfonts.
Preparing to unpack .../05-gsfonts_1%3a8.11+urwcyr1.0.7~pre44-4.4_all.deb ...
Unpacking gsfonts (1:8.11+urwcyr1.0.7~pre44-4.4) ...
Selecting previously unselected package imagemagick-6.q16.
Preparing to unpack .../06-imagemagick-6.q16_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_amd64.deb ...
Unpacking imagemagick-6.q16 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package imagemagick.
Preparing to unpack .../07-imagemagick_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_amd64.deb ...
Unpacking imagemagick (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package libilmbase25:amd64.
Preparing to unpack .../08-libilmbase25_2.5.3-2_amd64.deb ...
Unpacking libilmbase25:amd64 (2.5.3-2) ...
Selecting previously unselected package libopenexr25:amd64.
Preparing to unpack .../09-libopenexr25_2.5.3-2_amd64.deb ...
Unpacking libopenexr25:amd64 (2.5.3-2) ...
Selecting previously unselected package libmagickcore-6.q16-6-extra:amd64.
Preparing to unpack .../10-libmagickcore-6.q16-6-extra_8%3a6.9.10.23+dfsg-2.1ubuntu13.1_amd64.deb ...
Unpacking libmagickcore-6.q16-6-extra:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Selecting previously unselected package libnetpbm10.
Preparing to unpack .../11-libnetpbm10_2%3a10.0-15.3build1_amd64.deb ...
Unpacking libnetpbm10 (2:10.0-15.3build1) ...
Selecting previously unselected package netpbm.
Preparing to unpack .../12-netpbm_2%3a10.0-15.3build1_amd64.deb ...
Unpacking netpbm (2:10.0-15.3build1) ...
Setting up imagemagick-6-common (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Setting up libilmbase25:amd64 (2.5.3-2) ...
Setting up libnetpbm10 (2:10.0-15.3build1) ...
Setting up libopenexr25:amd64 (2.5.3-2) ...
Setting up gsfonts (1:8.11+urwcyr1.0.7~pre44-4.4) ...
Setting up netpbm (2:10.0-15.3build1) ...
Setting up libfftw3-double3:amd64 (3.3.8-2ubuntu6) ...
Setting up liblqr-1-0:amd64 (0.4.2-2.1) ...
Setting up libmagickcore-6.q16-6:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Setting up libmagickwand-6.q16-6:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Setting up libmagickcore-6.q16-6-extra:amd64 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Setting up imagemagick-6.q16 (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
update-alternatives: using /usr/bin/compare-im6.q16 to provide /usr/bin/compare (compare) in auto mode
update-alternatives: using /usr/bin/compare-im6.q16 to provide /usr/bin/compare-im6 (compare-im6) in auto mode
update-alternatives: using /usr/bin/animate-im6.q16 to provide /usr/bin/animate (animate) in auto mode
update-alternatives: using /usr/bin/animate-im6.q16 to provide /usr/bin/animate-im6 (animate-im6) in auto mode
update-alternatives: using /usr/bin/convert-im6.q16 to provide /usr/bin/convert (convert) in auto mode
update-alternatives: using /usr/bin/convert-im6.q16 to provide /usr/bin/convert-im6 (convert-im6) in auto mode
update-alternatives: using /usr/bin/composite-im6.q16 to provide /usr/bin/composite (composite) in auto mode
update-alternatives: using /usr/bin/composite-im6.q16 to provide /usr/bin/composite-im6 (composite-im6) in auto mode
update-alternatives: using /usr/bin/conjure-im6.q16 to provide /usr/bin/conjure (conjure) in auto mode
update-alternatives: using /usr/bin/conjure-im6.q16 to provide /usr/bin/conjure-im6 (conjure-im6) in auto mode
update-alternatives: using /usr/bin/import-im6.q16 to provide /usr/bin/import (import) in auto mode
update-alternatives: using /usr/bin/import-im6.q16 to provide /usr/bin/import-im6 (import-im6) in auto mode
update-alternatives: using /usr/bin/identify-im6.q16 to provide /usr/bin/identify (identify) in auto mode
update-alternatives: using /usr/bin/identify-im6.q16 to provide /usr/bin/identify-im6 (identify-im6) in auto mode
update-alternatives: using /usr/bin/stream-im6.q16 to provide /usr/bin/stream (stream) in auto mode
update-alternatives: using /usr/bin/stream-im6.q16 to provide /usr/bin/stream-im6 (stream-im6) in auto mode
update-alternatives: using /usr/bin/display-im6.q16 to provide /usr/bin/display (display) in auto mode
update-alternatives: using /usr/bin/display-im6.q16 to provide /usr/bin/display-im6 (display-im6) in auto mode
update-alternatives: using /usr/bin/montage-im6.q16 to provide /usr/bin/montage (montage) in auto mode
update-alternatives: using /usr/bin/montage-im6.q16 to provide /usr/bin/montage-im6 (montage-im6) in auto mode
update-alternatives: using /usr/bin/mogrify-im6.q16 to provide /usr/bin/mogrify (mogrify) in auto mode
update-alternatives: using /usr/bin/mogrify-im6.q16 to provide /usr/bin/mogrify-im6 (mogrify-im6) in auto mode
Setting up imagemagick (8:6.9.10.23+dfsg-2.1ubuntu13.1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu4) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for fontconfig (2.13.1-2ubuntu3) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

တချို့ package တွေက စက်ထဲမှာ ရှိတာသိတယ်။
သို့သော် update မဖြစ်ရင် သိချင်လို့ ...
နောက် စက်ထဲမှာ သုံးခဲ့တဲ့ version ကိုလည်း ခင်ဗျားတို့ကို သိစေချင်လို့...

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install make
Reading package lists... Done
Building dependency tree       
Reading state information... Done
make is already the newest version (4.3-4ubuntu1).
make set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 93 not upgraded.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install cmake
Reading package lists... Done
Building dependency tree       
Reading state information... Done
cmake is already the newest version (3.16.3-3ubuntu2).
0 upgraded, 0 newly installed, 0 to remove and 93 not upgraded.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install libgoogle-perftools-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libgoogle-perftools4 libtcmalloc-minimal4 libunwind-dev
The following NEW packages will be installed:
  libgoogle-perftools-dev libgoogle-perftools4 libtcmalloc-minimal4 libunwind-dev
0 upgraded, 4 newly installed, 0 to remove and 93 not upgraded.
Need to get 1,138 kB of archives.
After this operation, 8,373 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libtcmalloc-minimal4 amd64 2.7-1ubuntu6 [90.2 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libgoogle-perftools4 amd64 2.7-1ubuntu6 [189 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libunwind-dev amd64 1.3.2-2 [421 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libgoogle-perftools-dev amd64 2.7-1ubuntu6 [438 kB]
Fetched 1,138 kB in 3s (349 kB/s)                
Selecting previously unselected package libtcmalloc-minimal4:amd64.
(Reading database ... 290021 files and directories currently installed.)
Preparing to unpack .../libtcmalloc-minimal4_2.7-1ubuntu6_amd64.deb ...
Unpacking libtcmalloc-minimal4:amd64 (2.7-1ubuntu6) ...
Selecting previously unselected package libgoogle-perftools4:amd64.
Preparing to unpack .../libgoogle-perftools4_2.7-1ubuntu6_amd64.deb ...
Unpacking libgoogle-perftools4:amd64 (2.7-1ubuntu6) ...
Selecting previously unselected package libunwind-dev:amd64.
Preparing to unpack .../libunwind-dev_1.3.2-2_amd64.deb ...
Unpacking libunwind-dev:amd64 (1.3.2-2) ...
Selecting previously unselected package libgoogle-perftools-dev:amd64.
Preparing to unpack .../libgoogle-perftools-dev_2.7-1ubuntu6_amd64.deb ...
Unpacking libgoogle-perftools-dev:amd64 (2.7-1ubuntu6) ...
Setting up libunwind-dev:amd64 (1.3.2-2) ...
Setting up libtcmalloc-minimal4:amd64 (2.7-1ubuntu6) ...
Setting up libgoogle-perftools4:amd64 (2.7-1ubuntu6) ...
Setting up libgoogle-perftools-dev:amd64 (2.7-1ubuntu6) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install autoconf
Reading package lists... Done
Building dependency tree       
Reading state information... Done
autoconf is already the newest version (2.69-11.1).
autoconf set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 93 not upgraded.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install doxygen
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libclang1-10 libllvm10 libxapian30
Suggested packages:
  doxygen-latex doxygen-doc doxygen-gui xapian-tools
The following NEW packages will be installed:
  doxygen libclang1-10 libllvm10 libxapian30
0 upgraded, 4 newly installed, 0 to remove and 93 not upgraded.
Need to get 33.7 MB of archives.
After this operation, 157 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libllvm10 amd64 1:10.0.1-6 [16.4 MB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libclang1-10 amd64 1:10.0.1-6 [7,250 kB]                                                                                                  
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libxapian30 amd64 1.4.17-1 [664 kB]                                                                                                       
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 doxygen amd64 1.8.18-1ubuntu3 [9,465 kB]                                                                                                  
Fetched 33.7 MB in 53s (637 kB/s)                                                                                                                                                                         
Selecting previously unselected package libllvm10:amd64.
(Reading database ... 290183 files and directories currently installed.)
Preparing to unpack .../libllvm10_1%3a10.0.1-6_amd64.deb ...
Unpacking libllvm10:amd64 (1:10.0.1-6) ...
Selecting previously unselected package libclang1-10.
Preparing to unpack .../libclang1-10_1%3a10.0.1-6_amd64.deb ...
Unpacking libclang1-10 (1:10.0.1-6) ...
Selecting previously unselected package libxapian30:amd64.
Preparing to unpack .../libxapian30_1.4.17-1_amd64.deb ...
Unpacking libxapian30:amd64 (1.4.17-1) ...
Selecting previously unselected package doxygen.
Preparing to unpack .../doxygen_1.8.18-1ubuntu3_amd64.deb ...
Unpacking doxygen (1.8.18-1ubuntu3) ...
Setting up libxapian30:amd64 (1.4.17-1) ...
Setting up libllvm10:amd64 (1:10.0.1-6) ...
Setting up libclang1-10 (1:10.0.1-6) ...
Setting up doxygen (1.8.18-1ubuntu3) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$

## Run bjam again with some more parameters

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$time ./bjam --with-boost=/home/ye/tool/boost_1_75_0 --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8
...
...
...skipped <p/home/ye/tool/mosesdecoder/lib>libmoses.a for lack of <pmoses/bin/gcc-10/release/link-static/threading-multi>libmoses.a...
...skipped <pmoses/bin/gcc-10/release/link-static/threading-multi>moses_test for lack of <pmoses/bin/gcc-10/release/link-static/threading-multi>libmoses.a...
...skipped <pmoses/bin/gcc-10/release/link-static/threading-multi>moses_test.passed for lack of <pmoses/bin/gcc-10/release/link-static/threading-multi>moses_test...
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest for lack of <pmoses/LM/bin/gcc-10/release/link-static/threading-multi>SRI.o...
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest.run for lack of <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest...
...failed updating 2 targets...
...skipped 73 targets...
...updated 11 targets...
The build failed.  If you need support, run:
  ./jam-files/bjam --with-boost=/home/ye/tool/boost_1_75_0 --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 --debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
   1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
   2. Attach build.log.gz to your e-mail
   3. Say what is the EXACT command you executed when you got the error
ERROR

real	0m8.643s
user	0m13.800s
sys	0m0.893s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

## clean and rebuild

./bjam --clean

after that,
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ time ./bjam  --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -a
...
...
...
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
In file included from ./moses/TranslationTask.h:8,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:6:
./moses/IOWrapper.h:108:8: warning: ‘template<class> class std::auto_ptr’ is deprecated [-Wdeprecated-declarations]
  108 |   std::auto_ptr<Moses::OutputCollector> m_detailTreeFragmentsOutputCollector;
      |        ^~~~~~~~
In file included from /usr/include/c++/10/memory:83,
                 from /usr/local/include/boost/smart_ptr/detail/sp_counted_impl.hpp:35,
                 from /usr/local/include/boost/smart_ptr/detail/shared_count.hpp:27,
                 from /usr/local/include/boost/smart_ptr/shared_ptr.hpp:17,
                 from /usr/local/include/boost/shared_ptr.hpp:17,
                 from ./moses/TypeDef.h:29,
                 from ./moses/Factor.h:26,
                 from moses/LM/Implementation.h:26,
                 from moses/LM/SingleFactor.h:24,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.h:6,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:2:
/usr/include/c++/10/bits/unique_ptr.h:57:28: note: declared here
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
In file included from ./moses/TranslationTask.h:10,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:6:
./moses/ChartManager.h:48:8: warning: ‘template<class> class std::auto_ptr’ is deprecated [-Wdeprecated-declarations]
   48 |   std::auto_ptr<SentenceStats> m_sentenceStats;
      |        ^~~~~~~~
In file included from /usr/include/c++/10/memory:83,
                 from /usr/local/include/boost/smart_ptr/detail/sp_counted_impl.hpp:35,
                 from /usr/local/include/boost/smart_ptr/detail/shared_count.hpp:27,
                 from /usr/local/include/boost/smart_ptr/shared_ptr.hpp:17,
                 from /usr/local/include/boost/shared_ptr.hpp:17,
                 from ./moses/TypeDef.h:29,
                 from ./moses/Factor.h:26,
                 from moses/LM/Implementation.h:26,
                 from moses/LM/SingleFactor.h:24,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.h:6,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:2:
/usr/include/c++/10/bits/unique_ptr.h:57:28: note: declared here
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
In file included from ./moses/TranslationTask.h:10,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:6:
./moses/ChartManager.h: In member function ‘void Moses::ChartManager::ResetSentenceStats(const Moses::InputType&)’:
./moses/ChartManager.h:131:28: warning: ‘template<class> class std::auto_ptr’ is deprecated [-Wdeprecated-declarations]
  131 |     m_sentenceStats = std::auto_ptr<SentenceStats>(new SentenceStats(source));
      |                            ^~~~~~~~
In file included from /usr/include/c++/10/memory:83,
                 from /usr/local/include/boost/smart_ptr/detail/sp_counted_impl.hpp:35,
                 from /usr/local/include/boost/smart_ptr/detail/shared_count.hpp:27,
                 from /usr/local/include/boost/smart_ptr/shared_ptr.hpp:17,
                 from /usr/local/include/boost/shared_ptr.hpp:17,
                 from ./moses/TypeDef.h:29,
                 from ./moses/Factor.h:26,
                 from moses/LM/Implementation.h:26,
                 from moses/LM/SingleFactor.h:24,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.h:6,
                 from moses/LM/InMemoryPerSentenceOnDemandLM.cpp:2:
/usr/include/c++/10/bits/unique_ptr.h:57:28: note: declared here
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/HypergraphTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/BleuScorerTest.o
In file included from mert/BleuScorer.h:13,
                 from mert/BleuScorerTest.cpp:1:
mert/StatisticsBasedScorer.h: In member function ‘virtual float MosesTuning::StatisticsBasedScorer::getReferenceLength(const std::vector<float>&) const’:
mert/StatisticsBasedScorer.h:47:86: warning: no return statement in function returning non-void [-Wreturn-type]
   47 |   virtual float getReferenceLength(const std::vector<ScoreStatsType>& totals) const {}
      |                                                                                      ^
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/hypergraph_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/hypergraph_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/DataTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/FeatureDataTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/bleu_scorer_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/bleu_scorer_test.passed
Running 6 test cases...
name: reflen value: average
name: reflen value: shortest

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/data_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/data_test.passed
Running 3 test cases...
Data::m_score_type BLEU
Data::Scorer type from Scorer: BLEU
Data::m_score_type BLEU
Data::Scorer type from Scorer: BLEU
Data::m_score_type BLEU
Data::Scorer type from Scorer: BLEU
Data::m_score_type BLEU
Data::Scorer type from Scorer: BLEU
Data::m_score_type BLEU
Data::Scorer type from Scorer: BLEU

*** No errors detected
gcc.compile.c++ moses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi/Ken.o
In file included from ./lm/model.hh:13,
                 from moses/LM/Ken.cpp:30:
./lm/vocab.hh:210:43: warning: dynamic exception specifications are deprecated in C++11 [-Wdeprecated]
  210 | void MissingUnknown(const Config &config) throw(SpecialWordMissingException);
      |                                           ^~~~~
./lm/vocab.hh:211:67: warning: dynamic exception specifications are deprecated in C++11 [-Wdeprecated]
  211 | void MissingSentenceMarker(const Config &config, const char *str) throw(SpecialWordMissingException);
      |                                                                   ^~~~~
./lm/vocab.hh:213:85: warning: dynamic exception specifications are deprecated in C++11 [-Wdeprecated]
  213 | template <class Vocab> void CheckSpecials(const Config &config, const Vocab &vocab) throw(SpecialWordMissingException) {
      |                                                                                     ^~~~~
moses/LM/Ken.cpp: In member function ‘virtual Moses::FFState* Moses::LanguageModelKen<Model>::EvaluateWhenApplied(const Moses::Hypothesis&, const Moses::FFState*, Moses::ScoreComponentCollection*) const’:
moses/LM/Ken.cpp:201:8: warning: ‘template<class> class std::auto_ptr’ is deprecated [-Wdeprecated-declarations]
  201 |   std::auto_ptr<KenLMState> ret(new KenLMState());
      |        ^~~~~~~~
In file included from /usr/include/c++/10/memory:83,
                 from moses/LM/Ken.cpp:22:
/usr/include/c++/10/bits/unique_ptr.h:57:28: note: declared here
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/feature_data_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/feature_data_test.passed
Running 1 test case...

*** No errors detected
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest for lack of <pmoses/LM/bin/gcc-10/release/link-static/threading-multi>SRI.o...
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest.run for lack of <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest...
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/ForestRescoreTest.o
In file included from mert/BleuScorer.h:13,
                 from mert/ForestRescore.h:27,
                 from mert/ForestRescoreTest.cpp:5:
mert/StatisticsBasedScorer.h: In member function ‘virtual float MosesTuning::StatisticsBasedScorer::getReferenceLength(const std::vector<float>&) const’:
mert/StatisticsBasedScorer.h:47:86: warning: no return statement in function returning non-void [-Wreturn-type]
   47 |   virtual float getReferenceLength(const std::vector<ScoreStatsType>& totals) const {}
      |                                                                                      ^
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test.passed
Running 2 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/MiraFeatureVectorTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/NgramTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/SingletonTest.o
common.copy mert/mert
common.copy mert/extractor
common.copy mert/evaluator
common.copy mert/pro
...skipped <pmert>kbmira for lack of <pmert/bin/gcc-10/release/link-static/threading-multi>kbmira...
common.copy mert/sentence-bleu
common.copy mert/sentence-bleu-nbest
...skipped <pmert>hgdecode for lack of <pmert/bin/gcc-10/release/link-static/threading-multi>hgdecode...
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/ngram_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/ngram_test.passed
Running 3 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/TimerTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/singleton_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/singleton_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/timer_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/timer_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/OptimizerFactoryTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/PointTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test.passed
Running 2 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/point_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/point_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/ReferenceTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/reference_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/reference_test.passed
Running 5 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/UtilTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/util_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/util_test.passed
Running 3 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/VocabularyTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test.passed
Running 2 test cases...

*** No errors detected
...failed updating 5 targets...
...skipped 78 targets...
...updated 764 targets...
The build failed.  If you need support, run:
  ./jam-files/bjam --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -a --debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
   1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
   2. Attach build.log.gz to your e-mail
   3. Say what is the EXACT command you executed when you got the error
ERROR

real	3m44.076s
user	27m13.047s
sys	1m27.699s

/bin/ အောက်မှာ moses command လည်း မရှိလို့ Error!!!

## Install other dependencies

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ sudo apt-get install libsoap-lite-perl
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libclass-inspector-perl libconvert-binhex-perl libfcgi-perl libio-sessiondata-perl libmime-tools-perl libossp-uuid-perl libossp-uuid16 libtask-weaken-perl libxmlrpc-lite-perl
Suggested packages:
  uuid libapache2-mod-perl2 libmime-lite-perl libnet-jabber-perl
The following NEW packages will be installed:
  libclass-inspector-perl libconvert-binhex-perl libfcgi-perl libio-sessiondata-perl libmime-tools-perl libossp-uuid-perl libossp-uuid16 libsoap-lite-perl libtask-weaken-perl libxmlrpc-lite-perl
0 upgraded, 10 newly installed, 0 to remove and 93 not upgraded.
Need to get 591 kB of archives.
After this operation, 1,778 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libclass-inspector-perl all 1.36-1 [16.3 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libconvert-binhex-perl all 1.125-1 [29.7 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libfcgi-perl amd64 0.79-1 [33.1 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libio-sessiondata-perl all 1.03-1 [5,606 B]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libmime-tools-perl all 5.509-1 [192 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libossp-uuid16 amd64 1.6.2-1.5build7 [28.4 kB]
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libossp-uuid-perl amd64 1.6.2-1.5build7 [18.6 kB]
Get:8 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libtask-weaken-perl all 1.06-1 [8,700 B]
Get:9 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libsoap-lite-perl all 1.27-1 [236 kB]
Get:10 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libxmlrpc-lite-perl all 0.717-4 [22.5 kB]
Fetched 591 kB in 2s (332 kB/s)                 
Selecting previously unselected package libclass-inspector-perl.
(Reading database ... 290267 files and directories currently installed.)
Preparing to unpack .../0-libclass-inspector-perl_1.36-1_all.deb ...
Unpacking libclass-inspector-perl (1.36-1) ...
Selecting previously unselected package libconvert-binhex-perl.
Preparing to unpack .../1-libconvert-binhex-perl_1.125-1_all.deb ...
Unpacking libconvert-binhex-perl (1.125-1) ...
Selecting previously unselected package libfcgi-perl.
Preparing to unpack .../2-libfcgi-perl_0.79-1_amd64.deb ...
Unpacking libfcgi-perl (0.79-1) ...
Selecting previously unselected package libio-sessiondata-perl.
Preparing to unpack .../3-libio-sessiondata-perl_1.03-1_all.deb ...
Unpacking libio-sessiondata-perl (1.03-1) ...
Selecting previously unselected package libmime-tools-perl.
Preparing to unpack .../4-libmime-tools-perl_5.509-1_all.deb ...
Unpacking libmime-tools-perl (5.509-1) ...
Selecting previously unselected package libossp-uuid16:amd64.
Preparing to unpack .../5-libossp-uuid16_1.6.2-1.5build7_amd64.deb ...
Unpacking libossp-uuid16:amd64 (1.6.2-1.5build7) ...
Selecting previously unselected package libossp-uuid-perl.
Preparing to unpack .../6-libossp-uuid-perl_1.6.2-1.5build7_amd64.deb ...
Unpacking libossp-uuid-perl (1.6.2-1.5build7) ...
Selecting previously unselected package libtask-weaken-perl.
Preparing to unpack .../7-libtask-weaken-perl_1.06-1_all.deb ...
Unpacking libtask-weaken-perl (1.06-1) ...
Selecting previously unselected package libsoap-lite-perl.
Preparing to unpack .../8-libsoap-lite-perl_1.27-1_all.deb ...
Unpacking libsoap-lite-perl (1.27-1) ...
Selecting previously unselected package libxmlrpc-lite-perl.
Preparing to unpack .../9-libxmlrpc-lite-perl_0.717-4_all.deb ...
Unpacking libxmlrpc-lite-perl (0.717-4) ...
Setting up libio-sessiondata-perl (1.03-1) ...
Setting up libtask-weaken-perl (1.06-1) ...
Setting up libclass-inspector-perl (1.36-1) ...
Setting up libconvert-binhex-perl (1.125-1) ...
Setting up libossp-uuid16:amd64 (1.6.2-1.5build7) ...
Setting up libmime-tools-perl (5.509-1) ...
Setting up libfcgi-perl (0.79-1) ...
Setting up libossp-uuid-perl (1.6.2-1.5build7) ...
Setting up libsoap-lite-perl (1.27-1) ...
Setting up libxmlrpc-lite-perl (0.717-4) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ 

wget http://www.achrafothman.net/aslsmt/tools/cmph_2.0.orig.tar.gz
tar zxvf cmph_2.0.orig.tar.gz
cd cmph-2.0/
./configure
make
make install

wget http://www.achrafothman.net/aslsmt/tools/xmlrpc-c_1.33.14.orig.tar.gz
tar zxvf xmlrpc-c_1.33.14.orig.tar.gz
cd xmlrpc-c-1.33.14/
./configure
make
make install

## clean and run bjam again

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ ./bjam --clean
XMLRPC-C: USING VERSION 1.33.14 FROM /usr/local
BUILDING MOSES SERVER!
Performing configuration checks

    - Shared Boost             : yes
    - Static Boost             : yes
Building Moses2
...found 1 target...
...updating 1 target...
common.Clean clean
...updated 1 target...

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ time ./bjam  --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -a
...
...
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test.passed
Running 2 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/point_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/point_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/timer_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/timer_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/reference_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/reference_test.passed
Running 5 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/util_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/util_test.passed
Running 3 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test.passed
Running 2 test cases...

*** No errors detected
...failed updating 6 targets...
...skipped 75 targets...
...updated 934 targets...
The build failed.  If you need support, run:
  ./jam-files/bjam --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -a --debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
   1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
   2. Attach build.log.gz to your e-mail
   3. Say what is the EXACT command you executed when you got the error
ERROR

real	4m47.875s
user	34m52.430s
sys	1m54.282s

## Retry

time ./bjam  --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -a
...
...
...
In file included from /usr/include/c++/10/memory:83,
                 from moses/LM/Ken.cpp:22:
/usr/include/c++/10/bits/unique_ptr.h:57:28: note: declared here
   57 |   template<typename> class auto_ptr;
      |                            ^~~~~~~~
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/hypergraph_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/hypergraph_test.passed
Running 1 test case...

*** No errors detected
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest for lack of <pmoses/LM/bin/gcc-10/release/link-static/threading-multi>SRI.o...
...skipped <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest.run for lack of <pmoses/LM/bin/BackwardTest.test/gcc-10/release/link-static/threading-multi>BackwardTest...
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/ForestRescoreTest.o
In file included from mert/BleuScorer.h:13,
                 from mert/ForestRescore.h:27,
                 from mert/ForestRescoreTest.cpp:5:
mert/StatisticsBasedScorer.h: In member function ‘virtual float MosesTuning::StatisticsBasedScorer::getReferenceLength(const std::vector<float>&) const’:
mert/StatisticsBasedScorer.h:47:86: warning: no return statement in function returning non-void [-Wreturn-type]
   47 |   virtual float getReferenceLength(const std::vector<ScoreStatsType>& totals) const {}
      |                                                                                      ^
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/forest_rescore_test.passed
Running 2 test cases...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/MiraFeatureVectorTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/mira_feature_vector_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/SingletonTest.o
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/singleton_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/singleton_test.passed
Running 1 test case...

*** No errors detected
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/NgramTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/TimerTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/PointTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/OptimizerFactoryTest.o
gcc.link mert/mert
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/ngram_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/ngram_test.passed
Running 3 test cases...

*** No errors detected
gcc.link mert/extractor
gcc.link mert/evaluator
gcc.link mert/pro
gcc.link mert/kbmira
gcc.link mert/sentence-bleu
...on 900th target...
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/ReferenceTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/UtilTest.o
gcc.compile.c++ mert/bin/gcc-10/release/link-static/threading-multi/VocabularyTest.o
gcc.link mert/sentence-bleu-nbest
gcc.link mert/hgdecode
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/timer_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/timer_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/point_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/point_test.passed
Running 1 test case...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/optimizer_factory_test.passed
Running 2 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/reference_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/reference_test.passed
Running 5 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/util_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/util_test.passed
Running 3 test cases...

*** No errors detected
gcc.link mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test
testing.unit-test mert/bin/gcc-10/release/link-static/threading-multi/vocabulary_test.passed
Running 2 test cases...

*** No errors detected
...failed updating 6 targets...
...skipped 75 targets...
...updated 907 targets...
The build failed.  If you need support, run:
  ./jam-files/bjam --with-irstlm=/home/ye/tool/irstlm --with-srilm=/home/ye/tool/srilm-1.7.3/bin/i686-m64 -j8 -–with-cmph=/home/ye/tool/cmph-2.0 -a --debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
   1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
   2. Attach build.log.gz to your e-mail
   3. Say what is the EXACT command you executed when you got the error
ERROR

real	4m55.006s
user	34m54.304s
sys	1m53.954s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

ဒီတစ်ခါတော့ moses2 binary ထွက်လာတယ်။

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ cd bin
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/bin$ ls
biconcor      config.log        dump_counts  extractor  fragment  hgdecode  kenlm_benchmark  mert    moses_chart    phrase_table_vocab              pro    sentence-bleu        symal
build_binary  CreateProbingPT2  evaluator    filter     gcc-10    kbmira    lmplz            moses2  phrase-lookup  prepare-expected-bleu-training  query  sentence-bleu-nbest  train-expected-bleu
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/bin$ ./moses2 --help
Starting...
Moses - A beam search decoder for phrase-based statistical machine translation models
Copyright (C) 2006 University of Edinburgh

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA

***********************************************************************

Built on Feb  8 2021 at 06:28:41

WHO'S FAULT IS THIS GODDAM SOFTWARE:
Alexandra Constantin   eu sunt varza
Chris Callison-Burch	   contact: anytime, anywhere   international playboy
Brooke Cowan	   contact: brooke@csail.mit.edu   if you're going to san francisco, be sure to wear a flower in your hair
Ondrej Bojar   czech this out!
Richard Zens	   contact: richard at aachen dot de   I'll answer question on: ambiguous source input, confusion networks, confusing source code
Christine Moran	   contact: weird building at MIT
Philipp Koehn	   contact: only between 2 and 4am   I'll answer question on: Nothing fazes this dude
Hieu Hoang	   contact: http://www.hoang.co.uk/hieu/   phd student at Edinburgh Uni. Original Moses developer   I'll answer question on: general queries/ flames on Moses.
Marcello Federico	   contact: federico at itc at it   Researcher at ITC-irst, Trento, Italy   I'll answer question on: IRST language model
Nicola Bertoldi	   contact: 911   I'll answer question on: scripts & other stuff
Evan Herbst	   contact: Small college in upstate New York
Chris Dyer	   contact: can't. i'll be out driving my mustang   driving my mustang
Wade Shen	   contact: via morse code   buying another laptop


Usage:

Main Options:
  -f [ --config ]                  location of the configuration file
  -i [ --input-file ]              location of the input file to be translated
  -v [ --verbose ]                 verbosity level of the logging
  --show-weights                   print feature weights and exit

Moses Server Options:
  --server                         Run moses as a translation server.
  --server-port                    Port for moses server
  --server-log                     Log destination for moses server
  --serial                         Run server in serial mode, processing only 
                                   one request at a time.
  --server-maxconn                 Max. No of simultaneous HTTP transactions 
                                   allowed by the server.
  --server-maxconn-backlog         Max. No. of requests the OS will queue if 
                                   the server is busy.
  --server-keepalive-maxconn       Max. No. of requests the server will accept 
                                   on a single TCP connection.
  --server-keepalive-timeout       Max. number of seconds the server will keep 
                                   a persistent connection alive.
  --server-timeout                 Max. number of seconds the server will wait 
                                   for a client to submit a request once a 
                                   connection has been established.

Input Format Options:
  --input-factors                  list of factors in the input
  --inputtype                      text (0), confusion network (1), word 
                                   lattice (2), tree (3) (default = 0)
  --xml-input                      allows markup of input with desired 
                                   translations and probabilities. values can 
                                   be 'pass-through' (default), 'inclusive', 
                                   'exclusive', 'constraint', 'ignore'

Search Options:
  --search-algorithm               Which search algorithm to use.
                                   0=normal stack (default)
                                   1=cube pruning
                                   3=chart (with cube pruning)
                                   4=stack with batched lm requests
                                   5=chart (with incremental search)
                                   6=string-to-tree
                                   7=tree-to-string
                                   8=tree-to-string (SCFG-based)
                                   9=forest-to-string
  -b [ --beam-threshold ]          threshold for threshold pruning
  -s [ --stack ]                   maximum stack size for histogram pruning. 0 
                                   = unlimited stack size
  --weight                         weights for ALL models, 1 per line 
                                   'WeightName value'. Weight names can be 
                                   repeated
  --feature-overwrite              Override arguments in a particular feature 
                                   function with a particular key. Format: 
                                   -feature-overwrite "FeatureName key=value"
  --max-phrase-length              maximum phrase length (default 20)
  --threads                        number of threads to use in decoding 
                                   (defaults to single-threaded)

Cube pruning options.:
  --cube-pruning-pop-limit         How many hypotheses should be popped for 
                                   each stack. (default = 1000)
  --cube-pruning-diversity         How many hypotheses should be created for 
                                   each coverage. (default = 0)
  --cube-pruning-lazy-scoring      Don't fully score a hypothesis until it is 
                                   popped

Distortion options:
  --distortion-limit               distortion (reordering) limit in maximum 
                                   number of words (0 = monotone, -1 = 
                                   unlimited)
  --monotone-at-punctuation        do not reorder over punctuation

Chart Decoding Options:
  --max-chart-span                 maximum num. of source word chart rules can 
                                   consume (default 10)
  --non-terminals                  list of non-term symbols, space separated

Output Options:
  --output-factors                 list if factors in the output
  -T [ --translation-details ]     for each best hypothesis, report translation
                                   details to the given file
  --output-hypo-score              Output the hypo score to stdout with the 
                                   output string. For search error analysis. 
                                   Default is false
  -t [ --report-segmentation ]     report phrase segmentation in the output
  --report-segmentation-enriched   report phrase segmentation in the output 
                                   with additional information

N-best Options:
  --n-best-list                    file and size of n-best-list to be 
                                   generated; specify - as the file in order to
                                   write to STDOUT
  --n-best-factor                  factor to compute the maximum number of 
                                   contenders (=factor*nbest-size). value 0 
                                   means infinity, i.e. no threshold. default 
                                   is 0

OOV Handling Options:
  --drop-unknown                   drop unknown words instead of copying them
  --mark-unknown                   mark unknown words in output
  --unknown-word-prefix            prefix to unknwon word when marked (default:
                                   'UNK')
  --unknown-word-suffix            suffix to unknwon word when marked (default:
                                   '')

General Factorization Options:
  --mapping                        description of decoding steps
  --placeholder-factor             Which source factor to use to store the 
                                   original text for placeholders. The factor 
                                   must not be used by a translation or gen 
                                   model

Options used in tuning.:
  --weight-overwrite               special parameter for mert. All on 1 line. 
                                   Overrides weights specified in 'weights' 
                                   argument
  --feature-add                    Add a feature function on the command line. 
                                   Used by mira to add BLEU feature
  --weight-add                     Add weight for FF if it doesn't exist, i.e 
                                   weights here are added 1st, and can be 
                                   override by the ini file or on the command 
                                   line. Used to specify initial weights for FF
                                   that was also specified on the copmmand line

Miscellaneous Options:
  --decoding-graph-backoff         only use subsequent decoding paths for 
                                   unknown spans of given length
  --feature                        All the feature functions should be here
  --cpu-affinity-offset            CPU Affinity. Default = -1 (no affinity)
  --cpu-affinity-increment         Set to 1 (default) to put each thread on 
                                   different cores. 0 to run all threads on one
                                   core

Available feature functions:
Distortion ExampleStatefulFF ExampleStatelessFF GPULM KENLM KENLMBatch LanguageModel LexicalReordering MSPT OpSequenceModel PhraseDictionaryMemory PhraseDictionaryTransliteration PhrasePenalty ProbingPT UnknownWordPenalty WordPenalty 

No configuration file was specified.  Use -config or -f
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/bin$ 

######################
######################
## Download Sample Models

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ wget http://www.statmt.org/moses/download/sample-models.tgz
--2021-02-08 02:09:28--  http://www.statmt.org/moses/download/sample-models.tgz
Resolving www.statmt.org (www.statmt.org)... 129.215.197.184
Connecting to www.statmt.org (www.statmt.org)|129.215.197.184|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10956904 (10M) [application/x-gzip]
Saving to: ‘sample-models.tgz’

sample-models.tgz                                  100%[===============================================================================================================>]  10.45M   166KB/s    in 65s     

2021-02-08 02:10:34 (165 KB/s) - ‘sample-models.tgz’ saved [10956904/10956904]

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

## ls and tar

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ ls
biconcor  bjam        contrib  cruise-control  doc           jam-files  lib  mert   misc   moses2     OnDiskPt        previous.sh  README              run-regtests.sh    scripts  symal  vw
bin       compile.sh  COPYING  defer           doxygen.conf  Jamroot    lm   mingw  moses  moses-cmd  phrase-extract  probingpt    regression-testing  sample-models.tgz  search   util

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ tar xzf sample-models.tgz

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$ ls
biconcor  bjam        contrib  cruise-control  doc           jam-files  lib  mert   misc   moses2     OnDiskPt        previous.sh  README              run-regtests.sh  sample-models.tgz  search  util
bin       compile.sh  COPYING  defer           doxygen.conf  Jamroot    lm   mingw  moses  moses-cmd  phrase-extract  probingpt    regression-testing  sample-models    scripts            symal   vw
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ ls
lm  phrase-model  string-to-tree  tree-to-tree

## Testing the decoder

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ cat ./phrase-model/in 
das ist ein kleines haus
das ist ein kleines haus

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ ../bin/moses2 -f phrase-model/moses.ini < phrase-model/in > out
Starting...
Defined parameters (per moses.ini or switch):
	config: phrase-model/moses.ini 
	feature: KENLM name=LM factor=0 order=3 num-features=1 path=lm/europarl.srilm.gz Distortion WordPenalty UnknownWordPenalty PhraseDictionaryMemory input-factor=0 output-factor=0 path=phrase-model/phrase-table num-features=1 table-limit=10 
	input-factors: 0 
	mapping: T 0 
	n-best-list: nbest.txt 100 
	weight: WordPenalty0= 0 LM= 1 Distortion0= 1 PhraseDictionaryMemory0= 1 
START featureFunctions.Load()
Loading LM
Finished loading LM
Loading Distortion0
Finished loading Distortion0
Loading WordPenalty0
Finished loading WordPenalty0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading PhraseDictionaryMemory0
Finished loading PhraseDictionaryMemory0
START LoadMappings()
END LoadMappings()
END LoadDecodeGraphBackoff()
Loaded : [0.403846] seconds
RUN BATCH
Decoding took 0.406174
Finished

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ wc out
 2 10 46 out

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ cat out
this is a small house 
this is a small house 

## String to Tree Translation

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ cat ./string-to-tree/in
das ist ein kleines haus
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ ../bin/moses2 -f string-to-tree/moses.ini < string-to-tree/in > out.stt
Starting...
Defined parameters (per moses.ini or switch):
	config: string-to-tree/moses.ini 
	cube-pruning-pop-limit: 1000 
	feature: KENLM name=LM factor=0 order=3 num-features=1 path=lm/europarl.srilm.gz WordPenalty UnknownWordPenalty PhraseDictionaryMemory input-factor=0 output-factor=0 path=string-to-tree/rule-table num-features=1 table-limit=20 
	input-factors: 0 
	inputtype: 3 
	mapping: 0 T 0 
	max-chart-span: 20 1000 
	non-terminals: X S 
	search-algorithm: 3 
	translation-details: translation-details.log 
	weight: WordPenalty0= 0 LM= 0.5 PhraseDictionaryMemory0= 0.5 
START featureFunctions.Load()
Loading LM
Finished loading LM
Loading WordPenalty0
Finished loading WordPenalty0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading PhraseDictionaryMemory0
Finished loading PhraseDictionaryMemory0
START LoadMappings()
END LoadMappings()
END LoadDecodeGraphBackoff()
Loaded : [0.412322] seconds
RUN BATCH
Decoding took 0.412893
Finished
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ cat out.stt 
this is a small house

## Tree to Tree Translation

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ ../bin/moses2 -f tree-to-tree/moses.ini < tree-to-tree/in.xml > out.ttt
Starting...
Defined parameters (per moses.ini or switch):
	config: tree-to-tree/moses.ini 
	cube-pruning-pop-limit: 1000 
	feature: WordPenalty UnknownWordPenalty PhraseDictionaryMemory input-factor=0 output-factor=0 path=tree-to-tree/rule-table num-features=5 table-limit=20 PhraseDictionaryMemory input-factor=0 output-factor=0 path=tree-to-tree/glue num-features=1 table-limit=20 
	input-factors: 0 
	inputtype: 3 
	mapping: 0 T 0 1 T 1 
	max-chart-span: 20 1000 
	non-terminals: X S 
	search-algorithm: 3 
	translation-details: translation-details.log 
	weight: WordPenalty0= 0 PhraseDictionaryMemory0= 0.5 0.5 0.5 0.5 0.5 PhraseDictionaryMemory1= -0.5 
START featureFunctions.Load()
Loading WordPenalty0
Finished loading WordPenalty0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading PhraseDictionaryMemory0
Finished loading PhraseDictionaryMemory0
Loading PhraseDictionaryMemory1
Finished loading PhraseDictionaryMemory1
START LoadMappings()
END LoadMappings()
END LoadDecodeGraphBackoff()
Loaded : [0.000714271] seconds
RUN BATCH
Decoding took 0.0016255
Finished
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesdecoder/sample-models$ cat ./out.ttt 
<tree label="TOP"><tree label="OS">overhead</tree> <tree label="NS">oxygen</tree> <tree label="NS">masks</tree> in the <tree label="NS">cabin <tree label="NS">section</tree></tree> <tree label="OS">had dropped into place .</tree></tree>

## Note

PBSMT ကို training မလုပ်ခင်မှာ...
GIZA++ သို့မဟုတ် mgizapp ကို လည်း install လုပ်ဖို့ မမေ့နဲ့အုံး။

## Reference

https://achrafothman.net/site/how-to-install-moses-statistical-machine-translation-in-ubuntu/
https://github.com/artetxem/monoses/issues/12

