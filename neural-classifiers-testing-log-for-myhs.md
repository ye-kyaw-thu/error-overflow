# Neural Classifiers Testing Log

## Create a New Conda Env

```
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ conda create --name nclassi python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.3.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/nclassi

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    python-3.8.19              |       h955ad1f_0        23.8 MB
    ------------------------------------------------------------
                                           Total:        23.8 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2024.3.11-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.13-h7f8727e_0
  pip                pkgs/main/linux-64::pip-23.3.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.19-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.2.2-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.8.19        | 23.8 MB   | ####################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate nclassi
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

```
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ conda activate nclassi
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

## Install Requirements

God Error! as follows:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ pip install -r ./requirements.txt
Collecting numpy>=1.16.2 (from -r ./requirements.txt (line 1))
  Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.6 kB)
Collecting torch>=1.0.1.post2 (from -r ./requirements.txt (line 2))
  Downloading torch-2.2.2-cp38-cp38-manylinux1_x86_64.whl.metadata (25 kB)
Collecting filelock (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Downloading filelock-3.13.3-py3-none-any.whl.metadata (2.8 kB)
Collecting typing-extensions>=4.8.0 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached typing_extensions-4.10.0-py3-none-any.whl.metadata (3.0 kB)
Collecting sympy (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached sympy-1.12-py3-none-any.whl.metadata (12 kB)
Collecting networkx (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached networkx-3.1-py3-none-any.whl.metadata (5.3 kB)
Collecting jinja2 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached Jinja2-3.1.3-py3-none-any.whl.metadata (3.3 kB)
Collecting fsspec (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached fsspec-2024.3.1-py3-none-any.whl.metadata (6.8 kB)
Collecting nvidia-cuda-nvrtc-cu12==12.1.105 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting nvidia-cuda-runtime-cu12==12.1.105 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting nvidia-cuda-cupti-cu12==12.1.105 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cudnn-cu12==8.9.2.26 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cublas-cu12==12.1.3.1 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting nvidia-cufft-cu12==11.0.2.54 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting nvidia-curand-cu12==10.3.2.106 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting nvidia-cusolver-cu12==11.4.5.107 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cusparse-cu12==12.1.0.106 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-nccl-cu12==2.19.3 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_nccl_cu12-2.19.3-py3-none-manylinux1_x86_64.whl.metadata (1.8 kB)
Collecting nvidia-nvtx-cu12==12.1.105 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl.metadata (1.7 kB)
Collecting triton==2.2.0 (from torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached triton-2.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.4 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cusolver-cu12==11.4.5.107->torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached nvidia_nvjitlink_cu12-12.4.99-py3-none-manylinux2014_x86_64.whl.metadata (1.5 kB)
Requirement already satisfied: MarkupSafe>=2.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from jinja2->torch>=1.0.1.post2->-r ./requirements.txt (line 2)) (2.1.1)
Collecting mpmath>=0.19 (from sympy->torch>=1.0.1.post2->-r ./requirements.txt (line 2))
  Using cached mpmath-1.3.0-py3-none-any.whl.metadata (8.6 kB)
Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
Downloading torch-2.2.2-cp38-cp38-manylinux1_x86_64.whl (755.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 755.5/755.5 MB 1.7 MB/s eta 0:00:00
Using cached nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl (410.6 MB)
Using cached nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (14.1 MB)
Using cached nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (23.7 MB)
Using cached nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (823 kB)
Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl (731.7 MB)
Using cached nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl (121.6 MB)
Using cached nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl (56.5 MB)
Using cached nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl (124.2 MB)
Using cached nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl (196.0 MB)
Using cached nvidia_nccl_cu12-2.19.3-py3-none-manylinux1_x86_64.whl (166.0 MB)
Using cached nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (99 kB)
Using cached triton-2.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (167.9 MB)
Using cached typing_extensions-4.10.0-py3-none-any.whl (33 kB)
Downloading filelock-3.13.3-py3-none-any.whl (11 kB)
Using cached fsspec-2024.3.1-py3-none-any.whl (171 kB)
Using cached Jinja2-3.1.3-py3-none-any.whl (133 kB)
Using cached networkx-3.1-py3-none-any.whl (2.1 MB)
Using cached sympy-1.12-py3-none-any.whl (5.7 MB)
Using cached mpmath-1.3.0-py3-none-any.whl (536 kB)
Using cached nvidia_nvjitlink_cu12-12.4.99-py3-none-manylinux2014_x86_64.whl (21.1 MB)
Installing collected packages: mpmath, typing-extensions, sympy, nvidia-nvtx-cu12, nvidia-nvjitlink-cu12, nvidia-nccl-cu12, nvidia-curand-cu12, nvidia-cufft-cu12, nvidia-cuda-runtime-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-cupti-cu12, nvidia-cublas-cu12, numpy, networkx, jinja2, fsspec, filelock, triton, nvidia-cusparse-cu12, nvidia-cudnn-cu12, nvidia-cusolver-cu12, torch
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
seaborn 0.12.2 requires matplotlib!=3.6.1,>=3.1, which is not installed.
seaborn 0.12.2 requires pandas>=0.25, which is not installed.
tensorboard 2.11.2 requires requests<3,>=2.21.0, which is not installed.
tensorboard 2.11.2 requires werkzeug>=1.0.1, which is not installed.
tensorflow 2.11.0 requires six>=1.12.0, which is not installed.
Successfully installed filelock-3.13.3 fsspec-2024.3.1 jinja2-3.1.3 mpmath-1.3.0 networkx-3.1 numpy-1.24.4 nvidia-cublas-cu12-12.1.3.1 nvidia-cuda-cupti-cu12-12.1.105 nvidia-cuda-nvrtc-cu12-12.1.105 nvidia-cuda-runtime-cu12-12.1.105 nvidia-cudnn-cu12-8.9.2.26 nvidia-cufft-cu12-11.0.2.54 nvidia-curand-cu12-10.3.2.106 nvidia-cusolver-cu12-11.4.5.107 nvidia-cusparse-cu12-12.1.0.106 nvidia-nccl-cu12-2.19.3 nvidia-nvjitlink-cu12-12.4.99 nvidia-nvtx-cu12-12.1.105 sympy-1.12 torch-2.2.2 triton-2.2.0 typing-extensions-4.10.0
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```


```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ pip install seaborn
Requirement already satisfied: seaborn in /home/yekyaw.thu/.local/lib/python3.8/site-packages (0.12.2)
Requirement already satisfied: numpy!=1.24.0,>=1.17 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from seaborn) (1.24.4)
Collecting pandas>=0.25 (from seaborn)
  Using cached pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (18 kB)
Collecting matplotlib!=3.6.1,>=3.1 (from seaborn)
  Using cached matplotlib-3.7.5-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl.metadata (5.7 kB)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.0.7)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (0.11.0)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (4.38.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.4.4)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (23.0)
Collecting pillow>=6.2.0 (from matplotlib!=3.6.1,>=3.1->seaborn)
  Using cached pillow-10.2.0-cp38-cp38-manylinux_2_28_x86_64.whl.metadata (9.7 kB)
Requirement already satisfied: pyparsing>=2.3.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (3.0.9)
Requirement already satisfied: python-dateutil>=2.7 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (2.8.2)
Collecting importlib-resources>=3.2.0 (from matplotlib!=3.6.1,>=3.1->seaborn)
  Downloading importlib_resources-6.4.0-py3-none-any.whl.metadata (3.9 kB)
Requirement already satisfied: pytz>=2020.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from pandas>=0.25->seaborn) (2022.7.1)
Collecting tzdata>=2022.1 (from pandas>=0.25->seaborn)
  Downloading tzdata-2024.1-py2.py3-none-any.whl.metadata (1.4 kB)
Collecting zipp>=3.1.0 (from importlib-resources>=3.2.0->matplotlib!=3.6.1,>=3.1->seaborn)
  Using cached zipp-3.18.1-py3-none-any.whl.metadata (3.5 kB)
Collecting six>=1.5 (from python-dateutil>=2.7->matplotlib!=3.6.1,>=3.1->seaborn)
  Using cached six-1.16.0-py2.py3-none-any.whl.metadata (1.8 kB)
Using cached matplotlib-3.7.5-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (9.2 MB)
Using cached pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.4 MB)
Downloading importlib_resources-6.4.0-py3-none-any.whl (38 kB)
Using cached pillow-10.2.0-cp38-cp38-manylinux_2_28_x86_64.whl (4.5 MB)
Downloading tzdata-2024.1-py2.py3-none-any.whl (345 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 345.4/345.4 kB 1.9 MB/s eta 0:00:00
Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Using cached zipp-3.18.1-py3-none-any.whl (8.2 kB)
Installing collected packages: zipp, tzdata, six, pillow, importlib-resources, pandas, matplotlib
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
google-auth 2.16.0 requires pyasn1-modules>=0.2.1, which is not installed.
tensorboard 2.11.2 requires requests<3,>=2.21.0, which is not installed.
tensorboard 2.11.2 requires werkzeug>=1.0.1, which is not installed.
Successfully installed importlib-resources-6.4.0 matplotlib-3.7.5 pandas-2.0.3 pillow-10.2.0 six-1.16.0 tzdata-2024.1 zipp-3.18.1
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ pip install tensorflow
Requirement already satisfied: tensorflow in /home/yekyaw.thu/.local/lib/python3.8/site-packages (2.11.0)
Requirement already satisfied: absl-py>=1.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.4.0)
Requirement already satisfied: astunparse>=1.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.6.3)
Requirement already satisfied: flatbuffers>=2.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.1.4)
Requirement already satisfied: gast<=0.4.0,>=0.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.4.0)
Requirement already satisfied: google-pasta>=0.1.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.2.0)
Requirement already satisfied: grpcio<2.0,>=1.24.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.51.1)
Requirement already satisfied: h5py>=2.9.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.7.0)
Requirement already satisfied: keras<2.12,>=2.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.0)
Requirement already satisfied: libclang>=13.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (15.0.6.1)
Requirement already satisfied: numpy>=1.20 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorflow) (1.24.4)
Requirement already satisfied: opt-einsum>=2.3.2 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.3.0)
Requirement already satisfied: packaging in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.0)
Requirement already satisfied: protobuf<3.20,>=3.9.2 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.19.6)
Requirement already satisfied: setuptools in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorflow) (68.2.2)
Requirement already satisfied: six>=1.12.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorflow) (1.16.0)
Requirement already satisfied: tensorboard<2.12,>=2.11 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.2)
Requirement already satisfied: tensorflow-estimator<2.12,>=2.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.0)
Requirement already satisfied: termcolor>=1.1.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.2.0)
Requirement already satisfied: typing-extensions>=3.6.6 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorflow) (4.10.0)
Requirement already satisfied: wrapt>=1.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.14.1)
Requirement already satisfied: tensorflow-io-gcs-filesystem>=0.23.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.29.0)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from astunparse>=1.6.0->tensorflow) (0.41.2)
Requirement already satisfied: google-auth<3,>=1.6.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.16.0)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (0.4.6)
Requirement already satisfied: markdown>=2.6.8 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (3.4.1)
Collecting requests<3,>=2.21.0 (from tensorboard<2.12,>=2.11->tensorflow)
  Using cached requests-2.31.0-py3-none-any.whl.metadata (4.6 kB)
Requirement already satisfied: tensorboard-data-server<0.7.0,>=0.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (0.6.1)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (1.8.1)
Collecting werkzeug>=1.0.1 (from tensorboard<2.12,>=2.11->tensorflow)
  Using cached werkzeug-3.0.1-py3-none-any.whl.metadata (4.1 kB)
Requirement already satisfied: cachetools<6.0,>=2.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (5.2.1)
Collecting pyasn1-modules>=0.2.1 (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow)
  Downloading pyasn1_modules-0.4.0-py3-none-any.whl.metadata (3.4 kB)
Requirement already satisfied: rsa<5,>=3.1.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (4.9)
Requirement already satisfied: requests-oauthlib>=0.7.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.12,>=2.11->tensorflow) (1.3.1)
Requirement already satisfied: importlib-metadata>=4.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (6.0.0)
Collecting charset-normalizer<4,>=2 (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow)
  Using cached charset_normalizer-3.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (33 kB)
Collecting idna<4,>=2.5 (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow)
  Using cached idna-3.6-py3-none-any.whl.metadata (9.9 kB)
Collecting urllib3<3,>=1.21.1 (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow)
  Using cached urllib3-2.2.1-py3-none-any.whl.metadata (6.4 kB)
Collecting certifi>=2017.4.17 (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow)
  Using cached certifi-2024.2.2-py3-none-any.whl.metadata (2.2 kB)
Requirement already satisfied: MarkupSafe>=2.1.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from werkzeug>=1.0.1->tensorboard<2.12,>=2.11->tensorflow) (2.1.1)
Requirement already satisfied: zipp>=0.5 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (3.18.1)
Collecting pyasn1<0.7.0,>=0.4.6 (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow)
  Downloading pyasn1-0.6.0-py2.py3-none-any.whl.metadata (8.3 kB)
Collecting oauthlib>=3.0.0 (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.12,>=2.11->tensorflow)
  Downloading oauthlib-3.2.2-py3-none-any.whl.metadata (7.5 kB)
Using cached requests-2.31.0-py3-none-any.whl (62 kB)
Using cached werkzeug-3.0.1-py3-none-any.whl (226 kB)
Using cached certifi-2024.2.2-py3-none-any.whl (163 kB)
Using cached charset_normalizer-3.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (141 kB)
Using cached idna-3.6-py3-none-any.whl (61 kB)
Downloading pyasn1_modules-0.4.0-py3-none-any.whl (181 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.2/181.2 kB 971.6 kB/s eta 0:00:00
Using cached urllib3-2.2.1-py3-none-any.whl (121 kB)
Using cached oauthlib-3.2.2-py3-none-any.whl (151 kB)
Downloading pyasn1-0.6.0-py2.py3-none-any.whl (85 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 85.3/85.3 kB 860.1 kB/s eta 0:00:00
Installing collected packages: werkzeug, urllib3, pyasn1, oauthlib, idna, charset-normalizer, certifi, requests, pyasn1-modules
Successfully installed certifi-2024.2.2 charset-normalizer-3.3.2 idna-3.6 oauthlib-3.2.2 pyasn1-0.6.0 pyasn1-modules-0.4.0 requests-2.31.0 urllib3-2.2.1 werkzeug-3.0.1
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ pip install tensorboard
Requirement already satisfied: tensorboard in /home/yekyaw.thu/.local/lib/python3.8/site-packages (2.11.2)
Requirement already satisfied: absl-py>=0.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (1.4.0)
Requirement already satisfied: grpcio>=1.24.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (1.51.1)
Requirement already satisfied: google-auth<3,>=1.6.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (2.16.0)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (0.4.6)
Requirement already satisfied: markdown>=2.6.8 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (3.4.1)
Requirement already satisfied: numpy>=1.12.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorboard) (1.24.4)
Requirement already satisfied: protobuf<4,>=3.9.2 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (3.19.6)
Requirement already satisfied: requests<3,>=2.21.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorboard) (2.31.0)
Requirement already satisfied: setuptools>=41.0.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorboard) (68.2.2)
Requirement already satisfied: tensorboard-data-server<0.7.0,>=0.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (0.6.1)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard) (1.8.1)
Requirement already satisfied: werkzeug>=1.0.1 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorboard) (3.0.1)
Requirement already satisfied: wheel>=0.26 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from tensorboard) (0.41.2)
Requirement already satisfied: cachetools<6.0,>=2.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard) (5.2.1)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard) (0.4.0)
Requirement already satisfied: six>=1.9.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard) (1.16.0)
Requirement already satisfied: rsa<5,>=3.1.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard) (4.9)
Requirement already satisfied: requests-oauthlib>=0.7.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard) (1.3.1)
Requirement already satisfied: importlib-metadata>=4.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from markdown>=2.6.8->tensorboard) (6.0.0)
Requirement already satisfied: charset-normalizer<4,>=2 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard) (3.3.2)
Requirement already satisfied: idna<4,>=2.5 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard) (3.6)
Requirement already satisfied: urllib3<3,>=1.21.1 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard) (2.2.1)
Requirement already satisfied: certifi>=2017.4.17 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard) (2024.2.2)
Requirement already satisfied: MarkupSafe>=2.1.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from werkzeug>=1.0.1->tensorboard) (2.1.1)
Requirement already satisfied: zipp>=0.5 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard) (3.18.1)
Requirement already satisfied: pyasn1<0.7.0,>=0.4.6 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard) (0.6.0)
Requirement already satisfied: oauthlib>=3.0.0 in /home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard) (3.2.2)
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

## Testing-1

