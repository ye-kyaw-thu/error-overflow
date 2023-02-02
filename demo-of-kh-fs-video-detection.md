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

## Jupyter Notebook Installation on Local Notebook

Jupyter notebook installation will take time ...  

```
(fs-video-recog) ye@ykt-pro:~/exp$ conda install jupyter
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.14.0
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/fs-video-recog

  added / updated specs:
    - jupyter


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    anyio-3.5.0                |   py38h06a4308_0         165 KB
    argon2-cffi-21.3.0         |     pyhd3eb1b0_0          15 KB
    argon2-cffi-bindings-21.2.0|   py38h7f8727e_0          33 KB
    asttokens-2.0.5            |     pyhd3eb1b0_0          20 KB
    attrs-22.1.0               |   py38h06a4308_0          85 KB
    babel-2.11.0               |   py38h06a4308_0         6.8 MB
    beautifulsoup4-4.11.1      |   py38h06a4308_0         185 KB
    bleach-4.1.0               |     pyhd3eb1b0_0         123 KB
    brotlipy-0.7.0             |py38h27cfd23_1003         323 KB
    cffi-1.15.1                |   py38h5eee18b_3         241 KB
    charset-normalizer-2.0.4   |     pyhd3eb1b0_0          35 KB
    comm-0.1.2                 |   py38h06a4308_0          13 KB
    cryptography-38.0.4        |   py38h9ce1e76_0         1.4 MB
    debugpy-1.5.1              |   py38h295c915_0         1.7 MB
    decorator-5.1.1            |     pyhd3eb1b0_0          12 KB
    entrypoints-0.4            |   py38h06a4308_0          16 KB
    executing-0.8.3            |     pyhd3eb1b0_0          18 KB
    expat-2.4.9                |       h6a678d5_0         156 KB
    flit-core-3.6.0            |     pyhd3eb1b0_0          42 KB
    fontconfig-2.14.1          |       h52c9d5c_1         281 KB
    freetype-2.12.1            |       h4a9f257_0         626 KB
    giflib-5.2.1               |       h5eee18b_1          75 KB
    glib-2.69.1                |       he621ea3_2         1.9 MB
    gst-plugins-base-1.14.0    |       h8213a91_2         4.9 MB
    gstreamer-1.14.0           |       h28cd5cc_2         3.2 MB
    idna-3.4                   |   py38h06a4308_0          93 KB
    importlib-metadata-4.11.3  |   py38h06a4308_0          40 KB
    importlib_resources-5.2.0  |     pyhd3eb1b0_1          21 KB
    ipykernel-6.19.2           |   py38hb070fc8_0         218 KB
    ipython-8.8.0              |   py38h06a4308_0         1.0 MB
    jedi-0.18.1                |   py38h06a4308_1         982 KB
    jinja2-3.1.2               |   py38h06a4308_0         211 KB
    jpeg-9e                    |       h7f8727e_0         240 KB
    json5-0.9.6                |     pyhd3eb1b0_0          21 KB
    jsonschema-4.16.0          |   py38h06a4308_0         128 KB
    jupyter-1.0.0              |   py38h06a4308_8           7 KB
    jupyter_client-7.4.8       |   py38h06a4308_0         205 KB
    jupyter_console-6.4.4      |   py38h06a4308_0          42 KB
    jupyter_core-5.1.1         |   py38h06a4308_0          89 KB
    jupyter_server-1.23.4      |   py38h06a4308_0         382 KB
    jupyterlab-3.5.2           |   py38h06a4308_0         4.2 MB
    jupyterlab_server-2.16.5   |   py38h06a4308_0          80 KB
    krb5-1.19.4                |       h568e23c_0         1.3 MB
    lerc-3.0                   |       h295c915_0         196 KB
    libclang-10.0.1            |default_hb85057a_2        10.8 MB
    libdeflate-1.8             |       h7f8727e_5          51 KB
    libedit-3.1.20221030       |       h5eee18b_0         181 KB
    libevent-2.1.12            |       h8f2d780_0         425 KB
    libllvm10-10.0.1           |       hbcb73fb_5        22.1 MB
    libpq-12.9                 |       h16c4e8d_3         2.1 MB
    libtiff-4.5.0              |       hecacb30_0         528 KB
    libuuid-1.41.5             |       h5eee18b_0          27 KB
    libwebp-1.2.4              |       h11a3e52_0          79 KB
    libwebp-base-1.2.4         |       h5eee18b_0         347 KB
    libxcb-1.15                |       h7f8727e_0         505 KB
    libxkbcommon-1.0.1         |       hfa300c1_0         483 KB
    libxml2-2.9.14             |       h74e7548_0         718 KB
    libxslt-1.1.35             |       h4e12654_0         453 KB
    lxml-4.9.1                 |   py38h1edc446_0         1.3 MB
    lz4-c-1.9.4                |       h6a678d5_0         154 KB
    markupsafe-2.1.1           |   py38h7f8727e_0          21 KB
    matplotlib-inline-0.1.6    |   py38h06a4308_0          16 KB
    mistune-0.8.4              |py38h7b6447c_1000          55 KB
    nbclassic-0.4.8            |   py38h06a4308_0         5.8 MB
    nbclient-0.5.13            |   py38h06a4308_0          91 KB
    nbconvert-6.5.4            |   py38h06a4308_0         513 KB
    nbformat-5.7.0             |   py38h06a4308_0         133 KB
    nest-asyncio-1.5.6         |   py38h06a4308_0          14 KB
    notebook-6.5.2             |   py38h06a4308_0         510 KB
    notebook-shim-0.2.2        |   py38h06a4308_0          22 KB
    nspr-4.33                  |       h295c915_0         222 KB
    nss-3.74                   |       h0370c37_0         1.9 MB
    packaging-22.0             |   py38h06a4308_0          68 KB
    pandocfilters-1.5.0        |     pyhd3eb1b0_0          11 KB
    parso-0.8.3                |     pyhd3eb1b0_0          70 KB
    pkgutil-resolve-name-1.3.10|   py38h06a4308_0           9 KB
    platformdirs-2.5.2         |   py38h06a4308_0          23 KB
    ply-3.11                   |           py38_0          81 KB
    prometheus_client-0.14.1   |   py38h06a4308_0          90 KB
    prompt-toolkit-3.0.36      |   py38h06a4308_0         574 KB
    prompt_toolkit-3.0.36      |       hd3eb1b0_0           5 KB
    psutil-5.9.0               |   py38h5eee18b_0         330 KB
    pure_eval-0.2.2            |     pyhd3eb1b0_0          14 KB
    pygments-2.11.2            |     pyhd3eb1b0_0         759 KB
    pyopenssl-22.0.0           |     pyhd3eb1b0_0          50 KB
    pyqt-5.15.7                |   py38h6a678d5_1         5.1 MB
    pyqt5-sip-12.11.0          |   py38h6a678d5_1          87 KB
    pyrsistent-0.18.0          |   py38heee7806_0          94 KB
    pysocks-1.7.1              |   py38h06a4308_0          31 KB
    python-fastjsonschema-2.16.2|   py38h06a4308_0         230 KB
    pytz-2022.7                |   py38h06a4308_0         209 KB
    pyzmq-23.2.0               |   py38h6a678d5_0         448 KB
    qt-main-5.15.2             |       h327a75a_7        45.1 MB
    qt-webengine-5.15.9        |       hd2b0992_4        47.1 MB
    qtconsole-5.4.0            |   py38h06a4308_0         190 KB
    qtpy-2.2.0                 |   py38h06a4308_0          84 KB
    qtwebkit-5.212             |       h4eab89a_4        14.3 MB
    requests-2.28.1            |   py38h06a4308_0          92 KB
    sip-6.6.2                  |   py38h6a678d5_0         425 KB
    six-1.16.0                 |     pyhd3eb1b0_1          18 KB
    sniffio-1.2.0              |   py38h06a4308_1          15 KB
    soupsieve-2.3.2.post1      |   py38h06a4308_0          65 KB
    stack_data-0.2.0           |     pyhd3eb1b0_0          22 KB
    terminado-0.17.1           |   py38h06a4308_0          31 KB
    tinycss2-1.2.1             |   py38h06a4308_0          40 KB
    toml-0.10.2                |     pyhd3eb1b0_0          20 KB
    tomli-2.0.1                |   py38h06a4308_0          24 KB
    tornado-6.2                |   py38h5eee18b_0         590 KB
    traitlets-5.7.1            |   py38h06a4308_0         200 KB
    typing-extensions-4.4.0    |   py38h06a4308_0           8 KB
    typing_extensions-4.4.0    |   py38h06a4308_0          46 KB
    urllib3-1.26.14            |   py38h06a4308_0         196 KB
    webencodings-0.5.1         |           py38_1          20 KB
    websocket-client-0.58.0    |   py38h06a4308_4          66 KB
    widgetsnbextension-3.5.2   |   py38h06a4308_0         651 KB
    zipp-3.11.0                |   py38h06a4308_0          19 KB
    zstd-1.5.2                 |       ha4553b6_0         488 KB
    ------------------------------------------------------------
                                           Total:       199.0 MB

The following NEW packages will be INSTALLED:

  anyio              pkgs/main/linux-64::anyio-3.5.0-py38h06a4308_0
  argon2-cffi        pkgs/main/noarch::argon2-cffi-21.3.0-pyhd3eb1b0_0
  argon2-cffi-bindi~ pkgs/main/linux-64::argon2-cffi-bindings-21.2.0-py38h7f8727e_0
  asttokens          pkgs/main/noarch::asttokens-2.0.5-pyhd3eb1b0_0
  attrs              pkgs/main/linux-64::attrs-22.1.0-py38h06a4308_0
  babel              pkgs/main/linux-64::babel-2.11.0-py38h06a4308_0
  backcall           pkgs/main/noarch::backcall-0.2.0-pyhd3eb1b0_0
  beautifulsoup4     pkgs/main/linux-64::beautifulsoup4-4.11.1-py38h06a4308_0
  bleach             pkgs/main/noarch::bleach-4.1.0-pyhd3eb1b0_0
  brotlipy           pkgs/main/linux-64::brotlipy-0.7.0-py38h27cfd23_1003
  cffi               pkgs/main/linux-64::cffi-1.15.1-py38h5eee18b_3
  charset-normalizer pkgs/main/noarch::charset-normalizer-2.0.4-pyhd3eb1b0_0
  comm               pkgs/main/linux-64::comm-0.1.2-py38h06a4308_0
  cryptography       pkgs/main/linux-64::cryptography-38.0.4-py38h9ce1e76_0
  dbus               pkgs/main/linux-64::dbus-1.13.18-hb2f20db_0
  debugpy            pkgs/main/linux-64::debugpy-1.5.1-py38h295c915_0
  decorator          pkgs/main/noarch::decorator-5.1.1-pyhd3eb1b0_0
  defusedxml         pkgs/main/noarch::defusedxml-0.7.1-pyhd3eb1b0_0
  entrypoints        pkgs/main/linux-64::entrypoints-0.4-py38h06a4308_0
  executing          pkgs/main/noarch::executing-0.8.3-pyhd3eb1b0_0
  expat              pkgs/main/linux-64::expat-2.4.9-h6a678d5_0
  flit-core          pkgs/main/noarch::flit-core-3.6.0-pyhd3eb1b0_0
  fontconfig         pkgs/main/linux-64::fontconfig-2.14.1-h52c9d5c_1
  freetype           pkgs/main/linux-64::freetype-2.12.1-h4a9f257_0
  giflib             pkgs/main/linux-64::giflib-5.2.1-h5eee18b_1
  glib               pkgs/main/linux-64::glib-2.69.1-he621ea3_2
  gst-plugins-base   pkgs/main/linux-64::gst-plugins-base-1.14.0-h8213a91_2
  gstreamer          pkgs/main/linux-64::gstreamer-1.14.0-h28cd5cc_2
  icu                pkgs/main/linux-64::icu-58.2-he6710b0_3
  idna               pkgs/main/linux-64::idna-3.4-py38h06a4308_0
  importlib-metadata pkgs/main/linux-64::importlib-metadata-4.11.3-py38h06a4308_0
  importlib_resourc~ pkgs/main/noarch::importlib_resources-5.2.0-pyhd3eb1b0_1
  ipykernel          pkgs/main/linux-64::ipykernel-6.19.2-py38hb070fc8_0
  ipython            pkgs/main/linux-64::ipython-8.8.0-py38h06a4308_0
  ipython_genutils   pkgs/main/noarch::ipython_genutils-0.2.0-pyhd3eb1b0_1
  ipywidgets         pkgs/main/noarch::ipywidgets-7.6.5-pyhd3eb1b0_1
  jedi               pkgs/main/linux-64::jedi-0.18.1-py38h06a4308_1
  jinja2             pkgs/main/linux-64::jinja2-3.1.2-py38h06a4308_0
  jpeg               pkgs/main/linux-64::jpeg-9e-h7f8727e_0
  json5              pkgs/main/noarch::json5-0.9.6-pyhd3eb1b0_0
  jsonschema         pkgs/main/linux-64::jsonschema-4.16.0-py38h06a4308_0
  jupyter            pkgs/main/linux-64::jupyter-1.0.0-py38h06a4308_8
  jupyter_client     pkgs/main/linux-64::jupyter_client-7.4.8-py38h06a4308_0
  jupyter_console    pkgs/main/linux-64::jupyter_console-6.4.4-py38h06a4308_0
  jupyter_core       pkgs/main/linux-64::jupyter_core-5.1.1-py38h06a4308_0
  jupyter_server     pkgs/main/linux-64::jupyter_server-1.23.4-py38h06a4308_0
  jupyterlab         pkgs/main/linux-64::jupyterlab-3.5.2-py38h06a4308_0
  jupyterlab_pygmen~ pkgs/main/noarch::jupyterlab_pygments-0.1.2-py_0
  jupyterlab_server  pkgs/main/linux-64::jupyterlab_server-2.16.5-py38h06a4308_0
  jupyterlab_widgets pkgs/main/noarch::jupyterlab_widgets-1.0.0-pyhd3eb1b0_1
  krb5               pkgs/main/linux-64::krb5-1.19.4-h568e23c_0
  lerc               pkgs/main/linux-64::lerc-3.0-h295c915_0
  libclang           pkgs/main/linux-64::libclang-10.0.1-default_hb85057a_2
  libdeflate         pkgs/main/linux-64::libdeflate-1.8-h7f8727e_5
  libedit            pkgs/main/linux-64::libedit-3.1.20221030-h5eee18b_0
  libevent           pkgs/main/linux-64::libevent-2.1.12-h8f2d780_0
  libllvm10          pkgs/main/linux-64::libllvm10-10.0.1-hbcb73fb_5
  libpng             pkgs/main/linux-64::libpng-1.6.37-hbc83047_0
  libpq              pkgs/main/linux-64::libpq-12.9-h16c4e8d_3
  libsodium          pkgs/main/linux-64::libsodium-1.0.18-h7b6447c_0
  libtiff            pkgs/main/linux-64::libtiff-4.5.0-hecacb30_0
  libuuid            pkgs/main/linux-64::libuuid-1.41.5-h5eee18b_0
  libwebp            pkgs/main/linux-64::libwebp-1.2.4-h11a3e52_0
  libwebp-base       pkgs/main/linux-64::libwebp-base-1.2.4-h5eee18b_0
  libxcb             pkgs/main/linux-64::libxcb-1.15-h7f8727e_0
  libxkbcommon       pkgs/main/linux-64::libxkbcommon-1.0.1-hfa300c1_0
  libxml2            pkgs/main/linux-64::libxml2-2.9.14-h74e7548_0
  libxslt            pkgs/main/linux-64::libxslt-1.1.35-h4e12654_0
  lxml               pkgs/main/linux-64::lxml-4.9.1-py38h1edc446_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.4-h6a678d5_0
  markupsafe         pkgs/main/linux-64::markupsafe-2.1.1-py38h7f8727e_0
  matplotlib-inline  pkgs/main/linux-64::matplotlib-inline-0.1.6-py38h06a4308_0
  mistune            pkgs/main/linux-64::mistune-0.8.4-py38h7b6447c_1000
  nbclassic          pkgs/main/linux-64::nbclassic-0.4.8-py38h06a4308_0
  nbclient           pkgs/main/linux-64::nbclient-0.5.13-py38h06a4308_0
  nbconvert          pkgs/main/linux-64::nbconvert-6.5.4-py38h06a4308_0
  nbformat           pkgs/main/linux-64::nbformat-5.7.0-py38h06a4308_0
  nest-asyncio       pkgs/main/linux-64::nest-asyncio-1.5.6-py38h06a4308_0
  notebook           pkgs/main/linux-64::notebook-6.5.2-py38h06a4308_0
  notebook-shim      pkgs/main/linux-64::notebook-shim-0.2.2-py38h06a4308_0
  nspr               pkgs/main/linux-64::nspr-4.33-h295c915_0
  nss                pkgs/main/linux-64::nss-3.74-h0370c37_0
  packaging          pkgs/main/linux-64::packaging-22.0-py38h06a4308_0
  pandocfilters      pkgs/main/noarch::pandocfilters-1.5.0-pyhd3eb1b0_0
  parso              pkgs/main/noarch::parso-0.8.3-pyhd3eb1b0_0
  pcre               pkgs/main/linux-64::pcre-8.45-h295c915_0
  pexpect            pkgs/main/noarch::pexpect-4.8.0-pyhd3eb1b0_3
  pickleshare        pkgs/main/noarch::pickleshare-0.7.5-pyhd3eb1b0_1003
  pkgutil-resolve-n~ pkgs/main/linux-64::pkgutil-resolve-name-1.3.10-py38h06a4308_0
  platformdirs       pkgs/main/linux-64::platformdirs-2.5.2-py38h06a4308_0
  ply                pkgs/main/linux-64::ply-3.11-py38_0
  prometheus_client  pkgs/main/linux-64::prometheus_client-0.14.1-py38h06a4308_0
  prompt-toolkit     pkgs/main/linux-64::prompt-toolkit-3.0.36-py38h06a4308_0
  prompt_toolkit     pkgs/main/noarch::prompt_toolkit-3.0.36-hd3eb1b0_0
  psutil             pkgs/main/linux-64::psutil-5.9.0-py38h5eee18b_0
  ptyprocess         pkgs/main/noarch::ptyprocess-0.7.0-pyhd3eb1b0_2
  pure_eval          pkgs/main/noarch::pure_eval-0.2.2-pyhd3eb1b0_0
  pycparser          pkgs/main/noarch::pycparser-2.21-pyhd3eb1b0_0
  pygments           pkgs/main/noarch::pygments-2.11.2-pyhd3eb1b0_0
  pyopenssl          pkgs/main/noarch::pyopenssl-22.0.0-pyhd3eb1b0_0
  pyqt               pkgs/main/linux-64::pyqt-5.15.7-py38h6a678d5_1
  pyqt5-sip          pkgs/main/linux-64::pyqt5-sip-12.11.0-py38h6a678d5_1
  pyrsistent         pkgs/main/linux-64::pyrsistent-0.18.0-py38heee7806_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38h06a4308_0
  python-dateutil    pkgs/main/noarch::python-dateutil-2.8.2-pyhd3eb1b0_0
  python-fastjsonsc~ pkgs/main/linux-64::python-fastjsonschema-2.16.2-py38h06a4308_0
  pytz               pkgs/main/linux-64::pytz-2022.7-py38h06a4308_0
  pyzmq              pkgs/main/linux-64::pyzmq-23.2.0-py38h6a678d5_0
  qt-main            pkgs/main/linux-64::qt-main-5.15.2-h327a75a_7
  qt-webengine       pkgs/main/linux-64::qt-webengine-5.15.9-hd2b0992_4
  qtconsole          pkgs/main/linux-64::qtconsole-5.4.0-py38h06a4308_0
  qtpy               pkgs/main/linux-64::qtpy-2.2.0-py38h06a4308_0
  qtwebkit           pkgs/main/linux-64::qtwebkit-5.212-h4eab89a_4
  requests           pkgs/main/linux-64::requests-2.28.1-py38h06a4308_0
  send2trash         pkgs/main/noarch::send2trash-1.8.0-pyhd3eb1b0_1
  sip                pkgs/main/linux-64::sip-6.6.2-py38h6a678d5_0
  six                pkgs/main/noarch::six-1.16.0-pyhd3eb1b0_1
  sniffio            pkgs/main/linux-64::sniffio-1.2.0-py38h06a4308_1
  soupsieve          pkgs/main/linux-64::soupsieve-2.3.2.post1-py38h06a4308_0
  stack_data         pkgs/main/noarch::stack_data-0.2.0-pyhd3eb1b0_0
  terminado          pkgs/main/linux-64::terminado-0.17.1-py38h06a4308_0
  tinycss2           pkgs/main/linux-64::tinycss2-1.2.1-py38h06a4308_0
  toml               pkgs/main/noarch::toml-0.10.2-pyhd3eb1b0_0
  tomli              pkgs/main/linux-64::tomli-2.0.1-py38h06a4308_0
  tornado            pkgs/main/linux-64::tornado-6.2-py38h5eee18b_0
  traitlets          pkgs/main/linux-64::traitlets-5.7.1-py38h06a4308_0
  typing-extensions  pkgs/main/linux-64::typing-extensions-4.4.0-py38h06a4308_0
  typing_extensions  pkgs/main/linux-64::typing_extensions-4.4.0-py38h06a4308_0
  urllib3            pkgs/main/linux-64::urllib3-1.26.14-py38h06a4308_0
  wcwidth            pkgs/main/noarch::wcwidth-0.2.5-pyhd3eb1b0_0
  webencodings       pkgs/main/linux-64::webencodings-0.5.1-py38_1
  websocket-client   pkgs/main/linux-64::websocket-client-0.58.0-py38h06a4308_4
  widgetsnbextension pkgs/main/linux-64::widgetsnbextension-3.5.2-py38h06a4308_0
  zeromq             pkgs/main/linux-64::zeromq-4.3.4-h2531618_0
  zipp               pkgs/main/linux-64::zipp-3.11.0-py38h06a4308_0
  zstd               pkgs/main/linux-64::zstd-1.5.2-ha4553b6_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
jupyterlab_server-2. | 80 KB     | ########################################################## | 100% 
glib-2.69.1          | 1.9 MB    | ########################################################## | 100% 
nspr-4.33            | 222 KB    | ########################################################## | 100% 
importlib_resources- | 21 KB     | ########################################################## | 100% 
pkgutil-resolve-name | 9 KB      | ########################################################## | 100% 
packaging-22.0       | 68 KB     | ########################################################## | 100% 
sniffio-1.2.0        | 15 KB     | ########################################################## | 100% 
lz4-c-1.9.4          | 154 KB    | ########################################################## | 100% 
zipp-3.11.0          | 19 KB     | ########################################################## | 100% 
fontconfig-2.14.1    | 281 KB    | ########################################################## | 100% 
prompt-toolkit-3.0.3 | 574 KB    | ########################################################## | 100% 
debugpy-1.5.1        | 1.7 MB    | ########################################################## | 100% 
pandocfilters-1.5.0  | 11 KB     | ########################################################## | 100% 
bleach-4.1.0         | 123 KB    | ########################################################## | 100% 
stack_data-0.2.0     | 22 KB     | ########################################################## | 100% 
pyqt-5.15.7          | 5.1 MB    | ########################################################## | 100% 
freetype-2.12.1      | 626 KB    | ########################################################## | 100% 
libxslt-1.1.35       | 453 KB    | ########################################################## | 100% 
typing_extensions-4. | 46 KB     | ########################################################## | 100% 
argon2-cffi-bindings | 33 KB     | ########################################################## | 100% 
jupyter_client-7.4.8 | 205 KB    | ########################################################## | 100% 
pygments-2.11.2      | 759 KB    | ########################################################## | 100% 
widgetsnbextension-3 | 651 KB    | ########################################################## | 100% 
lerc-3.0             | 196 KB    | ########################################################## | 100% 
libclang-10.0.1      | 10.8 MB   | ########################################################## | 100% 
libxkbcommon-1.0.1   | 483 KB    | ########################################################## | 100% 
soupsieve-2.3.2.post | 65 KB     | ########################################################## | 100% 
nbconvert-6.5.4      | 513 KB    | ########################################################## | 100% 
idna-3.4             | 93 KB     | ########################################################## | 100% 
webencodings-0.5.1   | 20 KB     | ########################################################## | 100% 
tinycss2-1.2.1       | 40 KB     | ########################################################## | 100% 
python-fastjsonschem | 230 KB    | ########################################################## | 100% 
pyqt5-sip-12.11.0    | 87 KB     | ########################################################## | 100% 
babel-2.11.0         | 6.8 MB    | ########################################################## | 100% 
jupyter-1.0.0        | 7 KB      | ########################################################## | 100% 
nest-asyncio-1.5.6   | 14 KB     | ########################################################## | 100% 
libuuid-1.41.5       | 27 KB     | ########################################################## | 100% 
pyzmq-23.2.0         | 448 KB    | ########################################################## | 100% 
entrypoints-0.4      | 16 KB     | ########################################################## | 100% 
matplotlib-inline-0. | 16 KB     | ########################################################## | 100% 
gstreamer-1.14.0     | 3.2 MB    | ########################################################## | 100% 
pyrsistent-0.18.0    | 94 KB     | ########################################################## | 100% 
sip-6.6.2            | 425 KB    | ########################################################## | 100% 
qtconsole-5.4.0      | 190 KB    | ########################################################## | 100% 
qt-webengine-5.15.9  | 47.1 MB   | ########################################################## | 100% 
executing-0.8.3      | 18 KB     | ########################################################## | 100% 
nss-3.74             | 1.9 MB    | ########################################################## | 100% 
brotlipy-0.7.0       | 323 KB    | ########################################################## | 100% 
cffi-1.15.1          | 241 KB    | ########################################################## | 100% 
platformdirs-2.5.2   | 23 KB     | ########################################################## | 100% 
libdeflate-1.8       | 51 KB     | ########################################################## | 100% 
libllvm10-10.0.1     | 22.1 MB   | ########################################################## | 100% 
pure_eval-0.2.2      | 14 KB     | ########################################################## | 100% 
comm-0.1.2           | 13 KB     | ########################################################## | 100% 
libtiff-4.5.0        | 528 KB    | ########################################################## | 100% 
libpq-12.9           | 2.1 MB    | ########################################################## | 100% 
jinja2-3.1.2         | 211 KB    | ########################################################## | 100% 
terminado-0.17.1     | 31 KB     | ########################################################## | 100% 
jupyter_core-5.1.1   | 89 KB     | ########################################################## | 100% 
ipython-8.8.0        | 1.0 MB    | ########################################################## | 100% 
asttokens-2.0.5      | 20 KB     | ########################################################## | 100% 
six-1.16.0           | 18 KB     | ########################################################## | 100% 
decorator-5.1.1      | 12 KB     | ########################################################## | 100% 
importlib-metadata-4 | 40 KB     | ########################################################## | 100% 
prompt_toolkit-3.0.3 | 5 KB      | ########################################################## | 100% 
nbformat-5.7.0       | 133 KB    | ########################################################## | 100% 
attrs-22.1.0         | 85 KB     | ########################################################## | 100% 
nbclient-0.5.13      | 91 KB     | ########################################################## | 100% 
charset-normalizer-2 | 35 KB     | ########################################################## | 100% 
toml-0.10.2          | 20 KB     | ########################################################## | 100% 
libxml2-2.9.14       | 718 KB    | ########################################################## | 100% 
nbclassic-0.4.8      | 5.8 MB    | ########################################################## | 100% 
jpeg-9e              | 240 KB    | ########################################################## | 100% 
notebook-6.5.2       | 510 KB    | ########################################################## | 100% 
libwebp-1.2.4        | 79 KB     | ########################################################## | 100% 
psutil-5.9.0         | 330 KB    | ########################################################## | 100% 
libxcb-1.15          | 505 KB    | ########################################################## | 100% 
jsonschema-4.16.0    | 128 KB    | ########################################################## | 100% 
jupyterlab-3.5.2     | 4.2 MB    | ########################################################## | 100% 
websocket-client-0.5 | 66 KB     | ########################################################## | 100% 
markupsafe-2.1.1     | 21 KB     | ########################################################## | 100% 
urllib3-1.26.14      | 196 KB    | ########################################################## | 100% 
anyio-3.5.0          | 165 KB    | ########################################################## | 100% 
libevent-2.1.12      | 425 KB    | ########################################################## | 100% 
zstd-1.5.2           | 488 KB    | ########################################################## | 100% 
tornado-6.2          | 590 KB    | ########################################################## | 100% 
tomli-2.0.1          | 24 KB     | ########################################################## | 100% 
libedit-3.1.20221030 | 181 KB    | ########################################################## | 100% 
jupyter_console-6.4. | 42 KB     | ########################################################## | 100% 
qt-main-5.15.2       | 45.1 MB   | ########################################################## | 100% 
expat-2.4.9          | 156 KB    | ########################################################## | 100% 
lxml-4.9.1           | 1.3 MB    | ########################################################## | 100% 
flit-core-3.6.0      | 42 KB     | ########################################################## | 100% 
mistune-0.8.4        | 55 KB     | ########################################################## | 100% 
krb5-1.19.4          | 1.3 MB    | ########################################################## | 100% 
pyopenssl-22.0.0     | 50 KB     | ########################################################## | 100% 
qtwebkit-5.212       | 14.3 MB   | ########################################################## | 100% 
argon2-cffi-21.3.0   | 15 KB     | ########################################################## | 100% 
jupyter_server-1.23. | 382 KB    | ########################################################## | 100% 
pysocks-1.7.1        | 31 KB     | ########################################################## | 100% 
ipykernel-6.19.2     | 218 KB    | ########################################################## | 100% 
ply-3.11             | 81 KB     | ########################################################## | 100% 
jedi-0.18.1          | 982 KB    | ########################################################## | 100% 
qtpy-2.2.0           | 84 KB     | ########################################################## | 100% 
giflib-5.2.1         | 75 KB     | ########################################################## | 100% 
json5-0.9.6          | 21 KB     | ########################################################## | 100% 
typing-extensions-4. | 8 KB      | ########################################################## | 100% 
beautifulsoup4-4.11. | 185 KB    | ########################################################## | 100% 
requests-2.28.1      | 92 KB     | ########################################################## | 100% 
notebook-shim-0.2.2  | 22 KB     | ########################################################## | 100% 
prometheus_client-0. | 90 KB     | ########################################################## | 100% 
parso-0.8.3          | 70 KB     | ########################################################## | 100% 
gst-plugins-base-1.1 | 4.9 MB    | ########################################################## | 100% 
pytz-2022.7          | 209 KB    | ########################################################## | 100% 
libwebp-base-1.2.4   | 347 KB    | ########################################################## | 100% 
traitlets-5.7.1      | 200 KB    | ########################################################## | 100% 
cryptography-38.0.4  | 1.4 MB    | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
Retrieving notices: ...working... done
(fs-video-recog) ye@ykt-pro:~/exp$ 
```

