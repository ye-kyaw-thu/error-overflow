# ESPnet Installation Note

## git clone ESPnet

```
(base) rnd@gpu:~/tool$ git clone https://github.com/espnet/espnet
Cloning into 'espnet'...
remote: Enumerating objects: 194932, done.
remote: Total 194932 (delta 0), reused 0 (delta 0), pack-reused 194932
Receiving objects: 100% (194932/194932), 669.42 MiB | 13.22 MiB/s, done.
Resolving deltas: 100% (139637/139637), done.
(base) rnd@gpu:~/tool$ 
```

## git clone Kaldi

ESPnet 1 ကို သုံးမယ် ဆိုရင် Kaldi က လိုအပ်တာမို့လို့ ...  

```
(base) rnd@gpu:~/tool$ git clone https://github.com/kaldi-asr/kaldi.git
Cloning into 'kaldi'...
remote: Enumerating objects: 115158, done.
remote: Total 115158 (delta 0), reused 0 (delta 0), pack-reused 115158
Receiving objects: 100% (115158/115158), 121.90 MiB | 12.49 MiB/s, done.
Resolving deltas: 100% (88752/88752), done.
(base) rnd@gpu:~/tool$ 
```

## Create a New Anaconda Environment

```
(base) rnd@gpu:~/tool$ cd espnet/tools/
(base) rnd@gpu:~/tool/espnet/tools$ ls
Makefile   check_install.py  installers              setup_anaconda.sh  setup_python.sh
README.md  extra_path.sh     sentencepiece_commands  setup_cuda_env.sh  setup_venv.sh
(base) rnd@gpu:~/tool/espnet/tools$
```

Anaconda Environment က လက်ရှိ GPU စက်မှာ ရှိပြီးသားမို့လို့ Option A) Setup conda environment ဆိုတာကို skip လုပ်ခဲ့တယ်။  

```
(base) rnd@gpu:~/tool/espnet/tools$ echo $CONDA_EXE
/home/rnd/anaconda3/bin/conda
(base) rnd@gpu:~/tool/espnet/tools$
```

espnet ဆိုတဲ့ နာမည်နဲ့ env အသစ်ကို အောက်ပါအတိုင်း create လုပ်ခဲ့တယ်...  

```
(base) rnd@gpu:~/tool/espnet/tools$ conda create --name espnet python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/rnd/anaconda3/envs/espnet

  added / updated specs:
    - python=3.8


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.01.10-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2022.12.7-py38h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.2-h6a678d5_6
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-1.1.1t-h7f8727e_0
  pip                pkgs/main/linux-64::pip-23.0.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.16-h7a1cb2a_3
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-65.6.3-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.1-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.38.4-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.2.10-h5eee18b_1
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate espnet
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) rnd@gpu:~/tool/espnet/tools$ conda activate espnet
(espnet) rnd@gpu:~/tool/espnet/tools$
```

Python version ကိုလည်း စစ်ကြည့်ခဲ့ ...  

```
(espnet) rnd@gpu:~/tool/espnet/tools$ python --version
Python 3.8.16
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

## Installation of ESPnet

```
(espnet) rnd@gpu:~/tool/espnet/tools$ make
test -f activate_python.sh || { echo "Error: Run ./setup_python.sh or ./setup_anaconda.sh"; exit 1; }
Error: Run ./setup_python.sh or ./setup_anaconda.sh
make: *** [Makefile:35: activate_python.sh] Error 1
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

အထက်ပါအတိုင်း Error ပေး ....  

## Setup Python Environment

ဒီအဆင့်က မလုပ်လို့ မရ ...  

```
(espnet) rnd@gpu:~/tool/espnet/tools$ ./setup_python.sh $(command -v python3)
Warning: Setting PYTHONUSERBASE
Requirement already satisfied: pip in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (23.0.1)
Requirement already satisfied: wheel in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (0.38.4)
Collecting wheel
  Using cached wheel-0.40.0-py3-none-any.whl (64 kB)
Installing collected packages: wheel
  Attempting uninstall: wheel
    Found existing installation: wheel 0.38.4
    Uninstalling wheel-0.38.4:
      Successfully uninstalled wheel-0.38.4
Successfully installed wheel-0.40.0
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

## Installation of ESPnet

```
(espnet) rnd@gpu:~/tool/espnet/tools$ make
INFO:
Use 'installers/install_warp-transducer.sh' to install warprnnt_pytorch
Use 'installers/install_chainer_ctc.sh' to install chainer_ctc
Use 'installers/install_pyopenjtalk.sh' to install pyopenjtalk
Use 'installers/install_tdmelodic_pyopenjtalk.sh' to install tdmelodic_pyopenjtalk
Use 'installers/install_kenlm.sh' to install kenlm
Use 'installers/install_py3mmseg.sh' to install mmseg
Use 'installers/install_fairseq.sh' to install fairseq
Use 'installers/install_phonemizer.sh' to install phonemizer
Use 'installers/install_gtn.sh' to install gtn
Use 'installers/install_s3prl.sh' to install s3prl
Use 'installers/install_transformers.sh' to install transformers
Use 'installers/install_speechbrain.sh' to install speechbrain
Use 'installers/install_k2.sh' to install k2
Use 'installers/install_longformer.sh' to install longformer
Use 'installers/install_longformer.sh' to install nlg-eval
Use 'installers/install_longformer.sh' to install datasets
Use 'installers/install_cauchy_mult.sh' to install pykeops
Use 'installers/install_whisper.sh' to install whisper
Use 'installers/install_rawnet.sh' to install RawNet3
Use 'installers/install_reazonspeech.sh' to install reazonspeech
Use 'installers/install_muskits.sh' to install muskits
Type 'git clone --depth 1 https://github.com/kaldi-asr/kaldi' and see 'kaldi/tools/INSTALL' to install Kaldi
Use 'installers/install_pesq.sh' to install PESQ
Use 'installers/install_beamformit.sh' to install BeamformIt
(espnet) rnd@gpu:~/tool/espnet/tools$
```

## Install Custom Tools

```
(espnet) rnd@gpu:~/tool/espnet/tools$ . activate_python.sh 
(espnet) rnd@gpu:~/tool/espnet/tools$ . ./setup_cuda_env.sh /usr/local/cuda
CUDA_HOME=/usr/local/cuda
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

