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