Checking the installed Jupyter version and also for your ref:  

```
(fs-video-recog) ye@ykt-pro:~/exp$ jupyter --version
Selected Jupyter core packages...
IPython          : 8.8.0
ipykernel        : 6.19.2
ipywidgets       : 7.6.5
jupyter_client   : 7.4.8
jupyter_core     : 5.1.1
jupyter_server   : 1.23.4
jupyterlab       : 3.5.2
nbclient         : 0.5.13
nbconvert        : 6.5.4
nbformat         : 5.7.0
notebook         : 6.5.2
qtconsole        : 5.4.0
traitlets        : 5.7.1
(fs-video-recog) ye@ykt-pro:~/exp$ 
```

## Prepare ipython Notebook File for Data Collection  

I prepared new ipython notebook for data collection. When I run following function,   

```Python
cap = cv2.VideoCapture(0)
# Set mediapipe model 
with mp_holistic.Holistic(min_detection_confidence=0.5, min_tracking_confidence=0.5) as holistic:
    while cap.isOpened():
```

I got following error:  

```
AttributeError: module 'mediapipe.python.solutions.holistic' has no attribute 'FACE_CONNECTIONS'
```

I also noted that tensorflow cpu version was created as following message:  

```
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
```

I am not sure and anyway, I installed tensorflow (i.e. CPU) version as follows on my notebook:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip install tensorflow
Collecting tensorflow
  Using cached tensorflow-2.11.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (588.3 MB)