```
(espnet) rnd@gpu:~/tool/espnet/tools$ ./installers/install_warp-transducer.sh
...
...
...
[ 57%] Linking CXX executable test_gpu
[ 57%] Built target test_gpu
[ 64%] Building CXX object CMakeFiles/test_cpu.dir/tests/test_cpu.cpp.o
/home/rnd/tool/espnet/tools/warp-transducer/tests/test_cpu.cpp: In function ‘float numeric_grad(std::vector<float>&, std::vector<int>&, std::vector<int>&, std::vector<int>, int, int, void*, rnntOptions&, std::vector<float>&)’:
/home/rnd/tool/espnet/tools/warp-transducer/tests/test_cpu.cpp:285:1: warning: no return statement in function returning non-void [-Wreturn-type]
 }
 ^
[ 71%] Building CXX object CMakeFiles/test_cpu.dir/tests/random.cpp.o
[ 78%] Linking CXX executable test_cpu
[ 78%] Built target test_cpu
[ 85%] Building CXX object CMakeFiles/test_time.dir/tests/test_time.cpp.o
/home/rnd/tool/espnet/tools/warp-transducer/tests/test_time.cpp: In function ‘bool run_test(int, int, int, int, int)’:
/home/rnd/tool/espnet/tools/warp-transducer/tests/test_time.cpp:25:35: warning: control reaches end of non-void function [-Wreturn-type]
     std::vector<std::vector<int>> labels;
                                   ^~~~~~
[ 92%] Building CXX object CMakeFiles/test_time.dir/tests/random.cpp.o
[100%] Linking CXX executable test_time
[100%] Built target test_time
Obtaining file:///home/rnd/tool/espnet/tools/warp-transducer/pytorch_binding
  Preparing metadata (setup.py) ... done
Installing collected packages: warprnnt-pytorch
  Running setup.py develop for warprnnt-pytorch
Successfully installed warprnnt-pytorch-0.1
(espnet) rnd@gpu:~/tool/espnet/tools$
```

PyOpenJtalk ကိုလည်း installation လုပ်ကြည့်ခဲ့ ...  

```
(espnet) rnd@gpu:~/tool/espnet/tools$ ./installers/install_pyopenjtalk.sh
...
...
...
Collecting pyopenjtalk==0.3.0
  Downloading pyopenjtalk-0.3.0.tar.gz (1.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 8.3 MB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Requirement already satisfied: cython>=0.21.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from pyopenjtalk==0.3.0) (0.29.33)
Requirement already satisfied: numpy>=1.20.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from pyopenjtalk==0.3.0) (1.23.5)
Requirement already satisfied: six in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from pyopenjtalk==0.3.0) (1.16.0)
Requirement already satisfied: tqdm in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from pyopenjtalk==0.3.0) (4.65.0)
Building wheels for collected packages: pyopenjtalk
  Building wheel for pyopenjtalk (pyproject.toml) ... done
  Created wheel for pyopenjtalk: filename=pyopenjtalk-0.3.0-cp38-cp38-linux_x86_64.whl size=6125277 sha256=b5d1022c70e28a9e82ab949a13f0eeebdf0e7ed05cbd1b75a8d6debd9db7f115
  Stored in directory: /home/rnd/.cache/pip/wheels/88/74/65/3fffc9c6c6a4b625cd5108d4e42e599d6aee5fcf02b1480119
Successfully built pyopenjtalk
Installing collected packages: pyopenjtalk
Successfully installed pyopenjtalk-0.3.0
Downloading: "https://github.com/r9y9/open_jtalk/releases/download/v1.11.1/open_jtalk_dic_utf_8-1.11.tar.gz"
dic.tar.gz: 100%|████████████████████████████████████████████████| 22.6M/22.6M [00:40<00:00, 583kB/s]
Extracting tar file /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages/pyopenjtalk/dic.tar.gz
(espnet) rnd@gpu:~/tool/espnet/tools$
```

## Check ESPnet Installation 

