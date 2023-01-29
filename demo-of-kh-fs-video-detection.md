# Test Run for Khmer Fingerspelling Video Detection

## Installaing/Checking Python Libraries

You have to install followings:  

```
pip install tensorflow==2.4.1 tensorflow-gpu==2.4.1 opencv-python mediapipe sklearn matplotlib
```

For me I think, I only need cv2 library, I run inside sl-mnist conda env ... and thus install as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~$ pip install opencv-python
Collecting opencv-python
  Downloading opencv_python-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (61.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.8/61.8 MB 372.4 kB/s eta 0:00:00
Requirement already satisfied: numpy>=1.17.3 in ./.local/lib/python3.8/site-packages (from opencv-python) (1.24.1)
Installing collected packages: opencv-python
Successfully installed opencv-python-4.7.0.68
(sl-mnist) yekyaw.thu@gpu:~$ 
```

Test import:  

```
(sl-mnist) yekyaw.thu@gpu:~$ python
Python 3.8.15 (default, Nov 24 2022, 15:19:38) 
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> print(cv2.__version__)
4.7.0
>>> 
```

Check tensorflow libraries:  

```
(sl-mnist) yekyaw.thu@gpu:~$ python
Python 3.8.15 (default, Nov 24 2022, 15:19:38) 
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow
2023-01-29 17:20:14.120425: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-29 17:20:19.866964: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory
2023-01-29 17:20:19.867055: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory
2023-01-29 17:20:19.867068: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
>>> print(tensorflow.__version__)
2.11.0
>>> from tensorflow.keras.models import Sequential
>>> from tensorflow.keras.layers import LSTM, Dense
>>> from tensorflow.keras.callbacks import TensorBoard
>>> from tensorflow.keras.utils import to_categorical
>>> exit()
(sl-mnist) yekyaw.thu@gpu:~$
```

As shown in above, tensorflow libraries looks OK.  

Check other required libraries as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~$ python
Python 3.8.15 (default, Nov 24 2022, 15:19:38) 
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from sklearn.model_selection import train_test_split
>>> from sklearn.metrics import multilabel_confusion_matrix, accuracy_score
>>> 
>>> from scipy import stats
>>> import numpy as np
>>> import os
>>> from matplotlib import pyplot as plt
>>> import time
>>> import mediapipe as mp
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'mediapipe'
>>> 

```

As shown in above, I need to install mediapipe library. This is because in my previous experiment for sl-mnist, I made on-line testing on Window OS notebook.  
I installed mediapipe as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~$ pip install mediapipe
Collecting mediapipe
  Downloading mediapipe-0.9.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (33.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 33.0/33.0 MB 8.4 MB/s eta 0:00:00
Requirement already satisfied: absl-py in ./.local/lib/python3.8/site-packages (from mediapipe) (1.4.0)
Requirement already satisfied: numpy in ./.local/lib/python3.8/site-packages (from mediapipe) (1.24.1)
Requirement already satisfied: protobuf<4,>=3.11 in ./.local/lib/python3.8/site-packages (from mediapipe) (3.19.6)
Collecting opencv-contrib-python
  Downloading opencv_contrib_python-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (67.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 67.9/67.9 MB 8.8 MB/s eta 0:00:00
Requirement already satisfied: attrs>=19.1.0 in ./.conda/envs/sl-mnist/lib/python3.8/site-packages (from mediapipe) (22.2.0)
Requirement already satisfied: flatbuffers>=2.0 in ./.local/lib/python3.8/site-packages (from mediapipe) (23.1.4)
Requirement already satisfied: matplotlib in ./.local/lib/python3.8/site-packages (from mediapipe) (3.6.3)
Requirement already satisfied: kiwisolver>=1.0.1 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (1.4.4)
Requirement already satisfied: fonttools>=4.22.0 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (4.38.0)
Requirement already satisfied: pillow>=6.2.0 in ./.conda/envs/sl-mnist/lib/python3.8/site-packages (from matplotlib->mediapipe) (9.4.0)
Requirement already satisfied: pyparsing>=2.2.1 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (3.0.9)
Requirement already satisfied: contourpy>=1.0.1 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (1.0.7)
Requirement already satisfied: cycler>=0.10 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (0.11.0)
Requirement already satisfied: packaging>=20.0 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (23.0)
Requirement already satisfied: python-dateutil>=2.7 in ./.local/lib/python3.8/site-packages (from matplotlib->mediapipe) (2.8.2)
Requirement already satisfied: six>=1.5 in ./.conda/envs/sl-mnist/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib->mediapipe) (1.16.0)
Installing collected packages: opencv-contrib-python, mediapipe
Successfully installed mediapipe-0.9.0.1 opencv-contrib-python-4.7.0.68
(sl-mnist) yekyaw.thu@gpu:~$ 
```

check the installed mideapipe library:  

```
(sl-mnist) yekyaw.thu@gpu:~$ python
Python 3.8.15 (default, Nov 24 2022, 15:19:38) 
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import mediapipe as mp
>>> print(mp.__version__)
0.9.0.1
>>> 
```

## Check Tensorflow-GPU

Python code for checking tensorflow-gpu is as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$ cat check-tensorflow-gpu.py 
## Ref: https://intellipaat.com/community/33459/how-to-tell-if-tensorflow-is-using-gpu-acceleration-from-inside-python-shell

import tensorflow as tf 

if tf.test.gpu_device_name(): 
    print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
else:
   print("Please install GPU version of TF")
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$
```

When I run above python code:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$ python ./check-tensorflow-gpu.py 
2023-01-29 17:37:23.999379: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-29 17:37:24.626612: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory
2023-01-29 17:37:24.626660: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory
2023-01-29 17:37:24.626676: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2023-01-29 17:37:25.263877: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-29 17:37:27.093880: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:27.094542: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:27.100346: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:27.101023: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:27.102287: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:27.102920: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.066736: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.067412: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.068830: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.069929: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.071198: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:0 with 9637 MB memory:  -> device: 0, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:0a:00.0, compute capability: 7.5
2023-01-29 17:37:28.071615: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.072233: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:1 with 9637 MB memory:  -> device: 1, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:42:00.0, compute capability: 7.5
2023-01-29 17:37:28.072622: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.073250: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:2 with 9634 MB memory:  -> device: 2, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:43:00.0, compute capability: 7.5
2023-01-29 17:37:28.074206: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.074863: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.076169: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.076846: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.078146: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.078806: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.080138: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.080803: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.082069: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:0 with 9637 MB memory:  -> device: 0, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:0a:00.0, compute capability: 7.5
2023-01-29 17:37:28.082121: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.082749: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:1 with 9637 MB memory:  -> device: 1, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:42:00.0, compute capability: 7.5
2023-01-29 17:37:28.082800: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-29 17:37:28.083417: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /device:GPU:2 with 9634 MB memory:  -> device: 2, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:43:00.0, compute capability: 7.5
Default GPU Device: /device:GPU:0
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$ 
```

## Splitting the Original Code into Three Parts

In the original tutorial code, using the camera of the GPU computer. For our case, we have to use the local notebook or computer for data preparation and train the model on the GPU computer. Moreover, testing also should have to make with our local notebook computer. And thus, I assumed that we need to split the original code ...  


## Creating a New Anacoda Environment on Local Notebook

I created the same Python version with the GPU server.  


```
(base) ye@ykt-pro:~/exp$ conda create --name fs-video-recog python=3.8.15
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.14.0
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/fs-video-recog

  added / updated specs:
    - python=3.8.15


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2023.01.10 |       h06a4308_0         120 KB
    certifi-2022.12.7          |   py38h06a4308_0         150 KB
    ncurses-6.4                |       h6a678d5_0         914 KB
    pip-22.3.1                 |   py38h06a4308_0         2.7 MB
    setuptools-65.6.3          |   py38h06a4308_0         1.1 MB
    sqlite-3.40.1              |       h5082296_0         1.2 MB
    xz-5.2.10                  |       h5eee18b_1         429 KB
    ------------------------------------------------------------
                                           Total:         6.6 MB

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
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-22.3.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.15-h7a1cb2a_2
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-65.6.3-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.40.1-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.10-h5eee18b_1
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
ncurses-6.4          | 914 KB    | ########################################################## | 100% 
xz-5.2.10            | 429 KB    | ########################################################## | 100% 
sqlite-3.40.1        | 1.2 MB    | ########################################################## | 100% 
pip-22.3.1           | 2.7 MB    | ########################################################## | 100% 
setuptools-65.6.3    | 1.1 MB    | ########################################################## | 100% 
certifi-2022.12.7    | 150 KB    | ########################################################## | 100% 
ca-certificates-2023 | 120 KB    | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate fs-video-recog
#
# To deactivate an active environment, use
#
#     $ conda deactivate

Retrieving notices: ...working... done
(base) ye@ykt-pro:~/exp$ conda activate fs-video-recog
(fs-video-recog) ye@ykt-pro:~/exp$
```

## Installation of Required Library on Local Notebook

opencv installation ...  

```
(fs-video-recog) ye@ykt-pro:~/exp$ pip install opencv-python
Collecting opencv-python
  Downloading opencv_python-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (61.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.8/61.8 MB 2.4 MB/s eta 0:00:00
Collecting numpy>=1.17.0
  Downloading numpy-1.24.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.3/17.3 MB 2.5 MB/s eta 0:00:00
Installing collected packages: numpy, opencv-python
Successfully installed numpy-1.24.1 opencv-python-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp$ 
```

For this time, I will install mediapipe library ...  

```
(fs-video-recog) ye@ykt-pro:~/exp$ pip install mediapipe
Collecting mediapipe
  Downloading mediapipe-0.9.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (33.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 33.0/33.0 MB 2.4 MB/s eta 0:00:00
Collecting opencv-contrib-python
  Downloading opencv_contrib_python-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (67.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 67.9/67.9 MB 2.4 MB/s eta 0:00:00
Collecting flatbuffers>=2.0
  Downloading flatbuffers-23.1.21-py2.py3-none-any.whl (26 kB)
Collecting absl-py
  Downloading absl_py-1.4.0-py3-none-any.whl (126 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 126.5/126.5 kB 3.0 MB/s eta 0:00:00
Collecting protobuf<4,>=3.11
  Downloading protobuf-3.20.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 4.7 MB/s eta 0:00:00
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from mediapipe) (1.24.1)
Collecting attrs>=19.1.0
  Downloading attrs-22.2.0-py3-none-any.whl (60 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.0/60.0 kB 5.6 MB/s eta 0:00:00
Collecting matplotlib
  Downloading matplotlib-3.6.3-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (9.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.4/9.4 MB 2.8 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Using cached fonttools-4.38.0-py3-none-any.whl (965 kB)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pyparsing>=2.2.1
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.4.4-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.2 MB)
Collecting packaging>=20.0
  Downloading packaging-23.0-py3-none-any.whl (42 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.7/42.7 kB 2.2 MB/s eta 0:00:00
Collecting pillow>=6.2.0
  Downloading Pillow-9.4.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.3/3.3 MB 3.5 MB/s eta 0:00:00
Collecting contourpy>=1.0.1
  Downloading contourpy-1.0.7-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (300 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 300.0/300.0 kB 3.7 MB/s eta 0:00:00
Collecting python-dateutil>=2.7
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting six>=1.5
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: flatbuffers, six, pyparsing, protobuf, pillow, packaging, opencv-contrib-python, kiwisolver, fonttools, cycler, contourpy, attrs, absl-py, python-dateutil, matplotlib, mediapipe
Successfully installed absl-py-1.4.0 attrs-22.2.0 contourpy-1.0.7 cycler-0.11.0 flatbuffers-23.1.21 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.3 mediapipe-0.9.0.1 opencv-contrib-python-4.7.0.68 packaging-23.0 pillow-9.4.0 protobuf-3.20.3 pyparsing-3.0.9 python-dateutil-2.8.2 six-1.16.0
(fs-video-recog) ye@ykt-pro:~/exp$
```

I installed sklearn library according to the original code and got error message as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp$ pip install sklearn
Collecting sklearn
  Downloading sklearn-0.0.post1.tar.gz (3.6 kB)
  Preparing metadata (setup.py) ... error
  error: subprocess-exited-with-error
  
  × python setup.py egg_info did not run successfully.
  │ exit code: 1
  ╰─> [18 lines of output]
      The 'sklearn' PyPI package is deprecated, use 'scikit-learn'
      rather than 'sklearn' for pip commands.
      
      Here is how to fix this error in the main use cases:
      - use 'pip install scikit-learn' rather than 'pip install sklearn'
      - replace 'sklearn' by 'scikit-learn' in your pip requirements files
        (requirements.txt, setup.py, setup.cfg, Pipfile, etc ...)
      - if the 'sklearn' package is used by one of your dependencies,
        it would be great if you take some time to track which package uses
        'sklearn' instead of 'scikit-learn' and report it to their issue tracker
      - as a last resort, set the environment variable
        SKLEARN_ALLOW_DEPRECATED_SKLEARN_PACKAGE_INSTALL=True to avoid this error
      
      More information is available at
      https://github.com/scikit-learn/sklearn-pypi-package
      
      If the previous advice does not cover your use case, feel free to report it at
      https://github.com/scikit-learn/sklearn-pypi-package/issues/new
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
error: metadata-generation-failed

× Encountered error while generating package metadata.
╰─> See above for output.

note: This is an issue with the package mentioned above, not pip.
hint: See above for details.
(fs-video-recog) ye@ykt-pro:~/exp$
```

And thus, I install scikit-learn as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp$ pip install scikit-learn
Collecting scikit-learn
  Downloading scikit_learn-1.2.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.8/9.8 MB 2.6 MB/s eta 0:00:00
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting joblib>=1.1.1
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Collecting scipy>=1.3.2
  Downloading scipy-1.10.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 34.5/34.5 MB 2.4 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.17.3 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from scikit-learn) (1.24.1)
Installing collected packages: threadpoolctl, scipy, joblib, scikit-learn
Successfully installed joblib-1.2.0 scikit-learn-1.2.1 scipy-1.10.0 threadpoolctl-3.1.0
(fs-video-recog) ye@ykt-pro:~/exp$
```

Matplotlib looks no need to install as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp$ pip install matplotlib
Requirement already satisfied: matplotlib in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (3.6.3)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (1.4.4)
Requirement already satisfied: numpy>=1.19 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (1.24.1)
Requirement already satisfied: packaging>=20.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (23.0)
Requirement already satisfied: pillow>=6.2.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (9.4.0)
Requirement already satisfied: cycler>=0.10 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (0.11.0)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (2.8.2)
Requirement already satisfied: pyparsing>=2.2.1 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (3.0.9)
Requirement already satisfied: contourpy>=1.0.1 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (1.0.7)
Requirement already satisfied: fonttools>=4.22.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from matplotlib) (4.38.0)
Requirement already satisfied: six>=1.5 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)
(fs-video-recog) ye@ykt-pro:~/exp$
```

## Prepare ipython Notebook File for Data Collection  

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