Collecting tensorflow-estimator<2.12,>=2.11.0
  Using cached tensorflow_estimator-2.11.0-py2.py3-none-any.whl (439 kB)
Collecting astunparse>=1.6.0
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting protobuf<3.20,>=3.9.2
  Using cached protobuf-3.19.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting google-pasta>=0.1.1
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Requirement already satisfied: packaging in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (23.0)
Collecting tensorboard<2.12,>=2.11
  Downloading tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.0/6.0 MB 2.9 MB/s eta 0:00:00
Collecting termcolor>=1.1.0
  Downloading termcolor-2.2.0-py3-none-any.whl (6.6 kB)
Collecting keras<2.12,>=2.11.0
  Using cached keras-2.11.0-py2.py3-none-any.whl (1.7 MB)
Requirement already satisfied: setuptools in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (65.6.3)
Requirement already satisfied: flatbuffers>=2.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (23.1.21)
Requirement already satisfied: typing-extensions>=3.6.6 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (4.4.0)
Collecting wrapt>=1.11.0
  Using cached wrapt-1.14.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (81 kB)
Collecting h5py>=2.9.0
  Downloading h5py-3.8.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.7/4.7 MB 3.1 MB/s eta 0:00:00
Collecting libclang>=13.0.0
  Downloading libclang-15.0.6.1-py2.py3-none-manylinux2010_x86_64.whl (21.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 21.5/21.5 MB 2.5 MB/s eta 0:00:00
Collecting tensorflow-io-gcs-filesystem>=0.23.1
  Downloading tensorflow_io_gcs_filesystem-0.30.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (2.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.4/2.4 MB 3.6 MB/s eta 0:00:00
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting grpcio<2.0,>=1.24.3
  Using cached grpcio-1.51.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.8 MB)
Requirement already satisfied: six>=1.12.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (1.16.0)
Requirement already satisfied: numpy>=1.20 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (1.24.1)
Collecting gast<=0.4.0,>=0.2.1
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Requirement already satisfied: absl-py>=1.0.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorflow) (1.4.0)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from astunparse>=1.6.0->tensorflow) (0.37.1)
Requirement already satisfied: requests<3,>=2.21.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.28.1)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.16.0-py2.py3-none-any.whl (177 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 177.8/177.8 kB 5.1 MB/s eta 0:00:00
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.4.1-py3-none-any.whl (93 kB)
Collecting werkzeug>=1.0.1
  Using cached Werkzeug-2.2.2-py3-none-any.whl (232 kB)
Collecting rsa<5,>=3.1.4
  Using cached rsa-4.9-py3-none-any.whl (34 kB)
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.3.0-py3-none-any.whl (9.3 kB)
Collecting pyasn1-modules>=0.2.1
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Requirement already satisfied: importlib-metadata>=4.4 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (4.11.3)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (2022.12.7)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (3.4)
Requirement already satisfied: charset-normalizer<3,>=2 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (2.0.4)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (1.26.14)
Requirement already satisfied: MarkupSafe>=2.1.1 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from werkzeug>=1.0.1->tensorboard<2.12,>=2.11->tensorflow) (2.1.1)
Requirement already satisfied: zipp>=0.5 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (3.11.0)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.2.2-py3-none-any.whl (151 kB)
Installing collected packages: tensorboard-plugin-wit, pyasn1, libclang, wrapt, werkzeug, termcolor, tensorflow-io-gcs-filesystem, tensorflow-estimator, tensorboard-data-server, rsa, pyasn1-modules, protobuf, opt-einsum, oauthlib, keras, h5py, grpcio, google-pasta, gast, cachetools, astunparse, requests-oauthlib, markdown, google-auth, google-auth-oauthlib, tensorboard, tensorflow
  Attempting uninstall: protobuf
    Found existing installation: protobuf 3.20.3
    Uninstalling protobuf-3.20.3:
      Successfully uninstalled protobuf-3.20.3