```
(espnet) rnd@gpu:~/tool/espnet/tools$ bash -c ". ./activate_python.sh; . ./extra_path.sh; python3 check_install.py" | tee check_install.log
/home/rnd/tool/espnet/tools/chainer/chainer/backends/cuda.py:142: UserWarning: cuDNN is not enabled.
Please reinstall CuPy after you install cudnn
(see https://docs-cupy.chainer.org/en/stable/install.html#install-cudnn).
  warnings.warn(
[x] python=3.8.16 (default, Mar  2 2023, 03:21:46)  [GCC 11.2.0]

Python modules:
[x] torch=1.13.1+cu117
[x] torch cuda=11.7
[x] torch cudnn=8500
[x] torch nccl
[x] chainer=6.0.0
[x] chainer cuda
[ ] chainer cudnn
[x] cupy=6.0.0
[ ] cupy nccl
[x] torchaudio=0.13.1+cu117
[x] torch_optimizer=0.3.0
[x] warprnnt_pytorch
[ ] chainer_ctc
[x] pyopenjtalk=0.3.0
[ ] tdmelodic_pyopenjtalk
[ ] kenlm
[ ] mmseg
[x] espnet=202301
[x] numpy=1.23.5
[ ] fairseq
[ ] phonemizer
[ ] gtn
[ ] s3prl
[ ] transformers
[ ] speechbrain
[ ] k2
[ ] longformer
[ ] nlg-eval
[ ] datasets
[ ] pykeops
[ ] whisper
[ ] RawNet3
[ ] reazonspeech
[ ] muskits
[ ] Kaldi

Executables:
[x] sclite
[x] sph2pipe
[ ] PESQ
[ ] BeamformIt
[x] spm_train
[x] spm_encode
[x] spm_decode
[x] sox=14.4.2
[x] ffmpeg=6.0
[ ] flac
[x] cmake=3.26.0

INFO:
Use 'installers/install_chainer_ctc.sh' to install chainer_ctc
Use 'installers/install_tdmelodic_pyopenjtalk.sh' to install tdmelodic_pyopenjtalk
Use 'installers/install_kenlm.sh' to install kenlm
Use 'installers/install_py3mmseg.sh' to install mmseg
Use 'installers/install_fairseq.sh' to install fairseq
Use 'installers/install_phonemizer.sh' to install phonemizer
Use 'installers/install_gtn.sh' to install gtn
Use 'installers/install_s3prl.sh' to install s3prl
Use 'installers/install_transformers.sh' to install transformers
Use 'installers/install_speechbrain.sh' to install speechbrain
Use 'installers/install_k2.sh' to install k2
Use 'installers/install_longformer.sh' to install longformer
Use 'installers/install_longformer.sh' to install nlg-eval
Use 'installers/install_longformer.sh' to install datasets
Use 'installers/install_cauchy_mult.sh' to install pykeops
Use 'installers/install_whisper.sh' to install whisper
Use 'installers/install_rawnet.sh' to install RawNet3
Use 'installers/install_reazonspeech.sh' to install reazonspeech
Use 'installers/install_muskits.sh' to install muskits
Type 'git clone --depth 1 https://github.com/kaldi-asr/kaldi' and see 'kaldi/tools/INSTALL' to install Kaldi
Use 'installers/install_pesq.sh' to install PESQ
Use 'installers/install_beamformit.sh' to install BeamformIt
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

## Installation of Some More Tools for ESPnet

### Beamformit

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_beamformit.sh
...
...
...
In file included from /usr/include/stdio.h:867,
                 from /usr/include/c++/8/cstdio:42,
                 from /usr/include/c++/8/ext/string_conversions.h:43,
                 from /usr/include/c++/8/bits/basic_string.h:6400,
                 from /usr/include/c++/8/string:52,
                 from /home/rnd/tool/espnet/tools/installers/BeamformIt/includes/global.h:5,
                 from /home/rnd/tool/espnet/tools/installers/BeamformIt/includes/fileinout.h:4,
                 from /home/rnd/tool/espnet/tools/installers/BeamformIt/src/fileinout.cc:3:
/usr/include/x86_64-linux-gnu/bits/stdio2.h:67:35: note: ‘__builtin___snprintf_chk’ output 33 or more bytes (assuming 1056) into a destination of size 1024
   return __builtin___snprintf_chk (__s, __n, __USE_FORTIFY_LEVEL - 1,
          ~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        __bos (__s), __fmt, __va_arg_pack ());
        ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
[ 57%] Building CXX object CMakeFiles/BeamformIt.dir/src/parse_options.cc.o
[ 71%] Building CXX object CMakeFiles/BeamformIt.dir/src/support.cc.o
[ 85%] Building CXX object CMakeFiles/BeamformIt.dir/src/tdoa.cc.o
/home/rnd/tool/espnet/tools/installers/BeamformIt/src/tdoa.cc: In member function ‘void TDOA::continuity_filter()’:
/home/rnd/tool/espnet/tools/installers/BeamformIt/src/tdoa.cc:1322:7: warning: variable ‘CONTINUOUS_DELAY’ set but not used [-Wunused-but-set-variable]
   int CONTINUOUS_DELAY ;
       ^~~~~~~~~~~~~~~~
[100%] Linking CXX executable BeamformIt
[100%] Built target BeamformIt
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### Fairscale

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_fairscale.sh 
[INFO] torch_version=1.13.1+cu117
Requirement already satisfied: fairscale in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (0.4.13)
Requirement already satisfied: torch>=1.8.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairscale) (1.13.1+cu117)
Requirement already satisfied: numpy>=1.22.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairscale) (1.23.5)
Requirement already satisfied: typing-extensions in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from torch>=1.8.0->fairscale) (4.5.0)
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### FairSequence

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_fairseq.sh 
[INFO] torch_version=1.13.1+cu117
Cloning into 'fairseq'...
remote: Enumerating objects: 34534, done.
remote: Total 34534 (delta 0), reused 0 (delta 0), pack-reused 34534
Receiving objects: 100% (34534/34534), 24.06 MiB | 9.10 MiB/s, done.
Resolving deltas: 100% (25109/25109), done.
Switched to a new branch 'sync_commit'
Obtaining file:///home/rnd/tool/espnet/tools/installers/fairseq
  Installing build dependencies ... done
  Checking if build backend supports build_editable ... done
  Getting requirements to build editable ... done
  Installing backend dependencies ... done
  Preparing editable metadata (pyproject.toml) ... done
Collecting omegaconf<2.1
  Downloading omegaconf-2.0.6-py3-none-any.whl (36 kB)
Requirement already satisfied: torch in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (1.13.1+cu117)
Requirement already satisfied: cffi in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (1.15.1)
Requirement already satisfied: regex in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (2023.3.23)
Requirement already satisfied: sacrebleu>=1.4.12 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (2.3.1)
Requirement already satisfied: cython in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (0.29.33)
Requirement already satisfied: tqdm in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (4.65.0)
Requirement already satisfied: numpy in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from fairseq==1.0.0a0+313ff05) (1.23.5)
Collecting hydra-core<1.1
  Downloading hydra_core-1.0.7-py3-none-any.whl (123 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 123.8/123.8 kB 1.8 MB/s eta 0:00:00
Collecting antlr4-python3-runtime==4.8
  Downloading antlr4-python3-runtime-4.8.tar.gz (112 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 112.4/112.4 kB 2.8 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Requirement already satisfied: importlib-resources in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from hydra-core<1.1->fairseq==1.0.0a0+313ff05) (5.12.0)
Requirement already satisfied: PyYAML>=5.1.* in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from omegaconf<2.1->fairseq==1.0.0a0+313ff05) (6.0)
Requirement already satisfied: typing-extensions in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from omegaconf<2.1->fairseq==1.0.0a0+313ff05) (4.5.0)
Requirement already satisfied: colorama in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from sacrebleu>=1.4.12->fairseq==1.0.0a0+313ff05) (0.4.6)
Requirement already satisfied: tabulate>=0.8.9 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from sacrebleu>=1.4.12->fairseq==1.0.0a0+313ff05) (0.9.0)
Requirement already satisfied: portalocker in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from sacrebleu>=1.4.12->fairseq==1.0.0a0+313ff05) (2.7.0)
Requirement already satisfied: lxml in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from sacrebleu>=1.4.12->fairseq==1.0.0a0+313ff05) (4.9.2)
Requirement already satisfied: pycparser in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from cffi->fairseq==1.0.0a0+313ff05) (2.21)
Requirement already satisfied: zipp>=3.1.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from importlib-resources->hydra-core<1.1->fairseq==1.0.0a0+313ff05) (3.15.0)
Building wheels for collected packages: fairseq, antlr4-python3-runtime
  Building editable for fairseq (pyproject.toml) ... done
  Created wheel for fairseq: filename=fairseq-1.0.0a0+313ff05-0.editable-cp38-cp38-linux_x86_64.whl size=8653 sha256=ca3afe2e8a5eae5e355f2974791c01dc1fea2f9612888ede31393f8ed2032f41
  Stored in directory: /tmp/pip-ephem-wheel-cache-5y47c5uq/wheels/9e/51/1c/79e10226bf272c196552d72ae00854f2c363eafafbfe58d826
  Building wheel for antlr4-python3-runtime (setup.py) ... done
  Created wheel for antlr4-python3-runtime: filename=antlr4_python3_runtime-4.8-py3-none-any.whl size=141210 sha256=3f8014e4fb49269bd70a90daab22d67765c533c2297ef674cc3876e29cd1ecfd
  Stored in directory: /home/rnd/.cache/pip/wheels/c8/d0/ab/d43c02eaddc5b9004db86950802442ad9a26f279c619e28da0
Successfully built fairseq antlr4-python3-runtime
Installing collected packages: antlr4-python3-runtime, omegaconf, hydra-core, fairseq
  Attempting uninstall: antlr4-python3-runtime
    Found existing installation: antlr4-python3-runtime 4.9.3
    Uninstalling antlr4-python3-runtime-4.9.3:
      Successfully uninstalled antlr4-python3-runtime-4.9.3
  Attempting uninstall: omegaconf
    Found existing installation: omegaconf 2.3.0
    Uninstalling omegaconf-2.3.0:
      Successfully uninstalled omegaconf-2.3.0
  Attempting uninstall: hydra-core
    Found existing installation: hydra-core 1.3.2
    Uninstalling hydra-core-1.3.2:
      Successfully uninstalled hydra-core-1.3.2
Successfully installed antlr4-python3-runtime-4.8 fairseq-1.0.0a0+313ff05 hydra-core-1.0.7 omegaconf-2.0.6
Requirement already satisfied: filelock in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (3.10.6)
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### ffmpeg

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_ffmpeg.sh
...
...
...
ffmpeg-6.0-amd64-static/model/other_models/vmaf_v0.6.1mfz.json
ffmpeg-6.0-amd64-static/model/other_models/nflxall_vmafv3a.pkl
ffmpeg-6.0-amd64-static/model/other_models/nflxall_vmafv1.pkl.model
ffmpeg-6.0-amd64-static/model/other_models/nflxall_vmafv3.pkl
ffmpeg-6.0-amd64-static/model/other_models/nflxtrain_libsvmnusvr_currentbest.pkl
ffmpeg-6.0-amd64-static/model/other_models/nflxall_libsvmnusvr_currentbest.pkl
ffmpeg-6.0-amd64-static/model/other_models/nflx_vmaff_rf_v1.pkl
ffmpeg-6.0-amd64-static/model/other_models/nflxtrain_vmafv2.pkl.model
ffmpeg-6.0-amd64-static/model/other_models/nflxall_vmafv2.pkl
ffmpeg-6.0-amd64-static/model/other_models/model_V8a.model
ffmpeg-6.0-amd64-static/model/other_models/nflxtrain_norm_type_none.pkl.model
ffmpeg-6.0-amd64-static/model/other_models/nflxtrain_vmafv3a.pkl.model
ffmpeg-6.0-amd64-static/model/other_models/nflxall_vmafv3a.pkl.model
ffmpeg-6.0-amd64-static/model/other_models/nflxtrain_norm_type_none.json
ffmpeg-6.0-amd64-static/model/vmaf_float_v0.6.1.pkl.model
ffmpeg-6.0-amd64-static/readme.txt
ffmpeg-6.0-amd64-static/ffmpeg
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### GSS

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_gss.sh
...
...
...
  Downloading numpy-1.22.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.9/16.9 MB 14.5 MB/s eta 0:00:00
Requirement already satisfied: cffi>=1.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from SoundFile>=0.10->lhotse->gss==0.6.1) (1.15.1)
Requirement already satisfied: pycparser in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from cffi>=1.0->SoundFile>=0.10->lhotse->gss==0.6.1) (2.21)
Building wheels for collected packages: gss, intervaltree
  Building wheel for gss (setup.py) ... done
  Created wheel for gss: filename=gss-0.6.1-py3-none-any.whl size=40330 sha256=df3dd1c2a97b48c4566c4c24c9a218b83c9aa336b9bac42b8254386d248f4f12
  Stored in directory: /tmp/pip-ephem-wheel-cache-2ibre38z/wheels/09/1c/59/a4eee13aeaaef317d14149cadc7b76873edddf857bdfa7d295
  Building wheel for intervaltree (setup.py) ... done
  Created wheel for intervaltree: filename=intervaltree-3.1.0-py2.py3-none-any.whl size=26099 sha256=615bfa050a78eb2f4bb42b479cddffc277cffa3c3ffe6fdb17dd28561c312f0c
  Stored in directory: /home/rnd/.cache/pip/wheels/45/23/de/5789a92962483fd33cb06674792b9697c1b3766d7c7742830e
Successfully built gss intervaltree
Installing collected packages: sortedcontainers, dataclasses, cached_property, toolz, numpy, intervaltree, lilcom, cytoolz, lhotse, gss
  Attempting uninstall: numpy
    Found existing installation: numpy 1.23.5
    Uninstalling numpy-1.23.5:
      Successfully uninstalled numpy-1.23.5
Successfully installed cached_property-1.5.2 cytoolz-0.12.1 dataclasses-0.6 gss-0.6.1 intervaltree-3.1.0 lhotse-1.13.0 lilcom-1.6 numpy-1.22.4 sortedcontainers-2.4.0 toolz-0.12.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### gtn

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_gtn.sh 
Collecting gtn==0.0.0
  Downloading gtn-0.0.0.tar.gz (45 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.9/45.9 kB 520.4 kB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: gtn
  Building wheel for gtn (setup.py) ... done
  Created wheel for gtn: filename=gtn-0.0.0-cp38-cp38-linux_x86_64.whl size=566410 sha256=88a52e0975710ed6ae9c849fd1e9a3b22329e47754c2bb9aefe50852ffabdea7
  Stored in directory: /home/rnd/.cache/pip/wheels/e1/8e/fa/f19e40c5750bc992a5214c96123a1c19a92082fe6d45605da2
Successfully built gtn
Installing collected packages: gtn
Successfully installed gtn-0.0.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### k2

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_k2.sh 
[INFO] torch_version=1.13.1
[INFO] cuda_version=11.7
[INFO] libc_version=2.31
[WARNING] k2=1.10.dev20211112 for pip doesn't provide pytorch=1.13.1 binary. Skip k2-installation
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

pytorch version 1.13.1 နဲ့ မကိုက်လို့ skip လုပ်ခဲ့လိုက် ...  

### kenlm

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_kenlm.sh 
...
...
...
[ 88%] Building CXX object lm/builder/CMakeFiles/count_ngrams.dir/count_ngrams_main.cc.o
[ 90%] Linking CXX executable ../../bin/count_ngrams
[ 90%] Built target count_ngrams
[ 91%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/arpa_io.cc.o
[ 92%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/phrase.cc.o
[ 93%] Building CXX object lm/filter/CMakeFiles/kenlm_filter.dir/vocab.cc.o
[ 95%] Linking CXX static library ../../lib/libkenlm_filter.a
[ 95%] Built target kenlm_filter
[ 96%] Building CXX object lm/filter/CMakeFiles/filter.dir/filter_main.cc.o
[ 97%] Linking CXX executable ../../bin/filter
[ 97%] Built target filter
[ 98%] Building CXX object lm/filter/CMakeFiles/phrase_table_vocab.dir/phrase_table_vocab_main.cc.o
[100%] Linking CXX executable ../../bin/phrase_table_vocab
[100%] Built target phrase_table_vocab
Obtaining file:///home/rnd/tool/espnet/tools/installers/kenlm
  Installing build dependencies ... done
  Checking if build backend supports build_editable ... done
  Getting requirements to build editable ... done
  Preparing editable metadata (pyproject.toml) ... done
Building wheels for collected packages: kenlm
  Building editable for kenlm (pyproject.toml) ... done
  Created wheel for kenlm: filename=kenlm-0.0.0-0.editable-cp38-cp38-linux_x86_64.whl size=27724 sha256=1a8e4bc50754c2b03c7b748c1a761b1860df049e32cdd0e7564841e536abe2cb
  Stored in directory: /tmp/pip-ephem-wheel-cache-fd423jmk/wheels/22/94/3b/b9c30c06ea6e8d20961a547297e93774f57c45ce831ae8d127
Successfully built kenlm
Installing collected packages: kenlm
Successfully installed kenlm-0.0.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### longformer

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_longformer.sh
...
...
...
Requirement already satisfied: click in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from nltk>=3.4.5->nlg-eval==2.3) (8.1.3)
Requirement already satisfied: regex>=2021.8.3 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from nltk>=3.4.5->nlg-eval==2.3) (2023.3.23)
Requirement already satisfied: certifi>=2017.4.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests>=2.19->nlg-eval==2.3) (2022.12.7)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests>=2.19->nlg-eval==2.3) (1.26.15)
Requirement already satisfied: idna<4,>=2.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests>=2.19->nlg-eval==2.3) (3.4)
Requirement already satisfied: charset-normalizer<4,>=2 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests>=2.19->nlg-eval==2.3) (3.1.0)
Requirement already satisfied: threadpoolctl>=2.0.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from scikit-learn>=0.17->nlg-eval==2.3) (3.1.0)
Building wheels for collected packages: nlg-eval, Theano
  Building wheel for nlg-eval (setup.py) ... done
  Created wheel for nlg-eval: filename=nlg_eval-2.3-py3-none-any.whl size=68175144 sha256=e9909029f9d62b7f1e7c76ff42b0e8246d2bf302070cfc38563a4ca2bf46a581
  Stored in directory: /tmp/pip-ephem-wheel-cache-_2kbgw5_/wheels/66/f8/6f/2c77f60dc21872b5dcf58ff66b00a7e77721098b04e12191c9
  Building wheel for Theano (setup.py) ... done
  Created wheel for Theano: filename=Theano-1.0.5-py3-none-any.whl size=2668109 sha256=f6bc72ddb779dcd56505b5e2ecc12ceeb74c2465086f9270a8cd0e6348bdb147
  Stored in directory: /home/rnd/.cache/pip/wheels/84/cb/19/235b5b10d89b4621f685112f8762681570a9fa14dc1ce904d9
Successfully built nlg-eval Theano
Installing collected packages: xdg, smart-open, Theano, gensim, nlg-eval
Successfully installed Theano-1.0.5 gensim-3.8.3 nlg-eval-2.3 smart-open-6.3.0 xdg-6.0.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### muskits.sh

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_muskits.sh
...
...
...
site-packages (from matplotlib->music21) (2.8.2)
Requirement already satisfied: pillow>=6.2.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (9.4.0)
Requirement already satisfied: fonttools>=4.22.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (4.39.2)
Requirement already satisfied: packaging>=20.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (23.0)
Requirement already satisfied: pyparsing>=2.3.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (3.0.9)
Requirement already satisfied: importlib-resources>=3.2.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (5.12.0)
Requirement already satisfied: contourpy>=1.0.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from matplotlib->music21) (1.0.7)
Requirement already satisfied: idna<4,>=2.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->music21) (3.4)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->music21) (1.26.15)
Requirement already satisfied: certifi>=2017.4.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->music21) (2022.12.7)
Requirement already satisfied: charset-normalizer<4,>=2 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->music21) (3.1.0)
Requirement already satisfied: zipp>=3.1.0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from importlib-resources>=3.2.0->matplotlib->music21) (3.15.0)
Requirement already satisfied: six>=1.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib->music21) (1.16.0)
Installing collected packages: webcolors, more-itertools, jsonpickle, chardet, music21
Successfully installed chardet-5.1.0 jsonpickle-3.0.1 more-itertools-9.1.0 music21-8.1.0 webcolors-1.12
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### NKF

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_nkf.sh 
--2023-03-26 14:27:07--  https://ja.osdn.net/dl/nkf/nkf-2.1.4.tar.gz
Resolving ja.osdn.net (ja.osdn.net)... 52.10.189.44, 54.213.47.89
Connecting to ja.osdn.net (ja.osdn.net)|52.10.189.44|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://ja.osdn.net/projects/nkf/downloads/64158/nkf-2.1.4.tar.gz/ [following]
--2023-03-26 14:27:08--  https://ja.osdn.net/projects/nkf/downloads/64158/nkf-2.1.4.tar.gz/
Reusing existing connection to ja.osdn.net:443.
HTTP request sent, awaiting response... 302 Found
Location: https://ja.osdn.net/frs/redir.php?m=rwthaachen&f=nkf%2F64158%2Fnkf-2.1.4.tar.gz [following]
--2023-03-26 14:27:08--  https://ja.osdn.net/frs/redir.php?m=rwthaachen&f=nkf%2F64158%2Fnkf-2.1.4.tar.gz
Reusing existing connection to ja.osdn.net:443.
HTTP request sent, awaiting response... 302 Found
Location: https://ftp.halifax.rwth-aachen.de/osdn/nkf/64158/nkf-2.1.4.tar.gz [following]
--2023-03-26 14:27:08--  https://ftp.halifax.rwth-aachen.de/osdn/nkf/64158/nkf-2.1.4.tar.gz
Resolving ftp.halifax.rwth-aachen.de (ftp.halifax.rwth-aachen.de)... 137.226.34.46, 2a00:8a60:e012:a00::21
Connecting to ftp.halifax.rwth-aachen.de (ftp.halifax.rwth-aachen.de)|137.226.34.46|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 232479 (227K) [application/octet-stream]
Saving to: ‘nkf-2.1.4.tar.gz’

nkf-2.1.4.tar.gz          100%[==================================>] 227.03K   391KB/s    in 0.6s    

2023-03-26 14:27:10 (391 KB/s) - ‘nkf-2.1.4.tar.gz’ saved [232479/232479]

nkf-2.1.4/
nkf-2.1.4/Makefile
nkf-2.1.4/version.rc
nkf-2.1.4/dll.def
nkf-2.1.4/nkf.mak
nkf-2.1.4/INSTALL.j
nkf-2.1.4/MANIFEST
nkf-2.1.4/NKF.mod/
nkf-2.1.4/nkf32dll.c
nkf-2.1.4/INSTALL
nkf-2.1.4/nkf.c
nkf-2.1.4/make_test.pl
nkf-2.1.4/utf8tbl.h
nkf-2.1.4/nkf32.h
nkf-2.1.4/nkf.1
nkf-2.1.4/config.h
nkf-2.1.4/nkf_test.pl
nkf-2.1.4/utf8tbl.c
nkf-2.1.4/nkf32.c
nkf-2.1.4/nkf.h
nkf-2.1.4/test.pl
nkf-2.1.4/dll.rc
nkf-2.1.4/nkf.1j
nkf-2.1.4/nkf.doc
nkf-2.1.4/NKF.mod/Makefile.PL
nkf-2.1.4/NKF.mod/README
nkf-2.1.4/NKF.mod/MANIFEST
nkf-2.1.4/NKF.mod/Changes
nkf-2.1.4/NKF.mod/NKF.xs
nkf-2.1.4/NKF.mod/test.pl
nkf-2.1.4/NKF.mod/NKF.pm
cc -g -O2 -Wall -pedantic -c nkf.c
nkf.c: In function ‘module_connection’:
nkf.c:5710:5: warning: this ‘if’ clause does not guard... [-Wmisleading-indentation]
     if (nkf_enc_unicode_p(output_encoding))
     ^~
nkf.c:5713:2: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
  if (x0201_f == NKF_UNSPECIFIED) {
  ^~
cc -g -O2 -Wall -pedantic -c utf8tbl.c
cc -g -O2 -Wall -pedantic  -o nkf nkf.o utf8tbl.o
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### openface

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_openface.sh 
./install_openface.sh: line 24: [: too many arguments
./install_openface.sh: line 24: [: too many arguments
Downloading OpenFace
Cloning into 'OpenFace'...
remote: Enumerating objects: 21343, done.
remote: Total 21343 (delta 0), reused 0 (delta 0), pack-reused 21343
Receiving objects: 100% (21343/21343), 1.66 GiB | 13.58 MiB/s, done.
Resolving deltas: 100% (11225/11225), done.
Updating files: 100% (3672/3672), done.
cp: cannot stat 'CMakeLists.txt': No such file or directory
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

### SpeechBrain

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_speechbrain.sh 
...
...
...
  Downloading torchaudio-0.12.0-cp38-cp38-manylinux1_x86_64.whl (3.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.7/3.7 MB 13.0 MB/s eta 0:00:00
  Downloading torchaudio-0.11.0-cp38-cp38-manylinux1_x86_64.whl (2.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.9/2.9 MB 14.3 MB/s eta 0:00:00
Collecting ruamel.yaml.clib>=0.2.6
  Downloading ruamel.yaml.clib-0.2.7-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (555 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 555.3/555.3 kB 10.9 MB/s eta 0:00:00
Requirement already satisfied: charset-normalizer<4,>=2 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->huggingface-hub->speechbrain==0.5.11) (3.1.0)
Requirement already satisfied: certifi>=2017.4.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->huggingface-hub->speechbrain==0.5.11) (2022.12.7)
Requirement already satisfied: idna<4,>=2.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->huggingface-hub->speechbrain==0.5.11) (3.4)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->huggingface-hub->speechbrain==0.5.11) (1.26.15)
Installing collected packages: torch, ruamel.yaml.clib, torchaudio, ruamel.yaml, hyperpyyaml, speechbrain
  Attempting uninstall: torch
    Found existing installation: torch 1.13.1+cu117
    Uninstalling torch-1.13.1+cu117:
      Successfully uninstalled torch-1.13.1+cu117
  Attempting uninstall: torchaudio
    Found existing installation: torchaudio 0.13.1+cu117
    Uninstalling torchaudio-0.13.1+cu117:
      Successfully uninstalled torchaudio-0.13.1+cu117
Successfully installed hyperpyyaml-1.1.0 ruamel.yaml-0.17.21 ruamel.yaml.clib-0.2.7 speechbrain-0.5.11 torch-1.11.0 torchaudio-0.11.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### Transformers

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_transformers.sh 
...
...
...
Requirement already satisfied: tokenizers!=0.11.3,<0.14,>=0.11.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from transformers>=4.9.1) (0.13.2)
Requirement already satisfied: tqdm>=4.27 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from transformers>=4.9.1) (4.65.0)
Requirement already satisfied: pyyaml>=5.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from transformers>=4.9.1) (6.0)
Requirement already satisfied: filelock in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from transformers>=4.9.1) (3.10.6)
Requirement already satisfied: regex!=2019.12.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from transformers>=4.9.1) (2023.3.23)
Requirement already satisfied: typing-extensions>=3.7.4.3 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from huggingface-hub<1.0,>=0.11.0->transformers>=4.9.1) (4.5.0)
Requirement already satisfied: idna<4,>=2.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.9.1) (3.4)
Requirement already satisfied: charset-normalizer<4,>=2 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.9.1) (3.1.0)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.9.1) (1.26.15)
Requirement already satisfied: certifi>=2017.4.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.9.1) (2022.12.7)
(espnet) rnd@gpu:~/tool/espnet/tools/installers$
```