train.json config ဖိုင်ကို လေ့လာ ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$ cat train.json
{
  "task_info":{
    "label_type": "multi_label",
    "hierarchical": false,
    "hierar_taxonomy": "data/rcv1.taxonomy",
    "hierar_penalty": 0.000001
  },
  "device": "cuda",
  "model_name": "TextCNN",
  "checkpoint_dir": "checkpoint_dir_rcv1",
  "model_dir": "trained_model_rcv1",
  "data": {
    "train_json_files": [
      "data/rcv1_train.json"
    ],
    "validate_json_files": [
      "data/rcv1_dev.json"
    ],
    "test_json_files": [
      "data/rcv1_test.json"
    ],
    "generate_dict_using_json_files": true,
    "generate_dict_using_all_json_files": true,
    "generate_dict_using_pretrained_embedding": false,
    "generate_hierarchy_label": true,
    "dict_dir": "dict_rcv1",
    "num_worker": 4
  },
  "feature": {
    "feature_names": [
      "token"
    ],
    "min_token_count": 2,
    "min_char_count": 2,
    "token_ngram": 0,
    "min_token_ngram_count": 0,
    "min_keyword_count": 0,
    "min_topic_count": 2,
    "max_token_dict_size": 1000000,
    "max_char_dict_size": 150000,
    "max_token_ngram_dict_size": 10000000,
    "max_keyword_dict_size": 100,
    "max_topic_dict_size": 100,
    "max_token_len": 256,
    "max_char_len": 1024,
    "max_char_len_per_token": 4,
    "token_pretrained_file": "",
    "keyword_pretrained_file": ""
  },
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 5,
    "num_epochs_static_embedding": 0,
    "decay_steps": 1000,
    "decay_rate": 1.0,
    "clip_gradients": 100.0,
    "l2_lambda": 0.0,
    "loss_type": "BCEWithLogitsLoss",
    "sampler": "fixed",
    "num_sampled": 5,
    "visible_device_list": "0",
    "hidden_layer_dropout": 0.5
  },
  "embedding": {
    "type": "embedding",
    "dimension": 64,
    "region_embedding_type": "context_word",
    "region_size": 5,
    "initializer": "uniform",
    "fan_mode": "FAN_IN",
    "uniform_bound": 0.25,
    "random_stddev": 0.01,
    "dropout": 0.0
  },
  "optimizer": {
    "optimizer_type": "Adam",
    "learning_rate": 0.008,
    "adadelta_decay_rate": 0.95,
    "adadelta_epsilon": 1e-08
  },
  "TextCNN": {
    "kernel_sizes": [
      2,
      3,
      4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1
  },
  "TextRNN": {
    "hidden_dimension": 64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "doc_embedding_type": "Attention",
    "attention_dimension": 16,
    "bidirectional": true
  },
  "DRNN": {
    "hidden_dimension": 5,
    "window_size": 3,
    "rnn_type": "GRU",
    "bidirectional": true,
    "cell_hidden_dropout": 0.1
  },
  "eval": {
    "text_file": "data/rcv1_test.json",
    "threshold": 0.5,
    "dir": "eval_dir",
    "batch_size": 1024,
    "is_flat": true,
    "top_k": 100,
    "model_dir": "checkpoint_dir_rcv1/TextCNN_best"
  },
  "TextVDCNN": {
    "vdcnn_depth": 9,
    "top_k_max_pooling": 8
  },
  "DPCNN": {
    "kernel_size": 3,
    "pooling_stride": 2,
    "num_kernels": 16,
    "blocks": 2
  },
  "TextRCNN": {
    "kernel_sizes": [
        2,
        3,
        4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1,
    "hidden_dimension":64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "bidirectional": true
  },
  "Transformer": {
    "d_inner": 128,
    "d_k": 32,
    "d_v": 32,
    "n_head": 4,
    "n_layers": 1,
    "dropout": 0.1,
    "use_star": true
  },
  "AttentiveConvNet": {
    "attention_type": "bilinear",
    "margin_size": 3,
    "type": "advanced",
    "hidden_size": 64
  },
  "HMCN": {
    "hierarchical_depth": [0, 384, 384, 384, 384],
    "global2local": [0, 16, 192, 512, 64]
  },
  "log": {
    "logger_file": "log_test_rcv1_hierar",
    "log_level": "warn"
  }
}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$
```

Test run with the train.json config file ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python train.py conf/train.json
Use dataset to generate dict.
Size of doc_label dict is 102
Size of doc_token dict is 114596
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 102
Size of doc_token dict is 95439
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.882136, recall: 0.680969, fscore: 0.768607, macro-fscore: 0.355140, right: 45138, predict: 51169, standard: 66285.
Loss is: 0.062705.
Validate performance at epoch 1 is precision: 0.857013, recall: 0.636400, fscore: 0.730412, macro-fscore: 0.302818, right: 4717, predict: 5504, standard: 7412.
Loss is: 0.068822.
test performance at epoch 1 is precision: 0.849177, recall: 0.587261, fscore: 0.694340, macro-fscore: 0.275595, right: 15213, predict: 17915, standard: 25905.
Loss is: 0.073764.
Epoch 1 cost time: 33 second
Train performance at epoch 2 is precision: 0.886501, recall: 0.779000, fscore: 0.829281, macro-fscore: 0.532763, right: 51636, predict: 58247, standard: 66285.
Loss is: 0.047256.
Validate performance at epoch 2 is precision: 0.832732, recall: 0.685105, fscore: 0.751739, macro-fscore: 0.397822, right: 5078, predict: 6098, standard: 7412.
Loss is: 0.058962.
test performance at epoch 2 is precision: 0.827320, recall: 0.640842, fscore: 0.722238, macro-fscore: 0.358285, right: 16601, predict: 20066, standard: 25905.
Loss is: 0.064304.
Epoch 2 cost time: 32 second
Train performance at epoch 3 is precision: 0.886586, recall: 0.853255, fscore: 0.869601, macro-fscore: 0.677150, right: 56558, predict: 63793, standard: 66285.
Loss is: 0.039287.
Validate performance at epoch 3 is precision: 0.808711, recall: 0.741500, fscore: 0.773649, macro-fscore: 0.465489, right: 5496, predict: 6796, standard: 7412.
Loss is: 0.054251.
test performance at epoch 3 is precision: 0.801368, recall: 0.682764, fscore: 0.737327, macro-fscore: 0.421109, right: 17687, predict: 22071, standard: 25905.
Loss is: 0.060632.
Epoch 3 cost time: 32 second
Train performance at epoch 4 is precision: 0.913931, recall: 0.850962, fscore: 0.881323, macro-fscore: 0.682722, right: 56406, predict: 61718, standard: 66285.
Loss is: 0.031664.
Validate performance at epoch 4 is precision: 0.841375, recall: 0.719914, fscore: 0.775920, macro-fscore: 0.486596, right: 5336, predict: 6342, standard: 7412.
Loss is: 0.049509.
test performance at epoch 4 is precision: 0.817906, recall: 0.655935, fscore: 0.728021, macro-fscore: 0.405415, right: 16992, predict: 20775, standard: 25905.
Loss is: 0.056676.
Epoch 4 cost time: 32 second
Train performance at epoch 5 is precision: 0.909995, recall: 0.879641, fscore: 0.894560, macro-fscore: 0.734128, right: 58307, predict: 64074, standard: 66285.
Loss is: 0.028702.
Validate performance at epoch 5 is precision: 0.820855, recall: 0.730707, fscore: 0.773162, macro-fscore: 0.500457, right: 5416, predict: 6598, standard: 7412.
Loss is: 0.049231.
test performance at epoch 5 is precision: 0.805853, recall: 0.651650, fscore: 0.720594, macro-fscore: 0.430369, right: 16881, predict: 20948, standard: 25905.
Loss is: 0.056870.
Epoch 5 cost time: 32 second
Best test performance at epoch 4 is precision: 0.817906, recall: 0.655935, fscore: 0.728021, macro-fscore: 0.405415, right: 16992, predict: 20775, standard: 25905.
Loss is: 0.056676.

real    3m0.974s
user    8m5.646s
sys     0m30.197s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

output model တွေက အောက်ပါအတိုင်း ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/checkpoint_dir_rcv1$ ls
TextCNN_1  TextCNN_2  TextCNN_3  TextCNN_4  TextCNN_5  TextCNN_best
```

## Testing-2


Check the train.hierar.json configuration file ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$ cat train.hierar.json
{
  "task_info": {
    "label_type": "multi_label",
    "hierarchical": true,
    "hierar_taxonomy": "data/rcv1.taxonomy",
    "hierar_penalty": 0.000001
  },
  "device": "cuda",
  "model_name": "TextRNN",
  "checkpoint_dir": "checkpoint_dir_rcv1",
  "model_dir": "trained_model_rcv1",
  "data": {
    "train_json_files": [
      "data/rcv1_train.hierar.json"
    ],
    "validate_json_files": [
      "data/rcv1_dev.hierar.json"
    ],
    "test_json_files": [
      "data/rcv1_test.hierar.json"
    ],
    "generate_dict_using_json_files": true,
    "generate_dict_using_all_json_files": true,
    "generate_dict_using_pretrained_embedding": false,
    "generate_hierarchy_label": true,
    "dict_dir": "dict_rcv1",
    "num_worker": 4
  },
  "feature": {
    "feature_names": [
      "token"
    ],
    "min_token_count": 2,
    "min_char_count": 2,
    "token_ngram": 0,
    "min_token_ngram_count": 0,
    "min_keyword_count": 0,
    "min_topic_count": 2,
    "max_token_dict_size": 1000000,
    "max_char_dict_size": 150000,
    "max_token_ngram_dict_size": 10000000,
    "max_keyword_dict_size": 100,
    "max_topic_dict_size": 100,
    "max_token_len": 256,
    "max_char_len": 1024,
    "max_char_len_per_token": 4,
    "token_pretrained_file": "",
    "keyword_pretrained_file": ""
  },
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 50,
    "num_epochs_static_embedding": 0,
    "decay_steps": 1000,
    "decay_rate": 1.0,
    "clip_gradients": 100.0,
    "l2_lambda": 0.0,
    "loss_type": "BCEWithLogitsLoss",
    "sampler": "fixed",
    "num_sampled": 5,
    "visible_device_list": "0",
    "hidden_layer_dropout": 0.5
  },
  "embedding": {
    "type": "embedding",
    "dimension": 64,
    "region_embedding_type": "context_word",
    "region_size": 5,
    "initializer": "uniform",
    "fan_mode": "FAN_IN",
    "uniform_bound": 0.25,
    "random_stddev": 0.01,
    "dropout": 0.0
  },
  "optimizer": {
    "optimizer_type": "Adam",
    "learning_rate": 0.008,
    "adadelta_decay_rate": 0.95,
    "adadelta_epsilon": 1e-08
  },
  "TextCNN": {
    "kernel_sizes": [
      2,
      3,
      4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1
  },
  "TextRNN": {
    "hidden_dimension": 64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "doc_embedding_type": "Attention",
    "attention_dimension": 16,
    "bidirectional": true
  },
  "DRNN": {
    "hidden_dimension": 5,
    "window_size": 3,
    "rnn_type": "GRU",
    "bidirectional": true,
    "cell_hidden_dropout": 0.1
  },
  "eval": {
    "text_file": "data/rcv1_test.hierar.json",
    "threshold": 0.5,
    "dir": "eval_dir",
    "batch_size": 1024,
    "is_flat": true,
    "top_k": 100,
    "model_dir": "checkpoint_dir_rcv1/TextRNN_best"
  },
  "TextVDCNN": {
    "vdcnn_depth": 9,
    "top_k_max_pooling": 8
  },
  "DPCNN": {
    "kernel_size": 3,
    "pooling_stride": 2,
    "num_kernels": 16,
    "blocks": 2
  },
  "TextRCNN": {
    "kernel_sizes": [
        2,
        3,
        4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1,
    "hidden_dimension":64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "bidirectional": true
  },
  "Transformer": {
    "d_inner": 128,
    "d_k": 32,
    "d_v": 32,
    "n_head": 4,
    "n_layers": 1,
    "dropout": 0.1,
    "use_star": true
  },
  "AttentiveConvNet": {
    "attention_type": "bilinear",
    "margin_size": 3,
    "type": "advanced",
    "hidden_size": 64
  },
  "HMCN": {
    "hierarchical_depth": [0, 384, 384, 384, 384],
    "global2local": [0, 4, 55, 43, 1]
  },
  "log": {
    "logger_file": "log_test_rcv1_hierar",
    "log_level": "warn"
  }
}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$
```

For this time train with Hierar ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python train.py conf/train.hierar.json
Use dataset to generate dict.
Size of doc_label dict is 102
Size of doc_token dict is 114596
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 102
Size of doc_token dict is 95439
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.776508, recall: 0.544002, fscore: 0.639786, macro-fscore: 0.291783, right: 17129, predict: 22059, standard: 31487.
Loss is: 0.064779.
Validate performance at epoch 1 is precision: 0.759714, recall: 0.484477, fscore: 0.591652, macro-fscore: 0.255130, right: 1701, predict: 2239, standard: 3511.
Loss is: 0.067201.
test performance at epoch 1 is precision: 0.747625, recall: 0.421921, fscore: 0.539420, macro-fscore: 0.230689, right: 5193, predict: 6946, standard: 12308.
Loss is: 0.069657.
Epoch 1 cost time: 36 second
Train performance at epoch 2 is precision: 0.857760, recall: 0.680852, fscore: 0.759136, macro-fscore: 0.485970, right: 21438, predict: 24993, standard: 31487.
Loss is: 0.040860.
Validate performance at epoch 2 is precision: 0.796818, recall: 0.556252, fscore: 0.655149, macro-fscore: 0.361733, right: 1953, predict: 2451, standard: 3511.
Loss is: 0.045879.
test performance at epoch 2 is precision: 0.798575, recall: 0.482532, fscore: 0.601570, macro-fscore: 0.318036, right: 5939, predict: 7437, standard: 12308.
Loss is: 0.048847.
Epoch 2 cost time: 35 second
Train performance at epoch 3 is precision: 0.886943, recall: 0.804268, fscore: 0.843585, macro-fscore: 0.628786, right: 25324, predict: 28552, standard: 31487.
Loss is: 0.037235.
Validate performance at epoch 3 is precision: 0.792995, recall: 0.644831, fscore: 0.711279, macro-fscore: 0.459574, right: 2264, predict: 2855, standard: 3511.
Loss is: 0.044127.
test performance at epoch 3 is precision: 0.778323, recall: 0.541436, fscore: 0.638620, macro-fscore: 0.379475, right: 6664, predict: 8562, standard: 12308.
Loss is: 0.047763.
Epoch 3 cost time: 35 second
Train performance at epoch 4 is precision: 0.945242, recall: 0.815225, fscore: 0.875433, macro-fscore: 0.681201, right: 25669, predict: 27156, standard: 31487.
Loss is: 0.025097.
Validate performance at epoch 4 is precision: 0.846491, recall: 0.604671, fscore: 0.705433, macro-fscore: 0.454327, right: 2123, predict: 2508, standard: 3511.
Loss is: 0.033618.
test performance at epoch 4 is precision: 0.840564, recall: 0.499025, fscore: 0.626255, macro-fscore: 0.368482, right: 6142, predict: 7307, standard: 12308.
Loss is: 0.037832.
Epoch 4 cost time: 35 second
Train performance at epoch 5 is precision: 0.950203, recall: 0.861149, fscore: 0.903487, macro-fscore: 0.739059, right: 27115, predict: 28536, standard: 31487.
Loss is: 0.020143.
Validate performance at epoch 5 is precision: 0.835190, recall: 0.619197, fscore: 0.711155, macro-fscore: 0.473202, right: 2174, predict: 2603, standard: 3511.
Loss is: 0.030639.
test performance at epoch 5 is precision: 0.822291, recall: 0.517306, fscore: 0.635081, macro-fscore: 0.375152, right: 6367, predict: 7743, standard: 12308.
Loss is: 0.034747.
Epoch 5 cost time: 35 second
Train performance at epoch 6 is precision: 0.945222, recall: 0.906977, fscore: 0.925705, macro-fscore: 0.803675, right: 28558, predict: 30213, standard: 31487.
Loss is: 0.018006.
Validate performance at epoch 6 is precision: 0.806676, recall: 0.660780, fscore: 0.726476, macro-fscore: 0.483720, right: 2320, predict: 2876, standard: 3511.
Loss is: 0.030077.
test performance at epoch 6 is precision: 0.784876, recall: 0.548993, fscore: 0.646077, macro-fscore: 0.403954, right: 6757, predict: 8609, standard: 12308.
Loss is: 0.034407.
Epoch 6 cost time: 35 second
Train performance at epoch 7 is precision: 0.954985, recall: 0.919681, fscore: 0.937000, macro-fscore: 0.812118, right: 28958, predict: 30323, standard: 31487.
Loss is: 0.015853.
Validate performance at epoch 7 is precision: 0.818084, recall: 0.649388, fscore: 0.724039, macro-fscore: 0.506940, right: 2280, predict: 2787, standard: 3511.
Loss is: 0.028928.
test performance at epoch 7 is precision: 0.791459, recall: 0.528518, fscore: 0.633799, macro-fscore: 0.392267, right: 6505, predict: 8219, standard: 12308.
Loss is: 0.033586.
Epoch 7 cost time: 35 second
Train performance at epoch 8 is precision: 0.955097, recall: 0.928161, fscore: 0.941436, macro-fscore: 0.827727, right: 29225, predict: 30599, standard: 31487.
Loss is: 0.013868.
Validate performance at epoch 8 is precision: 0.801213, recall: 0.639419, fscore: 0.711231, macro-fscore: 0.491665, right: 2245, predict: 2802, standard: 3511.
Loss is: 0.028307.
test performance at epoch 8 is precision: 0.773444, recall: 0.522018, fscore: 0.623333, macro-fscore: 0.394942, right: 6425, predict: 8307, standard: 12308.
Loss is: 0.033312.
Epoch 8 cost time: 36 second
Train performance at epoch 9 is precision: 0.964611, recall: 0.940992, fscore: 0.952655, macro-fscore: 0.856347, right: 29629, predict: 30716, standard: 31487.
Loss is: 0.013268.
Validate performance at epoch 9 is precision: 0.814828, recall: 0.647964, fscore: 0.721878, macro-fscore: 0.519424, right: 2275, predict: 2792, standard: 3511.
Loss is: 0.028445.
test performance at epoch 9 is precision: 0.786893, recall: 0.515112, fscore: 0.622637, macro-fscore: 0.418313, right: 6340, predict: 8057, standard: 12308.
Loss is: 0.033577.
Epoch 9 cost time: 37 second
Train performance at epoch 10 is precision: 0.966496, recall: 0.950964, fscore: 0.958667, macro-fscore: 0.849205, right: 29943, predict: 30981, standard: 31487.
Loss is: 0.012023.
Validate performance at epoch 10 is precision: 0.805300, recall: 0.649103, fscore: 0.718814, macro-fscore: 0.506355, right: 2279, predict: 2830, standard: 3511.
Loss is: 0.027733.
test performance at epoch 10 is precision: 0.777511, recall: 0.526974, fscore: 0.628184, macro-fscore: 0.400736, right: 6486, predict: 8342, standard: 12308.
Loss is: 0.032838.
Epoch 10 cost time: 36 second
Train performance at epoch 11 is precision: 0.969694, recall: 0.952171, fscore: 0.960852, macro-fscore: 0.866892, right: 29981, predict: 30918, standard: 31487.
Loss is: 0.011028.
Validate performance at epoch 11 is precision: 0.807598, recall: 0.659926, fscore: 0.726332, macro-fscore: 0.529429, right: 2317, predict: 2869, standard: 3511.
Loss is: 0.027926.
test performance at epoch 11 is precision: 0.777284, recall: 0.525431, fscore: 0.627012, macro-fscore: 0.401018, right: 6467, predict: 8320, standard: 12308.
Loss is: 0.032752.
Epoch 11 cost time: 36 second

Train performance at epoch 12 is precision: 0.973614, recall: 0.950392, fscore: 0.961863, macro-fscore: 0.862532, right: 29925, predict: 30736, standard: 31487.
Loss is: 0.010233.
Validate performance at epoch 12 is precision: 0.805787, recall: 0.634577, fscore: 0.710006, macro-fscore: 0.509487, right: 2228, predict: 2765, standard: 3511.
Loss is: 0.027635.
test performance at epoch 12 is precision: 0.782450, recall: 0.506419, fscore: 0.614876, macro-fscore: 0.391641, right: 6233, predict: 7966, standard: 12308.
Loss is: 0.032917.
Epoch 12 cost time: 36 second
Train performance at epoch 13 is precision: 0.976034, recall: 0.948074, fscore: 0.961851, macro-fscore: 0.843680, right: 29852, predict: 30585, standard: 31487.
Loss is: 0.009747.
Validate performance at epoch 13 is precision: 0.810644, recall: 0.637710, fscore: 0.713853, macro-fscore: 0.498591, right: 2239, predict: 2762, standard: 3511.
Loss is: 0.027558.
test performance at epoch 13 is precision: 0.787921, recall: 0.507719, fscore: 0.617521, macro-fscore: 0.384562, right: 6249, predict: 7931, standard: 12308.
Loss is: 0.033047.
Epoch 13 cost time: 36 second
Train performance at epoch 14 is precision: 0.974105, recall: 0.962937, fscore: 0.968489, macro-fscore: 0.872659, right: 30320, predict: 31126, standard: 31487.
Loss is: 0.009297.
Validate performance at epoch 14 is precision: 0.792984, recall: 0.650242, fscore: 0.714554, macro-fscore: 0.502693, right: 2283, predict: 2879, standard: 3511.
Loss is: 0.027608.
test performance at epoch 14 is precision: 0.767472, recall: 0.523724, fscore: 0.622591, macro-fscore: 0.398376, right: 6446, predict: 8399, standard: 12308.
Loss is: 0.033167.
Epoch 14 cost time: 36 second
Train performance at epoch 15 is precision: 0.969329, recall: 0.964589, fscore: 0.966953, macro-fscore: 0.874380, right: 30372, predict: 31333, standard: 31487.
Loss is: 0.009987.
Validate performance at epoch 15 is precision: 0.796218, recall: 0.647679, fscore: 0.714308, macro-fscore: 0.511212, right: 2274, predict: 2856, standard: 3511.
Loss is: 0.028418.
test performance at epoch 15 is precision: 0.761388, recall: 0.513325, fscore: 0.613219, macro-fscore: 0.393879, right: 6318, predict: 8298, standard: 12308.
Loss is: 0.033931.
Epoch 15 cost time: 37 second
Train performance at epoch 16 is precision: 0.975862, recall: 0.960428, fscore: 0.968084, macro-fscore: 0.900867, right: 30241, predict: 30989, standard: 31487.
Loss is: 0.008659.
Validate performance at epoch 16 is precision: 0.810880, recall: 0.632583, fscore: 0.710720, macro-fscore: 0.494445, right: 2221, predict: 2739, standard: 3511.
Loss is: 0.027668.
test performance at epoch 16 is precision: 0.780929, recall: 0.494394, fscore: 0.605473, macro-fscore: 0.374565, right: 6085, predict: 7792, standard: 12308.
Loss is: 0.033631.
Epoch 16 cost time: 36 second
Train performance at epoch 17 is precision: 0.973207, recall: 0.964398, fscore: 0.968782, macro-fscore: 0.904586, right: 30366, predict: 31202, standard: 31487.
Loss is: 0.009121.
Validate performance at epoch 17 is precision: 0.809847, recall: 0.646539, fscore: 0.719037, macro-fscore: 0.491354, right: 2270, predict: 2803, standard: 3511.
Loss is: 0.028045.
test performance at epoch 17 is precision: 0.785206, recall: 0.510562, fscore: 0.618778, macro-fscore: 0.395980, right: 6284, predict: 8003, standard: 12308.
Loss is: 0.033614.
Epoch 17 cost time: 37 second
Train performance at epoch 18 is precision: 0.972810, recall: 0.966970, fscore: 0.969881, macro-fscore: 0.916774, right: 30447, predict: 31298, standard: 31487.
Loss is: 0.009340.
Validate performance at epoch 18 is precision: 0.780496, recall: 0.645115, fscore: 0.706378, macro-fscore: 0.505905, right: 2265, predict: 2902, standard: 3511.
Loss is: 0.028734.
test performance at epoch 18 is precision: 0.763196, recall: 0.507475, fscore: 0.609604, macro-fscore: 0.392643, right: 6246, predict: 8184, standard: 12308.
Loss is: 0.034548.
Epoch 18 cost time: 37 second
Train performance at epoch 19 is precision: 0.976201, recall: 0.967923, fscore: 0.972045, macro-fscore: 0.900886, right: 30477, predict: 31220, standard: 31487.
Loss is: 0.008647.
Validate performance at epoch 19 is precision: 0.788179, recall: 0.657078, fscore: 0.716682, macro-fscore: 0.517353, right: 2307, predict: 2927, standard: 3511.
Loss is: 0.028065.
test performance at epoch 19 is precision: 0.763606, recall: 0.514137, fscore: 0.614518, macro-fscore: 0.395041, right: 6328, predict: 8287, standard: 12308.
Loss is: 0.034014.
Epoch 19 cost time: 36 second
Train performance at epoch 20 is precision: 0.973454, recall: 0.965478, fscore: 0.969450, macro-fscore: 0.887614, right: 30400, predict: 31229, standard: 31487.
Loss is: 0.008685.
Validate performance at epoch 20 is precision: 0.779437, recall: 0.654230, fscore: 0.711366, macro-fscore: 0.507204, right: 2297, predict: 2947, standard: 3511.
Loss is: 0.028281.
test performance at epoch 20 is precision: 0.749912, recall: 0.516737, fscore: 0.611862, macro-fscore: 0.387753, right: 6360, predict: 8481, standard: 12308.
Loss is: 0.034265.
Epoch 20 cost time: 36 second
Train performance at epoch 21 is precision: 0.970329, recall: 0.974212, fscore: 0.972266, macro-fscore: 0.901294, right: 30675, predict: 31613, standard: 31487.
Loss is: 0.008858.
Validate performance at epoch 21 is precision: 0.767680, recall: 0.661635, fscore: 0.710724, macro-fscore: 0.509050, right: 2323, predict: 3026, standard: 3511.
Loss is: 0.028909.
test performance at epoch 21 is precision: 0.739537, recall: 0.526893, fscore: 0.615363, macro-fscore: 0.387523, right: 6485, predict: 8769, standard: 12308.
Loss is: 0.034692.
Epoch 21 cost time: 37 second
Train performance at epoch 22 is precision: 0.978870, recall: 0.962207, fscore: 0.970467, macro-fscore: 0.887565, right: 30297, predict: 30951, standard: 31487.
Loss is: 0.007879.
Validate performance at epoch 22 is precision: 0.804443, recall: 0.629165, fscore: 0.706089, macro-fscore: 0.482894, right: 2209, predict: 2746, standard: 3511.
Loss is: 0.028703.
test performance at epoch 22 is precision: 0.777650, recall: 0.493013, fscore: 0.603451, macro-fscore: 0.373849, right: 6068, predict: 7803, standard: 12308.
Loss is: 0.034620.
Epoch 22 cost time: 36 second
Train performance at epoch 23 is precision: 0.979839, recall: 0.964684, fscore: 0.972202, macro-fscore: 0.887262, right: 30375, predict: 31000, standard: 31487.
Loss is: 0.007879.
Validate performance at epoch 23 is precision: 0.795027, recall: 0.637425, fscore: 0.707556, macro-fscore: 0.504960, right: 2238, predict: 2815, standard: 3511.
Loss is: 0.029063.
test performance at epoch 23 is precision: 0.766294, recall: 0.484319, fscore: 0.593518, macro-fscore: 0.366197, right: 5961, predict: 7779, standard: 12308.
Loss is: 0.035256.
Epoch 23 cost time: 37 second
Train performance at epoch 24 is precision: 0.973557, recall: 0.969352, fscore: 0.971450, macro-fscore: 0.881531, right: 30522, predict: 31351, standard: 31487.
Loss is: 0.008305.
Validate performance at epoch 24 is precision: 0.782834, recall: 0.646824, fscore: 0.708359, macro-fscore: 0.513222, right: 2271, predict: 2901, standard: 3511.
Loss is: 0.029032.
test performance at epoch 24 is precision: 0.758117, recall: 0.510318, fscore: 0.610013, macro-fscore: 0.395032, right: 6281, predict: 8285, standard: 12308.
Loss is: 0.034672.
Epoch 24 cost time: 36 second
Train performance at epoch 25 is precision: 0.980330, recall: 0.959190, fscore: 0.969644, macro-fscore: 0.902023, right: 30202, predict: 30808, standard: 31487.
Loss is: 0.007702.
Validate performance at epoch 25 is precision: 0.798464, recall: 0.621760, fscore: 0.699119, macro-fscore: 0.474155, right: 2183, predict: 2734, standard: 3511.
Loss is: 0.028966.
test performance at epoch 25 is precision: 0.779172, recall: 0.484482, fscore: 0.597465, macro-fscore: 0.366015, right: 5963, predict: 7653, standard: 12308.
Loss is: 0.035052.
Epoch 25 cost time: 36 second
Train performance at epoch 26 is precision: 0.978961, recall: 0.959094, fscore: 0.968926, macro-fscore: 0.894992, right: 30199, predict: 30848, standard: 31487.
Loss is: 0.007668.
Validate performance at epoch 26 is precision: 0.796760, recall: 0.616349, fscore: 0.695038, macro-fscore: 0.490432, right: 2164, predict: 2716, standard: 3511.
Loss is: 0.029366.
test performance at epoch 26 is precision: 0.770595, recall: 0.476519, fscore: 0.588885, macro-fscore: 0.366856, right: 5865, predict: 7611, standard: 12308.
Loss is: 0.035408.
Epoch 26 cost time: 37 second
Train performance at epoch 27 is precision: 0.977694, recall: 0.959094, fscore: 0.968305, macro-fscore: 0.895369, right: 30199, predict: 30888, standard: 31487.
Loss is: 0.008226.
Validate performance at epoch 27 is precision: 0.788712, recall: 0.620906, fscore: 0.694821, macro-fscore: 0.478340, right: 2180, predict: 2764, standard: 3511.
Loss is: 0.029932.
test performance at epoch 27 is precision: 0.759887, recall: 0.479282, fscore: 0.587813, macro-fscore: 0.368041, right: 5899, predict: 7763, standard: 12308.
Loss is: 0.036096.
Epoch 27 cost time: 36 second
Train performance at epoch 28 is precision: 0.979856, recall: 0.960873, fscore: 0.970271, macro-fscore: 0.904714, right: 30255, predict: 30877, standard: 31487.
Loss is: 0.007590.
Validate performance at epoch 28 is precision: 0.794150, recall: 0.626317, fscore: 0.700318, macro-fscore: 0.465888, right: 2199, predict: 2769, standard: 3511.
Loss is: 0.029257.
test performance at epoch 28 is precision: 0.758782, recall: 0.487894, fscore: 0.593908, macro-fscore: 0.368905, right: 6005, predict: 7914, standard: 12308.
Loss is: 0.035734.
Epoch 28 cost time: 37 second
Train performance at epoch 29 is precision: 0.974334, recall: 0.968114, fscore: 0.971214, macro-fscore: 0.880389, right: 30483, predict: 31286, standard: 31487.
Loss is: 0.008186.
Validate performance at epoch 29 is precision: 0.769993, recall: 0.641698, fscore: 0.700016, macro-fscore: 0.493249, right: 2253, predict: 2926, standard: 3511.
Loss is: 0.029385.
test performance at epoch 29 is precision: 0.733096, recall: 0.502112, fscore: 0.596007, macro-fscore: 0.371198, right: 6180, predict: 8430, standard: 12308.
Loss is: 0.035969.
Epoch 29 cost time: 36 second
Train performance at epoch 30 is precision: 0.975125, recall: 0.964874, fscore: 0.969973, macro-fscore: 0.891944, right: 30381, predict: 31156, standard: 31487.
Loss is: 0.007839.
Validate performance at epoch 30 is precision: 0.781955, recall: 0.622045, fscore: 0.692893, macro-fscore: 0.496542, right: 2184, predict: 2793, standard: 3511.
Loss is: 0.029868.
test performance at epoch 30 is precision: 0.747416, recall: 0.487569, fscore: 0.590156, macro-fscore: 0.366724, right: 6001, predict: 8029, standard: 12308.
Loss is: 0.036499.
Epoch 30 cost time: 37 second
Train performance at epoch 31 is precision: 0.974966, recall: 0.968495, fscore: 0.971720, macro-fscore: 0.917148, right: 30495, predict: 31278, standard: 31487.
Loss is: 0.007699.
Validate performance at epoch 31 is precision: 0.780677, recall: 0.630590, fscore: 0.697652, macro-fscore: 0.507128, right: 2214, predict: 2836, standard: 3511.
Loss is: 0.029347.
test performance at epoch 31 is precision: 0.747964, recall: 0.485132, fscore: 0.588537, macro-fscore: 0.377969, right: 5971, predict: 7983, standard: 12308.
Loss is: 0.036265.
Epoch 31 cost time: 37 second
Train performance at epoch 32 is precision: 0.973218, recall: 0.970591, fscore: 0.971903, macro-fscore: 0.892565, right: 30561, predict: 31402, standard: 31487.
Loss is: 0.008020.
Validate performance at epoch 32 is precision: 0.773462, recall: 0.640843, fscore: 0.700935, macro-fscore: 0.488718, right: 2250, predict: 2909, standard: 3511.
Loss is: 0.030501.
test performance at epoch 32 is precision: 0.741073, recall: 0.497400, fscore: 0.595265, macro-fscore: 0.374011, right: 6122, predict: 8261, standard: 12308.
Loss is: 0.036586.
Epoch 32 cost time: 37 second
Train performance at epoch 33 is precision: 0.972347, recall: 0.972655, fscore: 0.972501, macro-fscore: 0.904234, right: 30626, predict: 31497, standard: 31487.
Loss is: 0.008322.
Validate performance at epoch 33 is precision: 0.763894, recall: 0.645970, fscore: 0.700000, macro-fscore: 0.521662, right: 2268, predict: 2969, standard: 3511.
Loss is: 0.030448.
test performance at epoch 33 is precision: 0.725545, recall: 0.505606, fscore: 0.595930, macro-fscore: 0.381209, right: 6223, predict: 8577, standard: 12308.
Loss is: 0.036351.
Epoch 33 cost time: 38 second
Train performance at epoch 34 is precision: 0.979740, recall: 0.966049, fscore: 0.972847, macro-fscore: 0.895006, right: 30418, predict: 31047, standard: 31487.
Loss is: 0.007331.
Validate performance at epoch 34 is precision: 0.784739, recall: 0.638565, fscore: 0.704146, macro-fscore: 0.515755, right: 2242, predict: 2857, standard: 3511.
Loss is: 0.029661.
test performance at epoch 34 is precision: 0.746952, recall: 0.492850, fscore: 0.593862, macro-fscore: 0.372740, right: 6066, predict: 8121, standard: 12308.
Loss is: 0.035990.
Epoch 34 cost time: 38 second
Train performance at epoch 35 is precision: 0.981631, recall: 0.962302, fscore: 0.971870, macro-fscore: 0.889771, right: 30300, predict: 30867, standard: 31487.
Loss is: 0.007117.
Validate performance at epoch 35 is precision: 0.786025, recall: 0.618342, fscore: 0.692173, macro-fscore: 0.497522, right: 2171, predict: 2762, standard: 3511.
Loss is: 0.030092.
test performance at epoch 35 is precision: 0.756154, recall: 0.474163, fscore: 0.582842, macro-fscore: 0.362643, right: 5836, predict: 7718, standard: 12308.
Loss is: 0.036393.
Epoch 35 cost time: 37 second
Train performance at epoch 36 is precision: 0.980485, recall: 0.968558, fscore: 0.974485, macro-fscore: 0.902816, right: 30497, predict: 31104, standard: 31487.
Loss is: 0.007318.
Validate performance at epoch 36 is precision: 0.783513, recall: 0.622615, fscore: 0.693858, macro-fscore: 0.498613, right: 2186, predict: 2790, standard: 3511.
Loss is: 0.030324.
test performance at epoch 36 is precision: 0.763261, recall: 0.477007, fscore: 0.587100, macro-fscore: 0.380284, right: 5871, predict: 7692, standard: 12308.
Loss is: 0.036568.
Epoch 36 cost time: 37 second
Train performance at epoch 37 is precision: 0.976618, recall: 0.971004, fscore: 0.973803, macro-fscore: 0.904682, right: 30574, predict: 31306, standard: 31487.
Loss is: 0.007457.
Validate performance at epoch 37 is precision: 0.768782, recall: 0.638280, fscore: 0.697479, macro-fscore: 0.508051, right: 2241, predict: 2915, standard: 3511.
Loss is: 0.030467.
test performance at epoch 37 is precision: 0.742552, recall: 0.502194, fscore: 0.599166, macro-fscore: 0.380314, right: 6181, predict: 8324, standard: 12308.
Loss is: 0.036345.
Epoch 37 cost time: 37 second
Train performance at epoch 38 is precision: 0.979287, recall: 0.966970, fscore: 0.973090, macro-fscore: 0.897676, right: 30447, predict: 31091, standard: 31487.
Loss is: 0.007852.
Validate performance at epoch 38 is precision: 0.773772, recall: 0.623469, fscore: 0.690536, macro-fscore: 0.473320, right: 2189, predict: 2829, standard: 3511.
Loss is: 0.030799.
test performance at epoch 38 is precision: 0.745457, recall: 0.479932, fscore: 0.583926, macro-fscore: 0.368126, right: 5907, predict: 7924, standard: 12308.
Loss is: 0.037624.
Epoch 38 cost time: 37 second
Train performance at epoch 39 is precision: 0.982474, recall: 0.966748, fscore: 0.974548, macro-fscore: 0.912017, right: 30440, predict: 30983, standard: 31487.
Loss is: 0.007274.
Validate performance at epoch 39 is precision: 0.778017, recall: 0.616918, fscore: 0.688165, macro-fscore: 0.495491, right: 2166, predict: 2784, standard: 3511.
Loss is: 0.030365.
test performance at epoch 39 is precision: 0.753567, recall: 0.472051, fscore: 0.580478, macro-fscore: 0.365034, right: 5810, predict: 7710, standard: 12308.
Loss is: 0.037411.
Epoch 39 cost time: 37 second
Train performance at epoch 40 is precision: 0.978543, recall: 0.968940, fscore: 0.973717, macro-fscore: 0.884471, right: 30509, predict: 31178, standard: 31487.
Loss is: 0.007664.
Validate performance at epoch 40 is precision: 0.755717, recall: 0.621191, fscore: 0.681882, macro-fscore: 0.471311, right: 2181, predict: 2886, standard: 3511.
Loss is: 0.031233.
test performance at epoch 40 is precision: 0.735126, recall: 0.479851, fscore: 0.580671, macro-fscore: 0.365328, right: 5906, predict: 8034, standard: 12308.
Loss is: 0.037886.
Epoch 40 cost time: 38 second
Train performance at epoch 41 is precision: 0.975678, recall: 0.969543, fscore: 0.972601, macro-fscore: 0.907477, right: 30528, predict: 31289, standard: 31487.
Loss is: 0.007698.
Validate performance at epoch 41 is precision: 0.758941, recall: 0.628596, fscore: 0.687646, macro-fscore: 0.493173, right: 2207, predict: 2908, standard: 3511.
Loss is: 0.032021.
test performance at epoch 41 is precision: 0.727562, recall: 0.483425, fscore: 0.580885, macro-fscore: 0.366826, right: 5950, predict: 8178, standard: 12308.
Loss is: 0.037906.
Epoch 41 cost time: 37 second
Train performance at epoch 42 is precision: 0.979143, recall: 0.954203, fscore: 0.966512, macro-fscore: 0.874560, right: 30045, predict: 30685, standard: 31487.
Loss is: 0.007562.
Validate performance at epoch 42 is precision: 0.779617, recall: 0.603532, fscore: 0.680366, macro-fscore: 0.472532, right: 2119, predict: 2718, standard: 3511.
Loss is: 0.030933.
test performance at epoch 42 is precision: 0.751875, recall: 0.456207, fscore: 0.567860, macro-fscore: 0.338327, right: 5615, predict: 7468, standard: 12308.
Loss is: 0.038474.
Epoch 42 cost time: 36 second
Train performance at epoch 43 is precision: 0.973860, recall: 0.964303, fscore: 0.969058, macro-fscore: 0.890444, right: 30363, predict: 31178, standard: 31487.
Loss is: 0.008062.
Validate performance at epoch 43 is precision: 0.754093, recall: 0.616633, fscore: 0.678471, macro-fscore: 0.477661, right: 2165, predict: 2871, standard: 3511.
Loss is: 0.031858.
test performance at epoch 43 is precision: 0.720210, recall: 0.479769, fscore: 0.575901, macro-fscore: 0.355154, right: 5905, predict: 8199, standard: 12308.
Loss is: 0.038150.
Epoch 43 cost time: 37 second
Train performance at epoch 44 is precision: 0.974652, recall: 0.957379, fscore: 0.965938, macro-fscore: 0.892510, right: 30145, predict: 30929, standard: 31487.
Loss is: 0.008103.
Validate performance at epoch 44 is precision: 0.765270, recall: 0.613785, fscore: 0.681208, macro-fscore: 0.484046, right: 2155, predict: 2816, standard: 3511.
Loss is: 0.031948.
test performance at epoch 44 is precision: 0.733588, recall: 0.468476, fscore: 0.571797, macro-fscore: 0.353358, right: 5766, predict: 7860, standard: 12308.
Loss is: 0.038974.
Epoch 44 cost time: 37 second
Train performance at epoch 45 is precision: 0.976112, recall: 0.965510, fscore: 0.970782, macro-fscore: 0.881686, right: 30401, predict: 31145, standard: 31487.
Loss is: 0.008037.
Validate performance at epoch 45 is precision: 0.755631, recall: 0.630590, fscore: 0.687471, macro-fscore: 0.481749, right: 2214, predict: 2930, standard: 3511.
Loss is: 0.031909.
test performance at epoch 45 is precision: 0.727582, recall: 0.486513, fscore: 0.583114, macro-fscore: 0.353633, right: 5988, predict: 8230, standard: 12308.
Loss is: 0.038439.
Epoch 45 cost time: 37 second

Train performance at epoch 46 is precision: 0.972478, recall: 0.956109, fscore: 0.964224, macro-fscore: 0.886852, right: 30105, predict: 30957, standard: 31487.
Loss is: 0.008626.
Validate performance at epoch 46 is precision: 0.758500, recall: 0.616349, fscore: 0.680075, macro-fscore: 0.463410, right: 2164, predict: 2853, standard: 3511.
Loss is: 0.032834.
test performance at epoch 46 is precision: 0.721284, recall: 0.482125, fscore: 0.577940, macro-fscore: 0.350018, right: 5934, predict: 8227, standard: 12308.
Loss is: 0.038843.
Epoch 46 cost time: 37 second
Train performance at epoch 47 is precision: 0.964125, recall: 0.948264, fscore: 0.956129, macro-fscore: 0.832657, right: 29858, predict: 30969, standard: 31487.
Loss is: 0.009535.
Validate performance at epoch 47 is precision: 0.740676, recall: 0.605241, fscore: 0.666144, macro-fscore: 0.453410, right: 2125, predict: 2869, standard: 3511.
Loss is: 0.033700.
test performance at epoch 47 is precision: 0.703788, recall: 0.475463, fscore: 0.567522, macro-fscore: 0.337447, right: 5852, predict: 8315, standard: 12308.
Loss is: 0.040009.
Epoch 47 cost time: 37 second
Train performance at epoch 48 is precision: 0.962856, recall: 0.951694, fscore: 0.957243, macro-fscore: 0.878249, right: 29966, predict: 31122, standard: 31487.
Loss is: 0.009924.
Validate performance at epoch 48 is precision: 0.735914, recall: 0.606380, fscore: 0.664897, macro-fscore: 0.449404, right: 2129, predict: 2893, standard: 3511.
Loss is: 0.033815.
test performance at epoch 48 is precision: 0.695391, recall: 0.479282, fscore: 0.567457, macro-fscore: 0.342397, right: 5899, predict: 8483, standard: 12308.
Loss is: 0.040257.
Epoch 48 cost time: 37 second
Train performance at epoch 49 is precision: 0.959274, recall: 0.953790, fscore: 0.956525, macro-fscore: 0.879951, right: 30032, predict: 31307, standard: 31487.
Loss is: 0.009759.
Validate performance at epoch 49 is precision: 0.729571, recall: 0.600114, fscore: 0.658540, macro-fscore: 0.455048, right: 2107, predict: 2888, standard: 3511.
Loss is: 0.034230.
test performance at epoch 49 is precision: 0.693992, recall: 0.473919, fscore: 0.563221, macro-fscore: 0.349318, right: 5833, predict: 8405, standard: 12308.
Loss is: 0.040278.
Epoch 49 cost time: 37 second
Train performance at epoch 50 is precision: 0.956475, recall: 0.936609, fscore: 0.946438, macro-fscore: 0.862462, right: 29491, predict: 30833, standard: 31487.
Loss is: 0.011097.
Validate performance at epoch 50 is precision: 0.723242, recall: 0.594702, fscore: 0.652704, macro-fscore: 0.433095, right: 2088, predict: 2887, standard: 3511.
Loss is: 0.035054.
test performance at epoch 50 is precision: 0.680805, recall: 0.459051, fscore: 0.548357, macro-fscore: 0.339398, right: 5650, predict: 8299, standard: 12308.
Loss is: 0.041672.
Epoch 50 cost time: 37 second
Best test performance at epoch 6 is precision: 0.784876, recall: 0.548993, fscore: 0.646077, macro-fscore: 0.403954, right: 6757, predict: 8609, standard: 12308.
Loss is: 0.034407.

real    31m6.191s
user    90m36.365s
sys     4m50.431s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

check the checkpoint outputs:  
 ရှေ့က run ထားတဲ့ output folder နဲ့ setting အတူတူ ထားထားတာကို ဂရုပြုမိ ...  
 
```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/checkpoint_dir_rcv1$ ls
TextCNN_1     TextRNN_13  TextRNN_22  TextRNN_31  TextRNN_40  TextRNN_5
TextCNN_2     TextRNN_14  TextRNN_23  TextRNN_32  TextRNN_41  TextRNN_50
TextCNN_3     TextRNN_15  TextRNN_24  TextRNN_33  TextRNN_42  TextRNN_6
TextCNN_4     TextRNN_16  TextRNN_25  TextRNN_34  TextRNN_43  TextRNN_7
TextCNN_5     TextRNN_17  TextRNN_26  TextRNN_35  TextRNN_44  TextRNN_8
TextCNN_best  TextRNN_18  TextRNN_27  TextRNN_36  TextRNN_45  TextRNN_9
TextRNN_1     TextRNN_19  TextRNN_28  TextRNN_37  TextRNN_46  TextRNN_best
TextRNN_10    TextRNN_2   TextRNN_29  TextRNN_38  TextRNN_47
TextRNN_11    TextRNN_20  TextRNN_3   TextRNN_39  TextRNN_48
TextRNN_12    TextRNN_21  TextRNN_30  TextRNN_4   TextRNN_49
```

## Testing-3


Check the train.hmcn.json config file ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$ cat train.hmcn.json
{
  "task_info": {
    "label_type": "multi_label",
    "hierarchical": true,
    "hierar_taxonomy": "data/rcv1.taxonomy",
    "hierar_penalty": 1e-5
  },
  "device": "cuda",
  "model_name": "HMCN",
  "checkpoint_dir": "checkpoint_dir_rcv1",
  "model_dir": "trained_model_rcv1",
  "data": {
    "train_json_files": [
      "data/rcv1_train.hierar.json"
    ],
    "validate_json_files": [
      "data/rcv1_dev.hierar.json"
    ],
    "test_json_files": [
      "data/rcv1_test.hierar.json"
    ],
    "generate_dict_using_json_files": true,
    "generate_dict_using_all_json_files": true,
    "generate_dict_using_pretrained_embedding": false,
    "generate_hierarchy_label": true,
    "dict_dir": "dict_rcv1",
    "num_worker": 4
  },
  "feature": {
    "feature_names": [
      "token"
    ],
    "min_token_count": 2,
    "min_char_count": 2,
    "token_ngram": 0,
    "min_token_ngram_count": 0,
    "min_keyword_count": 0,
    "min_topic_count": 2,
    "max_token_dict_size": 1000000,
    "max_char_dict_size": 150000,
    "max_token_ngram_dict_size": 10000000,
    "max_keyword_dict_size": 100,
    "max_topic_dict_size": 100,
    "max_token_len": 256,
    "max_char_len": 1024,
    "max_char_len_per_token": 4,
    "token_pretrained_file": "",
    "keyword_pretrained_file": ""
  },
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 50,
    "num_epochs_static_embedding": 0,
    "decay_steps": 1000,
    "decay_rate": 1.0,
    "clip_gradients": 100.0,
    "l2_lambda": 0.0,
    "loss_type": "BCEWithLogitsLoss",
    "sampler": "fixed",
    "num_sampled": 5,
    "visible_device_list": "0",
    "hidden_layer_dropout": 0.5
  },
  "embedding": {
    "type": "embedding",
    "dimension": 64,
    "region_embedding_type": "context_word",
    "region_size": 5,
    "initializer": "uniform",
    "fan_mode": "FAN_IN",
    "uniform_bound": 0.25,
    "random_stddev": 0.01,
    "dropout": 0.0
  },
  "optimizer": {
    "optimizer_type": "Adam",
    "learning_rate": 0.008,
    "adadelta_decay_rate": 0.95,
    "adadelta_epsilon": 1e-08
  },
  "TextCNN": {
    "kernel_sizes": [
      2,
      3,
      4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1
  },
  "TextRNN": {
    "hidden_dimension": 64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "doc_embedding_type": "Attention",
    "attention_dimension": 16,
    "bidirectional": true
  },
  "DRNN": {
    "hidden_dimension": 5,
    "window_size": 3,
    "rnn_type": "GRU",
    "bidirectional": true,
    "cell_hidden_dropout": 0.1
  },
  "eval": {
    "text_file": "data/rcv1_test.hierar.json",
    "threshold": 0.5,
    "dir": "eval_dir",
    "batch_size": 1024,
    "is_flat": true,
    "top_k": 100,
    "model_dir": "checkpoint_dir_rcv1/HMCN_best"
  },
  "TextVDCNN": {
    "vdcnn_depth": 9,
    "top_k_max_pooling": 8
  },
  "DPCNN": {
    "kernel_size": 3,
    "pooling_stride": 2,
    "num_kernels": 16,
    "blocks": 2
  },
  "TextRCNN": {
    "kernel_sizes": [
        2,
        3,
        4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1,
    "hidden_dimension":64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "bidirectional": true
  },
  "Transformer": {
    "d_inner": 128,
    "d_k": 32,
    "d_v": 32,
    "n_head": 4,
    "n_layers": 1,
    "dropout": 0.1,
    "use_star": true
  },
  "AttentiveConvNet": {
    "attention_type": "bilinear",
    "margin_size": 3,
    "type": "advanced",
    "hidden_size": 64
  },
  "HMCN": {
    "hierarchical_depth": [0, 384, 384, 384, 384],
    "global2local": [0, 4, 55, 43, 1]
  },
  "log": {
    "logger_file": "log_test_rcv1_hierar",
    "log_level": "warn"
  }
}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf$
```

tree test data ရဲ့ format ကို လေ့လာခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/data$ head ./rcv1_test.hierar.json
{"doc_label": ["ECAT--E13--E131", "ECAT--E21--E211"], "doc_token": ["Sri", "Lankan", "Deputy", "Finance", "Minister", "GL", "Peiris", "said", "estimated", "average", "annual", "inflation", "percent", "calendar", "percent", "We", "succeeded", "lowering", "rate", "inflation", "single", "digit", "level", "level", "past", "two", "years", "accelerated", "currently", "averages", "around", "percent", "Peiris", "told", "parliament", "presented", "governments", "annual", "budget", "calendar", "Inflation", "spurred", "lower", "farm", "output", "drought", "higher", "international", "prices", "commodities", "like", "crude", "oil", "wheat", "sugar", "higher", "defence", "spending", "said"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["CCAT--C11", "CCAT--C18--C181"], "doc_token": ["Viag", "chairman", "Georg", "Obermeier", "said", "Thursday", "Viag", "British", "Telecom", "plan", "crossshareholdings", "merge", "German", "telecommunications", "activities", "Responding", "reporters", "question", "Obermeier", "said", "Absolutely", "not", "We", "thinking", "crossshareholdings", "We", "consider", "sensible", "Obermeier", "added", "companies", "would", "quickly", "move", "form", "new", "joint", "company", "would", "give", "details", "equity", "division", "name", "company", "capital", "Viag", "BT", "hit", "Wednesday", "Obermeier", "called", "abrupt", "departure", "electrical", "utility", "RWE", "AG", "telecoms", "alliance", "link", "instead", "Veba", "AG", "Cable", "&", "Wireless", "Plc", "BT", "Viag", "seeking", "new", "partners", "join", "efforts", "crack", "German", "telecoms", "market", "Deutsche", "Telekom", "AG", "monopoly", "deregulation", "Bonn", "newsroom"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["CCAT--C15--C152"], "doc_token": ["Fingerhut", "Cos", "Inc", "Chairman", "Theodore", "Deikel", "said", "Tuesday", "expects", "company", "meet", "beat", "Wall", "Streets", "expectations", "earnings", "share", "Speaking", "annual", "meeting", "Deikel", "added", "management", "also", "comfortable", "Wall", "Street", "consensus", "share", "second", "quarter", "In", "Fingerhut", "earned", "share", "For", "yearago", "second", "quarter", "earned", "share", "Looking", "ahead", "Deikel", "told", "shareholders", "company", "focus", "new", "uses", "extensive", "database", "customers", "Fine", "tuning", "database", "allow", "Fingerhut", "send", "fewer", "catalogs", "expected", "million", "compared", "million", "higher", "sales", "added", "Fingerhut", "database", "marketing", "company", "selling", "broad", "range", "products", "services", "Using", "technology", "Internet", "Fingerhut", "plans", "expand", "globally", "year", "Deikel", "said", "company", "plans", "sell", "goods", "United", "Kingdom", "Internet", "end", "Deikel", "also", "said", "Fingerhut", "plans", "expand", "efforts", "credit", "business", "Metris", "Cos", "financial", "services", "subsidiary", "The", "company", "aiming", "grow", "credit", "card", "customer", "base", "approximately", "million", "million", "added", "Reuters", "Chicago", "Newsdesk"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["CCAT--C15--C151--C1511"], "doc_token": ["Calendar", "million", "Sfr", "unless", "stated", "Group", "net", "pct", "Div", "share", "vs", "Turnover", "pct", "Ordinary", "operating", "profit", "pct", "NOTE", "Fotolabo", "SA", "said", "said", "took", "million", "francs", "restructuring", "charges", "EBITDA", "changes", "net", "working", "capital", "rose", "percent", "million", "The", "drop", "net", "profit", "reflected", "losses", "photo", "booth", "activities", "higher", "taxes", "Zurich", "newsroom"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["CCAT--C14", "CCAT--C17--C171", "CCAT--C18--C183"], "doc_token": ["The", "subscription", "price", "international", "placement", "million", "shares", "Hungarian", "chemical", "company", "Borsodchem", "set", "forints/share", "/Global", "Depositary", "Receipt", "GDR", "Budapest", "Stock", "Exchange", "BSE", "said", "statement", "Monday", "The", "placement", "allowed", "seller", "Hungarys", "state", "privatisation", "agency", "APV", "Rt", "raise", "billion", "forints", "million", "BSE", "said"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["MCAT--M14--M141"], "doc_token": ["LIFFE", "cocoa", "futures", "edged", "slightly", "routine", "rangebound", "trade", "dominated", "March/March", "switches", "traders", "said", "The", "market", "dead", "trading", "narrow", "ranges", "said", "one", "The", "dominant", "feature", "March", "/March", "switches", "traded", "around", "stg", "The", "deals", "done", "morning", "volume", "noted", "afternoon", "traders", "said", "By", "close", "nearby", "March", "two", "stg", "tonne", "ranging", "within", "narrow", "five", "stg", "band", "Overall", "volume", "lots", "nearby", "March", "accounting", "Without", "major", "marketmoving", "news", "traders", "said", "market", "could", "see", "low", "volumes", "industry", "fund", "buying", "end", "year", "We", "seen", "good", "quality", "buying", "industry", "time", "now", "one", "said", "Until", "good", "quality", "buying", "I", "think", "market", "hold", "level", "He", "saw", "funds", "holding", "current", "positions", "building", "new", "big", "positions", "early", "In", "fundamental", "news", "head", "Ghanas", "Cocoa", "Board", "told", "reporters", "International", "Cocoa", "Organisation", "meeting", "London", "countrys", "total", "crop", "would", "tonnes", "current", "/", "season", "last", "season", "Traders", "said", "forecast", "within", "trade", "expectation", "But", "Malaysian", "crop", "could", "higher", "previous", "season", "Malaysian", "official", "told", "Reuters", "Production", "expected", "steadily", "increase", "/", "source", "said", "Jalil", "Hamid", "London", "newsroom"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["GCAT--GSPO"], "doc_token": ["Summaries", "Italian", "first", "division", "soccer", "matches", "Sunday", "late", "match", "Parma", "Stanic", "Chiesa", "Lazio", "HT", "Att", "Played", "earlier", "Sunday", "Bologna", "Udinese", "Att", "Cagliari", "Minotti", "Muzzi", "Tovalieri", "pen", "Verona", "Berretta", "og", "De", "Vitis", "HT", "Att", "Fiorentina", "Robbiati", "Juventus", "Del", "Piero", "Red", "card", "Carnasciali", "F", "HT", "Att", "Inter", "Djorkaeff", "Zamorano", "Atalanta", "HT", "Att", "Napoli", "Boghossian", "Sampdoria", "Mihajlovic", "HT", "Att", "Perugia", "Negri", "Milan", "Red", "card", "Dugarry", "M", "Maldini", "M", "HT", "Att", "Roma", "Moriero", "Totti", "Reggiana", "Simutenkov", "Tetradze", "og", "HT", "Att", "Vicenza", "Beghetto", "Piacenza", "Piovani", "HT", "Att"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["MCAT--M14--M143"], "doc_token": ["US", "West", "Coast", "light", "crude", "prices", "edged", "Friday", "line", "broader", "market", "gains", "trading", "minimal", "due", "endofmonth", "pipeline", "scheduling", "Not", "scheduling", "people", "finished", "August", "way", "early", "thinking", "September", "said", "refinery", "crude", "trader", "Regional", "benchmark", "Alaska", "North", "Slope", "ANS", "crude", "last", "traded", "West", "Coast", "market", "midJune", "benchmark", "West", "Texas", "Intermediate/Cushing", "trade", "Friday", "August", "WTI", "hardly", "changed", "day", "/", "cent", "previous", "day", "September", "around", "cents", "/", "Traders", "said", "dominant", "ANS", "seller", "BP", "Oil", "still", "trying", "get", "crude", "buyers", "bidding", "under", "plenty", "alternative", "supply", "available", "There", "four", "refiners", "running", "Ecadorean", "Oriente", "end", "August", "five", "running", "Mexican", "Maya", "said", "one", "trader", "Meanwhile", "Arco", "Pipeline", "Co", "plans", "announce", "apportionment", "Monday", "Line", "major", "pipeline", "Californias", "San", "Joaquin", "Valley", "SJV", "oil", "fields", "Los", "Angeles", "refineries", "New", "York", "Energy", "Desk"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["GCAT--GSPO"], "doc_token": ["Results", "World", "Cup", "Nordic", "skiing", "km", "classic", "crosscountry", "races", "Saturday", "Men", "Mika", "Myllyla", "Finland", "minutes", "two", "seconds", "Erling", "Jevne", "Norway", "Fulvio", "Valbusa", "Italy", "Harri", "Kirvesniemi", "Finland", "Sami", "Repo", "Finland", "Niklas", "Jonsson", "Sweden", "Alois", "Stadlober", "Austria", "Henrik", "Forsberg", "Sweden", "Anders", "Bergstroem", "Sweden", "Oyvind", "Skannes", "Norway", "OddBjorn", "Hjelmeset", "Norway", "Markus", "Gandler", "Austria", "Giorgio", "Vanzetta", "Italy", "Jochen", "Behle", "Germany", "Marco", "Albarello", "Italy", "Women", "Stefania", "Belmondo", "Italy", "Elena", "Vaelbe", "Russia", "Nina", "Gavriliuk", "Russia", "Liubov", "Egorova", "Russia", "Larissa", "Lazutina", "Russia", "Marit", "Mikkelsplass", "Norway", "Olga", "Danilova", "Russia", "Tuulikki", "Pyykkonen", "Finland", "Anita", "MoenGuidon", "Norway", "Bente", "Martinsen", "Norway", "Svetlana", "Nageikina", "Russia", "Julija", "Tschepalova", "Russia", "Trude", "Dybendahl", "Norway", "Sylvia", "Honegger", "Switzerland", "Fumiko", "Aoki", "Japan"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["CCAT--C11", "CCAT--C41"], "doc_token": ["May", "Davis", "Group", "Inc", "said", "Monday", "plans", "launch", "drive", "solicit", "consents", "NetLive", "Communcations", "Inc", "shareholders", "removal", "NetLives", "board", "directors", "elect", "new", "board", "It", "said", "made", "demand", "list", "NetLives", "shareholders", "February", "part", "plans", "May", "Owen", "spokesman", "May", "Davis", "said", "aim", "action", "to", "maximize", "shareholder", "value", "May", "Davis", "undrwrote", "NetLives", "initial", "public", "offering", "August", "said", "intends", "select", "nominees", "NetLive", "board"], "doc_keyword": [], "doc_topic": []}
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/data$
```

taxonomy file က အောက်ပါအတိုင်း ...  

```
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/data$ cat rcv1.taxonomy
Root    CCAT    ECAT    GCAT    MCAT
CCAT    C11     C12     C13     C14     C15     C16     C17     C18     C21     C22     C23       C24     C31     C32     C33     C34     C41     C42
C15     C151    C152
C151    C1511
C17     C171    C172    C173    C174
C18     C181    C182    C183
C31     C311    C312    C313
C33     C331
C41     C411
ECAT    E11     E12     E13     E14     E21     E31     E41     E51     E61     E71
E12     E121
E13     E131    E132
E14     E141    E142    E143
E21     E211    E212
E31     E311    E312    E313
E41     E411
E51     E511    E512    E513
GCAT    G15     GCRIM   GDEF    GDIP    GDIS    GENT    GENV    GFAS    GHEA    GJOB    GMIL      GOBIT   GODD    GPOL    GPRO    GREL    GSCI    GSPO    GTOUR   GVIO    GVOTE   GWEA      GWELF
G15     G151    G152    G153    G154    G155    G156    G157    G158    G159
MCAT    M11     M12     M13     M14
M13     M131    M132
M14     M141    M142    M143
(base) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/data$
```


Training a hierarchical classifier with HMCN ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python train.py conf/train.hmcn.json
Use dataset to generate dict.
Size of doc_label dict is 102
Size of doc_token dict is 114596
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 102
Size of doc_token dict is 95439
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Traceback (most recent call last):
  File "train.py", line 261, in <module>
    train(config)
  File "train.py", line 228, in train
    trainer.train(train_data_loader, model, optimizer, "Train", epoch)
  File "train.py", line 101, in train
    return self.run(data_loader, model, optimizer, stage, epoch,
  File "train.py", line 125, in run
    loss = self.loss_fn(
  File "/home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1511, in _wrapped_call_impl
    return self._call_impl(*args, **kwargs)
  File "/home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1520, in _call_impl
    return forward_call(*args, **kwargs)
  File "/home/yekyaw.thu/exp/NeuralNLP-NeuralClassifier/model/loss.py", line 123, in forward
    device = logits.device
AttributeError: 'tuple' object has no attribute 'device'

real    0m11.717s
user    0m12.240s
sys     0m2.289s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

README ဖိုင်ကို ပြန်ဖတ်ကြည့်တော့ "set task_info.hierarchical = false." လို့ရေးထားပေမဲ့ တကယ်တမ်း config ဖိုင်ထဲကို ဝင်ကြည့်တဲ့အခါမှာ true ပေးထားတာကို တွေ့ရတယ်။  
အဲဒါနဲ့ false ပြောင်းပေးပြီး နောက်တစ်ခေါက် ထပ် training လုပ်ကြည့်ခဲ့တော့ အောက်ပါအတိုင်း အဆင်ပြေသွားတာကို တွေ့ရတယ်။  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python train.py conf/train.hmcn.json
Use dataset to generate dict.
Size of doc_label dict is 102
Size of doc_token dict is 114596
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 102
Size of doc_token dict is 95439
Size of doc_char dict is 59
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.821330, recall: 0.151396, fscore: 0.255665, macro-fscore: 0.057376, right: 4767, predict: 5804, standard: 31487.
Loss is: 0.092260.
Validate performance at epoch 1 is precision: 0.827225, recall: 0.135004, fscore: 0.232125, macro-fscore: 0.053511, right: 474, predict: 573, standard: 3511.
Loss is: 0.096471.
test performance at epoch 1 is precision: 0.771213, recall: 0.099691, fscore: 0.176559, macro-fscore: 0.044684, right: 1227, predict: 1591, standard: 12308.
Loss is: 0.102654.
Epoch 1 cost time: 36 second
Train performance at epoch 2 is precision: 0.881130, recall: 0.438816, fscore: 0.585863, macro-fscore: 0.180696, right: 13817, predict: 15681, standard: 31487.
Loss is: 0.060067.
Validate performance at epoch 2 is precision: 0.839103, recall: 0.372828, fscore: 0.516269, macro-fscore: 0.156006, right: 1309, predict: 1560, standard: 3511.
Loss is: 0.070725.
test performance at epoch 2 is precision: 0.826421, recall: 0.305980, fscore: 0.446605, macro-fscore: 0.133984, right: 3766, predict: 4557, standard: 12308.
Loss is: 0.077452.
Epoch 2 cost time: 35 second
Train performance at epoch 3 is precision: 0.878781, recall: 0.584114, fscore: 0.701770, macro-fscore: 0.292905, right: 18392, predict: 20929, standard: 31487.
Loss is: 0.049051.
Validate performance at epoch 3 is precision: 0.813942, recall: 0.482199, fscore: 0.605616, macro-fscore: 0.250433, right: 1693, predict: 2080, standard: 3511.
Loss is: 0.062343.
test performance at epoch 3 is precision: 0.800192, recall: 0.405427, fscore: 0.538179, macro-fscore: 0.212599, right: 4990, predict: 6236, standard: 12308.
Loss is: 0.070539.
Epoch 3 cost time: 35 second
Train performance at epoch 4 is precision: 0.895343, recall: 0.634960, fscore: 0.742999, macro-fscore: 0.344988, right: 19993, predict: 22330, standard: 31487.
Loss is: 0.086063.
Validate performance at epoch 4 is precision: 0.802188, recall: 0.501282, fscore: 0.617003, macro-fscore: 0.281318, right: 1760, predict: 2194, standard: 3511.
Loss is: 0.076318.
test performance at epoch 4 is precision: 0.770018, recall: 0.421921, fscore: 0.545140, macro-fscore: 0.232946, right: 5193, predict: 6744, standard: 12308.
Loss is: 0.090298.
Epoch 4 cost time: 35 second
Train performance at epoch 5 is precision: 0.794841, recall: 0.704545, fscore: 0.746974, macro-fscore: 0.399661, right: 22184, predict: 27910, standard: 31487.
Loss is: 3.261326.
Validate performance at epoch 5 is precision: 0.685766, recall: 0.535175, fscore: 0.601184, macro-fscore: 0.298413, right: 1879, predict: 2740, standard: 3511.
Loss is: 2.210183.
test performance at epoch 5 is precision: 0.702795, recall: 0.449383, fscore: 0.548221, macro-fscore: 0.254891, right: 5531, predict: 7870, standard: 12308.
Loss is: 1.366985.
Epoch 5 cost time: 35 second
Train performance at epoch 6 is precision: 0.926849, recall: 0.765363, fscore: 0.838401, macro-fscore: 0.461940, right: 24099, predict: 26001, standard: 31487.
Loss is: 0.032174.
Validate performance at epoch 6 is precision: 0.777241, recall: 0.595272, fscore: 0.674194, macro-fscore: 0.353713, right: 2090, predict: 2689, standard: 3511.
Loss is: 0.060107.
test performance at epoch 6 is precision: 0.726971, recall: 0.497563, fscore: 0.590778, macro-fscore: 0.294119, right: 6124, predict: 8424, standard: 12308.
Loss is: 0.073843.
Epoch 6 cost time: 35 second
Train performance at epoch 7 is precision: 0.950329, recall: 0.775336, fscore: 0.853960, macro-fscore: 0.502533, right: 24413, predict: 25689, standard: 31487.
Loss is: 0.030464.
Validate performance at epoch 7 is precision: 0.804712, recall: 0.573911, fscore: 0.669992, macro-fscore: 0.364478, right: 2015, predict: 2504, standard: 3511.
Loss is: 0.061247.
test performance at epoch 7 is precision: 0.756260, recall: 0.471157, fscore: 0.580597, macro-fscore: 0.294162, right: 5799, predict: 7668, standard: 12308.
Loss is: 0.073497.
Epoch 7 cost time: 40 second
Train performance at epoch 8 is precision: 0.950909, recall: 0.800965, fscore: 0.869520, macro-fscore: 0.540039, right: 25220, predict: 26522, standard: 31487.
Loss is: 0.022014.
Validate performance at epoch 8 is precision: 0.782740, recall: 0.589006, fscore: 0.672192, macro-fscore: 0.362360, right: 2068, predict: 2642, standard: 3511.
Loss is: 0.065363.
test performance at epoch 8 is precision: 0.731549, recall: 0.495288, fscore: 0.590669, macro-fscore: 0.304057, right: 6096, predict: 8333, standard: 12308.
Loss is: 0.078055.
Epoch 8 cost time: 43 second
Train performance at epoch 9 is precision: 0.961842, recall: 0.816559, fscore: 0.883266, macro-fscore: 0.565057, right: 25711, predict: 26731, standard: 31487.
Loss is: 0.049064.
Validate performance at epoch 9 is precision: 0.796366, recall: 0.599259, fscore: 0.683894, macro-fscore: 0.366721, right: 2104, predict: 2642, standard: 3511.
Loss is: 0.066650.
test performance at epoch 9 is precision: 0.754066, recall: 0.489763, fscore: 0.593833, macro-fscore: 0.320382, right: 6028, predict: 7994, standard: 12308.
Loss is: 0.078155.
Epoch 9 cost time: 35 second
Train performance at epoch 10 is precision: 0.953870, recall: 0.853717, fscore: 0.901019, macro-fscore: 0.630915, right: 26881, predict: 28181, standard: 31487.
Loss is: 0.067457.
Validate performance at epoch 10 is precision: 0.768638, recall: 0.625463, fscore: 0.689698, macro-fscore: 0.398519, right: 2196, predict: 2857, standard: 3511.
Loss is: 0.065934.
test performance at epoch 10 is precision: 0.717280, recall: 0.525431, fscore: 0.606547, macro-fscore: 0.336366, right: 6467, predict: 9016, standard: 12308.
Loss is: 0.082226.
Epoch 10 cost time: 35 second
Train performance at epoch 11 is precision: 0.953503, recall: 0.883126, fscore: 0.916966, macro-fscore: 0.670516, right: 27807, predict: 29163, standard: 31487.
Loss is: 0.018420.
Validate performance at epoch 11 is precision: 0.751350, recall: 0.634292, fscore: 0.687876, macro-fscore: 0.412729, right: 2227, predict: 2964, standard: 3511.
Loss is: 0.068301.
test performance at epoch 11 is precision: 0.704645, recall: 0.536155, fscore: 0.608960, macro-fscore: 0.355626, right: 6599, predict: 9365, standard: 12308.
Loss is: 0.081196.
Epoch 11 cost time: 34 second
Train performance at epoch 12 is precision: 0.958157, recall: 0.890876, fscore: 0.923292, macro-fscore: 0.677082, right: 28051, predict: 29276, standard: 31487.
Loss is: 0.044393.
Validate performance at epoch 12 is precision: 0.757647, recall: 0.641982, fscore: 0.695035, macro-fscore: 0.420454, right: 2254, predict: 2975, standard: 3511.
Loss is: 0.069901.
test performance at epoch 12 is precision: 0.707776, recall: 0.541355, fscore: 0.613479, macro-fscore: 0.357823, right: 6663, predict: 9414, standard: 12308.
Loss is: 0.084913.
Epoch 12 cost time: 35 second
Train performance at epoch 13 is precision: 0.960798, recall: 0.908375, fscore: 0.933851, macro-fscore: 0.725275, right: 28602, predict: 29769, standard: 31487.
Loss is: 0.031954.
Validate performance at epoch 13 is precision: 0.752543, recall: 0.653090, fscore: 0.699299, macro-fscore: 0.441264, right: 2293, predict: 3047, standard: 3511.
Loss is: 0.070550.
test performance at epoch 13 is precision: 0.697251, recall: 0.550130, fscore: 0.615014, macro-fscore: 0.379154, right: 6771, predict: 9711, standard: 12308.
Loss is: 0.086432.
Epoch 13 cost time: 35 second

Train performance at epoch 14 is precision: 0.973342, recall: 0.899863, fscore: 0.935162, macro-fscore: 0.727543, right: 28334, predict: 29110, standard: 31487.
Loss is: 0.019827.
Validate performance at epoch 14 is precision: 0.791162, recall: 0.632298, fscore: 0.702865, macro-fscore: 0.438305, right: 2220, predict: 2806, standard: 3511.
Loss is: 0.071804.
test performance at epoch 14 is precision: 0.737023, recall: 0.522587, fscore: 0.611552, macro-fscore: 0.366274, right: 6432, predict: 8727, standard: 12308.
Loss is: 0.087079.
Epoch 14 cost time: 35 second
Train performance at epoch 15 is precision: 0.972092, recall: 0.915965, fscore: 0.943194, macro-fscore: 0.743288, right: 28841, predict: 29669, standard: 31487.
Loss is: 0.553413.
Validate performance at epoch 15 is precision: 0.764985, recall: 0.643406, fscore: 0.698948, macro-fscore: 0.438306, right: 2259, predict: 2953, standard: 3511.
Loss is: 0.195707.
test performance at epoch 15 is precision: 0.728296, recall: 0.536399, fscore: 0.617789, macro-fscore: 0.377421, right: 6602, predict: 9065, standard: 12308.
Loss is: 0.931134.
Epoch 15 cost time: 35 second
Train performance at epoch 16 is precision: 0.972440, recall: 0.916664, fscore: 0.943729, macro-fscore: 0.751764, right: 28863, predict: 29681, standard: 31487.
Loss is: 4.145817.
Validate performance at epoch 16 is precision: 0.760516, recall: 0.638565, fscore: 0.694225, macro-fscore: 0.441369, right: 2242, predict: 2948, standard: 3511.
Loss is: 0.075886.
test performance at epoch 16 is precision: 0.722969, recall: 0.528599, fscore: 0.610691, macro-fscore: 0.371196, right: 6506, predict: 8999, standard: 12308.
Loss is: 0.105153.
Epoch 16 cost time: 35 second
Train performance at epoch 17 is precision: 0.965835, recall: 0.936418, fscore: 0.950899, macro-fscore: 0.780778, right: 29485, predict: 30528, standard: 31487.
Loss is: 14.451197.
Validate performance at epoch 17 is precision: 0.752443, recall: 0.657932, fscore: 0.702021, macro-fscore: 0.490114, right: 2310, predict: 3070, standard: 3511.
Loss is: 0.124873.
test performance at epoch 17 is precision: 0.710650, recall: 0.551349, fscore: 0.620945, macro-fscore: 0.382545, right: 6786, predict: 9549, standard: 12308.
Loss is: 0.091104.
Epoch 17 cost time: 35 second
Train performance at epoch 18 is precision: 0.964879, recall: 0.938832, fscore: 0.951677, macro-fscore: 0.794230, right: 29561, predict: 30637, standard: 31487.
Loss is: 8.274200.
Validate performance at epoch 18 is precision: 0.769361, recall: 0.647964, fscore: 0.703463, macro-fscore: 0.463808, right: 2275, predict: 2957, standard: 3511.
Loss is: 0.078981.
test performance at epoch 18 is precision: 0.721692, recall: 0.540624, fscore: 0.618172, macro-fscore: 0.384929, right: 6654, predict: 9220, standard: 12308.
Loss is: 2.478878.
Epoch 18 cost time: 34 second
Train performance at epoch 19 is precision: 0.933803, recall: 0.942167, fscore: 0.937966, macro-fscore: 0.753133, right: 29666, predict: 31769, standard: 31487.
Loss is: 62.460275.
Validate performance at epoch 19 is precision: 0.758070, recall: 0.648818, fscore: 0.699202, macro-fscore: 0.481672, right: 2278, predict: 3005, standard: 3511.
Loss is: 0.081162.
test performance at epoch 19 is precision: 0.681448, recall: 0.536887, fscore: 0.600591, macro-fscore: 0.361617, right: 6608, predict: 9697, standard: 12308.
Loss is: 29.499831.
Epoch 19 cost time: 35 second
Train performance at epoch 20 is precision: 0.952315, recall: 0.941246, fscore: 0.946748, macro-fscore: 0.764335, right: 29637, predict: 31121, standard: 31487.
Loss is: 94.042662.
Validate performance at epoch 20 is precision: 0.762821, recall: 0.643976, fscore: 0.698378, macro-fscore: 0.471538, right: 2261, predict: 2964, standard: 3511.
Loss is: 0.098977.
test performance at epoch 20 is precision: 0.714740, recall: 0.529899, fscore: 0.608594, macro-fscore: 0.375726, right: 6522, predict: 9125, standard: 12308.
Loss is: 1.651449.
Epoch 20 cost time: 35 second
Train performance at epoch 21 is precision: 0.954537, recall: 0.946867, fscore: 0.950686, macro-fscore: 0.764340, right: 29814, predict: 31234, standard: 31487.
Loss is: 47.732798.
Validate performance at epoch 21 is precision: 0.765522, recall: 0.660211, fscore: 0.708977, macro-fscore: 0.468197, right: 2318, predict: 3028, standard: 3511.
Loss is: 0.079644.
test performance at epoch 21 is precision: 0.706462, recall: 0.547124, fscore: 0.616667, macro-fscore: 0.372145, right: 6734, predict: 9532, standard: 12308.
Loss is: 3.887909.
Epoch 21 cost time: 35 second
Train performance at epoch 22 is precision: 0.965200, recall: 0.955728, fscore: 0.960440, macro-fscore: 0.827885, right: 30093, predict: 31178, standard: 31487.
Loss is: 61.357128.
Validate performance at epoch 22 is precision: 0.755855, recall: 0.671034, fscore: 0.710923, macro-fscore: 0.494169, right: 2356, predict: 3117, standard: 3511.
Loss is: 10.063146.
test performance at epoch 22 is precision: 0.693255, recall: 0.553624, fscore: 0.615621, macro-fscore: 0.387135, right: 6814, predict: 9829, standard: 12308.
Loss is: 4.393452.
Epoch 22 cost time: 35 second
Train performance at epoch 23 is precision: 0.949210, recall: 0.942548, fscore: 0.945867, macro-fscore: 0.786669, right: 29678, predict: 31266, standard: 31487.
Loss is: 117.491951.
Validate performance at epoch 23 is precision: 0.733743, recall: 0.645970, fscore: 0.687065, macro-fscore: 0.440250, right: 2268, predict: 3091, standard: 3511.
Loss is: 83.764483.
test performance at epoch 23 is precision: 0.689004, recall: 0.527949, fscore: 0.597820, macro-fscore: 0.368981, right: 6498, predict: 9431, standard: 12308.
Loss is: 46.220677.
Epoch 23 cost time: 35 second
Train performance at epoch 24 is precision: 0.956516, recall: 0.964779, fscore: 0.960630, macro-fscore: 0.831694, right: 30378, predict: 31759, standard: 31487.
Loss is: 48.656476.
Validate performance at epoch 24 is precision: 0.717679, recall: 0.679863, fscore: 0.698259, macro-fscore: 0.473967, right: 2387, predict: 3326, standard: 3511.
Loss is: 15.499335.
test performance at epoch 24 is precision: 0.693005, recall: 0.558661, fscore: 0.618623, macro-fscore: 0.400977, right: 6876, predict: 9922, standard: 12308.
Loss is: 32.365777.
Epoch 24 cost time: 35 second
Train performance at epoch 25 is precision: 0.966119, recall: 0.961762, fscore: 0.963936, macro-fscore: 0.837333, right: 30283, predict: 31345, standard: 31487.
Loss is: 3.580402.
Validate performance at epoch 25 is precision: 0.744667, recall: 0.656223, fscore: 0.697653, macro-fscore: 0.479383, right: 2304, predict: 3094, standard: 3511.
Loss is: 0.599207.
test performance at epoch 25 is precision: 0.680895, recall: 0.539162, fscore: 0.601796, macro-fscore: 0.371081, right: 6636, predict: 9746, standard: 12308.
Loss is: 10.553482.
Epoch 25 cost time: 35 second
Train performance at epoch 26 is precision: 0.980311, recall: 0.956681, fscore: 0.968352, macro-fscore: 0.875236, right: 30123, predict: 30728, standard: 31487.
Loss is: 16.213156.
Validate performance at epoch 26 is precision: 0.780272, recall: 0.653375, fscore: 0.711208, macro-fscore: 0.507012, right: 2294, predict: 2940, standard: 3511.
Loss is: 28.503511.
test performance at epoch 26 is precision: 0.724961, recall: 0.528112, fscore: 0.611075, macro-fscore: 0.399563, right: 6500, predict: 8966, standard: 12308.
Loss is: 14.470669.
Epoch 26 cost time: 36 second
Train performance at epoch 27 is precision: 0.955467, recall: 0.963509, fscore: 0.959471, macro-fscore: 0.818084, right: 30338, predict: 31752, standard: 31487.
Loss is: 174.855343.
Validate performance at epoch 27 is precision: 0.757635, recall: 0.664198, fscore: 0.707846, macro-fscore: 0.501268, right: 2332, predict: 3078, standard: 3511.
Loss is: 0.137033.
test performance at epoch 27 is precision: 0.690110, recall: 0.543711, fscore: 0.608225, macro-fscore: 0.380024, right: 6692, predict: 9697, standard: 12308.
Loss is: 191.365079.
Epoch 27 cost time: 35 second
Train performance at epoch 28 is precision: 0.965531, recall: 0.968813, fscore: 0.967169, macro-fscore: 0.853780, right: 30505, predict: 31594, standard: 31487.
Loss is: 129.303949.
Validate performance at epoch 28 is precision: 0.716290, recall: 0.668755, fscore: 0.691707, macro-fscore: 0.477180, right: 2348, predict: 3278, standard: 3511.
Loss is: 119.800715.
test performance at epoch 28 is precision: 0.677017, recall: 0.556224, fscore: 0.610705, macro-fscore: 0.404369, right: 6846, predict: 10112, standard: 12308.
Loss is: 72.115033.
Epoch 28 cost time: 35 second
Train performance at epoch 29 is precision: 0.939755, recall: 0.969511, fscore: 0.954401, macro-fscore: 0.824526, right: 30527, predict: 32484, standard: 31487.
Loss is: 74.321478.
Validate performance at epoch 29 is precision: 0.703737, recall: 0.665053, fscore: 0.683848, macro-fscore: 0.476821, right: 2335, predict: 3318, standard: 3511.
Loss is: 85.244707.
test performance at epoch 29 is precision: 0.636697, recall: 0.549480, fscore: 0.589882, macro-fscore: 0.373424, right: 6763, predict: 10622, standard: 12308.
Loss is: 69.246027.
Epoch 29 cost time: 35 second

Train performance at epoch 30 is precision: 0.965941, recall: 0.969162, fscore: 0.967549, macro-fscore: 0.845698, right: 30516, predict: 31592, standard: 31487.
Loss is: 17.431451.
Validate performance at epoch 30 is precision: 0.757313, recall: 0.671034, fscore: 0.711568, macro-fscore: 0.497789, right: 2356, predict: 3111, standard: 3511.
Loss is: 0.088848.
test performance at epoch 30 is precision: 0.695131, recall: 0.550942, fscore: 0.614694, macro-fscore: 0.391152, right: 6781, predict: 9755, standard: 12308.
Loss is: 36.011000.
Epoch 30 cost time: 36 second
Train performance at epoch 31 is precision: 0.977933, recall: 0.969734, fscore: 0.973816, macro-fscore: 0.897316, right: 30534, predict: 31223, standard: 31487.
Loss is: 4.606950.
Validate performance at epoch 31 is precision: 0.746730, recall: 0.666762, fscore: 0.704484, macro-fscore: 0.509893, right: 2341, predict: 3135, standard: 3511.
Loss is: 0.218327.
test performance at epoch 31 is precision: 0.691303, recall: 0.550211, fscore: 0.612740, macro-fscore: 0.388575, right: 6772, predict: 9796, standard: 12308.
Loss is: 39.056346.
Epoch 31 cost time: 35 second
Train performance at epoch 32 is precision: 0.977392, recall: 0.969352, fscore: 0.973356, macro-fscore: 0.896174, right: 30522, predict: 31228, standard: 31487.
Loss is: 18.006342.
Validate performance at epoch 32 is precision: 0.736288, recall: 0.657647, fscore: 0.694750, macro-fscore: 0.492353, right: 2309, predict: 3136, standard: 3511.
Loss is: 5.950256.
test performance at epoch 32 is precision: 0.682533, recall: 0.549886, fscore: 0.609071, macro-fscore: 0.388637, right: 6768, predict: 9916, standard: 12308.
Loss is: 15.475835.
Epoch 32 cost time: 35 second
Train performance at epoch 33 is precision: 0.937390, recall: 0.846857, fscore: 0.889827, macro-fscore: 0.706693, right: 26665, predict: 28446, standard: 31487.
Loss is: 0.557476.
Validate performance at epoch 33 is precision: 0.737143, recall: 0.587867, fscore: 0.654096, macro-fscore: 0.429837, right: 2064, predict: 2800, standard: 3511.
Loss is: 0.197061.
test performance at epoch 33 is precision: 0.662934, recall: 0.461813, fscore: 0.544392, macro-fscore: 0.304168, right: 5684, predict: 8574, standard: 12308.
Loss is: 1.753058.
Epoch 33 cost time: 35 second
Train performance at epoch 34 is precision: 0.923941, recall: 0.862261, fscore: 0.892036, macro-fscore: 0.679418, right: 27150, predict: 29385, standard: 31487.
Loss is: 10.373974.
Validate performance at epoch 34 is precision: 0.745611, recall: 0.592709, fscore: 0.660425, macro-fscore: 0.447693, right: 2081, predict: 2791, standard: 3511.
Loss is: 0.072360.
test performance at epoch 34 is precision: 0.656631, recall: 0.481963, fscore: 0.555899, macro-fscore: 0.319896, right: 5932, predict: 9034, standard: 12308.
Loss is: 48.894802.
Epoch 34 cost time: 34 second
Train performance at epoch 35 is precision: 0.951537, recall: 0.845555, fscore: 0.895421, macro-fscore: 0.727529, right: 26624, predict: 27980, standard: 31487.
Loss is: 1.605362.
Validate performance at epoch 35 is precision: 0.773138, recall: 0.585303, fscore: 0.666234, macro-fscore: 0.453429, right: 2055, predict: 2658, standard: 3511.
Loss is: 0.117155.
test performance at epoch 35 is precision: 0.707830, recall: 0.461976, fscore: 0.559068, macro-fscore: 0.329858, right: 5686, predict: 8033, standard: 12308.
Loss is: 0.483170.
Epoch 35 cost time: 35 second
Train performance at epoch 36 is precision: 0.885954, recall: 0.891638, fscore: 0.888787, macro-fscore: 0.680772, right: 28075, predict: 31689, standard: 31487.
Loss is: 2056.721655.
Validate performance at epoch 36 is precision: 0.703368, recall: 0.618627, fscore: 0.658282, macro-fscore: 0.428482, right: 2172, predict: 3088, standard: 3511.
Loss is: 10.409944.
test performance at epoch 36 is precision: 0.637393, recall: 0.498294, fscore: 0.559325, macro-fscore: 0.320092, right: 6133, predict: 9622, standard: 12308.
Loss is: 1122.017526.
Epoch 36 cost time: 36 second
Train performance at epoch 37 is precision: 0.938322, recall: 0.883222, fscore: 0.909939, macro-fscore: 0.719636, right: 27810, predict: 29638, standard: 31487.
Loss is: 287.615263.
Validate performance at epoch 37 is precision: 0.749822, recall: 0.599259, fscore: 0.666139, macro-fscore: 0.454597, right: 2104, predict: 2806, standard: 3511.
Loss is: 234.099957.
test performance at epoch 37 is precision: 0.676362, recall: 0.476113, fscore: 0.558840, macro-fscore: 0.321324, right: 5860, predict: 8664, standard: 12308.
Loss is: 20.061219.
Epoch 37 cost time: 35 second
Train performance at epoch 38 is precision: 0.918290, recall: 0.896942, fscore: 0.907490, macro-fscore: 0.728697, right: 28242, predict: 30755, standard: 31487.
Loss is: 70.415134.
Validate performance at epoch 38 is precision: 0.719933, recall: 0.612076, fscore: 0.661638, macro-fscore: 0.422981, right: 2149, predict: 2985, standard: 3511.
Loss is: 21.600493.
test performance at epoch 38 is precision: 0.631347, recall: 0.488950, fscore: 0.551099, macro-fscore: 0.316699, right: 6018, predict: 9532, standard: 12308.
Loss is: 38.118845.
Epoch 38 cost time: 34 second
Train performance at epoch 39 is precision: 0.930319, recall: 0.927335, fscore: 0.928825, macro-fscore: 0.789781, right: 29199, predict: 31386, standard: 31487.
Loss is: 14.319849.
Validate performance at epoch 39 is precision: 0.713965, recall: 0.634862, fscore: 0.672094, macro-fscore: 0.464994, right: 2229, predict: 3122, standard: 3511.
Loss is: 0.079239.
test performance at epoch 39 is precision: 0.626121, recall: 0.521937, fscore: 0.569302, macro-fscore: 0.346088, right: 6424, predict: 10260, standard: 12308.
Loss is: 59.164866.
Epoch 39 cost time: 35 second
Train performance at epoch 40 is precision: 0.948615, recall: 0.887668, fscore: 0.917130, macro-fscore: 0.730882, right: 27950, predict: 29464, standard: 31487.
Loss is: 59.436465.
Validate performance at epoch 40 is precision: 0.776475, recall: 0.603532, fscore: 0.679167, macro-fscore: 0.443185, right: 2119, predict: 2729, standard: 3511.
Loss is: 0.080023.
test performance at epoch 40 is precision: 0.688536, recall: 0.482613, fscore: 0.567471, macro-fscore: 0.325609, right: 5940, predict: 8627, standard: 12308.
Loss is: 24.307915.
Epoch 40 cost time: 36 second
Train performance at epoch 41 is precision: 0.941332, recall: 0.918252, fscore: 0.929649, macro-fscore: 0.783498, right: 28913, predict: 30715, standard: 31487.
Loss is: 160.666079.
Validate performance at epoch 41 is precision: 0.727213, recall: 0.631729, fscore: 0.676116, macro-fscore: 0.468053, right: 2218, predict: 3050, standard: 3511.
Loss is: 0.079317.
test performance at epoch 41 is precision: 0.659822, recall: 0.506500, fscore: 0.573083, macro-fscore: 0.341540, right: 6234, predict: 9448, standard: 12308.
Loss is: 114.819372.
Epoch 41 cost time: 35 second
Train performance at epoch 42 is precision: 0.954858, recall: 0.907581, fscore: 0.930620, macro-fscore: 0.798359, right: 28577, predict: 29928, standard: 31487.
Loss is: 37.515918.
Validate performance at epoch 42 is precision: 0.743651, recall: 0.617203, fscore: 0.674553, macro-fscore: 0.462915, right: 2167, predict: 2914, standard: 3511.
Loss is: 40.042991.
test performance at epoch 42 is precision: 0.670011, recall: 0.499188, fscore: 0.572120, macro-fscore: 0.344190, right: 6144, predict: 9170, standard: 12308.
Loss is: 5.636997.
Epoch 42 cost time: 35 second
Train performance at epoch 43 is precision: 0.954828, recall: 0.903579, fscore: 0.928497, macro-fscore: 0.779807, right: 28451, predict: 29797, standard: 31487.
Loss is: 12.999065.
Validate performance at epoch 43 is precision: 0.746831, recall: 0.620906, fscore: 0.678072, macro-fscore: 0.468228, right: 2180, predict: 2919, standard: 3511.
Loss is: 4.501468.
test performance at epoch 43 is precision: 0.674156, recall: 0.499756, fscore: 0.574001, macro-fscore: 0.342489, right: 6151, predict: 9124, standard: 12308.
Loss is: 2.180796.
Epoch 43 cost time: 34 second
Train performance at epoch 44 is precision: 0.931027, recall: 0.908407, fscore: 0.919578, macro-fscore: 0.762711, right: 28603, predict: 30722, standard: 31487.
Loss is: 23.137681.
Validate performance at epoch 44 is precision: 0.716700, recall: 0.616064, fscore: 0.662582, macro-fscore: 0.433874, right: 2163, predict: 3018, standard: 3511.
Loss is: 17.779019.
test performance at epoch 44 is precision: 0.657158, recall: 0.499756, fscore: 0.567750, macro-fscore: 0.336546, right: 6151, predict: 9360, standard: 12308.
Loss is: 3.899084.
Epoch 44 cost time: 35 second
Train performance at epoch 45 is precision: 0.916481, recall: 0.912377, fscore: 0.914424, macro-fscore: 0.757098, right: 28728, predict: 31346, standard: 31487.
Loss is: 329.821178.
Validate performance at epoch 45 is precision: 0.708481, recall: 0.625748, fscore: 0.664549, macro-fscore: 0.440296, right: 2197, predict: 3101, standard: 3511.
Loss is: 175.611152.
test performance at epoch 45 is precision: 0.637158, recall: 0.503494, fscore: 0.562494, macro-fscore: 0.332496, right: 6197, predict: 9726, standard: 12308.
Loss is: 413.060948.
Epoch 45 cost time: 36 second
Train performance at epoch 46 is precision: 0.914367, recall: 0.903738, fscore: 0.909021, macro-fscore: 0.731747, right: 28456, predict: 31121, standard: 31487.
Loss is: 329.300365.
Validate performance at epoch 46 is precision: 0.713080, recall: 0.625748, fscore: 0.666566, macro-fscore: 0.439410, right: 2197, predict: 3081, standard: 3511.
Loss is: 257.697239.
test performance at epoch 46 is precision: 0.640371, recall: 0.505200, fscore: 0.564811, macro-fscore: 0.327611, right: 6218, predict: 9710, standard: 12308.
Loss is: 307.639788.
Epoch 46 cost time: 35 second
Train performance at epoch 47 is precision: 0.900984, recall: 0.907136, fscore: 0.904050, macro-fscore: 0.723226, right: 28563, predict: 31702, standard: 31487.
Loss is: 1145.403095.
Validate performance at epoch 47 is precision: 0.709355, recall: 0.626317, fscore: 0.665255, macro-fscore: 0.439934, right: 2199, predict: 3100, standard: 3511.
Loss is: 924.451861.
test performance at epoch 47 is precision: 0.624724, recall: 0.505444, fscore: 0.558789, macro-fscore: 0.322275, right: 6221, predict: 9958, standard: 12308.
Loss is: 409.590098.
Epoch 47 cost time: 37 second
Train performance at epoch 48 is precision: 0.939149, recall: 0.907771, fscore: 0.923194, macro-fscore: 0.770003, right: 28583, predict: 30435, standard: 31487.
Loss is: 271.171875.
Validate performance at epoch 48 is precision: 0.715262, recall: 0.626032, fscore: 0.667679, macro-fscore: 0.444334, right: 2198, predict: 3073, standard: 3511.
Loss is: 11.954388.
test performance at epoch 48 is precision: 0.643234, recall: 0.504794, fscore: 0.565667, macro-fscore: 0.337010, right: 6213, predict: 9659, standard: 12308.
Loss is: 122.289065.
Epoch 48 cost time: 34 second
Train performance at epoch 49 is precision: 0.938633, recall: 0.907422, fscore: 0.922764, macro-fscore: 0.769550, right: 28572, predict: 30440, standard: 31487.
Loss is: 316.612891.
Validate performance at epoch 49 is precision: 0.722277, recall: 0.621475, fscore: 0.668096, macro-fscore: 0.454742, right: 2182, predict: 3021, standard: 3511.
Loss is: 30.936896.
test performance at epoch 49 is precision: 0.633788, recall: 0.498050, fscore: 0.557780, macro-fscore: 0.325165, right: 6130, predict: 9672, standard: 12308.
Loss is: 1030.210029.
Epoch 49 cost time: 35 second
Train performance at epoch 50 is precision: 0.894367, recall: 0.909137, fscore: 0.901691, macro-fscore: 0.731530, right: 28626, predict: 32007, standard: 31487.
Loss is: 3004.326722.
Validate performance at epoch 50 is precision: 0.701190, recall: 0.620906, fscore: 0.658610, macro-fscore: 0.429070, right: 2180, predict: 3109, standard: 3511.
Loss is: 190.881530.
test performance at epoch 50 is precision: 0.617555, recall: 0.496181, fscore: 0.550255, macro-fscore: 0.319796, right: 6107, predict: 9889, standard: 12308.
Loss is: 896.100468.
Epoch 50 cost time: 35 second
Best test performance at epoch 30 is precision: 0.695131, recall: 0.550942, fscore: 0.614694, macro-fscore: 0.391152, right: 6781, predict: 9755, standard: 12308.
Loss is: 36.011000.

real    30m6.936s
user    87m33.525s
sys     4m45.900s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/checkpoint_dir_rcv1$ ls
HMCN_1   HMCN_24  HMCN_39  HMCN_8        TextRNN_16  TextRNN_30  TextRNN_45
HMCN_10  HMCN_25  HMCN_4   HMCN_9        TextRNN_17  TextRNN_31  TextRNN_46
HMCN_11  HMCN_26  HMCN_40  HMCN_best     TextRNN_18  TextRNN_32  TextRNN_47
HMCN_12  HMCN_27  HMCN_41  TextCNN_1     TextRNN_19  TextRNN_33  TextRNN_48
HMCN_13  HMCN_28  HMCN_42  TextCNN_2     TextRNN_2   TextRNN_34  TextRNN_49
HMCN_14  HMCN_29  HMCN_43  TextCNN_3     TextRNN_20  TextRNN_35  TextRNN_5
HMCN_15  HMCN_3   HMCN_44  TextCNN_4     TextRNN_21  TextRNN_36  TextRNN_50
HMCN_16  HMCN_30  HMCN_45  TextCNN_5     TextRNN_22  TextRNN_37  TextRNN_6
HMCN_17  HMCN_31  HMCN_46  TextCNN_best  TextRNN_23  TextRNN_38  TextRNN_7
HMCN_18  HMCN_32  HMCN_47  TextRNN_1     TextRNN_24  TextRNN_39  TextRNN_8
HMCN_19  HMCN_33  HMCN_48  TextRNN_10    TextRNN_25  TextRNN_4   TextRNN_9
HMCN_2   HMCN_34  HMCN_49  TextRNN_11    TextRNN_26  TextRNN_40  TextRNN_best
HMCN_20  HMCN_35  HMCN_5   TextRNN_12    TextRNN_27  TextRNN_41
HMCN_21  HMCN_36  HMCN_50  TextRNN_13    TextRNN_28  TextRNN_42
HMCN_22  HMCN_37  HMCN_6   TextRNN_14    TextRNN_29  TextRNN_43
HMCN_23  HMCN_38  HMCN_7   TextRNN_15    TextRNN_3   TextRNN_44
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/checkpoint_dir_rcv1$
```

## Format Conversion

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ python ./convert-to-json.py --input ./ltrain.txt --output ltrain.json
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ python ./convert-to-json.py --input ./ltest.txt --output ltest.json
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ head ltrain.json
{"doc_label": ["ab"], "doc_token": ["လီး", "တောင်", "ရိုးရိုး", "မ", "ဟုတ်", "ဘူး", "တပတ်လည်", "လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဆူ", "စရာ", "ရှိ", "လည်း", "ကွယ်ရာ", "မှာ", "ပြော", "ပါ", "လား", "ကွာ", "စိတ်", "နု", "တဲ့", "သူ", "ဆို", "ရှက်", "ပြီး", "သတ်သေ", "လောက်", "တယ်", "တစ်", "နိုင်ငံ", "လုံး", "မြင်", "အောင်", "ပြ", "နေ", "ကြ", "တာ", "မှား", "ရင်", "လည်း", "မှား", "မယ်", "အမှား", "ဆို", "အမှန်", "ကို", "ထောက်ပြ", "ပေး", "မှ", "ဆရာ", "ဖြစ်", "မှာ", "ခု", "ဟာ", "က", "ဆောက်ရှက်ခွဲ", "နေ", "တာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["သေခါနီး", "ရိက္ခာ", "ယူ", "နေ", "ကြ", "တယ်", "GL"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["အောက်တန်းစား", "စိတ်ဓာတ်", "တွေ", "ဖာဆန်", "တဲ့", "လုပ်ရပ်", "နဲ့", "အတွေး", "တွေ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["စာအုပ်", "အဟောင်း", "သတင်းစာ", "အဟောင်း", "ပဲ", "ကျန်", "တော့", "မှာ", "ဗျာ", "ရောင်းစား", "စရာ", "က", "လည်း"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖာ", "ဖြစ်", "မယ့်", "ကျောင်းသူ", "လေး", "များ", "တွေ့", "ရှိ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဒီ", "khwayဝဲစား", "ကောင်", "ကို", "ထောင်", "ချ", "ပစ်", "ရ", "မှာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ရူး", "ရင်", "လည်း", "ထမင်းလွတ်ရူး", "ကြ", "ပါ", "ကွာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["bo"], "doc_token": ["နင့်", "အသံ", "နဲ့", "သီချင်း", "နဲ့", "နင့်", "ဟန်ပန်", "အမူရာ", "က", "တခြားစီ", "ကားယား", "ပွတ်သပ်", "နေ", "တာ", "မသာမ", "ရဲ့", "မြူဆွယ်", "နေ", "တာ", "လား"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လီး", "ပဲ", "ဟေ့"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$
```

## Conversion for the Short-Data

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ python ./convert-to-json.py --input ./strain.txt --output ./strain.json
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ python ./convert-to-json.py --input ./stest.txt --output ./stest.json
```

Check the converted file:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ head ./strain.json
{"doc_label": ["ab"], "doc_token": ["လီး", "တောင်", "မ", "လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လောက်", "ဆောက်ရှက်ခွဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["သေခါနီး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["အောက်တန်းစား", "ဖာဆန်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["စာအုပ်", "အဟောင်း", "သတင်းစာ", "အဟောင်း", "ပဲ", "ကျန်", "တော့", "မှာ", "ဗျာ", "ရောင်းစား", "စရာ", "က", "လည်း"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["khwayဝဲစား", "ချ", "ပစ်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ရူး", "ထမင်းလွတ်ရူး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["bo"], "doc_token": ["ကားယား", "ပွတ်သပ်", "မသာမ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$
```

Check the test file ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ head ./stest.json
{"doc_label": ["ab"], "doc_token": ["$ရူး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["bo"], "doc_token": ["မ", "ပေါက်", "ရေမြင်းပါးစပ်", "ကျပ်မပြည့်မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["စောက်ကောင်မ", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["mmsp", "ပဲ", "ကိုမေကိုလိုး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဘောပြားမကြီး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဘောမ", "ခွေး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ခံ", "စောက်ရှက်ခွဲ", "ပဲ", "မ", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["မအေလိုး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["စောက်ခွက်", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖင်ခံ"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$
```

## Resplitting Train/Dev

Configuration file ကိုပြင်ရင်းနဲ့ သတိပြုမိတာက dev or valid data က training data ကနေ သူ့ဖာသူဆွဲထုတ်တာ မဟုတ်ပဲနဲ့ လူက ပြင်ပေးထားရတယ် ဆိုတဲ့အချက်။  
အဲဒါကြောင့်  train, dev ကို အောက်ပါအတိုင်း ခွဲထုတ်ခဲ့...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ head -n 8137 ./ltrain.txt > ltrain
(nclassi) yekyaw.thu@gpu:~/e
xp/NeuralNLP-NeuralClassifier/hs-data/long-data$ tail -n 1000 ./ltrain.txt > ldev
```

ဖိုင်နာမည် ပြန်ပြောင်း ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ mv ltrain.txt ./tmp/
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ ls
convert-to-json.py  ldev  ltest.json  ltest.txt  ltrain  tmp
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ mv ltrain ltrain.txt
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ mv ldev ldev.txt
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$
```

Format conversion ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ python convert-to-json.py --input ltrain.txt --output ltrain.json
(nclassi) 
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ python convert-to-json.py --input ./ldev.txt --output ldev.json
```

file size ကို confirm လုပ် ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ wc *.json
   1000   23906  338090 ldev.json
   1000   23896  335148 ltest.json
   8137  194429 2750995 ltrain.json
  10137  242231 3424233 total
```

ဖိုင်ကိုလည်း head command နဲ့ရိုက်ထုတ်ကြည့်ခဲ့ ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ head ltrain.json
{"doc_label": ["ab"], "doc_token": ["လီး", "တောင်", "ရိုးရိုး", "မ", "ဟုတ်", "ဘူး", "တပတ်လည်", "လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဆူ", "စရာ", "ရှိ", "လည်း", "ကွယ်ရာ", "မှာ", "ပြော", "ပါ", "လား", "ကွာ", "စိတ်", "နု", "တဲ့", "သူ", "ဆို", "ရှက်", "ပြီး", "သတ်သေ", "လောက်", "တယ်", "တစ်", "နိုင်ငံ", "လုံး", "မြင်", "အောင်", "ပြ", "နေ", "ကြ", "တာ", "မှား", "ရင်", "လည်း", "မှား", "မယ်", "အမှား", "ဆို", "အမှန်", "ကို", "ထောက်ပြ", "ပေး", "မှ", "ဆရာ", "ဖြစ်", "မှာ", "ခု", "ဟာ", "က", "ဆောက်ရှက်ခွဲ", "နေ", "တာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["သေခါနီး", "ရိက္ခာ", "ယူ", "နေ", "ကြ", "တယ်", "GL"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["အောက်တန်းစား", "စိတ်ဓာတ်", "တွေ", "ဖာဆန်", "တဲ့", "လုပ်ရပ်", "နဲ့", "အတွေး", "တွေ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["စာအုပ်", "အဟောင်း", "သတင်းစာ", "အဟောင်း", "ပဲ", "ကျန်", "တော့", "မှာ", "ဗျာ", "ရောင်းစား", "စရာ", "က", "လည်း"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖာ", "ဖြစ်", "မယ့်", "ကျောင်းသူ", "လေး", "များ", "တွေ့", "ရှိ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဒီ", "khwayဝဲစား", "ကောင်", "ကို", "ထောင်", "ချ", "ပစ်", "ရ", "မှာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ရူး", "ရင်", "လည်း", "ထမင်းလွတ်ရူး", "ကြ", "ပါ", "ကွာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["bo"], "doc_token": ["နင့်", "အသံ", "နဲ့", "သီချင်း", "နဲ့", "နင့်", "ဟန်ပန်", "အမူရာ", "က", "တခြားစီ", "ကားယား", "ပွတ်သပ်", "နေ", "တာ", "မသာမ", "ရဲ့", "မြူဆွယ်", "နေ", "တာ", "လား"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လီး", "ပဲ", "ဟေ့"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$
```

dev ဖိုင်ကိုလည်း confirm လုပ် ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$ head ldev.json
{"doc_label": ["ab"], "doc_token": ["ပုံ", "ထဲ", "က", "khwayဝဲဇား", "မ", "ရဲ့", "အောက်ဆွဲ", "မ", "လား", "မှန်မှန်", "ပြော", "😂", "😂"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["se"], "doc_token": ["အဲ့ဒီ", "စောက်စိ", "ကို", "ပြီး", "အောင်", "စုပ်", "ပေး", "ရင်", "ကြိုက်", "မ", "လား"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["po"], "doc_token": ["သူခိုး", "နဲ့", "စစ်ခွေး", "တွေ့", "ကြ", "ပြီ", "ပေါ့", "😂", "😂"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["စံချိန်", "လျှော့", "မယ်", "မ", "ပြော", "နဲ့", "မင်း", "တို့", "ကိုယ်တိုင်", "လည်း", "ဘာ", "စံချိန်", "မှ", "မ", "ရှိ", "တော့", "တာ", "ဒါ", "ထပ်", "ပို", "ပြော", "ရင်", "$ရှက်", "ကို", "မ", "ရှိ", "တော့", "တာ", "$ပို", "တွေ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဒီနေ့", "၇", "ရက်နေ့", "ညနေ", "၅", "နာရီ", "မှာ", "မီး", "လာ", "တယ်", "၅", "နာရီ", "၂၉", "မှာ", "မီး", "ဖြတ်", "တယ်", "ခု", "၇", "နာရီ", "၅", "မိနစ်", "ရှိ", "ပြီ", "ပြည်သူ", "ကို", "မီး", "ဖြတ်", "ပြီး", "စီးပွား", "ရေး", "လုပ်ငန်း", "ကို", "အောက်လမ်းနည်း", "နဲ့", "မီး", "ပေး", "နေ", "တဲ့", "ကမကလ", "တွေ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["အဲ့လို", "လုပ်", "ရဲ", "လား", "လို့", "ဒိုင်", "တွေ", "ကို", "မေး", "ကြည့်", "ဖူး", "လား", "အိမ်", "အပြန်", "လမ်း", "မှာ", "ဓားနဲ့ထိုး", "လို့", "အူ", "အခွေ", "လိုက်", "ပါ", "ထွက်ကျ", "သွား", "လိမ့်", "မယ်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["Kmkl", "တွေ", "မီး", "မ", "လာ", "သေး", "ဘူး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["ငါ", "တော့", "မင်း", "တို့", "မိဘ", "တွေ", "ပဲ", "သနား", "တယ်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["စခွက်", "တွေ", "က", "ဘာ", "လို့", "ချဥ်", "နေ", "တာ", "လဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["သီချင်း", "လား", "ကောင်း", "လိုက်", "တာ", "မျက်ရည်", "တောင်", "ကျ", "တယ်", "ငါ့မယားသား", "တွေ", "ရယ်"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/long-data$
```

## Split Train/Dev for Short Hatespeech Also

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ head -n 8137 ./strain.txt > strain
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ tail -n 1000 ./strain.txt > sdev
```

file rename လုပ်ခဲ့ ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ mv strain.txt ./tmp/
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ mv strain strain.txt
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ mv sdev sdev.txt
```

format conversion ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ python convert-to-json.py --input ./strain.txt --output ./strain.json
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ python convert-to-json.py --input ./sdev.txt --output ./sdev.json
```

Check json filesize:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ wc *.json
   1000   12689  174873 sdev.json
   1000   12731  174363 stest.json
   8137  104042 1442630 strain.json
  10137  129462 1791866 total
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$
```

train ဖိုင်အတွင်းပိုင်းကိုလည်း confirm လုပ်ခဲ့ ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ head strain.json
{"doc_label": ["ab"], "doc_token": ["လီး", "တောင်", "မ", "လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လောက်", "ဆောက်ရှက်ခွဲ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["သေခါနီး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["အောက်တန်းစား", "ဖာဆန်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["စာအုပ်", "အဟောင်း", "သတင်းစာ", "အဟောင်း", "ပဲ", "ကျန်", "တော့", "မှာ", "ဗျာ", "ရောင်းစား", "စရာ", "က", "လည်း"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖာ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["khwayဝဲစား", "ချ", "ပစ်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ရူး", "ထမင်းလွတ်ရူး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["bo"], "doc_token": ["ကားယား", "ပွတ်သပ်", "မသာမ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လီး", "ပဲ"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$
```

dev json ဖိုင် ရဲ့စာကြောင်းတွေကိုလည်း confirm လုပ်ခဲ့ ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$ head sdev.json
{"doc_label": ["ab"], "doc_token": ["khwayဝဲဇား", "မ", "အောက်ဆွဲ", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["se"], "doc_token": ["စောက်စိ", "စုပ်", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["po"], "doc_token": ["သူခိုး", "စစ်ခွေး"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["မ", "မ", "$ရှက်", "မ", "$ပို"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["ဖြတ်", "ဖြတ်", "ကမကလ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["လုပ်", "ဓားနဲ့ထိုး", "အူ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["Kmkl", "မ"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["no"], "doc_token": ["ငါ", "တော့", "မင်း", "တို့", "မိဘ", "တွေ", "ပဲ", "သနား", "တယ်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["စခွက်"], "doc_keyword": [], "doc_topic": []}
{"doc_label": ["ab"], "doc_token": ["တောင်", "ငါ့မယားသား"], "doc_keyword": [], "doc_topic": []}
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-data/short-data$
```

## Config file Preparation for Long Hatespeech

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf/hs/long$ cat train.json
{
  "task_info":{
    "label_type": "single_label",
    "hierarchical": false,
    "hierar_taxonomy": "data/rcv1.taxonomy",
    "hierar_penalty": 0.000001
  },
  "device": "cuda",
  "model_name": "TextCNN",
  "checkpoint_dir": "hs-checkpoint",
  "model_dir": "hs_model",
  "data": {
    "train_json_files": [
      "hs-data/long-data/ltrain.json"
    ],
    "validate_json_files": [
      "hs-data/long-data/ldev.json"
    ],
    "test_json_files": [
      "hs-data/long-data/ltest.json"
    ],
    "generate_dict_using_json_files": true,
    "generate_dict_using_all_json_files": true,
    "generate_dict_using_pretrained_embedding": false,
    "generate_hierarchy_label": false,
    "dict_dir": "hs-dict",
    "num_worker": 4
  },
  "feature": {
    "feature_names": [
      "token"
    ],
    "min_token_count": 1,
    "min_char_count": 2,
    "token_ngram": 0,
    "min_token_ngram_count": 0,
    "min_keyword_count": 0,
    "min_topic_count": 2,
    "max_token_dict_size": 1000000,
    "max_char_dict_size": 150000,
    "max_token_ngram_dict_size": 10000000,
    "max_keyword_dict_size": 100,
    "max_topic_dict_size": 100,
    "max_token_len": 256,
    "max_char_len": 1024,
    "max_char_len_per_token": 12,
    "token_pretrained_file": "",
    "keyword_pretrained_file": ""
  },
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 5,
    "num_epochs_static_embedding": 0,
    "decay_steps": 1000,
    "decay_rate": 1.0,
    "clip_gradients": 100.0,
    "l2_lambda": 0.0,
    "loss_type": "BCEWithLogitsLoss",
    "sampler": "fixed",
    "num_sampled": 5,
    "visible_device_list": "0,1,2,3",
    "hidden_layer_dropout": 0.5
  },
  "embedding": {
    "type": "embedding",
    "dimension": 64,
    "region_embedding_type": "context_word",
    "region_size": 5,
    "initializer": "uniform",
    "fan_mode": "FAN_IN",
    "uniform_bound": 0.25,
    "random_stddev": 0.01,
    "dropout": 0.0
  },
  "optimizer": {
    "optimizer_type": "Adam",
    "learning_rate": 0.008,
    "adadelta_decay_rate": 0.95,
    "adadelta_epsilon": 1e-08
  },
  "TextCNN": {
    "kernel_sizes": [
      2,
      3,
      4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1
  },
  "TextRNN": {
    "hidden_dimension": 64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "doc_embedding_type": "Attention",
    "attention_dimension": 16,
    "bidirectional": true
  },
  "DRNN": {
    "hidden_dimension": 5,
    "window_size": 3,
    "rnn_type": "GRU",
    "bidirectional": true,
    "cell_hidden_dropout": 0.1
  },
  "eval": {
    "text_file": "hs-data/long-data/ltest.json",
    "threshold": 0.5,
    "dir": "hs-eval",
    "batch_size": 1024,
    "is_flat": true,
    "top_k": 100,
    "model_dir": "hs-checkpoint/TextCNN_best"
  },
  "TextVDCNN": {
    "vdcnn_depth": 9,
    "top_k_max_pooling": 8
  },
  "DPCNN": {
    "kernel_size": 3,
    "pooling_stride": 2,
    "num_kernels": 16,
    "blocks": 2
  },
  "TextRCNN": {
    "kernel_sizes": [
        2,
        3,
        4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1,
    "hidden_dimension":64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "bidirectional": true
  },
  "Transformer": {
    "d_inner": 128,
    "d_k": 32,
    "d_v": 32,
    "n_head": 4,
    "n_layers": 1,
    "dropout": 0.1,
    "use_star": true
  },
  "AttentiveConvNet": {
    "attention_type": "bilinear",
    "margin_size": 3,
    "type": "advanced",
    "hidden_size": 64
  },
  "HMCN": {
    "hierarchical_depth": [0, 384, 384, 384, 384],
    "global2local": [0, 16, 192, 512, 64]
  },
  "log": {
    "logger_file": "log_hs_long",
    "log_level": "debug"
  }
}
```

## Training with HateSpeech Data

1st time training got following error:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python ./train.py conf/hs/long/train.json | tee long-train.log
Use dataset to generate dict.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 341
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 325
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Traceback (most recent call last):
  File "./train.py", line 261, in <module>
    train(config)
  File "./train.py", line 228, in train
    trainer.train(train_data_loader, model, optimizer, "Train", epoch)
  File "./train.py", line 101, in train
    return self.run(data_loader, model, optimizer, stage, epoch,
  File "./train.py", line 147, in run
    loss = self.loss_fn(
  File "/home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1511, in _wrapped_call_impl
    return self._call_impl(*args, **kwargs)
  File "/home/yekyaw.thu/.conda/envs/nclassi/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1520, in _call_impl
    return forward_call(*args, **kwargs)
  File "/home/yekyaw.thu/exp/NeuralNLP-NeuralClassifier/model/loss.py", line 141, in forward
    target = torch.eye(self.label_size)[target].to(device)
RuntimeError: indices should be either on cpu or on the same device as the indexed tensor (cpu)

real    0m5.212s
user    0m4.013s
sys     0m2.118s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

Debug ကို လုပ်ကြည့်ပေမဲ့ solution မရခဲ့ဘူး ...  

Ref Links:  
https://github.com/WongKinYiu/yolov7/issues/1101  


## Training TextCNN on CPU

configuration မှာ "cuda" အစား "cpu" ထားပြီး training လုပ်ကြည့်တော့ အောက်ပါအတိုင်း အဆင်ပြေပြေ run တာကို တွေ့ရတယ် ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python ./train.py  ./conf/hs/long/train.json
Use dataset to generate dict.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 341
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 325
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.705297, recall: 0.705297, fscore: 0.705297, macro-fscore: 0.283834, right: 5739, predict: 8137, standard: 8137.
Loss is: 0.201553.
Validate performance at epoch 1 is precision: 0.650000, recall: 0.650000, fscore: 0.650000, macro-fscore: 0.214142, right: 650, predict: 1000, standard: 1000.
Loss is: 0.218616.
test performance at epoch 1 is precision: 0.642000, recall: 0.642000, fscore: 0.642000, macro-fscore: 0.231603, right: 642, predict: 1000, standard: 1000.
Loss is: 0.220533.
Epoch 1 cost time: 8 second
Train performance at epoch 2 is precision: 0.811847, recall: 0.811847, fscore: 0.811847, macro-fscore: 0.463620, right: 6606, predict: 8137, standard: 8137.
Loss is: 0.157607.
Validate performance at epoch 2 is precision: 0.655000, recall: 0.655000, fscore: 0.655000, macro-fscore: 0.276815, right: 655, predict: 1000, standard: 1000.
Loss is: 0.205816.
test performance at epoch 2 is precision: 0.634000, recall: 0.634000, fscore: 0.634000, macro-fscore: 0.299048, right: 634, predict: 1000, standard: 1000.
Loss is: 0.205774.
Epoch 2 cost time: 7 second
Train performance at epoch 3 is precision: 0.865552, recall: 0.865552, fscore: 0.865552, macro-fscore: 0.637482, right: 7043, predict: 8137, standard: 8137.
Loss is: 0.114918.
Validate performance at epoch 3 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.326838, right: 662, predict: 1000, standard: 1000.
Loss is: 0.196574.
test performance at epoch 3 is precision: 0.652000, recall: 0.652000, fscore: 0.652000, macro-fscore: 0.365453, right: 652, predict: 1000, standard: 1000.
Loss is: 0.202553.
Epoch 3 cost time: 7 second
Train performance at epoch 4 is precision: 0.942116, recall: 0.942116, fscore: 0.942116, macro-fscore: 0.773998, right: 7666, predict: 8137, standard: 8137.
Loss is: 0.088334.
Validate performance at epoch 4 is precision: 0.671000, recall: 0.671000, fscore: 0.671000, macro-fscore: 0.421934, right: 671, predict: 1000, standard: 1000.
Loss is: 0.196886.
test performance at epoch 4 is precision: 0.636000, recall: 0.636000, fscore: 0.636000, macro-fscore: 0.387304, right: 636, predict: 1000, standard: 1000.
Loss is: 0.202062.
Epoch 4 cost time: 7 second
Train performance at epoch 5 is precision: 0.955881, recall: 0.955881, fscore: 0.955881, macro-fscore: 0.810310, right: 7778, predict: 8137, standard: 8137.
Loss is: 0.062592.
Validate performance at epoch 5 is precision: 0.686000, recall: 0.686000, fscore: 0.686000, macro-fscore: 0.387659, right: 686, predict: 1000, standard: 1000.
Loss is: 0.200583.
test performance at epoch 5 is precision: 0.671000, recall: 0.671000, fscore: 0.671000, macro-fscore: 0.386526, right: 671, predict: 1000, standard: 1000.
Loss is: 0.200195.
Epoch 5 cost time: 7 second
Best test performance at epoch 5 is precision: 0.671000, recall: 0.671000, fscore: 0.671000, macro-fscore: 0.386526, right: 671, predict: 1000, standard: 1000.
Loss is: 0.200195.

real    0m41.106s
user    4m26.797s
sys     0m41.401s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

no. of epoch ကို 10  ထားပြီး ရလဒ်အပြောင်းအလဲ ရှိမရှိကို confirm လုပ်ခဲ့ ...  

```
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 10,
```

Training Result ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python ./train.py  ./conf/hs/long/train.json
Use dataset to generate dict.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 341
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 325
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.705297, recall: 0.705297, fscore: 0.705297, macro-fscore: 0.283834, right: 5739, predict: 8137, standard: 8137.
Loss is: 0.201553.
Validate performance at epoch 1 is precision: 0.650000, recall: 0.650000, fscore: 0.650000, macro-fscore: 0.214142, right: 650, predict: 1000, standard: 1000.
Loss is: 0.218616.
test performance at epoch 1 is precision: 0.642000, recall: 0.642000, fscore: 0.642000, macro-fscore: 0.231603, right: 642, predict: 1000, standard: 1000.
Loss is: 0.220533.
Epoch 1 cost time: 7 second
Train performance at epoch 2 is precision: 0.811847, recall: 0.811847, fscore: 0.811847, macro-fscore: 0.463620, right: 6606, predict: 8137, standard: 8137.
Loss is: 0.157607.
Validate performance at epoch 2 is precision: 0.655000, recall: 0.655000, fscore: 0.655000, macro-fscore: 0.276815, right: 655, predict: 1000, standard: 1000.
Loss is: 0.205816.
test performance at epoch 2 is precision: 0.634000, recall: 0.634000, fscore: 0.634000, macro-fscore: 0.299048, right: 634, predict: 1000, standard: 1000.
Loss is: 0.205774.
Epoch 2 cost time: 7 second
Train performance at epoch 3 is precision: 0.865552, recall: 0.865552, fscore: 0.865552, macro-fscore: 0.637482, right: 7043, predict: 8137, standard: 8137.
Loss is: 0.114918.
Validate performance at epoch 3 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.326838, right: 662, predict: 1000, standard: 1000.
Loss is: 0.196574.
test performance at epoch 3 is precision: 0.652000, recall: 0.652000, fscore: 0.652000, macro-fscore: 0.365453, right: 652, predict: 1000, standard: 1000.
Loss is: 0.202553.
Epoch 3 cost time: 7 second
Train performance at epoch 4 is precision: 0.942116, recall: 0.942116, fscore: 0.942116, macro-fscore: 0.773998, right: 7666, predict: 8137, standard: 8137.
Loss is: 0.088334.
Validate performance at epoch 4 is precision: 0.671000, recall: 0.671000, fscore: 0.671000, macro-fscore: 0.421934, right: 671, predict: 1000, standard: 1000.
Loss is: 0.196886.
test performance at epoch 4 is precision: 0.636000, recall: 0.636000, fscore: 0.636000, macro-fscore: 0.387304, right: 636, predict: 1000, standard: 1000.
Loss is: 0.202062.
Epoch 4 cost time: 7 second
Train performance at epoch 5 is precision: 0.955881, recall: 0.955881, fscore: 0.955881, macro-fscore: 0.810310, right: 7778, predict: 8137, standard: 8137.
Loss is: 0.062592.
Validate performance at epoch 5 is precision: 0.686000, recall: 0.686000, fscore: 0.686000, macro-fscore: 0.387659, right: 686, predict: 1000, standard: 1000.
Loss is: 0.200583.
test performance at epoch 5 is precision: 0.671000, recall: 0.671000, fscore: 0.671000, macro-fscore: 0.386526, right: 671, predict: 1000, standard: 1000.
Loss is: 0.200195.
Epoch 5 cost time: 7 second
Train performance at epoch 6 is precision: 0.974684, recall: 0.974684, fscore: 0.974684, macro-fscore: 0.841702, right: 7931, predict: 8137, standard: 8137.
Loss is: 0.045889.
Validate performance at epoch 6 is precision: 0.697000, recall: 0.697000, fscore: 0.697000, macro-fscore: 0.416582, right: 697, predict: 1000, standard: 1000.
Loss is: 0.205167.
test performance at epoch 6 is precision: 0.669000, recall: 0.669000, fscore: 0.669000, macro-fscore: 0.412990, right: 669, predict: 1000, standard: 1000.
Loss is: 0.204668.
Epoch 6 cost time: 7 second
Train performance at epoch 7 is precision: 0.983409, recall: 0.983409, fscore: 0.983409, macro-fscore: 0.869469, right: 8002, predict: 8137, standard: 8137.
Loss is: 0.033668.
Validate performance at epoch 7 is precision: 0.678000, recall: 0.678000, fscore: 0.678000, macro-fscore: 0.410793, right: 678, predict: 1000, standard: 1000.
Loss is: 0.212746.
test performance at epoch 7 is precision: 0.639000, recall: 0.639000, fscore: 0.639000, macro-fscore: 0.381073, right: 639, predict: 1000, standard: 1000.
Loss is: 0.208664.
Epoch 7 cost time: 7 second
Train performance at epoch 8 is precision: 0.987096, recall: 0.987096, fscore: 0.987096, macro-fscore: 0.875280, right: 8032, predict: 8137, standard: 8137.
Loss is: 0.026415.
Validate performance at epoch 8 is precision: 0.687000, recall: 0.687000, fscore: 0.687000, macro-fscore: 0.391148, right: 687, predict: 1000, standard: 1000.
Loss is: 0.220337.
test performance at epoch 8 is precision: 0.670000, recall: 0.670000, fscore: 0.670000, macro-fscore: 0.403983, right: 670, predict: 1000, standard: 1000.
Loss is: 0.218624.
Epoch 8 cost time: 7 second
Train performance at epoch 9 is precision: 0.992258, recall: 0.992258, fscore: 0.992258, macro-fscore: 0.887017, right: 8074, predict: 8137, standard: 8137.
Loss is: 0.019156.
Validate performance at epoch 9 is precision: 0.668000, recall: 0.668000, fscore: 0.668000, macro-fscore: 0.416552, right: 668, predict: 1000, standard: 1000.
Loss is: 0.260651.
test performance at epoch 9 is precision: 0.656000, recall: 0.656000, fscore: 0.656000, macro-fscore: 0.416269, right: 656, predict: 1000, standard: 1000.
Loss is: 0.243699.
Epoch 9 cost time: 7 second
Train performance at epoch 10 is precision: 0.991029, recall: 0.991029, fscore: 0.991029, macro-fscore: 0.885878, right: 8064, predict: 8137, standard: 8137.
Loss is: 0.015725.
Validate performance at epoch 10 is precision: 0.687000, recall: 0.687000, fscore: 0.687000, macro-fscore: 0.384021, right: 687, predict: 1000, standard: 1000.
Loss is: 0.269271.
test performance at epoch 10 is precision: 0.667000, recall: 0.667000, fscore: 0.667000, macro-fscore: 0.416440, right: 667, predict: 1000, standard: 1000.
Loss is: 0.260586.
Epoch 10 cost time: 7 second
Best test performance at epoch 6 is precision: 0.669000, recall: 0.669000, fscore: 0.669000, macro-fscore: 0.412990, right: 669, predict: 1000, standard: 1000.
Loss is: 0.204668.

real    1m17.144s
user    8m40.939s
sys     1m28.222s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

testing result က epoch 10 အဖြစ်ပြောင်းခဲ့ပေမဲ့ အရမ်းကြီး အပြောင်းအလဲ မရှိဘူး။  

``` yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-checkpoint$ ls
TextCNN_1   TextCNN_2  TextCNN_4  TextCNN_6  TextCNN_8  TextCNN_best
TextCNN_10  TextCNN_3  TextCNN_5  TextCNN_7  TextCNN_9
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-checkpoint$
```

## Prediction of TextCNN

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python predict.py
conf/hs/long/train.json hs-data/long-data/ltest.json

real    0m2.484s
user    0m3.232s
sys     0m1.989s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```


```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ wc predict.txt
1000 1000 3000 predict.txt
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ mv predict.txt hs-cnn-predict.txt
```

## HS, Long, FastText

training ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time python ./train.py  ./conf/hs/long/train.json
Use dataset to generate dict.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 341
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Shrink dict over.
Size of doc_label dict is 10
Size of doc_token dict is 12152
Size of doc_char dict is 325
Size of doc_token_ngram dict is 0
Size of doc_keyword dict is 0
Size of doc_topic dict is 0
Train performance at epoch 1 is precision: 0.557945, recall: 0.557945, fscore: 0.557945, macro-fscore: 0.097961, right: 4540, predict: 8137, standard: 8137.
Loss is: 0.210320.
Validate performance at epoch 1 is precision: 0.572000, recall: 0.572000, fscore: 0.572000, macro-fscore: 0.103862, right: 572, predict: 1000, standard: 1000.
Loss is: 0.211159.
test performance at epoch 1 is precision: 0.545000, recall: 0.545000, fscore: 0.545000, macro-fscore: 0.070596, right: 545, predict: 1000, standard: 1000.
Loss is: 0.221670.
Epoch 1 cost time: 2 second
Train performance at epoch 2 is precision: 0.609193, recall: 0.609193, fscore: 0.609193, macro-fscore: 0.160192, right: 4957, predict: 8137, standard: 8137.
Loss is: 0.176007.
Validate performance at epoch 2 is precision: 0.591000, recall: 0.591000, fscore: 0.591000, macro-fscore: 0.127594, right: 591, predict: 1000, standard: 1000.
Loss is: 0.191135.
test performance at epoch 2 is precision: 0.566000, recall: 0.566000, fscore: 0.566000, macro-fscore: 0.155976, right: 566, predict: 1000, standard: 1000.
Loss is: 0.202352.
Epoch 2 cost time: 2 second
Train performance at epoch 3 is precision: 0.723854, recall: 0.723854, fscore: 0.723854, macro-fscore: 0.304849, right: 5890, predict: 8137, standard: 8137.
Loss is: 0.144103.
Validate performance at epoch 3 is precision: 0.657000, recall: 0.657000, fscore: 0.657000, macro-fscore: 0.229006, right: 657, predict: 1000, standard: 1000.
Loss is: 0.179639.
test performance at epoch 3 is precision: 0.630000, recall: 0.630000, fscore: 0.630000, macro-fscore: 0.228823, right: 630, predict: 1000, standard: 1000.
Loss is: 0.187587.
Epoch 3 cost time: 1 second
Train performance at epoch 4 is precision: 0.784810, recall: 0.784810, fscore: 0.784810, macro-fscore: 0.380964, right: 6386, predict: 8137, standard: 8137.
Loss is: 0.117819.
Validate performance at epoch 4 is precision: 0.683000, recall: 0.683000, fscore: 0.683000, macro-fscore: 0.272407, right: 683, predict: 1000, standard: 1000.
Loss is: 0.174751.
test performance at epoch 4 is precision: 0.644000, recall: 0.644000, fscore: 0.644000, macro-fscore: 0.239293, right: 644, predict: 1000, standard: 1000.
Loss is: 0.180502.
Epoch 4 cost time: 2 second
Train performance at epoch 5 is precision: 0.833600, recall: 0.833600, fscore: 0.833600, macro-fscore: 0.504987, right: 6783, predict: 8137, standard: 8137.
Loss is: 0.096259.
Validate performance at epoch 5 is precision: 0.678000, recall: 0.678000, fscore: 0.678000, macro-fscore: 0.275040, right: 678, predict: 1000, standard: 1000.
Loss is: 0.175893.
test performance at epoch 5 is precision: 0.659000, recall: 0.659000, fscore: 0.659000, macro-fscore: 0.279834, right: 659, predict: 1000, standard: 1000.
Loss is: 0.179084.
Epoch 5 cost time: 2 second
Train performance at epoch 6 is precision: 0.874278, recall: 0.874278, fscore: 0.874278, macro-fscore: 0.597410, right: 7114, predict: 8137, standard: 8137.
Loss is: 0.079357.
Validate performance at epoch 6 is precision: 0.685000, recall: 0.685000, fscore: 0.685000, macro-fscore: 0.315550, right: 685, predict: 1000, standard: 1000.
Loss is: 0.178196.
test performance at epoch 6 is precision: 0.659000, recall: 0.659000, fscore: 0.659000, macro-fscore: 0.294506, right: 659, predict: 1000, standard: 1000.
Loss is: 0.179904.
Epoch 6 cost time: 2 second
Train performance at epoch 7 is precision: 0.895662, recall: 0.895662, fscore: 0.895662, macro-fscore: 0.651130, right: 7288, predict: 8137, standard: 8137.
Loss is: 0.064729.
Validate performance at epoch 7 is precision: 0.681000, recall: 0.681000, fscore: 0.681000, macro-fscore: 0.315509, right: 681, predict: 1000, standard: 1000.
Loss is: 0.185430.
test performance at epoch 7 is precision: 0.659000, recall: 0.659000, fscore: 0.659000, macro-fscore: 0.295222, right: 659, predict: 1000, standard: 1000.
Loss is: 0.184442.
Epoch 7 cost time: 1 second
Train performance at epoch 8 is precision: 0.927860, recall: 0.927860, fscore: 0.927860, macro-fscore: 0.726225, right: 7550, predict: 8137, standard: 8137.
Loss is: 0.052207.
Validate performance at epoch 8 is precision: 0.686000, recall: 0.686000, fscore: 0.686000, macro-fscore: 0.356075, right: 686, predict: 1000, standard: 1000.
Loss is: 0.192420.
test performance at epoch 8 is precision: 0.656000, recall: 0.656000, fscore: 0.656000, macro-fscore: 0.299541, right: 656, predict: 1000, standard: 1000.
Loss is: 0.186700.
Epoch 8 cost time: 2 second
Train performance at epoch 9 is precision: 0.949736, recall: 0.949736, fscore: 0.949736, macro-fscore: 0.789755, right: 7728, predict: 8137, standard: 8137.
Loss is: 0.043104.
Validate performance at epoch 9 is precision: 0.684000, recall: 0.684000, fscore: 0.684000, macro-fscore: 0.366198, right: 684, predict: 1000, standard: 1000.
Loss is: 0.201442.
test performance at epoch 9 is precision: 0.653000, recall: 0.653000, fscore: 0.653000, macro-fscore: 0.336928, right: 653, predict: 1000, standard: 1000.
Loss is: 0.194962.
Epoch 9 cost time: 2 second
Train performance at epoch 10 is precision: 0.961288, recall: 0.961288, fscore: 0.961288, macro-fscore: 0.816541, right: 7822, predict: 8137, standard: 8137.
Loss is: 0.036105.
Validate performance at epoch 10 is precision: 0.687000, recall: 0.687000, fscore: 0.687000, macro-fscore: 0.356139, right: 687, predict: 1000, standard: 1000.
Loss is: 0.210710.
test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.337967, right: 662, predict: 1000, standard: 1000.
Loss is: 0.204353.
Epoch 10 cost time: 2 second
Best test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.337967, right: 662, predict: 1000, standard: 1000.
Loss is: 0.204353.

real    0m25.314s
user    2m4.740s
sys     0m21.881s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

Check the checkpoints folder:   

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-checkpoint$ ls
FastText_1   FastText_4  FastText_8     TextCNN_10  TextCNN_5  TextCNN_9
FastText_10  FastText_5  FastText_9     TextCNN_2   TextCNN_6  TextCNN_best
FastText_2   FastText_6  FastText_best  TextCNN_3   TextCNN_7
FastText_3   FastText_7  TextCNN_1      TextCNN_4   TextCNN_8
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-checkpoint$
```

## Prepare a Bash Shell Script

Support လုပ်တဲ့ မော်ဒယ်  

FastText、 TextCNN、 TextRNN、 TextRCNN、 DRNN、 VDCNN、 DPCNN、 AttentiveConvNet、 Transformer  

အကုန်ကို run ကြည့်ချင်တော့ shell script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ cat run-all.sh   

```bash
#!/bin/bash

models=("FastText" "TextCNN" "TextRNN" "TextRCNN" "DRNN" "VDCNN" "DPCNN" "AttentiveConvNet" "Transformer")

for model in "${models[@]}"
do
    echo "Updating model_name to $model in train.json..."
    sed -i '9s/.*/"model_name": "'"$model"'",/' conf/hs/long/train.json
    echo "Updated line 9 in train.json:"
    sed -n '9p' conf/hs/long/train.json
    echo "Training, Testing, $model..."
    time python ./train.py ./conf/hs/long/train.json | tee "$model".log
done
```

Running all models for long-hatespeech:  

```
time ./run-all.sh
...
...
...
Train performance at epoch 9 is precision: 0.954897, recall: 0.954897, fscore: 0.954897, macro-fscore: 0.781062, right: 7770, predict: 8137, standard: 8137.
Loss is: 0.061837.
Validate performance at epoch 9 is precision: 0.663000, recall: 0.663000, fscore: 0.663000, macro-fscore: 0.357309, right: 663, predict: 1000, standard: 1000.
Loss is: 0.192098.
test performance at epoch 9 is precision: 0.656000, recall: 0.656000, fscore: 0.656000, macro-fscore: 0.379704, right: 656, predict: 1000, standard: 1000.
Loss is: 0.189502.
Epoch 9 cost time: 13 second
Train performance at epoch 10 is precision: 0.969645, recall: 0.969645, fscore: 0.969645, macro-fscore: 0.841188, right: 7890, predict: 8137, standard: 8137.
Loss is: 0.045443.
Validate performance at epoch 10 is precision: 0.678000, recall: 0.678000, fscore: 0.678000, macro-fscore: 0.384190, right: 678, predict: 1000, standard: 1000.
Loss is: 0.190187.
test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.397364, right: 662, predict: 1000, standard: 1000.
Loss is: 0.189003.
Epoch 10 cost time: 13 second
Best test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.397364, right: 662, predict: 1000, standard: 1000.
Loss is: 0.189003.

real    2m21.080s
user    19m56.705s
sys     1m46.215s

real    15m36.886s
user    129m16.434s
sys     11m26.990s
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ mv hs-checkpoint/ hs-long-checkpoint
```

Check the hs-long-checkpoint models ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ ls ./hs-long-checkpoint/
AttentiveConvNet_1     DRNN_1         TextCNN_1      TextRNN_1
AttentiveConvNet_10    DRNN_10        TextCNN_10     TextRNN_10
AttentiveConvNet_2     DRNN_2         TextCNN_2      TextRNN_2
AttentiveConvNet_3     DRNN_3         TextCNN_3      TextRNN_3
AttentiveConvNet_4     DRNN_4         TextCNN_4      TextRNN_4
AttentiveConvNet_5     DRNN_5         TextCNN_5      TextRNN_5
AttentiveConvNet_6     DRNN_6         TextCNN_6      TextRNN_6
AttentiveConvNet_7     DRNN_7         TextCNN_7      TextRNN_7
AttentiveConvNet_8     DRNN_8         TextCNN_8      TextRNN_8
AttentiveConvNet_9     DRNN_9         TextCNN_9      TextRNN_9
AttentiveConvNet_best  DRNN_best      TextCNN_best   TextRNN_best
DPCNN_1                FastText_1     TextRCNN_1     Transformer_1
DPCNN_10               FastText_10    TextRCNN_10    Transformer_10
DPCNN_2                FastText_2     TextRCNN_2     Transformer_2
DPCNN_3                FastText_3     TextRCNN_3     Transformer_3
DPCNN_4                FastText_4     TextRCNN_4     Transformer_4
DPCNN_5                FastText_5     TextRCNN_5     Transformer_5
DPCNN_6                FastText_6     TextRCNN_6     Transformer_6
DPCNN_7                FastText_7     TextRCNN_7     Transformer_7
DPCNN_8                FastText_8     TextRCNN_8     Transformer_8
DPCNN_9                FastText_9     TextRCNN_9     Transformer_9
DPCNN_best             FastText_best  TextRCNN_best  Transformer_best
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$
```

VDCNN model ကိုတော့ ဆောက်မပေးနိုင်တဲ့ error ရှိနေတယ်။  

## Prepare a Shell Script for Checking the Results

(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-log$ cat chk.sh

```bash
#!/bin/bash

# Iterate through each log file
for logfile in *.log; do
    # Check if the file exists and is readable
    if [ -r "$logfile" ]; then
        # Extract the line containing "Best test performance" and print it
        echo "Log file: $logfile"
        grep "Best test performance" "$logfile"
        echo "----------------------------------------"
    else
        echo "Error: $logfile does not exist or is not readable."
    fi
done
```

Let's check hs long results ...   

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-long-log$ ./chk.sh
Log file: AttentiveConvNet.log
Best test performance at epoch 5 is precision: 0.667000, recall: 0.667000, fscore: 0.667000, macro-fscore: 0.424863, right: 667, predict: 1000, standard: 1000.
----------------------------------------
Log file: DPCNN.log
Best test performance at epoch 7 is precision: 0.628000, recall: 0.628000, fscore: 0.628000, macro-fscore: 0.352463, right: 628, predict: 1000, standard: 1000.
----------------------------------------
Log file: DRNN.log
Best test performance at epoch 3 is precision: 0.656000, recall: 0.656000, fscore: 0.656000, macro-fscore: 0.248989, right: 656, predict: 1000, standard: 1000.
----------------------------------------
Log file: FastText.log
Best test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.337967, right: 662, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextCNN.log
Best test performance at epoch 6 is precision: 0.669000, recall: 0.669000, fscore: 0.669000, macro-fscore: 0.412990, right: 669, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextRCNN.log
Best test performance at epoch 4 is precision: 0.656000, recall: 0.656000, fscore: 0.656000, macro-fscore: 0.307350, right: 656, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextRNN.log
Best test performance at epoch 5 is precision: 0.664000, recall: 0.664000, fscore: 0.664000, macro-fscore: 0.384330, right: 664, predict: 1000, standard: 1000.
----------------------------------------
Log file: Transformer.log
Best test performance at epoch 10 is precision: 0.662000, recall: 0.662000, fscore: 0.662000, macro-fscore: 0.397364, right: 662, predict: 1000, standard: 1000.
----------------------------------------
Log file: VDCNN.log
----------------------------------------
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-log$
```

## Training/Testing with HS Short

prepare config file ...  

(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/conf/hs/short$ cat train.json

```
{
  "task_info":{
    "label_type": "single_label",
    "hierarchical": false,
    "hierar_taxonomy": "data/rcv1.taxonomy",
    "hierar_penalty": 0.000001
  },
  "device": "cpu",
"model_name": "Transformer",
  "checkpoint_dir": "hs-short-checkpoint",
  "model_dir": "hs_short_model",
  "data": {
    "train_json_files": [
      "hs-data/short-data/strain.json"
    ],
    "validate_json_files": [
      "hs-data/short-data/sdev.json"
    ],
    "test_json_files": [
      "hs-data/short-data/stest.json"
    ],
    "generate_dict_using_json_files": true,
    "generate_dict_using_all_json_files": true,
    "generate_dict_using_pretrained_embedding": false,
    "generate_hierarchy_label": false,
    "dict_dir": "hs-short-dict",
    "num_worker": 4
  },
  "feature": {
    "feature_names": [
      "token"
    ],
    "min_token_count": 1,
    "min_char_count": 2,
    "token_ngram": 0,
    "min_token_ngram_count": 0,
    "min_keyword_count": 0,
    "min_topic_count": 2,
    "max_token_dict_size": 1000000,
    "max_char_dict_size": 150000,
    "max_token_ngram_dict_size": 10000000,
    "max_keyword_dict_size": 100,
    "max_topic_dict_size": 100,
    "max_token_len": 256,
    "max_char_len": 1024,
    "max_char_len_per_token": 12,
    "token_pretrained_file": "",
    "keyword_pretrained_file": ""
  },
  "train": {
    "batch_size": 64,
    "start_epoch": 1,
    "num_epochs": 10,
    "num_epochs_static_embedding": 0,
    "decay_steps": 1000,
    "decay_rate": 1.0,
    "clip_gradients": 100.0,
    "l2_lambda": 0.0,
    "loss_type": "BCEWithLogitsLoss",
    "sampler": "fixed",
    "num_sampled": 5,
    "visible_device_list": "0,1,2,3",
    "hidden_layer_dropout": 0.5
  },
  "embedding": {
    "type": "embedding",
    "dimension": 64,
    "region_embedding_type": "context_word",
    "region_size": 5,
    "initializer": "uniform",
    "fan_mode": "FAN_IN",
    "uniform_bound": 0.25,
    "random_stddev": 0.01,
    "dropout": 0.0
  },
  "optimizer": {
    "optimizer_type": "Adam",
    "learning_rate": 0.008,
    "adadelta_decay_rate": 0.95,
    "adadelta_epsilon": 1e-08
  },
  "TextCNN": {
    "kernel_sizes": [
      2,
      3,
      4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1
  },
  "TextRNN": {
    "hidden_dimension": 64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "doc_embedding_type": "Attention",
    "attention_dimension": 16,
    "bidirectional": true
  },
  "DRNN": {
    "hidden_dimension": 5,
    "window_size": 3,
    "rnn_type": "GRU",
    "bidirectional": true,
    "cell_hidden_dropout": 0.1
  },
  "eval": {
    "text_file": "hs-data/short-data/stest.json",
    "threshold": 0.5,
    "dir": "hs-short-eval",
    "batch_size": 1024,
    "is_flat": true,
    "top_k": 100,
    "model_dir": "hs-short-checkpoint/TextCNN_best"
  },
  "TextVDCNN": {
    "vdcnn_depth": 9,
    "top_k_max_pooling": 8
  },
  "DPCNN": {
    "kernel_size": 3,
    "pooling_stride": 2,
    "num_kernels": 16,
    "blocks": 2
  },
  "TextRCNN": {
    "kernel_sizes": [
        2,
        3,
        4
    ],
    "num_kernels": 100,
    "top_k_max_pooling": 1,
    "hidden_dimension":64,
    "rnn_type": "GRU",
    "num_layers": 1,
    "bidirectional": true
  },
  "Transformer": {
    "d_inner": 128,
    "d_k": 32,
    "d_v": 32,
    "n_head": 4,
    "n_layers": 1,
    "dropout": 0.1,
    "use_star": true
  },
  "AttentiveConvNet": {
    "attention_type": "bilinear",
    "margin_size": 3,
    "type": "advanced",
    "hidden_size": 64
  },
  "HMCN": {
    "hierarchical_depth": [0, 384, 384, 384, 384],
    "global2local": [0, 16, 192, 512, 64]
  },
  "log": {
    "logger_file": "log_hs_short",
    "log_level": "debug"
  }
}
```

Prepare bash shell script ...  

(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ cat ./run-short.sh  

```
#!/bin/bash

models=("FastText" "TextCNN" "TextRNN" "TextRCNN" "DRNN" "VDCNN" "DPCNN" "AttentiveConvNet" "Transformer")

for model in "${models[@]}"
do
    echo "Updating model_name to $model in conf/hs/short/train.json..."
    sed -i '9s/.*/"model_name": "'"$model"'",/' conf/hs/short/train.json
    echo "Updated line 9 in conf/hs/short/train.json:"
    sed -n '9p' conf/hs/short/train.json
    echo "Training, Testing, $model..."
    time python ./train.py ./conf/hs/short/train.json | tee "$model".log
done
```

Running the experiment with filtered data or short hs ...  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier$ time ./run-short.sh
...
...
...
939781, macro-fscore: 0.803035, right: 7647, predict: 8137, standard: 8137.
Loss is: 0.055889.
Validate performance at epoch 10 is precision: 0.736000, recall: 0.736000, fscore: 0.736000, macro-fscore: 0.394918, right: 736, predict: 1000, standard: 1000.
Loss is: 0.152611.
test performance at epoch 10 is precision: 0.742000, recall: 0.742000, fscore: 0.742000, macro-fscore: 0.459180, right: 742, predict: 1000, standard: 1000.
Loss is: 0.151283.
Epoch 10 cost time: 9 second
Best test performance at epoch 3 is precision: 0.756000, recall: 0.756000, fscore: 0.756000, macro-fscore: 0.309192, right: 756, predict: 1000, standard: 1000.
Loss is: 0.160792.

real    1m39.202s
user    13m51.838s
sys     1m19.316s

real    10m52.975s
user    89m22.254s
sys     8m29.077s
```

Check the output models:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-short-checkpoint$ ls
AttentiveConvNet_1     DRNN_1         TextCNN_1      TextRNN_1
AttentiveConvNet_10    DRNN_10        TextCNN_10     TextRNN_10
AttentiveConvNet_2     DRNN_2         TextCNN_2      TextRNN_2
AttentiveConvNet_3     DRNN_3         TextCNN_3      TextRNN_3
AttentiveConvNet_4     DRNN_4         TextCNN_4      TextRNN_4
AttentiveConvNet_5     DRNN_5         TextCNN_5      TextRNN_5
AttentiveConvNet_6     DRNN_6         TextCNN_6      TextRNN_6
AttentiveConvNet_7     DRNN_7         TextCNN_7      TextRNN_7
AttentiveConvNet_8     DRNN_8         TextCNN_8      TextRNN_8
AttentiveConvNet_9     DRNN_9         TextCNN_9      TextRNN_9
AttentiveConvNet_best  DRNN_best      TextCNN_best   TextRNN_best
DPCNN_1                FastText_1     TextRCNN_1     Transformer_1
DPCNN_10               FastText_10    TextRCNN_10    Transformer_10
DPCNN_2                FastText_2     TextRCNN_2     Transformer_2
DPCNN_3                FastText_3     TextRCNN_3     Transformer_3
DPCNN_4                FastText_4     TextRCNN_4     Transformer_4
DPCNN_5                FastText_5     TextRCNN_5     Transformer_5
DPCNN_6                FastText_6     TextRCNN_6     Transformer_6
DPCNN_7                FastText_7     TextRCNN_7     Transformer_7
DPCNN_8                FastText_8     TextRCNN_8     Transformer_8
DPCNN_9                FastText_9     TextRCNN_9     Transformer_9
DPCNN_best             FastText_best  TextRCNN_best  Transformer_best
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-short-checkpoint$
```

I moved the logs to hs-short-log/   

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-short-log$ ls
AttentiveConvNet.log  DRNN.log      TextCNN.log   TextRNN.log      VDCNN.log
DPCNN.log             FastText.log  TextRCNN.log  Transformer.log
```

Check the results:  

```
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-short-log$ ./chk.sh
Log file: AttentiveConvNet.log
Best test performance at epoch 2 is precision: 0.751000, recall: 0.751000, fscore: 0.751000, macro-fscore: 0.314448, right: 751, predict: 1000, standard: 1000.
----------------------------------------
Log file: DPCNN.log
Best test performance at epoch 2 is precision: 0.752000, recall: 0.752000, fscore: 0.752000, macro-fscore: 0.315819, right: 752, predict: 1000, standard: 1000.
----------------------------------------
Log file: DRNN.log
Best test performance at epoch 6 is precision: 0.758000, recall: 0.758000, fscore: 0.758000, macro-fscore: 0.359142, right: 758, predict: 1000, standard: 1000.
----------------------------------------
Log file: FastText.log
Best test performance at epoch 3 is precision: 0.734000, recall: 0.734000, fscore: 0.734000, macro-fscore: 0.299021, right: 734, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextCNN.log
Best test performance at epoch 2 is precision: 0.758000, recall: 0.758000, fscore: 0.758000, macro-fscore: 0.358805, right: 758, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextRCNN.log
Best test performance at epoch 1 is precision: 0.746000, recall: 0.746000, fscore: 0.746000, macro-fscore: 0.274256, right: 746, predict: 1000, standard: 1000.
----------------------------------------
Log file: TextRNN.log
Best test performance at epoch 2 is precision: 0.744000, recall: 0.744000, fscore: 0.744000, macro-fscore: 0.326796, right: 744, predict: 1000, standard: 1000.
----------------------------------------
Log file: Transformer.log
Best test performance at epoch 3 is precision: 0.756000, recall: 0.756000, fscore: 0.756000, macro-fscore: 0.309192, right: 756, predict: 1000, standard: 1000.
----------------------------------------
Log file: VDCNN.log
----------------------------------------
(nclassi) yekyaw.thu@gpu:~/exp/NeuralNLP-NeuralClassifier/hs-short-log$
```

## Latex Table

```
\begin{table}[htbp]
\centering
\caption{Comparison of Performance Metrics for Long and Short Hatespeech}
\label{tab:performance_comparison}
\begin{tabular}{@{}lccc@{}}
\toprule
\textbf{Model}         & \textbf{Metric} & \textbf{Long Hatespeech} & \textbf{Short Hatespeech} \\ \midrule
\multirow{3}{*}{AttentiveConvNet} & F1       & 0.667     & 0.751      \\
                          & Precision & 0.667     & 0.751      \\
                          & Recall    & 0.667     & 0.751      \\ \midrule
\multirow{3}{*}{DPCNN}           & F1       & 0.628     & 0.752      \\
                          & Precision & 0.628     & 0.752      \\
                          & Recall    & 0.628     & 0.752      \\ \midrule
\multirow{3}{*}{DRNN}            & F1       & 0.656     & 0.758      \\
                          & Precision & 0.656     & 0.758      \\
                          & Recall    & 0.656     & 0.758      \\ \midrule
\multirow{3}{*}{FastText}        & F1       & 0.662     & 0.734      \\
                          & Precision & 0.662     & 0.734      \\
                          & Recall    & 0.662     & 0.734      \\ \midrule
\multirow{3}{*}{TextCNN}         & F1       & 0.669     & 0.758      \\
                          & Precision & 0.669     & 0.758      \\
                          & Recall    & 0.669     & 0.758      \\ \midrule
\multirow{3}{*}{TextRCNN}        & F1       & 0.656     & 0.746      \\
                          & Precision & 0.656     & 0.746      \\
                          & Recall    & 0.656     & 0.746      \\ \midrule
\multirow{3}{*}{TextRNN}         & F1       & 0.664     & 0.744      \\
                          & Precision & 0.664     & 0.744      \\
                          & Recall    & 0.664     & 0.744      \\ \midrule
\multirow{3}{*}{Transformer}     & F1       & 0.662     & 0.756      \\
                          & Precision & 0.662     & 0.756      \\
                          & Recall    & 0.662     & 0.756      \\ \bottomrule
\end{tabular}
\end{table}

```

နောက်ထပ် layout တစ်မျိုးပြောင်းကြည့်ခဲ့...  

```
\begin{table}[htbp]
\centering
\caption{Comparison of Performance Metrics for Long and Short Hatespeech}
\label{tab:performance_comparison}
\begin{tabular}{@{}lccc@{}}
\toprule
\multicolumn{4}{c}{F1 Score}                                                                                                    \\ \midrule
\textbf{Model}         & \textbf{Long Hatespeech} & \textbf{Short Hatespeech} & \textbf{Difference} \\ \midrule
AttentiveConvNet & 0.667           & 0.751            & 0.084               \\
DPCNN            & 0.628           & 0.752            & 0.124               \\
DRNN             & 0.656           & 0.758            & 0.102               \\
FastText         & 0.662           & 0.734            & 0.072               \\
TextCNN          & 0.669           & 0.758            & 0.089               \\
TextRCNN         & 0.656           & 0.746            & 0.090               \\
TextRNN          & 0.664           & 0.744            & 0.080               \\
Transformer      & 0.662           & 0.756            & 0.094               \\ \midrule
\multicolumn{4}{c}{Precision}                                                                                                  \\ \midrule
\textbf{Model}         & \textbf{Long Hatespeech} & \textbf{Short Hatespeech} & \textbf{Difference} \\ \midrule
AttentiveConvNet & 0.667           & 0.751            & 0.084               \\
DPCNN            & 0.628           & 0.752            & 0.124               \\
DRNN             & 0.656           & 0.758            & 0.102               \\
FastText         & 0.662           & 0.734            & 0.072               \\
TextCNN          & 0.669           & 0.758            & 0.089               \\
TextRCNN         & 0.656           & 0.746            & 0.090               \\
TextRNN          & 0.664           & 0.744            & 0.080               \\
Transformer      & 0.662           & 0.756            & 0.094               \\ \midrule
\multicolumn{4}{c}{Recall}                                                                                                     \\ \midrule
\textbf{Model}         & \textbf{Long Hatespeech} & \textbf{Short Hatespeech} & \textbf{Difference} \\ \midrule
AttentiveConvNet & 0.667           & 0.751            & 0.084               \\
DPCNN            & 0.628           & 0.752            & 0.124               \\
DRNN             & 0.656           & 0.758            & 0.102               \\
FastText         & 0.662           & 0.734            & 0.072               \\
TextCNN          & 0.669           & 0.758            & 0.089               \\
TextRCNN         & 0.656           & 0.746            & 0.090               \\
TextRNN          & 0.664           & 0.744            & 0.080               \\
Transformer      & 0.662           & 0.756            & 0.094               \\ \bottomrule
\end{tabular}
\end{table}
```


## Markdown Table

```
| Model            | Metric    | Long Hatespeech | Short Hatespeech |
|------------------|-----------|-----------------|------------------|
| AttentiveConvNet | F1        | 0.667           | 0.751            |
|                  | Precision | 0.667           | 0.751            |
|                  | Recall    | 0.667           | 0.751            |
| DPCNN            | F1        | 0.628           | 0.752            |
|                  | Precision | 0.628           | 0.752            |
|                  | Recall    | 0.628           | 0.752            |
| DRNN             | F1        | 0.656           | 0.758            |
|                  | Precision | 0.656           | 0.758            |
|                  | Recall    | 0.656           | 0.758            |
| FastText         | F1        | 0.662           | 0.734            |
|                  | Precision | 0.662           | 0.734            |
|                  | Recall    | 0.662           | 0.734            |
| TextCNN          | F1        | 0.669           | 0.758            |
|                  | Precision | 0.669           | 0.758            |
|                  | Recall    | 0.669           | 0.758            |
| TextRCNN         | F1        | 0.656           | 0.746            |
|                  | Precision | 0.656           | 0.746            |
|                  | Recall    | 0.656           | 0.746            |
| TextRNN          | F1        | 0.664           | 0.744            |
|                  | Precision | 0.664           | 0.744            |
|                  | Recall    | 0.664           | 0.744            |
| Transformer      | F1        | 0.662           | 0.756            |
|                  | Precision | 0.662           | 0.756            |
|                  | Recall    | 0.662           | 0.756            |

```

နောက်ထပ် layout တစ်မျိုးပြောင်းကြည့်ခဲ့ ...  

```
| Model            | Metric    | Long Hatespeech | Short Hatespeech |
|------------------|-----------|-----------------|------------------|
|                  |           | F1 Score        |                  |
|------------------|-----------|-----------------|------------------|
| AttentiveConvNet | F1        | 0.667           | 0.751            |
| DPCNN            | F1        | 0.628           | 0.752            |
| DRNN             | F1        | 0.656           | 0.758            |
| FastText         | F1        | 0.662           | 0.734            |
| TextCNN          | F1        | 0.669           | 0.758            |
| TextRCNN         | F1        | 0.656           | 0.746            |
| TextRNN          | F1        | 0.664           | 0.744            |
| Transformer      | F1        | 0.662           | 0.756            |
|------------------|-----------|-----------------|------------------|
|                  |           | Precision       |                  |
|------------------|-----------|-----------------|------------------|
| AttentiveConvNet | Precision | 0.667           | 0.751            |
| DPCNN            | Precision | 0.628           | 0.752            |
| DRNN             | Precision | 0.656           | 0.758            |
| FastText         | Precision | 0.662           | 0.734            |
| TextCNN          | Precision | 0.669           | 0.758            |
| TextRCNN         | Precision | 0.656           | 0.746            |
| TextRNN          | Precision | 0.664           | 0.744            |
| Transformer      | Precision | 0.662           | 0.756            |
|------------------|-----------|-----------------|------------------|
|                  |           | Recall          |                  |
|------------------|-----------|-----------------|------------------|
| AttentiveConvNet | Recall    | 0.667           | 0.751            |
| DPCNN            | Recall    | 0.628           | 0.752            |
| DRNN             | Recall    | 0.656           | 0.758            |
| FastText         | Recall    | 0.662           | 0.734            |
| TextCNN          | Recall    | 0.669           | 0.758            |
| TextRCNN         | Recall    | 0.656           | 0.746            |
| TextRNN          | Recall    | 0.664           | 0.744            |
| Transformer      | Recall    | 0.662           | 0.756            |

```

## Backup

Run ထားတဲ့ folder တစ်ခုလုံးကို zip လုပ်ပြီးတော့ local စက်ထဲကို download လုပ်ထားခဲ့တယ်။  

```
C:\Users\801680>scp -P 2250 -i C:\Users\801680\.ssh\id_rsa-for-cadt-gpu-server yekyaw.thu@103.16.63.233:/home/yekyaw.thu/exp/NeuralNLP-NeuralClassifier.zip .\Downloads
Enter passphrase for key 'C:/Users/801680/.ssh/id_rsa-for-cadt-gpu-server':
NeuralNLP-NeuralClassifier.zip                          100% 1684MB  17.3MB/s   01:37
```