Successfully installed astunparse-1.6.3 cachetools-5.3.0 gast-0.4.0 google-auth-2.16.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.51.1 h5py-3.8.0 keras-2.11.0 libclang-15.0.6.1 markdown-3.4.1 oauthlib-3.2.2 opt-einsum-3.3.0 protobuf-3.19.6 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-oauthlib-1.3.1 rsa-4.9 tensorboard-2.11.2 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.11.0 tensorflow-estimator-2.11.0 tensorflow-io-gcs-filesystem-0.30.0 termcolor-2.2.0 werkzeug-2.2.2 wrapt-1.14.1
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

## Re-run the 1st Notebook

I restarted the jupyter notebook and re-run the 1st notebook and I got the same error as follows:  

```
AttributeError: module 'mediapipe.python.solutions.holistic' has no attribute 'FACE_CONNECTIONS'
```

Googling and try to fixed above error.  
Reference link:  https://stackoverflow.com/questions/69095372/attributeerror-module-mediapipe-python-solutions-holistic-has-no-attribute-f  

```
FACE_CONNECTIONS seems to be renamed/replaced by FACEMESH_TESSELATION.
```

I updated the code as follows:  

```Python
# I updated FACE_CONNECTIONS with FACEMESH_TESSELATION
def draw_landmarks(image, results):
    mp_drawing.draw_landmarks(image, results.face_landmarks, mp_holistic.FACEMESH_TESSELATION) # Draw face connections
    mp_drawing.draw_landmarks(image, results.pose_landmarks, mp_holistic.POSE_CONNECTIONS) # Draw pose connections
    mp_drawing.draw_landmarks(image, results.left_hand_landmarks, mp_holistic.HAND_CONNECTIONS) # Draw left hand connections
    mp_drawing.draw_landmarks(image, results.right_hand_landmarks, mp_holistic.HAND_CONNECTIONS) # Draw right hand connections
```