### Whisper

```
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ ./install_whisper.sh
...
...
...
te-packages (from numba->openai-whisper==20230308) (4.13.0)
Requirement already satisfied: llvmlite<0.40,>=0.39.0dev0 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from numba->openai-whisper==20230308) (0.39.1)
Requirement already satisfied: typing-extensions in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from torch->openai-whisper==20230308) (4.5.0)
Requirement already satisfied: zipp>=0.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from importlib-metadata->numba->openai-whisper==20230308) (3.15.0)
Requirement already satisfied: certifi>=2017.4.17 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.19.0->openai-whisper==20230308) (2022.12.7)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.19.0->openai-whisper==20230308) (1.26.15)
Requirement already satisfied: idna<4,>=2.5 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.19.0->openai-whisper==20230308) (3.4)
Requirement already satisfied: charset-normalizer<4,>=2 in /home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages (from requests->transformers>=4.19.0->openai-whisper==20230308) (3.1.0)
Building wheels for collected packages: openai-whisper
  Building wheel for openai-whisper (pyproject.toml) ... done
  Created wheel for openai-whisper: filename=openai_whisper-20230308-py3-none-any.whl size=1187481 sha256=9f652ee3867bdb3285dd80ebedd1b07342abf8b10e6b54ed5a1681c550304c67
  Stored in directory: /home/rnd/.cache/pip/wheels/b4/24/08/db680e86a15656ffc3be8cfec39531e8ee345cfeb48ca95c08
Successfully built openai-whisper
Installing collected packages: lit, cmake, triton, openai-whisper
Successfully installed cmake-3.26.1 lit-16.0.0 openai-whisper-20230308 triton-2.0.0
(espnet) rnd@gpu:~/tool/espnet/tools/installers$ 
```

သုံးချင်တဲ့ tools တွေ အားလုံးမဟုတ်ပေမဲ့ တော်တော်များများ ကို install လုပ်ထားခဲ့ ...  

## Installation of Kaldi Tools

```
(espnet) rnd@gpu:~/tool/kaldi/tools$ make
...
...
...
make[2]: Leaving directory '/home/rnd/tool/kaldi/tools/sctk-20159b5/src'
make[1]: Leaving directory '/home/rnd/tool/kaldi/tools/sctk-20159b5'
touch sctk/.compiled
if [ -d "" ]; then \
  cp -p "/sph2pipe-v2.5.tar.gz" \
        sph2pipe-2.5.tar.gz; \
else \
  wget -nv -T 10 -t 3 -O sph2pipe-2.5.tar.gz \
    https://github.com/burrmill/sph2pipe/archive/2.5.tar.gz; \
fi
2023-03-26 13:42:40 URL:https://codeload.github.com/burrmill/sph2pipe/tar.gz/refs/tags/2.5 [290693] -> "sph2pipe-2.5.tar.gz" [1]
rm -rf sph2pipe_v*
tar -xmzf sph2pipe-2.5.tar.gz
mv sph2pipe-2.5 sph2pipe_v2.5
make -C sph2pipe_v2.5
make[1]: Entering directory '/home/rnd/tool/kaldi/tools/sph2pipe_v2.5'
cc -o sph2pipe -s -w -g -O2  file_headers.c shorten_x.c sph2pipe.c -lm
make[1]: Leaving directory '/home/rnd/tool/kaldi/tools/sph2pipe_v2.5'
rm -f sph2pipe
ln -s sph2pipe_v2.5 sph2pipe
touch -r sph2pipe -c sph2pipe_v2.5/sph2pipe
-e 


Warning: IRSTLM is not installed by default anymore. If you need IRSTLM
Warning: use the script extras/install_irstlm.sh
All done OK.
(espnet) rnd@gpu:~/tool/kaldi/tools$
```