I updated another python code as follows:  

```Python
def draw_styled_landmarks(image, results):
    # Draw face connections
    # I updated FACE_CONNECTIONS with FACEMESH_TESSELATION
    mp_drawing.draw_landmarks(image, results.face_landmarks, mp_holistic.FACEMESH_TESSELATION, 
                             mp_drawing.DrawingSpec(color=(80,110,10), thickness=1, circle_radius=1), 
                             mp_drawing.DrawingSpec(color=(80,256,121), thickness=1, circle_radius=1)
                             ) 
    # Draw pose connections
    mp_drawing.draw_landmarks(image, results.pose_landmarks, mp_holistic.POSE_CONNECTIONS,
                             mp_drawing.DrawingSpec(color=(80,22,10), thickness=2, circle_radius=4), 
                             mp_drawing.DrawingSpec(color=(80,44,121), thickness=2, circle_radius=2)
                             ) 
    # Draw left hand connections
    mp_drawing.draw_landmarks(image, results.left_hand_landmarks, mp_holistic.HAND_CONNECTIONS, 
                             mp_drawing.DrawingSpec(color=(121,22,76), thickness=2, circle_radius=4), 
                             mp_drawing.DrawingSpec(color=(121,44,250), thickness=2, circle_radius=2)
                             ) 
    # Draw right hand connections  
    mp_drawing.draw_landmarks(image, results.right_hand_landmarks, mp_holistic.HAND_CONNECTIONS, 
                             mp_drawing.DrawingSpec(color=(245,117,66), thickness=2, circle_radius=4), 
                             mp_drawing.DrawingSpec(color=(245,66,230), thickness=2, circle_radius=2)
                             ) 
```

After updating with above code, run and now I can see mediapipe landmark detection points ...  

## Relating to np.save()

After you run the following code inside Jupyter notebook:  

```Python
np.save('0', result_test)
```

It will save as file ...  

```
(base) ye@ykt-pro:~/exp/fs-detection$ ls
0.npy  1.data-preparation.ipynb  note.txt
(base) ye@ykt-pro:~/exp/fs-detection$ 
```

Yes, it is a binary data file as follows:  

```
(base) ye@ykt-pro:~/exp/fs-detection$ file 0.npy 
0.npy: data
(base) ye@ykt-pro:~/exp/fs-detection$ 
```

After I run folder building bash script:  

```
(base) ye@ykt-pro:~/exp/fs-detection$ tree ./fs_data/
./fs_data/
├── ង
├── ក
├── គ
├── ខ
└── ឃ

5 directories, 0 files
(base) ye@ykt-pro:~/exp/fs-detection$ 

```

## MTS to MP4 Video Conversion

This is preprocessing. I learned Khmer 5 fingerspelling with MTS video but I cannot play MTS on linux machine.  
And thus, I need to convert it to mp4 and I did with ffmpeg linux command as follows:  

```
(base) ye@ykt-pro:~/exp/fs-detection/ref-video$ ls
00152.MTS
(base) ye@ykt-pro:~/exp/fs-detection/ref-video$ ffmpeg -i 00152.MTS -c:v copy -c:a aac -strict experimental -b:a 128k 00152.mp4
ffmpeg version 3.4.11-0ubuntu0.1 Copyright (c) 2000-2022 the FFmpeg developers
  built with gcc 7 (Ubuntu 7.5.0-3ubuntu1~18.04)
  configuration: --prefix=/usr --extra-version=0ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --enable-gpl --disable-stripping --enable-avresample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-librsvg --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libopencv --enable-libx264 --enable-shared
  libavutil      55. 78.100 / 55. 78.100
  libavcodec     57.107.100 / 57.107.100
  libavformat    57. 83.100 / 57. 83.100
  libavdevice    57. 10.100 / 57. 10.100
  libavfilter     6.107.100 /  6.107.100
  libavresample   3.  7.  0 /  3.  7.  0
  libswscale      4.  8.100 /  4.  8.100
  libswresample   2.  9.100 /  2.  9.100
  libpostproc    54.  7.100 / 54.  7.100
Input #0, mpegts, from '00152.MTS':
  Duration: 00:01:56.48, start: 1.040000, bitrate: 24029 kb/s
  Program 1 
    Stream #0:0[0x1011]: Video: h264 (High) (HDMV / 0x564D4448), yuv420p(top first), 1920x1080 [SAR 1:1 DAR 16:9], 25 fps, 50 tbr, 90k tbn, 50 tbc
    Stream #0:1[0x1100]: Audio: pcm_bluray (HDMV / 0x564D4448), 48000 Hz, stereo, s16, 1536 kb/s
    Stream #0:2[0x1200]: Subtitle: hdmv_pgs_subtitle ([144][0][0][0] / 0x0090), 1920x1080
Stream mapping:
  Stream #0:0 -> #0:0 (copy)
  Stream #0:1 -> #0:1 (pcm_bluray (native) -> aac (native))
Press [q] to stop, [?] for help
Output #0, mp4, to '00152.mp4':
  Metadata:
    encoder         : Lavf57.83.100
    Stream #0:0: Video: h264 (High) (avc1 / 0x31637661), yuv420p(top first), 1920x1080 [SAR 1:1 DAR 16:9], q=2-31, 25 fps, 50 tbr, 90k tbn, 90k tbc
    Stream #0:1: Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s
    Metadata:
      encoder         : Lavc57.107.100 aac
frame= 5824 fps=1303 q=-1.0 Lsize=  301677kB time=00:01:56.48 bitrate=21216.8kbits/s speed=26.1x    
video:299733kB audio:1825kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.039325%
[aac @ 0x5622f8afb760] Qavg: 646.826
(base) ye@ykt-pro:~/exp/fs-detection/ref-video$ ls
00152.mp4  00152.MTS
(base) ye@ykt-pro:~/exp/fs-detection/ref-video$ 
```

I was stack in following code:  

```python
#The following code got an error
for action in actions: 
    dirmax = np.max(np.array(os.listdir(os.path.join(DATA_PATH, action))).astype(int))
    for sequence in range(1,no_sequences+1):
        try: 
            os.makedirs(os.path.join(DATA_PATH, action, str(dirmax+sequence)))
        except:
            pass
```

And thus, I used the code from the Tutorial (i.e. not updated one):  

```
for action in actions: 
    for sequence in range(1,no_sequences+1):
        try: 
            os.makedirs(os.path.join(DATA_PATH, action, str(sequence)))
        except:
            pass
```

One more problem is when I try to start data collection, both of the source code (from the original Tutorial video and also the updated one) give an error and I have to wait for the long time ... 
I got following errors:  

```
QObject::moveToThread: Current thread (0x2e84730) is not the object's thread (0x2eddfb0).
Cannot move to target thread (0x2e84730)

QObject::moveToThread: Current thread (0x2e84730) is not the object's thread (0x2eddfb0).
Cannot move to target thread (0x2e84730)

QObject::moveToThread: Current thread (0x2e84730) is not the object's thread (0x2eddfb0).
Cannot move to target thread (0x2e84730)

...
...

```

Google the above error and I got following link:  

https://stackoverflow.com/questions/52337870/python-opencv-error-current-thread-is-not-the-objects-thread  