## Installation of Kaldi

```
(espnet) rnd@gpu:~/tool/kaldi/tools$ cd ../src
(espnet) rnd@gpu:~/tool/kaldi/src$ ./configure
Configuring KALDI to use MKL.
Checking compiler c++ ...
Checking OpenFst library in /home/rnd/tool/kaldi/tools/openfst-1.7.2 ...
Checking cub library in /home/rnd/tool/kaldi/tools/cub-1.8.0 ...
Performing OS specific configuration ...
On Linux: Checking for linear algebra header files ...
Configuring MKL library directory: Found /opt/intel/mkl/lib/intel64
MKL libs MKL_LDLIBS = -L/opt/intel/mkl/lib/intel64 -Wl,-rpath=/opt/intel/mkl/lib/intel64 -l:libmkl_intel_lp64.so -l:libmkl_core.so -l:libmkl_sequential.so -ldl -lpthread -lm.
MKL compile flags MKL_CXXFLAGS = -I/opt/intel/mkl/include.
*** MKL self-reported version:
Intel(R) Math Kernel Library Version 2020.0.0 Product Build 20191122 for Intel(R) 64 architecture applications
Successfully configured for Linux with MKL libraries found in /opt/intel/mkl
Using CUDA toolkit /usr/ (nvcc compiler and runtime libraries)
INFO: Configuring Kaldi not to link with Speex. Don't worry, it's only needed if
      you intend to use 'compress-uncompress-speex', which is very unlikely.
WARNING: slow expf() detected. expf() is slower than exp() by the factor of 1.83784
*** WARNING: expf() seems to be slower than exp() on your machine. This is
***          a known bug in old versions of glibc. Please consider updating it.
***          Kaldi will be configured to use exp() instead of expf() in
***          base/kaldi-math.h Exp() routine for single-precision floats.
Kaldi has been successfully configured. To compile:

  make -j clean depend; make -j <NCPU>

where <NCPU> is the number of parallel builds you can afford to do. If unsure,
use the smaller of the number of CPUs or the amount of RAM in GB divided by 2,
to stay within safe limits. 'make -j' without the numeric value may not limit
the number of parallel jobs at all, and overwhelm even a powerful workstation,
since Kaldi build is highly parallelized.
(espnet) rnd@gpu:~/tool/kaldi/src$
```

Run make ...  

```
(espnet) rnd@gpu:~/tool/kaldi/src$ time make
...
...
...
equential.so -ldl -lpthread -lm -lm -lpthread -ldl -o matrix-lib-test
c++ -std=c++14 -I.. -isystem /home/rnd/tool/kaldi/tools/openfst-1.7.2/include -O1 -Wall -Wno-sign-compare -Wno-unused-local-typedefs -Wno-deprecated-declarations -Winit-self -DKALDI_DOUBLEPRECISION=0 -DHAVE_EXECINFO_H=1 -DHAVE_CXXABI_H -DHAVE_MKL -I/opt/intel/mkl/include -m64 -msse -msse2 -pthread -g  -DHAVE_CUDA -I/usr//include -fPIC -pthread -isystem /home/rnd/tool/kaldi/tools/openfst-1.7.2/include -DKALDI_NO_EXPF   -c -o sparse-matrix-test.o sparse-matrix-test.cc
c++ -Wl,-rpath=/home/rnd/tool/kaldi/tools/openfst-1.7.2/lib -rdynamic   sparse-matrix-test.o kaldi-matrix.a ../base/kaldi-base.a   /home/rnd/tool/kaldi/tools/openfst-1.7.2/lib/libfst.so -L/opt/intel/mkl/lib/intel64 -Wl,-rpath=/opt/intel/mkl/lib/intel64 -l:libmkl_intel_lp64.so -l:libmkl_core.so -l:libmkl_sequential.so -ldl -lpthread -lm -lm -lpthread -ldl -o sparse-matrix-test
c++ -std=c++14 -I.. -isystem /home/rnd/tool/kaldi/tools/openfst-1.7.2/include -O1 -Wall -Wno-sign-compare -Wno-unused-local-typedefs -Wno-deprecated-declarations -Winit-self -DKALDI_DOUBLEPRECISION=0 -DHAVE_EXECINFO_H=1 -DHAVE_CXXABI_H -DHAVE_MKL -I/opt/intel/mkl/include -m64 -msse -msse2 -pthread -g  -DHAVE_CUDA -I/usr//include -fPIC -pthread -isystem /home/rnd/tool/kaldi/tools/openfst-1.7.2/include -DKALDI_NO_EXPF   -c -o numpy-array-test.o numpy-array-test.cc
c++ -Wl,-rpath=/home/rnd/tool/kaldi/tools/openfst-1.7.2/lib -rdynamic   numpy-array-test.o kaldi-matrix.a ../base/kaldi-base.a   /home/rnd/tool/kaldi/tools/openfst-1.7.2/lib/libfst.so -L/opt/intel/mkl/lib/intel64 -Wl,-rpath=/opt/intel/mkl/lib/intel64 -l:libmkl_intel_lp64.so -l:libmkl_core.so -l:libmkl_sequential.so -ldl -lpthread -lm -lm -lpthread -ldl -o numpy-array-test
Running matrix-lib-test ... 1s... SUCCESS matrix-lib-test
Running sparse-matrix-test ... 0s... SUCCESS sparse-matrix-test
Running numpy-array-test ... 0s... SUCCESS numpy-array-test
make[1]: Leaving directory '/home/rnd/tool/kaldi/src/matrix'
Done

real	61m59.103s
user	57m46.424s
sys	3m34.796s
(espnet) rnd@gpu:~/tool/kaldi/src$ 
```