From the above link last answer, I tried to remove the opencv and install headless version as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip uninstall opencv-python
Found existing installation: opencv-python 4.7.0.68
Uninstalling opencv-python-4.7.0.68:
  Would remove:
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/*
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python-4.7.0.68.dist-info/*
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Core-b6e66ee2.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Gui-dd62182f.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Test-c38a5234.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Widgets-e69d94fb.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5XcbQpa-dcb826d0.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libX11-xcb-69166bdf.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libXau-00ec42fe.so.6.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavcodec-087c3416.so.59.37.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavformat-85e01647.so.59.27.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavutil-82c407cb.so.57.28.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libcrypto-9cee340d.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libgfortran-91cc3cb1.so.3.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libopenblas-r0-f650aae0.3.3.so
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libpng16-186fce2e.so.16.37.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libquadmath-96973f99.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libssl-16e42f2f.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libswresample-d02fa90a.so.4.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libswscale-9b504c0d.so.6.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libvpx-5d0a9e1a.so.7.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-icccm-413c9f41.so.4.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-image-e82a276d.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-keysyms-21015570.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-randr-a96a5a87.so.0.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-render-637b984a.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-render-util-43ce00f5.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-shape-25c2b258.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-shm-7a199f70.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-sync-89374f40.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-util-4d666913.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xfixes-9be3ba6f.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xinerama-ae147f87.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xkb-9ba31ab3.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxkbcommon-71ae2972.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxkbcommon-x11-c65ed502.so.0.0.0
Proceed (Y/n)? Y
  Successfully uninstalled opencv-python-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

Install the headless version:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip install opencv-python-headless
Collecting opencv-python-headless
  Downloading opencv_python_headless-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (49.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 49.2/49.2 MB 2.4 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.17.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from opencv-python-headless) (1.24.1)
Installing collected packages: opencv-python-headless
Successfully installed opencv-python-headless-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

After installation, when I restart conda env, restart jupyter and run the source and I got following error at the OpenCV detection stage ...  

```
<class 'mediapipe.python.solution_base.SolutionOutputs'>
---------------------------------------------------------------------------
error                                     Traceback (most recent call last)
Cell In[8], line 17
     14 draw_styled_landmarks(image, results)
     16 # Show to screen
---> 17 cv2.imshow('OpenCV Feed', image)
     19 # Break gracefully
     20 if cv2.waitKey(10) & 0xFF == ord('q'):

error: OpenCV(4.7.0) /io/opencv/modules/highgui/src/window.cpp:1272: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Cocoa support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvShowImage'
```

headless installation is not working?! I try to solve based on the following link:  

https://stackoverflow.com/questions/67120450/error-2unspecified-error-the-function-is-not-implemented-rebuild-the-libra

Uninstall headless version as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip uninstall opencv-python-headless -y
Found existing installation: opencv-python-headless 4.7.0.68
Uninstalling opencv-python-headless-4.7.0.68:
  Successfully uninstalled opencv-python-headless-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

Install/Update as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip install opencv-python --upgrade
Collecting opencv-python
  Using cached opencv_python-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (61.8 MB)
Requirement already satisfied: numpy>=1.17.0 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from opencv-python) (1.24.1)
Installing collected packages: opencv-python
Successfully installed opencv-python-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

And then, rerun Jupyter and rerun the notebook again, detection testing stage is OK, but when I prepare to collect online data I got the same error as follows:  

```
QObject::moveToThread: Current thread (0x225ba00) is not the object's thread (0x24faba0).
Cannot move to target thread (0x225ba00)

QObject::moveToThread: Current thread (0x225ba00) is not the object's thread (0x24faba0).
Cannot move to target thread (0x225ba00)

QObject::moveToThread: Current thread (0x225ba00) is not the object's thread (0x24faba0).
Cannot move to target thread (0x225ba00)
```

Check the OpenCV current versions:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip list | grep opencv
opencv-contrib-python        4.7.0.68
opencv-python                4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

I installed the opencv-headless version:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip install opencv-python-headless
Collecting opencv-python-headless
  Using cached opencv_python_headless-4.7.0.68-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (49.2 MB)
Requirement already satisfied: numpy>=1.17.3 in /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages (from opencv-python-headless) (1.24.1)
Installing collected packages: opencv-python-headless
Successfully installed opencv-python-headless-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

Now, on my conda env, as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip list | grep opencv
opencv-contrib-python        4.7.0.68
opencv-python                4.7.0.68
opencv-python-headless       4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

When I deactivate, activate the conda env, rerun jupyter notebook and run the python notebook, I got following new error:  

```
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
<class 'mediapipe.python.solution_base.SolutionOutputs'>
---------------------------------------------------------------------------
error                                     Traceback (most recent call last)
Cell In[8], line 17
     14 draw_styled_landmarks(image, results)
     16 # Show to screen
---> 17 cv2.imshow('OpenCV Feed', image)
     19 # Break gracefully
     20 if cv2.waitKey(10) & 0xFF == ord('q'):

error: OpenCV(4.7.0) /io/opencv/modules/highgui/src/window.cpp:1272: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Cocoa support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvShowImage'
```

I removed opencv and made clean installation with conda as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip uninstall opencv-python
Found existing installation: opencv-python 4.7.0.68
Uninstalling opencv-python-4.7.0.68:
  Would remove:
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSans-Bold.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSans-BoldOblique.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSans-ExtraLight.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSans-Oblique.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSans.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSansCondensed-Bold.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSansCondensed-BoldOblique.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSansCondensed-Oblique.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/fonts/DejaVuSansCondensed.ttf
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/cv2/qt/plugins/platforms/libqxcb.so
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python-4.7.0.68.dist-info/*
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Core-b6e66ee2.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Gui-dd62182f.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Test-c38a5234.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5Widgets-e69d94fb.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libQt5XcbQpa-dcb826d0.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libX11-xcb-69166bdf.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libXau-00ec42fe.so.6.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavcodec-087c3416.so.59.37.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavformat-85e01647.so.59.27.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libavutil-82c407cb.so.57.28.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libcrypto-9cee340d.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libgfortran-91cc3cb1.so.3.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libopenblas-r0-f650aae0.3.3.so
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libpng16-186fce2e.so.16.37.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libquadmath-96973f99.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libssl-16e42f2f.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libswresample-d02fa90a.so.4.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libswscale-9b504c0d.so.6.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libvpx-5d0a9e1a.so.7.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-icccm-413c9f41.so.4.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-image-e82a276d.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-keysyms-21015570.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-randr-a96a5a87.so.0.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-render-637b984a.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-render-util-43ce00f5.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-shape-25c2b258.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-shm-7a199f70.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-sync-89374f40.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-util-4d666913.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xfixes-9be3ba6f.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xinerama-ae147f87.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxcb-xkb-9ba31ab3.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxkbcommon-71ae2972.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_python.libs/libxkbcommon-x11-c65ed502.so.0.0.0
Proceed (Y/n)? Y
  Successfully uninstalled opencv-python-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$
```

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ pip uninstall opencv-contrib-python
Found existing installation: opencv-contrib-python 4.7.0.68
Uninstalling opencv-contrib-python-4.7.0.68:
  Would remove:
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python-4.7.0.68.dist-info/*
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libQt5Core-b6e66ee2.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libQt5Gui-dd62182f.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libQt5Test-c38a5234.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libQt5Widgets-e69d94fb.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libQt5XcbQpa-dcb826d0.so.5.15.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libX11-xcb-69166bdf.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libXau-00ec42fe.so.6.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libavcodec-087c3416.so.59.37.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libavformat-85e01647.so.59.27.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libavutil-82c407cb.so.57.28.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libcrypto-9cee340d.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libgfortran-91cc3cb1.so.3.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libopenblas-r0-f650aae0.3.3.so
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libpng16-186fce2e.so.16.37.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libquadmath-96973f99.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libssl-16e42f2f.so.1.1
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libswresample-d02fa90a.so.4.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libswscale-9b504c0d.so.6.7.100
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libvpx-5d0a9e1a.so.7.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-icccm-413c9f41.so.4.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-image-e82a276d.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-keysyms-21015570.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-randr-a96a5a87.so.0.1.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-render-637b984a.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-render-util-43ce00f5.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-shape-25c2b258.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-shm-7a199f70.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-sync-89374f40.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-util-4d666913.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-xfixes-9be3ba6f.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-xinerama-ae147f87.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxcb-xkb-9ba31ab3.so.1.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxkbcommon-71ae2972.so.0.0.0
    /home/ye/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/opencv_contrib_python.libs/libxkbcommon-x11-c65ed502.so.0.0.0
Proceed (Y/n)? Y
  Successfully uninstalled opencv-contrib-python-4.7.0.68
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ conda install -c conda-forge opencv
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.14.0
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/fs-video-recog

  added / updated specs:
    - opencv


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    blas-1.0                   |         openblas          46 KB
    bzip2-1.0.8                |       h7f98852_4         484 KB  conda-forge
    ca-certificates-2022.12.7  |       ha878542_0         143 KB  conda-forge
    cairo-1.16.0               |       hb05425b_3         1.2 MB
    certifi-2022.12.7          |     pyhd8ed1ab_0         147 KB  conda-forge
    eigen-3.4.0                |       h4bd325d_0         1.2 MB  conda-forge
    ffmpeg-4.2.2               |       h20bf706_0        59.6 MB
    gmp-6.2.1                  |       h58526e2_0         806 KB  conda-forge
    gnutls-3.6.13              |       h85f3911_1         2.0 MB  conda-forge
    graphite2-1.3.14           |       h295c915_1          97 KB
    harfbuzz-4.3.0             |       hd55b92a_0         1.1 MB
    hdf5-1.10.6                |       h3ffc7dd_1         3.6 MB
    lame-3.100                 |    h7f98852_1001         496 KB  conda-forge
    libblas-3.9.0              |15_linux64_openblas          12 KB  conda-forge
    libcblas-3.9.0             |15_linux64_openblas          12 KB  conda-forge
    libgfortran-ng-12.2.0      |      h69a702a_19          22 KB  conda-forge
    libgfortran5-12.2.0        |      h337968e_19         1.8 MB  conda-forge
    liblapack-3.9.0            |15_linux64_openblas          12 KB  conda-forge
    libopenblas-0.3.20         |pthreads_h78a6416_0        10.1 MB  conda-forge
    libopus-1.3.1              |       h7f98852_1         255 KB  conda-forge
    libprotobuf-3.20.1         |       h4ff587b_0         2.1 MB
    nettle-3.6                 |       he412f7d_0         6.5 MB  conda-forge
    numpy-1.22.3               |   py38h99721a1_2         6.8 MB  conda-forge
    opencv-4.6.0               |   py38hd653453_2        26.8 MB
    openh264-2.1.1             |       h4ff587b_0         711 KB
    pixman-0.40.0              |       h36c2ea0_0         627 KB  conda-forge
    python_abi-3.8             |           2_cp38           4 KB  conda-forge
    x264-1!157.20191217        |       h7b6447c_0         922 KB
    ------------------------------------------------------------
                                           Total:       127.4 MB

The following NEW packages will be INSTALLED:

  blas               pkgs/main/linux-64::blas-1.0-openblas
  bzip2              conda-forge/linux-64::bzip2-1.0.8-h7f98852_4
  cairo              pkgs/main/linux-64::cairo-1.16.0-hb05425b_3
  eigen              conda-forge/linux-64::eigen-3.4.0-h4bd325d_0
  ffmpeg             pkgs/main/linux-64::ffmpeg-4.2.2-h20bf706_0
  gmp                conda-forge/linux-64::gmp-6.2.1-h58526e2_0
  gnutls             conda-forge/linux-64::gnutls-3.6.13-h85f3911_1
  graphite2          pkgs/main/linux-64::graphite2-1.3.14-h295c915_1
  harfbuzz           pkgs/main/linux-64::harfbuzz-4.3.0-hd55b92a_0
  hdf5               pkgs/main/linux-64::hdf5-1.10.6-h3ffc7dd_1
  lame               conda-forge/linux-64::lame-3.100-h7f98852_1001
  libblas            conda-forge/linux-64::libblas-3.9.0-15_linux64_openblas
  libcblas           conda-forge/linux-64::libcblas-3.9.0-15_linux64_openblas
  libgfortran-ng     conda-forge/linux-64::libgfortran-ng-12.2.0-h69a702a_19
  libgfortran5       conda-forge/linux-64::libgfortran5-12.2.0-h337968e_19
  liblapack          conda-forge/linux-64::liblapack-3.9.0-15_linux64_openblas
  libopenblas        conda-forge/linux-64::libopenblas-0.3.20-pthreads_h78a6416_0
  libopus            conda-forge/linux-64::libopus-1.3.1-h7f98852_1
  libprotobuf        pkgs/main/linux-64::libprotobuf-3.20.1-h4ff587b_0
  libvpx             pkgs/main/linux-64::libvpx-1.7.0-h439df22_0
  nettle             conda-forge/linux-64::nettle-3.6-he412f7d_0
  numpy              conda-forge/linux-64::numpy-1.22.3-py38h99721a1_2
  opencv             pkgs/main/linux-64::opencv-4.6.0-py38hd653453_2
  openh264           pkgs/main/linux-64::openh264-2.1.1-h4ff587b_0
  openjpeg           pkgs/main/linux-64::openjpeg-2.4.0-h3ad879b_0
  pixman             conda-forge/linux-64::pixman-0.40.0-h36c2ea0_0
  python_abi         conda-forge/linux-64::python_abi-3.8-2_cp38
  x264               pkgs/main/linux-64::x264-1!157.20191217-h7b6447c_0

The following packages will be SUPERSEDED by a higher-priority channel:

  ca-certificates    pkgs/main::ca-certificates-2023.01.10~ --> conda-forge::ca-certificates-2022.12.7-ha878542_0
  certifi            pkgs/main/linux-64::certifi-2022.12.7~ --> conda-forge/noarch::certifi-2022.12.7-pyhd8ed1ab_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
openh264-2.1.1       | 711 KB    | ########################################################## | 100% 
gmp-6.2.1            | 806 KB    | ########################################################## | 100% 
libopus-1.3.1        | 255 KB    | ########################################################## | 100% 
numpy-1.22.3         | 6.8 MB    | ########################################################## | 100% 
cairo-1.16.0         | 1.2 MB    | ########################################################## | 100% 
x264-1!157.20191217  | 922 KB    | ########################################################## | 100% 
libopenblas-0.3.20   | 10.1 MB   | ########################################################## | 100% 
certifi-2022.12.7    | 147 KB    | ########################################################## | 100% 
bzip2-1.0.8          | 484 KB    | ########################################################## | 100% 
eigen-3.4.0          | 1.2 MB    | ########################################################## | 100% 
gnutls-3.6.13        | 2.0 MB    | ########################################################## | 100% 
libgfortran5-12.2.0  | 1.8 MB    | ########################################################## | 100% 
hdf5-1.10.6          | 3.6 MB    | ########################################################## | 100% 
graphite2-1.3.14     | 97 KB     | ########################################################## | 100% 
opencv-4.6.0         | 26.8 MB   | ########################################################## | 100% 
liblapack-3.9.0      | 12 KB     | ########################################################## | 100% 
harfbuzz-4.3.0       | 1.1 MB    | ########################################################## | 100% 
libcblas-3.9.0       | 12 KB     | ########################################################## | 100% 
pixman-0.40.0        | 627 KB    | ########################################################## | 100% 
ffmpeg-4.2.2         | 59.6 MB   | ########################################################## | 100% 
libblas-3.9.0        | 12 KB     | ########################################################## | 100% 
lame-3.100           | 496 KB    | ########################################################## | 100% 
python_abi-3.8       | 4 KB      | ########################################################## | 100% 
ca-certificates-2022 | 143 KB    | ########################################################## | 100% 
libprotobuf-3.20.1   | 2.1 MB    | ########################################################## | 100% 
libgfortran-ng-12.2. | 22 KB     | ########################################################## | 100% 
blas-1.0             | 46 KB     | ########################################################## | 100% 
nettle-3.6           | 6.5 MB    | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
Retrieving notices: ...working... done
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

current opencv information is as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ conda list | grep opencv
opencv                    4.6.0            py38hd653453_2  
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

Currently, I am facing with following error:  

```
[ WARN:0@66.378] global /opt/conda/conda-bld/opencv-suite_1664548337286/work/modules/videoio/src/cap_gstreamer.cpp (862) isPipelinePlaying OpenCV | GStreamer warning: GStreamer: pipeline have not been created
---------------------------------------------------------------------------
FileNotFoundError                         Traceback (most recent call last)
Cell In[29], line 40
     38 keypoints = extract_keypoints(results)
     39 npy_path = os.path.join(DATA_PATH, action, str(sequence), str(frame_num))
---> 40 np.save(npy_path, keypoints)
     42 # Break gracefully
     43 if cv2.waitKey(10) & 0xFF == ord('q'):

File <__array_function__ internals>:180, in save(*args, **kwargs)

File ~/tool/anaconda3/envs/fs-video-recog/lib/python3.8/site-packages/numpy/lib/npyio.py:515, in save(file, arr, allow_pickle, fix_imports)
    513     if not file.endswith('.npy'):
    514         file = file + '.npy'
--> 515     file_ctx = open(file, "wb")
    517 with file_ctx as fid:
    518     arr = np.asanyarray(arr)

FileNotFoundError: [Errno 2] No such file or directory: 'fs_data/ka/31/0.npy'
```

I found that 31 also an error in the looping code ...  

Finally, I can solve the error, note I also updated the "start_folder = 1" and my OpenCV version on local notebook is as follows:  

```
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ conda list | grep opencv
opencv                    4.6.0            py38hd653453_2  
(fs-video-recog) ye@ykt-pro:~/exp/fs-detection$ 
```

I did data collection for the Khmer consonant Ka to Ngo (i.e. 1st five consonants of Khmer language).  


## Copy Data to GPU Server

```
(base) ye@ykt-pro:~$ scp -r -P xxxx -i /home/ye/.ssh/for-cadt-gpu/id_rsa yekyaw.thu@103.16.63.233  /home/ye/exp/fs-detection/fs_data yekyaw.thu@103.16.63.233:/home/yekyaw.thu/exp/fs-detection/
...
...
...
15.npy                                                             100%   13KB   1.2MB/s   00:00    
6.npy                                                              100%   13KB   1.1MB/s   00:00    
9.npy                                                              100%   13KB 973.0KB/s   00:00    
28.npy                                                             100%   13KB 977.3KB/s   00:00    
22.npy                                                             100%   13KB   1.7MB/s   00:00    
5.npy                                                              100%   13KB   1.8MB/s   00:00    
20.npy                                                             100%   13KB   1.9MB/s   00:00    
21.npy                                                             100%   13KB   2.0MB/s   00:00    
26.npy                                                             100%   13KB   1.4MB/s   00:00    
18.npy                                                             100%   13KB   1.8MB/s   00:00    
0.npy                                                              100%   13KB   2.0MB/s   00:00    
4.npy                                                              100%   13KB   1.4MB/s   00:00    
11.npy                                                             100%   13KB   1.9MB/s   00:00    
12.npy                                                             100%   13KB   1.8MB/s   00:00    
29.npy                                                             100%   13KB   1.6MB/s   00:00    
3.npy                                                              100%   13KB   2.1MB/s   00:00    
13.npy                                                             100%   13KB   2.2MB/s   00:00    
1.npy                                                              100%   13KB   2.1MB/s   00:00    
17.npy                                                             100%   13KB   1.4MB/s   00:00    
24.npy                                                             100%   13KB   2.0MB/s   00:00    
23.npy                                                             100%   13KB   1.8MB/s   00:00    
16.npy                                                             100%   13KB   2.1MB/s   00:00    
8.npy                                                              100%   13KB   1.9MB/s   00:00    
2.npy                                                              100%   13KB   2.0MB/s   00:00    
10.npy                                                             100%   13KB   2.1MB/s   00:00    
19.npy                                                             100%   13KB   1.9MB/s   00:00    
25.npy                                                             100%   13KB   1.9MB/s   00:00    
```

Check on server side:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$ ls
check-tensorflow-gpu.py  khmer-fingerspelling-detection-eg.ipynb  run-jupyter-on-server.sh
fs_data			 ref
(sl-mnist) yekyaw.thu@gpu:~/exp/fs-detection$
```

Run jupyter notebook on server side.  

After that port forwarding on the local notebook computer and update the jupyter notebook for preparing training/test and labels etc.   


## Training

```
(base) yekyaw.thu@gpu:~/exp/fs-detection$ wc kh-fs-5-consonant-2000epoch.h5 
  21193  121985 7226328 kh-fs-5-consonant-2000epoch.h5
```

## Summary

I splitted the original ipython notebook file into three parts and they are as follows:  
  File1: 1.data-preparation.ipynb  (run onou your notebook)  
  File2: 2.training-lstm.ipynb  (run on your GPU server)  
  File3: 3.real-time-test.ipynb  (run on your notebook)  

The link for the notebooks:[https://github.com/ye-kyaw-thu/error-overflow/tree/master/kh-sl-detection](https://github.com/ye-kyaw-thu/error-overflow/tree/master/kh-sl-detection)  
Before your run, you have to prepare required libraries on both of your local notebook and GPU server.  

## To Do

1. Training with 600 recorded fingerspelling words video data  
2. Hyperparameter tuning with current LSTM model  
3. Updating current LSTM network architecture 
4. Considering other neural network architecture such as Transformer  

## Reference

[1]. https://stackoverflow.com/questions/69095372/attributeerror-module-mediapipe-python-solutions-holistic-has-no-attribute-f
[2] https://datascience.stackexchange.com/questions/110484/attributeerror-nonetype-object-has-no-attribute-landmark
[3] https://stackoverflow.com/questions/52337870/python-opencv-error-current-thread-is-not-the-objects-thread
[4] https://stackoverflow.com/questions/67120450/error-2unspecified-error-the-function-is-not-implemented-rebuild-the-libra
[5] https://www.quora.com/How-do-I-fix-the-attribute-error-module-cv2-has-no-attribute-video-capture