## Create Soft-link for Kaldi

```
(espnet) rnd@gpu:~/tool/espnet/tools$ ln -s /home/rnd/tool/kaldi .
```

## Recheck After Installation of Some More Tools

```
(espnet) rnd@gpu:~/tool/espnet/tools$ bash -c ". ./activate_python.sh; . ./extra_path.sh; python3 check_install.py" | tee check_install.log
/home/rnd/anaconda3/envs/espnet/lib/python3.8/site-packages/cupy/_environment.py:399: UserWarning: 
nccl library could not be loaded.

Reason: ImportError (libnccl.so.2: cannot open shared object file: No such file or directory)

You can install the library by:

  $ conda install -c conda-forge nccl

  warnings.warn(msg)
/home/rnd/tool/espnet/tools/chainer/chainer/_environment_check.py:70: UserWarning: 
--------------------------------------------------------------------------------
CuPy (cupy) version 10.2.0 may not be compatible with this version of Chainer.
Please consider installing the supported version by running:
  $ pip install 'cupy>=6.0.0,<7.0.0'

See the following page for more details:
  https://docs-cupy.chainer.org/en/latest/install.html
--------------------------------------------------------------------------------

  warnings.warn(msg.format(
[x] python=3.8.16 (default, Mar  2 2023, 03:21:46)  [GCC 11.2.0]

Python modules:
[x] torch=1.11.0+cu102
[x] torch cuda=10.2
[x] torch cudnn=7605
[x] torch nccl
[x] chainer=6.0.0
[x] chainer cuda
[x] chainer cudnn
[x] cupy=10.2.0
[x] cupy nccl
[x] torchaudio=0.11.0+cu102
[x] torch_optimizer=0.3.0
[ ] warprnnt_pytorch
[ ] chainer_ctc
[ ] pyopenjtalk
[ ] tdmelodic_pyopenjtalk
[x] kenlm
[ ] mmseg
[x] espnet=202301
[x] numpy=1.22.4
[x] fairseq=1.0.0a0+313ff05
[ ] phonemizer
[x] gtn=0.0.0
[ ] s3prl
[x] transformers=4.27.3
[x] speechbrain=0.5.11
[ ] k2
[x] longformer
[ ] nlg-eval
[x] datasets=2.10.1
[ ] pykeops
[x] whisper=20230308
[ ] RawNet3
[ ] reazonspeech
[ ] muskits
[x] Kaldi (compiled)

Executables:
[x] sclite
[x] sph2pipe
[ ] PESQ
[ ] BeamformIt
[x] spm_train
[x] spm_encode
[x] spm_decode
[x] sox=14.4.2
[x] ffmpeg=6.0
[ ] flac
[x] cmake=3.26.1

INFO:
Use 'installers/install_warp-transducer.sh' to install warprnnt_pytorch
Use 'installers/install_chainer_ctc.sh' to install chainer_ctc
Use 'installers/install_pyopenjtalk.sh' to install pyopenjtalk
Use 'installers/install_tdmelodic_pyopenjtalk.sh' to install tdmelodic_pyopenjtalk
Use 'installers/install_py3mmseg.sh' to install mmseg
Use 'installers/install_phonemizer.sh' to install phonemizer
Use 'installers/install_s3prl.sh' to install s3prl
Use 'installers/install_k2.sh' to install k2
Use 'installers/install_longformer.sh' to install nlg-eval
Use 'installers/install_cauchy_mult.sh' to install pykeops
Use 'installers/install_rawnet.sh' to install RawNet3
Use 'installers/install_reazonspeech.sh' to install reazonspeech
Use 'installers/install_muskits.sh' to install muskits
Use 'installers/install_pesq.sh' to install PESQ
Use 'installers/install_beamformit.sh' to install BeamformIt
(espnet) rnd@gpu:~/tool/espnet/tools$ 
```

ဒီတစ်ခါတော့ Kaldi ရဲ့ checkbox မှာ on သွားပြီမို့ အဆင်ပြေပြီလို့ ယူဆ ...  
PyOpenJtalk ရဲ့ checkbox ကတော့ on မဖြစ်ဘူး။ ဒါကတော့ ဂျပန်စာ သုံးမှပဲ လိုတာမို့ ... 

